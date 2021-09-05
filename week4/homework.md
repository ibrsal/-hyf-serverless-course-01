# Homework for Week #4

## Overview

The Good Green Groceries sales team has once again shown their brilliant creativity by allowing all kind of vendors upload their inventory lists to our S3 buckets. They now want you to scan the uploaded files for specific categories and items within a specific price range. They are also tired of logging into AWS (where they are creating a great deal of havoc!) so they asked if we could kindly post the results in Slack.

Specifically, Good Green Groceries has made an agreement with external providers to upload files containing their inventory on a weekly basis in a public bucket. We only care about the **vegetables** and **fruits** categories, and will scan for the current prices. Given the price is under 10$, we will then publish a notification.

Also, your CTO has kindly asked you to not deploy the lambdas yet, as he is working on something secret that will make your changes automatically deployed in the future.

## Assignments

1. Green Good Groceries already had some old lambda in place from previously which we are lucky to use. It even have tests, a test bucket and a test file! Navigate to the lambda in the folder `homework-assignment` and run the command `npm run test` to execute the tests. You can also run the lambda itself with the command `sam local invoke S3JsonLoggerFunction --event events/event-s3.json`. Familiarize yourself with the lambda code.
2. Implement the functionality for listing all groceries and fruit categories with the cost of under 10.0$. Also find the maximum and minimum prices of all the valid candidates you just found.
3. Once done, we need to send this to a webhook of the slack channel `https://hooks.slack.com/services/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`. The webhook is a post endpoint, with the following payload: `{"text":"Hello, World!"}`. We will leave it to you to decide how to perform the http requests (one way is using javascripts `fetch`).
4. Make your lambda publish a SNS with the topic `INVENTORY_SCAN_COMPLETE`, and the objectID as the message body. You will need to add uncomment the SAM policies inside the `cloudformation.js`.
5. Create a new lambda which listens to the SNS topic `INVENTORY_SCAN_COMPLETE`. Extract the body, and then make the lambda delete the given file. To test this, feel free to use the event under `week4/materials/assignments/events/custom-delete-event.json` for local development.

## Optional assignments

6. Make your slack message even more fancy (see [here](https://api.slack.com/messaging/webhooks#advanced_message_formatting) for the slack documentation)
7. Good Green Groceries sales is once again exelling us with good ideas. For each category, they want the min, max, average and total values. Attach it to the message as well.
