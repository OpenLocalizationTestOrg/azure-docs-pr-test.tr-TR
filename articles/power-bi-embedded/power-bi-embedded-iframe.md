---
title: Power BI Embedded REST ile aaaHow toouse | Microsoft Docs
description: "Bilgi nasıl toouse Power BI Embedded REST ile "
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 8bcef780-cca0-4f30-9a9b-9daa1a7ae865
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 02/06/2017
ms.author: asaxton
ms.openlocfilehash: 98057724e60ba868f9c93de8c50383569eb8852d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-power-bi-embedded-with-rest"></a>Nasıl toouse Power BI Embedded REST ile

## <a name="power-bi-embedded-what-it-is-and-what-its-for"></a>Power BI Embedded: Nedir ve ne işe yaradığını

Power BI Embedded genel bakış hello resmi açıklanan [Power BI Embedded site](https://azure.microsoft.com/services/power-bi-embedded/), ancak REST ile kullanma hakkında ayrıntılar hello içine ulaşmadan hızlı bir göz atalım.

Gerçekten oldukça basit. toouse hello dinamik veri Görselleştirmelerini isteyebilirsiniz [Power BI](https://powerbi.microsoft.com) kendi uygulamanızda.

Özel uygulamaların çoğu toodeliver hello veri mutlaka kendi kuruluşunuzdaki kullanıcılar kendi müşteriler için gerekir. Şirket A ve B şirketi için bazı hizmet sunma, örneğin, Şirket A kullanıcılar yalnızca veri kendi Şirket A'daki görmeniz gerekir Diğer bir deyişle, hello çoklu kiracı hello teslimat için gereklidir.

Merhaba özel uygulama, form kimlik doğrulama, temel kimlik doğrulama vb. gibi kendi kimlik doğrulama yöntemleri de sunumu.. Ardından, çözüm katıştırma hello var olan bu kimlik doğrulama yöntemleri ile güvenli bir şekilde işbirliği gerekir. Ayrıca kullanıcılar toobe mümkün toouse için gerekli olan bu ISV uygulamaları olmadan hello fazladan satınalma ya da bir Power BI aboneliği lisans.

 **Power BI Embedded** tam olarak bu tür senaryoları için tasarlanmıştır. Bu nedenle, biz Bu hızlı giriş hello yolu dışında sahip olduğunuza göre şimdi bazı ayrıntılar alın

Merhaba .NET kullanabilirsiniz \(C#) veya Node.js SDK'sı, tooeasily Power BI Embedded ile uygulamanızı oluşturun. Ancak, bu makalede, HTTP akışı hakkında açıklayacağız \(dahil AuthN) SDK'ları olmadan Power BI. Bu akış anlama, uygulamanızı oluşturabilir **herhangi bir programlama dili ile**, ve Power BI Embedded hello özünü derine anlayabilirsiniz.

## <a name="create-power-bi-workspace-collection-and-get-access-key-provisioning"></a>Power BI oluşturma çalışma alanı koleksiyonu ve get erişim tuşu \(hazırlama)

Power BI Embedded hello Azure Hizmetleri biridir. Yalnızca hello Azure Portal kullanan ISV kullanım ücretleri için ücret \(saatlik kullanıcı oturumu başına), ve doldurulmamış veya hatta görünümleri hello rapor olmayan hello kullanıcının gerektiren bir Azure aboneliği.
Bizim uygulama geliştirme başlatmadan önce biz hello oluşturmalısınız **Power BI çalışma alanı koleksiyonu** Azure portalını kullanarak.

Hello çalışma (Kiracı) her müşteri için Power BI Embedded her çalışma alanıdır ve her çalışma alanı koleksiyonu birçok çalışma alanları ekleyebiliriz. Merhaba aynı erişim tuşu her çalışma alanı koleksiyonu kullanılır. İçinde etkisi, Power BI Embedded için hello güvenlik sınırı hello çalışma koleksiyonudur.

![](media/power-bi-embedded-iframe/create-workspace.png)

Merhaba çalışma alanı koleksiyonu oluşturma sona erdiğinde hello erişim tuşunu Azure Portal'dan kopyalayın.

![](media/power-bi-embedded-iframe/copy-access-key.png)

> [!NOTE]
> Biz de hello çalışma alanı koleksiyonu sağlayabilir ve erişim anahtarı REST API aracılığıyla alın. toolearn daha, fazla [Power BI kaynak sağlayıcısı API'leri](https://msdn.microsoft.com/library/azure/mt712306.aspx).

## <a name="create-pbix-file-with-power-bi-desktop"></a>Power BI Desktop ile .pbix dosyası oluşturma

Ardından, biz hello veri bağlantısı ve katıştırılmış raporları toobe oluşturmanız gerekir.
Bu görev için programlama veya kod yoktur. Yalnızca Power BI Desktop kullanırız.
Bu makalede, biz hello ayrıntıları Git olmaz toouse Power BI Desktop. Bazı burada yardıma gereksinim duyarsanız, bkz: [Power BI Desktop ile çalışmaya başlama](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/). Bizim örneğimizde, yalnızca hello kullanacağız [Retail Analysis örnek](https://powerbi.microsoft.com/documentation/powerbi-sample-datasets/).

![](media/power-bi-embedded-iframe/power-bi-desktop-1.png)

## <a name="create-a-power-bi-workspace"></a>Power BI çalışma alanı oluşturma

Merhaba sağlama tüm yapılır, REST API'leri aracılığıyla hello çalışma alanı koleksiyonu, bir müşterinin çalışma oluşturmayı başlayalım. Merhaba aşağıdaki HTTP POST isteği (REST) hello yeni çalışma bizim mevcut çalışma alanı koleksiyonu oluşturuyor. Merhaba budur [POST çalışma API](https://msdn.microsoft.com/library/azure/mt711503.aspx). Bizim örneğimizde, hello çalışma alanı koleksiyonu adı olan **mypbiapp**. Yalnızca size daha önce kopyaladığınız, hello erişim tuşu ayarlarız olarak **AppKey**. Çok basit kimlik doğrulama kadar!

**HTTP isteği**

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces
Authorization: AppKey MpaUgrTv5e...
```

**HTTP yanıtı**

```
HTTP/1.1 201 Created
Content-Type: application/json; odata.metadata=minimal; odata.streaming=true
Location: https://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces
RequestId: 4220d385-2fb3-406b-8901-4ebe11a5f6da

{
  "@odata.context": "http://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/$metadata#workspaces/$entity",
  "workspaceId": "32960a09-6366-4208-a8bb-9e0678cdbb9d",
  "workspaceCollectionName": "mypbiapp"
}
```

döndürülen hello **Workspaceıd** sonraki API çağrıları aşağıdaki hello için kullanılır. Bu değer uygulamamız korumanız gerekir.

## <a name="import-pbix-file-into-hello-workspace"></a>.Pbix dosyasını hello çalışma alanınıza alın

Bir çalışma alanındaki her bir raporun tooa tek Power BI Desktop dosyası bir veri kümesi ile karşılık gelen \(veri kaynağı ayarları dahil). Biz hello kodda aşağıda gösterildiği gibi bizim .pbix dosyası toohello çalışma içeri aktarabilirsiniz. Gördüğünüz gibi biz hello İkili MIME çok bölümlü http kullanarak .pbix dosyasının karşıya yükleyebilirsiniz.

Merhaba URI parça **32960a09-6366-4208-a8bb-9e0678cdbb9d** hello Workspaceıd ve sorgu parametresi **datasetDisplayName** hello veri kümesi adı toocreate değil. oluşturulan hello dataset tutan ilgili tüm verileri yapıları .pbix dosyasında alınan verileri gibi hello işaretçi toohello veri kaynağı, vb...

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports?datasetDisplayName=mydataset01
Authorization: AppKey MpaUgrTv5e...
Content-Type: multipart/form-data; boundary="A300testx"

--A300testx
Content-Disposition: form-data

{hello content (binary) of .pbix file}
--A300testx--
```

Bu görevi Al bir süre çalışabilir. Tamamlandığında, uygulamamız hello görev durumu alma kimliğini kullanarak sorabilirsiniz. Bizim örneğimizde, hello alma kimliğidir **4eec64dd-533b-47c3-a72c-6508ad854659**.

```
HTTP/1.1 202 Accepted
Content-Type: application/json; charset=utf-8
Location: https://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports/4eec64dd-533b-47c3-a72c-6508ad854659?tenantId=myorg
RequestId: 658bd6b4-b68d-4ec3-8818-2a94266dc220

{"id":"4eec64dd-533b-47c3-a72c-6508ad854659"}
```

Merhaba aşağıdaki bu içeri aktarma kimliği kullanarak durumunu soran:

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports/4eec64dd-533b-47c3-a72c-6508ad854659
Authorization: AppKey MpaUgrTv5e...
```

Merhaba görev tam değilse, HTTP yanıtı hello şöyle olabilir:

```
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
RequestId: 614a13a5-4de7-43e8-83c9-9cd225535136

{
  "id": "4eec64dd-533b-47c3-a72c-6508ad854659",
  "importState": "Publishing",
  "createdDateTime": "2016-07-19T07:36:06.227",
  "updatedDateTime": "2016-07-19T07:36:06.227",
  "name": "mydataset01"
}
```

Merhaba görev tamamlandığında, hello HTTP yanıtı şuna daha fazla olabilir:

```
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
RequestId: eb2c5a85-4d7d-4cc2-b0aa-0bafee4b1606

{
  "id": "4eec64dd-533b-47c3-a72c-6508ad854659",
  "importState": "Succeeded",
  "createdDateTime": "2016-07-19T07:36:06.227",
  "updatedDateTime": "2016-07-19T07:36:06.227",
  "reports": [
    {
      "id": "2027efc6-a308-4632-a775-b9a9186f087c",
      "name": "mydataset01",
      "webUrl": "https://app.powerbi.com/reports/2027efc6-a308-4632-a775-b9a9186f087c",
      "embedUrl": "https://app.powerbi.com/appTokenReportEmbed?reportId=2027efc6-a308-4632-a775-b9a9186f087c"
    }
  ],
  "datasets": [
    {
      "id": "458e0451-7215-4029-80b3-9627bf3417b0",
      "name": "mydataset01",
      "tables": [
      ],
      "webUrl": "https://app.powerbi.com/datasets/458e0451-7215-4029-80b3-9627bf3417b0"
    }
  ],
  "name": "mydataset01"
}
```

## <a name="data-source-connectivity-and-multi-tenancy-of-data"></a>Veri kaynağı bağlantısı \(ve verilerin çok kiracılı)

Neredeyse tüm .pbix dosyasında hello yapılarının bizim çalışma alanına alınırken, veri kaynaklarına hello kimlik bilgilerini değildir. Kullanırken, sonuç olarak, **DirectQuery modu**, hello yerleşik rapor düzgün gösterilemiyor. Ancak kullanırken **alma modunu**, biz hello varolan alınan verileri kullanarak hello raporu görüntüleyebilirsiniz. Böyle bir durumda, biz hello kimlik bilgisi hello REST çağrıları aşağıdaki adımları kullanarak ayarlamanız gerekir.

İlk olarak, biz hello ağ geçidi datasource almanız gerekir. Merhaba dataset biliyoruz **kimliği** hello önceden kimliği döndürülür.

**HTTP isteği**

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/datasets/458e0451-7215-4029-80b3-9627bf3417b0/Default.GetBoundGatewayDatasources
Authorization: AppKey MpaUgrTv5e...
```

**HTTP yanıtı**

```
GET HTTP/1.1 200 OK
Content-Type: application/json; odata.metadata=minimal; odata.streaming=true
RequestId: 574b0b18-a6fa-46a6-826c-e65840cf6e15

{
  "@odata.context": "http://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/$metadata#gatewayDatasources",
  "value": [
    {
      "id": "5f7ee2e7-4851-44a1-8b75-3eb01309d0ea",
      "gatewayId": "ca17e77f-1b51-429b-b059-6b3e3e9685d1",
      "datasourceType": "Sql",
      "connectionDetails": "{\"server\":\"testserver.database.windows.net\",\"database\":\"testdb01\"}"
    }
  ]
}
```

Hello kullanarak döndürülen ağ geçidi kimliği ve veri kaynağı kimliği \(hello önceki bkz **gatewayId** ve **kimliği** hello sonuç döndürdü), bu veri kaynağının hello kimlik bilgisi gibi değişiklik yapabilirsiniz:

**HTTP isteği**

```
PATCH https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/gateways/ca17e77f-1b51-429b-b059-6b3e3e9685d1/datasources/5f7ee2e7-4851-44a1-8b75-3eb01309d0ea
Authorization: AppKey MpaUgrTv5e...
Content-Type: application/json; charset=utf-8

{
  "credentialType": "Basic",
  "basicCredentials": {
    "username": "demouser",
    "password": "P@ssw0rd"
  }
}
```

**HTTP yanıtı**

```
HTTP/1.1 200 OK
Content-Type: application/octet-stream
RequestId: 0e533c13-266a-4a9d-8718-fdad90391099
```

Üretimde biz hello farklı bir bağlantı dizesi REST API kullanarak her çalışma alanı için de ayarlayabilirsiniz. \(yani, biz hello veritabanı her müşteri için ayırabilirsiniz.)

Merhaba aşağıdaki hello bağlantı dizesi REST aracılığıyla veri kaynağının değiştiriyor.

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/datasets/458e0451-7215-4029-80b3-9627bf3417b0/Default.SetAllConnections
Authorization: AppKey MpaUgrTv5e...
Content-Type: application/json; charset=utf-8

{
  "connectionString": "data source=testserver02.database.windows.net;initial catalog=testdb02;persist security info=True;encrypt=True;trustservercertificate=False"
}
```

Veya, biz hello veri bir rapordaki her kullanıcı için ayrı ve biz satır düzeyi güvenlik Power BI Embedded kullanabilirsiniz. As a Result, biz aynı .pbix her müşteri raporla sağlayabilirsiniz \(UI, vb.) ve farklı veri kaynakları.

> [!NOTE]
> Kullanıyorsanız, **alma modunu** yerine **DirectQuery modu**, hiçbir şekilde toorefresh modeli API aracılığıyla yoktur. Ve Power BI ağ geçidi üzerinden şirket içi veri kaynakları henüz Power BI Embedded içinde desteklenmiyor. Ancak, gerçekten tookeep hello sayfasındaki tercih edersiniz [Power BI blog](https://powerbi.microsoft.com/blog/) yenilikler ve yakında gelecek için serbest bırakır.

## <a name="authentication-and-hosting-embedding-reports-in-our-web-page"></a>Kimlik doğrulaması ve web sayfamızı (katıştırma) raporlarında barındırma

İçinde önceki REST API Merhaba, hello erişim tuşu kullanırız **AppKey** hello authorization üstbilgisi olarak kendisini. Bu çağrıları hello arka uç sunucu tarafında ele alınması için güvenlidir.

Ancak, biz web sayfamızı hello rapor ekleme, bu tür güvenlik bilgileri JavaScript kullanarak ele alınması \(ön uç). Ardından hello kimlik doğrulaması üstbilgi değeri güvenli hale getirilmelidir. Bizim erişim tuşu kötü amaçlı kullanıcı ya da kötü amaçlı kod tarafından bulunmuşsa, bunlar bu anahtarı kullanarak herhangi bir işlem çağırabilirsiniz.

Biz web sayfamızı hello rapor ekleme, biz hello hesaplanan belirteci erişim tuşu yerine kullanmalısınız **AppKey**. Uygulamamız hello OAuth Json Web belirteci oluşturmanız gerekir \(JWT) hello talep ve hello hesaplanan dijital imzadan oluşur. Aşağıda gösterildiği gibi bu OAuth JWT nokta ayrılmış kodlu bir dize belirteçleri gereklidir.

![](media/power-bi-embedded-iframe/oauth-jwt.png)

İlk olarak, biz daha sonra imzalı hello giriş değeri hazırlamanız gerekir. Bu değer hello Base64 ile kodlanmış URL'si (rfc4648) json aşağıdaki hello dizesidir ve bunlar hello noktayla ayrılmış \(.) karakter. Daha sonra nasıl tooget hello rapor kimliği açıklayacağız.

> [!NOTE]
> Biz toouse Power BI Embedded ile satır düzeyi güvenlik (RLS) isterseniz, biz de belirtmeniz gerekir **kullanıcıadı** ve **rolleri** hello taleplerdeki.

```
{
  "typ":"JWT",
  "alg":"HS256"
}
```

```
{
  "wid":"{workspace id}",
  "rid":"{report id}",
  "wcn":"{workspace collection name}",
  "iss":"PowerBISDK",
  "ver":"0.2.0",
  "aud":"https://analysis.windows.net/powerbi/api",
  "nbf":{start time of token expiration},
  "exp":{end time of token expiration}
}
```

Ardından, biz hello base64 kodlu dize HMAC oluşturmalısınız \(hello imza) SHA256 algoritmasını ile. Bu imzalı giriş hello önceki dize değeridir.

Son olarak, biz hello giriş değeri ve imza dize nokta kullanarak birleştirmeniz gerekir \(.) karakter. Tamamlanan Merhaba, rapor hello katıştırmak için hello uygulama belirteci dizesidir. Merhaba uygulama belirteci kötü niyetli bir kullanıcı tarafından bulunan olsa bile, bunlar hello özgün erişim anahtarı alınamıyor. Bu uygulama belirteci hızlı bir şekilde sona erecek.

Bir PHP örnek için aşağıdaki adımları şöyledir:

```
<?php
// 1. power bi access key
$accesskey = "MpaUgrTv5e...";

// 2. construct input value
$token1 = "{" .
  "\"typ\":\"JWT\"," .
  "\"alg\":\"HS256\"" .
  "}";
$token2 = "{" .
  "\"wid\":\"32960a09-6366-4208-a8bb-9e0678cdbb9d\"," . // workspace id
  "\"rid\":\"2027efc6-a308-4632-a775-b9a9186f087c\"," . // report id
  "\"wcn\":\"mypbiapp\"," . // workspace collection name
  "\"iss\":\"PowerBISDK\"," .
  "\"ver\":\"0.2.0\"," .
  "\"aud\":\"https://analysis.windows.net/powerbi/api\"," .
  "\"nbf\":" . date("U") . "," .
  "\"exp\":" . date("U" , strtotime("+1 hour")) .
  "}";
$inputval = rfc4648_base64_encode($token1) .
  "." .
  rfc4648_base64_encode($token2);

// 3. get encoded signature
$hash = hash_hmac("sha256",
    $inputval,
    $accesskey,
    true);
$sig = rfc4648_base64_encode($hash);

// 4. show result (which is hello apptoken)
$apptoken = $inputval . "." . $sig;
echo($apptoken);

// helper functions
function rfc4648_base64_encode($arg) {
  $res = $arg;
  $res = base64_encode($res);
  $res = str_replace("/", "_", $res);
  $res = str_replace("+", "-", $res);
  $res = rtrim($res, "=");
  return $res;
}
?>
```

## <a name="finally-embed-hello-report-into-hello-web-page"></a>Son olarak, hello web sayfasına hello rapor ekleme

Bizim rapor katıştırmak için biz hello almalısınız url ve rapor katıştırmak **kimliği** REST API aşağıdaki hello kullanarak.

**HTTP isteği**

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/reports
Authorization: AppKey MpaUgrTv5e...
```

**HTTP yanıtı**

```
HTTP/1.1 200 OK
Content-Type: application/json; odata.metadata=minimal; odata.streaming=true
RequestId: d4099022-405b-49d3-b3b7-3c60cf675958

{
  "@odata.context": "http://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/$metadata#reports",
  "value": [
    {
      "id": "2027efc6-a308-4632-a775-b9a9186f087c",
      "name": "mydataset01",
      "webUrl": "https://app.powerbi.com/reports/2027efc6-a308-4632-a775-b9a9186f087c",
      "embedUrl": "https://embedded.powerbi.com/appTokenReportEmbed?reportId=2027efc6-a308-4632-a775-b9a9186f087c",
      "isFromPbix": false
    }
  ]
}
```

Biz hello rapor web uygulamamız hello önceki uygulama belirteci kullanılarak eklenebilir.
Biz hello sonraki örnek kodu bakarsanız, hello eski parçası olan hello hello önceki örnek ile aynı. Merhaba ikinci bölümünde, bu örnek hello gösterir **embedUrl** \(hello önceki sonuçları görmek) IFRAME hello ve hello uygulama belirteci hello IFRAME gönderme.

> [!NOTE]
> Toochange hello rapor kimliği değeri tooone kendi gerekir. Ayrıca, içerik yönetimi sistemimizde tooa hata, hello IFRAME etiketi hello kod örneğinde tam anlamıyla okunur. Bu örnek kodu kopyalayıp tutulabilir hello metin hello etiketinden kaldırın.

```
    <?php
    // 1. power bi access key
    $accesskey = "MpaUgrTv5e...";

    // 2. construct input value
    $token1 = "{" .
      "\"typ\":\"JWT\"," .
      "\"alg\":\"HS256\"" .
      "}";
    $token2 = "{" .
      "\"wid\":\"32960a09-6366-4208-a8bb-9e0678cdbb9d\"," . // workspace id
      "\"rid\":\"2027efc6-a308-4632-a775-b9a9186f087c\"," . // report id
      "\"wcn\":\"mypbiapp\"," . // workspace collection name
      "\"iss\":\"PowerBISDK\"," .
      "\"ver\":\"0.2.0\"," .
      "\"aud\":\"https://analysis.windows.net/powerbi/api\"," .
      "\"nbf\":" . date("U") . "," .
      "\"exp\":" . date("U" , strtotime("+1 hour")) .
      "}";
    $inputval = rfc4648_base64_encode($token1) .
      "." .
      rfc4648_base64_encode($token2);

    // 3. get encoded signature value
    $hash = hash_hmac("sha256",
        $inputval,
        $accesskey,
        true);
    $sig = rfc4648_base64_encode($hash);

    // 4. get apptoken
    $apptoken = $inputval . "." . $sig;

    // helper functions
    function rfc4648_base64_encode($arg) {
      $res = $arg;
      $res = base64_encode($res);
      $res = str_replace("/", "_", $res);
      $res = str_replace("+", "-", $res);
      $res = rtrim($res, "=");
      return $res;
    }
    ?>
    <!DOCTYPE html>
    <html>
    <head>
      <meta charset="utf-8" />
      <meta http-equiv="X-UA-Compatible" content="IE=edge">
      <title>Test page</title>
      <meta name="viewport" content="width=device-width, initial-scale=1">
    </head>
    <body>
      <button id="btnView">View Report !</button>
      <div id="divView">
        <**REMOVE THIS CAPPED TEXT IF COPIED** iframe id="ifrTile" width="100%" height="400"></iframe>
      </div>
      <script>
        (function () {
          document.getElementById('btnView').onclick = function() {
            var iframe = document.getElementById('ifrTile');
            iframe.src = 'https://embedded.powerbi.com/appTokenReportEmbed?reportId=2027efc6-a308-4632-a775-b9a9186f087c';
            iframe.onload = function() {
              var msgJson = {
                action: "loadReport",
                accessToken: "<?=$apptoken?>",
                height: 500,
                width: 722
              };
              var msgTxt = JSON.stringify(msgJson);
              iframe.contentWindow.postMessage(msgTxt, "*");
            };
          };
        }());
      </script>
    </body>
```

Ve bizim sonuç şöyledir:

![](media/power-bi-embedded-iframe/view-report.png)

Şu anda Power BI Embedded yalnızca hello rapor hello IFRAME gösterir. Merhaba üzerinde ancak tutmak bir göz [Power BI Blog](https://powerbi.microsoft.com/blog/). Gelecekteki geliştirmeleri, yeni istemci tarafı bize hello IFRAME bilgiyi yanı sıra bilgi alacağınızı API'leri kullanabilirsiniz. Heyecan verici şeyler!

## <a name="see-also"></a>Ayrıca bkz.
* [Power BI Embedded ile kimlik doğrulaması ve yetkilendirme](power-bi-embedded-app-token-flow.md)

Başka sorunuz mu var? [Merhaba Power BI topluluk deneyin](http://community.powerbi.com/)

