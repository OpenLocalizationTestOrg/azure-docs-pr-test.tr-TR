---
title: "Azure Active Directory B2B işbirliği aaaWhat mi? | Microsoft Belgeleri"
description: "Azure Active Directory B2B işbirliği, şirket uygulamalarınızı iş ortakları tooselectively erişim sağlayarak, şirketler arası ilişkilerinizi destekler."
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 1464387b-ee8b-4c7c-94b3-2c5567224c27
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 06/27/2017
ms.author: curtand
ms.custom: aaddev
ms.reviewer: sasubram
ms.openlocfilehash: 359989b66f3d012c306e8748a607662fffacb919
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-ad-b2b-collaboration"></a><span data-ttu-id="0da3d-104">Azure AD B2B işbirliği nedir?</span><span class="sxs-lookup"><span data-stu-id="0da3d-104">What is Azure AD B2B collaboration?</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/AhwrweCBdsc" frameborder="0" allowfullscreen></iframe>

<span data-ttu-id="0da3d-105">Azure AD iş işletmeden işletmeye (B2B) işbirliği özelliklerinden herhangi diğer kuruluştan, küçük veya büyük kullanıcılarla güvenle ve güvenli bir şekilde Azure AD toowork kullanan herhangi bir kuruluş etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="0da3d-105">Azure AD business-to-business (B2B) collaboration capabilities enable any organization using Azure AD toowork safely and securely with users from any other organization, small or large.</span></span> <span data-ttu-id="0da3d-106">Bu kuruluşlardan Azure AD ile veya olmadan, hatta bir BT kuruluşu ile veya olmadan olabilir.</span><span class="sxs-lookup"><span data-stu-id="0da3d-106">Those organizations can be with Azure AD or without, or even with an IT organization or without.</span></span> 

<span data-ttu-id="0da3d-107">Azure AD kullanarak kuruluşlar kendi şirket verileri üzerinde tam denetimi korurken toodocuments, kaynaklar ve uygulamalar tootheir ortakları, erişim sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="0da3d-107">Organizations using Azure AD can provide access toodocuments, resources, and applications tootheir partners, while maintaining complete control over their own corporate data.</span></span> <span data-ttu-id="0da3d-108">Geliştiriciler, iki kuruluş birlikte daha güvenli bir şekilde Getir hello Azure AD iş iş API'leri toowrite uygulamaları kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="0da3d-108">Developers can use hello Azure AD business-to-business APIs toowrite applications that bring two organizations together in more securely.</span></span> <span data-ttu-id="0da3d-109">Ayrıca, son kullanıcıların toonavigate için oldukça kolaydır.</span><span class="sxs-lookup"><span data-stu-id="0da3d-109">Also, it's pretty easy for end users toonavigate.</span></span>

<span data-ttu-id="0da3d-110">Azure AD B2B işbirliği çok önemli toothem olduğundan, müşterilerimizin %97 olmamızı istiyordu.</span><span class="sxs-lookup"><span data-stu-id="0da3d-110">97% of our customers have told us Azure AD B2B collaboration is very important toothem.</span></span>

![Pasta grafik](media/active-directory-b2b-what-is-azure-ad-b2b/97-percent-support.png)

<span data-ttu-id="0da3d-112">Erken Nisan 2017 itibariyle zaten Azure AD B2B işbirliği özelliklerini kullanarak yaklaşık 3 milyon kullanıcı vardı.</span><span class="sxs-lookup"><span data-stu-id="0da3d-112">As of early April 2017, we had about 3 million users already using Azure AD B2B collaboration capabilities.</span></span> <span data-ttu-id="0da3d-113">Ve birden fazla %23 10'dan fazla kullanıcınız Azure AD kuruluşların zaten bu özelliklerini benefiting.</span><span class="sxs-lookup"><span data-stu-id="0da3d-113">And more than 23% of Azure AD organizations that have more than 10 users are already benefiting from these capabilities.</span></span>

## <a name="hello-key-benefits-of-azure-ad-b2b-collaboration-tooyour-organization"></a><span data-ttu-id="0da3d-114">Azure AD B2B işbirliği tooyour kuruluş Hello kilit yararları</span><span class="sxs-lookup"><span data-stu-id="0da3d-114">hello key benefits of Azure AD B2B collaboration tooyour organization</span></span>

