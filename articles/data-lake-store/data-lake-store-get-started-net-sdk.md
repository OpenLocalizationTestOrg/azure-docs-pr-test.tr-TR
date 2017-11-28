---
title: "Azure Data Lake Store’da uygulama geliştirmek için .NET SDK'sını kullanma | Microsoft Docs"
description: "Bir Data Lake Store hesabı oluşturmak ve Data Lake Store'da temel işlemleri gerçekleştirmek için Azure Data Lake Store .NET SDK’sını kullanma"
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
ms.openlocfilehash: 70f94a07b0102e3135eaf85e5877e3502762d7e3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-azure-data-lake-store-using-net-sdk"></a><span data-ttu-id="1ccb6-103">.NET SDK'yı kullanarak Azure Data Lake Store ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="1ccb6-103">Get started with Azure Data Lake Store using .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1ccb6-104">Portal</span><span class="sxs-lookup"><span data-stu-id="1ccb6-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="1ccb6-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1ccb6-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="1ccb6-106">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="1ccb6-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="1ccb6-107">Java SDK</span><span class="sxs-lookup"><span data-stu-id="1ccb6-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="1ccb6-108">REST API</span><span class="sxs-lookup"><span data-stu-id="1ccb6-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="1ccb6-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="1ccb6-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="1ccb6-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="1ccb6-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="1ccb6-111">Python</span><span class="sxs-lookup"><span data-stu-id="1ccb6-111">Python</span></span>](data-lake-store-get-started-python.md)
>
>

