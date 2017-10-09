---
title: "aaaOffice 365 dış paylaşım ve Azure Active Directory B2B işbirliği | Microsoft Docs"
description: "Azure Active Directory B2B işbirliği için başvuru eşleme talepleri"
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
ms.date: 05/24/2017
ms.author: sasubram
ms.openlocfilehash: 60452b27b328453eda729bd839c982b479cb6f1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="office-365-external-sharing-and-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="65db4-103">Office 365 dış paylaşım ve Azure Active Directory B2B işbirliği</span><span class="sxs-lookup"><span data-stu-id="65db4-103">Office 365 external sharing and Azure Active Directory B2B collaboration</span></span>

<span data-ttu-id="65db4-104">Office 365 (OneDrive, SharePoint Online, birleşik grupları, vb.) ve Azure Active Directory (Azure AD) B2B işbirliği olan teknik paylaşımı dış hello aynı şey.</span><span class="sxs-lookup"><span data-stu-id="65db4-104">External sharing in Office 365 (OneDrive, SharePoint Online, Unified Groups, etc.) and Azure Active Directory (Azure AD) B2B collaboration are technically hello same thing.</span></span> <span data-ttu-id="65db4-105">Tüm dış (OneDrive/SharePoint Online dışında) paylaşımı, Office 365 gruplarında konuklar dahil olmak üzere, zaten paylaşmak için hello Azure AD B2B İşbirliği davetini API'lerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="65db4-105">All external sharing (except OneDrive/SharePoint Online), including guests in Office 365 Groups, already uses hello Azure AD B2B collaboration invitation APIs for sharing.</span></span>

<span data-ttu-id="65db4-106">OneDrive/SharePoint Online ayrı davet Yöneticisi sahiptir.</span><span class="sxs-lookup"><span data-stu-id="65db4-106">OneDrive/SharePoint Online has a separate invitation manager.</span></span> <span data-ttu-id="65db4-107">Azure AD desteğini geliştirilen önce dış OneDrive/SharePoint Online'da paylaşım desteği başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="65db4-107">Support for external sharing in OneDrive/SharePoint Online started before Azure AD developed its support.</span></span> <span data-ttu-id="65db4-108">Zaman içerisinde, OneDrive/SharePoint Online dış paylaşım çeşitli özellikler tahakkuk ve hello ürün kullanan kullanıcılar ve milyonlarca-düzeni paylaşımı yerleşik.</span><span class="sxs-lookup"><span data-stu-id="65db4-108">Over time, OneDrive/SharePoint Online external sharing has accrued several features and many millions of users who use hello product's in-built sharing pattern.</span></span> <span data-ttu-id="65db4-109">Ancak, OneDrive/SharePoint Online dış paylaşım nasıl çalıştığını ve Azure AD B2B işbirliği nasıl çalıştığını arasındaki bazı farklar vardır:</span><span class="sxs-lookup"><span data-stu-id="65db4-109">However, there are some subtle differences between how OneDrive/SharePoint Online external sharing works and how Azure AD B2B collaboration works:</span></span>

- <span data-ttu-id="65db4-110">Kullanıcılar kendi davetleri kullanılan sonra OneDrive/SharePoint Online kullanıcıları toohello dizin ekler.</span><span class="sxs-lookup"><span data-stu-id="65db4-110">OneDrive/SharePoint Online adds users toohello directory after users have redeemed their invitations.</span></span> <span data-ttu-id="65db4-111">Bu nedenle, kullanım önce hello kullanıcı Azure AD portalında görmüyorum.</span><span class="sxs-lookup"><span data-stu-id="65db4-111">So, before redemption, you don't see hello user in Azure AD portal.</span></span> <span data-ttu-id="65db4-112">Başka bir siteye hello bir kullanıcı bu arada başvurulmasını ise yeni bir davet oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="65db4-112">If another site invites a user in hello meantime, a new invitation is generated.</span></span> <span data-ttu-id="65db4-113">Azure AD B2B işbirliği kullandığınızda, böylece her yerde göster ancak, kullanıcılar hemen davette eklenir.</span><span class="sxs-lookup"><span data-stu-id="65db4-113">However, when you use Azure AD B2B collaboration, users are added immediately on invitation so that they show up everywhere.</span></span>

