## ✅ ROUND 1 – TECHNICAL

### 1. What are your daily responsibilities as a DevOps engineer?

> **Answer:**
As a DevOps Engineer, my daily responsibilities include:
- Automating infrastructure provisioning using **Terraform**, **ARM Templates**, and **Azure CLI/gcloud CLI**.
- Managing **Kubernetes clusters (AKS/GKE)**, deploying microservices via **Helm**, and configuring **Istio** for service mesh.
- Building, maintaining, and optimizing **CI/CD pipelines** using **Jenkins**, **Azure DevOps**, and **GitHub Actions** for automated builds, testing, and multi-environment deployments.
- Implementing **monitoring and logging** using **Azure Monitor**, **Log Analytics**, **GCP Stackdriver**, **Grafana**, **ELK Stack**, and **Splunk**.
- Enforcing **security and compliance** via **Azure AD/GCP IAM**, **RBAC**, **Key Vault/Secret Manager**, and integrating **DevSecOps** tools.
- Writing and maintaining **automation scripts** in **Python**, **PowerShell**, and **Bash** for operational tasks like backups, snapshots, and user provisioning.
- Collaborating with Dev, QA, and Ops teams to ensure infrastructure aligns with business goals and SLAs.
- Performing **incident response**, **root cause analysis**, and **change management** to ensure high availability.

*(Source: Resume – Professional Summary, Indiana University Health & Lanvera roles)*

---

### 2. Have you worked with monitoring and logging tools like Prometheus, Grafana, or ELK Stack?

> **Answer:**
Yes, extensively. I’ve implemented comprehensive observability stacks across Azure and GCP environments:
- Deployed **ELK Stack (Elasticsearch, Logstash, Kibana)** for centralized log aggregation and analysis.
- Used **Grafana** with **Prometheus** (in earlier roles) and later with **Azure Monitor Metrics** and **Stackdriver** for real-time dashboards.
- Integrated **Filebeat** and **Logstash** to ship logs from Kubernetes pods and VMs.
- Built custom **Grafana dashboards** correlating infrastructure and application metrics for proactive alerting.
- Used **Azure Application Insights** and **GCP Operations (formerly Stackdriver)** for APM and distributed tracing.
- Configured alerts in **Azure Monitor** and **GCP Alerting Policies** tied to **Slack/email** for incident response.

*(Source: Resume – Monitoring Tools section, Indiana University Health & Lanvera roles)*

---

### 3. Can you describe the CI/CD workflow in your project?

> **Answer:**
In my most recent role at Indiana University Health:
- Developers commit code to **Git (GitHub/GitLab)** → triggers **Jenkins/Azure Pipelines**.
- Pipeline runs **unit tests**, **SonarQube** for code quality, and **Trivy/Snyk** for container vulnerability scanning.
- On success, it builds a **Docker image**, pushes to **Azure Container Registry (ACR)** or **GCP Artifact Registry**.
- Deploys to **AKS/GKE** using **Helm charts** with environment-specific values (dev/stage/prod).
- Implements **canary/blue-green** deployments via **Istio** for zero-downtime releases.
- Post-deployment, runs **integration/smoke tests**.
- On failure, pipeline **auto-rolls back** using Helm rollback or previous stable manifest.
- All stages require **manual approvals** for production.
- Infrastructure changes are deployed via **Terraform** in parallel pipelines with **Terraform Cloud** for state locking and policy checks.

*(Source: Resume – CI/CD, DevSecOps, Blue-Green Deployments, Lanvera & IU Health roles)*

---

### 4. How do you handle the continuous delivery (CD) aspect in your projects?

> **Answer:**
I ensure CD is safe, automated, and auditable:
- **Infrastructure as Code**: All environments provisioned via Terraform/ARM — identical dev/stage/prod.
- **Immutable Artifacts**: Docker images tagged with Git commit SHA — never overwritten.
- **Deployment Strategies**: Use **Helm + Istio** for **canary**, **blue-green**, and **rolling updates** with automatic rollback on health check failure.
- **Gates & Approvals**: Manual approval gates before prod; automated gates using test results and security scans.
- **Observability-Driven**: Deployment success validated via **Application Insights/Stackdriver dashboards** and synthetic tests.
- **Feature Flags**: Sometimes integrated via **Azure App Configuration** or **GCP Feature Flags** for toggling features without redeploying.

