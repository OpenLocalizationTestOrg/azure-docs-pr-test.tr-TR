---
title: "Özel durum işleme & hata günlüğü senaryo - Azure Logic Apps | Microsoft Docs"
description: "Gelişmiş özel durum işleme ve Azure mantıksal uygulamaları için hata günlüğünü hakkında gerçek kullanım örneğini açıklar"
keywords: 
services: logic-apps
author: hedidin
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 63b0b843-f6b0-4d9a-98d0-17500be17385
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 07/29/2016
ms.author: LADocs; b-hoedid
ms.openlocfilehash: 044de27c75da93c95609110d2b73336c42f746fe
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="scenario-exception-handling-and-error-logging-for-logic-apps"></a><span data-ttu-id="b3355-103">Senaryo: Özel durum işleme ve logic apps için hata günlüğü</span><span class="sxs-lookup"><span data-stu-id="b3355-103">Scenario: Exception handling and error logging for logic apps</span></span>

<span data-ttu-id="b3355-104">Bu senaryo, özel durum işleme daha iyi desteklemek için bir mantıksal uygulama nasıl genişletebileceğini açıklar.</span><span class="sxs-lookup"><span data-stu-id="b3355-104">This scenario describes how you can extend a logic app to better support exception handling.</span></span> <span data-ttu-id="b3355-105">Gerçekçi kullanım örneği soruyu yanıtlamak için kullandığımız: "Azure Logic Apps özel durumu ve hata işleme destekliyor mu?"</span><span class="sxs-lookup"><span data-stu-id="b3355-105">We've used a real-life use case to answer the question: "Does Azure Logic Apps support exception and error handling?"</span></span>

> [!NOTE]
> <span data-ttu-id="b3355-106">Geçerli Azure Logic Apps şeması eylem yanıtlar için bir standart şablon sağlar.</span><span class="sxs-lookup"><span data-stu-id="b3355-106">The current Azure Logic Apps schema provides a standard template for action responses.</span></span> <span data-ttu-id="b3355-107">Bu şablon, hem iç doğrulama hem de bir API uygulaması döndürülen hata yanıtları içerir.</span><span class="sxs-lookup"><span data-stu-id="b3355-107">This template includes both internal validation and error responses returned from an API app.</span></span>

## <a name="scenario-and-use-case-overview"></a><span data-ttu-id="b3355-108">Senaryo ve kullanım örneği genel bakış</span><span class="sxs-lookup"><span data-stu-id="b3355-108">Scenario and use case overview</span></span>

<span data-ttu-id="b3355-109">Bu senaryo için kullanım örneği olarak öykü şöyledir:</span><span class="sxs-lookup"><span data-stu-id="b3355-109">Here's the story as the use case for this scenario:</span></span> 

