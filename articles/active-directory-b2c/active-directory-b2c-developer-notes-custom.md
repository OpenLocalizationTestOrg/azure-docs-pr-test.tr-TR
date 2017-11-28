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
ms.openlocfilehash: 979b8a264eb819ee4a208b9171a53a5ffbf062c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="release-notes-for-azure-active-directory-b2c-custom-policy-public-preview"></a><span data-ttu-id="cf0fa-103">Azure Active Directory B2C özel ilke genel Önizleme için sürüm notları</span><span class="sxs-lookup"><span data-stu-id="cf0fa-103">Release notes for Azure Active Directory B2C custom policy public preview</span></span>
<span data-ttu-id="cf0fa-104">Merhaba özel İlkesi özellik kümesini artık genel Önizleme için tüm Azure Active Directory B2C altında değerlendirme için kullanılabilir (Azure AD B2C) müşteriler.</span><span class="sxs-lookup"><span data-stu-id="cf0fa-104">hello custom policy feature set is now available for evaluation under public preview for all Azure Active Directory B2C (Azure AD B2C) customers.</span></span> <span data-ttu-id="cf0fa-105">Bu özellik kümesi hello en karmaşık kimlik çözümleri oluşturma Gelişmiş kimlik geliştiricileri yöneliktir.</span><span class="sxs-lookup"><span data-stu-id="cf0fa-105">This feature set is targeted at advanced identity developers building hello most complex identity solutions.</span></span>  

<span data-ttu-id="cf0fa-106">Günümüzde, bu özellik kümesi geliştiriciler tooconfigure hello kimlik deneyimi Framework XML dosyasını düzenleyerek aracılığıyla doğrudan gerektirir.</span><span class="sxs-lookup"><span data-stu-id="cf0fa-106">Today, this feature set requires developers tooconfigure hello Identity Experience Framework directly via XML file editing.</span></span> <span data-ttu-id="cf0fa-107">Bu yapılandırma, güçlü ve karmaşık yöntemidir.</span><span class="sxs-lookup"><span data-stu-id="cf0fa-107">This method of configuration is powerful and complex.</span></span> <span data-ttu-id="cf0fa-108">Merhaba kullanan kimlik geliştiriciler Gelişmiş kimlik deneyimi Framework tooinvest kılavuzlarına tamamladıktan ve başvuru belgeleri okuma biraz zaman planlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="cf0fa-108">Advanced identity developers using hello Identity Experience Framework should plan tooinvest some time completing walk-throughs and reading reference documents.</span></span> 

## <a name="features-included-in-this-public-preview"></a><span data-ttu-id="cf0fa-109">Bu genel önizlemede bulunan özellikler</span><span class="sxs-lookup"><span data-stu-id="cf0fa-109">Features included in this public preview</span></span>
<span data-ttu-id="cf0fa-110">Hello genel Önizleme'de sunulan hello yeni özelliklerle, geliştiriciler hello aşağıdaki görevleri gerçekleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="cf0fa-110">With hello new features introduced in hello public preview, developers can perform hello following tasks:</span></span><br>

* <span data-ttu-id="cf0fa-111">Özel ilkeler kullanarak yazar ve karşıya yükleme özel kimlik doğrulama kullanıcı Yolculuklar.</span><span class="sxs-lookup"><span data-stu-id="cf0fa-111">Author and upload custom authentication user journeys by using custom policies.</span></span> 
   * <span data-ttu-id="cf0fa-112">Kullanıcı Yolculuklar alışverişleri adım adım talep sağlayıcıları arasında açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="cf0fa-112">Describe user journeys step-by-step as exchanges between claims providers.</span></span> 
   * <span data-ttu-id="cf0fa-113">Koşullu kullanıcı Yolculuklar dallanma tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="cf0fa-113">Define conditional branching in user journeys.</span></span> 
