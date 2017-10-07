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
# <a name="get-started-with-azure-data-lake-store-using-azure-sdk-for-nodejs"></a>Node.js için Azure SDK kullanarak Azure Data Lake Store ile çalışmaya başlama
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

> [!NOTE]
> Karşıya yükleme ve büyük miktarda veri (büyük dosyaları, çok sayıda dosya ya da her ikisi de) indirme için hello kullanmanızı öneririz [Python SDK](data-lake-store-get-started-python.md), hello [.NET SDK'sı](data-lake-store-get-started-net-sdk.md), [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md), veya [Azure PowerShell](data-lake-store-get-started-powershell.md). Bu seçenekler, birden çok iş parçacığı tooparallelize hello veri taşıma kullandıkları daha iyi performans içerir.
> 
> 

Nasıl toouse hello Azure SDK'sı için Node.js toocreate bir Azure Data Lake Store hesabı öğrenin ve gibi klasör oluşturma karşıya yükleme ve veri dosyalarını indirme temel işlemleri gerçekleştirmek, vb., hesabınızı silme. Data Lake Store hakkında daha fazla bilgi için bkz. [Data Lake Store'a Genel Bakış](data-lake-store-overview.md). Şu anda hello SDK destekler

* **Node.js sürümü: 0.10.0 veya üzeri**
* **Hesap için REST API sürümü: 2015-10-01-önizleme**
* **Dosya sistemi için REST API sürümü: 2015-10-01-Önizleme**

## <a name="prerequisites"></a>Ön koşullar
Bu makaleye başlamadan önce hello şunlara sahip olmanız gerekir:

* **Bir Azure aboneliği**. Bkz. [Azure ücretsiz deneme sürümü edinme](https://azure.microsoft.com/pricing/free-trial/).
* **Azure Active Directory Uygulaması oluşturma**. Azure AD ile hello Azure AD uygulama tooauthenticate hello Data Lake Store uygulaması kullanın. Hangi Azure AD ile farklı yaklaşımlara tooauthenticate olan **son kullanıcı kimlik doğrulaması** veya **hizmeti için kimlik doğrulama**. Yönergeler ve hakkında daha fazla bilgi için tooauthenticate, bkz: [son kullanıcı kimlik doğrulaması](data-lake-store-end-user-authenticate-using-active-directory.md) veya [hizmeti için kimlik doğrulama](data-lake-store-authenticate-using-active-directory.md).

## <a name="how-tooinstall"></a>Nasıl tooInstall
```bash
npm install azure-arm-datalake-store
```

## <a name="authenticate-using-azure-active-directory"></a>Azure Active Directory'yi kullanarak kimlik doğrulama
Aşağıdaki Hello kod parçacıkları, Azure AD kullanarak Data Lake Store ile kimlik doğrulaması iki ayrı yolu gösterir. Data Lake Store ile kimlik doğrulaması için çeşitli yöntemler toouse hakkında ayrıntılı bilgi için bkz: [Data Lake Store ile Azure Active Directory'yi kullanarak kimlik doğrulama](data-lake-store-authenticate-using-active-directory.md).

Aşağıdaki Hello parçacığı ayrıca Azure AD etki alanı adı, bir Azure AD uygulaması, vb. için istemci kimliği gibi giriş gerektirir. Bu ayrıntılar hello ayrıntılarını da yukarıdaki bağlantıyı dahil edilen oluşturulan, gereken bir Azure AD uygulamasından alınabilir.

 ```javascript
 var msrestAzure = require('ms-rest-azure');
 //user authentication
 var credentials = new msRestAzure.UserTokenCredentials('your-client-id', 'your-domain', 'your-username', 'your-password', 'your-redirect-uri');
 //service principal authentication
 var credentials = new msRestAzure.ApplicationTokenCredentials('your-client-id', 'your-domain', 'your-secret');
 ```

## <a name="create-hello-data-lake-store-clients"></a>Merhaba Data Lake deposu istemcileri oluşturma
```javascript
var adlsManagement = require("azure-arm-datalake-store");
var acccountClient = new adlsManagement.DataLakeStoreAccountClient(credentials, "your-subscription-id");
var filesystemClient = new adlsManagement.DataLakeStoreFileSystemClient(credentials);
```

## <a name="create-a-data-lake-store-account"></a>Bir Data Lake Store hesabı oluşturma
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

## <a name="create-a-file-with-content"></a>İçerik ile bir dosya oluşturun
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

## <a name="get-a-list-of-files-and-folders"></a>Dosya ve klasörlerin listesini al
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

## <a name="see-also"></a>Ayrıca bkz.
* [Node.js için Microsoft Azure SDK](https://github.com/azure/azure-sdk-for-node)
* [Node.js - Data Lake Analytics yönetimi için Microsoft Azure SDK'sı](https://www.npmjs.com/package/azure-arm-datalake-analytics)

