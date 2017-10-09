---
title: aaaAzure kaynak ilkeleri | Microsoft Docs
description: "Dağıtım sırasında toouse Azure Resource Manager ilkeleri tooensure tutarlı kaynak özellikleri nasıl ayarlanacağını açıklar. Merhaba abonelik veya kaynak gruplarının ilkeleri uygulanabilir."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: abde0f73-c0fe-4e6d-a1ee-32a6fce52a2d
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/02/2017
ms.author: tomfitz
ms.openlocfilehash: f1b0bbb5f838f6bb70721e1040ad3eac2d881cea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="resource-policy-overview"></a>Kaynak ilkesine genel bakış
Kaynak ilkeleri, kuruluşunuzdaki kaynakların tooestablish kuralları etkinleştirin. Kuralları tanımlayarak, daha kolay kaynaklarınızı yönetmek ve maliyetleri denetleyebilirsiniz. Örneğin, sanal makineler yalnızca belirli türdeki izin verildiğini belirtebilirsiniz. Veya, tüm kaynakların belirli bir etikete sahip olması gerekir. İlkeler tüm alt kaynaklar tarafından devralınır. Bu nedenle, bir ilke uygulanmış tooa kaynak grubu ise, uygun tooall hello kaynakların kaynak grubunda olur.

İki kavramları toounderstand ilkeleri hakkında vardır:

* ilke tanımı - hello İlkesi uygulandığında ne zaman ve hangi eylemini tootake açıklanmaktadır
* ilke ataması - hello ilke tanımı tooa kapsamı (abonelik veya kaynak grubu) Uygula

Bu konu, ilke tanımı odaklanır. İlke ataması hakkında daha fazla bilgi için bkz: [kullanım Azure portal tooassign ve kaynak ilkelerini yönetme](resource-manager-policy-portal.md) veya [atayın ve komut dosyası aracılığıyla ilkelerini yönetme](resource-manager-policy-create-assign.md).

İlkeleri oluşturma ve (PUT ve işlemleri düzeltme eki) kaynakları güncelleştirme değerlendirilir.

> [!NOTE]
> Şu anda, ilke etiketleri, türü ve konumu hello Microsoft.Resources/deployments kaynak türü gibi desteklemez kaynak türleri değerlendirmez. Bu destek gelecek bir zamanda eklenir. tooavoid geriye dönük uyumluluk sorunları, ilkeleri yazarken daha açıkça belirtilen türünü belirtmeniz gerekir. Örneğin, türleri belirtmeyen bir etiket İlkesi tüm türleri için uygulanır. Bu durumda, bir şablon dağıtımı etiketleri desteklemiyor iç içe geçmiş bir kaynak yoksa başarısız olabilir ve hello dağıtım kaynak türü toopolicy değerlendirme eklenmiştir. 
> 
> 

## <a name="how-is-it-different-from-rbac"></a>Nasıl RBAC farklı mı?
İlke ve rol tabanlı erişim denetimi (RBAC) arasındaki bazı farklar vardır. RBAC odaklanır **kullanıcı** farklı kapsamlar eylemlerini. Örneğin, değişiklikleri toothat kaynak grubu olabilmeniz toohello katkıda bulunan rolü bir kaynak grubu için istenen hello kapsamda eklenir. İlke odaklanır **kaynak** dağıtımı sırasında özellikler. Örneğin, ilkeler aracılığıyla sağlanabilir kaynak hello türleri kontrol edebilirsiniz. Ya da hello kaynakları sağlanabilir hello konumları kısıtlayabilirsiniz. RBAC, bir varsayılan izin ilkedir ve açık sistem engelle. 

toouse ilkeleri RBAC kimliğinin doğrulanması gerekir. Özellikle, hesabınızı gerekir:

* `Microsoft.Authorization/policydefinitions/write`izin toodefine bir ilke
* `Microsoft.Authorization/policyassignments/write`izin tooassign bir ilke 

Bu izinleri hello dahil edilmeyen **katkıda bulunan** rol.

## <a name="built-in-policies"></a>Yerleşik ilkeleri

Azure sağlar hello sayısını azaltabilir bazı yerleşik ilke tanımları ilkelerini toodefine sahip. İlke tanımları ile devam etmeden önce yerleşik bir ilke zaten ihtiyaç hello tanımı sağlayıp sağlamadığını göz önünde bulundurmalısınız. Merhaba yerleşik ilke tanımları şunlardır:

* İzin verilen konumların
* İzin verilen kaynak türleri
* Depolama hesabı SKU'ları izin
* Sanal makine SKU'ları izin
* Etiket ve varsayılan değer Uygula
* Etiket ve değer zorla
* Kaynak türleri izin verilmiyor
* SQL Server sürüm 12.0 gerektirir
* Depolama hesabı şifreleme iste

