---
title: "Parola tek oturum açma için Galeri olmayan uygulama yapılandırma aaaProblem | Microsoft Docs"
description: "Parola tek oturum açma için listelenmeyen Özel Galeri olmayan uygulamaları hello Azure AD uygulama galerisinde yapılandırırken Hello ortak sorunları kişiler yüz anlama"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 3aee0a4c525bb3da338da2da0882ec572cf0e5e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-password-single-sign-on-for-a-non-gallery-application"></a>Parola tek oturum açma için Galeri olmayan uygulama yapılandırma sorunu

Bu makalede yardımcı toounderstand hello ortak sorunları kişiler yüz yapılandırırken **parola çoklu oturum açma** bir galeri olmayan uygulama ile.

## <a name="how-toocapture-sign-in-fields-for-an-application"></a>Nasıl toocapture oturum açma için uygulama alanları

Oturum açma alan yakalama HTML etkin oturum açma sayfaları için yalnızca desteklenir ve olduğu **için standart olmayan oturum açma sayfaları desteklenmeyen**, Flash, veya diğer HTML etkin olmayan teknolojileri kullananlar ister.

Özel uygulamalarınız için oturum açma alanları yakalamak için iki yolu vardır:

-   Otomatik oturum açma alan yakalama

-   Oturum açma el ile alan yakalama

**Otomatik oturum açma alan yakalama** kullanıyorlarsa iyi çoğu HTML etkin oturum açma sayfaları ile çalışır **hello kullanıcı adı ve parola girişi için iyi bilinen DIV kimlikleri** alan. Bu çalışır hello değiştirilene hello HTML hello sayfa toofind belirli ölçütlere uyan DIV kimlikleri üzerinde ve parolaları tooit daha sonra yeniden şekilde bu uygulama için bu meta veri kaydetme tarafından yoludur.

**Oturum açma el ile alan yakalama** uygulama hello hello durumda kullanılabilir **satıcı etiket değil** hello giriş oturum açmak için kullanılan alanları. Oturum açma el ile alan yakalama hello durumda hello olduğunda da kullanılabilir **satıcı işler birden çok alan** , otomatik olarak algılanır olamaz. Merhaba üzerinde olduğu gibi birçok alan oturum açma sayfası, gibi bu alanların hello sayfasında olduğu bize sürece azure AD için veri depolayabilirsiniz.

Genel olarak, **otomatik oturum açma alan yakalama çalışmazsa, her zaman çalışırken hello el ile seçeneği öneririz.**

### <a name="how-tooautomatically-capture-sign-in-fields-for-an-application"></a>Nasıl tooautomatically yakalama alanları bir uygulama için oturum açma

tooconfigure **parola tabanlı çoklu oturum açma** kullanarak bir uygulama için **otomatik oturum açma alan yakalama**, hello adımları izleyin:

1.  Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**

2.  Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.

3.  Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.

4.  Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.

5.  Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.

  * Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**

6.  Tooconfigure çoklu oturum açma hello uygulamasını seçin.

7.  Merhaba uygulamanın yüklediği sonra hello tıklayın **çoklu oturum açma** hello uygulamanın sol taraftaki gezinti menüsünde.

8.  Select hello modu **parola tabanlı oturum açma.**

9.  Merhaba girin **oturum açma URL'si**. Bu kullanıcılar kendi kullanıcı adı ve parola toosign içinde için girdiğiniz yere hello URL'dir. **Merhaba oturum alanları sağladığınız hello URL'de görünür olduğundan emin olun**.

10. Merhaba tıklatın **kaydetmek** düğmesi.

11. Bunu, biz otomatik olarak bir kullanıcı adı için bu URL'yi scrape ve parola giriş kutusu ve izin sonra toouse Azure AD toosecurely hello erişim paneli tarayıcı uzantısı kullanarak parolaları toothat uygulaması iletme.

## <a name="how-toomanually-capture-sign-in-fields-for-an-application"></a>Nasıl toomanually yakalama alanları bir uygulama için oturum açma

