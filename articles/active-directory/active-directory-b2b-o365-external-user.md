---
title: "Office 365 dış paylaşım ve Azure Active Directory B2B işbirliği | Microsoft Docs"
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
ms.openlocfilehash: cad0ce8f745f3d6ca14436fd714b08c60de0e459
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="office-365-external-sharing-and-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="b690e-103">Office 365 dış paylaşım ve Azure Active Directory B2B işbirliği</span><span class="sxs-lookup"><span data-stu-id="b690e-103">Office 365 external sharing and Azure Active Directory B2B collaboration</span></span>

<span data-ttu-id="b690e-104">Dış paylaşım Office 365 (OneDrive, SharePoint Online, birleşik grupları, vb.) ve Azure Active Directory (Azure AD) B2B işbirliği teknik olarak aynı şeydir.</span><span class="sxs-lookup"><span data-stu-id="b690e-104">External sharing in Office 365 (OneDrive, SharePoint Online, Unified Groups, etc.) and Azure Active Directory (Azure AD) B2B collaboration are technically the same thing.</span></span> <span data-ttu-id="b690e-105">Tüm dış (OneDrive/SharePoint Online dışında) paylaşımı, Office 365 gruplarında konuklar dahil olmak üzere, paylaşım için Azure AD B2B İşbirliği davetini API'leri zaten kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="b690e-105">All external sharing (except OneDrive/SharePoint Online), including guests in Office 365 Groups, already uses the Azure AD B2B collaboration invitation APIs for sharing.</span></span>

<span data-ttu-id="b690e-106">OneDrive/SharePoint Online ayrı davet Yöneticisi sahiptir.</span><span class="sxs-lookup"><span data-stu-id="b690e-106">OneDrive/SharePoint Online has a separate invitation manager.</span></span> <span data-ttu-id="b690e-107">Azure AD desteğini geliştirilen önce dış OneDrive/SharePoint Online'da paylaşım desteği başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="b690e-107">Support for external sharing in OneDrive/SharePoint Online started before Azure AD developed its support.</span></span> <span data-ttu-id="b690e-108">Zaman içerisinde, OneDrive/SharePoint Online dış paylaşım çeşitli özellikler tahakkuk ve ürün kullanan kullanıcılar ve milyonlarca-düzeni paylaşımı yerleşik.</span><span class="sxs-lookup"><span data-stu-id="b690e-108">Over time, OneDrive/SharePoint Online external sharing has accrued several features and many millions of users who use the product's in-built sharing pattern.</span></span> <span data-ttu-id="b690e-109">Ancak, OneDrive/SharePoint Online dış paylaşım nasıl çalıştığını ve Azure AD B2B işbirliği nasıl çalıştığını arasındaki bazı farklar vardır:</span><span class="sxs-lookup"><span data-stu-id="b690e-109">However, there are some subtle differences between how OneDrive/SharePoint Online external sharing works and how Azure AD B2B collaboration works:</span></span>

- <span data-ttu-id="b690e-110">Kullanıcılar kendi davetleri kullanılan sonra OneDrive/SharePoint Online dizine kullanıcılar ekler.</span><span class="sxs-lookup"><span data-stu-id="b690e-110">OneDrive/SharePoint Online adds users to the directory after users have redeemed their invitations.</span></span> <span data-ttu-id="b690e-111">Bu nedenle, kullanım önce kullanıcının Azure AD portalında görmüyorum.</span><span class="sxs-lookup"><span data-stu-id="b690e-111">So, before redemption, you don't see the user in Azure AD portal.</span></span> <span data-ttu-id="b690e-112">Bir kullanıcı bu arada başka bir siteye başvurulmasını ise yeni bir davet oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="b690e-112">If another site invites a user in the meantime, a new invitation is generated.</span></span> <span data-ttu-id="b690e-113">Azure AD B2B işbirliği kullandığınızda, böylece her yerde göster ancak, kullanıcılar hemen davette eklenir.</span><span class="sxs-lookup"><span data-stu-id="b690e-113">However, when you use Azure AD B2B collaboration, users are added immediately on invitation so that they show up everywhere.</span></span>

