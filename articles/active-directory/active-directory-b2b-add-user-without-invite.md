---
title: "Davetiye olmadan aaaAdd B2B işbirliği kullanıcılar tooAzure Active Directory | Microsoft Docs"
description: "Azure Active Directory B2B işbirliği daveti redeeming olmadan diğer Konuk kullanıcılar tooyour Azure AD eklemek Konuk kullanıcı izin verebilirsiniz."
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
ms.openlocfilehash: 459d99b9f856a35973d1b2cbfabdc23fe40c8f44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-b2b-collaboration-guest-users-without-an-invitation"></a><span data-ttu-id="93add-103">Davetiye olmayan B2B işbirliği Konuk kullanıcılar ekleme</span><span class="sxs-lookup"><span data-stu-id="93add-103">Add B2B collaboration guest users without an invitation</span></span>

<span data-ttu-id="93add-104">Bir iş ortağı temsilcisi, tooadd kullanıcıları davet toobe kullanılan gerek olmadan hello iş ortağı tooyour kuruluştan gibi bir kullanıcı izin verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="93add-104">You can allow a user, such as a partner representative, tooadd users from hello partner tooyour organization without needing invitations toobe redeemed.</span></span> <span data-ttu-id="93add-105">Tüm yapmanız gereken olduğu kullanıcı hello iş ortağı Krlş. için kullanmakta olduğunuz hello dizininde numaralandırması ayrıcalıkları vermek</span><span class="sxs-lookup"><span data-stu-id="93add-105">All you must do is grant that user enumeration privileges in hello directory you're using for hello partner org.</span></span> 

<span data-ttu-id="93add-106">Bunlar ayrıcalıkları ne zaman verin:</span><span class="sxs-lookup"><span data-stu-id="93add-106">Grant these privileges when:</span></span>

1. <span data-ttu-id="93add-107">Merhaba iş ortağı kuruluştan bir kullanıcı bir kullanıcı hello konak kuruluşta (örneğin, WoodGrove) başvurulmasını (örneğin, Sam@litware.com) konuk olarak.</span><span class="sxs-lookup"><span data-stu-id="93add-107">A user in hello host organization (for example, WoodGrove) invites one user from hello partner organization (for example, Sam@litware.com) as Guest.</span></span>
2. <span data-ttu-id="93add-108">Hello Yöneticisi hello konak kuruluşunuzdaki Sam tooidentify izin ve hello iş ortağı kuruluştan (Lıtware) diğer kullanıcı ekleme ilkeleri ayarlar.</span><span class="sxs-lookup"><span data-stu-id="93add-108">hello admin in hello host organization sets up policies that allow Sam tooidentify and add other users from hello partner organization (Litware).</span></span>
3. <span data-ttu-id="93add-109">Artık Sam diğer kullanıcıların Lıtware toohello WoodGrove dizin, grupları veya uygulamalardan kullanılan davetleri toobe gerek kalmadan ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="93add-109">Now Sam can add other users from Litware toohello WoodGrove directory, groups, or applications without needing invitations toobe redeemed.</span></span> <span data-ttu-id="93add-110">SAM Lıtware içinde hello uygun numaralandırma ayrıcalıkları varsa, otomatik olarak gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="93add-110">If Sam has hello appropriate enumeration privileges in Litware, it happens automatically.</span></span>

### <a name="next-steps"></a><span data-ttu-id="93add-111">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="93add-111">Next steps</span></span>

<span data-ttu-id="93add-112">Azure AD B2B işbirliği ile ilgili diğer makalelerimize göz atın:</span><span class="sxs-lookup"><span data-stu-id="93add-112">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="93add-113">Azure AD B2B işbirliği nedir?</span><span class="sxs-lookup"><span data-stu-id="93add-113">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="93add-114">Azure Active Directory yöneticileri B2B işbirliği kullanıcıların nasıl eklenir?</span><span class="sxs-lookup"><span data-stu-id="93add-114">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="93add-115">Bilgi çalışanları B2B işbirliği kullanıcıların nasıl eklenir?</span><span class="sxs-lookup"><span data-stu-id="93add-115">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="93add-116">Merhaba B2B işbirliği davet e-posta Hello öğeleri</span><span class="sxs-lookup"><span data-stu-id="93add-116">hello elements of hello B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="93add-117">B2B işbirliği davet kullanım</span><span class="sxs-lookup"><span data-stu-id="93add-117">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="93add-118">Azure AD B2B işbirliği lisanslama</span><span class="sxs-lookup"><span data-stu-id="93add-118">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="93add-119">Azure Active Directory B2B işbirliği sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="93add-119">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="93add-120">Azure Active Directory B2B işbirliği sık sorulan sorular (SSS)</span><span class="sxs-lookup"><span data-stu-id="93add-120">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="93add-121">Azure Active Directory B2B işbirliği API ve özelleştirme</span><span class="sxs-lookup"><span data-stu-id="93add-121">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="93add-122">B2B işbirliği kullanıcıları için çok faktörlü kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="93add-122">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="93add-123">Azure Active Directory'de Uygulama Yönetimi için Makale Dizini</span><span class="sxs-lookup"><span data-stu-id="93add-123">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)