---
title: "Etiket mantıksal kuruluşunuz için Azure kaynaklarını | Microsoft Docs"
description: "Faturalama ve yönetmek için Azure kaynaklarını düzenlemek için etiketleri uygulamak gösterilmiştir."
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
ms.openlocfilehash: 4f52c30614ad39da8a34ff6ecfb707b75400517f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="use-tags-to-organize-your-azure-resources"></a><span data-ttu-id="785db-103">Azure kaynaklarınızı düzenlemek için etiketleri kullanma</span><span class="sxs-lookup"><span data-stu-id="785db-103">Use tags to organize your Azure resources</span></span>
[!INCLUDE [resource-manager-tag-introduction](../../includes/resource-manager-tag-introduction.md)]

> [!NOTE]
> <span data-ttu-id="785db-104">Azure Resource Manager işlemlerini destekleyen kaynaklara etiket uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="785db-104">You can apply tags only to resources that support Azure Resource Manager operations.</span></span> <span data-ttu-id="785db-105">Bir sanal makine, sanal ağ veya Klasik dağıtım modeli üzerinden depolama hesabı oluşturduysanız (gibi Klasik Azure Portalı aracılığıyla), bu kaynak için bir etiket uygulanamıyor.</span><span class="sxs-lookup"><span data-stu-id="785db-105">If you created a virtual machine, virtual network, or storage account through the classic deployment model (such as through the Azure classic portal), you cannot apply a tag to that resource.</span></span> <span data-ttu-id="785db-106">Etiketleme desteklemek için bu kaynakları Kaynak Yöneticisi aracılığıyla yeniden dağıtın.</span><span class="sxs-lookup"><span data-stu-id="785db-106">To support tagging, redeploy these resources through Resource Manager.</span></span> <span data-ttu-id="785db-107">Diğer tüm kaynaklar etiketleme desteği.</span><span class="sxs-lookup"><span data-stu-id="785db-107">All other resources support tagging.</span></span>
> 
> 

## <a name="policies-for-tag-consistency"></a><span data-ttu-id="785db-108">Etiket tutarlılık için ilkeleri</span><span class="sxs-lookup"><span data-stu-id="785db-108">Policies for tag consistency</span></span>

<span data-ttu-id="785db-109">Kuruluşunuz için standart kurallar oluşturmak için kaynak ilkelerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="785db-109">You can use resource policies to create standard rules for your organization.</span></span> <span data-ttu-id="785db-110">Kaynakları uygun değerlerle etiketlenir olun ilkeleri oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="785db-110">You can create policies that ensure resources are tagged with the appropriate values.</span></span> <span data-ttu-id="785db-111">Daha fazla bilgi için bkz: [etiketleri için kaynak ilkelerini uygulamak](resource-manager-policy-tags.md).</span><span class="sxs-lookup"><span data-stu-id="785db-111">For more information, see [Apply resource policies for tags](resource-manager-policy-tags.md).</span></span>

## <a name="powershell"></a><span data-ttu-id="785db-112">PowerShell</span><span class="sxs-lookup"><span data-stu-id="785db-112">PowerShell</span></span>
[!INCLUDE [resource-manager-tag-resources-powershell](../../includes/resource-manager-tag-resources-powershell.md)]

## <a name="azure-cli"></a><span data-ttu-id="785db-113">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="785db-113">Azure CLI</span></span>

<span data-ttu-id="785db-114">Bir *kaynak grubunun* mevcut etiketlerini görmek şunu kullanın:</span><span class="sxs-lookup"><span data-stu-id="785db-114">To see the existing tags for a *resource group*, use:</span></span>

```azurecli
az group show -n examplegroup --query tags
```

<span data-ttu-id="785db-115">Bu betik aşağıdaki biçimde veri döndürür:</span><span class="sxs-lookup"><span data-stu-id="785db-115">That script returns the following format:</span></span>

```json
{
  "Dept"        : "IT",
  "Environment" : "Test"
}
```

