<p align="center">
<img src="img/Banner-ignite-25.png" alt="decorative banner" width="1200"/>
</p>

# [Microsoft Ignite 2025](https://ignite.microsoft.com)

## 🔥LAB520: Start, Get, and Stay Resilient for your mission critical applications and infrastructure in Azure's operations platform.

### Session Description

Understand the Start, Get, and Stay Resilient journey and get equipped with the tools & insights to architect your mission critical applications with Azure’s Resiliency and Configuration experiences. Assess your resiliency posture, apply recommendations, validate your posture, and orchestrate recovery. With the Essentials Machine Management bundle from Azure, manage and maintain the state of your resources, enforce configurations across devices, and ensure resilience is not a one-time goal but an ongoing state. 

### 🧠 Learning Outcomes

By the end of this session, learners will be able to:

- Start Resilient: Begin your resiliency journey by creating application-aware service groups and assigning goals aligned to your business objectives
- Get Resilient: Evaluate and improve your resiliency posture by deploying recommendations and fixing architectural drifts (Copilot)
- Stay Resilient: Keep your infrastructure resilient by applying baseline configuration recommendations, enforcing policies to maintain the expected state.

### 💻 Technologies Used

1. Azure Operations Center
1. Azure Resilency Center
1. Azure Backup
1. Azure Policy
1. Azure Machine Configuration

## Content Owners
<table>
<tr>
    <td align="center"><a href="http://github.com/mikekinsman">
        <img src="https://github.com/StevenBucher98.png" width="100px;" alt="Steven Bucher"
"/><br />
        <sub><b> Steven Bucher
</b></sub></a><br />
            <a href="https://github.com/mikekinsman" title="talk">📢</a> 
    </td>
    <td align="center"><a href="http://github.com/akarshprabhu">
        <img src="https://github.com/akarshprabhu.png" width="100px;" alt="Akarsh Prabhu
"/><br />
        <sub><b>Akarsh Prabhu
</b></sub></a><br />
            <a href="https://github.com/Akarsh Prabhu" title="talk">📢</a> 
    </td>
</tr></table>

## Start, Get, and Stay Resilient with Azure

---

Simulate the journey of a financial services firm, **Contoso**, deploying an insurance claims processing application on **Azure** with a focus on:

- **Infrastructure Resiliency**
- **Data Resiliency**
- **Cyber Resiliency**

By the end of this lab, Contoso will:

- 🌐 Meet **zonal resiliency goals**, ensuring high availability even during Azure infrastructure or zonal outages.
- ✅ Have a **fully backed-up and protected** claims processing application.
- 🛡️ Be **resilient to ransomware attacks** through intelligent recovery point tagging and threat detection.

---

## Overview

**Contoso**, a leading financial services firm, embarks on modernizing its claims processing system by leveraging **Microsoft Azure**.

---
> [!TIP]
> - **Credentials** for logging into the system and into Azure are on the **Resources tab** beside the Instructions tab that you are currently on. <br>

# Exercise 0: Onboarding to Operations Center Essentials Machine Management

### 🎯 Goal

Onboard your subscription to the essential machine management services within operations center. This bundle which helps manage the configuration and compliance of your environment. The enrollment provides the following to all machines within the subscription enrolled:

- Azure Update Manager periodic assessments
- Machine Change Tracking and Inventory
- Machine Configuration and the Azure Security Baseline policy
- Azure Monitoring insights

This will help you manage machines in your infrastructure to keep them up to date, configured correctly and compliant with your organization's security and best practice standards.

#### Instructions:

1. Go to *https://aka.ms/OperationsCenterLab* and navigate to **Operations Center → Configuration → Machine Enrollment**.
2. In the middle of the page, select **Enable**.
3. Let's start with the scope of enablement
    1. Select the subscription to onboard, there should be only one
    2. Select User assigned managed identity, **"Lab520-ManagedIdentity"**.
    3. Click **Next: Configure**
4. Next let's configure the enrollment
    1. Select **"Lab520-LogAnalytics"** for the Log Analytics workspace used to capture inventory and change data for your machines
    2. Select **"Lab520-MonitoringWorkspace"** for the Azure Monitoring workspace for all monitoring data.
    3. Click **Next** and keep the Security default selections.
    4. Click **Next** and **Enable**
