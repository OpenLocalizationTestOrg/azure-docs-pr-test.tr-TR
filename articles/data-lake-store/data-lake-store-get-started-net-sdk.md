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
# <a name="get-started-with-azure-data-lake-store-using-net-sdk"></a>.NET SDK'yı kullanarak Azure Data Lake Store ile çalışmaya başlama
> [!div class="op_single_selector"]
> * [Portal](data-lake-store-get-started-portal.md)
> * [PowerShell](data-lake-store-get-started-powershell.md)
> * [.NET SDK](data-lake-store-get-started-net-sdk.md)
> * [Java SDK](data-lake-store-get-started-java-sdk.md)
> * [REST API](data-lake-store-get-started-rest-api.md)
> * [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md)
> * [Node.js](data-lake-store-manage-use-nodejs.md)
> * [Python](data-lake-store-get-started-python.md)
>
>

Bilgi nasıl toouse hello [Azure Data Lake Store .NET SDK](https://docs.microsoft.com/dotnet/api/overview/azure/data-lake-store?view=azure-dotnet) gibi temel işlemleri tooperform klasörleri oluşturmak, karşıya yükleme ve indirme vb. veri dosyaları. Data Lake hakkında daha fazla bilgi için bkz. [Azure Data Lake Store](data-lake-store-overview.md).

## <a name="prerequisites"></a>Ön koşullar
* **Visual Studio 2013, 2015 veya 2017**. Visual Studio 2015 güncelleştirme 2 Hello aşağıdaki yönergeleri kullanın.

* **Bir Azure aboneliği**. Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/pricing/free-trial/).

* **Azure Data Lake Store hesabı**. Yönergeler için hesabı, bir toocreate bakın [Azure Data Lake Store ile çalışmaya başlama](data-lake-store-get-started-portal.md)

* **Azure Active Directory Uygulaması oluşturma**. Azure AD ile hello Azure AD uygulama tooauthenticate hello Data Lake Store uygulaması kullanın. Hangi Azure AD ile farklı yaklaşımlara tooauthenticate olan **son kullanıcı kimlik doğrulaması** veya **hizmeti için kimlik doğrulama**. Yönergeler ve hakkında daha fazla bilgi için tooauthenticate, bkz: [son kullanıcı kimlik doğrulaması](data-lake-store-end-user-authenticate-using-active-directory.md) veya [hizmeti için kimlik doğrulama](data-lake-store-authenticate-using-active-directory.md).

## <a name="create-a-net-application"></a>.NET uygulaması oluşturma
1. Visual Studio'yu açın ve bir konsol uygulaması oluşturun.
2. Merhaba gelen **dosya** menüsünde tıklatın **yeni**ve ardından **proje**.
3. Gelen **yeni proje**değerleri aşağıdaki hello seçin veya yazın:

   | Özellik | Değer |
   | --- | --- |
   | Kategori |Şablonlar/Visual C#/Windows |
   | Şablon |Konsol Uygulaması |
   | Ad |CreateADLApplication |
4. Tıklatın **Tamam** toocreate hello projesi.
5. Merhaba Nuget paketleri tooyour projeye ekleyin.

   1. Merhaba Çözüm Gezgini'nde Hello proje adına sağ tıklatın ve **NuGet paketlerini Yönet**.
   2. Merhaba, **Nuget Paket Yöneticisi** sekmesinde, olduğundan emin olun **paket kaynağı** çok ayarlanır**nuget.org** ve **dahil et** onay kutusu seçilir.
   3. Arama ve NuGet paketleri aşağıdaki hello yükleyin:

      * `Microsoft.Azure.Management.DataLake.Store` - Bu öğreticide v2.1.3-preview kullanılır.
      * `Microsoft.Rest.ClientRuntime.Azure.Authentication` - Bu öğreticide v2.2.12 kullanılır.

        ![Nuget kaynağı ekleme](./media/data-lake-store-get-started-net-sdk/data-lake-store-install-nuget-package.png "Yeni bir Azure Data Lake hesabı oluşturma")
   4. Kapat hello **Nuget Paket Yöneticisi**.
6. Açık **Program.cs**hello var olan kodu silin ve deyimleri tooadd başvuruları toonamespaces aşağıdaki hello içerir.

        using System;
        using System.IO;
        using System.Security.Cryptography.X509Certificates; // Required only if you are using an Azure AD application created with certificates
        using System.Threading;

        using Microsoft.Azure.Management.DataLake.Store;
        using Microsoft.Azure.Management.DataLake.Store.Models;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;
        using Microsoft.Rest.Azure.Authentication;

7. Aşağıda gösterildiği gibi hello değişkenleri bildirin ve Data Lake Store adı ve zaten hello kaynak grubu adı için hello değerler sağlayın. Ayrıca, burada sağladığınız hello yerel yolu ve dosya adı hello bilgisayar üzerinde var olduğundan emin olun. Kod parçacığı hello ad alanı bildirimlerinden sonra aşağıdaki hello ekleyin.

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

Merhaba makale bölümlerini kalan hello nasıl toouse hello kimlik doğrulaması, karşıya dosya yükleme, vb. gibi kullanılabilir .NET yöntemleri tooperform işlemleri görebilirsiniz.

