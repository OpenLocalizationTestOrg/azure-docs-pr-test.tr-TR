---
title: AMQP 1.0 Java hizmet veri yolu API'si ile kullanma | Microsoft Docs
description: "Java ileti hizmeti (JMS) Azure Service Bus ve Gelişmiş Message Queuing Protodol (AMQP) 1.0 ile nasıl kullanılır."
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
ms.openlocfilehash: 0848facd764c4fb0d7f95c1ae89ecb02a32257e1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-the-java-message-service-jms-api-with-service-bus-and-amqp-10"></a><span data-ttu-id="3b3ff-103">Hizmet veri yolu AMQP 1.0 ile Java ileti hizmeti (JMS) API kullanma</span><span class="sxs-lookup"><span data-stu-id="3b3ff-103">How to use the Java Message Service (JMS) API with Service Bus and AMQP 1.0</span></span>
<span data-ttu-id="3b3ff-104">Gelişmiş Message Queuing Protokolü (AMQP) 1.0, güçlü, platformlar arası ileti uygulamaları oluşturmak için kullanabileceğiniz bir verimli, güvenilir ve hat düzeyinde Mesajlaşma protokolüdür.</span><span class="sxs-lookup"><span data-stu-id="3b3ff-104">The Advanced Message Queuing Protocol (AMQP) 1.0 is an efficient, reliable, wire-level messaging protocol that you can use to build robust, cross-platform messaging applications.</span></span>

<span data-ttu-id="3b3ff-105">Destek için hizmet veri yolu AMQP 1.0 queuing kullanın ve yayımlama/aracılı Mesajlaşma özellikleri verimli bir ikili protokolünü kullanarak platformları aralığından abonelik anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="3b3ff-105">Support for AMQP 1.0 in Service Bus means that you can use the queuing and publish/subscribe brokered messaging features from a range of platforms using an efficient binary protocol.</span></span> <span data-ttu-id="3b3ff-106">Ayrıca, diller, çerçevelerinin ve işletim sistemlerinin bir karışımını kullanılarak oluşturulan bileşenlerden oluşan uygulamalar oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="3b3ff-106">Furthermore, you can build applications comprised of components built using a mix of languages, frameworks, and operating systems.</span></span>

<span data-ttu-id="3b3ff-107">Bu makalede, popüler Java ileti hizmeti (JMS) API standart kullanarak Java uygulamalardan nasıl Service Bus (kuyruklar ve konu başlıkları Yayınla/Abone ol) özellikleri Mesajlaşma kullanılacağı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="3b3ff-107">This article explains how to use Service Bus messaging features (queues and publish/subscribe topics) from Java applications using the popular Java Message Service (JMS) API standard.</span></span> <span data-ttu-id="3b3ff-108">Var olan bir [yardımcı makale](service-bus-amqp-dotnet.md) , hizmet veri yolu .NET API kullanarak aynı şeyi açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="3b3ff-108">There is a [companion article](service-bus-amqp-dotnet.md) that explains how to do the same using the Service Bus .NET API.</span></span> <span data-ttu-id="3b3ff-109">AMQP 1.0 kullanarak platformlar arası ileti hakkında bilgi edinmek için bu iki kılavuzları birlikte kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3b3ff-109">You can use these two guides together to learn about cross-platform messaging using AMQP 1.0.</span></span>

