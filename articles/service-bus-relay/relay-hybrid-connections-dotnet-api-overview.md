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
# <a name="azure-relay-hybrid-connections-net-standard-api-overview"></a><span data-ttu-id="36f37-103">Azure geçişi karma bağlantıları .NET standart API genel bakış</span><span class="sxs-lookup"><span data-stu-id="36f37-103">Azure Relay Hybrid Connections .NET Standard API overview</span></span>

<span data-ttu-id="36f37-104">Bu makalede Azure geçişi karma bağlantıları .NET standart hello anahtar özetlenmektedir [istemci API](/dotnet/api/microsoft.azure.relay).</span><span class="sxs-lookup"><span data-stu-id="36f37-104">This article summarizes some of hello key Azure Relay Hybrid Connections .NET Standard [client APIs](/dotnet/api/microsoft.azure.relay).</span></span>
  
## <a name="relay-connection-string-builder"></a><span data-ttu-id="36f37-105">Geçiş bağlantı dizesi Oluşturucusu</span><span class="sxs-lookup"><span data-stu-id="36f37-105">Relay Connection String Builder</span></span>

<span data-ttu-id="36f37-106">Merhaba [RelayConnectionStringBuilder] [ RelayConnectionStringBuilder] sınıfı belirli tooRelay karma bağlantılar bağlantı dizeleri biçimlendirir.</span><span class="sxs-lookup"><span data-stu-id="36f37-106">hello [RelayConnectionStringBuilder][RelayConnectionStringBuilder] class formats connection strings that are specific tooRelay Hybrid Connections.</span></span> <span data-ttu-id="36f37-107">Bir bağlantı dizesi veya toobuild sıfırdan bir bağlantı dizesi tooverify hello biçimini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="36f37-107">You can use it tooverify hello format of a connection string, or toobuild a connection string from scratch.</span></span> <span data-ttu-id="36f37-108">Aşağıdaki kod örneği için hello bakın:</span><span class="sxs-lookup"><span data-stu-id="36f37-108">See hello following code for an example:</span></span>

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

<span data-ttu-id="36f37-109">Bir bağlantı geçebilen doğrudan toohello dize `RelayConnectionStringBuilder` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="36f37-109">You can also pass a connection string directly toohello `RelayConnectionStringBuilder` method.</span></span> <span data-ttu-id="36f37-110">Bu işlem hello bağlantı dizesi geçerli bir biçimde olduğunu tooverify sağlar.</span><span class="sxs-lookup"><span data-stu-id="36f37-110">This operation enables you tooverify that hello connection string is in a valid format.</span></span> <span data-ttu-id="36f37-111">Merhaba parametrelerinden herhangi biri geçersiz, hello Oluşturucusu oluşturur. bir `ArgumentException`.</span><span class="sxs-lookup"><span data-stu-id="36f37-111">If any of hello parameters are invalid, hello constructor generates an `ArgumentException`.</span></span>

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

## <a name="hybrid-connection-stream"></a><span data-ttu-id="36f37-112">Karma bağlantı akışı</span><span class="sxs-lookup"><span data-stu-id="36f37-112">Hybrid Connection Stream</span></span>
<span data-ttu-id="36f37-113">Merhaba [HybridConnectionStream] [ HCStream] sınıfının hello kullanılan birincil nesnesi toosend olması ve çalıştığınız olup olmadığını verileri bir Azure geçiş uç noktasından almak bir [HybridConnectionClient] [ HCClient], veya bir [HybridConnectionListener][HCListener].</span><span class="sxs-lookup"><span data-stu-id="36f37-113">hello [HybridConnectionStream][HCStream] class is hello primary object used toosend and receive data from an Azure Relay endpoint, whether you are working with a [HybridConnectionClient][HCClient], or a [HybridConnectionListener][HCListener].</span></span>

### <a name="getting-a-hybrid-connection-stream"></a><span data-ttu-id="36f37-114">Karma bağlantı akışı alma</span><span class="sxs-lookup"><span data-stu-id="36f37-114">Getting a Hybrid Connection Stream</span></span>

#### <a name="listener"></a><span data-ttu-id="36f37-115">Dinleyici</span><span class="sxs-lookup"><span data-stu-id="36f37-115">Listener</span></span>
<span data-ttu-id="36f37-116">Kullanarak bir [HybridConnectionListener][HCListener], elde edebilirsiniz bir `HybridConnectionStream` gibi nesnesi:</span><span class="sxs-lookup"><span data-stu-id="36f37-116">Using a [HybridConnectionListener][HCListener], you can obtain a `HybridConnectionStream` object as follows:</span></span>

```csharp
// Use hello RelayConnectionStringBuilder tooget a valid connection string
var listener = new HybridConnectionListener(csb.ToString());
// Open a connection toohello Relay endpoint
await listener.OpenAsync();
// Get a `HybridConnectionStream`
var hybridConnectionStream = await listener.AcceptConnectionAsync();
```

#### <a name="client"></a><span data-ttu-id="36f37-117">İstemci</span><span class="sxs-lookup"><span data-stu-id="36f37-117">Client</span></span>
<span data-ttu-id="36f37-118">Kullanarak bir [HybridConnectionClient][HCClient], elde edebilirsiniz bir `HybridConnectionStream` gibi nesnesi:</span><span class="sxs-lookup"><span data-stu-id="36f37-118">Using a [HybridConnectionClient][HCClient], you can obtain a `HybridConnectionStream` object as follows:</span></span>

