---
title: "Azure Active Directory B2B işbirliği nedir? | Microsoft Belgeleri"
description: "Azure Active Directory B2B işbirliği Kurumsal uygulamalarınıza seçmeli olarak erişmek için iş ortaklarıyla etkinleştirerek, şirketler arası ilişkilerinizi destekler."
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
ms.openlocfilehash: fbc12a52555b190d43b5e953fd4d19923a25b0ed
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="what-is-azure-ad-b2b-collaboration"></a><span data-ttu-id="118b1-104">Azure AD B2B işbirliği nedir?</span><span class="sxs-lookup"><span data-stu-id="118b1-104">What is Azure AD B2B collaboration?</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/AhwrweCBdsc" frameborder="0" allowfullscreen></iframe>

<span data-ttu-id="118b1-105">Azure AD iş işletmeden işletmeye (B2B) işbirliği özelliklerinden herhangi diğer kuruluştan, küçük veya büyük kullanıcılarla güvenle ve güvenli bir şekilde çalışması için Azure AD kullanan herhangi bir kuruluş etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="118b1-105">Azure AD business-to-business (B2B) collaboration capabilities enable any organization using Azure AD to work safely and securely with users from any other organization, small or large.</span></span> <span data-ttu-id="118b1-106">Bu kuruluşlardan Azure AD ile veya olmadan, hatta bir BT kuruluşu ile veya olmadan olabilir.</span><span class="sxs-lookup"><span data-stu-id="118b1-106">Those organizations can be with Azure AD or without, or even with an IT organization or without.</span></span> 

<span data-ttu-id="118b1-107">Azure AD kullanarak kuruluşlar kendi şirket verileri üzerinde tam denetimi korurken belgeleri, kaynakları ve ortakları, uygulamalara erişim sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="118b1-107">Organizations using Azure AD can provide access to documents, resources, and applications to their partners, while maintaining complete control over their own corporate data.</span></span> <span data-ttu-id="118b1-108">Geliştiriciler, Azure AD-işletmeler kullanabileceğiniz iki kuruluş birlikte daha güvenli bir şekilde Getir uygulamalar yazmak üzere API'ler.</span><span class="sxs-lookup"><span data-stu-id="118b1-108">Developers can use the Azure AD business-to-business APIs to write applications that bring two organizations together in more securely.</span></span> <span data-ttu-id="118b1-109">Ayrıca, son kullanıcıların gitmek oldukça kolaydır.</span><span class="sxs-lookup"><span data-stu-id="118b1-109">Also, it's pretty easy for end users to navigate.</span></span>

<span data-ttu-id="118b1-110">Azure AD B2B işbirliği için çok önemlidir, müşterilerimizin %97 olmamızı istiyordu.</span><span class="sxs-lookup"><span data-stu-id="118b1-110">97% of our customers have told us Azure AD B2B collaboration is very important to them.</span></span>

![Pasta grafik](media/active-directory-b2b-what-is-azure-ad-b2b/97-percent-support.png)

<span data-ttu-id="118b1-112">Erken Nisan 2017 itibariyle zaten Azure AD B2B işbirliği özelliklerini kullanarak yaklaşık 3 milyon kullanıcı vardı.</span><span class="sxs-lookup"><span data-stu-id="118b1-112">As of early April 2017, we had about 3 million users already using Azure AD B2B collaboration capabilities.</span></span> <span data-ttu-id="118b1-113">Ve birden fazla %23 10'dan fazla kullanıcınız Azure AD kuruluşların zaten bu özelliklerini benefiting.</span><span class="sxs-lookup"><span data-stu-id="118b1-113">And more than 23% of Azure AD organizations that have more than 10 users are already benefiting from these capabilities.</span></span>

## <a name="the-key-benefits-of-azure-ad-b2b-collaboration-to-your-organization"></a><span data-ttu-id="118b1-114">Kuruluşunuz için Azure AD B2B işbirliği kilit yararları</span><span class="sxs-lookup"><span data-stu-id="118b1-114">The key benefits of Azure AD B2B collaboration to your organization</span></span>

### <a name="work-with-any-user-from-any-partner"></a><span data-ttu-id="118b1-115">Herhangi bir ortaktan herhangi bir kullanıcı ile çalışma</span><span class="sxs-lookup"><span data-stu-id="118b1-115">Work with any user from any partner</span></span>

