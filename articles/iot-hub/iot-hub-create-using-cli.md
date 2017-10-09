---
title: Azure CLI (az.py) kullanarak bir IOT Hub aaaCreate | Microsoft Docs
description: "Nasıl bir Azure IOT hub'ı kullanarak toocreate hello platformlar arası Azure CLI 2.0 (az.py)."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 
ms.service: iot-hub
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.openlocfilehash: 9c9639235c2ac343e6ceb9578291dafaea26ea24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-azure-cli-20"></a>Hello Azure CLI 2.0 kullanarak IOT hub oluşturma

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a>Giriş

Azure CLI 2.0 (az.py) toocreate kullanın ve Azure IOT hub'ları program aracılığıyla yönetebilirsiniz. Bu makale size nasıl toouse hello Azure CLI 2.0 (az.py) toocreate IOT hub'ı gösterir.

CLI sürümleri aşağıdaki hello birini kullanarak hello görevi tamamlamak:

* [Azure CLI (azure.js)](iot-hub-create-using-cli-nodejs.md) – hello Klasik ve kaynak yönetimi dağıtım modelleri için CLI hello.
* Azure CLI 2.0 (az.py) - Bu makalede anlatıldığı gibi hello kaynak yönetimi dağıtım modeli için yeni nesil CLI hello.

toocomplete Bu öğretici, aşağıdaki hello gerekir:

* Etkin bir Azure hesabı. Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.
* [Azure CLI 2.0][lnk-CLI-install].

## <a name="sign-in-and-set-your-azure-account"></a>Oturum açma ve Azure hesabınızı ayarlama

Tooyour Azure hesabı oturum ve aboneliğinizi seçin.

1. Merhaba Hello komut isteminde çalıştırmak [oturum açma komut][lnk-login-command]:
    
    ```azurecli
    az login
    ```

    Merhaba yönergeleri tooauthenticate Hello kod kullanarak izleyin ve oturum açma tooyour bir web tarayıcısı aracılığıyla Azure hesabı.

2. Birden çok Azure aboneliğiniz varsa tooAzure imzalama tooall erişim verir kimlik bilgilerinizle ilişkili Azure hesapları hello. Merhaba aşağıdaki kullanın [komutu toolist hello Azure hesapları] [ lnk-az-account-command] , toouse için kullanılabilir:
    
    ```azurecli
    az account list 
    ```

    IOT hub'ınızı toocreate toouse toorun hello komutları istediğiniz komut tooselect abonelik aşağıdaki hello kullanın. Merhaba hello önceki komutunun çıktısından hello abonelik adı veya kimliği kullanabilirsiniz:

    ```azurecli
    az account set --subscription {your subscription name or id}
    ```

## <a name="create-an-iot-hub"></a>IOT Hub oluşturma

Hello Azure CLI toocreate bir kaynak grubu ve IOT hub'ı ekleyin.

1. IOT hub'ı oluşturduğunuzda, bir kaynak grubunda oluşturmanız gerekir. Var olan bir kaynak grubunu kullanabilir veya hello aşağıdaki komutu çalıştırarak [komutu toocreate bir kaynak grubu][lnk-az-resource-command]:
    
    ```azurecli
     az group create --name {your resource group name} --location westus
    ```

    > [!TIP]
    > Merhaba önceki örnek hello Batı ABD konumu hello kaynak grubu oluşturur. Merhaba komutu çalıştırarak kullanılabilir konumların bir listesini görüntüleyebilirsiniz `az account list-locations -o table`.
    >
    >

2. Merhaba aşağıdaki komutu çalıştırarak [komutu toocreate IOT hub'ı] [ lnk-az-iot-command] kaynak grubunuzdaki IOT hub'ınız için genel benzersiz bir ad kullanarak:
    
    ```azurecli
    az iot hub create --name {your iot hub name} --resource-group {your resource group name} --sku S1
    ```

   [!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]


> [!NOTE]
> Merhaba önceki komutu fiyatlandırma katmanı için faturalandırılır hello S1 IOT hub'ı oluşturur. Daha fazla bilgi için bkz: [Azure IOT Hub fiyatlandırma][lnk-iot-pricing].
>
>

## <a name="remove-an-iot-hub"></a>IOT hub'ı kaldırma

Hello Azure CLI kullanabileceğine[tek başına bir kaynak silme][lnk-az-resource-command]bir IOT hub'ı veya silme gibi bir kaynak grubu ve tüm IOT hub'ları da dahil olmak üzere tüm kaynaklarını,.

bir IOT hub toodelete hello aşağıdaki komutu çalıştırın:

```azurecli
az iot hub delete --name {your iot hub name} --resource-group {your resource group name}
```

bir kaynak grubu ve tüm kaynaklarını, aşağıdaki çalışma hello komutu toodelete:

```azurecli
az group delete --name {your resource group name}
```

## <a name="next-steps"></a>Sonraki adımlar
IOT hub'ı geliştirme hakkında daha fazla toolearn makaleler hello bakın:

* [IOT Hub Geliştirici Kılavuzu][lnk-devguide]

toofurther IOT hub'ı hello özelliklerini keşfedin, bakın:

* [Hello Azure portal toomanage IOT hub'ı kullanma][lnk-portal]

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-CLI-install]: https://docs.microsoft.com/cli/azure/install-az-cli2
[lnk-login-command]: https://docs.microsoft.com/cli/azure/get-started-with-az-cli2
[lnk-az-account-command]: https://docs.microsoft.com/cli/azure/account
[lnk-az-register-command]: https://docs.microsoft.com/cli/azure/provider
[lnk-az-addcomponent-command]: https://docs.microsoft.com/cli/azure/component
[lnk-az-resource-command]: https://docs.microsoft.com/cli/azure/resource
[lnk-az-iot-command]: https://docs.microsoft.com/cli/azure/iot
[lnk-iot-pricing]: https://azure.microsoft.com/pricing/details/iot-hub/
[lnk-devguide]: iot-hub-devguide.md
[lnk-portal]: iot-hub-create-through-portal.md 
