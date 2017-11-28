---
title: "aaaManage DNS bölgeleri Azure DNS - Azure CLI 1.0 | Microsoft Docs"
description: "DNS bölgelerini Azure CLI 1.0 kullanarak yönetebilirsiniz. Bu makalede nasıl tooupdate, silme ve Azure DNS üzerinde DNS bölgeleri oluşturma gösterilmektedir."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 8ab63bc4-5135-4ed8-8c0b-5f0712b9afed
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/21/2016
ms.author: gwallace
ms.openlocfilehash: cb9790cc46626ef7f38a43edb57511104fe6057e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-in-azure-dns-using-hello-azure-cli-10"></a><span data-ttu-id="0fa19-104">Azure DNS kullanarak toomanage DNS bölgeleri Azure CLI 1.0 nasıl hello</span><span class="sxs-lookup"><span data-stu-id="0fa19-104">How toomanage DNS Zones in Azure DNS using hello Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="0fa19-105">Portal</span><span class="sxs-lookup"><span data-stu-id="0fa19-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="0fa19-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0fa19-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="0fa19-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="0fa19-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="0fa19-108">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="0fa19-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)

<span data-ttu-id="0fa19-109">Bu kılavuz, nasıl toomanage hello platformlar arası Azure CLI 1.0, Windows, Mac ve Linux için kullanılabilir olduğu kullanarak DNS bölgeleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="0fa19-109">This guide shows how toomanage your DNS zones by using hello cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="0fa19-110">DNS bölgelerini kullanarak da yönetebilirsiniz [Azure PowerShell](dns-operations-dnszones.md) ya da Azure portal hello.</span><span class="sxs-lookup"><span data-stu-id="0fa19-110">You can also manage your DNS zones using [Azure PowerShell](dns-operations-dnszones.md) or hello Azure portal.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="0fa19-111">CLI sürümleri toocomplete hello görevi</span><span class="sxs-lookup"><span data-stu-id="0fa19-111">CLI versions toocomplete hello task</span></span>

<span data-ttu-id="0fa19-112">CLI sürümleri aşağıdaki hello birini kullanarak hello görevi tamamlamak:</span><span class="sxs-lookup"><span data-stu-id="0fa19-112">You can complete hello task using one of hello following CLI versions:</span></span>

* <span data-ttu-id="0fa19-113">[Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) -bizim CLI hello Klasik ve kaynak yönetimi dağıtım modelleri için.</span><span class="sxs-lookup"><span data-stu-id="0fa19-113">[Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) - our CLI for hello classic and resource management deployment models.</span></span>
* <span data-ttu-id="0fa19-114">[Azure CLI 2.0](dns-operations-dnszones-cli.md) -bizim nesil CLI hello kaynak yönetimi dağıtım modeli için.</span><span class="sxs-lookup"><span data-stu-id="0fa19-114">[Azure CLI 2.0](dns-operations-dnszones-cli.md) - our next generation CLI for hello resource management deployment model.</span></span>

## <a name="introduction"></a><span data-ttu-id="0fa19-115">Giriş</span><span class="sxs-lookup"><span data-stu-id="0fa19-115">Introduction</span></span>

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

[!INCLUDE [dns-cli-setup](../../includes/dns-cli-setup-include.md)]

## <a name="getting-help"></a><span data-ttu-id="0fa19-116">Yardım alma</span><span class="sxs-lookup"><span data-stu-id="0fa19-116">Getting help</span></span>

<span data-ttu-id="0fa19-117">TooAzure DNS ile ilgili tüm CLI 1.0 komutları başlayın `azure network dns`.</span><span class="sxs-lookup"><span data-stu-id="0fa19-117">All CLI 1.0 commands relating tooAzure DNS start with `azure network dns`.</span></span> <span data-ttu-id="0fa19-118">Merhaba kullanan her komut için Yardım kullanılabilir `--help` seçeneği (kısa form `-h`).</span><span class="sxs-lookup"><span data-stu-id="0fa19-118">Help is available for each command using hello `--help` option (short form `-h`).</span></span>  <span data-ttu-id="0fa19-119">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="0fa19-119">For example:</span></span>

