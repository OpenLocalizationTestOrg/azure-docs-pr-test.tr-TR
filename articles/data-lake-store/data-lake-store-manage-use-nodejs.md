---
title: "Node.js için Azure SDK kullanarak Azure Data Lake Store ile çalışmaya aaaGet | Microsoft Docs"
description: "Nasıl toouse Node.js toowork Data Lake Store hesapları ve hello dosya sistemi öğrenin."
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 2fee173c-69ae-4e1d-8773-48618cda9e16
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/06/2017
ms.author: nitinme
ms.openlocfilehash: ce36a2e0de4e091a4e85ed784a3381415ef6f9e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-azure-sdk-for-nodejs"></a><span data-ttu-id="a8889-103">Node.js için Azure SDK kullanarak Azure Data Lake Store ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="a8889-103">Get started with Azure Data Lake Store using Azure SDK for Node.js</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a8889-104">Portal</span><span class="sxs-lookup"><span data-stu-id="a8889-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="a8889-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a8889-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="a8889-106">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="a8889-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="a8889-107">Java SDK</span><span class="sxs-lookup"><span data-stu-id="a8889-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="a8889-108">REST API</span><span class="sxs-lookup"><span data-stu-id="a8889-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="a8889-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="a8889-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="a8889-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="a8889-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="a8889-111">Python</span><span class="sxs-lookup"><span data-stu-id="a8889-111">Python</span></span>](data-lake-store-get-started-python.md)
>
> 

