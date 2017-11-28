---
title: "Azure DNS'de - PowerShell DNS bölgelerini yönetme | Microsoft Docs"
description: "DNS bölgelerini Azure Powershell kullanarak yönetebilirsiniz. Bu makalede, güncelleştirme, silme ve DNS bölgelerini Azure DNS üzerinde oluşturmak açıklar"
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
ms.openlocfilehash: 92f1da660d875c76d5d826669d6c1d12018c3d0a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-dns-zones-using-powershell"></a><span data-ttu-id="a7a3e-104">PowerShell kullanarak DNS bölgelerini yönetme</span><span class="sxs-lookup"><span data-stu-id="a7a3e-104">How to manage DNS Zones using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="a7a3e-105">Portal</span><span class="sxs-lookup"><span data-stu-id="a7a3e-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="a7a3e-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a7a3e-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="a7a3e-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="a7a3e-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="a7a3e-108">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="a7a3e-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)

<span data-ttu-id="a7a3e-109">Bu makalede, Azure PowerShell kullanarak DNS bölgelerini yönetme gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="a7a3e-109">This article shows you how to manage your DNS zones by using Azure PowerShell.</span></span> <span data-ttu-id="a7a3e-110">Platformlar arası kullanarak DNS bölgelerini yönetebilmeniz için [Azure CLI](dns-operations-dnszones-cli.md) ya da Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a7a3e-110">You can also manage your DNS zones using the cross-platform [Azure CLI](dns-operations-dnszones-cli.md) or the Azure portal.</span></span>

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

[!INCLUDE [dns-powershell-setup](../../includes/dns-powershell-setup-include.md)]


## <a name="create-a-dns-zone"></a><span data-ttu-id="a7a3e-111">DNS bölgesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="a7a3e-111">Create a DNS zone</span></span>

<span data-ttu-id="a7a3e-112">DNS bölgesi, `New-AzureRmDnsZone` cmdlet’i kullanılarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="a7a3e-112">A DNS zone is created by using the `New-AzureRmDnsZone` cmdlet.</span></span>

<span data-ttu-id="a7a3e-113">Aşağıdaki örnek adlı bir DNS bölgesi oluşturur *contoso.com* kaynak grubunda *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="a7a3e-113">The following example creates a DNS zone called *contoso.com* in the resource group called *MyResourceGroup*:</span></span>

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
```

<span data-ttu-id="a7a3e-114">Aşağıdaki örnek bir DNS bölgesi iki oluşturulacağını gösterir [Azure Resource Manager etiketlerine](dns-zones-records.md#tags), *project = demo* ve *env = test*:</span><span class="sxs-lookup"><span data-stu-id="a7a3e-114">The following example shows how to create a DNS zone with two [Azure Resource Manager tags](dns-zones-records.md#tags), *project = demo* and *env = test*:</span></span>

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup -Tag @{ project="demo"; env="test" }
```

## <a name="get-a-dns-zone"></a><span data-ttu-id="a7a3e-115">Bir DNS bölgesini alın</span><span class="sxs-lookup"><span data-stu-id="a7a3e-115">Get a DNS zone</span></span>

<span data-ttu-id="a7a3e-116">Bir DNS bölgesi almak kullanın `Get-AzureRmDnsZone` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="a7a3e-116">To retrieve a DNS zone, use the `Get-AzureRmDnsZone` cmdlet.</span></span> <span data-ttu-id="a7a3e-117">Bu işlem, Azure DNS'de mevcut bir bölgeyi karşılık gelen bir DNS bölgesi nesnesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="a7a3e-117">This operation returns a DNS zone object corresponding to an existing zone in Azure DNS.</span></span> <span data-ttu-id="a7a3e-118">Nesne bölge (örneğin, kayıt kümesi sayısı) hakkında veri içerir, ancak kayıt kümelerini içermiyor (bkz: `Get-AzureRmDnsRecordSet`).</span><span class="sxs-lookup"><span data-stu-id="a7a3e-118">The object contains data about the zone (such as the number of record sets), but does not contain the record sets themselves (see `Get-AzureRmDnsRecordSet`).</span></span>

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

## <a name="list-dns-zones"></a><span data-ttu-id="a7a3e-119">Liste DNS bölgeleri</span><span class="sxs-lookup"><span data-stu-id="a7a3e-119">List DNS zones</span></span>

<span data-ttu-id="a7a3e-120">Bölge adı atlama tarafından `Get-AzureRmDnsZone`, bir kaynak grubundaki tüm bölgeler sıralayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a7a3e-120">By omitting the zone name from `Get-AzureRmDnsZone`, you can enumerate all zones in a resource group.</span></span> <span data-ttu-id="a7a3e-121">Bu işlem, bölge nesneleri içeren bir dizi döndürür.</span><span class="sxs-lookup"><span data-stu-id="a7a3e-121">This operation returns an array of zone objects.</span></span>

