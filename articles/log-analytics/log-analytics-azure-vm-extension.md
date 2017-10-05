---
title: "Azure sanal makineler için günlük analizi bağlanma | Microsoft Docs"
description: "Windows ve Linux sanal Azure'da çalışan makineler için önerilen toplanan günlüklerini ve ölçümleri günlük analizi Azure VM uzantısı yükleyerek yoludur. Azure VM'ler üzerine günlük analizi sanal makine uzantısı yüklemek için Azure portal veya PowerShell kullanın."
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: ewinner
editor: 
ms.assetid: ca39e586-a6af-42fe-862e-80978a58d9b1
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2017
ms.author: richrund
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: cdae291b546fef4d7fdb8b067c8e4f4c9708d43f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="connect-azure-virtual-machines-to-log-analytics-with-a-log-analytics-agent"></a><span data-ttu-id="10546-104">Azure sanal makineler için günlük analizi günlük analizi aracı ile bağlanma</span><span class="sxs-lookup"><span data-stu-id="10546-104">Connect Azure virtual machines to Log Analytics with a Log Analytics agent</span></span>

<span data-ttu-id="10546-105">Windows ve Linux bilgisayarlar için günlükleri ve ölçümleri toplamak için önerilen günlük analizi Aracısı'nı yükleyerek yöntemdir.</span><span class="sxs-lookup"><span data-stu-id="10546-105">For Windows and Linux computers, the recommended method for collecting logs and metrics is by installing the Log Analytics agent.</span></span>

<span data-ttu-id="10546-106">Günlük analizi VM uzantısı aracılığıyla Azure sanal makinelerde günlük analizi Aracısı'nı yüklemek için en kolay yoludur.</span><span class="sxs-lookup"><span data-stu-id="10546-106">The easiest way to install the Log Analytics agent on Azure virtual machines is through the Log Analytics VM Extension.</span></span>  <span data-ttu-id="10546-107">Uzantısını kullanarak yükleme işlemini basitleştirir ve belirttiğiniz için günlük analizi çalışma alanına veri göndermek için aracı otomatik olarak yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="10546-107">Using the extension simplifies the installation process and automatically configures the agent to send data to the Log Analytics workspace that you specify.</span></span> <span data-ttu-id="10546-108">Aracı ayrıca otomatik olarak en son özellikleri ve düzeltmeleri sahip olduktan yükseltilir.</span><span class="sxs-lookup"><span data-stu-id="10546-108">The agent is also upgraded automatically, ensuring that you have the latest features and fixes.</span></span>

<span data-ttu-id="10546-109">Windows sanal makineler için etkinleştirmeniz *Microsoft İzleme Aracısı* sanal makine uzantısı.</span><span class="sxs-lookup"><span data-stu-id="10546-109">For Windows virtual machines, you enable the *Microsoft Monitoring Agent* virtual machine extension.</span></span>
<span data-ttu-id="10546-110">Linux sanal makineleri için etkinleştirmeniz *için OMS Aracısı Linux* sanal makine uzantısı.</span><span class="sxs-lookup"><span data-stu-id="10546-110">For Linux virtual machines, you enable the *OMS Agent For Linux* virtual machine extension.</span></span>

