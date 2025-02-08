---
share: "true"
---

[gcloud CLI](https://cloud.google.com/cli) is an excellent way to manage and work with your Google Cloud resources (VMs, storage buckets, databases and more) right within your terminal.

## Initial Setup
Download and install the gcloud CLI for your operating system. See the install instructions [here](https://cloud.google.com/sdk/docs/install)

Once it is properly installed, set up your credentials:

```bash
gcloud auth login
```

Set your project ID:

```bash
gcloud config set project [PROJECT_ID]
```

Note: gcloud CLI is already installed on VM instances and the cloud shell on Google Cloud Console. If you want to use the gcloud CLI in these environments, there's no need for an installation.
## A few useful commands

There's a nice [cheatsheet](https://cloud.google.com/sdk/docs/cheatsheet) giving a good overview of the CLI commands. Here's a few commands that I've personally found really useful so far :

### `gcloud compute ssh`

You can `ssh` in to your VM instances using the `gcloud compute ssh` command. Example usage:

```bash
gcloud compute ssh [USERNAME]@[VM_INSTANCE_NAME]
```

Docs : [gcloud compute ssh](https://cloud.google.com/sdk/gcloud/reference/compute/ssh)

### `gcloud compute scp`

Use `gcloud compute scp` for copying files to and from Google Compute Engine virtual machines via `scp`

- Copying a file from your local device to your VM instance:

```bash
# copies the local source file to the specified destination on your VM
$ gcloud compute scp [SOURCE_FILE] [USER]@[VM_INSTANCE_NAME]:[REMOTE_DEST]
```


- Downloading a file from a VM instance to your local device
```bash
# downloads a specified file from your VM to a local destination
gcloud compute scp [USER]@[VM_INSTANCE_NAME]:[REMOTE_DEST] [SOURCE_DEST]
```

Docs : [gcloud compute scp](https://cloud.google.com/sdk/gcloud/reference/compute/scp)

## `gcloud storage`

Using `gcloud storage` commands, you can create and manage Cloud Storage buckets and objects. If you're familiar with the standard unix commands like : `ls`, `cp`, `mv`, `rm`, then `gcloud storage` commands will feel right at home for you.

A few examples:

- List the contents of a storage bucket:
```bash
$ gcloud storage ls gs://my-bucket
```

- Copy all text files from a bucket into your current local directory:
```bash
gcloud storage cp gs://my-bucket/*.txt .
```

- For copying a full directory to your bucket, you need to use the `--recursive` option. For example: the following command recursively copies the videos directory to your bucket
```bash
gcloud storage cp --recursive videos gs://my-bucket
```

- To remove a specific object from your bucket you can use the `gcloud storage rm` command:
```bash
gcloud storage rm gs://my-bucket/my-object
```

Docs : [glcoud storage](https://cloud.google.com/sdk/gcloud/reference/storage)
