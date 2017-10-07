---
title: "Azure AD kimlik doğrulama tooaccess Azure Media Services API REST ile aaaUse | Microsoft Docs"
description: "Tooaccess Azure Media Services API kullanarak Azure Active Directory kimlik doğrulaması ile nasıl REST öğrenin."
services: media-services
documentationcenter: 
author: willzhan
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: willzhan;juliako
ms.openlocfilehash: 114f7bdde3a8f5fe6189d712e05b6afdc8a8787a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-ad-authentication-tooaccess-hello-azure-media-services-api-with-rest"></a>Azure Media Services API REST ile kullanım Azure AD kimlik doğrulama tooaccess hello

Hello Azure Media Services ekip Azure Media Services erişimi için Azure Active Directory (Azure AD) kimlik doğrulama desteği yayımladı. Ayrıca, Media Services erişimi için planları toodeprecate Azure erişim denetimi hizmeti kimlik doğrulamasını duyurdu. Her Azure aboneliği ve her medya hizmetleri hesabı ekli tooan Azure AD Kiracı olduğundan, Azure AD kimlik doğrulama desteği birçok güvenlik avantajları beraberinde getirir. Bu değişiklik ve (uygulamanız için'de hello Media Services .NET SDK'sı kullanıyorsanız) geçiş ayrıntılarını görmek için hello şu blog yazılarını ve makaleler:

