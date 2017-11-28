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
# <a name="how-toouse-hello-java-message-service-jms-api-with-service-bus-and-amqp-10"></a><span data-ttu-id="79e1a-103">Nasıl toouse hello Java ileti hizmeti (JMS) API Service Bus ve AMQP 1.0</span><span class="sxs-lookup"><span data-stu-id="79e1a-103">How toouse hello Java Message Service (JMS) API with Service Bus and AMQP 1.0</span></span>
<span data-ttu-id="79e1a-104">Merhaba Gelişmiş Message Queuing Protokolü (AMQP) 1.0 toobuild güçlü, platformlar arası ileti uygulamaları kullanabilirsiniz verimli, güvenilir ve hat düzeyinde bir Mesajlaşma iletişim kuralıdır.</span><span class="sxs-lookup"><span data-stu-id="79e1a-104">hello Advanced Message Queuing Protocol (AMQP) 1.0 is an efficient, reliable, wire-level messaging protocol that you can use toobuild robust, cross-platform messaging applications.</span></span>

<span data-ttu-id="79e1a-105">Hizmet kullanabileceğiniz anlamına gelir queuing hello ve yayımlama/aracılı Mesajlaşma özellikleri verimli bir ikili protokolünü kullanarak platformları aralığından abonelik veri yolu AMQP 1.0 için destek.</span><span class="sxs-lookup"><span data-stu-id="79e1a-105">Support for AMQP 1.0 in Service Bus means that you can use hello queuing and publish/subscribe brokered messaging features from a range of platforms using an efficient binary protocol.</span></span> <span data-ttu-id="79e1a-106">Ayrıca, diller, çerçevelerinin ve işletim sistemlerinin bir karışımını kullanılarak oluşturulan bileşenlerden oluşan uygulamalar oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="79e1a-106">Furthermore, you can build applications comprised of components built using a mix of languages, frameworks, and operating systems.</span></span>

<span data-ttu-id="79e1a-107">Bu makalede, popüler Java ileti hizmeti (JMS) API standart toouse Service Bus Mesajlaşma özelliklerinden (kuyruklar ve yayımlama/abonelik konuları) kullanarak Java uygulamaları nasıl hello açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="79e1a-107">This article explains how toouse Service Bus messaging features (queues and publish/subscribe topics) from Java applications using hello popular Java Message Service (JMS) API standard.</span></span> <span data-ttu-id="79e1a-108">Var olan bir [yardımcı makale](service-bus-amqp-dotnet.md) nasıl toodo hello aynı hello Service Bus .NET API kullanarak açıklar.</span><span class="sxs-lookup"><span data-stu-id="79e1a-108">There is a [companion article](service-bus-amqp-dotnet.md) that explains how toodo hello same using hello Service Bus .NET API.</span></span> <span data-ttu-id="79e1a-109">AMQP 1.0 kullanarak platformlar arası ileti gönderme hakkında şu iki kılavuzları birlikte toolearn kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="79e1a-109">You can use these two guides together toolearn about cross-platform messaging using AMQP 1.0.</span></span>

