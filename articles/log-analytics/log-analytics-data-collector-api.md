---
title: "aaaLog Analytics HTTP veri toplayıcı API | Microsoft Docs"
description: "Merhaba günlük analizi HTTP veri toplayıcı API tooadd POST JSON veri toohello günlük analizi deposu hello REST API'si çağırabilirsiniz herhangi bir istemciden kullanabilirsiniz. Bu makalede nasıl toouse API hello ve örnekleri sahip farklı programlama dillerini kullanarak toopublish veri."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: 
ms.assetid: a831fd90-3f55-423b-8b20-ccbaaac2ca75
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: bwren
ms.openlocfilehash: c2921082831c49da764d946ac9c4fab975a38185
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="send-data-toolog-analytics-with-hello-http-data-collector-api"></a>Merhaba HTTP veri toplayıcı API ile veri tooLog Analytics Gönder
Bu makalede nasıl toouse hello REST API istemciden gelen HTTP veri toplayıcı API toosend veri tooLog Analytics gösterilmektedir.  Komut dosyası veya uygulama tarafından toplanan tooformat verileri bir istekte içerir ve nasıl günlük analizi tarafından yetkili bu istekte açıklar.  PowerShell, C# ve Python için örnekler verilmiştir.

## <a name="concepts"></a>Kavramlar
Bir REST API'si çağırabilirsiniz herhangi bir istemciden hello HTTP veri toplayıcı API toosend veri tooLog Analytics kullanabilirsiniz.  Bu runbook olabilir Azure Otomasyonu'nda yönetim toplar Azure veya başka bir bulut ya da verileri günlük analizi tooconsolidate kullanan bir alternatif yönetim sisteminin ve verileri analiz etmek.

Merhaba günlük analizi deposundaki tüm verileri belirli bir kayıt türü içeren bir kayıt olarak depolanır.  Veri toosend toohello HTTP veri toplayıcı API JSON içinde birden çok kayıt olarak biçimlendirin.  Merhaba veri gönderdiğinde, tek bir kaydın hello depo hello isteği yükü her kayıt için oluşturulur.


![HTTP veri toplayıcı genel bakış](media/log-analytics-data-collector-api/overview.png)



## <a name="create-a-request"></a>Bir isteği oluşturun
toouse hello HTTP veri toplayıcı API hello veri toosend JavaScript nesne gösterimi (JSON) içeren bir POST isteği oluşturun.  her istek için gerekli olan sonraki üç tablolar listesi hello öznitelikler hello. Biz her özniteliği hello makalenin sonraki bölümlerinde daha ayrıntılı açıklanmıştır.

### <a name="request-uri"></a>İstek URI'si
| Öznitelik | Özellik |
|:--- |:--- |
| Yöntem |YAYINLA |
| URI |https://\<CustomerID\>.ods.opinsights.azure.com/api/logs?api-version=2016-04-01 |
| İçerik türü |uygulama/json |

### <a name="request-uri-parameters"></a>İstek URI parametreleri
| Parametre | Açıklama |
|:--- |:--- |
| CustomerID |Merhaba hello Microsoft Operations Management Suite çalışma alanı için benzersiz tanımlayıcı. |
| Kaynak |Merhaba API kaynak adı: / api/günlükleri. |
| API sürümü |Bu istek ile Merhaba API toouse Hello sürümü. Şu anda, 2016-04-01 değil. |

### <a name="request-headers"></a>İstek üstbilgileri
| Üstbilgi | Açıklama |
|:--- |:--- |
| Yetkilendirme |Merhaba yetkilendirme imzası. Merhaba makalenin sonraki bölümlerinde, hakkında bilgi edinebilirsiniz toocreate HMAC SHA256 üstbilgi. |
| Günlük türü |Merhaba kayıt gönderiliyor hello veri türünü belirtin. Şu anda, yalnızca alfasayısal karakterler hello günlük türünü destekler. Sayısal türler veya özel karakterler desteklemez. |
| x-ms-date |Başlangıç tarihi, Başlangıç isteği işlendi, RFC 1123 biçiminde. |
| saat oluşturulan alanı |Merhaba veri öğesinin hello zaman damgası içeren hello veri alanına Hello adı. Bir alan belirtin sonra içeriği için kullanılan **TimeGenerated**. Bu alan belirtilmezse, varsayılan hello **TimeGenerated** bu hello hello zamandır ileti alınan. Merhaba ileti alanının Merhaba içeriğine hello ISO 8601 biçimi YYYY izlemelidir-aa-: ssZ. |

