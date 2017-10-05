---
title: "Scheduler giden bağlantı kimlik doğrulaması"
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
ms.openlocfilehash: e345b2e22daae5b24c23645f7d2636f66df630ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="scheduler-outbound-authentication"></a><span data-ttu-id="d1d19-103">Scheduler giden bağlantı kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="d1d19-103">Scheduler Outbound Authentication</span></span>
<span data-ttu-id="d1d19-104">Zamanlayıcı işlerinin kimlik doğrulaması gerektiren hizmetleri çağrısı gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="d1d19-104">Scheduler jobs may need to call out to services that require authentication.</span></span> <span data-ttu-id="d1d19-105">Bu şekilde, Scheduler işi kaynaklarına erişebilir, çağrılan hizmet belirleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d1d19-105">This way, a called service can determine if the Scheduler job can access its resources.</span></span> <span data-ttu-id="d1d19-106">Bu hizmetlerden bazılarını diğer Azure Hizmetleri, Salesforce.com, Facebook ve güvenli özel Web siteleri içerir.</span><span class="sxs-lookup"><span data-stu-id="d1d19-106">Some of these services include other Azure services, Salesforce.com, Facebook, and secure custom websites.</span></span>

## <a name="adding-and-removing-authentication"></a><span data-ttu-id="d1d19-107">Ekleme ve kaldırma kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="d1d19-107">Adding and Removing Authentication</span></span>
<span data-ttu-id="d1d19-108">Scheduler işi için kimlik doğrulaması basittir – bir JSON alt öğesi ekleyin ekleme `authentication` için `request` oluştururken veya güncelleştirirken bir iş öğesi.</span><span class="sxs-lookup"><span data-stu-id="d1d19-108">Adding authentication to a Scheduler job is simple – add a JSON child element `authentication` to the `request` element when creating or updating a job.</span></span> <span data-ttu-id="d1d19-109">Gizli bir parçası olarak bir PUT, PATCH veya POST isteğinde – Zamanlayıcı hizmeti için geçirilen `authentication` nesnesi – hiçbir zaman yanıtları döndürülür.</span><span class="sxs-lookup"><span data-stu-id="d1d19-109">Secrets passed to the Scheduler service in a PUT, PATCH, or POST request – as part of the `authentication` object – are never returned in responses.</span></span> <span data-ttu-id="d1d19-110">Yanıtları, gizli bilgilerini ayarlamak null veya kimliği doğrulanmış varlık temsil eden bir ortak belirteci olabilir.</span><span class="sxs-lookup"><span data-stu-id="d1d19-110">In responses, secret information is set to null or may have a public token that represents the authenticated entity.</span></span>

<span data-ttu-id="d1d19-111">Kimlik doğrulama kaldırmak için PUT veya ayarlama işi açıkça, düzeltme eki `authentication` nesne null.</span><span class="sxs-lookup"><span data-stu-id="d1d19-111">To remove authentication, PUT or PATCH the job explicitly, setting the `authentication` object to null.</span></span> <span data-ttu-id="d1d19-112">Tüm kimlik doğrulama özellikleri geri yanıtında görmezsiniz.</span><span class="sxs-lookup"><span data-stu-id="d1d19-112">You will not see any authentication properties back in response.</span></span>

<span data-ttu-id="d1d19-113">Şu anda, yalnızca desteklenen kimlik doğrulama türleridir `ClientCertificate` (için SSL/TLS istemci sertifikalarını kullanarak), model `Basic` (Temel kimlik doğrulaması için), model ve `ActiveDirectoryOAuth` model (için Active Directory OAuth kimlik doğrulaması.)</span><span class="sxs-lookup"><span data-stu-id="d1d19-113">Currently, the only supported authentication types are the `ClientCertificate` model (for using the SSL/TLS client certificates), the `Basic` model (for Basic authentication), and the `ActiveDirectoryOAuth` model (for Active Directory OAuth authentication.)</span></span>

## <a name="request-body-for-clientcertificate-authentication"></a><span data-ttu-id="d1d19-114">İstek gövdesindeki ClientCertificate kimlik doğrulaması için</span><span class="sxs-lookup"><span data-stu-id="d1d19-114">Request Body for ClientCertificate Authentication</span></span>
<span data-ttu-id="d1d19-115">Kimlik doğrulaması kullanarak eklerken `ClientCertificate` model, aşağıdaki ek öğeler istek gövdesinde belirtin.</span><span class="sxs-lookup"><span data-stu-id="d1d19-115">When adding authentication using the `ClientCertificate` model, specify the following additional elements in the request body.</span></span>  

