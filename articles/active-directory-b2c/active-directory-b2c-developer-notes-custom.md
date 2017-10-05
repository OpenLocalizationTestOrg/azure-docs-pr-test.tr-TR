---
title: "Azure Active Directory B2C: özel ilkelerini kullanma Geliştirici Notları | Microsoft Docs"
description: "Yapılandırma ve Azure AD B2C ile özel ilkeler koruma geliştiriciler için Notlar"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 05/05/2017
ms.author: joroja
ms.openlocfilehash: a5f222e5b11e05286152a9f1cc55d2c3fc27a9dc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="release-notes-for-azure-active-directory-b2c-custom-policy-public-preview"></a><span data-ttu-id="db305-103">Azure Active Directory B2C özel ilke genel Önizleme için sürüm notları</span><span class="sxs-lookup"><span data-stu-id="db305-103">Release notes for Azure Active Directory B2C custom policy public preview</span></span>
<span data-ttu-id="db305-104">Özel ilke özellik kümesi artık genel Önizleme için tüm Azure Active Directory B2C altında değerlendirme için kullanılabilir (Azure AD B2C) müşteriler.</span><span class="sxs-lookup"><span data-stu-id="db305-104">The custom policy feature set is now available for evaluation under public preview for all Azure Active Directory B2C (Azure AD B2C) customers.</span></span> <span data-ttu-id="db305-105">Bu özellik kümesi, Gelişmiş kimlik geliştiricileri en karmaşık kimlik çözümleri oluşturma yöneliktir.</span><span class="sxs-lookup"><span data-stu-id="db305-105">This feature set is targeted at advanced identity developers building the most complex identity solutions.</span></span>  

<span data-ttu-id="db305-106">Günümüzde, bu özellik kümesi XML dosyasını düzenleyerek aracılığıyla doğrudan kimlik deneyimi Framework yapılandırmak geliştiricilere gerektirir.</span><span class="sxs-lookup"><span data-stu-id="db305-106">Today, this feature set requires developers to configure the Identity Experience Framework directly via XML file editing.</span></span> <span data-ttu-id="db305-107">Bu yapılandırma, güçlü ve karmaşık yöntemidir.</span><span class="sxs-lookup"><span data-stu-id="db305-107">This method of configuration is powerful and complex.</span></span> <span data-ttu-id="db305-108">Gelişmiş kimlik kimlik deneyimi Framework kullanan geliştiriciler kılavuzlarına tamamladıktan ve başvuru belgeleri okuma biraz zaman yatırım planlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="db305-108">Advanced identity developers using the Identity Experience Framework should plan to invest some time completing walk-throughs and reading reference documents.</span></span> 

## <a name="features-included-in-this-public-preview"></a><span data-ttu-id="db305-109">Bu genel önizlemede bulunan özellikler</span><span class="sxs-lookup"><span data-stu-id="db305-109">Features included in this public preview</span></span>
<span data-ttu-id="db305-110">Genel önizlemede sunulan yeni özelliklerle geliştiriciler aşağıdaki görevleri gerçekleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="db305-110">With the new features introduced in the public preview, developers can perform the following tasks:</span></span><br>

* <span data-ttu-id="db305-111">Özel ilkeler kullanarak yazar ve karşıya yükleme özel kimlik doğrulama kullanıcı Yolculuklar.</span><span class="sxs-lookup"><span data-stu-id="db305-111">Author and upload custom authentication user journeys by using custom policies.</span></span> 
   * <span data-ttu-id="db305-112">Kullanıcı Yolculuklar alışverişleri adım adım talep sağlayıcıları arasında açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="db305-112">Describe user journeys step-by-step as exchanges between claims providers.</span></span> 
   * <span data-ttu-id="db305-113">Koşullu kullanıcı Yolculuklar dallanma tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="db305-113">Define conditional branching in user journeys.</span></span> 
* <span data-ttu-id="db305-114">Özel kimlik doğrulama kullanıcı Yolculuklar REST API etkin Hizmetleri'nde tümleştirin.</span><span class="sxs-lookup"><span data-stu-id="db305-114">Integrate REST API-enabled services in your custom authentication user journeys.</span></span>  
* <span data-ttu-id="db305-115">Standart Openıdconnect ile uyumlu olan kimlik sağlayıcıları ile Federasyon ekleyin.</span><span class="sxs-lookup"><span data-stu-id="db305-115">Add federation with identity providers that are compliant with the OpenIDConnect standard.</span></span> <br>
* <span data-ttu-id="db305-116">SAML 2.0 protokolünü kullanan kimlik sağlayıcıları ile Federasyon ekleyin.</span><span class="sxs-lookup"><span data-stu-id="db305-116">Add federation with identity providers that adhere to the SAML 2.0 protocol.</span></span> 

## <a name="terms-of-the-public-preview"></a><span data-ttu-id="db305-117">Genel Önizleme koşulları</span><span class="sxs-lookup"><span data-stu-id="db305-117">Terms of the public preview</span></span>

