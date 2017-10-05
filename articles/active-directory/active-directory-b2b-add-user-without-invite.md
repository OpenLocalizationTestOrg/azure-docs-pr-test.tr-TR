---
title: "B2B işbirliği kullanıcılar davetsiz Azure Active Directory'ye ekleme | Microsoft Docs"
description: "Azure Active Directory B2B işbirliği daveti redeeming olmadan diğer Konuk kullanıcılar için Azure AD eklemek Konuk kullanıcı izin verebilirsiniz."
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
ms.openlocfilehash: 91b9477cdb679851e7d8d2942c06999a05f64e46
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="add-b2b-collaboration-guest-users-without-an-invitation"></a><span data-ttu-id="a7525-103">Davetiye olmayan B2B işbirliği Konuk kullanıcılar ekleme</span><span class="sxs-lookup"><span data-stu-id="a7525-103">Add B2B collaboration guest users without an invitation</span></span>

<span data-ttu-id="a7525-104">Kullanıcılar, kullanılan için davet gerek kalmadan kuruluşunuz için iş ortağı eklemek için bir iş ortağı temsilcisi gibi bir kullanıcı izin verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a7525-104">You can allow a user, such as a partner representative, to add users from the partner to your organization without needing invitations to be redeemed.</span></span> <span data-ttu-id="a7525-105">Yapmanız gereken tek şey bu kullanıcı için iş ortağı Krlş. kullanmakta olduğunuz dizinde numaralandırması ayrıcalıkları vermek</span><span class="sxs-lookup"><span data-stu-id="a7525-105">All you must do is grant that user enumeration privileges in the directory you're using for the partner org.</span></span> 

<span data-ttu-id="a7525-106">Bunlar ayrıcalıkları ne zaman verin:</span><span class="sxs-lookup"><span data-stu-id="a7525-106">Grant these privileges when:</span></span>

1. <span data-ttu-id="a7525-107">İş ortağı kuruluştan bir kullanıcı bir kullanıcı ana bilgisayar kuruluştaki (örneğin, WoodGrove) başvurulmasını (örneğin, Sam@litware.com) konuk olarak.</span><span class="sxs-lookup"><span data-stu-id="a7525-107">A user in the host organization (for example, WoodGrove) invites one user from the partner organization (for example, Sam@litware.com) as Guest.</span></span>
2. <span data-ttu-id="a7525-108">Ana bilgisayar kuruluşunuzdaki yönetim tanımlamak ve iş ortağı kuruluştan (Lıtware) diğer kullanıcıları eklemek Sam izin ilkeleri ayarlar.</span><span class="sxs-lookup"><span data-stu-id="a7525-108">The admin in the host organization sets up policies that allow Sam to identify and add other users from the partner organization (Litware).</span></span>
3. <span data-ttu-id="a7525-109">Artık Sam diğer kullanıcıların Lıtware WoodGrove dizini, grupları veya uygulamalar için kullanılan için davet gerek kalmadan ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a7525-109">Now Sam can add other users from Litware to the WoodGrove directory, groups, or applications without needing invitations to be redeemed.</span></span> <span data-ttu-id="a7525-110">SAM Lıtware içinde uygun numaralandırma ayrıcalıkları varsa, otomatik olarak gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="a7525-110">If Sam has the appropriate enumeration privileges in Litware, it happens automatically.</span></span>

### <a name="next-steps"></a><span data-ttu-id="a7525-111">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a7525-111">Next steps</span></span>

<span data-ttu-id="a7525-112">Azure AD B2B işbirliği ile ilgili diğer makalelerimize göz atın:</span><span class="sxs-lookup"><span data-stu-id="a7525-112">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="a7525-113">Azure AD B2B işbirliği nedir?</span><span class="sxs-lookup"><span data-stu-id="a7525-113">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="a7525-114">Azure Active Directory yöneticileri B2B işbirliği kullanıcıların nasıl eklenir?</span><span class="sxs-lookup"><span data-stu-id="a7525-114">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="a7525-115">Bilgi çalışanları B2B işbirliği kullanıcıların nasıl eklenir?</span><span class="sxs-lookup"><span data-stu-id="a7525-115">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="a7525-116">B2B işbirliği davet e-posta öğeleri</span><span class="sxs-lookup"><span data-stu-id="a7525-116">The elements of the B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="a7525-117">B2B işbirliği davet kullanım</span><span class="sxs-lookup"><span data-stu-id="a7525-117">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="a7525-118">Azure AD B2B işbirliği lisanslama</span><span class="sxs-lookup"><span data-stu-id="a7525-118">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="a7525-119">Azure Active Directory B2B işbirliği sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="a7525-119">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="a7525-120">Azure Active Directory B2B işbirliği sık sorulan sorular (SSS)</span><span class="sxs-lookup"><span data-stu-id="a7525-120">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="a7525-121">Azure Active Directory B2B işbirliği API ve özelleştirme</span><span class="sxs-lookup"><span data-stu-id="a7525-121">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="a7525-122">B2B işbirliği kullanıcıları için çok faktörlü kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="a7525-122">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="a7525-123">Azure Active Directory'de Uygulama Yönetimi için Makale Dizini</span><span class="sxs-lookup"><span data-stu-id="a7525-123">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)