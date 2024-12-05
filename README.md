# Install Docker Engine on Ubuntu

# Supported Ubuntu Versions:
- Ubuntu Oracular 24.10
- Ubuntu Noble 24.04 (LTS)
- Ubuntu Jammy 22.04 (LTS)
- Ubuntu Focal 20.04 (LTS)
Supported architectures: x86_64 (amd64), armhf, arm64, s390x, ppc64le (ppc64el).

# Uninstall old versions
Remove conflicting packages before installing Docker Engine
```bash
for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc; do sudo apt-get remove $pkg; done
```
Note: The above command may report no packages found. Docker data in /var/lib/docker/ is not removed automatically.

# Set up Docker apt repository

Add Docker's official GPG key
```bash
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc
```

Add Docker repository
```bash
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```

# If using a derivative like Linux Mint, replace $VERSION_CODENAME with $UBUNTU_CODENAME

Install Docker Engine
```bash
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
Verify installation
```bash
sudo docker run hello-world
```

This downloads a test image and prints a confirmation message if successful.

Tip: If encountering errors running without sudo:
Add your user to the docker group to avoid using sudo for Docker commands:
```bash
sudo groupadd docker
sudo usermod -aG docker $USER
```
# Then restart your shell or log out and back in.
