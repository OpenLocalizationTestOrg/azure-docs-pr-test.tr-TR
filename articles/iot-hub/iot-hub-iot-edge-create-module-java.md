---
title: "Java ile Azure IOT kenar modülü oluşturma | Microsoft Docs"
description: "Bu öğretici nasıl en son Azure IOT kenar Maven paketlerini kullanma bırak veri dönüştürücü modülü yazılacağını gösterir."
services: iot-hub
author: junyi
manager: timlt
ms.service: iot-hub
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 06/28/2017
ms.author: junyi
ms.openlocfilehash: 0c430272225d79737baec2be15ed7c93991cdeac
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-azure-iot-edge-module-with-java"></a><span data-ttu-id="76793-103">Java ile Azure IOT kenar modülü oluşturun</span><span class="sxs-lookup"><span data-stu-id="76793-103">Create an Azure IoT Edge Module with Java</span></span>

<span data-ttu-id="76793-104">Bu öğretici bir Java Azure IOT sınır için bir modül nasıl oluşturabilir gösterir.</span><span class="sxs-lookup"><span data-stu-id="76793-104">This tutorial showcases how one might build a module for Azure IoT Edge in Java.</span></span>

<span data-ttu-id="76793-105">Bu öğreticide, biz ortam kurulumu ve nasıl yazılacağını yükselteceğinizi bir [bırak](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) veri dönüştürücü modülü en son Azure IOT kenar Maven paketleri kullanma.</span><span class="sxs-lookup"><span data-stu-id="76793-105">In this tutorial, we will walk through environment setup and how to write a [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) data converter module using the latest Azure IoT Edge Maven packages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="76793-106">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="76793-106">Prerequisites</span></span>

<span data-ttu-id="76793-107">Bu bölümde IOT kenar modülü geliştirme ortamınızı ayarlayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="76793-107">In this section, you will set up your environment for IoT Edge module development.</span></span> <span data-ttu-id="76793-108">Her ikisi de geçerli *64-bit Windows* ve *64-bit Linux (Ubuntu/Debian 8)* işletim sistemleri.</span><span class="sxs-lookup"><span data-stu-id="76793-108">It applies to both *64-bit Windows* and *64-bit Linux (Ubuntu/Debian 8)* operating systems.</span></span>

<span data-ttu-id="76793-109">Aşağıdaki yazılımlar gereklidir:</span><span class="sxs-lookup"><span data-stu-id="76793-109">The following software is required:</span></span>