> [!NOTE]
> <span data-ttu-id="a8889-112">Karşıya yükleme ve büyük miktarda veri (büyük dosyaları, çok sayıda dosya ya da her ikisi de) indirme için hello kullanmanızı öneririz [Python SDK](data-lake-store-get-started-python.md), hello [.NET SDK'sı](data-lake-store-get-started-net-sdk.md), [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md), veya [Azure PowerShell](data-lake-store-get-started-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="a8889-112">For uploading and downloading large amount of data (large files, a large number of files, or both), we recommend that you use hello [Python SDK](data-lake-store-get-started-python.md), hello [.NET SDK](data-lake-store-get-started-net-sdk.md), [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md), or [Azure PowerShell](data-lake-store-get-started-powershell.md).</span></span> <span data-ttu-id="a8889-113">Bu seçenekler, birden çok iş parçacığı tooparallelize hello veri taşıma kullandıkları daha iyi performans içerir.</span><span class="sxs-lookup"><span data-stu-id="a8889-113">These options have better performance as they use multiple threads tooparallelize hello data movement.</span></span>
> 
> 

<span data-ttu-id="a8889-114">Nasıl toouse hello Azure SDK'sı için Node.js toocreate bir Azure Data Lake Store hesabı öğrenin ve gibi klasör oluşturma karşıya yükleme ve veri dosyalarını indirme temel işlemleri gerçekleştirmek, vb., hesabınızı silme. Data Lake Store hakkında daha fazla bilgi için bkz. [Data Lake Store'a Genel Bakış](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a8889-114">Learn how toouse hello Azure SDK for Node.js toocreate an Azure Data Lake Store account and perform basic operations such as create folders, upload and download data files, delete your account, etc. For more information about Data Lake Store, see [Overview of Data Lake Store](data-lake-store-overview.md).</span></span> <span data-ttu-id="a8889-115">Şu anda hello SDK destekler</span><span class="sxs-lookup"><span data-stu-id="a8889-115">Currently, hello SDK supports</span></span>

* <span data-ttu-id="a8889-116">**Node.js sürümü: 0.10.0 veya üzeri**</span><span class="sxs-lookup"><span data-stu-id="a8889-116">**Node.js version: 0.10.0 or higher**</span></span>
* <span data-ttu-id="a8889-117">**Hesap için REST API sürümü: 2015-10-01-önizleme**</span><span class="sxs-lookup"><span data-stu-id="a8889-117">**REST API version for Account: 2015-10-01-preview**</span></span>
* <span data-ttu-id="a8889-118">**Dosya sistemi için REST API sürümü: 2015-10-01-Önizleme**</span><span class="sxs-lookup"><span data-stu-id="a8889-118">**REST API version for FileSystem: 2015-10-01-preview**</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a8889-119">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="a8889-119">Prerequisites</span></span>
<span data-ttu-id="a8889-120">Bu makaleye başlamadan önce hello şunlara sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="a8889-120">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="a8889-121">**Bir Azure aboneliği**.</span><span class="sxs-lookup"><span data-stu-id="a8889-121">**An Azure subscription**.</span></span> <span data-ttu-id="a8889-122">Bkz. [Azure ücretsiz deneme sürümü edinme](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a8889-122">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="a8889-123">**Azure Active Directory Uygulaması oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="a8889-123">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="a8889-124">Azure AD ile hello Azure AD uygulama tooauthenticate hello Data Lake Store uygulaması kullanın.</span><span class="sxs-lookup"><span data-stu-id="a8889-124">You use hello Azure AD application tooauthenticate hello Data Lake Store application with Azure AD.</span></span> <span data-ttu-id="a8889-125">Hangi Azure AD ile farklı yaklaşımlara tooauthenticate olan **son kullanıcı kimlik doğrulaması** veya **hizmeti için kimlik doğrulama**.</span><span class="sxs-lookup"><span data-stu-id="a8889-125">There are different approaches tooauthenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="a8889-126">Yönergeler ve hakkında daha fazla bilgi için tooauthenticate, bkz: [son kullanıcı kimlik doğrulaması](data-lake-store-end-user-authenticate-using-active-directory.md) veya [hizmeti için kimlik doğrulama](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="a8889-126">For instructions and more information on how tooauthenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="how-tooinstall"></a><span data-ttu-id="a8889-127">Nasıl tooInstall</span><span class="sxs-lookup"><span data-stu-id="a8889-127">How tooInstall</span></span>
```bash
npm install azure-arm-datalake-store
```

## <a name="authenticate-using-azure-active-directory"></a><span data-ttu-id="a8889-128">Azure Active Directory'yi kullanarak kimlik doğrulama</span><span class="sxs-lookup"><span data-stu-id="a8889-128">Authenticate using Azure Active Directory</span></span>
<span data-ttu-id="a8889-129">Aşağıdaki Hello kod parçacıkları, Azure AD kullanarak Data Lake Store ile kimlik doğrulaması iki ayrı yolu gösterir.</span><span class="sxs-lookup"><span data-stu-id="a8889-129">hello snippets below show two separate ways of authenticating with Data Lake Store using Azure AD.</span></span> <span data-ttu-id="a8889-130">Data Lake Store ile kimlik doğrulaması için çeşitli yöntemler toouse hakkında ayrıntılı bilgi için bkz: [Data Lake Store ile Azure Active Directory'yi kullanarak kimlik doğrulama](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="a8889-130">For a detailed discussion on various methods toouse for authentication with Data Lake Store, see [Authenticate with Data Lake Store using Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span></span>

<span data-ttu-id="a8889-131">Aşağıdaki Hello parçacığı ayrıca Azure AD etki alanı adı, bir Azure AD uygulaması, vb. için istemci kimliği gibi giriş gerektirir. Bu ayrıntılar hello ayrıntılarını da yukarıdaki bağlantıyı dahil edilen oluşturulan, gereken bir Azure AD uygulamasından alınabilir.</span><span class="sxs-lookup"><span data-stu-id="a8889-131">hello snippet below also requires inputs like Azure AD domain name, client ID for an Azure AD app, etc. All these details can be retrieved from an Azure AD application that you must created, hello details of which are also included in link above.</span></span>

 ```javascript
 var msrestAzure = require('ms-rest-azure');
 //user authentication
 var credentials = new msRestAzure.UserTokenCredentials('your-client-id', 'your-domain', 'your-username', 'your-password', 'your-redirect-uri');
 //service principal authentication
 var credentials = new msRestAzure.ApplicationTokenCredentials('your-client-id', 'your-domain', 'your-secret');
 ```

## <a name="create-hello-data-lake-store-clients"></a><span data-ttu-id="a8889-132">Merhaba Data Lake deposu istemcileri oluşturma</span><span class="sxs-lookup"><span data-stu-id="a8889-132">Create hello Data Lake Store Clients</span></span>
```javascript
var adlsManagement = require("azure-arm-datalake-store");
var acccountClient = new adlsManagement.DataLakeStoreAccountClient(credentials, "your-subscription-id");
var filesystemClient = new adlsManagement.DataLakeStoreFileSystemClient(credentials);
```

## <a name="create-a-data-lake-store-account"></a><span data-ttu-id="a8889-133">Bir Data Lake Store hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a8889-133">Create a Data Lake Store Account</span></span>
```javascript
var util = require('util');
var resourceGroupName = 'testrg';
var accountName = 'testadlsacct';
var location = 'eastus2';

// account object toocreate
var accountToCreate = {
  tags: {
    testtag1: 'testvalue1',
    testtag2: 'testvalue2'
  },
  name: accountName,
  location: location
};

client.account.create(resourceGroupName, accountName, accountToCreate, function (err, result, request, response) {
  if (err) {
    console.log(err);
    /*err has reference toohello actual request and response, so you can see what was sent and received on hello wire.
      hello structure of err looks like this:
      err: {
        code: 'Error Code',
        message: 'Error Message',
        body: 'hello response body if any',
        request: reference tooa stripped version of http request
        response: reference tooa stripped version of hello response
      }
    */
  } else {
    console.log('result is: ' + util.inspect(result, {depth: null}));
  }
});
```

## <a name="create-a-file-with-content"></a><span data-ttu-id="a8889-134">İçerik ile bir dosya oluşturun</span><span class="sxs-lookup"><span data-stu-id="a8889-134">Create a file with content</span></span>
```javascript
var util = require('util');
var accountName = 'testadlsacct';
var fileToCreate = '/myfolder/myfile.txt';
var options = {
  streamContents: new Buffer('some string content')
}

filesystemClient.fileSystem.listFileStatus(accountName, fileToCreate, options, function (err, result, request, response) {
  if (err) {
    console.log(err);
  } else {
    // no result is returned, only a 201 response for success.
    console.log('response is: ' + util.inspect(response, {depth: null}));
  }
});
```

## <a name="get-a-list-of-files-and-folders"></a><span data-ttu-id="a8889-135">Dosya ve klasörlerin listesini al</span><span class="sxs-lookup"><span data-stu-id="a8889-135">Get a list of files and folders</span></span>
```javascript
var util = require('util');
var accountName = 'testadlsacct';
var pathToEnumerate = '/myfolder';
filesystemClient.fileSystem.listFileStatus(accountName, pathToEnumerate, function (err, result, request, response) {
  if (err) {
    console.log(err);
  } else {
    console.log('result is: ' + util.inspect(result, {depth: null}));
  }
});
```

## <a name="see-also"></a><span data-ttu-id="a8889-136">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="a8889-136">See also</span></span>
* [<span data-ttu-id="a8889-137">Node.js için Microsoft Azure SDK</span><span class="sxs-lookup"><span data-stu-id="a8889-137">Microsoft Azure SDK for Node.js</span></span>](https://github.com/azure/azure-sdk-for-node)
* [<span data-ttu-id="a8889-138">Node.js - Data Lake Analytics yönetimi için Microsoft Azure SDK'sı</span><span class="sxs-lookup"><span data-stu-id="a8889-138">Microsoft Azure SDK for Node.js - Data Lake Analytics Management</span></span>](https://www.npmjs.com/package/azure-arm-datalake-analytics)

