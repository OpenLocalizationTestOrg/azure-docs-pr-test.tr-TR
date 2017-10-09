---
title: "Paylaşılan erişim imzaları ile aaaAzure Service Bus kimlik doğrulaması | Microsoft Docs"
description: "Hizmet veri yolu paylaşılan erişim imzaları genel bakış, SAS kimlik doğrulaması Azure Service Bus ile ilgili ayrıntıları kullanarak kimlik doğrulamasına genel bakış."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/23/2017
ms.author: sethm
ms.openlocfilehash: 773bb11720384d7245820b56dc25b8e064ffa746
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-authentication-with-shared-access-signatures"></a>Paylaşılan erişim imzaları ile Service Bus kimlik doğrulaması

*Paylaşılan erişim imzası* (SAS) olan Service Bus Mesajlaşma hizmeti için hello birincil güvenlik mekanizması. Nasıl çalıştıklarını ve nasıl SAS, bu makalede ele toouse platform belirsiz şekilde bunları.

SAS kimlik doğrulama uygulamaları tooauthenticate tooService hello ad alanı veya belirli hakları ilişkili olan varlık (kuyruk veya konu) Mesajlaşma hello yapılandırılmış bir erişim anahtarı kullanarak veri yolu sağlar. Daha sonra bu anahtar toogenerate istemcileri tooauthenticate tooService Bus sırayla kullanabileceğiniz bir SAS belirteci kullanabilirsiniz.

SAS kimlik doğrulama desteği hello Azure SDK'sı sürüm 2.0 ve üzeri dahil edilmiştir.

## <a name="overview-of-sas"></a>SAS genel bakış

Paylaşılan erişim imzaları, SHA-256 güvenli karmaları veya URI dayalı bir kimlik doğrulama mekanizmasıdır. SAS tüm Service Bus hizmetler tarafından kullanılan son derece güçlü bir mekanizmadır. Gerçek kullanımda SAS iki bileşenden oluşur: bir *paylaşılan erişim ilkesi* ve *paylaşılan erişim imzası* (genellikle olarak adlandırılan bir *belirteci*).

Hizmet veri yolu SAS kimlik doğrulaması, bir şifreleme anahtarıyla ilişkili haklar bir Service Bus kaynakta hello yapılandırmasını içerir. Bir SAS belirteci sunarak istemcileri talep erişim tooService Bus kaynaklar. Bu belirteç hello Kaynak URI erişilen oluşur ve anahtar hello ile imzalanmış bir sona erme yapılandırılır.

