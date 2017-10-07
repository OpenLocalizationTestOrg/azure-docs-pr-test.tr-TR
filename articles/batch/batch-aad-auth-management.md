---
title: "aaaUse Azure Active Directory tooauthenticate toplu yönetim çözümleri | Microsoft Docs"
description: "Uygulamaları Azure resource manager ile oluşturulmuş ve hello toplu kaynak sağlayıcısı Azure AD ile kimlik doğrulaması."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/27/2017
ms.author: tamram
ms.openlocfilehash: 192aa9f8d7cbfc0282a4a0c33ab1659f1f351525
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-batch-management-solutions-with-active-directory"></a>Toplu işlem yönetimi çözümleri Active Directory ile kimlik doğrulaması

Hello Azure toplu işlem yönetimi hizmeti çağıran uygulamalar kimlik doğrulaması ile [Azure Active Directory] [ aad_about] (Azure AD). Azure AD, Microsoft'un çok kiracılı bulut tabanlı dizin ve Kimlik Yönetimi Hizmeti ' dir. Azure kendisini müşteriler, hizmet yöneticileri ve kuruluş kullanıcılarının hello kimlik doğrulaması için Azure AD kullanır.

Merhaba Batch yönetimi .NET kitaplığı, Batch hesaplarını, hesabı anahtarları, uygulamalar ve uygulama paketleri ile çalışmak için türü ortaya çıkarır. Merhaba Batch yönetimi .NET kitaplığı bir Azure kaynak sağlayıcısı istemci ve ile birlikte kullanılan [Azure Resource Manager] [ resman_overview] toomanage bu kaynakları programlı olarak. Azure AD olduğu ve hello Batch yönetimi .NET kitaplığı dahil olmak üzere tüm Azure kaynak sağlayıcısı istemci aracılığıyla yapılan gerekli tooauthenticate istekleri [Azure Resource Manager][resman_overview].

Bu makalede, Azure AD tooauthenticate hello Batch yönetimi .NET kitaplığını kullanan uygulamalardan kullanarak keşfedin. Azure AD toouse tooauthenticate Abonelik Yöneticisi veya ortak yönetici, kullanarak kimlik doğrulaması nasıl tümleşik gösterir. Merhaba kullanırız [AccountManagment] [ acct_mgmt_sample] örnek proje, github'da Azure AD ile Merhaba Batch yönetimi .NET kitaplığını kullanarak aracılığıyla toowalk kullanılabilir.

Merhaba Batch yönetimi .NET kitaplığı ve hello AccountManagement örnek, kullanma hakkında daha fazla toolearn bkz [yönetmek Batch hesaplarını ve kotalarını hello Batch Yönetimi istemci kitaplığı için .NET ile](batch-management-dotnet.md).

## <a name="register-your-application-with-azure-ad"></a>Azure AD ile uygulamanızı kaydetme

