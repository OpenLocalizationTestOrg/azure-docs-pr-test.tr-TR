---
title: "Intellij için hello Azure Gezgini aaaManaging Redis önbellekleri kullanarak | Microsoft Docs"
description: "Nasıl toomanage Intellij için hello Azure Explorer'ı kullanarak Azure redis önbellekleri öğrenin."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 06/14/2017
ms.author: robmcm
ms.openlocfilehash: 76ba37a2a35c26d0045e17003181108992eb957d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-redis-caches-using-hello-azure-explorer-for-intellij"></a><span data-ttu-id="6782c-103">Redis önbellekleri Intellij için hello Azure Gezgini kullanarak yönetme</span><span class="sxs-lookup"><span data-stu-id="6782c-103">Managing Redis Caches using hello Azure Explorer for IntelliJ</span></span>

<span data-ttu-id="6782c-104">Merhaba hello Intellij için Azure Araç Seti parçası olan, kullanımı kolay çözümünü Java geliştiricilere yönetme redis için kendi Azure hesabında içinde önbellekleri Intellij IDE hello sağlar Azure Gezgini.</span><span class="sxs-lookup"><span data-stu-id="6782c-104">hello Azure Explorer, which is part of hello Azure Toolkit for IntelliJ, provides Java developers with an easy-to-use solution for managing redis caches in their Azure account from inside hello IntelliJ IDE.</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-redis-cache-by-using-intellij"></a><span data-ttu-id="6782c-105">Intellij kullanarak bir Redis önbelleği oluşturma</span><span class="sxs-lookup"><span data-stu-id="6782c-105">Create a Redis Cache by using IntelliJ</span></span>

<span data-ttu-id="6782c-106">Aşağıdaki adımları hello hello Azure Gezgini kullanarak redis önbelleği hello adımları toocreate yol.</span><span class="sxs-lookup"><span data-stu-id="6782c-106">hello following steps walk you through hello steps toocreate a redis cache using hello Azure Explorer.</span></span>

1. <span data-ttu-id="6782c-107">İçinde tooyour Azure hesabı hello adımları hello kullanarak oturum [hello Intellij için Azure Araç Seti içinde oturum yönergeleri] makalesi.</span><span class="sxs-lookup"><span data-stu-id="6782c-107">Sign in tooyour Azure account using hello steps in hello [Sign In Instructions for hello Azure Toolkit for IntelliJ] article.</span></span>

1. <span data-ttu-id="6782c-108">Merhaba, **Azure Gezgini** araç penceresi, hello genişletin **Azure** düğümünü sağ tıklatın **Redis önbellekleri**ve ardından **Redis önbelleği oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="6782c-108">In hello **Azure Explorer** tool window, expand hello **Azure** node, right-click **Redis Caches**, and then click **Create Redis Cache**.</span></span>

   ![Redis önbelleği menü oluşturma][CR01]

