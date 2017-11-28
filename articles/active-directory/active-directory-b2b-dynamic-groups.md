---
title: "aaaDynamic grupları ve Azure Active Directory B2B işbirliği | Microsoft Docs"
description: "Azure Active Directory B2B işbirliği dinamik Azure AD grupları ile kullanılabilir"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 06/27/2017
ms.author: curtand
ms.reviewer: sasubram
ms.openlocfilehash: b011298de5fd2c851c6d9caaf5c2b257807ef0a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-groups-and-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="ec87b-103">Dinamik gruplar ve Azure Active Directory B2B işbirliği</span><span class="sxs-lookup"><span data-stu-id="ec87b-103">Dynamic groups and Azure Active Directory B2B collaboration</span></span>

## <a name="what-are-dynamic-groups"></a><span data-ttu-id="ec87b-104">Dinamik grupların nelerdir?</span><span class="sxs-lookup"><span data-stu-id="ec87b-104">What are dynamic groups?</span></span>
<span data-ttu-id="ec87b-105">Azure Active Directory (Azure AD) için dinamik yapılandırma, güvenlik grubunun üyeliği kullanılabilir [Azure portal hello](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ec87b-105">Dynamic configuration of security group membership for Azure Active Directory (Azure AD) is available in [hello Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="ec87b-106">Yöneticiler, Azure Active Directory'de oluşturulan toopopulate grupları (örneğin, userType, bölüme veya ülke) kullanıcı özniteliklerini temel alarak kurallar ayarlayabilir.</span><span class="sxs-lookup"><span data-stu-id="ec87b-106">Administrators can set rules toopopulate groups that are created in Azure Active Directory based on user attributes (such as userType, department, or country).</span></span> <span data-ttu-id="ec87b-107">Üyeleri, kendi özniteliklerini temel alarak bir güvenlik grubu tooor kaldırılmasını otomatik olarak eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="ec87b-107">Members can be automatically added tooor removed from a security group based on their attributes.</span></span> <span data-ttu-id="ec87b-108">Tooassign toomembers lisansları ve bu grupları tooapplications veya Bulut kaynakları (SharePoint siteleri, belgeleri) erişim sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ec87b-108">These groups can provide access tooapplications or cloud resources (SharePoint sites, documents) and tooassign licenses toomembers.</span></span> <span data-ttu-id="ec87b-109">Dinamik grupları hakkında daha fazla bilgiyi [ayrılmış Azure Active Directory'deki grupları](active-directory-accessmanagement-dedicated-groups.md).</span><span class="sxs-lookup"><span data-stu-id="ec87b-109">Read more about dynamic groups in [Dedicated groups in Azure Active Directory](active-directory-accessmanagement-dedicated-groups.md).</span></span>

<span data-ttu-id="ec87b-110">Merhaba uygun [lisans Azure AD Premium P1 veya P2](https://azure.microsoft.com/pricing/details/active-directory/) gerekli toocreate ve kullanım dinamik grupları.</span><span class="sxs-lookup"><span data-stu-id="ec87b-110">hello appropriate [Azure AD Premium P1 or P2 licensing](https://azure.microsoft.com/pricing/details/active-directory/) is required toocreate and use dynamic groups.</span></span> <span data-ttu-id="ec87b-111">Merhaba makalede daha fazla bilgi edinin [öznitelik tabanlı kurallar dinamik grup üyeliği için Azure Active Directory'de oluşturmak](active-directory-groups-dynamic-membership-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ec87b-111">Learn more in hello article [Create attribute-based rules for dynamic group membership in Azure Active Directory](active-directory-groups-dynamic-membership-azure-portal.md).</span></span>

## <a name="what-are-hello-built-in-dynamic-groups"></a><span data-ttu-id="ec87b-112">Merhaba yerleşik dinamik grupların nelerdir?</span><span class="sxs-lookup"><span data-stu-id="ec87b-112">What are hello built-in dynamic groups?</span></span>
<span data-ttu-id="ec87b-113">Merhaba **tüm kullanıcılar** dinamik Grup tek bir hello kiracıdaki tüm kullanıcıları içeren bir grubu tıklatın Kiracı yöneticileri toocreate sağlar.</span><span class="sxs-lookup"><span data-stu-id="ec87b-113">hello **All users** dynamic group enables tenant admins toocreate a group containing all users in hello tenant with a single click.</span></span> <span data-ttu-id="ec87b-114">Varsayılan olarak, hello **tüm kullanıcılar** Grup üyeleri ve konuklar gibi hello dizinde tüm kullanıcıları içerir.</span><span class="sxs-lookup"><span data-stu-id="ec87b-114">By default, hello **All users** group includes all users in hello directory, including Members and Guests.</span></span>
<span data-ttu-id="ec87b-115">Merhaba yeni Azure Active Directory Yönetim Portalı içinden tooenable hello seçebilirsiniz **tüm kullanıcılar** Grup ayarlarını görüntülemek hello grubu.</span><span class="sxs-lookup"><span data-stu-id="ec87b-115">Within hello new Azure Active Directory admin portal, you can choose tooenable hello **All users** group in hello Group Settings view.</span></span>

![yerleşik gruplar](media/active-directory-b2b-dynamic-groups/built-in-groups.png)

## <a name="hardening-hello-all-users-dynamic-group"></a><span data-ttu-id="ec87b-117">Sağlamlaştırma hello tüm kullanıcılar dinamik Grup</span><span class="sxs-lookup"><span data-stu-id="ec87b-117">Hardening hello All users dynamic group</span></span>
<span data-ttu-id="ec87b-118">Varsayılan olarak, hello **tüm kullanıcılar** grubu B2B işbirliği (konuk) kullanıcılarınızın de içerir.</span><span class="sxs-lookup"><span data-stu-id="ec87b-118">By default, hello **All users** group contains your B2B collaboration (guest) users as well.</span></span> <span data-ttu-id="ec87b-119">Daha fazla güvenli, **tüm kullanıcılar** bir kural tooremove Konuk kullanıcılar kullanarak grup.</span><span class="sxs-lookup"><span data-stu-id="ec87b-119">You can further secure your **All users** group by using a rule tooremove guest users.</span></span> <span data-ttu-id="ec87b-120">Merhaba aşağıda gösterilmiştir hello **tüm kullanıcılar** grubunu tooexclude konuklar değiştirdi.</span><span class="sxs-lookup"><span data-stu-id="ec87b-120">hello following illustration shows hello **All users** group modified tooexclude guests.</span></span>

![tüm kullanıcılar grubu etkinleştir](media/active-directory-b2b-dynamic-groups/enable-all-users-group.png)

<span data-ttu-id="ec87b-122">Böylece ilkeleri (örneğin, Azure AD koşullu erişim ilkeleri) toothem uygulayabilirsiniz yararlı toocreate yalnızca konuk kullanıcılar içeren yeni bir dinamik Grup bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ec87b-122">You might also find it useful toocreate a new dynamic group that contains only guest users, so that you can apply policies (such as Azure AD Conditional Access policies) toothem.</span></span>
<span data-ttu-id="ec87b-123">Ne tür bir grup aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="ec87b-123">What such a group might look like:</span></span>

![Konuk kullanıcılar Dışla](media/active-directory-b2b-dynamic-groups/exclude-guest-users.png)

## <a name="next-steps"></a><span data-ttu-id="ec87b-125">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ec87b-125">Next steps</span></span>

<span data-ttu-id="ec87b-126">Azure AD B2B işbirliği ile ilgili diğer makalelerimize göz atın:</span><span class="sxs-lookup"><span data-stu-id="ec87b-126">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="ec87b-127">Azure AD B2B işbirliği nedir?</span><span class="sxs-lookup"><span data-stu-id="ec87b-127">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="ec87b-128">B2B işbirliği kullanıcı özellikleri</span><span class="sxs-lookup"><span data-stu-id="ec87b-128">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="ec87b-129">B2B işbirliği kullanıcı tooa rolü ekleme</span><span class="sxs-lookup"><span data-stu-id="ec87b-129">Adding a B2B collaboration user tooa role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="ec87b-130">B2B işbirliği davetleri temsilci seçme</span><span class="sxs-lookup"><span data-stu-id="ec87b-130">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="ec87b-131">B2B işbirliği kodu ve PowerShell örnekleri</span><span class="sxs-lookup"><span data-stu-id="ec87b-131">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="ec87b-132">SaaS uygulamaları B2B işbirliği için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ec87b-132">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="ec87b-133">B2B işbirliği kullanıcı belirteçleri</span><span class="sxs-lookup"><span data-stu-id="ec87b-133">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="ec87b-134">B2B işbirliği kullanıcı taleplerini eşleme</span><span class="sxs-lookup"><span data-stu-id="ec87b-134">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="ec87b-135">Office 365 dış paylaşım</span><span class="sxs-lookup"><span data-stu-id="ec87b-135">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="ec87b-136">B2B işbirliği geçerli sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="ec87b-136">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
