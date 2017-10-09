---
title: "aaaAuthentication senaryoları için Azure AD | Microsoft Docs"
description: "Merhaba beş en yaygın kimlik doğrulama senaryoları için Azure Active Directory (AAD) genel bakış"
services: active-directory
documentationcenter: dev-center-name
author: skwan
manager: mbaldwin
editor: 
ms.assetid: 0c84e7d0-16aa-4897-82f2-f53c6c990fd9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: skwan
ms.custom: aaddev
ms.openlocfilehash: 5b391e3f096fcb52934c4a8aff08688352bfd3dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-scenarios-for-azure-ad"></a>Azure AD için Kimlik Doğrulama Senaryoları
Azure Active Directory (Azure AD), OAuth 2.0 ve Openıd Connect, aynı zamanda farklı platformlarda toohelp için açık kaynak kitaplıkları gibi endüstri standardı protokoller için kimlik bir hizmet olarak desteğiyle sağlayarak geliştiriciler için kimlik doğrulama basitleştirir Hızlı kod yazmaya başlayın. Bu belge yardımcı olacak anlamak çeşitli senaryolar Azure AD destekler hello ve tooget nasıl başlatılacağını gösterir. Aşağıdaki bölümlerde hello ayrılır:

* [Azure AD kimlik doğrulaması temelleri](#basics-of-authentication-in-azure-ad)
* [Azure AD güvenlik belirteçleri talepleri](#claims-in-azure-ad-security-tokens)
* [Azure AD'de uygulama kaydetme temelleri](#basics-of-registering-an-application-in-azure-ad)
* [Uygulama türleri ve senaryolar](#application-types-and-scenarios)
  
  * [Web tarayıcısı tooWeb uygulama](#web-browser-to-web-application)
  * [Tek sayfalı uygulama (SPA)](#single-page-application-spa)
  * [Yerel uygulama tooWeb API](#native-application-to-web-api)
  * [Web uygulama tooWeb API](#web-application-to-web-api)
  * [Arka plan programı veya sunucu uygulaması tooWeb API](#daemon-or-server-application-to-web-api)

## <a name="basics-of-authentication-in-azure-ad"></a>Azure AD kimlik doğrulaması temelleri
Azure AD alanında kimlik doğrulaması temel kavramları hakkında bilginiz yoksa bu bölümü okuyun. Aksi takdirde, tooskip aşağı çok isteyebilirsiniz[uygulama türleri ve senaryolar](#application-types-and-scenarios).

Şimdi kimlik olduğu gerekli hello en temel senaryo düşünün: bir kullanıcının bir web tarayıcısında tooauthenticate tooa web uygulaması gerekir. Bu senaryo, daha ayrıntılı biçimde hello açıklanan [Web tarayıcısı tooWeb uygulama](#web-browser-to-web-application) bölüm, ancak kullanıcının yararlı hello Azure AD özelliklerini ve hello senaryoda nasıl çalıştığını conceptualize noktası tooillustrate başlatılıyor. Bu senaryo için diyagram aşağıdaki hello göz önünde bulundurun:

![Oturum açma tooweb uygulama genel bakış](./media/active-directory-authentication-scenarios/basics_of_auth_in_aad.png)

Merhaba Yukarıdaki diyagramda ile unutmayın, işte gerekenler tooknow çeşitli bileşenleri hakkında:

* Azure AD hello kimlik sağlayıcısı, kullanıcılar ve kuruluşun dizininde mevcut uygulamalar, hello kimliğini doğrulamak ve sonuçta bu kullanıcıların ve uygulamaların başarılı bir kimlik doğrulaması sırasında güvenlik belirteçleri verme sorumlu'dır.
* Toooutsource kimlik doğrulaması tooAzure AD istediği bir uygulama kaydeder ve hello uygulama hello dizininde benzersiz olarak tanımlayan Azure AD'de kayıtlı olması gerekir.
* Geliştiriciler hello açık kaynaklı Azure AD kimlik doğrulama kitaplıkları toomake kimlik doğrulaması kolay hello Protokolü ayrıntıları işleyerek kullanabilirsiniz. Bkz: [Azure Active Directory kimlik doğrulama kitaplıkları](active-directory-authentication-libraries.md) daha fazla bilgi için.

• Bir kullanıcı kimliği, Merhaba uygulaması hello kullanıcının güvenlik belirteci tooensure doğrulama gerekir hello taraflara hedeflenen için kimlik doğrulamanın başarılı oldu. Geliştiriciler hiçbir belirteci kimlik doğrulama kitaplıkları toohandle doğrulaması JSON Web belirteçleri (JWT) veya SAML 2.0 dahil olmak üzere Azure AD'den sağlanan hello kullanabilir. Merhaba tooperform doğrulama el ile istiyorsanız bkz [JWT belirteci işleyicisi](https://msdn.microsoft.com/library/dn205065.aspx) belgeleri.

> [!IMPORTANT]
> Azure AD, ortak anahtar şifrelemesini toosign belirteçleri kullanır ve geçerli olduğunu doğrulayın. Bkz: [önemli bilgiler hakkında imzalama anahtarı Rollover Azure AD'de](active-directory-signing-key-rollover.md) hello gerekli mantığı hakkında daha fazla bilgi, uygulama tooensure olması gerekir, her zaman hello son anahtarlarla güncelleştirilir.
> 
> 

• hello akış isteklerin ve yanıtların hello kimlik doğrulaması için OAuth 2.0 gibi Openıd Connect, kullanılan hello kimlik doğrulama protokolü tarafından belirlenir WS-Federasyon veya SAML 2.0. Bu protokollerin hello daha ayrıntılı ele alınmıştır [Azure Active Directory kimlik doğrulama protokolleri](active-directory-authentication-protocols.md) konu ve aşağıdaki hello bölümler.

> [!NOTE]
> Azure AD hello OAuth 2.0 destekler ve kapsamlı olun Openıd Connect standartları taşıyıcı belirteçler, taşıyıcı belirteçlerini Jwt'ler temsil dahil olmak üzere kullanabilirsiniz. Bir basit güvenlik belirteci verir "bearer" erişim tooa hello korumalı kaynak bir taşıyıcı belirtecidir. Bu anlamda hello "bearer" Merhaba belirteci sunabilir herhangi bir tarafa ' dir. Merhaba adımları toosecure hello belirteçte iletim ve depolama katılmaz gerekirse bir taraf ilk Azure AD tooreceive hello taşıyıcı belirteci ile kimlik doğrulaması yapması gereken ancak ele ve istenmeyen bir şahıs tarafından kullanılır. Bazı güvenlik belirteçleri kullanarak gelen yetkisiz tarafların engellemek için yerleşik bir mekanizma olmakla birlikte, taşıyıcı belirteçlerini bu düzenek yoksa ve Aktarım Katmanı Güvenliği (HTTPS) gibi güvenli bir kanal taşınan gerekir. Bir taşıyıcı belirteci hello Temizle iletilirse, ADAM bileşenini hello Orta saldırı kötü amaçlı taraf tooacquire hello belirteci kullanılabilir ve yetkisiz erişim korumalı tooa kaynak için kullanın. Merhaba aynı güvenlik ilkelerini depolamak veya taşıyıcı belirteçlerini daha sonra kullanmak için önbelleğe alma uygulayın. Her zaman, uygulamanızın aktarır ve güvenli bir şekilde taşıyıcı belirteçleri depolar emin olun. Taşıyıcı belirteçlerini hakkında daha fazla güvenlik konuları için bkz: [RFC 6750 bölüm 5](http://tools.ietf.org/html/rfc6750).
> 
> 

Merhaba temelleri toounderstand aşağıda hello bölümleri okuyun, genel bir bakış sahip olduğunuza göre nasıl sağlama Azure AD içinde çalışır ve hello yaygın senaryolar Azure AD destekler.

## <a name="claims-in-azure-ad-security-tokens"></a>Azure AD güvenlik belirteçleri talepleri
Azure AD tarafından yayınlanan güvenlik belirteçleri talep veya onaylar doğrulandı hello konu hakkındaki bilgileri içerir. Bu talep için çeşitli görevleri hello uygulama tarafından kullanılabilir. Örneğin, bunlar kullanılan toovalidate hello belirteci, hello ilgilinin dizin Kiracı tanımlamak, kullanıcı bilgilerini görüntülemek, hello ilgilinin yetkilendirme belirlemek ve benzeri. Merhaba talep herhangi belirli güvenlik belirtecinde belirtecin hello türü, hello türüne kullanılan kimlik bilgilerini tooauthenticate hello kullanıcı hello uygulama yapılandırması ve bağlıdır. Her Azure AD tarafından gösterilen talep türünü kısa bir açıklamasını hello aşağıdaki tabloda sağlanır. Daha fazla bilgi için çok başvurun[desteklenen belirteç ve talep türleri](active-directory-token-and-claims.md).

| İste | Açıklama |
| --- | --- |
| Uygulama Kimliği |Merhaba belirteci kullanarak hello uygulamayı tanımlar. |
| Hedef kitle |Merhaba alıcı kaynağı tanımlayan hello belirteci için tasarlanmıştır. |
| Uygulama kimlik doğrulama bağlamı sınıf başvurusu |Nasıl hello istemci kimliği doğrulanmış (ortak istemci gizli istemci karşılaştırması) gösterir. |
| Anlık kimlik doğrulaması |Kayıtları tarih ve saat hello kimlik doğrulaması gerçekleştiği hello. |
| Kimlik Doğrulama Yöntemi |Merhaba konu hello belirtecinin nasıl doğrulandı gösterir (parola, sertifika, vb.). |
| Ad |Merhaba verilen adı hello kullanıcı kümesi olarak Azure AD içinde sağlar. |
| Gruplar |Merhaba kullanıcının üyesi olduğu nesne kimlikleri Azure AD grupları içerir. |
| Kimlik Sağlayıcısı |Merhaba belirtecinin hello konu kimliği doğrulanmış hello kimlik sağlayıcısı kaydeder. |
| Çıkışı |Kayıtları hello zamanı sırasında hangi hello belirteci, belirteç yenilik için sık kullanılan verilmiş. |
| Veren |Hello Azure AD kiracısı yanı sıra hello belirteci yayılan hello STS tanımlar. |
| Soyadı |Merhaba kullanıcı Hello Soyadı kümesi olarak Azure AD içinde sağlar. |
| Ad |Merhaba konu hello belirtecinin tanımlayan bir insan okunabilir değer sağlar. |
| Nesne Kimliği |Merhaba konunun değişmez, benzersiz tanıtıcısı Azure AD'de içerir. |
| Roller |Kolay adlarını içeren Azure AD uygulama rolleri hello kullanıcı verildi. |
| Kapsam |Merhaba izinleri verilen toohello istemci uygulaması gösterir. |
| Konu |Hangi hello hakkında bilgi belirteci onaylar hello asıl gösterir. |
| Kiracı kimliği |Değişmez, benzersiz bir tanımlayıcı hello belirteç hello dizin Kiracı içerir. |
| Belirteç ömrü |Bir belirtecin geçerli olduğu hello zaman aralığı tanımlar. |
| Kullanıcı asıl adı |Merhaba kullanıcı asıl adı hello konu içeriyor. |
| Sürüm |Merhaba belirteci Hello sürüm numarasını içerir. |

## <a name="basics-of-registering-an-application-in-azure-ad"></a>Azure AD'de uygulama kaydetme temelleri
AD bir dizinde kaydedilmelidir kimlik doğrulama tooAzure outsources herhangi bir uygulama. Bu adımı uygulamanız hakkında olduğu hello URL'si de dahil olmak üzere Azure AD söyleyen içerir bulunan, hello URL toosend kimlik doğrulamasından sonra hello URI tooidentify uygulamanız ve daha fazlasını yanıtlar. Bu bilgiler birkaç anahtar nedenlerle gereklidir:

* Azure AD oturum açma veya değiş tokuşu belirteçleri işlerken hello uygulamayla koordinatları toocommunicate gerekir. Bunlar hello şunları içerir:
  
  * Uygulama Kimliği URI: bir uygulama hello tanımlayıcı. Bu değer için bir belirteç hangi uygulama hello çağıran istediği kimlik doğrulama tooindicate sırasında AD tooAzure gönderilir. Ayrıca, böylece hello hedef hedeflenen edildi Merhaba uygulaması bilir bu değer hello belirteçte dahil edilir.
  * URL ve yeniden yönlendirme URI'sini Yanıtla: bir web API ya da web uygulaması hello durumda hello yanıt URL'si hello konumu toowhich Azure AD kimlik doğrulama başarılı olursa bir belirteçle birlikte hello kimlik doğrulaması yanıtını gönderecek olan. Yerel bir uygulamaya Hello durumda hello yeniden yönlendirme URI'si benzersiz tanımlayıcı toowhich Azure AD hello Kullanıcı aracısını bir OAuth 2.0 isteğindeki yönlendirir ' dir.
  * Uygulama Kimliği: Merhaba uygulaması kaydettirildiğini Azure AD tarafından oluşturulan bir uygulama için kimliği hello. Bir yetkilendirme kodu veya belirteç isterken hello uygulama kimliği ve anahtarı kimlik doğrulaması sırasında AD tooAzure gönderilir.
  * Anahtar: tooAzure AD toocall bir web API doğrulanırken bir uygulama kimliği ile birlikte gönderilen hello anahtarı.
* Azure AD gereksinimlerini tooensure hello uygulaması gerekli izinleri tooaccess dizin verileri, diğer uygulamalar, kuruluşunuzda hello vb.

Geliştirilmiş ve Azure AD ile tümleşik uygulamalar iki kategorisi vardır anladığınızda sağlama daha anlaşılır olur:

* Tek kiracılı uygulama: tek bir kiracı uygulama kullanan bir kuruluştaki yöneliktir. Bir kurumsal geliştirici tarafından yazılan genellikle satır iş kolu (LoB) uygulamaları şunlardır. Tek kiracılı uygulama, yalnızca bir dizindeki kullanıcı tarafından erişilen toobe gerekir ve bunun sonucunda, yalnızca bir dizinde sağlanan toobe gerekir. Bu uygulamalar genellikle hello kuruluşunuzdaki bir geliştirici tarafından kaydedilir.
* Çok kiracılı uygulama: çok kiracılı uygulama birçok kuruluşta kullanılmak üzere tasarlanmamıştır yalnızca bir kuruluş. Bunlar genellikle yazılım olarak-hizmet (SaaS) uygulamaları bir bağımsız yazılım satıcısı (ISV) tarafından yazılmış olan. Çok kiracılı uygulamalara gereksinim kullanıcı veya yönetici onayı tooregister gerektiren burada kullanılacakları, her dizin için sağlanan toobe bunları. Bir uygulama hello dizinde kayıtlı ve verilen erişim toohello grafik API'sini veya belki başka bir web API bu onay işlemi başlar. Bir kullanıcı veya farklı bir kuruluşta yöneticisinden toouse hello uygulamayı oluşturan oturum açtığında, bunlar hello uygulama gerektirir hello izinleri görüntüleyen bir iletişim kutusu sunulur. Merhaba kullanıcı veya yönetici veri hello uygulama erişim toohello verir onayı toohello uygulamasını belirtildiği ve son olarak, dizinlerini uygulamada yazmaçlar hello sonra'nı kullanabilirsiniz. Daha fazla bilgi için bkz: [hello onayı Framework genel bakış](active-directory-integrating-applications.md#overview-of-the-consent-framework).

Bazı hususlar, çok kiracılı uygulama yerine tek bir kiracı Uygulama geliştirirken kaynaklanır. Örneğin, birden fazla dizinde, uygulama kullanılabilir toousers yapıyorsanız, bir mekanizma toodetermine gerekir, Kiracı oldukları içinde. Çok kiracılı uygulama tooidentify belirli bir kullanıcının tüm hello dizinlerinden Azure AD'de gereken sırada tek kiracılı uygulama toolook kendi dizininde bir kullanıcı için yeterlidir. tooaccomplish bu görev Azure AD burada herhangi bir çok kiracılı uygulama yönlendirebilir oturum açma istekleri, bir kiracı özel uç noktası yerine ortak bir kimlik doğrulama uç noktası sağlar. Bir kiracı özel uç noktası https://login.microsoftonline.com/contoso.onmicrosoft.com olabilir ancak bu bitiş https://login.microsoftonline.com/common tüm dizinler için Azure AD'de noktasıdır. Merhaba ortak uç nokta özellikle önemli tooconsider hello gerekli mantığı toohandle oturum açma, oturum kapatma ve belirteç doğrulama sırasında birden çok kiracıya gerekir çünkü Uygulamanızı geliştirirken var.

Şu anda bir tek kiracılı uygulama geliştirme ancak toomake istediğiniz, kullanılabilir toomany kuruluşlar kolayca yapabilirsiniz değişiklikleri toohello uygulama ve yapılandırmasıyla Azure AD toomake, çok kiracılı özelliğine sahip. Ayrıca, Azure AD hello kullanır. aynı imzalama anahtarı tüm dizinlerde tüm belirteçleri, mı yoksa, sağlayan tek bir kiracı ya da çok kiracılı uygulama kimlik doğrulaması.

Bu belgede listelenen her bir senaryo, sağlama gereksinimleri açıklanır alt bir bölüm içerir. Azure AD'de bir uygulama sağlama hakkında daha ayrıntılı bilgi için ve hello tek ve çoklu kiracı uygulamaları arasındaki farklar, bkz: [Azure Active Directory Tümleştirme uygulamalarla](active-directory-integrating-applications.md) daha fazla bilgi için. Azure AD'de hello ortak uygulama senaryoları toounderstand okuma devam edin.

## <a name="application-types-and-scenarios"></a>Uygulama türleri ve senaryolar
Bu belgede açıklanan hello senaryoların her biri, çeşitli diller ve platformlar kullanılarak geliştirilebilir. Bunlar tüm kullanılabilir tam kod örnekleri tarafından yedeklenen bizim [kod örnekleri Kılavuzu](active-directory-code-samples.md), veya doğrudan hello karşılık gelen [GitHub örnek depoları](https://github.com/Azure-Samples?utf8=%E2%9C%93&query=active-directory). Uygulamanızı özgül ya da bir uçtan uca senaryoyu parçası gerekirse, ayrıca, çoğu durumda bu işlev bağımsız olarak eklenebilir. Örneğin, bir web API'si çağıran yerel bir uygulamanız varsa, ayrıca hello web API'si çağıran bir web uygulaması kolayca ekleyebilirsiniz. Merhaba Aşağıdaki diyagram bu senaryoları ve uygulama türleri gösterir ve farklı bileşenler eklenebilir nasıl:

![Uygulama türleri ve senaryolar](./media/active-directory-authentication-scenarios/application_types_and_scenarios.png)

Azure AD tarafından desteklenen hello beş birincil uygulama senaryoları şunlardır:

* [Web tarayıcısı tooWeb uygulama](#web-browser-to-web-application): bir kullanıcının Azure AD tarafından güvenli hale getirilen tooa web uygulamasında toosign gerekir.
* [Tek sayfa uygulama (SPA)](#single-page-application-spa): bir kullanıcının Azure AD tarafından güvenli hale getirilen tooa tek sayfa uygulamada toosign gerekir.
* [Yerel uygulama tooWeb API](#native-application-to-web-api): Azure AD tarafından güvenli hale getirilen telefon, tablet veya PC gereksinimlerini tooauthenticate kullanıcı tooget kaynakları bir web API çalışan bir yerel uygulaması.
* [Web uygulama tooWeb API](#web-application-to-web-api): tooget kaynaklardan bir web API'sini Azure AD tarafından güvenliği sağlanan bir web uygulaması gerekiyor.
* [Arka plan programı veya sunucu uygulaması tooWeb API](#daemon-or-server-application-to-web-api): arka plan programı uygulamanın veya bir sunucu uygulaması web kullanıcı arabirimi ile bir web API'sini Azure AD tarafından güvenli hale getirilmiş tooget kaynaklardan gerekiyor.

### <a name="web-browser-tooweb-application"></a>Web tarayıcısı tooWeb uygulama
Bu bölümde bir web tarayıcısı tooa web uygulamasında bir kullanıcının kimliğini doğrulayan bir uygulama açıklanmaktadır. Bu senaryoda, Merhaba web uygulaması hello kullanıcının tarayıcı toosign yönlendirir tooAzure AD bunları. Azure AD bir güvenlik belirteci hello kullanıcı hakkında talepleri içeren hello kullanıcının tarayıcısından oturum açma yanıt verir. Oturum açma bu senaryoyu destekler hello WS-Federation, SAML 2.0 ve Openıd Connect protokolleri kullanarak.

#### <a name="diagram"></a>Diyagram
![Tarayıcı tooweb uygulaması için kimlik doğrulama akışı](./media/active-directory-authentication-scenarios/web_browser_to_web_api.png)

#### <a name="description-of-protocol-flow"></a>Protokol akışı açıklaması
1. Bir kullanıcı olarak toosign hello uygulama ziyaretleri ve gerektiğinde cihazın Azure AD'de oturum açma isteği toohello kimlik doğrulama uç noktası aracılığıyla yönlendirilir.
2. Merhaba hello oturum açma sayfasında oturum açtığında.
3. Kimlik doğrulaması başarılı olursa, Azure AD kimlik doğrulama belirteci oluşturur ve hello Azure Portal yapılandırılan bir oturum açma yanıt toohello uygulamanın yanıt URL'si döndürür. Bir üretim uygulaması için HTTPS bu yanıt URL'si olmalıdır. belirteç döndürdü hello hello kullanıcı ve Azure AD hello uygulama toovalidate hello belirteci tarafından gerekli olan talepleri içerir.
4. Merhaba uygulaması, bir ortak imzalama anahtarı ve sertifikayı verenin bilgileri kullanılabilir hello Federasyon meta veri belgesi için Azure AD kullanarak hello belirteci doğrular. Merhaba uygulaması hello belirteci doğrular sonra Azure AD ile Merhaba kullanıcı yeni bir oturum başlatır. Bu oturumda, sona erene kadar hello kullanıcı tooaccess Merhaba uygulaması sağlar.

#### <a name="code-samples"></a>Kod Örnekleri
Merhaba kod örnekleri Web tarayıcısı tooWeb uygulama senaryoları için bkz. Ve daha sonra yeniden sık--hello zaman yeni örnekler eklediğimiz denetleyin. [Web tarayıcısı tooWeb uygulama](active-directory-code-samples.md#web-browser-to-web-application).

#### <a name="registering"></a>Kaydetme
* Tek bir kiracı: yalnızca kuruluşunuz için bir uygulama geliştiriyorsanız, şirketinizin dizininde hello Azure Portal kullanarak kayıtlı olması gerekir.
* Çok Kiracılı: kuruluşunuzun dışındaki kullanıcılar tarafından kullanılan bir uygulama geliştiriyorsanız, şirketinizin dizinde kayıtlı olması gerekir, ancak aynı zamanda Merhaba uygulaması kullanarak her kuruluşun dizinde kayıtlı olması gerekir. toomake uygulamanız kendi dizininde bulunan, tooconsent tooyour uygulama sağlar, müşterileriniz için kaydolma işlemine dahil edebilirsiniz. Bunlar, uygulamanız için kaydolduğunuzda, hello izinleri Merhaba uygulaması gerektirir ve seçeneği tooconsent hello gösteren bir iletişim kutusu sunulur. Merhaba gerekli izinler, yönetici hello olarak bağlı olarak diğer kuruluşun olabilir toogive izni gereklidir. Merhaba kullanıcı veya yönetici izin, Merhaba uygulaması kendi Directory'ye kaydedilir. Daha fazla bilgi için bkz: [Azure Active Directory Tümleştirme uygulamalarla](active-directory-integrating-applications.md).

#### <a name="token-expiration"></a>Belirteç süre sonu
Azure AD tarafından hello belirteç Hello süresi dolduğunda hello kullanıcının oturum sona erer. Uygulamanızı bir süre işlem yapılmadığında üzerinde temel alarak kullanıcılara imzalama gibi isterseniz, bu süre içinde kısaltabilir. Merhaba oturumu sona erdiğinde hello kullanıcı, istendiğinde toosign yeniden olur.

### <a name="single-page-application-spa"></a>Tek sayfalı uygulama (SPA)
Uygulaması için kimlik doğrulaması bir tek sayfa, Azure AD kullanır, bu bölümde açıklanmıştır ve hello OAuth 2.0 örtük yetki web API'si geri sona toosecure. Tek sayfalık uygulamalar genellikle hello tarayıcı ve sunucu üzerinde çalışan bir Web API arka uç çalıştıran bir JavaScript sunu katmanı (ön uç) olarak yapılandırılmıştır ve uygulamanın iş mantığını uygular hello. Merhaba örtük yetkilendirme verme ve karar Uygulama senaryonuz için uygun olup olmadığını Yardım hakkında daha fazla toolearn bkz [anlama hello OAuth2 örtük izin akışı Azure Active Directory'de](active-directory-dev-understanding-oauth2-implicit-grant.md).

Merhaba kullanıcı oturum açtığında bu senaryoda, JavaScript ön uç kullanır hello [Active Directory Authentication Library (ADAL JavaScript için. JS)](https://github.com/AzureAD/azure-activedirectory-library-for-js/tree/dev) ve hello örtük yetkilendirme kimliği belirteci (id_token) tooobtain Azure AD verin. Merhaba belirteç önbelleğe alınır ve hello istemci bunu toohello isteği hello taşıyıcı belirteci olarak tooits Web API güvenliğinin hello OWIN ara yazılımı ile son geri çağrıları yapılırken ekler. 

#### <a name="diagram"></a>Diyagram
![Tek sayfa uygulama diyagramı](./media/active-directory-authentication-scenarios/single_page_app.png)

#### <a name="description-of-protocol-flow"></a>Protokol akışı açıklaması
1. Merhaba kullanıcıyı toohello web uygulaması götürür.
2. Merhaba uygulaması hello JavaScript ön uç (sunu katmanı) toohello tarayıcı döndürür.
3. Merhaba kullanıcı oturum açma bağlantısına tıklayarak oturum açma, örneğin başlatır. Merhaba tarayıcı bir GET toohello Azure AD yetkilendirme uç noktası toorequest kimliği belirteci gönderir. Bu istek hello uygulama kimliği ve yanıt URL'si hello sorgu parametrelerini içerir.
4. Azure AD hello karşı yanıt URL'si hello Azure Portal yapılandırılan yanıt URL'si kayıtlı hello doğrular.
5. Merhaba hello oturum açma sayfasında oturum açtığında.
6. Kimlik doğrulaması başarılı olursa, Azure AD kimliği belirteci oluşturur ve bir URL parçası (#) toohello uygulamanın yanıt URL'si olarak döndürür. Bir üretim uygulaması için HTTPS bu yanıt URL'si olmalıdır. belirteç döndürdü hello hello kullanıcı ve Azure AD hello uygulama toovalidate hello belirteci tarafından gerekli olan talepleri içerir.
7. Merhaba tarayıcıda çalışan hello JavaScript istemci kodu hello belirteci geri toohello uygulamanın web API son çağrıları korumak hello yanıt toouse gelen ayıklar.
8. Tarayıcı çağrıları hello uygulamanın web API geri bitiş hello erişim belirteciyle hello yetkilendirme üstbilgisinde hello.

#### <a name="code-samples"></a>Kod Örnekleri
Merhaba kod örnekleri tek sayfa uygulama (SPA) senaryoları için bkz. Sık--olarak emin toocheck dönecek yeni örnekler hello zaman ekleriz. [Tek sayfa uygulama (SPA)](active-directory-code-samples.md#single-page-application-spa).

#### <a name="registering"></a>Kaydetme
* Tek bir kiracı: yalnızca kuruluşunuz için bir uygulama geliştiriyorsanız, şirketinizin dizininde hello Azure Portal kullanarak kayıtlı olması gerekir.
* Çok Kiracılı: kuruluşunuzun dışındaki kullanıcılar tarafından kullanılan bir uygulama geliştiriyorsanız, şirketinizin dizinde kayıtlı olması gerekir, ancak aynı zamanda Merhaba uygulaması kullanarak her kuruluşun dizinde kayıtlı olması gerekir. toomake uygulamanız kendi dizininde bulunan, tooconsent tooyour uygulama sağlar, müşterileriniz için kaydolma işlemine dahil edebilirsiniz. Bunlar, uygulamanız için kaydolduğunuzda, hello izinleri Merhaba uygulaması gerektirir ve seçeneği tooconsent hello gösteren bir iletişim kutusu sunulur. Merhaba gerekli izinler, yönetici hello olarak bağlı olarak diğer kuruluşun olabilir toogive izni gereklidir. Merhaba kullanıcı veya yönetici izin, Merhaba uygulaması kendi Directory'ye kaydedilir. Daha fazla bilgi için bkz: [Azure Active Directory Tümleştirme uygulamalarla](active-directory-integrating-applications.md).

Merhaba uygulaması kaydolduktan sonra yapılandırılmış toouse OAuth 2.0 örtük verme Protokolü olması gerekir. Varsayılan olarak, bu protokolü uygulamalar için devre dışıdır. tooenable hello OAuth2 örtük Grant protokolü, uygulamanız için kendi uygulama hello Azure Portal bildiriminden düzenleyin ve hello "oauth2AllowImplicitFlow" değeri tootrue ayarlayın. Ayrıntılı yönergeler için bkz: [etkinleştirme OAuth 2.0 örtük verme tek sayfa uygulamaları için](active-directory-integrating-applications.md).

#### <a name="token-expiration"></a>Belirteç süre sonu
Azure AD ile ADAL.js toomanage kimlik doğrulaması kullandığınızda, süresi dolmuş bir belirtecini yenilemeyi yanı sıra hello uygulama tarafından çağrılabilir ek web API kaynaklar için belirteçleri alma kolaylaştıran birkaç özelliklerinden yararlanır. Merhaba kullanıcı Azure AD ile başarıyla doğruladığında bir tanımlama bilgisi tarafından güvenli bir oturum hello tarayıcı ve Azure AD arasındaki hello kullanıcı için oluşturulur. Merhaba oturum hello kullanıcı ve Azure AD arasında ve hello kullanıcı ve hello sunucu üzerinde çalışan Merhaba web uygulaması arasında değil mevcut önemli toonote olur. Bir belirteç süresi dolduğunda ADAL.js toosilently başka bir belirteç elde bu oturumu kullanır. Bu gizli IFRAME toosend kullanarak yapar ve hello OAuth örtük verme protokolü kullanarak hello isteği alır. ADAL.js aynı düzenek de kullanabilir toosilently destek çıkış noktaları arası kaynak paylaşımı (CORS), bu kaynakları sürece hello uygulama çağrıları hello kullanıcının dizinde kayıtlı API kaynakları erişim belirteçleri Azure AD'den diğer web için edinmek ve gerekli tüm izin hello kullanıcı tarafından oturum açma sırasında verildi.

### <a name="native-application-tooweb-api"></a>Yerel uygulama tooWeb API
Bu bölümde, bir kullanıcı adına bir web API'si çağıran bir yerel uygulamayı açıklanmaktadır. Bu senaryo hello OAuth 2.0 yetkilendirme kodu verme ortak istemci türüyle hello 4.1 bölümünde açıklandığı gibi üzerine inşa edilmiştir [OAuth 2.0 belirtimi](http://tools.ietf.org/html/rfc6749). Merhaba yerel uygulaması hello OAuth 2.0 protokolünü kullanarak hello kullanıcı için bir erişim belirteci alır. Bu erişim belirteci hello kullanıcı yetkisi verir ve istenen hello kaynak döndüren hello isteği toohello web API'de, daha sonra gönderilir.

#### <a name="diagram"></a>Diyagram
![Yerel uygulama tooWeb API diyagramı](./media/active-directory-authentication-scenarios/native_app_to_web_api.png)

#### <a name="authentication-flow-for-native-application-tooapi"></a>Yerel uygulama tooAPI için kimlik doğrulama akışı
#### <a name="description-of-protocol-flow"></a>Protokol akışı açıklaması
Merhaba AD kimlik doğrulama kitaplıkları kullanıyorsanız, aşağıda açıklanan hello protokol ayrıntılarını çoğunu sizin için hello tarayıcı açılır pencere, belirteç önbelleğe alma ve yenileme belirteçleri işlenmesi gibi işlenir.

1. Açılan bir tarayıcı kullanarak, Merhaba yerel uygulaması Azure AD'de bir istek toohello yetkilendirme uç noktası sağlar. Bu istek hello Azure Portal ve hello uygulama kimliği URI'si hello web API'si için gösterildiği gibi hello uygulama kimliği ve hello yeniden yönlendirme URI'si hello yerel uygulamasının içerir. Merhaba kullanıcı zaten oturum taşınmadığından, istendiğinde toosign içinde yeniden oldukları
2. Azure AD hello kullanıcının kimliğini doğrular. Bunlar zaten yapmadıysanız, çok kiracılı bir uygulamadır ve onayı gerekli toouse hello uygulama ise, hello kullanıcı gerekli tooconsent olacaktır. Azure AD, izin verme sonra ve temel kimlik doğrulaması başarılı bir yetkilendirme kodu yanıtı geri toohello istemci uygulamanın yeniden yönlendirme URI'si verir.
3. Azure AD bir kimlik doğrulama kodu yanıtı verdiğinde toohello yeniden yönlendirme URI'si, istemci uygulaması durdurur tarayıcı etkileşimi ve ayıklar hello yetkilendirme kodundan hello yanıt hello. Bu yetkilendirme kodu kullanarak, hello yetkilendirme kodu içeren bir istek tooAzure Reklamın belirteç uç noktası Merhaba istemci uygulaması gönderir, ayrıntılar hakkında istemci uygulaması (uygulama kimliği ve yeniden yönlendirme URI'si) hello ve istenen kaynak (uygulama kimliği hello URI hello web API için).
4. Merhaba yetkilendirme kodu ve Merhaba istemci uygulaması ve web API hakkındaki bilgileri Azure AD tarafından doğrulanır. Başarılı bir doğrulama sırasında Azure AD iki belirteci döndürür: JWT erişim belirteci ve bir JWT yenileme belirteci. Ayrıca, Azure AD görünen adı ve Kiracı kimliklerine gibi hello kullanıcı hakkındaki temel bilgileri döndürür
5. HTTPS üzerinden Merhaba istemci uygulaması JWT erişim belirteci tooadd hello "Bearer" tayin JWT dizesiyle hello yetkilendirme üstbilgisinde hello isteği toohello Web API döndürülen hello kullanır. Merhaba web API sonra hello JWT belirteci doğrular ve doğrulama başarılı olursa, kaynak döndürür hello istenen.
6. Merhaba erişim belirtecinin süresi dolduğunda, Merhaba istemci uygulaması hello kullanıcının tooauthenticate yeniden gereken belirten bir hata alırsınız. Merhaba uygulaması geçerli yenileme belirteci varsa, kullanılan tooacquire sormadan yeni bir erişim belirteci hello kullanıcı toosign yeniden olabilir. Merhaba yenileme belirtecinin süresi dolarsa Merhaba uygulaması gerekir toointeractively hello kullanıcı yeniden kimlik doğrulaması.

> [!NOTE]
> Merhaba yenileme belirteci Azure AD tarafından verilen kullanılan tooaccess birden fazla kaynak olabilir. Örneğin, izin toocall iki web API'leri sahip bir istemci uygulaması varsa, hello yenileme belirteci kullanılan tooget bir erişim belirteci toohello diğer web API de olabilir.
> 
> 

#### <a name="code-samples"></a>Kod Örnekleri
Merhaba kod örnekleri yerel uygulama tooWeb API senaryoları için bkz. Ve daha sonra yeniden sık--hello zaman yeni örnekler eklediğimiz denetleyin. [Yerel uygulama tooWeb API](active-directory-code-samples.md#native-application-to-web-api).

#### <a name="registering"></a>Kaydetme
* Tek bir kiracı: Hem de yerel uygulama hello ve hello hello web API kayıtlı aynı Azure AD dizininde. Merhaba web API yapılandırılmış tooexpose kullanılan toolimit hello yerel uygulamanın erişim tooits kaynakları izinleri olabilir. ardından Merhaba istemci uygulaması istenen hello izinleri hello Azure Portal hello "İzinleri tooOther uygulamaları" açılan menüsünden seçer.
* Çok Kiracılı: İlk olarak, hello yerel uygulama her zaman sadece hello geliştirici veya publisher'ın dizinde kayıtlı. İkinci olarak, hello yerel toobe işlevsel gerektirir yapılandırılmış tooindicate hello izinleri uygulamasıdır. Bir kullanıcının veya yöneticinin hello hedef dizinde kullanılabilir tootheir kuruluşun yaptığı onayı toohello uygulamasını verdiğinde bu gerekli izinlerin listesi iletişim kutusunda gösterilir. Bazı uygulamalar hello kuruluştaki herhangi bir kullanıcı onayı yalnızca kullanıcı düzeyinde izinler gerektirir. Diğer uygulamalar hello kuruluşunuzdaki bir kullanıcının onay veremez yönetici düzeyi izinler gerektirir. Yalnızca bir dizin Yöneticisi bu izin düzeyi, gerekli izni tooapplications verebilirsiniz. Merhaba kullanıcı veya yönetici izin, yalnızca hello web API kendi Directory'ye kaydedilir. Daha fazla bilgi için bkz: [Azure Active Directory Tümleştirme uygulamalarla](active-directory-integrating-applications.md).

#### <a name="token-expiration"></a>Belirteç süre sonu
Merhaba yerel uygulama, yetkilendirme kodu tooget JWT erişim belirteci kullandığında, ayrıca, bir JWT yenileme belirteci alır. Merhaba erişim belirtecinin süresi dolduğunda, hello yenileme belirteci kullanılan toore olabilir-toosign içinde yeniden gerektirmeden için bunları hello kullanıcı kimlik doğrulaması. Bu yenileme belirteci kullanılan tooauthenticate hello sonra kullanıcı, hangi sonuçları yeni bir erişim belirteci ve yenileme belirteci.

### <a name="web-application-tooweb-api"></a>Web uygulama tooWeb API
Bu bölümde bir web API tooget kaynaklardan gerektiren bir web uygulaması açıklanmaktadır. Bu senaryoda, vardır web uygulaması hello iki kimlik türlerinin tooauthenticate kullanın ve hello web API çağrısı: uygulama kimliği ya da temsilci atanan kullanıcı kimliği.

*Uygulama Kimliği:* web API OAuth 2.0 istemci kimlik bilgileri verin tooauthenticate hello uygulama ve erişim hello Bu senaryoda kullanır. Uygulama kimliği, hello web API, yalnızca Merhaba web uygulaması, aradığı algılayabilir kullanırken hello hello kullanıcı hakkında hiçbir bilgi web API almaz. Merhaba uygulaması hello kullanıcı hakkındaki bilgileri alırsa, hello uygulama protokolü aracılığıyla gönderilir ve Azure AD tarafından imzalanmamış. Merhaba web API Merhaba web uygulaması hello kullanıcı kimlik doğrulaması güvenir. Bu nedenle, bu deseni güvenilir alt sistem adı verilir.

*Kullanıcı kimliği için temsilci:* bu senaryo iki yolla gerçekleştirilebilir: Openıd Connect ve OAuth 2.0 yetkilendirme kodu verme gizli istemcisi ile. Merhaba web uygulaması, toohello web API, hello başarılı bir şekilde kimliği doğrulanmış bir kullanıcı toohello web uygulaması kanıtlar ve mümkün tooobtain temsilci atanan kullanıcı kimliğini toocall hello web API'si Merhaba web uygulaması olan hello kullanıcı için bir erişim belirteci alır. Bu erişim belirteci hello kullanıcı yetkisi verir ve istenen hello kaynak döndüren hello isteği toohello web API'de, gönderilir.

#### <a name="diagram"></a>Diyagram
![Web uygulama tooWeb API diyagramı](./media/active-directory-authentication-scenarios/web_app_to_web_api.png)

#### <a name="description-of-protocol-flow"></a>Protokol akışı açıklaması
Hem uygulama kimliği hello ve temsilci olarak atanan kullanıcı kimliğini türleri akışı hello aşağıda ele alınmıştır. Merhaba anahtar aralarında hello kullanıcı oturum açma ve erişim toohello web API elde önce temsilci hello kullanıcı kimliğini ilk bir yetkilendirme kodu almalıdır farktır.

##### <a name="application-identity-with-oauth-20-client-credentials-grant"></a>Uygulama Kimliği OAuth 2.0 istemci ile kimlik bilgileri verin
1. TooAzure AD hello web uygulamasında kullanıcı oturumu açık (Merhaba bkz [Web tarayıcısı tooWeb uygulama](#web-browser-to-web-application) yukarıda).
2. Böylece toohello web API kimlik doğrulaması ve istenen hello kaynak almak hello web uygulamasının tooacquire bir erişim belirteci gerekiyor. Merhaba kimlik bilgisi, uygulama kimliği ve web API uygulama kimliği URI'si sağlama isteği tooAzure Reklamın belirteç uç noktası kolaylaştırır.
3. Azure AD hello uygulama kimliğini doğrular ve kullanılan toocall hello web API'sini bir JWT erişim belirtecini döndürür.
4. HTTPS üzerinden hello web uygulaması JWT erişim belirteci tooadd hello "Bearer" tayin JWT dizesiyle hello yetkilendirme üstbilgisinde hello isteği toohello Web API döndürülen hello kullanır. Merhaba web API sonra hello JWT belirteci doğrular ve doğrulama başarılı olursa, kaynak döndürür hello istenen.

##### <a name="delegated-user-identity-with-openid-connect"></a>Openıd temsilci atanan kullanıcı kimliğiyle Bağlan
1. Bir kullanıcı Azure AD kullanarak tooa web uygulamasında oturum (Merhaba bkz [Web tarayıcısı tooWeb uygulama](#web-browser-to-web-application) yukarıdaki bölümde). Merhaba web uygulamasının Hello kullanıcı henüz tooallowing hello web uygulama toocall hello web API kendi adına seçtiği değil, hello kullanıcı tooconsent gerekir. Merhaba uygulaması gerektiriyorsa hello izinleri görüntüler ve bunları herhangi biri yönetici düzeyi izinler varsa, hello dizininde normal bir kullanıcı mümkün tooconsent olmaz. Merhaba uygulaması zaten hello gerekli izinlere sahip şekilde bu onay işlemi yalnızca toomulti Kiracı uygulamalar, değil tek bir kiracı uygulamaları geçerlidir. Merhaba kullanıcının oturum açtığı zaman Merhaba web uygulaması hello kullanıcı gibi bir kimlik doğrulama kodu hakkında bilgi içeren bir kimliği belirteci aldı.
2. Azure AD tarafından verilen hello yetkilendirme kodu kullanarak, Merhaba web uygulaması hello yetkilendirme kodu içeren bir istek tooAzure Reklamın belirteç uç noktası gönderir, istenen kaynak (Merhaba istemci uygulaması (uygulama kimliği ve yeniden yönlendirme URI'si) ve hello hakkında ayrıntılar Uygulama Kimliği URI'si hello web API).
3. Merhaba yetkilendirme kodu ve Merhaba web uygulaması ve web API hakkındaki bilgileri Azure AD tarafından doğrulanır. Başarılı bir doğrulama sırasında Azure AD iki belirteci döndürür: JWT erişim belirteci ve bir JWT yenileme belirteci.
4. HTTPS üzerinden hello web uygulaması JWT erişim belirteci tooadd hello "Bearer" tayin JWT dizesiyle hello yetkilendirme üstbilgisinde hello isteği toohello Web API döndürülen hello kullanır. Merhaba web API sonra hello JWT belirteci doğrular ve doğrulama başarılı olursa, kaynak döndürür hello istenen.

##### <a name="delegated-user-identity-with-oauth-20-authorization-code-grant"></a>Temsilci atanan kullanıcı kimliği ile OAuth 2.0 yetkilendirme kodu verme
1. Bir kullanıcı zaten tooa web uygulaması Azure AD, kimlik doğrulama mekanizması bağımsızdır imzalanır.
2. Merhaba web uygulaması bir yetkilendirme isteği hello uygulama kimliği sağlama hello tarayıcı tooAzure Reklamın yetkilendirme uç noktası aracılığıyla sorunları için bir erişim belirteci tooacquire kod ve sonra Başlangıç web uygulaması için yeniden yönlendirme URI'si gerektirir başarılı kimlik doğrulaması. Merhaba kullanıcı tooAzure AD açar.
3. Merhaba web uygulamasının Hello kullanıcı henüz tooallowing hello web uygulama toocall hello web API kendi adına seçtiği değil, hello kullanıcı tooconsent gerekir. Merhaba uygulaması gerektiriyorsa hello izinleri görüntüler ve bunları herhangi biri yönetici düzeyi izinler varsa, hello dizininde normal bir kullanıcı mümkün tooconsent olmaz. Bu onay tooboth tek ve çok kiracılı uygulama geçerlidir.  Merhaba tek bir kiracı durumda da, bir yönetici, kullanıcılar adına yönetici onayı tooconsent gerçekleştirebilirsiniz.  Bu yapılabilir hello kullanarak `Grant Permissions` hello düğmesini [Azure Portal](https://portal.azure.com). 
4. Merhaba kullanıcı seçtiği sonra Merhaba web uygulaması tooacquire bir erişim belirteci ihtiyaç duyduğu hello yetkilendirme kodu alır.
5. Azure AD tarafından verilen hello yetkilendirme kodu kullanarak, Merhaba web uygulaması hello yetkilendirme kodu içeren bir istek tooAzure Reklamın belirteç uç noktası gönderir, istenen kaynak (Merhaba istemci uygulaması (uygulama kimliği ve yeniden yönlendirme URI'si) ve hello hakkında ayrıntılar Uygulama Kimliği URI'si hello web API).
6. Merhaba yetkilendirme kodu ve Merhaba web uygulaması ve web API hakkındaki bilgileri Azure AD tarafından doğrulanır. Başarılı bir doğrulama sırasında Azure AD iki belirteci döndürür: JWT erişim belirteci ve bir JWT yenileme belirteci.
7. HTTPS üzerinden hello web uygulaması JWT erişim belirteci tooadd hello "Bearer" tayin JWT dizesiyle hello yetkilendirme üstbilgisinde hello isteği toohello Web API döndürülen hello kullanır. Merhaba web API sonra hello JWT belirteci doğrular ve doğrulama başarılı olursa, kaynak döndürür hello istenen.

#### <a name="code-samples"></a>Kod Örnekleri
Merhaba kod örnekleri Web uygulaması tooWeb API senaryoları için bkz. Ve daha sonra yeniden sık--hello zaman yeni örnekler eklediğimiz denetleyin. Web [uygulama tooWeb API](active-directory-code-samples.md#web-application-to-web-api).

#### <a name="registering"></a>Kaydetme
* Web uygulaması hello uygulama kimliği ve temsilci atanan kullanıcı kimliğini çalışmaları için tek bir kiracı: Merhaba ve hello hello web API kayıtlı aynı Azure AD dizininde. Merhaba web API yapılandırılmış tooexpose kullanılan toolimit hello web uygulamasının erişim tooits kaynakları izinleri olabilir. Temsilci atanan kullanıcı kimlik türü kullanılıyorsa, Merhaba web uygulaması hello Azure Portal hello "İzinleri tooOther uygulamaları" açılan menüsünden tooselect istenen hello izinleri olması gerekir. Merhaba uygulama kimlik türü kullanılıyorsa bu adım gerekli değildir.
* Çok Kiracılı: İlk olarak, Merhaba web uygulaması toobe işlevsel gerektirir yapılandırılmış tooindicate hello izinleridir. Bir kullanıcının veya yöneticinin hello hedef dizinde kullanılabilir tootheir kuruluşun yaptığı onayı toohello uygulamasını verdiğinde bu gerekli izinlerin listesi iletişim kutusunda gösterilir. Bazı uygulamalar hello kuruluştaki herhangi bir kullanıcı onayı yalnızca kullanıcı düzeyinde izinler gerektirir. Diğer uygulamalar hello kuruluşunuzdaki bir kullanıcının onay veremez yönetici düzeyi izinler gerektirir. Yalnızca bir dizin Yöneticisi bu izin düzeyi, gerekli izni tooapplications verebilirsiniz. Merhaba kullanıcı veya yönetici onayları Merhaba, web uygulaması ve hello web API hem de bunların dizinde kaydedilir.

#### <a name="token-expiration"></a>Belirteç süre sonu
Merhaba web uygulaması, yetkilendirme kodu tooget JWT erişim belirteci kullandığında, ayrıca, bir JWT yenileme belirteci alır. Merhaba erişim belirtecinin süresi dolduğunda, hello yenileme belirteci kullanılan toore olabilir-toosign içinde yeniden gerektirmeden için bunları hello kullanıcı kimlik doğrulaması. Bu yenileme belirteci kullanılan tooauthenticate hello sonra kullanıcı, hangi sonuçları yeni bir erişim belirteci ve yenileme belirteci.

### <a name="daemon-or-server-application-tooweb-api"></a>Arka plan programı veya sunucu uygulaması tooWeb API
Bu bölümde bir web API tooget kaynaklardan gereken bir arka plan programı veya sunucu uygulaması açıklanmaktadır. Toothis bölüm geçerli iki alt senaryo vardır: toocall OAuth 2.0 istemci kimlik bilgileri verme türünü; yerleşik bir web API gereken bir arka plan programı ve toocall gerektiren bir sunucu uygulaması (örneğin, bir web API) web API'si, yerleşik OAuth 2.0 On-Behalf-Of taslak belirtimi.

Arka plan programı uygulama toocall bir web API gerektiğinde Merhaba senaryo için önemli toounderstand olmasından birkaç. İlk olarak, kullanıcı etkileşimi hello uygulama toohave kendi kimliğini gerektirir ve arka plan programı uygulama ile mümkün değildir. Arka plan programı uygulama toplu iş veya hello arka planda çalışan bir işletim sistemi hizmet örneğidir. Bu tür bir uygulama, kendi uygulama kimliğini kullanır ve uygulama kimliği, kimlik bilgisi (parola veya sertifika) ve uygulama kimliği URI'si tooAzure AD sunan bir erişim belirteci ister. Başarılı kimlik doğrulamasından sonra hello arka plan programı kullanılan toocall hello sonra web API olan Azure AD'den bir erişim belirteci alır.

Bir sunucu uygulaması toocall web API'si, gerektiğinde hello için bu yararlı toouse örnek bir senaryodur. Bir kullanıcı kimlik doğrulaması yerel bir uygulamaya ve bu yerel uygulama toocall bir web API gerekiyor düşünün. Azure AD JWT erişim belirteci toocall hello web API'si verir. Merhaba web API başka bir aşağı akış web API'si toocall gerekiyorsa, bu hello üzerinde-temsili akış toodelegate hello kullanıcının kimliğini kullanın ve toohello ikinci katmanlı web API kimlik doğrulaması.

#### <a name="diagram"></a>Diyagram
![Arka plan programı veya sunucu uygulaması tooWeb API diyagramı](./media/active-directory-authentication-scenarios/daemon_server_app_to_web_api.png)

#### <a name="description-of-protocol-flow"></a>Protokol akışı açıklaması
##### <a name="application-identity-with-oauth-20-client-credentials-grant"></a>Uygulama Kimliği OAuth 2.0 istemci ile kimlik bilgileri verin
1. İlk olarak, bir etkileşimli oturum açma iletişim kutusu gibi herhangi bir insan etkileşimi olmadan kendisini olarak Azure AD ile tooauthenticate hello sunucu uygulaması gerekir. Merhaba kimlik bilgisi, uygulama kimliği ve uygulama kimliği URI'si sağlama isteği tooAzure Reklamın belirteç uç noktası kolaylaştırır.
2. Azure AD hello uygulama kimliğini doğrular ve kullanılan toocall hello web API'sini bir JWT erişim belirtecini döndürür.
3. HTTPS üzerinden hello web uygulaması JWT erişim belirteci tooadd hello "Bearer" tayin JWT dizesiyle hello yetkilendirme üstbilgisinde hello isteği toohello Web API döndürülen hello kullanır. Merhaba web API sonra hello JWT belirteci doğrular ve doğrulama başarılı olursa, kaynak döndürür hello istenen.

##### <a name="delegated-user-identity-with-oauth-20-on-behalf-of-draft-specification"></a>OAuth 2.0 üzerinde-adına-Of taslak belirtimiyle temsilci olarak atanan kullanıcı kimliği
aşağıda açıklanan hello akış (örneğin, bir yerel uygulamayı) başka bir uygulama üzerinde bir kullanıcı kimliği ve kullanıcı kimliklerini kullanılan tooacquire bir erişim belirteci toohello ilk katmanlı web API bırakıldı varsayar.

1. Merhaba yerel uygulaması hello erişim belirteci toohello ilk katmanlı web API gönderir.
2. Merhaba ilk katmanlı web API hello kullanıcının erişim belirtecini yanı sıra uygulama Kimliğini ve kimlik bilgilerini sağlama isteği tooAzure Reklamın belirteç uç noktası gönderir. Ek olarak, hello isteği ile gönderilen bir hello gösteren parametresi on_behalf_of hello özgün kullanıcı adına bir aşağı akış web API'si toocall API yeni isteyen web belirteçleri.
3. Azure AD, bir JWT erişim belirteci ve bir JWT belirteci toohello ilk katmanlı web API yenileme döndürme bu hello ilk katmanlı web API izinleri tooaccess hello ikinci katmanlı web API sahiptir ve hello isteği doğrular doğrular.
4. HTTPS üzerinden ardından API çağrılarının hello ilk katmanlı web hello ikinci katmanlı web API hello belirteç dizesini hello yetkilendirme hello istek üstbilgisinde ekleyerek. Merhaba erişim belirteci ve yenileme belirteçleri geçerli olduğu sürece hello ilk katmanlı web API toocall hello ikinci katmanlı web API devam edebilirsiniz.

#### <a name="code-samples"></a>Kod Örnekleri
Merhaba kod örnekleri arka plan programı veya sunucu uygulaması tooWeb API senaryoları için bkz. Ve daha sonra yeniden sık--hello zaman yeni örnekler eklediğimiz denetleyin. [Sunucu veya arka plan programı uygulama tooWeb API](active-directory-code-samples.md#server-or-daemon-application-to-web-api)

#### <a name="registering"></a>Kaydetme
* Tek bir kiracı: hello uygulama kimliği ve temsilci atanan kullanıcı kimliğini çalışmaları için hello arka plan programı veya sunucu uygulaması hello kaydedilmelidir aynı Azure AD dizininde. Merhaba web API yapılandırılmış tooexpose kullanılan toolimit hello arka plan programı veya sunucunun tooits erişimine izin kümesi olabilir. Temsilci atanan kullanıcı kimlik türü kullanılıyorsa, hello sunucu uygulaması hello Azure Portal hello "İzinleri tooOther uygulamaları" açılan menüsünden tooselect istenen hello izinleri olması gerekir. Merhaba uygulama kimlik türü kullanılıyorsa bu adım gerekli değildir.
* Çok Kiracılı: İlk olarak, hello arka plan programı veya sunucu uygulaması toobe işlevsel gerektirir yapılandırılmış tooindicate hello izinleridir. Bir kullanıcının veya yöneticinin hello hedef dizinde kullanılabilir tootheir kuruluşun yaptığı onayı toohello uygulamasını verdiğinde bu gerekli izinlerin listesi iletişim kutusunda gösterilir. Bazı uygulamalar hello kuruluştaki herhangi bir kullanıcı onayı yalnızca kullanıcı düzeyinde izinler gerektirir. Diğer uygulamalar hello kuruluşunuzdaki bir kullanıcının onay veremez yönetici düzeyi izinler gerektirir. Yalnızca bir dizin Yöneticisi bu izin düzeyi, gerekli izni tooapplications verebilirsiniz. Merhaba kullanıcı veya yönetici izin, hello web API'leri her ikisi de kendi dizininde kaydedilir.

#### <a name="token-expiration"></a>Belirteç süre sonu
Merhaba ilk uygulama, yetkilendirme kodu tooget JWT erişim belirteci kullandığında, ayrıca, bir JWT yenileme belirteci alır. Merhaba erişim belirtecinin süresi dolduğunda, hello yenileme belirteci kullanılan toore olabilir-hello kullanıcı kimlik bilgileri olmadan kimlik doğrulaması. Bu yenileme belirteci kullanılan tooauthenticate hello sonra kullanıcı, hangi sonuçları yeni bir erişim belirteci ve yenileme belirteci.

## <a name="see-also"></a>Ayrıca Bkz.
[Azure Active Directory Geliştirici Kılavuzu](active-directory-developers-guide.md)

[Azure Active Directory kod örnekleri](active-directory-code-samples.md)

[Azure AD'de anahtar geçişi imzalama hakkında önemli bilgiler](active-directory-signing-key-rollover.md)

[Azure AD'de OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx)

