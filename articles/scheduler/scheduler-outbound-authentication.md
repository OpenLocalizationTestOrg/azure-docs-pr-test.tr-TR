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
# <a name="scheduler-outbound-authentication"></a><span data-ttu-id="cc61a-103">Scheduler giden bağlantı kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="cc61a-103">Scheduler Outbound Authentication</span></span>
<span data-ttu-id="cc61a-104">Zamanlayıcı işlerinin kimlik doğrulaması gerektiren tooservices çıkışı toocall gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="cc61a-104">Scheduler jobs may need toocall out tooservices that require authentication.</span></span> <span data-ttu-id="cc61a-105">Bu şekilde hello Scheduler işi kaynaklarına erişebilir, çağrılan hizmet belirleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cc61a-105">This way, a called service can determine if hello Scheduler job can access its resources.</span></span> <span data-ttu-id="cc61a-106">Bu hizmetlerden bazılarını diğer Azure Hizmetleri, Salesforce.com, Facebook ve güvenli özel Web siteleri içerir.</span><span class="sxs-lookup"><span data-stu-id="cc61a-106">Some of these services include other Azure services, Salesforce.com, Facebook, and secure custom websites.</span></span>

## <a name="adding-and-removing-authentication"></a><span data-ttu-id="cc61a-107">Ekleme ve kaldırma kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="cc61a-107">Adding and Removing Authentication</span></span>
<span data-ttu-id="cc61a-108">Kimlik doğrulama tooa Scheduler işi basittir – bir JSON alt öğesi ekleyin ekleme `authentication` toohello `request` oluştururken veya güncelleştirirken bir iş öğesi.</span><span class="sxs-lookup"><span data-stu-id="cc61a-108">Adding authentication tooa Scheduler job is simple – add a JSON child element `authentication` toohello `request` element when creating or updating a job.</span></span> <span data-ttu-id="cc61a-109">Gizli hello bir parçası olarak bir PUT, PATCH veya POST isteğinde – toohello Zamanlayıcı hizmeti geçirilen `authentication` nesnesi – hiçbir zaman yanıtları döndürülür.</span><span class="sxs-lookup"><span data-stu-id="cc61a-109">Secrets passed toohello Scheduler service in a PUT, PATCH, or POST request – as part of hello `authentication` object – are never returned in responses.</span></span> <span data-ttu-id="cc61a-110">Yanıtlar, gizli bilgi toonull ayarlayın veya kimliği doğrulanmış hello varlığı temsil eden bir ortak belirteci olabilir.</span><span class="sxs-lookup"><span data-stu-id="cc61a-110">In responses, secret information is set toonull or may have a public token that represents hello authenticated entity.</span></span>

<span data-ttu-id="cc61a-111">tooremove kimlik doğrulaması, PUT veya hello ayarı hello işi açıkça, düzeltme eki `authentication` toonull nesne.</span><span class="sxs-lookup"><span data-stu-id="cc61a-111">tooremove authentication, PUT or PATCH hello job explicitly, setting hello `authentication` object toonull.</span></span> <span data-ttu-id="cc61a-112">Tüm kimlik doğrulama özellikleri geri yanıtında görmezsiniz.</span><span class="sxs-lookup"><span data-stu-id="cc61a-112">You will not see any authentication properties back in response.</span></span>

<span data-ttu-id="cc61a-113">Şu anda, yalnızca desteklenen hello kimlik doğrulaması hello türleridir `ClientCertificate` (Merhaba SSL/TLS istemci sertifikalarını kullanan) modeli, hello `Basic` model (Temel kimlik doğrulaması için) ve hello `ActiveDirectoryOAuth` (için Active Directory OAuth model kimlik doğrulaması.)</span><span class="sxs-lookup"><span data-stu-id="cc61a-113">Currently, hello only supported authentication types are hello `ClientCertificate` model (for using hello SSL/TLS client certificates), hello `Basic` model (for Basic authentication), and hello `ActiveDirectoryOAuth` model (for Active Directory OAuth authentication.)</span></span>

