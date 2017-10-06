---
title: "aaaHow toobuild herhangi bir Azure AD kullanıcı oturum bir uygulama | Microsoft Docs"
description: "Adım adım bir uygulama oluşturmaya yönelik yönergeler olarak da bilinen bir çok kiracılı uygulama tüm Azure Active Directory kiracısındaki bir kullanıcı olarak oturum açabilir."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 35af95cb-ced3-46ad-b01d-5d2f6fd064a3
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/26/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 123ea8125fa3c308ce0f124cc58e85ec28d476d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosign-in-any-azure-active-directory-ad-user-using-hello-multi-tenant-application-pattern"></a>Nasıl tüm Azure Active Directory (AD) kullanıcı kullanarak toosign hello çok kiracılı uygulama düzeni
Kuruluşların bir hizmet uygulaması toomany bir yazılım teklifi sunuyorsanız, uygulama tooaccept oturum açmalardan tüm Azure AD kiracısı yapılandırabilirsiniz.  Azure AD'de bu uygulama birden çok Kiracı yapmadan çağrılır.  Tüm Azure AD Kiracı kullanıcılar sonra tooyour uygulamada mümkün toosign olur, uygulamanızın hesaplarıyla toouse onaylıyorsunuz.  

Kendi hesabı sistem veya diğer oturum açma diğer bulut sağlayıcılardan türünü destekler, var olan bir uygulamanız varsa, ekleme Azure AD oturum açma dikey basit bir işlemdir. Yalnızca uygulamanızı kaydetme, oturum açma kodu OAuth2, Openıd Connect veya SAML aracılığıyla ekleyin ve "Sign In ile Microsoft" düğmesi, uygulamanızda yerleştirin. Uygulamanızı markalama hakkında daha fazla düğmesini toolearn aşağıdaki hello'ı tıklatın.

[! [Düğmesini oturum] [AAD-oturum açma]][AAD-App-Branding]

Bu makale, zaten Azure AD için tek bir kiracı uygulama oluşturmaya tanıdık varsayar.  Siz değilseniz, head toohello geri [Geliştirici Kılavuzu giriş sayfası] [ AAD-Dev-Guide] ve bizim hızlı başlangıçlar birini deneyin!

Bir Azure AD çok kiracılı uygulama uygulamanıza dört basit adımda tooconvert vardır:

1. Uygulama kayıt toobe çok Kiracı güncelleştir
2. Kod toosend istekleri toohello/Common güncelleştirme bitiş noktası 
3. Kod toohandle birden çok veren değerleri güncelleştirin
4. Kullanıcı ve yönetici onayı anlamak ve uygun kodu değişiklikleri yapın

Her adım ayrıntılı bakalım. Ayrıca düz çok atlayabilirsiniz[bu liste çok kiracılı örnekleri][AAD-Samples-MT].

## <a name="update-registration-toobe-multi-tenant"></a>Güncelleştirme kayıt toobe çok kiracılı
Varsayılan olarak, tek bir kiracı web app/API kayıtlar Azure AD'de etkilenir.  Kaydınızı hello "çok kiralanan" geçiş uygulama kaydınızı hello hello özellikleri sayfasında bularak çok kiracılı yapabileceğiniz [Azure portal] [ AZURE-portal] ve çok "Evet" ayarı.

Ayrıca unutmayın, çok kiracılı bir uygulama yapılabilmesi için önce Azure AD hello hello uygulama toobe genel benzersiz uygulama kimliği URI'sini gerektirir. Merhaba uygulama kimliği URI'si uygulama protokolü iletilerinde tanımlanan hello yollardan biridir.  Tek kiracılı uygulama için hello uygulama kimliği URI'si toobe Kiracı içinde benzersiz için yeterli olur.  Azure AD arasında tüm kiracılar Merhaba uygulaması bulabilmek için çok kiracılı uygulama için genel olarak benzersiz olmalıdır.  Genel benzersizlik hello uygulama kimliği URI'si toohave hello Azure AD kiracısı doğrulanmış bir etki alanı ile eşleşen bir ana bilgisayar adı gerektirerek zorlanır.  Örneğin, kiracınızın hello adını contoso.onmicrosoft.com sonra geçerli bir ise uygulama kimliği URI'si olması `https://contoso.onmicrosoft.com/myapp`.  Kiracı doğrulanmış bir etki alanı varsa `contoso.com`, geçerli bir uygulama kimliği URI'sini de sonra `https://contoso.com/myapp`.  Merhaba uygulama kimliği URI'si bu deseni izlemenizi değil çok kiracılı bir uygulama ayarı başarısız olur.

