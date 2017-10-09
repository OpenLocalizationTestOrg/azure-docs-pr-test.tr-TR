---
title: "Azure Event Hubs kimlik doğrulaması ve güvenlik modeli aaaOverview | Microsoft Docs"
description: "Olay hub'ları kimlik doğrulaması ve güvenlik modeline genel bakış."
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 93841e30-0c5c-4719-9dc1-57a4814342e7
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/30/2017
ms.author: sethm;clemensv
ms.openlocfilehash: e57ccda33e5ee20e635487cf91d9e8af594d3bd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-authentication-and-security-model-overview"></a><span data-ttu-id="fda1d-103">Olay hub'ları kimlik doğrulaması ve güvenlik modeline genel bakış</span><span class="sxs-lookup"><span data-stu-id="fda1d-103">Event Hubs authentication and security model overview</span></span>
<span data-ttu-id="fda1d-104">Hello Azure Event Hubs güvenlik modeli gereksinimlerine hello uyuyor:</span><span class="sxs-lookup"><span data-stu-id="fda1d-104">hello Azure Event Hubs security model meets hello following requirements:</span></span>

* <span data-ttu-id="fda1d-105">Geçerli kimlik bilgileri sunmak yalnızca istemciler tooan event hub'ı veri gönderebilir.</span><span class="sxs-lookup"><span data-stu-id="fda1d-105">Only clients that present valid credentials can send data tooan event hub.</span></span>
* <span data-ttu-id="fda1d-106">Bir istemci, başka bir istemci taklit edilemez.</span><span class="sxs-lookup"><span data-stu-id="fda1d-106">A client cannot impersonate another client.</span></span>
* <span data-ttu-id="fda1d-107">Standart dışı bir istemci tooan event hub'ı veri göndermesini engellenebilir.</span><span class="sxs-lookup"><span data-stu-id="fda1d-107">A rogue client can be blocked from sending data tooan event hub.</span></span>

## <a name="client-authentication"></a><span data-ttu-id="fda1d-108">İstemci kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="fda1d-108">Client authentication</span></span>
<span data-ttu-id="fda1d-109">Merhaba olay hub'ları güvenlik modelini bir birleşimini temel [paylaşılan erişim imzası (SAS)](../service-bus-messaging/service-bus-sas.md) belirteçleri ve *olay yayımcıları*.</span><span class="sxs-lookup"><span data-stu-id="fda1d-109">hello Event Hubs security model is based on a combination of [Shared Access Signature (SAS)](../service-bus-messaging/service-bus-sas.md) tokens and *event publishers*.</span></span> <span data-ttu-id="fda1d-110">Sanal bir uç noktası bir event hub için bir olay yayımcısı tanımlar.</span><span class="sxs-lookup"><span data-stu-id="fda1d-110">An event publisher defines a virtual endpoint for an event hub.</span></span> <span data-ttu-id="fda1d-111">Merhaba yayımcı yalnızca kullanılan toosend iletileri tooan olay hub'ı olabilir.</span><span class="sxs-lookup"><span data-stu-id="fda1d-111">hello publisher can only be used toosend messages tooan event hub.</span></span> <span data-ttu-id="fda1d-112">Bu olası tooreceive iletileri bir yayımcıdan değil.</span><span class="sxs-lookup"><span data-stu-id="fda1d-112">It is not possible tooreceive messages from a publisher.</span></span>

<span data-ttu-id="fda1d-113">Genellikle, istemci başına bir yayımcı bir olay hub'ı kullanır.</span><span class="sxs-lookup"><span data-stu-id="fda1d-113">Typically, an event hub employs one publisher per client.</span></span> <span data-ttu-id="fda1d-114">Bir olay hub'ının hello yayımcılar tooany gönderilen tüm iletiler sıraya alınan bu olay hub'ın içinde ' dir.</span><span class="sxs-lookup"><span data-stu-id="fda1d-114">All messages that are sent tooany of hello publishers of an event hub are enqueued within that event hub.</span></span> <span data-ttu-id="fda1d-115">Yayımcılar ayrıntılı erişim denetimi ve azaltma etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="fda1d-115">Publishers enable fine-grained access control and throttling.</span></span>

