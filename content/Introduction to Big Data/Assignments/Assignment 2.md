---
share: "true"
---

**Problem Statement**

This assignment is very similar to the first one. You just need to count the number of lines in a text file placed in a storage bucket. But this time, using [[Cloud Run Functions]] instead of a VM.

**Solution**

We need to write a simple Cloud Function that watches for any file uploads to our bucket and prints out the number of lines in that file.

To start, you can search for Cloud Run Functions and create a new function. For creating a function, two things are required:

1. **Configuration**
	- The basic configuration for the function like function name, region, etc
	- You also need to specify the trigger type, i.e. which kind of events the function will respond to. There are several options like:
		- HTTPS
		- Cloud Storage
		- Cloud Pub/Sub
		- Cloud Firestore
	- Since we want to respond to Cloud Storage events, pick the Cloud Storage trigger.
	- We also need to specify the **event type**:
		- _Object finalized_ : Occurs when a new object is created or overwritten
		- _Object deleted_ : Occurs when an object is deleted
		- _Object archived_ : Occurs when a live version of an object becomes a noncurrent version.
		- _Object metadata updated_ : Occurs when the metadata of an existing object changes
	- Since we're watching for file upload events, we'll pick the _Object finalized_ event. We also need to specify the bucket for which we'll be watching this event.
	- You can also configure the memory, CPU, autoscaling functionality for the function here.
2. **Code**
	- The next step is the actual code of the function itself
	- You need to choose your language of choice and write the function's code
	- Also, note that if your function needs any libraries, you need to specify them in the requirements file. For example, in this case, we'll make use of the `google-cloud-storage` python library in our function so we need to add it to the `requirements.txt` file for the function to work!
	- Add `google-cloud-storage==3.0.0` (latest at the time of writing) in the requirements file.

Once this is done, you can deploy the function!

**Example Function Code**:

```python
import functions_framework
from google.cloud import storage 

# Triggered by a change in a storage bucket
@functions_framework.cloud_event
def count_lines(cloud_event):
    """Count the number of lines in a text file uploaded to a bucket"""

    data = cloud_event.data

    event_id = cloud_event["id"]
    event_type = cloud_event["type"]

    bucket_name = data["bucket"] # bucket name
    file_name = data["name"] # file name of the uploaded file

    client = storage.Client()
    bucket = client.bucket(bucket_name) # get the bucket object
    text_file = bucket.blob(file_name) # get the file object

    text_file_content = text_file.download_as_text()
    lines = text_file_content.split('\n')
    count = len(lines)

    print(f"Event ID: {event_id}")
    print(f"Event type: {event_type}")
    print(f"Bucket: {bucket}")
    print(f"File: {file_name}")
    print(f"The number of lines in the file {file_name} is {count}.")
```

For testing, you can upload a text file to the bucket specified during configuration and check that your deployed function's logs show the number of lines in the uploaded file along with other details like event type and bucket name.

References:
[Tutorial - Using Cloud Functions with Storage Events](https://cloud.google.com/functions/docs/tutorials/storage)