## <a name="authentication"></a>Kimlik Doğrulaması

### <a name="if-you-are-using-end-user-authentication-recommended-for-this-tutorial"></a>Son kullanıcı kimlik doğrulaması kullanıyorsanız (bu öğretici için önerilir)

Bu, uygulamanızın var olan bir Azure AD yerel uygulama tooauthenticate kullanın **etkileşimli olarak**, hangi anlamına gelir, gereken tooenter Azure kimlik bilgileriniz istenir.

Kullanım kolaylığı için aşağıdaki hello parçacığı istemci kimliği ve yeniden yönlendirme URI'si hiçbir Azure aboneliği ile çalışması için varsayılan değerleri kullanır. Bu öğreticide daha hızlı tamamlanmasına toohelp, bu yaklaşım kullanmanızı öneririz. Merhaba aşağıdaki parçacığında, Kiracı kimliğinizi hello değeri yalnızca belirtin. Verilen hello yönergeleri kullanarak alabilir [Active Directory Uygulama oluşturma](data-lake-store-end-user-authenticate-using-active-directory.md).

    // User login via interactive popup
    // Use hello client ID of an existing AAD Web application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());
    var tenant_id = "<AAD_tenant_id>"; // Replace this string with hello user's Azure Active Directory tenant ID
    var nativeClientApp_clientId = "1950a258-227b-4e31-a9cf-717495945fc2";
    var activeDirectoryClientSettings = ActiveDirectoryClientSettings.UsePromptOnly(nativeClientApp_clientId, new Uri("urn:ietf:wg:oauth:2.0:oob"));
    var creds = UserTokenProvider.LoginWithPromptAsync(tenant_id, activeDirectoryClientSettings).Result;

Yukarıdaki bu parçacığında hakkında şeyler tooknow birkaç:

* Hızlı Başlangıç Öğreticisi tamamlamanız toohelp, bu kod parçacığında kullanan bir Azure AD tüm Azure abonelikleri için varsayılan olarak kullanılabilir etki alanı ve istemci kimliği. Böylece **bu kod parçacığını uygulamanızda olduğu gibi kullanabilirsiniz**.
* Ancak, toouse kendi Azure AD etki alanı isterseniz ve uygulama istemci Kimliğini, Azure AD yerel uygulaması oluşturmanız gerekir ve ardından kullanımı hello Azure AD kimliği, istemci kimliği, Kiracı ve Merhaba uygulaması için yeniden yönlendirme URI'si oluşturuldu. Yönergeler için, bkz: [Data Lake Store ile son kullanıcı kimlik doğrulaması için Active Directory Uygulama oluşturma](data-lake-store-end-user-authenticate-using-active-directory.md).

### <a name="if-you-are-using-service-to-service-authentication-with-client-secret"></a>Gizli anahtar ile hizmetten hizmete kimlik doğrulaması kullanıyorsanız
Merhaba kod parçacığında kullanılan tooauthenticate uygulamanız olabilir **etkileşimsiz**, hello istemci gizli anahtarı kullanarak / anahtar için bir uygulama / hizmet sorumlusu. Bunu var olan Azure AD "Web App" uygulaması ile birlikte kullanın. Yönergeler için toocreate hello Azure AD uygulaması ve tooretrieve nasıl hello istemci Kimliğini ve istemci parolasını aşağıdaki, hello parçacığında gerekli nasıl görürüm [verilerle hizmeti için kimlik doğrulaması için Active Directory Uygulama oluşturma Lake deposu](data-lake-store-authenticate-using-active-directory.md).

    // Service principal / appplication authentication with client secret / key
    // Use hello client ID of an existing AAD "Web App" application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());

    var domain = "<AAD-directory-domain>";
    var webApp_clientId = "<AAD-application-clientid>";
    var clientSecret = "<AAD-application-client-secret>";
    var clientCredential = new ClientCredential(webApp_clientId, clientSecret);
    var creds = await ApplicationTokenProvider.LoginSilentAsync(domain, clientCredential);

### <a name="if-you-are-using-service-to-service-authentication-with-certificate"></a>Sertifika ile hizmetten hizmete kimlik doğrulaması kullanıyorsanız

Üçüncü, hello seçenek olarak kod parçacığında kullanılan tooauthenticate uygulamanız olabilir **etkileşimsiz**, bir Azure Active Directory uygulaması için hello sertifikayla / hizmet sorumlusu. Bunu var olan, [Sertifikalı Azure AD Uygulaması](../azure-resource-manager/resource-group-authenticate-service-principal.md) ile birlikte kullanın.

    // Service principal / application authentication with certificate
    // Use hello client ID and certificate of an existing AAD "Web App" application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());

    var domain = "<AAD-directory-domain>";
    var webApp_clientId = "<AAD-application-clientid>";
    var clientCert = <AAD-application-client-certificate>
    var clientAssertionCertificate = new ClientAssertionCertificate(webApp_clientId, clientCert);
    var creds = await ApplicationTokenProvider.LoginSilentWithCertificateAsync(domain, clientAssertionCertificate);

