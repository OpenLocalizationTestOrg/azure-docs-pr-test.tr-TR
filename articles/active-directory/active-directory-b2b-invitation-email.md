---
title: "hello Azure Active Directory B2B işbirliği davet e-posta aaaThe öğeleri | Microsoft Docs"
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
ms.openlocfilehash: f4908014d71a63442bbdca2182f54c7a79675a82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="hello-elements-of-hello-b2b-collaboration-invitation-email"></a><span data-ttu-id="35406-103">Merhaba B2B işbirliği davet e-posta Hello öğeleri</span><span class="sxs-lookup"><span data-stu-id="35406-103">hello elements of hello B2B collaboration invitation email</span></span>

<span data-ttu-id="35406-104">Davet e-postaların bir kritik bileşeni toobring karttaki B2B işbirliği kullanıcılar olarak Azure AD içinde ortaklarıdır.</span><span class="sxs-lookup"><span data-stu-id="35406-104">Invitation emails are a critical component toobring partners on board as B2B collaboration users in Azure AD.</span></span> <span data-ttu-id="35406-105">Bunları tooincrease hello alıcının güven kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="35406-105">You can use them tooincrease hello recipient's trust.</span></span> <span data-ttu-id="35406-106">yasallığı ve sosyal kanıtını toohello e-posta ekleyebilirsiniz, toomake emin hello alıcı hissi hello seçme ile rahat **Get Started** düğmesini tooaccept hello davet.</span><span class="sxs-lookup"><span data-stu-id="35406-106">you can add legitimacy and social proof toohello email, toomake sure hello recipient feels comfortable with selecting hello **Get Started** button tooaccept hello invitation.</span></span> <span data-ttu-id="35406-107">Bu güven dir bir anahtar uyuşmazlık paylaşımı tooreduce anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="35406-107">This trust is a key means tooreduce sharing friction.</span></span> <span data-ttu-id="35406-108">Ve ayrıca toomake hello e-posta görünüm harika!</span><span class="sxs-lookup"><span data-stu-id="35406-108">And you also want toomake hello email look great!</span></span>

![Azure AD B2b davet e-postası](media/active-directory-b2b-invitation-email/invitation-email.png)

## <a name="explaining-hello-email"></a><span data-ttu-id="35406-110">Merhaba e-posta açıklayan</span><span class="sxs-lookup"><span data-stu-id="35406-110">Explaining hello email</span></span>
<span data-ttu-id="35406-111">En iyi nasıl toouse yeteneklerini bilmesi hello e-postanın birkaç öğeler bakalım.</span><span class="sxs-lookup"><span data-stu-id="35406-111">Let's look at a few elements of hello email so you know how best toouse their capabilities.</span></span>

### <a name="subject"></a><span data-ttu-id="35406-112">Konu</span><span class="sxs-lookup"><span data-stu-id="35406-112">Subject</span></span>
<span data-ttu-id="35406-113">Merhaba hello e-postanın konu izleyen desen aşağıdaki hello: sizi davet toohello &lt;tenantname&gt; kuruluş</span><span class="sxs-lookup"><span data-stu-id="35406-113">hello subject of hello email follows hello following pattern: You're invited toohello &lt;tenantname&gt; organization</span></span>

### <a name="from-address"></a><span data-ttu-id="35406-114">Adresinden</span><span class="sxs-lookup"><span data-stu-id="35406-114">From address</span></span>
<span data-ttu-id="35406-115">Bir LinkedIn desen adresinden hello için kullanırız.</span><span class="sxs-lookup"><span data-stu-id="35406-115">We use a LinkedIn-like pattern for hello From address.</span></span>  <span data-ttu-id="35406-116">Merhaba davet eden olduğu ve hangi şirket ve ayrıca açıklamak hello e-posta bir Microsoft e-posta adresinden gelen açık olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="35406-116">You should be clear who hello inviter is and from which company, and also clarify that hello email is coming from a Microsoft email address.</span></span> <span data-ttu-id="35406-117">Merhaba biçimi: &lt;davet eden görünen adını&gt; gelen &lt;tenantname&gt; (aracılığıyla Microsoft) <invites@microsoft.com&gt;</span><span class="sxs-lookup"><span data-stu-id="35406-117">hello format is: &lt;Display name of inviter&gt; from &lt;tenantname&gt; (via Microsoft) <invites@microsoft.com&gt;</span></span>