5. Now your subscription is enrolled in the **Essentials Machine Management** bundle. It will take time to provision so let's continue with getting your application and infrastructure resilient.

---

# Exercise 1: Data Resiliency - Resource-Level Protection

### 🎯 Goal

Ensure backup coverage for critical resources to meet compliance requirements.

---

### 🏢 Contoso's Approach

Contoso begins by enabling **Azure Backup** for its **Storage Accounts** (Azure Blob), ensuring that all scanned documents and logs are protected.The **Virtual Machines (VMs)** are already backed up, completing the resource-level data protection strategy.

---

### 🛠️ Task 1: Create a Backup Policy

1. Go to *https://aka.ms/OperationsCenterLab* in the browser.
2. Navigate to the **Operations Center → Resiliency → Backup+Recovery** section in the left TOC.
3. Navigate to the **Protection Policies** tab
4. Select **+Create Policy** and choose **Create backup policy**
5. On the **Start: Create Policy** page:
    - Select the **Datasource type** as **Azure Blobs (Azure Storage)**.
    - Click **Continue**.
6. On the **Create Backup Policy** page:
    - Under the **Basics** tab:
        - Enter a **Policy name**.
        - From **Select vault**, choose `Contoso-App-BackupVault` to associate this policy.
        - Click **Next: Schedule + retention**.
7. On the **Schedule + retention** tab:
    - Either keep the defaults or Edit the **Backup scehdule and Retention settings** of the data store.
    - esnure both **Operational** and **Vaulted backup** are selected.
8. Click **Review + create**.
9. Once the review is successful, click **Create**.
10. You can view the created policy on the Protection policy tab. Make sure to set the datasource type to Azure Blobs (Azure Storage). 

---

### 🛠️ Task 2: Create Vaulted Backup for Blob

1. Navigate to **Resiliency > Backup + Recovery** section in the left TOC from Operations Center
2. In the Backup + Recovery tab, navigate to **+ Configure Protection**
3. On the **Configure protection** pane:
    - Under **Resources managed by** choose **Azure**
    - Under the **Datasource type** choose **Azure Blobs (Azure Storage)**.
    - Choose the solution as **Azure Backup** to configure protection.
4. On the **Configure Backup** page:
    - Under the **Basics** tab:
        - Choose **Azure Blobs (Azure Storage)** as the Datasource type.
        - Select `Contoso-App-BackupVault` to associate with your storage accounts as the **Vault**.
5. Review the **Selected backup vault details**, then click **Next**.
6. On the **Backup policy** tab:
    - Select the backup policy you created as part of Task 1.
7. Review the **Selected policy details**, then click **Next**.
8. On the **Datasources** tab:
    - Click on Add/Edit
    - Select any of the storage account starting with **zonalstg*** to backup.
        - Validation might take a minute or two
    - If you get an error regarding missing permissions, grant the required permissions by selecting the datasource and clicking on 'Assign missing roles'

9. Once validation succeeds, go to the **Review + configure** tab.
10. Review the details and click **Next** to initiate the **Configure Backup** operation.
11. You can view the configured backup on the datasource in the **Protected items** tab. Make sure to set the datasource type to Azure Blobs (Azure Storage). 

---


## Exercise 2: Infra Resiliency

### 🎯 Goal

Contoso's claims processing application is now zonally resilient, ensuring high availability.

---

### 🛠️ Task 1: Create a Service Group for ClaimsApp

Contoso bundles all components of the ClaimsApp into a **Service Group** to manage zonal resiliency.

#### Instructions:

1. Search for **Service Groups** in the portal search bar.
2. Click **+ Create service group** to start creating a new group.
3. Fill in the required information:
    - **Service Group Name**: Unique identifier for the group. Ex: **ClaimsAppSG**
    - **Display Name**: Friendly name shown in the portal. Ex: **Claims App Service group**
    - **Parent**: Use **Tenant root service group** as the parent.
4. Click **Next**.
5. Click on **+ Add members**
6. Select members of the Service Group and select resources. Include all resources of type 
    - Virtual machine 
    - Disk 
    - Application gateway 
    - Load balancer 
    - Azure Database for PostgreSQL flexible server
7. Click on **Next**, review the details and proceed to Create the service group by clicking on **Review and create**.
8. You can view the created service group in the Operations center as part of the next task.


