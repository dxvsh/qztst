---
share: "true"
---

**Problem Statement**

This week's assignment requires us to spin up a VM and write a program to count the number of lines in a plain text file kept in a Google Cloud Storage bucket.

**Solution**

The task is pretty simple, we just need to spin up a VM and write a python program in it that can access a plain text file placed in a storage bucket and counts the number of lines in it.

To be able to access and fetch the files placed in a storage bucket, we can use [Google Cloud Storage client library](https://cloud.google.com/storage/docs/reference/libraries#client-libraries-install-python). Using it, we can create buckets, download and upload objects to and from our buckets.

```bash
pip install --upgrade google-cloud-storage
```

**Python Code**

```python
from google.cloud import storage

def count_lines(bucket_name, file_name, destination_file_name):
	"""Count the number of lines in the given file"""
	
	# construct a Storage Client object
	client = storage.Client()
	
	# specify bucket name
	bucket = client.bucket(bucket_name)
	
	# specify the blob name to fetch
	blob = bucket.blob(file_name)
	
	# download blob to disk 
	blob.download_to_filename(destination_file_name)
	
	with open(destination_file_name, 'r') as f:
		lines = f.readlines()
		
	print(f"Number of lines in {file_name} : {len(lines)}")
	
if __name__ == "__main__":
	bucket_name = "my-bucket"
	file_name = "my-file.txt"
	destination_file_name = "my-file.txt"
	count_lines(bucket_name, file_name, destination_file_name)	
```

Running this script downloads the specified file to disk and counts the number of lines in it. 

Its interesting to note that since you're running this code on a VM authenticated to your Google Cloud project, you don't need to set up any authentication. The `storage.Client()` calls implicitly uses the Application Default Credentials (ADC), automatically picking up the service account credentials associated with the VM's instance.

If you were running the code outside of a Compute Engine VM (e.g., locally on your machine), this automatic authentication would not work and you'll need to explicitly authenticate as mentioned in the [docs](https://cloud.google.com/storage/docs/reference/libraries#authentication).
