---
title: "Azure Active Directory B2B işbirliği aaaSelf hizmet kayıt portalı | Microsoft Docs"
description: "Azure Active Directory B2B işbirliği Kurumsal uygulamalarınıza iş ortakları tooselectively erişim sağlayarak, şirketler arası ilişkilerinizi destekler."
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
ms.openlocfilehash: c78920ecf812f7efc06a8b54b1fff834c32904f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="self-service-portal-for-azure-ad-b2b-collaboration-sign-up"></a><span data-ttu-id="2434f-103">Azure AD B2B işbirliği kayıt için Self Servis portalı</span><span class="sxs-lookup"><span data-stu-id="2434f-103">Self-service portal for Azure AD B2B collaboration sign-up</span></span>

<span data-ttu-id="2434f-104">Müşteriler yapabilir çok bizim BT yöneticisi sunulan hello yerleşik özellikleri ile [Azure portal](https://portal.azure.com) ve bizim [uygulama erişim Paneli'ne](https://myapps.microsoft.com) son kullanıcılar için.</span><span class="sxs-lookup"><span data-stu-id="2434f-104">Customers can do a lot with hello built-in features that are exposed through our IT admin [Azure portal](https://portal.azure.com) and our [Application Access Panel](https://myapps.microsoft.com) for end users.</span></span> <span data-ttu-id="2434f-105">Ancak biz de işletmeler toocustomize hello ekleme iş akışı B2B kullanıcılar toofit için kuruluşun gereksinimlerini gerektiğini fark.</span><span class="sxs-lookup"><span data-stu-id="2434f-105">But we are also aware that businesses need toocustomize hello onboarding workflow for B2B users toofit their organization’s needs.</span></span> <span data-ttu-id="2434f-106">İle yapabileceklerini [API'mize](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation).</span><span class="sxs-lookup"><span data-stu-id="2434f-106">They can do that with [our API](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation).</span></span>

<span data-ttu-id="2434f-107">Müşterilerimizin ile tartışmalara bir ortak yukarıdaki tüm diğer hesapları yükselmeye bakın.</span><span class="sxs-lookup"><span data-stu-id="2434f-107">In discussions with our customers, we see one common need rise up above all others.</span></span> <span data-ttu-id="2434f-108">Kuruluş davet hello hello zaman öncesinde tootheir kaynaklarına erişebilecek tek tek dış ortak olan bilemeyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2434f-108">hello inviting organization may not know ahead of time who hello individual external collaborators are who need access tootheir resources.</span></span> <span data-ttu-id="2434f-109">İş ortağı şirketlerden kullanıcılar çok kendilerini ilkeleri kümesiyle kuruluş denetimleri davet bu hello kaydolmak için bir yol istedikleri.</span><span class="sxs-lookup"><span data-stu-id="2434f-109">They wanted a way for users from partner companies too sign themselves up with a set of policies that hello inviting organization controls.</span></span> <span data-ttu-id="2434f-110">Biz bunu vermedi Github projede yayımlanan şekilde bu senaryo bizim API'leri aracılığıyla mümkündür: [örnek Github proje](https://github.com/Azure/active-directory-dotnet-graphapi-b2bportal-web).</span><span class="sxs-lookup"><span data-stu-id="2434f-110">This scenario is possible through our APIs,  so we published a project on Github that did just that: [sample Github project](https://github.com/Azure/active-directory-dotnet-graphapi-b2bportal-web).</span></span>

<span data-ttu-id="2434f-111">Github Projemizin nasıl kuruluşlar bizim API'leri ve kullanabileceğiniz erişebilecekleri hello uygulamaları belirleyen kuralları ile güvenilir ortakları için bir ilke tabanlı, Self Servis kaydolma yeteneği sağlamak gösterir.</span><span class="sxs-lookup"><span data-stu-id="2434f-111">Our Github project demonstrates how organizations can use our APIs, and provide a policy-based, self-service sign-up capability for their trusted partners, with rules that determine hello apps they can access.</span></span> <span data-ttu-id="2434f-112">İş ortağı kullanıcılar, erişimi tooresources alabilirsiniz, bunları güvenli bir şekilde, yerleşik kuruluş toomanually davet hello gerek kalmadan istedikleri zaman bunları.</span><span class="sxs-lookup"><span data-stu-id="2434f-112">Partner users can get access tooresources when they need them, securely, without requiring hello inviting organization toomanually onboard them.</span></span> <span data-ttu-id="2434f-113">Tercih ettiğiniz bir Azure aboneliğinize hello proje kolayca dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2434f-113">You can easily deploy hello project into an Azure subscription of your choice.</span></span>

## <a name="as-is-code"></a><span data-ttu-id="2434f-114">Olarak-kodu.</span><span class="sxs-lookup"><span data-stu-id="2434f-114">As-is code</span></span>

<span data-ttu-id="2434f-115">Bu kod hello Azure Active Directory B2B davet API örnek toodemonstrate kullanımını kullanılabilir hale getirileceğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="2434f-115">Remember that this code is made available as a sample toodemonstrate usage of hello Azure Active Directory B2B invitation API.</span></span> <span data-ttu-id="2434f-116">Geliştirme ekibiniz veya bir iş ortağı tarafından özelleştirilmelidir ve bir üretim senaryosunda dağıtılmadan önce gözden geçirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="2434f-116">It should be customized by your dev team or a partner, and should be reviewed before being deployed in a production scenario.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2434f-117">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2434f-117">Next steps</span></span>

<span data-ttu-id="2434f-118">Azure AD B2B işbirliği ile ilgili diğer makalelerimize göz atın:</span><span class="sxs-lookup"><span data-stu-id="2434f-118">Browse our other articles on Azure AD B2B collaboration:</span></span>
* [<span data-ttu-id="2434f-119">Azure AD B2B işbirliği nedir?</span><span class="sxs-lookup"><span data-stu-id="2434f-119">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="2434f-120">Azure Active Directory yöneticileri B2B işbirliği kullanıcıların nasıl eklenir?</span><span class="sxs-lookup"><span data-stu-id="2434f-120">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="2434f-121">Bilgi çalışanları B2B işbirliği kullanıcıların nasıl eklenir?</span><span class="sxs-lookup"><span data-stu-id="2434f-121">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="2434f-122">Merhaba B2B işbirliği davet e-posta Hello öğeleri</span><span class="sxs-lookup"><span data-stu-id="2434f-122">hello elements of hello B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="2434f-123">B2B işbirliği davet kullanım</span><span class="sxs-lookup"><span data-stu-id="2434f-123">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="2434f-124">Azure AD B2B işbirliği lisanslama</span><span class="sxs-lookup"><span data-stu-id="2434f-124">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="2434f-125">Azure Active Directory B2B işbirliği sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="2434f-125">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="2434f-126">Azure Active Directory B2B işbirliği sık sorulan sorular (SSS)</span><span class="sxs-lookup"><span data-stu-id="2434f-126">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="2434f-127">B2B işbirliği kullanıcıları için çok faktörlü kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="2434f-127">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="2434f-128">B2B işbirliği kullanıcıları davet olmadan ekleme</span><span class="sxs-lookup"><span data-stu-id="2434f-128">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="2434f-129">Azure Active Directory'de Uygulama Yönetimi için Makale Dizini</span><span class="sxs-lookup"><span data-stu-id="2434f-129">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)