*(Source: Resume – DevOps Practices, Lanvera role – Blue-Green Deployments)*

---

### 5. What methods do you use to check for code vulnerabilities?

> **Answer:**
I integrate **DevSecOps** practices into CI/CD:
- **SAST**: **SonarQube** for static code analysis (Java, Python, JS) — blocks builds on critical bugs or tech debt.
- **Container Scanning**: **Trivy**, **Aqua Security**, or **Azure Container Registry vulnerability scanning** to scan Docker images for CVEs.
- **Dependency Scanning**: **OWASP Dependency-Check** or **Snyk** for Maven/Gradle/NPM dependencies.
- **IaC Scanning**: **Checkov** or **tfsec** for Terraform misconfigurations (e.g., public S3 buckets, open security groups).
- **Secrets Detection**: **GitGuardian** or **Azure Key Vault integration** to prevent secrets in code.
- All scans run in pipeline — **fail fast** on critical vulnerabilities.

*(Source: Resume – Lanvera role: “Integrated security tools and vulnerability scanners into CI/CD workflows to enforce DevSecOps best practices.”)*

---

### 6. What AWS services are you proficient in? → CONVERTED TO AZURE/GCP

> **Answer:**
While I don’t have production AWS experience, I am deeply proficient in **Azure and GCP equivalents**:

| AWS Service       | Azure Equivalent             | GCP Equivalent               |
|-------------------|------------------------------|------------------------------|
| EC2               | Azure VMs / Azure App Service | Compute Engine / Cloud Run   |
| S3                | Azure Blob Storage           | Cloud Storage                |
| RDS               | Azure SQL DB / Azure Database for MySQL/PostgreSQL | Cloud SQL                    |
| Lambda            | Azure Functions              | Cloud Functions              |
| IAM               | Azure AD + RBAC              | GCP IAM                      |
| VPC               | Azure VNet                   | VPC Network                  |
| ALB/NLB           | Azure Load Balancer / Application Gateway | GCP Load Balancer            |
| CloudWatch        | Azure Monitor + Log Analytics | GCP Operations (Stackdriver) |
| EKS               | AKS                          | GKE                          |
| CodePipeline      | Azure DevOps Pipelines       | Cloud Build                  |
| Secrets Manager   | Azure Key Vault              | Secret Manager               |
| Route 53          | Azure DNS                    | Cloud DNS                    |

I can map any AWS architecture to Azure/GCP using IaC (Terraform) and have done multi-cloud/hybrid deployments.

*(Source: Resume – Technical Skills, Professional Summary, IU Health & Lanvera roles)*

---

### 7. How would you access data in a Cloud Storage bucket from Account A when your application is running on a VM in Account B? → CONVERTED TO AZURE/GCP

> **Answer:**

#### In Azure:
- Use **Azure RBAC** + **Managed Identity**:
  1. Assign a **Managed Identity** to the VM in Account B.
  2. In Account A’s **Storage Account**, grant **Storage Blob Data Reader** role to that Managed Identity (via Azure AD cross-tenant if needed, or same tenant).
  3. App on VM uses **DefaultAzureCredential()** (Azure SDK) to auth — no keys needed.

#### In GCP:
- Use **Workload Identity Federation** or **Service Account Cross-Project Access**:
  1. Create a **Service Account** in Project A (bucket owner).
  2. Grant **Storage Object Viewer** role on the bucket to a Service Account from Project B (or to a group).
  3. Attach that Service Account to the **Compute Engine VM** in Project B via **Workload Identity** (preferred) or service account key (less secure).
  4. App uses **Application Default Credentials**.

> ✅ Best Practice: Avoid keys — use **Managed Identities (Azure)** or **Workload Identity (GCP)**.

*(Source: Resume – Managed Identities, Azure AD, GCP IAM, IU Health role)*

---

### 8. How do containerization technologies like Docker and Kubernetes simplify application deployment and management?

