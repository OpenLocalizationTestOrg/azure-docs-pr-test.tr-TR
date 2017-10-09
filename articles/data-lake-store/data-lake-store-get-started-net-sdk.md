---
title: "aaaUse hello .NET SDK'sı toodevelop Azure Data Lake Store uygulamalarda | Microsoft Docs"
description: "Azure Data Lake Store .NET SDK toocreate bir Data Lake Store hesabı kullanıp hello Data Lake Store temel işlemleri"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ea57d5a9-2929-4473-9d30-08227912aba7
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/09/2017
ms.author: nitinme
ms.openlocfilehash: cb3a1dfb2f6379f728069d66b0ee77ce0f838fe7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-net-sdk"></a><span data-ttu-id="06a41-103">.NET SDK'yı kullanarak Azure Data Lake Store ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="06a41-103">Get started with Azure Data Lake Store using .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="06a41-104">Portal</span><span class="sxs-lookup"><span data-stu-id="06a41-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="06a41-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="06a41-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="06a41-106">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="06a41-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="06a41-107">Java SDK</span><span class="sxs-lookup"><span data-stu-id="06a41-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="06a41-108">REST API</span><span class="sxs-lookup"><span data-stu-id="06a41-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="06a41-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="06a41-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="06a41-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="06a41-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="06a41-111">Python</span><span class="sxs-lookup"><span data-stu-id="06a41-111">Python</span></span>](data-lake-store-get-started-python.md)
>
>

