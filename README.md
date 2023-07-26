# Traefik Proxy

```
cp sample-docker-compose.yaml docker-compose.yaml
```

I use Cloudflare as my DNS provider. This configuration is used to reach out to cloudflare to create a TLS certificate that I use within my network. 



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


