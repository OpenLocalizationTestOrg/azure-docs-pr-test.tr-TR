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
# <a name="relay-hybrid-connections-node-api-overview"></a>Karma bağlantılar düğümü API genel bakış geçiş

## <a name="overview"></a>Genel Bakış

Merhaba [ `hyco-ws` ](https://www.npmjs.com/package/hyco-ws) Azure geçişi karma bağlantılar için düğüm paketi üzerine kurulmuştur ve hello genişletir ['ws'](https://www.npmjs.com/package/ws) NPM paket. Bu paket, temel pakette, tüm dışarı yeniden aktarır ve hello Azure geçiş hizmeti karma bağlantılar özelliği ile tümleştirmeyi etkinleştir yeni dışarı ekler. 

Var olan uygulamalar, `require('ws')` bu paketle birlikte kullanabilirsiniz `require('hyco-ws')` bunun yerine, ayrıca sağlayan, bir uygulama dinleme "Merhaba güvenlik duvarı içinde" ve karma bağlantılar aracılığıyla yerel olarak üzerinden WebSocket bağlantıları için tümünü karma senaryolar aynı hello zaman.
  
## <a name="documentation"></a>Belgeler

Merhaba apı'leridir [hello ana 'ws' paketinde belgelenen](https://github.com/websockets/ws/blob/master/doc/ws.md). Bu makalede, bu paket, taban çizgisinden nasıl farklı açıklanmaktadır. 

Merhaba hello temel paketi ve bu 'hyco-ws' arasındaki temel farklılıklar olan aracılığıyla verilen yeni bir sunucu sınıfı ekler `require('hyco-ws').RelayedServer`ve birkaç yardımcı yöntemler.

### <a name="package-helper-methods"></a>Paket yardımcı yöntemler

Aşağıdaki gibi başvurabilir hello paketi verme sırasında birkaç yardımcı program yöntemleri vardır:

```JavaScript
const WebSocket = require('hyco-ws');

var listenUri = WebSocket.createRelayListenUri('namespace.servicebus.windows.net', 'path');
listenUri = WebSocket.appendRelayToken(listenUri, 'ruleName', '...key...')
...

```

Hello yardımcı yöntemler bu paketi ile kullanmak için olan, ancak web veya aygıt istemcileri toocreate dinleyicileri veya Gönderenler etkinleştirmek için bir düğümü sunucu tarafından da kullanılabilir. Merhaba sunucu kısa süreli belirteçler katıştırmak URI'ler geçirerek bu yöntemleri kullanır. Bu URI ayarı HTTP üstbilgilerini hello WebSocket el sıkışma için desteklemeyen ortak WebSocket yığınları ile de kullanılabilir. URI için öncelikle bu kitaplığı dış kullanım senaryoları desteklenir hello içine yetkilendirme belirteçleri katıştırma. 

#### <a name="createrelaylistenuri"></a>createRelayListenUri

```JavaScript
var uri = createRelayListenUri([namespaceName], [path], [[token]], [[id]])
```

Verilen ad ve yol hello için geçerli bir Azure geçişi karma bağlantı dinleyici URI oluşturur. Bu URI hello geçiş sürümü hello WebSocketServer sınıfı ile kullanılabilir.

- `namespaceName`(gerekli) - etki alanı adını hello Azure geçiş ad alanı toouse hello.
- `path`(gerekli) - bu ad alanında mevcut bir Azure geçişi karma bağlantıyı adını hello.
- `token`(isteğe bağlı) - daha önce verilen geçiş erişim belirteci, hello dinleyicisi URI'si katıştırılmış (Merhaba aşağıdaki örneğine bakın).
- `id`(isteğe bağlı) - istekleri uçtan uca tanılama izlemeyi sağlayan bir izleme tanımlayıcısı.

Merhaba `token` değer isteğe bağlıdır ve olası toosend HTTP üstbilgileri hello WebSocket el sıkışması, birlikte değilse hello hello W3C WebSocket yığınına sahip olduğu gibi yalnızca kullanılmalıdır.                  


#### <a name="createrelaysenduri"></a>createRelaySendUri
 
```JavaScript
var uri = createRelaySendUri([namespaceName], [path], [[token]], [[id]])
```

Verilen ad ve yol hello için geçerli bir Azure geçişi karma bağlantı gönderme URI oluşturur. Bu URI herhangi bir Web yuvası istemci ile kullanılabilir.

- `namespaceName`(gerekli) - etki alanı adını hello Azure geçiş ad alanı toouse hello.
- `path`(gerekli) - bu ad alanında mevcut bir Azure geçişi karma bağlantıyı adını hello.
- `token`(isteğe bağlı) - hello katıştırılmış önceden düzenlenen bir geçiş erişim belirteci Gönder URI (Merhaba aşağıdaki örneğine bakın).
- `id`(isteğe bağlı) - istekleri uçtan uca tanılama izlemeyi sağlayan bir izleme tanımlayıcısı.

Merhaba `token` değer isteğe bağlıdır ve olası toosend HTTP üstbilgileri hello WebSocket el sıkışması, birlikte değilse hello hello W3C WebSocket yığınına sahip olduğu gibi yalnızca kullanılmalıdır.                   


#### <a name="createrelaytoken"></a>createRelayToken 

```JavaScript
var token = createRelayToken([uri], [ruleName], [key], [[expirationSeconds]])
```

Verilen hello hedef URI, SAS kuralı ve hello süre sonu bağımsız değişken belirtilmezse saniye veya bir saat sayısını hello geçerli anlık verilen hello için geçerli olan SAS kuralı anahtarı için bir Azure geçiş paylaşılan erişim imzası (SAS) belirteci oluşturur.

- `uri`(gerekli) - hangi Merhaba verilen toobe belirtecidir URI hello. Merhaba URI normalleştirilmiş toouse hello HTTP düzenidir ve sorgu dize bilgilerini yapılandırıldıktan.
- `ruleName`SAS URI'si verilen hello tarafından temsil edilen ya da hello varlık için ad kural (gerekli) - veya hello için ad alanı URI ana bilgisayar bölümü tarafından hello temsil.
- `key`(gerekli) - hello SAS kural için geçerli anahtar. 
- `expirationSeconds`(isteğe bağlı) - belirteç hello oluşturulan kadar hello saniyeyi sona. Belirtilmezse, hello 1 saat (3600) varsayılandır.

verilen hello belirteci confers belirtilen hello ile ilişkili hello hakları süresi verilen hello için SAS kuralı.

#### <a name="appendrelaytoken"></a>appendRelayToken

```JavaScript
var uri = appendRelayToken([uri], [ruleName], [key], [[expirationSeconds]])
```

Bu bir yöntemdir işlevsel olarak eşdeğer toohello `createRelayToken` yöntemi belgelenen daha önce ancak döndürür hello belirteci doğru eklenmiş toohello giriş URI'si.

### <a name="class-wsrelayedserver"></a>Sınıf ws. RelayedServer

Merhaba `hycows.RelayedServer` sınıfı, bir alternatif toohello `ws.Server` hello yerel ağda dinlemez ancak dinleme toohello Azure geçiş hizmeti temsilci sınıfı.

Merhaba iki sınıflardır çoğunlukla hello kullanarak var olan bir uygulama anlamı uyumlu sözleşme `ws.Server` sınıfı değiştirilmiş toouse geçişli hello sürüm kolayca olabilir. Merhaba temel farklılıklar hello oluşturucusu ve hello kullanılabilir seçenekler şunlardır.

#### <a name="constructor"></a>Oluşturucusu  

```JavaScript 
var ws = require('hyco-ws');
var server = ws.RelayedServer;

var wss = new server(
    {
        server: ws.createRelayListenUri(ns, path),
        token: function() { return ws.createRelayToken('http://' + ns, keyrule, key); }
    });
```

Merhaba `RelayedServer` oluşturucu bağımsız değişkenleri hello daha farklı bir kümesini destekler `Server`bir tek başına dinleyicisi veya varolan bir HTTP dinleyicisi Framework'e katıştırılmış mümkün toobe olmadığından. Ayrıca daha az seçenek kullanılabilir olduğundan hello WebSocket yönetimini büyük ölçüde temsilci toohello geçiş hizmeti olduğundan.

Oluşturucu bağımsız değişkenleri:

- `server`(gerekli) - hello URI genellikle hello WebSocket.createRelayListenUri() yardımcı yöntemi ile oluşturulan hangi toolisten üzerinde bir karma bağlantı adı için tam.
- `token`(gerekli) - bu bağımsız değişken, daha önce verilen bir belirteç dizesi veya tooobtain belirteci bir dize çağrılan bir geri çağırma işlevini tutar. Merhaba geri arama seçeneğini tercih edilen, aynıdır belirteci yenileme sağlar.

#### <a name="events"></a>Olaylar

`RelayedServer`örnekleri, toohandle gelen istekleri etkinleştirmek bağlantıları kurmak ve hata koşullarını algılamak üç olayları yayma. Toohello abone olmalısınız `connect` olay toohandle iletileri. 

##### <a name="headers"></a>Üstbilgileri

```JavaScript 
function(headers)
```

Merhaba `headers` yalnızca gelen bağlantının, hello üstbilgileri toosend toohello istemci değiştirilmesini etkinleştirme kabul edilmeden önce olayı oluşturulur. 

##### <a name="connection"></a>bağlantı

```JavaScript
function(socket)
```

Yeni bir WebSocket bağlantı kabul edildiğinde yayılan. Merhaba nesne türüdür `ws.WebSocket`, hello temel paketi ile aynı.


##### <a name="error"></a>error

```JavaScript
function(error)
```

Bir hata Hello temel sunucu yayar, burada iletilir.  

#### <a name="helpers"></a>Yardımcıları

geçirilen bir sunucu ve hemen tooincoming bağlantıları hello abone paketini toosimplify başlangıç de hello örneklerde, aşağıdaki gibi kullanılır basit yardımcı bir işlev gösterir:

##### <a name="createrelayedlistener"></a>createRelayedListener

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

##### <a name="createrelayedserver"></a>createRelayedServer

```javascript
var server = createRelayedServer([options], [connectCallback] )
```

Bu yöntem hello Oluşturucusu toocreate hello RelayedServer yeni bir örneğini çağırır ve sağlanan hello geri çağırma toohello 'bağlantı' olay abone olur.
 
##### <a name="relayedconnect"></a>relayedConnect

Yalnızca hello yansıtma `createRelayedServer` işlevinde yardımcı `relayedConnect` istemci bağlantısını oluşturur ve toohello 'açık' hello elde edilen yuva olayına abone olur.

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

## <a name="next-steps"></a>Sonraki adımlar
toolearn Azure geçişi hakkında daha fazla bilgi için bu bağlantıları ziyaret edin:
* [Azure Geçiş nedir?](relay-what-is-it.md)
* [Kullanılabilir geçiş API'leri](relay-api-overview.md)
