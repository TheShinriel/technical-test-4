# Technical test

## Introduction

Fabien just came back from a meeting with an incubator and told them we have a platform “up and running” to monitor people's activities and control the budget for their startups !

All others developers are busy and we need you to deliver the app for tomorrow.
Some bugs are left and we need you to fix those. Don't spend to much time on it.

We need you to follow these steps to understand the app and to fix the bug : 
 - Sign up to the app
 - Create at least 2 others users on people page ( not with signup ) 
 - Edit these profiles and add aditional information 
 - Create a project
 - Input some information about the project
 - Input some activities to track your work in the good project
  
Then, see what happens in the app and fix the bug you found doing that.

## Then
Time to be creative, and efficient. Do what you think would be the best for your product under a short period.

### The goal is to fix at least 3 bugs and implement 1 quick win feature than could help us sell the platform

## Setup api

- cd api
- Run `npm i`
- Run `npm run dev`

## Setup app

- cd app
- Run `npm i`
- Run `npm run dev`

## Finally

Send us the project and answer to those simple questions : 
- What bugs did you find ? How did you solve these and why ? 
- Which feature did you develop and why ? 
- Do you have any feedback about the code / architecture of the project and what was the difficulty you encountered while doing it ? 


# Feedbacks

## Global
If want to use a monorepo (multiple project on same git repo) we might as well do it completely with global scripts
Typescript will be safer

## Api
/!\ .env committed for the api/, thank for the workshop but very dangerous

## App
React without jsx
Redux is a bit too much for the project, React query is enough, there is no business in the app


# Bugs

## User are created without username
-> Username from front was never sended to the api (error on form)

## uncontrolled input
Warning: A component is changing an uncontrolled input of type undefined to be controlled. Input elements should not switch from uncontrolled to controlled (or vice versa). Decide between using a controlled or uncontrolled input element for the lifetime of the component. More info: https://fb.me/react-controlled-components

## Cannot update a user
The button never call the event OnClick to save the user

## When create a new project, it is not listed
Not critical, workaround -> F5

## Cannot open a new project

TypeError
Cannot read properties of undefined (reading 'toString')
Call Stack
 ProjectDetails
  29c5082d802abaf481f4.index.js:8545:19
 renderWithHooks
  29c5082d802abaf481f4.index.js:53786:18
 mountIndeterminateComponent
  29c5082d802abaf481f4.index.js:56465:13
 beginWork
  29c5082d802abaf481f4.index.js:57579:16
 HTMLUnknownElement.callCallback
  29c5082d802abaf481f4.index.js:39171:14
 Object.invokeGuardedCallbackDev
  29c5082d802abaf481f4.index.js:39220:16
 invokeGuardedCallback
  29c5082d802abaf481f4.index.js:39275:31
 beginWork$1
  29c5082d802abaf481f4.index.js:62186:7
 performUnitOfWork
  29c5082d802abaf481f4.index.js:61137:12
 workLoopSync
  29c5082d802abaf481f4.index.js:61113:22

Api /project/:id return an array, fix by changing "find" by "findOne"

## Deliver on Undefined
Please add a comment on what you deliver on undefined (We need to show value created to clients)

Quick fix -> e.project doesn't exist, so use projectId or projectName when it makes sense

## Activity index: {true && (
Useless -> Quickfix: delete this line

## Cannot edit email from account page
The event OnChange was not listened

# Improvements

## Can do more than 1 day per day on activities
Have to check with the business if we want to be able to do 300 days the same day

## Clarify hours/days on activities
If I put 2 on activities, I mean that would say: 2 days
We have to clarify to the users there is 8 hours per day

## Days worked
I guess that means that is the number of day per month?
Must be annual or something else
There is not always the same number of days per month

OR it could be the total of day worked, so it mustn't be editable, could be calculated every day for example with a cron task


## Cost per day & Sell per day
"Cost per day" and "Sell per day" are 2 properties that could evolved in the futur

It is well handle by calculate on activities, but could be difficult to handle for a partial month, or to update a previous month with a different price
```js
n[i].cost = (n[i].total / 8) * user.costPerDay;
n[i].value = (n[i].total / 8) * (user.sellPerDay || 0);
```

## return new Promise(async (resolve, reject) => {
"new promise()" create a promise, the function must not be async, the keyword is an error, but luck it is handle and ignore by javascript
