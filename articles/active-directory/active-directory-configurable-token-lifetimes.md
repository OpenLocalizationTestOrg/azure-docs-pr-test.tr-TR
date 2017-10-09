---
title: "Azure Active Directory'de aaaConfigurable belirteci yaşam süreleri | Microsoft Docs"
description: "Nasıl tooset ömürleri belirteçler için Azure AD tarafından verilen öğrenin."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 06f5b317-053e-44c3-aaaa-cf07d8692735
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: billmath
ms.custom: aaddev
ms.reviewer: anchitn
ms.openlocfilehash: 0d4c8545981c5463cc7c95f669167bbc38230123
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configurable-token-lifetimes-in-azure-active-directory-public-preview"></a>Azure Active Directory'de (genel Önizleme) yapılandırılabilir belirteci yaşam süresi
Azure Active Directory (Azure AD) tarafından verilmiş bir belirteç ömrü hello belirtebilirsiniz. Kuruluşunuzdaki tüm uygulamalar, kuruluşunuzda, çok kiracılı (çok kuruluş) uygulama veya belirli hizmet sorumlusu belirteci yaşam süresi ayarlayabilirsiniz.

> [!NOTE]
> Bu özellik şu anda genel önizlemede değil. Toorevert hazırlanması veya herhangi bir değişiklik kaldırın. Genel Önizleme sırasında herhangi bir Azure Active Directory abonelik Hello özelliği kullanılabilir. Ancak, hello özelliği genel kullanıma sunulduğunda hello özelliği bazı yönlerini gerektirebilir bir [Azure Active Directory Premium](active-directory-get-started-premium.md) abonelik.
>
>

Azure AD'de bireysel uygulamaları ya da bir kuruluşta tüm uygulamaları zorlanan kuralları kümesi bir ilke nesnesi temsil eder. Her ilke türünün uygulanan tooobjects toowhich atanmış olan özellikler kümesi ile benzersiz bir yapısı var.

Kuruluşunuz için bir ilke hello varsayılan ilke olarak belirleyebilirsiniz. yüksek önceliğe sahip bir ilke tarafından kılınmayan sürece hello ilkesi uygulanan tooany hello kuruluşunuzdaki uygulamasıdır. Bir ilke toospecific uygulamalar da atayabilirsiniz. Merhaba öncelik sırasına göre ilke türüne göre değişir.


## <a name="token-types"></a>Belirteç türleri

Yenileme belirteçleri, erişim belirteçleri, oturum belirteçleri ve kimlik belirteçlerini belirteç ömrü ilkelerini ayarlayabilirsiniz.

### <a name="access-tokens"></a>Erişim belirteçleri
İstemcileri kullanımı erişim tooaccess korunan bir kaynağa belirteçleri. Bir erişim belirteci, kullanıcı, istemci ve kaynak yalnızca belirli bir birleşim için kullanılabilir. Erişim belirteci iptal edilemiyor ve bunların süre sonu kadar geçerlidir. Bir erişim belirteci elde kötü amaçlı bir aktör yaşam uzantı için kullanabilirsiniz. Merhaba ömrü ayarlama bir erişim belirteç sistem performansı iyileştirme arasında bir denge ve hello kullanıcı hesabı devre dışı bırakıldıktan sonra erişimi artan hello süreyi istemci hello korur. Geliştirilmiş sistem performansı kez tooacquire yeni erişim belirteci istemci gereken hello sayısını azaltarak elde edilir.

### <a name="refresh-tokens"></a>Yenileme belirteçlerini
Bir istemci bir erişim belirteci tooaccess korunan bir kaynağa elde ettiğinde hello istemci bir yenileme belirteci ve bir erişim belirteci alır. Merhaba geçerli erişim belirtecinin süresi dolduğunda hello yenileme belirteci kullanılan tooobtain yeni erişim/yenileme belirteci çiftleri ' dir. Bir yenileme belirteci ilişkili tooa kullanıcı ve istemci birleşimidir. Bir yenileme belirteci iptal edilebilir ve hello belirteci her kullanılışında hello belirtecin geçerlilik denetlenir.

