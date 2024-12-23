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

