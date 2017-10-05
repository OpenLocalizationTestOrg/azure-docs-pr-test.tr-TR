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
# <a name="customize-azure-ad-functionality-for-self-service-password-reset"></a>Self Servis parola sıfırlama için Azure AD işlevselliği özelleştirme

Self Servis parola sıfırlama dağıtmak isteyen BT uzmanları, kullanıcıları eşleştirmek için deneyimi özelleştirebilirsiniz.

## <a name="customize-the-contact-your-administrator-link"></a>Kişinin yöneticisine bağlantınız özelleştirme

SSPR etkinleştirilmemiş olsa bile kullanıcılar hala bir "yöneticinize başvurun" parola bağlantı portal sıfırlayın.  Bu bağlantıyı tıklatarak kullanıcının parolasını değiştirme konusunda yardım almak için isteyen yöneticilerinizi e-postalar. Bu e-posta aşağıdaki sırayla aşağıdaki alıcılara gönderilir:

1. Varsa **parola Yöneticisi** rol atanır, Yöneticiler bu rolüne sahip bildirim
2. Parola yöneticileri atanır varsa, ardından yöneticilerine **Kullanıcı Yöneticisi** rol bildirim
3. Önceki roller hiçbiri, ardından atanmış ise **genel Yöneticiler** bildirilir

Her durumda en fazla 100 alıcıların bildirim.

