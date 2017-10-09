---
title: "aaaAzure kapsayıcı kayıt defteri depoları | Microsoft Docs"
description: "Nasıl toouse Azure kapsayıcı kayıt defteri depoları Docker görüntüleri"
services: container-registry
documentationcenter: 
author: cristy
manager: balans
editor: dlepow
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: cristyg
ms.openlocfilehash: 108622c565e41777fbb1fc9da9a01168abc7a7fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-registry-repositories"></a>Azure kapsayıcı kayıt defteri depoları

Azure kapsayıcı kayıt defteri depoları toostore kapsayıcı görüntüleri sağlar. Depoları görüntüleri depolayarak Yalıtılmış ortamlarda görüntü (veya görüntüleri sürümü) grupları olabilir. Görüntüleri tooyour kayıt defteri bastığınızda bu depoları belirtebilirsiniz.


## <a name="prerequisites"></a>Ön koşullar
* **Azure kapsayıcısı kayıt defteri** -Azure aboneliğinizde bir kapsayıcı kayıt defteri oluşturun. Örneğin, hello kullan [Azure portal](container-registry-get-started-portal.md) veya hello [Azure CLI 2.0](container-registry-get-started-azure-cli.md).
* **Docker CLI** -tooset bir Docker ana bilgisayar ve erişim hello Docker CLI komutları olarak, yerel bilgisayarınıza yüklemek [Docker altyapısına](https://docs.docker.com/engine/installation/).
* **Bir görüntü çekme** - görüntüyü hello ortak Docker hub'a kayıt defterinden çekme etiketlemek ve tooyour kayıt defteri itme. Nasıl hakkında yönergeler için anında iletme ve çekme görüntüleri bkz [itme Docker görüntü tooAzure özel kayıt defteri](container-registry-get-started-docker-cli.md).


## <a name="viewing-repositories-in-hello-portal"></a>Depoları hello Portal görüntüleme

Görüntüleri tooyour kapsayıcı kayıt defteri gönderilen sonra hello Azure portal hello görüntülerinde barındırma hello depoları listesini görebilirsiniz.

Merhaba hello adımları izlediyseniz [anında Docker görüntü tooAzure özel kayıt defteri](container-registry-get-started-docker-cli.md) makale, kapsayıcı kayıt defterinizde Nginx görüntü şimdi olmalıdır. Merhaba yönergeleri bir parçası olarak hello görüntüsü için bir ad belirttiğinizden. Merhaba aşağıdaki örnekte, hello komutu hello NGinx görüntü toohello "örneklerini" deposuna iter:

```
docker push myregistry.azurecr.io/samples/nginx
```
 Azure Container Kayıt Defteri, çok düzeyli depo ad alanlarını destekler. Bu özellik, görüntüleri ilgili tooa belirli uygulama toogroup koleksiyonları veya uygulamaları toospecific geliştirme veya işletimsel takımlar koleksiyonunu sağlar. kapsayıcı kayıt defterleri, depoları hakkında daha fazla tooread bkz [özel Docker kapsayıcısı kayıt defterleri azure'da](container-registry-intro.md).

tooview hello kapsayıcı kayıt defteri depoları:

1. Toohello Azure portalında oturum açın
2. Merhaba üzerinde **Azure kapsayıcı kayıt defteri** dikey penceresinde, tooinspect istediğiniz select hello kayıt defteri
3. Merhaba kayıt defteri dikey penceresinde tıklayın **depoları** toosee tüm hello depoları ve resimlerinin listesi
4. (İsteğe bağlı) Özel görüntü toosee etiketler seçin

![Merhaba portalında depoları](./media/container-registry-repositories/container-registry-repositories.png)


## <a name="next-steps"></a>Sonraki adımlar
Merhaba temelleri bildiğinize göre kayıt defterini kullanarak hazır toostart olduğunuz! Örneğin, kapsayıcı görüntüleri tooan dağıtmaya başlamadan [Azure kapsayıcı hizmeti](https://azure.microsoft.com/documentation/services/container-service/) küme.
