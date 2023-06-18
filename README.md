## TastyCookCloud
### Prerequisites

You need following tools for [TastyCookBackend](https://github.com/TastyCook/TastyCookBackend) and TastyCookCloud projects:
1. [Chocolatey](https://docs.chocolatey.org/en-us/)

Chocolatey is a software management solution for Windows. Open your cmd with admin access and paste this command:
```bash
@"%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe" -NoProfile -InputFormat None -ExecutionPolicy Bypass -Command "[System.Net.ServicePointManager]::SecurityProtocol = 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))" && SET "PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin"
```

2. [Docker](https://www.docker.com/)

We use Docker to containerise our application and ship it to Kubernetes cluster.
Install it with choco:
```bash
choco install docker-desktop
```

This will install Docker desktop application and start docker daemon
in the background.

3. [Kubernetes CLI](https://kubernetes.io/)

Kubernetes CLI is needed to connect to remote AKS cluster.

```bash
choco install kubernetes-cli
```

4. [Make](https://www.gnu.org/software/make/manual/make.html)

We use Makefile to run tasks.

```bash
choco install make
```

5. [Azure CLI](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli-windows?tabs=powershell)

You need Azure CLI to connect to remote AKS cluster.
To install the Azure CLI using PowerShell, start PowerShell as administrator and run the following command:
```bash
$ProgressPreference = 'SilentlyContinue'; Invoke-WebRequest -Uri https://aka.ms/installazurecliwindows -OutFile .\AzureCLI.msi; Start-Process msiexec.exe -Wait -ArgumentList '/I AzureCLI.msi /quiet'; Remove-Item .\AzureCLI.msi
```

### Test server

1. Open [TastyCookBackend](https://github.com/TastyCook/TastyCookBackend) project.
2. Run `make docker-start` in the root of the project.
3. Docker containers should launch and be accessible from these ports:
   * recipes-api: http://localhost:9001
   * users-api: http://localhost:9002
   * products-api: http://localhost:9003

### [Connect to AKS cluster](https://learn.microsoft.com/en-us/azure/aks/learn/quick-kubernetes-deploy-cli#connect-to-the-cluster)

1. Login to AKS:
    ```azure
    az login
    ```
2. Get credentials:
    ```azure
    az aks get-credentials --resource-group tastygroup --name tastycook
    ```
3. Test that you are connected:
    ```bash
    kubectl get nodes
    ```
    Expected output:
    ```bash
    NAME                                STATUS   ROLES   AGE     VERSION
    aks-agentpool-19222163-vmss000005   Ready    agent   8d      v1.25.6
    aks-agentpool-19222163-vmss00000b   Ready    agent   7d15h   v1.25.6
    ```
