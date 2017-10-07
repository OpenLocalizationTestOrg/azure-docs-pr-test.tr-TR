---
title: "HL7 FHIR kaynaklar - Azure Cosmos DB akış aaaChange | Microsoft Docs"
description: "Nasıl tooset yukarı değişiklik Azure mantıksal uygulamaları, Azure Cosmos DB ve hizmet veri yolu kullanarak HL7 FHIR hasta sağlık kayıtları bildirimlerinin öğrenin."
keywords: HL7 fhir
services: cosmos-db
author: hedidin
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: 0d25c11f-9197-419a-aa19-4614c6ab2d06
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: b-hoedid
ms.openlocfilehash: d2809bf5c6d8c193c49438d20684c56caea646bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="notifying-patients-of-hl7-fhir-health-care-record-changes-using-logic-apps-and-azure-cosmos-db"></a>Logic Apps ile Azure Cosmos DB HL7 FHIR sağlık kayıt değişiklikleri hastalar bildirme

Azure MVP Howard Edidin son tooadd yeni işlevsellik tootheir hasta portal istedik sağlık bir kuruluş tarafından kurulduğunu. Bunlar, sistem durumu kayıt güncelleştirildi ve hastalar toobe mümkün toosubscribe toothese güncelleştirmeler gerekli olduğunda toosend bildirimleri toopatients gerekli. 

Bu makalede Azure Cosmos DB, mantıksal uygulamalar ve hizmet veri yolu kullanarak sağlık bu kuruluş için oluşturulan hello değişiklik akış bildirim çözüm anlatılmaktadır. 

