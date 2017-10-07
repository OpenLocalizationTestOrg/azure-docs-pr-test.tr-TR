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
# <a name="how-tooconfigure-a-spring-boot-initializer-app-toouse-redis-cache"></a><span data-ttu-id="1601b-104">Nasıl tooconfigure yay önyükleme Başlatıcı uygulama toouse Redis önbelleği</span><span class="sxs-lookup"><span data-stu-id="1601b-104">How tooconfigure a Spring Boot Initializer app toouse Redis Cache</span></span>

## <a name="overview"></a><span data-ttu-id="1601b-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="1601b-105">Overview</span></span>

<span data-ttu-id="1601b-106">Merhaba  **[yay Framework]**  Java geliştiriciler kuruluş düzeyinde uygulamalar oluşturmanıza yardımcı olan bir açık kaynak çözümüdür.</span><span class="sxs-lookup"><span data-stu-id="1601b-106">hello **[Spring Framework]** is an open-source solution which helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="1601b-107">Yerleşik hello daha popüler projeleri üzerinde üst o platform biri [yay önyükleme], tek başına Java uygulamaları oluşturmak için basitleştirilmiş bir yaklaşım sağlar.</span><span class="sxs-lookup"><span data-stu-id="1601b-107">One of hello more-popular projects which is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="1601b-108">toohelp geliştiriciler yay önyüklemesini Başlarken, birkaç örnek yay önyükleme paketleri kullanılabilir <https://github.com/spring-guides/>.</span><span class="sxs-lookup"><span data-stu-id="1601b-108">toohelp developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="1601b-109">Buna ek olarak temel yay önyükleme hello listesinden toochoosing, hello projeleri  **[yay Initializr]**  özel yay önyükleme uygulamalar oluşturmaya başlamak geliştiricilere yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="1601b-109">In addition toochoosing from hello list of basic Spring Boot projects, hello **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<span data-ttu-id="1601b-110">Bu makalede hello hello kullanarak Azure portal kullanarak Redis önbelleği oluşturma ile anlatılmaktadır **yay Initializr** toocreate özel bir uygulama ve Java oluşturma web kullanarak verileri alır ve bunlara uygulaması, Redis önbelleği.</span><span class="sxs-lookup"><span data-stu-id="1601b-110">This article walks you through creating a Redis cache using hello Azure portal, then using hello **Spring Initializr** toocreate a custom application, and then creating a Java web application which stores and retrieves data using your Redis cache.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1601b-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="1601b-111">Prerequisites</span></span>

<span data-ttu-id="1601b-112">Önkoşullar aşağıdaki hello bu makaledeki sipariş toofollow hello adımlar gereklidir:</span><span class="sxs-lookup"><span data-stu-id="1601b-112">hello following prerequisites are required in order toofollow hello steps in this article:</span></span>

* <span data-ttu-id="1601b-113">Bir Azure aboneliği; bir Azure aboneliği zaten sahip değilseniz, etkinleştirebilir, [MSDN abone Avantajlarınızı] veya kaydolun bir [ücretsiz Azure hesabı].</span><span class="sxs-lookup"><span data-stu-id="1601b-113">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>

