---
title: "Azure Active Directory B2B işbirliği aaaDelegate davetleri | Microsoft Docs"
description: "Azure Active Directory B2B işbirliği kullanıcı özellikleri yapılandırılabilir"
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
ms.date: 05/23/2017
ms.author: sasubram
ms.openlocfilehash: c0122d6f60d494c6e251c41d947dc254ea887620
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="delegate-invitations-for-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="74f9b-103">Azure Active Directory B2B işbirliği için temsilci davetleri</span><span class="sxs-lookup"><span data-stu-id="74f9b-103">Delegate invitations for Azure Active Directory B2B collaboration</span></span>

<span data-ttu-id="74f9b-104">Azure Active Directory (Azure AD) işletmeden işletmeye (B2B) işbirliğiyle, toobe bir genel yönetici toosend davetleri gerekmez.</span><span class="sxs-lookup"><span data-stu-id="74f9b-104">With Azure Active Directory (Azure AD) business-to-business (B2B) collaboration, you do not have toobe a global admin toosend invitations.</span></span> <span data-ttu-id="74f9b-105">Bunun yerine, ilkeleri kullanın ve davetleri toousers toosend davetleri izin olan roller atayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="74f9b-105">Instead, you can use policies and delegate invitations toousers whose roles allow them toosend invitations.</span></span> <span data-ttu-id="74f9b-106">Bir önemli yeni yolu toodelegate Konuk kullanıcı davetleri hello Konuk davet eden rolü üzerinden olur.</span><span class="sxs-lookup"><span data-stu-id="74f9b-106">An important new way toodelegate guest user invitations is through hello Guest Inviter role.</span></span>

## <a name="guest-inviter-role"></a><span data-ttu-id="74f9b-107">Konuk davet eden rolü</span><span class="sxs-lookup"><span data-stu-id="74f9b-107">Guest Inviter role</span></span>
<span data-ttu-id="74f9b-108">Sizi davet eden rol toosend davetleri hello kullanıcı tooGuest atayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="74f9b-108">We can assign hello user tooGuest Inviter role toosend invitations.</span></span> <span data-ttu-id="74f9b-109">Merhaba genel yönetici rolü toosend davetleri toobe üyesi yok.</span><span class="sxs-lookup"><span data-stu-id="74f9b-109">You don't have toobe member of hello global admin role toosend invitations.</span></span> <span data-ttu-id="74f9b-110">Varsayılan olarak, normal kullanıcı genel yönetici davetleri normal kullanıcılar için devre dışı bırakılmamışsa hello davet API de çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="74f9b-110">By default, regular users can also invoke hello invite API unless a global admin disabled invitations for regular users.</span></span> <span data-ttu-id="74f9b-111">Bir kullanıcı hello API hello Azure portal veya PowerShell kullanarak da çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="74f9b-111">A user can also invoke hello API using hello Azure portal or PowerShell.</span></span>

<span data-ttu-id="74f9b-112">İşte gösteren bir örnek nasıl toouse PowerShell tooadd kullanıcı toohello Konuk davet eden rolü:</span><span class="sxs-lookup"><span data-stu-id="74f9b-112">Here's an example that shows how toouse PowerShell tooadd a user toohello Guest Inviter role:</span></span>

```
Add-MsolRoleMember -RoleObjectId 95e79109-95c0-4d8e-aee3-d01accf2d47b -RoleMemberEmailAddress <RoleMemberEmailAddress>
```

## <a name="control-who-can-invite"></a><span data-ttu-id="74f9b-113">Davet edebilirsiniz denetimi</span><span class="sxs-lookup"><span data-stu-id="74f9b-113">Control who can invite</span></span>

![Denetim nasıl tooinvite](media/active-directory-b2b-delegate-invitations/control-who-to-invite.png)

<span data-ttu-id="74f9b-115">Azure AD B2B işbirliği ile bir kiracı Yöneticisi aşağıdaki davet ilkeler hello ayarlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="74f9b-115">With Azure AD B2B collaboration, a tenant admin can set hello following invitation policies:</span></span>

- <span data-ttu-id="74f9b-116">Davetiye devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="74f9b-116">Turn off invitations</span></span>
- <span data-ttu-id="74f9b-117">Yalnızca Yöneticiler ve kullanıcılar hello Konuk davet eden rolündeki davet edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="74f9b-117">Only admins and users in hello Guest Inviter role can invite</span></span>
- <span data-ttu-id="74f9b-118">Yöneticiler, hello Konuk davet eden rolü ve üyeleri davet edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="74f9b-118">Admins, hello Guest Inviter role, and members can invite</span></span>
- <span data-ttu-id="74f9b-119">Konuklar, dahil tüm kullanıcıları davet edebilir</span><span class="sxs-lookup"><span data-stu-id="74f9b-119">All users, including guests, can invite</span></span>

<span data-ttu-id="74f9b-120">Varsayılan olarak, kiracılar çok ayarlanır #4.</span><span class="sxs-lookup"><span data-stu-id="74f9b-120">By default, tenants are set too#4.</span></span> <span data-ttu-id="74f9b-121">(Tüm kullanıcılar, Konuklar, dahil B2B kullanıcıları davet edebilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="74f9b-121">(All users, including guests, can invite B2B users.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="74f9b-122">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="74f9b-122">Next steps</span></span>

<span data-ttu-id="74f9b-123">Azure AD B2B işbirliği ile ilgili diğer makalelerimize göz atın:</span><span class="sxs-lookup"><span data-stu-id="74f9b-123">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="74f9b-124">Azure AD B2B işbirliği nedir?</span><span class="sxs-lookup"><span data-stu-id="74f9b-124">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="74f9b-125">B2B işbirliği kullanıcı özellikleri</span><span class="sxs-lookup"><span data-stu-id="74f9b-125">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="74f9b-126">B2B işbirliği kullanıcı tooa rolü ekleme</span><span class="sxs-lookup"><span data-stu-id="74f9b-126">Adding a B2B collaboration user tooa role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="74f9b-127">Dinamik gruplar ve B2B işbirliği</span><span class="sxs-lookup"><span data-stu-id="74f9b-127">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="74f9b-128">B2B işbirliği kodu ve PowerShell örnekleri</span><span class="sxs-lookup"><span data-stu-id="74f9b-128">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="74f9b-129">SaaS uygulamaları B2B işbirliği için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="74f9b-129">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="74f9b-130">B2B işbirliği kullanıcı belirteçleri</span><span class="sxs-lookup"><span data-stu-id="74f9b-130">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="74f9b-131">B2B işbirliği kullanıcı taleplerini eşleme</span><span class="sxs-lookup"><span data-stu-id="74f9b-131">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="74f9b-132">Office 365 dış paylaşım</span><span class="sxs-lookup"><span data-stu-id="74f9b-132">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="74f9b-133">B2B işbirliği geçerli sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="74f9b-133">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
