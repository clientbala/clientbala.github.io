---
layout: post
title: Azure - KeyVault - set multiple access policies using the arm template
published: true
---


In the recent years, Azure services has become the common go to platform to develop, host many small to large enterprise applications and also the commonly used service to extend / implement any custom O365 functionality like site provisioning, custom governance application etc. Azure KeyVault will be one of the heavily used one across all the types of Business solution to store the secret / certificate / keys etc.

Recently, I was involved in implementing a various application for a client where we have to keep some of the secret data like connectionstring for Sql, Access tokens, Instrument keys etc in a single KeyVault. Here we will quickly see how to setup the access policies in the KeyVault for a multiple service principal registered in the tenant using the ARM template.

#### KeyVault Template - Multiple ServicePrincipal with fixed permission.

The below template takes an array of serviceprincipal object id's and sets a access policies within the KeyVault.


<script src="https://gist.github.com/clientbala/9cba1fc0787c7bb42405992a1bd7782d.js"></script>


#### KeyVault Template - Multiple ServicePrincipal with variable permission.

The below template takes an array of serviceprincipal object id's along with the permission as a Json and sets the access policies accordingly.

<script src="https://gist.github.com/clientbala/1b90b10ac15a2777e9910a6acd415d28.js"></script>

#### Template parameters: The paramters value can be passed as below either using the PowerShell / Cli / Azure Devops tasks.

-keyVaultName "kv-cb-set-accesspolicies" -keyVaultLocation "UK South" -servicePrincipalObjects [{"Id":"aaa103ae-9073-4959-97cd-c35b00c6e6e1", "Permissions":{"keys": [],"secrets": ["Get","List"],"certificates":[]}}]

**Example - DevOps:**

<img src="../images/posts/1-DevOps%20-%20Arm%20Template%20-%20KV.png">