## <a name="create-client-objects"></a>İstemci nesneleri oluşturma
Merhaba aşağıdaki kod parçacığında hello Data Lake Store hesabı ve dosya sistemi kullanılan istemci nesneleri oluşturur tooissue toohello hizmet ister.

    // Create client objects and set hello subscription ID
    _adlsClient = new DataLakeStoreAccountManagementClient(creds) { SubscriptionId = _subId };
    _adlsFileSystemClient = new DataLakeStoreFileSystemManagementClient(creds);

## <a name="list-all-data-lake-store-accounts-within-a-subscription"></a>Bir abonelik içindeki tüm Data Lake Store hesaplarını listeleme
Merhaba aşağıdaki kod parçacığında belirli bir Azure aboneliği içindeki tüm Data Lake Store hesaplarını listeler.

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

## <a name="create-a-directory"></a>Dizin oluşturma
Aşağıdaki kod parçacığında gösterildiği hello bir `CreateDirectory` yöntemi toocreate bir dizin içinde bir Data Lake Store hesabı kullanabilirsiniz.

    // Create a directory
    public static async Task CreateDirectory(string path)
    {
        await _adlsFileSystemClient.FileSystem.MkdirsAsync(_adlsAccountName, path);
    }

## <a name="upload-a-file"></a>Dosyayı karşıya yükleme
Aşağıdaki kod parçacığında gösterildiği hello bir `UploadFile` tooupload kullanabileceğiniz yöntemi dosyaları tooa Data Lake Store hesabı.

    // Upload a file
    public static void UploadFile(string srcFilePath, string destFilePath, bool force = true)
    {
        _adlsFileSystemClient.FileSystem.UploadFile(_adlsAccountName, srcFilePath, destFilePath, overwrite:force);
    }

Merhaba SDK özyinelemeli karşıya yükleme ve indirme bir yerel dosya yolu ve bir Data Lake Store dosya yolu arasında destekler.    

## <a name="get-file-or-directory-info"></a>Dosya veya dizin bilgilerini alma
Aşağıdaki kod parçacığında gösterildiği hello bir `GetItemInfo` yöntemi Data Lake Store içinde bir dosya veya dizin kullanılabilir tooretrieve bilgilerini kullanabilirsiniz.

    // Get file or directory info
    public static async Task<FileStatusProperties> GetItemInfo(string path)
    {
        return await _adlsFileSystemClient.FileSystem.GetFileStatusAsync(_adlsAccountName, path).FileStatus;
    }

## <a name="list-file-or-directories"></a>Dosyayı veya dizinleri listeleme
Aşağıdaki kod parçacığında gösterildiği hello bir `ListItem` toolist hello dosya ve dizinleri bir Data Lake Store hesabında kullanabilirsiniz yöntemi.

    // List files and directories
    public static List<FileStatusProperties> ListItems(string directoryPath)
    {
        return _adlsFileSystemClient.FileSystem.ListFileStatus(_adlsAccountName, directoryPath).FileStatuses.FileStatus.ToList();
    }

## <a name="concatenate-files"></a>Dosyaları birleştirme
Aşağıdaki kod parçacığında gösterildiği hello bir `ConcatenateFiles` yöntemi tooconcatenate dosyalarını kullanın.

    // Concatenate files
    public static Task ConcatenateFiles(string[] srcFilePaths, string destFilePath)
    {
        await _adlsFileSystemClient.FileSystem.ConcatAsync(_adlsAccountName, destFilePath, srcFilePaths);
    }

## <a name="append-tooa-file"></a>Tooa dosya ekleme
Aşağıdaki kod parçacığında gösterildiği hello bir `AppendToFile` append bir Data Lake Store hesabında zaten depolanmış verileri tooa dosyası kullandığınız yöntemi.

    // Append toofile
    public static async Task AppendToFile(string path, string content)
    {
        using (var stream = new MemoryStream(Encoding.UTF8.GetBytes(content)))
        {
            await _adlsFileSystemClient.FileSystem.AppendAsync(_adlsAccountName, path, stream);
        }
    }

## <a name="download-a-file"></a>Dosya indirme
Aşağıdaki kod parçacığında gösterildiği hello bir `DownloadFile` yöntemi toodownload bir dosyadan bir Data Lake Store hesabı kullanın.

    // Download file
    public static void DownloadFile(string srcFilePath, string destFilePath)
    {
         _adlsFileSystemClient.FileSystem.DownloadFile(_adlsAccountName, srcFilePath, destFilePath);
    }

## <a name="next-steps"></a>Sonraki adımlar
* [Data Lake Store'da verilerin güvenliğini sağlama](data-lake-store-secure-data.md)
* [Azure Data Lake Analytics'i Data Lake Store ile kullanma](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Azure HDInsight'ı Data Lake Store ile kullanma](data-lake-store-hdinsight-hadoop-use-portal.md)
* [Data Lake Store .NET SDK Başvurusu](https://docs.microsoft.com/dotnet/api/?view=azuremgmtdatalakestore-2.1.0-preview&term=DataLake.Store)
* [Data Lake Store REST Başvurusu](https://msdn.microsoft.com/library/mt693424.aspx)
