---
title: "aaaWhat hello Azure AD v2.0 uç farklı mı çalışıyor? | Microsoft Belgeleri"
description: "Merhaba özgün Azure AD ve hello v2.0 uç noktaları arasında bir karşılaştırma."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 5060da46-b091-4e25-9fa8-af4ae4359b6c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: e7ed196f9053fc21db799cd6bc513ba5c2b92885
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="whats-different-about-hello-v20-endpoint"></a>Merhaba v2.0 uç hakkında farklı nedir?
Azure Active Directory ile tanıdık veya uygulamaları hello son olarak Azure AD ile tümleşik değil beklediğiniz hello v2.0 uç noktası bazı farklılıklar olabilir.  Bu belge, anlamak için bu farkları çıkışı çağırır.

> [!NOTE]
> Tüm Azure Active Directory senaryolarını ve özelliklerini hello v2.0 uç noktası tarafından desteklenir.  Merhaba v2.0 uç noktası, kullanmanız gereken varsa toodetermine okuyun hakkında [v2.0 sınırlamaları](active-directory-v2-limitations.md).
>

## <a name="microsoft-accounts-and-azure-ad-accounts"></a>Microsoft ve Azure AD hesapları
Merhaba v2.0 uç geliştiriciler oturum açma tek kimlik doğrulama uç noktası kullanarak, Microsoft Accounts ve Azure AD hesaplarının kabul toowrite uygulamaları izin verir.  Uygulamanızı tamamen hesap belirsiz özelliği toowrite hello bu verir; kullanmayan kullanıcı işaretlerini ile Merhaba hesabının hello türünde olabilir.  Elbette, *yapabilirsiniz* uygulamanızı belirli bir oturumda kullanılan hesap hello türü farkında olun, ancak zorunda değilsiniz.

