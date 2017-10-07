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
# <a name="create-an-azure-iot-edge-module-with-java"></a>Java ile Azure IOT kenar modülü oluşturun

Bu öğretici bir Java Azure IOT sınır için bir modül nasıl oluşturabilir gösterir.

Bu öğreticide, ortamı kurulumu aracılığıyla size yol gösterir ve nasıl toowrite bir [bırak](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) veri dönüştürücü modülü hello en son Azure IOT kenar Maven paketleri kullanma.

## <a name="prerequisites"></a>Ön koşullar

Bu bölümde IOT kenar modülü geliştirme ortamınızı ayarlayacaksınız. Tooboth geçerlidir *64-bit Windows* ve *64-bit Linux (Ubuntu/Debian 8)* işletim sistemleri.

yazılımı aşağıdaki hello gereklidir:

* [Git istemci](https://git-scm.com/downloads).
* [**x64** JDK](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).
* [Maven](https://maven.apache.org/install.html).

Depo izleyen bir komut satırı terminal penceresi ve kopya hello açın:

1. `git clone https://github.com/Azure-Samples/iot-edge-samples.git`.
2. `cd iot-edge-samples/java/simulated_ble`

## <a name="overall-architecture"></a>Genel mimari

Hello Azure IOT kenar platform yoğun hello uyarlar [Von Neumann mimarisi](https://en.wikipedia.org/wiki/Von_Neumann_architecture). Bu hello tüm Azure IOT kenar mimarisi anlamına gelir, işleyen giriş ve çıkışı üretir bir sistemdir; ve tek tek her modül küçük bir giriş-çıkış alt olduğunu. Bu öğreticide, şu iki modülleri aşağıdaki hello getirir:

1. Sanal alan bir modül [bırak](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) sinyal ve biçimlendirilmiş dönüştürür [JSON](https://en.wikipedia.org/wiki/JSON) ileti.
2. Alınan hello yazdırır bir modül [JSON](https://en.wikipedia.org/wiki/JSON) ileti.

Merhaba aşağıdaki görüntüde hello tipik uçtan uca veri akışı bu proje için görüntüler:

![Veri akışı üç modülleri arasında](media/iot-hub-iot-edge-create-module/dataflow.png "giriş: benzetimli bırak Modülü; İşlemci: Dönüştürücü Modülü; Çıktı: Yazıcı Modülü")

## <a name="understanding-hello-code"></a>Merhaba kodu anlama

### <a name="maven-project-structure"></a>Maven projesi yapısı

Azure IOT kenar paketleri Maven üzerinde dayandığından, toocreate içeren tipik bir Maven projesi yapısı ihtiyacımız bir `pom.xml` dosyası.

Merhaba POM devralır hello `com.microsoft.azure.gateway.gateway-module-base` tüm hello çalışma zamanı ikili dosyaları, hello ağ geçidi yapılandırma dosyası yolu ve hello yürütme davranışı içeren bir modülü projesi tarafından gerekli hello bağımlılıklarını bildirir paket. Bu bize çok fazla kaydeder ve hello gerek toowrite ortadan kaldırmak ve kod satırlarını yüzlerce tekrar tekrar yeniden yazın.

Merhaba gerekli bağımlılıkları/eklenti ve hello aşağıdaki kod parçacığında gösterildiği gibi bizim modülü tarafından kullanılan hello yapılandırma dosyası toobe hello adını bildirerek tooupdate pom.xml dosyasını ihtiyacımız var.

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

### <a name="basic-understanding-of-an-azure-iot-edge-module"></a>Bir Azure IOT kenar modülün temel anlama

Bir veri işleri için işlemci olarak Azure IOT kenar modülü davranabilirsiniz: girişi almak, işlemesi ve çıktı üretir.

Merhaba giriş donanım (gibi hareket algılayıcısı) verileri, bir ileti diğer modüller ya da (örneğin, düzenli aralıklarla bir Zamanlayıcı tarafından oluşturulan bir rastgele sayı) başka bir şey olabilir.

Merhaba çıkış benzer toohello giriş, donanım davranış (gibi hello ışığı yanıp sönen), bir ileti tooother modülleri ya da (yazdırma toohello konsolu gibi) başka bir şey tetikleyebilir.

Modüller birbirleri ile kullanarak iletişim `com.microsoft.azure.gateway.messaging.Message` sınıfı. Merhaba **içerik** , bir `Message` istediğiniz verilerin herhangi bir tür temsil etme işleyebilen bir bayt dizisi. **Özellikler** de hello kullanılabilir `Message` ve yalnızca bir dize-dize eşleme. Düşünebilirsiniz **özellikleri** bir HTTP isteğinin ya da hello meta veri dosyasının hello başlığı olarak.

Sipariş toodevelop Java Azure IOT kenar modülünde'da, toocreate devraldığı yeni bir modül sınıf gereken `com.microsoft.azure.gateway.core.GatewayModule` ve gerekli hello soyut yöntemleri uygulamak `receive()` ve `destroy()`. Bu noktada, ayrıca isteğe bağlı tooimplement hello tercih edebilirsiniz `start()` veya `create()` de yöntemleri. Aşağıdaki kod parçacığını hello Azure IOT kenar modülü yazma tooget nasıl başlatılacağını gösterir.

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

### <a name="converter-module"></a>Dönüştürücü Modülü

| Girdi                    | İşlemci                              | Çıktı                 | Kaynak dosya            |
| ------------------------ | -------------------------------------- | ---------------------- | ---------------------- |
| Sıcaklık veri iletisi | Ayrıştırma ve yeni bir JSON ileti oluşturun | Yapı JSON iletisi | `ConverterModule.java` |

Bu modül tipik bir Azure IOT kenar modüldür. Diğer modüllerden sıcaklık iletileri kabul eder (bir donanım modülü veya bu bizim benzetimli bırak modülü durumda); ve (Merhaba ileti kimliği, tootrigger hello sıcaklık uyarı ihtiyacımız hello özelliğini ayarlama ekleme de dahil olmak üzere vb.) yapılandırılmış tooa JSON iletinin hello sıcaklık iletiyi normalleştirir.

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

### <a name="printer-module"></a>Yazıcı Modülü

| Girdi                          | İşlemci | Çıktı                     | Kaynak dosya          |
| ------------------------------ | --------- | -------------------------- | -------------------- |
| Diğer modüllerden herhangi bir iletisi | Yok       | Merhaba ileti tooconsole oturum | `PrinterModule.java` |

Bu, hello alınan iletileri toohello terminal penceresi çıkarır basit ve açıklayıcı, bir modüldür.

```java
@Override
public void receive(Message message) {
  System.out.println(message.toString());
}
```

### <a name="azure-iot-edge-configuration"></a>Azure IOT kenar yapılandırma

Merhaba modülleri çalıştırmadan önce hello son tooconfigure hello Azure IOT kenarı ve modülleri arasında tooestablish hello bağlantıları adımdır.

Toodeclare tarafından başvurulan (itibaren Azure IOT kenar destekler yükleyicilerini farklı dillerde) bizim Java yükleyicisi ilk ihtiyacımız kendi `name` hello bölümlerde daha sonra.

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

Biz bizim yükleyicilerini bildirdikten sonra biz toodeclare bizim modüller de gerekir. Benzer toodeclaring hello yükleyicileri, bunlar ayrıca başvurulabilir tarafından kendi `name` özniteliği. Bir modül bildirirken (hangi önce tanımladığımız hello biri olmalıdır) kullanması gereken toospecify hello yükleyicisi ihtiyacımız ve -(bizim modülün hello normalleştirilmiş sınıf adı olmalıdır) için giriş noktası her modül hello. Merhaba `simulated_device` hello Azure IOT kenar çekirdek çalışma zamanı paketinde bulunan bir yerel modül modülüdür. Her zaman içermelidir `args` JSON dosyası, olsa bile hello içinde `null`.

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

Merhaba yapılandırma Hello sonunda hello bağlantı kurar. Her bağlantı ile ifade edilen `source` ve `sink`. Önceden tanımlanmış bir modül her ikisi de başvurmalısınız. Merhaba çıkış iletisini `source` modülü toohello girişi iletilir `sink` modülü.

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

## <a name="running-hello-modules"></a>Çalışan hello modülleri

Kullanım `mvn package` toobuild hello içine her şeyi `target/` klasör. `mvn clean package`Ayrıca temiz bir yapı için tavsiye edilir.

Kullanım `mvn exec:exec` toorun hello Azure IOT kenarı ve inceleyin hello sıcaklık veri ve tüm hello özellikler sabit oranı yazdırılan toohello konsolunda mevcuttur.

Tooterminate Merhaba uygulaması istiyorsanız basın `<Enter>` anahtarı.

> [!IMPORTANT]
> Toouse Ctrl + C tooterminate hello IOT kenar önerilmez ağ geçidi uygulaması. Bu aşırı hello işlem tooterminate neden olarak.