| <span data-ttu-id="d1d19-116">Öğesi</span><span class="sxs-lookup"><span data-stu-id="d1d19-116">Element</span></span> | <span data-ttu-id="d1d19-117">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d1d19-117">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="d1d19-118">*kimlik doğrulaması (üst öğe)*</span><span class="sxs-lookup"><span data-stu-id="d1d19-118">*authentication (parent element)*</span></span> |<span data-ttu-id="d1d19-119">Bir SSL istemci sertifikası kullanmak için kimlik doğrulaması nesne.</span><span class="sxs-lookup"><span data-stu-id="d1d19-119">Authentication object for using an SSL client certificate.</span></span> |
| <span data-ttu-id="d1d19-120">*türü*</span><span class="sxs-lookup"><span data-stu-id="d1d19-120">*type*</span></span> |<span data-ttu-id="d1d19-121">Gerekli.</span><span class="sxs-lookup"><span data-stu-id="d1d19-121">Required.</span></span> <span data-ttu-id="d1d19-122">Kimlik doğrulama türü. SSL istemci sertifikaları için değer olmalıdır `ClientCertificate`.</span><span class="sxs-lookup"><span data-stu-id="d1d19-122">Type of authentication.For SSL client certificates, the value must be `ClientCertificate`.</span></span> |
| <span data-ttu-id="d1d19-123">*PFX*</span><span class="sxs-lookup"><span data-stu-id="d1d19-123">*pfx*</span></span> |<span data-ttu-id="d1d19-124">Gerekli.</span><span class="sxs-lookup"><span data-stu-id="d1d19-124">Required.</span></span> <span data-ttu-id="d1d19-125">PFX dosyasının içeriği Base64 ile kodlanmış.</span><span class="sxs-lookup"><span data-stu-id="d1d19-125">Base64-encoded contents of the PFX file.</span></span> |
| <span data-ttu-id="d1d19-126">*Parola*</span><span class="sxs-lookup"><span data-stu-id="d1d19-126">*password*</span></span> |<span data-ttu-id="d1d19-127">Gerekli.</span><span class="sxs-lookup"><span data-stu-id="d1d19-127">Required.</span></span> <span data-ttu-id="d1d19-128">PFX dosyası erişim için parola.</span><span class="sxs-lookup"><span data-stu-id="d1d19-128">Password to access the PFX file.</span></span> |

## <a name="response-body-for-clientcertificate-authentication"></a><span data-ttu-id="d1d19-129">Yanıt gövdesi ClientCertificate kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="d1d19-129">Response Body for ClientCertificate Authentication</span></span>
<span data-ttu-id="d1d19-130">Kimlik bilgileri ile bir istek gönderildiğinde, yanıt kimlik doğrulaması ile ilgili aşağıdaki öğeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="d1d19-130">When a request is sent with authentication info, the response contains the following authentication-related elements.</span></span>

| <span data-ttu-id="d1d19-131">Öğesi</span><span class="sxs-lookup"><span data-stu-id="d1d19-131">Element</span></span> | <span data-ttu-id="d1d19-132">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d1d19-132">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="d1d19-133">*kimlik doğrulaması (üst öğe)*</span><span class="sxs-lookup"><span data-stu-id="d1d19-133">*authentication (parent element)*</span></span> |<span data-ttu-id="d1d19-134">Bir SSL istemci sertifikası kullanmak için kimlik doğrulaması nesne.</span><span class="sxs-lookup"><span data-stu-id="d1d19-134">Authentication object for using an SSL client certificate.</span></span> |
| <span data-ttu-id="d1d19-135">*türü*</span><span class="sxs-lookup"><span data-stu-id="d1d19-135">*type*</span></span> |<span data-ttu-id="d1d19-136">Kimlik doğrulama türü.</span><span class="sxs-lookup"><span data-stu-id="d1d19-136">Type of authentication.</span></span> <span data-ttu-id="d1d19-137">SSL istemci sertifikaları için değeri olan `ClientCertificate`.</span><span class="sxs-lookup"><span data-stu-id="d1d19-137">For SSL client certificates, the value is `ClientCertificate`.</span></span> |
| <span data-ttu-id="d1d19-138">*certificateThumbprint*</span><span class="sxs-lookup"><span data-stu-id="d1d19-138">*certificateThumbprint*</span></span> |<span data-ttu-id="d1d19-139">Sertifikanın parmak izi.</span><span class="sxs-lookup"><span data-stu-id="d1d19-139">The thumbprint of the certificate.</span></span> |
| <span data-ttu-id="d1d19-140">*certificateSubjectName*</span><span class="sxs-lookup"><span data-stu-id="d1d19-140">*certificateSubjectName*</span></span> |<span data-ttu-id="d1d19-141">Sertifika konu ayırt edici adı.</span><span class="sxs-lookup"><span data-stu-id="d1d19-141">The subject distinguished name of the certificate.</span></span> |
| <span data-ttu-id="d1d19-142">*certificateExpiration*</span><span class="sxs-lookup"><span data-stu-id="d1d19-142">*certificateExpiration*</span></span> |<span data-ttu-id="d1d19-143">Sertifikanın sona erme tarihi.</span><span class="sxs-lookup"><span data-stu-id="d1d19-143">The expiration date of the certificate.</span></span> |

