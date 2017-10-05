---
title: "DNS geriye doğru için Azure services | Microsoft Docs"
description: "Geriye doğru DNS araması Azure içinde barındırılan hizmetler için yapılandırma hakkında bilgi edinin"
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/29/2017
ms.author: jonatul
ms.openlocfilehash: 63701e1ce0c1c6dcf2ce02ebce272b8280395e7f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-reverse-dns-for-services-hosted-in-azure"></a><span data-ttu-id="1322b-103">Azure üzerinde barındırılan hizmetleri için ters DNS yapılandırma</span><span class="sxs-lookup"><span data-stu-id="1322b-103">Configure reverse DNS for services hosted in Azure</span></span>

<span data-ttu-id="1322b-104">Bu makalede, Azure üzerinde barındırılan hizmetleri için ters DNS araması yapılandırma açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="1322b-104">This article explains how to configure reverse DNS lookups for services hosted in Azure.</span></span>

<span data-ttu-id="1322b-105">Azure Hizmetleri Azure tarafından atanan ve Microsoft tarafından ait IP adresleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="1322b-105">Services in Azure use IP addresses assigned by Azure and owned by Microsoft.</span></span> <span data-ttu-id="1322b-106">Geriye doğru DNS kayıtlarının (PTR kayıtları) karşılık gelen Microsoft ait geriye doğru DNS arama bölgeleri oluşturulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1322b-106">These reverse DNS records (PTR records) must be created in the corresponding Microsoft-owned reverse DNS lookup zones.</span></span> <span data-ttu-id="1322b-107">Bu makalede bunun nasıl yapılacağı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="1322b-107">This article explains how to do this.</span></span>

