---
title: aaaConnect Azure sanal makineleri tooLog Analytics | Microsoft Docs
description: "Windows ve Linux için Azure'da çalışan sanal makineler hello toplanan günlüklerinin yolu önerilen ve ölçümleri hello günlük analizi Azure VM uzantısı yüklemektir. Hello Azure portal veya PowerShell tooinstall hello Azure VM üzerine günlük analizi sanal makine uzantısını kullanabilirsiniz."
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
ms.openlocfilehash: ac96c242d03ed3a22ca96368e5a8cc53f9a993db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-azure-virtual-machines-toolog-analytics-with-a-log-analytics-agent"></a><span data-ttu-id="de4bd-104">Günlük analizi aracı ile Azure sanal makineleri tooLog Analytics Bağlan</span><span class="sxs-lookup"><span data-stu-id="de4bd-104">Connect Azure virtual machines tooLog Analytics with a Log Analytics agent</span></span>

<span data-ttu-id="de4bd-105">Windows ve Linux bilgisayarlar için hello yöntemi günlüklerinin toplanması için önerilen ve ölçümleri hello günlük analizi aracı yüklemektir.</span><span class="sxs-lookup"><span data-stu-id="de4bd-105">For Windows and Linux computers, hello recommended method for collecting logs and metrics is by installing hello Log Analytics agent.</span></span>

<span data-ttu-id="de4bd-106">Hello kolay şekilde tooinstall hello günlük analizi Azure sanal makinelerde hello Log Analytics VM uzantısı aracısıdır.</span><span class="sxs-lookup"><span data-stu-id="de4bd-106">hello easiest way tooinstall hello Log Analytics agent on Azure virtual machines is through hello Log Analytics VM Extension.</span></span>  <span data-ttu-id="de4bd-107">Merhaba uzantısını kullanarak hello yükleme işlemini basitleştirir ve belirttiğiniz hello Aracısı toosend veri toohello günlük analizi çalışma alanı otomatik olarak yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="de4bd-107">Using hello extension simplifies hello installation process and automatically configures hello agent toosend data toohello Log Analytics workspace that you specify.</span></span> <span data-ttu-id="de4bd-108">Merhaba aracı ayrıca otomatik olarak hello en son özellikleri ve düzeltmeleri sahip olduktan yükseltilir.</span><span class="sxs-lookup"><span data-stu-id="de4bd-108">hello agent is also upgraded automatically, ensuring that you have hello latest features and fixes.</span></span>

<span data-ttu-id="de4bd-109">Windows sanal makineler için hello etkinleştirmek *Microsoft İzleme Aracısı* sanal makine uzantısı.</span><span class="sxs-lookup"><span data-stu-id="de4bd-109">For Windows virtual machines, you enable hello *Microsoft Monitoring Agent* virtual machine extension.</span></span>
<span data-ttu-id="de4bd-110">Linux sanal makineleri için hello etkinleştirmek *için OMS Aracısı Linux* sanal makine uzantısı.</span><span class="sxs-lookup"><span data-stu-id="de4bd-110">For Linux virtual machines, you enable hello *OMS Agent For Linux* virtual machine extension.</span></span>

