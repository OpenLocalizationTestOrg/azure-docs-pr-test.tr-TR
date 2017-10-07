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
# <a name="customize-azure-ad-functionality-for-self-service-password-reset"></a>Self Servis parola sıfırlama için Azure AD işlevselliği özelleştirme

BT uzmanları toodeploy Self Servis parola sıfırlama arayan hello deneyimi toomatch kullanıcılarının özelleştirebilirsiniz.

## <a name="customize-hello-contact-your-administrator-link"></a>Yönetici bağlantı Hello kişi özelleştirme

SSPR etkin kullanıcıları olsa bile hello parola hala bir "yöneticinize başvurun" bağlantısında portal sıfırlayın.  Bu bağlantıyı tıklatarak hello kullanıcının parolasını değiştirme konusunda yardım almak için isteyen yöneticilerinizi e-postalar. Bu e-posta alıcıları sırasının hello aşağıdaki toohello gönderilir:

1. Merhaba, **parola Yöneticisi** rol atanır, Yöneticiler bu rolüne sahip bildirim
2. Parola yöneticileri atanır varsa, ardından hello yöneticilerine **Kullanıcı Yöneticisi** rol bildirim
3. Merhaba önceki roller hiçbiri, ardından atanmış ise **genel Yöneticiler** bildirilir

Her durumda en fazla 100 alıcıların bildirim.

