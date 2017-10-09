---
title: "aaaManage DNS bölgeleri Azure DNS - PowerShell | Microsoft Docs"
description: "DNS bölgelerini Azure Powershell kullanarak yönetebilirsiniz. Bu makalede nasıl tooupdate, silme ve Azure DNS üzerinde DNS bölgeleri oluşturma"
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: a67992ab-8166-4052-9b28-554c5a39e60c
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/14/2016
ms.author: gwallace
ms.openlocfilehash: 261b89f72213aa9784034d47ff9d1c55a4e80d65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-using-powershell"></a><span data-ttu-id="7fda7-104">Nasıl toomanage DNS bölgeleri PowerShell'i kullanma</span><span class="sxs-lookup"><span data-stu-id="7fda7-104">How toomanage DNS Zones using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="7fda7-105">Portal</span><span class="sxs-lookup"><span data-stu-id="7fda7-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="7fda7-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7fda7-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="7fda7-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="7fda7-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="7fda7-108">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="7fda7-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)

<span data-ttu-id="7fda7-109">Bu makalede, nasıl Azure PowerShell kullanarak toomanage DNS bölgeleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="7fda7-109">This article shows you how toomanage your DNS zones by using Azure PowerShell.</span></span> <span data-ttu-id="7fda7-110">DNS bölgelerini hello platformlar arası kullanarak da yönetebilirsiniz [Azure CLI](dns-operations-dnszones-cli.md) ya da Azure portal hello.</span><span class="sxs-lookup"><span data-stu-id="7fda7-110">You can also manage your DNS zones using hello cross-platform [Azure CLI](dns-operations-dnszones-cli.md) or hello Azure portal.</span></span>

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

[!INCLUDE [dns-powershell-setup](../../includes/dns-powershell-setup-include.md)]


## <a name="create-a-dns-zone"></a><span data-ttu-id="7fda7-111">DNS bölgesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="7fda7-111">Create a DNS zone</span></span>

<span data-ttu-id="7fda7-112">Bir DNS bölgesi hello kullanılarak oluşturulan `New-AzureRmDnsZone` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="7fda7-112">A DNS zone is created by using hello `New-AzureRmDnsZone` cmdlet.</span></span>

<span data-ttu-id="7fda7-113">Merhaba aşağıdaki örnek adlı bir DNS bölgesi oluşturur *contoso.com* adlı hello kaynak grubunda *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="7fda7-113">hello following example creates a DNS zone called *contoso.com* in hello resource group called *MyResourceGroup*:</span></span>

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
```

<span data-ttu-id="7fda7-114">Hello aşağıdaki örnekte nasıl toocreate bir DNS bölgesi iki gösterir [Azure Resource Manager etiketlerine](dns-zones-records.md#tags), *project = demo* ve *env = test*:</span><span class="sxs-lookup"><span data-stu-id="7fda7-114">hello following example shows how toocreate a DNS zone with two [Azure Resource Manager tags](dns-zones-records.md#tags), *project = demo* and *env = test*:</span></span>

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup -Tag @{ project="demo"; env="test" }
```

## <a name="get-a-dns-zone"></a><span data-ttu-id="7fda7-115">Bir DNS bölgesini alın</span><span class="sxs-lookup"><span data-stu-id="7fda7-115">Get a DNS zone</span></span>

<span data-ttu-id="7fda7-116">tooretrieve bir DNS bölgesi kullanmak hello `Get-AzureRmDnsZone` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="7fda7-116">tooretrieve a DNS zone, use hello `Get-AzureRmDnsZone` cmdlet.</span></span> <span data-ttu-id="7fda7-117">Bu işlem, bir DNS bölgesi nesne karşılık gelen tooan varolan bir bölge Azure DNS'de döndürür.</span><span class="sxs-lookup"><span data-stu-id="7fda7-117">This operation returns a DNS zone object corresponding tooan existing zone in Azure DNS.</span></span> <span data-ttu-id="7fda7-118">Merhaba nesne hello bölge (örneğin, kayıt kümesi sayısı hello) hakkında veri içerir, ancak kayıt kümelerini hello kendilerini içermiyor (bkz: `Get-AzureRmDnsRecordSet`).</span><span class="sxs-lookup"><span data-stu-id="7fda7-118">hello object contains data about hello zone (such as hello number of record sets), but does not contain hello record sets themselves (see `Get-AzureRmDnsRecordSet`).</span></span>

