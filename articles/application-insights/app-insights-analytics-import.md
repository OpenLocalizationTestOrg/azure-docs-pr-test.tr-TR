---
title: "aaaImport, veri tooAnalytics Azure Application ınsights'ta | Microsoft Docs"
description: "Statik veri toojoin uygulama telemetri ile içeri aktarma veya ayrı veri akışı tooquery Analytics ile içeri aktarın."
services: application-insights
keywords: "Şema, veri alma açın"
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: bwren
ms.openlocfilehash: 7a3a3c9155adc1885dd366ddb13dda80bb894adb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="import-data-into-analytics"></a>İçeri aktarma veri analizi

Hiç tablo verisi içine aktarmak [Analytics](app-insights-analytics.md), ya da toojoin ile [Application Insights](app-insights-overview.md) , uygulamanızdan alınan telemetri veya böylece ayrı bir akış olarak çözümleyebilirsiniz. Analytics telemetri bir güçlü sorgu dili oldukça uygun tooanalyzing yüksek hacimli zaman damgalı Akışları ' dir.

Veri kendi Şeması'nı kullanarak Analytics aktarabilirsiniz. Toouse hello istek veya izleme gibi standart Application Insights şemalar sahip değil.

JSON veya DSV (sınırlayıcı virgülle ayrılmış değerler - virgül, noktalı virgül veya sekme) içe aktarabilirsiniz dosyaları.

TooAnalytics alma yararlı olduğu üç durumlar vardır:

* **Uygulama telemetriyle katılın.** Örneğin, gelen Web sitesi toomore okunabilir sayfa başlıklarını URL'leri eşleyen bir tablo içe aktarılamadı. Analizleri, on en popüler sayfa, Web sitenizdeki hello gösteren bir Pano grafiği raporunu oluşturabilirsiniz. Şimdi, sayfa başlıklarını hello URL'leri yerine hello gösterebilir.
* **Uygulama telemetrinin bağıntısını** ağ trafiğini gibi diğer kaynaklar ile sunucu verilerini ya da CDN günlük dosyaları.
* **Analytics tooa ayrı veri akışı uygulayın.** Uygulama Öngörüler Analytics seyrek, zaman damgalı akışları - SQL birçok durumda daha iyi ile iyi çalışan bir güçlü aracıdır. Bu tür bir akış başka bir kaynak sunucudan varsa Analytics ile analiz edebilirsiniz.

Gönderen veri tooyour veri kaynağı kolaydır. 

1. (Bir saat) Verilerinizi 'veri kaynağında' Hello şeması tanımlayın.
2. (Düzenli aralıklarla) Veri tooAzure depolama alanınızı karşıya yükleme ve hello REST API toonotify yeni veri alımı için bekliyor bizi arayın. Birkaç dakika içinde hello veri analizi sorgu için kullanılabilir.

Merhaba hello karşıya yükleme sıklığını sizin tarafınızdan tanımlanır ve sorgular için kullanılabilir, veri toobe ne kadar hızlı istersiniz. Daha verimli tooupload veri daha büyük öbek, ancak 1 GB'den büyük var.

