# 프로젝트 생성

- `npm create vite@latest .`
- `react` > `typescript` 로 설치
- `npm install`
- `npm run dev` 로 설치 확인

## 깃 세팅

- `git init`
- `git remote add origin 깃주소`

## ESLint 및 Prettier 세팅

- `npm install --save-dev prettier eslint-config-prettier eslint-plugin-prettier` 실행
- `npm i eslint-plugin-react` 실행
- `.prettierrc` 파일 생성

```
{
  "singleQuote": false,
  "semi": true,
  "useTabs": false,
  "tabWidth": 2,
  "trailingComma": "all",
  "printWidth": 80,
  "arrowParens": "avoid",
  "endOfLine": "auto"
}
```

- `eslint.config.js` 수정

```js
import js from "@eslint/js";
import globals from "globals";
import reactHooks from "eslint-plugin-react-hooks";
import reactRefresh from "eslint-plugin-react-refresh";
import tseslint from "typescript-eslint";
import prettier from "eslint-plugin-prettier";

export default tseslint.config(
  { ignores: ["dist"] },
  {
    extends: [js.configs.recommended, ...tseslint.configs.recommended],
    files: ["**/*.{ts,tsx,js,jsx}"], //검사할 파일 종류
    languageOptions: {
      ecmaVersion: 2020,
      globals: globals.browser,
    },
    plugins: {
      "react-hooks": reactHooks,
      "react-refresh": reactRefresh,
      prettier, // Prettier 플러그인
    },
    rules: {
      ...reactHooks.configs.recommended.rules,
      "react-refresh/only-export-components": [
        "warn",
        { allowConstantExport: true },
      ],
      "prettier/prettier": "warn", // Prettier 규칙 (포매팅 오류를 에러로 표시)
    },
  },
);
```

## .gitignore 추가

```
#env
.env
.env.*
```

## npm 설치

- npm i axios
- npm i react-router-dom
- npm i react-icons
- npm i react-hook-form yup @hookform/resolvers
- npm i react-quill
- npm i quill
- npm i dompurify
- npm i react-calendar
- npm i swiper
- npm i recoil
- npm i antd --save
- npm install -D tailwindcss postcss autoprefixer

## Tailwindcss 세팅

- `npx tailwindcss init` 실행
- tailwind.config.js

```js
/** @type {import('tailwindcss').Config} */
export default {
  content: [
    "./index.html",
    "./src/**/*.{js,ts,jsx,tsx}", // Vite 프로젝트에 맞는 파일 확장자 추가
  ],
  theme: {
    extend: {},
  },
  plugins: [],
};
```

- vite.config.ts

```ts
import { defineConfig } from "vite";
import react from "@vitejs/plugin-react";
import tailwindcss from "tailwindcss";

// https://vite.dev/config/
export default defineConfig({
  plugins: [react()],
  css: {
    postcss: {
      plugins: [tailwindcss()],
    },
  },
});
```

- index.css

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

## Recoil 세팅

- main.tsx

```tsx
import { createRoot } from "react-dom/client";
import { RecoilRoot } from "recoil";
import App from "./App.tsx";
import "./index.css";

createRoot(document.getElementById("root")!).render(
  <RecoilRoot>
    <App />
  </RecoilRoot>,
);
```

## tsconfig.app.json을 통한 js 사용 설정

```json
/* 추가설정 */
"allowJs": true,
```

## proxy 사용 설정

- vite.config.js

```ts
  server: {
    proxy: {
      "/api": {
        target: "http://서버 아이피:5214",
        changeOrigin: true,
        secure: false,
      },
    },
  },
```
