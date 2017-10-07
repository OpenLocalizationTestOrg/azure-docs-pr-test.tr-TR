---
title: "Azure AD uygulama proxy'si aaaSecurity dikkate alınacak noktalar | Microsoft Docs"
description: "Azure AD uygulama proxy'si kullanarak güvenlik konuları kapsar"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: ebd14b9d1fc8f4629c5916e5a910595727d935d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="security-considerations-for-accessing-apps-remotely-with-azure-ad-application-proxy"></a>Uygulamaları Azure AD uygulama proxy'si ile uzaktan erişim için güvenlik konuları

Bu makale, Azure Active Directory Uygulama proxy'si yayımlama ve uygulamalarınızı uzaktan erişim için güvenli bir hizmet nasıl sağladığını açıklar.

Aşağıdaki diyagramda gösterildiği nasıl Azure AD hello tooyour şirket içi uygulamalara güvenli uzaktan erişim sağlar.

 ![Azure AD uygulama proxy'si aracılığıyla güvenli uzaktan erişim diyagramı](./media/application-proxy-security-considerations/secure-remote-access.png)

## <a name="security-benefits"></a>Güvenlik avantajları

Azure AD uygulama proxy'si güvenlik avantajlarından aşağıdaki hello sunar:

### <a name="authenticated-access"></a>Kimliği doğrulanmış erişim 

Toouse Azure Active Directory ön kimlik doğrulamasını seçerseniz, yalnızca kimliği doğrulanmış bağlantılar ağınıza erişebilirsiniz.

Azure AD uygulama proxy'si hello Azure AD güvenlik belirteci hizmeti (STS) tüm kimlik doğrulaması için kullanır.  Ön kimlik doğrulaması, yalnızca kimliği doğrulanmış kimlikleri Merhaba arka uç uygulaması erişebildiğinden gereği, anonim saldırıları, çok sayıda engeller.

Ön kimlik doğrulaması yöntemi olarak geçiş seçerseniz, bu avantajı elde etmezsiniz. 

### <a name="conditional-access"></a>Koşullu erişim

Tooyour ağ kurulan bağlantılar önce daha zengin İlkesi denetimleri uygulayın.

İle [koşullu erişim](active-directory-conditional-access-azuread-connected-apps.md), tanımlayabileceğiniz hangi trafik kısıtlamalar izin tooaccess arka uç uygulamalarınızı. Oturum açma işlemleri kimlik doğrulama ve kullanıcı riski profili gücünü konuma göre kısıtlayan ilkeler oluşturabilirsiniz.

Güvenlik tooyour kullanıcı kimlik doğrulamalarını, başka bir katman ekleme koşullu erişim tooconfigure çok faktörlü kimlik doğrulama ilkelerini de kullanabilirsiniz. 

### <a name="traffic-termination"></a>Trafik sonlandırma

Tüm trafiği hello bulutta sonlandırılır.

Azure AD uygulama proxy'si ters proxy olduğundan, tüm trafik tooback uç uygulamaları hello hizmeti tarafından sonlandırılır. Merhaba oturum yalnızca hello arka uç sunucuyla yeniden sunulan toodirect HTTP trafiği arka uç sunucusu olmayan anlamına gelir. Bu yapılandırma, hedeflenen saldırılara karşı daha iyi korunur anlamına gelir.

### <a name="all-access-is-outbound"></a>Tüm erişim giden 

Tooopen gelen bağlantıları toohello şirket ağı gerekmez.

Uygulama proxy'si bağlayıcıları yalnızca tooopen güvenlik duvarı bağlantı noktalarını gelen bağlantılar için gerekli olduğu anlamına gelir giden bağlantılar toohello Azure AD uygulama proxy'si hizmeti kullanın. Geleneksel proxy'leri bir çevre ağına gerekli (olarak da bilinen *DMZ*, *sivil bölge*, veya *Perdeli alt ağ*) ve erişim toounauthenticated izin verilir bağlantıları hello ağ sınırında. Bu senaryo, web uygulaması birçok ek yatırım ürünleri tooanalyze trafiğinin güvenlik duvarı ve toplama korumaları toohello ortam önermiş gereklidir. Uygulama proxy'si ile tüm bağlantıları giden olduğu ve güvenli bir kanal üzerinden gerçekleşmesi için bir çevre ağına gerekmez.

Bağlayıcılar hakkında daha fazla bilgi için bkz: [anlamak Azure AD uygulama proxy'si Bağlayıcılar](application-proxy-understand-connectors.md).

### <a name="cloud-scale-analytics-and-machine-learning"></a>Bulut ölçekli analizi ve makine öğrenme 

Modern güvenlik koruması alın.

Azure Active Directory'nin parçası olduğu için uygulama proxy'si yararlanabilirsiniz [Azure AD Identity Protection](active-directory-identityprotection.md), öğrenme tabanlı makine Intelligence ve hello Microsoft Security Response Center ve dijital Suçlar Birimi'nin veriler ile. Birlikte biz proaktif olarak güvenliği aşılmış hesaplarını tanımlayan ve bu yüksek riskli oturum açma işlemleri gerçek zamanlı koruma sağlar. Biz anonymizing ağlarına virüs bulaşmış cihazlardan ve alışılmadık ve tahmin edilemez konumlardan erişim gibi çok sayıda faktöre dikkate alın.

Bu raporlar ve olayları birçoğu, aynı zamanda güvenlik bilgileri ve Olay yönetimi (SIEM) sistemleri ile tümleştirme için bir API aracılığıyla zaten kullanılabilir.

### <a name="remote-access-as-a-service"></a>Bir hizmet olarak uzaktan erişim

Koruma ve şirket içi sunucular düzeltme eki uygulama hakkında tooworry yok.

Hala yüklenmemiş yazılım saldırıları, çok sayıda için hesapları. Her zaman hello en son güvenlik düzeltme eki ve yükseltmelerini almak için azure AD uygulama proxy'si Microsoft sahibi, bir Internet ölçeğinde hizmetidir.

Azure AD uygulama proxy'si tarafından yayımlanan uygulamaların tooimprove hello güvenlik, dizin oluşturma ve uygulamalarınızı arşivleme web Gezgin robots engelleyin. Bir web Gezgini robot yayımlanan bir uygulamanın robot kullanıcının ayarlarını almak için her çalıştığında uygulama proxy'si yanıtları içeren bir robots.txt dosyası ile `User-agent: * Disallow: /`.

## <a name="under-hello-hood"></a>Merhaba başlık altında

Azure AD uygulama proxy'si iki bölümden oluşur:

* bulut tabanlı hizmet Hello: Bu hizmet, Azure üzerinde çalışır ve burada hello dış istemci/kullanıcı bağlantıları yapılan olduğu.
* [Merhaba şirket içi Bağlayıcısı](application-proxy-understand-connectors.md): hello bağlayıcı bir şirket içi bileşeni hello Azure AD uygulama proxy'si hizmeti gelen istekleri dinler ve bağlantıları toohello iç uygulamaları işler. 

Bir akış hello bağlayıcı ile Merhaba uygulama proxy'si hizmeti arasında kurulan zaman:

* Merhaba bağlayıcı ilk ayarlanır.
* Merhaba bağlayıcı hello uygulama proxy'si hizmeti yapılandırma bilgileri çeker.
* Bir kullanıcı bir yayımlanan uygulamaya erişiyor.

>[!NOTE]
>SSL üzerinden tüm iletişimler ortaya ve bunlar her zaman hello bağlayıcı toohello uygulama proxy'si hizmeti kaynaklanan. Merhaba yalnızca giden hizmetidir.

Merhaba bağlayıcı bir istemci sertifikası tooauthenticate toohello neredeyse tüm çağrıları için uygulama proxy'si hizmeti kullanır. Merhaba yalnızca özel durum toothis hello ilk kurulum adım hello istemci sertifikası burada kurulur işlemidir.

### <a name="installing-hello-connector"></a>Merhaba bağlayıcısını yükleme

Merhaba bağlayıcı ilk olarak ayarlandığında, akış olaylarını aşağıdaki hello gerçekleşir:

1. Merhaba bağlayıcı kayıt toohello hizmeti hello yükleme hello Bağlayıcısı'nın bir parçası olarak gerçekleşir. Kullanıcılar kendi Azure AD yönetici kimlik bilgileri istendiğinde tooenter şunlardır. Bu kimlik doğrulamasını edinilen belirteci sonra toohello Azure AD uygulama proxy'si hizmeti sunulur.
2. Merhaba uygulama proxy'si hizmeti hello belirteci değerlendirir. Bunu hello kullanıcı belirteci hello hello Kiracı içinde bir şirket Yöneticisi için verilmiş sağlar. Merhaba kullanıcı bir yönetici değilse, hello işlem sonlandırıldı.
3. Merhaba bağlayıcı istemci sertifika isteği oluşturur ve, hello belirteç, toohello uygulama proxy'si hizmeti ile birlikte geçirir. Merhaba hizmeti sırayla hello belirteci doğrular ve hello istemci sertifika isteğini imzalar.
4. Merhaba bağlayıcı hello istemci sertifikasını hello uygulama proxy'si hizmeti ile gelecekteki iletişim için kullanır.
5. Hello bağlayıcı hello sistem yapılandırma verilerinin ilk bir çekme, istemci sertifikasını kullanarak hello hizmetinden gerçekleştirir ve şimdi hazır tootake isteği sayısıdır.

### <a name="updating-hello-configuration-settings"></a>Merhaba yapılandırma ayarları güncelleştiriliyor

Merhaba uygulama Proxy hizmeti başlangıç yapılandırma ayarlarını güncelleştirdiğinde, akış olaylarını aşağıdaki hello gerçekleşir:

1. Merhaba bağlayıcı toohello yapılandırma endpoint hello uygulama proxy'si hizmeti içinde istemci sertifikasını kullanarak bağlanır.
2. Merhaba istemci sertifikası doğrulandıktan sonra hello uygulama proxy'si hizmeti yapılandırma veri toohello Bağlayıcısı döndürür (örneğin, bağlayıcı hello hello bağlayıcı Grup parçası olmalıdır).
3. Merhaba geçerli sertifika 180 günden daha eski ise, hello bağlayıcı etkili bir şekilde hello istemci sertifikası 180 günde güncelleştirmeleri yeni bir sertifika isteği oluşturur.

### <a name="accessing-published-applications"></a>Yayımlanan uygulamalara erişme

Kullanıcılar yayımlanmış bir uygulama eriştiğinde hello aşağıdaki olaylar hello uygulama proxy'si hizmeti ile Merhaba uygulama ara sunucusu Bağlayıcısı arasındaki gerçekleşir:

1. [Merhaba hizmeti hello kullanıcı hello uygulaması için kimlik doğrulaması](#the-service-checks-the-configuration-settings-for-the-app)
2. [Merhaba hizmet isteği hello bağlayıcı sırasına yerleştirir.](#The-service-places-a-request-in-the-connector-queue)
3. [Bir bağlayıcı hello sırasından hello isteğini işler](#the-connector-receives-the-request-from-the-queue)
4. [Merhaba bağlayıcı için bir yanıt bekler](#the-connector-waits-for-a-response)
5. [Merhaba hizmet akışları veri toohello kullanıcısı](#the-service-streams-data-to-the-user)

Bu adımların her biri bir yerde neler hakkında daha fazla toolearn tutmak okunuyor.


#### <a name="1-hello-service-authenticates-hello-user-for-hello-app"></a>1. hello hizmeti hello kullanıcı hello uygulaması için kimlik doğrulaması

Merhaba uygulama toouse geçiş, ön kimlik doğrulaması yöntemi olarak yapılandırdıysanız, bu bölümdeki hello adımları atlanır.

Azure AD ile Merhaba uygulama toopreauthenticate yapılandırdıysanız, kullanıcılar yeniden yönlendirilen toohello Azure AD STS tooauthenticate ve hello aşağıdaki adımlar gerçekleşir:

1. Koşullu erişim ilkesi gereksinimlere hello belirli uygulama için uygulama proxy'si denetler. Bu adım, bu hello kullanıcı toohello uygulama atanan sağlar. İki aşamalı doğrulama gerekliyse, hello kimlik doğrulaması dizisi ikinci bir kimlik doğrulama yöntemi hello kullanıcıya sorar.

2. Tüm denetimler geçtikten sonra hello Azure AD STS Merhaba uygulaması için imzalı bir belirteç verir ve kullanıcı geri toohello uygulama proxy'si hizmeti yeniden yönlendirmeleri hello.

3. Uygulama proxy'si hello belirtecini toocorrect hello uygulama verilen doğrular. Diğer denetimleri de gerçekleştirir, o hello sağlama gibi belirteci Azure AD tarafından imzalanmış ve onun hala hello geçerli içinde penceredir.

4. Uygulama proxy'si kimlik doğrulaması toohello uygulama oluştu şifreli kimlik doğrulama tanımlama bilgisi tooindicate ayarlar. kimlik doğrulama hello hello kullanıcı adı dayanır gibi hello tanımlama bilgisi hello belirteci Azure AD'den ve diğer veriler temel alınarak bir sona erme zaman damgası içerir. Merhaba tanımlama bilgisi yalnızca toohello uygulama proxy'si hizmeti bilinen özel bir anahtarla şifrelenir.

5. Uygulama proxy'si yeniden yönlendirmeleri hello kullanıcı geri toohello başlangıçta URL istendi.

Herhangi bir kısmını hello ön kimlik doğrulama adımları başarısız olursa, hello kullanıcının isteği reddedilir ve hello kullanıcı hello sorunun hello kaynağını belirten bir ileti gösterilir.


#### <a name="2-hello-service-places-a-request-in-hello-connector-queue"></a>2. hello hizmet isteği hello bağlayıcı sırasına yerleştirir.

Bağlayıcılar bir giden bağlantı açık toohello uygulama proxy'si hizmeti tutun. Bir istek geldiğinde, açık olan bağlantıların hello hello bağlayıcı toopick için hello isteği yukarı hello hizmet sıralar.

Merhaba istek hello uygulama hello istek üstbilgileri, şifrelenmiş hello tanımlama bilgisi verileri gibi öğeleri içerir, hello Kullanıcı isteği hello ve hello hale istek kimliği. Merhaba şifreli tanımlama bilgisi verileri hello istekle gönderilen rağmen hello kimlik doğrulama tanımlama bilgisi değildir.

#### <a name="3-hello-connector-processes-hello-request-from-hello-queue"></a>3. hello bağlayıcı hello sırasından hello isteğini işler. 

Merhaba isteği temel alarak, uygulama proxy'si eylemleri aşağıdaki hello birini gerçekleştirir:

* Merhaba istek basit bir işlemle ise (örneğin, bir RESTful ile olduğu gibi hello gövdesi içinde veri yok *almak* isteği), hello Bağlayıcısı bağlantı toohello hedef iç kaynak yapar ve sonra bir yanıt için bekler.

* Merhaba isteği hello gövdesinde ilişkili veri varsa (örneğin, bir RESTful *POST* işlemi), hello bağlayıcı hello istemci sertifikası toohello uygulama proxy'si örneği kullanarak giden bir bağlantı sağlar. Bu bağlantı toorequest hello verileri yapar ve bir bağlantı toohello iç kaynağı açın. Merhaba bağlayıcısından hello isteği aldıktan sonra hello uygulama proxy'si hizmeti hello kullanıcı içerikten kabul başlar ve veri toohello Bağlayıcısı iletir. Merhaba bağlayıcı sırayla hello veri toohello iç kaynak iletir.

#### <a name="4-hello-connector-waits-for-a-response"></a>4. hello bağlayıcı için bir yanıt bekler.

Hello isteğini ve tüm içerik toohello iletimini geri sonra son tamamlandıktan, hello bağlayıcı için bir yanıt bekler.

Yanıt aldıktan sonra bir giden bağlantı toohello uygulama proxy'si hizmeti hello bağlayıcı yapar, tooreturn başlık ayrıntıları hello ve hello dönüş verileri akış başlamadan.

#### <a name="5-hello-service-streams-data-toohello-user"></a>5. hello hizmet akışları veri toohello kullanıcı. 

Merhaba uygulaması bazı işlenmesini burada ortaya çıkabilir. Uygulama proxy'si tootranslate üstbilgilerinde veya URL'leri uygulamanızda yapılandırdıysanız, bu işlem bu adım sırasında gerektiği şekilde gerçekleşir.


## <a name="next-steps"></a>Sonraki adımlar

[Azure AD uygulama proxy'si kullanırken ağ topolojisi hakkında önemli noktalar](application-proxy-network-topology-considerations.md)

[Azure AD uygulama proxy'si bağlayıcılar anlama](application-proxy-understand-connectors.md)