## <a name="project-requirements"></a>Proje gereksinimleri
- XML biçiminde HL7 birleştirilmiş Klinik belge mimarisi (C-CDA) belgeleri sağlayıcıları gönderin. C CDA belgeleri neredeyse her belge türü, klinik belgelerini ailesi geçmişlerini ve immunization kayıtları, de olarak yönetim gibi iş akışı ve finansal dahil olmak üzere Klinik kapsar. 
- C CDA belgeleri çok dönüştürülür[HL7 FHIR kaynakları](http://hl7.org/fhir/2017Jan/resourcelist.html) JSON biçiminde.
- Değiştirilen FHIR kaynak belgeler, JSON biçiminde e-postayla gönderilir.

## <a name="solution-workflow"></a>Çözümü iş akışı 

Yüksek düzeyde, aşağıdaki iş akışı adımları proje gerekli hello hello: 
1. C CDA belgeleri tooFHIR kaynakları dönüştürün.
2. Değiştirilen FHIR kaynaklar için yoklama yinelenen tetikleyici gerçekleştirin. 
2. Bir özel uygulama, FhirNotificationApi, tooconnect tooAzure Cosmos DB ve sorgu için yeni veya değiştirilmiş belgeleri çağırın.
3. Merhaba yanıt tootoohello Service Bus kuyruğuna kaydedin.
4. Yoklama hello Service Bus kuyruğuna yeni iletiler için.
5. E-posta bildirimleri toopatients gönderin.

## <a name="solution-architecture"></a>Çözüm mimarisi
Bu çözüm gereksinimleri ve tam hello çözümü iş akışı yukarıdaki üç Logic Apps toomeet hello gerektirir. Merhaba üç mantıksal uygulamalar şunlardır:
1. **HL7 FHIR eşleme uygulama**: Merhaba HL7 C-CDA belge alır, toohello FHIR kaynak dönüştürür ve ardından tooAzure Cosmos DB kaydeder.
2. **EHR uygulama**: hello Azure Cosmos DB FHIR depo sorgular ve hello yanıt tooa Service Bus kuyruğuna kaydeder. Bu mantıksal uygulama kullanan bir [API uygulaması](#api-app) tooretrieve yeni ve değiştirilmiş belgeleri.
3. **İşlem bildirim uygulama**: hello gövdesinde hello FHIR kaynak belgeleri içeren bir e-posta bildirimi gönderir.

![Bu HL7 FHIR sağlık çözümde kullanılan Hello üç Logic Apps](./media/change-feed-hl7-fhir-logic-apps/health-care-solution-hl7-fhir.png)



### <a name="azure-services-used-in-hello-solution"></a>Merhaba çözümde kullanılan azure Hizmetleri

#### <a name="azure-cosmos-db-documentdb-api"></a>Azure Cosmos DB DocumentDB API
Azure Cosmos DB hello hello FHIR kaynaklar için hello aşağıdaki şekilde gösterildiği gibi depodur.

![Bu HL7 FHIR sağlık öğreticide kullanılan hello Azure Cosmos DB hesabı](./media/change-feed-hl7-fhir-logic-apps/account.png)

#### <a name="logic-apps"></a>Logic Apps
Logic Apps hello iş akışı işlemi işleyin. Merhaba aşağıdaki ekran görüntüleri hello Logic apps Bu çözüm için oluşturulan gösterir. 


1. **HL7 FHIR eşleme uygulama**: Merhaba HL7 C-CDA belge almak ve Logic Apps Enterprise Integration Pack Merhaba kullanarak tooan FHIR kaynak Dönüştür. Merhaba Enterprise Integration Pack Merhaba C CDA tooFHIR kaynakları eşleme hello işler.

    ![Merhaba mantıksal uygulama tooreceive HL7 FHIR sağlık kayıtları kullanılan](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-json-transform.png)


2. **EHR uygulama**: Sorgu hello Azure Cosmos DB FHIR depo ve hello yanıt tooa Service Bus sıraya. Merhaba hello GetNewOrModifiedFHIRDocuments uygulama aşağıda kodudur.

    ![Merhaba mantıksal kullanılan uygulama tooquery Azure Cosmos DB](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-api-app.png)

3. **İşlem bildirim uygulama**: hello gövdesinde hello FHIR kaynak belgeleri içeren bir e-posta bildirimi gönder.

    ![Merhaba mantıksal uygulama'hello gövdesinde hello HL7 FHIR kaynakla hasta e-posta gönderir](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-send-email.png)

#### <a name="service-bus"></a>Service Bus
Şekil gösterir hello hastalar sıra hello. Merhaba etiket özelliği değeri hello e-posta konusu için kullanılır.

![Merhaba bu HL7 FHIR öğreticide kullanılan hizmet veri yolu kuyruğu](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-service-bus-queue.png)

<a id="api-app"></a>

#### <a name="api-app"></a>API uygulaması
Bir API uygulaması tooAzure Cosmos DB ve kaynak türüne göre yeni veya değiştirilmiş FHIR belgeler için sorgular bağlanır. Bu uygulamanın bir denetleyici yok **FhirNotificationApi** tek bir işlemle **GetNewOrModifiedFhirDocuments**, bkz: [API uygulaması için kaynak](#api-app-source).

Merhaba kullanıyoruz [ `CreateDocumentChangeFeedQuery` ](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery.aspx) hello Azure Cosmos DB DocumentDB .NET API sınıfından. Daha fazla bilgi için bkz: Merhaba [değişiklik akış makale](change-feed.md). 

##### <a name="getnewormodifiedfhirdocuments-operation"></a>GetNewOrModifiedFhirDocuments işlemi

**Girişleri**
- Databaseıd
- CollectionId
- HL7 FHIR kaynak türü adı
- Boolean: Başlangıçtan itibaren Başlat
- Int: Döndürülen belgelerin sayısı

**Çıkışları**
- BAŞARI: Durum kodu: 200, yanıt: belgeleri (JSON dizisi) listesi
- Hata: Durum kodu: 404, yanıt: "hiçbir belge bulundu '*kaynak adı '* kaynak türü"

<a id="api-app-source"></a>

**Merhaba API uygulaması için kaynak**

```C#

    using System.Collections.Generic;
    using System.Linq;
    using System.Net;
    using System.Net.Http;
    using System.Threading.Tasks;
    using System.Web.Http;
    using Microsoft.Azure.Documents;
    using Microsoft.Azure.Documents.Client;
    using Swashbuckle.Swagger.Annotations;
    using TRex.Metadata;
    
    namespace FhirNotificationApi.Controllers
    {
        /// <summary>
        ///     FHIR Resource Type Controller
        /// </summary>
        /// <seealso cref="System.Web.Http.ApiController" />
        public class FhirResourceTypeController : ApiController
        {
            /// <summary>
            ///     Gets hello new or modified FHIR documents from Last Run Date 
            ///     or create date of hello collection
            /// </summary>
            /// <param name="databaseId"></param>
            /// <param name="collectionId"></param>
            /// <param name="resourceType"></param>
            /// <param name="startfromBeginning"></param>
            /// <param name="maximumItemCount">-1 returns all (default)</param>
            /// <returns></returns>
            [Metadata("Get New or Modified FHIR Documents",
                "Query for new or modifed FHIR Documents By Resource Type " +
                "from Last Run Date or Begining of Collection creation"
            )]
            [SwaggerResponse(HttpStatusCode.OK, type: typeof(Task<dynamic>))]
            [SwaggerResponse(HttpStatusCode.NotFound, "No New or Modifed Documents found")]
            [SwaggerOperation("GetNewOrModifiedFHIRDocuments")]
            public async Task<dynamic> GetNewOrModifiedFhirDocuments(
                [Metadata("Database Id", "Database Id")] string databaseId,
                [Metadata("Collection Id", "Collection Id")] string collectionId,
                [Metadata("Resource Type", "FHIR resource type name")] string resourceType,
                [Metadata("Start from Beginning ", "Change Feed Option")] bool startfromBeginning,
                [Metadata("Maximum Item Count", "Number of documents returned. '-1 returns all' (default)")] int maximumItemCount = -1
            )
            {
                var collectionLink = UriFactory.CreateDocumentCollectionUri(databaseId, collectionId);
    
                var context = new DocumentDbContext();  
    
                var docs = new List<dynamic>();
    
                var partitionKeyRanges = new List<PartitionKeyRange>();
                FeedResponse<PartitionKeyRange> pkRangesResponse;
    
                do
                {
                    pkRangesResponse = await context.Client.ReadPartitionKeyRangeFeedAsync(collectionLink);
                    partitionKeyRanges.AddRange(pkRangesResponse);
                } while (pkRangesResponse.ResponseContinuation != null);
    
                foreach (var pkRange in partitionKeyRanges)
                {
                    var changeFeedOptions = new ChangeFeedOptions
                    {
                        StartFromBeginning = startfromBeginning,
                        RequestContinuation = null,
                        MaxItemCount = maximumItemCount,
                        PartitionKeyRangeId = pkRange.Id
                    };
    
                    using (var query = context.Client.CreateDocumentChangeFeedQuery(collectionLink, changeFeedOptions))
                    {
                        do
                        {
                            if (query != null)
                            {
                                var results = await query.ExecuteNextAsync<dynamic>().ConfigureAwait(false);
                                if (results.Count > 0)
                                    docs.AddRange(results.Where(doc => doc.resourceType == resourceType));
                            }
                            else
                            {
                                throw new HttpResponseException(new HttpResponseMessage(HttpStatusCode.NotFound));
                            }
                        } while (query.HasMoreResults);
                    }
                }
                if (docs.Count > 0)
                    return docs;
                var msg = new StringContent("No documents found for " + resourceType + " Resource");
                var response = new HttpResponseMessage
                {
                    StatusCode = HttpStatusCode.NotFound,
                    Content = msg
                };
                return response;
            }
        }
    }
    
```

### <a name="testing-hello-fhirnotificationapi"></a>Merhaba FhirNotificationApi test etme 

Merhaba aşağıdaki görüntüde nasıl swagger kullanılan tootootest hello olduğu gösterilmektedir [FhirNotificationApi](#api-app-source).

![Merhaba Swagger dosyası tootest hello API uygulaması kullanılan](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-testing-app.png)


### <a name="azure-portal-dashboard"></a>Azure portalı panosunun

Görüntü aşağıdaki hello tüm hello hello Azure portalı çalıştıran Bu çözüm için Azure services gösterir.

![Merhaba bu HL7 FHIR öğreticide kullanılan tüm hello Hizmetleri gösteren Azure portalı](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-portal.png)


## <a name="summary"></a>Özet

- Azure Cosmos DB yerel suppport bildirimleri için yeni veya değiştirilen belgeler ve toouse olmasından ne kadar kolay olduğunu öğrendiniz. 
- Logic Apps yararlanarak, herhangi bir kod yazmak zorunda kalmadan iş akışları oluşturabilirsiniz.
- Azure Service Bus kuyruklarını toohandle hello dağıtım hello HL7 FHIR belgeler için kullanma.

## <a name="next-steps"></a>Sonraki adımlar
Hello Azure Cosmos DB hakkında daha fazla bilgi için bkz: [Azure Cosmos DB giriş sayfası](https://azure.microsoft.com/services/cosmos-db/). Logic Apps hakkında daha fazla bilgi için bkz: [Logic Apps](https://azure.microsoft.com/services/logic-apps/).


