## How to deploy

### Prerequisites

You need following tools to deploy Tasty Cook correctly:
1. [Chocolatey](https://docs.chocolatey.org/en-us/)

Chocolatey is a software management solution for Windows. Open your cmd with admin access and paste this command:
```bash
@"%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe" -NoProfile -InputFormat None -ExecutionPolicy Bypass -Command "[System.Net.ServicePointManager]::SecurityProtocol = 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))" && SET "PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin"
```

2. [Docker](https://www.docker.com/)

We use Docker to containerise our application and ship it to Kubernetes cluster. Install it with choco:
```bash
choco install docker-desktop
```

This will install Docker desktop application and start docker daemon
in the background which will operate our containers.


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
