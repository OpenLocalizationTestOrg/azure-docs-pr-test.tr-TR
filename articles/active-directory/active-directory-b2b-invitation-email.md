---
title: "Azure Active Directory B2B işbirliği davet e-posta öğelerini | Microsoft Docs"
description: "Azure Active Directory B2B işbirliği davet e-posta şablonu"
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
ms.date: 05/23/2017
ms.author: sasubram
ms.openlocfilehash: 458a2cab13b7e83f120e0926a95d454070181dfb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="the-elements-of-the-b2b-collaboration-invitation-email"></a><span data-ttu-id="e9b16-103">B2B işbirliği davet e-posta öğeleri</span><span class="sxs-lookup"><span data-stu-id="e9b16-103">The elements of the B2B collaboration invitation email</span></span>

<span data-ttu-id="e9b16-104">Davet e-postaları karttaki ortaklar B2B işbirliği kullanıcılar olarak Azure AD içinde getirmek için kritik bir bileşen var.</span><span class="sxs-lookup"><span data-stu-id="e9b16-104">Invitation emails are a critical component to bring partners on board as B2B collaboration users in Azure AD.</span></span> <span data-ttu-id="e9b16-105">Alıcının güven artırmak için bunları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e9b16-105">You can use them to increase the recipient's trust.</span></span> <span data-ttu-id="e9b16-106">yasallığı ekleyebilir ve alıcı emin olmak için e-posta, sosyal kanıt hissi seçme ile rahat **Get Started** daveti kabul düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e9b16-106">you can add legitimacy and social proof to the email, to make sure the recipient feels comfortable with selecting the **Get Started** button to accept the invitation.</span></span> <span data-ttu-id="e9b16-107">Bu güven dir paylaşım uyuşmazlık azaltmak bir anahtar anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="e9b16-107">This trust is a key means to reduce sharing friction.</span></span> <span data-ttu-id="e9b16-108">Ve ayrıca görünümlü e-posta yapmak istediğiniz!</span><span class="sxs-lookup"><span data-stu-id="e9b16-108">And you also want to make the email look great!</span></span>

![Azure AD B2b davet e-postası](media/active-directory-b2b-invitation-email/invitation-email.png)

## <a name="explaining-the-email"></a><span data-ttu-id="e9b16-110">E-posta açıklayan</span><span class="sxs-lookup"><span data-stu-id="e9b16-110">Explaining the email</span></span>
<span data-ttu-id="e9b16-111">En iyi şekilde nasıl yeteneklerini kullanmak için bilmesi e-postanın birkaç öğeler bakalım.</span><span class="sxs-lookup"><span data-stu-id="e9b16-111">Let's look at a few elements of the email so you know how best to use their capabilities.</span></span>

### <a name="subject"></a><span data-ttu-id="e9b16-112">Konu</span><span class="sxs-lookup"><span data-stu-id="e9b16-112">Subject</span></span>
<span data-ttu-id="e9b16-113">E-postanın konu şu deseni izler: davet ettiğiniz &lt;tenantname&gt; kuruluş</span><span class="sxs-lookup"><span data-stu-id="e9b16-113">The subject of the email follows the following pattern: You're invited to the &lt;tenantname&gt; organization</span></span>

### <a name="from-address"></a><span data-ttu-id="e9b16-114">Adresinden</span><span class="sxs-lookup"><span data-stu-id="e9b16-114">From address</span></span>
<span data-ttu-id="e9b16-115">Başlangıç adresi için bir LinkedIn desen kullanırız.</span><span class="sxs-lookup"><span data-stu-id="e9b16-115">We use a LinkedIn-like pattern for the From address.</span></span>  <span data-ttu-id="e9b16-116">Davet eden olan temizleyin ve hangi şirket ve ayrıca bir Microsoft e-posta geliyor açıklamak e-posta adresi gerekir.</span><span class="sxs-lookup"><span data-stu-id="e9b16-116">You should be clear who the inviter is and from which company, and also clarify that the email is coming from a Microsoft email address.</span></span> <span data-ttu-id="e9b16-117">Biçim: &lt;davet eden görünen adını&gt; gelen &lt;tenantname&gt; (aracılığıyla Microsoft) <invites@microsoft.com&gt;</span><span class="sxs-lookup"><span data-stu-id="e9b16-117">The format is: &lt;Display name of inviter&gt; from &lt;tenantname&gt; (via Microsoft) <invites@microsoft.com&gt;</span></span>

