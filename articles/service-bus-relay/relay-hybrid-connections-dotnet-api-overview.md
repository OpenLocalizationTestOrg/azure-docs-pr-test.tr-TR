---
title: "Azure geçişi .NET standart API'lerini genel bakış | Microsoft Docs"
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
ms.openlocfilehash: f3f4a2e721b1a75a5b92a5c17a9939c7013340d4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-relay-hybrid-connections-net-standard-api-overview"></a><span data-ttu-id="033ee-103">Azure geçişi karma bağlantıları .NET standart API genel bakış</span><span class="sxs-lookup"><span data-stu-id="033ee-103">Azure Relay Hybrid Connections .NET Standard API overview</span></span>

<span data-ttu-id="033ee-104">Bu makalede Azure geçişi karma bağlantıları .NET standart anahtar özetlenmektedir [istemci API](/dotnet/api/microsoft.azure.relay).</span><span class="sxs-lookup"><span data-stu-id="033ee-104">This article summarizes some of the key Azure Relay Hybrid Connections .NET Standard [client APIs](/dotnet/api/microsoft.azure.relay).</span></span>
  
## <a name="relay-connection-string-builder"></a><span data-ttu-id="033ee-105">Geçiş bağlantı dizesi Oluşturucusu</span><span class="sxs-lookup"><span data-stu-id="033ee-105">Relay Connection String Builder</span></span>

<span data-ttu-id="033ee-106">[RelayConnectionStringBuilder] [ RelayConnectionStringBuilder] sınıfı geçişi karma bağlantılar için belirli bağlantı dizeleri biçimlendirir.</span><span class="sxs-lookup"><span data-stu-id="033ee-106">The [RelayConnectionStringBuilder][RelayConnectionStringBuilder] class formats connection strings that are specific to Relay Hybrid Connections.</span></span> <span data-ttu-id="033ee-107">Bir bağlantı dizesi biçimi doğrulamak için ya da sıfırdan bir bağlantı dizesi oluşturmak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="033ee-107">You can use it to verify the format of a connection string, or to build a connection string from scratch.</span></span> <span data-ttu-id="033ee-108">Aşağıdaki kod örneği için bkz:</span><span class="sxs-lookup"><span data-stu-id="033ee-108">See the following code for an example:</span></span>