## <a name="sample-rest-request-for-clientcertificate-authentication"></a><span data-ttu-id="d1d19-144">ClientCertificate kimlik doğrulaması için örnek REST istek</span><span class="sxs-lookup"><span data-stu-id="d1d19-144">Sample REST Request for ClientCertificate Authentication</span></span>
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

## <a name="sample-rest-response-for-clientcertificate-authentication"></a><span data-ttu-id="d1d19-145">Örnek REST yanıt ClientCertificate kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="d1d19-145">Sample REST Response for ClientCertificate Authentication</span></span>
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

## <a name="request-body-for-basic-authentication"></a><span data-ttu-id="d1d19-146">Temel kimlik doğrulaması için istek gövdesi</span><span class="sxs-lookup"><span data-stu-id="d1d19-146">Request Body for Basic Authentication</span></span>
<span data-ttu-id="d1d19-147">Kimlik doğrulaması kullanarak eklerken `Basic` model, aşağıdaki ek öğeler istek gövdesinde belirtin.</span><span class="sxs-lookup"><span data-stu-id="d1d19-147">When adding authentication using the `Basic` model, specify the following additional elements in the request body.</span></span>

| <span data-ttu-id="d1d19-148">Öğesi</span><span class="sxs-lookup"><span data-stu-id="d1d19-148">Element</span></span> | <span data-ttu-id="d1d19-149">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d1d19-149">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="d1d19-150">*kimlik doğrulaması (üst öğe)*</span><span class="sxs-lookup"><span data-stu-id="d1d19-150">*authentication (parent element)*</span></span> |<span data-ttu-id="d1d19-151">Temel kimlik doğrulaması kullanmak için kimlik doğrulaması nesne.</span><span class="sxs-lookup"><span data-stu-id="d1d19-151">Authentication object for using Basic authentication.</span></span> |
| <span data-ttu-id="d1d19-152">*türü*</span><span class="sxs-lookup"><span data-stu-id="d1d19-152">*type*</span></span> |<span data-ttu-id="d1d19-153">Gerekli.</span><span class="sxs-lookup"><span data-stu-id="d1d19-153">Required.</span></span> <span data-ttu-id="d1d19-154">Kimlik doğrulama türü.</span><span class="sxs-lookup"><span data-stu-id="d1d19-154">Type of authentication.</span></span> <span data-ttu-id="d1d19-155">Temel kimlik doğrulaması için değer olmalıdır `Basic`.</span><span class="sxs-lookup"><span data-stu-id="d1d19-155">For Basic authentication, the value must be `Basic`.</span></span> |
| <span data-ttu-id="d1d19-156">*Kullanıcı adı*</span><span class="sxs-lookup"><span data-stu-id="d1d19-156">*username*</span></span> |<span data-ttu-id="d1d19-157">Gerekli.</span><span class="sxs-lookup"><span data-stu-id="d1d19-157">Required.</span></span> <span data-ttu-id="d1d19-158">Kimlik doğrulaması için kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="d1d19-158">Username to authenticate.</span></span> |
| <span data-ttu-id="d1d19-159">*Parola*</span><span class="sxs-lookup"><span data-stu-id="d1d19-159">*password*</span></span> |<span data-ttu-id="d1d19-160">Gerekli.</span><span class="sxs-lookup"><span data-stu-id="d1d19-160">Required.</span></span> <span data-ttu-id="d1d19-161">Kimlik doğrulaması için parola.</span><span class="sxs-lookup"><span data-stu-id="d1d19-161">Password to authenticate.</span></span> |

