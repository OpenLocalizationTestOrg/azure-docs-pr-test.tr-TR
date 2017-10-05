---
title: "Azure Event Hubs kimlik doğrulaması ve güvenlik modeline genel bakış | Microsoft Docs"
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
ms.openlocfilehash: 5abdbf70d4fdb2c7feb0f3537ecc0f2abf0775a0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="event-hubs-authentication-and-security-model-overview"></a><span data-ttu-id="ad681-103">Olay hub'ları kimlik doğrulaması ve güvenlik modeline genel bakış</span><span class="sxs-lookup"><span data-stu-id="ad681-103">Event Hubs authentication and security model overview</span></span>
<span data-ttu-id="ad681-104">Azure Event Hubs güvenlik modeli, aşağıdaki gereksinimleri karşıladığından:</span><span class="sxs-lookup"><span data-stu-id="ad681-104">The Azure Event Hubs security model meets the following requirements:</span></span>

* <span data-ttu-id="ad681-105">Geçerli kimlik bilgileri sunmak yalnızca istemcileri verileri olay hub'ına gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ad681-105">Only clients that present valid credentials can send data to an event hub.</span></span>
* <span data-ttu-id="ad681-106">Bir istemci, başka bir istemci taklit edilemez.</span><span class="sxs-lookup"><span data-stu-id="ad681-106">A client cannot impersonate another client.</span></span>
* <span data-ttu-id="ad681-107">Standart dışı bir istemci, bir olay hub'ına veri gönderme engellenebilir.</span><span class="sxs-lookup"><span data-stu-id="ad681-107">A rogue client can be blocked from sending data to an event hub.</span></span>

## <a name="client-authentication"></a><span data-ttu-id="ad681-108">İstemci kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="ad681-108">Client authentication</span></span>
<span data-ttu-id="ad681-109">Olay hub'ları güvenlik modeli bir bileşimine dayalı [paylaşılan erişim imzası (SAS)](../service-bus-messaging/service-bus-sas.md) belirteçleri ve *olay yayımcıları*.</span><span class="sxs-lookup"><span data-stu-id="ad681-109">The Event Hubs security model is based on a combination of [Shared Access Signature (SAS)](../service-bus-messaging/service-bus-sas.md) tokens and *event publishers*.</span></span> <span data-ttu-id="ad681-110">Sanal bir uç noktası bir event hub için bir olay yayımcısı tanımlar.</span><span class="sxs-lookup"><span data-stu-id="ad681-110">An event publisher defines a virtual endpoint for an event hub.</span></span> <span data-ttu-id="ad681-111">Yayımcı, yalnızca bir olay hub'ına iletileri göndermek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ad681-111">The publisher can only be used to send messages to an event hub.</span></span> <span data-ttu-id="ad681-112">Bir yayımcıdan iletileri almak mümkün değildir.</span><span class="sxs-lookup"><span data-stu-id="ad681-112">It is not possible to receive messages from a publisher.</span></span>

<span data-ttu-id="ad681-113">Genellikle, istemci başına bir yayımcı bir olay hub'ı kullanır.</span><span class="sxs-lookup"><span data-stu-id="ad681-113">Typically, an event hub employs one publisher per client.</span></span> <span data-ttu-id="ad681-114">Herhangi bir olay hub'ı yayımcılar gönderilen tüm iletileri sıraya alınan bu olay hub'ın içinde edilir.</span><span class="sxs-lookup"><span data-stu-id="ad681-114">All messages that are sent to any of the publishers of an event hub are enqueued within that event hub.</span></span> <span data-ttu-id="ad681-115">Yayımcılar ayrıntılı erişim denetimi ve azaltma etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="ad681-115">Publishers enable fine-grained access control and throttling.</span></span>