<span data-ttu-id="785db-116">*Kaynak kimliği belirtilmiş bir kaynağın* mevcut etiketlerini görmek için şunu kullanın:</span><span class="sxs-lookup"><span data-stu-id="785db-116">To see the existing tags for a *resource that has a specified resource ID*, use:</span></span>

```azurecli
az resource show --id {resource-id} --query tags
```

<span data-ttu-id="785db-117">Veya varolan etiketleri için görmek için bir *belirtilen adını, türünü ve kaynak grubuna sahip kaynak*, kullanın:</span><span class="sxs-lookup"><span data-stu-id="785db-117">Or, to see the existing tags for a *resource that has a specified name, type, and resource group*, use:</span></span>

```azurecli
az resource show -n examplevnet -g examplegroup --resource-type "Microsoft.Network/virtualNetworks" --query tags
```

<span data-ttu-id="785db-118">Belirli bir etikete sahip kaynak gruplarını elde etmek için kullanın `az group list`:</span><span class="sxs-lookup"><span data-stu-id="785db-118">To get resource groups that have a specific tag, use `az group list`:</span></span>

```azurecli
az group list --tag Dept=IT
```

<span data-ttu-id="785db-119">Özel etiket ve değerine sahip tüm kaynakları almak için `az resource list`:</span><span class="sxs-lookup"><span data-stu-id="785db-119">To get all the resources that have a particular tag and value, use `az resource list`:</span></span>

```azurecli
az resource list --tag Dept=Finance
```

<span data-ttu-id="785db-120">Bir kaynağa veya kaynak grubuna etiket uyguladığınız her durumda ilgili kaynağın veya kaynak grubunun üzerinde mevcut olan etiketlerin üzerine yazarsınız.</span><span class="sxs-lookup"><span data-stu-id="785db-120">Every time you apply tags to a resource or a resource group, you overwrite the existing tags on that resource or resource group.</span></span> <span data-ttu-id="785db-121">Bu nedenle, kaynakta veya kaynak grubunda etiketlerin mevcut olup olmamasına bağlı olarak farklı bir yaklaşım kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="785db-121">Therefore, you must use a different approach based on whether the resource or resource group has existing tags.</span></span> 

<span data-ttu-id="785db-122">*Mevcut etiketi olmayan bir kaynak grubuna* etiket eklemek için şunu kullanın:</span><span class="sxs-lookup"><span data-stu-id="785db-122">To add tags to a *resource group without existing tags*, use:</span></span>

```azurecli
az group update -n examplegroup --set tags.Environment=Test tags.Dept=IT
```

<span data-ttu-id="785db-123">*Mevcut etiketi olmayan bir kaynağa* etiket eklemek için şunu kullanın:</span><span class="sxs-lookup"><span data-stu-id="785db-123">To add tags to a *resource without existing tags*, use:</span></span>

```azurecli
az resource tag --tags Dept=IT Environment=Test -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks"
``` 

<span data-ttu-id="785db-124">Etiketleri zaten olan bir kaynağın etiketleri eklemek için varolan etiketleri almak, bu değeri yeniden biçimlendirin ve var olan ve yeni etiketler yeniden uygulayın:</span><span class="sxs-lookup"><span data-stu-id="785db-124">To add tags to a resource that already has tags, retrieve the existing tags, reformat that value, and reapply the existing and new tags:</span></span> 

```azurecli
jsonrtag=$(az resource show -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks" --query tags)
rt=$(echo $jsonrtag | tr -d '"{},' | sed 's/: /=/g')
az resource tag --tags $rt Project=Redesign -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks"
```

<span data-ttu-id="785db-125">Bir kaynak grubundaki tüm etiketleri *kaynaklardaki mevcut etiketleri korumadan* gruptaki kaynaklara uygulamak için aşağıdaki betiği kullanın:</span><span class="sxs-lookup"><span data-stu-id="785db-125">To apply all tags from a resource group to its resources, and *not retain existing tags on the resources*, use the following script:</span></span>

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

