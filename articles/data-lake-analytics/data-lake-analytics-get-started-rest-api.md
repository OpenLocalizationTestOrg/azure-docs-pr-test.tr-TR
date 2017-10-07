---
title: "aaaGet REST API'sini kullanarak Data Lake Analytics ile çalışmaya | Microsoft Docs"
description: "Data Lake Analytics WebHDFS REST API'lerini tooperform işlemleri kullanın"
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 5e133d92-baaa-44c9-890c-ab2d85c91122
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 02/03/2017
ms.author: jgao
ms.openlocfilehash: a0b13d521821fd2d74716cc52485585feb7c51b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-rest-apis"></a>REST API’lerini kullanarak Azure Data Lake Analytics ile çalışmaya başlama | Azure
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

Nasıl toouse WebHDFS REST API'lerini ve Data Lake Analytics REST API'leri toomanage Data Lake Analytics hesaplarını, işlerini ve Katalog öğrenin. 

## <a name="prerequisites"></a>Ön koşullar
* **Bir Azure aboneliği**. Bkz. [Azure ücretsiz deneme sürümü edinme](https://azure.microsoft.com/pricing/free-trial/).
* **Azure Active Directory Uygulaması oluşturma**. Azure AD ile hello Azure AD uygulama tooauthenticate hello Data Lake Analytics uygulaması kullanın. Hangi Azure AD ile farklı yaklaşımlara tooauthenticate olan **son kullanıcı kimlik doğrulaması** veya **hizmeti için kimlik doğrulama**. Yönergeler ve hakkında daha fazla bilgi için tooauthenticate, bkz: [Azure Active Directory kullanarak Data Lake Analytics ile kimlik doğrulama](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).
* [cURL](http://curl.haxx.se/). Bu makalede, nasıl bir Data Lake Analytics hesabı karşı toomake REST API çağrıları cURL toodemonstrate kullanır.

## <a name="authenticate-with-azure-active-directory"></a>Azure Active Directory ile kimlik doğrulama
Azure Active Directory ile kimlik doğrulama gerçekleştirmek için kullanılabilecek iki yöntem vardır.

### <a name="end-user-authentication-interactive"></a>Son kullanıcı kimlik doğrulaması (etkileşimli)
Bu yöntemi kullanarak, uygulama hello kullanıcı toolog ister ve tüm hello işlemler hello hello kullanıcı bağlamında gerçekleştirilir. 

Etkileşimli kimlik doğrulaması için aşağıdaki adımları izleyin:

1. Uygulamanızı kullanarak URL aşağıdaki hello kullanıcı toohello yönlendir:
   
        https://login.microsoftonline.com/<TENANT-ID>/oauth2/authorize?client_id=<CLIENT-ID>&response_type=code&redirect_uri=<REDIRECT-URI>
   
   > [!NOTE]
   > \<Yeniden yönlendirme URI'si > kullanılmak üzere bir URL kodlanmış toobe gerekiyor. Bu nedenle, https://localhost için `https%3A%2F%2Flocalhost` kullanılır)
   > 
   > 
   
    Bu öğretici Hello amaçla hello URL'de hello yer tutucu değerlerini değiştirin ve bir web tarayıcısının Adres çubuğuna yapıştırın. Azure oturum açma bilgilerinizi kullanarak yeniden yönlendirilen tooauthenticate olacaktır. Başarıyla oturum açmanızın sonra hello yanıt hello tarayıcının adres çubuğunda görüntülenir. Merhaba yanıt biçimi aşağıdaki hello olacaktır:
   
        http://localhost/?code=<AUTHORIZATION-CODE>&session_state=<GUID>
2. Merhaba yanıt Hello yetkilendirme kodundan yakalayın. Bu öğretici için hello web tarayıcınızın adres çubuğunda hello hello yetkilendirme kodu kopyalayın ve aşağıda gösterildiği gibi hello POST isteği toohello belirteç uç noktasında geçirin:
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token \
        -F redirect_uri=<REDIRECT-URI> \
        -F grant_type=authorization_code \
        -F resource=https://management.core.windows.net/ \
        -F client_id=<CLIENT-ID> \
        -F code=<AUTHORIZATION-CODE>
   
   > [!NOTE]
   > Bu durumda, hello \<REDIRECT-URI > öğesinin kodlanması gerekmez.
   > 
   > 
3. Merhaba yanıt olan bir erişim belirteci içeren bir JSON nesnesi (örn., `"access_token": "<ACCESS_TOKEN>"`) ve bir yenileme belirteci (örn., `"refresh_token": "<REFRESH_TOKEN>"`). Bir erişim belirtecinin süresi dolduğunda, uygulamanızın hello erişim belirteci Azure Data Lake Store ve hello yenileme belirteci tooget erişirken başka bir erişim belirteci kullanır.
   
        {"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","expires_on":"1461865782","not_before":    "1461861882","resource":"https://management.core.windows.net/","access_token":"<REDACTED>","refresh_token":"<REDACTED>","id_token":"<REDACTED>"}
4. Merhaba erişim belirtecinin süresi dolduğunda, aşağıda gösterildiği gibi hello yenileme belirtecini kullanarak yeni bir erişim belirteci isteyebilirsiniz:
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
             -F grant_type=refresh_token \
             -F resource=https://management.core.windows.net/ \
             -F client_id=<CLIENT-ID> \
             -F refresh_token=<REFRESH-TOKEN>

Etkileşimli kullanıcı kimlik doğrulaması hakkında daha fazla bilgi için bkz. [Yetki kodu izin akışı](https://msdn.microsoft.com/library/azure/dn645542.aspx).

### <a name="service-to-service-authentication-non-interactive"></a>Hizmetten hizmete kimlik doğrulaması (etkileşimli olmayan)
Bu yöntemi kullanarak, uygulama kendi kimlik bilgilerini tooperform hello işlemler sağlar. Bunun için aşağıda gösterilene hello gibi bir POST isteği yayımlamanız gerekir: 

    curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
      -F grant_type=client_credentials \
      -F resource=https://management.core.windows.net/ \
      -F client_id=<CLIENT-ID> \
      -F client_secret=<AUTH-KEY>

Merhaba bu isteğin çıktısı, bir yetki belirteci içerir (belirtilmiştir `access-token` hello çıkışı aşağıdaki), REST API çağrıları ile sonradan geçecek. Bu kimlik doğrulama belirtecini bir metin dosyasına kaydedin; belirteç, bu makalenin ilerleyen bölümlerinde gerekli olacaktır.

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1458245447","not_before":"1458241547","resource":"https://management.core.windows.net/","access_token":"<REDACTED>"}

Bu makalede hello kullanan **etkileşimli olmayan** yaklaşım. Etkileşimli olmayan (hizmet-hizmet çağrıları) hakkında daha fazla bilgi için bkz: [hizmet kimlik bilgilerini kullanarak tooservice çağrıları](https://msdn.microsoft.com/library/azure/dn645543.aspx).

## <a name="create-a-data-lake-analytics-account"></a>Data Lake Analytics hesabı oluşturma
Data Lake Analytics hesabı oluşturabilmek için Azure kaynak grubu ve Data Lake Store hesabı oluşturmanız gerekir.  Bkz. [Data Lake Store hesabı oluşturma](../data-lake-store/data-lake-store-get-started-rest-api.md#create-a-data-lake-store-account).

Curl komutunu gösterir nasıl aşağıdaki hello toocreate bir hesap:

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -H "Content-Type: application/json" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<NewAzureDataLakeAnalyticsAccountName>?api-version=2016-11-01 -d@"C:\tutorials\adla\CreateDataLakeAnalyticsAccountRequest.json"

Değiştir \< `REDACTED` \> hello yetkilendirme belirteci ile \< `AzureSubscriptionID` \> değerini abonelik kimliğinizle \< `AzureResourceGroupName` \> mevcut bir Azure kaynağı ile Grup adı ve \< `NewAzureDataLakeAnalyticsAccountName` \> ile yeni bir Data Lake Analytics hesap adı. Bu komut için başlangıç istek yükü hello bulunan **CreateDatalakeAnalyticsAccountRequest.json** hello için sağlanan dosya `-d` yukarıdaki parametresini. hello input.json dosyasının Merhaba içeriğine hello aşağıdakine benzer:

    {  
        "location": "East US 2",  
        "name": "myadla1004",  
        "tags": {},  
        "properties": {  
            "defaultDataLakeStoreAccount": "my1004store",  
            "dataLakeStoreAccounts": [  
                {  
                    "name": "my1004store"  
                }     
            ]
        }  
    }  


## <a name="list-data-lake-analytics-accounts-in-a-subscription"></a>Bir abonelikteki Data Lake Analytics hesaplarını listeleme
Aşağıdaki Curl komutunu hello nasıl toolist bir abonelikte hesapları gösterir:

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/providers/Microsoft.DataLakeAnalytics/Accounts?api-version=2016-11-01

Değiştir \< `REDACTED` \> hello yetkilendirme belirteci ile \< `AzureSubscriptionID` \> abonelik kimliğinizi içeren Merhaba çıkış benzer:

    {
        "value": [
            {
            "properties": {
                "provisioningState": "Succeeded",
                "state": "Active",
                "endpoint": "myadla0831.azuredatalakeanalytics.net",
                "accountId": "21e74660-0941-4880-ae72-b143c2615ea9",
                "creationTime": "2016-09-01T12:49:12.7451428Z",
                "lastModifiedTime": "2016-09-01T12:49:12.7451428Z"
            },
            "location": "East US 2",
            "tags": {},
            "id": "/subscriptions/65a1016d-0f67-45d2-b838-b8f373d6d52e/resourceGroups/myadla0831rg/providers/Microsoft.DataLakeAnalytics/accounts/myadla0831",
            "name": "myadla0831",
            "type": "Microsoft.DataLakeAnalytics/accounts"
            },
            {
            "properties": {
                "provisioningState": "Succeeded",
                "state": "Active",
                "endpoint": "myadla1004.azuredatalakeanalytics.net",
                "accountId": "3ff9b93b-11c4-43c6-83cc-276292eeb350",
                "creationTime": "2016-10-04T20:46:42.287147Z",
                "lastModifiedTime": "2016-10-04T20:46:42.287147Z"
            },
            "location": "East US 2",
            "tags": {},
            "id": "/subscriptions/65a1016d-0f67-45d2-b838-b8f373d6d52e/resourceGroups/myadla1004rg/providers/Microsoft.DataLakeAnalytics/accounts/myadla1004",
            "name": "myadla1004",
            "type": "Microsoft.DataLakeAnalytics/accounts"
            }
        ]
    }

## <a name="get-information-about-a-data-lake-analytics-account"></a>Bir Data Lake Analytics hesabı hakkında bilgi edinme
Curl komutunu gösterir nasıl aşağıdaki hello tooget bir hesap bilgileri:

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<DataLakeAnalyticsAccountName>?api-version=2015-11-01

Değiştir \< `REDACTED` \> hello yetkilendirme belirteci ile \< `AzureSubscriptionID` \> değerini abonelik kimliğinizle \< `AzureResourceGroupName` \> mevcut bir Azure kaynağı ile Grup adı ve \< `DataLakeAnalyticsAccountName` \> varolan bir Data Lake Analytics hesabı hello adı. Merhaba çıkış benzer:

    {
        "properties": {
            "defaultDataLakeStoreAccount": "my1004store",
            "dataLakeStoreAccounts": [
            {
                "properties": {
                "suffix": "azuredatalakestore.net"
                },
                "name": "my1004store"
            }
            ],
            "provisioningState": "Creating",
            "state": null,
            "endpoint": null,
            "accountId": "3ff9b93b-11c4-43c6-83cc-276292eeb350",
            "creationTime": null,
            "lastModifiedTime": null
        },
        "location": "East US 2",
        "tags": {},
        "id": "/subscriptions/65a1016d-0f67-45d2-b838-b8f373d6d52e/resourceGroups/myadla1004rg/providers/Microsoft.DataLakeAnalytics/accounts/myadla1004",
        "name": "myadla1004",
        "type": "Microsoft.DataLakeAnalytics/accounts"
    }

## <a name="list-data-lake-stores-of-a-data-lake-analytics-account"></a>Bir Data Lake Analytics hesabının Data Lake Store bilgilerini listeleme
Aşağıdaki Curl komutunu hello nasıl toolist Data Lake bir hesabı depoladığını gösterir:

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<DataLakeAnalyticsAccountName>/DataLakeStoreAccounts/?api-version=2016-11-01

Değiştir \< `REDACTED` \> hello yetkilendirme belirteci ile \< `AzureSubscriptionID` \> değerini abonelik kimliğinizle \< `AzureResourceGroupName` \> mevcut bir Azure kaynağı ile Grup adı ve \< `DataLakeAnalyticsAccountName` \> varolan bir Data Lake Analytics hesabı hello adı. Merhaba çıkış benzer:

    {
        "value": [
            {
            "properties": {
                "suffix": "azuredatalakestore.net"
            },
            "id": "/subscriptions/65a1016d-0f67-45d2-b838-b8f373d6d52e/resourceGroups/myadla1004rg/providers/Microsoft.DataLakeAnalytics/accounts/myadla1004/dataLakeStoreAccounts/my1004store",
            "name": "my1004store",
            "type": "Microsoft.DataLakeAnalytics/accounts/dataLakeStoreAccounts"
            }
        ]
    }

## <a name="submit-u-sql-jobs"></a>U-SQL işlerini gönderme
Curl komutunu gösterir nasıl aşağıdaki hello toosubmit U-SQL işi:

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/Jobs/<NewGUID>?api-version=2016-03-20-preview -d@"C:\tutorials\adla\SubmitADLAJob.json"

Değiştir \< `REDACTED` \> hello yetkilendirme belirteci ile \< `DataLakeAnalyticsAccountName` \> varolan bir Data Lake Analytics hesabı hello adı. Bu komut için başlangıç istek yükü hello bulunan **SubmitADLAJob.json** hello için sağlanan dosya `-d` yukarıdaki parametresini. hello input.json dosyasının Merhaba içeriğine hello aşağıdakine benzer:

    {
        "jobId": "8f8ebf8c-4b63-428a-ab46-a03d2cc5b65a",
        "name": "convertTSVtoCSV",
        "type": "USql",
        "degreeOfParallelism": 1,
        "priority": 1000,
        "properties": {
            "type": "USql",
            "script": "@searchlog =\n    EXTRACT UserId          int,\n            Start           DateTime,\n            Region          string,\n            Query          
        string,\n            Duration        int?,\n            Urls            string,\n            ClickedUrls     string\n    FROM \"/Samples/Data/SearchLog.tsv\"\n    US
        ING Extractors.Tsv();\n\nOUTPUT @searchlog   \n    too\"/Output/SearchLog-from-Data-Lake.csv\"\nUSING Outputters.Csv();"
        }
    }

Merhaba çıkış benzer:

    {
        "jobId": "8f8ebf8c-4b63-428a-ab46-a03d2cc5b65a",
        "name": "convertTSVtoCSV",
        "type": "USql",
        "submitter": "myadl@SPI",
        "degreeOfParallelism": 1,
        "priority": 1000,
        "submitTime": "2016-10-05T13:54:59.9871859+00:00",
        "state": "Compiling",
        "result": "Succeeded",
        "stateAuditRecords": [
            {
            "newState": "New",
            "timeStamp": "2016-10-05T13:54:59.9871859+00:00",
            "details": "userName:myadl@SPI;submitMachine:N/A"
            }
        ],
        "properties": {
            "owner": "myadl@SPI",
            "resources": [],
            "runtimeVersion": "default",
            "rootProcessNodeId": "00000000-0000-0000-0000-000000000000",
            "algebraFilePath": "adl://myadls0831.azuredatalakestore.net/system/jobservice/jobs/Usql/2016/10/05/13/54/8f8ebf8c-4b63-428a-ab46-a03d2cc5b65a/algebra.xml",
            "compileMode": "Semantic",
            "errorSource": "Unknown",
            "totalCompilationTime": "PT0S",
            "totalPausedTime": "PT0S",
            "totalQueuedTime": "PT0S",
            "totalRunningTime": "PT0S",
            "type": "USql"
        }
    }


## <a name="list-u-sql-jobs"></a>U-SQL işlerini listeleme
Curl komutunu gösterir nasıl aşağıdaki hello toolist U-SQL işleri:

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/Jobs?api-version=2016-11-01 

Değiştir \< `REDACTED` \> hello yetkilendirme belirteci ile ve \< `DataLakeAnalyticsAccountName` \> varolan bir Data Lake Analytics hesabı hello adı. 

Merhaba çıkış benzer:

    {
    "value": [
        {
        "jobId": "65cf1691-9dbe-43cd-90ed-1cafbfb406fb",
        "name": "convertTSVtoCSV",
        "type": "USql",
        "submitter": "someone@microsoft.com",
        "account": null,
        "degreeOfParallelism": 1,
        "priority": 1000,
        "submitTime": "Wed, 05 Oct 2016 13:46:53 GMT",
        "startTime": "Wed, 05 Oct 2016 13:47:33 GMT",
        "endTime": "Wed, 05 Oct 2016 13:48:07 GMT",
        "state": "Ended",
        "result": "Succeeded",
        "errorMessage": null,
        "storageAccounts": null,
        "stateAuditRecords": null,
        "logFilePatterns": null,
        "properties": null
        },
        {
        "jobId": "8f8ebf8c-4b63-428a-ab46-a03d2cc5b65a",
        "name": "convertTSVtoCSV",
        "type": "USql",
        "submitter": "someoneadl@SPI",
        "account": null,
        "degreeOfParallelism": 1,
        "priority": 1000,
        "submitTime": "Wed, 05 Oct 2016 13:54:59 GMT",
        "startTime": "Wed, 05 Oct 2016 13:55:43 GMT",
        "endTime": "Wed, 05 Oct 2016 13:56:11 GMT",
        "state": "Ended",
        "result": "Succeeded",
        "errorMessage": null,
        "storageAccounts": null,
        "stateAuditRecords": null,
        "logFilePatterns": null,
        "properties": null
        }
    ],
    "nextLink": null,
    "count": null
    }


## <a name="get-catalog-items"></a>Katalog öğelerini alma
Aşağıdaki Curl komutunu hello nasıl tooget hello veritabanlarından katalog hello gösterir:

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/catalog/usql/databases?api-version=2016-11-01

Merhaba çıkış benzer:

    {
    "@odata.context":"https://myadla0831.azuredatalakeanalytics.net/sqlip/$metadata#databases","value":[
        {
        "computeAccountName":"myadla0831","databaseName":"mytest","version":"f6956327-90b8-4648-ad8b-de3ff09274ea"
        },{
        "computeAccountName":"myadla0831","databaseName":"master","version":"e8bca908-cc73-41a3-9564-e9bcfaa21f4e"
        }
    ]
    }

## <a name="see-also"></a>Ayrıca bkz.
* toosee daha karmaşık bir sorgu görmek [Web sitesi günlüklerini çözümleme Azure Data Lake Analytics'i kullanarak](data-lake-analytics-analyze-weblogs.md).
* U-SQL uygulamalarını geliştirmeye başlatılan tooget bkz [Visual Studio için Data Lake Araçları'nı kullanarak geliştirme U-SQL betikleri](data-lake-analytics-data-lake-tools-get-started.md).
* U-SQL, toolearn bkz [Azure Data Lake Analytics U-SQL dili ile çalışmaya başlama](data-lake-analytics-u-sql-get-started.md).
* Yönetim görevleri için bkz. [Azure portalı kullanarak Azure Data Lake Analytics'i yönetme](data-lake-analytics-manage-use-portal.md).
* bir Data Lake Analytics özetini tooget bkz [Azure Data Lake Analytics'e genel bakış](data-lake-analytics-overview.md).
* toosee hello aynı öğreticiyi diğer araçları kullanarak, hello sekmesini seçiciler hello sayfasının hello üstte'ı tıklatın.