* <span data-ttu-id="cf0fa-114">Özel kimlik doğrulama kullanıcı Yolculuklar REST API etkin Hizmetleri'nde tümleştirin.</span><span class="sxs-lookup"><span data-stu-id="cf0fa-114">Integrate REST API-enabled services in your custom authentication user journeys.</span></span>  
* <span data-ttu-id="cf0fa-115">Openıdconnect standart hello ile uyumlu olan kimlik sağlayıcıları ile Federasyon ekleyin.</span><span class="sxs-lookup"><span data-stu-id="cf0fa-115">Add federation with identity providers that are compliant with hello OpenIDConnect standard.</span></span> <br>
* <span data-ttu-id="cf0fa-116">Federasyon toohello SAML 2.0 protokolü uyması kimlik sağlayıcıları ile ekleyin.</span><span class="sxs-lookup"><span data-stu-id="cf0fa-116">Add federation with identity providers that adhere toohello SAML 2.0 protocol.</span></span> 

## <a name="terms-of-hello-public-preview"></a><span data-ttu-id="cf0fa-117">Merhaba genel Önizleme koşulları</span><span class="sxs-lookup"><span data-stu-id="cf0fa-117">Terms of hello public preview</span></span>

* <span data-ttu-id="cf0fa-118">Toouse hello yeni özellikler yalnızca değerlendirme amacıyla öneririz.</span><span class="sxs-lookup"><span data-stu-id="cf0fa-118">We encourage you toouse hello new features for evaluation purposes only.</span></span><br>
* <span data-ttu-id="cf0fa-119">Yeni özellikler, bir üretim ortamında kullanılması amaçlanmamıştır.</span><span class="sxs-lookup"><span data-stu-id="cf0fa-119">The new features are not intended for use in a production environment.</span></span><br>
* <span data-ttu-id="cf0fa-120">Hizmet düzeyi sözleşmelerine (SLA) toohello yeni özellikleri geçerli değildir.</span><span class="sxs-lookup"><span data-stu-id="cf0fa-120">Service level agreements (SLAs) do not apply toohello new features.</span></span> <br>
* <span data-ttu-id="cf0fa-121">Destek istekleri normal destek kanallarını Dosyalanan.</span><span class="sxs-lookup"><span data-stu-id="cf0fa-121">Support requests can be filed through regular support channels.</span></span> <br>
* <span data-ttu-id="cf0fa-122">Genel kullanılabilirlik taahhüt edilen tarih yoktur.</span><span class="sxs-lookup"><span data-stu-id="cf0fa-122">There is no promised date for general availability.</span></span><br>
* <span data-ttu-id="cf0fa-123">Bizim tedbirli ve herhangi bir nedenle, Microsoft bayrak ve reddetme veya senaryoları ve hello Azure AD B2C ürün kurucu tooserve müşteri kimlik ve erişim yönetimi (CIAM) platformu olarak hello kapsamını aşan kullanıcı Yolculuklar kısıtlama.</span><span class="sxs-lookup"><span data-stu-id="cf0fa-123">At our discretion, and for any reason, Microsoft can flag and reject or restrict scenarios and user journeys that exceed hello scope of hello Azure AD B2C product charter tooserve as a customer identity and access management (CIAM) platform.</span></span>

## <a name="responsibilities-of-custom-policy-feature-set-developers"></a><span data-ttu-id="cf0fa-124">Özel ilke özellik kümesi geliştiricilerin sorumlulukları</span><span class="sxs-lookup"><span data-stu-id="cf0fa-124">Responsibilities of custom policy feature-set developers</span></span>
<span data-ttu-id="cf0fa-125">El ile ilke yapılandırması Azure AD B2C platformu temel düşük düzeyli erişim toohello verir ve benzersiz, tam olarak özelleştirilebilir güven framework hello oluşturulmasında sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="cf0fa-125">Manual policy configuration grants lower-level access toohello underlying platform of Azure AD B2C and results in hello creation of a unique, fully customizable trust framework.</span></span> <span data-ttu-id="cf0fa-126">Olası alternatifler özel kimlik sağlayıcıları, güven ilişkileri dış hizmetler ve adım adım iş akışları ile tümleştirmeleri bunları kullanan geliştiriciler Gelişmiş hello üzerinde büyük taleplerini yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="cf0fa-126">The possible permutations of custom identity providers, trust relationships, integrations with external services, and step-by-step workflows place greater demands on hello advanced developers consuming them.</span></span>

