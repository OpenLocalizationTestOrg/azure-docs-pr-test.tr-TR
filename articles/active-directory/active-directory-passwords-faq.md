---
title: "Sık sorulan sorular: Azure AD SSPR'yi | Microsoft Docs"
description: "Azure AD Self Servis parola hakkında sık sorulan sorular Sıfırla"
services: active-directory
keywords: "Active directory parola yönetimi, Azure AD parola yönetimi self servis parola sıfırlama"
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
ms.openlocfilehash: d04a9efeb3b35421aa605cadb2aa25f656a4d515
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="password-management-frequently-asked-questions"></a><span data-ttu-id="0e017-104">Parola yönetimi sık sorulan sorular</span><span class="sxs-lookup"><span data-stu-id="0e017-104">Password management frequently asked questions</span></span>

<span data-ttu-id="0e017-105">Aşağıdaki hello toopassword sıfırlama her şey ilgili sık sorulan bazı sorular olursunuz.</span><span class="sxs-lookup"><span data-stu-id="0e017-105">hello following are some frequently asked questions for all things related toopassword reset.</span></span>

<span data-ttu-id="0e017-106">Azure AD hakkında genel bir sorunuz varsa ve Self Servis parola burada cevaplanıp değil, sıfırlama, istenir hello Topluluk Yardım için hello üzerinde [Azure Ad forumları](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WindowsAzureAD).</span><span class="sxs-lookup"><span data-stu-id="0e017-106">If you have a general question about Azure AD and self-service password reset, that is not answered here, you can ask hello community for assistance on hello [Azure Ad forums](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WindowsAzureAD).</span></span> <span data-ttu-id="0e017-107">Merhaba topluluk üyeleri mühendisleri, ürün yöneticileri, MVP ve arkadaşa BT uzmanları içerir.</span><span class="sxs-lookup"><span data-stu-id="0e017-107">Members of hello community include Engineers, Product Managers, MVPs, and fellow IT Professionals.</span></span>

<span data-ttu-id="0e017-108">Bu SSS, aşağıdaki bölümlerde hello ayrılır:</span><span class="sxs-lookup"><span data-stu-id="0e017-108">This FAQ is split into hello following sections:</span></span>