* <span data-ttu-id="118b1-116">İş ortakları kendi kimlik bilgilerini kullan</span><span class="sxs-lookup"><span data-stu-id="118b1-116">Partners use their own credentials</span></span>

* <span data-ttu-id="118b1-117">Azure AD kullanmak iş ortakları için gereksinimi yoktur</span><span class="sxs-lookup"><span data-stu-id="118b1-117">No requirement for partners to use Azure AD</span></span>

* <span data-ttu-id="118b1-118">Hiçbir dış dizinleri veya karmaşık Kurulum gerekli</span><span class="sxs-lookup"><span data-stu-id="118b1-118">No external directories or complex set-up required</span></span>

### <a name="simple-and-secure-collaboration"></a><span data-ttu-id="118b1-119">Basit ve güvenli işbirliği</span><span class="sxs-lookup"><span data-stu-id="118b1-119">Simple and secure collaboration</span></span>

* <span data-ttu-id="118b1-120">Gelişmiş, Azure AD destekli Yetkilendirme İlkeleri uygulanırken herhangi bir şirket uygulamasını veya veri erişim sağlamak</span><span class="sxs-lookup"><span data-stu-id="118b1-120">Provide access to any corporate app or data, while applying sophisticated, Azure AD-powered authorization policies</span></span>

* <span data-ttu-id="118b1-121">Kullanıcılar için kolay</span><span class="sxs-lookup"><span data-stu-id="118b1-121">Easy for users</span></span>

* <span data-ttu-id="118b1-122">Uygulamalar ve veriler için kurumsal düzeyde güvenlik</span><span class="sxs-lookup"><span data-stu-id="118b1-122">Enterprise-grade security for apps and data</span></span>

### <a name="no-management-overhead"></a><span data-ttu-id="118b1-123">Yönetim yükü</span><span class="sxs-lookup"><span data-stu-id="118b1-123">No management overhead</span></span>

* <span data-ttu-id="118b1-124">Dış bir hesap veya parola yönetimi</span><span class="sxs-lookup"><span data-stu-id="118b1-124">No external account or password management</span></span>

* <span data-ttu-id="118b1-125">Hiçbir eşitleme veya el ile hesap yaşam döngüsü yönetimi</span><span class="sxs-lookup"><span data-stu-id="118b1-125">No sync or manual account lifecycle management</span></span>

* <span data-ttu-id="118b1-126">Hiçbir dış yönetim yükü</span><span class="sxs-lookup"><span data-stu-id="118b1-126">No external administrative overhead</span></span>

## <a name="you-can-easily-add-b2b-collaboration-users-to-your-organization"></a><span data-ttu-id="118b1-127">B2B işbirliği kullanıcılar kuruluşunuza kolayca ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="118b1-127">You can easily add B2B collaboration users to your organization</span></span>