<span data-ttu-id="cf0fa-127">toofully avantajı hello genel Önizlemesi'nden, geliştiricilerin hello özel İlkesi özellik kümesini kullanma yönergeleri izleyerek toohello uygun olan öneririz:</span><span class="sxs-lookup"><span data-stu-id="cf0fa-127">toofully benefit from hello public preview, we suggest that developers consuming hello custom policy feature set adhere toohello following guidelines:</span></span>
* <span data-ttu-id="cf0fa-128">Merhaba kimlik deneyimi altyapısı Hello yapılandırma dilini ve anahtar/parolalar yönetimi konusunda bilgi sahibi olur.</span><span class="sxs-lookup"><span data-stu-id="cf0fa-128">Become familiar with hello configuration language of hello Identity Experience Engine and key/secrets management.</span></span>
* <span data-ttu-id="cf0fa-129">Senaryolar ve özel tümleştirmeler sahipliğini alın.</span><span class="sxs-lookup"><span data-stu-id="cf0fa-129">Take ownership of scenarios and custom integrations.</span></span>
* <span data-ttu-id="cf0fa-130">Sistemli senaryo test gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="cf0fa-130">Perform methodical scenario testing.</span></span>
* <span data-ttu-id="cf0fa-131">Yazılım geliştirme ve en iyi yöntemlerle en az bir geliştirme ve test ortamı ve bir üretim ortamında hazırlama izleyin.</span><span class="sxs-lookup"><span data-stu-id="cf0fa-131">Follow software development and staging best practices with a minimum of one development and testing environment and one production environment.</span></span>
* <span data-ttu-id="cf0fa-132">Merhaba kimlik sağlayıcıları ve Hizmetleri ile tümleştirme yeni gelişmeler hakkında bilgi sahibi olma.</span><span class="sxs-lookup"><span data-stu-id="cf0fa-132">Stay informed about new developments from hello identity providers and services you integrate with.</span></span> <span data-ttu-id="cf0fa-133">Örneğin, gizli ve zamanlanmış ve zamanlanmamış değişiklikleri toohello hizmetinin değişiklikleri takip edin.</span><span class="sxs-lookup"><span data-stu-id="cf0fa-133">For example, keep track of changes in secrets and of scheduled and unscheduled changes toohello service.</span></span>
* <span data-ttu-id="cf0fa-134">Etkin izleme işlevini ayarlama ve üretim ortamlarında hello yeteneğini izleyin.</span><span class="sxs-lookup"><span data-stu-id="cf0fa-134">Set up active monitoring, and monitor hello responsiveness of production environments.</span></span>
* <span data-ttu-id="cf0fa-135">İletişim e-posta adresleri güncel tutun ve esnek toohello Microsoft live site takım e-postaları kalır.</span><span class="sxs-lookup"><span data-stu-id="cf0fa-135">Keep contact email addresses current, and stay responsive toohello Microsoft live-site team emails.</span></span>
* <span data-ttu-id="cf0fa-136">Tavsiye edilir toodo giderek hello durumlarda Microsoft live site ekibi zamanında eyleme.</span><span class="sxs-lookup"><span data-stu-id="cf0fa-136">Take timely action when advised toodo so by hello Microsoft live-site team.</span></span> 


>[!NOTE]
><span data-ttu-id="cf0fa-137">Bu özellikler sonunda daha erişilebilir tooall geliştiriciler yaparak Azure AD yerleşik İlkeleri'nde bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="cf0fa-137">These features might eventually be included in Azure AD built-in policies, making them more accessible tooall developers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cf0fa-138">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="cf0fa-138">Next steps</span></span>
<span data-ttu-id="cf0fa-139">[Özel ilkelerini kullanmaya başlama](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="cf0fa-139">[Get started with custom policies](active-directory-b2c-get-started-custom.md).</span></span>
