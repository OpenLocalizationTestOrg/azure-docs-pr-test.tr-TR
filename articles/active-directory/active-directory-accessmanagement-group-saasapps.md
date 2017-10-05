---
title: "SaaS uygulamalarına erişimi yönetmek için bir grup kullanma | Microsoft Docs"
description: "Azure Active Directory Premium veya Basic grupları Azure Active Directory ile tümleşik SaaS uygulamalarına erişimi atamak için nasıl kullanılacağını."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: ab8dee63-bedc-46ca-8852-234f5c16ae98
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: curtand
ms.reviewer: piotrci
ms.custom: it-pro;oldportal
ms.openlocfilehash: d350011ee9fc5ced9ddb16993f68d3c840a645a5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="using-a-group-to-manage-access-to-saas-applications"></a><span data-ttu-id="261be-103">SaaS uygulamalarına erişimi yönetmek için grup kullanma</span><span class="sxs-lookup"><span data-stu-id="261be-103">Using a group to manage access to SaaS applications</span></span>
<span data-ttu-id="261be-104">Bir Azure AD Premium veya Azure AD temel lisansı ile Azure Active Directory (Azure AD) kullanarak Azure AD ile tümleşik bir SaaS uygulaması erişim atamak için grupları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="261be-104">Using Azure Active Directory (Azure AD) with an Azure AD Premium or Azure AD Basic license, you can use groups to assign access to a SaaS application that's integrated with Azure AD.</span></span> <span data-ttu-id="261be-105">Örneğin, beş farklı SaaS uygulamaları kullanmak pazarlama departmanı için erişim atamak istiyorsanız, pazarlama departmanındaki kullanıcılar içeren bir grup oluşturabilir ve tarafından gerekli olan bu beş SaaS uygulamaları için o grubun atayın Pazarlama departmanı.</span><span class="sxs-lookup"><span data-stu-id="261be-105">For example, if you want to assign access for the marketing department to use five different SaaS applications, you can create a group that contains the users in the marketing department, and then assign that group to these five SaaS applications that are needed by the marketing department.</span></span> <span data-ttu-id="261be-106">Bu şekilde, tek bir yerde pazarlama departmanı üyeliğini yöneterek zaman tasarrufu sağlar.</span><span class="sxs-lookup"><span data-stu-id="261be-106">This way you can save time by managing the membership of the marketing department in one place.</span></span> <span data-ttu-id="261be-107">Kullanıcılar daha sonra uygulamaya pazarlama grubunun bir üyesi olarak eklenir ve pazarlama gruptan kaldırdığınızda atamalarını uygulamasından kaldırmış atanır.</span><span class="sxs-lookup"><span data-stu-id="261be-107">Users then are assigned to the application when they are added as members of the marketing group, and have their assignments removed from the application when they are removed from the marketing group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="261be-108">Microsoft, Azure AD’yi bu makalede bahsedilen Klasik Azure Portalı yerine Azure portalındaki [Azure AD yönetim merkezini](https://aad.portal.azure.com) kullanarak yönetmenizi öneriyor.</span><span class="sxs-lookup"><span data-stu-id="261be-108">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span> 

<span data-ttu-id="261be-109">Bu özellik, Azure AD uygulama galerisinde içinde ekleyebilirsiniz uygulamaları yüzlerce kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="261be-109">This capability can be used with hundreds of applications that you can add from within the Azure AD Application Gallery.</span></span>

<span data-ttu-id="261be-110">**Bir SaaS uygulaması için bir grup için erişim atamak için**</span><span class="sxs-lookup"><span data-stu-id="261be-110">**To assign access for a group to a SaaS application**</span></span>