<span data-ttu-id="ad681-116">Her olay hub'ları istemci istemciye karşıya bir benzersiz belirteci atanır.</span><span class="sxs-lookup"><span data-stu-id="ad681-116">Each Event Hubs client is assigned a unique token, which is uploaded to the client.</span></span> <span data-ttu-id="ad681-117">Her benzersiz belirteç erişimi için farklı bir benzersiz yayımcı verir şekilde belirteçleri oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="ad681-117">The tokens are produced such that each unique token grants access to a different unique publisher.</span></span> <span data-ttu-id="ad681-118">Bir belirteç sahip bir istemci, yalnızca bir yayımcı, ancak herhangi bir yayımcı gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ad681-118">A client that possesses a token can only send to one publisher, but no other publisher.</span></span> <span data-ttu-id="ad681-119">Birden çok istemci aynı belirteci paylaşıyorsanız, bunların her biri bir yayımcı paylaşır.</span><span class="sxs-lookup"><span data-stu-id="ad681-119">If multiple clients share the same token, then each of them shares a publisher.</span></span>

<span data-ttu-id="ad681-120">Önerilmemesine rağmen bir olay hub'ına doğrudan erişim belirteçleri ile cihazları Donatı mümkündür.</span><span class="sxs-lookup"><span data-stu-id="ad681-120">Although not recommended, it is possible to equip devices with tokens that grant direct access to an event hub.</span></span> <span data-ttu-id="ad681-121">Bu belirteç tutan herhangi bir aygıt, doğrudan bu olay hub'ına iletileri gönderebilir.</span><span class="sxs-lookup"><span data-stu-id="ad681-121">Any device that holds this token can send messages directly into that event hub.</span></span> <span data-ttu-id="ad681-122">Böyle bir cihazı azaltma tabi olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="ad681-122">Such a device will not be subject to throttling.</span></span> <span data-ttu-id="ad681-123">Ayrıca, cihaz, olay hub'ına göndermesinin kara listede olamaz.</span><span class="sxs-lookup"><span data-stu-id="ad681-123">Furthermore, the device cannot be blacklisted from sending to that event hub.</span></span>

<span data-ttu-id="ad681-124">Tüm belirteçlerin bir SAS anahtarla imzalanmıştır.</span><span class="sxs-lookup"><span data-stu-id="ad681-124">All tokens are signed with a SAS key.</span></span> <span data-ttu-id="ad681-125">Genellikle, tüm belirteçleri aynı anahtarla imzalanmıştır.</span><span class="sxs-lookup"><span data-stu-id="ad681-125">Typically, all tokens are signed with the same key.</span></span> <span data-ttu-id="ad681-126">İstemciler anahtarın farkında değildir; Bu, diğer istemcilerin belirteçleri üretim önler.</span><span class="sxs-lookup"><span data-stu-id="ad681-126">Clients are not aware of the key; this prevents other clients from manufacturing tokens.</span></span>

### <a name="create-the-sas-key"></a><span data-ttu-id="ad681-127">SAS anahtarı oluşturma</span><span class="sxs-lookup"><span data-stu-id="ad681-127">Create the SAS key</span></span>

<span data-ttu-id="ad681-128">Bir olay hub'ları ad alanı oluştururken, hizmet adında bir 256 bit SAS anahtarı oluşturur **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="ad681-128">When creating an Event Hubs namespace, the service generates a 256-bit SAS key named **RootManageSharedAccessKey**.</span></span> <span data-ttu-id="ad681-129">Bu anahtar verir göndermek, dinleme ve ad alanı hakkı yönetin.</span><span class="sxs-lookup"><span data-stu-id="ad681-129">This key grants send, listen, and manage rights to the namespace.</span></span> <span data-ttu-id="ad681-130">Ek anahtarlar da oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ad681-130">You can also create additional keys.</span></span> <span data-ttu-id="ad681-131">Belirli bir olay hub'ına verir izinleri göndermek bir anahtar oluşturmak önerilir.</span><span class="sxs-lookup"><span data-stu-id="ad681-131">It is recommended that you produce a key that grants send permissions to the specific event hub.</span></span> <span data-ttu-id="ad681-132">Bu konunun geri kalanı için bu anahtar adlı görünür duruma varsayılır **EventHubSendKey**.</span><span class="sxs-lookup"><span data-stu-id="ad681-132">For the remainder of this topic, it is assumed that you named this key **EventHubSendKey**.</span></span>

<span data-ttu-id="ad681-133">Aşağıdaki örnek, olay hub'ı oluştururken yalnızca gönderme bir anahtar oluşturur:</span><span class="sxs-lookup"><span data-stu-id="ad681-133">The following example creates a send-only key when creating the event hub:</span></span>