### <a name="reply-to"></a><span data-ttu-id="35406-118">Yanıtla</span><span class="sxs-lookup"><span data-stu-id="35406-118">Reply To</span></span>
<span data-ttu-id="35406-119">Merhaba yanıt-tooemail toohello davet ın eden eposta kullanılabilir olduğunda, bir e-posta geri toohello davet eden toohello e-posta gönderir yanıtlama şekilde ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="35406-119">hello reply-tooemail is set toohello inviter's email when available, so that replying toohello email sends an email back toohello inviter.</span></span>

### <a name="branding"></a><span data-ttu-id="35406-120">Markalama</span><span class="sxs-lookup"><span data-stu-id="35406-120">Branding</span></span>
<span data-ttu-id="35406-121">hello şirket, markası, Kiracı gelen e-postaları kullanmak hello davet kiracınız için ayarladığınız.</span><span class="sxs-lookup"><span data-stu-id="35406-121">hello invitation emails from your tenant use hello company branding that you may have set up for your tenant.</span></span> <span data-ttu-id="35406-122">Bu özellik tootake avantajlarından istiyorsanız [burada](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal) hello ayrıntıları nasıl tooconfigure onu.</span><span class="sxs-lookup"><span data-stu-id="35406-122">If you want tootake advantage of this capability, [here](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal) are hello details on how tooconfigure it.</span></span> <span data-ttu-id="35406-123">Merhaba başlık logosu hello e-postayla görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="35406-123">hello banner logo appears in hello email.</span></span> <span data-ttu-id="35406-124">Merhaba görüntü boyutu izleyin ve kalite yönergeleri [burada](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal) en iyi sonuçlar için.</span><span class="sxs-lookup"><span data-stu-id="35406-124">Follow hello image size and quality instructions [here](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal) for best results.</span></span> <span data-ttu-id="35406-125">Ayrıca, hello şirket adı da hello çağrısı tooaction görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="35406-125">In addition, hello company name also shows up in hello call tooaction.</span></span>

### <a name="call-tooaction"></a><span data-ttu-id="35406-126">Çağrı tooaction</span><span class="sxs-lookup"><span data-stu-id="35406-126">Call tooaction</span></span>
<span data-ttu-id="35406-127">Merhaba çağrısı tooaction iki bölümden oluşur: hello alıcı hello posta neden aldı ve hangi hello alıcı toodo hakkında isteniyor açıklayan.</span><span class="sxs-lookup"><span data-stu-id="35406-127">hello call tooaction consists of two parts: explaining why hello recipient has received hello mail and what hello recipient is being asked toodo about it.</span></span>
- <span data-ttu-id="35406-128">"neden" bölüm düzeni aşağıdaki hello kullanarak çözülebilir hello: hello davet edilen tooaccess uygulamalarda verilmiş &lt;tenantname&gt; kuruluş</span><span class="sxs-lookup"><span data-stu-id="35406-128">hello "why" section can be addressed using hello following pattern: You've been invited tooaccess applications in hello &lt;tenantname&gt; organization</span></span>

- <span data-ttu-id="35406-129">Ve "ne, toodo isteniyor" bölümü hello hello varlığını tarafından gösterilen hello **Get Started** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="35406-129">And hello "what you're being asked toodo" section is indicated by hello presence of hello **Get Started** button.</span></span> <span data-ttu-id="35406-130">Merhaba alıcı davetleri hello gerek kalmadan eklendiğinde bu düğme göstermez.</span><span class="sxs-lookup"><span data-stu-id="35406-130">When hello recipient has been added without hello need for invitations, this button doesn't show up.</span></span>

### <a name="inviters-information"></a><span data-ttu-id="35406-131">Davet eden'ın bilgi</span><span class="sxs-lookup"><span data-stu-id="35406-131">Inviter's information</span></span>
<span data-ttu-id="35406-132">Merhaba davet ın eden görünen adı hello e-postayla dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="35406-132">hello inviter's display name is included in hello email.</span></span> <span data-ttu-id="35406-133">Ve Azure AD hesabınız için bir profil resmi oluşturmadıysanız, ayrıca, e-posta davet hello o resmi de içerir.</span><span class="sxs-lookup"><span data-stu-id="35406-133">And in addition, if you've set up a profile picture for your Azure AD account, hello inviting email will include that picture as well.</span></span> <span data-ttu-id="35406-134">Her iki hedeflenen tooincrease hello e-posta alıcının güveni olan.</span><span class="sxs-lookup"><span data-stu-id="35406-134">Both are intended tooincrease your recipient's confidence in hello email.</span></span>