## <a name="get-started-with-service-bus"></a><span data-ttu-id="79e1a-110">Service Bus’ı kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="79e1a-110">Get started with Service Bus</span></span>
<span data-ttu-id="79e1a-111">Bu kılavuz, adlandırılan bir kuyruğun içeren bir hizmet veri yolu ad alanı zaten sahip olduğunuzu varsayar **sıra 1**.</span><span class="sxs-lookup"><span data-stu-id="79e1a-111">This guide assumes that you already have a Service Bus namespace containing a queue named **queue1**.</span></span> <span data-ttu-id="79e1a-112">Bunu yapmanız sonra şunları yapabilirsiniz [hello ad alanı ve Kuyruk oluşturma](service-bus-create-namespace-portal.md) hello kullanarak [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="79e1a-112">If you do not, then you can [create hello namespace and queue](service-bus-create-namespace-portal.md) using hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="79e1a-113">Toocreate hizmet veri yolu ad alanları ve Kuyruklar nasıl görürüm hakkında daha fazla bilgi için [Service Bus kuyrukları ile çalışmaya başlama](service-bus-dotnet-get-started-with-queues.md).</span><span class="sxs-lookup"><span data-stu-id="79e1a-113">For more information about how toocreate Service Bus namespaces and queues, see [Get started with Service Bus queues](service-bus-dotnet-get-started-with-queues.md).</span></span>

> [!NOTE]
> <span data-ttu-id="79e1a-114">Bölümlenmiş kuyruklar ve konu başlıkları da AMQP destekler.</span><span class="sxs-lookup"><span data-stu-id="79e1a-114">Partitioned queues and topics also support AMQP.</span></span> <span data-ttu-id="79e1a-115">Daha fazla bilgi için bkz: [bölümlenmiş Mesajlaşma varlıkları](service-bus-partitioning.md) ve [hizmet veri yolu AMQP 1.0 desteği bölümlenmiş kuyruklar ve konu başlıkları](service-bus-partitioned-queues-and-topics-amqp-overview.md).</span><span class="sxs-lookup"><span data-stu-id="79e1a-115">For more information, see [Partitioned messaging entities](service-bus-partitioning.md) and [AMQP 1.0 support for Service Bus partitioned queues and topics](service-bus-partitioned-queues-and-topics-amqp-overview.md).</span></span>
> 
> 

## <a name="downloading-hello-amqp-10-jms-client-library"></a><span data-ttu-id="79e1a-116">İndirme hello AMQP 1.0 JMS istemci kitaplığı</span><span class="sxs-lookup"><span data-stu-id="79e1a-116">Downloading hello AMQP 1.0 JMS client library</span></span>
<span data-ttu-id="79e1a-117">Burada toodownload hello hello Apache Qpid JMS AMQP 1.0 istemci kitaplığının en son sürümü hakkında daha fazla bilgi için [https://qpid.apache.org/download.html](https://qpid.apache.org/download.html).</span><span class="sxs-lookup"><span data-stu-id="79e1a-117">For information about where toodownload hello latest version of hello Apache Qpid JMS AMQP 1.0 client library, visit [https://qpid.apache.org/download.html](https://qpid.apache.org/download.html).</span></span>

<span data-ttu-id="79e1a-118">Merhaba Apache Qpid JMS AMQP 1.0 dağıtım arşiv toohello ' Java sınıf oluşturma ve Service Bus ile JMS uygulamaları çalıştırırken aşağıdaki dört JAR dosyaları hello eklemeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="79e1a-118">You must add hello following four JAR files from hello Apache Qpid JMS AMQP 1.0 distribution archive toohello Java CLASSPATH when building and running JMS applications with Service Bus:</span></span>

* <span data-ttu-id="79e1a-119">geronimo jms\_1.1\_spec 1.0.jar</span><span class="sxs-lookup"><span data-stu-id="79e1a-119">geronimo-jms\_1.1\_spec-1.0.jar</span></span>
* <span data-ttu-id="79e1a-120">qpid-amqp-1-0-client-[Version].jar</span><span class="sxs-lookup"><span data-stu-id="79e1a-120">qpid-amqp-1-0-client-[version].jar</span></span>
* <span data-ttu-id="79e1a-121">qpid-amqp-1-0-Client-jms-[Version].jar</span><span class="sxs-lookup"><span data-stu-id="79e1a-121">qpid-amqp-1-0-client-jms-[version].jar</span></span>
* <span data-ttu-id="79e1a-122">qpid-amqp-1-0-Common-[Version].jar</span><span class="sxs-lookup"><span data-stu-id="79e1a-122">qpid-amqp-1-0-common-[version].jar</span></span>

## <a name="coding-java-applications"></a><span data-ttu-id="79e1a-123">Java uygulamalarını kodlama</span><span class="sxs-lookup"><span data-stu-id="79e1a-123">Coding Java applications</span></span>
### <a name="java-naming-and-directory-interface-jndi"></a><span data-ttu-id="79e1a-124">Java adlandırma ve dizini arabirimi (JNDI)</span><span class="sxs-lookup"><span data-stu-id="79e1a-124">Java Naming and Directory Interface (JNDI)</span></span>
<span data-ttu-id="79e1a-125">JMS hello Java adlandırma ve dizin arabirimi (JNDI) toocreate mantıksal ve fiziksel adlarını arasında ayrım kullanır.</span><span class="sxs-lookup"><span data-stu-id="79e1a-125">JMS uses hello Java Naming and Directory Interface (JNDI) toocreate a separation between logical names and physical names.</span></span> <span data-ttu-id="79e1a-126">İki tür JMS nesneleri JNDI kullanarak çözümlenir: ConnectionFactory ve hedef.</span><span class="sxs-lookup"><span data-stu-id="79e1a-126">Two types of JMS objects are resolved using JNDI: ConnectionFactory and Destination.</span></span> <span data-ttu-id="79e1a-127">JNDI farklı dizin hizmetleri toohandle ad çözümleme görevlerini ekleyebilirsiniz sağlayıcı modeli kullanır.</span><span class="sxs-lookup"><span data-stu-id="79e1a-127">JNDI uses a provider model into which you can plug different directory services toohandle name resolution duties.</span></span> <span data-ttu-id="79e1a-128">Merhaba Apache Qpid JMS AMQP 1.0 kitaplığı basit özellikleri ile birlikte gelen dosya tabanlı JNDI hello aşağıdaki özellikleri dosyası kullanılarak yapılandırılmış sağlayıcısı biçimi:</span><span class="sxs-lookup"><span data-stu-id="79e1a-128">hello Apache Qpid JMS AMQP 1.0 library comes with a simple properties file-based JNDI Provider that is configured using a properties file of hello following format:</span></span>

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

#### <a name="configure-hello-connectionfactory"></a><span data-ttu-id="79e1a-129">Merhaba ConnectionFactory yapılandırın</span><span class="sxs-lookup"><span data-stu-id="79e1a-129">Configure hello ConnectionFactory</span></span>
<span data-ttu-id="79e1a-130">kullanılan girdisi toodefine hello bir **ConnectionFactory** hello Qpid özellikleri dosya JNDI biçimini izleyen Merhaba sağlayıcısıdır:</span><span class="sxs-lookup"><span data-stu-id="79e1a-130">hello entry used toodefine a **ConnectionFactory** in hello Qpid properties file JNDI provider is of hello following format:</span></span>

```
connectionfactory.[jndi_name] = [ConnectionURL]
```

<span data-ttu-id="79e1a-131">Burada **[jndi_name]** ve **[ConnectionURL]** anlamları aşağıdaki hello vardır:</span><span class="sxs-lookup"><span data-stu-id="79e1a-131">Where **[jndi_name]** and **[ConnectionURL]** have hello following meanings:</span></span>

* <span data-ttu-id="79e1a-132">**[jndi_name]** : Merhaba ConnectionFactory hello mantıksal adı.</span><span class="sxs-lookup"><span data-stu-id="79e1a-132">**[jndi_name]**: hello logical name of hello ConnectionFactory.</span></span> <span data-ttu-id="79e1a-133">Bu, Merhaba Java uygulaması hello JNDI IntialContext.lookup() yöntemini kullanarak çözümlenir hello addır.</span><span class="sxs-lookup"><span data-stu-id="79e1a-133">This is hello name that will be resolved in hello Java application using hello JNDI IntialContext.lookup() method.</span></span>
* <span data-ttu-id="79e1a-134">**[ConnectionURL]** : Hello bilgilerle hello JMS kitaplığı sağlayan bir URL gerekli toohello AMQP Aracısı.</span><span class="sxs-lookup"><span data-stu-id="79e1a-134">**[ConnectionURL]**: A URL that provides hello JMS library with hello information required toohello AMQP broker.</span></span>

<span data-ttu-id="79e1a-135">Merhaba Hello biçimi **ConnectionURL** aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="79e1a-135">hello format of hello **ConnectionURL** is as follows:</span></span>

```
amqps://[SASPolicyName]:[SASPolicyKey]@[namespace].servicebus.windows.net
```
<span data-ttu-id="79e1a-136">Burada **[ad]**, **[SASPolicyName]** ve **[SASPolicyKey]** anlamları aşağıdaki hello vardır:</span><span class="sxs-lookup"><span data-stu-id="79e1a-136">Where **[namespace]**, **[SASPolicyName]** and **[SASPolicyKey]** have hello following meanings:</span></span>

* <span data-ttu-id="79e1a-137">**[ad]** : Service Bus ad alanı hello.</span><span class="sxs-lookup"><span data-stu-id="79e1a-137">**[namespace]**: hello Service Bus namespace.</span></span>
* <span data-ttu-id="79e1a-138">**[SASPolicyName]** : hello sıra paylaşılan erişim imzası ilke adı.</span><span class="sxs-lookup"><span data-stu-id="79e1a-138">**[SASPolicyName]**: hello Queue Shared Access Signature policy name.</span></span>
* <span data-ttu-id="79e1a-139">**[SASPolicyKey]** : hello sıra paylaşılan erişim imzası ilke anahtarı.</span><span class="sxs-lookup"><span data-stu-id="79e1a-139">**[SASPolicyKey]**: hello Queue Shared Access Signature policy key.</span></span>

> [!NOTE]
> <span data-ttu-id="79e1a-140">URL kodlama hello parola el ile gerekir.</span><span class="sxs-lookup"><span data-stu-id="79e1a-140">You must URL-encode hello password manually.</span></span> <span data-ttu-id="79e1a-141">URL kodlaması yararlı bir yardımcı şu adresten edinilebilir [http://www.w3schools.com/tags/ref_urlencode.asp](http://www.w3schools.com/tags/ref_urlencode.asp).</span><span class="sxs-lookup"><span data-stu-id="79e1a-141">A useful URL-encoding utility is available at [http://www.w3schools.com/tags/ref_urlencode.asp](http://www.w3schools.com/tags/ref_urlencode.asp).</span></span>
> 
> 

#### <a name="configure-destinations"></a><span data-ttu-id="79e1a-142">Hedeflerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="79e1a-142">Configure destinations</span></span>
<span data-ttu-id="79e1a-143">Merhaba giriş biçimini izleyen Merhaba hello Qpid özellikleri dosya JNDI sağlayıcısında bir hedefi olan toodefine kullanılır:</span><span class="sxs-lookup"><span data-stu-id="79e1a-143">hello entry used toodefine a destination in hello Qpid properties file JNDI provider is of hello following format:</span></span>

```
queue.[jndi_name] = [physical_name]
```

<span data-ttu-id="79e1a-144">or</span><span class="sxs-lookup"><span data-stu-id="79e1a-144">or</span></span>

```
topic.[jndi_name] = [physical_name]
```

<span data-ttu-id="79e1a-145">Burada **[JNDI\_adı]** ve **[fiziksel\_adı]** anlamları aşağıdaki hello vardır:</span><span class="sxs-lookup"><span data-stu-id="79e1a-145">Where **[jndi\_name]** and **[physical\_name]** have hello following meanings:</span></span>

* <span data-ttu-id="79e1a-146">**[jndi_name]** : hello hedef hello mantıksal adı.</span><span class="sxs-lookup"><span data-stu-id="79e1a-146">**[jndi_name]**: hello logical name of hello destination.</span></span> <span data-ttu-id="79e1a-147">Bu, Merhaba Java uygulaması hello JNDI IntialContext.lookup() yöntemini kullanarak çözümlenir hello addır.</span><span class="sxs-lookup"><span data-stu-id="79e1a-147">This is hello name that will be resolved in hello Java application using hello JNDI IntialContext.lookup() method.</span></span>
* <span data-ttu-id="79e1a-148">**[physical_name]** : hello Service Bus varlık toowhich Merhaba uygulaması hello adını gönderir veya iletilerini alır.</span><span class="sxs-lookup"><span data-stu-id="79e1a-148">**[physical_name]**: hello name of hello Service Bus entity toowhich hello application sends or receives messages.</span></span>

> [!NOTE]
> <span data-ttu-id="79e1a-149">Bir hizmet veri yolu konusu abonelikten alırken hello fiziksel ad JNDI içinde belirtilen hello konunun hello adı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="79e1a-149">When receiving from a Service Bus topic subscription, hello physical name specified in JNDI should be hello name of hello topic.</span></span> <span data-ttu-id="79e1a-150">Merhaba dayanıklı abonelik hello JMS uygulama kodu oluşturulduğunda hello abonelik adı sağlanır.</span><span class="sxs-lookup"><span data-stu-id="79e1a-150">hello subscription name is provided when hello durable subscription is created in hello JMS application code.</span></span> <span data-ttu-id="79e1a-151">Merhaba [hizmet veri yolu AMQP 1.0 Geliştirici Kılavuzu](service-bus-amqp-dotnet.md) JMS Service Bus konularından ile çalışma hakkında daha fazla ayrıntı sağlar.</span><span class="sxs-lookup"><span data-stu-id="79e1a-151">hello [Service Bus AMQP 1.0 Developer's Guide](service-bus-amqp-dotnet.md) provides more details on working with Service Bus topics from JMS.</span></span>
> 
> 

### <a name="write-hello-jms-application"></a><span data-ttu-id="79e1a-152">Merhaba JMS uygulaması yazma</span><span class="sxs-lookup"><span data-stu-id="79e1a-152">Write hello JMS application</span></span>
<span data-ttu-id="79e1a-153">Özel API'leri veya JMS Service Bus ile kullanırken gereken seçenekler yok.</span><span class="sxs-lookup"><span data-stu-id="79e1a-153">There are no special APIs or options required when using JMS with Service Bus.</span></span> <span data-ttu-id="79e1a-154">Ancak, daha sonra ele alınacak bazı kısıtlamalar vardır.</span><span class="sxs-lookup"><span data-stu-id="79e1a-154">However, there are a few restrictions that will be covered later.</span></span> <span data-ttu-id="79e1a-155">Herhangi bir JMS uygulama ile Merhaba JNDI ortamının, toobe mümkün tooresolve yapılandırması hello ilk şey gerekli olduğu gibi bir **ConnectionFactory** ve hedefler.</span><span class="sxs-lookup"><span data-stu-id="79e1a-155">As with any JMS application, hello first thing required is configuration of hello JNDI environment, toobe able tooresolve a **ConnectionFactory** and destinations.</span></span>

#### <a name="configure-hello-jndi-initialcontext"></a><span data-ttu-id="79e1a-156">Merhaba JNDI InitialContext yapılandırın</span><span class="sxs-lookup"><span data-stu-id="79e1a-156">Configure hello JNDI InitialContext</span></span>
<span data-ttu-id="79e1a-157">Merhaba JNDI ortamı hello javax.naming.InitialContext sınıfı hello oluşturucuya yapılandırma bilgilerini bir hashtable geçirerek yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="79e1a-157">hello JNDI environment is configured by passing a hashtable of configuration information into hello constructor of hello javax.naming.InitialContext class.</span></span> <span data-ttu-id="79e1a-158">Merhaba iki gerekli hello hashtable içinde hello ilk bağlam fabrikası hello sınıf adını ve hello sağlayıcısı URL öğelerdir.</span><span class="sxs-lookup"><span data-stu-id="79e1a-158">hello two required elements in hello hashtable are hello class name of hello Initial Context Factory and hello Provider URL.</span></span> <span data-ttu-id="79e1a-159">Merhaba aşağıdaki kod nasıl tooconfigure hello JNDI ortam toouse hello Qpid özellikleri dosya adlı bir özellik dosyası JNDI sağlayıcı tabanlı gösterir **servicebus.properties**.</span><span class="sxs-lookup"><span data-stu-id="79e1a-159">hello following code shows how tooconfigure hello JNDI environment toouse hello Qpid properties file based JNDI Provider with a properties file named **servicebus.properties**.</span></span>

```java
Hashtable<String, String> env = new Hashtable<String, String>(); 
env.put(Context.INITIAL_CONTEXT_FACTORY, "org.apache.qpid.amqp_1_0.jms.jndi.PropertiesFileInitialContextFactory"); 
env.put(Context.PROVIDER_URL, "servicebus.properties"); 
InitialContext context = new InitialContext(env);
``` 

### <a name="a-simple-jms-application-using-a-service-bus-queue"></a><span data-ttu-id="79e1a-160">Service Bus kuyruğu kullanarak basit bir JMS uygulama</span><span class="sxs-lookup"><span data-stu-id="79e1a-160">A simple JMS application using a Service Bus queue</span></span>
<span data-ttu-id="79e1a-161">Merhaba aşağıdaki örnek program JMS TextMessages tooa Service Bus kuyruğuna sırasının hello JNDI mantıksal adı ile gönderir ve hello iletilerini geri alır.</span><span class="sxs-lookup"><span data-stu-id="79e1a-161">hello following example program sends JMS TextMessages tooa Service Bus queue with hello JNDI logical name of QUEUE, and receives hello messages back.</span></span>

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

### <a name="run-hello-application"></a><span data-ttu-id="79e1a-162">Merhaba uygulamayı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="79e1a-162">Run hello application</span></span>
<span data-ttu-id="79e1a-163">Merhaba uygulaması çalıştıran hello formunun bir çıktı üretir:</span><span class="sxs-lookup"><span data-stu-id="79e1a-163">Running hello application produces output of hello form:</span></span>

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

## <a name="cross-platform-messaging-between-jms-and-net"></a><span data-ttu-id="79e1a-164">Platformlar arası ileti JMS ve .NET arasında</span><span class="sxs-lookup"><span data-stu-id="79e1a-164">Cross-platform messaging between JMS and .NET</span></span>
<span data-ttu-id="79e1a-165">Bu kılavuz nasıl oluşturulacağını gösterir toosend ve hizmet JMS kullanarak veri yolundan iletileri tooand alırsınız.</span><span class="sxs-lookup"><span data-stu-id="79e1a-165">This guide showed how toosend and receive messages tooand from Service Bus using JMS.</span></span> <span data-ttu-id="79e1a-166">Ancak, hello avantajları AMQP 1.0 güvenilir bir şekilde ve tam bir güvenilirlik, alınıp iletilerle farklı dillerde yazılmış Bileşenler'den yerleşik uygulamaları toobe etkinleştirir biridir.</span><span class="sxs-lookup"><span data-stu-id="79e1a-166">However, one of hello key benefits of AMQP 1.0 is that it enables applications toobe built from components written in different languages, with messages exchanged reliably and at full fidelity.</span></span>

<span data-ttu-id="79e1a-167">Yukarıda açıklanan hello örnek JMS uygulama ve yardımcı makaleden gerçekleştirilecek benzer bir .NET uygulaması kullanarak [kullanarak Service Bus .NET AMQP 1.0 ile birlikte gelen](service-bus-amqp-dotnet.md), .NET ve Java arasında iletileri değiştirebilir.</span><span class="sxs-lookup"><span data-stu-id="79e1a-167">Using hello sample JMS application described above and a similar .NET application taken from a companion article, [Using Service Bus from .NET with AMQP 1.0](service-bus-amqp-dotnet.md), you can exchange messages between .NET and Java.</span></span> <span data-ttu-id="79e1a-168">Platformlar arası Service Bus ve AMQP 1.0 kullanarak Mesajlaşma, hello ayrıntıları hakkında daha fazla bilgi için bu makaleyi okuyun.</span><span class="sxs-lookup"><span data-stu-id="79e1a-168">Read this article for more information about hello details of cross-platform messaging using Service Bus and AMQP 1.0.</span></span>

### <a name="jms-toonet"></a><span data-ttu-id="79e1a-169">JMS too.NET</span><span class="sxs-lookup"><span data-stu-id="79e1a-169">JMS too.NET</span></span>
<span data-ttu-id="79e1a-170">toodemonstrate JMS too.NET ileti:</span><span class="sxs-lookup"><span data-stu-id="79e1a-170">toodemonstrate JMS too.NET messaging:</span></span>

* <span data-ttu-id="79e1a-171">Tüm komut satırı bağımsız değişkenleri olmadan Merhaba .NET örnek uygulaması başlatın.</span><span class="sxs-lookup"><span data-stu-id="79e1a-171">Start hello .NET sample application without any command-line arguments.</span></span>
* <span data-ttu-id="79e1a-172">Merhaba Java örnek uygulaması hello "sendonly" komut satırı bağımsız değişkeniyle başlatın.</span><span class="sxs-lookup"><span data-stu-id="79e1a-172">Start hello Java sample application with hello "sendonly" command-line argument.</span></span> <span data-ttu-id="79e1a-173">Bu modda, hello uygulama hello kuyruktan iletileri almaz, yalnızca gönderir.</span><span class="sxs-lookup"><span data-stu-id="79e1a-173">In this mode, hello application will not receive messages from hello queue, it will only send.</span></span>
* <span data-ttu-id="79e1a-174">Tuşuna **Enter** birkaç kez hello Java uygulama konsolunda neden olacak gönderilen iletileri toobe.</span><span class="sxs-lookup"><span data-stu-id="79e1a-174">Press **Enter** a few times in hello Java application console, which will cause messages toobe sent.</span></span>
* <span data-ttu-id="79e1a-175">Bu iletiler hello .NET uygulaması tarafından alınır.</span><span class="sxs-lookup"><span data-stu-id="79e1a-175">These messages are received by hello .NET application.</span></span>

#### <a name="output-from-jms-application"></a><span data-ttu-id="79e1a-176">JMS uygulama çıktısı</span><span class="sxs-lookup"><span data-stu-id="79e1a-176">Output from JMS application</span></span>
```
> java SimpleSenderReceiver sendonly
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Sent message with JMSMessageID = ID:4364096528752411591
Sent message with JMSMessageID = ID:459252991689389983
Sent message with JMSMessageID = ID:1565011046230456854
exit
```

#### <a name="output-from-net-application"></a><span data-ttu-id="79e1a-177">.NET uygulaması çıktısı</span><span class="sxs-lookup"><span data-stu-id="79e1a-177">Output from .NET application</span></span>
```
> SimpleSenderReceiver.exe    
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Received message with MessageID = 4364096528752411591
Received message with MessageID = 459252991689389983
Received message with MessageID = 1565011046230456854
exit
```

### <a name="net-toojms"></a><span data-ttu-id="79e1a-178">.NET tooJMS</span><span class="sxs-lookup"><span data-stu-id="79e1a-178">.NET tooJMS</span></span>
<span data-ttu-id="79e1a-179">toodemonstrate .NET tooJMS ileti:</span><span class="sxs-lookup"><span data-stu-id="79e1a-179">toodemonstrate .NET tooJMS messaging:</span></span>

* <span data-ttu-id="79e1a-180">Merhaba .NET örnek uygulaması hello "sendonly" komut satırı bağımsız değişkeniyle başlatın.</span><span class="sxs-lookup"><span data-stu-id="79e1a-180">Start hello .NET sample application with hello "sendonly" command-line argument.</span></span> <span data-ttu-id="79e1a-181">Bu modda, hello uygulama hello kuyruktan iletileri almaz, yalnızca gönderir.</span><span class="sxs-lookup"><span data-stu-id="79e1a-181">In this mode, hello application will not receive messages from hello queue, it will only send.</span></span>
* <span data-ttu-id="79e1a-182">Tüm komut satırı bağımsız değişkenleri olmadan Hello Java örnek uygulamayı başlatın.</span><span class="sxs-lookup"><span data-stu-id="79e1a-182">Start hello Java sample application without any command-line arguments.</span></span>
* <span data-ttu-id="79e1a-183">Tuşuna **Enter** birkaç kez hello .NET uygulama konsolunda neden olacak gönderilen iletileri toobe.</span><span class="sxs-lookup"><span data-stu-id="79e1a-183">Press **Enter** a few times in hello .NET application console, which will cause messages toobe sent.</span></span>
* <span data-ttu-id="79e1a-184">Bu iletiler hello Java uygulaması tarafından alınır.</span><span class="sxs-lookup"><span data-stu-id="79e1a-184">These messages are received by hello Java application.</span></span>

#### <a name="output-from-net-application"></a><span data-ttu-id="79e1a-185">.NET uygulaması çıktısı</span><span class="sxs-lookup"><span data-stu-id="79e1a-185">Output from .NET application</span></span>
```
> SimpleSenderReceiver.exe sendonly
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Sent message with MessageID = d64e681a310a48a1ae0ce7b017bf1cf3    
Sent message with MessageID = 98a39664995b4f74b32e2a0ecccc46bb
Sent message with MessageID = acbca67f03c346de9b7893026f97ddeb
exit
```

#### <a name="output-from-jms-application"></a><span data-ttu-id="79e1a-186">JMS uygulama çıktısı</span><span class="sxs-lookup"><span data-stu-id="79e1a-186">Output from JMS application</span></span>
```
> java SimpleSenderReceiver    
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Received message with JMSMessageID = ID:d64e681a310a48a1ae0ce7b017bf1cf3
Received message with JMSMessageID = ID:98a39664995b4f74b32e2a0ecccc46bb
Received message with JMSMessageID = ID:acbca67f03c346de9b7893026f97ddeb
exit
```

## <a name="unsupported-features-and-restrictions"></a><span data-ttu-id="79e1a-187">Desteklenmeyen özellikler ve kısıtlamalar</span><span class="sxs-lookup"><span data-stu-id="79e1a-187">Unsupported features and restrictions</span></span>
<span data-ttu-id="79e1a-188">kısıtlamaları aşağıdaki hello JMS Service Bus ile AMQP 1.0 üzerinden öğesine kullanırken mevcuttur:</span><span class="sxs-lookup"><span data-stu-id="79e1a-188">hello following restrictions exist when using JMS over AMQP 1.0 with Service Bus, namely:</span></span>

* <span data-ttu-id="79e1a-189">Yalnızca bir **MessageProducer** veya **MessageConsumer** başına izin verilen **oturum**.</span><span class="sxs-lookup"><span data-stu-id="79e1a-189">Only one **MessageProducer** or **MessageConsumer** is allowed per **Session**.</span></span> <span data-ttu-id="79e1a-190">Toocreate gerekiyorsa birden çok **MessageProducers** veya **MessageConsumers** bir uygulamada, ayrılmış bir oluşturma **oturum** her biri için.</span><span class="sxs-lookup"><span data-stu-id="79e1a-190">If you need toocreate multiple **MessageProducers** or **MessageConsumers** in an application, create a dedicated **Session** for each of them.</span></span>
* <span data-ttu-id="79e1a-191">Volatile konu abonelikleri şu anda desteklenmemektedir.</span><span class="sxs-lookup"><span data-stu-id="79e1a-191">Volatile topic subscriptions are not currently supported.</span></span>
* <span data-ttu-id="79e1a-192">**MessageSelectors** şu anda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="79e1a-192">**MessageSelectors** are not currently supported.</span></span>
* <span data-ttu-id="79e1a-193">Geçici hedefleri; Örneğin, **TemporaryQueue**, **TemporaryTopic** şu anda, birlikte hello desteklenmemektedir **QueueRequestor** ve **TopicRequestor**Kullanılacakları API'leri.</span><span class="sxs-lookup"><span data-stu-id="79e1a-193">Temporary destinations; for example, **TemporaryQueue**, **TemporaryTopic** are not currently supported, along with hello **QueueRequestor** and **TopicRequestor** APIs that use them.</span></span>
* <span data-ttu-id="79e1a-194">Uygulaması yapılan oturumlar ve dağıtılmış işlemler desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="79e1a-194">Transacted sessions and distributed transactions are not supported.</span></span>

## <a name="summary"></a><span data-ttu-id="79e1a-195">Özet</span><span class="sxs-lookup"><span data-stu-id="79e1a-195">Summary</span></span>
<span data-ttu-id="79e1a-196">Bu nasıl tooguide nasıl Java kullanarak toouse Service Bus aracılı Mesajlaşma özellikleri (kuyruklar ve yayımlama/abonelik konuları) popüler JMS API ve AMQP 1.0 hello gösterdi.</span><span class="sxs-lookup"><span data-stu-id="79e1a-196">This how-tooguide showed how toouse Service Bus brokered messaging features (queues and publish/subscribe topics) from Java using hello popular JMS API and AMQP 1.0.</span></span>

<span data-ttu-id="79e1a-197">Hizmet veri yolu AMQP 1.0 .NET, C, Python ve PHP gibi diğer dillerden de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="79e1a-197">You can also use Service Bus AMQP 1.0 from other languages, including .NET, C, Python, and PHP.</span></span> <span data-ttu-id="79e1a-198">Bu farklı diller kullanılarak oluşturulan bileşenleri, güvenilir ve hizmet veri yolundaki kullanılarak hello AMQP 1.0 desteği tam uygunluğunu iletileri değiştirebilir.</span><span class="sxs-lookup"><span data-stu-id="79e1a-198">Components built using these different languages can exchange messages reliably and at full fidelity using hello AMQP 1.0 support in Service Bus.</span></span>

## <a name="next-steps"></a><span data-ttu-id="79e1a-199">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="79e1a-199">Next steps</span></span>
* [<span data-ttu-id="79e1a-200">Azure hizmet veri yolu AMQP 1.0 desteği</span><span class="sxs-lookup"><span data-stu-id="79e1a-200">AMQP 1.0 support in Azure Service Bus</span></span>](service-bus-amqp-overview.md)
* [<span data-ttu-id="79e1a-201">Nasıl toouse AMQP 1.0 ile Merhaba Service Bus .NET API</span><span class="sxs-lookup"><span data-stu-id="79e1a-201">How toouse AMQP 1.0 with hello Service Bus .NET API</span></span>](service-bus-dotnet-advanced-message-queuing.md)
* [<span data-ttu-id="79e1a-202">Hizmet veri yolu AMQP 1.0 Geliştirici Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="79e1a-202">Service Bus AMQP 1.0 Developer's Guide</span></span>](service-bus-amqp-dotnet.md)
* [<span data-ttu-id="79e1a-203">Service Bus kuyrukları ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="79e1a-203">Get started with Service Bus queues</span></span>](service-bus-dotnet-get-started-with-queues.md)
* [<span data-ttu-id="79e1a-204">Java Geliştirici Merkezi</span><span class="sxs-lookup"><span data-stu-id="79e1a-204">Java Developer Center</span></span>](https://azure.microsoft.com/develop/java/)

