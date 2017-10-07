---
title: "aaaException işleme ve hata günlüğü senaryo - Azure Logic Apps | Microsoft Docs"
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
ms.openlocfilehash: e893a7b652254dca7b8a82398e8afd571f6ccd25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="scenario-exception-handling-and-error-logging-for-logic-apps"></a><span data-ttu-id="413f5-103">Senaryo: Özel durum işleme ve logic apps için hata günlüğü</span><span class="sxs-lookup"><span data-stu-id="413f5-103">Scenario: Exception handling and error logging for logic apps</span></span>

<span data-ttu-id="413f5-104">Bu senaryo, bir mantıksal uygulama toobetter destek özel durum işleme nasıl genişletebileceğini açıklar.</span><span class="sxs-lookup"><span data-stu-id="413f5-104">This scenario describes how you can extend a logic app toobetter support exception handling.</span></span> <span data-ttu-id="413f5-105">Gerçekçi kullanım örneği tooanswer hello soru kullandığımız: "Azure Logic Apps özel durumu ve hata işleme destekliyor mu?"</span><span class="sxs-lookup"><span data-stu-id="413f5-105">We've used a real-life use case tooanswer hello question: "Does Azure Logic Apps support exception and error handling?"</span></span>

> [!NOTE]
> <span data-ttu-id="413f5-106">Merhaba geçerli Azure Logic Apps şeması eylem yanıtlar için bir standart şablon sağlar.</span><span class="sxs-lookup"><span data-stu-id="413f5-106">hello current Azure Logic Apps schema provides a standard template for action responses.</span></span> <span data-ttu-id="413f5-107">Bu şablon, hem iç doğrulama hem de bir API uygulaması döndürülen hata yanıtları içerir.</span><span class="sxs-lookup"><span data-stu-id="413f5-107">This template includes both internal validation and error responses returned from an API app.</span></span>

## <a name="scenario-and-use-case-overview"></a><span data-ttu-id="413f5-108">Senaryo ve kullanım örneği genel bakış</span><span class="sxs-lookup"><span data-stu-id="413f5-108">Scenario and use case overview</span></span>

<span data-ttu-id="413f5-109">Bu senaryo için hello kullanım örneği olarak hello Öykü şöyledir:</span><span class="sxs-lookup"><span data-stu-id="413f5-109">Here's hello story as hello use case for this scenario:</span></span> 

