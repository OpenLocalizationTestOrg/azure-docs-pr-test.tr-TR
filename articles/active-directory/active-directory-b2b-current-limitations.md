---
title: "Azure Active Directory B2B işbirliği sınırlamaları | Microsoft Docs"
description: "Azure Active Directory B2B işbirliği geçerli sınırlamalar"
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
ms.openlocfilehash: 581e5d1fb5fb08d0dc89ed2c85edcb5f0005650b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="limitations-of-azure-ad-b2b-collaboration"></a><span data-ttu-id="2f196-103">Azure AD B2B işbirliği sınırlamaları</span><span class="sxs-lookup"><span data-stu-id="2f196-103">Limitations of Azure AD B2B collaboration</span></span>
<span data-ttu-id="2f196-104">Azure Active Directory (Azure AD) B2B işbirliği şu anda bu makalede açıklanan sınırlamalara tabidir.</span><span class="sxs-lookup"><span data-stu-id="2f196-104">Azure Active Directory (Azure AD) B2B collaboration is currently subject to the limitations described in this article.</span></span>

## <a name="possible-double-multi-factor-authentication"></a><span data-ttu-id="2f196-105">Olası çift çok faktörlü kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="2f196-105">Possible double multi-factor authentication</span></span>
<span data-ttu-id="2f196-106">Azure AD B2B ile kaynak kuruluştaki (davet kuruluş) çok faktörlü kimlik doğrulamasını zorunlu kılabilir.</span><span class="sxs-lookup"><span data-stu-id="2f196-106">With Azure AD B2B, you can enforce multi-factor authentication at the resource organization (the inviting organization).</span></span> <span data-ttu-id="2f196-107">Bu yaklaşım nedenlerle ayrıntıları [B2B işbirliği kullanıcılar için koşullu erişim](active-directory-b2b-mfa-instructions.md).</span><span class="sxs-lookup"><span data-stu-id="2f196-107">The reasons for this approach are detailed in [Conditional access for B2B collaboration users](active-directory-b2b-mfa-instructions.md).</span></span> <span data-ttu-id="2f196-108">Bir iş ortağı ayarlama ve zorlanan çok faktörlü kimlik doğrulaması zaten varsa, ev kuruluşlarında bir kez kimlik doğrulaması yapmak, kullanıcılar olabilir ve ardından yeniden size ait.</span><span class="sxs-lookup"><span data-stu-id="2f196-108">If a partner already has multi-factor authentication set up and enforced, their users might have to perform the authentication once in their home organization and then again in yours.</span></span>

## <a name="instant-on"></a><span data-ttu-id="2f196-109">Anında açık</span><span class="sxs-lookup"><span data-stu-id="2f196-109">Instant-on</span></span>
<span data-ttu-id="2f196-110">B2B işbirliği akışları içinde dizine kullanıcılar eklemek ve davet kullanım, uygulama atama ve benzeri sırasında dinamik olarak güncelleştir.</span><span class="sxs-lookup"><span data-stu-id="2f196-110">In the B2B collaboration flows, we add users to the directory and dynamically update them during invitation redemption, app assignment, and so on.</span></span> <span data-ttu-id="2f196-111">Güncelleştirmeleri ve yazma işlemleri genellikle bir dizin örneğinde gerçekleşir ve tüm örneklerde çoğaltılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="2f196-111">The updates and writes ordinarily happen in one directory instance and must be replicated across all instances.</span></span> <span data-ttu-id="2f196-112">Tüm örnekleri güncelleştirilir sonra çoğaltma tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="2f196-112">Replication is completed once all instances are updated.</span></span> <span data-ttu-id="2f196-113">Bazen nesne yazılmış ya da bir örneğinde güncelleştirilmiş ve bu nesne almak için başka bir örneğine çağrıdır, çoğaltma gecikmeleri oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="2f196-113">Sometimes when the object is written or updated in one instance and the call to retrieve this object is to another instance, replication latencies can occur.</span></span> <span data-ttu-id="2f196-114">Bu durumda, yenileme veya yardımcı olması için yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="2f196-114">If that happens, refresh or retry to help.</span></span> <span data-ttu-id="2f196-115">Bizim API kullanarak bir uygulama yazıyorsanız, bazı geri alma ile yeniden deneme ise bu sorunu gidermek için iyi, savunma bir yöntem.</span><span class="sxs-lookup"><span data-stu-id="2f196-115">If you are writing an app using our API, then retries with some back-off is a good, defensive practice to alleviate this issue.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2f196-116">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2f196-116">Next steps</span></span>

<span data-ttu-id="2f196-117">Azure AD B2B işbirliği ile ilgili diğer makalelerimize göz atın:</span><span class="sxs-lookup"><span data-stu-id="2f196-117">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="2f196-118">Azure AD B2B işbirliği nedir?</span><span class="sxs-lookup"><span data-stu-id="2f196-118">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="2f196-119">B2B işbirliği kullanıcı özellikleri</span><span class="sxs-lookup"><span data-stu-id="2f196-119">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="2f196-120">Bir role B2B işbirliği kullanıcı ekleme</span><span class="sxs-lookup"><span data-stu-id="2f196-120">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="2f196-121">B2bB işbirliği davetleri temsilci seçme</span><span class="sxs-lookup"><span data-stu-id="2f196-121">Delegate B2bB collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="2f196-122">Dinamik gruplar ve B2B işbirliği</span><span class="sxs-lookup"><span data-stu-id="2f196-122">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="2f196-123">B2B işbirliği kodu ve PowerShell örnekleri</span><span class="sxs-lookup"><span data-stu-id="2f196-123">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="2f196-124">SaaS uygulamaları B2B işbirliği için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="2f196-124">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="2f196-125">B2B işbirliği kullanıcı belirteçleri</span><span class="sxs-lookup"><span data-stu-id="2f196-125">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="2f196-126">B2B işbirliği kullanıcı taleplerini eşleme</span><span class="sxs-lookup"><span data-stu-id="2f196-126">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="2f196-127">Office 365 dış paylaşım</span><span class="sxs-lookup"><span data-stu-id="2f196-127">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