Örneğin, uygulamanızın hello çağırırsa [Microsoft Graph](https://graph.microsoft.io), kullanılabilir tooenterprise kullanıcılar, SharePoint sitelerinde veya dizin verileri gibi bazı ek işlevler ve veri olacaktır.  Ancak birçok eylemler gibi [bir kullanıcının posta okuma](https://graph.microsoft.io/docs/api-reference/v1.0/resources/message), hello kodu tam olarak yazılabilir aynı Microsoft Accounts ve Azure AD hesapları için hello.  

Uygulamanızı Microsoft Accounts ve Azure AD hesapları ile tümleştirme şimdi bir basit bir işlemdir.  Uç noktaları, tek bir kitaplık ve bir tek uygulama kayıt toogain erişim tooboth hello müşteri ve kuruluş dünyaları tek bir dizi kullanabilirsiniz.  toolearn hakkında daha fazla bilgi v2.0 uç Merhaba, kullanıma [genel bakış hello](active-directory-appmodel-v2-overview.md).

## <a name="new-app-registration-portal"></a>Yeni uygulama kayıt portalı
tooregister hello v2.0 uç noktası ile çalışan bir uygulama, yeni bir uygulama kayıt portalı kullanmanız gerekir: [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList).  Bu burada edinebilirsiniz bir uygulama kimliği hello portalıdır uygulamanızın oturum açma sayfası ve daha fazlasını hello görünümünü özelleştirin.  Tüm tooaccess hello portal gereken gücü Microsoft hesabı - kişisel veya iş/Okul hesap budur.

## <a name="one-app-id-for-all-platforms"></a>Tüm platformlar için bir uygulama kimliği
Azure Active Directory kullandıysanız, büyük olasılıkla birkaç farklı uygulamaları tek bir proje için kaydınız.  Örneğin, bir Web sitesi ve bir iOS uygulaması oluşturulduysa, tooregister vardı bunları ayrı olarak, iki farklı uygulama kimlikleri kullanma. Hello Azure AD uygulama kayıt portalı kaydı sırasında Bu ayrım, toomake zorla:

![Eski uygulama kaydı kullanıcı Arabirimi](../../media/active-directory-v2-flows/old_app_registration.PNG)

Bir Web sitesi ve web API'si arka uç olsaydı, benzer şekilde, her ayrı bir uygulama olarak Azure AD içinde kaydettiğiniz.  Veya bir iOS uygulaması ve bir Android uygulaması varsa, aynı zamanda iki farklı uygulamalar kaydettiğiniz.  Her bir uygulama bileşeninin kaydetme neden toosome beklenmeyen davranışları geliştiriciler ve müşterileri için:

* Her müşterinin hello Azure Active Directory kiracısı içinde ayrı bir uygulama olarak her bileşenin görüldü.
* Bir kiracı yönetici erişimi yönetmek veya bir uygulamayı silmek için tooapply İlkesi çalışırken toodo olurdu hello uygulamasının her bileşen için bunu.
* Müşteriler tooan uygulama rıza, her bileşenin farklı bir uygulama olarak hello onay ekranında görüntülenir.

Merhaba v2.0 uç noktası ile artık projenizin tüm bileşenleri tek uygulama kaydı kaydetmek ve tek bir uygulama kimliği projeniz için kullanın.  Birkaç "platformlar" tooa her proje ekleyin ve eklediğiniz her platform için hello uygun veriler sağlar.  Elbette, gereksinimlerinize bağlı olarak ister, ancak yalnızca bir uygulama kimliği için hello çoğu kez, gerekli olması gereken şekilde sayıda uygulamaları oluşturabilirsiniz.

Bizim AIM bu Basitleştirilmiş tooa uygulama yönetimi ve geliştirme deneyimi sağlama, üzerinde çalışabilir tek bir proje, fazla birleştirilmiş bir görünümünü oluşturmak olmasıdır.

## <a name="scopes-not-resources"></a>Kapsamları, kaynakları değil
Azure Active Directory'de bir uygulama olarak davranabilir bir **kaynak**, veya bir alıcının belirteçleri.  Bir kaynak bir dizi tanımlayabilirsiniz **kapsamları** veya **oAuth2Permissions** anladığı, istemci uygulamaları toorequest belirteçleri toothat kaynak belirli bir dizi kapsamlar için izin verme.  Örnek bir kaynak olarak Hello Azure AD Graph API göz önünde bulundurun:

* Kaynak tanımlayıcısı veya `AppID URI`:`https://graph.windows.net/`
* Kapsamları veya `OAuth2Permissions`: `Directory.Read`, `Directory.Write`vb..  

Tüm bu tutar hello hello v2.0 uç noktası için true.  Bir uygulamayı hala davranabilir kaynak olarak kapsamları tanımlamak ve bir URI tarafından tanımlanan.  İstemci uygulamaları hala erişim toothose kapsamları isteyebilir.  Ancak, bir istemci bu izinleri ister hello şekilde değiştirdi.  Hello geçmiş, bir OAuth 2.0 yetkilendirme isteği tooAzure AD gibi attıktan:

```
GET https://login.microsoftonline.com/common/oauth2/authorize?
client_id=2d4d11a2-f814-46a7-890a-274a72a7309e
&resource=https%3A%2F%2Fgraph.windows.net%2F
...
```

Burada hello **kaynak** parametresi belirtilen yetkilendirme için hangi kaynak hello istemci uygulamanın istiyor.  Azure AD hello Azure Portal'ın statik yapılandırmasını temel alarak ve verilen belirteçler uygun şekilde hello uygulama tarafından gerekli hello izinler hesaplanır.  Şimdi, hello aynı OAuth 2.0 yetkilendirme isteği görülüyor:

```
GET https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=2d4d11a2-f814-46a7-890a-274a72a7309e
&scope=https%3A%2F%2Fgraph.windows.net%2Fdirectory.read%20https%3A%2F%2Fgraph.windows.net%2Fdirectory.write
...
```

Burada hello **kapsam** parametre, yetkilendirme için hangi kaynak ve izinleri hello uygulama isteyen belirtir. Merhaba, kaynak hala hello çok istekte - bunu yalnızca her hello kapsam parametresi hello değerlerini ileride olan istenen.  Bu şekilde Hello kapsam parametresi kullanılarak hello v2.0 uç noktası toobe hello OAuth 2.0 belirtimi daha uyumlu sağlar ve daha yakından ortak endüstri yöntemlerle hizalar.  Ayrıca uygulamalar tooperform sağlar [artımlı izin](#incremental-and-dynamic-consent), hello sonraki bölümde açıklanmaktadır.

## <a name="incremental-and-dynamic-consent"></a>Artımlı ve dinamik onayı
Uygulamaları Azure AD daha önce gerekli toospecify gerekli OAuth 2.0 izinlerini hello Azure Portal, uygulama oluşturma zamanında kayıtlı:

![İzinleri kayıt kullanıcı Arabirimi](../../media/active-directory-v2-flows/app_reg_permissions.PNG)

gerekli bir uygulama yapılandırıldı hello izinleri **statik olarak**.  Bu hello Azure Portal hello uygulama tooexist yapılandırılmasına izin ve iyi ve basit hello kod tutulan olsa da, geliştiriciler için bazı sorunları gösterir:

* Bir uygulama tooknow sahip hiç gerek uygulama oluşturma zamanında hello izinleri.  Zaman içinde izinlerini eklemek zor bir işlem.
* Bir uygulama tooknow sahip şimdiye kadar erişim süresi öncesinde hello kaynakların tümünü.  Rastgele bir kaynak sayısı erişebilir zor toocreate uygulamalar oluştu.
* Bir uygulama toorequest hiç hello kullanıcının ilk oturum açma sırasında gerekir tüm hello izinleri vardı.  Bazı durumlarda bu tooa çok uzun ilk oturum açma hello uygulamanın erişimi onaylama gelen son kullanıcılar önermez izinlerin listesi gerektiriyordu.

Merhaba v2.0 uç noktası ile Merhaba izinlerini belirtebilirsiniz uygulama gereksinimlerinizi **dinamik olarak**, uygulamanızın normal kullanım sırasında çalışma zamanında.  toodo, hello kapsamları uygulama gereksinimlerinizi verilen herhangi bir noktada zamanında hello dahil ederek belirtebilirsiniz `scope` bir yetkilendirme isteği parametresinin:

```
GET https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=2d4d11a2-f814-46a7-890a-274a72a7309e
&scope=https%3A%2F%2Fgraph.windows.net%2Fdirectory.read%20https%3A%2F%2Fgraph.windows.net%2Fdirectory.write
...
```

Yukarıdaki Merhaba, bir Azure AD kullanıcının dizin verilerini yanı sıra yazma veri tootheir dizini hello uygulama tooread için izin ister.  Merhaba kullanıcı hello geçmiş toothose izin verdiği varsa bu belirli uygulama için bunlar yalnızca kimlik bilgilerini girer ve hello uygulamaya imzalanmış.  Merhaba kullanıcı bu izinlerin tooany seçtiği değil, hello v2.0 uç hello kullanıcı onayı toothose izinlerini isteyin.  Daha fazla toolearn, alabileceğiniz üzerinde [izinleri, onay ve kapsamları](active-directory-v2-scopes.md).

Bir uygulamanın dinamik olarak hello aracılığıyla toorequest izinleri verme `scope` parametresi, kullanıcı deneyimi üzerinde tam denetim verir.  İsterseniz, onayınızı deneyimi ve bir başlangıç yetkilendirme isteği tüm izinleri isteyin toofrontload seçebilirsiniz.  Veya, uygulamanız çok sayıda izinleri gerektiriyorsa, bunlar toouse, uygulamanızın belirli özellikleri zamanla denemesi gibi toogather bu izinleri hello kullanıcıdan artımlı olarak, seçebilirsiniz.

## <a name="well-known-scopes"></a>İyi bilinen kapsamları
#### <a name="offline-access"></a>Çevrimdışı erişim
Merhaba v2.0 uç kullanarak uygulamaları gerektirebilir yeni bir iyi bilinen izin hello kullanımını uygulamaları için - hello `offline_access` kapsam.  Bir kullanıcının hello adına tooaccess kaynaklara süresi, uzun süren bir süre için bile hello kullanıcı hello uygulama etkin olarak kullanan değil ihtiyaç duydukları tüm uygulamalar toorequest bu izni gerekir.  Merhaba `offline_access` kapsam olarak iletişimleri "Verilerinizi çevrimdışı erişim" onay toohello kullanıcı görünür hello kullanıcı için kabul etmesi gerekir.  İstekte bulunan hello `offline_access` izni web uygulama tooreceive OAuth 2.0 refresh_tokens hello v2.0 uç noktasından etkinleştirir.  Refresh_tokens uzun süreli ve uzun süreler erişim için yeni OAuth 2.0 access_tokens değiştirilebilir.  

Uygulamanızı hello istemezse `offline_access` kapsam refresh_tokens almaz.  Bu bir authorization_code hello OAuth 2.0 yetkilendirme kodu akışı içinde kullanmak, yalnızca geri bir access_token hello alacağınız anlamına gelir `/token` uç noktası.  Bu access_token saati (genellikle bir saat) kısa bir süre için geçerli kalır, ancak sonunda dolacaktır.  Bu noktada, zaman içindeki tooredirect hello kullanıcı toohello uygulamanıza gerekecek `/authorize` uç nokta tooretrieve yeni authorization_code.  Bu yeniden yönlendirme sırasında hello kullanıcı olabilir veya düzgün tooenter kimlik bilgilerini yeniden gerekir veya uygulamanın hello hello türüne bağlı olarak toopermissions yeniden onayı.

Merhaba OAuth 2.0, refresh_tokens ve access_tokens, kullanıma hakkında daha fazla toolearn [v2.0 protokol başvurusu](active-directory-v2-protocols.md).

#### <a name="openid-profile-and-email"></a>Openıd, profili ve e-posta
Geçmişte, hello en temel Openıd Connect oturum açma akışını Azure Active Directory ile bol miktarda hello elde edilen id_token hello kullanıcı hakkında bilgi sağlar.  bir id_token Hello Taleplerde hello kullanıcının adı, tercih edilen kullanıcı adı, e-posta adresi, nesne kimliği ve daha fazlasını içerebilir.

Bu hello hello bilgi kısıtlama artık duyuyoruz `openid` kapsam uygulama erişiminizi ortaya koymaktadır.  Hello 'openıd' kapsamı yalnızca uygulama toosign hello kullanıcınız izin ve hello kullanıcı için uygulamaya özgü tanımlayıcıyı alır.  Uygulamanızda hello kullanıcı hakkında tooobtain kişisel bilgileri (PII) istiyorsanız, uygulamanızı toorequest hello kullanıcıdan ek izinler gerekir.  İki yeni kapsamlar – hello sunuyoruz `email` ve `profile` toodo şekilde izin kapsamları –.

Merhaba `email` kapsamı çok basit –, uygulama erişim toohello kullanıcının birincil e-posta adresi hello aracılığıyla verir `email` hello id_token talep.  Merhaba `profile` nesne kimliği kapsam ortaya koymaktadır, uygulama erişim tooall hello kullanıcı – kendi adı, tercih edilen kullanıcı adı, hakkındaki diğer temel bilgileri ve benzeri.

Toocode bu sayede uygulamanız açığa en az bir şekilde – yalnızca uygulamanızı işini toodo gerektirdiği bilgiler hello kümesi için hello kullanıcı sorabilirsiniz.  Bu kapsamları hakkında daha fazla bilgi için çok başvuran[hello v2.0 kapsam başvurusu](active-directory-v2-scopes.md).

## <a name="token-claims"></a>Belirteç talep
Merhaba v2.0 uç noktası tarafından yayınlanan belirteçleri Hello Taleplerde hello Azure AD genel olarak kullanılabilir uç noktaları tarafından verilen aynı tootokens olmaz - toohello yeni hizmet geçirme uygulamalar belirli bir talep id_tokens veya access_tokens bulunacağı varsayımında bulunmamalıdır. toolearn hello belirli talepler v2.0 belirteçlerinde yayınlaması hakkında bkz hello [v2.0 belirteç başvurusu](active-directory-v2-tokens.md).

## <a name="limitations"></a>Sınırlamalar
Merhaba v2.0 nokta kullanılırken farkında birkaç kısıtlamaları toobe vardır.  Lütfen toohello bakın [v2.0 sınırlamaları belge](active-directory-v2-limitations.md) herhangi biri bu kısıtlamalar tooyour belirli senaryoları geçerliyse toosee.
