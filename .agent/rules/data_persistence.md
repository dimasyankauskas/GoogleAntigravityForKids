# Data Persistence Protocol

> Every app that involves user data MUST persist data to disk using the Vite server middleware pattern. Data must survive browser clears, page refreshes, and system reboots.

---

## Architecture

Data persistence uses a **Vite dev server plugin** that adds REST endpoints to the existing dev server. No extra processes, no extra dependencies, no setup.

```
Browser App ←→ /api/store/* ←→ data/*.json (on disk)
```

---

## Implementation

### 1. Vite Plugin (`src/server/persistence.ts`)

Generate this file in every project that stores data:

```typescript
import type { Plugin } from 'vite';
import fs from 'fs';
import path from 'path';

export function persistencePlugin(): Plugin {
  const dataDir = path.resolve(process.cwd(), 'data');

  return {
    name: 'local-persistence',
    configureServer(server) {
      // Ensure data directory exists
      if (!fs.existsSync(dataDir)) {
        fs.mkdirSync(dataDir, { recursive: true });
      }

      // GET /api/store/:collection - Read data
      server.middlewares.use((req, res, next) => {
        if (!req.url?.startsWith('/api/store/')) return next();

        const collection = req.url.replace('/api/store/', '').split('?')[0];
        const filePath = path.join(dataDir, `${collection}.json`);

        if (req.method === 'GET') {
          try {
            const data = fs.existsSync(filePath)
              ? JSON.parse(fs.readFileSync(filePath, 'utf-8'))
              : [];
            res.setHeader('Content-Type', 'application/json');
            res.end(JSON.stringify(data));
          } catch {
            res.setHeader('Content-Type', 'application/json');
            res.end('[]');
          }
          return;
        }

        if (req.method === 'POST') {
          let body = '';
          req.on('data', chunk => { body += chunk; });
          req.on('end', () => {
            try {
              const data = JSON.parse(body);
              fs.writeFileSync(filePath, JSON.stringify(data, null, 2));
              res.setHeader('Content-Type', 'application/json');
              res.end(JSON.stringify({ ok: true }));
            } catch {
              res.statusCode = 400;
              res.end(JSON.stringify({ error: 'Invalid JSON' }));
            }
          });
          return;
        }

        next();
      });
    }
  };
}
```

### 2. Vite Config (`vite.config.ts`)

Add the plugin to the Vite config:

```typescript
import { defineConfig } from 'vite';
import react from '@vitejs/plugin-react';
import { persistencePlugin } from './src/server/persistence';

export default defineConfig({
  plugins: [react(), persistencePlugin()],
});
```

### 3. React Hook (`src/hooks/useStore.ts`)

Generate this hook for the builder to use:

```typescript
import { useState, useEffect, useCallback } from 'react';

export function useStore<T>(collection: string, initialValue: T[] = []) {
  const [data, setData] = useState<T[]>(initialValue);
  const [loading, setLoading] = useState(true);

  // Load on mount
  useEffect(() => {
    fetch(`/api/store/${collection}`)
      .then(res => res.json())
      .then(items => {
        setData(items);
        setLoading(false);
      })
      .catch(() => setLoading(false));
  }, [collection]);

  // Save function
  const save = useCallback(async (newData: T[]) => {
    setData(newData);
    await fetch(`/api/store/${collection}`, {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify(newData),
    });
  }, [collection]);

  // Convenience: add single item
  const add = useCallback(async (item: T) => {
    const updated = [...data, item];
    await save(updated);
  }, [data, save]);

  // Convenience: remove by index
  const remove = useCallback(async (index: number) => {
    const updated = data.filter((_, i) => i !== index);
    await save(updated);
  }, [data, save]);

  // Convenience: update by index
  const update = useCallback(async (index: number, item: T) => {
    const updated = data.map((existing, i) => i === index ? item : existing);
    await save(updated);
  }, [data, save]);

  return { data, save, add, remove, update, loading };
}
```

### 4. Data Directory

Create a `data/` directory with a `.gitkeep` file. Add `data/*.json` to `.gitignore` so user data is never committed.

---

## Rules

1. **Always use `useStore` for persistence** — never use `localStorage` directly.
2. **Each data type gets its own collection** — `useStore("moods")`, `useStore("entries")`, `useStore("settings")`.
3. **Data files are human-readable JSON** — stored in `data/moods.json`, `data/entries.json`, etc.
4. **Never expose the data directory in the browser** — only accessible via the `/api/store/` endpoints.
5. **The builder never sees any of this** — they just see their data persist across sessions.

---

## What the Builder Sees

Nothing. The agent generates the plugin, hook, and config automatically. The builder's experience:

```
"Build me a mood tracker"
→ App works
→ Add moods
→ Close browser
→ Open browser next day
→ All moods are still there
```

---

## Upgrade Path

If the builder's app outgrows JSON file storage (needs relations, queries, sorting on large datasets), the agent should suggest upgrading to PocketBase:

> "Your app has a lot of data now. Want me to add a real database? It'll make searching and sorting much faster."

This is a Phase 5 feature and is NOT part of the default template.
