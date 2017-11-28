---
title: "aaaTag Azure mantıksal kuruluş kaynakları | Microsoft Docs"
description: "Nasıl tooapply tooorganize Azure etiketleri gösterir faturalama ve yönetmek için kaynaklar."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 003a78e5-2ff8-4685-93b4-e94d6fb8ed5b
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: AzurePortal
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: tomfitz
ms.openlocfilehash: e07470463d160f8cefe5c80bc91e66a96af6ca45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-tags-tooorganize-your-azure-resources"></a><span data-ttu-id="51efc-103">Azure kaynaklarınızı etiketleri tooorganize kullanın</span><span class="sxs-lookup"><span data-stu-id="51efc-103">Use tags tooorganize your Azure resources</span></span>
[!INCLUDE [resource-manager-tag-introduction](../../includes/resource-manager-tag-introduction.md)]

> [!NOTE]
> <span data-ttu-id="51efc-104">Azure Resource Manager işlemlerini destekleyen etiketleri yalnızca tooresources uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="51efc-104">You can apply tags only tooresources that support Azure Resource Manager operations.</span></span> <span data-ttu-id="51efc-105">Bir sanal makine, sanal ağ ya da (örneğin olarak aracılığıyla Klasik Azure portalı hello) hello Klasik dağıtım modeli üzerinden depolama hesabı oluşturduysanız, etiket toothat kaynak uygulanamıyor.</span><span class="sxs-lookup"><span data-stu-id="51efc-105">If you created a virtual machine, virtual network, or storage account through hello classic deployment model (such as through hello Azure classic portal), you cannot apply a tag toothat resource.</span></span> <span data-ttu-id="51efc-106">toosupport etiketleme, bu kaynakları Kaynak Yöneticisi aracılığıyla yeniden dağıtın.</span><span class="sxs-lookup"><span data-stu-id="51efc-106">toosupport tagging, redeploy these resources through Resource Manager.</span></span> <span data-ttu-id="51efc-107">Diğer tüm kaynaklar etiketleme desteği.</span><span class="sxs-lookup"><span data-stu-id="51efc-107">All other resources support tagging.</span></span>
> 
> 

## <a name="policies-for-tag-consistency"></a><span data-ttu-id="51efc-108">Etiket tutarlılık için ilkeleri</span><span class="sxs-lookup"><span data-stu-id="51efc-108">Policies for tag consistency</span></span>

<span data-ttu-id="51efc-109">Kaynak ilkeleri toocreate standart kurallar, kuruluşunuz için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="51efc-109">You can use resource policies toocreate standard rules for your organization.</span></span> <span data-ttu-id="51efc-110">Kaynakları hello uygun değerlerle etiketlenir olun ilkeleri oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="51efc-110">You can create policies that ensure resources are tagged with hello appropriate values.</span></span> <span data-ttu-id="51efc-111">Daha fazla bilgi için bkz: [etiketleri için kaynak ilkelerini uygulamak](resource-manager-policy-tags.md).</span><span class="sxs-lookup"><span data-stu-id="51efc-111">For more information, see [Apply resource policies for tags](resource-manager-policy-tags.md).</span></span>

## <a name="powershell"></a><span data-ttu-id="51efc-112">PowerShell</span><span class="sxs-lookup"><span data-stu-id="51efc-112">PowerShell</span></span>
[!INCLUDE [resource-manager-tag-resources-powershell](../../includes/resource-manager-tag-resources-powershell.md)]

## <a name="azure-cli"></a><span data-ttu-id="51efc-113">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="51efc-113">Azure CLI</span></span>

<span data-ttu-id="51efc-114">toosee hello için varolan etiketleri bir *kaynak grubu*, kullanın:</span><span class="sxs-lookup"><span data-stu-id="51efc-114">toosee hello existing tags for a *resource group*, use:</span></span>

```azurecli
az group show -n examplegroup --query tags
```

<span data-ttu-id="51efc-115">Bu komut dosyası biçimini izleyen hello döndürür:</span><span class="sxs-lookup"><span data-stu-id="51efc-115">That script returns hello following format:</span></span>

```json
{
  "Dept"        : "IT",
  "Environment" : "Test"
}
```

