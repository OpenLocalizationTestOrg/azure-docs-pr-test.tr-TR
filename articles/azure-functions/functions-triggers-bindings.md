---
title: "Tetikleyicileri ve bağlamaları Azure işlevlerinde ile aaaWork | Microsoft Docs"
description: "Nasıl toouse tetikler ve Azure işlevleri tooconnect bağlama kod yürütme tooonline olayları ve bulut tabanlı hizmetleri öğrenin."
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "azure işlevleri, işlevler, olay işleme, web kancaları, dinamik işlem, sunucusuz mimari"
ms.assetid: cbc7460a-4d8a-423f-a63e-1cd33fef7252
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/30/2017
ms.author: donnam
ms.openlocfilehash: eb2ebfca172fcc8c0f479adbcfec99e90fc33615
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-triggers-and-bindings-concepts"></a><span data-ttu-id="f04c4-104">Azure işlevleri Tetikleyicileri ve bağlamaları kavramları</span><span class="sxs-lookup"><span data-stu-id="f04c4-104">Azure Functions triggers and bindings concepts</span></span>
<span data-ttu-id="f04c4-105">Azure işlevleri sağlar, Azure ve diğer hizmetleri yanıt tooevents toowrite kodda aracılığıyla *Tetikleyicileri* ve *bağlamaları*.</span><span class="sxs-lookup"><span data-stu-id="f04c4-105">Azure Functions allows you toowrite code in response tooevents in Azure and other services, through *triggers* and *bindings*.</span></span> <span data-ttu-id="f04c4-106">Bu makalede Tetikleyicileri kavramsal genel bakış olduğundan ve tüm bağlamaları desteklenen programlama dilleri.</span><span class="sxs-lookup"><span data-stu-id="f04c4-106">This article is a conceptual overview of triggers and bindings for all supported programming languages.</span></span> <span data-ttu-id="f04c4-107">Ortak tooall bağlamaları özellikleri burada açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="f04c4-107">Features that are common tooall bindings are described here.</span></span>

## <a name="overview"></a><span data-ttu-id="f04c4-108">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="f04c4-108">Overview</span></span>

<span data-ttu-id="f04c4-109">Tetikleyicileri ve bağlamaları olan bir bildirim temelli yolu toodefine nasıl bir işlev çağrılır ve hangi verilerin, ile birlikte çalışır.</span><span class="sxs-lookup"><span data-stu-id="f04c4-109">Triggers and bindings are a declarative way toodefine how a function is invoked and what data it works with.</span></span> <span data-ttu-id="f04c4-110">A *tetikleyici* bir işlev nasıl çağrıldığını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="f04c4-110">A *trigger* defines how a function is invoked.</span></span> <span data-ttu-id="f04c4-111">Bir işlev tam olarak bir tetikleyici olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f04c4-111">A function must have exactly one trigger.</span></span> <span data-ttu-id="f04c4-112">Tetikleyiciler genellikle hello işlevi tetiklenen hello yükü olduğu veri ilişkilendirdiniz.</span><span class="sxs-lookup"><span data-stu-id="f04c4-112">Triggers have associated data, which is usually hello payload that triggered hello function.</span></span> 

<span data-ttu-id="f04c4-113">Giriş ve çıkış *bağlamaları* kodunuzu içinde bildirim temelli yolu tooconnect toodata gelen sağlayın.</span><span class="sxs-lookup"><span data-stu-id="f04c4-113">Input and output *bindings* provide a declarative way tooconnect toodata from within your code.</span></span> <span data-ttu-id="f04c4-114">Benzer tootriggers işlevi yapılandırmanızda bağlantı dizeleri ve diğer özellikleri belirtin.</span><span class="sxs-lookup"><span data-stu-id="f04c4-114">Similar tootriggers, you specify connection strings and other properties in your function configuration.</span></span> <span data-ttu-id="f04c4-115">Bağlamaları isteğe bağlıdır ve bir işlev birden fazla giriş varsa ve bağlamaları çıktı.</span><span class="sxs-lookup"><span data-stu-id="f04c4-115">Bindings are optional and a function can have multiple input and output bindings.</span></span> 

<span data-ttu-id="f04c4-116">Tetikleyicileri ve bağlamaları kullanarak, daha genel olan ve olmayan stillerinizin hello ayrıntılarını hello Hizmetleri ile etkileşime giren mu kod yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f04c4-116">Using triggers and bindings, you can write code that is more generic and does not hardcode hello details of hello services with which it interacts.</span></span> <span data-ttu-id="f04c4-117">İşlevi kodunuz için giriş değerleri Hizmetleri yalnızca haline gelen veri.</span><span class="sxs-lookup"><span data-stu-id="f04c4-117">Data coming from services simply become input values for your function code.</span></span> <span data-ttu-id="f04c4-118">(örneğin, yeni bir satır Azure tablo Depolama'da oluşturma), toooutput veri tooanother hizmeti hello hello yönteminin dönüş değeri kullanın.</span><span class="sxs-lookup"><span data-stu-id="f04c4-118">toooutput data tooanother service (such as creating a new row in Azure Table Storage), use hello return value of hello method.</span></span> <span data-ttu-id="f04c4-119">Veya birden çok değer toooutput gerekiyorsa, bir yardımcı nesnesi kullanın.</span><span class="sxs-lookup"><span data-stu-id="f04c4-119">Or, if you need toooutput multiple values, use a helper object.</span></span> <span data-ttu-id="f04c4-120">Tetikleyicileri ve bağlamaları sahip bir **adı** kod tooaccess hello bağlamasında kullandığınız bir tanımlayıcıdır özelliği.</span><span class="sxs-lookup"><span data-stu-id="f04c4-120">Triggers and bindings have a **name** property, which is an identifier you use in your code tooaccess hello binding.</span></span>

