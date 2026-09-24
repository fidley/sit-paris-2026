# ARC-1 Docker installation

## Pull and run ARC-1

### Powershell
```powershell
docker pull ghcr.io/arc-mcp/arc-1:latest
```

Create `.env.arc1-dev` file containing environmental variables:

```dotenv
SAP_URL=https://your-sap-dev-host:44300
SAP_USER=SAP_USER
SAP_PASSWORD=SAP_USER_PASSWORD
SAP_CLIENT=SAP_CLIENT
SAP_LANGUAGE=EN
SAP_INSECURE=false
SAP_ALLOW_WRITES=true
SAP_ALLOW_DATA_PREVIEW=true
SAP_ALLOW_FREE_SQL=true
SAP_ALLOW_TRANSPORT_WRITES=true
SAP_ALLOW_GIT_WRITES=false
SAP_ALLOWED_PACKAGES=$TMP,Z*
ARC1_ALLOW_HTTP_NO_AUTH=true
```

```powershell
docker run -d --name arc1-dev --restart unless-stopped -p 127.0.0.1:8080:8080 --env-file .env.arc1-dev ghcr.io/arc-mcp/arc-1:latest
```

Verify the container:

```powershell
docker ps --filter name=arc1-dev
docker logs --tail 40 arc1-dev
Invoke-WebRequest http://localhost:8080/health
```

Go to Eclipse and Copilot preferences, MCP Settings and add this server
```json
{
  "servers": {
     "arc1-dev": {
        "url": "http://localhost:8080/mcp"
   }
  }
}
```
After adding press Apply and check the visible tools under arc1-dev MCP
<img width="921" height="844" alt="image" src="https://github.com/user-attachments/assets/5148a927-37ca-4be1-9f21-bf802fec0db9" />

Now let's repeat the steps for QA system. 

Create `.env.arc1-qa` file containing environmental variables:

```dotenv
SAP_URL=https://your-sap-qa-host:44300
SAP_USER=SAP_USER
SAP_PASSWORD=SAP_USER_PASSWORD
SAP_CLIENT=SAP_CLIENT
SAP_LANGUAGE=EN
SAP_INSECURE=false
SAP_ALLOW_WRITES=false
SAP_ALLOW_DATA_PREVIEW=true
SAP_ALLOW_FREE_SQL=true
SAP_ALLOW_TRANSPORT_WRITES=false
SAP_ALLOW_GIT_WRITES=false
SAP_ALLOWED_PACKAGES=$TMP,Z*
ARC1_ALLOW_HTTP_NO_AUTH=true
```
Please notice port difference in the Powershell call
```powershell
docker run -d --name arc1-qa --restart unless-stopped -p 127.0.0.1:8081:8080 --env-file .env.arc1-qa ghcr.io/arc-mcp/arc-1:latest
```

Verify the container:

```powershell
docker ps --filter name=arc1-qa
docker logs --tail 40 arc1-qa
Invoke-WebRequest http://localhost:8081/health
```

Go to Eclipse and Copilot preferences, MCP Settings and add this server
```json
{
  "servers": {
     "arc1-dev": {
        "url": "http://localhost:8080/mcp"
   },
     "arc1-qa": {
        "url": "http://localhost:8081/mcp"
   }
  }
}
```
After adding press Apply and check the visible tools under arc1-qa MCP. Please notice some of the tools like SAPWrite is not visible
<img width="694" height="296" alt="image" src="https://github.com/user-attachments/assets/4373858f-0a4f-4b73-bc23-bc63e75f476a" />