```powershell
$zoneList = Get-AzureRmDnsZone -ResourceGroupName MyAzureResourceGroup
```

<span data-ttu-id="a7a3e-122">Bölge adı ve kaynak grubu adı atlama tarafından `Get-AzureRmDnsZone`, Azure aboneliğindeki tüm bölgeler sıralayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a7a3e-122">By omitting both the zone name and the resource group name from `Get-AzureRmDnsZone`, you can enumerate all zones in the Azure subscription.</span></span>

```powershell
$zoneList = Get-AzureRmDnsZone
```

## <a name="update-a-dns-zone"></a><span data-ttu-id="a7a3e-123">Bir DNS bölgesini güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="a7a3e-123">Update a DNS zone</span></span>

<span data-ttu-id="a7a3e-124">Kullanarak bir DNS bölgesi kaynak değişiklikler yapılabilir `Set-AzureRmDnsZone`.</span><span class="sxs-lookup"><span data-stu-id="a7a3e-124">Changes to a DNS zone resource can be made by using `Set-AzureRmDnsZone`.</span></span> <span data-ttu-id="a7a3e-125">Bu cmdlet herhangi bir bölgede DNS kayıt kümelerini güncelleştirmez (bkz [yönetmek DNS kayıtlarını nasıl](dns-operations-recordsets.md)).</span><span class="sxs-lookup"><span data-stu-id="a7a3e-125">This cmdlet does not update any of the DNS record sets within the zone (see [How to Manage DNS records](dns-operations-recordsets.md)).</span></span> <span data-ttu-id="a7a3e-126">Yalnızca, bölge kaynak özelliklerini güncelleştirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a7a3e-126">It's only used to update properties of the zone resource itself.</span></span> <span data-ttu-id="a7a3e-127">Yazılabilir bölge özellikleri şu anda sınırlı [Azure Resource Manager 'etiketleri' bölge kaynak için](dns-zones-records.md#tags).</span><span class="sxs-lookup"><span data-stu-id="a7a3e-127">The writable zone properties are currently limited to the [Azure Resource Manager ‘tags’ for the zone resource](dns-zones-records.md#tags).</span></span>

<span data-ttu-id="a7a3e-128">Bir DNS bölgesi güncelleştirmek için aşağıdaki iki yöntemden birini kullanın:</span><span class="sxs-lookup"><span data-stu-id="a7a3e-128">Use one of the following two ways to update a DNS zone:</span></span>

### <a name="specify-the-zone-using-the-zone-name-and-resource-group"></a><span data-ttu-id="a7a3e-129">Bölge adını ve kaynak grubu kullanarak bölgesi belirtin</span><span class="sxs-lookup"><span data-stu-id="a7a3e-129">Specify the zone using the zone name and resource group</span></span>

<span data-ttu-id="a7a3e-130">Bu yaklaşım varolan bölge etiketleri belirtilen değerlerle değiştirir.</span><span class="sxs-lookup"><span data-stu-id="a7a3e-130">This approach replaces the existing zone tags with the values specified.</span></span>

```powershell
Set-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup -Tag @{ project="demo"; env="test" }
```

### <a name="specify-the-zone-using-a-zone-object"></a><span data-ttu-id="a7a3e-131">Bir $zone nesnesi kullanılarak dilimini belirtin</span><span class="sxs-lookup"><span data-stu-id="a7a3e-131">Specify the zone using a $zone object</span></span>

<span data-ttu-id="a7a3e-132">Bu yaklaşım, bölge nesnelerinden alır, etiketleri değiştirir ve değişiklikleri kaydeder.</span><span class="sxs-lookup"><span data-stu-id="a7a3e-132">This approach retrieves the existing zone object, modifies the tags, and then commits the changes.</span></span> <span data-ttu-id="a7a3e-133">Bu şekilde, varolan etiketleri korunabilir.</span><span class="sxs-lookup"><span data-stu-id="a7a3e-133">In this way, existing tags can be preserved.</span></span>

```powershell
# Get the zone object
$zone = Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup

# Remove an existing tag
$zone.Tags.Remove("project")

# Add a new tag
$zone.Tags.Add("status","approved")

# Commit changes
Set-AzureRmDnsZone -Zone $zone
```