1. <span data-ttu-id="6782c-110">Ne zaman hello **yeni Redis önbelleği** iletişim kutusu görüntülenirse, aşağıdaki seçenekleri şu hello belirtin:</span><span class="sxs-lookup"><span data-stu-id="6782c-110">When hello **New Redis Cache** dialog box appears, specify hello following options:</span></span>

   ![Yeni Redis önbelleği iletişim kutusu oluşturma][CR02]

   <span data-ttu-id="6782c-112">a.</span><span class="sxs-lookup"><span data-stu-id="6782c-112">a.</span></span> <span data-ttu-id="6782c-113">**DNS adı**: hello DNS alt çok $a hello yeni redis önbelleği için belirtir ". redis.cache.windows .net"; Örneğin: *wingtiptoys.redis.cache.windows.net*.</span><span class="sxs-lookup"><span data-stu-id="6782c-113">**DNS Name**: Specifies hello DNS subdomain for hello new redis cache, which are prepended too".redis.cache.windows.net"; for example: *wingtiptoys.redis.cache.windows.net*.</span></span>

   <span data-ttu-id="6782c-114">b.</span><span class="sxs-lookup"><span data-stu-id="6782c-114">b.</span></span> <span data-ttu-id="6782c-115">**Abonelik**: hello hello yeni redis önbelleği için toouse istediğiniz Azure aboneliği belirtir.</span><span class="sxs-lookup"><span data-stu-id="6782c-115">**Subscription**: Specifies hello Azure subscription you want toouse for hello new redis cache.</span></span>

   <span data-ttu-id="6782c-116">c.</span><span class="sxs-lookup"><span data-stu-id="6782c-116">c.</span></span> <span data-ttu-id="6782c-117">**Kaynak grubu**: hello kaynak grubu, redis önbelleği için belirtir; seçenekleri aşağıdaki Merhaba, toochoose gerekir:</span><span class="sxs-lookup"><span data-stu-id="6782c-117">**Resource Group**: Specifies hello resource group for your redis cache; you need toochoose one of hello following options:</span></span>
      * <span data-ttu-id="6782c-118">**Yeni Oluştur**: toocreate yeni bir kaynak grubu istediğinizi belirtir.</span><span class="sxs-lookup"><span data-stu-id="6782c-118">**Create New**: Specifies that you want toocreate a new resource group.</span></span>
      * <span data-ttu-id="6782c-119">**Varolan kullanmak**: Azure hesabınızla ilişkili kaynak gruplarının bir listeden seçer belirtir.</span><span class="sxs-lookup"><span data-stu-id="6782c-119">**Use Existing**: Specifies that you will choose from a list of resource groups associated with your Azure account.</span></span>

   <span data-ttu-id="6782c-120">d.</span><span class="sxs-lookup"><span data-stu-id="6782c-120">d.</span></span> <span data-ttu-id="6782c-121">**Konum**: Burada, redis önbelleği oluşturulur; hello konumu belirtir örneğin, *Batı ABD*.</span><span class="sxs-lookup"><span data-stu-id="6782c-121">**Location**: Specifies hello location where your redis cache is created; for example, *West US*.</span></span>

   <span data-ttu-id="6782c-122">e.</span><span class="sxs-lookup"><span data-stu-id="6782c-122">e.</span></span> <span data-ttu-id="6782c-123">**Fiyatlandırma katmanı**: redis önbelleği kullanan hangi fiyatlandırma katmanı belirtir; bu ayarı, istemci bağlantılarının hello sayısını belirler.</span><span class="sxs-lookup"><span data-stu-id="6782c-123">**Pricing Tier**: Specifies which pricing tier your redis cache uses; this setting determines hello number of client connections.</span></span> <span data-ttu-id="6782c-124">(Daha fazla bilgi için bkz: [Redis önbelleği fiyatlandırma].)</span><span class="sxs-lookup"><span data-stu-id="6782c-124">(For more information, see [Redis Cache Pricing].)</span></span>

   <span data-ttu-id="6782c-125">f.</span><span class="sxs-lookup"><span data-stu-id="6782c-125">f.</span></span> <span data-ttu-id="6782c-126">**SSL olmayan bağlantı noktası**: belirtir mi, redis önbelleği sağlayan SSL olmayan bağlantıları; varsayılan olarak, yalnızca SSL bağlantılarına izin verilir.</span><span class="sxs-lookup"><span data-stu-id="6782c-126">**Non-SSL port**: Specifies whether your redis cache allows non-SSL connections; by default, only SSL connections are allowed.</span></span>

1. <span data-ttu-id="6782c-127">Tüm redis önbelleği ayarları belirtildiğinde tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="6782c-127">When you have specified all your redis cache settings, click **OK**.</span></span>