- <span data-ttu-id="65db4-114">Merhaba kullanım deneyimi OneDrive/SharePoint Online'da Azure AD B2B işbirliği hello deneyimi farklı arar.</span><span class="sxs-lookup"><span data-stu-id="65db4-114">hello redemption experience in OneDrive/SharePoint Online looks different from hello experience in Azure AD B2B collaboration.</span></span> <span data-ttu-id="65db4-115">Bir kullanıcıya bir davet redeems sonra hello deneyimleri benzer.</span><span class="sxs-lookup"><span data-stu-id="65db4-115">After a user redeems an invitation, hello experiences look alike.</span></span>

- <span data-ttu-id="65db4-116">Azure AD B2B işbirliği davet kullanıcıların OneDrive/SharePoint Online'a iletişim kutuları paylaşımı çekilebilir.</span><span class="sxs-lookup"><span data-stu-id="65db4-116">Azure AD B2B collaboration invited users can be picked from OneDrive/SharePoint Online sharing dialog boxes.</span></span> <span data-ttu-id="65db4-117">OneDrive/SharePoint davet Çevrimiçi kullanıcılar ayrıca kendi davetleri kullanmak sonra Azure AD içinde gösterilir.</span><span class="sxs-lookup"><span data-stu-id="65db4-117">OneDrive/SharePoint Online invited users also show up in Azure AD after they redeem their invitations.</span></span>

- <span data-ttu-id="65db4-118">toomanage dış OneDrive/SharePoint Online ile Azure AD B2B işbirliği ile paylaşımı ayarlama hello OneDrive/SharePoint Online dış çok ayarı paylaşımı**yalnızca dış kullanıcılarla zaten hello dizininde paylaşımına izin ver**.</span><span class="sxs-lookup"><span data-stu-id="65db4-118">toomanage external sharing in OneDrive/SharePoint Online with Azure AD B2B collaboration, set hello OneDrive/SharePoint Online external sharing setting too**Only allow sharing with external users already in hello directory**.</span></span> <span data-ttu-id="65db4-119">Kullanıcıların paylaşılan tooexternally siteleri gidebilir ve yönetici hello dış ortak çekme ekledi.</span><span class="sxs-lookup"><span data-stu-id="65db4-119">Users can go tooexternally shared sites and pick from external collaborators that hello admin has added.</span></span> <span data-ttu-id="65db4-120">Hello Yöneticisi hello dış ortak hello B2B İşbirliği davetini API'leri aracılığıyla ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="65db4-120">hello admin can add hello external collaborators through hello B2B collaboration invitation APIs.</span></span>

![Merhaba OneDrive/SharePoint Online paylaşımı ayarı dış](media/active-directory-b2b-o365-external-user/odsp-sharing-setting.png)

## <a name="next-steps"></a><span data-ttu-id="65db4-122">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="65db4-122">Next steps</span></span>

<span data-ttu-id="65db4-123">Azure AD B2B işbirliği ile ilgili diğer makalelerimize göz atın:</span><span class="sxs-lookup"><span data-stu-id="65db4-123">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="65db4-124">Azure AD B2B işbirliği nedir?</span><span class="sxs-lookup"><span data-stu-id="65db4-124">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="65db4-125">B2B işbirliği kullanıcı özellikleri</span><span class="sxs-lookup"><span data-stu-id="65db4-125">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="65db4-126">B2B işbirliği kullanıcı tooa rolü ekleme</span><span class="sxs-lookup"><span data-stu-id="65db4-126">Adding a B2B collaboration user tooa role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="65db4-127">B2B işbirliği davetleri temsilci seçme</span><span class="sxs-lookup"><span data-stu-id="65db4-127">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="65db4-128">Dinamik gruplar ve B2B işbirliği</span><span class="sxs-lookup"><span data-stu-id="65db4-128">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="65db4-129">B2B işbirliği kodu ve PowerShell örnekleri</span><span class="sxs-lookup"><span data-stu-id="65db4-129">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="65db4-130">SaaS uygulamaları B2B işbirliği için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="65db4-130">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="65db4-131">B2B işbirliği kullanıcı belirteçleri</span><span class="sxs-lookup"><span data-stu-id="65db4-131">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="65db4-132">B2B işbirliği kullanıcı taleplerini eşleme</span><span class="sxs-lookup"><span data-stu-id="65db4-132">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="65db4-133">B2B işbirliği geçerli sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="65db4-133">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
