Install Dependincies

Ruby

mutagen

mutagen-compose

docker-compose

```
console

# Install Dependincies

sudo zypper install Ruby

sudo zypper install python3-docker-compose

wget https://github.com/mutagen-io/mutagen/releases/download/v0.13.1/mutagen_linux_amd64_v0.13.1.tar.gz

tar -xvzf mutagen_linux_amd64_v0.13.1.tar.gz

mv mutagen /usr/local/bin/

wget https://github.com/mutagen-io/mutagen-compose/releases/download/v0.13.1/mutagen-compose_linux_amd64_v0.13.1.tar.gz

tar -xvzf mutagen-compose_linux_amd64_v0.13.1.tar.gz

mv mutagen-compose /usr/local/bin/

# Setup canvas

git clone https://github.com/instructure/canvas-lms.git

cd canvas-lms

# Run startup script

./script/docker_dev_setup.sh

Note the script will ask you to do multiple actions manually

1. dory is not required

2. Fill in the email and password field (This is for the admin account on canvas lms website)

3. DROP tables if there is no exsisting db

4. once the script is finish run 'sudo mutagen-compose up -d'

5. Run docker ps

6. run docker inspect on container image 'canvas-lms_web' (docker inspect <CONTAINER ID>)

7. scroll to the bottom of the command and enter the "IPAddress": <ip-address> into the web browser

8. login
```
