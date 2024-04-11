**Instruktioner hur man uppgraderar ett Vite React-projekt i Javascript till Typescript**

1. Installera dev dependencies

`npm install -D typescript @types/react @types/react-dom`

2. Byt ut i packages.json

`"build": "vite build"`
med 👇

`"build": "tsc && vite build"`

3. Byt ut  vite.config.js och main.jsx till vite.config.ts och main.tsx

4. Skapa tsconfig.json i roten med följande: 

```
{
  "compilerOptions": {
    "target": "ESNext",
    "useDefineForClassFields": true,
    "lib": ["DOM", "DOM.Iterable", "ESNext"],
    "allowJs": false,
    "skipLibCheck": true,
    "esModuleInterop": false,
    "allowSyntheticDefaultImports": true,
    "strict": true,
    "forceConsistentCasingInFileNames": true,
    "module": "ESNext",
    "moduleResolution": "Node",
    "resolveJsonModule": true,
    "isolatedModules": true,
    "noEmit": true,
    "jsx": "react-jsx"
  },
  "include": ["src"],
  "references": [{ "path": "./tsconfig.node.json" }]
}
```

5. Skapa tsconfig.node.json i roten med följande: 

```
{
  "compilerOptions": {
    "composite": true,
    "module": "ESNext",
    "moduleResolution": "Node",
    "allowSyntheticDefaultImports": true
  },
  "include": ["vite.config.ts"]
}
```

6. Skapa en fil `vite-env.d.ts` i src/ foldern och kopiera in följande:

`/// <reference types="vite/client" />`

7. Ändra till main.tsx i index.html

`<script type="module" src="/src/main.tsx"></script>`

8. Lägg till ett utropstecken i main.tsx efter document.getElementById('root')

```
ReactDOM.createRoot(document.getElementById('root')!).render(
  <React.StrictMode>
    <AuthProvider>
    <Provider store={store}>
      <App />
      </Provider>
    </AuthProvider>
  </React.StrictMode>,
)
```
