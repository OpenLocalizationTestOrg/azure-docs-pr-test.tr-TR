---
title: "Azure zaman serisi Öngörüler aaaData erişim ilkelerinde | Microsoft Docs"
description: "Bu öğreticide, toomanage veri erişimi ilkelerini zaman serisi bilgiler öğrenin"
keywords: 
services: time-series-insights
documentationcenter: 
author: op-ravi
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/01/2017
ms.author: omravi
ms.openlocfilehash: f286d26c8c5c851c523e9384760dc4b10711fa3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="grant-data-access-tooa-time-series-insights-environment-using-azure-portal"></a><span data-ttu-id="43e01-103">Azure portalı kullanarak veri erişim tooa zaman serisi Öngörüler ortamı verin</span><span class="sxs-lookup"><span data-stu-id="43e01-103">Grant data access tooa Time Series Insights environment using Azure portal</span></span>

<span data-ttu-id="43e01-104">Zaman Serisi Görüşleri ortamlarının birbirinden bağımsız türde iki erişim ilkesi vardır:</span><span class="sxs-lookup"><span data-stu-id="43e01-104">Time Series Insights environments have two independent types of access policies:</span></span>

* <span data-ttu-id="43e01-105">Yönetim erişimi ilkeleri</span><span class="sxs-lookup"><span data-stu-id="43e01-105">Management access policies</span></span>
* <span data-ttu-id="43e01-106">Veri erişimi ilkeleri</span><span class="sxs-lookup"><span data-stu-id="43e01-106">Data access policies</span></span>

<span data-ttu-id="43e01-107">Her iki ilke de Azure Active Directory asıl adlarına (kullanıcılar ve uygulamalar) belirli bir ortam üzerinde çeşitli izinler verir.</span><span class="sxs-lookup"><span data-stu-id="43e01-107">Both policies grant Azure Active Directory principals (users and apps) various permissions on a particular environment.</span></span> <span data-ttu-id="43e01-108">Merhaba ilkelerini (kullanıcılar ve uygulamalar) toohello etkin ait olmalıdır hello ortamı içeren hello abonelikle ilişkili dizin (veya "Azure Kiracı").</span><span class="sxs-lookup"><span data-stu-id="43e01-108">hello principals (users and apps) must belong toohello active directory (or “Azure tenant”) associated with hello subscription containing hello environment.</span></span>

<span data-ttu-id="43e01-109">Yönetim erişim ilkeleri hello ortamının izinleri ilgili toohello yapılandırması gibi verin</span><span class="sxs-lookup"><span data-stu-id="43e01-109">Management access policies grant permissions related toohello configuration of hello environment, such as</span></span>
*   <span data-ttu-id="43e01-110">Oluşturma ve silme hello ortamının olay kaynakları başvuru veri kümelerini ve</span><span class="sxs-lookup"><span data-stu-id="43e01-110">Creation and deletion of hello environment, event sources, reference data sets, and</span></span>
*   <span data-ttu-id="43e01-111">Merhaba veri erişimi ilkelerini yönetimi.</span><span class="sxs-lookup"><span data-stu-id="43e01-111">Management of hello data access policies.</span></span>

<span data-ttu-id="43e01-112">Veri erişimi ilkelerini tooissue veri sorguları, izinleri hello ortamında başvuru verileri işlemek ve kaydedilmiş sorguları hello ortamı Perspektifler paylaşın.</span><span class="sxs-lookup"><span data-stu-id="43e01-112">Data access policies grant permissions tooissue data queries, manipulate reference data in hello environment, and share saved queries and perspectives associated with hello environment.</span></span>

<span data-ttu-id="43e01-113">iki tür ilkeleri Hello hello ortamının erişim toohello yönetimi ve erişimi toohello verileri hello ortamı içindeki arasında açıkça birbirinden izin verir.</span><span class="sxs-lookup"><span data-stu-id="43e01-113">hello two kinds of policies allow clear separation between access toohello management of hello environment and access toohello data inside hello environment.</span></span> <span data-ttu-id="43e01-114">Örneğin, Hello sahibi/creator hello ortamının hello veri erişimden kaldırılır, olası toosetup bir ortam olur.</span><span class="sxs-lookup"><span data-stu-id="43e01-114">For example, it is possible toosetup an environment such that hello owner/creator of hello environment is removed from hello data access.</span></span> <span data-ttu-id="43e01-115">Kullanıcılar ve tooread veri hello ortamından izin verilen hizmetler yanı sıra hello ortamının hiçbir erişim toohello yapılandırması verilebilir.</span><span class="sxs-lookup"><span data-stu-id="43e01-115">As well as users and services that are allowed tooread data from hello environment may be granted no access toohello configuration of hello environment.</span></span>

