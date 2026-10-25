---
title:  "Node.js and React"
description: "Getting Started with React, D3, and Modern JavaScript. Created with AI support."
categories: [Programming]
tags: [Node,React,D3]
image: /assets/img/2026-10-25/node-and-react.png
---


# Getting Started with React, D3, and Modern JavaScript

This guide covers the essential setup and foundational concepts you need to build interactive data visualizations using **[React](https://react.dev/)** and **[D3.js](https://d3js.org/)**, powered by **[Node.js](https://nodejs.org/)** and modern **JavaScript**.



## 1. Environment Setup: Node.js and NVM

Before building anything, you need Node.js and npm (Node Package Manager) installed on your system. Using **NVM (Node Version Manager)** is recommended because it lets you easily install and switch between multiple Node.js versions.

### Installation (Linux/macOS)

Run the following commands in your terminal to install NVM and Node.js (version 20 LTS):

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.0/install.sh | bash
nvm install 20

```

*This makes the `node` and `npm` commands available in your terminal shell.* For alternative installation methods, check the official [Node.js Package Manager Guide](https://nodejs.org/en/download/package-manager).


## 2. Creating a React Application

While older tutorials often used `create-react-app`, modern React development typically relies on **Vite** for a faster, lighter developer experience. However, if you are following standard introductory paths, here is how a traditional React project setup looks:

```bash
npx create-react-app my-app

Success! Created my-app at /home/user/git/my-app
Inside that directory, you can run several commands:

  npm start
    Starts the development server.

  npm run build
    Bundles the app into static files for production.

  npm test
    Starts the test runner.

  npm run eject
    Removes this tool and copies build dependencies, configuration files
    and scripts into the app directory. If you do this, you can’t go back!

We suggest that you begin by typing:

  cd my-app
  npm start

Happy hacking!

```

* **Official Documentation:** Learn more on the [React Official Website](https://react.dev/) or follow the [VS Code Node.js / ReactJS Tutorial](https://code.visualstudio.com/docs/nodejs/reactjs-tutorial).

---

## 3. Integrating D3.js with React

D3 (Data-Driven Documents) is a powerful JavaScript library for producing dynamic, interactive data visualizations in web browsers.

To install D3 in your React project, run:

```bash
npm install d3 --save

```

### Recommended Reading & Tutorials

Combining D3 and React can sometimes be tricky because both want to control the DOM. Here are some of the best articles to help you master their integration:

* [Official D3 Getting Started Guide](https://d3js.org/getting-started)
* [LogRocket: Getting Started with D3.js and React](https://blog.logrocket.com/getting-started-d3-js-react/)
* [Pluralsight: Using D3.js Inside a React App](https://www.pluralsight.com/resources/blog/guides/using-d3js-inside-a-react-app)
* [Shirley Wattenbergers Guide on React and D3](https://2019.wattenberger.com/blog/react-and-d3) *(Highly recommended!)*
* [SitePoint: D3.js & React Interactive Data Visualizations](https://www.sitepoint.com/d3-js-react-interactive-data-visualizations/)



## 4. JavaScript Basics: Arrow Functions

Arrow functions provide a concise syntax for writing function expressions. They do not have their own `this` binding, making them ideal for callbacks and functional components.

> For a deep dive, check the official [MDN Arrow Functions Documentation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions).

```javascript
// Traditional anonymous function
(function (a) {
  return a + 100;
});

// 1. Remove the word "function" and place an arrow between the argument and opening body brace
(a) => {
  return a + 100;
};

// 2. Remove the body braces and word "return" — the return is implied.
(a) => a + 100;

// 3. Remove the parameter parentheses (if there is only one parameter)
a => a + 100;

// Traditional anonymous function (no parameters)
(function () {
  return 100; // corrected logic scope reference
});

// Arrow function (no parameters)
() => 100;

```


## 5. React Components: Functional vs. Class Components

> Read more about component structures in this [Geekster Guide on Functional vs. Class Components](https://blog.geekster.in/functional-components-vs-class-components/).

### Functional Components

Functional components are the modern standard in React. They are simple, fast, and easy to write. They return JSX **and** use React hooks (like `useState` for state management and `useEffect` for lifecycle handling).

```jsx
function MyComponent(props) {
  return (
    <div>
      <h1>{props.title}</h1>
      <p>{props.description}</p>
    </div>
  );
}

```

### Class Components

Class components (also known as stateful components) are written using ES6 classes and extend `React.Component`. They manage state internally using `this.state` and utilize lifecycle methods (like `componentDidMount`). They require a `render()` method to return JSX elements.

```jsx
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = { count: 0 };
  }

  render() {
    return (
      <div>
        <h1>{this.props.title}</h1>
        <p>{this.props.description}</p>
        <button onClick={() => this.setState({ count: this.state.count + 1 })}>
          Click me
        </button>
        <p>Count: {this.state.count}</p>
      </div>
    );
  }
}

```


## 6. Summary

The core building blocks required to start developing interactive data visualization web applications:

* **Environment Setup:** Installing **Node.js** via **NVM** ensures an adaptable, controllable JavaScript runtime environment.
* **React Fundamentals:** Initializing a React application unlocks a component-driven paradigm. Modern development favors **Functional Components** using **React Hooks** (`useState`, `useEffect`) over legacy **Class Components** due to simplicity and readability.
* **Modern JavaScript:** Leveraging concise syntax like **Arrow Functions** reduces boilerplate code and improves code readability across React components and callbacks.
* **D3 Integration:** Combining **D3.js** with React brings flexible SVG and canvas rendering capabilities to component state architectures.

Building data-driven web applications with **React** and **D3.js** gives you the best of both worlds: React efficiently manages the UI state and component structure, while D3 provides powerful math, rendering, and scaling tools to turn raw data into meaningful visuals.

As you dive deeper into React and D3 development, keep in mind:

1. **Choose the right tool for DOM manipulation:** Decide whether React or D3 will control the DOM elements (typically, letting React render SVGs and using D3 for math/scales works best).
2. **Embrace Functional React:** Focus on functional components and hooks, as they align seamlessly with modern JavaScript practices and libraries.