Herhangi bir hello aracılığıyla bu ilkeleri atayabilirsiniz [portal](resource-manager-policy-portal.md), [PowerShell](resource-manager-policy-create-assign.md#powershell), veya [Azure CLI](resource-manager-policy-create-assign.md#azure-cli).

## <a name="policy-definition-structure"></a>İlke tanımı yapısı
JSON toocreate bir ilke tanımı kullanın. Merhaba ilke tanımı için öğeleri içerir:

* parametreler
* Görünen ad
* açıklama
* İlke kuralı
  * mantıksal değerlendirme
  * Etkisi

Aşağıdaki örnek hello kaynakları dağıtıldığı sınırlar bir ilke gösterir:

```json
{
  "properties": {
    "parameters": {
      "allowedLocations": {
        "type": "array",
        "metadata": {
          "description": "hello list of locations that can be specified when deploying resources",
          "strongType": "location",
          "displayName": "Allowed locations"
        }
      }
    },
    "displayName": "Allowed locations",
    "description": "This policy enables you toorestrict hello locations your organization can specify when deploying resources.",
    "policyRule": {
      "if": {
        "not": {
          "field": "location",
          "in": "[parameters('allowedLocations')]"
        }
      },
      "then": {
        "effect": "deny"
      }
    }
  }
}
```

## <a name="parameters"></a>Parametreler
Parametrelerini kullanarak ilke tanımları hello sayısını azaltarak ilke yönetimini basitleştirmeye yardımcı olur. (Örneğin kaynaklar dağıtıldığı hello konumları sınırlama) kaynak özelliği için bir ilke tanımlayın ve hello tanımında parametreleri içerir. Ardından, bu ilke tanımı farklı senaryolar için (örneğin, bir dizi bir abonelik için konumları belirtme) farklı değerler geçirerek ne zaman yeniden hello ilkesi atama.

İlke tanımları oluşturduğunuzda parametreleri bildirin.

```json
"parameters": {
  "allowedLocations": {
    "type": "array",
    "metadata": {
      "description": "hello list of allowed locations for resources.",
      "displayName": "Allowed locations"
    }
  }
}
```

parametrenin Hello türü string veya dizi olabilir. Merhaba meta veri özelliği, Azure portal toodisplay kullanıcı dostu bilgiler gibi araçları için kullanılır. 

Hello İlkesi kuralında sözdizimi aşağıdaki hello ile parametreleri başvuru: 

```json
{ 
    "field": "location",
    "in": "[parameters('allowedLocations')]"
}
```

## <a name="display-name-and-description"></a>Görünen ad ve açıklama

Merhaba kullandığınız **displayName** ve **açıklama** tooidentify hello ilke tanımı ve ne zaman kullanıldığı için bağlamı sağlar.

## <a name="policy-rule"></a>İlke kuralı

Hello İlkesi kuralı oluşur **varsa** ve **sonra** engeller. Merhaba, **varsa** bloğu, ne zaman hello İlkesi uygulandığında belirten bir veya daha fazla koşullarını tanımlayın. Mantıksal işleçler toothese koşullar geçerli tooprecisely hello senaryo için bir ilke tanımlayın. Merhaba, **sonra** bloğu hello olur hello etkisi tanımladığınız **varsa** koşullar yerine.

```json
{
  "if": {
    <condition> | <logical operator>
  },
  "then": {
    "effect": "deny | audit | append"
  }
}
```

### <a name="logical-operators"></a>Mantıksal işleçler
desteklenen hello mantıksal işleçler şunlardır:

* `"not": {condition  or operator}`
* `"allOf": [{condition or operator},{condition or operator}]`
* `"anyOf": [{condition or operator},{condition or operator}]`

Merhaba **değil** sözdizimi hello koşul hello sonucunu tersine çevirir. Merhaba **tümü** sözdizimi (benzer toohello mantıksal **ve** işlemi) tüm koşullar toobe true gerektirir. Merhaba **herhangi** sözdizimi (benzer toohello mantıksal **veya** işlemi) bir veya daha fazla koşullar toobe true gerektirir.

Mantıksal işleçler yerleştirebilirsiniz. Aşağıdaki örnekte gösterildiği hello bir **değil** içinde iç içe işlemi bir **tümü** işlemi. 

```json
"if": {
  "allOf": [
    {
      "not": {
        "field": "tags",
        "containsKey": "application"
      }
    },
    {
      "field": "type",
      "equals": "Microsoft.Storage/storageAccounts"
    }
  ]
},
```

### <a name="conditions"></a>Koşullar
Merhaba koşulu değerlendirir olup bir **alan** belirli kriterlere uyan. desteklenen hello koşullar şunlardır:

* `"equals": "value"`
* `"like": "value"`
* `"match": "value"`
* `"contains": "value"`
* `"in": ["value1","value2"]`
* `"containsKey": "keyName"`
* `"exists": "bool"`

Merhaba kullanırken **gibi** koşulu, bir joker (*) hello değer sağlayabilir.

Merhaba kullanırken **eşleşen** koşul, sağlayın `#` toorepresent bir basamak `?` bir harf ve diğer toorepresent Bu gerçek karakteri için. Örnekler için bkz: [adları ve metin için kaynak ilkelerini uygulamak](resource-manager-policy-naming-convention.md).

### <a name="fields"></a>Alanları
Koşullar alanlar kullanılarak oluşturulur. Bir alan hello kaynak isteği yükü özelliklerinde temsil eden başka bir deyişle kullanılan toodescribe hello hello kaynağının durumu.  

alanları aşağıdaki hello desteklenir:

* `name`
* `kind`
* `type`
* `location`
* `tags`
* `tags.*` 
* özellik diğer adlar - bir listesi için bkz: [diğer adlar](#aliases).

### <a name="effect"></a>Etki
İlke etkili - üç tür destekler `deny`, `audit`, ve `append`. 

* **Reddetme** hello Denetim günlüğüne bir olay oluşturur ve hello isteği başarısız olur
* **Denetim** Denetim günlüğüne bir uyarı olayı oluşturur ama hello isteği başarısız değil
* **Append** alanları toohello isteği tanımlanan hello kümesi ekler 

İçin **sona**, aşağıdaki ayrıntılara hello sağlamanız gerekir:

```json
"effect": "append",
"details": [
  {
    "field": "field name",
    "value": "value of hello field"
  }
]
```

Merhaba değer bir dize veya bir JSON biçimi nesnesi olabilir. 

## <a name="aliases"></a>Diğer adlar

Bir kaynak türü için özellik diğer adlar tooaccess belirli özelliklerini kullanın. Diğer adlar hangi değerleri veya koşullara bir özelliği bir kaynak için izin verilen toorestrict etkinleştirin. Her bir diğer ad toopaths belirli kaynak türlerine yönelik farklı API sürümlerindeki eşler. İlke değerlendirmesi sırasında hello ilke altyapısı, API sürümü hello özelliği yolunu alır.

**Microsoft.Cache/Redis**

| Diğer ad | Açıklama |
| ----- | ----------- |
| Microsoft.Cache/Redis/enableNonSslPort | Ayarlanmış olup olmadığını hello ssl olmayan Redis bağlantı noktası (6379) etkindir. |
| Microsoft.Cache/Redis/shardCount | Premium küme önbelleği üzerinde oluşturulan parça toobe Hello sayısını ayarlayın.  |
| Microsoft.Cache/Redis/sku.capacity | Merhaba Redis önbelleği toodeploy Hello boyutunu ayarlayın.  |
| Microsoft.Cache/Redis/sku.family | Merhaba SKU ailesi toouse ayarlayın. |
| Microsoft.Cache/Redis/sku.name | Redis önbelleği toodeploy Hello türünü ayarlayın. |

**Microsoft.Cdn/profiles**

| Diğer ad | Açıklama |
| ----- | ----------- |
| Microsoft.CDN/profiles/sku.name | Fiyatlandırma katmanı hello Hello adını ayarlayın. |

**Microsoft.Compute/disks**

| Diğer ad | Açıklama |
| ----- | ----------- |
| Microsoft.Compute/imageOffer | Set hello teklif hello platform görüntüsü veya Market görüntüsü toocreate hello sanal makine kullanılır. |
| Microsoft.Compute/imagePublisher | Merhaba platform görüntüsü veya Market görüntüsü kümesi hello yayımcısına toocreate hello sanal makine kullanılır. |
| Microsoft.Compute/imageSku | Set hello hello platform görüntüsü veya Market görüntüsü SKU'su toocreate hello sanal makine kullanılır. |
| Microsoft.Compute/imageVersion | Merhaba platform görüntüsü veya Market görüntüsü sürümü kümesi hello toocreate hello sanal makine kullanılır. |


**Microsoft.Compute/virtualMachines**

| Diğer ad | Açıklama |
| ----- | ----------- |
| Microsoft.Compute/imageId | Merhaba kullanılan görüntü toocreate hello sanal makine Hello tanıtıcısı ayarlayın. |
| Microsoft.Compute/imageOffer | Set hello teklif hello platform görüntüsü veya Market görüntüsü toocreate hello sanal makine kullanılır. |
| Microsoft.Compute/imagePublisher | Merhaba platform görüntüsü veya Market görüntüsü kümesi hello yayımcısına toocreate hello sanal makine kullanılır. |
| Microsoft.Compute/imageSku | Set hello hello platform görüntüsü veya Market görüntüsü SKU'su toocreate hello sanal makine kullanılır. |
| Microsoft.Compute/imageVersion | Merhaba platform görüntüsü veya Market görüntüsü sürümü kümesi hello toocreate hello sanal makine kullanılır. |
| Microsoft.Compute/licenseType | Merhaba görüntü veya disk içi lisanslı ayarlanır. Bu değer yalnızca hello Windows Server işletim sistemi içeren görüntüler için kullanılır.  |
| Microsoft.Compute/virtualMachines/imageOffer | Set hello teklif hello platform görüntüsü veya Market görüntüsü toocreate hello sanal makine kullanılır. |
| Microsoft.Compute/virtualMachines/imagePublisher | Merhaba platform görüntüsü veya Market görüntüsü kümesi hello yayımcısına toocreate hello sanal makine kullanılır. |
| Microsoft.Compute/virtualMachines/imageSku | Set hello hello platform görüntüsü veya Market görüntüsü SKU'su toocreate hello sanal makine kullanılır. |
| Microsoft.Compute/virtualMachines/imageVersion | Merhaba platform görüntüsü veya Market görüntüsü sürümü kümesi hello toocreate hello sanal makine kullanılır. |
| Microsoft.Compute/virtualMachines/osDisk.Uri | Merhaba vhd URI ayarlayın. |
| Microsoft.Compute/virtualMachines/sku.name | Merhaba hello sanal makine boyutunu ayarlayın. |

**Microsoft.Compute/virtualMachines/extensions**

| Diğer ad | Açıklama |
| ----- | ----------- |
| Microsoft.Compute/virtualMachines/extensions/publisher | Merhaba hello uzantının yayımcının adını ayarlayın. |
| Microsoft.Compute/virtualMachines/extensions/type | Uzantı Hello türünü ayarlayın. |
| Microsoft.Compute/virtualMachines/extensions/typeHandlerVersion | Merhaba uzantıları Hello sürümünü ayarlayın. |

**Microsoft.Compute/virtualMachineScaleSets**

| Diğer ad | Açıklama |
| ----- | ----------- |
| Microsoft.Compute/imageId | Merhaba kullanılan görüntü toocreate hello sanal makine Hello tanıtıcısı ayarlayın. |
| Microsoft.Compute/imageOffer | Set hello teklif hello platform görüntüsü veya Market görüntüsü toocreate hello sanal makine kullanılır. |
| Microsoft.Compute/imagePublisher | Merhaba platform görüntüsü veya Market görüntüsü kümesi hello yayımcısına toocreate hello sanal makine kullanılır. |
| Microsoft.Compute/imageSku | Set hello hello platform görüntüsü veya Market görüntüsü SKU'su toocreate hello sanal makine kullanılır. |
| Microsoft.Compute/imageVersion | Merhaba platform görüntüsü veya Market görüntüsü sürümü kümesi hello toocreate hello sanal makine kullanılır. |
| Microsoft.Compute/licenseType | Merhaba görüntü veya disk içi lisanslı ayarlanır. Bu değer yalnızca hello Windows Server işletim sistemi içeren görüntüler için kullanılır. |
| Microsoft.Compute/VirtualMachineScaleSets/computerNamePrefix | Merhaba bilgisayar adı öneki tüm hello sanal makineler için hello ölçek kümesinde ayarlayın. |
| Microsoft.Compute/VirtualMachineScaleSets/osdisk.imageUrl | Kullanıcı görüntüsü için Hello blob URI'si ayarlayın. |
| Microsoft.Compute/VirtualMachineScaleSets/osdisk.vhdContainers | Merhaba ölçek kümesi için kullanılan toostore işletim sistemi diskler hello kapsayıcı URL'lerini ayarlayın. |
| Microsoft.Compute/VirtualMachineScaleSets/sku.name | Sanal makineler Hello boyutunu ölçek kümesinde ayarlayın. |
| Microsoft.Compute/VirtualMachineScaleSets/sku.tier | Sanal makinelerin Hello katmanı ölçek kümesinde ayarlayın. |
  
**Microsoft.Network/applicationGateways**

| Diğer ad | Açıklama |
| ----- | ----------- |
| Microsoft.Network/applicationGateways/sku.name | Merhaba ağ geçidi Hello boyutunu ayarlayın. |

**Microsoft.Network/virtualNetworkGateways**

| Diğer ad | Açıklama |
| ----- | ----------- |
| Microsoft.Network/virtualNetworkGateways/gatewayType | Bu sanal ağ geçidi Hello türünü ayarlayın. |
| Microsoft.Network/virtualNetworkGateways/sku.name | Merhaba ağ geçidi SKU adına ayarlayın. |

**Microsoft.Sql/servers**

| Diğer ad | Açıklama |
| ----- | ----------- |
| Microsoft.Sql/servers/version | Merhaba server Hello sürümünü ayarlayın. |

**Microsoft.Sql/databases**

| Diğer ad | Açıklama |
| ----- | ----------- |
| Microsoft.Sql/servers/databases/edition | Merhaba veritabanı Hello sürümünü ayarlayın. |
| Microsoft.Sql/servers/databases/elasticPoolName | Merhaba esnek havuz hello veritabanının kümesi hello adı kullanılıyor. |
| Microsoft.Sql/servers/databases/requestedServiceObjectiveId | Hello yapılandırılan hizmet düzeyi hedefi kimliği hello veritabanının ayarlayın. |
| Microsoft.Sql/servers/databases/requestedServiceObjectiveName | Merhaba hello yapılandırılan hizmet düzeyi hedefi hello veritabanının adını ayarlayın.  |

**Microsoft.Sql/elasticpools**

| Diğer ad | Açıklama |
| ----- | ----------- |
| sunucuları/elasticpools | Microsoft.Sql/servers/elasticPools/dtu | Set hello toplam DTU hello veritabanı esnek havuz için paylaşılan. |
| sunucuları/elasticpools | Microsoft.Sql/servers/elasticPools/edition | Merhaba esnek havuz Hello sürümünü ayarlayın. |

**Microsoft.Storage/storageAccounts**

| Diğer ad | Açıklama |
| ----- | ----------- |
| Microsoft.Storage/storageAccounts/accessTier | Set hello erişim katmanı için fatura kullanılır. |
| Microsoft.Storage/storageAccounts/accountType | Merhaba SKU adına ayarlayın. |
| Microsoft.Storage/storageAccounts/enableBlobEncryption | Merhaba blob depolama hizmetinde depolanan gibi hello hizmet hello verileri şifreler gerekip gerekmediğini belirleyin. |
| Microsoft.Storage/storageAccounts/enableFileEncryption | Merhaba dosya depolama hizmetinde depolanan gibi hello hizmet hello verileri şifreler gerekip gerekmediğini belirleyin. |
| Microsoft.Storage/storageAccounts/sku.name | Merhaba SKU adına ayarlayın. |
| Microsoft.Storage/storageAccounts/supportsHttpsTrafficOnly | Tooallow yalnızca https trafiği toostorage hizmetini ayarlayın. |


## <a name="policy-examples"></a>İlke örnekleri

Aşağıdaki konularda hello ilkesi örnekleri içerir:

* Etiket örnekleri ilkeleri için bkz: [etiketleri için kaynak ilkelerini uygulamak](resource-manager-policy-tags.md).
* Adlandırma ve metin düzeni örnekleri için bkz: [adları ve metin için kaynak ilkelerini uygulamak](resource-manager-policy-naming-convention.md).
* Depolama ilkeleri örnekleri için bkz: [kaynak ilkeleri toostorage hesapları geçerli](resource-manager-policy-storage.md).
* Sanal makine ilkeleri örnekleri için bkz: [kaynak ilkeleri tooLinux VM'ler uygulamak](../virtual-machines/linux/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json) ve [kaynak ilkeleri tooWindows VM'ler Uygula](../virtual-machines/windows/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json)


## <a name="next-steps"></a>Sonraki adımlar
* İlke kuralı tanımladıktan sonra tooa kapsamı atayın. Merhaba portal aracılığıyla tooassign ilkeleri Bkz [kullanım Azure portal tooassign ve kaynak ilkelerini yönetme](resource-manager-policy-portal.md). REST API'si, PowerShell veya Azure CLI aracılığıyla tooassign ilkeleri Bkz [atayın ve komut dosyası aracılığıyla ilkelerini yönetme](resource-manager-policy-create-assign.md).
* Kuruluşların Resource Manager tooeffectively nasıl kullanabileceğiniz hakkında rehberlik için abonelikleri yönetmek için bkz: [Azure enterprise iskele - Düzenleyici abonelik idare](resource-manager-subscription-governance.md).
* Hello İlkesi Şema konumunda yayımlanır [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json). 

