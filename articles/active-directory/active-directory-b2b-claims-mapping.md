---
title: "B2B işbirliği kullanıcı talepleri, Azure Active Directory'de eşleme | Microsoft Docs"
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
ms.openlocfilehash: 5f8559450b24effd40a38879aeae3a8dd03944a3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="b2b-collaboration-user-claims-mapping-in-azure-active-directory"></a><span data-ttu-id="cb856-103">Eşleme Azure Active Directory B2B işbirliği kullanıcı talepleri</span><span class="sxs-lookup"><span data-stu-id="cb856-103">B2B collaboration user claims mapping in Azure Active Directory</span></span>

<span data-ttu-id="cb856-104">B2B işbirliği kullanıcılar için SAML belirtecinde verilen talepler özelleştiriliyor azure Active Directory (Azure AD) destekler.</span><span class="sxs-lookup"><span data-stu-id="cb856-104">Azure Active Directory (Azure AD) supports customizing the claims issued in the SAML token for B2B collaboration users.</span></span> <span data-ttu-id="cb856-105">Kullanıcı uygulamaya doğruladığında, Azure AD benzersiz olarak tanımlayan kullanıcı hakkında bilgileri (veya talep) içeren uygulamaya bir SAML belirteci verir.</span><span class="sxs-lookup"><span data-stu-id="cb856-105">When a user authenticates to the application, Azure AD issues a SAML token to the app that contains information (or claims) about the user that uniquely identifies them.</span></span> <span data-ttu-id="cb856-106">Varsayılan olarak, bu kullanıcının kullanıcı adı, e-posta adresi, ad ve Soyadı içerir.</span><span class="sxs-lookup"><span data-stu-id="cb856-106">By default, this includes the user's user name, email address, first name, and last name.</span></span> <span data-ttu-id="cb856-107">Görüntüleyin veya SAML belirteci öznitelikler sekmesinde altındaki uygulamaya gönderilen talepleri düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="cb856-107">You can view or edit the claims sent in the SAML token to the application under the Attributes tab.</span></span>

<span data-ttu-id="cb856-108">Neden SAML belirtecinde verilen talepler düzenlemek için gerekebilecek iki olası nedeni vardır.</span><span class="sxs-lookup"><span data-stu-id="cb856-108">There are two possible reasons why you might need to edit the claims issued in the SAML token.</span></span>

1. <span data-ttu-id="cb856-109">Uygulama talep URI'ler farklı kümesi gerektiren veya talep değerleri için yazılmış</span><span class="sxs-lookup"><span data-stu-id="cb856-109">The application has been written to require a different set of claim URIs or claim values</span></span>

2. <span data-ttu-id="cb856-110">Uygulamanız Azure Active Directory'de depolanan kullanıcı asıl adı dışında bir şey olması NameIdentifier talep gerektirir.</span><span class="sxs-lookup"><span data-stu-id="cb856-110">Your application requires the NameIdentifier claim to be something other than the user principal name stored in Azure Active Directory.</span></span>

  ![SAML belirteci görünüm talepleri](media/active-directory-b2b-claims-mapping/view-claims-in-saml-token.png)

<span data-ttu-id="cb856-112">Bu makalede talep özelleştirme ekleyin ve talep düzenleme hakkında daha fazla bilgi için kullanıma [Azure Active Directory'de önceden tümleştirilen uygulamalar için SAML belirtecinde verilen talepler özelleştiriliyor](develop/active-directory-saml-claims-customization.md).</span><span class="sxs-lookup"><span data-stu-id="cb856-112">For information on how to add and edit claims, check out this article on claims customization, [Customizing claims issued in the SAML token for pre-integrated apps in Azure Active Directory](develop/active-directory-saml-claims-customization.md).</span></span> <span data-ttu-id="cb856-113">B2B işbirliği için NameID ve UPN arası Kiracı eşleme kullanıcıları, güvenlik nedenleriyle engellenir.</span><span class="sxs-lookup"><span data-stu-id="cb856-113">For B2B collaboration users, mapping NameID and UPN cross-tenant are prevented for security reasons.</span></span>


## <a name="next-steps"></a><span data-ttu-id="cb856-114">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="cb856-114">Next steps</span></span>

<span data-ttu-id="cb856-115">Azure AD B2B işbirliği ile ilgili diğer makalelerimize göz atın:</span><span class="sxs-lookup"><span data-stu-id="cb856-115">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="cb856-116">Azure AD B2B işbirliği nedir?</span><span class="sxs-lookup"><span data-stu-id="cb856-116">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="cb856-117">B2B işbirliği kullanıcı özellikleri</span><span class="sxs-lookup"><span data-stu-id="cb856-117">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="cb856-118">Bir role B2B işbirliği kullanıcı ekleme</span><span class="sxs-lookup"><span data-stu-id="cb856-118">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="cb856-119">B2bB işbirliği davetleri temsilci seçme</span><span class="sxs-lookup"><span data-stu-id="cb856-119">Delegate B2bB collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="cb856-120">Dinamik gruplar ve B2B işbirliği</span><span class="sxs-lookup"><span data-stu-id="cb856-120">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="cb856-121">B2B işbirliği kodu ve PowerShell örnekleri</span><span class="sxs-lookup"><span data-stu-id="cb856-121">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="cb856-122">SaaS uygulamaları B2B işbirliği için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="cb856-122">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="cb856-123">Office 365 dış paylaşım</span><span class="sxs-lookup"><span data-stu-id="cb856-123">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="cb856-124">B2B işbirliği kullanıcı belirteçleri</span><span class="sxs-lookup"><span data-stu-id="cb856-124">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="cb856-125">B2B işbirliği geçerli sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="cb856-125">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
