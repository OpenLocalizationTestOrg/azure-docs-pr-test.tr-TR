---
title: "aaaCreate özel Docker kayıt defteri - Azure portalı | Microsoft Docs"
description: "Oluşturma ve yönetme özel Docker kapsayıcısı kayıt defterleri hello Azure portal ile çalışmaya başlama"
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: dlepow
tags: 
keywords: 
ms.assetid: 53a3b3cb-ab4b-4560-bc00-366e2759f1a1
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 40f3ce44fea26e5fbeca865c9da6df55c2df9511
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-private-docker-container-registry-using-hello-azure-portal"></a><span data-ttu-id="b800e-103">Hello Azure portal kullanarak özel bir Docker kapsayıcısı kayıt oluşturun</span><span class="sxs-lookup"><span data-stu-id="b800e-103">Create a private Docker container registry using hello Azure portal</span></span>
<span data-ttu-id="b800e-104">Hello Azure portal toocreate bir kapsayıcı kayıt defteri kullanın ve ayarlarını yönetin.</span><span class="sxs-lookup"><span data-stu-id="b800e-104">Use hello Azure portal toocreate a container registry and manage its settings.</span></span> <span data-ttu-id="b800e-105">Ayrıca oluşturmak ve kapsayıcı kayıt defterleri hello kullanarak yönetmek [Azure CLI 2.0 komutları](container-registry-get-started-azure-cli.md), [Azure PowerShell](container-registry-get-started-powershell.md) veya program aracılığıyla hello kapsayıcı kayıt defteri [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376).</span><span class="sxs-lookup"><span data-stu-id="b800e-105">You can also create and manage container registries using hello [Azure CLI 2.0 commands](container-registry-get-started-azure-cli.md), [Azure PowerShell](container-registry-get-started-powershell.md) or programmatically with hello Container Registry [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376).</span></span>

<span data-ttu-id="b800e-106">Arka plan ve kavramları için bkz: [genel bakış hello](container-registry-intro.md).</span><span class="sxs-lookup"><span data-stu-id="b800e-106">For background and concepts, see [hello overview](container-registry-intro.md).</span></span>