> **Answer:**
- **Docker**:
  - Packages app + deps into **immutable, portable images** — “build once, run anywhere”.
  - Eliminates “works on my machine” issues.
  - Enables **CI/CD consistency** — same image from dev to prod.
- **Kubernetes (AKS/GKE)**:
  - Automates **deployment, scaling, self-healing** (restarts failed pods).
  - Manages **rollouts/rollbacks** declaratively via YAML.
  - Abstracts infrastructure — devs don’t care if it’s Azure or GCP.
  - Enables **microservices** with service discovery (via Services, Ingress, Istio).
  - Integrates with **HPA, Cluster Autoscaler** for cost efficiency.
  - Centralized **logging (sidecar containers)**, **monitoring (cAdvisor, Prometheus)**.

> In my projects, I used **Helm** for templating and **Istio** for traffic management — reducing deployment complexity by 70%+.

*(Source: Resume – Containerization, Orchestration, IU Health & Lanvera roles)*

---

## ✅ ROUND 2 – TECHNICAL

*(Note: Question 8 is duplicate — already answered above)*

### 9. How can Instance 2, with a static IP, communicate with Instance 1, which is in a private subnet and mapped to a multi-AZ load balancer? → CONVERTED TO AZURE/GCP

> **Answer:**

#### In Azure:
- Instance 1 (private subnet) → fronted by **Internal Azure Load Balancer** (multi-AZ via Availability Zones).
- Instance 2 (static public IP) → must be in same VNet or peered VNet.
- If external: Use **Application Gateway** (Layer 7) or **Public Load Balancer** with **NSG rules** allowing traffic from Instance 2’s IP to the LB frontend IP.
- Backend pool of LB points to Instance 1’s private IP.
- Health probes ensure only healthy instances get traffic.

#### In GCP:
- Instance 1 → behind **Internal TCP/UDP Load Balancer** (regional, multi-zone).
- Instance 2 → if external, use **External HTTP(S) LB** or **TCP Proxy LB**.
- Configure **Firewall Rules** to allow traffic from Instance 2’s static IP to the LB’s frontend.
- Backend service points to Instance Group containing Instance 1.

> ✅ Security: Always use **NSGs (Azure)** / **Firewall Rules (GCP)** to restrict source IPs.

*(Source: Resume – Azure Load Balancer, Application Gateway, GCP Load Balancing, IU Health role)*

---

### 10. For a VM in a private subnet, how can it download packages from the internet without NAT gateway or bastion? → CONVERTED TO AZURE/GCP

> **Answer:**

#### In Azure:
Use **Azure Firewall** with **Network Rules** or **Web Categories**:
- Deploy Azure Firewall in a dedicated subnet.
- Route table on private subnet: 0.0.0.0/0 → Azure Firewall.
- Firewall allows outbound to package repos (apt/yum/pypi) via FQDN tags or IPs.
- No public IP on VM needed.

> Alternative: **Private Endpoints** for Azure Artifacts/Container Registry — but not for public internet.

#### In GCP:
Use **Cloud NAT** (you said “without NAT” — so alternative):
- **Private Google Access** + **VPC Service Controls**:
  - Enable **Private Google Access** on subnet — VMs can reach Google APIs (including package repos like apt.gcp.io) via internal IPs.
  - For non-Google repos: Use **Serverless VPC Access** + **Cloud Functions** to proxy downloads (complex).

> ✅ Reality: **Cloud NAT is the standard**. If banned, use **proxy VM with public IP** (not bastion) in same VNet — route private VM traffic to it.

*(Source: Resume – Azure Firewall, GCP Cloud NAT, Networking, IU Health role)*

---

### 11. What is typical latency for a load balancer, and if high, what monitoring steps?

