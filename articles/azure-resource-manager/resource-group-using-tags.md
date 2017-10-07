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
# <a name="use-tags-tooorganize-your-azure-resources"></a>Azure kaynaklarınızı etiketleri tooorganize kullanın
[!INCLUDE [resource-manager-tag-introduction](../../includes/resource-manager-tag-introduction.md)]

> [!NOTE]
> Azure Resource Manager işlemlerini destekleyen etiketleri yalnızca tooresources uygulayabilirsiniz. Bir sanal makine, sanal ağ ya da (örneğin olarak aracılığıyla Klasik Azure portalı hello) hello Klasik dağıtım modeli üzerinden depolama hesabı oluşturduysanız, etiket toothat kaynak uygulanamıyor. toosupport etiketleme, bu kaynakları Kaynak Yöneticisi aracılığıyla yeniden dağıtın. Diğer tüm kaynaklar etiketleme desteği.
> 
> 

## <a name="policies-for-tag-consistency"></a>Etiket tutarlılık için ilkeleri

Kaynak ilkeleri toocreate standart kurallar, kuruluşunuz için kullanabilirsiniz. Kaynakları hello uygun değerlerle etiketlenir olun ilkeleri oluşturabilirsiniz. Daha fazla bilgi için bkz: [etiketleri için kaynak ilkelerini uygulamak](resource-manager-policy-tags.md).

## <a name="powershell"></a>PowerShell
[!INCLUDE [resource-manager-tag-resources-powershell](../../includes/resource-manager-tag-resources-powershell.md)]

## <a name="azure-cli"></a>Azure CLI

toosee hello için varolan etiketleri bir *kaynak grubu*, kullanın:

```azurecli
az group show -n examplegroup --query tags
```

Bu komut dosyası biçimini izleyen hello döndürür:

```json
{
  "Dept"        : "IT",
  "Environment" : "Test"
}
```

toosee hello için varolan etiketleri bir *belirtilen kaynak Kimliğine sahip kaynak*, kullanın:

```azurecli
az resource show --id {resource-id} --query tags
```

Ya da toosee hello için varolan etiketleri bir *belirtilen adını, türünü ve kaynak grubuna sahip kaynak*, kullanın:

```azurecli
az resource show -n examplevnet -g examplegroup --resource-type "Microsoft.Network/virtualNetworks" --query tags
```

belirli bir etikete sahip tooget kaynak gruplarını kullanma `az group list`:

```azurecli
az group list --tag Dept=IT
```

bir özel etiket ve değer, sahip tüm hello kaynakları tooget kullanmak `az resource list`:

```azurecli
az resource list --tag Dept=Finance
```

Etiketler tooa kaynağa veya bir kaynak grubuna uygulamak her zaman, o kaynak veya kaynak grubu hello varolan etiketleri üzerine yazın. Bu nedenle, olup hello kaynağı veya kaynak grubunu varolan etiketleri temel alarak farklı bir yaklaşım kullanmanız gerekir. 

tooadd etiketler tooa *kaynak grubu mevcut etiketleri olmadan*, kullanın:

```azurecli
az group update -n examplegroup --set tags.Environment=Test tags.Dept=IT
```

tooadd etiketler tooa *varolan etiketleri olmadan kaynak*, kullanın:

```azurecli
az resource tag --tags Dept=IT Environment=Test -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks"
``` 

Etiketler, zaten tooadd etiketleri tooa kaynak hello varolan etiketleri almak, bu değeri yeniden biçimlendirin ve hello mevcut ve yeni etiketler yeniden uygulayın: 

```azurecli
jsonrtag=$(az resource show -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks" --query tags)
rt=$(echo $jsonrtag | tr -d '"{},' | sed 's/: /=/g')
az resource tag --tags $rt Project=Redesign -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks"
```

tooapply tüm etiketleri bir kaynak grubu tooits kaynakları ve *hello kaynaklardaki varolan etiketleri korumuyor*, komut dosyası izleyen hello kullanın:

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