<span data-ttu-id="1ccb6-112">Klasör oluşturma, veri dosyalarını karşıya yükleme ve indirme gibi temel işlemler gerçekleştirmek üzere [Azure Data Lake Store .NET SDK’sını](https://docs.microsoft.com/dotnet/api/overview/azure/data-lake-store?view=azure-dotnet) kullanma hakkında bilgi edinin. Data Lake hakkında daha fazla bilgi için bkz. [Azure Data Lake Store](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1ccb6-112">Learn how to use the [Azure Data Lake Store .NET SDK](https://docs.microsoft.com/dotnet/api/overview/azure/data-lake-store?view=azure-dotnet) to perform basic operations such as create folders, upload and download data files, etc. For more information about Data Lake, see [Azure Data Lake Store](data-lake-store-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1ccb6-113">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="1ccb6-113">Prerequisites</span></span>
* <span data-ttu-id="1ccb6-114">**Visual Studio 2013, 2015 veya 2017**.</span><span class="sxs-lookup"><span data-stu-id="1ccb6-114">**Visual Studio 2013, 2015, or 2017**.</span></span> <span data-ttu-id="1ccb6-115">Aşağıdaki yönergelerde Visual Studio 2015 Güncelleştirme 2 kullanılmıştır.</span><span class="sxs-lookup"><span data-stu-id="1ccb6-115">The instructions below use Visual Studio 2015 Update 2.</span></span>

* <span data-ttu-id="1ccb6-116">**Bir Azure aboneliği**.</span><span class="sxs-lookup"><span data-stu-id="1ccb6-116">**An Azure subscription**.</span></span> <span data-ttu-id="1ccb6-117">Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1ccb6-117">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="1ccb6-118">**Azure Data Lake Store hesabı**.</span><span class="sxs-lookup"><span data-stu-id="1ccb6-118">**Azure Data Lake Store account**.</span></span> <span data-ttu-id="1ccb6-119">Hesap oluşturmaya ilişkin yönergeler için bkz. [Azure Data Lake Store kullanmaya başlama](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="1ccb6-119">For instructions on how to create an account, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>

* <span data-ttu-id="1ccb6-120">**Azure Active Directory Uygulaması oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="1ccb6-120">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="1ccb6-121">Data Lake Store uygulamasında Azure AD ile kimlik doğrulaması yapmak için Azure AD uygulamasını kullanın.</span><span class="sxs-lookup"><span data-stu-id="1ccb6-121">You use the Azure AD application to authenticate the Data Lake Store application with Azure AD.</span></span> <span data-ttu-id="1ccb6-122">Azure AD kimlik doğrulaması için **son kullanıcı kimlik doğrulaması** veya **hizmetten hizmete kimlik doğrulama** gibi farklı yaklaşımlar bulunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="1ccb6-122">There are different approaches to authenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="1ccb6-123">Kimlik doğrulaması gerçekleştirmeyle ilgili yönergeler ve daha fazla bilgi için [Son kullanıcı kimlik doğrulaması](data-lake-store-end-user-authenticate-using-active-directory.md) veya [Hizmetten hizmete kimlik doğrulaması](data-lake-store-authenticate-using-active-directory.md) bölümlerine göz atın.</span><span class="sxs-lookup"><span data-stu-id="1ccb6-123">For instructions and more information on how to authenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="create-a-net-application"></a><span data-ttu-id="1ccb6-124">.NET uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="1ccb6-124">Create a .NET application</span></span>
1. <span data-ttu-id="1ccb6-125">Visual Studio'yu açın ve bir konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1ccb6-125">Open Visual Studio and create a console application.</span></span>
2. <span data-ttu-id="1ccb6-126">**Dosya** menüsünde **Yeni**'ye ve ardından **Proje**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1ccb6-126">From the **File** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="1ccb6-127">**Yeni Proje** bölümünden, aşağıdaki değerleri yazın veya seçin:</span><span class="sxs-lookup"><span data-stu-id="1ccb6-127">From **New Project**, type or select the following values:</span></span>

   | <span data-ttu-id="1ccb6-128">Özellik</span><span class="sxs-lookup"><span data-stu-id="1ccb6-128">Property</span></span> | <span data-ttu-id="1ccb6-129">Değer</span><span class="sxs-lookup"><span data-stu-id="1ccb6-129">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="1ccb6-130">Kategori</span><span class="sxs-lookup"><span data-stu-id="1ccb6-130">Category</span></span> |<span data-ttu-id="1ccb6-131">Şablonlar/Visual C#/Windows</span><span class="sxs-lookup"><span data-stu-id="1ccb6-131">Templates/Visual C#/Windows</span></span> |
   | <span data-ttu-id="1ccb6-132">Şablon</span><span class="sxs-lookup"><span data-stu-id="1ccb6-132">Template</span></span> |<span data-ttu-id="1ccb6-133">Konsol Uygulaması</span><span class="sxs-lookup"><span data-stu-id="1ccb6-133">Console Application</span></span> |
   | <span data-ttu-id="1ccb6-134">Ad</span><span class="sxs-lookup"><span data-stu-id="1ccb6-134">Name</span></span> |<span data-ttu-id="1ccb6-135">CreateADLApplication</span><span class="sxs-lookup"><span data-stu-id="1ccb6-135">CreateADLApplication</span></span> |
4. <span data-ttu-id="1ccb6-136">Projeyi oluşturmak için **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1ccb6-136">Click **OK** to create the project.</span></span>
5. <span data-ttu-id="1ccb6-137">Nuget paketlerini projenize ekleyin.</span><span class="sxs-lookup"><span data-stu-id="1ccb6-137">Add the Nuget packages to your project.</span></span>

   1. <span data-ttu-id="1ccb6-138">Çözüm Gezgini'nde proje adına sağ tıklayın ve **NuGet Paketlerini Yönet**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1ccb6-138">Right-click the project name in the Solution Explorer and click **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="1ccb6-139">**Nuget Paket Yöneticisi** sekmesinde, **Paket kaynağının** **nuget.org** olarak ayarlandığından ve **Ön sürümü dahil et** onay kutusunun işaretli olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="1ccb6-139">In the **Nuget Package Manager** tab, make sure that **Package source** is set to **nuget.org** and that **Include prerelease** check box is selected.</span></span>
   3. <span data-ttu-id="1ccb6-140">Aşağıdaki NuGet paketlerini arayıp yükleyin:</span><span class="sxs-lookup"><span data-stu-id="1ccb6-140">Search for and install the following NuGet packages:</span></span>

      * <span data-ttu-id="1ccb6-141">`Microsoft.Azure.Management.DataLake.Store` - Bu öğreticide v2.1.3-preview kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1ccb6-141">`Microsoft.Azure.Management.DataLake.Store` - This tutorial uses v2.1.3-preview.</span></span>
      * <span data-ttu-id="1ccb6-142">`Microsoft.Rest.ClientRuntime.Azure.Authentication` - Bu öğreticide v2.2.12 kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1ccb6-142">`Microsoft.Rest.ClientRuntime.Azure.Authentication` - This tutorial uses v2.2.12.</span></span>

        <span data-ttu-id="1ccb6-143">![Nuget kaynağı ekleme](./media/data-lake-store-get-started-net-sdk/data-lake-store-install-nuget-package.png "Yeni bir Azure Data Lake hesabı oluşturma")</span><span class="sxs-lookup"><span data-stu-id="1ccb6-143">![Add a Nuget source](./media/data-lake-store-get-started-net-sdk/data-lake-store-install-nuget-package.png "Create a new Azure Data Lake account")</span></span>
   4. <span data-ttu-id="1ccb6-144">**Nuget Paket Yöneticisi**'ni kapatın.</span><span class="sxs-lookup"><span data-stu-id="1ccb6-144">Close the **Nuget Package Manager**.</span></span>
6. <span data-ttu-id="1ccb6-145">**Program.cs** öğesini açın, var olan kodu silin ve ardından ad alanlarına başvurular eklemek için aşağıdaki deyimleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="1ccb6-145">Open **Program.cs**, delete the existing code, and then include the following statements to add references to namespaces.</span></span>

        using System;
        using System.IO;
        using System.Security.Cryptography.X509Certificates; // Required only if you are using an Azure AD application created with certificates
        using System.Threading;

        using Microsoft.Azure.Management.DataLake.Store;
        using Microsoft.Azure.Management.DataLake.Store.Models;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;
        using Microsoft.Rest.Azure.Authentication;

7. <span data-ttu-id="1ccb6-146">Aşağıda gösterildiği gibi değişkenleri tanımlayın ve Data Lake Store adına ve zaten var olan kaynak grubu adına yönelik değerleri sağlayın.</span><span class="sxs-lookup"><span data-stu-id="1ccb6-146">Declare the variables as shown below, and provide the values for Data Lake Store name and the resource group name that already exist.</span></span> <span data-ttu-id="1ccb6-147">Ayrıca, burada sağladığınız yerel yolun ve dosya adının bilgisayar üzerinde var olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="1ccb6-147">Also, make sure the local path and file name you provide here must exist on the computer.</span></span> <span data-ttu-id="1ccb6-148">Aşağıdaki kod parçacığını ad alanı bildirimlerinden sonra ekleyin.</span><span class="sxs-lookup"><span data-stu-id="1ccb6-148">Add the following code snippet after the namespace declarations.</span></span>

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
                    _adlsAccountName = "<DATA-LAKE-STORE-NAME>"; // TODO: Replace this value with the name of your existing Data Lake Store account.
                    _resourceGroupName = "<RESOURCE-GROUP-NAME>"; // TODO: Replace this value with the name of the resource group containing your Data Lake Store account.
                    _location = "East US 2";
                    _subId = "<SUBSCRIPTION-ID>";

                    string localFolderPath = @"C:\local_path\"; // TODO: Make sure this exists and can be overwritten.
                    string localFilePath = Path.Combine(localFolderPath, "file.txt"); // TODO: Make sure this exists and can be overwritten.
                    string remoteFolderPath = "/data_lake_path/";
                    string remoteFilePath = Path.Combine(remoteFolderPath, "file.txt");
                }
            }
        }