## <a name="grant-data-access"></a><span data-ttu-id="43e01-116">Veri erişim izni verme</span><span class="sxs-lookup"><span data-stu-id="43e01-116">Grant data access</span></span>
<span data-ttu-id="43e01-117">Merhaba aşağıdaki adımları toogrant veri için bir kullanıcı asıl nasıl erişim göster:</span><span class="sxs-lookup"><span data-stu-id="43e01-117">hello following steps show how toogrant data access for a user principal:</span></span>

1.  <span data-ttu-id="43e01-118">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="43e01-118">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2.  <span data-ttu-id="43e01-119">"Tüm kaynaklar" Merhaba menü hello sol tarafındaki hello Azure portal'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="43e01-119">Click “All resources” in hello menu on hello left side of hello Azure portal.</span></span>
3.  <span data-ttu-id="43e01-120">Zaman Serisi Görüşleri ortamınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="43e01-120">Select your Time Series Insights environment.</span></span>

  ![Merhaba zaman serisi Öngörüler kaynak - yönetmek ortamı](media/data-access/getstarted-grant-data-access1.png)

4.  <span data-ttu-id="43e01-122">“Veri Düzlemi Erişimi” öğesini seçin, “Ekle” düğmesine tıklayın</span><span class="sxs-lookup"><span data-stu-id="43e01-122">Select “Data Plane Access”, click “Add”</span></span>

  ![Merhaba zaman serisi Öngörüler kaynak yönetme - ekleme](media/data-access/getstarted-grant-data-access2.png)

5.  <span data-ttu-id="43e01-124">"Kullanıcı seç" öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="43e01-124">Click “Select user”.</span></span>
6.  <span data-ttu-id="43e01-125">Arama ve hello e-posta ile kullanıcı seçin.</span><span class="sxs-lookup"><span data-stu-id="43e01-125">Search and select user by hello email.</span></span>
7.  <span data-ttu-id="43e01-126">“Kullanıcı Seç” dikey penceresinde “Seç” düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="43e01-126">Click “Select” in “Select User” blade.</span></span>

  ![Merhaba zaman serisi Öngörüler kaynak - kullanıcı yönetme](media/data-access/getstarted-grant-data-access3.png)

8.  <span data-ttu-id="43e01-128">“Rol seç” öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="43e01-128">Click “Select role”.</span></span>
9.  <span data-ttu-id="43e01-129">Perspektif ve kaydedilmiş sorguları hello ortamının diğer kullanıcılarla paylaşmak ve tooallow kullanıcı toochange başvuru verileri isterseniz "Katılımcı" seçin.</span><span class="sxs-lookup"><span data-stu-id="43e01-129">Select “Contributor” if you want tooallow user toochange reference data and share saved queries and perspectives with other users of hello environment.</span></span> <span data-ttu-id="43e01-130">Aksi takdirde hello ortamında "Okuyucu" tooallow kullanıcı sorgu verileri seçin ve kişisel (paylaşılmayan) sorguları hello ortamında kaydedin.</span><span class="sxs-lookup"><span data-stu-id="43e01-130">Otherwise select “Reader” tooallow user query data in hello environment and save personal (not shared) queries in hello environment.</span></span>
10. <span data-ttu-id="43e01-131">"Tamam" hello "Rolü Seç" dikey penceresinde'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="43e01-131">Click “Ok” in hello “Select Role” blade.</span></span>

  ![Merhaba zaman serisi Öngörüler kaynak - select rolünü yönetme](media/data-access/getstarted-grant-data-access4.png)

11. <span data-ttu-id="43e01-133">"Tamam" hello "Kullanıcı rolü Seç" dikey penceresinde'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="43e01-133">Click “Ok” in hello “Select User Role” blade.</span></span>
12. <span data-ttu-id="43e01-134">Şunu görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="43e01-134">You should see:</span></span>

  ![Merhaba zaman serisi Öngörüler kaynak - sonuçlarını yönetme](media/data-access/getstarted-grant-data-access5.png)

## <a name="next-steps"></a><span data-ttu-id="43e01-136">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="43e01-136">Next steps</span></span>

* [<span data-ttu-id="43e01-137">Olay kaynağı oluşturma</span><span class="sxs-lookup"><span data-stu-id="43e01-137">Create an event source</span></span>](time-series-insights-add-event-source.md)
* <span data-ttu-id="43e01-138">[Olayları göndermek](time-series-insights-send-events.md) toohello olay kaynağı</span><span class="sxs-lookup"><span data-stu-id="43e01-138">[Send events](time-series-insights-send-events.md) toohello event source</span></span>
* <span data-ttu-id="43e01-139">[Zaman Serisi Görüşleri Portalı](https://insights.timeseries.azure.com)’nda ortamınızı görüntüleme</span><span class="sxs-lookup"><span data-stu-id="43e01-139">View your environment in [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