Merhaba farklı yönetici rolleri ve nasıl görebileceği tooassign hello belge hakkında daha fazla toofind [Azure Active Directory'de yönetici rolleri atama](active-directory-assign-admin-roles.md)

### <a name="disable-contact-your-administrator-emails"></a>Devre dışı bırakma, yönetici e-postaları başvurun

Kuruluşunuzun parola hakkında bildirim Yöneticiler istekleri sıfırlama istemiyorsa hello aşağıdaki yapılandırma etkinleştirilebilir

* Self Servis parola sıfırlama tüm son kullanıcılarınız için etkinleştirin. Bu seçenek altındadır **parola sıfırlama > Özellikler**.
    * Kullanıcıların kendi parolalarını kullanıcılar tooreset istemiyorsanız erişim tooan boş grubu kapsamını belirleyebilirsiniz **bu seçeneği önermiyoruz**.
* Web URL veya mailto Hello Yardım Masası bağlantısı tooprovide özelleştirme: adresi kullanıcılar tooget Yardım kullanabilir. Bu seçenek altındadır **parola sıfırlama > özelleştirme > özel Yardım Masası e-posta veya URL**.

## <a name="customize-adfs-sign-in-page-for-sspr"></a>SSPR için ADFS oturum açma sayfasını özelleştirme

ADFS Yöneticiler hello makalede bulunan hello kılavuzu kullanarak bir bağlantıyı tootheir oturum açma sayfası ekleyebilirsiniz [Ekle oturum açma sayfası açıklaması](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/add-sign-in-page-description).

ADFS sunucunuzda aşağıdaki hello komutunu kullanarak kullanıcıların tooenter hello Self Servis parola sıfırlama iş akışı doğrudan sağlayan bir bağlantı toohello ADFS oturum açma sayfasına ekler.

``` Set-ADFSGlobalWebContent -SigninPageDescriptionText "<p><A href=’https://passwordreset.microsoftonline.com’>Can’t access your account?</A></p>" ```

## <a name="customize-hello-sign-in-and-access-panel-look-and-feel"></a>Merhaba oturum açma ve erişim panelinde görünüm özelleştirme

Kullanıcılarınızın hello oturum açma sayfasına eriştiğinizde, şirket markanızla hello oturum açma sayfası görüntü toofit yanı sıra görünür hello logosu özelleştirebilirsiniz.

Bu grafik koşullar aşağıdaki hello gösterilmektedir:

* Sonra bir kullanıcının kullanıcı adı türleri
* Özelleştirilmiş url kullanıcının eriştiği
    * Geçirme hello tarafından sayfası "https://login.microsoftonline.com/?whr=contoso.com" gibi "ws" parametresi toohello parola sıfırlama
    * Gibi sayfa, "kullanıcıadı" Merhaba tarafından geçirme parametresi toohello parola sıfırlama "https://login.microsoftonline.com/?username=admin@contoso.com"

### <a name="graphics-details"></a>Grafik ayrıntıları

Merhaba aşağıdaki ayarları toochange hello görsel özelliklerini hello oturum açma sayfasının izin ve altında bulunan **Azure Active Directory**, **şirket markası**, **şirket Düzenle Markalama**

* Oturum açma sayfası görüntü PNG veya JPG dosya 1420 x 1200 piksel ve no olmalıdır 500KB daha büyük. Bu toobe yaklaşık 200 KB en iyi sonuçlar için öneririz.
* Oturum açma sayfası arka plan rengi Yüksek gecikmeli bağlantılarında kullanılır ve hello RGB onaltılık biçiminde olması gerekir.
* Başlık resmi, PNG veya JPG dosya 60 x 280 piksel ve no olmalıdır 10 KB'den büyük.
* Kare logo (normal açık ve koyu renkli tema) PNG veya JPG 240 x 240 (yeniden boyutlandırılabilir) 10 KB'den büyük.

### <a name="sign-in-text-options"></a>Metin oturum açma seçenekleri

ayarları aşağıdaki hello tooadd metin toohello oturum açma sayfasında ilgili tooyour kuruluş izin verin. Bu ayarlar altında bulunabilir **Azure Active Directory**, **şirket markası**, **düzenleme şirket markası**

* **Kullanıcı adı İpucu** değiştirir hello örnek metnin someone@example.com bir şey ile kullanıcılarınız için daha uygun, iç ve dış kullanıcılar desteklendiğinde toobe sol varsayılan önerilir
* **Oturum açma sayfası metni** en fazla 256 karakter uzunluğunda. Bu metin, kullanıcıların oturum açma çevrimiçi ve hello Azure AD katılım deneyimi Windows 10 herhangi bir yerde görüntülenir. Bu metin koşullarını kullanın, yönergeler ve kullanıcılarınız için ipuçları için kullanın. **Herkes herhangi bir önemli bilgi burada sağlamaz, oturum açma sayfanızı görebilirsiniz.**

### <a name="keep-me-signed-in-disabled"></a>Oturumumu açık bırak devre dışı

Merhaba seçeneği "tutmak Oturumumu açık devre dışı" kullanıcılar tooremain kapatın ve bunların tarayıcı penceresini yeniden açın, oturum sağlar. Bu seçenek oturum süreleri etkilemez. Bu ayarı altında bulunan **Azure Active Directory > Şirket markası > Düzenle şirket markası**.

SharePoint Online ve Office 2010 özelliklerinden bazıları mümkün toocheck bu kutu olan kullanıcılar bir bağımlılık vardır. Bu seçenek gizleme, kullanıcıları ek ve beklenmeyen oturum açma komut istemlerini alabilir.

### <a name="directory-name"></a>Dizin adı

Merhaba name özniteliği altında değiştirebilirsiniz **Azure Active Directory > Özellikler** tooshow kolay kuruluş adı hello Portalı'nda görülen ve iletişim otomatik. Bu seçenek en izleyin hello formlarda otomatik e-postalar hello biçiminde görülebilir

* E-posta "Microsoft CONTOSO tanıtım adına" kolay ad
* E-posta "CONTOSO demo hesabı e-posta doğrulama kodu" konu satırında

## <a name="next-steps"></a>Sonraki adımlar

bağlantılar aşağıdaki hello parola sıfırlama ve Azure AD kullanma ile ilgili ek bilgiler sağlar

* [**Hızlı Başlangıç**](active-directory-passwords-getting-started.md) - Azure AD self servis parola yönetimi ile çalışmaya hazırlanın 
* [**Lisanslama**](active-directory-passwords-licensing.md) - Azure AD Lisanslarınızı yapılandırın
* [**Veri** ](active-directory-passwords-data.md) - gereklidir hello verileri anlamak ve nasıl kullanıldığı için parola yönetimi
* [**Sunum** ](active-directory-passwords-best-practices.md) -planlama ve burada bulunan hello kılavuzu kullanarak SSPR tooyour kullanıcılara dağıtma
* [**İlke**](active-directory-passwords-policy.md) - Azure AD parola ilkelerini anlayın ve ayarlayın
* [**Parola Geri Yazma**](active-directory-passwords-writeback.md) - Şirket içi dizininizde parola geri yazma özelliğinin nasıl çalıştığını anlayın
* [**Raporlama**](active-directory-passwords-reporting.md) - Kullanıcılarınızın SSPR işlevine erişip erişmediğini, ne zaman ve nerede eriştiğini öğrenin
* [**Teknik derinlemesine** ](active-directory-passwords-how-it-works.md) -hello perdenin toounderstand nasıl çalıştığını gidin
* [**Sık Sorulan Sorular**](active-directory-passwords-faq.md) - Nasıl? Neden? Ne? Nerede? Kim? Ne zaman? -Her zaman tooask istediğinizi tooquestions yanıtlar
* [**Sorun giderme** ](active-directory-passwords-troubleshoot.md) -nasıl biz SSPR ile bkz tooresolve ortak sorunları öğrenin