## <a name="request-body-for-clientcertificate-authentication"></a><span data-ttu-id="cc61a-114">İstek gövdesindeki ClientCertificate kimlik doğrulaması için</span><span class="sxs-lookup"><span data-stu-id="cc61a-114">Request Body for ClientCertificate Authentication</span></span>
<span data-ttu-id="cc61a-115">Hello kullanarak kimlik doğrulaması eklerken `ClientCertificate` model, ek öğeler hello istek gövdesindeki aşağıdaki hello belirtin.</span><span class="sxs-lookup"><span data-stu-id="cc61a-115">When adding authentication using hello `ClientCertificate` model, specify hello following additional elements in hello request body.</span></span>  

| <span data-ttu-id="cc61a-116">Öğesi</span><span class="sxs-lookup"><span data-stu-id="cc61a-116">Element</span></span> | <span data-ttu-id="cc61a-117">Açıklama</span><span class="sxs-lookup"><span data-stu-id="cc61a-117">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="cc61a-118">*kimlik doğrulaması (üst öğe)*</span><span class="sxs-lookup"><span data-stu-id="cc61a-118">*authentication (parent element)*</span></span> |<span data-ttu-id="cc61a-119">Bir SSL istemci sertifikası kullanmak için kimlik doğrulaması nesne.</span><span class="sxs-lookup"><span data-stu-id="cc61a-119">Authentication object for using an SSL client certificate.</span></span> |
| <span data-ttu-id="cc61a-120">*türü*</span><span class="sxs-lookup"><span data-stu-id="cc61a-120">*type*</span></span> |<span data-ttu-id="cc61a-121">Gereklidir.</span><span class="sxs-lookup"><span data-stu-id="cc61a-121">Required.</span></span> <span data-ttu-id="cc61a-122">Kimlik doğrulama türü. SSL istemci sertifikaları için başlangıç değeri olmalıdır `ClientCertificate`.</span><span class="sxs-lookup"><span data-stu-id="cc61a-122">Type of authentication.For SSL client certificates, hello value must be `ClientCertificate`.</span></span> |
| <span data-ttu-id="cc61a-123">*PFX*</span><span class="sxs-lookup"><span data-stu-id="cc61a-123">*pfx*</span></span> |<span data-ttu-id="cc61a-124">Gereklidir.</span><span class="sxs-lookup"><span data-stu-id="cc61a-124">Required.</span></span> <span data-ttu-id="cc61a-125">Base64 ile kodlanmış hello PFX dosyasının içeriğini.</span><span class="sxs-lookup"><span data-stu-id="cc61a-125">Base64-encoded contents of hello PFX file.</span></span> |
| <span data-ttu-id="cc61a-126">*Parola*</span><span class="sxs-lookup"><span data-stu-id="cc61a-126">*password*</span></span> |<span data-ttu-id="cc61a-127">Gereklidir.</span><span class="sxs-lookup"><span data-stu-id="cc61a-127">Required.</span></span> <span data-ttu-id="cc61a-128">Parola tooaccess hello PFX dosyası.</span><span class="sxs-lookup"><span data-stu-id="cc61a-128">Password tooaccess hello PFX file.</span></span> |

## <a name="response-body-for-clientcertificate-authentication"></a><span data-ttu-id="cc61a-129">Yanıt gövdesi ClientCertificate kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="cc61a-129">Response Body for ClientCertificate Authentication</span></span>
<span data-ttu-id="cc61a-130">Kimlik bilgileri ile bir istek gönderildiğinde hello yanıt kimlik doğrulaması ile ilgili öğeleri aşağıdaki hello içerir.</span><span class="sxs-lookup"><span data-stu-id="cc61a-130">When a request is sent with authentication info, hello response contains hello following authentication-related elements.</span></span>

