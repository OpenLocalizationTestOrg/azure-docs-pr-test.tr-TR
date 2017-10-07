---
title: "aaaScheduler giden bağlantı kimlik doğrulaması"
description: "Scheduler giden bağlantı kimlik doğrulaması"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 6707f82b-7e32-401b-a960-02aae7bb59cc
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/15/2016
ms.author: deli
ms.openlocfilehash: ef713f4770b48d0a9176415e87c1042a823582e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="scheduler-outbound-authentication"></a>Scheduler giden bağlantı kimlik doğrulaması
Zamanlayıcı işlerinin kimlik doğrulaması gerektiren tooservices çıkışı toocall gerekebilir. Bu şekilde hello Scheduler işi kaynaklarına erişebilir, çağrılan hizmet belirleyebilirsiniz. Bu hizmetlerden bazılarını diğer Azure Hizmetleri, Salesforce.com, Facebook ve güvenli özel Web siteleri içerir.

## <a name="adding-and-removing-authentication"></a>Ekleme ve kaldırma kimlik doğrulaması
Kimlik doğrulama tooa Scheduler işi basittir – bir JSON alt öğesi ekleyin ekleme `authentication` toohello `request` oluştururken veya güncelleştirirken bir iş öğesi. Gizli hello bir parçası olarak bir PUT, PATCH veya POST isteğinde – toohello Zamanlayıcı hizmeti geçirilen `authentication` nesnesi – hiçbir zaman yanıtları döndürülür. Yanıtlar, gizli bilgi toonull ayarlayın veya kimliği doğrulanmış hello varlığı temsil eden bir ortak belirteci olabilir.

tooremove kimlik doğrulaması, PUT veya hello ayarı hello işi açıkça, düzeltme eki `authentication` toonull nesne. Tüm kimlik doğrulama özellikleri geri yanıtında görmezsiniz.

Şu anda, yalnızca desteklenen hello kimlik doğrulaması hello türleridir `ClientCertificate` (Merhaba SSL/TLS istemci sertifikalarını kullanan) modeli, hello `Basic` model (Temel kimlik doğrulaması için) ve hello `ActiveDirectoryOAuth` (için Active Directory OAuth model kimlik doğrulaması.)

## <a name="request-body-for-clientcertificate-authentication"></a>İstek gövdesindeki ClientCertificate kimlik doğrulaması için
Hello kullanarak kimlik doğrulaması eklerken `ClientCertificate` model, ek öğeler hello istek gövdesindeki aşağıdaki hello belirtin.  

| Öğesi | Açıklama |
|:--- |:--- |
| *kimlik doğrulaması (üst öğe)* |Bir SSL istemci sertifikası kullanmak için kimlik doğrulaması nesne. |
| *türü* |Gereklidir. Kimlik doğrulama türü. SSL istemci sertifikaları için başlangıç değeri olmalıdır `ClientCertificate`. |
| *PFX* |Gereklidir. Base64 ile kodlanmış hello PFX dosyasının içeriğini. |
| *Parola* |Gereklidir. Parola tooaccess hello PFX dosyası. |

## <a name="response-body-for-clientcertificate-authentication"></a>Yanıt gövdesi ClientCertificate kimlik doğrulaması
Kimlik bilgileri ile bir istek gönderildiğinde hello yanıt kimlik doğrulaması ile ilgili öğeleri aşağıdaki hello içerir.

| Öğesi | Açıklama |
|:--- |:--- |
| *kimlik doğrulaması (üst öğe)* |Bir SSL istemci sertifikası kullanmak için kimlik doğrulaması nesne. |
| *türü* |Kimlik doğrulama türü. SSL istemci sertifikaları için hello değerdir `ClientCertificate`. |
| *certificateThumbprint* |Merhaba sertifikanın parmak izi hello. |
| *certificateSubjectName* |Merhaba sertifikanın Hello konu ayırt edici adı. |
| *certificateExpiration* |Merhaba sertifika Hello sona erme tarihi. |

## <a name="sample-rest-request-for-clientcertificate-authentication"></a>ClientCertificate kimlik doğrulaması için örnek REST istek
```
PUT https://management.azure.com/subscriptions/1fe0abdf-581e-4dfe-9ec7-e5cb8e7b205e/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobcollections/southeastasiajc/jobs/httpjob?api-version=2016-01-01 HTTP/1.1
User-Agent: Fiddler
Host: management.azure.com
Authorization: Bearer sometoken
Content-Type: application/json; charset=utf-8

{
  "properties": {
    "startTime": "2015-05-14T14:10:00Z",
    "action": {
      "request": {
        "uri": "https://mywebserviceendpoint.com",
        "method": "GET",
        "headers": {
          "x-ms-version": "2013-03-01"
        },
        "authentication": {
          "type": "clientcertificate",
          "password": "password",
          "pfx": "pfx key"
        }
      },
      "type": "http"
    },
    "recurrence": {
      "frequency": "minute",
      "endTime": "2016-04-10T08:00:00Z",
      "interval": 1
    },
    "state": "enabled",
  }
}
```

