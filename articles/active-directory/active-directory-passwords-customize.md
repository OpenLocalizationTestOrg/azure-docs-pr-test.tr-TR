---
title: "Özelleştirme: Azure AD SSPR'yi | Microsoft Docs"
description: "Özelleştirme için Azure AD self servis parola sıfırlama seçenekleri"
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
ms.openlocfilehash: 8b9c120815473b25140b8717f8fdd539c97ebb04
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="customize-azure-ad-functionality-for-self-service-password-reset"></a><span data-ttu-id="0e8fc-103">Self Servis parola sıfırlama için Azure AD işlevselliği özelleştirme</span><span class="sxs-lookup"><span data-stu-id="0e8fc-103">Customize Azure AD functionality for Self-Service Password Reset</span></span>

<span data-ttu-id="0e8fc-104">Self Servis parola sıfırlama dağıtmak isteyen BT uzmanları, kullanıcıları eşleştirmek için deneyimi özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e8fc-104">IT Professionals looking to deploy self-service password reset can customize the experience to match their users.</span></span>

## <a name="customize-the-contact-your-administrator-link"></a><span data-ttu-id="0e8fc-105">Kişinin yöneticisine bağlantınız özelleştirme</span><span class="sxs-lookup"><span data-stu-id="0e8fc-105">Customize the contact your administrator link</span></span>

<span data-ttu-id="0e8fc-106">SSPR etkinleştirilmemiş olsa bile kullanıcılar hala bir "yöneticinize başvurun" parola bağlantı portal sıfırlayın.</span><span class="sxs-lookup"><span data-stu-id="0e8fc-106">Even if SSPR is not enabled users still a "contact your administrator" link on the password reset portal.</span></span>  <span data-ttu-id="0e8fc-107">Bu bağlantıyı tıklatarak kullanıcının parolasını değiştirme konusunda yardım almak için isteyen yöneticilerinizi e-postalar.</span><span class="sxs-lookup"><span data-stu-id="0e8fc-107">Clicking this link emails your administrators asking for assistance in changing the user's password.</span></span> <span data-ttu-id="0e8fc-108">Bu e-posta aşağıdaki sırayla aşağıdaki alıcılara gönderilir:</span><span class="sxs-lookup"><span data-stu-id="0e8fc-108">This email is sent to the following recipients in the following order:</span></span>

1. <span data-ttu-id="0e8fc-109">Varsa **parola Yöneticisi** rol atanır, Yöneticiler bu rolüne sahip bildirim</span><span class="sxs-lookup"><span data-stu-id="0e8fc-109">If the **Password administrator** role is assigned, administrators with this role are notified</span></span>
2. <span data-ttu-id="0e8fc-110">Parola yöneticileri atanır varsa, ardından yöneticilerine **Kullanıcı Yöneticisi** rol bildirim</span><span class="sxs-lookup"><span data-stu-id="0e8fc-110">If no Password administrators are assigned, then administrators with the **User administrator** role are notified</span></span>
3. <span data-ttu-id="0e8fc-111">Önceki roller hiçbiri, ardından atanmış ise **genel Yöneticiler** bildirilir</span><span class="sxs-lookup"><span data-stu-id="0e8fc-111">If neither of the previous roles were assigned, then **Global administrators** are notified</span></span>

<span data-ttu-id="0e8fc-112">Her durumda en fazla 100 alıcıların bildirim.</span><span class="sxs-lookup"><span data-stu-id="0e8fc-112">In all cases, a maximum of 100 recipients are notified.</span></span>

