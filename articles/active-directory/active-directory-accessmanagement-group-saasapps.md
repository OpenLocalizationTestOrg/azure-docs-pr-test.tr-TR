---
title: "bir grup toomanage erişim tooSaaS uygulamaları aaaUsing | Microsoft Docs"
description: "Nasıl toouse grupları Azure Active Directory Premium veya Basic tooassign Azure Active Directory ile tümleşik tooSaaS uygulamaları erişin."
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
ms.openlocfilehash: f45ea4472b3d88e8ea514af3db31b4cc9ea68d58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-a-group-toomanage-access-toosaas-applications"></a><span data-ttu-id="91bcc-103">Bir grup toomanage erişim tooSaaS uygulamaları kullanma</span><span class="sxs-lookup"><span data-stu-id="91bcc-103">Using a group toomanage access tooSaaS applications</span></span>
<span data-ttu-id="91bcc-104">Bir Azure AD Premium veya Azure AD temel lisansı ile Azure Active Directory (Azure AD) kullanarak Azure AD ile tümleşik grupları tooassign access tooa SaaS uygulaması kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="91bcc-104">Using Azure Active Directory (Azure AD) with an Azure AD Premium or Azure AD Basic license, you can use groups tooassign access tooa SaaS application that's integrated with Azure AD.</span></span> <span data-ttu-id="91bcc-105">Örneğin, tooassign erişim hello pazarlama departmanı toouse beş farklı SaaS uygulamaları için isterseniz, hello pazarlama departmanındaki hello kullanıcıları içeren bir grup oluşturabilir ve bu Grup toothese beş SaaS uygulamaları atayın Merhaba pazarlama departmanı tarafından gerekli.</span><span class="sxs-lookup"><span data-stu-id="91bcc-105">For example, if you want tooassign access for hello marketing department toouse five different SaaS applications, you can create a group that contains hello users in hello marketing department, and then assign that group toothese five SaaS applications that are needed by hello marketing department.</span></span> <span data-ttu-id="91bcc-106">Bu şekilde pazarlama departmanı tek bir yerde hello hello üyeliğini yöneterek zaman tasarrufu sağlar.</span><span class="sxs-lookup"><span data-stu-id="91bcc-106">This way you can save time by managing hello membership of hello marketing department in one place.</span></span> <span data-ttu-id="91bcc-107">Kullanıcılar, ardından hello pazarlama grubunun bir üyesi olarak eklenir ve pazarlama grubunun hello kaldırıldığında atamalarını hello uygulamasından kaldırmış toohello uygulama atanır.</span><span class="sxs-lookup"><span data-stu-id="91bcc-107">Users then are assigned toohello application when they are added as members of hello marketing group, and have their assignments removed from hello application when they are removed from hello marketing group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="91bcc-108">Microsoft önerir hello kullanarak Azure AD'yi yönetme [Azure AD Yönetim Merkezi](https://aad.portal.azure.com) hello yerine Azure portal hello bu makalede başvurulan Klasik Azure portalı.</span><span class="sxs-lookup"><span data-stu-id="91bcc-108">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span> 

<span data-ttu-id="91bcc-109">Bu özellik, Azure AD uygulama galerisinde hello içinde ekleyebilirsiniz uygulamaları yüzlerce kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="91bcc-109">This capability can be used with hundreds of applications that you can add from within hello Azure AD Application Gallery.</span></span>

<span data-ttu-id="91bcc-110">**bir grup tooa SaaS uygulaması için tooassign erişim**</span><span class="sxs-lookup"><span data-stu-id="91bcc-110">**tooassign access for a group tooa SaaS application**</span></span>

1. <span data-ttu-id="91bcc-111">Merhaba, [Klasik Azure portalı](https://manage.windowsazure.com)seçin **Active Directory** hello hello sol taraftaki gezinti çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="91bcc-111">In hello [Azure classic portal](https://manage.windowsazure.com), select **Active Directory** on hello navigation bar on hello left hand side.</span></span>
2. <span data-ttu-id="91bcc-112">Select hello **Directory** sekmesini ve ardından açık hello dizin tooassign erişim grubu tooa SaaS uygulaması için istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="91bcc-112">Select hello **Directory** tab, and then open hello directory in which you want tooassign access for a group tooa SaaS application.</span></span>
3. <span data-ttu-id="91bcc-113">Select hello **uygulamaları** sekmesi. Uygulama Galerisi hello eklenen bir uygulama seçin ve hello ardından **kullanıcılar ve gruplar** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="91bcc-113">Select hello **Applications** tab. Select an application that you added from hello Application Gallery, and then click  hello **Users and Groups** tab.</span></span>
4. <span data-ttu-id="91bcc-114">Merhaba üzerinde **kullanıcılar ve gruplar** sekmede hello **başlayarak** hello ad alanına, tooassign erişim istediğiniz hello Grup toowhich ve ardından sağ üst hello onay işareti seçin hello.</span><span class="sxs-lookup"><span data-stu-id="91bcc-114">On hello **Users and Groups** tab, in hello **Starting with** field, enter hello name of hello group toowhich you want tooassign access, and then select hello check mark in hello upper right.</span></span> <span data-ttu-id="91bcc-115">Yalnızca tootype hello ilk bölümü bir grubun adı gerekir.</span><span class="sxs-lookup"><span data-stu-id="91bcc-115">You only need tootype hello first part of a group's name.</span></span>
5. <span data-ttu-id="91bcc-116">Merhaba grubunu seçin ve ardından hello seçip **atamak erişim** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="91bcc-116">Select hello group, then then select hello **Assign Access** button.</span></span> <span data-ttu-id="91bcc-117">Seçin **Evet** hello onay iletisi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="91bcc-117">Select **Yes** when you see hello confirmation message.</span></span> <span data-ttu-id="91bcc-118">İç içe geçmiş grup üyelikleri grup tabanlı atama tooapplications için şu anda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="91bcc-118">Nested group memberships are not supported for group-based assignment tooapplications at this time.</span></span>
6. <span data-ttu-id="91bcc-119">Hangi kullanıcıların toohello uygulama, doğrudan veya bir gruba üyelik tarafından atanan de görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="91bcc-119">You can also see which users are assigned toohello application, either directly or by membership in a group.</span></span> <span data-ttu-id="91bcc-120">toodo Bu, değişiklik hello **'Gruplarından' açılır Göster** çok**'Tüm kullanıcılar'**.</span><span class="sxs-lookup"><span data-stu-id="91bcc-120">toodo this, change hello **Show dropdown from 'Groups'** too**'All Users'**.</span></span> <span data-ttu-id="91bcc-121">Merhaba liste hello dizin ve isteyip istemediğinizi her kullanıcı toohello uygulama atanmış kullanıcıları gösterir.</span><span class="sxs-lookup"><span data-stu-id="91bcc-121">hello list shows users in hello directory and whether or not each user is assigned toohello application.</span></span> <span data-ttu-id="91bcc-122">Merhaba liste hello atanan kullanıcıların doğrudan toohello uygulama ('doğrudan' gösterilen atama türü) atanmış olup olmadığını veya grup üyeliği ('Devralınan' gösterilen atama türü), ayrıca gösterir</span><span class="sxs-lookup"><span data-stu-id="91bcc-122">hello list also shows whether hello assigned users are assigned toohello application directly (assignment type shown as 'Direct'), or by virtue of group membership (assignment type shown as 'Inherited.')</span></span>

> [!NOTE]
> <span data-ttu-id="91bcc-123">Yalnızca Azure AD Premium veya Azure AD temel etkinleştirdikten sonra hello kullanıcılar ve Gruplar sekmesinde görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="91bcc-123">You can see hello Users and Groups tab only after you have enabled Azure AD Premium or Azure AD Basic.</span></span>
>
>

### <a name="next-steps"></a><span data-ttu-id="91bcc-124">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="91bcc-124">Next steps</span></span>
<span data-ttu-id="91bcc-125">Bu makalelerde Azure Active Directory ile ilgili ek bilgi sağlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="91bcc-125">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="91bcc-126">Azure Active Directory grupları ile erişim tooresources yönetme</span><span class="sxs-lookup"><span data-stu-id="91bcc-126">Managing access tooresources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="91bcc-127">Azure Active Directory'de Uygulama Yönetimi için Makale Dizini</span><span class="sxs-lookup"><span data-stu-id="91bcc-127">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="91bcc-128">Grup ayarlarını yapılandırmak için Azure Active Directory cmdlet'leri</span><span class="sxs-lookup"><span data-stu-id="91bcc-128">Azure Active Directory cmdlets for configuring group settings</span></span>](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [<span data-ttu-id="91bcc-129">Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="91bcc-129">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="91bcc-130">Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme</span><span class="sxs-lookup"><span data-stu-id="91bcc-130">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
