<h1>To Install Python 3, Python modules </h1>
https://www.python.org/

sudo apt update
sudo apt -y upgrade

python3 -V
Python 3.8.10

sudo apt install -y python3-pip



python3 -m pip install jsonpath-ng

<hr></hr>
<h2>To Install Docker</h2>

https://docs.docker.com/engine/install/ubuntu/#installation-methods

sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release


echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null


 curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg  



sudo apt-get update;
sudo apt-get install docker-ce docker-ce-cli containerd.io;  

Test docker installation
sudo docker run hello-world

Post installation steps for Linux.
https://docs.docker.com/engine/install/linux-postinstall/
sudo usermod -aG docker $USER  
newgrp docker

Add current user to docker group


Configure Docker to start on boot
sudo systemctl enable docker.service;
sudo systemctl enable containerd.service;