| <span data-ttu-id="cc61a-131">Öğesi</span><span class="sxs-lookup"><span data-stu-id="cc61a-131">Element</span></span> | <span data-ttu-id="cc61a-132">Açıklama</span><span class="sxs-lookup"><span data-stu-id="cc61a-132">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="cc61a-133">*kimlik doğrulaması (üst öğe)*</span><span class="sxs-lookup"><span data-stu-id="cc61a-133">*authentication (parent element)*</span></span> |<span data-ttu-id="cc61a-134">Bir SSL istemci sertifikası kullanmak için kimlik doğrulaması nesne.</span><span class="sxs-lookup"><span data-stu-id="cc61a-134">Authentication object for using an SSL client certificate.</span></span> |
| <span data-ttu-id="cc61a-135">*türü*</span><span class="sxs-lookup"><span data-stu-id="cc61a-135">*type*</span></span> |<span data-ttu-id="cc61a-136">Kimlik doğrulama türü.</span><span class="sxs-lookup"><span data-stu-id="cc61a-136">Type of authentication.</span></span> <span data-ttu-id="cc61a-137">SSL istemci sertifikaları için hello değerdir `ClientCertificate`.</span><span class="sxs-lookup"><span data-stu-id="cc61a-137">For SSL client certificates, hello value is `ClientCertificate`.</span></span> |
| <span data-ttu-id="cc61a-138">*certificateThumbprint*</span><span class="sxs-lookup"><span data-stu-id="cc61a-138">*certificateThumbprint*</span></span> |<span data-ttu-id="cc61a-139">Merhaba sertifikanın parmak izi hello.</span><span class="sxs-lookup"><span data-stu-id="cc61a-139">hello thumbprint of hello certificate.</span></span> |
| <span data-ttu-id="cc61a-140">*certificateSubjectName*</span><span class="sxs-lookup"><span data-stu-id="cc61a-140">*certificateSubjectName*</span></span> |<span data-ttu-id="cc61a-141">Merhaba sertifikanın Hello konu ayırt edici adı.</span><span class="sxs-lookup"><span data-stu-id="cc61a-141">hello subject distinguished name of hello certificate.</span></span> |
| <span data-ttu-id="cc61a-142">*certificateExpiration*</span><span class="sxs-lookup"><span data-stu-id="cc61a-142">*certificateExpiration*</span></span> |<span data-ttu-id="cc61a-143">Merhaba sertifika Hello sona erme tarihi.</span><span class="sxs-lookup"><span data-stu-id="cc61a-143">hello expiration date of hello certificate.</span></span> |

## <a name="sample-rest-request-for-clientcertificate-authentication"></a><span data-ttu-id="cc61a-144">ClientCertificate kimlik doğrulaması için örnek REST istek</span><span class="sxs-lookup"><span data-stu-id="cc61a-144">Sample REST Request for ClientCertificate Authentication</span></span>
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

## <a name="sample-rest-response-for-clientcertificate-authentication"></a><span data-ttu-id="cc61a-145">Örnek REST yanıt ClientCertificate kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="cc61a-145">Sample REST Response for ClientCertificate Authentication</span></span>
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

## <a name="request-body-for-basic-authentication"></a><span data-ttu-id="cc61a-146">Temel kimlik doğrulaması için istek gövdesi</span><span class="sxs-lookup"><span data-stu-id="cc61a-146">Request Body for Basic Authentication</span></span>
<span data-ttu-id="cc61a-147">Hello kullanarak kimlik doğrulaması eklerken `Basic` model, ek öğeler hello istek gövdesindeki aşağıdaki hello belirtin.</span><span class="sxs-lookup"><span data-stu-id="cc61a-147">When adding authentication using hello `Basic` model, specify hello following additional elements in hello request body.</span></span>

