---
title: "aaaAzure işlevleri Mobile Apps bağlamaları | Microsoft Docs"
description: "Anlamak nasıl toouse Azure Mobile Apps bağlamaları Azure işlevlerinde."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
keywords: "Azure işlevleri, İşlevler, olay işleme dinamik işlem sunucusuz mimarisi"
ms.assetid: faad1263-0fa5-41a9-964f-aecbc0be706a
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 10/31/2016
ms.author: glenga
ms.openlocfilehash: d3679a5d5c66705b32e422ec17e3a1e6d6ac063c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-mobile-apps-bindings"></a>Azure işlevleri Mobile Apps bağlamaları
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

Bu makalede açıklanır nasıl tooconfigure ve kod [Azure Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) Azure işlevlerinde bağlar. Giriş ve Mobile Apps için bağlamaları çıktı Azure işlevleri destekler.

Merhaba Mobile Apps giriş ve çıkış bağlamaları izin [okuma ve yazma toodata tabloları](../app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations) mobil uygulamanızda.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="input"></a>

## <a name="mobile-apps-input-binding"></a>Mobile Apps giriş bağlama
Merhaba Mobile Apps giriş bağlaması bir kaydı bir mobil tablo uç noktasından yükler ve işlevinizin geçirir. C# ve F # işlevleri herhangi bir yapılan değişiklikler toohello kaydı otomatik olarak gönderilir geri toohello tablo hello işlevi başarıyla çıktığında.

Merhaba Mobile Apps giriş tooa işlevini kullanan hello JSON nesnesinde aşağıdaki hello `bindings` function.json dizisi:

```json
{
    "name": "<Name of input parameter in function signature>",
    "type": "mobileTable",
    "tableName": "<Name of your mobile app's data table>",
    "id" : "<Id of hello record tooretrieve - see below>",
    "connection": "<Name of app setting that has your mobile app's URL - see below>",
    "apiKey": "<Name of app setting that has your mobile app's API key - see below>",
    "direction": "in"
}
```

Merhaba aşağıdakileri göz önünde bulundurun:

* `id`Merhaba işlevi çağırır hello Tetikle dayanabilir veya statik olabilir. Kullanırsanız, örneğin, bir [sıra tetikleyici]() , işlev, ardından `"id": "{queueTrigger}"` kullandığı hello hello kuyruk iletisini dize değerini kayıt kimliği tooretrieve hello gibi.
* `connection`bir uygulama ayarı sırayla mobil uygulamanızı hello URL'sini içeren işlevi uygulamanızda Hello adını içermelidir. Bu URL tooconstruct gerekli hello REST işlemlerini mobil uygulamanızı karşı Hello işlevini kullanır. [İşlevi uygulamanıza bir uygulama ayarı oluşturmak]() , mobil uygulamanızın URL'si içeren (gibi görünen `http://<appname>.azurewebsites.net`), ardından hello hello uygulama ayarı hello adını belirtin `connection` giriş bağlaması özelliği. 
* Toospecify gerek `apiKey` varsa, [bir API anahtarı, Node.js mobil uygulama arka ucuna uygulamak](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), veya [bir API anahtarı, .NET Mobil uygulama arka ucuna uygulamak](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key). toodo bunu, [işlevi uygulamanıza bir uygulama ayarı oluşturmak]() hello API anahtarı içeren, hello eklemek `apiKey` giriş bağlamanız hello uygulama ayarı hello adıyla bir özellik. 
  
  > [!IMPORTANT]
  > Bu API anahtarı ile mobil uygulama istemcilerinizi paylaşılmayan gerekir. Yalnızca Azure işlevleri gibi dağıtılmış güvenli bir şekilde tooservice tarafı istemcileri olması gerekir. 
  > 
  > [!NOTE]
  > Azure işlevleri depolar bağlantı bilgilerini ve API anahtarlarını uygulama ayarlarda böylece kaynak denetimi deponuzun denetlenmez. Bu, hassas bilgilerinizi koruma sağlar.
  > 
  > 

<a name="inputusage"></a>

## <a name="input-usage"></a>Giriş kullanımı
Bu bölümde, işlev kodunuzda bağlama toouse mobil uygulamalarınızı nasıl giriş gösterir. 