tooapply tüm etiketleri bir kaynak grubu tooits kaynakları ve *kaynaklardaki varolan etiketleri korumak*, komut dosyası izleyen hello kullanın:

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


## <a name="templates"></a>Şablonlar

[!INCLUDE [resource-manager-tags-in-templates](../../includes/resource-manager-tags-in-templates.md)]

## <a name="portal"></a>Portal
[!INCLUDE [resource-manager-tag-resource](../../includes/resource-manager-tag-resources.md)]


## <a name="rest-api"></a>REST API
Hello Azure portalı ve PowerShell hello kullan [Resource Manager REST API'si](https://docs.microsoft.com/rest/api/resources/) hello perde arkasında. Başka bir ortama etiketleme toointegrate gerekiyorsa, etiketleri kullanarak alabileceğiniz **almak** hello kaynak kimliği ve güncelleştirme hello kümesi üzerinde etiketleri kullanarak bir **düzeltme eki** çağırın.

## <a name="tags-and-billing"></a>Etiketleri ve faturalama
Faturalama verileriniz etiketleri toogroup kullanabilirsiniz. Örneğin, birden çok VM farklı kuruluşlarda çalıştırıyorsanız, hello etiketleri toogroup kullanımını maliyet merkezi tarafından kullanın. Merhaba üretim ortamında çalışan sanal makineler için fatura kullanım hello gibi çalışma zamanı ortamı tarafından etiketleri toocategorize maliyetleri de kullanabilirsiniz.


Merhaba aracılığıyla etiketleri hakkında bilgi alabilir [Azure kaynak kullanımı ve RateCard API'leri](../billing/billing-usage-rate-card-overview.md) veya hello kullanım virgülle ayrılmış değerler (CSV) dosyası. Hello hello kullanım dosyasını karşıdan [Azure hesap portalı](https://account.windowsazure.com/) veya [EA portal](https://ea.azure.com). Programlı erişim toobilling bilgileri hakkında daha fazla bilgi için bkz: [Microsoft Azure kaynak tüketimini Öngörüler elde](../billing/billing-usage-rate-card-overview.md). REST API işlemleri için bkz: [Azure faturalama REST API Başvurusu](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c).


Faturalama etiketleriyle destekleyen hizmetler için hello kullanım CSV yüklediğinizde hello hello etiketler görünür **etiketleri** sütun. Daha fazla bilgi için bkz: [faturanızı anlamak için Microsoft Azure](../billing/billing-understand-your-bill.md).

![Faturalama etiketlerinde bakın](./media/resource-group-using-tags/billing_csv.png)

## <a name="next-steps"></a>Sonraki adımlar
* Özelleştirilmiş ilkeler kullanarak aboneliğinizi arasında kısıtlamaları ve kuralları uygulayabilirsiniz. Tanımladığınız bir ilke tüm kaynakların belirli bir etiket için bir değere sahip gerektirebilir. Daha fazla bilgi için bkz: [ilkeleri toomanage kaynakları kullanın ve erişimi denetlemenize](resource-manager-policy.md).
* Bir giriş toousing Azure PowerShell kaynakları dağıtıyorsanız, bkz: [Azure PowerShell kullanarak Azure Resource Manager ile](powershell-azure-resource-manager.md).
* Bir giriş toousing hello Azure CLI için kaynakları dağıtıyorsanız, bkz: [kullanma hello Mac, Linux ve Windows Azure Resource Manager ile Azure CLI](xplat-cli-azure-resource-manager.md).
* Bir giriş toousing hello portal için bkz: [kullanarak Azure kaynaklarınızı Azure portal toomanage hello](resource-group-portal.md).  
* Kuruluşların Resource Manager tooeffectively nasıl kullanabileceğiniz hakkında rehberlik için abonelikleri yönetmek için bkz: [Azure enterprise iskele - Düzenleyici abonelik idare](resource-manager-subscription-governance.md).