| <span data-ttu-id="cc61a-148">Öğesi</span><span class="sxs-lookup"><span data-stu-id="cc61a-148">Element</span></span> | <span data-ttu-id="cc61a-149">Açıklama</span><span class="sxs-lookup"><span data-stu-id="cc61a-149">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="cc61a-150">*kimlik doğrulaması (üst öğe)*</span><span class="sxs-lookup"><span data-stu-id="cc61a-150">*authentication (parent element)*</span></span> |<span data-ttu-id="cc61a-151">Temel kimlik doğrulaması kullanmak için kimlik doğrulaması nesne.</span><span class="sxs-lookup"><span data-stu-id="cc61a-151">Authentication object for using Basic authentication.</span></span> |
| <span data-ttu-id="cc61a-152">*türü*</span><span class="sxs-lookup"><span data-stu-id="cc61a-152">*type*</span></span> |<span data-ttu-id="cc61a-153">Gereklidir.</span><span class="sxs-lookup"><span data-stu-id="cc61a-153">Required.</span></span> <span data-ttu-id="cc61a-154">Kimlik doğrulama türü.</span><span class="sxs-lookup"><span data-stu-id="cc61a-154">Type of authentication.</span></span> <span data-ttu-id="cc61a-155">Temel kimlik doğrulaması için hello değeri olmalıdır `Basic`.</span><span class="sxs-lookup"><span data-stu-id="cc61a-155">For Basic authentication, hello value must be `Basic`.</span></span> |
| <span data-ttu-id="cc61a-156">*Kullanıcı adı*</span><span class="sxs-lookup"><span data-stu-id="cc61a-156">*username*</span></span> |<span data-ttu-id="cc61a-157">Gereklidir.</span><span class="sxs-lookup"><span data-stu-id="cc61a-157">Required.</span></span> <span data-ttu-id="cc61a-158">Kullanıcı adı tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="cc61a-158">Username tooauthenticate.</span></span> |
| <span data-ttu-id="cc61a-159">*Parola*</span><span class="sxs-lookup"><span data-stu-id="cc61a-159">*password*</span></span> |<span data-ttu-id="cc61a-160">Gereklidir.</span><span class="sxs-lookup"><span data-stu-id="cc61a-160">Required.</span></span> <span data-ttu-id="cc61a-161">Parola tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="cc61a-161">Password tooauthenticate.</span></span> |

## <a name="response-body-for-basic-authentication"></a><span data-ttu-id="cc61a-162">Temel kimlik doğrulaması için yanıt gövdesi</span><span class="sxs-lookup"><span data-stu-id="cc61a-162">Response Body for Basic Authentication</span></span>
<span data-ttu-id="cc61a-163">Kimlik bilgileri ile bir istek gönderildiğinde hello yanıt kimlik doğrulaması ile ilgili öğeleri aşağıdaki hello içerir.</span><span class="sxs-lookup"><span data-stu-id="cc61a-163">When a request is sent with authentication info, hello response contains hello following authentication-related elements.</span></span>

| <span data-ttu-id="cc61a-164">Öğesi</span><span class="sxs-lookup"><span data-stu-id="cc61a-164">Element</span></span> | <span data-ttu-id="cc61a-165">Açıklama</span><span class="sxs-lookup"><span data-stu-id="cc61a-165">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="cc61a-166">*kimlik doğrulaması (üst öğe)*</span><span class="sxs-lookup"><span data-stu-id="cc61a-166">*authentication (parent element)*</span></span> |<span data-ttu-id="cc61a-167">Temel kimlik doğrulaması kullanmak için kimlik doğrulaması nesne.</span><span class="sxs-lookup"><span data-stu-id="cc61a-167">Authentication object for using Basic authentication.</span></span> |
| <span data-ttu-id="cc61a-168">*türü*</span><span class="sxs-lookup"><span data-stu-id="cc61a-168">*type*</span></span> |<span data-ttu-id="cc61a-169">Kimlik doğrulama türü.</span><span class="sxs-lookup"><span data-stu-id="cc61a-169">Type of authentication.</span></span> <span data-ttu-id="cc61a-170">Temel kimlik doğrulaması için hello değerdir `Basic`.</span><span class="sxs-lookup"><span data-stu-id="cc61a-170">For Basic authentication, hello value is `Basic`.</span></span> |
| <span data-ttu-id="cc61a-171">*Kullanıcı adı*</span><span class="sxs-lookup"><span data-stu-id="cc61a-171">*username*</span></span> |<span data-ttu-id="cc61a-172">Merhaba, kullanıcı adı kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="cc61a-172">hello authenticated username.</span></span> |