## <a name="sample-rest-response-for-clientcertificate-authentication"></a>Örnek REST yanıt ClientCertificate kimlik doğrulaması
```
HTTP/1.1 200 OK
Cache-Control: no-cache
Pragma: no-cache
Content-Length: 858
Content-Type: application/json; charset=utf-8
Expires: -1
x-ms-request-id: 56c7b40e-721a-437e-88e6-f68562a73aa8
Server: Microsoft-IIS/8.5
X-AspNet-Version: 4.0.30319
X-Powered-By: ASP.NET
x-ms-ratelimit-remaining-subscription-resource-requests: 599
x-ms-correlation-request-id: 1075219e-e879-4030-bc81-094e54fbabce
x-ms-routing-request-id: WESTUS:20160316T190424Z:1075219e-e879-4030-bc81-094e54fbabce
Strict-Transport-Security: max-age=31536000; includeSubDomains
Date: Wed, 16 Mar 2016 19:04:23 GMT

{
  "id": "/subscriptions/1fe0abdf-581e-4dfe-9ec7-e5cb8e7b205e/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobCollections/southeastasiajc/jobs/httpjob",
  "type": "Microsoft.Scheduler/jobCollections/jobs",
  "name": "southeastasiajc/httpjob",
  "properties": {
    "startTime": "2015-05-14T14:10:00Z",
    "action": {
      "request": {
        "uri": "https://mywebserviceendpoint.com",
        "method": "GET",
        "headers": {
          "x-ms-version": "2013-03-01"
        },
        "authentication": {
          "certificateThumbprint": "88105CG9DF9ADE75B835711D899296CB217D7055",
          "certificateExpiration": "2021-01-01T07:00:00Z",
          "certificateSubjectName": "CN=Scheduler Mgmt",
          "type": "ClientCertificate"
        }
      },
      "type": "http"
    },
    "recurrence": {
      "frequency": "minute",
      "endTime": "2016-04-10T08:00:00Z",
      "interval": 1
    },
    "state": "enabled",
    "status": {
      "nextExecutionTime": "2016-03-16T19:05:00Z",
      "executionCount": 0,
      "failureCount": 0,
      "faultedCount": 0
    }
  }
}
```

## <a name="request-body-for-basic-authentication"></a>Temel kimlik doğrulaması için istek gövdesi
Hello kullanarak kimlik doğrulaması eklerken `Basic` model, ek öğeler hello istek gövdesindeki aşağıdaki hello belirtin.

| Öğesi | Açıklama |
|:--- |:--- |
| *kimlik doğrulaması (üst öğe)* |Temel kimlik doğrulaması kullanmak için kimlik doğrulaması nesne. |
| *türü* |Gereklidir. Kimlik doğrulama türü. Temel kimlik doğrulaması için hello değeri olmalıdır `Basic`. |
| *Kullanıcı adı* |Gereklidir. Kullanıcı adı tooauthenticate. |
| *Parola* |Gereklidir. Parola tooauthenticate. |

## <a name="response-body-for-basic-authentication"></a>Temel kimlik doğrulaması için yanıt gövdesi
Kimlik bilgileri ile bir istek gönderildiğinde hello yanıt kimlik doğrulaması ile ilgili öğeleri aşağıdaki hello içerir.

| Öğesi | Açıklama |
|:--- |:--- |
| *kimlik doğrulaması (üst öğe)* |Temel kimlik doğrulaması kullanmak için kimlik doğrulaması nesne. |
| *türü* |Kimlik doğrulama türü. Temel kimlik doğrulaması için hello değerdir `Basic`. |
| *Kullanıcı adı* |Merhaba, kullanıcı adı kimlik doğrulaması. |

## <a name="sample-rest-request-for-basic-authentication"></a>Temel kimlik doğrulaması için örnek REST istek
```
PUT https://management.azure.com/subscriptions/1d908808-e491-4fe5-b97e-29886e18efd4/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobcollections/southeastasiajc/jobs/httpjob?api-version=2016-01-01 HTTP/1.1
User-Agent: Fiddler
Host: management.azure.com
Authorization: Bearer sometoken
Content-Length: 562
Content-Type: application/json; charset=utf-8

{
  "properties": {
    "startTime": "2015-05-14T14:10:00Z",
    "action": {
      "request": {
        "uri": "https://mywebserviceendpoint.com",
        "method": "GET",
        "headers": {
          "x-ms-version": "2013-03-01"
        },
        "authentication": {
          "type": "basic",
          "username": "user",
          "password": "password"
        }
      },
      "type": "http"
    },
    "recurrence": {
      "frequency": "minute",
      "endTime": "2016-04-10T08:00:00Z",
      "interval": 1
    },
    "state": "enabled",
  }
}
```

