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
# <a name="scenario-exception-handling-and-error-logging-for-logic-apps"></a>Senaryo: Özel durum işleme ve logic apps için hata günlüğü

Bu senaryo, bir mantıksal uygulama toobetter destek özel durum işleme nasıl genişletebileceğini açıklar. Gerçekçi kullanım örneği tooanswer hello soru kullandığımız: "Azure Logic Apps özel durumu ve hata işleme destekliyor mu?"

> [!NOTE]
> Merhaba geçerli Azure Logic Apps şeması eylem yanıtlar için bir standart şablon sağlar. Bu şablon, hem iç doğrulama hem de bir API uygulaması döndürülen hata yanıtları içerir.

## <a name="scenario-and-use-case-overview"></a>Senaryo ve kullanım örneği genel bakış

Bu senaryo için hello kullanım örneği olarak hello Öykü şöyledir: 

İyi bilinen bir sağlık kuruluş bize toodevelop hasta portal Microsoft Dynamics CRM Online kullanarak oluşturacak Azure çözümünü gerçekleştiriliyor. Bunlar toosend randevu kayıtlarını hello Dynamics CRM Online hasta portal Salesforce arasındaki gerekli. Toouse hello sorulan [HL7 FHIR](http://www.hl7.org/implement/standards/fhir/) tüm hasta kayıtları için standart.

Merhaba proje iki ana gereksinimlerini vardı:  

* Dynamics CRM Online portalı hello yöntemi toolog kayıtları gönderilen
* Bir şekilde tooview hello iş akışı içinde oluşan hatalar

> [!TIP]
> Bu proje hakkında üst düzey video için bkz: [tümleştirme kullanıcı grubu](http://www.integrationusergroup.com/logic-apps-support-error-handling/ "tümleştirme kullanıcı grubu").

## <a name="how-we-solved-hello-problem"></a>Nasıl biz hello sorun çözüldü

Seçtik [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/ "Azure Cosmos DB") (Cosmos DB başvuruyor belgeleri olarak toorecords) hello günlük ve hata kayıtları için depo olarak. Azure Logic Apps tüm yanıtlar için standart bir şablon olduğundan, biz toocreate özel şeması sahip olmaz. API uygulaması çok oluşturma**Ekle** ve **sorgu** hata ve günlük kayıtları için. Biz de her hello API uygulaması içindeki bir şema tanımlayabilirsiniz.  

Başka bir gereksinim toopurge kayıtları belirli bir tarihten sonra oluştu. Cosmos DB adlı bir özelliği vardır [zaman tooLive](https://azure.microsoft.com/blog/documentdb-now-supports-time-to-live-ttl/ "zaman tooLive") (TTL) izin bize tooset bir **zaman tooLive** her bir kayıt veya koleksiyon için değer. Bu özellik hello gerek toomanually Cosmos DB'de kayıt silme ortadan.

> [!IMPORTANT]
> toocomplete Bu öğretici, toocreate Cosmos DB veritabanı ve iki koleksiyonları (günlüğe kaydetme ve hatalar) gerekir.

## <a name="create-hello-logic-app"></a>Merhaba mantıksal uygulama oluşturma

Merhaba ilk toocreate hello mantıksal uygulama ve açık hello uygulama mantığını Uygulama Tasarımcısı'nda adımdır. Bu örnekte, üst-alt logic apps kullanıyoruz. Biz hello üst oluşturmuş ve toocreate bir alt mantıksal uygulama giderek varsayalım.

Dynamics CRM Online dışında gelen toolog hello kayıt olmaz çünkü hello üstünde başlayalım. Biz kullanmanız gerekir bir **isteği** hello üst mantıksal uygulama bu alt tetikler çünkü tetikler.

### <a name="logic-app-trigger"></a>Mantıksal uygulama tetikleyici

Kullanıyoruz bir **isteği** tetiklemek hello aşağıdaki örnekte gösterildiği gibi:

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


## <a name="steps"></a>Adımlar

Biz hello hasta kaydının hello kaynak (istek) hello Dynamics CRM Online portalından oturum açmanız gerekir.

1. Size yeni bir randevu kayıt Dynamics CRM Online'dan almanız gerekir.

   Merhaba tetikleyici CRM'den gelen sağlar bize ile Merhaba **CRM PatentId**, **kayıt türü**, **yeni veya güncelleştirilmiş kayıt** (yeni veya Boolean değeri güncelleştirin), ve  **SalesforceId**. Merhaba **SalesforceId** için bir güncelleştirme yalnızca kullanıldığından null olabilir.
   Biz hello CRM kullanarak hello CRM kaydı alma **PatientID** ve hello **kayıt türü**.

2. Tooadd bizim DocumentDB API uygulaması daha ihtiyacımız **InsertLogEntry** mantığı Uygulama Tasarımcısı'nda aşağıda gösterildiği gibi işlemi.

   **Günlük Girişi Ekle**

   ![Günlük Girişi Ekle](media/logic-apps-scenario-error-and-exception-handling/lognewpatient.png)

   **Hata Girişi Ekle**

   ![Günlük Girişi Ekle](media/logic-apps-scenario-error-and-exception-handling/insertlogentry.png)

   **Onay için kayıt hatası oluşturma**

   ![Koşul](media/logic-apps-scenario-error-and-exception-handling/condition.png)

## <a name="logic-app-source-code"></a>Mantıksal uygulama kaynak kodu

> [!NOTE]
> Örnek hello yalnızca örneklerdir. Bu öğretici, uygulama artık üretim dayalı olduğundan değerini hello bir **kaynak düğüm** ilgili tooscheduling bir randevu. özellikler görüntülemeyebilir > 

### <a name="logging"></a>Günlüğe kaydetme

mantıksal uygulama kodu aşağıdaki hello örnek gösterir nasıl toohandle günlüğe kaydetme.

#### <a name="log-entry"></a>Günlük girişi

Burada, bir günlük girişi ekleme hello mantığı uygulama kaynak kodu verilmiştir.

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

#### <a name="log-request"></a>Günlük isteği

Merhaba günlük istek iletisi toohello API uygulaması gönderilen aşağıdadır.

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


#### <a name="log-response"></a>Yanıtı Günlüğe Kaydet

Merhaba günlük yanıt iletisi hello API uygulaması'ndan aşağıda verilmiştir.

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

Şimdi adımları işleme hello hatasında bakalım.

### <a name="error-handling"></a>Hata işleme

Hello aşağıdaki mantığı uygulama kod örneği, hata işleme nasıl uygulayabileceğiniz gösterir.

#### <a name="create-error-record"></a>Hata kaydı oluşturma

Burada, bir hata kaydı oluşturmak için hello mantığı uygulama kaynak kodu verilmiştir.

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

#### <a name="insert-error-into-cosmos-db--request"></a>Ekleme hatası Cosmos Veritabanına--isteği

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

#### <a name="insert-error-into-cosmos-db--response"></a>Cosmos Veritabanına--yanıt ekleme hatası

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

#### <a name="salesforce-error-response"></a>Salesforce hata yanıtı

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

### <a name="return-hello-response-back-tooparent-logic-app"></a>Dönüş hello yanıt geri tooparent mantıksal uygulama

Merhaba yanıt aldıktan sonra hello yanıt geçirebilirsiniz geri toohello üst mantıksal uygulama.

#### <a name="return-success-response-tooparent-logic-app"></a>Başarılı yanıt tooparent mantıksal uygulama Döndür

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

#### <a name="return-error-response-tooparent-logic-app"></a>Döndürülen hata yanıtı tooparent mantıksal uygulama

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


## <a name="cosmos-db-repository-and-portal"></a>Cosmos DB depo ve portal

Çözümümüzdür eklenen özellikleriyle [Cosmos DB](https://azure.microsoft.com/services/documentdb).

### <a name="error-management-portal"></a>Hata Yönetim Portalı

tooview hello hataları Cosmos DB'den bir MVC web uygulaması toodisplay hello hata kaydı oluşturabilirsiniz. Merhaba **listesi**, **ayrıntıları**, **Düzenle**, ve **silmek** işlemleri hello geçerli sürümde dahil edilir.

> [!NOTE]
> İşlem düzenleme: Cosmos DB hello tüm belgeyi yerini alır. Merhaba hello gösterilecek kayıt **listesi** ve **ayrıntı** örnekleri yalnızca görünümlerdir. Bunlar gerçek hasta randevu kayıtlarını olup olmadığı.

Örnekler bizim MVC uygulamasının hello ile daha önce oluşturduğunuz ayrıntıları yaklaşımı açıklanmaktadır.

#### <a name="error-management-list"></a>Hata yönetim listesi
![Hata listesi](media/logic-apps-scenario-error-and-exception-handling/errorlist.png)

#### <a name="error-management-detail-view"></a>Hata yönetim ayrıntılı Görünüm
![Hata Ayrıntıları](media/logic-apps-scenario-error-and-exception-handling/errordetails.png)

### <a name="log-management-portal"></a>Günlük Yönetim Portalı

tooview hello günlükleri, ayrıca bir MVC web uygulaması oluşturduk. Örnekler bizim MVC uygulamasının hello ile daha önce oluşturduğunuz ayrıntıları yaklaşımı açıklanmaktadır.

#### <a name="sample-log-detail-view"></a>Örnek günlük ayrıntılı Görünüm
![Günlük ayrıntılı Görünüm](media/logic-apps-scenario-error-and-exception-handling/samplelogdetail.png)

### <a name="api-app-details"></a>API uygulama ayrıntıları

#### <a name="logic-apps-exception-management-api"></a>Logic Apps özel durum yönetimi API

Burada açıklandığı gibi açık kaynaklı Azure Logic Apps özel durum yönetimi API'si uygulamamıza işlevsellik sağlar - iki denetleyicisi vardır:

* **ErrorController** bir DocumentDB koleksiyonu içinde bir hata kaydı (belge) ekler.
* **LogController** bir DocumentDB koleksiyonu içinde bir günlük kaydı (belge) ekler.

> [!TIP]
> Her iki denetleyicilerinin kullandığı `async Task<dynamic>` biz oluşturabilmesi için işlemleri tooresolve çalışma zamanında işlemleri, DocumentDB şema hello işlemi hello gövdesinde hello. 
> 

Her DocumentDB belgede benzersiz bir kimliği olmalıdır Kullanıyoruz `PatientId` ve dönüştürülen tooa UNIX zaman damgası değeri (double) olan bir zaman damgası ekleme. Merhaba değeri tooremove hello kesir değerini olacak biçimde kesin.

Bizim hata denetleyicisinin API hello kaynak kodu görüntüleyebilirsiniz [github'dan](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi/blob/master/Logic App Exception Management API/Controllers/ErrorController.cs).

Sözdizimi aşağıdaki hello kullanarak hello API mantığı uygulamasından diyoruz:

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

Merhaba hello kod örnek denetler önceki hello ifadesinde *Create_NewPatientRecord* durumunu **başarısız**.

## <a name="summary"></a>Özet

* Günlüğe kaydetme ve hata işleme bir mantıksal uygulama kolayca uygulayabilirsiniz.
* DocumentDB günlük ve hata kayıtları (belgeler) hello deposu olarak kullanabilirsiniz.
* MVC toocreate portal toodisplay günlük ve hata kaydı kullanabilirsiniz.

### <a name="source-code"></a>Kaynak kod

Merhaba hello Logic Apps özel durum yönetimi API uygulaması için kaynak kodunu kullanılabilir bu [GitHub deposunu](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi "mantığı uygulama özel durum yönetimi API").

## <a name="next-steps"></a>Sonraki adımlar

* [Daha fazla mantıksal uygulama örnekleri ve senaryoları görüntüleyin](../logic-apps/logic-apps-examples-and-scenarios.md)
* [Mantıksal uygulamaları izleme hakkında bilgi edinin](../logic-apps/logic-apps-monitor-your-logic-apps.md)
* [Mantıksal uygulamalar için otomatik dağıtım şablonlar oluşturma](../logic-apps/logic-apps-create-deploy-template.md)
