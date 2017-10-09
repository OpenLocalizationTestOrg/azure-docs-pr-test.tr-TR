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
# <a name="create-an-azure-iot-edge-module-with-nodejs"></a><span data-ttu-id="0009d-103">Node.js ile Azure IOT kenar modülü oluşturun</span><span class="sxs-lookup"><span data-stu-id="0009d-103">Create an Azure IoT Edge Module with Node.js</span></span>

<span data-ttu-id="0009d-104">Bu öğretici paylaşan nasıl toocreate için Azure IOT Edge'de JS modül.</span><span class="sxs-lookup"><span data-stu-id="0009d-104">This tutorial showcases how toocreate a module for Azure IoT Edge in JS.</span></span>

<span data-ttu-id="0009d-105">Bu öğreticide, biz ortamı kurulumu aracılığıyla yol ve nasıl toowrite bir [bırak](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) veri dönüştürücü modülü hello en son Azure IOT kenar NPM paketleri kullanma.</span><span class="sxs-lookup"><span data-stu-id="0009d-105">In this tutorial, we walk through environment setup and how toowrite a [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) data converter module using hello latest Azure IoT Edge NPM packages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0009d-106">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="0009d-106">Prerequisites</span></span>

<span data-ttu-id="0009d-107">Bu bölümde IOT kenar modülü geliştirme ortamınızı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="0009d-107">In this section, you set up your environment for IoT Edge module development.</span></span> <span data-ttu-id="0009d-108">Tooboth geçerlidir *64-bit Windows* ve *64-bit Linux (Ubuntu 14 +)* işletim sistemleri.</span><span class="sxs-lookup"><span data-stu-id="0009d-108">It applies tooboth *64-bit Windows* and *64-bit Linux (Ubuntu 14+)* operating systems.</span></span>

