## If you prefer watching a video...

###### Be sure to Subscribe to the Official [Code Angle](https://www.youtube.com/c/TheCodeAngle/videos) Youtube Channel for more videos.
<a href="https://www.youtube.com/watch?v=enqRAjGox2Q" title="How to setup and Deploy React 18 Alpha using Snowpack and Vercel" target="_blank"><img src="https://res.cloudinary.com/dz4tt9omp/image/upload/v1626749625/react18.png" alt="Alternate Text" /></a>


> *Talk is cheap. Show me the code*  
> *― Linus Torvalds*

## Table of Contents

-   ***Introduction***
-   ***Installation and Setup of React using Snowpack***
-   ***Folder Restructure***
-   ***code overview***
-   ***Running the app***
-   ***Deployment Process Using Vercel***
-   ***Conclusion***

## Introduction

Earlier this month the React Team released some updates concerning the release of React 18. These updates include the following:

-   Work has begun on the React 18 release, which will be the next major version.
-   A working group has been created to prepare the community for the gradual adoption of new features.
-   An Alpha version has already been published for library authors to try and provide valuable feedback.

The purpose of this tutorial is to set up the React 18 Alpha version using SnowPack, a lightning-fast frontend build tool, designed for the modern web. Then we deploy on **Vercel**.

## Installation and Setup of React 18 Alpha using Snowpack

First, you need to have [Node.js](https://nodejs.org/en/) installed, once that is done then you can now install [Snowpack](https://www.snowpack.dev/). You can use the command below to install Snowpack.

```
npm install snowpack
```

Once that is installed, then you can head to a directory where you want to put your new project.

Now run the following command in your terminal to create a new directory called ***react-snowpack.*** This will automatically generate a minimal boilerplate template.
```
npx create-snowpack-app react-snowpack --template @snowpack/app-template-minimal
```

You can now head to the new directory with the following command
```
cd react-snowpack
```
Once inside this directory, we can finally install the React 18 Alpha version by running the command below.
```
npm i react@alpha react-dom@alpha
```
Once this is done, you can check your package.json file to confirm ***React 18 Alpha*** has been installed. It should look something like what we have below.
```json
  "dependencies": {
    "react": "^18.0.0-alpha-cb8afda18-20210708",
    "react-dom": "^18.0.0-alpha-cb8afda18-20210708"
  }
}
```
## Folder Restructure

React makes use of a templating language called **JSX**. **JSX** stands for JavaScript XML. It is an inline markup that looks like **HTML** that gets transformed to **JavaScript** at runtime**.**

The First step towards the folder restructure is to rename the ***index.js*** file with a **jsx** extension like so, ***index.jsx.*** Doing this will allow ***Snowpack*** to know that we are running a React project.

Next up we create an **src** and **public** folder. Once this is done, we move the ***index.jsx*** file inside the ***src*** folder, still inside the ***src*** folder, we will create a new file called ***app.jsx***.  
Both the ***index.html*** and ***index.css*** file will also be moved into the ***public*** folder.

In the end, we should have the folder structure below.
```
> public
  > index.css
  > index.html
> src
  > App.jsx
  > index.jsx
.gitignore
 package-lock.json
 package.json
 snowpack.config.mjs
```
## Code Overview

We are going to have code modification in four files(***index.html, App.jsx, index.jsx and snowpack.config.mjs***) before we start up the app and deploy it on Vercel.

### index.html
```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <meta name="description" content="Starter Snowpack App" />
  <link rel="stylesheet" type="text/css" href="/index.css" />
  <title>Starter Snowpack App</title>
</head>

<body>
  <div id="root"></div>
  <script type="module" src="/dist/index.js"></script>
</body>

</html>
```
In the index.html code, three things have to be noted:

-   The ***id*** called ***root*** which we will refer to in the index.jsx file.
-   In the script tag, we have a type called module to enable snowpack to know we will be making use of ES6 syntax.
-   Also in the script tag, we have an src attribute to signify the path of our deployment directory which will be configured in the ***snowpack.config.mjs*** file.

### App.jsx
```jsx
import React from "react";

function App() {
  return (
    <div>
      <header>
        <img
          src="https://res.cloudinary.com/dz4tt9omp/image/upload/v1625528354/react.png"
          alt="logo"
        />
        <p>React 18 Alpha Setup Deployed on Vercel with SnowPack</p>
      </header>
    </div>
  );
}
export default App;
```
Above in the ***app.jsx*** file, we generate a simple ***React*** boilerplate template using a functional component.

### index.jsx
```jsx
import React from "react";
import ReactDOM from "react-dom";
import App from "./App";

const rootElement = document.getElementById("root");
const root = ReactDOM.createRoot(rootElement);
root.render(<App />);
```
In the ***index.jsx*** file, we did three things to enable us startup the app.

-   First, we import **React, ReactDOM** and the ***App.jsx*** file.
-   Then we created a variable to get the id in the ***index.html*** file.
-   Finally we made use of the new createRoot API in **React 18** to render the application.

### snowpack.config.mjs
```javascript
/\*\* @type {import("snowpack").SnowpackUserConfig } \*/
export default {
  mount: {
    /\* ... \*/
    public: '/',
    src: '/dist'
  },
  plugins: \[
    /\* ... \*/
  \],
  routes: \[
    /\* Enable an SPA Fallback in development: \*/
    // {"match": "routes", "src": ".\*", "dest": "/index.html"},
  \],
  optimize: {
    /\* Example: Bundle your final build: \*/
    // "bundle": true,
  },
  packageOptions: {
    /\* ... \*/
  },
  devOptions: {
    /\* ... \*/
  },
  buildOptions: {
    /\* ... \*/
  },
};
```
Every Snowpack app makes use of the ***snowpack.config.mjs*** file for any configurations like the deployment process. In this project, we will only edit the mount object by adding the ***public*** and ***src*** key.

These serve as a pointer to the path where our deployment folder will be built when we run the build command.

## Running the Application

Now with all our files saved, we can head back to our terminal and run the start command `npm run start`, which will produce the page below in the browser.

![page preview](https://res.cloudinary.com/dz4tt9omp/image/upload/v1626625210/snow.png)

Now our ***React 18 alpha*** app is successfully up and running.

## Deployment Process using Vercel

> Vercel enables developers to host websites and web services that deploy instantly and scale automatically all without any configuration.
> 
> **\-Vercel** Documentation

The first step to take towards deployment is to run the command below at the root of our project.
```
npm run build
```
This will generate a **build** directory. Inside the **build** directory is a ***dist*** folder that contains the code we will push to **Vercel**.

Next up we do the following:

**1). Install Vercel **

To do this we run the command ```npm i -g vercel```

**2). Login into Vercel**