## <a name="sample-rest-request-for-basic-authentication"></a><span data-ttu-id="cc61a-173">Temel kimlik doğrulaması için örnek REST istek</span><span class="sxs-lookup"><span data-stu-id="cc61a-173">Sample REST Request for Basic Authentication</span></span>
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

## <a name="sample-rest-response-for-basic-authentication"></a><span data-ttu-id="cc61a-174">Temel kimlik doğrulaması için örnek REST yanıt</span><span class="sxs-lookup"><span data-stu-id="cc61a-174">Sample REST Response for Basic Authentication</span></span>
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

## <a name="request-body-for-activedirectoryoauth-authentication"></a><span data-ttu-id="cc61a-175">İstek gövdesindeki ActiveDirectoryOAuth kimlik doğrulaması için</span><span class="sxs-lookup"><span data-stu-id="cc61a-175">Request Body for ActiveDirectoryOAuth Authentication</span></span>
<span data-ttu-id="cc61a-176">Hello kullanarak kimlik doğrulaması eklerken `ActiveDirectoryOAuth` model, ek öğeler hello istek gövdesindeki aşağıdaki hello belirtin.</span><span class="sxs-lookup"><span data-stu-id="cc61a-176">When adding authentication using hello `ActiveDirectoryOAuth` model, specify hello following additional elements in hello request body.</span></span>