- [Azure Media Services, Azure AD için destek sunar ve erişim denetimi kimlik doğrulamasının kullanımdan kaldırma](https://azure.microsoft.com/blog/azure%20media%20service%20aad%20auth%20and%20acs%20deprecation)
- [Azure AD kimlik doğrulamasını kullanarak erişim Azure Media Services API](media-services-use-aad-auth-to-access-ams-api.md)
- [Microsoft .NET kullanarak Azure AD kimlik doğrulama tooaccess Azure Media Services API](media-services-dotnet-get-started-with-aad.md)
- [Hello Azure portal kullanarak Azure AD kimlik doğrulaması ile çalışmaya başlama](media-services-portal-get-started-with-aad.md)

Bazı müşteriler, Media Services çözümleri kısıtlamaları aşağıdaki hello altında toodevelop gerekir:

*   Microsoft .NET veya C# programlama bir dil kullanın veya Windows hello çalışma zamanı ortamı değil.
*   Active Directory kimlik doğrulama kitaplıkları gibi Azure AD kitaplıkları programlama dili hello için kullanılabilir değil veya kendi çalışma zamanı ortamı için kullanılamaz.

Bazı müşteriler, erişim denetimi kimlik doğrulaması ve Azure Media Services erişimi için REST API kullanarak uygulamaları geliştirdik. Bu müşteriler için Azure AD kimlik doğrulaması için bir yol toouse yalnızca hello REST API gerekir ve sonraki Azure Media Services erişebilirsiniz. Toonot gereken herhangi bir hello Azure AD kitaplıkları veya hello Media Services .NET SDK'sını kullanır. Bu makalede, bir çözüm açıklar ve bu senaryo için örnek kod sağlar. Merhaba kod hiçbir bağımlılık tüm Azure AD ile tüm REST API çağrıları olduğundan veya Azure Media Services kitaplığı hello kod kolayca diğer programlama dili çevrilmiş tooany olabilir.

> [!IMPORTANT]
> Şu anda, Media Services hello Azure erişim denetimi Hizmetleri kimlik doğrulama modelini destekler. Ancak, erişim denetimi kimlik doğrulaması 1 Haziran 2018 kullanım dışı kalacaktır. Mümkün olan en kısa sürede toohello Azure AD kimlik doğrulama modeli geçirmek öneririz.


## <a name="design"></a>Tasarlayın

Bu makalede, kimlik doğrulama ve yetkilendirme tasarım aşağıdaki hello kullanın:

*  Yetkilendirme Protokolü: OAuth 2.0. OAuth 2.0 kimlik doğrulama ve yetkilendirme kapsayan bir web güvenlik standardıdır. Google, Microsoft, Facebook ve PayPal tarafından desteklenir. Ekim 2012 onay. Microsoft, OAuth 2.0 ve Openıd Connect sıkıca destekler. Bu standartlar her ikisinin birden çok hizmet ve istemci kitaplıkları, Azure Active Directory gibi .NET (OWIN) Katana açık Web arabirimi desteklenir ve Azure AD kitaplıkları.
*  Vermek türü: istemci kimlik bilgileri vermenizi türü. İstemci kimlik bilgileri biridir hello dört sağlama türleri, OAuth 2.0. Genellikle, Azure AD Microsoft Graph API erişimi için de kullanılır.
*  Kimlik doğrulama modu: hizmet sorumlusu. Merhaba diğer kimlik doğrulama kullanıcı veya etkileşimli kimlik doğrulama modudur.

Dört uygulamalar veya hizmetler toplam söz konusu Media Services'i kullanarak hello Azure AD kimlik doğrulama ve yetkilendirme akışı. Merhaba uygulamaları ve Hizmetleri ve hello akış, aşağıdaki tablonun hello açıklanmaktadır:

|Uygulama türü |Uygulama |Akış|
|---|---|---|
|İstemci | Müşteri uygulama ya da çözüm | Bu uygulamayı (aslında, kendi proxy) hizmet hesabı hello Azure aboneliği ve hello medya bulunan hello Azure AD kiracısında kaydedilir. Merhaba hizmet sorumlusu kayıtlı hello uygulamasının sonra hello hello medya hizmet hesabının erişim denetimi (IAM) sahibi veya katkıda bulunan rolü ile verilir. Merhaba hizmet sorumlusu hello uygulama istemci Kimliğini ve istemci gizli anahtarı temsil edilir. |
|Kimlik sağlayıcıyı (IDP) | IDP olarak Azure AD | Merhaba kayıtlı uygulama hizmet sorumlusu (istemci kimliği ve istemci gizli anahtarı) hello IDP olarak Azure AD tarafından doğrulanır. Bu kimlik doğrulaması, dahili ve örtük olarak gerçekleştirilir. İstemci kimlik bilgileri akışının olduğu gibi hello istemci yerine hello kullanıcının kimliği doğrulanır. |
|Belirteç Hizmeti (STS) güvenli / OAuth sunucu | STS olarak Azure AD | Merhaba IDP (veya OAuth sunucusu OAuth 2.0 terimleriyle) göre kimlik doğrulamasından sonra bir erişim belirteci veya JSON Web Token (JWT) erişim toohello orta katman Kaynak STS/OAuth sunucusu olarak Azure AD tarafından verilir: Örneğimizde, Media Services REST API uç noktası hello. |
|Kaynak | Media Services REST API'si | Her Media Services REST API çağrısı STS veya hello OAuth sunucu olarak Azure AD tarafından verilen bir erişim belirteci tarafından yetkilendirildi. |

Merhaba örnek kodu çalıştırmak ve yakalama JWT veya bir erişim belirteci, hello JWT öznitelikleri aşağıdaki hello sahiptir:

    aud: "https://rest.media.azure.net",

    iss: "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/",

    iat: 1497146280,

    nbf: 1497146280,
    exp: 1497150180,

    aio: "Y2ZgYDjuy7SptPzO/muf+uRu1B+ZDQA=",

    appid: "02ed1e8e-af8b-477e-af3d-7e7219a99ac6",

    appidacr: "1",

    idp: "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/",

    oid: "a938cfcc-d3de-479c-b0dd-d4ffe6f50f7c",

    sub: "a938cfcc-d3de-479c-b0dd-d4ffe6f50f7c",

    tid: "72f988bf-86f1-41af-91ab-2d7cd011db47",

Merhaba JWT ve uygulamalarında hello dört hello öznitelikleri veya tablo önceki hello Hizmetleri'nde arasında hello eşlemeleri şunlardır:

|Uygulama türü |Uygulama |JWT özniteliği |
|---|---|---|
|İstemci |Müşteri uygulama ya da çözüm |AppID: "02ed1e8e-af8b-477e-af3d-7e7219a99ac6". Merhaba istemci kimliği bir uygulama hello sonraki bölümde tooAzure AD kaydeder. |
|Kimlik sağlayıcıyı (IDP) | IDP olarak Azure AD |IDP: "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/".  Merhaba GUID hello Microsoft kimliği Kiracı (microsoft.onmicrosoft.com) olur. Her bir kiracı kendi, benzersiz kimliği vardır. |
|Belirteç Hizmeti (STS) güvenli / OAuth sunucu |STS olarak Azure AD | ISS: "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/". Merhaba GUID hello Microsoft kimliği Kiracı (microsoft.onmicrosoft.com) olur. |
|Kaynak | Media Services REST API'si |aud: "https://rest.media.azure.net". Merhaba alıcı veya İzleyici hello erişim belirteci. |

## <a name="steps-for-setup"></a>Kurulum adımları

tooregister ve Azure AD uygulaması Azure AD kimlik doğrulaması ve tooobtain hello Azure Media Services REST API uç noktası, aşağıdaki adımları tam hello çağırmak için bir erişim belirteci ayarlayın:

1.  Merhaba, [Klasik Azure portalı](http://go.microsoft.com/fwlink/?LinkID=213885), Azure AD uygulama (örneğin, wzmediaservice) toohello Azure AD kiracısı (örneğin, microsoft.onmicrosoft.com) kaydedin. Web uygulaması veya yerel uygulama kayıtlı olup olmadığını önemli değildir. Ayrıca, tüm oturum açma URL'si ve yanıt URL'si (örneğin, her ikisi için de http://wzmediaservice.com) seçebilirsiniz.
2. Merhaba, [Klasik Azure portalı](http://go.microsoft.com/fwlink/?LinkID=213885), Git toohello **yapılandırma** uygulamanızın sekmesi. Not hello **istemci kimliği**. Ardından, altında **anahtarları**, Oluştur bir **istemci anahtar** (gizli). 

    > [!NOTE] 
    > Merhaba istemci gizli anahtarı not edin. Yeniden gösterilmeyecektir.
    
3.  Merhaba, [Azure portal](http://ms.portal.azure.com), Git toohello Media Services hesabı. Select hello **erişim denetimi** (IAM) bölmesi. Merhaba sahibi veya hello katkıda bulunan rolü sahip yeni bir üye ekleyin. Merhaba sorumlusu için (Bu örnekte, wzmediaservice) 1. adımda kaydettiğiniz hello uygulama adını arayın.

## <a name="info-toocollect"></a>Bilgi toocollect

tooprepare kodlama tutun, aşağıdaki veri noktaları tooinclude hello kodda hello Topla:

*   Bir STS uç noktası olarak Azure AD: https://login.microsoftonline.com/microsoft.onmicrosoft.com/oauth2/token. Bu uç noktasından bir JWT erişim belirteci istendi. Ayrıca tooserving bir IDP olarak Azure AD aynı zamanda bir STS olarak görev yapar. Azure AD kaynak erişimi (bir erişim belirteci) için JWT verir. JWT belirteci çeşitli talep vardır.
*   Kaynak veya hedef kitle olarak Azure Media Services REST API: https://rest.media.azure.net.
*   İstemci kimliği: Bkz. Adım 2'de [kurulum adımları](#steps-for-setup).
*   İstemci gizliliği: bkz: adım 2'de [kurulum adımları](#steps-for-setup).
*   Media Services hesabı REST API uç noktanızı biçimini izleyen hello içinde:

    https://[media_service_account_name].restv2. [data_center].media.azure.net/API 

    Bu karşı tüm hangi Media Services REST API çağrıları, uygulamanızda yapılan hello uç noktadır. Örneğin, https://willzhanmswjapan.restv2.japanwest.media.azure.net/API.

Ardından, web.config veya app.config dosyasını toouse kodunuzda bu beş parametreleri koyabilirsiniz.

## <a name="sample-code"></a>Örnek kod

Merhaba örnek kodda bulabilirsiniz [Azure Media Services erişimi için Azure AD kimlik doğrulamasını: REST API aracılığıyla her ikisi de](https://github.com/willzhan/WAMSRESTSoln).

Merhaba örnek kod iki bölümden oluşur:

*   Azure AD kimlik doğrulama ve yetkilendirme için tüm hello REST API koduna sahip bir DLL Kitaplığı projesi. Ayrıca, REST API çağrıları toohello Media Services REST API uç noktası, hello erişim belirteci ile yapmak için bir yöntem vardır.
*   Azure AD kimlik doğrulaması başlatır ve farklı Media Services REST API çağrıları bir konsol test istemcisi.

Merhaba örnek proje üç özelliklere sahiptir:

*   Yalnızca hello REST API kullanarak Azure AD kimlik doğrulamaları hello istemci kimlik bilgileri aracılığıyla verin.
*   Yalnızca hello REST API kullanarak azure Media Services erişimi.
*   Azure depolama erişim kullanarak yalnızca hello REST API (olarak kullanılan toocreate REST API kullanarak bir Media Services hesabı).


## <a name="where-is-hello-refresh-token"></a>Merhaba yenileme belirteci nerede?

Bazı okuyucular isteyebilir: hello yenileme belirteci nerede? Neden bir yenileme belirteci burada kullanabilir?

bir yenileme belirteci Hello amacı toorefresh bir erişim belirteci değil. Bunun yerine, son kullanıcı kimlik doğrulaması veya kullanıcı müdahalesi tasarlanmış toobypass değildir ve bir önceki belirtecinin süresi dolduğunda hala geçerli erişim belirteci alın. Bir yenileme belirteci için daha iyi bir adı "kullanıcı yeniden-oturumu açma belirteci atlama."gibi bir şey olabilir

Merhaba OAuth 2.0 yetkilendirme izin akışı (kullanıcı adı ve parola, bir kullanıcı adına hareket) kullanırsanız, bir yenileme belirteci, kullanıcı müdahalesi gerektirmeden yenilenmiş bir erişim belirteci almak yardımcı olur. Ancak, hello OAuth 2.0 istemci kimlik bilgileri Biz bu makalede açıklamak akış vermek için hello istemci kendi adına hareket eder. Hiçbir kullanıcı etkileşimi gerekmez ve hello yetkilendirme sunucusu, bir yenileme belirteci vermek çok gerekmez ve olmaz. Merhaba ayıklaması **GetUrlEncodedJWT** yöntemi, fark hello yanıt hello belirteç uç noktasından bir erişim belirteci ancak herhangi bir yenileme belirteci sahiptir.

## <a name="next-steps"></a>Sonraki adımlar

Kullanmaya başlama [tooyour hesabı dosyaları karşıya yükleme](media-services-dotnet-upload-files.md).
