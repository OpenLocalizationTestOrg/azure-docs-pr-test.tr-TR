---
title: "aaaManage DNS bölgeleri Azure DNS - Azure CLI 2.0 | Microsoft Docs"
description: "DNS bölgelerini Azure CLI 2.0 kullanarak yönetebilirsiniz. Bu makalede nasıl tooupdate, silme ve Azure DNS üzerinde DNS bölgeleri oluşturma gösterilmektedir."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 8ab63bc4-5135-4ed8-8c0b-5f0712b9afed
ms.service: dns
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/27/2017
ms.author: gwallace
ms.openlocfilehash: 3945a558b2db3490e50678d8395a47e55a85c8fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-in-azure-dns-using-hello-azure-cli-20"></a><span data-ttu-id="d784e-104">Azure DNS kullanarak toomanage DNS bölgeleri Azure CLI 2.0 nasıl hello</span><span class="sxs-lookup"><span data-stu-id="d784e-104">How toomanage DNS Zones in Azure DNS using hello Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="d784e-105">Portal</span><span class="sxs-lookup"><span data-stu-id="d784e-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="d784e-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d784e-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="d784e-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="d784e-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="d784e-108">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="d784e-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)


<span data-ttu-id="d784e-109">Bu kılavuz, Windows, Mac ve Linux için kullanılabilir olduğu hello platformlar arası Azure CLI kullanarak DNS sunucunuzun nasıl toomanage bölgeleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="d784e-109">This guide shows how toomanage your DNS zones by using hello cross-platform Azure CLI, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="d784e-110">DNS bölgelerini kullanarak da yönetebilirsiniz [Azure PowerShell](dns-operations-dnszones.md) ya da Azure portal hello.</span><span class="sxs-lookup"><span data-stu-id="d784e-110">You can also manage your DNS zones using [Azure PowerShell](dns-operations-dnszones.md) or hello Azure portal.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="d784e-111">CLI sürümleri toocomplete hello görevi</span><span class="sxs-lookup"><span data-stu-id="d784e-111">CLI versions toocomplete hello task</span></span>

<span data-ttu-id="d784e-112">CLI sürümleri aşağıdaki hello birini kullanarak hello görevi tamamlamak:</span><span class="sxs-lookup"><span data-stu-id="d784e-112">You can complete hello task using one of hello following CLI versions:</span></span>

* <span data-ttu-id="d784e-113">[Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) -bizim CLI hello Klasik ve kaynak yönetimi dağıtım modelleri için.</span><span class="sxs-lookup"><span data-stu-id="d784e-113">[Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) - our CLI for hello classic and resource management deployment models.</span></span>
* <span data-ttu-id="d784e-114">[Azure CLI 2.0](dns-operations-dnszones-cli.md) -bizim nesil CLI hello kaynak yönetimi dağıtım modeli için.</span><span class="sxs-lookup"><span data-stu-id="d784e-114">[Azure CLI 2.0](dns-operations-dnszones-cli.md) - our next generation CLI for hello resource management deployment model.</span></span>

## <a name="introduction"></a><span data-ttu-id="d784e-115">Giriş</span><span class="sxs-lookup"><span data-stu-id="d784e-115">Introduction</span></span>

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

## <a name="set-up-azure-cli-20-for-azure-dns"></a><span data-ttu-id="d784e-116">Azure DNS için Azure CLI 2.0'ı ayarlama</span><span class="sxs-lookup"><span data-stu-id="d784e-116">Set up Azure CLI 2.0 for Azure DNS</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="d784e-117">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="d784e-117">Before you begin</span></span>

<span data-ttu-id="d784e-118">Yapılandırmanıza başlamadan önce aşağıdaki öğelerindeki hello sahip olduğunuzu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="d784e-118">Verify that you have hello following items before beginning your configuration.</span></span>