| <span data-ttu-id="cc61a-177">Öğesi</span><span class="sxs-lookup"><span data-stu-id="cc61a-177">Element</span></span> | <span data-ttu-id="cc61a-178">Açıklama</span><span class="sxs-lookup"><span data-stu-id="cc61a-178">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="cc61a-179">*kimlik doğrulaması (üst öğe)*</span><span class="sxs-lookup"><span data-stu-id="cc61a-179">*authentication (parent element)*</span></span> |<span data-ttu-id="cc61a-180">ActiveDirectoryOAuth kimlik doğrulaması kullanmak için kimlik doğrulaması nesne.</span><span class="sxs-lookup"><span data-stu-id="cc61a-180">Authentication object for using ActiveDirectoryOAuth authentication.</span></span> |
| <span data-ttu-id="cc61a-181">*türü*</span><span class="sxs-lookup"><span data-stu-id="cc61a-181">*type*</span></span> |<span data-ttu-id="cc61a-182">Gereklidir.</span><span class="sxs-lookup"><span data-stu-id="cc61a-182">Required.</span></span> <span data-ttu-id="cc61a-183">Kimlik doğrulama türü.</span><span class="sxs-lookup"><span data-stu-id="cc61a-183">Type of authentication.</span></span> <span data-ttu-id="cc61a-184">ActiveDirectoryOAuth kimlik doğrulaması için hello değeri olmalıdır `ActiveDirectoryOAuth`.</span><span class="sxs-lookup"><span data-stu-id="cc61a-184">For ActiveDirectoryOAuth authentication, hello value must be `ActiveDirectoryOAuth`.</span></span> |
| <span data-ttu-id="cc61a-185">*Kiracı*</span><span class="sxs-lookup"><span data-stu-id="cc61a-185">*tenant*</span></span> |<span data-ttu-id="cc61a-186">Gereklidir.</span><span class="sxs-lookup"><span data-stu-id="cc61a-186">Required.</span></span> <span data-ttu-id="cc61a-187">hello Azure AD Kiracı Hello Kiracı tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="cc61a-187">hello tenant identifier for hello Azure AD tenant.</span></span> |
| <span data-ttu-id="cc61a-188">*Hedef kitle*</span><span class="sxs-lookup"><span data-stu-id="cc61a-188">*audience*</span></span> |<span data-ttu-id="cc61a-189">Gereklidir.</span><span class="sxs-lookup"><span data-stu-id="cc61a-189">Required.</span></span> <span data-ttu-id="cc61a-190">Bu toohttps://management.core.windows.net/ ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="cc61a-190">This is set toohttps://management.core.windows.net/.</span></span> |
| <span data-ttu-id="cc61a-191">*istemci kimliği*</span><span class="sxs-lookup"><span data-stu-id="cc61a-191">*clientId*</span></span> |<span data-ttu-id="cc61a-192">Gereklidir.</span><span class="sxs-lookup"><span data-stu-id="cc61a-192">Required.</span></span> <span data-ttu-id="cc61a-193">Merhaba istemci tanımlayıcısı hello Azure AD uygulaması sağlar.</span><span class="sxs-lookup"><span data-stu-id="cc61a-193">Provide hello client identifier for hello Azure AD application.</span></span> |
| <span data-ttu-id="cc61a-194">*Gizli*</span><span class="sxs-lookup"><span data-stu-id="cc61a-194">*secret*</span></span> |<span data-ttu-id="cc61a-195">Gereklidir.</span><span class="sxs-lookup"><span data-stu-id="cc61a-195">Required.</span></span> <span data-ttu-id="cc61a-196">Merhaba belirteç isteme hello istemci gizli anahtarı.</span><span class="sxs-lookup"><span data-stu-id="cc61a-196">Secret of hello client that is requesting hello token.</span></span> |

### <a name="determining-your-tenant-identifier"></a><span data-ttu-id="cc61a-197">Kiracı Tanımlayıcınız belirleme</span><span class="sxs-lookup"><span data-stu-id="cc61a-197">Determining your Tenant Identifier</span></span>
<span data-ttu-id="cc61a-198">Merhaba Kiracı tanımlayıcı hello Azure AD kiracısı çalıştırarak bulabileceğiniz `Get-AzureAccount` Azure PowerShell'de.</span><span class="sxs-lookup"><span data-stu-id="cc61a-198">You can find hello tenant identifier for hello Azure AD tenant by running `Get-AzureAccount` in Azure PowerShell.</span></span>

## <a name="response-body-for-activedirectoryoauth-authentication"></a><span data-ttu-id="cc61a-199">Yanıt gövdesi ActiveDirectoryOAuth kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="cc61a-199">Response Body for ActiveDirectoryOAuth Authentication</span></span>
<span data-ttu-id="cc61a-200">Kimlik bilgileri ile bir istek gönderildiğinde hello yanıt kimlik doğrulaması ile ilgili öğeleri aşağıdaki hello içerir.</span><span class="sxs-lookup"><span data-stu-id="cc61a-200">When a request is sent with authentication info, hello response contains hello following authentication-related elements.</span></span>