* <span data-ttu-id="db305-118">Yalnızca değerlendirme amacıyla yeni özellikleri kullanmak için önerilir.</span><span class="sxs-lookup"><span data-stu-id="db305-118">We encourage you to use the new features for evaluation purposes only.</span></span><br>
* <span data-ttu-id="db305-119">Yeni özellikler, bir üretim ortamında kullanılması amaçlanmamıştır.</span><span class="sxs-lookup"><span data-stu-id="db305-119">The new features are not intended for use in a production environment.</span></span><br>
* <span data-ttu-id="db305-120">Hizmet düzeyi sözleşmelerine (SLA) için yeni özellikleri geçerli değildir.</span><span class="sxs-lookup"><span data-stu-id="db305-120">Service level agreements (SLAs) do not apply to the new features.</span></span> <br>
* <span data-ttu-id="db305-121">Destek istekleri normal destek kanallarını Dosyalanan.</span><span class="sxs-lookup"><span data-stu-id="db305-121">Support requests can be filed through regular support channels.</span></span> <br>
* <span data-ttu-id="db305-122">Genel kullanılabilirlik taahhüt edilen tarih yoktur.</span><span class="sxs-lookup"><span data-stu-id="db305-122">There is no promised date for general availability.</span></span><br>
* <span data-ttu-id="db305-123">Bizim tedbirli ve herhangi bir nedenle, Microsoft bayrak ve reddetme veya senaryoları ve bir müşteri kimlik ve erişim yönetimi (CIAM) platformu olarak hizmet vermek için Azure AD B2C ürün kurucu kapsamını aşan kullanıcı Yolculuklar kısıtlama.</span><span class="sxs-lookup"><span data-stu-id="db305-123">At our discretion, and for any reason, Microsoft can flag and reject or restrict scenarios and user journeys that exceed the scope of the Azure AD B2C product charter to serve as a customer identity and access management (CIAM) platform.</span></span>

## <a name="responsibilities-of-custom-policy-feature-set-developers"></a><span data-ttu-id="db305-124">Özel ilke özellik kümesi geliştiricilerin sorumlulukları</span><span class="sxs-lookup"><span data-stu-id="db305-124">Responsibilities of custom policy feature-set developers</span></span>
<span data-ttu-id="db305-125">El ile ilke yapılandırması, Azure AD B2C temel platform düşük düzeyli erişim verir ve benzersiz, tam olarak özelleştirilebilir güven framework oluşturulmasında sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="db305-125">Manual policy configuration grants lower-level access to the underlying platform of Azure AD B2C and results in the creation of a unique, fully customizable trust framework.</span></span> <span data-ttu-id="db305-126">Olası alternatifler özel kimlik sağlayıcıları, güven ilişkileri dış hizmetler ve adım adım iş akışları ile tümleştirmeleri bunları kullanan gelişmiş geliştiriciler üzerinde büyük taleplerini yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="db305-126">The possible permutations of custom identity providers, trust relationships, integrations with external services, and step-by-step workflows place greater demands on the advanced developers consuming them.</span></span>

<span data-ttu-id="db305-127">Genel Önizlemesi'nden tam olarak yararlanmak için özel İlkesi özellik kümesini kullanan geliştiriciler için aşağıdaki yönergelere uyması öneririz:</span><span class="sxs-lookup"><span data-stu-id="db305-127">To fully benefit from the public preview, we suggest that developers consuming the custom policy feature set adhere to the following guidelines:</span></span>
* <span data-ttu-id="db305-128">Anahtar/parolalar yönetimi ve kimlik deneyimi altyapısı yapılandırma dili ile Windows'un öğrenin.</span><span class="sxs-lookup"><span data-stu-id="db305-128">Become familiar with the configuration language of the Identity Experience Engine and key/secrets management.</span></span>
* <span data-ttu-id="db305-129">Senaryolar ve özel tümleştirmeler sahipliğini alın.</span><span class="sxs-lookup"><span data-stu-id="db305-129">Take ownership of scenarios and custom integrations.</span></span>
* <span data-ttu-id="db305-130">Sistemli senaryo test gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="db305-130">Perform methodical scenario testing.</span></span>
* <span data-ttu-id="db305-131">Yazılım geliştirme ve en iyi yöntemlerle en az bir geliştirme ve test ortamı ve bir üretim ortamında hazırlama izleyin.</span><span class="sxs-lookup"><span data-stu-id="db305-131">Follow software development and staging best practices with a minimum of one development and testing environment and one production environment.</span></span>
* <span data-ttu-id="db305-132">Kimlik sağlayıcılar ve Hizmetleri ile tümleştirme yeni gelişmeler hakkında bilgi sahibi olma.</span><span class="sxs-lookup"><span data-stu-id="db305-132">Stay informed about new developments from the identity providers and services you integrate with.</span></span> <span data-ttu-id="db305-133">Örneğin, değişiklikleri gizli ve hizmet zamanlanmış ve zamanlanmamış değişiklikleri takip edin.</span><span class="sxs-lookup"><span data-stu-id="db305-133">For example, keep track of changes in secrets and of scheduled and unscheduled changes to the service.</span></span>
* <span data-ttu-id="db305-134">Etkin izleme işlevini ayarlama ve üretim ortamlarını yanıtlama izleyin.</span><span class="sxs-lookup"><span data-stu-id="db305-134">Set up active monitoring, and monitor the responsiveness of production environments.</span></span>
* <span data-ttu-id="db305-135">İletişim e-posta adresleri güncel tutun ve Microsoft live site takım e-postalar için yanıt verebilir durumda kalır.</span><span class="sxs-lookup"><span data-stu-id="db305-135">Keep contact email addresses current, and stay responsive to the Microsoft live-site team emails.</span></span>
* <span data-ttu-id="db305-136">Microsoft live site ekibi tarafından bunu tavsiye zaman zamanında eylemi gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="db305-136">Take timely action when advised to do so by the Microsoft live-site team.</span></span> 


>[!NOTE]
><span data-ttu-id="db305-137">Bu özellikler sonunda tüm geliştiriciler için daha erişilebilir hale getirme Azure AD yerleşik İlkeleri'nde bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="db305-137">These features might eventually be included in Azure AD built-in policies, making them more accessible to all developers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="db305-138">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="db305-138">Next steps</span></span>
<span data-ttu-id="db305-139">[Özel ilkelerini kullanmaya başlama](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="db305-139">[Get started with custom policies](active-directory-b2c-get-started-custom.md).</span></span>
