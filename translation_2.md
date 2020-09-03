# Translation 2

## Google Cloud Platform Fundamentals - Core Infrastructure
### Module: GCP Fundamentals: Getting Started with Compute Engine 

1.  __Objectives__

- Create a Compute Engine virtual machine using the Google Cloud Platform (GCP) Console.
- Create a Compute Engine virtual machine using the gcloud command-line interface.
- Connect between the two instances.


__Task 1. Create a Compute Engine virtual machine using the Google Cloud Platform (GCP) Console.__

Set your zone
```
gcloud config set compute/zone us-central1-b

```
To create a VM instance called my-vm-1 in that zone, execute this command:    
 ```
  gcloud compute instances create "my-vm-1" \
--machine-type "n1-standard-1" \
--image-project "debian-cloud" \
--image "debian-9-stretch-v20190213" \
--subnet "default" \
--tags http-server

  ```
  __Task 2. Create a virtual machine using the gcloud command line__
  
  To create a VM instance called my-vm-2 in that zone, execute this command:   
  
```
gcloud compute instances create "my-vm-2" \
--machine-type "n1-standard-1" \
--image-project "debian-cloud" \
--image "debian-9-stretch-v20190213" \
--subnet "default"

```

 __Task 3. Connect between VM instances__
 
- Use the `ping` command to confirm that my-vm-2 can communicate with my-vm-1
Connect to my-vm-2:
```
gcloud compute ssh my-vm-2

```
Ping my-vm-1 from my-vm-2
```
ping -c 3 my-vm-1

```
Use the ssh command to open my-vm-1 from my-vm-2
```
ssh my-vm-1

```
Now ping my-vm-2 from my-vm-1
```
ping -c 3 my-vm-2

```