```csharp
var endpoint = "{Relay namespace}";
var entityPath = "{Name of the Hybrid Connection}";
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

<span data-ttu-id="033ee-109">Doğrudan bir bağlantı dizesi geçirebilirsiniz `RelayConnectionStringBuilder` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="033ee-109">You can also pass a connection string directly to the `RelayConnectionStringBuilder` method.</span></span> <span data-ttu-id="033ee-110">Bu işlem, bağlantı dizesi geçerli bir biçimde olduğunu doğrulamak sağlar.</span><span class="sxs-lookup"><span data-stu-id="033ee-110">This operation enables you to verify that the connection string is in a valid format.</span></span> <span data-ttu-id="033ee-111">Parametrelerden biri geçersiz olan Oluşturucusu oluşturur bir `ArgumentException`.</span><span class="sxs-lookup"><span data-stu-id="033ee-111">If any of the parameters are invalid, the constructor generates an `ArgumentException`.</span></span>

```csharp
var myConnectionString = "{RelayConnectionString}";
// Declare the connectionStringBuilder so that it can be used outside of the loop if needed
RelayConnectionStringBuilder connectionStringBuilder;
try
{
    // Create the connectionStringBuilder using the supplied connection string
    connectionStringBuilder = new RelayConnectionStringBuilder(myConnectionString);
}
catch (ArgumentException ae)
{
    // Perform some error handling
}
```

## <a name="hybrid-connection-stream"></a><span data-ttu-id="033ee-112">Karma bağlantı akışı</span><span class="sxs-lookup"><span data-stu-id="033ee-112">Hybrid Connection Stream</span></span>
<span data-ttu-id="033ee-113">[HybridConnectionStream] [ HCStream] sınıftır çalıştığınız olup olmadığını veri göndermek ve bir Azure geçiş uç noktasından almak için kullanılan birincil nesne bir [HybridConnectionClient] [ HCClient], veya bir [HybridConnectionListener][HCListener].</span><span class="sxs-lookup"><span data-stu-id="033ee-113">The [HybridConnectionStream][HCStream] class is the primary object used to send and receive data from an Azure Relay endpoint, whether you are working with a [HybridConnectionClient][HCClient], or a [HybridConnectionListener][HCListener].</span></span>

### <a name="getting-a-hybrid-connection-stream"></a><span data-ttu-id="033ee-114">Karma bağlantı akışı alma</span><span class="sxs-lookup"><span data-stu-id="033ee-114">Getting a Hybrid Connection Stream</span></span>

#### <a name="listener"></a><span data-ttu-id="033ee-115">Dinleyici</span><span class="sxs-lookup"><span data-stu-id="033ee-115">Listener</span></span>
<span data-ttu-id="033ee-116">Kullanarak bir [HybridConnectionListener][HCListener], elde edebilirsiniz bir `HybridConnectionStream` gibi nesnesi:</span><span class="sxs-lookup"><span data-stu-id="033ee-116">Using a [HybridConnectionListener][HCListener], you can obtain a `HybridConnectionStream` object as follows:</span></span>

```csharp
// Use the RelayConnectionStringBuilder to get a valid connection string
var listener = new HybridConnectionListener(csb.ToString());
// Open a connection to the Relay endpoint
await listener.OpenAsync();
// Get a `HybridConnectionStream`
var hybridConnectionStream = await listener.AcceptConnectionAsync();
```

#### <a name="client"></a><span data-ttu-id="033ee-117">İstemci</span><span class="sxs-lookup"><span data-stu-id="033ee-117">Client</span></span>
<span data-ttu-id="033ee-118">Kullanarak bir [HybridConnectionClient][HCClient], elde edebilirsiniz bir `HybridConnectionStream` gibi nesnesi:</span><span class="sxs-lookup"><span data-stu-id="033ee-118">Using a [HybridConnectionClient][HCClient], you can obtain a `HybridConnectionStream` object as follows:</span></span>

```csharp
// Use the RelayConnectionStringBuilder to get a valid connection string
var client = new HybridConnectionClient(csb.ToString());
// Open a connection to the Relay endpoint and get a `HybridConnectionStream`
var hybridConnectionStream = await client.CreateConnectionAsync();
```

### <a name="receiving-data"></a><span data-ttu-id="033ee-119">Veri alma</span><span class="sxs-lookup"><span data-stu-id="033ee-119">Receiving data</span></span>
<span data-ttu-id="033ee-120">[HybridConnectionStream] [ HCStream] sınıfı iki yönlü iletişim sağlar.</span><span class="sxs-lookup"><span data-stu-id="033ee-120">The [HybridConnectionStream][HCStream] class enables two-way communication.</span></span> <span data-ttu-id="033ee-121">Çoğu durumda, sürekli olarak akıştan alırsınız.</span><span class="sxs-lookup"><span data-stu-id="033ee-121">In most cases, you continuously receive from the stream.</span></span> <span data-ttu-id="033ee-122">Akıştan metin okuma, ayrıca kullanmak istediğiniz bir [StreamReader](https://msdn.microsoft.com/library/system.io.streamreader(v=vs.110).aspx) daha kolay verilerini ayrıştırma sağlayan nesne.</span><span class="sxs-lookup"><span data-stu-id="033ee-122">If you are reading text from the stream, you may also want to use a [StreamReader](https://msdn.microsoft.com/library/system.io.streamreader(v=vs.110).aspx) object, which enables easier parsing of the data.</span></span> <span data-ttu-id="033ee-123">Örneğin, metin olarak yerine olarak verileri okuyabilir `byte[]`.</span><span class="sxs-lookup"><span data-stu-id="033ee-123">For example, you can read data as text, rather than as `byte[]`.</span></span>

<span data-ttu-id="033ee-124">İptal istendi kadar aşağıdaki kodu tek tek satırlık metin akıştan okur:</span><span class="sxs-lookup"><span data-stu-id="033ee-124">The following code reads individual lines of text from the stream until a cancellation is requested:</span></span>

```csharp
// Create a CancellationToken, so that we can cancel the while loop
var cancellationToken = new CancellationToken();
// Create a StreamReader from the 'hybridConnectionStream`
var streamReader = new StreamReader(hybridConnectionStream);

