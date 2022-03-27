<h1>To Install Python 3, Python modules </h1>
https://www.python.org/

<pre>
sudo apt update
sudo apt -y upgrade

python3 -V

sudo apt install -y python3-pip
sudo apt install unzip

python3 -m pip install jsonpath-ng
</pre>
<hr></hr>
<h2>To Install Docker</h2>

https://docs.docker.com/engine/install/ubuntu/#installation-methods

<pre>
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
</pre>

Test docker installation
<br>
sudo docker run hello-world
<br>
<p>
Post installation steps for Linux.
Add current user to docker group
https://docs.docker.com/engine/install/linux-postinstall/
<pre>    
sudo usermod -aG docker $USER  
newgrp docker
</pre>

Configure Docker to start on boot
<pre>
sudo systemctl enable docker.service;
sudo systemctl enable containerd.service;
</pre>