1. <span data-ttu-id="261be-111">İçinde [Klasik Azure portalı](https://manage.windowsazure.com)seçin **Active Directory** sol taraftaki gezinti çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="261be-111">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory** on the navigation bar on the left hand side.</span></span>
2. <span data-ttu-id="261be-112">Seçin **Directory** sekmesini ve sonra bir SaaS uygulaması için bir grup için erişim atamak istediğiniz dizini açın.</span><span class="sxs-lookup"><span data-stu-id="261be-112">Select the **Directory** tab, and then open the directory in which you want to assign access for a group to a SaaS application.</span></span>
3. <span data-ttu-id="261be-113">Seçin **uygulamaları** sekmesi. Uygulama Galeriden eklenen bir uygulama seçin ve ardından **kullanıcılar ve gruplar** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="261be-113">Select the **Applications** tab. Select an application that you added from the Application Gallery, and then click  the **Users and Groups** tab.</span></span>
4. <span data-ttu-id="261be-114">Üzerinde **kullanıcılar ve gruplar** sekmesinde **başlayarak** alanına erişim atamak istediğiniz grubun adını girin ve ardından üst köşedeki onay işaretini seçin.</span><span class="sxs-lookup"><span data-stu-id="261be-114">On the **Users and Groups** tab, in the **Starting with** field, enter the name of the group to which you want to assign access, and then select the check mark in the upper right.</span></span> <span data-ttu-id="261be-115">Yalnızca ilk bölümü bir grubun adını yazmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="261be-115">You only need to type the first part of a group's name.</span></span>
5. <span data-ttu-id="261be-116">Grup seçin ve ardından **atamak erişim** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="261be-116">Select the group, then then select the **Assign Access** button.</span></span> <span data-ttu-id="261be-117">Seçin **Evet** onay iletisi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="261be-117">Select **Yes** when you see the confirmation message.</span></span> <span data-ttu-id="261be-118">Şu anda uygulamalara grup tabanlı atama yapmak için iç içe geçmiş grup üyelikleri desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="261be-118">Nested group memberships are not supported for group-based assignment to applications at this time.</span></span>
6. <span data-ttu-id="261be-119">Hangi kullanıcıların uygulamayı, doğrudan veya bir gruba üyelik tarafından atanan de görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="261be-119">You can also see which users are assigned to the application, either directly or by membership in a group.</span></span> <span data-ttu-id="261be-120">Bunu yapmak için değiştirme **'Gruplarından' açılır Göster** için **'Tüm kullanıcılar'**.</span><span class="sxs-lookup"><span data-stu-id="261be-120">To do this, change the **Show dropdown from 'Groups'** to **'All Users'**.</span></span> <span data-ttu-id="261be-121">Liste, dizinde ve isteyip istemediğinizi her bir kullanıcı uygulamaya atanan kullanıcıları gösterir.</span><span class="sxs-lookup"><span data-stu-id="261be-121">The list shows users in the directory and whether or not each user is assigned to the application.</span></span> <span data-ttu-id="261be-122">Liste ayrıca atanan kullanıcılar uygulamaya doğrudan ('doğrudan' gösterilen atama türü) ya da grup üyeliği ('Devralınan' gösterilen atama türü), atanmış olup olmadığını gösterir</span><span class="sxs-lookup"><span data-stu-id="261be-122">The list also shows whether the assigned users are assigned to the application directly (assignment type shown as 'Direct'), or by virtue of group membership (assignment type shown as 'Inherited.')</span></span>

> [!NOTE]
> <span data-ttu-id="261be-123">Yalnızca Azure AD Premium veya Azure AD temel etkinleştirdikten sonra kullanıcılar ve Gruplar sekmesinde görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="261be-123">You can see the Users and Groups tab only after you have enabled Azure AD Premium or Azure AD Basic.</span></span>
>
>

### <a name="next-steps"></a><span data-ttu-id="261be-124">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="261be-124">Next steps</span></span>
<span data-ttu-id="261be-125">Bu makalelerde Azure Active Directory ile ilgili ek bilgi sağlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="261be-125">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="261be-126">Azure Active Directory grupları ile kaynaklara erişimi yönetme</span><span class="sxs-lookup"><span data-stu-id="261be-126">Managing access to resources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="261be-127">Azure Active Directory'de Uygulama Yönetimi için Makale Dizini</span><span class="sxs-lookup"><span data-stu-id="261be-127">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="261be-128">Grup ayarlarını yapılandırmak için Azure Active Directory cmdlet'leri</span><span class="sxs-lookup"><span data-stu-id="261be-128">Azure Active Directory cmdlets for configuring group settings</span></span>](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [<span data-ttu-id="261be-129">Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="261be-129">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="261be-130">Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme</span><span class="sxs-lookup"><span data-stu-id="261be-130">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
