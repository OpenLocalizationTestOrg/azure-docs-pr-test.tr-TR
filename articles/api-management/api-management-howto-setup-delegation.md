---
title: "kayıt ve ürün aaaHow toodelegate kullanıcı aboneliği"
description: "Nasıl toodelegate kullanıcı kayıt ve ürün abonelik tooa üçüncü taraf Azure API Management'te öğrenin."
services: api-management
documentationcenter: 
author: antonba
manager: erikre
editor: 
ms.assetid: 8b7ad5ee-a873-4966-a400-7e508bbbe158
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 406648db2d2f37c4dcda466294726d331cc0551b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodelegate-user-registration-and-product-subscription"></a>Nasıl toodelegate kullanıcı kayıt ve ürün aboneliği
Temsilci toouse sağlayan Geliştirici oturum-açma/kaydolma ve abonelik tooproducts olarak işlemek için varolan Web sitenizi toousing hello hello Geliştirici Portalı'nda yerleşik bir işlevi değil. Bu Web sitesi tooown hello kullanıcı verilerinizi sağlar ve özel bir şekilde hello doğrulama bu adımları gerçekleştirin.

## <a name="delegate-signin-up"></a>İçin temsilci seçme Geliştirici oturum açma ve kaydolma
Merhaba API Management Geliştirici Portalı'ndan başlatılan böyle bir istek için giriş noktası hello gibi davranır, sitenizde toocreate özel temsilci endpoint gerekir toodelegate Geliştirici oturum açma ve kaydolma tooyour varolan Web sitesi.

Merhaba son iş akışı şu şekilde olacaktır:

1. Geliştirici hello API Management Geliştirici Portalı hello oturum açma veya kaydolma bağlantısına tıklar
2. Yeniden yönlendirilen toohello temsilci endpoint tarayıcısıdır
3. Temsilci endpoint iade tooor sunar UI soran kullanıcı toosign açma veya kaydolma yönlendirir
4. Başarılıysa hello kullanıcı bunlar başlattığınız yeniden yönlendirilen geri toohello API Management Geliştirici portal sayfasıdır

toobegin, ilk kurulum API Management tooroute temsilci uç noktanızı şimdi ister. Merhaba API Management yayımcı Portalı'nda tıklatın **güvenlik** ve hello ardından **temsilci** sekmesi. Merhaba onay kutusunu tooenable 'Temsilci oturum açma ve kaydolma' tıklayın.

![Temsilci seçme sayfası][api-management-delegation-signin-up]

* Hangi özel temsilci uç noktanızı hello URL'sini ve olması hello girin karar **temsilci uç nokta URL'si** alan. 
* Merhaba içinde **temsilci kimlik doğrulama anahtarı** alan isteği hello doğrulama tooensure için sağlanan imza tooyou gerçekten Azure API Yönetimi'nden gelen kullanılan toocompute olacak bir gizlilik girin. Merhaba tıklayabilirsiniz **oluşturmak** düğmesini toohave API yönetim rastgele oluşturmak bir anahtarı sizin için.

Toocreate hello gereksinim artık **temsilci endpoint**. Tooperform çeşitli eylemleri içerir:

1. Bir istek form aşağıdaki hello alırsınız:
   
   > *http://www.yourwebsite.com/apimdelegation?Operation=SignIn&returnUrl= {kaynak sayfasının URL'sini} & salt = {dize} & SIG = {dize}*
   > 
   > 
   
    Sorgu parametreleri hello oturum açma / kaydolma çalışması için:
   
   * **işlem**: olduğu - yalnızca olabilir temsilci istek türünü tanımlayan **Signın** bu durumda
   * **returnUrl**: hello kullanıcı bir oturum açma veya kaydolma bağlantısına tıklattığınız hello sayfasının URL'sini hello
   * **Salt**: güvenlik karma hesaplama için kullanılan özel bir salt dizesi
   * **SIG**: kendi karşılaştırma tooyour için kullanılan bir hesaplanmış güvenlik karma toobe hesaplanan karma
