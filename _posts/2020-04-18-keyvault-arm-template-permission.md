---
layout: post
title: Azure - KeyVault - set multiple access policies using the ARM template
published: true
---


Azure services is one of the commonly used service to extend / implement any custom M365 functionality like site provisioning, custom governance application etc. 

Here we will quickly see how to setup the access policies in the KeyVault for a multiple service principal registered in the tenant.

#### KeyVault Template - Multiple ServicePrincipal with fixed permission.

The below template takes an array of serviceprincipal object id's and sets a access policies within the KeyVault.


<script src="https://gist.github.com/clientbala/9cba1fc0787c7bb42405992a1bd7782d.js"></script>


#### KeyVault Template - Multiple ServicePrincipal with variable permission.

The below template takes an array of serviceprincipal object id's along with the permission as a Json and sets the access policies accordingly.

<script src="https://gist.github.com/clientbala/9cba1fc0787c7bb42405992a1bd7782d.js"></script>