## <a name="create-a-container-registry"></a><span data-ttu-id="b800e-107">Kapsayıcı kayıt defteri oluşturma</span><span class="sxs-lookup"><span data-stu-id="b800e-107">Create a container registry</span></span>
1. <span data-ttu-id="b800e-108">Merhaba, [Azure portal](https://portal.azure.com), tıklatın **+ yeni**.</span><span class="sxs-lookup"><span data-stu-id="b800e-108">In hello [Azure portal](https://portal.azure.com), click **+ New**.</span></span>
2. <span data-ttu-id="b800e-109">Arama hello Market **Azure kapsayıcı kayıt defteri**.</span><span class="sxs-lookup"><span data-stu-id="b800e-109">Search hello marketplace for **Azure container registry**.</span></span>
3. <span data-ttu-id="b800e-110">Yayımcısı **Microsoft** olan **Azure Kapsayıcı Kayıt Defteri** uygulamasını seçin.</span><span class="sxs-lookup"><span data-stu-id="b800e-110">Select **Azure Container Registry**, with publisher **Microsoft**.</span></span>
    <span data-ttu-id="b800e-111">![Azure Market’te Container Kayıt Defteri hizmeti](./media/container-registry-get-started-portal/container-registry-marketplace.png)</span><span class="sxs-lookup"><span data-stu-id="b800e-111">![Container Registry service in Azure Marketplace](./media/container-registry-get-started-portal/container-registry-marketplace.png)</span></span>
4. <span data-ttu-id="b800e-112">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b800e-112">Click **Create**.</span></span> <span data-ttu-id="b800e-113">Merhaba **Azure kapsayıcı kayıt defteri** dikey penceresi görünür.</span><span class="sxs-lookup"><span data-stu-id="b800e-113">hello **Azure Container Registry** blade appears.</span></span>

    ![Container kayıt defteri ayarları](./media/container-registry-get-started-portal/container-registry-settings.png)
5. <span data-ttu-id="b800e-115">Merhaba, **Azure kapsayıcı kayıt defteri** dikey penceresinde, aşağıdaki bilgilerle hello girin.</span><span class="sxs-lookup"><span data-stu-id="b800e-115">In hello **Azure Container Registry** blade, enter hello following information.</span></span> <span data-ttu-id="b800e-116">İşiniz bittiğinde **Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b800e-116">Click **Create** when you are done.</span></span>

    <span data-ttu-id="b800e-117">a.</span><span class="sxs-lookup"><span data-stu-id="b800e-117">a.</span></span> <span data-ttu-id="b800e-118">**Kayıt defteri adı**: Oluşturduğunuz kayıt defterinize özel olan, genel olarak benzersiz bir üst düzey etki alanı adı.</span><span class="sxs-lookup"><span data-stu-id="b800e-118">**Registry name**: A globally unique top-level domain name for your specific registry.</span></span> <span data-ttu-id="b800e-119">Bu örnekte hello kayıt defteri adıdır *myRegistry01*, ancak kendi benzersiz adı değiştirin.</span><span class="sxs-lookup"><span data-stu-id="b800e-119">In this example, hello registry name is *myRegistry01*, but substitute a unique name of your own.</span></span> <span data-ttu-id="b800e-120">Merhaba ad yalnızca harfler ve sayılar içerebilir.</span><span class="sxs-lookup"><span data-stu-id="b800e-120">hello name can contain only letters and numbers.</span></span>

    <span data-ttu-id="b800e-121">b.</span><span class="sxs-lookup"><span data-stu-id="b800e-121">b.</span></span> <span data-ttu-id="b800e-122">**Kaynak grubu**: Varolan seçin [kaynak grubu](../azure-resource-manager/resource-group-overview.md#resource-groups) veya yeni bir hello adını yazın.</span><span class="sxs-lookup"><span data-stu-id="b800e-122">**Resource group**: Select an existing [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) or type hello name for a new one.</span></span>

    <span data-ttu-id="b800e-123">c.</span><span class="sxs-lookup"><span data-stu-id="b800e-123">c.</span></span> <span data-ttu-id="b800e-124">**Konum**: hello hizmet olduğu bir Azure veri merkezi konum seçin [kullanılabilir](https://azure.microsoft.com/regions/services/), gibi **Orta Güney ABD**.</span><span class="sxs-lookup"><span data-stu-id="b800e-124">**Location**: Select an Azure datacenter location where hello service is [available](https://azure.microsoft.com/regions/services/), such as **South Central US**.</span></span>

    <span data-ttu-id="b800e-125">d.</span><span class="sxs-lookup"><span data-stu-id="b800e-125">d.</span></span> <span data-ttu-id="b800e-126">**Yönetici kullanıcı**: istiyorsanız, bir yönetici kullanıcı tooaccess hello kayıt defteri etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="b800e-126">**Admin user**: If you want, enable an admin user tooaccess hello registry.</span></span> <span data-ttu-id="b800e-127">Merhaba kayıt defteri oluşturduktan sonra bu ayarı değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b800e-127">You can change this setting after creating hello registry.</span></span>

      > [!IMPORTANT]
      > <span data-ttu-id="b800e-128">Ayrıca bir yönetici kullanıcı hesabıyla erişim tooproviding, kapsayıcı kayıt defterleri Azure Active Directory hizmet asıl adı tarafından desteklenen kimlik doğrulama desteği.</span><span class="sxs-lookup"><span data-stu-id="b800e-128">In addition tooproviding access through an admin user account, container registries support authentication backed by Azure Active Directory service principals.</span></span> <span data-ttu-id="b800e-129">Daha fazla bilgi ve göz önünde bulundurulması gereken diğer noktalar için bkz. [Kapsayıcı kayıt defteri ile kimlik doğrulama](container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="b800e-129">For more information and considerations, see [Authenticate with a container registry](container-registry-authentication.md).</span></span>
      >

    <span data-ttu-id="b800e-130">e.</span><span class="sxs-lookup"><span data-stu-id="b800e-130">e.</span></span> <span data-ttu-id="b800e-131">**Depolama hesabı**: hello varsayılan ayarı toocreate kullanmak bir [depolama hesabı](../storage/common/storage-introduction.md), veya mevcut bir depolama hesabını hello seçin aynı konumu.</span><span class="sxs-lookup"><span data-stu-id="b800e-131">**Storage account**: Use hello default setting toocreate a [storage account](../storage/common/storage-introduction.md), or select an existing storage account in hello same location.</span></span> <span data-ttu-id="b800e-132">Premium Depolama şu anda desteklenmemektedir.</span><span class="sxs-lookup"><span data-stu-id="b800e-132">Currently Premium Storage is not supported.</span></span>

## <a name="manage-registry-settings"></a><span data-ttu-id="b800e-133">Kayıt defteri ayarlarını yönetme</span><span class="sxs-lookup"><span data-stu-id="b800e-133">Manage registry settings</span></span>
<span data-ttu-id="b800e-134">Merhaba kayıt defteri oluşturduktan sonra hello kayıt defteri ayarları hello başlatarak **kapsayıcı kayıt defterleri** dikey penceresinde hello portal.</span><span class="sxs-lookup"><span data-stu-id="b800e-134">After creating hello registry, find hello registry settings by starting at hello **Container Registries** blade in hello portal.</span></span> <span data-ttu-id="b800e-135">Örneğin, hello ayarları toolog tooyour kayıt defterinde gerekebilir veya tooenable istediğiniz veya hello yönetici kullanıcıyı devre dışı olabilir.</span><span class="sxs-lookup"><span data-stu-id="b800e-135">For example, you might need hello settings toolog in tooyour registry, or you might want tooenable or disable hello admin user.</span></span>

1. <span data-ttu-id="b800e-136">Merhaba üzerinde **kapsayıcı kayıt defterleri** dikey penceresinde, kayıt defteri hello adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b800e-136">On hello **Container Registries** blade, click hello name of your registry.</span></span>

    ![Container kayıt defteri dikey penceresi](./media/container-registry-get-started-portal/container-registry-blade.png)
2. <span data-ttu-id="b800e-138">toomanage erişim ayarlar'ı **erişim tuşu**.</span><span class="sxs-lookup"><span data-stu-id="b800e-138">toomanage access settings, click **Access key**.</span></span>

    ![Container kayıt defteri erişimi](./media/container-registry-get-started-portal/container-registry-access.png)
3. <span data-ttu-id="b800e-140">Ayarları aşağıdaki hello dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="b800e-140">Note hello following settings:</span></span>

   * <span data-ttu-id="b800e-141">**Oturum açma sunucusu** -hello tam adı toohello kayıt defterinde toolog kullanın.</span><span class="sxs-lookup"><span data-stu-id="b800e-141">**Login server** - hello fully qualified name you use toolog in toohello registry.</span></span> <span data-ttu-id="b800e-142">Bu örnekte bu değer `myregistry01.azurecr.io`’dur.</span><span class="sxs-lookup"><span data-stu-id="b800e-142">In this example, it is `myregistry01.azurecr.io`.</span></span>
   * <span data-ttu-id="b800e-143">**Yönetici kullanıcı** - geçiş tooenable veya hello kayıt defterindeki yönetici kullanıcı hesabı devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="b800e-143">**Admin user** - Toggle tooenable or disable hello registry's admin user account.</span></span>
   * <span data-ttu-id="b800e-144">**Kullanıcı adı** ve **parola** -(etkinse) hello yönetici kullanıcı hesabının kimlik bilgilerini hello toohello kayıt defterinde toolog kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b800e-144">**Username** and **Password** - hello credentials of hello admin user account (if enabled) you can use toolog in toohello registry.</span></span> <span data-ttu-id="b800e-145">İsteğe bağlı olarak hello parolaları yeniden oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b800e-145">You can optionally regenerate hello passwords.</span></span> <span data-ttu-id="b800e-146">İki parola bağlantıları toohello kayıt defteri hello yeniden oluşturmak, bir parola kullanarak diğer parola bulundurabilirsiniz şekilde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="b800e-146">Two passwords are created so that you can maintain connections toohello registry by using one password while you regenerate hello other password.</span></span> <span data-ttu-id="b800e-147">Bunun yerine, bir hizmet asıl tooauthenticate bkz [özel Docker kapsayıcısı kayıt defteri ile kimlik doğrulama](container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="b800e-147">tooauthenticate with a service principal instead, see [Authenticate with a private Docker container registry](container-registry-authentication.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b800e-148">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b800e-148">Next steps</span></span>
* [<span data-ttu-id="b800e-149">Merhaba Docker CLI kullanarak ilk görüntünüzü bildirme</span><span class="sxs-lookup"><span data-stu-id="b800e-149">Push your first image using hello Docker CLI</span></span>](container-registry-get-started-docker-cli.md)
