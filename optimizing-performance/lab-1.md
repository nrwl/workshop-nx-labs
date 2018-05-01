# Lab: Lighthouse Analysis

## Time: 5 minutes

## Scenario
We're going to start our application in Angular CLI's "production" mode to make our application as lightweight and fast as possible for performance analysis.

With the application running, we'll use Lighthouse to analyze the performance of the application. The Lighthouse tool is built into Google Chrome's developer tools.

## Instructions
1. Start the server by running `npm run server`.
1. In a new terminal window, start the customer portal in production mode by running `npm run customer-portal:prod`.
1. Open Google Chrome and navigate to localhost:4203.
1. Open Chrome Devtools:
   1. Mac: `Cmd + Opt + I`
   1. Windows: `F12`
1. Click the "Audits" tab then click the "Perform an Audit" button.
1. In the audit modal, uncheck all audits except "Performance".
1. Click "Run Audit" and watch Lighthouse work its magic. You should see Lighthouse reload the page in an emulated mobile device, with emulated 3G network and emulated mobile CPU performance.
1. After the audit is finished, you should see a report with several scores. Record the scores for **First Meaningful Paint** and **First Interactive** so we can compare them after we've made some optimizations. Also notice the screenshots of progression as the app is loaded.

## Bonus

What interesting information can be found from other audits?

What opportunities or recommendations does Lighthouse provide?

## Next Lab
Go to Optimizing Performance Lab #2: [Source Map Explorer](lab-2.md)