Yerel istemci kayıtları varsayılan olarak çok kiracılı.  Herhangi bir yerel istemci uygulaması kayıt çok kiracılı eylem toomake tootake gerek yoktur.

## <a name="update-your-code-toosend-requests-toocommon"></a>Kod toosend istekleri çok/ortak güncelleştir
Tek bir kiracı uygulamada oturum açma istekleri toohello kiracının oturum açma uç noktası gönderilir. Örneğin, contoso.onmicrosoft.com için hello uç noktası olur:

    https://login.microsoftonline.com/contoso.onmicrosoft.com

Gönderdiği istekleri tooa kiracının endpoint kullanıcılar (veya konuklar) bu Kiracı tooapplications Kiracı içinde oturum açma.  Çok kiracılı uygulama ile Merhaba uygulaması bilmiyor Önden gönderemiyor böylece, hangi Kiracı hello kullanıcının olduğu tooa kiracının endpoint ister.  Bunun yerine, tüm Azure AD kiracılar arasında multiplexes tooan endpoint gönderdiği istekleri:

    https://login.microsoftonline.com/common

Azure AD hello bir isteği ne zaman alır/ortak bir uç hello kullanıcı oturum açtığında ve bir sonuç hangi Kiracı hello kullanıcı bulur gibi arasındadır.  Merhaba/ortak uç nokta çalışır tüm Azure AD tarafından desteklenen hello kimlik doğrulama protokolleri: Openıd Connect, OAuth 2.0, SAML 2.0 ve WS-Federasyon.

Merhaba oturum açma yanıt toohello uygulama hello kullanıcıyı temsil eden bir belirteci içeriyor.  Hello veren değeriyle hello belirteci uygulamanın hangi Kiracı hello kullanıcı arasındadır söyler.  Ne zaman hello bir yanıt döndürür/ortak uç noktası, hello veren değeriyle hello belirtecindeki toohello kullanıcının Kiracı karşılık gelir.  Bu önemli toonote hello/ortak uç noktası bir kiracı değil ve bir veren değil, yalnızca çoğaltıcı olduğu.  / Common kullanırken, uygulama toovalidate belirteçleri hello mantığı güncelleştirilmiş toobe tootake bu hesaba gerekir. 

Daha önce açıklanan, çok kiracılı uygulamalar da kullanıcılar için tutarlı bir oturum açma deneyimini sağlamalıdır gibi aşağıdaki yönergeleri markalama Azure AD uygulaması hello. Uygulamanızı markalama hakkında daha fazla düğmesini toolearn aşağıdaki hello'ı tıklatın.

[! [Düğmesini oturum] [AAD-oturum açma]][AAD-App-Branding]

Merhaba/Common hello kullanımını bir göz atalım uç noktası ve kod uygulamanızda daha ayrıntılı bilgi.

## <a name="update-your-code-toohandle-multiple-issuer-values"></a>Kod toohandle birden çok veren değerleri güncelleştirin
Web uygulamaları ve web API'leri alır ve Azure AD'den belirteçleri doğrulamak.  

> [!NOTE]
> Yerel istemci uygulamaları istemek ve Azure AD'den belirteçleri almak olsa da, bunu toosend yaparlar bunları tooAPIs, bunlar burada doğrulanır.  Yerel uygulama belirteçleri doğrulamaz ve bunları donuk olarak ele almanız gerekir.
> 
> 

Bakalım Uygulama belirteçleri nasıl doğrular Azure AD'den alır.  Tek kiracılı uygulama gibi bir uç nokta değeri normal olarak gösterecektir:

    https://login.microsoftonline.com/contoso.onmicrosoft.com

ve meta veri URL'sini (Bu durumda, Openıd Connect) gibi tooconstruct kullanın:

    https://login.microsoftonline.com/contoso.onmicrosoft.com/.well-known/openid-configuration

kullanılan toovalidate belirteçler olan toodownload iki kritik bilgi parçalarını: hello Kiracı İmzalama anahtarları ve veren değeri.  Her Azure AD kiracısı hello form benzersiz veren değerine sahip:

    https://sts.windows.net/31537af4-6d77-4bb9-a681-d2394888ea26/