## <a name="authorization"></a>Yetkilendirme
Tüm istek toohello günlük analizi HTTP veri toplayıcı API bir authorization üstbilgisi eklemeniz gerekir. bir istek tooauthenticate hello istekle hello birincil ya da hello isteği yapan hello çalışma alanı için ikincil anahtar hello oturum açmanız gerekir. Daha sonra bu imza hello isteğin bir parçası geçirin.   

Merhaba authorization üstbilgisi için hello biçimi şöyledir:

```
Authorization: SharedKey <WorkspaceID>:<Signature>
```

*Workspaceıd* hello Operations Management Suite çalışma hello benzersiz tanımlayıcısıdır. *İmza* olan bir [karma tabanlı ileti kimlik doğrulama kodu (HMAC)](https://msdn.microsoft.com/library/system.security.cryptography.hmacsha256.aspx) hello isteğinden oluşturulan ve hello kullanarak hesaplanan [SHA256 algoritmasını](https://msdn.microsoft.com/library/system.security.cryptography.sha256.aspx). Ardından, onu Base64 kodlaması kullanarak kodlayın.

Bu biçim tooencode hello kullan **SharedKey** imza dizesi:

```
StringToSign = VERB + "\n" +
                  Content-Length + "\n" +
               Content-Type + "\n" +
                  x-ms-date + "\n" +
                  "/api/logs";
```

İmza dize örneği şöyledir:

```
POST\n1024\napplication/json\nx-ms-date:Mon, 04 Apr 2016 08:00:00 GMT\n/api/logs
```

Kullanarak kodlayın hello imza dize olduğunda HMAC SHA256 algoritmasını hello UTF-8 kodlu dize üzerinde hello ve hello sonucu Base64 olarak kodlayın. Şu biçimi kullanın:

```
Signature=Base64(HMAC-SHA256(UTF8(StringToSign)))
```

Merhaba sonraki bölümlerde Hello örnekleri bir authorization üstbilgisi oluşturduğunuz örnek kod toohelp sahip.

## <a name="request-body"></a>İstek gövdesi
Merhaba ileti gövdesi Hello JSON'de olması gerekir. Bu biçimde hello özelliği ad ve değer çiftleri ile bir veya daha fazla kayıt içermesi gerekir:

```
{
"property1": "value1",
" property 2": "value2"
" property 3": "value3",
" property 4": "value4"
}
```

Biçim aşağıdaki hello kullanarak tek bir istekte birden çok kayıt toplu. Tüm hello kayıtları hello olmalıdır aynı kayıt türü.

```
{
"property1": "value1",
" property 2": "value2"
" property 3": "value3",
" property 4": "value4"
},
{
"property1": "value1",
" property 2": "value2"
" property 3": "value3",
" property 4": "value4"
}
```

## <a name="record-type-and-properties"></a>Kayıt türü ve özellikleri
Merhaba günlük analizi HTTP veri toplayıcı API aracılığıyla veri gönderdiğinde, özel bir kayıt türü tanımlarsınız. Şu anda, oluşturulan kayıt türleri diğer veri türleri ve çözümleri tarafından veri tooexisting yazamıyor. Günlük analizi hello gelen verileri okur ve girdiğiniz hello değerlerin hello veri türüyle eşleşen özelliklerini oluşturur.

Günlük analizi API içermelidir her isteği toohello bir **günlük türü** hello kayıt türünün hello ada sahip üstbilgi. Merhaba soneki **_CL** otomatik olarak eklenen toohello addır, diğer günlüğünden türleri özel bir günlük toodistinguish girin. Örneğin, hello adı girerseniz **MyNewRecordType**, günlük analizi hello türündeki bir kayıt oluşturur **MyNewRecordType_CL**. Bu, kullanıcı tarafından oluşturulan tür adları ve bunlar geçerli veya gelecek Microsoft çözümlerinde sevk arasında çakışmalar olduğundan emin olun yardımcı olur.

tooidentify bir özelliğin veri türü, günlük analizi soneki toohello özellik adı ekler. Bir özellik boş bir değer içeriyorsa, hello özelliği bulunan ve bu kaydı bulunmaz. Bu tabloda hello özellik veri türünü ve karşılık gelen sonekinin listelenmektedir:

| Özellik veri türü | Son eki |
|:--- |:--- |
| Dize |_Yanları |
| Boole değeri |_B |
| Çift |_D |
| Tarih/saat |_T |
| GUID |_g |

Merhaba kayıt türü hello yeni kayıt için zaten var olup üzerinde her özelliği için günlük analizi kullanan hello veri türüne bağlıdır.

* Günlük analizi Hello kayıt türü mevcut değilse yeni bir tane oluşturur. Günlük analizi hello JSON türü çıkarımı toodetermine hello veri türü hello yeni kayıt için her bir özellik için kullanır.
* Merhaba kayıt türü mevcut değilse, günlük analizi toocreate varolan özelliğe göre yeni bir kayıt çalışır. Merhaba hello yeni kayıttaki bir özellik için veri türü değil eşleşen ve olamaz dönüştürülmüş toohello türü mevcut olması veya hello kaydı varolmayan bir özellik içerir, günlük analizi yeni bir özellik oluşturur, hello ilgili soneki olmaz.

Örneğin, bir kayıt üç özellik ile bu gönderimi giriş oluşturursunuz **number_d**, **boolean_b**, ve **string_s**:

![Kayıt örneği 1](media/log-analytics-data-collector-api/record-01.png)

Ardından tüm değerleri dize olarak biçimlendirilmiş bu sonraki giriş gönderdiyseniz hello özellikleri değişmediği. Bu değerler dönüştürülmüş tooexisting veri türleri olabilir:

![Örnek kaydı 2](media/log-analytics-data-collector-api/record-02.png)

Ancak, daha sonra bu sonraki gönderme yaptıysanız, günlük analizi yeni özellikleri hello oluşturacak **boolean_d** ve **string_d**. Bu değerleri dönüştürülemiyor:

![Örnek kayıt 3](media/log-analytics-data-collector-api/record-03.png)

Ardından hello kayıt türü oluşturulmadan önce girişi, aşağıdaki hello gönderdiyseniz, günlük analizi üç özellik ile bir kayıt oluşturacak **başarı sayısı**, **boolean_s**, ve **string_s**. Bu girdiye hello ilk değerlerin her birini bir dize olarak biçimlendirilmiş:

![Örnek kayıt 4](media/log-analytics-data-collector-api/record-04.png)

## <a name="data-limits"></a>Veri sınırları
Merhaba veri toohello Log Analytics verisi toplama API gönderilen geçici bazı kısıtlamalar vardır.

* Post tooLog Analytics Veri Toplayıcı API başına en fazla 30 MB. Tek bir posta için boyut sınırı budur. 30 MB aşıyor tek bir post verilerden Merhaba, toosmaller boyuta sahip verileri öbekleri ve eş zamanlı gönderme hello bölme durumunda.
* En fazla 32 KB sınırını alan değerleri için. Merhaba alan değeri 32 KB'den büyükse hello verileri kesilecek.
* Önerilen alanı sayısı için belirli bir türde 50'dir. Kullanılabilirlik ve arama deneyimi perspektifinden pratik sınır budur.  

## <a name="return-codes"></a>Dönüş kodları
HTTP durum kodu 200 Hello bu hello istek işleme için alınan anlamına gelir. Bu, o hello işlemi başarıyla tamamlandı gösterir.

Bu tabloda hello eksiksiz hello hizmet döndürebilir durum kodları listelenmektedir:

| Kod | Durum | Hata kodu | Açıklama |
|:--- |:--- |:--- |:--- |
| 200 |TAMAM | |Merhaba isteği başarıyla kabul edildi. |
| 400 |Hatalı istek |InactiveCustomer |Merhaba çalışma kapatıldı. |
| 400 |Hatalı istek |InvalidApiVersion |Belirttiğiniz hello API sürümü hello hizmeti tarafından tanınmadı. |
| 400 |Hatalı istek |InvalidCustomerId |Belirtilen hello çalışma alanı kimliği geçersiz. |
| 400 |Hatalı istek |InvalidDataFormat |Geçersiz JSON gönderildi. Merhaba yanıt gövdesi nasıl tooresolve hello hata hakkında daha fazla bilgi içerebilir. |
| 400 |Hatalı istek |InvalidLogType |Kapsanan özel karakter veya sayı belirtilen Hello günlük türü. |
| 400 |Hatalı istek |MissingApiVersion |Merhaba API sürümü belirtilmedi. |
| 400 |Hatalı istek |MissingContentType |Merhaba içerik türü belirtilmedi. |
| 400 |Hatalı istek |MissingLogType |Merhaba, değer günlük türü belirtilmedi gereklidir. |
| 400 |Hatalı istek |UnsupportedContentType |Merhaba içerik türü çok ayarlanmamış**uygulama/json**. |
| 403 |Yasak |InvalidAuthorization |Merhaba hizmet tooauthenticate hello isteği başarısız oldu. Bu hello çalışma alanı kimliği ve bağlantı anahtarı geçerli olduğundan emin olun. |
| 404 |Bulunamadı | | Sağlanan hello URL yanlış ya da hello isteği çok büyük. |
| 429 |Çok fazla istek | | Merhaba hizmet hesabınızdan veri hacmi yüksek yaşıyor. Lütfen hello isteği daha sonra yeniden deneyin. |
| 500 |İç sunucu hatası |UnspecifiedError |Merhaba hizmeti bir iç hatayla karşılaştı. Lütfen hello isteği yeniden deneyin. |
| 503 |Hizmet kullanılamıyor |ServiceUnavailable |Merhaba Hizmet şu anda kullanılamıyor tooreceive isteği sayısıdır. Lütfen isteğinizi yeniden deneyin. |

## <a name="query-data"></a>Verileri sorgulama
Merhaba günlük analizi HTTP veri toplayıcı API, arama ile kayıt tarafından gönderilen tooquery veri **türü** diğer bir deyişle eşit toohello **LogType** , belirttiğiniz değer eklenmiş olan **_CL**. Örneğin, kullandığınız **MyCustomLog**, tüm kayıtları döndürecekti sonra **türü MyCustomLog_CL =**.

>[!NOTE]
> Çalışma alanınızı yükseltilmiş toohello yüklediyse [yeni günlük analizi sorgu dili](log-analytics-log-search-upgrade.md), sorgu yukarıda hello toohello aşağıdaki değişeceğinden sonra.

> `MyCustomLog_CL`

## <a name="sample-requests"></a>Örnek istek
Merhaba sonraki bölümlerde, nasıl örnekleri bulabilirsiniz toosubmit veri toohello günlük analizi HTTP veri toplayıcı API farklı programlama dillerini kullanarak.

Her bir örnek için tooset hello değişkenleri hello authorization üstbilgisi için bu adımları uygulayın:

1. Merhaba Hello Operations Management Suite Portalı'nda seçin **ayarları** döşeme ve hello ardından **bağlı kaynakları** sekmesi.
2. sağ toohello **çalışma alanı kimliği**hello Kopyala simgesini seçin ve hello kimliği hello hello değeri olarak yapıştırın **Müşteri Kimliği** değişkeni.
3. sağ toohello **birincil anahtar**hello Kopyala simgesini seçin ve hello kimliği hello hello değeri olarak yapıştırın **paylaşılan anahtar** değişkeni.

Alternatif olarak, hello değişkenleri hello günlük türü ve JSON verileri için değiştirebilirsiniz.

### <a name="powershell-sample"></a>PowerShell örnek
```
# Replace with your Workspace ID
$CustomerId = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"  

# Replace with your Primary Key
$SharedKey = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"

# Specify hello name of hello record type that you'll be creating
$LogType = "MyRecordType"

# Specify a field with hello created time for hello records
$TimeStampField = "DateValue"


# Create two records with hello same set of properties toocreate
$json = @"
[{  "StringValue": "MyString1",
    "NumberValue": 42,
    "BooleanValue": true,
    "DateValue": "2016-05-12T20:00:00.625Z",
    "GUIDValue": "9909ED01-A74C-4874-8ABF-D2678E3AE23D"
},
{   "StringValue": "MyString2",
    "NumberValue": 43,
    "BooleanValue": false,
    "DateValue": "2016-05-12T20:00:00.625Z",
    "GUIDValue": "8809ED01-A74C-4874-8ABF-D2678E3AE23D"
}]
"@

# Create hello function toocreate hello authorization signature
Function Build-Signature ($customerId, $sharedKey, $date, $contentLength, $method, $contentType, $resource)
{
    $xHeaders = "x-ms-date:" + $date
    $stringToHash = $method + "`n" + $contentLength + "`n" + $contentType + "`n" + $xHeaders + "`n" + $resource

    $bytesToHash = [Text.Encoding]::UTF8.GetBytes($stringToHash)
    $keyBytes = [Convert]::FromBase64String($sharedKey)

    $sha256 = New-Object System.Security.Cryptography.HMACSHA256
    $sha256.Key = $keyBytes
    $calculatedHash = $sha256.ComputeHash($bytesToHash)
    $encodedHash = [Convert]::ToBase64String($calculatedHash)
    $authorization = 'SharedKey {0}:{1}' -f $customerId,$encodedHash
    return $authorization
}


# Create hello function toocreate and post hello request
Function Post-OMSData($customerId, $sharedKey, $body, $logType)
{
    $method = "POST"
    $contentType = "application/json"
    $resource = "/api/logs"
    $rfc1123date = [DateTime]::UtcNow.ToString("r")
    $contentLength = $body.Length
    $signature = Build-Signature `
        -customerId $customerId `
        -sharedKey $sharedKey `
        -date $rfc1123date `
        -contentLength $contentLength `
        -fileName $fileName `
        -method $method `
        -contentType $contentType `
        -resource $resource
    $uri = "https://" + $customerId + ".ods.opinsights.azure.com" + $resource + "?api-version=2016-04-01"

    $headers = @{
        "Authorization" = $signature;
        "Log-Type" = $logType;
        "x-ms-date" = $rfc1123date;
        "time-generated-field" = $TimeStampField;
    }

    $response = Invoke-WebRequest -Uri $uri -Method $method -ContentType $contentType -Headers $headers -Body $body -UseBasicParsing
    return $response.StatusCode

}

# Submit hello data toohello API endpoint
Post-OMSData -customerId $customerId -sharedKey $sharedKey -body ([System.Text.Encoding]::UTF8.GetBytes($json)) -logType $logType  
```

### <a name="c-sample"></a>C# örneği
```
using System;
using System.Net;
using System.Net.Http;
using System.Net.Http.Headers;
using System.Security.Cryptography;
using System.Text;
using System.Threading.Tasks;

namespace OIAPIExample
{
    class ApiExample
    {
        // An example JSON object, with key/value pairs
        static string json = @"[{""DemoField1"":""DemoValue1"",""DemoField2"":""DemoValue2""},{""DemoField3"":""DemoValue3"",""DemoField4"":""DemoValue4""}]";

        // Update customerId tooyour Operations Management Suite workspace ID
        static string customerId = "xxxxxxxx-xxx-xxx-xxx-xxxxxxxxxxxx";

        // For sharedKey, use either hello primary or hello secondary Connected Sources client authentication key   
        static string sharedKey = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx";

        // LogName is name of hello event type that is being submitted tooLog Analytics
        static string LogName = "DemoExample";

        // You can use an optional field toospecify hello timestamp from hello data. If hello time field is not specified, Log Analytics assumes hello time is hello message ingestion time
        static string TimeStampField = "";

        static void Main()
        {
            // Create a hash for hello API signature
            var datestring = DateTime.UtcNow.ToString("r");
            string stringToHash = "POST\n" + json.Length + "\napplication/json\n" + "x-ms-date:" + datestring + "\n/api/logs";
            string hashedString = BuildSignature(stringToHash, sharedKey);
            string signature = "SharedKey " + customerId + ":" + hashedString;

            PostData(signature, datestring, json);
        }

        // Build hello API signature
        public static string BuildSignature(string message, string secret)
        {
            var encoding = new System.Text.ASCIIEncoding();
            byte[] keyByte = Convert.FromBase64String(secret);
            byte[] messageBytes = encoding.GetBytes(message);
            using (var hmacsha256 = new HMACSHA256(keyByte))
            {
                byte[] hash = hmacsha256.ComputeHash(messageBytes);
                return Convert.ToBase64String(hash);
            }
        }

        // Send a request toohello POST API endpoint
        public static void PostData(string signature, string date, string json)
        {
            try
            {
                string url = "https://" + customerId + ".ods.opinsights.azure.com/api/logs?api-version=2016-04-01";

                System.Net.Http.HttpClient client = new System.Net.Http.HttpClient();
                client.DefaultRequestHeaders.Add("Accept", "application/json");
                client.DefaultRequestHeaders.Add("Log-Type", LogName);
                client.DefaultRequestHeaders.Add("Authorization", signature);
                client.DefaultRequestHeaders.Add("x-ms-date", date);
                client.DefaultRequestHeaders.Add("time-generated-field", TimeStampField);

                System.Net.Http.HttpContent httpContent = new StringContent(json, Encoding.UTF8);
                httpContent.Headers.ContentType = new MediaTypeHeaderValue("application/json");
                Task<System.Net.Http.HttpResponseMessage> response = client.PostAsync(new Uri(url), httpContent);

                System.Net.Http.HttpContent responseContent = response.Result.Content;
                string result = responseContent.ReadAsStringAsync().Result;
                Console.WriteLine("Return Result: " + result);
            }
            catch (Exception excep)
            {
                Console.WriteLine("API Post Exception: " + excep.Message);
            }
        }
    }
}

```

### <a name="python-sample"></a>Python örneği
```
import json
import requests
import datetime
import hashlib
import hmac
import base64

# Update hello customer ID tooyour Operations Management Suite workspace ID
customer_id = 'xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx'

# For hello shared key, use either hello primary or hello secondary Connected Sources client authentication key   
shared_key = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"

# hello log type is hello name of hello event that is being submitted
log_type = 'WebMonitorTest'

# An example JSON web monitor object
json_data = [{
   "slot_ID": 12345,
    "ID": "5cdad72f-c848-4df0-8aaa-ffe033e75d57",
    "availability_Value": 100,
    "performance_Value": 6.954,
    "measurement_Name": "last_one_hour",
    "duration": 3600,
    "warning_Threshold": 0,
    "critical_Threshold": 0,
    "IsActive": "true"
},
{   
    "slot_ID": 67890,
    "ID": "b6bee458-fb65-492e-996d-61c4d7fbb942",
    "availability_Value": 100,
    "performance_Value": 3.379,
    "measurement_Name": "last_one_hour",
    "duration": 3600,
    "warning_Threshold": 0,
    "critical_Threshold": 0,
    "IsActive": "false"
}]
body = json.dumps(json_data)

#####################
######Functions######  
#####################

# Build hello API signature
def build_signature(customer_id, shared_key, date, content_length, method, content_type, resource):
    x_headers = 'x-ms-date:' + date
    string_to_hash = method + "\n" + str(content_length) + "\n" + content_type + "\n" + x_headers + "\n" + resource
    bytes_to_hash = bytes(string_to_hash).encode('utf-8')  
    decoded_key = base64.b64decode(shared_key)
    encoded_hash = base64.b64encode(hmac.new(decoded_key, bytes_to_hash, digestmod=hashlib.sha256).digest())
    authorization = "SharedKey {}:{}".format(customer_id,encoded_hash)
    return authorization

# Build and send a request toohello POST API
def post_data(customer_id, shared_key, body, log_type):
    method = 'POST'
    content_type = 'application/json'
    resource = '/api/logs'
    rfc1123date = datetime.datetime.utcnow().strftime('%a, %d %b %Y %H:%M:%S GMT')
    content_length = len(body)
    signature = build_signature(customer_id, shared_key, rfc1123date, content_length, method, content_type, resource)
    uri = 'https://' + customer_id + '.ods.opinsights.azure.com' + resource + '?api-version=2016-04-01'

    headers = {
        'content-type': content_type,
        'Authorization': signature,
        'Log-Type': log_type,
        'x-ms-date': rfc1123date
    }

    response = requests.post(uri,data=body, headers=headers)
    if (response.status_code >= 200 and response.status_code <= 299):
        print 'Accepted'
    else:
        print "Response code: {}".format(response.status_code)

post_data(customer_id, shared_key, body, log_type)
```

## <a name="next-steps"></a>Sonraki adımlar
- Kullanım hello [günlük arama API](log-analytics-log-search-api.md) hello günlük analizi depodan tooretrieve veri.
