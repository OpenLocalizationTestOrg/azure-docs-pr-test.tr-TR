---
title: 'Lisans: Azure AD SSPR''yi | Microsoft Docs'
description: "Lisans gereksinimlerini Azure AD Self Servis parola sıfırlama"
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 9cecaaac429165346f7082f1965dc8a21063fe7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="licensing-requirements-for-azure-ad-self-service-password-reset"></a><span data-ttu-id="fd5f1-103">Lisans gereksinimleri için Azure AD Self Servis parola sıfırlama</span><span class="sxs-lookup"><span data-stu-id="fd5f1-103">Licensing requirements for Azure AD self-service password reset</span></span>

<span data-ttu-id="fd5f1-104">Azure AD parola sıfırlama toofunction sırada, **kuruluşunuzda atanan en az bir Lisansı olmalıdır**.</span><span class="sxs-lookup"><span data-stu-id="fd5f1-104">In order for Azure AD Password Reset toofunction, you **must have at least one license assigned in your organization**.</span></span> <span data-ttu-id="fd5f1-105">Kullanıcı başına hello parola sıfırlama deneyimi lisans uygulamaz.</span><span class="sxs-lookup"><span data-stu-id="fd5f1-105">We do not enforce per-user licensing on hello password reset experience.</span></span> <span data-ttu-id="fd5f1-106">Microsoft lisans sözleşmenize uyumluluğun toomaintain, premium özellikleri kullanmanız tooassign lisansları tooany kullanıcıların gerekir.</span><span class="sxs-lookup"><span data-stu-id="fd5f1-106">toomaintain compliance with your Microsoft licensing agreement, you need tooassign licenses tooany users that use premium features.</span></span>

* <span data-ttu-id="fd5f1-107">**Yalnızca kullanıcıların bulut** -Office 365 (O365) herhangi bir SKU veya Azure AD temel Ücretli</span><span class="sxs-lookup"><span data-stu-id="fd5f1-107">**Cloud only users** - Office 365 (O365) any paid SKU, or Azure AD Basic</span></span>
* <span data-ttu-id="fd5f1-108">**Bulut** ve/veya **şirket içi kullanıcıların** -Azure AD Premium P1 veya P2, Enterprise Mobility + Security (EMS) veya güvenli üretken Enterprise (Parametreyi)</span><span class="sxs-lookup"><span data-stu-id="fd5f1-108">**Cloud** and/or **on-premises users** - Azure AD Premium P1 or P2, Enterprise Mobility + Security (EMS), or Secure Productive Enterprise (SPE)</span></span>

## <a name="licenses-required-for-password-writeback"></a><span data-ttu-id="fd5f1-109">Parola geri yazma için gerekli lisansları</span><span class="sxs-lookup"><span data-stu-id="fd5f1-109">Licenses required for password writeback</span></span>

<span data-ttu-id="fd5f1-110">toouse parola geri yazma, kiracınızda atanan lisansları aşağıdaki hello birine sahip olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="fd5f1-110">toouse password writeback, you must have one of hello following licenses assigned in your tenant.</span></span>

* <span data-ttu-id="fd5f1-111">Azure AD Premium P1</span><span class="sxs-lookup"><span data-stu-id="fd5f1-111">Azure AD Premium P1</span></span>
* <span data-ttu-id="fd5f1-112">Azure AD Premium P2</span><span class="sxs-lookup"><span data-stu-id="fd5f1-112">Azure AD Premium P2</span></span>
* <span data-ttu-id="fd5f1-113">Enterprise Mobility + Security E3</span><span class="sxs-lookup"><span data-stu-id="fd5f1-113">Enterprise Mobility + Security E3</span></span>
* <span data-ttu-id="fd5f1-114">Enterprise Mobility + Security E5</span><span class="sxs-lookup"><span data-stu-id="fd5f1-114">Enterprise Mobility + Security E5</span></span>
* <span data-ttu-id="fd5f1-115">Secure Productive Enterprise E3</span><span class="sxs-lookup"><span data-stu-id="fd5f1-115">Secure Productive Enterprise E3</span></span>
* <span data-ttu-id="fd5f1-116">Secure Productive Enterprise E5</span><span class="sxs-lookup"><span data-stu-id="fd5f1-116">Secure Productive Enterprise E5</span></span>