<span data-ttu-id="785db-126">Tüm etiketleri kaynaklarını için bir kaynak grubundan uygulamak için ve *kaynaklardaki varolan etiketleri korumak*, aşağıdaki komut dosyasını kullanın:</span><span class="sxs-lookup"><span data-stu-id="785db-126">To apply all tags from a resource group to its resources, and *retain existing tags on resources*, use the following script:</span></span>

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


## <a name="templates"></a><span data-ttu-id="785db-127">Şablonlar</span><span class="sxs-lookup"><span data-stu-id="785db-127">Templates</span></span>

[!INCLUDE [resource-manager-tags-in-templates](../../includes/resource-manager-tags-in-templates.md)]

## <a name="portal"></a><span data-ttu-id="785db-128">Portal</span><span class="sxs-lookup"><span data-stu-id="785db-128">Portal</span></span>
[!INCLUDE [resource-manager-tag-resource](../../includes/resource-manager-tag-resources.md)]


## <a name="rest-api"></a><span data-ttu-id="785db-129">REST API</span><span class="sxs-lookup"><span data-stu-id="785db-129">REST API</span></span>
<span data-ttu-id="785db-130">Azure portalı ve her ikisini de kullanmanız PowerShell [Resource Manager REST API'si](https://docs.microsoft.com/rest/api/resources/) arka planda.</span><span class="sxs-lookup"><span data-stu-id="785db-130">The Azure portal and PowerShell both use the [Resource Manager REST API](https://docs.microsoft.com/rest/api/resources/) behind the scenes.</span></span> <span data-ttu-id="785db-131">Başka bir ortama etiketleme tümleştirme gerekiyorsa, etiketleri kullanarak alabileceğiniz **almak** kaynak kimliği ile güncelleştirme kullanarak etiketleri kümesi üzerinde bir **düzeltme eki** çağırın.</span><span class="sxs-lookup"><span data-stu-id="785db-131">If you need to integrate tagging into another environment, you can get tags by using **GET** on the resource ID and update the set of tags by using a **PATCH** call.</span></span>

## <a name="tags-and-billing"></a><span data-ttu-id="785db-132">Etiketleri ve faturalama</span><span class="sxs-lookup"><span data-stu-id="785db-132">Tags and billing</span></span>
<span data-ttu-id="785db-133">Faturalama verileriniz gruplandırmak için etiketler kullanın.</span><span class="sxs-lookup"><span data-stu-id="785db-133">You can use tags to group your billing data.</span></span> <span data-ttu-id="785db-134">Örneğin, birden çok VM farklı kuruluşlarda çalıştırıyorsanız, etiketleri Grup kullanım için maliyet merkezi tarafından kullanın.</span><span class="sxs-lookup"><span data-stu-id="785db-134">For example, if you are running multiple VMs for different organizations, use the tags to group usage by cost center.</span></span> <span data-ttu-id="785db-135">Etiketler, maliyetleri üretim ortamında çalışan sanal makineler için fatura kullanımı gibi çalışma zamanı ortamı tarafından kategorilere ayırmak için de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="785db-135">You can also use tags to categorize costs by runtime environment, such as the billing usage for VMs running in the production environment.</span></span>


<span data-ttu-id="785db-136">Etiketler hakkında bilgi alabilir [Azure kaynak kullanımı ve RateCard API'leri](../billing/billing-usage-rate-card-overview.md) veya kullanım virgülle ayrılmış değerler (CSV) dosyası.</span><span class="sxs-lookup"><span data-stu-id="785db-136">You can retrieve information about tags through the [Azure Resource Usage and RateCard APIs](../billing/billing-usage-rate-card-overview.md) or the usage comma-separated values (CSV) file.</span></span> <span data-ttu-id="785db-137">Kullanım dosyasını indirin [Azure hesap portalı](https://account.windowsazure.com/) veya [EA portal](https://ea.azure.com).</span><span class="sxs-lookup"><span data-stu-id="785db-137">You download the usage file from the [Azure account portal](https://account.windowsazure.com/) or [EA portal](https://ea.azure.com).</span></span> <span data-ttu-id="785db-138">Faturalandırma bilgileri programlı erişim hakkında daha fazla bilgi için bkz: [Microsoft Azure kaynak tüketimini Öngörüler elde](../billing/billing-usage-rate-card-overview.md).</span><span class="sxs-lookup"><span data-stu-id="785db-138">For more information about programmatic access to billing information, see [Gain insights into your Microsoft Azure resource consumption](../billing/billing-usage-rate-card-overview.md).</span></span> <span data-ttu-id="785db-139">REST API işlemleri için bkz: [Azure faturalama REST API Başvurusu](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c).</span><span class="sxs-lookup"><span data-stu-id="785db-139">For REST API operations, see [Azure Billing REST API Reference](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c).</span></span>


<span data-ttu-id="785db-140">Faturalama etiketleriyle destekleyen hizmetler için kullanım CSV yüklediğinizde etiketler görünür **etiketleri** sütun.</span><span class="sxs-lookup"><span data-stu-id="785db-140">When you download the usage CSV for services that support tags with billing, the tags appear in the **Tags** column.</span></span> <span data-ttu-id="785db-141">Daha fazla bilgi için bkz: [faturanızı anlamak için Microsoft Azure](../billing/billing-understand-your-bill.md).</span><span class="sxs-lookup"><span data-stu-id="785db-141">For more information, see [Understand your bill for Microsoft Azure](../billing/billing-understand-your-bill.md).</span></span>

![Faturalama etiketlerinde bakın](./media/resource-group-using-tags/billing_csv.png)

## <a name="next-steps"></a><span data-ttu-id="785db-143">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="785db-143">Next steps</span></span>
* <span data-ttu-id="785db-144">Özelleştirilmiş ilkeler kullanarak aboneliğinizi arasında kısıtlamaları ve kuralları uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="785db-144">You can apply restrictions and conventions across your subscription by using customized policies.</span></span> <span data-ttu-id="785db-145">Tanımladığınız bir ilke tüm kaynakların belirli bir etiket için bir değere sahip gerektirebilir.</span><span class="sxs-lookup"><span data-stu-id="785db-145">A policy that you define might require that all resources have a value for a particular tag.</span></span> <span data-ttu-id="785db-146">Daha fazla bilgi için bkz: [kaynakları yönetmek ve erişimi denetlemek için ilkeleri kullanma](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="785db-146">For more information, see [Use policies to manage resources and control access](resource-manager-policy.md).</span></span>
* <span data-ttu-id="785db-147">Kaynakları dağıtırken Azure PowerShell kullanarak bir giriş için bkz: [Azure PowerShell kullanarak Azure Resource Manager ile](powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="785db-147">For an introduction to using Azure PowerShell when you're deploying resources, see [Using Azure PowerShell with Azure Resource Manager](powershell-azure-resource-manager.md).</span></span>
* <span data-ttu-id="785db-148">Kaynakları dağıtırken Azure CLI kullanarak bir giriş için bkz: [Mac, Linux ve Windows Azure Resource Manager ile Azure CLI kullanarak](xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="785db-148">For an introduction to using the Azure CLI when you're deploying resources, see [Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](xplat-cli-azure-resource-manager.md).</span></span>
* <span data-ttu-id="785db-149">Portalı kullanarak bir giriş için bkz: [Azure kaynaklarınızı yönetmek için Azure portalını kullanarak](resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="785db-149">For an introduction to using the portal, see [Using the Azure portal to manage your Azure resources](resource-group-portal.md).</span></span>  
* <span data-ttu-id="785db-150">Kuruluşların abonelikleri etkili bir şekilde yönetmek için Resource Manager'ı nasıl kullanabileceği hakkında yönergeler için bkz. [Azure kurumsal iskelesi: öngörücü abonelik idaresi](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="785db-150">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

