# Week 5 : DynamoDB and Serverless API's

## Pre-requisites:

Preperation
Last weeks exercises

## Lesson Plan:

So far, we have ventured into the the serverless landscape of **compute** and **storage**, but are missing yet another important area of serverless: **databases**. This week, we will turn our attention to add databases to our Good Green Groceries application through DynamoDB and AWS API Gateway.

## Serverless databases

Databases is a vast field, solves many use cases, and can solved with **serverful** and **serverless** databases. Cloud providers has services for partial and full serverless databases. These services carry the serverless principles (e.g scalability, cost and low maintanence).

The important thing to note is that there is [no free lunch](https://en.wikipedia.org/wiki/There_ain%27t_no_such_thing_as_a_free_lunch) - i.e every choice toward serverless will remove the benefits of serverful databases. So be careful when choosing database for architecture, since there are alot of good choices out there. Pro top: always discuss and research this with your colleagues and align with your stakeholders.

With that said, we will venture into where serverless databases are very popular: NoSql databases and unstructured data. In AWS, this service is called DynamoDB.

## DynamoDB

From AWS we get the description:

source: https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Introduction.html

```
Amazon DynamoDB is a fully managed NoSQL database service that provides fast and predictable performance with seamless scalability. DynamoDB lets you offload the administrative burdens of operating and scaling a distributed database so that you don't have to worry about hardware provisioning, setup and configuration, replication, software patching, or cluster scaling. DynamoDB also offers encryption at rest, which eliminates the operational burden and complexity involved in protecting sensitive data. For more information, see DynamoDB Encryption at Rest.

With DynamoDB, you can create database tables that can store and retrieve any amount of data and serve any level of request traffic. You can scale up or scale down your tables' throughput capacity without downtime or performance degradation. You can use the AWS Management Console to monitor resource utilization and performance metrics.

DynamoDB provides on-demand backup capability. It allows you to create full backups of your tables for long-term retention and archival for regulatory compliance needs. For more information, see On-Demand Backup and Restore for DynamoDB.

(...)

```

We can interface with DyanmoDB through the SDK, in node, this looks like the following:

```
// Import required AWS SDK clients and commands for Node.js
import { PutItemCommand } from "@aws-sdk/client-dynamodb";
import { ddbClient } from "./libs/ddbClient.js";

// Set the parameters
const params = {
  TableName: "TABLE_NAME",
  Item: {
    CUSTOMER_ID: { N: "001" },
    CUSTOMER_NAME: { S: "Richard Roe" },
  },
};

const run = async () => {
  try {
    const data = await ddbClient.send(new PutItemCommand(params));
    console.log(data);
    return data;
  } catch (err) {
    console.error(err);
  }
};
run();
```

For more examples node DynamoDB examples, see [here](https://docs.aws.amazon.com/sdk-for-javascript/v3/developer-guide/dynamodb-example-table-read-write.html)

## API Gateway

From AWS, we once again get an accurate description of the API Gateway service:

source: https://aws.amazon.com/api-gateway/

```
Amazon API Gateway is a fully managed service that makes it easy for developers to create, publish, maintain, monitor, and secure APIs at any scale. APIs act as the "front door" for applications to access data, business logic, or functionality from your backend services. Using API Gateway, you can create RESTful APIs and WebSocket APIs that enable real-time two-way communication applications. API Gateway supports containerized and serverless workloads, as well as web applications.

API Gateway handles all the tasks involved in accepting and processing up to hundreds of thousands of concurrent API calls, including traffic management, CORS support, authorization and access control, throttling, monitoring, and API version management. API Gateway has no minimum fees or startup costs. You pay for the API calls you receive and the amount of data transferred out and, with the API Gateway tiered pricing model, you can reduce your cost as your API usage scales.
```

### 6. Class Assignments