<span data-ttu-id="fda1d-116">Her olay hub'ları istemci karşıya yüklenen toohello istemci benzersiz bir belirteç atanır.</span><span class="sxs-lookup"><span data-stu-id="fda1d-116">Each Event Hubs client is assigned a unique token, which is uploaded toohello client.</span></span> <span data-ttu-id="fda1d-117">her benzersiz belirteç erişim tooa farklı benzersiz yayımcı verir şekilde hello belirteçleri oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="fda1d-117">hello tokens are produced such that each unique token grants access tooa different unique publisher.</span></span> <span data-ttu-id="fda1d-118">Bir belirteç sahip bir istemci, yalnızca tooone publisher, ancak herhangi bir yayımcı gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fda1d-118">A client that possesses a token can only send tooone publisher, but no other publisher.</span></span> <span data-ttu-id="fda1d-119">Aynı belirteci ve sonra bunların her biri birden çok istemcileri paylaşımı Merhaba, bir yayımcı paylaşır.</span><span class="sxs-lookup"><span data-stu-id="fda1d-119">If multiple clients share hello same token, then each of them shares a publisher.</span></span>

<span data-ttu-id="fda1d-120">Önerilmemesine rağmen tooan event hub'ı doğrudan erişim vermek belirteçleri ile olası tooequip cihazları var.</span><span class="sxs-lookup"><span data-stu-id="fda1d-120">Although not recommended, it is possible tooequip devices with tokens that grant direct access tooan event hub.</span></span> <span data-ttu-id="fda1d-121">Bu belirteç tutan herhangi bir aygıt, doğrudan bu olay hub'ına iletileri gönderebilir.</span><span class="sxs-lookup"><span data-stu-id="fda1d-121">Any device that holds this token can send messages directly into that event hub.</span></span> <span data-ttu-id="fda1d-122">Böyle bir cihazı konu toothrottling olmaz.</span><span class="sxs-lookup"><span data-stu-id="fda1d-122">Such a device will not be subject toothrottling.</span></span> <span data-ttu-id="fda1d-123">Ayrıca, hello aygıt toothat olay hub'ı göndermesinin kara listede olamaz.</span><span class="sxs-lookup"><span data-stu-id="fda1d-123">Furthermore, hello device cannot be blacklisted from sending toothat event hub.</span></span>

<span data-ttu-id="fda1d-124">Tüm belirteçlerin bir SAS anahtarla imzalanmıştır.</span><span class="sxs-lookup"><span data-stu-id="fda1d-124">All tokens are signed with a SAS key.</span></span> <span data-ttu-id="fda1d-125">Genellikle, tüm belirteçleri hello ile imzalanmış aynı anahtarı.</span><span class="sxs-lookup"><span data-stu-id="fda1d-125">Typically, all tokens are signed with hello same key.</span></span> <span data-ttu-id="fda1d-126">İstemcileri hello anahtarı farkında değildir; Bu, diğer istemcilerin belirteçleri üretim önler.</span><span class="sxs-lookup"><span data-stu-id="fda1d-126">Clients are not aware of hello key; this prevents other clients from manufacturing tokens.</span></span>

### <a name="create-hello-sas-key"></a><span data-ttu-id="fda1d-127">Merhaba SAS anahtarı oluşturma</span><span class="sxs-lookup"><span data-stu-id="fda1d-127">Create hello SAS key</span></span>

<span data-ttu-id="fda1d-128">Bir olay hub'ları ad alanı oluştururken, hello hizmeti adlı 256 bit SAS anahtarı üretir **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="fda1d-128">When creating an Event Hubs namespace, hello service generates a 256-bit SAS key named **RootManageSharedAccessKey**.</span></span> <span data-ttu-id="fda1d-129">Bu anahtar verir göndermek, dinleme ve hakları toohello ad alanı yönetin.</span><span class="sxs-lookup"><span data-stu-id="fda1d-129">This key grants send, listen, and manage rights toohello namespace.</span></span> <span data-ttu-id="fda1d-130">Ek anahtarlar da oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fda1d-130">You can also create additional keys.</span></span> <span data-ttu-id="fda1d-131">Verir izinleri toohello belirli olay hub'ı Gönder bir anahtar oluşturmak önerilir.</span><span class="sxs-lookup"><span data-stu-id="fda1d-131">It is recommended that you produce a key that grants send permissions toohello specific event hub.</span></span> <span data-ttu-id="fda1d-132">Bu konuda Hello kalanı için bu anahtar adlı görünür duruma varsayılır **EventHubSendKey**.</span><span class="sxs-lookup"><span data-stu-id="fda1d-132">For hello remainder of this topic, it is assumed that you named this key **EventHubSendKey**.</span></span>

