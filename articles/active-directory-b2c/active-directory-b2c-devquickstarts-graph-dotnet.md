---
title: "Azure Active Directory B2C: Kullanım hello grafik API'si | Microsoft Docs"
description: "Nasıl toocall hello grafik API'si bir B2C Kiracı için bir uygulama kimliği tooautomate hello işlemi kullanarak."
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: f9904516-d9f7-43b1-ae4f-e4d9eb1c67a0
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/07/2017
ms.author: parakhj
ms.openlocfilehash: a17cdc4adf57dbf22592d99ef8ecde41652763fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-use-hello-graph-api"></a>Azure AD B2C: hello grafik API'sini kullanın
Azure Active Directory (Azure AD) B2C kiracılar toobe çok büyük eğilimlidir. Bu, birçok genel kiracı yönetim görevlerini programlı olarak gerçekleştirilen toobe gerektiği anlamına gelir. Kullanıcı Yönetimi buna birincil bir örnektir. Mevcut bir kullanıcı deposu tooa B2C Kiracı toomigrate gerekebilir. Kendi sayfasında toohost kullanıcı kaydı istediğiniz ve hello perde arkasında Azure AD B2C dizininizde kullanıcı hesapları oluşturun. Bu tür bir görev hello özelliği toocreate, okuma, güncelleştirme gerektiren ve kullanıcı hesaplarını silin. Bu görevleri hello Azure AD Graph API kullanarak yapabilirsiniz.

B2C kiracılar için hello grafik API'si ile iletişim iki birincil modu mevcuttur.

* Merhaba görevleri gerçekleştirdiğinizde etkileşimli, bir kez çalıştır görevler için bir yönetici hesabı hello B2C Kiracı olarak işlem yapmalıdır. Yöneticinin tüm çağrıları toohello grafik API'si gerçekleştirmeden önce bu modu yönetici toosign kimlik bilgilerinizle gerektirir.
* Otomatik, sürekli görevleri için bazı türünü sağladığınız hizmet hesabının hello gerekli ayrıcalıklara tooperform yönetim görevleri ile kullanmanız gerekir. Azure AD'de bu uygulama kaydetme ve tooAzure AD kimlik doğrulaması yapabilirsiniz. Bu kullanılarak yapılır bir **uygulama kimliği** hello kullanan [OAuth 2.0 istemci kimlik bilgileri vermenizi](../active-directory/develop/active-directory-authentication-scenarios.md#daemon-or-server-application-to-web-api). Bu durumda, hello uygulama bir kullanıcı olarak değil kendisini toocall hello grafik API'si görür.

Bu makalede, sizi nasıl tooperform hello otomatik kullanım örneği ele alacağız. toodemonstrate, biz yapı .NET 4.5 `B2CGraphClient` gerçekleştiren kullanıcı oluşturma, okuma, güncelleştirme ve Sil (CRUD) işlemleridir. Merhaba istemci bir Windows komut satırı tooinvoke sağlayan arabirimi (CLI) çeşitli yöntemlerle sahip olur. Ancak, hello kodu toobehave etkileşimsiz, otomatik bir şekilde yazılır.

## <a name="get-an-azure-ad-b2c-tenant"></a>Bir Azure AD B2C kiracısı edinme
Uygulama veya kullanıcıların oluşturabilir veya Azure AD ile etkileşimde önce Azure AD B2C kiracısı ve hello kiracısında genel yönetici hesabı gerekir. Zaten bir kiracı yoksa [Azure AD B2C ile çalışmaya başlama](active-directory-b2c-get-started.md).

