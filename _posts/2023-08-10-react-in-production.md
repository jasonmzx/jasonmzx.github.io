---
layout: page
title: React In Production
date:   2023-07-30 06:00
description: Discussion of React.js in Production, Research & Notes
tags: [react.js]
toc: true
---

# React In Production

When it’s time to move your app to production, having multiple JavaScript or CSS files isn’t ideal. When a user visits your site, each of your files will require an *additional* HTTP request, ~making your site slower to load.~ So to remedy this, you can create a **“build”** of our app, which merges all your CSS files into one file, and does the same with your JavaScript. This way, you minimize the number and size of files the user gets. To create this **“build”**, you use a **“build tool”**. Hence the use of `npm run build`.

After you run npm run build your build directory will be:

```
build/
  static/
    css/
      main.css
    js/
      main.js
```

(Right now, with `npm start`, the **React Components** are visible, not minified & combined like a build)

[Quoted from StackOverflow](https://stackoverflow.com/questions/43830866/what-is-npm-run-build-in-create-react-app)

---

From my understanding, you're essentially **serve**ng a static version of your build *(A.K.A Webpack Bundle)*

### What is Webpack, what does it do for React Build?
Webpack simplifies the build process for React applications. It allows developers to manage dependencies and bundle files with ease. Webpack can also optimize code and assets for production, reducing the file size of the application and improving performance.
*(Minification of JavaScript, HTML & CSS... Making React.js Code More Obscured... Bundling of Website)*



Serving a React Build: *(npm **[Serve Library, by Vercel](https://www.npmjs.com/package/serve)** required)*

`npm install -g serve`
`serve -s build`

Serving React Build on specific port: *(Auto default is port 3000)*

`serve -s build -l 4000`

[SRC: Create-React-App Deployment Docs](https://create-react-app.dev/docs/deployment/)

---

## What if I don't want to use serve, and just deploy the Static Site directly to NGINX... 

Dockerfile for React.js Build, without serve
```Dockerfile
FROM node:16-alpine as builder
# Set the working directory to /app inside the container
WORKDIR /app
# Copy app files
COPY . .
# Install dependencies (npm ci makes sure the exact versions in the lockfile gets installed)
RUN npm ci 
# Build the app
RUN npm run build

# Bundle static assets with nginx
FROM nginx:1.21.0-alpine as production
ENV NODE_ENV production
# Copy built assets from `builder` image
COPY --from=builder /app/build /usr/share/nginx/html
# Add your nginx.conf
COPY nginx.conf /etc/nginx/conf.d/default.conf
# Expose port
EXPOSE 80
# Start nginx
CMD ["nginx", "-g", "daemon off;"]
```

NGINX Setup, it will literally just be manually serving the "Static" HTML built by React Build & the whole Web Pack?

```bash
// nginx.conf

server {
  listen 80;

  location / {
    root /usr/share/nginx/html/;
    include /etc/nginx/mime.types;
    try_files $uri $uri/ /index.html;
  }
}
```

look into these jason

TODO: https://jsramblings.com/dockerizing-a-react-app/

TODO: Look into this link https://medium.com/bb-tutorials-and-thoughts/how-to-serve-react-application-with-nginx-and-docker-9c51ac2c50ba



