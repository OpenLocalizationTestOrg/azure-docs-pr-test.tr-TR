---
title: "Windows Azure VM görüntülerini ile Packer oluşturma | Microsoft Docs"
description: "Azure'da Windows sanal makine görüntülerini oluşturmak için Packer kullanmayı öğrenin"
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
ms.openlocfilehash: 11a4a4d65be09e6c518836c25bb455a6df738dcb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-packer-to-create-windows-virtual-machine-images-in-azure"></a><span data-ttu-id="ac0f3-103">Azure'da Windows sanal makine görüntülerini oluşturmak için Packer kullanma</span><span class="sxs-lookup"><span data-stu-id="ac0f3-103">How to use Packer to create Windows virtual machine images in Azure</span></span>
<span data-ttu-id="ac0f3-104">Azure her sanal makine (VM) Windows Dağıtım ve işletim sistemi sürümü tanımlayan bir görüntüden oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="ac0f3-104">Each virtual machine (VM) in Azure is created from an image that defines the Windows distribution and OS version.</span></span> <span data-ttu-id="ac0f3-105">Görüntüleri, önceden yüklenmiş uygulamalar ve yapılandırmalar içerebilir.</span><span class="sxs-lookup"><span data-stu-id="ac0f3-105">Images can include pre-installed applications and configurations.</span></span> <span data-ttu-id="ac0f3-106">Azure Market birçok ilk ve üçüncü taraf en yaygın işletim sistemi için sağlar ve uygulama ortamları veya gereksinimlerinize göre tasarlanmıştır, kendi özel görüntülerinizi oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ac0f3-106">The Azure Marketplace provides many first and third-party images for most common OS' and application environments, or you can create your own custom images tailored to your needs.</span></span> <span data-ttu-id="ac0f3-107">Bu makalede açık kaynak aracının nasıl kullanılacağını ayrıntıları [Packer](https://www.packer.io/) tanımlamak ve Azure özel görüntülerinizi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="ac0f3-107">This article details how to use the open source tool [Packer](https://www.packer.io/) to define and build custom images in Azure.</span></span>


## <a name="create-azure-resource-group"></a><span data-ttu-id="ac0f3-108">Azure kaynak grubu oluşturun</span><span class="sxs-lookup"><span data-stu-id="ac0f3-108">Create Azure resource group</span></span>
<span data-ttu-id="ac0f3-109">Kaynak VM oluştururken oluşturma işlemi sırasında geçici Azure kaynaklarını Packer oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ac0f3-109">During the build process, Packer creates temporary Azure resources as it builds the source VM.</span></span> <span data-ttu-id="ac0f3-110">Bir görüntü olarak kullanmak için bu kaynak VM yakalamak için bir kaynak grubu tanımlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ac0f3-110">To capture that source VM for use as an image, you must define a resource group.</span></span> <span data-ttu-id="ac0f3-111">Çıktısı Packer oluşturma işlemi, bu kaynak grubunda depolanır.</span><span class="sxs-lookup"><span data-stu-id="ac0f3-111">The output from the Packer build process is stored in this resource group.</span></span>