<span data-ttu-id="de4bd-111">Daha fazla bilgi edinmek [Azure sanal makine uzantıları](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) ve hello [Linux Aracısı](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="de4bd-111">Learn more about [Azure virtual machine extensions](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and hello [Linux agent](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="de4bd-112">Aracı tabanlı koleksiyon için günlük verileri kullandığınızda, yapılandırmalısınız [günlük analizi veri kaynaklarında](log-analytics-data-sources.md) toospecify hello günlüklerini ve ölçümleri toocollect istiyor.</span><span class="sxs-lookup"><span data-stu-id="de4bd-112">When you use agent-based collection for log data, you must configure [data sources in Log Analytics](log-analytics-data-sources.md) toospecify hello logs and metrics that you want toocollect.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="de4bd-113">Günlük analizi tooindex günlük verilerini kullanarak yapılandırırsanız [Azure tanılama](log-analytics-azure-storage.md), ve hello günlükleri iki kez toplandıktan sonra aynı günlükleri, hello Aracısı toocollect hello yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="de4bd-113">If you configure Log Analytics tooindex log data by using [Azure diagnostics](log-analytics-azure-storage.md), and you configure hello agent toocollect hello same logs, then hello logs are collected twice.</span></span> <span data-ttu-id="de4bd-114">Her iki veri kaynakları için ücretlendirilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="de4bd-114">You are charged for both data sources.</span></span> <span data-ttu-id="de4bd-115">Merhaba aracısı yüklü varsa, yalnızca hello aracı kullanarak günlük verileri toplamak - Azure tanılama günlük analizi toocollect günlük verilerini yapılandırmayın.</span><span class="sxs-lookup"><span data-stu-id="de4bd-115">If you have hello agent installed, then collect log data by using only hello agent - don't configure Log Analytics toocollect log data from Azure diagnostics.</span></span>
>
>

<span data-ttu-id="de4bd-116">Tooenable hello günlük analizi sanal makine uzantısı kolay üç yolu vardır:</span><span class="sxs-lookup"><span data-stu-id="de4bd-116">There are three easy ways tooenable hello Log Analytics virtual machine extension:</span></span>

* <span data-ttu-id="de4bd-117">Hello Azure portal kullanarak</span><span class="sxs-lookup"><span data-stu-id="de4bd-117">By using hello Azure portal</span></span>
* <span data-ttu-id="de4bd-118">Azure PowerShell kullanarak</span><span class="sxs-lookup"><span data-stu-id="de4bd-118">By using Azure PowerShell</span></span>
* <span data-ttu-id="de4bd-119">Bir Azure Resource Manager şablonu kullanarak</span><span class="sxs-lookup"><span data-stu-id="de4bd-119">By using an Azure Resource Manager template</span></span>

## <a name="enable-hello-vm-extension-in-hello-azure-portal"></a><span data-ttu-id="de4bd-120">Hello Azure portal Hello VM uzantı etkinleştirilemedi</span><span class="sxs-lookup"><span data-stu-id="de4bd-120">Enable hello VM extension in hello Azure portal</span></span>
<span data-ttu-id="de4bd-121">Günlük analizi için hello aracısı yükleyin ve hello üzerinde çalıştığı hello kullanarak Azure sanal makinesi bağlanın [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="de4bd-121">You can install hello agent for Log Analytics and connect hello Azure virtual machine that it runs on by using hello [Azure portal](https://portal.azure.com).</span></span>

### <a name="tooinstall-hello-log-analytics-agent-and-connect-hello-virtual-machine-tooa-log-analytics-workspace"></a><span data-ttu-id="de4bd-122">tooinstall günlük analizi aracı hello ve hello sanal makine tooa günlük analizi çalışma bağlayın</span><span class="sxs-lookup"><span data-stu-id="de4bd-122">tooinstall hello Log Analytics agent and connect hello virtual machine tooa Log Analytics workspace</span></span>
1. <span data-ttu-id="de4bd-123">Merhaba içine oturum [Azure portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="de4bd-123">Sign into hello [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="de4bd-124">Seçin **Gözat** üzerinde hello hello portal ve ardından çok sol tarafı**günlük analizi (OMS)** ve seçin.</span><span class="sxs-lookup"><span data-stu-id="de4bd-124">Select **Browse** on hello left side of hello portal, and then go too**Log Analytics (OMS)** and select it.</span></span>
3. <span data-ttu-id="de4bd-125">Günlük analizi çalışma alanları, listeden toouse hello Azure VM ile istediğiniz hello birini seçin.</span><span class="sxs-lookup"><span data-stu-id="de4bd-125">In your list of Log Analytics workspaces, select hello one that you want toouse with hello Azure VM.</span></span>  
   ![OMS çalışma alanları](./media/log-analytics-azure-vm-extension/oms-connect-azure-01.png)
4. <span data-ttu-id="de4bd-127">Altında **oturum analytics Yönetimi**seçin **sanal makineleri**.</span><span class="sxs-lookup"><span data-stu-id="de4bd-127">Under **Log analytics management**, select **Virtual machines**.</span></span>  
   <span data-ttu-id="de4bd-128">![Sanal makineler](./media/log-analytics-azure-vm-extension/oms-connect-azure-02.png)</span><span class="sxs-lookup"><span data-stu-id="de4bd-128">![Virtual machines](./media/log-analytics-azure-vm-extension/oms-connect-azure-02.png)</span></span>
5. <span data-ttu-id="de4bd-129">Merhaba listesinde **sanal makineleri**, hello tooinstall hello Aracısı istediğiniz sanal makinenin seçin.</span><span class="sxs-lookup"><span data-stu-id="de4bd-129">In hello list of **Virtual machines**, select hello virtual machine on which you want tooinstall hello agent.</span></span> <span data-ttu-id="de4bd-130">Merhaba **OMS bağlantı durumu** şekilde hello VM gösterir için **bağlı**.</span><span class="sxs-lookup"><span data-stu-id="de4bd-130">hello **OMS connection status** for hello VM indicates that it is **Not connected**.</span></span>  
   <span data-ttu-id="de4bd-131">![VM bağlı değil](./media/log-analytics-azure-vm-extension/oms-connect-azure-03.png)</span><span class="sxs-lookup"><span data-stu-id="de4bd-131">![VM not connected](./media/log-analytics-azure-vm-extension/oms-connect-azure-03.png)</span></span>
6. <span data-ttu-id="de4bd-132">Sanal makineniz için Hello ayrıntılarında seçin **Bağlan**.</span><span class="sxs-lookup"><span data-stu-id="de4bd-132">In hello details for your virtual machine, select **Connect**.</span></span> <span data-ttu-id="de4bd-133">Merhaba Aracısı otomatik olarak yüklenir ve günlük analizi çalışma alanınız için yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="de4bd-133">hello agent is automatically installed and configured for your Log Analytics workspace.</span></span> <span data-ttu-id="de4bd-134">Bu işlem hello OMS bağlantı durumu hangi sırada olan birkaç dakika sürer *bağlanıyor...*</span><span class="sxs-lookup"><span data-stu-id="de4bd-134">This process takes a few minutes, during which time hello OMS Connection status is *Connecting...*</span></span>  
   <span data-ttu-id="de4bd-135">![VM Bağlan](./media/log-analytics-azure-vm-extension/oms-connect-azure-04.png)</span><span class="sxs-lookup"><span data-stu-id="de4bd-135">![Connect VM](./media/log-analytics-azure-vm-extension/oms-connect-azure-04.png)</span></span>
7. <span data-ttu-id="de4bd-136">Yükleyip hello aracısına bağlanmak sonra hello **OMS bağlantısı** durum güncelleştirilmiş tooshow olacaktır **bu çalışma**.</span><span class="sxs-lookup"><span data-stu-id="de4bd-136">After you install and connect hello agent, hello **OMS connection** status will be updated tooshow **This workspace**.</span></span>  
   <span data-ttu-id="de4bd-137">![Bağlı](./media/log-analytics-azure-vm-extension/oms-connect-azure-05.png)</span><span class="sxs-lookup"><span data-stu-id="de4bd-137">![Connected](./media/log-analytics-azure-vm-extension/oms-connect-azure-05.png)</span></span>

## <a name="enable-hello-vm-extension-using-powershell"></a><span data-ttu-id="de4bd-138">PowerShell kullanarak hello VM uzantısı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="de4bd-138">Enable hello VM extension using PowerShell</span></span>
<span data-ttu-id="de4bd-139">PowerShell kullanarak sanal makineniz yapılandırırken tooprovide hello gerekir **Workspaceıd** ve **workspaceKey**.</span><span class="sxs-lookup"><span data-stu-id="de4bd-139">When you configure your virtual machine by using PowerShell, you need tooprovide hello **workspaceId** and **workspaceKey**.</span></span> <span data-ttu-id="de4bd-140">json yapılandırmanızda Hello özellik adları **büyük küçük harfe duyarlı**.</span><span class="sxs-lookup"><span data-stu-id="de4bd-140">hello property names in your json configuration are **case-sensitive**.</span></span>

<span data-ttu-id="de4bd-141">Merhaba kimliği ve anahtarı üzerinde hello bulabilir **ayarları** sayfasında hello OMS portalı veya hello önceki örnekte gösterildiği gibi PowerShell kullanarak.</span><span class="sxs-lookup"><span data-stu-id="de4bd-141">You can find hello Id and key on hello **Settings** page of hello OMS portal, or by using PowerShell as shown in hello preceding example.</span></span>

![Çalışma alanı kimliği ve birincil anahtar](./media/log-analytics-azure-vm-extension/oms-analyze-azure-sources.png)

<span data-ttu-id="de4bd-143">Azure Klasik sanal makineleri ve Resource Manager sanal makineleri için farklı komutlar vardır.</span><span class="sxs-lookup"><span data-stu-id="de4bd-143">There are different commands for Azure classic virtual machines and Resource Manager virtual machines.</span></span> <span data-ttu-id="de4bd-144">Aşağıda, Klasik ve Resource Manager sanal makineleri için örnekler verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="de4bd-144">Following are examples for both classic and Resource Manager virtual machines.</span></span>

<span data-ttu-id="de4bd-145">Klasik sanal makineler için aşağıdaki PowerShell örneğine hello kullan:</span><span class="sxs-lookup"><span data-stu-id="de4bd-145">For classic virtual machines, use hello following PowerShell example:</span></span>

```PowerShell
Add-AzureAccount

$workspaceId = "enter workspace ID here"
$workspaceKey = "enter workspace key here"
$hostedService = "enter hosted service here"

$vm = Get-AzureVM –ServiceName $hostedService

# For Windows VM uncomment hello following line
# Set-AzureVMExtension -VM $vm -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionName 'MicrosoftMonitoringAgent' -Version '1.*' -PublicConfiguration "{'workspaceId': '$workspaceId'}" -PrivateConfiguration "{'workspaceKey': '$workspaceKey' }" | Update-AzureVM -Verbose

# For Linux VM uncomment hello following line
# Set-AzureVMExtension -VM $vm -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionName 'OmsAgentForLinux' -Version '1.*' -PublicConfiguration "{'workspaceId': '$workspaceId'}" -PrivateConfiguration "{'workspaceKey': '$workspaceKey' }" | Update-AzureVM -Verbose
```

<span data-ttu-id="de4bd-146">CLI aşağıdaki hello kullanarak Resource Manager Linux VM'ler için</span><span class="sxs-lookup"><span data-stu-id="de4bd-146">For Resource Manager Linux VMs using hello following CLI</span></span>
```azurecli
az vm extension set --resource-group myRGMonitor --vm-name myMonitorVM --name OmsAgentForLinux --publisher Microsoft.EnterpriseCloud.Monitoring --version 1.3 --protected-settings ‘{"workspaceKey": "<workspace-key>"}’ --settings ‘{"workspaceId": "<workspace-id>"}’ 
```

<span data-ttu-id="de4bd-147">Resource Manager sanal makineler için aşağıdaki PowerShell örneğine hello kullan:</span><span class="sxs-lookup"><span data-stu-id="de4bd-147">For Resource Manager virtual machines, use hello following PowerShell example:</span></span>

```PowerShell
Login-AzureRMAccount
Select-AzureRMSubscription -SubscriptionId "**"

$workspaceName = "your workspace name"
$VMresourcegroup = "**"
$VMresourcename = "**"

$workspace = (Get-AzureRmOperationalInsightsWorkspace).Where({$_.Name -eq $workspaceName})

if ($workspace.Name -ne $workspaceName)
{
    Write-Error "Unable toofind OMS Workspace $workspaceName. Do you need toorun Select-AzureRMSubscription?"
}

$workspaceId = $workspace.CustomerId
$workspaceKey = (Get-AzureRmOperationalInsightsWorkspaceSharedKeys -ResourceGroupName $workspace.ResourceGroupName -Name $workspace.Name).PrimarySharedKey

$vm = Get-AzureRmVM -ResourceGroupName $VMresourcegroup -Name $VMresourcename
$location = $vm.Location

# For Windows VM uncomment hello following line
# Set-AzureRmVMExtension -ResourceGroupName $VMresourcegroup -VMName $VMresourcename -Name 'MicrosoftMonitoringAgent' -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionType 'MicrosoftMonitoringAgent' -TypeHandlerVersion '1.0' -Location $location -SettingString "{'workspaceId': '$workspaceId'}" -ProtectedSettingString "{'workspaceKey': '$workspaceKey'}"

# For Linux VM uncomment hello following line
# Set-AzureRmVMExtension -ResourceGroupName $VMresourcegroup -VMName $VMresourcename -Name 'OmsAgentForLinux' -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionType 'OmsAgentForLinux' -TypeHandlerVersion '1.0' -Location $location -SettingString "{'workspaceId': '$workspaceId'}" -ProtectedSettingString "{'workspaceKey': '$workspaceKey'}"


```


## <a name="deploy-hello-vm-extension-using-a-template"></a><span data-ttu-id="de4bd-148">Bir şablon kullanarak hello VM uzantısı dağıtma</span><span class="sxs-lookup"><span data-stu-id="de4bd-148">Deploy hello VM extension using a template</span></span>
<span data-ttu-id="de4bd-149">Azure Kaynak Yöneticisi'ni kullanarak hello dağıtım ve uygulamanızın yapılandırmasını tanımlayan bir şablon (JSON biçiminde) oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="de4bd-149">By using Azure Resource Manager, you can create a template (in JSON format) that defines hello deployment and configuration of your application.</span></span> <span data-ttu-id="de4bd-150">Bu şablon Resource Manager şablonu olarak bilinir ve bildirim temelli yolu toodefine dağıtılmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="de4bd-150">This template is known as a Resource Manager template and provides a declarative way toodefine deployment.</span></span> <span data-ttu-id="de4bd-151">Bir şablon kullanarak, sürekli olarak hello uygulama yaşam döngüsü boyunca uygulamanızı dağıtmak ve kaynaklarınızın tutarlı bir durumda dağıtılması emin olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="de4bd-151">By using a template, you can repeatedly deploy your application throughout hello app lifecycle and have confidence that your resources are being deployed in a consistent state.</span></span>

<span data-ttu-id="de4bd-152">Merhaba günlük analizi aracı, Resource Manager şablonu bir parçası olarak dahil ederek, her bir sanal makine önceden yapılandırılmış tooreport tooyour günlük analizi çalışma alanı olduğundan emin olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="de4bd-152">By including hello Log Analytics agent as part of your Resource Manager template, you can ensure that each virtual machine is pre-configured tooreport tooyour Log Analytics workspace.</span></span>

<span data-ttu-id="de4bd-153">Resource Manager şablonları hakkında daha fazla bilgi için bkz: [Azure Resource Manager şablonları yazma](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="de4bd-153">For more information about Resource Manager templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="de4bd-154">Windows hello yüklü Microsoft İzleme Aracısı uzantısı ile çalışan bir sanal makine dağıtmak için kullanılan bir Resource Manager şablonu örneği verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="de4bd-154">Following is an example of a Resource Manager template that's used for deploying a virtual machine that's running Windows with hello Microsoft Monitoring Agent extension installed.</span></span> <span data-ttu-id="de4bd-155">Bu şablon bir tipik sanal makine şablonuyla eklemeleri aşağıdaki hello şöyledir:</span><span class="sxs-lookup"><span data-stu-id="de4bd-155">This template is a typical virtual machine template, with hello following additions:</span></span>

* <span data-ttu-id="de4bd-156">Workspaceıd ve workspaceName parametreleri</span><span class="sxs-lookup"><span data-stu-id="de4bd-156">workspaceId and workspaceName parameters</span></span>
* <span data-ttu-id="de4bd-157">Microsoft.EnterpriseCloud.Monitoring kaynak uzantısı bölümü</span><span class="sxs-lookup"><span data-stu-id="de4bd-157">Microsoft.EnterpriseCloud.Monitoring resource extension section</span></span>
* <span data-ttu-id="de4bd-158">Merhaba Workspaceıd ve workspaceSharedKey çıkışları toolook</span><span class="sxs-lookup"><span data-stu-id="de4bd-158">Outputs toolook up hello workspaceId and workspaceSharedKey</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "adminUsername": {
      "type": "string",
      "metadata": {
        "description": "Username for hello Virtual Machine."
      }
    },
    "adminPassword": {
      "type": "securestring",
      "metadata": {
        "description": "Password for hello Virtual Machine."
      }
    },
    "dnsLabelPrefix": {
       "type": "string",
       "metadata": {
          "description": "DNS Label for hello Public IP. Must be lowercase. It should match with hello following regular expression: ^[a-z][a-z0-9-]{1,61}[a-z0-9]$ or it will raise an error."
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
        "description": "hello Windows version for hello VM. This will pick a fully patched image of this given Windows version. Allowed values: 2008-R2-SP1, 2012-Datacenter, 2012-R2-Datacenter, Windows-Server-Technical-Preview."
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

<span data-ttu-id="de4bd-159">Bir şablonu PowerShell komutunu aşağıdaki hello kullanarak dağıtabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="de4bd-159">You can deploy a template by using hello following PowerShell command:</span></span>

```PowerShell
New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateFile $templateFilePath
```

## <a name="troubleshooting-hello-log-analytics-vm-extension"></a><span data-ttu-id="de4bd-160">Merhaba günlük analizi VM uzantısı sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="de4bd-160">Troubleshooting hello Log Analytics VM extension</span></span>
<span data-ttu-id="de4bd-161">Genellikle Azure portalında veya Azure powershell şeyler çalışmıyor zaman bir ileti alırsınız.</span><span class="sxs-lookup"><span data-stu-id="de4bd-161">Usually you receive a message when things don't work, from either Azure portal or Azure powershell.</span></span>

1. <span data-ttu-id="de4bd-162">Merhaba içine oturum [Azure portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="de4bd-162">Sign into hello [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="de4bd-163">Merhaba VM bulun ve VM Ayrıntıları'nı açın.</span><span class="sxs-lookup"><span data-stu-id="de4bd-163">Find hello VM and open VM details.</span></span>
3. <span data-ttu-id="de4bd-164">Tıklatın **uzantıları** OMS uzantısı veya etkinleştirilirse toocheck.</span><span class="sxs-lookup"><span data-stu-id="de4bd-164">Click **Extensions** toocheck if OMS extension is enabled or not.</span></span>

   ![VM uzantısı görünümü](./media/log-analytics-azure-vm-extension/oms-vmview-extensions.png)

4. <span data-ttu-id="de4bd-166">Merhaba tıklatın *MicrosoftMonitoringAgent*(Windows) veya *OmsAgentForLinux*(Linux) uzantısı ve görünüm ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="de4bd-166">Click hello *MicrosoftMonitoringAgent*(Windows) or *OmsAgentForLinux*(Linux) extension and view details.</span></span> 

   ![VM uzantısı ayrıntıları](./media/log-analytics-azure-vm-extension/oms-vmview-extensiondetails.png)

### <a name="troubleshooting-windows-virtual-machines"></a><span data-ttu-id="de4bd-168">Sorun giderme Windows sanal makineler</span><span class="sxs-lookup"><span data-stu-id="de4bd-168">Troubleshooting Windows Virtual Machines</span></span>
<span data-ttu-id="de4bd-169">Merhaba, *Microsoft İzleme Aracısı* VM Aracısı uzantısı yükleme değil veya raporlama, aşağıdaki adımları tootroubleshoot hello sorunu hello gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="de4bd-169">If hello *Microsoft Monitoring Agent* VM agent extension is not installing or reporting, you can perform hello following steps tootroubleshoot hello issue.</span></span>

1. <span data-ttu-id="de4bd-170">Hello Azure VM aracısının yüklü olduğundan ve doğru şekilde de hello kullanarak çalışma adımları denetleyin [KB 2965986](https://support.microsoft.com/kb/2965986#mt1).</span><span class="sxs-lookup"><span data-stu-id="de4bd-170">Check if hello Azure VM agent is installed and working correctly by using hello steps in [KB 2965986](https://support.microsoft.com/kb/2965986#mt1).</span></span>
   * <span data-ttu-id="de4bd-171">Merhaba VM aracı günlük dosyasını gözden geçirebilirsiniz`C:\WindowsAzure\logs\WaAppAgent.log`</span><span class="sxs-lookup"><span data-stu-id="de4bd-171">You can also review hello VM agent log file `C:\WindowsAzure\logs\WaAppAgent.log`</span></span>
   * <span data-ttu-id="de4bd-172">Merhaba günlük yoksa hello VM aracısı yüklü değil.</span><span class="sxs-lookup"><span data-stu-id="de4bd-172">If hello log does not exist, hello VM agent is not installed.</span></span>
     * [<span data-ttu-id="de4bd-173">Klasik sanal makinelerin Hello Azure VM Aracısı yükleme</span><span class="sxs-lookup"><span data-stu-id="de4bd-173">Install hello Azure VM Agent on classic VMs</span></span>](../virtual-machines/windows/classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
2. <span data-ttu-id="de4bd-174">Merhaba uzantısı sinyal görev hello aşağıdaki adımları kullanarak çalışan Microsoft Monitoring Agent onaylayın:</span><span class="sxs-lookup"><span data-stu-id="de4bd-174">Confirm hello Microsoft Monitoring Agent extension heartbeat task is running using hello following steps:</span></span>
   * <span data-ttu-id="de4bd-175">Toohello sanal makinede oturum açın</span><span class="sxs-lookup"><span data-stu-id="de4bd-175">Log in toohello virtual machine</span></span>
   * <span data-ttu-id="de4bd-176">Görev Zamanlayıcısı'nı açın ve hello bulur `update_azureoperationalinsight_agent_heartbeat` görevi</span><span class="sxs-lookup"><span data-stu-id="de4bd-176">Open task scheduler and find hello `update_azureoperationalinsight_agent_heartbeat` task</span></span>
   * <span data-ttu-id="de4bd-177">Hello görev etkinleştirilir ve bir dakikada çalıştığını onaylayın</span><span class="sxs-lookup"><span data-stu-id="de4bd-177">Confirm hello task is enabled and is running every one minute</span></span>
   * <span data-ttu-id="de4bd-178">Merhaba sinyal günlük dosyası iade etme`C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\heartbeat.log`</span><span class="sxs-lookup"><span data-stu-id="de4bd-178">Check hello heartbeat logfile in `C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\heartbeat.log`</span></span>
3. <span data-ttu-id="de4bd-179">Merhaba Microsoft İzleme Aracısı VM uzantısı günlük dosyalarını inceleyin`C:\Packages\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent`</span><span class="sxs-lookup"><span data-stu-id="de4bd-179">Review hello Microsoft Monitoring Agent VM extension log files in `C:\Packages\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent`</span></span>
4. <span data-ttu-id="de4bd-180">Merhaba sanal makine PowerShell betikleri çalıştırabilirsiniz emin olun</span><span class="sxs-lookup"><span data-stu-id="de4bd-180">Ensure hello virtual machine can run PowerShell scripts</span></span>
5. <span data-ttu-id="de4bd-181">C:\Windows\temp izinlerini değiştirmezsiniz emin olun</span><span class="sxs-lookup"><span data-stu-id="de4bd-181">Ensure permissions on C:\Windows\temp haven’t been changed</span></span>
6. <span data-ttu-id="de4bd-182">Komutu yükseltilmiş bir PowerShell penceresinde hello sanal makinede aşağıdaki hello yazarak Microsoft İzleme Aracısı hello hello durumunu görüntüleme`  (New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg').GetCloudWorkspaces() | Format-List`</span><span class="sxs-lookup"><span data-stu-id="de4bd-182">View hello status of hello Microsoft Monitoring Agent by typing hello following command in an elevated PowerShell window on hello virtual machine `  (New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg').GetCloudWorkspaces() | Format-List`</span></span>
7. <span data-ttu-id="de4bd-183">Merhaba Microsoft Monitoring Agent Kurulum günlük dosyalarını inceleyin`C:\Windows\System32\config\systemprofile\AppData\Local\SCOM\Logs`</span><span class="sxs-lookup"><span data-stu-id="de4bd-183">Review hello Microsoft Monitoring Agent setup log files in `C:\Windows\System32\config\systemprofile\AppData\Local\SCOM\Logs`</span></span>

<span data-ttu-id="de4bd-184">Daha fazla bilgi için bkz: [Windows uzantıları sorun giderme](../virtual-machines/windows/extensions-troubleshoot.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="de4bd-184">For more information, see [troubleshooting Windows extensions](../virtual-machines/windows/extensions-troubleshoot.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

### <a name="troubleshooting-linux-virtual-machines"></a><span data-ttu-id="de4bd-185">Linux sanal makineleri sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="de4bd-185">Troubleshooting Linux Virtual Machines</span></span>
<span data-ttu-id="de4bd-186">Merhaba, *Linux için OMS aracısının* VM Aracısı uzantısı yükleme değil veya raporlama, aşağıdaki adımları tootroubleshoot hello sorunu hello gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="de4bd-186">If hello *OMS Agent for Linux* VM agent extension is not installing or reporting, you can perform hello following steps tootroubleshoot hello issue.</span></span>

1. <span data-ttu-id="de4bd-187">Merhaba uzantı durumu ise *bilinmeyen* hello Azure VM aracısı yüklü olup olmadığını denetleyin ve doğru şekilde hello VM aracı günlük dosyasını gözden geçirerek çalışma`/var/log/waagent.log`</span><span class="sxs-lookup"><span data-stu-id="de4bd-187">If hello extension status is *Unknown* check if hello Azure VM agent is installed and working correctly by reviewing hello VM agent log file `/var/log/waagent.log`</span></span>
   * <span data-ttu-id="de4bd-188">Merhaba günlük yoksa hello VM aracısı yüklü değil.</span><span class="sxs-lookup"><span data-stu-id="de4bd-188">If hello log does not exist, hello VM agent is not installed.</span></span>
   * [<span data-ttu-id="de4bd-189">Linux VM'ler Hello Azure VM Aracısı yükleme</span><span class="sxs-lookup"><span data-stu-id="de4bd-189">Install hello Azure VM Agent on Linux VMs</span></span>](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
2. <span data-ttu-id="de4bd-190">Sağlıksız diğer durumlar için Linux VM uzantısı için gözden geçirme hello OMS aracısının günlük dosyaları `/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/extension.log` ve`/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/CommandExecution.log`</span><span class="sxs-lookup"><span data-stu-id="de4bd-190">For other unhealthy statuses, review hello OMS Agent for Linux VM extension logs files in `/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/extension.log` and `/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/CommandExecution.log`</span></span>
3. <span data-ttu-id="de4bd-191">Merhaba uzantı durumu sağlam ancak veri karşıya Linux oturum açmak için dosyaları hello OMS Aracısı gözden geçirin`/var/opt/microsoft/omsagent/log/omsagent.log`</span><span class="sxs-lookup"><span data-stu-id="de4bd-191">If hello extension status is healthy, but data is not being uploaded review hello OMS Agent for Linux log files in `/var/opt/microsoft/omsagent/log/omsagent.log`</span></span>

## <a name="next-steps"></a><span data-ttu-id="de4bd-192">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="de4bd-192">Next steps</span></span>
* <span data-ttu-id="de4bd-193">Yapılandırma [günlük analizi veri kaynaklarında](log-analytics-data-sources.md) toospecify hello günlüklerini ve ölçümleri toocollect.</span><span class="sxs-lookup"><span data-stu-id="de4bd-193">Configure [data sources in Log Analytics](log-analytics-data-sources.md) toospecify hello logs and metrics toocollect.</span></span>
* <span data-ttu-id="de4bd-194">sanal makineler toogather verileri [hello Çözümleri Galerisi eklemek günlük analizi çözümleri](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="de4bd-194">toogather data from virtual machines [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>
* <span data-ttu-id="de4bd-195">[Azure Tanılama'yı kullanarak verileri toplamak](log-analytics-azure-storage.md) Azure'da çalışan diğer kaynaklar için.</span><span class="sxs-lookup"><span data-stu-id="de4bd-195">[Collect data by using Azure Diagnostics](log-analytics-azure-storage.md) for other resources that are running in Azure.</span></span>

<span data-ttu-id="de4bd-196">Azure'da olmayan bilgisayarlar için hello günlük analizi aracı makaleler hello açıklanan hello yöntemleri kullanarak yükleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="de4bd-196">For computers that are not in Azure, you can install hello Log Analytics agent by using hello methods that are described in hello following articles:</span></span>

* [<span data-ttu-id="de4bd-197">Windows bilgisayarları tooLog Analytics Bağlan</span><span class="sxs-lookup"><span data-stu-id="de4bd-197">Connect Windows computers tooLog Analytics</span></span>](log-analytics-windows-agents.md)
* [<span data-ttu-id="de4bd-198">Linux bilgisayarları tooLog Analytics Bağlan</span><span class="sxs-lookup"><span data-stu-id="de4bd-198">Connect Linux computers tooLog Analytics</span></span>](log-analytics-linux-agents.md)
