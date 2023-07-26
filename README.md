# Traefik Proxy

## Quickstart

```
cp sample-docker-compose.yaml docker-compose.yaml
```

I use Cloudflare (CF) as my DNS provider. This configuration is used to reach out to cloudflare to create a TLS certificate that I use within my network. 

Update your `docker-compose.yaml` to include environment variables for you CF account and DNS API Token (create this in CF).

Make note of the labels and adjust accordingly.

### Bootstrap Authentication and Password

- [Follow this tutorial](https://technotim.live/posts/traefik-portainer-ssl/#generate-basic-auth-password)

### Update the volumes to reflect your server's directory

for example,

![image](https://github.com/andygodish/traefik-docker/assets/33811239/217d53d6-351a-4902-8050-cfa3adb865a8)

### Run 

```
docker compose up -d
```


### Create Proxy Doccker Network

```
docket network create proxy
```

---

### data/acme.json

This is the file that CF will write the certificate to. You just need to supply a blank `acme.json` file and give it adequate permissions.

```
touch ./data/acme.json
chmod 600 ./data/acme.json
```

### data/traefik.yml

Provides Traefik-specific configurations. 

I'm place the server running the Traefik reverse proxy infront of other servers on my network that are implementing self-signed certificates. 

Since we are running this on docker, we use that as the provider and bind to the docker socket. 

Certificate Resolver is where Cloudflare is defined as the certificate issuer. 

### docker-compose

This is where you pass in your cloudflare API key. 