<span data-ttu-id="f04c4-121">Hello Tetikleyicileri ve bağlamaları yapılandırabilirsiniz **tümleştir** hello Azure işlevleri portalına sekmesindedir.</span><span class="sxs-lookup"><span data-stu-id="f04c4-121">You can configure triggers and bindings in hello **Integrate** tab in hello Azure Functions portal.</span></span> <span data-ttu-id="f04c4-122">Merhaba perde arkasında hello UI adlı bir dosya değiştirir *function.json* hello işlevi dizindeki dosyayı.</span><span class="sxs-lookup"><span data-stu-id="f04c4-122">Under hello covers, hello UI modifies a file called *function.json* file in hello function directory.</span></span> <span data-ttu-id="f04c4-123">Bu dosyayı toohello değiştirerek düzenleyebilirsiniz **Gelişmiş Düzenleyici**.</span><span class="sxs-lookup"><span data-stu-id="f04c4-123">You can edit this file by changing toohello **Advanced editor**.</span></span>

<span data-ttu-id="f04c4-124">Merhaba aşağıdaki tabloda hello tetikleyiciler ve Azure işlevleri ile desteklenen bağlamaları gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="f04c4-124">hello following table shows hello triggers and bindings that are supported with Azure Functions.</span></span> 

[!INCLUDE [Full bindings table](../../includes/functions-bindings.md)]

### <a name="example-queue-trigger-and-table-output-binding"></a><span data-ttu-id="f04c4-125">Örnek: bağlama sırası tetikleyici ve tablo çıktısı</span><span class="sxs-lookup"><span data-stu-id="f04c4-125">Example: queue trigger and table output binding</span></span>

<span data-ttu-id="f04c4-126">Her Azure kuyruk depolamada yeni bir ileti görüntülendiğinde toowrite yeni bir satır tooAzure Table Storage istediğinizi varsayalım.</span><span class="sxs-lookup"><span data-stu-id="f04c4-126">Suppose you want toowrite a new row tooAzure Table Storage whenever a new message appears in Azure Queue Storage.</span></span> <span data-ttu-id="f04c4-127">Bu senaryo, bir Azure kuyruk kullanarak uygulanabilir tetikleyici ve bir tablo çıktısı bağlama.</span><span class="sxs-lookup"><span data-stu-id="f04c4-127">This scenario can be implemented using an Azure Queue trigger and a Table output binding.</span></span> 

<span data-ttu-id="f04c4-128">Bir kuyruk tetikleyici hello bilgileri aşağıdaki hello gerektirir **tümleştir** sekmesi:</span><span class="sxs-lookup"><span data-stu-id="f04c4-128">A queue trigger requires hello following information in hello **Integrate** tab:</span></span>

* <span data-ttu-id="f04c4-129">Merhaba depolama hesabı bağlantı dizesi hello sıranın içeren hello uygulama ayarı Hello adı</span><span class="sxs-lookup"><span data-stu-id="f04c4-129">hello name of hello app setting that contains hello storage account connection string for hello queue</span></span>
* <span data-ttu-id="f04c4-130">Merhaba kuyruk adı</span><span class="sxs-lookup"><span data-stu-id="f04c4-130">hello queue name</span></span>
* <span data-ttu-id="f04c4-131">Merhaba kuyruk iletisi, kod tooread hello içeriğini tanımlayıcı gibi hello `order`.</span><span class="sxs-lookup"><span data-stu-id="f04c4-131">hello identifier in your code tooread hello contents of hello queue message, such as `order`.</span></span>

<span data-ttu-id="f04c4-132">toowrite tooAzure Table Storage, aşağıdaki ayrıntılara hello ile bir çıktı bağlama kullanın:</span><span class="sxs-lookup"><span data-stu-id="f04c4-132">toowrite tooAzure Table Storage, use an output binding with hello following details:</span></span>

* <span data-ttu-id="f04c4-133">Merhaba tablonun hello depolama hesabı bağlantı dizesi içeren hello uygulama ayarı Hello adı</span><span class="sxs-lookup"><span data-stu-id="f04c4-133">hello name of hello app setting that contains hello storage account connection string for hello table</span></span>
* <span data-ttu-id="f04c4-134">Merhaba tablo adı</span><span class="sxs-lookup"><span data-stu-id="f04c4-134">hello table name</span></span>
* <span data-ttu-id="f04c4-135">kod toocreate Hello tanımlayıcıda öğeler veya hello dönüş değeri hello işlevden çıktı.</span><span class="sxs-lookup"><span data-stu-id="f04c4-135">hello identifier in your code toocreate output items, or hello return value from hello function.</span></span>