## <a name="sample-rest-response-for-basic-authentication"></a>Temel kimlik doğrulaması için örnek REST yanıt
```
HTTP/1.1 200 OK
Cache-Control: no-cache
Pragma: no-cache
Content-Length: 701
Content-Type: application/json; charset=utf-8
Expires: -1
x-ms-request-id: a2dcb9cd-1aea-4887-8893-d81273a8cf04
Server: Microsoft-IIS/8.5
X-AspNet-Version: 4.0.30319
X-Powered-By: ASP.NET
x-ms-ratelimit-remaining-subscription-resource-requests: 599
x-ms-correlation-request-id: 7816f222-6ea7-468d-b919-e6ddebbd7e95
x-ms-routing-request-id: WESTUS:20160316T190506Z:7816f222-6ea7-468d-b919-e6ddebbd7e95
Strict-Transport-Security: max-age=31536000; includeSubDomains
Date: Wed, 16 Mar 2016 19:05:06 GMT

{  
   "id":"/subscriptions/1d908808-e491-4fe5-b97e-29886e18efd4/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobCollections/southeastasiajc/jobs/httpjob",
   "type":"Microsoft.Scheduler/jobCollections/jobs",
   "name":"southeastasiajc/httpjob",
   "properties":{  
      "startTime":"2015-05-14T14:10:00Z",
      "action":{  
         "request":{  
            "uri":"https://mywebserviceendpoint.com",
            "method":"GET",
            "headers":{  
               "x-ms-version":"2013-03-01"
            },
            "authentication":{  
               "username":"user1",
               "type":"Basic"
            }
         },
         "type":"http"
      },
      "recurrence":{  
         "frequency":"minute",
         "endTime":"2016-04-10T08:00:00Z",
         "interval":1
      },
      "state":"enabled",
      "status":{  
         "nextExecutionTime":"2016-03-16T19:06:00Z",
         "executionCount":0,
         "failureCount":0,
         "faultedCount":0
      }
   }
}
```

## <a name="request-body-for-activedirectoryoauth-authentication"></a>İstek gövdesindeki ActiveDirectoryOAuth kimlik doğrulaması için
Hello kullanarak kimlik doğrulaması eklerken `ActiveDirectoryOAuth` model, ek öğeler hello istek gövdesindeki aşağıdaki hello belirtin.

| Öğesi | Açıklama |
|:--- |:--- |
| *kimlik doğrulaması (üst öğe)* |ActiveDirectoryOAuth kimlik doğrulaması kullanmak için kimlik doğrulaması nesne. |
| *türü* |Gereklidir. Kimlik doğrulama türü. ActiveDirectoryOAuth kimlik doğrulaması için hello değeri olmalıdır `ActiveDirectoryOAuth`. |
| *Kiracı* |Gereklidir. hello Azure AD Kiracı Hello Kiracı tanımlayıcısı. |
| *Hedef kitle* |Gereklidir. Bu toohttps://management.core.windows.net/ ayarlanır. |
| *istemci kimliği* |Gereklidir. Merhaba istemci tanımlayıcısı hello Azure AD uygulaması sağlar. |
| *Gizli* |Gereklidir. Merhaba belirteç isteme hello istemci gizli anahtarı. |

### <a name="determining-your-tenant-identifier"></a>Kiracı Tanımlayıcınız belirleme
Merhaba Kiracı tanımlayıcı hello Azure AD kiracısı çalıştırarak bulabileceğiniz `Get-AzureAccount` Azure PowerShell'de.

## <a name="response-body-for-activedirectoryoauth-authentication"></a>Yanıt gövdesi ActiveDirectoryOAuth kimlik doğrulaması
Kimlik bilgileri ile bir istek gönderildiğinde hello yanıt kimlik doğrulaması ile ilgili öğeleri aşağıdaki hello içerir.

| Öğesi | Açıklama |
|:--- |:--- |
| *kimlik doğrulaması (üst öğe)* |ActiveDirectoryOAuth kimlik doğrulaması kullanmak için kimlik doğrulaması nesne. |
| *türü* |Kimlik doğrulama türü. ActiveDirectoryOAuth kimlik doğrulaması için hello değerdir `ActiveDirectoryOAuth`. |
| *Kiracı* |hello Azure AD Kiracı Hello Kiracı tanımlayıcısı. |
| *Hedef kitle* |Bu toohttps://management.core.windows.net/ ayarlanır. |
| *istemci kimliği* |Merhaba Azure AD uygulaması için istemci tanımlayıcı hello. |

