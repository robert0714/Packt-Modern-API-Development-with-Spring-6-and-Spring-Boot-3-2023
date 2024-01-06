# Chpater 7 Designing a User Interface
This UI app will be a **single-page application** (SPA) that consists of interactive components such as *Login, Product Listing, Product Detail, Cart, and Order Listing*. This chapter will conclude the end-to-end development and communication between different layers of an online shopping app. By the end of this chapter, you will have learned about SPAs, UI component development using React, and consuming the REST APIs using the browser’s built-in **Fetch API**.

This chapter will cover the following topics:

* Learning React fundamentals
* Exploring React components and other features
* Designing e-commerce app components
* Consuming APIs using Fetch
* Implementing authentication

## Technical requirements
You need the following prerequisites for developing and executing the code:

* You should be familiar with JavaScript: data types, variables, functions, loops, and array methods such as map(), Promises, and async, and so on.
* Node.js 18.x with Node Package Manager (npm) 9.x (and optionally, Yarn, which you can install using ``npm install yarn -g``).
* Visual Studio Code (VS Code): This is a free source code editor. You can use any other source code editor of your choice.
* React 18 libraries that will be included when you use create-react-app.
## Learning React fundamentals
React is a declarative library used to build interactive and dynamic UIs, including isolated small components. It is also sometimes referred to as a framework because it is as capable as and comparable with other JavaScript frameworks such as AngularJS. However, React is a library and works with other supported libraries, including React Router, React Redux, and so on. You normally use it to develop SPAs, but it can also be used to develop full stack applications.

React is used to build the view layer of the application per the MVC architecture. You can build reusable UI components with their own state. You can use either plain JavaScript with HTML or **JavaScript Syntax Extension** (JSX) for templating. We’ll be using JSX in this chapter, which employs a **virtual Document Object Model** (VDOM) for dynamic changes and interactions.

Let’s create a new React app using the create-react-app utility next. This utility scaffolds and provides the basic app structure that you’ll use to develop the example e-commerce app frontend.

### Creating a React app
You can configure and build a React UI app from scratch. However, as mentioned, React provides a create-react-app utility that bootstraps and builds a basic running app template. You can take it further to build a full-fleshed UI application.

Its syntax is shown here:
```bash
npx create-react-app <app name>
```
**npm package executor** (NPX) is a tool that allows you to use command-line interface (CLI) tools and other executables available in the npm registry. It is by default available with npm 5.2.0, or you can install it using npm i npx. It executes the create-react-app React package directly.

Now, let’s create an ecomm-ui application using the following command:
```bash
npx create-react-app ecomm-ui

Creating a new React app in /Users/dev/Modern-API-Development-with-Spring-6-and-Spring-Boot-3/Chapter07/ecomm-ui.

Installing packages. This might take a couple of minutes.
Installing react, react-dom, and react-scripts with cra-template...

//… stripped output for brevity

added 1418 packages in 50s
Success! Created ecomm-ui at /Users/sourabhsharma/dev/pws/java/Modern-API-Development-with-Spring-6-and-Spring-Boot-3/Chapter07/ecomm-ui

//… stripped output for brevity

Inside that directory
We suggest that you begin by typing:
  cd ecomm-ui
  npm start
```

Once it has been installed successfully, you can go to the app directory and start the installed application using create-react-app by running the following command:
```bash
$ cd ecomm-ui
$ code .
```

The ``code .`` command opens the ecomm-ui app project in VS Code. You can then use the following command in the terminal in VS Code to start the development server:
```bash
$ npm start
```
Once the server has started successfully, it will open a new tab on your default browser at localhost:3000.

## Understanding React hooks
Earlier (prior to React version **16.8**), the state was only supported in components defined using classes. Now, React supports the state in both functional and class components. React supports the state in functional components using hooks such as **useState()**, **useContext()**, and so on.

### WHAT ARE HOOKS?

> Hooks are special React built-in functions or user-defined functions that can be stateful and are used to manage the side effects of React functional components. Popular and frequently used hooks are **useState()** and **useEffect()**.