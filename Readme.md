#### 1. Add Kong Helm repo

```
helm repo add kong https://charts.konghq.com
helm repo update
```

#### 2. Install Kong

```
helm install kong-gateway kong/kong \
  --set ingressController.installCRDs=true \
  --set image.repository=kong/kong-gateway \
  --set image.tag="3.2.2.0-alpine" \
  --set proxy.type=NodePort \
  --set proxy.http.nodePort=30000 \
  --set proxy.tls.nodePort=30001
```

#### 3. Setup AuthO

Fill out AuthO Application Settings / Credentials in auth_config.json

It should be located in the src folder

Note the audience value is found in the "APIs" tab when you are looking at your application in the AuthO dashboard

```json
{
  "domain": "<APPLICATION_DOMAIN>",
  "clientId": "<APPLICATION_CLIENTID>",
  "audience": "<APPLICATION_API_IDENTIFIER>"
}
```

When you are looking at your application in the AuthO dashboard, go to the "Credentials" tab and iin the Authentication Method secion, make sure "None" is selected. Other options say "mTLS (CA-signed)", "Client Secret (Post)" , etc.