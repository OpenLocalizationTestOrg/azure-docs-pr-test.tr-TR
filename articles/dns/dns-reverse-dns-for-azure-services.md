---
title: "Azure Hizmetleri için DNS aaaReverse | Microsoft Docs"
description: "Nasıl tooconfigure ters DNS araması Azure içinde barındırılan hizmetler için bilgi edinin"
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
ms.openlocfilehash: c6fe1d80232f124be86dd7fc57abc20699be7eba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-reverse-dns-for-services-hosted-in-azure"></a><span data-ttu-id="d9e8e-103">Azure üzerinde barındırılan hizmetleri için ters DNS yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d9e8e-103">Configure reverse DNS for services hosted in Azure</span></span>

<span data-ttu-id="d9e8e-104">Bu makalede nasıl tooconfigure ters DNS araması Azure içinde barındırılan hizmetler için açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="d9e8e-104">This article explains how tooconfigure reverse DNS lookups for services hosted in Azure.</span></span>

<span data-ttu-id="d9e8e-105">Azure Hizmetleri Azure tarafından atanan ve Microsoft tarafından ait IP adresleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="d9e8e-105">Services in Azure use IP addresses assigned by Azure and owned by Microsoft.</span></span> <span data-ttu-id="d9e8e-106">Geriye doğru DNS kayıtlarının (PTR kayıtları) hello karşılık gelen Microsoft ait geriye doğru DNS araması bölgelerinde oluşturulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d9e8e-106">These reverse DNS records (PTR records) must be created in hello corresponding Microsoft-owned reverse DNS lookup zones.</span></span> <span data-ttu-id="d9e8e-107">Bu makalede açıklanır nasıl toodo bu.</span><span class="sxs-lookup"><span data-stu-id="d9e8e-107">This article explains how toodo this.</span></span>

