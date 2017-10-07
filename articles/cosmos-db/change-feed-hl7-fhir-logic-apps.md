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
# <a name="notifying-patients-of-hl7-fhir-health-care-record-changes-using-logic-apps-and-azure-cosmos-db"></a><span data-ttu-id="1953d-104">Logic Apps ile Azure Cosmos DB HL7 FHIR sağlık kayıt değişiklikleri hastalar bildirme</span><span class="sxs-lookup"><span data-stu-id="1953d-104">Notifying patients of HL7 FHIR health care record changes using Logic Apps and Azure Cosmos DB</span></span>

<span data-ttu-id="1953d-105">Azure MVP Howard Edidin son tooadd yeni işlevsellik tootheir hasta portal istedik sağlık bir kuruluş tarafından kurulduğunu.</span><span class="sxs-lookup"><span data-stu-id="1953d-105">Azure MVP Howard Edidin was recently contacted by a healthcare organization that wanted tooadd new functionality tootheir patient portal.</span></span> <span data-ttu-id="1953d-106">Bunlar, sistem durumu kayıt güncelleştirildi ve hastalar toobe mümkün toosubscribe toothese güncelleştirmeler gerekli olduğunda toosend bildirimleri toopatients gerekli.</span><span class="sxs-lookup"><span data-stu-id="1953d-106">They needed toosend notifications toopatients when their health record was updated, and they needed patients toobe able toosubscribe toothese updates.</span></span> 

<span data-ttu-id="1953d-107">Bu makalede Azure Cosmos DB, mantıksal uygulamalar ve hizmet veri yolu kullanarak sağlık bu kuruluş için oluşturulan hello değişiklik akış bildirim çözüm anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="1953d-107">This article walks through hello change feed notification solution created for this healthcare organization using Azure Cosmos DB, Logic Apps, and Service Bus.</span></span> 

