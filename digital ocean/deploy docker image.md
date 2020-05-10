# Deploy Docker Image

1, First generate a personal access token in your API area of digital ocean.

2, Create a droplet:

```bash
docker-machine create --digitalocean-size "s-1vcpu-1gb" --digitalocean-region lon1 --driver digitalocean --digitalocean-access-token <access-token> nginx-test-1
```

3, All being well, this will create a droplet. You can verify this by typing:

```bash
docker-machine ls
```

4, Connect to the new droplet:

```bash
eval $(docker-machine env nginx-test-1)
```

5, Run your container:

```bash
docker run -d -p 80:80 nginx
```

6, Get the IP:

```bash
docker-machine ip nginx-test-1
```

7, View in browser.