* <span data-ttu-id="76793-110">[Git istemci](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="76793-110">[Git Client](https://git-scm.com/downloads).</span></span>
* <span data-ttu-id="76793-111">[**x64** JDK](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="76793-111">[**x64** JDK](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
* <span data-ttu-id="76793-112">[Maven](https://maven.apache.org/install.html).</span><span class="sxs-lookup"><span data-stu-id="76793-112">[Maven](https://maven.apache.org/install.html).</span></span>

<span data-ttu-id="76793-113">Komut satırı bir terminal penceresi açın ve aşağıdaki depoyu kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="76793-113">Open a command-line terminal window and clone the following repository:</span></span>

1. <span data-ttu-id="76793-114">`git clone https://github.com/Azure-Samples/iot-edge-samples.git`.</span><span class="sxs-lookup"><span data-stu-id="76793-114">`git clone https://github.com/Azure-Samples/iot-edge-samples.git`.</span></span>
2. `cd iot-edge-samples/java/simulated_ble`

## <a name="overall-architecture"></a><span data-ttu-id="76793-115">Genel mimari</span><span class="sxs-lookup"><span data-stu-id="76793-115">Overall architecture</span></span>

<span data-ttu-id="76793-116">Azure IOT kenar platform yoğun uyarlar [Von Neumann mimarisi](https://en.wikipedia.org/wiki/Von_Neumann_architecture).</span><span class="sxs-lookup"><span data-stu-id="76793-116">The Azure IoT Edge platform heavily adopts the [Von Neumann architecture](https://en.wikipedia.org/wiki/Von_Neumann_architecture).</span></span> <span data-ttu-id="76793-117">Hangi tüm Azure IOT kenar mimarisi, işleyen giriş ve çıkışı üretir bir sistem anlamına gelir; ve tek tek her modül küçük bir giriş-çıkış alt olduğunu.</span><span class="sxs-lookup"><span data-stu-id="76793-117">Which means that the entire Azure IoT Edge architecture is a system which processes input and produces output; and that each individual module is also a tiny input-output subsystem.</span></span> <span data-ttu-id="76793-118">Bu öğreticide, biz aşağıdaki iki modüller getirir:</span><span class="sxs-lookup"><span data-stu-id="76793-118">In this tutorial, we will introduce the following two modules:</span></span>

1. <span data-ttu-id="76793-119">Sanal alan bir modül [bırak](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) sinyal ve biçimlendirilmiş dönüştürür [JSON](https://en.wikipedia.org/wiki/JSON) ileti.</span><span class="sxs-lookup"><span data-stu-id="76793-119">A module which receives a simulated [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) signal and converts it into a formatted [JSON](https://en.wikipedia.org/wiki/JSON) message.</span></span>
2. <span data-ttu-id="76793-120">Alınan yazdırır bir modül [JSON](https://en.wikipedia.org/wiki/JSON) ileti.</span><span class="sxs-lookup"><span data-stu-id="76793-120">A module which prints the received [JSON](https://en.wikipedia.org/wiki/JSON) message.</span></span>

<span data-ttu-id="76793-121">Aşağıdaki resimde bu proje için tipik uçtan uca veri akışı görüntüler:</span><span class="sxs-lookup"><span data-stu-id="76793-121">The following image displays the typical end-to-end dataflow for this project:</span></span>

<span data-ttu-id="76793-122">![Veri akışı üç modülleri arasında](media/iot-hub-iot-edge-create-module/dataflow.png "giriş: benzetimli bırak Modülü; İşlemci: Dönüştürücü Modülü; Çıktı: Yazıcı Modülü")</span><span class="sxs-lookup"><span data-stu-id="76793-122">![Dataflow between three modules](media/iot-hub-iot-edge-create-module/dataflow.png "Input: Simulated BLE Module; Processor: Converter Module; Output: Printer Module")</span></span>

## <a name="understanding-the-code"></a><span data-ttu-id="76793-123">Kodu anlama</span><span class="sxs-lookup"><span data-stu-id="76793-123">Understanding the code</span></span>

### <a name="maven-project-structure"></a><span data-ttu-id="76793-124">Maven projesi yapısı</span><span class="sxs-lookup"><span data-stu-id="76793-124">Maven project structure</span></span>

<span data-ttu-id="76793-125">Azure IOT kenar paketleri Maven üzerinde dayandığından, içeren tipik bir Maven projesi yapısı oluşturmak ihtiyacımız bir `pom.xml` dosyası.</span><span class="sxs-lookup"><span data-stu-id="76793-125">Since Azure IoT Edge packages are based on Maven, we need to create a typical Maven project structure, which contains a `pom.xml` file.</span></span>

<span data-ttu-id="76793-126">POM devraldığı `com.microsoft.azure.gateway.gateway-module-base` tüm çalışma zamanı ikili dosyaları, ağ geçidi yapılandırma dosyası yolu ve yürütme davranışını içeren bir modülü projesi tarafından gerekli bağımlılıkların bildirir paket.</span><span class="sxs-lookup"><span data-stu-id="76793-126">The POM inherits from the `com.microsoft.azure.gateway.gateway-module-base` package, which declares all of the dependencies needed by a module project which includes the runtime binaries, the gateway configuration file path, and the execution behavior.</span></span> <span data-ttu-id="76793-127">Bu, bize çok fazla kaydeder ve yazma ve kod satırlarını yüzlerce tekrar tekrar yeniden yazma gereksinimini ortadan kaldırır.</span><span class="sxs-lookup"><span data-stu-id="76793-127">This saves us lots of time and eliminate the need to write and rewrite hundreds of lines of code over and over again.</span></span>

<span data-ttu-id="76793-128">Biz gerekli bağımlılıkları/eklenti ve aşağıdaki kod parçacığında gösterildiği gibi bizim modülü tarafından kullanılacak yapılandırma dosyasının adını bildirerek pom.xml dosyasını güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="76793-128">We need to update the pom.xml file by declaring the required dependencies/plugins and the name of the configuration file to be used by our module as shown in the following code snippet.</span></span>

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <!-- Inherit from parent -->
  <parent>
    <groupId>com.microsoft.azure.gateway</groupId>
    <artifactId>gateway-module-base</artifactId>
    <version>1.0.1</version>
  </parent>
  
  <groupId>com.microsoft.azure.gateway</groupId>
  <artifactId>ble-converter</artifactId>
  <version>1.0</version>
  <packaging>jar</packaging>

  <!-- Set the filename of the Azure IoT Edge configuration located
       under ./src/main/resources/gateway/ which is used in parent -->
  <properties>
    <gw.config.fileName>gw-config.json</gw.config.fileName>
  </properties>

  <!-- Re-declare dependencies used in parent -->
  <dependencies>
    <dependency>
      <groupId>com.microsoft.azure.gateway</groupId>
      <artifactId>gateway-java-binding</artifactId>
    </dependency>
    <dependency>
      <groupId>${dependency.runtime.group}</groupId>
      <artifactId>${dependency.runtime.name}</artifactId>
    </dependency>
  </dependencies>

  <!-- Re-declare plugins used in parent -->
  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-dependency-plugin</artifactId>
      </plugin>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-resources-plugin</artifactId>
      </plugin>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-shade-plugin</artifactId>
      </plugin>
      <plugin>
        <groupId>org.codehaus.mojo</groupId>
        <artifactId>exec-maven-plugin</artifactId>
      </plugin>
    </plugins>
  </build>
</project>
```

### <a name="basic-understanding-of-an-azure-iot-edge-module"></a><span data-ttu-id="76793-129">Bir Azure IOT kenar modülün temel anlama</span><span class="sxs-lookup"><span data-stu-id="76793-129">Basic understanding of an Azure IoT Edge module</span></span>

<span data-ttu-id="76793-130">Bir veri işleri için işlemci olarak Azure IOT kenar modülü davranabilirsiniz: girişi almak, işlemesi ve çıktı üretir.</span><span class="sxs-lookup"><span data-stu-id="76793-130">You can treat an Azure IoT Edge module as a data processor whose job is to: receive input, process it, and produce output.</span></span>

<span data-ttu-id="76793-131">Giriş (gibi hareket algılayıcısı) donanım verilerden bir ileti diğer modüller ya da (örneğin, düzenli aralıklarla bir Zamanlayıcı tarafından oluşturulan bir rastgele sayı) başka bir şey olabilir.</span><span class="sxs-lookup"><span data-stu-id="76793-131">The input might be data from hardware (like a motion detector), a message from other modules, or anything else (like a random number generated periodically by a timer).</span></span>

<span data-ttu-id="76793-132">Giriş benzer bir çıkış, tetikleyebilir donanım davranış (gibi yanıp sönen LED), diğer modüller ya da (örneğin, yazdırma konsoluna) başka bir şey için bir ileti.</span><span class="sxs-lookup"><span data-stu-id="76793-132">The output is similar to the input, it could trigger hardware behavior (like the blinking LED), a message to other modules, or anything else (like printing to the console).</span></span>

<span data-ttu-id="76793-133">Modüller birbirleri ile kullanarak iletişim `com.microsoft.azure.gateway.messaging.Message` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="76793-133">Modules communicate with each other using `com.microsoft.azure.gateway.messaging.Message` class.</span></span> <span data-ttu-id="76793-134">**İçerik** , bir `Message` istediğiniz verilerin herhangi bir tür temsil etme işleyebilen bir bayt dizisi.</span><span class="sxs-lookup"><span data-stu-id="76793-134">The **Content** of a `Message` is a byte array which is capable of representing any kind of data you like.</span></span> <span data-ttu-id="76793-135">**Özellikler** mevcuttur `Message` ve yalnızca bir dize-dize eşleme.</span><span class="sxs-lookup"><span data-stu-id="76793-135">**Properties** are also available in the `Message` and are simply a string-to-string mapping.</span></span> <span data-ttu-id="76793-136">Düşünebilirsiniz **özellikleri** bir HTTP isteğinin ya da meta veri dosyasının başlığı olarak.</span><span class="sxs-lookup"><span data-stu-id="76793-136">You may think of **Properties** as the headers in an HTTP request, or the metadata of a file.</span></span>

<span data-ttu-id="76793-137">Java Azure IOT kenar modülünde geliştirmek için hangi devraldığı yeni bir modül sınıfı oluşturmanız gerekir `com.microsoft.azure.gateway.core.GatewayModule` ve gerekli soyut yöntemleri uygulamak `receive()` ve `destroy()`.</span><span class="sxs-lookup"><span data-stu-id="76793-137">In order to develop an Azure IoT Edge module in Java, you need to create a new module class which inherits from `com.microsoft.azure.gateway.core.GatewayModule` and implement the required abstract methods `receive()` and `destroy()`.</span></span> <span data-ttu-id="76793-138">Bu noktada, ayrıca isteğe bağlı uygulamayı seçebilir `start()` veya `create()` de yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="76793-138">At this point, you may also choose to implement the optional `start()` or `create()` methods as well.</span></span> <span data-ttu-id="76793-139">Aşağıdaki kod parçacığını bir Azure IOT kenar modülü yazma başlayacağınızı gösterir.</span><span class="sxs-lookup"><span data-stu-id="76793-139">The following code snippet shows you how to get started authoring an Azure IoT Edge module.</span></span>

```java
import com.microsoft.azure.gateway.core.Broker;
import com.microsoft.azure.gateway.core.GatewayModule;
import com.microsoft.azure.gateway.messaging.Message;

public class MyEdgeModule extends GatewayModule {
  public MyEdgeModule(long address, Broker broker, String configuration) {
    /* Let the GatewayModule do the dirty work of initialization. It's also
       a good time to parse your own configuration defined in Azure IoT Edge
       configuration file (typically ./src/main/resources/gateway/gw-config.json) */
    super(address, broker, configuration);
  }

  @Override
  public void start() {
    /* Acquire the resources you need. If you don't
       need any resources, you may omit this method. */
  }

  @Override
  public void destroy() {
    /* It's time to release all resources. This method is required. */
  }

  @Override
  public void receive(Message message) {
    /* Logic to process the input message. This method is required. */
    // ...
    /* Use publish() method to do the output. You are
       allowed to publish your new Message instance. */
    this.publish(message);
  }
}
```

### <a name="converter-module"></a><span data-ttu-id="76793-140">Dönüştürücü Modülü</span><span class="sxs-lookup"><span data-stu-id="76793-140">Converter module</span></span>

| <span data-ttu-id="76793-141">Girdi</span><span class="sxs-lookup"><span data-stu-id="76793-141">Input</span></span>                    | <span data-ttu-id="76793-142">İşlemci</span><span class="sxs-lookup"><span data-stu-id="76793-142">Processor</span></span>                              | <span data-ttu-id="76793-143">Çıktı</span><span class="sxs-lookup"><span data-stu-id="76793-143">Output</span></span>                 | <span data-ttu-id="76793-144">Kaynak dosya</span><span class="sxs-lookup"><span data-stu-id="76793-144">Source File</span></span>            |
| ------------------------ | -------------------------------------- | ---------------------- | ---------------------- |
| <span data-ttu-id="76793-145">Sıcaklık veri iletisi</span><span class="sxs-lookup"><span data-stu-id="76793-145">Temperature data message</span></span> | <span data-ttu-id="76793-146">Ayrıştırma ve yeni bir JSON ileti oluşturun</span><span class="sxs-lookup"><span data-stu-id="76793-146">Parse and construct a new JSON message</span></span> | <span data-ttu-id="76793-147">Yapı JSON iletisi</span><span class="sxs-lookup"><span data-stu-id="76793-147">Structure JSON message</span></span> | `ConverterModule.java` |

<span data-ttu-id="76793-148">Bu modül tipik bir Azure IOT kenar modüldür.</span><span class="sxs-lookup"><span data-stu-id="76793-148">This module is a typical Azure IoT Edge module.</span></span> <span data-ttu-id="76793-149">Diğer modüllerden sıcaklık iletileri kabul eder (bir donanım modülü veya bu bizim benzetimli bırak modülü durumda); ve (sıcaklık uyarı tetiklemesi ve benzeri için ihtiyacımız özelliğini ayarlama ileti kimliği ekleme dahil) yapılandırılmış bir JSON iletisi sıcaklık iletisinde normalleştirir.</span><span class="sxs-lookup"><span data-stu-id="76793-149">It accepts temperature messages from other modules (a hardware module, or in this case our simulated BLE module); and then normalizes the temperature message in to a structured JSON message (including appending the message ID, setting the property of whether we need to trigger the temperature alert, and so on).</span></span>

```java
@Override
public void receive(Message message) {
  try {
    JSONObject messageFromBle = new JSONObject(new String(message.getContent()));
    double temperature = messageFromBle.getDouble("temperature");
    Map<String, String> inputProperties = message.getProperties();

    HashMap<String, String> properties = new HashMap<>();
    properties.put("source", inputProperties.get("source"));
    properties.put("macAddress", inputProperties.get("macAddress"));
    properties.put("temperatureAlert", temperature > 30 ? "true" : "false");

    String content = String.format(
        "{ \"deviceId\": \"Intel NUC Gateway\", \"messageId\": %d, \"temperature\": %f }",
        ++this.messageCount, temperature);

    this.publish(new Message(content.getBytes(), properties));
  } catch (Exception ex) {
    ex.printStackTrace();
  }
}
```

### <a name="printer-module"></a><span data-ttu-id="76793-150">Yazıcı Modülü</span><span class="sxs-lookup"><span data-stu-id="76793-150">Printer module</span></span>

| <span data-ttu-id="76793-151">Girdi</span><span class="sxs-lookup"><span data-stu-id="76793-151">Input</span></span>                          | <span data-ttu-id="76793-152">İşlemci</span><span class="sxs-lookup"><span data-stu-id="76793-152">Processor</span></span> | <span data-ttu-id="76793-153">Çıktı</span><span class="sxs-lookup"><span data-stu-id="76793-153">Output</span></span>                     | <span data-ttu-id="76793-154">Kaynak dosya</span><span class="sxs-lookup"><span data-stu-id="76793-154">Source File</span></span>          |
| ------------------------------ | --------- | -------------------------- | -------------------- |
| <span data-ttu-id="76793-155">Diğer modüllerden herhangi bir iletisi</span><span class="sxs-lookup"><span data-stu-id="76793-155">Any message from other modules</span></span> | <span data-ttu-id="76793-156">Yok</span><span class="sxs-lookup"><span data-stu-id="76793-156">N/A</span></span>       | <span data-ttu-id="76793-157">İleti konsola oturum</span><span class="sxs-lookup"><span data-stu-id="76793-157">Log the message to console</span></span> | `PrinterModule.java` |

<span data-ttu-id="76793-158">Bu, terminal penceresi alınan iletileri çıkarır basit ve açıklayıcı, bir modüldür.</span><span class="sxs-lookup"><span data-stu-id="76793-158">This is a simple, self-explanatory, module which outputs the received messages to the terminal window.</span></span>

```java
@Override
public void receive(Message message) {
  System.out.println(message.toString());
}
```

### <a name="azure-iot-edge-configuration"></a><span data-ttu-id="76793-159">Azure IOT kenar yapılandırma</span><span class="sxs-lookup"><span data-stu-id="76793-159">Azure IoT Edge configuration</span></span>

<span data-ttu-id="76793-160">Modülleri çalıştırmadan önce son adım, Azure IOT kenar yapılandırmak ve modülleri arasında bağlantı kurmak için ' dir.</span><span class="sxs-lookup"><span data-stu-id="76793-160">The final step before running the modules is to configure the Azure IoT Edge and to establish the connections between modules.</span></span>

<span data-ttu-id="76793-161">İlk başvurduğu (itibaren Azure IOT kenar destekler yükleyicilerini farklı dillerde) bizim Java yükleyicisi bildirmek ihtiyacımız kendi `name` bölümlerde daha sonra.</span><span class="sxs-lookup"><span data-stu-id="76793-161">First we need to declare our Java loader (since Azure IoT Edge supports loaders of different languages) which could be referenced by its `name` in the sections afterward.</span></span>

```json
"loaders": [{
  "type": "java",
  "name": "java",
  "configuration": {
    "jvm.options": {
      "library.path": "./"
    }
  }
}]
```

<span data-ttu-id="76793-162">Biz bizim yükleyicilerini bildirdikten sonra biz de bizim modülleri bildirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="76793-162">Once we have declared our loaders, we will also need to declare our modules as well.</span></span> <span data-ttu-id="76793-163">Benzer yükleyicileri bildirmek için bunlar ayrıca tarafından başvurulabilir kendi `name` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="76793-163">Similar to declaring the loaders, they can also be referenced by their `name` attribute.</span></span> <span data-ttu-id="76793-164">Bir modül bildirirken (hangi önce tanımladığımız biri olmalıdır) kullanması gereken yükleyicisi belirtmek ihtiyacımız ve-(bizim modül normalleştirilmiş sınıf adı olmalıdır) için giriş noktası her modül.</span><span class="sxs-lookup"><span data-stu-id="76793-164">When declaring a module, we need to specify the loader it should use (which should be the one we defined before) and the entry-point (should be the normalized class name of our module) for each module.</span></span> <span data-ttu-id="76793-165">`simulated_device` Azure IOT kenar çekirdek çalışma zamanı paketinde bulunan bir yerel modül modülüdür.</span><span class="sxs-lookup"><span data-stu-id="76793-165">The `simulated_device` module is a native module which is included in the Azure IoT Edge core runtime package.</span></span> <span data-ttu-id="76793-166">Her zaman içermelidir `args` JSON'dosyası, olsa bile `null`.</span><span class="sxs-lookup"><span data-stu-id="76793-166">You should always include `args` in the JSON file even if it is `null`.</span></span>

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
      "name": "java",
      "entrypoint": {
        "class.name": "com/microsoft/azure/gateway/ConverterModule",
        "class.path": "./ble-converter-1.0-with-deps.jar"
      }
    },
    "args": null
  },
  {
    "name": "print",
    "loader": {
      "name": "java",
      "entrypoint": {
        "class.name": "com/microsoft/azure/gateway/PrinterModule",
        "class.path": "./ble-converter-1.0-with-deps.jar"
      }
    },
    "args": null
  }
]
```

<span data-ttu-id="76793-167">Yapılandırma sonunda bağlantı kurun.</span><span class="sxs-lookup"><span data-stu-id="76793-167">At the end of the configuration, we establish the connections.</span></span> <span data-ttu-id="76793-168">Her bağlantı ile ifade edilen `source` ve `sink`.</span><span class="sxs-lookup"><span data-stu-id="76793-168">Each connection is expressed by `source` and `sink`.</span></span> <span data-ttu-id="76793-169">Önceden tanımlanmış bir modül her ikisi de başvurmalısınız.</span><span class="sxs-lookup"><span data-stu-id="76793-169">They should both reference a pre-defined module.</span></span> <span data-ttu-id="76793-170">Çıktı ileti `source` modülü girişi için iletilir `sink` modülü.</span><span class="sxs-lookup"><span data-stu-id="76793-170">The output message of `source` module will be forwarded to the input of `sink` module.</span></span>

```json
"links": [
  {
    "source": "simulated_device",
    "sink": "converter"
  },
  {
    "source": "converter",
    "sink": "print"
  }
]
```

## <a name="running-the-modules"></a><span data-ttu-id="76793-171">Modülleri çalıştırma</span><span class="sxs-lookup"><span data-stu-id="76793-171">Running the modules</span></span>

<span data-ttu-id="76793-172">Kullanım `mvn package` içine her şeyi oluşturmak için `target/` klasör.</span><span class="sxs-lookup"><span data-stu-id="76793-172">Use `mvn package` to build everything into the `target/` folder.</span></span> <span data-ttu-id="76793-173">`mvn clean package`Ayrıca temiz bir yapı için tavsiye edilir.</span><span class="sxs-lookup"><span data-stu-id="76793-173">`mvn clean package` is also recommended for a clean build.</span></span>

<span data-ttu-id="76793-174">Kullanım `mvn exec:exec` Azure IOT kenar ve çalıştırmak için sıcaklık veri ve tüm özellikler sabit bir oranda konsola yazdırılır gözlemlemek.</span><span class="sxs-lookup"><span data-stu-id="76793-174">Use `mvn exec:exec` to run the Azure IoT Edge and you should observe that the temperature data and all the properties are printed to the console at a fixed rate.</span></span>

<span data-ttu-id="76793-175">Uygulamayı istiyorsanız, basın `<Enter>` anahtarı.</span><span class="sxs-lookup"><span data-stu-id="76793-175">If you want to terminate the application, press `<Enter>` key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="76793-176">IOT sınır ağ geçidi sonlandırmak için Ctrl + C kullanmak için önerilmez.</span><span class="sxs-lookup"><span data-stu-id="76793-176">It is not recommended to use Ctrl + C to terminate the IoT Edge gateway application.</span></span> <span data-ttu-id="76793-177">Bu, olağan dışı ciddiyeti işlemin neden olabilir ve.</span><span class="sxs-lookup"><span data-stu-id="76793-177">As this may cause the process to terminate abnormally.</span></span>