- <span data-ttu-id="b690e-114">OneDrive/SharePoint Online'daki kullanım deneyimi Azure AD B2B işbirliği deneyimi farklı arar.</span><span class="sxs-lookup"><span data-stu-id="b690e-114">The redemption experience in OneDrive/SharePoint Online looks different from the experience in Azure AD B2B collaboration.</span></span> <span data-ttu-id="b690e-115">Bir kullanıcıya bir davet redeems sonra deneyimleri benzer.</span><span class="sxs-lookup"><span data-stu-id="b690e-115">After a user redeems an invitation, the experiences look alike.</span></span>

- <span data-ttu-id="b690e-116">Azure AD B2B işbirliği davet kullanıcıların OneDrive/SharePoint Online'a iletişim kutuları paylaşımı çekilebilir.</span><span class="sxs-lookup"><span data-stu-id="b690e-116">Azure AD B2B collaboration invited users can be picked from OneDrive/SharePoint Online sharing dialog boxes.</span></span> <span data-ttu-id="b690e-117">OneDrive/SharePoint davet Çevrimiçi kullanıcılar ayrıca kendi davetleri kullanmak sonra Azure AD içinde gösterilir.</span><span class="sxs-lookup"><span data-stu-id="b690e-117">OneDrive/SharePoint Online invited users also show up in Azure AD after they redeem their invitations.</span></span>

- <span data-ttu-id="b690e-118">Dış OneDrive/SharePoint Online ile Azure AD B2B işbirliği paylaşım yönetmek için OneDrive/SharePoint Online dış ayarına paylaşımı ayarlayın **yalnızca dış kullanıcılarla zaten dizinde paylaşımına izin ver**.</span><span class="sxs-lookup"><span data-stu-id="b690e-118">To manage external sharing in OneDrive/SharePoint Online with Azure AD B2B collaboration, set the OneDrive/SharePoint Online external sharing setting to **Only allow sharing with external users already in the directory**.</span></span> <span data-ttu-id="b690e-119">Kullanıcılar, harici olarak paylaşılan sitelere gidin ve yönetici ekledi dış ortak çalışanlarla seçin.</span><span class="sxs-lookup"><span data-stu-id="b690e-119">Users can go to externally shared sites and pick from external collaborators that the admin has added.</span></span> <span data-ttu-id="b690e-120">B2B İşbirliği davetini API'leri aracılığıyla dış ortak yönetici ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b690e-120">The admin can add the external collaborators through the B2B collaboration invitation APIs.</span></span>

![OneDrive/SharePoint Online paylaşımı ayarı dış](media/active-directory-b2b-o365-external-user/odsp-sharing-setting.png)

## <a name="next-steps"></a><span data-ttu-id="b690e-122">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b690e-122">Next steps</span></span>

<span data-ttu-id="b690e-123">Azure AD B2B işbirliği ile ilgili diğer makalelerimize göz atın:</span><span class="sxs-lookup"><span data-stu-id="b690e-123">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="b690e-124">Azure AD B2B işbirliği nedir?</span><span class="sxs-lookup"><span data-stu-id="b690e-124">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="b690e-125">B2B işbirliği kullanıcı özellikleri</span><span class="sxs-lookup"><span data-stu-id="b690e-125">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="b690e-126">Bir role B2B işbirliği kullanıcı ekleme</span><span class="sxs-lookup"><span data-stu-id="b690e-126">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="b690e-127">B2B işbirliği davetleri temsilci seçme</span><span class="sxs-lookup"><span data-stu-id="b690e-127">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="b690e-128">Dinamik gruplar ve B2B işbirliği</span><span class="sxs-lookup"><span data-stu-id="b690e-128">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="b690e-129">B2B işbirliği kodu ve PowerShell örnekleri</span><span class="sxs-lookup"><span data-stu-id="b690e-129">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="b690e-130">SaaS uygulamaları B2B işbirliği için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b690e-130">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="b690e-131">B2B işbirliği kullanıcı belirteçleri</span><span class="sxs-lookup"><span data-stu-id="b690e-131">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="b690e-132">B2B işbirliği kullanıcı taleplerini eşleme</span><span class="sxs-lookup"><span data-stu-id="b690e-132">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="b690e-133">B2B işbirliği geçerli sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="b690e-133">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
