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
# <a name="send-events-tooazure-event-hubs-using-c"></a>Olayları tooAzure olay hub'ın C kullanarak Gönder

## <a name="introduction"></a>Giriş
Olay hub'ları bir uygulama tooprocess etkinleştirme saniye başına milyonlarca olayı alma ve veri bağlı cihazlarınız ve uygulamalarınız tarafından üretilen oldukça büyük miktardaki hello analiz bir yüksek düzeyde ölçeklenebilir bir alım sistem olur. Bir olay hub'ına toplandığında, dönüştürme ve herhangi bir gerçek zamanlı analiz sağlayıcısı veya depolama kümesi kullanarak verileri depolar.

Daha fazla bilgi için lütfen bkz hello [Event Hubs'a genel bakış] [Event Hubs'a genel bakış].

Bu öğreticide şunları öğreneceksiniz nasıl hello uygun alıcı dilde hello sol İçindekiler C. tooreceive olaylarında bir konsol uygulaması kullanarak toosend olayları tooan olay hub'ı tıklatın.

toocomplete Bu öğreticiyi izleyerek hello gerekir:

* Bir C geliştirme ortamı. Bu öğreticide, Azure Linux VM'de Ubuntu 14.04 ile Merhaba gcc yığın varsayacağız.
* [Microsoft Visual Studio](https://www.visualstudio.com/).
* Etkin bir Azure hesabı. Hesabınız yoksa yalnızca birkaç dakika içinde ücretsiz bir deneme sürümü hesabı oluşturabilirsiniz. Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/).

## <a name="send-messages-tooevent-hubs"></a>TooEvent hub iletileri gönder
Bu bölümde bir C uygulama toosend olayları tooyour olay hub'ı yazma. Hello kodu kullanan hello Protonun durgun AMQP hello kitaplığından [Apache Qpid proje](http://qpid.apache.org/). Benzer toousing Service Bus kuyrukları ve konularından AMQP c ile gösterildiği gibi budur [burada](https://code.msdn.microsoft.com/Using-Apache-Qpid-Proton-C-afd76504). Daha fazla bilgi için bkz: [Qpid Proton belgelerine](http://qpid.apache.org/proton/index.html).

1. Merhaba gelen [Qpid AMQP Messenger sayfa](https://qpid.apache.org/proton/messenger.html), ortamınıza bağlı olarak hello yönergeleri tooinstall Qpid Proton izleyin.
2. toocompile Protonun durgun kitaplığı Merhaba, paketleri aşağıdaki hello yükleyin:
   
    ```shell
    sudo apt-get install build-essential cmake uuid-dev openssl libssl-dev
    ```
3. Merhaba karşıdan [Qpid Proton Kitaplığı](http://qpid.apache.org/proton/index.html)ve, örneğin ayıklayın:
   
    ```shell
    wget http://archive.apache.org/dist/qpid/proton/0.7/qpid-proton-0.7.tar.gz
    tar xvfz qpid-proton-0.7.tar.gz
    ```
4. Derleme dizini, derleme ve yükleme oluşturun:
   
    ```shell
    cd qpid-proton-0.7
    mkdir build
    cd build
    cmake -DCMAKE_INSTALL_PREFIX=/usr ..
    sudo make install
    ```
5. İş dizininizde adlı yeni bir dosya oluşturun **sender.c** koddan hello ile. Olay hub'ı adı ve ad alanı adı için toosubstitute hello değer unutmayın. Başlangıç anahtarı hello için URL kodlanmış bir sürümü yerine gerekir **SendRule** daha önce oluşturduğunuz. URL kodlamak için bunu [burada](http://www.w3schools.com/tags/ref_urlencode.asp).
   
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
6. Merhaba dosyasını derleyin varsayılarak **gcc**:
   
    ```
    gcc sender.c -o sender -lqpid-proton
    ```

    > [!NOTE]
    > Bu kodda 1 tooforce hello iletilerini giden bir pencerenin mümkün olan en kısa sürede kullanırız. Genel olarak, uygulamanızın toobatch iletileri tooincrease verimlilik denemelisiniz. Merhaba bkz [Qpid AMQP Messenger sayfa](https://qpid.apache.org/proton/messenger.html) nasıl toouse hello Qpid Proton kitaplığı bu ve diğer ortamlara ve bağlamaları sağlanan platformlar hakkında daha fazla bilgi için (şu anda Perl, PHP, Python ve Ruby).


## <a name="next-steps"></a>Sonraki adımlar
Bağlantılar aşağıdaki hello ziyaret ederek Event Hubs hakkında daha fazla bilgi edinebilirsiniz:

* [Event Hubs’a genel bakış](event-hubs-what-is-event-hubs.md
)
* [Olay Hub’ı oluşturma](event-hubs-create.md)
* [Event Hubs ile ilgili SSS](event-hubs-faq.md)

<!-- Images. -->
[21]: ./media/event-hubs-c-ephcs-getstarted/run-csharp-ephcs1.png
[24]: ./media/event-hubs-c-ephcs-getstarted/receive-eph-c.png
