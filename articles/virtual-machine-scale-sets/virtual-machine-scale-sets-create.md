---
title: "aaaCreate bir Azure sanal makine ölçek kümesi | Microsoft Docs"
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
ms.openlocfilehash: 73de25c1dd2424e64655b3accfea848926e72f69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-a-virtual-machine-scale-set"></a><span data-ttu-id="f5760-103">Oluşturma ve bir sanal makine ölçek kümesini dağıtma</span><span class="sxs-lookup"><span data-stu-id="f5760-103">Create and deploy a virtual machine scale set</span></span>
<span data-ttu-id="f5760-104">Sanal makine ölçek kümeleri sizin için toodeploy kolaylaştırır ve aynı sanal makineleri bir küme olarak yönetin.</span><span class="sxs-lookup"><span data-stu-id="f5760-104">Virtual machine scale sets make it easy for you toodeploy and manage identical virtual machines as a set.</span></span> <span data-ttu-id="f5760-105">Ölçek kümeleri ölçekte uygulamalar için yüksek oranda ölçeklenebilir ve özelleştirilebilir bilgi işlem katmanını sağlar ve Windows platform görüntüleri, Linux platform görüntüleri, özel resimler ve uzantıları destekler.</span><span class="sxs-lookup"><span data-stu-id="f5760-105">Scale sets provide a highly scalable and customizable compute layer for hyperscale applications, and they support Windows platform images, Linux platform images, custom images, and extensions.</span></span> <span data-ttu-id="f5760-106">Ölçek kümeleri hakkında daha fazla bilgi için bkz: [sanal makine ölçek kümeleri](virtual-machine-scale-sets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f5760-106">For more information about scale sets, see [Virtual machine scale sets](virtual-machine-scale-sets-overview.md).</span></span>

<span data-ttu-id="f5760-107">Bu öğretici, bir sanal makine ölçek toocreate nasıl ayarlanacağını gösterir. **olmadan** hello Azure portal kullanarak.</span><span class="sxs-lookup"><span data-stu-id="f5760-107">This tutorial shows you how toocreate a virtual machine scale set **without** using hello Azure portal.</span></span> <span data-ttu-id="f5760-108">Nasıl toouse hello Azure portal hakkında daha fazla bilgi için bkz: [nasıl toocreate hello Azure portal ile bir sanal makine ölçek kümesi](virtual-machine-scale-sets-portal-create.md).</span><span class="sxs-lookup"><span data-stu-id="f5760-108">For information about how toouse hello Azure portal, see [How toocreate a virtual machine scale set with hello Azure portal](virtual-machine-scale-sets-portal-create.md).</span></span>

>[!NOTE]
><span data-ttu-id="f5760-109">Azure Resource Manager kaynakları hakkında daha fazla bilgi için bkz: [Azure Resource Manager ve klasik dağıtım](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="f5760-109">For more information about Azure Resource Manager resources, see [Azure Resource Manager vs. classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>

## <a name="sign-in-tooazure"></a><span data-ttu-id="f5760-110">İçinde tooAzure oturum</span><span class="sxs-lookup"><span data-stu-id="f5760-110">Sign in tooAzure</span></span>

<span data-ttu-id="f5760-111">Azure CLI 2.0 veya Azure PowerShell toocreate ölçek kullanıyorsanız, ayarlanırsa, ilk tooyour Abonelikteki toosign gerekir.</span><span class="sxs-lookup"><span data-stu-id="f5760-111">If you're using Azure CLI 2.0 or Azure PowerShell toocreate a scale set, you first need toosign in tooyour subscription.</span></span>

<span data-ttu-id="f5760-112">Ayarlama, tooinstall ve oturum açma tooAzure Azure CLI veya PowerShell ile nasıl görürüm hakkında daha fazla bilgi için [Azure CLI 2.0 ile çalışmaya başlama](/cli/azure/get-started-with-azure-cli.md) veya [Azure PowerShell cmdlet'leri kullanmaya başlama](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f5760-112">For more information about how tooinstall, set up, and sign in tooAzure with Azure CLI or PowerShell, see [Getting Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md) or [Get started with Azure PowerShell cmdlets](/powershell/azure/overview).</span></span>

```azurecli
az login
```

```powershell
Login-AzureRmAccount
```

## <a name="create-a-resource-group"></a><span data-ttu-id="f5760-113">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="f5760-113">Create a resource group</span></span>

<span data-ttu-id="f5760-114">Önce hello sanal makine ölçek kümesi bir kaynak grubu ile ilişkili toocreate gerekir.</span><span class="sxs-lookup"><span data-stu-id="f5760-114">You first need toocreate a resource group that hello virtual machine scale set is associated with.</span></span>

```azurecli
az group create --location westus2 --name MyResourceGroup1
```

```powershell
New-AzureRmResourceGroup -Location westus2 -Name MyResourceGroup1
```

## <a name="create-from-azure-cli"></a><span data-ttu-id="f5760-115">Azure CLI üzerinden oluşturma</span><span class="sxs-lookup"><span data-stu-id="f5760-115">Create from Azure CLI</span></span>

<span data-ttu-id="f5760-116">Azure CLI ile en az çaba ile ayarlanmış bir sanal makine ölçek oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f5760-116">With Azure CLI, you can create a virtual machine scale set with minimal effort.</span></span> <span data-ttu-id="f5760-117">Varsayılan değerleri atlarsanız, bunlar sizin için sağlanır.</span><span class="sxs-lookup"><span data-stu-id="f5760-117">If you omit default values, they are provided for you.</span></span> <span data-ttu-id="f5760-118">Örneğin, herhangi bir sanal ağ bilgi belirtmezseniz, bir sanal ağ sizin için oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="f5760-118">For example, if you don't specify any virtual network information, a virtual network is created for you.</span></span> <span data-ttu-id="f5760-119">Bölümleri aşağıdaki hello atlarsanız, bunlar sizin için oluşturulur:</span><span class="sxs-lookup"><span data-stu-id="f5760-119">If you omit hello following parts, they are created for you:</span></span> 
- <span data-ttu-id="f5760-120">Bir yük dengeleyici</span><span class="sxs-lookup"><span data-stu-id="f5760-120">A load balancer</span></span>
- <span data-ttu-id="f5760-121">Bir sanal ağ</span><span class="sxs-lookup"><span data-stu-id="f5760-121">A virtual network</span></span>
- <span data-ttu-id="f5760-122">Bir ortak IP adresi</span><span class="sxs-lookup"><span data-stu-id="f5760-122">A public IP address</span></span>

<span data-ttu-id="f5760-123">Merhaba sanal makine ölçek kümesi üzerinde toouse istediğiniz sanal makine görüntüsü seçme Merhaba, birkaç seçeneğiniz vardır:</span><span class="sxs-lookup"><span data-stu-id="f5760-123">When choosing hello virtual machine image that you want toouse on hello virtual machine scale set, you have a few choices:</span></span>

- <span data-ttu-id="f5760-124">URN</span><span class="sxs-lookup"><span data-stu-id="f5760-124">URN</span></span>  
<span data-ttu-id="f5760-125">bir kaynak tanıtıcısı Hello:</span><span class="sxs-lookup"><span data-stu-id="f5760-125">hello identifier of a resource:</span></span>  
<span data-ttu-id="f5760-126">**Win2012R2Datacenter**</span><span class="sxs-lookup"><span data-stu-id="f5760-126">**Win2012R2Datacenter**</span></span>

- <span data-ttu-id="f5760-127">URN diğer adı</span><span class="sxs-lookup"><span data-stu-id="f5760-127">URN alias</span></span>  
<span data-ttu-id="f5760-128">kolay adı bir URN Hello:</span><span class="sxs-lookup"><span data-stu-id="f5760-128">hello friendly name of a URN:</span></span>  
<span data-ttu-id="f5760-129">**MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest**</span><span class="sxs-lookup"><span data-stu-id="f5760-129">**MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest**</span></span>

- <span data-ttu-id="f5760-130">Özel kaynak kimliği</span><span class="sxs-lookup"><span data-stu-id="f5760-130">Custom resource id</span></span>  
<span data-ttu-id="f5760-131">Merhaba yolu tooan Azure kaynağı:</span><span class="sxs-lookup"><span data-stu-id="f5760-131">hello path tooan Azure resource:</span></span>  
<span data-ttu-id="f5760-132">**/Subscriptions/Subscription-guid/resourceGroups/MyResourceGroup/providers/Microsoft.COMPUTE/images/MyImage**</span><span class="sxs-lookup"><span data-stu-id="f5760-132">**/subscriptions/subscription-guid/resourceGroups/MyResourceGroup/providers/Microsoft.Compute/images/MyImage**</span></span>

- <span data-ttu-id="f5760-133">Web kaynağı</span><span class="sxs-lookup"><span data-stu-id="f5760-133">Web resource</span></span>  
<span data-ttu-id="f5760-134">Merhaba yolu tooan HTTP URI:</span><span class="sxs-lookup"><span data-stu-id="f5760-134">hello path tooan HTTP URI:</span></span>  
<span data-ttu-id="f5760-135">**http://contoso.BLOB.Core.Windows.NET/vhds/osdiskimage.vhd**</span><span class="sxs-lookup"><span data-stu-id="f5760-135">**http://contoso.blob.core.windows.net/vhds/osdiskimage.vhd**</span></span>

>[!TIP]
><span data-ttu-id="f5760-136">Kullanılabilir görüntülerle listesini almak `az vm image list`.</span><span class="sxs-lookup"><span data-stu-id="f5760-136">You can get a list of available images with `az vm image list`.</span></span>

<span data-ttu-id="f5760-137">toocreate bir sanal makine ölçek kümesi, hello aşağıdakileri belirtin:</span><span class="sxs-lookup"><span data-stu-id="f5760-137">toocreate a virtual machine scale set, you must specify hello following:</span></span>

- <span data-ttu-id="f5760-138">Kaynak grubu</span><span class="sxs-lookup"><span data-stu-id="f5760-138">Resource group</span></span> 
- <span data-ttu-id="f5760-139">Ad</span><span class="sxs-lookup"><span data-stu-id="f5760-139">Name</span></span>
- <span data-ttu-id="f5760-140">İşletim sistemi görüntüsü</span><span class="sxs-lookup"><span data-stu-id="f5760-140">Operating system image</span></span>
- <span data-ttu-id="f5760-141">Kimlik doğrulama bilgileri</span><span class="sxs-lookup"><span data-stu-id="f5760-141">Authentication information</span></span> 
 
<span data-ttu-id="f5760-142">Aşağıdaki örnek hello (Bu adım birkaç dakika sürebilir) temel sanal makine ölçek kümesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f5760-142">hello following example creates a basic virtual machine scale set (this step might take a few minutes).</span></span>

```azurecli
az vmss create --resource-group MyResourceGroup1 --name MyScaleSet --image UbuntuLTS --authentication-type password --admin-username azureuser --admin-password P@ssw0rd!
```

<span data-ttu-id="f5760-143">Merhaba komut bittikten sonra oluşturulan ayarlayın, sanal makine ölçek şimdi sahip olur.</span><span class="sxs-lookup"><span data-stu-id="f5760-143">Once hello command finishes you will now have your virtual machine scale set created.</span></span> <span data-ttu-id="f5760-144">Tooit bağlanabilmesi tooget hello hello sanal makinenin IP adresini gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="f5760-144">You may need tooget hello IP address of hello virtual machine so that you can connect tooit.</span></span> <span data-ttu-id="f5760-145">Komutu aşağıdaki hello ile çok sayıda hello sanal makine (Merhaba IP adresi dahil) hakkında farklı bilgi elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f5760-145">You can get a lot of different information about hello virtual machine (including hello IP address) with hello following command.</span></span> 

```azurecli
az vmss list-instance-connection-info --resource-group MyResourceGroup1 --name MyScaleSet
```

## <a name="create-from-powershell"></a><span data-ttu-id="f5760-146">Powershell'den oluşturma</span><span class="sxs-lookup"><span data-stu-id="f5760-146">Create from PowerShell</span></span>

<span data-ttu-id="f5760-147">Azure CLI'den daha karmaşık toouse powershell'dir.</span><span class="sxs-lookup"><span data-stu-id="f5760-147">PowerShell is more complicated toouse than Azure CLI.</span></span> <span data-ttu-id="f5760-148">Azure CLI ağla ilgili kaynaklar (örneğin, yük Dengeleyiciler, IP adresleri ve sanal ağları) için varsayılan sağlarken, PowerShell desteklemez.</span><span class="sxs-lookup"><span data-stu-id="f5760-148">While Azure CLI provides defaults for networking-related resources (such as load balancers, IP addresses, and virtual networks), PowerShell does not.</span></span> <span data-ttu-id="f5760-149">PowerShell ile bir görüntü başvuran bir biraz daha çok karmaşıktır.</span><span class="sxs-lookup"><span data-stu-id="f5760-149">Referencing an image with PowerShell is a slightly more complicated too.</span></span> <span data-ttu-id="f5760-150">Cmdlet aşağıdaki hello ile görüntüleri alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f5760-150">You can get images with hello following cmdlets:</span></span>

1. <span data-ttu-id="f5760-151">Get-AzureRMVMImagePublisher</span><span class="sxs-lookup"><span data-stu-id="f5760-151">Get-AzureRMVMImagePublisher</span></span>
2. <span data-ttu-id="f5760-152">Get-AzureRMVMImageOffer</span><span class="sxs-lookup"><span data-stu-id="f5760-152">Get-AzureRMVMImageOffer</span></span>
3. <span data-ttu-id="f5760-153">Get-AzureRmVMImageSku</span><span class="sxs-lookup"><span data-stu-id="f5760-153">Get-AzureRmVMImageSku</span></span>

<span data-ttu-id="f5760-154">Merhaba cmdlet'leri iş sırayla yöneltilen.</span><span class="sxs-lookup"><span data-stu-id="f5760-154">hello cmdlets work can be piped in sequence.</span></span> <span data-ttu-id="f5760-155">Merhaba nasıl tooget tüm görüntüleri bir örnek şudur **Batı ABD 2** hello ada sahip bir yayımcı bölgesiyle **microsoft** da.</span><span class="sxs-lookup"><span data-stu-id="f5760-155">Here is an example of how tooget all images for hello **West US 2** region with a publisher that has hello name **microsoft** in it.</span></span>

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

<span data-ttu-id="f5760-156">bir sanal makine ölçek kümesi oluşturmak için hello iş akışı aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="f5760-156">hello workflow for creating a virtual machine scale set is as follows:</span></span>

1. <span data-ttu-id="f5760-157">Merhaba ölçek kümesi hakkında bilgi içeren bir yapılandırma nesnesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f5760-157">Create a config object that holds information about hello scale set.</span></span>
2. <span data-ttu-id="f5760-158">Başvuru hello temel işletim sistemi görüntüsü.</span><span class="sxs-lookup"><span data-stu-id="f5760-158">Reference hello base OS image.</span></span>
3. <span data-ttu-id="f5760-159">Merhaba işletim sistemi ayarlarını yapılandırın: kimlik doğrulaması, VM adı ön ekini ve kullanıcı/geçirin.</span><span class="sxs-lookup"><span data-stu-id="f5760-159">Configure hello operating system settings: authentication, VM name prefix, and user/pass.</span></span>
4. <span data-ttu-id="f5760-160">Ağ yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="f5760-160">Configure networking.</span></span>
5. <span data-ttu-id="f5760-161">Merhaba ölçek kümesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f5760-161">Create hello scale set.</span></span>

<span data-ttu-id="f5760-162">Bu örnek, Windows Server 2016 sahip bir bilgisayar için temel bir iki örnekli ölçek oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f5760-162">This example creates a basic two-instance scale set for a computer that has Windows Server 2016 installed.</span></span>

```powershell
# Resource group name from above
$rg = "MyResourceGroup1"
$location = "WestUS2"

# Create a config object
$vmssConfig = New-AzureRmVmssConfig -Location $location -SkuCapacity 2 -SkuName Standard_A0  -UpgradePolicyMode Automatic

# Reference a virtual machine image from hello gallery
Set-AzureRmVmssStorageProfile $vmssConfig -ImageReferencePublisher MicrosoftWindowsServer -ImageReferenceOffer WindowsServer -ImageReferenceSku 2016-Datacenter -ImageReferenceVersion latest

# Set up information for authenticating with hello virtual machine
Set-AzureRmVmssOsProfile $vmssConfig -AdminUsername azureuser -AdminPassword P@ssw0rd! -ComputerNamePrefix myvmssvm

# Create hello virtual network resources

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

# Attach hello virtual network toohello IP object
Add-AzureRmVmssNetworkInterfaceConfiguration -VirtualMachineScaleSet $vmssConfig -Name "network-config" -Primary $true -IPConfiguration $ipConfig

# Create hello scale set with hello config object (this step might take a few minutes)
New-AzureRmVmss -ResourceGroupName $rg -Name "MyScaleSet1" -VirtualMachineScaleSet $vmssConfig
```

### <a name="using-a-custom-virtual-machine-image"></a><span data-ttu-id="f5760-163">Bir özel sanal makine görüntüsü kullanma</span><span class="sxs-lookup"><span data-stu-id="f5760-163">Using a custom virtual machine image</span></span>
<span data-ttu-id="f5760-164">Bir sanal makine görüntüsü hello Galerisi'nden başvuran yerine kendi özel görüntünüzü kümeden bir ölçek oluşturuyorsanız hello _kümesi AzureRmVmssStorageProfile_ komutu şuna benzeyebilir:</span><span class="sxs-lookup"><span data-stu-id="f5760-164">If you are creating a scale set from your own custom image, instead of referencing a virtual machine image from hello gallery, hello _Set-AzureRmVmssStorageProfile_ command would look like this:</span></span>
```PowerShell
Set-AzureRmVmssStorageProfile -OsDiskCreateOption FromImage -ManagedDisk PremiumLRS -OsDiskCaching "None" -OsDiskOsType Linux -ImageReferenceId (Get-AzureRmImage -ImageName $VMImage -ResourceGroupName $rg).id
```

## <a name="create-from-a-template"></a><span data-ttu-id="f5760-165">Şablondan oluşturma</span><span class="sxs-lookup"><span data-stu-id="f5760-165">Create from a template</span></span>

<span data-ttu-id="f5760-166">Bir Azure Resource Manager şablonu kullanarak bir sanal makine ölçek dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f5760-166">You can deploy a virtual machine scale set by using an Azure Resource Manager template.</span></span> <span data-ttu-id="f5760-167">Kendi şablonunuzu oluşturun ya da bir hello kullan [şablonu deposu](https://azure.microsoft.com/resources/templates/?term=vmss).</span><span class="sxs-lookup"><span data-stu-id="f5760-167">You can create your own template or use one from hello [template repository](https://azure.microsoft.com/resources/templates/?term=vmss).</span></span> <span data-ttu-id="f5760-168">Bu şablonlar dağıtılabilir doğrudan tooyour Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="f5760-168">These templates can be deployed directly tooyour Azure subscription.</span></span>

>[!NOTE]
><span data-ttu-id="f5760-169">toocreate kendi şablonunuzu bir JSON metin dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f5760-169">toocreate your own template, you create a JSON text file.</span></span> <span data-ttu-id="f5760-170">Hakkında genel bilgi için toocreate ve şablonu özelleştirme bkz [Azure Resource Manager şablonları](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="f5760-170">For general information about how toocreate and customize a template, see [Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="f5760-171">Örnek şablon kullanılabilir [github'da](https://github.com/gatneil/mvss/tree/minimum-viable-scale-set).</span><span class="sxs-lookup"><span data-stu-id="f5760-171">A sample template is available [on GitHub](https://github.com/gatneil/mvss/tree/minimum-viable-scale-set).</span></span> <span data-ttu-id="f5760-172">Nasıl bkz: toocreate ve örnek, kullanma hakkında daha fazla bilgi için [en uygun ölçek kümesini](.\virtual-machine-scale-sets-mvss-start.md).</span><span class="sxs-lookup"><span data-stu-id="f5760-172">For more information about how toocreate and use that sample, see [Minimum viable scale set](.\virtual-machine-scale-sets-mvss-start.md).</span></span>

## <a name="create-from-visual-studio"></a><span data-ttu-id="f5760-173">Visual Studio'dan oluşturma</span><span class="sxs-lookup"><span data-stu-id="f5760-173">Create from Visual Studio</span></span>

<span data-ttu-id="f5760-174">Visual Studio ile bir Azure kaynak grubu projesi oluşturun ve şablon tooit bir sanal makine ölçek kümesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f5760-174">With Visual Studio, you can create an Azure resource group project and add a virtual machine scale set template tooit.</span></span> <span data-ttu-id="f5760-175">Tooimport isteyip istemediğinizi seçebilirsiniz, GitHub veya hello Azure Web uygulama Galerisi.</span><span class="sxs-lookup"><span data-stu-id="f5760-175">You can choose whether you want tooimport it from GitHub or hello Azure Web Application Gallery.</span></span> <span data-ttu-id="f5760-176">Bir dağıtım PowerShell komut dosyası ayrıca sizin için oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="f5760-176">A deployment PowerShell script is also generated for you.</span></span> <span data-ttu-id="f5760-177">Daha fazla bilgi için bkz: [nasıl toocreate Visual Studio ile bir sanal makine ölçek kümesi](virtual-machine-scale-sets-vs-create.md).</span><span class="sxs-lookup"><span data-stu-id="f5760-177">For more information, see [How toocreate a virtual machine scale set with Visual Studio](virtual-machine-scale-sets-vs-create.md).</span></span>

## <a name="create-from-hello-azure-portal"></a><span data-ttu-id="f5760-178">Azure portal Hello oluşturma</span><span class="sxs-lookup"><span data-stu-id="f5760-178">Create from hello Azure portal</span></span>

<span data-ttu-id="f5760-179">Hello Azure portal tooquickly ölçek kümesi oluştur kullanışlı bir yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="f5760-179">hello Azure portal provides a convenient way tooquickly create a scale set.</span></span> <span data-ttu-id="f5760-180">Daha fazla bilgi için bkz: [nasıl toocreate hello Azure portal ile bir sanal makine ölçek kümesi](virtual-machine-scale-sets-portal-create.md).</span><span class="sxs-lookup"><span data-stu-id="f5760-180">For more information, see [How toocreate a virtual machine scale set with hello Azure portal](virtual-machine-scale-sets-portal-create.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f5760-181">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f5760-181">Next steps</span></span>

<span data-ttu-id="f5760-182">Daha fazla bilgi edinmek [veri diskleri](virtual-machine-scale-sets-attached-disks.md).</span><span class="sxs-lookup"><span data-stu-id="f5760-182">Learn more about [data disks](virtual-machine-scale-sets-attached-disks.md).</span></span>

<span data-ttu-id="f5760-183">Nasıl çok öğrenin[uygulamalarınızı yönetmek](virtual-machine-scale-sets-deploy-app.md).</span><span class="sxs-lookup"><span data-stu-id="f5760-183">Learn how too[manage your apps](virtual-machine-scale-sets-deploy-app.md).</span></span>