<span data-ttu-id="1322b-108">Bu senaryo yeteneği ile karıştırılmamalıdır [Azure DNS'de, atanan IP aralıkları için geriye doğru DNS arama bölgeleri barındıran](dns-reverse-dns-hosting.md).</span><span class="sxs-lookup"><span data-stu-id="1322b-108">This scenario should not be confused with the ability to [host the reverse DNS lookup zones for your assigned IP ranges in Azure DNS](dns-reverse-dns-hosting.md).</span></span> <span data-ttu-id="1322b-109">Bu durumda, geriye doğru arama bölgesi tarafından temsil edilen IP aralıkları, kuruluşunuz için genellikle ISS'niz tarafından atanmış olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1322b-109">In this case, the IP ranges represented by the reverse lookup zone must be assigned to your organization, typically by your ISP.</span></span>

<span data-ttu-id="1322b-110">Bu makalede okumadan önce bu bilgi sahibi olmanız [geriye doğru DNS ve Azure desteği'na genel bakış](dns-reverse-dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1322b-110">Before reading this article, you should be familiar with this [Overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md).</span></span>

<span data-ttu-id="1322b-111">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="1322b-111">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>
* <span data-ttu-id="1322b-112">Resource Manager dağıtım modelinde, işlem kaynakları (örneğin, sanal makineler, sanal makine ölçek kümeleri veya Service Fabric kümeleri) Publicıpaddress kaynak sunulur.</span><span class="sxs-lookup"><span data-stu-id="1322b-112">In the Resource Manager deployment model, compute resources (such as virtual machines, virtual machine scale sets, or Service Fabric clusters) are exposed via a PublicIpAddress resource.</span></span> <span data-ttu-id="1322b-113">Geriye doğru DNS araması Publicıpaddress 'ReverseFqdn' özelliği kullanılarak yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="1322b-113">Reverse DNS lookups are configured using the 'ReverseFqdn' property of the PublicIpAddress.</span></span>
* <span data-ttu-id="1322b-114">Klasik dağıtım modeli, bulut hizmetlerini kullanarak işlem kaynaklarını sunulur.</span><span class="sxs-lookup"><span data-stu-id="1322b-114">In the Classic deployment model, compute resources are exposed using Cloud Services.</span></span> <span data-ttu-id="1322b-115">Geriye doğru DNS araması bulut hizmetinin 'ReverseDnsFqdn' özelliği kullanılarak yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="1322b-115">Reverse DNS lookups are configured using the 'ReverseDnsFqdn' property of the Cloud Service.</span></span>

<span data-ttu-id="1322b-116">Geriye doğru DNS Azure App Service için şu anda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="1322b-116">Reverse DNS is not currently supported for the Azure App Service.</span></span>

## <a name="validation-of-reverse-dns-records"></a><span data-ttu-id="1322b-117">Geriye doğru DNS kayıtlarını doğrulama</span><span class="sxs-lookup"><span data-stu-id="1322b-117">Validation of reverse DNS records</span></span>

<span data-ttu-id="1322b-118">Bir üçüncü taraf kendi Azure hizmeti eşleme, DNS etki alanı için geriye doğru DNS kayıtları oluşturmak mümkün olmaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1322b-118">A third party should not be able to create reverse DNS records for their Azure service mapping to your DNS domains.</span></span> <span data-ttu-id="1322b-119">Bunu önlemek için Azure yalnızca geriye doğru DNS kaydında belirtilen etki alanı adı ile aynı olduğu geriye doğru DNS kaydı oluşturulmasına izin verir veya DNS adı veya IP adresini bir Publicıpaddress veya Bulut hizmeti aynı Azure abonelik giderir.</span><span class="sxs-lookup"><span data-stu-id="1322b-119">To prevent this, Azure only allows the creation of a reverse DNS record where domain name specified in the reverse DNS record is the same as, or resolves to, the DNS name or IP address of a PublicIpAddress or Cloud Service in the same Azure subscription.</span></span>

<span data-ttu-id="1322b-120">Bu doğrulama yalnızca geriye doğru DNS kaydı ayarlayın veya değiştirilirken gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="1322b-120">This validation is only performed when the reverse DNS record is set or modified.</span></span> <span data-ttu-id="1322b-121">Düzenli aralıklarla yeniden doğrulama yapılmaz.</span><span class="sxs-lookup"><span data-stu-id="1322b-121">Periodic re-validation is not performed.</span></span>

<span data-ttu-id="1322b-122">Örneğin: Publicıpaddress kaynak IP adresi 23.96.52.53 ve DNS adı contosoapp1.northus.cloudapp.azure.com sahip olduğunu varsayın.</span><span class="sxs-lookup"><span data-stu-id="1322b-122">For example: suppose the PublicIpAddress resource has the DNS name contosoapp1.northus.cloudapp.azure.com and IP address 23.96.52.53.</span></span> <span data-ttu-id="1322b-123">Publicıpaddress ReverseFqdn olarak belirtilebilir:</span><span class="sxs-lookup"><span data-stu-id="1322b-123">The ReverseFqdn for the PublicIpAddress can be specified as:</span></span>
* <span data-ttu-id="1322b-124">Publicıpaddress için DNS adını contosoapp1.northus.cloudapp.azure.com</span><span class="sxs-lookup"><span data-stu-id="1322b-124">The DNS name for the PublicIpAddress, contosoapp1.northus.cloudapp.azure.com</span></span>
* <span data-ttu-id="1322b-125">Aynı abonelikte contosoapp2.westus.cloudapp.azure.com gibi farklı bir Publicıpaddress için DNS adı</span><span class="sxs-lookup"><span data-stu-id="1322b-125">The DNS name for a different PublicIpAddress in the same subscription, such as contosoapp2.westus.cloudapp.azure.com</span></span>
* <span data-ttu-id="1322b-126">Bu ad olduğu sürece bir gösterim DNS, app1.contoso.com gibi ad *ilk* contosoapp1.northus.cloudapp.azure.com veya farklı bir Publicıpaddress aynı abonelik için bir CNAME olarak yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="1322b-126">A vanity DNS name, such as app1.contoso.com, so long as this name is *first* configured as a CNAME to contosoapp1.northus.cloudapp.azure.com, or to a different PublicIpAddress in the same subscription.</span></span>
* <span data-ttu-id="1322b-127">Bu ad olduğu sürece bir gösterim DNS, app1.contoso.com gibi ad *ilk* 23.96.52.53 IP adresine ya da aynı Abonelikteki farklı bir Publicıpaddress IP adresi için bir A kaydı olarak yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="1322b-127">A vanity DNS name, such as app1.contoso.com, so long as this name is *first* configured as an A record to the IP address 23.96.52.53, or to the IP address of a different PublicIpAddress in the same subscription.</span></span>

<span data-ttu-id="1322b-128">Aynı kısıtlamalar DNS bulut Hizmetleri için ters geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="1322b-128">The same constraints apply to reverse DNS for Cloud Services.</span></span>


## <a name="reverse-dns-for-publicipaddress-resources"></a><span data-ttu-id="1322b-129">Geriye doğru DNS Publicıpaddress kaynaklar için</span><span class="sxs-lookup"><span data-stu-id="1322b-129">Reverse DNS for PublicIpAddress resources</span></span>

<span data-ttu-id="1322b-130">Bu bölümde Azure PowerShell, Azure CLI 1.0 veya Azure CLI 2.0 kullanarak Resource Manager dağıtım modelinde Publicıpaddress kaynaklar için geriye doğru DNS yapılandırma hakkında ayrıntılı yönergeler sağlar.</span><span class="sxs-lookup"><span data-stu-id="1322b-130">This section provides detailed instructions for how to configure reverse DNS for PublicIpAddress resources in the Resource Manager deployment model, using either Azure PowerShell, Azure CLI 1.0, or Azure CLI 2.0.</span></span> <span data-ttu-id="1322b-131">Geriye doğru DNS Publicıpaddress kaynakları için yapılandırma, Azure portalı üzerinden şu anda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="1322b-131">Configuring reverse DNS for PublicIpAddress resources is not currently supported via the Azure portal.</span></span>

<span data-ttu-id="1322b-132">Azure şu anda destekler DNS yalnızca IPv4 Publicıpaddress kaynaklar için ters çevrilir.</span><span class="sxs-lookup"><span data-stu-id="1322b-132">Azure currently supports reverse DNS only for IPv4 PublicIpAddress resources.</span></span> <span data-ttu-id="1322b-133">IPv6 için desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="1322b-133">It is not supported for IPv6.</span></span>

### <a name="add-reverse-dns-to-an-existing-publicipaddresses"></a><span data-ttu-id="1322b-134">Varolan bir Publicıpaddresses için geriye doğru DNS ekleyin</span><span class="sxs-lookup"><span data-stu-id="1322b-134">Add reverse DNS to an existing PublicIpAddresses</span></span>

#### <a name="powershell"></a><span data-ttu-id="1322b-135">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1322b-135">PowerShell</span></span>

<span data-ttu-id="1322b-136">Geriye doğru DNS için var olan bir Publicıpaddress eklemek için:</span><span class="sxs-lookup"><span data-stu-id="1322b-136">To add reverse DNS to an existing PublicIpAddress:</span></span>

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings.ReverseFqdn = "contosoapp1.westus.cloudapp.azure.com."
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

<span data-ttu-id="1322b-137">Geriye doğru DNS zaten bir DNS adı yok var olan bir Publicıpaddress eklemek için de bir DNS adı belirtmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="1322b-137">To add reverse DNS to an existing PublicIpAddress that doesn't already have a DNS name, you must also specify a DNS name:</span></span>

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings = New-Object -TypeName "Microsoft.Azure.Commands.Network.Models.PSPublicIpAddressDnsSettings"
$pip.DnsSettings.DomainNameLabel = "contosoapp1"
$pip.DnsSettings.ReverseFqdn = "contosoapp1.westus.cloudapp.azure.com."
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

#### <a name="azure-cli-10"></a><span data-ttu-id="1322b-138">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="1322b-138">Azure CLI 1.0</span></span>

<span data-ttu-id="1322b-139">Geriye doğru DNS için var olan bir Publicıpaddress eklemek için:</span><span class="sxs-lookup"><span data-stu-id="1322b-139">To add reverse DNS to an existing PublicIpAddress:</span></span>

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup -f contosoapp1.westus.cloudapp.azure.com.
```

<span data-ttu-id="1322b-140">Geriye doğru DNS zaten bir DNS adı yok var olan bir Publicıpaddress eklemek için de bir DNS adı belirtmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="1322b-140">To add reverse DNS to an existing PublicIpAddress that doesn't already have a DNS name, you must also specify a DNS name:</span></span>

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup -d contosoapp1 -f contosoapp1.westus.cloudapp.azure.com.
```

#### <a name="azure-cli-20"></a><span data-ttu-id="1322b-141">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="1322b-141">Azure CLI 2.0</span></span>

<span data-ttu-id="1322b-142">Geriye doğru DNS için var olan bir Publicıpaddress eklemek için:</span><span class="sxs-lookup"><span data-stu-id="1322b-142">To add reverse DNS to an existing PublicIpAddress:</span></span>

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn contosoapp1.westus.cloudapp.azure.com.
```

<span data-ttu-id="1322b-143">Geriye doğru DNS zaten bir DNS adı yok var olan bir Publicıpaddress eklemek için de bir DNS adı belirtmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="1322b-143">To add reverse DNS to an existing PublicIpAddress that doesn't already have a DNS name, you must also specify a DNS name:</span></span>

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn contosoapp1.westus.cloudapp.azure.com --dns-name contosoapp1
```

### <a name="create-a-public-ip-address-with-reverse-dns"></a><span data-ttu-id="1322b-144">Geriye doğru DNS ile bir ortak IP adresi oluştur</span><span class="sxs-lookup"><span data-stu-id="1322b-144">Create a Public IP Address with reverse DNS</span></span>

<span data-ttu-id="1322b-145">Ters DNS özelliği zaten belirtilen yeni Publicıpaddress oluşturmak için:</span><span class="sxs-lookup"><span data-stu-id="1322b-145">To create a new PublicIpAddress with the reverse DNS property already specified:</span></span>

#### <a name="powershell"></a><span data-ttu-id="1322b-146">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1322b-146">PowerShell</span></span>

```powershell
New-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup" -Location "WestUS" -AllocationMethod Dynamic -DomainNameLabel "contosoapp2" -ReverseFqdn "contosoapp2.westus.cloudapp.azure.com."
```

#### <a name="azure-cli-10"></a><span data-ttu-id="1322b-147">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="1322b-147">Azure CLI 1.0</span></span>

```azurecli
azure network public-ip create -n PublicIp -g MyResourceGroup -l westus -d contosoapp3 -f contosoapp3.westus.cloudapp.azure.com.
```

#### <a name="azure-cli-20"></a><span data-ttu-id="1322b-148">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="1322b-148">Azure CLI 2.0</span></span>

```azurecli
az network public-ip create --name PublicIp --resource-group MyResourceGroup --location westcentralus --dns-name contosoapp1 --reverse-fqdn contosoapp1.westcentralus.cloudapp.azure.com
```

### <a name="view-reverse-dns-for-an-existing-publicipaddress"></a><span data-ttu-id="1322b-149">Varolan bir Publicıpaddress için ters DNS görünümü</span><span class="sxs-lookup"><span data-stu-id="1322b-149">View reverse DNS for an existing PublicIpAddress</span></span>

<span data-ttu-id="1322b-150">Varolan bir Publicıpaddress için yapılandırılmış bir değeri görüntülemek için:</span><span class="sxs-lookup"><span data-stu-id="1322b-150">To view the configured value for an existing PublicIpAddress:</span></span>

#### <a name="powershell"></a><span data-ttu-id="1322b-151">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1322b-151">PowerShell</span></span>

```powershell
Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
```

#### <a name="azure-cli-10"></a><span data-ttu-id="1322b-152">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="1322b-152">Azure CLI 1.0</span></span>

```azurecli
azure network public-ip show -n PublicIp -g MyResourceGroup
```

#### <a name="azure-cli-20"></a><span data-ttu-id="1322b-153">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="1322b-153">Azure CLI 2.0</span></span>

```azurecli
az network public-ip show --name PublicIp --resource-group MyResourceGroup
```

### <a name="remove-reverse-dns-from-existing-public-ip-addresses"></a><span data-ttu-id="1322b-154">Mevcut ortak IP adreslerinden geriye doğru DNS Kaldır</span><span class="sxs-lookup"><span data-stu-id="1322b-154">Remove reverse DNS from existing Public IP Addresses</span></span>

<span data-ttu-id="1322b-155">Varolan bir Publicıpaddress ters DNS özelliği kaldırmak için:</span><span class="sxs-lookup"><span data-stu-id="1322b-155">To remove a reverse DNS property from an existing PublicIpAddress:</span></span>

#### <a name="powershell"></a><span data-ttu-id="1322b-156">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1322b-156">PowerShell</span></span>

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings.ReverseFqdn = ""
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

#### <a name="azure-cli-10"></a><span data-ttu-id="1322b-157">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="1322b-157">Azure CLI 1.0</span></span>

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup –f ""
```

#### <a name="azure-cli-20"></a><span data-ttu-id="1322b-158">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="1322b-158">Azure CLI 2.0</span></span>

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn ""
```


## <a name="configure-reverse-dns-for-cloud-services"></a><span data-ttu-id="1322b-159">Bulut Hizmetleri için ters DNS yapılandırma</span><span class="sxs-lookup"><span data-stu-id="1322b-159">Configure reverse DNS for Cloud Services</span></span>

<span data-ttu-id="1322b-160">Bu bölümde Azure PowerShell kullanarak Klasik dağıtım modelinde bulut Hizmetleri için ters DNS yapılandırma hakkında ayrıntılı yönergeler sağlar.</span><span class="sxs-lookup"><span data-stu-id="1322b-160">This section provides detailed instructions for how to configure reverse DNS for Cloud Services in the Classic deployment model, using Azure PowerShell.</span></span> <span data-ttu-id="1322b-161">Bulut Hizmetleri için ters DNS yapılandırma Azure portalı Azure CLI 1.0 veya Azure CLI 2.0 desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="1322b-161">Configuring reverse DNS for Cloud Services is not supported via the Azure portal, Azure CLI 1.0, or Azure CLI 2.0.</span></span>

### <a name="add-reverse-dns-to-existing-cloud-services"></a><span data-ttu-id="1322b-162">Mevcut bulut Hizmetleri için ters DNS ekleme</span><span class="sxs-lookup"><span data-stu-id="1322b-162">Add reverse DNS to existing Cloud Services</span></span>

<span data-ttu-id="1322b-163">Geriye doğru DNS kaydı var olan bir bulut hizmetine eklemek için:</span><span class="sxs-lookup"><span data-stu-id="1322b-163">To add a reverse DNS record to an existing Cloud Service:</span></span>

```powershell
Set-AzureService –ServiceName "contosoapp1" –Description "App1 with Reverse DNS" –ReverseDnsFqdn "contosoapp1.cloudapp.net."
```

### <a name="create-a-cloud-service-with-reverse-dns"></a><span data-ttu-id="1322b-164">Geriye doğru DNS ile bir bulut hizmeti oluştur</span><span class="sxs-lookup"><span data-stu-id="1322b-164">Create a Cloud Service with reverse DNS</span></span>

<span data-ttu-id="1322b-165">Ters DNS özelliği zaten belirtilen yeni bir bulut hizmeti oluşturmak için:</span><span class="sxs-lookup"><span data-stu-id="1322b-165">To create a new Cloud Service with the reverse DNS property already specified:</span></span>

```powershell
New-AzureService –ServiceName "contosoapp1" –Location "West US" –Description "App1 with Reverse DNS" –ReverseDnsFqdn "contosoapp1.cloudapp.net."
```

### <a name="view-reverse-dns-for-existing-cloud-services"></a><span data-ttu-id="1322b-166">Mevcut bulut Hizmetleri için ters DNS görünümü</span><span class="sxs-lookup"><span data-stu-id="1322b-166">View reverse DNS for existing Cloud Services</span></span>

<span data-ttu-id="1322b-167">Var olan bir bulut hizmeti için ters DNS özelliği görüntülemek için:</span><span class="sxs-lookup"><span data-stu-id="1322b-167">To view the reverse DNS property for an existing Cloud Service:</span></span>

```powershell
Get-AzureService "contosoapp1"
```

### <a name="remove-reverse-dns-from-existing-cloud-services"></a><span data-ttu-id="1322b-168">Mevcut bulut hizmetlerinden geriye doğru DNS Kaldır</span><span class="sxs-lookup"><span data-stu-id="1322b-168">Remove reverse DNS from existing Cloud Services</span></span>

<span data-ttu-id="1322b-169">Var olan bir bulut hizmetinden geriye doğru DNS özelliğini kaldırmak için:</span><span class="sxs-lookup"><span data-stu-id="1322b-169">To remove a reverse DNS property from an existing Cloud Service:</span></span>

```powershell
Set-AzureService –ServiceName "contosoapp1" –Description "App1 with Reverse DNS" –ReverseDnsFqdn ""
```

## <a name="faq"></a><span data-ttu-id="1322b-170">SSS</span><span class="sxs-lookup"><span data-stu-id="1322b-170">FAQ</span></span>

### <a name="how-much-do-reverse-dns-records-cost"></a><span data-ttu-id="1322b-171">DNS kayıtları maliyeti ne kadar ters?</span><span class="sxs-lookup"><span data-stu-id="1322b-171">How much do reverse DNS records cost?</span></span>

<span data-ttu-id="1322b-172">Bunlar boş!</span><span class="sxs-lookup"><span data-stu-id="1322b-172">They're free!</span></span>  <span data-ttu-id="1322b-173">Geriye doğru DNS kayıtlarını veya sorguları için ek bir maliyet yoktur.</span><span class="sxs-lookup"><span data-stu-id="1322b-173">There is no additional cost for reverse DNS records or queries.</span></span>

### <a name="will-my-reverse-dns-records-resolve-from-the-internet"></a><span data-ttu-id="1322b-174">Geriye doğru DNS kayıtlarımı internet'ten çözer?</span><span class="sxs-lookup"><span data-stu-id="1322b-174">Will my reverse DNS records resolve from the internet?</span></span>

<span data-ttu-id="1322b-175">Evet.</span><span class="sxs-lookup"><span data-stu-id="1322b-175">Yes.</span></span> <span data-ttu-id="1322b-176">Azure hizmetiniz için ters DNS özelliği ayarladıktan sonra Azure tüm geriye doğru DNS kaydı tüm Internet kullanıcıları için çözümlendiğinden emin olmak için gereken DNS bölgeleri ve DNS temsilcilerine yönetir.</span><span class="sxs-lookup"><span data-stu-id="1322b-176">Once you set the reverse DNS property for your Azure service, Azure manages all the DNS delegations and DNS zones required to ensure that reverse DNS record resolves for all Internet users.</span></span>

### <a name="are-default-reverse-dns-records-created-for-my-azure-services"></a><span data-ttu-id="1322b-177">Varsayılan geriye doğru DNS kayıtları için Azure Hizmetlerim oluşturulur?</span><span class="sxs-lookup"><span data-stu-id="1322b-177">Are default reverse DNS records created for my Azure services?</span></span>

<span data-ttu-id="1322b-178">Hayır.</span><span class="sxs-lookup"><span data-stu-id="1322b-178">No.</span></span> <span data-ttu-id="1322b-179">Geriye doğru DNS, bir katılımı özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="1322b-179">Reverse DNS is an opt-in feature.</span></span> <span data-ttu-id="1322b-180">Bunları yapılandırmamaya seçerseniz varsayılan geriye doğru DNS kaydı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="1322b-180">No default reverse DNS records are created if you choose not to configure them.</span></span>

### <a name="what-is-the-format-for-the-fully-qualified-domain-name-fqdn"></a><span data-ttu-id="1322b-181">Tam etki alanı adı (FQDN) biçiminde nedir?</span><span class="sxs-lookup"><span data-stu-id="1322b-181">What is the format for the fully-qualified domain name (FQDN)?</span></span>

<span data-ttu-id="1322b-182">FQDN'ler ileriye doğru sırada belirtilir ve bir nokta (örneğin, "app1.contoso.com.") ile bitmelidir.</span><span class="sxs-lookup"><span data-stu-id="1322b-182">FQDNs are specified in forward order, and must be terminated by a dot (for example, "app1.contoso.com.").</span></span>

### <a name="what-happens-if-the-validation-check-for-the-reverse-dns-ive-specified-fails"></a><span data-ttu-id="1322b-183">Başarısız geriye doğru DNS için doğrulama denetimi ı belirttiğiniz ne olur?</span><span class="sxs-lookup"><span data-stu-id="1322b-183">What happens if the validation check for the reverse DNS I've specified fails?</span></span>

<span data-ttu-id="1322b-184">Geriye doğru DNS doğrulama denetimi başarısız olduğunda, geriye doğru DNS kaydını yapılandırmak için işlem başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="1322b-184">Where the reverse DNS validation check fails, the operation to configure the reverse DNS record fails.</span></span> <span data-ttu-id="1322b-185">Geriye doğru DNS değeri gerektiği gibi düzeltin ve yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="1322b-185">Correct the reverse DNS value as required, and retry.</span></span>

### <a name="can-i-configure-reverse-dns-for-azure-app-service"></a><span data-ttu-id="1322b-186">Azure App Service için ters DNS yapılandırabilir miyim?</span><span class="sxs-lookup"><span data-stu-id="1322b-186">Can I configure reverse DNS for Azure App Service?</span></span>

<span data-ttu-id="1322b-187">Hayır.</span><span class="sxs-lookup"><span data-stu-id="1322b-187">No.</span></span> <span data-ttu-id="1322b-188">Geriye doğru DNS Azure App Service için desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="1322b-188">Reverse DNS is not supported for the Azure App Service.</span></span>

### <a name="can-i-configure-multiple-reverse-dns-records-for-my-azure-service"></a><span data-ttu-id="1322b-189">Birden çok geriye doğru DNS kaydı için Azure Hizmetim yapılandırabilir miyim?</span><span class="sxs-lookup"><span data-stu-id="1322b-189">Can I configure multiple reverse DNS records for my Azure service?</span></span>

<span data-ttu-id="1322b-190">Hayır.</span><span class="sxs-lookup"><span data-stu-id="1322b-190">No.</span></span> <span data-ttu-id="1322b-191">Azure, her Azure bulut hizmeti veya Publicıpaddress için tek bir geriye doğru DNS kaydını destekler.</span><span class="sxs-lookup"><span data-stu-id="1322b-191">Azure supports a single reverse DNS record for each Azure Cloud Service or PublicIpAddress.</span></span>

### <a name="can-i-configure-reverse-dns-for-ipv6-publicipaddress-resources"></a><span data-ttu-id="1322b-192">IPv6 Publicıpaddress kaynaklar için ters DNS yapılandırabilir miyim?</span><span class="sxs-lookup"><span data-stu-id="1322b-192">Can I configure reverse DNS for IPv6 PublicIpAddress resources?</span></span>

<span data-ttu-id="1322b-193">Hayır.</span><span class="sxs-lookup"><span data-stu-id="1322b-193">No.</span></span> <span data-ttu-id="1322b-194">Azure şu anda destekler DNS yalnızca IPv4 Publicıpaddress kaynaklar ve bulut Hizmetleri için ters çevrilir.</span><span class="sxs-lookup"><span data-stu-id="1322b-194">Azure currently supports reverse DNS only for IPv4 PublicIpAddress resources and Cloud Services.</span></span>

### <a name="can-i-send-emails-to-external-domains-from-my-azure-compute-services"></a><span data-ttu-id="1322b-195">Azure işlem Hizmetlerim e-postaları dış etki alanlarına gönderebilirim?</span><span class="sxs-lookup"><span data-stu-id="1322b-195">Can I send emails to external domains from my Azure Compute services?</span></span>

<span data-ttu-id="1322b-196">Hayır.</span><span class="sxs-lookup"><span data-stu-id="1322b-196">No.</span></span> [<span data-ttu-id="1322b-197">Azure işlem Hizmetleri dış etki alanlarına gönderen e-postaları desteklemez</span><span class="sxs-lookup"><span data-stu-id="1322b-197">Azure Compute services do not support sending emails to external domains</span></span>](https://blogs.msdn.microsoft.com/mast/2016/04/04/sending-e-mail-from-azure-compute-resource-to-external-domains/)

## <a name="next-steps"></a><span data-ttu-id="1322b-198">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1322b-198">Next steps</span></span>

<span data-ttu-id="1322b-199">Geriye doğru DNS hakkında daha fazla bilgi için bkz: [wikipedia'da ters DNS araması](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span><span class="sxs-lookup"><span data-stu-id="1322b-199">For more information on reverse DNS, see [reverse DNS lookup on Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span></span>
<br>
<span data-ttu-id="1322b-200">Bilgi edinmek için nasıl [ISS atanan IP aralığınızı Azure DNS geriye doğru arama bölgesini barındırmak](dns-reverse-dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="1322b-200">Learn how to [host the reverse lookup zone for your ISP-assigned IP range in Azure DNS](dns-reverse-dns-for-azure-services.md).</span></span>

