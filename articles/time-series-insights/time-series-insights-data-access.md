---
title: "Azure Zaman Serisi Görüşleri’nde veri erişimi ilkeleri | Microsoft Docs"
description: "Bu öğreticide, Zaman Serisi Görüşleri’nde veri erişimi ilkelerini yönetmeyi öğreneceksiniz"
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
ms.openlocfilehash: e975c6d8f217bc73948c0c046204b16b1a742bc7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="grant-data-access-to-a-time-series-insights-environment-using-azure-portal"></a><span data-ttu-id="e53aa-103">Azure Portal’ı kullanarak Zaman Serisi Görüşleri ortamına veri erişimi verme</span><span class="sxs-lookup"><span data-stu-id="e53aa-103">Grant data access to a Time Series Insights environment using Azure portal</span></span>

<span data-ttu-id="e53aa-104">Zaman Serisi Görüşleri ortamlarının birbirinden bağımsız türde iki erişim ilkesi vardır:</span><span class="sxs-lookup"><span data-stu-id="e53aa-104">Time Series Insights environments have two independent types of access policies:</span></span>

* <span data-ttu-id="e53aa-105">Yönetim erişimi ilkeleri</span><span class="sxs-lookup"><span data-stu-id="e53aa-105">Management access policies</span></span>
* <span data-ttu-id="e53aa-106">Veri erişimi ilkeleri</span><span class="sxs-lookup"><span data-stu-id="e53aa-106">Data access policies</span></span>

<span data-ttu-id="e53aa-107">Her iki ilke de Azure Active Directory asıl adlarına (kullanıcılar ve uygulamalar) belirli bir ortam üzerinde çeşitli izinler verir.</span><span class="sxs-lookup"><span data-stu-id="e53aa-107">Both policies grant Azure Active Directory principals (users and apps) various permissions on a particular environment.</span></span> <span data-ttu-id="e53aa-108">Asıl adların (kullanıcılar ve uygulamalar), ortamı içeren abonelikle ilişkilendirilmiş Active Directory (veya “Azure kiracısı”) içinde yer almaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="e53aa-108">The principals (users and apps) must belong to the active directory (or “Azure tenant”) associated with the subscription containing the environment.</span></span>

<span data-ttu-id="e53aa-109">Yönetim erişimi ilkeleri, ortamı, olay kaynaklarını, başvuru veri kümelerini oluşturma ve</span><span class="sxs-lookup"><span data-stu-id="e53aa-109">Management access policies grant permissions related to the configuration of the environment, such as</span></span>
*   <span data-ttu-id="e53aa-110">Silme, veri erişimi ilkelerini yönetme gibi ortamın yapılandırmasıyla ilgili izinler</span><span class="sxs-lookup"><span data-stu-id="e53aa-110">Creation and deletion of the environment, event sources, reference data sets, and</span></span>
*   <span data-ttu-id="e53aa-111">verir.</span><span class="sxs-lookup"><span data-stu-id="e53aa-111">Management of the data access policies.</span></span>

<span data-ttu-id="e53aa-112">Veri erişimi ilkeleri, veri sorguları gönderme, ortamdaki başvuru verilerini işleme, ortamla ilişkilendirilmiş kaydedilen sorguları ve perspektifleri paylaşma izinleri verir.</span><span class="sxs-lookup"><span data-stu-id="e53aa-112">Data access policies grant permissions to issue data queries, manipulate reference data in the environment, and share saved queries and perspectives associated with the environment.</span></span>

<span data-ttu-id="e53aa-113">İki ilke türü de ortamın yönetimine erişim ile ortam içindeki verilere erişim arasında net bir ayrım yapmaya olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="e53aa-113">The two kinds of policies allow clear separation between access to the management of the environment and access to the data inside the environment.</span></span> <span data-ttu-id="e53aa-114">Örneğin, ortamın sahibinin/oluşturucusunun veri erişiminden kaldırıldığı bir ortam kurmak mümkündür.</span><span class="sxs-lookup"><span data-stu-id="e53aa-114">For example, it is possible to setup an environment such that the owner/creator of the environment is removed from the data access.</span></span> <span data-ttu-id="e53aa-115">Bunun yanı sıra, ortamdaki verileri okumasına izin verilen kullanıcılar ve hizmetlere, ortamın yapılandırması üzerinde erişim verilmeyebilir.</span><span class="sxs-lookup"><span data-stu-id="e53aa-115">As well as users and services that are allowed to read data from the environment may be granted no access to the configuration of the environment.</span></span>

