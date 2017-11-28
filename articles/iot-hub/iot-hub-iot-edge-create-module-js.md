---
title: "Node.js ile Azure IOT kenar modülü oluşturma | Microsoft Docs"
description: "Bu öğreticide en son Azure IOT kenar NPM paket ve Yeoman kullanarak bir bırak veri dönüştürücü modülü yazma paylaşan Oluşturucu."
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
ms.openlocfilehash: ba466f47e157d805600c41fa3d84ed5a0363969c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-azure-iot-edge-module-with-nodejs"></a><span data-ttu-id="69286-103">Node.js ile Azure IOT kenar modülü oluşturun</span><span class="sxs-lookup"><span data-stu-id="69286-103">Create an Azure IoT Edge Module with Node.js</span></span>

<span data-ttu-id="69286-104">Bu öğretici Azure IOT Edge'de JS için bir modül oluşturma gösterir.</span><span class="sxs-lookup"><span data-stu-id="69286-104">This tutorial showcases how to create a module for Azure IoT Edge in JS.</span></span>

<span data-ttu-id="69286-105">Ortam kurulumu ve nasıl yazılacağını Bu öğreticide, biz yol bir [bırak](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) veri dönüştürücü modülü en son Azure IOT kenar NPM paketleri kullanma.</span><span class="sxs-lookup"><span data-stu-id="69286-105">In this tutorial, we walk through environment setup and how to write a [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) data converter module using the latest Azure IoT Edge NPM packages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="69286-106">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="69286-106">Prerequisites</span></span>

<span data-ttu-id="69286-107">Bu bölümde IOT kenar modülü geliştirme ortamınızı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="69286-107">In this section, you set up your environment for IoT Edge module development.</span></span> <span data-ttu-id="69286-108">Her ikisi de geçerli *64-bit Windows* ve *64-bit Linux (Ubuntu 14 +)* işletim sistemleri.</span><span class="sxs-lookup"><span data-stu-id="69286-108">It applies to both *64-bit Windows* and *64-bit Linux (Ubuntu 14+)* operating systems.</span></span>

