---
title: "Dinamik gruplar ve Azure Active Directory B2B işbirliği | Microsoft Docs"
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
ms.openlocfilehash: 5818c41610c8c5df89abcb0dcd058bcbe9579ce7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="dynamic-groups-and-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="e42ac-103">Dinamik gruplar ve Azure Active Directory B2B işbirliği</span><span class="sxs-lookup"><span data-stu-id="e42ac-103">Dynamic groups and Azure Active Directory B2B collaboration</span></span>

## <a name="what-are-dynamic-groups"></a><span data-ttu-id="e42ac-104">Dinamik grupların nelerdir?</span><span class="sxs-lookup"><span data-stu-id="e42ac-104">What are dynamic groups?</span></span>
<span data-ttu-id="e42ac-105">Azure Active Directory (Azure AD) için dinamik yapılandırma, güvenlik grubunun üyeliği kullanılabilir [Azure portalı](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e42ac-105">Dynamic configuration of security group membership for Azure Active Directory (Azure AD) is available in [the Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="e42ac-106">Yöneticiler için Azure Active Directory'de (örneğin, userType, bölüme veya ülke) kullanıcı özniteliklerini temel alarak oluşturulan grupları doldurmak için kurallar ayarlayabilir.</span><span class="sxs-lookup"><span data-stu-id="e42ac-106">Administrators can set rules to populate groups that are created in Azure Active Directory based on user attributes (such as userType, department, or country).</span></span> <span data-ttu-id="e42ac-107">Üyeler otomatik olarak eklenecek veya bunların özniteliklerini temel alarak bir güvenlik grubu kaldırıldı.</span><span class="sxs-lookup"><span data-stu-id="e42ac-107">Members can be automatically added to or removed from a security group based on their attributes.</span></span> <span data-ttu-id="e42ac-108">Bu grupları, uygulamalar veya Bulut kaynakları (SharePoint siteleri, belgeleri) ve üyelerine lisansları atamak için erişim sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="e42ac-108">These groups can provide access to applications or cloud resources (SharePoint sites, documents) and to assign licenses to members.</span></span> <span data-ttu-id="e42ac-109">Dinamik grupları hakkında daha fazla bilgiyi [ayrılmış Azure Active Directory'deki grupları](active-directory-accessmanagement-dedicated-groups.md).</span><span class="sxs-lookup"><span data-stu-id="e42ac-109">Read more about dynamic groups in [Dedicated groups in Azure Active Directory](active-directory-accessmanagement-dedicated-groups.md).</span></span>

<span data-ttu-id="e42ac-110">Uygun [lisans Azure AD Premium P1 veya P2](https://azure.microsoft.com/pricing/details/active-directory/) dinamik grupları oluşturma ve kullanma için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="e42ac-110">The appropriate [Azure AD Premium P1 or P2 licensing](https://azure.microsoft.com/pricing/details/active-directory/) is required to create and use dynamic groups.</span></span> <span data-ttu-id="e42ac-111">Makalede daha fazla bilgi edinin [öznitelik tabanlı kurallar dinamik grup üyeliği için Azure Active Directory'de oluşturmak](active-directory-groups-dynamic-membership-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e42ac-111">Learn more in the article [Create attribute-based rules for dynamic group membership in Azure Active Directory](active-directory-groups-dynamic-membership-azure-portal.md).</span></span>

## <a name="what-are-the-built-in-dynamic-groups"></a><span data-ttu-id="e42ac-112">Yerleşik dinamik grupların nelerdir?</span><span class="sxs-lookup"><span data-stu-id="e42ac-112">What are the built-in dynamic groups?</span></span>
<span data-ttu-id="e42ac-113">**Tüm kullanıcılar** dinamik Grup tek bir tıklatmayla kiracıdaki tüm kullanıcıları içeren bir grup oluşturmak Kiracı yöneticileri sağlar.</span><span class="sxs-lookup"><span data-stu-id="e42ac-113">The **All users** dynamic group enables tenant admins to create a group containing all users in the tenant with a single click.</span></span> <span data-ttu-id="e42ac-114">Varsayılan olarak, **tüm kullanıcılar** Grup üyeleri ve konuklar dahil olmak üzere dizinde tüm kullanıcıları içerir.</span><span class="sxs-lookup"><span data-stu-id="e42ac-114">By default, the **All users** group includes all users in the directory, including Members and Guests.</span></span>
<span data-ttu-id="e42ac-115">Yeni Azure Active Directory Yönetim portalını etkinleştirmeyi seçebilirsiniz **tüm kullanıcılar** grup ayarları görünümünde grubu.</span><span class="sxs-lookup"><span data-stu-id="e42ac-115">Within the new Azure Active Directory admin portal, you can choose to enable the **All users** group in the Group Settings view.</span></span>

![yerleşik gruplar](media/active-directory-b2b-dynamic-groups/built-in-groups.png)

## <a name="hardening-the-all-users-dynamic-group"></a><span data-ttu-id="e42ac-117">Tüm kullanıcılar dinamik Grup sağlamlaştırma</span><span class="sxs-lookup"><span data-stu-id="e42ac-117">Hardening the All users dynamic group</span></span>
<span data-ttu-id="e42ac-118">Varsayılan olarak, **tüm kullanıcılar** grubu B2B işbirliği (konuk) kullanıcılarınızın de içerir.</span><span class="sxs-lookup"><span data-stu-id="e42ac-118">By default, the **All users** group contains your B2B collaboration (guest) users as well.</span></span> <span data-ttu-id="e42ac-119">Daha fazla güvenli, **tüm kullanıcılar** Konuk kullanıcılar kaldırmak için bir kural kullanarak göre gruplandırın.</span><span class="sxs-lookup"><span data-stu-id="e42ac-119">You can further secure your **All users** group by using a rule to remove guest users.</span></span> <span data-ttu-id="e42ac-120">Aşağıdaki çizimde gösterildiği **tüm kullanıcılar** grubunu değiştiren konuklar dışlanacak.</span><span class="sxs-lookup"><span data-stu-id="e42ac-120">The following illustration shows the **All users** group modified to exclude guests.</span></span>

![tüm kullanıcılar grubu etkinleştir](media/active-directory-b2b-dynamic-groups/enable-all-users-group.png)

<span data-ttu-id="e42ac-122">Ayrıca Konuk kullanıcılar yalnızca kendilerine içerir ve böylece (örneğin, Azure AD koşullu erişim ilkeleri) ilkeleri uygulayabilirsiniz yeni dinamik bir grup oluşturmak yararlı.</span><span class="sxs-lookup"><span data-stu-id="e42ac-122">You might also find it useful to create a new dynamic group that contains only guest users, so that you can apply policies (such as Azure AD Conditional Access policies) to them.</span></span>
<span data-ttu-id="e42ac-123">Ne tür bir grup aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="e42ac-123">What such a group might look like:</span></span>

![Konuk kullanıcılar Dışla](media/active-directory-b2b-dynamic-groups/exclude-guest-users.png)

## <a name="next-steps"></a><span data-ttu-id="e42ac-125">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e42ac-125">Next steps</span></span>

<span data-ttu-id="e42ac-126">Azure AD B2B işbirliği ile ilgili diğer makalelerimize göz atın:</span><span class="sxs-lookup"><span data-stu-id="e42ac-126">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="e42ac-127">Azure AD B2B işbirliği nedir?</span><span class="sxs-lookup"><span data-stu-id="e42ac-127">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="e42ac-128">B2B işbirliği kullanıcı özellikleri</span><span class="sxs-lookup"><span data-stu-id="e42ac-128">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="e42ac-129">Bir role B2B işbirliği kullanıcı ekleme</span><span class="sxs-lookup"><span data-stu-id="e42ac-129">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="e42ac-130">B2B işbirliği davetleri temsilci seçme</span><span class="sxs-lookup"><span data-stu-id="e42ac-130">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="e42ac-131">B2B işbirliği kodu ve PowerShell örnekleri</span><span class="sxs-lookup"><span data-stu-id="e42ac-131">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="e42ac-132">SaaS uygulamaları B2B işbirliği için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="e42ac-132">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="e42ac-133">B2B işbirliği kullanıcı belirteçleri</span><span class="sxs-lookup"><span data-stu-id="e42ac-133">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="e42ac-134">B2B işbirliği kullanıcı taleplerini eşleme</span><span class="sxs-lookup"><span data-stu-id="e42ac-134">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="e42ac-135">Office 365 dış paylaşım</span><span class="sxs-lookup"><span data-stu-id="e42ac-135">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="e42ac-136">B2B işbirliği geçerli sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="e42ac-136">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