```csharp
// Create namespace manager.
string serviceNamespace = "YOUR_NAMESPACE";
string namespaceManageKeyName = "RootManageSharedAccessKey";
string namespaceManageKey = "YOUR_ROOT_MANAGE_SHARED_ACCESS_KEY";
Uri uri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, string.Empty);
TokenProvider td = TokenProvider.CreateSharedAccessSignatureTokenProvider(namespaceManageKeyName, namespaceManageKey);
NamespaceManager nm = new NamespaceManager(namespaceUri, namespaceManageTokenProvider);

// Create event hub with a SAS rule that enables sending to that event hub
EventHubDescription ed = new EventHubDescription("MY_EVENT_HUB") { PartitionCount = 32 };
string eventHubSendKeyName = "EventHubSendKey";
string eventHubSendKey = SharedAccessAuthorizationRule.GenerateRandomKey();
SharedAccessAuthorizationRule eventHubSendRule = new SharedAccessAuthorizationRule(eventHubSendKeyName, eventHubSendKey, new[] { AccessRights.Send });
ed.Authorization.Add(eventHubSendRule); 
nm.CreateEventHub(ed);
```

### <a name="generate-tokens"></a><span data-ttu-id="ad681-134">Belirteçleri oluşturmak</span><span class="sxs-lookup"><span data-stu-id="ad681-134">Generate tokens</span></span>

<span data-ttu-id="ad681-135">SAS anahtarını kullanarak belirteçleri üretebilir.</span><span class="sxs-lookup"><span data-stu-id="ad681-135">You can generate tokens using the SAS key.</span></span> <span data-ttu-id="ad681-136">İstemci başına yalnızca bir belirteç üretmek gerekir.</span><span class="sxs-lookup"><span data-stu-id="ad681-136">You must produce only one token per client.</span></span> <span data-ttu-id="ad681-137">Belirteçleri, ardından aşağıdaki yöntemi kullanarak üretilebilir.</span><span class="sxs-lookup"><span data-stu-id="ad681-137">Tokens can then be produced using the following method.</span></span> <span data-ttu-id="ad681-138">Tüm belirteçleri kullanarak oluşturulan **EventHubSendKey** anahtarı.</span><span class="sxs-lookup"><span data-stu-id="ad681-138">All tokens are generated using the **EventHubSendKey** key.</span></span> <span data-ttu-id="ad681-139">Her belirteç benzersiz bir URI atanır.</span><span class="sxs-lookup"><span data-stu-id="ad681-139">Each token is assigned a unique URI.</span></span>

```csharp
public static string SharedAccessSignatureTokenProvider.GetSharedAccessSignature(string keyName, string sharedAccessKey, string resource, TimeSpan tokenTimeToLive)
```

<span data-ttu-id="ad681-140">Bu yöntem çağrılırken URI olarak belirtilmelidir: `//<NAMESPACE>.servicebus.windows.net/<EVENT_HUB_NAME>/publishers/<PUBLISHER_NAME>`.</span><span class="sxs-lookup"><span data-stu-id="ad681-140">When calling this method, the URI should be specified as `//<NAMESPACE>.servicebus.windows.net/<EVENT_HUB_NAME>/publishers/<PUBLISHER_NAME>`.</span></span> <span data-ttu-id="ad681-141">Tüm belirteçleri için URI dışında aynı `PUBLISHER_NAME`, olacağı için her belirteci farklı.</span><span class="sxs-lookup"><span data-stu-id="ad681-141">For all tokens, the URI is identical, with the exception of `PUBLISHER_NAME`, which should be different for each token.</span></span> <span data-ttu-id="ad681-142">İdeal olarak, `PUBLISHER_NAME` belirtecini alır istemci Kimliğini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="ad681-142">Ideally, `PUBLISHER_NAME` represents the ID of the client that receives that token.</span></span>

<span data-ttu-id="ad681-143">Bu yöntem, şu yapıda bir belirteç oluşturur:</span><span class="sxs-lookup"><span data-stu-id="ad681-143">This method generates a token with the following structure:</span></span>

```csharp
SharedAccessSignature sr={URI}&sig={HMAC_SHA256_SIGNATURE}&se={EXPIRATION_TIME}&skn={KEY_NAME}
```

