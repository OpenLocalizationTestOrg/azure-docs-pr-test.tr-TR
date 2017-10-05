---
title: "Azure DNS'de - Azure CLI 2.0 DNS bölgelerini yönetme | Microsoft Docs"
description: "DNS bölgelerini Azure CLI 2.0 kullanarak yönetebilirsiniz. Bu makalede, güncelleştirme, silme ve Azure DNS üzerinde DNS bölgeleri oluşturma gösterilmektedir."
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
ms.openlocfilehash: 1414baf9e51d648cc3a46c4f8635040b4d276910
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-dns-zones-in-azure-dns-using-the-azure-cli-20"></a><span data-ttu-id="14961-104">Azure CLI 2.0 kullanan Azure DNS'de DNS bölgelerini yönetme</span><span class="sxs-lookup"><span data-stu-id="14961-104">How to manage DNS Zones in Azure DNS using the Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="14961-105">Portal</span><span class="sxs-lookup"><span data-stu-id="14961-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="14961-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="14961-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="14961-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="14961-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="14961-108">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="14961-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)


<span data-ttu-id="14961-109">Bu kılavuz, Windows, Mac ve Linux için kullanılabilir olduğu platformlar arası Azure CLI kullanarak DNS bölgelerini yönetme gösterir.</span><span class="sxs-lookup"><span data-stu-id="14961-109">This guide shows how to manage your DNS zones by using the cross-platform Azure CLI, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="14961-110">DNS bölgelerini kullanarak da yönetebilirsiniz [Azure PowerShell](dns-operations-dnszones.md) ya da Azure portal.</span><span class="sxs-lookup"><span data-stu-id="14961-110">You can also manage your DNS zones using [Azure PowerShell](dns-operations-dnszones.md) or the Azure portal.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="14961-111">Görevi tamamlamak için kullanılacak CLI sürümleri</span><span class="sxs-lookup"><span data-stu-id="14961-111">CLI versions to complete the task</span></span>

<span data-ttu-id="14961-112">Görevi aşağıdaki CLI sürümlerinden birini kullanarak tamamlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="14961-112">You can complete the task using one of the following CLI versions:</span></span>

* <span data-ttu-id="14961-113">[Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md): Klasik ve kaynak yönetimi dağıtım modellerine yönelik CLI'mız.</span><span class="sxs-lookup"><span data-stu-id="14961-113">[Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) - our CLI for the classic and resource management deployment models.</span></span>
* <span data-ttu-id="14961-114">[Azure CLI 2.0](dns-operations-dnszones-cli.md): Kaynak yönetimi dağıtım modeline yönelik yeni nesil CLI'mız.</span><span class="sxs-lookup"><span data-stu-id="14961-114">[Azure CLI 2.0](dns-operations-dnszones-cli.md) - our next generation CLI for the resource management deployment model.</span></span>

## <a name="introduction"></a><span data-ttu-id="14961-115">Giriş</span><span class="sxs-lookup"><span data-stu-id="14961-115">Introduction</span></span>

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

## <a name="set-up-azure-cli-20-for-azure-dns"></a><span data-ttu-id="14961-116">Azure DNS için Azure CLI 2.0'ı ayarlama</span><span class="sxs-lookup"><span data-stu-id="14961-116">Set up Azure CLI 2.0 for Azure DNS</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="14961-117">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="14961-117">Before you begin</span></span>

<span data-ttu-id="14961-118">Yapılandırmanıza başlamadan önce aşağıdaki öğelerin bulunduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="14961-118">Verify that you have the following items before beginning your configuration.</span></span>

