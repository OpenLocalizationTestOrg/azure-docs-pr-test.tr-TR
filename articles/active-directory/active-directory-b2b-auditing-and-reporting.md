---
title: "Denetim ve bir Azure Active Directory B2B işbirliği kullanıcı raporlama | Microsoft Docs"
description: "Konuk kullanıcı özelliklerini Azure Active Directory B2B işbirliği yapılandırılabilir"
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
ms.date: 04/12/2017
ms.author: sasubram
ms.openlocfilehash: ba782270f3280e52235bc13148d232284b55762a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="auditing-and-reporting-a-b2b-collaboration-user"></a><span data-ttu-id="39c53-103">Denetim ve B2B işbirliği kullanıcı raporlama</span><span class="sxs-lookup"><span data-stu-id="39c53-103">Auditing and reporting a B2B collaboration user</span></span>
<span data-ttu-id="39c53-104">Konuk kullanıcılar, üye kullanıcılarla denetim özelliklerine benzer sahip.</span><span class="sxs-lookup"><span data-stu-id="39c53-104">With guest users, you have auditing capabilities similar to with member users.</span></span> <span data-ttu-id="39c53-105">Davet edilene Sam Oogle daveti ve kullanım geçmişinin bir örneği burada verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="39c53-105">Here's an example of the invitation and redemption history of invitee Sam Oogle:</span></span>

![Denetim günlüğü](./media/active-directory-b2b-auditing-and-reporting/audit-log.png)

<span data-ttu-id="39c53-107">Ayrıntılı bilgi almak için bu olayların her biri başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="39c53-107">You can dive into each of these events to get the details.</span></span> <span data-ttu-id="39c53-108">Örneğin, kabul ayrıntıları bakalım.</span><span class="sxs-lookup"><span data-stu-id="39c53-108">For example, let's look at the acceptance details.</span></span>

![Etkinlik ayrıntıları](./media/active-directory-b2b-auditing-and-reporting/activity-details.png)

<span data-ttu-id="39c53-110">Ayrıca, Azure AD'den Bu günlükleri dışarı aktarmak ve özelleştirilmiş raporlarla almak için tercih ettiğiniz raporlama aracını kullanın.</span><span class="sxs-lookup"><span data-stu-id="39c53-110">You can also export these logs from Azure AD and use the reporting tool of your choice to get customized reports.</span></span>

### <a name="next-steps"></a><span data-ttu-id="39c53-111">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="39c53-111">Next steps</span></span>

<span data-ttu-id="39c53-112">Azure AD B2B işbirliği ile ilgili diğer makalelerimize göz atın:</span><span class="sxs-lookup"><span data-stu-id="39c53-112">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="39c53-113">Azure AD B2B işbirliği nedir?</span><span class="sxs-lookup"><span data-stu-id="39c53-113">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="39c53-114">B2B işbirliği kullanıcı özellikleri</span><span class="sxs-lookup"><span data-stu-id="39c53-114">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="39c53-115">Bir role B2B işbirliği kullanıcı ekleme</span><span class="sxs-lookup"><span data-stu-id="39c53-115">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="39c53-116">B2bB işbirliği davetleri temsilci seçme</span><span class="sxs-lookup"><span data-stu-id="39c53-116">Delegate B2bB collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="39c53-117">Dinamik gruplar ve B2B işbirliği</span><span class="sxs-lookup"><span data-stu-id="39c53-117">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="39c53-118">B2B işbirliği kodu ve PowerShell örnekleri</span><span class="sxs-lookup"><span data-stu-id="39c53-118">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="39c53-119">SaaS uygulamaları B2B işbirliği için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="39c53-119">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="39c53-120">B2B işbirliği kullanıcı belirteçleri</span><span class="sxs-lookup"><span data-stu-id="39c53-120">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="39c53-121">B2B işbirliği kullanıcı taleplerini eşleme</span><span class="sxs-lookup"><span data-stu-id="39c53-121">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="39c53-122">Office 365 dış paylaşım</span><span class="sxs-lookup"><span data-stu-id="39c53-122">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="39c53-123">B2B işbirliği geçerli sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="39c53-123">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