> [!NOTE]
> *Çok sayıda veri kaynakları tooanalyze var mı?* [*Kullanmayı* logstash *tooship Application Insights verilerinizi.*](https://github.com/Microsoft/logstash-output-application-insights)
> 

## <a name="before-you-start"></a>Başlamadan önce

Gerekenler:

1. Microsoft Azure Application Insights kaynağı.

 * Verilerinizden ayrı olarak diğer telemetri tooanalyze istiyorsanız [yeni bir Application Insights kaynağı oluşturma](app-insights-create-new-resource.md).
 * Birleştirme ya da Application Insights ile zaten ayarlanmış bir uygulamadan telemetri verilerinizle karşılaştırma, bu uygulama için hello kaynak kullanabilirsiniz.
 * Katkıda bulunan veya sahibi erişim toothat kaynak.
 
2. Azure depolama. TooAzure depolama yükleme ve analiz verilerinizi buradan alır. 

 * Bloblarınızın için ayrılmış depolama hesabı oluşturma öneririz. Diğer işlemlerle bloblarınızın paylaştırılmışsa bloblarınızın bizim işlemleri tooread için daha uzun sürer.


## <a name="define-your-schema"></a>Şemanızı tanımlayın

Veri almadan önce tanımlamalısınız bir *veri kaynağı* hello şema verilerinizin belirtir.
Tek bir Application Insights kaynağı too50 veri kaynaklarına sahip olabilir

1. Merhaba veri kaynağı Sihirbazı'nı başlatın. "Yeni veri kaynağı Ekle" düğmesini kullanın. Alternatif olarak - sağ üst köşedeki ayarlar düğmesine tıklayın ve açılan menüde "Veri kaynakları" seçin.

    ![Yeni veri kaynağı ekleme](./media/app-insights-analytics-import/add-new-data-source.png)

    Yeni veri kaynağı için bir ad sağlayın.

2. Karşıya yükleyecek hello dosyalarının biçimi tanımlayın.

    Merhaba biçimi manuel olarak tanımlamak veya bir örnek dosya karşıya yükleme.

    CSV biçiminde Hello veri olması durumunda hello örnek hello ilk satırında sütun üst bilgileri olabilir. Merhaba sonraki adımda hello alan adlarını değiştirebilirsiniz.

    Merhaba örnek en az 10 satır veya veri kayıtlarının içermelidir.

    Sütun veya alan adı alfasayısal adlarını (olmadan, boşluk veya noktalama) olması gerekir.

    ![Örnek dosya karşıya yükleme](./media/app-insights-analytics-import/sample-data-file.png)


3. Sihirbaz hello gözden geçirme hello şema aldım. Bir örnek hello türlerinden çıkarımı yapılan tooadjust çıkarımı yapılan hello hello sütun türlerini gerekebilir.

    ![Gözden geçirme çıkarımı yapılan hello şeması](./media/app-insights-analytics-import/data-source-review-schema.png)

 * (İsteğe bağlı.) Bir şema tanımı karşıya yükleyin. Aşağıdaki Hello biçimini bakın.

 * Bir zaman damgası seçin. Tüm veriler Analytics, zaman damgası alanı olması gerekir. Türü olmalıdır `datetime`, ancak 'timestamp' adlı toobe sahip değil. Verilerinizi bir tarih ve saati ISO biçiminde içeren bir sütun varsa, bu hello zaman damgası sütunu olarak seçin. Aksi takdirde, "veri olarak gelen" seçin ve hello içeri aktarma işlemi zaman damgası alanı ekler.

5. Merhaba veri kaynağı oluşturun.

### <a name="schema-definition-file-format"></a>Şema tanımlama dosyası biçimi

UI Hello şemada düzenlemek yerine, bir dosyadan hello şema tanımı yükleyebilirsiniz. Merhaba şema tanım biçimi aşağıdaki gibidir: 

Sınırlandırılmış biçimi 
```
[ 
    {"location": "0", "name": "RequestName", "type": "string"}, 
    {"location": "1", "name": "timestamp", "type": "datetime"}, 
    {"location": "2", "name": "IPAddress", "type": "string"} 
] 
```

JSON biçimi 
```
[ 
    {"location": "$.name", "name": "name", "type": "string"}, 
    {"location": "$.alias", "name": "alias", "type": "string"}, 
    {"location": "$.room", "name": "room", "type": "long"} 
]
```
 
Her sütunun hello konumu, adı ve türü ile tanımlanır. 

* Konum – ayrılmış dosya biçimlendirmek için eşlenen hello değerin hello konumu değil. JSON için onu hello jpath eşlenen hello anahtarının biçimidir.
* Adı – hello hello sütunun adı görüntülenir.
* Türü – bu sütunun veri türünü hello.
 
Örnek verileri kullanıldı ve dosya biçimi ayrılmış durumda hello şema tanımı tüm sütunları eşleme ve yeni sütunlar hello sonunda eklemeniz gerekir. 

JSON hello veri kısmi bir eşleme sağlar, bu nedenle hello JSON biçimine şema tanımı toomap örnek verilerde bulunan her anahtar yok. Bunu ayrıca hello örnek veri parçası olmayan sütunları eşleyebilirsiniz. 

## <a name="import-data"></a>Veri içeri aktarma

tooimport veri tooAzure depolama yükleme, bir erişim anahtarı oluşturun ve ardından bir REST API çağrısı yapın.

![Yeni veri kaynağı ekleme](./media/app-insights-analytics-import/analytics-upload-process.png)

İşlemi el ile aşağıdaki hello gerçekleştirmek veya Otomatik Sistem toodo düzenli aralıklarla ayarlayın. Tooimport istediğiniz her veri bloğu için şu adımları toofollow gerekir.

1. Merhaba verileri çok karşıya[Azure blob depolama](../storage/blobs/storage-dotnet-how-to-use-blobs.md). 

 * BLOB'ları sıkıştırılmamış too1GB yukarı herhangi bir boyutta olabilir. Yüzlerce MB büyük BLOB'lar performans açısından idealdir.
 * Gzip tooimprove karşıya yükleme zamanı ve hello veri toobe sorgu için kullanılabilecek için gecikme süresine sahip sıkıştırabilirsiniz. Kullanım hello `.gz` dosya adı uzantısı.
 * Bu amaçla tooavoid çağrıları performans yavaşlamasının farklı hizmetlerden en iyi toouse ayrı bir depolama hesabı içindir.
 * Yüksek yoğunlukta veri gönderirken, her birkaç saniyede bir depolama hesabı, performans nedenleriyle birden çok toouse önerilir.

 
2. [Merhaba blob için bir paylaşılan erişim imzası anahtar oluşturma](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md). Hello anahtarı bir sona erme süresi bir gün ve okuma erişimi sağlamanız gerekir.
3. Bir REST çağrısı toonotify veri bekleyen Application Insights olun.

 * Uç noktası:`https://dc.services.visualstudio.com/v2/track`
 * HTTP yöntemini: POST
 * Yük:

```JSON

    {
       "data": {
            "baseType":"OpenSchemaData",
            "baseData":{
               "ver":"2",
               "blobSasUri":"<Blob URI with Shared Access Key>",
               "sourceName":"<Schema ID>",
               "sourceVersion":"1.0"
             }
       },
       "ver":1,
       "name":"Microsoft.ApplicationInsights.OpenSchema",
       "time":"<DateTime>",
       "iKey":"<instrumentation key>"
    }
```

Merhaba yer tutucuları şunlardır:

* `Blob URI with Shared Access Key`:, İşlem bu bir anahtar oluşturmak için hello yordamdan alırsınız. Belirli toohello blob var.
* `Schema ID`: Merhaba, tanımlı bir şeması için oluşturulan şema kimliği. Bu blob Hello verilerde toohello şema uygun olmalıdır.
* `DateTime`: hangi hello isteği gönderildi, başlangıç zamanı UTC. Biz bu biçimlerini kabul: ISO8601 (gibi "2016-01-01 13:45:01"); Rfc822 ("Çar, 14 Ara 16 14:57:01 + 0000"); RFC850 ("Çarşamba, 14 Ara 16 14:57:00 UTC"); RFC1123 ("Çar, 14 Ara 2016 14:57:00 + 0000").
* `Instrumentation key`Application Insights kaynağınıza.

Merhaba veri analizleri birkaç dakika sonra kullanılabilir.

## <a name="error-responses"></a>Hata yanıtları

* **400 Hatalı istek**: Bu hello isteği yükü geçersiz gösterir. Denetleme:
 * Doğru izleme anahtarı.
 * Geçerli saat değeri. Başlangıç zamanı, UTC şimdi olmalıdır.
 * JSON hello olayın toohello şema uyumludur.
* **403 Yasak**: hello blob gönderilen erişilebilir durumda değil. Bu hello paylaşılan erişim anahtarı geçerli değil ve süresi geçmemiş emin olun.
* **404 Bulunamadı**:
 * Merhaba blob yok.
 * Merhaba SourceId yanlış olur.

Daha ayrıntılı bilgi hello yanıt hata iletisinde kullanılabilir.


## <a name="sample-code"></a>Örnek kod

Bu kodu hello kullanır [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) NuGet paketi.

### <a name="classes"></a>Sınıfları

```C#
namespace IngestionClient 
{ 
    using System; 
    using Newtonsoft.Json; 

    public class AnalyticsDataSourceIngestionRequest 
    { 
        #region Members 
        private const string BaseDataRequiredVersion = "2"; 
        private const string RequestName = "Microsoft.ApplicationInsights.OpenSchema"; 
        #endregion Members 

        public AnalyticsDataSourceIngestionRequest(string ikey, string schemaId, string blobSasUri, int version = 1) 
        { 
            Ver = version; 
            IKey = ikey; 
            Data = new Data 
            { 
                BaseData = new BaseData 
                { 
                    Ver = BaseDataRequiredVersion, 
                    BlobSasUri = blobSasUri, 
                    SourceName = schemaId, 
                    SourceVersion = version.ToString() 
                } 
            }; 
        } 


        [JsonProperty("data")] 
        public Data Data { get; set; } 

        [JsonProperty("ver")] 
        public int Ver { get; set; } 

        [JsonProperty("name")] 
        public string Name { get { return RequestName; } } 

        [JsonProperty("time")] 
        public DateTime Time { get { return DateTime.UtcNow; } } 

        [JsonProperty("iKey")] 
        public string IKey { get; set; } 
    } 

    #region Internal Classes 

    public class Data 
    { 
        private const string DataBaseType = "OpenSchemaData"; 

        [JsonProperty("baseType")] 
        public string BaseType 
        { 
            get { return DataBaseType; } 
        } 

        [JsonProperty("baseData")] 
        public BaseData BaseData { get; set; } 
    } 


    public class BaseData 
    { 
        [JsonProperty("ver")] 
        public string Ver { get; set; } 

        [JsonProperty("blobSasUri")] 
        public string BlobSasUri { get; set; } 

        [JsonProperty("sourceName")] 
        public string SourceName { get; set; } 

        [JsonProperty("sourceVersion")] 
        public string SourceVersion { get; set; } 
    } 

    #endregion Internal Classes 
} 


namespace IngestionClient 
{ 
    using System; 
    using System.IO; 
    using System.Net; 
    using System.Text; 
    using System.Threading.Tasks; 
    using Newtonsoft.Json; 

    public class AnalyticsDataSourceClient 
    { 
        #region Members 
        private readonly Uri endpoint = new Uri("https://dc.services.visualstudio.com/v2/track"); 
        private const string RequestContentType = "application/json; charset=UTF-8"; 
        private const string RequestAccess = "application/json"; 
        #endregion Members 

        #region Public 

        public async Task<bool> RequestBlobIngestion(AnalyticsDataSourceIngestionRequest ingestionRequest) 
        { 
            HttpWebRequest request = WebRequest.CreateHttp(endpoint); 
            request.Method = WebRequestMethods.Http.Post; 
            request.ContentType = RequestContentType; 
            request.Accept = RequestAccess; 

            string notificationJson = Serialize(ingestionRequest); 
            byte[] notificationBytes = GetContentBytes(notificationJson); 
            request.ContentLength = notificationBytes.Length; 

            Stream requestStream = request.GetRequestStream(); 
            requestStream.Write(notificationBytes, 0, notificationBytes.Length); 
            requestStream.Close(); 

            try 
            { 
                using (var response = (HttpWebResponse)await request.GetResponseAsync())
                {
                    return response.StatusCode == HttpStatusCode.OK;
                }
            } 
            catch (WebException e) 
            { 
                HttpWebResponse httpResponse = e.Response as HttpWebResponse; 
                if (httpResponse != null) 
                { 
                    Console.WriteLine( 
                        "Ingestion request failed with status code: {0}. Error: {1}", 
                        httpResponse.StatusCode, 
                        httpResponse.StatusDescription); 
                    return false; 
                }
                throw; 
            } 
        } 
        #endregion Public 

        #region Private 
        private byte[] GetContentBytes(string content) 
        { 
            return Encoding.UTF8.GetBytes(content);
        } 


        private string Serialize(AnalyticsDataSourceIngestionRequest ingestionRequest) 
        { 
            return JsonConvert.SerializeObject(ingestionRequest); 
        } 
        #endregion Private 
    } 
} 
```

### <a name="ingest-data"></a>Veriyi çekme

Bu kodu her bir blob için kullanın. 

```C#
   AnalyticsDataSourceClient client = new AnalyticsDataSourceClient(); 

   var ingestionRequest = new AnalyticsDataSourceIngestionRequest("iKey", "sourceId", "blobUrlWithSas"); 

   bool success = await client.RequestBlobIngestion(ingestionRequest);
```

## <a name="next-steps"></a>Sonraki adımlar

* [Merhaba günlük analizi sorgu dili turu](app-insights-analytics-tour.md)
* [Kullanım *Logstash* toosend veri tooApplication Öngörüler](https://github.com/Microsoft/logstash-output-application-insights)