### <a name="work-with-any-user-from-any-partner"></a><span data-ttu-id="0da3d-115">Herhangi bir ortaktan herhangi bir kullanıcı ile çalışma</span><span class="sxs-lookup"><span data-stu-id="0da3d-115">Work with any user from any partner</span></span>

* <span data-ttu-id="0da3d-116">İş ortakları kendi kimlik bilgilerini kullan</span><span class="sxs-lookup"><span data-stu-id="0da3d-116">Partners use their own credentials</span></span>

* <span data-ttu-id="0da3d-117">İş ortakları toouse Azure AD için bir gereksinimi</span><span class="sxs-lookup"><span data-stu-id="0da3d-117">No requirement for partners toouse Azure AD</span></span>

* <span data-ttu-id="0da3d-118">Hiçbir dış dizinleri veya karmaşık Kurulum gerekli</span><span class="sxs-lookup"><span data-stu-id="0da3d-118">No external directories or complex set-up required</span></span>

### <a name="simple-and-secure-collaboration"></a><span data-ttu-id="0da3d-119">Basit ve güvenli işbirliği</span><span class="sxs-lookup"><span data-stu-id="0da3d-119">Simple and secure collaboration</span></span>

* <span data-ttu-id="0da3d-120">Gelişmiş, Azure AD destekli Yetkilendirme İlkeleri uygulanırken Access tooany şirket uygulaması veya verileri sağlar</span><span class="sxs-lookup"><span data-stu-id="0da3d-120">Provide access tooany corporate app or data, while applying sophisticated, Azure AD-powered authorization policies</span></span>

* <span data-ttu-id="0da3d-121">Kullanıcılar için kolay</span><span class="sxs-lookup"><span data-stu-id="0da3d-121">Easy for users</span></span>

* <span data-ttu-id="0da3d-122">Uygulamalar ve veriler için kurumsal düzeyde güvenlik</span><span class="sxs-lookup"><span data-stu-id="0da3d-122">Enterprise-grade security for apps and data</span></span>

### <a name="no-management-overhead"></a><span data-ttu-id="0da3d-123">Yönetim yükü</span><span class="sxs-lookup"><span data-stu-id="0da3d-123">No management overhead</span></span>

* <span data-ttu-id="0da3d-124">Dış bir hesap veya parola yönetimi</span><span class="sxs-lookup"><span data-stu-id="0da3d-124">No external account or password management</span></span>

* <span data-ttu-id="0da3d-125">Hiçbir eşitleme veya el ile hesap yaşam döngüsü yönetimi</span><span class="sxs-lookup"><span data-stu-id="0da3d-125">No sync or manual account lifecycle management</span></span>

* <span data-ttu-id="0da3d-126">Hiçbir dış yönetim yükü</span><span class="sxs-lookup"><span data-stu-id="0da3d-126">No external administrative overhead</span></span>

## <a name="you-can-easily-add-b2b-collaboration-users-tooyour-organization"></a><span data-ttu-id="0da3d-127">B2B işbirliği kullanıcılar tooyour kuruluş kolayca ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0da3d-127">You can easily add B2B collaboration users tooyour organization</span></span>