* <span data-ttu-id="d784e-119">Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="d784e-119">An Azure subscription.</span></span> <span data-ttu-id="d784e-120">Henüz Azure aboneliğiniz yoksa [MSDN abonelik avantajlarınızı](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) etkinleştirebilir veya [ücretsiz bir hesap](https://azure.microsoft.com/pricing/free-trial/) için kaydolabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d784e-120">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="d784e-121">Merhaba hello Azure CLI 2.0, Windows, Linux veya Mac için kullanılabilir en son sürümünü yükleyin</span><span class="sxs-lookup"><span data-stu-id="d784e-121">Install hello latest version of hello Azure CLI 2.0, available for Windows, Linux, or MAC.</span></span> <span data-ttu-id="d784e-122">Daha fazla bilgi için bkz. [yükleme hello Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="d784e-122">More information is available at [Install hello Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

### <a name="sign-in-tooyour-azure-account"></a><span data-ttu-id="d784e-123">Azure hesabı tooyour içinde oturum</span><span class="sxs-lookup"><span data-stu-id="d784e-123">Sign in tooyour Azure account</span></span>

<span data-ttu-id="d784e-124">Bir konsol penceresi açın ve kimlik bilgilerinizi girerek kimliğinizi doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="d784e-124">Open a console window and authenticate with your credentials.</span></span> <span data-ttu-id="d784e-125">Daha fazla bilgi için bkz: günlük hello Azure CLI gelen tooAzure içinde</span><span class="sxs-lookup"><span data-stu-id="d784e-125">For more information, see Log in tooAzure from hello Azure CLI</span></span>

```
az login
```

### <a name="select-hello-subscription"></a><span data-ttu-id="d784e-126">Merhaba aboneliği seçin</span><span class="sxs-lookup"><span data-stu-id="d784e-126">Select hello subscription</span></span>

<span data-ttu-id="d784e-127">Merhaba hesabının Hello abonelikleri kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="d784e-127">Check hello subscriptions for hello account.</span></span>

```
az account list
```

<span data-ttu-id="d784e-128">Azure abonelikleri toouse hangisinin seçin.</span><span class="sxs-lookup"><span data-stu-id="d784e-128">Choose which of your Azure subscriptions toouse.</span></span>

```azurecli
az account set --subscription "subscription name"
```

### <a name="create-a-resource-group"></a><span data-ttu-id="d784e-129">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="d784e-129">Create a resource group</span></span>

<span data-ttu-id="d784e-130">Azure Resource Manager, tüm kaynak gruplarının bir konum belirtmesini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="d784e-130">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="d784e-131">Bu kaynak grubundaki kaynaklar için hello varsayılan konum olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d784e-131">This is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="d784e-132">Ancak, tüm DNS kaynakları global olduğundan, bölgesel değil, kaynak grubu konumu hello seçimine Azure DNS üzerinde hiçbir etkisi olmaz.</span><span class="sxs-lookup"><span data-stu-id="d784e-132">However, because all DNS resources are global, not regional, hello choice of resource group location has no impact on Azure DNS.</span></span>

<span data-ttu-id="d784e-133">Var olan bir kaynak grubunu kullanıyorsanız bu adımı atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d784e-133">You can skip this step if you are using an existing resource group.</span></span>

```azurecli
az group create --name myresourcegroup --location "West US"
```

## <a name="getting-help"></a><span data-ttu-id="d784e-134">Yardım alma</span><span class="sxs-lookup"><span data-stu-id="d784e-134">Getting help</span></span>

<span data-ttu-id="d784e-135">TooAzure DNS ile ilgili tüm CLI 2.0 komutları başlayın `az network dns`.</span><span class="sxs-lookup"><span data-stu-id="d784e-135">All CLI 2.0 commands relating tooAzure DNS start with `az network dns`.</span></span> <span data-ttu-id="d784e-136">Merhaba kullanan her komut için Yardım kullanılabilir `--help` seçeneği (kısa form `-h`).</span><span class="sxs-lookup"><span data-stu-id="d784e-136">Help is available for each command using hello `--help` option (short form `-h`).</span></span>  <span data-ttu-id="d784e-137">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="d784e-137">For example:</span></span>

```azurecli
az network dns --help
az network dns zone --help
az network dns zone create --help
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="d784e-138">DNS bölgesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="d784e-138">Create a DNS zone</span></span>

<span data-ttu-id="d784e-139">Bir DNS bölgesi hello kullanılarak oluşturulan `az network dns zone create` komutu.</span><span class="sxs-lookup"><span data-stu-id="d784e-139">A DNS zone is created using hello `az network dns zone create` command.</span></span> <span data-ttu-id="d784e-140">Yardım için bkz. `az network dns zone create -h`.</span><span class="sxs-lookup"><span data-stu-id="d784e-140">For help, see `az network dns zone create -h`.</span></span>

<span data-ttu-id="d784e-141">Merhaba aşağıdaki örnek adlı bir DNS bölgesi oluşturur *contoso.com* adlı hello kaynak grubunda *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="d784e-141">hello following example creates a DNS zone called *contoso.com* in hello resource group called *MyResourceGroup*:</span></span>

```azurecli
az network dns zone create --resource-group MyResourceGroup --name contoso.com
```

### <a name="toocreate-a-dns-zone-with-tags"></a><span data-ttu-id="d784e-142">bir DNS bölgesini etiketlerle toocreate</span><span class="sxs-lookup"><span data-stu-id="d784e-142">toocreate a DNS zone with tags</span></span>

<span data-ttu-id="d784e-143">Merhaba aşağıdaki örnekte nasıl toocreate bir DNS bölgesi iki gösterir [Azure Resource Manager etiketlerine](dns-zones-records.md#tags), *proje demo =* ve *env = test*, hello kullanarak `--tags` parametre (kısa form `-t`):</span><span class="sxs-lookup"><span data-stu-id="d784e-143">hello following example shows how toocreate a DNS zone with two [Azure Resource Manager tags](dns-zones-records.md#tags), *project = demo* and *env = test*, by using hello `--tags` parameter (short form `-t`):</span></span>

```azurecli
az network dns zone create --resource-group MyResourceGroup --name contoso.com --tags "project=demo" "env=test"
```

## <a name="get-a-dns-zone"></a><span data-ttu-id="d784e-144">Bir DNS bölgesini alın</span><span class="sxs-lookup"><span data-stu-id="d784e-144">Get a DNS zone</span></span>

<span data-ttu-id="d784e-145">bir DNS bölgesi tooretrieve kullanmak `az network dns zone show`.</span><span class="sxs-lookup"><span data-stu-id="d784e-145">tooretrieve a DNS zone, use `az network dns zone show`.</span></span> <span data-ttu-id="d784e-146">Yardım için bkz. `az network dns zone show --help`.</span><span class="sxs-lookup"><span data-stu-id="d784e-146">For help, see `az network dns zone show --help`.</span></span>

<span data-ttu-id="d784e-147">Merhaba aşağıdaki örnek verir hello DNS bölgesi *contoso.com* ve ilişkili verileri kaynak grubundan *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="d784e-147">hello following example returns hello DNS zone *contoso.com* and its associated data from resource group *MyResourceGroup*.</span></span> 

```azurecli
az network dns zone show --resource-group myresourcegroup --name contoso.com
```

<span data-ttu-id="d784e-148">Aşağıdaki örnek hello hello yanıt ' dir.</span><span class="sxs-lookup"><span data-stu-id="d784e-148">hello following example is hello response.</span></span>

```json
{
  "etag": "00000002-0000-0000-3d4d-64aa3689d201",
  "id": "/subscriptions/147a22e9-2356-4e56-b3de-1f5842ae4a3b/resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com",
  "location": "global",
  "maxNumberOfRecordSets": 5000,
  "name": "contoso.com",
  "nameServers": [
    "ns1-04.azure-dns.com.",
    "ns2-04.azure-dns.net.",
    "ns3-04.azure-dns.org.",
    "ns4-04.azure-dns.info."
  ],
  "numberOfRecordSets": 4,
  "resourceGroup": "myresourcegroup",
  "tags": {},
  "type": "Microsoft.Network/dnszones"
}
```

<span data-ttu-id="d784e-149">DNS kayıtlarını tarafından döndürülen değil Not `az network dns zone show`.</span><span class="sxs-lookup"><span data-stu-id="d784e-149">Note that DNS records are not returned by `az network dns zone show`.</span></span> <span data-ttu-id="d784e-150">toolist DNS kayıtlarını kullanmak `az network dns record-set list`.</span><span class="sxs-lookup"><span data-stu-id="d784e-150">toolist DNS records, use `az network dns record-set list`.</span></span>


## <a name="list-dns-zones"></a><span data-ttu-id="d784e-151">Liste DNS bölgeleri</span><span class="sxs-lookup"><span data-stu-id="d784e-151">List DNS zones</span></span>

<span data-ttu-id="d784e-152">tooenumerate DNS bölgeleri kullanmak `az network dns zone list`.</span><span class="sxs-lookup"><span data-stu-id="d784e-152">tooenumerate DNS zones, use `az network dns zone list`.</span></span> <span data-ttu-id="d784e-153">Yardım için bkz. `az network dns zone list --help`.</span><span class="sxs-lookup"><span data-stu-id="d784e-153">For help, see `az network dns zone list --help`.</span></span>

<span data-ttu-id="d784e-154">Belirten hello kaynak grubu yalnızca hello kaynak grubunda bölgelerini listeler:</span><span class="sxs-lookup"><span data-stu-id="d784e-154">Specifying hello resource group lists only those zones within hello resource group:</span></span>

```azurecli
az network dns zone list --resource-group MyResourceGroup
```

<span data-ttu-id="d784e-155">Atlama hello kaynak grubu hello Abonelikteki tüm bölgeler listeler:</span><span class="sxs-lookup"><span data-stu-id="d784e-155">Omitting hello resource group lists all zones in hello subscription:</span></span>

```azurecli
az network dns zone list 
```

## <a name="update-a-dns-zone"></a><span data-ttu-id="d784e-156">Bir DNS bölgesini güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="d784e-156">Update a DNS zone</span></span>

<span data-ttu-id="d784e-157">DNS bölge kaynak kullanılarak yapılabilir değişiklikleri tooa `az network dns zone update`.</span><span class="sxs-lookup"><span data-stu-id="d784e-157">Changes tooa DNS zone resource can be made using `az network dns zone update`.</span></span> <span data-ttu-id="d784e-158">Yardım için bkz. `az network dns zone update --help`.</span><span class="sxs-lookup"><span data-stu-id="d784e-158">For help, see `az network dns zone update --help`.</span></span>

<span data-ttu-id="d784e-159">Bu komut hello DNS kayıt kümelerini hello bölgedeki hiçbirini güncelleştirmez (bkz [nasıl tooManage DNS kayıtlarını](dns-operations-recordsets-cli.md)).</span><span class="sxs-lookup"><span data-stu-id="d784e-159">This command does not update any of hello DNS record sets within hello zone (see [How tooManage DNS records](dns-operations-recordsets-cli.md)).</span></span> <span data-ttu-id="d784e-160">Yalnızca kullanılan tooupdate özelliklerini hello bölge kaynağını kendisini olur.</span><span class="sxs-lookup"><span data-stu-id="d784e-160">It is only used tooupdate properties of hello zone resource itself.</span></span> <span data-ttu-id="d784e-161">Bu özellikleri şu anda sınırlı toohello olan [Azure Resource Manager 'etiketleri'](dns-zones-records.md#tags) hello bölge kaynak için.</span><span class="sxs-lookup"><span data-stu-id="d784e-161">These properties are currently limited toohello [Azure Resource Manager 'tags'](dns-zones-records.md#tags) for hello zone resource.</span></span>

<span data-ttu-id="d784e-162">Merhaba aşağıdaki örnek bir DNS bölgesinin nasıl tooupdate hello etiketleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="d784e-162">hello following example shows how tooupdate hello tags on a DNS zone.</span></span> <span data-ttu-id="d784e-163">Merhaba varolan etiketleri belirtilen hello değeriyle değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="d784e-163">hello existing tags are replaced by hello value specified.</span></span>

```azurecli
az network dns zone update --resource-group myresourcegroup --name contoso.com --set tags.team=support
```

## <a name="delete-a-dns-zone"></a><span data-ttu-id="d784e-164">Bir DNS bölgesi Sil</span><span class="sxs-lookup"><span data-stu-id="d784e-164">Delete a DNS zone</span></span>

<span data-ttu-id="d784e-165">DNS bölgeleri kullanılarak silinebilir `az network dns zone delete`.</span><span class="sxs-lookup"><span data-stu-id="d784e-165">DNS zones can be deleted using `az network dns zone delete`.</span></span> <span data-ttu-id="d784e-166">Yardım için bkz. `az network dns zone delete --help`.</span><span class="sxs-lookup"><span data-stu-id="d784e-166">For help, see `az network dns zone delete --help`.</span></span>

> [!NOTE]
> <span data-ttu-id="d784e-167">Bir DNS bölgesi silme hello bölgedeki tüm DNS kayıtlarını siler.</span><span class="sxs-lookup"><span data-stu-id="d784e-167">Deleting a DNS zone also deletes all DNS records within hello zone.</span></span> <span data-ttu-id="d784e-168">Bu işlem geri alınamaz.</span><span class="sxs-lookup"><span data-stu-id="d784e-168">This operation cannot be undone.</span></span> <span data-ttu-id="d784e-169">Merhaba DNS bölgesi kullanımdaysa hello bölge silindiğinde hello bölge kullanarak Hizmetleri başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="d784e-169">If hello DNS zone is in use, services using hello zone will fail when hello zone is deleted.</span></span>
>
><span data-ttu-id="d784e-170">yanlışlıkla bölge silinmesine karşı tooprotect bkz [nasıl tooprotect DNS bölgeleri ve kayıtları](dns-protect-zones-recordsets.md).</span><span class="sxs-lookup"><span data-stu-id="d784e-170">tooprotect against accidental zone deletion, see [How tooprotect DNS zones and records](dns-protect-zones-recordsets.md).</span></span>

<span data-ttu-id="d784e-171">Bu komut onaylamanızı ister.</span><span class="sxs-lookup"><span data-stu-id="d784e-171">This command prompts for confirmation.</span></span> <span data-ttu-id="d784e-172">İsteğe bağlı Hello `--yes` anahtar bu istemi gizler.</span><span class="sxs-lookup"><span data-stu-id="d784e-172">hello optional `--yes` switch suppresses this prompt.</span></span>

<span data-ttu-id="d784e-173">Merhaba aşağıdaki örnekte nasıl toodelete hello bölge gösterir *contoso.com* kaynak grubundan *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="d784e-173">hello following example shows how toodelete hello zone *contoso.com* from resource group *MyResourceGroup*.</span></span>

```azurecli
az network dns zone delete --resource-group myresourcegroup --name contoso.com
```

## <a name="next-steps"></a><span data-ttu-id="d784e-174">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d784e-174">Next steps</span></span>

<span data-ttu-id="d784e-175">Nasıl çok öğrenin[kayıt kümelerini ve kayıtları yönetmek](dns-getstarted-create-recordset-cli.md) DNS bölgesinde.</span><span class="sxs-lookup"><span data-stu-id="d784e-175">Learn how too[manage record sets and records](dns-getstarted-create-recordset-cli.md) in your DNS zone.</span></span>

<span data-ttu-id="d784e-176">Nasıl çok öğrenin[, etki alanı tooAzure DNS temsilci](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="d784e-176">Learn how too[delegate your domain tooAzure DNS](dns-domain-delegation.md).</span></span>