<span data-ttu-id="10546-111">Daha fazla bilgi edinmek [Azure sanal makine uzantıları](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) ve [Linux Aracısı](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="10546-111">Learn more about [Azure virtual machine extensions](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and the [Linux agent](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="10546-112">Aracı tabanlı koleksiyon için günlük verileri kullandığınızda, yapılandırmalısınız [günlük analizi veri kaynaklarında](log-analytics-data-sources.md) günlüklerini ve toplamak istediğiniz ölçümleri belirtmek için.</span><span class="sxs-lookup"><span data-stu-id="10546-112">When you use agent-based collection for log data, you must configure [data sources in Log Analytics](log-analytics-data-sources.md) to specify the logs and metrics that you want to collect.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="10546-113">Kullanarak günlük analizi günlük veri dizini oluşturmak için yapılandırırsanız [Azure tanılama](log-analytics-azure-storage.md)ve aynı günlükleri toplamak için aracısını yapılandırın, ardından Günlükler iki kez toplanır.</span><span class="sxs-lookup"><span data-stu-id="10546-113">If you configure Log Analytics to index log data by using [Azure diagnostics](log-analytics-azure-storage.md), and you configure the agent to collect the same logs, then the logs are collected twice.</span></span> <span data-ttu-id="10546-114">Her iki veri kaynakları için ücretlendirilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="10546-114">You are charged for both data sources.</span></span> <span data-ttu-id="10546-115">Yüklü aracı varsa, yalnızca aracı kullanarak günlük verileri toplamak - Azure tanılama günlük verilerini toplamak için günlük analizi yapılandırmayın.</span><span class="sxs-lookup"><span data-stu-id="10546-115">If you have the agent installed, then collect log data by using only the agent - don't configure Log Analytics to collect log data from Azure diagnostics.</span></span>
>
>

<span data-ttu-id="10546-116">Günlük analizi sanal makine uzantısını etkinleştirmek için üç kolay yol vardır:</span><span class="sxs-lookup"><span data-stu-id="10546-116">There are three easy ways to enable the Log Analytics virtual machine extension:</span></span>

* <span data-ttu-id="10546-117">Azure Portalı'nı kullanarak</span><span class="sxs-lookup"><span data-stu-id="10546-117">By using the Azure portal</span></span>
* <span data-ttu-id="10546-118">Azure PowerShell kullanarak</span><span class="sxs-lookup"><span data-stu-id="10546-118">By using Azure PowerShell</span></span>
* <span data-ttu-id="10546-119">Bir Azure Resource Manager şablonu kullanarak</span><span class="sxs-lookup"><span data-stu-id="10546-119">By using an Azure Resource Manager template</span></span>

## <a name="enable-the-vm-extension-in-the-azure-portal"></a><span data-ttu-id="10546-120">Azure portalında VM uzantısı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="10546-120">Enable the VM extension in the Azure portal</span></span>
<span data-ttu-id="10546-121">Günlük analizi için aracıyı yükleyin ve üzerinde çalıştığı kullanarak Azure sanal makineyi bağlayın [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="10546-121">You can install the agent for Log Analytics and connect the Azure virtual machine that it runs on by using the [Azure portal](https://portal.azure.com).</span></span>

### <a name="to-install-the-log-analytics-agent-and-connect-the-virtual-machine-to-a-log-analytics-workspace"></a><span data-ttu-id="10546-122">Günlük analizi Aracısı'nı yükleme ve sanal makine günlük analizi çalışma alanına bağlayın</span><span class="sxs-lookup"><span data-stu-id="10546-122">To install the Log Analytics agent and connect the virtual machine to a Log Analytics workspace</span></span>
1. <span data-ttu-id="10546-123">[Azure portal](http://portal.azure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="10546-123">Sign into the [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="10546-124">Seçin **Gözat** portal ve sonra Git sol tarafındaki **günlük analizi (OMS)** ve seçin.</span><span class="sxs-lookup"><span data-stu-id="10546-124">Select **Browse** on the left side of the portal, and then go to **Log Analytics (OMS)** and select it.</span></span>
3. <span data-ttu-id="10546-125">Azure VM ile kullanmak istediğiniz bir günlük analizi çalışma alanları, listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="10546-125">In your list of Log Analytics workspaces, select the one that you want to use with the Azure VM.</span></span>  
   ![OMS çalışma alanları](./media/log-analytics-azure-vm-extension/oms-connect-azure-01.png)
4. <span data-ttu-id="10546-127">Altında **oturum analytics Yönetimi**seçin **sanal makineleri**.</span><span class="sxs-lookup"><span data-stu-id="10546-127">Under **Log analytics management**, select **Virtual machines**.</span></span>  
   <span data-ttu-id="10546-128">![Sanal makineler](./media/log-analytics-azure-vm-extension/oms-connect-azure-02.png)</span><span class="sxs-lookup"><span data-stu-id="10546-128">![Virtual machines](./media/log-analytics-azure-vm-extension/oms-connect-azure-02.png)</span></span>
5. <span data-ttu-id="10546-129">Listesinde **sanal makineleri**, aracıyı yüklemek istediğiniz sanal makineyi seçin.</span><span class="sxs-lookup"><span data-stu-id="10546-129">In the list of **Virtual machines**, select the virtual machine on which you want to install the agent.</span></span> <span data-ttu-id="10546-130">**OMS bağlantı durumu** VM, olup olmadığını gösterir **bağlı**.</span><span class="sxs-lookup"><span data-stu-id="10546-130">The **OMS connection status** for the VM indicates that it is **Not connected**.</span></span>  
   <span data-ttu-id="10546-131">![VM bağlı değil](./media/log-analytics-azure-vm-extension/oms-connect-azure-03.png)</span><span class="sxs-lookup"><span data-stu-id="10546-131">![VM not connected](./media/log-analytics-azure-vm-extension/oms-connect-azure-03.png)</span></span>
6. <span data-ttu-id="10546-132">Sanal makineniz için Ayrıntılar seçin **Bağlan**.</span><span class="sxs-lookup"><span data-stu-id="10546-132">In the details for your virtual machine, select **Connect**.</span></span> <span data-ttu-id="10546-133">Aracıyı otomatik olarak yüklenir ve günlük analizi çalışma alanınız için yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="10546-133">The agent is automatically installed and configured for your Log Analytics workspace.</span></span> <span data-ttu-id="10546-134">Bu işlem hangi sırada OMS bağlantısı durumudur birkaç dakika sürer *bağlanıyor...*</span><span class="sxs-lookup"><span data-stu-id="10546-134">This process takes a few minutes, during which time the OMS Connection status is *Connecting...*</span></span>  
   <span data-ttu-id="10546-135">![VM Bağlan](./media/log-analytics-azure-vm-extension/oms-connect-azure-04.png)</span><span class="sxs-lookup"><span data-stu-id="10546-135">![Connect VM](./media/log-analytics-azure-vm-extension/oms-connect-azure-04.png)</span></span>
7. <span data-ttu-id="10546-136">Yükleyip aracısına bağlanmak sonra **OMS bağlantısı** durumunu göstermek için güncelleştirilmeyecek **bu çalışma**.</span><span class="sxs-lookup"><span data-stu-id="10546-136">After you install and connect the agent, the **OMS connection** status will be updated to show **This workspace**.</span></span>  
   <span data-ttu-id="10546-137">![Bağlı](./media/log-analytics-azure-vm-extension/oms-connect-azure-05.png)</span><span class="sxs-lookup"><span data-stu-id="10546-137">![Connected](./media/log-analytics-azure-vm-extension/oms-connect-azure-05.png)</span></span>

## <a name="enable-the-vm-extension-using-powershell"></a><span data-ttu-id="10546-138">PowerShell kullanarak VM uzantısı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="10546-138">Enable the VM extension using PowerShell</span></span>
<span data-ttu-id="10546-139">PowerShell kullanarak sanal makineniz yapılandırdığınızda sağlamanız gereken **Workspaceıd** ve **workspaceKey**.</span><span class="sxs-lookup"><span data-stu-id="10546-139">When you configure your virtual machine by using PowerShell, you need to provide the **workspaceId** and **workspaceKey**.</span></span> <span data-ttu-id="10546-140">Json yapılandırmanızda özellik adları **büyük küçük harfe duyarlı**.</span><span class="sxs-lookup"><span data-stu-id="10546-140">The property names in your json configuration are **case-sensitive**.</span></span>

<span data-ttu-id="10546-141">Kimliğini bulun ve üzerinde anahtar **ayarları** sayfasında OMS portalı veya önceki örnekte gösterildiği gibi PowerShell kullanarak.</span><span class="sxs-lookup"><span data-stu-id="10546-141">You can find the Id and key on the **Settings** page of the OMS portal, or by using PowerShell as shown in the preceding example.</span></span>

![Çalışma alanı kimliği ve birincil anahtar](./media/log-analytics-azure-vm-extension/oms-analyze-azure-sources.png)

<span data-ttu-id="10546-143">Azure Klasik sanal makineleri ve Resource Manager sanal makineleri için farklı komutlar vardır.</span><span class="sxs-lookup"><span data-stu-id="10546-143">There are different commands for Azure classic virtual machines and Resource Manager virtual machines.</span></span> <span data-ttu-id="10546-144">Aşağıda, Klasik ve Resource Manager sanal makineleri için örnekler verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="10546-144">Following are examples for both classic and Resource Manager virtual machines.</span></span>

<span data-ttu-id="10546-145">Klasik sanal makineler için aşağıdaki PowerShell örneği kullanın:</span><span class="sxs-lookup"><span data-stu-id="10546-145">For classic virtual machines, use the following PowerShell example:</span></span>

```PowerShell
Add-AzureAccount

$workspaceId = "enter workspace ID here"
$workspaceKey = "enter workspace key here"
$hostedService = "enter hosted service here"

$vm = Get-AzureVM –ServiceName $hostedService

# For Windows VM uncomment the following line
# Set-AzureVMExtension -VM $vm -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionName 'MicrosoftMonitoringAgent' -Version '1.*' -PublicConfiguration "{'workspaceId': '$workspaceId'}" -PrivateConfiguration "{'workspaceKey': '$workspaceKey' }" | Update-AzureVM -Verbose

# For Linux VM uncomment the following line
# Set-AzureVMExtension -VM $vm -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionName 'OmsAgentForLinux' -Version '1.*' -PublicConfiguration "{'workspaceId': '$workspaceId'}" -PrivateConfiguration "{'workspaceKey': '$workspaceKey' }" | Update-AzureVM -Verbose
```

<span data-ttu-id="10546-146">Resource Manager Linux VM'ler için aşağıdaki CLI kullanma</span><span class="sxs-lookup"><span data-stu-id="10546-146">For Resource Manager Linux VMs using the following CLI</span></span>
```azurecli
az vm extension set --resource-group myRGMonitor --vm-name myMonitorVM --name OmsAgentForLinux --publisher Microsoft.EnterpriseCloud.Monitoring --version 1.3 --protected-settings ‘{"workspaceKey": "<workspace-key>"}’ --settings ‘{"workspaceId": "<workspace-id>"}’ 
```

<span data-ttu-id="10546-147">Resource Manager sanal makineler için aşağıdaki PowerShell örneği kullanın:</span><span class="sxs-lookup"><span data-stu-id="10546-147">For Resource Manager virtual machines, use the following PowerShell example:</span></span>

```PowerShell
Login-AzureRMAccount
Select-AzureRMSubscription -SubscriptionId "**"

$workspaceName = "your workspace name"
$VMresourcegroup = "**"
$VMresourcename = "**"

$workspace = (Get-AzureRmOperationalInsightsWorkspace).Where({$_.Name -eq $workspaceName})

if ($workspace.Name -ne $workspaceName)
{
    Write-Error "Unable to find OMS Workspace $workspaceName. Do you need to run Select-AzureRMSubscription?"
}

$workspaceId = $workspace.CustomerId
$workspaceKey = (Get-AzureRmOperationalInsightsWorkspaceSharedKeys -ResourceGroupName $workspace.ResourceGroupName -Name $workspace.Name).PrimarySharedKey

$vm = Get-AzureRmVM -ResourceGroupName $VMresourcegroup -Name $VMresourcename
$location = $vm.Location

# For Windows VM uncomment the following line
# Set-AzureRmVMExtension -ResourceGroupName $VMresourcegroup -VMName $VMresourcename -Name 'MicrosoftMonitoringAgent' -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionType 'MicrosoftMonitoringAgent' -TypeHandlerVersion '1.0' -Location $location -SettingString "{'workspaceId': '$workspaceId'}" -ProtectedSettingString "{'workspaceKey': '$workspaceKey'}"

# For Linux VM uncomment the following line
# Set-AzureRmVMExtension -ResourceGroupName $VMresourcegroup -VMName $VMresourcename -Name 'OmsAgentForLinux' -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionType 'OmsAgentForLinux' -TypeHandlerVersion '1.0' -Location $location -SettingString "{'workspaceId': '$workspaceId'}" -ProtectedSettingString "{'workspaceKey': '$workspaceKey'}"


```


## <a name="deploy-the-vm-extension-using-a-template"></a><span data-ttu-id="10546-148">Bir şablon kullanarak VM uzantısı dağıtma</span><span class="sxs-lookup"><span data-stu-id="10546-148">Deploy the VM extension using a template</span></span>
<span data-ttu-id="10546-149">Azure Kaynak Yöneticisi'ni kullanarak, dağıtım ve uygulamanızın yapılandırmasını tanımlayan bir şablon (JSON biçiminde) oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="10546-149">By using Azure Resource Manager, you can create a template (in JSON format) that defines the deployment and configuration of your application.</span></span> <span data-ttu-id="10546-150">Bu şablon Resource Manager şablonu olarak bilinir ve dağıtımı tanımlamanın bildirim temelli bir yolunu sunar.</span><span class="sxs-lookup"><span data-stu-id="10546-150">This template is known as a Resource Manager template and provides a declarative way to define deployment.</span></span> <span data-ttu-id="10546-151">Bir şablon kullanarak, sürekli olarak uygulama yaşam döngüsü boyunca uygulamanızı dağıtmak ve kaynaklarınızın tutarlı bir durumda dağıtılması emin olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="10546-151">By using a template, you can repeatedly deploy your application throughout the app lifecycle and have confidence that your resources are being deployed in a consistent state.</span></span>

<span data-ttu-id="10546-152">Günlük analizi aracı, Resource Manager şablonu bir parçası olarak dahil ederek, her bir sanal makine için günlük analizi çalışma alanınız bildirmek için önceden yapılandırılmış olduğundan emin olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="10546-152">By including the Log Analytics agent as part of your Resource Manager template, you can ensure that each virtual machine is pre-configured to report to your Log Analytics workspace.</span></span>

<span data-ttu-id="10546-153">Resource Manager şablonları hakkında daha fazla bilgi için bkz: [Azure Resource Manager şablonları yazma](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="10546-153">For more information about Resource Manager templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="10546-154">Microsoft Monitoring Agent uzantı yüklü Windows çalıştıran bir sanal makine dağıtmak için kullanılan bir Resource Manager şablonu örneği verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="10546-154">Following is an example of a Resource Manager template that's used for deploying a virtual machine that's running Windows with the Microsoft Monitoring Agent extension installed.</span></span> <span data-ttu-id="10546-155">Bu şablon tipik sanal makine şablonu, aşağıdaki eklemelerle şöyledir:</span><span class="sxs-lookup"><span data-stu-id="10546-155">This template is a typical virtual machine template, with the following additions:</span></span>

* <span data-ttu-id="10546-156">Workspaceıd ve workspaceName parametreleri</span><span class="sxs-lookup"><span data-stu-id="10546-156">workspaceId and workspaceName parameters</span></span>
* <span data-ttu-id="10546-157">Microsoft.EnterpriseCloud.Monitoring kaynak uzantısı bölümü</span><span class="sxs-lookup"><span data-stu-id="10546-157">Microsoft.EnterpriseCloud.Monitoring resource extension section</span></span>
* <span data-ttu-id="10546-158">Workspaceıd ve workspaceSharedKey yedekleme aramak için çıkışları</span><span class="sxs-lookup"><span data-stu-id="10546-158">Outputs to look up the workspaceId and workspaceSharedKey</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "adminUsername": {
      "type": "string",
      "metadata": {
        "description": "Username for the Virtual Machine."
      }
    },
    "adminPassword": {
      "type": "securestring",
      "metadata": {
        "description": "Password for the Virtual Machine."
      }
    },
    "dnsLabelPrefix": {
       "type": "string",
       "metadata": {
          "description": "DNS Label for the Public IP. Must be lowercase. It should match with the following regular expression: ^[a-z][a-z0-9-]{1,61}[a-z0-9]$ or it will raise an error."
       }
    },
    "workspaceId": {
      "type": "string",
      "metadata": {
        "description": "OMS workspace ID"
      }
    },
    "workspaceName": {
      "type": "string",
      "metadata": {
         "description": "OMS workspace name"
      }
    },
    "windowsOSVersion": {
      "type": "string",
      "defaultValue": "2012-R2-Datacenter",
      "allowedValues": [
        "2008-R2-SP1",
        "2012-Datacenter",
        "2012-R2-Datacenter",
        "Windows-Server-Technical-Preview"
      ],
      "metadata": {
        "description": "The Windows version for the VM. This will pick a fully patched image of this given Windows version. Allowed values: 2008-R2-SP1, 2012-Datacenter, 2012-R2-Datacenter, Windows-Server-Technical-Preview."
      }
    }
  },
  "variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]",
    "apiVersion": "2015-06-15",
    "imagePublisher": "MicrosoftWindowsServer",
    "imageOffer": "WindowsServer",
    "OSDiskName": "osdiskforwindowssimple",
    "nicName": "myVMNic",
    "addressPrefix": "10.0.0.0/16",
    "subnetName": "Subnet",
    "subnetPrefix": "10.0.0.0/24",
    "storageAccountType": "Standard_LRS",
    "publicIPAddressName": "myPublicIP",
    "publicIPAddressType": "Dynamic",
    "vmStorageAccountContainerName": "vhds",
    "vmName": "MyWindowsVM",
    "vmSize": "Standard_DS1",
    "virtualNetworkName": "MyVNET",
    "resourceId": "[resourceGroup().id]",
    "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',variables('virtualNetworkName'))]",
    "subnetRef": "[concat(variables('vnetID'),'/subnets/',variables('subnetName'))]"
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[variables('storageAccountName')]",
      "apiVersion": "[variables('apiVersion')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "accountType": "[variables('storageAccountType')]"
      }
    },
    {
      "apiVersion": "[variables('apiVersion')]",
      "type": "Microsoft.Network/publicIPAddresses",
      "name": "[variables('publicIPAddressName')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "publicIPAllocationMethod": "[variables('publicIPAddressType')]",
        "dnsSettings": {
          "domainNameLabel": "[parameters('dnsLabelPrefix')]"
        }
      }
    },
    {
      "apiVersion": "[variables('apiVersion')]",
      "type": "Microsoft.Network/virtualNetworks",
      "name": "[variables('virtualNetworkName')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "addressSpace": {
          "addressPrefixes": [
            "[variables('addressPrefix')]"
          ]
        },
        "subnets": [
          {
            "name": "[variables('subnetName')]",
            "properties": {
              "addressPrefix": "[variables('subnetPrefix')]"
            }
          }
        ]
      }
    },
    {
      "apiVersion": "[variables('apiVersion')]",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[variables('nicName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'))]",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
      ],
      "properties": {
        "ipConfigurations": [
          {
            "name": "ipconfig1",
            "properties": {
              "privateIPAllocationMethod": "Dynamic",
              "publicIPAddress": {
                "id": "[resourceId('Microsoft.Network/publicIPAddresses',variables('publicIPAddressName'))]"
              },
              "subnet": {
                "id": "[variables('subnetRef')]"
              }
            }
          }
        ]
      }
    },
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Compute/virtualMachines",
      "name": "[variables('vmName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))]",
        "[concat('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
      ],
      "properties": {
        "hardwareProfile": {
          "vmSize": "[variables('vmSize')]"
        },
        "osProfile": {
          "computername": "[variables('vmName')]",
          "adminUsername": "[parameters('adminUsername')]",
          "adminPassword": "[parameters('adminPassword')]"
        },
        "storageProfile": {
          "imageReference": {
            "publisher": "[variables('imagePublisher')]",
            "offer": "[variables('imageOffer')]",
            "sku": "[parameters('windowsOSVersion')]",
            "version": "latest"
          },
          "osDisk": {
            "name": "osdisk",
            "vhd": {
              "uri": "[concat('http://',variables('storageAccountName'),'.blob.core.windows.net/',variables('vmStorageAccountContainerName'),'/',variables('OSDiskName'),'.vhd')]"
            },
            "caching": "ReadWrite",
            "createOption": "FromImage"
          }
        },
        "networkProfile": {
          "networkInterfaces": [
            {
              "id": "[resourceId('Microsoft.Network/networkInterfaces',variables('nicName'))]"
            }
          ]
        },
        "diagnosticsProfile": {
          "bootDiagnostics": {
             "enabled": "true",
             "storageUri": "[concat('http://',variables('storageAccountName'),'.blob.core.windows.net')]"
          }
        }
      },
      "resources": [
        {
          "type": "extensions",
          "name": "Microsoft.EnterpriseCloud.Monitoring",
          "apiVersion": "[variables('apiVersion')]",
          "location": "[resourceGroup().location]",
          "dependsOn": [
            "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
          ],
          "properties": {
            "publisher": "Microsoft.EnterpriseCloud.Monitoring",
            "type": "MicrosoftMonitoringAgent",
            "typeHandlerVersion": "1.0",
            "autoUpgradeMinorVersion": true,
            "settings": {
              "workspaceId": "[parameters('workspaceId')]"
            },
            "protectedSettings": {
              "workspaceKey": "[listKeys(resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspaceName')), '2015-03-20').primarySharedKey]"
            }
          }
        }
      ]
    }
  ],
  "outputs": {
      "sharedKeyOutput": {
         "value": "[listKeys(resourceId('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName')), '2015-03-20').primarySharedKey]",
         "type": "string"
      },
      "workspaceIdOutput": {
         "value": "[reference(concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName')), '2015-03-20').customerId]",
        "type" : "string"
      }
  }
}
```

<span data-ttu-id="10546-159">Aşağıdaki PowerShell komutunu kullanarak şablonu dağıtabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="10546-159">You can deploy a template by using the following PowerShell command:</span></span>

```PowerShell
New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateFile $templateFilePath
```

## <a name="troubleshooting-the-log-analytics-vm-extension"></a><span data-ttu-id="10546-160">Günlük analizi VM uzantısı sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="10546-160">Troubleshooting the Log Analytics VM extension</span></span>
<span data-ttu-id="10546-161">Genellikle Azure portalında veya Azure powershell şeyler çalışmıyor zaman bir ileti alırsınız.</span><span class="sxs-lookup"><span data-stu-id="10546-161">Usually you receive a message when things don't work, from either Azure portal or Azure powershell.</span></span>

1. <span data-ttu-id="10546-162">[Azure portal](http://portal.azure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="10546-162">Sign into the [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="10546-163">VM bulun ve VM Ayrıntıları'nı açın.</span><span class="sxs-lookup"><span data-stu-id="10546-163">Find the VM and open VM details.</span></span>
3. <span data-ttu-id="10546-164">Tıklatın **uzantıları** için OMS uzantısı veya etkin olup olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="10546-164">Click **Extensions** to check if OMS extension is enabled or not.</span></span>

   ![VM uzantısı görünümü](./media/log-analytics-azure-vm-extension/oms-vmview-extensions.png)

4. <span data-ttu-id="10546-166">Tıklatın *MicrosoftMonitoringAgent*(Windows) veya *OmsAgentForLinux*(Linux) uzantısı ve görünüm ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="10546-166">Click the *MicrosoftMonitoringAgent*(Windows) or *OmsAgentForLinux*(Linux) extension and view details.</span></span> 

   ![VM uzantısı ayrıntıları](./media/log-analytics-azure-vm-extension/oms-vmview-extensiondetails.png)

### <a name="troubleshooting-windows-virtual-machines"></a><span data-ttu-id="10546-168">Sorun giderme Windows sanal makineler</span><span class="sxs-lookup"><span data-stu-id="10546-168">Troubleshooting Windows Virtual Machines</span></span>
<span data-ttu-id="10546-169">Varsa *Microsoft İzleme Aracısı* VM Aracısı uzantısı yükleme değil veya raporlama, sorunu gidermek için aşağıdaki adımları gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="10546-169">If the *Microsoft Monitoring Agent* VM agent extension is not installing or reporting, you can perform the following steps to troubleshoot the issue.</span></span>

1. <span data-ttu-id="10546-170">Azure VM aracısı yüklü olup olmadığını denetleyin ve doğru adımları kullanarak çalışma [KB 2965986](https://support.microsoft.com/kb/2965986#mt1).</span><span class="sxs-lookup"><span data-stu-id="10546-170">Check if the Azure VM agent is installed and working correctly by using the steps in [KB 2965986](https://support.microsoft.com/kb/2965986#mt1).</span></span>
   * <span data-ttu-id="10546-171">VM Aracısı günlük dosyasını gözden geçirebilirsiniz`C:\WindowsAzure\logs\WaAppAgent.log`</span><span class="sxs-lookup"><span data-stu-id="10546-171">You can also review the VM agent log file `C:\WindowsAzure\logs\WaAppAgent.log`</span></span>
   * <span data-ttu-id="10546-172">Günlük mevcut değilse, VM aracısı yüklü değil.</span><span class="sxs-lookup"><span data-stu-id="10546-172">If the log does not exist, the VM agent is not installed.</span></span>
     * [<span data-ttu-id="10546-173">Klasik sanal makinelerin Azure VM Aracısı'nı yükleme</span><span class="sxs-lookup"><span data-stu-id="10546-173">Install the Azure VM Agent on classic VMs</span></span>](../virtual-machines/windows/classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
2. <span data-ttu-id="10546-174">Microsoft Monitoring Agent uzantısı sinyal görev aşağıdaki adımları kullanarak çalışıyor onaylayın:</span><span class="sxs-lookup"><span data-stu-id="10546-174">Confirm the Microsoft Monitoring Agent extension heartbeat task is running using the following steps:</span></span>
   * <span data-ttu-id="10546-175">Sanal makinede oturum açın</span><span class="sxs-lookup"><span data-stu-id="10546-175">Log in to the virtual machine</span></span>
   * <span data-ttu-id="10546-176">Görev Zamanlayıcısı'nı açın ve Bul `update_azureoperationalinsight_agent_heartbeat` görevi</span><span class="sxs-lookup"><span data-stu-id="10546-176">Open task scheduler and find the `update_azureoperationalinsight_agent_heartbeat` task</span></span>
   * <span data-ttu-id="10546-177">Görev etkin ve bir dakikada çalıştığını onaylayın</span><span class="sxs-lookup"><span data-stu-id="10546-177">Confirm the task is enabled and is running every one minute</span></span>
   * <span data-ttu-id="10546-178">Sinyal günlük dosyası iade etme`C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\heartbeat.log`</span><span class="sxs-lookup"><span data-stu-id="10546-178">Check the heartbeat logfile in `C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\heartbeat.log`</span></span>
3. <span data-ttu-id="10546-179">Microsoft İzleme Aracısı VM uzantısı günlük dosyalarını inceleyin`C:\Packages\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent`</span><span class="sxs-lookup"><span data-stu-id="10546-179">Review the Microsoft Monitoring Agent VM extension log files in `C:\Packages\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent`</span></span>
4. <span data-ttu-id="10546-180">Sanal makine PowerShell betikleri çalıştırabilirsiniz emin olun</span><span class="sxs-lookup"><span data-stu-id="10546-180">Ensure the virtual machine can run PowerShell scripts</span></span>
5. <span data-ttu-id="10546-181">C:\Windows\temp izinlerini değiştirmezsiniz emin olun</span><span class="sxs-lookup"><span data-stu-id="10546-181">Ensure permissions on C:\Windows\temp haven’t been changed</span></span>
6. <span data-ttu-id="10546-182">Sanal makine üzerinde yükseltilmiş bir PowerShell penceresinde aşağıdaki komutu yazarak Microsoft Monitoring Agent durumunu görüntüleme`  (New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg').GetCloudWorkspaces() | Format-List`</span><span class="sxs-lookup"><span data-stu-id="10546-182">View the status of the Microsoft Monitoring Agent by typing the following command in an elevated PowerShell window on the virtual machine `  (New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg').GetCloudWorkspaces() | Format-List`</span></span>
7. <span data-ttu-id="10546-183">Microsoft Monitoring Agent Kurulum günlük dosyalarını inceleyin`C:\Windows\System32\config\systemprofile\AppData\Local\SCOM\Logs`</span><span class="sxs-lookup"><span data-stu-id="10546-183">Review the Microsoft Monitoring Agent setup log files in `C:\Windows\System32\config\systemprofile\AppData\Local\SCOM\Logs`</span></span>

<span data-ttu-id="10546-184">Daha fazla bilgi için bkz: [Windows uzantıları sorun giderme](../virtual-machines/windows/extensions-troubleshoot.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="10546-184">For more information, see [troubleshooting Windows extensions](../virtual-machines/windows/extensions-troubleshoot.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

### <a name="troubleshooting-linux-virtual-machines"></a><span data-ttu-id="10546-185">Linux sanal makineleri sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="10546-185">Troubleshooting Linux Virtual Machines</span></span>
<span data-ttu-id="10546-186">Varsa *Linux için OMS aracısının* VM Aracısı uzantısı yükleme değil veya raporlama, sorunu gidermek için aşağıdaki adımları gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="10546-186">If the *OMS Agent for Linux* VM agent extension is not installing or reporting, you can perform the following steps to troubleshoot the issue.</span></span>

1. <span data-ttu-id="10546-187">Uzantı durumu ise *bilinmeyen* Azure VM aracısı yüklü olup olmadığını denetleyin ve doğru VM aracı günlük dosyasını gözden geçirerek çalışma`/var/log/waagent.log`</span><span class="sxs-lookup"><span data-stu-id="10546-187">If the extension status is *Unknown* check if the Azure VM agent is installed and working correctly by reviewing the VM agent log file `/var/log/waagent.log`</span></span>
   * <span data-ttu-id="10546-188">Günlük mevcut değilse, VM aracısı yüklü değil.</span><span class="sxs-lookup"><span data-stu-id="10546-188">If the log does not exist, the VM agent is not installed.</span></span>
   * [<span data-ttu-id="10546-189">Linux VM'ler üzerinde Azure VM Aracısı yükleme</span><span class="sxs-lookup"><span data-stu-id="10546-189">Install the Azure VM Agent on Linux VMs</span></span>](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
2. <span data-ttu-id="10546-190">Linux VM uzantısı günlük dosyaları için sağlıksız diğer durumlar için OMS Aracısı'nı gözden `/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/extension.log` ve`/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/CommandExecution.log`</span><span class="sxs-lookup"><span data-stu-id="10546-190">For other unhealthy statuses, review the OMS Agent for Linux VM extension logs files in `/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/extension.log` and `/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/CommandExecution.log`</span></span>
3. <span data-ttu-id="10546-191">Uzantı durumu iyi değil, ancak veri değil yükleniyor Linux günlük dosyalarında OMS Aracısı gözden geçirin.`/var/opt/microsoft/omsagent/log/omsagent.log`</span><span class="sxs-lookup"><span data-stu-id="10546-191">If the extension status is healthy, but data is not being uploaded review the OMS Agent for Linux log files in `/var/opt/microsoft/omsagent/log/omsagent.log`</span></span>

## <a name="next-steps"></a><span data-ttu-id="10546-192">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="10546-192">Next steps</span></span>
* <span data-ttu-id="10546-193">Yapılandırma [günlük analizi veri kaynaklarında](log-analytics-data-sources.md) günlüklerini ve ölçümleri toplamak için belirtmek için.</span><span class="sxs-lookup"><span data-stu-id="10546-193">Configure [data sources in Log Analytics](log-analytics-data-sources.md) to specify the logs and metrics to collect.</span></span>
* <span data-ttu-id="10546-194">Sanal makinelerden veri toplamak üzere [Çözümleri Galerisi eklemek günlük analizi çözümleri](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="10546-194">To gather data from virtual machines [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>
* <span data-ttu-id="10546-195">[Azure Tanılama'yı kullanarak verileri toplamak](log-analytics-azure-storage.md) Azure'da çalışan diğer kaynaklar için.</span><span class="sxs-lookup"><span data-stu-id="10546-195">[Collect data by using Azure Diagnostics](log-analytics-azure-storage.md) for other resources that are running in Azure.</span></span>

<span data-ttu-id="10546-196">Azure'da olmayan bilgisayarlar için günlük analizi aracısı aşağıdaki makalelerde açıklanan yöntemlerle yükleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="10546-196">For computers that are not in Azure, you can install the Log Analytics agent by using the methods that are described in the following articles:</span></span>

* [<span data-ttu-id="10546-197">Windows bilgisayarları günlük Analizi'ne bağlayın</span><span class="sxs-lookup"><span data-stu-id="10546-197">Connect Windows computers to Log Analytics</span></span>](log-analytics-windows-agents.md)
* [<span data-ttu-id="10546-198">Linux bilgisayarları günlük Analizi'ne bağlayın</span><span class="sxs-lookup"><span data-stu-id="10546-198">Connect Linux computers to Log Analytics</span></span>](log-analytics-linux-agents.md)
