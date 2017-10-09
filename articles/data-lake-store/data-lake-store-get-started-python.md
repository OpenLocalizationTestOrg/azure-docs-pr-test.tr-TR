---
title: "aaaUse hello Python SDK tooget Azure Data Lake Store ile çalışmaya | Microsoft Docs"
description: "Nasıl toouse Python SDK toowork Data Lake Store hesapları ve hello dosya sistemi öğrenin."
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 75f6de6f-6fd8-48f4-8707-cb27d22d27a6
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 7061fdf25ef607608bab618a20ddd3d6fc7af01d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-python"></a>Python’u kullanarak Azure Data Lake Store ile çalışmaya başlama

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

Nasıl toouse hello Python SDK'sı Azure ve Azure Data Lake Store tooperform temel işlemleri gibi klasör oluşturma için karşıya yükleme ve indirme veri dosyaları, vb. öğrenin. Data Lake hakkında daha fazla bilgi için bkz. [Azure Data Lake Store](data-lake-store-overview.md).

## <a name="prerequisites"></a>Ön koşullar

* **Python**. Python’u [buradan](https://www.python.org/downloads/) indirebilirsiniz. Bu makalede Python 3.5.2 kullanılmıştır.

* **Azure aboneliği**. Bkz. [Azure ücretsiz deneme sürümü edinme](https://azure.microsoft.com/pricing/free-trial/).

* **Azure Active Directory Uygulaması oluşturma**. Azure AD ile hello Azure AD uygulama tooauthenticate hello Data Lake Store uygulaması kullanın. Hangi Azure AD ile farklı yaklaşımlara tooauthenticate olan **son kullanıcı kimlik doğrulaması** veya **hizmeti için kimlik doğrulama**. Yönergeler ve hakkında daha fazla bilgi için tooauthenticate, bkz: [son kullanıcı kimlik doğrulaması](data-lake-store-end-user-authenticate-using-active-directory.md) veya [hizmeti için kimlik doğrulama](data-lake-store-authenticate-using-active-directory.md).

## <a name="install-hello-modules"></a>Merhaba modüllerini yükleyin

toowork Python kullanarak Data Lake Store ile tooinstall üç modülleri gerekir.

* Merhaba `azure-mgmt-resource` modülü. Bu, Active Directory gibi şeyler için Azure modüllerini içerir
* Merhaba `azure-mgmt-datalake-store` modülü. Bu hello Azure Data Lake Store hesabı yönetim işlemlerini içerir. Bu modül hakkında daha fazla bilgi için bkz. [Azure Data Lake Store Yönetimi modül başvurusu](http://azure-sdk-for-python.readthedocs.io/en/latest/sample_azure-mgmt-datalake-store.html).
* Merhaba `azure-datalake-store` modülü. Bu hello Azure Data Lake Store dosya sistemi işlemleri içerir. Bu modül hakkında daha fazla bilgi için bkz. [Azure Data Lake Store Dosya Sistemi modül başvurusu](http://azure-datalake-store.readthedocs.io/en/latest/).

Aşağıdaki komutları tooinstall hello modülleri hello kullanın.

```
pip install azure-mgmt-resource
pip install azure-mgmt-datalake-store
pip install azure-datalake-store
```

## <a name="create-a-new-python-application"></a>Yeni Python uygulaması oluşturma

1. Merhaba tercih ettiğiniz IDE Örneğin, yeni bir Python uygulaması oluşturma **mysample.py**.

2. Aşağıdaki satırları tooimport gerekli hello modülleri hello ekleme

    ```
    ## Use this only for Azure AD service-to-service authentication
    from azure.common.credentials import ServicePrincipalCredentials

    ## Use this only for Azure AD end-user authentication
    from azure.common.credentials import UserPassCredentials

    ## Use this only for Azure AD multi-factor authentication
    from msrestazure.azure_active_directory import AADTokenCredentials

    ## Required for Azure Data Lake Store account management
    from azure.mgmt.datalake.store import DataLakeStoreAccountManagementClient
    from azure.mgmt.datalake.store.models import DataLakeStoreAccount

    ## Required for Azure Data Lake Store filesystem management
    from azure.datalake.store import core, lib, multithread

    # Common Azure imports
    from azure.mgmt.resource.resources import ResourceManagementClient
    from azure.mgmt.resource.resources.models import ResourceGroup

    ## Use these as needed for your application
    import logging, getpass, pprint, uuid, time
    ```

3. Değişiklikleri toomysample.py kaydedin.

## <a name="authentication"></a>Kimlik Doğrulaması

Bu bölümde, biz hello farklı şekillerde tooauthenticate Azure AD ile ilgili konuşun. Başlangıç seçenekleri şunlardır:

* Son kullanıcı kimlik doğrulaması
* Hizmetten hizmete kimlik doğrulaması
* Multi-factor authentication

Bu kimlik doğrulama seçeneklerini hem hesap yönetimi hem de dosya sistemi yönetim modülleri için kullanmanız gerekir.

### <a name="end-user-authentication-for-account-management"></a>Hesap yönetimi için son kullanıcı kimlik doğrulaması

Bu tooauthenticate (oluşturma/silme Data Lake Store hesabı, vs.) hesap yönetimi işlemleri için Azure AD ile kullanın. Bir Azure AD kullanıcısının kullanıcı adını ve parolasını sağlamalısınız. Merhaba kullanıcının çok faktörlü kimlik doğrulaması için yapılandırılmamalıdır unutmayın.

    user = input('Enter hello user tooauthenticate with that has permission toosubscription: ')
    password = getpass.getpass()

    credentials = UserPassCredentials(user, password)

### <a name="end-user-authentication-for-filesystem-operations"></a>Dosya sistemi işlemleri için son kullanıcı kimlik doğrulaması

Dosya sistemi işlemleri (klasör, karşıya yükleme dosyasını oluşturun.) Azure AD ile bu tooauthenticate kullanın. Bunu mevcut bir Azure AD **yerel istemci** uygulaması ile kullanın. hello Azure AD kullanıcı kimlik bilgilerini sağlayın, çok faktörlü kimlik doğrulaması için yapılandırılmamalıdır.

    tenant_id = 'FILL-IN-HERE'
    client_id = 'FILL-IN-HERE'
    user = input('Enter hello user tooauthenticate with that has permission toosubscription: ')
    password = getpass.getpass()

    token = lib.auth(tenant_id, user, password, client_id)

### <a name="service-to-service-authentication-with-client-secret-for-account-management"></a>Hesap yönetimi için gizli anahtarla hizmetten hizmete kimlik doğrulaması

Bu tooauthenticate (oluşturma/silme Data Lake Store hesabı, vs.) hesap yönetimi işlemleri için Azure AD ile kullanın. Merhaba kod parçacığında kullanılan tooauthenticate uygulamanızı etkileşimsiz, hello gizli bir uygulama / hizmet sorumlusu için kullanılması olabilir. Bunu mevcut Azure AD "Web App" uygulaması ile birlikte kullanın.

    credentials = ServicePrincipalCredentials(client_id = 'FILL-IN-HERE', secret = 'FILL-IN-HERE', tenant = 'FILL-IN-HERE')

### <a name="service-to-service-authentication-with-client-secret-for-filesystem-operations"></a>Dosya sistemi işlemleri için gizli anahtarla hizmetten hizmete kimlik doğrulaması

Dosya sistemi işlemleri (klasör, karşıya yükleme dosyasını oluşturun.) Azure AD ile bu tooauthenticate kullanın. Merhaba kod parçacığında kullanılan tooauthenticate uygulamanızı etkileşimsiz, hello gizli bir uygulama / hizmet sorumlusu için kullanılması olabilir. Bunu mevcut Azure AD "Web App" uygulaması ile birlikte kullanın.

    token = lib.auth(tenant_id = 'FILL-IN-HERE', client_secret = 'FILL-IN-HERE', client_id = 'FILL-IN-HERE')

### <a name="multi-factor-authentication-for-account-management"></a>Hesap yönetimi için multi-factor authentication

Bu tooauthenticate (oluşturma/silme Data Lake Store hesabı, vs.) hesap yönetimi işlemleri için Azure AD ile kullanın. Merhaba aşağıdaki kod parçacığında olabilir çok faktörlü kimlik doğrulaması kullanarak uygulamanızı tooauthenticate kullanılır. Bunu mevcut Azure AD "Web App" uygulaması ile birlikte kullanın.

    authority_host_url = "https://login.microsoftonline.com"
    tenant = "FILL-IN-HERE"
    authority_url = authority_host_url + '/' + tenant
    client_id = 'FILL-IN-HERE'
    redirect = 'urn:ietf:wg:oauth:2.0:oob'
    RESOURCE = 'https://management.core.windows.net/'
    
    context = adal.AuthenticationContext(authority_url)
    code = context.acquire_user_code(RESOURCE, client_id)
    print(code['message'])
    mgmt_token = context.acquire_token_with_device_code(RESOURCE, code, client_id)
    credentials = AADTokenCredentials(mgmt_token, client_id)

### <a name="multi-factor-authentication-for-filesystem-management"></a>Dosya sistemi yönetimi için multi-factor authentication

Dosya sistemi işlemleri (klasör, karşıya yükleme dosyasını oluşturun.) Azure AD ile bu tooauthenticate kullanın. Merhaba aşağıdaki kod parçacığında olabilir çok faktörlü kimlik doğrulaması kullanarak uygulamanızı tooauthenticate kullanılır. Bunu mevcut Azure AD "Web App" uygulaması ile birlikte kullanın.

    token = lib.auth(tenant_id='FILL-IN-HERE')

## <a name="create-an-azure-resource-group"></a>Azure Kaynak Grubu oluşturma

Aşağıdaki kod parçacığını toocreate Azure kaynak grubu hello kullan:

    ## Declare variables
    subscriptionId= 'FILL-IN-HERE'
    resourceGroup = 'FILL-IN-HERE'
    location = 'eastus2'
    
    ## Create management client object
    resourceClient = ResourceManagementClient(
        credentials,
        subscriptionId
    )
    
    ## Create an Azure Resource Group
    resourceClient.resource_groups.create_or_update(
        resourceGroup,
        ResourceGroup(
            location=location
        )
    )

## <a name="create-clients-and-data-lake-store-account"></a>İstemciler ve Data Lake Store hesabı oluşturma

kod parçacığında önce aşağıdaki hello hello Data Lake Store hesabı istemci oluşturur. Merhaba istemci nesnesi toocreate Data Lake Store hesabını kullanır. Son olarak, hello kod parçacığında, bir dosya sistemi istemci nesnesi oluşturur.

    ## Declare variables
    subscriptionId = 'FILL-IN-HERE'
    adlsAccountName = 'FILL-IN-HERE'

    ## Create management client object
    adlsAcctClient = DataLakeStoreAccountManagementClient(credentials, subscriptionId)

    ## Create a Data Lake Store account
    adlsAcctResult = adlsAcctClient.account.create(
        resourceGroup,
        adlsAccountName,
        DataLakeStoreAccount(
            location=location
        )
    ).wait()

    ## Create a filesystem client object
    adlsFileSystemClient = core.AzureDLFileSystem(token, store_name=adlsAccountName)

## <a name="list-hello-data-lake-store-accounts"></a>Merhaba Data Lake Store hesapları listeleme

    ## List hello existing Data Lake Store accounts
    result_list_response = adlsAcctClient.account.list()
    result_list = list(result_list_response)
    for items in result_list:
        print(items)

## <a name="create-a-directory"></a>Dizin oluşturma

    ## Create a directory
    adlsFileSystemClient.mkdir('/mysampledirectory')

## <a name="upload-a-file"></a>Dosyayı karşıya yükleme


    ## Upload a file
    multithread.ADLUploader(adlsFileSystemClient, lpath='C:\\data\\mysamplefile.txt', rpath='/mysampledirectory/mysamplefile.txt', nthreads=64, overwrite=True, buffersize=4194304, blocksize=4194304)


## <a name="download-a-file"></a>Dosya indirme

    ## Download a file
    multithread.ADLDownloader(adlsFileSystemClient, lpath='C:\\data\\mysamplefile.txt.out', rpath='/mysampledirectory/mysamplefile.txt', nthreads=64, overwrite=True, buffersize=4194304, blocksize=4194304)

## <a name="delete-a-directory"></a>Bir dizini silme

    ## Delete a directory
    adlsFileSystemClient.rm('/mysampledirectory', recursive=True)

## <a name="see-also"></a>Ayrıca bkz.

- [Data Lake Store'da verilerin güvenliğini sağlama](data-lake-store-secure-data.md)
- [Azure Data Lake Analytics'i Data Lake Store ile kullanma](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
- [Azure HDInsight'ı Data Lake Store ile kullanma](data-lake-store-hdinsight-hadoop-use-portal.md)
- [Data Lake Store .NET SDK Başvurusu](https://msdn.microsoft.com/library/mt581387.aspx)
- [Data Lake Store REST Başvurusu](https://msdn.microsoft.com/library/mt693424.aspx)