## <a name="response-body-for-basic-authentication"></a><span data-ttu-id="d1d19-162">Temel kimlik doğrulaması için yanıt gövdesi</span><span class="sxs-lookup"><span data-stu-id="d1d19-162">Response Body for Basic Authentication</span></span>
<span data-ttu-id="d1d19-163">Kimlik bilgileri ile bir istek gönderildiğinde, yanıt kimlik doğrulaması ile ilgili aşağıdaki öğeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="d1d19-163">When a request is sent with authentication info, the response contains the following authentication-related elements.</span></span>

| <span data-ttu-id="d1d19-164">Öğesi</span><span class="sxs-lookup"><span data-stu-id="d1d19-164">Element</span></span> | <span data-ttu-id="d1d19-165">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d1d19-165">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="d1d19-166">*kimlik doğrulaması (üst öğe)*</span><span class="sxs-lookup"><span data-stu-id="d1d19-166">*authentication (parent element)*</span></span> |<span data-ttu-id="d1d19-167">Temel kimlik doğrulaması kullanmak için kimlik doğrulaması nesne.</span><span class="sxs-lookup"><span data-stu-id="d1d19-167">Authentication object for using Basic authentication.</span></span> |
| <span data-ttu-id="d1d19-168">*türü*</span><span class="sxs-lookup"><span data-stu-id="d1d19-168">*type*</span></span> |<span data-ttu-id="d1d19-169">Kimlik doğrulama türü.</span><span class="sxs-lookup"><span data-stu-id="d1d19-169">Type of authentication.</span></span> <span data-ttu-id="d1d19-170">Temel kimlik doğrulaması için değerdir `Basic`.</span><span class="sxs-lookup"><span data-stu-id="d1d19-170">For Basic authentication, the value is `Basic`.</span></span> |
| <span data-ttu-id="d1d19-171">*Kullanıcı adı*</span><span class="sxs-lookup"><span data-stu-id="d1d19-171">*username*</span></span> |<span data-ttu-id="d1d19-172">Kimliği doğrulanmış kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="d1d19-172">The authenticated username.</span></span> |

## <a name="sample-rest-request-for-basic-authentication"></a><span data-ttu-id="d1d19-173">Temel kimlik doğrulaması için örnek REST istek</span><span class="sxs-lookup"><span data-stu-id="d1d19-173">Sample REST Request for Basic Authentication</span></span>
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

## <a name="sample-rest-response-for-basic-authentication"></a><span data-ttu-id="d1d19-174">Temel kimlik doğrulaması için örnek REST yanıt</span><span class="sxs-lookup"><span data-stu-id="d1d19-174">Sample REST Response for Basic Authentication</span></span>
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

## <a name="request-body-for-activedirectoryoauth-authentication"></a><span data-ttu-id="d1d19-175">İstek gövdesindeki ActiveDirectoryOAuth kimlik doğrulaması için</span><span class="sxs-lookup"><span data-stu-id="d1d19-175">Request Body for ActiveDirectoryOAuth Authentication</span></span>
<span data-ttu-id="d1d19-176">Kimlik doğrulaması kullanarak eklerken `ActiveDirectoryOAuth` model, aşağıdaki ek öğeler istek gövdesinde belirtin.</span><span class="sxs-lookup"><span data-stu-id="d1d19-176">When adding authentication using the `ActiveDirectoryOAuth` model, specify the following additional elements in the request body.</span></span>

