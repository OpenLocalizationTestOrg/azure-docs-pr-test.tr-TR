---
title: "aaaUse Azure Active Directory tooauthenticate Azure Batch hizmeti çözümleri | Microsoft Docs"
description: "Toplu Azure AD hello Batch hizmeti kimlik doğrulamasını destekler."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/20/2017
ms.author: tamram
ms.openlocfilehash: 6c825c30f1c80bb059a797a2e78367e599acd109
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-batch-service-solutions-with-active-directory"></a>Toplu hizmet çözümlerine Active Directory ile kimlik doğrulaması

Azure Batch destekleyen kimlik doğrulama ile [Azure Active Directory] [ aad_about] (Azure AD). Azure AD, Microsoft'un çok kiracılı bulut tabanlı dizin ve Kimlik Yönetimi Hizmeti ' dir. Azure kendisi, müşteriler, hizmet yöneticileri ve kuruluş kullanıcıları Azure AD tooauthenticate kullanır.

Azure AD kimlik doğrulaması ile Azure Batch kullanırken, aşağıdaki iki yöntemden biriyle doğrulayabilir:

- Kullanarak **tümleşik kimlik doğrulaması** tooauthenticate hello uygulama ile etkileşim bir kullanıcı. Tümleşik kimlik doğrulaması kullanarak bir uygulamayı bir kullanıcının kimlik bilgilerini toplar ve bu kimlik bilgileri tooauthenticate erişim tooBatch kaynakları kullanır.
- Kullanarak bir **hizmet sorumlusu** tooauthenticate katılımsız bir uygulama. Bir hizmet sorumlusu hello İlkesi ve bir uygulama için izinler çalışma zamanında kaynaklara erişirken sipariş toorepresent hello uygulamada tanımlar.

