---
title: "Azure Active Directory B2B işbirliği için davet temsilci | Microsoft Docs"
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
ms.openlocfilehash: 78613cc978b585a98d235245194c02371f7f3849
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="delegate-invitations-for-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="b98fa-103">Azure Active Directory B2B işbirliği için temsilci davetleri</span><span class="sxs-lookup"><span data-stu-id="b98fa-103">Delegate invitations for Azure Active Directory B2B collaboration</span></span>

<span data-ttu-id="b98fa-104">Azure Active Directory (Azure AD) işletmeden işletmeye (B2B) işbirliğiyle Davetleri Gönder için genel yönetici olmanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="b98fa-104">With Azure Active Directory (Azure AD) business-to-business (B2B) collaboration, you do not have to be a global admin to send invitations.</span></span> <span data-ttu-id="b98fa-105">Bunun yerine, ilkeleri kullanın ve kullanıcıları, rolleri Davetleri Gönder izin davetleri atayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b98fa-105">Instead, you can use policies and delegate invitations to users whose roles allow them to send invitations.</span></span> <span data-ttu-id="b98fa-106">Konuk kullanıcı davetleri temsilci için önemli bir yeni yol Konuk davet eden rolüdür.</span><span class="sxs-lookup"><span data-stu-id="b98fa-106">An important new way to delegate guest user invitations is through the Guest Inviter role.</span></span>

## <a name="guest-inviter-role"></a><span data-ttu-id="b98fa-107">Konuk davet eden rolü</span><span class="sxs-lookup"><span data-stu-id="b98fa-107">Guest Inviter role</span></span>
<span data-ttu-id="b98fa-108">Biz kullanıcı davet göndermek için konuk davet eden rolüne atayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b98fa-108">We can assign the user to Guest Inviter role to send invitations.</span></span> <span data-ttu-id="b98fa-109">Davetiye göndermek için genel yönetici rolünün üyesi olması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="b98fa-109">You don't have to be member of the global admin role to send invitations.</span></span> <span data-ttu-id="b98fa-110">Varsayılan olarak, genel yönetici davetleri normal kullanıcılar için devre dışı bırakılmamışsa normal kullanıcıların davet API de çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b98fa-110">By default, regular users can also invoke the invite API unless a global admin disabled invitations for regular users.</span></span> <span data-ttu-id="b98fa-111">Bir kullanıcı Azure portal veya PowerShell kullanarak API de çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b98fa-111">A user can also invoke the API using the Azure portal or PowerShell.</span></span>

<span data-ttu-id="b98fa-112">PowerShell Konuk davet eden role bir kullanıcı eklemek için nasıl kullanılacağını gösteren örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="b98fa-112">Here's an example that shows how to use PowerShell to add a user to the Guest Inviter role:</span></span>

```
Add-MsolRoleMember -RoleObjectId 95e79109-95c0-4d8e-aee3-d01accf2d47b -RoleMemberEmailAddress <RoleMemberEmailAddress>
```

## <a name="control-who-can-invite"></a><span data-ttu-id="b98fa-113">Davet edebilirsiniz denetimi</span><span class="sxs-lookup"><span data-stu-id="b98fa-113">Control who can invite</span></span>

![Davet etme denetleme](media/active-directory-b2b-delegate-invitations/control-who-to-invite.png)

<span data-ttu-id="b98fa-115">Azure AD B2B işbirliği ile bir kiracı Yöneticisi aşağıdaki davet ilkeleri ayarlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b98fa-115">With Azure AD B2B collaboration, a tenant admin can set the following invitation policies:</span></span>

- <span data-ttu-id="b98fa-116">Davetiye devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="b98fa-116">Turn off invitations</span></span>
- <span data-ttu-id="b98fa-117">Yalnızca Yöneticiler ve kullanıcılar Konuk davet eden rolündeki davet edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="b98fa-117">Only admins and users in the Guest Inviter role can invite</span></span>
- <span data-ttu-id="b98fa-118">Yöneticiler, Konuk davet eden rolü ve üyeleri davet edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="b98fa-118">Admins, the Guest Inviter role, and members can invite</span></span>
- <span data-ttu-id="b98fa-119">Konuklar, dahil tüm kullanıcıları davet edebilir</span><span class="sxs-lookup"><span data-stu-id="b98fa-119">All users, including guests, can invite</span></span>

<span data-ttu-id="b98fa-120">Varsayılan olarak, kiracılar #4'e ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="b98fa-120">By default, tenants are set to #4.</span></span> <span data-ttu-id="b98fa-121">(Tüm kullanıcılar, Konuklar, dahil B2B kullanıcıları davet edebilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="b98fa-121">(All users, including guests, can invite B2B users.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="b98fa-122">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b98fa-122">Next steps</span></span>

<span data-ttu-id="b98fa-123">Azure AD B2B işbirliği ile ilgili diğer makalelerimize göz atın:</span><span class="sxs-lookup"><span data-stu-id="b98fa-123">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="b98fa-124">Azure AD B2B işbirliği nedir?</span><span class="sxs-lookup"><span data-stu-id="b98fa-124">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="b98fa-125">B2B işbirliği kullanıcı özellikleri</span><span class="sxs-lookup"><span data-stu-id="b98fa-125">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="b98fa-126">Bir role B2B işbirliği kullanıcı ekleme</span><span class="sxs-lookup"><span data-stu-id="b98fa-126">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="b98fa-127">Dinamik gruplar ve B2B işbirliği</span><span class="sxs-lookup"><span data-stu-id="b98fa-127">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="b98fa-128">B2B işbirliği kodu ve PowerShell örnekleri</span><span class="sxs-lookup"><span data-stu-id="b98fa-128">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="b98fa-129">SaaS uygulamaları B2B işbirliği için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b98fa-129">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="b98fa-130">B2B işbirliği kullanıcı belirteçleri</span><span class="sxs-lookup"><span data-stu-id="b98fa-130">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="b98fa-131">B2B işbirliği kullanıcı taleplerini eşleme</span><span class="sxs-lookup"><span data-stu-id="b98fa-131">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="b98fa-132">Office 365 dış paylaşım</span><span class="sxs-lookup"><span data-stu-id="b98fa-132">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="b98fa-133">B2B işbirliği geçerli sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="b98fa-133">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