<span data-ttu-id="fda1d-133">Aşağıdaki örnek hello hello olay hub'ı oluştururken yalnızca gönderme bir anahtar oluşturur:</span><span class="sxs-lookup"><span data-stu-id="fda1d-133">hello following example creates a send-only key when creating hello event hub:</span></span>

```csharp
// Create namespace manager.
string serviceNamespace = "YOUR_NAMESPACE";
string namespaceManageKeyName = "RootManageSharedAccessKey";
string namespaceManageKey = "YOUR_ROOT_MANAGE_SHARED_ACCESS_KEY";
Uri uri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, string.Empty);
TokenProvider td = TokenProvider.CreateSharedAccessSignatureTokenProvider(namespaceManageKeyName, namespaceManageKey);
NamespaceManager nm = new NamespaceManager(namespaceUri, namespaceManageTokenProvider);

// Create event hub with a SAS rule that enables sending toothat event hub
EventHubDescription ed = new EventHubDescription("MY_EVENT_HUB") { PartitionCount = 32 };
string eventHubSendKeyName = "EventHubSendKey";
string eventHubSendKey = SharedAccessAuthorizationRule.GenerateRandomKey();
SharedAccessAuthorizationRule eventHubSendRule = new SharedAccessAuthorizationRule(eventHubSendKeyName, eventHubSendKey, new[] { AccessRights.Send });
ed.Authorization.Add(eventHubSendRule); 
nm.CreateEventHub(ed);
```

### <a name="generate-tokens"></a><span data-ttu-id="fda1d-134">Belirteçleri oluşturmak</span><span class="sxs-lookup"><span data-stu-id="fda1d-134">Generate tokens</span></span>

<span data-ttu-id="fda1d-135">Merhaba SAS anahtarı kullanarak belirteçleri üretebilir.</span><span class="sxs-lookup"><span data-stu-id="fda1d-135">You can generate tokens using hello SAS key.</span></span> <span data-ttu-id="fda1d-136">İstemci başına yalnızca bir belirteç üretmek gerekir.</span><span class="sxs-lookup"><span data-stu-id="fda1d-136">You must produce only one token per client.</span></span> <span data-ttu-id="fda1d-137">Ardından belirteçleri yöntemi aşağıdaki hello kullanarak da üretilmesi.</span><span class="sxs-lookup"><span data-stu-id="fda1d-137">Tokens can then be produced using hello following method.</span></span> <span data-ttu-id="fda1d-138">Tüm belirteçleri hello kullanarak oluşturulan **EventHubSendKey** anahtarı.</span><span class="sxs-lookup"><span data-stu-id="fda1d-138">All tokens are generated using hello **EventHubSendKey** key.</span></span> <span data-ttu-id="fda1d-139">Her belirteç benzersiz bir URI atanır.</span><span class="sxs-lookup"><span data-stu-id="fda1d-139">Each token is assigned a unique URI.</span></span>

```csharp
public static string SharedAccessSignatureTokenProvider.GetSharedAccessSignature(string keyName, string sharedAccessKey, string resource, TimeSpan tokenTimeToLive)
```

<span data-ttu-id="fda1d-140">Bu yöntem çağrılırken hello URI olarak belirtilmelidir: `//<NAMESPACE>.servicebus.windows.net/<EVENT_HUB_NAME>/publishers/<PUBLISHER_NAME>`.</span><span class="sxs-lookup"><span data-stu-id="fda1d-140">When calling this method, hello URI should be specified as `//<NAMESPACE>.servicebus.windows.net/<EVENT_HUB_NAME>/publishers/<PUBLISHER_NAME>`.</span></span> <span data-ttu-id="fda1d-141">Tüm belirteçleri için hello URI hello özel durumla aynıdır `PUBLISHER_NAME`, olacağı için her belirteci farklı.</span><span class="sxs-lookup"><span data-stu-id="fda1d-141">For all tokens, hello URI is identical, with hello exception of `PUBLISHER_NAME`, which should be different for each token.</span></span> <span data-ttu-id="fda1d-142">İdeal olarak, `PUBLISHER_NAME` temsil hello belirtecini alır hello istemcinin kimliği.</span><span class="sxs-lookup"><span data-stu-id="fda1d-142">Ideally, `PUBLISHER_NAME` represents hello ID of hello client that receives that token.</span></span>