## <a name="project-requirements"></a><span data-ttu-id="1953d-108">Proje gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="1953d-108">Project requirements</span></span>
- <span data-ttu-id="1953d-109">XML biçiminde HL7 birleştirilmiş Klinik belge mimarisi (C-CDA) belgeleri sağlayıcıları gönderin.</span><span class="sxs-lookup"><span data-stu-id="1953d-109">Providers send HL7 Consolidated-Clinical Document Architecture (C-CDA) documents in XML format.</span></span> <span data-ttu-id="1953d-110">C CDA belgeleri neredeyse her belge türü, klinik belgelerini ailesi geçmişlerini ve immunization kayıtları, de olarak yönetim gibi iş akışı ve finansal dahil olmak üzere Klinik kapsar.</span><span class="sxs-lookup"><span data-stu-id="1953d-110">C-CDA documents encompass just about every type of clinical document, including clinical documents such as family histories and immunization records, as well as administrative, workflow, and financial documents.</span></span> 
- <span data-ttu-id="1953d-111">C CDA belgeleri çok dönüştürülür[HL7 FHIR kaynakları](http://hl7.org/fhir/2017Jan/resourcelist.html) JSON biçiminde.</span><span class="sxs-lookup"><span data-stu-id="1953d-111">C-CDA documents are converted too[HL7 FHIR Resources](http://hl7.org/fhir/2017Jan/resourcelist.html) in JSON format.</span></span>
- <span data-ttu-id="1953d-112">Değiştirilen FHIR kaynak belgeler, JSON biçiminde e-postayla gönderilir.</span><span class="sxs-lookup"><span data-stu-id="1953d-112">Modified FHIR resource documents are sent by email in JSON format.</span></span>

## <a name="solution-workflow"></a><span data-ttu-id="1953d-113">Çözümü iş akışı</span><span class="sxs-lookup"><span data-stu-id="1953d-113">Solution workflow</span></span> 

<span data-ttu-id="1953d-114">Yüksek düzeyde, aşağıdaki iş akışı adımları proje gerekli hello hello:</span><span class="sxs-lookup"><span data-stu-id="1953d-114">At a high level, hello project required hello following workflow steps:</span></span> 
1. <span data-ttu-id="1953d-115">C CDA belgeleri tooFHIR kaynakları dönüştürün.</span><span class="sxs-lookup"><span data-stu-id="1953d-115">Convert C-CDA documents tooFHIR resources.</span></span>
2. <span data-ttu-id="1953d-116">Değiştirilen FHIR kaynaklar için yoklama yinelenen tetikleyici gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="1953d-116">Perform recurring trigger polling for modified FHIR resources.</span></span> 
2. <span data-ttu-id="1953d-117">Bir özel uygulama, FhirNotificationApi, tooconnect tooAzure Cosmos DB ve sorgu için yeni veya değiştirilmiş belgeleri çağırın.</span><span class="sxs-lookup"><span data-stu-id="1953d-117">Call a custom app, FhirNotificationApi, tooconnect tooAzure Cosmos DB and query for new or modified documents.</span></span>
3. <span data-ttu-id="1953d-118">Merhaba yanıt tootoohello Service Bus kuyruğuna kaydedin.</span><span class="sxs-lookup"><span data-stu-id="1953d-118">Save hello response tootoohello Service Bus queue.</span></span>
4. <span data-ttu-id="1953d-119">Yoklama hello Service Bus kuyruğuna yeni iletiler için.</span><span class="sxs-lookup"><span data-stu-id="1953d-119">Poll for new messages in hello Service Bus queue.</span></span>
5. <span data-ttu-id="1953d-120">E-posta bildirimleri toopatients gönderin.</span><span class="sxs-lookup"><span data-stu-id="1953d-120">Send email notifications toopatients.</span></span>

## <a name="solution-architecture"></a><span data-ttu-id="1953d-121">Çözüm mimarisi</span><span class="sxs-lookup"><span data-stu-id="1953d-121">Solution architecture</span></span>
<span data-ttu-id="1953d-122">Bu çözüm gereksinimleri ve tam hello çözümü iş akışı yukarıdaki üç Logic Apps toomeet hello gerektirir.</span><span class="sxs-lookup"><span data-stu-id="1953d-122">This solution requires three Logic Apps toomeet hello above requirements and complete hello solution workflow.</span></span> <span data-ttu-id="1953d-123">Merhaba üç mantıksal uygulamalar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="1953d-123">hello three logic apps are:</span></span>
1. <span data-ttu-id="1953d-124">**HL7 FHIR eşleme uygulama**: Merhaba HL7 C-CDA belge alır, toohello FHIR kaynak dönüştürür ve ardından tooAzure Cosmos DB kaydeder.</span><span class="sxs-lookup"><span data-stu-id="1953d-124">**HL7-FHIR-Mapping app**: Receives hello HL7 C-CDA document, transforms it toohello FHIR Resource, then saves it tooAzure Cosmos DB.</span></span>
2. <span data-ttu-id="1953d-125">**EHR uygulama**: hello Azure Cosmos DB FHIR depo sorgular ve hello yanıt tooa Service Bus kuyruğuna kaydeder.</span><span class="sxs-lookup"><span data-stu-id="1953d-125">**EHR app**: Queries hello Azure Cosmos DB FHIR repository and saves hello response tooa Service Bus queue.</span></span> <span data-ttu-id="1953d-126">Bu mantıksal uygulama kullanan bir [API uygulaması](#api-app) tooretrieve yeni ve değiştirilmiş belgeleri.</span><span class="sxs-lookup"><span data-stu-id="1953d-126">This logic app uses an [API app](#api-app) tooretrieve new and changed documents.</span></span>
3. <span data-ttu-id="1953d-127">**İşlem bildirim uygulama**: hello gövdesinde hello FHIR kaynak belgeleri içeren bir e-posta bildirimi gönderir.</span><span class="sxs-lookup"><span data-stu-id="1953d-127">**Process notification app**: Sends an email notification with hello FHIR resource documents in hello body.</span></span>

![Bu HL7 FHIR sağlık çözümde kullanılan Hello üç Logic Apps](./media/change-feed-hl7-fhir-logic-apps/health-care-solution-hl7-fhir.png)



### <a name="azure-services-used-in-hello-solution"></a><span data-ttu-id="1953d-129">Merhaba çözümde kullanılan azure Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="1953d-129">Azure services used in hello solution</span></span>

#### <a name="azure-cosmos-db-documentdb-api"></a><span data-ttu-id="1953d-130">Azure Cosmos DB DocumentDB API</span><span class="sxs-lookup"><span data-stu-id="1953d-130">Azure Cosmos DB DocumentDB API</span></span>
<span data-ttu-id="1953d-131">Azure Cosmos DB hello hello FHIR kaynaklar için hello aşağıdaki şekilde gösterildiği gibi depodur.</span><span class="sxs-lookup"><span data-stu-id="1953d-131">Azure Cosmos DB is hello repository for hello FHIR resources as shown in hello following figure.</span></span>

![Bu HL7 FHIR sağlık öğreticide kullanılan hello Azure Cosmos DB hesabı](./media/change-feed-hl7-fhir-logic-apps/account.png)

#### <a name="logic-apps"></a><span data-ttu-id="1953d-133">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="1953d-133">Logic Apps</span></span>
<span data-ttu-id="1953d-134">Logic Apps hello iş akışı işlemi işleyin.</span><span class="sxs-lookup"><span data-stu-id="1953d-134">Logic Apps handle hello workflow process.</span></span> <span data-ttu-id="1953d-135">Merhaba aşağıdaki ekran görüntüleri hello Logic apps Bu çözüm için oluşturulan gösterir.</span><span class="sxs-lookup"><span data-stu-id="1953d-135">hello following screenshots show hello Logic apps created for this solution.</span></span> 


1. <span data-ttu-id="1953d-136">**HL7 FHIR eşleme uygulama**: Merhaba HL7 C-CDA belge almak ve Logic Apps Enterprise Integration Pack Merhaba kullanarak tooan FHIR kaynak Dönüştür.</span><span class="sxs-lookup"><span data-stu-id="1953d-136">**HL7-FHIR-Mapping app**: Receive hello HL7 C-CDA document and transform it tooan FHIR resource using hello Enterprise Integration Pack for Logic Apps.</span></span> <span data-ttu-id="1953d-137">Merhaba Enterprise Integration Pack Merhaba C CDA tooFHIR kaynakları eşleme hello işler.</span><span class="sxs-lookup"><span data-stu-id="1953d-137">hello Enterprise Integration Pack handles hello mapping from hello C-CDA tooFHIR resources.</span></span>

    ![Merhaba mantıksal uygulama tooreceive HL7 FHIR sağlık kayıtları kullanılan](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-json-transform.png)


2. <span data-ttu-id="1953d-139">**EHR uygulama**: Sorgu hello Azure Cosmos DB FHIR depo ve hello yanıt tooa Service Bus sıraya.</span><span class="sxs-lookup"><span data-stu-id="1953d-139">**EHR app**: Query hello Azure Cosmos DB FHIR repository and save hello response tooa Service Bus queue.</span></span> <span data-ttu-id="1953d-140">Merhaba hello GetNewOrModifiedFHIRDocuments uygulama aşağıda kodudur.</span><span class="sxs-lookup"><span data-stu-id="1953d-140">hello code for hello GetNewOrModifiedFHIRDocuments app is below.</span></span>

    ![Merhaba mantıksal kullanılan uygulama tooquery Azure Cosmos DB](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-api-app.png)

3. <span data-ttu-id="1953d-142">**İşlem bildirim uygulama**: hello gövdesinde hello FHIR kaynak belgeleri içeren bir e-posta bildirimi gönder.</span><span class="sxs-lookup"><span data-stu-id="1953d-142">**Process notification app**: Send an email notification with hello FHIR resource documents in hello body.</span></span>

    ![Merhaba mantıksal uygulama'hello gövdesinde hello HL7 FHIR kaynakla hasta e-posta gönderir](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-send-email.png)

#### <a name="service-bus"></a><span data-ttu-id="1953d-144">Service Bus</span><span class="sxs-lookup"><span data-stu-id="1953d-144">Service Bus</span></span>
<span data-ttu-id="1953d-145">Şekil gösterir hello hastalar sıra hello.</span><span class="sxs-lookup"><span data-stu-id="1953d-145">hello following figure shows hello patients queue.</span></span> <span data-ttu-id="1953d-146">Merhaba etiket özelliği değeri hello e-posta konusu için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1953d-146">hello Tag property value is used for hello email subject.</span></span>

![Merhaba bu HL7 FHIR öğreticide kullanılan hizmet veri yolu kuyruğu](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-service-bus-queue.png)

<a id="api-app"></a>

#### <a name="api-app"></a><span data-ttu-id="1953d-148">API uygulaması</span><span class="sxs-lookup"><span data-stu-id="1953d-148">API app</span></span>
<span data-ttu-id="1953d-149">Bir API uygulaması tooAzure Cosmos DB ve kaynak türüne göre yeni veya değiştirilmiş FHIR belgeler için sorgular bağlanır.</span><span class="sxs-lookup"><span data-stu-id="1953d-149">An API app connects tooAzure Cosmos DB and queries for new or modified FHIR documents By resource type.</span></span> <span data-ttu-id="1953d-150">Bu uygulamanın bir denetleyici yok **FhirNotificationApi** tek bir işlemle **GetNewOrModifiedFhirDocuments**, bkz: [API uygulaması için kaynak](#api-app-source).</span><span class="sxs-lookup"><span data-stu-id="1953d-150">This app has one controller, **FhirNotificationApi** with a one operation **GetNewOrModifiedFhirDocuments**, see [source for API app](#api-app-source).</span></span>

<span data-ttu-id="1953d-151">Merhaba kullanıyoruz [ `CreateDocumentChangeFeedQuery` ](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery.aspx) hello Azure Cosmos DB DocumentDB .NET API sınıfından.</span><span class="sxs-lookup"><span data-stu-id="1953d-151">We are using hello [`CreateDocumentChangeFeedQuery`](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery.aspx) class from hello Azure Cosmos DB DocumentDB .NET API.</span></span> <span data-ttu-id="1953d-152">Daha fazla bilgi için bkz: Merhaba [değişiklik akış makale](change-feed.md).</span><span class="sxs-lookup"><span data-stu-id="1953d-152">For more information, see hello [change feed article](change-feed.md).</span></span> 

##### <a name="getnewormodifiedfhirdocuments-operation"></a><span data-ttu-id="1953d-153">GetNewOrModifiedFhirDocuments işlemi</span><span class="sxs-lookup"><span data-stu-id="1953d-153">GetNewOrModifiedFhirDocuments operation</span></span>

<span data-ttu-id="1953d-154">**Girişleri**</span><span class="sxs-lookup"><span data-stu-id="1953d-154">**Inputs**</span></span>
- <span data-ttu-id="1953d-155">Databaseıd</span><span class="sxs-lookup"><span data-stu-id="1953d-155">DatabaseId</span></span>
- <span data-ttu-id="1953d-156">CollectionId</span><span class="sxs-lookup"><span data-stu-id="1953d-156">CollectionId</span></span>
- <span data-ttu-id="1953d-157">HL7 FHIR kaynak türü adı</span><span class="sxs-lookup"><span data-stu-id="1953d-157">HL7 FHIR Resource Type name</span></span>
- <span data-ttu-id="1953d-158">Boolean: Başlangıçtan itibaren Başlat</span><span class="sxs-lookup"><span data-stu-id="1953d-158">Boolean: Start from Beginning</span></span>
- <span data-ttu-id="1953d-159">Int: Döndürülen belgelerin sayısı</span><span class="sxs-lookup"><span data-stu-id="1953d-159">Int: Number of documents returned</span></span>

<span data-ttu-id="1953d-160">**Çıkışları**</span><span class="sxs-lookup"><span data-stu-id="1953d-160">**Outputs**</span></span>
- <span data-ttu-id="1953d-161">BAŞARI: Durum kodu: 200, yanıt: belgeleri (JSON dizisi) listesi</span><span class="sxs-lookup"><span data-stu-id="1953d-161">Success: Status Code: 200, Response: List of Documents (JSON Array)</span></span>
- <span data-ttu-id="1953d-162">Hata: Durum kodu: 404, yanıt: "hiçbir belge bulundu '*kaynak adı '* kaynak türü"</span><span class="sxs-lookup"><span data-stu-id="1953d-162">Failure: Status Code: 404, Response: "No Documents found for '*resource name'* Resource Type"</span></span>

<a id="api-app-source"></a>

<span data-ttu-id="1953d-163">**Merhaba API uygulaması için kaynak**</span><span class="sxs-lookup"><span data-stu-id="1953d-163">**Source for hello API app**</span></span>

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

### <a name="testing-hello-fhirnotificationapi"></a><span data-ttu-id="1953d-164">Merhaba FhirNotificationApi test etme</span><span class="sxs-lookup"><span data-stu-id="1953d-164">Testing hello FhirNotificationApi</span></span> 

<span data-ttu-id="1953d-165">Merhaba aşağıdaki görüntüde nasıl swagger kullanılan tootootest hello olduğu gösterilmektedir [FhirNotificationApi](#api-app-source).</span><span class="sxs-lookup"><span data-stu-id="1953d-165">hello following image demonstrates how swagger was used tootootest hello [FhirNotificationApi](#api-app-source).</span></span>

![Merhaba Swagger dosyası tootest hello API uygulaması kullanılan](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-testing-app.png)


### <a name="azure-portal-dashboard"></a><span data-ttu-id="1953d-167">Azure portalı panosunun</span><span class="sxs-lookup"><span data-stu-id="1953d-167">Azure portal dashboard</span></span>

<span data-ttu-id="1953d-168">Görüntü aşağıdaki hello tüm hello hello Azure portalı çalıştıran Bu çözüm için Azure services gösterir.</span><span class="sxs-lookup"><span data-stu-id="1953d-168">hello following image shows all of hello Azure services for this solution running in hello Azure portal.</span></span>

![Merhaba bu HL7 FHIR öğreticide kullanılan tüm hello Hizmetleri gösteren Azure portalı](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-portal.png)


## <a name="summary"></a><span data-ttu-id="1953d-170">Özet</span><span class="sxs-lookup"><span data-stu-id="1953d-170">Summary</span></span>

- <span data-ttu-id="1953d-171">Azure Cosmos DB yerel suppport bildirimleri için yeni veya değiştirilen belgeler ve toouse olmasından ne kadar kolay olduğunu öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="1953d-171">You have learned that Azure Cosmos DB has native suppport for notifications for new or modifed documents and how easy it is toouse.</span></span> 
- <span data-ttu-id="1953d-172">Logic Apps yararlanarak, herhangi bir kod yazmak zorunda kalmadan iş akışları oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1953d-172">By leveraging Logic Apps, you can create workflows without writing any code.</span></span>
- <span data-ttu-id="1953d-173">Azure Service Bus kuyruklarını toohandle hello dağıtım hello HL7 FHIR belgeler için kullanma.</span><span class="sxs-lookup"><span data-stu-id="1953d-173">Using Azure Service Bus Queues toohandle hello distribution for hello HL7 FHIR documents.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1953d-174">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1953d-174">Next steps</span></span>
<span data-ttu-id="1953d-175">Hello Azure Cosmos DB hakkında daha fazla bilgi için bkz: [Azure Cosmos DB giriş sayfası](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="1953d-175">For more information about Azure Cosmos DB, see hello [Azure Cosmos DB home page](https://azure.microsoft.com/services/cosmos-db/).</span></span> <span data-ttu-id="1953d-176">Logic Apps hakkında daha fazla bilgi için bkz: [Logic Apps](https://azure.microsoft.com/services/logic-apps/).</span><span class="sxs-lookup"><span data-stu-id="1953d-176">For more informaiton about Logic Apps, see [Logic Apps](https://azure.microsoft.com/services/logic-apps/).</span></span>


