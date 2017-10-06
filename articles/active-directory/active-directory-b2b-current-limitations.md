---
title: "Azure Active Directory B2B işbirliği aaaLimitations | Microsoft Docs"
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
ms.openlocfilehash: 322081f32fbacfe67ee1300993c7df1870e498bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="limitations-of-azure-ad-b2b-collaboration"></a><span data-ttu-id="024dc-103">Azure AD B2B işbirliği sınırlamaları</span><span class="sxs-lookup"><span data-stu-id="024dc-103">Limitations of Azure AD B2B collaboration</span></span>
<span data-ttu-id="024dc-104">Azure Active Directory (Azure AD) B2B işbirliği şu anda bu makalede açıklanan konu toohello sınırlamalar olur.</span><span class="sxs-lookup"><span data-stu-id="024dc-104">Azure Active Directory (Azure AD) B2B collaboration is currently subject toohello limitations described in this article.</span></span>

## <a name="possible-double-multi-factor-authentication"></a><span data-ttu-id="024dc-105">Olası çift çok faktörlü kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="024dc-105">Possible double multi-factor authentication</span></span>
<span data-ttu-id="024dc-106">Azure AD B2B ile Merhaba kaynak kuruluştaki (kuruluş davet hello) çok faktörlü kimlik doğrulamasını zorunlu kılabilir.</span><span class="sxs-lookup"><span data-stu-id="024dc-106">With Azure AD B2B, you can enforce multi-factor authentication at hello resource organization (hello inviting organization).</span></span> <span data-ttu-id="024dc-107">Bu yaklaşım Hello nedenlerle ayrıntılı olarak [B2B işbirliği kullanıcılar için koşullu erişim](active-directory-b2b-mfa-instructions.md).</span><span class="sxs-lookup"><span data-stu-id="024dc-107">hello reasons for this approach are detailed in [Conditional access for B2B collaboration users](active-directory-b2b-mfa-instructions.md).</span></span> <span data-ttu-id="024dc-108">Bir iş ortağı ayarlama ve zorlanan çok faktörlü kimlik doğrulaması zaten varsa, bunların kullanıcıları tooperform hello kimlik doğrulaması kez giriş kuruluşlarında olabilir ve ardından yeniden size ait.</span><span class="sxs-lookup"><span data-stu-id="024dc-108">If a partner already has multi-factor authentication set up and enforced, their users might have tooperform hello authentication once in their home organization and then again in yours.</span></span>

## <a name="instant-on"></a><span data-ttu-id="024dc-109">Anında açık</span><span class="sxs-lookup"><span data-stu-id="024dc-109">Instant-on</span></span>
<span data-ttu-id="024dc-110">Merhaba B2B işbirliği akışlar, biz kullanıcıların toohello dizin ekleyin ve davet kullanım, uygulama atama ve benzeri sırasında dinamik olarak güncelleştir.</span><span class="sxs-lookup"><span data-stu-id="024dc-110">In hello B2B collaboration flows, we add users toohello directory and dynamically update them during invitation redemption, app assignment, and so on.</span></span> <span data-ttu-id="024dc-111">Merhaba güncelleştirmeleri ve yazma işlemleri genellikle bir dizin örneğinde gerçekleşir ve tüm örneklerde çoğaltılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="024dc-111">hello updates and writes ordinarily happen in one directory instance and must be replicated across all instances.</span></span> <span data-ttu-id="024dc-112">Tüm örnekleri güncelleştirilir sonra çoğaltma tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="024dc-112">Replication is completed once all instances are updated.</span></span> <span data-ttu-id="024dc-113">Bazen zaman hello nesne yazıldığı veya bir örneğinde güncelleştirildi ve hello çağırın tooretrieve bu nesne tooanother çoğaltma gecikmeleri oluşabilir örneğidir.</span><span class="sxs-lookup"><span data-stu-id="024dc-113">Sometimes when hello object is written or updated in one instance and hello call tooretrieve this object is tooanother instance, replication latencies can occur.</span></span> <span data-ttu-id="024dc-114">Bu durumda, yenileme veya toohelp yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="024dc-114">If that happens, refresh or retry toohelp.</span></span> <span data-ttu-id="024dc-115">Bizim API, ardından yeniden deneme bazı kullanarak bir uygulama yazıyorsanız, geri alma iyi, savunma yöntem tooalleviate bu sorunudur.</span><span class="sxs-lookup"><span data-stu-id="024dc-115">If you are writing an app using our API, then retries with some back-off is a good, defensive practice tooalleviate this issue.</span></span>

## <a name="next-steps"></a><span data-ttu-id="024dc-116">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="024dc-116">Next steps</span></span>

<span data-ttu-id="024dc-117">Azure AD B2B işbirliği ile ilgili diğer makalelerimize göz atın:</span><span class="sxs-lookup"><span data-stu-id="024dc-117">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="024dc-118">Azure AD B2B işbirliği nedir?</span><span class="sxs-lookup"><span data-stu-id="024dc-118">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="024dc-119">B2B işbirliği kullanıcı özellikleri</span><span class="sxs-lookup"><span data-stu-id="024dc-119">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="024dc-120">B2B işbirliği kullanıcı tooa rolü ekleme</span><span class="sxs-lookup"><span data-stu-id="024dc-120">Adding a B2B collaboration user tooa role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="024dc-121">B2bB işbirliği davetleri temsilci seçme</span><span class="sxs-lookup"><span data-stu-id="024dc-121">Delegate B2bB collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="024dc-122">Dinamik gruplar ve B2B işbirliği</span><span class="sxs-lookup"><span data-stu-id="024dc-122">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="024dc-123">B2B işbirliği kodu ve PowerShell örnekleri</span><span class="sxs-lookup"><span data-stu-id="024dc-123">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="024dc-124">SaaS uygulamaları B2B işbirliği için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="024dc-124">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="024dc-125">B2B işbirliği kullanıcı belirteçleri</span><span class="sxs-lookup"><span data-stu-id="024dc-125">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="024dc-126">B2B işbirliği kullanıcı taleplerini eşleme</span><span class="sxs-lookup"><span data-stu-id="024dc-126">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="024dc-127">Office 365 dış paylaşım</span><span class="sxs-lookup"><span data-stu-id="024dc-127">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