<span data-ttu-id="ac0f3-112">Bir kaynak grubu ile oluşturmak [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="ac0f3-112">Create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="ac0f3-113">Aşağıdaki örnek, bir kaynak grubu oluşturur *myResourceGroup* içinde *eastus* konumu:</span><span class="sxs-lookup"><span data-stu-id="ac0f3-113">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```powershell
$rgName = "myResourceGroup"
$location = "East US"
New-AzureRmResourceGroup -Name $rgName -Location $location
```

## <a name="create-azure-credentials"></a><span data-ttu-id="ac0f3-114">Azure kimlik bilgileri oluşturun</span><span class="sxs-lookup"><span data-stu-id="ac0f3-114">Create Azure credentials</span></span>
<span data-ttu-id="ac0f3-115">Packer bir hizmet sorumlusu kullanarak Azure ile kimliğini doğrular.</span><span class="sxs-lookup"><span data-stu-id="ac0f3-115">Packer authenticates with Azure using a service principal.</span></span> <span data-ttu-id="ac0f3-116">Bir Azure hizmet sorumlusu uygulamaları, hizmetleri ve Packer gibi Otomasyon araçları ile birlikte kullanabileceğiniz bir güvenlik kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="ac0f3-116">An Azure service principal is a security identity that you can use with apps, services, and automation tools like Packer.</span></span> <span data-ttu-id="ac0f3-117">Denetim ve hizmet sorumlusu Azure'da gerçekleştirebilirsiniz ne gibi işlemler için izinler tanımlar.</span><span class="sxs-lookup"><span data-stu-id="ac0f3-117">You control and define the permissions as to what operations the service principal can perform in Azure.</span></span>

<span data-ttu-id="ac0f3-118">Bir hizmet sorumlusu ile oluşturma [yeni AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) ve hizmet sorumlusu oluşturmak ve kaynakları yönetmek izinleri atayın [New-AzureRmRoleAssignment](/powershell/module/azurerm.resources/new-azurermroleassignment):</span><span class="sxs-lookup"><span data-stu-id="ac0f3-118">Create a service principal with [New-AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) and assign permissions for the service principal to create and manage resources with [New-AzureRmRoleAssignment](/powershell/module/azurerm.resources/new-azurermroleassignment):</span></span>

```powershell
$sp = New-AzureRmADServicePrincipal -DisplayName "Azure Packer IKF" -Password "P@ssw0rd!"
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

<span data-ttu-id="ac0f3-119">Azure için kimlik doğrulaması için Azure Kiracı ve abonelik kimlikleri ile elde etmeniz [Get-AzureRmSubscription](/powershell/module/azurerm.profile/get-azurermsubscription):</span><span class="sxs-lookup"><span data-stu-id="ac0f3-119">To authenticate to Azure, you also need to obtain your Azure tenant and subscription IDs with [Get-AzureRmSubscription](/powershell/module/azurerm.profile/get-azurermsubscription):</span></span>

```powershell
$sub = Get-AzureRmSubscription
$sub.TenantId
$sub.SubscriptionId
```

<span data-ttu-id="ac0f3-120">Sonraki adımda bu iki kimlikleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="ac0f3-120">You use these two IDs in the next step.</span></span>


## <a name="define-packer-template"></a><span data-ttu-id="ac0f3-121">Packer şablon oluştur</span><span class="sxs-lookup"><span data-stu-id="ac0f3-121">Define Packer template</span></span>
<span data-ttu-id="ac0f3-122">Görüntüleri oluşturmak için bir şablon bir JSON dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ac0f3-122">To build images, you create a template as a JSON file.</span></span> <span data-ttu-id="ac0f3-123">Şablonda oluşturucular ve gerçek derleme işlemini yürütmek provisioners tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="ac0f3-123">In the template, you define builders and provisioners that carry out the actual build process.</span></span> <span data-ttu-id="ac0f3-124">Packer sahip bir [Azure sağlayıcısı](https://www.packer.io/docs/builders/azure.html) sağlayan Azure kaynaklarını tanımlamak önceki oluşturulan hizmet asıl kimlik bilgilerini adım gibi.</span><span class="sxs-lookup"><span data-stu-id="ac0f3-124">Packer has a [provisioner for Azure](https://www.packer.io/docs/builders/azure.html) that allows you to define Azure resources, such as the service principal credentials created in the preceding step.</span></span>

<span data-ttu-id="ac0f3-125">Adlı bir dosya oluşturun *windows.json* ve aşağıdaki içeriği yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="ac0f3-125">Create a file named *windows.json* and paste the following content.</span></span> <span data-ttu-id="ac0f3-126">Aşağıdakiler için kendi değerlerinizi girin:</span><span class="sxs-lookup"><span data-stu-id="ac0f3-126">Enter your own values for the following:</span></span>

| <span data-ttu-id="ac0f3-127">Parametre</span><span class="sxs-lookup"><span data-stu-id="ac0f3-127">Parameter</span></span>                           | <span data-ttu-id="ac0f3-128">Nereden</span><span class="sxs-lookup"><span data-stu-id="ac0f3-128">Where to obtain</span></span> |
|-------------------------------------|----------------------------------------------------|
| <span data-ttu-id="ac0f3-129">*client_id*</span><span class="sxs-lookup"><span data-stu-id="ac0f3-129">*client_id*</span></span>                         | <span data-ttu-id="ac0f3-130">Görünüm hizmet asıl kimliği ile`$sp.applicationId`</span><span class="sxs-lookup"><span data-stu-id="ac0f3-130">View service principal ID with `$sp.applicationId`</span></span> |
| <span data-ttu-id="ac0f3-131">*client_secret*</span><span class="sxs-lookup"><span data-stu-id="ac0f3-131">*client_secret*</span></span>                     | <span data-ttu-id="ac0f3-132">Belirttiğiniz parola`$securePassword`</span><span class="sxs-lookup"><span data-stu-id="ac0f3-132">Password you specified in `$securePassword`</span></span> |
| <span data-ttu-id="ac0f3-133">*tenant_id*</span><span class="sxs-lookup"><span data-stu-id="ac0f3-133">*tenant_id*</span></span>                         | <span data-ttu-id="ac0f3-134">Çıktı `$sub.TenantId` komutu</span><span class="sxs-lookup"><span data-stu-id="ac0f3-134">Output from `$sub.TenantId` command</span></span> |
| <span data-ttu-id="ac0f3-135">*ABONELİK_KİMLİĞİ*</span><span class="sxs-lookup"><span data-stu-id="ac0f3-135">*subscription_id*</span></span>                   | <span data-ttu-id="ac0f3-136">Çıktı `$sub.SubscriptionId` komutu</span><span class="sxs-lookup"><span data-stu-id="ac0f3-136">Output from `$sub.SubscriptionId` command</span></span> |
| <span data-ttu-id="ac0f3-137">*object_id*</span><span class="sxs-lookup"><span data-stu-id="ac0f3-137">*object_id*</span></span>                         | <span data-ttu-id="ac0f3-138">Görünüm hizmet asıl nesne kimliği ile`$sp.Id`</span><span class="sxs-lookup"><span data-stu-id="ac0f3-138">View service principal object ID with `$sp.Id`</span></span> |
| <span data-ttu-id="ac0f3-139">*managed_image_resource_group_name*</span><span class="sxs-lookup"><span data-stu-id="ac0f3-139">*managed_image_resource_group_name*</span></span> | <span data-ttu-id="ac0f3-140">İlk adımda oluşturduğunuz kaynak grubunun adı</span><span class="sxs-lookup"><span data-stu-id="ac0f3-140">Name of resource group you created in the first step</span></span> |
| <span data-ttu-id="ac0f3-141">*managed_image_name*</span><span class="sxs-lookup"><span data-stu-id="ac0f3-141">*managed_image_name*</span></span>                | <span data-ttu-id="ac0f3-142">Oluşturulan yönetilen disk görüntüsü için adı</span><span class="sxs-lookup"><span data-stu-id="ac0f3-142">Name for the managed disk image that is created</span></span> |

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

<span data-ttu-id="ac0f3-143">Bu şablon Windows Server 2016 VM oluşturur, IIS yükler ve sonra Sysprep ile VM genelleştirir.</span><span class="sxs-lookup"><span data-stu-id="ac0f3-143">This template builds a Windows Server 2016 VM, installs IIS, then generalizes the VM with Sysprep.</span></span>


## <a name="build-packer-image"></a><span data-ttu-id="ac0f3-144">Packer yansıması oluştur</span><span class="sxs-lookup"><span data-stu-id="ac0f3-144">Build Packer image</span></span>
<span data-ttu-id="ac0f3-145">Yerel makinenizde yüklü Packer zaten yoksa [Packer yükleme yönergelerini izleyin](https://www.packer.io/docs/install/index.html).</span><span class="sxs-lookup"><span data-stu-id="ac0f3-145">If you don't already have Packer installed on your local machine, [follow the Packer installation instructions](https://www.packer.io/docs/install/index.html).</span></span>

<span data-ttu-id="ac0f3-146">Görüntü, Packer belirterek şablon dosyası gibi oluşturun:</span><span class="sxs-lookup"><span data-stu-id="ac0f3-146">Build the image by specifying your Packer template file as follows:</span></span>

```bash
./packer build windows.json
```

<span data-ttu-id="ac0f3-147">Çıkış örneği önceki komutlarındaki aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="ac0f3-147">An example of the output from the preceding commands is as follows:</span></span>

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
==> azure-arm: Getting the certificate’s URL ...
==> azure-arm:  -> Key Vault Name        : ‘pkrkvpq0mthtbtt’
==> azure-arm:  -> Key Vault Secret Name : ‘packerKeyVaultSecret’
==> azure-arm:  -> Certificate URL       : ‘https://pkrkvpq0mthtbtt.vault.azure.net/secrets/packerKeyVaultSecret/8c7bd823e4fa44e1abb747636128adbb'
==> azure-arm: Setting the certificate’s URL ...
==> azure-arm: Validating deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> DeploymentName    : ‘pkrdppq0mthtbtt’
==> azure-arm: Deploying deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> DeploymentName    : ‘pkrdppq0mthtbtt’
==> azure-arm: Getting the VM’s IP address ...
==> azure-arm:  -> ResourceGroupName   : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> PublicIPAddressName : ‘packerPublicIP’
==> azure-arm:  -> NicName             : ‘packerNic’
==> azure-arm:  -> Network Connection  : ‘PublicEndpoint’
==> azure-arm:  -> IP Address          : ‘40.76.55.35’
==> azure-arm: Waiting for WinRM to become available...
==> azure-arm: Connected to WinRM!
==> azure-arm: Provisioning with Powershell...
==> azure-arm: Provisioning with shell script: /var/folders/h1/ymh5bdx15wgdn5hvgj1wc0zh0000gn/T/packer-powershell-provisioner902510110
    azure-arm: #< CLIXML
    azure-arm:
    azure-arm: Success Restart Needed Exit Code      Feature Result
    azure-arm: ------- -------------- ---------      --------------
    azure-arm: True    No             Success        {Common HTTP Features, Default Document, D...
    azure-arm: <Objs Version=“1.1.0.1” xmlns=“http://schemas.microsoft.com/powershell/2004/04"><Obj S=“progress” RefId=“0"><TN RefId=“0”><T>System.Management.Automation.PSCustomObject</T><T>System.Object</T></TN><MS><I64 N=“SourceId”>1</I64><PR N=“Record”><AV>Preparing modules for first use.</AV><AI>0</AI><Nil /><PI>-1</PI><PC>-1</PC><T>Completed</T><SR>-1</SR><SD> </SD></PR></MS></Obj></Objs>
==> azure-arm: Querying the machine’s properties ...
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
==> azure-arm: Deleting the temporary OS disk ...
==> azure-arm:  -> OS Disk : skipping, managed disk was used...
Build ‘azure-arm’ finished.

==> Builds finished. The artifacts of successful builds are:
--> azure-arm: Azure.ResourceManagement.VMImage:

ManagedImageResourceGroupName: myResourceGroup
ManagedImageName: myPackerImage
ManagedImageLocation: eastus
```

<span data-ttu-id="ac0f3-148">VM oluşturmak için provisioners çalıştırıp dağıtım temizlemek Packer birkaç dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="ac0f3-148">It takes a few minutes for Packer to build the VM, run the provisioners, and clean up the deployment.</span></span>


## <a name="create-vm-from-azure-image"></a><span data-ttu-id="ac0f3-149">Azure görüntüden VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="ac0f3-149">Create VM from Azure Image</span></span>
<span data-ttu-id="ac0f3-150">Yönetici olan VM'ler için kullanıcı adı ve parola ayarlayın [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential).</span><span class="sxs-lookup"><span data-stu-id="ac0f3-150">Set an administrator username and password for the VMs with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential).</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="ac0f3-151">Artık bir VM ile görüntüden oluşturabilirsiniz [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="ac0f3-151">You can now create a VM from your Image with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="ac0f3-152">Aşağıdaki örnek, adlandırılmış bir VM'nin oluşturur *myVM* gelen *myPackerImage*.</span><span class="sxs-lookup"><span data-stu-id="ac0f3-152">The following example creates a VM named *myVM* from *myPackerImage*.</span></span>

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

# Define the image created by Packer
$image = Get-AzureRMImage -ImageName myPackerImage -ResourceGroupName $rgName

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_DS2 | `
Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
Set-AzureRmVMSourceImage -Id $image.Id | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vmConfig
```

<span data-ttu-id="ac0f3-153">VM oluşturmak için birkaç dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="ac0f3-153">It takes a few minutes to create the VM.</span></span>


## <a name="test-vm-and-iis"></a><span data-ttu-id="ac0f3-154">Test VM ve IIS</span><span class="sxs-lookup"><span data-stu-id="ac0f3-154">Test VM and IIS</span></span>
<span data-ttu-id="ac0f3-155">VM ile genel IP adresi elde [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="ac0f3-155">Obtain the public IP address of your VM with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="ac0f3-156">Aşağıdaki örnek IP adresi alacağı *myPublicIP* daha önce oluşturduğunuz:</span><span class="sxs-lookup"><span data-stu-id="ac0f3-156">The following example obtains the IP address for *myPublicIP* created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName $rgName `
    -Name "myPublicIP" | select "IpAddress"
```

<span data-ttu-id="ac0f3-157">Bir web tarayıcısı ortak IP adresi girebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ac0f3-157">You can then enter the public IP address in to a web browser.</span></span>

![Varsayılan IIS sitesi](./media/build-image-with-packer/iis.png) 


## <a name="next-steps"></a><span data-ttu-id="ac0f3-159">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ac0f3-159">Next steps</span></span>
<span data-ttu-id="ac0f3-160">Bu örnekte, Packer IIS zaten yüklü bir VM görüntüsü oluşturmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ac0f3-160">In this example, you used Packer to create a VM image with IIS already installed.</span></span> <span data-ttu-id="ac0f3-161">Varolan dağıtım iş akışları, yanı sıra bu VM görüntüsü gibi Team Services, Ansible, Chef veya Puppet görüntüden oluşturulan VM'ler için uygulamanızı dağıtmak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ac0f3-161">You can use this VM image alongside existing deployment workflows, such as to deploy your app to VMs created from the Image with Team Services, Ansible, Chef, or Puppet.</span></span>

<span data-ttu-id="ac0f3-162">Diğer Windows distro'lar için ek örnek Packer şablonları için bkz: [bu GitHub deposuna](https://github.com/hashicorp/packer/tree/master/examples/azure).</span><span class="sxs-lookup"><span data-stu-id="ac0f3-162">For additional example Packer templates for other Windows distros, see [this GitHub repo](https://github.com/hashicorp/packer/tree/master/examples/azure).</span></span>