> ✅ By the end of this task, you will have created a Service Group representing Contoso's ClaimsApp, ready for resiliency evaluation.

---

### 🛠️ Task 2: Assign Resiliency Goals & Review Posture

Contoso uses **Operations Center** to monitor and manage resiliency.

#### Instructions:

1. Go to *https://aka.ms/OperationsCenterLab* in the browser.
2. Navigate to the **Operations Center → Resiliency → Service Group Resiliency** section in the left TOC.
3. Locate the service group that your created **Ex: ClaimsApp Service Group**.
4. To assign Resiliency goals, click **Goals not assigned** in the table:
    - Review the **Goals assignment blade**.
    - Click **Assign Goals** to enable **Zonal Resiliency Goals**.
5. After the assignment:
    - View **Resiliency Status** and **Zonally Resilient Resources**.
    - If marked **Not Resilient**, click **View Recommendations**.

> 🔍 Example: The **PGSQL DB** in ClaimsApp is not zonally resilient.

---

### 🛠️ Task 3: Action on Resiliency Recommendations to Make ClaimsApp Zonally Resilient

1. As part of the previous task, you have clicked **View recommendations** for the Non Resilient Service group in **Operations Center → Resiliency → Service Group Resiliency**
2. Select any recommendation to open the **Recommendation Details** page:
    - View impacted resource(s).
    - Understand why the recommendation was raised.
    - Review **cost implications** (High, Medium, Low).
    - Follow **step-by-step remediation guidance** to resolve the issue, or mark the resource as **exempt** or **manually attested**.

> 💡 **Note**: Azure Advisor now includes preview features that show qualitative cost indicators (High, Medium, Low) with explanations to help assess potential cost increases.

>[!Important] 
> 🛠️ If your lab was launched recently, recommendations take upto 24 hours to reflect. Please extend the life of your lab and come back to test the remaining steps in this exercise. On the day of the event, lab will be auto provisioned 24 hrs in advance

4. In the **Recommended Action** section:
    - Click **Copilot Action**.
    - Follow the Copilot prompts to generate a script that makes the **PGSQL DB** zonally resilient.

---

### 🧪 Run the Script in Azure PowerShell

1. Open **Cloud Shell** in the Azure portal.
2. Select the **PowerShell** option.
3. Choose **No storage account required**.
4. Select your **subscription** and click **Apply**.
5. Once Cloud Shell is ready:
    - Paste the script.
    - Wait for it to complete.

> ✅ After completion, the **PGSQL DB** should be zonally resilient.

---

### Exercise 3: Cyber Resiliency

### 🎯 Goal

Contoso's claims processing app is now resilient to cyber threats, with enhanced visibility and recovery capabilities.

---

### 🛡️ Contoso's Approach

Contoso uses **Microsoft Defender for Cloud (MDC)** to scan its **Virtual Machines (VMs)**.**Azure Backup** intelligently tags recovery points as **Clean** or **Suspicious**, enabling confident recovery from ransomware attacks using verified clean snapshots.

---


### 🛠️ Task 1: Enable Threat Detection

1. Enable **Defender for Servers P1 or P2** on your subscription:
    - Search for **Defender for Cloud** from the Azure portal.
    - Navigate to **Management > Environment settings** 
    - Click on **Expand all** to select your subscription at the bottom of the heirarchy.
    - Under **Cloud workload protection**, ensure that **Servers** has either **Plan 1** or **Plan 2** enabled. If not, set the Status to '**On**' and click on **Save**.
2. Search for **Recovery services vaults** on the portal. Go to **Contoso-App-RSVault**.
3. Under **Settings**, go to **Properties**.
4. In the **Security settings** section:
    - Locate the **Threat Detection** setting and ensure it is Configured. 

---

### 🛠️ Task 2: Create On-Demand Backup and Validate Tagging


1. Go to **Protected Items > Backup items** in the vault, Click on **Azure Virtual Machine** and select **Contoso-AppVM3**.
2. Click on **View details** on the backup item pertaining to the **Contoso-AppVM3**.
3. Click **Backup now** to initiate an on-demand backup.
> It will take upto 30 minutes for the vaulted restore point to show up post the on-demand backup. You can look for any existing restore point in the meanwhile to continue. The restore point needs to be of Recovery type **Snapshot and Vault-Standard**