```powershell
Get-AzureRmDnsZone -Name contoso.com –ResourceGroupName MyAzureResourceGroup

Name                  : contoso.com
ResourceGroupName     : myresourcegroup
Etag                  : 00000003-0000-0000-8ec2-f4879750d201
Tags                  : {project, env}
NameServers           : {ns1-01.azure-dns.com., ns2-01.azure-dns.net., ns3-01.azure-dns.org.,
                        ns4-01.azure-dns.info.}
NumberOfRecordSets    : 2
MaxNumberOfRecordSets : 5000
```

## <a name="list-dns-zones"></a><span data-ttu-id="7fda7-119">Liste DNS bölgeleri</span><span class="sxs-lookup"><span data-stu-id="7fda7-119">List DNS zones</span></span>

<span data-ttu-id="7fda7-120">Merhaba bölge adını atlama tarafından `Get-AzureRmDnsZone`, bir kaynak grubundaki tüm bölgeler sıralayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7fda7-120">By omitting hello zone name from `Get-AzureRmDnsZone`, you can enumerate all zones in a resource group.</span></span> <span data-ttu-id="7fda7-121">Bu işlem, bölge nesneleri içeren bir dizi döndürür.</span><span class="sxs-lookup"><span data-stu-id="7fda7-121">This operation returns an array of zone objects.</span></span>

```powershell
$zoneList = Get-AzureRmDnsZone -ResourceGroupName MyAzureResourceGroup
```

<span data-ttu-id="7fda7-122">Merhaba bölge adı ve hello kaynak grubu adı atlama tarafından `Get-AzureRmDnsZone`, tüm bölgelerde hello Azure aboneliği sıralayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7fda7-122">By omitting both hello zone name and hello resource group name from `Get-AzureRmDnsZone`, you can enumerate all zones in hello Azure subscription.</span></span>

```powershell
$zoneList = Get-AzureRmDnsZone
```

## <a name="update-a-dns-zone"></a><span data-ttu-id="7fda7-123">Bir DNS bölgesini güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="7fda7-123">Update a DNS zone</span></span>

<span data-ttu-id="7fda7-124">Değişiklikleri kullanarak DNS bölgesi kaynak yapılabilir tooa `Set-AzureRmDnsZone`.</span><span class="sxs-lookup"><span data-stu-id="7fda7-124">Changes tooa DNS zone resource can be made by using `Set-AzureRmDnsZone`.</span></span> <span data-ttu-id="7fda7-125">Bu cmdlet herhangi bir hello DNS kayıt kümelerini hello bölge içinde güncelleştirmez (bkz [nasıl tooManage DNS kayıtlarını](dns-operations-recordsets.md)).</span><span class="sxs-lookup"><span data-stu-id="7fda7-125">This cmdlet does not update any of hello DNS record sets within hello zone (see [How tooManage DNS records](dns-operations-recordsets.md)).</span></span> <span data-ttu-id="7fda7-126">Yalnızca hello bölge kaynağını kendisini tooupdate özelliklerini de kullandı.</span><span class="sxs-lookup"><span data-stu-id="7fda7-126">It's only used tooupdate properties of hello zone resource itself.</span></span> <span data-ttu-id="7fda7-127">Merhaba yazılabilir bölge özellikleri olan şu anda sınırlı toohello [Azure Resource Manager 'etiketleri' hello bölge kaynak için](dns-zones-records.md#tags).</span><span class="sxs-lookup"><span data-stu-id="7fda7-127">hello writable zone properties are currently limited toohello [Azure Resource Manager ‘tags’ for hello zone resource](dns-zones-records.md#tags).</span></span>