<span data-ttu-id="d9e8e-108">Bu senaryo hello yeteneği çok karıştırılmamalıdır[hello geriye doğru DNS arama bölgeleri Azure DNS'de, atanan IP aralıkları için ana bilgisayar](dns-reverse-dns-hosting.md).</span><span class="sxs-lookup"><span data-stu-id="d9e8e-108">This scenario should not be confused with hello ability too[host hello reverse DNS lookup zones for your assigned IP ranges in Azure DNS](dns-reverse-dns-hosting.md).</span></span> <span data-ttu-id="d9e8e-109">Bu durumda, hello geriye doğru arama bölgesi tarafından temsil edilen hello IP aralıkları tooyour kuruluş, genellikle ISS'niz tarafından atanmış olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d9e8e-109">In this case, hello IP ranges represented by hello reverse lookup zone must be assigned tooyour organization, typically by your ISP.</span></span>

<span data-ttu-id="d9e8e-110">Bu makalede okumadan önce bu bilgi sahibi olmanız [geriye doğru DNS ve Azure desteği'na genel bakış](dns-reverse-dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d9e8e-110">Before reading this article, you should be familiar with this [Overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md).</span></span>

<span data-ttu-id="d9e8e-111">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="d9e8e-111">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>
* <span data-ttu-id="d9e8e-112">Merhaba Resource Manager dağıtım modelinde, işlem kaynakları (örneğin, sanal makineler, sanal makine ölçek kümeleri veya Service Fabric kümeleri) Publicıpaddress kaynak sunulur.</span><span class="sxs-lookup"><span data-stu-id="d9e8e-112">In hello Resource Manager deployment model, compute resources (such as virtual machines, virtual machine scale sets, or Service Fabric clusters) are exposed via a PublicIpAddress resource.</span></span> <span data-ttu-id="d9e8e-113">Geriye doğru DNS araması hello Publicıpaddress hello 'ReverseFqdn' özelliği kullanılarak yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="d9e8e-113">Reverse DNS lookups are configured using hello 'ReverseFqdn' property of hello PublicIpAddress.</span></span>
* <span data-ttu-id="d9e8e-114">Merhaba Klasik dağıtım modelinde, bulut hizmetlerini kullanarak işlem kaynaklarını sunulur.</span><span class="sxs-lookup"><span data-stu-id="d9e8e-114">In hello Classic deployment model, compute resources are exposed using Cloud Services.</span></span> <span data-ttu-id="d9e8e-115">Geriye doğru DNS araması hello bulut hizmeti hello 'ReverseDnsFqdn' özelliği kullanılarak yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="d9e8e-115">Reverse DNS lookups are configured using hello 'ReverseDnsFqdn' property of hello Cloud Service.</span></span>

<span data-ttu-id="d9e8e-116">Geriye doğru DNS hello Azure uygulama hizmeti şu anda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="d9e8e-116">Reverse DNS is not currently supported for hello Azure App Service.</span></span>

## <a name="validation-of-reverse-dns-records"></a><span data-ttu-id="d9e8e-117">Geriye doğru DNS kayıtlarını doğrulama</span><span class="sxs-lookup"><span data-stu-id="d9e8e-117">Validation of reverse DNS records</span></span>

<span data-ttu-id="d9e8e-118">Bir üçüncü taraf mümkün toocreate geriye doğru DNS kayıtlarını Azure hizmeti eşleme tooyour DNS etki alanları için olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="d9e8e-118">A third party should not be able toocreate reverse DNS records for their Azure service mapping tooyour DNS domains.</span></span> <span data-ttu-id="d9e8e-119">tooprevent Bu, Azure yalnızca aynı hello veya DNS adı veya IP adresini Publicıpaddress veya Bulut hello için çözümler hizmet hello aynı hello geriye doğru DNS kaydında belirtilen etki alanı adı olduğu geriye doğru DNS kaydı hello oluşturulmasını sağlayan Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="d9e8e-119">tooprevent this, Azure only allows hello creation of a reverse DNS record where domain name specified in hello reverse DNS record is hello same as, or resolves to, hello DNS name or IP address of a PublicIpAddress or Cloud Service in hello same Azure subscription.</span></span>

<span data-ttu-id="d9e8e-120">Bu doğrulama Hello geriye doğru DNS kaydı kümesi değiştirildiğinde veya yalnızca gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="d9e8e-120">This validation is only performed when hello reverse DNS record is set or modified.</span></span> <span data-ttu-id="d9e8e-121">Düzenli aralıklarla yeniden doğrulama yapılmaz.</span><span class="sxs-lookup"><span data-stu-id="d9e8e-121">Periodic re-validation is not performed.</span></span>

<span data-ttu-id="d9e8e-122">Örneğin: Merhaba Publicıpaddress kaynak hello DNS adı contosoapp1.northus.cloudapp.azure.com ve IP adresi 23.96.52.53 sahip olduğunu varsayın.</span><span class="sxs-lookup"><span data-stu-id="d9e8e-122">For example: suppose hello PublicIpAddress resource has hello DNS name contosoapp1.northus.cloudapp.azure.com and IP address 23.96.52.53.</span></span> <span data-ttu-id="d9e8e-123">Merhaba ReverseFqdn Publicıpaddress olarak belirtilen hello:</span><span class="sxs-lookup"><span data-stu-id="d9e8e-123">hello ReverseFqdn for hello PublicIpAddress can be specified as:</span></span>
* <span data-ttu-id="d9e8e-124">Merhaba Publicıpaddress Hello DNS adı, contosoapp1.northus.cloudapp.azure.com</span><span class="sxs-lookup"><span data-stu-id="d9e8e-124">hello DNS name for hello PublicIpAddress, contosoapp1.northus.cloudapp.azure.com</span></span>
* <span data-ttu-id="d9e8e-125">Merhaba DNS hello içinde farklı bir Publicıpaddress için aynı adı contosoapp2.westus.cloudapp.azure.com gibi abonelik</span><span class="sxs-lookup"><span data-stu-id="d9e8e-125">hello DNS name for a different PublicIpAddress in hello same subscription, such as contosoapp2.westus.cloudapp.azure.com</span></span>
* <span data-ttu-id="d9e8e-126">Bu ad olduğu sürece bir gösterim DNS, app1.contoso.com gibi ad *ilk* bir CNAME toocontosoapp1.northus.cloudapp.azure.com veya tooa olarak farklı Publicıpaddress hello yapılandırılmış aynı abonelik.</span><span class="sxs-lookup"><span data-stu-id="d9e8e-126">A vanity DNS name, such as app1.contoso.com, so long as this name is *first* configured as a CNAME toocontosoapp1.northus.cloudapp.azure.com, or tooa different PublicIpAddress in hello same subscription.</span></span>
* <span data-ttu-id="d9e8e-127">Bu ad olduğu sürece bir gösterim DNS, app1.contoso.com gibi ad *ilk* hello 23.96.52.53 veya farklı bir Publicıpaddress toohello IP adresini bir A kaydı toohello IP adresi yapılandırılmış aynı abonelik.</span><span class="sxs-lookup"><span data-stu-id="d9e8e-127">A vanity DNS name, such as app1.contoso.com, so long as this name is *first* configured as an A record toohello IP address 23.96.52.53, or toohello IP address of a different PublicIpAddress in hello same subscription.</span></span>

<span data-ttu-id="d9e8e-128">Merhaba aynı kısıtlamaları tooreverse DNS bulut Hizmetleri için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="d9e8e-128">hello same constraints apply tooreverse DNS for Cloud Services.</span></span>


## <a name="reverse-dns-for-publicipaddress-resources"></a><span data-ttu-id="d9e8e-129">Geriye doğru DNS Publicıpaddress kaynaklar için</span><span class="sxs-lookup"><span data-stu-id="d9e8e-129">Reverse DNS for PublicIpAddress resources</span></span>

<span data-ttu-id="d9e8e-130">Bu bölümde nasıl tooconfigure ters DNS hello Resource Manager dağıtım modelinde, Azure PowerShell, Azure CLI 1.0 veya Azure CLI 2.0 kullanarak Publicıpaddress kaynaklar için ayrıntılı yönergeler sağlar.</span><span class="sxs-lookup"><span data-stu-id="d9e8e-130">This section provides detailed instructions for how tooconfigure reverse DNS for PublicIpAddress resources in hello Resource Manager deployment model, using either Azure PowerShell, Azure CLI 1.0, or Azure CLI 2.0.</span></span> <span data-ttu-id="d9e8e-131">Geriye doğru DNS Publicıpaddress kaynakları için yapılandırma hello Azure portal şu anda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="d9e8e-131">Configuring reverse DNS for PublicIpAddress resources is not currently supported via hello Azure portal.</span></span>

<span data-ttu-id="d9e8e-132">Azure şu anda destekler DNS yalnızca IPv4 Publicıpaddress kaynaklar için ters çevrilir.</span><span class="sxs-lookup"><span data-stu-id="d9e8e-132">Azure currently supports reverse DNS only for IPv4 PublicIpAddress resources.</span></span> <span data-ttu-id="d9e8e-133">IPv6 için desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="d9e8e-133">It is not supported for IPv6.</span></span>

### <a name="add-reverse-dns-tooan-existing-publicipaddresses"></a><span data-ttu-id="d9e8e-134">Geriye doğru DNS tooan Publicıpaddresses varolan Ekle</span><span class="sxs-lookup"><span data-stu-id="d9e8e-134">Add reverse DNS tooan existing PublicIpAddresses</span></span>

#### <a name="powershell"></a><span data-ttu-id="d9e8e-135">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d9e8e-135">PowerShell</span></span>

<span data-ttu-id="d9e8e-136">Publicıpaddress varolan tooadd geriye doğru DNS tooan:</span><span class="sxs-lookup"><span data-stu-id="d9e8e-136">tooadd reverse DNS tooan existing PublicIpAddress:</span></span>

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings.ReverseFqdn = "contosoapp1.westus.cloudapp.azure.com."
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

<span data-ttu-id="d9e8e-137">tooadd ters DNS tooan zaten bir DNS adı yok Publicıpaddress var, bir DNS adı belirtmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="d9e8e-137">tooadd reverse DNS tooan existing PublicIpAddress that doesn't already have a DNS name, you must also specify a DNS name:</span></span>

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings = New-Object -TypeName "Microsoft.Azure.Commands.Network.Models.PSPublicIpAddressDnsSettings"
$pip.DnsSettings.DomainNameLabel = "contosoapp1"
$pip.DnsSettings.ReverseFqdn = "contosoapp1.westus.cloudapp.azure.com."
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

#### <a name="azure-cli-10"></a><span data-ttu-id="d9e8e-138">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="d9e8e-138">Azure CLI 1.0</span></span>

<span data-ttu-id="d9e8e-139">Publicıpaddress varolan tooadd geriye doğru DNS tooan:</span><span class="sxs-lookup"><span data-stu-id="d9e8e-139">tooadd reverse DNS tooan existing PublicIpAddress:</span></span>

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup -f contosoapp1.westus.cloudapp.azure.com.
```

<span data-ttu-id="d9e8e-140">tooadd ters DNS tooan zaten bir DNS adı yok Publicıpaddress var, bir DNS adı belirtmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="d9e8e-140">tooadd reverse DNS tooan existing PublicIpAddress that doesn't already have a DNS name, you must also specify a DNS name:</span></span>

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup -d contosoapp1 -f contosoapp1.westus.cloudapp.azure.com.
```

#### <a name="azure-cli-20"></a><span data-ttu-id="d9e8e-141">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="d9e8e-141">Azure CLI 2.0</span></span>

<span data-ttu-id="d9e8e-142">Publicıpaddress varolan tooadd geriye doğru DNS tooan:</span><span class="sxs-lookup"><span data-stu-id="d9e8e-142">tooadd reverse DNS tooan existing PublicIpAddress:</span></span>

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn contosoapp1.westus.cloudapp.azure.com.
```

<span data-ttu-id="d9e8e-143">tooadd ters DNS tooan zaten bir DNS adı yok Publicıpaddress var, bir DNS adı belirtmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="d9e8e-143">tooadd reverse DNS tooan existing PublicIpAddress that doesn't already have a DNS name, you must also specify a DNS name:</span></span>

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn contosoapp1.westus.cloudapp.azure.com --dns-name contosoapp1
```

### <a name="create-a-public-ip-address-with-reverse-dns"></a><span data-ttu-id="d9e8e-144">Geriye doğru DNS ile bir ortak IP adresi oluştur</span><span class="sxs-lookup"><span data-stu-id="d9e8e-144">Create a Public IP Address with reverse DNS</span></span>

<span data-ttu-id="d9e8e-145">toocreate zaten belirtilen hello ters DNS özelliği ile yeni bir Publicıpaddress:</span><span class="sxs-lookup"><span data-stu-id="d9e8e-145">toocreate a new PublicIpAddress with hello reverse DNS property already specified:</span></span>

#### <a name="powershell"></a><span data-ttu-id="d9e8e-146">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d9e8e-146">PowerShell</span></span>

```powershell
New-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup" -Location "WestUS" -AllocationMethod Dynamic -DomainNameLabel "contosoapp2" -ReverseFqdn "contosoapp2.westus.cloudapp.azure.com."
```

#### <a name="azure-cli-10"></a><span data-ttu-id="d9e8e-147">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="d9e8e-147">Azure CLI 1.0</span></span>

```azurecli
azure network public-ip create -n PublicIp -g MyResourceGroup -l westus -d contosoapp3 -f contosoapp3.westus.cloudapp.azure.com.
```

#### <a name="azure-cli-20"></a><span data-ttu-id="d9e8e-148">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="d9e8e-148">Azure CLI 2.0</span></span>

```azurecli
az network public-ip create --name PublicIp --resource-group MyResourceGroup --location westcentralus --dns-name contosoapp1 --reverse-fqdn contosoapp1.westcentralus.cloudapp.azure.com
```

### <a name="view-reverse-dns-for-an-existing-publicipaddress"></a><span data-ttu-id="d9e8e-149">Varolan bir Publicıpaddress için ters DNS görünümü</span><span class="sxs-lookup"><span data-stu-id="d9e8e-149">View reverse DNS for an existing PublicIpAddress</span></span>

<span data-ttu-id="d9e8e-150">tooview hello değer var olan bir Publicıpaddress için yapılandırılmış:</span><span class="sxs-lookup"><span data-stu-id="d9e8e-150">tooview hello configured value for an existing PublicIpAddress:</span></span>

#### <a name="powershell"></a><span data-ttu-id="d9e8e-151">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d9e8e-151">PowerShell</span></span>

```powershell
Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
```

#### <a name="azure-cli-10"></a><span data-ttu-id="d9e8e-152">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="d9e8e-152">Azure CLI 1.0</span></span>

```azurecli
azure network public-ip show -n PublicIp -g MyResourceGroup
```

#### <a name="azure-cli-20"></a><span data-ttu-id="d9e8e-153">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="d9e8e-153">Azure CLI 2.0</span></span>

```azurecli
az network public-ip show --name PublicIp --resource-group MyResourceGroup
```

### <a name="remove-reverse-dns-from-existing-public-ip-addresses"></a><span data-ttu-id="d9e8e-154">Mevcut ortak IP adreslerinden geriye doğru DNS Kaldır</span><span class="sxs-lookup"><span data-stu-id="d9e8e-154">Remove reverse DNS from existing Public IP Addresses</span></span>

<span data-ttu-id="d9e8e-155">Varolan bir Publicıpaddress geriye doğru DNS özelliğinden tooremove:</span><span class="sxs-lookup"><span data-stu-id="d9e8e-155">tooremove a reverse DNS property from an existing PublicIpAddress:</span></span>

#### <a name="powershell"></a><span data-ttu-id="d9e8e-156">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d9e8e-156">PowerShell</span></span>

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings.ReverseFqdn = ""
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

#### <a name="azure-cli-10"></a><span data-ttu-id="d9e8e-157">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="d9e8e-157">Azure CLI 1.0</span></span>

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup –f ""
```

#### <a name="azure-cli-20"></a><span data-ttu-id="d9e8e-158">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="d9e8e-158">Azure CLI 2.0</span></span>

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn ""
```


## <a name="configure-reverse-dns-for-cloud-services"></a><span data-ttu-id="d9e8e-159">Bulut Hizmetleri için ters DNS yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d9e8e-159">Configure reverse DNS for Cloud Services</span></span>

<span data-ttu-id="d9e8e-160">Bu bölümde nasıl tooconfigure ters DNS için bulut hizmetlerini Azure PowerShell kullanarak hello Klasik dağıtım modelinde, ayrıntılı yönergeler sağlar.</span><span class="sxs-lookup"><span data-stu-id="d9e8e-160">This section provides detailed instructions for how tooconfigure reverse DNS for Cloud Services in hello Classic deployment model, using Azure PowerShell.</span></span> <span data-ttu-id="d9e8e-161">Bulut Hizmetleri için ters DNS yapılandırma hello Azure portal, Azure CLI 1.0 veya Azure CLI 2.0 desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="d9e8e-161">Configuring reverse DNS for Cloud Services is not supported via hello Azure portal, Azure CLI 1.0, or Azure CLI 2.0.</span></span>

### <a name="add-reverse-dns-tooexisting-cloud-services"></a><span data-ttu-id="d9e8e-162">Geriye doğru DNS tooexisting bulut Hizmetleri Ekle</span><span class="sxs-lookup"><span data-stu-id="d9e8e-162">Add reverse DNS tooexisting Cloud Services</span></span>

<span data-ttu-id="d9e8e-163">Bulut hizmeti varolan geriye doğru DNS kaydı tooan tooadd:</span><span class="sxs-lookup"><span data-stu-id="d9e8e-163">tooadd a reverse DNS record tooan existing Cloud Service:</span></span>

```powershell
Set-AzureService –ServiceName "contosoapp1" –Description "App1 with Reverse DNS" –ReverseDnsFqdn "contosoapp1.cloudapp.net."
```

### <a name="create-a-cloud-service-with-reverse-dns"></a><span data-ttu-id="d9e8e-164">Geriye doğru DNS ile bir bulut hizmeti oluştur</span><span class="sxs-lookup"><span data-stu-id="d9e8e-164">Create a Cloud Service with reverse DNS</span></span>

<span data-ttu-id="d9e8e-165">toocreate zaten belirtilen hello ters DNS özelliği ile yeni bir bulut hizmeti:</span><span class="sxs-lookup"><span data-stu-id="d9e8e-165">toocreate a new Cloud Service with hello reverse DNS property already specified:</span></span>

```powershell
New-AzureService –ServiceName "contosoapp1" –Location "West US" –Description "App1 with Reverse DNS" –ReverseDnsFqdn "contosoapp1.cloudapp.net."
```

### <a name="view-reverse-dns-for-existing-cloud-services"></a><span data-ttu-id="d9e8e-166">Mevcut bulut Hizmetleri için ters DNS görünümü</span><span class="sxs-lookup"><span data-stu-id="d9e8e-166">View reverse DNS for existing Cloud Services</span></span>

<span data-ttu-id="d9e8e-167">tooview hello ters DNS özelliği var olan bir bulut hizmeti için:</span><span class="sxs-lookup"><span data-stu-id="d9e8e-167">tooview hello reverse DNS property for an existing Cloud Service:</span></span>

```powershell
Get-AzureService "contosoapp1"
```

### <a name="remove-reverse-dns-from-existing-cloud-services"></a><span data-ttu-id="d9e8e-168">Mevcut bulut hizmetlerinden geriye doğru DNS Kaldır</span><span class="sxs-lookup"><span data-stu-id="d9e8e-168">Remove reverse DNS from existing Cloud Services</span></span>

<span data-ttu-id="d9e8e-169">var olan bir bulut hizmetinden geriye doğru DNS özelliği tooremove:</span><span class="sxs-lookup"><span data-stu-id="d9e8e-169">tooremove a reverse DNS property from an existing Cloud Service:</span></span>

```powershell
Set-AzureService –ServiceName "contosoapp1" –Description "App1 with Reverse DNS" –ReverseDnsFqdn ""
```

## <a name="faq"></a><span data-ttu-id="d9e8e-170">SSS</span><span class="sxs-lookup"><span data-stu-id="d9e8e-170">FAQ</span></span>

### <a name="how-much-do-reverse-dns-records-cost"></a><span data-ttu-id="d9e8e-171">DNS kayıtları maliyeti ne kadar ters?</span><span class="sxs-lookup"><span data-stu-id="d9e8e-171">How much do reverse DNS records cost?</span></span>

<span data-ttu-id="d9e8e-172">Bunlar boş!</span><span class="sxs-lookup"><span data-stu-id="d9e8e-172">They're free!</span></span>  <span data-ttu-id="d9e8e-173">Geriye doğru DNS kayıtlarını veya sorguları için ek bir maliyet yoktur.</span><span class="sxs-lookup"><span data-stu-id="d9e8e-173">There is no additional cost for reverse DNS records or queries.</span></span>

### <a name="will-my-reverse-dns-records-resolve-from-hello-internet"></a><span data-ttu-id="d9e8e-174">My geriye doğru DNS kayıtları çözümleme Internet hello?</span><span class="sxs-lookup"><span data-stu-id="d9e8e-174">Will my reverse DNS records resolve from hello internet?</span></span>

<span data-ttu-id="d9e8e-175">Evet.</span><span class="sxs-lookup"><span data-stu-id="d9e8e-175">Yes.</span></span> <span data-ttu-id="d9e8e-176">Azure hizmetiniz için hello ters DNS özelliği ayarladıktan sonra tüm hello DNS temsilcilerine Azure yönetir ve tüm Internet kullanıcılar için DNS kaydı ters tooensure çözümler DNS bölgeleri gerekli.</span><span class="sxs-lookup"><span data-stu-id="d9e8e-176">Once you set hello reverse DNS property for your Azure service, Azure manages all hello DNS delegations and DNS zones required tooensure that reverse DNS record resolves for all Internet users.</span></span>

### <a name="are-default-reverse-dns-records-created-for-my-azure-services"></a><span data-ttu-id="d9e8e-177">Varsayılan geriye doğru DNS kayıtları için Azure Hizmetlerim oluşturulur?</span><span class="sxs-lookup"><span data-stu-id="d9e8e-177">Are default reverse DNS records created for my Azure services?</span></span>

<span data-ttu-id="d9e8e-178">Hayır.</span><span class="sxs-lookup"><span data-stu-id="d9e8e-178">No.</span></span> <span data-ttu-id="d9e8e-179">Geriye doğru DNS, bir katılımı özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="d9e8e-179">Reverse DNS is an opt-in feature.</span></span> <span data-ttu-id="d9e8e-180">Geriye doğru DNS kayıtlarını değil tooconfigure seçerseniz oluşturulan varsayılan bunları.</span><span class="sxs-lookup"><span data-stu-id="d9e8e-180">No default reverse DNS records are created if you choose not tooconfigure them.</span></span>

### <a name="what-is-hello-format-for-hello-fully-qualified-domain-name-fqdn"></a><span data-ttu-id="d9e8e-181">Merhaba biçimi hello tam etki alanı adı (FQDN) nedir?</span><span class="sxs-lookup"><span data-stu-id="d9e8e-181">What is hello format for hello fully-qualified domain name (FQDN)?</span></span>

<span data-ttu-id="d9e8e-182">FQDN'ler ileriye doğru sırada belirtilir ve bir nokta (örneğin, "app1.contoso.com.") ile bitmelidir.</span><span class="sxs-lookup"><span data-stu-id="d9e8e-182">FQDNs are specified in forward order, and must be terminated by a dot (for example, "app1.contoso.com.").</span></span>

### <a name="what-happens-if-hello-validation-check-for-hello-reverse-dns-ive-specified-fails"></a><span data-ttu-id="d9e8e-183">Hello için hello doğrulama denetimi belirtmiş olduğunuz DNS geriye doğru başarısız olur ne olur?</span><span class="sxs-lookup"><span data-stu-id="d9e8e-183">What happens if hello validation check for hello reverse DNS I've specified fails?</span></span>

<span data-ttu-id="d9e8e-184">Merhaba geriye doğru DNS doğrulama denetimi başarısız olduğunda, hello işlemi tooconfigure hello geriye doğru DNS kaydı başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="d9e8e-184">Where hello reverse DNS validation check fails, hello operation tooconfigure hello reverse DNS record fails.</span></span> <span data-ttu-id="d9e8e-185">Merhaba geriye doğru DNS değeri gerektiği gibi düzeltin ve yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="d9e8e-185">Correct hello reverse DNS value as required, and retry.</span></span>

### <a name="can-i-configure-reverse-dns-for-azure-app-service"></a><span data-ttu-id="d9e8e-186">Azure App Service için ters DNS yapılandırabilir miyim?</span><span class="sxs-lookup"><span data-stu-id="d9e8e-186">Can I configure reverse DNS for Azure App Service?</span></span>

<span data-ttu-id="d9e8e-187">Hayır.</span><span class="sxs-lookup"><span data-stu-id="d9e8e-187">No.</span></span> <span data-ttu-id="d9e8e-188">Geriye doğru DNS hello Azure App Service için desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="d9e8e-188">Reverse DNS is not supported for hello Azure App Service.</span></span>

### <a name="can-i-configure-multiple-reverse-dns-records-for-my-azure-service"></a><span data-ttu-id="d9e8e-189">Birden çok geriye doğru DNS kaydı için Azure Hizmetim yapılandırabilir miyim?</span><span class="sxs-lookup"><span data-stu-id="d9e8e-189">Can I configure multiple reverse DNS records for my Azure service?</span></span>

<span data-ttu-id="d9e8e-190">Hayır.</span><span class="sxs-lookup"><span data-stu-id="d9e8e-190">No.</span></span> <span data-ttu-id="d9e8e-191">Azure, her Azure bulut hizmeti veya Publicıpaddress için tek bir geriye doğru DNS kaydını destekler.</span><span class="sxs-lookup"><span data-stu-id="d9e8e-191">Azure supports a single reverse DNS record for each Azure Cloud Service or PublicIpAddress.</span></span>

### <a name="can-i-configure-reverse-dns-for-ipv6-publicipaddress-resources"></a><span data-ttu-id="d9e8e-192">IPv6 Publicıpaddress kaynaklar için ters DNS yapılandırabilir miyim?</span><span class="sxs-lookup"><span data-stu-id="d9e8e-192">Can I configure reverse DNS for IPv6 PublicIpAddress resources?</span></span>

<span data-ttu-id="d9e8e-193">Hayır.</span><span class="sxs-lookup"><span data-stu-id="d9e8e-193">No.</span></span> <span data-ttu-id="d9e8e-194">Azure şu anda destekler DNS yalnızca IPv4 Publicıpaddress kaynaklar ve bulut Hizmetleri için ters çevrilir.</span><span class="sxs-lookup"><span data-stu-id="d9e8e-194">Azure currently supports reverse DNS only for IPv4 PublicIpAddress resources and Cloud Services.</span></span>

### <a name="can-i-send-emails-tooexternal-domains-from-my-azure-compute-services"></a><span data-ttu-id="d9e8e-195">Azure işlem Hizmetlerim e-postaları tooexternal etki alanları gönderebilirim?</span><span class="sxs-lookup"><span data-stu-id="d9e8e-195">Can I send emails tooexternal domains from my Azure Compute services?</span></span>

<span data-ttu-id="d9e8e-196">Hayır.</span><span class="sxs-lookup"><span data-stu-id="d9e8e-196">No.</span></span> [<span data-ttu-id="d9e8e-197">Azure işlem Hizmetleri gönderen e-postaları tooexternal etki alanlarını desteklemiyor</span><span class="sxs-lookup"><span data-stu-id="d9e8e-197">Azure Compute services do not support sending emails tooexternal domains</span></span>](https://blogs.msdn.microsoft.com/mast/2016/04/04/sending-e-mail-from-azure-compute-resource-to-external-domains/)

## <a name="next-steps"></a><span data-ttu-id="d9e8e-198">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d9e8e-198">Next steps</span></span>

<span data-ttu-id="d9e8e-199">Geriye doğru DNS hakkında daha fazla bilgi için bkz: [wikipedia'da ters DNS araması](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span><span class="sxs-lookup"><span data-stu-id="d9e8e-199">For more information on reverse DNS, see [reverse DNS lookup on Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span></span>
<br>
<span data-ttu-id="d9e8e-200">Nasıl çok öğrenin[konak hello geriye doğru arama bölgesi ISS atanan IP aralığınızı Azure DNS'de için](dns-reverse-dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="d9e8e-200">Learn how too[host hello reverse lookup zone for your ISP-assigned IP range in Azure DNS](dns-reverse-dns-for-azure-services.md).</span></span>