> [!NOTE]
> <span data-ttu-id="fd5f1-117">Tek başına Office 365 planları lisans **parola geri yazma desteklemeyen** ve bu işlevselliği toowork planları önceki hello birini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="fd5f1-117">Standalone Office 365 licensing plans **do not support password writeback** and require one of hello preceding plans for this functionality toowork.</span></span>

<span data-ttu-id="fd5f1-118">Maliyetleri dahil olmak üzere ek lisans bilgilerine sayfaları aşağıdaki hello üzerinde bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="fd5f1-118">Additional licensing info including costs can be found on hello following pages</span></span>

* [<span data-ttu-id="fd5f1-119">Azure Active Directory fiyatlandırma site</span><span class="sxs-lookup"><span data-stu-id="fd5f1-119">Azure Active Directory Pricing site</span></span>](https://azure.microsoft.com/pricing/details/active-directory/)
* [<span data-ttu-id="fd5f1-120">Enterprise Mobility + Security</span><span class="sxs-lookup"><span data-stu-id="fd5f1-120">Enterprise Mobility + Security</span></span>](https://www.microsoft.com/cloud-platform/enterprise-mobility-security)
* [<span data-ttu-id="fd5f1-121">Güvenli üretken Enterprise</span><span class="sxs-lookup"><span data-stu-id="fd5f1-121">Secure Productive Enterprise</span></span>](https://www.microsoft.com/secure-productive-enterprise/default.aspx)

## <a name="enable-group-or-user-based-licensing"></a><span data-ttu-id="fd5f1-122">Grup veya kullanıcı tabanlı lisans etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="fd5f1-122">Enable group or user-based licensing</span></span>

<span data-ttu-id="fd5f1-123">Artık Azure AD, Grup tabanlı lisans izin Yöneticiler tooassign lisanslar toplu tooa grubundaki kullanıcılar yerine bir seferde bir atama destekler.</span><span class="sxs-lookup"><span data-stu-id="fd5f1-123">Azure AD now supports group-based licensing allowing administrators tooassign licenses in bulk tooa group of users, rather than assigning them one at a time.</span></span> [<span data-ttu-id="fd5f1-124">Ata, doğrulayın ve lisans sorunları gidermek</span><span class="sxs-lookup"><span data-stu-id="fd5f1-124">Assign, verify, and resolve problems with licenses</span></span>](active-directory-licensing-group-assignment-azure-portal.md#step-1-assign-the-required-licenses)

<span data-ttu-id="fd5f1-125">Bazı Microsoft Hizmetleri tüm konumlarda kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="fd5f1-125">Some Microsoft services are not available in all locations.</span></span> <span data-ttu-id="fd5f1-126">Hello Yöneticisi tooa kullanıcıya bir lisans atanabilir önce hello "Kullanım konumu" özelliği hello kullanıcı belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="fd5f1-126">Before a license can be assigned tooa user, hello administrator must specify hello “Usage location” property on hello user.</span></span> <span data-ttu-id="fd5f1-127">Lisans atama kullanıcı altında yapılabilir > Profil > hello Azure Portalı'ndaki ayarları.</span><span class="sxs-lookup"><span data-stu-id="fd5f1-127">Assignment of licenses can be done under User > Profile > Settings section in hello Azure portal.</span></span> <span data-ttu-id="fd5f1-128">**Grup lisans atamasını kullanırken, belirtilen bir kullanım konumu olmayan tüm kullanıcılar hello dizininin hello konumu devralır.**</span><span class="sxs-lookup"><span data-stu-id="fd5f1-128">**When using group license assignment, any users without a usage location specified inherit hello location of hello directory.**</span></span>

## <a name="next-steps"></a><span data-ttu-id="fd5f1-129">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fd5f1-129">Next steps</span></span>

<span data-ttu-id="fd5f1-130">bağlantılar aşağıdaki hello parola sıfırlama ve Azure AD kullanma ile ilgili ek bilgiler sağlar</span><span class="sxs-lookup"><span data-stu-id="fd5f1-130">hello following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="fd5f1-131">[**Hızlı Başlangıç**](active-directory-passwords-getting-started.md) - Azure AD self servis parola yönetimi ile çalışmaya hazırlanın</span><span class="sxs-lookup"><span data-stu-id="fd5f1-131">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="fd5f1-132">[**Veri** ](active-directory-passwords-data.md) - gereklidir hello verileri anlamak ve nasıl kullanıldığı için parola yönetimi</span><span class="sxs-lookup"><span data-stu-id="fd5f1-132">[**Data**](active-directory-passwords-data.md) - Understand hello data that is required and how it is used for password management</span></span>
* <span data-ttu-id="fd5f1-133">[**Sunum** ](active-directory-passwords-best-practices.md) -planlama ve burada bulunan hello kılavuzu kullanarak SSPR tooyour kullanıcılara dağıtma</span><span class="sxs-lookup"><span data-stu-id="fd5f1-133">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR tooyour users using hello guidance found here</span></span>
* <span data-ttu-id="fd5f1-134">[**Özelleştirme** ](active-directory-passwords-customize.md) -hello görünümüne hello SSPR deneyimi, şirketiniz için özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fd5f1-134">[**Customize**](active-directory-passwords-customize.md) - Customize hello look and feel of hello SSPR experience for your company.</span></span>
* <span data-ttu-id="fd5f1-135">[**Raporlama**](active-directory-passwords-reporting.md) - Kullanıcılarınızın SSPR işlevine erişip erişmediğini, ne zaman ve nerede eriştiğini öğrenin</span><span class="sxs-lookup"><span data-stu-id="fd5f1-135">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="fd5f1-136">[**Teknik derinlemesine** ](active-directory-passwords-how-it-works.md) -hello perdenin toounderstand nasıl çalıştığını gidin</span><span class="sxs-lookup"><span data-stu-id="fd5f1-136">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind hello curtain toounderstand how it works</span></span>
* <span data-ttu-id="fd5f1-137">[**Sık Sorulan Sorular**](active-directory-passwords-faq.md) - Nasıl?</span><span class="sxs-lookup"><span data-stu-id="fd5f1-137">[**Frequently Asked Questions**](active-directory-passwords-faq.md) - How?</span></span> <span data-ttu-id="fd5f1-138">Neden?</span><span class="sxs-lookup"><span data-stu-id="fd5f1-138">Why?</span></span> <span data-ttu-id="fd5f1-139">Ne?</span><span class="sxs-lookup"><span data-stu-id="fd5f1-139">What?</span></span> <span data-ttu-id="fd5f1-140">Nerede?</span><span class="sxs-lookup"><span data-stu-id="fd5f1-140">Where?</span></span> <span data-ttu-id="fd5f1-141">Kim?</span><span class="sxs-lookup"><span data-stu-id="fd5f1-141">Who?</span></span> <span data-ttu-id="fd5f1-142">Ne zaman?</span><span class="sxs-lookup"><span data-stu-id="fd5f1-142">When?</span></span> <span data-ttu-id="fd5f1-143">-Her zaman tooask istediğinizi tooquestions yanıtlar</span><span class="sxs-lookup"><span data-stu-id="fd5f1-143">- Answers tooquestions you always wanted tooask</span></span>
* <span data-ttu-id="fd5f1-144">[**Sorun giderme** ](active-directory-passwords-troubleshoot.md) -nasıl biz SSPR ile bkz tooresolve ortak sorunları öğrenin</span><span class="sxs-lookup"><span data-stu-id="fd5f1-144">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how tooresolve common issues that we see with SSPR</span></span>