> **Answer:**
- **Typical Latency**: 1-5 ms for internal LBs, 10-100 ms for external/global LBs (depends on geo, TLS, WAF).
- **Troubleshooting Steps**:
  1. Check **LB Metrics**:
     - Azure: **Metrics in Azure Monitor** — Avg Response Time, Healthy Host Count.
     - GCP: **Cloud Monitoring → Load Balancer metrics**.
  2. Enable **Access Logs**:
     - Azure: Diagnostic Settings → Storage/Log Analytics.
     - GCP: Enable Logging → Cloud Logging.
  3. Check **Backend Health**:
     - Are backend VMs/pods healthy? (CPU, memory, app logs).
     - Are health probes passing? (Check probe config — path, port, interval).
  4. **Network Path**:
     - Use **Network Watcher (Azure)** / **Connectivity Tests (GCP)** to trace route.
  5. **Client-Side**:
     - Use **Application Insights RUM** / **GCP Frontend Monitoring** to see client vs server latency.
  6. **TLS/SSL**: Offload SSL at LB? Cipher mismatch can add latency.

> In IU Health, I reduced LB latency by 40% by tuning health probe intervals and enabling HTTP/2.

*(Source: Resume – Azure Monitor, GCP Stackdriver, Performance Tuning, IU Health role)*

---

### 12. If your app is hosted in Blob Storage/Cloud Storage and users are global, how reduce latency? → CONVERTED

> **Answer:**

#### Azure:
- Enable **Azure CDN** (Standard Microsoft or Verizon tier).
- Point CDN to Blob Storage endpoint.
- Configure **caching rules**, **compression**, **geo-filtering**.
- Use **Azure Front Door** for global routing + WAF + CDN combo.

#### GCP:
- Use **Cloud CDN** + **Cloud Storage**.
- Enable **CDN on Load Balancer** backend bucket.
- Set **TTLs**, **cache keys**, **signed URLs** for private content.
- Use **Multi-Regional Storage** for frequently accessed data.

> Bonus: For static sites, use **Azure Static Web Apps** or **GCP Firebase Hosting** — built-in CDN.

*(Source: Resume – Azure CDN, Front Door, GCP Cloud CDN, Lanvera role)*

---

### 13. Example of a complex automation script you've written?

> **Answer:**
At Lanvera, I wrote a **Python script** to automate **Azure VM snapshot backups + retention**:

```python
from azure.identity import DefaultAzureCredential
from azure.mgmt.compute import ComputeManagementClient
from datetime import datetime, timedelta

def take_snapshot(resource_group, vm_name, location, retention_days=7):
    credential = DefaultAzureCredential()
    compute_client = ComputeManagementClient(credential, subscription_id)

    # Get VM
    vm = compute_client.virtual_machines.get(resource_group, vm_name)

    # Create snapshot config
    snapshot_name = f"{vm_name}-snap-{datetime.now().strftime('%Y%m%d')}"
    snapshot_config = {
        'location': location,
        'creation_data': {
            'create_option': 'Copy',
            'source_uri': vm.storage_profile.os_disk.managed_disk.id
        }
    }

    # Create snapshot
    async_snapshot = compute_client.snapshots.begin_create_or_update(
        resource_group, snapshot_name, snapshot_config
    )
    snapshot = async_snapshot.result()

    # Delete snapshots older than retention_days
    snapshots = compute_client.snapshots.list_by_resource_group(resource_group)
    for snap in snapshots:
        if snap.name.startswith(f"{vm_name}-snap-"):
            snap_date_str = snap.name.split('-snap-')[-1]
            snap_date = datetime.strptime(snap_date_str, '%Y%m%d')
            if datetime.now() - snap_date > timedelta(days=retention_days):
                compute_client.snapshots.begin_delete(resource_group, snap.name)

    return f"Snapshot {snapshot_name} created and old snapshots cleaned."
```

> Also wrote **PowerShell scripts** for **Azure AD user provisioning** and **GCP gcloud scripts** for **GKE node pool scaling**.

*(Source: Resume – Python, PowerShell, Automation, IU Health & Lanvera roles)*

---

### 14. How do you approach troubleshooting and debugging automation scripts?

> **Answer:**
My methodology:
1. **Logging**: Add verbose logging with timestamps — log to file + stdout.
2. **Dry Runs**: Use `--what-if` (ARM), `terraform plan`, or script `--dry-run` flags.
3. **Modularize**: Break scripts into small functions — test each independently.
4. **Error Handling**: Use try/catch (Python/PowerShell) — log exceptions with stack traces.
5. **Version Control**: Track script changes in Git — bisect to find breaking commits.
6. **Environment Isolation**: Test in dev/stage first — never prod.
7. **Monitoring**: Integrate script runs into **Azure Monitor** / **GCP Logging** — alert on failures.
8. **Peer Review**: Mandatory PR reviews for all automation scripts.