<span data-ttu-id="35406-135">Profil resminizi henüz ayarlamadıysanız hello resim yerine hello davet ın eden baş harflerini içeren bir simge gösterilir:</span><span class="sxs-lookup"><span data-stu-id="35406-135">If you haven't yet set up your profile picture, an icon with hello inviter's initials in place of hello picture is shown:</span></span>

  ![görüntüleme hello davet eden'ın baş harfleri](media/active-directory-b2b-invitation-email/inviters-initials.png)

### <a name="body"></a><span data-ttu-id="35406-137">Gövde</span><span class="sxs-lookup"><span data-stu-id="35406-137">Body</span></span>
<span data-ttu-id="35406-138">Merhaba gövdesinde selamlama iletisine bu hello davet eden oluşturur veya hello davet API geçirilir.</span><span class="sxs-lookup"><span data-stu-id="35406-138">hello body contains hello message that hello inviter composes or is passed through hello invitation API.</span></span> <span data-ttu-id="35406-139">Güvenlik nedenleriyle HTML etiketlerini işlemek için bir metin alanı var.</span><span class="sxs-lookup"><span data-stu-id="35406-139">It is a text area, so it does not process HTML tags for security reasons.</span></span>

### <a name="footer-section"></a><span data-ttu-id="35406-140">Altbilgi bölümü</span><span class="sxs-lookup"><span data-stu-id="35406-140">Footer section</span></span>
<span data-ttu-id="35406-141">Merhaba altbilgi hello Microsoft şirketinizin markasını içeren ve hello e-posta izlenmeyen bir diğer ad tarafından gönderildiyse bilmeniz hello alıcı olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="35406-141">hello footer contains hello Microsoft company brand and lets hello recipient know if hello email was sent from an unmonitored alias.</span></span> <span data-ttu-id="35406-142">Özel durumlar:</span><span class="sxs-lookup"><span data-stu-id="35406-142">Special cases:</span></span>

- <span data-ttu-id="35406-143">Merhaba davet eden bir e-posta adresi kiralama davet hello sahip değil</span><span class="sxs-lookup"><span data-stu-id="35406-143">hello inviter doesn't have an email address in hello inviting tenancy</span></span>

  ![davet eden resmi bir e-posta adresi kiralama davet hello sahip değil](media/active-directory-b2b-invitation-email/inviter-no-email.png)


- <span data-ttu-id="35406-145">Merhaba alıcı tooredeem hello davet gerek yoktur</span><span class="sxs-lookup"><span data-stu-id="35406-145">hello recipient doesn't need tooredeem hello invitation</span></span>

  ![Alıcı tooredeem davet gerektiğinde değil](media/active-directory-b2b-invitation-email/when-recipient-doesnt-redeem.png)


## <a name="next-steps"></a><span data-ttu-id="35406-147">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="35406-147">Next steps</span></span>

<span data-ttu-id="35406-148">Azure AD B2B işbirliği ile ilgili diğer makalelerimize göz atın:</span><span class="sxs-lookup"><span data-stu-id="35406-148">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="35406-149">Azure AD B2B işbirliği nedir</span><span class="sxs-lookup"><span data-stu-id="35406-149">What is Azure AD B2B collaboration</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="35406-150">Azure Active Directory yöneticileri B2B işbirliği kullanıcıların nasıl eklenir?</span><span class="sxs-lookup"><span data-stu-id="35406-150">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="35406-151">Bilgi çalışanları B2B işbirliği kullanıcıların nasıl eklenir?</span><span class="sxs-lookup"><span data-stu-id="35406-151">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="35406-152">B2B işbirliği davet kullanım</span><span class="sxs-lookup"><span data-stu-id="35406-152">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="35406-153">Azure AD B2B işbirliği lisanslama</span><span class="sxs-lookup"><span data-stu-id="35406-153">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="35406-154">Azure Active Directory B2B işbirliği sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="35406-154">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="35406-155">Azure Active Directory B2B işbirliği sık sorulan sorular (SSS)</span><span class="sxs-lookup"><span data-stu-id="35406-155">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="35406-156">Azure Active Directory B2B işbirliği API ve özelleştirme</span><span class="sxs-lookup"><span data-stu-id="35406-156">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="35406-157">B2B işbirliği kullanıcıları için çok faktörlü kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="35406-157">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="35406-158">B2B işbirliği kullanıcıları davet olmadan ekleme</span><span class="sxs-lookup"><span data-stu-id="35406-158">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="35406-159">Azure Active Directory'de Uygulama Yönetimi için Makale Dizini</span><span class="sxs-lookup"><span data-stu-id="35406-159">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
