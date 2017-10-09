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
# <a name="event-hubs-authentication-and-security-model-overview"></a>Olay hub'ları kimlik doğrulaması ve güvenlik modeline genel bakış
Hello Azure Event Hubs güvenlik modeli gereksinimlerine hello uyuyor:

* Geçerli kimlik bilgileri sunmak yalnızca istemciler tooan event hub'ı veri gönderebilir.
* Bir istemci, başka bir istemci taklit edilemez.
* Standart dışı bir istemci tooan event hub'ı veri göndermesini engellenebilir.

## <a name="client-authentication"></a>İstemci kimlik doğrulaması
Merhaba olay hub'ları güvenlik modelini bir birleşimini temel [paylaşılan erişim imzası (SAS)](../service-bus-messaging/service-bus-sas.md) belirteçleri ve *olay yayımcıları*. Sanal bir uç noktası bir event hub için bir olay yayımcısı tanımlar. Merhaba yayımcı yalnızca kullanılan toosend iletileri tooan olay hub'ı olabilir. Bu olası tooreceive iletileri bir yayımcıdan değil.

Genellikle, istemci başına bir yayımcı bir olay hub'ı kullanır. Bir olay hub'ının hello yayımcılar tooany gönderilen tüm iletiler sıraya alınan bu olay hub'ın içinde ' dir. Yayımcılar ayrıntılı erişim denetimi ve azaltma etkinleştirin.

Her olay hub'ları istemci karşıya yüklenen toohello istemci benzersiz bir belirteç atanır. her benzersiz belirteç erişim tooa farklı benzersiz yayımcı verir şekilde hello belirteçleri oluşturulur. Bir belirteç sahip bir istemci, yalnızca tooone publisher, ancak herhangi bir yayımcı gönderebilirsiniz. Aynı belirteci ve sonra bunların her biri birden çok istemcileri paylaşımı Merhaba, bir yayımcı paylaşır.

Önerilmemesine rağmen tooan event hub'ı doğrudan erişim vermek belirteçleri ile olası tooequip cihazları var. Bu belirteç tutan herhangi bir aygıt, doğrudan bu olay hub'ına iletileri gönderebilir. Böyle bir cihazı konu toothrottling olmaz. Ayrıca, hello aygıt toothat olay hub'ı göndermesinin kara listede olamaz.

Tüm belirteçlerin bir SAS anahtarla imzalanmıştır. Genellikle, tüm belirteçleri hello ile imzalanmış aynı anahtarı. İstemcileri hello anahtarı farkında değildir; Bu, diğer istemcilerin belirteçleri üretim önler.

### <a name="create-hello-sas-key"></a>Merhaba SAS anahtarı oluşturma

Bir olay hub'ları ad alanı oluştururken, hello hizmeti adlı 256 bit SAS anahtarı üretir **RootManageSharedAccessKey**. Bu anahtar verir göndermek, dinleme ve hakları toohello ad alanı yönetin. Ek anahtarlar da oluşturabilirsiniz. Verir izinleri toohello belirli olay hub'ı Gönder bir anahtar oluşturmak önerilir. Bu konuda Hello kalanı için bu anahtar adlı görünür duruma varsayılır **EventHubSendKey**.

Aşağıdaki örnek hello hello olay hub'ı oluştururken yalnızca gönderme bir anahtar oluşturur:

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

### <a name="generate-tokens"></a>Belirteçleri oluşturmak

Merhaba SAS anahtarı kullanarak belirteçleri üretebilir. İstemci başına yalnızca bir belirteç üretmek gerekir. Ardından belirteçleri yöntemi aşağıdaki hello kullanarak da üretilmesi. Tüm belirteçleri hello kullanarak oluşturulan **EventHubSendKey** anahtarı. Her belirteç benzersiz bir URI atanır.

```csharp
public static string SharedAccessSignatureTokenProvider.GetSharedAccessSignature(string keyName, string sharedAccessKey, string resource, TimeSpan tokenTimeToLive)
```

Bu yöntem çağrılırken hello URI olarak belirtilmelidir: `//<NAMESPACE>.servicebus.windows.net/<EVENT_HUB_NAME>/publishers/<PUBLISHER_NAME>`. Tüm belirteçleri için hello URI hello özel durumla aynıdır `PUBLISHER_NAME`, olacağı için her belirteci farklı. İdeal olarak, `PUBLISHER_NAME` temsil hello belirtecini alır hello istemcinin kimliği.