## <a name="get-started-with-service-bus"></a><span data-ttu-id="3b3ff-110">Service Bus’ı kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="3b3ff-110">Get started with Service Bus</span></span>
<span data-ttu-id="3b3ff-111">Bu kılavuz, adlandırılan bir kuyruğun içeren bir hizmet veri yolu ad alanı zaten sahip olduğunuzu varsayar **sıra 1**.</span><span class="sxs-lookup"><span data-stu-id="3b3ff-111">This guide assumes that you already have a Service Bus namespace containing a queue named **queue1**.</span></span> <span data-ttu-id="3b3ff-112">Bunu yapmanız sonra şunları yapabilirsiniz [ad alanı oluşturup sıra](service-bus-create-namespace-portal.md) kullanarak [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3b3ff-112">If you do not, then you can [create the namespace and queue](service-bus-create-namespace-portal.md) using the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="3b3ff-113">Hizmet veri yolu ad alanları ve Kuyruklar oluşturma hakkında daha fazla bilgi için bkz: [Service Bus kuyrukları ile çalışmaya başlama](service-bus-dotnet-get-started-with-queues.md).</span><span class="sxs-lookup"><span data-stu-id="3b3ff-113">For more information about how to create Service Bus namespaces and queues, see [Get started with Service Bus queues](service-bus-dotnet-get-started-with-queues.md).</span></span>

> [!NOTE]
> <span data-ttu-id="3b3ff-114">Bölümlenmiş kuyruklar ve konu başlıkları da AMQP destekler.</span><span class="sxs-lookup"><span data-stu-id="3b3ff-114">Partitioned queues and topics also support AMQP.</span></span> <span data-ttu-id="3b3ff-115">Daha fazla bilgi için bkz: [bölümlenmiş Mesajlaşma varlıkları](service-bus-partitioning.md) ve [hizmet veri yolu AMQP 1.0 desteği bölümlenmiş kuyruklar ve konu başlıkları](service-bus-partitioned-queues-and-topics-amqp-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3b3ff-115">For more information, see [Partitioned messaging entities](service-bus-partitioning.md) and [AMQP 1.0 support for Service Bus partitioned queues and topics](service-bus-partitioned-queues-and-topics-amqp-overview.md).</span></span>
> 
> 

## <a name="downloading-the-amqp-10-jms-client-library"></a><span data-ttu-id="3b3ff-116">AMQP 1.0 JMS istemci kitaplığı indirme</span><span class="sxs-lookup"><span data-stu-id="3b3ff-116">Downloading the AMQP 1.0 JMS client library</span></span>
<span data-ttu-id="3b3ff-117">Apache Qpid JMS AMQP 1.0 istemci kitaplığının en son sürümü karşıdan yükleme konumu hakkında daha fazla bilgi için ziyaret [https://qpid.apache.org/download.html](https://qpid.apache.org/download.html).</span><span class="sxs-lookup"><span data-stu-id="3b3ff-117">For information about where to download the latest version of the Apache Qpid JMS AMQP 1.0 client library, visit [https://qpid.apache.org/download.html](https://qpid.apache.org/download.html).</span></span>

<span data-ttu-id="3b3ff-118">Aşağıdaki dört JAR dosyalarını Apache Qpid JMS AMQP 1.0 dağıtım arşivinden Java sınıf oluşturma ve Service Bus ile JMS uygulamaları çalıştırırken eklemeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="3b3ff-118">You must add the following four JAR files from the Apache Qpid JMS AMQP 1.0 distribution archive to the Java CLASSPATH when building and running JMS applications with Service Bus:</span></span>

* <span data-ttu-id="3b3ff-119">geronimo jms\_1.1\_spec 1.0.jar</span><span class="sxs-lookup"><span data-stu-id="3b3ff-119">geronimo-jms\_1.1\_spec-1.0.jar</span></span>
* <span data-ttu-id="3b3ff-120">qpid-amqp-1-0-client-[Version].jar</span><span class="sxs-lookup"><span data-stu-id="3b3ff-120">qpid-amqp-1-0-client-[version].jar</span></span>
* <span data-ttu-id="3b3ff-121">qpid-amqp-1-0-Client-jms-[Version].jar</span><span class="sxs-lookup"><span data-stu-id="3b3ff-121">qpid-amqp-1-0-client-jms-[version].jar</span></span>
* <span data-ttu-id="3b3ff-122">qpid-amqp-1-0-Common-[Version].jar</span><span class="sxs-lookup"><span data-stu-id="3b3ff-122">qpid-amqp-1-0-common-[version].jar</span></span>

## <a name="coding-java-applications"></a><span data-ttu-id="3b3ff-123">Java uygulamalarını kodlama</span><span class="sxs-lookup"><span data-stu-id="3b3ff-123">Coding Java applications</span></span>
### <a name="java-naming-and-directory-interface-jndi"></a><span data-ttu-id="3b3ff-124">Java adlandırma ve dizini arabirimi (JNDI)</span><span class="sxs-lookup"><span data-stu-id="3b3ff-124">Java Naming and Directory Interface (JNDI)</span></span>
<span data-ttu-id="3b3ff-125">JMS, mantıksal ve fiziksel adlarını arasında ayrım oluşturmak için Java adlandırma ve dizin arabirimi (JNDI) kullanır.</span><span class="sxs-lookup"><span data-stu-id="3b3ff-125">JMS uses the Java Naming and Directory Interface (JNDI) to create a separation between logical names and physical names.</span></span> <span data-ttu-id="3b3ff-126">İki tür JMS nesneleri JNDI kullanarak çözümlenir: ConnectionFactory ve hedef.</span><span class="sxs-lookup"><span data-stu-id="3b3ff-126">Two types of JMS objects are resolved using JNDI: ConnectionFactory and Destination.</span></span> <span data-ttu-id="3b3ff-127">JNDI ad çözümleme görevlerini işlemek için farklı dizin hizmetleri ekleyebilirsiniz sağlayıcı modeli kullanır.</span><span class="sxs-lookup"><span data-stu-id="3b3ff-127">JNDI uses a provider model into which you can plug different directory services to handle name resolution duties.</span></span> <span data-ttu-id="3b3ff-128">Dosya tabanlı JNDI aşağıdaki özellikleri dosyası kullanılarak yapılandırılmış sağlayıcısı kitaplığı basit özellikleri ile birlikte gelen Apache Qpid JMS AMQP 1.0 Biçimlendir:</span><span class="sxs-lookup"><span data-stu-id="3b3ff-128">The Apache Qpid JMS AMQP 1.0 library comes with a simple properties file-based JNDI Provider that is configured using a properties file of the following format:</span></span>

```
# servicebus.properties - sample JNDI configuration

# Register a ConnectionFactory in JNDI using the form:
# connectionfactory.[jndi_name] = [ConnectionURL]
connectionfactory.SBCF = amqps://[SASPolicyName]:[SASPolicyKey]@[namespace].servicebus.windows.net

# Register some queues in JNDI using the form
# queue.[jndi_name] = [physical_name]
# topic.[jndi_name] = [physical_name]
queue.QUEUE = queue1
```

#### <a name="configure-the-connectionfactory"></a><span data-ttu-id="3b3ff-129">ConnectionFactory yapılandırın</span><span class="sxs-lookup"><span data-stu-id="3b3ff-129">Configure the ConnectionFactory</span></span>
<span data-ttu-id="3b3ff-130">Girişi tanımlamak için kullanılan bir **ConnectionFactory** Qpid özellikleri JNDI sağlayıcısı şu biçimde dosyasıdır:</span><span class="sxs-lookup"><span data-stu-id="3b3ff-130">The entry used to define a **ConnectionFactory** in the Qpid properties file JNDI provider is of the following format:</span></span>

```
connectionfactory.[jndi_name] = [ConnectionURL]
```

<span data-ttu-id="3b3ff-131">Burada **[jndi_name]** ve **[ConnectionURL]** şu anlama gelir:</span><span class="sxs-lookup"><span data-stu-id="3b3ff-131">Where **[jndi_name]** and **[ConnectionURL]** have the following meanings:</span></span>

* <span data-ttu-id="3b3ff-132">**[jndi_name]** : ConnectionFactory mantıksal adı.</span><span class="sxs-lookup"><span data-stu-id="3b3ff-132">**[jndi_name]**: The logical name of the ConnectionFactory.</span></span> <span data-ttu-id="3b3ff-133">Bu, JNDI IntialContext.lookup() yöntemini kullanarak Java uygulamasında çözümlenir addır.</span><span class="sxs-lookup"><span data-stu-id="3b3ff-133">This is the name that will be resolved in the Java application using the JNDI IntialContext.lookup() method.</span></span>
* <span data-ttu-id="3b3ff-134">**[ConnectionURL]** : JMS kitaplığı AMQP aracısı için gereken bilgileri sağlayan bir URL.</span><span class="sxs-lookup"><span data-stu-id="3b3ff-134">**[ConnectionURL]**: A URL that provides the JMS library with the information required to the AMQP broker.</span></span>

<span data-ttu-id="3b3ff-135">Biçimi **ConnectionURL** aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="3b3ff-135">The format of the **ConnectionURL** is as follows:</span></span>

```
amqps://[SASPolicyName]:[SASPolicyKey]@[namespace].servicebus.windows.net
```
<span data-ttu-id="3b3ff-136">Burada **[ad]**, **[SASPolicyName]** ve **[SASPolicyKey]** şu anlama gelir:</span><span class="sxs-lookup"><span data-stu-id="3b3ff-136">Where **[namespace]**, **[SASPolicyName]** and **[SASPolicyKey]** have the following meanings:</span></span>

* <span data-ttu-id="3b3ff-137">**[ad]** : Hizmet veri yolu ad alanı.</span><span class="sxs-lookup"><span data-stu-id="3b3ff-137">**[namespace]**: The Service Bus namespace.</span></span>
* <span data-ttu-id="3b3ff-138">**[SASPolicyName]** : Sıra paylaşılan erişim imzası ilke adı.</span><span class="sxs-lookup"><span data-stu-id="3b3ff-138">**[SASPolicyName]**: The Queue Shared Access Signature policy name.</span></span>
* <span data-ttu-id="3b3ff-139">**[SASPolicyKey]** : Sıra paylaşılan erişim imzası ilke anahtarı.</span><span class="sxs-lookup"><span data-stu-id="3b3ff-139">**[SASPolicyKey]**: The Queue Shared Access Signature policy key.</span></span>

> [!NOTE]
> <span data-ttu-id="3b3ff-140">URL kodlama parola kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="3b3ff-140">You must URL-encode the password manually.</span></span> <span data-ttu-id="3b3ff-141">URL kodlaması yararlı bir yardımcı şu adresten edinilebilir [http://www.w3schools.com/tags/ref_urlencode.asp](http://www.w3schools.com/tags/ref_urlencode.asp).</span><span class="sxs-lookup"><span data-stu-id="3b3ff-141">A useful URL-encoding utility is available at [http://www.w3schools.com/tags/ref_urlencode.asp](http://www.w3schools.com/tags/ref_urlencode.asp).</span></span>
> 
> 

#### <a name="configure-destinations"></a><span data-ttu-id="3b3ff-142">Hedeflerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="3b3ff-142">Configure destinations</span></span>
<span data-ttu-id="3b3ff-143">Bir hedef Qpid özellikleri dosya JNDI sağlayıcısında tanımlamak için kullanılan girişinin aşağıdaki biçimi şöyledir:</span><span class="sxs-lookup"><span data-stu-id="3b3ff-143">The entry used to define a destination in the Qpid properties file JNDI provider is of the following format:</span></span>

```
queue.[jndi_name] = [physical_name]
```

<span data-ttu-id="3b3ff-144">or</span><span class="sxs-lookup"><span data-stu-id="3b3ff-144">or</span></span>

```
topic.[jndi_name] = [physical_name]
```

<span data-ttu-id="3b3ff-145">Burada **[JNDI\_adı]** ve **[fiziksel\_adı]** şu anlama gelir:</span><span class="sxs-lookup"><span data-stu-id="3b3ff-145">Where **[jndi\_name]** and **[physical\_name]** have the following meanings:</span></span>

* <span data-ttu-id="3b3ff-146">**[jndi_name]** : Hedef mantıksal adı.</span><span class="sxs-lookup"><span data-stu-id="3b3ff-146">**[jndi_name]**: The logical name of the destination.</span></span> <span data-ttu-id="3b3ff-147">Bu, JNDI IntialContext.lookup() yöntemini kullanarak Java uygulamasında çözümlenir addır.</span><span class="sxs-lookup"><span data-stu-id="3b3ff-147">This is the name that will be resolved in the Java application using the JNDI IntialContext.lookup() method.</span></span>
* <span data-ttu-id="3b3ff-148">**[physical_name]** : Uygulama gönderir veya iletileri alan Service Bus varlık adı.</span><span class="sxs-lookup"><span data-stu-id="3b3ff-148">**[physical_name]**: The name of the Service Bus entity to which the application sends or receives messages.</span></span>

> [!NOTE]
> <span data-ttu-id="3b3ff-149">Bir hizmet veri yolu konusu abonelikten alırken JNDI içinde belirtilen fiziksel adı konu adı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="3b3ff-149">When receiving from a Service Bus topic subscription, the physical name specified in JNDI should be the name of the topic.</span></span> <span data-ttu-id="3b3ff-150">Dayanıklı abonelik JMS uygulama kodunda oluşturulduğunda, abonelik adını sağlanır.</span><span class="sxs-lookup"><span data-stu-id="3b3ff-150">The subscription name is provided when the durable subscription is created in the JMS application code.</span></span> <span data-ttu-id="3b3ff-151">[Hizmet veri yolu AMQP 1.0 Geliştirici Kılavuzu](service-bus-amqp-dotnet.md) JMS Service Bus konularından ile çalışma hakkında daha fazla ayrıntı sağlar.</span><span class="sxs-lookup"><span data-stu-id="3b3ff-151">The [Service Bus AMQP 1.0 Developer's Guide](service-bus-amqp-dotnet.md) provides more details on working with Service Bus topics from JMS.</span></span>
> 
> 

### <a name="write-the-jms-application"></a><span data-ttu-id="3b3ff-152">JMS uygulama yazma</span><span class="sxs-lookup"><span data-stu-id="3b3ff-152">Write the JMS application</span></span>
<span data-ttu-id="3b3ff-153">Özel API'leri veya JMS Service Bus ile kullanırken gereken seçenekler yok.</span><span class="sxs-lookup"><span data-stu-id="3b3ff-153">There are no special APIs or options required when using JMS with Service Bus.</span></span> <span data-ttu-id="3b3ff-154">Ancak, daha sonra ele alınacak bazı kısıtlamalar vardır.</span><span class="sxs-lookup"><span data-stu-id="3b3ff-154">However, there are a few restrictions that will be covered later.</span></span> <span data-ttu-id="3b3ff-155">Herhangi bir JMS uygulama ile çözümleyebilmesi için JNDI ortamının yapılandırması ilk şey gerekli olduğu gibi bir **ConnectionFactory** ve hedefler.</span><span class="sxs-lookup"><span data-stu-id="3b3ff-155">As with any JMS application, the first thing required is configuration of the JNDI environment, to be able to resolve a **ConnectionFactory** and destinations.</span></span>

#### <a name="configure-the-jndi-initialcontext"></a><span data-ttu-id="3b3ff-156">JNDI InitialContext yapılandırın</span><span class="sxs-lookup"><span data-stu-id="3b3ff-156">Configure the JNDI InitialContext</span></span>
<span data-ttu-id="3b3ff-157">JNDI ortam yapılandırma bilgilerini bir hashtable javax.naming.InitialContext sınıfı oluşturucusuna geçirerek yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="3b3ff-157">The JNDI environment is configured by passing a hashtable of configuration information into the constructor of the javax.naming.InitialContext class.</span></span> <span data-ttu-id="3b3ff-158">İki hashtable öğelerindeki ilk bağlam fabrikası ve sağlayıcı URL sınıf adı gereklidir.</span><span class="sxs-lookup"><span data-stu-id="3b3ff-158">The two required elements in the hashtable are the class name of the Initial Context Factory and the Provider URL.</span></span> <span data-ttu-id="3b3ff-159">Aşağıdaki kod özellikleri dosya adlı bir özellik dosyası JNDI sağlayıcı tabanlı Qpid kullanmak için JNDI ortamını yapılandırma gösterir **servicebus.properties**.</span><span class="sxs-lookup"><span data-stu-id="3b3ff-159">The following code shows how to configure the JNDI environment to use the Qpid properties file based JNDI Provider with a properties file named **servicebus.properties**.</span></span>

```java
Hashtable<String, String> env = new Hashtable<String, String>(); 
env.put(Context.INITIAL_CONTEXT_FACTORY, "org.apache.qpid.amqp_1_0.jms.jndi.PropertiesFileInitialContextFactory"); 
env.put(Context.PROVIDER_URL, "servicebus.properties"); 
InitialContext context = new InitialContext(env);
``` 

### <a name="a-simple-jms-application-using-a-service-bus-queue"></a><span data-ttu-id="3b3ff-160">Service Bus kuyruğu kullanarak basit bir JMS uygulama</span><span class="sxs-lookup"><span data-stu-id="3b3ff-160">A simple JMS application using a Service Bus queue</span></span>
<span data-ttu-id="3b3ff-161">Aşağıdaki örnek program sırasının JNDI mantıksal adı ile Service Bus kuyruğuna JMS TextMessages gönderir ve iletilerini geri alır.</span><span class="sxs-lookup"><span data-stu-id="3b3ff-161">The following example program sends JMS TextMessages to a Service Bus queue with the JNDI logical name of QUEUE, and receives the messages back.</span></span>

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
            System.out.println("Press [enter] to send a message. Type 'exit' + [enter] to quit.");
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

### <a name="run-the-application"></a><span data-ttu-id="3b3ff-162">Uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="3b3ff-162">Run the application</span></span>
<span data-ttu-id="3b3ff-163">Uygulamayı çalıştıran biçiminde bir çıktı üretir:</span><span class="sxs-lookup"><span data-stu-id="3b3ff-163">Running the application produces output of the form:</span></span>

```
> java SimpleSenderReceiver
Press [enter] to send a message. Type 'exit' + [enter] to quit.

Sent message with JMSMessageID = ID:2867600614942270318
Received message with JMSMessageID = ID:2867600614942270318

Sent message with JMSMessageID = ID:7578408152750301483
Received message with JMSMessageID = ID:7578408152750301483

Sent message with JMSMessageID = ID:956102171969368961
Received message with JMSMessageID = ID:956102171969368961
exit
```

## <a name="cross-platform-messaging-between-jms-and-net"></a><span data-ttu-id="3b3ff-164">Platformlar arası ileti JMS ve .NET arasında</span><span class="sxs-lookup"><span data-stu-id="3b3ff-164">Cross-platform messaging between JMS and .NET</span></span>
<span data-ttu-id="3b3ff-165">Bu kılavuz, JMS kullanarak Service Bus gelen ve giden ileti gönderme ve alma nasıl oluşturulacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="3b3ff-165">This guide showed how to send and receive messages to and from Service Bus using JMS.</span></span> <span data-ttu-id="3b3ff-166">Ancak, AMQP 1.0 kilit yararları güvenilir bir şekilde ve tam bir güvenilirlik, alınıp iletilerle farklı dillerde yazılmış bileşenlerinden oluşturulacak uygulamalar sağlayan biridir.</span><span class="sxs-lookup"><span data-stu-id="3b3ff-166">However, one of the key benefits of AMQP 1.0 is that it enables applications to be built from components written in different languages, with messages exchanged reliably and at full fidelity.</span></span>

<span data-ttu-id="3b3ff-167">Yukarıda açıklanan örnek JMS uygulama ve yardımcı makaleden gerçekleştirilecek benzer bir .NET uygulaması kullanarak [kullanarak Service Bus .NET AMQP 1.0 ile birlikte gelen](service-bus-amqp-dotnet.md), .NET ve Java arasında iletileri değiştirebilir.</span><span class="sxs-lookup"><span data-stu-id="3b3ff-167">Using the sample JMS application described above and a similar .NET application taken from a companion article, [Using Service Bus from .NET with AMQP 1.0](service-bus-amqp-dotnet.md), you can exchange messages between .NET and Java.</span></span> <span data-ttu-id="3b3ff-168">Platformlar arası Service Bus ve AMQP 1.0 kullanarak Mesajlaşma, ayrıntıları hakkında daha fazla bilgi için bu makaleyi okuyun.</span><span class="sxs-lookup"><span data-stu-id="3b3ff-168">Read this article for more information about the details of cross-platform messaging using Service Bus and AMQP 1.0.</span></span>

### <a name="jms-to-net"></a><span data-ttu-id="3b3ff-169">.NET için JMS</span><span class="sxs-lookup"><span data-stu-id="3b3ff-169">JMS to .NET</span></span>
<span data-ttu-id="3b3ff-170">.NET ileti JMS göstermek için:</span><span class="sxs-lookup"><span data-stu-id="3b3ff-170">To demonstrate JMS to .NET messaging:</span></span>

* <span data-ttu-id="3b3ff-171">Tüm komut satırı bağımsız değişkenleri olmadan .NET örnek uygulaması başlatın.</span><span class="sxs-lookup"><span data-stu-id="3b3ff-171">Start the .NET sample application without any command-line arguments.</span></span>
* <span data-ttu-id="3b3ff-172">Java örnek uygulaması "sendonly" komut satırı bağımsız değişkeniyle başlatın.</span><span class="sxs-lookup"><span data-stu-id="3b3ff-172">Start the Java sample application with the "sendonly" command-line argument.</span></span> <span data-ttu-id="3b3ff-173">Bu modda, uygulama iletileri almaz sıradan, yalnızca gönderir.</span><span class="sxs-lookup"><span data-stu-id="3b3ff-173">In this mode, the application will not receive messages from the queue, it will only send.</span></span>
* <span data-ttu-id="3b3ff-174">Tuşuna **Enter** birkaç kez Java uygulama konsolunda neden olacak gönderilecek iletilerin.</span><span class="sxs-lookup"><span data-stu-id="3b3ff-174">Press **Enter** a few times in the Java application console, which will cause messages to be sent.</span></span>
* <span data-ttu-id="3b3ff-175">Bu iletiler .NET uygulama tarafından alınır.</span><span class="sxs-lookup"><span data-stu-id="3b3ff-175">These messages are received by the .NET application.</span></span>

#### <a name="output-from-jms-application"></a><span data-ttu-id="3b3ff-176">JMS uygulama çıktısı</span><span class="sxs-lookup"><span data-stu-id="3b3ff-176">Output from JMS application</span></span>
```
> java SimpleSenderReceiver sendonly
Press [enter] to send a message. Type 'exit' + [enter] to quit.
Sent message with JMSMessageID = ID:4364096528752411591
Sent message with JMSMessageID = ID:459252991689389983
Sent message with JMSMessageID = ID:1565011046230456854
exit
```

#### <a name="output-from-net-application"></a><span data-ttu-id="3b3ff-177">.NET uygulaması çıktısı</span><span class="sxs-lookup"><span data-stu-id="3b3ff-177">Output from .NET application</span></span>
```
> SimpleSenderReceiver.exe    
Press [enter] to send a message. Type 'exit' + [enter] to quit.
Received message with MessageID = 4364096528752411591
Received message with MessageID = 459252991689389983
Received message with MessageID = 1565011046230456854
exit
```

### <a name="net-to-jms"></a><span data-ttu-id="3b3ff-178">JMS için .NET</span><span class="sxs-lookup"><span data-stu-id="3b3ff-178">.NET to JMS</span></span>
<span data-ttu-id="3b3ff-179">İleti gönderme ve alma JMS .NET göstermek için:</span><span class="sxs-lookup"><span data-stu-id="3b3ff-179">To demonstrate .NET to JMS messaging:</span></span>

* <span data-ttu-id="3b3ff-180">.NET örnek uygulaması "sendonly" komut satırı bağımsız değişkeniyle başlatın.</span><span class="sxs-lookup"><span data-stu-id="3b3ff-180">Start the .NET sample application with the "sendonly" command-line argument.</span></span> <span data-ttu-id="3b3ff-181">Bu modda, uygulama iletileri almaz sıradan, yalnızca gönderir.</span><span class="sxs-lookup"><span data-stu-id="3b3ff-181">In this mode, the application will not receive messages from the queue, it will only send.</span></span>
* <span data-ttu-id="3b3ff-182">Tüm komut satırı bağımsız değişkenleri olmadan Java örnek uygulamayı başlatın.</span><span class="sxs-lookup"><span data-stu-id="3b3ff-182">Start the Java sample application without any command-line arguments.</span></span>
* <span data-ttu-id="3b3ff-183">Tuşuna **Enter** birkaç kez .NET uygulama konsolunda neden olacak gönderilecek iletilerin.</span><span class="sxs-lookup"><span data-stu-id="3b3ff-183">Press **Enter** a few times in the .NET application console, which will cause messages to be sent.</span></span>
* <span data-ttu-id="3b3ff-184">Bu iletiler Java uygulama tarafından alınır.</span><span class="sxs-lookup"><span data-stu-id="3b3ff-184">These messages are received by the Java application.</span></span>

#### <a name="output-from-net-application"></a><span data-ttu-id="3b3ff-185">.NET uygulaması çıktısı</span><span class="sxs-lookup"><span data-stu-id="3b3ff-185">Output from .NET application</span></span>
```
> SimpleSenderReceiver.exe sendonly
Press [enter] to send a message. Type 'exit' + [enter] to quit.
Sent message with MessageID = d64e681a310a48a1ae0ce7b017bf1cf3    
Sent message with MessageID = 98a39664995b4f74b32e2a0ecccc46bb
Sent message with MessageID = acbca67f03c346de9b7893026f97ddeb
exit
```

#### <a name="output-from-jms-application"></a><span data-ttu-id="3b3ff-186">JMS uygulama çıktısı</span><span class="sxs-lookup"><span data-stu-id="3b3ff-186">Output from JMS application</span></span>
```
> java SimpleSenderReceiver    
Press [enter] to send a message. Type 'exit' + [enter] to quit.
Received message with JMSMessageID = ID:d64e681a310a48a1ae0ce7b017bf1cf3
Received message with JMSMessageID = ID:98a39664995b4f74b32e2a0ecccc46bb
Received message with JMSMessageID = ID:acbca67f03c346de9b7893026f97ddeb
exit
```

## <a name="unsupported-features-and-restrictions"></a><span data-ttu-id="3b3ff-187">Desteklenmeyen özellikler ve kısıtlamalar</span><span class="sxs-lookup"><span data-stu-id="3b3ff-187">Unsupported features and restrictions</span></span>
<span data-ttu-id="3b3ff-188">Yani JMS Service Bus ile AMQP 1.0 üzerinden kullanırken, aşağıdaki kısıtlamalar mevcuttur:</span><span class="sxs-lookup"><span data-stu-id="3b3ff-188">The following restrictions exist when using JMS over AMQP 1.0 with Service Bus, namely:</span></span>

* <span data-ttu-id="3b3ff-189">Yalnızca bir **MessageProducer** veya **MessageConsumer** başına izin verilen **oturum**.</span><span class="sxs-lookup"><span data-stu-id="3b3ff-189">Only one **MessageProducer** or **MessageConsumer** is allowed per **Session**.</span></span> <span data-ttu-id="3b3ff-190">Birden çok oluşturmanız gerekiyorsa **MessageProducers** veya **MessageConsumers** bir uygulamada, ayrılmış bir oluşturma **oturum** her biri için.</span><span class="sxs-lookup"><span data-stu-id="3b3ff-190">If you need to create multiple **MessageProducers** or **MessageConsumers** in an application, create a dedicated **Session** for each of them.</span></span>
* <span data-ttu-id="3b3ff-191">Volatile konu abonelikleri şu anda desteklenmemektedir.</span><span class="sxs-lookup"><span data-stu-id="3b3ff-191">Volatile topic subscriptions are not currently supported.</span></span>
* <span data-ttu-id="3b3ff-192">**MessageSelectors** şu anda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="3b3ff-192">**MessageSelectors** are not currently supported.</span></span>
* <span data-ttu-id="3b3ff-193">Geçici hedefleri; Örneğin, **TemporaryQueue**, **TemporaryTopic** şu anda, bunların ile desteklenmemektedir **QueueRequestor** ve **TopicRequestor**Kullanılacakları API'leri.</span><span class="sxs-lookup"><span data-stu-id="3b3ff-193">Temporary destinations; for example, **TemporaryQueue**, **TemporaryTopic** are not currently supported, along with the **QueueRequestor** and **TopicRequestor** APIs that use them.</span></span>
* <span data-ttu-id="3b3ff-194">Uygulaması yapılan oturumlar ve dağıtılmış işlemler desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="3b3ff-194">Transacted sessions and distributed transactions are not supported.</span></span>

## <a name="summary"></a><span data-ttu-id="3b3ff-195">Özet</span><span class="sxs-lookup"><span data-stu-id="3b3ff-195">Summary</span></span>
<span data-ttu-id="3b3ff-196">Nasıl yapılır bu kılavuz, popüler JMS API ve AMQP 1.0 kullanarak Service Bus aracılı Mesajlaşma özellikleri (kuyruklar ve konu başlıkları Yayınla/Abone ol) Java'dan kullanmak nasıl oluşturulacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="3b3ff-196">This how-to guide showed how to use Service Bus brokered messaging features (queues and publish/subscribe topics) from Java using the popular JMS API and AMQP 1.0.</span></span>

<span data-ttu-id="3b3ff-197">Hizmet veri yolu AMQP 1.0 .NET, C, Python ve PHP gibi diğer dillerden de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3b3ff-197">You can also use Service Bus AMQP 1.0 from other languages, including .NET, C, Python, and PHP.</span></span> <span data-ttu-id="3b3ff-198">Bu farklı diller kullanılarak oluşturulan bileşenleri ileti güvenilir bir şekilde gönderip ve AMQP 1.0 kullanarak tam bir güvenilirlik hizmet veri yolundaki destekler.</span><span class="sxs-lookup"><span data-stu-id="3b3ff-198">Components built using these different languages can exchange messages reliably and at full fidelity using the AMQP 1.0 support in Service Bus.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3b3ff-199">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3b3ff-199">Next steps</span></span>
* [<span data-ttu-id="3b3ff-200">Azure hizmet veri yolu AMQP 1.0 desteği</span><span class="sxs-lookup"><span data-stu-id="3b3ff-200">AMQP 1.0 support in Azure Service Bus</span></span>](service-bus-amqp-overview.md)
* [<span data-ttu-id="3b3ff-201">AMQP 1.0 ile Service Bus .NET API kullanma</span><span class="sxs-lookup"><span data-stu-id="3b3ff-201">How to use AMQP 1.0 with the Service Bus .NET API</span></span>](service-bus-dotnet-advanced-message-queuing.md)
* [<span data-ttu-id="3b3ff-202">Hizmet veri yolu AMQP 1.0 Geliştirici Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="3b3ff-202">Service Bus AMQP 1.0 Developer's Guide</span></span>](service-bus-amqp-dotnet.md)
* [<span data-ttu-id="3b3ff-203">Service Bus kuyrukları ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="3b3ff-203">Get started with Service Bus queues</span></span>](service-bus-dotnet-get-started-with-queues.md)
* [<span data-ttu-id="3b3ff-204">Java Geliştirici Merkezi</span><span class="sxs-lookup"><span data-stu-id="3b3ff-204">Java Developer Center</span></span>](https://azure.microsoft.com/develop/java/)