<span data-ttu-id="1ccb6-149">Makalenin geriye kalan bölümlerinde, kullanılabilir .NET yöntemlerinin, kimlik doğrulama, dosyayı karşıya yükleme vb. işlemleri gerçekleştirmek üzere nasıl kullanılacağını öğrenebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1ccb6-149">In the remaining sections of the article, you can see how to use the available .NET methods to perform operations such as authentication, file upload, etc.</span></span>

## <a name="authentication"></a><span data-ttu-id="1ccb6-150">Kimlik Doğrulaması</span><span class="sxs-lookup"><span data-stu-id="1ccb6-150">Authentication</span></span>

### <a name="if-you-are-using-end-user-authentication-recommended-for-this-tutorial"></a><span data-ttu-id="1ccb6-151">Son kullanıcı kimlik doğrulaması kullanıyorsanız (bu öğretici için önerilir)</span><span class="sxs-lookup"><span data-stu-id="1ccb6-151">If you are using end-user authentication (recommended for this tutorial)</span></span>

<span data-ttu-id="1ccb6-152">Uygulamanızın kimliğini **etkileşimli olarak** doğrulamak üzere bunu var olan bir Azure AD yerle uygulamasıyla kullanın, bunun anlamı Azure kimlik bilgilerinizi girmeniz isteneceğidir.</span><span class="sxs-lookup"><span data-stu-id="1ccb6-152">Use this with an existing Azure AD native application to authenticate your application **interactively**, which means you will be prompted to enter your Azure credentials.</span></span>

