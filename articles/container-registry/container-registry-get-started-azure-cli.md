---
title: "aaaCreate özel Docker kapsayıcısı kayıt defteri - Azure CLI | Microsoft Docs"
description: "Oluşturma ve yönetme özel Docker kapsayıcısı kayıt defterleri hello Azure CLI 2.0 ile çalışmaya başlama"
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: cristyg
tags: 
keywords: 
ms.assetid: 29e20d75-bf39-4f7d-815f-a2e47209be7d
ms.service: container-registry
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/06/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f0d876a70b71a5e1bd564fbc9198f693dfe8a347
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-private-docker-container-registry-using-hello-azure-cli-20"></a>Hello Azure CLI 2.0 kullanarak özel bir Docker kapsayıcısı kayıt oluşturun
Hello komutlarını kullanmak [Azure CLI 2.0](https://github.com/Azure/azure-cli) toocreate bir kapsayıcı kayıt defteri ve Linux, Mac veya Windows bilgisayarınızdan ayarlarını yönetin. Ayrıca oluşturmak ve kapsayıcı kayıt defterleri hello kullanarak yönetmek [Azure portal](container-registry-get-started-portal.md) veya program aracılığıyla hello kapsayıcı kayıt defteri [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376).


* Arka plan ve kavramları için bkz: [hello genel bakış](container-registry-intro.md)
* Kapsayıcı kayıt defteri CLI komutlar hakkında Yardım almak için (`az acr` komutları), hello geçirmek `-h` parametresi tooany komutu.


## <a name="prerequisites"></a>Ön koşullar
* **Azure CLI 2.0**: tooinstall ve hello CLI 2.0 ile çalışmaya başlama bkz hello [yükleme yönergeleri](/cli/azure/install-azure-cli). Çalıştırarak tooyour Azure aboneliği oturum `az login`. Daha fazla bilgi için bkz: [hello CLI 2.0 ile çalışmaya başlama](/cli/azure/get-started-with-azure-cli).
* **Kaynak grubu**: Kapsayıcı kayıt defteri oluşturmadan önce bir [kaynak grubu](../azure-resource-manager/resource-group-overview.md#resource-groups) oluşturun veya mevcut bir kaynak grubunu kullanın. Merhaba kaynak grubu hello kapsayıcı kayıt defteri hizmeti olduğu bir konumda olduğundan emin olun [kullanılabilir](https://azure.microsoft.com/regions/services/). kullanarak bir kaynak grubu toocreate hello CLI 2.0 bkz [hello CLI 2.0 başvurusu](/cli/azure/group).
* **Depolama hesabı** (isteğe bağlı): bir standart Azure oluşturma [depolama hesabı](../storage/common/storage-introduction.md) tooback hello kapsayıcı hello kayıt defterinde aynı konumu. Kayıt defteri ile oluştururken, bir depolama hesabı belirtmezseniz `az acr create`, hello komut sizin için bir tane oluşturur. bir depolama hesabı kullanarak toocreate CLI 2.0 Merhaba, bkz: [hello CLI 2.0 başvurusu](/cli/azure/storage/account). Premium Depolama şu anda desteklenmemektedir.
* **Hizmet sorumlusu** (isteğe bağlı): bir kayıt defteri hello CLI ile oluşturduğunuzda, varsayılan olarak, erişim için kurulu değil. Gereksinimlerinize bağlı olarak, varolan bir Azure Active Directory hizmet asıl tooa kayıt atayabilirsiniz (veya oluşturun ve yeni bir ata), veya hello kayıt defterindeki yönetici kullanıcı hesabını etkinleştirin. Bu makalenin sonraki bölümlerinde Hello bölümlere bakın. Kayıt defteri erişim hakkında daha fazla bilgi için bkz: [hello kapsayıcı kayıt defteri ile kimlik doğrulama](container-registry-authentication.md).

## <a name="create-a-container-registry"></a>Kapsayıcı kayıt defteri oluşturma
Merhaba çalıştırmak `az acr create` komutu toocreate bir kapsayıcı kayıt defteri.

> [!TIP]
> Bir kayıt defteri oluştururken yalnızca harf ve sayı içeren genel olarak benzersiz bir üst düzey etki alanı adı sağlayın. Merhaba kayıt defteri adı hello örneklerde `myRegistry1`, ancak kendi benzersiz adı değiştirin.
>
>

kullandığı hello en az parametreleri toocreate kapsayıcı kayıt defteri komutu aşağıdaki hello `myRegistry1` hello kaynak grubunda `myResourceGroup`ve hello kullanarak *temel* sku:

```azurecli
az acr create --name myRegistry1 --resource-group myResourceGroup --sku Basic
```

* `--storage-account-name` isteğe bağlıdır. Yoksa belirtilen hello kayıt defteri adını oluşan bir ada sahip bir depolama hesabı oluşturulur ve kaynak grubu bir zaman damgasına hello belirtilen.

Merhaba kayıt oluşturulduğunda hello çıkış benzer toohello aşağıda verilmiştir:

```azurecli
{
  "adminUserEnabled": false,
  "creationDate": "2017-06-06T18:36:29.124842+00:00",
  "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myResourceGroup/providers/Microsoft.ContainerRegistry
/registries/myRegistry1",
  "location": "southcentralus",
  "loginServer": "myregistry1.azurecr.io",
  "name": "myRegistry1",
  "provisioningState": "Succeeded",
  "sku": {
    "name": "Basic",
    "tier": "Basic"
  },
  "storageAccount": {
    "name": "myregistry123456789"
  },
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}

```


Özellikle şunlara dikkat edin:

* `id`-Tooassign bir hizmet sorumlusu istiyorsanız, gereksinim duyduğunuz aboneliğinizde hello kayıt defteri tanıtıcısı.
* `loginServer`-Belirttiğiniz çok hello tam adı[toohello kayıt defterinde oturum](container-registry-authentication.md). Bu örnekte, hello adıdır `myregistry1.exp.azurecr.io` (tüm küçük harf).

## <a name="assign-a-service-principal"></a>Hizmet sorumlusu atama
CLI 2.0 komutları tooassign bir Azure Active Directory hizmet asıl tooa kayıt defteri kullanın. Merhaba hizmet sorumlusu Bu örneklerde hello sahibi rolü atanmış, ancak atayabilirsiniz [diğer rolleri](../active-directory/role-based-access-control-configure.md) istiyorsanız.

### <a name="create-a-service-principal-and-assign-access-toohello-registry"></a>Bir hizmet sorumlusu oluşturun ve erişim toohello kayıt defteri atayın
Komutu aşağıdaki hello, yeni bir hizmet sorumlusu sahibi rolü erişim toohello kayıt defteri tanımlayıcısı ile Merhaba geçirilen atanır `--scopes` parametresi. Güçlü bir parola ile Merhaba belirtin `--password` parametresi.

```azurecli
az ad sp create-for-rbac --scopes /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myresourcegroup/providers/Microsoft.ContainerRegistry/registries/myregistry1 --role Owner --password myPassword
```



### <a name="assign-an-existing-service-principal"></a>Mevcut bir hizmet sorumlusunu atama
Zaten bir hizmet sorumlusu varsa ve tooassign istiyorsanız, aşağıdaki örnek komut benzer toohello çalıştırmak sahibi rolü erişim toohello kayıt defteri,. Hello kullanarak hello hizmet asıl uygulama kimliği geçirdiğiniz `--assignee` parametre:

```azurecli
az role assignment create --scope /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myresourcegroup/providers/Microsoft.ContainerRegistry/registries/myregistry1 --role Owner --assignee myAppId
```



## <a name="manage-admin-credentials"></a>Yönetici kimlik bilgilerini yönetme
Her kapsayıcı kayıt defteri için otomatik olarak bir yönetici hesabı oluşturulur ve varsayılan olarak devre dışı bırakılır. Aşağıdaki örneklerde gösterildiği hello `az acr` CLI komutları kapsayıcı kaydınız toomanage hello yönetici kimlik bilgileri.

### <a name="obtain-admin-user-credentials"></a>Yönetici kullanıcı kimlik bilgileri edinme
```azurecli
az acr credential show -n myRegistry1
```

### <a name="enable-admin-user-for-an-existing-registry"></a>Mevcut bir kayıt defteri için yönetici kullanıcıyı etkinleştirme
```azurecli
az acr update -n myRegistry1 --admin-enabled true
```

### <a name="disable-admin-user-for-an-existing-registry"></a>Mevcut bir kayıt defteri için yönetici kullanıcıyı devre dışı bırakma
```azurecli
az acr update -n myRegistry1 --admin-enabled false
```

## <a name="list-images-and-tags"></a>Görüntüleri ve etiketleri listeleme
Kullanım hello `az acr` CLI komutları tooquery hello görüntüleri ve bir havuzda etiketler.

> [!NOTE]
> Şu anda, kapsayıcı kayıt defteri hello desteklemiyor `docker search` komutu tooquery görüntüler ve etiketler için.


### <a name="list-repositories"></a>Depoları listeleme
Merhaba aşağıdaki örnek JSON (JavaScript nesne gösterimi) biçiminde bir kayıt defterindeki hello depoları listeler:

```azurecli
az acr repository list -n myRegistry1 -o json
```

### <a name="list-tags"></a>Etiketleri listeleme
Merhaba aşağıdaki örnek listeler hello hello etiketlerini **samples/nginx** JSON biçiminde deposu:

```azurecli
az acr repository show-tags -n myRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a>Sonraki adımlar
* [Merhaba Docker CLI kullanarak ilk görüntünüzü bildirme](container-registry-get-started-docker-cli.md)
