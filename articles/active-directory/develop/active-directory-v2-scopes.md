---
title: "Active Directory aaaAzure v2.0 kapsamları, izinler ve onay | Microsoft Docs"
description: "Hello Azure AD v2.0 uç noktası, kapsamları, izinler ve onay dahil olmak üzere yetkilendirme açıklaması."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 8f98cbf0-a71d-4e34-babf-e644ad9ff423
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 5721d368c435868bfb4ae91cff7fbb9bc4a79b66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="scopes-permissions-and-consent-in-hello-azure-active-directory-v20-endpoint"></a>Kapsam, izinleri ve hello Azure Active Directory v2.0 uç onay
Azure Active Directory (Azure AD) ile tümleştirme uygulamalarını kullanıcılara bir uygulama verilerini nasıl erişebileceğinizi üzerinde denetim sağlar bir yetkilendirme modelini izler. Hello v2.0 hello yetkilendirme modelini uyarlamasını güncelleştirilen ve bir uygulamayı Azure AD ile nasıl etkileşim kurmalıdır değiştirir. Bu makalede kapsamları, izinler ve onay dahil olmak üzere bu yetkilendirme modelin hello temel kavramları kapsar.

> [!NOTE]
> Merhaba v2.0 uç tüm Azure Active Directory senaryolarını ve özelliklerini desteklemez. mı hello v2.0 uç kullanılacağını toodetermine okuma hakkında [v2.0 sınırlamaları](active-directory-v2-limitations.md).
>
>

## <a name="scopes-and-permissions"></a>Kapsamlar ve izinleri
Azure AD uygulayan hello [OAuth 2.0](active-directory-v2-protocols.md) Yetkilendirme Protokolü. OAuth 2.0 üzerinden bir üçüncü taraf uygulama bir kullanıcı adına web barındırılan kaynaklara erişebilir bir yöntemdir. Azure AD ile tümleşir web barındırılan kaynak bir kaynak tanımlayıcısı vardır veya *uygulama kimliği URI'si*. Örneğin, Microsoft'un web barındırılan kaynaklar bazıları şunlardır:

* Office 365 birleşik posta API Hello:`https://outlook.office.com`
* Azure AD Graph API Hello:`https://graph.windows.net`
* Microsoft Graph:`https://graph.microsoft.com`