Hello Azure [Active Directory kimlik doğrulama Kitaplığı] [ aad_adal] (ADAL) kullanmak için AD uygulamalarınız içinde bir programlama arabirimidir tooAzure sağlar. ADAL toocall uygulamanızdan bir Azure AD kiracısında uygulamanızı kaydetmeniz gerekir. Uygulamanızı kaydederken hello Azure AD kiracısı içinde bir ad da dahil olmak üzere uygulamanız hakkındaki bilgilerle Azure AD sağlayın. Ardından Azure AD uygulama kimliği sağlar çalışma zamanında Azure AD ile uygulamanızı tooassociate kullanın. toolearn hello uygulama kimliği hakkında daha fazla bilgi görmek [uygulama ve hizmet asıl nesneler Azure Active Directory'de](../active-directory/develop/active-directory-application-objects.md).

tooregister hello AccountManagement örnek uygulama izleyin hello hello adımlarda [bir uygulama ekleme](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) bölümüne [uygulamaları Azure Active Directory ile tümleştirme] [ aad_integrate]. Belirtin **yerel istemci uygulaması** hello tür bir uygulama için. Merhaba endüstri hello standart OAuth 2.0 URI'sini **yeniden yönlendirme URI'si** olan `urn:ietf:wg:oauth:2.0:oob`. Ancak, geçerli bir URI belirtebilirsiniz (gibi `http://myaccountmanagementsample`) hello için **yeniden yönlendirme URI'si**toobe gerçek bir uç noktası gerekmez gibi:

![](./media/batch-aad-auth-management/app-registration-management-plane.png)

Merhaba kayıt işlemini tamamladıktan sonra hello uygulama kimliği görebilir ve uygulamanız için listelenen nesne (hizmet sorumlusu) kimliği hello.  

![](./media/batch-aad-auth-management/app-registration-client-id.png)

## <a name="grant-hello-azure-resource-manager-api-access-tooyour-application"></a>Merhaba Azure Kaynak Yöneticisi API'si erişim tooyour uygulaması verin

Ardından, toodelegate erişim tooyour uygulama toohello Azure Kaynak Yöneticisi API'si gerekir. Merhaba Resource Manager API Hello Azure AD tanımlayıcısıdır **Windows Azure Hizmet Yönetimi API'si**.

Hello Azure Portalı'nda aşağıdaki adımları izleyin:

1. Merhaba sol gezinti bölmesinde hello Azure portal'ı seçin **daha Hizmetleri**, tıklatın **uygulama kayıtlar**, tıklatıp **Ekle**.
2. Merhaba listesinde uygulamanızın uygulama kayıtların hello adını arayın:

    ![Uygulama adınız arayın](./media/batch-aad-auth-management/search-app-registration.png)

3. Görüntü hello **ayarları** dikey. Merhaba, **API erişimini** bölümünde, select **gerekli izinleri**.
4. Tıklatın **Ekle** tooadd yeni gerekli izni. 
5. 1. adımda girin **Windows Azure Hizmet Yönetimi API'si**, bu API hello sonuçları listesinden seçin ve hello tıklatın **seçin** düğmesi.
6. 2. adımda seç onay kutusunu sonraki çok hello**erişim Azure Klasik dağıtım modeli kuruluş kullanıcılar olarak**, hello tıklatıp **seçin** düğmesi.
7. Merhaba tıklatın **Bitti** düğmesi.

Merhaba **gerekli izinler** ADAL ve Resource Manager API'leri izinleri tooyour uygulama tooboth verilen gösterir hello artık dikey. Uygulamanızı Azure AD ile ilk kez kaydederken izinleri tooADAL varsayılan olarak verilir.

![Temsilci izinleri toohello Azure Kaynak Yöneticisi API'si](./media/batch-aad-auth-management/required-permissions-management-plane.png)

## <a name="azure-ad-endpoints"></a>Azure AD uç noktaları

tooauthenticate, toplu yönetimini çözümleriniz Azure AD ile iyi bilinen iki uç nokta gerekir.

- Merhaba **Azure AD ortak uç nokta** belirli bir kiracı sağlanmadığında tümleşik kimlik doğrulaması hello durumda olduğu gibi arabirimi toplama genel bir kimlik bilgisi sağlanır:

    `https://login.microsoftonline.com/common`

- Merhaba **Azure Kaynak Yöneticisi uç noktası** kullanılan tooacquire istekleri toohello toplu yönetim hizmeti kimlik doğrulaması için bir belirteçtir:

    `https://management.core.windows.net/`

Merhaba AccountManagement örnek uygulama Bu uç noktalar için sabitleri tanımlar. Bu sabitleri değiştirmeden bırakın:

```csharp
// Azure Active Directory "common" endpoint.
private const string AuthorityUri = "https://login.microsoftonline.com/common";
// Azure Resource Manager endpoint 
private const string ResourceUri = "https://management.core.windows.net/";
```

## <a name="reference-your-application-id"></a>Uygulama Kimliğinizi başvurusu 

İstemci uygulamanızı çalışma zamanında hello uygulama kimliği (Ayrıca başvurulan tooas hello istemci kimliği) tooaccess Azure AD kullanır. Hello Azure portal, uygulamanızın kaydedildikten sonra kayıtlı uygulamanız için Azure AD tarafından sağlanan kod toouse hello uygulama Kimliğinizi güncelleştirin. Hello AccountManagement örnek uygulama, uygulama Kimliğiniz hello Azure portal toohello uygun sabiti kopyalayın:

```csharp
// Specify hello unique identifier (hello "Client ID") for your application. This is required so that your
// native client application (i.e. this sample) can access hello Microsoft Azure AD Graph API. For information
// about registering an application in Azure Active Directory, please see "Adding an Application" here:
// https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/
private const string ClientId = "<application-id>";
```
Ayrıca hello yeniden yönlendirme hello kayıt işlemi sırasında belirtilen URI'sini kopyalayın. Merhaba yeniden yönlendirme URI'si kodunuzda belirtilen hello yeniden yönlendirme Merhaba uygulaması kaydolurken sağladığınız URI eşleşmesi gerekir.

```csharp
// hello URI toowhich Azure AD will redirect in response tooan OAuth 2.0 request. This value is
// specified by you when you register an application with AAD (see ClientId comment). It does not
// need toobe a real endpoint, but must be a valid URI (e.g. https://accountmgmtsampleapp).
private const string RedirectUri = "http://myaccountmanagementsample";
```

## <a name="acquire-an-azure-ad-authentication-token"></a>Azure AD kimlik doğrulama belirtecini alma

Merhaba AccountManagement örnek hello Azure AD kiracısında kaydetmek ve değerleri ile Merhaba örnek kaynak kodunu güncelleştirin sonra hello Azure AD kullanarak hazır tooauthenticate örnektir. Merhaba örneği çalıştırdığınızda, hello ADAL tooacquire kimlik doğrulama belirtecini çalışır. Bu adımda, Microsoft kimlik bilgilerinizi ister: 

```csharp
// Obtain an access token using hello "common" AAD resource. This allows hello application
// tooquery AAD for information that lies outside hello application's tenant (such as for
// querying subscription information in your Azure account).
AuthenticationContext authContext = new AuthenticationContext(AuthorityUri);
AuthenticationResult authResult = authContext.AcquireToken(ResourceUri,
                                                        ClientId,
                                                        new Uri(RedirectUri),
                                                        PromptBehavior.Auto);
```

Kimlik bilgilerinizi sağlayın sonra hello örnek uygulama kimliği doğrulanmış tooissue istekleri toohello toplu yönetim hizmeti geçebilirsiniz. 

## <a name="next-steps"></a>Sonraki adımlar

Merhaba çalıştırma hakkında daha fazla bilgi için [AccountManagement örnek uygulama][acct_mgmt_sample], bkz: [yönetmek Batch hesaplarını ve kotalarını hello Batch Yönetimi istemci kitaplığı için .NETile](batch-management-dotnet.md).

Azure AD hakkında daha fazla toolearn bkz hello [Azure Active Directory belgeleri](https://docs.microsoft.com/azure/active-directory/). Nasıl toouse ADAL kullanılabilir hello gösteren ayrıntılı örnekler [Azure Kod örnekleri](https://azure.microsoft.com/resources/samples/?service=active-directory) kitaplığı.

Azure AD kullanarak tooauthenticate Batch hizmeti uygulamaları bkz [Active Directory ile kimlik doğrulaması toplu hizmet çözümlerine](batch-aad-auth.md). 


[aad_about]: ../active-directory/active-directory-whatis.md "Azure Active Directory nedir?"
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Azure AD için kimlik doğrulama senaryoları"
[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Uygulamaları Azure Active Directory ile tümleştirme"
[acct_mgmt_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/AccountManagement
[azure_portal]: http://portal.azure.com
[resman_overview]: ../azure-resource-manager/resource-group-overview.md