<span data-ttu-id="f04c4-136">Bağlantı dizeleri tooenforce hello en iyi uygulama için bağlamaları kullanma uygulaması ayarları *function.json* hizmet gizli içermiyor.</span><span class="sxs-lookup"><span data-stu-id="f04c4-136">Bindings use app settings for connection strings tooenforce hello best practice that *function.json* does not contain service secrets.</span></span>

<span data-ttu-id="f04c4-137">Sonra kodunuzu Azure Storage ile toointegrate sağlanan hello tanımlayıcılar kullanın.</span><span class="sxs-lookup"><span data-stu-id="f04c4-137">Then, use hello identifiers you provided toointegrate with Azure Storage in your code.</span></span>

```cs
#r "Newtonsoft.Json"

using Newtonsoft.Json.Linq;

// From an incoming queue message that is a JSON object, add fields and write tooTable Storage
// hello method return value creates a new row in Table Storage
public static Person Run(JObject order, TraceWriter log)
{
    return new Person() { 
            PartitionKey = "Orders", 
            RowKey = Guid.NewGuid().ToString(),  
            Name = order["Name"].ToString(),
            MobileNumber = order["MobileNumber"].ToString() };  
}
 
public class Person
{
    public string PartitionKey { get; set; }
    public string RowKey { get; set; }
    public string Name { get; set; }
    public string MobileNumber { get; set; }
}
```

```javascript
// From an incoming queue message that is a JSON object, add fields and write tooTable Storage
// hello second parameter toocontext.done is used as hello value for hello new row
module.exports = function (context, order) {
    order.PartitionKey = "Orders";
    order.RowKey = generateRandomId(); 

    context.done(null, order);
};

function generateRandomId() {
    return Math.random().toString(36).substring(2, 15) +
        Math.random().toString(36).substring(2, 15);
}
```

<span data-ttu-id="f04c4-138">Merhaba işte *function.json* kod önceki toohello karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="f04c4-138">Here is hello *function.json* that corresponds toohello preceding code.</span></span> <span data-ttu-id="f04c4-139">Merhaba işlev uygulama hello dilinden bağımsız olarak aynı yapılandırmayı kullanılabilir o hello unutmayın.</span><span class="sxs-lookup"><span data-stu-id="f04c4-139">Note that hello same configuration can be used, regardless of hello language of hello function implementation.</span></span>

```json
{
  "bindings": [
    {
      "name": "order",
      "type": "queueTrigger",
      "direction": "in",
      "queueName": "myqueue-items",
      "connection": "MY_STORAGE_ACCT_APP_SETTING"
    },
    {
      "name": "$return",
      "type": "table",
      "direction": "out",
      "tableName": "outTable",
      "connection": "MY_TABLE_STORAGE_ACCT_APP_SETTING"
    }
  ]
}
```
<span data-ttu-id="f04c4-140">tooview ve düzenleme Merhaba içeriğine *function.json* hello hello Azure portal'ı tıklatın **Gelişmiş Düzenleyici** hello seçeneği **tümleştir** işlevinizi sekmesinde.</span><span class="sxs-lookup"><span data-stu-id="f04c4-140">tooview and edit hello contents of *function.json* in hello Azure portal, click hello **Advanced editor** option on hello **Integrate** tab of your function.</span></span>

<span data-ttu-id="f04c4-141">Daha fazla kod örnekleri ve Azure Storage ile tümleştirme hakkında bilgi için bkz: [Azure işlevleri Tetikleyicileri ve bağlamaları Azure Storage için](functions-bindings-storage.md).</span><span class="sxs-lookup"><span data-stu-id="f04c4-141">For more code examples and details on integrating with Azure Storage, see [Azure Functions triggers and bindings for Azure Storage](functions-bindings-storage.md).</span></span>

### <a name="binding-direction"></a><span data-ttu-id="f04c4-142">Bağlama yönü</span><span class="sxs-lookup"><span data-stu-id="f04c4-142">Binding direction</span></span>

<span data-ttu-id="f04c4-143">Tüm Tetikleyicileri ve bağlamaları sahip bir `direction` özelliği:</span><span class="sxs-lookup"><span data-stu-id="f04c4-143">All triggers and bindings have a `direction` property:</span></span>

- <span data-ttu-id="f04c4-144">Tetikleyiciler için her zaman hello yönü olur`in`</span><span class="sxs-lookup"><span data-stu-id="f04c4-144">For triggers, hello direction is always `in`</span></span>
- <span data-ttu-id="f04c4-145">Giriş ve çıkış bağlamaları kullanmak `in` ve`out`</span><span class="sxs-lookup"><span data-stu-id="f04c4-145">Input and output bindings use `in` and `out`</span></span>
- <span data-ttu-id="f04c4-146">Özel bir yön bazı bağlamaları Destek `inout`.</span><span class="sxs-lookup"><span data-stu-id="f04c4-146">Some bindings support a special direction `inout`.</span></span> <span data-ttu-id="f04c4-147">Kullanırsanız `inout`, yalnızca hello **Gelişmiş Düzenleyici** hello kullanılabilir **tümleştir** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="f04c4-147">If you use `inout`, only hello **Advanced editor** is available in hello **Integrate** tab.</span></span>