<span data-ttu-id="413f5-110">İyi bilinen bir sağlık kuruluş bize toodevelop hasta portal Microsoft Dynamics CRM Online kullanarak oluşturacak Azure çözümünü gerçekleştiriliyor.</span><span class="sxs-lookup"><span data-stu-id="413f5-110">A well-known healthcare organization engaged us toodevelop an Azure solution that would create a patient portal by using Microsoft Dynamics CRM Online.</span></span> <span data-ttu-id="413f5-111">Bunlar toosend randevu kayıtlarını hello Dynamics CRM Online hasta portal Salesforce arasındaki gerekli.</span><span class="sxs-lookup"><span data-stu-id="413f5-111">They needed toosend appointment records between hello Dynamics CRM Online patient portal and Salesforce.</span></span> <span data-ttu-id="413f5-112">Toouse hello sorulan [HL7 FHIR](http://www.hl7.org/implement/standards/fhir/) tüm hasta kayıtları için standart.</span><span class="sxs-lookup"><span data-stu-id="413f5-112">We were asked toouse hello [HL7 FHIR](http://www.hl7.org/implement/standards/fhir/) standard for all patient records.</span></span>

<span data-ttu-id="413f5-113">Merhaba proje iki ana gereksinimlerini vardı:</span><span class="sxs-lookup"><span data-stu-id="413f5-113">hello project had two major requirements:</span></span>  

* <span data-ttu-id="413f5-114">Dynamics CRM Online portalı hello yöntemi toolog kayıtları gönderilen</span><span class="sxs-lookup"><span data-stu-id="413f5-114">A method toolog records sent from hello Dynamics CRM Online portal</span></span>
* <span data-ttu-id="413f5-115">Bir şekilde tooview hello iş akışı içinde oluşan hatalar</span><span class="sxs-lookup"><span data-stu-id="413f5-115">A way tooview any errors that occurred within hello workflow</span></span>

> [!TIP]
> <span data-ttu-id="413f5-116">Bu proje hakkında üst düzey video için bkz: [tümleştirme kullanıcı grubu](http://www.integrationusergroup.com/logic-apps-support-error-handling/ "tümleştirme kullanıcı grubu").</span><span class="sxs-lookup"><span data-stu-id="413f5-116">For a high-level video about this project, see [Integration User Group](http://www.integrationusergroup.com/logic-apps-support-error-handling/ "Integration User Group").</span></span>

## <a name="how-we-solved-hello-problem"></a><span data-ttu-id="413f5-117">Nasıl biz hello sorun çözüldü</span><span class="sxs-lookup"><span data-stu-id="413f5-117">How we solved hello problem</span></span>

<span data-ttu-id="413f5-118">Seçtik [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/ "Azure Cosmos DB") (Cosmos DB başvuruyor belgeleri olarak toorecords) hello günlük ve hata kayıtları için depo olarak.</span><span class="sxs-lookup"><span data-stu-id="413f5-118">We chose [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/ "Azure Cosmos DB") As a repository for hello log and error records (Cosmos DB refers toorecords as documents).</span></span> <span data-ttu-id="413f5-119">Azure Logic Apps tüm yanıtlar için standart bir şablon olduğundan, biz toocreate özel şeması sahip olmaz.</span><span class="sxs-lookup"><span data-stu-id="413f5-119">Because Azure Logic Apps has a standard template for all responses, we would not have toocreate a custom schema.</span></span> <span data-ttu-id="413f5-120">API uygulaması çok oluşturma**Ekle** ve **sorgu** hata ve günlük kayıtları için.</span><span class="sxs-lookup"><span data-stu-id="413f5-120">We could create an API app too**Insert** and **Query** for both error and log records.</span></span> <span data-ttu-id="413f5-121">Biz de her hello API uygulaması içindeki bir şema tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="413f5-121">We could also define a schema for each within hello API app.</span></span>  

<span data-ttu-id="413f5-122">Başka bir gereksinim toopurge kayıtları belirli bir tarihten sonra oluştu.</span><span class="sxs-lookup"><span data-stu-id="413f5-122">Another requirement was toopurge records after a certain date.</span></span> <span data-ttu-id="413f5-123">Cosmos DB adlı bir özelliği vardır [zaman tooLive](https://azure.microsoft.com/blog/documentdb-now-supports-time-to-live-ttl/ "zaman tooLive") (TTL) izin bize tooset bir **zaman tooLive** her bir kayıt veya koleksiyon için değer.</span><span class="sxs-lookup"><span data-stu-id="413f5-123">Cosmos DB has a property called [Time tooLive](https://azure.microsoft.com/blog/documentdb-now-supports-time-to-live-ttl/ "Time tooLive") (TTL), which allowed us tooset a **Time tooLive** value for each record or collection.</span></span> <span data-ttu-id="413f5-124">Bu özellik hello gerek toomanually Cosmos DB'de kayıt silme ortadan.</span><span class="sxs-lookup"><span data-stu-id="413f5-124">This capability eliminated hello need toomanually delete records in Cosmos DB.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="413f5-125">toocomplete Bu öğretici, toocreate Cosmos DB veritabanı ve iki koleksiyonları (günlüğe kaydetme ve hatalar) gerekir.</span><span class="sxs-lookup"><span data-stu-id="413f5-125">toocomplete this tutorial, you need toocreate a Cosmos DB database and two collections (Logging and Errors).</span></span>

## <a name="create-hello-logic-app"></a><span data-ttu-id="413f5-126">Merhaba mantıksal uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="413f5-126">Create hello logic app</span></span>

<span data-ttu-id="413f5-127">Merhaba ilk toocreate hello mantıksal uygulama ve açık hello uygulama mantığını Uygulama Tasarımcısı'nda adımdır.</span><span class="sxs-lookup"><span data-stu-id="413f5-127">hello first step is toocreate hello logic app and open hello app in Logic App Designer.</span></span> <span data-ttu-id="413f5-128">Bu örnekte, üst-alt logic apps kullanıyoruz.</span><span class="sxs-lookup"><span data-stu-id="413f5-128">In this example, we are using parent-child logic apps.</span></span> <span data-ttu-id="413f5-129">Biz hello üst oluşturmuş ve toocreate bir alt mantıksal uygulama giderek varsayalım.</span><span class="sxs-lookup"><span data-stu-id="413f5-129">Let's assume that we have already created hello parent and are going toocreate one child logic app.</span></span>

<span data-ttu-id="413f5-130">Dynamics CRM Online dışında gelen toolog hello kayıt olmaz çünkü hello üstünde başlayalım.</span><span class="sxs-lookup"><span data-stu-id="413f5-130">Because we are going toolog hello record coming out of Dynamics CRM Online, let's start at hello top.</span></span> <span data-ttu-id="413f5-131">Biz kullanmanız gerekir bir **isteği** hello üst mantıksal uygulama bu alt tetikler çünkü tetikler.</span><span class="sxs-lookup"><span data-stu-id="413f5-131">We must use a **Request** trigger because hello parent logic app triggers this child.</span></span>

### <a name="logic-app-trigger"></a><span data-ttu-id="413f5-132">Mantıksal uygulama tetikleyici</span><span class="sxs-lookup"><span data-stu-id="413f5-132">Logic app trigger</span></span>

<span data-ttu-id="413f5-133">Kullanıyoruz bir **isteği** tetiklemek hello aşağıdaki örnekte gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="413f5-133">We are using a **Request** trigger as shown in hello following example:</span></span>

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


## <a name="steps"></a><span data-ttu-id="413f5-134">Adımlar</span><span class="sxs-lookup"><span data-stu-id="413f5-134">Steps</span></span>

<span data-ttu-id="413f5-135">Biz hello hasta kaydının hello kaynak (istek) hello Dynamics CRM Online portalından oturum açmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="413f5-135">We must log hello source (request) of hello patient record from hello Dynamics CRM Online portal.</span></span>

1. <span data-ttu-id="413f5-136">Size yeni bir randevu kayıt Dynamics CRM Online'dan almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="413f5-136">We must get a new appointment record from Dynamics CRM Online.</span></span>

   <span data-ttu-id="413f5-137">Merhaba tetikleyici CRM'den gelen sağlar bize ile Merhaba **CRM PatentId**, **kayıt türü**, **yeni veya güncelleştirilmiş kayıt** (yeni veya Boolean değeri güncelleştirin), ve  **SalesforceId**.</span><span class="sxs-lookup"><span data-stu-id="413f5-137">hello trigger coming from CRM provides us with hello **CRM PatentId**, **record type**, **New or Updated Record** (new or update Boolean value), and **SalesforceId**.</span></span> <span data-ttu-id="413f5-138">Merhaba **SalesforceId** için bir güncelleştirme yalnızca kullanıldığından null olabilir.</span><span class="sxs-lookup"><span data-stu-id="413f5-138">hello **SalesforceId** can be null because it's only used for an update.</span></span>
   <span data-ttu-id="413f5-139">Biz hello CRM kullanarak hello CRM kaydı alma **PatientID** ve hello **kayıt türü**.</span><span class="sxs-lookup"><span data-stu-id="413f5-139">We get hello CRM record by using hello CRM **PatientID** and hello **Record Type**.</span></span>

2. <span data-ttu-id="413f5-140">Tooadd bizim DocumentDB API uygulaması daha ihtiyacımız **InsertLogEntry** mantığı Uygulama Tasarımcısı'nda aşağıda gösterildiği gibi işlemi.</span><span class="sxs-lookup"><span data-stu-id="413f5-140">Next, we need tooadd our DocumentDB API app **InsertLogEntry** operation as shown here in Logic App Designer.</span></span>

   <span data-ttu-id="413f5-141">**Günlük Girişi Ekle**</span><span class="sxs-lookup"><span data-stu-id="413f5-141">**Insert log entry**</span></span>

   ![Günlük Girişi Ekle](media/logic-apps-scenario-error-and-exception-handling/lognewpatient.png)

   <span data-ttu-id="413f5-143">**Hata Girişi Ekle**</span><span class="sxs-lookup"><span data-stu-id="413f5-143">**Insert error entry**</span></span>

   ![Günlük Girişi Ekle](media/logic-apps-scenario-error-and-exception-handling/insertlogentry.png)

   <span data-ttu-id="413f5-145">**Onay için kayıt hatası oluşturma**</span><span class="sxs-lookup"><span data-stu-id="413f5-145">**Check for create record failure**</span></span>

   ![Koşul](media/logic-apps-scenario-error-and-exception-handling/condition.png)

## <a name="logic-app-source-code"></a><span data-ttu-id="413f5-147">Mantıksal uygulama kaynak kodu</span><span class="sxs-lookup"><span data-stu-id="413f5-147">Logic app source code</span></span>

> [!NOTE]
> <span data-ttu-id="413f5-148">Örnek hello yalnızca örneklerdir.</span><span class="sxs-lookup"><span data-stu-id="413f5-148">hello following examples are samples only.</span></span> <span data-ttu-id="413f5-149">Bu öğretici, uygulama artık üretim dayalı olduğundan değerini hello bir **kaynak düğüm** ilgili tooscheduling bir randevu. özellikler görüntülemeyebilir ></span><span class="sxs-lookup"><span data-stu-id="413f5-149">Because this tutorial is based on an implementation now in production, hello value of a **Source Node** might not display properties that are related tooscheduling an appointment.></span></span> 

### <a name="logging"></a><span data-ttu-id="413f5-150">Günlüğe kaydetme</span><span class="sxs-lookup"><span data-stu-id="413f5-150">Logging</span></span>

<span data-ttu-id="413f5-151">mantıksal uygulama kodu aşağıdaki hello örnek gösterir nasıl toohandle günlüğe kaydetme.</span><span class="sxs-lookup"><span data-stu-id="413f5-151">hello following logic app code sample shows how toohandle logging.</span></span>

#### <a name="log-entry"></a><span data-ttu-id="413f5-152">Günlük girişi</span><span class="sxs-lookup"><span data-stu-id="413f5-152">Log entry</span></span>

<span data-ttu-id="413f5-153">Burada, bir günlük girişi ekleme hello mantığı uygulama kaynak kodu verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="413f5-153">Here is hello logic app source code for inserting a log entry.</span></span>

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

#### <a name="log-request"></a><span data-ttu-id="413f5-154">Günlük isteği</span><span class="sxs-lookup"><span data-stu-id="413f5-154">Log request</span></span>

<span data-ttu-id="413f5-155">Merhaba günlük istek iletisi toohello API uygulaması gönderilen aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="413f5-155">Here is hello log request message posted toohello API app.</span></span>

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


#### <a name="log-response"></a><span data-ttu-id="413f5-156">Yanıtı Günlüğe Kaydet</span><span class="sxs-lookup"><span data-stu-id="413f5-156">Log response</span></span>

<span data-ttu-id="413f5-157">Merhaba günlük yanıt iletisi hello API uygulaması'ndan aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="413f5-157">Here is hello log response message from hello API app.</span></span>

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

<span data-ttu-id="413f5-158">Şimdi adımları işleme hello hatasında bakalım.</span><span class="sxs-lookup"><span data-stu-id="413f5-158">Now let's look at hello error handling steps.</span></span>

### <a name="error-handling"></a><span data-ttu-id="413f5-159">Hata işleme</span><span class="sxs-lookup"><span data-stu-id="413f5-159">Error handling</span></span>

<span data-ttu-id="413f5-160">Hello aşağıdaki mantığı uygulama kod örneği, hata işleme nasıl uygulayabileceğiniz gösterir.</span><span class="sxs-lookup"><span data-stu-id="413f5-160">hello following logic app code sample shows how you can implement error handling.</span></span>

#### <a name="create-error-record"></a><span data-ttu-id="413f5-161">Hata kaydı oluşturma</span><span class="sxs-lookup"><span data-stu-id="413f5-161">Create error record</span></span>

<span data-ttu-id="413f5-162">Burada, bir hata kaydı oluşturmak için hello mantığı uygulama kaynak kodu verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="413f5-162">Here is hello logic app source code for creating an error record.</span></span>

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

#### <a name="insert-error-into-cosmos-db--request"></a><span data-ttu-id="413f5-163">Ekleme hatası Cosmos Veritabanına--isteği</span><span class="sxs-lookup"><span data-stu-id="413f5-163">Insert error into Cosmos DB--request</span></span>

``` json

{
    "uri": "https://.../api/CrMtoSfError",
    "method": "post",
    "body": {
        "action": "New_Patient",
        "isError": true,
        "crmId": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "patientId": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "message": "Salesforce failed toocomplete task: Message: duplicate value found: Account_ID_MED__c duplicates value on record with id: 001U000001c83gK",
        "providerId": "",
        "severity": 4,
        "salesforceId": "",
        "update": false,
        "source": "{/"Account_Class_vod__c/":/"PRAC/",/"Account_Status_MED__c/":/"I/",/"CRM_HUB_ID__c/":/"6b115f6d-a7ee-e511-80f5-3863bb2eb2d0/",/"Credentials_vod__c/",/"DTC_ID_MED__c/":/"/",/"Fax/":/"/",/"FirstName/":/"A/",/"Gender_vod__c/":/"/",/"IMS_ID__c/":/"/",/"LastName/":/"BAILEY/",/"MasterID_mp__c/":/"/",/"C_ID_MED__c/":/"851588/",/"Middle_vod__c/":/"/",/"NPI_vod__c/":/"/",/"PDRP_MED__c/":false,/"PersonDoNotCall/":false,/"PersonEmail/":/"/",/"PersonHasOptedOutOfEmail/":false,/"PersonHasOptedOutOfFax/":false,/"PersonMobilePhone/":/"/",/"Phone/":/"/",/"Practicing_Specialty__c/":/"FM - FAMILY MEDICINE/",/"Primary_City__c/":/"/",/"Primary_State__c/":/"/",/"Primary_Street_Line2__c/":/"/",/"Primary_Street__c/":/"/",/"Primary_Zip__c/":/"/",/"RecordTypeId/":/"012U0000000JaPWIA0/",/"Request_Date__c/":/"2016-06-10T22:31:55.9647467Z/",/"ONY_ID__c/":/"/",/"Specialty_1_vod__c/":/"/",/"Suffix_vod__c/":/"/",/"Website/":/"/"}",
        "statusCode": "400"
    }
}
```

#### <a name="insert-error-into-cosmos-db--response"></a><span data-ttu-id="413f5-164">Cosmos Veritabanına--yanıt ekleme hatası</span><span class="sxs-lookup"><span data-stu-id="413f5-164">Insert error into Cosmos DB--response</span></span>

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
        "body": "CRM failed toocomplete task: Message: duplicate value found: CRM_HUB_ID__c duplicates value on record with id: 001U000001c83gK",
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

#### <a name="salesforce-error-response"></a><span data-ttu-id="413f5-165">Salesforce hata yanıtı</span><span class="sxs-lookup"><span data-stu-id="413f5-165">Salesforce error response</span></span>

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
        "message": "Salesforce failed toocomplete task: Message: duplicate value found: Account_ID_MED__c duplicates value on record with id: 001U000001c83gK",
        "source": "Salesforce.Common",
        "errors": []
    }
}

```

### <a name="return-hello-response-back-tooparent-logic-app"></a><span data-ttu-id="413f5-166">Dönüş hello yanıt geri tooparent mantıksal uygulama</span><span class="sxs-lookup"><span data-stu-id="413f5-166">Return hello response back tooparent logic app</span></span>

<span data-ttu-id="413f5-167">Merhaba yanıt aldıktan sonra hello yanıt geçirebilirsiniz geri toohello üst mantıksal uygulama.</span><span class="sxs-lookup"><span data-stu-id="413f5-167">After you get hello response, you can pass hello response back toohello parent logic app.</span></span>

#### <a name="return-success-response-tooparent-logic-app"></a><span data-ttu-id="413f5-168">Başarılı yanıt tooparent mantıksal uygulama Döndür</span><span class="sxs-lookup"><span data-stu-id="413f5-168">Return success response tooparent logic app</span></span>

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

#### <a name="return-error-response-tooparent-logic-app"></a><span data-ttu-id="413f5-169">Döndürülen hata yanıtı tooparent mantıksal uygulama</span><span class="sxs-lookup"><span data-stu-id="413f5-169">Return error response tooparent logic app</span></span>

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


## <a name="cosmos-db-repository-and-portal"></a><span data-ttu-id="413f5-170">Cosmos DB depo ve portal</span><span class="sxs-lookup"><span data-stu-id="413f5-170">Cosmos DB repository and portal</span></span>

<span data-ttu-id="413f5-171">Çözümümüzdür eklenen özellikleriyle [Cosmos DB](https://azure.microsoft.com/services/documentdb).</span><span class="sxs-lookup"><span data-stu-id="413f5-171">Our solution added capabilities with [Cosmos DB](https://azure.microsoft.com/services/documentdb).</span></span>

### <a name="error-management-portal"></a><span data-ttu-id="413f5-172">Hata Yönetim Portalı</span><span class="sxs-lookup"><span data-stu-id="413f5-172">Error management portal</span></span>

<span data-ttu-id="413f5-173">tooview hello hataları Cosmos DB'den bir MVC web uygulaması toodisplay hello hata kaydı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="413f5-173">tooview hello errors, you can create an MVC web app toodisplay hello error records from Cosmos DB.</span></span> <span data-ttu-id="413f5-174">Merhaba **listesi**, **ayrıntıları**, **Düzenle**, ve **silmek** işlemleri hello geçerli sürümde dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="413f5-174">hello **List**, **Details**, **Edit**, and **Delete** operations are included in hello current version.</span></span>

> [!NOTE]
> <span data-ttu-id="413f5-175">İşlem düzenleme: Cosmos DB hello tüm belgeyi yerini alır.</span><span class="sxs-lookup"><span data-stu-id="413f5-175">Edit operation: Cosmos DB replaces hello entire document.</span></span> <span data-ttu-id="413f5-176">Merhaba hello gösterilecek kayıt **listesi** ve **ayrıntı** örnekleri yalnızca görünümlerdir.</span><span class="sxs-lookup"><span data-stu-id="413f5-176">hello records shown in hello **List** and **Detail** views are samples only.</span></span> <span data-ttu-id="413f5-177">Bunlar gerçek hasta randevu kayıtlarını olup olmadığı.</span><span class="sxs-lookup"><span data-stu-id="413f5-177">They are not actual patient appointment records.</span></span>

<span data-ttu-id="413f5-178">Örnekler bizim MVC uygulamasının hello ile daha önce oluşturduğunuz ayrıntıları yaklaşımı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="413f5-178">Here are examples of our MVC app details created with hello previously described approach.</span></span>

#### <a name="error-management-list"></a><span data-ttu-id="413f5-179">Hata yönetim listesi</span><span class="sxs-lookup"><span data-stu-id="413f5-179">Error management list</span></span>
![Hata listesi](media/logic-apps-scenario-error-and-exception-handling/errorlist.png)

#### <a name="error-management-detail-view"></a><span data-ttu-id="413f5-181">Hata yönetim ayrıntılı Görünüm</span><span class="sxs-lookup"><span data-stu-id="413f5-181">Error management detail view</span></span>
![Hata Ayrıntıları](media/logic-apps-scenario-error-and-exception-handling/errordetails.png)

### <a name="log-management-portal"></a><span data-ttu-id="413f5-183">Günlük Yönetim Portalı</span><span class="sxs-lookup"><span data-stu-id="413f5-183">Log management portal</span></span>

<span data-ttu-id="413f5-184">tooview hello günlükleri, ayrıca bir MVC web uygulaması oluşturduk.</span><span class="sxs-lookup"><span data-stu-id="413f5-184">tooview hello logs, we also created an MVC web app.</span></span> <span data-ttu-id="413f5-185">Örnekler bizim MVC uygulamasının hello ile daha önce oluşturduğunuz ayrıntıları yaklaşımı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="413f5-185">Here are examples of our MVC app details created with hello previously described approach.</span></span>

#### <a name="sample-log-detail-view"></a><span data-ttu-id="413f5-186">Örnek günlük ayrıntılı Görünüm</span><span class="sxs-lookup"><span data-stu-id="413f5-186">Sample log detail view</span></span>
![Günlük ayrıntılı Görünüm](media/logic-apps-scenario-error-and-exception-handling/samplelogdetail.png)

### <a name="api-app-details"></a><span data-ttu-id="413f5-188">API uygulama ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="413f5-188">API app details</span></span>

#### <a name="logic-apps-exception-management-api"></a><span data-ttu-id="413f5-189">Logic Apps özel durum yönetimi API</span><span class="sxs-lookup"><span data-stu-id="413f5-189">Logic Apps exception management API</span></span>

<span data-ttu-id="413f5-190">Burada açıklandığı gibi açık kaynaklı Azure Logic Apps özel durum yönetimi API'si uygulamamıza işlevsellik sağlar - iki denetleyicisi vardır:</span><span class="sxs-lookup"><span data-stu-id="413f5-190">Our open-source Azure Logic Apps exception management API app provides functionality as described here - there are two controllers:</span></span>

* <span data-ttu-id="413f5-191">**ErrorController** bir DocumentDB koleksiyonu içinde bir hata kaydı (belge) ekler.</span><span class="sxs-lookup"><span data-stu-id="413f5-191">**ErrorController** inserts an error record (document) in a DocumentDB collection.</span></span>
* <span data-ttu-id="413f5-192">**LogController** bir DocumentDB koleksiyonu içinde bir günlük kaydı (belge) ekler.</span><span class="sxs-lookup"><span data-stu-id="413f5-192">**LogController** Inserts a log record (document) in a DocumentDB collection.</span></span>

> [!TIP]
> <span data-ttu-id="413f5-193">Her iki denetleyicilerinin kullandığı `async Task<dynamic>` biz oluşturabilmesi için işlemleri tooresolve çalışma zamanında işlemleri, DocumentDB şema hello işlemi hello gövdesinde hello.</span><span class="sxs-lookup"><span data-stu-id="413f5-193">Both controllers use `async Task<dynamic>` operations, allowing operations tooresolve at runtime, so we can create hello DocumentDB schema in hello body of hello operation.</span></span> 
> 

<span data-ttu-id="413f5-194">Her DocumentDB belgede benzersiz bir kimliği olmalıdır</span><span class="sxs-lookup"><span data-stu-id="413f5-194">Every document in DocumentDB must have a unique ID.</span></span> <span data-ttu-id="413f5-195">Kullanıyoruz `PatientId` ve dönüştürülen tooa UNIX zaman damgası değeri (double) olan bir zaman damgası ekleme.</span><span class="sxs-lookup"><span data-stu-id="413f5-195">We are using `PatientId` and adding a timestamp that is converted tooa Unix timestamp value (double).</span></span> <span data-ttu-id="413f5-196">Merhaba değeri tooremove hello kesir değerini olacak biçimde kesin.</span><span class="sxs-lookup"><span data-stu-id="413f5-196">We truncate hello value tooremove hello fractional value.</span></span>

<span data-ttu-id="413f5-197">Bizim hata denetleyicisinin API hello kaynak kodu görüntüleyebilirsiniz [github'dan](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi/blob/master/Logic App Exception Management API/Controllers/ErrorController.cs).</span><span class="sxs-lookup"><span data-stu-id="413f5-197">You can view hello source code of our error controller API [from GitHub](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi/blob/master/Logic App Exception Management API/Controllers/ErrorController.cs).</span></span>

<span data-ttu-id="413f5-198">Sözdizimi aşağıdaki hello kullanarak hello API mantığı uygulamasından diyoruz:</span><span class="sxs-lookup"><span data-stu-id="413f5-198">We call hello API from a logic app by using hello following syntax:</span></span>

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

<span data-ttu-id="413f5-199">Merhaba hello kod örnek denetler önceki hello ifadesinde *Create_NewPatientRecord* durumunu **başarısız**.</span><span class="sxs-lookup"><span data-stu-id="413f5-199">hello expression in hello preceding code sample checks for hello *Create_NewPatientRecord* status of **Failed**.</span></span>

## <a name="summary"></a><span data-ttu-id="413f5-200">Özet</span><span class="sxs-lookup"><span data-stu-id="413f5-200">Summary</span></span>

* <span data-ttu-id="413f5-201">Günlüğe kaydetme ve hata işleme bir mantıksal uygulama kolayca uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="413f5-201">You can easily implement logging and error handling in a logic app.</span></span>
* <span data-ttu-id="413f5-202">DocumentDB günlük ve hata kayıtları (belgeler) hello deposu olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="413f5-202">You can use DocumentDB as hello repository for log and error records (documents).</span></span>
* <span data-ttu-id="413f5-203">MVC toocreate portal toodisplay günlük ve hata kaydı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="413f5-203">You can use MVC toocreate a portal toodisplay log and error records.</span></span>

### <a name="source-code"></a><span data-ttu-id="413f5-204">Kaynak kod</span><span class="sxs-lookup"><span data-stu-id="413f5-204">Source code</span></span>

<span data-ttu-id="413f5-205">Merhaba hello Logic Apps özel durum yönetimi API uygulaması için kaynak kodunu kullanılabilir bu [GitHub deposunu](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi "mantığı uygulama özel durum yönetimi API").</span><span class="sxs-lookup"><span data-stu-id="413f5-205">hello source code for hello Logic Apps exception management API application is available in this [GitHub repository](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi "Logic App Exception Management API").</span></span>

## <a name="next-steps"></a><span data-ttu-id="413f5-206">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="413f5-206">Next steps</span></span>

* [<span data-ttu-id="413f5-207">Daha fazla mantıksal uygulama örnekleri ve senaryoları görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="413f5-207">View more logic app examples and scenarios</span></span>](../logic-apps/logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="413f5-208">Mantıksal uygulamaları izleme hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="413f5-208">Learn about monitoring logic apps</span></span>](../logic-apps/logic-apps-monitor-your-logic-apps.md)
* [<span data-ttu-id="413f5-209">Mantıksal uygulamalar için otomatik dağıtım şablonlar oluşturma</span><span class="sxs-lookup"><span data-stu-id="413f5-209">Create automated deployment templates for logic apps</span></span>](../logic-apps/logic-apps-create-deploy-template.md)