> Example: Debugged a failing Terraform apply by enabling `TF_LOG=DEBUG` and found a race condition in NSG rule creation.

*(Source: Resume – Scripting, Automation, Incident Management, IU Health role)*

---

## ✅ ROUND 3 – TECHNICAL

### 15. Which services can be integrated with a CDN? → CONVERTED

> **Answer:**

#### Azure CDN integrates with:
- **Blob Storage** (static websites)
- **App Service** (dynamic content)
- **API Management** (API caching)
- **Media Services** (video streaming)
- **Cloud Services / VMs** (via origin pull)

#### GCP Cloud CDN integrates with:
- **Cloud Storage** (buckets)
- **Compute Engine** (instance groups)
- **GKE** (via Ingress + NEG)
- **Serverless** (Cloud Run, App Engine via Load Balancer)

> Also integrates with **WAF** (Azure Front Door WAF, GCP Armor) and **DDoS Protection**.

*(Source: Resume – Azure CDN, Front Door, GCP Cloud CDN, Lanvera role)*

---

### 16. How to dynamically retrieve VPC details in IaC to create a VM? → CONVERTED + CODE

> **Answer: Using Terraform with Azure**

```hcl
# data source to get existing VNet and subnet
data "azurerm_virtual_network" "existing" {
  name                = "prod-vnet"
  resource_group_name = "network-rg"
}

data "azurerm_subnet" "existing" {
  name                 = "app-subnet"
  virtual_network_name = data.azurerm_virtual_network.existing.name
  resource_group_name  = data.azurerm_virtual_network.existing.resource_group_name
}

# create VM in that subnet
resource "azurerm_linux_virtual_machine" "app_vm" {
  name                = "app-vm-01"
  resource_group_name = "app-rg"
  location            = data.azurerm_virtual_network.existing.location
  size                = "Standard_B2s"
  admin_username      = "adminuser"

  network_interface_ids = [
    azurerm_network_interface.app_nic.id
  ]

  os_disk {
    caching              = "ReadWrite"
    storage_account_type = "Standard_LRS"
  }

  source_image_reference {
    publisher = "Canonical"
    offer     = "UbuntuServer"
    sku       = "18.04-LTS"
    version   = "latest"
  }
}

resource "azurerm_network_interface" "app_nic" {
  name                = "app-nic-01"
  location            = data.azurerm_virtual_network.existing.location
  resource_group_name = "app-rg"

  ip_configuration {
    name                          = "internal"
    subnet_id                     = data.azurerm_subnet.existing.id
    private_ip_address_allocation = "Dynamic"
  }
}
```

> ✅ Same pattern in GCP using `data "google_compute_network"` and `data "google_compute_subnetwork"`.

*(Source: Resume – Terraform, IaC, IU Health role)*

---

### 17. How do you manage unmanaged cloud resources in Terraform?

> **Answer:**
Use **`terraform import`** to bring existing resources under Terraform control:

#### Steps:
1. Write Terraform config (`.tf` file) matching the existing resource.
2. Run `terraform import <resource-address> <cloud-resource-id>`
   - Azure: `terraform import azurerm_resource_group.rg /subscriptions/.../resourceGroups/my-rg`
   - GCP: `terraform import google_compute_network.vpc projects/my-project/global/networks/my-vpc`
3. Run `terraform plan` — should show “no changes” if config matches.
4. From now on, manage via Terraform.

> ⚠️ **Critical**: Import ONLY if you’re sure no one else will modify it manually. Use **Terraform Cloud policy sets** to prevent drift.

*(Source: Resume – Terraform, IaC, IU Health role)*

---

### 18. Prerequisites before importing a VPC in Terraform?

