---
title: "Azure Active Directory'de aaaNamed konumları | Microsoft Docs"
description: "Konumları adlı yapılandırarak IP sahip önleyebilirsiniz kuruluşunuz tarafından sahip olunan adresleri hello mümkün olmayan seyahat tooatypical konumları risk olay türü için hatalı pozitif sonuç oluşturur."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: f56e042a-78d5-4ea3-be33-94004f2a0fc3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 591e4b94b2ec9d45e20c01711e922f9972e047e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="named-locations-in-azure-active-directory"></a><span data-ttu-id="7e193-103">Azure Active Directory'de adlandırılmış konumları</span><span class="sxs-lookup"><span data-stu-id="7e193-103">Named locations in Azure Active Directory</span></span>

<span data-ttu-id="7e193-104">Azure Active Directory konumları özelliği adlı hello ile kuruluşların güvenilir IP adres aralıklarını etiketleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7e193-104">With hello named locations feature of Azure Active Directory, you can label trusted IP address ranges in your organizations.</span></span> <span data-ttu-id="7e193-105">Ortamınızda, adlandırılmış konumlarını hello algılanması hello bağlamda kullanabilirsiniz [risk olayları](active-directory-reporting-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="7e193-105">In your environment, you can use named locations in hello context of hello detection of [risk events](active-directory-reporting-risk-events.md).</span></span> <span data-ttu-id="7e193-106">Merhaba özelliği, hello hello için bildirilen hatalı pozitif uyarıların sayısını azaltmaya yardımcı olur *mümkün olmayan seyahat tooatypical konumları* risk olayı türü.</span><span class="sxs-lookup"><span data-stu-id="7e193-106">hello feature helps reduce hello number of reported false positives for hello *Impossible travel tooatypical locations* risk event type.</span></span> 

## <a name="configuration"></a><span data-ttu-id="7e193-107">Yapılandırma</span><span class="sxs-lookup"><span data-stu-id="7e193-107">Configuration</span></span>

<span data-ttu-id="7e193-108">tooconfigure adlandırılmış bir konumu:</span><span class="sxs-lookup"><span data-stu-id="7e193-108">tooconfigure a named location:</span></span>

1. <span data-ttu-id="7e193-109">İçinde toohello oturum [Azure portal](https://portal.azure.com) genel yönetici olarak.</span><span class="sxs-lookup"><span data-stu-id="7e193-109">Sign in toohello [Azure portal](https://portal.azure.com) as global administrator.</span></span>

2. <span data-ttu-id="7e193-110">Merhaba sol bölmede **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7e193-110">In hello left pane, click **Azure Active Directory**.</span></span>

    ![Merhaba sol bölmede Hello Azure Active Directory bağlantısı](./media/active-directory-named-locations/01.png)

3. <span data-ttu-id="7e193-112">Merhaba üzerinde **Azure Active Directory** dikey penceresinde hello **güvenlik** 'yi tıklatın **koşullu erişim**.</span><span class="sxs-lookup"><span data-stu-id="7e193-112">On hello **Azure Active Directory** blade, in hello **Security** section, click **Conditional access**.</span></span>

    ![Merhaba koşullu erişim komutu](./media/active-directory-named-locations/05.png)


4. <span data-ttu-id="7e193-114">Merhaba üzerinde **koşullu erişim** dikey penceresinde hello **Yönet** 'yi tıklatın **konumları adlı**.</span><span class="sxs-lookup"><span data-stu-id="7e193-114">On hello **Conditional Access** blade, in hello **Manage** section, click **Named locations**.</span></span>

    ![Merhaba adlandırılmış konumları komutu](./media/active-directory-named-locations/06.png)


5. <span data-ttu-id="7e193-116">Merhaba üzerinde **konumları adlı** dikey penceresinde tıklatın **yeni konum**.</span><span class="sxs-lookup"><span data-stu-id="7e193-116">On hello **Named locations** blade, click **New location**.</span></span>

    ![Merhaba yeni konum komutu](./media/active-directory-named-locations/07.png)


6. <span data-ttu-id="7e193-118">Merhaba üzerinde **yeni** dikey penceresinde, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="7e193-118">On hello **New** blade, do hello following:</span></span>

    ![Merhaba yeni dikey penceresi](./media/active-directory-named-locations/08.png)

    <span data-ttu-id="7e193-120">a.</span><span class="sxs-lookup"><span data-stu-id="7e193-120">a.</span></span> <span data-ttu-id="7e193-121">Merhaba, **adı** adlandırılmış konumunuz için bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="7e193-121">In hello **Name** box, type a name for your named location.</span></span>

    <span data-ttu-id="7e193-122">b.</span><span class="sxs-lookup"><span data-stu-id="7e193-122">b.</span></span> <span data-ttu-id="7e193-123">Merhaba, **IP aralıkları** bir IP aralığı yazın.</span><span class="sxs-lookup"><span data-stu-id="7e193-123">In hello **IP ranges** box, type an IP range.</span></span> <span data-ttu-id="7e193-124">Merhaba IP aralığı gereken hello toobe *sınıfsız etki alanları arası yönlendirme* (CIDR) biçimi.</span><span class="sxs-lookup"><span data-stu-id="7e193-124">hello IP range needs toobe in hello *Classless Inter-Domain Routing* (CIDR) format.</span></span>  

    <span data-ttu-id="7e193-125">c.</span><span class="sxs-lookup"><span data-stu-id="7e193-125">c.</span></span> <span data-ttu-id="7e193-126">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7e193-126">Click **Create**.</span></span>



## <a name="what-you-should-know"></a><span data-ttu-id="7e193-127">Bilmeniz gerekenler</span><span class="sxs-lookup"><span data-stu-id="7e193-127">What you should know</span></span>

<span data-ttu-id="7e193-128">**Toplu güncelleştirmeler**: oluşturduğunuzda veya toplu güncelleştirmeler için adlandırılmış konumlarını güncelleştirin karşıya yükleme veya hello IP aralıklarını içeren bir CSV dosyası indirme.</span><span class="sxs-lookup"><span data-stu-id="7e193-128">**Bulk updates**: When you create or update named locations, for bulk updates, you can upload or download a CSV file with hello IP ranges.</span></span> <span data-ttu-id="7e193-129">Karşıya yükleme hello IP aralıkları hello listesi üzerine yerine hello dosya toohello listesinde ekler.</span><span class="sxs-lookup"><span data-stu-id="7e193-129">An upload adds hello IP ranges in hello file toohello list instead of overwriting hello list.</span></span>

![Merhaba karşıya ve karşıdan yükleme bağlantıları](./media/active-directory-named-locations/09.png)


<span data-ttu-id="7e193-131">**Sınırlamalar**: en fazla 60 adlandırılmış konumları, bunların bir IP aralığı atanan tooeach ile tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7e193-131">**Limitations**: You can define a maximum of 60 named locations, with one IP range assigned tooeach of them.</span></span> <span data-ttu-id="7e193-132">Yapılandırılmış tek bir adlandırılmış konumunuz varsa too500 IP aralıkları için tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7e193-132">If you have just one named location configured, you can define up too500 IP ranges for it.</span></span>


## <a name="next-steps"></a><span data-ttu-id="7e193-133">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7e193-133">Next steps</span></span>

<span data-ttu-id="7e193-134">toolearn risk olaylar hakkında daha fazla bilgi görmek [Azure Active Directory risk olaylarını](active-directory-reporting-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="7e193-134">toolearn more about risk events, see [Azure Active Directory risk events](active-directory-reporting-risk-events.md).</span></span>

