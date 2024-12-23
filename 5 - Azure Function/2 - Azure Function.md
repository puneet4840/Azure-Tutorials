# Azure Function

Azure Function is the **cloud-based service** by microsoft that allows you to run small piece of code (called "functions") without worrying about servers and infrastructure.

**Azure Functions** is a **serverless compute service**. Serverless means:
- You write code, and Azure handles infrastructure (servers, scaling, and maintenance).
- The code is triggered by external events or schedules.
- It’s ideal for short-running, event-driven tasks like data processing, event handling, or microservices.

## Why use Azure Functions?

- **Event-Driven**: Functions execute in response to triggers like HTTP requests, timer schedules, or messages in a queue.
- **Scalable**: Automatically scales based on demand.
- **Cost-Effective**: You pay only for the time your function runs.

## Function App Architecture

<img src="https://drive.google.com/uc?export=view&id=14_Q67adSir4Q7wPqIeDHNCB6o5ojfguY" width="500" height="410">

In the above architecture you can see that when we create a Function App on azure the following steps has been followed by azure:
- Select the Azure Data Center based on your region choice.
- It selects a physical server inside the data center.
- Create a Virtual Machine in the physical server based on your choice between Linux or Windows and assign it for function app.
- Create a Function App inside the VM, that is the Serverless. We only able to see our function but azure has create that Function app inside the virtual machine.
- If we want to create multiple same os related function apps so we can create it.

Here, Serverless means there is azure managed server on which you function app is create by azure. Azure scales or de-scales it based on the load on your function app.

This is the concept of serverless.

## Components of Azure Function

- **Function App**:

  The Function App is a container that holds one or more Azure Functions. All functions in a Function App share:
  - Runtime and configurations.
  - Deployment settings.

- **Trigger**:

  Trigger defines how the function is invoked. A trigger is what causes your function to execute. Types include:

  - **HTTP Trigger**: A Function executes when an HTTP request is received.
  - **Timer Trigger**: Function runs based on a scheduled time in cron syntax.
  - **Blob Trigger**: Runs when a new file is uploaded to Azure Blob Storage.
  - **Queue Trigger**: Executes when a message is added to a queue.
 
- **Input Binding**:

  Input bindings provide data to the function when it executes. For example:
  - Reading data from a SQL database or Azure Storage Blob.

- **Output Binding**:

  Output bindings send data from the function to an external service. For example:
  - Writing messages to a queue or saving files to Blob Storage.

- **Runtime**:

  The runtime is the execution environment for Azure Functions, available in:
  - .Net, Python, Java, PowerShell and more.