## <a name="using-hello-function-return-type-tooreturn-a-single-output"></a><span data-ttu-id="f04c4-148">Merhaba işlevi dönüş türü tooreturn tek bir çıktı kullanma</span><span class="sxs-lookup"><span data-stu-id="f04c4-148">Using hello function return type tooreturn a single output</span></span>

<span data-ttu-id="f04c4-149">Merhaba önceki örnekte nasıl toouse hello işlevi dönüş değeri tooprovide hello özel name parametresi kullanılarak elde edilir tooa bağlama çıktısını gösterir `$return`.</span><span class="sxs-lookup"><span data-stu-id="f04c4-149">hello preceding example shows how toouse hello function return value tooprovide output tooa binding, which is achieved by using hello special name parameter `$return`.</span></span> <span data-ttu-id="f04c4-150">(Bu yalnızca C#, JavaScript ve F # gibi bir dönüş değerine sahip dillerde desteklenir.) Bir işlev birden çok çıktı bağlaması içeriyorsa `$return` hello çıkış bağlamaları yalnızca biri için.</span><span class="sxs-lookup"><span data-stu-id="f04c4-150">(This is only supported in languages that have a return value, such as C#, JavaScript, and F#.) If a function has multiple output bindings, use `$return` for only one of hello output bindings.</span></span> 

```json
// excerpt of function.json
{
    "name": "$return",
    "type": "blob",
    "direction": "out",
    "path": "output-container/{id}"
}
```

<span data-ttu-id="f04c4-151">C#, JavaScript ve F # çıkış bağlamalarla türleri kullanılır Hello örnekleri Göster aşağıda nasıl döndür.</span><span class="sxs-lookup"><span data-stu-id="f04c4-151">hello examples below show how return types are used with output bindings in C#, JavaScript, and F#.</span></span>

```cs
// C# example: use method return value for output binding
public static string Run(WorkItem input, TraceWriter log)
{
    string json = string.Format("{{ \"id\": \"{0}\" }}", input.Id);
    log.Info($"C# script processed queue message. Item={json}");
    return json;
}
```

```cs
// C# example: async method, using return value for output binding
public static Task<string> Run(WorkItem input, TraceWriter log)
{
    string json = string.Format("{{ \"id\": \"{0}\" }}", input.Id);
    log.Info($"C# script processed queue message. Item={json}");
    return json;
}
```

```javascript
// JavaScript: return a value in hello second parameter toocontext.done
module.exports = function (context, input) {
    var json = JSON.stringify(input);
    context.log('Node.js script processed queue message', json);
    context.done(null, json);
}
```

```fsharp
// F# example: use return value for output binding
let Run(input: WorkItem, log: TraceWriter) =
    let json = String.Format("{{ \"id\": \"{0}\" }}", input.Id)   
    log.Info(sprintf "F# script processed queue message '%s'" json)
    json
```

## <a name="binding-datatype-property"></a><span data-ttu-id="f04c4-152">DataType özelliği için bağlama</span><span class="sxs-lookup"><span data-stu-id="f04c4-152">Binding dataType property</span></span>

<span data-ttu-id="f04c4-153">.NET ile Merhaba türleri toodefine hello veri türü için giriş verileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="f04c4-153">In .NET, use hello types toodefine hello data type for input data.</span></span> <span data-ttu-id="f04c4-154">Örneğin, kullanın `string` toobind toohello metnin bir sıra tetikleyici ve bir bayt dizisi tooread ikili olarak.</span><span class="sxs-lookup"><span data-stu-id="f04c4-154">For instance, use `string` toobind toohello text of a queue trigger and a byte array tooread as binary.</span></span>

<span data-ttu-id="f04c4-155">JavaScript gibi dinamik olarak yazılan diller için hello kullan `dataType` hello bağlama tanımında özelliği.</span><span class="sxs-lookup"><span data-stu-id="f04c4-155">For languages that are dynamically typed such as JavaScript, use hello `dataType` property in hello binding definition.</span></span> <span data-ttu-id="f04c4-156">Örneğin, tooread ikili biçimde bir HTTP isteğinin içerik Merhaba, hello türünü kullanmak `binary`:</span><span class="sxs-lookup"><span data-stu-id="f04c4-156">For example, tooread hello content of an HTTP request in binary format, use hello type `binary`:</span></span>

```json
{
    "type": "httpTrigger",
    "name": "req",
    "direction": "in",
    "dataType": "binary"
}
```

<span data-ttu-id="f04c4-157">Diğer seçenekler için `dataType` olan `stream` ve `string`.</span><span class="sxs-lookup"><span data-stu-id="f04c4-157">Other options for `dataType` are `stream` and `string`.</span></span>

## <a name="resolving-app-settings"></a><span data-ttu-id="f04c4-158">Uygulama ayarlarını çözümleme</span><span class="sxs-lookup"><span data-stu-id="f04c4-158">Resolving app settings</span></span>
<span data-ttu-id="f04c4-159">En iyi uygulama, parolaları ve bağlantı dizeleri yapılandırma dosyalarını yerine uygulama ayarları kullanılarak yönetilmelidir.</span><span class="sxs-lookup"><span data-stu-id="f04c4-159">As a best practice, secrets and connection strings should be managed using app settings, rather than configuration files.</span></span> <span data-ttu-id="f04c4-160">Bu sınırlar erişim toothese gizli ve güvenli toostore kolaylaştırır *function.json* ortak kaynak denetimi havuzunda.</span><span class="sxs-lookup"><span data-stu-id="f04c4-160">This limits access toothese secrets and makes it safe toostore *function.json* in a public source control repository.</span></span>

<span data-ttu-id="f04c4-161">Uygulama ayarları da hello ortamına bağlı toochange yapılandırma istediğinizde kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="f04c4-161">App settings are also useful whenever you want toochange configuration based on hello environment.</span></span> <span data-ttu-id="f04c4-162">Örneğin, bir test ortamında toomonitor farklı bir sıra veya blob depolama kapsayıcısı isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f04c4-162">For example, in a test environment, you may want toomonitor a different queue or blob storage container.</span></span>

<span data-ttu-id="f04c4-163">Uygulama ayarları, yüzde işaretleri gibi içine alınmış bir değer her çözümlendirinden `%MyAppSetting%`.</span><span class="sxs-lookup"><span data-stu-id="f04c4-163">App settings are resolved whenever a value is enclosed in percent signs, such as `%MyAppSetting%`.</span></span> <span data-ttu-id="f04c4-164">Bu hello Not `connection` Tetikleyicileri ve bağlamaları özelliği özel bir durumdur ve uygulama ayarlarının değerleri otomatik olarak çözer.</span><span class="sxs-lookup"><span data-stu-id="f04c4-164">Note that hello `connection` property of triggers and bindings is a special case and automatically resolves values as app settings.</span></span> 

<span data-ttu-id="f04c4-165">Merhaba aşağıdaki örnekte olduğu bir uygulama ayarını kullanan bir sıra tetikleyici `%input-queue-name%` toodefine hello sıra tootrigger üzerinde.</span><span class="sxs-lookup"><span data-stu-id="f04c4-165">hello following example is a queue trigger that uses an app setting `%input-queue-name%` toodefine hello queue tootrigger on.</span></span>

```json
{
  "bindings": [
    {
      "name": "order",
      "type": "queueTrigger",
      "direction": "in",
      "queueName": "%input-queue-name%",
      "connection": "MY_STORAGE_ACCT_APP_SETTING"
    }
  ]
}
```

## <a name="trigger-metadata-properties"></a><span data-ttu-id="f04c4-166">Tetikleyici meta veri özellikleri</span><span class="sxs-lookup"><span data-stu-id="f04c4-166">Trigger metadata properties</span></span>

<span data-ttu-id="f04c4-167">Toohello veri yükü tetikleyici (örneğin, bir işlev tetiklenen hello kuyruk iletisi) tarafından sağlanan ek birçok Tetikleyicileri ek meta veri değerleri sağlayın.</span><span class="sxs-lookup"><span data-stu-id="f04c4-167">In addition toohello data payload provided by a trigger (such as hello queue message that triggered a function), many triggers provide additional metadata values.</span></span> <span data-ttu-id="f04c4-168">Bu değerler, C# ve F # veya hello özellikleri giriş parametresi olarak kullanılabilir `context.bindings` JavaScript nesne.</span><span class="sxs-lookup"><span data-stu-id="f04c4-168">These values can be used as input parameters in C# and F# or properties on hello `context.bindings` object in JavaScript.</span></span> 

<span data-ttu-id="f04c4-169">Örneğin, bir sıra tetikleyici aşağıdaki özelliklere hello destekler:</span><span class="sxs-lookup"><span data-stu-id="f04c4-169">For example, a queue trigger supports hello following properties:</span></span>

* <span data-ttu-id="f04c4-170">QueueTrigger - geçerli bir dize, ileti içeriği tetikleme</span><span class="sxs-lookup"><span data-stu-id="f04c4-170">QueueTrigger - triggering message content if a valid string</span></span>
* <span data-ttu-id="f04c4-171">DequeueCount</span><span class="sxs-lookup"><span data-stu-id="f04c4-171">DequeueCount</span></span>
* <span data-ttu-id="f04c4-172">expirationTime</span><span class="sxs-lookup"><span data-stu-id="f04c4-172">ExpirationTime</span></span>
* <span data-ttu-id="f04c4-173">Kimlik</span><span class="sxs-lookup"><span data-stu-id="f04c4-173">Id</span></span>
* <span data-ttu-id="f04c4-174">InsertionTime</span><span class="sxs-lookup"><span data-stu-id="f04c4-174">InsertionTime</span></span>
* <span data-ttu-id="f04c4-175">NextVisibleTime</span><span class="sxs-lookup"><span data-stu-id="f04c4-175">NextVisibleTime</span></span>
* <span data-ttu-id="f04c4-176">PopReceipt</span><span class="sxs-lookup"><span data-stu-id="f04c4-176">PopReceipt</span></span>

<span data-ttu-id="f04c4-177">Her tetikleyici için meta veri özelliklerini ayrıntılarını hello karşılık gelen başvuru konusunda açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="f04c4-177">Details of metadata properties for each trigger are described in hello corresponding reference topic.</span></span> <span data-ttu-id="f04c4-178">Belgeleri kullanılabilir ayrıca hello **tümleştir** hello portalında hello sekmesinde **belgelerine** hello bağlama yapılandırma alanı aşağıdaki bölümüne.</span><span class="sxs-lookup"><span data-stu-id="f04c4-178">Documentation is also available in hello **Integrate** tab of hello portal, in hello **Documentation** section below hello binding configuration area.</span></span>  

<span data-ttu-id="f04c4-179">Bazı gecikmeler BLOB Tetikleyicileri sahip olduğundan, örneğin, bir sıra tetikleyici toorun işlevinizi kullanabilirsiniz (bkz [Blob Depolama tetikleyici](functions-bindings-storage-blob.md#storage-blob-trigger).</span><span class="sxs-lookup"><span data-stu-id="f04c4-179">For example, since blob triggers have some delays, you can use a queue trigger toorun your function (see [Blob Storage Trigger](functions-bindings-storage-blob.md#storage-blob-trigger).</span></span> <span data-ttu-id="f04c4-180">Merhaba kuyruk iletisi üzerinde hello blob filename tootrigger içerecektir.</span><span class="sxs-lookup"><span data-stu-id="f04c4-180">hello queue message would contain hello blob filename tootrigger on.</span></span> <span data-ttu-id="f04c4-181">Hello kullanarak `queueTrigger` meta veri özelliği, tüm yapılandırmanızı yerine kodunuzu bu davranış belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f04c4-181">Using hello `queueTrigger` metadata property, you can specify this behavior all in your configuration, rather than your code.</span></span>

```json
  "bindings": [
    {
      "name": "myQueueItem",
      "type": "queueTrigger",
      "queueName": "myqueue-items",
      "connection": "MyStorageConnection",
    },
    {
      "name": "myInputBlob",
      "type": "blob",
      "path": "samples-workitems/{queueTrigger}",
      "direction": "in",
      "connection": "MyStorageConnection"
    }
  ]
```

<span data-ttu-id="f04c4-182">Bir tetikleyiciden meta veri özelliklerini de kullanılabilir bir *ifade bağlama* bölümden açıklandığı hello olarak başka bir bağlama için.</span><span class="sxs-lookup"><span data-stu-id="f04c4-182">Metadata properties from a trigger can also be used in a *binding expression* for another binding, as described in hello following section.</span></span>

## <a name="binding-expressions-and-patterns"></a><span data-ttu-id="f04c4-183">İfadeler ve desenler bağlama</span><span class="sxs-lookup"><span data-stu-id="f04c4-183">Binding expressions and patterns</span></span>

<span data-ttu-id="f04c4-184">Tetikleyicileri ve bağlamaları hello en güçlü özelliklerden biridir *ifadeleri bağlama*.</span><span class="sxs-lookup"><span data-stu-id="f04c4-184">One of hello most powerful features of triggers and bindings is *binding expressions*.</span></span> <span data-ttu-id="f04c4-185">İçinde bağlama, diğer bağlamaları veya kodunuzu daha sonra kullanılabilir düzeni ifadeler tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f04c4-185">Within your binding, you can define pattern expressions which can then be used in other bindings or your code.</span></span> <span data-ttu-id="f04c4-186">Tetikleyici meta veri bölümü önceki hello hello örnek Göster olarak ifadeleri, bağlama de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="f04c4-186">Trigger metadata can also be used in binding expressions, as show in hello sample in hello preceding section.</span></span>

<span data-ttu-id="f04c4-187">Örneğin, belirli bir blob depolama kapsayıcısını, benzer toohello tooresize görüntülerinde istediğinizi varsayalım **görüntü Boyutlandır** hello şablonunda **yeni işlev** sayfası.</span><span class="sxs-lookup"><span data-stu-id="f04c4-187">For example, suppose you want tooresize images in particular blob storage container, similar toohello **Image Resizer** template in hello **New Function** page.</span></span> <span data-ttu-id="f04c4-188">Çok Git**yeni işlev** dil -> **C#** senaryo -> **örnekleri** -> **ImageResizer CSharp**.</span><span class="sxs-lookup"><span data-stu-id="f04c4-188">Go too**New Function** -> Language **C#** -> Scenario **Samples** -> **ImageResizer-CSharp**.</span></span> 

<span data-ttu-id="f04c4-189">Merhaba işte *function.json* tanımı:</span><span class="sxs-lookup"><span data-stu-id="f04c4-189">Here is hello *function.json* definition:</span></span>

```json
{
  "bindings": [
    {
      "name": "image",
      "type": "blobTrigger",
      "path": "sample-images/{filename}",
      "direction": "in",
      "connection": "MyStorageConnection"
    },
    {
      "name": "imageSmall",
      "type": "blob",
      "path": "sample-images-sm/{filename}",
      "direction": "out",
      "connection": "MyStorageConnection"
    }
  ],
}
```

<span data-ttu-id="f04c4-190">Bu hello fark `filename` parametresi hem hello blob tetikleyicinizin tanımını yanı sıra hello blobu kullanılır bağlama çıktı.</span><span class="sxs-lookup"><span data-stu-id="f04c4-190">Notice that hello `filename` parameter is used in both hello blob trigger definition as well as hello blob output binding.</span></span> <span data-ttu-id="f04c4-191">Bu parametre, işlev kodu de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="f04c4-191">This parameter can also be used in function code.</span></span>

```csharp
// C# example of binding too{filename}
public static void Run(Stream image, string filename, Stream imageSmall, TraceWriter log)  
{
    log.Info($"Blob trigger processing: {filename}");
    // ...
} 
```

<!--TODO: add JavaScript example -->
<!-- Blocked by bug https://github.com/Azure/Azure-Functions/issues/248 -->


### <a name="random-guids"></a><span data-ttu-id="f04c4-192">Rastgele GUID'leri</span><span class="sxs-lookup"><span data-stu-id="f04c4-192">Random GUIDs</span></span>
<span data-ttu-id="f04c4-193">Azure işlevleri hello aracılığıyla, bağlamalarda GUID'ler oluşturmak için bir kolaylık sözdizimi sağlar `{rand-guid}` ifade bağlama.</span><span class="sxs-lookup"><span data-stu-id="f04c4-193">Azure Functions provides a convenience syntax for generating GUIDs in your bindings, through hello `{rand-guid}` binding expression.</span></span> <span data-ttu-id="f04c4-194">Merhaba aşağıdaki örnekte bu toogenerate benzersiz blob adı kullanır:</span><span class="sxs-lookup"><span data-stu-id="f04c4-194">hello following example uses this toogenerate a unique blob name:</span></span> 

```json
{
  "type": "blob",
  "name": "blobOutput",
  "direction": "out",
  "path": "my-output-container/{rand-guid}"
}
```

### <a name="current-time"></a><span data-ttu-id="f04c4-195">Geçerli saat</span><span class="sxs-lookup"><span data-stu-id="f04c4-195">Current time</span></span>

<span data-ttu-id="f04c4-196">Merhaba bağlama deyimi kullanabilirsiniz `DateTime`, hangi çözümler çok`DateTime.UtcNow`.</span><span class="sxs-lookup"><span data-stu-id="f04c4-196">You can use hello binding expression `DateTime`, which resolves too`DateTime.UtcNow`.</span></span>

```json
{
  "type": "blob",
  "name": "blobOutput",
  "direction": "out",
  "path": "my-output-container/{DateTime}"
}
```

## <a name="bind-toocustom-input-properties-in-a-binding-expression"></a><span data-ttu-id="f04c4-197">Bir bağlama ifadesinde toocustom giriş özellikleri bağlama</span><span class="sxs-lookup"><span data-stu-id="f04c4-197">Bind toocustom input properties in a binding expression</span></span>

<span data-ttu-id="f04c4-198">İfadeler bağlama hello tetikleyici yükünde kendisini tanımlanan özellikler başvuruda bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="f04c4-198">Binding expressions can also reference properties that are defined in hello trigger payload itself.</span></span> <span data-ttu-id="f04c4-199">Örneğin, bir Web kancası sağlanan bir dosya adı toodynamically bağlama tooa blob depolama dosyası isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f04c4-199">For example, you may want toodynamically bind tooa blob storage file from a filename provided in a webhook.</span></span>

<span data-ttu-id="f04c4-200">Örneğin, aşağıdaki hello *function.json* adlı bir özellik kullanır `BlobName` hello tetikleyici yükü gelen:</span><span class="sxs-lookup"><span data-stu-id="f04c4-200">For example, hello following *function.json* uses a property called `BlobName` from hello trigger payload:</span></span>

```json
{
  "bindings": [
    {
      "name": "info",
      "type": "httpTrigger",
      "direction": "in",
      "webHookType": "genericJson",
    },
    {
      "name": "blobContents",
      "type": "blob",
      "direction": "in",
      "path": "strings/{BlobName}",
      "connection": "AzureWebJobsStorage"
    },
    {
      "name": "res",
      "type": "http",
      "direction": "out"
    }
  ]
}
```

<span data-ttu-id="f04c4-201">tooaccomplish bu C# ve F # ' hello tetikleyici yükünde seri durumdan hello alanlarını tanımlayan bir POCO tanımlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f04c4-201">tooaccomplish this in C# and F#, you must define a POCO that defines hello fields that will be deserialized in hello trigger payload.</span></span>

```csharp
using System.Net;

public class BlobInfo
{
    public string BlobName { get; set; }
}
  
public static HttpResponseMessage Run(HttpRequestMessage req, BlobInfo info, string blobContents)
{
    if (blobContents == null) {
        return req.CreateResponse(HttpStatusCode.NotFound);
    } 

    return req.CreateResponse(HttpStatusCode.OK, new {
        data = $"{blobContents}"
    });
}
```

<span data-ttu-id="f04c4-202">JavaScript, JSON seri durumundan çıkarma otomatik olarak gerçekleştirilir ve doğrudan hello özelliklerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f04c4-202">In JavaScript, JSON deserialization is automatically performed and you can use hello properties directly.</span></span>

```javascript
module.exports = function (context, info) {
    if ('BlobName' in info) {
        context.res = {
            body: { 'data': context.bindings.blobContents }
        }
    }
    else {
        context.res = {
            status: 404
        };
    }
    context.done();
}
```

## <a name="configuring-binding-data-at-runtime"></a><span data-ttu-id="f04c4-203">Çalışma zamanında veri bağlama yapılandırma</span><span class="sxs-lookup"><span data-stu-id="f04c4-203">Configuring binding data at runtime</span></span>

<span data-ttu-id="f04c4-204">C# ve diğer .NET dilleri karşılıklı toohello bildirim temelli bağlama olarak kesinlik temelli bağlama düzeni kullanabilirsiniz *function.json*.</span><span class="sxs-lookup"><span data-stu-id="f04c4-204">In C# and other .NET languages, you can use an imperative binding pattern, as opposed toohello declarative bindings in *function.json*.</span></span> <span data-ttu-id="f04c4-205">Kesinlik temelli bağlama bağlama parametreleri tasarım yerine çalışma zamanında hesaplanan toobe gerektiğinde kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="f04c4-205">Imperative binding is useful when binding parameters need toobe computed at runtime rather than design time.</span></span> <span data-ttu-id="f04c4-206">toolearn daha, fazla [kesinlik temelli bağlamaları aracılığıyla çalışma zamanında bağlama](functions-reference-csharp.md#imperative-bindings) hello C# Geliştirici Başvurusu.</span><span class="sxs-lookup"><span data-stu-id="f04c4-206">toolearn more, see [Binding at runtime via imperative bindings](functions-reference-csharp.md#imperative-bindings) in hello C# developer reference.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f04c4-207">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f04c4-207">Next steps</span></span>
<span data-ttu-id="f04c4-208">Belirli bir bağlama hakkında daha fazla bilgi için aşağıdaki makaleler hello bakın:</span><span class="sxs-lookup"><span data-stu-id="f04c4-208">For more information on a specific binding, see hello following articles:</span></span>

- [<span data-ttu-id="f04c4-209">HTTP ve web kancaları</span><span class="sxs-lookup"><span data-stu-id="f04c4-209">HTTP and webhooks</span></span>](functions-bindings-http-webhook.md)
- [<span data-ttu-id="f04c4-210">Zamanlayıcı</span><span class="sxs-lookup"><span data-stu-id="f04c4-210">Timer</span></span>](functions-bindings-timer.md)
- [<span data-ttu-id="f04c4-211">Kuyruk depolama</span><span class="sxs-lookup"><span data-stu-id="f04c4-211">Queue storage</span></span>](functions-bindings-storage-queue.md)
- [<span data-ttu-id="f04c4-212">Blob depolama</span><span class="sxs-lookup"><span data-stu-id="f04c4-212">Blob storage</span></span>](functions-bindings-storage-blob.md)
- [<span data-ttu-id="f04c4-213">Tablo depolama</span><span class="sxs-lookup"><span data-stu-id="f04c4-213">Table storage</span></span>](functions-bindings-storage-table.md)
- [<span data-ttu-id="f04c4-214">Olay Hub’ı</span><span class="sxs-lookup"><span data-stu-id="f04c4-214">Event Hub</span></span>](functions-bindings-event-hubs.md)
- [<span data-ttu-id="f04c4-215">Service Bus</span><span class="sxs-lookup"><span data-stu-id="f04c4-215">Service Bus</span></span>](functions-bindings-service-bus.md)
- [<span data-ttu-id="f04c4-216">Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="f04c4-216">Cosmos DB</span></span>](functions-bindings-documentdb.md)
- [<span data-ttu-id="f04c4-217">SendGrid</span><span class="sxs-lookup"><span data-stu-id="f04c4-217">SendGrid</span></span>](functions-bindings-sendgrid.md)
- [<span data-ttu-id="f04c4-218">Twilio</span><span class="sxs-lookup"><span data-stu-id="f04c4-218">Twilio</span></span>](functions-bindings-twilio.md)
- [<span data-ttu-id="f04c4-219">Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="f04c4-219">Notification Hubs</span></span>](functions-bindings-notification-hubs.md)
- [<span data-ttu-id="f04c4-220">Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="f04c4-220">Mobile Apps</span></span>](functions-bindings-mobile-apps.md)
- [<span data-ttu-id="f04c4-221">Dış dosya</span><span class="sxs-lookup"><span data-stu-id="f04c4-221">External file</span></span>](functions-bindings-external-file.md)