## <a name="sample-rest-request-for-activedirectoryoauth-authentication"></a>ActiveDirectoryOAuth kimlik doğrulaması için örnek REST istek
```
PUT https://management.azure.com/subscriptions/1d908808-e491-4fe5-b97e-29886e18efd4/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobcollections/southeastasiajc/jobs/httpjob?api-version=2016-01-01 HTTP/1.1
User-Agent: Fiddler
Host: management.azure.com
Authorization: Bearer sometoken
Content-Length: 757
Content-Type: application/json; charset=utf-8

{
  "properties": {
    "startTime": "2015-05-14T14:10:00Z",
    "action": {
      "request": {
        "uri": "https://mywebserviceendpoint.com",
        "method": "GET",
        "headers": {
          "x-ms-version": "2013-03-01"
        },
        "authentication": {
          "tenant":"microsoft.onmicrosoft.com",
          "audience":"https://management.core.windows.net/",
          "clientId":"dc23e764-9be6-4a33-9b9a-c46e36f0c137",
          "secret": "G6u071r8Gjw4V4KSibnb+VK4+tX399hkHaj7LOyHuj5=",
          "type":"ActiveDirectoryOAuth"
        }
      },
      "type": "http"
    },
    "recurrence": {
      "frequency": "minute",
      "endTime": "2016-04-10T08:00:00Z",
      "interval": 1
    },
    "state": "enabled",
  }
}
```

## <a name="sample-rest-response-for-activedirectoryoauth-authentication"></a>Örnek REST yanıt ActiveDirectoryOAuth kimlik doğrulaması
```
HTTP/1.1 200 OK
Cache-Control: no-cache
Pragma: no-cache
Content-Length: 885
Content-Type: application/json; charset=utf-8
Expires: -1
x-ms-request-id: 86d8e9fd-ac0d-4bed-9420-9baba1af3251
Server: Microsoft-IIS/8.5
X-AspNet-Version: 4.0.30319
X-Powered-By: ASP.NET
x-ms-ratelimit-remaining-subscription-resource-requests: 599
x-ms-correlation-request-id: 5183bbf4-9fa1-44bb-98c6-6872e3f2e7ce
x-ms-routing-request-id: WESTUS:20160316T191003Z:5183bbf4-9fa1-44bb-98c6-6872e3f2e7ce
Strict-Transport-Security: max-age=31536000; includeSubDomains
Date: Wed, 16 Mar 2016 19:10:02 GMT

{  
   "id":"/subscriptions/1d908808-e491-4fe5-b97e-29886e18efd4/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobCollections/southeastasiajc/jobs/httpjob",
   "type":"Microsoft.Scheduler/jobCollections/jobs",
   "name":"southeastasiajc/httpjob",
   "properties":{  
      "startTime":"2015-05-14T14:10:00Z",
      "action":{  
         "request":{  
            "uri":"https://mywebserviceendpoint.com",
            "method":"GET",
            "headers":{  
               "x-ms-version":"2013-03-01"
            },
            "authentication":{  
               "tenant":"microsoft.onmicrosoft.com",
               "audience":"https://management.core.windows.net/",
               "clientId":"dc23e764-9be6-4a33-9b9a-c46e36f0c137",
               "type":"ActiveDirectoryOAuth"
            }
         },
         "type":"http"
      },
      "recurrence":{  
         "frequency":"minute",
         "endTime":"2016-04-10T08:00:00Z",
         "interval":1
      },
      "state":"enabled",
      "status":{  
         "lastExecutionTime":"2016-03-16T19:10:00.3762123Z",
         "nextExecutionTime":"2016-03-16T19:11:00Z",
         "executionCount":5,
         "failureCount":5,
         "faultedCount":1
      }
   }
}
```

## <a name="see-also"></a>Ayrıca Bkz.
 [Scheduler nedir?](scheduler-intro.md)

 [Azure Scheduler kavramları, terminolojisi ve varlık hiyerarşisi](scheduler-concepts-terms.md)

 [Zamanlayıcı hello Azure portalını kullanmaya başlama](scheduler-get-started-portal.md)

 [Azure Scheduler’da planlar ve faturalama](scheduler-plans-billing.md)

 [Azure Scheduler REST API başvurusu](https://msdn.microsoft.com/library/mt629143)

 [Azure Scheduler PowerShell cmdlet’leri başvurusu](scheduler-powershell-reference.md)

 [Yüksek Azure Scheduler kullanılabilirliği ve güvenilirliği](scheduler-high-availability-reliability.md)

 [Azure Scheduler sınırları, varsayılanları ve hata kodları](scheduler-limits-defaults-errors.md)