<span data-ttu-id="ad681-144">Belirteç süre sonu zamanı, 1 Ocak 1970'ten gelen saniye cinsinden belirtilir.</span><span class="sxs-lookup"><span data-stu-id="ad681-144">The token expiration time is specified in seconds from Jan 1, 1970.</span></span> <span data-ttu-id="ad681-145">Belirtecin bir örnek verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="ad681-145">The following is an example of a token:</span></span>

```csharp
SharedAccessSignature sr=contoso&sig=nPzdNN%2Gli0ifrfJwaK4mkK0RqAB%2byJUlt%2bGFmBHG77A%3d&se=1403130337&skn=RootManageSharedAccessKey
```

<span data-ttu-id="ad681-146">Genellikle, belirteçleri benzer veya istemci Sysprep'in aşıyor bir kullanım ömrü vardır.</span><span class="sxs-lookup"><span data-stu-id="ad681-146">Typically, the tokens have a lifespan that resembles or exceeds the lifespan of the client.</span></span> <span data-ttu-id="ad681-147">İstemci yeni bir belirteç elde yeteneği varsa, daha kısa bir ömre sahip belirteçler kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ad681-147">If the client has the capability to obtain a new token, tokens with a shorter lifespan can be used.</span></span>

### <a name="sending-data"></a><span data-ttu-id="ad681-148">Verileri gönderme</span><span class="sxs-lookup"><span data-stu-id="ad681-148">Sending data</span></span>
<span data-ttu-id="ad681-149">Belirteçleri oluşturduktan sonra her bir istemci kendi benzersiz belirteciyle sağlanır.</span><span class="sxs-lookup"><span data-stu-id="ad681-149">Once the tokens have been created, each client is provisioned with its own unique token.</span></span>

<span data-ttu-id="ad681-150">İstemci bir event hub'ına veri gönderdiğinde, kendi gönderme isteği belirteci ile etiketler.</span><span class="sxs-lookup"><span data-stu-id="ad681-150">When the client sends data into an event hub, it tags its send request with the token.</span></span> <span data-ttu-id="ad681-151">Bir saldırgan, gizli dinleme ve belirteç çalınmasını engellemek için olay hub'ı ile istemci arasındaki iletişimi şifrelenmiş bir kanal üzerinden gerçekleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="ad681-151">To prevent an attacker from eavesdropping and stealing the token, the communication between the client and the event hub must occur over an encrypted channel.</span></span>

### <a name="blacklisting-clients"></a><span data-ttu-id="ad681-152">İstemcileri kara liste</span><span class="sxs-lookup"><span data-stu-id="ad681-152">Blacklisting clients</span></span>
<span data-ttu-id="ad681-153">Bir saldırgan tarafından bir belirteç çalınırsa, saldırgan, belirteç çalınırsa istemcinin kimliğine bürünebilir.</span><span class="sxs-lookup"><span data-stu-id="ad681-153">If a token is stolen by an attacker, the attacker can impersonate the client whose token has been stolen.</span></span> <span data-ttu-id="ad681-154">Farklı bir yayımcı kullanan yeni bir belirteç alıncaya kadar bir istemci kara liste istemci kullanılamaz işler.</span><span class="sxs-lookup"><span data-stu-id="ad681-154">Blacklisting a client renders that client unusable until it receives a new token that uses a different publisher.</span></span>

## <a name="authentication-of-back-end-applications"></a><span data-ttu-id="ad681-155">Arka uç uygulamalarının kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="ad681-155">Authentication of back-end applications</span></span>

