---
title: "Çoklu DRM ve erişim denetimi ile CENC: bir başvuru tasarım ve uygulama Azure ve Azure Media Services | Microsoft Docs"
description: "Nasıl toolicensing hello hakkında Microsoft® kesintisiz akış istemci bağlantı noktası oluşturma Seti öğrenin."
services: media-services
documentationcenter: 
author: willzhan
manager: cfowler
editor: 
ms.assetid: 7814739b-cea9-4b9b-8370-538702e5c615
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: willzhan;kilroyh;yanmf;juliako
ms.openlocfilehash: 033fb618650c4fbe9069d467159a8734da759bba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="cenc-with-multi-drm-and-access-control-a-reference-design-and-implementation-on-azure-and-azure-media-services"></a>Çoklu DRM ve Access Control ile CENC: Azure ve Azure Media Services Tasarım ve Uygulama Başvurusu
 
## <a name="introduction"></a>Giriş
İyi bilinen bir karmaşık görev toodesign olduğu ve DRM alt sistemi için bir OTT yapı veya çevrimiçi çözüm akış. Ve ortak bir uygulama işleçleri/çevrimiçi video sağlayıcıları toooutsource için bu bölümü toospecialized DRM hizmet sağlayıcıları. Merhaba, bu belgenin toopresent başvuru tasarımı ve uygulama OTT veya çevrimiçi akış çözüm uçtan uca DRM alt sisteminin hedeftir.

Bu belgenin hedeflenen hello okuyucular DRM Subsystem OTT veya çevrimiçi akış/çok-screen çözümleri ya da tüm okuyucular DRM alt sisteminde ilgilenen çalışma mühendisleri ' dir. Merhaba okuyucular hello DRM teknolojileri PlayReady, Widevine, FairPlay veya Adobe erişim gibi hello piyasadaki en az biri alışık olduğunuz varsayılır.

