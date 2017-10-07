---
title: "aaaCreate özel Docker kayıt defteri - Azure portalı | Microsoft Docs"
description: "Oluşturma ve yönetme özel Docker kapsayıcısı kayıt defterleri hello Azure portal ile çalışmaya başlama"
services: container-registry
documentationcenter: 
author: neilpeterson
manager: timlt
editor: na
tags: 
keywords: 
ms.assetid: 53a3b3cb-ab4b-4560-bc00-366e2759f1a1
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: nepeters
ms.custom: na
ms.openlocfilehash: cf3ce0dcf3036d0e9cd1eaf01721deccb00248d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-container-registry-using-hello-azure-portal"></a>Hello Azure portal kullanarak bir yönetilen kapsayıcı kayıt defteri oluşturma

Azure Container Registry, özel Docker kapsayıcı görüntülerini depolamak için kullanılan bir yönetilen Docker kapsayıcı kayıt defteridir. Bu kılavuzu ayrıntıları Hello Azure portal kullanarak yönetilen Azure kapsayıcı kayıt defteri örneği oluşturma.

Yönetilen Azure kapsayıcı kayıt defterleri önizleme aşamasındadır ve tüm bölgelerde kullanılamaz.

## <a name="log-in-tooazure"></a>İçinde tooAzure oturum

İçinde toohello http://portal.azure.com Azure portalında oturum açın.

## <a name="create-a-container-registry"></a>Kapsayıcı kayıt defteri oluşturma

1. Merhaba tıklatın **yeni** düğmesi hello sol üst köşesinin hello Azure portalı üzerinde bulunamadı.

2. Arama hello Market **Azure kapsayıcı kayıt defteri** ve seçin.

3. Tıklatın **oluşturma** hello ACR oluşturma dikey penceresi açılır.

    ![Container kayıt defteri ayarları](./media/container-registry-get-started-portal/managed-container-registry-settings.png)

4. Merhaba, **Azure kapsayıcı kayıt defteri** dikey penceresinde, aşağıdaki bilgilerle hello girin. İşiniz bittiğinde **Oluştur**’a tıklayın.

    a. **Kayıt defteri adı**: Oluşturduğunuz kayıt defterinize özel olan, genel olarak benzersiz bir üst düzey etki alanı adı. Bu örnekte hello kayıt defteri adıdır *myAzureContainerRegistry1*, ancak kendi benzersiz adı değiştirin. Merhaba ad yalnızca harfler ve sayılar içerebilir.

    b. **Kaynak grubu**: Varolan seçin [kaynak grubu](../azure-resource-manager/resource-group-overview.md#resource-groups) veya yeni bir hello adını yazın.

    c. **Konum**: hello hizmet olduğu bir Azure veri merkezi konum seçin [kullanılabilir](https://azure.microsoft.com/regions/services/), gibi **Orta Güney ABD**.

    d. **Yönetici kullanıcı**: istiyorsanız, bir yönetici kullanıcı tooaccess hello kayıt defteri etkinleştirin. Merhaba kayıt defteri oluşturduktan sonra bu ayarı değiştirebilirsiniz.

    e. **Kullanım yönetilen kayıt defteri**: Evet'i seçin toohave ACR otomatik olarak hello kayıt defteri depolama yönetin, Web kancası kullanın ve AAD kimlik doğrulaması kullanın.

    f. **Fiyatlandırma Katmanı**: Fiyatlandırma katmanını seçin; daha fazla bilgi için buradaki ACR fiyatlandırma bölümüne bakın.

## <a name="log-in-tooacr-instance"></a>TooACR örneğinde oturum

İletme ve kapsayıcı görüntüleri çekme önce toohello ACR örneğinde oturum açmanız gerekir. 

toodo, bu nedenle, hello Azure CLI 2.0 kullanın. İlk olarak, gerekirse, hello kullanarak Azure'da oturum [az oturum açma](/cli/azure/#login) komutu. 

```azurecli
az login
```

Ardından, hello kullanın [az acr oturum açma](/cli/azure/acr#login) toohello Azure kapsayıcı kayıt defteri, komut toolog.

```azurecli-interactive
az acr login --name myAzureContainerRegistry1
```

## <a name="use-azure-container-registry"></a>Azure Container Registry’yi kullanma

### <a name="list-container-images"></a>Kapsayıcı görüntülerini listeleme

Kullanım hello `az acr` CLI komutları tooquery hello görüntüleri ve bir havuzda etiketler.

> [!NOTE]
> Şu anda, kapsayıcı kayıt defteri hello desteklemiyor `docker search` komutu tooquery görüntüler ve etiketler için.

### <a name="list-repositories"></a>Depoları listeleme

Merhaba aşağıdaki örnek JSON (JavaScript nesne gösterimi) biçiminde bir kayıt defterindeki hello depoları listeler:

```azurecli
az acr repository list -n myContainerRegistry1 -o json
```

### <a name="list-tags"></a>Etiketleri listeleme

Merhaba aşağıdaki örnek listeler hello hello etiketlerini **samples/nginx** JSON biçiminde deposu:

```azurecli
az acr repository show-tags -n myContainerRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a>Sonraki adımlar

Bu hızlı başlangıç bölümünde hello Azure portal kullanarak yönetilen Azure kapsayıcı kayıt defteri örneği oluşturduğunuzu düşünün.

> [!div class="nextstepaction"]
> [Merhaba Docker CLI kullanarak ilk görüntünüzü bildirme](container-registry-get-started-docker-cli.md)
