---
title: "aaaHow toouse erişim denetimi (Java) | Microsoft Docs"
description: "Bilgi toodevelop ve kullanım erişim denetimi ile nasıl azure'da Java."
services: active-directory
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 247dfd59-0221-4193-97ec-4f3ebe01d3c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.custom: aaddev
ms.openlocfilehash: cbbce3b1a05eabf3b86a8cb91db1bde92dbb8960
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooauthenticate-web-users-with-azure-access-control-service-using-eclipse"></a>Nasıl tooAuthenticate Web kullanıcıları Azure erişim denetimi hizmeti kullanılarak Eclipse ile
Bu kılavuz size nasıl toouse hello Azure erişim denetimi Hizmeti'nden (ACS) hello Eclipse için Azure Araç Seti içinde gösterir. Merhaba ACS hakkında daha fazla bilgi için bkz: [sonraki adımlar](#next_steps) bölümü.

> [!NOTE]
> Hello Azure Erişim Hizmetleri Denetim filtresi topluluk teknoloji önizlemesidir. Yayın öncesi yazılım olarak bunu resmi olarak Microsoft tarafından desteklenmiyor.
> 
> 

## <a name="what-is-acs"></a>ACS nedir?
Çoğu geliştirici kimlik uzmanlar değildir ve genellikle zaman geliştirme kimlik doğrulama ve yetkilendirme mekanizmaları kullanıcıların uygulamaları ve Hizmetleri için harcadıkları istemiyorsanız. ACS tooaccess web uygulamalarınızın isteyen kullanıcıların kimliğini doğrulamak için kolay bir yol sağlayan bir Azure hizmeti ve toofactor karmaşık kimlik doğrulaması mantığı kodunuzu içine kalmadan Hizmetleri ' dir.

özellikler aşağıdaki hello ACS kullanılabilir:

* Windows Identity Foundation (WIF) ile tümleştirme.
* Windows Live ID, Google, Yahoo! ve Facebook dahil olmak üzere popüler web kimlik sağlayıcıları (IP) desteği.
* Active Directory Federasyon Hizmetleri (AD FS) için destek 2.0.
* Açık Veri Protokolü (OData)-tooACS ayarları programlı erişim sağlayan Yönetim hizmetini alan.
* Toohello ACS ayarları yönetim erişimine izin veren bir Yönetim Portalı.

ACS hakkında daha fazla bilgi için bkz: [erişim denetimi hizmeti 2.0][Access Control Service 2.0].

## <a name="concepts"></a>Kavramlar
Azure ACS hello sorumluları bir tutarlı bir yaklaşım toocreating kimlik doğrulama mekanizmaları hello bulutta veya şirket içi çalışan uygulamalar için talep tabanlı kimlik -, yerleşik olarak bulunur. Talep tabanlı kimlik, uygulamaları ve Hizmetleri tooacquire ihtiyaç duydukları diğer kuruluşlardan ve hello Internet kendi kuruluş içindeki kullanıcıların kimlik bilgilerini için ortak bir yol sağlar.

toocomplete başlangıç görevleri bu kılavuzdaki kavramlar aşağıdaki hello anlamanız gerekir:

**İstemci** -bu nasıl tooguide hello bağlamda toogain erişim tooyour web uygulaması çalışırken bir tarayıcı budur.

**Bağlı olan taraf (RP) uygulama** -bir Web sitesi veya kimlik doğrulama tooone dış yetkilisi outsources hizmeti, bir RP uygulamasıdır. Kimlik terimler o hello RP imzaladığınızda söyleyin. Bu kılavuz açıklar nasıl tooconfigure, uygulama tootrust ACS.

**Belirteç** -genellikle bir kullanıcının başarılı kimlik doğrulama sırasında verilen güvenlik verilerinin bir koleksiyonunu bir belirteçtir. Bir dizi içerdiği *talep*, hello özniteliklerini kimliği doğrulanmış kullanıcı. Bir talep bir kullanıcının adını gösterebilir, bir kullanıcının yaşı vb. için bir kullanıcı rolü için bir tanımlayıcı ait. Bir belirteç genellikle dijital olarak imzalanmış, her zaman kaynaklı geri tooits veren olabilir ve içeriği ile değiştirilmemesi anlamına gelir. Merhaba RP uygulaması güvendiği bir yetkili tarafından verilen geçerli bir belirteci sunarak bir kullanıcı kazançlar erişim tooa RP uygulaması.