| <span data-ttu-id="cc61a-201">Öğesi</span><span class="sxs-lookup"><span data-stu-id="cc61a-201">Element</span></span> | <span data-ttu-id="cc61a-202">Açıklama</span><span class="sxs-lookup"><span data-stu-id="cc61a-202">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="cc61a-203">*kimlik doğrulaması (üst öğe)*</span><span class="sxs-lookup"><span data-stu-id="cc61a-203">*authentication (parent element)*</span></span> |<span data-ttu-id="cc61a-204">ActiveDirectoryOAuth kimlik doğrulaması kullanmak için kimlik doğrulaması nesne.</span><span class="sxs-lookup"><span data-stu-id="cc61a-204">Authentication object for using ActiveDirectoryOAuth authentication.</span></span> |
| <span data-ttu-id="cc61a-205">*türü*</span><span class="sxs-lookup"><span data-stu-id="cc61a-205">*type*</span></span> |<span data-ttu-id="cc61a-206">Kimlik doğrulama türü.</span><span class="sxs-lookup"><span data-stu-id="cc61a-206">Type of authentication.</span></span> <span data-ttu-id="cc61a-207">ActiveDirectoryOAuth kimlik doğrulaması için hello değerdir `ActiveDirectoryOAuth`.</span><span class="sxs-lookup"><span data-stu-id="cc61a-207">For ActiveDirectoryOAuth authentication, hello value is `ActiveDirectoryOAuth`.</span></span> |
| <span data-ttu-id="cc61a-208">*Kiracı*</span><span class="sxs-lookup"><span data-stu-id="cc61a-208">*tenant*</span></span> |<span data-ttu-id="cc61a-209">hello Azure AD Kiracı Hello Kiracı tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="cc61a-209">hello tenant identifier for hello Azure AD tenant.</span></span> |
| <span data-ttu-id="cc61a-210">*Hedef kitle*</span><span class="sxs-lookup"><span data-stu-id="cc61a-210">*audience*</span></span> |<span data-ttu-id="cc61a-211">Bu toohttps://management.core.windows.net/ ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="cc61a-211">This is set toohttps://management.core.windows.net/.</span></span> |
| <span data-ttu-id="cc61a-212">*istemci kimliği*</span><span class="sxs-lookup"><span data-stu-id="cc61a-212">*clientId*</span></span> |<span data-ttu-id="cc61a-213">Merhaba Azure AD uygulaması için istemci tanımlayıcı hello.</span><span class="sxs-lookup"><span data-stu-id="cc61a-213">hello client identifier for hello Azure AD application.</span></span> |

## <a name="sample-rest-request-for-activedirectoryoauth-authentication"></a><span data-ttu-id="cc61a-214">ActiveDirectoryOAuth kimlik doğrulaması için örnek REST istek</span><span class="sxs-lookup"><span data-stu-id="cc61a-214">Sample REST Request for ActiveDirectoryOAuth Authentication</span></span>
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

## <a name="sample-rest-response-for-activedirectoryoauth-authentication"></a><span data-ttu-id="cc61a-215">Örnek REST yanıt ActiveDirectoryOAuth kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="cc61a-215">Sample REST Response for ActiveDirectoryOAuth Authentication</span></span>
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

## <a name="see-also"></a><span data-ttu-id="cc61a-216">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="cc61a-216">See Also</span></span>
 [<span data-ttu-id="cc61a-217">Scheduler nedir?</span><span class="sxs-lookup"><span data-stu-id="cc61a-217">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="cc61a-218">Azure Scheduler kavramları, terminolojisi ve varlık hiyerarşisi</span><span class="sxs-lookup"><span data-stu-id="cc61a-218">Azure Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="cc61a-219">Zamanlayıcı hello Azure portalını kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="cc61a-219">Get started using Scheduler in hello Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="cc61a-220">Azure Scheduler’da planlar ve faturalama</span><span class="sxs-lookup"><span data-stu-id="cc61a-220">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="cc61a-221">Azure Scheduler REST API başvurusu</span><span class="sxs-lookup"><span data-stu-id="cc61a-221">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="cc61a-222">Azure Scheduler PowerShell cmdlet’leri başvurusu</span><span class="sxs-lookup"><span data-stu-id="cc61a-222">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="cc61a-223">Yüksek Azure Scheduler kullanılabilirliği ve güvenilirliği</span><span class="sxs-lookup"><span data-stu-id="cc61a-223">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="cc61a-224">Azure Scheduler sınırları, varsayılanları ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="cc61a-224">Azure Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

