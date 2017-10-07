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
# <a name="authenticate-batch-management-solutions-with-active-directory"></a><span data-ttu-id="29381-103">Toplu işlem yönetimi çözümleri Active Directory ile kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="29381-103">Authenticate Batch Management solutions with Active Directory</span></span>

<span data-ttu-id="29381-104">Hello Azure toplu işlem yönetimi hizmeti çağıran uygulamalar kimlik doğrulaması ile [Azure Active Directory] [ aad_about] (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="29381-104">Applications that call hello Azure Batch Management service authenticate with [Azure Active Directory][aad_about] (Azure AD).</span></span> <span data-ttu-id="29381-105">Azure AD, Microsoft'un çok kiracılı bulut tabanlı dizin ve Kimlik Yönetimi Hizmeti ' dir.</span><span class="sxs-lookup"><span data-stu-id="29381-105">Azure AD is Microsoft’s multi-tenant cloud based directory and identity management service.</span></span> <span data-ttu-id="29381-106">Azure kendisini müşteriler, hizmet yöneticileri ve kuruluş kullanıcılarının hello kimlik doğrulaması için Azure AD kullanır.</span><span class="sxs-lookup"><span data-stu-id="29381-106">Azure itself uses Azure AD for hello authentication of its customers, service administrators, and organizational users.</span></span>

<span data-ttu-id="29381-107">Merhaba Batch yönetimi .NET kitaplığı, Batch hesaplarını, hesabı anahtarları, uygulamalar ve uygulama paketleri ile çalışmak için türü ortaya çıkarır.</span><span class="sxs-lookup"><span data-stu-id="29381-107">hello Batch Management .NET library exposes types for working with Batch accounts, account keys, applications, and application packages.</span></span> <span data-ttu-id="29381-108">Merhaba Batch yönetimi .NET kitaplığı bir Azure kaynak sağlayıcısı istemci ve ile birlikte kullanılan [Azure Resource Manager] [ resman_overview] toomanage bu kaynakları programlı olarak.</span><span class="sxs-lookup"><span data-stu-id="29381-108">hello Batch Management .NET library is an Azure resource provider client, and is used together with [Azure Resource Manager][resman_overview] toomanage these resources programmatically.</span></span> <span data-ttu-id="29381-109">Azure AD olduğu ve hello Batch yönetimi .NET kitaplığı dahil olmak üzere tüm Azure kaynak sağlayıcısı istemci aracılığıyla yapılan gerekli tooauthenticate istekleri [Azure Resource Manager][resman_overview].</span><span class="sxs-lookup"><span data-stu-id="29381-109">Azure AD is required tooauthenticate requests made through any Azure resource provider client, including hello Batch Management .NET library, and through [Azure Resource Manager][resman_overview].</span></span>

<span data-ttu-id="29381-110">Bu makalede, Azure AD tooauthenticate hello Batch yönetimi .NET kitaplığını kullanan uygulamalardan kullanarak keşfedin.</span><span class="sxs-lookup"><span data-stu-id="29381-110">In this article, we explore using Azure AD tooauthenticate from applications that use hello Batch Management .NET library.</span></span> <span data-ttu-id="29381-111">Azure AD toouse tooauthenticate Abonelik Yöneticisi veya ortak yönetici, kullanarak kimlik doğrulaması nasıl tümleşik gösterir.</span><span class="sxs-lookup"><span data-stu-id="29381-111">We show how toouse Azure AD tooauthenticate a subscription administrator or co-administrator, using integrated authentication.</span></span> <span data-ttu-id="29381-112">Merhaba kullanırız [AccountManagment] [ acct_mgmt_sample] örnek proje, github'da Azure AD ile Merhaba Batch yönetimi .NET kitaplığını kullanarak aracılığıyla toowalk kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="29381-112">We use hello [AccountManagment][acct_mgmt_sample] sample project, available on GitHub, toowalk through using Azure AD with hello Batch Management .NET library.</span></span>

<span data-ttu-id="29381-113">Merhaba Batch yönetimi .NET kitaplığı ve hello AccountManagement örnek, kullanma hakkında daha fazla toolearn bkz [yönetmek Batch hesaplarını ve kotalarını hello Batch Yönetimi istemci kitaplığı için .NET ile](batch-management-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="29381-113">toolearn more about using hello Batch Management .NET library and hello AccountManagement sample, see [Manage Batch accounts and quotas with hello Batch Management client library for .NET](batch-management-dotnet.md).</span></span>

## <a name="register-your-application-with-azure-ad"></a><span data-ttu-id="29381-114">Azure AD ile uygulamanızı kaydetme</span><span class="sxs-lookup"><span data-stu-id="29381-114">Register your application with Azure AD</span></span>

<span data-ttu-id="29381-115">Hello Azure [Active Directory kimlik doğrulama Kitaplığı] [ aad_adal] (ADAL) kullanmak için AD uygulamalarınız içinde bir programlama arabirimidir tooAzure sağlar.</span><span class="sxs-lookup"><span data-stu-id="29381-115">hello Azure [Active Directory Authentication Library][aad_adal] (ADAL) provides a programmatic interface tooAzure AD for use within your applications.</span></span> <span data-ttu-id="29381-116">ADAL toocall uygulamanızdan bir Azure AD kiracısında uygulamanızı kaydetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="29381-116">toocall ADAL from your application, you must register your application in an Azure AD tenant.</span></span> <span data-ttu-id="29381-117">Uygulamanızı kaydederken hello Azure AD kiracısı içinde bir ad da dahil olmak üzere uygulamanız hakkındaki bilgilerle Azure AD sağlayın.</span><span class="sxs-lookup"><span data-stu-id="29381-117">When you register your application, you supply Azure AD with information about your application, including a name for it within hello Azure AD tenant.</span></span> <span data-ttu-id="29381-118">Ardından Azure AD uygulama kimliği sağlar çalışma zamanında Azure AD ile uygulamanızı tooassociate kullanın.</span><span class="sxs-lookup"><span data-stu-id="29381-118">Azure AD then provides an application ID that you use tooassociate your application with Azure AD at runtime.</span></span> <span data-ttu-id="29381-119">toolearn hello uygulama kimliği hakkında daha fazla bilgi görmek [uygulama ve hizmet asıl nesneler Azure Active Directory'de](../active-directory/develop/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="29381-119">toolearn more about hello application ID, see [Application and service principal objects in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span></span>

<span data-ttu-id="29381-120">tooregister hello AccountManagement örnek uygulama izleyin hello hello adımlarda [bir uygulama ekleme](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) bölümüne [uygulamaları Azure Active Directory ile tümleştirme] [ aad_integrate].</span><span class="sxs-lookup"><span data-stu-id="29381-120">tooregister hello AccountManagement sample application, follow hello steps in hello [Adding an Application](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) section in [Integrating applications with Azure Active Directory][aad_integrate].</span></span> <span data-ttu-id="29381-121">Belirtin **yerel istemci uygulaması** hello tür bir uygulama için.</span><span class="sxs-lookup"><span data-stu-id="29381-121">Specify **Native Client Application** for hello type of application.</span></span> <span data-ttu-id="29381-122">Merhaba endüstri hello standart OAuth 2.0 URI'sini **yeniden yönlendirme URI'si** olan `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="29381-122">hello industry standard OAuth 2.0 URI for hello **Redirect URI** is `urn:ietf:wg:oauth:2.0:oob`.</span></span> <span data-ttu-id="29381-123">Ancak, geçerli bir URI belirtebilirsiniz (gibi `http://myaccountmanagementsample`) hello için **yeniden yönlendirme URI'si**toobe gerçek bir uç noktası gerekmez gibi:</span><span class="sxs-lookup"><span data-stu-id="29381-123">However, you can specify any valid URI (such as `http://myaccountmanagementsample`) for hello **Redirect URI**, as it does not need toobe a real endpoint:</span></span>

![](./media/batch-aad-auth-management/app-registration-management-plane.png)

<span data-ttu-id="29381-124">Merhaba kayıt işlemini tamamladıktan sonra hello uygulama kimliği görebilir ve uygulamanız için listelenen nesne (hizmet sorumlusu) kimliği hello.</span><span class="sxs-lookup"><span data-stu-id="29381-124">Once you complete hello registration process, you'll see hello application ID and hello object (service principal) ID listed for your application.</span></span>  

![](./media/batch-aad-auth-management/app-registration-client-id.png)

## <a name="grant-hello-azure-resource-manager-api-access-tooyour-application"></a><span data-ttu-id="29381-125">Merhaba Azure Kaynak Yöneticisi API'si erişim tooyour uygulaması verin</span><span class="sxs-lookup"><span data-stu-id="29381-125">Grant hello Azure Resource Manager API access tooyour application</span></span>

<span data-ttu-id="29381-126">Ardından, toodelegate erişim tooyour uygulama toohello Azure Kaynak Yöneticisi API'si gerekir.</span><span class="sxs-lookup"><span data-stu-id="29381-126">Next, you'll need toodelegate access tooyour application toohello Azure Resource Manager API.</span></span> <span data-ttu-id="29381-127">Merhaba Resource Manager API Hello Azure AD tanımlayıcısıdır **Windows Azure Hizmet Yönetimi API'si**.</span><span class="sxs-lookup"><span data-stu-id="29381-127">hello Azure AD identifier for hello Resource Manager API is **Windows Azure Service Management API**.</span></span>

<span data-ttu-id="29381-128">Hello Azure Portalı'nda aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="29381-128">Follow these steps in hello Azure portal:</span></span>

1. <span data-ttu-id="29381-129">Merhaba sol gezinti bölmesinde hello Azure portal'ı seçin **daha Hizmetleri**, tıklatın **uygulama kayıtlar**, tıklatıp **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="29381-129">In hello left-hand navigation pane of hello Azure portal, choose **More Services**, click **App Registrations**, and click **Add**.</span></span>
2. <span data-ttu-id="29381-130">Merhaba listesinde uygulamanızın uygulama kayıtların hello adını arayın:</span><span class="sxs-lookup"><span data-stu-id="29381-130">Search for hello name of your application in hello list of app registrations:</span></span>

    ![Uygulama adınız arayın](./media/batch-aad-auth-management/search-app-registration.png)

3. <span data-ttu-id="29381-132">Görüntü hello **ayarları** dikey.</span><span class="sxs-lookup"><span data-stu-id="29381-132">Display hello **Settings** blade.</span></span> <span data-ttu-id="29381-133">Merhaba, **API erişimini** bölümünde, select **gerekli izinleri**.</span><span class="sxs-lookup"><span data-stu-id="29381-133">In hello **API Access** section, select **Required permissions**.</span></span>
4. <span data-ttu-id="29381-134">Tıklatın **Ekle** tooadd yeni gerekli izni.</span><span class="sxs-lookup"><span data-stu-id="29381-134">Click **Add** tooadd a new required permission.</span></span> 
5. <span data-ttu-id="29381-135">1. adımda girin **Windows Azure Hizmet Yönetimi API'si**, bu API hello sonuçları listesinden seçin ve hello tıklatın **seçin** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="29381-135">In step 1, enter **Windows Azure Service Management API**, select that API from hello list of results, and click hello **Select** button.</span></span>
6. <span data-ttu-id="29381-136">2. adımda seç onay kutusunu sonraki çok hello**erişim Azure Klasik dağıtım modeli kuruluş kullanıcılar olarak**, hello tıklatıp **seçin** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="29381-136">In step 2, select hello check box next too**Access Azure classic deployment model as organization users**, and click hello **Select** button.</span></span>
7. <span data-ttu-id="29381-137">Merhaba tıklatın **Bitti** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="29381-137">Click hello **Done** button.</span></span>

<span data-ttu-id="29381-138">Merhaba **gerekli izinler** ADAL ve Resource Manager API'leri izinleri tooyour uygulama tooboth verilen gösterir hello artık dikey.</span><span class="sxs-lookup"><span data-stu-id="29381-138">hello **Required Permissions** blade now shows that permissions tooyour application are granted tooboth hello ADAL and Resource Manager APIs.</span></span> <span data-ttu-id="29381-139">Uygulamanızı Azure AD ile ilk kez kaydederken izinleri tooADAL varsayılan olarak verilir.</span><span class="sxs-lookup"><span data-stu-id="29381-139">Permissions are granted tooADAL by default when you first register your app with Azure AD.</span></span>

![Temsilci izinleri toohello Azure Kaynak Yöneticisi API'si](./media/batch-aad-auth-management/required-permissions-management-plane.png)

## <a name="azure-ad-endpoints"></a><span data-ttu-id="29381-141">Azure AD uç noktaları</span><span class="sxs-lookup"><span data-stu-id="29381-141">Azure AD endpoints</span></span>

<span data-ttu-id="29381-142">tooauthenticate, toplu yönetimini çözümleriniz Azure AD ile iyi bilinen iki uç nokta gerekir.</span><span class="sxs-lookup"><span data-stu-id="29381-142">tooauthenticate your Batch Management solutions with Azure AD, you'll need two well-known endpoints.</span></span>

- <span data-ttu-id="29381-143">Merhaba **Azure AD ortak uç nokta** belirli bir kiracı sağlanmadığında tümleşik kimlik doğrulaması hello durumda olduğu gibi arabirimi toplama genel bir kimlik bilgisi sağlanır:</span><span class="sxs-lookup"><span data-stu-id="29381-143">hello **Azure AD common endpoint** provides a generic credential gathering interface when a specific tenant is not provided, as in hello case of integrated authentication:</span></span>

    `https://login.microsoftonline.com/common`

- <span data-ttu-id="29381-144">Merhaba **Azure Kaynak Yöneticisi uç noktası** kullanılan tooacquire istekleri toohello toplu yönetim hizmeti kimlik doğrulaması için bir belirteçtir:</span><span class="sxs-lookup"><span data-stu-id="29381-144">hello **Azure Resource Manager endpoint** is used tooacquire a token for authenticating requests toohello Batch management service:</span></span>

    `https://management.core.windows.net/`

<span data-ttu-id="29381-145">Merhaba AccountManagement örnek uygulama Bu uç noktalar için sabitleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="29381-145">hello AccountManagement sample application defines constants for these endpoints.</span></span> <span data-ttu-id="29381-146">Bu sabitleri değiştirmeden bırakın:</span><span class="sxs-lookup"><span data-stu-id="29381-146">Leave these constants unchanged:</span></span>

```csharp
// Azure Active Directory "common" endpoint.
private const string AuthorityUri = "https://login.microsoftonline.com/common";
// Azure Resource Manager endpoint 
private const string ResourceUri = "https://management.core.windows.net/";
```

## <a name="reference-your-application-id"></a><span data-ttu-id="29381-147">Uygulama Kimliğinizi başvurusu</span><span class="sxs-lookup"><span data-stu-id="29381-147">Reference your application ID</span></span> 

<span data-ttu-id="29381-148">İstemci uygulamanızı çalışma zamanında hello uygulama kimliği (Ayrıca başvurulan tooas hello istemci kimliği) tooaccess Azure AD kullanır.</span><span class="sxs-lookup"><span data-stu-id="29381-148">Your client application uses hello application ID (also referred tooas hello client ID) tooaccess Azure AD at runtime.</span></span> <span data-ttu-id="29381-149">Hello Azure portal, uygulamanızın kaydedildikten sonra kayıtlı uygulamanız için Azure AD tarafından sağlanan kod toouse hello uygulama Kimliğinizi güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="29381-149">Once you've registered your application in hello Azure portal, update your code toouse hello application ID provided by Azure AD for your registered application.</span></span> <span data-ttu-id="29381-150">Hello AccountManagement örnek uygulama, uygulama Kimliğiniz hello Azure portal toohello uygun sabiti kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="29381-150">In hello AccountManagement sample application, copy your application ID from hello Azure portal toohello appropriate constant:</span></span>

```csharp
// Specify hello unique identifier (hello "Client ID") for your application. This is required so that your
// native client application (i.e. this sample) can access hello Microsoft Azure AD Graph API. For information
// about registering an application in Azure Active Directory, please see "Adding an Application" here:
// https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/
private const string ClientId = "<application-id>";
```
<span data-ttu-id="29381-151">Ayrıca hello yeniden yönlendirme hello kayıt işlemi sırasında belirtilen URI'sini kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="29381-151">Also copy hello redirect URI that you specified during hello registration process.</span></span> <span data-ttu-id="29381-152">Merhaba yeniden yönlendirme URI'si kodunuzda belirtilen hello yeniden yönlendirme Merhaba uygulaması kaydolurken sağladığınız URI eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="29381-152">hello redirect URI specified in your code must match hello redirect URI that you provided when you registered hello application.</span></span>

```csharp
// hello URI toowhich Azure AD will redirect in response tooan OAuth 2.0 request. This value is
// specified by you when you register an application with AAD (see ClientId comment). It does not
// need toobe a real endpoint, but must be a valid URI (e.g. https://accountmgmtsampleapp).
private const string RedirectUri = "http://myaccountmanagementsample";
```

## <a name="acquire-an-azure-ad-authentication-token"></a><span data-ttu-id="29381-153">Azure AD kimlik doğrulama belirtecini alma</span><span class="sxs-lookup"><span data-stu-id="29381-153">Acquire an Azure AD authentication token</span></span>

<span data-ttu-id="29381-154">Merhaba AccountManagement örnek hello Azure AD kiracısında kaydetmek ve değerleri ile Merhaba örnek kaynak kodunu güncelleştirin sonra hello Azure AD kullanarak hazır tooauthenticate örnektir.</span><span class="sxs-lookup"><span data-stu-id="29381-154">After you register hello AccountManagement sample in hello Azure AD tenant and update hello sample source code with your values, hello sample is ready tooauthenticate using Azure AD.</span></span> <span data-ttu-id="29381-155">Merhaba örneği çalıştırdığınızda, hello ADAL tooacquire kimlik doğrulama belirtecini çalışır.</span><span class="sxs-lookup"><span data-stu-id="29381-155">When you run hello sample, hello ADAL attempts tooacquire an authentication token.</span></span> <span data-ttu-id="29381-156">Bu adımda, Microsoft kimlik bilgilerinizi ister:</span><span class="sxs-lookup"><span data-stu-id="29381-156">At this step, it prompts you for your Microsoft credentials:</span></span> 

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

<span data-ttu-id="29381-157">Kimlik bilgilerinizi sağlayın sonra hello örnek uygulama kimliği doğrulanmış tooissue istekleri toohello toplu yönetim hizmeti geçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="29381-157">After you provide your credentials, hello sample application can proceed tooissue authenticated requests toohello Batch management service.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="29381-158">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="29381-158">Next steps</span></span>

<span data-ttu-id="29381-159">Merhaba çalıştırma hakkında daha fazla bilgi için [AccountManagement örnek uygulama][acct_mgmt_sample], bkz: [yönetmek Batch hesaplarını ve kotalarını hello Batch Yönetimi istemci kitaplığı için .NETile](batch-management-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="29381-159">For more information on running hello [AccountManagement sample application][acct_mgmt_sample], see [Manage Batch accounts and quotas with hello Batch Management client library for .NET](batch-management-dotnet.md).</span></span>

<span data-ttu-id="29381-160">Azure AD hakkında daha fazla toolearn bkz hello [Azure Active Directory belgeleri](https://docs.microsoft.com/azure/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="29381-160">toolearn more about Azure AD, see hello [Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span></span> <span data-ttu-id="29381-161">Nasıl toouse ADAL kullanılabilir hello gösteren ayrıntılı örnekler [Azure Kod örnekleri](https://azure.microsoft.com/resources/samples/?service=active-directory) kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="29381-161">In-depth examples showing how toouse ADAL are available in hello [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=active-directory) library.</span></span>

<span data-ttu-id="29381-162">Azure AD kullanarak tooauthenticate Batch hizmeti uygulamaları bkz [Active Directory ile kimlik doğrulaması toplu hizmet çözümlerine](batch-aad-auth.md).</span><span class="sxs-lookup"><span data-stu-id="29381-162">tooauthenticate Batch service applications using Azure AD, see [Authenticate Batch service solutions with Active Directory](batch-aad-auth.md).</span></span> 


[aad_about]: ../active-directory/active-directory-whatis.md "Azure Active Directory nedir?"
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Azure AD için kimlik doğrulama senaryoları"
[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Uygulamaları Azure Active Directory ile tümleştirme"
[acct_mgmt_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/AccountManagement
[azure_portal]: http://portal.azure.com
[resman_overview]: ../azure-resource-manager/resource-group-overview.md
