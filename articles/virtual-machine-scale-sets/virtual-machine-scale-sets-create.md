---
title: "Bir Azure sanal makine ölçek kümesi oluşturma | Microsoft Docs"
description: "Oluşturun ve Azure CLI, PowerShell, şablon veya Visual Studio ile ayarlanmış bir Linux veya Windows Azure sanal makine ölçek dağıtın."
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 07/21/2017
ms.author: adegeo
ms.openlocfilehash: 32af01aa545c541688128a7ae6bbb82a0e046f2d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="create-and-deploy-a-virtual-machine-scale-set"></a><span data-ttu-id="11f22-103">Oluşturma ve bir sanal makine ölçek kümesini dağıtma</span><span class="sxs-lookup"><span data-stu-id="11f22-103">Create and deploy a virtual machine scale set</span></span>
<span data-ttu-id="11f22-104">Sanal makine ölçek kümeleri dağıtmak ve bir küme olarak aynı sanal makineleri yönetmek için kolay hale getirir.</span><span class="sxs-lookup"><span data-stu-id="11f22-104">Virtual machine scale sets make it easy for you to deploy and manage identical virtual machines as a set.</span></span> <span data-ttu-id="11f22-105">Ölçek kümeleri ölçekte uygulamalar için yüksek oranda ölçeklenebilir ve özelleştirilebilir bilgi işlem katmanını sağlar ve Windows platform görüntüleri, Linux platform görüntüleri, özel resimler ve uzantıları destekler.</span><span class="sxs-lookup"><span data-stu-id="11f22-105">Scale sets provide a highly scalable and customizable compute layer for hyperscale applications, and they support Windows platform images, Linux platform images, custom images, and extensions.</span></span> <span data-ttu-id="11f22-106">Ölçek kümeleri hakkında daha fazla bilgi için bkz: [sanal makine ölçek kümeleri](virtual-machine-scale-sets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="11f22-106">For more information about scale sets, see [Virtual machine scale sets](virtual-machine-scale-sets-overview.md).</span></span>

<span data-ttu-id="11f22-107">Bu öğreticide, bir sanal makine ölçek kümesi oluşturmak nasıl gösterilir **olmadan** Azure portalını kullanarak.</span><span class="sxs-lookup"><span data-stu-id="11f22-107">This tutorial shows you how to create a virtual machine scale set **without** using the Azure portal.</span></span> <span data-ttu-id="11f22-108">Azure Portalı'nı kullanma hakkında daha fazla bilgi için bkz: [kümesinin nasıl bir sanal makine ölçek oluşturulacağı Azure portalıyla](virtual-machine-scale-sets-portal-create.md).</span><span class="sxs-lookup"><span data-stu-id="11f22-108">For information about how to use the Azure portal, see [How to create a virtual machine scale set with the Azure portal](virtual-machine-scale-sets-portal-create.md).</span></span>

>[!NOTE]
><span data-ttu-id="11f22-109">Azure Resource Manager kaynakları hakkında daha fazla bilgi için bkz: [Azure Resource Manager ve klasik dağıtım](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="11f22-109">For more information about Azure Resource Manager resources, see [Azure Resource Manager vs. classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>

## <a name="sign-in-to-azure"></a><span data-ttu-id="11f22-110">Azure'da oturum açma</span><span class="sxs-lookup"><span data-stu-id="11f22-110">Sign in to Azure</span></span>

<span data-ttu-id="11f22-111">Bir ölçek kümesi oluşturmak için Azure CLI 2.0 veya Azure PowerShell kullanıyorsanız, önce aboneliğinize imzalamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="11f22-111">If you're using Azure CLI 2.0 or Azure PowerShell to create a scale set, you first need to sign in to your subscription.</span></span>

<span data-ttu-id="11f22-112">Yüklemek, ayarlayın ve Azure CLI veya PowerShell ile Azure oturumu hakkında daha fazla bilgi için bkz: [Azure CLI 2.0 ile çalışmaya başlama](/cli/azure/get-started-with-azure-cli.md) veya [Azure PowerShell cmdlet'leri kullanmaya başlama](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="11f22-112">For more information about how to install, set up, and sign in to Azure with Azure CLI or PowerShell, see [Getting Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md) or [Get started with Azure PowerShell cmdlets](/powershell/azure/overview).</span></span>

```azurecli
az login
```

```powershell
Login-AzureRmAccount
```

## <a name="create-a-resource-group"></a><span data-ttu-id="11f22-113">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="11f22-113">Create a resource group</span></span>

<span data-ttu-id="11f22-114">İlk sanal makine ölçek kümesi ile ilişkili bir kaynak grubu oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="11f22-114">You first need to create a resource group that the virtual machine scale set is associated with.</span></span>

```azurecli
az group create --location westus2 --name MyResourceGroup1
```

```powershell
New-AzureRmResourceGroup -Location westus2 -Name MyResourceGroup1
```

## <a name="create-from-azure-cli"></a><span data-ttu-id="11f22-115">Azure CLI üzerinden oluşturma</span><span class="sxs-lookup"><span data-stu-id="11f22-115">Create from Azure CLI</span></span>

<span data-ttu-id="11f22-116">Azure CLI ile en az çaba ile ayarlanmış bir sanal makine ölçek oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="11f22-116">With Azure CLI, you can create a virtual machine scale set with minimal effort.</span></span> <span data-ttu-id="11f22-117">Varsayılan değerleri atlarsanız, bunlar sizin için sağlanır.</span><span class="sxs-lookup"><span data-stu-id="11f22-117">If you omit default values, they are provided for you.</span></span> <span data-ttu-id="11f22-118">Örneğin, herhangi bir sanal ağ bilgi belirtmezseniz, bir sanal ağ sizin için oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="11f22-118">For example, if you don't specify any virtual network information, a virtual network is created for you.</span></span> <span data-ttu-id="11f22-119">Aşağıdaki bölümleri atlarsanız, bunlar sizin için oluşturulur:</span><span class="sxs-lookup"><span data-stu-id="11f22-119">If you omit the following parts, they are created for you:</span></span> 
- <span data-ttu-id="11f22-120">Bir yük dengeleyici</span><span class="sxs-lookup"><span data-stu-id="11f22-120">A load balancer</span></span>
- <span data-ttu-id="11f22-121">Bir sanal ağ</span><span class="sxs-lookup"><span data-stu-id="11f22-121">A virtual network</span></span>
- <span data-ttu-id="11f22-122">Bir ortak IP adresi</span><span class="sxs-lookup"><span data-stu-id="11f22-122">A public IP address</span></span>

<span data-ttu-id="11f22-123">Sanal makine ölçek kümesi üzerinde kullanmak istediğiniz sanal makine görüntüsü seçerken, birkaç seçeneğiniz vardır:</span><span class="sxs-lookup"><span data-stu-id="11f22-123">When choosing the virtual machine image that you want to use on the virtual machine scale set, you have a few choices:</span></span>

- <span data-ttu-id="11f22-124">URN</span><span class="sxs-lookup"><span data-stu-id="11f22-124">URN</span></span>  
<span data-ttu-id="11f22-125">Bir kaynak tanımlayıcısı:</span><span class="sxs-lookup"><span data-stu-id="11f22-125">The identifier of a resource:</span></span>  
<span data-ttu-id="11f22-126">**Win2012R2Datacenter**</span><span class="sxs-lookup"><span data-stu-id="11f22-126">**Win2012R2Datacenter**</span></span>

- <span data-ttu-id="11f22-127">URN diğer adı</span><span class="sxs-lookup"><span data-stu-id="11f22-127">URN alias</span></span>  
<span data-ttu-id="11f22-128">Bir URN kolay adı:</span><span class="sxs-lookup"><span data-stu-id="11f22-128">The friendly name of a URN:</span></span>  
<span data-ttu-id="11f22-129">**MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest**</span><span class="sxs-lookup"><span data-stu-id="11f22-129">**MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest**</span></span>

- <span data-ttu-id="11f22-130">Özel kaynak kimliği</span><span class="sxs-lookup"><span data-stu-id="11f22-130">Custom resource id</span></span>  
<span data-ttu-id="11f22-131">Bir Azure kaynağı yolu:</span><span class="sxs-lookup"><span data-stu-id="11f22-131">The path to an Azure resource:</span></span>  
<span data-ttu-id="11f22-132">**/Subscriptions/Subscription-guid/resourceGroups/MyResourceGroup/providers/Microsoft.COMPUTE/images/MyImage**</span><span class="sxs-lookup"><span data-stu-id="11f22-132">**/subscriptions/subscription-guid/resourceGroups/MyResourceGroup/providers/Microsoft.Compute/images/MyImage**</span></span>

- <span data-ttu-id="11f22-133">Web kaynağı</span><span class="sxs-lookup"><span data-stu-id="11f22-133">Web resource</span></span>  
<span data-ttu-id="11f22-134">Bir HTTP URI yolu:</span><span class="sxs-lookup"><span data-stu-id="11f22-134">The path to an HTTP URI:</span></span>  
<span data-ttu-id="11f22-135">**http://contoso.BLOB.Core.Windows.NET/vhds/osdiskimage.vhd**</span><span class="sxs-lookup"><span data-stu-id="11f22-135">**http://contoso.blob.core.windows.net/vhds/osdiskimage.vhd**</span></span>

>[!TIP]
><span data-ttu-id="11f22-136">Kullanılabilir görüntülerle listesini almak `az vm image list`.</span><span class="sxs-lookup"><span data-stu-id="11f22-136">You can get a list of available images with `az vm image list`.</span></span>

<span data-ttu-id="11f22-137">Bir sanal makine ölçek kümesi oluşturmak için aşağıdakileri belirtmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="11f22-137">To create a virtual machine scale set, you must specify the following:</span></span>

- <span data-ttu-id="11f22-138">Kaynak grubu</span><span class="sxs-lookup"><span data-stu-id="11f22-138">Resource group</span></span> 
- <span data-ttu-id="11f22-139">Ad</span><span class="sxs-lookup"><span data-stu-id="11f22-139">Name</span></span>
- <span data-ttu-id="11f22-140">İşletim sistemi görüntüsü</span><span class="sxs-lookup"><span data-stu-id="11f22-140">Operating system image</span></span>
- <span data-ttu-id="11f22-141">Kimlik doğrulama bilgileri</span><span class="sxs-lookup"><span data-stu-id="11f22-141">Authentication information</span></span> 
 
<span data-ttu-id="11f22-142">Aşağıdaki örnek, (Bu adım birkaç dakika sürebilir) temel sanal makine ölçek kümesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="11f22-142">The following example creates a basic virtual machine scale set (this step might take a few minutes).</span></span>

```azurecli
az vmss create --resource-group MyResourceGroup1 --name MyScaleSet --image UbuntuLTS --authentication-type password --admin-username azureuser --admin-password P@ssw0rd!
```

<span data-ttu-id="11f22-143">Komut bittikten sonra oluşturulan ayarlayın, sanal makine ölçek şimdi sahip olur.</span><span class="sxs-lookup"><span data-stu-id="11f22-143">Once the command finishes you will now have your virtual machine scale set created.</span></span> <span data-ttu-id="11f22-144">Sanal makinenin IP adresi için bağlanabilmesi yapmanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="11f22-144">You may need to get the IP address of the virtual machine so that you can connect to it.</span></span> <span data-ttu-id="11f22-145">Aşağıdaki komutla bir çok sayıda sanal makine (IP adresi dahil) hakkında farklı bilgi elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="11f22-145">You can get a lot of different information about the virtual machine (including the IP address) with the following command.</span></span> 

```azurecli
az vmss list-instance-connection-info --resource-group MyResourceGroup1 --name MyScaleSet
```

## <a name="create-from-powershell"></a><span data-ttu-id="11f22-146">Powershell'den oluşturma</span><span class="sxs-lookup"><span data-stu-id="11f22-146">Create from PowerShell</span></span>

<span data-ttu-id="11f22-147">PowerShell Azure CLI kullanmak çok daha karmaşıktır.</span><span class="sxs-lookup"><span data-stu-id="11f22-147">PowerShell is more complicated to use than Azure CLI.</span></span> <span data-ttu-id="11f22-148">Azure CLI ağla ilgili kaynaklar (örneğin, yük Dengeleyiciler, IP adresleri ve sanal ağları) için varsayılan sağlarken, PowerShell desteklemez.</span><span class="sxs-lookup"><span data-stu-id="11f22-148">While Azure CLI provides defaults for networking-related resources (such as load balancers, IP addresses, and virtual networks), PowerShell does not.</span></span> <span data-ttu-id="11f22-149">PowerShell ile bir görüntü başvuran bir biraz daha çok karmaşıktır.</span><span class="sxs-lookup"><span data-stu-id="11f22-149">Referencing an image with PowerShell is a slightly more complicated too.</span></span> <span data-ttu-id="11f22-150">Aşağıdaki cmdlet ile görüntüleri alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="11f22-150">You can get images with the following cmdlets:</span></span>

1. <span data-ttu-id="11f22-151">Get-AzureRMVMImagePublisher</span><span class="sxs-lookup"><span data-stu-id="11f22-151">Get-AzureRMVMImagePublisher</span></span>
2. <span data-ttu-id="11f22-152">Get-AzureRMVMImageOffer</span><span class="sxs-lookup"><span data-stu-id="11f22-152">Get-AzureRMVMImageOffer</span></span>
3. <span data-ttu-id="11f22-153">Get-AzureRmVMImageSku</span><span class="sxs-lookup"><span data-stu-id="11f22-153">Get-AzureRmVMImageSku</span></span>

<span data-ttu-id="11f22-154">Cmdlet'leri iş sırayla yöneltilen.</span><span class="sxs-lookup"><span data-stu-id="11f22-154">The cmdlets work can be piped in sequence.</span></span> <span data-ttu-id="11f22-155">İşte bir örnek için tüm görüntüleri alma **Batı ABD 2** bölge adına sahip bir yayımcı ile **microsoft** da.</span><span class="sxs-lookup"><span data-stu-id="11f22-155">Here is an example of how to get all images for the **West US 2** region with a publisher that has the name **microsoft** in it.</span></span>

```powershell
Get-AzureRMVMImagePublisher -Location WestUS2 | Where-Object PublisherName -Like *microsoft* | Get-AzureRMVMImageOffer | Get-AzureRmVMImageSku | Select-Object PublisherName, Offer, Skus
```

```
PublisherName              Offer                    Skus
-------------              -----                    ----
microsoft-ads              linux-data-science-vm    linuxdsvm
microsoft-ads              standard-data-science-vm standard-data-science-vm
MicrosoftAzureSiteRecovery Process-Server           Windows-2012-R2-Datacenter
MicrosoftBizTalkServer     BizTalk-Server           2013-R2-Enterprise
MicrosoftBizTalkServer     BizTalk-Server           2013-R2-Standard
MicrosoftBizTalkServer     BizTalk-Server           2016-Developer
MicrosoftBizTalkServer     BizTalk-Server           2016-Enterprise
...
```

<span data-ttu-id="11f22-156">Bir sanal makine ölçek kümesi oluşturmak için iş akışı aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="11f22-156">The workflow for creating a virtual machine scale set is as follows:</span></span>

1. <span data-ttu-id="11f22-157">Ölçek kümesi hakkında bilgi içeren bir yapılandırma nesnesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="11f22-157">Create a config object that holds information about the scale set.</span></span>
2. <span data-ttu-id="11f22-158">Temel işletim sistemi görüntüsü başvuru.</span><span class="sxs-lookup"><span data-stu-id="11f22-158">Reference the base OS image.</span></span>
3. <span data-ttu-id="11f22-159">İşletim sistemi ayarlarını yapılandırın: kimlik doğrulaması, VM adı ön ekini ve kullanıcı/geçirin.</span><span class="sxs-lookup"><span data-stu-id="11f22-159">Configure the operating system settings: authentication, VM name prefix, and user/pass.</span></span>
4. <span data-ttu-id="11f22-160">Ağ yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="11f22-160">Configure networking.</span></span>
5. <span data-ttu-id="11f22-161">Ölçek kümesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="11f22-161">Create the scale set.</span></span>

<span data-ttu-id="11f22-162">Bu örnek, Windows Server 2016 sahip bir bilgisayar için temel bir iki örnekli ölçek oluşturur.</span><span class="sxs-lookup"><span data-stu-id="11f22-162">This example creates a basic two-instance scale set for a computer that has Windows Server 2016 installed.</span></span>

```powershell
# Resource group name from above
$rg = "MyResourceGroup1"
$location = "WestUS2"

# Create a config object
$vmssConfig = New-AzureRmVmssConfig -Location $location -SkuCapacity 2 -SkuName Standard_A0  -UpgradePolicyMode Automatic

# Reference a virtual machine image from the gallery
Set-AzureRmVmssStorageProfile $vmssConfig -ImageReferencePublisher MicrosoftWindowsServer -ImageReferenceOffer WindowsServer -ImageReferenceSku 2016-Datacenter -ImageReferenceVersion latest

# Set up information for authenticating with the virtual machine
Set-AzureRmVmssOsProfile $vmssConfig -AdminUsername azureuser -AdminPassword P@ssw0rd! -ComputerNamePrefix myvmssvm

# Create the virtual network resources

## Basics
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name "my-subnet" -AddressPrefix 10.0.0.0/24
$vnet = New-AzureRmVirtualNetwork -Name "my-network" -ResourceGroupName $rg -Location $location -AddressPrefix 10.0.0.0/16 -Subnet $subnet

## Load balancer
$publicIP = New-AzureRmPublicIpAddress -Name "PublicIP" -ResourceGroupName $rg -Location $location -AllocationMethod Static -DomainNameLabel "myuniquedomain"
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name "LB-Frontend" -PublicIpAddress $publicIP
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "LB-backend"
$probe = New-AzureRmLoadBalancerProbeConfig -Name "HealthProbe" -Protocol Tcp -Port 80 -IntervalInSeconds 15 -ProbeCount 2
$inboundNATRule1= New-AzureRmLoadBalancerRuleConfig -Name "webserver" -FrontendIpConfiguration $frontendIP -Protocol Tcp -FrontendPort 80 -BackendPort 80 -IdleTimeoutInMinutes 15 -Probe $probe -BackendAddressPool $backendPool
$inboundNATPool1 = New-AzureRmLoadBalancerInboundNatPoolConfig -Name "RDP" -FrontendIpConfigurationId $frontendIP.Id -Protocol TCP -FrontendPortRangeStart 53380 -FrontendPortRangeEnd 53390 -BackendPort 3389

New-AzureRmLoadBalancer -ResourceGroupName $rg -Name "LB1" -Location $location -FrontendIpConfiguration $frontendIP -LoadBalancingRule $inboundNATRule1 -InboundNatPool $inboundNATPool1 -BackendAddressPool $backendPool -Probe $probe

## IP address config
$ipConfig = New-AzureRmVmssIpConfig -Name "my-ipaddress" -LoadBalancerBackendAddressPoolsId $backendPool.Id -SubnetId $vnet.Subnets[0].Id -LoadBalancerInboundNatPoolsId $inboundNATPool1.Id

# Attach the virtual network to the IP object
Add-AzureRmVmssNetworkInterfaceConfiguration -VirtualMachineScaleSet $vmssConfig -Name "network-config" -Primary $true -IPConfiguration $ipConfig

# Create the scale set with the config object (this step might take a few minutes)
New-AzureRmVmss -ResourceGroupName $rg -Name "MyScaleSet1" -VirtualMachineScaleSet $vmssConfig
```

### <a name="using-a-custom-virtual-machine-image"></a><span data-ttu-id="11f22-163">Bir özel sanal makine görüntüsü kullanma</span><span class="sxs-lookup"><span data-stu-id="11f22-163">Using a custom virtual machine image</span></span>
<span data-ttu-id="11f22-164">Galeriden bir sanal makine görüntüsü başvuran yerine kendi özel görüntünüzü kümeden bir ölçek oluşturuyorsanız _kümesi AzureRmVmssStorageProfile_ komutu şuna benzeyebilir:</span><span class="sxs-lookup"><span data-stu-id="11f22-164">If you are creating a scale set from your own custom image, instead of referencing a virtual machine image from the gallery, the _Set-AzureRmVmssStorageProfile_ command would look like this:</span></span>
```PowerShell
Set-AzureRmVmssStorageProfile -OsDiskCreateOption FromImage -ManagedDisk PremiumLRS -OsDiskCaching "None" -OsDiskOsType Linux -ImageReferenceId (Get-AzureRmImage -ImageName $VMImage -ResourceGroupName $rg).id
```

## <a name="create-from-a-template"></a><span data-ttu-id="11f22-165">Şablondan oluşturma</span><span class="sxs-lookup"><span data-stu-id="11f22-165">Create from a template</span></span>

<span data-ttu-id="11f22-166">Bir Azure Resource Manager şablonu kullanarak bir sanal makine ölçek dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="11f22-166">You can deploy a virtual machine scale set by using an Azure Resource Manager template.</span></span> <span data-ttu-id="11f22-167">Kendi şablonunuzu oluşturun ya da birinden kullanmak [şablonu deposu](https://azure.microsoft.com/resources/templates/?term=vmss).</span><span class="sxs-lookup"><span data-stu-id="11f22-167">You can create your own template or use one from the [template repository](https://azure.microsoft.com/resources/templates/?term=vmss).</span></span> <span data-ttu-id="11f22-168">Bu şablonları Azure aboneliğinize doğrudan dağıtılabilir.</span><span class="sxs-lookup"><span data-stu-id="11f22-168">These templates can be deployed directly to your Azure subscription.</span></span>

>[!NOTE]
><span data-ttu-id="11f22-169">Kendi şablonunuzu oluşturmak için JSON metin dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="11f22-169">To create your own template, you create a JSON text file.</span></span> <span data-ttu-id="11f22-170">Oluşturma ve bir şablonu özelleştirme hakkında genel bilgi için bkz: [Azure Resource Manager şablonları](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="11f22-170">For general information about how to create and customize a template, see [Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="11f22-171">Örnek şablon kullanılabilir [github'da](https://github.com/gatneil/mvss/tree/minimum-viable-scale-set).</span><span class="sxs-lookup"><span data-stu-id="11f22-171">A sample template is available [on GitHub](https://github.com/gatneil/mvss/tree/minimum-viable-scale-set).</span></span> <span data-ttu-id="11f22-172">Oluşturun ve bu örneği kullanmak hakkında daha fazla bilgi için bkz: [en uygun ölçek kümesini](.\virtual-machine-scale-sets-mvss-start.md).</span><span class="sxs-lookup"><span data-stu-id="11f22-172">For more information about how to create and use that sample, see [Minimum viable scale set](.\virtual-machine-scale-sets-mvss-start.md).</span></span>

## <a name="create-from-visual-studio"></a><span data-ttu-id="11f22-173">Visual Studio'dan oluşturma</span><span class="sxs-lookup"><span data-stu-id="11f22-173">Create from Visual Studio</span></span>

<span data-ttu-id="11f22-174">Visual Studio ile bir Azure kaynak grubu projesi oluşturun ve şablon için bir sanal makine ölçek kümesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="11f22-174">With Visual Studio, you can create an Azure resource group project and add a virtual machine scale set template to it.</span></span> <span data-ttu-id="11f22-175">GitHub veya Azure Web uygulama Galerisi almak isteyip istemediğinizi seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="11f22-175">You can choose whether you want to import it from GitHub or the Azure Web Application Gallery.</span></span> <span data-ttu-id="11f22-176">Bir dağıtım PowerShell komut dosyası ayrıca sizin için oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="11f22-176">A deployment PowerShell script is also generated for you.</span></span> <span data-ttu-id="11f22-177">Daha fazla bilgi için bkz: [kümesinin Visual Studio ile nasıl bir sanal makine ölçek oluşturulacağı](virtual-machine-scale-sets-vs-create.md).</span><span class="sxs-lookup"><span data-stu-id="11f22-177">For more information, see [How to create a virtual machine scale set with Visual Studio](virtual-machine-scale-sets-vs-create.md).</span></span>

## <a name="create-from-the-azure-portal"></a><span data-ttu-id="11f22-178">Azure portalından oluşturmak</span><span class="sxs-lookup"><span data-stu-id="11f22-178">Create from the Azure portal</span></span>

<span data-ttu-id="11f22-179">Azure portal, hızlı bir şekilde bir ölçek kümesi oluşturmak için kolay bir yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="11f22-179">The Azure portal provides a convenient way to quickly create a scale set.</span></span> <span data-ttu-id="11f22-180">Daha fazla bilgi için bkz: [kümesinin nasıl bir sanal makine ölçek oluşturulacağı Azure portalıyla](virtual-machine-scale-sets-portal-create.md).</span><span class="sxs-lookup"><span data-stu-id="11f22-180">For more information, see [How to create a virtual machine scale set with the Azure portal](virtual-machine-scale-sets-portal-create.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="11f22-181">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="11f22-181">Next steps</span></span>

<span data-ttu-id="11f22-182">Daha fazla bilgi edinmek [veri diskleri](virtual-machine-scale-sets-attached-disks.md).</span><span class="sxs-lookup"><span data-stu-id="11f22-182">Learn more about [data disks](virtual-machine-scale-sets-attached-disks.md).</span></span>

<span data-ttu-id="11f22-183">Bilgi edinmek için nasıl [uygulamalarınızı yönetmek](virtual-machine-scale-sets-deploy-app.md).</span><span class="sxs-lookup"><span data-stu-id="11f22-183">Learn how to [manage your apps](virtual-machine-scale-sets-deploy-app.md).</span></span>
