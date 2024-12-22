# What is Serverless?

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

## Advantages of Serverless

- **Reduced Operational Complexity**:
  - Developers don’t need to manage infrastructure.
  - Focus is entirely on writing business logic.

- **Cost Efficiency**:
  - No need to pay for idle servers; you only pay for active usage.

- **Scalability**:
  - The platform scales your application automatically based on demand.
 
- **Faster Time-to-Market**:
  - With no infrastructure to manage, development is faster.


## Challenges of Serverless

- **Cold Starts**:
  - Serverless functions may take time to initialize when invoked after being idle, causing delays.
 
- **Vendor Lock-In**:
  - Functions are often tied to a specific cloud provider, making it hard to migrate.

- **Debugging and Monitoring**:
  - Debugging serverless applications can be challenging due to their distributed nature.

- **Limited Execution Time**:
  - Many platforms have maximum execution time limits for functions (e.g., 15 minutes in AWS Lambda).
 
<br>

## Example: Building a Serverless Application

**Scenario**

You want to build an API that returns weather information when requested.

### Steps:

- **Write Code**: Create a serverless function to fetch weather data from an API.

  python file
  ```
  def get_weather(event, context):
      import requests
      city = event.get("queryStringParameters", {}).get("city", "London")
      response = requests.get(f"https://api.weatherapi.com/v1/current.json?key=API_KEY&q={city}")
      return {
          "statusCode": 200,
          "body": response.json()
      }
  ```

- **Choose Trigger**: Use an HTTP trigger to call the function via an HTTP request.

- **Deploy to Azure Function**:
  - Upload the function to Azure Function.
  - Attach an API Gateway to handle HTTP requests.
 
- **Test**:
  - Make a request to the API Gateway URL: ```https://api.example.com/weather?city=Paris```.
 
<br>
<br>

## Serverless in Azure

In Azure, serverless computing is a cloud computing model where Microsoft Azure handles the infrastructure, scaling, and management, allowing developers to focus solely on writing and deploying code. Azure provides several serverless services designed to simplify building, deploying, and managing applications without the need to manage servers or virtual machines.

- ### Azure Functions
  - **What it is**: A serverless compute service for running small pieces of code (functions) in response to events or triggers, such as HTTP requests, timer schedules, or changes in a storage account.
    
  - **Use Cases**:
    - Process HTTP requests (APIs).
    - Perform scheduled tasks (e.g., cleanup jobs).
    - React to changes in Azure Storage or Service Bus.
      
  - **Example**: A function that resizes images when uploaded to Azure Blob Storage.
 

- ### Azure Logic Apps
  - **What it is**: A serverless workflow automation tool for integrating apps, data, and services.
    
  - **Use Cases**:
    - Automate workflows, such as sending an email when a file is uploaded.
    - Connect multiple services (e.g., Salesforce, Office 365, Twitter).

  - **Example**: A workflow that monitors tweets about your company and sends a notification to Slack.
 
- ### Azure Event Grid
  - **What it is**: A fully managed event routing service that connects event sources to subscribers.
 
  - **Use Cases**:
    - Build event-driven architectures.
    - Trigger Azure Functions or Logic Apps on events.
   
  - **Example**: Send notifications to a monitoring system when new resources are created in Azure.
 
- ### Azure Kubernetes Service (AKS) with Virtual Nodes
  - **What it is**: Allows you to run serverless containers in Azure Kubernetes Service.

  - **Use Cases**:
    - Run containers without managing cluster infrastructure.

  - **Example**: Deploying a microservice that scales automatically based on demand.
 
- ### Azure Container Instances (ACI)
  - **What it is**: A service for running containers on-demand without managing virtual machines.

  - **Use Cases**:
    - Quick deployment of containerized applications.

  - **Example**: Running a one-time batch job to process data.


## How Does Serverless Work in Azure?

- **Write Your Code or Workflow**:
  - Write code for Azure Functions or define workflows in Logic Apps.
  - Select the event or trigger that starts your code or workflow.

- **Deploy to Azure**:
  - Deploy your code or workflow to Azure using the Azure Portal, Azure CLI, or DevOps tools.

- **Azure Manages Infrastructure**:
  - Azure automatically provisions the necessary compute resources to run your code.
  - It scales up or down based on the demand for your application.

- **Execute on Demand**:
  - Your application runs only when triggered by an event.
  - After execution, Azure releases the resources, so you’re not paying for idle time.