<span data-ttu-id="0009d-109">yazılımı aşağıdaki hello gereklidir:</span><span class="sxs-lookup"><span data-stu-id="0009d-109">hello following software is required:</span></span>
* <span data-ttu-id="0009d-110">[Git istemci](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="0009d-110">[Git Client](https://git-scm.com/downloads).</span></span>
* <span data-ttu-id="0009d-111">[Düğüm LTS](https://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="0009d-111">[Node LTS](https://nodejs.org).</span></span>
* <span data-ttu-id="0009d-112">`npm install -g yo`.</span><span class="sxs-lookup"><span data-stu-id="0009d-112">`npm install -g yo`.</span></span>
* `npm install -g generator-az-iot-gw-module`

## <a name="architecture"></a><span data-ttu-id="0009d-113">Mimari</span><span class="sxs-lookup"><span data-stu-id="0009d-113">Architecture</span></span>

<span data-ttu-id="0009d-114">Hello Azure IOT kenar platform yoğun hello uyarlar [Von Neumann mimarisi](https://en.wikipedia.org/wiki/Von_Neumann_architecture).</span><span class="sxs-lookup"><span data-stu-id="0009d-114">hello Azure IoT Edge platform heavily adopts hello [Von Neumann architecture](https://en.wikipedia.org/wiki/Von_Neumann_architecture).</span></span> <span data-ttu-id="0009d-115">O hello tüm Azure IOT kenar mimari başka bir deyişle, giriş işler ve bir çıktı üretir bir sistemdir; ve tek tek her modül küçük bir giriş-çıkış alt olduğunu.</span><span class="sxs-lookup"><span data-stu-id="0009d-115">Which means that hello entire Azure IoT Edge architecture is a system that processes input and produces output; and that each individual module is also a tiny input-output subsystem.</span></span> <span data-ttu-id="0009d-116">Bu öğreticide, iki modülleri aşağıdaki hello tanıtmaktadır:</span><span class="sxs-lookup"><span data-stu-id="0009d-116">In this tutorial, we introduce hello following two modules:</span></span>

1. <span data-ttu-id="0009d-117">Sanal alan modül [bırak](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) sinyal ve biçimlendirilmiş dönüştürür [JSON](https://en.wikipedia.org/wiki/JSON) ileti.</span><span class="sxs-lookup"><span data-stu-id="0009d-117">A module that receives a simulated [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) signal and converts it into a formatted [JSON](https://en.wikipedia.org/wiki/JSON) message.</span></span>
2. <span data-ttu-id="0009d-118">Alınan hello yazdırır bir modül [JSON](https://en.wikipedia.org/wiki/JSON) ileti.</span><span class="sxs-lookup"><span data-stu-id="0009d-118">A module that prints hello received [JSON](https://en.wikipedia.org/wiki/JSON) message.</span></span>

<span data-ttu-id="0009d-119">Merhaba aşağıdaki resimde bu proje için hello tipik son tooend veri akışı görüntüler:</span><span class="sxs-lookup"><span data-stu-id="0009d-119">hello following image displays hello typical end tooend dataflow for this project:</span></span>

<span data-ttu-id="0009d-120">![Veri akışı üç modülleri arasında](media/iot-hub-iot-edge-create-module/dataflow.png "giriş: benzetimli bırak Modülü; İşlemci: Dönüştürücü Modülü; Çıktı: Yazıcı Modülü")</span><span class="sxs-lookup"><span data-stu-id="0009d-120">![Dataflow between three modules](media/iot-hub-iot-edge-create-module/dataflow.png "Input: Simulated BLE Module; Processor: Converter Module; Output: Printer Module")</span></span>

## <a name="set-up-hello-environment"></a><span data-ttu-id="0009d-121">Merhaba ortamını ayarlama</span><span class="sxs-lookup"><span data-stu-id="0009d-121">Set up hello environment</span></span>
<span data-ttu-id="0009d-122">Aşağıda tooquickly ortam toostart toowrite JS ilk, bırak dönüştürücü modülüyle nasıl ayarlanacağını gösteriyoruz.</span><span class="sxs-lookup"><span data-stu-id="0009d-122">Below we show you how tooquickly set up environment toostart toowrite your first BLE converter module with JS.</span></span>

### <a name="create-module-project"></a><span data-ttu-id="0009d-123">Modül projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="0009d-123">Create module project</span></span>
1. <span data-ttu-id="0009d-124">Bir komut satırı penceresi açın, çalıştırmak `yo az-iot-gw-module`.</span><span class="sxs-lookup"><span data-stu-id="0009d-124">Open a command-line window, run `yo az-iot-gw-module`.</span></span>
2. <span data-ttu-id="0009d-125">Merhaba ekranında toofinish hello başlatma modül projenizin Hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="0009d-125">Follow hello steps on hello screen toofinish hello initialization of your module project.</span></span>

### <a name="project-structure"></a><span data-ttu-id="0009d-126">Proje yapısı</span><span class="sxs-lookup"><span data-stu-id="0009d-126">Project structure</span></span>
<span data-ttu-id="0009d-127">JS modül proje bileşenleri aşağıdaki Merhaba oluşur:</span><span class="sxs-lookup"><span data-stu-id="0009d-127">A JS module project consists of hello following components:</span></span>

<span data-ttu-id="0009d-128">`modules`-hello özelleştirilmiş JS modül kaynak dosyaları.</span><span class="sxs-lookup"><span data-stu-id="0009d-128">`modules` - hello customized JS module source files.</span></span> <span data-ttu-id="0009d-129">Merhaba varsayılan Değiştir `sensor.js` ve `printer.js` kendi modülü dosyalarla.</span><span class="sxs-lookup"><span data-stu-id="0009d-129">Replace hello default `sensor.js` and `printer.js` with your own module files.</span></span>

<span data-ttu-id="0009d-130">`app.js`-hello giriş dosyası toostart hello kenar örneği.</span><span class="sxs-lookup"><span data-stu-id="0009d-130">`app.js` - hello entry file toostart hello Edge instance.</span></span>

<span data-ttu-id="0009d-131">`gw.config.json`-hello yapılandırma dosyası toocustomize hello modülleri toobe kenarından yüklendi.</span><span class="sxs-lookup"><span data-stu-id="0009d-131">`gw.config.json` - hello configuration file toocustomize hello modules toobe loaded by Edge.</span></span>

<span data-ttu-id="0009d-132">`package.json`-hello modülü projesi için meta veri bilgileri.</span><span class="sxs-lookup"><span data-stu-id="0009d-132">`package.json` - hello metadata information for module project.</span></span>

<span data-ttu-id="0009d-133">`README.md`-hello modülü projesi için temel belgelere.</span><span class="sxs-lookup"><span data-stu-id="0009d-133">`README.md` - hello basic documentation for module project.</span></span>


### <a name="package-file"></a><span data-ttu-id="0009d-134">Paket dosyası</span><span class="sxs-lookup"><span data-stu-id="0009d-134">Package file</span></span>

<span data-ttu-id="0009d-135">Bu `package.json` hello adı, sürüm, giriş, komut dosyaları, çalışma zamanı ve geliştirme bağımlılıklar içeren bir modülü projesi gerekli tüm hello meta veri bilgileri bildirir.</span><span class="sxs-lookup"><span data-stu-id="0009d-135">This `package.json` declares all hello metadata information needed by a module project that includes hello name, version, entry, scripts, runtime, and development dependencies.</span></span>

<span data-ttu-id="0009d-136">Kod parçacığını gösterir nasıl tooconfigure bırak dönüştürücü için örnek proje.</span><span class="sxs-lookup"><span data-stu-id="0009d-136">Following code snippet shows how tooconfigure for BLE converter sample project.</span></span>
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


### <a name="entry-file"></a><span data-ttu-id="0009d-137">Girdi dosyası</span><span class="sxs-lookup"><span data-stu-id="0009d-137">Entry file</span></span>
<span data-ttu-id="0009d-138">Merhaba `app.js` hello yolu tooinitialize hello kenar örnek tanımlar.</span><span class="sxs-lookup"><span data-stu-id="0009d-138">hello `app.js` defines hello way tooinitialize hello edge instance.</span></span> <span data-ttu-id="0009d-139">Burada herhangi bir değişiklik toomake gerekmez.</span><span class="sxs-lookup"><span data-stu-id="0009d-139">Here we don't need toomake any change.</span></span>

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

### <a name="interface-of-module"></a><span data-ttu-id="0009d-140">Modülün arabirimi</span><span class="sxs-lookup"><span data-stu-id="0009d-140">Interface of module</span></span>
<span data-ttu-id="0009d-141">Bir veri işleri için işlemci olarak Azure IOT kenar modülü davranabilirsiniz: girişi almak, işlemesi ve çıktı üretir.</span><span class="sxs-lookup"><span data-stu-id="0009d-141">You can treat an Azure IoT Edge module as a data processor whose job is to: receive input, process it, and produce output.</span></span>

<span data-ttu-id="0009d-142">Merhaba giriş donanım (gibi hareket algılayıcısı) verileri, bir ileti diğer modüller ya da (örneğin, düzenli aralıklarla bir Zamanlayıcı tarafından oluşturulan bir rastgele sayı) başka bir şey olabilir.</span><span class="sxs-lookup"><span data-stu-id="0009d-142">hello input might be data from hardware (like a motion detector), a message from other modules, or anything else (like a random number generated periodically by a timer).</span></span>

<span data-ttu-id="0009d-143">Merhaba çıkış benzer toohello giriş, donanım davranış (gibi hello ışığı yanıp sönen), bir ileti tooother modülleri ya da (yazdırma toohello konsolu gibi) başka bir şey tetikleyebilir.</span><span class="sxs-lookup"><span data-stu-id="0009d-143">hello output is similar toohello input, it could trigger hardware behavior (like hello blinking LED), a message tooother modules, or anything else (like printing toohello console).</span></span>

<span data-ttu-id="0009d-144">Modüller birbirleri ile kullanarak iletişim `message` nesnesi.</span><span class="sxs-lookup"><span data-stu-id="0009d-144">Modules communicate with each other using `message` object.</span></span> <span data-ttu-id="0009d-145">Merhaba **içerik** , bir `message` istediğiniz verilerin herhangi bir tür temsil etme özelliğine sahip bir bayt dizisi.</span><span class="sxs-lookup"><span data-stu-id="0009d-145">hello **content** of a `message` is a byte array that is capable of representing any kind of data you like.</span></span> <span data-ttu-id="0009d-146">**Özellikler** de hello kullanılabilir `message` ve yalnızca bir dize-dize eşleme.</span><span class="sxs-lookup"><span data-stu-id="0009d-146">**Properties** are also available in hello `message` and are simply a string-to-string mapping.</span></span> <span data-ttu-id="0009d-147">Düşünebilirsiniz **özellikleri** bir HTTP isteğinin ya da hello meta veri dosyasının hello başlığı olarak.</span><span class="sxs-lookup"><span data-stu-id="0009d-147">You may think of **properties** as hello headers in an HTTP request, or hello metadata of a file.</span></span>

<span data-ttu-id="0009d-148">Sipariş toodevelop JS Azure IOT kenar modülünde'da, toocreate gerekli hello yöntemlerini uygulayan yeni bir modül nesne gereksinim `receive()`.</span><span class="sxs-lookup"><span data-stu-id="0009d-148">In order toodevelop an Azure IoT Edge module in JS, you need toocreate a new module object that implements hello required methods `receive()`.</span></span> <span data-ttu-id="0009d-149">Bu noktada, ayrıca isteğe bağlı tooimplement hello tercih edebilirsiniz `create()` veya `start()`, veya `destroy()` de yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="0009d-149">At this point, you may also choose tooimplement hello optional `create()` or `start()`, or `destroy()` methods as well.</span></span> <span data-ttu-id="0009d-150">Aşağıdaki kod parçacığını hello JS modül nesnesinin iskele hello gösterir.</span><span class="sxs-lookup"><span data-stu-id="0009d-150">hello following code snippet shows you hello scaffolding of JS module object.</span></span>

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

### <a name="converter-module"></a><span data-ttu-id="0009d-151">Dönüştürücü Modülü</span><span class="sxs-lookup"><span data-stu-id="0009d-151">Converter module</span></span>
| <span data-ttu-id="0009d-152">Girdi</span><span class="sxs-lookup"><span data-stu-id="0009d-152">Input</span></span>                    | <span data-ttu-id="0009d-153">İşlemci</span><span class="sxs-lookup"><span data-stu-id="0009d-153">Processor</span></span>                              | <span data-ttu-id="0009d-154">Çıktı</span><span class="sxs-lookup"><span data-stu-id="0009d-154">Output</span></span>                 | <span data-ttu-id="0009d-155">Kaynak dosya</span><span class="sxs-lookup"><span data-stu-id="0009d-155">Source File</span></span>            |
| ------------------------ | -------------------------------------- | ---------------------- | ---------------------- |
| <span data-ttu-id="0009d-156">Sıcaklık veri iletisi</span><span class="sxs-lookup"><span data-stu-id="0009d-156">Temperature data message</span></span> | <span data-ttu-id="0009d-157">Ayrıştırma ve yeni bir JSON ileti oluşturun</span><span class="sxs-lookup"><span data-stu-id="0009d-157">Parse and construct a new JSON message</span></span> | <span data-ttu-id="0009d-158">Yapı JSON iletisi</span><span class="sxs-lookup"><span data-stu-id="0009d-158">Structure JSON message</span></span> | `converter.js` |

<span data-ttu-id="0009d-159">Bu modül tipik bir Azure IOT kenar modüldür.</span><span class="sxs-lookup"><span data-stu-id="0009d-159">This module is a typical Azure IoT Edge module.</span></span> <span data-ttu-id="0009d-160">Diğer modüllerden sıcaklık iletileri kabul eder (bir donanım modülü veya bu bizim benzetimli bırak modülü durumda); ve (Merhaba ileti kimliği, tootrigger hello sıcaklık uyarı ihtiyacımız hello özelliğini ayarlama ekleme de dahil olmak üzere vb.) yapılandırılmış tooa JSON iletinin hello sıcaklık iletiyi normalleştirir.</span><span class="sxs-lookup"><span data-stu-id="0009d-160">It accepts temperature messages from other modules (a hardware module, or in this case our simulated BLE module); and then normalizes hello temperature message in tooa structured JSON message (including appending hello message ID, setting hello property of whether we need tootrigger hello temperature alert, and so on).</span></span>

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

### <a name="printer-module"></a><span data-ttu-id="0009d-161">Yazıcı Modülü</span><span class="sxs-lookup"><span data-stu-id="0009d-161">Printer module</span></span>
| <span data-ttu-id="0009d-162">Girdi</span><span class="sxs-lookup"><span data-stu-id="0009d-162">Input</span></span>                          | <span data-ttu-id="0009d-163">İşlemci</span><span class="sxs-lookup"><span data-stu-id="0009d-163">Processor</span></span> | <span data-ttu-id="0009d-164">Çıktı</span><span class="sxs-lookup"><span data-stu-id="0009d-164">Output</span></span>                     | <span data-ttu-id="0009d-165">Kaynak dosya</span><span class="sxs-lookup"><span data-stu-id="0009d-165">Source File</span></span>          |
| ------------------------------ | --------- | -------------------------- | -------------------- |
| <span data-ttu-id="0009d-166">Diğer modüllerden herhangi bir iletisi</span><span class="sxs-lookup"><span data-stu-id="0009d-166">Any message from other modules</span></span> | <span data-ttu-id="0009d-167">Yok</span><span class="sxs-lookup"><span data-stu-id="0009d-167">N/A</span></span>       | <span data-ttu-id="0009d-168">Merhaba ileti tooconsole oturum</span><span class="sxs-lookup"><span data-stu-id="0009d-168">Log hello message tooconsole</span></span> | `printer.js` |

<span data-ttu-id="0009d-169">Bu modül basit ve açıklayıcı, hangi hello alınan iletileri (özelliği, içerik) toohello terminal penceresi çıkarır.</span><span class="sxs-lookup"><span data-stu-id="0009d-169">This module is simple, self-explanatory, which outputs hello received messages(property, content) toohello terminal window.</span></span>

```javascript
receive: function (message) {
  let properties = JSON.stringify(message.properties);
  let content = Buffer.from(message.content).toString('utf8');

  console.log(`printer.receive.properties - ${properties}`);
  console.log(`printer.receive.content - ${content}\n`);
}
```

### <a name="configuration"></a><span data-ttu-id="0009d-170">Yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0009d-170">Configuration</span></span>
<span data-ttu-id="0009d-171">Merhaba modülleri çalıştırmadan önce hello son tooconfigure hello Azure IOT kenarı ve modülleri arasında tooestablish hello bağlantıları adımdır.</span><span class="sxs-lookup"><span data-stu-id="0009d-171">hello final step before running hello modules is tooconfigure hello Azure IoT Edge and tooestablish hello connections between modules.</span></span>

<span data-ttu-id="0009d-172">Toodeclare ilk ihtiyacımız bizim `node` (itibaren Azure IOT kenar destekler yükleyicilerini farklı dillerde) tarafından başvurulan yükleyicisi kendi `name` hello bölümlerde daha sonra.</span><span class="sxs-lookup"><span data-stu-id="0009d-172">First we need toodeclare our `node` loader (since Azure IoT Edge supports loaders of different languages) which could be referenced by its `name` in hello sections afterward.</span></span>

```json
"loaders": [
  {
    "type": "node",
    "name": "node"
  }
]
```

<span data-ttu-id="0009d-173">Ayrıca, biz bizim yükleyicilerini bildirdikten sonra toodeclare bizim modüller de gerekir.</span><span class="sxs-lookup"><span data-stu-id="0009d-173">Once we have declared our loaders, we also need toodeclare our modules as well.</span></span> <span data-ttu-id="0009d-174">Benzer toodeclaring hello yükleyicileri, bunlar ayrıca başvurulabilir tarafından kendi `name` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="0009d-174">Similar toodeclaring hello loaders, they can also be referenced by their `name` attribute.</span></span> <span data-ttu-id="0009d-175">Bir modül bildirirken (hangi önce tanımladığımız hello biri olmalıdır) kullanması gereken toospecify hello yükleyicisi ihtiyacımız ve -(bizim modülün hello normalleştirilmiş sınıf adı olmalıdır) için giriş noktası her modül hello.</span><span class="sxs-lookup"><span data-stu-id="0009d-175">When declaring a module, we need toospecify hello loader it should use (which should be hello one we defined before) and hello entry-point (should be hello normalized class name of our module) for each module.</span></span> <span data-ttu-id="0009d-176">Merhaba `simulated_device` hello Azure IOT kenar çekirdek çalışma zamanı paketinde bulunan bir yerel modül modülüdür.</span><span class="sxs-lookup"><span data-stu-id="0009d-176">hello `simulated_device` module is a native module that is included in hello Azure IoT Edge core runtime package.</span></span> <span data-ttu-id="0009d-177">Dahil `args` JSON dosyası, olsa bile hello içinde `null`.</span><span class="sxs-lookup"><span data-stu-id="0009d-177">Include `args` in hello JSON file even if it is `null`.</span></span>

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

<span data-ttu-id="0009d-178">Merhaba yapılandırma Hello sonunda hello bağlantı kurar.</span><span class="sxs-lookup"><span data-stu-id="0009d-178">At hello end of hello configuration, we establish hello connections.</span></span> <span data-ttu-id="0009d-179">Her bağlantı ile ifade edilen `source` ve `sink`.</span><span class="sxs-lookup"><span data-stu-id="0009d-179">Each connection is expressed by `source` and `sink`.</span></span> <span data-ttu-id="0009d-180">Önceden tanımlanmış bir modül her ikisi de başvurmalısınız.</span><span class="sxs-lookup"><span data-stu-id="0009d-180">They should both reference a pre-defined module.</span></span> <span data-ttu-id="0009d-181">Merhaba çıkış iletisini `source` modülü toohello girişi iletilen `sink` modülü.</span><span class="sxs-lookup"><span data-stu-id="0009d-181">hello output message of `source` module is forwarded toohello input of `sink` module.</span></span>

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

## <a name="running-hello-modules"></a><span data-ttu-id="0009d-182">Çalışan hello modülleri</span><span class="sxs-lookup"><span data-stu-id="0009d-182">Running hello modules</span></span>
1. `npm install`
2. `npm start`

<span data-ttu-id="0009d-183">Tooterminate Merhaba uygulaması istiyorsanız basın `<Enter>` anahtarı.</span><span class="sxs-lookup"><span data-stu-id="0009d-183">If you want tooterminate hello application, press `<Enter>` key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0009d-184">Toouse Ctrl + C tooterminate hello IOT kenar önerilmez uygulama.</span><span class="sxs-lookup"><span data-stu-id="0009d-184">It is not recommended toouse Ctrl + C tooterminate hello IoT Edge application.</span></span> <span data-ttu-id="0009d-185">Bu şekilde hello işlem tooterminate aşırı neden olabilecek şekilde.</span><span class="sxs-lookup"><span data-stu-id="0009d-185">As this way may cause hello process tooterminate abnormally.</span></span>