<span data-ttu-id="51efc-116">toosee hello için varolan etiketleri bir *belirtilen kaynak Kimliğine sahip kaynak*, kullanın:</span><span class="sxs-lookup"><span data-stu-id="51efc-116">toosee hello existing tags for a *resource that has a specified resource ID*, use:</span></span>

```azurecli
az resource show --id {resource-id} --query tags
```

<span data-ttu-id="51efc-117">Ya da toosee hello için varolan etiketleri bir *belirtilen adını, türünü ve kaynak grubuna sahip kaynak*, kullanın:</span><span class="sxs-lookup"><span data-stu-id="51efc-117">Or, toosee hello existing tags for a *resource that has a specified name, type, and resource group*, use:</span></span>

```azurecli
az resource show -n examplevnet -g examplegroup --resource-type "Microsoft.Network/virtualNetworks" --query tags
```

<span data-ttu-id="51efc-118">belirli bir etikete sahip tooget kaynak gruplarını kullanma `az group list`:</span><span class="sxs-lookup"><span data-stu-id="51efc-118">tooget resource groups that have a specific tag, use `az group list`:</span></span>

```azurecli
az group list --tag Dept=IT
```

<span data-ttu-id="51efc-119">bir özel etiket ve değer, sahip tüm hello kaynakları tooget kullanmak `az resource list`:</span><span class="sxs-lookup"><span data-stu-id="51efc-119">tooget all hello resources that have a particular tag and value, use `az resource list`:</span></span>

```azurecli
az resource list --tag Dept=Finance
```

<span data-ttu-id="51efc-120">Etiketler tooa kaynağa veya bir kaynak grubuna uygulamak her zaman, o kaynak veya kaynak grubu hello varolan etiketleri üzerine yazın.</span><span class="sxs-lookup"><span data-stu-id="51efc-120">Every time you apply tags tooa resource or a resource group, you overwrite hello existing tags on that resource or resource group.</span></span> <span data-ttu-id="51efc-121">Bu nedenle, olup hello kaynağı veya kaynak grubunu varolan etiketleri temel alarak farklı bir yaklaşım kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="51efc-121">Therefore, you must use a different approach based on whether hello resource or resource group has existing tags.</span></span> 

<span data-ttu-id="51efc-122">tooadd etiketler tooa *kaynak grubu mevcut etiketleri olmadan*, kullanın:</span><span class="sxs-lookup"><span data-stu-id="51efc-122">tooadd tags tooa *resource group without existing tags*, use:</span></span>

```azurecli
az group update -n examplegroup --set tags.Environment=Test tags.Dept=IT
```

<span data-ttu-id="51efc-123">tooadd etiketler tooa *varolan etiketleri olmadan kaynak*, kullanın:</span><span class="sxs-lookup"><span data-stu-id="51efc-123">tooadd tags tooa *resource without existing tags*, use:</span></span>

```azurecli
az resource tag --tags Dept=IT Environment=Test -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks"
``` 

<span data-ttu-id="51efc-124">Etiketler, zaten tooadd etiketleri tooa kaynak hello varolan etiketleri almak, bu değeri yeniden biçimlendirin ve hello mevcut ve yeni etiketler yeniden uygulayın:</span><span class="sxs-lookup"><span data-stu-id="51efc-124">tooadd tags tooa resource that already has tags, retrieve hello existing tags, reformat that value, and reapply hello existing and new tags:</span></span> 

```azurecli
jsonrtag=$(az resource show -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks" --query tags)
rt=$(echo $jsonrtag | tr -d '"{},' | sed 's/: /=/g')
az resource tag --tags $rt Project=Redesign -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks"
```

<span data-ttu-id="51efc-125">tooapply tüm etiketleri bir kaynak grubu tooits kaynakları ve *hello kaynaklardaki varolan etiketleri korumuyor*, komut dosyası izleyen hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="51efc-125">tooapply all tags from a resource group tooits resources, and *not retain existing tags on hello resources*, use hello following script:</span></span>

```azurecli
groups=$(az group list --query [].name --output tsv)
for rg in $groups 
do 
  jsontag=$(az group show -n $rg --query tags)
  t=$(echo $jsontag | tr -d '"{},' | sed 's/: /=/g')
  r=$(az resource list -g $rg --query [].id --output tsv) 
  for resid in $r 
  do 
    az resource tag --tags $t --id $resid
  done 
done
```