2. Bu hello istek Azure API Yönetimi'nden (isteğe bağlı, ancak güvenlik için önerilen yüksek oranda) gelen doğrulayın
   
   * Merhaba üzerinde dayalı bir dize HMAC SHA512 karmasını işlem **returnUrl** ve **salt** sorgu parametreleri ([aşağıda sağlanan örnek kod]):
     
     > HMAC (**salt** + '\n' + **returnUrl**)
     > 
     > 
   * Merhaba yukarıda hesaplanan karma toohello hello değerini karşılaştırın **SIG** sorgu parametresi. Merhaba iki karmalar eşleşiyorsa toohello sonraki adımda taşıdığınızda, aksi takdirde hello isteği reddedecek.
3. Sign-ın/oturum-yukarı için bir istek aldığını onaylayın: Merhaba **işlemi** sorgu parametresi çok ayarlanacak "**Signın**".
4. Kullanıcı Arabirimi toosign açma veya kaydolma ile mevcut hello kullanıcı
5. Merhaba kullanıcı kaydolduğunuz ise, toocreate karşılık gelen bir hesap için API Management'te sağlayın. [Bir kullanıcı oluşturmak] hello API Management REST API ile. Bunu yaparken, aynı kullanıcı deponuzda olduğu veya, izlemek tooan kimliği hello kullanıcı kimliği toohello ayarlamak emin olun.
6. Ne zaman hello kullanıcı başarıyla kimlik doğrulaması:
   
   * [bir çoklu oturum açma (SSO) belirteci isteği] hello API Management REST API aracılığıyla
   * returnUrl sorgu parametresi toohello SSO hello API çağrısından yukarıdaki aldığınız URL Ekle:
     
     > Örneğin https://customer.portal.azure-api.net/signin-sso?token&returnUrl=/return/url 
     > 
     > 
   * URL yeniden yönlendirme hello kullanıcı toohello yukarıdaki üretilen

Toplama toohello içinde **Signın** işlemi de gerçekleştirebilirsiniz hesap yönetimi aşağıdaki hello önceki adımları ve işlemleri aşağıdaki hello birini kullanarak.

* **Parola değiştirme**
* **ChangeProfile**
* **CloseAccount**

Hesap yönetimi işlemleri için sorgu parametreleri aşağıdaki hello geçmesi gerekir.

* **işlem**: (parola değiştirme, ChangeProfile veya CloseAccount) için temsilci seçme isteği türünü tanımlar
* **UserId**: hello hesap toomanage hello kullanıcı kimliği
* **Salt**: güvenlik karma hesaplama için kullanılan özel bir salt dizesi
* **SIG**: kendi karşılaştırma tooyour için kullanılan bir hesaplanmış güvenlik karma toobe hesaplanan karma

## <a name="delegate-product-subscription"></a>Ürün aboneliği için temsilci seçme
Ürün aboneliği için temsilci seçme toodelegating kullanıcı oturum açma/yukarı benzer şekilde çalışır. Merhaba son iş akışı aşağıdaki gibi olur:

1. Geliştirici hello API Management Geliştirici Portalı'nda bir ürün seçer ve hello abone ol düğmesini tıklattığında
2. Yeniden yönlendirilen toohello temsilci endpoint tarayıcısıdır
3. Temsilci endpoint gerekli ürün abonelik adımları gerçekleştirir - bu tooyou ve faturalama bilgileri, ek sorular sormak veya yalnızca hello bilgilerini depolamak ve herhangi bir kullanıcı eylemi gerektirmeyen yeniden yönlendirme tooanother sayfa toorequest gerektirdiği

Merhaba üzerinde tooenable hello işlevselliği **temsilci** sayfasında **temsilci ürün aboneliği**.

Ardından hello temsilci endpoint hello aşağıdaki eylemleri gerçekleştirir emin olun:

1. Bir istek form aşağıdaki hello alırsınız:
   
   > *{işlemi} http://www.yourwebsite.com/apimdelegation?Operation= & ProductID {ürün toosubscribe} = & UserID = {isteği yapan kullanıcı} & salt = {dize} & SIG = {dize}*
   > 
   > 
   
    Sorgu parametreleri hello ürün abonelik çalışması için:
   
   * **işlem**: olmasından temsilci istek türünü tanımlar. Ürün abonelik için istekleri hello geçerli seçenekler şunlardır:
     * "Abone": ürünle birlikte verilen bir istek toosubscribe hello kullanıcı tooa sağlanan kimliği (aşağıya bakın)
     * "Aboneliği": İstek toounsubscribe bir ürün kullanıcıdan
     * "Yenile": requst toorenew (örneğin erecek) bir abonelik
   * **ProductID**: hello hello ürün hello kullanıcının Kimliğini istenen toosubscribe için
   * **UserId**: kendisi için hello istek yapıldığında hello kullanıcının Kimliğini hello
   * **Salt**: güvenlik karma hesaplama için kullanılan özel bir salt dizesi
   * **SIG**: kendi karşılaştırma tooyour için kullanılan bir hesaplanmış güvenlik karma toobe hesaplanan karma