<span data-ttu-id="69286-109">Aşağıdaki yazılımlar gereklidir:</span><span class="sxs-lookup"><span data-stu-id="69286-109">The following software is required:</span></span>
* <span data-ttu-id="69286-110">[Git istemci](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="69286-110">[Git Client](https://git-scm.com/downloads).</span></span>
* <span data-ttu-id="69286-111">[Düğüm LTS](https://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="69286-111">[Node LTS](https://nodejs.org).</span></span>
* <span data-ttu-id="69286-112">`npm install -g yo`.</span><span class="sxs-lookup"><span data-stu-id="69286-112">`npm install -g yo`.</span></span>
* `npm install -g generator-az-iot-gw-module`

## <a name="architecture"></a><span data-ttu-id="69286-113">Mimari</span><span class="sxs-lookup"><span data-stu-id="69286-113">Architecture</span></span>

<span data-ttu-id="69286-114">Azure IOT kenar platform yoğun uyarlar [Von Neumann mimarisi](https://en.wikipedia.org/wiki/Von_Neumann_architecture).</span><span class="sxs-lookup"><span data-stu-id="69286-114">The Azure IoT Edge platform heavily adopts the [Von Neumann architecture](https://en.wikipedia.org/wiki/Von_Neumann_architecture).</span></span> <span data-ttu-id="69286-115">Hangi tüm Azure IOT kenar mimarisi girişi işler ve bir çıktı üretir sistem anlamına gelir; ve tek tek her modül küçük bir giriş-çıkış alt olduğunu.</span><span class="sxs-lookup"><span data-stu-id="69286-115">Which means that the entire Azure IoT Edge architecture is a system that processes input and produces output; and that each individual module is also a tiny input-output subsystem.</span></span> <span data-ttu-id="69286-116">Bu öğreticide, aşağıdaki iki modüller tanıtmaktadır:</span><span class="sxs-lookup"><span data-stu-id="69286-116">In this tutorial, we introduce the following two modules:</span></span>

1. <span data-ttu-id="69286-117">Sanal alan modül [bırak](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) sinyal ve biçimlendirilmiş dönüştürür [JSON](https://en.wikipedia.org/wiki/JSON) ileti.</span><span class="sxs-lookup"><span data-stu-id="69286-117">A module that receives a simulated [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) signal and converts it into a formatted [JSON](https://en.wikipedia.org/wiki/JSON) message.</span></span>
2. <span data-ttu-id="69286-118">Alınan yazdırır bir modül [JSON](https://en.wikipedia.org/wiki/JSON) ileti.</span><span class="sxs-lookup"><span data-stu-id="69286-118">A module that prints the received [JSON](https://en.wikipedia.org/wiki/JSON) message.</span></span>

<span data-ttu-id="69286-119">Aşağıdaki resimde bu proje için tipik uçtan uca veri akışı görüntüler:</span><span class="sxs-lookup"><span data-stu-id="69286-119">The following image displays the typical end to end dataflow for this project:</span></span>

<span data-ttu-id="69286-120">![Veri akışı üç modülleri arasında](media/iot-hub-iot-edge-create-module/dataflow.png "giriş: benzetimli bırak Modülü; İşlemci: Dönüştürücü Modülü; Çıktı: Yazıcı Modülü")</span><span class="sxs-lookup"><span data-stu-id="69286-120">![Dataflow between three modules](media/iot-hub-iot-edge-create-module/dataflow.png "Input: Simulated BLE Module; Processor: Converter Module; Output: Printer Module")</span></span>

## <a name="set-up-the-environment"></a><span data-ttu-id="69286-121">Ortamını ayarlama</span><span class="sxs-lookup"><span data-stu-id="69286-121">Set up the environment</span></span>
<span data-ttu-id="69286-122">Aşağıda, ilk bırak dönüştürücü modülü JS ile yazmaya başlamak için ortamı hızlı bir şekilde ayarlamak nasıl gösteriyoruz.</span><span class="sxs-lookup"><span data-stu-id="69286-122">Below we show you how to quickly set up environment to start to write your first BLE converter module with JS.</span></span>

### <a name="create-module-project"></a><span data-ttu-id="69286-123">Modül projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="69286-123">Create module project</span></span>
1. <span data-ttu-id="69286-124">Bir komut satırı penceresi açın, çalıştırmak `yo az-iot-gw-module`.</span><span class="sxs-lookup"><span data-stu-id="69286-124">Open a command-line window, run `yo az-iot-gw-module`.</span></span>
2. <span data-ttu-id="69286-125">Modül projenizin başlatma tamamlamak için ekrandaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="69286-125">Follow the steps on the screen to finish the initialization of your module project.</span></span>

### <a name="project-structure"></a><span data-ttu-id="69286-126">Proje yapısı</span><span class="sxs-lookup"><span data-stu-id="69286-126">Project structure</span></span>
<span data-ttu-id="69286-127">JS modül proje aşağıdaki bileşenlerden oluşur:</span><span class="sxs-lookup"><span data-stu-id="69286-127">A JS module project consists of the following components:</span></span>

<span data-ttu-id="69286-128">`modules`-Özelleştirilmiş JS modül kaynak dosyaları.</span><span class="sxs-lookup"><span data-stu-id="69286-128">`modules` - The customized JS module source files.</span></span> <span data-ttu-id="69286-129">Varsayılan değiştirme `sensor.js` ve `printer.js` kendi modülü dosyalarla.</span><span class="sxs-lookup"><span data-stu-id="69286-129">Replace the default `sensor.js` and `printer.js` with your own module files.</span></span>

<span data-ttu-id="69286-130">`app.js`-Kenar örneği başlatmak için giriş dosyası.</span><span class="sxs-lookup"><span data-stu-id="69286-130">`app.js` - The entry file to start the Edge instance.</span></span>

<span data-ttu-id="69286-131">`gw.config.json`-Edge tarafından yüklenmesi için modülleri özelleştirmek için yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="69286-131">`gw.config.json` - The configuration file to customize the modules to be loaded by Edge.</span></span>

<span data-ttu-id="69286-132">`package.json`-Modülü projesi meta veri bilgilerini.</span><span class="sxs-lookup"><span data-stu-id="69286-132">`package.json` - The metadata information for module project.</span></span>

<span data-ttu-id="69286-133">`README.md`-Temel belgeleri modülü projesi.</span><span class="sxs-lookup"><span data-stu-id="69286-133">`README.md` - The basic documentation for module project.</span></span>


### <a name="package-file"></a><span data-ttu-id="69286-134">Paket dosyası</span><span class="sxs-lookup"><span data-stu-id="69286-134">Package file</span></span>

<span data-ttu-id="69286-135">Bu `package.json` adı, sürüm, giriş, komut dosyaları, çalışma zamanı ve geliştirme bağımlılıklar içeren bir modülü projesi tarafından gerekli olan tüm meta veri bilgileri bildirir.</span><span class="sxs-lookup"><span data-stu-id="69286-135">This `package.json` declares all the metadata information needed by a module project that includes the name, version, entry, scripts, runtime, and development dependencies.</span></span>

<span data-ttu-id="69286-136">Aşağıdaki kod parçacığını bırak dönüştürücü örnek projesi için yapılandırma gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="69286-136">Following code snippet shows how to configure for BLE converter sample project.</span></span>
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


### <a name="entry-file"></a><span data-ttu-id="69286-137">Girdi dosyası</span><span class="sxs-lookup"><span data-stu-id="69286-137">Entry file</span></span>
<span data-ttu-id="69286-138">`app.js` Kenar örneği başlatmak için biçimini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="69286-138">The `app.js` defines the way to initialize the edge instance.</span></span> <span data-ttu-id="69286-139">Burada size herhangi bir değişiklik yapmak gerekmez.</span><span class="sxs-lookup"><span data-stu-id="69286-139">Here we don't need to make any change.</span></span>

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

### <a name="interface-of-module"></a><span data-ttu-id="69286-140">Modülün arabirimi</span><span class="sxs-lookup"><span data-stu-id="69286-140">Interface of module</span></span>
<span data-ttu-id="69286-141">Bir veri işleri için işlemci olarak Azure IOT kenar modülü davranabilirsiniz: girişi almak, işlemesi ve çıktı üretir.</span><span class="sxs-lookup"><span data-stu-id="69286-141">You can treat an Azure IoT Edge module as a data processor whose job is to: receive input, process it, and produce output.</span></span>

<span data-ttu-id="69286-142">Giriş (gibi hareket algılayıcısı) donanım verilerden bir ileti diğer modüller ya da (örneğin, düzenli aralıklarla bir Zamanlayıcı tarafından oluşturulan bir rastgele sayı) başka bir şey olabilir.</span><span class="sxs-lookup"><span data-stu-id="69286-142">The input might be data from hardware (like a motion detector), a message from other modules, or anything else (like a random number generated periodically by a timer).</span></span>

<span data-ttu-id="69286-143">Giriş benzer bir çıkış, tetikleyebilir donanım davranış (gibi yanıp sönen LED), diğer modüller ya da (örneğin, yazdırma konsoluna) başka bir şey için bir ileti.</span><span class="sxs-lookup"><span data-stu-id="69286-143">The output is similar to the input, it could trigger hardware behavior (like the blinking LED), a message to other modules, or anything else (like printing to the console).</span></span>

<span data-ttu-id="69286-144">Modüller birbirleri ile kullanarak iletişim `message` nesnesi.</span><span class="sxs-lookup"><span data-stu-id="69286-144">Modules communicate with each other using `message` object.</span></span> <span data-ttu-id="69286-145">**İçerik** , bir `message` istediğiniz verilerin herhangi bir tür temsil etme özelliğine sahip bir bayt dizisi.</span><span class="sxs-lookup"><span data-stu-id="69286-145">The **content** of a `message` is a byte array that is capable of representing any kind of data you like.</span></span> <span data-ttu-id="69286-146">**Özellikler** mevcuttur `message` ve yalnızca bir dize-dize eşleme.</span><span class="sxs-lookup"><span data-stu-id="69286-146">**Properties** are also available in the `message` and are simply a string-to-string mapping.</span></span> <span data-ttu-id="69286-147">Düşünebilirsiniz **özellikleri** bir HTTP isteğinin ya da meta veri dosyasının başlığı olarak.</span><span class="sxs-lookup"><span data-stu-id="69286-147">You may think of **properties** as the headers in an HTTP request, or the metadata of a file.</span></span>

<span data-ttu-id="69286-148">JS Azure IOT kenar modülünde geliştirmek için gereken yöntemleri uygulayan yeni bir modül nesnesi oluşturmak ihtiyacınız `receive()`.</span><span class="sxs-lookup"><span data-stu-id="69286-148">In order to develop an Azure IoT Edge module in JS, you need to create a new module object that implements the required methods `receive()`.</span></span> <span data-ttu-id="69286-149">Bu noktada, ayrıca isteğe bağlı uygulamayı seçebilir `create()` veya `start()`, veya `destroy()` de yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="69286-149">At this point, you may also choose to implement the optional `create()` or `start()`, or `destroy()` methods as well.</span></span> <span data-ttu-id="69286-150">Aşağıdaki kod parçacığını JS modül nesne iskelesini gösterir.</span><span class="sxs-lookup"><span data-stu-id="69286-150">The following code snippet shows you the scaffolding of JS module object.</span></span>

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

### <a name="converter-module"></a><span data-ttu-id="69286-151">Dönüştürücü Modülü</span><span class="sxs-lookup"><span data-stu-id="69286-151">Converter module</span></span>
| <span data-ttu-id="69286-152">Girdi</span><span class="sxs-lookup"><span data-stu-id="69286-152">Input</span></span>                    | <span data-ttu-id="69286-153">İşlemci</span><span class="sxs-lookup"><span data-stu-id="69286-153">Processor</span></span>                              | <span data-ttu-id="69286-154">Çıktı</span><span class="sxs-lookup"><span data-stu-id="69286-154">Output</span></span>                 | <span data-ttu-id="69286-155">Kaynak dosya</span><span class="sxs-lookup"><span data-stu-id="69286-155">Source File</span></span>            |
| ------------------------ | -------------------------------------- | ---------------------- | ---------------------- |
| <span data-ttu-id="69286-156">Sıcaklık veri iletisi</span><span class="sxs-lookup"><span data-stu-id="69286-156">Temperature data message</span></span> | <span data-ttu-id="69286-157">Ayrıştırma ve yeni bir JSON ileti oluşturun</span><span class="sxs-lookup"><span data-stu-id="69286-157">Parse and construct a new JSON message</span></span> | <span data-ttu-id="69286-158">Yapı JSON iletisi</span><span class="sxs-lookup"><span data-stu-id="69286-158">Structure JSON message</span></span> | `converter.js` |

<span data-ttu-id="69286-159">Bu modül tipik bir Azure IOT kenar modüldür.</span><span class="sxs-lookup"><span data-stu-id="69286-159">This module is a typical Azure IoT Edge module.</span></span> <span data-ttu-id="69286-160">Diğer modüllerden sıcaklık iletileri kabul eder (bir donanım modülü veya bu bizim benzetimli bırak modülü durumda); ve (sıcaklık uyarı tetiklemesi ve benzeri için ihtiyacımız özelliğini ayarlama ileti kimliği ekleme dahil) yapılandırılmış bir JSON iletisi sıcaklık iletisinde normalleştirir.</span><span class="sxs-lookup"><span data-stu-id="69286-160">It accepts temperature messages from other modules (a hardware module, or in this case our simulated BLE module); and then normalizes the temperature message in to a structured JSON message (including appending the message ID, setting the property of whether we need to trigger the temperature alert, and so on).</span></span>

```javascript
receive: function (message) {
  // Initialize the messageCount in global object at first time.
  if (!global.messageCount) {
    global.messageCount = 0;
  }

  // Read the content and properties objects from message.
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

  // Publish the new message to broker.
  this.broker.publish(
    {
      properties: newProperties,
      content: new Uint8Array(Buffer.from(JSON.stringify(newContent), 'utf8'))
    }
  );
},
```

### <a name="printer-module"></a><span data-ttu-id="69286-161">Yazıcı Modülü</span><span class="sxs-lookup"><span data-stu-id="69286-161">Printer module</span></span>
| <span data-ttu-id="69286-162">Girdi</span><span class="sxs-lookup"><span data-stu-id="69286-162">Input</span></span>                          | <span data-ttu-id="69286-163">İşlemci</span><span class="sxs-lookup"><span data-stu-id="69286-163">Processor</span></span> | <span data-ttu-id="69286-164">Çıktı</span><span class="sxs-lookup"><span data-stu-id="69286-164">Output</span></span>                     | <span data-ttu-id="69286-165">Kaynak dosya</span><span class="sxs-lookup"><span data-stu-id="69286-165">Source File</span></span>          |
| ------------------------------ | --------- | -------------------------- | -------------------- |
| <span data-ttu-id="69286-166">Diğer modüllerden herhangi bir iletisi</span><span class="sxs-lookup"><span data-stu-id="69286-166">Any message from other modules</span></span> | <span data-ttu-id="69286-167">Yok</span><span class="sxs-lookup"><span data-stu-id="69286-167">N/A</span></span>       | <span data-ttu-id="69286-168">İleti konsola oturum</span><span class="sxs-lookup"><span data-stu-id="69286-168">Log the message to console</span></span> | `printer.js` |

<span data-ttu-id="69286-169">Bu modül basit ve açıklayıcı, hangi alınan iletiler (özelliği, içerik) terminal penceresine çıkarır.</span><span class="sxs-lookup"><span data-stu-id="69286-169">This module is simple, self-explanatory, which outputs the received messages(property, content) to the terminal window.</span></span>

```javascript
receive: function (message) {
  let properties = JSON.stringify(message.properties);
  let content = Buffer.from(message.content).toString('utf8');

  console.log(`printer.receive.properties - ${properties}`);
  console.log(`printer.receive.content - ${content}\n`);
}
```

### <a name="configuration"></a><span data-ttu-id="69286-170">Yapılandırma</span><span class="sxs-lookup"><span data-stu-id="69286-170">Configuration</span></span>
<span data-ttu-id="69286-171">Modülleri çalıştırmadan önce son adım, Azure IOT kenar yapılandırmak ve modülleri arasında bağlantı kurmak için ' dir.</span><span class="sxs-lookup"><span data-stu-id="69286-171">The final step before running the modules is to configure the Azure IoT Edge and to establish the connections between modules.</span></span>

<span data-ttu-id="69286-172">İlk bildirmek ihtiyacımız bizim `node` (itibaren Azure IOT kenar destekler yükleyicilerini farklı dillerde) tarafından başvurulan yükleyicisi kendi `name` bölümlerde daha sonra.</span><span class="sxs-lookup"><span data-stu-id="69286-172">First we need to declare our `node` loader (since Azure IoT Edge supports loaders of different languages) which could be referenced by its `name` in the sections afterward.</span></span>

```json
"loaders": [
  {
    "type": "node",
    "name": "node"
  }
]
```

<span data-ttu-id="69286-173">Biz bizim yükleyicilerini bildirdikten sonra biz de bizim modüller de bildirmek gerekir.</span><span class="sxs-lookup"><span data-stu-id="69286-173">Once we have declared our loaders, we also need to declare our modules as well.</span></span> <span data-ttu-id="69286-174">Benzer yükleyicileri bildirmek için bunlar ayrıca tarafından başvurulabilir kendi `name` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="69286-174">Similar to declaring the loaders, they can also be referenced by their `name` attribute.</span></span> <span data-ttu-id="69286-175">Bir modül bildirirken (hangi önce tanımladığımız biri olmalıdır) kullanması gereken yükleyicisi belirtmek ihtiyacımız ve-(bizim modül normalleştirilmiş sınıf adı olmalıdır) için giriş noktası her modül.</span><span class="sxs-lookup"><span data-stu-id="69286-175">When declaring a module, we need to specify the loader it should use (which should be the one we defined before) and the entry-point (should be the normalized class name of our module) for each module.</span></span> <span data-ttu-id="69286-176">`simulated_device` Azure IOT kenar çekirdek çalışma zamanı paketinde bulunan bir yerel modül modülüdür.</span><span class="sxs-lookup"><span data-stu-id="69286-176">The `simulated_device` module is a native module that is included in the Azure IoT Edge core runtime package.</span></span> <span data-ttu-id="69286-177">Dahil `args` JSON'dosyası, olsa bile `null`.</span><span class="sxs-lookup"><span data-stu-id="69286-177">Include `args` in the JSON file even if it is `null`.</span></span>

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

<span data-ttu-id="69286-178">Yapılandırma sonunda bağlantı kurun.</span><span class="sxs-lookup"><span data-stu-id="69286-178">At the end of the configuration, we establish the connections.</span></span> <span data-ttu-id="69286-179">Her bağlantı ile ifade edilen `source` ve `sink`.</span><span class="sxs-lookup"><span data-stu-id="69286-179">Each connection is expressed by `source` and `sink`.</span></span> <span data-ttu-id="69286-180">Önceden tanımlanmış bir modül her ikisi de başvurmalısınız.</span><span class="sxs-lookup"><span data-stu-id="69286-180">They should both reference a pre-defined module.</span></span> <span data-ttu-id="69286-181">Çıktı ileti `source` modülü girişi için iletilen `sink` modülü.</span><span class="sxs-lookup"><span data-stu-id="69286-181">The output message of `source` module is forwarded to the input of `sink` module.</span></span>

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

## <a name="running-the-modules"></a><span data-ttu-id="69286-182">Modülleri çalıştırma</span><span class="sxs-lookup"><span data-stu-id="69286-182">Running the modules</span></span>
1. `npm install`
2. `npm start`

<span data-ttu-id="69286-183">Uygulamayı istiyorsanız, basın `<Enter>` anahtarı.</span><span class="sxs-lookup"><span data-stu-id="69286-183">If you want to terminate the application, press `<Enter>` key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="69286-184">IOT kenar sonlandırmak için Ctrl + C kullanmak için önerilmez.</span><span class="sxs-lookup"><span data-stu-id="69286-184">It is not recommended to use Ctrl + C to terminate the IoT Edge application.</span></span> <span data-ttu-id="69286-185">Bu şekilde aşırı ciddiyeti işlemin neden olarak.</span><span class="sxs-lookup"><span data-stu-id="69286-185">As this way may cause the process to terminate abnormally.</span></span>
