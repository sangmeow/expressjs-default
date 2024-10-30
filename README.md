# expressjs-default

## CREATE A NEW PROJECT

```
yarn init -y
yarn add express dotenv
yarn add --dev typescript ts-node @types/node @types/express
yarn add --dev concurrently nodemon
```

## TYPESCRIPT CONFIGURATION

```
npx tsc -init
```

```json
{
  "compilerOptions": {
    "rootDirs": ["src"],
    "outDir": "./dist",
    "lib": ["es2020"],
    "target": "es5",
    "module": "CommonJS",
    "moduleResolution": "node",
    "strict": true,
    "esModuleInterop": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true,
    "types": ["node"]
  },
  "exclude": ["node_modules"],
  "include": ["./src/**/*.tsx", "./src/**/*.ts"]
}
```

## SET EXPRESSJS TS CONFIG

#### package.json

```json
{
  // ...
  "main": "src/index.ts",
  "scripts": {
    "build": "npx tsc",
    "start": "node dist/express.js",
    "build:start.mac": "npx tsc && node dist/express.js",
    "build:start.win": "npx tsc&& node dist/express.js",
    "dev.mac": "export NODE_ENV=dev && nodemon --watch './src/**/*.ts' --exec ts-node src/express.ts",
    "dev.win": "set NODE_ENV=dev&& nodemon --watch './src/**/*.ts' --exec ts-node src/express.ts"
  }
  // ...
}
```

- --watch : 변경을 감지할 파일을 지정한다.
- --exec : 실행할 명령어를 지정할 수 있다.

## CREATE DIRECTORIES

```
src
|- config
|- controllers
|- documents
|- libs
|- middlewares
|- models
|- repositories
|- routes
|- services
|- types
|- utils
express.ts
```

## src/express.ts

```typescript
import express, { Express, Request, Response } from "express";
import dotenv from "dotenv";

dotenv.config();

const app: Express = express();
const port = process.env.PORT;

app.get("/", (req: Request, res: Response) => {
  res.send("Express + TypeScript Server");
});

app.listen(port, () => {
  console.log(`⚡️[server]: Server is running at http://localhost:${port}`);
});
```

## START SERVER

```
> npm run dev:mac
```

## PRETTIERRC

```
{
  "trailingComma": "es5",
  "tabWidth": 2,
  "semi": true,
  "singleQuote": false,
  "printWidth": 180
}
```

## ESLINT

```
import globals from "globals";
import pluginJs from "@eslint/js";
import tseslint from "typescript-eslint";


export default [
  {files: ["**/*.{js,mjs,cjs,ts}"]},
  {files: ["**/*.js"], languageOptions: {sourceType: "script"}},
  {languageOptions: { globals: globals.browser }},
  pluginJs.configs.recommended,
  ...tseslint.configs.recommended,
];
```