Merhaba aynı Azure AD ile tümleşik tüm üçüncü taraf kaynaklar için geçerlidir. Bu kaynaklardan herhangi birini daha küçük parçalara bu kaynağın kullanılan toodivide hello işlev olabilir izinleri de tanımlayabilirsiniz. Örneğin, [Microsoft Graph](https://graph.microsoft.io) görevleri, diğerlerinin yanı sıra aşağıdaki izinleri toodo hello tanımlanır:

* Kullanıcının Takvim okuma
* Yazma tooa kullanıcının Takvim
* Kullanıcı olarak posta gönderme

Bu tür izin tanımlayarak hello kaynak verilerini ve nasıl hello veri açığa hassas denetime sahiptir. Bir üçüncü taraf uygulaması bu izinleri bir uygulama kullanıcıdan isteyebilir. Merhaba uygulama hello kullanıcının adına işlem yapabileceği önce hello uygulama kullanıcı hello izinleri onaylamanız gerekir. Daha küçük izin kümeleri Hello kaynağın işlevsellik Öbekleme tarafından üçüncü taraf uygulamalar tooperform işlevlerine gereksinim yerleşik toorequest yalnızca hello özel izinler olabilir. Uygulama kullanıcıların tam olarak bir uygulama verilerini nasıl kullanılacağını bilmeniz ve bu hello uygulama ile kötü amaçlı çalışmıyorsa doğrulayabilirse olabilir.

Azure AD'de ve OAuth, izinleri bu tür çağrılır *kapsamları*. Bazen başvurulan tooas oldukları *oAuth2Permissions*. Bir kapsam Azure AD'de bir dize değeri olarak temsil edilir. Merhaba Microsoft Graph örnekle devam edersek, her izin hello kapsam değeri şudur:

* Kullanıcının takvim kullanarak okuyun`Calendar.Read`
* Kullanarak tooa kullanıcının Takvim yazma`Mail.ReadWrite`
* Kullanarak bir kullanıcı tarafından olarak posta gönderme`Mail.Send`

Uygulama istekleri toohello v2.0 uç hello kapsamları belirterek bu izinleri isteyebilir.

## <a name="openid-connect-scopes"></a>Openıd Connect kapsamları
Openıd Connect Hello v2.0 uygulaması tooa belirli kaynak uygulamayın birkaç iyi tanımlanmış kapsamları sahiptir: `openid`, `email`, `profile`, ve `offline_access`.

### <a name="openid"></a>openıd
Bir uygulama oturum açma kullanarak gerçekleştirirse [Openıd Connect](active-directory-v2-protocols.md), hello istemelidir `openid` kapsam. Merhaba `openid` "oturum" izni hello gibi sayfa onay ve hello kişisel Microsoft hesabı "Profilinizi görüntüleyin ve tooapps ve Microsoft hesabınızı kullanarak hizmetlere bağlanma" izni hello gibi sayfa onayı hello iş hesabındaki kapsam gösterir. Bu izne sahip bir uygulama hello hello biçiminde hello kullanıcı için benzersiz bir tanımlayıcı alabilir `sub` talep. Ayrıca hello uygulama erişim toohello kullanıcı bilgisi bitiş noktası da sağlar. Merhaba `openid` kapsamı, bir uygulamanın farklı bileşenleri arasındaki kullanılan toosecure HTTP çağrıları olabilen hello v2.0 belirteç uç noktası tooacquire kimliği belirteçleri en kullanılabilir.

### <a name="email"></a>E-posta
Merhaba `email` kapsam ile Merhaba kullanılabilir `openid` kapsam ve herhangi diğer. Merhaba hello biçiminde hello uygulama erişim toohello kullanıcının birincil e-posta adresini verir `email` talep. Merhaba `email` yalnızca bir e-posta adresi her zaman hello durumda olmayan hello kullanıcı hesabı ile ilişkili ise talep bir belirteç içine eklenmiştir. Hello kullanıyorsa, `email` kapsamı, uygulamanızı olmalıdır hangi hello durumda toohandle hazırlanmış `email` talep hello belirteçte mevcut değil.

### <a name="profile"></a>Profili
Merhaba `profile` kapsam ile Merhaba kullanılabilir `openid` kapsam ve herhangi diğer. Merhaba uygulama erişim tooa önemli miktarda hello kullanıcı hakkında bilgi sağlar. erişebildiğinizi hello bilgi içerir, ancak hello kullanıcının verilen adı, Soyadı, tercih edilen kullanıcı adı ve kimliği nesne için sınırlı değildir Merhaba hello profil hello id_tokens parametresinde kullanılabilir talepler belirli bir kullanıcı için tam bir listesi için bkz: [v2.0 belirteçler başvuru](active-directory-v2-tokens.md).

### <a name="offlineaccess"></a>offline_access
Merhaba [ `offline_access` kapsam](http://openid.net/specs/openid-connect-core-1_0.html#OfflineAccess) uygulama erişim tooresources hello kullanıcı adına uzun bir süre sağlar. Merhaba iş hesabı onay sayfasında, bu kapsamı "dilediğiniz zaman, veri erişim" izni hello gibi görünür. Merhaba kişisel Microsoft hesabı onay sayfasında, "bilgilerinize dilediğiniz zaman erişin" izni hello gibi görünür. Ne zaman bir kullanıcı onaylarsa hello `offline_access` kapsamı, uygulamanızı hello v2.0 belirteç uç noktasından yenileme belirteçleri alabilir. Yenileme belirteçleri uzun süreli. Eskiler süresi dolduğundan, uygulamanızın yeni erişim belirteçleri elde edebilirsiniz.

Uygulamanızı hello istemezse `offline_access` kapsamı, yenileme belirteçleri almazsınız. Merhaba yetkilendirme kodunda kullanmak olduğunda bunun anlamı [OAuth 2.0 yetkilendirme kodu akışını](active-directory-v2-protocols.md), yalnızca bir erişim belirteci hello alırsınız `/token` uç noktası. Merhaba erişim belirteci kısa bir süre için geçerli değil. Merhaba erişim belirteci, genellikle bir saat içinde süresi dolar. Bu noktada, uygulamanızın tooredirect hello kullanıcı toohello gerektiğini `/authorize` uç nokta tooget yeni bir yetkilendirme kodu. Uygulama, türünü hello bağlı olarak bu yeniden yönlendirme sırasında hello kullanıcı tooenter kimlik bilgilerini yeniden veya ihtiyacınız olabilir yeniden toopermissions onay vermiş olursunuz.

Merhaba nasıl tooget ve kullanım yenileme belirteçlerini hakkında daha fazla bilgi için bkz: [v2.0 protokol başvurusu](active-directory-v2-protocols.md).

## <a name="requesting-individual-user-consent"></a>Tek tek kullanıcı izni isteniyor
İçinde bir [Openıd Connect veya OAuth 2.0](active-directory-v2-protocols.md) yetkilendirme isteği, bir uygulama gerekiyor hello kullanarak hello izinleri isteyebileceği `scope` sorgu parametresi. Örneğin, bir kullanıcı tooan uygulamada oturum açtığında, hello uygulama (okunabilirliği için eklenen satır sonuyla) aşağıdaki örneğine hello gibi bir isteği gönderir:

```
GET https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=code
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&response_mode=query
&scope=
https%3A%2F%2Fgraph.microsoft.com%2Fcalendar.read%20
https%3A%2F%2Fgraph.microsoft.com%2Fmail.send
&state=12345
```

Merhaba `scope` parametredir boşlukla ayrılmış bir liste uygulama hello kapsamların istiyor. Her kapsam hello kapsam değeri toohello kaynağın tanımlayıcı (Merhaba uygulama kimliği URI'si) eklenerek belirtilir. Merhaba isteği örnekte hello uygulamanın hello kullanıcı olarak izni tooread hello kullanıcının takvim ve posta gönderme gerekir.

Merhaba kullanıcı kimlik bilgilerini girdikten sonra hello v2.0 uç noktası için eşleşen bir kayıt denetler *kullanıcı izni*. Merhaba kullanıcı olmayan seçtiği varsa hello tooany hello v2.0 uç hello kullanıcı toogrant ister hello geçmiş, izinler istenen hello istenen izinleri.

![İş hesabı onayı](../../media/active-directory-v2-flows/work_account_consent.png)

Hello kullanıcı hello izni onayladığında, böylece hello kullanıcının tooconsent yeniden sonraki hesap oturum açma işlemlerini üzerinde yoksa hello izin kaydedilir.

## <a name="requesting-consent-for-an-entire-tenant"></a>Tüm Kiracı onay isteme
Genellikle, bir kuruluşun bir lisans ya da bir uygulama için abonelik satın aldığında hello kuruluş toofully sağlama hello uygulama çalışanlarının için istemektedir. Bu işlemin bir parçası olarak, bir yönetici herhangi bir personel adına hello uygulama tooact izin verebilirsiniz. Hello Yöneticisi hello tüm Kiracı izin verirse hello kuruluşunuzun çalışanları Merhaba uygulaması için bir onay sayfasına görmezsiniz.

Uygulamanızı bir kiracıdaki tüm kullanıcılar için toorequest izin hello yönetici onayı uç noktası kullanabilirsiniz.

## <a name="admin-restricted-scopes"></a>Yönetici kısıtlanmış kapsamları
Bazı yüksek ayrıcalıklı izinlere hello Microsoft ekosistemindeki çok ayarlanabilir*yönetici kısıtlanmış*. Aşağıdaki izinleri hello kapsamları bu tür örnekleri:

* Kullanarak bir kuruluşun dizin verilerini okuma`Directory.Read`
* Kullanarak verileri tooan kuruluşunuzun dizininde yazma`Directory.ReadWrite`
* Bir kuruluşun Directory'de güvenlik gruplarını kullanarak okuyun`Groups.Read.All`

Bir tüketici kullanıcı bir uygulama erişim toothis tür veri verebilir rağmen kuruluş kullanıcılarının aynı hassas şirket verilerinin ayarlamak erişim toohello verme kısıtlanır. Uygulamanızı bir kuruluş kullanıcıdan bu izinlere erişim tooone isterse hello kullanıcı bunlar yetkili tooconsent tooyour uygulamanın izinleri olmayan bildiren bir hata iletisi alır.

Uygulamanızı tooadmin kısıtlı erişim kapsamları kuruluşlarda gerektiriyorsa, bunları bir şirket yöneticisinden doğrudan da sonraki bölümde açıklandığı hello yönetici onayı uç noktasını kullanarak isteğinde.

Yönetici uç noktası bu izinleri hello Yöneticisi aracılığıyla izin veriyorsa hello Kiracı tüm kullanıcılar için izin verilir.

## <a name="using-hello-admin-consent-endpoint"></a>Merhaba yönetici onayı uç noktası kullanma
Bu adımları izlerseniz, uygulamanızı yönetici kısıtlanmış kapsamları dahil olmak üzere, bir kiracıdaki tüm kullanıcılar için izinler toplayabilirsiniz. toosee hello adımları uygulayan bir kod örneği görmek hello [yönetici kısıtlanmış kapsamları örnek](https://github.com/Azure-Samples/active-directory-dotnet-admin-restricted-scopes-v2).

### <a name="request-hello-permissions-in-hello-app-registration-portal"></a>Merhaba uygulama kayıt Portalı'nda Hello izinleri iste
1. Merhaba tooyour uygulamada Git [uygulama kayıt portalı](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), veya [bir uygulama oluşturmak](active-directory-v2-app-registration.md) yapmadıysanız.
2. Merhaba bulun **Microsoft Graph izinleri** bölümünde ve ardından uygulamanızı gerektirir hello izinleri ekleyin.
3. Emin olun **kaydetmek** hello uygulama kaydı.

### <a name="recommended-sign-hello-user-in-tooyour-app"></a>Önerilir: Tooyour uygulamasında oturum hello kullanıcı
Genellikle, bir uygulama oluşturduğunuzda hello yönetici onayı uç noktası kullanan, sayfa veya hangi hello yönetici hello uygulamanın izinleri onaylayabilirsiniz görünüm hello uygulamanın gerekir. Merhaba uygulamanın ayarları veya parçası ayrılmış "akış Bağlan" olabilir, bu sayfayı hello uygulamanın kaydolma akışının parçası olabilir. Çoğu durumda, hello uygulama tooshow için bu "yalnızca bir kullanıcı bir iş veya Okul Microsoft hesabı oturum imzaladığı sonra bağlantı görünümü" mantıklıdır.

Merhaba kullanıcı tooyour uygulamasında oturum açtığınızda, hello kuruluş tanımlayabilirsiniz toowhich hello Yöneticisi ait tooapprove hello gerekli izinleri isteyen önce. Kesinlikle gerekli olmasa da, kuruluş, kullanıcılarınızın daha sezgisel bir deneyim oluşturmanıza yardımcı olur. uygulamasında, izleme toosign hello kullanıcı bizim [v2.0 protokol öğreticileri](active-directory-v2-protocols.md).

### <a name="request-hello-permissions-from-a-directory-admin"></a>Bir dizin yöneticisinden gelen isteği hello izinleri
Kuruluşunuzun yöneticisine hazır toorequest izinlerinin olduğunuzda hello kullanıcı toohello v2.0 yönlendirebilirsiniz *yönetici onayı uç noktası*.

```
// Line breaks are for legibility only.

GET https://login.microsoftonline.com/{tenant}/adminconsent?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&state=12345
&redirect_uri=http://localhost/myapp/permissions
```

```
// Pro tip: Try pasting hello below request in a browser!
```

```
https://login.microsoftonline.com/common/adminconsent?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&state=12345&redirect_uri=http://localhost/myapp/permissions
```

| Parametre | Koşul | Açıklama |
| --- | --- | --- |
| Kiracı |Gerekli |toorequest izni istediğiniz hello directory kiracısı. GUID veya kolay ad biçiminde sağlanabilir. |
| client_id |Gerekli |Merhaba uygulama kimliği bu hello [uygulama kayıt portalı](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) tooyour uygulama atanmış. |
| redirect_uri |Gerekli |Merhaba, uygulama toohandle için gönderilen hello yanıt toobe istediğiniz URI yönlendirin. Bu tam olarak hello yeniden yönlendirme hello uygulama kayıt Portalı'nda kayıtlı URI'ler biriyle eşleşmelidir. |
| durum |Önerilen |Hello belirteci yanıt olarak da döndürülür hello istekte bulunan bir değer. İstediğiniz herhangi bir içerik dizesi olabilir. Merhaba sayfa veya görünüm üzerinde oldukları gibi Hello kimlik doğrulama isteği oluşmadan önce hello uygulamasında hello kullanıcının durumu hakkında hello durumu tooencode bilgileri kullanın. |

Bu noktada, Azure AD Kiracı yönetici toosign toocomplete hello isteğindeki gerektirir. Hello Yöneticisi tüm hello uygulama kayıt Portalı'nda, uygulamanız için istenen izinleri hello tooapprove istedi.

#### <a name="successful-response"></a>Başarılı yanıt
Hello Yöneticisi uygulamanızı hello izinlerini onaylarsa, hello başarılı yanıtı şuna benzer:

```
GET http://localhost/myapp/permissions?tenant=a8990e1f-ff32-408a-9f8e-78d3b9139b95&state=state=12345&admin_consent=True
```

| Parametre | Açıklama |
| --- | --- | --- |
| Kiracı |Uygulama hello izinlerin hello dizin Kiracı bunu, GUID biçiminde istedi. |
| durum |Merhaba, aynı zamanda isteğinde bir değer hello belirteci yanıt olarak döndürülür. İstediğiniz herhangi bir içerik dizesi olabilir. hello sayfa veya görünüm üzerinde oldukları gibi Hello kimlik doğrulama isteği oluşmadan önce hello durumu kullanılan tooencode hello uygulamasında hello kullanıcının durumu hakkındaki bilgilerdir. |
| admin_consent |Çok ayarlanacak**doğru**. |

#### <a name="error-response"></a>Hata yanıtı
Hello Yöneticisi uygulamanızı hello izinlerini onaylamaz, bu yanıt görülüyor hello başarısız oldu:

```
GET http://localhost/myapp/permissions?error=permission_denied&error_description=The+admin+canceled+the+request
```

| Parametre | Açıklama |
| --- | --- | --- |
| error |Oluşan hataları kullanılan tooclassify türde olabilir ve kullanılan tooreact tooerrors olabilir bir hata kodu dizesi. |
| error_description |Bir geliştirici yardımcı olabilecek belirli bir hata iletisi hello kök bir hatanın nedenini belirleyin. |

Merhaba yönetici onayı uç noktasından başarılı bir yanıt aldık sonra uygulamanızı hello izinler istendiğinde kazanmıştır. Ardından, istediğiniz hello kaynak için bir belirteç talep edebilirsiniz.

## <a name="using-permissions"></a>İzinlerini kullanma
Uygulamanız için toopermissions Hello kullanıcı izin sonra uygulamanızı uygulamanızın izni tooaccess bazı kapasite bir kaynağı temsil erişim belirteçleri elde edebilirsiniz. Bir erişim belirteci yalnızca tek bir kaynak için kullanılabilir, ancak hello erişim belirteci içine kodlanmış uygulamanız bu kaynak için verilen her izni yok. tooacquire bir erişim belirteci, uygulamanızı bir istek toohello v2.0 belirteç uç noktası, bu gibi yapabilirsiniz:

```
POST common/oauth2/v2.0/token HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/json

{
    "grant_type": "authorization_code",
    "client_id": "6731de76-14a6-49ae-97bc-6eba6914391e",
    "scope": "https://outlook.office.com/mail.read https://outlook.office.com/mail.send",
    "code": "AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq..."
    "redirect_uri": "https://localhost/myapp",
    "client_secret": "zc53fwe80980293klaj9823"  // NOTE: Only required for web apps
}
```

HTTP istekleri toohello kaynağında hello elde edilen erişim belirteci kullanabilirsiniz. Güvenilir bir şekilde, toohello kaynak uygulamanızı belirli bir görevi hello uygun izni tooperform olduğunu gösterir.  

Merhaba OAuth 2.0 hakkında daha fazla bilgi için protokolünü ve nasıl tooget erişim belirteçleri, bakın hello [v2.0 uç noktası Protokolü başvurusu](active-directory-v2-protocols.md).
