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
# <a name="authenticate-with-a-private-docker-container-registry"></a><span data-ttu-id="680b9-103">Bir özel Docker kapsayıcısı kayıt defteri ile kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="680b9-103">Authenticate with a private Docker container registry</span></span>
<span data-ttu-id="680b9-104">toowork bir Azure kapsayıcı kayıt defterindeki kapsayıcı görüntülerle oturum hello kullanarak `docker login` komutu.</span><span class="sxs-lookup"><span data-stu-id="680b9-104">toowork with container images in an Azure container registry, you log in using hello `docker login` command.</span></span> <span data-ttu-id="680b9-105">Ya da kullanarak oturum bir  **[Azure Active Directory hizmet asıl](../active-directory/active-directory-application-objects.md)**  veya kayıt defteri özgü **yönetici hesabı**.</span><span class="sxs-lookup"><span data-stu-id="680b9-105">You can log in using either an **[Azure Active Directory service principal](../active-directory/active-directory-application-objects.md)** or a registry-specific **admin account**.</span></span> <span data-ttu-id="680b9-106">Bu makalede bu kimlikleri hakkında daha fazla ayrıntı sağlar.</span><span class="sxs-lookup"><span data-stu-id="680b9-106">This article provides more detail about these identities.</span></span>



## <a name="service-principal"></a><span data-ttu-id="680b9-107">Hizmet sorumlusu</span><span class="sxs-lookup"><span data-stu-id="680b9-107">Service principal</span></span>

