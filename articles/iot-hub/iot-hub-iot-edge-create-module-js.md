---
title: "aaaCreate bir Node.js ile Azure IOT kenar Modülü | Microsoft Docs"
description: "Bu öğretici bir bırak veri dönüştürücü modülünü kullanarak toowrite nasıl hello en son Azure IOT kenar NPM paket ve Yeoman paylaşan Oluşturucu."
services: iot-hub
author: sushi
manager: timlt
ms.service: iot-hub
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: js
ms.topic: article
ms.date: 06/28/2017
ms.author: sushi
ms.openlocfilehash: d3e696b5a310377ffb8e99998ff0714bf7c0bb41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-iot-edge-module-with-nodejs"></a>Node.js ile Azure IOT kenar modülü oluşturun

Bu öğretici paylaşan nasıl toocreate için Azure IOT Edge'de JS modül.

Bu öğreticide, biz ortamı kurulumu aracılığıyla yol ve nasıl toowrite bir [bırak](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) veri dönüştürücü modülü hello en son Azure IOT kenar NPM paketleri kullanma.

## <a name="prerequisites"></a>Ön koşullar

Bu bölümde IOT kenar modülü geliştirme ortamınızı ayarlayın. Tooboth geçerlidir *64-bit Windows* ve *64-bit Linux (Ubuntu 14 +)* işletim sistemleri.