* <span data-ttu-id="14961-119">Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="14961-119">An Azure subscription.</span></span> <span data-ttu-id="14961-120">Henüz Azure aboneliğiniz yoksa [MSDN abonelik avantajlarınızı](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) etkinleştirebilir veya [ücretsiz bir hesap](https://azure.microsoft.com/pricing/free-trial/) için kaydolabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="14961-120">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="14961-121">Azure CLI 2.0, Windows, Linux veya Mac için kullanılabilir en son sürümünü yükleyin</span><span class="sxs-lookup"><span data-stu-id="14961-121">Install the latest version of the Azure CLI 2.0, available for Windows, Linux, or MAC.</span></span> <span data-ttu-id="14961-122">Daha fazla bilgi için bkz. [Azure CLI 2.0'ı yükleme](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="14961-122">More information is available at [Install the Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

### <a name="sign-in-to-your-azure-account"></a><span data-ttu-id="14961-123">Azure hesabınızda oturum açma</span><span class="sxs-lookup"><span data-stu-id="14961-123">Sign in to your Azure account</span></span>

<span data-ttu-id="14961-124">Bir konsol penceresi açın ve kimlik bilgilerinizi girerek kimliğinizi doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="14961-124">Open a console window and authenticate with your credentials.</span></span> <span data-ttu-id="14961-125">Daha fazla bilgi için bkz. Azure CLI üzerinden Azure'da oturum açma</span><span class="sxs-lookup"><span data-stu-id="14961-125">For more information, see Log in to Azure from the Azure CLI</span></span>

```
az login
```

### <a name="select-the-subscription"></a><span data-ttu-id="14961-126">Aboneliği seçme</span><span class="sxs-lookup"><span data-stu-id="14961-126">Select the subscription</span></span>

<span data-ttu-id="14961-127">Hesapla ilişkili abonelikleri kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="14961-127">Check the subscriptions for the account.</span></span>

```
az account list
```

<span data-ttu-id="14961-128">Hangi Azure aboneliğinizin kullanılacağını seçin.</span><span class="sxs-lookup"><span data-stu-id="14961-128">Choose which of your Azure subscriptions to use.</span></span>

```azurecli
az account set --subscription "subscription name"
```

### <a name="create-a-resource-group"></a><span data-ttu-id="14961-129">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="14961-129">Create a resource group</span></span>

<span data-ttu-id="14961-130">Azure Resource Manager, tüm kaynak gruplarının bir konum belirtmesini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="14961-130">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="14961-131">Bu, kaynak grubunda kaynaklar için varsayılan konum olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="14961-131">This is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="14961-132">Ancak tüm DNS kaynakları bölgesel değil de global olduğundan, kaynak grubu konumu seçiminin Azure DNS üzerinde hiçbir etkisi yoktur.</span><span class="sxs-lookup"><span data-stu-id="14961-132">However, because all DNS resources are global, not regional, the choice of resource group location has no impact on Azure DNS.</span></span>

<span data-ttu-id="14961-133">Var olan bir kaynak grubunu kullanıyorsanız bu adımı atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="14961-133">You can skip this step if you are using an existing resource group.</span></span>

```azurecli
az group create --name myresourcegroup --location "West US"
```

## <a name="getting-help"></a><span data-ttu-id="14961-134">Yardım alma</span><span class="sxs-lookup"><span data-stu-id="14961-134">Getting help</span></span>

<span data-ttu-id="14961-135">Azure DNS ile ilgili tüm CLI 2.0 komutları başlayın `az network dns`.</span><span class="sxs-lookup"><span data-stu-id="14961-135">All CLI 2.0 commands relating to Azure DNS start with `az network dns`.</span></span> <span data-ttu-id="14961-136">Yardım her komutu kullanmak için mevcut `--help` seçeneği (kısa form `-h`).</span><span class="sxs-lookup"><span data-stu-id="14961-136">Help is available for each command using the `--help` option (short form `-h`).</span></span>  <span data-ttu-id="14961-137">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="14961-137">For example:</span></span>

```azurecli
az network dns --help
az network dns zone --help
az network dns zone create --help
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="14961-138">DNS bölgesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="14961-138">Create a DNS zone</span></span>

<span data-ttu-id="14961-139">DNS bölgesi, `az network dns zone create` komutu kullanılarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="14961-139">A DNS zone is created using the `az network dns zone create` command.</span></span> <span data-ttu-id="14961-140">Yardım için bkz. `az network dns zone create -h`.</span><span class="sxs-lookup"><span data-stu-id="14961-140">For help, see `az network dns zone create -h`.</span></span>

<span data-ttu-id="14961-141">Aşağıdaki örnek adlı bir DNS bölgesi oluşturur *contoso.com* kaynak grubunda *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="14961-141">The following example creates a DNS zone called *contoso.com* in the resource group called *MyResourceGroup*:</span></span>

```azurecli
az network dns zone create --resource-group MyResourceGroup --name contoso.com
```

### <a name="to-create-a-dns-zone-with-tags"></a><span data-ttu-id="14961-142">Etiketle bir DNS bölgesi oluşturmak için</span><span class="sxs-lookup"><span data-stu-id="14961-142">To create a DNS zone with tags</span></span>

<span data-ttu-id="14961-143">Aşağıdaki örnekte, iki DNS bölgesi oluşturmak gösterilmiştir [Azure Resource Manager etiketlerine](dns-zones-records.md#tags), *proje demo =* ve *env = test*, kullanarak `--tags` parametre (kısa form `-t`):</span><span class="sxs-lookup"><span data-stu-id="14961-143">The following example shows how to create a DNS zone with two [Azure Resource Manager tags](dns-zones-records.md#tags), *project = demo* and *env = test*, by using the `--tags` parameter (short form `-t`):</span></span>

```azurecli
az network dns zone create --resource-group MyResourceGroup --name contoso.com --tags "project=demo" "env=test"
```

## <a name="get-a-dns-zone"></a><span data-ttu-id="14961-144">Bir DNS bölgesini alın</span><span class="sxs-lookup"><span data-stu-id="14961-144">Get a DNS zone</span></span>

<span data-ttu-id="14961-145">Bir DNS bölgesi almak kullanın `az network dns zone show`.</span><span class="sxs-lookup"><span data-stu-id="14961-145">To retrieve a DNS zone, use `az network dns zone show`.</span></span> <span data-ttu-id="14961-146">Yardım için bkz. `az network dns zone show --help`.</span><span class="sxs-lookup"><span data-stu-id="14961-146">For help, see `az network dns zone show --help`.</span></span>

<span data-ttu-id="14961-147">Aşağıdaki örnek DNS bölgesi verir *contoso.com* ve ilişkili verileri kaynak grubundan *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="14961-147">The following example returns the DNS zone *contoso.com* and its associated data from resource group *MyResourceGroup*.</span></span> 

```azurecli
az network dns zone show --resource-group myresourcegroup --name contoso.com
```

<span data-ttu-id="14961-148">Aşağıdaki örnek, yanıttır.</span><span class="sxs-lookup"><span data-stu-id="14961-148">The following example is the response.</span></span>

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

<span data-ttu-id="14961-149">DNS kayıtlarını tarafından döndürülen değil Not `az network dns zone show`.</span><span class="sxs-lookup"><span data-stu-id="14961-149">Note that DNS records are not returned by `az network dns zone show`.</span></span> <span data-ttu-id="14961-150">DNS kayıtlarını listesinde, kullanmak için `az network dns record-set list`.</span><span class="sxs-lookup"><span data-stu-id="14961-150">To list DNS records, use `az network dns record-set list`.</span></span>


## <a name="list-dns-zones"></a><span data-ttu-id="14961-151">Liste DNS bölgeleri</span><span class="sxs-lookup"><span data-stu-id="14961-151">List DNS zones</span></span>

<span data-ttu-id="14961-152">DNS bölgelerini numaralandırmak için kullanmanız `az network dns zone list`.</span><span class="sxs-lookup"><span data-stu-id="14961-152">To enumerate DNS zones, use `az network dns zone list`.</span></span> <span data-ttu-id="14961-153">Yardım için bkz. `az network dns zone list --help`.</span><span class="sxs-lookup"><span data-stu-id="14961-153">For help, see `az network dns zone list --help`.</span></span>

<span data-ttu-id="14961-154">Kaynak grubu belirterek yalnızca kaynak grubunda bölgelerini listeler:</span><span class="sxs-lookup"><span data-stu-id="14961-154">Specifying the resource group lists only those zones within the resource group:</span></span>

```azurecli
az network dns zone list --resource-group MyResourceGroup
```

<span data-ttu-id="14961-155">Kaynak grubu atlama Abonelikteki tüm bölgeler listeler:</span><span class="sxs-lookup"><span data-stu-id="14961-155">Omitting the resource group lists all zones in the subscription:</span></span>

```azurecli
az network dns zone list 
```

## <a name="update-a-dns-zone"></a><span data-ttu-id="14961-156">Bir DNS bölgesini güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="14961-156">Update a DNS zone</span></span>

<span data-ttu-id="14961-157">Kullanarak bir DNS bölgesi kaynak değişiklikler yapılabilir `az network dns zone update`.</span><span class="sxs-lookup"><span data-stu-id="14961-157">Changes to a DNS zone resource can be made using `az network dns zone update`.</span></span> <span data-ttu-id="14961-158">Yardım için bkz. `az network dns zone update --help`.</span><span class="sxs-lookup"><span data-stu-id="14961-158">For help, see `az network dns zone update --help`.</span></span>

<span data-ttu-id="14961-159">Bu komut bölge içinde DNS kayıt kümelerini hiçbirini güncelleştirmez (bkz [yönetmek DNS kayıtlarını nasıl](dns-operations-recordsets-cli.md)).</span><span class="sxs-lookup"><span data-stu-id="14961-159">This command does not update any of the DNS record sets within the zone (see [How to Manage DNS records](dns-operations-recordsets-cli.md)).</span></span> <span data-ttu-id="14961-160">Yalnızca, bölge kaynak özelliklerini güncelleştirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="14961-160">It is only used to update properties of the zone resource itself.</span></span> <span data-ttu-id="14961-161">Bu özellikleri şu anda sınırlı [Azure Resource Manager 'etiketleri'](dns-zones-records.md#tags) bölge kaynak için.</span><span class="sxs-lookup"><span data-stu-id="14961-161">These properties are currently limited to the [Azure Resource Manager 'tags'](dns-zones-records.md#tags) for the zone resource.</span></span>

<span data-ttu-id="14961-162">Aşağıdaki örnek, bir DNS bölgesi etiketleri güncelleştirmek gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="14961-162">The following example shows how to update the tags on a DNS zone.</span></span> <span data-ttu-id="14961-163">Varolan etiketleri belirtilen değeriyle değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="14961-163">The existing tags are replaced by the value specified.</span></span>

```azurecli
az network dns zone update --resource-group myresourcegroup --name contoso.com --set tags.team=support
```

## <a name="delete-a-dns-zone"></a><span data-ttu-id="14961-164">Bir DNS bölgesi Sil</span><span class="sxs-lookup"><span data-stu-id="14961-164">Delete a DNS zone</span></span>

<span data-ttu-id="14961-165">DNS bölgeleri kullanılarak silinebilir `az network dns zone delete`.</span><span class="sxs-lookup"><span data-stu-id="14961-165">DNS zones can be deleted using `az network dns zone delete`.</span></span> <span data-ttu-id="14961-166">Yardım için bkz. `az network dns zone delete --help`.</span><span class="sxs-lookup"><span data-stu-id="14961-166">For help, see `az network dns zone delete --help`.</span></span>

> [!NOTE]
> <span data-ttu-id="14961-167">Bir DNS bölgesi silme bölgedeki tüm DNS kayıtlarını siler.</span><span class="sxs-lookup"><span data-stu-id="14961-167">Deleting a DNS zone also deletes all DNS records within the zone.</span></span> <span data-ttu-id="14961-168">Bu işlem geri alınamaz.</span><span class="sxs-lookup"><span data-stu-id="14961-168">This operation cannot be undone.</span></span> <span data-ttu-id="14961-169">DNS bölgesi kullanımdaysa, bölge silindiğinde bölge kullanarak Hizmetleri başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="14961-169">If the DNS zone is in use, services using the zone will fail when the zone is deleted.</span></span>
>
><span data-ttu-id="14961-170">Yanlışlıkla bölge silinmeye karşı korumak için bkz: [DNS bölgeleri ve kayıtları korumak nasıl](dns-protect-zones-recordsets.md).</span><span class="sxs-lookup"><span data-stu-id="14961-170">To protect against accidental zone deletion, see [How to protect DNS zones and records](dns-protect-zones-recordsets.md).</span></span>

<span data-ttu-id="14961-171">Bu komut onaylamanızı ister.</span><span class="sxs-lookup"><span data-stu-id="14961-171">This command prompts for confirmation.</span></span> <span data-ttu-id="14961-172">İsteğe bağlı `--yes` anahtar bu istemi gizler.</span><span class="sxs-lookup"><span data-stu-id="14961-172">The optional `--yes` switch suppresses this prompt.</span></span>

<span data-ttu-id="14961-173">Aşağıdaki örnekte, bölgenin silmek gösterilmiştir *contoso.com* kaynak grubundan *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="14961-173">The following example shows how to delete the zone *contoso.com* from resource group *MyResourceGroup*.</span></span>

```azurecli
az network dns zone delete --resource-group myresourcegroup --name contoso.com
```

## <a name="next-steps"></a><span data-ttu-id="14961-174">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="14961-174">Next steps</span></span>

<span data-ttu-id="14961-175">Bilgi edinmek için nasıl [kayıt kümelerini ve kayıtları yönetmek](dns-getstarted-create-recordset-cli.md) DNS bölgesinde.</span><span class="sxs-lookup"><span data-stu-id="14961-175">Learn how to [manage record sets and records](dns-getstarted-create-recordset-cli.md) in your DNS zone.</span></span>

<span data-ttu-id="14961-176">Bilgi edinmek için nasıl [etki alanınızı Azure DNS'ye temsilci](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="14961-176">Learn how to [delegate your domain to Azure DNS](dns-domain-delegation.md).</span></span>