<span data-ttu-id="118b1-128">Yöneticiler, B2B işbirliği (konuk) kullanıcılar ekleyebilirsiniz [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="118b1-128">Admins can add B2B collaboration (guest) users in the [Azure portal](https://portal.azure.com).</span></span>

![Konuk kullanıcı ekleme](media/active-directory-b2b-what-is-azure-ad-b2b/adding-b2b-users-admin.png)

### <a name="enable-your-collaborators-to-bring-their-own-identity"></a><span data-ttu-id="118b1-130">Kendi kimliğini getirmek, ortak etkinleştir</span><span class="sxs-lookup"><span data-stu-id="118b1-130">Enable your collaborators to bring their own identity</span></span>

<span data-ttu-id="118b1-131">B2B Ortak Çalışanlar kendi seçtikleri kimlik bilgilerinizle oturum açabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="118b1-131">B2B collaborators can sign in with an identity of their choice.</span></span> <span data-ttu-id="118b1-132">Kullanıcının bir Microsoft hesabı veya bir Azure AD hesabı – yoksa, bunlar için sorunsuz bir şekilde teklif kullanım için anda oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="118b1-132">If the user doesn’t have a Microsoft account or an Azure AD account – one is created for them seamlessly at the time for offer redemption.</span></span>

![oturum açma kimlik seçimi](media/active-directory-b2b-what-is-azure-ad-b2b/sign-in-identity-choice.png)

### <a name="delegate-to-application-and-group-owners"></a><span data-ttu-id="118b1-134">Uygulama ve Grup sahipleri için temsilci seçme</span><span class="sxs-lookup"><span data-stu-id="118b1-134">Delegate to application and group owners</span></span> 
<span data-ttu-id="118b1-135">Bir Microsoft uygulaması olup olmadığına bakılmaksızın uygulama ve Grup sahipleri B2B kullanıcılar, ilgilendiğiniz doğrudan herhangi bir uygulama ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="118b1-135">Application and group owners can add B2B users directly to any application that you care about, whether it is a Microsoft application or not.</span></span> <span data-ttu-id="118b1-136">Yöneticiler, yönetici olmayanlar için B2B kullanıcılar ekleme izni devredebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="118b1-136">Admins can delegate permission to add B2B users to non-admins.</span></span> <span data-ttu-id="118b1-137">Olmayan yöneticilere kullanabileceğiniz [Azure AD uygulama erişim Paneli'ne](https://myapps.microsoft.com) B2B işbirliği kullanıcılar uygulamaları veya grupları eklemek için.</span><span class="sxs-lookup"><span data-stu-id="118b1-137">Non-admins can use the [Azure AD Application Access Panel](https://myapps.microsoft.com) to add B2B collaboration users to applications or groups.</span></span>

![erişim paneli](media/active-directory-b2b-what-is-azure-ad-b2b/access-panel.png)

![üye ekleme](media/active-directory-b2b-what-is-azure-ad-b2b/add-member.png)

### <a name="authorization-policies-protect-your-corporate-content"></a><span data-ttu-id="118b1-140">Yetkilendirme İlkeleri, şirket içeriğini koruyun</span><span class="sxs-lookup"><span data-stu-id="118b1-140">Authorization policies protect your corporate content</span></span>

<span data-ttu-id="118b1-141">Koşullu erişim ilkeleri, çok faktörlü kimlik doğrulaması gibi uygulanabilir:</span><span class="sxs-lookup"><span data-stu-id="118b1-141">Conditional access policies, such as multi-factor authentication, can be enforced:</span></span>
- <span data-ttu-id="118b1-142">Kiracı düzeyinde</span><span class="sxs-lookup"><span data-stu-id="118b1-142">At the tenant level</span></span>
- <span data-ttu-id="118b1-143">Uygulama düzeyinde</span><span class="sxs-lookup"><span data-stu-id="118b1-143">At the application level</span></span>
- <span data-ttu-id="118b1-144">Belirli kullanıcıların şirket uygulamaları ve verileri koruma</span><span class="sxs-lookup"><span data-stu-id="118b1-144">For specific users to protect corporate apps and data</span></span>

![üye ekleme](media/active-directory-b2b-what-is-azure-ad-b2b/add-member.png)

### <a name="use-our-apis-and-sample-code-to-easily-build-applications-to-onboard"></a><span data-ttu-id="118b1-146">Bizim API'leri kullanan ve kolayca yerleşik uygulamaları oluşturmak için kod örneği</span><span class="sxs-lookup"><span data-stu-id="118b1-146">Use our APIs and sample code to easily build applications to onboard</span></span>
<span data-ttu-id="118b1-147">Dış ortaklarınız karttaki kuruluşunuzun gereksinimlerine göre özelleştirilmiş yolları duruma getirin.</span><span class="sxs-lookup"><span data-stu-id="118b1-147">Bring your external partners on board in ways customized to your organization’s needs.</span></span>

<span data-ttu-id="118b1-148">Kullanarak [B2B İşbirliği davetini API'leri](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation), Self Servis kaydolma portalları oluşturma dahil olmak üzere onboarding deneyimlerinizi özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="118b1-148">Using the [B2B collaboration invitation APIs](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation), you can customize your onboarding experiences, including creating self-service sign-up portals.</span></span> <span data-ttu-id="118b1-149">Bir Self Servis portalı için örnek kod sağladığımız [github'da](https://github.com/Azure/active-directory-dotnet-graphapi-b2bportal-web).</span><span class="sxs-lookup"><span data-stu-id="118b1-149">We provide sample code for a self-service portal [on Github](https://github.com/Azure/active-directory-dotnet-graphapi-b2bportal-web).</span></span>

![Kayıt portalı](media/active-directory-b2b-what-is-azure-ad-b2b/sign-up-portal.png)

<span data-ttu-id="118b1-151">Azure AD B2B işbirliği ile iş ortağı ilişkileri, son kullanıcıların kolay ve sezgisel Bul şekilde korumak için Azure ad tam güç elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="118b1-151">With Azure AD B2B collaboration, you can get the full power of Azure AD to protect your partner relationships in a way that end users find easy and intuitive.</span></span> <span data-ttu-id="118b1-152">Bu nedenle devam edin, Azure AD B2B kendi dış işbirliği için zaten kullanan kuruluş binlerce katılın!</span><span class="sxs-lookup"><span data-stu-id="118b1-152">So go ahead, join the thousands of organizations that are already using Azure AD B2B for their external collaboration!</span></span>

## <a name="next-steps"></a><span data-ttu-id="118b1-153">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="118b1-153">Next steps</span></span>

* <span data-ttu-id="118b1-154">Yönetici deneyimleri içinde bulunan [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="118b1-154">Administrator experiences are found in the [Azure portal](https://portal.azure.com).</span></span>

* <span data-ttu-id="118b1-155">Bilgi çalışanı deneyimleri kullanılabilir [erişim paneli](https://myapps.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="118b1-155">Information worker experiences are available in the [Access Panel](https://myapps.microsoft.com).</span></span>

* <span data-ttu-id="118b1-156">Ve her zaman olduğu gibi tüm geri bildirim, tartışmalara ve üzerinden öneriler için ürün ekibi bağlamak bizim [Microsoft teknik topluluk](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-B2B/bd-p/AzureAD_B2b).</span><span class="sxs-lookup"><span data-stu-id="118b1-156">And, as always, connect with the product team for any feedback, discussions, and suggestions through our [Microsoft Tech Community](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-B2B/bd-p/AzureAD_B2b).</span></span>

<span data-ttu-id="118b1-157">Azure AD B2B işbirliği ile ilgili diğer makalelerimize göz atın:</span><span class="sxs-lookup"><span data-stu-id="118b1-157">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="118b1-158">Azure Active Directory yöneticileri B2B işbirliği kullanıcıların nasıl eklenir?</span><span class="sxs-lookup"><span data-stu-id="118b1-158">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="118b1-159">Bilgi çalışanları B2B işbirliği kullanıcıların nasıl eklenir?</span><span class="sxs-lookup"><span data-stu-id="118b1-159">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="118b1-160">B2B işbirliği davet e-posta öğeleri</span><span class="sxs-lookup"><span data-stu-id="118b1-160">The elements of the B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="118b1-161">B2B işbirliği davet kullanım</span><span class="sxs-lookup"><span data-stu-id="118b1-161">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="118b1-162">Azure AD B2B işbirliği lisanslama</span><span class="sxs-lookup"><span data-stu-id="118b1-162">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="118b1-163">Azure Active Directory B2B işbirliği sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="118b1-163">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="118b1-164">Azure Active Directory B2B işbirliği sık sorulan sorular (SSS)</span><span class="sxs-lookup"><span data-stu-id="118b1-164">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="118b1-165">Azure Active Directory B2B işbirliği API ve özelleştirme</span><span class="sxs-lookup"><span data-stu-id="118b1-165">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="118b1-166">B2B işbirliği kullanıcıları için çok faktörlü kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="118b1-166">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="118b1-167">B2B işbirliği kullanıcıları davet olmadan ekleme</span><span class="sxs-lookup"><span data-stu-id="118b1-167">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="118b1-168">B2B işbirliği kullanıcı Denetim ve Raporlama</span><span class="sxs-lookup"><span data-stu-id="118b1-168">B2B collaboration user auditing and reporting</span></span>](active-directory-b2b-auditing-and-reporting.md)
* [<span data-ttu-id="118b1-169">Azure Active Directory'de Uygulama Yönetimi için Makale Dizini</span><span class="sxs-lookup"><span data-stu-id="118b1-169">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
