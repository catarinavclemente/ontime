# Docker

### Detaching Without Stopping <a href="#detaching-without-stopping" id="detaching-without-stopping"></a>

Docker supports a keyboard combination to gracefully detach from a container. Press Ctrl-P, followed by Ctrl-Q, to detach from your connection.

You’ll be dropped back into your shell but the previously attached process will remain alive, keeping your container running. You can check this by using `docker ps` to get a list of running containers.

**Docker installation and configuration guide for EC VPN and proxy:**

[https://citnet.tech.ec.europa.eu/CITnet/confluence/display/DEVSECOPS/1.+Docker+HowTo](https://citnet.tech.ec.europa.eu/CITnet/confluence/display/DEVSECOPS/1.+Docker+HowTo)

{% embed url="https://docs.docker.com/config/pruning/" %}
