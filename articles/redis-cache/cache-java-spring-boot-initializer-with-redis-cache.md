---
title: "aaaHow tooconfigure yay önyükleme Başlatıcı uygulama toouse Redis önbelleği"
description: "Tooconfigure yay önyükleme uygulama hello yay Initializr toouse Azure Redis önbelleği nasıl oluşturulacağını öğrenin."
services: redis-cache
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
keywords: "İlkbahar, yay önyükleme Starter, Redis önbelleği"
ms.assetid: 
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: java
ms.topic: article
ms.date: 7/21/2017
ms.author: robmcm;zhijzhao;yidon
ms.openlocfilehash: ad532c88d2d67b97079eeb0e0e392add29ac365b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-a-spring-boot-initializer-app-toouse-redis-cache"></a>Nasıl tooconfigure yay önyükleme Başlatıcı uygulama toouse Redis önbelleği

## <a name="overview"></a>Genel Bakış

Merhaba  **[yay Framework]**  Java geliştiriciler kuruluş düzeyinde uygulamalar oluşturmanıza yardımcı olan bir açık kaynak çözümüdür. Yerleşik hello daha popüler projeleri üzerinde üst o platform biri [yay önyükleme], tek başına Java uygulamaları oluşturmak için basitleştirilmiş bir yaklaşım sağlar. toohelp geliştiriciler yay önyüklemesini Başlarken, birkaç örnek yay önyükleme paketleri kullanılabilir <https://github.com/spring-guides/>. Buna ek olarak temel yay önyükleme hello listesinden toochoosing, hello projeleri  **[yay Initializr]**  özel yay önyükleme uygulamalar oluşturmaya başlamak geliştiricilere yardımcı olur.

Bu makalede hello hello kullanarak Azure portal kullanarak Redis önbelleği oluşturma ile anlatılmaktadır **yay Initializr** toocreate özel bir uygulama ve Java oluşturma web kullanarak verileri alır ve bunlara uygulaması, Redis önbelleği.

## <a name="prerequisites"></a>Ön koşullar

Önkoşullar aşağıdaki hello bu makaledeki sipariş toofollow hello adımlar gereklidir:

* Bir Azure aboneliği; bir Azure aboneliği zaten sahip değilseniz, etkinleştirebilir, [MSDN abone Avantajlarınızı] veya kaydolun bir [ücretsiz Azure hesabı].

