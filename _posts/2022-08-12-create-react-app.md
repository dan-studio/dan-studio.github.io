--- 
layout: single 
title:  "[React] create-react-app"
categories: React
tags: react
toc: true
sidebar: 
    nav: "docs"
---

# [React](https://reactjs.org)
> A JavaScript library created by Facebook for building user interfaces

![post-thumbnail](https://velog.velcdn.com/images/danchoi/post/bad31f41-5e76-4ab0-b60e-cb4742e30d19/image.jpeg)

![](https://3ulsmb4eg8vz37c0vz2si64j-wpengine.netdna-ssl.com/wp-content/uploads/2019/05/react-native-UX-design.gif)

### What Is React?
declarative, efficient, and flexible JavaScript library for building user interfaces. It lets you compose complex UIs from small and isolated pieces of code called “components”.

### Create React App
To set up create-react-app, run the following code in your terminal, one directory up from where you want the project to be created.
```
$ npx create-react-app app-name
```
Once that finishes installing, move to the newly created directory and start the project.
```
$ cd react-tutorial && npm start
```
Once you run this command, a new window will popup at localhost:3000 with your new React app.
![](https://velog.velcdn.com/images/danchoi/post/742cc798-4be8-498c-90c8-156e0d12d6c1/image.png)

If you want to change the defalt port 3000 to something else,
update the "start" command in your package.json file

```json
//for Mac OS and Linux
{
  "scripts": {
    "start": "export PORT=5000 && react-scripts start",
  },
}
```
```json
//for Windows
{
  "scripts": {
    "start": "set PORT=5000 && react-scripts start",
  },
}
```
