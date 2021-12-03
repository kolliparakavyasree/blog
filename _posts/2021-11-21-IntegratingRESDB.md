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

Create React App doesn’t handle backend logic or databases; it just creates a frontend build pipeline, so you can use it with any backend. Then we created components for Sign up, Sign in, Home page, Upload Page, and Document List. Next, State management to maintain the session for the user and authenticate each transaction using the token associated with that user. Document state to maintain the state of the document, whether it is pending approval, approved, rejected or pending transaction hash from blockchain. And then, connected the frontend to the backend by calling the backend API’s for different actions such as authenticating users, exchanging data and carrying out transactions.

### Back End Development

We installed the dependencies for the backend using NPM. 
```bash
npm install express --save
```

Since we are using Express, we need to create a server. We will use the Express framework to create a server. We implemented REST APIs using Express JS Framework for user functionalities and some document functionalities. REST APIs for 

1. User registration with details such as user email, first name, last name, and password and for Login, we used JSON Web tokens for user Authentication.
2. For document upload API, the user should include attributes such as the document, associated users, and the location of the file.
3. Edit the document to replace the whole document.
4. Edit data of the document.
5. Some REST APIs to list the users, search a user.
6. User transactions such as approve and reject.
7. List pending requests of a specific user.

Subsequently, we integrated MongoDB for storing user data, document data, and transactional data and integrated Resilient DB to store and verify the document hash.

### ResilientDB Service