<span data-ttu-id="51efc-126">tooapply tüm etiketleri bir kaynak grubu tooits kaynakları ve *kaynaklardaki varolan etiketleri korumak*, komut dosyası izleyen hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="51efc-126">tooapply all tags from a resource group tooits resources, and *retain existing tags on resources*, use hello following script:</span></span>

```azurecli
groups=$(az group list --query [].name --output tsv)
for rg in $groups 
do 
  jsontag=$(az group show -n $rg --query tags)
  t=$(echo $jsontag | tr -d '"{},' | sed 's/: /=/g')
  r=$(az resource list -g $rg --query [].id --output tsv) 
  for resid in $r 
  do 
    jsonrtag=$(az resource show --id $resid --query tags)
    rt=$(echo $jsonrtag | tr -d '"{},' | sed 's/: /=/g')
    az resource tag --tags $t$rt --id $resid
  done 
done
```


## <a name="templates"></a><span data-ttu-id="51efc-127">Şablonlar</span><span class="sxs-lookup"><span data-stu-id="51efc-127">Templates</span></span>

[!INCLUDE [resource-manager-tags-in-templates](../../includes/resource-manager-tags-in-templates.md)]

## <a name="portal"></a><span data-ttu-id="51efc-128">Portal</span><span class="sxs-lookup"><span data-stu-id="51efc-128">Portal</span></span>
[!INCLUDE [resource-manager-tag-resource](../../includes/resource-manager-tag-resources.md)]


