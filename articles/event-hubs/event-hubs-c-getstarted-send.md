---
title: "aaaSend olayları tooAzure olay hub'ları C kullanarak | Microsoft Docs"
description: "Olayları tooAzure olay hub'ın C kullanarak Gönder"
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: c
ms.devlang: csharp
ms.topic: article
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: bb53300c070debb4a3658a38df9d3966f08e81ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="send-events-tooazure-event-hubs-using-c"></a><span data-ttu-id="fe949-103">Olayları tooAzure olay hub'ın C kullanarak Gönder</span><span class="sxs-lookup"><span data-stu-id="fe949-103">Send events tooAzure Event Hubs using C</span></span>

## <a name="introduction"></a><span data-ttu-id="fe949-104">Giriş</span><span class="sxs-lookup"><span data-stu-id="fe949-104">Introduction</span></span>
<span data-ttu-id="fe949-105">Olay hub'ları bir uygulama tooprocess etkinleştirme saniye başına milyonlarca olayı alma ve veri bağlı cihazlarınız ve uygulamalarınız tarafından üretilen oldukça büyük miktardaki hello analiz bir yüksek düzeyde ölçeklenebilir bir alım sistem olur.</span><span class="sxs-lookup"><span data-stu-id="fe949-105">Event Hubs is a highly scalable ingestion system that can ingest millions of events per second, enabling an application tooprocess and analyze hello massive amounts of data produced by your connected devices and applications.</span></span> <span data-ttu-id="fe949-106">Bir olay hub'ına toplandığında, dönüştürme ve herhangi bir gerçek zamanlı analiz sağlayıcısı veya depolama kümesi kullanarak verileri depolar.</span><span class="sxs-lookup"><span data-stu-id="fe949-106">Once collected into an event hub, you can transform and store data using any real-time analytics provider or storage cluster.</span></span>

<span data-ttu-id="fe949-107">Daha fazla bilgi için lütfen bkz hello [Event Hubs'a genel bakış] [Event Hubs'a genel bakış].</span><span class="sxs-lookup"><span data-stu-id="fe949-107">For more information, please see hello [Event Hubs overview][Event Hubs overview].</span></span>

<span data-ttu-id="fe949-108">Bu öğreticide şunları öğreneceksiniz nasıl hello uygun alıcı dilde hello sol İçindekiler C. tooreceive olaylarında bir konsol uygulaması kullanarak toosend olayları tooan olay hub'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="fe949-108">In this tutorial, you will learn how toosend events tooan event hub using a console application in C. tooreceive events, click hello appropriate receiving language in hello left-hand table of contents.</span></span>

<span data-ttu-id="fe949-109">toocomplete Bu öğreticiyi izleyerek hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="fe949-109">toocomplete this tutorial, you will need hello following:</span></span>

