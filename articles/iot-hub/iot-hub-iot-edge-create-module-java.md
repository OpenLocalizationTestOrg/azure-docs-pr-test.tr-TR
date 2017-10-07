---
title: "aaaCreate bir Java ile Azure IOT kenar Modülü | Microsoft Docs"
description: "Bu öğretici, nasıl bir bırak veri dönüştürücü modülünü kullanarak toowrite hello en son Azure IOT kenar Maven paketlerin gösterir."
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
ms.openlocfilehash: abb560933d13d133ae9a1da08b503d5735b230e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-iot-edge-module-with-java"></a><span data-ttu-id="d4446-103">Java ile Azure IOT kenar modülü oluşturun</span><span class="sxs-lookup"><span data-stu-id="d4446-103">Create an Azure IoT Edge Module with Java</span></span>

<span data-ttu-id="d4446-104">Bu öğretici bir Java Azure IOT sınır için bir modül nasıl oluşturabilir gösterir.</span><span class="sxs-lookup"><span data-stu-id="d4446-104">This tutorial showcases how one might build a module for Azure IoT Edge in Java.</span></span>

<span data-ttu-id="d4446-105">Bu öğreticide, ortamı kurulumu aracılığıyla size yol gösterir ve nasıl toowrite bir [bırak](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) veri dönüştürücü modülü hello en son Azure IOT kenar Maven paketleri kullanma.</span><span class="sxs-lookup"><span data-stu-id="d4446-105">In this tutorial, we will walk through environment setup and how toowrite a [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) data converter module using hello latest Azure IoT Edge Maven packages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d4446-106">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="d4446-106">Prerequisites</span></span>

<span data-ttu-id="d4446-107">Bu bölümde IOT kenar modülü geliştirme ortamınızı ayarlayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="d4446-107">In this section, you will set up your environment for IoT Edge module development.</span></span> <span data-ttu-id="d4446-108">Tooboth geçerlidir *64-bit Windows* ve *64-bit Linux (Ubuntu/Debian 8)* işletim sistemleri.</span><span class="sxs-lookup"><span data-stu-id="d4446-108">It applies tooboth *64-bit Windows* and *64-bit Linux (Ubuntu/Debian 8)* operating systems.</span></span>

<span data-ttu-id="d4446-109">yazılımı aşağıdaki hello gereklidir:</span><span class="sxs-lookup"><span data-stu-id="d4446-109">hello following software is required:</span></span>