DRM tarafından biz de çoklu DRM ile CENC (ortak şifreleme) içerir. Çevrimiçi akış ve OTT endüstri önemli bir eğilimi vardiya çoklu DRM ve kendi İstemci SDK çeşitli istemci platformları için kullanarak, önceki eğilimi hello da hangi çok-native DRM çeşitli istemci platformlarında ile CENC toouse olmasıdır. CENC çok-native DRM ile kullanırken, PlayReady ve Widevine hello şifrelenir [ortak şifreleme (ISO/IEC 23001-7 CENC)](http://www.iso.org/iso/home/store/catalogue_ics/catalogue_detail_ics.htm?csnumber=65271/) belirtimi.

Çoklu DRM ile CENC Hello avantajları aşağıdaki gibidir:

1. Şifreleme tek şifreleme işleme kendi yerel DRMs ile farklı platformları hedefleme kullanıldığından maliyeti azaltır;
2. Yalnızca tek bir kopyasını şifrelenmiş varlıklar gerekli olmadığından şifrelenmiş varlıklarını yönetme hello maliyetini azaltır;
3. DRM istemci Hello yerel DRM istemci kendi yerel platformda genellikle boş olduğundan maliyet lisansı ortadan kaldırır.

Microsoft, kısa çizgi ve CENC etkin bir promoter bazı önemli endüstri oynatıcıları birlikte olmuştur. Microsoft Azure Media Services, tire ve CENC desteği sağlama. Son Duyurular için lütfen Mingfei'nın Bloglara bakın: [tanışın Google Widevine lisans teslim hizmetleri Azure Media Services](https://azure.microsoft.com/blog/announcing-general-availability-of-google-widevine-license-services/), ve [Azure Media Services ekler çoklu DRM akış teslim etmek için Google Widevine paketlemeyi](https://azure.microsoft.com/blog/azure-media-services-adds-google-widevine-packaging-for-delivering-multi-drm-stream/).  

### <a name="overview-of-this-article"></a>Bu makalede genel bakış
Bu makalede Hello amacı hello aşağıdakileri içerir:

1. Çoklu DRM ile CENC kullanarak DRM alt sisteminin başvuru tasarımı sağlar;
2. Bir başvuru uygulaması, Microsoft Azure/Azure Media Services platformda sağlar;
3. Bazı tasarım ve uygulama konuları anlatılmaktadır.

Merhaba makalesinde "çoklu DRM" Merhaba aşağıdakileri kapsar:

1. Microsoft PlayReady
2. Google Widevine
3. Apple FairPlay 

Merhaba aşağıdaki tabloda hello yerel platform/yerel uygulama ve her DRM tarafından desteklenen Gözatıcıların özetlenmektedir.

| **İstemci Platformu** | **Yerel DRM desteği** | **Tarayıcı/uygulaması** | **Akış biçimlerine** |
| --- | --- | --- | --- |
| **Akıllı TV, işleci STB, OTT STB** |PlayReady öncelikle, ve/veya Widevine ve/veya diğer |Linux, Opera, WebKit, diğer |Çeşitli biçimleri |
| **Windows 10 cihazları (Windows PC, Windows tabletler, Windows Phone, Xbox)** |PlayReady |MS kenar/IE11/EME<br/><br/><br/>UWP |TİRE (HLS için PlayReady desteklenmez)<br/><br/>DASH, kesintisiz akış (HLS için PlayReady desteklenmez) |
| **Android cihazlar (telefon, Tablet, TV)** |Widevine |Chrome/EME |DASH, HLS |
| **iOS (iPhone, iPad), OS X istemcileri ve Apple TV** |FairPlay |Safari 8 +/ EME |HLS |


Merhaba geçerli durumunu dağıtım her DRM için göz önünde bulundurularak, bir hizmet genellikle 2 veya 3 tooimplement DRMs toomake hello en iyi uç noktalarını tüm hello türleri adres emin isteyeceksiniz yolu.

Hello hizmet mantığı hello karmaşıklığını arasında bir kolaylığını yoktur ve hello istemci tarafı tooreach kullanıcı belirli bir düzeyde hello kapsamına çeşitli istemciler üzerinde hello karşılaşırsınız.

toomake içinde kalmasını seçiminiz şunları aklınızda bu bilgiler:

* PlayReady ve neredeyse her platformda yazılım SDK aracılığıyla kullanılabilen bazı Android cihazlarda, her Windows aygıt yerel olarak uygulanan
* Widevine her Android cihazı, Chrome ve diğer bazı cihazların yerel olarak uygulanır
* FairPlay yalnızca iOS ve Mac OS istemciler veya iTunes aracılığıyla kullanılabilir.

Bu nedenle, tipik bir çoklu DRM olacaktır:

* Seçenek 1: PlayReady ve Widevine
* Seçenek 2: PlayReady, Widevine ve FairPlay

## <a name="a-reference-design"></a>Bir başvuru tasarımı
Bu bölümde, biz kullanılan belirsiz tootechnologies tooimplement olan bir başvuru tasarımı sunacaktır onu.

DRM alt sistemi bileşenleri aşağıdaki hello içerebilir:

1. Anahtar Yönetimi
2. DRM paketleme
3. DRM lisansı verme
4. Yetkilendirme denetimi
5. Kimlik doğrulama/yetkilendirme
6. Player
7. Kaynak/CDN

Merhaba Aşağıdaki diyagramda hello yüksek düzey etkileşim DRM alt sistemi hello bileşenler arasında gösterilmektedir.

![DRM alt sistemi ile CENC](./media/media-services-cenc-with-multidrm-access-control/media-services-generic-drm-subsystem-with-cenc.png)

Merhaba tasarımında üç temel "katmanları" vardır:

1. Harici olarak gösterilmeyen arka ofis Katmanı ('Siyah);
2. Genel kullanıma yönelik tüm hello uç noktaları içeren "DMZ" katman (mavi);
3. CDN ve trafik oyuncularla ortak Internet üzerinden içeren ortak Internet katman (mavi).

DRM koruma denetlemek için bir içerik yönetim aracı olmalıdır, ne olursa olsun statik veya dinamik şifreleme olduğundan. DRM şifreleme Hello girdileri içermelidir:

1. MBR video içeriği;
2. İçerik anahtarı;
3. Lisans edinme URL'leri.

Kayıttan yürütme zamanı sırasında hello yüksek düzey akış sunar:

1. Kullanıcının kimliği doğrulanır;
2. Yetkilendirme belirtecini hello kullanıcı için oluşturulur;
3. DRM korumalı içeriği (bildirim) indirilen tooplayer,
4. Player gönderir lisans edinme isteği toolicense sunucuları ile birlikte anahtar kimliği ve yetkilendirme belirteci.

Taşıma toohello sonraki konuyu önce anahtar yönetimi hello hakkında birkaç sözcük tasarlayın.

| **ContentKey – varlık** | **Senaryo** |
| --- | --- |
| 1 – 1 |Merhaba en basit durumda. Merhaba en belirgin denetim sağlar. Ancak bu genelde yüksek lisans teslimat maliyeti hello sonuçlanır. En az bir lisans isteği korunan her varlık için gereklidir. |
| 1 – çok |İçerik aynı anahtar için birden çok varlığı hello kullanabilirsiniz. Örneğin, bir tarzını veya bir alt kümesini Tarz (veya film Gene) gibi mantıksal bir gruptaki tüm hello varlıklar için tek bir içerik anahtarı kullanabilirsiniz. |
| Çok – 1 |Birden çok içerik anahtarı her varlık için gereklidir. <br/><br/>Örneğin, MPEG DASH ve HLS için dinamik AES-128 şifrelemesi tooapply dinamik CENC koruma çoklu DRM ile ihtiyacınız varsa, iki farklı içerik anahtarları, her biri kendi ContentKeyType gerekir. (Dinamik CENC koruma için kullanılan hello içerik anahtarını, ContentKeyType.CommonEncryption, hello sırada ContentKeyType.EnvelopeEncryption dinamik AES-128 şifrelemesi için kullanılacak anahtarı kullanılması gereken içerik için kullanılması gerekir.)<br/><br/>Başka bir örnekte, tire CENC korumasını içerik, teorik olarak, bir içerik anahtarı kullanılan tooprotect video akışına ve başka bir içerik anahtarı tooprotect ses akışı olabilir. |
| Çok-çok-çok |İki senaryo yukarıda hello birleşimi: bir içerik kümesinin başarısızlığını anahtarları her biri için kullanılır, aynı varlık "grubu" Merhaba birden çok varlıkları hello. |

Başka bir önemli faktör tooconsider kalıcı ve kalıcı olmayan lisansları hello kullanılır.

Bu noktalar neden önemlidir?

Lisans teslimat için genel bulut kullanırsanız, Maliyet doğrudan etkisi toolicense teslim sahiptirler. Şimdi iki farklı tasarım durumlarda tooillustrate aşağıdaki hello göz önünde bulundurun:

1. Aylık abonelik: kalıcı lisans ve 1-çok içerik anahtarı varlık eşleme kullanın. Örneğin Tüm hello çocuklar filmler için tek bir içerik anahtarı şifreleme için kullanın. Bu durumda:

    Toplam tüm çocuklar filmler/aygıt için istenen # lisans = 1
2. Aylık abonelik: kalıcı olmayan lisans ve içerik anahtarı ve varlık arasında 1-1 eşleme kullanın. Bu durumda:

    Toplam tüm çocuklar filmler/aygıt için istenen # lisans [# filmler izlenen] = [# oturumları] x

Kolayca görebileceğiniz gibi iki farklı tasarımları çok farklı lisans neden hello lisans teslimat hizmeti Azure Media Services gibi genel bulut tarafından sağlanıyorsa maliyet lisans teslimat bu nedenle desenleri isteyin.

## <a name="mapping-design-tootechnology-for-implementation"></a>Uygulama için eşleme tasarım tootechnology
Ardından, biz her Yapı bloğu için hangi teknoloji toouse belirterek bizim genel tasarım tootechnologies Microsoft Azure/Azure Media Services platformunda eşleyin.

Merhaba aşağıdaki tabloda hello eşleme gösterilmektedir:

| **Yapı Taşı** | **Teknoloji** |
| --- | --- |
| **Player** |[Azure Media Player](https://azure.microsoft.com/services/media-services/media-player/) |
| **Kimlik sağlayıcıyı (IDP)** |Azure Active Directory |
| **Güvenli belirteç hizmeti (STS)** |Azure Active Directory |
| **DRM koruma iş akışı** |Dinamik koruma Azure medya Hizmetleri |
| **DRM lisans teslimat** |1. Azure Media Services lisans teslimat (PlayReady, Widevine, FairPlay) veya <br/>2. Axinom lisans sunucusu <br/>3. Özel PlayReady lisans sunucusu |
| **Kaynak** |Akış uç Azure medya Hizmetleri |
| **Anahtar Yönetimi** |Başvuru uygulaması için gerekli değil |
| **İçerik Yönetimi** |Bir C# konsol uygulaması |

Diğer bir deyişle, kimlik sağlayıcısı (IDP) ve güvenli belirteç hizmeti (STS) Azure AD olacaktır. Player için kullanacağız [Azure Media Player API](http://amp.azure.net/libs/amp/latest/docs/). Azure Media Services ve Azure Media Player çoklu DRM ile DASH ve CENC destekler.

Aşağıdaki diyagramda gösterildiği hello teknolojisi eşleme yukarıda hello ile genel yapısını ve akış hello.

![AMS üzerinde CENC](./media/media-services-cenc-with-multidrm-access-control/media-services-cenc-subsystem-on-AMS-platform.png)

Dinamik CENC şifrelemenin sipariş tooset içinde girişleri aşağıdaki hello hello içerik yönetimi aracını kullanır:

1. Açık içerik;
2. Anahtarından içerik anahtarı oluşturma/Yönetim;
3. Lisans edinme URL'leri;
4. Azure AD'den bilgi listesi.

Merhaba çıktı hello içerik Yönetim Aracı'nın olacaktır:

1. JWT belirteci ve DRM lisans belirtimleri lisans teslimat nasıl doğrular üzerinde hello belirtimi içeren ContentKeyAuthorizationPolicy;
2. Biçim, DRM koruma ve lisans edinme URL'leri akış üzerinde belirtimleri içeren AssetDeliveryPolicy.

Çalışma zamanı sırasında hello olarak akışıdır altında:

1. Kullanıcı kimlik doğrulaması sırasında bir JWT belirteci oluşturulur;
2. Merhaba talep hello JWT belirtecinde yer alan "grupları" talep "EntitledUserGroup" Merhaba grup nesne Kimliğini içeren biridir. Bu talep "yetkilendirme onay" geçirmek için kullanılır.
3. Bir CENC Player yüklemeleri istemci bildirimi, korumalı içeriği ve "hello aşağıdaki görür":

   1. anahtar kimliği,
   2. Merhaba, korumalı CENC içeriktir,
   3. Lisans edinme URL'leri.
4. Player hello tarayıcı/desteklenen DRM üzerinde temel lisans edinme isteğinde bulunur. Merhaba lisans edinme isteği, anahtar kimliği ve hello JWT belirteci da gönderilir. Lisans teslimat hizmeti hello JWT belirteci ve hello veren lisans gerekli önce yer alan hello talep doğrular.

## <a name="implementation"></a>Uygulama
### <a name="implementation-procedures"></a>Uygulama yordamları
Merhaba uygulama hello aşağıdaki adımları içerir:

1. Test kıymetlerin hazırlayın: kodlama/paketi bir test video toomulti bit hızlı parçalanmış MP4 Azure Media Services. Bu varlık DRM korumalı değil. DRM korumasını daha sonra dinamik Koruması tarafından yapılır.
2. Anahtar kimliği ve içerik oluşturma (isteğe bağlı olarak gelen anahtar seed) anahtarı. Biz yalnızca tek bir dizi ile çalışıyorsanız olmadığından bu konudaki Hedefimiz için anahtar yönetimi sistemi gerekli değildir anahtar kimliği ve içerik anahtarı birkaç test varlıklar;
3. AMS API tooconfigure çoklu DRM lisans teslimat hizmetlerini hello test varlık için kullanın. Şirketiniz veya Azure Media Services lisans Hizmetleri'nde yerine şirketinizin satıcıları tarafından özel lisans sunucuları kullanıyorsanız, bu adımı atlayın ve lisans teslimat yapılandırma hello adımda lisans edinme URL'leri belirtin. AMS API'dir gerekli toospecify bazı ayrıntılı yetkilendirme ilkesi kısıtlama gibi yapılandırmaları lisans farklı DRM lisans Hizmetleri, vb. için yanıt şablonları. Şu anda hello Azure portal yok henüz hello UI bu yapılandırma için gerekli sağlayın. API düzeyi bilgileri bulmak ve örnek koduna Jale Kornich'ın belgedeki: [kullanarak PlayReady ve/veya Widevine dinamik ortak şifreleme](media-services-protect-with-drm.md).
4. AMS API tooconfigure varlık teslim ilkesini hello test varlık için kullanın. API düzeyi bilgileri bulmak ve örnek koduna Jale Kornich'ın belgedeki: [kullanarak PlayReady ve/veya Widevine dinamik ortak şifreleme](media-services-protect-with-drm.md).
5. Oluşturma ve Azure Active Directory kiracısı Azure'da yapılandırın;
6. Birkaç kullanıcı hesapları ve grupları, Azure Active Directory kiracınızda oluşturun: en az oluşturmalısınız "EntitledUser" Grup ve kullanıcı toothis grubunu ekleyin. Bu gruptaki kullanıcılar lisans edinme yetkilendirme denetimi başarılı ve bu gruptaki kullanıcılar toopass kimlik doğrulama denetimi başarısız olur ve mümkün tooacquire herhangi bir lisans olmaz. Bu "EntitledUser" grubunun bir üyesi olması gereken "grupları" talep Azure AD tarafından verilen hello JWT belirteci olur. Çoklu DRM lisans teslimat hizmetlerini adım yapılandırmada bu talep gereksinim belirtilmelidir.
7. Video oynatıcı barındıran bir ASP.NET MVC uygulaması oluşturursunuz. Bu ASP.NET uygulamasını kullanıcı kimlik doğrulamasıyla hello Azure Active Directory Kiracı karşı korunur. Uygun talep kullanıcı kimlik doğrulamasından sonra elde hello erişim belirteçleri eklenecektir. Openıd Connect API, bu adım için önerilir. NuGet paketleri aşağıdaki tooinstall hello gerekir:
   * Install-Package Microsoft.Azure.ActiveDirectory.GraphClient
   * Install-Package Microsoft.Owin.Security.OpenIdConnect
   * Install-Package Microsoft.Owin.Security.Cookies
   * Install-Package Microsoft.Owin.Host.SystemWeb
   * Install-Package Microsoft.IdentityModel.Clients.activedirectory tarafından
8. Kullanarak bir oynatıcı oluşturmak [Azure Media Player API](http://amp.azure.net/libs/amp/latest/docs/). [Azure Media Player'ın ProtectionInfo API](http://amp.azure.net/libs/amp/latest/docs/) toospecify sağlayan farklı DRM platformunda hangi DRM teknolojisi toouse.
9. Testi matris:

| **DRM** | **Tarayıcı** | **Yetkili kullanıcı için sonuç** | **Sonuç beklemediğiniz yetkili bir kullanıcı için** |
| --- | --- | --- | --- |
| **PlayReady** |MS kenar veya Windows 10 IE11 |Başarılı |Başarısız |
| **Widevine** |Windows 10 Chrome |Başarılı |Başarısız |
| **FairPlay** |TBD | | |

Azure Media Services ekibine George Trifonov Azure Active Directory için bir ASP.NET MVC oynatıcı uygulaması ayarlama hakkında ayrıntılı adımlar sağlayan bir blog yazma: [tümleştirmek Azure Media Services OWIN MVC uygulama Azure Active Directory ile temel ve JWT talepleri temelinde içerik anahtar teslim kısıtlamak](http://gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).

George da yazılmış bir blog üzerinde [JWT belirteci kimlik doğrulaması Azure Media Services ve dinamik şifreleme](http://gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/). Burada da kaldırmalıdır [Azure Media Services anahtar teslim Azure AD tümleştirme örnek](https://github.com/AzureMediaServicesSamples/Key-delivery-with-AAD-integration/).

Azure Active Directory hakkında daha fazla bilgi için:

* Geliştirici bilgiler bulabilirsiniz [Azure Active Directory Geliştirici Kılavuzu](../active-directory/active-directory-developers-guide.md).
* Yönetici bilgileri bulabilirsiniz [yönetmek bilgisayarınızı Azure AD dizini](../active-directory/active-directory-administer.md).

### <a name="some-gotchas-in-implementation"></a>Uygulamasındaki bazı FRİKİKLERİNDEN
Merhaba uygulamasında bazı "FRİKİKLERİNDEN" vardır. Neyse "FRİKİKLERİNDEN" listesi aşağıdaki hello sorunla çalışması durumunda sorun giderme yardımcı olabilir.

1. **Veren** URL ile bitmelidir **"/"**.  

    **Hedef kitle** player uygulama istemci Kimliğini hello ve de eklemeniz gerekir olmalıdır **"/"** hello sonunda hello veren URL'si.

        <add key="ida:audience" value="[Application Client ID GUID]" />
        <add key="ida:issuer" value="https://sts.windows.net/[AAD Tenant ID]/" />

    İçinde [JWT Decoder](http://jwt.calebb.net/), görmeniz gerekir **aud** ve **ISS** hello JWT belirteci olarak aşağıda içinde:

    ![1. sorunu](./media/media-services-cenc-with-multidrm-access-control/media-services-1st-gotcha.png)
2. (İzinleri toohello uygulama AAD'de yapılandırma sekmesinde hello uygulamasının) ekleyin. Bu, her uygulama için (yerel ve dağıtılan sürümler) gereklidir.

    ![2 sorunu](./media/media-services-cenc-with-multidrm-access-control/media-services-perms-to-other-apps.png)
3. Dinamik CENC koruma kurulumuna içinde doğru veren hello kullan:

        <add key="ida:issuer" value="https://sts.windows.net/[AAD Tenant ID]/"/>

    Merhaba aşağıdakiler çalışmaz:

        <add key="ida:issuer" value="https://willzhanad.onmicrosoft.com/" />

    Merhaba GUID hello AAD Kiracı kimliğidir. Merhaba GUID uç noktaları açılan penceresinde Azure Portalı'nda bulunabilir.
4. GRANT grup üyeliği ayrıcalıkları talepleri. AAD uygulama bildirim dosyasında emin olun, biz hello aşağıdakilere sahip

    "groupMembershipClaims": "Tümü", (Merhaba varsayılan değeri null)
5. Uygun TokenType kısıtlama gereksinimleri oluştururken ayarlama.

        objTokenRestrictionTemplate.TokenType = TokenType.JWT;

    Ekleme desteği JWT (AAD) bu yana ayrıca tooSWT (ACS), hello TokenType TokenType.JWT varsayılandır. SWT/ACS kullanırsanız tooTokenType.SWT ayarlamanız gerekir.

## <a name="additional-topics-for-implementation"></a>Uygulama için ek konular
Sonraki biz uss bazı ek konular tasarım ve uygulama disk.

### <a name="http-or-https"></a>HTTP veya HTTPS?
Merhaba oluşturduğumuz ASP.NET MVC oynatıcı uygulaması hello aşağıdaki desteklemesi gerekir:

1. Kullanıcı kimlik doğrulaması HTTPS altında toobe gereken Azure AD ile;
2. JWT belirteci exchange HTTPS altında toobe gereken Azure AD ile istemci arasında;
3. Lisans teslimat Azure Media Services tarafından sağlanıyorsa, gerekli toobe HTTPS altında olan hello istemci tarafından DRM lisans edinme. Elbette, PlayReady ürün paketini HTTPS lisans teslimat için zorunlu kılabilir değil. PlayReady lisans sunucunuz Azure Media Services dışında ise, HTTP veya HTTPS kullanılabilir.

Bu nedenle, hello ASP.NET oynatıcı uygulaması en iyi uygulama olarak HTTPS kullanır. Bu, Azure Media Player sayfasında HTTPS altında olacak hello anlamına gelir. Ancak, akış için biz HTTP tercih ederseniz, bu nedenle karışık içerik sorunu tooconsider ihtiyacımız.

1. Tarayıcı karışık içeriğe izin vermiyor. Ancak eklentileri kesintisiz için Silverlight ve OSMF eklentisi ve çizgi gibi izin verin. Karışık içerik güvenlik sorunu - bu toohello tehlike hello özelliği tooinject müşteri verileri toobe risk neden kötü amaçlı JS hello.  Tarayıcılar bu varsayılan olarak engelliyor ve o ana kadarki hello tek yolu toowork çevresinde hello (kaynak) sunucu tarafı, tooallow tüm etki alanları (bakılmaksızın https veya http) olur. Bu bir ya da fikirdir olmayabilir.
2. Karışık içerik kaçınmanız gerekir: her ikisi de HTTP kullanabilir veya her ikisi de HTTPS kullanır. Karışık içerik yürütürken silverlightSS teknik bir karışık içerik uyarı temizlenmesini gerektirir. flashSS teknik karışık içerik uyarmadan karışık içerik işler.
3. Akış uç noktanızı Ağustos 2014 önce oluşturulduysa, HTTPS desteklemez. Bu durumda, lütfen oluşturun ve yeni bir akış uç noktası için HTTPS kullanın.

Merhaba başvuru uygulamasında DRM korumalı içeriği için uygulama ve akış HTTTPS altında olacaktır. Her iki HTTP hello özgürlük toouse alacak şekilde açık içeriği için hello player kimlik doğrulaması veya lisansı gerekmez veya HTTPS.

### <a name="azure-active-directory-signing-key-rollover"></a>Anahtar geçişi imzalama Azure Active Directory
Uygulamanızın dikkate önemli bir nokta tootake budur. Uygulamanızda bu katmazsanız tamamlandı hello sistem sonunda tamamen en çok 6 hafta içinde çalışmayı durdurur.

Azure AD kendisi ve Azure AD kullanarak uygulamalar arasında endüstri standart tooestablish güven kullanır. Özellikle, Azure AD genel ve özel bir anahtar çiftinden oluşur bir imzalama anahtarı kullanır. Azure AD hello kullanıcı hakkındaki bilgileri içeren bir güvenlik belirteci oluşturduğunda, bu belirteç geri toohello uygulama gönderilmeden önce özel anahtarını kullanarak Azure AD tarafından imzalanır. belirteç hello tooverify geçerli ve gerçekte kaynaklı Azure AD'den, Merhaba uygulaması hello kiracının Federasyon meta veri belgesi içinde yer alan Azure AD tarafından sunulan hello ortak anahtarı kullanılarak hello belirtecinin imzası doğrulamanız gerekir. Bu ortak anahtarı – ve imzalama anahtarı kendisinden türetilen hello – hello Azure AD'de tüm kiracılar için kullanılan aynı olur.

Azure AD anahtar geçişi hakkında ayrıntılı bilgiler hello belgesinde bulunabilir: [imzalama anahtarı Rollover Azure AD'de hakkında önemli bilgiler](../active-directory/active-directory-signing-key-rollover.md).

Merhaba arasında [genel-özel anahtar çifti](https://login.microsoftonline.com/common/discovery/keys/),

* Merhaba özel anahtarı kullanılır tarafından Azure Active Directory toogenerate bir JWT belirteci;
* Merhaba ortak anahtar AMS tooverify hello JWT belirteci DRM lisans teslimat hizmetlerini gibi uygulama tarafından kullanılır;

Güvenlik amaç için Azure Active Directory bu sertifikayı düzenli aralıklarla (6 haftada) döndürür. Güvenlik ihlallerini durumunda hello anahtar geçişi dilediğiniz zaman ortaya çıkabilir. Bu nedenle, AMS lisans teslim hizmetleri hello Azure AD hello anahtar çifti döndürür, aksi takdirde AMS belirteci kimlik doğrulaması başarısız olur ve hiçbir lisans verilecek olarak kullanılan tooupdate hello ortak anahtar gerekir.

Bu, DRM lisans teslimat hizmetlerini yapılandırırken TokenRestrictionTemplate.OpenIdConnectDiscoveryDocument ayarlayarak sağlanır.

Merhaba JWT belirteci akışı olduğu olarak aşağıda:

1. Azure AD hello kimliği doğrulanmış bir kullanıcı için geçerli özel anahtarı olan hello JWT belirteci vermek;
2. Bir oyuncu çoklu DRM korumalı içeriği ile CENC gördüğünde, ilk Azure AD tarafından verilen hello JWT belirteci bulacaktır.
3. Merhaba player içinde AMS lisans edinme isteği hello JWT belirteci toolicense teslim Hizmetleri ile gönderir;
4. Merhaba lisans teslim hizmetleri AMS lisans vermeden önce geçerli/geçerli ortak anahtar Azure AD tooverify hello JWT belirteci hello kullanır.

DRM lisans teslimat hizmetlerini hello geçerli/geçerli ortak anahtar, Azure AD'den için her zaman denetleniyor. Azure AD tarafından sunulan hello ortak anahtar Azure AD tarafından verilen JWT belirteci doğrulamak için kullanılan hello anahtar olacaktır.

Ne hello anahtar geçişi sonra AAD JWT belirteci oluşturur ama hello önce JWT belirteci oynatıcıları tooDRM lisans teslim hizmetleri AMS doğrulama tarafından gönderilen olur?

Herhangi bir anda bir anahtar alınması çünkü her zaman birden fazla geçerli ortak anahtar hello Federasyon meta veri belgesi mevcut değil. Azure Media Services lisans teslimat anahtarları belirtilen hello belgede bir anahtar yakında geri alınması beri başka değişimi olması ve benzeri hello birini kullanabilirsiniz.

### <a name="where-is-hello-access-token"></a>Burada olan hello erişim belirteci?
Bir web uygulaması altında bir API uygulamasını nasıl çağıran en baktığınızda [uygulama kimliği OAuth 2.0 istemci kimlik bilgilerini verme ile](../active-directory/develop/active-directory-authentication-scenarios.md#web-application-to-web-api), hello kimlik doğrulaması akışı olduğu olarak aşağıda:

1. TooAzure AD hello web uygulamasında kullanıcı oturumu açık (Merhaba bkz [Web tarayıcısı tooWeb uygulama](../active-directory/develop/active-directory-authentication-scenarios.md#web-browser-to-web-application).
2. Hello Azure AD yetkilendirme uç noktası hello kullanıcı aracısı geri toohello istemci uygulaması bir yetkilendirme kodu ile yeniden yönlendirir. Merhaba kullanıcı aracısı yetkilendirme kodu toohello istemci uygulamanın yeniden yönlendirme URI'si döndürür.
3. Böylece toohello web API kimlik doğrulaması ve istenen hello kaynak almak hello web uygulamasının tooacquire bir erişim belirteci gerekiyor. Merhaba kimlik bilgisi, istemci kimliği ve web API uygulama kimliği URI'si sağlama isteği tooAzure Reklamın belirteç uç noktası kolaylaştırır. Bu hello hello yetkilendirme kodu tooprove sunar kullanıcı rıza.
4. Azure AD hello uygulama kimliğini doğrular ve kullanılan toocall hello web API'sini bir JWT erişim belirtecini döndürür.
5. HTTPS üzerinden hello web uygulaması JWT erişim belirteci tooadd hello "Bearer" tayin JWT dizesiyle hello yetkilendirme üstbilgisinde hello isteği toohello Web API döndürülen hello kullanır. Merhaba web API sonra hello JWT belirteci doğrular ve doğrulama başarılı olursa, kaynak döndürür hello istenen.

Bu "uygulama kimliği" akışında hello web API hello web uygulama kimliği doğrulanmış hello kullanıcının güvenir. Bu nedenle, bu deseni güvenilir alt sistem adı verilir. Merhaba [diyagram, bu sayfada](https://docs.microsoft.com/azure/active-directory/active-directory-protocols-oauth-code) nasıl yetki kodu izin akışı works açıklar.

Lisans edinme belirteç kısıtlamasına'de, biz hello takip aynı güvenilir alt sistem düzeni. Ve Azure Media Services hello lisans teslimat hizmetinin hello web API kaynak, "arka uç kaynak" Merhaba tooaccess bir web uygulaması gerekiyor. Bu nedenle hello erişim belirteci nerede?

Aslında, biz erişim belirteci Azure AD'den alma. Kullanıcı başarıyla kimlik doğrulamasından sonra yetkilendirme kodu döndürülür. Merhaba yetkilendirme kodu daha sonra istemci kimliği ve uygulama anahtarı, tooexchange erişim belirteci ile birlikte kullanılır. Ve hello erişim belirteci "işaretçi" gösteren uygulama erişme veya Azure Media Services lisans teslimat hizmeti temsil eden için.

Biz tooregister gerekir ve hello adımları izleyerek Azure AD'de hello "işaretçi" uygulamayı yapılandırabilirsiniz:

1. Hello Azure AD kiracısında

   * oturum açma URL'si ile bir uygulama (kaynak) ekleyin:

   https://[resource_name].azurewebsites.NET/ ve

   * Uygulama Kimliği URL'si:

   https://[aad_tenant_name].onmicrosoft.com/[resource_name];
2. Merhaba kaynak uygulama için yeni bir anahtar ekleyin;
3. Aşağıdaki değeri hello Hello groupMembershipClaims özelliğine sahip olması hello uygulama bildirim dosyasını güncelleştirin: "groupMembershipClaims": "Tümü",  
4. "İzinleri tooother uygulamaları" Merhaba bölümündeki toohello player web uygulaması işaret eden hello Azure AD uygulaması yukarıdaki 1. adımda eklenen hello kaynak uygulama ekleyin. "İzinleri atanmış altında", "Erişim [resource_name]" onay işaretine denetleyin. Bu hello web uygulama izni toocreate erişim belirteçleri hello kaynak uygulama erişmek için sağlar. Visual Studio ve Azure web uygulaması geliştiriyorsanız hello web uygulaması hem yerel hem de dağıtılan sürümü için bunu yapmalısınız.

Bu nedenle Azure AD tarafından verilen hello JWT belirteci gerçekten bu "işaretçi" kaynağa erişmek için erişim belirteci hello olur.

### <a name="what-about-live-streaming"></a>Canlı ne akış?
Yukarıdaki Hello içinde bizim tartışma isteğe bağlı varlıklar üzerinde odaklanan. Ne hakkında canlı akış?

Merhaba müjde, tam olarak kullanabileceğiniz olduğu aynı tasarım ve canlı Azure Media Services'de akış "VOD varlık" olarak bir programla ilişkili hello varlık düşünerek korunması için uygulama hello.

Özellikle, toodo canlı akış Azure Media Services, bir kanal sonra bir program hello kanal altında toocreate gerek tanınmış. toocreate hello program toocreate hello Canlı arşiv hello program için yer alacağı bir varlık gerekir. Çoklu DRM koruması hello dinamik içerik, tüm toodo, ihtiyacınız olan sipariş tooprovide CENC içinde olduğu tooapply hello aynı kurulum/işleme toohello varlık hello program başlamadan önce bunu "VOD varlık" boşmuş gibi.

### <a name="what-about-license-servers-outside-of-azure-media-services"></a>Lisans sunucuları Azure Media Services dışında nasıldır?
Genellikle, müşteriler kendi veri merkezi ya da barındırılan lisans sunucu grubundaki DRM hizmet sağlayıcıları tarafından yatırım yapmış kullanıcılar. Neyse ki, Azure medya Hizmetleri içerik koruma toooperate karma modda sağlar: içeriği barındırılan ve Azure Media Services dışında sunucuları tarafından DRM lisansları teslim ederken dinamik olarak Azure Media Services ile korumalı. Bu durumda, değişiklikleri hususlara aşağıdaki hello vardır:

1. kabul edilebilir olan ve hello lisans sunucusu grubu tarafından doğrulanabilir hello güvenli belirteç hizmeti gereksinimlerini tooissue belirteçleri. Örneğin, Axinom tarafından sağlanan hello Widevine lisans sunucuları "yetkilendirme ileti" içeren belirli bir JWT belirteci gerektirir. Bu nedenle, bu tür JWT belirteci toohave bir STS tooissue gerekir. Hello yazarlar gibi bir uygulama tamamlanmıştır ve belgede aşağıdaki hello hello ayrıntıları bulabilirsiniz [Azure Belge Merkezi'nde](https://azure.microsoft.com/documentation/): [kullanarak Axinom toodeliver Widevine lisansları tooAzure Media Services](media-services-axinom-integration.md).
2. Artık Azure Media Services tooconfigure lisans teslimat hizmetinin (ContentKeyAuthorizationPolicy) gerekmez. Gerekenler toodo olan tooprovide hello lisans edinme (PlayReady, Widevine ve URL'leri FairPlay) çoklu DRM ile CENC ayarı AssetDeliveryPolicy yapılandırırken.

### <a name="what-if-i-want-toouse-a-custom-sts"></a>Ne toouse özel bir STS istiyorum?
Bir müşteri, JWT belirteçleri sağlamak için toouse özel STS (güvenli belirteç hizmeti) seçebilir birkaç nedeni olabilir. Bunlardan bazıları şunlardır:

1. Merhaba kimlik sağlayıcısı (IDP) hello müşteri tarafından kullanılan STS desteklemez. Bu durumda özel bir STS bir seçenek olabilir.
2. Merhaba Müşteri daha esnek ya da daha sıkı STS faturalama sisteminize müşterinin aboneye tümleştirme kontrol gerekebilir. Örneğin, premium, basic, spor gibi bir MVPD işleci birden çok OTT abone paket sunabilir, yalnızca hello sağ paket içeriğini yapıldığında böylece kullanılabilir vb. hello işleci toomatch hello talep belirteci bir abonenin paketiyle isteyebilirsiniz. Bu durumda, özel bir STS sağlar esneklik ve denetim hello gerekli.

İki değişiklik özel bir STS'ye kullanılırken yapılan toobe gerekir:

1. Bir varlık için lisans teslimat hizmeti yapılandırırken, Azure Active Directory'den geçerli anahtar hello yerine hello özel STS (daha fazla ayrıntı aşağıdadır) tarafından doğrulama için kullanılan toospecify hello güvenlik anahtarı gerekir.
2. JTW belirteç oluşturulduğunda Azure Active Directory'de hello geçerli X509 sertifikasının özel anahtarı hello yerine bir güvenlik anahtarı belirtilmiş.

Güvenlik anahtarları iki tür vardır:

1. Simetrik anahtar: hello aynı anahtar oluşturma hem bir JWT belirteci; doğrulamak için kullanılır
2. Asimetrik anahtar: sertifika hello belirteci doğrulamak için bir JWT belirteci ve hello ortak anahtar şifreleme/oluşturmak için özel anahtar olarak kullanılan bir X509 bir genel-özel anahtar çifti.

#### <a name="tech-note"></a>Teknik Not
.NET Framework'te kullanıyorsanız / C# geliştirme platformu olarak hello X509 asimetrik güvenlik anahtarı için kullanılan sertifika anahtar uzunluğu en az 2048 olması gerekir. Bu, .NET Framework'teki System.IdentityModel.Tokens.X509AsymmetricSecurityKey hello sınıfının bir gereksinimdir. Aksi takdirde, özel durum aşağıdaki hello oluşturulur:

IDX10630: imzalama 'System.IdentityModel.Tokens.X509AsymmetricSecurityKey' hello '2048' bitten küçük olamaz.

## <a name="hello-completed-system-and-test"></a>Tamamlanan hello sistem ve test
Okuyucular temel bir hello davranış "resim" oturum açma hesabı almadan önce böylece birkaç senaryolar üzerinden tamamlandı hello uçtan uca sistemde anlatılmaktadır.

Merhaba player web uygulama ve onun oturum açma bulunabilir [burada](https://openidconnectweb.azurewebsites.net/).

Gerekenler "tümleşik olmayan" senaryo ise: video varlıklar barındırılan Azure Media Services ile hangi ya da korumasız olan veya DRM korumalı ancak (istediği bir lisans toowhoever veren) belirteci kimlik doğrulaması olmadan, bu oturum açma bilgileri olmadan (geçerek test edebilirsiniz video akışı HTTP üzerinden ise tooHTTP).

Gerekenler uçtan uca tümleşik senaryo ise: video varlıklar belirteci kimlik doğrulaması ve Azure AD tarafından oluşturulan JWT belirteci ile Azure Media Services, dinamik DRM koruma altında toologin gerekir.

### <a name="user-login"></a>Kullanıcı oturum açma
Sipariş tootest hello uçtan uca tümleşik DRM sistemde, toohave "oluşturulan veya eklenen bir hesabı" gerekir.

Hangi hesabı?

Artık Azure başlangıçta yalnızca Microsoft hesabı kullanıcıları tarafından erişime izin verse de her iki sistemle kullanıcıları tarafından erişime izin verir. Burada Azure AD hello Microsoft hesabı tüketici kimliği sistemine güvendiği bu tüm hello Azure özellikleri güven Azure AD kimlik doğrulama, kuruluş kullanıcılarının kimliğini Azure AD'ye sahip olması ve bir Federasyon ilişkisi oluşturularak yapılmadı tooauthenticate tüketici kullanıcılar. Sonuç olarak, Azure AD "yerel" Azure AD hesaplarının yanı sıra mümkün tooauthenticate "konuk" Microsoft hesapları ' dir.

Azure AD Microsoft hesabı (MSA) etki alanı güvenleri olduğundan, özel Azure AD etki alanları toohello aşağıdaki hello birinden herhangi bir hesabı Kiracı ve hello hesap toologin kullanmak ekleyebilirsiniz:

| **Etki alanı adı** | **Etki alanı** |
| --- | --- |
| **Özel Azure AD Kiracı etki alanı** |somename.onmicrosoft.com |
| **Şirket etki alanı** |Microsoft.com |
| **Microsoft hesabı (MSA) etki alanı** |Outlook.com, live.com, hotmail.com |

Merhaba yazarlar toohave oluşturulan veya sizin için eklenen bir hesap başvurabilirsiniz.

Aşağıda, farklı bir etki alanı hesapları tarafından kullanılan farklı bir oturum açma sayfalarını hello ekran görüntüleri verilmiştir.

**Özel Azure AD Kiracı etki alanı hesabı**: Bu durumda, hello özel Azure AD Kiracı etki alanının hello özelleştirilmiş oturum açma sayfasına bakın.

![Özel Azure AD Kiracı etki alanı hesabı](./media/media-services-cenc-with-multidrm-access-control/media-services-ad-tenant-domain1.png)

**Microsoft etki alanı hesabı akıllı kart ile**: Microsoft tarafından şirket özelleştirilmiş hello oturum açma sayfası bu durumda gördüğünüz iki faktörlü kimlik doğrulaması ile BT.

![Özel Azure AD Kiracı etki alanı hesabı](./media/media-services-cenc-with-multidrm-access-control/media-services-ad-tenant-domain2.png)

**Microsoft hesabı (MSA)**: Bu durumda, Tüketiciler için Microsoft Account hello oturum açma sayfasına bakın.

![Özel Azure AD Kiracı etki alanı hesabı](./media/media-services-cenc-with-multidrm-access-control/media-services-ad-tenant-domain3.png)

### <a name="using-encrypted-media-extensions-for-playready"></a>Şifrelenmiş Media uzantıları için PlayReady kullanma
Modern bir tarayıcı ile şifrelenmiş medya Uzantıları (EME) desteği, Windows 10, PlayReady IE 11 Windows 8.1 ve yukarı ve Microsoft Edge tarayıcısı gibi olacaktır PlayReady için üzerinde EME için temel alınan DRM hello.

![PlayReady için EME kullanma](./media/media-services-cenc-with-multidrm-access-control/media-services-eme-for-playready1.png)

Merhaba koyu player PlayReady koruması bir ekran yakalama korumalı videonun yapmasını engeller toohello olgu son alanıdır.

Merhaba aşağıdaki ekran hello player eklenti ve MSE/EME destek gösterir.

![PlayReady için EME kullanma](./media/media-services-cenc-with-multidrm-access-control/media-services-eme-for-playready2.png)

Microsoft Edge ve Windows 10 IE 11 EME sağlar, çağırma [PlayReady SL3000](https://www.microsoft.com/playready/features/EnhancedContentProtection.aspx/) destekleyen Windows 10 cihazlarda. PlayReady SL3000 hello akış geliştirilmiş premium içeriğinin kilidini açar (4K, HDR, vb.) ve yeni içerik teslim modellerinden (Gelişmiş içerik için erken pencere).

Odak hello Windows cihazlarda: PlayReady DRM hello HW (PlayReady SL3000) Windows cihazlarda kullanılabilir içinde yalnızca hello. Bir akış hizmeti PlayReady EME ya da bir UWP uygulamasını kullanın ve başka bir DRM daha PlayReady SL3000 kullanarak daha yüksek bir video kalitesini sunar. Genellikle 2K içerik Chrome veya Firefox aracılığıyla akar ve 4 K Microsoft Edge/IE11 veya bir UWP uygulaması içerik üzerinde (bağlı olarak hizmet ayarlarını ve uygulama) aynı aygıt hello.

#### <a name="using-eme-for-widevine"></a>Widevine için EME kullanma
Modern bir tarayıcı, Chrome 41 + Windows 10, Windows 8.1, Mac OSX Yosemite ve Chrome gibi EME/Widevine destek Android 4.4.4 ile Google Widevine DRM EME arkasında hello açıktır.

![Widevine için EME kullanma](./media/media-services-cenc-with-multidrm-access-control/media-services-eme-for-widevine1.png)

Widevine bir ekran yakalama korumalı videonun yapmasını engellemeyeceğini dikkat edin.

![Widevine için EME kullanma](./media/media-services-cenc-with-multidrm-access-control/media-services-eme-for-widevine2.png)

### <a name="not-entitled-users"></a>Değil yetkili kullanıcılar
Bir kullanıcı "Başlıklı kullanıcıları" grubunun bir üyesi değilse, hello kullanıcı yetkilendirme mümkün toopass "onay" olmayacaktır ve aşağıda gösterildiği gibi hello çoklu DRM lisans hizmeti tooissue hello istenen lisans reddeder. Merhaba ayrıntılı açıklama olan "Lisans başarısız oldu", tasarlandığı gibi olduğu.

![Beklemediğiniz yetkili kullanıcılar](./media/media-services-cenc-with-multidrm-access-control/media-services-unentitledusers.png)

### <a name="running-custom-secure-token-service"></a>Özel güvenli belirteç hizmeti çalışıyor
Merhaba senaryo özel güvenli belirteç hizmeti (STS) çalışan hello JWT belirteci simetrik ya da asimetrik anahtar kullanılarak hello özel STS tarafından verilir.

simetrik anahtar (Chrome kullanarak) kullanarak hello durum:

![Özel STS çalıştırma](./media/media-services-cenc-with-multidrm-access-control/media-services-running-sts1.png)

Merhaba bir X509 asimetrik anahtarla kullanma durumu (Microsoft modern tarayıcısı kullanılarak) sertifika.

![Özel STS çalıştırma](./media/media-services-cenc-with-multidrm-access-control/media-services-running-sts2.png)

Merhaba durumlarda yukarıda her ikisinde kullanıcı kimlik doğrulaması kalır aynı – Azure AD üzerinden hello. Merhaba tek fark, JWT belirteçleri Azure AD yerine hello özel STS tarafından verilen olmasıdır. Elbette, dinamik CENC koruma yapılandırırken, lisans teslimat hizmetinin hello kısıtlama hello JWT belirteci türünü belirtir simetrik ya da asimetrik anahtar.

## <a name="summary"></a>Özet
Bu belgede, biz CENC belirteci kimlik doğrulaması aracılığıyla çok native DRM ve erişim denetimi ile açıklanan: tasarımını ve Azure, Azure Media Services ve Azure Media Player kullanarak kendi uygulama.

* Bir başvuru tasarımı DRM/CENC alt sistemi tüm hello gerekli bileşenleri içeren sunulur;
* Bir başvuru uygulaması Azure, Azure Media Services ve Azure Media Player.
* Merhaba tasarım ve uygulama doğrudan ilgili bazı konular da ele alınmıştır.

## <a name="media-services-learning-paths"></a>Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
 
