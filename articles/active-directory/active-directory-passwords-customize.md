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
ms.openlocfilehash: 4762fffef040f9b409355f9ee0e8cc593e3eea0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-azure-ad-functionality-for-self-service-password-reset"></a><span data-ttu-id="2bcbd-103">Self Servis parola sıfırlama için Azure AD işlevselliği özelleştirme</span><span class="sxs-lookup"><span data-stu-id="2bcbd-103">Customize Azure AD functionality for Self-Service Password Reset</span></span>

<span data-ttu-id="2bcbd-104">BT uzmanları toodeploy Self Servis parola sıfırlama arayan hello deneyimi toomatch kullanıcılarının özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2bcbd-104">IT Professionals looking toodeploy self-service password reset can customize hello experience toomatch their users.</span></span>

## <a name="customize-hello-contact-your-administrator-link"></a><span data-ttu-id="2bcbd-105">Yönetici bağlantı Hello kişi özelleştirme</span><span class="sxs-lookup"><span data-stu-id="2bcbd-105">Customize hello contact your administrator link</span></span>

<span data-ttu-id="2bcbd-106">SSPR etkin kullanıcıları olsa bile hello parola hala bir "yöneticinize başvurun" bağlantısında portal sıfırlayın.</span><span class="sxs-lookup"><span data-stu-id="2bcbd-106">Even if SSPR is not enabled users still a "contact your administrator" link on hello password reset portal.</span></span>  <span data-ttu-id="2bcbd-107">Bu bağlantıyı tıklatarak hello kullanıcının parolasını değiştirme konusunda yardım almak için isteyen yöneticilerinizi e-postalar.</span><span class="sxs-lookup"><span data-stu-id="2bcbd-107">Clicking this link emails your administrators asking for assistance in changing hello user's password.</span></span> <span data-ttu-id="2bcbd-108">Bu e-posta alıcıları sırasının hello aşağıdaki toohello gönderilir:</span><span class="sxs-lookup"><span data-stu-id="2bcbd-108">This email is sent toohello following recipients in hello following order:</span></span>

1. <span data-ttu-id="2bcbd-109">Merhaba, **parola Yöneticisi** rol atanır, Yöneticiler bu rolüne sahip bildirim</span><span class="sxs-lookup"><span data-stu-id="2bcbd-109">If hello **Password administrator** role is assigned, administrators with this role are notified</span></span>
2. <span data-ttu-id="2bcbd-110">Parola yöneticileri atanır varsa, ardından hello yöneticilerine **Kullanıcı Yöneticisi** rol bildirim</span><span class="sxs-lookup"><span data-stu-id="2bcbd-110">If no Password administrators are assigned, then administrators with hello **User administrator** role are notified</span></span>
3. <span data-ttu-id="2bcbd-111">Merhaba önceki roller hiçbiri, ardından atanmış ise **genel Yöneticiler** bildirilir</span><span class="sxs-lookup"><span data-stu-id="2bcbd-111">If neither of hello previous roles were assigned, then **Global administrators** are notified</span></span>

<span data-ttu-id="2bcbd-112">Her durumda en fazla 100 alıcıların bildirim.</span><span class="sxs-lookup"><span data-stu-id="2bcbd-112">In all cases, a maximum of 100 recipients are notified.</span></span>

