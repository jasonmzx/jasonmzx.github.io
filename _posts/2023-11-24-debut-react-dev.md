---
layout: page
title: React.dev
date:   2023-09-09 06:00
description: N/A
tags: [react.js]
toc: true
---

I've been using `create-react-app` for a while now, and I've realized the React Ecosystem has faced some major changes.
- *create-react-app* >> **React.dev**
- React is now Exclusively Typescript
- React is now heavily integrated with modern web frameworks like **Next.js** and **Remix**

**Redux Toolkit** is still used for State Management for Serializable data *JSON-esque*

**React Router** is still used URL Page routing & tied to Top-level component *(as I like to call them, pages)*

---
### Vite
*(French word for "quick", pronounced /vit/)* is a build tool that aims to provide a faster and leaner development experience for modern web projects. It consists of two major parts:

- A dev server that provides rich feature enhancements over native ES modules, for example extremely fast Hot Module Replacement (HMR).

- A build command that bundles your code with Rollup, pre-configured to output highly optimized static assets for production.
---

Using Vite & Node to *create my JS react app*
`npm create vite@latest firepit-wa -- --template react`

**output:**
```
Scaffolding project in C:\Users\jason\firepit-wa...
Done. Now run:

  cd firepit-wa
  npm install
  npm run dev
```

![vr](/assets/custom/pictures/vite_react.png)

### Trying the React-Router

`npm install react-router-dom`

```js
import { useState } from 'react'
import { BrowserRouter as Router, Route, Routes } from "react-router-dom";
import './App.css'
import LandingPage from './components/LandingPage';

function App() {
  return (
<Router>
    <Routes>
      <Route path="/" element={<LandingPage />}></Route>
      <Route path="/landing/:id" element={<LandingPage />}></Route>
    </Routes>
  </Router>
  )
}

export default App
```

To many surprise, the **React-Router-Dom** *(RRD)* works the exact same as the old React! Yay, checkout `/landing/:id`

Which is utilized in that component via **RRD**'s useParams function. 

```js
import React from 'react'
import { useParams } from 'react-router-dom';

const LandingPage = () => {
  const [count, setCount] = React.useState(0);
  //* URL PARAMTER
  const { id } = useParams();
  return (
    <><div>

      </div>
      <div className="card">
        <button onClick={() => setCount((count) => count + 1)}>
          count is {count}
        </button>
        <p>
          Landed! {id}
        </p>
      </div></>);
}
export default LandingPage
```