```azurecli
azure network dns -h
azure network dns zone -h
azure network dns zone create -h
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="0fa19-120">DNS bölgesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="0fa19-120">Create a DNS zone</span></span>

<span data-ttu-id="0fa19-121">Bir DNS bölgesi hello kullanılarak oluşturulan `azure network dns zone create` komutu.</span><span class="sxs-lookup"><span data-stu-id="0fa19-121">A DNS zone is created using hello `azure network dns zone create` command.</span></span> <span data-ttu-id="0fa19-122">Yardım için bkz. `azure network dns zone create -h`.</span><span class="sxs-lookup"><span data-stu-id="0fa19-122">For help, see `azure network dns zone create -h`.</span></span>

<span data-ttu-id="0fa19-123">Merhaba aşağıdaki örnek adlı bir DNS bölgesi oluşturur *contoso.com* adlı hello kaynak grubunda *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="0fa19-123">hello following example creates a DNS zone called *contoso.com* in hello resource group called *MyResourceGroup*:</span></span>

```azurecli
azure network dns zone create MyResourceGroup contoso.com
```

### <a name="toocreate-a-dns-zone-with-tags"></a><span data-ttu-id="0fa19-124">bir DNS bölgesini etiketlerle toocreate</span><span class="sxs-lookup"><span data-stu-id="0fa19-124">toocreate a DNS zone with tags</span></span>

<span data-ttu-id="0fa19-125">Merhaba aşağıdaki örnekte nasıl toocreate bir DNS bölgesi iki gösterir [Azure Resource Manager etiketlerine](dns-zones-records.md#tags), *proje demo =* ve *env = test*, hello kullanarak `--tags` parametre (kısa form `-t`):</span><span class="sxs-lookup"><span data-stu-id="0fa19-125">hello following example shows how toocreate a DNS zone with two [Azure Resource Manager tags](dns-zones-records.md#tags), *project = demo* and *env = test*, by using hello `--tags` parameter (short form `-t`):</span></span>

```azurecli
azure network dns zone create MyResourceGroup contoso.com -t "project=demo";"env=test"
```

## <a name="get-a-dns-zone"></a><span data-ttu-id="0fa19-126">Bir DNS bölgesini alın</span><span class="sxs-lookup"><span data-stu-id="0fa19-126">Get a DNS zone</span></span>

<span data-ttu-id="0fa19-127">bir DNS bölgesi tooretrieve kullanmak `azure network dns zone show`.</span><span class="sxs-lookup"><span data-stu-id="0fa19-127">tooretrieve a DNS zone, use `azure network dns zone show`.</span></span> <span data-ttu-id="0fa19-128">Yardım için bkz. `azure network dns zone show -h`.</span><span class="sxs-lookup"><span data-stu-id="0fa19-128">For help, see `azure network dns zone show -h`.</span></span>

<span data-ttu-id="0fa19-129">Merhaba aşağıdaki örnek verir hello DNS bölgesi *contoso.com* ve ilişkili verileri kaynak grubundan *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="0fa19-129">hello following example returns hello DNS zone *contoso.com* and its associated data from resource group *MyResourceGroup*.</span></span> 

```azurecli
azure network dns zone show MyResourceGroup contoso.com
```

<span data-ttu-id="0fa19-130">Aşağıdaki örnek hello hello yanıt ' dir.</span><span class="sxs-lookup"><span data-stu-id="0fa19-130">hello following example is hello response.</span></span>

```
info:    Executing command network dns zone show
+ Looking up hello dns zone "contoso.com"
data:    Id                              : /subscriptions/.../contoso.com
data:    Name                            : contoso.com
data:    Type                            : Microsoft.Network/dnszones
data:    Location                        : global
data:    Number of record sets           : 2
data:    Max number of record sets       : 5000
data:    Name servers:
data:        ns1-01.azure-dns.com.
data:        ns2-01.azure-dns.net.
data:        ns3-01.azure-dns.org.
data:        ns4-01.azure-dns.info.
data:    Tags                            : project=demo;env=test
info:    network dns zone show command OK
```

<span data-ttu-id="0fa19-131">DNS kayıtlarını tarafından döndürülen değil Not `azure network dns zone show`.</span><span class="sxs-lookup"><span data-stu-id="0fa19-131">Note that DNS records are not returned by `azure network dns zone show`.</span></span> <span data-ttu-id="0fa19-132">toolist DNS kayıtlarını kullanmak `azure network dns record-set list`.</span><span class="sxs-lookup"><span data-stu-id="0fa19-132">toolist DNS records, use `azure network dns record-set list`.</span></span>


## <a name="list-dns-zones"></a><span data-ttu-id="0fa19-133">Liste DNS bölgeleri</span><span class="sxs-lookup"><span data-stu-id="0fa19-133">List DNS zones</span></span>

<span data-ttu-id="0fa19-134">tooenumerate DNS bölgeleri kullanmak `azure network dns zone list`.</span><span class="sxs-lookup"><span data-stu-id="0fa19-134">tooenumerate DNS zones, use `azure network dns zone list`.</span></span> <span data-ttu-id="0fa19-135">Yardım için bkz. `azure network dns zone list -h`.</span><span class="sxs-lookup"><span data-stu-id="0fa19-135">For help, see `azure network dns zone list -h`.</span></span>

<span data-ttu-id="0fa19-136">Belirten hello kaynak grubu yalnızca hello kaynak grubunda bölgelerini listeler:</span><span class="sxs-lookup"><span data-stu-id="0fa19-136">Specifying hello resource group lists only those zones within hello resource group:</span></span>

```azurecli
azure network dns zone list MyResourceGroup
```

<span data-ttu-id="0fa19-137">Atlama hello kaynak grubu hello Abonelikteki tüm bölgeler listeler:</span><span class="sxs-lookup"><span data-stu-id="0fa19-137">Omitting hello resource group lists all zones in hello subscription:</span></span>

```azurecli
azure network dns zone list 
```

## <a name="update-a-dns-zone"></a><span data-ttu-id="0fa19-138">Bir DNS bölgesini güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="0fa19-138">Update a DNS zone</span></span>

<span data-ttu-id="0fa19-139">DNS bölge kaynak kullanılarak yapılabilir değişiklikleri tooa `azure network dns zone set`.</span><span class="sxs-lookup"><span data-stu-id="0fa19-139">Changes tooa DNS zone resource can be made using `azure network dns zone set`.</span></span> <span data-ttu-id="0fa19-140">Yardım için bkz. `azure network dns zone set -h`.</span><span class="sxs-lookup"><span data-stu-id="0fa19-140">For help, see `azure network dns zone set -h`.</span></span>

<span data-ttu-id="0fa19-141">Bu komut hello DNS kayıt kümelerini hello bölgedeki hiçbirini güncelleştirmez (bkz [nasıl tooManage DNS kayıtlarını](dns-operations-recordsets-cli-nodejs.md)).</span><span class="sxs-lookup"><span data-stu-id="0fa19-141">This command does not update any of hello DNS record sets within hello zone (see [How tooManage DNS records](dns-operations-recordsets-cli-nodejs.md)).</span></span> <span data-ttu-id="0fa19-142">Yalnızca kullanılan tooupdate özelliklerini hello bölge kaynağını kendisini olur.</span><span class="sxs-lookup"><span data-stu-id="0fa19-142">It is only used tooupdate properties of hello zone resource itself.</span></span> <span data-ttu-id="0fa19-143">Bu özellikleri şu anda sınırlı toohello olan [Azure Resource Manager 'etiketleri'](dns-zones-records.md#tags) hello bölge kaynak için.</span><span class="sxs-lookup"><span data-stu-id="0fa19-143">These properties are currently limited toohello [Azure Resource Manager 'tags'](dns-zones-records.md#tags) for hello zone resource.</span></span>

<span data-ttu-id="0fa19-144">Merhaba aşağıdaki örnek bir DNS bölgesinin nasıl tooupdate hello etiketleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="0fa19-144">hello following example shows how tooupdate hello tags on a DNS zone.</span></span> <span data-ttu-id="0fa19-145">Merhaba varolan etiketleri belirtilen hello değeriyle değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="0fa19-145">hello existing tags are replaced by hello value specified.</span></span>

```azurecli
azure network dns zone set MyResourceGroup contoso.com -t "team=support"
```

## <a name="delete-a-dns-zone"></a><span data-ttu-id="0fa19-146">Bir DNS bölgesi Sil</span><span class="sxs-lookup"><span data-stu-id="0fa19-146">Delete a DNS Zone</span></span>

<span data-ttu-id="0fa19-147">DNS bölgeleri kullanılarak silinebilir `azure network dns zone delete`.</span><span class="sxs-lookup"><span data-stu-id="0fa19-147">DNS zones can be deleted using `azure network dns zone delete`.</span></span> <span data-ttu-id="0fa19-148">Yardım için bkz. `azure network dns zone delete -h`.</span><span class="sxs-lookup"><span data-stu-id="0fa19-148">For help, see `azure network dns zone delete -h`.</span></span>

> [!NOTE]
> <span data-ttu-id="0fa19-149">Bir DNS bölgesi silme hello bölgedeki tüm DNS kayıtlarını siler.</span><span class="sxs-lookup"><span data-stu-id="0fa19-149">Deleting a DNS zone also deletes all DNS records within hello zone.</span></span> <span data-ttu-id="0fa19-150">Bu işlem geri alınamaz.</span><span class="sxs-lookup"><span data-stu-id="0fa19-150">This operation cannot be undone.</span></span> <span data-ttu-id="0fa19-151">Merhaba DNS bölgesi kullanımdaysa hello bölge silindiğinde hello bölge kullanarak Hizmetleri başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="0fa19-151">If hello DNS zone is in use, services using hello zone will fail when hello zone is deleted.</span></span>
>
><span data-ttu-id="0fa19-152">yanlışlıkla bölge silinmesine karşı tooprotect bkz [nasıl tooprotect DNS bölgeleri ve kayıtları](dns-protect-zones-recordsets.md).</span><span class="sxs-lookup"><span data-stu-id="0fa19-152">tooprotect against accidental zone deletion, see [How tooprotect DNS zones and records](dns-protect-zones-recordsets.md).</span></span>

<span data-ttu-id="0fa19-153">Bu komut onaylamanızı ister.</span><span class="sxs-lookup"><span data-stu-id="0fa19-153">This command prompts for confirmation.</span></span> <span data-ttu-id="0fa19-154">İsteğe bağlı Hello `--quiet` geçiş (kısa form `-q`) bu istemi gizler.</span><span class="sxs-lookup"><span data-stu-id="0fa19-154">hello optional `--quiet` switch (short form `-q`) suppresses this prompt.</span></span>

<span data-ttu-id="0fa19-155">Merhaba aşağıdaki örnekte nasıl toodelete hello bölge gösterir *contoso.com* kaynak grubundan *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="0fa19-155">hello following example shows how toodelete hello zone *contoso.com* from resource group *MyResourceGroup*.</span></span>

```azurecli
azure network dns zone delete MyResourceGroup contoso.com
```

## <a name="next-steps"></a><span data-ttu-id="0fa19-156">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0fa19-156">Next steps</span></span>

<span data-ttu-id="0fa19-157">Nasıl çok öğrenin[kayıt kümelerini ve kayıtları yönetmek](dns-getstarted-create-recordset-cli-nodejs.md) DNS bölgesinde.</span><span class="sxs-lookup"><span data-stu-id="0fa19-157">Learn how too[manage record sets and records](dns-getstarted-create-recordset-cli-nodejs.md) in your DNS zone.</span></span>

<span data-ttu-id="0fa19-158">Nasıl çok öğrenin[, etki alanı tooAzure DNS temsilci](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="0fa19-158">Learn how too[delegate your domain tooAzure DNS](dns-domain-delegation.md).</span></span>