## <a name="grant-data-access"></a><span data-ttu-id="e53aa-116">Veri erişim izni verme</span><span class="sxs-lookup"><span data-stu-id="e53aa-116">Grant data access</span></span>
<span data-ttu-id="e53aa-117">Aşağıdaki adımlar, bir kullanıcı asıl adına veri erişimi verme işlemini gösterir:</span><span class="sxs-lookup"><span data-stu-id="e53aa-117">The following steps show how to grant data access for a user principal:</span></span>

1.  <span data-ttu-id="e53aa-118">[Azure Portal](https://portal.azure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="e53aa-118">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2.  <span data-ttu-id="e53aa-119">Azure Portal'ın sol tarafındaki menüde "Tüm kaynaklar"a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e53aa-119">Click “All resources” in the menu on the left side of the Azure portal.</span></span>
3.  <span data-ttu-id="e53aa-120">Zaman Serisi Görüşleri ortamınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="e53aa-120">Select your Time Series Insights environment.</span></span>

  ![Zaman Serisi Görüşleri kaynağını yönetme - ortam](media/data-access/getstarted-grant-data-access1.png)

4.  <span data-ttu-id="e53aa-122">“Veri Düzlemi Erişimi” öğesini seçin, “Ekle” düğmesine tıklayın</span><span class="sxs-lookup"><span data-stu-id="e53aa-122">Select “Data Plane Access”, click “Add”</span></span>

  ![Zaman Serisi Görüşleri kaynağını yönetme - ekleme](media/data-access/getstarted-grant-data-access2.png)

5.  <span data-ttu-id="e53aa-124">"Kullanıcı seç" öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e53aa-124">Click “Select user”.</span></span>
6.  <span data-ttu-id="e53aa-125">Kullanıcıyı e-postaya göre arayın ve seçin.</span><span class="sxs-lookup"><span data-stu-id="e53aa-125">Search and select user by the email.</span></span>
7.  <span data-ttu-id="e53aa-126">“Kullanıcı Seç” dikey penceresinde “Seç” düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e53aa-126">Click “Select” in “Select User” blade.</span></span>

  ![Zaman Serisi Görüşleri kaynağını yönetme - kullanıcı seçme](media/data-access/getstarted-grant-data-access3.png)

8.  <span data-ttu-id="e53aa-128">“Rol seç” öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e53aa-128">Click “Select role”.</span></span>
9.  <span data-ttu-id="e53aa-129">Kullanıcıya başvuru verilerini değiştirme ve kaydedilmiş sorgularla perspektifleri ortamdaki diğer kullanıcılarla paylaşma izni vermek istiyorsanız, “Katılımcı” öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="e53aa-129">Select “Contributor” if you want to allow user to change reference data and share saved queries and perspectives with other users of the environment.</span></span> <span data-ttu-id="e53aa-130">Aksi takdirde, kullanıcının ortamdaki verileri sorgulamasına ve kişisel (paylaşılmayan) sorguları ortama kaydetmesine izin vermek için “Okuyucu” öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="e53aa-130">Otherwise select “Reader” to allow user query data in the environment and save personal (not shared) queries in the environment.</span></span>
10. <span data-ttu-id="e53aa-131">“Rol Seç” dikey penceresinde “Tamam” düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e53aa-131">Click “Ok” in the “Select Role” blade.</span></span>

  ![Zaman Serisi Görüşleri kaynağını yönetme - rol seçme](media/data-access/getstarted-grant-data-access4.png)

11. <span data-ttu-id="e53aa-133">“Kullanıcı Rolü Seç” dikey penceresinde “Tamam” düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e53aa-133">Click “Ok” in the “Select User Role” blade.</span></span>
12. <span data-ttu-id="e53aa-134">Şunu görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="e53aa-134">You should see:</span></span>

  ![Zaman Serisi Görüşleri kaynağını yönetme - sonuçlar](media/data-access/getstarted-grant-data-access5.png)

## <a name="next-steps"></a><span data-ttu-id="e53aa-136">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e53aa-136">Next steps</span></span>

* [<span data-ttu-id="e53aa-137">Olay kaynağı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e53aa-137">Create an event source</span></span>](time-series-insights-add-event-source.md)
* <span data-ttu-id="e53aa-138">Olay kaynağına [olayları gönderme](time-series-insights-send-events.md)</span><span class="sxs-lookup"><span data-stu-id="e53aa-138">[Send events](time-series-insights-send-events.md) to the event source</span></span>
* <span data-ttu-id="e53aa-139">[Zaman Serisi Görüşleri Portalı](https://insights.timeseries.azure.com)’nda ortamınızı görüntüleme</span><span class="sxs-lookup"><span data-stu-id="e53aa-139">View your environment in [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