### <a name="reply-to"></a><span data-ttu-id="e9b16-118">Yanıtla</span><span class="sxs-lookup"><span data-stu-id="e9b16-118">Reply To</span></span>
<span data-ttu-id="e9b16-119">E-posta yanıtlama geri davet eden bir e-posta gönderir Yanıtla e-posta davet eden'ın e-posta için kullanılabilir olduğunda ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="e9b16-119">The reply-to email is set to the inviter's email when available, so that replying to the email sends an email back to the inviter.</span></span>

### <a name="branding"></a><span data-ttu-id="e9b16-120">Markalama</span><span class="sxs-lookup"><span data-stu-id="e9b16-120">Branding</span></span>
<span data-ttu-id="e9b16-121">Kiracı kullanımınız gelen davet e-postaları, marka şirket kiracınız için ayarladığınız.</span><span class="sxs-lookup"><span data-stu-id="e9b16-121">The invitation emails from your tenant use the company branding that you may have set up for your tenant.</span></span> <span data-ttu-id="e9b16-122">Bu özellikten yararlanabilir istiyorsanız [burada](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal) nasıl yapılandırılacağı hakkında bilgi.</span><span class="sxs-lookup"><span data-stu-id="e9b16-122">If you want to take advantage of this capability, [here](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal) are the details on how to configure it.</span></span> <span data-ttu-id="e9b16-123">Başlık logosu e-postasında görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="e9b16-123">The banner logo appears in the email.</span></span> <span data-ttu-id="e9b16-124">Görüntü boyutu izleyin ve kalite yönergeleri [burada](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal) en iyi sonuçlar için.</span><span class="sxs-lookup"><span data-stu-id="e9b16-124">Follow the image size and quality instructions [here](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal) for best results.</span></span> <span data-ttu-id="e9b16-125">Ayrıca, şirket adı da eylem çağrısında görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="e9b16-125">In addition, the company name also shows up in the call to action.</span></span>

### <a name="call-to-action"></a><span data-ttu-id="e9b16-126">Arama eylemi için</span><span class="sxs-lookup"><span data-stu-id="e9b16-126">Call to action</span></span>
<span data-ttu-id="e9b16-127">Eylem çağrısı iki bölümden oluşur: alıcı posta neden aldı ve ne alıcı ne yapmanız isteniyor açıklayan.</span><span class="sxs-lookup"><span data-stu-id="e9b16-127">The call to action consists of two parts: explaining why the recipient has received the mail and what the recipient is being asked to do about it.</span></span>
- <span data-ttu-id="e9b16-128">"Neden" bölümünde şu biçimi kullanarak çözülebilir: uygulamalarında erişmeye davet &lt;tenantname&gt; kuruluş</span><span class="sxs-lookup"><span data-stu-id="e9b16-128">The "why" section can be addressed using the following pattern: You've been invited to access applications in the &lt;tenantname&gt; organization</span></span>

- <span data-ttu-id="e9b16-129">Ve "ne, yapmanız isteniyor" bölümü varlığını tarafından gösterilen **Get Started** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e9b16-129">And the "what you're being asked to do" section is indicated by the presence of the **Get Started** button.</span></span> <span data-ttu-id="e9b16-130">Alıcı davetleri gerek kalmadan eklendiğinde bu düğme göstermez.</span><span class="sxs-lookup"><span data-stu-id="e9b16-130">When the recipient has been added without the need for invitations, this button doesn't show up.</span></span>

### <a name="inviters-information"></a><span data-ttu-id="e9b16-131">Davet eden'ın bilgi</span><span class="sxs-lookup"><span data-stu-id="e9b16-131">Inviter's information</span></span>
<span data-ttu-id="e9b16-132">Davet eden'ın görünen adı e-postasında dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="e9b16-132">The inviter's display name is included in the email.</span></span> <span data-ttu-id="e9b16-133">Ve Azure AD hesabınız için bir profil resmi oluşturmadıysanız, ayrıca, davet e-posta o resmi de içerir.</span><span class="sxs-lookup"><span data-stu-id="e9b16-133">And in addition, if you've set up a profile picture for your Azure AD account, the inviting email will include that picture as well.</span></span> <span data-ttu-id="e9b16-134">Her ikisi de, e-posta alıcının güveni artırmak için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="e9b16-134">Both are intended to increase your recipient's confidence in the email.</span></span>