Bu yöntem, yapı izlenerek hello ile bir belirteç oluşturur:

```csharp
SharedAccessSignature sr={URI}&sig={HMAC_SHA256_SIGNATURE}&se={EXPIRATION_TIME}&skn={KEY_NAME}
```

Merhaba belirteci süre sonu 1 Ocak 1970'ten gelen saniye cinsinden belirtilir. Merhaba, bir belirteç örneği aşağıdadır:

```csharp
SharedAccessSignature sr=contoso&sig=nPzdNN%2Gli0ifrfJwaK4mkK0RqAB%2byJUlt%2bGFmBHG77A%3d&se=1403130337&skn=RootManageSharedAccessKey
```

Genellikle, hello belirteçleri hello istemci hello Sysprep'in aşıyor ya da benzer bir kullanım ömrü vardır. Merhaba istemci yeni bir belirteç hello yetenek tooobtain varsa, daha kısa bir ömre sahip belirteçler kullanılabilir.

### <a name="sending-data"></a>Verileri gönderme
Merhaba belirteçleri oluşturduktan sonra her bir istemci kendi benzersiz belirteciyle sağlanır.

Merhaba istemcisi bir event hub'ına veri gönderdiğinde, kendi gönderme isteği hello belirteci ile etiketler. bir saldırganın çalmak hello belirteci, hello istemci hello olay hub'ı arasında hello iletişimi ve gizli dinleme tooprevent şifrelenmiş bir kanal üzerinden bulunması gerekir.

### <a name="blacklisting-clients"></a>İstemcileri kara liste
Bir saldırgan tarafından bir belirteç çalınırsa, hello saldırgan, belirteç çalınırsa hello istemcinin kimliğine bürünebilir. Farklı bir yayımcı kullanan yeni bir belirteç alıncaya kadar bir istemci kara liste istemci kullanılamaz işler.

## <a name="authentication-of-back-end-applications"></a>Arka uç uygulamalarının kimlik doğrulaması

Event Hubs olay hub'ları istemciler tarafından oluşturulan hello verileri kullanmak tooauthenticate arka uç uygulama Service Bus konuları kullanılan benzer toohello modeli bir güvenlik modeli kullanır. Bir olay hub'ları tüketici eşdeğer tooa abonelik tooa Service Bus konu grubudur. Merhaba istek toocreate hello tüketici grubu hello olay hub'ına yönelik ayrıcalıklar verir yönetmek veya hello olay hub'ı hello ad alanı toowhich ait bir belirteç tarafından bulunuyorsa, istemci bir tüketici grubu oluşturabilirsiniz. Bir istemci hello istek alırsanız bir belirteç tarafından bir tüketici grubundan tooconsume veri eşlik bu tüketici grubunda hakları verir Al, hello olay hub'ı veya hello ad alanı toowhich hello olay hub'ı ait izin verilir.

Merhaba geçerli sürümü, hizmet veri yolu SAS kuralları için bireysel abonelikleri desteklemez. Merhaba aynı olay hub'ları tüketici grupları için geçerlidir. Merhaba gelecekteki içinde her iki özellik için SAS destek eklenecektir.

Tek tek tüketici grupları için SAS kimlik doğrulamasının Hello olmaması durumunda, bir ortak anahtar ile tüm tüketici grupları SAS anahtarları toosecure kullanabilirsiniz. Bu yaklaşım, bir uygulama tooconsume verilerden herhangi bir event hub'hello tüketici grupları sağlar.

## <a name="next-steps"></a>Sonraki adımlar
Event Hubs hakkında daha fazla toolearn aşağıdaki konularda hello ziyaret edin:

* [Event Hubs’a genel bakış]
* [Paylaşılan erişim imzaları genel bakış]
* [Event Hubs kullanan örnek uygulamalar]

[Event Hubs’a genel bakış]: event-hubs-what-is-event-hubs.md
[Event Hubs kullanan örnek uygulamalar]: https://github.com/Azure/azure-event-hubs/tree/master/samples
[Paylaşılan erişim imzaları genel bakış]: ../service-bus-messaging/service-bus-sas.md