* [<span data-ttu-id="0e017-109">**Parola sıfırlama kaydı hakkında sorular**</span><span class="sxs-lookup"><span data-stu-id="0e017-109">**Questions about Password Reset Registration**</span></span>](#password-reset-registration)
* [<span data-ttu-id="0e017-110">**Parola sıfırlama hakkında sorular**</span><span class="sxs-lookup"><span data-stu-id="0e017-110">**Questions about Password Reset**</span></span>](#password-reset)
* [<span data-ttu-id="0e017-111">**Parola değiştirme hakkında sorular**</span><span class="sxs-lookup"><span data-stu-id="0e017-111">**Questions about Password Change**</span></span>](#password-change)
* [<span data-ttu-id="0e017-112">**Parola yönetimi hakkında sorular raporları**</span><span class="sxs-lookup"><span data-stu-id="0e017-112">**Questions about password management Reports**</span></span>](#password-management-reports)
* [<span data-ttu-id="0e017-113">**Parola geri yazma hakkında sorular**</span><span class="sxs-lookup"><span data-stu-id="0e017-113">**Questions about password writeback**</span></span>](#password-writeback)

## <a name="password-reset-registration"></a><span data-ttu-id="0e017-114">Parola sıfırlama kaydı</span><span class="sxs-lookup"><span data-stu-id="0e017-114">Password reset registration</span></span>
* <span data-ttu-id="0e017-115">**S: Kullanıcılarım kendi parola sıfırlama verileri kaydedebilirsiniz?**</span><span class="sxs-lookup"><span data-stu-id="0e017-115">**Q:  Can my users register their own password reset data?**</span></span>

  > <span data-ttu-id="0e017-116">**Y:** Evet, parola sıfırlama etkinleştirilmişse ve lisansına sahip olduğunuz sürece, bunlar toohello parola sıfırlama kayıt portalı http://aka.ms/ssprsetup tooregister ', kimlik doğrulama bilgilerini gidebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e017-116">**A:** Yes, as long as password reset is enabled and they are licensed, they can go toohello Password Reset Registration portal at http://aka.ms/ssprsetup tooregister their authentication information.</span></span> <span data-ttu-id="0e017-117">Kullanıcılar ayrıca giderek toohello http://myapps.microsoft.com, adresinden erişim Paneli'nde tarafından hello profil sekmesini tıklatıp seçenek parola sıfırlama için kaydetme hello tıklatarak kaydedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e017-117">Users can also register by going toohello access panel at http://myapps.microsoft.com, clicking hello profile tab, and clicking hello Register for Password Reset option.</span></span>
  >
  >
* <span data-ttu-id="0e017-118">**S: parola sıfırlama verileri Kullanıcılarım adına tanımlamak?**</span><span class="sxs-lookup"><span data-stu-id="0e017-118">**Q:  Can I define password reset data on behalf of my users?**</span></span>

  > <span data-ttu-id="0e017-119">**Y:** Evet, Azure AD Connect, PowerShell hello ile yapabilirsiniz [Azure portal](https://portal.azure.com), veya hello Office Yönetim Portalı.</span><span class="sxs-lookup"><span data-stu-id="0e017-119">**A:** Yes, you can do so with Azure AD Connect, PowerShell, hello [Azure portal](https://portal.azure.com), or hello Office Admin portal.</span></span> <span data-ttu-id="0e017-120">Daha fazla bilgi için hello makalesine bakın [Azure AD Self Servis parola sıfırlama tarafından kullanılan verileri](active-directory-passwords-data.md).</span><span class="sxs-lookup"><span data-stu-id="0e017-120">For more information, see hello article [Data used by Azure AD Self-Service Password Reset](active-directory-passwords-data.md).</span></span>
  >
  >
* <span data-ttu-id="0e017-121">**S: şirket içi güvenlik soruları verileri eşitlemek?**</span><span class="sxs-lookup"><span data-stu-id="0e017-121">**Q:  Can I synchronize data for security questions from on premises?**</span></span>

  > <span data-ttu-id="0e017-122">**Y:** bu bugün mümkün değildir.</span><span class="sxs-lookup"><span data-stu-id="0e017-122">**A:** This is not possible today.</span></span>
  >
  >
* <span data-ttu-id="0e017-123">**S: Kullanıcılarım veri diğer kullanıcılar bu verileri göremez yolla kaydedebilirsiniz?**</span><span class="sxs-lookup"><span data-stu-id="0e017-123">**Q:  Can my users register data in such a way that other users cannot see this data?**</span></span>

  > <span data-ttu-id="0e017-124">**Y:** Evet, kullanıcılar yalnızca genel Yöneticiler ve hello kullanıcı tarafından görülebilir özel kimlik doğrulama alanlara hello kaydedilen parola sıfırlama kayıt portalı kullanarak veri kaydettiğinizde.</span><span class="sxs-lookup"><span data-stu-id="0e017-124">**A:** Yes, when users register data using hello Password Reset Registration Portal it is saved into private authentication fields that are only visible by Global Administrators and hello user.</span></span>
    >
    > [!NOTE]
    > <span data-ttu-id="0e017-125">Varsa bir **Azure yönetici hesabı** hello cep telefonu alanına da doldurulur ve görünür kendi kimlik doğrulama telefon numaranızı kaydeder.</span><span class="sxs-lookup"><span data-stu-id="0e017-125">If an **Azure Administrator account** registers their authentication phone number it is also populated into hello mobile phone field and is visible.</span></span>
    >
  >
  >
* <span data-ttu-id="0e017-126">**S: Kullanıcılarım parola sıfırlamayı kullanabilmek kayıtlı toobe var mı?**</span><span class="sxs-lookup"><span data-stu-id="0e017-126">**Q:  Do my users have toobe registered before they can use password reset?**</span></span>

  > <span data-ttu-id="0e017-127">**Y:** onların adına yeterli kimlik doğrulaması bilgilerini tanımlayın, Hayır, kullanıcıların tooregister yoktur.</span><span class="sxs-lookup"><span data-stu-id="0e017-127">**A:** No, if you define enough authentication information on their behalf, users do not have tooregister.</span></span> <span data-ttu-id="0e017-128">Merhaba uygun hello dizin alanlarında depolanan verilerin düzgün biçimlendirilmiş olduğu sürece works parolasını sıfırlayın.</span><span class="sxs-lookup"><span data-stu-id="0e017-128">Password reset works as long as you have properly formatted data stored in hello appropriate fields in hello directory.</span></span>
  >
  >
* <span data-ttu-id="0e017-129">**S: eşitlemek veya miyim Kullanıcılarım adına ayarlanmış hello kimlik doğrulama telefon, kimlik doğrulama e-posta veya diğer kimlik doğrulama telefon alanları?**</span><span class="sxs-lookup"><span data-stu-id="0e017-129">**Q:  Can I synchronize or set hello Authentication Phone, Authentication Email or Alternate Authentication Phone fields on behalf of my users?**</span></span>

  > <span data-ttu-id="0e017-130">**Y:** bu bugün mümkün değildir.</span><span class="sxs-lookup"><span data-stu-id="0e017-130">**A:** This is not possible today.</span></span>
  >
  >
* <span data-ttu-id="0e017-131">**S: nasıl hello kayıt portalı hangi seçenekleri tooshow Kullanıcılarım biliyor?**</span><span class="sxs-lookup"><span data-stu-id="0e017-131">**Q:  How does hello registration portal know which options tooshow my users?**</span></span>

  > <span data-ttu-id="0e017-132">**Y:** gösterir, kullanıcılarınız için etkinleştirdiğiniz seçenekleri hello yalnızca hello parola sıfırlama kayıt portalı.</span><span class="sxs-lookup"><span data-stu-id="0e017-132">**A:** hello password reset registration portal only shows hello options that you have enabled for your users.</span></span> <span data-ttu-id="0e017-133">Bu seçenekler, dizinin Yapılandır sekmesi kullanıcı parolası sıfırlama ilkesini bölümünü hello altında bulunur. Örneğin, bu güvenlik soruları etkinleştirmezseniz, ardından kullanıcıları bu seçenek için mümkün tooregister anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="0e017-133">These options are found under hello User Password Reset Policy section of your directory’s Configure tab. For example, this means that if you do not enable security questions, then users are not able tooregister for that option.</span></span>
  >
  >
* <span data-ttu-id="0e017-134">**Kullanıcı ne zaman kabul s: kayıtlı?**</span><span class="sxs-lookup"><span data-stu-id="0e017-134">**Q:  When is a user considered registered?**</span></span>

  > <span data-ttu-id="0e017-135">**Y:** kayıtlı olduğunda SSPR için kayıtlı kullanıcı kabul en az hello **yöntemleri gerekli tooreset sayısı** hello ayarladığınız [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0e017-135">**A:** A user is considered registered for SSPR when they have registered at least hello **Number of methods required tooreset** that you have set in hello [Azure portal](https://portal.azure.com).</span></span>
  >
  >
## <a name="password-reset"></a><span data-ttu-id="0e017-136">Parola sıfırlama</span><span class="sxs-lookup"><span data-stu-id="0e017-136">Password reset</span></span>
* <span data-ttu-id="0e017-137">**S: ne kadar ı tooreceive bir e-posta, SMS ya da parola sıfırlama telefon çağrısında beklemesi gerektiğini?**</span><span class="sxs-lookup"><span data-stu-id="0e017-137">**Q:  How long should I wait tooreceive an email, SMS, or phone call from password reset?**</span></span>

  > <span data-ttu-id="0e017-138">**Y:** SMS iletileri, e-posta ve telefon aramaları altında bir dakika içinde 5-20 saniye hello normal durumuyla ulaşması.</span><span class="sxs-lookup"><span data-stu-id="0e017-138">**A:** Email, SMS messages, and phone calls should arrive in under one minute, with hello normal case being 5-20 seconds.</span></span>
    ><span data-ttu-id="0e017-139">Bu zaman dilimi içinde hello bildirim almazsanız:</span><span class="sxs-lookup"><span data-stu-id="0e017-139">If you do not receive hello notification in this time frame:</span></span>
        > * <span data-ttu-id="0e017-140">Gereksiz klasörünüzü kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="0e017-140">Check your junk folder.</span></span>
        > * <span data-ttu-id="0e017-141">Onay hello numarası veya e-posta iletişim kurulan hello bir beklediğiniz değil.</span><span class="sxs-lookup"><span data-stu-id="0e017-141">Check hello number or email being contacted is hello one you expect.</span></span>
        > * <span data-ttu-id="0e017-142">Merhaba dizinindeki Hello kimlik doğrulama verileri doğru biçimlendirilmiş denetleyin.</span><span class="sxs-lookup"><span data-stu-id="0e017-142">Check hello authentication data in hello directory is correctly formatted.</span></span>
                >     * <span data-ttu-id="0e017-143">Örnek: "+ 1 4255551234" veya "user@contoso.com"</span><span class="sxs-lookup"><span data-stu-id="0e017-143">Example: "+1 4255551234" or "user@contoso.com"</span></span>
  >
  >
* <span data-ttu-id="0e017-144">**S: hangi dilde parola sıfırlama tarafından destekleniyor mu?**</span><span class="sxs-lookup"><span data-stu-id="0e017-144">**Q:  What languages are supported by password reset?**</span></span>

  > <span data-ttu-id="0e017-145">**Y:** hello parola sıfırlama kullanıcı Arabirimi, SMS iletileri ve sesli aramalar hello yerelleştirilmiş Office 365'te desteklenen dillerini.</span><span class="sxs-lookup"><span data-stu-id="0e017-145">**A:** hello password reset UI, SMS messages, and voice calls are localized in hello same languages that are supported in Office 365.</span></span>
  >
  >
* <span data-ttu-id="0e017-146">**S: ı my dizininde markalama kuruluş ayarladığınızda hello parola sıfırlama deneyimi hangi kısımlarının markalı alma kullanıcının yapılandırma sekmesi?**</span><span class="sxs-lookup"><span data-stu-id="0e017-146">**Q:  What parts of hello password reset experience get branded when I set organizational branding in my directory’s configure tab?**</span></span>

  > <span data-ttu-id="0e017-147">**Y:** hello parola sıfırlama portalı kuruluş logonuzun gösterir ve tooconfigure hello kişi yönetici bağlantı toopoint tooa özel e-posta adresiniz veya URL sağlar.</span><span class="sxs-lookup"><span data-stu-id="0e017-147">**A:** hello password reset portal shows your organizational logo and allows you tooconfigure hello Contact your administrator link toopoint tooa custom email or URL.</span></span> <span data-ttu-id="0e017-148">Parola sıfırlama gönderilir e-posta kuruluşunuzun logosu, renkler, adı hello hello e-posta gövdesindeki içerir ve adından özelleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="0e017-148">Any email that gets sent by password reset includes your organization’s logo, colors, name in hello body of hello email, and customized from name.</span></span>
  >
  >
* <span data-ttu-id="0e017-149">**S: nasıl miyim eğitin Kullanıcılarım nerede hakkında toogo tooreset parolalarını?**</span><span class="sxs-lookup"><span data-stu-id="0e017-149">**Q:  How can I educate my users about where toogo tooreset their passwords?**</span></span>

  > <span data-ttu-id="0e017-150">**Y:** kullanıcılar toohttps://passwordreset.microsoftonline.com doğrudan gönderebilir veya tooclick hello söyleyebilirsiniz **hesap bağlantısı erişemiyor** herhangi bir iş veya Okul oturum açma sayfasında bulunan.</span><span class="sxs-lookup"><span data-stu-id="0e017-150">**A:** You can send your users toohttps://passwordreset.microsoftonline.com directly, or you can instruct them tooclick hello **Can’t access your account link** found on any Work or School sign-in page.</span></span> <span data-ttu-id="0e017-151">Ayrıca, bu bağlantılar bir yerden kolayca erişilebilir tooyour kullanıcılar yayımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e017-151">You can also publish these links in a place easily accessible tooyour users.</span></span>
  >
  >
* <span data-ttu-id="0e017-152">**S: bir mobil aygıttan bu sayfayı kullanın?**</span><span class="sxs-lookup"><span data-stu-id="0e017-152">**Q:  Can I use this page from a mobile device?**</span></span>

  > <span data-ttu-id="0e017-153">**Y:** Evet, bu sayfayı mobil cihazlarda çalışır.</span><span class="sxs-lookup"><span data-stu-id="0e017-153">**A:** Yes, this page works on mobile devices.</span></span>
  >
  >
* <span data-ttu-id="0e017-154">**S: kullanıcıların parolalarını sıfırladığınızda kilidini açma yerel active directory hesaplarını destekler mi?**</span><span class="sxs-lookup"><span data-stu-id="0e017-154">**Q:  Do you support unlocking local active directory accounts when users reset their passwords?**</span></span>

  > <span data-ttu-id="0e017-155">**Y:** parolalarını sıfırladığınızda Evet, bir kullanıcının parolasını sıfırlar ve parola geri yazma dağıtılan Azure AD Connect'i kullanarak, bu kullanıcı hesabının kilidi otomatik olarak kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="0e017-155">**A:** Yes, when a user resets their password and password writeback has been deployed using Azure AD Connect, that user’s account is automatically unlocked when they reset their password.</span></span>
  >
  >
* <span data-ttu-id="0e017-156">**S: parola sıfırlama doğrudan my kullanıcının masaüstü oturum açma deneyimi nasıl tümleştirebilir miyim?**</span><span class="sxs-lookup"><span data-stu-id="0e017-156">**Q:  How can I integrate password reset directly into my user’s desktop sign-in experience?**</span></span>

  > <span data-ttu-id="0e017-157">**Y:** bir Azure AD Premium müşterisiyseniz, hiçbir ek ücret Microsoft Identity Manager yükleme ve bu gereksinim hello şirket içi parola sıfırlama çözüm toomeet dağıtma.</span><span class="sxs-lookup"><span data-stu-id="0e017-157">**A:** If you are an Azure AD Premium customer, you can install Microsoft Identity Manager at no additional cost and deploy hello on-premises password reset solution toomeet this requirement.</span></span>
  >
  >
* <span data-ttu-id="0e017-158">**S: farklı yerel ayarlar için farklı güvenlik soruları ayarlamak?**</span><span class="sxs-lookup"><span data-stu-id="0e017-158">**Q:  Can I set different security questions for different locales?**</span></span>

  > <span data-ttu-id="0e017-159">**Y:** bu bugün mümkün değildir.</span><span class="sxs-lookup"><span data-stu-id="0e017-159">**A:** This is not possible today.</span></span>
  >
  >
* <span data-ttu-id="0e017-160">**S: kaç soruları biz hello güvenlik soruları kimlik doğrulaması seçeneği için yapılandırabilir miyim?**</span><span class="sxs-lookup"><span data-stu-id="0e017-160">**Q:  How many questions can we configure for hello Security Questions authentication option?**</span></span>

  > <span data-ttu-id="0e017-161">**Y:** too20 özel güvenlik soruları hello içinde yukarı yapılandırabilirsiniz [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0e017-161">**A:** You can configure up too20 custom security questions in hello [Azure portal](https://portal.azure.com).</span></span>
  >
  >
* <span data-ttu-id="0e017-162">**S: ne kadar süreyle güvenlik soruları olabilir mi?**</span><span class="sxs-lookup"><span data-stu-id="0e017-162">**Q:  How long may security questions be?**</span></span>

  > <span data-ttu-id="0e017-163">**Y:** güvenlik soruları 3 ila 200 karakter uzunluğunda olabilir.</span><span class="sxs-lookup"><span data-stu-id="0e017-163">**A:** Security questions may be between 3 and 200 characters long.</span></span>
  >
  >
* <span data-ttu-id="0e017-164">**S: ne kadar süreyle yanıtlar toosecurity soruları olabilir mi?**</span><span class="sxs-lookup"><span data-stu-id="0e017-164">**Q:  How long may answers toosecurity questions be?**</span></span>

  > <span data-ttu-id="0e017-165">**Y:** yanıtlar 3 too40 karakter uzunluğunda olabilir.</span><span class="sxs-lookup"><span data-stu-id="0e017-165">**A:** Answers may be 3 too40 characters long.</span></span>
  >
  >
* <span data-ttu-id="0e017-166">**S: Yinelenen yanıtlara toosecurity sorular reddedilir?**</span><span class="sxs-lookup"><span data-stu-id="0e017-166">**Q:  Are duplicate answers toosecurity questions rejected?**</span></span>

  > <span data-ttu-id="0e017-167">**Y:** Evet, biz yinelenen yanıtlara toosecurity sorular reddedin.</span><span class="sxs-lookup"><span data-stu-id="0e017-167">**A:** Yes, we reject duplicate answers toosecurity questions.</span></span>
  >
  >
* <span data-ttu-id="0e017-168">**S: May bir kullanıcı kaydı hello aynı Güvenlik sorusu birden çok kez?**</span><span class="sxs-lookup"><span data-stu-id="0e017-168">**Q:  May a user register hello same security question more than once?**</span></span>

  > <span data-ttu-id="0e017-169">**Y:** bir kullanıcı belirli bir sorunun kaydeder sonra Hayır, bunlar bu soruyu ikinci kez kayıt.</span><span class="sxs-lookup"><span data-stu-id="0e017-169">**A:** No, once a user registers a particular question, they may not register for that question a second time.</span></span>
  >
  >
* <span data-ttu-id="0e017-170">**S: olası tooset kaydı ve sıfırlama için güvenlik soruları minimum sınırı nedir?**</span><span class="sxs-lookup"><span data-stu-id="0e017-170">**Q:  Is it possible tooset a minimum limit of security questions for registration and reset?**</span></span>

  > <span data-ttu-id="0e017-171">**Y:** kaydı ve sıfırlama için başka bir sınır Evet, ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="0e017-171">**A:** Yes, one limit can be set for registration and another for reset.</span></span> <span data-ttu-id="0e017-172">3-5 güvenlik soruları kaydı için gerekli olabilir ve 3-5 sıfırlama için gerekli olabilir.</span><span class="sxs-lookup"><span data-stu-id="0e017-172">3-5 security questions may be required for registration and 3-5 may be required for reset.</span></span>
  >
  >
* <span data-ttu-id="0e017-173">**S: nasıl bir kullanıcı birden çok soruları gerekli tooreset hello sayısının kaydedildiyse, güvenlik soruları sıfırlaması sırasında seçilir?**</span><span class="sxs-lookup"><span data-stu-id="0e017-173">**Q:  If a user has registered more than hello maximum number of questions required tooreset, how are security questions selected during reset?**</span></span>

  > <span data-ttu-id="0e017-174">**Y:** N güvenlik soruları seçili rastgele hello toplam soru kullanıcı sayısını dışında kayıtlı, burada N hello **sorular gerekli tooreset sayısı**.</span><span class="sxs-lookup"><span data-stu-id="0e017-174">**A:** N security questions are selected at random out of hello total number of questions a user has registered for, where N is hello **Number of questions required tooreset**.</span></span> <span data-ttu-id="0e017-175">Örneğin, bir kullanıcı 5 güvenlik soruları kayıtlı var, ancak yalnızca 3'ü gerekli tooreset, hello 5 3 rastgele seçilir ve sıfırlama sırasında sunulan.</span><span class="sxs-lookup"><span data-stu-id="0e017-175">For example, if a user has 5 security questions registered, but only 3 are required tooreset, 3 of hello 5 are selected randomly and presented at reset.</span></span> <span data-ttu-id="0e017-176">Merhaba kullanıcı hello yanıtlar toohello sorular yanlış alırsa, soru tooprevent sözcüğüne hello seçimi işlemi oluşana.</span><span class="sxs-lookup"><span data-stu-id="0e017-176">If hello user gets hello answers toohello questions wrong, hello selection process reoccurs tooprevent question hammering.</span></span>
  >
  >
* <span data-ttu-id="0e017-177">**S: kullanıcıları parola sıfırlama birçok kez kısa süre içinde denemelerini önlemek?**</span><span class="sxs-lookup"><span data-stu-id="0e017-177">**Q:  Do you prevent users from attempting password reset many times in a short time period?**</span></span>

  > <span data-ttu-id="0e017-178">**Y:** Evet, parola sıfırlama tooprotect kötüye yerleşik güvenlik özellikleri vardır.</span><span class="sxs-lookup"><span data-stu-id="0e017-178">**A:** Yes, there are security features built into password reset tooprotect from misuse.</span></span> <span data-ttu-id="0e017-179">Kullanıcılar yalnızca 5 parola sıfırlama girişimlerine 24 saat kilitlenmelerini önce bir saat içinde deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e017-179">Users may only try 5 password reset attempts within an hour before being locked out for 24 hours.</span></span> <span data-ttu-id="0e017-180">Kullanıcılar, 24 saat kilitlenmelerini önce bir saat içinde 5 kez toovalidate bir telefon numarası yalnızca deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e017-180">Users may only try toovalidate a phone number 5 times within an hour before being locked out for 24 hours.</span></span> <span data-ttu-id="0e017-181">Kullanıcılar, 24 saat kilitlenmelerini önce 5 kez bir saat içinde tek kimlik doğrulama yöntemini yalnızca deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e017-181">Users may only try a single authentication method 5 times within an hour before being locked out for 24 hours.</span></span>
  >
  >
* <span data-ttu-id="0e017-182">**S: ne kadar süreyle hello e-posta ve SMS bir kerelik geçiş kodu geçerli misiniz?**</span><span class="sxs-lookup"><span data-stu-id="0e017-182">**Q:  For how long are hello email and SMS one-time passcode valid?**</span></span>

  > <span data-ttu-id="0e017-183">**Y:** hello oturum yaşam parola sıfırlama için olan 105 dakika.</span><span class="sxs-lookup"><span data-stu-id="0e017-183">**A:** hello session lifetime for password reset is 105 minutes.</span></span> <span data-ttu-id="0e017-184">Merhaba Hello baştan işlemi parola sıfırlama, hello kullanıcı parolalarını 105 dakika tooreset sahiptir.</span><span class="sxs-lookup"><span data-stu-id="0e017-184">From hello beginning of hello password reset operation, hello user has 105 minutes tooreset their password.</span></span> <span data-ttu-id="0e017-185">Bu süre dolduktan sonra hello e-posta ve SMS bir kerelik geçiş kodu geçersiz.</span><span class="sxs-lookup"><span data-stu-id="0e017-185">hello email and SMS one-time passcode are invalid after this time period expires.</span></span>
  >
  >

## <a name="password-change"></a><span data-ttu-id="0e017-186">Parola değiştirme</span><span class="sxs-lookup"><span data-stu-id="0e017-186">Password change</span></span>
* <span data-ttu-id="0e017-187">**S: Kullanıcılarım toochange parolalarını nereye?**</span><span class="sxs-lookup"><span data-stu-id="0e017-187">**Q:  Where should my users go toochange their passwords?**</span></span>

  > <span data-ttu-id="0e017-188">**Y:** kullanıcıların parolalarını değişebilir gördüğünüz her yerde bunlar kendi profil resmi veya simgesi (Merhaba sağ üst köşedeki ister kendi [Office 365](https://portal.office.com) veya [erişim paneli](https://myapps.microsoft.com) karşılaştığında.</span><span class="sxs-lookup"><span data-stu-id="0e017-188">**A:** Users may change their passwords anywhere they see their profile picture or icon (like in hello upper right corner of their [Office 365](https://portal.office.com) or [Access Panel](https://myapps.microsoft.com) experiences.</span></span> <span data-ttu-id="0e017-189">Kullanıcıların parolalarını hello değişebilir [erişim paneli profili sayfasını](https://account.activedirectory.windowsazure.com/r#/profile).</span><span class="sxs-lookup"><span data-stu-id="0e017-189">Users may change their passwords from hello [Access Panel profile page](https://account.activedirectory.windowsazure.com/r#/profile).</span></span> <span data-ttu-id="0e017-190">Kullanıcılar ayrıca olabilir parolalarının süresinin dolduğu varsa toochange parolalarını hello Azure AD oturum açma ekranı otomatik olarak istedi.</span><span class="sxs-lookup"><span data-stu-id="0e017-190">Users may also be asked toochange their passwords automatically at hello Azure AD sign-in screen if their passwords have expired.</span></span> <span data-ttu-id="0e017-191">Son olarak, kullanıcılar toohello gidin [Azure AD parola değişikliği Portal](https://account.activedirectory.windowsazure.com/ChangePassword.aspx) doğrudan toochange parolalarını istediklerinde.</span><span class="sxs-lookup"><span data-stu-id="0e017-191">Finally, users may navigate toohello [Azure AD Password Change Portal](https://account.activedirectory.windowsazure.com/ChangePassword.aspx) directly if they wish toochange their passwords.</span></span>
  >
  >
* <span data-ttu-id="0e017-192">**S: şirket içi parolalarını sona erdiğinde Kullanıcılarım hello Office portalı bildirilebilir?**</span><span class="sxs-lookup"><span data-stu-id="0e017-192">**Q:  Can my users be notified in hello Office Portal when their on-premises password expires?**</span></span>

  > <span data-ttu-id="0e017-193">**Y:** burada hello yönergeleri izleyerek ADFS kullanıyorsanız, bu bugün mümkündür: [ADFS ile parola ilkesi talep gönderme](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configure-ad-fs-to-send-password-expiry-claims?f=255&MSPPError=-2147217396).</span><span class="sxs-lookup"><span data-stu-id="0e017-193">**A:** This is possible today if you are using ADFS by following hello instructions here: [Sending Password Policy Claims with ADFS](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configure-ad-fs-to-send-password-expiry-claims?f=255&MSPPError=-2147217396).</span></span> <span data-ttu-id="0e017-194">Parola karma eşitlemesi kullanıyorsanız, bu bugün mümkün değildir.</span><span class="sxs-lookup"><span data-stu-id="0e017-194">If you are using password hash synchronization, this is not possible today.</span></span> <span data-ttu-id="0e017-195">Biz şirket içi parola ilkeleri eşitleme değil çünkü bu, bize mümkün değildir toopost süre sonu bildirimleri toocloud karşılaştığında.</span><span class="sxs-lookup"><span data-stu-id="0e017-195">This is because we do not sync password policies from on-premises, so it is not possible for us toopost expiry notifications toocloud experiences.</span></span> <span data-ttu-id="0e017-196">Her iki durumda da çok mümkündür[parolaları hakkında tooexpire PowerShell kullanarak kullanıcıları bildir](https://social.technet.microsoft.com/wiki/contents/articles/23313.notify-active-directory-users-about-password-expiry-using-powershell.aspx).</span><span class="sxs-lookup"><span data-stu-id="0e017-196">In either case, it is also possible too[notify users whose passwords are about tooexpire by using PowerShell](https://social.technet.microsoft.com/wiki/contents/articles/23313.notify-active-directory-users-about-password-expiry-using-powershell.aspx).</span></span>
  >
  >

## <a name="password-management-reports"></a><span data-ttu-id="0e017-197">Parola yönetimi raporları</span><span class="sxs-lookup"><span data-stu-id="0e017-197">Password management reports</span></span>
* <span data-ttu-id="0e017-198">**S: hello parola yönetimi raporlardaki verileri tooshow ne kadar sürer?**</span><span class="sxs-lookup"><span data-stu-id="0e017-198">**Q:  How long does it take for data tooshow up on hello password management reports?**</span></span>

  > <span data-ttu-id="0e017-199">**Y:** veri 5-10 dakika içinde hello parola yönetimi raporlarda görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="0e017-199">**A:** Data should appear on hello password management reports within 5-10 minutes.</span></span> <span data-ttu-id="0e017-200">Bu tooan saat tooappear sürebilir bazı örnekler.</span><span class="sxs-lookup"><span data-stu-id="0e017-200">It some instances it may take up tooan hour tooappear.</span></span>
  >
  >
* <span data-ttu-id="0e017-201">**S: Merhaba parola yönetimi raporları filtre nasıl sağlayabilirsiniz?**</span><span class="sxs-lookup"><span data-stu-id="0e017-201">**Q:  How can I filter hello password management reports?**</span></span>

  > <span data-ttu-id="0e017-202">**Y:** hello raporun hello üstüne yakın hello sütun etiketlerinin hello küçük Büyüteç toohello aşırı sağ tıklayarak hello parola yönetimi raporları filtreleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e017-202">**A:** You can filter hello password management reports by clicking hello small magnifying glass toohello extreme right of hello column labels, near hello top of hello report.</span></span> <span data-ttu-id="0e017-203">Toodo daha zengin filtreleme istiyorsanız hello rapor tooexcel indirin ve bir PivotTable oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0e017-203">If you want toodo richer filtering, you can download hello report tooexcel and create a pivot table.</span></span>
  >
  >
* <span data-ttu-id="0e017-204">**S: hello sayısı en çok olay nedir depolanır hello parola yönetimi raporlarda?**</span><span class="sxs-lookup"><span data-stu-id="0e017-204">**Q: What is hello maximum number of events are stored in hello password management reports?**</span></span>

  > <span data-ttu-id="0e017-205">**Y:** too75 000 parola sıfırlama veya parola sıfırlama kayıt olayları hello parola yönetimi raporları, geri too30 günleri kapsayıcı depolanır.</span><span class="sxs-lookup"><span data-stu-id="0e017-205">**A:** Up too75,000 password reset or password reset registration events are stored in hello password management reports, spanning back up too30 days.</span></span>  <span data-ttu-id="0e017-206">Tooexpand bu çalışıyoruz tooinclude daha fazla olay numarası.</span><span class="sxs-lookup"><span data-stu-id="0e017-206">We are working tooexpand this number tooinclude more events.</span></span>
  >
  >
* <span data-ttu-id="0e017-207">**S: hello parola yönetimi raporları ne kadar geri dönün?**</span><span class="sxs-lookup"><span data-stu-id="0e017-207">**Q:  How far back do hello password management reports go?**</span></span>

  > <span data-ttu-id="0e017-208">**Y:** hello parola yönetimi raporları son 30 gün içinde hello yürütülen Göster işlem.</span><span class="sxs-lookup"><span data-stu-id="0e017-208">**A:** hello password management reports show operations occurring within hello last 30 days.</span></span> <span data-ttu-id="0e017-209">Şu an için bu verileri tooarchive gerekiyorsa, hello raporları düzenli aralıklarla indirin ve bunları ayrı bir konuma kaydedin.</span><span class="sxs-lookup"><span data-stu-id="0e017-209">For now, if you need tooarchive this data, you can download hello reports periodically and save them in a separate location.</span></span>
  >
  >
* <span data-ttu-id="0e017-210">**S: hello parola yönetimi raporlarda görüntülenen satır sayısının üst sınırını var mı?**</span><span class="sxs-lookup"><span data-stu-id="0e017-210">**Q:  Is there a maximum number of rows that can appear on hello password management reports?**</span></span>

  > <span data-ttu-id="0e017-211">**Y:** bunlar gösterilir olup olmadığını Evet, en fazla 75,000 satırları hello parola yönetimi raporları, birini görünebilir UI veya yüklenen hello.</span><span class="sxs-lookup"><span data-stu-id="0e017-211">**A:** Yes, a maximum of 75,000 rows may appear on either of hello password management reports, whether they are being shown in hello UI or being downloaded.</span></span>
  >
  >
* <span data-ttu-id="0e017-212">**S: bir API tooaccess hello parola sıfırlama veya kayıt raporlama verileri var mı?**</span><span class="sxs-lookup"><span data-stu-id="0e017-212">**Q:  Is there an API tooaccess hello password reset or registration reporting data?**</span></span>

  > <span data-ttu-id="0e017-213">**Y:** Evet, hello bkz belgeleri toolearn hello parola nasıl erişebileceğinizi raporlama veri akışı sıfırlayın.</span><span class="sxs-lookup"><span data-stu-id="0e017-213">**A:** Yes, see hello following documentation toolearn how you can access hello password reset reporting data stream.</span></span>  <span data-ttu-id="0e017-214">[Nasıl tooaccess parola raporlama olayları program aracılığıyla sıfırlama öğrenin](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent).</span><span class="sxs-lookup"><span data-stu-id="0e017-214">[Learn how tooaccess password reset reporting events programmatically](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent).</span></span>
  >
  >

## <a name="password-writeback"></a><span data-ttu-id="0e017-215">Parola geri yazma</span><span class="sxs-lookup"><span data-stu-id="0e017-215">Password writeback</span></span>
* <span data-ttu-id="0e017-216">**S: parola geri yazma hello arka planda nasıl çalışır?**</span><span class="sxs-lookup"><span data-stu-id="0e017-216">**Q:  How does password writeback work behind hello scenes?**</span></span>

  > <span data-ttu-id="0e017-217">**Y:** bkz [parola geri yazma nasıl çalıştığını](active-directory-passwords-writeback.md) , parola geri yazma ve veri hello sistemi üzerinden şirket içi ortamınıza geri akışını sağlayan bir açıklama ne gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="0e017-217">**A:** See [How password writeback works](active-directory-passwords-writeback.md) for an explanation of what happens when you enable password writeback, and how data flows through hello system back into your on-premises environment.</span></span>
  >
  >
* <span data-ttu-id="0e017-218">**S: parola geri yazma toowork ne kadar sürer?  Parola karma eşitlemesi ile gibi bir eşitleme gecikme var mı?**</span><span class="sxs-lookup"><span data-stu-id="0e017-218">**Q:  How long does password writeback take toowork?  Is there a synchronization delay like with password hash sync?**</span></span>

  > <span data-ttu-id="0e017-219">**Y:** parola geri yazma anlık.</span><span class="sxs-lookup"><span data-stu-id="0e017-219">**A:** Password writeback is instant.</span></span> <span data-ttu-id="0e017-220">Parola karma eşitlemesi temelde farklı çalışır zaman uyumlu bir ardışık düzen olur.</span><span class="sxs-lookup"><span data-stu-id="0e017-220">It is a synchronous pipeline that works fundamentally differently than password hash synchronization.</span></span> <span data-ttu-id="0e017-221">Parola geri yazma, kullanıcıların parolalarını hello başarısını hakkında gerçek zamanlı geri tooget sıfırlama veya değiştirme işlemi sağlar.</span><span class="sxs-lookup"><span data-stu-id="0e017-221">Password writeback allows users tooget real-time feedback about hello success of their password reset or change operation.</span></span> <span data-ttu-id="0e017-222">başarılı bir parola geri yazma için ortalama süreyi Hello altında 500 ms ' dir.</span><span class="sxs-lookup"><span data-stu-id="0e017-222">hello average time for a successful writeback of a password is under 500 ms.</span></span>
  >
  >
* <span data-ttu-id="0e017-223">**S: şirket içi Hesabımı devre dışıysa, my bulut hesabı/erişimi nasıl etkileniyor mu?**</span><span class="sxs-lookup"><span data-stu-id="0e017-223">**Q:  If my on-premises account is disabled, how is my cloud account/access affected?**</span></span>

  > <span data-ttu-id="0e017-224">**Y:** şirket içi Kimliğinizi devre dışıysa, kimliği/erişim de devre dışı bırakılacak hello sonraki eşitleme aralıkta AAD Connect byt varsayılan aracılığıyla bulut 30 dakikada budur.</span><span class="sxs-lookup"><span data-stu-id="0e017-224">**A:** If your on-premises ID is disabled, your cloud ID/access will also be disabled at hello next sync interval via AAD Connect byt default this is every 30 minutes.</span></span>
  >
  >
* <span data-ttu-id="0e017-225">**S: şirket içi Hesabımı bir şirket içi Active Directory parola ilkesi tarafından kısıtlı, SSPR hello parolayı değiştirdiğinizde, bu ilke uyma mu?**</span><span class="sxs-lookup"><span data-stu-id="0e017-225">**Q:  If my on-premises account is constrained by an on-premises Active Directory password policy, does SSPR obey this policy when I change hello password?**</span></span>

  > <span data-ttu-id="0e017-226">**Y:** Evet, SSPR kullanır ve bağlıdır hello şirket içi tanımlanmış tüm hassas parola ilkeleri yanı sıra AD parola ilkesi tipik AD etki alanı parola ilkesi de dahil olmak üzere, hedeflenen kullanıcı verilen tooa.</span><span class="sxs-lookup"><span data-stu-id="0e017-226">**A:** Yes, SSPR relies on and abides by hello on-premises AD password policy, including typical AD domain password policy, as well as any defined fine grained password policies targeted tooa given user.</span></span>
  >
  >
* <span data-ttu-id="0e017-227">**S: hangi tür hesabı için parola geri yazma çalışıyor mu?**</span><span class="sxs-lookup"><span data-stu-id="0e017-227">**Q:  What types of accounts does password writeback work for?**</span></span>

  > <span data-ttu-id="0e017-228">**Y:** parola geri yazma federe ve parola karma eşitlenen kullanıcılar için çalışır.</span><span class="sxs-lookup"><span data-stu-id="0e017-228">**A:** Password writeback works for Federated and Password Hash Synchronized users.</span></span>
  >
  >
* <span data-ttu-id="0e017-229">**S: parola geri yazma etki alanımın parola ilkelerini zorlamak mu?**</span><span class="sxs-lookup"><span data-stu-id="0e017-229">**Q:  Does password writeback enforce my domain’s password policies?**</span></span>

  > <span data-ttu-id="0e017-230">**Y:** Evet, parola geri yazma özelliğini parola geçerlilik süresi, geçmiş, karmaşıklık, filtreleri ve yerleştirdiğiniz parolaları bir yerde yerel etki alanınızda kısıtlama zorlar.</span><span class="sxs-lookup"><span data-stu-id="0e017-230">**A:** Yes, password writeback enforces password age, history, complexity, filters, and any other restriction you may put in place on passwords in your local domain.</span></span>
  >
  >
* <span data-ttu-id="0e017-231">**S: parola geri yazma güvenli mi?  I bilgisayar korsanlarının saldırısına uğrarsa olmaz nasıl mutlaka?**</span><span class="sxs-lookup"><span data-stu-id="0e017-231">**Q:  Is password writeback secure?  How can I be sure I won’t get hacked?**</span></span>

  > <span data-ttu-id="0e017-232">**Y:** Evet, parola geri yazma güvenlidir.</span><span class="sxs-lookup"><span data-stu-id="0e017-232">**A:** Yes, password writeback is secure.</span></span> <span data-ttu-id="0e017-233">Merhaba dört güvenlik katmanları hakkında daha fazla tooread hello parola geri yazma hizmeti tarafından uygulanan, hello denetleyin [parola geri yazma güvenlik modeli](active-directory-passwords-writeback.md#password-writeback-security-model) parola geri yazma nasıl çalıştığını, bölüm.</span><span class="sxs-lookup"><span data-stu-id="0e017-233">tooread more about hello four layers of security implemented by hello password writeback service, check out hello [Password writeback security model](active-directory-passwords-writeback.md#password-writeback-security-model) section in How password writeback works.</span></span>
  >
  >

## <a name="next-steps"></a><span data-ttu-id="0e017-234">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0e017-234">Next steps</span></span>

<span data-ttu-id="0e017-235">bağlantılar aşağıdaki hello parola sıfırlama ve Azure AD kullanma ile ilgili ek bilgiler sağlar</span><span class="sxs-lookup"><span data-stu-id="0e017-235">hello following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="0e017-236">[**Hızlı Başlangıç**](active-directory-passwords-getting-started.md) - Azure AD self servis parola yönetimi ile çalışmaya hazırlanın</span><span class="sxs-lookup"><span data-stu-id="0e017-236">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="0e017-237">[**Lisanslama**](active-directory-passwords-licensing.md) - Azure AD Lisanslarınızı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="0e017-237">[**Licensing**](active-directory-passwords-licensing.md) - Configure your Azure AD Licensing</span></span>
* <span data-ttu-id="0e017-238">[**Veri** ](active-directory-passwords-data.md) - gereklidir hello verileri anlamak ve nasıl kullanıldığı için parola yönetimi</span><span class="sxs-lookup"><span data-stu-id="0e017-238">[**Data**](active-directory-passwords-data.md) - Understand hello data that is required and how it is used for password management</span></span>
* <span data-ttu-id="0e017-239">[**Sunum** ](active-directory-passwords-best-practices.md) -planlama ve burada bulunan hello kılavuzu kullanarak SSPR tooyour kullanıcılara dağıtma</span><span class="sxs-lookup"><span data-stu-id="0e017-239">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR tooyour users using hello guidance found here</span></span>
* <span data-ttu-id="0e017-240">[**Özelleştirme** ](active-directory-passwords-customize.md) -hello görünümüne hello SSPR deneyimi, şirketiniz için özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e017-240">[**Customize**](active-directory-passwords-customize.md) - Customize hello look and feel of hello SSPR experience for your company.</span></span>
* <span data-ttu-id="0e017-241">[**Raporlama**](active-directory-passwords-reporting.md) - Kullanıcılarınızın SSPR işlevine erişip erişmediğini, ne zaman ve nerede eriştiğini öğrenin</span><span class="sxs-lookup"><span data-stu-id="0e017-241">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="0e017-242">[**İlke**](active-directory-passwords-policy.md) - Azure AD parola ilkelerini anlayın ve ayarlayın</span><span class="sxs-lookup"><span data-stu-id="0e017-242">[**Policy**](active-directory-passwords-policy.md) - Understand and set Azure AD password policies</span></span>
* <span data-ttu-id="0e017-243">[**Parola Geri Yazma**](active-directory-passwords-writeback.md) - Şirket içi dizininizde parola geri yazma özelliğinin nasıl çalıştığını anlayın</span><span class="sxs-lookup"><span data-stu-id="0e017-243">[**Password Writeback**](active-directory-passwords-writeback.md) - How does password writeback work with your on-premises directory</span></span>
* <span data-ttu-id="0e017-244">[**Teknik derinlemesine** ](active-directory-passwords-how-it-works.md) -hello perdenin toounderstand nasıl çalıştığını gidin</span><span class="sxs-lookup"><span data-stu-id="0e017-244">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind hello curtain toounderstand how it works</span></span>
* <span data-ttu-id="0e017-245">[**Sorun giderme** ](active-directory-passwords-troubleshoot.md) -nasıl biz SSPR ile bkz tooresolve ortak sorunları öğrenin</span><span class="sxs-lookup"><span data-stu-id="0e017-245">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how tooresolve common issues that we see with SSPR</span></span>