<span data-ttu-id="fda1d-143">Bu yöntem, yapı izlenerek hello ile bir belirteç oluşturur:</span><span class="sxs-lookup"><span data-stu-id="fda1d-143">This method generates a token with hello following structure:</span></span>

```csharp
SharedAccessSignature sr={URI}&sig={HMAC_SHA256_SIGNATURE}&se={EXPIRATION_TIME}&skn={KEY_NAME}
```

<span data-ttu-id="fda1d-144">Merhaba belirteci süre sonu 1 Ocak 1970'ten gelen saniye cinsinden belirtilir.</span><span class="sxs-lookup"><span data-stu-id="fda1d-144">hello token expiration time is specified in seconds from Jan 1, 1970.</span></span> <span data-ttu-id="fda1d-145">Merhaba, bir belirteç örneği aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="fda1d-145">hello following is an example of a token:</span></span>

```csharp
SharedAccessSignature sr=contoso&sig=nPzdNN%2Gli0ifrfJwaK4mkK0RqAB%2byJUlt%2bGFmBHG77A%3d&se=1403130337&skn=RootManageSharedAccessKey
```

<span data-ttu-id="fda1d-146">Genellikle, hello belirteçleri hello istemci hello Sysprep'in aşıyor ya da benzer bir kullanım ömrü vardır.</span><span class="sxs-lookup"><span data-stu-id="fda1d-146">Typically, hello tokens have a lifespan that resembles or exceeds hello lifespan of hello client.</span></span> <span data-ttu-id="fda1d-147">Merhaba istemci yeni bir belirteç hello yetenek tooobtain varsa, daha kısa bir ömre sahip belirteçler kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="fda1d-147">If hello client has hello capability tooobtain a new token, tokens with a shorter lifespan can be used.</span></span>

### <a name="sending-data"></a><span data-ttu-id="fda1d-148">Verileri gönderme</span><span class="sxs-lookup"><span data-stu-id="fda1d-148">Sending data</span></span>
<span data-ttu-id="fda1d-149">Merhaba belirteçleri oluşturduktan sonra her bir istemci kendi benzersiz belirteciyle sağlanır.</span><span class="sxs-lookup"><span data-stu-id="fda1d-149">Once hello tokens have been created, each client is provisioned with its own unique token.</span></span>

<span data-ttu-id="fda1d-150">Merhaba istemcisi bir event hub'ına veri gönderdiğinde, kendi gönderme isteği hello belirteci ile etiketler.</span><span class="sxs-lookup"><span data-stu-id="fda1d-150">When hello client sends data into an event hub, it tags its send request with hello token.</span></span> <span data-ttu-id="fda1d-151">bir saldırganın çalmak hello belirteci, hello istemci hello olay hub'ı arasında hello iletişimi ve gizli dinleme tooprevent şifrelenmiş bir kanal üzerinden bulunması gerekir.</span><span class="sxs-lookup"><span data-stu-id="fda1d-151">tooprevent an attacker from eavesdropping and stealing hello token, hello communication between hello client and hello event hub must occur over an encrypted channel.</span></span>

### <a name="blacklisting-clients"></a><span data-ttu-id="fda1d-152">İstemcileri kara liste</span><span class="sxs-lookup"><span data-stu-id="fda1d-152">Blacklisting clients</span></span>
<span data-ttu-id="fda1d-153">Bir saldırgan tarafından bir belirteç çalınırsa, hello saldırgan, belirteç çalınırsa hello istemcinin kimliğine bürünebilir.</span><span class="sxs-lookup"><span data-stu-id="fda1d-153">If a token is stolen by an attacker, hello attacker can impersonate hello client whose token has been stolen.</span></span> <span data-ttu-id="fda1d-154">Farklı bir yayımcı kullanan yeni bir belirteç alıncaya kadar bir istemci kara liste istemci kullanılamaz işler.</span><span class="sxs-lookup"><span data-stu-id="fda1d-154">Blacklisting a client renders that client unusable until it receives a new token that uses a different publisher.</span></span>

## <a name="authentication-of-back-end-applications"></a><span data-ttu-id="fda1d-155">Arka uç uygulamalarının kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="fda1d-155">Authentication of back-end applications</span></span>