<span data-ttu-id="1ccb6-153">Kullanım kolaylığı için, aşağıdaki kod parçacığında, herhangi bir Azure aboneliğiyle çalışacak yönlendirme URI’si ve istemci kimliği için varsayılan değerler kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1ccb6-153">For ease of use, the snippet below uses default values for client ID and redirect URI that will work with any Azure subscription.</span></span> <span data-ttu-id="1ccb6-154">Bu öğreticiyi daha hızlı tamamlamanıza yardımcı olması için bu yaklaşımı kullanmanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="1ccb6-154">To help you complete this tutorial faster, we recommend you use this approach.</span></span> <span data-ttu-id="1ccb6-155">Aşağıdaki kod parçacığında, yalnızca kiracı kimliğiniz için değeri sağlayın.</span><span class="sxs-lookup"><span data-stu-id="1ccb6-155">In the snippet below, just provide the value for your tenant ID.</span></span> <span data-ttu-id="1ccb6-156">[Active Directory Uygulaması oluşturma](data-lake-store-end-user-authenticate-using-active-directory.md) kısmında verilen yönergeleri kullanarak bunu alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1ccb6-156">You can retrieve it using the instructions provided at [Create an Active Directory Application](data-lake-store-end-user-authenticate-using-active-directory.md).</span></span>

    // User login via interactive popup
    // Use the client ID of an existing AAD Web application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());
    var tenant_id = "<AAD_tenant_id>"; // Replace this string with the user's Azure Active Directory tenant ID
    var nativeClientApp_clientId = "1950a258-227b-4e31-a9cf-717495945fc2";
    var activeDirectoryClientSettings = ActiveDirectoryClientSettings.UsePromptOnly(nativeClientApp_clientId, new Uri("urn:ietf:wg:oauth:2.0:oob"));
    var creds = UserTokenProvider.LoginWithPromptAsync(tenant_id, activeDirectoryClientSettings).Result;

<span data-ttu-id="1ccb6-157">Yukarıdaki bu kod parçacığı hakkında bilmeniz gereken birkaç şey:</span><span class="sxs-lookup"><span data-stu-id="1ccb6-157">A couple of things to know about this snippet above:</span></span>

* <span data-ttu-id="1ccb6-158">Öğreticiyi daha hızlı tamamlamanıza yardımcı olmak üzere bu kod parçacığı tüm Azure abonelikleri için varsayılan olarak kullanılabilen bir Azure AD etki alanı ve istemci kimliği kullanır.</span><span class="sxs-lookup"><span data-stu-id="1ccb6-158">To help you complete the tutorial faster, this snippet uses an an Azure AD domain and client ID that is available by default for all Azure subscriptions.</span></span> <span data-ttu-id="1ccb6-159">Böylece **bu kod parçacığını uygulamanızda olduğu gibi kullanabilirsiniz**.</span><span class="sxs-lookup"><span data-stu-id="1ccb6-159">So, you can **use this snippet as-is in your application**.</span></span>
* <span data-ttu-id="1ccb6-160">Ancak, kendi Azure AD etki alanınızı ve uygulama istemci kimliğinizi kullanmak istemiyorsanız, bir Azure AD yerel uygulaması oluşturmanız ve ardından oluşturduğunuz uygulamaya ait Azure AD kiracı kimliği, istemci kimliği ve yeniden yönlendirme URI’sini kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1ccb6-160">However, if you do want to use your own Azure AD domain and application client ID, you must create an Azure AD native application and then use the Azure AD tenant ID, client ID, and redirect URI for the application you created.</span></span> <span data-ttu-id="1ccb6-161">Yönergeler için, bkz: [Data Lake Store ile son kullanıcı kimlik doğrulaması için Active Directory Uygulama oluşturma](data-lake-store-end-user-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="1ccb6-161">See [Create an Active Directory Application for end-user authentication with Data Lake Store](data-lake-store-end-user-authenticate-using-active-directory.md) for instructions.</span></span>

