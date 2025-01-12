
# Docker Installation Notes

Before installing Docker, you need to understand some important security considerations, especially when dealing with firewall settings.

---

## Firewall Limitations with Docker

When you expose ports from your containers using Docker, these ports bypass your firewall settings, which could lead to security concerns if not managed properly. If you're using a firewall tool like `ufw` (Uncomplicated Firewall) or `firewalld` to control your network security, you should be aware of the following:

### 1.  🔴 Bypassing Firewall Rules 🔴
- When you use Docker to expose a container port, Docker automatically allows network access to that port without consulting your firewall settings.
- This means that any port exposed by Docker could be accessible from outside your system, even if your firewall is set to block traffic on those ports.

**Example:**
If your firewall blocks access to **port `8080`,** **but Docker exposes that same port from a container, Docker will override the firewall rule and allow traffic on port `8080`**.

### 2. Incompatibility with iptables-nft
- Docker is compatible with `iptables-nft` and `iptables-legacy`, but firewall rules created using `nft` (new firewall ruleset) are not supported.
- If your system uses `nft` for packet filtering, Docker might not work as expected, leading to potential security vulnerabilities.

---

### How to Avoid Conflicts:
- Ensure you're using either `iptables` or `ip6tables` for firewall rules.
- Place firewall rules in the `DOCKER-USER` chain to allow Docker to manage your firewall settings correctly.
- If you're using `ufw` or `firewalld`, refer to the respective documentation for detailed instructions on how to configure Docker with these firewalls.

For more details, refer to Docker’s official documentation on [Packet filtering and firewalls](https://docs.docker.com/network/iptables/).

---

## Steps to Install Docker on Ubuntu

### 1. Set Up the APT Repository
To add Docker’s official repository to your system, first ensure your system is ready by installing dependencies:

```bash
sudo apt-get update
sudo apt-get install ca-certificates curl
```

Then, install Docker’s GPG key, which is necessary for secure installations:

```bash
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc
```

Next, add the Docker repository:

```bash
echo   "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu   $(. /etc/os-release && echo "$VERSION_CODENAME") stable" |   sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

Finally, update your APT sources:

```bash
sudo apt-get update
```

---

### 2. Install Docker

To install the latest version of Docker, run:

```bash
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

---

### 3. Verify Docker Installation

Once Docker is installed, verify the installation by running the following command:

```bash
sudo docker run hello-world
```

If the installation is successful, Docker will display a **"Hello from Docker!"** message.

---

## Summary of Key Points:
1. **Firewall Considerations:**
   - Docker bypasses firewall settings for exposed container ports. If you use `ufw` or `firewalld`, Docker might override your firewall rules, so configure your firewall settings properly.
2. **Firewall Compatibility:**
   - Docker works with `iptables-nft` and `iptables-legacy`, but not with `nft`-based rules. Always ensure that firewall rules are placed in the `DOCKER-USER` chain for proper integration.
3. **Installation Steps:**
   - Follow the instructions above to install Docker on your Ubuntu system, including adding the GPG key, repository, and installing Docker's components.


Source: https://docs.docker.com/ , chatgpt
