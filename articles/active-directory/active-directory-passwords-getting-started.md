---
title: "Hızlı Başlangıç: Azure AD SSPR | Microsoft Docs"
description: "Azure AD self servis parola sıfırlamayı hızlıca dağıtma"
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: bde8799f-0b42-446a-ad95-7ebb374c3bec
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 4fed3a1c690fd6423ee5d3e5baef690d8896fbe9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-azure-ad-self-service-password-reset"></a><span data-ttu-id="07130-103">Hızlı Başlangıç: Azure AD self servis parola sıfırlama</span><span class="sxs-lookup"><span data-stu-id="07130-103">Quickstart: Azure AD self-service password reset</span></span>

> [!IMPORTANT]
> <span data-ttu-id="07130-104">**Oturum açmada sorun yaşadığınız için mi buradasınız?**</span><span class="sxs-lookup"><span data-stu-id="07130-104">**Are you here because you're having problems signing in?**</span></span> <span data-ttu-id="07130-105">Sorun yaşıyorsanız bkz. [kendi parolanızı değiştirme ve sıfırlama](active-directory-passwords-update-your-own-password.md).</span><span class="sxs-lookup"><span data-stu-id="07130-105">If so, [here's how you can change and reset your own password](active-directory-passwords-update-your-own-password.md).</span></span>

## <a name="rapidly-deploy-self-service-password-reset"></a><span data-ttu-id="07130-106">Self servis parola sıfırlamayı hızlıca dağıtma</span><span class="sxs-lookup"><span data-stu-id="07130-106">Rapidly deploy self-service password reset</span></span>

<span data-ttu-id="07130-107">Basit bir BT yöneticileri tooempower kullanıcılar tooreset anlamına gelir veya bunların parolaları veya hesaplarının kilidini (SSPR) teklifleri Self Servis parola sıfırlama.</span><span class="sxs-lookup"><span data-stu-id="07130-107">Self-service password reset (SSPR) offers a simple means for IT administrators tooempower users tooreset or unlock their passwords or accounts.</span></span> <span data-ttu-id="07130-108">Kullanıcıların hello sistem bildirimleri tooalert birlikte kullandığınızda hello sistem ayrıntılı raporlama tootrack içerir, toomisuse veya Uygunsuz kullanım.</span><span class="sxs-lookup"><span data-stu-id="07130-108">hello system includes detailed reporting tootrack when users use hello system along with notifications tooalert you toomisuse or abuse.</span></span>