toomanually yakalama oturum alanları hello erişim paneli tarayıcı uzantısı yüklü ilk olmalıdır ve **InPrivate, incognito ya da özel modunda çalışmıyor.** tooinstall hello tarayıcı uzantısı, hello adımları hello içinde [nasıl tooinstall hello erişim paneli tarayıcı uzantısı](#i-cannot-manually-detect-sign-in-fields-for-my-application) bölümü.

tooconfigure **parola tabanlı çoklu oturum açma** kullanarak bir uygulama için **oturum açma el ile alan yakalama**, hello adımları izleyin:

1.  Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**

2.  Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.

3.  Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.

4.  Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.

5.  Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.

   * Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**

6.  Tooconfigure çoklu oturum açma hello uygulamasını seçin.

7.  Merhaba uygulamanın yüklediği sonra hello tıklayın **çoklu oturum açma** hello uygulamanın sol taraftaki gezinti menüsünde.

8.  Select hello modu **parola tabanlı oturum açma.**

9.  Merhaba girin **oturum açma URL'si**. Bu kullanıcılar kendi kullanıcı adı ve parola toosign içinde için girdiğiniz yere hello URL'dir. **Merhaba oturum alanları sağladığınız hello URL'de görünür olduğundan emin olun**.

10. Merhaba tıklatın **kaydetmek** düğmesi.

11. Bunu, biz otomatik olarak bir kullanıcı adı için bu URL'yi scrape ve parola giriş kutusu ve izin sonra toouse Azure AD toosecurely hello erişim paneli tarayıcı uzantısı kullanarak parolaları toothat uygulaması iletme. Bu başarısız hello durumda cihazı **hello oturum açma modu toouse oturum açma el ile alan yakalama değiştirme** toostep 12 etmeden tarafından.

12. tıklatın **yapılandırma &lt;appname&gt; parola çoklu oturum açma ayarları**.

13. Select hello **el ile oturum açma alanları algılama** yapılandırma seçeneği.

14. **Tamam**’a tıklayın.

15. **Kaydet** düğmesine tıklayın.

16. Merhaba ekranında yönergeleri toouse hello erişim paneli izleyin.

## <a name="i-see-a-we-couldnt-find-any-sign-in-fields-at-that-url-error"></a>"Bu URL'de oturum açma alanları bulamadık" hata bakın

Oturum açma alanlarının otomatik algılama başarısız olduğunda, bu hatayı görürsünüz. Bu sorun, deneyin oturum açma el ile alan algılama aşağıdaki hello tarafından adımları hello tooresolve [nasıl toomanually yakalama alanları bir uygulama için oturum açma](#how-to-manually-capture-sign-in-fields-for-an-application) bölümü.

## <a name="i-see-an-unable-toosave-single-sign-on-configuration-error"></a>Bir "çoklu oturum açma oluşturulamıyor toosave yapılandırma" hatası bakın

Belirli nadir durumlarda, oturum açma hello tek yapılandırmasını güncelleştirme başarısız olabilir. tooresolve bu deneyin hello tek oturum açma yapılandırması yeniden kaydediliyor.

Bu toofail tutarlı bir şekilde devam ederse, destek olayı açın ve hello toplanan hello bilgilerini [nasıl toosee hello portal bildirim ayrıntılarını](#i-cannot-manually-detect-sign-in-fields-for-my-application) ve [tooget nasıl yardımcı bildirim ayrıntıları tooa göndererek Destek Mühendisi](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) bölümler.

## <a name="i-cannot-manually-detect-sign-in-fields-for-my-application"></a>I el ile oturum alanlarında Uygulamam için algılayamıyor

El ile algılama çalışmıyor açtığınızda görebilirsiniz hello davranışları bazıları şunlardır:

-   Merhaba el ile yakalama işlemi toowork görünen ancak yakalanan hello alanları doğru değildi

-   Merhaba sağ alanları hello yakalama işlemi gerçekleştirirken vurgulanmış yok

-   Merhaba yakalama işlemi bana toohello uygulamanın oturum açma sayfasına beklendiği gibi alır, ancak hiçbir şey olmaz

-   El ile yakalama toowork görünür, ancak Kullanıcılarım hello erişim paneli toohello uygulamadan gittiğinizde SSO gerçekleşmez.

Bu sorunların karşılaşırsanız hello aşağıdakileri denetleyin:

-   Merhaba erişim paneli tarayıcı uzantısı hello en son sürümüne sahip olduğunuzdan emin olun **yüklü** ve **etkin** hello hello adımları izleyerek [nasıl tooinstall hello paneli tarayıcı erişimi Uzantı](#how-to-install-the-access-panel-browser-extension) bölümü.

-   Merhaba yakalama işlemi sırasında tarayıcınızda denediğiniz değil emin olun **incognito, InPrivate ya da özel mod**. Merhaba erişim paneli uzantısı bu modda desteklenmiyor.

-   Kullanıcılarınızın panelinden hello erişim sırasında toohello uygulamada toosign ayarlamadığınızdan emin olun **incognito, InPrivate ya da özel mod**. Merhaba erişim paneli uzantısı bu modda desteklenmiyor.

-   Merhaba el ile yakalama işlemi yeniden deneyin, hello kırmızı işaretçileri alanlardır hello doğru sağlama.

-   Merhaba el ile yakalama işlemi toohang gibi görünüyor veya hello oturum açma sayfası yapmaz (durum 3 yukarıda), her şeyi hello el ile yakalama işlemi yeniden deneyin. Ancak, bu kez basın hello hello işlemi tamamladıktan sonra **F12** tooopen tarayıcınızın Geliştirici konsol düğmesi. Bir kez Merhaba, açık **konsol** ve türü **window.location= "&lt;hello oturum hello uygulama yapılandırırken belirttiğiniz URL'yi girin&gt;"** ve tuşuna basın  **Girin**. Bu sayfa zorla hello yakalama işlemi sona erdirmek ve yakalanan hello alanları depolamak yeniden yönlendir.

Bu yaklaşım hiçbiri sizin için çalışıyorsanız, size yardımcı olabilir. Merhaba ayrıntılarını ne çalıştığınız yanı sıra hello toplanan hello bilgi ile bir destek servis talebi açma [nasıl toosee hello portal bildirim ayrıntılarını](#i-cannot-manually-detect-sign-in-fields-for-my-application) ve [tooget nasıl yardımcı tooa destek bildirim ayrıntıları göndererek mühendislik](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) (varsa) bölümler.

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a>Nasıl tooinstall hello erişim paneli tarayıcı uzantısı

tooinstall hello erişim paneli tarayıcı uzantısı hello adımları izleyin:

1.  Açık hello [erişim paneli](https://myapps.microsoft.com) hello Desteklenen tarayıcılar ve oturum açma olarak birinde bir **kullanıcı** Azure ad.

2.  Tıklatın bir **parola SSO uygulaması** hello erişim paneli içinde.

3.  Hello komut istemi soran tooinstall hello yazılımda seçin **Şimdi Yükle**.

4.  Tarayıcınıza bağlı yönlendirilmiş toohello indirme bağlantısı olabilir. **Ekleme** hello uzantısı tooyour tarayıcı.

5.  Tarayıcınız isterse, tooeither seçin **etkinleştirmek** veya **izin** hello uzantısı.

6.  Bir kez yüklenir, **yeniden** tarayıcı oturumunda.

7.  Erişim paneli hello oturum açın ve, varsa görebilirsiniz **başlatma** parola SSO uygulamalarınızı.

Ayrıca hello uzantısı Chrome ve Firefox için hello doğrudan bağlantılarından aşağıdaki yükleyebilirsiniz:

-   [Chrome erişim paneli uzantısı](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [Firefox erişim paneli uzantısı](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="how-toosee-hello-details-of-a-portal-notification"></a>Nasıl bir portal bildirim toosee hello ayrıntıları

Merhaba adımları izleyerek herhangi bir portal bildirim hello ayrıntılarını görebilirsiniz:

1.  Merhaba tıklatın **bildirimleri** hello sağ üst köşesinde, hello Azure Portal (Merhaba zil) simgesi

2.  Herhangi bir bildirim seçin bir **hata** durumu (kırmızı (!) sonraki toothem sahip olanlar).

  >! DİKKAT] bildirimleri tıklatın olamaz bir **başarılı** veya **sürüyor** durumu.
  >
  >

3.  Bu açık hello **bildirim ayrıntıları** dikey.

4.  Bu bilgileri kendiniz hello sorun hakkında daha fazla ayrıntı toounderstand kullanın.

5.  Hala yardıma ihtiyacınız varsa, sorununuzu ile bir destek mühendisi veya hello ürün grubu tooget Yardım ile bu bilgileri de paylaşabilir.

6.  Merhaba tıklatın **kopyalama** **simgesi** hello sağında toohello **kopyalama hatası** textbox toocopy tüm bildirim ayrıntıları tooshare bir destek veya ürün grubu mühendisi ile Merhaba.

## <a name="how-tooget-help-by-sending-notification-details-tooa-support-engineer"></a>Tooget nasıl yardımcı bildirim ayrıntıları tooa destek mühendisine göndererek

Paylaştığınız çok önemlidir **tüm ayrıntılar aşağıda listelenen hello** size hızla yardımcı böylece yardıma gereksiniminiz varsa bir destek mühendisine ile. Bu yana kolayca yapabilirsiniz **bir ekran görüntüsü alma** veya hello tıklatarak **kopyalama hata simgesi**, hello toohello sağındaki bulundu **kopyalama hatası** textbox.

## <a name="notification-details-explained"></a>Açıklanan bildirim ayrıntıları

Merhaba aşağıdaki daha hangi öğelerin her birini hello bildirim anlamına gelir ve bunların her birini verir örnekleri açıklanmaktadır.

### <a name="essential-notification-items"></a>Temel bildirim öğeleri

-   **Başlık** – hello hello bildirim açıklayıcı bir başlık

    -   Örnek – **uygulama proxy ayarları**

-   **Açıklama** – hello ne hello işlem sonucunda oluşan açıklaması

    -   Örnek – **girilen iç url başka bir uygulama tarafından zaten kullanılıyor**

-   **Bildirim kimliği** – hello bildirim hello benzersiz kimliği

    -   Örnek – **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**

-   **İstemci istek kimliği** – tarayıcınız tarafından yapılan hello belirli bir istek kimliği

    -   Örnek – **302fd775-3329-4670-a9f3-bea37004f0bc**

-   **Zaman damgası UTC** – sırasında hello bildirim meydana geldiği UTC zaman damgası hello

    -   Örnek – **2017-03-23T19:50:43.7583681Z**

-   **İç işlem kimliği** – kullanabileceğiniz toolook hello hata bizim sistemlerinde iç kimliği hello

    -   Örnek – **71a2f329-ca29-402f-aa72-bc00a7aca603**

-   **UPN** – hello işlemi gerçekleştiren hello kullanıcı

    -   Örnek –**tperkins@f128.info**

-   **Kiracı kimliği** – hello benzersiz kimliği kullanıcı hello hello Kiracı hello işlemi gerçekleştiren bir üyesi.

    -   Örnek – **7918d4b5-0442-4a97-be2d-36f9f9962ece**

-   **Kullanıcı nesnesi kimliği** – hello işlemi gerçekleştiren hello kullanıcının benzersiz Kimliğini hello

    -   Örnek – **17f84be4-51f8-483a-b533-383791227a99**

### <a name="detailed-notification-items"></a>Ayrıntılı bildirim öğeleri

-   **Görünen ad** – **(boş olabilir)** hello hatası için ayrıntılı bir görünen ad

    -   Örnek * – **uygulama proxy ayarları**

-   **Durum** – hello hello bildirim özel durumu

    -   Örnek * – **başarısız oldu**

-   **Nesne Kimliği** – **(boş olabilir)** karşı hangi hello işlemi gerçekleştirildiği nesne kimliği hello

    -   Örnek – **8e08161d-f2fd-40ad-a34a-a9632d6bb599**

-   **Ayrıntılar** – hello ayrıntılı ne hello işlem sonucunda oluşan açıklaması

    -   Örnek – **iç url 'http://bing.com/', zaten kullanımda olduğundan geçersiz**

-   **Kopyalama hatası** – tıklatın hello **Kopyala simgesi** hello sağında toohello **kopyalama hatası** textbox toocopy tüm bildirim ayrıntıları tooshare bir destek veya ürün grubu mühendisi ile Merhaba

    -   Örnek –```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```

## <a name="next-steps"></a>Sonraki adımlar
[Uygulama proxy'si ile çoklu oturum açma tooyour uygulamaları sağlayın](active-directory-application-proxy-sso-using-kcd.md)