yazılımı aşağıdaki hello gereklidir:
* [Git istemci](https://git-scm.com/downloads).
* [Düğüm LTS](https://nodejs.org).
* `npm install -g yo`.
* `npm install -g generator-az-iot-gw-module`

## <a name="architecture"></a>Mimari

Hello Azure IOT kenar platform yoğun hello uyarlar [Von Neumann mimarisi](https://en.wikipedia.org/wiki/Von_Neumann_architecture). O hello tüm Azure IOT kenar mimari başka bir deyişle, giriş işler ve bir çıktı üretir bir sistemdir; ve tek tek her modül küçük bir giriş-çıkış alt olduğunu. Bu öğreticide, iki modülleri aşağıdaki hello tanıtmaktadır:

1. Sanal alan modül [bırak](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) sinyal ve biçimlendirilmiş dönüştürür [JSON](https://en.wikipedia.org/wiki/JSON) ileti.
2. Alınan hello yazdırır bir modül [JSON](https://en.wikipedia.org/wiki/JSON) ileti.

Merhaba aşağıdaki resimde bu proje için hello tipik son tooend veri akışı görüntüler:

![Veri akışı üç modülleri arasında](media/iot-hub-iot-edge-create-module/dataflow.png "giriş: benzetimli bırak Modülü; İşlemci: Dönüştürücü Modülü; Çıktı: Yazıcı Modülü")

## <a name="set-up-hello-environment"></a>Merhaba ortamını ayarlama
Aşağıda tooquickly ortam toostart toowrite JS ilk, bırak dönüştürücü modülüyle nasıl ayarlanacağını gösteriyoruz.

### <a name="create-module-project"></a>Modül projesi oluşturma
1. Bir komut satırı penceresi açın, çalıştırmak `yo az-iot-gw-module`.
2. Merhaba ekranında toofinish hello başlatma modül projenizin Hello adımları izleyin.

### <a name="project-structure"></a>Proje yapısı
JS modül proje bileşenleri aşağıdaki Merhaba oluşur:

`modules`-hello özelleştirilmiş JS modül kaynak dosyaları. Merhaba varsayılan Değiştir `sensor.js` ve `printer.js` kendi modülü dosyalarla.

`app.js`-hello giriş dosyası toostart hello kenar örneği.

`gw.config.json`-hello yapılandırma dosyası toocustomize hello modülleri toobe kenarından yüklendi.

`package.json`-hello modülü projesi için meta veri bilgileri.

`README.md`-hello modülü projesi için temel belgelere.


### <a name="package-file"></a>Paket dosyası

Bu `package.json` hello adı, sürüm, giriş, komut dosyaları, çalışma zamanı ve geliştirme bağımlılıklar içeren bir modülü projesi gerekli tüm hello meta veri bilgileri bildirir.

Kod parçacığını gösterir nasıl tooconfigure bırak dönüştürücü için örnek proje.
```json
{
  "name": "converter",
  "version": "1.0.0",
  "description": "BLE data converter sample for Azure IoT Edge.",
  "repository": {
    "type": "git",
    "url": "https://github.com/Azure-Samples/iot-edge-samples"
  },
  "main": "app.js",
  "scripts": {
    "start": "node app.js"
  },
  "author": "Microsoft Corporation",
  "license": "MIT",
  "dependencies": {
  },
  "devDependencies": {
    "azure-iot-gateway": "~1.1.3"
  }
}
```


### <a name="entry-file"></a>Girdi dosyası
Merhaba `app.js` hello yolu tooinitialize hello kenar örnek tanımlar. Burada herhangi bir değişiklik toomake gerekmez.

```javascript
(function() {
  'use strict';

  const Gateway = require('azure-iot-gateway');
  let config_path = './gw.config.json';

  // node app.js
  if (process.argv.length < 2) {
    throw 'Calling pattern should be node app.js.';
  }

  const gw = new Gateway(config_path);
  gw.run();
})();
```

### <a name="interface-of-module"></a>Modülün arabirimi
Bir veri işleri için işlemci olarak Azure IOT kenar modülü davranabilirsiniz: girişi almak, işlemesi ve çıktı üretir.

Merhaba giriş donanım (gibi hareket algılayıcısı) verileri, bir ileti diğer modüller ya da (örneğin, düzenli aralıklarla bir Zamanlayıcı tarafından oluşturulan bir rastgele sayı) başka bir şey olabilir.

Merhaba çıkış benzer toohello giriş, donanım davranış (gibi hello ışığı yanıp sönen), bir ileti tooother modülleri ya da (yazdırma toohello konsolu gibi) başka bir şey tetikleyebilir.

Modüller birbirleri ile kullanarak iletişim `message` nesnesi. Merhaba **içerik** , bir `message` istediğiniz verilerin herhangi bir tür temsil etme özelliğine sahip bir bayt dizisi. **Özellikler** de hello kullanılabilir `message` ve yalnızca bir dize-dize eşleme. Düşünebilirsiniz **özellikleri** bir HTTP isteğinin ya da hello meta veri dosyasının hello başlığı olarak.

Sipariş toodevelop JS Azure IOT kenar modülünde'da, toocreate gerekli hello yöntemlerini uygulayan yeni bir modül nesne gereksinim `receive()`. Bu noktada, ayrıca isteğe bağlı tooimplement hello tercih edebilirsiniz `create()` veya `start()`, veya `destroy()` de yöntemleri. Aşağıdaki kod parçacığını hello JS modül nesnesinin iskele hello gösterir.

```javascript
'use strict';

module.exports = {
  broker: null,
  configuration: null,

  create: function (broker, configuration) {
    // Default implementation.
    this.broker = broker;
    this.configuration = configuration;

    return true;
  },

  start: function () {
    // Produce
  },

  receive: function (message) {
    // Consume
  },

  destroy: function () {
  }
};
```

### <a name="converter-module"></a>Dönüştürücü Modülü
| Girdi                    | İşlemci                              | Çıktı                 | Kaynak dosya            |
| ------------------------ | -------------------------------------- | ---------------------- | ---------------------- |
| Sıcaklık veri iletisi | Ayrıştırma ve yeni bir JSON ileti oluşturun | Yapı JSON iletisi | `converter.js` |

Bu modül tipik bir Azure IOT kenar modüldür. Diğer modüllerden sıcaklık iletileri kabul eder (bir donanım modülü veya bu bizim benzetimli bırak modülü durumda); ve (Merhaba ileti kimliği, tootrigger hello sıcaklık uyarı ihtiyacımız hello özelliğini ayarlama ekleme de dahil olmak üzere vb.) yapılandırılmış tooa JSON iletinin hello sıcaklık iletiyi normalleştirir.

```javascript
receive: function (message) {
  // Initialize hello messageCount in global object at first time.
  if (!global.messageCount) {
    global.messageCount = 0;
  }

  // Read hello content and properties objects from message.
  let rawContent = JSON.parse(Buffer.from(message.content).toString('utf8'));
  let rawProperties = message.properties;

  // Generate new properties object.
  let newProperties = {
    source: rawProperties.source,
    macAddress: rawProperties.macAddress,
    temperatureAlert: rawContent.temperature > 30 ? 'true' : 'false'
  };

  // Generate new content object.
  let newContent = {
    deviceId: 'Intel NUC Gateway',
    messageId: ++global.messageCount,
    temperature: rawContent.temperature
  };

  // Publish hello new message toobroker.
  this.broker.publish(
    {
      properties: newProperties,
      content: new Uint8Array(Buffer.from(JSON.stringify(newContent), 'utf8'))
    }
  );
},
```

### <a name="printer-module"></a>Yazıcı Modülü
| Girdi                          | İşlemci | Çıktı                     | Kaynak dosya          |
| ------------------------------ | --------- | -------------------------- | -------------------- |
| Diğer modüllerden herhangi bir iletisi | Yok       | Merhaba ileti tooconsole oturum | `printer.js` |

Bu modül basit ve açıklayıcı, hangi hello alınan iletileri (özelliği, içerik) toohello terminal penceresi çıkarır.

```javascript
receive: function (message) {
  let properties = JSON.stringify(message.properties);
  let content = Buffer.from(message.content).toString('utf8');

  console.log(`printer.receive.properties - ${properties}`);
  console.log(`printer.receive.content - ${content}\n`);
}
```

### <a name="configuration"></a>Yapılandırma
Merhaba modülleri çalıştırmadan önce hello son tooconfigure hello Azure IOT kenarı ve modülleri arasında tooestablish hello bağlantıları adımdır.

Toodeclare ilk ihtiyacımız bizim `node` (itibaren Azure IOT kenar destekler yükleyicilerini farklı dillerde) tarafından başvurulan yükleyicisi kendi `name` hello bölümlerde daha sonra.

```json
"loaders": [
  {
    "type": "node",
    "name": "node"
  }
]
```

Ayrıca, biz bizim yükleyicilerini bildirdikten sonra toodeclare bizim modüller de gerekir. Benzer toodeclaring hello yükleyicileri, bunlar ayrıca başvurulabilir tarafından kendi `name` özniteliği. Bir modül bildirirken (hangi önce tanımladığımız hello biri olmalıdır) kullanması gereken toospecify hello yükleyicisi ihtiyacımız ve -(bizim modülün hello normalleştirilmiş sınıf adı olmalıdır) için giriş noktası her modül hello. Merhaba `simulated_device` hello Azure IOT kenar çekirdek çalışma zamanı paketinde bulunan bir yerel modül modülüdür. Dahil `args` JSON dosyası, olsa bile hello içinde `null`.

```json
"modules": [
  {
    "name": "simulated_device",
    "loader": {
      "name": "native",
      "entrypoint": {
        "module.path": "simulated_device"
      }
    },
    "args": {
      "macAddress": "01:02:03:03:02:01",
      "messagePeriod": 500
    }
  },
  {
    "name": "converter",
    "loader": {
      "name": "node",
      "entrypoint": {
        "main.path": "modules/converter.js"
      }
    },
    "args": null
  },
  {
    "name": "printer",
    "loader": {
      "name": "node",
      "entrypoint": {
        "main.path": "modules/printer.js"
      }
    },
    "args": null
  }
]
```

Merhaba yapılandırma Hello sonunda hello bağlantı kurar. Her bağlantı ile ifade edilen `source` ve `sink`. Önceden tanımlanmış bir modül her ikisi de başvurmalısınız. Merhaba çıkış iletisini `source` modülü toohello girişi iletilen `sink` modülü.

```json
"links": [
  {
    "source": "simulated_device",
    "sink": "converter"
  },
  {
    "source": "converter",
    "sink": "printer"
  }
]
```

## <a name="running-hello-modules"></a>Çalışan hello modülleri
1. `npm install`
2. `npm start`

Tooterminate Merhaba uygulaması istiyorsanız basın `<Enter>` anahtarı.

> [!IMPORTANT]
> Toouse Ctrl + C tooterminate hello IOT kenar önerilmez uygulama. Bu şekilde hello işlem tooterminate aşırı neden olabilecek şekilde.