* <span data-ttu-id="d4446-110">[Git istemci](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="d4446-110">[Git Client](https://git-scm.com/downloads).</span></span>
* <span data-ttu-id="d4446-111">[**x64** JDK](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="d4446-111">[**x64** JDK](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
* <span data-ttu-id="d4446-112">[Maven](https://maven.apache.org/install.html).</span><span class="sxs-lookup"><span data-stu-id="d4446-112">[Maven](https://maven.apache.org/install.html).</span></span>

<span data-ttu-id="d4446-113">Depo izleyen bir komut satırı terminal penceresi ve kopya hello açın:</span><span class="sxs-lookup"><span data-stu-id="d4446-113">Open a command-line terminal window and clone hello following repository:</span></span>

1. <span data-ttu-id="d4446-114">`git clone https://github.com/Azure-Samples/iot-edge-samples.git`.</span><span class="sxs-lookup"><span data-stu-id="d4446-114">`git clone https://github.com/Azure-Samples/iot-edge-samples.git`.</span></span>
2. `cd iot-edge-samples/java/simulated_ble`

## <a name="overall-architecture"></a><span data-ttu-id="d4446-115">Genel mimari</span><span class="sxs-lookup"><span data-stu-id="d4446-115">Overall architecture</span></span>

<span data-ttu-id="d4446-116">Hello Azure IOT kenar platform yoğun hello uyarlar [Von Neumann mimarisi](https://en.wikipedia.org/wiki/Von_Neumann_architecture).</span><span class="sxs-lookup"><span data-stu-id="d4446-116">hello Azure IoT Edge platform heavily adopts hello [Von Neumann architecture](https://en.wikipedia.org/wiki/Von_Neumann_architecture).</span></span> <span data-ttu-id="d4446-117">Bu hello tüm Azure IOT kenar mimarisi anlamına gelir, işleyen giriş ve çıkışı üretir bir sistemdir; ve tek tek her modül küçük bir giriş-çıkış alt olduğunu.</span><span class="sxs-lookup"><span data-stu-id="d4446-117">Which means that hello entire Azure IoT Edge architecture is a system which processes input and produces output; and that each individual module is also a tiny input-output subsystem.</span></span> <span data-ttu-id="d4446-118">Bu öğreticide, şu iki modülleri aşağıdaki hello getirir:</span><span class="sxs-lookup"><span data-stu-id="d4446-118">In this tutorial, we will introduce hello following two modules:</span></span>

1. <span data-ttu-id="d4446-119">Sanal alan bir modül [bırak](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) sinyal ve biçimlendirilmiş dönüştürür [JSON](https://en.wikipedia.org/wiki/JSON) ileti.</span><span class="sxs-lookup"><span data-stu-id="d4446-119">A module which receives a simulated [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) signal and converts it into a formatted [JSON](https://en.wikipedia.org/wiki/JSON) message.</span></span>
2. <span data-ttu-id="d4446-120">Alınan hello yazdırır bir modül [JSON](https://en.wikipedia.org/wiki/JSON) ileti.</span><span class="sxs-lookup"><span data-stu-id="d4446-120">A module which prints hello received [JSON](https://en.wikipedia.org/wiki/JSON) message.</span></span>

<span data-ttu-id="d4446-121">Merhaba aşağıdaki görüntüde hello tipik uçtan uca veri akışı bu proje için görüntüler:</span><span class="sxs-lookup"><span data-stu-id="d4446-121">hello following image displays hello typical end-to-end dataflow for this project:</span></span>

<span data-ttu-id="d4446-122">![Veri akışı üç modülleri arasında](media/iot-hub-iot-edge-create-module/dataflow.png "giriş: benzetimli bırak Modülü; İşlemci: Dönüştürücü Modülü; Çıktı: Yazıcı Modülü")</span><span class="sxs-lookup"><span data-stu-id="d4446-122">![Dataflow between three modules](media/iot-hub-iot-edge-create-module/dataflow.png "Input: Simulated BLE Module; Processor: Converter Module; Output: Printer Module")</span></span>

## <a name="understanding-hello-code"></a><span data-ttu-id="d4446-123">Merhaba kodu anlama</span><span class="sxs-lookup"><span data-stu-id="d4446-123">Understanding hello code</span></span>

### <a name="maven-project-structure"></a><span data-ttu-id="d4446-124">Maven projesi yapısı</span><span class="sxs-lookup"><span data-stu-id="d4446-124">Maven project structure</span></span>

<span data-ttu-id="d4446-125">Azure IOT kenar paketleri Maven üzerinde dayandığından, toocreate içeren tipik bir Maven projesi yapısı ihtiyacımız bir `pom.xml` dosyası.</span><span class="sxs-lookup"><span data-stu-id="d4446-125">Since Azure IoT Edge packages are based on Maven, we need toocreate a typical Maven project structure, which contains a `pom.xml` file.</span></span>

<span data-ttu-id="d4446-126">Merhaba POM devralır hello `com.microsoft.azure.gateway.gateway-module-base` tüm hello çalışma zamanı ikili dosyaları, hello ağ geçidi yapılandırma dosyası yolu ve hello yürütme davranışı içeren bir modülü projesi tarafından gerekli hello bağımlılıklarını bildirir paket.</span><span class="sxs-lookup"><span data-stu-id="d4446-126">hello POM inherits from hello `com.microsoft.azure.gateway.gateway-module-base` package, which declares all of hello dependencies needed by a module project which includes hello runtime binaries, hello gateway configuration file path, and hello execution behavior.</span></span> <span data-ttu-id="d4446-127">Bu bize çok fazla kaydeder ve hello gerek toowrite ortadan kaldırmak ve kod satırlarını yüzlerce tekrar tekrar yeniden yazın.</span><span class="sxs-lookup"><span data-stu-id="d4446-127">This saves us lots of time and eliminate hello need toowrite and rewrite hundreds of lines of code over and over again.</span></span>

<span data-ttu-id="d4446-128">Merhaba gerekli bağımlılıkları/eklenti ve hello aşağıdaki kod parçacığında gösterildiği gibi bizim modülü tarafından kullanılan hello yapılandırma dosyası toobe hello adını bildirerek tooupdate pom.xml dosyasını ihtiyacımız var.</span><span class="sxs-lookup"><span data-stu-id="d4446-128">We need tooupdate the pom.xml file by declaring hello required dependencies/plugins and hello name of hello configuration file toobe used by our module as shown in hello following code snippet.</span></span>

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

  <!-- Set hello filename of hello Azure IoT Edge configuration located
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

### <a name="basic-understanding-of-an-azure-iot-edge-module"></a><span data-ttu-id="d4446-129">Bir Azure IOT kenar modülün temel anlama</span><span class="sxs-lookup"><span data-stu-id="d4446-129">Basic understanding of an Azure IoT Edge module</span></span>

<span data-ttu-id="d4446-130">Bir veri işleri için işlemci olarak Azure IOT kenar modülü davranabilirsiniz: girişi almak, işlemesi ve çıktı üretir.</span><span class="sxs-lookup"><span data-stu-id="d4446-130">You can treat an Azure IoT Edge module as a data processor whose job is to: receive input, process it, and produce output.</span></span>

<span data-ttu-id="d4446-131">Merhaba giriş donanım (gibi hareket algılayıcısı) verileri, bir ileti diğer modüller ya da (örneğin, düzenli aralıklarla bir Zamanlayıcı tarafından oluşturulan bir rastgele sayı) başka bir şey olabilir.</span><span class="sxs-lookup"><span data-stu-id="d4446-131">hello input might be data from hardware (like a motion detector), a message from other modules, or anything else (like a random number generated periodically by a timer).</span></span>

<span data-ttu-id="d4446-132">Merhaba çıkış benzer toohello giriş, donanım davranış (gibi hello ışığı yanıp sönen), bir ileti tooother modülleri ya da (yazdırma toohello konsolu gibi) başka bir şey tetikleyebilir.</span><span class="sxs-lookup"><span data-stu-id="d4446-132">hello output is similar toohello input, it could trigger hardware behavior (like hello blinking LED), a message tooother modules, or anything else (like printing toohello console).</span></span>

<span data-ttu-id="d4446-133">Modüller birbirleri ile kullanarak iletişim `com.microsoft.azure.gateway.messaging.Message` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="d4446-133">Modules communicate with each other using `com.microsoft.azure.gateway.messaging.Message` class.</span></span> <span data-ttu-id="d4446-134">Merhaba **içerik** , bir `Message` istediğiniz verilerin herhangi bir tür temsil etme işleyebilen bir bayt dizisi.</span><span class="sxs-lookup"><span data-stu-id="d4446-134">hello **Content** of a `Message` is a byte array which is capable of representing any kind of data you like.</span></span> <span data-ttu-id="d4446-135">**Özellikler** de hello kullanılabilir `Message` ve yalnızca bir dize-dize eşleme.</span><span class="sxs-lookup"><span data-stu-id="d4446-135">**Properties** are also available in hello `Message` and are simply a string-to-string mapping.</span></span> <span data-ttu-id="d4446-136">Düşünebilirsiniz **özellikleri** bir HTTP isteğinin ya da hello meta veri dosyasının hello başlığı olarak.</span><span class="sxs-lookup"><span data-stu-id="d4446-136">You may think of **Properties** as hello headers in an HTTP request, or hello metadata of a file.</span></span>

<span data-ttu-id="d4446-137">Sipariş toodevelop Java Azure IOT kenar modülünde'da, toocreate devraldığı yeni bir modül sınıf gereken `com.microsoft.azure.gateway.core.GatewayModule` ve gerekli hello soyut yöntemleri uygulamak `receive()` ve `destroy()`.</span><span class="sxs-lookup"><span data-stu-id="d4446-137">In order toodevelop an Azure IoT Edge module in Java, you need toocreate a new module class which inherits from `com.microsoft.azure.gateway.core.GatewayModule` and implement hello required abstract methods `receive()` and `destroy()`.</span></span> <span data-ttu-id="d4446-138">Bu noktada, ayrıca isteğe bağlı tooimplement hello tercih edebilirsiniz `start()` veya `create()` de yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="d4446-138">At this point, you may also choose tooimplement hello optional `start()` or `create()` methods as well.</span></span> <span data-ttu-id="d4446-139">Aşağıdaki kod parçacığını hello Azure IOT kenar modülü yazma tooget nasıl başlatılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="d4446-139">hello following code snippet shows you how tooget started authoring an Azure IoT Edge module.</span></span>

```java
import com.microsoft.azure.gateway.core.Broker;
import com.microsoft.azure.gateway.core.GatewayModule;
import com.microsoft.azure.gateway.messaging.Message;

public class MyEdgeModule extends GatewayModule {
  public MyEdgeModule(long address, Broker broker, String configuration) {
    /* Let hello GatewayModule do hello dirty work of initialization. It's also
       a good time tooparse your own configuration defined in Azure IoT Edge
       configuration file (typically ./src/main/resources/gateway/gw-config.json) */
    super(address, broker, configuration);
  }

  @Override
  public void start() {
    /* Acquire hello resources you need. If you don't
       need any resources, you may omit this method. */
  }

  @Override
  public void destroy() {
    /* It's time toorelease all resources. This method is required. */
  }

  @Override
  public void receive(Message message) {
    /* Logic tooprocess hello input message. This method is required. */
    // ...
    /* Use publish() method toodo hello output. You are
       allowed toopublish your new Message instance. */
    this.publish(message);
  }
}
```

### <a name="converter-module"></a><span data-ttu-id="d4446-140">Dönüştürücü Modülü</span><span class="sxs-lookup"><span data-stu-id="d4446-140">Converter module</span></span>

| <span data-ttu-id="d4446-141">Girdi</span><span class="sxs-lookup"><span data-stu-id="d4446-141">Input</span></span>                    | <span data-ttu-id="d4446-142">İşlemci</span><span class="sxs-lookup"><span data-stu-id="d4446-142">Processor</span></span>                              | <span data-ttu-id="d4446-143">Çıktı</span><span class="sxs-lookup"><span data-stu-id="d4446-143">Output</span></span>                 | <span data-ttu-id="d4446-144">Kaynak dosya</span><span class="sxs-lookup"><span data-stu-id="d4446-144">Source File</span></span>            |
| ------------------------ | -------------------------------------- | ---------------------- | ---------------------- |
| <span data-ttu-id="d4446-145">Sıcaklık veri iletisi</span><span class="sxs-lookup"><span data-stu-id="d4446-145">Temperature data message</span></span> | <span data-ttu-id="d4446-146">Ayrıştırma ve yeni bir JSON ileti oluşturun</span><span class="sxs-lookup"><span data-stu-id="d4446-146">Parse and construct a new JSON message</span></span> | <span data-ttu-id="d4446-147">Yapı JSON iletisi</span><span class="sxs-lookup"><span data-stu-id="d4446-147">Structure JSON message</span></span> | `ConverterModule.java` |

<span data-ttu-id="d4446-148">Bu modül tipik bir Azure IOT kenar modüldür.</span><span class="sxs-lookup"><span data-stu-id="d4446-148">This module is a typical Azure IoT Edge module.</span></span> <span data-ttu-id="d4446-149">Diğer modüllerden sıcaklık iletileri kabul eder (bir donanım modülü veya bu bizim benzetimli bırak modülü durumda); ve (Merhaba ileti kimliği, tootrigger hello sıcaklık uyarı ihtiyacımız hello özelliğini ayarlama ekleme de dahil olmak üzere vb.) yapılandırılmış tooa JSON iletinin hello sıcaklık iletiyi normalleştirir.</span><span class="sxs-lookup"><span data-stu-id="d4446-149">It accepts temperature messages from other modules (a hardware module, or in this case our simulated BLE module); and then normalizes hello temperature message in tooa structured JSON message (including appending hello message ID, setting hello property of whether we need tootrigger hello temperature alert, and so on).</span></span>

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

### <a name="printer-module"></a><span data-ttu-id="d4446-150">Yazıcı Modülü</span><span class="sxs-lookup"><span data-stu-id="d4446-150">Printer module</span></span>

| <span data-ttu-id="d4446-151">Girdi</span><span class="sxs-lookup"><span data-stu-id="d4446-151">Input</span></span>                          | <span data-ttu-id="d4446-152">İşlemci</span><span class="sxs-lookup"><span data-stu-id="d4446-152">Processor</span></span> | <span data-ttu-id="d4446-153">Çıktı</span><span class="sxs-lookup"><span data-stu-id="d4446-153">Output</span></span>                     | <span data-ttu-id="d4446-154">Kaynak dosya</span><span class="sxs-lookup"><span data-stu-id="d4446-154">Source File</span></span>          |
| ------------------------------ | --------- | -------------------------- | -------------------- |
| <span data-ttu-id="d4446-155">Diğer modüllerden herhangi bir iletisi</span><span class="sxs-lookup"><span data-stu-id="d4446-155">Any message from other modules</span></span> | <span data-ttu-id="d4446-156">Yok</span><span class="sxs-lookup"><span data-stu-id="d4446-156">N/A</span></span>       | <span data-ttu-id="d4446-157">Merhaba ileti tooconsole oturum</span><span class="sxs-lookup"><span data-stu-id="d4446-157">Log hello message tooconsole</span></span> | `PrinterModule.java` |

<span data-ttu-id="d4446-158">Bu, hello alınan iletileri toohello terminal penceresi çıkarır basit ve açıklayıcı, bir modüldür.</span><span class="sxs-lookup"><span data-stu-id="d4446-158">This is a simple, self-explanatory, module which outputs hello received messages toohello terminal window.</span></span>

```java
@Override
public void receive(Message message) {
  System.out.println(message.toString());
}
```

### <a name="azure-iot-edge-configuration"></a><span data-ttu-id="d4446-159">Azure IOT kenar yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d4446-159">Azure IoT Edge configuration</span></span>

<span data-ttu-id="d4446-160">Merhaba modülleri çalıştırmadan önce hello son tooconfigure hello Azure IOT kenarı ve modülleri arasında tooestablish hello bağlantıları adımdır.</span><span class="sxs-lookup"><span data-stu-id="d4446-160">hello final step before running hello modules is tooconfigure hello Azure IoT Edge and tooestablish hello connections between modules.</span></span>

<span data-ttu-id="d4446-161">Toodeclare tarafından başvurulan (itibaren Azure IOT kenar destekler yükleyicilerini farklı dillerde) bizim Java yükleyicisi ilk ihtiyacımız kendi `name` hello bölümlerde daha sonra.</span><span class="sxs-lookup"><span data-stu-id="d4446-161">First we need toodeclare our Java loader (since Azure IoT Edge supports loaders of different languages) which could be referenced by its `name` in hello sections afterward.</span></span>

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

<span data-ttu-id="d4446-162">Biz bizim yükleyicilerini bildirdikten sonra biz toodeclare bizim modüller de gerekir.</span><span class="sxs-lookup"><span data-stu-id="d4446-162">Once we have declared our loaders, we will also need toodeclare our modules as well.</span></span> <span data-ttu-id="d4446-163">Benzer toodeclaring hello yükleyicileri, bunlar ayrıca başvurulabilir tarafından kendi `name` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="d4446-163">Similar toodeclaring hello loaders, they can also be referenced by their `name` attribute.</span></span> <span data-ttu-id="d4446-164">Bir modül bildirirken (hangi önce tanımladığımız hello biri olmalıdır) kullanması gereken toospecify hello yükleyicisi ihtiyacımız ve -(bizim modülün hello normalleştirilmiş sınıf adı olmalıdır) için giriş noktası her modül hello.</span><span class="sxs-lookup"><span data-stu-id="d4446-164">When declaring a module, we need toospecify hello loader it should use (which should be hello one we defined before) and hello entry-point (should be hello normalized class name of our module) for each module.</span></span> <span data-ttu-id="d4446-165">Merhaba `simulated_device` hello Azure IOT kenar çekirdek çalışma zamanı paketinde bulunan bir yerel modül modülüdür.</span><span class="sxs-lookup"><span data-stu-id="d4446-165">hello `simulated_device` module is a native module which is included in hello Azure IoT Edge core runtime package.</span></span> <span data-ttu-id="d4446-166">Her zaman içermelidir `args` JSON dosyası, olsa bile hello içinde `null`.</span><span class="sxs-lookup"><span data-stu-id="d4446-166">You should always include `args` in hello JSON file even if it is `null`.</span></span>

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

<span data-ttu-id="d4446-167">Merhaba yapılandırma Hello sonunda hello bağlantı kurar.</span><span class="sxs-lookup"><span data-stu-id="d4446-167">At hello end of hello configuration, we establish hello connections.</span></span> <span data-ttu-id="d4446-168">Her bağlantı ile ifade edilen `source` ve `sink`.</span><span class="sxs-lookup"><span data-stu-id="d4446-168">Each connection is expressed by `source` and `sink`.</span></span> <span data-ttu-id="d4446-169">Önceden tanımlanmış bir modül her ikisi de başvurmalısınız.</span><span class="sxs-lookup"><span data-stu-id="d4446-169">They should both reference a pre-defined module.</span></span> <span data-ttu-id="d4446-170">Merhaba çıkış iletisini `source` modülü toohello girişi iletilir `sink` modülü.</span><span class="sxs-lookup"><span data-stu-id="d4446-170">hello output message of `source` module will be forwarded toohello input of `sink` module.</span></span>

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

## <a name="running-hello-modules"></a><span data-ttu-id="d4446-171">Çalışan hello modülleri</span><span class="sxs-lookup"><span data-stu-id="d4446-171">Running hello modules</span></span>

<span data-ttu-id="d4446-172">Kullanım `mvn package` toobuild hello içine her şeyi `target/` klasör.</span><span class="sxs-lookup"><span data-stu-id="d4446-172">Use `mvn package` toobuild everything into hello `target/` folder.</span></span> <span data-ttu-id="d4446-173">`mvn clean package`Ayrıca temiz bir yapı için tavsiye edilir.</span><span class="sxs-lookup"><span data-stu-id="d4446-173">`mvn clean package` is also recommended for a clean build.</span></span>

<span data-ttu-id="d4446-174">Kullanım `mvn exec:exec` toorun hello Azure IOT kenarı ve inceleyin hello sıcaklık veri ve tüm hello özellikler sabit oranı yazdırılan toohello konsolunda mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="d4446-174">Use `mvn exec:exec` toorun hello Azure IoT Edge and you should observe that hello temperature data and all hello properties are printed toohello console at a fixed rate.</span></span>

<span data-ttu-id="d4446-175">Tooterminate Merhaba uygulaması istiyorsanız basın `<Enter>` anahtarı.</span><span class="sxs-lookup"><span data-stu-id="d4446-175">If you want tooterminate hello application, press `<Enter>` key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d4446-176">Toouse Ctrl + C tooterminate hello IOT kenar önerilmez ağ geçidi uygulaması.</span><span class="sxs-lookup"><span data-stu-id="d4446-176">It is not recommended toouse Ctrl + C tooterminate hello IoT Edge gateway application.</span></span> <span data-ttu-id="d4446-177">Bu aşırı hello işlem tooterminate neden olarak.</span><span class="sxs-lookup"><span data-stu-id="d4446-177">As this may cause hello process tooterminate abnormally.</span></span>