<span data-ttu-id="07130-109">Bu kılavuz, çalışan bir deneme sürümü ya da lisanslı bir Azure AD kiracısına zaten sahip olduğunuzu varsayar.</span><span class="sxs-lookup"><span data-stu-id="07130-109">This guide assumes you already have a working trial or licensed Azure AD tenant.</span></span> <span data-ttu-id="07130-110">Azure AD ayarı yardıma gereksinim duyarsanız, hello makalesine bakın [Azure AD ile çalışmaya başlama](https://azure.microsoft.com/trial/get-started-active-directory/).</span><span class="sxs-lookup"><span data-stu-id="07130-110">If you need help setting up Azure AD, see hello article [Getting Started with Azure AD](https://azure.microsoft.com/trial/get-started-active-directory/).</span></span>

1. <span data-ttu-id="07130-111">Var olan Azure AD kiracınızda **"Parola sıfırlama"** öğesini seçin</span><span class="sxs-lookup"><span data-stu-id="07130-111">From your existing Azure AD tenant, select **"Password reset"**</span></span>

2. <span data-ttu-id="07130-112">Merhaba gelen **"Özellikler"** "Self Servis parola sıfırlama etkin" Merhaba aşağıdakilerden birini hello seçeneği altında ekranı</span><span class="sxs-lookup"><span data-stu-id="07130-112">From hello **"Properties"** screen, under hello option "Self Service Password Reset Enabled" choose one of hello following</span></span>
    * <span data-ttu-id="07130-113">Kimse - herhangi bir mümkün toouse SSPR işlevdir</span><span class="sxs-lookup"><span data-stu-id="07130-113">Nobody - No one is able toouse SSPR functionality</span></span>
    * <span data-ttu-id="07130-114">Bir - belirli bir Azure AD yalnızca üyeleri, seçtiğiniz grubu mümkün toouse SSPR işlevselliği olan</span><span class="sxs-lookup"><span data-stu-id="07130-114">A group - Only members of a specific Azure AD group that you choose are able toouse SSPR functionality</span></span>
    * <span data-ttu-id="07130-115">Herkes - tüm kullanıcılar Azure AD kiracınıza hesaplarıyla olan mümkün toouse SSPR işlevi</span><span class="sxs-lookup"><span data-stu-id="07130-115">Everybody - All users with accounts in your Azure AD tenant are able toouse SSPR functionality</span></span>

3. <span data-ttu-id="07130-116">Merhaba gelen **"Kimlik doğrulama yöntemleri"** ekran'ı seçin</span><span class="sxs-lookup"><span data-stu-id="07130-116">From hello **"Authentication methods"** screen choose</span></span>
    * <span data-ttu-id="07130-117">Birkaç yöntem tooreset gerekli - en az bir ya da en az iki destekliyoruz</span><span class="sxs-lookup"><span data-stu-id="07130-117">Number of methods required tooreset - We support a minimum of one or a maximum of two</span></span>
    * <span data-ttu-id="07130-118">Yöntemleri kullanılabilir toousers - en az bir ihtiyacımız ancak hiçbir zaman toohave kullanılabilir bir ek seçim hurts</span><span class="sxs-lookup"><span data-stu-id="07130-118">Methods available toousers - We need at least one but it never hurts toohave an extra choice available</span></span>
        * <span data-ttu-id="07130-119">**E-posta** bir e-posta kodu toohello kullanıcı kimlik doğrulama e-posta adresi yapılandırılmış gönderir</span><span class="sxs-lookup"><span data-stu-id="07130-119">**Email** sends an email with a code toohello user's configured authentication email address</span></span>
        * <span data-ttu-id="07130-120">**Cep telefonu** verir hello kullanıcı hello seçim tooreceive bir çağrı veya metin kodu tootheir ile yapılandırılmış mobil telefon numarası</span><span class="sxs-lookup"><span data-stu-id="07130-120">**Mobile Phone** gives hello user hello choice tooreceive a call or text with a code tootheir configured mobile phone number</span></span>
        * <span data-ttu-id="07130-121">**Ofis telefonu** çağrıları hello kullanıcı kodu tootheir ile yapılandırılan ofis telefon numarası</span><span class="sxs-lookup"><span data-stu-id="07130-121">**Office Phone** calls hello user with a code tootheir configured office phone number</span></span>
        * <span data-ttu-id="07130-122">**Güvenlik soruları** toochoose gerektirir</span><span class="sxs-lookup"><span data-stu-id="07130-122">**Security Questions** requires you toochoose</span></span>
            * <span data-ttu-id="07130-123">Soru sayısı tooregister gerekli - başarılı kaydı, yani bir kullanıcı için hello en az bir havuzu toopull gelen sorulara daha fazla toocreate tooanswer seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="07130-123">Number of questions required tooregister - hello minimum for successful registration, meaning a user can choose tooanswer more toocreate a pool of questions toopull from.</span></span> <span data-ttu-id="07130-124">Bu seçenek 3-5'ten ayarlanabilir ve daha büyük veya gerekir soruları gerekli tooreset toohello sayısı eşit.</span><span class="sxs-lookup"><span data-stu-id="07130-124">This option can be set from 3-5 and must be greater than or equal toohello number of questions required tooreset.</span></span>
                * <span data-ttu-id="07130-125">Özel soru güvenlik soruları seçerken hello "Özel" düğmesine tıklayarak eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="07130-125">Custom questions can be added by clicking hello "Custom" button when selecting security questions</span></span>
            * <span data-ttu-id="07130-126">Gereken soru sayısını tooreset - 3-5 soruları toobe sıfırlama veya kilidi kullanıcıların parola toobe izin vermeden önce doğru yanıtların gelen ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="07130-126">Number of questions required tooreset - Can be set from 3-5 questions toobe answered correctly before allowing a users password toobe reset or unlocked.</span></span>

4. <span data-ttu-id="07130-127">Önerilen: **"Özelleştirme"** tanımladığınız toochange hello "yöneticinize başvurun" bağlantı toopoint tooa sayfa veya e-posta adresi izin verir</span><span class="sxs-lookup"><span data-stu-id="07130-127">RECOMMENDED: **"Customization"** allows you toochange hello "Contact your administrator" link toopoint tooa page or email address you define</span></span>

5. <span data-ttu-id="07130-128">İsteğe bağlı: Merhaba **"Kayıt"** ekran Yöneticiler için başlangıç seçeneklerini sağlar:</span><span class="sxs-lookup"><span data-stu-id="07130-128">OPTIONAL: hello **"Registration"** screen provides administrators hello options for:</span></span>
    * <span data-ttu-id="07130-129">Oturum açarken kullanıcıların tooregister gerektirir</span><span class="sxs-lookup"><span data-stu-id="07130-129">Require users tooregister when signing in</span></span>
    * <span data-ttu-id="07130-130">Sayısı kullanıcılar önce gün sorulan tooreconfirm kendi kimlik doğrulama bilgileri</span><span class="sxs-lookup"><span data-stu-id="07130-130">Number of days before users are asked tooreconfirm their authentication information</span></span>

6. <span data-ttu-id="07130-131">İsteğe bağlı: Merhaba **"Bildirim"** ekran Yöneticiler için hello seçenekleri sağlar:</span><span class="sxs-lookup"><span data-stu-id="07130-131">OPTIONAL: hello **"Notification"** screen provides administrators hello options to:</span></span>
    * <span data-ttu-id="07130-132">Parola sıfırlamayı kullanıcılara bildir</span><span class="sxs-lookup"><span data-stu-id="07130-132">Notify users on password resets</span></span>
    * <span data-ttu-id="07130-133">Diğer yöneticiler parolalarını sıfırladığında tüm yöneticilere bildir</span><span class="sxs-lookup"><span data-stu-id="07130-133">Notify all admins when other admins reset their password</span></span>

<span data-ttu-id="07130-134">**Bu noktada Azure AD kiracınız için SSPR’ı yapılandırdınız**.</span><span class="sxs-lookup"><span data-stu-id="07130-134">**At this point, you have configured SSPR for your Azure AD tenant**.</span></span> <span data-ttu-id="07130-135">Burada durdurun ya da üzerinde tooconfigure devam parolaları tooan eşitlemesini şirket içi AD etki alanı.</span><span class="sxs-lookup"><span data-stu-id="07130-135">You can stop here or continue on tooconfigure synchronization of passwords tooan on-premises AD domain.</span></span>

> [!NOTE]
> <span data-ttu-id="07130-136">Microsoft, Azure yönetici hesapları için güçlü kimlik doğrulama gereksinimleri uyguladığından, SSPR özelliğini yönetici olmayan bir kullanıcıyla test edin.</span><span class="sxs-lookup"><span data-stu-id="07130-136">Test SSPR with a user and not an administrator as Microsoft enforces strong authentication requirements for Azure administrator type accounts.</span></span> <span data-ttu-id="07130-137">Hello Yöneticisi parola ilkesi hakkında daha fazla bilgi için bkz: bizim [parola ilkesi makale](active-directory-passwords-policy.md#administrator-password-policy-differences).</span><span class="sxs-lookup"><span data-stu-id="07130-137">For more information regarding hello administrator password policy, see our [password policy article](active-directory-passwords-policy.md#administrator-password-policy-differences).</span></span>

## <a name="configure-synchronization-tooexisting-identity-source"></a><span data-ttu-id="07130-138">Eşitleme tooexisting kimlik kaynağı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="07130-138">Configure synchronization tooexisting identity source</span></span>

<span data-ttu-id="07130-139">tooenable şirket içi kimlik eşitleme tooAzure AD, yapılandırmak ve tooinstall gereksinim [Azure AD Connect](./connect/active-directory-aadconnect.md) kuruluşunuzdaki bir sunucuda.</span><span class="sxs-lookup"><span data-stu-id="07130-139">tooenable on-premises identity synchronization tooAzure AD, you need tooinstall and configure [Azure AD Connect](./connect/active-directory-aadconnect.md) on a server in your organization.</span></span> <span data-ttu-id="07130-140">Bu uygulama, eşitleme üzerinden kullanıcıların ve grupların varolan kimlik kaynak tooyour Azure AD kiracınıza işler.</span><span class="sxs-lookup"><span data-stu-id="07130-140">This application handles synchronizing users and groups from your existing identity source tooyour Azure AD tenant.</span></span>

* [<span data-ttu-id="07130-141">DirSync veya Azure AD eşitleme tooAzure AD Connect yükseltme</span><span class="sxs-lookup"><span data-stu-id="07130-141">Upgrade from DirSync or Azure AD Sync tooAzure AD Connect</span></span>](./connect/active-directory-aadconnect-dirsync-deprecated.md)
* [<span data-ttu-id="07130-142">Hızlı ayarları kullanarak Azure AD Connect ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="07130-142">Getting started with Azure AD Connect using express settings</span></span>](./connect/active-directory-aadconnect-get-started-express.md)
* <span data-ttu-id="07130-143">[Parola geri yazma yapılandırma](active-directory-passwords-writeback.md#configuring-password-writeback) toowrite parolaları Azure AD alanından geri tooyour şirket içi dizin.</span><span class="sxs-lookup"><span data-stu-id="07130-143">[Configure password writeback](active-directory-passwords-writeback.md#configuring-password-writeback) toowrite passwords from Azure AD back tooyour on-premises directory.</span></span>

## <a name="disabling-self-service-password-reset"></a><span data-ttu-id="07130-144">Self servis parola sıfırlamayı devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="07130-144">Disabling self-service password reset</span></span>

<span data-ttu-id="07130-145">Self Servis parola sıfırlama devre dışı bırakma Azure AD kiracınıza açarak ve çok giderek olarak basit**parola sıfırlama > Özellikler** > seçin **hiçbiri** altında **Self Servis parola sıfırlama Etkin**</span><span class="sxs-lookup"><span data-stu-id="07130-145">Disabling self-service password reset is as simple as opening your Azure AD tenant and going too**Password Reset > Properties** > choose **None** under **Self Service Password Reset Enabled**</span></span>

### <a name="learn-more"></a><span data-ttu-id="07130-146">Daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="07130-146">Learn more</span></span>
<span data-ttu-id="07130-147">bağlantılar aşağıdaki hello parola sıfırlama ve Azure AD kullanma ile ilgili ek bilgiler sağlar</span><span class="sxs-lookup"><span data-stu-id="07130-147">hello following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="07130-148">[**Lisanslama**](active-directory-passwords-licensing.md) - Azure AD Lisanslarınızı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="07130-148">[**Licensing**](active-directory-passwords-licensing.md) - Configure your Azure AD Licensing</span></span>
* <span data-ttu-id="07130-149">[**Veri** ](active-directory-passwords-data.md) - gereklidir hello verileri anlamak ve nasıl kullanıldığı için parola yönetimi</span><span class="sxs-lookup"><span data-stu-id="07130-149">[**Data**](active-directory-passwords-data.md) - Understand hello data that is required and how it is used for password management</span></span>
* <span data-ttu-id="07130-150">[**Sunum** ](active-directory-passwords-best-practices.md) -planlama ve burada bulunan hello kılavuzu kullanarak SSPR tooyour kullanıcılara dağıtma</span><span class="sxs-lookup"><span data-stu-id="07130-150">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR tooyour users using hello guidance found here</span></span>
* <span data-ttu-id="07130-151">[**Özelleştirme** ](active-directory-passwords-customize.md) -hello görünümüne hello SSPR deneyimi, şirketiniz için özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="07130-151">[**Customize**](active-directory-passwords-customize.md) - Customize hello look and feel of hello SSPR experience for your company.</span></span>
* <span data-ttu-id="07130-152">[**İlke**](active-directory-passwords-policy.md) - Azure AD parola ilkelerini anlayın ve ayarlayın</span><span class="sxs-lookup"><span data-stu-id="07130-152">[**Policy**](active-directory-passwords-policy.md) - Understand and set Azure AD password policies</span></span>
* <span data-ttu-id="07130-153">[**Raporlama**](active-directory-passwords-reporting.md) - Kullanıcılarınızın SSPR işlevine erişip erişmediğini, ne zaman ve nerede eriştiğini öğrenin</span><span class="sxs-lookup"><span data-stu-id="07130-153">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="07130-154">[**Teknik derinlemesine** ](active-directory-passwords-how-it-works.md) -hello perdenin toounderstand nasıl çalıştığını gidin</span><span class="sxs-lookup"><span data-stu-id="07130-154">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind hello curtain toounderstand how it works</span></span>
* <span data-ttu-id="07130-155">[**Sık Sorulan Sorular**](active-directory-passwords-faq.md) - Nasıl?</span><span class="sxs-lookup"><span data-stu-id="07130-155">[**Frequently Asked Questions**](active-directory-passwords-faq.md) - How?</span></span> <span data-ttu-id="07130-156">Neden?</span><span class="sxs-lookup"><span data-stu-id="07130-156">Why?</span></span> <span data-ttu-id="07130-157">Ne?</span><span class="sxs-lookup"><span data-stu-id="07130-157">What?</span></span> <span data-ttu-id="07130-158">Nerede?</span><span class="sxs-lookup"><span data-stu-id="07130-158">Where?</span></span> <span data-ttu-id="07130-159">Kim?</span><span class="sxs-lookup"><span data-stu-id="07130-159">Who?</span></span> <span data-ttu-id="07130-160">Ne zaman?</span><span class="sxs-lookup"><span data-stu-id="07130-160">When?</span></span> <span data-ttu-id="07130-161">-Her zaman tooask istediğinizi tooquestions yanıtlar</span><span class="sxs-lookup"><span data-stu-id="07130-161">- Answers tooquestions you always wanted tooask</span></span>
* <span data-ttu-id="07130-162">[**Sorun giderme** ](active-directory-passwords-troubleshoot.md) -nasıl biz SSPR ile bkz tooresolve ortak sorunları öğrenin</span><span class="sxs-lookup"><span data-stu-id="07130-162">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how tooresolve common issues that we see with SSPR</span></span>

## <a name="next-steps"></a><span data-ttu-id="07130-163">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="07130-163">Next steps</span></span>

<span data-ttu-id="07130-164">Bu Hızlı Başlangıç, kullanıcılarınız için nasıl tooconfigure Self Servis parola sıfırlama öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="07130-164">In this quickstart, you’ve learned how tooconfigure self-service password reset for your users.</span></span> <span data-ttu-id="07130-165">Merhaba toohello portal bağlantıya toocontinue toohello Azure portal toocomplete şu adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="07130-165">toocontinue toohello Azure portal toocomplete these steps follow hello link below toohello portal.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="07130-166">Self servis parola sıfırlamayı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="07130-166">Enable self-service password reset</span></span>](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/PasswordReset)

