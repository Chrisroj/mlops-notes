# Install Dependencies

Now we need to install the next dependencies(you can update the links for Anaconda and Docker Compose):

- **Install Anaconda**:

```bash
cd ~
wget https://repo.anaconda.com/archive/Anaconda3-2022.05-Linux-x86_64.sh
bash Anaconda3-2022.05-Linux-x86_64.sh
```

- **Install Docker**:

```bash
sudo apt update
sudo apt install docker.io
```

- **Install Docker Compose**

```bash
mkdir soft
cd soft/
wget https://github.com/docker/compose/releases/download/v2.5.0/docker-compose-linux-x86_64 -O docker-compose
chmod +x docker-compose
```

- **Modified PATH Varibles**


   Type `cd` to return to the original directory and type ```nano .bashrc```, copy and paste the next at the end of the `.bashrc` file

```bash
export PATH="${HOME}/soft:${PATH}"
```

Type `source .bashrc`, now everything that is in `/soft` directory will be in the PATH then you can execute it everywhere.

- **Add current user to docker group**

```bash
sudo usermod -aG docker $USER
logout
```

Then logback to the VM.

- **Verify Installation**

```bash
which python
# /home/ubuntu/anaconda3/bin/python

which docker
# /usr/bin/docker

which docker-compose
# /home/ubuntu/soft/docker-compose

docker run hello-world
```

- **Run Jupyter Notebook**

```bash
jupyter notebook
```
