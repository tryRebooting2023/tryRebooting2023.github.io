---
layout: default
---
# tryRebooting's Ask Us
![ci-badge](https://github.com/tryRebooting2023/askus/workflows/its-ask-us/badge.svg)
## [Our Deployed Project](https://askusits.site/)

## Table of Contents
- [Strategy](#strategy)
- [ITS Ask Us Overview](#its-ask-us-overview)
- [User Guide](#user-guide)
  - [Landing Page](#landing-page)
  - [Navigation Bar](#navigation-bar)
  - [Footer](#footer)
  - [Dark mode](#dark-mode)
  - [Once logged in](#once-logged-in)
  - [Scrolling through a message](#scrolling-through-a-message)
  - [Tutorial Page](#tutorial-page)
- [Community Feedback](#community-feedback)
- [Developer Guide](#developer-guide)
- [Project Breakdown](#project-breakdown)
- [Quality Assurance](#quality-assurance)
- [Development history](#development-history)
- [Team Contract Link](#team-contract-link)
- [Team Members](#team-members)

### ITS Ask Us Overview

The goal of this project is to improve the searching effectiveness of the University of Hawaii's Ask Us search engine, which takes in user queries and attempts to return a list of IT-related articles that may help the users resolve their IT issues. We will be attempting to implement an AI search engine which will hopefully alleviate the need to contact the IT help desk representative.

We want this AI search engine to be able to respond to queries as helpfully as possible for anyone with a specific question, or even a general topic to a question. This means being able to ask follow-up questions to unclear queries and being conversational.

We plan on providing the interface for all users at the landing page, but also want to provide login capabilities in order for the AI to be able to store previous chat sessions. This includes "admin" accounts that have access to our "Analytics" page that helps to show the most popular articles used as references to form a response.

### Strategy

Our project follows the Issue Driven Project Management (IDPM) guidelines. Due to very incompatible schedules, all team members will likely only meet in person during class on Monday and Wednesday mornings. Our primary mode of communication is done through Discord. Furthermore each member is assigned different tasks that are agreed upon between the assigner and assignee, with each task listed as an issue on the [source code repository](https://github.com/tryRebooting2023/askus).

## User Guide

### Landing page

Upon entering the [application's site](https://askusits.site/), this is what should be displayed:

<img src="doc/m2-images/landing-page-1.png">
<img src="doc/m2-images/landing-page-3.png">

Users will immediately be allowed to use the Chat function upon landing. This is for the convenience of the general public being able to use it, right away. The input group to the left will send user queries to OpenAI for it to process and then return a response intended to answer the input query. 

### Navigation Bar

<img src="doc/navigation-bar.png">

The navigation bar at the top is present on all pages and allows for quick navigation through different pages. The logo, on click, will return users to the landing or home depending on if the user is logged in. The dropdown menu on the top right includes links to other pages of the UH ITS main site, such as an "About" page. Of course, there will be a drop-down under the "Log in" tab to sign up or sign in. This is also where the user's email will be shown when logged in.

### Footer

<img src="doc/footer.png">

The footer includes some information about the maintenance team. Some hyperlinks allow for quick access to our team's information page (this page), a Google Form for feedback, and the official ITS Contact page.

### Dark mode

<img src="doc/m2-images/dark-light-mode-toggle.png" width="150px">

We also offer a "dark mode" that the user may toggle on/off with the switch. This feature was decided as necessary as it reduces eye strain and cuts glare, especially at nighttime. We strive to maximize our audience's comfort while using our application. We have future ideas for personalization features to better satisfy a broad range of preferences.

### Sign-In Page

<img src="doc/979C376C-B0C2-49BF-9129-CDC9F267D416.jpeg">

Upon selecting the 'Sign In' option within the login dropdown situated at the upper right corner of the navigation bar, users will be directed to the Sign-In page. Here, they have the option to log in using their email and password or opt for Google Authentication. Moreover, for individuals without an existing account, they can conveniently navigate to the 'Sign Up' page by clicking the 'Click here to Register' hyperlink.  

### Once logged in

Users are either admin or non-admin. Their home pages are currently identical. Admin users in particular are granted access to an 'Analytics' page which should provide a list of queries and their associated AI-generated responses along with a positive or negative rating. This allows for an easy visual representation of which articles have been referenced the most which enables developers and ITS employees to concentrate on improving ease of access to these particular articles.

<img src="doc/m2-images/analytics.png">

### Scrolling through a message

<img src="doc/scroll-feature.png">

When a response is large enough, we enable a scrollable feature for that single response to reduce the space taken up by the number of responses. As seen in the screenshot, the user can scroll down the singular message without needing to move the other responses. It is currently being debated whether we want the whole conversation compacted and scrollable or continue using the singular, scrollable response. With M2 completed, the conversation will now automatically scroll down to the most recent response.

### Tutorial Page

<img src="doc/m2-images/tutorial-page.png">

Detailed instructions on our site can be found on the ʻTutorialʻ page, accessed through the toggle dropdown in the navigation bar. We included screenshots of the particular sections on our page to make it easy for readers to follow.

## Community Feedback

From our testing, we found that providing the "Related Article Links" was a popular feature. Most testers complimented this function as it was beneficial to them because those links provided further detail into what the question topic is. The "Tutorial" page was also a liked feature as it was simple enough to read through and understand. Our testers, on average, voted 3.7/5 in terms of how likely they would use the application.

However, there were some complaints about implementing more content, bugs, and the UI design. The main complaint we received was that the site doesn't look like a "conversation" with the bot. Users would rather be presented with a familiar space, such as seeing the user's inputs to the right and the responses to the left. It was foreseen that having not much content would be a complaint because our main page, and focus, is on the "Chat Bot itself. This can go hand-in-hand with the UI design where users may want more "content" to look at or to interact with. There were some bugs that our team hadn't thought of, such as ensuring the "Home" tab works, mainly because we focused on getting the responses as accurate as possible. 

From the overall feedback, our team will work on fixing the bugs found and changing the UI to resemble a conversation similar to how a text message would be seen on mobile phones. We are also working to include more content for the user such as adding reactions or an optional "send feedback" form to fill out. This way, the user feels as though there is a lot of effort put into the project without overpopulating the page.

## Developer Guide

This section provides information of interest to Meteor developers wishing to use this code base as a basis for their own development tasks.

### Initialization

1. Install [Meteor.](https://www.meteor.com/install)
2. Visit the [Ask Us application github page](https://tryrebooting2023.github.io/), and click the “Use this template” button to create your own repository initialized with a copy of this application. Alternatively, you can download the sources as a zip file or make a fork of the repo. However you do it, download a copy of the repo to your local computer.
3. cd into the askus/app directory (using `cd app`) and install libraries with: `meteor npm install`
4. You need to create environment keys and follow these instructions:
   
##### Environment Keys

An `OPENAI_API_KEY` must be set up from [OpenAI](https://help.openai.com/en/articles/5112595-best-practices-for-api-key-safety) and a `PINECONE_API_KEY`, `PINECONE_ENVIRONMENT`, and `PINECONE_INDEX` must be set up from  [Pinecone](https://docs.pinecone.io/docs/quickstart). Lastly a `GOOGLE_CLIENT_ID`, and `GOOGLE_CLIENT_SECRET` must be set up from [Google Identity](https://developers.google.com/identity/protocols/oauth2) in order for the chat to function. Please refer to their respective API Quickstart guides on best practices for this. Do not share personal keys with anyone, and keep them safe.

Create a `settings.json` file and paste this template into it. Replace keys you made where appropriate.

```
  "OPENAI_API_KEY": "your-openai-api-key",
  "PINECONE_API_KEY": "your-pinecone-api-key",
  "PINECONE_ENVIRONMENT": "your-pinecone-environment",
  "PINECONE_INDEX": "your-pinecone-index",
  "GOOGLE_CLIENT_ID": "your-google-client-id",
  "GOOGLE_CLIENT_SECRET": "your-google-client-secret"
```

5. Run the system with: `meteor npm run start`

If all goes well, the application will appear at http://localhost:3000.

## Project breakdown

<img src="doc/Ask-Us-flowchart.png">

Our initial work involved setting up the chatbot and the databases. As illustrated in the diagram above, we had to parse several HTML files of their important text content, split the contents of each article into smaller chunks of text, convert these chunks into arrays of vectors, and then store these arrays into a dedicated vector database. We accomplished this by introducing additional technologies.         [Cheerio](https://cheerio.js.org/) was used to parse the HTML content into a CSV file, which we then fed to [LangChain](https://js.langchain.com/docs/get_started/introduction).  [OpenAI](https://openai.com/) provided us with the tools to create the text embeddings. [Pinecone](https://docs.pinecone.io/docs/overview) was utilized to store our collection of embeddings.


On the other end, OpenAI was also used to provide the chatbot. We set up the bot to create embeddings of the user query and directly compare those embeddings to those within Pinecone's index in a process called [Cosine Similarity](https://en.wikipedia.org/wiki/Cosine_similarity), which enables the semantic search operation our application was set to employ. Unfortunately, the construction process of the application took more time than we anticipated, so in general, the UI was minimal at best.

## Quality Assurance

### ESLint

Ask Us includes a .eslintrc file to define the coding style adhered to in this application. You can invoke ESLint from the command line as follows: `meteor npm run lint`

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

To run the end-to-end tests in development mode, you must first start up a Ask Us instance by invoking meteor npm run start in one console window.

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

[M2 - November 15 - November 27](https://github.com/orgs/tryRebooting2023/projects/2/views/1)

[M3 - November 27 - December 10](https://github.com/orgs/tryRebooting2023/projects/3/views/1) 

### Team Contract Link:
[Click Here](https://docs.google.com/document/d/15H0tS0bpVW0NQiGvWMAU79zyLRmt6mj2KbrBsFjrVd8/edit?usp=sharing)

### Team Members

This application is designed, implemented, and maintained by [James Ligeralde](https://jligeral.github.io/), [Frances Michelle Uy](https://frances-uy.github.io/), [Jonathan Sapolu](https://jsapolu99.github.io/) and [Michelle Ho](https://michho8.github.io/). 

For contact information, please visit our contract link.
