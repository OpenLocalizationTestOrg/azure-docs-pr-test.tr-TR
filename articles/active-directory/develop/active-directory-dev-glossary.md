---
title: "Active Directory Geliştirici sözlüğü aaaAzure | Microsoft Docs"
description: "Yaygın olarak kullanılan Azure Active Directory Geliştirici kavramları ve Özellikler koşulları listesi."
services: active-directory
documentationcenter: 
author: bryanla
manager: mbaldwin
editor: 
ms.assetid: 551512df-46fb-4219-a14b-9c9fc23998ba
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: bryanla
ms.custom: aaddev
ms.openlocfilehash: 32a6a6194b8d01409159a2b60263bb66a87a843c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-developer-glossary"></a>Azure Active Directory Geliştirici sözlüğü
Bu makalede, Azure AD için uygulama geliştirme öğrenmeye olduğunda faydalıdır hello Azure Active Directory (AD) Geliştirici kavramları, bazıları için tanımları içerir.

## <a name="access-token"></a>erişim belirteci
Bir tür [güvenlik belirteci](#security-token) tarafından verilen bir [yetkilendirme sunucusu](#authorization-server)ve tarafından kullanılan bir [istemci uygulaması](#client-application) sipariş tooaccess içinde bir [korumalı kaynak sunucusu ](#resource-server). Genellikle biçiminde hello bir [JSON Web Token (JWT)][JWT], hello belirteci içerir toohello istemci hello tarafından verilen hello yetkilendirme [kaynak sahibi](#resource-owner), istenen düzeyi için erişimi. Merhaba belirteç uygulanabilir tüm içerir [talep](#claim) hello istemci uygulaması toouse etkinleştirme hakkında hello konu belirli bir kaynağa erişirken kimlik bilgisinin bir form olarak. Bu ayrıca hello kaynak sahibi tooexpose kimlik bilgileri toohello istemci hello gereksinimini ortadan kaldırır.

Erişim belirteçleri bazen başvurulan tooas "Kullanıcı + uygulama" ya da "Uygulama yalnızca" Merhaba bağlı olarak temsil ettiği kimlik bilgileri. Örneğin, bir istemci uygulaması kullandığında:

* ["Yetkilendirme kodu" yetkilendirme verme](#authorization-grant)hello son kullanıcı hello kaynak sahibi olarak ilk kimlik doğrulaması, yetkilendirme toohello temsilci istemci tooaccess kaynak hello. Merhaba istemci daha sonra hello erişim belirteci alma kimliğini doğrular. Merhaba istemci uygulaması ve Merhaba uygulaması yetkili hem hello kullanıcı gösteren hello belirteci bazen özellikle bir "Kullanıcı + uygulama" belirteci olarak başvurulan toomore olabilir.
* ["İstemci kimlik bilgileri" yetkilendirme verme](#authorization-grant)hello istemci hello tek kimlik doğrulama sağlar, başvurulan tooas bir "Yalnızca uygulama" belirteci hello belirteci bazen şekilde hello kaynak-sahibinin kimlik doğrulama/yetkilendirme çalışmıyor olabilir.

Bkz: [Azure AD belirteç başvurusu] [ AAD-Tokens-Claims] daha fazla ayrıntı için.

## <a name="application-manifest"></a>Uygulama bildirimi
Merhaba tarafından sağlanan bir özellik [Azure portal][AZURE-portal], ilişkili güncelleştirme mekanizması olarak kullanılan hello uygulama kimliği yapılandırmasına göre bir JSON temsili üretir [ Uygulama] [ AAD-Graph-App-Entity] ve [ServicePrincipal] [ AAD-Graph-Sp-Entity] varlıklar. Bkz: [anlama hello Azure Active Directory Uygulama bildirimini] [ AAD-App-Manifest] daha fazla ayrıntı için.

## <a name="application-object"></a>Uygulama nesnesi
Ne zaman, kaydetme/güncelleştirme hello uygulamada [Azure portal][AZURE-portal], hello portal/güncelleştirme uygulama nesnesi ve karşılık gelen [hizmet sorumlusu nesnesi](#service-principal-object)Kiracı için. Merhaba uygulama nesnesi *tanımlar* uygulamanın kimlik yapılandırması (sahip olduğu erişim genel olarak tüm kiracılar arasında) Merhaba, kendi karşılık gelen hizmet asıl nesneleri olan bir şablonu sağlama  *türetilmiş* yerel olarak çalışma zamanında (içinde belirli bir kiracı) kullanmak için.

Bkz: [uygulama ve hizmet sorumlusu nesneleri] [ AAD-App-SP-Objects] daha fazla bilgi için.

## <a name="application-registration"></a>Uygulama kaydı
İçinde tooallow ile uygulama toointegrate ve temsilci kimlik ve erişim yönetimi işlevleri tooAzure AD sipariş, Azure AD ile kaydedilmelidir [Kiracı](#tenant). Azure AD ile uygulamanızı kaydederken, Azure AD ile toointegrate izin vererek, uygulamanız için sağlayan bir kimlik yapılandırması ve özellikleri gibi kullanın:

* Güçlü bir yönetim, çoklu oturum açma Azure AD Kimlik Yönetimi'ni kullanarak özelliğini ve [Openıd Connect] [ OpenIDConnect] protokol uygulanması
* Erişim çok aracılı[korunan kaynakları](#resource-server) tarafından [istemci uygulamaları](#client-application), Azure AD OAuth 2.0 aracılığıyla [yetkilendirme sunucusu](#authorization-server) uygulama
* [Onay framework](#consent) kaynak sahibi kimlik tabanlı, istemci erişim tooprotected kaynakları yönetmek için.

Bkz: [uygulamaları Azure Active Directory ile tümleştirme] [ AAD-Integrating-Apps] daha fazla ayrıntı için.

## <a name="authentication"></a>Kimlik doğrulaması
kimlik ve erişim denetimi için kullanılan bir güvenlik sorumlusu toobe oluşturulması için hello temel sağlayan bir taraf yasal kimlik bilgileri, zor hello eylemi. Sırasında bir [OAuth2 yetkilendirme verme](#authorization-grant) hello taraf kimlik doğrulaması hello rolü ya da örneğin, doldurma [kaynak sahibi](#resource-owner) veya [istemci uygulaması](#client-application)bağlı olarak kullanılan hello verin.

## <a name="authorization"></a>Yetkilendirme
Kimliği doğrulanmış güvenlik sorumlusu izni toodo bir şey verme hello eylemi. Hello Azure AD programlama modelinde iki birincil kullanım örnekleri şunlardır:

* Sırasında bir [OAuth2 yetkilendirme verme](#authorization-grant) akış: ne zaman hello [kaynak sahibi](#resource-owner) yetkilendirme toohello verir [istemci uygulaması](#client-application), hello istemci tooaccess hello izin verme Kaynak sahibinin kaynaklar.
* Kaynak erişim hello istemci tarafından sırasında: hello tarafından uygulandığı gibi [kaynak sunucusu](#resource-server), hello kullanarak [talep](#claim) değerleri sunmak hello [erişim belirteci](#access-token) toomake erişim denetimi Bunlar üzerine dayalı olarak karar.

## <a name="authorization-code"></a>Yetkilendirme kodu
Tooa sağlanan kısa ömürlü "token" [istemci uygulaması](#client-application) hello tarafından [yetkilendirme uç noktası](#authorization-endpoint), hello "yetkilendirme kodu" akışının bir parçası, aşağıdakilerden birini hello dört OAuth2 [yetkilendirme verir ](#authorization-grant). Merhaba kod toohello istemci uygulaması içinde yanıt tooauthentication döndürülen bir [kaynak sahibi](#resource-owner), hello kaynak sahibi yetkilendirme tooaccess hello temsilci belirten istenen kaynakları. Merhaba akışının bir parçası hello kodu daha sonra için kullanılan bir [erişim belirteci](#access-token).

## <a name="authorization-endpoint"></a>Yetkilendirme uç noktası
Merhaba tarafından uygulanan hello uç noktaları birini [yetkilendirme sunucusu](#authorization-server), toointeract hello ile kullanılan [kaynak sahibi](#resource-owner) sipariş tooprovide içinde bir [yetkilendirme verme](#authorization-grant) sırasında bir OAuth2 yetkilendirme akışı verin. Merhaba bağlı olarak kullanıldığında, akış hello gerçek sağlanan grant gösterebilir, dahil olmak üzere yetki bir [yetkilendirme kodu](#authorization-code) veya [güvenlik belirteci](#security-token).

Merhaba OAuth2 belirtimi'nın bkz [yetki türleri] [ OAuth2-AuthZ-Grant-Types] ve [yetkilendirme uç noktası] [ OAuth2-AuthZ-Endpoint] bölümler ve hello [Openıdconnect belirtimi] [ OpenIDConnect-AuthZ-Endpoint] daha fazla ayrıntı için.

## <a name="authorization-grant"></a>Yetkilendirme verme
Merhaba temsil eden bir kimlik bilgisi [kaynak sahibinin](#resource-owner) [yetkilendirme](#authorization) tooaccess tooa verilen kaynaklarını korumalı [istemci uygulaması](#client-application). Bir istemci uygulaması hello birini kullanabilirsiniz [dört verme hello OAuth2 yetkilendirme Framework tarafından tanımlanan türlerini] [ OAuth2-AuthZ-Grant-Types] tooobtain istemci türü/gereksinimlerine bağlı olarak bir verin: "yetkilendirme kodu verme", " istemci kimlik bilgileri vermenizi","örtük grant"ve"kaynak sahibi parolası kimlik bilgileri verin". Merhaba kimlik bilgisi döndürülen toohello istemci ya da bir [erişim belirteci](#access-token), veya bir [yetkilendirme kodu](#authorization-code) (daha sonra bir erişim belirteci için değiştirilen), yetkilendirme verme kullanılan hello türüne bağlı olarak.

## <a name="authorization-server"></a>Yetkilendirme sunucusu
Merhaba tarafından tanımlandığı şekilde [OAuth2 yetkilendirme Framework][OAuth2-Role-Def], hello sunucu erişimi vermekten sorumlu belirteçler toohello [istemci](#client-application) başarıyla kimlik doğrulandıktan sonra Merhaba [kaynak sahibi](#resource-owner) ve kendi yetkilendirme alma. A [istemci uygulaması](#client-application) hello yetkilendirme sunucusu çalışma zamanında etkileşimde kendi [yetkilendirme](#authorization-endpoint) ve [belirteci](#token-endpoint) hello tanımlanan OAuth2 uygun olarak uç noktaları [yetkilendirme verir](#authorization-grant).

Azure AD uygulama tümleştirmesi Hello durumda Azure AD uygulayan hello yetkilendirme sunucusu rolü için Azure AD uygulamaları ve Microsoft hizmet API'leri, örneğin [Microsoft Graph API][Microsoft-Graph].

## <a name="claim"></a>Talep
A [güvenlik belirteci](#security-token) bir varlık onaylar sağlayan talepleri içerir (gibi bir [istemci uygulaması](#client-application) veya [kaynak sahibi](#resource-owner)) (örneğin, hello tooanother varlık [kaynak sunucusu](#resource-server)). Taleplerdir hello belirteci konu hakkında bilgiler geçiş ad/değer çiftleri (örneğin, hello tarafından doğrulandı hello güvenlik sorumlusu [yetkilendirme sunucusu](#authorization-server)). Merhaba talep verilen belirteçte belirtecin hello türü, hello türünü kullanılan kimlik bilgilerini tooauthenticate hello konu, hello uygulama yapılandırması, vb. dahil olmak üzere çeşitli değişkenler bağlıdır.

Bkz: [Azure AD belirteç başvurusu] [ AAD-Tokens-Claims] daha fazla ayrıntı için.

## <a name="client-application"></a>istemci uygulaması
Merhaba tarafından tanımlandığı şekilde [OAuth2 yetkilendirme Framework][OAuth2-Role-Def], hello adına kaynak istekleri yapan bir uygulamada korunan [kaynak sahibi](#resource-owner). (örneğin, Merhaba uygulaması bir sunucu, bir masaüstü veya diğer cihazları yürütür olup olmadığını) "istemci" Merhaba terim herhangi belirli donanım uygulama özelliklerine göstermez.  

Bir istemci uygulaması ister [yetkilendirme](#authorization) kaynak sahibi tooparticipate gelen bir [OAuth2 yetkilendirme verme](#authorization-grant) akış ve API/data hello kaynak sahibinin adınıza erişebilir. Merhaba OAuth2 yetkilendirme Framework [iki istemci türlerini tanımlayan][OAuth2-Client-Types], "gizli" ve "Genel", hello istemcinin özelliği toomaintain hello kendi kimlik gizliliğini göre. Uygulamaları uygulayabilirsiniz bir [web istemcisi (gizli)](#web-client) bir web sunucusunda çalışan bir [yerel istemci (Genel)](#native-client) bir aygıtta yüklü veya [kullanıcı aracısı-tabanlı istemci (Genel)](#user-agent-based-client)bir cihazın tarayıcısında çalıştırır.

## <a name="consent"></a>Onay
Merhaba sürecinin bir [kaynak sahibi](#resource-owner) yetkilendirme tooa verme [istemci uygulaması](#client-application), tooaccess korumalı özel kaynaklarınıza [izinleri](#permissions), hello adına Kaynak sahibi. Merhaba istemci tarafından istenilen hello izinlerine bağlı olarak onay tooallow tootheir kuruluşun/tek verilere erişmek için sırasıyla bir yönetici veya kullanıcı istenir. Unutmayın, içinde bir [çok kiracılı](#multi-tenant-application) senaryosu, hello uygulamanın [hizmet sorumlusu](#service-principal-object) hello onaylıyorsunuz kullanıcı hello Kiracı da kaydedilir.

## <a name="id-token"></a>ID simgesi
Bir [Openıd Connect] [ OpenIDConnect-ID-Token] [güvenlik belirteci](#security-token) tarafından sağlanan bir [yetkilendirme sunucunun](#authorization-server) [yetkilendirme uç noktası](#authorization-endpoint), içeren [talep](#claim) toohello kimliğini ilgili bir son kullanıcı [kaynak sahibi](#resource-owner). Gibi bir erişim belirteci, ayrıca kimlik belirteçlerini temsil dijital olarak imzalanmış olarak [JSON Web Token (JWT)][JWT]. Bir erişim belirteci yine de bir kimliği belirtecin talep amacıyla ilgili tooresource erişim ve özellikle erişim denetimi için kullanılmaz.

Bkz: [Azure AD belirteç başvurusu] [ AAD-Tokens-Claims] daha fazla ayrıntı için.

## <a name="multi-tenant-application"></a>çok kiracılı uygulama
Oturum açma sağlayan uygulama sınıfının ve [onayı](#consent) tüm Azure AD içinde sağlanan kullanıcılar tarafından [Kiracı](#tenant), kiracılar hello biri, hello istemci kayıtlı dışında dahil olmak üzere. [Yerel istemci](#native-client) uygulamalar varsayılan olarak, çok kiracılı ancak [web istemcisi](#web-client) ve [web kaynak/API](#resource-server) uygulamanız hello özelliği tooselect tek veya birden çok Kiracı arasında. Bunun aksine, bir web uygulaması tek-Kiracı olarak kayıtlı, oturum açma işlemleri aynı hello bir kiracı hello sağlanan kullanıcı hesaplarından Merhaba uygulaması, kayıtlı yalnızca olanak tanır.

Bkz: [nasıl tüm Azure AD kullanıcı kullanarak toosign hello çok kiracılı uygulama düzeni] [ AAD-Multi-Tenant-Overview] daha fazla ayrıntı için.

## <a name="native-client"></a>yerel istemci
Bir tür [istemci uygulaması](#client-application) yüklü olan yerel bir aygıtta. Tüm kod, bir cihazda yürütülür olduğundan, son tooits bağlanamama toostore kimlik bilgileri özel olarak/ilkemiz "Genel" bir istemci olarak kabul edilir. Bkz: [OAuth2 istemci türleri ve profiller] [ OAuth2-Client-Types] daha fazla ayrıntı için.

## <a name="permissions"></a>İzinleri
A [istemci uygulaması](#client-application) kazancı erişim tooa [kaynak sunucusu](#resource-server) izin istekleri bildirme tarafından. İki tür mevcuttur:

* "Belirtin izinleri atanmış" [kapsam tabanlı](#scopes) temsilci oturum açmış hello gelen yetkilendirme access kullanarak [kaynak sahibi](#resource-owner), toohello kaynak çalışma zamanında sunulan ["scp "talep](#claim) hello istemcinin içinde [erişim belirteci](#access-token).
* Belirtin "Uygulama" izinleri [rol tabanlı](#roles) erişim hello istemci uygulamanın kimlik bilgileri/kimliğini kullanarak, çalışma zamanında sunulan toohello kaynak ["rol" talep](#claim) hello içinde istemcinin erişim belirteci.

Bunlar ayrıca sırasında hello yüzey [onayı](#consent) hello Yöneticisi veya kaynak sahibi hello fırsat toogrant/reddetme hello istemci erişim tooresources kendi Kiracı vermiş işlemi.

İzin istekleri "Uygulamaları" Merhaba üzerinde yapılandırılmış olan / "Ayarlar" sekmesini hello [Azure portal][AZURE-portal], altında "Gerekli izinleri", "İzinlere temsilci" Merhaba seçerek istenen ve " Uygulama izinleri"(Merhaba ikinci hello genel yönetici rolü üyeliği gerektirir). Çünkü bir [ortak istemci](#client-application) kimlik bilgileri, güvenli bir şekilde korunamaz izinlere temsilci, yalnızca isteyebilir sırada bir [gizli istemci](#client-application) hello özelliği toorequest yetkilendirilen ve uygulama vardır izinler. Merhaba istemcinin [uygulama nesnesi](#application-object) izinleri bildirilen depoları hello kendi [requiredResourceAccess özelliği][AAD-Graph-App-Entity].

## <a name="resource-owner"></a>Kaynak sahibi
Merhaba tarafından tanımlandığı şekilde [OAuth2 yetkilendirme Framework][OAuth2-Role-Def], erişim tooa verme yeteneğine sahip bir varlık korumalı kaynak. Merhaba kaynak sahibine bir kişi olduğunda, başvurulan tooas bir son kullanıcı olur. Örneğin, bir [istemci uygulaması](#client-application) tooaccess hello aracılığıyla bir kullanıcının posta istediği [Microsoft Graph API][Microsoft-Graph], hello kaynak sahibinin izni gerektirir Merhaba posta kutusu.

## <a name="resource-server"></a>Kaynak sunucusu
Merhaba tarafından tanımlandığı şekilde [OAuth2 yetkilendirme Framework][OAuth2-Role-Def], ana bilgisayar kaynakları, kabul etme ve tooprotected kaynak yanıt korunan bir sunucu istekleri tarafından [istemci uygulamaları](#client-application) , mevcut bir [erişim belirteci](#access-token). Olarak da bilinen bir korumalı kaynak sunucuda veya kaynak uygulama.

Kaynak sunucuda API'lerini gösterir ve üzerinden tooits korumalı kaynaklara erişmelerine zorlar [kapsamları](#scopes) ve [rolleri](#roles), OAuth 2.0 yetkilendirme Framework hello kullanarak. Örnek tooAzure AD Kiracı verilere erişmek ve hello posta ve takvim gibi erişim toodata sağlayan bir Office 365 API'leri sağlayan hello Azure AD Graph API verilebilir. Bunların her ikisi de aynı zamanda hello erişilebilir [Microsoft Graph API][Microsoft-Graph].  

Yalnızca bir istemci uygulaması gibi kaynak uygulamanın kimlik yapılandırması üzerinden kurulur [kayıt](#application-registration) hello uygulama ve hizmet sorumlusu nesnesi bir Azure AD kiracısında sağlama. Hello Azure AD grafik API'si gibi bazı Microsoft tarafından sağlanan API'leri sağlama işlemi sırasında tüm kiracılar kullanılabilir hale hizmet asıl adı önceden kaydettiniz.

## <a name="roles"></a>roles
Gibi [kapsamları](#scopes), rollerini sağlamak için bir yol bir [kaynak sunucusu](#resource-server) toogovern erişim tooits korumalı kaynaklar. İki tür vardır: bir "uygulama" rolü uygulayan sırada erişim toohello kaynak gerektiren kullanıcıları/grupları için aynı hello için rol tabanlı erişim denetimi "kullanıcı" rolü uygulayan [istemci uygulamaları](#client-application) erişimi gerektirir.

Rolleri, kaynak tanımlı dizeleri (örneğin "gider onaylayıcı", "Salt okunur", "Directory.ReadWrite.All"), hello yönetilen [Azure portal] [ AZURE-portal] hello kaynağın aracılığıyla [uygulama bildirim](#application-manifest)ve hello kaynağın depolanan [appRoles özelliği][AAD-Graph-Sp-Entity]. Hello Azure portal ayrıca kullanılan tooassign kullanıcılar çok olan "kullanıcı" rolleri ve istemci yapılandırma [uygulama izinleri](#permissions) tooaccess "uygulama" rolü.

Azure AD grafik API'si tarafından kullanıma sunulan hello uygulama rolleri hakkında ayrıntılı bilgi için bkz: [grafik API'si izin kapsamları][AAD-Graph-Perm-Scopes]. Adım adım uygulama örnek için bkz: [rol tabanlı erişim denetimi kullanarak Azure AD bulut uygulamalarında][Duyshant-Role-Blog].

## <a name="scopes"></a>Kapsamları
Gibi [rolleri](#roles), kapsamları sağlamak için bir yol bir [kaynak sunucusu](#resource-server) toogovern erişim tooits korumalı kaynaklar. Kapsamlardır kullanılan tooimplement [kapsam tabanlı] [ OAuth2-Access-Token-Scopes] için erişim denetimi, bir [istemci uygulaması](#client-application) , verildiği atanmış erişim toohello kaynak sahibi tarafından.

Kapsamları dizelerdir hello yönetilen kaynak tanımlı (örneğin "Mail.Read", "Directory.ReadWrite.All"), [Azure portal] [ AZURE-portal] hello kaynağın aracılığıyla [uygulama bildirimi](#application-manifest)ve hello kaynağın depolanan [oauth2Permissions özelliği][AAD-Graph-Sp-Entity]. Hello Azure portal ayrıca kullanılan tooconfigure istemci uygulamasıdır [izinleri atanmış](#permissions) tooaccess bir kapsam.

En iyi yöntem adlandırma kuralı, toouse "resource.operation.constraint" biçiminde olur. Azure AD grafik API'si tarafından kullanıma sunulan hello kapsamları hakkında ayrıntılı bilgi için bkz: [grafik API'si izin kapsamları][AAD-Graph-Perm-Scopes]. Office 365 Hizmetleri tarafından sunulan kapsamlar için bkz: [Office 365 API izinleri başvurusu][O365-Perm-Ref].

## <a name="security-token"></a>Güvenlik belirteci
OAuth2 belirteci veya SAML 2.0 onaylama gibi talepleri içeren imzalı bir belge. Bir OAuth2 için [yetkilendirme verme](#authorization-grant), bir [erişim belirteci](#access-token) (OAuth2) ve bir [kimliği belirteci](http://openid.net/specs/openid-connect-core-1_0.html#IDToken) güvenlik belirteçleri, her ikisi de olarak uygulanır türleridir bir [JSON Web Token (JWT)][JWT].

## <a name="service-principal-object"></a>Hizmet sorumlusu nesnesi
Ne zaman, kaydetme/güncelleştirme hello uygulamada [Azure portal][AZURE-portal], hello portal/güncelleştirme hem de bir [uygulama nesnesi](#application-object) ve karşılık gelen hizmet sorumlusu Kiracı nesnesi. Merhaba uygulama nesnesi *tanımlar* (burada ilişkili Merhaba uygulaması verildiğini erişim genel olarak tüm kiracılar arasında), uygulamanın kimlik yapılandırması hello ve hangi hello şablondan karşılık gelen hizmet Asıl nesneleri olan *türetilmiş* yerel olarak çalışma zamanında (içinde belirli bir kiracı) kullanmak için.

Bkz: [uygulama ve hizmet sorumlusu nesneleri] [ AAD-App-SP-Objects] daha fazla bilgi için.

## <a name="sign-in"></a>oturum açma
Merhaba sürecinin bir [istemci uygulaması](#client-application) son kullanıcı kimlik doğrulamayı başlatan ve yakalama ilgili durumu alınırken hello amacı için bir [güvenlik belirteci](#security-token) ve hello uygulama oturumu toothat kapsamı durumu. Kullanıcı profili bilgileri gibi yapılarını içerebilir ve bu bilgileri belirteci talepleri türetilmiş durumu.

bir uygulama oturum açma Hello işlevi genellikle kullanılan tooimplement çoklu oturum açma (SSO) olduğu. Bu aynı zamanda "kaydolma" bir işlev tarafından bir son kullanıcı toogain erişim tooan uygulamasına (ilk oturum açma) için hello giriş noktası olarak öncesinde. Merhaba kaydolma işlevi kullanılan toogather olduğunu ve ek durumu belirli toohello kullanıcı kalıcı hale getirmek ve gerektirebilir [kullanıcı izni](#consent).

## <a name="sign-out"></a>oturum kapatma
Merhaba ile ilişkili hello kullanıcı durumunu ayırma bir son kullanıcı beklemediğiniz kimlik doğrulama işlemi hello [istemci uygulaması](#client-application) oturumu sırasında [oturum açma](#sign-in)

## <a name="tenant"></a>Kiracı
Başvurulan tooas Azure AD kiracısı Azure AD dizini örneğidir. Özellikler de dahil olmak üzere, çeşitli sağlar:

* Tümleşik uygulamalar için bir kayıt defteri hizmeti
* kimlik doğrulama kullanıcı hesapları ve kayıtlı uygulamalar
* REST uç noktalarını toosupport OAuth2 ve hello dahil olmak üzere SAML dahil çeşitli protokoller gerekli [yetkilendirme uç noktası](#authorization-endpoint), [belirteç uç noktası](#token-endpoint) ve "Genel" uç nokta tarafından kullanılan hello [ çok kiracılı uygulamalara](#multi-tenant-application).

Bir kiracı, bir Azure AD ile de ilişkilidir veya hello abonelik için kimlik ve erişim yönetimi özellikleri sağlayarak hello aboneliğin sağlama sırasında Office 365 aboneliği. Bkz: [nasıl tooget bir Azure Active Directory Kiracı] [ AAD-How-To-Tenant] hello hakkında ayrıntılı bilgi için erişim tooa alabilirsiniz çeşitli şekillerde Kiracı. Bkz: [Azure aboneliklerinin Azure Active Directory ile ilişkili] [ AAD-How-Subscriptions-Assoc] abonelikleri ve Azure AD kiracısı arasında hello ilişki hakkında ayrıntılı bilgi için.

## <a name="token-endpoint"></a>belirteç uç noktası
Merhaba tarafından uygulanan hello uç noktaları birini [yetkilendirme sunucusu](#authorization-server) toosupport OAuth2 [yetkilendirme verir](#authorization-grant). Merhaba grant bağlı olarak, kullanılan tooacquire olabilir bir [erişim belirteci](#access-token) (ve ilgili "Yenile" belirteç) tooa [istemci](#client-application), veya [kimliği belirteci](#ID-token) hello ile kullanıldığında [ Openıd Connect] [ OpenIDConnect] protokolü.

## <a name="user-agent-based-client"></a>İstemci kullanıcı aracısı tabanlı
Bir tür [istemci uygulaması](#client-application) , kodu bir web sunucusundan indirir ve bir kullanıcı aracısı içinde (örneğin, bir web tarayıcısı), bir tek sayfa uygulama (SPA) gibi yürütür. Tüm kod, bir cihazda yürütülür olduğundan, son tooits bağlanamama toostore kimlik bilgileri özel olarak/ilkemiz "Genel" bir istemci olarak kabul edilir. Bkz: [OAuth2 istemci türleri ve profiller] [ OAuth2-Client-Types] daha fazla ayrıntı için.

## <a name="user-principal"></a>Kullanıcı asıl adı
Bir hizmet asıl kullanılan toorepresent uygulama örneğini nesnesidir benzer toohello şekilde kullanıcı asıl nesne başka bir kullanıcı temsil eden güvenlik sorumlusu türüdür. Hello Azure AD grafik [kullanıcı varlığı] [ AAD-Graph-User-Entity] hello şema adı ve Soyadı, kullanıcı asıl adı, dizin rol üyeliğini vb. gibi kullanıcı ile ilgili özellikler de dahil olmak üzere bir kullanıcı nesnesi için tanımlar. Bu, Azure AD tooestablish çalışma zamanında asıl kullanıcı için hello kullanıcı kimliği yapılandırması sağlar. Merhaba kullanıcı asıl olduğu kullanılan toorepresent için çoklu oturum açma, kimliği doğrulanmış bir kullanıcı kaydı [onayı](#consent) temsilci, erişim denetimi kararlarını, vb. yapma.

## <a name="web-client"></a>Web istemcisi
Bir tür [istemci uygulaması](#client-application) yürütmelerinin tüm kodu bir web sunucusu ve mümkün toofunction "gizli" istemci olarak, kimlik bilgileri güvenli bir şekilde hello sunucuda depolayarak. Bkz: [OAuth2 istemci türleri ve profiller] [ OAuth2-Client-Types] daha fazla ayrıntı için.

## <a name="next-steps"></a>Sonraki adımlar
Merhaba [Azure AD Geliştirici Kılavuzu] [ AAD-Dev-Guide] hello portal toouse tüm Azure AD geliştirme için olan ilgili konular, genel bir bakış da dahil olmak üzere [uygulama tümleştirmesi] [ AAD-How-To-Integrate] ve hello Temelleri [Azure AD kimlik doğrulama ve desteklenen kimlik doğrulama senaryoları][AAD-Auth-Scenarios].

Lütfen Açıklamalar bölümüne tooprovide geribildirim aşağıdaki hello kullanın ve daraltın ve yeni tanımları istekleri dahil olmak üzere veya var olanları güncelleştirme bizim içerik şekil yardımcı olur!

<!--Image references-->

<!--Reference style links -->
[AAD-App-Manifest]: ./active-directory-application-manifest.md
[AAD-App-SP-Objects]: ./active-directory-application-objects.md
[AAD-Auth-Scenarios]: ./active-directory-authentication-scenarios.md
[AAD-Dev-Guide]: ./active-directory-developers-guide.md
[AAD-Graph-Perm-Scopes]: https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-graph-api-permission-scopes
[AAD-Graph-App-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#application-entity
[AAD-Graph-Sp-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity
[AAD-Graph-User-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#user-entity
[AAD-How-Subscriptions-Assoc]: ../active-directory-how-subscriptions-associated-directory.md
[AAD-How-To-Integrate]: ./active-directory-how-to-integrate.md
[AAD-How-To-Tenant]: active-directory-howto-tenant.md
[AAD-Integrating-Apps]: ./active-directory-integrating-applications.md
[AAD-Multi-Tenant-Overview]: active-directory-devhowto-multi-tenant-overview.md
[AAD-Security-Token-Claims]: ./active-directory-authentication-scenarios/#claims-in-azure-ad-security-tokens
[AAD-Tokens-Claims]: ./active-directory-token-and-claims.md
[AZURE-portal]: https://portal.azure.com
[Duyshant-Role-Blog]: http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/
[JWT]: https://tools.ietf.org/html/draft-ietf-oauth-json-web-token-32
[Microsoft-Graph]: https://graph.microsoft.io
[O365-Perm-Ref]: https://msdn.microsoft.com/en-us/office/office365/howto/application-manifest
[OAuth2-Access-Token-Scopes]: https://tools.ietf.org/html/rfc6749#section-3.3
[OAuth2-AuthZ-Endpoint]: https://tools.ietf.org/html/rfc6749#section-3.1
[OAuth2-AuthZ-Grant-Types]: https://tools.ietf.org/html/rfc6749#section-1.3
[OAuth2-Client-Types]: https://tools.ietf.org/html/rfc6749#section-2.1
[OAuth2-Role-Def]: https://tools.ietf.org/html/rfc6749#page-6
[OpenIDConnect]: http://openid.net/specs/openid-connect-core-1_0.html
[OpenIDConnect-AuthZ-Endpoint]: http://openid.net/specs/openid-connect-core-1_0.html#AuthorizationEndpoint
[OpenIDConnect-ID-Token]: http://openid.net/specs/openid-connect-core-1_0.html#IDToken