Burada hello GUID değeri hello yeniden adlandırma güvenli hello Kiracı kimliği hello Kiracı sürümüdür.  Meta veri bağlantısı için önceki hello tıklatırsanız `contoso.onmicrosoft.com`, bu veren değeriyle hello belgedeki görebilirsiniz.

Tek kiracılı uygulama bir belirteç doğrular hello imza hello belirtecinin hello meta veri belgesi anahtarları imzalama hello karşı denetler. Bu, toomake emin hello veren değeriyle hello meta veri belgesinde bulunan hello belirteci eşleşmeleri hello bir sağlar.

Merhaba itibaren/ortak uç nokta tooa Kiracı karşılık gelmiyor ve bir veren hello meta verilerindeki hello veren değerini inceleyin / genel, gerçek değer yerine şablonlu bir URL'ye sahip değil:

    https://sts.windows.net/{tenantid}/

Bu nedenle, çok kiracılı uygulama belirteçleri hello veren değeriyle hello meta hello ile eşleştirerek doğrulayamıyor `issuer` hello belirteç değeri.  Çok kiracılı uygulama mantığını toodecide hangi veren değerler geçerlidir ve hangi olan gereksinim duyar değil, hello Kiracı'hello veren değeriyle kimliği bölümünü tabanlı.  

Çok kiracılı uygulama yalnızca kendi hizmet için kaydolup, belirli kiracıdan oturum açma izin veriyorsa, örneğin, sonra hello veren değer veya hello kullanıma gerekir `tid` talep değeri hello belirteci toomake Kiracı kendi listesinde olduğundan emin olarak Aboneler.  Çok kiracılı uygulama yalnızca kişiler ile ilgilenir ve kiracılar dayanarak hiçbir erişim kararları değil, ardından hello veren değeriyle tamamen yok sayabilirsiniz.

