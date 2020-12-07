---
layout: post
title: >-
  M365 - PowerAutomate - Clone (Create) Flow and Attach it to a Site using a Flow.
published: true
featured-image: ../images/posts/6/Create-Model.png
tags: [7, M365, PowerAutomate, CreateFlow]
---

Here we will see how to use the PowerAutomate to create a new Flow from a template Flow and attach it to a document library with an ability to maintain the Flow functionality in one place. In this example, we will see how a "Request manager approval for a selected file" template flow can be attached a site and a same mechanism can be applied to any custom Flow.

### SharePoint Template Site and Document Library

Provision a new site and a document library for the template "Request manager approval for a selected file" Flow.

<img src="../images/posts/7/7_SharePoint_Template_Site.png" width="100%" height="100%">

### Create "Request manager approval for a selected file" Flow 

Provision "Request manager approval for a selected file" Flow and attach it to the Document library. This teamplate Flow will be used to create a new instance and attached it to a Site document library.

<img src="../images/posts/7/7_Request_Manager_Approval.png" width="70%" height="70%">

#### Create the template Flow and attach to the Document lirary

The flow can be triggered by an user for a selected document.

<img src="../images/posts/7/7_Attach_Document.png" width="70%" height="70%">

In this scenario, we will use the above Flow to create a new instance based on this template Flow and attach it to a new Site Document library using an another Flow.

#### ApprovedSites List

Create a new SharePoint List "ApprovedSites" containing a list of sites which we need to create a new Flow based on the template Flow and attach it to the Document library.

<img src="../images/posts/7/7_ApprovedSites.png" width="100%" height="100%">

### Create a Flow to clone the template Flow and attach it to the Document library

In this step, we will create a new Flow to clone the template flow to a list to clone the template Flow and attach it to the ApprovedSite Document library as below.

#### Set the Trigger

Attach this flow to the "ApprovedSites".

<img src="../images/posts/7/7_Trigger_ApprovedSites.png" width="100%" height="100%">

This Flow will be triggered everytime a new Approved Site is created in the "ApprovedSites" list.

#### Initialise the variables

Initialise some variables to hold the template FlowDefinition, Connections values.

<img src="../images/posts/7/7_Vars_AttachFlow.png" width="100%" height="100%">

#### Get the "Request manager approval for a selected file" FlowDefinition

<img src="../images/posts/7/7_Get_Flow.png" width="100%" height="100%">

#### Get the FlowDefinition, ConnectionReferences details from the Templated Flow

Set the FlowDefinition, Connections variables with the details from the "GetFlow" action followed by parsing the connections as a JSON and compose the Connections array. These values will be used to create the new flow instance.

<img src="../images/posts/7/7_Vars_Assign_FlowDefinitions_ConnectionRefs.png" width="100%" height="100%">

#### Replace the Trigger Url and the Document Library ID in the templated FlowDefinition

The templated Flow contains the Url of the template Site and the Document library and replace it with the ApprovedSite Url and Document Library.

<img src="../images/posts/7/7_Replace_FlowDefinition_With_ApprovedSite.png" width="100%" height="100%">

#### Create Flow for the ApprovedSite Document Library

Call "Create Flow" actions with the FlowDefintion and ConnectionReferences.

<img src="../images/posts/7/7_CreateFlow_ApprovedSite.png" width="100%" height="100%">

The above sets the FlowDefinition and Connection properties with the updated FlowDefinition (containing the ApprovedSite url and DocumentLibrary Id) and Connection References (using the existing connection).

Note: ConnectionReferencesName is set as - variables('ConnectionArray')?[<<index>>]['connectionName'] and ConnectionReferencesId is set as - variables('ConnectionArray')?[<<index>>]['id'].

### ApprovedSite Flow

Once site is registed in the ApprovedSite, "Create Flow - For Approved Sites" Flow gets executed and creates a Flow on the ApprovedSite based on the templated Flow.

#### Regiser a Site in the "ApprovedSites" List

<img src="../images/posts/7/7_Add_ApprovedSite_Perspective.png" width="100%" height="100%">

#### The configured flow creates a new Flow instance for the ApprovedSite

<img src="../images/posts/7/7_Create_Flow_Execution.png" width="100%" height="100%">

#### The new Flow is attached to the ApprovedSite's Document Library

<img src="../images/posts/7/7_Flow_Perpective_Attached.png" width="100%" height="100%">

Note: The above creates a Flow for a Document Library using the existing connection references and there are certain limits on the PowerAutomate on the number of Flows can be owned by an User or Account. More details on the limit and the work around can be found <a href='https://docs.microsoft.com/en-us/power-automate/limits-and-config' target='_blank'>here</a>.