<span data-ttu-id="7fda7-128">Bir DNS bölgesi iki yolu tooupdate aşağıdaki hello birini kullanın:</span><span class="sxs-lookup"><span data-stu-id="7fda7-128">Use one of hello following two ways tooupdate a DNS zone:</span></span>

### <a name="specify-hello-zone-using-hello-zone-name-and-resource-group"></a><span data-ttu-id="7fda7-129">Merhaba bölge adı ve kaynak grubu kullanarak hello bölgesi belirtin</span><span class="sxs-lookup"><span data-stu-id="7fda7-129">Specify hello zone using hello zone name and resource group</span></span>

<span data-ttu-id="7fda7-130">Bu yaklaşım hello varolan bölge etiketleri belirtilen hello değerlerle değiştirir.</span><span class="sxs-lookup"><span data-stu-id="7fda7-130">This approach replaces hello existing zone tags with hello values specified.</span></span>

```powershell
Set-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup -Tag @{ project="demo"; env="test" }
```

### <a name="specify-hello-zone-using-a-zone-object"></a><span data-ttu-id="7fda7-131">Bir $zone nesnesi kullanılarak hello dilimini belirtin</span><span class="sxs-lookup"><span data-stu-id="7fda7-131">Specify hello zone using a $zone object</span></span>

<span data-ttu-id="7fda7-132">Bu yaklaşım hello varolan bölge nesnesi alır, hello etiketleri değiştirir ve hello değişiklikleri kaydeder.</span><span class="sxs-lookup"><span data-stu-id="7fda7-132">This approach retrieves hello existing zone object, modifies hello tags, and then commits hello changes.</span></span> <span data-ttu-id="7fda7-133">Bu şekilde, varolan etiketleri korunabilir.</span><span class="sxs-lookup"><span data-stu-id="7fda7-133">In this way, existing tags can be preserved.</span></span>

```powershell
# Get hello zone object
$zone = Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup

# Remove an existing tag
$zone.Tags.Remove("project")

# Add a new tag
$zone.Tags.Add("status","approved")

# Commit changes
Set-AzureRmDnsZone -Zone $zone
```