| <span data-ttu-id="d1d19-177">Öğesi</span><span class="sxs-lookup"><span data-stu-id="d1d19-177">Element</span></span> | <span data-ttu-id="d1d19-178">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d1d19-178">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="d1d19-179">*kimlik doğrulaması (üst öğe)*</span><span class="sxs-lookup"><span data-stu-id="d1d19-179">*authentication (parent element)*</span></span> |<span data-ttu-id="d1d19-180">ActiveDirectoryOAuth kimlik doğrulaması kullanmak için kimlik doğrulaması nesne.</span><span class="sxs-lookup"><span data-stu-id="d1d19-180">Authentication object for using ActiveDirectoryOAuth authentication.</span></span> |
| <span data-ttu-id="d1d19-181">*türü*</span><span class="sxs-lookup"><span data-stu-id="d1d19-181">*type*</span></span> |<span data-ttu-id="d1d19-182">Gerekli.</span><span class="sxs-lookup"><span data-stu-id="d1d19-182">Required.</span></span> <span data-ttu-id="d1d19-183">Kimlik doğrulama türü.</span><span class="sxs-lookup"><span data-stu-id="d1d19-183">Type of authentication.</span></span> <span data-ttu-id="d1d19-184">ActiveDirectoryOAuth kimlik doğrulaması için değer olmalıdır `ActiveDirectoryOAuth`.</span><span class="sxs-lookup"><span data-stu-id="d1d19-184">For ActiveDirectoryOAuth authentication, the value must be `ActiveDirectoryOAuth`.</span></span> |
| <span data-ttu-id="d1d19-185">*Kiracı*</span><span class="sxs-lookup"><span data-stu-id="d1d19-185">*tenant*</span></span> |<span data-ttu-id="d1d19-186">Gerekli.</span><span class="sxs-lookup"><span data-stu-id="d1d19-186">Required.</span></span> <span data-ttu-id="d1d19-187">Azure AD kiracısı için Kiracı tanımlayıcı.</span><span class="sxs-lookup"><span data-stu-id="d1d19-187">The tenant identifier for the Azure AD tenant.</span></span> |
| <span data-ttu-id="d1d19-188">*Hedef kitle*</span><span class="sxs-lookup"><span data-stu-id="d1d19-188">*audience*</span></span> |<span data-ttu-id="d1d19-189">Gerekli.</span><span class="sxs-lookup"><span data-stu-id="d1d19-189">Required.</span></span> <span data-ttu-id="d1d19-190">Bu https://management.core.windows.net/ için ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="d1d19-190">This is set to https://management.core.windows.net/.</span></span> |
| <span data-ttu-id="d1d19-191">*istemci kimliği*</span><span class="sxs-lookup"><span data-stu-id="d1d19-191">*clientId*</span></span> |<span data-ttu-id="d1d19-192">Gerekli.</span><span class="sxs-lookup"><span data-stu-id="d1d19-192">Required.</span></span> <span data-ttu-id="d1d19-193">İstemci tanımlayıcısı için Azure AD uygulaması sağlar.</span><span class="sxs-lookup"><span data-stu-id="d1d19-193">Provide the client identifier for the Azure AD application.</span></span> |
| <span data-ttu-id="d1d19-194">*Gizli*</span><span class="sxs-lookup"><span data-stu-id="d1d19-194">*secret*</span></span> |<span data-ttu-id="d1d19-195">Gerekli.</span><span class="sxs-lookup"><span data-stu-id="d1d19-195">Required.</span></span> <span data-ttu-id="d1d19-196">Belirteç isteme istemci gizli anahtarı.</span><span class="sxs-lookup"><span data-stu-id="d1d19-196">Secret of the client that is requesting the token.</span></span> |

### <a name="determining-your-tenant-identifier"></a><span data-ttu-id="d1d19-197">Kiracı Tanımlayıcınız belirleme</span><span class="sxs-lookup"><span data-stu-id="d1d19-197">Determining your Tenant Identifier</span></span>
<span data-ttu-id="d1d19-198">Azure AD kiracısı için Kiracı tanımlayıcı çalıştırarak bulabilirsiniz `Get-AzureAccount` Azure PowerShell'de.</span><span class="sxs-lookup"><span data-stu-id="d1d19-198">You can find the tenant identifier for the Azure AD tenant by running `Get-AzureAccount` in Azure PowerShell.</span></span>

## <a name="response-body-for-activedirectoryoauth-authentication"></a><span data-ttu-id="d1d19-199">Yanıt gövdesi ActiveDirectoryOAuth kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="d1d19-199">Response Body for ActiveDirectoryOAuth Authentication</span></span>
<span data-ttu-id="d1d19-200">Kimlik bilgileri ile bir istek gönderildiğinde, yanıt kimlik doğrulaması ile ilgili aşağıdaki öğeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="d1d19-200">When a request is sent with authentication info, the response contains the following authentication-related elements.</span></span>