<span data-ttu-id="e9b16-135">Profil resminizi henüz ayarlamadıysanız, resmi yerine davet eden'ın baş harflerini içeren bir simge gösterilir:</span><span class="sxs-lookup"><span data-stu-id="e9b16-135">If you haven't yet set up your profile picture, an icon with the inviter's initials in place of the picture is shown:</span></span>

  ![Davet eden'ın baş harflerini görüntüleme](media/active-directory-b2b-invitation-email/inviters-initials.png)

### <a name="body"></a><span data-ttu-id="e9b16-137">Gövde</span><span class="sxs-lookup"><span data-stu-id="e9b16-137">Body</span></span>
<span data-ttu-id="e9b16-138">Davet eden oluşturur veya API davet yoluyla geçirilen ileti gövdesi içerir.</span><span class="sxs-lookup"><span data-stu-id="e9b16-138">The body contains the message that the inviter composes or is passed through the invitation API.</span></span> <span data-ttu-id="e9b16-139">Güvenlik nedenleriyle HTML etiketlerini işlemek için bir metin alanı var.</span><span class="sxs-lookup"><span data-stu-id="e9b16-139">It is a text area, so it does not process HTML tags for security reasons.</span></span>

### <a name="footer-section"></a><span data-ttu-id="e9b16-140">Altbilgi bölümü</span><span class="sxs-lookup"><span data-stu-id="e9b16-140">Footer section</span></span>
<span data-ttu-id="e9b16-141">Altbilgi Microsoft şirketinizin markasını içeren ve e-posta izlenmeyen bir diğer ad tarafından gönderildiğini bilmeniz alıcı olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="e9b16-141">The footer contains the Microsoft company brand and lets the recipient know if the email was sent from an unmonitored alias.</span></span> <span data-ttu-id="e9b16-142">Özel durumlar:</span><span class="sxs-lookup"><span data-stu-id="e9b16-142">Special cases:</span></span>

- <span data-ttu-id="e9b16-143">Davet eden davet kiralama ile bir e-posta adresi yok</span><span class="sxs-lookup"><span data-stu-id="e9b16-143">The inviter doesn't have an email address in the inviting tenancy</span></span>

  ![davet eden resmini davet kiralama ile bir e-posta adresi yok](media/active-directory-b2b-invitation-email/inviter-no-email.png)


- <span data-ttu-id="e9b16-145">Alıcı daveti kullanmak gerekmez</span><span class="sxs-lookup"><span data-stu-id="e9b16-145">The recipient doesn't need to redeem the invitation</span></span>

  ![ne zaman alıcı davet kullanmak gerekmez](media/active-directory-b2b-invitation-email/when-recipient-doesnt-redeem.png)


## <a name="next-steps"></a><span data-ttu-id="e9b16-147">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e9b16-147">Next steps</span></span>

<span data-ttu-id="e9b16-148">Azure AD B2B işbirliği ile ilgili diğer makalelerimize göz atın:</span><span class="sxs-lookup"><span data-stu-id="e9b16-148">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="e9b16-149">Azure AD B2B işbirliği nedir</span><span class="sxs-lookup"><span data-stu-id="e9b16-149">What is Azure AD B2B collaboration</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="e9b16-150">Azure Active Directory yöneticileri B2B işbirliği kullanıcıların nasıl eklenir?</span><span class="sxs-lookup"><span data-stu-id="e9b16-150">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="e9b16-151">Bilgi çalışanları B2B işbirliği kullanıcıların nasıl eklenir?</span><span class="sxs-lookup"><span data-stu-id="e9b16-151">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="e9b16-152">B2B işbirliği davet kullanım</span><span class="sxs-lookup"><span data-stu-id="e9b16-152">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="e9b16-153">Azure AD B2B işbirliği lisanslama</span><span class="sxs-lookup"><span data-stu-id="e9b16-153">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="e9b16-154">Azure Active Directory B2B işbirliği sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="e9b16-154">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="e9b16-155">Azure Active Directory B2B işbirliği sık sorulan sorular (SSS)</span><span class="sxs-lookup"><span data-stu-id="e9b16-155">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="e9b16-156">Azure Active Directory B2B işbirliği API ve özelleştirme</span><span class="sxs-lookup"><span data-stu-id="e9b16-156">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="e9b16-157">B2B işbirliği kullanıcıları için çok faktörlü kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="e9b16-157">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="e9b16-158">B2B işbirliği kullanıcıları davet olmadan ekleme</span><span class="sxs-lookup"><span data-stu-id="e9b16-158">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="e9b16-159">Azure Active Directory'de Uygulama Yönetimi için Makale Dizini</span><span class="sxs-lookup"><span data-stu-id="e9b16-159">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
