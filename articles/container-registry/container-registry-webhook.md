---
title: "Azure kapsayıcı kayıt defteri kancalarını | Microsoft Docs"
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
ms.openlocfilehash: d0190f5725671c320d92b897f0dcef7a526a86e3
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/29/2017
---
# <a name="using-azure-container-registry-webhooks---azure-portal"></a>Azure kapsayıcı kayıt defteri kancalarını - Azure portalını kullanma

Azure kapsayıcı kayıt defteri depolar ve özel Docker kapsayıcısı görüntüleri, benzer Docker hub'a genel Docker görüntüleri depolayan şekilde yönetir. Web kancalarını belirli eylemleri, kayıt defteri depoları biri gerçekleştiğinde tetikleyici olaylar için kullanın. Web kancası kayıt defteri düzeyinde olaylara yanıt verebilir veya belirli depo etiketi kadar kapsamlı. 

Daha fazla arka plan ve kavramları için bkz: [genel bakış](./container-registry-intro.md).

## <a name="prerequisites"></a>Ön koşullar 

- Azure kapsayıcı kayıt defteri - yönetilen Azure aboneliğinizde bir yönetilen kapsayıcı kayıt oluşturun. Örneğin, Azure portalında veya Azure CLI 2.0 kullanın. 
- Docker CLI - yerel bilgisayarınıza Docker ana bilgisayar olarak ayarlayabilir ve Docker CLI komutlara erişmek için Docker altyapısına yükleyin. 

## <a name="create-webhook-azure-portal"></a>Azure portal Web kancası oluşturma

1. Azure portalında oturum açın ve Web kancalarını oluşturmak istediğiniz kayıt defteri gidin. 

2. Kapsayıcı dikey penceresinde "Kancalarını" sekmesini seçin. 

3. "Ekle" Web kancası dikey araç çubuğundan seçin. 

4. Tamamlamak *Web kancası oluşturma* form aşağıdaki bilgilerle:

| Değer | Açıklama |
|---|---|
| Ad | Web kancası için vermek istediğiniz adı. Ad yalnızca küçük harfler ve sayılar içerebilir ve 5-50 karakter arasında. |
| Hizmet URI'si | Web kancası POST bildirimleri burada göndermesi gereken URI. |
| Özel Üstbilgileri | Üstbilgiler POST istekle birlikte geçirmek isteyebilirsiniz. İçinde olmalıdır "anahtar: değer" biçimi. |
| Tetikleyici eylemleri | Web kancası tetiklemek eylemler. Şu anda Web kancalarını itme tarafından tetiklenen ve/veya görüntüye eylemlerini silme. |
| Durum | Web kancası oluşturulduktan sonra durumu. Varsayılan olarak etkindir. |
| Kapsam | Web kancası çalıştığı kapsamı. Varsayılan olarak tüm olayları kayıt defterinde kapsamı içindir. Bu depo veya bir etiket için şu biçimi kullanarak belirtilebilir "deposu: Etiket". |

Örnek Web kancası form:

![DCOS KULLANICI ARABİRİMİ](./media/container-registry-webhook/webhook.png)

## <a name="create-webhook-azure-cli"></a>Web kancası Azure CLI oluşturma

Azure CLI kullanarak bir Web kancası oluşturmak üzere kullanmanız [az acr Web kancası oluşturma](/cli/azure/acr/webhook#create) komutu.

```azurecli-interactive
az acr webhook create --registry mycontainerregistry --name myacrwebhook01 --actions delete --uri http://webhookuri.com
```

## <a name="test-webhook"></a>Test Web kancası

### <a name="azure-portal"></a>Azure portalına

Kullanarak önceki kapsayıcısı üzerinde Web kancası görüntü gönderme ve silme eylemlerini, kullanılarak sınanabilir **Ping** düğmesi. Kullanıldığında, ping işlemi için belirtilen uç nokta bir genel post isteği gönderir ve yanıt günlüğe kaydeder. Bu, Web kancası doğru şekilde ayarlanmış olması gerektiğini doğrulamak yararlıdır.

1. Test etmek istediğiniz Web kancası seçin. 
2. Üst araç çubuğunda, "Ping" eylemini seçin. 
3. İstek ve yanıt denetleyin.

### <a name="azure-cli"></a>Azure CLI

Azure CLI ile bir ACR Web kancası sınamak için kullanın [az acr Web kancası ping](/cli/azure/acr/webhook#ping) komutu.

```azurecli-interactive
az acr webhook ping --registry mycontainerregistry --name myacrwebhook01
```

Sonuçları görmek için [az acr Web kancası listesi-olayları](/cli/azure/acr/webhook#list-events) komutu. 

```azurecli-interactive
az acr webhook list-events --registry mycontainerregistry08 --name myacrwebhook01
```

## <a name="delete-webhook"></a>Web kancası silme

### <a name="azure-portal"></a>Azure portalına

Her Web kancası Web kancası ve Azure Portal'da Sil düğmesini seçerek silinebilir.

### <a name="azure-cli"></a>Azure CLI

```azurecli-interactive
az acr webhook delete --registry mycontainerregistry --name myacrwebhook01
```