Azure AD hakkında daha fazla toolearn bkz hello [Azure Active Directory belgeleri](https://docs.microsoft.com/azure/active-directory/).

## <a name="authentication-and-pool-allocation-mode"></a>Kimlik doğrulama ve havuzu ayırma modu

Bir toplu işlem hesabı oluşturduğunuzda, o hesap için oluşturulan havuzlarının burada ayrılmalıdır belirtebilirsiniz. Merhaba varsayılan Batch hizmeti aboneliğiniz veya bir kullanıcı abonelik tooallocate havuzları seçebilirsiniz. Tercih ettiğiniz bu hesaptaki erişim tooresources nasıl kimlik doğrulaması etkiler.

- **Batch hizmeti abonelik**. Varsayılan olarak, bir toplu işlem hizmeti abonelikte Batch havuzları ayrılır. Bu seçeneği seçerseniz, size bu hesaptaki erişim tooresources ile ya da doğrulayabilir [paylaşılan anahtar](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service) veya Azure AD ile.
- **Kullanıcı aboneliği.** Batch havuzları, belirttiğiniz bir kullanıcı aboneliği tooallocate seçebilirsiniz. Bu seçeneği seçerseniz, Azure AD ile kimlik doğrulaması gerekir.

## <a name="endpoints-for-authentication"></a>Kimlik doğrulaması için uç noktalar

Azure AD ile tooauthenticate toplu iş uygulamaları, gereksinim duyduğunuz tooinclude kodunuzda iyi bilinen bazı uç noktaları.

### <a name="azure-ad-endpoint"></a>Azure AD uç noktası

Merhaba temel Azure AD yetkilisi uç noktası:

`https://login.microsoftonline.com/`

Azure AD ile tooauthenticate, bu uç noktaya hello Kiracı kimliği (dizin kimliği) ile birlikte kullanın. Merhaba Kiracı kimliği hello Azure AD Kiracı toouse kimlik doğrulaması için tanımlar. tooretrieve Kiracı kimliği Merhaba, özetlenen hello adımları [hello Kiracı Kimliği almak için Azure Active Directory'yi](#get-the-tenant-id-for-your-active-directory):

`https://login.microsoftonline.com/<tenant-id>`

> [!NOTE] 
> bir hizmet sorumlusunu kullanarak kimlik doğrulaması sırasında hello Kiracı özgü uç noktası gereklidir. 
> 
> tümleşik kimlik doğrulaması kullanarak kimlik doğrulaması sırasında isteğe bağlıdır, ancak önerilen Hello Kiracı özgü uç noktadır. Ancak, hello Azure AD ortak uç nokta de kullanabilirsiniz. Merhaba ortak uç nokta belirli bir kiracı sağlanmadığında arabirimi toplama genel bir kimlik bilgisi sağlanır. Merhaba ortak uç noktası `https://login.microsoftonline.com/common`.
>
>

Azure AD uç noktaları hakkında daha fazla bilgi için bkz: [Azure AD için kimlik doğrulama senaryoları][aad_auth_scenarios].

### <a name="batch-resource-endpoint"></a>Batch kaynak uç noktası

Kullanım hello **Azure Batch kaynak endpoint** tooacquire kimlik doğrulaması için bir belirteç isteklerini toohello Batch hizmeti:

`https://batch.core.windows.net/`

## <a name="register-your-application-with-a-tenant"></a>Bir kiracı ile uygulamanızı kaydetme

Azure AD tooauthenticate kullanarak hello ilk adımı uygulamanız bir Azure AD kiracısında kaydediyor. Uygulamanızı kaydetme sağlar toocall hello Azure [Active Directory kimlik doğrulama Kitaplığı] [ aad_adal] (ADAL) kodunuzdan. Merhaba ADAL uygulamanızdan Azure AD ile kimlik doğrulaması için bir API sağlar. Uygulamanızı kaydetme toouse tümleşik kimlik doğrulaması veya bir hizmet sorumlusu planlama olup olmadığını gereklidir.

Uygulamanızı kaydederken, uygulama tooAzure AD hakkında bilgi sağlayın. Ardından Azure AD uygulama kimliği sağlar çalışma zamanında Azure AD ile uygulamanızı tooassociate kullanın. toolearn hello uygulama kimliği hakkında daha fazla bilgi görmek [uygulama ve hizmet asıl nesneler Azure Active Directory'de](../active-directory/develop/active-directory-application-objects.md).

tooregister toplu uygulamanızı hello adımları hello içinde [bir uygulama ekleme](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) bölümüne [uygulamaları Azure Active Directory ile tümleştirme][aad_integrate]. Yerel bir uygulama olarak, uygulamanızın kaydolursanız, hello için geçerli bir URI belirtebilirsiniz **yeniden yönlendirme URI'si**. Toobe gerçek bir uç noktası gerekmez.

Uygulamanızı kaydınız sonra hello uygulama kimliği görürsünüz:

![Batch uygulamanızı Azure AD ile kaydetme](./media/batch-aad-auth/app-registration-data-plane.png)

Uygulama Azure AD ile kaydetme hakkında daha fazla bilgi için bkz: [Azure AD için kimlik doğrulama senaryoları](../active-directory/develop/active-directory-authentication-scenarios.md).

## <a name="get-hello-tenant-id-for-your-active-directory"></a>Active Directory için Hello Kiracı Kimliğinizi alma

Merhaba Kiracı kimliği, kimlik doğrulama hizmetleri tooyour uygulamanın sağladığı hello Azure AD kiracısı tanımlar. tooget Kiracı kimliği Merhaba, şu adımları izleyin:

1. Hello Azure portal, Active Directory seçin.
2. **Özellikler**'e tıklayın.
3. Merhaba dizin kimliği için sağlanan hello GUID değeri kopyalayın Bu değer hello Kiracı kimliği olarak da adlandırılır

![Merhaba dizin Kimliğini kopyalayın](./media/batch-aad-auth/aad-directory-id.png)


## <a name="use-integrated-authentication"></a>Tümleşik kimlik doğrulamasını kullan

tooauthenticate ile tümleşik kimlik doğrulaması, uygulama izinleri tooconnect toohello Batch hizmeti API'si toogrant gerekir. Bu adım, uygulama tooauthenticate çağrıları toohello Batch hizmeti API'si Azure AD ile sağlar.

Seçtiğiniz sonra [uygulamanızı kayıtlı](#register-your-application-with-an-azure-ad-tenant), hello toohello Batch hizmeti erişim Azure portalı toogrant'nda aşağıdaki adımları izleyin:

1. Merhaba sol gezinti bölmesinde hello Azure portal'ı seçin **daha Hizmetleri**, tıklatın **uygulama kayıtlar**.
2. Merhaba listesinde uygulamanızın uygulama kayıtların hello adını arayın:

    ![Uygulama adınız arayın](./media/batch-aad-auth/search-app-registration.png)

3. Açık hello **ayarları** dikey penceresinde uygulamanız için. Merhaba, **API erişimini** bölümünde, select **gerekli izinleri**.
4. Hello içinde **gerekli izinleri** dikey penceresinde hello tıklatın **Ekle** düğmesi.
5. 1. adımda toplu API hello için arama yapın. Arama hello API bulana kadar bu dizelerin her biri için:
    1. **MicrosoftAzureBatch**.
    2. **Microsoft Azure Batch**. Daha yeni Azure AD kiracıları bu adı kullanıyor olabilir.
    3. **ddbf3205-c6bd-46ae-8127-60eb93363864** hello toplu API hello kimliğidir. 
6. Merhaba toplu API bulduktan sonra onu seçin ve hello tıklatın **seçin** düğmesi.
6. 2. adımda seç onay kutusunu sonraki çok hello**erişim Azure Batch hizmeti** hello tıklatıp **seçin** düğmesi.
7. Merhaba tıklatın **Bitti** düğmesi.

Merhaba **gerekli izinler** tooboth ADAL erişmek ve toplu işlem hizmeti API'si Merhaba, Azure AD uygulaması yok gösterir artık dikey. Uygulamanızı Azure AD ile ilk kez kaydederken izinleri tooADAL otomatik olarak verilir.

![GRANT API izinleri](./media/batch-aad-auth/required-permissions-data-plane.png)

## <a name="use-a-service-principal"></a>Bir hizmet sorumlusu kullanın 

tooauthenticate katılımsız çalışan bir uygulama, bir hizmet sorumlusu kullanın. Uygulamanızı kaydınız sonra hello Azure portal tooconfigure bir hizmet sorumlusu'nda aşağıdaki adımları izleyin:

1. Uygulamanız için gizli bir anahtar isteyin.
2. RBAC rolü tooyour uygulama atama.

### <a name="request-a-secret-key-for-your-application"></a>Uygulamanız için gizli bir anahtarı iste

Uygulamanızın hizmet sorumlusuyla kimlik doğruladığında, hello uygulama kimliği ve gizli anahtar tooAzure AD gönderir. Toocreate ihtiyacınız ve kodunuzdan hello gizli anahtar toouse kopyalayın.

Hello Azure Portalı'nda aşağıdaki adımları izleyin:

1. Merhaba sol gezinti bölmesinde hello Azure portal'ı seçin **daha Hizmetleri**, tıklatın **uygulama kayıtlar**.
2. Merhaba listesinde uygulamanızın uygulama kayıtların hello adını arayın.
3. Görüntü hello **ayarları** dikey. Merhaba, **API erişimini** bölümünde, select **anahtarları**.
4. toocreate bir anahtar hello anahtarı için bir açıklama girin. Ardından bir veya iki yıllık hello anahtarı için bir süre seçin. 
5. Hello tıklatın **kaydetmek** düğmesini toocreate ve başlangıç anahtarı görüntüler. Mümkün tooaccess olmayacak şekilde hello anahtar değeri tooa güvenli bir yerde, kopyalayın, sonra yeniden bırakın hello dikey. 

    ![Gizli bir anahtar oluşturun](./media/batch-aad-auth/secret-key.png)

### <a name="assign-an-rbac-role-tooyour-application"></a>RBAC rolü tooyour uygulama atama

tooauthenticate bir hizmet asıl tooassign RBAC rolü tooyour uygulama gerekir. Şu adımları uygulayın:

1. Hello Azure portal, uygulamanız tarafından kullanılan toohello toplu işlem hesabı gidin.
2. Merhaba, **ayarları** dikey penceresinde hello toplu işlem hesabı için select **erişim denetimi (IAM)**.
3. Merhaba tıklatın **Ekle** düğmesi. 
4. Merhaba gelen **rol** açılan listesinde, her iki hello seçin _katkıda bulunan_ veya _okuyucu_ rolü uygulamanız için. Bu rolleri hakkında daha fazla bilgi için bkz: [hello Azure portal'ın rol tabanlı erişim denetimi ile çalışmaya başlama](../active-directory/role-based-access-control-what-is.md).  
5. Merhaba, **seçin** alanında, uygulamanızın hello adını girin. Uygulamanızı hello listeden seçin ve tıklatın **kaydetmek**.

Uygulamanız artık bir RBAC rolü atanmış erişim denetimi ayarlarınızda görünmelidir. 

![RBAC rolü tooyour uygulama atama](./media/batch-aad-auth/app-rbac-role.png)

### <a name="get-hello-tenant-id-for-your-azure-active-directory"></a>Azure Active Directory için Hello Kiracı Kimliğinizi alma

Merhaba Kiracı kimliği, kimlik doğrulama hizmetleri tooyour uygulamanın sağladığı hello Azure AD kiracısı tanımlar. tooget Kiracı kimliği Merhaba, şu adımları izleyin:

1. Hello Azure portal, Active Directory seçin.
2. **Özellikler**'e tıklayın.
3. Merhaba dizin kimliği için sağlanan hello GUID değeri kopyalayın Bu değer hello Kiracı kimliği olarak da adlandırılır

![Merhaba dizin Kimliğini kopyalayın](./media/batch-aad-auth/aad-directory-id.png)


## <a name="code-examples"></a>Kod örnekleri

Bu bölümdeki Hello kod örnekleri tooauthenticate kullanarak Azure AD ile tümleşik kimlik doğrulaması nasıl ve bir hizmet sorumlusu gösterir. Bu kod örnekleri .NET kullanır, ancak hello kavramları diğer diller için benzerdir.

> [!NOTE]
> Azure AD kimlik doğrulama belirtecini bir saat sonra süresi dolar. Bir uzun süreli kullanırken **BatchClient** nesnesi, bir belirteç almak öneririz ADAL her isteği tooensure özelliğini, her zaman geçerli bir belirteci vardır. 
>
>
> tooachieve bu .NET yazma bir yöntemi alır Azure AD'den belirteci hello ve bu yöntem tooa geçirin **BatchTokenCredentials** temsilci olarak nesne. Geçerli bir belirteci sağlanan her isteği toohello Batch hizmeti tooensure üzerinde Hello temsilci yöntemi çağrılır. Yeni bir belirteç Azure AD'den alınan için varsayılan olarak ADAL belirteçleri, önbelleğe alır. yalnızca gerekli olduğunda. Azure AD'de belirteçleri hakkında daha fazla bilgi için bkz: [Azure AD için kimlik doğrulama senaryoları][aad_auth_scenarios].
>
>

### <a name="code-example-using-azure-ad-integrated-authentication-with-batch-net"></a>Kod örneği: Batch .NET ile tümleşik kimlik doğrulaması Azure AD kullanma

Batch .NET, başvuru hello tümleşik kimlik doğrulamasını ile tooauthenticate [Azure Batch .NET](https://www.nuget.org/packages/Azure.Batch/) paket ve hello [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) paket.

Merhaba şunlar `using` deyimlerinde kodunuzu:

```csharp
using Microsoft.Azure.Batch;
using Microsoft.Azure.Batch.Auth;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

Başvuru hello Azure AD endpoint hello dahil olmak üzere, kodunuzda Kiracı kimliği. tooretrieve Kiracı kimliği Merhaba, özetlenen hello adımları [hello Kiracı Kimliği almak için Azure Active Directory'yi](#get-the-tenant-id-for-your-active-directory):

```csharp
private const string AuthorityUri = "https://login.microsoftonline.com/<tenant-id>";
```

Başvuru hello Batch hizmeti kaynak uç noktası:

```csharp
private const string BatchResourceUri = "https://batch.core.windows.net/";
```

Batch hesabınıza başvurusu:

```csharp
private const string BatchAccountUrl = "https://myaccount.mylocation.batch.azure.com";
```

Uygulamanız için Hello uygulama kimliği (istemci kimliği) belirtin. Merhaba uygulama kimliği uygulama kaydınızı hello Azure portalı içinde kullanılabilir:

```csharp
private const string ClientId = "<application-id>";
```

Ayrıca hello yeniden yönlendirme hello kayıt işlemi sırasında belirtilen URI'sini kopyalayın. Merhaba yeniden yönlendirme URI'si kodunuzda belirtilen hello yeniden yönlendirme Merhaba uygulaması kaydolurken sağladığınız URI eşleşmesi gerekir:

```csharp
private const string RedirectUri = "http://mybatchdatasample";
```

Bir geri çağırma yöntemi tooacquire hello kimlik doğrulama belirteci Azure AD'den yazma. Merhaba **GetAuthenticationTokenAsync** burada gösterilen geri çağırma yöntemi hello uygulama ile etkileşim bir kullanıcı ADAL tooauthenticate çağırır. Merhaba **AcquireTokenAsync** yöntemi tarafından ADAL istemleri kullanıcı kimlik bilgilerinin hello ve Merhaba uygulaması ilerler kez hello kullanıcı sağlanan sağlar bunları (Bu zaten kimlik bilgilerini önbelleğe sürece):

```csharp
public static async Task<string> GetAuthenticationTokenAsync()
{
    var authContext = new AuthenticationContext(AuthorityUri);

    // Acquire hello authentication token from Azure AD.
    var authResult = await authContext.AcquireTokenAsync(BatchResourceUri, 
                                                        ClientId, 
                                                        new Uri(RedirectUri), 
                                                        new PlatformParameters(PromptBehavior.Auto));

    return authResult.AccessToken;
}
```

Oluşturmak bir **BatchTokenCredentials** hello temsilcisi bir parametre olarak alan nesne. Bu kimlik bilgileri tooopen kullanan bir **BatchClient** nesnesi. Kullanan **BatchClient** nesne hello Batch hizmeti karşı sonraki işlemleri için:

```csharp
public static async Task PerformBatchOperations()
{
    Func<Task<string>> tokenProvider = () => GetAuthenticationTokenAsync();

    using (var client = await BatchClient.OpenAsync(new BatchTokenCredentials(BatchAccountUrl, tokenProvider)))
    {
        await client.JobOperations.ListJobs().ToListAsync();
    }
}
```

### <a name="code-example-using-an-azure-ad-service-principal-with-batch-net"></a>Kod örneği: Azure AD hizmet sorumlusu Batch .NET ile kullanma

Batch .NET, başvuru hello alanından bir hizmet asıl tooauthenticate [Azure Batch .NET](https://www.nuget.org/packages/Azure.Batch/) paket ve hello [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) paket.

Merhaba şunlar `using` deyimlerinde kodunuzu:

```csharp
using Microsoft.Azure.Batch;
using Microsoft.Azure.Batch.Auth;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

Başvuru hello Azure AD endpoint hello dahil olmak üzere, kodunuzda Kiracı kimliği. Bir hizmet sorumlusu kullanırken, bir kiracı özel uç noktası sağlamanız gerekir. tooretrieve Kiracı kimliği Merhaba, özetlenen hello adımları [hello Kiracı Kimliği almak için Azure Active Directory'yi](#get-the-tenant-id-for-your-active-directory):

```csharp
private const string AuthorityUri = "https://login.microsoftonline.com/<tenant-id>";
```

Başvuru hello Batch hizmeti kaynak uç noktası:  

```csharp
private const string BatchResourceUri = "https://batch.core.windows.net/";
```

Batch hesabınıza başvurusu:

```csharp
private const string BatchAccountUrl = "https://myaccount.mylocation.batch.azure.com";
```

Uygulamanız için Hello uygulama kimliği (istemci kimliği) belirtin. Merhaba uygulama kimliği uygulama kaydınızı hello Azure portalı içinde kullanılabilir:

```csharp
private const string ClientId = "<application-id>";
```

Azure portal hello kopyalanan hello gizli anahtarı belirtin:

```csharp
private const string ClientKey = "<secret-key>";
```

Bir geri çağırma yöntemi tooacquire hello kimlik doğrulama belirteci Azure AD'den yazma. Merhaba **GetAuthenticationTokenAsync** katılımsız kimlik doğrulaması için ADAL çağrıları burada gösterilen geri çağırma yöntemi:

```csharp
public static async Task<string> GetAuthenticationTokenAsync()
{
    AuthenticationContext authContext = new AuthenticationContext(AuthorityUri);
    AuthenticationResult authResult = await authContext.AcquireTokenAsync(BatchResourceUri, new ClientCredential(ClientId, ClientKey));

    return authResult.AccessToken;
}
```

Oluşturmak bir **BatchTokenCredentials** hello temsilcisi bir parametre olarak alan nesne. Bu kimlik bilgileri tooopen kullanan bir **BatchClient** nesnesi. Ardından, kullanabileceğiniz **BatchClient** nesne hello Batch hizmeti karşı sonraki işlemleri için:

```csharp
public static async Task PerformBatchOperations()
{
    Func<Task<string>> tokenProvider = () => GetAuthenticationTokenAsync();

    using (var client = await BatchClient.OpenAsync(new BatchTokenCredentials(BatchAccountUrl, tokenProvider)))
    {
        await client.JobOperations.ListJobs().ToListAsync();
    }
}
```

## <a name="next-steps"></a>Sonraki adımlar

Azure AD hakkında daha fazla toolearn bkz hello [Azure Active Directory belgeleri](https://docs.microsoft.com/azure/active-directory/). Nasıl toouse ADAL kullanılabilir hello gösteren ayrıntılı örnekler [Azure Kod örnekleri](https://azure.microsoft.com/resources/samples/?service=active-directory) kitaplığı.

Hizmet sorumluları hakkında daha fazla toolearn bkz [uygulama ve hizmet asıl nesneler Azure Active Directory'de](../active-directory/develop/active-directory-application-objects.md). kullanarak bir hizmet asıl toocreate hello Azure portal, bkz: [portal toocreate Active Directory Uygulama ve kaynaklarına erişebilir hizmet sorumlusu kullanmak](../resource-group-create-service-principal-portal.md). Bir hizmet sorumlusu, PowerShell veya Azure CLI ile de oluşturabilirsiniz. 

Azure AD kullanarak tooauthenticate toplu yönetim uygulamaları bkz [Active Directory ile kimlik doğrulaması toplu yönetim çözümleri](batch-aad-auth-management.md). 

[aad_about]: ../active-directory/active-directory-whatis.md "Azure Active Directory nedir?"
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Azure AD için kimlik doğrulama senaryoları"
[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Uygulamaları Azure Active Directory ile tümleştirme"
[azure_portal]: http://portal.azure.com
