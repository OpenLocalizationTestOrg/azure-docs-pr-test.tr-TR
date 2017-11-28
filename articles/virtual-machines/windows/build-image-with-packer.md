---
title: "Windows Azure VM görüntülerini Packer ile aaaHow toocreate | Microsoft Docs"
description: "Bilgi nasıl toouse Packer toocreate görüntülerini azure'da Windows sanal makineler"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 08/18/2017
ms.author: iainfou
ms.openlocfilehash: d310fae3becb453b52d21281cb8ac53fa14a3fc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-packer-toocreate-windows-virtual-machine-images-in-azure"></a><span data-ttu-id="8d4ba-103">Azure'da nasıl toouse Packer toocreate Windows sanal makine görüntüleri</span><span class="sxs-lookup"><span data-stu-id="8d4ba-103">How toouse Packer toocreate Windows virtual machine images in Azure</span></span>
<span data-ttu-id="8d4ba-104">Her sanal makine (VM) azure'da hello Windows Dağıtım ve işletim sistemi sürümü tanımlayan bir görüntüden oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="8d4ba-104">Each virtual machine (VM) in Azure is created from an image that defines hello Windows distribution and OS version.</span></span> <span data-ttu-id="8d4ba-105">Görüntüleri, önceden yüklenmiş uygulamalar ve yapılandırmalar içerebilir.</span><span class="sxs-lookup"><span data-stu-id="8d4ba-105">Images can include pre-installed applications and configurations.</span></span> <span data-ttu-id="8d4ba-106">Hello Azure Marketi birçok ilk ve üçüncü taraf en yaygın işletim sistemi için sağlar ve uygulama ortamları veya kendi özel görüntülerinizi uyarlanmış tooyour gereksinimlerini oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8d4ba-106">hello Azure Marketplace provides many first and third-party images for most common OS' and application environments, or you can create your own custom images tailored tooyour needs.</span></span> <span data-ttu-id="8d4ba-107">Bu makalede nasıl toouse hello açık kaynak aracı ayrıntıları [Packer](https://www.packer.io/) azure'da toodefine ve yapı özel görüntüler.</span><span class="sxs-lookup"><span data-stu-id="8d4ba-107">This article details how toouse hello open source tool [Packer](https://www.packer.io/) toodefine and build custom images in Azure.</span></span>


## <a name="create-azure-resource-group"></a><span data-ttu-id="8d4ba-108">Azure kaynak grubu oluşturun</span><span class="sxs-lookup"><span data-stu-id="8d4ba-108">Create Azure resource group</span></span>
<span data-ttu-id="8d4ba-109">Merhaba kaynak VM derlemeler gibi hello oluşturma işlemi sırasında geçici Azure kaynaklarını Packer oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8d4ba-109">During hello build process, Packer creates temporary Azure resources as it builds hello source VM.</span></span> <span data-ttu-id="8d4ba-110">bir görüntü olarak kullanmak üzere VM kaynak toocapture, bir kaynak grubu tanımlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8d4ba-110">toocapture that source VM for use as an image, you must define a resource group.</span></span> <span data-ttu-id="8d4ba-111">Merhaba hello Packer oluşturma işleminin çıktısı bu kaynak grubunda depolanır.</span><span class="sxs-lookup"><span data-stu-id="8d4ba-111">hello output from hello Packer build process is stored in this resource group.</span></span>

<span data-ttu-id="8d4ba-112">Bir kaynak grubu ile oluşturmak [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="8d4ba-112">Create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="8d4ba-113">Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroup* hello içinde *eastus* konumu:</span><span class="sxs-lookup"><span data-stu-id="8d4ba-113">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```powershell
$rgName = "myResourceGroup"
$location = "East US"
New-AzureRmResourceGroup -Name $rgName -Location $location
```

## <a name="create-azure-credentials"></a><span data-ttu-id="8d4ba-114">Azure kimlik bilgileri oluşturun</span><span class="sxs-lookup"><span data-stu-id="8d4ba-114">Create Azure credentials</span></span>
<span data-ttu-id="8d4ba-115">Packer bir hizmet sorumlusu kullanarak Azure ile kimliğini doğrular.</span><span class="sxs-lookup"><span data-stu-id="8d4ba-115">Packer authenticates with Azure using a service principal.</span></span> <span data-ttu-id="8d4ba-116">Bir Azure hizmet sorumlusu uygulamaları, hizmetleri ve Packer gibi Otomasyon araçları ile birlikte kullanabileceğiniz bir güvenlik kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="8d4ba-116">An Azure service principal is a security identity that you can use with apps, services, and automation tools like Packer.</span></span> <span data-ttu-id="8d4ba-117">Denetim ve toowhat işlemleri hello hizmet sorumlusu Azure'da gerçekleştirebilirsiniz gibi hello izinleri tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="8d4ba-117">You control and define hello permissions as toowhat operations hello service principal can perform in Azure.</span></span>

<span data-ttu-id="8d4ba-118">Bir hizmet sorumlusu ile oluşturma [yeni AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) hello hizmet asıl toocreate izinlerini atamak ve kaynaklarını yönetecek [New-AzureRmRoleAssignment](/powershell/module/azurerm.resources/new-azurermroleassignment):</span><span class="sxs-lookup"><span data-stu-id="8d4ba-118">Create a service principal with [New-AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) and assign permissions for hello service principal toocreate and manage resources with [New-AzureRmRoleAssignment](/powershell/module/azurerm.resources/new-azurermroleassignment):</span></span>

```powershell
$sp = New-AzureRmADServicePrincipal -DisplayName "Azure Packer IKF" -Password "P@ssw0rd!"
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

<span data-ttu-id="8d4ba-119">tooauthenticate tooAzure etmeniz tooobtain Azure Kiracı ve abonelik kimlikleri ile [Get-AzureRmSubscription](/powershell/module/azurerm.profile/get-azurermsubscription):</span><span class="sxs-lookup"><span data-stu-id="8d4ba-119">tooauthenticate tooAzure, you also need tooobtain your Azure tenant and subscription IDs with [Get-AzureRmSubscription](/powershell/module/azurerm.profile/get-azurermsubscription):</span></span>

```powershell
$sub = Get-AzureRmSubscription
$sub.TenantId
$sub.SubscriptionId
```

<span data-ttu-id="8d4ba-120">Bu iki kimlikleri hello sonraki adımda kullanın.</span><span class="sxs-lookup"><span data-stu-id="8d4ba-120">You use these two IDs in hello next step.</span></span>


## <a name="define-packer-template"></a><span data-ttu-id="8d4ba-121">Packer şablon oluştur</span><span class="sxs-lookup"><span data-stu-id="8d4ba-121">Define Packer template</span></span>
<span data-ttu-id="8d4ba-122">toobuild görüntüleri bir JSON dosyası olarak bir şablon oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8d4ba-122">toobuild images, you create a template as a JSON file.</span></span> <span data-ttu-id="8d4ba-123">Merhaba şablonunda hello gerçek taşımak provisioners derleme işlemi ve oluşturucular tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="8d4ba-123">In hello template, you define builders and provisioners that carry out hello actual build process.</span></span> <span data-ttu-id="8d4ba-124">Packer sahip bir [Azure sağlayıcısı](https://www.packer.io/docs/builders/azure.html) toodefine Azure sağlayan adım önceki hello oluşturulan hello hizmet asıl kimlik bilgileri gibi kaynaklar.</span><span class="sxs-lookup"><span data-stu-id="8d4ba-124">Packer has a [provisioner for Azure](https://www.packer.io/docs/builders/azure.html) that allows you toodefine Azure resources, such as hello service principal credentials created in hello preceding step.</span></span>

<span data-ttu-id="8d4ba-125">Adlı bir dosya oluşturun *windows.json* ve Yapıştır hello aşağıdaki içeriği.</span><span class="sxs-lookup"><span data-stu-id="8d4ba-125">Create a file named *windows.json* and paste hello following content.</span></span> <span data-ttu-id="8d4ba-126">Kendi değerlerinizi için hello aşağıdakileri girin:</span><span class="sxs-lookup"><span data-stu-id="8d4ba-126">Enter your own values for hello following:</span></span>

| <span data-ttu-id="8d4ba-127">Parametre</span><span class="sxs-lookup"><span data-stu-id="8d4ba-127">Parameter</span></span>                           | <span data-ttu-id="8d4ba-128">Burada tooobtain</span><span class="sxs-lookup"><span data-stu-id="8d4ba-128">Where tooobtain</span></span> |
|-------------------------------------|----------------------------------------------------|
| <span data-ttu-id="8d4ba-129">*client_id*</span><span class="sxs-lookup"><span data-stu-id="8d4ba-129">*client_id*</span></span>                         | <span data-ttu-id="8d4ba-130">Görünüm hizmet asıl kimliği ile`$sp.applicationId`</span><span class="sxs-lookup"><span data-stu-id="8d4ba-130">View service principal ID with `$sp.applicationId`</span></span> |
| <span data-ttu-id="8d4ba-131">*client_secret*</span><span class="sxs-lookup"><span data-stu-id="8d4ba-131">*client_secret*</span></span>                     | <span data-ttu-id="8d4ba-132">Belirttiğiniz parola`$securePassword`</span><span class="sxs-lookup"><span data-stu-id="8d4ba-132">Password you specified in `$securePassword`</span></span> |
| <span data-ttu-id="8d4ba-133">*tenant_id*</span><span class="sxs-lookup"><span data-stu-id="8d4ba-133">*tenant_id*</span></span>                         | <span data-ttu-id="8d4ba-134">Çıktı `$sub.TenantId` komutu</span><span class="sxs-lookup"><span data-stu-id="8d4ba-134">Output from `$sub.TenantId` command</span></span> |
| <span data-ttu-id="8d4ba-135">*ABONELİK_KİMLİĞİ*</span><span class="sxs-lookup"><span data-stu-id="8d4ba-135">*subscription_id*</span></span>                   | <span data-ttu-id="8d4ba-136">Çıktı `$sub.SubscriptionId` komutu</span><span class="sxs-lookup"><span data-stu-id="8d4ba-136">Output from `$sub.SubscriptionId` command</span></span> |
| <span data-ttu-id="8d4ba-137">*object_id*</span><span class="sxs-lookup"><span data-stu-id="8d4ba-137">*object_id*</span></span>                         | <span data-ttu-id="8d4ba-138">Görünüm hizmet asıl nesne kimliği ile`$sp.Id`</span><span class="sxs-lookup"><span data-stu-id="8d4ba-138">View service principal object ID with `$sp.Id`</span></span> |
| <span data-ttu-id="8d4ba-139">*managed_image_resource_group_name*</span><span class="sxs-lookup"><span data-stu-id="8d4ba-139">*managed_image_resource_group_name*</span></span> | <span data-ttu-id="8d4ba-140">Merhaba ilk adımda oluşturduğunuz kaynak grubunun adı</span><span class="sxs-lookup"><span data-stu-id="8d4ba-140">Name of resource group you created in hello first step</span></span> |
| <span data-ttu-id="8d4ba-141">*managed_image_name*</span><span class="sxs-lookup"><span data-stu-id="8d4ba-141">*managed_image_name*</span></span>                | <span data-ttu-id="8d4ba-142">Oluşturulan hello yönetilen disk görüntüsü için adı</span><span class="sxs-lookup"><span data-stu-id="8d4ba-142">Name for hello managed disk image that is created</span></span> |

```json
{
  "builders": [{
    "type": "azure-arm",

    "client_id": "0831b578-8ab6-40b9-a581-9a880a94aab1",
    "client_secret": "P@ssw0rd!",
    "tenant_id": "72f988bf-86f1-41af-91ab-2d7cd011db47",
    "subscription_id": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxx",
    "object_id": "a7dfb070-0d5b-47ac-b9a5-cf214fff0ae2",

    "managed_image_resource_group_name": "myResourceGroup",
    "managed_image_name": "myPackerImage",

    "os_type": "Windows",
    "image_publisher": "MicrosoftWindowsServer",
    "image_offer": "WindowsServer",
    "image_sku": "2016-Datacenter",

    "communicator": "winrm",
    "winrm_use_ssl": "true",
    "winrm_insecure": "true",
    "winrm_timeout": "3m",
    "winrm_username": "packer",

    "azure_tags": {
        "dept": "Engineering",
        "task": "Image deployment"
    },

    "location": "East US",
    "vm_size": "Standard_DS2_v2"
  }],
  "provisioners": [{
    "type": "powershell",
    "inline": [
      "Add-WindowsFeature Web-Server",
      "if( Test-Path $Env:SystemRoot\\windows\\system32\\Sysprep\\unattend.xml ){ rm $Env:SystemRoot\\windows\\system32\\Sysprep\\unattend.xml -Force}",
      "& $Env:SystemRoot\\System32\\Sysprep\\Sysprep.exe /oobe /generalize /shutdown /quiet"
    ]
  }]
}
```

<span data-ttu-id="8d4ba-143">Bu şablon Windows Server 2016 VM oluşturur, IIS yükler ve sonra hello Sysprep ile VM genelleştirir.</span><span class="sxs-lookup"><span data-stu-id="8d4ba-143">This template builds a Windows Server 2016 VM, installs IIS, then generalizes hello VM with Sysprep.</span></span>


## <a name="build-packer-image"></a><span data-ttu-id="8d4ba-144">Packer yansıması oluştur</span><span class="sxs-lookup"><span data-stu-id="8d4ba-144">Build Packer image</span></span>
<span data-ttu-id="8d4ba-145">Yerel makinenizde yüklü Packer zaten yoksa [hello Packer yükleme yönergelerini izleyin](https://www.packer.io/docs/install/index.html).</span><span class="sxs-lookup"><span data-stu-id="8d4ba-145">If you don't already have Packer installed on your local machine, [follow hello Packer installation instructions](https://www.packer.io/docs/install/index.html).</span></span>

<span data-ttu-id="8d4ba-146">Merhaba görüntüsünü, Packer belirterek şablon dosyasını aşağıdaki gibi oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="8d4ba-146">Build hello image by specifying your Packer template file as follows:</span></span>

```bash
./packer build windows.json
```

<span data-ttu-id="8d4ba-147">Komutları önceki hello hello çıktının bir örnek aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="8d4ba-147">An example of hello output from hello preceding commands is as follows:</span></span>

```bash
azure-arm output will be in this color.

==> azure-arm: Running builder ...
    azure-arm: Creating Azure Resource Manager (ARM) client ...
==> azure-arm: Creating resource group ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> Location          : ‘East US’
==> azure-arm:  -> Tags              :
==> azure-arm:  ->> task : Image deployment
==> azure-arm:  ->> dept : Engineering
==> azure-arm: Validating deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> DeploymentName    : ‘pkrdppq0mthtbtt’
==> azure-arm: Deploying deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> DeploymentName    : ‘pkrdppq0mthtbtt’
==> azure-arm: Getting hello certificate’s URL ...
==> azure-arm:  -> Key Vault Name        : ‘pkrkvpq0mthtbtt’
==> azure-arm:  -> Key Vault Secret Name : ‘packerKeyVaultSecret’
==> azure-arm:  -> Certificate URL       : ‘https://pkrkvpq0mthtbtt.vault.azure.net/secrets/packerKeyVaultSecret/8c7bd823e4fa44e1abb747636128adbb'
==> azure-arm: Setting hello certificate’s URL ...
==> azure-arm: Validating deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> DeploymentName    : ‘pkrdppq0mthtbtt’
==> azure-arm: Deploying deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> DeploymentName    : ‘pkrdppq0mthtbtt’
==> azure-arm: Getting hello VM’s IP address ...
==> azure-arm:  -> ResourceGroupName   : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> PublicIPAddressName : ‘packerPublicIP’
==> azure-arm:  -> NicName             : ‘packerNic’
==> azure-arm:  -> Network Connection  : ‘PublicEndpoint’
==> azure-arm:  -> IP Address          : ‘40.76.55.35’
==> azure-arm: Waiting for WinRM toobecome available...
==> azure-arm: Connected tooWinRM!
==> azure-arm: Provisioning with Powershell...
==> azure-arm: Provisioning with shell script: /var/folders/h1/ymh5bdx15wgdn5hvgj1wc0zh0000gn/T/packer-powershell-provisioner902510110
    azure-arm: #< CLIXML
    azure-arm:
    azure-arm: Success Restart Needed Exit Code      Feature Result
    azure-arm: ------- -------------- ---------      --------------
    azure-arm: True    No             Success        {Common HTTP Features, Default Document, D...
    azure-arm: <Objs Version=“1.1.0.1” xmlns=“http://schemas.microsoft.com/powershell/2004/04"><Obj S=“progress” RefId=“0"><TN RefId=“0”><T>System.Management.Automation.PSCustomObject</T><T>System.Object</T></TN><MS><I64 N=“SourceId”>1</I64><PR N=“Record”><AV>Preparing modules for first use.</AV><AI>0</AI><Nil /><PI>-1</PI><PC>-1</PC><T>Completed</T><SR>-1</SR><SD> </SD></PR></MS></Obj></Objs>
==> azure-arm: Querying hello machine’s properties ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> ComputeName       : ‘pkrvmpq0mthtbtt’
==> azure-arm:  -> Managed OS Disk   : ‘/subscriptions/guid/resourceGroups/packer-Resource-Group-pq0mthtbtt/providers/Microsoft.Compute/disks/osdisk’
==> azure-arm: Powering off machine ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> ComputeName       : ‘pkrvmpq0mthtbtt’
==> azure-arm: Capturing image ...
==> azure-arm:  -> Compute ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> Compute Name              : ‘pkrvmpq0mthtbtt’
==> azure-arm:  -> Compute Location          : ‘East US’
==> azure-arm:  -> Image ResourceGroupName   : ‘myResourceGroup’
==> azure-arm:  -> Image Name                : ‘myPackerImage’
==> azure-arm:  -> Image Location            : ‘eastus’
==> azure-arm: Deleting resource group ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm: Deleting hello temporary OS disk ...
==> azure-arm:  -> OS Disk : skipping, managed disk was used...
Build ‘azure-arm’ finished.

==> Builds finished. hello artifacts of successful builds are:
--> azure-arm: Azure.ResourceManagement.VMImage:

ManagedImageResourceGroupName: myResourceGroup
ManagedImageName: myPackerImage
ManagedImageLocation: eastus
```

<span data-ttu-id="8d4ba-148">Merhaba dağıtım temizleme ve Packer toobuild hello VM hello provisioners çalıştırmak için birkaç dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="8d4ba-148">It takes a few minutes for Packer toobuild hello VM, run hello provisioners, and clean up hello deployment.</span></span>


## <a name="create-vm-from-azure-image"></a><span data-ttu-id="8d4ba-149">Azure görüntüden VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="8d4ba-149">Create VM from Azure Image</span></span>
<span data-ttu-id="8d4ba-150">Yönetici olan hello VM'ler için kullanıcı adı ve parola ayarlayın [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential).</span><span class="sxs-lookup"><span data-stu-id="8d4ba-150">Set an administrator username and password for hello VMs with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential).</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="8d4ba-151">Artık bir VM ile görüntüden oluşturabilirsiniz [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="8d4ba-151">You can now create a VM from your Image with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="8d4ba-152">Merhaba aşağıdaki örnekte oluşturur adlı bir VM'den *myVM* gelen *myPackerImage*.</span><span class="sxs-lookup"><span data-stu-id="8d4ba-152">hello following example creates a VM named *myVM* from *myPackerImage*.</span></span>

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName $rgName `
    -Location $location `
    -Name myVnet `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$publicIP = New-AzureRmPublicIpAddress `
    -ResourceGroupName $rgName `
    -Location $location `
    -AllocationMethod "Static" `
    -IdleTimeoutInMinutes 4 `
    -Name "myPublicIP"

# Create an inbound network security group rule for port 80
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig `
    -Name myNetworkSecurityGroupRuleWWW  `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1001 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 80 `
    -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName $rgName `
    -Location $location `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRuleWeb

# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface `
    -Name myNic `
    -ResourceGroupName $rgName `
    -Location $location `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $publicIP.Id `
    -NetworkSecurityGroupId $nsg.Id

# Define hello image created by Packer
$image = Get-AzureRMImage -ImageName myPackerImage -ResourceGroupName $rgName

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_DS2 | `
Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
Set-AzureRmVMSourceImage -Id $image.Id | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vmConfig
```

<span data-ttu-id="8d4ba-153">Birkaç dakika toocreate hello VM alır.</span><span class="sxs-lookup"><span data-stu-id="8d4ba-153">It takes a few minutes toocreate hello VM.</span></span>


## <a name="test-vm-and-iis"></a><span data-ttu-id="8d4ba-154">Test VM ve IIS</span><span class="sxs-lookup"><span data-stu-id="8d4ba-154">Test VM and IIS</span></span>
<span data-ttu-id="8d4ba-155">Merhaba, VM ile genel IP adresi elde [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="8d4ba-155">Obtain hello public IP address of your VM with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="8d4ba-156">Merhaba aşağıdaki örnek alacağı için başlangıç IP adresi *myPublicIP* daha önce oluşturduğunuz:</span><span class="sxs-lookup"><span data-stu-id="8d4ba-156">hello following example obtains hello IP address for *myPublicIP* created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName $rgName `
    -Name "myPublicIP" | select "IpAddress"
```

<span data-ttu-id="8d4ba-157">Ardından tooa web tarayıcısında hello genel IP adresi girebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8d4ba-157">You can then enter hello public IP address in tooa web browser.</span></span>

![Varsayılan IIS sitesi](./media/build-image-with-packer/iis.png) 


## <a name="next-steps"></a><span data-ttu-id="8d4ba-159">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8d4ba-159">Next steps</span></span>
<span data-ttu-id="8d4ba-160">Bu örnekte, yüklü IIS ile Packer toocreate bir VM görüntüsü kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8d4ba-160">In this example, you used Packer toocreate a VM image with IIS already installed.</span></span> <span data-ttu-id="8d4ba-161">Var olan dağıtım iş akışları, uygulama tooVMs hello Team Services, Ansible, Chef veya Puppet görüntüsüyle oluşturulan toodeploy gibi yanı sıra bu VM görüntüsü kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8d4ba-161">You can use this VM image alongside existing deployment workflows, such as toodeploy your app tooVMs created from hello Image with Team Services, Ansible, Chef, or Puppet.</span></span>

<span data-ttu-id="8d4ba-162">Diğer Windows distro'lar için ek örnek Packer şablonları için bkz: [bu GitHub deposuna](https://github.com/hashicorp/packer/tree/master/examples/azure).</span><span class="sxs-lookup"><span data-stu-id="8d4ba-162">For additional example Packer templates for other Windows distros, see [this GitHub repo](https://github.com/hashicorp/packer/tree/master/examples/azure).</span></span>