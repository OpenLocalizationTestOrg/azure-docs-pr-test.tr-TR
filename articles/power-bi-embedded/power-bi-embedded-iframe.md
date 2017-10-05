---
title: Power BI Embedded REST ile kullanma | Microsoft Docs
description: "Power BI Embedded KALAN ile kullanmayı öğrenin "
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
ms.openlocfilehash: 31624b9d15772a4f08cf013ac713b3aa636acfca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-power-bi-embedded-with-rest"></a>Power BI Embedded REST ile kullanma

## <a name="power-bi-embedded-what-it-is-and-what-its-for"></a>Power BI Embedded: Nedir ve ne işe yaradığını

Power BI Embedded genel bakış resmi açıklanan [Power BI Embedded site](https://azure.microsoft.com/services/power-bi-embedded/), ancak biz REST ile kullanma hakkında ayrıntılı bilgi almak önce hızlı bir göz atalım.

Gerçekten oldukça basit. dinamik veri Görselleştirmelerini kullanmak isteyebilirsiniz [Power BI](https://powerbi.microsoft.com) kendi uygulamanızda.

Kendi müşteriler için veriler, mutlaka kullanıcılar kendi kuruluşunda sunmak özel uygulamaların çoğu gerekir. Şirket A ve B şirketi için bazı hizmet sunma, örneğin, Şirket A kullanıcılar yalnızca veri kendi Şirket A'daki görmeniz gerekir Diğer bir deyişle, çoklu kiracı teslimat için gereklidir.

Özel uygulama, form kimlik doğrulama, temel kimlik doğrulama vb. gibi kendi kimlik doğrulama yöntemleri de sunumu.. Ardından, katıştırma çözüm var olan bu kimlik doğrulama yöntemleri ile güvenli bir şekilde işbirliği gerekir. Kullanıcıların bu ISV uygulamalar fazladan satın almadan kullanmak için veya bir Power BI aboneliğin lisans olması için gerekli değildir.

 **Power BI Embedded** tam olarak bu tür senaryoları için tasarlanmıştır. Bu nedenle, biz Bu hızlı giriş göz önünden sahip olduğunuza göre şimdi bazı ayrıntılar alın

.NET kullanabilirsiniz \(C#) veya kolayca Power BI Embedded ile uygulamanızı oluşturmak için Node.js SDK. Ancak, bu makalede, HTTP akışı hakkında açıklayacağız \(dahil AuthN) SDK'ları olmadan Power BI. Bu akış anlama, uygulamanızı oluşturabilir **herhangi bir programlama dili ile**, ve Power BI Embedded özünü derine anlayabilirsiniz.

## <a name="create-power-bi-workspace-collection-and-get-access-key-provisioning"></a>Power BI oluşturma çalışma alanı koleksiyonu ve get erişim tuşu \(hazırlama)

Power BI Embedded, Azure Hizmetleri biridir. Azure Portal kullanan ISV kullanım ücretleri için sizden ücret \(saatlik kullanıcı oturumu başına), ve rapor görünümleri kullanıcının ücret değil veya bile bir Azure aboneliği gerektirir.
Bizim uygulama geliştirme başlatmadan önce biz oluşturmalısınız **Power BI çalışma alanı koleksiyonu** Azure portalını kullanarak.

Power BI Embedded her çalışma (Kiracı) her müşteri için çalışma alanıdır ve her çalışma alanı koleksiyonu birçok çalışma alanları ekleyebiliriz. Aynı erişim anahtarını her çalışma alanı koleksiyonu kullanılır. İçinde etkisi, Power BI Embedded için güvenlik sınırı çalışma koleksiyonudur.

![](media/power-bi-embedded-iframe/create-workspace.png)

Çalışma alanı koleksiyonu oluşturma sona erdiğinde erişim tuşunu Azure Portal'dan kopyalayın.

![](media/power-bi-embedded-iframe/copy-access-key.png)

> [!NOTE]
> Biz de çalışma alanı koleksiyonu sağlayabilir ve erişim anahtarı REST API aracılığıyla alın. Daha fazla bilgi için bkz: [Power BI kaynak sağlayıcısı API'leri](https://msdn.microsoft.com/library/azure/mt712306.aspx).

## <a name="create-pbix-file-with-power-bi-desktop"></a>Power BI Desktop ile .pbix dosyası oluşturma

Ardından, biz katıştırılacak raporları ve veri bağlantısı oluşturmanız gerekir.
Bu görev için programlama veya kod yoktur. Yalnızca Power BI Desktop kullanırız.
Bu makalede, biz Power BI Desktop kullanma hakkında ayrıntılar gidin olmaz. Bazı burada yardıma gereksinim duyarsanız, bkz: [Power BI Desktop ile çalışmaya başlama](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/). Bizim örneğimizde, biz yalnızca kullanacağız [Retail Analysis örnek](https://powerbi.microsoft.com/documentation/powerbi-sample-datasets/).

![](media/power-bi-embedded-iframe/power-bi-desktop-1.png)

## <a name="create-a-power-bi-workspace"></a>Power BI çalışma alanı oluşturma

Sağlama tüm yapılır, REST API'leri aracılığıyla çalışma alanı koleksiyonu, bir müşterinin çalışma oluşturmayı başlayalım. Aşağıdaki HTTP POST isteği (REST) bizim mevcut çalışma alanı koleksiyonu yeni bir çalışma alanı oluşturuyor. Bu [POST çalışma API](https://msdn.microsoft.com/library/azure/mt711503.aspx). Bizim örneğimizde, çalışma alanı koleksiyonu addır **mypbiapp**. Yalnızca size daha önce kopyaladığınız, erişim tuşu ayarlarız olarak **AppKey**. Çok basit kimlik doğrulama kadar!

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

Döndürülen **Workspaceıd** aşağıdaki sonraki API çağrıları için kullanılır. Bu değer uygulamamız korumanız gerekir.

## <a name="import-pbix-file-into-the-workspace"></a>Çalışma alanına .pbix dosyasını içeri aktarma

Bir veri kümesi ile tek bir Power BI Desktop dosyası bir çalışma alanındaki her bir raporun karşılık \(veri kaynağı ayarları dahil). Aşağıdaki kodda gösterildiği gibi çalışma alanına biz bizim .pbix dosyasını içeri aktarabilirsiniz. Gördüğünüz gibi biz MIME çok bölümlü http kullanarak .pbix dosyasını ikili karşıya yükleyebilirsiniz.

URI parça **32960a09-6366-4208-a8bb-9e0678cdbb9d** Workspaceıd ve sorgu parametresi **datasetDisplayName** oluşturmak için veri kümesi adı. Oluşturulan veri kümesini .pbix yapıları gibi dosya ilgili tüm verileri tutan içeri aktarılan veriler, veri kaynağına işaretçi olarak vb...

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports?datasetDisplayName=mydataset01
Authorization: AppKey MpaUgrTv5e...
Content-Type: multipart/form-data; boundary="A300testx"

--A300testx
Content-Disposition: form-data

{the content (binary) of .pbix file}
--A300testx--
```

Bu görevi Al bir süre çalışabilir. Tamamlandığında, uygulamamız alma kimliğini kullanarak görev durumu sorabilirsiniz. Bizim örneğimizde içeri aktarma kimliğidir **4eec64dd-533b-47c3-a72c-6508ad854659**.

```
HTTP/1.1 202 Accepted
Content-Type: application/json; charset=utf-8
Location: https://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports/4eec64dd-533b-47c3-a72c-6508ad854659?tenantId=myorg
RequestId: 658bd6b4-b68d-4ec3-8818-2a94266dc220

{"id":"4eec64dd-533b-47c3-a72c-6508ad854659"}
```

Bu içeri aktarma kimliğini kullanarak durumu aşağıdaki istemesi:

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports/4eec64dd-533b-47c3-a72c-6508ad854659
Authorization: AppKey MpaUgrTv5e...
```

Görev tam değilse, HTTP yanıtı şöyle olabilir:

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

Görev tamamlandığında, HTTP yanıtı şuna daha fazla olabilir:

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

Neredeyse tüm .pbix dosyasında yapılarının bizim çalışma alanına alınırken, veri kaynaklarına ilişkin kimlik bilgilerini değildir. Kullanırken, sonuç olarak, **DirectQuery modu**, yerleşik rapor düzgün gösterilemiyor. Ancak kullanırken **alma modunu**, biz varolan alınan verileri kullanarak raporu görüntüleyebilirsiniz. Böyle bir durumda, biz REST çağrıları aracılığıyla aşağıdaki adımları kullanarak kimlik bilgilerini ayarlamanız gerekir.

İlk olarak, biz ağ geçidi datasource almanız gerekir. Veri kümesi biliyoruz **kimliği** daha önce döndürülen kimliğidir.

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

Döndürülen ağ geçidi kimliği ve veri kaynağı kimliği kullanarak \(önceki bkz **gatewayId** ve **kimliği** döndürülen sonuç), bu veri kaynağının kimlik bilgisi gibi değişiklik yapabilirsiniz:

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

Üretimde biz REST API kullanarak her çalışma alanı için farklı bağlantı dizesini de ayarlayabilirsiniz. \(yani, biz veritabanı her müşteri için ayırabilirsiniz.)

Aşağıdaki REST aracılığıyla veri kaynağının bağlantı dizesi değiştiriyor.

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/datasets/458e0451-7215-4029-80b3-9627bf3417b0/Default.SetAllConnections
Authorization: AppKey MpaUgrTv5e...
Content-Type: application/json; charset=utf-8

{
  "connectionString": "data source=testserver02.database.windows.net;initial catalog=testdb02;persist security info=True;encrypt=True;trustservercertificate=False"
}
```

Veya, bir rapor her kullanıcılar için veri ayırmanıza ve biz satır düzeyi güvenlik Power BI Embedded içinde kullanabilirsiniz. As a Result, biz aynı .pbix her müşteri raporla sağlayabilirsiniz \(UI, vb.) ve farklı veri kaynakları.

> [!NOTE]
> Kullanıyorsanız, **alma modunu** yerine **DirectQuery modu**, API aracılığıyla modelleri yenilemek için bir yolu yoktur. Ve Power BI ağ geçidi üzerinden şirket içi veri kaynakları henüz Power BI Embedded içinde desteklenmiyor. Bununla birlikte, gerçekten takip istersiniz [Power BI blog](https://powerbi.microsoft.com/blog/) yenilikler ve yakında gelecek için serbest bırakır.

## <a name="authentication-and-hosting-embedding-reports-in-our-web-page"></a>Kimlik doğrulaması ve web sayfamızı (katıştırma) raporlarında barındırma

Önceki REST API biz erişim tuşunu kullanabilirsiniz **AppKey** authorization üstbilgisi olarak kendisini. Bu çağrı arka uç sunucu tarafında işlenebilir çünkü güvenlidir.

Ancak, biz web sayfamızı rapor ekleme, bu tür güvenlik bilgileri JavaScript kullanarak ele alınması \(ön uç). Ardından kimlik doğrulaması üstbilgi değeri güvenli hale getirilmelidir. Bizim erişim tuşu kötü amaçlı kullanıcı ya da kötü amaçlı kod tarafından bulunmuşsa, bunlar bu anahtarı kullanarak herhangi bir işlem çağırabilirsiniz.

Biz web sayfamızı rapor ekleme, hesaplanan belirtecin erişim tuşu yerine kullanırız gerekir **AppKey**. Uygulamamız OAuth Json Web belirteci oluşturmak \(JWT) talepleri ve hesaplanan dijital imzadan oluşur. Aşağıda gösterildiği gibi bu OAuth JWT nokta ayrılmış kodlu bir dize belirteçleri gereklidir.

![](media/power-bi-embedded-iframe/oauth-jwt.png)

İlk olarak, biz daha sonra oturum giriş değeri hazırlamanız gerekir. Bu değer aşağıdaki json Base64 ile kodlanmış URL'si (rfc4648) dizesi ve bunlar noktayla ayrılmış \(.) karakter. Daha sonra rapor kimliği alma açıklayacağız.

> [!NOTE]
> Biz satır düzeyi güvenlik (RLS) Power BI Embedded ile kullanmak istiyorsanız, biz de belirtmeniz gerekir **kullanıcıadı** ve **rolleri** taleplerdeki.

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

Ardından, biz base64 kodlu dize HMAC oluşturmalısınız \(imza) SHA256 algoritmasını ile. Bu imzalı giriş önceki dize değeridir.

Son olarak, biz nokta kullanarak giriş değeri ve imza dizesi birleştirmeniz gerekir \(.) karakter. Rapor katıştırmak için uygulama belirtecinde tamamlanmış dizesidir. Kötü niyetli bir kullanıcı tarafından uygulama belirtecinde bulunan olsa bile özgün erişim tuşu elde edilemiyor. Bu uygulama belirteci hızlı bir şekilde sona erecek.

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

// 4. show result (which is the apptoken)
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

## <a name="finally-embed-the-report-into-the-web-page"></a>Son olarak, web sayfasına rapor ekleme

Bizim rapor katıştırmak için biz embed url ve rapor almalısınız **kimliği** aşağıdaki REST API kullanarak.

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

Biz raporu web uygulamamız önceki uygulama belirteci kullanılarak eklenebilir.
Biz sonraki örnek kodu bakarsanız, önceki bölümü önceki örnek ile aynıdır. İkinci bölümü, bu örnek göstermektedir **embedUrl** \(önceki sonuçları görmek) IFRAME içinde ve uygulama belirteci IFRAME gönderme.

> [!NOTE]
> Rapor Kimliği değeri, kendi birine değiştirmeniz gerekir. Ayrıca, içerik yönetimi sistemimizde bir hata nedeniyle kod örnek IFRAME etiketinde tam anlamıyla okunur. Bu örnek kodu kopyalayıp capped metin etiketinden kaldırın.

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

Şu anda Power BI Embedded yalnızca rapor IFRAME gösterir. Ancak, bir göz açık tutmak [Power BI Blog](https://powerbi.microsoft.com/blog/). Gelecekteki geliştirmeleri, yeni istemci tarafı bize IFRAME bilgiyi yanı sıra bilgi alacağınızı API'leri kullanabilirsiniz. Heyecan verici şeyler!

## <a name="see-also"></a>Ayrıca bkz.
* [Power BI Embedded ile kimlik doğrulaması ve yetkilendirme](power-bi-embedded-app-token-flow.md)

Başka sorunuz mu var? [Power BI Topluluğu'nu deneyin](http://community.powerbi.com/)