* A [Java Geliştirme Seti (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), 1,7 veya sonraki bir sürümü.

* [Apache Maven](http://maven.apache.org/), sürüm 3.0 veya üstü.

## <a name="create-a-redis-cache-on-azure"></a>Azure’da Redis Cache oluşturma

1. Toohello Azure göz atın, portal <https://portal.azure.com/> ve hello öğesini **+ yeni**.

   ![Azure portalına][AZ01]

1. Tıklatın **veritabanı**ve ardından **Redis önbelleği**.

   ![Azure portalına][AZ02]

1. Merhaba üzerinde **yeni Redis önbelleği** hello want **DNS adı** önbelleğiniz için ardından belirtin, **abonelik**, **kaynak grubu**,  **Konum**, ve **fiyatlandırma katmanı**. Bu seçenek belirtildiğinde tıklatın **oluşturma** toocreate önbelleğiniz.

   ![Azure portalına][AZ03]

1. Önbelleğinizi tamamlandığında, Azure üzerinde listelendiğini göreceksiniz **Pano**, hello gibi altında yanı **tüm kaynakları**, ve **Redis önbellekleri** sayfaları. Önbelleğinizi herhangi bu konumları tooopen hello Özellikler sayfasının önbelleğiniz için tıklatabilirsiniz.

   ![Azure portalına][AZ04]

1. Merhaba önbelleğiniz için özelliklerin listesini içeren hello sayfası görüntülendiğinde tıklayın **erişim anahtarları** ve önbelleğiniz için erişim tuşlarınızı kopyalayın.

   ![Azure portalına][AZ05]

## <a name="create-a-custom-application-using-hello-spring-initializr"></a>Merhaba yay Initializr kullanarak özel bir uygulama oluşturma

1. Çok Gözat<https://start.spring.io/>.

1. Toogenerate istediğinizi belirtin bir **Maven** ile proje **Java**, hello girin **grup** ve **Aritifact** , uygulamanız için adları ve ardından hello bağlantıyı çok**anahtar toohello tam sürüm** hello yay Initializr.

   ![Basic yay Initializr seçenekleri][SI01]

   > [!NOTE]
   >
   > Merhaba yay Initializr hello kullanacağınız **grup** ve **Aritifact** adları toocreate hello paket adı; örneğin: *com.contoso.myazuredemo*.
   >

1. Toohello aşağı kaydırın **Web** bölümünde ve hello kutuyu **Web**, toohello kaydırarak **NoSQL** bölümünde ve hello kutuyu **Redis**hello sayfanın toohello kaydırın ve çok olarak hello düğmesini**proje oluştur**.

   ![Tam yay Initializr seçenekleri][SI02]

1. İstendiğinde, yerel bilgisayarınızda hello proje tooa yolu indirin.

   ![Özel yay önyükleme projenizi indirin][SI03]

1. Yerel sisteminizde hello dosyaları ayıkladıktan sonra özel yay önyükleme uygulamanız düzenleme için hazır olacaktır.

   ![Özel yay önyükleme proje dosyaları][SI04]

## <a name="configure-your-custom-spring-boot-toouse-your-redis-cache"></a>Redis önbelleği özel yay önyükleme toouse yapılandırın

1. Merhaba bulun *application.properties* hello dosyasında *kaynakları* , uygulamanızın dizin veya zaten yoksa, hello dosyası oluşturun.

   ![Merhaba application.properties dosyasını bulun][RE01]

1. Açık hello *application.properties* dosyasını bir metin düzenleyicisinde ve aşağıdaki satırları toohello dosyasına hello ekleyin ve önbelleğiniz uygun özelliklerinden hello hello örnek değerleri değiştirin:

   ```yaml
   # Specify hello DNS URI of your Redis cache.
   spring.redis.host=myspringbootcache.redis.cache.windows.net

   # Specify hello port for your Redis cache.
   spring.redis.port=6380

   # Specify hello access key for your Redis cache.
   spring.redis.password=57686f6120447564652c2049495320526f636b73=
   ```

   ![Merhaba application.properties dosya düzenleme][RE02]

1. Kaydet ve Kapat hello *application.properties* dosya.

1. Adlı bir klasör oluşturun *denetleyicisi* paketinize; hello kaynak klasörü altında örneğin:

   `C:\SpringBoot\myazuredemo\src\main\java\com\contoso\myazuredemo\controller`

   -veya-

   `/users/example/home/myazuredemo/src/main/java/com/contoso/myazuredemo/controller`

1. Adlı yeni bir dosya oluşturun *HelloController.java* hello içinde *denetleyicisi* klasör. Merhaba dosyasını bir metin düzenleyicisinde açın ve aşağıdaki kodu tooit hello ekleyin:

   ```java
   package com.contoso.myazuredemo;

   import org.springframework.web.bind.annotation.RequestMapping;
   import org.springframework.web.bind.annotation.RestController;
   import org.springframework.beans.factory.annotation.Value;
   import redis.clients.jedis.Jedis;
   import redis.clients.jedis.JedisShardInfo;

   @RestController
   public class HelloController {
   
      // Retrieve hello DNS name for your cache.
      @Value("${spring.redis.host}")
      private String redisHost;

      // Retrieve hello port for your cache.
      @Value("${spring.redis.port}")
      private int redisPort;

      // Retrieve hello access key for your cache.
      @Value("${spring.redis.password}")
      private String redisPassword;

      @RequestMapping("/")
      // Define hello Hello World controller.
      public String hello() {
      
         // Create a JedisShardInfo object tooconnect tooyour Redis cache.
         JedisShardInfo jedisShardInfo = new JedisShardInfo(redisHost, redisPort, true);
         // Specify your access key.
         jedisShardInfo.setPassword(redisPassword);
         // Create a Jedis object toostore/retrieve information from your cache.
         Jedis jedis = new Jedis(jedisShardInfo);

         // Add a Hello World string tooyour cache.
         jedis.set("greeting", "Hello World!");

         // Return hello string from your cache.
         return jedis.get("greeting");
      }
   }
   ```
   
   Burada gerekir tooreplace `com.contoso.myazuredemo` projeniz için hello paket adı ile.

1. Kaydet ve Kapat hello *HelloController.java* dosya.

1. Yay önyükleme uygulamanızı Maven ile ve çalıştırın; Örneğin:

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. Bir web tarayıcısı kullanarak toohttp://localhost:8080 göz atarak Hello web uygulaması test veya curl kullanılabilir varsa aşağıdaki örneğine hello gibi hello sözdizimini kullanın:

   ```shell
   curl http://localhost:8080
   ```

   "Hello World!" Merhaba görmeniz gerekir hangi Redis önbellekten dinamik olarak alındığını görüntülenen örnek denetleyicinizi ileti.

## <a name="next-steps"></a>Sonraki adımlar

Azure üzerinde yay önyükleme uygulamalarında kullanma hakkında daha fazla bilgi için aşağıdaki makaleler hello bakın:

* [Yay önyükleme uygulama toohello Azure App Service'e dağıtma](../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)

* [Yay önyükleme uygulama hello Azure kapsayıcı hizmeti Kubernetes kümede çalışan](../container-service/container-service-deploy-spring-boot-app-on-kubernetes.md)

Azure Java ile kullanma hakkında daha fazla bilgi için bkz: Merhaba [Azure Java Geliştirici Merkezi] ve hello [Visual Studio Team Services için Java Araçları].

Redis önbelleği ile Azure üzerinde Java kullanmaya başlama hakkında daha fazla bilgi görmek için [nasıl toouse Azure Redis önbelleği ile Java][Redis Cache with Java].

<!-- URL List -->

[Azure Java Geliştirici Merkezi]: https://azure.microsoft.com/develop/java/
[ücretsiz Azure hesabı]: https://azure.microsoft.com/pricing/free-trial/
[Visual Studio Team Services için Java Araçları]: https://java.visualstudio.com/
[MSDN abone Avantajlarınızı]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[yay önyükleme]: http://projects.spring.io/spring-boot/
[yay Initializr]: https://start.spring.io/
[yay Framework]: https://spring.io/
[Redis Cache with Java]: cache-java-get-started.md

<!-- IMG List -->

[AZ01]: ./media/cache-java-spring-boot-initializer-with-redis-cache/AZ01.png
[AZ02]: ./media/cache-java-spring-boot-initializer-with-redis-cache/AZ02.png
[AZ03]: ./media/cache-java-spring-boot-initializer-with-redis-cache/AZ03.png
[AZ04]: ./media/cache-java-spring-boot-initializer-with-redis-cache/AZ04.png
[AZ05]: ./media/cache-java-spring-boot-initializer-with-redis-cache/AZ05.png

[SI01]: ./media/cache-java-spring-boot-initializer-with-redis-cache/SI01.png
[SI02]: ./media/cache-java-spring-boot-initializer-with-redis-cache/SI02.png
[SI03]: ./media/cache-java-spring-boot-initializer-with-redis-cache/SI03.png
[SI04]: ./media/cache-java-spring-boot-initializer-with-redis-cache/SI04.png

[RE01]: ./media/cache-java-spring-boot-initializer-with-redis-cache/RE01.png
[RE02]: ./media/cache-java-spring-boot-initializer-with-redis-cache/RE02.png