<span data-ttu-id="0da3d-128">Yöneticileri hello B2B işbirliği (konuk) kullanıcılar ekleyebilirsiniz [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0da3d-128">Admins can add B2B collaboration (guest) users in hello [Azure portal](https://portal.azure.com).</span></span>

![Konuk kullanıcı ekleme](media/active-directory-b2b-what-is-azure-ad-b2b/adding-b2b-users-admin.png)

### <a name="enable-your-collaborators-toobring-their-own-identity"></a><span data-ttu-id="0da3d-130">Ortak Çalışanlar toobring kendi kimliğini etkinleştir</span><span class="sxs-lookup"><span data-stu-id="0da3d-130">Enable your collaborators toobring their own identity</span></span>

<span data-ttu-id="0da3d-131">B2B Ortak Çalışanlar kendi seçtikleri kimlik bilgilerinizle oturum açabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0da3d-131">B2B collaborators can sign in with an identity of their choice.</span></span> <span data-ttu-id="0da3d-132">Merhaba kullanıcının bir Microsoft hesabı veya bir Azure AD hesabı – yoksa, bunlar için sorunsuz bir şekilde hello anda teklif kullanım için oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="0da3d-132">If hello user doesn’t have a Microsoft account or an Azure AD account – one is created for them seamlessly at hello time for offer redemption.</span></span>

![oturum açma kimlik seçimi](media/active-directory-b2b-what-is-azure-ad-b2b/sign-in-identity-choice.png)

### <a name="delegate-tooapplication-and-group-owners"></a><span data-ttu-id="0da3d-134">Temsilci tooapplication ve grubu sahipleri</span><span class="sxs-lookup"><span data-stu-id="0da3d-134">Delegate tooapplication and group owners</span></span> 
<span data-ttu-id="0da3d-135">Uygulama ve Grup sahipleri B2B kullanıcılar ekleyebilir, bir Microsoft uygulaması olsun veya olmasın, ilgilendiğiniz doğrudan tooany uygulama.</span><span class="sxs-lookup"><span data-stu-id="0da3d-135">Application and group owners can add B2B users directly tooany application that you care about, whether it is a Microsoft application or not.</span></span> <span data-ttu-id="0da3d-136">Yöneticileri izin tooadd B2B kullanıcılar toonon-yöneticileri atayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0da3d-136">Admins can delegate permission tooadd B2B users toonon-admins.</span></span> <span data-ttu-id="0da3d-137">Olmayan yöneticilere hello kullanabileceğiniz [Azure AD uygulama erişim Paneli'ne](https://myapps.microsoft.com) tooadd B2B işbirliği kullanıcılar tooapplications veya gruplar.</span><span class="sxs-lookup"><span data-stu-id="0da3d-137">Non-admins can use hello [Azure AD Application Access Panel](https://myapps.microsoft.com) tooadd B2B collaboration users tooapplications or groups.</span></span>

![erişim paneli](media/active-directory-b2b-what-is-azure-ad-b2b/access-panel.png)

![üye ekleme](media/active-directory-b2b-what-is-azure-ad-b2b/add-member.png)

### <a name="authorization-policies-protect-your-corporate-content"></a><span data-ttu-id="0da3d-140">Yetkilendirme İlkeleri, şirket içeriğini koruyun</span><span class="sxs-lookup"><span data-stu-id="0da3d-140">Authorization policies protect your corporate content</span></span>

<span data-ttu-id="0da3d-141">Koşullu erişim ilkeleri, çok faktörlü kimlik doğrulaması gibi uygulanabilir:</span><span class="sxs-lookup"><span data-stu-id="0da3d-141">Conditional access policies, such as multi-factor authentication, can be enforced:</span></span>
- <span data-ttu-id="0da3d-142">Merhaba Kiracı düzeyinde</span><span class="sxs-lookup"><span data-stu-id="0da3d-142">At hello tenant level</span></span>
- <span data-ttu-id="0da3d-143">Merhaba uygulama düzeyinde</span><span class="sxs-lookup"><span data-stu-id="0da3d-143">At hello application level</span></span>
- <span data-ttu-id="0da3d-144">Belirli kullanıcıları tooprotect şirket uygulamaları ve verileri için</span><span class="sxs-lookup"><span data-stu-id="0da3d-144">For specific users tooprotect corporate apps and data</span></span>

![üye ekleme](media/active-directory-b2b-what-is-azure-ad-b2b/add-member.png)

### <a name="use-our-apis-and-sample-code-tooeasily-build-applications-tooonboard"></a><span data-ttu-id="0da3d-146">Bizim API'leri kullanan ve örnek kod tooeasily uygulamaları tooonboard derleme</span><span class="sxs-lookup"><span data-stu-id="0da3d-146">Use our APIs and sample code tooeasily build applications tooonboard</span></span>
<span data-ttu-id="0da3d-147">Dış ortaklarınız karttaki yolları özelleştirilmiş tooyour kuruluşunuzun gereksinimlerini duruma getirin.</span><span class="sxs-lookup"><span data-stu-id="0da3d-147">Bring your external partners on board in ways customized tooyour organization’s needs.</span></span>

<span data-ttu-id="0da3d-148">Hello kullanarak [B2B İşbirliği davetini API'leri](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation), Self Servis kaydolma portalları oluşturma dahil olmak üzere onboarding deneyimlerinizi özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0da3d-148">Using hello [B2B collaboration invitation APIs](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation), you can customize your onboarding experiences, including creating self-service sign-up portals.</span></span> <span data-ttu-id="0da3d-149">Bir Self Servis portalı için örnek kod sağladığımız [github'da](https://github.com/Azure/active-directory-dotnet-graphapi-b2bportal-web).</span><span class="sxs-lookup"><span data-stu-id="0da3d-149">We provide sample code for a self-service portal [on Github](https://github.com/Azure/active-directory-dotnet-graphapi-b2bportal-web).</span></span>

![Kayıt portalı](media/active-directory-b2b-what-is-azure-ad-b2b/sign-up-portal.png)

<span data-ttu-id="0da3d-151">Azure AD B2B işbirliği ile Azure AD tooprotect hello gücünü son kullanıcıların kolay ve sezgisel bulabileceğiniz bir şekilde, iş ortağı ilişkileri alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0da3d-151">With Azure AD B2B collaboration, you can get hello full power of Azure AD tooprotect your partner relationships in a way that end users find easy and intuitive.</span></span> <span data-ttu-id="0da3d-152">Bu nedenle, Azure AD B2B kendi dış işbirliği için zaten kullanıyorsanız kuruluşların birleştirme hello binlerce devam!</span><span class="sxs-lookup"><span data-stu-id="0da3d-152">So go ahead, join hello thousands of organizations that are already using Azure AD B2B for their external collaboration!</span></span>

## <a name="next-steps"></a><span data-ttu-id="0da3d-153">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0da3d-153">Next steps</span></span>

* <span data-ttu-id="0da3d-154">Yönetici deneyimleri hello bulunduğunda [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0da3d-154">Administrator experiences are found in hello [Azure portal](https://portal.azure.com).</span></span>

* <span data-ttu-id="0da3d-155">Bilgi çalışanı deneyimleri hello kullanılabilir [erişim paneli](https://myapps.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="0da3d-155">Information worker experiences are available in hello [Access Panel](https://myapps.microsoft.com).</span></span>

* <span data-ttu-id="0da3d-156">Ve her zaman olduğu gibi tüm geri bildirim, tartışmalara ve üzerinden öneriler için hello ürün ekibi bağlamak bizim [Microsoft teknik topluluk](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-B2B/bd-p/AzureAD_B2b).</span><span class="sxs-lookup"><span data-stu-id="0da3d-156">And, as always, connect with hello product team for any feedback, discussions, and suggestions through our [Microsoft Tech Community](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-B2B/bd-p/AzureAD_B2b).</span></span>

<span data-ttu-id="0da3d-157">Azure AD B2B işbirliği ile ilgili diğer makalelerimize göz atın:</span><span class="sxs-lookup"><span data-stu-id="0da3d-157">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="0da3d-158">Azure Active Directory yöneticileri B2B işbirliği kullanıcıların nasıl eklenir?</span><span class="sxs-lookup"><span data-stu-id="0da3d-158">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="0da3d-159">Bilgi çalışanları B2B işbirliği kullanıcıların nasıl eklenir?</span><span class="sxs-lookup"><span data-stu-id="0da3d-159">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="0da3d-160">Merhaba B2B işbirliği davet e-posta Hello öğeleri</span><span class="sxs-lookup"><span data-stu-id="0da3d-160">hello elements of hello B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="0da3d-161">B2B işbirliği davet kullanım</span><span class="sxs-lookup"><span data-stu-id="0da3d-161">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="0da3d-162">Azure AD B2B işbirliği lisanslama</span><span class="sxs-lookup"><span data-stu-id="0da3d-162">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="0da3d-163">Azure Active Directory B2B işbirliği sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="0da3d-163">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="0da3d-164">Azure Active Directory B2B işbirliği sık sorulan sorular (SSS)</span><span class="sxs-lookup"><span data-stu-id="0da3d-164">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="0da3d-165">Azure Active Directory B2B işbirliği API ve özelleştirme</span><span class="sxs-lookup"><span data-stu-id="0da3d-165">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="0da3d-166">B2B işbirliği kullanıcıları için çok faktörlü kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="0da3d-166">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="0da3d-167">B2B işbirliği kullanıcıları davet olmadan ekleme</span><span class="sxs-lookup"><span data-stu-id="0da3d-167">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="0da3d-168">B2B işbirliği kullanıcı Denetim ve Raporlama</span><span class="sxs-lookup"><span data-stu-id="0da3d-168">B2B collaboration user auditing and reporting</span></span>](active-directory-b2b-auditing-and-reporting.md)
* [<span data-ttu-id="0da3d-169">Azure Active Directory'de Uygulama Yönetimi için Makale Dizini</span><span class="sxs-lookup"><span data-stu-id="0da3d-169">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
