# iosCheckLiquidGlassUI

Vue3 + Vite + TypeScript + Tailwind CSS + Headless UI の最小サンプルプロジェクト

## 要件

- Node.js 18以上
- npm

## プロジェクト構成

```
iosCheckLiquidGlassUI/
├── index.html                      # HTMLエントリーポイント
├── package.json                    # プロジェクト依存関係
├── tsconfig.json                   # TypeScript設定
├── tsconfig.node.json              # Node用TypeScript設定
├── vite.config.ts                  # Vite設定
├── postcss.config.js               # PostCSS設定
├── tailwind.config.js              # Tailwind CSS設定
├── .gitignore                      # Git除外設定
├── src/
│   ├── main.ts                     # アプリケーションエントリーポイント
│   ├── index.css                   # グローバルスタイル（Tailwind + modal-openスタイル）
│   ├── App.vue                     # メインアプリケーションコンポーネント
│   └── components/
│       └── ModalExample.vue        # Headless UI Dialogモーダルコンポーネント
└── README.md                       # このファイル
```

## 実行手順

### 1. 依存関係のインストール

```bash
npm install
```

### 2. 開発サーバーの起動

```bash
npm run dev
```

ブラウザで http://localhost:5173 にアクセスしてください。

### 3. プロダクションビルド

```bash
npm run build
```

ビルド成果物は `dist` ディレクトリに生成されます。

### 4. プレビュー

```bash
npm run preview
```

## 主要な実装内容

### 依存関係

- **Vue 3**: UI フレームワーク
- **Vite**: ビルドツール
- **TypeScript**: 型安全な開発
- **Tailwind CSS**: ユーティリティファーストCSSフレームワーク
- **@headlessui/vue**: アクセシブルなUIコンポーネント
- **PostCSS**: CSS処理

### 技術的特徴

#### 1. `<script setup>` 構文の使用
全てのVueコンポーネントで`<script setup>`構文を使用し、簡潔なコードを実現しています。

#### 2. Tailwind CSS (PostCSS経由)
- `postcss.config.js`でPostCSSを通じてTailwind CSSを適用
- `tailwind.config.js`でTailwindの設定を管理

#### 3. Headless UI Dialog実装
`ModalExample.vue`でHeadless UIの`Dialog`コンポーネントを実装:

- **透明オーバーレイ**: `bg-transparent`クラスでオーバーレイを透明化
- **クリックで閉じる**: オーバーレイクリックでモーダルを閉じる
- **modal-openクラス**: モーダル開時に`document.body`に`modal-open`クラスを付与
- **背景減光**: `body.modal-open`で背景を`rgba(0, 0, 0, 0.4)`に設定
- **h-dvh使用**: 100vhの代わりに`h-dvh`（dynamic viewport height）を使用

#### 4. グローバルスタイル (src/index.css)

```css
@tailwind base;
@tailwind components;
@tailwind utilities;

body.modal-open {
  background: rgba(0, 0, 0, 0.4);
}
```

モーダル表示時にbodyタグに`modal-open`クラスが追加され、背景が自動的に減光されます。

## ファイル内容

### package.json

```json
{
  "name": "ios-check-liquid-glass-ui",
  "private": true,
  "version": "0.0.0",
  "type": "module",
  "scripts": {
    "dev": "vite",
    "build": "vue-tsc && vite build",
    "preview": "vite preview"
  },
  "dependencies": {
    "@headlessui/vue": "^1.7.16",
    "vue": "^3.3.8"
  },
  "devDependencies": {
    "@vitejs/plugin-vue": "^5.0.0",
    "autoprefixer": "^10.4.16",
    "postcss": "^8.4.32",
    "tailwindcss": "^3.3.6",
    "typescript": "^5.2.2",
    "vite": "^5.0.10",
    "vue-tsc": "^2.0.0"
  }
}
```

### vite.config.ts

```typescript
import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [vue()],
})
```

### tsconfig.json

```json
{
  "compilerOptions": {
    "target": "ES2020",
    "useDefineForClassFields": true,
    "module": "ESNext",
    "lib": ["ES2020", "DOM", "DOM.Iterable"],
    "skipLibCheck": true,

    /* Bundler mode */
    "moduleResolution": "bundler",
    "allowImportingTsExtensions": true,
    "resolveJsonModule": true,
    "isolatedModules": true,
    "noEmit": true,
    "jsx": "preserve",

    /* Linting */
    "strict": true,
    "noUnusedLocals": true,
    "noUnusedParameters": true,
    "noFallthroughCasesInSwitch": true
  },
  "include": ["src/**/*.ts", "src/**/*.tsx", "src/**/*.vue"],
  "references": [{ "path": "./tsconfig.node.json" }]
}
```

