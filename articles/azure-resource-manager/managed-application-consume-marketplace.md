---
title: "Azure yönetilen uygulama pazarında aaaConsume | Microsoft Docs"
description: "Describeshow toocreate bir Azure yönetilen hello Market kullanılabilen uygulama."
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/11/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: 9ae6e11a3f63eb58a9f3199364b5606a7afe5618
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="consume-azure-managed-applications-in-hello-marketplace"></a><span data-ttu-id="bff91-103">Azure tüketen yönetilen hello Market uygulamalarda</span><span class="sxs-lookup"><span data-stu-id="bff91-103">Consume Azure managed applications in hello Marketplace</span></span>

<span data-ttu-id="bff91-104">Hello anlatıldığı gibi [yönetilen uygulama genel bakış](managed-application-overview.md) makalesi, hello son tooend deneyimi iki senaryo vardır.</span><span class="sxs-lookup"><span data-stu-id="bff91-104">As discussed in hello [Managed Application overview](managed-application-overview.md) article, there are two scenarios in hello end tooend experience.</span></span> <span data-ttu-id="bff91-105">Merhaba yayımcı veya toocreate müşteriler tarafından kullanılmak üzere bir yönetilen uygulamayı isteyen satıcı biridir.</span><span class="sxs-lookup"><span data-stu-id="bff91-105">One is hello publisher or vendor who wants toocreate a managed application for use by customers.</span></span> <span data-ttu-id="bff91-106">Merhaba ikinci hello son müşteri veya yönetilen hello uygulamasının hello tüketici içindir.</span><span class="sxs-lookup"><span data-stu-id="bff91-106">hello second is hello end customer or hello consumer of hello managed application.</span></span> <span data-ttu-id="bff91-107">Bu makalede, hello ikinci senaryo yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="bff91-107">This article covers hello second scenario.</span></span> <span data-ttu-id="bff91-108">Bu, Microsoft Azure Market hello yönetilen bir uygulamadan nasıl dağıtabileceğini açıklar.</span><span class="sxs-lookup"><span data-stu-id="bff91-108">It describes how you can deploy a managed application from hello Microsoft Azure Marketplace.</span></span>

## <a name="create-from-hello-marketplace"></a><span data-ttu-id="bff91-109">Market Hello oluşturma</span><span class="sxs-lookup"><span data-stu-id="bff91-109">Create from hello Marketplace</span></span>

<span data-ttu-id="bff91-110">Merhaba Market yönetilen bir uygulamadan dağıtımı hello Market kaynaklardan herhangi bir tür benzer toodeploying..</span><span class="sxs-lookup"><span data-stu-id="bff91-110">Deploying a managed application from hello Marketplace is similar toodeploying any type of resources from hello Marketplace.</span></span> 

<span data-ttu-id="bff91-111">Merhaba Portalı'nda seçin **+ yeni** ve çözüm toodeploy hello türünü arayın.</span><span class="sxs-lookup"><span data-stu-id="bff91-111">In hello portal, select **+ New** and search for hello type of solution toodeploy.</span></span> <span data-ttu-id="bff91-112">Merhaba kullanılabilir seçeneklerden hello gereksinim seçin.</span><span class="sxs-lookup"><span data-stu-id="bff91-112">From hello available options, select hello one you need.</span></span>

![arama çözümü](./media/managed-application-consume-marketplace/search-apps.png)

<span data-ttu-id="bff91-114">Merhaba uygulaması hello özetini gözden geçirin ve seçin **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="bff91-114">Review hello summary of hello application, and select **Create**.</span></span>

![yönetilen uygulama oluşturma](./media/managed-application-consume-marketplace/create-marketplace-managed-app.png)

<span data-ttu-id="bff91-116">Başka herhangi bir çözümü gibi alanları tooprovide değerleri ile sunulur.</span><span class="sxs-lookup"><span data-stu-id="bff91-116">Like any other solution, you are presented with fields tooprovide values for.</span></span> <span data-ttu-id="bff91-117">Bu alanların yönetilen uygulamayı oluşturduğunuz hello türüne göre değişir.</span><span class="sxs-lookup"><span data-stu-id="bff91-117">These fields vary by hello type of managed application you create.</span></span> 

## <a name="view-support-information"></a><span data-ttu-id="bff91-118">Destek bilgilerini görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="bff91-118">View support information</span></span>

<span data-ttu-id="bff91-119">Yönetilen Uygulamanız dağıtıldıktan sonra hello uygulaması hello destek bilgilerini görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="bff91-119">After your managed application has deployed, view hello support information for hello application.</span></span> <span data-ttu-id="bff91-120">Merhaba yönetilen uygulamayı dikey penceresinde hello destek bilgileri listelenir.</span><span class="sxs-lookup"><span data-stu-id="bff91-120">In hello managed application blade, hello support information is listed.</span></span>

![Destek](./media/managed-application-consume-marketplace/support.png)

## <a name="view-publisher-permissions"></a><span data-ttu-id="bff91-122">Yayımcı izinleri görüntüleme</span><span class="sxs-lookup"><span data-stu-id="bff91-122">View publisher permissions</span></span>

<span data-ttu-id="bff91-123">Uygulamanızı yönetir hello satıcı tooyour kaynaklarına erişim verilir.</span><span class="sxs-lookup"><span data-stu-id="bff91-123">hello vendor that manages your application is granted access tooyour resources.</span></span> <span data-ttu-id="bff91-124">Bu izinleri toosee seçin **yetkilerini**.</span><span class="sxs-lookup"><span data-stu-id="bff91-124">toosee those permissions, select **Authorizations**.</span></span>

![Yetkileri değiştirme](./media/managed-application-consume-marketplace/authorizations.png)

## <a name="next-steps"></a><span data-ttu-id="bff91-126">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bff91-126">Next steps</span></span>

* <span data-ttu-id="bff91-127">Yönetilen bir uygulama yayımlama hello Market hakkında daha fazla bilgi için bkz: [Azure yönetilen uygulamalarda Market](managed-application-author-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="bff91-127">For information about publishing a managed application in hello Marketplace, see [Azure Managed Applications in Marketplace](managed-application-author-marketplace.md).</span></span>
* <span data-ttu-id="bff91-128">toopublish yönetilen yalnızca kullanılabilir toousers, kuruluşunuzdaki uygulamaları bkz [oluşturma ve hizmet Kataloğu yönetilen uygulamayı yayımlayın](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="bff91-128">toopublish managed applications that are only available toousers in your organization, see [Create and publish Service Catalog Managed Application](managed-application-publishing.md).</span></span>
* <span data-ttu-id="bff91-129">tooconsume yönetilen yalnızca kullanılabilir toousers, kuruluşunuzdaki uygulamaları bkz [yönetilen bir hizmet Kataloğu uygulaması tüketen](managed-application-consumption.md).</span><span class="sxs-lookup"><span data-stu-id="bff91-129">tooconsume managed applications that are only available toousers in your organization, see [Consume a Service Catalog Managed Application](managed-application-consumption.md).</span></span>
