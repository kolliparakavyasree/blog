---
layout: article
title: Integrating an Application with ResilientDB   #review
author: alex #ask about author 
tags: Walkthrough ResilientDB 
aside:
    toc: true
article_header:
  type: overlay
  theme: dark
  background_color: '#000000'
  background_image:
    gradient: 'linear-gradient(135deg, rgba(0, 204, 154 , .2), rgba(51, 154, 154, .2))'
    src: /assets/images/IntegratingResdb/titleImage.png
---


This is an installment of the ResilientDB tutorial series. ResilientDB is a permissioned blockchain fabric developed by the developers at the Exploratory Systems Lab at UC Davis. We are a group of researchers on a mission led by Prof. Mohammad Sadoghi to pioneer a resilient data platform at scale.
{:.info}

In this post we will discuss about integrating Resilient DB with a web application. We have developed web application using React JS for User Interface and Express for Backend. In the web application you can upload a document and add users associated with that document. The associated users can accept or reject the document. The uploaded document's hash is stored in the ResilientDB, so they can verify the document. Whenever the document is modified, every associated user must approve the change. So this application has three major parts, Front End, Back End, and ResilientDB Service. 

### Front End Development

First, we created a React project using Node package manager, NPX.

```bash
npx create-react-app my-app
```

Creating a React App doesn’t handle backend logic or databases; it just creates a frontend build pipeline, so you can use it with any backend. Then we created components for Sign up, Sign in, Home page, Upload Page, and Document List using ES6 classes.

```jsx
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```

Next comes the State management to maintain the session for the user and authenticate each transaction using the JWT Token. Document state to maintain the state of the document, whether it is pending, approved, or rejected. Lastly, we connected the frontend to the backend by calling the backend REST API’s for different actions such as authenticating users, exchanging data and carrying out transactions.

```jsx
// Make a GET request
axios({
  method: 'get',
  url: 'https://resilient-doc.com/api/v1/documents',
});

// Make a Post Request
axios({
  method: 'post',
  url: '/login',
  data: {
    userName: 'john1234',
    password: '*******'
  }
});
```

### Back End Development

We installed the dependencies for the backend using NPM. 
```bash
npm install express --save
```

We implemented REST APIs using Express JS Framework for user functionalities and some document functionalities. Subsequently, we integrated MongoDB for storing user data, document data, and transactional data and integrated Resilient DB to store and verify the document hash. We need to create a MongoDB database and have our application connect to it. We will also need to install mongoose dependency so we can use mongoose to interact with our database.

```js
var mongoose   = require('mongoose');
mongoose.connect('mongodb://127.0.0.1/my_database'); // connect to database
```

We will use mongoose to create models to define the Schema. Then, we create routes for all the REST APIs. We use an instance of the Express Router to handle all of our routes.


### ResilientDB Service

