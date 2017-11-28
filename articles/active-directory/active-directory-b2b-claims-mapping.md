---
title: "aaaB2B işbirliği kullanıcı talepleri, Azure Active Directory'de eşleme | Microsoft Docs"
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
ms.date: 03/15/2017
ms.author: sasubram
ms.openlocfilehash: 9e26085e91a6004b2f11286ae9c1df133bd47341
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="b2b-collaboration-user-claims-mapping-in-azure-active-directory"></a><span data-ttu-id="b8770-103">Eşleme Azure Active Directory B2B işbirliği kullanıcı talepleri</span><span class="sxs-lookup"><span data-stu-id="b8770-103">B2B collaboration user claims mapping in Azure Active Directory</span></span>

<span data-ttu-id="b8770-104">B2B işbirliği kullanıcılar için hello SAML belirtecinde verilen hello talepler özelleştiriliyor azure Active Directory (Azure AD) destekler.</span><span class="sxs-lookup"><span data-stu-id="b8770-104">Azure Active Directory (Azure AD) supports customizing hello claims issued in hello SAML token for B2B collaboration users.</span></span> <span data-ttu-id="b8770-105">Bir kullanıcı toohello uygulama doğruladığında, Azure AD benzersiz olarak tanımlayan hello kullanıcı hakkında bilgileri (veya talep) içeren bir SAML belirteci toohello uygulaması verir.</span><span class="sxs-lookup"><span data-stu-id="b8770-105">When a user authenticates toohello application, Azure AD issues a SAML token toohello app that contains information (or claims) about hello user that uniquely identifies them.</span></span> <span data-ttu-id="b8770-106">Varsayılan olarak, bu hello kullanıcının kullanıcı adı, e-posta adresi, ad ve Soyadı içerir.</span><span class="sxs-lookup"><span data-stu-id="b8770-106">By default, this includes hello user's user name, email address, first name, and last name.</span></span> <span data-ttu-id="b8770-107">Görüntüleyin ya da hello SAML belirteci toohello uygulama hello öznitelikler sekmesi altında gönderilen hello talep düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="b8770-107">You can view or edit hello claims sent in hello SAML token toohello application under hello Attributes tab.</span></span>

<span data-ttu-id="b8770-108">Merhaba SAML belirtecinde verilen tooedit hello talepler neden gerekebilecek iki olası nedeni vardır.</span><span class="sxs-lookup"><span data-stu-id="b8770-108">There are two possible reasons why you might need tooedit hello claims issued in hello SAML token.</span></span>

1. <span data-ttu-id="b8770-109">farklı bir talep URI'ler ayarlayın veya talep değerleri toorequire Hello uygulaması yazıldı</span><span class="sxs-lookup"><span data-stu-id="b8770-109">hello application has been written toorequire a different set of claim URIs or claim values</span></span>

2. <span data-ttu-id="b8770-110">Uygulamanız Azure Active Directory'de depolanan hello kullanıcı asıl adı dışında bir şey hello NameIdentifier talep toobe gerektirir.</span><span class="sxs-lookup"><span data-stu-id="b8770-110">Your application requires hello NameIdentifier claim toobe something other than hello user principal name stored in Azure Active Directory.</span></span>

  ![SAML belirteci görünüm talepleri](media/active-directory-b2b-claims-mapping/view-claims-in-saml-token.png)

<span data-ttu-id="b8770-112">Bu makalede talep özelleştirme nasıl tooadd ve düzenleme talepleri hakkında daha fazla bilgi için kullanıma [hello Azure Active Directory'de önceden tümleştirilen uygulamalar için SAML belirtecinde verilen talepler özelleştiriliyor](develop/active-directory-saml-claims-customization.md).</span><span class="sxs-lookup"><span data-stu-id="b8770-112">For information on how tooadd and edit claims, check out this article on claims customization, [Customizing claims issued in hello SAML token for pre-integrated apps in Azure Active Directory](develop/active-directory-saml-claims-customization.md).</span></span> <span data-ttu-id="b8770-113">B2B işbirliği için NameID ve UPN arası Kiracı eşleme kullanıcıları, güvenlik nedenleriyle engellenir.</span><span class="sxs-lookup"><span data-stu-id="b8770-113">For B2B collaboration users, mapping NameID and UPN cross-tenant are prevented for security reasons.</span></span>


## <a name="next-steps"></a><span data-ttu-id="b8770-114">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b8770-114">Next steps</span></span>

<span data-ttu-id="b8770-115">Azure AD B2B işbirliği ile ilgili diğer makalelerimize göz atın:</span><span class="sxs-lookup"><span data-stu-id="b8770-115">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="b8770-116">Azure AD B2B işbirliği nedir?</span><span class="sxs-lookup"><span data-stu-id="b8770-116">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="b8770-117">B2B işbirliği kullanıcı özellikleri</span><span class="sxs-lookup"><span data-stu-id="b8770-117">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="b8770-118">B2B işbirliği kullanıcı tooa rolü ekleme</span><span class="sxs-lookup"><span data-stu-id="b8770-118">Adding a B2B collaboration user tooa role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="b8770-119">B2bB işbirliği davetleri temsilci seçme</span><span class="sxs-lookup"><span data-stu-id="b8770-119">Delegate B2bB collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="b8770-120">Dinamik gruplar ve B2B işbirliği</span><span class="sxs-lookup"><span data-stu-id="b8770-120">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="b8770-121">B2B işbirliği kodu ve PowerShell örnekleri</span><span class="sxs-lookup"><span data-stu-id="b8770-121">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="b8770-122">SaaS uygulamaları B2B işbirliği için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b8770-122">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="b8770-123">Office 365 dış paylaşım</span><span class="sxs-lookup"><span data-stu-id="b8770-123">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="b8770-124">B2B işbirliği kullanıcı belirteçleri</span><span class="sxs-lookup"><span data-stu-id="b8770-124">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="b8770-125">B2B işbirliği geçerli sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="b8770-125">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