### tsconfig.node.json

```json
{
  "compilerOptions": {
    "composite": true,
    "skipLibCheck": true,
    "module": "ESNext",
    "moduleResolution": "bundler",
    "allowSyntheticDefaultImports": true
  },
  "include": ["vite.config.ts"]
}
```

### postcss.config.js

```javascript
export default {
  plugins: {
    tailwindcss: {},
    autoprefixer: {},
  },
}
```

### tailwind.config.js

```javascript
/** @type {import('tailwindcss').Config} */
export default {
  content: [
    "./index.html",
    "./src/**/*.{vue,js,ts,jsx,tsx}",
  ],
  theme: {
    extend: {},
  },
  plugins: [],
}
```

### index.html

```html
<!doctype html>
<html lang="ja">
  <head>
    <meta charset="UTF-8" />
    <link rel="icon" type="image/svg+xml" href="/vite.svg" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Vue 3 + Vite + TypeScript + Tailwind</title>
  </head>
  <body>
    <div id="app"></div>
    <script type="module" src="/src/main.ts"></script>
  </body>
</html>
```

### src/index.css

```css
@tailwind base;
@tailwind components;
@tailwind utilities;

/* Global styles for modal-open class on body */
body.modal-open {
  background: rgba(0, 0, 0, 0.4);
}
```

### src/main.ts

```typescript
import { createApp } from 'vue'
import './index.css'
import App from './App.vue'

createApp(App).mount('#app')
```

### src/App.vue

```vue
<script setup lang="ts">
import ModalExample from './components/ModalExample.vue'
</script>

<template>
  <div class="min-h-dvh flex items-center justify-center bg-gradient-to-br from-blue-50 to-indigo-100">
    <div class="text-center">
      <h1 class="text-4xl font-bold text-gray-800 mb-8">
        Vue 3 + Vite + TypeScript + Tailwind
      </h1>
      <ModalExample />
    </div>
  </div>
</template>
```

### src/components/ModalExample.vue

```vue
<script setup lang="ts">
import { ref, watch } from 'vue'
import { Dialog, DialogPanel, DialogTitle } from '@headlessui/vue'

const isOpen = ref(false)

function openModal() {
  isOpen.value = true
}

function closeModal() {
  isOpen.value = false
}

// Add/remove modal-open class on body when modal opens/closes
watch(isOpen, (newValue) => {
  if (newValue) {
    document.body.classList.add('modal-open')
  } else {
    document.body.classList.remove('modal-open')
  }
})
</script>

<template>
  <div>
    <button
      type="button"
      @click="openModal"
      class="rounded-md bg-indigo-600 px-4 py-2 text-sm font-medium text-white hover:bg-indigo-700 focus:outline-none focus-visible:ring-2 focus-visible:ring-indigo-500 focus-visible:ring-offset-2"
    >
      モーダルを開く
    </button>

    <Dialog :open="isOpen" @close="closeModal" class="relative z-50">
      <!-- Transparent overlay that closes on click -->
      <div class="fixed inset-0 bg-transparent" aria-hidden="true" @click="closeModal" />

      <!-- Full-screen container to center the panel -->
      <div class="fixed inset-0 flex items-center justify-center p-4">
        <DialogPanel class="w-full max-w-md rounded-lg bg-white p-6 shadow-xl">
          <DialogTitle class="text-lg font-medium leading-6 text-gray-900 mb-4">
            モーダルダイアログ
          </DialogTitle>

          <div class="mt-2">
            <p class="text-sm text-gray-500 mb-4">
              これはHeadless UIのDialogコンポーネントを使用したモーダルの例です。
              オーバーレイは透明で、クリックすると閉じます。
            </p>
            <p class="text-sm text-gray-500 mb-4">
              モーダルが開いている間、bodyタグに<code class="bg-gray-100 px-1 rounded">modal-open</code>クラスが付与され、
              背景が減光されます。
            </p>
            <p class="text-sm text-gray-500">
              高さの指定には100vhではなく<code class="bg-gray-100 px-1 rounded">h-dvh</code>を使用しています。
            </p>
          </div>

          <div class="mt-6 flex justify-end space-x-3">
            <button
              type="button"
              @click="closeModal"
              class="rounded-md bg-indigo-600 px-4 py-2 text-sm font-medium text-white hover:bg-indigo-700 focus:outline-none focus-visible:ring-2 focus-visible:ring-indigo-500 focus-visible:ring-offset-2"
            >
              閉じる
            </button>
          </div>
        </DialogPanel>
      </div>
    </Dialog>
  </div>
</template>
```

## ライセンス

MIT