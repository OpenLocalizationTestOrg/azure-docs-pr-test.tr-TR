---
title: "hello Azure Geçiş düğümü API'leri aaaOverview | Microsoft Docs"
description: "Geçiş düğümü API genel bakış"
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: b7d6e822-7c32-4cb5-a4b8-df7d009bdc85
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/05/2017
ms.author: sethm
ms.openlocfilehash: d231acc854be0eaa965dec0229cf63b08ff27067
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="relay-hybrid-connections-node-api-overview"></a><span data-ttu-id="d5e85-103">Karma bağlantılar düğümü API genel bakış geçiş</span><span class="sxs-lookup"><span data-stu-id="d5e85-103">Relay Hybrid Connections Node API overview</span></span>

## <a name="overview"></a><span data-ttu-id="d5e85-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="d5e85-104">Overview</span></span>

<span data-ttu-id="d5e85-105">Merhaba [ `hyco-ws` ](https://www.npmjs.com/package/hyco-ws) Azure geçişi karma bağlantılar için düğüm paketi üzerine kurulmuştur ve hello genişletir ['ws'](https://www.npmjs.com/package/ws) NPM paket.</span><span class="sxs-lookup"><span data-stu-id="d5e85-105">hello [`hyco-ws`](https://www.npmjs.com/package/hyco-ws) Node package for Azure Relay Hybrid Connections is built on and extends hello ['ws'](https://www.npmjs.com/package/ws) NPM package.</span></span> <span data-ttu-id="d5e85-106">Bu paket, temel pakette, tüm dışarı yeniden aktarır ve hello Azure geçiş hizmeti karma bağlantılar özelliği ile tümleştirmeyi etkinleştir yeni dışarı ekler.</span><span class="sxs-lookup"><span data-stu-id="d5e85-106">This package re-exports all exports of that base package and adds new exports that enable integration with hello Azure Relay service Hybrid Connections feature.</span></span> 

<span data-ttu-id="d5e85-107">Var olan uygulamalar, `require('ws')` bu paketle birlikte kullanabilirsiniz `require('hyco-ws')` bunun yerine, ayrıca sağlayan, bir uygulama dinleme "Merhaba güvenlik duvarı içinde" ve karma bağlantılar aracılığıyla yerel olarak üzerinden WebSocket bağlantıları için tümünü karma senaryolar aynı hello zaman.</span><span class="sxs-lookup"><span data-stu-id="d5e85-107">Existing applications that `require('ws')` can use this package with `require('hyco-ws')` instead, which also enables hybrid scenarios in which an application can listen for WebSocket connections locally from "inside hello firewall" and via Hybrid Connections, all at hello same time.</span></span>
  
## <a name="documentation"></a><span data-ttu-id="d5e85-108">Belgeler</span><span class="sxs-lookup"><span data-stu-id="d5e85-108">Documentation</span></span>

<span data-ttu-id="d5e85-109">Merhaba apı'leridir [hello ana 'ws' paketinde belgelenen](https://github.com/websockets/ws/blob/master/doc/ws.md).</span><span class="sxs-lookup"><span data-stu-id="d5e85-109">hello APIs are [documented in hello main 'ws' package](https://github.com/websockets/ws/blob/master/doc/ws.md).</span></span> <span data-ttu-id="d5e85-110">Bu makalede, bu paket, taban çizgisinden nasıl farklı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="d5e85-110">This article describes how this package differs from that baseline.</span></span> 

<span data-ttu-id="d5e85-111">Merhaba hello temel paketi ve bu 'hyco-ws' arasındaki temel farklılıklar olan aracılığıyla verilen yeni bir sunucu sınıfı ekler `require('hyco-ws').RelayedServer`ve birkaç yardımcı yöntemler.</span><span class="sxs-lookup"><span data-stu-id="d5e85-111">hello key differences between hello base package and this 'hyco-ws' is that it adds a new server class, exported via `require('hyco-ws').RelayedServer`, and a few helper methods.</span></span>

### <a name="package-helper-methods"></a><span data-ttu-id="d5e85-112">Paket yardımcı yöntemler</span><span class="sxs-lookup"><span data-stu-id="d5e85-112">Package helper methods</span></span>

<span data-ttu-id="d5e85-113">Aşağıdaki gibi başvurabilir hello paketi verme sırasında birkaç yardımcı program yöntemleri vardır:</span><span class="sxs-lookup"><span data-stu-id="d5e85-113">There are several utility methods available on hello package export that you can reference as follows:</span></span>

```JavaScript
const WebSocket = require('hyco-ws');

var listenUri = WebSocket.createRelayListenUri('namespace.servicebus.windows.net', 'path');
listenUri = WebSocket.appendRelayToken(listenUri, 'ruleName', '...key...')
...

```

<span data-ttu-id="d5e85-114">Hello yardımcı yöntemler bu paketi ile kullanmak için olan, ancak web veya aygıt istemcileri toocreate dinleyicileri veya Gönderenler etkinleştirmek için bir düğümü sunucu tarafından da kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="d5e85-114">hello helper methods are for use with this package, but can also be used by a Node server for enabling web or device clients toocreate listeners or senders.</span></span> <span data-ttu-id="d5e85-115">Merhaba sunucu kısa süreli belirteçler katıştırmak URI'ler geçirerek bu yöntemleri kullanır.</span><span class="sxs-lookup"><span data-stu-id="d5e85-115">hello server uses these methods by passing them URIs that embed short-lived tokens.</span></span> <span data-ttu-id="d5e85-116">Bu URI ayarı HTTP üstbilgilerini hello WebSocket el sıkışma için desteklemeyen ortak WebSocket yığınları ile de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="d5e85-116">These URIs can also be used with common WebSocket stacks that do not support setting HTTP headers for hello WebSocket handshake.</span></span> <span data-ttu-id="d5e85-117">URI için öncelikle bu kitaplığı dış kullanım senaryoları desteklenir hello içine yetkilendirme belirteçleri katıştırma.</span><span class="sxs-lookup"><span data-stu-id="d5e85-117">Embedding authorization tokens into hello URI is supported primarily for those library-external usage scenarios.</span></span> 

#### <a name="createrelaylistenuri"></a><span data-ttu-id="d5e85-118">createRelayListenUri</span><span class="sxs-lookup"><span data-stu-id="d5e85-118">createRelayListenUri</span></span>

```JavaScript
var uri = createRelayListenUri([namespaceName], [path], [[token]], [[id]])
```

<span data-ttu-id="d5e85-119">Verilen ad ve yol hello için geçerli bir Azure geçişi karma bağlantı dinleyici URI oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d5e85-119">Creates a valid Azure Relay Hybrid Connection listener URI for hello given namespace and path.</span></span> <span data-ttu-id="d5e85-120">Bu URI hello geçiş sürümü hello WebSocketServer sınıfı ile kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="d5e85-120">This URI can then be used with hello relay version of hello WebSocketServer class.</span></span>

- <span data-ttu-id="d5e85-121">`namespaceName`(gerekli) - etki alanı adını hello Azure geçiş ad alanı toouse hello.</span><span class="sxs-lookup"><span data-stu-id="d5e85-121">`namespaceName` (required) - hello domain-qualified name of hello Azure Relay namespace toouse.</span></span>
- <span data-ttu-id="d5e85-122">`path`(gerekli) - bu ad alanında mevcut bir Azure geçişi karma bağlantıyı adını hello.</span><span class="sxs-lookup"><span data-stu-id="d5e85-122">`path` (required) - hello name of an existing Azure Relay Hybrid Connection in that namespace.</span></span>
- <span data-ttu-id="d5e85-123">`token`(isteğe bağlı) - daha önce verilen geçiş erişim belirteci, hello dinleyicisi URI'si katıştırılmış (Merhaba aşağıdaki örneğine bakın).</span><span class="sxs-lookup"><span data-stu-id="d5e85-123">`token` (optional) - a previously issued Relay access token that is embedded in hello listener URI (see hello following example).</span></span>
- <span data-ttu-id="d5e85-124">`id`(isteğe bağlı) - istekleri uçtan uca tanılama izlemeyi sağlayan bir izleme tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="d5e85-124">`id` (optional) - a tracking identifier that enables end-to-end diagnostics tracking of requests.</span></span>

<span data-ttu-id="d5e85-125">Merhaba `token` değer isteğe bağlıdır ve olası toosend HTTP üstbilgileri hello WebSocket el sıkışması, birlikte değilse hello hello W3C WebSocket yığınına sahip olduğu gibi yalnızca kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d5e85-125">hello `token` value is optional and should only be used when it is not possible toosend HTTP headers along with hello WebSocket handshake, as is hello case with hello W3C WebSocket stack.</span></span>                  


#### <a name="createrelaysenduri"></a><span data-ttu-id="d5e85-126">createRelaySendUri</span><span class="sxs-lookup"><span data-stu-id="d5e85-126">createRelaySendUri</span></span>
 
```JavaScript
var uri = createRelaySendUri([namespaceName], [path], [[token]], [[id]])
```

<span data-ttu-id="d5e85-127">Verilen ad ve yol hello için geçerli bir Azure geçişi karma bağlantı gönderme URI oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d5e85-127">Creates a valid Azure Relay Hybrid Connection send URI for hello given namespace and path.</span></span> <span data-ttu-id="d5e85-128">Bu URI herhangi bir Web yuvası istemci ile kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="d5e85-128">This URI can be used with any WebSocket client.</span></span>

- <span data-ttu-id="d5e85-129">`namespaceName`(gerekli) - etki alanı adını hello Azure geçiş ad alanı toouse hello.</span><span class="sxs-lookup"><span data-stu-id="d5e85-129">`namespaceName` (required) - hello domain-qualified name of hello Azure Relay namespace toouse.</span></span>
- <span data-ttu-id="d5e85-130">`path`(gerekli) - bu ad alanında mevcut bir Azure geçişi karma bağlantıyı adını hello.</span><span class="sxs-lookup"><span data-stu-id="d5e85-130">`path` (required) - hello name of an existing Azure Relay Hybrid Connection in that namespace.</span></span>
- <span data-ttu-id="d5e85-131">`token`(isteğe bağlı) - hello katıştırılmış önceden düzenlenen bir geçiş erişim belirteci Gönder URI (Merhaba aşağıdaki örneğine bakın).</span><span class="sxs-lookup"><span data-stu-id="d5e85-131">`token` (optional) - a previously issued Relay access token that is embedded in hello send URI (see hello following example).</span></span>
- <span data-ttu-id="d5e85-132">`id`(isteğe bağlı) - istekleri uçtan uca tanılama izlemeyi sağlayan bir izleme tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="d5e85-132">`id` (optional) - a tracking identifier that enables end-to-end diagnostics tracking of requests.</span></span>

<span data-ttu-id="d5e85-133">Merhaba `token` değer isteğe bağlıdır ve olası toosend HTTP üstbilgileri hello WebSocket el sıkışması, birlikte değilse hello hello W3C WebSocket yığınına sahip olduğu gibi yalnızca kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d5e85-133">hello `token` value is optional and should only be used when it is not possible toosend HTTP headers along with hello WebSocket handshake, as is hello case with hello W3C WebSocket stack.</span></span>                   


#### <a name="createrelaytoken"></a><span data-ttu-id="d5e85-134">createRelayToken</span><span class="sxs-lookup"><span data-stu-id="d5e85-134">createRelayToken</span></span> 

```JavaScript
var token = createRelayToken([uri], [ruleName], [key], [[expirationSeconds]])
```

<span data-ttu-id="d5e85-135">Verilen hello hedef URI, SAS kuralı ve hello süre sonu bağımsız değişken belirtilmezse saniye veya bir saat sayısını hello geçerli anlık verilen hello için geçerli olan SAS kuralı anahtarı için bir Azure geçiş paylaşılan erişim imzası (SAS) belirteci oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d5e85-135">Creates an Azure Relay Shared Access Signature (SAS) token for hello given target URI, SAS rule, and SAS rule key that is valid for hello given number of seconds or for an hour from hello current instant if hello expiry argument is omitted.</span></span>

- <span data-ttu-id="d5e85-136">`uri`(gerekli) - hangi Merhaba verilen toobe belirtecidir URI hello.</span><span class="sxs-lookup"><span data-stu-id="d5e85-136">`uri` (required) - hello URI for which hello token is toobe issued.</span></span> <span data-ttu-id="d5e85-137">Merhaba URI normalleştirilmiş toouse hello HTTP düzenidir ve sorgu dize bilgilerini yapılandırıldıktan.</span><span class="sxs-lookup"><span data-stu-id="d5e85-137">hello URI is normalized toouse hello HTTP scheme, and query string information is stripped.</span></span>
- <span data-ttu-id="d5e85-138">`ruleName`SAS URI'si verilen hello tarafından temsil edilen ya da hello varlık için ad kural (gerekli) - veya hello için ad alanı URI ana bilgisayar bölümü tarafından hello temsil.</span><span class="sxs-lookup"><span data-stu-id="d5e85-138">`ruleName` (required) - SAS rule name for either hello entity represented by hello given URI, or for hello namespace represented by hello URI host portion.</span></span>
- <span data-ttu-id="d5e85-139">`key`(gerekli) - hello SAS kural için geçerli anahtar.</span><span class="sxs-lookup"><span data-stu-id="d5e85-139">`key` (required) - valid key for hello SAS rule.</span></span> 
- <span data-ttu-id="d5e85-140">`expirationSeconds`(isteğe bağlı) - belirteç hello oluşturulan kadar hello saniyeyi sona.</span><span class="sxs-lookup"><span data-stu-id="d5e85-140">`expirationSeconds` (optional) - hello number of seconds until hello generated token should expire.</span></span> <span data-ttu-id="d5e85-141">Belirtilmezse, hello 1 saat (3600) varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="d5e85-141">If not specified, hello default is 1 hour (3600).</span></span>

<span data-ttu-id="d5e85-142">verilen hello belirteci confers belirtilen hello ile ilişkili hello hakları süresi verilen hello için SAS kuralı.</span><span class="sxs-lookup"><span data-stu-id="d5e85-142">hello issued token confers hello rights associated with hello specified SAS rule for hello given duration.</span></span>

#### <a name="appendrelaytoken"></a><span data-ttu-id="d5e85-143">appendRelayToken</span><span class="sxs-lookup"><span data-stu-id="d5e85-143">appendRelayToken</span></span>

```JavaScript
var uri = appendRelayToken([uri], [ruleName], [key], [[expirationSeconds]])
```

<span data-ttu-id="d5e85-144">Bu bir yöntemdir işlevsel olarak eşdeğer toohello `createRelayToken` yöntemi belgelenen daha önce ancak döndürür hello belirteci doğru eklenmiş toohello giriş URI'si.</span><span class="sxs-lookup"><span data-stu-id="d5e85-144">This method is functionally equivalent toohello `createRelayToken` method documented previously, but returns hello token correctly appended toohello input URI.</span></span>

### <a name="class-wsrelayedserver"></a><span data-ttu-id="d5e85-145">Sınıf ws. RelayedServer</span><span class="sxs-lookup"><span data-stu-id="d5e85-145">Class ws.RelayedServer</span></span>

<span data-ttu-id="d5e85-146">Merhaba `hycows.RelayedServer` sınıfı, bir alternatif toohello `ws.Server` hello yerel ağda dinlemez ancak dinleme toohello Azure geçiş hizmeti temsilci sınıfı.</span><span class="sxs-lookup"><span data-stu-id="d5e85-146">hello `hycows.RelayedServer` class is an alternative toohello `ws.Server` class that does not listen on hello local network, but delegates listening toohello Azure Relay service.</span></span>

<span data-ttu-id="d5e85-147">Merhaba iki sınıflardır çoğunlukla hello kullanarak var olan bir uygulama anlamı uyumlu sözleşme `ws.Server` sınıfı değiştirilmiş toouse geçişli hello sürüm kolayca olabilir.</span><span class="sxs-lookup"><span data-stu-id="d5e85-147">hello two classes are mostly contract compatible, meaning that an existing application using hello `ws.Server` class can easily be changed toouse hello relayed version.</span></span> <span data-ttu-id="d5e85-148">Merhaba temel farklılıklar hello oluşturucusu ve hello kullanılabilir seçenekler şunlardır.</span><span class="sxs-lookup"><span data-stu-id="d5e85-148">hello main differences are in hello constructor and in hello available options.</span></span>

#### <a name="constructor"></a><span data-ttu-id="d5e85-149">Oluşturucusu</span><span class="sxs-lookup"><span data-stu-id="d5e85-149">Constructor</span></span>  

```JavaScript 
var ws = require('hyco-ws');
var server = ws.RelayedServer;

var wss = new server(
    {
        server: ws.createRelayListenUri(ns, path),
        token: function() { return ws.createRelayToken('http://' + ns, keyrule, key); }
    });
```

<span data-ttu-id="d5e85-150">Merhaba `RelayedServer` oluşturucu bağımsız değişkenleri hello daha farklı bir kümesini destekler `Server`bir tek başına dinleyicisi veya varolan bir HTTP dinleyicisi Framework'e katıştırılmış mümkün toobe olmadığından.</span><span class="sxs-lookup"><span data-stu-id="d5e85-150">hello `RelayedServer` constructor supports a different set of arguments than hello `Server`, because it is not a standalone listener, or able toobe embedded into an existing HTTP listener framework.</span></span> <span data-ttu-id="d5e85-151">Ayrıca daha az seçenek kullanılabilir olduğundan hello WebSocket yönetimini büyük ölçüde temsilci toohello geçiş hizmeti olduğundan.</span><span class="sxs-lookup"><span data-stu-id="d5e85-151">There are also fewer options available since hello WebSocket management is largely delegated toohello Relay service.</span></span>

<span data-ttu-id="d5e85-152">Oluşturucu bağımsız değişkenleri:</span><span class="sxs-lookup"><span data-stu-id="d5e85-152">Constructor arguments:</span></span>

- <span data-ttu-id="d5e85-153">`server`(gerekli) - hello URI genellikle hello WebSocket.createRelayListenUri() yardımcı yöntemi ile oluşturulan hangi toolisten üzerinde bir karma bağlantı adı için tam.</span><span class="sxs-lookup"><span data-stu-id="d5e85-153">`server` (required) - hello fully qualified URI for a Hybrid Connection name on which toolisten, usually constructed with hello WebSocket.createRelayListenUri() helper method.</span></span>
- <span data-ttu-id="d5e85-154">`token`(gerekli) - bu bağımsız değişken, daha önce verilen bir belirteç dizesi veya tooobtain belirteci bir dize çağrılan bir geri çağırma işlevini tutar.</span><span class="sxs-lookup"><span data-stu-id="d5e85-154">`token` (required) - this argument holds either a previously issued token string or a callback function that can be called tooobtain such a token string.</span></span> <span data-ttu-id="d5e85-155">Merhaba geri arama seçeneğini tercih edilen, aynıdır belirteci yenileme sağlar.</span><span class="sxs-lookup"><span data-stu-id="d5e85-155">hello callback option is preferred, as it enables token renewal.</span></span>

#### <a name="events"></a><span data-ttu-id="d5e85-156">Olaylar</span><span class="sxs-lookup"><span data-stu-id="d5e85-156">Events</span></span>

<span data-ttu-id="d5e85-157">`RelayedServer`örnekleri, toohandle gelen istekleri etkinleştirmek bağlantıları kurmak ve hata koşullarını algılamak üç olayları yayma.</span><span class="sxs-lookup"><span data-stu-id="d5e85-157">`RelayedServer` instances emit three events that enable you toohandle incoming requests, establish connections, and detect error conditions.</span></span> <span data-ttu-id="d5e85-158">Toohello abone olmalısınız `connect` olay toohandle iletileri.</span><span class="sxs-lookup"><span data-stu-id="d5e85-158">You must subscribe toohello `connect` event toohandle messages.</span></span> 

##### <a name="headers"></a><span data-ttu-id="d5e85-159">Üstbilgileri</span><span class="sxs-lookup"><span data-stu-id="d5e85-159">headers</span></span>

```JavaScript 
function(headers)
```

<span data-ttu-id="d5e85-160">Merhaba `headers` yalnızca gelen bağlantının, hello üstbilgileri toosend toohello istemci değiştirilmesini etkinleştirme kabul edilmeden önce olayı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="d5e85-160">hello `headers` event is raised just before an incoming connection is accepted, enabling modification of hello headers toosend toohello client.</span></span> 

##### <a name="connection"></a><span data-ttu-id="d5e85-161">bağlantı</span><span class="sxs-lookup"><span data-stu-id="d5e85-161">connection</span></span>

```JavaScript
function(socket)
```

<span data-ttu-id="d5e85-162">Yeni bir WebSocket bağlantı kabul edildiğinde yayılan.</span><span class="sxs-lookup"><span data-stu-id="d5e85-162">Emitted when a new WebSocket connection is accepted.</span></span> <span data-ttu-id="d5e85-163">Merhaba nesne türüdür `ws.WebSocket`, hello temel paketi ile aynı.</span><span class="sxs-lookup"><span data-stu-id="d5e85-163">hello object is of type `ws.WebSocket`, same as with hello base package.</span></span>


##### <a name="error"></a><span data-ttu-id="d5e85-164">error</span><span class="sxs-lookup"><span data-stu-id="d5e85-164">error</span></span>

```JavaScript
function(error)
```

<span data-ttu-id="d5e85-165">Bir hata Hello temel sunucu yayar, burada iletilir.</span><span class="sxs-lookup"><span data-stu-id="d5e85-165">If hello underlying server emits an error, it is forwarded here.</span></span>  

#### <a name="helpers"></a><span data-ttu-id="d5e85-166">Yardımcıları</span><span class="sxs-lookup"><span data-stu-id="d5e85-166">Helpers</span></span>

<span data-ttu-id="d5e85-167">geçirilen bir sunucu ve hemen tooincoming bağlantıları hello abone paketini toosimplify başlangıç de hello örneklerde, aşağıdaki gibi kullanılır basit yardımcı bir işlev gösterir:</span><span class="sxs-lookup"><span data-stu-id="d5e85-167">toosimplify starting a relayed server and immediately subscribing tooincoming connections, hello package exposes a simple helper function, which is also used in hello examples, as follows:</span></span>

##### <a name="createrelayedlistener"></a><span data-ttu-id="d5e85-168">createRelayedListener</span><span class="sxs-lookup"><span data-stu-id="d5e85-168">createRelayedListener</span></span>

```JavaScript
var WebSocket = require('hyco-ws');

var wss = WebSocket.createRelayedServer(
    {
        server: WebSocket.createRelayListenUri(ns, path),
        token: function() { return WebSocket.createRelayToken('http://' + ns, keyrule, key); }
    }, 
    function (ws) {
        console.log('connection accepted');
        ws.onmessage = function (event) {
            console.log(JSON.parse(event.data));
        };
        ws.on('close', function () {
            console.log('connection closed');
        });       
});
``` 

##### <a name="createrelayedserver"></a><span data-ttu-id="d5e85-169">createRelayedServer</span><span class="sxs-lookup"><span data-stu-id="d5e85-169">createRelayedServer</span></span>

```javascript
var server = createRelayedServer([options], [connectCallback] )
```

<span data-ttu-id="d5e85-170">Bu yöntem hello Oluşturucusu toocreate hello RelayedServer yeni bir örneğini çağırır ve sağlanan hello geri çağırma toohello 'bağlantı' olay abone olur.</span><span class="sxs-lookup"><span data-stu-id="d5e85-170">This method calls hello constructor toocreate a new instance of hello RelayedServer and then subscribes hello provided callback toohello 'connection' event.</span></span>
 
##### <a name="relayedconnect"></a><span data-ttu-id="d5e85-171">relayedConnect</span><span class="sxs-lookup"><span data-stu-id="d5e85-171">relayedConnect</span></span>

<span data-ttu-id="d5e85-172">Yalnızca hello yansıtma `createRelayedServer` işlevinde yardımcı `relayedConnect` istemci bağlantısını oluşturur ve toohello 'açık' hello elde edilen yuva olayına abone olur.</span><span class="sxs-lookup"><span data-stu-id="d5e85-172">Simply mirroring hello `createRelayedServer` helper in function, `relayedConnect` creates a client connection and subscribes toohello 'open' event on hello resulting socket.</span></span>

```JavaScript
var uri = WebSocket.createRelaySendUri(ns, path);
WebSocket.relayedConnect(
    uri,
    WebSocket.createRelayToken(uri, keyrule, key),
    function (socket) {
        ...
    }
);
```

## <a name="next-steps"></a><span data-ttu-id="d5e85-173">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d5e85-173">Next steps</span></span>
<span data-ttu-id="d5e85-174">toolearn Azure geçişi hakkında daha fazla bilgi için bu bağlantıları ziyaret edin:</span><span class="sxs-lookup"><span data-stu-id="d5e85-174">toolearn more about Azure Relay, visit these links:</span></span>
* [<span data-ttu-id="d5e85-175">Azure Geçiş nedir?</span><span class="sxs-lookup"><span data-stu-id="d5e85-175">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="d5e85-176">Kullanılabilir geçiş API'leri</span><span class="sxs-lookup"><span data-stu-id="d5e85-176">Available Relay APIs</span></span>](relay-api-overview.md)