<span data-ttu-id="fda1d-156">Event Hubs olay hub'ları istemciler tarafından oluşturulan hello verileri kullanmak tooauthenticate arka uç uygulama Service Bus konuları kullanılan benzer toohello modeli bir güvenlik modeli kullanır.</span><span class="sxs-lookup"><span data-stu-id="fda1d-156">tooauthenticate back-end applications that consume hello data generated by Event Hubs clients, Event Hubs employs a security model that is similar toohello model that is used for Service Bus topics.</span></span> <span data-ttu-id="fda1d-157">Bir olay hub'ları tüketici eşdeğer tooa abonelik tooa Service Bus konu grubudur.</span><span class="sxs-lookup"><span data-stu-id="fda1d-157">An Event Hubs consumer group is equivalent tooa subscription tooa Service Bus topic.</span></span> <span data-ttu-id="fda1d-158">Merhaba istek toocreate hello tüketici grubu hello olay hub'ına yönelik ayrıcalıklar verir yönetmek veya hello olay hub'ı hello ad alanı toowhich ait bir belirteç tarafından bulunuyorsa, istemci bir tüketici grubu oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fda1d-158">A client can create a consumer group if hello request toocreate hello consumer group is accompanied by a token that grants manage privileges for hello event hub, or for hello namespace toowhich hello event hub belongs.</span></span> <span data-ttu-id="fda1d-159">Bir istemci hello istek alırsanız bir belirteç tarafından bir tüketici grubundan tooconsume veri eşlik bu tüketici grubunda hakları verir Al, hello olay hub'ı veya hello ad alanı toowhich hello olay hub'ı ait izin verilir.</span><span class="sxs-lookup"><span data-stu-id="fda1d-159">A client is allowed tooconsume data from a consumer group if hello receive request is accompanied by a token that grants receive rights on that consumer group, hello event hub, or hello namespace toowhich hello event hub belongs.</span></span>

<span data-ttu-id="fda1d-160">Merhaba geçerli sürümü, hizmet veri yolu SAS kuralları için bireysel abonelikleri desteklemez.</span><span class="sxs-lookup"><span data-stu-id="fda1d-160">hello current version of Service Bus does not support SAS rules for individual subscriptions.</span></span> <span data-ttu-id="fda1d-161">Merhaba aynı olay hub'ları tüketici grupları için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="fda1d-161">hello same holds true for Event Hubs consumer groups.</span></span> <span data-ttu-id="fda1d-162">Merhaba gelecekteki içinde her iki özellik için SAS destek eklenecektir.</span><span class="sxs-lookup"><span data-stu-id="fda1d-162">SAS support will be added for both features in hello future.</span></span>

<span data-ttu-id="fda1d-163">Tek tek tüketici grupları için SAS kimlik doğrulamasının Hello olmaması durumunda, bir ortak anahtar ile tüm tüketici grupları SAS anahtarları toosecure kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fda1d-163">In hello absence of SAS authentication for individual consumer groups, you can use SAS keys toosecure all consumer groups with a common key.</span></span> <span data-ttu-id="fda1d-164">Bu yaklaşım, bir uygulama tooconsume verilerden herhangi bir event hub'hello tüketici grupları sağlar.</span><span class="sxs-lookup"><span data-stu-id="fda1d-164">This approach enables an application tooconsume data from any of hello consumer groups of an event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fda1d-165">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fda1d-165">Next steps</span></span>
<span data-ttu-id="fda1d-166">Event Hubs hakkında daha fazla toolearn aşağıdaki konularda hello ziyaret edin:</span><span class="sxs-lookup"><span data-stu-id="fda1d-166">toolearn more about Event Hubs, visit hello following topics:</span></span>

* <span data-ttu-id="fda1d-167">[Event Hubs’a genel bakış]</span><span class="sxs-lookup"><span data-stu-id="fda1d-167">[Event Hubs overview]</span></span>
* <span data-ttu-id="fda1d-168">[Paylaşılan erişim imzaları genel bakış]</span><span class="sxs-lookup"><span data-stu-id="fda1d-168">[Overview of Shared Access Signatures]</span></span>
* <span data-ttu-id="fda1d-169">[Event Hubs kullanan örnek uygulamalar]</span><span class="sxs-lookup"><span data-stu-id="fda1d-169">[Sample applications that use Event Hubs]</span></span>

[Event Hubs’a genel bakış]: event-hubs-what-is-event-hubs.md
[Event Hubs kullanan örnek uygulamalar]: https://github.com/Azure/azure-event-hubs/tree/master/samples
[Paylaşılan erişim imzaları genel bakış]: ../service-bus-messaging/service-bus-sas.md

