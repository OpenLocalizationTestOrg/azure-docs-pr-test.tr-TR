---
title: "tooyour oturum açma ve erişim paneli sayfasında aaaAdd şirket markası"
description: "Nasıl tooadd şirket markasıyla toohello Azure oturum açma sayfası ve hello erişim paneli sayfası öğrenin"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: f74621b4-4ef0-4899-8c0e-0c20347a8c31
ms.service: active-directory
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/23/2017
ms.author: curtand
ms.openlocfilehash: b1c6442028393552bff3d380312c8cd1bfda5d31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-company-branding-tooyour-sign-in-and-access-panel-pages"></a>Tooyour oturum açma ve erişim paneli sayfasında şirket markası ekleme
tooavoid Karışıklığı önlemek için birçok şirket tüm hello Web siteleri ve yönettikleri hizmetlerde tooapply tutarlı bir görünüm istiyor. Azure Active Directory web sayfalarıyla şirket Logonuzla ve özel renk düzenleri aşağıdaki hello toocustomize hello görünümünü sağlayarak bu yeteneği sağlar:

* **Oturum açma sayfası** -tooOffice 365 oturum açtığınızda görüntülenen hello sayfa veya Azure AD kimlik sağlayıcınız olarak kullanan diğer web tabanlı uygulamalar budur. Kimlik bilgilerinizi bu sayfayı giriş bölgesi bulma veya tooenter sırasında ile etkileşim. Merhaba giriş bölgesi bulma hello sistem tooredirect federe kullanıcılar tootheir şirket içi STS'LERİNE (örneğin, AD FS) sağlar.
* **Erişim paneli sayfası** - hello erişim paneli olduğu tooview sağlayan web tabanlı bir portal ve Azure AD yöneticinizin izni başlatma hello bulut tabanlı uygulamalara erişmek için. tooaccess hello erişim paneli, URL aşağıdaki kullanım hello: [https://myapps.microsoft.com](https://myapps.microsoft.com).

Bu konuda hello oturum açma sayfası ve hello erişim paneli sayfasına nasıl özelleştirebileceğiniz açıklanmaktadır.

> [!NOTE]
> * Şirket markası, yalnızca toohello Premium veya Basic sürümüne Azure Active Directory yükselttiyseniz kullanılabilir veya bir Office 365 kullanıcısıysanız bir özelliktir. Daha fazla bilgi için bkz. [Azure Active Directory sürümleri](active-directory-editions.md).
> * Azure Active Directory Premium ve Basic sürümleri Azure Active Directory Merhaba Dünya çapındaki örneğini kullanan Çin müşteriler için kullanılabilir. Azure Active Directory Premium ve Basic sürümleri şu anda Çin'de 21Vianet tarafından işletilen hello Microsoft Azure hizmetindeki desteklenmez. Daha fazla bilgi için bize hello başvurun [Azure Active Directory Forumu](https://feedback.azure.com/forums/169401-azure-active-directory/).
>
>

## <a name="customizing-hello-sign-in-page"></a>Merhaba oturum açma sayfasını özelleştirme
Genellikle, tarayıcı tabanlı erişim tooyour bulut uygulamalarınıza ve kuruluşunuzun abonesi olduğu hizmetlere gerekiyorsa, hello oturum açma sayfasını kullanın.

Değişiklikleri tooyour oturum açma sayfası uyguladıysanız, tooan saat hello değişiklikleri tooappear için yukarı alabilir.

Bir hizmeti, https://outlook.com/**contoso**.com veya https://mail.**contoso**.com gibi yalnızca kiracıya özgü bir URL ile ziyaret ettiğinizde markalı oturum açma sayfası görüntülenir.

Hizmeti https://mail.office365.com gibi kiracıya özgü olmayan bir URL ile ziyaret ederseniz markasız oturum açma sayfası görüntülenir. Bu durumda markanız, kullanıcı kimliğinizi girdiğinizde veya kullanıcı kutucuğunu seçtiğinizde görüntülenir.

> [!NOTE]
> * Etki alanı adınızı hello "Etkin" olarak görünmesi gereken **Active Directory** > **Directory** > **etki alanları** hello Klasik Azure portalı bölümü Burada, marka yapılandırdınız.
> * Oturum açma sayfası markalama toohello tüketici oturum açma sayfasına Microsoft üzerinden taşımak değil. Kişisel bir Microsoft hesabıyla oturum açın, Azure AD tarafından işlenen kullanıcı kutucuklarının markalı bir listesini görebilirsiniz ancak kuruluşunuzun hello markası toohello Microsoft hesabı oturum açma sayfasına uygulanmaz.
>
>

Şirketinizin markasını, renklerini ve diğer özelleştirilebilir öğelerini bu sayfadaki tooshow istiyorsanız, hello iki deneyim arasındaki görüntüleri toounderstand hello fark aşağıdaki hello bakın.

Merhaba ekran gösterir ve örnek hello Office 365 oturum açma sayfasında bir masaüstü bilgisayar için aşağıdaki **önce** bir özelleştirme:

![Özelleştirmeden önce Office 365 oturum açma sayfası][1]

Merhaba ekran gösterir ve örnek hello Office 365 oturum açma sayfasında bir masaüstü bilgisayar için aşağıdaki **sonra** bir özelleştirme:

![Özelleştirmeden sonra Office 365 oturum açma sayfası][2]

Merhaba aşağıdaki ekran görüntüsü hello Office 365 oturum açma sayfası örneği bir mobil cihazda gösterir **önce** bir özelleştirme:

![Özelleştirmeden önce Office 365 oturum açma sayfası][3]

Merhaba aşağıdaki ekran görüntüsü hello Office 365 oturum açma sayfası örneği bir mobil cihazda gösterir **sonra** bir özelleştirme:

![Özelleştirmeden sonra Office 365 oturum açma sayfası][4]

Tarayıcı penceresini yeniden boyutlandırdığınızda büyük çizim Merhaba, hello gibi bir daha önce gösterilen genellikle kırpılmış tooaccommodate farklı ekran en boy oranlarına. Bunlar her zaman hello sol üst köşede (sağdan sola yazılan diller için sağ üst) görünmesini sağlayacak şekilde bu unutmayın, tookeep hello temel görsel öğeleri hello çizimdeki denemelisiniz. Yeniden boyutlandırma genellikle hello sol / üst doğrultusunda hello sağ alt köşe gitmesini önleyen veya hello üst doğrultusunda hello Alttan oluştuğundan bu önemlidir.

Merhaba aşağıdaki resimde hello tarayıcı sol yeniden boyutlandırılan toohello olduğunda nasıl hello çizim kırpıldığı gösterilmiştir:

![][6]

İşte hello tarayıcı hello yukarı doğru yeniden boyutlandırıldıktan sonra şu şekilde görünür:

![][7]

## <a name="what-elements-on-hello-page-can-i-customize"></a>Merhaba sayfadaki hangi öğeleri özelleştirebilirim?
Oturum açma hello sayfasında öğeleri aşağıdaki hello özelleştirebilirsiniz:

![][5]

| Sayfa öğesi | Merhaba sayfadaki konum |
|:--- | --- |
| Başlık Logosu |Merhaba sağ üst tarafında hello sayfası gösterilir. Merhaba logosu hello hedef site içinde toodisplays (örneğin, oturum açıyorsanız değiştirir Office 365 veya Azure) görüntülenen logonun yerini alır. |
| Büyük Çizim/Arka Plan Rengi |Merhaba hello sayfanın solunda gösterilir. Merhaba görüntü hello hedef site içinde toodisplays imza yerini alır. Merhaba büyük çizim düşük bant genişliğine sahip bağlantılarda veya dar ekranlarda yerine Hello arka plan rengi gösterilebilir. |
| Oturumum açık kalsın |Merhaba parola metin kutusu altında gösterilir. |
| Oturum Açma Sayfası Metni |Bir oturum açma bir iş veya Okul hesabıyla önce tooconvey yardımcı olacak bilgiler gerektiğinde Merhaba sayfa alt bilgisinde gösterilir. Örneğin, tooinclude hello telefon numarası tooyour yardım masasına veya yasal bildirim isteyebilir. |

> [!NOTE]
> Tüm öğeler isteğe bağlıdır. Örneğin, bir başlık logosu ancak büyük çizim belirtirseniz, hello oturum açma sayfası logo ve hello çizim hello hedef sitenin (diğer bir deyişle, hello Office 365'in California Otoyol görüntüsü) gösterir.
>
>

Oturum açma sayfanızda hello **Oturumumu açık bırak** onay kutusunu kapatın ve yeniden tarayıcısında açın açtığınız kullanıcı tooremain sağlar. Bu durum oturum ömrünü etkilemez. Oturum açma hello Azure Active Directory sayfasında hello onay kutusunu gizleyebilirsiniz.

Merhaba onay kutusu görüntülenip görüntülenmeyeceğini, hello ayarına bağlıdır **Gizle KMSI**.

![][9]

toohide onay kutusunu Merhaba, bu çok ayarını yapılandırmak**gizli**.

> [!NOTE]
> Bu kutu mümkün toocheck olan kullanıcılar SharePoint Online ve Office 2010 bazı özelliklerine bağlıdır. Bu ayar toohidden yapılandırırsanız, kullanıcılarınızın ek ve beklenmeyen komut istemlerini toosign de görebilirsiniz.
>
>

Ayrıca bu sayfadaki tüm öğeleri yerelleştirebilirsiniz. Özelleştirme öğelerine ilişkin "varsayılan" bir küme yapılandırdıktan sonra farklı yerel ayarlar için daha fazla sürüm yapılandırabilirsiniz. Ayrıca, çeşitli öğeleri karıştırabilir ve eşleştirebilirsiniz. Örneğin, şunları yapabilirsiniz:

* Tüm kültürler için kullanılabilecek "varsayılan" bir Büyük Çizim oluşturup İngilizce ve Fransızca için belirli sürümler oluşturabilirsiniz. Bu iki dillerden, tarayıcılar tooone ayarladığınızda, hello varsayılan çizim için tüm diğer dillere görüntülenirken hello belirli görüntü görünür.
* Kuruluşunuz için farklı logolar (örneğin, Japonca veya İbranice sürümler) yapılandırabilirsiniz.

## <a name="access-panel-page-customization"></a>Erişim paneli sayfa özelleştirmesi
size verilmiş olan hızlı erişim toohello bulut uygulamalarını tooby yöneticinize erişmek için hello erişim paneli sayfası aslında bir portal sayfasıdır. Uygulamalarınız, bu sayfada tıklanabilir uygulama kutucukları olarak görünür.

Ekran aşağıdaki hello özelleştirme sonrasında bir erişim paneli sayfası örneği gösterilmektedir.

![][8]

## <a name="configure-your-directory-with-company-branding"></a>Dizininizi şirket markasıyla yapılandırma
Merhaba Klasik Azure portalında her dizin özelleştirilebilir öğelere ilişkin bir varsayılan küme yapılandırabilirsiniz. Merhaba varsayılanlar kaydedildikten sonra yönetici farklı diller için her öğenin yerelleştirilmiş sürümlerini ekleyebilir / yerel ayarlar. Tüm özelleştirilebilir öğeler isteğe bağlıdır.

Örneğin, varsayılan başlık logosunu ancak büyük çizim yapılandırırsanız, hello oturum açma sayfası logonuzun hello sağ üst köşesinde görüntüler. Ancak hello site hello varsayılan çizimi görüntülenir.

Yapılandırma aşağıdaki hello düşünün:

* İngilizce dilinde varsayılan bir Başlık Logosu ve Oturum Açma Sayfası Metni
* Almanca için dile özgü Oturum Açma Sayfası Metni 

Dil tercihiniz Almanca ise, hello varsayılan başlık logosunu ancak hello Almanca metni alırsınız.

Teknik olarak Azure AD tarafından desteklenen her dil için farklı bir küme yapılandırabilirsiniz ancak hello Varyasyon sayısını düşük bakım ve performans nedenleriyle tutmanızı öneririz.

> [!IMPORTANT]
> Yammer değil hello kullanıcı oturum açtıktan sonra Azure AD oturum açma sayfası kadar markalı Göster hello yapar. Merhaba kullanıcı genel Office 365 oturum açma sayfasına ilk hello ve ardından hello sayfa bundan sonra markalı görür.   
 
 
**tooadd marka tooyour dizin şirket, hello aşağıdaki adımları gerçekleştirin:**

1. İçinde toohello oturum [Klasik Azure portalı](https://manage.windowsazure.com) hello directory yönetici olarak toocustomize istiyor.
2. Toocustomize istediğiniz hello dizini seçin.
3. Merhaba üstte Hello araç çubuğunda **yapılandırma**.
4. **Customize Branding (Markayı Özelleştir)**düğmesine tıklayın.
5. Toocustomize istediğiniz hello öğeleri değiştirin. Tüm alanlar isteğe bağlıdır.
6. **Kaydet** düğmesine tıklayın.

Bu yeni değişiklik tooan saattir yukarı yapabileceğiniz tooappear marka toohello oturum açma sayfası yapılan.

**tooadd dile özgü şirket markası, hello aşağıdaki adımları gerçekleştirin:**

1. İçinde toohello oturum [Klasik Azure portalı](https://manage.windowsazure.com) hello directory yönetici olarak toocustomize istiyor.
2. Toocustomize istediğiniz hello dizini seçin.
fs3. Merhaba üstte Hello araç çubuğunda **yapılandırma**.
4. **Customize Branding (Markayı Özelleştir)**düğmesine tıklayın.
5. **Add branding for a specific language (Belirli bir dil için marka ekle)** düğmesine tıklayın.
6. Toocustomize hello logosu istediğiniz ve ardından hello dili seçin **sonraki**.
7. Yalnızca tooconfigure dile özgü geçersiz kılmaları istediğiniz hello öğeleri düzenleyin. Tüm alanlar isteğe bağlıdır. Bir alan boş bırakılırsa, ardından hello özel varsayılan değer görüntülenir (veya özel varsayılan yapılandırılmamışsa Microsoft varsayılan hello).
8. **Kaydet** düğmesine tıklayın.

**tooremove şirket markası, Directory'den hello aşağıdaki adımları gerçekleştirin:**

1. İçinde toohello oturum [Klasik Azure portalı](https://manage.windowsazure.com) hello directory yönetici olarak toocustomize istiyor.
2. Toocustomize istediğiniz hello dizini seçin.
3. Merhaba üstte Hello araç çubuğunda **yapılandırma**.
4. **Customize Branding (Markayı Özelleştir)**düğmesine tıklayın.
5. Merhaba marka Özelleştirme sayfasında, seçin **var olan marka ayarlarını Düzenle** ve toohello sonraki sayfaya gidin.
6. Hangi öğelerin bağlı olarak tooremove istediğiniz, bir veya daha fazla hello aşağıdakileri yapın:

    a. **Banner Logo (Başlık Logosu)** altında **Remove uploaded logo (Karşıya yüklenen logoyu kaldır)** seçeneğini belirleyin.

    b. **Tile Logo (Kutucuk Logosu)** altında **Remove uploaded logo (Karşıya yüklenen logoyu kaldır)** seçeneğini belirleyin.

    c. Merhaba metin tüm kutularındaki metinleri kaldırın.

    d. **İleri**’ye tıklayın.

    e. Merhaba metin tüm kutularındaki metinleri kaldırın.
7. Tıklatın **kaydetmek** tooremove hello öğeleri.
8. Gerekirse, **marka özelleştirme** yeniden ve tüm dile özgü marka toobe gereken kaldırılan için bu adımları yineleyin.
    ' I tıklattığınızda tüm marka ayarları kaldırılmıştır **marka özelleştirme** ve hello **varsayılan marka özelleştirme** yapılandırılmış bir ayar ile form.

## <a name="testing-and-examples"></a>Test ve örnekler
Üretim ortamınızda değişiklik yapmadan önce bir kiracı ile deneme yapmanızı öneririz.

**tooverify olup marka bilgilerinizi uygulanmış:**

1. InPrivate veya Incognito tarayıcı oturumu açın.
2. Contoso.com özelleştirdiğiniz hello etki alanıyla değiştirerek https://outlook.com/contoso.com adresini ziyaret edin.

Bu, contoso.onmicrosoft.com gibi görünen etki alanları için de geçerlidir.

toohelp etkili özelleştirme kümeleri oluşturma, şu iki kurgusal oturum açma sayfaları aşağıdaki hello özelleştirdikten:

* [http://aka.ms/aaddemo001](http://aka.ms/aaddemo001)
* [http://aka.ms/aaddemo002](http://aka.ms/aaddemo002)

tootest hello dile özgü ayarları özelleştirme sırasında ayarladığınız sizin dilinizde web tarayıcısı tooa toomodify hello varsayılan dil tercihlerini gerekir. Internet Explorer'da bu hello yapılandırdığınız **Internet Seçenekleri** menüsü.

## <a name="customizable-elements"></a>Özelleştirilebilir öğeler
Azure AD'deki bazı özelleştirilebilir öğelerin birden çok kullanım durumu vardır. Hem, hello oturum açma ve erişim paneli sayfasında kullanılır ve şirket logolarını her dizin için bir kez yapılandırabilirsiniz. Bazı özelleştirilebilir öğeler belirli yalnızca toohello oturum açma sayfası bağlıdır. Merhaba aşağıdaki tabloda Ayrıntılar Merhaba farklı özelleştirilebilir öğelerle sağlar.

| Ad | Açıklama | Kısıtlamalar | Öneriler |
| --- | --- | --- | --- |
| Başlık Logosu |Merhaba başlık logosu hello oturum açma sayfası ve hello erişim paneli görüntülenir. |<p>JPG veya PNG</p><p>60x280 piksel</p><p>10 KB</p> |<p>Kuruluşunuzun tam logosunu (piktogram ve logo türü dahil) kullanın</p><p>Mobil cihazlarda kaydırma çubukları Tanıtımı altında 30 piksel yüksek tooavoid tutun</p><p>4 KB altında tutun</p><p>Saydam bir PNG kullanın (oturum açma bu hello sayfası her zaman beyaz bir arka plan olduğu varsaymayın)</p> |
| Kutucuk Logosu |(şu anda hello oturum açma sayfasında kullanılmıyor) Hello gelecekteki, bu metin kullanılan tooreplace hello genel "iş veya Okul hesabı" piktogram hello deneyiminin farklı yerlerde olabilir. |<p>JPG veya PNG</p><p>120x120 piksel</p><p>10 KB</p> |<p>Bu görüntü yeniden boyutlandırılan too50% olabileceğinden basit (küçük metin olmaksızın), tutun |
| </p> | | | |
| Oturum Açma Sayfası Kullanıcı Adı Etiketi |(şu anda hello oturum açma sayfasında kullanılmıyor) Hello gelecekteki, bu metin kullanılan tooreplace hello hello deneyiminin farklı yerlerde genel "iş veya Okul hesabı" dizesini olabilir. "Contoso hesabı" veya "Contoso kimliği" gibi toosomething ayarlayın |<p>Unicode metin too50 karakterleri ayarlama</p><p>Yalnızca düz metin (bağlantılar veya HTML etiketleri olmadan)</p> |<p>Kısa ve basit tutun</p><p>Kullanıcılarınızı nasıl genellikle başvuran toohello iş veya Okul hesabı ile bunları sağlamanız isteyin.</p> |
| Oturum Açma Sayfası Metni |Bu "ortak" metin hello oturum açma sayfası formunun altında görünür ve kullanılan toocommunicate ek yönergeler olması veya tooget Yardım ve Destek burada yapabilirsiniz. |<p>Unicode metin too256 karakterleri ayarlama</p><p>Yalnızca düz metin (bağlantılar veya HTML etiketleri olmadan)</p> |250 karakterin altında tutun (yaklaşık 3 metin satırı)  |
| Oturum Açma Sayfası Çizimi |Merhaba, Itanium tabanlı sistemler için hello oturum açma sayfası toohello sol hello oturum açma sayfası formunun tarafta görüntülenen büyük bir görüntü çizimidir. |<p>JPG veya PNG</p><p>1420x1200</p><p>500 KB</p> |<p>1420x1200 piksel</p><p>Önemli: Olabildiğince küçük tutun; 200 KB'ın altında olması idealdir. Bu resim çok büyük ise hello önbelleğe alınmadığında hello oturum açma sayfası hello performansı etkilenir</p><p>Bu görüntü genellikle kırpılmış, tooaccommodate farklı ekran oranları. Merhaba birincil görsel öğeleri hello üst köşede (RTL dilleri için sağ üstte), yeniden boyutlandırma hello tarayıcı küçüldükçe sol / üst hello doğru giderek hello sağ alt köşeden oluştuğundan sol unutmayın.</p> |
| Oturum Açma Sayfası Arka Plan Rengi |Hello oturum açma sayfası arka plan rengi, Itanium tabanlı sistemler için hello alanı toohello sol hello oturum açma sayfası formunun kullanılır. |Arka plan rengi, onaltılık biçimde bir RGB rengi olmalıdır (örnek: #FFFFFF) |<p>Merhaba arka plan rengi hello yerine gösterilen düşük bant genişliğine sahip bağlantılarda büyük çizim</p><p>Merhaba başlık logosu hello birincil rengini çekme öneririz</p> |

## <a name="next-steps"></a>Sonraki adımlar
* [Azure Active Directory Premium ile çalışmaya başlama](active-directory-get-started-premium.md)
* [Erişim ve kullanım raporlarınızı görüntüleme](active-directory-view-access-usage-reports.md)

<!--Image references-->
[1]: ./media/active-directory-add-company-branding/SignInPage_beforecustomization.png
[2]: ./media/active-directory-add-company-branding/SignInPage_aftercustomization.png
[3]: ./media/active-directory-add-company-branding/SignInPage_mobile_beforecustomization.png
[4]: ./media/active-directory-add-company-branding/SignInPage_mobile_aftercustomization.png
[5]: ./media/active-directory-add-company-branding/SignInPage_aftercustomization_elements.png
[6]: ./media/active-directory-add-company-branding/SignInPage_aftercustomization_croppedleft.png
[7]: ./media/active-directory-add-company-branding/SignInPage_aftercustomization_croppedtop.png
[8]: ./media/active-directory-add-company-branding/APBranding.png
[9]: ./media/active-directory-add-company-branding/hidekmsi.png
