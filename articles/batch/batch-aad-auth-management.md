---
title: "Toplu işlem yönetimi çözümlerinin kimlik doğrulaması için Azure Active Directory kullanmak | Microsoft Docs"
description: "Uygulamaları Azure resource manager ile oluşturulmuş ve toplu kaynak sağlayıcısı Azure AD ile kimlik doğrulaması."
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
ms.openlocfilehash: 26d4adf4f74f9aacc4cf8cf24be293ebdb4d63c8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="authenticate-batch-management-solutions-with-active-directory"></a><span data-ttu-id="574e7-103">Toplu işlem yönetimi çözümleri Active Directory ile kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="574e7-103">Authenticate Batch Management solutions with Active Directory</span></span>

<span data-ttu-id="574e7-104">Azure Batch yönetim hizmeti çağıran uygulamalar kimlik doğrulaması ile [Azure Active Directory] [ aad_about] (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="574e7-104">Applications that call the Azure Batch Management service authenticate with [Azure Active Directory][aad_about] (Azure AD).</span></span> <span data-ttu-id="574e7-105">Azure AD, Microsoft'un çok kiracılı bulut tabanlı dizin ve Kimlik Yönetimi Hizmeti ' dir.</span><span class="sxs-lookup"><span data-stu-id="574e7-105">Azure AD is Microsoft’s multi-tenant cloud based directory and identity management service.</span></span> <span data-ttu-id="574e7-106">Azure kendisini müşteriler, hizmet yöneticileri ve kuruluş kullanıcıların kimlik doğrulaması için Azure AD kullanır.</span><span class="sxs-lookup"><span data-stu-id="574e7-106">Azure itself uses Azure AD for the authentication of its customers, service administrators, and organizational users.</span></span>

<span data-ttu-id="574e7-107">Batch yönetimi .NET kitaplığı, Batch hesaplarını, hesabı anahtarları, uygulamalar ve uygulama paketleri ile çalışmak için türü ortaya çıkarır.</span><span class="sxs-lookup"><span data-stu-id="574e7-107">The Batch Management .NET library exposes types for working with Batch accounts, account keys, applications, and application packages.</span></span> <span data-ttu-id="574e7-108">Batch yönetimi .NET kitaplığı bir Azure kaynak sağlayıcısı istemci ve ile birlikte kullanılan [Azure Resource Manager] [ resman_overview] bu kaynakları programlı olarak yönetmek için.</span><span class="sxs-lookup"><span data-stu-id="574e7-108">The Batch Management .NET library is an Azure resource provider client, and is used together with [Azure Resource Manager][resman_overview] to manage these resources programmatically.</span></span> <span data-ttu-id="574e7-109">Azure AD ve toplu işlem yönetimi .NET kitaplığı dahil olmak üzere tüm Azure kaynak sağlayıcısı istemci aracılığıyla yapılan istekleri kimlik doğrulaması için gerekli olduğunu [Azure Resource Manager][resman_overview].</span><span class="sxs-lookup"><span data-stu-id="574e7-109">Azure AD is required to authenticate requests made through any Azure resource provider client, including the Batch Management .NET library, and through [Azure Resource Manager][resman_overview].</span></span>

<span data-ttu-id="574e7-110">Bu makalede, Azure AD Batch yönetimi .NET kitaplığı kullanan uygulamalardan kimlik doğrulaması kullanmayı keşfedin.</span><span class="sxs-lookup"><span data-stu-id="574e7-110">In this article, we explore using Azure AD to authenticate from applications that use the Batch Management .NET library.</span></span> <span data-ttu-id="574e7-111">Azure AD Abonelik Yöneticisi veya ortak yönetici, tümleşik kimlik doğrulaması kullanarak kimlik doğrulaması için nasıl kullanılacağını gösteriyoruz.</span><span class="sxs-lookup"><span data-stu-id="574e7-111">We show how to use Azure AD to authenticate a subscription administrator or co-administrator, using integrated authentication.</span></span> <span data-ttu-id="574e7-112">Kullanırız [AccountManagment] [ acct_mgmt_sample] örnek proje, github'da Azure AD ile Batch yönetimi .NET kitaplığını kullanarak izlenecek yol için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="574e7-112">We use the [AccountManagment][acct_mgmt_sample] sample project, available on GitHub, to walk through using Azure AD with the Batch Management .NET library.</span></span>

<span data-ttu-id="574e7-113">Batch yönetimi .NET kitaplığı ve AccountManagement örnek kullanma hakkında daha fazla bilgi edinmek için [yönetmek Batch hesaplarını ve kotalarını .NET için Batch Yönetimi istemci kitaplığı ile](batch-management-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="574e7-113">To learn more about using the Batch Management .NET library and the AccountManagement sample, see [Manage Batch accounts and quotas with the Batch Management client library for .NET](batch-management-dotnet.md).</span></span>

## <a name="register-your-application-with-azure-ad"></a><span data-ttu-id="574e7-114">Azure AD ile uygulamanızı kaydetme</span><span class="sxs-lookup"><span data-stu-id="574e7-114">Register your application with Azure AD</span></span>

<span data-ttu-id="574e7-115">Azure [Active Directory kimlik doğrulama Kitaplığı] [ aad_adal] (ADAL) Azure ad uygulamalarınız içinde kullanmak için programa dayalı bir arabirim sağlar.</span><span class="sxs-lookup"><span data-stu-id="574e7-115">The Azure [Active Directory Authentication Library][aad_adal] (ADAL) provides a programmatic interface to Azure AD for use within your applications.</span></span> <span data-ttu-id="574e7-116">ADAL uygulamanızdan çağırmak için bir Azure AD kiracısında uygulamanızı kaydetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="574e7-116">To call ADAL from your application, you must register your application in an Azure AD tenant.</span></span> <span data-ttu-id="574e7-117">Uygulamanızı kaydederken, Azure AD kiracısı içinde bir ad da dahil olmak üzere uygulamanız hakkındaki bilgilerle Azure AD sağlayın.</span><span class="sxs-lookup"><span data-stu-id="574e7-117">When you register your application, you supply Azure AD with information about your application, including a name for it within the Azure AD tenant.</span></span> <span data-ttu-id="574e7-118">Ardından Azure AD çalışma zamanında Azure AD ile uygulamanızı ilişkilendirmek için kullandığınız bir uygulama kimliği sağlar.</span><span class="sxs-lookup"><span data-stu-id="574e7-118">Azure AD then provides an application ID that you use to associate your application with Azure AD at runtime.</span></span> <span data-ttu-id="574e7-119">Uygulama kimliği hakkında daha fazla bilgi için bkz: [uygulama ve hizmet asıl nesneler Azure Active Directory'de](../active-directory/develop/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="574e7-119">To learn more about the application ID, see [Application and service principal objects in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span></span>

<span data-ttu-id="574e7-120">AccountManagement örnek uygulama kaydetmek için adımları [bir uygulama ekleme](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) bölümüne [uygulamaları Azure Active Directory ile tümleştirme][aad_integrate].</span><span class="sxs-lookup"><span data-stu-id="574e7-120">To register the AccountManagement sample application, follow the steps in the [Adding an Application](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) section in [Integrating applications with Azure Active Directory][aad_integrate].</span></span> <span data-ttu-id="574e7-121">Belirtin **yerel istemci uygulaması** uygulama türü için.</span><span class="sxs-lookup"><span data-stu-id="574e7-121">Specify **Native Client Application** for the type of application.</span></span> <span data-ttu-id="574e7-122">Endüstri Standart OAuth 2.0 URI'sini **yeniden yönlendirme URI'si** olan `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="574e7-122">The industry standard OAuth 2.0 URI for the **Redirect URI** is `urn:ietf:wg:oauth:2.0:oob`.</span></span> <span data-ttu-id="574e7-123">Ancak, geçerli bir URI belirtebilirsiniz (gibi `http://myaccountmanagementsample`) için **yeniden yönlendirme URI'si**gibi gerçek bir uç nokta olması gerekmez:</span><span class="sxs-lookup"><span data-stu-id="574e7-123">However, you can specify any valid URI (such as `http://myaccountmanagementsample`) for the **Redirect URI**, as it does not need to be a real endpoint:</span></span>

![](./media/batch-aad-auth-management/app-registration-management-plane.png)

<span data-ttu-id="574e7-124">Kayıt işlemini tamamladıktan sonra uygulama kimliği ve uygulamanız için listelenen nesne (hizmet sorumlusu) kimliği görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="574e7-124">Once you complete the registration process, you'll see the application ID and the object (service principal) ID listed for your application.</span></span>  

![](./media/batch-aad-auth-management/app-registration-client-id.png)

## <a name="grant-the-azure-resource-manager-api-access-to-your-application"></a><span data-ttu-id="574e7-125">Uygulamanız için Azure Kaynak Yöneticisi API'si erişim</span><span class="sxs-lookup"><span data-stu-id="574e7-125">Grant the Azure Resource Manager API access to your application</span></span>

<span data-ttu-id="574e7-126">Ardından, Azure Resource Manager API uygulamanıza erişimi temsilci gerekir.</span><span class="sxs-lookup"><span data-stu-id="574e7-126">Next, you'll need to delegate access to your application to the Azure Resource Manager API.</span></span> <span data-ttu-id="574e7-127">Kaynak Yöneticisi API'si için Azure AD tanımlayıcısıdır **Windows Azure Hizmet Yönetimi API'si**.</span><span class="sxs-lookup"><span data-stu-id="574e7-127">The Azure AD identifier for the Resource Manager API is **Windows Azure Service Management API**.</span></span>

<span data-ttu-id="574e7-128">Azure portalında aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="574e7-128">Follow these steps in the Azure portal:</span></span>

1. <span data-ttu-id="574e7-129">Azure portalının sol gezinti bölmesinde seçin **daha Hizmetleri**, tıklatın **uygulama kayıtlar**, tıklatıp **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="574e7-129">In the left-hand navigation pane of the Azure portal, choose **More Services**, click **App Registrations**, and click **Add**.</span></span>
2. <span data-ttu-id="574e7-130">Listedeki uygulamanızın uygulama kayıtların adını arayın:</span><span class="sxs-lookup"><span data-stu-id="574e7-130">Search for the name of your application in the list of app registrations:</span></span>

    ![Uygulama adınız arayın](./media/batch-aad-auth-management/search-app-registration.png)

3. <span data-ttu-id="574e7-132">Görüntü **ayarları** dikey.</span><span class="sxs-lookup"><span data-stu-id="574e7-132">Display the **Settings** blade.</span></span> <span data-ttu-id="574e7-133">İçinde **API erişimini** bölümünde, select **gerekli izinleri**.</span><span class="sxs-lookup"><span data-stu-id="574e7-133">In the **API Access** section, select **Required permissions**.</span></span>
4. <span data-ttu-id="574e7-134">Tıklatın **Ekle** yeni bir gerekli izin eklemek için.</span><span class="sxs-lookup"><span data-stu-id="574e7-134">Click **Add** to add a new required permission.</span></span> 
5. <span data-ttu-id="574e7-135">1. adımda girin **Windows Azure Hizmet Yönetimi API'si**, bu API sonuçları listesinden seçin ve tıklatın **seçin** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="574e7-135">In step 1, enter **Windows Azure Service Management API**, select that API from the list of results, and click the **Select** button.</span></span>
6. <span data-ttu-id="574e7-136">2. adımda yanındaki onay kutusunu işaretleyin **erişim Azure Klasik dağıtım modeli kuruluş kullanıcılar olarak**, tıklatıp **seçin** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="574e7-136">In step 2, select the check box next to **Access Azure classic deployment model as organization users**, and click the **Select** button.</span></span>
7. <span data-ttu-id="574e7-137">Tıklatın **Bitti** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="574e7-137">Click the **Done** button.</span></span>

<span data-ttu-id="574e7-138">**Gerekli izinler** dikey şimdi gösterir, uygulamanız için ADAL hem Resource Manager API'leri için izinlerin verildiğinden emin.</span><span class="sxs-lookup"><span data-stu-id="574e7-138">The **Required Permissions** blade now shows that permissions to your application are granted to both the ADAL and Resource Manager APIs.</span></span> <span data-ttu-id="574e7-139">Uygulamanızı Azure AD ile ilk kez kaydederken izinleri ADAL için varsayılan olarak verilir.</span><span class="sxs-lookup"><span data-stu-id="574e7-139">Permissions are granted to ADAL by default when you first register your app with Azure AD.</span></span>

![Azure Kaynak Yöneticisi API'si temsilci izinleri](./media/batch-aad-auth-management/required-permissions-management-plane.png)

## <a name="azure-ad-endpoints"></a><span data-ttu-id="574e7-141">Azure AD uç noktaları</span><span class="sxs-lookup"><span data-stu-id="574e7-141">Azure AD endpoints</span></span>

<span data-ttu-id="574e7-142">Toplu işlem yönetimi çözümlerinizi Azure AD ile kimlik doğrulaması yapmak için iyi bilinen iki uç nokta gerekir.</span><span class="sxs-lookup"><span data-stu-id="574e7-142">To authenticate your Batch Management solutions with Azure AD, you'll need two well-known endpoints.</span></span>

- <span data-ttu-id="574e7-143">**Azure AD ortak uç nokta** belirli bir kiracı sağlanmadığında tümleşik kimlik doğrulaması gibi söz konusu olduğunda arabirimi toplama genel bir kimlik bilgisi sağlanır:</span><span class="sxs-lookup"><span data-stu-id="574e7-143">The **Azure AD common endpoint** provides a generic credential gathering interface when a specific tenant is not provided, as in the case of integrated authentication:</span></span>

    `https://login.microsoftonline.com/common`

- <span data-ttu-id="574e7-144">**Azure Kaynak Yöneticisi uç noktası** toplu yönetim hizmeti isteklerine kimlik doğrulaması için bir belirteç almak üzere kullanılır:</span><span class="sxs-lookup"><span data-stu-id="574e7-144">The **Azure Resource Manager endpoint** is used to acquire a token for authenticating requests to the Batch management service:</span></span>

    `https://management.core.windows.net/`

<span data-ttu-id="574e7-145">Bu uç noktalar için sabitleri AccountManagement örnek uygulama tanımlar.</span><span class="sxs-lookup"><span data-stu-id="574e7-145">The AccountManagement sample application defines constants for these endpoints.</span></span> <span data-ttu-id="574e7-146">Bu sabitleri değiştirmeden bırakın:</span><span class="sxs-lookup"><span data-stu-id="574e7-146">Leave these constants unchanged:</span></span>

```csharp
// Azure Active Directory "common" endpoint.
private const string AuthorityUri = "https://login.microsoftonline.com/common";
// Azure Resource Manager endpoint 
private const string ResourceUri = "https://management.core.windows.net/";
```

## <a name="reference-your-application-id"></a><span data-ttu-id="574e7-147">Uygulama Kimliğinizi başvurusu</span><span class="sxs-lookup"><span data-stu-id="574e7-147">Reference your application ID</span></span> 

<span data-ttu-id="574e7-148">İstemci uygulamanızı Azure AD çalışma zamanında erişmek için uygulama kimliği (istemci kimliği olarak da bilinir) kullanır.</span><span class="sxs-lookup"><span data-stu-id="574e7-148">Your client application uses the application ID (also referred to as the client ID) to access Azure AD at runtime.</span></span> <span data-ttu-id="574e7-149">Azure Portal'da uygulamanızın kaydedildikten sonra kayıtlı uygulamanız için Azure AD tarafından sağlanan uygulama kimliği kullanmak için kodunuzu güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="574e7-149">Once you've registered your application in the Azure portal, update your code to use the application ID provided by Azure AD for your registered application.</span></span> <span data-ttu-id="574e7-150">AccountManagement örnek uygulama için uygun sabiti Azure portalından uygulama Kimliğinizi kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="574e7-150">In the AccountManagement sample application, copy your application ID from the Azure portal to the appropriate constant:</span></span>

```csharp
// Specify the unique identifier (the "Client ID") for your application. This is required so that your
// native client application (i.e. this sample) can access the Microsoft Azure AD Graph API. For information
// about registering an application in Azure Active Directory, please see "Adding an Application" here:
// https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/
private const string ClientId = "<application-id>";
```
<span data-ttu-id="574e7-151">Ayrıca kayıt işlemi sırasında belirtilen URI yeniden yönlendirme kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="574e7-151">Also copy the redirect URI that you specified during the registration process.</span></span> <span data-ttu-id="574e7-152">URI kodunuzda belirtilen yeniden yönlendirme yeniden yönlendirilen uygulamayı kaydolurken sağladığınız URI eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="574e7-152">The redirect URI specified in your code must match the redirect URI that you provided when you registered the application.</span></span>

```csharp
// The URI to which Azure AD will redirect in response to an OAuth 2.0 request. This value is
// specified by you when you register an application with AAD (see ClientId comment). It does not
// need to be a real endpoint, but must be a valid URI (e.g. https://accountmgmtsampleapp).
private const string RedirectUri = "http://myaccountmanagementsample";
```

## <a name="acquire-an-azure-ad-authentication-token"></a><span data-ttu-id="574e7-153">Azure AD kimlik doğrulama belirtecini alma</span><span class="sxs-lookup"><span data-stu-id="574e7-153">Acquire an Azure AD authentication token</span></span>

<span data-ttu-id="574e7-154">Azure AD kiracısında AccountManagement örnek kaydetmek ve değerleri ile örnek kaynak kodunu güncelleştirin sonra Azure AD kullanarak kimlik doğrulaması için hazır bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="574e7-154">After you register the AccountManagement sample in the Azure AD tenant and update the sample source code with your values, the sample is ready to authenticate using Azure AD.</span></span> <span data-ttu-id="574e7-155">Örneği çalıştırdığınızda, ADAL kimlik doğrulama belirtecini almayı dener.</span><span class="sxs-lookup"><span data-stu-id="574e7-155">When you run the sample, the ADAL attempts to acquire an authentication token.</span></span> <span data-ttu-id="574e7-156">Bu adımda, Microsoft kimlik bilgilerinizi ister:</span><span class="sxs-lookup"><span data-stu-id="574e7-156">At this step, it prompts you for your Microsoft credentials:</span></span> 

```csharp
// Obtain an access token using the "common" AAD resource. This allows the application
// to query AAD for information that lies outside the application's tenant (such as for
// querying subscription information in your Azure account).
AuthenticationContext authContext = new AuthenticationContext(AuthorityUri);
AuthenticationResult authResult = authContext.AcquireToken(ResourceUri,
                                                        ClientId,
                                                        new Uri(RedirectUri),
                                                        PromptBehavior.Auto);
```

<span data-ttu-id="574e7-157">Kimlik bilgilerinizi sağlayın sonra örnek uygulaması Batch yönetim hizmeti kimliği doğrulanmış istekler verecek geçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="574e7-157">After you provide your credentials, the sample application can proceed to issue authenticated requests to the Batch management service.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="574e7-158">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="574e7-158">Next steps</span></span>

<span data-ttu-id="574e7-159">Çalıştırma hakkında daha fazla bilgi için [AccountManagement örnek uygulama][acct_mgmt_sample], bkz: [yönetmek Batch hesaplarını ve kotalarını .NET için Batch Yönetimi istemci kitaplığı ile](batch-management-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="574e7-159">For more information on running the [AccountManagement sample application][acct_mgmt_sample], see [Manage Batch accounts and quotas with the Batch Management client library for .NET](batch-management-dotnet.md).</span></span>

<span data-ttu-id="574e7-160">Azure AD hakkında daha fazla bilgi için bkz: [Azure Active Directory belgeleri](https://docs.microsoft.com/azure/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="574e7-160">To learn more about Azure AD, see the [Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span></span> <span data-ttu-id="574e7-161">ADAL'nin kullanımı gösteren ayrıntılı örnekler kullanılabilir [Azure Kod örnekleri](https://azure.microsoft.com/resources/samples/?service=active-directory) kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="574e7-161">In-depth examples showing how to use ADAL are available in the [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=active-directory) library.</span></span>

<span data-ttu-id="574e7-162">Toplu hizmet uygulamaları Azure AD kullanarak kimlik doğrulaması yapmak için bkz: [Active Directory ile kimlik doğrulaması toplu hizmet çözümlerine](batch-aad-auth.md).</span><span class="sxs-lookup"><span data-stu-id="574e7-162">To authenticate Batch service applications using Azure AD, see [Authenticate Batch service solutions with Active Directory](batch-aad-auth.md).</span></span> 


<span data-ttu-id="574e7-163">[aad_about]: ../active-directory/active-directory-whatis.md "Azure Active Directory nedir?"</span><span class="sxs-lookup"><span data-stu-id="574e7-163">[aad_about]: ../active-directory/active-directory-whatis.md "What is Azure Active Directory?"</span></span>
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
<span data-ttu-id="574e7-164">[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Azure AD için kimlik doğrulama senaryoları"</span><span class="sxs-lookup"><span data-stu-id="574e7-164">[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Authentication Scenarios for Azure AD"</span></span>
<span data-ttu-id="574e7-165">[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Uygulamaları Azure Active Directory ile tümleştirme"</span><span class="sxs-lookup"><span data-stu-id="574e7-165">[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Integrating Applications with Azure Active Directory"</span></span>
[acct_mgmt_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/AccountManagement
[azure_portal]: http://portal.azure.com
[resman_overview]: ../azure-resource-manager/resource-group-overview.md
