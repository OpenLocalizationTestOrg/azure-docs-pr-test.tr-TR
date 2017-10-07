---
title: Merhaba Java hizmet veri yolu API'si ile aaaHow toouse AMQP 1.0 | Microsoft Docs
description: "Nasıl toouse Java ileti hizmeti (JMS) Azure Service Bus ve Gelişmiş Message Queuing Protodol (AMQP) 1.0 ile Merhaba."
services: service-bus-messaging
documentationcenter: java
author: sethmanheim
manager: timlt
editor: 
ms.assetid: be766f42-6fd1-410c-b275-8c400c811519
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 3e1d0329f2675a2273e12bb7389d3ce38b156a5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-java-message-service-jms-api-with-service-bus-and-amqp-10"></a>Nasıl toouse hello Java ileti hizmeti (JMS) API Service Bus ve AMQP 1.0
Merhaba Gelişmiş Message Queuing Protokolü (AMQP) 1.0 toobuild güçlü, platformlar arası ileti uygulamaları kullanabilirsiniz verimli, güvenilir ve hat düzeyinde bir Mesajlaşma iletişim kuralıdır.

Hizmet kullanabileceğiniz anlamına gelir queuing hello ve yayımlama/aracılı Mesajlaşma özellikleri verimli bir ikili protokolünü kullanarak platformları aralığından abonelik veri yolu AMQP 1.0 için destek. Ayrıca, diller, çerçevelerinin ve işletim sistemlerinin bir karışımını kullanılarak oluşturulan bileşenlerden oluşan uygulamalar oluşturabilir.

Bu makalede, popüler Java ileti hizmeti (JMS) API standart toouse Service Bus Mesajlaşma özelliklerinden (kuyruklar ve yayımlama/abonelik konuları) kullanarak Java uygulamaları nasıl hello açıklanmaktadır. Var olan bir [yardımcı makale](service-bus-amqp-dotnet.md) nasıl toodo hello aynı hello Service Bus .NET API kullanarak açıklar. AMQP 1.0 kullanarak platformlar arası ileti gönderme hakkında şu iki kılavuzları birlikte toolearn kullanabilirsiniz.

