---
title: "aaaAzure Active Directory kimlik doğrulama ve Resource Manager | Microsoft Docs"
description: "Bir uygulama başka Azure abonelikleri ile tümleştirmek için bir Geliştirici Kılavuzu tooauthentication hello Azure Kaynak Yöneticisi API'si ve Azure Active Directory ile."
services: azure-resource-manager,active-directory
documentationcenter: na
author: dushyantgill
manager: timlt
editor: tysonn
ms.assetid: 17b2b40d-bf42-4c7d-9a88-9938409c5088
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 12/27/2016
ms.author: dugill;tomfitz
ms.openlocfilehash: 757e45fdb28488b45de70647746461888bf35a56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-resource-manager-authentication-api-tooaccess-subscriptions"></a>Resource Manager kimlik doğrulaması API'sini tooaccess abonelikleri kullanın
## <a name="introduction"></a>Giriş
Toocreate müşterinin Azure kaynaklarını yöneten uygulama gereken bir yazılım geliştirici varsa, bu konuda nasıl tooauthenticate ile Azure Resource Manager API'leri hello ve diğer abonelikler erişim tooresources geçirmesine gösterilmektedir.

Uygulamanızı hello çeşitli şekillerde Resource Manager API'leri erişebilirsiniz:

1. **Kullanıcı + uygulama erişimi**: oturum açmış bir kullanıcı adına kaynaklara uygulamalar için. Bu yaklaşım, web uygulamaları ve yalnızca "Etkileşimli Yönetimi" Azure kaynakları ile ilgili komut satırı araçları gibi uygulamalar için çalışır.
2. **Yalnızca uygulama erişim**: arka plan programı Hizmetleri ve zamanlanmış işler çalışan uygulamalar için. Merhaba uygulamanın kimliğini toohello kaynaklarına doğrudan erişim verilir. Bu yaklaşım, uzun vadeli gözetimsiz (katılımsız) erişim tooAzure gerektiren uygulamalar için çalışır.

Bu konu hakkında adım adım yönergeler toocreate her iki yetkilendirme yöntemi kullanan bir uygulama sağlar. Bunu nasıl tooperform her adım REST API veya C# ile gösterilir. Merhaba tam ASP.NET MVC uygulaması kullanılabilir [https://github.com/dushyantgill/VipSwapper/tree/master/CloudSense](https://github.com/dushyantgill/VipSwapper/tree/master/CloudSense).

## <a name="what-hello-web-app-does"></a>Hangi hello web uygulaması yapar
Merhaba web uygulaması:

1. Bir Azure kullanıcı oturum açtığında.
2. Kullanıcı toogrant hello web uygulama erişim tooResource Yöneticisi sorar.
3. Resource Manager erişmek için kullanıcı + uygulama erişim belirtecini alır.
4. (3. adım) belirtecine toocall Resource Manager ve ata hello uygulamanın hizmet asıl tooa rolü hello uygulama uzun vadeli erişim toohello abonelik verir hello abonelikte kullanır.
5. Yalnızca uygulama erişim belirtecini alır.
6. (5. adım) belirtecine toomanage kaynakları hello abonelik Kaynak Yöneticisi'ni kullanır.

Merhaba uçtan uca akış hello web uygulamasının aşağıdadır.

![Kaynak Yöneticisi kimlik doğrulama akışı](./media/resource-manager-api-authentication/Auth-Swim-Lane.png)

Bir kullanıcı olarak sağladığınız hello abonelik kimliği toouse istediğiniz hello abonelik için:

![Abonelik kimliği sağlayın](./media/resource-manager-api-authentication/sample-ux-1.png)

Oturum açma için hello hesap toouse seçin.

![hesabı seçin](./media/resource-manager-api-authentication/sample-ux-2.png)

Kimlik bilgilerinizi sağlayın.

![kimlik bilgilerini sağlayın](./media/resource-manager-api-authentication/sample-ux-3.png)

Merhaba uygulama erişim tooyour Azure abonelikleri verin:

![Erişim verme](./media/resource-manager-api-authentication/sample-ux-4.png)

Bağlı aboneliklerinizi yönetin:

![Abonelik Bağlan](./media/resource-manager-api-authentication/sample-ux-7.png)

## <a name="register-application"></a>Uygulamayı Kaydet
Kodlama başlamadan önce web uygulamanızı Azure Active Directory (AD ile) kaydedin. Merhaba uygulama kaydı Azure AD'de, uygulamanız için merkezi bir kimliği oluşturur. Uygulamanızı tooauthenticate ve erişim Azure Resource Manager API'leri kullanır uygulamanız OAuth istemci kimliği, yanıt URL'leri ve kimlik bilgileri gibi ilgili temel bilgileri tutar. Merhaba uygulama kaydı ayrıca çeşitli Microsoft APIs hello kullanıcı adına erişirken uygulamanız gereken izinleri atanmış hello kaydeder.

