---
title: "aaaAzure kapsayıcı kayıt defteri kancalarını | Microsoft Docs"
description: "Azure kapsayıcı kayıt defteri Web kancaları"
services: container-registry
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acr, azure-container-registry
keywords: "Docker, kapsayıcıları, ACR"
ms.assetid: 
ms.service: container-registry
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/06/2017
ms.author: nepeters
ms.openlocfilehash: adc2afec486007e2d54cd689e6f7ef8b1098db06
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-container-registry-webhooks---azure-portal"></a>Azure kapsayıcı kayıt defteri kancalarını - Azure portalını kullanma

Azure kapsayıcı kayıt defteri depolar ve özel Docker kapsayıcısı görüntüleri, Docker hub'a genel Docker görüntüleri depolayan benzer toohello şekilde yönetir. Bazı Eylemler, kayıt defteri depoları biri gerçekleştiğinde Web kancalarını tootrigger olayları kullanın. Web kancası tooevents hello kayıt defteri düzeyinde yanıt verebilir veya tooa belirli depo etiketi kapsamlı. 

Daha fazla arka plan ve kavramları hello bkz [genel bakış](./container-registry-intro.md).

## <a name="prerequisites"></a>Ön koşullar 

- Azure kapsayıcı kayıt defteri - yönetilen Azure aboneliğinizde bir yönetilen kapsayıcı kayıt oluşturun. Örneğin, hello Azure portal kullanın veya Azure CLI 2.0 hello. 
- Docker CLI - yerel bilgisayarınızı bir Docker ana bilgisayar ve erişim hello Docker CLI komutları olarak tooset Docker altyapısına yükleyin. 

## <a name="create-webhook-azure-portal"></a>Azure portal Web kancası oluşturma

1. Toohello Azure portalında oturum açın ve toocreate kancalarını istediğiniz toohello kayıt defteri gidin. 

2. Merhaba kapsayıcı dikey penceresinde hello "Kancalarını" sekmesini seçin. 

3. "Ekle" Merhaba Web kancası dikey araç çubuğundan seçin. 

4. Tam hello *Web kancası oluşturma* bilgisinden hello formla:

| Değer | Açıklama |
|---|---|
| Ad | toogive toohello Web kancası istediğiniz hello adı. Ad yalnızca küçük harfler ve sayılar içerebilir ve 5-50 karakter arasında. |
| Hizmet URI'si | Merhaba URI burada hello Web kancası POST bildirimlerini göndermesi gerekir. |
| Özel Üstbilgileri | Merhaba POST isteği birlikte toopass istediğiniz üstbilgileri. İçinde olmalıdır "anahtar: değer" biçimi. |
| Tetikleyici eylemleri | Merhaba Web kancası tetiklemek eylemler. Şu anda Web kancalarını itme tarafından tetiklenen ve/veya Eylemler tooan resmini silin. |
| Durum | Merhaba Web kancası oluşturulduktan sonra başlangıç durumu. Varsayılan olarak etkindir. |
| Kapsam | hangi hello Web kancası works kapsamda Hello. Varsayılan olarak tüm olayları hello kayıt defterinde hello kapsam içindir. Bu depo veya bir etiket için hello biçimi kullanılarak belirtilebilir "deposu: Etiket". |

Örnek Web kancası form:

![DCOS KULLANICI ARABİRİMİ](./media/container-registry-webhook/webhook.png)

## <a name="create-webhook-azure-cli"></a>Web kancası Azure CLI oluşturma

kullanarak bir Web kancası toocreate hello Azure CLI, kullanım hello [az acr Web kancası oluşturma](/cli/azure/acr/webhook#create) komutu.

```azurecli-interactive
az acr webhook create --registry mycontainerregistry --name myacrwebhook01 --actions delete --uri http://webhookuri.com
```

## <a name="test-webhook"></a>Test Web kancası

### <a name="azure-portal"></a>Azure portalına

Önceki toousing hello Web kancası kapsayıcısı üzerinde görüntü gönderme ve silme eylemlerini, hello kullanılarak sınanabilir **Ping** düğmesi. Kullanıldığında, uç nokta ve günlükleri yanıt hello genel post isteği toohello belirtilen hello Ping gönderir. Bu yararlı olur Web kancası hello tooverify doğru şekilde ayarlanmış.

1. Merhaba Web kancası tootest istediğinizi seçin. 
2. Merhaba üst araç çubuğunda hello "Ping" eylemini seçin. 
3. Merhaba istek ve yanıt denetleyin.

### <a name="azure-cli"></a>Azure CLI

tootest bir ACR Web kancası hello Azure CLI ile kullanmak hello [az acr Web kancası ping](/cli/azure/acr/webhook#ping) komutu.

```azurecli-interactive
az acr webhook ping --registry mycontainerregistry --name myacrwebhook01
```

toosee hello sonuçları kullanmak hello [az acr Web kancası listesi-olayları](/cli/azure/acr/webhook#list-events) komutu. 

```azurecli-interactive
az acr webhook list-events --registry mycontainerregistry08 --name myacrwebhook01
```

## <a name="delete-webhook"></a>Web kancası silme

### <a name="azure-portal"></a>Azure portalına

Her Web kancası hello Web kancası ve hello Azure portal hello Sil düğmesini seçerek silinebilir.

### <a name="azure-cli"></a>Azure CLI

```azurecli-interactive
az acr webhook delete --registry mycontainerregistry --name myacrwebhook01
```