<span data-ttu-id="b3355-110">İyi bilinen bir sağlık kuruluş bize hasta portal Microsoft Dynamics CRM Online kullanarak oluşturacak Azure çözümünü geliştirmek için gerçekleştiriliyor.</span><span class="sxs-lookup"><span data-stu-id="b3355-110">A well-known healthcare organization engaged us to develop an Azure solution that would create a patient portal by using Microsoft Dynamics CRM Online.</span></span> <span data-ttu-id="b3355-111">Dynamics CRM Online hasta portal Salesforce arasındaki randevu kayıtlarını göndermek gerekli.</span><span class="sxs-lookup"><span data-stu-id="b3355-111">They needed to send appointment records between the Dynamics CRM Online patient portal and Salesforce.</span></span> <span data-ttu-id="b3355-112">Biz kullanılacak sorulan [HL7 FHIR](http://www.hl7.org/implement/standards/fhir/) tüm hasta kayıtları için standart.</span><span class="sxs-lookup"><span data-stu-id="b3355-112">We were asked to use the [HL7 FHIR](http://www.hl7.org/implement/standards/fhir/) standard for all patient records.</span></span>

<span data-ttu-id="b3355-113">Proje iki ana gereksinimlerini vardı:</span><span class="sxs-lookup"><span data-stu-id="b3355-113">The project had two major requirements:</span></span>  

* <span data-ttu-id="b3355-114">Dynamics CRM Online portalından gönderilen kayıtlarını günlüğe kaydetmek için bir yöntem</span><span class="sxs-lookup"><span data-stu-id="b3355-114">A method to log records sent from the Dynamics CRM Online portal</span></span>
* <span data-ttu-id="b3355-115">İş akışı içinde oluşan hataları görüntülemek için bir yol</span><span class="sxs-lookup"><span data-stu-id="b3355-115">A way to view any errors that occurred within the workflow</span></span>

> [!TIP]
> <span data-ttu-id="b3355-116">Bu proje hakkında üst düzey video için bkz: [tümleştirme kullanıcı grubu](http://www.integrationusergroup.com/logic-apps-support-error-handling/ "Integration User Group").</span><span class="sxs-lookup"><span data-stu-id="b3355-116">For a high-level video about this project, see [Integration User Group](http://www.integrationusergroup.com/logic-apps-support-error-handling/ "Integration User Group").</span></span>

## <a name="how-we-solved-the-problem"></a><span data-ttu-id="b3355-117">Biz nasıl sorun çözüldü</span><span class="sxs-lookup"><span data-stu-id="b3355-117">How we solved the problem</span></span>

<span data-ttu-id="b3355-118">Seçtik [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/ "Azure Cosmos DB") (Cosmos DB başvurduğu belgeleri olarak kayıtları) günlük ve hata kayıtları için depo olarak.</span><span class="sxs-lookup"><span data-stu-id="b3355-118">We chose [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/ "Azure Cosmos DB") As a repository for the log and error records (Cosmos DB refers to records as documents).</span></span> <span data-ttu-id="b3355-119">Azure Logic Apps tüm yanıtlar için standart bir şablon olduğundan, biz özel şeması oluşturmak sahip.</span><span class="sxs-lookup"><span data-stu-id="b3355-119">Because Azure Logic Apps has a standard template for all responses, we would not have to create a custom schema.</span></span> <span data-ttu-id="b3355-120">Bir API uygulamasına oluşturuyoruz **Ekle** ve **sorgu** hata ve günlük kayıtları için.</span><span class="sxs-lookup"><span data-stu-id="b3355-120">We could create an API app to **Insert** and **Query** for both error and log records.</span></span> <span data-ttu-id="b3355-121">Biz de her API uygulaması içindeki bir şema tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b3355-121">We could also define a schema for each within the API app.</span></span>  

<span data-ttu-id="b3355-122">Belirli bir tarihten sonra kayıtları temizlemek için başka bir gereksinim oluştu.</span><span class="sxs-lookup"><span data-stu-id="b3355-122">Another requirement was to purge records after a certain date.</span></span> <span data-ttu-id="b3355-123">Cosmos DB adlı bir özelliği vardır [yaşam süresi](https://azure.microsoft.com/blog/documentdb-now-supports-time-to-live-ttl/ "yaşam süresi") (TTL) izin bize ayarlamak bir **yaşam süresi** her bir kayıt veya koleksiyon için değer.</span><span class="sxs-lookup"><span data-stu-id="b3355-123">Cosmos DB has a property called [Time to Live](https://azure.microsoft.com/blog/documentdb-now-supports-time-to-live-ttl/ "Time to Live") (TTL), which allowed us to set a **Time to Live** value for each record or collection.</span></span> <span data-ttu-id="b3355-124">Bu özellik Cosmos DB kayıtları el ile silmek için gereken ortadan.</span><span class="sxs-lookup"><span data-stu-id="b3355-124">This capability eliminated the need to manually delete records in Cosmos DB.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b3355-125">Bu öğreticiyi tamamlamak için bir Cosmos DB veritabanı ve iki koleksiyonları (günlüğe kaydetme ve hatalar) oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b3355-125">To complete this tutorial, you need to create a Cosmos DB database and two collections (Logging and Errors).</span></span>

## <a name="create-the-logic-app"></a><span data-ttu-id="b3355-126">Mantıksal uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="b3355-126">Create the logic app</span></span>

<span data-ttu-id="b3355-127">Mantıksal uygulama oluşturma ve uygulama mantığını Uygulama Tasarımcısı'nda açmak için ilk adımdır bakın.</span><span class="sxs-lookup"><span data-stu-id="b3355-127">The first step is to create the logic app and open the app in Logic App Designer.</span></span> <span data-ttu-id="b3355-128">Bu örnekte, üst-alt logic apps kullanıyoruz.</span><span class="sxs-lookup"><span data-stu-id="b3355-128">In this example, we are using parent-child logic apps.</span></span> <span data-ttu-id="b3355-129">Biz üst oluşturmuş ve bir alt mantıksal uygulama oluşturma sunduğu varsayalım.</span><span class="sxs-lookup"><span data-stu-id="b3355-129">Let's assume that we have already created the parent and are going to create one child logic app.</span></span>

<span data-ttu-id="b3355-130">Dynamics CRM Online dışında gelen kayıt oturum kalacaklarını olduğundan, en üstte başlayalım.</span><span class="sxs-lookup"><span data-stu-id="b3355-130">Because we are going to log the record coming out of Dynamics CRM Online, let's start at the top.</span></span> <span data-ttu-id="b3355-131">Biz kullanmalısınız bir **isteği** üst mantıksal uygulama bu alt tetikler çünkü tetikler.</span><span class="sxs-lookup"><span data-stu-id="b3355-131">We must use a **Request** trigger because the parent logic app triggers this child.</span></span>

### <a name="logic-app-trigger"></a><span data-ttu-id="b3355-132">Mantıksal uygulama tetikleyici</span><span class="sxs-lookup"><span data-stu-id="b3355-132">Logic app trigger</span></span>

<span data-ttu-id="b3355-133">Kullanıyoruz bir **isteği** tetiklemek aşağıdaki örnekte gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="b3355-133">We are using a **Request** trigger as shown in the following example:</span></span>

```` json
"triggers": {
        "request": {
          "type": "request",
          "kind": "http",
          "inputs": {
            "schema": {
              "properties": {
                "CRMid": {
                  "type": "string"
                },
                "recordType": {
                  "type": "string"
                },
                "salesforceID": {
                  "type": "string"
                },
                "update": {
                  "type": "boolean"
                }
              },
              "required": [
                "CRMid",
                "recordType",
                "salesforceID",
                "update"
              ],
              "type": "object"
            }
          }
        }
      },

````


## <a name="steps"></a><span data-ttu-id="b3355-134">Adımlar</span><span class="sxs-lookup"><span data-stu-id="b3355-134">Steps</span></span>

<span data-ttu-id="b3355-135">Biz Hasta kayıt kaynağı (istek) Dynamics CRM Online portalı üzerinden oturum açmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b3355-135">We must log the source (request) of the patient record from the Dynamics CRM Online portal.</span></span>

1. <span data-ttu-id="b3355-136">Size yeni bir randevu kayıt Dynamics CRM Online'dan almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b3355-136">We must get a new appointment record from Dynamics CRM Online.</span></span>

   <span data-ttu-id="b3355-137">CRM'den gelen tetikleyici bizimle sağlar **CRM PatentId**, **kayıt türü**, **yeni veya güncelleştirilmiş kayıt** (yeni veya Boolean değeri güncelleştirin), ve  **SalesforceId**.</span><span class="sxs-lookup"><span data-stu-id="b3355-137">The trigger coming from CRM provides us with the **CRM PatentId**, **record type**, **New or Updated Record** (new or update Boolean value), and **SalesforceId**.</span></span> <span data-ttu-id="b3355-138">**SalesforceId** için bir güncelleştirme yalnızca kullanıldığından null olabilir.</span><span class="sxs-lookup"><span data-stu-id="b3355-138">The **SalesforceId** can be null because it's only used for an update.</span></span>
   <span data-ttu-id="b3355-139">Biz CRM kullanarak CRM kaydı alma **PatientID** ve **kayıt türü**.</span><span class="sxs-lookup"><span data-stu-id="b3355-139">We get the CRM record by using the CRM **PatientID** and the **Record Type**.</span></span>

2. <span data-ttu-id="b3355-140">Ardından, bizim DocumentDB API uygulaması eklemek ihtiyacımız **InsertLogEntry** mantığı Uygulama Tasarımcısı'nda aşağıda gösterildiği gibi işlemi.</span><span class="sxs-lookup"><span data-stu-id="b3355-140">Next, we need to add our DocumentDB API app **InsertLogEntry** operation as shown here in Logic App Designer.</span></span>

   <span data-ttu-id="b3355-141">**Günlük Girişi Ekle**</span><span class="sxs-lookup"><span data-stu-id="b3355-141">**Insert log entry**</span></span>

   ![Günlük Girişi Ekle](media/logic-apps-scenario-error-and-exception-handling/lognewpatient.png)

   <span data-ttu-id="b3355-143">**Hata Girişi Ekle**</span><span class="sxs-lookup"><span data-stu-id="b3355-143">**Insert error entry**</span></span>

   ![Günlük Girişi Ekle](media/logic-apps-scenario-error-and-exception-handling/insertlogentry.png)

   <span data-ttu-id="b3355-145">**Onay için kayıt hatası oluşturma**</span><span class="sxs-lookup"><span data-stu-id="b3355-145">**Check for create record failure**</span></span>

   ![Koşul](media/logic-apps-scenario-error-and-exception-handling/condition.png)

## <a name="logic-app-source-code"></a><span data-ttu-id="b3355-147">Mantıksal uygulama kaynak kodu</span><span class="sxs-lookup"><span data-stu-id="b3355-147">Logic app source code</span></span>

> [!NOTE]
> <span data-ttu-id="b3355-148">Aşağıdaki örnekler yalnızca örneklerdir.</span><span class="sxs-lookup"><span data-stu-id="b3355-148">The following examples are samples only.</span></span> <span data-ttu-id="b3355-149">Bu öğreticide uygulama artık üretim, değerini bağlı olduğu bir **kaynak düğüm** bir randevu. zamanlama için ilgili özellikleri görüntülemeyebilir ></span><span class="sxs-lookup"><span data-stu-id="b3355-149">Because this tutorial is based on an implementation now in production, the value of a **Source Node** might not display properties that are related to scheduling an appointment.></span></span> 

### <a name="logging"></a><span data-ttu-id="b3355-150">Günlüğe kaydetme</span><span class="sxs-lookup"><span data-stu-id="b3355-150">Logging</span></span>

<span data-ttu-id="b3355-151">Aşağıdaki mantığı uygulama kod örneği günlüğü nasıl ele alınacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="b3355-151">The following logic app code sample shows how to handle logging.</span></span>

#### <a name="log-entry"></a><span data-ttu-id="b3355-152">Günlük girişi</span><span class="sxs-lookup"><span data-stu-id="b3355-152">Log entry</span></span>

<span data-ttu-id="b3355-153">Aşağıda, bir günlük girdisi eklemek için mantığı uygulama kaynak kodu verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="b3355-153">Here is the logic app source code for inserting a log entry.</span></span>

``` json
"InsertLogEntry": {
        "metadata": {
        "apiDefinitionUrl": "https://.../swagger/docs/v1",
        "swaggerSource": "website"
        },
        "type": "Http",
        "inputs": {
        "body": {
            "date": "@{outputs('Gets_NewPatientRecord')['headers']['Date']}",
            "operation": "New Patient",
            "patientId": "@{triggerBody()['CRMid']}",
            "providerId": "@{triggerBody()['providerID']}",
            "source": "@{outputs('Gets_NewPatientRecord')['headers']}"
        },
        "method": "post",
        "uri": "https://.../api/Log"
        },
        "runAfter":    {
            "Gets_NewPatientecord": ["Succeeded"]
        }
}
```

#### <a name="log-request"></a><span data-ttu-id="b3355-154">Günlük isteği</span><span class="sxs-lookup"><span data-stu-id="b3355-154">Log request</span></span>

<span data-ttu-id="b3355-155">Burada, API uygulamasına gönderilen günlük istek iletisi verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="b3355-155">Here is the log request message posted to the API app.</span></span>

``` json
    {
    "uri": "https://.../api/Log",
    "method": "post",
    "body": {
        "date": "Fri, 10 Jun 2016 22:31:56 GMT",
        "operation": "New Patient",
        "patientId": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "providerId": "",
        "source": "{/"Pragma/":/"no-cache/",/"x-ms-request-id/":/"e750c9a9-bd48-44c4-bbba-1688b6f8a132/",/"OData-Version/":/"4.0/",/"Cache-Control/":/"no-cache/",/"Date/":/"Fri, 10 Jun 2016 22:31:56 GMT/",/"Set-Cookie/":/"ARRAffinity=785f4334b5e64d2db0b84edcc1b84f1bf37319679aefce206b51510e56fd9770;Path=/;Domain=127.0.0.1/",/"Server/":/"Microsoft-IIS/8.0,Microsoft-HTTPAPI/2.0/",/"X-AspNet-Version/":/"4.0.30319/",/"X-Powered-By/":/"ASP.NET/",/"Content-Length/":/"1935/",/"Content-Type/":/"application/json; odata.metadata=minimal; odata.streaming=true/",/"Expires/":/"-1/"}"
        }
    }

```


#### <a name="log-response"></a><span data-ttu-id="b3355-156">Yanıtı Günlüğe Kaydet</span><span class="sxs-lookup"><span data-stu-id="b3355-156">Log response</span></span>

<span data-ttu-id="b3355-157">API uygulaması'ndan günlük yanıt iletisi aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="b3355-157">Here is the log response message from the API app.</span></span>

``` json
{
    "statusCode": 200,
    "headers": {
        "Pragma": "no-cache",
        "Cache-Control": "no-cache",
        "Date": "Fri, 10 Jun 2016 22:32:17 GMT",
        "Server": "Microsoft-IIS/8.0",
        "X-AspNet-Version": "4.0.30319",
        "X-Powered-By": "ASP.NET",
        "Content-Length": "964",
        "Content-Type": "application/json; charset=utf-8",
        "Expires": "-1"
    },
    "body": {
        "ttl": 2592000,
        "id": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0_1465597937",
        "_rid": "XngRAOT6IQEHAAAAAAAAAA==",
        "_self": "dbs/XngRAA==/colls/XngRAOT6IQE=/docs/XngRAOT6IQEHAAAAAAAAAA==/",
        "_ts": 1465597936,
        "_etag": "/"0400fc2f-0000-0000-0000-575b3ff00000/"",
        "patientID": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "timestamp": "2016-06-10T22:31:56Z",
        "source": "{/"Pragma/":/"no-cache/",/"x-ms-request-id/":/"e750c9a9-bd48-44c4-bbba-1688b6f8a132/",/"OData-Version/":/"4.0/",/"Cache-Control/":/"no-cache/",/"Date/":/"Fri, 10 Jun 2016 22:31:56 GMT/",/"Set-Cookie/":/"ARRAffinity=785f4334b5e64d2db0b84edcc1b84f1bf37319679aefce206b51510e56fd9770;Path=/;Domain=127.0.0.1/",/"Server/":/"Microsoft-IIS/8.0,Microsoft-HTTPAPI/2.0/",/"X-AspNet-Version/":/"4.0.30319/",/"X-Powered-By/":/"ASP.NET/",/"Content-Length/":/"1935/",/"Content-Type/":/"application/json; odata.metadata=minimal; odata.streaming=true/",/"Expires/":/"-1/"}",
        "operation": "New Patient",
        "salesforceId": "",
        "expired": false
    }
}

```

<span data-ttu-id="b3355-158">Şimdi adımları işleme hatası bakalım.</span><span class="sxs-lookup"><span data-stu-id="b3355-158">Now let's look at the error handling steps.</span></span>

### <a name="error-handling"></a><span data-ttu-id="b3355-159">Hata işleme</span><span class="sxs-lookup"><span data-stu-id="b3355-159">Error handling</span></span>

<span data-ttu-id="b3355-160">Hata işleme nasıl uygulayacağınıza dair aşağıdaki mantığı uygulama kod örneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="b3355-160">The following logic app code sample shows how you can implement error handling.</span></span>

#### <a name="create-error-record"></a><span data-ttu-id="b3355-161">Hata kaydı oluşturma</span><span class="sxs-lookup"><span data-stu-id="b3355-161">Create error record</span></span>

<span data-ttu-id="b3355-162">Aşağıda, bir hata kaydı oluşturmak için mantığı uygulama kaynak kodu verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="b3355-162">Here is the logic app source code for creating an error record.</span></span>

``` json
"actions": {
    "CreateErrorRecord": {
        "metadata": {
        "apiDefinitionUrl": "https://.../swagger/docs/v1",
        "swaggerSource": "website"
        },
        "type": "Http",
        "inputs": {
        "body": {
            "action": "New_Patient",
            "isError": true,
            "crmId": "@{triggerBody()['CRMid']}",
            "patientID": "@{triggerBody()['CRMid']}",
            "message": "@{body('Create_NewPatientRecord')['message']}",
            "providerId": "@{triggerBody()['providerId']}",
            "severity": 4,
            "source": "@{actions('Create_NewPatientRecord')['inputs']['body']}",
            "statusCode": "@{int(outputs('Create_NewPatientRecord')['statusCode'])}",
            "salesforceId": "",
            "update": false
        },
        "method": "post",
        "uri": "https://.../api/CrMtoSfError"
        },
        "runAfter":
        {
            "Create_NewPatientRecord": ["Failed" ]
        }
    }
}             
```

#### <a name="insert-error-into-cosmos-db--request"></a><span data-ttu-id="b3355-163">Ekleme hatası Cosmos Veritabanına--isteği</span><span class="sxs-lookup"><span data-stu-id="b3355-163">Insert error into Cosmos DB--request</span></span>

``` json

{
    "uri": "https://.../api/CrMtoSfError",
    "method": "post",
    "body": {
        "action": "New_Patient",
        "isError": true,
        "crmId": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "patientId": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "message": "Salesforce failed to complete task: Message: duplicate value found: Account_ID_MED__c duplicates value on record with id: 001U000001c83gK",
        "providerId": "",
        "severity": 4,
        "salesforceId": "",
        "update": false,
        "source": "{/"Account_Class_vod__c/":/"PRAC/",/"Account_Status_MED__c/":/"I/",/"CRM_HUB_ID__c/":/"6b115f6d-a7ee-e511-80f5-3863bb2eb2d0/",/"Credentials_vod__c/",/"DTC_ID_MED__c/":/"/",/"Fax/":/"/",/"FirstName/":/"A/",/"Gender_vod__c/":/"/",/"IMS_ID__c/":/"/",/"LastName/":/"BAILEY/",/"MasterID_mp__c/":/"/",/"C_ID_MED__c/":/"851588/",/"Middle_vod__c/":/"/",/"NPI_vod__c/":/"/",/"PDRP_MED__c/":false,/"PersonDoNotCall/":false,/"PersonEmail/":/"/",/"PersonHasOptedOutOfEmail/":false,/"PersonHasOptedOutOfFax/":false,/"PersonMobilePhone/":/"/",/"Phone/":/"/",/"Practicing_Specialty__c/":/"FM - FAMILY MEDICINE/",/"Primary_City__c/":/"/",/"Primary_State__c/":/"/",/"Primary_Street_Line2__c/":/"/",/"Primary_Street__c/":/"/",/"Primary_Zip__c/":/"/",/"RecordTypeId/":/"012U0000000JaPWIA0/",/"Request_Date__c/":/"2016-06-10T22:31:55.9647467Z/",/"ONY_ID__c/":/"/",/"Specialty_1_vod__c/":/"/",/"Suffix_vod__c/":/"/",/"Website/":/"/"}",
        "statusCode": "400"
    }
}
```

#### <a name="insert-error-into-cosmos-db--response"></a><span data-ttu-id="b3355-164">Cosmos Veritabanına--yanıt ekleme hatası</span><span class="sxs-lookup"><span data-stu-id="b3355-164">Insert error into Cosmos DB--response</span></span>

``` json
{
    "statusCode": 200,
    "headers": {
        "Pragma": "no-cache",
        "Cache-Control": "no-cache",
        "Date": "Fri, 10 Jun 2016 22:31:57 GMT",
        "Server": "Microsoft-IIS/8.0",
        "X-AspNet-Version": "4.0.30319",
        "X-Powered-By": "ASP.NET",
        "Content-Length": "1561",
        "Content-Type": "application/json; charset=utf-8",
        "Expires": "-1"
    },
    "body": {
        "id": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0-1465597917",
        "_rid": "sQx2APhVzAA8AAAAAAAAAA==",
        "_self": "dbs/sQx2AA==/colls/sQx2APhVzAA=/docs/sQx2APhVzAA8AAAAAAAAAA==/",
        "_ts": 1465597912,
        "_etag": "/"0c00eaac-0000-0000-0000-575b3fdc0000/"",
        "prescriberId": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "timestamp": "2016-06-10T22:31:57.3651027Z",
        "action": "New_Patient",
        "salesforceId": "",
        "update": false,
        "body": "CRM failed to complete task: Message: duplicate value found: CRM_HUB_ID__c duplicates value on record with id: 001U000001c83gK",
        "source": "{/"Account_Class_vod__c/":/"PRAC/",/"Account_Status_MED__c/":/"I/",/"CRM_HUB_ID__c/":/"6b115f6d-a7ee-e511-80f5-3863bb2eb2d0/",/"Credentials_vod__c/":/"DO - Degree level is DO/",/"DTC_ID_MED__c/":/"/",/"Fax/":/"/",/"FirstName/":/"A/",/"Gender_vod__c/":/"/",/"IMS_ID__c/":/"/",/"LastName/":/"BAILEY/",/"MterID_mp__c/":/"/",/"Medicis_ID_MED__c/":/"851588/",/"Middle_vod__c/":/"/",/"NPI_vod__c/":/"/",/"PDRP_MED__c/":false,/"PersonDoNotCall/":false,/"PersonEmail/":/"/",/"PersonHasOptedOutOfEmail/":false,/"PersonHasOptedOutOfFax/":false,/"PersonMobilePhone/":/"/",/"Phone/":/"/",/"Practicing_Specialty__c/":/"FM - FAMILY MEDICINE/",/"Primary_City__c/":/"/",/"Primary_State__c/":/"/",/"Primary_Street_Line2__c/":/"/",/"Primary_Street__c/":/"/",/"Primary_Zip__c/":/"/",/"RecordTypeId/":/"012U0000000JaPWIA0/",/"Request_Date__c/":/"2016-06-10T22:31:55.9647467Z/",/"XXXXXXX/":/"/",/"Specialty_1_vod__c/":/"/",/"Suffix_vod__c/":/"/",/"Website/":/"/"}",
        "code": 400,
        "errors": null,
        "isError": true,
        "severity": 4,
        "notes": null,
        "resolved": 0
        }
}
```

#### <a name="salesforce-error-response"></a><span data-ttu-id="b3355-165">Salesforce hata yanıtı</span><span class="sxs-lookup"><span data-stu-id="b3355-165">Salesforce error response</span></span>

``` json
{
    "statusCode": 400,
    "headers": {
        "Pragma": "no-cache",
        "x-ms-request-id": "3e8e4884-288e-4633-972c-8271b2cc912c",
        "X-Content-Type-Options": "nosniff",
        "Cache-Control": "no-cache",
        "Date": "Fri, 10 Jun 2016 22:31:56 GMT",
        "Set-Cookie": "ARRAffinity=785f4334b5e64d2db0b84edcc1b84f1bf37319679aefce206b51510e56fd9770;Path=/;Domain=127.0.0.1",
        "Server": "Microsoft-IIS/8.0,Microsoft-HTTPAPI/2.0",
        "X-AspNet-Version": "4.0.30319",
        "X-Powered-By": "ASP.NET",
        "Content-Length": "205",
        "Content-Type": "application/json; charset=utf-8",
        "Expires": "-1"
    },
    "body": {
        "status": 400,
        "message": "Salesforce failed to complete task: Message: duplicate value found: Account_ID_MED__c duplicates value on record with id: 001U000001c83gK",
        "source": "Salesforce.Common",
        "errors": []
    }
}

```

### <a name="return-the-response-back-to-parent-logic-app"></a><span data-ttu-id="b3355-166">Üst mantıksal uygulama yanıta geri dönün</span><span class="sxs-lookup"><span data-stu-id="b3355-166">Return the response back to parent logic app</span></span>

<span data-ttu-id="b3355-167">Yanıt aldıktan sonra yanıt üst mantıksal uygulama geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b3355-167">After you get the response, you can pass the response back to the parent logic app.</span></span>

#### <a name="return-success-response-to-parent-logic-app"></a><span data-ttu-id="b3355-168">Başarılı yanıt üst mantığı uygulamaya döndürür</span><span class="sxs-lookup"><span data-stu-id="b3355-168">Return success response to parent logic app</span></span>

``` json
"SuccessResponse": {
    "runAfter":
        {
            "UpdateNew_CRMPatientResponse": ["Succeeded"]
        },
    "inputs": {
        "body": {
            "status": "Success"
    },
    "headers": {
    "    Content-type": "application/json",
        "x-ms-date": "@utcnow()"
    },
    "statusCode": 200
    },
    "type": "Response"
}
```

#### <a name="return-error-response-to-parent-logic-app"></a><span data-ttu-id="b3355-169">Üst mantıksal uygulama hata yanıtı döndürür</span><span class="sxs-lookup"><span data-stu-id="b3355-169">Return error response to parent logic app</span></span>

``` json
"ErrorResponse": {
    "runAfter":
        {
            "Create_NewPatientRecord": ["Failed"]
        },
    "inputs": {
        "body": {
            "status": "BadRequest"
        },
        "headers": {
            "Content-type": "application/json",
            "x-ms-date": "@utcnow()"
        },
        "statusCode": 400
    },
    "type": "Response"
}

```


## <a name="cosmos-db-repository-and-portal"></a><span data-ttu-id="b3355-170">Cosmos DB depo ve portal</span><span class="sxs-lookup"><span data-stu-id="b3355-170">Cosmos DB repository and portal</span></span>

<span data-ttu-id="b3355-171">Çözümümüzdür eklenen özellikleriyle [Cosmos DB](https://azure.microsoft.com/services/documentdb).</span><span class="sxs-lookup"><span data-stu-id="b3355-171">Our solution added capabilities with [Cosmos DB](https://azure.microsoft.com/services/documentdb).</span></span>

### <a name="error-management-portal"></a><span data-ttu-id="b3355-172">Hata Yönetim Portalı</span><span class="sxs-lookup"><span data-stu-id="b3355-172">Error management portal</span></span>

<span data-ttu-id="b3355-173">Hataları görüntülemek için Cosmos DB'den hata kayıtları görüntülemek için bir MVC web uygulaması oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b3355-173">To view the errors, you can create an MVC web app to display the error records from Cosmos DB.</span></span> <span data-ttu-id="b3355-174">**Listesi**, **ayrıntıları**, **Düzenle**, ve **silmek** işlemleri geçerli sürümde dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="b3355-174">The **List**, **Details**, **Edit**, and **Delete** operations are included in the current version.</span></span>

> [!NOTE]
> <span data-ttu-id="b3355-175">İşlem düzenleme: Cosmos DB tüm belgeyi yerini alır.</span><span class="sxs-lookup"><span data-stu-id="b3355-175">Edit operation: Cosmos DB replaces the entire document.</span></span> <span data-ttu-id="b3355-176">Gösterilen kayıtları **listesi** ve **ayrıntı** örnekleri yalnızca görünümlerdir.</span><span class="sxs-lookup"><span data-stu-id="b3355-176">The records shown in the **List** and **Detail** views are samples only.</span></span> <span data-ttu-id="b3355-177">Bunlar gerçek hasta randevu kayıtlarını olup olmadığı.</span><span class="sxs-lookup"><span data-stu-id="b3355-177">They are not actual patient appointment records.</span></span>

<span data-ttu-id="b3355-178">Daha önce açıklanan yaklaşımda oluşturulan bizim MVC uygulama ayrıntıları örnekleri aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="b3355-178">Here are examples of our MVC app details created with the previously described approach.</span></span>

#### <a name="error-management-list"></a><span data-ttu-id="b3355-179">Hata yönetim listesi</span><span class="sxs-lookup"><span data-stu-id="b3355-179">Error management list</span></span>
![Hata listesi](media/logic-apps-scenario-error-and-exception-handling/errorlist.png)

#### <a name="error-management-detail-view"></a><span data-ttu-id="b3355-181">Hata yönetim ayrıntılı Görünüm</span><span class="sxs-lookup"><span data-stu-id="b3355-181">Error management detail view</span></span>
![Hata Ayrıntıları](media/logic-apps-scenario-error-and-exception-handling/errordetails.png)

### <a name="log-management-portal"></a><span data-ttu-id="b3355-183">Günlük Yönetim Portalı</span><span class="sxs-lookup"><span data-stu-id="b3355-183">Log management portal</span></span>

<span data-ttu-id="b3355-184">Günlükleri görüntülemek için de bir MVC web uygulaması oluşturduk.</span><span class="sxs-lookup"><span data-stu-id="b3355-184">To view the logs, we also created an MVC web app.</span></span> <span data-ttu-id="b3355-185">Daha önce açıklanan yaklaşımda oluşturulan bizim MVC uygulama ayrıntıları örnekleri aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="b3355-185">Here are examples of our MVC app details created with the previously described approach.</span></span>

#### <a name="sample-log-detail-view"></a><span data-ttu-id="b3355-186">Örnek günlük ayrıntılı Görünüm</span><span class="sxs-lookup"><span data-stu-id="b3355-186">Sample log detail view</span></span>
![Günlük ayrıntılı Görünüm](media/logic-apps-scenario-error-and-exception-handling/samplelogdetail.png)

### <a name="api-app-details"></a><span data-ttu-id="b3355-188">API uygulama ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="b3355-188">API app details</span></span>

#### <a name="logic-apps-exception-management-api"></a><span data-ttu-id="b3355-189">Logic Apps özel durum yönetimi API</span><span class="sxs-lookup"><span data-stu-id="b3355-189">Logic Apps exception management API</span></span>

<span data-ttu-id="b3355-190">Burada açıklandığı gibi açık kaynaklı Azure Logic Apps özel durum yönetimi API'si uygulamamıza işlevsellik sağlar - iki denetleyicisi vardır:</span><span class="sxs-lookup"><span data-stu-id="b3355-190">Our open-source Azure Logic Apps exception management API app provides functionality as described here - there are two controllers:</span></span>

* <span data-ttu-id="b3355-191">**ErrorController** bir DocumentDB koleksiyonu içinde bir hata kaydı (belge) ekler.</span><span class="sxs-lookup"><span data-stu-id="b3355-191">**ErrorController** inserts an error record (document) in a DocumentDB collection.</span></span>
* <span data-ttu-id="b3355-192">**LogController** bir DocumentDB koleksiyonu içinde bir günlük kaydı (belge) ekler.</span><span class="sxs-lookup"><span data-stu-id="b3355-192">**LogController** Inserts a log record (document) in a DocumentDB collection.</span></span>

> [!TIP]
> <span data-ttu-id="b3355-193">Her iki denetleyicilerinin kullandığı `async Task<dynamic>` işlemleri, DocumentDB şema işlemi gövdesinde oluşturabilmesi için çalışma zamanında çözümlemek işlem yapılmasına olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="b3355-193">Both controllers use `async Task<dynamic>` operations, allowing operations to resolve at runtime, so we can create the DocumentDB schema in the body of the operation.</span></span> 
> 

<span data-ttu-id="b3355-194">Her DocumentDB belgede benzersiz bir kimliği olmalıdır</span><span class="sxs-lookup"><span data-stu-id="b3355-194">Every document in DocumentDB must have a unique ID.</span></span> <span data-ttu-id="b3355-195">Kullanıyoruz `PatientId` ve bir UNIX zaman damgası değerine (double) dönüştürülen bir zaman damgası ekleme.</span><span class="sxs-lookup"><span data-stu-id="b3355-195">We are using `PatientId` and adding a timestamp that is converted to a Unix timestamp value (double).</span></span> <span data-ttu-id="b3355-196">Kesir değerini kaldırmak için değer olacak şekilde kısaltın.</span><span class="sxs-lookup"><span data-stu-id="b3355-196">We truncate the value to remove the fractional value.</span></span>

<span data-ttu-id="b3355-197">Bizim hata denetleyicisinin API kaynak kodu görüntüleyebilirsiniz [github'dan](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi/blob/master/Logic App Exception Management API/Controllers/ErrorController.cs).</span><span class="sxs-lookup"><span data-stu-id="b3355-197">You can view the source code of our error controller API [from GitHub](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi/blob/master/Logic App Exception Management API/Controllers/ErrorController.cs).</span></span>

<span data-ttu-id="b3355-198">API mantığı uygulamadan aşağıdaki sözdizimini kullanarak diyoruz:</span><span class="sxs-lookup"><span data-stu-id="b3355-198">We call the API from a logic app by using the following syntax:</span></span>

``` json
 "actions": {
        "CreateErrorRecord": {
          "metadata": {
            "apiDefinitionUrl": "https://.../swagger/docs/v1",
            "swaggerSource": "website"
          },
          "type": "Http",
          "inputs": {
            "body": {
              "action": "New_Patient",
              "isError": true,
              "crmId": "@{triggerBody()['CRMid']}",
              "prescriberId": "@{triggerBody()['CRMid']}",
              "message": "@{body('Create_NewPatientRecord')['message']}",
              "salesforceId": "@{triggerBody()['salesforceID']}",
              "severity": 4,
              "source": "@{actions('Create_NewPatientRecord')['inputs']['body']}",
              "statusCode": "@{int(outputs('Create_NewPatientRecord')['statusCode'])}",
              "update": false
            },
            "method": "post",
            "uri": "https://.../api/CrMtoSfError"
          },
          "runAfter": {
              "Create_NewPatientRecord": ["Failed"]
            }
        }
 }
```

<span data-ttu-id="b3355-199">Önceki kod örneğinde ifadesi kontrol *Create_NewPatientRecord* durumunu **başarısız**.</span><span class="sxs-lookup"><span data-stu-id="b3355-199">The expression in the preceding code sample checks for the *Create_NewPatientRecord* status of **Failed**.</span></span>

## <a name="summary"></a><span data-ttu-id="b3355-200">Özet</span><span class="sxs-lookup"><span data-stu-id="b3355-200">Summary</span></span>

* <span data-ttu-id="b3355-201">Günlüğe kaydetme ve hata işleme bir mantıksal uygulama kolayca uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b3355-201">You can easily implement logging and error handling in a logic app.</span></span>
* <span data-ttu-id="b3355-202">DocumentDB günlük ve hata kayıtları (belgeler) deposu olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b3355-202">You can use DocumentDB as the repository for log and error records (documents).</span></span>
* <span data-ttu-id="b3355-203">MVC, günlük ve hata kayıtları görüntülemek için portalı oluşturmak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b3355-203">You can use MVC to create a portal to display log and error records.</span></span>

### <a name="source-code"></a><span data-ttu-id="b3355-204">Kaynak kod</span><span class="sxs-lookup"><span data-stu-id="b3355-204">Source code</span></span>

<span data-ttu-id="b3355-205">Logic Apps özel durum yönetimi API uygulaması için kaynak kodunu bu kullanılabilir [GitHub deposunu](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi "mantığı uygulama özel durum yönetimi API").</span><span class="sxs-lookup"><span data-stu-id="b3355-205">The source code for the Logic Apps exception management API application is available in this [GitHub repository](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi "Logic App Exception Management API").</span></span>

## <a name="next-steps"></a><span data-ttu-id="b3355-206">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b3355-206">Next steps</span></span>

* [<span data-ttu-id="b3355-207">Daha fazla mantıksal uygulama örnekleri ve senaryoları görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="b3355-207">View more logic app examples and scenarios</span></span>](../logic-apps/logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="b3355-208">Mantıksal uygulamaları izleme hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="b3355-208">Learn about monitoring logic apps</span></span>](../logic-apps/logic-apps-monitor-your-logic-apps.md)
* [<span data-ttu-id="b3355-209">Mantıksal uygulamalar için otomatik dağıtım şablonlar oluşturma</span><span class="sxs-lookup"><span data-stu-id="b3355-209">Create automated deployment templates for logic apps</span></span>](../logic-apps/logic-apps-create-deploy-template.md)
