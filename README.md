# README
Setting up HTTP docker with static IP.

- Docker image: `httpd:latest`
- IP address: 172.16.233.0
- Network device: en0


```bash
# Creating the network with bridge adapter on 172.16.233.0 subnet
docker network create -d bridge --subnet=172.16.233.0/24 --gateway=172.16.233.1 my_own_network

# Assign IP address: 172.16.233.10 to the container
docker run --rm --net my_own_network --ip 172.16.233.10 -p 172.16.233.10:80:80 httpd:latest

# Attach IP to the 'actual' network device, so we can access them on our network
sudo ip addr add 172.16.233.10/24 dev en0
```

- Access the site on http://172.16.233.10/

![image](https://github.com/yosep-tenly/static-ip-docker-httpd/assets/41761997/d8630919-c276-49e0-b514-41ca6bcc3b1d)