## <a name="register-your-application-in-your-tenant"></a>Kiracınızda uygulamanızı kaydetme
B2C Kiracı aldıktan sonra hello aracılığıyla uygulamanızı tooregister gerek [Azure Portal](https://portal.azure.com).

> [!IMPORTANT]
> toouse hello grafik API'si B2C kiracınızın ile Merhaba genel kullanarak tooregister adanmış bir uygulama gerekiyor *uygulama kayıtlar* dikey penceresinde hello Azure Portal, **değil** Azure AD B2C'in  *Uygulamaları* dikey. Hello Azure AD B2C'ın kayıtlı hello zaten varolan B2C uygulamaları tekrar kullanamazsınız *uygulamaları* dikey.

1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Azure AD B2C kiracınızın hello sağ üst köşedeki hello sayfasının hesabınızı seçerek belirleyin.
3. Merhaba sol gezinti bölmesinde seçin **daha Hizmetleri**, tıklatın **uygulama kayıtlar**, tıklatıp **Ekle**.
4. Merhaba komut istemlerini izleyin ve yeni bir uygulama oluşturun. 
    1. Seçin **Web uygulaması / API** uygulama türü hello gibi.    
    2. Sağlamak **URI herhangi bir yeniden yönlendirme** (örneğin https://B2CGraphAPI) Bu örnek için uygun değil olarak.  
5. Merhaba uygulama şimdi yukarı uygulamaları hello listesinde göster üzerinde tooobtain hello **uygulama kimliği** (istemci kimliği olarak da bilinir). Bir sonraki bölümde gereksinim duyacağınız kopyalayın.
6. Merhaba ayarlar dikey penceresinde tıklayın **anahtarları** ve yeni bir anahtar (istemci gizli anahtarı olarak da bilinir) ekleyin. Ayrıca daha sonraki bir bölüme kullanmak için kopyalayın.

## <a name="configure-create-read-and-update-permissions-for-your-application"></a>Yapılandırma oluşturmak, okumak ve güncelleştirmek, uygulamanız için izinler
Tooconfigure gereksinim artık tüm Merhaba, uygulama tooget izinleri toocreate gerekli, okuma, güncelleştirme ve kullanıcıları silme.

1. İçinde etmeden Azure portal'ın uygulama kayıtlar dikey Merhaba, uygulamanızı seçin.
2. Merhaba ayarlar dikey penceresinde tıklayın **gerekli izinleri**.
3. Merhaba gerekli izinleri dikey penceresinde tıklayın **Windows Azure Active Directory**.
4. Merhaba erişimi etkinleştir dikey penceresinde hello seçin **dizin verilerini okuma ve yazma** iznini **uygulama izinleri** tıklatıp **kaydetmek**.
5. Son olarak, geri hello gerekli izinleri dikey penceresinde hello üzerinde tıklayın **izinler** düğmesi.

B2C kiracınızın izin toocreate, okuma ve güncelleştirme kullanıcıları olan bir uygulama artık sahipsiniz.

## <a name="configure-delete-permissions-for-your-application"></a>Uygulamanız için silme izinleri yapılandırma
Şu anda hello *dizin verilerini okuma ve yazma* izin vermez **değil** hello özelliği toodo kullanıcıları silme gibi tüm silme işlemleri içerir. Uygulama hello özelliği toodelete kullanıcılarınızın toogive istiyorsanız, PowerShell ile ilgili aşağıdaki ek adımları toodo gerekir, aksi takdirde, toohello sonraki bölümü atlayabilirsiniz.

İlk olarak, karşıdan yüklenip hello [Microsoft Online Services oturum açma Yardımcısı](http://go.microsoft.com/fwlink/?LinkID=286152). Ardından yükleyip hello [64-bit Windows PowerShell için Azure Active Directory Modülü](http://go.microsoft.com/fwlink/p/?linkid=236297).

Merhaba PowerShell modülü yükledikten sonra PowerShell'i açın ve tooyour B2C Kiracı bağlanın. Çalıştırdıktan sonra `Get-Credential`, bir kullanıcı adı ve parola, hello kullanıcı adını girin ve B2C Kiracı yönetici hesabınızın parolası istenir.

> [!IMPORTANT]
> İhtiyacınız olan toouse bir B2C Kiracı yönetici hesabı **yerel** toohello B2C Kiracı. Bu hesapları şuna: myusername@myb2ctenant.onmicrosoft.com.

```powershell
Connect-MsolService
```

Merhaba kullanacağız artık **uygulama kimliği** toodelete kullanıcılar olanak tanıyan tooassign hello uygulama hello kullanıcı hesabı yönetici rolü aşağıdaki hello komut. Bu roller, iyi bilinen tanımlayıcıları vardır, yani tüm toodo ihtiyacınız giriş, **uygulama kimliği** hello komut dosyasında aşağıdaki.

```powershell
$applicationId = "<YOUR_APPLICATION_ID>"
$sp = Get-MsolServicePrincipal -AppPrincipalId $applicationId
Add-MsolRoleMember -RoleObjectId fe930be7-5e62-47db-91af-98c3a49a38b1 -RoleMemberObjectId $sp.ObjectId -RoleMemberType servicePrincipal
```

Uygulamanızı şimdi izinleri toodelete B2C kiracınızın kullanıcılardan de vardır.

## <a name="download-configure-and-build-hello-sample-code"></a>Karşıdan yükleme, yapılandırma ve hello örnek kodu derleme
İlk olarak, hello örnek kodu indirin ve çalışmasını alın. Ardından biz yakından bakmak sürer.  Yapabilecekleriniz [hello örnek kod bir .zip dosyası olarak karşıdan](https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet/archive/master.zip). Ayrıca tercih ettiğiniz dizinine kopyalayabilirsiniz:

```
git clone https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet.git
```

Açık hello `B2CGraphClient\B2CGraphClient.sln` Visual Studio çözümü Visual Studio'da. Merhaba, `B2CGraphClient` proje, açık hello dosya `App.config`. Merhaba üç uygulama ayarlarını kendi değerlerinizle değiştirin:

```
<appSettings>
    <add key="b2c:Tenant" value="{Your Tenant Name}" />
    <add key="b2c:ClientId" value="{hello ApplicationID from above}" />
    <add key="b2c:ClientSecret" value="{hello Key from above}" />
</appSettings>
```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

Ardından, hello üzerinde sağ `B2CGraphClient` hello örnek çözümü ve yeniden oluşturma. Başarılı olursa, şimdi olmalıdır bir `B2C.exe` içinde bulunan yürütülebilir dosyasını `B2CGraphClient\bin\Debug`.

## <a name="build-user-crud-operations-by-using-hello-graph-api"></a>Kullanıcı CRUD işlemleri hello grafik API'sini kullanarak oluşturma
toouse hello B2CGraphClient, açık bir `cmd` Windows komut istemine ve dizin toohello değiştirmek `Debug` dizin. Merhaba çalıştırmak `B2C Help` komutu.

```
> cd B2CGraphClient\bin\Debug
> B2C Help
```

Bu her komut kısa bir açıklamasını görüntüler. Aşağıdaki komutlardan birini çağırma her zaman `B2CGraphClient` isteği toohello Azure AD Graph API sağlar.

### <a name="get-an-access-token"></a>Bir erişim belirteci alma
Tüm istek toohello grafik API'si bir erişim belirteci için kimlik doğrulaması gerektirir. `B2CGraphClient`kullandığı hello açık kaynak Active Directory Authentication Library (ADAL) toohelp erişim belirteci alın. ADAL belirteç edinme basit bir API sağlayarak ve erişim belirteçleri önbelleğe alma gibi bazı önemli ayrıntıları alma verdiğiniz kolaylaştırır. Toouse ADAL tooget belirteçleri, ancak yok. Ayrıca, HTTP isteklerini hazırlayın tarafından belirteç alabilir.

> [!NOTE]
> Bu kod örneği hello grafik API'si ile sipariş toocommunicate ADAL v2 kullanır.  ADAL v2 veya v3 hello Azure AD grafik API'si ile kullanılabilen sipariş tooget erişim belirteçleri kullanmanız gerekir.
> 
> 

Zaman `B2CGraphClient` çalıştırır, hello örneği oluşturur `B2CGraphClient` sınıfı. Bu sınıf için Hello Oluşturucu ADAL kimlik doğrulaması iskele kurma ayarlar:

```C#
public B2CGraphClient(string clientId, string clientSecret, string tenant)
{
    // hello client_id, client_secret, and tenant are provided in Program.cs, which pulls hello values from App.config
    this.clientId = clientId;
    this.clientSecret = clientSecret;
    this.tenant = tenant;

    // hello AuthenticationContext is ADAL's primary class, in which you indicate hello tenant toouse.
    this.authContext = new AuthenticationContext("https://login.microsoftonline.com/" + tenant);

    // hello ClientCredential is where you pass in your client_id and client_secret, which are
    // provided tooAzure AD in order tooreceive an access_token by using hello app's identity.
    this.credential = new ClientCredential(clientId, clientSecret);
}
```

Merhaba kullanacağız `B2C Get-User` bir örnek olarak komutu. Zaman `B2C Get-User` , hello CLI çağrıları hello gibi ek tüm girişleri çağrılan `B2CGraphClient.GetAllUsers(...)` yöntemi. Bu yöntemi çağırır `B2CGraphClient.SendGraphGetRequest(...)`, bir HTTP GET isteği toohello grafik API'si gönderir. Önce `B2CGraphClient.SendGraphGetRequest(...)` hello GET isteği gönderir, onu önce bir erişim ADAL kullanarak belirtecini alır:

```C#
public async Task<string> SendGraphGetRequest(string api, string query)
{
    // First, use ADAL tooacquire a token by using hello app's identity (hello credential)
    // hello first parameter is hello resource we want an access_token for; in this case, hello Graph API.
    AuthenticationResult result = authContext.AcquireToken("https://graph.windows.net", credential);

    ...

```

Bir erişim hello grafik API'si çağırma hello ADAL tarafından için belirteç sağlayabilmek için `AuthenticationContext.AcquireToken(...)` yöntemi. Ardından ADAL döndüren bir `access_token` hello uygulamanın kimliğini temsil eder.

### <a name="read-users"></a>Kullanıcıların okuma
Tooget kullanıcıların listesini istediğiniz veya belirli bir kullanıcı grafik API'si hello almak, bir HTTP gönderebilirsiniz `GET` toohello isteği `/users` uç noktası. Tüm Kiracı hello kullanıcılar için bir istek şöyle görünür:

```
GET https://graph.windows.net/contosob2c.onmicrosoft.com/users?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
```

toosee çalıştırmak, bu isteği:

 ```
 > B2C Get-User
 ```

İki önemli noktalar toonote vardır:

* Merhaba ADAL edinilen erişim belirteci toohello eklenen `Authorization` hello kullanarak üstbilgi `Bearer` düzeni.
* B2C kiracılar için hello sorgu parametresi kullanmalısınız `api-version=1.6`.

Bu ayrıntıları her ikisi de hello işlenir `B2CGraphClient.SendGraphGetRequest(...)` yöntemi:

```C#
public async Task<string> SendGraphGetRequest(string api, string query)
{
    ...

    // For B2C user management, be sure toouse hello 1.6 Graph API version.
    HttpClient http = new HttpClient();
    string url = "https://graph.windows.net/" + tenant + api + "?" + "api-version=1.6";
    if (!string.IsNullOrEmpty(query))
    {
        url += "&" + query;
    }

    // Append hello access token for hello Graph API toohello Authorization header of hello request by using hello Bearer scheme.
    HttpRequestMessage request = new HttpRequestMessage(HttpMethod.Get, url);
    request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);
    HttpResponseMessage response = await http.SendAsync(request);

    ...
```

### <a name="create-consumer-user-accounts"></a>Tüketici kullanıcı hesapları oluşturun
B2C kiracınızda kullanıcı hesapları oluştururken, bir HTTP gönderebilirsiniz `POST` toohello isteği `/users` uç noktası:

```
POST https://graph.windows.net/contosob2c.onmicrosoft.com/users?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
Content-Type: application/json
Content-Length: 338

{
    // All of these properties are required toocreate consumer users.

    "accountEnabled": true,
    "signInNames": [                            // controls which identifier hello user uses toosign in toohello account
        {
            "type": "emailAddress",             // can be 'emailAddress' or 'userName'
            "value": "joeconsumer@gmail.com"
        }
    ],
    "creationType": "LocalAccount",            // always set too'LocalAccount'
    "displayName": "Joe Consumer",                // a value that can be used for displaying toohello end user
    "mailNickname": "joec",                        // an email alias for hello user
    "passwordProfile": {
        "password": "P@ssword!",
        "forceChangePasswordNextLogin": false   // always set toofalse
    },
    "passwordPolicies": "DisablePasswordExpiration"
}
```

Bu isteği bu özelliklerin çoğu, gerekli toocreate tüketici kullanıcılardır. toolearn daha fazlasını tıklatın [burada](https://msdn.microsoft.com/library/azure/ad/graph/api/users-operations#CreateLocalAccountUser). Bu hello Not `//` açıklamaları çizim için dahil edilmiştir. Bunları, gerçek bir istekte dahil etmeyin.

toosee hello isteği, komutları aşağıdaki hello birini çalıştırın:

```
> B2C Create-User ..\..\..\usertemplate-email.json
> B2C Create-User ..\..\..\usertemplate-username.json
```

Merhaba `Create-User` komutu bir .json dosyası olarak bir giriş parametresi alır. Bu, bir kullanıcı nesnesinin bir JSON temsili içerir. Merhaba örnek kodda iki örnek .json dosyası vardır: `usertemplate-email.json` ve `usertemplate-username.json`. Bu dosyaları toosuit gereksinimlerinizi değiştirebilirsiniz. Ayrıca toohello gerekli alanları yukarıdaki, kullanabileceğiniz birkaç isteğe bağlı alanları bu dosyaları dahil edilir. Ayrıntılar hello isteğe bağlı alanları hello bulunabilir [Azure AD Graph API varlık başvurusu](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#user-entity).

Merhaba POST isteği nasıl oluşturulur görebilirsiniz `B2CGraphClient.SendGraphPostRequest(...)`.

* Bir erişim belirteci toohello iliştirir `Authorization` hello isteği üstbilgisi.
* Bu ayarlar `api-version=1.6`.
* Bu, hello hello istek gövdesinde hello JSON kullanıcı nesnesi içerir.

> [!NOTE]
> Merhaba hesapları var olan bir kullanıcı deposundan toomigrate başlangıç değerinden daha düşük parola gücünü sahip isterseniz [Azure AD B2C tarafından zorlanan güçlü parola gücünü](https://msdn.microsoft.com/library/azure/jj943764.aspx), hello kullanarakhellogüçlüparolagereksiniminidevredışıbırakabilirsiniz`DisableStrongPassword`hello değerinde `passwordPolicies` özelliği. Merhaba örneği için değiştirebileceğiniz gibi yukarıda verilen kullanıcı isteği oluşturma: `"passwordPolicies": "DisablePasswordExpiration, DisableStrongPassword"`.
> 
> 

### <a name="update-consumer-user-accounts"></a>Tüketici kullanıcı hesaplarını güncelleştirme
Kullanıcı nesneleri güncelleştirdiğinizde hello benzer toohello toocreate kullanıcı nesneleri kullandığınız işlemdir. Ancak bu işlem hello HTTP kullanan `PATCH` yöntemi:

```
PATCH https://graph.windows.net/contosob2c.onmicrosoft.com/users/<user-object-id>?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
Content-Type: application/json
Content-Length: 37

{
    "displayName": "Joe Consumer",                // this request updates only hello user's displayName
}
```

Tooupdate bir kullanıcı yeni verilerle, JSON dosyalarınızın güncelleştirerek deneyin. Daha sonra `B2CGraphClient` toorun aşağıdaki komutlardan birini:

```
> B2C Update-User <user-object-id> ..\..\..\usertemplate-email.json
> B2C Update-User <user-object-id> ..\..\..\usertemplate-username.json
```

Merhaba incelemek `B2CGraphClient.SendGraphPatchRequest(...)` yöntemi hakkında ayrıntılar için toosend bu isteği.

### <a name="search-users"></a>Kullanıcılarda arama
B2C kiracınızda çeşitli şekillerde kullanıcılar için arama yapabilirsiniz. Merhaba kullanıcının nesne kimliği veya hello kullanıcının oturum açma tanımlayıcı kullanarak iki kullanarak bir (yani, hello `signInNames` özelliği).

Belirli bir kullanıcı için komutları toosearch aşağıdaki hello birini çalıştırın:

```
> B2C Get-User <user-object-id>
> B2C Get-User <filter-query-expression>
```

Aşağıda birkaç örnek verilmiştir:

```
> B2C Get-User 2bcf1067-90b6-4253-9991-7f16449c2d91
> B2C Get-User $filter=signInNames/any(x:x/value%20eq%20%27joeconsumer@gmail.com%27)
```

### <a name="delete-users"></a>Kullanıcıları silme
Kullanıcı silme hello basit bir işlemdir. Kullanım hello HTTP `DELETE` hello yöntemi ve yapı hello URL'SİYLE düzeltmek nesne kimliği:

```
DELETE https://graph.windows.net/contosob2c.onmicrosoft.com/users/<user-object-id>?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
```

toosee bir örnek yazdırılan toohello konsol bu komut ve görünüm hello silme isteği girin:

```
> B2C Delete-User <object-id-of-user>
```

Merhaba incelemek `B2CGraphClient.SendGraphDeleteRequest(...)` yöntemi hakkında ayrıntılar için toosend bu isteği.

Toplama toouser Yönetimi'nde hello Azure AD Graph API birçok başka eylemler gerçekleştirebilir. [Azure AD Graph API Başvurusu](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) örnek istekleri yanı sıra her bir eylemde ayrıntıları sağlar.

## <a name="use-custom-attributes"></a>Özel öznitelikler kullanma
Çoğu tüketici uygulamaları herhangi bir tür özel kullanıcı profili bilgilerini toostore gerekir. Bunu yapmak için bir toodefine B2C kiracınızın özel bir öznitelikte yoludur. Ardından bu özniteliği hello davranabilirsiniz aynı şekilde bir kullanıcı nesnesi üzerinde herhangi bir özellik işle. Merhaba özniteliği güncelleştirebilir Sil hello özniteliğinin, sorgu hello özniteliği tarafından hello özniteliği ve oturum açma belirteçleri talep olarak gönder.

toodefine B2C kiracınızın özel bir öznitelikte bkz hello [B2C özel öznitelik başvurusu](active-directory-b2c-reference-custom-attr.md).

B2C kiracınızda kullanarak tanımlanan özel özniteliklere hello görüntüleyebilirsiniz `B2CGraphClient`:

```
> B2C Get-B2C-Application
> B2C Get-Extension-Attribute <object-id-in-the-output-of-the-above-command>
```

Bu işlevlerin Hello çıktı gibi her özel özniteliğinin hello ayrıntıları ortaya çıkarır:

```JSON
{
      "odata.type": "Microsoft.DirectoryServices.ExtensionProperty",
      "objectType": "ExtensionProperty",
      "objectId": "cec6391b-204d-42fe-8f7c-89c2b1964fca",
      "deletionTimestamp": null,
      "appDisplayName": "",
      "name": "extension_55dc0861f9a44eb999e0a8a872204adb_Jersey_Number",
      "dataType": "Integer",
      "isSyncedFromOnPremises": false,
      "targetObjects": [
        "User"
      ]
}
```

Hello gibi tam adı kullanabilirsiniz `extension_55dc0861f9a44eb999e0a8a872204adb_Jersey_Number`, kullanıcı nesneleri bir özellik olarak.  Merhaba yeni özellik ve hello özelliği için bir değer ile .json dosyanızı güncelleştirin ve ardından çalıştırın:

```
> B2C Update-User <object-id-of-user> <path-to-json-file>
```

Kullanarak `B2CGraphClient`, B2C Kiracı kullanıcılarınızın program aracılığıyla yönetebilen bir hizmet uygulaması sahip. `B2CGraphClient`kendi uygulama kimliği tooauthenticate toohello Azure AD Graph API kullanır. Ayrıca, istemci parolasını kullanarak belirteçleri da alır. Bu işlev uygulamanıza dahil, B2C uygulamalar için birkaç önemli nokta unutmayın:

* Toogrant hello uygulama hello uygun izinleri hello Kiracı gerekir.
* Şimdilik, toouse ADAL (değil MSAL) tooget erişim belirteçleri gerekir. (Ayrıca protokol iletilerini doğrudan bir kitaplık kullanılarak olmadan gönderebilirsiniz.)
* Merhaba grafik API'si çağırdığınızda, kullanabilirsiniz `api-version=1.6`.
* Oluşturduğunuzda ve tüketici kullanıcıları güncelleştirmek birkaç özelliği yukarıda açıklandığı gibi gereklidir.

Herhangi bir sorunuz veya Eylemler tooperform hello grafik API'sini kullanarak istediğiniz istekleri varsa B2C kiracınızın bu makalede bir yorum yazın veya bir sorunu hello GitHub kod örnek deposunda dosya.

