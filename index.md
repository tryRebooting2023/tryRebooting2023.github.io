---
layout: default
---
# tryRebooting's Ask Us
![ci-badge](https://github.com/tryRebooting2023/askus/workflows/its-ask-us/badge.svg)
## [Our Application's Deployment](http://137.184.70.155/)

## Table of Contents
- [Strategy](#strategy)
- [ITS Ask Us Overview](#its-ask-us-overview)
- [The Application Anatomy](#the-application-anatomy)
- [Landing Page](#landing-page)
  - [Navigation Bar](#navigation-bar)
  - [Dark mode](#dark-mode)
  - [Once logged in](#once-logged-in)
  - [Scrolling through a message](#scrolling-through-a-message)
  - [Tutorial Page](#tutorial-page)
- [Development Guide](#development-guide)
- [Development history](#development-history)
- [Team Contract Link](#team-contract-link)
- [Team Members](#team-members)

### Strategy

Our project follows the Issue Driven Project Management (IDPM) guidelines. Due to very incompatible schedules, all team members will likely only meet in person during class on Monday and Wednesday mornings. Our primary mode of communication is done through Discord. Furthermore each member is assigned different tasks that are agreed upon between the assigner and assignee, with each task listed as an issue on the [source code repository](https://github.com/tryRebooting2023/askus).

### ITS Ask Us Overview

The goal of this project is to improve the searching effectiveness of the University of Hawaii's Ask Us search engine, which takes in user queries and attempts to return a list of IT-related articles that may help the users resolve their IT issues. We will be attempting to implement an AI search engine which will hopefully alleviate the need to contact the IT help desk representative.

We want this AI search engine to be able to respond to queries as helpfully as possible for anyone with a specific question, or even a general topic to a question. This means being able to ask follow-up questions to unclear queries and being conversational.

We plan on providing the interface for all users at the landing page, but also want to provide login capabilities in order for the AI to be able to store previous chat sessions.

### The Application Anatomy

This is a user-guide for Ask Us.

#### Landing page

Upon entering the [application's site](http://137.184.70.155/), this is what should be displayed:

<img src="doc/m2-images/landing-page-1.png">
<img src="doc/m2-images/landing-page-3.png">

Users will immediately be allowed to use the Chat function upon landing. This is for the convenience of the general public being able to use it, right away. The input group to the left will send user queries to OpenAI for it to process and then return a statement intended to answer the input query. 

#### Navigation Bar
The navigation bar at the top is present on all pages and the logo, on click, will return users to landing or home depending on if the user is logged in. In addition to the logo is a dropdown menu with links to other parts of UH's main site, to sign-up, or sign-in.

#### Dark mode

<img src="doc/m2-images/dark-light-mode-toggle.png" width="150px">

We also offer a "dark mode" that the user may toggle on/off with the switch. This feature was decided as necessary as it reduces eye strain and cuts glare, especially at nighttime. We strive to maximize our audience's comfort while using our application. We have future ideas for personalization features to better satisfy a broad range of preferences.


#### Once logged in

Users are either admin or non-admin. Their home pages are currently identical. Admin users in particular are granted access to a
'Analytics' page which should provide a list of queries and their associated AI-generated responses along with a positive or negative rating.

<img src="doc/m2-images/analytics.png">

#### Scrolling through a message

<img src="doc/scroll-feature.png">

When a response is large enough, we enable a scrollable feature for that single response in order to reduce the space taken up by the number of responses. As seen in the screenshot, the user is able to scroll down the singular message without needing to move the other responses. It is currently being debated whether we want the whole conversation compacted and scrollable or continue using the singular, scrollable response.

#### Tutorial Page

<img src="doc/m2-images/tutorial-page.png">

Detailed intructions can be found through the ʻTutorialʻ page, accessed through the toggle dropdown in the navigation bar.


### Development guide

This section provides information of interest to Meteor developers wishing to use this code base as a basis for their own development tasks.

##### Initialization

First, install [Meteor.](https://www.meteor.com/install)

Second, visit the [Ask Us application github page](https://tryrebooting2023.github.io/), and click the “Use this template” button to create your own repository initialized with a copy of this application. Alternatively, you can download the sources as a zip file or make a fork of the repo. However you do it, download a copy of the repo to your local computer.

Third, cd into the askus/app directory and install libraries with:

``
meteor npm install
``

Fourth, run the system with:

``
meteor npm run start
``

If all goes well, the application will appear at http://localhost:3000.


##### Project breakdown

<img src="doc/Ask-Us-flowchart.png">

Our initial work involved setting up the chatbot and the databases. As illustrated in the diagram above, we had to parse several HTML files of its important text content, split the contents of each article into smaller chunks of text, convert these chunks into arrays of vectors, and then store these arrays into a dedicated vector database. We accomplished this by introducing additional technologies.         [Cheerio](https://cheerio.js.org/) was used to parse the HTML content into a CSV file, which we then fed to [LangChain](https://js.langchain.com/docs/get_started/introduction).  [OpenAI](https://openai.com/) provided us with the tools to create the text embeddings. [Pinecone](https://docs.pinecone.io/docs/overview) was utilized to store our collection of embeddings.


On the other end, OpenAI was also used to provide the chat bot. We set up the bot to create embeddings of the user query and directly compare those embeddings to those within Pinecone's index in a process called [Cosine Similarity](https://en.wikipedia.org/wiki/Cosine_similarity), which enables the semantic search operation our application was set to employ. Unfortunately, the construction process of the application took more time than we anticipated, so in general the UI was minimal at best.

#### Quality Assurance

##### ESLint

Ask Us includes a .eslintrc file to define the coding style adhered to in this application. You can invoke ESLint from the command line as follows:

``meteor npm run lint``

Here is sample output indicating that no ESLint errors were detected:


````
$ meteor npm run lint

> meteor-application-template-react@ lint /Users/michelleuy/Desktop/github/askus/app
> eslint --quiet --ext .jsx --ext .js ./imports && eslint --quiet --ext .js ./tests

$
````
ESLint should run without generating any errors.

It’s significantly easier to do development with ESLint integrated directly into your IDE (such as IntelliJ).

##### End to End Testing

Ask Us uses TestCafe to provide automated end-to-end testing.

To run the end-to-end tests in development mode, you must first start up a BowFolios instance by invoking meteor npm run start in one console window.

Then, in another console window, start up the end-to-end tests with:

``meteor npm run testcafe``

You will see browser windows appear and disappear as the tests run. If the tests finish successfully, you should see the following in your second console window:

```
 % meteor npm run testcafe

> meteor-application-template-react@ testcafe /Users/michelleuy/Desktop/github/askus/app
> testcafe chrome tests/*.testcafe.js

 Running tests in:
 - Chrome 119.0.0.0 / Ventura 13

 meteor-application-template-react localhost test with default db
 ✓ Test that landing page shows up
 ✓ Test that signin and signout work
 ✓ Test the Analytics page
 ✓ Test the Tutorial page
 ✓ Test search function


 5 passed (21s)
(base) michelleuy@MacBook-Pro-28 app %
```


### Development history

[M1 - October 25 - November 15](https://github.com/orgs/tryRebooting2023/projects/1/views/1)  
[M2 - November 15 - Present](https://github.com/orgs/tryRebooting2023/projects/2/views/1)  
  
As previously stated, we plan to update the site's user and admin pages to enable additional features. These additional features will be a handy resource for UH IT related topics. The user feedback page is the first new page we will create. Its implementation will involve setting up a new collection on MongoDB, displaying a form after each chatbot response for users to interact with, and creating the admin-only-accessible page which should display the feedback data. The last additional page we plan to implement is a tutorial page, which we will have accessible through the navigation bar. It walks you through how to maximize your search experience as a user.

### Team Contract Link:
[Click Here](https://docs.google.com/document/d/15H0tS0bpVW0NQiGvWMAU79zyLRmt6mj2KbrBsFjrVd8/edit?usp=sharing)

### Team Members

This application is designed, implemented, and maintained by [James Ligeralde](https://jligeral.github.io/), [Frances Michelle Uy](https://frances-uy.github.io/), [Jonathan Sapolu](https://jsapolu99.github.io/) and [Michelle Ho](https://michho8.github.io/). 

For contact information, please visit our contract link.
