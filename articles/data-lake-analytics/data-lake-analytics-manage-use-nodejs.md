---
title: "Node.js için Azure SDK kullanarak Azure Data Lake Analytics aaaManage | Microsoft Docs"
description: "Toomanage Data Lake Analytics hesaplarını, veri kaynakları, işlerin nasıl ve Node.js için Azure SDK'sını kullanarak kullanıcıların bilgi edinin"
services: data-lake-analytics
documentationcenter: 
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: 9de1bcf4-b15b-4d0b-9284-8889ecf0c438
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: 07acd058bf252af2fc98c4cfe87a135e0b79900f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-using-azure-sdk-for-nodejs"></a>Azure Data Lake Analytics'i Node.js için Azure SDK'yı kullanarak yönetme
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

Merhaba Node.js için Azure SDK, Azure Data Lake Analytics hesaplarını, işlerini ve kataloglarını yönetmek için kullanılabilir. toosee yönetim konu diğer araçları kullanarak yukarıdaki hello sekme seçimine tıklayın.

Şu anda aşağıdakiler desteklenmektedir:

* **Node.js sürümü: 0.10.0 veya üzeri**
* **Hesap için REST API sürümü: 2015-10-01-önizleme**
* **Katalog için REST API sürümü: 2015-10-01-önizleme**
* **İş için REST API sürümü: 2016-03-20-önizleme**

## <a name="features"></a>Özellikler
* Hesap yönetimi: oluşturma, alma, listeleme, güncelleştirme ve silme.
* İş yönetimi: gönderme, alma, listeleme ve iptal etme.
* Katalog yönetimi: alma ve listeleme.

## <a name="how-tooinstall"></a>Nasıl tooInstall
```bash
npm install azure-arm-datalake-analytics
```

## <a name="authenticate-using-azure-active-directory"></a>Azure Active Directory'yi kullanarak kimlik doğrulama
 ```javascript
 var msrestAzure = require('ms-rest-azure');
 //user authentication
 var credentials = new msRestAzure.UserTokenCredentials('your-client-id', 'your-domain', 'your-username', 'your-password', 'your-redirect-uri');
 //service principal authentication
 var credentials = new msRestAzure.ApplicationTokenCredentials('your-client-id', 'your-domain', 'your-secret');
 ```

## <a name="create-hello-data-lake-analytics-client"></a>Merhaba Data Lake Analytics istemcisi oluşturma
```javascript
var adlaManagement = require("azure-arm-datalake-analytics");
var acccountClient = new adlaManagement.DataLakeAnalyticsAccountClient(credentials, 'your-subscription-id');
var jobClient = new adlaManagement.DataLakeAnalyticsJobClient(credentials, 'azuredatalakeanalytics.net');
var catalogClient = new adlaManagement.DataLakeAnalyticsCatalogClient(credentials, 'azuredatalakeanalytics.net');
```

## <a name="create-a-data-lake-analytics-account"></a>Data Lake Analytics hesabı oluşturma
```javascript
var util = require('util');
var resourceGroupName = 'testrg';
var accountName = 'testadlaacct';
var location = 'eastus2';

// A Data Lake Store account must already have been created toocreate
// a Data Lake Analytics account. See hello Data Lake Store readme for
// information on doing so. For now, we assume one exists already.
var datalakeStoreAccountName = 'existingadlsaccount';

// account object toocreate
var accountToCreate = {
  tags: {
    testtag1: 'testvalue1',
    testtag2: 'testvalue2'
  },
  name: accountName,
  location: location,
  properties: {
    defaultDataLakeStoreAccount: datalakeStoreAccountName,
    dataLakeStoreAccounts: [
      {
        name: datalakeStoreAccountName
      }
    ]
  }
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

## <a name="get-a-list-of-jobs"></a>İşlerin listesini alma
```javascript
var util = require('util');
var accountName = 'testadlaacct';
jobClient.job.list(accountName, function (err, result, request, response) {
  if (err) {
    console.log(err);
  } else {
    console.log('result is: ' + util.inspect(result, {depth: null}));
  }
});
```

## <a name="get-a-list-of-databases-in-hello-data-lake-analytics-catalog"></a>Merhaba Data Lake Analytics Kataloğu veritabanlarının listesini alma
```javascript
var util = require('util');
var accountName = 'testadlaacct';
catalogClient.catalog.listDatabases(accountName, function (err, result, request, response) {
  if (err) {
    console.log(err);
  } else {
    console.log('result is: ' + util.inspect(result, {depth: null}));
  }
});
```

## <a name="see-also"></a>Ayrıca bkz.
* [Node.js için Microsoft Azure SDK](https://github.com/azure/azure-sdk-for-node)
* [Node.js için Microsoft Azure SDK - Data Lake Store Yönetimi](https://github.com/Azure/azure-sdk-for-node/tree/autorest/lib/services/dataLake.Store)