Merhaba Hello kaydıyla tablo ve kayıt kimliği bulundu belirtildiğinde adlı hello geçirilir [JObject](http://www.newtonsoft.com/json/help/html/t_newtonsoft_json_linq_jobject.htm) parametresi (veya Node.js içinde hello geçirilir `context.bindings.<name>` nesnesi). Merhaba kayıt bulunamadı, hello parametredir `null`. 

C# ve F # işlevleri giriş toohello kaydı (giriş parametresi) yaptığınız tüm değişiklikler otomatik olarak gönderilen geri toohello Mobile Apps tablo hello işlevi başarıyla çıktığında. Node.js işlevlerini kullanmak `context.bindings.<name>` tooaccess hello Giriş kaydı. Node.js kaydında değiştiremezsiniz.

<a name="inputsample"></a>

## <a name="input-sample"></a>Giriş örneği
Function.json aşağıdaki hello olduğunu varsayalım, bir mobil uygulama tablosu kaydı hello kuyruk tetikleyici iletisi hello kimliği alır:

```json
{
"bindings": [
    {
    "name": "myQueueItem",
    "queueName": "myqueue-items",
    "connection":"",
    "type": "queueTrigger",
    "direction": "in"
    },
    {
        "name": "record",
        "type": "mobileTable",
        "tableName": "MyTable",
        "id" : "{queueTrigger}",
        "connection": "My_MobileApp_Url",
        "apiKey": "My_MobileApp_Key",
        "direction": "in"
    }
],
"disabled": false
}
```

Merhaba bağlama girdi kaydından hello kullanan hello dile özgü örneğine bakın. Merhaba C# ve F # örnekleri ayrıca hello kaydın değişiklik `text` özelliği.

* [C#](#inputcsharp)
* [Node.js](#inputnodejs)

<a name="inputcsharp"></a>

### <a name="input-sample-in-c"></a>C# giriş örneği #

```cs
#r "Newtonsoft.Json"    
using Newtonsoft.Json.Linq;

public static void Run(string myQueueItem, JObject record)
{
    if (record != null)
    {
        record["Text"] = "This has changed.";
    }    
}
```

<!--
<a name="inputfsharp"></a>
### Input sample in F# ## 

```fsharp
#r "Newtonsoft.Json"    
open Newtonsoft.Json.Linq
let Run(myQueueItem: string, record: JObject) =
  inputDocument?text <- "This has changed."
```
-->

<a name="inputnodejs"></a>

### <a name="input-sample-in-nodejs"></a>Node.js giriş örneği

```javascript
module.exports = function (context, myQueueItem) {    
    context.log(context.bindings.record);
    context.done();
};
```

<a name="output"></a>

## <a name="mobile-apps-output-binding"></a>Mobile Apps bağlama çıktı
Merhaba Mobile Apps çıkış bağlama toowrite yeni bir kayıt tooa Mobile Apps tablo uç noktası kullanın.  

Merhaba Mobile Apps hello JSON nesnesinde aşağıdaki hello işlevi kullanan çıktısı `bindings` function.json dizisi:

```json
{
    "name": "<Name of output parameter in function signature>",
    "type": "mobileTable",
    "tableName": "<Name of your mobile app's data table>",
    "connection": "<Name of app setting that has your mobile app's URL - see below>",
    "apiKey": "<Name of app setting that has your mobile app's API key - see below>",
    "direction": "out"
}
```

Merhaba aşağıdakileri göz önünde bulundurun:

* `connection`bir uygulama ayarı sırayla mobil uygulamanızı hello URL'sini içeren işlevi uygulamanızda Hello adını içermelidir. Bu URL tooconstruct gerekli hello REST işlemlerini mobil uygulamanızı karşı Hello işlevini kullanır. [İşlevi uygulamanıza bir uygulama ayarı oluşturmak]() , mobil uygulamanızın URL'si içeren (gibi görünen `http://<appname>.azurewebsites.net`), ardından hello hello uygulama ayarı hello adını belirtin `connection` giriş bağlaması özelliği. 
* Toospecify gerek `apiKey` varsa, [bir API anahtarı, Node.js mobil uygulama arka ucuna uygulamak](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), veya [bir API anahtarı, .NET Mobil uygulama arka ucuna uygulamak](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key). toodo bunu, [işlevi uygulamanıza bir uygulama ayarı oluşturmak]() hello API anahtarı içeren, hello eklemek `apiKey` giriş bağlamanız hello uygulama ayarı hello adıyla bir özellik. 
  
  > [!IMPORTANT]
  > Bu API anahtarı ile mobil uygulama istemcilerinizi paylaşılmayan gerekir. Yalnızca Azure işlevleri gibi dağıtılmış güvenli bir şekilde tooservice tarafı istemcileri olması gerekir. 
  > 
  > [!NOTE]
  > Azure işlevleri depolar bağlantı bilgilerini ve API anahtarlarını uygulama ayarlarda böylece kaynak denetimi deponuzun denetlenmez. Bu, hassas bilgilerinizi koruma sağlar.
  > 
  > 

<a name="outputusage"></a>

## <a name="output-usage"></a>Çıktı kullanımı
Bu bölümde işlevi kodunuzda bağlama toouse mobil uygulamalarınızı nasıl çıktısını gösterir. 

C# işlevlerde, türünde bir adlandırılmış çıktı parametresi kullanın `out object` tooaccess hello çıkış kaydı. Node.js işlevlerini kullanmak `context.bindings.<name>` tooaccess hello çıkış kaydı.

<a name="outputsample"></a>

## <a name="output-sample"></a>Çıkış örneği
Bir kuyruk tetikleyici ve Mobile Apps çıkış tanımlayan function.json aşağıdaki hello olduğunu varsayalım:

```json
{
"bindings": [
    {
    "name": "myQueueItem",
    "queueName": "myqueue-items",
    "connection":"",
    "type": "queueTrigger",
    "direction": "in"
    },
    {
    "name": "record",
    "type": "mobileTable",
    "tableName": "MyTable",
    "connection": "My_MobileApp_Url",
    "apiKey": "My_MobileApp_Key",
    "direction": "out"
    }
],
"disabled": false
}
```

Merhaba Mobile Apps tablo endpoint hello kuyruk iletisi Merhaba içeriğine sahip bir kayıt oluşturur hello dile özgü örneğine bakın.

* [C#](#outcsharp)
* [Node.js](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a>C# çıktı örneği #

```cs
public static void Run(string myQueueItem, out object record)
{
    record = new {
        Text = $"I'm running in a C# function! {myQueueItem}"
    };
}
```

<!--
<a name="outfsharp"></a>
### Output sample in F# ## 
```fsharp

```
-->
<a name="outnodejs"></a>

### <a name="output-sample-in-nodejs"></a>Node.js çıktı örneği

```javascript
module.exports = function (context, myQueueItem) {

    context.bindings.record = {
        text : "I'm running in a Node function! Data: '" + myQueueItem + "'"
    }   

    context.done();
};
```

## <a name="next-steps"></a>Sonraki adımlar
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

