# What is Servesless?

ServerLess is the cloud computing execution model where the cloud provider manages the infrastructure and automatically allocate resources to run your code.

As a developer, you only focus on writing and deploying code, without worrying about managing servers, scaling or operating systems. 

Despite its name, ```serverless``` does not mean there are no servers. Instead, it means **you don't have to manage servers** - the cloud provider takes care of all server realted tasks.

```
OR
```

Serverless computing is an application development model where you can build and run applications without having to manage servers. It means you can build run applications on the third-party managed server infrastructure.

You need to pay only for the exact amount of resources used by your application.

```Serverless एक cloud computing model है जिसमे developer small code लिखता है और code को run करने के लिए cloud provider infrastructure manage करता है|```

<br>

In **Azure**, **serverless computing** is a cloud computing model where Microsoft Azure handles the infrastructure, scaling, and management, allowing developers to focus solely on writing and deploying code.


<br>

## Key Characteristics of Serverless

- ### No Server Management:
  - You don’t need to provision, configure, or manage servers.
  - The cloud provider ensures that your code runs on reliable infrastructure.

- ### Event-Driven Execution:
  - Serverless applications execute code in response to events, such as HTTP requests, database updates, or file uploads.

- ### Automatic Scaling:
  - Serverless platforms automatically scale your application based on demand, whether it's a single request or thousands per second.

- ### Pay-Per-Use:
  - You only pay for the actual execution time of your code, measured in milliseconds or seconds.
  - No cost is incurred when your code is not running.


<br>

## How Does Serverless Work?

- **Write Code**: You write a small piece of code (called a function) that performs a specific task.

- **Choose a Trigger**: You define an event that will invoke your function. For example:
  - An HTTP request triggers your function.
  - A file upload to cloud storage triggers your function.

- **Deploy to the Cloud**: Deploy your code to a serverless platform like AWS Lambda, Azure Functions, or Google Cloud Functions.

- **Cloud Provider Executes**:
  - When the trigger occurs, the cloud provider runs your function in a managed environment.
  - After execution, the environment is torn down.

## Examples of Serverless Platforms

- **AWS Lambda**: Runs code in response to events from AWS services like S3 or DynamoDB.
- **Azure Functions**: Microsoft’s serverless platform for running event-driven code.
- **Google Cloud Functions**: Google’s solution for serverless execution.

## Usecases for Serverless

- Real-time data processing.
- User triggered actions on a website (like sending welcome emails on signup).
- Backend logic for mobile apps.
- Image resizing on upload.
- Scheduled tasks and chatbots.