Önemli toomake gizli ve ortak istemciler arasında bir ayrım olur. Farklı istemci türleri hakkında daha fazla bilgi için bkz: [RFC 6749](https://tools.ietf.org/html/rfc6749#section-2.1).

#### <a name="token-lifetimes-with-confidential-client-refresh-tokens"></a>Gizli istemci yenileme belirteçleri ile belirteci yaşam süresi
Gizli istemcileri güvenli bir şekilde bir istemci parolası (gizli) depolayabilirsiniz uygulamalardır. İsteklerin Merhaba istemci uygulaması ve kötü amaçlı aktör'ndan değil geldiğini kanıtlarlar. Örneğin, bir web uygulaması hello web sunucusunda bir istemci parolası depolayabileceğiniz gizli bir istemcidir. Bu açık değil. Bu akışlar daha güvenli olduğundan, yenileme belirteçleri verilen toothese akışları olan varsayılan ömrü hello `until-revoked`İlkesi kullanılarak değiştirilemez ve gönüllü parola sıfırlama üzerinde iptal değil.

#### <a name="token-lifetimes-with-public-client-refresh-tokens"></a>Ortak istemci yenileme belirteçleri ile belirteci yaşam süresi

Ortak istemcileri güvenli bir şekilde bir istemci parolası (gizli) depolanamıyor. Örneğin, ortak bir istemci olarak kabul edilir şekilde iOS/Android uygulama gizli anahtarı hello kaynak sahibinden belirsizleştirirseniz olamaz. Ortak istemcilerden gelen yeni bir erişim/yenileme belirteci çifti alma belirli bir süre şundan eski yararlı tooprevent yenileme belirteçleri kaynaklardaki ilkeleri ayarlayabilirsiniz. (toodo Bu, kullanım hello yenileme belirteci etkin olmayan zaman sınırı özelliğini.) Bir süre hangi hello yenileme belirteçleri ötesinde artık kabul ilkeleri tooset de kullanabilirsiniz. (toodo Bu, kullanım hello yenileme belirteci Maksimum yaş özelliğini.) Zaman ve ne sıklıkta hello kullanıcı sessiz bir şekilde, bir ortak istemci uygulamasını kullanırken, yeniden kimlik doğrulaması yerine gerekli tooreenter kimlik bilgileri olan bir yenileme belirteci toocontrol hello ömrü ayarlayabilirsiniz.

### <a name="id-tokens"></a>Kimliği belirteçleri
Kimlik belirteçlerini toowebsites ve yerel istemci geçirilir. Kimlik belirteçlerini bir kullanıcı profili bilgilerini içerir. Bir kimliği belirteci ilişkili tooa belirli kullanıcı ve istemci birleşimidir. Kimlik belirteçlerini kendi süre sonu kadar geçerli kabul edilir. Genellikle, bir kullanıcının bir web uygulaması eşleşip hello uygulama toohello hello kimliği belirteç ömrü oturum yaşam süresi hello kullanıcı için verilen. Merhaba web uygulaması hello uygulama oturumu ve ne sıklıkta hello kullanıcı toobe (Sessiz veya etkileşimli) Azure AD ile yeniden kimlik doğrulaması gerektiren süresi bir kimliği belirteci toocontrol ne sıklıkta hello ömrü ayarlayabilirsiniz.

### <a name="single-sign-on-session-tokens"></a>Tek oturum açma oturumu belirteçleri
Ne zaman bir kullanıcı Azure AD ile doğrular ve seçer hello **Oturumumu açık bırak** onay kutusu, bir tek oturum açma (SSO) hello kullanıcının tarayıcı ve Azure AD ile oturumun. bir tanımlama bilgisi hello biçiminde Hello SSO belirteci bu oturumu temsil eder. Bu hello SSO Oturum belirteci ilişkili tooa belirli bir kaynak/istemci uygulaması değil unutmayın. SSO oturum belirteçleri iptal edilebilir ve kullanıldıkları her zaman geçerliliği denetlenir.

Azure AD iki tür SSO oturum belirteçleri kullanır: kalıcı ve kalıcı olmayan. Kalıcı oturum belirteçleri kalıcı tanımlama bilgileri hello tarayıcı tarafından depolanır. Kalıcı olmayan oturum belirteç oturum tanımlama bilgileri depolanır. (Merhaba tarayıcı kapatıldığında oturum tanımlama bilgileri yok.)

Kalıcı olmayan oturum belirteçleri 24 saatlik bir ömrü vardır. Kalıcı belirteçleri 180 gün ömrü vardır. SSO Oturum belirteci, geçerlilik süresi içinde kullanılan dilediğiniz zaman hello geçerlilik süresi, başka bir 24 saat veya hello belirteci türüne bağlı olarak 180 gün genişletilir. SSO Oturum belirteci, geçerlilik süresi içinde kullanılmazsa, olarak kabul süresi doldu ve artık kabul edilir.

Merhaba ilk oturum belirteci hangi hello artık oturum belirteci kabul verilmiş bir ilke tooset hello süre sonra kullanabilirsiniz. (toodo Bu, kullanım hello Oturum belirteci Maksimum yaş özelliğini.) Zaman ve ne sıklıkta bir kullanıcı sessiz bir şekilde, bir web uygulaması kullanırken kimlik doğrulaması gerçekleştirilen yerine gerekli tooreenter kimlik bilgileri olan bir oturum belirteci toocontrol hello ömrü ayarlayabilirsiniz.

### <a name="token-lifetime-policy-properties"></a>Belirteç ömrü ilkesi özellikleri
Belirteç ömrü ilkesi, belirteç ömrü kuralları içeren ilke nesne türüdür. Kullanım hello hello İlkesi toocontrol özelliklerini belirteci yaşam süresi belirtilen. İlke yok ayarlarsanız hello sistem hello varsayılan yaşam süresi değeri zorlar.

### <a name="configurable-token-lifetime-properties"></a>Yapılandırılabilir belirteç ömrü özellikleri
| Özellik | İlke özellik dizesi | Etkiler | Varsayılan | Minimum | Maksimum |
| --- | --- | --- | --- | --- | --- |
| Erişim belirteci ömrü |AccessTokenLifetime |Erişim belirteçleri, kimlik belirteçlerini, SAML2 belirteçleri |1 saat |10 dakika |1 gün |
| Etkin olmayan zaman belirteci sınırı Yenile |MaxInactiveTime |Yenileme belirteçlerini |14 gün |10 dakika |90 gün |
| Tek Faktörlü yenileme belirteci Maksimum yaş |MaxAgeSingleFactor |Yenileme belirteçlerini (tüm kullanıcılar için) |Kadar iptal |10 dakika |Kadar iptal<sup>1</sup> |
| Çok faktörlü yenileme belirteci Maksimum yaş |MaxAgeMultiFactor |Yenileme belirteçlerini (tüm kullanıcılar için) |Kadar iptal |10 dakika |Kadar iptal<sup>1</sup> |
| Tek Faktörlü Oturum belirteci Maksimum yaş |MaxAgeSessionSingleFactor<sup>2</sup> |Oturum belirteçleri (kalıcı ve kalıcı olmayan) |Kadar iptal |10 dakika |Kadar iptal<sup>1</sup> |
| Çok faktörlü Oturum belirteci Maksimum yaş |MaxAgeSessionMultiFactor<sup>3</sup> |Oturum belirteçleri (kalıcı ve kalıcı olmayan) |Kadar iptal |10 dakika |Kadar iptal<sup>1</sup> |

* <sup>1</sup>365 gündür bu öznitelikler için ayarlanabilecek hello açık uzunluk.
* <sup>2</sup>varsa **MaxAgeSessionSingleFactor** ayarlanmazsa bu değeri alır hello **MaxAgeSingleFactor** değeri. Hiçbir parametre ayarlanırsa hello özelliği hello varsayılan değer (kadar iptal edilen) alır.
* <sup>3</sup>varsa **MaxAgeSessionMultiFactor** ayarlanmazsa bu değeri alır hello **MaxAgeMultiFactor** değeri. Hiçbir parametre ayarlanırsa hello özelliği hello varsayılan değer (kadar iptal edilen) alır.

### <a name="exceptions"></a>Özel durumlar
| Özellik | Etkiler | Varsayılan |
| --- | --- | --- |
| Belirteç Maksimum yaş Yenile (yetersiz iptal bilgilerini federe kullanıcılar için verilen<sup>1</sup>) |Yenileme belirteçlerini (yetersiz iptal bilgilerini federe kullanıcılar için verilen<sup>1</sup>) |12 saat |
| Belirteç etkin olmayan (gizli istemcileri için verilen) zaman sınırı Yenile |Yenileme belirteçlerini (gizli istemcileri için verilen) |90 gün |
| Belirteç Maksimum yaş (gizli istemcileri için verilen) Yenile |Yenileme belirteçlerini (gizli istemcileri için verilen) |Kadar iptal |

* <sup>1</sup>yetersiz iptal bilgilerini olmayan tüm kullanıcılar dahil olan federe kullanıcılar hello eşitlenen "LastPasswordChangeTimestamp" özniteliği. Eski (değiştirilmiş bir parola gibi) kimlik bilgisi ve geri daha sık tooensure içinde hello kullanıcı denetlemelidir tooan toorevoke belirteçler bağlı olduğunda AAD oluşturulamıyor tooverify olduğundan bu kullanıcılar bu kısa Maksimum yaş verilir ve ilişkili belirteçler hala olan iyi durumu içinde. Bu deneyim, Kiracı yöneticileri bunlar eşitleniyor olmanız gerekir (Bu Powershell kullanarak hello kullanıcı nesnesi veya Modu'nu aracılığıyla ayarlanabilir) "LastPasswordChangeTimestamp" özniteliği hello tooimprove.

### <a name="policy-evaluation-and-prioritization"></a>İlke değerlendirmesi ve öncelik belirleme
Oluşturma ve belirteç ömrü ilkesi tooa belirli bir uygulama, tooyour kuruluş ve tooservice ilkeleri atayın. Birden çok ilke tooa belirli uygulama uygulanabilir. etkinleşir hello belirteç ömrü ilkesi bu kurallar aşağıdaki gibidir:

* Bir ilke açıkça toohello hizmet sorumlusu atanmışsa zorlanır.
* İlke yok açıkça atanan toohello hizmet sorumlusu ise, açıkça toohello üst hello hizmet sorumlusu kuruluşu atanmış bir ilke uygulanır.
* İlke yok açıkça toohello hizmet sorumlusu veya toohello kuruluş atanırsa, atanan toohello uygulama hello ilkesi uygulanır.
* İlke yok toohello hizmet sorumlusu, hello kuruluş veya hello uygulama nesnesi, hello varsayılan değerleri atanmışsa zorlanır. (Merhaba tabloya bakın [yapılandırılabilir belirteç ömrü özellikleri](#configurable-token-lifetime-properties).)

Merhaba uygulama ve hizmet asıl nesneleri arasındaki ilişki hakkında daha fazla bilgi için bkz: [uygulama ve hizmet asıl nesneler Azure Active Directory'de](active-directory-application-objects.md).

Bir belirtecin geçerlilik hello belirteci kullanılır hello zamanında değerlendirilir. Hello İlkesi hello erişiliyor hello uygulama üzerinde en yüksek önceliğe sahip etkinleşir.

> [!NOTE]
> Burada, örnek bir senaryo verilmiştir.
>
> Bir kullanıcının tooaccess iki web uygulamaları istediği: bir Web uygulaması ve Web uygulama b
> 
> Faktörleri:
> * Her iki web uygulaması hello olan aynı üst kuruluş.
> * Belirteç ömrü ilkesi 1 ile bir oturum belirteci Maksimum yaş sekiz saat hello üst kuruluşunuzun varsayılan olarak ayarlanır.
> * Web uygulaması A normal kullanım web uygulaması ve bağlantılı tooany ilkeleri değil.
> * Web uygulaması B son derece hassas işlemler için kullanılır. Kendi hizmet sorumlusu bir oturum belirteci Maksimum yaş 30 dakika olan bağlantılı tooToken ömrü ilkesi 2 ' dir.
>
> 12:00 PM hello kullanıcı yeni bir tarayıcı oturumu başlatır ve çalıştığında tooaccess Web Uygulama A. hello kullanıcı yeniden yönlendirilen tooAzure AD ve toosign içinde sorulan. Oturum belirteci hello tarayıcıda sahip bir tanımlama bilgisi oluşturur. Merhaba, yeniden yönlendirilen geri tooWeb uygulama A Merhaba uygulaması hello kullanıcı tooaccess izin veren bir kimliği belirteci ile kullanıcıdır.
>
> 12:15 PM hello kullanıcı tooaccess Web uygulama B. hello tarayıcı yeniden yönlendirmeleri tooAzure hello oturum tanımlama bilgisi algılar AD çalışır. Web uygulaması B'nin hizmet sorumlusu, bağlantılı tooToken ömrü ilkesi 2 olmakla birlikte varsayılan belirteç ömrü ilkesi 1 ile Merhaba üst kuruluş parçası olduğunu da. İlkeleri bağlantılı tooservice sorumluları kuruluş varsayılan ilkelerden daha yüksek önceliğe sahip olduğundan belirteç ömrü ilkesi 2 etkinleşir. geçerli kabul edilir şekilde hello Oturum belirteci son 30 dakika içinde hello ilk yayımlandığında. Merhaba, yeniden yönlendirilen geri tooWeb uygulama B erişim veren bir kimliği belirteci ile kullanıcıdır.
>
> 1: 00'da, hello çalıştığında tooaccess Web Uygulama A. hello kullanıcı yeniden yönlendirilen tooAzure AD ' dir. Web Uygulama A bağlantılı tooany ilkeleri değildir, ancak varsayılan belirteç ömrü ilkesi 1 olan bir kuruluşta olduğu için bu ilke etkili olur. Son sekiz saat içinde hello ilk yayımlandığında hello oturum tanımlama bilgisi algılandı. Hello, sessiz bir şekilde yeniden yönlendirilen geri tooWeb uygulama A yeni bir kimliği belirteci ile kullanıcıdır. Merhaba kullanıcı gerekli tooauthenticate değil.
>
> Daha sonra hello kullanıcı çalıştığında hemen tooaccess Web uygulama B. hello yeniden yönlendirilen tooAzure AD kullanıcıdır. Olarak daha önce belirteç ömrü ilkesi 2 etkinleşir. Merhaba belirteci 30 dakikadan daha önce verilmiş, hello kullanıcı istendiğinde tooreenter olduğundan oturum açma kimlik bilgilerini. Yeni Oturum belirteci ve kimliği belirteci verilir. Merhaba kullanıcı daha sonra Web uygulama B. erişebilirsiniz
>
>

## <a name="configurable-policy-property-details"></a>Yapılandırılabilir İlkesi özellik ayrıntıları
### <a name="access-token-lifetime"></a>Erişim belirteci ömrü
**Dize:** AccessTokenLifetime

**Etkiler:** erişim belirteçleri, kimlik belirteçlerini

**Özet:** Bu ilke ne kadar süreyle erişim ve kimliği belirteçleri bu kaynak için geçerli olarak kabul denetler. Merhaba erişim belirteç ömrü özelliği azaltma bir erişim belirteci veya kötü amaçlı bir oyuncu tarafından uzun bir süre için kullanılan kimliği belirteci hello riskini azaltır. (Bu belirteçleri iptal edilemiyor.) Merhaba dengelemeyi performansı olumsuz şekilde etkilenir daha sık değiştirilen toobe Hello belirteçlere sahip olmasıdır.

### <a name="refresh-token-max-inactive-time"></a>Etkin olmayan zaman belirteci sınırı Yenile
**Dize:** MaxInactiveTime

**Etkiler:** yenileme belirteçleri

**Özet:** Bu ilke bir istemci artık tooretrieve yeni bir erişim/yenileme belirteci çifti tooaccess bu kaynak çalışırken kullanmadan önce ne kadar eski bir yenileme belirteci olabilir denetler. Bir yenileme belirteci kullanıldığında, yeni bir yenileme belirteci genellikle döndürüldüğünden hello istemci sırasında hello hello geçerli yenileme belirtecini kullanarak herhangi bir kaynağa süre belirtilen tooaccess çalışırsa, bu ilke erişimi engeller.

Bu ilke, istemci tooreauthenticate tooretrieve yeni bir yenileme belirteci etkin edilmemiş kullanıcılar zorlar.

Merhaba yenileme belirteci etkin olmayan zaman sınırı özelliği hello tek Etmenli belirteci Maksimum yaş değerinden daha düşük değer tooa ve hello multi-Factor yenileme belirteci Maksimum yaş özelliklerini ayarlamanız gerekir.

### <a name="single-factor-refresh-token-max-age"></a>Tek Faktörlü yenileme belirteci Maksimum yaş
**Dize:** MaxAgeSingleFactor

**Etkiler:** yenileme belirteçleri

**Özet:** Bu ilke denetimleri uzun bir kullanıcı yeni bir yenileme belirteci tooget kullanabilirsiniz nasıl erişim/token çifti son yalnızca tek bir faktörü kullanarak kimlik doğrulamasının sonra yenileme. Bir kullanıcının kimliğini doğrular ve yeni bir yenileme belirteci aldıktan sonra hello kullanıcı için belirtilen hello hello yenileme belirteci akışı kullanabilir dönem süre. (Bu hello geçerli yenileme belirteci iptal ve, hello etkin olmayan saatten daha uzun bir süre kullanılmayan bırakılır değil sürece geçerlidir.) Bu noktada, zorla tooreauthenticate tooreceive yeni bir yenileme belirteci hello kullanıcıdır.

Merhaba Maksimum yaş azaltarak kullanıcıların tooauthenticate daha sık zorlar. Tek faktörlü kimlik doğrulaması çok faktörlü kimlik doğrulamasından daha az güvenli olduğu kabul edildiği için bu özellik tooa değeri ayarlamanızı öneririz yani eşit tooor hello multi-Factor yenileme belirteci Maksimum yaş özelliği küçüktür.

### <a name="multi-factor-refresh-token-max-age"></a>Çok faktörlü yenileme belirteci Maksimum yaş
**Dize:** MaxAgeMultiFactor

**Etkiler:** yenileme belirteçleri

**Özet:** Bu ilke denetimleri uzun bir kullanıcı yeni bir yenileme belirteci tooget kullanabilirsiniz nasıl erişim/token çifti son birden çok faktörünü kullanarak kimlik doğrulamasının sonra yenileme. Bir kullanıcının kimliğini doğrular ve yeni bir yenileme belirteci aldıktan sonra hello kullanıcı için belirtilen hello hello yenileme belirteci akışı kullanabilir dönem süre. (Bu hello geçerli yenileme belirteci iptal ve hello etkin olmayan saatten daha uzun bir süre kullanılmayan değil sürece geçerlidir.) Bu noktada, kullanıcıların tooreauthenticate tooreceive yeni bir yenileme belirteci zorlanır.

Merhaba Maksimum yaş azaltarak kullanıcıların tooauthenticate daha sık zorlar. Tek faktörlü kimlik doğrulaması çok faktörlü kimlik doğrulamasından daha az güvenli olduğu kabul edildiği için eşit tooor hello tek Faktörlü yenileme belirteci Maksimum yaş özelliğinden büyük olduğundan bu özellik tooa değeri ayarlamanızı öneririz.

### <a name="single-factor-session-token-max-age"></a>Tek Faktörlü Oturum belirteci Maksimum yaş
**Dize:** MaxAgeSessionSingleFactor

**Etkiler:** oturum belirteçleri (kalıcı ve kalıcı olmayan)

**Özet:** bir kullanıcının, yeni bir kimliği ve oturum token son yalnızca tek bir faktörü kullanarak kimlik doğrulamasının sonra oturum belirteci tooget kullanabileceği Bu ilke denetimleri ne kadar süre. Bir kullanıcının kimliğini doğrular ve yeni oturum belirteci aldıktan sonra hello kullanıcı için belirtilen hello hello Oturum belirteci akışı kullanabilir dönem süre. (Merhaba geçerli oturum belirteci iptal ve süresi geçmemiş sürece bu doğrudur.) Merhaba süre belirtilen sonra hello zorlanmış tooreauthenticate tooreceive yeni oturum belirteci kullanıcıdır.

Merhaba Maksimum yaş azaltarak kullanıcıların tooauthenticate daha sık zorlar. Tek faktörlü kimlik doğrulaması çok faktörlü kimlik doğrulamasından daha az güvenli olduğu kabul edildiği için eşit hello'den küçük tooor çok faktörlü Oturum belirteci Maksimum yaş özelliği bu özellik tooa değeri ayarlamanızı öneririz.

### <a name="multi-factor-session-token-max-age"></a>Çok faktörlü Oturum belirteci Maksimum yaş
**Dize:** MaxAgeSessionMultiFactor

**Etkiler:** oturum belirteçleri (kalıcı ve kalıcı olmayan)

**Özet:** bir kullanıcının, yeni bir kimliği ve oturum belirteci sonra oturum belirteci tooget kullanabileceği Bu ilke denetimleri ne kadar süreyle hello doğrulandığını başarıyla birden çok faktörünü kullanarak son zamanı. Bir kullanıcının kimliğini doğrular ve yeni oturum belirteci aldıktan sonra hello kullanıcı için belirtilen hello hello Oturum belirteci akışı kullanabilir dönem süre. (Merhaba geçerli oturum belirteci iptal ve süresi geçmemiş sürece bu doğrudur.) Merhaba süre belirtilen sonra hello zorlanmış tooreauthenticate tooreceive yeni oturum belirteci kullanıcıdır.

Merhaba Maksimum yaş azaltarak kullanıcıların tooauthenticate daha sık zorlar. Tek faktörlü kimlik doğrulaması çok faktörlü kimlik doğrulamasından daha az güvenli olduğu kabul edildiği için eşit tooor hello tek Faktörlü Oturum belirteci Maksimum yaş özelliğinden büyük olduğundan bu özellik tooa değeri ayarlamanızı öneririz.

## <a name="example-token-lifetime-policies"></a>Örnek belirteç ömrü ilkeleri
Birçok senaryoları oluşturabilir ve uygulamaları, hizmet asıl adı ve genel kuruluşunuz için belirteç ömürleri yönetmek zaman Azure AD'de mümkündür. Bu bölümde, yeni kurallar için zorunlu tuttukları yardımcı olacak birkaç ilke senaryoları size rehberlik eder:

* Belirteç ömrü
* Etkin olmayan zaman belirteci sınırı
* Belirteç Maksimum yaş

Merhaba örneklerde öğrenebilir nasıl yapılır:

* Bir kuruluşun varsayılan ilkesini yönetme
* Web oturum açma için bir ilke oluşturun
* Web API'si çağıran yerel bir uygulama için bir ilke oluşturun
* Gelişmiş ilkesini yönetme

### <a name="prerequisites"></a>Ön koşullar
Merhaba, örnek olarak oluşturmak, güncelleştirme, bağlantı ve uygulamaları, hizmet asıl adı ve genel kuruluşunuz için ilkelerini silin. Yeni tooAzure AD varsa, hakkında bilgi edinin öneririz [nasıl tooget bir Azure AD Kiracı](active-directory-howto-tenant.md) bu örnekleri ile devam etmeden önce.  

başlatıldı, tooget hello adımları izleyin:

1. Merhaba son karşıdan [Azure AD PowerShell modülü genel Önizleme sürümü](https://www.powershellgallery.com/packages/AzureADPreview).
2. Merhaba çalıştırmak `Connect` komutu toosign tooyour Azure AD yönetim hesabı olarak. Her zaman bu komutu çalıştırmak yeni bir oturum başlatın.

    ```PowerShell
    Connect-AzureAD -Confirm
    ```

3. toosee kuruluşunuzda aşağıdaki çalışma hello oluşturulan tüm ilkeler komutu. Çoğu işlemlerinde senaryoları aşağıdaki hello sonra bu komutu çalıştırın. Hello komut ayrıca hello size yardımcı çalıştıran ** **, ilkelerinizin.

    ```PowerShell
    Get-AzureADPolicy
    ```

### <a name="example-manage-an-organizations-default-policy"></a>Örnek: bir kuruluşun varsayılan ilkesini yönetme
Bu örnekte, tüm kuruluş genelinde daha az sıklıkta oturum açın, kullanıcılarınızın sağlayan bir ilkesi oluşturun. toodo Bu, tek Faktörlü Yenile kuruluşunuz genelinde uygulanan belirteçleri, bir belirteç ömrü ilkesi oluşturun. Merhaba, kuruluşunuz ve bir ilke kümesi zaten yok tooeach hizmet sorumlusu uygulanan tooevery uygulamada ilkesidir.

1. Bir belirteç ömrü ilkesi oluşturun.

    1.  Çok "kadar iptal edilen." Merhaba tek Faktörlü yenileme belirteci ayarlayın erişimi iptal kadar hello belirtecinin kullanım süresi sona ermiyor. İlke tanımı aşağıdaki hello oluşturun:

        ```PowerShell
        @('{
            "TokenLifetimePolicy":
            {
                "Version":1,
                "MaxAgeSingleFactor":"until-revoked"
            }
        }')
        ```

    2.  toocreate hello İlkesi, hello aşağıdaki komutu çalıştırın:

        ```PowerShell
        New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1, "MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "OrganizationDefaultPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"
        ```

    3.  toosee yeni ilke ve tooget hello İlkesi'nin **objectID**çalıştırın hello komutu aşağıdaki:

        ```PowerShell
        Get-AzureADPolicy
        ```

2. Hello İlkesi güncelleştirin.

    Bu örnekte, ayarladığınız hello ilk ilke hizmetiniz için gerekli olarak katı değil karar verebilirsiniz. iki gün içinde tek Faktörlü yenileme belirteci, tooexpire tooset çalıştırmak hello komutu:

    ```PowerShell
    Set-AzureADPolicy -Id <ObjectId FROM GET COMMAND> -DisplayName "OrganizationDefaultPolicyUpdatedScenario" -Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxAgeSingleFactor":"2.00:00:00"}}')
    ```

### <a name="example-create-a-policy-for-web-sign-in"></a>Örnek: web oturum açma için bir ilke oluşturun

Bu örnekte, web uygulamanızda daha sık kullanıcılar tooauthenticate gerektiren bir ilke oluşturun. Bu ilke hello erişim/kimlik belirteçlerini hello ömrü ve hello Maksimum yaş çok faktörlü Oturum belirteci toohello hizmet asıl web uygulamanızın ayarlar.

1. Bir belirteç ömrü ilkesi oluşturun.

    Bu ilke için web oturum açma, hello erişim/kimliği belirteç ömrü ve hello max tek Faktörlü Oturum belirteci yaş tootwo saatleri ayarlar.

    1.  toocreate hello İlkesi, bu komutu çalıştırın:

        ```PowerShell
        New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1,"AccessTokenLifetime":"02:00:00","MaxAgeSessionSingleFactor":"02:00:00"}}') -DisplayName "WebPolicyScenario" -IsOrganizationDefault $false -Type "TokenLifetimePolicy"
        ```

    2.  toosee yeni ilke ve tooget hello İlkesi **objectID**çalıştırın hello komutu aşağıdaki:

        ```PowerShell
        Get-AzureADPolicy
        ```

2.  Hello İlkesi tooyour hizmet sorumlusu atayın. Tooget hello etmeniz **objectID** hizmet asıl. 

    1.  toosee kuruluşunuzun tüm hizmet asıl adı, Sorgulayabileceğiniz [Microsoft Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity). Veya, [Azure AD Graph Explorer'a](https://graphexplorer.cloudapp.net/), tooyour Azure AD hesabının oturum açın.

    2.  Merhaba olduğunda **objectID** , hizmet sorumlusu komutu aşağıdaki hello çalıştırın:

        ```PowerShell
        Add-AzureADServicePrincipalPolicy -Id <ObjectId of hello ServicePrincipal> -RefObjectId <ObjectId of hello Policy>
        ```


### <a name="example-create-a-policy-for-a-native-app-that-calls-a-web-api"></a>Örnek: web API'si çağıran yerel bir uygulama için bir ilke oluşturun
Bu örnekte, kullanıcıların tooauthenticate daha az sıklıkla gerektiren bir ilke oluşturun. Hello İlkesi de hello süreyi hello kullanıcı sağlamalarını gerekir önce bir kullanıcı devre dışı olabilir uzatır. Hello ilkesi uygulanan toohello web API'dır. Bir kaynak olarak hello web API Hello yerel uygulama istediğinde, bu ilke uygulanır.

1. Bir belirteç ömrü ilkesi oluşturun.

    1.  toocreate web API'si, komutu aşağıdaki hello çalıştırmak için bir katı İlkesi:

        ```PowerShell
        New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxInactiveTime":"30.00:00:00","MaxAgeMultiFactor":"until-revoked","MaxAgeSingleFactor":"180.00:00:00"}}') -DisplayName "WebApiDefaultPolicyScenario" -IsOrganizationDefault $false -Type "TokenLifetimePolicy"
        ```

    2.  toosee yeni ilke ve tooget hello İlkesi **objectID**çalıştırın hello komutu aşağıdaki:

        ```PowerShell
        Get-AzureADPolicy
        ```

2. Hello İlkesi tooyour web API atayın. Tooget hello etmeniz **objectID** uygulamanızın. Uygulamanızın en iyi şekilde toofind hello **objectID** toouse hello olan [Azure portal](https://portal.azure.com/).

   Merhaba olduğunda **objectID** , uygulamanızın hello aşağıdaki komutu çalıştırın:

        ```PowerShell
        Add-AzureADApplicationPolicy -Id <ObjectId of hello Application> -RefObjectId <ObjectId of hello Policy>
        ```


### <a name="example-manage-an-advanced-policy"></a>Örnek: bir Gelişmiş ilkesini yönetme
Bu örnekte, birkaç ilkeleri, hello öncelik sisteminin nasıl çalıştığı toolearn oluşturun. Ayrıca öğrenebilirsiniz nasıl toomanage uygulanan tooseveral nesneler birden çok ilke.

1. Bir belirteç ömrü ilkesi oluşturun.

    1.  toocreate hello tek Faktörlü yenileme belirteci ömrü too30 gün, komutu aşağıdaki hello çalıştırmak ayarlar bir kuruluş varsayılan ilke:

        ```PowerShell
        New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxAgeSingleFactor":"30.00:00:00"}}') -DisplayName "ComplexPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"
        ```

    2.  toosee yeni ilke ve tooget hello İlkesi'nin **objectID**çalıştırın hello komutu aşağıdaki:

        ```PowerShell
        Get-AzureADPolicy
        ```

2. Hello İlkesi tooa hizmet sorumlusu atayın.

    Artık, kuruluşun tamamına toohello geçerli bir ilkesi var. Belirli hizmet sorumlusu için bu 30 günlük ilkesi toopreserve istiyor ancak "kadar iptal edilen.", hello kuruluş varsayılan ilke toohello üst sınırı değiştirmek

    1.  toosee kuruluşunuzun tüm hizmet asıl adı, Sorgulayabileceğiniz [Microsoft Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity). Veya, [Azure AD Graph Explorer'a](https://graphexplorer.cloudapp.net/), Azure AD hesabınızı kullanarak oturum açın.

    2.  Merhaba olduğunda **objectID** , hizmet sorumlusu komutu aşağıdaki hello çalıştırın:

            ```PowerShell
            Add-AzureADServicePrincipalPolicy -Id <ObjectId of hello ServicePrincipal> -RefObjectId <ObjectId of hello Policy>
            ```
        
3. Set hello `IsOrganizationDefault` toofalse bayrak:

    ```PowerShell
    Set-AzureADPolicy -Id <ObjectId of Policy> -DisplayName "ComplexPolicyScenario" -IsOrganizationDefault $false
    ```

4. Yeni bir kuruluş varsayılan ilke oluşturun:

    ```PowerShell
    New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "ComplexPolicyScenarioTwo" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"
    ```

    Şimdi hello özgün ilke bağlantılı tooyour hizmet sorumlusu varsa ve hello yeni ilke, kuruluş varsayılan ilke olarak ayarlanır. Önemli tooremember ilkelerinin uygulandığı tooservice sorumluları kuruluş varsayılan ilke önceliğe sahip olur.

## <a name="cmdlet-reference"></a>Cmdlet başvurusu

### <a name="manage-policies"></a>İlkeleri yönetme

Aşağıdaki cmdlet'leri toomanage ilkeler hello kullanabilirsiniz.

#### <a name="new-azureadpolicy"></a>AzureADPolicy yeni

Yeni bir ilke oluşturur.

```PowerShell
New-AzureADPolicy -Definition <Array of Rules> -DisplayName <Name of Policy> -IsOrganizationDefault <boolean> -Type <Policy Type>
```

| Parametreler | Açıklama | Örnek |
| --- | --- | --- |
| <code>&#8209;Definition</code> |Tüm hello İlkesi'nin kuralları içeren stringified JSON dizisi. | `-Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxInactiveTime":"20:00:00"}}')` |
| <code>&#8209;DisplayName</code> |Hello ilkesi adı dizesi. |`-DisplayName "MyTokenPolicy"` |
| <code>&#8209;IsOrganizationDefault</code> |TRUE ise, hello İlkesi hello kuruluşunuzun varsayılan ilke olarak ayarlar. False ise, hiçbir şey yapmaz. |`-IsOrganizationDefault $true` |
| <code>&#8209;Type</code> |İlke türü. Belirteç yaşam süreleri her zaman "TokenLifetimePolicy." kullan | `-Type "TokenLifetimePolicy"` |
| <code>&#8209;AlternativeIdentifier</code>[İsteğe bağlı] |Hello ilkesi için alternatif bir kimlik ayarlar. |`-AlternativeIdentifier "myAltId"` |

</br></br>

#### <a name="get-azureadpolicy"></a>Get-AzureADPolicy
Tüm Azure AD ilkeleri veya belirtilen ilkesini alır.

```PowerShell
Get-AzureADPolicy
```

| Parametreler | Açıklama | Örnek |
| --- | --- | --- |
| <code>&#8209;Id</code>[İsteğe bağlı] |**ObjectID (ID)** istediğiniz hello ilkesi. |`-Id <ObjectId of Policy>` |

</br></br>

#### <a name="get-azureadpolicyappliedobject"></a>Get-AzureADPolicyAppliedObject
Tüm uygulamaları ve bağlantılı tooa ilkesi olan hizmet asıl adı alır.

```PowerShell
Get-AzureADPolicyAppliedObject -Id <ObjectId of Policy>
```

| Parametreler | Açıklama | Örnek |
| --- | --- | --- |
| <code>&#8209;Id</code> |**ObjectID (ID)** istediğiniz hello ilkesi. |`-Id <ObjectId of Policy>` |

</br></br>

#### <a name="set-azureadpolicy"></a>Set-AzureADPolicy
Mevcut bir ilkenin güncelleştirir.

```PowerShell
Set-AzureADPolicy -Id <ObjectId of Policy> -DisplayName <string>
```

| Parametreler | Açıklama | Örnek |
| --- | --- | --- |
| <code>&#8209;Id</code> |**ObjectID (ID)** istediğiniz hello ilkesi. |`-Id <ObjectId of Policy>` |
| <code>&#8209;DisplayName</code> |Hello ilkesi adı dizesi. |`-DisplayName "MyTokenPolicy"` |
| <code>&#8209;Definition</code>[İsteğe bağlı] |Tüm hello İlkesi'nin kuralları içeren stringified JSON dizisi. |`-Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxInactiveTime":"20:00:00"}}')` |
| <code>&#8209;IsOrganizationDefault</code>[İsteğe bağlı] |TRUE ise, hello İlkesi hello kuruluşunuzun varsayılan ilke olarak ayarlar. False ise, hiçbir şey yapmaz. |`-IsOrganizationDefault $true` |
| <code>&#8209;Type</code>[İsteğe bağlı] |İlke türü. Belirteç yaşam süreleri her zaman "TokenLifetimePolicy." kullan |`-Type "TokenLifetimePolicy"` |
| <code>&#8209;AlternativeIdentifier</code>[İsteğe bağlı] |Hello ilkesi için alternatif bir kimlik ayarlar. |`-AlternativeIdentifier "myAltId"` |

</br></br>

#### <a name="remove-azureadpolicy"></a>Remove-AzureADPolicy
Siler hello İlkesi belirtilmiş.

```PowerShell
 Remove-AzureADPolicy -Id <ObjectId of Policy>
```

| Parametreler | Açıklama | Örnek |
| --- | --- | --- |
| <code>&#8209;Id</code> |**ObjectID (ID)** istediğiniz hello ilkesi. | `-Id <ObjectId of Policy>` |

</br></br>

### <a name="application-policies"></a>Uygulama ilkeleri
Uygulama ilkeleri için cmdlet'leri aşağıdaki hello kullanabilirsiniz.</br></br>

#### <a name="add-azureadapplicationpolicy"></a>Ekleme AzureADApplicationPolicy
Bağlantılar hello İlkesi tooan uygulama belirtilen.

```PowerShell
Add-AzureADApplicationPolicy -Id <ObjectId of Application> -RefObjectId <ObjectId of Policy>
```

| Parametreler | Açıklama | Örnek |
| --- | --- | --- |
| <code>&#8209;Id</code> |**ObjectID (ID)** hello uygulamasının. | `-Id <ObjectId of Application>` |
| <code>&#8209;RefObjectId</code> |**ObjectID** hello ilkesi. | `-RefObjectId <ObjectId of Policy>` |

</br></br>

#### <a name="get-azureadapplicationpolicy"></a>Get-AzureADApplicationPolicy
Atanan tooan uygulama hello ilkesini alır.

```PowerShell
Get-AzureADApplicationPolicy -Id <ObjectId of Application>
```

| Parametreler | Açıklama | Örnek |
| --- | --- | --- |
| <code>&#8209;Id</code> |**ObjectID (ID)** hello uygulamasının. | `-Id <ObjectId of Application>` |

</br></br>

#### <a name="remove-azureadapplicationpolicy"></a>Remove-AzureADApplicationPolicy
Bir ilke bir uygulamadan kaldırır.

```PowerShell
Remove-AzureADApplicationPolicy -Id <ObjectId of Application> -PolicyId <ObjectId of Policy>
```

| Parametreler | Açıklama | Örnek |
| --- | --- | --- |
| <code>&#8209;Id</code> |**ObjectID (ID)** hello uygulamasının. | `-Id <ObjectId of Application>` |
| <code>&#8209;PolicyId</code> |**ObjectID** hello ilkesi. | `-PolicyId <ObjectId of Policy>` |

</br></br>

### <a name="service-principal-policies"></a>Hizmet asıl ilkeleri
Hizmet asıl ilkeleri için cmdlet'leri aşağıdaki hello kullanabilirsiniz.

#### <a name="add-azureadserviceprincipalpolicy"></a>Ekleme AzureADServicePrincipalPolicy
Bağlantılar belirtilen ilke tooa hizmet sorumlusu hello.

```PowerShell
Add-AzureADServicePrincipalPolicy -Id <ObjectId of ServicePrincipal> -RefObjectId <ObjectId of Policy>
```

| Parametreler | Açıklama | Örnek |
| --- | --- | --- |
| <code>&#8209;Id</code> |**ObjectID (ID)** hello uygulamasının. | `-Id <ObjectId of Application>` |
| <code>&#8209;RefObjectId</code> |**ObjectID** hello ilkesi. | `-RefObjectId <ObjectId of Policy>` |

</br></br>

#### <a name="get-azureadserviceprincipalpolicy"></a>Get-AzureADServicePrincipalPolicy
Herhangi bir ilke bağlantılı toohello belirtilen hizmet asıl alır.

```PowerShell
Get-AzureADServicePrincipalPolicy -Id <ObjectId of ServicePrincipal>
```

| Parametreler | Açıklama | Örnek |
| --- | --- | --- |
| <code>&#8209;Id</code> |**ObjectID (ID)** hello uygulamasının. | `-Id <ObjectId of Application>` |

</br></br>

#### <a name="remove-azureadserviceprincipalpolicy"></a>Remove-AzureADServicePrincipalPolicy
Hello İlkesi hello belirtilen hizmet sorumlusu kaldırır.

```PowerShell
Remove-AzureADServicePrincipalPolicy -Id <ObjectId of ServicePrincipal>  -PolicyId <ObjectId of Policy>
```

| Parametreler | Açıklama | Örnek |
| --- | --- | --- |
| <code>&#8209;Id</code> |**ObjectID (ID)** hello uygulamasının. | `-Id <ObjectId of Application>` |
| <code>&#8209;PolicyId</code> |**ObjectID** hello ilkesi. | `-PolicyId <ObjectId of Policy>` |