<span data-ttu-id="ad681-156">Olay hub'ları istemciler tarafından oluşturulan verileri kullanan arka uç uygulama kimliğini doğrulamak için Event Hubs için Service Bus konuları kullanılan model benzer bir güvenlik modeli kullanır.</span><span class="sxs-lookup"><span data-stu-id="ad681-156">To authenticate back-end applications that consume the data generated by Event Hubs clients, Event Hubs employs a security model that is similar to the model that is used for Service Bus topics.</span></span> <span data-ttu-id="ad681-157">Bir olay hub'ları tüketici grubu, Service Bus konu başlığına bir abonelik eşdeğerdir.</span><span class="sxs-lookup"><span data-stu-id="ad681-157">An Event Hubs consumer group is equivalent to a subscription to a Service Bus topic.</span></span> <span data-ttu-id="ad681-158">Tüketici grubu oluşturma isteği tarafından bir belirteç verir ayrıcalıkları olay hub'ı ya da olay hub'ı ait olduğu ad alanını yönetmek bulunuyorsa, istemci bir tüketici grubu oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ad681-158">A client can create a consumer group if the request to create the consumer group is accompanied by a token that grants manage privileges for the event hub, or for the namespace to which the event hub belongs.</span></span> <span data-ttu-id="ad681-159">Bir istemci bu tüketici grubu, olay hub'ı veya olay hub'ı ait olduğu ad alanını alma hakları veren bir belirteç tarafından alma isteği bulunuyorsa, verileri bir tüketici grubundan kullanmak izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="ad681-159">A client is allowed to consume data from a consumer group if the receive request is accompanied by a token that grants receive rights on that consumer group, the event hub, or the namespace to which the event hub belongs.</span></span>

<span data-ttu-id="ad681-160">Hizmet veri yolu geçerli sürümü tek tek abonelikler için SAS kuralları desteklemez.</span><span class="sxs-lookup"><span data-stu-id="ad681-160">The current version of Service Bus does not support SAS rules for individual subscriptions.</span></span> <span data-ttu-id="ad681-161">Aynı olay hub'ları tüketici grupları için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="ad681-161">The same holds true for Event Hubs consumer groups.</span></span> <span data-ttu-id="ad681-162">SAS desteği için her iki özellik gelecekte eklenir.</span><span class="sxs-lookup"><span data-stu-id="ad681-162">SAS support will be added for both features in the future.</span></span>

<span data-ttu-id="ad681-163">Tek tek tüketici grupları için SAS kimlik doğrulaması olmaması durumunda tüm tüketici grupları bir ortak anahtar ile güvenli hale getirmek için SAS tuşlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ad681-163">In the absence of SAS authentication for individual consumer groups, you can use SAS keys to secure all consumer groups with a common key.</span></span> <span data-ttu-id="ad681-164">Bu yaklaşım, herhangi bir event hub tüketici grupları verileri kullanmak üzere bir uygulama sağlar.</span><span class="sxs-lookup"><span data-stu-id="ad681-164">This approach enables an application to consume data from any of the consumer groups of an event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ad681-165">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ad681-165">Next steps</span></span>
<span data-ttu-id="ad681-166">Event Hubs hakkında daha fazla bilgi için aşağıdaki konuları ziyaret edin:</span><span class="sxs-lookup"><span data-stu-id="ad681-166">To learn more about Event Hubs, visit the following topics:</span></span>

* <span data-ttu-id="ad681-167">[Event Hubs’a genel bakış]</span><span class="sxs-lookup"><span data-stu-id="ad681-167">[Event Hubs overview]</span></span>
* <span data-ttu-id="ad681-168">[Paylaşılan erişim imzaları genel bakış]</span><span class="sxs-lookup"><span data-stu-id="ad681-168">[Overview of Shared Access Signatures]</span></span>
* <span data-ttu-id="ad681-169">[Event Hubs kullanan örnek uygulamalar]</span><span class="sxs-lookup"><span data-stu-id="ad681-169">[Sample applications that use Event Hubs]</span></span>

<span data-ttu-id="ad681-170">[Event Hubs’a genel bakış]: event-hubs-what-is-event-hubs.md</span><span class="sxs-lookup"><span data-stu-id="ad681-170">[Event Hubs overview]: event-hubs-what-is-event-hubs.md</span></span>
<span data-ttu-id="ad681-171">[Event Hubs kullanan örnek uygulamalar]: https://github.com/Azure/azure-event-hubs/tree/master/samples</span><span class="sxs-lookup"><span data-stu-id="ad681-171">[Sample applications that use Event Hubs]: https://github.com/Azure/azure-event-hubs/tree/master/samples</span></span>
<span data-ttu-id="ad681-172">[Paylaşılan erişim imzaları genel bakış]: ../service-bus-messaging/service-bus-sas.md</span><span class="sxs-lookup"><span data-stu-id="ad681-172">[Overview of Shared Access Signatures]: ../service-bus-messaging/service-bus-sas.md</span></span>

