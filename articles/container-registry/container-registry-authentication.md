---
title: "Azure kapsayıcı kayıt defteri ile aaaAuthenticate | Microsoft Docs"
description: "Kayıt defterinde bir Azure Active Directory'yi kullanarak tooan Azure kapsayıcı toolog nasıl hizmet asıl veya bir yönetici hesabı"
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: cristyg
tags: 
keywords: 
ms.assetid: 128a937a-766a-415b-b9fc-35a6c2f27417
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a0b0462e8432b2567689debca322e2426baa7fa2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-with-a-private-docker-container-registry"></a>Bir özel Docker kapsayıcısı kayıt defteri ile kimlik doğrulaması
toowork bir Azure kapsayıcı kayıt defterindeki kapsayıcı görüntülerle oturum hello kullanarak `docker login` komutu. Ya da kullanarak oturum bir  **[Azure Active Directory hizmet asıl](../active-directory/active-directory-application-objects.md)**  veya kayıt defteri özgü **yönetici hesabı**. Bu makalede bu kimlikleri hakkında daha fazla ayrıntı sağlar.



## <a name="service-principal"></a>Hizmet sorumlusu

Yapabilecekleriniz [bir hizmet sorumlusu atamak](container-registry-get-started-azure-cli.md#assign-a-service-principal) tooyour kayıt defteri ve temel Docker kimlik doğrulaması için kullanın. Bir hizmet sorumlusunu kullanarak çoğu senaryolar için önerilir. Merhaba uygulama kimliği ve hello hizmet asıl toohello parolasını girmeniz `docker login` hello aşağıdaki örnekte gösterildiği gibi komut:

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

Tooremember hello uygulama kimliği gerekmeyen şekilde oturum açtıktan sonra Docker hello kimlik bilgileri önbelleğe alır

> [!TIP]
> İsterseniz, hello çalıştırarak bir hizmet sorumlusu hello parolasını yeniden oluşturabilmeniz `az ad sp reset-credentials` komutu.
>


Hizmet sorumluları izin [rol tabanlı erişim](../active-directory/role-based-access-control-configure.md) tooa kayıt defteri. Kullanılabilir roller şunlardır:
  * Okuyucu (çekme yalnızca erişimi).
  * Katkıda bulunan (çekme ve itme).
  * (Çekme, gönderim ve ata rolleri tooother kullanıcılar) sahip.

Anonim erişim Azure kapsayıcı kayıt defterleri üzerinde kullanılabilir değil. Ortak görüntüler için kullandığınız [Docker hub'a](https://docs.docker.com/docker-hub/).

Farklı kullanıcılar veya uygulamalar için toodefine erişime tooa kayıt defteri birden çok hizmet asıl adı atayabilirsiniz. Hizmet asıl adı da "gözetimsiz" bağlantı tooa kayıt defterinde geliştirici veya DevOps senaryolar hello örnekler aşağıdaki gibi etkinleştirin:

  * DC/OS, Docker Swarm ve Kubernetes dahil olmak üzere bir kayıt defteri tooorchestration sistemlerden kapsayıcı dağıtımlarını. Ayrıca kapsayıcı kayıt defterleri toorelated Azure Hizmetleri gibi çekebilir [kapsayıcı hizmeti](../container-service/index.yml), [uygulama hizmeti](../app-service/index.md), [toplu](../batch/index.md), [Service Fabric](/azure/service-fabric/)ve diğerleri.

  * Kapsayıcı görüntülerini oluşturmak ve bunları gönderme sürekli tümleştirme ve dağıtım çözümleri (örneğin, Visual Studio Team Services veya Jenkins) tooa kayıt defteri.





## <a name="admin-account"></a>Yönetici hesabı
Oluşturduğunuz her kayıt defteri ile bir yönetici hesabı otomatik olarak oluşturulan. Merhaba hesap varsayılan olarak devre dışıdır, ancak etkinleştirmek ve örneğin hello üzerinden hello kimlik bilgilerini yöneten [portal](container-registry-get-started-portal.md#manage-registry-settings) veya hello kullanarak [Azure CLI 2.0 komutları](container-registry-get-started-azure-cli.md#manage-admin-credentials). İki parola ile her ikisi de üretilebilir sağlanan her yönetici hesabıdır. Merhaba iki parola hello yeniden oluşturmak diğer parola bir parola kullanarak toomaintain bağlantıları toohello kayıt defteri izin. Merhaba hesap etkinleştirilirse, hello kullanıcı adı ve ya da parola toohello geçirebilirsiniz `docker login` temel kimlik doğrulaması toohello kayıt defteri için komutu. Örneğin:

```
docker login myregistry.azurecr.io -u myAdminName -p myPassword1
```

> [!IMPORTANT]
> Merhaba yönetici hesabı tek kullanıcı tooaccess hello için kayıt defteri, çoğunlukla test amaçları için tasarlanmıştır. Diğer kullanıcılarla tooshare hello yönetici hesabı kimlik bilgileri önerilmez. Tüm kullanıcılar tek kullanıcı toohello kayıt defteri görünür. Değiştirme veya bu hesap devre dışı bırakma hello kimlik bilgilerini kullanan tüm kullanıcılar için kayıt defteri erişimini devre dışı bırakır.
>


### <a name="next-steps"></a>Sonraki adımlar
* [Merhaba Docker CLI kullanarak ilk görüntünüzü anında](container-registry-get-started-docker-cli.md).
* Merhaba hello kapsayıcı kayıt defteri Önizleme'de kimlik doğrulaması hakkında daha fazla bilgi için bkz: [blog gönderisi](https://blogs.msdn.microsoft.com/stevelasker/2016/11/17/azure-container-registry-user-accounts/).