* <span data-ttu-id="fe949-110">Bir C geliştirme ortamı.</span><span class="sxs-lookup"><span data-stu-id="fe949-110">A C development environment.</span></span> <span data-ttu-id="fe949-111">Bu öğreticide, Azure Linux VM'de Ubuntu 14.04 ile Merhaba gcc yığın varsayacağız.</span><span class="sxs-lookup"><span data-stu-id="fe949-111">For this tutorial, we will assume hello gcc stack on an Azure Linux VM with Ubuntu 14.04.</span></span>
* <span data-ttu-id="fe949-112">[Microsoft Visual Studio](https://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="fe949-112">[Microsoft Visual Studio](https://www.visualstudio.com/).</span></span>
* <span data-ttu-id="fe949-113">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="fe949-113">An active Azure account.</span></span> <span data-ttu-id="fe949-114">Hesabınız yoksa yalnızca birkaç dakika içinde ücretsiz bir deneme sürümü hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fe949-114">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="fe949-115">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fe949-115">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="send-messages-tooevent-hubs"></a><span data-ttu-id="fe949-116">TooEvent hub iletileri gönder</span><span class="sxs-lookup"><span data-stu-id="fe949-116">Send messages tooEvent Hubs</span></span>
<span data-ttu-id="fe949-117">Bu bölümde bir C uygulama toosend olayları tooyour olay hub'ı yazma.</span><span class="sxs-lookup"><span data-stu-id="fe949-117">In this section we write a C app toosend events tooyour event hub.</span></span> <span data-ttu-id="fe949-118">Hello kodu kullanan hello Protonun durgun AMQP hello kitaplığından [Apache Qpid proje](http://qpid.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="fe949-118">hello code uses hello Proton AMQP library from hello [Apache Qpid project](http://qpid.apache.org/).</span></span> <span data-ttu-id="fe949-119">Benzer toousing Service Bus kuyrukları ve konularından AMQP c ile gösterildiği gibi budur [burada](https://code.msdn.microsoft.com/Using-Apache-Qpid-Proton-C-afd76504).</span><span class="sxs-lookup"><span data-stu-id="fe949-119">This is analogous toousing Service Bus queues and topics with AMQP from C as shown [here](https://code.msdn.microsoft.com/Using-Apache-Qpid-Proton-C-afd76504).</span></span> <span data-ttu-id="fe949-120">Daha fazla bilgi için bkz: [Qpid Proton belgelerine](http://qpid.apache.org/proton/index.html).</span><span class="sxs-lookup"><span data-stu-id="fe949-120">For more information, see [Qpid Proton documentation](http://qpid.apache.org/proton/index.html).</span></span>

1. <span data-ttu-id="fe949-121">Merhaba gelen [Qpid AMQP Messenger sayfa](https://qpid.apache.org/proton/messenger.html), ortamınıza bağlı olarak hello yönergeleri tooinstall Qpid Proton izleyin.</span><span class="sxs-lookup"><span data-stu-id="fe949-121">From hello [Qpid AMQP Messenger page](https://qpid.apache.org/proton/messenger.html), follow hello instructions tooinstall Qpid Proton, depending on your environment.</span></span>
2. <span data-ttu-id="fe949-122">toocompile Protonun durgun kitaplığı Merhaba, paketleri aşağıdaki hello yükleyin:</span><span class="sxs-lookup"><span data-stu-id="fe949-122">toocompile hello Proton library, install hello following packages:</span></span>
   
    ```shell
    sudo apt-get install build-essential cmake uuid-dev openssl libssl-dev
    ```
3. <span data-ttu-id="fe949-123">Merhaba karşıdan [Qpid Proton Kitaplığı](http://qpid.apache.org/proton/index.html)ve, örneğin ayıklayın:</span><span class="sxs-lookup"><span data-stu-id="fe949-123">Download hello [Qpid Proton library](http://qpid.apache.org/proton/index.html), and extract it, e.g.:</span></span>
   
    ```shell
    wget http://archive.apache.org/dist/qpid/proton/0.7/qpid-proton-0.7.tar.gz
    tar xvfz qpid-proton-0.7.tar.gz
    ```
4. <span data-ttu-id="fe949-124">Derleme dizini, derleme ve yükleme oluşturun:</span><span class="sxs-lookup"><span data-stu-id="fe949-124">Create a build directory, compile and install:</span></span>
   
    ```shell
    cd qpid-proton-0.7
    mkdir build
    cd build
    cmake -DCMAKE_INSTALL_PREFIX=/usr ..
    sudo make install
    ```
5. <span data-ttu-id="fe949-125">İş dizininizde adlı yeni bir dosya oluşturun **sender.c** koddan hello ile.</span><span class="sxs-lookup"><span data-stu-id="fe949-125">In your work directory, create a new file called **sender.c** with hello following code.</span></span> <span data-ttu-id="fe949-126">Olay hub'ı adı ve ad alanı adı için toosubstitute hello değer unutmayın.</span><span class="sxs-lookup"><span data-stu-id="fe949-126">Remember toosubstitute hello value for your event hub name and namespace name.</span></span> <span data-ttu-id="fe949-127">Başlangıç anahtarı hello için URL kodlanmış bir sürümü yerine gerekir **SendRule** daha önce oluşturduğunuz.</span><span class="sxs-lookup"><span data-stu-id="fe949-127">You must also substitute a URL-encoded version of hello key for hello **SendRule** created earlier.</span></span> <span data-ttu-id="fe949-128">URL kodlamak için bunu [burada](http://www.w3schools.com/tags/ref_urlencode.asp).</span><span class="sxs-lookup"><span data-stu-id="fe949-128">You can URL-encode it [here](http://www.w3schools.com/tags/ref_urlencode.asp).</span></span>
   
    ```c
    #include "proton/message.h"
    #include "proton/messenger.h"
   
    #include <getopt.h>
    #include <proton/util.h>
    #include <sys/time.h>
    #include <stddef.h>
    #include <stdio.h>
    #include <string.h>
    #include <unistd.h>
    #include <stdlib.h>
   
    #define check(messenger)                                                     
      {                                                                          
        if(pn_messenger_errno(messenger))                                        
        {                                                                        
          printf("check\n");                                                     
          die(__FILE__, __LINE__, pn_error_text(pn_messenger_error(messenger))); 
        }                                                                        
      }  
   
    pn_timestamp_t time_now(void)
    {
      struct timeval now;
      if (gettimeofday(&now, NULL)) pn_fatal("gettimeofday failed\n");
      return ((pn_timestamp_t)now.tv_sec) * 1000 + (now.tv_usec / 1000);
    }  
   
    void die(const char *file, int line, const char *message)
    {
      printf("Dead\n");
      fprintf(stderr, "%s:%i: %s\n", file, line, message);
      exit(1);
    }
   
    int sendMessage(pn_messenger_t * messenger) {
        char * address = (char *) "amqps://SendRule:{Send Rule key}@{namespace name}.servicebus.windows.net/{event hub name}";
        char * msgtext = (char *) "Hello from C!";
   
        pn_message_t * message;
        pn_data_t * body;
        message = pn_message();
   
        pn_message_set_address(message, address);
        pn_message_set_content_type(message, (char*) "application/octect-stream");
        pn_message_set_inferred(message, true);
   
        body = pn_message_body(message);
        pn_data_put_binary(body, pn_bytes(strlen(msgtext), msgtext));
   
        pn_messenger_put(messenger, message);
        check(messenger);
        pn_messenger_send(messenger, 1);
        check(messenger);
   
        pn_message_free(message);
    }
   
    int main(int argc, char** argv) {
        printf("Press Ctrl-C toostop hello sender process\n");
   
        pn_messenger_t *messenger = pn_messenger(NULL);
        pn_messenger_set_outgoing_window(messenger, 1);
        pn_messenger_start(messenger);
   
        while(true) {
            sendMessage(messenger);
            printf("Sent message\n");
            sleep(1);
        }
   
        // release messenger resources
        pn_messenger_stop(messenger);
        pn_messenger_free(messenger);
   
        return 0;
    }
    ```
6. <span data-ttu-id="fe949-129">Merhaba dosyasını derleyin varsayılarak **gcc**:</span><span class="sxs-lookup"><span data-stu-id="fe949-129">Compile hello file, assuming **gcc**:</span></span>
   
    ```
    gcc sender.c -o sender -lqpid-proton
    ```

    > [!NOTE]
    > <span data-ttu-id="fe949-130">Bu kodda 1 tooforce hello iletilerini giden bir pencerenin mümkün olan en kısa sürede kullanırız.</span><span class="sxs-lookup"><span data-stu-id="fe949-130">In this code, we use an outgoing window of 1 tooforce hello messages out as soon as possible.</span></span> <span data-ttu-id="fe949-131">Genel olarak, uygulamanızın toobatch iletileri tooincrease verimlilik denemelisiniz.</span><span class="sxs-lookup"><span data-stu-id="fe949-131">In general, your application should try toobatch messages tooincrease throughput.</span></span> <span data-ttu-id="fe949-132">Merhaba bkz [Qpid AMQP Messenger sayfa](https://qpid.apache.org/proton/messenger.html) nasıl toouse hello Qpid Proton kitaplığı bu ve diğer ortamlara ve bağlamaları sağlanan platformlar hakkında daha fazla bilgi için (şu anda Perl, PHP, Python ve Ruby).</span><span class="sxs-lookup"><span data-stu-id="fe949-132">See hello [Qpid AMQP Messenger page](https://qpid.apache.org/proton/messenger.html) for information about how toouse hello Qpid Proton library in this and other environments, and from platforms for which bindings are provided (currently Perl, PHP, Python, and Ruby).</span></span>


## <a name="next-steps"></a><span data-ttu-id="fe949-133">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fe949-133">Next steps</span></span>
<span data-ttu-id="fe949-134">Bağlantılar aşağıdaki hello ziyaret ederek Event Hubs hakkında daha fazla bilgi edinebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="fe949-134">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="fe949-135">Event Hubs’a genel bakış</span><span class="sxs-lookup"><span data-stu-id="fe949-135">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md
)
* [<span data-ttu-id="fe949-136">Olay Hub’ı oluşturma</span><span class="sxs-lookup"><span data-stu-id="fe949-136">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="fe949-137">Event Hubs ile ilgili SSS</span><span class="sxs-lookup"><span data-stu-id="fe949-137">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Images. -->
[21]: ./media/event-hubs-c-ephcs-getstarted/run-csharp-ephcs1.png
[24]: ./media/event-hubs-c-ephcs-getstarted/receive-eph-c.png