<span data-ttu-id="680b9-108">Yapabilecekleriniz [bir hizmet sorumlusu atamak](container-registry-get-started-azure-cli.md#assign-a-service-principal) tooyour kayıt defteri ve temel Docker kimlik doğrulaması için kullanın.</span><span class="sxs-lookup"><span data-stu-id="680b9-108">You can [assign a service principal](container-registry-get-started-azure-cli.md#assign-a-service-principal) tooyour registry and use it for basic Docker authentication.</span></span> <span data-ttu-id="680b9-109">Bir hizmet sorumlusunu kullanarak çoğu senaryolar için önerilir.</span><span class="sxs-lookup"><span data-stu-id="680b9-109">Using a service principal is recommended for most scenarios.</span></span> <span data-ttu-id="680b9-110">Merhaba uygulama kimliği ve hello hizmet asıl toohello parolasını girmeniz `docker login` hello aşağıdaki örnekte gösterildiği gibi komut:</span><span class="sxs-lookup"><span data-stu-id="680b9-110">Provide hello app ID and password of hello service principal toohello `docker login` command, as shown in hello following example:</span></span>

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

<span data-ttu-id="680b9-111">Tooremember hello uygulama kimliği gerekmeyen şekilde oturum açtıktan sonra Docker hello kimlik bilgileri önbelleğe alır</span><span class="sxs-lookup"><span data-stu-id="680b9-111">Once logged in, Docker caches hello credentials, so you don't need tooremember hello app ID.</span></span>

> [!TIP]
> <span data-ttu-id="680b9-112">İsterseniz, hello çalıştırarak bir hizmet sorumlusu hello parolasını yeniden oluşturabilmeniz `az ad sp reset-credentials` komutu.</span><span class="sxs-lookup"><span data-stu-id="680b9-112">If you want, you can regenerate hello password of a service principal by running hello `az ad sp reset-credentials` command.</span></span>
>


<span data-ttu-id="680b9-113">Hizmet sorumluları izin [rol tabanlı erişim](../active-directory/role-based-access-control-configure.md) tooa kayıt defteri.</span><span class="sxs-lookup"><span data-stu-id="680b9-113">Service principals allow [role-based access](../active-directory/role-based-access-control-configure.md) tooa registry.</span></span> <span data-ttu-id="680b9-114">Kullanılabilir roller şunlardır:</span><span class="sxs-lookup"><span data-stu-id="680b9-114">Available roles are:</span></span>
  * <span data-ttu-id="680b9-115">Okuyucu (çekme yalnızca erişimi).</span><span class="sxs-lookup"><span data-stu-id="680b9-115">Reader (pull only access).</span></span>
  * <span data-ttu-id="680b9-116">Katkıda bulunan (çekme ve itme).</span><span class="sxs-lookup"><span data-stu-id="680b9-116">Contributor (pull and push).</span></span>
  * <span data-ttu-id="680b9-117">(Çekme, gönderim ve ata rolleri tooother kullanıcılar) sahip.</span><span class="sxs-lookup"><span data-stu-id="680b9-117">Owner (pull, push, and assign roles tooother users).</span></span>

<span data-ttu-id="680b9-118">Anonim erişim Azure kapsayıcı kayıt defterleri üzerinde kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="680b9-118">Anonymous access is not available on Azure Container Registries.</span></span> <span data-ttu-id="680b9-119">Ortak görüntüler için kullandığınız [Docker hub'a](https://docs.docker.com/docker-hub/).</span><span class="sxs-lookup"><span data-stu-id="680b9-119">For public images you can use [Docker Hub](https://docs.docker.com/docker-hub/).</span></span>

<span data-ttu-id="680b9-120">Farklı kullanıcılar veya uygulamalar için toodefine erişime tooa kayıt defteri birden çok hizmet asıl adı atayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="680b9-120">You can assign multiple service principals tooa registry, which allows you toodefine access for different users or applications.</span></span> <span data-ttu-id="680b9-121">Hizmet asıl adı da "gözetimsiz" bağlantı tooa kayıt defterinde geliştirici veya DevOps senaryolar hello örnekler aşağıdaki gibi etkinleştirin:</span><span class="sxs-lookup"><span data-stu-id="680b9-121">Service principals also enable "headless" connectivity tooa registry in developer or DevOps scenarios such as hello following examples:</span></span>

  * <span data-ttu-id="680b9-122">DC/OS, Docker Swarm ve Kubernetes dahil olmak üzere bir kayıt defteri tooorchestration sistemlerden kapsayıcı dağıtımlarını.</span><span class="sxs-lookup"><span data-stu-id="680b9-122">Container deployments from a registry tooorchestration systems including DC/OS, Docker Swarm and Kubernetes.</span></span> <span data-ttu-id="680b9-123">Ayrıca kapsayıcı kayıt defterleri toorelated Azure Hizmetleri gibi çekebilir [kapsayıcı hizmeti](../container-service/index.yml), [uygulama hizmeti](../app-service/index.md), [toplu](../batch/index.md), [Service Fabric](/azure/service-fabric/)ve diğerleri.</span><span class="sxs-lookup"><span data-stu-id="680b9-123">You can also pull container registries toorelated Azure services such as [Container Service](../container-service/index.yml), [App Service](../app-service/index.md), [Batch](../batch/index.md), [Service Fabric](/azure/service-fabric/), and others.</span></span>

  * <span data-ttu-id="680b9-124">Kapsayıcı görüntülerini oluşturmak ve bunları gönderme sürekli tümleştirme ve dağıtım çözümleri (örneğin, Visual Studio Team Services veya Jenkins) tooa kayıt defteri.</span><span class="sxs-lookup"><span data-stu-id="680b9-124">Continuous integration and deployment solutions (such as Visual Studio Team Services or Jenkins) that build container images and push them tooa registry.</span></span>





## <a name="admin-account"></a><span data-ttu-id="680b9-125">Yönetici hesabı</span><span class="sxs-lookup"><span data-stu-id="680b9-125">Admin account</span></span>
<span data-ttu-id="680b9-126">Oluşturduğunuz her kayıt defteri ile bir yönetici hesabı otomatik olarak oluşturulan.</span><span class="sxs-lookup"><span data-stu-id="680b9-126">With each registry you create, an admin account gets created automatically.</span></span> <span data-ttu-id="680b9-127">Merhaba hesap varsayılan olarak devre dışıdır, ancak etkinleştirmek ve örneğin hello üzerinden hello kimlik bilgilerini yöneten [portal](container-registry-get-started-portal.md#manage-registry-settings) veya hello kullanarak [Azure CLI 2.0 komutları](container-registry-get-started-azure-cli.md#manage-admin-credentials).</span><span class="sxs-lookup"><span data-stu-id="680b9-127">By default hello account is disabled, but you can enable it and manage hello credentials, for example through hello [portal](container-registry-get-started-portal.md#manage-registry-settings) or using hello [Azure CLI 2.0 commands](container-registry-get-started-azure-cli.md#manage-admin-credentials).</span></span> <span data-ttu-id="680b9-128">İki parola ile her ikisi de üretilebilir sağlanan her yönetici hesabıdır.</span><span class="sxs-lookup"><span data-stu-id="680b9-128">Each admin account is provided with two passwords, both of which can be regenerated.</span></span> <span data-ttu-id="680b9-129">Merhaba iki parola hello yeniden oluşturmak diğer parola bir parola kullanarak toomaintain bağlantıları toohello kayıt defteri izin.</span><span class="sxs-lookup"><span data-stu-id="680b9-129">hello two passwords allow you toomaintain connections toohello registry by using one password while you regenerate hello other password.</span></span> <span data-ttu-id="680b9-130">Merhaba hesap etkinleştirilirse, hello kullanıcı adı ve ya da parola toohello geçirebilirsiniz `docker login` temel kimlik doğrulaması toohello kayıt defteri için komutu.</span><span class="sxs-lookup"><span data-stu-id="680b9-130">If hello account is enabled, you can pass hello user name and either password toohello `docker login` command for basic authentication toohello registry.</span></span> <span data-ttu-id="680b9-131">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="680b9-131">For example:</span></span>

```
docker login myregistry.azurecr.io -u myAdminName -p myPassword1
```

> [!IMPORTANT]
> <span data-ttu-id="680b9-132">Merhaba yönetici hesabı tek kullanıcı tooaccess hello için kayıt defteri, çoğunlukla test amaçları için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="680b9-132">hello admin account is designed for a single user tooaccess hello registry, mainly for test purposes.</span></span> <span data-ttu-id="680b9-133">Diğer kullanıcılarla tooshare hello yönetici hesabı kimlik bilgileri önerilmez.</span><span class="sxs-lookup"><span data-stu-id="680b9-133">It is not recommended tooshare hello admin account credentials among other users.</span></span> <span data-ttu-id="680b9-134">Tüm kullanıcılar tek kullanıcı toohello kayıt defteri görünür.</span><span class="sxs-lookup"><span data-stu-id="680b9-134">All users appear as a single user toohello registry.</span></span> <span data-ttu-id="680b9-135">Değiştirme veya bu hesap devre dışı bırakma hello kimlik bilgilerini kullanan tüm kullanıcılar için kayıt defteri erişimini devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="680b9-135">Changing or disabling this account disables registry access for all users who use hello credentials.</span></span>
>


### <a name="next-steps"></a><span data-ttu-id="680b9-136">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="680b9-136">Next steps</span></span>
* <span data-ttu-id="680b9-137">[Merhaba Docker CLI kullanarak ilk görüntünüzü anında](container-registry-get-started-docker-cli.md).</span><span class="sxs-lookup"><span data-stu-id="680b9-137">[Push your first image using hello Docker CLI](container-registry-get-started-docker-cli.md).</span></span>
* <span data-ttu-id="680b9-138">Merhaba hello kapsayıcı kayıt defteri Önizleme'de kimlik doğrulaması hakkında daha fazla bilgi için bkz: [blog gönderisi](https://blogs.msdn.microsoft.com/stevelasker/2016/11/17/azure-container-registry-user-accounts/).</span><span class="sxs-lookup"><span data-stu-id="680b9-138">For more information about authentication in hello Container Registry preview, see hello [blog post](https://blogs.msdn.microsoft.com/stevelasker/2016/11/17/azure-container-registry-user-accounts/).</span></span>
