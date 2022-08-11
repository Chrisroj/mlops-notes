# VM Instance in AWS

Before to start working with MLOps you should use a VM instance to work with and setup the environment to work.

You can prepare your environment in your local machine, but in our case we are going to set up a VM instance in AWS. You need to have an AWS account(if you want to do the same in GCP go to [VM Instance in GCP](../Appendixes/A_gcp.md))

1. **Create EC2 instance:**

    Go to EC2 service and click in launch instance(orange button), now config the VM as:
    - Name: `mlops-zoomcamp`
    - Amazon Machine Image: `Ubuntu Server 22.04 LTS (HVM), SSD Volume Type`
    - Architecture: `64-bit (x86)`
    - Instance type: `t2.large`    
    - Create and select a key pair:   
        - Key pair name: `asus-laptop`
        - Key pair type: `RSA`
        - Private key file format: `.pem`
    - Configure Storage: `1x 30 Gib gp2 Root Volume`.HOLI
        


2. **Copy and paste `.pem` file:** 

    When you create a key pair a `.pem` will downloaded automatically, you will have to copy and paste this file to your  `~/.ssh` directory in your local machine.
    
    
3. **Connect to VM Instance:** 

    Go to `~./.ssh` directory and locate the `config` file type nano `~/.ssh/config` copy and paste:
    
    ```bash
    Host mlops-zoomcamp
        HostName EXTERNAL_IP
        User USER
        IdentityFile KEY_FILENAME_DIRECTORY
        LocalForward PORT_1 IP:PORT_1
        LocalForward PORT_2 IP:PORT_2
        LocalForward PORT_3 IP:PORT_3
    ```
    
    **Example:**

    ```bash
    Host mlops-zoomcamp
        HostName 18.117.147.165
        User ubuntu
        IdentityFile C:\Users\ferro\.ssh\asus-laptop.pem
        LocalForward 8888 localhost:8888
        LocalForward 5000 127.0.0.1:5000
        LocalForward 4200 0.0.0.0:4200
    ```
    
    
     
The EXTERNAL_IP can change every time you power one the VM. 
Now you can type `ssh mlops-zoomcamp` in your console and you'll get connected to the VM.

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
ssh-keygen -R EXTERNAL_IP
```

Example:


```bash
ssh-keygen -R "34.125.105.3"
```

[Back to the top](#)

### VS Code Setup <a name="vscode"></a>
If you want to use the VM with a local VS code, follow:

1. Install "Remote - SSH" extension in VS Code
2. Click on "Open a Remote Window" icon on bottom-left corner
3. From dropdown select "Connect to Host" and then select the host name that you put in the `config` file, in this case `mlops-zoomcamp`. That opens a new VSCode window.