<span data-ttu-id="a7a3e-134">Kullanırken `Set-AzureRmDnsZone` $zone nesnesiyle [Etag denetler](dns-zones-records.md#etags) eşzamanlı değişiklikleri yazılmaz sağlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a7a3e-134">When using `Set-AzureRmDnsZone` with a $zone object, [Etag checks](dns-zones-records.md#etags) are used to ensure concurrent changes are not overwritten.</span></span> <span data-ttu-id="a7a3e-135">Kullanabileceğiniz isteğe bağlı `-Overwrite` bu denetimleri gizlemek için anahtar.</span><span class="sxs-lookup"><span data-stu-id="a7a3e-135">You can use the optional `-Overwrite` switch to suppress these checks.</span></span>

## <a name="delete-a-dns-zone"></a><span data-ttu-id="a7a3e-136">Bir DNS bölgesi Sil</span><span class="sxs-lookup"><span data-stu-id="a7a3e-136">Delete a DNS Zone</span></span>

<span data-ttu-id="a7a3e-137">DNS bölgeleri kullanılarak silinebilir `Remove-AzureRmDnsZone` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="a7a3e-137">DNS zones can be deleted using the `Remove-AzureRmDnsZone` cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="a7a3e-138">Bir DNS bölgesi silme bölgedeki tüm DNS kayıtlarını siler.</span><span class="sxs-lookup"><span data-stu-id="a7a3e-138">Deleting a DNS zone also deletes all DNS records within the zone.</span></span> <span data-ttu-id="a7a3e-139">Bu işlem geri alınamaz.</span><span class="sxs-lookup"><span data-stu-id="a7a3e-139">This operation cannot be undone.</span></span> <span data-ttu-id="a7a3e-140">DNS bölgesi kullanımdaysa, bölge silindiğinde bölge kullanarak Hizmetleri başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="a7a3e-140">If the DNS zone is in use, services using the zone will fail when the zone is deleted.</span></span>
>
><span data-ttu-id="a7a3e-141">Yanlışlıkla bölge silinmeye karşı korumak için bkz: [DNS bölgeleri ve kayıtları korumak nasıl](dns-protect-zones-recordsets.md).</span><span class="sxs-lookup"><span data-stu-id="a7a3e-141">To protect against accidental zone deletion, see [How to protect DNS zones and records](dns-protect-zones-recordsets.md).</span></span>


<span data-ttu-id="a7a3e-142">Bir DNS bölgesini silmek için aşağıdaki iki yöntemden birini kullanın:</span><span class="sxs-lookup"><span data-stu-id="a7a3e-142">Use one of the following two ways to delete a DNS zone:</span></span>

### <a name="specify-the-zone-using-the-zone-name-and-resource-group-name"></a><span data-ttu-id="a7a3e-143">Kaynak grubu adı ve bölge adını kullanarak bölgesi belirtin</span><span class="sxs-lookup"><span data-stu-id="a7a3e-143">Specify the zone using the zone name and resource group name</span></span>

```powershell
Remove-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
```

### <a name="specify-the-zone-using-a-zone-object"></a><span data-ttu-id="a7a3e-144">Bir $zone nesnesi kullanılarak dilimini belirtin</span><span class="sxs-lookup"><span data-stu-id="a7a3e-144">Specify the zone using a $zone object</span></span>

<span data-ttu-id="a7a3e-145">Kullanarak silinmesi bölgesine belirtebilirsiniz bir `$zone` tarafından döndürülen nesne `Get-AzureRmDnsZone`.</span><span class="sxs-lookup"><span data-stu-id="a7a3e-145">You can specify the zone to be deleted using a `$zone` object returned by `Get-AzureRmDnsZone`.</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
Remove-AzureRmDnsZone -Zone $zone
```

<span data-ttu-id="a7a3e-146">Bölge nesnesini parametre olarak geçirilen yerine de yöneltilen:</span><span class="sxs-lookup"><span data-stu-id="a7a3e-146">The zone object can also be piped instead of being passed as a parameter:</span></span>

```powershell
Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup | Remove-AzureRmDnsZone

```

<span data-ttu-id="a7a3e-147">İle `Set-AzureRmDnsZone`, bölge kullanarak belirten bir `$zone` nesne eşzamanlı değişiklikleri silinmez emin olmak Etag denetimleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="a7a3e-147">As with `Set-AzureRmDnsZone`, specifying the zone using a `$zone` object enables Etag checks to ensure concurrent changes are not deleted.</span></span> <span data-ttu-id="a7a3e-148">Kullanım `-Overwrite` bu denetimleri gizlemek için anahtar.</span><span class="sxs-lookup"><span data-stu-id="a7a3e-148">Use the `-Overwrite` switch to suppress these checks.</span></span>

## <a name="confirmation-prompts"></a><span data-ttu-id="a7a3e-149">Onay istekleri</span><span class="sxs-lookup"><span data-stu-id="a7a3e-149">Confirmation prompts</span></span>

<span data-ttu-id="a7a3e-150">`New-AzureRmDnsZone`, `Set-AzureRmDnsZone`, Ve `Remove-AzureRmDnsZone` cmdlet'leri tüm destek onay ister.</span><span class="sxs-lookup"><span data-stu-id="a7a3e-150">The `New-AzureRmDnsZone`, `Set-AzureRmDnsZone`, and `Remove-AzureRmDnsZone` cmdlets all support confirmation prompts.</span></span>

<span data-ttu-id="a7a3e-151">Her ikisi de `New-AzureRmDnsZone` ve `Set-AzureRmDnsZone` için onay iste `$ConfirmPreference` PowerShell tercih değişkeni değerine sahip `Medium` veya daha düşük.</span><span class="sxs-lookup"><span data-stu-id="a7a3e-151">Both `New-AzureRmDnsZone` and `Set-AzureRmDnsZone` prompt for confirmation if the `$ConfirmPreference` PowerShell preference variable has a value of `Medium` or lower.</span></span> <span data-ttu-id="a7a3e-152">Bir DNS bölgesi silme olasılığı yüksek etkisi nedeniyle `Remove-AzureRmDnsZone` cmdlet, onay ister `$ConfirmPreference` PowerShell değişkeni sahip herhangi bir değer dışındaki `None`.</span><span class="sxs-lookup"><span data-stu-id="a7a3e-152">Due to the potentially high impact of deleting a DNS zone, the `Remove-AzureRmDnsZone` cmdlet prompts for confirmation if the `$ConfirmPreference` PowerShell variable has any value other than `None`.</span></span>

<span data-ttu-id="a7a3e-153">İçin varsayılan değer itibaren `$ConfirmPreference` olan `High`, yalnızca `Remove-AzureRmDnsZone` varsayılan olarak onaylamanız istenir.</span><span class="sxs-lookup"><span data-stu-id="a7a3e-153">Since the default value for `$ConfirmPreference` is `High`, only `Remove-AzureRmDnsZone` prompts for confirmation by default.</span></span>

<span data-ttu-id="a7a3e-154">Geçerli kılabilirsiniz `$ConfirmPreference` kullanarak ayarlama `-Confirm` parametresi.</span><span class="sxs-lookup"><span data-stu-id="a7a3e-154">You can override the current `$ConfirmPreference` setting using the `-Confirm` parameter.</span></span> <span data-ttu-id="a7a3e-155">Belirtirseniz `-Confirm` veya `-Confirm:$True` , cmdlet sizden onay kendisinden önce çalışır ister.</span><span class="sxs-lookup"><span data-stu-id="a7a3e-155">If you specify `-Confirm` or `-Confirm:$True` , the cmdlet prompts you for confirmation before it runs.</span></span> <span data-ttu-id="a7a3e-156">Belirtirseniz `-Confirm:$False` , cmdlet onaylamanız istenmez.</span><span class="sxs-lookup"><span data-stu-id="a7a3e-156">If you specify `-Confirm:$False` , the cmdlet does not prompt you for confirmation.</span></span>

<span data-ttu-id="a7a3e-157">Hakkında daha fazla bilgi için `-Confirm` ve `$ConfirmPreference`, bkz: [tercih değişkenleri hakkında](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).</span><span class="sxs-lookup"><span data-stu-id="a7a3e-157">For more information about `-Confirm` and `$ConfirmPreference`, see [About Preference Variables](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a7a3e-158">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a7a3e-158">Next steps</span></span>

<span data-ttu-id="a7a3e-159">Bilgi edinmek için nasıl [kayıt kümelerini ve kayıtları yönetmek](dns-operations-recordsets.md) DNS bölgesinde.</span><span class="sxs-lookup"><span data-stu-id="a7a3e-159">Learn how to [manage record sets and records](dns-operations-recordsets.md) in your DNS zone.</span></span>
<br>
<span data-ttu-id="a7a3e-160">Bilgi edinmek için nasıl [etki alanınızı Azure DNS'ye temsilci](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="a7a3e-160">Learn how to [delegate your domain to Azure DNS](dns-domain-delegation.md).</span></span>
<br>
<span data-ttu-id="a7a3e-161">Gözden geçirme [Azure DNS PowerShell başvuru belgeleri](/powershell/module/azurerm.dns).</span><span class="sxs-lookup"><span data-stu-id="a7a3e-161">Review the [Azure DNS PowerShell reference documentation](/powershell/module/azurerm.dns).</span></span>