<span data-ttu-id="7fda7-134">Kullanırken `Set-AzureRmDnsZone` $zone nesnesiyle [Etag denetler](dns-zones-records.md#etags) kullanılan tooensure eşzamanlı değişiklikleri yazılmaz.</span><span class="sxs-lookup"><span data-stu-id="7fda7-134">When using `Set-AzureRmDnsZone` with a $zone object, [Etag checks](dns-zones-records.md#etags) are used tooensure concurrent changes are not overwritten.</span></span> <span data-ttu-id="7fda7-135">İsteğe bağlı hello kullanabilirsiniz `-Overwrite` bu denetimleri toosuppress geçin.</span><span class="sxs-lookup"><span data-stu-id="7fda7-135">You can use hello optional `-Overwrite` switch toosuppress these checks.</span></span>

## <a name="delete-a-dns-zone"></a><span data-ttu-id="7fda7-136">Bir DNS bölgesi Sil</span><span class="sxs-lookup"><span data-stu-id="7fda7-136">Delete a DNS Zone</span></span>

<span data-ttu-id="7fda7-137">DNS bölgelerini hello kullanarak silinebilir `Remove-AzureRmDnsZone` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="7fda7-137">DNS zones can be deleted using hello `Remove-AzureRmDnsZone` cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="7fda7-138">Bir DNS bölgesi silme hello bölgedeki tüm DNS kayıtlarını siler.</span><span class="sxs-lookup"><span data-stu-id="7fda7-138">Deleting a DNS zone also deletes all DNS records within hello zone.</span></span> <span data-ttu-id="7fda7-139">Bu işlem geri alınamaz.</span><span class="sxs-lookup"><span data-stu-id="7fda7-139">This operation cannot be undone.</span></span> <span data-ttu-id="7fda7-140">Merhaba DNS bölgesi kullanımdaysa hello bölge silindiğinde hello bölge kullanarak Hizmetleri başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="7fda7-140">If hello DNS zone is in use, services using hello zone will fail when hello zone is deleted.</span></span>
>
><span data-ttu-id="7fda7-141">yanlışlıkla bölge silinmesine karşı tooprotect bkz [nasıl tooprotect DNS bölgeleri ve kayıtları](dns-protect-zones-recordsets.md).</span><span class="sxs-lookup"><span data-stu-id="7fda7-141">tooprotect against accidental zone deletion, see [How tooprotect DNS zones and records](dns-protect-zones-recordsets.md).</span></span>


<span data-ttu-id="7fda7-142">Bir DNS bölgesi iki yolu toodelete aşağıdaki hello birini kullanın:</span><span class="sxs-lookup"><span data-stu-id="7fda7-142">Use one of hello following two ways toodelete a DNS zone:</span></span>

### <a name="specify-hello-zone-using-hello-zone-name-and-resource-group-name"></a><span data-ttu-id="7fda7-143">Merhaba bölge adı ve kaynak grubu adı kullanarak hello bölgesi belirtin</span><span class="sxs-lookup"><span data-stu-id="7fda7-143">Specify hello zone using hello zone name and resource group name</span></span>

```powershell
Remove-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
```

### <a name="specify-hello-zone-using-a-zone-object"></a><span data-ttu-id="7fda7-144">Bir $zone nesnesi kullanılarak hello dilimini belirtin</span><span class="sxs-lookup"><span data-stu-id="7fda7-144">Specify hello zone using a $zone object</span></span>

<span data-ttu-id="7fda7-145">Merhaba bölge toobe kullanılarak silinen belirtebilirsiniz bir `$zone` tarafından döndürülen nesne `Get-AzureRmDnsZone`.</span><span class="sxs-lookup"><span data-stu-id="7fda7-145">You can specify hello zone toobe deleted using a `$zone` object returned by `Get-AzureRmDnsZone`.</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
Remove-AzureRmDnsZone -Zone $zone
```

<span data-ttu-id="7fda7-146">Merhaba bölge nesnesini parametre olarak geçirilen yerine de yöneltilen:</span><span class="sxs-lookup"><span data-stu-id="7fda7-146">hello zone object can also be piped instead of being passed as a parameter:</span></span>

```powershell
Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup | Remove-AzureRmDnsZone

```

<span data-ttu-id="7fda7-147">İle `Set-AzureRmDnsZone`, belirtme hello bölge kullanarak bir `$zone` nesne Etag denetler tooensure eşzamanlı değişiklikleri silinmez etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="7fda7-147">As with `Set-AzureRmDnsZone`, specifying hello zone using a `$zone` object enables Etag checks tooensure concurrent changes are not deleted.</span></span> <span data-ttu-id="7fda7-148">Kullanım hello `-Overwrite` bu denetimleri toosuppress geçin.</span><span class="sxs-lookup"><span data-stu-id="7fda7-148">Use hello `-Overwrite` switch toosuppress these checks.</span></span>

## <a name="confirmation-prompts"></a><span data-ttu-id="7fda7-149">Onay istekleri</span><span class="sxs-lookup"><span data-stu-id="7fda7-149">Confirmation prompts</span></span>

<span data-ttu-id="7fda7-150">Merhaba `New-AzureRmDnsZone`, `Set-AzureRmDnsZone`, ve `Remove-AzureRmDnsZone` cmdlet'leri tüm destek onay ister.</span><span class="sxs-lookup"><span data-stu-id="7fda7-150">hello `New-AzureRmDnsZone`, `Set-AzureRmDnsZone`, and `Remove-AzureRmDnsZone` cmdlets all support confirmation prompts.</span></span>

<span data-ttu-id="7fda7-151">Her ikisi de `New-AzureRmDnsZone` ve `Set-AzureRmDnsZone` hello varsa onay iste `$ConfirmPreference` PowerShell tercih değişkeni değerine sahip `Medium` veya daha düşük.</span><span class="sxs-lookup"><span data-stu-id="7fda7-151">Both `New-AzureRmDnsZone` and `Set-AzureRmDnsZone` prompt for confirmation if hello `$ConfirmPreference` PowerShell preference variable has a value of `Medium` or lower.</span></span> <span data-ttu-id="7fda7-152">Bir DNS bölgesi hello silme toohello olasılığı yüksek etkisi nedeniyle `Remove-AzureRmDnsZone` cmdlet hello varsa onay ister `$ConfirmPreference` PowerShell değişkeni sahip herhangi bir değer dışındaki `None`.</span><span class="sxs-lookup"><span data-stu-id="7fda7-152">Due toohello potentially high impact of deleting a DNS zone, hello `Remove-AzureRmDnsZone` cmdlet prompts for confirmation if hello `$ConfirmPreference` PowerShell variable has any value other than `None`.</span></span>

<span data-ttu-id="7fda7-153">Merhaba varsayılan değeri itibaren `$ConfirmPreference` olan `High`, yalnızca `Remove-AzureRmDnsZone` varsayılan olarak onaylamanız istenir.</span><span class="sxs-lookup"><span data-stu-id="7fda7-153">Since hello default value for `$ConfirmPreference` is `High`, only `Remove-AzureRmDnsZone` prompts for confirmation by default.</span></span>

<span data-ttu-id="7fda7-154">Merhaba geçerli kılabilirsiniz `$ConfirmPreference` hello kullanarak ayarını `-Confirm` parametresi.</span><span class="sxs-lookup"><span data-stu-id="7fda7-154">You can override hello current `$ConfirmPreference` setting using hello `-Confirm` parameter.</span></span> <span data-ttu-id="7fda7-155">Belirtirseniz `-Confirm` veya `-Confirm:$True` , hello cmdlet sizden, önce onay çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="7fda7-155">If you specify `-Confirm` or `-Confirm:$True` , hello cmdlet prompts you for confirmation before it runs.</span></span> <span data-ttu-id="7fda7-156">Belirtirseniz `-Confirm:$False` , hello cmdlet istenmez sizin için onay.</span><span class="sxs-lookup"><span data-stu-id="7fda7-156">If you specify `-Confirm:$False` , hello cmdlet does not prompt you for confirmation.</span></span>

<span data-ttu-id="7fda7-157">Hakkında daha fazla bilgi için `-Confirm` ve `$ConfirmPreference`, bkz: [tercih değişkenleri hakkında](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).</span><span class="sxs-lookup"><span data-stu-id="7fda7-157">For more information about `-Confirm` and `$ConfirmPreference`, see [About Preference Variables](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7fda7-158">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7fda7-158">Next steps</span></span>

<span data-ttu-id="7fda7-159">Nasıl çok öğrenin[kayıt kümelerini ve kayıtları yönetmek](dns-operations-recordsets.md) DNS bölgesinde.</span><span class="sxs-lookup"><span data-stu-id="7fda7-159">Learn how too[manage record sets and records](dns-operations-recordsets.md) in your DNS zone.</span></span>
<br>
<span data-ttu-id="7fda7-160">Nasıl çok öğrenin[, etki alanı tooAzure DNS temsilci](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="7fda7-160">Learn how too[delegate your domain tooAzure DNS](dns-domain-delegation.md).</span></span>
<br>
<span data-ttu-id="7fda7-161">Gözden geçirme hello [Azure DNS PowerShell başvuru belgeleri](/powershell/module/azurerm.dns).</span><span class="sxs-lookup"><span data-stu-id="7fda7-161">Review hello [Azure DNS PowerShell reference documentation](/powershell/module/azurerm.dns).</span></span>

