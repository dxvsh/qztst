---
share: "true"
---

Cloud Run functions is a lightweight compute solution for developers to create single-purpose, stand-alone functions that respond to Cloud events without the need to manage a server or runtime environment (serverless).

Using Cloud Run Functions, you can respond to *events* that happen in your cloud environment. For example: a user hitting a URL endpoint, changes made in a database, files being added/deleted in a cloud storage bucket, etc. All of these are examples of events. With Cloud Functions, you can write simple, independent functions that watch for these events and *do something* whenever they're triggered.  

Cloud Functions is a fully managed, serverless solution so you don't need to manage and configure any servers, update software, etc. It also scales automatically based on demand, and resources are provisioned automatically in response to events

Visit the Cloud Run Functions [Overview](https://cloud.google.com/functions/docs/concepts/overview) for an excellent explanation.

Functions can be triggered by:

- HTTP Events
- Google Cloud Products
	- Cloud Storage
	- Cloud Pub/Sub
	- Cloud Firestore
	- Firebase
	- Cloud Logging

Check out the Cloud Run Functions docs [here](https://cloud.google.com/functions/docs)