<span data-ttu-id="0e8fc-113">Farklı yönetici hakkında daha fazla bilgi için roller ve bunları atama belgesine bakın [Azure Active Directory'de yönetici rolleri atama](active-directory-assign-admin-roles.md)</span><span class="sxs-lookup"><span data-stu-id="0e8fc-113">To find out more about the different administrator roles and how to assign them see the document [Assigning administrator roles in Azure Active Directory](active-directory-assign-admin-roles.md)</span></span>

### <a name="disable-contact-your-administrator-emails"></a><span data-ttu-id="0e8fc-114">Devre dışı bırakma, yönetici e-postaları başvurun</span><span class="sxs-lookup"><span data-stu-id="0e8fc-114">Disable contact your administrator emails</span></span>

<span data-ttu-id="0e8fc-115">Kuruluşunuzun parola hakkında bildirim Yöneticiler istekleri sıfırlama istemiyorsa aşağıdaki yapılandırma etkinleştirilebilir</span><span class="sxs-lookup"><span data-stu-id="0e8fc-115">If your organization does not want administrators notified about password reset requests, the following configuration can be enabled</span></span>

* <span data-ttu-id="0e8fc-116">Self Servis parola sıfırlama tüm son kullanıcılarınız için etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="0e8fc-116">Enable self-service password reset for all end users.</span></span> <span data-ttu-id="0e8fc-117">Bu seçenek altındadır **parola sıfırlama > Özellikler**.</span><span class="sxs-lookup"><span data-stu-id="0e8fc-117">This option is under **Password Reset > Properties**.</span></span>
    * <span data-ttu-id="0e8fc-118">Kullanıcıların kendi parolalarını sıfırlamasına izin istemezseniz, boş bir grubu erişim kapsamını belirleyebilirsiniz **bu seçeneği önermiyoruz**.</span><span class="sxs-lookup"><span data-stu-id="0e8fc-118">If you do not wish users to reset their own passwords, you can scope access to an empty group **we do not recommend this option**.</span></span>
* <span data-ttu-id="0e8fc-119">Bir web URL'si veya mailto sağlamak için Yardım Masası bağlantısı özelleştirme: kullanıcıların Yardım almak için kullanabileceği adresi.</span><span class="sxs-lookup"><span data-stu-id="0e8fc-119">Customize the helpdesk link to provide a web URL or mailto: address that users can use to get assistance.</span></span> <span data-ttu-id="0e8fc-120">Bu seçenek altındadır **parola sıfırlama > özelleştirme > özel Yardım Masası e-posta veya URL**.</span><span class="sxs-lookup"><span data-stu-id="0e8fc-120">This option is under **Password Reset > Customization > Custom helpdesk email or URL**.</span></span>

## <a name="customize-adfs-sign-in-page-for-sspr"></a><span data-ttu-id="0e8fc-121">SSPR için ADFS oturum açma sayfasını özelleştirme</span><span class="sxs-lookup"><span data-stu-id="0e8fc-121">Customize ADFS sign-in page for SSPR</span></span>

<span data-ttu-id="0e8fc-122">ADFS Yöneticiler makalede bulunan yönergeleri kullanarak kullanıcıların oturum açma sayfasına bir bağlantı ekleyebilirsiniz [Ekle oturum açma sayfası açıklaması](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/add-sign-in-page-description).</span><span class="sxs-lookup"><span data-stu-id="0e8fc-122">ADFS Administrators can add a link to their sign-in page using the guidance found in the article [Add sign-in page description](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/add-sign-in-page-description).</span></span>

<span data-ttu-id="0e8fc-123">ADFS sunucunuzda aşağıdaki komutu kullanarak, kullanıcıların Self Servis parola girmesini sağlayan ADFS oturum açma sayfasına bir bağlantı iş akışı doğrudan sıfırlama ekler.</span><span class="sxs-lookup"><span data-stu-id="0e8fc-123">Using the command that follows on your ADFS server adds a link to the ADFS login page allowing users to enter the self-service password reset workflow directly.</span></span>

``` Set-ADFSGlobalWebContent -SigninPageDescriptionText "<p><A href=’https://passwordreset.microsoftonline.com’>Can’t access your account?</A></p>" ```

## <a name="customize-the-sign-in-and-access-panel-look-and-feel"></a><span data-ttu-id="0e8fc-124">Oturum açma ve erişim panelinde görünüm özelleştirme</span><span class="sxs-lookup"><span data-stu-id="0e8fc-124">Customize the sign-in and access panel look and feel</span></span>

<span data-ttu-id="0e8fc-125">Kullanıcılarınız oturum açma sayfasına eriştiğinde, şirket markanızla sığması için oturum açma sayfası görüntüsü yanı sıra görünür logosunu özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e8fc-125">When your users access the login page, you can customize the logo that appears along with the sign-in page image to fit your company branding.</span></span>

<span data-ttu-id="0e8fc-126">Bu grafik, aşağıdaki durumlarda gösterilir:</span><span class="sxs-lookup"><span data-stu-id="0e8fc-126">These graphics are shown in the following circumstances:</span></span>

* <span data-ttu-id="0e8fc-127">Sonra bir kullanıcının kullanıcı adı türleri</span><span class="sxs-lookup"><span data-stu-id="0e8fc-127">After a user types their username</span></span>
* <span data-ttu-id="0e8fc-128">Özelleştirilmiş url kullanıcının eriştiği</span><span class="sxs-lookup"><span data-stu-id="0e8fc-128">User accesses customized url</span></span>
    * <span data-ttu-id="0e8fc-129">"Ws" geçirerek parola parametresi "https://login.microsoftonline.com/?whr=contoso.com" gibi sayfa Sıfırla</span><span class="sxs-lookup"><span data-stu-id="0e8fc-129">By passing the "whr" parameter to the password reset page, like "https://login.microsoftonline.com/?whr=contoso.com"</span></span>
    * <span data-ttu-id="0e8fc-130">"Username" geçirerek gibi sayfasında, parametre parolayı Sıfırla "https://login.microsoftonline.com/?username=admin@contoso.com"</span><span class="sxs-lookup"><span data-stu-id="0e8fc-130">By passing the "username" parameter to the password reset page, like "https://login.microsoftonline.com/?username=admin@contoso.com"</span></span>

### <a name="graphics-details"></a><span data-ttu-id="0e8fc-131">Grafik ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="0e8fc-131">Graphics details</span></span>

<span data-ttu-id="0e8fc-132">Aşağıdaki ayarlar, oturum açma sayfasının görsel özelliklerini değiştirmenize izin verir ve altında bulunan **Azure Active Directory**, **şirket markası**, **düzenleme şirket markası**</span><span class="sxs-lookup"><span data-stu-id="0e8fc-132">The following settings allow you to change the visual characteristics of the sign-in page and can be found under **Azure Active Directory**, **Company branding**, **Edit company branding**</span></span>

* <span data-ttu-id="0e8fc-133">Oturum açma sayfası görüntü PNG veya JPG dosya 1420 x 1200 piksel ve no olmalıdır 500KB daha büyük.</span><span class="sxs-lookup"><span data-stu-id="0e8fc-133">Sign-in page image should be a PNG or JPG file 1420x1200 pixels and no larger than 500KB.</span></span> <span data-ttu-id="0e8fc-134">En iyi sonuçlar için yaklaşık 200 KB olmasını öneririz.</span><span class="sxs-lookup"><span data-stu-id="0e8fc-134">We recommend it to be around 200 KB for best results.</span></span>
* <span data-ttu-id="0e8fc-135">Oturum açma sayfası arka plan rengi Yüksek gecikmeli bağlantılarında kullanılır ve RGB onaltılık biçiminde olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="0e8fc-135">Sign-in page background color is used when on high-latency connections and must be in the RGB hex format.</span></span>
* <span data-ttu-id="0e8fc-136">Başlık resmi, PNG veya JPG dosya 60 x 280 piksel ve no olmalıdır 10 KB'den büyük.</span><span class="sxs-lookup"><span data-stu-id="0e8fc-136">Banner image should be a PNG or JPG file 60x280 pixels and no larger than 10 KB.</span></span>
* <span data-ttu-id="0e8fc-137">Kare logo (normal açık ve koyu renkli tema) PNG veya JPG 240 x 240 (yeniden boyutlandırılabilir) 10 KB'den büyük.</span><span class="sxs-lookup"><span data-stu-id="0e8fc-137">Square logo (normal and dark theme) PNG or JPG 240x240 (resizable) no larger than 10 KB.</span></span>

### <a name="sign-in-text-options"></a><span data-ttu-id="0e8fc-138">Metin oturum açma seçenekleri</span><span class="sxs-lookup"><span data-stu-id="0e8fc-138">Sign-in text options</span></span>

<span data-ttu-id="0e8fc-139">Aşağıdaki ayarlar, oturum açma sayfası kuruluşunuza uygun metin eklemenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="0e8fc-139">The following settings allow you to add text to the sign-in page relevant to your organization.</span></span> <span data-ttu-id="0e8fc-140">Bu ayarlar altında bulunabilir **Azure Active Directory**, **şirket markası**, **düzenleme şirket markası**</span><span class="sxs-lookup"><span data-stu-id="0e8fc-140">These settings can be found under **Azure Active Directory**, **Company branding**, **Edit company branding**</span></span>

* <span data-ttu-id="0e8fc-141">**Kullanıcı adı İpucu** örnek metnini değiştirir someone@example.com bir şey ile kullanıcılarınız için daha uygun, önerilen varsayılan iç ve dış kullanıcılar desteklendiğinde bırakılması için</span><span class="sxs-lookup"><span data-stu-id="0e8fc-141">**User name hint** replaces the example text of someone@example.com with something more appropriate for your users, recommended to be left default when supporting internal and external users</span></span>
* <span data-ttu-id="0e8fc-142">**Oturum açma sayfası metni** en fazla 256 karakter uzunluğunda.</span><span class="sxs-lookup"><span data-stu-id="0e8fc-142">**Sign-in page text** is a maximum of 256 characters in length.</span></span> <span data-ttu-id="0e8fc-143">Bu metin herhangi bir yere çevrimiçi ve Windows 10 Azure AD katılım deneyimi, kullanıcıların oturum açma görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="0e8fc-143">This text appears anywhere your users login online, and in the Azure AD Join experience on Windows 10.</span></span> <span data-ttu-id="0e8fc-144">Bu metin koşullarını kullanın, yönergeler ve kullanıcılarınız için ipuçları için kullanın.</span><span class="sxs-lookup"><span data-stu-id="0e8fc-144">Use this text for terms of use, instructions, and tips for your users.</span></span> <span data-ttu-id="0e8fc-145">**Herkes herhangi bir önemli bilgi burada sağlamaz, oturum açma sayfanızı görebilirsiniz.**</span><span class="sxs-lookup"><span data-stu-id="0e8fc-145">**Anyone can see your sign-in page so do not provide any sensitive information here.**</span></span>

### <a name="keep-me-signed-in-disabled"></a><span data-ttu-id="0e8fc-146">Oturumumu açık bırak devre dışı</span><span class="sxs-lookup"><span data-stu-id="0e8fc-146">Keep me signed in disabled</span></span>

<span data-ttu-id="0e8fc-147">Seçeneğini kapatın ve bunların tarayıcı penceresini yeniden açın, oturum açmış durumda kalmak için kullanıcıların "Benim devre dışı imzalı tut" sağlar.</span><span class="sxs-lookup"><span data-stu-id="0e8fc-147">The option "Keep me signed in disabled" allows users to remain signed in when they close and reopen their browser window.</span></span> <span data-ttu-id="0e8fc-148">Bu seçenek oturum süreleri etkilemez.</span><span class="sxs-lookup"><span data-stu-id="0e8fc-148">This option does not impact session lifetimes.</span></span> <span data-ttu-id="0e8fc-149">Bu ayarı altında bulunan **Azure Active Directory > Şirket markası > Düzenle şirket markası**.</span><span class="sxs-lookup"><span data-stu-id="0e8fc-149">This setting is found under **Azure Active Directory > Company branding > Edit company branding**.</span></span>

<span data-ttu-id="0e8fc-150">SharePoint Online ve Office 2010 özelliklerinden bazıları bu kutuyu yetkisi olan kullanıcılar bir bağımlılık sahip.</span><span class="sxs-lookup"><span data-stu-id="0e8fc-150">Some features of SharePoint Online and Office 2010 have a dependency on users being able to check this box.</span></span> <span data-ttu-id="0e8fc-151">Bu seçenek gizleme, kullanıcıları ek ve beklenmeyen oturum açma komut istemlerini alabilir.</span><span class="sxs-lookup"><span data-stu-id="0e8fc-151">If you hide this option, users may get additional and unexpected sign-in prompts.</span></span>

### <a name="directory-name"></a><span data-ttu-id="0e8fc-152">Dizin adı</span><span class="sxs-lookup"><span data-stu-id="0e8fc-152">Directory name</span></span>

<span data-ttu-id="0e8fc-153">Ad özniteliği altında değiştirebilirsiniz **Azure Active Directory > Özellikler** portal ve otomatik iletişimlerde görülen bir kolay kuruluş adı göstermek için.</span><span class="sxs-lookup"><span data-stu-id="0e8fc-153">You can change the name attribute under **Azure Active Directory > Properties** to show a friendly organization name seen in the portal and automated communications.</span></span> <span data-ttu-id="0e8fc-154">Bu seçenek en izleyin formlarda otomatik e-postalar biçiminde görülebilir</span><span class="sxs-lookup"><span data-stu-id="0e8fc-154">This option is most visible in the form of automated emails in the forms that follow</span></span>

* <span data-ttu-id="0e8fc-155">E-posta "Microsoft CONTOSO tanıtım adına" kolay ad</span><span class="sxs-lookup"><span data-stu-id="0e8fc-155">Friendly name in email “Microsoft on behalf of CONTOSO demo”</span></span>
* <span data-ttu-id="0e8fc-156">E-posta "CONTOSO demo hesabı e-posta doğrulama kodu" konu satırında</span><span class="sxs-lookup"><span data-stu-id="0e8fc-156">Subject line in email “CONTOSO demo account email verification code”</span></span>

## <a name="next-steps"></a><span data-ttu-id="0e8fc-157">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0e8fc-157">Next steps</span></span>

<span data-ttu-id="0e8fc-158">Aşağıdaki bağlantılar, Azure AD kullanarak parola sıfırlama ile ilgili ek bilgiler sağlar</span><span class="sxs-lookup"><span data-stu-id="0e8fc-158">The following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="0e8fc-159">[**Hızlı Başlangıç**](active-directory-passwords-getting-started.md) - Azure AD self servis parola yönetimi ile çalışmaya hazırlanın</span><span class="sxs-lookup"><span data-stu-id="0e8fc-159">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="0e8fc-160">[**Lisanslama**](active-directory-passwords-licensing.md) - Azure AD Lisanslarınızı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="0e8fc-160">[**Licensing**](active-directory-passwords-licensing.md) - Configure your Azure AD Licensing</span></span>
* <span data-ttu-id="0e8fc-161">[**Veri**](active-directory-passwords-data.md) - Gerekli olan verileri ve parola yönetimi için nasıl kullanıldığını anlayın</span><span class="sxs-lookup"><span data-stu-id="0e8fc-161">[**Data**](active-directory-passwords-data.md) - Understand the data that is required and how it is used for password management</span></span>
* <span data-ttu-id="0e8fc-162">[**Kullanıma Sunma** ](active-directory-passwords-best-practices.md) - Buradaki yönergelerle SSPR’ı planlayın ve kullanıcılarınıza dağıtın</span><span class="sxs-lookup"><span data-stu-id="0e8fc-162">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR to your users using the guidance found here</span></span>
* <span data-ttu-id="0e8fc-163">[**İlke**](active-directory-passwords-policy.md) - Azure AD parola ilkelerini anlayın ve ayarlayın</span><span class="sxs-lookup"><span data-stu-id="0e8fc-163">[**Policy**](active-directory-passwords-policy.md) - Understand and set Azure AD password policies</span></span>
* <span data-ttu-id="0e8fc-164">[**Parola Geri Yazma**](active-directory-passwords-writeback.md) - Şirket içi dizininizde parola geri yazma özelliğinin nasıl çalıştığını anlayın</span><span class="sxs-lookup"><span data-stu-id="0e8fc-164">[**Password Writeback**](active-directory-passwords-writeback.md) - How does password writeback work with your on-premises directory</span></span>
* <span data-ttu-id="0e8fc-165">[**Raporlama**](active-directory-passwords-reporting.md) - Kullanıcılarınızın SSPR işlevine erişip erişmediğini, ne zaman ve nerede eriştiğini öğrenin</span><span class="sxs-lookup"><span data-stu-id="0e8fc-165">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="0e8fc-166">[**Teknik Ayrıntı**](active-directory-passwords-how-it-works.md) - Nasıl çalıştığını anlamak için perde arkasına gidin</span><span class="sxs-lookup"><span data-stu-id="0e8fc-166">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind the curtain to understand how it works</span></span>
* <span data-ttu-id="0e8fc-167">[**Sık Sorulan Sorular**](active-directory-passwords-faq.md) - Nasıl?</span><span class="sxs-lookup"><span data-stu-id="0e8fc-167">[**Frequently Asked Questions**](active-directory-passwords-faq.md) - How?</span></span> <span data-ttu-id="0e8fc-168">Neden?</span><span class="sxs-lookup"><span data-stu-id="0e8fc-168">Why?</span></span> <span data-ttu-id="0e8fc-169">Ne?</span><span class="sxs-lookup"><span data-stu-id="0e8fc-169">What?</span></span> <span data-ttu-id="0e8fc-170">Nerede?</span><span class="sxs-lookup"><span data-stu-id="0e8fc-170">Where?</span></span> <span data-ttu-id="0e8fc-171">Kim?</span><span class="sxs-lookup"><span data-stu-id="0e8fc-171">Who?</span></span> <span data-ttu-id="0e8fc-172">Ne zaman?</span><span class="sxs-lookup"><span data-stu-id="0e8fc-172">When?</span></span> <span data-ttu-id="0e8fc-173">- Her zaman sormak istediğiniz soruların yanıtları</span><span class="sxs-lookup"><span data-stu-id="0e8fc-173">- Answers to questions you always wanted to ask</span></span>
* <span data-ttu-id="0e8fc-174">[**Sorun giderme**](active-directory-passwords-troubleshoot.md) - SSPR ile yaygın olarak karşılaştığımız sorunların çözümü hakkında bilgi alın</span><span class="sxs-lookup"><span data-stu-id="0e8fc-174">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how to resolve common issues that we see with SSPR</span></span>