<span data-ttu-id="2bcbd-113">Merhaba farklı yönetici rolleri ve nasıl görebileceği tooassign hello belge hakkında daha fazla toofind [Azure Active Directory'de yönetici rolleri atama](active-directory-assign-admin-roles.md)</span><span class="sxs-lookup"><span data-stu-id="2bcbd-113">toofind out more about hello different administrator roles and how tooassign them see hello document [Assigning administrator roles in Azure Active Directory](active-directory-assign-admin-roles.md)</span></span>

### <a name="disable-contact-your-administrator-emails"></a><span data-ttu-id="2bcbd-114">Devre dışı bırakma, yönetici e-postaları başvurun</span><span class="sxs-lookup"><span data-stu-id="2bcbd-114">Disable contact your administrator emails</span></span>

<span data-ttu-id="2bcbd-115">Kuruluşunuzun parola hakkında bildirim Yöneticiler istekleri sıfırlama istemiyorsa hello aşağıdaki yapılandırma etkinleştirilebilir</span><span class="sxs-lookup"><span data-stu-id="2bcbd-115">If your organization does not want administrators notified about password reset requests, hello following configuration can be enabled</span></span>

* <span data-ttu-id="2bcbd-116">Self Servis parola sıfırlama tüm son kullanıcılarınız için etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="2bcbd-116">Enable self-service password reset for all end users.</span></span> <span data-ttu-id="2bcbd-117">Bu seçenek altındadır **parola sıfırlama > Özellikler**.</span><span class="sxs-lookup"><span data-stu-id="2bcbd-117">This option is under **Password Reset > Properties**.</span></span>
    * <span data-ttu-id="2bcbd-118">Kullanıcıların kendi parolalarını kullanıcılar tooreset istemiyorsanız erişim tooan boş grubu kapsamını belirleyebilirsiniz **bu seçeneği önermiyoruz**.</span><span class="sxs-lookup"><span data-stu-id="2bcbd-118">If you do not wish users tooreset their own passwords, you can scope access tooan empty group **we do not recommend this option**.</span></span>
* <span data-ttu-id="2bcbd-119">Web URL veya mailto Hello Yardım Masası bağlantısı tooprovide özelleştirme: adresi kullanıcılar tooget Yardım kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="2bcbd-119">Customize hello helpdesk link tooprovide a web URL or mailto: address that users can use tooget assistance.</span></span> <span data-ttu-id="2bcbd-120">Bu seçenek altındadır **parola sıfırlama > özelleştirme > özel Yardım Masası e-posta veya URL**.</span><span class="sxs-lookup"><span data-stu-id="2bcbd-120">This option is under **Password Reset > Customization > Custom helpdesk email or URL**.</span></span>

## <a name="customize-adfs-sign-in-page-for-sspr"></a><span data-ttu-id="2bcbd-121">SSPR için ADFS oturum açma sayfasını özelleştirme</span><span class="sxs-lookup"><span data-stu-id="2bcbd-121">Customize ADFS sign-in page for SSPR</span></span>

<span data-ttu-id="2bcbd-122">ADFS Yöneticiler hello makalede bulunan hello kılavuzu kullanarak bir bağlantıyı tootheir oturum açma sayfası ekleyebilirsiniz [Ekle oturum açma sayfası açıklaması](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/add-sign-in-page-description).</span><span class="sxs-lookup"><span data-stu-id="2bcbd-122">ADFS Administrators can add a link tootheir sign-in page using hello guidance found in hello article [Add sign-in page description](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/add-sign-in-page-description).</span></span>

<span data-ttu-id="2bcbd-123">ADFS sunucunuzda aşağıdaki hello komutunu kullanarak kullanıcıların tooenter hello Self Servis parola sıfırlama iş akışı doğrudan sağlayan bir bağlantı toohello ADFS oturum açma sayfasına ekler.</span><span class="sxs-lookup"><span data-stu-id="2bcbd-123">Using hello command that follows on your ADFS server adds a link toohello ADFS login page allowing users tooenter hello self-service password reset workflow directly.</span></span>

``` Set-ADFSGlobalWebContent -SigninPageDescriptionText "<p><A href=’https://passwordreset.microsoftonline.com’>Can’t access your account?</A></p>" ```

## <a name="customize-hello-sign-in-and-access-panel-look-and-feel"></a><span data-ttu-id="2bcbd-124">Merhaba oturum açma ve erişim panelinde görünüm özelleştirme</span><span class="sxs-lookup"><span data-stu-id="2bcbd-124">Customize hello sign-in and access panel look and feel</span></span>

<span data-ttu-id="2bcbd-125">Kullanıcılarınızın hello oturum açma sayfasına eriştiğinizde, şirket markanızla hello oturum açma sayfası görüntü toofit yanı sıra görünür hello logosu özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2bcbd-125">When your users access hello login page, you can customize hello logo that appears along with hello sign-in page image toofit your company branding.</span></span>

<span data-ttu-id="2bcbd-126">Bu grafik koşullar aşağıdaki hello gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="2bcbd-126">These graphics are shown in hello following circumstances:</span></span>

* <span data-ttu-id="2bcbd-127">Sonra bir kullanıcının kullanıcı adı türleri</span><span class="sxs-lookup"><span data-stu-id="2bcbd-127">After a user types their username</span></span>
* <span data-ttu-id="2bcbd-128">Özelleştirilmiş url kullanıcının eriştiği</span><span class="sxs-lookup"><span data-stu-id="2bcbd-128">User accesses customized url</span></span>
    * <span data-ttu-id="2bcbd-129">Geçirme hello tarafından sayfası "https://login.microsoftonline.com/?whr=contoso.com" gibi "ws" parametresi toohello parola sıfırlama</span><span class="sxs-lookup"><span data-stu-id="2bcbd-129">By passing hello "whr" parameter toohello password reset page, like "https://login.microsoftonline.com/?whr=contoso.com"</span></span>
    * <span data-ttu-id="2bcbd-130">Gibi sayfa, "kullanıcıadı" Merhaba tarafından geçirme parametresi toohello parola sıfırlama "https://login.microsoftonline.com/?username=admin@contoso.com"</span><span class="sxs-lookup"><span data-stu-id="2bcbd-130">By passing hello "username" parameter toohello password reset page, like "https://login.microsoftonline.com/?username=admin@contoso.com"</span></span>

### <a name="graphics-details"></a><span data-ttu-id="2bcbd-131">Grafik ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="2bcbd-131">Graphics details</span></span>

<span data-ttu-id="2bcbd-132">Merhaba aşağıdaki ayarları toochange hello görsel özelliklerini hello oturum açma sayfasının izin ve altında bulunan **Azure Active Directory**, **şirket markası**, **şirket Düzenle Markalama**</span><span class="sxs-lookup"><span data-stu-id="2bcbd-132">hello following settings allow you toochange hello visual characteristics of hello sign-in page and can be found under **Azure Active Directory**, **Company branding**, **Edit company branding**</span></span>

* <span data-ttu-id="2bcbd-133">Oturum açma sayfası görüntü PNG veya JPG dosya 1420 x 1200 piksel ve no olmalıdır 500KB daha büyük.</span><span class="sxs-lookup"><span data-stu-id="2bcbd-133">Sign-in page image should be a PNG or JPG file 1420x1200 pixels and no larger than 500KB.</span></span> <span data-ttu-id="2bcbd-134">Bu toobe yaklaşık 200 KB en iyi sonuçlar için öneririz.</span><span class="sxs-lookup"><span data-stu-id="2bcbd-134">We recommend it toobe around 200 KB for best results.</span></span>
* <span data-ttu-id="2bcbd-135">Oturum açma sayfası arka plan rengi Yüksek gecikmeli bağlantılarında kullanılır ve hello RGB onaltılık biçiminde olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="2bcbd-135">Sign-in page background color is used when on high-latency connections and must be in hello RGB hex format.</span></span>
* <span data-ttu-id="2bcbd-136">Başlık resmi, PNG veya JPG dosya 60 x 280 piksel ve no olmalıdır 10 KB'den büyük.</span><span class="sxs-lookup"><span data-stu-id="2bcbd-136">Banner image should be a PNG or JPG file 60x280 pixels and no larger than 10 KB.</span></span>
* <span data-ttu-id="2bcbd-137">Kare logo (normal açık ve koyu renkli tema) PNG veya JPG 240 x 240 (yeniden boyutlandırılabilir) 10 KB'den büyük.</span><span class="sxs-lookup"><span data-stu-id="2bcbd-137">Square logo (normal and dark theme) PNG or JPG 240x240 (resizable) no larger than 10 KB.</span></span>

### <a name="sign-in-text-options"></a><span data-ttu-id="2bcbd-138">Metin oturum açma seçenekleri</span><span class="sxs-lookup"><span data-stu-id="2bcbd-138">Sign-in text options</span></span>

<span data-ttu-id="2bcbd-139">ayarları aşağıdaki hello tooadd metin toohello oturum açma sayfasında ilgili tooyour kuruluş izin verin.</span><span class="sxs-lookup"><span data-stu-id="2bcbd-139">hello following settings allow you tooadd text toohello sign-in page relevant tooyour organization.</span></span> <span data-ttu-id="2bcbd-140">Bu ayarlar altında bulunabilir **Azure Active Directory**, **şirket markası**, **düzenleme şirket markası**</span><span class="sxs-lookup"><span data-stu-id="2bcbd-140">These settings can be found under **Azure Active Directory**, **Company branding**, **Edit company branding**</span></span>

* <span data-ttu-id="2bcbd-141">**Kullanıcı adı İpucu** değiştirir hello örnek metnin someone@example.com bir şey ile kullanıcılarınız için daha uygun, iç ve dış kullanıcılar desteklendiğinde toobe sol varsayılan önerilir</span><span class="sxs-lookup"><span data-stu-id="2bcbd-141">**User name hint** replaces hello example text of someone@example.com with something more appropriate for your users, recommended toobe left default when supporting internal and external users</span></span>
* <span data-ttu-id="2bcbd-142">**Oturum açma sayfası metni** en fazla 256 karakter uzunluğunda.</span><span class="sxs-lookup"><span data-stu-id="2bcbd-142">**Sign-in page text** is a maximum of 256 characters in length.</span></span> <span data-ttu-id="2bcbd-143">Bu metin, kullanıcıların oturum açma çevrimiçi ve hello Azure AD katılım deneyimi Windows 10 herhangi bir yerde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="2bcbd-143">This text appears anywhere your users login online, and in hello Azure AD Join experience on Windows 10.</span></span> <span data-ttu-id="2bcbd-144">Bu metin koşullarını kullanın, yönergeler ve kullanıcılarınız için ipuçları için kullanın.</span><span class="sxs-lookup"><span data-stu-id="2bcbd-144">Use this text for terms of use, instructions, and tips for your users.</span></span> <span data-ttu-id="2bcbd-145">**Herkes herhangi bir önemli bilgi burada sağlamaz, oturum açma sayfanızı görebilirsiniz.**</span><span class="sxs-lookup"><span data-stu-id="2bcbd-145">**Anyone can see your sign-in page so do not provide any sensitive information here.**</span></span>

### <a name="keep-me-signed-in-disabled"></a><span data-ttu-id="2bcbd-146">Oturumumu açık bırak devre dışı</span><span class="sxs-lookup"><span data-stu-id="2bcbd-146">Keep me signed in disabled</span></span>

<span data-ttu-id="2bcbd-147">Merhaba seçeneği "tutmak Oturumumu açık devre dışı" kullanıcılar tooremain kapatın ve bunların tarayıcı penceresini yeniden açın, oturum sağlar.</span><span class="sxs-lookup"><span data-stu-id="2bcbd-147">hello option "Keep me signed in disabled" allows users tooremain signed in when they close and reopen their browser window.</span></span> <span data-ttu-id="2bcbd-148">Bu seçenek oturum süreleri etkilemez.</span><span class="sxs-lookup"><span data-stu-id="2bcbd-148">This option does not impact session lifetimes.</span></span> <span data-ttu-id="2bcbd-149">Bu ayarı altında bulunan **Azure Active Directory > Şirket markası > Düzenle şirket markası**.</span><span class="sxs-lookup"><span data-stu-id="2bcbd-149">This setting is found under **Azure Active Directory > Company branding > Edit company branding**.</span></span>

<span data-ttu-id="2bcbd-150">SharePoint Online ve Office 2010 özelliklerinden bazıları mümkün toocheck bu kutu olan kullanıcılar bir bağımlılık vardır.</span><span class="sxs-lookup"><span data-stu-id="2bcbd-150">Some features of SharePoint Online and Office 2010 have a dependency on users being able toocheck this box.</span></span> <span data-ttu-id="2bcbd-151">Bu seçenek gizleme, kullanıcıları ek ve beklenmeyen oturum açma komut istemlerini alabilir.</span><span class="sxs-lookup"><span data-stu-id="2bcbd-151">If you hide this option, users may get additional and unexpected sign-in prompts.</span></span>

### <a name="directory-name"></a><span data-ttu-id="2bcbd-152">Dizin adı</span><span class="sxs-lookup"><span data-stu-id="2bcbd-152">Directory name</span></span>

<span data-ttu-id="2bcbd-153">Merhaba name özniteliği altında değiştirebilirsiniz **Azure Active Directory > Özellikler** tooshow kolay kuruluş adı hello Portalı'nda görülen ve iletişim otomatik.</span><span class="sxs-lookup"><span data-stu-id="2bcbd-153">You can change hello name attribute under **Azure Active Directory > Properties** tooshow a friendly organization name seen in hello portal and automated communications.</span></span> <span data-ttu-id="2bcbd-154">Bu seçenek en izleyin hello formlarda otomatik e-postalar hello biçiminde görülebilir</span><span class="sxs-lookup"><span data-stu-id="2bcbd-154">This option is most visible in hello form of automated emails in hello forms that follow</span></span>

* <span data-ttu-id="2bcbd-155">E-posta "Microsoft CONTOSO tanıtım adına" kolay ad</span><span class="sxs-lookup"><span data-stu-id="2bcbd-155">Friendly name in email “Microsoft on behalf of CONTOSO demo”</span></span>
* <span data-ttu-id="2bcbd-156">E-posta "CONTOSO demo hesabı e-posta doğrulama kodu" konu satırında</span><span class="sxs-lookup"><span data-stu-id="2bcbd-156">Subject line in email “CONTOSO demo account email verification code”</span></span>

## <a name="next-steps"></a><span data-ttu-id="2bcbd-157">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2bcbd-157">Next steps</span></span>

<span data-ttu-id="2bcbd-158">bağlantılar aşağıdaki hello parola sıfırlama ve Azure AD kullanma ile ilgili ek bilgiler sağlar</span><span class="sxs-lookup"><span data-stu-id="2bcbd-158">hello following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="2bcbd-159">[**Hızlı Başlangıç**](active-directory-passwords-getting-started.md) - Azure AD self servis parola yönetimi ile çalışmaya hazırlanın</span><span class="sxs-lookup"><span data-stu-id="2bcbd-159">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="2bcbd-160">[**Lisanslama**](active-directory-passwords-licensing.md) - Azure AD Lisanslarınızı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="2bcbd-160">[**Licensing**](active-directory-passwords-licensing.md) - Configure your Azure AD Licensing</span></span>
* <span data-ttu-id="2bcbd-161">[**Veri** ](active-directory-passwords-data.md) - gereklidir hello verileri anlamak ve nasıl kullanıldığı için parola yönetimi</span><span class="sxs-lookup"><span data-stu-id="2bcbd-161">[**Data**](active-directory-passwords-data.md) - Understand hello data that is required and how it is used for password management</span></span>
* <span data-ttu-id="2bcbd-162">[**Sunum** ](active-directory-passwords-best-practices.md) -planlama ve burada bulunan hello kılavuzu kullanarak SSPR tooyour kullanıcılara dağıtma</span><span class="sxs-lookup"><span data-stu-id="2bcbd-162">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR tooyour users using hello guidance found here</span></span>
* <span data-ttu-id="2bcbd-163">[**İlke**](active-directory-passwords-policy.md) - Azure AD parola ilkelerini anlayın ve ayarlayın</span><span class="sxs-lookup"><span data-stu-id="2bcbd-163">[**Policy**](active-directory-passwords-policy.md) - Understand and set Azure AD password policies</span></span>
* <span data-ttu-id="2bcbd-164">[**Parola Geri Yazma**](active-directory-passwords-writeback.md) - Şirket içi dizininizde parola geri yazma özelliğinin nasıl çalıştığını anlayın</span><span class="sxs-lookup"><span data-stu-id="2bcbd-164">[**Password Writeback**](active-directory-passwords-writeback.md) - How does password writeback work with your on-premises directory</span></span>
* <span data-ttu-id="2bcbd-165">[**Raporlama**](active-directory-passwords-reporting.md) - Kullanıcılarınızın SSPR işlevine erişip erişmediğini, ne zaman ve nerede eriştiğini öğrenin</span><span class="sxs-lookup"><span data-stu-id="2bcbd-165">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="2bcbd-166">[**Teknik derinlemesine** ](active-directory-passwords-how-it-works.md) -hello perdenin toounderstand nasıl çalıştığını gidin</span><span class="sxs-lookup"><span data-stu-id="2bcbd-166">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind hello curtain toounderstand how it works</span></span>
* <span data-ttu-id="2bcbd-167">[**Sık Sorulan Sorular**](active-directory-passwords-faq.md) - Nasıl?</span><span class="sxs-lookup"><span data-stu-id="2bcbd-167">[**Frequently Asked Questions**](active-directory-passwords-faq.md) - How?</span></span> <span data-ttu-id="2bcbd-168">Neden?</span><span class="sxs-lookup"><span data-stu-id="2bcbd-168">Why?</span></span> <span data-ttu-id="2bcbd-169">Ne?</span><span class="sxs-lookup"><span data-stu-id="2bcbd-169">What?</span></span> <span data-ttu-id="2bcbd-170">Nerede?</span><span class="sxs-lookup"><span data-stu-id="2bcbd-170">Where?</span></span> <span data-ttu-id="2bcbd-171">Kim?</span><span class="sxs-lookup"><span data-stu-id="2bcbd-171">Who?</span></span> <span data-ttu-id="2bcbd-172">Ne zaman?</span><span class="sxs-lookup"><span data-stu-id="2bcbd-172">When?</span></span> <span data-ttu-id="2bcbd-173">-Her zaman tooask istediğinizi tooquestions yanıtlar</span><span class="sxs-lookup"><span data-stu-id="2bcbd-173">- Answers tooquestions you always wanted tooask</span></span>
* <span data-ttu-id="2bcbd-174">[**Sorun giderme** ](active-directory-passwords-troubleshoot.md) -nasıl biz SSPR ile bkz tooresolve ortak sorunları öğrenin</span><span class="sxs-lookup"><span data-stu-id="2bcbd-174">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how tooresolve common issues that we see with SSPR</span></span>