Uygulamanızı diğer abonelik eriştiği için bir çok kiracılı uygulama olarak yapılandırmanız gerekir. toopass doğrulama, Azure Active Directory ile ilişkilendirilmiş bir etki alanı belirtin. toosee hello etki alanları toohello günlüğünde, Azure Active Directory ile ilişkili [Klasik portal](https://manage.windowsazure.com). Azure Active Directory'yi seçin ve ardından **etki alanları**.

Aşağıdaki örnek hello nasıl tooregister hello uygulama Azure PowerShell kullanarak gösterir. Hello için en son sürümünü (Ağustos 2016) Azure PowerShell Bu komut toowork olması gerekir.

    $app = New-AzureRmADApplication -DisplayName "{app name}" -HomePage "https://{your domain}/{app name}" -IdentifierUris "https://{your domain}/{app name}" -Password "{your password}" -AvailableToOtherTenants $true

Merhaba AD uygulaması olarak toolog içinde hello uygulama kimliği ve parola gerekir. Merhaba önceki komuttan, kullanım döndürülen toosee hello uygulama kimliği:

    $app.ApplicationId

Aşağıdaki örnek hello nasıl tooregister hello uygulama Azure CLI kullanarak gösterir.

    azure ad app create --name {app name} --home-page https://{your domain}/{app name} --identifier-uris https://{your domain}/{app name} --password {your password} --available true

Merhaba sonuçları hello Merhaba uygulaması doğrulanırken ihtiyacınız AppID içerir.

### <a name="optional-configuration---certificate-credential"></a>İsteğe bağlı yapılandırma - sertifika kimlik bilgisi
Azure AD uygulamaları için de sertifika kimlik bilgileri destekler: otomatik olarak imzalanan bir sertifika oluşturun, hello özel anahtarı tutmak ve hello ortak anahtar tooyour Azure AD uygulama kaydı ekleyin. Kimlik doğrulaması için bir küçük yükü tooAzure özel anahtarınızı kullanarak imzalanmış AD ve Azure AD kaydettiğiniz hello ortak anahtarı kullanılarak hello imzayı doğrular, uygulamanızın gönderir.

Bir sertifika ile AD uygulaması oluşturma hakkında daha fazla bilgi için bkz [kullanım Azure PowerShell toocreate bir hizmet sorumlusu tooaccess kaynakları](resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority) veya [kullanım Azure CLI toocreate bir hizmet sorumlusu tooaccess kaynakları](resource-group-authenticate-service-principal-cli.md#create-service-principal-with-certificate).

## <a name="get-tenant-id-from-subscription-id"></a>Abonelik kimliği Kiracı kimliğinizi alma
toorequest kullanılan toocall Resource Manager olabilir bir belirteç, tooknow hello Kiracı kimliği hello Azure aboneliği barındıran hello Azure AD Kiracı uygulamanız gerekir. Büyük olasılıkla, kullanıcılarınızın abonelik kimlikleri biliyorum, ancak bunlar kendi Kiracı kimlikleri için Azure Active Directory anlamayabilirsiniz. tooget hello abonelik kimliği için isteyin hello kullanıcı hello kullanıcının Kiracı kimliği. Bu abonelik kimliği hello abonelik ilgili bir istek gönderirken sağlar:

    https://management.azure.com/subscriptions/{subscription-id}?api-version=2015-01-01

Merhaba isteği hello kullanıcı henüz oturum açmasını değil, ancak hello Kiracı kimliği hello yanıt almak için başarısız olur. Bu özel durum için hello yanıt üstbilgisi değeri hello Kiracı Kimliği almak **WWW-Authenticate**. Bu hello uygulamasında gördüğünüz [GetDirectoryForSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L20) yöntemi.

## <a name="get-user--app-access-token"></a>Kullanıcı + uygulama erişim belirteci alın
Uygulamanız hello kullanıcı tooAzure AD bir OAuth 2.0 yetkilendirme isteği - tooauthenticate hello kullanıcının kimlik bilgileri ile yeniden yönlendirir ve bir kimlik doğrulama kodu dönebilirsiniz. Uygulamanız için kaynak yöneticisi hello yetkilendirme kodu tooget bir erişim belirteci kullanır. Merhaba [ConnectSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/Controllers/HomeController.cs#L42) yöntemi hello yetkilendirme isteği oluşturur.

Bu konu hello REST API istekleri tooauthenticate hello kullanıcı gösterir. Kodunuzda Yardımcısı kitaplıkları tooperform kimlik doğrulaması de kullanabilirsiniz. Bu kitaplıklar hakkında daha fazla bilgi için bkz: [Azure Active Directory kimlik doğrulama kitaplıkları](../active-directory/active-directory-authentication-libraries.md). Kimlik Yönetimi uygulamada tümleştirme ile ilgili yönergeler için bkz: [Azure Active Directory Geliştirici Kılavuzu](../active-directory/active-directory-developers-guide.md).

### <a name="auth-request-oauth-20"></a>Kimlik doğrulama isteği (OAuth 2.0)
Açık Bağlan/OAuth2.0 yetkilendirmek istek kimliği toohello Azure AD Authorize son nokta yürütün:

    https://login.microsoftonline.com/{tenant-id}/OAuth2/Authorize

Bu istek için kullanılabilir hello sorgu dizesi parametreleri hello açıklanan [bir kimlik doğrulama kodu isteme](../active-directory/develop/active-directory-protocols-oauth-code.md#request-an-authorization-code) konu.

örnekte gösterildiği nasıl aşağıdaki hello toorequest OAuth2.0 yetkilendirme:

    https://login.microsoftonline.com/{tenant-id}/OAuth2/Authorize?client_id=a0448380-c346-4f9f-b897-c18733de9394&response_mode=query&response_type=code&redirect_uri=http%3a%2f%2fwww.vipswapper.com%2fcloudsense%2fAccount%2fSignIn&resource=https%3a%2f%2fgraph.windows.net%2f&domain_hint=live.com

Azure AD hello kullanıcının kimliğini doğrular ve gerekirse, hello kullanıcı toogrant izin toohello uygulama sorar. Merhaba yetkilendirme kodu toohello, uygulamanızın yanıt URL'si döndürür. Merhaba bağlı olarak response_mode, verileri sorgu dizesi veya gönderme verisi olarak da gönderir geri hello Azure AD istedi.

    code=AAABAAAAiL****FDMZBUwZ8eCAA&session_state=2d16bbce-d5d1-443f-acdf-75f6b0ce8850

### <a name="auth-request-open-id-connect"></a>Kimlik doğrulama isteği (Open ID Connect)
Bir açık bağlanma yetkisi istek kimliği, yalnızca tooaccess Azure Resource Manager hello kullanıcı adına istiyor, ancak Ayrıca kendi Azure AD hesabını kullanarak tooyour uygulamada hello kullanıcı toosign izin verin. Open ID Connect ile uygulamanızı uygulamanızı hello kullanıcı toosign kullanabileceğiniz Azure AD'den bir id_token de alır.

Bu istek için kullanılabilir hello sorgu dizesi parametreleri hello açıklanan [oturum açma gönderme hello isteği](../active-directory/develop/active-directory-protocols-openid-connect-code.md#send-the-sign-in-request) konu.

Bir örnek Open ID Connect isteğidir:

     https://login.microsoftonline.com/{tenant-id}/OAuth2/Authorize?client_id=a0448380-c346-4f9f-b897-c18733de9394&response_mode=form_post&response_type=code+id_token&redirect_uri=http%3a%2f%2fwww.vipswapper.com%2fcloudsense%2fAccount%2fSignIn&resource=https%3a%2f%2fgraph.windows.net%2f&scope=openid+profile&nonce=63567Dc4MDAw&domain_hint=live.com&state=M_12tMyKaM8

Azure AD hello kullanıcının kimliğini doğrular ve gerekirse, hello kullanıcı toogrant izin toohello uygulama sorar. Merhaba yetkilendirme kodu toohello, uygulamanızın yanıt URL'si döndürür. Merhaba bağlı olarak response_mode, verileri sorgu dizesi veya gönderme verisi olarak da gönderir geri hello Azure AD istedi.

Open ID Connect yanıt örneğidir:

    code=AAABAAAAiL*****I4rDWd7zXsH6WUjlkIEQxIAA&id_token=eyJ0eXAiOiJKV1Q*****T3GrzzSFxg&state=M_12tMyKaM8&session_state=2d16bbce-d5d1-443f-acdf-75f6b0ce8850

### <a name="token-request-oauth20-code-grant-flow"></a>Belirteç isteği (OAuth2.0 kod Grant akış)
Uygulamanızı Azure AD'den hello yetkilendirme kodu aldı, zaman tooget hello erişim belirteci için Azure Resource Manager var.  Bir OAuth2.0 kod Grant belirteç isteği toohello Azure AD belirteç uç noktası gönderin:

    https://login.microsoftonline.com/{tenant-id}/OAuth2/Token

Bu istek için kullanılabilir hello sorgu dizesi parametreleri hello açıklanan [hello yetkilendirme kodu kullanın](../active-directory/develop/active-directory-protocols-oauth-code.md#use-the-authorization-code-to-request-an-access-token) konu.

Aşağıdaki örneğine hello kod grant belirteci parola kimlik bilgisi için bir istek gösterir:

    POST https://login.microsoftonline.com/7fe877e6-a150-4992-bbfe-f517e304dfa0/oauth2/token HTTP/1.1

    Content-Type: application/x-www-form-urlencoded
    Content-Length: 1012

    grant_type=authorization_code&code=AAABAAAAiL9Kn2Z*****L1nVMH3Z5ESiAA&redirect_uri=http%3A%2F%2Flocalhost%3A62080%2FAccount%2FSignIn&client_id=a0448380-c346-4f9f-b897-c18733de9394&client_secret=olna84E8*****goScOg%3D

Sertifika kimlik bilgileri ile çalışırken, bir JSON Web Token (JWT) ve uygulamanızın sertifika kimlik bilgisi özel anahtarı hello kullanarak oturum (RSA SHA256) oluşturun. Merhaba hello belirteci için talep türleri gösterilir [JWT belirteci taleplerini](../active-directory/develop/active-directory-protocols-oauth-code.md#jwt-token-claims). Başvuru için bkz: Merhaba [Active Directory kimlik doğrulama kitaplığı (.NET) kod](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet/blob/dev/src/ADAL.PCL.Desktop/CryptographyHelper.cs) toosign istemci onaylama JWT belirteçleri.

Merhaba bkz [Open ID Connect spec](http://openid.net/specs/openid-connect-core-1_0.html#ClientAuthentication) istemci kimlik doğrulaması hakkında ayrıntılı bilgi için.

Aşağıdaki örneğine hello kod grant belirteciyle sertifika kimlik bilgisi için bir istek gösterir:

    POST https://login.microsoftonline.com/7fe877e6-a150-4992-bbfe-f517e304dfa0/oauth2/token HTTP/1.1

    Content-Type: application/x-www-form-urlencoded
    Content-Length: 1012

    grant_type=authorization_code&code=AAABAAAAiL9Kn2Z*****L1nVMH3Z5ESiAA&redirect_uri=http%3A%2F%2Flocalhost%3A62080%2FAccount%2FSignIn&client_id=a0448380-c346-4f9f-b897-c18733de9394&client_assertion_type=urn%3Aietf%3Aparams%3Aoauth%3Aclient-assertion-type%3Ajwt-bearer&client_assertion=eyJhbG*****Y9cYo8nEjMyA

Bir örnek yanıt kodu için belirteç verin:

    HTTP/1.1 200 OK

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1432039858","not_before":"1432035958","resource":"https://management.core.windows.net/","access_token":"eyJ0eXAiOiJKV1Q****M7Cw6JWtfY2lGc5A","refresh_token":"AAABAAAAiL9Kn2Z****55j-sjnyYgAA","scope":"user_impersonation","id_token":"eyJ0eXAiOiJKV*****-drP1J3P-HnHi9Rr46kGZnukEBH4dsg"}

#### <a name="handle-code-grant-token-response"></a>Kod grant belirteç yanıtı işlemek
Başarılı bir token yanıt için Azure Resource Manager hello (kullanıcı + uygulama) erişim belirteci içeriyor. Uygulamanız hello kullanıcı adına bu erişim belirteci tooaccess Kaynak Yöneticisi'ni kullanır. Azure AD tarafından verilen erişim belirteçleri Hello yaşam süresi bir saattir. Web uygulamanızı toorenew hello (kullanıcı + uygulama) erişim belirtecine ihtiyaç duyduğu düşüktür. Toorenew hello erişim belirteci alması gerekiyorsa, uygulamanızın hello belirteci yanıtta alır hello yenileme belirteci kullanın. Bir OAuth2.0 belirteci isteği toohello Azure AD belirteç uç noktası gönderin:

    https://login.microsoftonline.com/{tenant-id}/OAuth2/Token

Merhaba parametreleri toouse hello yenileme isteği ile açıklanan [yenileme hello erişim belirteci](../active-directory/develop/active-directory-protocols-oauth-code.md#refreshing-the-access-tokens).

Merhaba aşağıdaki örnekte nasıl toouse hello yenileme belirteci gösterilmektedir:

    POST https://login.microsoftonline.com/7fe877e6-a150-4992-bbfe-f517e304dfa0/oauth2/token HTTP/1.1

    Content-Type: application/x-www-form-urlencoded
    Content-Length: 1012

    grant_type=refresh_token&refresh_token=AAABAAAAiL9Kn2Z****55j-sjnyYgAA&client_id=a0448380-c346-4f9f-b897-c18733de9394&client_secret=olna84E8*****goScOg%3D

Yenileme belirteçleri kullanılan tooget yeni erişim belirteçleri için Azure Resource Manager olsa da, bunlar uygulamanızı çevrimdışı erişmek için uygun değildir. Merhaba yenileme belirteçleri ömrü sınırlı olduğunu ve yenileme belirteçleri ilişkili toohello kullanıcı. Merhaba kullanıcı hello kuruluş bırakırsa hello yenileme belirtecini kullanarak hello uygulama erişim kaybeder. Bu yaklaşım olan uygulamalar için uygun değil Azure kaynaklarını takımlar toomanage tarafından kullanılır.

## <a name="check-if-user-can-assign-access-toosubscription"></a>Kullanıcı erişim toosubscription atamaktır denetleyin
Uygulamanız artık Azure Resource Manager hello kullanıcı adına bir belirteç tooaccess sahiptir. Merhaba sonraki adım, uygulama toohello aboneliğinizin tooconnect olduğunu. Merhaba kullanıcı mevcut değilse bile bağladıktan sonra uygulamanızı bu abonelikleri yönetebilirsiniz (uzun süreli çevrimdışı erişim).

Her abonelik tooconnect için hello çağrısı [Resource Manager liste izinlerini](https://docs.microsoft.com/rest/api/authorization/permissions) API toodetermine hello kullanıcı hello abonelik için erişim yönetim haklarına sahip olup olmadığını belirler.

Merhaba [UserCanManagerAccessForSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L44) yöntemi hello ASP.NET MVC örnek uygulaması, bu çağrıyı uygular.

örnekte gösterildiği nasıl aşağıdaki hello toorequest bir abonelik bir kullanıcının izinleri. 83cfe939-2402-4581-b761-4f59b0a041e4 hello hello abonelik kimliğini gösterir.

    GET https://management.azure.com/subscriptions/83cfe939-2402-4581-b761-4f59b0a041e4/providers/microsoft.authorization/permissions?api-version=2015-07-01 HTTP/1.1

    Authorization: Bearer eyJ0eXAiOiJKV1QiLC***lwO1mM7Cw6JWtfY2lGc5A

Abonelik hello yanıt tooget kullanıcının izinlerini örneğidir:

    HTTP/1.1 200 OK

    {"value":[{"actions":["*"],"notActions":["Microsoft.Authorization/*/Write","Microsoft.Authorization/*/Delete"]},{"actions":["*/read"],"notActions":[]}]}

Merhaba izinleri API birden çok izin verir. Her izin izin verilen eylemleri (Eylemler) oluşur ve eylemleri (notactions) izin verilmiyor. Herhangi bir izni eylemler listesi izin hello bir eylem varsa ve bu izni hello notactions listesinde, hello kullanıcı yoksa tooperform Bu eyleme izin. **Microsoft.Authorization/roleassignments/Write** hello eylem, yönetim haklarına erişim verir. Uygulamanızı hello izinleri sonuç toolook regex eşleşme hello eylemleri ve her izin notactions Bu eylem dizesini ayrıştırma gerekir.

## <a name="get-app-only-access-token"></a>Yalnızca uygulama erişim belirteci alma
Şimdi, Hello kullanıcı erişimi toohello Azure aboneliği atayabilirsiniz varsa bilirsiniz. Merhaba sonraki adımlar şunlardır:

1. Merhaba uygun RBAC rolü tooyour uygulamanın kimliğini hello abonelikte atayın.
2. Merhaba erişim atama hello abonelik hello uygulamanın izni sorgulanırken veya Kaynak Yöneticisi'ni yalnızca uygulama belirteci kullanarak erişerek doğrulayın.
3. Merhaba hello abonelik kimliğini kalıcı uygulamaları "bağlı abonelikleri" veri yapınızı - kayıt hello bağlantı.

Merhaba ilk adımda daha yakın olarak bakalım. tooassign hello uygun RBAC rolü toohello uygulamanın kimliği belirlemeniz gerekir:

* Uygulamanızın kimlik hello kullanıcının Azure Active Directory'de Hello nesne kimliği
* Merhaba abonelikte uygulamanızın gerektirdiği hello RBAC rolü Hello tanıtıcısı

Uygulamanız bir Azure AD'den bir kullanıcı kimliği doğruladığında, Azure AD'de, uygulamanız için bir hizmet sorumlusu nesnesi oluşturur. Azure RBAC rolleri toobe tooservice ilkeleri atanan toogrant doğrudan erişim toocorresponding uygulamalar Azure kaynaklar sağlar. Bu tam olarak ne toodo istediğimiz eylemdir. Sorgu hello Azure AD grafik API'si toodetermine hello tanıtıcısı hello hizmet sorumlusu hello oturum açmış kullanıcı, uygulamanızın Azure AD kullanıcının.

Azure kaynak yöneticisi için yalnızca bir erişim belirteci sahip - yeni bir erişim belirteci toocall hello Azure AD Graph API gerekir. Azure AD'de her uygulama izni tooquery kendi hizmet sorumlusu nesnesi sahiptir, böylece yalnızca uygulama erişim belirteci yeterlidir.

<a id="app-azure-ad-graph" />

### <a name="get-app-only-access-token-for-azure-ad-graph-api"></a>Yalnızca uygulama erişimi için Azure AD Graph API belirteci alma
tooauthenticate, uygulama ve get belirteci tooAzure AD grafik API'si, sertifika bir istemci kimlik bilgileri verin OAuth2.0 akış belirteç isteği tooAzure AD belirteç uç noktası (**https://login.microsoftonline.com/ {directory_domain_name} / OAuth2/Token**).

Merhaba [GetObjectIdOfServicePrincipalInOrganization](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureADGraphAPIUtil.cs) ASP.net MVC örnek uygulama yalnızca uygulama access grafik API'sini kullanarak için belirteç alır hello yöntemi hello Active Directory kimlik doğrulama kitaplığı .NET için.

Bu istek için kullanılabilir hello sorgu dizesi parametreleri hello açıklanan [bir erişim belirteci isteği](../active-directory/develop/active-directory-protocols-oauth-service-to-service.md#request-an-access-token) konu.

İstemci kimlik bilgileri için bir örnek isteği belirteci verin:

    POST https://login.microsoftonline.com/62e173e9-301e-423e-bcd4-29121ec1aa24/oauth2/token HTTP/1.1
    Content-Type: application/x-www-form-urlencoded
    Content-Length: 187</pre>
    <pre>grant_type=client_credentials&client_id=a0448380-c346-4f9f-b897-c18733de9394&resource=https%3A%2F%2Fgraph.windows.net%2F &client_secret=olna8C*****Og%3D

İstemci kimlik bilgisi için bir örnek yanıt belirteç verin:

    HTTP/1.1 200 OK

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1432039862","not_before":"1432035962","resource":"https://graph.windows.net/","access_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSIsImtpZCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSJ9.eyJhdWQiOiJodHRwczovL2dyYXBoLndpbmRv****G5gUTV-kKorR-pg"}

### <a name="get-objectid-of-application-service-principal-in-user-azure-ad"></a>Kullanıcı Azure AD uygulama hizmet sorumlusu objectID alın
Şimdi hello yalnızca uygulama erişim belirteci tooquery hello kullanın [Azure AD grafik hizmet asıl adı](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity) API toodetermine hello hello uygulamanın hizmet sorumlusu hello dizinindeki nesne kimliği.

Merhaba [GetObjectIdOfServicePrincipalInOrganization](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureADGraphAPIUtil.cs#) yöntemi hello ASP.net MVC örnek uygulaması, bu çağrıyı uygular.

örnekte gösterildiği nasıl aşağıdaki hello toorequest bir uygulamanın hizmet sorumlusu. a0448380-c346-4f9f-b897-c18733de9394 hello istemci Merhaba uygulaması kimliğidir.

    GET https://graph.windows.net/62e173e9-301e-423e-bcd4-29121ec1aa24/servicePrincipals?api-version=1.5&$filter=appId%20eq%20'a0448380-c346-4f9f-b897-c18733de9394' HTTP/1.1

    Authorization: Bearer eyJ0eXAiOiJK*****-kKorR-pg

Merhaba aşağıdaki örnek bir uygulama hizmeti için bir yanıt toohello isteği asıl gösterir

    HTTP/1.1 200 OK

    {"odata.metadata":"https://graph.windows.net/62e173e9-301e-423e-bcd4-29121ec1aa24/$metadata#directoryObjects/Microsoft.DirectoryServices.ServicePrincipal","value":[{"odata.type":"Microsoft.DirectoryServices.ServicePrincipal","objectType":"ServicePrincipal","objectId":"9b5018d4-6951-42ed-8a92-f11ec283ccec","deletionTimestamp":null,"accountEnabled":true,"appDisplayName":"CloudSense","appId":"a0448380-c346-4f9f-b897-c18733de9394","appOwnerTenantId":"62e173e9-301e-423e-bcd4-29121ec1aa24","appRoleAssignmentRequired":false,"appRoles":[],"displayName":"CloudSense","errorUrl":null,"homepage":"http://www.vipswapper.com/cloudsense","keyCredentials":[],"logoutUrl":null,"oauth2Permissions":[{"adminConsentDescription":"Allow hello application tooaccess CloudSense on behalf of hello signed-in user.","adminConsentDisplayName":"Access CloudSense","id":"b7b7338e-683a-4796-b95e-60c10380de1c","isEnabled":true,"type":"User","userConsentDescription":"Allow hello application tooaccess CloudSense on your behalf.","userConsentDisplayName":"Access CloudSense","value":"user_impersonation"}],"passwordCredentials":[],"preferredTokenSigningKeyThumbprint":null,"publisherName":"vipswapper"quot;,"replyUrls":["http://www.vipswapper.com/cloudsense","http://www.vipswapper.com","http://vipswapper.com","http://vipswapper.azurewebsites.net","http://localhost:62080"],"samlMetadataUrl":null,"servicePrincipalNames":["http://www.vipswapper.com/cloudsense","a0448380-c346-4f9f-b897-c18733de9394"],"tags":["WindowsAzureActiveDirectoryIntegratedApp"]}]}

### <a name="get-azure-rbac-role-identifier"></a>Azure RBAC rolü tanımlayıcısını alın
tooassign hello uygun RBAC rolü tooyour hizmet sorumlusu, hello Azure RBAC rolü hello tanıtıcısı belirlemeniz gerekir.

Merhaba uygun RBAC rolü uygulamanız için:

* Yalnızca uygulamanızı herhangi bir değişiklik yapmadan hello abonelik izler, yalnızca hello abonelik okuyucusu izinleri gerektirir. Merhaba atamak **okuyucu** rol.
* Uygulamanızı Azure hello abonelik, varlıkları oluşturma/değiştirme/silme, yönetiyorsa hello katkıda bulunan izinleri birini gerektirir.
  * toomanage kaynak, belirli bir tür atama hello kaynak özgü katkıda bulunan rollerinin (sanal makine Katılımcısı, sanal ağ Katılımcısı, depolama hesabı katkıda bulunan, vb.)
  * toomanage herhangi bir kaynak türü, Ata hello **katkıda bulunan** rol.

Merhaba rol ataması, uygulamanız için gereken en az ayrıcalık seçin hello görünür toousers olduğundan.

Merhaba çağrısı [Kaynağı Yöneticisi rol tanımı API](https://docs.microsoft.com/rest/api/authorization/roledefinitions) tüm Azure RBAC rolleri ve arama sonra hello sonuç toofind hello yineleme toolist ada göre rol tanımı istenen.

Merhaba [GetRoleId](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L246) yöntemi hello ASP.net MVC örnek uygulaması, bu çağrıyı uygular.

Merhaba aşağıdaki örnekte gösterildiği nasıl isteği tooget Azure RBAC rolü tanımlayıcısı. 09cbd307-aa71-4aca-b346-5f253e6e3ebb hello hello abonelik kimliğini gösterir.

    GET https://management.azure.com/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleDefinitions?api-version=2015-07-01 HTTP/1.1

    Authorization: Bearer eyJ0eXAiOiJKV*****fY2lGc5

Merhaba yanıt hello biçimi aşağıdaki gibidir:

    HTTP/1.1 200 OK

    {"value":[{"properties":{"roleName":"API Management Service Contributor","type":"BuiltInRole","description":"Lets you manage API Management services, but not access toothem.","scope":"/","permissions":[{"actions":["Microsoft.ApiManagement/Services/*","Microsoft.Authorization/*/read","Microsoft.Resources/subscriptions/resources/read","Microsoft.Resources/subscriptions/resourceGroups/read","Microsoft.Resources/subscriptions/resourceGroups/resources/read","Microsoft.Resources/subscriptions/resourceGroups/deployments/*","Microsoft.Insights/alertRules/*","Microsoft.Support/*"],"notActions":[]}]},"id":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleDefinitions/312a565d-c81f-4fd8-895a-4e21e48d571c","type":"Microsoft.Authorization/roleDefinitions","name":"312a565d-c81f-4fd8-895a-4e21e48d571c"},{"properties":{"roleName":"Application Insights Component Contributor","type":"BuiltInRole","description":"Lets you manage Application Insights components, but not access toothem.","scope":"/","permissions":[{"actions":["Microsoft.Insights/components/*","Microsoft.Insights/webtests/*","Microsoft.Authorization/*/read","Microsoft.Resources/subscriptions/resources/read","Microsoft.Resources/subscriptions/resourceGroups/read","Microsoft.Resources/subscriptions/resourceGroups/resources/read","Microsoft.Resources/subscriptions/resourceGroups/deployments/*","Microsoft.Insights/alertRules/*","Microsoft.Support/*"],"notActions":[]}]},"id":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleDefinitions/ae349356-3a1b-4a5e-921d-050484c6347e","type":"Microsoft.Authorization/roleDefinitions","name":"ae349356-3a1b-4a5e-921d-050484c6347e"}]}

Bu API düzenli olarak toocall gerekmez. Saptadıktan sonra hello rol tanımı iyi bilinen GUID Merhaba, hello rol tanımı kimliği olarak oluşturabileceğiniz:

    /subscriptions/{subscription_id}/providers/Microsoft.Authorization/roleDefinitions/{well-known-role-guid}

Yaygın olarak kullanılan yerleşik roller hello iyi bilinen GUID'lerini şunlardır:

| Rol | GUID |
| --- | --- |
| Okuyucu |acdd72a7-3385-48EF-bd42-f606fba81ae7 |
| Katılımcı |b24988ac-6180-42a0-ab88-20f7382dd24c |
| Sanal makine Katılımcısı |d73bb868-a0df-4d4d-bd69-98a00b01fccb |
| Sanal ağ Katılımcısı |b34d265f-36f7-4a0d-a4d4-e158ca92e90f |
| Depolama hesabı katkıda bulunan |86e8f5dc-a6e9-4c67-9d15-de283e8eac25 |
| Web sitesi katkıda bulunan |de139f84-1756-47ae-9be6-808fbbe84772 |
| Web planı katkıda bulunan |2cc479cb-7b4d-49a8-b449-8c00fd0f0a4b |
| SQL Server katkıda bulunan |6d8ee4ec-f05a-4a1d-8b00-a9b17e38b437 |
| SQL DB Katılımcısı |9b7fa17d-e63e-47b0-bb0a-15c516ac86ec |

### <a name="assign-rbac-role-tooapplication"></a>RBAC rolü tooapplication atayın
Gereksinim duyduğunuz her şeyi tooassign hello uygun RBAC rolü tooyour hizmet sorumlusu hello kullanarak sahip [Kaynağı Yöneticisi rol ataması oluşturma](https://docs.microsoft.com/rest/api/authorization/roleassignments) API.

Merhaba [GrantRoleToServicePrincipalOnSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L170) yöntemi hello ASP.net MVC örnek uygulaması, bu çağrıyı uygular.

Bir örnek istek tooassign RBAC rolü tooapplication:

    PUT https://management.azure.com/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/microsoft.authorization/roleassignments/4f87261d-2816-465d-8311-70a27558df4c?api-version=2015-07-01 HTTP/1.1

    Authorization: Bearer eyJ0eXAiOiJKV1QiL*****FlwO1mM7Cw6JWtfY2lGc5
    Content-Type: application/json
    Content-Length: 230

    {"properties": {"roleDefinitionId":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleDefinitions/acdd72a7-3385-48ef-bd42-f606fba81ae7","principalId":"c3097b31-7309-4c59-b4e3-770f8406bad2"}}

Merhaba istekte değerleri aşağıdaki hello kullanılır:

| GUID | Açıklama |
| --- | --- |
| 09cbd307-aa71-4aca-b346-5f253e6e3ebb |Merhaba abonelik Hello kimliği |
| c3097b31-7309-4c59-b4e3-770f8406bad2 |Merhaba hizmet sorumlusu hello uygulamasının Hello nesne kimliği |
| acdd72a7-3385-48EF-bd42-f606fba81ae7 |Merhaba okuyucu rolüne Hello kimliği |
| 4f87261d-2816-465D-8311-70a27558df4c |Merhaba yeni rol ataması için oluşturulan yeni bir GUID |

Merhaba yanıt hello biçimi aşağıdaki gibidir:

    HTTP/1.1 201 Created

    {"properties":{"roleDefinitionId":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleDefinitions/acdd72a7-3385-48ef-bd42-f606fba81ae7","principalId":"c3097b31-7309-4c59-b4e3-770f8406bad2","scope":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb"},"id":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleAssignments/4f87261d-2816-465d-8311-70a27558df4c","type":"Microsoft.Authorization/roleAssignments","name":"4f87261d-2816-465d-8311-70a27558df4c"}

### <a name="get-app-only-access-token-for-azure-resource-manager"></a>Azure kaynak yöneticisi için yalnızca uygulama erişim belirteci alma
toovalidate hello abonelikte bu uygulama istenen hello erişimi, yalnızca uygulama belirteci kullanarak hello abonelikte test görevi gerçekleştirin.

tooget bir yalnızca uygulama erişim belirteci bölümündeki yönergeleri izleyerek [almak yalnızca uygulama erişim belirteci için Azure AD Graph API](#app-azure-ad-graph), hello kaynak parametresi için farklı bir değere sahip:

    https://management.core.windows.net/

Merhaba [ServicePrincipalHasReadAccessToSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L110) ASP.NET MVC örnek uygulama yalnızca uygulama erişim Azure Kaynak Yöneticisi'ni kullanarak için belirteç alır hello yöntemi hello Active Directory kimlik doğrulama kitaplığı .net için.

#### <a name="get-applications-permissions-on-subscription"></a>Uygulama izinleri abonelikte Al
Uygulamanızı sahip hello toocheck istenen bir Azure aboneliği erişimi, hello da çağırabilir [kaynak yöneticisi izinleri](https://docs.microsoft.com/rest/api/authorization/permissions) API. Bu yaklaşım hello kullanıcı hello abonelik için erişim yönetim haklarına sahip olup olmadığını belirledi benzer toohow olur. Ancak, bu süre, hello izinleri API hello önceki adımda aldığınız hello yalnızca uygulama erişim belirteci ile çağırın.

Merhaba [ServicePrincipalHasReadAccessToSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L110) yöntemi hello ASP.NET MVC örnek uygulaması, bu çağrıyı uygular.

## <a name="manage-connected-subscriptions"></a>Bağlı aboneliklerini yönetme
Merhaba uygun RBAC rolü tooyour uygulamanın hizmet sorumlusu hello abonelikte atandığında, uygulamanızın izleme/Azure kaynak yöneticisi için yalnızca uygulama erişim belirteçleri kullanarak yönetme tutun.

Artık mümkün tooaccess Bu abonelik ise bir abonelik sahibi, uygulamanızın rol ataması hello Klasik portalında veya komut satırı araçlarını, uygulamanızı kullanarak kaldırır. Bu durumda, dış hello uygulamadan hello aboneliğiyle hello bağlantısı koptu hello kullanıcıya bildirme ve bir seçenek çok "Onar" Merhaba bağlantı vermediğiniz gerekir. "Onar" yalnızca çevrimdışı silindi hello rol ataması yeniden oluşturur.

Merhaba kullanıcı tooconnect abonelikleri tooyour uygulaması yalnızca etkin olarak hello kullanıcı toodisconnect abonelikleri çok izin vermeniz gerekir. Bir erişim yönetimi açısından bakıldığında, bağlantı kesme hello uygulamanın hizmet sorumlusu hello abonelikte sahip hello rol atamasının kaldırılması anlamına gelir. İsteğe bağlı olarak, hello abonelik hello uygulamada herhangi bir durum çok kaldırılmış olabilir.
Yalnızca hello abonelik erişim yönetim izni olan kullanıcılar mümkün toodisconnect hello abonelik ' dir.

Merhaba [RevokeRoleFromServicePrincipalOnSubscription yöntemi](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L200) hello ASP.net MVC örnek uygulama bu çağrıyı uygular.

İşte bu kadar - kullanıcılar artık kolayca bağlanabilir ve uygulamanız ile bunların Azure Aboneliklerini yönetmek.