### <a name="if-you-are-using-service-to-service-authentication-with-client-secret"></a><span data-ttu-id="1ccb6-162">Gizli anahtar ile hizmetten hizmete kimlik doğrulaması kullanıyorsanız</span><span class="sxs-lookup"><span data-stu-id="1ccb6-162">If you are using service-to-service authentication with client secret</span></span>
<span data-ttu-id="1ccb6-163">Gizli anahtar / uygulama anahtarı / hizmet sorumlusu kullanılarak aşağıdaki kod parçacığı uygulamanızın **etkileşimli olmayan** kimlik doğrulaması için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="1ccb6-163">The following snippet can be used to authenticate your application **non-interactively**, using the client secret / key for an application / service principal.</span></span> <span data-ttu-id="1ccb6-164">Bunu var olan Azure AD "Web App" uygulaması ile birlikte kullanın.</span><span class="sxs-lookup"><span data-stu-id="1ccb6-164">Use this with an existing Azure AD "Web App" Application.</span></span> <span data-ttu-id="1ccb6-165">Azure AD web uygulamasının nasıl oluşturulacağını ve aşağıdaki kod parçacığında gereken istemci kimliği ile istemci parolasının nasıl alınacağıyla ilgili yönergeler için, bkz: [Data Lake Store ile servis-servis kimlik doğrulaması için Active Directory Uygulaması oluşturma](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="1ccb6-165">For instructions on how to create the Azure AD web application and how to retrieve the client ID and client secret required in the snippet below, see [Create an Active Directory Application for service-to-service authentication with Data Lake Store](data-lake-store-authenticate-using-active-directory.md).</span></span>

    // Service principal / appplication authentication with client secret / key
    // Use the client ID of an existing AAD "Web App" application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());

    var domain = "<AAD-directory-domain>";
    var webApp_clientId = "<AAD-application-clientid>";
    var clientSecret = "<AAD-application-client-secret>";
    var clientCredential = new ClientCredential(webApp_clientId, clientSecret);
    var creds = await ApplicationTokenProvider.LoginSilentAsync(domain, clientCredential);

### <a name="if-you-are-using-service-to-service-authentication-with-certificate"></a><span data-ttu-id="1ccb6-166">Sertifika ile hizmetten hizmete kimlik doğrulaması kullanıyorsanız</span><span class="sxs-lookup"><span data-stu-id="1ccb6-166">If you are using service-to-service authentication with certificate</span></span>

<span data-ttu-id="1ccb6-167">Üçüncü bir seçenek olarak, bir Azure Active Directory uygulama sertifikası / hizmet sorumlusu kullanılarak aşağıdaki kod parçacığı uygulamanızın **etkileşimli olmayan** kimlik doğrulaması için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="1ccb6-167">As a third option, the following snippet can be used to authenticate your application **non-interactively**, using the certificate for an Azure Active Directory application / service principal.</span></span> <span data-ttu-id="1ccb6-168">Bunu var olan, [Sertifikalı Azure AD Uygulaması](../azure-resource-manager/resource-group-authenticate-service-principal.md) ile birlikte kullanın.</span><span class="sxs-lookup"><span data-stu-id="1ccb6-168">Use this with an existing [Azure AD Application with certificates](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

    // Service principal / application authentication with certificate
    // Use the client ID and certificate of an existing AAD "Web App" application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());

    var domain = "<AAD-directory-domain>";
    var webApp_clientId = "<AAD-application-clientid>";
    var clientCert = <AAD-application-client-certificate>
    var clientAssertionCertificate = new ClientAssertionCertificate(webApp_clientId, clientCert);
    var creds = await ApplicationTokenProvider.LoginSilentWithCertificateAsync(domain, clientAssertionCertificate);

## <a name="create-client-objects"></a><span data-ttu-id="1ccb6-169">İstemci nesneleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="1ccb6-169">Create client objects</span></span>
<span data-ttu-id="1ccb6-170">Aşağıdaki kod parçacığı Data Lake Store hesabını ve hizmete verme isteği göndermek için kullanılan dosya sistemi istemci nesnelerini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1ccb6-170">The following snippet creates the Data Lake Store account and filesystem client objects, which are used to issue requests to the service.</span></span>

    // Create client objects and set the subscription ID
    _adlsClient = new DataLakeStoreAccountManagementClient(creds) { SubscriptionId = _subId };
    _adlsFileSystemClient = new DataLakeStoreFileSystemManagementClient(creds);

## <a name="list-all-data-lake-store-accounts-within-a-subscription"></a><span data-ttu-id="1ccb6-171">Bir abonelik içindeki tüm Data Lake Store hesaplarını listeleme</span><span class="sxs-lookup"><span data-stu-id="1ccb6-171">List all Data Lake Store accounts within a subscription</span></span>
<span data-ttu-id="1ccb6-172">Aşağıdaki kod parçacığı belirli bir Azure aboneliği içindeki tüm Data Lake Store hesaplarını listeler.</span><span class="sxs-lookup"><span data-stu-id="1ccb6-172">The following snippet lists all Data Lake Store accounts within a given Azure subscription.</span></span>

    // List all ADLS accounts within the subscription
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

## <a name="create-a-directory"></a><span data-ttu-id="1ccb6-173">Dizin oluşturma</span><span class="sxs-lookup"><span data-stu-id="1ccb6-173">Create a directory</span></span>
<span data-ttu-id="1ccb6-174">Aşağıdaki kod parçacığında, bir Data Lake Store hesabında dizin oluşturmak için kullanabileceğiniz bir `CreateDirectory` yöntemi gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="1ccb6-174">The following snippet shows a `CreateDirectory` method that you can use to create a directory within a Data Lake Store account.</span></span>

    // Create a directory
    public static async Task CreateDirectory(string path)
    {
        await _adlsFileSystemClient.FileSystem.MkdirsAsync(_adlsAccountName, path);
    }

## <a name="upload-a-file"></a><span data-ttu-id="1ccb6-175">Dosyayı karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="1ccb6-175">Upload a file</span></span>
<span data-ttu-id="1ccb6-176">Aşağıdaki kod parçacığında, bir Data Lake Store hesabına dosya yüklemek için kullanabileceğiniz bir `UploadFile` yöntemi gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="1ccb6-176">The following snippet shows an `UploadFile` method that you can use to upload files to a Data Lake Store account.</span></span>

    // Upload a file
    public static void UploadFile(string srcFilePath, string destFilePath, bool force = true)
    {
        _adlsFileSystemClient.FileSystem.UploadFile(_adlsAccountName, srcFilePath, destFilePath, overwrite:force);
    }

<span data-ttu-id="1ccb6-177">SDK bir yerel dosya ile Data Lake Store dosya yolu arasında yinelemeli karşıya yükleme ve indirmeyi destekler.</span><span class="sxs-lookup"><span data-stu-id="1ccb6-177">The SDK supports recursive upload and download between a local file path and a Data Lake Store file path.</span></span>    

## <a name="get-file-or-directory-info"></a><span data-ttu-id="1ccb6-178">Dosya veya dizin bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="1ccb6-178">Get file or directory info</span></span>
<span data-ttu-id="1ccb6-179">Aşağıdaki kod parçacığında, Data Lake Store'da kullanılabilir olan bir dosya veya dizin ile ilgili bilgileri almak için kullanabileceğiniz bir `GetItemInfo` yöntemi gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="1ccb6-179">The following snippet shows a `GetItemInfo` method that you can use to retrieve information about a file or directory available in Data Lake Store.</span></span>

    // Get file or directory info
    public static async Task<FileStatusProperties> GetItemInfo(string path)
    {
        return await _adlsFileSystemClient.FileSystem.GetFileStatusAsync(_adlsAccountName, path).FileStatus;
    }

## <a name="list-file-or-directories"></a><span data-ttu-id="1ccb6-180">Dosyayı veya dizinleri listeleme</span><span class="sxs-lookup"><span data-stu-id="1ccb6-180">List file or directories</span></span>
<span data-ttu-id="1ccb6-181">Aşağıdaki kod parçacığında, bir Data Lake Store hesabındaki dosyaları ve dizinleri listelemek için kullanabileceğiniz bir `ListItem` yöntemi gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="1ccb6-181">The following snippet shows a `ListItem` method that can use to list the file and directories in a Data Lake Store account.</span></span>

    // List files and directories
    public static List<FileStatusProperties> ListItems(string directoryPath)
    {
        return _adlsFileSystemClient.FileSystem.ListFileStatus(_adlsAccountName, directoryPath).FileStatuses.FileStatus.ToList();
    }

## <a name="concatenate-files"></a><span data-ttu-id="1ccb6-182">Dosyaları birleştirme</span><span class="sxs-lookup"><span data-stu-id="1ccb6-182">Concatenate files</span></span>
<span data-ttu-id="1ccb6-183">Aşağıdaki kod parçacığında, dosyaları birleştirmek için kullanabileceğiniz bir `ConcatenateFiles` yöntemi gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="1ccb6-183">The following snippet shows a `ConcatenateFiles` method that you use to concatenate files.</span></span>

    // Concatenate files
    public static Task ConcatenateFiles(string[] srcFilePaths, string destFilePath)
    {
        await _adlsFileSystemClient.FileSystem.ConcatAsync(_adlsAccountName, destFilePath, srcFilePaths);
    }

## <a name="append-to-a-file"></a><span data-ttu-id="1ccb6-184">Dosyanın sonuna ekleme</span><span class="sxs-lookup"><span data-stu-id="1ccb6-184">Append to a file</span></span>
<span data-ttu-id="1ccb6-185">Aşağıdaki kod parçacığında, bir Data Lake Store hesabında zaten depolanmış olan bir dosyanın sonuna veri eklemek için kullanabileceğiniz bir `AppendToFile` yöntemi gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="1ccb6-185">The following snippet shows a `AppendToFile` method that you use append data to a file already stored in a Data Lake Store account.</span></span>

    // Append to file
    public static async Task AppendToFile(string path, string content)
    {
        using (var stream = new MemoryStream(Encoding.UTF8.GetBytes(content)))
        {
            await _adlsFileSystemClient.FileSystem.AppendAsync(_adlsAccountName, path, stream);
        }
    }

## <a name="download-a-file"></a><span data-ttu-id="1ccb6-186">Dosya indirme</span><span class="sxs-lookup"><span data-stu-id="1ccb6-186">Download a file</span></span>
<span data-ttu-id="1ccb6-187">Aşağıdaki kod parçacığında, bir Data Lake Store hesabındaki bir dosyayı indirmek için kullanabileceğiniz bir `DownloadFile` yöntemi gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="1ccb6-187">The following snippet shows a `DownloadFile` method that you use to download a file from a Data Lake Store account.</span></span>

    // Download file
    public static void DownloadFile(string srcFilePath, string destFilePath)
    {
         _adlsFileSystemClient.FileSystem.DownloadFile(_adlsAccountName, srcFilePath, destFilePath);
    }

## <a name="next-steps"></a><span data-ttu-id="1ccb6-188">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1ccb6-188">Next steps</span></span>
* [<span data-ttu-id="1ccb6-189">Data Lake Store'da verilerin güvenliğini sağlama</span><span class="sxs-lookup"><span data-stu-id="1ccb6-189">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="1ccb6-190">Azure Data Lake Analytics'i Data Lake Store ile kullanma</span><span class="sxs-lookup"><span data-stu-id="1ccb6-190">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="1ccb6-191">Azure HDInsight'ı Data Lake Store ile kullanma</span><span class="sxs-lookup"><span data-stu-id="1ccb6-191">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
* [<span data-ttu-id="1ccb6-192">Data Lake Store .NET SDK Başvurusu</span><span class="sxs-lookup"><span data-stu-id="1ccb6-192">Data Lake Store .NET SDK Reference</span></span>](https://docs.microsoft.com/dotnet/api/?view=azuremgmtdatalakestore-2.1.0-preview&term=DataLake.Store)
* [<span data-ttu-id="1ccb6-193">Data Lake Store REST Başvurusu</span><span class="sxs-lookup"><span data-stu-id="1ccb6-193">Data Lake Store REST Reference</span></span>](https://msdn.microsoft.com/library/mt693424.aspx)