<span data-ttu-id="06a41-112">Bilgi nasıl toouse hello [Azure Data Lake Store .NET SDK](https://docs.microsoft.com/dotnet/api/overview/azure/data-lake-store?view=azure-dotnet) gibi temel işlemleri tooperform klasörleri oluşturmak, karşıya yükleme ve indirme vb. veri dosyaları. Data Lake hakkında daha fazla bilgi için bkz. [Azure Data Lake Store](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="06a41-112">Learn how toouse hello [Azure Data Lake Store .NET SDK](https://docs.microsoft.com/dotnet/api/overview/azure/data-lake-store?view=azure-dotnet) tooperform basic operations such as create folders, upload and download data files, etc. For more information about Data Lake, see [Azure Data Lake Store](data-lake-store-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="06a41-113">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="06a41-113">Prerequisites</span></span>
* <span data-ttu-id="06a41-114">**Visual Studio 2013, 2015 veya 2017**.</span><span class="sxs-lookup"><span data-stu-id="06a41-114">**Visual Studio 2013, 2015, or 2017**.</span></span> <span data-ttu-id="06a41-115">Visual Studio 2015 güncelleştirme 2 Hello aşağıdaki yönergeleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="06a41-115">hello instructions below use Visual Studio 2015 Update 2.</span></span>

* <span data-ttu-id="06a41-116">**Bir Azure aboneliği**.</span><span class="sxs-lookup"><span data-stu-id="06a41-116">**An Azure subscription**.</span></span> <span data-ttu-id="06a41-117">Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="06a41-117">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="06a41-118">**Azure Data Lake Store hesabı**.</span><span class="sxs-lookup"><span data-stu-id="06a41-118">**Azure Data Lake Store account**.</span></span> <span data-ttu-id="06a41-119">Yönergeler için hesabı, bir toocreate bakın [Azure Data Lake Store ile çalışmaya başlama](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="06a41-119">For instructions on how toocreate an account, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>

* <span data-ttu-id="06a41-120">**Azure Active Directory Uygulaması oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="06a41-120">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="06a41-121">Azure AD ile hello Azure AD uygulama tooauthenticate hello Data Lake Store uygulaması kullanın.</span><span class="sxs-lookup"><span data-stu-id="06a41-121">You use hello Azure AD application tooauthenticate hello Data Lake Store application with Azure AD.</span></span> <span data-ttu-id="06a41-122">Hangi Azure AD ile farklı yaklaşımlara tooauthenticate olan **son kullanıcı kimlik doğrulaması** veya **hizmeti için kimlik doğrulama**.</span><span class="sxs-lookup"><span data-stu-id="06a41-122">There are different approaches tooauthenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="06a41-123">Yönergeler ve hakkında daha fazla bilgi için tooauthenticate, bkz: [son kullanıcı kimlik doğrulaması](data-lake-store-end-user-authenticate-using-active-directory.md) veya [hizmeti için kimlik doğrulama](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="06a41-123">For instructions and more information on how tooauthenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="create-a-net-application"></a><span data-ttu-id="06a41-124">.NET uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="06a41-124">Create a .NET application</span></span>
1. <span data-ttu-id="06a41-125">Visual Studio'yu açın ve bir konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="06a41-125">Open Visual Studio and create a console application.</span></span>
2. <span data-ttu-id="06a41-126">Merhaba gelen **dosya** menüsünde tıklatın **yeni**ve ardından **proje**.</span><span class="sxs-lookup"><span data-stu-id="06a41-126">From hello **File** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="06a41-127">Gelen **yeni proje**değerleri aşağıdaki hello seçin veya yazın:</span><span class="sxs-lookup"><span data-stu-id="06a41-127">From **New Project**, type or select hello following values:</span></span>

   | <span data-ttu-id="06a41-128">Özellik</span><span class="sxs-lookup"><span data-stu-id="06a41-128">Property</span></span> | <span data-ttu-id="06a41-129">Değer</span><span class="sxs-lookup"><span data-stu-id="06a41-129">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="06a41-130">Kategori</span><span class="sxs-lookup"><span data-stu-id="06a41-130">Category</span></span> |<span data-ttu-id="06a41-131">Şablonlar/Visual C#/Windows</span><span class="sxs-lookup"><span data-stu-id="06a41-131">Templates/Visual C#/Windows</span></span> |
   | <span data-ttu-id="06a41-132">Şablon</span><span class="sxs-lookup"><span data-stu-id="06a41-132">Template</span></span> |<span data-ttu-id="06a41-133">Konsol Uygulaması</span><span class="sxs-lookup"><span data-stu-id="06a41-133">Console Application</span></span> |
   | <span data-ttu-id="06a41-134">Ad</span><span class="sxs-lookup"><span data-stu-id="06a41-134">Name</span></span> |<span data-ttu-id="06a41-135">CreateADLApplication</span><span class="sxs-lookup"><span data-stu-id="06a41-135">CreateADLApplication</span></span> |
4. <span data-ttu-id="06a41-136">Tıklatın **Tamam** toocreate hello projesi.</span><span class="sxs-lookup"><span data-stu-id="06a41-136">Click **OK** toocreate hello project.</span></span>
5. <span data-ttu-id="06a41-137">Merhaba Nuget paketleri tooyour projeye ekleyin.</span><span class="sxs-lookup"><span data-stu-id="06a41-137">Add hello Nuget packages tooyour project.</span></span>

   1. <span data-ttu-id="06a41-138">Merhaba Çözüm Gezgini'nde Hello proje adına sağ tıklatın ve **NuGet paketlerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="06a41-138">Right-click hello project name in hello Solution Explorer and click **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="06a41-139">Merhaba, **Nuget Paket Yöneticisi** sekmesinde, olduğundan emin olun **paket kaynağı** çok ayarlanır**nuget.org** ve **dahil et** onay kutusu seçilir.</span><span class="sxs-lookup"><span data-stu-id="06a41-139">In hello **Nuget Package Manager** tab, make sure that **Package source** is set too**nuget.org** and that **Include prerelease** check box is selected.</span></span>
   3. <span data-ttu-id="06a41-140">Arama ve NuGet paketleri aşağıdaki hello yükleyin:</span><span class="sxs-lookup"><span data-stu-id="06a41-140">Search for and install hello following NuGet packages:</span></span>

      * <span data-ttu-id="06a41-141">`Microsoft.Azure.Management.DataLake.Store` - Bu öğreticide v2.1.3-preview kullanılır.</span><span class="sxs-lookup"><span data-stu-id="06a41-141">`Microsoft.Azure.Management.DataLake.Store` - This tutorial uses v2.1.3-preview.</span></span>
      * <span data-ttu-id="06a41-142">`Microsoft.Rest.ClientRuntime.Azure.Authentication` - Bu öğreticide v2.2.12 kullanılır.</span><span class="sxs-lookup"><span data-stu-id="06a41-142">`Microsoft.Rest.ClientRuntime.Azure.Authentication` - This tutorial uses v2.2.12.</span></span>

        <span data-ttu-id="06a41-143">![Nuget kaynağı ekleme](./media/data-lake-store-get-started-net-sdk/data-lake-store-install-nuget-package.png "Yeni bir Azure Data Lake hesabı oluşturma")</span><span class="sxs-lookup"><span data-stu-id="06a41-143">![Add a Nuget source](./media/data-lake-store-get-started-net-sdk/data-lake-store-install-nuget-package.png "Create a new Azure Data Lake account")</span></span>
   4. <span data-ttu-id="06a41-144">Kapat hello **Nuget Paket Yöneticisi**.</span><span class="sxs-lookup"><span data-stu-id="06a41-144">Close hello **Nuget Package Manager**.</span></span>
6. <span data-ttu-id="06a41-145">Açık **Program.cs**hello var olan kodu silin ve deyimleri tooadd başvuruları toonamespaces aşağıdaki hello içerir.</span><span class="sxs-lookup"><span data-stu-id="06a41-145">Open **Program.cs**, delete hello existing code, and then include hello following statements tooadd references toonamespaces.</span></span>

        using System;
        using System.IO;
        using System.Security.Cryptography.X509Certificates; // Required only if you are using an Azure AD application created with certificates
        using System.Threading;

        using Microsoft.Azure.Management.DataLake.Store;
        using Microsoft.Azure.Management.DataLake.Store.Models;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;
        using Microsoft.Rest.Azure.Authentication;

7. <span data-ttu-id="06a41-146">Aşağıda gösterildiği gibi hello değişkenleri bildirin ve Data Lake Store adı ve zaten hello kaynak grubu adı için hello değerler sağlayın.</span><span class="sxs-lookup"><span data-stu-id="06a41-146">Declare hello variables as shown below, and provide hello values for Data Lake Store name and hello resource group name that already exist.</span></span> <span data-ttu-id="06a41-147">Ayrıca, burada sağladığınız hello yerel yolu ve dosya adı hello bilgisayar üzerinde var olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="06a41-147">Also, make sure hello local path and file name you provide here must exist on hello computer.</span></span> <span data-ttu-id="06a41-148">Kod parçacığı hello ad alanı bildirimlerinden sonra aşağıdaki hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="06a41-148">Add hello following code snippet after hello namespace declarations.</span></span>

        namespace SdkSample
        {
            class Program
            {
                private static DataLakeStoreAccountManagementClient _adlsClient;
                private static DataLakeStoreFileSystemManagementClient _adlsFileSystemClient;

                private static string _adlsAccountName;
                private static string _resourceGroupName;
                private static string _location;
                private static string _subId;

                private static void Main(string[] args)
                {
                    _adlsAccountName = "<DATA-LAKE-STORE-NAME>"; // TODO: Replace this value with hello name of your existing Data Lake Store account.
                    _resourceGroupName = "<RESOURCE-GROUP-NAME>"; // TODO: Replace this value with hello name of hello resource group containing your Data Lake Store account.
                    _location = "East US 2";
                    _subId = "<SUBSCRIPTION-ID>";

                    string localFolderPath = @"C:\local_path\"; // TODO: Make sure this exists and can be overwritten.
                    string localFilePath = Path.Combine(localFolderPath, "file.txt"); // TODO: Make sure this exists and can be overwritten.
                    string remoteFolderPath = "/data_lake_path/";
                    string remoteFilePath = Path.Combine(remoteFolderPath, "file.txt");
                }
            }
        }

<span data-ttu-id="06a41-149">Merhaba makale bölümlerini kalan hello nasıl toouse hello kimlik doğrulaması, karşıya dosya yükleme, vb. gibi kullanılabilir .NET yöntemleri tooperform işlemleri görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="06a41-149">In hello remaining sections of hello article, you can see how toouse hello available .NET methods tooperform operations such as authentication, file upload, etc.</span></span>

## <a name="authentication"></a><span data-ttu-id="06a41-150">Kimlik Doğrulaması</span><span class="sxs-lookup"><span data-stu-id="06a41-150">Authentication</span></span>

### <a name="if-you-are-using-end-user-authentication-recommended-for-this-tutorial"></a><span data-ttu-id="06a41-151">Son kullanıcı kimlik doğrulaması kullanıyorsanız (bu öğretici için önerilir)</span><span class="sxs-lookup"><span data-stu-id="06a41-151">If you are using end-user authentication (recommended for this tutorial)</span></span>

<span data-ttu-id="06a41-152">Bu, uygulamanızın var olan bir Azure AD yerel uygulama tooauthenticate kullanın **etkileşimli olarak**, hangi anlamına gelir, gereken tooenter Azure kimlik bilgileriniz istenir.</span><span class="sxs-lookup"><span data-stu-id="06a41-152">Use this with an existing Azure AD native application tooauthenticate your application **interactively**, which means you will be prompted tooenter your Azure credentials.</span></span>

<span data-ttu-id="06a41-153">Kullanım kolaylığı için aşağıdaki hello parçacığı istemci kimliği ve yeniden yönlendirme URI'si hiçbir Azure aboneliği ile çalışması için varsayılan değerleri kullanır.</span><span class="sxs-lookup"><span data-stu-id="06a41-153">For ease of use, hello snippet below uses default values for client ID and redirect URI that will work with any Azure subscription.</span></span> <span data-ttu-id="06a41-154">Bu öğreticide daha hızlı tamamlanmasına toohelp, bu yaklaşım kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="06a41-154">toohelp you complete this tutorial faster, we recommend you use this approach.</span></span> <span data-ttu-id="06a41-155">Merhaba aşağıdaki parçacığında, Kiracı kimliğinizi hello değeri yalnızca belirtin.</span><span class="sxs-lookup"><span data-stu-id="06a41-155">In hello snippet below, just provide hello value for your tenant ID.</span></span> <span data-ttu-id="06a41-156">Verilen hello yönergeleri kullanarak alabilir [Active Directory Uygulama oluşturma](data-lake-store-end-user-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="06a41-156">You can retrieve it using hello instructions provided at [Create an Active Directory Application](data-lake-store-end-user-authenticate-using-active-directory.md).</span></span>

    // User login via interactive popup
    // Use hello client ID of an existing AAD Web application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());
    var tenant_id = "<AAD_tenant_id>"; // Replace this string with hello user's Azure Active Directory tenant ID
    var nativeClientApp_clientId = "1950a258-227b-4e31-a9cf-717495945fc2";
    var activeDirectoryClientSettings = ActiveDirectoryClientSettings.UsePromptOnly(nativeClientApp_clientId, new Uri("urn:ietf:wg:oauth:2.0:oob"));
    var creds = UserTokenProvider.LoginWithPromptAsync(tenant_id, activeDirectoryClientSettings).Result;

<span data-ttu-id="06a41-157">Yukarıdaki bu parçacığında hakkında şeyler tooknow birkaç:</span><span class="sxs-lookup"><span data-stu-id="06a41-157">A couple of things tooknow about this snippet above:</span></span>

* <span data-ttu-id="06a41-158">Hızlı Başlangıç Öğreticisi tamamlamanız toohelp, bu kod parçacığında kullanan bir Azure AD tüm Azure abonelikleri için varsayılan olarak kullanılabilir etki alanı ve istemci kimliği.</span><span class="sxs-lookup"><span data-stu-id="06a41-158">toohelp you complete hello tutorial faster, this snippet uses an an Azure AD domain and client ID that is available by default for all Azure subscriptions.</span></span> <span data-ttu-id="06a41-159">Böylece **bu kod parçacığını uygulamanızda olduğu gibi kullanabilirsiniz**.</span><span class="sxs-lookup"><span data-stu-id="06a41-159">So, you can **use this snippet as-is in your application**.</span></span>
* <span data-ttu-id="06a41-160">Ancak, toouse kendi Azure AD etki alanı isterseniz ve uygulama istemci Kimliğini, Azure AD yerel uygulaması oluşturmanız gerekir ve ardından kullanımı hello Azure AD kimliği, istemci kimliği, Kiracı ve Merhaba uygulaması için yeniden yönlendirme URI'si oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="06a41-160">However, if you do want toouse your own Azure AD domain and application client ID, you must create an Azure AD native application and then use hello Azure AD tenant ID, client ID, and redirect URI for hello application you created.</span></span> <span data-ttu-id="06a41-161">Yönergeler için, bkz: [Data Lake Store ile son kullanıcı kimlik doğrulaması için Active Directory Uygulama oluşturma](data-lake-store-end-user-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="06a41-161">See [Create an Active Directory Application for end-user authentication with Data Lake Store](data-lake-store-end-user-authenticate-using-active-directory.md) for instructions.</span></span>

### <a name="if-you-are-using-service-to-service-authentication-with-client-secret"></a><span data-ttu-id="06a41-162">Gizli anahtar ile hizmetten hizmete kimlik doğrulaması kullanıyorsanız</span><span class="sxs-lookup"><span data-stu-id="06a41-162">If you are using service-to-service authentication with client secret</span></span>
<span data-ttu-id="06a41-163">Merhaba kod parçacığında kullanılan tooauthenticate uygulamanız olabilir **etkileşimsiz**, hello istemci gizli anahtarı kullanarak / anahtar için bir uygulama / hizmet sorumlusu.</span><span class="sxs-lookup"><span data-stu-id="06a41-163">hello following snippet can be used tooauthenticate your application **non-interactively**, using hello client secret / key for an application / service principal.</span></span> <span data-ttu-id="06a41-164">Bunu var olan Azure AD "Web App" uygulaması ile birlikte kullanın.</span><span class="sxs-lookup"><span data-stu-id="06a41-164">Use this with an existing Azure AD "Web App" Application.</span></span> <span data-ttu-id="06a41-165">Yönergeler için toocreate hello Azure AD uygulaması ve tooretrieve nasıl hello istemci Kimliğini ve istemci parolasını aşağıdaki, hello parçacığında gerekli nasıl görürüm [verilerle hizmeti için kimlik doğrulaması için Active Directory Uygulama oluşturma Lake deposu](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="06a41-165">For instructions on how toocreate hello Azure AD web application and how tooretrieve hello client ID and client secret required in hello snippet below, see [Create an Active Directory Application for service-to-service authentication with Data Lake Store](data-lake-store-authenticate-using-active-directory.md).</span></span>

    // Service principal / appplication authentication with client secret / key
    // Use hello client ID of an existing AAD "Web App" application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());

    var domain = "<AAD-directory-domain>";
    var webApp_clientId = "<AAD-application-clientid>";
    var clientSecret = "<AAD-application-client-secret>";
    var clientCredential = new ClientCredential(webApp_clientId, clientSecret);
    var creds = await ApplicationTokenProvider.LoginSilentAsync(domain, clientCredential);

### <a name="if-you-are-using-service-to-service-authentication-with-certificate"></a><span data-ttu-id="06a41-166">Sertifika ile hizmetten hizmete kimlik doğrulaması kullanıyorsanız</span><span class="sxs-lookup"><span data-stu-id="06a41-166">If you are using service-to-service authentication with certificate</span></span>

<span data-ttu-id="06a41-167">Üçüncü, hello seçenek olarak kod parçacığında kullanılan tooauthenticate uygulamanız olabilir **etkileşimsiz**, bir Azure Active Directory uygulaması için hello sertifikayla / hizmet sorumlusu.</span><span class="sxs-lookup"><span data-stu-id="06a41-167">As a third option, hello following snippet can be used tooauthenticate your application **non-interactively**, using hello certificate for an Azure Active Directory application / service principal.</span></span> <span data-ttu-id="06a41-168">Bunu var olan, [Sertifikalı Azure AD Uygulaması](../azure-resource-manager/resource-group-authenticate-service-principal.md) ile birlikte kullanın.</span><span class="sxs-lookup"><span data-stu-id="06a41-168">Use this with an existing [Azure AD Application with certificates](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

    // Service principal / application authentication with certificate
    // Use hello client ID and certificate of an existing AAD "Web App" application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());

    var domain = "<AAD-directory-domain>";
    var webApp_clientId = "<AAD-application-clientid>";
    var clientCert = <AAD-application-client-certificate>
    var clientAssertionCertificate = new ClientAssertionCertificate(webApp_clientId, clientCert);
    var creds = await ApplicationTokenProvider.LoginSilentWithCertificateAsync(domain, clientAssertionCertificate);

## <a name="create-client-objects"></a><span data-ttu-id="06a41-169">İstemci nesneleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="06a41-169">Create client objects</span></span>
<span data-ttu-id="06a41-170">Merhaba aşağıdaki kod parçacığında hello Data Lake Store hesabı ve dosya sistemi kullanılan istemci nesneleri oluşturur tooissue toohello hizmet ister.</span><span class="sxs-lookup"><span data-stu-id="06a41-170">hello following snippet creates hello Data Lake Store account and filesystem client objects, which are used tooissue requests toohello service.</span></span>

    // Create client objects and set hello subscription ID
    _adlsClient = new DataLakeStoreAccountManagementClient(creds) { SubscriptionId = _subId };
    _adlsFileSystemClient = new DataLakeStoreFileSystemManagementClient(creds);

## <a name="list-all-data-lake-store-accounts-within-a-subscription"></a><span data-ttu-id="06a41-171">Bir abonelik içindeki tüm Data Lake Store hesaplarını listeleme</span><span class="sxs-lookup"><span data-stu-id="06a41-171">List all Data Lake Store accounts within a subscription</span></span>
<span data-ttu-id="06a41-172">Merhaba aşağıdaki kod parçacığında belirli bir Azure aboneliği içindeki tüm Data Lake Store hesaplarını listeler.</span><span class="sxs-lookup"><span data-stu-id="06a41-172">hello following snippet lists all Data Lake Store accounts within a given Azure subscription.</span></span>

    // List all ADLS accounts within hello subscription
    public static async Task<List<DataLakeStoreAccount>> ListAdlStoreAccounts()
    {
        var response = await _adlsClient.Account.ListAsync();
        var accounts = new List<DataLakeStoreAccount>(response);

        while (response.NextPageLink != null)
        {
            response = _adlsClient.Account.ListNext(response.NextPageLink);
            accounts.AddRange(response);
        }

        return accounts;
    }

## <a name="create-a-directory"></a><span data-ttu-id="06a41-173">Dizin oluşturma</span><span class="sxs-lookup"><span data-stu-id="06a41-173">Create a directory</span></span>
<span data-ttu-id="06a41-174">Aşağıdaki kod parçacığında gösterildiği hello bir `CreateDirectory` yöntemi toocreate bir dizin içinde bir Data Lake Store hesabı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="06a41-174">hello following snippet shows a `CreateDirectory` method that you can use toocreate a directory within a Data Lake Store account.</span></span>

    // Create a directory
    public static async Task CreateDirectory(string path)
    {
        await _adlsFileSystemClient.FileSystem.MkdirsAsync(_adlsAccountName, path);
    }

## <a name="upload-a-file"></a><span data-ttu-id="06a41-175">Dosyayı karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="06a41-175">Upload a file</span></span>
<span data-ttu-id="06a41-176">Aşağıdaki kod parçacığında gösterildiği hello bir `UploadFile` tooupload kullanabileceğiniz yöntemi dosyaları tooa Data Lake Store hesabı.</span><span class="sxs-lookup"><span data-stu-id="06a41-176">hello following snippet shows an `UploadFile` method that you can use tooupload files tooa Data Lake Store account.</span></span>

    // Upload a file
    public static void UploadFile(string srcFilePath, string destFilePath, bool force = true)
    {
        _adlsFileSystemClient.FileSystem.UploadFile(_adlsAccountName, srcFilePath, destFilePath, overwrite:force);
    }

<span data-ttu-id="06a41-177">Merhaba SDK özyinelemeli karşıya yükleme ve indirme bir yerel dosya yolu ve bir Data Lake Store dosya yolu arasında destekler.</span><span class="sxs-lookup"><span data-stu-id="06a41-177">hello SDK supports recursive upload and download between a local file path and a Data Lake Store file path.</span></span>    

## <a name="get-file-or-directory-info"></a><span data-ttu-id="06a41-178">Dosya veya dizin bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="06a41-178">Get file or directory info</span></span>
<span data-ttu-id="06a41-179">Aşağıdaki kod parçacığında gösterildiği hello bir `GetItemInfo` yöntemi Data Lake Store içinde bir dosya veya dizin kullanılabilir tooretrieve bilgilerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="06a41-179">hello following snippet shows a `GetItemInfo` method that you can use tooretrieve information about a file or directory available in Data Lake Store.</span></span>

    // Get file or directory info
    public static async Task<FileStatusProperties> GetItemInfo(string path)
    {
        return await _adlsFileSystemClient.FileSystem.GetFileStatusAsync(_adlsAccountName, path).FileStatus;
    }

## <a name="list-file-or-directories"></a><span data-ttu-id="06a41-180">Dosyayı veya dizinleri listeleme</span><span class="sxs-lookup"><span data-stu-id="06a41-180">List file or directories</span></span>
<span data-ttu-id="06a41-181">Aşağıdaki kod parçacığında gösterildiği hello bir `ListItem` toolist hello dosya ve dizinleri bir Data Lake Store hesabında kullanabilirsiniz yöntemi.</span><span class="sxs-lookup"><span data-stu-id="06a41-181">hello following snippet shows a `ListItem` method that can use toolist hello file and directories in a Data Lake Store account.</span></span>

    // List files and directories
    public static List<FileStatusProperties> ListItems(string directoryPath)
    {
        return _adlsFileSystemClient.FileSystem.ListFileStatus(_adlsAccountName, directoryPath).FileStatuses.FileStatus.ToList();
    }

## <a name="concatenate-files"></a><span data-ttu-id="06a41-182">Dosyaları birleştirme</span><span class="sxs-lookup"><span data-stu-id="06a41-182">Concatenate files</span></span>
<span data-ttu-id="06a41-183">Aşağıdaki kod parçacığında gösterildiği hello bir `ConcatenateFiles` yöntemi tooconcatenate dosyalarını kullanın.</span><span class="sxs-lookup"><span data-stu-id="06a41-183">hello following snippet shows a `ConcatenateFiles` method that you use tooconcatenate files.</span></span>

    // Concatenate files
    public static Task ConcatenateFiles(string[] srcFilePaths, string destFilePath)
    {
        await _adlsFileSystemClient.FileSystem.ConcatAsync(_adlsAccountName, destFilePath, srcFilePaths);
    }

## <a name="append-tooa-file"></a><span data-ttu-id="06a41-184">Tooa dosya ekleme</span><span class="sxs-lookup"><span data-stu-id="06a41-184">Append tooa file</span></span>
<span data-ttu-id="06a41-185">Aşağıdaki kod parçacığında gösterildiği hello bir `AppendToFile` append bir Data Lake Store hesabında zaten depolanmış verileri tooa dosyası kullandığınız yöntemi.</span><span class="sxs-lookup"><span data-stu-id="06a41-185">hello following snippet shows a `AppendToFile` method that you use append data tooa file already stored in a Data Lake Store account.</span></span>

    // Append toofile
    public static async Task AppendToFile(string path, string content)
    {
        using (var stream = new MemoryStream(Encoding.UTF8.GetBytes(content)))
        {
            await _adlsFileSystemClient.FileSystem.AppendAsync(_adlsAccountName, path, stream);
        }
    }

## <a name="download-a-file"></a><span data-ttu-id="06a41-186">Dosya indirme</span><span class="sxs-lookup"><span data-stu-id="06a41-186">Download a file</span></span>
<span data-ttu-id="06a41-187">Aşağıdaki kod parçacığında gösterildiği hello bir `DownloadFile` yöntemi toodownload bir dosyadan bir Data Lake Store hesabı kullanın.</span><span class="sxs-lookup"><span data-stu-id="06a41-187">hello following snippet shows a `DownloadFile` method that you use toodownload a file from a Data Lake Store account.</span></span>

    // Download file
    public static void DownloadFile(string srcFilePath, string destFilePath)
    {
         _adlsFileSystemClient.FileSystem.DownloadFile(_adlsAccountName, srcFilePath, destFilePath);
    }

## <a name="next-steps"></a><span data-ttu-id="06a41-188">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="06a41-188">Next steps</span></span>
* [<span data-ttu-id="06a41-189">Data Lake Store'da verilerin güvenliğini sağlama</span><span class="sxs-lookup"><span data-stu-id="06a41-189">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="06a41-190">Azure Data Lake Analytics'i Data Lake Store ile kullanma</span><span class="sxs-lookup"><span data-stu-id="06a41-190">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="06a41-191">Azure HDInsight'ı Data Lake Store ile kullanma</span><span class="sxs-lookup"><span data-stu-id="06a41-191">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
* [<span data-ttu-id="06a41-192">Data Lake Store .NET SDK Başvurusu</span><span class="sxs-lookup"><span data-stu-id="06a41-192">Data Lake Store .NET SDK Reference</span></span>](https://docs.microsoft.com/dotnet/api/?view=azuremgmtdatalakestore-2.1.0-preview&term=DataLake.Store)
* [<span data-ttu-id="06a41-193">Data Lake Store REST Başvurusu</span><span class="sxs-lookup"><span data-stu-id="06a41-193">Data Lake Store REST Reference</span></span>](https://msdn.microsoft.com/library/mt693424.aspx)
