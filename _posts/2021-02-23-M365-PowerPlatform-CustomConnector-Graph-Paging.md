---
layout: post
title: >-
  M365 - PowerPlatform - Custom Connector to query M365 groups using the graph api in pages from PowerAutomate
published: true
featured-image: ../images/posts/8/PowerPlatform-CustomConnector-Create-Action.png
tags: [8, M365, PowerPlatform, Custom Connector, Graph, API, PowerAutomate, Flow, Page]
---

Here we will see how to Create, Configure and Consume the Custom Connector to query a M365 group members as a paged result using the M365 Graph api.

### Register an Application with a Delegated Group.Read.All permission

First, Register an application for the PowerPlatform Custom connector with the Delegated permission to read the groups.

<img src="../images/posts/8/PowerPlatform-AppReg-Delegated.png" width="100%" height="100%">

### Create a Custom Connector

Create a new custom connector as below with the host as 'graph.microsoft.com'

<img src="../images/posts/8/PowerPlatform-CustomConnector-GeneralInformation.png" width="70%" height="70%">

#### Set the Authentication type

In the Security tab, set the authentication type as below using the details from the registered app.

<img src="../images/posts/8/PowerPlatform-CustomConnector-Security.png" width="70%" height="70%">

#### Update the app with the Custom Connector redirect url

Once the connector is updated, update the app with the redirect url.

<img src="../images/posts/8/PowerPlatform-App-SetRedirectUrl.png" width="80%" height="80%">

### Create a Definition to get the group members

Create an action to get the list of group members as below.

<img src="../images/posts/8/PowerPlatform-CustomConnector-Definition-Action.png" width="80%" height="80%">

#### Test the action

Test the configured "getgroupmembers" action.

<img src="../images/posts/8/PowerPlatform-CustomConnector-Default-Test.png" width="80%" height="80%">

### Amend the action using the Swagger editor to accept the query parameters

Amend the definition to include the additional query parameters required for the graph api to return the list of members for the specified page as below.

<img src="../images/posts/8/PowerPlatform-CustonConnector-Swagger-Graph-Member-Pages.png" width="80%" height="80%">

Sample swagger json:
<script src="https://gist.github.com/clientbala/3daf11e4034b6e5795ba27c7a5d72b18.js"></script>

#### Test the action with the query parameters

<img src="../images/posts/8/PowerPlatform-CustomConnector-Test-With-Pages.png" width="80%" height="80%">

### Create a PowerAutomate

We will create a PowerAutomate to read all the group members in pages and call the same action again with the right token to query members of a group.

#### Add the custom connector action

Include the custom connection action to get group members one at a time as below.

<img src="../images/posts/8/PowerPlatform-CustomConnector-Create-Action.png" width="80%" height="80%">

#### Check for the response and call the same action again with the additional parameters

Get the response and check for the @odata.nextLink in the response.

<img src="../images/posts/8/PowerPlatform-CustomConnector-Flow-Implementation.png" width="80%" height="80%">

#### Call the same action again by passing the token received from the previous response

Get all the members until the last page of members is received.

<img src="../images/posts/8/PowerPlatform-CustomConnector-Flow-NextPages.png" width="80%" height="80%">

### PowerAutomate Result

<a href="../images/posts/8/PowerPlatform-CustomConnector-Result.mov" title="PowerAutomate Custom Connector" target="_blank">
  <img src="../images/posts/8/PowerPlatform-CustomConnector-Video.png" alt="Custom Connector">
</a>




