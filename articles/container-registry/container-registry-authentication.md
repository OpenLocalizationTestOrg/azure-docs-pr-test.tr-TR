---
title: "Azure kapsayıcı kayıt defteri ile kimlik doğrulaması | Microsoft Docs"
description: "Bir Azure Active Directory hizmet asıl veya bir yönetici hesabı kullanarak bir Azure kapsayıcı kayıt defteri oturum açmak nasıl"
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
ms.openlocfilehash: aa2a6bf3d7d9ec22020036851fc0f2bca37e31bf
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="authenticate-with-a-private-docker-container-registry"></a><span data-ttu-id="69d2a-103">Bir özel Docker kapsayıcısı kayıt defteri ile kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="69d2a-103">Authenticate with a private Docker container registry</span></span>
<span data-ttu-id="69d2a-104">Azure kapsayıcı kayıt defteri kapsayıcı görüntülerinde çalışmak için kullanarak oturum `docker login` komutu.</span><span class="sxs-lookup"><span data-stu-id="69d2a-104">To work with container images in an Azure container registry, you log in using the `docker login` command.</span></span> <span data-ttu-id="69d2a-105">Ya da kullanarak oturum bir  **[Azure Active Directory hizmet asıl](../active-directory/active-directory-application-objects.md)**  veya kayıt defteri özgü **yönetici hesabı**.</span><span class="sxs-lookup"><span data-stu-id="69d2a-105">You can log in using either an **[Azure Active Directory service principal](../active-directory/active-directory-application-objects.md)** or a registry-specific **admin account**.</span></span> <span data-ttu-id="69d2a-106">Bu makalede bu kimlikleri hakkında daha fazla ayrıntı sağlar.</span><span class="sxs-lookup"><span data-stu-id="69d2a-106">This article provides more detail about these identities.</span></span>



## <a name="service-principal"></a><span data-ttu-id="69d2a-107">Hizmet sorumlusu</span><span class="sxs-lookup"><span data-stu-id="69d2a-107">Service principal</span></span>