* <span data-ttu-id="1601b-114">A [Java Geliştirme Seti (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), 1,7 veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="1601b-114">A [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>

* <span data-ttu-id="1601b-115">[Apache Maven](http://maven.apache.org/), sürüm 3.0 veya üstü.</span><span class="sxs-lookup"><span data-stu-id="1601b-115">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-a-redis-cache-on-azure"></a><span data-ttu-id="1601b-116">Azure’da Redis Cache oluşturma</span><span class="sxs-lookup"><span data-stu-id="1601b-116">Create a Redis cache on Azure</span></span>

1. <span data-ttu-id="1601b-117">Toohello Azure göz atın, portal <https://portal.azure.com/> ve hello öğesini **+ yeni**.</span><span class="sxs-lookup"><span data-stu-id="1601b-117">Browse toohello Azure portal at <https://portal.azure.com/> and click hello item for **+New**.</span></span>

   ![Azure portalına][AZ01]

1. <span data-ttu-id="1601b-119">Tıklatın **veritabanı**ve ardından **Redis önbelleği**.</span><span class="sxs-lookup"><span data-stu-id="1601b-119">Click **Database**, and then click **Redis Cache**.</span></span>

   ![Azure portalına][AZ02]

1. <span data-ttu-id="1601b-121">Merhaba üzerinde **yeni Redis önbelleği** hello want **DNS adı** önbelleğiniz için ardından belirtin, **abonelik**, **kaynak grubu**,  **Konum**, ve **fiyatlandırma katmanı**.</span><span class="sxs-lookup"><span data-stu-id="1601b-121">On hello **New Redis Cache** page, enter hello **DNS name** for your cache, then specify your **Subscription**, **Resource group**, **Location**, and **Pricing tier**.</span></span> <span data-ttu-id="1601b-122">Bu seçenek belirtildiğinde tıklatın **oluşturma** toocreate önbelleğiniz.</span><span class="sxs-lookup"><span data-stu-id="1601b-122">When you have specified these options, click **Create** toocreate your cache.</span></span>

   ![Azure portalına][AZ03]

1. <span data-ttu-id="1601b-124">Önbelleğinizi tamamlandığında, Azure üzerinde listelendiğini göreceksiniz **Pano**, hello gibi altında yanı **tüm kaynakları**, ve **Redis önbellekleri** sayfaları.</span><span class="sxs-lookup"><span data-stu-id="1601b-124">Once your cache has been completed, you will see it listed on your Azure **Dashboard**, as well as under hello **All Resources**, and **Redis Caches** pages.</span></span> <span data-ttu-id="1601b-125">Önbelleğinizi herhangi bu konumları tooopen hello Özellikler sayfasının önbelleğiniz için tıklatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1601b-125">You can click on your cache on any of those locations tooopen hello properties page for your cache.</span></span>

   ![Azure portalına][AZ04]

1. <span data-ttu-id="1601b-127">Merhaba önbelleğiniz için özelliklerin listesini içeren hello sayfası görüntülendiğinde tıklayın **erişim anahtarları** ve önbelleğiniz için erişim tuşlarınızı kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="1601b-127">When hello page which contains hello list of properties for your cache is displayed, click **Access keys** and copy your access keys for your cache.</span></span>

   ![Azure portalına][AZ05]

## <a name="create-a-custom-application-using-hello-spring-initializr"></a><span data-ttu-id="1601b-129">Merhaba yay Initializr kullanarak özel bir uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="1601b-129">Create a custom application using hello Spring Initializr</span></span>

1. <span data-ttu-id="1601b-130">Çok Gözat<https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="1601b-130">Browse too<https://start.spring.io/>.</span></span>

1. <span data-ttu-id="1601b-131">Toogenerate istediğinizi belirtin bir **Maven** ile proje **Java**, hello girin **grup** ve **Aritifact** , uygulamanız için adları ve ardından hello bağlantıyı çok**anahtar toohello tam sürüm** hello yay Initializr.</span><span class="sxs-lookup"><span data-stu-id="1601b-131">Specify that you want toogenerate a **Maven** project with **Java**, enter hello **Group** and **Aritifact** names for your application, and then click hello link too**Switch toohello full version** of hello Spring Initializr.</span></span>

   ![Basic yay Initializr seçenekleri][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="1601b-133">Merhaba yay Initializr hello kullanacağınız **grup** ve **Aritifact** adları toocreate hello paket adı; örneğin: *com.contoso.myazuredemo*.</span><span class="sxs-lookup"><span data-stu-id="1601b-133">hello Spring Initializr will use hello **Group** and **Aritifact** names toocreate hello package name; for example: *com.contoso.myazuredemo*.</span></span>
   >

1. <span data-ttu-id="1601b-134">Toohello aşağı kaydırın **Web** bölümünde ve hello kutuyu **Web**, toohello kaydırarak **NoSQL** bölümünde ve hello kutuyu **Redis**hello sayfanın toohello kaydırın ve çok olarak hello düğmesini**proje oluştur**.</span><span class="sxs-lookup"><span data-stu-id="1601b-134">Scroll down toohello **Web** section and check hello box for **Web**, then scroll down toohello **NoSQL** section and check hello box for **Redis**, then scroll toohello bottom of hello page and click hello button too**Generate Project**.</span></span>

   ![Tam yay Initializr seçenekleri][SI02]

1. <span data-ttu-id="1601b-136">İstendiğinde, yerel bilgisayarınızda hello proje tooa yolu indirin.</span><span class="sxs-lookup"><span data-stu-id="1601b-136">When prompted, download hello project tooa path on your local computer.</span></span>

   ![Özel yay önyükleme projenizi indirin][SI03]

1. <span data-ttu-id="1601b-138">Yerel sisteminizde hello dosyaları ayıkladıktan sonra özel yay önyükleme uygulamanız düzenleme için hazır olacaktır.</span><span class="sxs-lookup"><span data-stu-id="1601b-138">After you have extracted hello files on your local system, your custom Spring Boot application will be ready for editing.</span></span>

   ![Özel yay önyükleme proje dosyaları][SI04]

## <a name="configure-your-custom-spring-boot-toouse-your-redis-cache"></a><span data-ttu-id="1601b-140">Redis önbelleği özel yay önyükleme toouse yapılandırın</span><span class="sxs-lookup"><span data-stu-id="1601b-140">Configure your custom Spring Boot toouse your Redis Cache</span></span>

1. <span data-ttu-id="1601b-141">Merhaba bulun *application.properties* hello dosyasında *kaynakları* , uygulamanızın dizin veya zaten yoksa, hello dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1601b-141">Locate hello *application.properties* file in hello *resources* directory of your app, or create hello file if it does not already exist.</span></span>

   ![Merhaba application.properties dosyasını bulun][RE01]

1. <span data-ttu-id="1601b-143">Açık hello *application.properties* dosyasını bir metin düzenleyicisinde ve aşağıdaki satırları toohello dosyasına hello ekleyin ve önbelleğiniz uygun özelliklerinden hello hello örnek değerleri değiştirin:</span><span class="sxs-lookup"><span data-stu-id="1601b-143">Open hello *application.properties* file in a text editor, and add hello following lines toohello file, and replace hello sample values with hello appropriate properties from your cache:</span></span>

   ```yaml
   # Specify hello DNS URI of your Redis cache.
   spring.redis.host=myspringbootcache.redis.cache.windows.net

   # Specify hello port for your Redis cache.
   spring.redis.port=6380

   # Specify hello access key for your Redis cache.
   spring.redis.password=57686f6120447564652c2049495320526f636b73=
   ```

   ![Merhaba application.properties dosya düzenleme][RE02]

1. <span data-ttu-id="1601b-145">Kaydet ve Kapat hello *application.properties* dosya.</span><span class="sxs-lookup"><span data-stu-id="1601b-145">Save and close hello *application.properties* file.</span></span>

1. <span data-ttu-id="1601b-146">Adlı bir klasör oluşturun *denetleyicisi* paketinize; hello kaynak klasörü altında örneğin:</span><span class="sxs-lookup"><span data-stu-id="1601b-146">Create a folder named *controller* under hello source folder for your package; for example:</span></span>

   `C:\SpringBoot\myazuredemo\src\main\java\com\contoso\myazuredemo\controller`

   <span data-ttu-id="1601b-147">-veya-</span><span class="sxs-lookup"><span data-stu-id="1601b-147">-or-</span></span>

   `/users/example/home/myazuredemo/src/main/java/com/contoso/myazuredemo/controller`

1. <span data-ttu-id="1601b-148">Adlı yeni bir dosya oluşturun *HelloController.java* hello içinde *denetleyicisi* klasör.</span><span class="sxs-lookup"><span data-stu-id="1601b-148">Create a new file named *HelloController.java* in hello *controller* folder.</span></span> <span data-ttu-id="1601b-149">Merhaba dosyasını bir metin düzenleyicisinde açın ve aşağıdaki kodu tooit hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="1601b-149">Open hello file in a text editor and add hello following code tooit:</span></span>

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
   
   <span data-ttu-id="1601b-150">Burada gerekir tooreplace `com.contoso.myazuredemo` projeniz için hello paket adı ile.</span><span class="sxs-lookup"><span data-stu-id="1601b-150">Where you will need tooreplace `com.contoso.myazuredemo` with hello package name for your project.</span></span>

1. <span data-ttu-id="1601b-151">Kaydet ve Kapat hello *HelloController.java* dosya.</span><span class="sxs-lookup"><span data-stu-id="1601b-151">Save and close hello *HelloController.java* file.</span></span>

1. <span data-ttu-id="1601b-152">Yay önyükleme uygulamanızı Maven ile ve çalıştırın; Örneğin:</span><span class="sxs-lookup"><span data-stu-id="1601b-152">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. <span data-ttu-id="1601b-153">Bir web tarayıcısı kullanarak toohttp://localhost:8080 göz atarak Hello web uygulaması test veya curl kullanılabilir varsa aşağıdaki örneğine hello gibi hello sözdizimini kullanın:</span><span class="sxs-lookup"><span data-stu-id="1601b-153">Test hello web app by browsing toohttp://localhost:8080 using a web browser, or use hello syntax like hello following example if you have curl available:</span></span>

   ```shell
   curl http://localhost:8080
   ```

   <span data-ttu-id="1601b-154">"Hello World!" Merhaba görmeniz gerekir</span><span class="sxs-lookup"><span data-stu-id="1601b-154">You should see hello "Hello World!"</span></span> <span data-ttu-id="1601b-155">hangi Redis önbellekten dinamik olarak alındığını görüntülenen örnek denetleyicinizi ileti.</span><span class="sxs-lookup"><span data-stu-id="1601b-155">message from your sample controller displayed, which is being retrieved dynamically from your Redis cache.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1601b-156">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1601b-156">Next steps</span></span>

<span data-ttu-id="1601b-157">Azure üzerinde yay önyükleme uygulamalarında kullanma hakkında daha fazla bilgi için aşağıdaki makaleler hello bakın:</span><span class="sxs-lookup"><span data-stu-id="1601b-157">For more information about using Spring Boot applications on Azure, see hello following articles:</span></span>

* [<span data-ttu-id="1601b-158">Yay önyükleme uygulama toohello Azure App Service'e dağıtma</span><span class="sxs-lookup"><span data-stu-id="1601b-158">Deploy a Spring Boot Application toohello Azure App Service</span></span>](../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)

* [<span data-ttu-id="1601b-159">Yay önyükleme uygulama hello Azure kapsayıcı hizmeti Kubernetes kümede çalışan</span><span class="sxs-lookup"><span data-stu-id="1601b-159">Running a Spring Boot Application on a Kubernetes Cluster in hello Azure Container Service</span></span>](../container-service/container-service-deploy-spring-boot-app-on-kubernetes.md)

<span data-ttu-id="1601b-160">Azure Java ile kullanma hakkında daha fazla bilgi için bkz: Merhaba [Azure Java Geliştirici Merkezi] ve hello [Visual Studio Team Services için Java Araçları].</span><span class="sxs-lookup"><span data-stu-id="1601b-160">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="1601b-161">Redis önbelleği ile Azure üzerinde Java kullanmaya başlama hakkında daha fazla bilgi görmek için [nasıl toouse Azure Redis önbelleği ile Java][Redis Cache with Java].</span><span class="sxs-lookup"><span data-stu-id="1601b-161">For more information about getting started using Redis Cache with Java on Azure, see [How toouse Azure Redis Cache with Java][Redis Cache with Java].</span></span>

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
