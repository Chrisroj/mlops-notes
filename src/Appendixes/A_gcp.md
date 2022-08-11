# VM Instance in GCP


Before to create an instance in GCP we need to generate a SSH key(if you want to know what SSH is you can check this [video](https://www.youtube.com/watch?v=RMS5zBYQIqA)). In your local console(in my case in Git Bash in windows) follow:

You can watch this [video](https://www.youtube.com/watch?v=ae-CV2KfoN0) or follow the next instructions.

1. **Create SSH keys:**

    Create(if you don't have) and go to ```~/.ssh``` directory and type:

```bash
ssh-keygen -t rsa -f KEY_FILENAME -C USER -b 2048
```
    Example:

```bash
ssh-keygen -t rsa -f gcp_ssh -C w10 -b 2048
```

[Source](https://cloud.google.com/compute/docs/connect/create-ssh-keys)

2. **Put this SSH key in GCP:**
    
    1. Copy public key:
    
        ```bash
        cat KEY_FILENAME.pub
        ```
        Example:
        ```bash
        cat gcp_ssh.pub
        ```
    2. In Cloud console go to **Metadata** -> **EDIT** -> **SSH keys** -> **Add item** -> **Paste public key** -> **Save**
    
_[Source](https://cloud.google.com/compute/docs/connect/add-ssh-keys)_
    
3. **Create VM Instance:**

    In Cloud console go to **Compute Engine** -> **VM Instances** -> **Create Instance** config the VM as:
    * name: `mlops-zoomcamp-vm`
    * region: `us-west4 (Las Vegas)`, zone: `us-west4-b`
    * serie: `E2`, type: `e2-standard-4`
    * boot disk image: `Ubuntu 22.04 LTS` boot disk type: `balanced persistent disk` size(gb): `30`
    
4. **Connect to VM Instance:** 

    Go to ```~./.ssh``` directory and locate the ```config``` type ```nano ~/.ssh/config```copy and paste:

```bash
Host mlops-zoomcamp-vm
    HostName EXTERNAL_IP
    User USER
    IdentityFile KEY_FILENAME_DIRECTORY
    LocalForward PORT_1 IP:PORT_1
    LocalForward PORT_2 IP:PORT_2
    LocalForward PORT_3 IP:PORT_3
```
  
    Example:

```bash
Host mlops-zoomcamp-vm
    HostName 34.125.197.156
    User w10
    IdentityFile C:\Users\w10\.ssh\gcp_ssh
    LocalForward 8888 localhost:8888
    LocalForward 5000 127.0.0.1:5000
    LocalForward 4200 0.0.0.0:4200
```


    The EXTERNAL_IP can change every time you power one the VM. 
Now you can type `ssh mlops-zoomcamp-vm` in your console and you'll get connected to the VM.

**Note0**: In step 4 in ```config``` file the last two lines are to forward multiple port through the same host, in this case 
```LocalForward 8888 localhost:8888``` is for jupyter, ```LocalForward 5000 127.0.0.1:5000``` is for MLflow and ```LocalForward 4200 0.0.0.0:4200``` is for Prefect. You can add more LocalForward if you want.

**Note1**: Don't forget to power off the VM after your work you can use ```sudo poweroff```. 

**Note2**: if you get the next warning:
```bash
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@    WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!     @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
```
Then copy and paste the EXTERNAL_IP of your VM and type:

```bash
ssh-keygen -R "34.125.105.3"
```