Service Bus paylaşılan erişim imzası yetkilendirme kuralları yapılandırabilirsiniz [geçişleri](service-bus-fundamentals-hybrid-solutions.md#relays), [sıraları](service-bus-fundamentals-hybrid-solutions.md#queues), ve [konuları](service-bus-fundamentals-hybrid-solutions.md#topics).

SAS kimlik doğrulaması öğeleri aşağıdaki hello kullanır:

* [Paylaşılan erişim yetkilendirme kuralı](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule): A 256 bit Base64 gösteriminde birincil şifreleme anahtarı, isteğe bağlı bir ikincil anahtarı ve bir anahtar adı ve ilişkili haklar (koleksiyonu *dinleme*, *Gönder*, veya *Yönet* hakları).
* [Paylaşılan erişim imzası](/dotnet/api/microsoft.servicebus.sharedaccesssignaturetokenprovider) belirteci: hello HMAC SHA256 erişilir hello kaynak URI'si Merhaba oluşan bir kaynak dizesi ve bir süre sonu hello şifreleme anahtarıyla kullanılarak oluşturulan. Merhaba imza ve diğer öğeleri hello aşağıdaki bölümlerde açıklanan dize tooform hello SAS belirteci biçimlendirilir.

## <a name="shared-access-policy"></a>Paylaşılan Erişim İlkesi

SAS hakkında önemli şey toounderstand İlkesi ile başlayıp ' dir. Her ilke için üç parça bilgi karar verin: **adı**, **kapsam**, ve **izinleri**. Merhaba **adı** yalnızca bu; bu kapsam içinde benzersiz bir ad. Merhaba kapsamı kadar kolaydır: kendi hello söz konusu hello kaynak URI'si. Bir hizmet veri yolu ad alanı için hello kapsam hello tam etki alanı adı (FQDN) olduğu gibi `https://<yournamespace>.servicebus.windows.net/`.

bir ilke kullanılabilir izinlerini Hello büyük ölçüde kendinden açıklamalıdır şunlardır:

* Gönder
* Dinleme
* Yönet

Hello ilkesi oluşturduktan sonra atanan bir *birincil anahtar* ve *ikincil anahtar*. Şifreleme açısından güçlü anahtarları şunlardır. Bunları kaybeder veya bunları sızıntısı yok - bunlar her zaman hello kullanılabilir olacak [Azure portal][Azure portal]. Oluşturulan hello anahtarları birini kullanabilirsiniz ve her zaman yeniden oluşturabilirsiniz. Ancak, yeniden oluşturmak veya hello İlkesi'nde hello birincil anahtar değiştirirseniz tüm paylaşılan erişim imzaları oluşturulan geçersiz kılınır.

Bir hizmet veri yolu ad alanı oluşturduğunuzda, bir ilke olarak adlandırılan hello tüm ad alanı için otomatik olarak oluşturulur **RootManageSharedAccessKey**, ve bu ilkeyi tüm izinlere sahiptir. Olarak oturum yok **kök**, gerçekten iyi bir neden olmadıkça bu ilkeyi kullanmayın. Ek ilkeler hello oluşturabilirsiniz **yapılandırma** hello portalında hello ad alanı için sekmesi. Bir tek ağacı düzey Service Bus (ad alanı, kuyruk, vb.) yalnızca too12 bağlı ilkeleri tooit olabilir önemli toonote olur.

## <a name="configuration-for-shared-access-signature-authentication"></a>Paylaşılan erişim imzası kimlik doğrulaması için yapılandırma
Merhaba yapılandırabilirsiniz [Rootmanagesharedaccesskey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) hizmet veri yolu ad alanları, kuyruk veya konuları kuralı. Yapılandırma bir [Rootmanagesharedaccesskey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) bir Service Bus abonelik şu anda desteklenmiyor ancak üzerinde bir ad alanı veya konu toosecure erişim toosubscriptions yapılandırılmış kurallarını kullanabilirsiniz. Bu yordamı gösterilmektedir çalışan bir örnek için hello bkz [kullanarak paylaşılan erişim imzası (SAS) kimlik doğrulama hizmet veri yolu abonelikleri ile](http://code.msdn.microsoft.com/Using-Shared-Access-e605b37c) örnek.

En fazla 12 Bu kurallar, bir hizmet veri yolu ad alanı, kuyruk veya konu yapılandırılabilir. Bir hizmet veri yolu ad alanı üzerinde yapılandırılmış olan kurallar bu ad alanındaki tooall varlıklara uygulanır.

![SAS](./media/service-bus-sas/service-bus-namespace.png)

Bu şekilde, hello *manageRuleNS*, *sendRuleNS*, ve *listenRuleNS* yetkilendirme kuralları uygula S1 tooboth sırasını ve konu T1, sırada *listenRuleQ*  ve *sendRuleQ* yalnızca tooqueue S1 uygulamak ve *sendRuleT* yalnızca tootopic T1 uygular.

anahtar parametrelerinin hello bir [Rootmanagesharedaccesskey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) aşağıdaki gibidir:

| Parametre | Açıklama |
| --- | --- |
| *Anahtar adı* |Merhaba yetkilendirme kuralı tanımlayan bir dize. |
| *PrimaryKey* |İmzalama ve hello SAS belirteci doğrulanırken bir base64 ile kodlanmış 256 bit birincil anahtar. |
| *SecondaryKey* |İmzalama ve hello SAS belirteci doğrulanırken bir base64 ile kodlanmış 256 bit ikincil anahtarı. |
| *ErişimHakları* |Merhaba yetkilendirme kuralı tarafından verilen erişim hakları listesi. Bu haklar dinle, Gönder ve Yönet hakların herhangi bir koleksiyonu olabilir. |

Hizmet veri yolu ad alanı sağlandığında bir [Rootmanagesharedaccesskey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule), ile [KeyName](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_KeyName) çok ayarlamak**RootManageSharedAccessKey**, varsayılan olarak oluşturulur.

## <a name="generate-a-shared-access-signature-token"></a>Paylaşılan erişim imzası (belirteç) oluştur

Hello İlkesi kendisi için Service Bus hello erişim belirteci değil. Bu hangi hello erişim belirteci - ya da hello birincil veya ikincil anahtarı kullanılarak oluşturulur hello nesnesidir. Merhaba paylaşılan erişim yetkilendirme kuralında belirtilen anahtarları imzalama erişim toohello sahip herhangi bir istemci hello SAS belirteci oluşturabilir. Merhaba belirteci biçimi aşağıdaki hello dizesinde dikkatle hazırlayın tarafından oluşturulur:

```
SharedAccessSignature sig=<signature-string>&se=<expiry>&skn=<keyName>&sr=<URL-encoded-resourceURI>
```

Burada `signature-string` hello belirteci hello kapsamını hello SHA-256 Karması (**kapsam** hello önceki bölümde açıklandığı gibi) eklenmiş CRLF ve sona erme saati (hello dönem bu yana saniye cinsinden: `00:00:00 UTC` 1 Ocak 1970'ten üzerinde). 

> [!NOTE]
> tooavoid bir kısa belirteç süre sonu zamanı en az bir 32 bit işaretsiz tamsayıyı veya uzun süre (64 bit) tamsayı tercihen hello sona erme süresi değeri kodlamak önerilir.  
> 
> 

Merhaba karma sahte kod aşağıdaki benzer toohello arar ve 32 bayt döndürür.

```
SHA-256('https://<yournamespace>.servicebus.windows.net/'+'\n'+ 1438205742)
```

Merhaba karma olmayan değerler hello **SharedAccessSignature** hello alıcı hello karma hesaplayabilirsiniz böylece dize hello ile aynı parametreleri, onu döndürdüğünden emin toobe aynı sonucu hello. Merhaba URI hello kapsamını belirtir ve hello İlkesi kullanılan toobe toocompute hello karması hello anahtar adını tanımlar. Bu, güvenlik açısından önemlidir. Hangi hello alıcı (Service Bus) hesaplar Hello imza eşleşmiyorsa, erişim reddedildi. Bu noktada hello gönderenden erişim toohello anahtarı var ve hello İlkesi'nde belirtilen hello hakları verilmelidir emin olabilirsiniz.

Bu işlem için kodlanmış hello kaynak URI'si kullanması gerektiğini unutmayın. Merhaba URI hello Service Bus kaynak toowhich erişimi tam URI'sini talep hello kaynaktır. Örneğin, `http://<namespace>.servicebus.windows.net/<entityPath>` veya `sb://<namespace>.servicebus.windows.net/<entityPath>`; diğer bir deyişle, `http://contoso.servicebus.windows.net/contosoTopics/T1/Subscriptions/S3`.

Bu URI tarafından ya da hiyerarşik üst öğelerinden biri tarafından belirtilen hello varlıkta hello paylaşılan erişim yetkilendirme kuralı imzalama için kullanılan yapılandırılmış olması gerekir. Örneğin, `http://contoso.servicebus.windows.net/contosoTopics/T1` veya `http://contoso.servicebus.windows.net` hello önceki örnekte.

Bir SAS belirteci hello tüm kaynaklar için geçerli `<resourceURI>` hello kullanılan `signature-string`.

Merhaba [KeyName](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_KeyName) hello SAS belirteci toohello başvuruyor **keyName** Merhaba paylaşılan erişim yetkilendirme kuralı toogenerate hello belirteci kullanılır.

Merhaba *URL kodlanmış resourceURI* gerekir olması hello hello dize-için-oturum aç hello imza hello hesaplaması sırasında kullanılan URI hello aynıdır. Olmalıdır [yüzde olarak kodlanmış](https://msdn.microsoft.com/library/4fkewx0t.aspx).

Hello kullanılan hello anahtarları düzenli aralıklarla yeniden önerilir [Rootmanagesharedaccesskey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) nesnesi. Uygulamaları hello genellikle kullanması gereken [PrimaryKey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_PrimaryKey) toogenerate bir SAS belirteci. Merhaba anahtarlarını yeniden oluştururken hello değiştirmelisiniz [SecondaryKey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_SecondaryKey) ile Merhaba eski birincil anahtar ve hello yeni birincil anahtarı olarak yeni bir anahtar oluşturmak. Bu, hello eski birincil anahtara sahip verilmiş olan ve henüz süresinin dolmadığını yetkilendirme için belirteçleri kullanarak toocontinue sağlar.

Bir anahtar güvenliği aşıldığında ve toorevoke hello anahtarlara sahip değilse, her iki hello yeniden [PrimaryKey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_PrimaryKey) ve hello [SecondaryKey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_SecondaryKey) , bir [Rootmanagesharedaccesskey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule), bunları yeni anahtarlarla değiştiriliyor. Bu yordamı hello eski anahtarlarla imzalanması tüm belirteçleri geçersiz kılar.

## <a name="how-toouse-shared-access-signature-authentication-with-service-bus"></a>Nasıl Service Bus ile paylaşılan erişim imzası kimlik doğrulaması toouse

Aşağıdaki senaryolar hello yetkilendirme kuralları yapılandırma, nesil SAS belirteci ve istemci kimlik doğrulaması içerir.

Bir tam için hello yapılandırması ve kullandığı SAS yetkilendirme gösterilmektedir bir hizmet veri yolu uygulaması çalışma örneği bkz [Service Bus ile paylaşılan erişim imzası kimlik doğrulaması](http://code.msdn.microsoft.com/Shared-Access-Signature-0a88adf8). Ad alanları veya konuları toosecure Service Bus Aboneliklerde yapılandırılmış SAS yetkilendirme kuralları hello kullanımını göstermektedir ilgili bir örnek aşağıda verilmiştir: [hizmet veri yolu abonelikleri ile kullanarak paylaşılan erişim imzası (SAS) kimlik doğrulaması ](http://code.msdn.microsoft.com/Using-Shared-Access-e605b37c).

## <a name="access-shared-access-authorization-rules-on-a-namespace"></a>Bir ad alanında erişim paylaşılan erişim yetkilendirme kuralları

İşlemler hello hizmet veri yolu ad alanı kök sertifika kimlik doğrulaması gerektirir. Azure aboneliğiniz için bir yönetim sertifikası yüklemeniz gerekir. tooupload bir yönetim sertifikası hello adımları [burada](../cloud-services/cloud-services-configure-ssl-certificate-portal.md#step-3-upload-a-certificate), hello kullanarak [Azure portal][Azure portal]. Azure yönetim sertifikaları hakkında daha fazla bilgi için bkz: Merhaba [Azure sertifikalara genel bakış](../cloud-services/cloud-services-certs-create.md#what-are-management-certificates).

bir hizmet veri yolu ad alanı paylaşılan erişim yetkilendirme kurallarının erişmek için hello uç noktası aşağıdaki gibidir:

```http
https://management.core.windows.net/{subscriptionId}/services/ServiceBus/namespaces/{namespace}/AuthorizationRules/
```

toocreate bir [Rootmanagesharedaccesskey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) nesne üzerinde bir hizmet veri yolu ad alanı, JSON veya XML olarak serileştirilmiş hello kural bilgileri ile Bu uç noktada POST işlemine yürütün. Örneğin:

```csharp
// Base address for accessing authorization rules on a namespace
string baseAddress = @"https://management.core.windows.net/<subscriptionId>/services/ServiceBus/namespaces/<namespace>/AuthorizationRules/";

// Configure authorization rule with base64-encoded 256-bit key and Send rights
var sendRule = new SharedAccessAuthorizationRule("contosoSendAll",
    SharedAccessAuthorizationRule.GenerateRandomKey(),
    new[] { AccessRights.Send });

// Operations on hello Service Bus namespace root require certificate authentication.
WebRequestHandler handler = new WebRequestHandler
{
    ClientCertificateOptions = ClientCertificateOption.Manual
};
// Access hello management certificate by subject name
handler.ClientCertificates.Add(GetCertificate(<certificateSN>));

HttpClient httpClient = new HttpClient(handler)
{
    BaseAddress = new Uri(baseAddress)
};
httpClient.DefaultRequestHeaders.Accept.Add(
    new MediaTypeWithQualityHeaderValue("application/json"));
httpClient.DefaultRequestHeaders.Add("x-ms-version", "2015-01-01");

// Execute a POST operation on hello baseAddress above toocreate an auth rule
var postResult = httpClient.PostAsJsonAsync("", sendRule).Result;
```

Benzer şekilde, bir GET işlemi hello ad yapılandırılmış hello uç nokta tooread hello yetkilendirme kuralları kullanın.

tooupdate ya da delete belirli yetkilendirme kuralı uç noktası aşağıdaki hello kullan:

```http
https://management.core.windows.net/{subscriptionId}/services/ServiceBus/namespaces/{namespace}/AuthorizationRules/{KeyName}
```

## <a name="access-shared-access-authorization-rules-on-an-entity"></a>Bir varlık üzerinde erişim paylaşılan erişim yetkilendirme kuralları

Erişebileceğiniz bir [Microsoft.ServiceBus.Messaging.SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) bir Service Bus kuyruğu veya konu hello üzerinden yapılandırılmış nesne [AuthorizationRules](/dotnet/api/microsoft.servicebus.messaging.authorizationrules) hello koleksiyonunda karşılık gelen [QueueDescription](/dotnet/api/microsoft.servicebus.messaging.queuedescription) veya [TopicDescription](/dotnet/api/microsoft.servicebus.messaging.topicdescription).

koddan hello nasıl bir kuyruk için tooadd yetkilendirme kuralları gösterir.

```csharp
// Create an instance of NamespaceManager for hello operation
NamespaceManager nsm = NamespaceManager.CreateFromConnectionString(
    <connectionString> );
QueueDescription qd = new QueueDescription( <qPath> );

// Create a rule with send rights with keyName as "contosoQSendKey"
// and add it toohello queue description.
qd.Authorization.Add(new SharedAccessAuthorizationRule("contosoSendKey",
    SharedAccessAuthorizationRule.GenerateRandomKey(),
    new[] { AccessRights.Send }));

// Create a rule with listen rights with keyName as "contosoQListenKey"
// and add it toohello queue description.
qd.Authorization.Add(new SharedAccessAuthorizationRule("contosoQListenKey",
    SharedAccessAuthorizationRule.GenerateRandomKey(),
    new[] { AccessRights.Listen }));

// Create a rule with manage rights with keyName as "contosoQManageKey"
// and add it toohello queue description.
// A rule with manage rights must also have send and receive rights.
qd.Authorization.Add(new SharedAccessAuthorizationRule("contosoQManageKey",
    SharedAccessAuthorizationRule.GenerateRandomKey(),
    new[] {AccessRights.Manage, AccessRights.Listen, AccessRights.Send }));

// Create hello queue.
nsm.CreateQueue(qd);
```

## <a name="use-shared-access-signature-authorization"></a>Paylaşılan erişim imzası yetkilendirme kullanın

Merhaba Service Bus .NET kitaplıklarıyla Hello Azure .NET SDK kullanarak uygulamalar SAS yetkilendirme hello aracılığıyla kullanabilir [SharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.sharedaccesssignaturetokenprovider) sınıfı. Merhaba aşağıdaki kod hello belirteç sağlayıcısı toosend iletileri tooa Service Bus kuyruğuna hello kullanımını gösterir.

```csharp
Uri runtimeUri = ServiceBusEnvironment.CreateServiceUri("sb",
    <yourServiceNamespace>, string.Empty);
MessagingFactory mf = MessagingFactory.Create(runtimeUri,
    TokenProvider.CreateSharedAccessSignatureTokenProvider(keyName, key));
QueueClient sendClient = mf.CreateQueueClient(qPath);

//Sending hello message tooqueue.
BrokeredMessage helloMessage = new BrokeredMessage("Hello, Service Bus!");
helloMessage.MessageId = "SAS-Sample-Message";
sendClient.Send(helloMessage);
```

Uygulamalar da SAS kimlik doğrulaması için bağlantı dizelerini kabul yöntemlerinde bir SAS bağlantı dizesi kullanarak kullanabilirsiniz.

Service Bus geçişlerini ile bu toouse SAS yetkilendirme unutmayın, SAS anahtarları hello Service Bus ad alanı üzerinde yapılandırılmış kullanabilirsiniz. Bir geçiş hello ad açıkça oluşturursanız ([NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) ile bir [RelayDescription](/dotnet/api/microsoft.servicebus.messaging.relaydescription)) nesne hello SAS kuralları yalnızca bu geçiş için ayarlayabilirsiniz. Hizmet veri yolu abonelikleri ile toouse SAS yetkilendirme, bir hizmet veri yolu ad alanı veya konu yapılandırılmış SAS tuşlarını kullanabilirsiniz.

## <a name="use-hello-shared-access-signature-at-http-level"></a>Merhaba paylaşılan erişim imzası (HTTP düzeyinde) kullanın

Nasıl toocreate paylaşılan erişim imzaları Service Bus içinde herhangi bir varlık için olduğunuz bildiğinize göre bir HTTP POST tooperform hazır:

```http
POST https://<yournamespace>.servicebus.windows.net/<yourentity>/messages
Content-Type: application/json
Authorization: SharedAccessSignature sr=https%3A%2F%2F<yournamespace>.servicebus.windows.net%2F<yourentity>&sig=<yoursignature from code above>&se=1438205742&skn=KeyName
ContentType: application/atom+xml;type=entry;charset=utf-8
``` 

Unutmayın, bu her şey için çalışır. Bir kuyruk, konu veya abonelik için SAS oluşturabilirsiniz. 

Bir gönderici veya istemci bir SAS belirteci vermek, başlangıç anahtarı doğrudan sahip olmayan ve hello karma tooobtain tersine çeviremezsiniz onu. Bu nedenle, Denetim nasıl ve ne erişebilecekleri üzerinden uzun sahip. Önemli şey tooremember hello İlkesi'nde hello birincil anahtar değiştirirseniz, tüm paylaşılan erişim imzaları oluşturulan doğrulanacak ' dir.

## <a name="use-hello-shared-access-signature-at-amqp-level"></a>Merhaba paylaşılan erişim imzası (AMQP düzeyinde) kullanın

Merhaba önceki bölümde nasıl toouse hello veri toohello Service Bus göndermek için bir HTTP POST isteği ile SAS belirteci gördünüz. Bildiğiniz gibi Service Bus erişebilirsiniz kullanarak hello Gelişmiş Message Queuing Protokolü (Merhaba tercih edilen Protokolü toouse Performans nedeniyle, birçok senaryoda olan AMQP). Merhaba AMQP ile SAS belirteci kullanımını hello belgede açıklanan [AMQP Claim-Based güvenlik sürüm 1.0](https://www.oasis-open.org/committees/download.php/50506/amqp-cbs-v1%200-wd02%202013-08-12.doc) diğer bir deyişle içinde çalışma taslak bugün 2013 Azure tarafından desteklenen iyi ancak bu yana.

Toosend veri tooService Bus başlatmadan önce hello yayımcı hello SAS belirteci adlı bir AMQP ileti tooa iyi tanımlanmış AMQP düğümü içine göndermelidir **$cbs** (Merhaba hizmet tooacquire tarafından kullanılan "özel" bir sıra olarak bakın ve tüm doğrulama Merhaba SAS belirteci). Merhaba yayımcı hello belirtmelisiniz **ReplyTo** alan hello AMQP ileti içine; bu hangi hello hizmet yanıtlar hello belirteci doğrulama (Basit istek/yanıt desen arasında hello sonucunu toohello yayımcıyla hello düğümü Yayımcı ve hizmeti). Bu yanıt düğüm oluşturulmuş "açık"dinamik oluşturma uzak düğümün hakkında"Merhaba AMQP 1.0 belirtimi tarafından açıklanan konuşarak hello anında". Merhaba yayımcı, bu hello SAS belirteci geçerli denetledikten sonra İleri gitmektedir ve toosend veri toohello hizmetini başlatın.

Merhaba aşağıdaki adımları nasıl toosend hello SAS belirteci hello kullanarak AMQP protokolüyle Göster [AMQP.Net Lite](https://github.com/Azure/amqpnetlite) kitaplığı. Merhaba resmi kullanamıyorsanız kullanışlıdır hizmet veri yolu SDK'sı (örneğin üzerinde WinRT, .net Compact Framework, .net mikro Framework ve Mono) C'de geliştirme\#. Elbette, bu kitaplık yararlıdır toohelp anlamak nasıl talep tabanlı güvenlik düzeyindeki hello HTTP (bir HTTP POST isteği ve hello SAS belirteci içinde gönderilen hello "Yetkilendirme" başlığı) nasıl çalışır anlatıldığı gibi hello AMQP düzeyinde çalışır. AMQP hakkında ayrıntılı oluşturabildiğinden ihtiyaç duymuyorsanız hello resmi kullanabilirsiniz .net ile Service Bus SDK sizin için ne yapacağını Framework uygulamaları.

### <a name="c35"></a>C&#35;

```csharp
/// <summary>
/// Send claim-based security (CBS) token
/// </summary>
/// <param name="shareAccessSignature">Shared access signature (token) toosend</param>
private bool PutCbsToken(Connection connection, string sasToken)
{
    bool result = true;
    Session session = new Session(connection);

    string cbsClientAddress = "cbs-client-reply-to";
    var cbsSender = new SenderLink(session, "cbs-sender", "$cbs");
    var cbsReceiver = new ReceiverLink(session, cbsClientAddress, "$cbs");

    // construct hello put-token message
    var request = new Message(sasToken);
    request.Properties = new Properties();
    request.Properties.MessageId = Guid.NewGuid().ToString();
    request.Properties.ReplyTo = cbsClientAddress;
    request.ApplicationProperties = new ApplicationProperties();
    request.ApplicationProperties["operation"] = "put-token";
    request.ApplicationProperties["type"] = "servicebus.windows.net:sastoken";
    request.ApplicationProperties["name"] = Fx.Format("amqp://{0}/{1}", sbNamespace, entity);
    cbsSender.Send(request);

    // receive hello response
    var response = cbsReceiver.Receive();
    if (response == null || response.Properties == null || response.ApplicationProperties == null)
    {
        result = false;
    }
    else
    {
        int statusCode = (int)response.ApplicationProperties["status-code"];
        if (statusCode != (int)HttpStatusCode.Accepted && statusCode != (int)HttpStatusCode.OK)
        {
            result = false;
        }
    }

    // hello sender/receiver may be kept open for refreshing tokens
    cbsSender.Close();
    cbsReceiver.Close();
    session.Close();

    return result;
}
```

Merhaba `PutCbsToken()` yöntemi alır hello *bağlantı* (Merhaba tarafından sağlanan AMQP bağlantı sınıf örneği [AMQP .NET Lite Kitaplığı](https://github.com/Azure/amqpnetlite)) hello TCP bağlantısı toohello hizmeti ve hello temsil eden *sasToken* hello SAS belirteci toosend olan parametre. 

> [!NOTE]
> Merhaba bağlantısı ile oluşturulur önemlidir **SASL kimlik doğrulama mekanizması ayarlamak tooEXTERNAL** (ve kullanıcı adı ve parola toosend hello SAS belirteci gerekmediğinde kullanılan varsayılan DÜZ hello değil).
> 
> 

Ardından, hello yayımcı hello SAS belirteci göndermek ve hello hizmetinden hello yanıt (Merhaba belirteci doğrulama sonucu) almak için iki AMQP bağlantılarını oluşturur.

Merhaba AMQP ileti bir özellikler kümesi ve basit bir ileti daha fazla bilgi içerir. Merhaba SAS belirteci hello (kendi oluşturucusunu kullanarak) hello ileti gövdesi ' dir. Merhaba **"ReplyTo"** özelliği toohello düğüm adı (değiştirebileceğiniz adını ve dinamik olarak hello hizmeti tarafından oluşturulan istiyorsanız) hello alıcı bağlantıyı hello doğrulama sonucu almak için ayarlanır. Merhaba son üç uygulama/özel özellikler hello hizmet tooindicate tarafından kullanılan ne tür isteğe bağlı olarak işlem tooexecute sahiptir. Merhaba CBS taslak belirtim tarafından açıklandığı gibi hello olmalıdır **işlem adı** ("put-token"), hello **Belirtecin türü** (Bu durumda, bir "servicebus.windows.net:sastoken"), gelen ve hello **" adı"Merhaba İzleyici** toowhich hello belirteci (Merhaba tüm varlık) uygulanır.

Merhaba SAS belirteci hello gönderen bağlantısında gönderdikten sonra hello yayımcı hello yanıt hello alıcı bağlantıyı okumalısınız. Merhaba yanıt olan adlı bir uygulama özelliği içeren basit bir AMQP ileti **"durum kodu"** aynı değer bir HTTP durum kodu hello içerebilir.

## <a name="rights-required-for-service-bus-operations"></a>Hizmet veri yolu işlemleri için gereken haklar

Merhaba aşağıdaki tabloda Service Bus kaynaklarını üzerinde çeşitli işlemler için gerekli hello erişim haklarını gösterir.

| İşlem | Gerekli talep | Talep kapsamı |
| --- | --- | --- |
| **Namespace** | | |
| Yetkilendirme kuralı üzerinde bir ad alanı yapılandırma |Yönet |Herhangi bir ad alanı adresi |
| **Hizmet kayıt defteri** | | |
| Özel ilkeler listeleme |Yönet |Herhangi bir ad alanı adresi |
| Bir ad alanı üzerinde dinleme yapmaya başlamasını |Dinleme |Herhangi bir ad alanı adresi |
| Bir ad alanında iletileri tooa dinleyicisi Gönder |Gönder |Herhangi bir ad alanı adresi |
| **Sırası** | | |
| Bir kuyruk oluşturma |Yönet |Herhangi bir ad alanı adresi |
| Bir kuyruk silme |Yönet |Herhangi bir geçerli sıra adresi |
| Kuyruklar listeleme |Yönet |$ Kaynakları/sıraları |
| Al Hello sıra açıklaması |Yönet |Herhangi bir geçerli sıra adresi |
| Sıra için yetkilendirme kuralı yapılandırma |Yönet |Herhangi bir geçerli sıra adresi |
| Toohello kuyruğa Gönder |Gönder |Herhangi bir geçerli sıra adresi |
| Kuyruktan ileti alma |Dinleme |Herhangi bir geçerli sıra adresi |
| Bırakın ya da iletileri selamlama iletisine gözlem kilidinin modunda aldıktan sonra tamamlamak |Dinleme |Herhangi bir geçerli sıra adresi |
| Sonraki alınması için bir ileti erteleme |Dinleme |Herhangi bir geçerli sıra adresi |
| Sahipsiz bir ileti |Dinleme |Herhangi bir geçerli sıra adresi |
| İleti sırası oturumla ilişkili hello durumu alma |Dinleme |Herhangi bir geçerli sıra adresi |
| İleti sırası oturumla ilişkili hello durumunu ayarlama |Dinleme |Herhangi bir geçerli sıra adresi |
| **Konu** | | |
| Konu başlığı oluşturma |Yönet |Herhangi bir ad alanı adresi |
| Bir konu Sil |Yönet |Herhangi bir geçerli konu adresi |
| Konular listeleme |Yönet |$ Kaynakları/konuları |
| Al Hello konu açıklaması |Yönet |Herhangi bir geçerli konu adresi |
| Bir konu için yetkilendirme kuralı yapılandırma |Yönet |Herhangi bir geçerli konu adresi |
| Toohello konu gönderin |Gönder |Herhangi bir geçerli konu adresi |
| **Abonelik** | | |
| Abonelik oluşturma |Yönet |Herhangi bir ad alanı adresi |
| Aboneliği silme |Yönet |.. /myTopic/Subscriptions/mySubscription |
| Aboneliklerini listeleme |Yönet |.. / myTopic/abonelikleri |
| Al abonelik açıklaması |Yönet |.. /myTopic/Subscriptions/mySubscription |
| Bırakın ya da iletileri selamlama iletisine gözlem kilidinin modunda aldıktan sonra tamamlamak |Dinleme |.. /myTopic/Subscriptions/mySubscription |
| Sonraki alınması için bir ileti erteleme |Dinleme |.. /myTopic/Subscriptions/mySubscription |
| Sahipsiz bir ileti |Dinleme |.. /myTopic/Subscriptions/mySubscription |
| Bir konu oturumla ilişkili hello durumunu Al |Dinleme |.. /myTopic/Subscriptions/mySubscription |
| Bir konu oturumla ilişkili hello durumunu ayarlama |Dinleme |.. /myTopic/Subscriptions/mySubscription |
| **Kuralları** | | |
| Bir kural oluşturun |Yönet |.. /myTopic/Subscriptions/mySubscription |
| Kural silme |Yönet |.. /myTopic/Subscriptions/mySubscription |
| Kuralları listeleme |Dinlemek veya yönetme |.. /myTopic/Subscriptions/mySubscription/Rules 

## <a name="next-steps"></a>Sonraki adımlar

Service Bus Mesajlaşma, hakkında daha fazla toolearn aşağıdaki konularda hello bakın.

* [Service Bus ile ilgili temel bilgiler](service-bus-fundamentals-hybrid-solutions.md)
* [Service Bus kuyrukları, konu başlıkları ve abonelikleri](service-bus-queues-topics-subscriptions.md)
* [Nasıl toouse Service Bus kuyrukları](service-bus-dotnet-get-started-with-queues.md)
* [Nasıl toouse Service Bus konuları ve abonelikleri](service-bus-dotnet-how-to-use-topics-subscriptions.md)

[Azure portal]: https://portal.azure.com