After installing Vercel globally on your machine. Type `vercel` in the terminal. This will prompt you to log into your account if you are not already logged in.

**3).  Project Setup and Deployment**

![prompt terminal](https://res.cloudinary.com/dz4tt9omp/image/upload/v1626647529/react-snoww.png)

To summarize the prompt question in the image above, the following questions will be asked:

-   Set up and deploy — ***Y*** *(It's a new application).*
-   Which scope do you want to deploy to? *\- Select the name of your account.*
-   Found project "desoga10/snowpack-react". Link to it? - ***N*** (Because we want to deploy as a different project).*
-   Link to a different existing project? - ***N*** *(Because we are creating a new project).*
-   What’s your project's name? *(react-snoww).*
-   In which directory is your code created? ./build (It's in the build folder we generated with the ***npm run build*** command).
-    Want to override the settings? ***N****(To prevent Vercel from making changes to or default settings ).*
    

Vercel will now build the application, installing all dependencies in the process. When the installation is done, an inspect link will be available in the terminal. With this link, we can access the Vercel dashboard to see our deployed app.

![project dashboard](https://res.cloudinary.com/dz4tt9omp/image/upload/v1626648623/vercel.png)

**4).  Open the Deployed Project**

You can now visit the newly deployed project by clicking on the “visit” button on your dashboard shown in the image above.

![live project image](https://res.cloudinary.com/dz4tt9omp/image/upload/v1626625210/snow.png)

## Conclusion

You can find the deployed code in my [GitHub](https://github.com/desoga10/react-snow) account.

I create [Youtube](https://www.youtube.com/TheCodeAngle) tutorials too, make sure to subscribe, thank you.
