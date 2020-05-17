---
layout: post
title: >-
  Azure - Functions - Connect to an OnPremise endpoints - Hybrid Connection Manager
published: true
tags: [4, Azure, Azure Functions, Hybrid Connections, Azure Relay]
---

I was looking into some of the options available to connect to the onpremise endpoints from Azure for an O365 solution. Azure Hybrid Connection is one them and here we will see how to set it up to connect to an sample api hosted locally (OnPremise) from the Azure function.

### Azure Hybrid Connection
This uses the Azure Service Bus Relay capability to establish a secure connection between the systems. One of the key benefit of using this is easy to setup and it uses and the connections are all outbound over standard ports. More details of the Hybrid Connection can be found <a href='https://docs.microsoft.com/en-us/azure/app-service/app-service-hybrid-connections'>here</a>.

### Setup
Here we will see some of the key steps to setup the connection between an OnPremise system hosting an api.

#### OnPremise API Setup:
For this scenario, setup the below end points with the self-signed certificates on my local machine as detailed below.

1. https://localhost:44369/api/cities
   
   returns: ["London","Madras"]

2. https://localhost:5001/WeatherForecast
   
   returns:[{"date":"2020-05-10T11:32:37.2718655+01:00","temperatureC":-8,"temperatureF":18,"summary":"Hot"}..]

#### Azure Functions:
Implement a Azure Function to call the above api and return the combined output.

<script src="https://gist.github.com/clientbala/8788e77b3053b1f9f9be54e813f3a9d4.js"></script>

#### Azure Hybrid Connection Manager Setup:
Download the Azure Hybrid Connection Manager from the Hybrid Connections sections panel by clicking the "Download connection Manger".

<img src="../images/posts/4/4-Azure-HybridConnection-Mgr-Download.png" width="80%" height="80%">

#### Add a new Hybrid Connection:
Configure a new hybrid connection for the first endpoint -  https://localhost:44369/api/cities .

<img src="../images/posts/4/4-Azure-HybridConnection-Create-New.png" width="30%" height="30%">

Once the connection is created, it will be ready to connect to the specified end point as below.

<img src="../images/posts/4/4-Azure-HybridConnection-NotConnected.png" width="80%" height="80%">

#### Azure Relay:
Adding a new Hybrid connection creates a new Azure relay resource, creates an hybrid connection and gets associated with the Azure Functions.

<img src="../images/posts/4/4-Azure-Relay-HybridConnection.png" width="80%" height="80%">

#### Install and Setup the Azure Hybrid Connection Manager:
Download the Azure Hybrid Connection Manager from the Hybrid Connections sections panel by clicking the "Download connection Manger".

<img src="../images/posts/4/4-Azure-HybrigConnection-Create-Connection-OnPremise.png" width="50%" height="50%">

Once the setup is completed, the status will be changed to "Connected".

<img src="../images/posts/4/4-Azure-Connection-Connected.png" width="80%" height="80%">

#### Setup and Configure for the second endpoint:

The second endpoint - https://localhost:5001/weatherforecast can be configured the same by following the above steps or by adding the connection directly to the existing Azure relay.

a. Add a new hybrid connection in the existing relay

<img src="../images/posts/4/4-Azure-Relay-NewConnection.png" width="80%" height="80%">

b. Add the hybrid connection in the Azure Functions

<img src="../images/posts/4/4-Azure-Add-Existing-Connection.png" width="100%" height="100%">

c. Configure the connection locally on the Hybrid Connection Manager

<img src="../images/posts/4/4-Azure-onpremise-weatherforecast.png" width="75%" height="75%">

d. Check the connection status in the Azure function

<img src="../images/posts/4/4-Azure-Connection-Connected.png" width="75%" height="75%">

### Run the function:

<img src="../images/posts/4/4-Azure-functions-test-e2e.png" width="75%" height="75%">

Important Notes:

1. TCP Port 9350 - 9354 is open to connect to the ServiceBus from the client.