> **Answer:**
1. **Write Config First**: Create `.tf` file with exact settings (name, CIDR, subnets, etc.) of existing VPC.
2. **Initialize Backend**: `terraform init` — state backend (e.g., Azure Storage, GCS) must be configured.
3. **Permissions**: Terraform identity needs **READ + MANAGE** permissions on the VPC (e.g., Network Contributor in Azure, Compute Network Admin in GCP).
4. **No Conflicts**: Ensure no other Terraform state already manages this resource.
5. **Backup State**: Backup `terraform.tfstate` before import — in case of errors.
6. **Validate**: Run `terraform validate` and `terraform plan` after import to confirm no drift.

*(Source: Resume – Terraform, IaC, Best Practices)*

---

### 19. If a Storage Bucket was created via Terraform but someone manually added a policy, how handle via IaC?

> **Answer:**
Terraform will **overwrite** the manual change on next `apply` — because Terraform enforces desired state.

#### To preserve manual policy:
1. **Import Policy into Terraform**:
   - Add the policy block to your `.tf` config.
   - Use `terraform refresh` or re-import if needed.
2. **Use `lifecycle` Ignore Changes** (NOT RECOMMENDED — leads to drift):
   ```hcl
   resource "azurerm_storage_account" "sa" {
     # ... config ...
     lifecycle {
       ignore_changes = [network_rules]
     }
   }
   ```
3. **Best Practice**: **Never allow manual changes**. Enforce via:
   - **Azure Policy** / **GCP Organization Policy** to block non-Terraform changes.
   - **Terraform Cloud Sentinel Policies** to require PR reviews.

> In IU Health, we used **Azure Policy “Deny”** for any storage changes not via Terraform pipeline.

*(Source: Resume – Terraform, Azure Policy, GCP IAM, IU Health role)*

---

### 20. Have you upgraded any Kubernetes clusters?

> **Answer:**
Yes — multiple times in **AKS** and **GKE**:

#### AKS Upgrade:
- Check available versions: `az aks get-upgrades`
- Upgrade control plane first: `az aks upgrade --control-plane-only`
- Then node pools (one at a time): `az aks nodepool upgrade`
- Use **Surge Upgrades** to minimize downtime.
- Test apps after each step.

#### GKE Upgrade:
- Master: `gcloud container clusters upgrade CLUSTER --master`
- Nodes: `gcloud container clusters upgrade CLUSTER --node-pool=POOL`
- Use **Node Auto-Upgrades** for patch versions.

> Always:
- Backup **etcd** (via Velero).
- Test in **dev cluster** first.
- Schedule during **maintenance windows**.
- Notify teams — potential brief pod restarts.

*(Source: Resume – AKS, GKE, IU Health & Lanvera roles)*

---

### 21. How do you deploy an application in a Kubernetes cluster?

> **Answer:**
Standard workflow:
1. **Build Docker Image** → push to **ACR/GCR**.
2. **Write Kubernetes Manifests**:
   - `Deployment.yaml` (replicas, image, resources, probes)
   - `Service.yaml` (ClusterIP/LoadBalancer)
   - `Ingress.yaml` (if external access)
   - `ConfigMap/Secret.yaml` (config, env vars)
3. **Apply via CI/CD**:
   ```bash
   kubectl apply -f deployment.yaml
   ```
   or better — **Helm**:
   ```bash
   helm upgrade --install myapp ./chart --values values-prod.yaml
   ```
4. **Verify**:
   ```bash
   kubectl rollout status deployment/myapp
   kubectl get pods,svc,ingress
   ```

> I always include **liveness/readiness probes**, **resource requests/limits**, and **affinity rules**.

*(Source: Resume – Kubernetes, Helm, IU Health & Lanvera roles)*

---

### 22. How do you communicate with a Jenkins server and a Kubernetes cluster?

> **Answer:**
- **Jenkins → Kubernetes**:
  - Jenkins runs on **VM or container** (even in K8s).
  - Uses **kubectl CLI** or **Kubernetes Plugin**.
  - Authenticates via:
    - **Service Account Token** (mounted in Jenkins pod) — for Jenkins in K8s.
    - **kubeconfig file** (with Azure AD/GCP IAM auth) — for external Jenkins.
  - Executes `kubectl apply`, `helm upgrade`, etc., as build steps.

