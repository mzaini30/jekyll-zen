---
layout: post
title: SolidJS Router file-based
image: https://opencollective-production.s3.us-west-1.amazonaws.com/dc256140-1811-11eb-8450-a7b84694d9f2.png
category: solid
---

## Example File Structure

```
pages/
├── index.jsx
├── users.jsx
└── users/
    └── _id.jsx
```

## Install Packages

```bash
pnpm i -D chokidar npm-run-all solid-app-router vue-route-generator-jsx
```

## Set Up `package.json` in `scripts` Section

```json
{
  "name": "vite-template-solid",
  "version": "0.0.0",
  "description": "",
  "scripts": {
    "dev": "run-p dev:*",
    "dev:vite": "vite",
    "dev:routify": "node routify.js -w",
    "build": "node routify.js && vite build",
    "serve": "vite preview"
  },
  "license": "MIT",
  "devDependencies": {
    "chokidar": "^3.5.2",
    "npm-run-all": "^4.1.5",
    "solid-app-router": "^0.0.50",
    "vite": "^2.3.8",
    "vite-plugin-solid": "^2.0.0",
    "vue-route-generator-jsx": "0.0.3"
  },
  "dependencies": {
    "solid-js": "^1.0.0"
  }
}

```

## Create `routify.js`

```javascript
const fs = require('fs')
const { generateRoutes } = require('vue-route-generator-jsx')
const chokidar = require('chokidar');

const generate = () => fs.writeFileSync('./src/routes.js', generateRoutes({
  pages: './src/pages'
}))

if (process.argv[2] == '-w') {
  const watcher = chokidar.watch('./src/pages')
  watcher.on('add', () => generate())
  watcher.on('unlink', () => generate())  
} else {
  generate()
}
```

## Set Up `src/App.jsx`

```jsx
import {Route, Router} from 'solid-app-router'
import routes from './routes'

export default function App(){
  return <>
    <Router routes={routes}>
      <Route></Route>
    </Router>
  </>
}
```

## Create `src/pages/index.jsx` File

```jsx
export default function App(){
	return <>
		<h1>Hello World</h1>
	</>
}
```

## Run

```bash
npm run dev
```

## Build

```bash
npm run build
```