Farklı yönetici hakkında daha fazla bilgi için roller ve bunları atama belgesine bakın [Azure Active Directory'de yönetici rolleri atama](active-directory-assign-admin-roles.md)

### <a name="disable-contact-your-administrator-emails"></a>Devre dışı bırakma, yönetici e-postaları başvurun

Kuruluşunuzun parola hakkında bildirim Yöneticiler istekleri sıfırlama istemiyorsa aşağıdaki yapılandırma etkinleştirilebilir

* Self Servis parola sıfırlama tüm son kullanıcılarınız için etkinleştirin. Bu seçenek altındadır **parola sıfırlama > Özellikler**.
    * Kullanıcıların kendi parolalarını sıfırlamasına izin istemezseniz, boş bir grubu erişim kapsamını belirleyebilirsiniz **bu seçeneği önermiyoruz**.
* Bir web URL'si veya mailto sağlamak için Yardım Masası bağlantısı özelleştirme: kullanıcıların Yardım almak için kullanabileceği adresi. Bu seçenek altındadır **parola sıfırlama > özelleştirme > özel Yardım Masası e-posta veya URL**.

## <a name="customize-adfs-sign-in-page-for-sspr"></a>SSPR için ADFS oturum açma sayfasını özelleştirme

ADFS Yöneticiler makalede bulunan yönergeleri kullanarak kullanıcıların oturum açma sayfasına bir bağlantı ekleyebilirsiniz [Ekle oturum açma sayfası açıklaması](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/add-sign-in-page-description).

ADFS sunucunuzda aşağıdaki komutu kullanarak, kullanıcıların Self Servis parola girmesini sağlayan ADFS oturum açma sayfasına bir bağlantı iş akışı doğrudan sıfırlama ekler.

``` Set-ADFSGlobalWebContent -SigninPageDescriptionText "<p><A href=’https://passwordreset.microsoftonline.com’>Can’t access your account?</A></p>" ```

## <a name="customize-the-sign-in-and-access-panel-look-and-feel"></a>Oturum açma ve erişim panelinde görünüm özelleştirme

Kullanıcılarınız oturum açma sayfasına eriştiğinde, şirket markanızla sığması için oturum açma sayfası görüntüsü yanı sıra görünür logosunu özelleştirebilirsiniz.

Bu grafik, aşağıdaki durumlarda gösterilir:

* Sonra bir kullanıcının kullanıcı adı türleri
* Özelleştirilmiş url kullanıcının eriştiği
    * "Ws" geçirerek parola parametresi "https://login.microsoftonline.com/?whr=contoso.com" gibi sayfa Sıfırla
    * "Username" geçirerek gibi sayfasında, parametre parolayı Sıfırla "https://login.microsoftonline.com/?username=admin@contoso.com"

### <a name="graphics-details"></a>Grafik ayrıntıları

Aşağıdaki ayarlar, oturum açma sayfasının görsel özelliklerini değiştirmenize izin verir ve altında bulunan **Azure Active Directory**, **şirket markası**, **düzenleme şirket markası**

* Oturum açma sayfası görüntü PNG veya JPG dosya 1420 x 1200 piksel ve no olmalıdır 500KB daha büyük. En iyi sonuçlar için yaklaşık 200 KB olmasını öneririz.
* Oturum açma sayfası arka plan rengi Yüksek gecikmeli bağlantılarında kullanılır ve RGB onaltılık biçiminde olması gerekir.
* Başlık resmi, PNG veya JPG dosya 60 x 280 piksel ve no olmalıdır 10 KB'den büyük.
* Kare logo (normal açık ve koyu renkli tema) PNG veya JPG 240 x 240 (yeniden boyutlandırılabilir) 10 KB'den büyük.

### <a name="sign-in-text-options"></a>Metin oturum açma seçenekleri

Aşağıdaki ayarlar, oturum açma sayfası kuruluşunuza uygun metin eklemenize olanak sağlar. Bu ayarlar altında bulunabilir **Azure Active Directory**, **şirket markası**, **düzenleme şirket markası**

* **Kullanıcı adı İpucu** örnek metnini değiştirir someone@example.com bir şey ile kullanıcılarınız için daha uygun, önerilen varsayılan iç ve dış kullanıcılar desteklendiğinde bırakılması için
* **Oturum açma sayfası metni** en fazla 256 karakter uzunluğunda. Bu metin herhangi bir yere çevrimiçi ve Windows 10 Azure AD katılım deneyimi, kullanıcıların oturum açma görüntülenir. Bu metin koşullarını kullanın, yönergeler ve kullanıcılarınız için ipuçları için kullanın. **Herkes herhangi bir önemli bilgi burada sağlamaz, oturum açma sayfanızı görebilirsiniz.**

### <a name="keep-me-signed-in-disabled"></a>Oturumumu açık bırak devre dışı

Seçeneğini kapatın ve bunların tarayıcı penceresini yeniden açın, oturum açmış durumda kalmak için kullanıcıların "Benim devre dışı imzalı tut" sağlar. Bu seçenek oturum süreleri etkilemez. Bu ayarı altında bulunan **Azure Active Directory > Şirket markası > Düzenle şirket markası**.

SharePoint Online ve Office 2010 özelliklerinden bazıları bu kutuyu yetkisi olan kullanıcılar bir bağımlılık sahip. Bu seçenek gizleme, kullanıcıları ek ve beklenmeyen oturum açma komut istemlerini alabilir.

### <a name="directory-name"></a>Dizin adı

Ad özniteliği altında değiştirebilirsiniz **Azure Active Directory > Özellikler** portal ve otomatik iletişimlerde görülen bir kolay kuruluş adı göstermek için. Bu seçenek en izleyin formlarda otomatik e-postalar biçiminde görülebilir

* E-posta "Microsoft CONTOSO tanıtım adına" kolay ad
* E-posta "CONTOSO demo hesabı e-posta doğrulama kodu" konu satırında

## <a name="next-steps"></a>Sonraki adımlar

Aşağıdaki bağlantılar, Azure AD kullanarak parola sıfırlama ile ilgili ek bilgiler sağlar

* [**Hızlı Başlangıç**](active-directory-passwords-getting-started.md) - Azure AD self servis parola yönetimi ile çalışmaya hazırlanın 
* [**Lisanslama**](active-directory-passwords-licensing.md) - Azure AD Lisanslarınızı yapılandırın
* [**Veri**](active-directory-passwords-data.md) - Gerekli olan verileri ve parola yönetimi için nasıl kullanıldığını anlayın
* [**Kullanıma Sunma** ](active-directory-passwords-best-practices.md) - Buradaki yönergelerle SSPR’ı planlayın ve kullanıcılarınıza dağıtın
* [**İlke**](active-directory-passwords-policy.md) - Azure AD parola ilkelerini anlayın ve ayarlayın
* [**Parola Geri Yazma**](active-directory-passwords-writeback.md) - Şirket içi dizininizde parola geri yazma özelliğinin nasıl çalıştığını anlayın
* [**Raporlama**](active-directory-passwords-reporting.md) - Kullanıcılarınızın SSPR işlevine erişip erişmediğini, ne zaman ve nerede eriştiğini öğrenin
* [**Teknik Ayrıntı**](active-directory-passwords-how-it-works.md) - Nasıl çalıştığını anlamak için perde arkasına gidin
* [**Sık Sorulan Sorular**](active-directory-passwords-faq.md) - Nasıl? Neden? Ne? Nerede? Kim? Ne zaman? - Her zaman sormak istediğiniz soruların yanıtları
* [**Sorun giderme**](active-directory-passwords-troubleshoot.md) - SSPR ile yaygın olarak karşılaştığımız sorunların çözümü hakkında bilgi alın