<span data-ttu-id="6782c-128">Redis önbelleği oluşturulduktan sonra hello Azure Gezgini görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="6782c-128">After your redis cache has been created, it will be displayed in hello Azure Explorer.</span></span>

   ![Redis önbelleği Azure Explorer'da][CR03]

> [!NOTE]
>
> <span data-ttu-id="6782c-130">Redis önbelleği ayarları Azure yapılandırma hakkında daha fazla bilgi için bkz: [nasıl tooconfigure Azure Redis önbelleği].</span><span class="sxs-lookup"><span data-stu-id="6782c-130">For more information about configuring your Azure redis cache settings, see [How tooconfigure Azure Redis Cache].</span></span>
>

## <a name="display-hello-properties-for-your-redis-cache-in-intellij"></a><span data-ttu-id="6782c-131">Redis Önbelleği'nde Intellij için Hello özelliklerini görüntüle</span><span class="sxs-lookup"><span data-stu-id="6782c-131">Display hello properties for your Redis Cache in IntelliJ</span></span>

1. <span data-ttu-id="6782c-132">İçinde Azure Gezgini Merhaba, redis önbelleği sağ tıklatın ve **Göster özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="6782c-132">In hello Azure Explorer, right-click your redis cache and click **Show properties**.</span></span>

   ![Azure Explorer bağlam menüsü toodisplay özellikleri redis önbelleği için][SP01]

1. <span data-ttu-id="6782c-134">Hello Azure Gezgini, redis önbelleği için hello özelliklerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="6782c-134">hello Azure Explorer displays hello properties for your redis cache.</span></span>

   ![Redis önbelleği özellikleri][SP02]

## <a name="delete-your-redis-cache-by-using-intellij"></a><span data-ttu-id="6782c-136">Redis önbelleği Intellij kullanarak silme</span><span class="sxs-lookup"><span data-stu-id="6782c-136">Delete your Redis Cache by using IntelliJ</span></span>

1. <span data-ttu-id="6782c-137">İçinde Azure Gezgini Merhaba, redis önbelleği sağ tıklatın ve **silmek**.</span><span class="sxs-lookup"><span data-stu-id="6782c-137">In hello Azure Explorer, right-click your redis cache and click **Delete**.</span></span>

   ![Azure Explorer bağlam menüsü toodelete redis önbelleği][DE01]

1. <span data-ttu-id="6782c-139">Tıklatın **Evet** olduğunda, redis önbelleği toodelete istenir.</span><span class="sxs-lookup"><span data-stu-id="6782c-139">Click **Yes** when prompted toodelete your redis cache.</span></span>

   ![Redis önbelleği istemi Sil][DE02]

## <a name="next-steps"></a><span data-ttu-id="6782c-141">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6782c-141">Next steps</span></span>

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<span data-ttu-id="6782c-142">Azure redis önbellekleri, yapılandırma ayarlarını ve fiyatlandırma hakkında daha fazla bilgi için bağlantılar aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="6782c-142">For more information about Azure redis caches, configuration settings and pricing, see hello following links:</span></span>

* <span data-ttu-id="6782c-143">[Azure Redis Önbelleği]</span><span class="sxs-lookup"><span data-stu-id="6782c-143">[Azure Redis Cache]</span></span>
* <span data-ttu-id="6782c-144">[Redis önbelleği belgeleri]</span><span class="sxs-lookup"><span data-stu-id="6782c-144">[Redis Cache Documentation]</span></span>
* <span data-ttu-id="6782c-145">[Redis önbelleği fiyatlandırma]</span><span class="sxs-lookup"><span data-stu-id="6782c-145">[Redis Cache Pricing]</span></span>
* <span data-ttu-id="6782c-146">[nasıl tooconfigure Azure Redis önbelleği]</span><span class="sxs-lookup"><span data-stu-id="6782c-146">[How tooconfigure Azure Redis Cache]</span></span>

<!-- URL List -->

[Redis önbelleği fiyatlandırma]: https://azure.microsoft.com/pricing/details/cache/
[Azure Redis Önbelleği]: https://azure.microsoft.com/services/cache/
[Redis önbelleği belgeleri]: ./redis-cache/index.md
[nasıl tooconfigure Azure Redis önbelleği]: ./redis-cache/cache-configure.md
[hello Intellij için Azure Araç Seti içinde oturum yönergeleri]: ./azure-toolkit-for-intellij-sign-in-instructions.md

<!-- IMG List -->

[CR01]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/CR01.png
[CR02]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/CR02.png
[CR03]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/CR03.png

[SP01]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/SP01.png
[SP02]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/SP02.png

[DE01]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/DE01.png
[DE02]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/DE02.png