2. Bu hello istek Azure API Yönetimi'nden (isteğe bağlı, ancak güvenlik için önerilen yüksek oranda) gelen doğrulayın
   
   * HMAC SHA512 üzerinde hello dayalı bir dizenin işlem **ProductID**, **UserID** ve **salt** sorgu parametreleri:
     
     > HMAC (**salt** + '\n' + **ProductID** + '\n' + **UserID**)
     > 
     > 
   * Merhaba yukarıda hesaplanan karma toohello hello değerini karşılaştırın **SIG** sorgu parametresi. Merhaba iki karmalar eşleşiyorsa toohello sonraki adımda taşıdığınızda, aksi takdirde hello isteği reddedecek.
3. İçinde istenen işlemi hello türüne göre herhangi bir ürün Abonelik işlem gerçekleştirme **işlemi** -örn: faturalandırma, ayrıntılı sorular, vb..
4. Merhaba kullanıcı toohello ürün, tarafında başarıyla abone üzerinde hello kullanıcı toohello API Management ürün abone [ürün abonelik için REST API çağırma hello].

## <a name="delegate-example-code"></a> Örnek kod
Bu kod örnekleri Göster nasıl tootake hello *temsilci doğrulama anahtarı*hello yayımcı portalının temsilci ekranında hello ayarlayın, toocreate sonra olan bir HMAC kullanılan hello hello geçerliliğini kanıtlayan toovalidate hello imza geçirilen returnUrl. Merhaba hello ProductID ve küçük değişiklik kullanıcı kimliği için aynı kodu çalışır.

**C# kod toogenerate karmasını returnUrl**

```c#
using System.Security.Cryptography;

string key = "delegation validation key";
string returnUrl = "returnUrl query parameter";
string salt = "salt query parameter";
string signature;
using (var encoder = new HMACSHA512(Convert.FromBase64String(key)))
{
    signature = Convert.ToBase64String(encoder.ComputeHash(Encoding.UTF8.GetBytes(salt + "\n" + returnUrl)));
    // change too(salt + "\n" + productId + "\n" + userId) when delegating product subscription
    // compare signature toosig query parameter
}
```

**NodeJS kod toogenerate returnUrl karmasını**

```
var crypto = require('crypto');

var key = 'delegation validation key'; 
var returnUrl = 'returnUrl query parameter';
var salt = 'salt query parameter';

var hmac = crypto.createHmac('sha512', new Buffer(key, 'base64'));
var digest = hmac.update(salt + '\n' + returnUrl).digest();
// change too(salt + "\n" + productId + "\n" + userId) when delegating product subscription
// compare signature toosig query parameter

var signature = digest.toString('base64');
```

## <a name="next-steps"></a>Sonraki adımlar
Temsilci seçme hakkında daha fazla bilgi için video aşağıdaki hello bakın.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Delegating-User-Authentication-and-Product-Subscription-to-a-3rd-Party-Site/player]
> 
> 

[Delegating developer sign-in and sign-up]: #delegate-signin-up
[Delegating product subscription]: #delegate-product-subscription
[bir çoklu oturum açma (SSO) belirteci isteği]: http://go.microsoft.com/fwlink/?LinkId=507409
[bir kullanıcı oluşturun]: http://go.microsoft.com/fwlink/?LinkId=507655#CreateUser
[ürün abonelik için REST API çağırma hello]: http://go.microsoft.com/fwlink/?LinkId=507655#SSO
[Next steps]: #next-steps
[aşağıda sağlanan örnek kod]: #delegate-example-code

[api-management-delegation-signin-up]: ./media/api-management-howto-setup-delegation/api-management-delegation-signin-up.png 