Merhaba hello çok kiracılı örneklerindeki [ilgili içerik](#related-content) bu makalede, veren doğrulama hello sonunda bölümdür devre dışı tooenable tüm Azure AD Kiracı toosign.

Şimdi toomulti Kiracı uygulamalarda imzalama kullanıcıların hello kullanıcı deneyimini bakalım.

## <a name="understanding-user-and-admin-consent"></a>Anlama kullanıcı ve yönetici onayı
Azure AD'de tooan uygulamada bir kullanıcı toosign için Merhaba uygulaması hello kullanıcının Kiracı gösterilmelidir.  Bu, kendi Kiracı kullanıcılardan toohello uygulamada oturum açtığınızda benzersiz ilkeleri uygulamak gibi toodo işlemler hello kuruluşunuzun olanak sağlar.  Tek kiracılı uygulama için bu kayıt kolaydır; Bunu sahip hello hello Merhaba uygulaması kaydederken oluşan bir [Azure portal][AZURE-portal].

Çok kiracılı uygulama için hello uygulama hello ilk kaydı hello geliştirici tarafından kullanılan hello Azure AD kiracısında yaşar.  Farklı bir kiracısındaki bir kullanıcı toohello uygulamada hello için ilk kez oturum açtığında, Azure AD hello uygulama tarafından istenen tooconsent toohello izinleri ister.  Bunlar onayı sonra Merhaba uygulaması gösterimini adlı bir *hizmet sorumlusu* oluşturulan kullanıcının Kiracı hello ve oturum açma işlemi devam edebilir. Bir temsilci da hello kullanıcının onayı toohello uygulamasını kaydeder hello dizinde oluşturulur. Bkz: [uygulama ve hizmet sorumlusu nesneleri] [ AAD-App-SP-Objects] hello uygulamanın uygulama ve ServicePrincipal nesneleri ve ne tooeach diğer ilişkili oldukları hakkında ayrıntılı bilgi için.

![Onay toosingle katmanlı uygulama][Consent-Single-Tier] 

Bu onayı deneyimi hello uygulama tarafından istenen hello izinleri etkilenir.  Azure AD, yalnızca uygulama ve temsilci izinleri iki tür destekler:

* Oturum açmış olan kullanıcının hello şeyler hello kullanıcı alt kümeleri için yaptığınız gibi bir uygulama hello özelliği tooact bir temsilci izin verir.  Örneğin, kullanıcının takvimde imzalı bir uygulama hello temsilci izni tooread hello verebilirsiniz.
* Yalnızca uygulama izni doğrudan Merhaba uygulaması toohello kimliği verilir.  Örneğin, bir uygulama hello yalnızca uygulama izni tooread hello kullanıcıların listesini toohello uygulamada imzalanmış bakılmaksızın bir kiracıdaki verebilirsiniz.

Diğer bir kiracı yöneticisinin iznini gerektirirken bazı izinler razı tooby normal bir kullanıcı olabilir. 

### <a name="admin-consent"></a>Yönetici onayı
Yalnızca uygulama izinleri her zaman bir kiracı yönetici izni gerektirir.  Uygulamanızı bir yalnızca uygulama izni ister ve toosign toohello uygulamada bir kullanıcı çalışırsa, hello kullanıcı mümkün tooconsent değil bildiren bir hata iletisi görüntülenir.

Belirli izinlere temsilci, ayrıca bir kiracı yönetici izni gerektirir.  Örneğin, hello özelliği toowrite geri tooAzure AD kullanıcı imzalı hello olarak bir kiracı yönetici izni gerektirir.  Sıradan bir kullanıcı yönetici izni gerektiren bir temsilci izni isteklerini tooan uygulamada toosign çalışırsa, yalnızca uygulama izinleri gibi uygulamanızı hata iletisi alırsınız.  İzin gerektirip gerektirmediğini yönetici onayı hello kaynak yayımlanan hello geliştirici tarafından belirlenir ve hello kaynak hello belgelerinde bulunabilir.  Bağlantılar için hello Azure AD grafik API'si ve Microsoft Graph API hello hello izinleri açıklayan tootopics [ilgili içerik](#related-content) bu makalenin.

Uygulamanızı yönetici izni gerektiren izinleri kullanıyorsa, toohave düğmesini veya hello Yöneticisi hello eylem burada başlatabilirsiniz bağlantısını gibi hareket gerekir.  Uygulamanız bu eylemi normal bir OAuth2/Openıd Connect yetkilendirme isteği değildir ancak hello de içeren gönderir hello isteği `prompt=admin_consent` sorgu dizesi parametresi.  Hello Yöneticisi rıza ve hello hizmet sorumlusu hello müşterinin Kiracı içinde oluşturulan sonra sonraki oturum açma istekleri hello gerekmez `prompt=admin_consent` parametresi. Merhaba yönetici izinleri kabul edilebilir hello istenen karar vermiştir beri hello kiracısında başka hiçbir kullanıcı o noktadan izin istenir.

Merhaba `prompt=admin_consent` parametresi da yönetici onayı gerektirmeyen izinleri gerektiren uygulamalar tarafından kullanılabilir. Merhaba uygulama bir deneyim gerektirdiğinde bu burada hello Kiracı Yöneticisi "kaydolduğunda" yapılır bir saat ve başka kullanıcılara sorulur o noktadan itibaren izin üzerinde.

Bir uygulama yönetici izni gerektirir ve bir yönetici, ancak hello imzalar `prompt=admin_consent` parametresi gönderilmez, hello Yöneticisi başarıyla toohello uygulama onay **yalnızca kullanıcı hesapları için**.  Normal kullanıcılar yine de mümkün toosign ve onay toohello uygulama olmaz.  Bu, diğer kullanıcılar erişime izin vermeden önce uygulamanızın toogive hello Kiracı yönetici hello özelliği tooexplore istiyorsanız kullanışlıdır.

Kiracı Yöneticisi normal kullanıcıların tooconsent tooapplications hello özelliği devre dışı bırakabilirsiniz.  Bu özelliği devre dışıysa, yönetici onayı her zaman hello uygulama toobe hello kiracısında ayarlamak için gereklidir.  Normal kullanıcı izni uygulamanızla devre dışı tootest istiyorsanız, hello yapılandırma anahtarı hello Azure AD kiracısında hello yapılandırma bölümünde bulabilirsiniz [Azure portal][AZURE-portal].

> [!NOTE]
> Bazı uygulamalar, nerede normal kullanıcılar mümkün tooconsent başlangıçta ve sonraki Merhaba uygulaması hello yönetici ve yönetici izni gerektiren istek izinlerine içerebileceği bir deneyim istiyor.  Yoktur hiçbir şekilde toodo bu bir tek bir uygulama kaydı bugün Azure AD'de.  Merhaba yaklaşan Azure AD v2 endpoint uygulamaları toorequest izinler çalışma zamanında yerine bu senaryo etkinleştirecek kayıt aynı anda izin verir.  Daha fazla bilgi için bkz: Merhaba [Azure AD uygulama modeli v2 Geliştirici Kılavuzu][AAD-V2-Dev-Guide].
> 
> 

### <a name="consent-and-multi-tier-applications"></a>İzin ve çok katmanlı uygulamalar
Uygulamanız birden çok katman olabilir, her kendi kayıt tarafından Azure AD'de temsil.  Örneğin, bir web API çağrılarının yerel bir uygulama veya bir web uygulaması, web API çağırır.  Bu durumların her ikisinde hello istemci (yerel uygulama veya web uygulaması) izinleri toocall hello kaynak (web API) ister.  Merhaba istemci toobe başarıyla bir müşterinin Kiracı rıza için izinleri isteyen tüm kaynakları toowhich hello Müşteri'nin kiracısında önceden var olmalıdır.  Bu koşul değil, Azure AD kaynak hello hatayla ilk eklenmelidir döndürür.

**Tek bir kiracı içinde birden çok katmanları**

Mantıksal uygulamanızı iki veya daha fazla uygulama kayıtları, örneğin ayrı istemci ve kaynak oluşuyorsa bu bir sorun olabilir.  Nasıl hello kaynak hello müşteri Kiracı ilk alıyorsunuz?  Bu durumda istemci etkinleştirerek Azure AD kapsar ve tek bir adımda kaynak toobe rıza. Merhaba kullanıcı hello toplamının hello istemci ve kaynak hello onay sayfasında tarafından istenen hello izinleri görür.  tooenable Bu davranış hello istemcinin uygulama kimliği olarak hello kaynağın uygulama kaydı içermelidir bir `knownClientApplications` kendi uygulama bildiriminde.  Örneğin:

    knownClientApplications": ["94da0930-763f-45c7-8d26-04d5938baab2"]

Bu özellik aracılığıyla hello kaynağa güncelleştirilebilir [uygulama bildirimi][AAD-App-Manifest]. Bu web API'si örneğinin hello çağırma çok katmanlı bir yerel İstemcisi'nde gösterilen [ilgili içerik](#related-content) hello bu makalenin sonunda bölüm. Merhaba Aşağıdaki diyagramda izin genel bir bakış için tek bir kiracı kayıtlı çok katmanlı bir uygulama sağlar:

![Toomulti katman bilinen istemci uygulaması onayı][Consent-Multi-Tier-Known-Client] 

**Birden çok Kiracı içinde birden çok katmanları**

Bir uygulama farklı katmanlarda Hello farklı kiracılar kayıtlı benzer bir durumda olur.  Örneğin, Office 365 Exchange Online API hello çağıran bir yerel istemci uygulaması oluşturmanın hello durumu göz önünde bulundurun.  toodevelop hello yerel uygulama ve daha yeni bir müşterinin Kiracı içinde hello yerel uygulama toorun, hello Exchange Online hizmet sorumlusu mevcut olması gerekir.  Bu durumda, hello Geliştirici ve müşteri Exchange Online hello hizmet asıl toobe kiracıları içinde oluşturulan için satın almanız gerekir.  

Microsoft dışındaki bir kuruluş tarafından oluşturulan bir API Hello durumda hello geliştiricisi hello API, müşterilerin kiracılar kendi müşteriler tooconsent hello uygulamasına için tooprovide bir yol gerekir. Merhaba sağlayacak şekilde bir web istemcisi tooimplement kaydolma çalışabilir tasarım hello 3 taraf geliştirici toobuild hello için API önerilir:

1. Merhaba izleyin önceki bölümlerde tooensure hello API uygulayan hello çok kiracılı uygulama kaydı/kodu gereksinimleri
2. Buna ek olarak tooexposing hello API'nin kapsamları/rolleri, emin hello kayıt içerir hello "oturum açın ve kullanıcı profilini okuma" (varsayılan olarak sağlanır) Azure AD izni
3. Bir oturum-açma/kaydolma sayfası hello web istemcisi hello aşağıdaki uygulamak [yönetici onayı](#admin-consent) Kılavuzu daha önce ele alınan 
4. Merhaba kullanıcı toohello uygulama izin sonra hello hizmet asıl ve onay temsilci bağlantılar kendi Kiracı içinde oluşturulur ve hello yerel uygulama hello API için belirteç alabilir

Diyagram aşağıdaki hello farklı kiracılar kayıtlı çok katmanlı bir uygulama için izin genel bir bakış sağlar:

![Çok kişili toomulti katmanlı uygulama onayı][Consent-Multi-Tier-Multi-Party] 

### <a name="revoking-consent"></a>İzni iptal etme
Kullanıcıların ve yöneticilerin onayı tooyour uygulamasını dilediğiniz zaman iptal edebilirsiniz:

* Bunları kaldırarak kullanıcılar revoke erişim tooindividual uygulamaları kendi [erişim paneli uygulamaları] [ AAD-Access-Panel] listesi.
* Yöneticiler, hello Azure AD Yönetimi hello bölümünü kullanarak Azure AD'den kaldırarak erişim tooapplications iptal etme [Azure portal][AZURE-portal].

Yönetici bir kiracıdaki tüm kullanıcılar için tooan uygulama bulursa, kullanıcılar tek tek erişim iptal edilemez.  Merhaba yönetici erişimi iptal edebilirsiniz yalnızca ve yalnızca hello tüm uygulama için.

### <a name="consent-and-protocol-support"></a>İzin ve protokol desteği
Onay hello OAuth, Openıd Connect, aracılığıyla Azure AD'de desteklenir WS-Federation ve SAML protokoller.  Merhaba SAML ve WS-Federasyon protokollerini hello desteklemeyen `prompt=admin_consent` yönetici izni yalnızca OAuth ve Openıd Connect aracılığıyla mümkün olması için parametre.

## <a name="multi-tenant-applications-and-caching-access-tokens"></a>Çok Kiracılı uygulamalara ve erişim belirteçleri önbelleğe alma
Çok kiracılı uygulamalara erişim belirteçleri toocall Azure AD tarafından korunan API'lerini de alabilirsiniz.  Merhaba Active Directory Authentication Library (ADAL) çok kiracılı uygulama ile kullanırken yaygın görülen bir hata olduğundan tooinitially istek/Common kullanarak bir kullanıcı için bir belirteç, yanıt ve sonra da/Common kullanarak, aynı kullanıcı için bir sonraki belirteç isteği.  Merhaba yanıt Azure AD'den bir kiracıdan gelen değil/hello kiracısı olarak hello belirteci ortak, ADAL önbelleğe beri. Merhaba sonraki hello kullanıcı isabetsiz hello önbellek girişi ve hello kullanıcı için bir erişim belirteci yeniden istendiğinde toosign içinde olduğu çok/ortak tooget çağırın.  Merhaba önbellek eksik tooavoid, zaten oturum açmış olan kullanıcı için yapma emin sonraki çağrılar toohello kiracının endpoint yapılır.

## <a name="next-steps"></a>Sonraki adımlar
Bu makalede, nasıl öğrenilen toobuild uygulamanın tüm Azure Active Directory kiracısındaki bir kullanıcı oturum açabilirsiniz. Çoklu oturum açma uygulama ve Azure Active Directory arasında etkinleştirdikten sonra uygulama tooaccess Office 365 gibi Microsoft kaynakları tarafından sunulan API'ları da güncelleştirebilirsiniz. Bu nedenle örneğin bağlamsal bilgileri kendi profil resmi veya kendi sonraki takvim randevu gibi toohello kullanıcıları gösteren, uygulamanızda kişiselleştirilmiş bir deneyim sunabilir. API yapma hakkında daha fazla toolearn tooAzure Active Directory çağırır ve Exchange, SharePoint, OneDrive, OneNote, Planlayıcısı, Excel ve daha fazlası gibi Office 365 hizmetlerini ziyaret edin: [Microsoft Graph API][MSFT-Graph-overview].


## <a name="related-content"></a>İlgili içerik
* [Çok kiracılı uygulama örnekleri][AAD-Samples-MT]
* [Uygulamalar için markalama talimatları][AAD-App-Branding]
* [Azure AD Geliştirici Kılavuzu][AAD-Dev-Guide]
* [Uygulama nesneleri ve hizmet sorumlusu nesneleri][AAD-App-SP-Objects]
* [Uygulamaları Azure Active Directory ile tümleştirme][AAD-Integrating-Apps]
* [Merhaba onayı Framework genel bakış][AAD-Consent-Overview]
* [Microsoft Graph API'si izin kapsamları][MSFT-Graph-permision-scopes]
* [Azure AD grafik API'si izin kapsamları][AAD-Graph-Perm-Scopes]

Lütfen Açıklamalar bölümüne tooprovide geribildirim aşağıdaki hello kullanın ve daraltın ve içeriği şekil yardımcı olur.

<!--Reference style links IN USE -->
[AAD-Access-Panel]:  https://myapps.microsoft.com
[AAD-App-Branding]: ./active-directory-branding-guidelines.md
[AAD-App-Manifest]: ./active-directory-application-manifest.md
[AAD-App-SP-Objects]: ./active-directory-application-objects.md
[AAD-Auth-Scenarios]: ./active-directory-authentication-scenarios.md
[AAD-Consent-Overview]: ./active-directory-integrating-applications.md#overview-of-the-consent-framework
[AAD-Dev-Guide]: ./active-directory-developers-guide.md
[AAD-Graph-Overview]: https://azure.microsoft.com/en-us/documentation/articles/active-directory-graph-api/
[AAD-Graph-Perm-Scopes]: https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-graph-api-permission-scopes
[AAD-Integrating-Apps]: ./active-directory-integrating-applications.md
[AAD-Samples-MT]: https://azure.microsoft.com/documentation/samples/?service=active-directory&term=multitenant
[AAD-Why-To-Integrate]: ./active-directory-how-to-integrate.md
[AZURE-portal]: https://portal.azure.com
[MSFT-Graph-overview]: https://graph.microsoft.io/en-us/docs/overview/overview
[MSFT-Graph-permision-scopes]: https://graph.microsoft.io/en-us/docs/authorization/permission_scopes

<!--Image references-->
[AAD-Sign-In]: ./media/active-directory-devhowto-multi-tenant-overview/sign-in-with-microsoft-light.png
[Consent-Single-Tier]: ./media/active-directory-devhowto-multi-tenant-overview/consent-flow-single-tier.png
[Consent-Multi-Tier-Known-Client]: ./media/active-directory-devhowto-multi-tenant-overview/consent-flow-multi-tier-known-clients.png
[Consent-Multi-Tier-Multi-Party]: ./media/active-directory-devhowto-multi-tenant-overview/consent-flow-multi-tier-multi-party.png

<!--Reference style links -->
[AAD-App-Manifest]: ./active-directory-application-manifest.md
[AAD-App-SP-Objects]: ./active-directory-application-objects.md
[AAD-Auth-Scenarios]: ./active-directory-authentication-scenarios.md
[AAD-Integrating-Apps]: ./active-directory-integrating-applications.md
[AAD-Dev-Guide]: ./active-directory-developers-guide.md
[AAD-Graph-Perm-Scopes]: https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-graph-api-permission-scopes
[AAD-Graph-App-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#application-entity
[AAD-Graph-Sp-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity
[AAD-Graph-User-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#user-entity
[AAD-How-To-Integrate]: ./active-directory-how-to-integrate.md
[AAD-Security-Token-Claims]: ./active-directory-authentication-scenarios/#claims-in-azure-ad-security-tokens
[AAD-Tokens-Claims]: ./active-directory-token-and-claims.md
[AAD-V2-Dev-Guide]: ../active-directory-appmodel-v2-overview.md
[AZURE-portal]: https://portal.azure.com
[Duyshant-Role-Blog]: http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/
[JWT]: https://tools.ietf.org/html/draft-ietf-oauth-json-web-token-32
[O365-Perm-Ref]: https://msdn.microsoft.com/en-us/office/office365/howto/application-manifest
[OAuth2-Access-Token-Scopes]: https://tools.ietf.org/html/rfc6749#section-3.3
[OAuth2-AuthZ-Code-Grant-Flow]: https://msdn.microsoft.com/library/azure/dn645542.aspx
[OAuth2-AuthZ-Grant-Types]: https://tools.ietf.org/html/rfc6749#section-1.3 
[OAuth2-Client-Types]: https://tools.ietf.org/html/rfc6749#section-2.1
[OAuth2-Role-Def]: https://tools.ietf.org/html/rfc6749#page-6
[OpenIDConnect]: http://openid.net/specs/openid-connect-core-1_0.html
[OpenIDConnect-ID-Token]: http://openid.net/specs/openid-connect-core-1_0.html#IDToken














