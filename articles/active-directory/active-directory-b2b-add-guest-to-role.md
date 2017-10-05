---
title: "Bir Azure Active Directory B2B işbirliği kullanıcı role ekleme | Microsoft Docs"
description: "Azure Active Directory'de bir rolü Konuk kullanıcı ekleme"
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
ms.date: 03/15/2017
ms.author: sasubram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e816349ea971c997f655b4d51672dba666bc3e89
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="grant-permissions-to-users-from-partner-organizations-in-your-azure-active-directory-tenant"></a><span data-ttu-id="768ad-103">Azure Active Directory kiracınızda iş ortağı kuruluşlardan kullanıcıların izinleri verin</span><span class="sxs-lookup"><span data-stu-id="768ad-103">Grant permissions to users from partner organizations in your Azure Active Directory tenant</span></span>

<span data-ttu-id="768ad-104">Azure Active Directory (Azure AD) B2B işbirliği kullanıcılar dizinine Konuk kullanıcılar olarak eklenir ve varsayılan olarak kısıtlı dizinde Konuk izinleri.</span><span class="sxs-lookup"><span data-stu-id="768ad-104">Azure Active Directory (Azure AD) B2B collaboration users are added as guest users to the directory, and guest permissions in the directory are restricted by default.</span></span> <span data-ttu-id="768ad-105">İş, kuruluşunuzda daha yüksek ayrıcalıklı rolleri doldurmak için bazı Konuk kullanıcılar gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="768ad-105">Your business may need some guest users to fill higher-privilege roles in your organization.</span></span> <span data-ttu-id="768ad-106">Daha yüksek ayrıcalıklı rolleri tanımlama desteklemek için konuk kullanıcılar istediğiniz, kuruluşunuzun ihtiyaçlarına göre herhangi bir rol için eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="768ad-106">To support defining higher-privilege roles, guest users can be added to any roles you desire, based on your organization's needs.</span></span>

## <a name="default-role"></a><span data-ttu-id="768ad-107">Varsayılan rol</span><span class="sxs-lookup"><span data-stu-id="768ad-107">Default role</span></span>

![Varsayılan rol](./media/active-directory-b2b-add-guest-to-role/default-role.png)

## <a name="global-administrator-role"></a><span data-ttu-id="768ad-109">Genel yönetici rolü</span><span class="sxs-lookup"><span data-stu-id="768ad-109">Global Administrator Role</span></span>

![Genel yönetici rolü](./media/active-directory-b2b-add-guest-to-role/global-admin-role.png)

## <a name="limited-administrator-role"></a><span data-ttu-id="768ad-111">Sınırlı Yönetici rolü</span><span class="sxs-lookup"><span data-stu-id="768ad-111">Limited Administrator Role</span></span>

![sınırlı yönetim rolü](./media/active-directory-b2b-add-guest-to-role/limited-admin-role.png)

## <a name="next-steps"></a><span data-ttu-id="768ad-113">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="768ad-113">Next steps</span></span>

<span data-ttu-id="768ad-114">Azure AD B2B işbirliği ile ilgili diğer makalelerimize göz atın:</span><span class="sxs-lookup"><span data-stu-id="768ad-114">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="768ad-115">Azure AD B2B işbirliği nedir?</span><span class="sxs-lookup"><span data-stu-id="768ad-115">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="768ad-116">B2B işbirliği kullanıcı özellikleri</span><span class="sxs-lookup"><span data-stu-id="768ad-116">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="768ad-117">B2bB işbirliği davetleri temsilci seçme</span><span class="sxs-lookup"><span data-stu-id="768ad-117">Delegate B2bB collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="768ad-118">Dinamik gruplar ve B2B işbirliği</span><span class="sxs-lookup"><span data-stu-id="768ad-118">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="768ad-119">B2B işbirliği kodu ve PowerShell örnekleri</span><span class="sxs-lookup"><span data-stu-id="768ad-119">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="768ad-120">SaaS uygulamaları B2B işbirliği için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="768ad-120">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="768ad-121">B2B işbirliği kullanıcı belirteçleri</span><span class="sxs-lookup"><span data-stu-id="768ad-121">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="768ad-122">B2B işbirliği kullanıcı taleplerini eşleme</span><span class="sxs-lookup"><span data-stu-id="768ad-122">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="768ad-123">Office 365 dış paylaşım</span><span class="sxs-lookup"><span data-stu-id="768ad-123">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="768ad-124">B2B işbirliği geçerli sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="768ad-124">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
