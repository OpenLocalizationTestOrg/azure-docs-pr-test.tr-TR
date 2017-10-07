---
title: Azure CLI (azure.js) kullanarak bir IOT hub aaaCreate | Microsoft Docs
description: "Nasıl bir Azure IOT hub'ı kullanarak toocreate hello platformlar arası Azure CLI (azure.js)."
services: iot-hub
documentationcenter: .net
author: BeatriceOltean
manager: timlt
editor: 
ms.assetid: 46a17831-650c-41d9-b228-445c5bb423d3
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/04/2017
ms.author: boltean
ms.openlocfilehash: c2a7ea98500b0a0e55a39f4cdfea4605c92add94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-azure-cli"></a>Hello Azure CLI kullanarak IOT hub oluşturma

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a>Giriş

Azure CLI (azure.js) toocreate kullanın ve Azure IOT hub'ları program aracılığıyla yönetebilirsiniz. Bu makale size nasıl toouse hello Azure CLI (azure.js) toocreate IOT hub'ı gösterir.

CLI sürümleri aşağıdaki hello birini kullanarak hello görevi tamamlamak:

* Azure CLI (azure.js) – hello CLI hello Klasik ve bu makalede anlatıldığı gibi kaynak yönetimi dağıtım modelleri için.
* [Azure CLI 2.0 (az.py)](iot-hub-create-using-cli.md) -hello kaynak yönetimi dağıtım modeli için yeni nesil CLI hello.

toocomplete Bu öğretici, aşağıdaki hello gerekir:

* Etkin bir Azure hesabı. Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.
* [Azure CLI 0.10.4] [ lnk-CLI-install] veya sonraki bir sürümü. Hello Azure CLI yüklenmiş zaten varsa, komutu aşağıdaki hello ile Merhaba geçerli sürümü hello komut isteminde doğrulayabilirsiniz:

```azurecli
azure --version
```

> [!NOTE]
> Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Azure Resource Manager ve klasik](../azure-resource-manager/resource-manager-deployment-model.md). Hello Azure CLI, Azure Kaynak Yöneticisi modunda olması gerekir:
>
> ```azurecli
> azure config mode arm
> ```

## <a name="set-your-azure-account-and-subscription"></a>Azure hesabınızı ve aboneliğinizi ayarlama

1. Merhaba komut isteminde, komutu aşağıdaki hello yazarak oturum açma:

   ```azurecli
    azure login
   ```

   Merhaba önerilen web tarayıcısı ve kod tooauthenticate kullanın.
1. Birden çok Azure aboneliğiniz varsa, tooAzure bağlanma verir tooall erişim kimlik bilgilerinizle ilişkili Azure abonelik hello. Görüntüleyebileceğiniz Azure abonelikleri hello ve hangisinin hello komutunu kullanarak Merhaba, varsayılandır belirleyin:

   ```azurecli
    azure account list
   ```

   tooset hello abonelik bağlam altında toorun hello kalan hello komutlarını kullanmak istediğiniz:

   ```azurecli
    azure account set <subscription name>
   ```

1. Bir kaynak grubu yoksa, bir adlı oluşturabilirsiniz **exampleResourceGroup**:

   ```azurecli
    azure group create -n exampleResourceGroup -l westus
   ```

> [!TIP]
> Hello makale [hello Azure CLI toomanage Azure kullanmak kaynaklar ve kaynak grupları] [ lnk-CLI-arm] nasıl toouse hello Azure CLI toomanage Azure hakkında daha fazla bilgi sağlayan kaynakları.

## <a name="create-an-iot-hub"></a>IOT Hub oluşturma

Gerekli Parametreler:

```azurecli
azure iothub create -g <resource-group> -n <name> -l <location> -s <sku-name> -u <units>
```

* **kaynak grubu**. Merhaba kaynak grubu adı. Merhaba büyük küçük harfe duyarlı alfasayısal, alt çizgi ve tire, 1-64 uzunluğu biçimidir.
* **name**. oluşturulan hello IOT hub toobe Hello adı. Merhaba büyük küçük harfe duyarlı alfasayısal, alt çizgi ve tire, 3-50 uzunluğu biçimidir.
* **Konum**. Başlangıç konumu (azure bölge/veri merkezi) tooprovision hello IOT hub.
* **SKU adı**. Merhaba SKU'su, aşağıdakilerden birini Hello adı: [F1, S1, S2, S3]. Merhaba en son tam listesi için fiyatlandırma sayfası için IOT Hub toohello bakın.
* **birimleri**. sağlanan birimleri Hello sayısı. Aralık: F1 [1-1]: S1, S2 [1-200]: [1-10] S3. IOT Hub birimleri toplam ileti sayısı ve hello sayısı aygıtlar üzerinde tooconnect istiyor.

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

toosee tüm oluşturma için kullanılabilen parametreleri Merhaba, komut istemi'nde hello Yardım komutunu kullanabilirsiniz:

```azurecli
azure iothub create -h
```

Örnek: bir IOT Hub adı verilen toocreate **exampleIoTHubName** hello kaynak grubunda **exampleResourceGroup**çalıştırın hello komutu aşağıdaki:

```azurecli
azure iothub create -g exampleResourceGroup -n exampleIoTHubName -l westus -k s1 -u 1
```

> [!NOTE]
> Bu Azure CLI komut S1 standart IOT için faturalandırılır hub'ı oluşturur. Merhaba IOT hub'ı silebilmek için **exampleIoTHubName** komutu kullanarak:
>
> ```azurecli
> azure iothub delete -g exampleResourceGroup -n exampleIoTHubName
> ```

## <a name="next-steps"></a>Sonraki adımlar

IOT hub'ı geliştirme hakkında daha fazla toolearn aşağıdaki makaleye bakın hello bakın:

* [IOT SDK'ları][lnk-sdks]

toofurther IOT hub'ı hello özelliklerini keşfedin, bakın:

* [Hello Azure portal toomanage IOT hub'ı kullanma][lnk-portal]

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-azure-portal]: https://portal.azure.com/
[lnk-status]: https://azure.microsoft.com/status/
[lnk-CLI-install]:../cli-install-nodejs.md
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-CLI-arm]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md

[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-portal]: iot-hub-create-through-portal.md 