| <span data-ttu-id="d1d19-201">Öğesi</span><span class="sxs-lookup"><span data-stu-id="d1d19-201">Element</span></span> | <span data-ttu-id="d1d19-202">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d1d19-202">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="d1d19-203">*kimlik doğrulaması (üst öğe)*</span><span class="sxs-lookup"><span data-stu-id="d1d19-203">*authentication (parent element)*</span></span> |<span data-ttu-id="d1d19-204">ActiveDirectoryOAuth kimlik doğrulaması kullanmak için kimlik doğrulaması nesne.</span><span class="sxs-lookup"><span data-stu-id="d1d19-204">Authentication object for using ActiveDirectoryOAuth authentication.</span></span> |
| <span data-ttu-id="d1d19-205">*türü*</span><span class="sxs-lookup"><span data-stu-id="d1d19-205">*type*</span></span> |<span data-ttu-id="d1d19-206">Kimlik doğrulama türü.</span><span class="sxs-lookup"><span data-stu-id="d1d19-206">Type of authentication.</span></span> <span data-ttu-id="d1d19-207">ActiveDirectoryOAuth kimlik doğrulaması için değerdir `ActiveDirectoryOAuth`.</span><span class="sxs-lookup"><span data-stu-id="d1d19-207">For ActiveDirectoryOAuth authentication, the value is `ActiveDirectoryOAuth`.</span></span> |
| <span data-ttu-id="d1d19-208">*Kiracı*</span><span class="sxs-lookup"><span data-stu-id="d1d19-208">*tenant*</span></span> |<span data-ttu-id="d1d19-209">Azure AD kiracısı için Kiracı tanımlayıcı.</span><span class="sxs-lookup"><span data-stu-id="d1d19-209">The tenant identifier for the Azure AD tenant.</span></span> |
| <span data-ttu-id="d1d19-210">*Hedef kitle*</span><span class="sxs-lookup"><span data-stu-id="d1d19-210">*audience*</span></span> |<span data-ttu-id="d1d19-211">Bu https://management.core.windows.net/ için ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="d1d19-211">This is set to https://management.core.windows.net/.</span></span> |
| <span data-ttu-id="d1d19-212">*istemci kimliği*</span><span class="sxs-lookup"><span data-stu-id="d1d19-212">*clientId*</span></span> |<span data-ttu-id="d1d19-213">Azure AD uygulaması istemci tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="d1d19-213">The client identifier for the Azure AD application.</span></span> |

## <a name="sample-rest-request-for-activedirectoryoauth-authentication"></a><span data-ttu-id="d1d19-214">ActiveDirectoryOAuth kimlik doğrulaması için örnek REST istek</span><span class="sxs-lookup"><span data-stu-id="d1d19-214">Sample REST Request for ActiveDirectoryOAuth Authentication</span></span>
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

## <a name="sample-rest-response-for-activedirectoryoauth-authentication"></a><span data-ttu-id="d1d19-215">Örnek REST yanıt ActiveDirectoryOAuth kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="d1d19-215">Sample REST Response for ActiveDirectoryOAuth Authentication</span></span>
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

## <a name="see-also"></a><span data-ttu-id="d1d19-216">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="d1d19-216">See Also</span></span>
 [<span data-ttu-id="d1d19-217">Scheduler nedir?</span><span class="sxs-lookup"><span data-stu-id="d1d19-217">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="d1d19-218">Azure Scheduler kavramları, terminolojisi ve varlık hiyerarşisi</span><span class="sxs-lookup"><span data-stu-id="d1d19-218">Azure Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="d1d19-219">Azure portalında Scheduler’ı kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="d1d19-219">Get started using Scheduler in the Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="d1d19-220">Azure Scheduler’da planlar ve faturalama</span><span class="sxs-lookup"><span data-stu-id="d1d19-220">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="d1d19-221">Azure Scheduler REST API başvurusu</span><span class="sxs-lookup"><span data-stu-id="d1d19-221">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="d1d19-222">Azure Scheduler PowerShell cmdlet’leri başvurusu</span><span class="sxs-lookup"><span data-stu-id="d1d19-222">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="d1d19-223">Yüksek Azure Scheduler kullanılabilirliği ve güvenilirliği</span><span class="sxs-lookup"><span data-stu-id="d1d19-223">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="d1d19-224">Azure Scheduler sınırları, varsayılanları ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="d1d19-224">Azure Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