4. Once the **Backup Recovery Point (RP)** is created:
    - Navigate to the **Recovery Points** section. This can be found by clicking on *View details* on the *Backup items* page for your VM. 
    - Identify the **health status** of the backup RP.

---

## Exercise 4: Infra Compliance and Configuration

### 🎯 Goal

Now that you have your Infrastructure resilient, let's ensure your resources meet compliance requirements. This includes checking if your machines' configurations are properly set and comply with the Azure Security baselines and additional policies. First, familiarize yourself with the **Configuration** page, see what stands out, and explore the table of contents of Configuration.

---

### 🛠️ Task 1: Analyze the baseline rules and assignments

The Contoso application leverages the Azure Security Baselines to **maintain compliance and be secure**.

#### Instructions:

1. Go to **Operations Center → Configuration → Configuration** and familiarize yourself with this page.
2. In order to keep your infrastructure resilient, you want to ensure all your machines are meeting the **Azure Security Baseline** requirements, your progress can be seen under the **Baseline compliance** block of the page.
3. To view all the recommendations to apply to your machine click on the **View Details** button within the **Baseline compliance page**.
4. Navigate to the **Baselines** tab to see all of the rules that are assessed.
5. Let's make your machine more resilient by keeping it from accessing network drives and drive redirection, in the filter search bar at the top of the page, search for **"Do not allow drive redirection"**
6. Click on the name of the baseline rule **Do not allow drive redirection** to open up a page with more details about this rule.
7. Close this overview by clicking the "X" at the top right of the page.
8. Now click on the **View Machines** item in the column **Details**, this page shows which machines are compliant or not.
9. Choose **Contoso-AppVM3** to navigate to the machines page.
10. Under the **Operations** table of contents go to the **Run Command** page and choose to **RunPowerShellScript**
11. In the editor that opens, paste below and run it:

```powershell
#  Disable Drive Redirection
#  This script modifies the registry to enforce the "Do not allow drive redirection" policy.

#  Define the registry path and value
$regPath = "HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services"
$regName = "fDisableCdm"
$regValue = 1  # 1 = Disable drive redirection, 0 = Enable drive redirection

#  Check if the registry path exists, create it if not
if (-not (Test-Path $regPath)) {
    New-Item -Path $regPath -Force | Out-Null
}

#  Set the registry value
Set-ItemProperty -Path $regPath -Name $regName -Value $regValue

#  Confirm the change
Write-Output "Drive redirection has been disabled successfully."

#  This will restart the Guest Configuration Service for re-evaluating the policy.
Get-Service GCService | Restart-Service
```

11. The guest configuration agent is restarted and will re-evaluate if that policy still is within compliance or not. It can take between 15-30 minutes to reflect in the portal. However once it does evaluate you can navigate back to the Operations Center > Configuration > Machine Configuration > Baselines page and search for the same rule **"Do not allow drive redirection"**, you should see number of machines compliant increase by one!


> ✅ By the end of this task, you have familiarized yourself with the Configuration section of Operations Center and have explored the recommendations Azure Security Baseline rule has applied and remediated a task successfully!

Thank you for completing this lab and learning how to be more resilient on Azure!

## Contributing

This project welcomes contributions and suggestions.  Most contributions require you to agree to a
Contributor License Agreement (CLA) declaring that you have the right to, and actually do, grant us
the rights to use your contribution. For details, visit [Contributor License Agreements](https://cla.opensource.microsoft.com).

When you submit a pull request, a CLA bot will automatically determine whether you need to provide
a CLA and decorate the PR appropriately (e.g., status check, comment). Simply follow the instructions
provided by the bot. You will only need to do this once across all repos using our CLA.

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/).
For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or
contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments.

## Trademarks

This project may contain trademarks or logos for projects, products, or services. Authorized use of Microsoft
trademarks or logos is subject to and must follow
[Microsoft's Trademark & Brand Guidelines](https://www.microsoft.com/legal/intellectualproperty/trademarks/usage/general).
Use of Microsoft trademarks or logos in modified versions of this project must not cause confusion or imply Microsoft sponsorship.
Any use of third-party trademarks or logos are subject to those third-party's policies.
