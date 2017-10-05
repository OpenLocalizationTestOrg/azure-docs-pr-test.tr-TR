---
title: "Azure Active Directory konumlarında adlı | Microsoft Docs"
description: "Konumları adlı yapılandırarak, kuruluşunuz tarafından sahip olunan IP adreslerini oluşturmak sahip önleyebilirsiniz Impossible için hatalı pozitif sonuç seyahat alışılmadık konumlara risk olayı türü."
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
ms.openlocfilehash: ff31ded1d9d60e47e0ae5f01119de78cd7f2df38
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="named-locations-in-azure-active-directory"></a><span data-ttu-id="3ae22-103">Azure Active Directory'de adlandırılmış konumları</span><span class="sxs-lookup"><span data-stu-id="3ae22-103">Named locations in Azure Active Directory</span></span>

<span data-ttu-id="3ae22-104">Azure Active Directory adlandırılmış konumlara özelliğiyle, kuruluşların güvenilir IP adres aralıklarını etiketleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3ae22-104">With the named locations feature of Azure Active Directory, you can label trusted IP address ranges in your organizations.</span></span> <span data-ttu-id="3ae22-105">Ortamınızda, adlandırılmış konumlarını algılanması bağlamında kullanabilirsiniz [risk olayları](active-directory-reporting-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="3ae22-105">In your environment, you can use named locations in the context of the detection of [risk events](active-directory-reporting-risk-events.md).</span></span> <span data-ttu-id="3ae22-106">Bu özellik için bildirilen hatalı pozitif uyarıların sayısını azaltır *Impossible seyahat alışılmadık konumlara* risk olayı türü.</span><span class="sxs-lookup"><span data-stu-id="3ae22-106">The feature helps reduce the number of reported false positives for the *Impossible travel to atypical locations* risk event type.</span></span> 

## <a name="configuration"></a><span data-ttu-id="3ae22-107">Yapılandırma</span><span class="sxs-lookup"><span data-stu-id="3ae22-107">Configuration</span></span>

<span data-ttu-id="3ae22-108">Adlandırılmış bir konumu yapılandırmak için:</span><span class="sxs-lookup"><span data-stu-id="3ae22-108">To configure a named location:</span></span>

1. <span data-ttu-id="3ae22-109">Oturum [Azure portal](https://portal.azure.com) genel yönetici olarak.</span><span class="sxs-lookup"><span data-stu-id="3ae22-109">Sign in to the [Azure portal](https://portal.azure.com) as global administrator.</span></span>

2. <span data-ttu-id="3ae22-110">Sol bölmede **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3ae22-110">In the left pane, click **Azure Active Directory**.</span></span>

    ![Sol bölmede Azure Active Directory bağlantısı](./media/active-directory-named-locations/01.png)

3. <span data-ttu-id="3ae22-112">Üzerinde **Azure Active Directory** dikey penceresindeki **güvenlik** 'yi tıklatın **koşullu erişim**.</span><span class="sxs-lookup"><span data-stu-id="3ae22-112">On the **Azure Active Directory** blade, in the **Security** section, click **Conditional access**.</span></span>

    ![Koşullu erişim komutu](./media/active-directory-named-locations/05.png)


4. <span data-ttu-id="3ae22-114">Üzerinde **koşullu erişim** dikey penceresindeki **Yönet** 'yi tıklatın **konumları adlı**.</span><span class="sxs-lookup"><span data-stu-id="3ae22-114">On the **Conditional Access** blade, in the **Manage** section, click **Named locations**.</span></span>

    ![Adlandırılmış konumları komutu](./media/active-directory-named-locations/06.png)


5. <span data-ttu-id="3ae22-116">Üzerinde **konumları adlı** dikey penceresinde tıklatın **yeni konum**.</span><span class="sxs-lookup"><span data-stu-id="3ae22-116">On the **Named locations** blade, click **New location**.</span></span>

    ![Yeni konum komutu](./media/active-directory-named-locations/07.png)


6. <span data-ttu-id="3ae22-118">Üzerinde **yeni** dikey penceresinde aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="3ae22-118">On the **New** blade, do the following:</span></span>

    ![Yeni bir dikey pencere](./media/active-directory-named-locations/08.png)

    <span data-ttu-id="3ae22-120">a.</span><span class="sxs-lookup"><span data-stu-id="3ae22-120">a.</span></span> <span data-ttu-id="3ae22-121">İçinde **adı** adlandırılmış konumunuz için bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="3ae22-121">In the **Name** box, type a name for your named location.</span></span>

    <span data-ttu-id="3ae22-122">b.</span><span class="sxs-lookup"><span data-stu-id="3ae22-122">b.</span></span> <span data-ttu-id="3ae22-123">İçinde **IP aralıkları** bir IP aralığı yazın.</span><span class="sxs-lookup"><span data-stu-id="3ae22-123">In the **IP ranges** box, type an IP range.</span></span> <span data-ttu-id="3ae22-124">IP aralığı içinde olması gereken *sınıfsız etki alanları arası yönlendirme* (CIDR) biçimi.</span><span class="sxs-lookup"><span data-stu-id="3ae22-124">The IP range needs to be in the *Classless Inter-Domain Routing* (CIDR) format.</span></span>  

    <span data-ttu-id="3ae22-125">c.</span><span class="sxs-lookup"><span data-stu-id="3ae22-125">c.</span></span> <span data-ttu-id="3ae22-126">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3ae22-126">Click **Create**.</span></span>



## <a name="what-you-should-know"></a><span data-ttu-id="3ae22-127">Bilmeniz gerekenler</span><span class="sxs-lookup"><span data-stu-id="3ae22-127">What you should know</span></span>

<span data-ttu-id="3ae22-128">**Toplu güncelleştirmeler**: oluşturduğunuzda veya toplu güncelleştirmeler için adlandırılmış konumlarını güncelleştirin karşıya yükleme veya IP aralıklarını içeren bir CSV dosyası indirme.</span><span class="sxs-lookup"><span data-stu-id="3ae22-128">**Bulk updates**: When you create or update named locations, for bulk updates, you can upload or download a CSV file with the IP ranges.</span></span> <span data-ttu-id="3ae22-129">Karşıya yükleme IP aralıklarını dosyasında listenin üzerine yerine listesine ekler.</span><span class="sxs-lookup"><span data-stu-id="3ae22-129">An upload adds the IP ranges in the file to the list instead of overwriting the list.</span></span>

![Karşıya yükleme ve indirme bağlantıları](./media/active-directory-named-locations/09.png)


<span data-ttu-id="3ae22-131">**Sınırlamalar**: en fazla 60 adlandırılmış konumları, her birine atanan bir IP aralığı ile tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3ae22-131">**Limitations**: You can define a maximum of 60 named locations, with one IP range assigned to each of them.</span></span> <span data-ttu-id="3ae22-132">Yapılandırılmış tek bir adlandırılmış konumunuz varsa, en fazla 500 IP aralıkları için tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3ae22-132">If you have just one named location configured, you can define up to 500 IP ranges for it.</span></span>


## <a name="next-steps"></a><span data-ttu-id="3ae22-133">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3ae22-133">Next steps</span></span>

<span data-ttu-id="3ae22-134">Risk olaylar hakkında daha fazla bilgi için bkz: [Azure Active Directory risk olaylarını](active-directory-reporting-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="3ae22-134">To learn more about risk events, see [Azure Active Directory risk events](active-directory-reporting-risk-events.md).</span></span>