## <a name="rest-api"></a><span data-ttu-id="51efc-129">REST API</span><span class="sxs-lookup"><span data-stu-id="51efc-129">REST API</span></span>
<span data-ttu-id="51efc-130">Hello Azure portalı ve PowerShell hello kullan [Resource Manager REST API'si](https://docs.microsoft.com/rest/api/resources/) hello perde arkasında.</span><span class="sxs-lookup"><span data-stu-id="51efc-130">hello Azure portal and PowerShell both use hello [Resource Manager REST API](https://docs.microsoft.com/rest/api/resources/) behind hello scenes.</span></span> <span data-ttu-id="51efc-131">Başka bir ortama etiketleme toointegrate gerekiyorsa, etiketleri kullanarak alabileceğiniz **almak** hello kaynak kimliği ve güncelleştirme hello kümesi üzerinde etiketleri kullanarak bir **düzeltme eki** çağırın.</span><span class="sxs-lookup"><span data-stu-id="51efc-131">If you need toointegrate tagging into another environment, you can get tags by using **GET** on hello resource ID and update hello set of tags by using a **PATCH** call.</span></span>

## <a name="tags-and-billing"></a><span data-ttu-id="51efc-132">Etiketleri ve faturalama</span><span class="sxs-lookup"><span data-stu-id="51efc-132">Tags and billing</span></span>
<span data-ttu-id="51efc-133">Faturalama verileriniz etiketleri toogroup kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="51efc-133">You can use tags toogroup your billing data.</span></span> <span data-ttu-id="51efc-134">Örneğin, birden çok VM farklı kuruluşlarda çalıştırıyorsanız, hello etiketleri toogroup kullanımını maliyet merkezi tarafından kullanın.</span><span class="sxs-lookup"><span data-stu-id="51efc-134">For example, if you are running multiple VMs for different organizations, use hello tags toogroup usage by cost center.</span></span> <span data-ttu-id="51efc-135">Merhaba üretim ortamında çalışan sanal makineler için fatura kullanım hello gibi çalışma zamanı ortamı tarafından etiketleri toocategorize maliyetleri de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="51efc-135">You can also use tags toocategorize costs by runtime environment, such as hello billing usage for VMs running in hello production environment.</span></span>


<span data-ttu-id="51efc-136">Merhaba aracılığıyla etiketleri hakkında bilgi alabilir [Azure kaynak kullanımı ve RateCard API'leri](../billing/billing-usage-rate-card-overview.md) veya hello kullanım virgülle ayrılmış değerler (CSV) dosyası.</span><span class="sxs-lookup"><span data-stu-id="51efc-136">You can retrieve information about tags through hello [Azure Resource Usage and RateCard APIs](../billing/billing-usage-rate-card-overview.md) or hello usage comma-separated values (CSV) file.</span></span> <span data-ttu-id="51efc-137">Hello hello kullanım dosyasını karşıdan [Azure hesap portalı](https://account.windowsazure.com/) veya [EA portal](https://ea.azure.com).</span><span class="sxs-lookup"><span data-stu-id="51efc-137">You download hello usage file from hello [Azure account portal](https://account.windowsazure.com/) or [EA portal](https://ea.azure.com).</span></span> <span data-ttu-id="51efc-138">Programlı erişim toobilling bilgileri hakkında daha fazla bilgi için bkz: [Microsoft Azure kaynak tüketimini Öngörüler elde](../billing/billing-usage-rate-card-overview.md).</span><span class="sxs-lookup"><span data-stu-id="51efc-138">For more information about programmatic access toobilling information, see [Gain insights into your Microsoft Azure resource consumption](../billing/billing-usage-rate-card-overview.md).</span></span> <span data-ttu-id="51efc-139">REST API işlemleri için bkz: [Azure faturalama REST API Başvurusu](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c).</span><span class="sxs-lookup"><span data-stu-id="51efc-139">For REST API operations, see [Azure Billing REST API Reference](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c).</span></span>


<span data-ttu-id="51efc-140">Faturalama etiketleriyle destekleyen hizmetler için hello kullanım CSV yüklediğinizde hello hello etiketler görünür **etiketleri** sütun.</span><span class="sxs-lookup"><span data-stu-id="51efc-140">When you download hello usage CSV for services that support tags with billing, hello tags appear in hello **Tags** column.</span></span> <span data-ttu-id="51efc-141">Daha fazla bilgi için bkz: [faturanızı anlamak için Microsoft Azure](../billing/billing-understand-your-bill.md).</span><span class="sxs-lookup"><span data-stu-id="51efc-141">For more information, see [Understand your bill for Microsoft Azure](../billing/billing-understand-your-bill.md).</span></span>

![Faturalama etiketlerinde bakın](./media/resource-group-using-tags/billing_csv.png)

## <a name="next-steps"></a><span data-ttu-id="51efc-143">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="51efc-143">Next steps</span></span>
* <span data-ttu-id="51efc-144">Özelleştirilmiş ilkeler kullanarak aboneliğinizi arasında kısıtlamaları ve kuralları uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="51efc-144">You can apply restrictions and conventions across your subscription by using customized policies.</span></span> <span data-ttu-id="51efc-145">Tanımladığınız bir ilke tüm kaynakların belirli bir etiket için bir değere sahip gerektirebilir.</span><span class="sxs-lookup"><span data-stu-id="51efc-145">A policy that you define might require that all resources have a value for a particular tag.</span></span> <span data-ttu-id="51efc-146">Daha fazla bilgi için bkz: [ilkeleri toomanage kaynakları kullanın ve erişimi denetlemenize](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="51efc-146">For more information, see [Use policies toomanage resources and control access](resource-manager-policy.md).</span></span>
* <span data-ttu-id="51efc-147">Bir giriş toousing Azure PowerShell kaynakları dağıtıyorsanız, bkz: [Azure PowerShell kullanarak Azure Resource Manager ile](powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="51efc-147">For an introduction toousing Azure PowerShell when you're deploying resources, see [Using Azure PowerShell with Azure Resource Manager](powershell-azure-resource-manager.md).</span></span>
* <span data-ttu-id="51efc-148">Bir giriş toousing hello Azure CLI için kaynakları dağıtıyorsanız, bkz: [kullanma hello Mac, Linux ve Windows Azure Resource Manager ile Azure CLI](xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="51efc-148">For an introduction toousing hello Azure CLI when you're deploying resources, see [Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](xplat-cli-azure-resource-manager.md).</span></span>
* <span data-ttu-id="51efc-149">Bir giriş toousing hello portal için bkz: [kullanarak Azure kaynaklarınızı Azure portal toomanage hello](resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="51efc-149">For an introduction toousing hello portal, see [Using hello Azure portal toomanage your Azure resources](resource-group-portal.md).</span></span>  
* <span data-ttu-id="51efc-150">Kuruluşların Resource Manager tooeffectively nasıl kullanabileceğiniz hakkında rehberlik için abonelikleri yönetmek için bkz: [Azure enterprise iskele - Düzenleyici abonelik idare](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="51efc-150">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