<span data-ttu-id="69d2a-108">Şunları yapabilirsiniz [bir hizmet sorumlusu atamak](container-registry-get-started-azure-cli.md#assign-a-service-principal) , kayıt defterine ve temel Docker kimlik doğrulaması için kullanın.</span><span class="sxs-lookup"><span data-stu-id="69d2a-108">You can [assign a service principal](container-registry-get-started-azure-cli.md#assign-a-service-principal) to your registry and use it for basic Docker authentication.</span></span> <span data-ttu-id="69d2a-109">Bir hizmet sorumlusunu kullanarak çoğu senaryolar için önerilir.</span><span class="sxs-lookup"><span data-stu-id="69d2a-109">Using a service principal is recommended for most scenarios.</span></span> <span data-ttu-id="69d2a-110">Uygulama kimliği ve hizmet sorumlusu için parola sağlayın `docker login` aşağıdaki örnekte gösterildiği gibi komut:</span><span class="sxs-lookup"><span data-stu-id="69d2a-110">Provide the app ID and password of the service principal to the `docker login` command, as shown in the following example:</span></span>

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

<span data-ttu-id="69d2a-111">Bir uygulama kimliği unutmayın gerek kalmaması oturum açtıktan sonra Docker kimlik bilgileri önbelleğe alır</span><span class="sxs-lookup"><span data-stu-id="69d2a-111">Once logged in, Docker caches the credentials, so you don't need to remember the app ID.</span></span>

> [!TIP]
> <span data-ttu-id="69d2a-112">İsterseniz, çalıştırarak bir hizmet sorumlusu parolasını yeniden oluşturabilmeniz `az ad sp reset-credentials` komutu.</span><span class="sxs-lookup"><span data-stu-id="69d2a-112">If you want, you can regenerate the password of a service principal by running the `az ad sp reset-credentials` command.</span></span>
>


<span data-ttu-id="69d2a-113">Hizmet sorumluları izin [rol tabanlı erişim](../active-directory/role-based-access-control-configure.md) bir kayıt defteri.</span><span class="sxs-lookup"><span data-stu-id="69d2a-113">Service principals allow [role-based access](../active-directory/role-based-access-control-configure.md) to a registry.</span></span> <span data-ttu-id="69d2a-114">Kullanılabilir roller şunlardır:</span><span class="sxs-lookup"><span data-stu-id="69d2a-114">Available roles are:</span></span>
  * <span data-ttu-id="69d2a-115">Okuyucu (çekme yalnızca erişimi).</span><span class="sxs-lookup"><span data-stu-id="69d2a-115">Reader (pull only access).</span></span>
  * <span data-ttu-id="69d2a-116">Katkıda bulunan (çekme ve itme).</span><span class="sxs-lookup"><span data-stu-id="69d2a-116">Contributor (pull and push).</span></span>
  * <span data-ttu-id="69d2a-117">(Çekme, gönderim ve ata rolleri diğer kullanıcılara) sahip.</span><span class="sxs-lookup"><span data-stu-id="69d2a-117">Owner (pull, push, and assign roles to other users).</span></span>

<span data-ttu-id="69d2a-118">Anonim erişim Azure kapsayıcı kayıt defterleri üzerinde kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="69d2a-118">Anonymous access is not available on Azure Container Registries.</span></span> <span data-ttu-id="69d2a-119">Ortak görüntüler için kullandığınız [Docker hub'a](https://docs.docker.com/docker-hub/).</span><span class="sxs-lookup"><span data-stu-id="69d2a-119">For public images you can use [Docker Hub](https://docs.docker.com/docker-hub/).</span></span>

<span data-ttu-id="69d2a-120">Farklı kullanıcılar veya uygulamalar için erişim tanımlamanıza olanak sağlayan bir kayıt defteri, birden çok hizmet asıl adı atayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="69d2a-120">You can assign multiple service principals to a registry, which allows you to define access for different users or applications.</span></span> <span data-ttu-id="69d2a-121">Hizmet asıl adı da geliştirici veya DevOps senaryolar aşağıdaki örneklerde olduğu gibi bir kayıt defteri "gözetimsiz" bağlantısını etkinleştir:</span><span class="sxs-lookup"><span data-stu-id="69d2a-121">Service principals also enable "headless" connectivity to a registry in developer or DevOps scenarios such as the following examples:</span></span>

  * <span data-ttu-id="69d2a-122">DC/OS, Docker Swarm ve Kubernetes gibi orchestration sistemlere kapsayıcı dağıtımlarını bir kayıt defteri.</span><span class="sxs-lookup"><span data-stu-id="69d2a-122">Container deployments from a registry to orchestration systems including DC/OS, Docker Swarm and Kubernetes.</span></span> <span data-ttu-id="69d2a-123">Kapsayıcı kayıt defterleri ilgili Azure hizmetlerine gibi çekebilir [kapsayıcı hizmeti](../container-service/index.yml), [uygulama hizmeti](../app-service/index.md), [toplu](../batch/index.md), [Service Fabric](/azure/service-fabric/)ve diğerleri.</span><span class="sxs-lookup"><span data-stu-id="69d2a-123">You can also pull container registries to related Azure services such as [Container Service](../container-service/index.yml), [App Service](../app-service/index.md), [Batch](../batch/index.md), [Service Fabric](/azure/service-fabric/), and others.</span></span>

  * <span data-ttu-id="69d2a-124">Kapsayıcı görüntülerini oluşturmak ve bunları bir kayıt defterine gönderme sürekli tümleştirme ve dağıtım çözümleri (örneğin, Visual Studio Team Services veya Jenkins).</span><span class="sxs-lookup"><span data-stu-id="69d2a-124">Continuous integration and deployment solutions (such as Visual Studio Team Services or Jenkins) that build container images and push them to a registry.</span></span>





## <a name="admin-account"></a><span data-ttu-id="69d2a-125">Yönetici hesabı</span><span class="sxs-lookup"><span data-stu-id="69d2a-125">Admin account</span></span>
<span data-ttu-id="69d2a-126">Oluşturduğunuz her kayıt defteri ile bir yönetici hesabı otomatik olarak oluşturulan.</span><span class="sxs-lookup"><span data-stu-id="69d2a-126">With each registry you create, an admin account gets created automatically.</span></span> <span data-ttu-id="69d2a-127">Hesap varsayılan olarak devre dışıdır, ancak etkinleştirmek ve kimlik bilgilerini, örneğin aracılığıyla yönetmek [portal](container-registry-get-started-portal.md#manage-registry-settings) veya kullanarak [Azure CLI 2.0 komutları](container-registry-get-started-azure-cli.md#manage-admin-credentials).</span><span class="sxs-lookup"><span data-stu-id="69d2a-127">By default the account is disabled, but you can enable it and manage the credentials, for example through the [portal](container-registry-get-started-portal.md#manage-registry-settings) or using the [Azure CLI 2.0 commands](container-registry-get-started-azure-cli.md#manage-admin-credentials).</span></span> <span data-ttu-id="69d2a-128">İki parola ile her ikisi de üretilebilir sağlanan her yönetici hesabıdır.</span><span class="sxs-lookup"><span data-stu-id="69d2a-128">Each admin account is provided with two passwords, both of which can be regenerated.</span></span> <span data-ttu-id="69d2a-129">İki parola diğer parola yeniden sırada bir parola kullanarak kayıt defteri bağlantılar sağlamanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="69d2a-129">The two passwords allow you to maintain connections to the registry by using one password while you regenerate the other password.</span></span> <span data-ttu-id="69d2a-130">Hesap etkinleştirilirse, kullanıcı adı ve ya da parola geçirebilirsiniz `docker login` temel kimlik doğrulaması yapmak için kayıt defteri komutu.</span><span class="sxs-lookup"><span data-stu-id="69d2a-130">If the account is enabled, you can pass the user name and either password to the `docker login` command for basic authentication to the registry.</span></span> <span data-ttu-id="69d2a-131">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="69d2a-131">For example:</span></span>

```
docker login myregistry.azurecr.io -u myAdminName -p myPassword1
```

> [!IMPORTANT]
> <span data-ttu-id="69d2a-132">Yönetici hesabı çoğunlukla test amaçları için kayıt defterini erişmek tek bir kullanıcı için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="69d2a-132">The admin account is designed for a single user to access the registry, mainly for test purposes.</span></span> <span data-ttu-id="69d2a-133">Yönetici kimlik bilgileriniz diğer kullanıcılarla paylaşmak için önerilmez.</span><span class="sxs-lookup"><span data-stu-id="69d2a-133">It is not recommended to share the admin account credentials among other users.</span></span> <span data-ttu-id="69d2a-134">Tüm kullanıcılar kayıt defterine tek bir kullanıcı olarak görünür.</span><span class="sxs-lookup"><span data-stu-id="69d2a-134">All users appear as a single user to the registry.</span></span> <span data-ttu-id="69d2a-135">Değiştirme veya bu hesap devre dışı bırakma kayıt defteri erişim kimlik bilgilerini kullanan tüm kullanıcılar için devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="69d2a-135">Changing or disabling this account disables registry access for all users who use the credentials.</span></span>
>


### <a name="next-steps"></a><span data-ttu-id="69d2a-136">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="69d2a-136">Next steps</span></span>
* <span data-ttu-id="69d2a-137">[Docker CLI kullanarak ilk görüntünüzü anında](container-registry-get-started-docker-cli.md).</span><span class="sxs-lookup"><span data-stu-id="69d2a-137">[Push your first image using the Docker CLI](container-registry-get-started-docker-cli.md).</span></span>
* <span data-ttu-id="69d2a-138">Kapsayıcı kayıt defteri Önizleme'de kimlik doğrulaması hakkında daha fazla bilgi için bkz: [blog gönderisi](https://blogs.msdn.microsoft.com/stevelasker/2016/11/17/azure-container-registry-user-accounts/).</span><span class="sxs-lookup"><span data-stu-id="69d2a-138">For more information about authentication in the Container Registry preview, see the [blog post](https://blogs.msdn.microsoft.com/stevelasker/2016/11/17/azure-container-registry-user-accounts/).</span></span>