## <a name="get-started-with-service-bus"></a>Service Bus’ı kullanmaya başlama
Bu kılavuz, adlandırılan bir kuyruğun içeren bir hizmet veri yolu ad alanı zaten sahip olduğunuzu varsayar **sıra 1**. Bunu yapmanız sonra şunları yapabilirsiniz [hello ad alanı ve Kuyruk oluşturma](service-bus-create-namespace-portal.md) hello kullanarak [Azure portal](https://portal.azure.com). Toocreate hizmet veri yolu ad alanları ve Kuyruklar nasıl görürüm hakkında daha fazla bilgi için [Service Bus kuyrukları ile çalışmaya başlama](service-bus-dotnet-get-started-with-queues.md).

> [!NOTE]
> Bölümlenmiş kuyruklar ve konu başlıkları da AMQP destekler. Daha fazla bilgi için bkz: [bölümlenmiş Mesajlaşma varlıkları](service-bus-partitioning.md) ve [hizmet veri yolu AMQP 1.0 desteği bölümlenmiş kuyruklar ve konu başlıkları](service-bus-partitioned-queues-and-topics-amqp-overview.md).
> 
> 

## <a name="downloading-hello-amqp-10-jms-client-library"></a>İndirme hello AMQP 1.0 JMS istemci kitaplığı
Burada toodownload hello hello Apache Qpid JMS AMQP 1.0 istemci kitaplığının en son sürümü hakkında daha fazla bilgi için [https://qpid.apache.org/download.html](https://qpid.apache.org/download.html).

Merhaba Apache Qpid JMS AMQP 1.0 dağıtım arşiv toohello ' Java sınıf oluşturma ve Service Bus ile JMS uygulamaları çalıştırırken aşağıdaki dört JAR dosyaları hello eklemeniz gerekir:

* geronimo jms\_1.1\_spec 1.0.jar
* qpid-amqp-1-0-client-[Version].jar
* qpid-amqp-1-0-Client-jms-[Version].jar
* qpid-amqp-1-0-Common-[Version].jar

## <a name="coding-java-applications"></a>Java uygulamalarını kodlama
### <a name="java-naming-and-directory-interface-jndi"></a>Java adlandırma ve dizini arabirimi (JNDI)
JMS hello Java adlandırma ve dizin arabirimi (JNDI) toocreate mantıksal ve fiziksel adlarını arasında ayrım kullanır. İki tür JMS nesneleri JNDI kullanarak çözümlenir: ConnectionFactory ve hedef. JNDI farklı dizin hizmetleri toohandle ad çözümleme görevlerini ekleyebilirsiniz sağlayıcı modeli kullanır. Merhaba Apache Qpid JMS AMQP 1.0 kitaplığı basit özellikleri ile birlikte gelen dosya tabanlı JNDI hello aşağıdaki özellikleri dosyası kullanılarak yapılandırılmış sağlayıcısı biçimi:

```
# servicebus.properties - sample JNDI configuration

# Register a ConnectionFactory in JNDI using hello form:
# connectionfactory.[jndi_name] = [ConnectionURL]
connectionfactory.SBCF = amqps://[SASPolicyName]:[SASPolicyKey]@[namespace].servicebus.windows.net

# Register some queues in JNDI using hello form
# queue.[jndi_name] = [physical_name]
# topic.[jndi_name] = [physical_name]
queue.QUEUE = queue1
```

#### <a name="configure-hello-connectionfactory"></a>Merhaba ConnectionFactory yapılandırın
kullanılan girdisi toodefine hello bir **ConnectionFactory** hello Qpid özellikleri dosya JNDI biçimini izleyen Merhaba sağlayıcısıdır:

```
connectionfactory.[jndi_name] = [ConnectionURL]
```

Burada **[jndi_name]** ve **[ConnectionURL]** anlamları aşağıdaki hello vardır:

* **[jndi_name]** : Merhaba ConnectionFactory hello mantıksal adı. Bu, Merhaba Java uygulaması hello JNDI IntialContext.lookup() yöntemini kullanarak çözümlenir hello addır.
* **[ConnectionURL]** : Hello bilgilerle hello JMS kitaplığı sağlayan bir URL gerekli toohello AMQP Aracısı.

Merhaba Hello biçimi **ConnectionURL** aşağıdaki gibidir:

```
amqps://[SASPolicyName]:[SASPolicyKey]@[namespace].servicebus.windows.net
```
Burada **[ad]**, **[SASPolicyName]** ve **[SASPolicyKey]** anlamları aşağıdaki hello vardır:

* **[ad]** : Service Bus ad alanı hello.
* **[SASPolicyName]** : hello sıra paylaşılan erişim imzası ilke adı.
* **[SASPolicyKey]** : hello sıra paylaşılan erişim imzası ilke anahtarı.

> [!NOTE]
> URL kodlama hello parola el ile gerekir. URL kodlaması yararlı bir yardımcı şu adresten edinilebilir [http://www.w3schools.com/tags/ref_urlencode.asp](http://www.w3schools.com/tags/ref_urlencode.asp).
> 
> 

#### <a name="configure-destinations"></a>Hedeflerini yapılandırma
Merhaba giriş biçimini izleyen Merhaba hello Qpid özellikleri dosya JNDI sağlayıcısında bir hedefi olan toodefine kullanılır:

```
queue.[jndi_name] = [physical_name]
```

or

```
topic.[jndi_name] = [physical_name]
```

Burada **[JNDI\_adı]** ve **[fiziksel\_adı]** anlamları aşağıdaki hello vardır:

* **[jndi_name]** : hello hedef hello mantıksal adı. Bu, Merhaba Java uygulaması hello JNDI IntialContext.lookup() yöntemini kullanarak çözümlenir hello addır.
* **[physical_name]** : hello Service Bus varlık toowhich Merhaba uygulaması hello adını gönderir veya iletilerini alır.

> [!NOTE]
> Bir hizmet veri yolu konusu abonelikten alırken hello fiziksel ad JNDI içinde belirtilen hello konunun hello adı olmalıdır. Merhaba dayanıklı abonelik hello JMS uygulama kodu oluşturulduğunda hello abonelik adı sağlanır. Merhaba [hizmet veri yolu AMQP 1.0 Geliştirici Kılavuzu](service-bus-amqp-dotnet.md) JMS Service Bus konularından ile çalışma hakkında daha fazla ayrıntı sağlar.
> 
> 

### <a name="write-hello-jms-application"></a>Merhaba JMS uygulaması yazma
Özel API'leri veya JMS Service Bus ile kullanırken gereken seçenekler yok. Ancak, daha sonra ele alınacak bazı kısıtlamalar vardır. Herhangi bir JMS uygulama ile Merhaba JNDI ortamının, toobe mümkün tooresolve yapılandırması hello ilk şey gerekli olduğu gibi bir **ConnectionFactory** ve hedefler.

#### <a name="configure-hello-jndi-initialcontext"></a>Merhaba JNDI InitialContext yapılandırın
Merhaba JNDI ortamı hello javax.naming.InitialContext sınıfı hello oluşturucuya yapılandırma bilgilerini bir hashtable geçirerek yapılandırılır. Merhaba iki gerekli hello hashtable içinde hello ilk bağlam fabrikası hello sınıf adını ve hello sağlayıcısı URL öğelerdir. Merhaba aşağıdaki kod nasıl tooconfigure hello JNDI ortam toouse hello Qpid özellikleri dosya adlı bir özellik dosyası JNDI sağlayıcı tabanlı gösterir **servicebus.properties**.

```java
Hashtable<String, String> env = new Hashtable<String, String>(); 
env.put(Context.INITIAL_CONTEXT_FACTORY, "org.apache.qpid.amqp_1_0.jms.jndi.PropertiesFileInitialContextFactory"); 
env.put(Context.PROVIDER_URL, "servicebus.properties"); 
InitialContext context = new InitialContext(env);
``` 

### <a name="a-simple-jms-application-using-a-service-bus-queue"></a>Service Bus kuyruğu kullanarak basit bir JMS uygulama
Merhaba aşağıdaki örnek program JMS TextMessages tooa Service Bus kuyruğuna sırasının hello JNDI mantıksal adı ile gönderir ve hello iletilerini geri alır.

```java
// SimpleSenderReceiver.java

import javax.jms.*;
import javax.naming.Context;
import javax.naming.InitialContext;
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.Hashtable;
import java.util.Random;

public class SimpleSenderReceiver implements MessageListener {
    private static boolean runReceiver = true;
    private Connection connection;
    private Session sendSession;
    private Session receiveSession;
    private MessageProducer sender;
    private MessageConsumer receiver;
    private static Random randomGenerator = new Random();

    public SimpleSenderReceiver() throws Exception {
        // Configure JNDI environment
        Hashtable<String, String> env = new Hashtable<String, String>();
        env.put(Context.INITIAL_CONTEXT_FACTORY, 
                   "org.apache.qpid.amqp_1_0.jms.jndi.PropertiesFileInitialContextFactory");
        env.put(Context.PROVIDER_URL, "servicebus.properties");
        Context context = new InitialContext(env);

        // Look up ConnectionFactory and Queue
        ConnectionFactory cf = (ConnectionFactory) context.lookup("SBCF");
        Destination queue = (Destination) context.lookup("QUEUE");

        // Create Connection
        connection = cf.createConnection();

        // Create sender-side Session and MessageProducer
        sendSession = connection.createSession(false, Session.AUTO_ACKNOWLEDGE);
        sender = sendSession.createProducer(queue);

        if (runReceiver) {
            // Create receiver-side Session, MessageConsumer,and MessageListener
            receiveSession = connection.createSession(false, Session.CLIENT_ACKNOWLEDGE);
            receiver = receiveSession.createConsumer(queue);
            receiver.setMessageListener(this);
            connection.start();
        }
    }

    public static void main(String[] args) {
        try {

            if ((args.length > 0) && args[0].equalsIgnoreCase("sendonly")) {
                runReceiver = false;
            }

            SimpleSenderReceiver simpleSenderReceiver = new SimpleSenderReceiver();
            System.out.println("Press [enter] toosend a message. Type 'exit' + [enter] tooquit.");
            BufferedReader commandLine = new java.io.BufferedReader(new InputStreamReader(System.in));

            while (true) {
                String s = commandLine.readLine();
                if (s.equalsIgnoreCase("exit")) {
                    simpleSenderReceiver.close();
                    System.exit(0);
                } else {
                    simpleSenderReceiver.sendMessage();
                }
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    private void sendMessage() throws JMSException {
        TextMessage message = sendSession.createTextMessage();
        message.setText("Test AMQP message from JMS");
        long randomMessageID = randomGenerator.nextLong() >>>1;
        message.setJMSMessageID("ID:" + randomMessageID);
        sender.send(message);
        System.out.println("Sent message with JMSMessageID = " + message.getJMSMessageID());
    }

    public void close() throws JMSException {
        connection.close();
    }

    public void onMessage(Message message) {
        try {
            System.out.println("Received message with JMSMessageID = " + message.getJMSMessageID());
            message.acknowledge();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}    
```

### <a name="run-hello-application"></a>Merhaba uygulamayı çalıştırın
Merhaba uygulaması çalıştıran hello formunun bir çıktı üretir:

```
> java SimpleSenderReceiver
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.

Sent message with JMSMessageID = ID:2867600614942270318
Received message with JMSMessageID = ID:2867600614942270318

Sent message with JMSMessageID = ID:7578408152750301483
Received message with JMSMessageID = ID:7578408152750301483

Sent message with JMSMessageID = ID:956102171969368961
Received message with JMSMessageID = ID:956102171969368961
exit
```

## <a name="cross-platform-messaging-between-jms-and-net"></a>Platformlar arası ileti JMS ve .NET arasında
Bu kılavuz nasıl oluşturulacağını gösterir toosend ve hizmet JMS kullanarak veri yolundan iletileri tooand alırsınız. Ancak, hello avantajları AMQP 1.0 güvenilir bir şekilde ve tam bir güvenilirlik, alınıp iletilerle farklı dillerde yazılmış Bileşenler'den yerleşik uygulamaları toobe etkinleştirir biridir.

Yukarıda açıklanan hello örnek JMS uygulama ve yardımcı makaleden gerçekleştirilecek benzer bir .NET uygulaması kullanarak [kullanarak Service Bus .NET AMQP 1.0 ile birlikte gelen](service-bus-amqp-dotnet.md), .NET ve Java arasında iletileri değiştirebilir. Platformlar arası Service Bus ve AMQP 1.0 kullanarak Mesajlaşma, hello ayrıntıları hakkında daha fazla bilgi için bu makaleyi okuyun.

### <a name="jms-toonet"></a>JMS too.NET
toodemonstrate JMS too.NET ileti:

* Tüm komut satırı bağımsız değişkenleri olmadan Merhaba .NET örnek uygulaması başlatın.
* Merhaba Java örnek uygulaması hello "sendonly" komut satırı bağımsız değişkeniyle başlatın. Bu modda, hello uygulama hello kuyruktan iletileri almaz, yalnızca gönderir.
* Tuşuna **Enter** birkaç kez hello Java uygulama konsolunda neden olacak gönderilen iletileri toobe.
* Bu iletiler hello .NET uygulaması tarafından alınır.

#### <a name="output-from-jms-application"></a>JMS uygulama çıktısı
```
> java SimpleSenderReceiver sendonly
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Sent message with JMSMessageID = ID:4364096528752411591
Sent message with JMSMessageID = ID:459252991689389983
Sent message with JMSMessageID = ID:1565011046230456854
exit
```

#### <a name="output-from-net-application"></a>.NET uygulaması çıktısı
```
> SimpleSenderReceiver.exe    
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Received message with MessageID = 4364096528752411591
Received message with MessageID = 459252991689389983
Received message with MessageID = 1565011046230456854
exit
```

### <a name="net-toojms"></a>.NET tooJMS
toodemonstrate .NET tooJMS ileti:

* Merhaba .NET örnek uygulaması hello "sendonly" komut satırı bağımsız değişkeniyle başlatın. Bu modda, hello uygulama hello kuyruktan iletileri almaz, yalnızca gönderir.
* Tüm komut satırı bağımsız değişkenleri olmadan Hello Java örnek uygulamayı başlatın.
* Tuşuna **Enter** birkaç kez hello .NET uygulama konsolunda neden olacak gönderilen iletileri toobe.
* Bu iletiler hello Java uygulaması tarafından alınır.

#### <a name="output-from-net-application"></a>.NET uygulaması çıktısı
```
> SimpleSenderReceiver.exe sendonly
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Sent message with MessageID = d64e681a310a48a1ae0ce7b017bf1cf3    
Sent message with MessageID = 98a39664995b4f74b32e2a0ecccc46bb
Sent message with MessageID = acbca67f03c346de9b7893026f97ddeb
exit
```

#### <a name="output-from-jms-application"></a>JMS uygulama çıktısı
```
> java SimpleSenderReceiver    
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Received message with JMSMessageID = ID:d64e681a310a48a1ae0ce7b017bf1cf3
Received message with JMSMessageID = ID:98a39664995b4f74b32e2a0ecccc46bb
Received message with JMSMessageID = ID:acbca67f03c346de9b7893026f97ddeb
exit
```

## <a name="unsupported-features-and-restrictions"></a>Desteklenmeyen özellikler ve kısıtlamalar
kısıtlamaları aşağıdaki hello JMS Service Bus ile AMQP 1.0 üzerinden öğesine kullanırken mevcuttur:

* Yalnızca bir **MessageProducer** veya **MessageConsumer** başına izin verilen **oturum**. Toocreate gerekiyorsa birden çok **MessageProducers** veya **MessageConsumers** bir uygulamada, ayrılmış bir oluşturma **oturum** her biri için.
* Volatile konu abonelikleri şu anda desteklenmemektedir.
* **MessageSelectors** şu anda desteklenmiyor.
* Geçici hedefleri; Örneğin, **TemporaryQueue**, **TemporaryTopic** şu anda, birlikte hello desteklenmemektedir **QueueRequestor** ve **TopicRequestor**Kullanılacakları API'leri.
* Uygulaması yapılan oturumlar ve dağıtılmış işlemler desteklenmiyor.

## <a name="summary"></a>Özet
Bu nasıl tooguide nasıl Java kullanarak toouse Service Bus aracılı Mesajlaşma özellikleri (kuyruklar ve yayımlama/abonelik konuları) popüler JMS API ve AMQP 1.0 hello gösterdi.

Hizmet veri yolu AMQP 1.0 .NET, C, Python ve PHP gibi diğer dillerden de kullanabilirsiniz. Bu farklı diller kullanılarak oluşturulan bileşenleri, güvenilir ve hizmet veri yolundaki kullanılarak hello AMQP 1.0 desteği tam uygunluğunu iletileri değiştirebilir.

## <a name="next-steps"></a>Sonraki adımlar
* [Azure hizmet veri yolu AMQP 1.0 desteği](service-bus-amqp-overview.md)
* [Nasıl toouse AMQP 1.0 ile Merhaba Service Bus .NET API](service-bus-dotnet-advanced-message-queuing.md)
* [Hizmet veri yolu AMQP 1.0 Geliştirici Kılavuzu](service-bus-amqp-dotnet.md)
* [Service Bus kuyrukları ile çalışmaya başlama](service-bus-dotnet-get-started-with-queues.md)
* [Java Geliştirici Merkezi](https://azure.microsoft.com/develop/java/)