**Kimlik sağlayıcısı (IP)** -IP kullanıcı kimliklerini doğrular ve güvenlik belirteçleri bir yetkili değil. belirteç hello gerçek iş güvenlik belirteci hizmeti (STS) adlı bir özel hizmet olsa uygulanır. Windows Live ID, Facebook, iş kullanıcı depoları (örneğin, Active Directory) ve benzeri IP'leri tipik örnekleri içerir.
ACS yapılandırılmış tootrust IP olduğunda hello sistem kabul etmek ve bu IP tarafından yayınlanan belirteçleri doğrulamak. ACS, uygulamanızın ACS güvendiğinde, uygulama tooall hello anında sunabileceğiniz anlamına gelir IP'leri Bu ACS sizin adınıza güvendiği tüm hello kullanıcılardan kimliği doğrulanmış birden çok IP aynı anda güvenebilirsiniz.

**Federasyon sağlayıcısı (FP)** -IP'leri kullanıcılar, doğrudan bilgiye sahip ve bunları kendi kimlik bilgilerini kullanarak kimlik doğrulaması ve sorun hakkında ne bunlarla ilgili bildikleri talep. Bir Federasyon sağlayıcı (FP) yetkilisi farklı türüdür: kullanıcıların doğrudan kimlik doğrulaması yerine, bir aracı ve aracıların arasındaki kimlik doğrulaması bir RP bir görür veya daha fazla IP. IP ve FPs belirteçleri güvenlik, dolayısıyla her ikisi de güvenlik belirteci Hizmetleri (STS) kullanın. ACS bir dp ' dir.

**ACS kuralı altyapısı** -güvenilen IP'leri tootokens gelen kullanılan tootransform gelen belirteçleri amacı basit biçiminde hello RP tarafından tüketilen toobe kod oluşturulmuş hello mantığı talep dönüştürme kuralları. ACS, RP için belirtilen dönüşüm mantığı uygulamak mvc'deki bir kuralı altyapısı sunar.

**ACS Namespace** -ayarlarınızı düzenlemek için kullandığınız ACS en üst düzey bölümünü bir ad alanıdır. Bir ad alanı güvendiğiniz IP'leri listesini tutar, hello RP uygulamaları tooserve, beklediğiniz hello kuralları istediğiniz kuralı altyapısı tooprocess gelen belirteçleri vb. hello. Bir ad alanı olacak çeşitli uç noktalarını kullanıma sunar hello uygulama ve geliştirici tooget ACS tooperform tarafından kendi işlevi kullanılır.

Merhaba aşağıdaki şekilde ACS kimlik doğrulaması bir web uygulaması ile nasıl çalıştığı gösterilmektedir:

![ACS Akış Diyagramı][acs_flow]

1. Merhaba istemcisinde (Bu durumda bir tarayıcı) bir sayfayı hello RP ' ister.
2. Merhaba isteği henüz doğrulanmamış olduğundan, hello RP ACS olduğu güvendiği, hello kullanıcı toohello yetkilisi yönlendirir. Merhaba ACS hello kullanıcı için bu RP belirtilmiş IP'leri hello seçimine sunar. Merhaba kullanıcı hello uygun IP seçer.
3. Merhaba istemci toohello IP'ın kimlik doğrulaması sayfası gözatar ve üzerinde hello kullanıcı toolog ister.
4. Merhaba IP Hello istemci (örneğin, girilen kimlik bilgileri hello kimlik) doğrulandıktan sonra bir güvenlik belirteci verir.
5. Bir güvenlik belirteci gönderdikten, hello IP hello istemci tooACS yeniden yönlendirir ve hello güvenlik belirteci IP tooACS hello tarafından verilen hello istemciye gönderir.
6. ACS hello kimlik hello ACS kuralları motoruna bu belirteç talep, hello çıkış kimlik talepleri hesaplar ve bu çıkış talepleri içeren yeni bir güvenlik belirteci verir girişleri hello IP tarafından verilen hello güvenlik belirteci doğrular.
7. ACS hello istemci toohello RP yönlendirir. Merhaba istemci ACS toohello RP tarafından verilen hello yeni güvenlik belirteci gönderir. Merhaba RP ACS tarafından verilen hello güvenlik belirtecine hello imzayı doğrular, bu belirteç hello Taleplerde doğrular ve başlangıçta istenen hello sayfasını döndürür.

## <a name="prerequisites"></a>Ön koşullar
toocomplete hello görevler bu kılavuzda hello aşağıdaki gerekir:

* Bir Java Geliştirme Seti (JDK), v 1.6 veya sonraki sürümleri.
* Java EE geliştiricileri için Eclipse IDE Indigo olarak biliniyordu veya üzeri. Bu adresten yüklenebilir <http://www.eclipse.org/downloads/>. 
* Java tabanlı web sunucusu ya da Apache Tomcat, GlassFish, JBoss uygulama sunucusu veya Jetty gibi uygulama sunucusu dağıtımı.
* öğesinden alınan bir Azure aboneliği <http://www.microsoft.com/windowsazure/offers/>.
* Merhaba, Eclipse için Azure Araç Seti sürüm Nisan 2014 veya üzeri. Daha fazla bilgi için bkz: [yükleme hello Eclipse için Azure Araç Seti](http://msdn.microsoft.com/library/windowsazure/hh690946.aspx).
* Bir X.509 sertifikası toouse uygulamanız ile. Bu sertifika ortak sertifika (.cer) ve kişisel bilgi değişimi gerekir (. PFX) biçimi. (Bu sertifikayı oluşturmak için seçenekler daha sonra Bu öğreticide açıklanacaktır).
* Aşina hello Azure işlem öykünücüsü ve dağıtım teknikleri, ele alınan [Hello World uygulamasının Azure için Eclipse'te oluşturma](http://msdn.microsoft.com/library/windowsazure/hh690944.aspx).

## <a name="create-an-acs-namespace"></a>Bir ACS Namespace oluşturma
Azure'da, erişim denetimi Hizmeti'nden (ACS) kullanarak toobegin bir ACS ad alanı oluşturmanız gerekir. Merhaba ad alanı, uygulamanızda ACS kaynaklardan adresleme için benzersiz bir kapsam sağlar.

1. Merhaba günlüğüne [Azure Yönetim Portalı][Azure Management Portal].
2. Tıklatın **Active Directory**. 
3. toocreate yeni bir erişim denetimi ad alanı tıklatın **yeni**, tıklatın **uygulama hizmetleri**, tıklatın **erişim denetimi**ve ardından **hızlı Oluştur** . 
4. Merhaba ad alanı için bir ad girin. Azure, bu hello adının benzersiz olduğundan doğrular.
5. Hangi hello ad kullanılan hello bölgeyi seçin. Merhaba en iyi performans için uygulamanızı dağıtıyorsanız hello bölge kullanın.
6. Birden fazla aboneliğiniz varsa, toouse hello ACS ad alanı için istediğiniz hello aboneliği seçin.
7. **Oluştur**'a tıklayın.

Azure oluşturur ve hello ad alanı etkinleştirir. Merhaba yeni ad alanı Hello durumunu olana kadar bekleyin **etkin** devam etmeden önce. 

## <a name="add-identity-providers"></a>Kimlik sağlayıcısı ekleyin
Bu görevde, kimlik doğrulaması için RP uygulamanızla IP'leri toouse ekleyin. Tanıtım amacıyla, bu görev tooadd Windows Live bir IP, ancak olarak IP'leri hello ACS yönetim portalı listelenen hello hiçbirini nasıl kullanabileceğinizi gösterir.

1. Merhaba, [Azure Yönetim Portalı][Azure Management Portal], tıklatın **Active Directory**, bir erişim denetimi ad alanını seçin ve ardından **Yönet**. Merhaba ACS yönetim portalı açar.
2. Merhaba sol gezinti bölmesinde hello ACS yönetim portalı tıklatın **kimlik sağlayıcıları**.
3. Windows Live ID, varsayılan olarak etkindir ve silinemez. Bu öğreticinin amaçları doğrultusunda, yalnızca Windows Live ID kullanılır. Bu, ancak diğer IP'leri hello tıklayarak eklediğiniz ekrandır **Ekle** düğmesi.

Windows Live ID ACS ad alanınız için bir IP olarak etkinleştirilmiştir. Ardından, Java web uygulamanıza (daha sonra oluşturulan toobe) belirttiğiniz bir RP olarak.

## <a name="add-a-relying-party-application"></a>Bir bağlı olan taraf uygulaması ekleyin
Bu görevde, ACS toorecognize geçerli bir RP uygulama Java web uygulamanızı yapılandırın.

1. Hello ACS yönetim portalı, tıklatın **bağlı olan taraf uygulamaları**.
2. Merhaba üzerinde **bağlı olan taraf uygulamaları** sayfasında, **Ekle**.
3. Merhaba üzerinde **bağlı olan taraf uygulaması Ekle** sayfasında, aşağıdaki hello:
   
   1. İçinde **adı**, hello RP tür hello adı. Bu öğreticinin amaçları doğrultusunda yazın **Azure Web uygulaması**.
   2. İçinde **modu**seçin **ayarlarını girin el ile**.
   3. İçinde **bölge**, türü hello URI toowhich hello güvenlik belirteci ACS tarafından verilen uygular. Bu görev için yazın **http://localhost: 8080 /**.
      ![İşlem öykünücüsü kullanmak için bağlı olan taraf bölgesi][relying_party_realm_emulator]
   4. İçinde **dönüş URL'si** türü hello URL toowhich ACS hello güvenlik belirteci verir. Bu görev için yazın **http://localhost:8080/MyACSHelloWorld/index.jsp**
      ![bağlı olan taraf işlem öykünücüsü kullanmak için URL döndürür][relying_party_return_url_emulator]
   5. Merhaba kalan hello alanlarının Hello varsayılan değerleri kabul edin.
4. **Kaydet** düğmesine tıklayın.

Hello Azure işlem öykünücüsü çalıştırdığınızda artık başarıyla Java web uygulamanıza yapılandırdınız (adresindeki http://localhost: 8080 /) toobe ACS ad alanındaki bir RP. Ardından, hello kuralları oluşturun ACS hello RP için tooprocess talepleri kullanır.

## <a name="create-rules"></a>Kuralları oluşturma
Bu görevde, talep IP'leri tooyour RP ' nasıl geçtiğini sürücü hello kuralları tanımlar. Bu kılavuzun amacı Hello için biz yalnızca ACS toocopy hello giriş talep türlerini ve değerlerini doğrudan hello çıkış belirteçte filtreleme veya bunları değiştirme yapılandırır.

1. Merhaba ACS yönetim portalı ana sayfasında, tıklatın **Kural gruplarını**.
2. Merhaba üzerinde **kuralı grupları** sayfasında, **Azure Web uygulaması için varsayılan kuralı grubu**.
3. Merhaba üzerinde **kural grubunu Düzenle** sayfasında, **Generate**.
4. Merhaba üzerinde **kuralları oluştur: Azure Web uygulaması için varsayılan kuralı grubu** sayfasında, Windows Live ID işaretli emin olun ve ardından **Generate**.    
5. Merhaba üzerinde **kural grubunu Düzenle** sayfasında, **kaydetmek**.

## <a name="upload-a-certificate-tooyour-acs-namespace"></a>Bir sertifika tooyour ACS ad alanı karşıya yükle
Bu görevde, karşıya bir. ACS ad alanınızı tarafından oluşturulan kullanılan toosign belirteç istekleri olacaktır PFX sertifikası.

1. Merhaba ACS yönetim portalı ana sayfasında, tıklatın **sertifikaları ve anahtarları**.
2. Merhaba üzerinde **sertifikaları ve anahtarları** sayfasında, **Ekle** yukarıda **belirteç imzalama**.
3. Merhaba üzerinde **eklemek belirteç imzalama sertifikası veya anahtar** sayfa:
   1. Merhaba, **için kullanılan** 'yi tıklatın **bağlı olan taraf uygulaması** seçip **Azure Web uygulaması** (Bu, daha önce bağlı olan taraf uygulamanızı hello adı olarak ayarlayın).
   2. Merhaba, **türü** bölümünde, select **X.509 sertifikası**.
   3. Merhaba, **sertifika** bölümünde hello Gözat düğmesini tıklatın ve istediğiniz toouse toohello X.509 sertifika dosyasını gidin. Bu bir. PFX dosyası. Merhaba dosyasını seçin, **açık**ve hello sertifika parolası hello enter **parola** metin kutusu. Test amacıyla, bir self-signed sertifika kullanmak unutmayın. toocreate kendinden imzalı bir sertifika kullanmak hello **yeni** hello düğmesini **ACS filtre kitaplığı** (aşağıda açıklanmıştır), iletişim veya hello **encutil.exe** yardımcı programı'ndan hello [proje Web sitesi] [ project website] hello Java için Azure Starter Kit.
   4. Emin **olun birincil** denetlenir. **Eklemek belirteç imzalama sertifikası veya anahtar** sayfa benzer toohello aşağıdaki görünmelidir.
       ![Belirteç imzalama sertifikası ekleme][add_token_signing_cert]
   5. Tıklatın **kaydetmek** toosave Kapat hello ve ayarlarınızı **eklemek belirteç imzalama sertifikası veya anahtar** sayfası.

Ardından, hello uygulama tümleştirmesi sayfası ve kopyalama hello URI hello bilgileri, Java web uygulaması toouse ACS tooconfigure gerekir gözden geçirin.

## <a name="review-hello-application-integration-page"></a>Gözden geçirme hello uygulama tümleştirmesi sayfası
Tüm hello bilgileri ve hello kodu gerekli tooconfigure, Java web uygulaması (Merhaba RP uygulama) toowork ACS ile Merhaba ACS yönetim Portalı'nın hello uygulama tümleştirmesi sayfasında bulabilirsiniz. Java web uygulamanızı federe kimlik doğrulaması için yapılandırırken bu bilgileri gerekir.

1. Hello ACS yönetim portalı, tıklatın **uygulama tümleştirmesi**.  
2. Merhaba, **uygulama tümleştirmesi** sayfasında, **oturum açma sayfaları**.
3. Merhaba, **oturum açma sayfası tümleştirme** sayfasında, **Azure Web uygulaması**.

Merhaba, **oturum açma sayfası tümleştirme: Azure Web uygulaması** sayfasında, listelenen hello URL **seçenek 1: bağlantı tooan ACS barındırılan oturum açma sayfasına** Java web uygulamanızda kullanılacak. Hello Azure erişim denetimi Hizmetleri filtre kitaplığı tooyour Java uygulaması eklediğinizde, bu değer gerekir.

## <a name="create-a-java-web-application"></a>Bir Java web uygulaması oluşturma
1. Merhaba menüsünü Eclipse içinde **dosya**, tıklatın **yeni**ve ardından **dinamik Web projesi**. (Görmüyorsanız **dinamik Web projesi** tıkladıktan sonra kullanılabilir bir proje listelenen **dosya**, **yeni**, ardından aşağıdaki hello: tıklatın **dosya**, tıklatın **yeni**,'ı tıklatın **proje**, genişletin **Web**, tıklatın **dinamik Web projesi**, tıklatıp  **Sonraki**.) Bu öğreticinin amaçları doğrultusunda hello proje adı **MyACSHelloWorld**. (Emin bu adı kullanın, bu öğreticide sonraki adımlarda beklediğiniz MyACSHelloWorld adlı, WAR dosyasını toobe). Ekranınızın benzer toohello aşağıdaki görünür:
   
    ![ACS exampple için Hello World projesi oluşturma][create_acs_hello_world]
   
    **Son**'a tıklayın.
2. Eclipse'nın Proje Gezgini görünümü içinde genişletmek **MyACSHelloWorld**. **WebContent**'e sağ tıklayın, **Yeni**'ye tıklayın ve ardından **JSP Dosyası**'na tıklayın.
3. Merhaba, **yeni JSP dosyası** iletişim, adı hello dosyası **index.jsp**. Merhaba aşağıda gösterildiği gibi Hello üst klasörü MyACSHelloWorld/WebContent olarak tutun:
   
    ![ACS örneğin bir JSP dosyası ekleme][add_jsp_file_acs]
   
    **İleri**’ye tıklayın.
4. Merhaba, **JSP şablon seç** iletişim kutusunda **yeni JSP dosyası (html)** tıklatıp **son**.
5. Merhaba index.jsp dosyası Eclipse'te açıldığında, metin toodisplay ekleme **Hello ACS World!** Merhaba varolan içinde `<body>` öğesi. Güncelleştirilmiş `<body>` içerik hello aşağıdaki gibi görünmelidir:
   
        <body>
          <b><% out.println("Hello ACS World!"); %></b>
        </body>
   
    İndex.jsp kaydedin.

## <a name="add-hello-acs-filter-library-tooyour-application"></a>Merhaba ACS filtre kitaplık tooyour uygulaması ekleyin
1. Eclipse'nın Proje Gezgini'nde sağ **MyACSHelloWorld**, tıklatın **yapı yolu**ve ardından **oluşturma yolunu Yapılandır**.
2. Merhaba, **Java oluşturma yolu** iletişim kutusunda, hello tıklatın **kitaplıkları** sekmesi.
3. Tıklatın **Kitaplığı eklemek**.
4. Tıklatın **Azure erişim denetimi Hizmetleri filtresi (tarafından MS açık teknik)** ve ardından **sonraki**. Merhaba **Azure erişim denetimi Hizmetleri filtre** iletişim kutusu gösterilir.  (Merhaba **konumu** alan Eclipse, yüklediğiniz bağlı olarak farklı bir yol olabilir ve hello sürüm numarası, yazılım güncelleştirmelerini bağlı olarak farklı olabilir.)
   
    ![ACS filtre kitaplığı Ekle][add_acs_filter_lib]
5. Bir tarayıcı kullanılarak açılmasını toohello **oturum açma sayfası tümleştirme** hello Yönetim Portalı hello listelenen kopyalama hello URL sayfanın **seçenek 1: bağlantı tooan ACS barındırılan oturum açma sayfasına** alan ve helloyapıştırma**ACS kimlik doğrulama uç noktası** hello Eclipse iletişim alanı.
6. Bir tarayıcı kullanılarak açılmasını toohello **bağlı olan taraf uygulamayı Düzenle** hello Yönetim Portalı hello listelenen kopyalama hello URL sayfanın **bölge** alan ve hello yapıştırma **bağlı olan taraf bölgesi**  hello Eclipse iletişim alanı.
7. Merhaba içinde **güvenlik** toouse var olan bir sertifikayı istiyorsanız, hello Eclipse iletişim kutusu bölümüne tıklatın **Gözat**, toouse istediğinizi seçin ve tıklatın toohello sertifika gidin  **Açık**. Veya yeni bir sertifika toocreate istiyorsanız, **yeni** toodisplay hello **yeni sertifika** iletişim kutusunda, hello parola, hello .cer dosyasının adını ve yeni hello için hello .pfx dosyasının adını belirtin Sertifika.
8. Denetleme **Embed hello hello WAR dosyasını sertifikada**. Bu şekilde katıştırma hello sertifikası içerir gerektirmeden dağıtımınızdaki toomanually add bir bileşeni olarak. (Bunun yerine, sertifikanızı dışarıdan WAR dosyanızdan depolamanız gerekir, bir rol bileşeni olarak hello sertifika Ekle ve seçeneğinin işaretini kaldırın **Embed hello hello WAR dosyasını sertifikada**.)
9. [İsteğe bağlı] Tutmak **gerektiren HTTPS bağlantıları** işaretli. Bu seçeneği ayarlarsanız tooaccess hello HTTPS protokolünü kullanarak uygulamanız gerekir. Toorequire HTTPS bağlantıları istemiyorsanız bu seçeneği temizleyin.
10. Bir dağıtım için toohello işlem öykünücüsü, **Azure ACS filtre** ayarları benzer toohello aşağıdaki görünür.
    
    ![Bir dağıtım toohello Azure ACS filtresi ayarlarını işlem öykünücüsü][add_acs_filter_lib_emulator]
11. **Son**'a tıklayın.
12. Tıklatın **Evet** bir iletişim kutusu web.xml dosyasını oluşturulacak belirten ile birlikte sunulan olduğunda.
13. Tıklatın **Tamam** tooclose hello **Java oluşturma yolu** iletişim.

## <a name="deploy-toohello-compute-emulator"></a>Toohello işlem öykünücüsü dağıtma
1. Eclipse'nın Proje Gezgini'nde sağ **MyACSHelloWorld**, tıklatın **Azure**ve ardından **Azure için paket**.
2. İçin **proje adı**, türü **MyAzureACSProject** tıklatıp **sonraki**.
3. Bir JDK'yı seçin ve uygulama sunucusu. (Bu adımları ayrıntılı hello olarak ele alınmıştır [Hello World uygulamasının Azure için Eclipse'te oluşturma](http://msdn.microsoft.com/library/windowsazure/hh690944.aspx) öğretici).
4. **Son**'a tıklayın.
5. Merhaba tıklatın **Azure öykünücüsünde çalıştırın** düğmesi.
6. Java web uygulamanıza hello işlem öykünücüsü başladıktan sonra (geçerli bir tarayıcı oturumu ACS oturum açma testinizle karışmaması böylece) tarayıcınızın tüm örneklerini kapatın.
7. Açarak uygulamanızı çalıştırın <http://localhost: 8080/MyACSHelloWorld/> tarayıcınızda (veya <https://localhost:8080/MyACSHelloWorld/> , işaretlediyseniz **gerektiren HTTPS bağlantıları**). Sizin için bir Windows Live ID oturum sorulması sonra bağlı olan taraf uygulamanız için belirtilen toohello dönüş URL'si yapılması gerekir.
8. Uygulamanızı görüntülemeyi bitirdikten hello tıklatın **Azure öykünücüsünü sıfırlayın** düğmesi.

## <a name="deploy-tooazure"></a>TooAzure dağıtma
toodeploy tooAzure toochange hello bağlı olan taraf bölge ve dönüş URL'si için ACS ad alanınızı gerekir.

1. Merhaba hello Azure Yönetim Portalı içinde **bağlı olan taraf uygulamayı Düzenle** sayfasında, değişiklik **bölge** toobe hello dağıtılan sitenizin URL'sini. Değiştir **örnek** dağıtımınız için belirttiğiniz hello DNS adına sahip.
   
    ![Üretimde kullanım için bağlı olan taraf bölgesi][relying_party_realm_production]
2. Değiştirme **dönüş URL'si** uygulamanızın toobe hello URL. Değiştir **örnek** dağıtımınız için belirttiğiniz hello DNS adına sahip.
   
    ![Üretimde kullanım için bağlı olan taraf dönüş URL'si][relying_party_return_url_production]
3. Tıklatın **kaydetmek** güncelleştirilmiş bölümünde, bağlı olan taraf bölge ve return URL'nizi toosave değiştirir.
4. Merhaba tutmak **oturum açma sayfası tümleştirme** tarayıcınızda açık sayfasında, dışarı toocopy kısa bir süre sonra ihtiyacınız olacaktır.
5. Eclipse'nın Proje Gezgini'nde sağ **MyACSHelloWorld**, tıklatın **yapı yolu**ve ardından **oluşturma yolunu Yapılandır**.
6. Merhaba tıklatın **kitaplıkları** sekmesini tıklatın, **Azure erişim denetimi Hizmetleri filtre**ve ardından **Düzenle**.
7. Bir tarayıcı kullanılarak açılmasını toohello **oturum açma sayfası tümleştirme** hello Yönetim Portalı hello listelenen kopyalama hello URL sayfanın **seçenek 1: bağlantı tooan ACS barındırılan oturum açma sayfasına** alan ve helloyapıştırma**ACS kimlik doğrulama uç noktası** hello Eclipse iletişim alanı.
8. Bir tarayıcı kullanılarak açılmasını toohello **bağlı olan taraf uygulamayı Düzenle** hello Yönetim Portalı hello listelenen kopyalama hello URL sayfanın **bölge** alan ve hello yapıştırma **bağlı olan taraf bölgesi**  hello Eclipse iletişim alanı.
9. Merhaba içinde **güvenlik** toouse var olan bir sertifikayı istiyorsanız, hello Eclipse iletişim kutusu bölümüne tıklatın **Gözat**, toouse istediğinizi seçin ve tıklatın toohello sertifika gidin  **Açık**. Veya yeni bir sertifika toocreate istiyorsanız, **yeni** toodisplay hello **yeni sertifika** iletişim kutusunda, hello parola, hello .cer dosyasının adını ve yeni hello için hello .pfx dosyasının adını belirtin Sertifika.
10. Tutmak **Embed hello hello WAR dosyasını sertifikada** tooembed hello hello WAR dosyasını sertifikada istediğiniz olduğu varsayılarak, kontrol.
11. [İsteğe bağlı] Tutmak **gerektiren HTTPS bağlantıları** işaretli. Bu seçeneği ayarlarsanız tooaccess hello HTTPS protokolünü kullanarak uygulamanız gerekir. Toorequire HTTPS bağlantıları istemiyorsanız bu seçeneği temizleyin.
12. Dağıtım tooAzure için Azure ACS filtre ayarlarınızı benzer toohello aşağıdaki arar.
    
    ![Üretim dağıtımı için Azure ACS filtresi ayarları][add_acs_filter_lib_production]
13. Tıklatın **son** tooclose hello **düzenleme Kitaplığı** iletişim.
14. Tıklatın **Tamam** tooclose hello **MyACSHelloWorld özelliklerini** iletişim.
15. Eclipse'te hello tıklatın **tooAzure bulut yayımlama** düğmesi. Hello yapıldığı şekilde benzer toohello istemler yanıt **toodeploy uygulama tooAzure** hello bölümünü [Hello World uygulamasının Azure için Eclipse'te oluşturma](http://msdn.microsoft.com/library/windowsazure/hh690944.aspx) konu. 

Sonra web uygulamanızın dağıtılan, Kapat tüm açık tarayıcı oturumları çalıştırmak, web uygulamanızın ve, sorulması toosign toohello tarafından gönderilen ve ardından Windows Live ID kimlik bilgilerinizle bağlı olan taraf uygulamanızı URL'sini döndürür.

İşiniz bittiğinde ACS Hello World uygulamanızı kullanarak, toodelete hello dağıtım unutmayın (öğrenebilir nasıl toodelete hello bir dağıtımda [Hello World uygulamasının Azure için Eclipse'te oluşturma](http://msdn.microsoft.com/library/windowsazure/hh690944.aspx) konu).

## <a name="next_steps"></a>Sonraki adımlar
Merhaba güvenlik onaylama işlemi biçimlendirme dili (SAML) ACS tooyour uygulama tarafından döndürülen incelenmesi için bkz: [nasıl tooview SAML hello Azure erişim denetimi hizmeti tarafından döndürülen][How tooview SAML returned by hello Azure Access Control Service]. toofurther ACS'ın işlevselliği ve daha karmaşık senaryolar ile tooexperiment keşfetmek için bkz: [erişim denetimi hizmeti 2.0][Access Control Service 2.0].

Ayrıca, bu örnekte kullanılan hello **Embed hello hello WAR dosyasını sertifikada** seçeneği. Bu seçenek, basit toodeploy hello sertifika kolaylaştırır. Bunun yerine, tookeep imzalama sertifikanızın WAR dosyasını ayrı istiyorsanız, teknik aşağıdaki hello kullanabilirsiniz:

1. Merhaba içinde **güvenlik** hello bölümünü **Azure erişim denetimi Hizmetleri filtre** iletişim, türü **${env. JAVA_HOME}/mycert.cer** ve işaretini **Embed hello hello WAR dosyasını sertifikada**. (Sertifika dosyası adı farklıysa Sertifikam.cer ayarlayın.) Tıklatın **son** tooclose hello iletişim.
2. Dağıtımınızda bir bileşen olarak kopyalama hello sertifika: Eclipse'nın Proje Gezgini'nde genişletin **MyAzureACSProject**, sağ tıklayın **WorkerRole1**, tıklatın **özellikleri** , genişletin **Azure rol**, tıklatıp **bileşenleri**.
3. **Ekle**'ye tıklayın.
4. Merhaba içinde **Bileşen Ekle** iletişim:
   
   1. Merhaba, **alma** bölümü:
      1. Kullanım hello **dosya** toouse istediğiniz düğmesi toonavigate toohello sertifika. 
      2. İçin **yöntemi**seçin **kopya**.
   2. İçin **olarak adı**' hello metin kutusuna tıklayın ve hello varsayılan adı kabul edin.
   3. Merhaba, **dağıtma** bölümü:
      1. İçin **yöntemi**seçin **kopya**.
      2. İçin **toodirectory**, türü **JAVA_HOME %**.
   4. **Bileşen Ekle** iletişim benzer toohello aşağıdaki görünmelidir.
      
       ![Sertifika Bileşen Ekle][add_cert_component]
   5. **Tamam** düğmesine tıklayın.

Bu noktada, sertifikanızı dağıtımınızda eklenmesi. Hello sertifika hello WAR dosyasını katıştırmak mı bileşen tooyour dağıtım Ekle bağımsız olarak, hello açıklandığı gibi tooupload hello sertifika tooyour ad alanı gerekir Not [bir sertifika tooyour ACS ad alanıKarşıyaYükle] [ Upload a certificate tooyour ACS namespace] bölümü.

[What is ACS?]: #what-is
[Concepts]: #concepts
[Prerequisites]: #pre
[Create a Java web application]: #create-java-app
[Create an ACS Namespace]: #create-namespace
[Add Identity Providers]: #add-IP
[Add a Relying Party Application]: #add-RP
[Create Rules]: #create-rules
[Upload a certificate tooyour ACS namespace]: #upload-certificate
[Review hello Application Integration Page]: #review-app-int
[Configure Trust between ACS and Your ASP.NET Web Application]: #config-trust
[Add hello ACS Filter library tooyour application]: #add_acs_filter_library
[Deploy toohello compute emulator]: #deploy_compute_emulator
[Deploy tooAzure]: #deploy_azure
[Next steps]: #next_steps
[project website]: http://wastarterkit4java.codeplex.com/releases/view/61026
[How tooview SAML returned by hello Azure Access Control Service]: active-directory-java-view-saml-returned-by-access-control.md
[Access Control Service 2.0]: http://go.microsoft.com/fwlink/?LinkID=212360
[Windows Identity Foundation]: http://www.microsoft.com/download/en/details.aspx?id=17331
[Windows Identity Foundation SDK]: http://www.microsoft.com/download/en/details.aspx?id=4451
[Azure Management Portal]: https://manage.windowsazure.com
[acs_flow]: ./media/active-directory-java-authenticate-users-access-control-eclipse/ACSFlow.png

<!-- Eclipse-specific -->
[add_acs_filter_lib]: ./media/active-directory-java-authenticate-users-access-control-eclipse/AddACSFilterLibrary.png
[add_acs_filter_lib_emulator]: ./media/active-directory-java-authenticate-users-access-control-eclipse/AddACSFilterLibraryEmulator.png
[add_acs_filter_lib_production]: ./media/active-directory-java-authenticate-users-access-control-eclipse/AddACSFilterLibraryProduction.png

[relying_party_realm_emulator]: ./media/active-directory-java-authenticate-users-access-control-eclipse/RelyingPartyRealmEmulator.png
[relying_party_return_url_emulator]: ./media/active-directory-java-authenticate-users-access-control-eclipse/RelyingPartyReturnURLEmulator.png
[relying_party_realm_production]: ./media/active-directory-java-authenticate-users-access-control-eclipse/RelyingPartyRealmProduction.png
[relying_party_return_url_production]: ./media/active-directory-java-authenticate-users-access-control-eclipse/RelyingPartyReturnURLProduction.png
[add_cert_component]: ./media/active-directory-java-authenticate-users-access-control-eclipse/AddCertificateComponent.png
[add_jsp_file_acs]: ./media/active-directory-java-authenticate-users-access-control-eclipse/AddJSPFileACS.png
[create_acs_hello_world]: ./media/active-directory-java-authenticate-users-access-control-eclipse/CreateACSHelloWorld.png
[add_token_signing_cert]: ./media/active-directory-java-authenticate-users-access-control-eclipse/AddTokenSigningCertificate.png

