---
layout: post
title: >-
  M365 - SharePoint Syntex - Classify, Extract Metadata, Apply Contentype and Retain documents automatically.
published: true
featured-image: ../images/posts/6/Create-Model.png
tags: [6, SharePoint, PowerAutomate, Compliance, Syntex]
---

After the recent announcement about the SharePoint Syntex, I started looking into how to utilise SharePoint Syntex capability for my day to day work to manage all the documents (Statements, Expenses etc), classify and retain it easily as soon as the document is scanned and uploaded using the PowerApp and PowerAutomate.

### SharePoint Syntex Setup

Get the SharePoint Syntex licence for the tenant.

<img src="../images/posts/6/SharePoint-Syntex-Product.png" width="50%" height="50%">

#### Create a Content Centre

Create a new "Content Center" site.

<img src="../images/posts/6/Content-Center-Template.png" width="50%" height="50%">

Go to the Content Centre site

<img src="../images/posts/6/Content-Center-Site.png" width="50%" height="50%">

### Create a model

Once the content centre is ready, Create a model 'Expenses' to train some sample content for classification, extraction and apply it to a document library.

<img src="../images/posts/6/Create-Model-1.png" width="80%" height="80%">

The above creates the model with a new Intelligent Document content type.

<img src="../images/posts/6/Model-ContentType.png" width="80%" height="80%">

Train, Classify, Extract Metadata and Publish the model to a library.

<img src="../images/posts/6/Create-Model.png" width="80%" height="80%">

#### Add example files

Upload a list of sample documents to the model.

<img src="../images/posts/6/Sample-Model-Files.png" width="40%" height="40%">

#### Classify files and run training

Classify the uploaded sample files for the type 'Expenses'.

<img src="../images/posts/6/Train_Classify_files.png" width="70%" height="70%">

#### Create and Train Extractors

Create an Extractor 'Total' to get the Total amount from the expenses document and Train it with the sample uploaded documents.

<img src="../images/posts/6/Create-Extractor-Train.png" width="70%" height="70%">

The above step will extract the data and store it as a metadata in the document library.

#### Apply model to libraries

Apply the model to a document library by selecting the site and the document library.

<img src="../images/posts/6/Apply-Model-Library.png" width="70%" height="70%">

The applied model can be removed from the model dashboard page.

<img src="../images/posts/6/Model-Libraries.png" width="70%" height="70%">

Once the model is applied to the document library, it publishes the 'Expenses' model content type with the additional metadata like 'Classification Date', 'Confidential Score' and along with the 'Total' extracted metadata specified in the model.

<img src="../images/posts/6/Library-ContentTypes.png" width="70%" height="70%">

Now we have the model created and applied to a document library ready to classify and extract the data.

### Create a powerapp to scan and upload the document

Create a PowerApp / PowerAutomate (based on <a target='_blank' href='https://www.youtube.com/watch?v=3QaiM8SeWfM'>Shane Young - PowerApp video</a>) to scan and upload the document to the above library.

<img src="../images/posts/6/powerapp-scan.png" width="70%" height="70%">

Link the below PowerAutomate to upload to upload the scanned document.

<img src="../images/posts/6/powerautomate-scan.png" width="70%" height="70%">

### Scan and Upload the document

Now lets scan the document and upload it to the document library.

#### Scan the document
<img src="../images/posts/6/powerapp-syntex-scan.png" width="20%" height="20%">

#### Upload the document to the SharePoint library
<img src="../images/posts/6/model-document-upload.png" width="70%" height="70%">

#### Document classified and metadata extracted based on the model configuration

Once the document is uploaded to the document library, the model will scan and extract the metadata accordingly.
In this case, it has automatically extracted the Total amount spend on the expenses and update the 'Total' metadata column and updates the content type as 'Expenses'

<img src="../images/posts/6/model-document-classified.png" width="70%" height="70%">

### Retain document based on the Content Type

The above can also be used to apply the retention label to the document based on the model so that the contents can be retained based on the type of document.

#### Set the Retention label on the model

The model can be set to apply label at the time of classification as below.

<img src="../images/posts/6/model-retentionlabel.png" width="70%" height="70%">

Once it is configured, the retention label is applied at the time of classification.

<img src="../images/posts/6/document-sample-with-retention.png" width="70%" height="70%">