- **Securing it**:
  - **RBAC**: Jenkins SA has only needed permissions (e.g., `deployment/*`, `service/*` in target namespace).
  - **Network**: Jenkins in same VNet/VPC as cluster — or use **Private AKS/GKE endpoint**.
  - **Secrets**: Store kubeconfig in **Azure Key Vault** / **GCP Secret Manager** — inject via Jenkins Credentials Binding.

*(Source: Resume – Jenkins, Kubernetes, Azure AD, GCP IAM, IU Health role)*

---

### 23. Do you only update Docker images in Kubernetes, or also replicas, storage, CPU?

> **Answer:**
I update **everything** declaratively via GitOps:

- **Docker Image**: Update `image: tag` in Deployment — triggers rolling update.
- **Replicas**: Change `replicas: N` — HPA may override this if enabled.
- **CPU/Memory**: Update `resources.requests/limits` — pods restart with new limits.
- **Storage**: Update PVC size (if VolumeExpansion enabled) or mount new volumes.
- **Config**: Update `ConfigMap` → pods restart or reload via sidecar (e.g., Reloader).

> All changes go through **CI/CD pipeline** → **Git PR** → **Approval** → **Apply**. Never `kubectl edit` in prod.

*(Source: Resume – Kubernetes, HPA, ConfigMap, IU Health role)*

---

## ✅ ADDITIONAL TECHNICAL ROUND QUESTIONS (From your list)

### 1. Explain your CI/CD pipeline design. Tools used and why?

> **Answer:**
Designed for **speed, safety, auditability**:

- **Tools**:
  - **Jenkins** (flexible, plugin-rich) + **Azure DevOps** (for Azure-native teams).
  - **Git** (GitHub/GitLab) — single source of truth.
  - **SonarQube** — code quality gate.
  - **Trivy** — container scanning.
  - **Helm** — Kubernetes deployments.
  - **Terraform** — infra deployments.
  - **Slack** — approvals + alerts.

- **Why**:
  - Jenkins: Mature, supports complex workflows.
  - Azure DevOps: Tight Azure integration, YAML pipelines.
  - Helm: Templating, rollbacks, dependency management.
  - Terraform: Multi-cloud, state management.

> Pipeline Stages: Build → Test → Scan → Deploy Dev → Deploy Stage (auto) → Deploy Prod (manual approval).

*(Source: Resume – CI/CD, Lanvera & IU Health roles)*

---

### 5. How do you integrate SonarQube?

> **Answer:**
In Jenkins pipeline:
```groovy
stage('SonarQube Analysis') {
    steps {
        script {
            withSonarQubeEnv('SonarQube-Server') {
                sh 'mvn sonar:sonar -Dsonar.projectKey=myapp'
            }
        }
    }
}
stage('Quality Gate') {
    steps {
        script {
            timeout(time: 1, unit: 'HOURS') {
                def qg = waitForQualityGate()
                if (qg.status != 'OK') {
                    error "Pipeline aborted due to SonarQube quality gate failure: ${qg.status}"
                }
            }
        }
    }
}
```

> Integrated in **pre-merge** — blocks PR if coverage < 80% or critical bugs found.

*(Source: Resume – Lanvera role: “integrated code quality tools like SonarQube”)*

---

### 6. Write a production-ready Dockerfile? Best practices?

> **Answer:**
```dockerfile
# Use specific tag — NOT latest
FROM openjdk:11-jre-slim@sha256:abc123

# Non-root user
RUN groupadd -r app && useradd -r -g app app
USER app

# Set workdir
WORKDIR /app

# Copy only what’s needed — .dockerignore for node_modules, .git, etc.
COPY --chown=app:app target/myapp.jar .

# Healthcheck
HEALTHCHECK --interval=30s --timeout=3s --start-period=5s --retries=3 \
  CMD curl -f http://localhost:8080/health || exit 1

# Use ENTRYPOINT for immutability
ENTRYPOINT ["java", "-jar", "myapp.jar"]
```