```csharp
// Use hello RelayConnectionStringBuilder tooget a valid connection string
var client = new HybridConnectionClient(csb.ToString());
// Open a connection toohello Relay endpoint and get a `HybridConnectionStream`
var hybridConnectionStream = await client.CreateConnectionAsync();
```

### <a name="receiving-data"></a><span data-ttu-id="36f37-119">Veri alma</span><span class="sxs-lookup"><span data-stu-id="36f37-119">Receiving data</span></span>
<span data-ttu-id="36f37-120">Merhaba [HybridConnectionStream] [ HCStream] sınıfı iki yönlü iletişim sağlar.</span><span class="sxs-lookup"><span data-stu-id="36f37-120">hello [HybridConnectionStream][HCStream] class enables two-way communication.</span></span> <span data-ttu-id="36f37-121">Çoğu durumda, sürekli olarak hello akıştan alırsınız.</span><span class="sxs-lookup"><span data-stu-id="36f37-121">In most cases, you continuously receive from hello stream.</span></span> <span data-ttu-id="36f37-122">Merhaba akışından metin okuma, ayrıca toouse isteyebilirsiniz bir [StreamReader](https://msdn.microsoft.com/library/system.io.streamreader(v=vs.110).aspx) daha kolay hello verilerini ayrıştırma sağlayan nesne.</span><span class="sxs-lookup"><span data-stu-id="36f37-122">If you are reading text from hello stream, you may also want toouse a [StreamReader](https://msdn.microsoft.com/library/system.io.streamreader(v=vs.110).aspx) object, which enables easier parsing of hello data.</span></span> <span data-ttu-id="36f37-123">Örneğin, metin olarak yerine olarak verileri okuyabilir `byte[]`.</span><span class="sxs-lookup"><span data-stu-id="36f37-123">For example, you can read data as text, rather than as `byte[]`.</span></span>

<span data-ttu-id="36f37-124">İptal istendi kadar hello aşağıdaki kodu tek tek satırlık metin hello akıştan okur:</span><span class="sxs-lookup"><span data-stu-id="36f37-124">hello following code reads individual lines of text from hello stream until a cancellation is requested:</span></span>

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

### <a name="sending-data"></a><span data-ttu-id="36f37-125">Verileri gönderme</span><span class="sxs-lookup"><span data-stu-id="36f37-125">Sending data</span></span>
<span data-ttu-id="36f37-126">Bir bağlantı kuruldu olduktan sonra bir ileti toohello geçiş uç noktası gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="36f37-126">Once you have a connection established, you can send a message toohello Relay endpoint.</span></span> <span data-ttu-id="36f37-127">Merhaba bağlantı nesnesi devralındığından [akış](https://msdn.microsoft.com/library/system.io.stream(v=vs.110).aspx), verilerinizi olarak gönderme bir `byte[]`.</span><span class="sxs-lookup"><span data-stu-id="36f37-127">Because hello connection object inherits [Stream](https://msdn.microsoft.com/library/system.io.stream(v=vs.110).aspx), send your data as a `byte[]`.</span></span> <span data-ttu-id="36f37-128">örnekte gösterildiği nasıl aşağıdaki hello toodo bu:</span><span class="sxs-lookup"><span data-stu-id="36f37-128">hello following example shows how toodo this:</span></span>

```csharp
var data = Encoding.UTF8.GetBytes("hello");
await clientConnection.WriteAsync(data, 0, data.Length);
```

<span data-ttu-id="36f37-129">Ancak, toosend metin doğrudan, her zaman tooencode hello dize gerek kalmadan istiyorsanız hello kayabilir `hybridConnectionStream` nesnesi ile bir [StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx) nesnesi.</span><span class="sxs-lookup"><span data-stu-id="36f37-129">However, if you want toosend text directly, without needing tooencode hello string each time, you can wrap hello `hybridConnectionStream` object with a [StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx) object.</span></span>

```csharp
// hello StreamWriter object only needs toobe created once
var textWriter = new StreamWriter(hybridConnectionStream);
await textWriter.WriteLineAsync("hello");
```

## <a name="next-steps"></a><span data-ttu-id="36f37-130">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="36f37-130">Next steps</span></span>
<span data-ttu-id="36f37-131">toolearn Azure geçişi hakkında daha fazla bilgi için bu bağlantıları ziyaret edin:</span><span class="sxs-lookup"><span data-stu-id="36f37-131">toolearn more about Azure Relay, visit these links:</span></span>

* [<span data-ttu-id="36f37-132">Microsoft.Azure.Relay başvurusu</span><span class="sxs-lookup"><span data-stu-id="36f37-132">Microsoft.Azure.Relay reference</span></span>](/dotnet/api/microsoft.azure.relay)
* [<span data-ttu-id="36f37-133">Azure Geçiş nedir?</span><span class="sxs-lookup"><span data-stu-id="36f37-133">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="36f37-134">Kullanılabilir geçiş API'leri</span><span class="sxs-lookup"><span data-stu-id="36f37-134">Available Relay APIs</span></span>](relay-api-overview.md)

[RelayConnectionStringBuilder]: /dotnet/api/microsoft.azure.relay.relayconnectionstringbuilder
[HCStream]: /dotnet/api/microsoft.azure.relay.hybridconnectionstream
[HCClient]: /dotnet/api/microsoft.azure.relay.hybridconnectionclient
[HCListener]: /dotnet/api/microsoft.azure.relay.hybridconnectionlistener