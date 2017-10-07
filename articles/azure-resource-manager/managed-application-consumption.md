---
title: "bir Azure aaaConsume yönetilen uygulama | Microsoft Docs"
description: "Bir müşteri Azure nasıl oluşturduğunu açıklar yayımlanan dosyalarından yönetilen uygulama."
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 08/23/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: b8510086eb05304c0e351a391b7e0cf34a467568
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="consume-an-internal-managed-application"></a>Bir iç yönetilen uygulama kullanma

Azure tüketebileceği [yönetilen uygulamaları](managed-application-overview.md) kuruluşunuzun üyeleri için yöneliktir. Örneğin, kuruluş standartlarıyla uyumluluğu sağlamak BT departmanınızın yönetilen uygulamaları seçin. Bu yönetilen uygulamaların hello hizmet Kataloğu, hello Azure Market kullanılabilir.

Bu makale ile devam etmeden önce aboneliğiniz için bir yönetilen uygulamayı hello hizmet Kataloğu'nda kullanılabilir olmalıdır. Birisi, kuruluşunuzdaki yönetilen bir uygulamaya oluşturulmamış olup [dahili tüketim için yönetilen bir uygulama yayımlama](managed-application-publishing.md).

Şu anda, Azure CLI veya hello Azure portal tooconsume yönetilen bir uygulama kullanabilirsiniz.

## <a name="create-hello-managed-application-by-using-hello-portal"></a>Merhaba portalını kullanarak yönetilen Merhaba uygulaması oluşturma

toodeploy hello portal aracılığıyla bir yönetilen uygulamayı aşağıdaki adımları izleyin:

1. Toohello Azure portalına gidin. Arama **hizmet Kataloğu yönetilen uygulama**.

   ![Hizmet Kataloğu yönetilen uygulama](./media/managed-application-consumption/create-service-catalog-managed-application.png)

1. Select hello toocreate kullanılabilir çözümler hello listesinden istediğiniz uygulama yönetiliyor. **Oluştur**’u seçin.

   ![Yönetilen uygulama seçimi](./media/managed-application-consumption/select-offer.png)

1. Gerekli tooprovision hello kaynakları hello parametreleri için değerleri girin. Seçin **Batı Orta ABD** konumu. **Tamam**’ı seçin.

   ![Yönetilen uygulama parametreleri](./media/managed-application-consumption/input-parameters.png)

1. Merhaba şablon sağladığınız hello değerleri doğrular. Doğrulama başarılı olursa seçin **Tamam** toostart hello dağıtım.

   ![Yönetilen uygulama doğrulama](./media/managed-application-consumption/validation.png)

Merhaba dağıtım tamamlandıktan sonra hello uygun kaynaklara hello şablonda tanımlanan sağladığınız hello yönetilen kaynak grubunda sağlanır.

## <a name="create-hello-managed-application-by-using-azure-cli"></a>Azure CLI kullanarak yönetilen Merhaba uygulaması oluşturma

Vardır iki yolu toocreate yönetilen bir uygulamaya Azure CLI kullanarak:

* Yönetilen uygulamalar oluşturmak için Hello komutunu kullanın.
* Merhaba Normal şablon dağıtımı komutunu kullanın.

### <a name="use-hello-template-deployment-command"></a>Merhaba şablon dağıtımı komutunu kullanın

Oluşturulan satıcı hello hello applianceMainTemplate.json dosyasını dağıtın.

Daha sonra iki kaynak grubu oluşturun. Merhaba ilk kaynak grubu burada hello yönetilen uygulama kaynağı oluşturulur: Microsoft.Solutions/appliances. Merhaba ikinci kaynak grubu mainTemplate.json içinde tanımlanan tüm hello kaynaklar içeriyor. Bu kaynak grubu hello ISV tarafından yönetilir.

```azurecli
az group create --name mainResourceGroup --location westcentralus
az group create --name managedResourceGroup --location westcentralus
```

> [!NOTE]
> Kullanım `westcentralus` hello kaynak grubunun hello konumu olarak.
>

toodeploy applianceMainTemplate.json mainResourceGroup, komutu aşağıdaki kullanım hello içinde:

```azurecli
az group deployment create --name managedAppDeployment --resourceGroup mainResourceGroup --templateUri
```

Şablon çalıştırır önceki hello sonra onu hello hello şablonunda tanımlanan hello parametrelerinin değerlerini ister. Ayrıca bir şablon tooprovision kaynaklarında toohello Parametreler gerekli, iki anahtar parametre değerlerini gerekir:

- **managedResourceGroupId**: applianceMainTemplate.json içinde tanımlanan hello kaynak grubu içeren hello kaynaklara Kimliğini hello. Merhaba kimliğidir hello biçiminde `/subscriptions/{subscriptionId}/resourceGroups/{resoureGroupName}`. Örnek önceki hello hello Kimliğini kullanıcının `managedResourceGroup`.
- **applianceDefinitionId**: hello hello Kimliğini yönetilen uygulama tanımı kaynağı. Bu değer hello ISV tarafından sağlanır.

> [!NOTE]
> Merhaba yayımcı hello yönetilen uygulama tanımını içeren toohello kaynak grubu erişim vermeniz gerekir. Merhaba tanımı kaynak hello yayımcı abonelikte oluşturulur. Bu nedenle, bir kullanıcı, kullanıcı grubu veya hello müşteri Kiracı uygulamada okuma erişimi toothis kaynak gerekir.

Merhaba dağıtım başarıyla tamamlandıktan sonra yönetilen hello bkz uygulama mainResourceGroup içinde oluşturulur. Merhaba storageAccount kaynak managedResourceGroup içinde oluşturulur.

### <a name="use-hello-create-command"></a>Kullanım hello Oluştur komutu

Merhaba kullanabilirsiniz `az managedapp create` komutu toocreate hello yönetilen bir uygulamadan yönetilen uygulama tanımı.

```azurecli
az managedapp create --name ravtestappliance401 --location "westcentralus"
    --kind "Servicecatalog" --resource-group "ravApplianceCustRG401"
    --managedapp-definition-id "/subscriptions/{guid}/resourceGroups/ravApplianceDefRG401/providers/Microsoft.Solutions/applianceDefinitions/ravtestAppDef401"
    --managed-rg-id "/subscriptions/{guid}/resourceGroups/ravApplianceCustManagedRG401"
    --parameters "{\"storageAccountName\": {\"value\": \"ravappliancedemostore1\"}}"
    --debug
```

* **Gereci tanımı kimliği**: hello hello kaynak kimliği yönetilen adım önceki hello oluşturulan uygulama tanımı. tooobtain hello aşağıdaki komutu çalıştırın, bu kimliği:

  ```azurecli
  az appliance definition show -n ravtestAppDef1 -g ravApplianceRG2
  ```

  Bu komut, yönetilen hello uygulama tanımı döndürür. Merhaba kimliği özelliğinin hello değeri gerekir.

* **Yönetilen-rg-ID**: applianceMainTemplate.json içinde tanımlanan hello kaynak grubu içeren hello kaynaklara hello adı. Bu kaynak grubu hello yönetilen kaynak grubudur. Merhaba yayımcı tarafından yönetilir. Yoksa, sizin için oluşturulur.
* **kaynak grubu**: hello Uygulama kaynağı yönetildiği hello kaynak grubu oluşturulur. Bu kaynak grubunda Hello Microsoft.Solutions/appliance kaynak yaşar.
* **parametreleri**: Merhaba applianceMainTemplate.json içinde tanımlanan hello kaynaklar için gerekli olan parametreleri.

## <a name="known-issues"></a>Bilinen sorunlar

Bu önizleme sürümü sorunları aşağıdaki hello içerir:

* Yönetilen Merhaba uygulaması hello oluşturma sırasında 500 İç sunucu hatası görüntülenir. Bu sorunu yaşayıp çalıştırmak, büyük olasılıkla toobe aralıklı olur. Merhaba işlemi yeniden deneyin.
* Yeni bir kaynak grubu hello yönetilen kaynak grubu için gereklidir. Varolan bir kaynak grubu kullanıyorsanız, hello dağıtımı başarısız olur.
* Merhaba hello Microsoft.Solutions/appliances kaynak içeren kaynak grubunu hello oluşturulmalıdır **westcentralus** konumu.

## <a name="next-steps"></a>Sonraki adımlar

* Bir giriş toomanaged uygulamalar için bkz [yönetilen uygulama genel bakış](managed-application-overview.md).
* Hizmet Kataloğu yönetilen uygulama yayımlama hakkında daha fazla bilgi için bkz: [oluşturma ve bir hizmet Kataloğu yönetilen uygulamayı yayımlayın](managed-application-publishing.md).
* Yönetilen uygulamaların toohello Azure Marketi'nde yayımlama hakkında daha fazla bilgi için bkz: [Azure hello Market uygulamalarda yönetilen](managed-application-author-marketplace.md).
* Merhaba Market yönetilen bir uygulamadan kullanma hakkında daha fazla bilgi için bkz: [tüketen Azure hello Market uygulamalarda yönetilen](managed-application-consume-marketplace.md).
