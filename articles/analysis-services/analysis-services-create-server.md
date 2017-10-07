---
title: bir Analysis Services sunucusuna Azure aaaCreate | Microsoft Docs
description: "Nasıl toocreate bir Analysis Services sunucusu örneği Azure'da öğrenin."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 7f560216-8a9a-4d06-852e-48cf24deab19
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 3668f659039f79f3dd71498d1066e8682bf33228
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-analysis-services-server-in-azure-portal"></a><span data-ttu-id="aef72-103">Azure portalında bir Azure Analysis Services sunucusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="aef72-103">Create an Azure Analysis Services server in Azure portal</span></span>
<span data-ttu-id="aef72-104">Bu makalede, Azure aboneliğinizde bir Analysis Services sunucu kaynağı oluşturmada size anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="aef72-104">This article walks you through creating an Analysis Services server resource in your Azure subscription.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="aef72-105">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="aef72-105">Before you begin</span></span>
<span data-ttu-id="aef72-106">toocomplete Bu Hızlı Başlangıç, gerekir:</span><span class="sxs-lookup"><span data-stu-id="aef72-106">toocomplete this quickstart, you need:</span></span>

* <span data-ttu-id="aef72-107">**Azure aboneliği**: ziyaret [Azure ücretsiz deneme sürümü](https://azure.microsoft.com/offers/ms-azr-0044p/) toocreate bir hesap.</span><span class="sxs-lookup"><span data-stu-id="aef72-107">**Azure subscription**: Visit [Azure Free Trial](https://azure.microsoft.com/offers/ms-azr-0044p/) toocreate an account.</span></span>
* <span data-ttu-id="aef72-108">**Azure Active Directory**: aboneliğinizi bir Azure Active Directory Kiracı ile ilişkilendirilmiş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="aef72-108">**Azure Active Directory**: Your subscription must be associated with an Azure Active Directory tenant.</span></span> <span data-ttu-id="aef72-109">Ve tooAzure içinde bu Azure Active Directory'de bir hesapla oturum toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="aef72-109">And, you need toobe signed in tooAzure with an account in that Azure Active Directory.</span></span> <span data-ttu-id="aef72-110">Microsoft hesapları desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="aef72-110">Microsoft accounts are not supported.</span></span> <span data-ttu-id="aef72-111">toolearn daha, fazla [kimlik doğrulaması ve kullanıcı izinleri](analysis-services-manage-users.md).</span><span class="sxs-lookup"><span data-stu-id="aef72-111">toolearn more, see [Authentication and user permissions](analysis-services-manage-users.md).</span></span>
* <span data-ttu-id="aef72-112">**Kaynak grubu**: zaten bir kaynak grubunu kullanın veya [yeni bir tane oluşturun](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="aef72-112">**Resource group**: Use a resource group you already have or [create a new one](../azure-resource-manager/resource-group-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="aef72-113">Sunucu oluşturulması ek hizmet ücretlerine neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="aef72-113">Creating a server might result in a new billable service.</span></span> <span data-ttu-id="aef72-114">toolearn daha, fazla [Analysis Services fiyatlandırma](https://azure.microsoft.com/pricing/details/analysis-services/).</span><span class="sxs-lookup"><span data-stu-id="aef72-114">toolearn more, see [Analysis Services pricing](https://azure.microsoft.com/pricing/details/analysis-services/).</span></span>
> 
> 

## <a name="toocreate-a-server-in-azure-portal"></a><span data-ttu-id="aef72-115">toocreate Azure portalında bir sunucu</span><span class="sxs-lookup"><span data-stu-id="aef72-115">toocreate a server in Azure portal</span></span>
1. <span data-ttu-id="aef72-116">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="aef72-116">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>  
2. <span data-ttu-id="aef72-117">Tıklatın **+ yeni** > **veri + analiz** > **Analysis Services**.</span><span class="sxs-lookup"><span data-stu-id="aef72-117">Click **+ New** > **Data + analytics** > **Analysis Services**.</span></span>
3. <span data-ttu-id="aef72-118">Merhaba, **Analysis Services** dikey penceresinde hello gerekli alanları doldurun ve sonra basın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="aef72-118">In hello **Analysis Services** blade, fill in hello required fields, and then press **Create**.</span></span>
   
    ![Sunucu oluşturma](./media/analysis-services-create-server/aas-create-server-blade.png)
   
   * <span data-ttu-id="aef72-120">**Sunucu adı**: kullanılan benzersiz bir ad tooreference hello sunucu yazın.</span><span class="sxs-lookup"><span data-stu-id="aef72-120">**Server name**: Type a unique name used tooreference hello server.</span></span>
   * <span data-ttu-id="aef72-121">**Abonelik**: Bu sunucunun bills için hello abonelik seçin.</span><span class="sxs-lookup"><span data-stu-id="aef72-121">**Subscription**: Select hello subscription this server bills to.</span></span>
   * <span data-ttu-id="aef72-122">**Kaynak grubu**: Azure kaynağı koleksiyonunu yönetmenize tasarlanmış toohelp bu kapsayıcılardır.</span><span class="sxs-lookup"><span data-stu-id="aef72-122">**Resource group**: These containers are designed toohelp you manage a collection of Azure resources.</span></span> <span data-ttu-id="aef72-123">toolearn daha, fazla [kaynak grupları](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="aef72-123">toolearn more, see [resource groups](../azure-resource-manager/resource-group-overview.md).</span></span>
   * <span data-ttu-id="aef72-124">**Konum**: Bu Azure veri merkezi konum konakları hello sunucu.</span><span class="sxs-lookup"><span data-stu-id="aef72-124">**Location**: This Azure datacenter location hosts hello server.</span></span> <span data-ttu-id="aef72-125">En büyük kullanıcı tabanınızı en yakın bir konum seçin.</span><span class="sxs-lookup"><span data-stu-id="aef72-125">Choose a location nearest your largest user base.</span></span>
   * <span data-ttu-id="aef72-126">**Fiyatlandırma katmanı**: bir fiyatlandırma katmanı seçin.</span><span class="sxs-lookup"><span data-stu-id="aef72-126">**Pricing tier**: Select a pricing tier.</span></span> <span data-ttu-id="aef72-127">Tablolu modeller too400 GB yukarı desteklenir.</span><span class="sxs-lookup"><span data-stu-id="aef72-127">Tabular models up too400 GB are supported.</span></span> <span data-ttu-id="aef72-128">toolearn daha, fazla [Azure Analysis Services fiyatlandırma](https://azure.microsoft.com/pricing/details/analysis-services/).</span><span class="sxs-lookup"><span data-stu-id="aef72-128">toolearn more, see [Azure Analysis Services pricing](https://azure.microsoft.com/pricing/details/analysis-services/).</span></span>
4. <span data-ttu-id="aef72-129">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="aef72-129">Click **Create**.</span></span>

<span data-ttu-id="aef72-130">Oluşturma genellikle bir dakika altında; alır genellikle yalnızca birkaç saniye sayısı.</span><span class="sxs-lookup"><span data-stu-id="aef72-130">Create usually takes under a minute; often just a few seconds.</span></span> <span data-ttu-id="aef72-131">Seçtiyseniz **tooPortal ekleme**, yeni sunucunuzu tooyour portal toosee gidin.</span><span class="sxs-lookup"><span data-stu-id="aef72-131">If you selected **Add tooPortal**, navigate tooyour portal toosee your new server.</span></span> <span data-ttu-id="aef72-132">Ya da çok gidin**daha fazla hizmet** > **Analysis Services** sunucunuz hazır olup olmadığını toosee.</span><span class="sxs-lookup"><span data-stu-id="aef72-132">Or, navigate too**More services** > **Analysis Services** toosee if your server is ready.</span></span>

 ![Pano](./media/analysis-services-create-server/aas-create-server-dashboard.png)


## <a name="next-steps"></a><span data-ttu-id="aef72-134">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="aef72-134">Next steps</span></span>
<span data-ttu-id="aef72-135">Sunucunuz oluşturduktan sonra [bir model dağıtma](analysis-services-deploy.md) tooit SSDT kullanarak veya SSMS ile.</span><span class="sxs-lookup"><span data-stu-id="aef72-135">Once you've created your server, you can [deploy a model](analysis-services-deploy.md) tooit by using SSDT or with SSMS.</span></span>

<span data-ttu-id="aef72-136">Tooyour sunucu dağıttığınız bir model tooon içi veri kaynaklarına bağlanıyorsa, tooinstall gereken bir [şirket içi veri ağ geçidi](analysis-services-gateway.md) ağınızdaki bir bilgisayara.</span><span class="sxs-lookup"><span data-stu-id="aef72-136">If a model you deploy tooyour server connects tooon-premises data sources, you need tooinstall an [On-premises data gateway](analysis-services-gateway.md) on a computer in your network.</span></span>

