---
title: "hello Azure geçiş .NET standart API'leri aaaOverview | Microsoft Docs"
description: ".NET standart API genel bakış geçiş"
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: b1da9ac1-811b-4df7-a22c-ccd013405c40
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/05/2017
ms.author: sethm
ms.openlocfilehash: c90e00e809bd44eb0fbbff5eb03dfc8afa486523
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-relay-hybrid-connections-net-standard-api-overview"></a>Azure geçişi karma bağlantıları .NET standart API genel bakış

Bu makalede Azure geçişi karma bağlantıları .NET standart hello anahtar özetlenmektedir [istemci API](/dotnet/api/microsoft.azure.relay).
  
## <a name="relay-connection-string-builder"></a>Geçiş bağlantı dizesi Oluşturucusu

Merhaba [RelayConnectionStringBuilder] [ RelayConnectionStringBuilder] sınıfı belirli tooRelay karma bağlantılar bağlantı dizeleri biçimlendirir. Bir bağlantı dizesi veya toobuild sıfırdan bir bağlantı dizesi tooverify hello biçimini kullanabilirsiniz. Aşağıdaki kod örneği için hello bakın:

```csharp
var endpoint = "{Relay namespace}";
var entityPath = "{Name of hello Hybrid Connection}";
var sharedAccessKeyName = "{SAS key name}";
var sharedAccessKey = "{SAS key value}";

var connectionStringBuilder = new RelayConnectionStringBuilder()
{
    Endpoint = endpoint,
    EntityPath = entityPath,
    SharedAccessKeyName = sasKeyName,
    SharedAccessKey = sasKeyValue
};
```

Bir bağlantı geçebilen doğrudan toohello dize `RelayConnectionStringBuilder` yöntemi. Bu işlem hello bağlantı dizesi geçerli bir biçimde olduğunu tooverify sağlar. Merhaba parametrelerinden herhangi biri geçersiz, hello Oluşturucusu oluşturur. bir `ArgumentException`.

```csharp
var myConnectionString = "{RelayConnectionString}";
// Declare hello connectionStringBuilder so that it can be used outside of hello loop if needed
RelayConnectionStringBuilder connectionStringBuilder;
try
{
    // Create hello connectionStringBuilder using hello supplied connection string
    connectionStringBuilder = new RelayConnectionStringBuilder(myConnectionString);
}
catch (ArgumentException ae)
{
    // Perform some error handling
}
```

## <a name="hybrid-connection-stream"></a>Karma bağlantı akışı
Merhaba [HybridConnectionStream] [ HCStream] sınıfının hello kullanılan birincil nesnesi toosend olması ve çalıştığınız olup olmadığını verileri bir Azure geçiş uç noktasından almak bir [HybridConnectionClient] [ HCClient], veya bir [HybridConnectionListener][HCListener].

### <a name="getting-a-hybrid-connection-stream"></a>Karma bağlantı akışı alma

#### <a name="listener"></a>Dinleyici
Kullanarak bir [HybridConnectionListener][HCListener], elde edebilirsiniz bir `HybridConnectionStream` gibi nesnesi:

```csharp
// Use hello RelayConnectionStringBuilder tooget a valid connection string
var listener = new HybridConnectionListener(csb.ToString());
// Open a connection toohello Relay endpoint
await listener.OpenAsync();
// Get a `HybridConnectionStream`
var hybridConnectionStream = await listener.AcceptConnectionAsync();
```

#### <a name="client"></a>İstemci
Kullanarak bir [HybridConnectionClient][HCClient], elde edebilirsiniz bir `HybridConnectionStream` gibi nesnesi:

```csharp
// Use hello RelayConnectionStringBuilder tooget a valid connection string
var client = new HybridConnectionClient(csb.ToString());
// Open a connection toohello Relay endpoint and get a `HybridConnectionStream`
var hybridConnectionStream = await client.CreateConnectionAsync();
```

### <a name="receiving-data"></a>Veri alma
Merhaba [HybridConnectionStream] [ HCStream] sınıfı iki yönlü iletişim sağlar. Çoğu durumda, sürekli olarak hello akıştan alırsınız. Merhaba akışından metin okuma, ayrıca toouse isteyebilirsiniz bir [StreamReader](https://msdn.microsoft.com/library/system.io.streamreader(v=vs.110).aspx) daha kolay hello verilerini ayrıştırma sağlayan nesne. Örneğin, metin olarak yerine olarak verileri okuyabilir `byte[]`.

İptal istendi kadar hello aşağıdaki kodu tek tek satırlık metin hello akıştan okur:

```csharp
// Create a CancellationToken, so that we can cancel hello while loop
var cancellationToken = new CancellationToken();
// Create a StreamReader from hello 'hybridConnectionStream`
var streamReader = new StreamReader(hybridConnectionStream);

while (!cancellationToken.IsCancellationRequested)
{
    // Read a line of input until a newline is encountered
    var line = await streamReader.ReadLineAsync();
    if (string.IsNullOrEmpty(line))
    {
        // If there's no input data, we will signal that 
        // we will no longer send data on this connection
        // and then break out of hello processing loop.
        await hybridConnectionStream.ShutdownAsync(cancellationToken);
        break;
    }
}
```

### <a name="sending-data"></a>Verileri gönderme
Bir bağlantı kuruldu olduktan sonra bir ileti toohello geçiş uç noktası gönderebilirsiniz. Merhaba bağlantı nesnesi devralındığından [akış](https://msdn.microsoft.com/library/system.io.stream(v=vs.110).aspx), verilerinizi olarak gönderme bir `byte[]`. örnekte gösterildiği nasıl aşağıdaki hello toodo bu:

```csharp
var data = Encoding.UTF8.GetBytes("hello");
await clientConnection.WriteAsync(data, 0, data.Length);
```

Ancak, toosend metin doğrudan, her zaman tooencode hello dize gerek kalmadan istiyorsanız hello kayabilir `hybridConnectionStream` nesnesi ile bir [StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx) nesnesi.

```csharp
// hello StreamWriter object only needs toobe created once
var textWriter = new StreamWriter(hybridConnectionStream);
await textWriter.WriteLineAsync("hello");
```

## <a name="next-steps"></a>Sonraki adımlar
toolearn Azure geçişi hakkında daha fazla bilgi için bu bağlantıları ziyaret edin:

* [Microsoft.Azure.Relay başvurusu](/dotnet/api/microsoft.azure.relay)
* [Azure Geçiş nedir?](relay-what-is-it.md)
* [Kullanılabilir geçiş API'leri](relay-api-overview.md)

[RelayConnectionStringBuilder]: /dotnet/api/microsoft.azure.relay.relayconnectionstringbuilder
[HCStream]: /dotnet/api/microsoft.azure.relay.hybridconnectionstream
[HCClient]: /dotnet/api/microsoft.azure.relay.hybridconnectionclient
[HCListener]: /dotnet/api/microsoft.azure.relay.hybridconnectionlistener