> **Best Practices**:
> - Multi-stage builds (not shown here — for compiled languages).
> - Minimize layers — chain RUN commands.
> - Scan images — Trivy in CI.
> - Sign images — Docker Content Trust.

*(Source: Resume – Docker, Lanvera role)*

---

### 10. What are pods, deployments, services in Kubernetes?

> **Answer:**
- **Pod**: Smallest deployable unit — 1+ containers sharing storage/network. Ephemeral.
- **Deployment**: Manages ReplicaSets → ensures N pod replicas are running. Handles updates/rollbacks.
- **Service**: Network endpoint (ClusterIP, NodePort, LoadBalancer) to access pods — stable IP/DNS.

> Example: Deployment creates 3 nginx pods → Service (LoadBalancer) exposes them externally.

*(Source: Resume – Kubernetes, IU Health role)*

---

### 13. How handle resource limits/requests in Kubernetes?

> **Answer:**
In Deployment YAML:
```yaml
resources:
  requests:
    memory: "64Mi"
    cpu: "250m"
  limits:
    memory: "128Mi"
    cpu: "500m"
```

> **Why**:
> - **Requests**: Scheduler reserves this — ensures pod lands on node with enough resources.
> - **Limits**: Hard cap — pod killed if exceeded (OOMKilled).
> - Use **Vertical Pod Autoscaler (VPA)** to recommend values.
> - Monitor via **Prometheus + Grafana** — adjust based on usage.

*(Source: Resume – Kubernetes, HPA, IU Health role)*

---

### 17. How securely store secrets in pipelines?

> **Answer:**

#### Azure:
- **Azure Key Vault**:
  - Store secrets (passwords, tokens, certs).
  - Jenkins/Azure DevOps uses **Service Connection** with Managed Identity to access.
  - Inject as env vars: `$(KeyVaultSecret)` in Azure Pipelines.

#### GCP:
- **Secret Manager**:
  - Store secrets.
  - Jenkins uses **Workload Identity** or **Service Account Key** (less secure) to access.
  - Inject via `gcloud secrets versions access`.

> Never store secrets in Git or pipeline YAML.

*(Source: Resume – Azure Key Vault, GCP Secret Manager, IU Health role)*

---

### 20. How rollback faulty deployment using Git and CI tools?

> **Answer:**
- **Git Revert**:
  ```bash
  git revert <bad-commit-sha>
  git push origin main
  ```
  → Triggers CI/CD → deploys previous good state.

- **Helm Rollback**:
  ```bash
  helm rollback myapp 1  # revert to revision 1
  ```

- **Terraform**:
  ```bash
  terraform apply -var-file=previous.tfvars
  ```

> **Automated Rollback**: In pipeline — if smoke tests fail → auto-run `helm rollback`.

*(Source: Resume – CI/CD, Rollback, IU Health role)*

---

### 22. Approach to logging and monitoring?

> **Answer:**
**Four Pillars**:
1. **Metrics**: Azure Monitor / GCP Metrics → CPU, memory, HTTP errors.
2. **Logs**: ELK Stack / Azure Log Analytics → app + infra logs.
3. **Traces**: Application Insights / GCP Trace → distributed tracing.
4. **Alerts**: Based on SLOs — e.g., “Error rate > 1% for 5m” → PagerDuty/Slack.

> **Dashboards**: Grafana — single pane for infra + app health.

*(Source: Resume – Monitoring Tools, IU Health role)*

---

### 23. Implemented DevSecOps? Example?

> **Answer:**
Yes — at Lanvera:

- **Shift Left Security**:
  - **Pre-commit**: Pre-commit hooks for secrets scan (GitGuardian).
  - **CI Pipeline**:
    - **SAST**: SonarQube (block on critical).
    - **Container Scan**: Trivy (block on HIGH CVE).
    - **IaC Scan**: Checkov (block on public storage bucket).
  - **CD Gate**: Manual security approval for prod.
- **Runtime**:
  - **WAF** (Azure Front Door / GCP Armor).
  - **Pod Security Policies** (AKS/GKE).

> Result: Reduced critical vulnerabilities by 90% in 6 months.

*(Source: Resume – DevSecOps, Lanvera role)*

---