while (!cancellationToken.IsCancellationRequested)
{
    // Read a line of input until a newline is encountered
    var line = await streamReader.ReadLineAsync();
    if (string.IsNullOrEmpty(line))
    {
        // If there's no input data, we will signal that 
        // we will no longer send data on this connection
        // and then break out of the processing loop.
        await hybridConnectionStream.ShutdownAsync(cancellationToken);
        break;
    }
}
```

### <a name="sending-data"></a><span data-ttu-id="033ee-125">Verileri gönderme</span><span class="sxs-lookup"><span data-stu-id="033ee-125">Sending data</span></span>
<span data-ttu-id="033ee-126">Bir bağlantı kuruldu olduktan sonra geçiş uç noktasına bir ileti gönderebilir.</span><span class="sxs-lookup"><span data-stu-id="033ee-126">Once you have a connection established, you can send a message to the Relay endpoint.</span></span> <span data-ttu-id="033ee-127">Bağlantı nesnesi devralındığından [akış](https://msdn.microsoft.com/library/system.io.stream(v=vs.110).aspx), verilerinizi olarak gönderme bir `byte[]`.</span><span class="sxs-lookup"><span data-stu-id="033ee-127">Because the connection object inherits [Stream](https://msdn.microsoft.com/library/system.io.stream(v=vs.110).aspx), send your data as a `byte[]`.</span></span> <span data-ttu-id="033ee-128">Aşağıdaki örnek, bunun nasıl yapılacağı gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="033ee-128">The following example shows how to do this:</span></span>

```csharp
var data = Encoding.UTF8.GetBytes("hello");
await clientConnection.WriteAsync(data, 0, data.Length);
```

<span data-ttu-id="033ee-129">Metin her zaman dizesini kodlayın gerek kalmadan doğrudan göndermek istiyorsanız, ancak kayabilir `hybridConnectionStream` nesnesi ile bir [StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx) nesnesi.</span><span class="sxs-lookup"><span data-stu-id="033ee-129">However, if you want to send text directly, without needing to encode the string each time, you can wrap the `hybridConnectionStream` object with a [StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx) object.</span></span>

```csharp
// The StreamWriter object only needs to be created once
var textWriter = new StreamWriter(hybridConnectionStream);
await textWriter.WriteLineAsync("hello");
```

## <a name="next-steps"></a><span data-ttu-id="033ee-130">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="033ee-130">Next steps</span></span>
<span data-ttu-id="033ee-131">Azure geçişi hakkında daha fazla bilgi için bu bağlantıları ziyaret edin:</span><span class="sxs-lookup"><span data-stu-id="033ee-131">To learn more about Azure Relay, visit these links:</span></span>

* [<span data-ttu-id="033ee-132">Microsoft.Azure.Relay başvurusu</span><span class="sxs-lookup"><span data-stu-id="033ee-132">Microsoft.Azure.Relay reference</span></span>](/dotnet/api/microsoft.azure.relay)
* [<span data-ttu-id="033ee-133">Azure Geçiş nedir?</span><span class="sxs-lookup"><span data-stu-id="033ee-133">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="033ee-134">Kullanılabilir geçiş API'leri</span><span class="sxs-lookup"><span data-stu-id="033ee-134">Available Relay APIs</span></span>](relay-api-overview.md)

[RelayConnectionStringBuilder]: /dotnet/api/microsoft.azure.relay.relayconnectionstringbuilder
[HCStream]: /dotnet/api/microsoft.azure.relay.hybridconnectionstream
[HCClient]: /dotnet/api/microsoft.azure.relay.hybridconnectionclient
[HCListener]: /dotnet/api/microsoft.azure.relay.hybridconnectionlistener