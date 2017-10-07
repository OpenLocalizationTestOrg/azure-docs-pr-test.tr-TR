---
title: "aaaHow toouse hello yay önyükleme Starter bir Azure Cosmos DB DocumentDB API'si"
description: "Bir uygulama tooconfigure hello yay önyükleme Başlatıcı hello Azure Cosmos DB DocumentDB API ile birlikte nasıl oluşturulacağını öğrenin."
services: cosmos-db
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
keywords: "İlkbahar, yay önyükleme Starter Cosmos DB"
ms.assetid: 
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 08/08/2017
ms.author: robmcm;yungez;kevinzha
ms.openlocfilehash: a2c6de678f850676cb2887e224e5c12950db0e53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-spring-boot-starter-with-azure-cosmos-db-documentdb-api"></a><span data-ttu-id="f1468-104">Nasıl toouse hello Azure Cosmos DB DocumentDB API ile yay önyükleme Başlatıcı</span><span class="sxs-lookup"><span data-stu-id="f1468-104">How toouse hello Spring Boot Starter with Azure Cosmos DB DocumentDB API</span></span>

## <a name="overview"></a><span data-ttu-id="f1468-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="f1468-105">Overview</span></span>

<span data-ttu-id="f1468-106">Merhaba  **[yay Framework]**  Java geliştiriciler kuruluş düzeyinde uygulamalar oluşturmanıza yardımcı olan bir açık kaynaklı bir çözümdür.</span><span class="sxs-lookup"><span data-stu-id="f1468-106">hello **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="f1468-107">Yerleşik hello daha popüler projelerden biri üzerinde üst o platformudur [yay önyükleme], tek başına Java uygulamaları oluşturmak için basitleştirilmiş bir yaklaşım sağlar.</span><span class="sxs-lookup"><span data-stu-id="f1468-107">One of hello more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="f1468-108">toohelp geliştiriciler yay önyüklemesini Başlarken, birkaç örnek yay önyükleme paketleri kullanılabilir <https://github.com/spring-guides/>.</span><span class="sxs-lookup"><span data-stu-id="f1468-108">toohelp developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="f1468-109">Buna ek olarak temel yay önyükleme hello listesinden toochoosing, hello projeleri  **[yay Initializr]**  özel yay önyükleme uygulamalar oluşturmaya başlamak geliştiricilere yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="f1468-109">In addition toochoosing from hello list of basic Spring Boot projects, hello **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<span data-ttu-id="f1468-110">Azure Cosmos DB, geliştiricilerin sağlayan bir genel dağıtılmış veritabanı hizmetidir toowork DocumentDB, MongoDB, grafik ve tablo API'leri gibi standart API'leri çeşitli kullanarak verileri.</span><span class="sxs-lookup"><span data-stu-id="f1468-110">Azure Cosmos DB is a globally-distributed database service that allows developers toowork with data using a variety of standard APIs, such as DocumentDB, MongoDB, Graph, and Table APIs.</span></span> <span data-ttu-id="f1468-111">Microsoft'un yay önyükleme Starter kolayca DocumentDB API'lerini kullanarak Azure Cosmos DB ile tümleştirmek geliştiriciler toouse yay önyükleme uygulamaları etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="f1468-111">Microsoft's Spring Boot Starter enables developers toouse Spring Boot applications that easily integrate with Azure Cosmos DB by using DocumentDB APIs.</span></span>

<span data-ttu-id="f1468-112">Bu makale bir Azure Cosmos hello Azure portal kullanarak, daha sonra hello kullanarak DB oluşturmayı gösterir **yay Initializr** toocreate özel java uygulaması ve hello yay önyükleme Starter işlevselliği tooyour özel ekleyin Uygulama toostore verileri ve DB'den, Azure Cosmos hello DocumentDB API kullanarak verileri almak.</span><span class="sxs-lookup"><span data-stu-id="f1468-112">This article demonstrates creating an Azure Cosmos DB using hello Azure portal, then using hello **Spring Initializr** toocreate a custom java application, and then add hello Spring Boot Starter functionality tooyour custom application toostore data in and retrieve data from your Azure Cosmos DB by using hello DocumentDB API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f1468-113">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="f1468-113">Prerequisites</span></span>

<span data-ttu-id="f1468-114">Önkoşullar aşağıdaki hello bu makaledeki sipariş toofollow hello adımlar gereklidir:</span><span class="sxs-lookup"><span data-stu-id="f1468-114">hello following prerequisites are required in order toofollow hello steps in this article:</span></span>

* <span data-ttu-id="f1468-115">Bir Azure aboneliği; bir Azure aboneliği zaten sahip değilseniz, etkinleştirebilir, [MSDN abone Avantajlarınızı] veya kaydolun bir [ücretsiz Azure hesabı].</span><span class="sxs-lookup"><span data-stu-id="f1468-115">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>

* <span data-ttu-id="f1468-116">A [Java Geliştirme Seti (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), 1,7 veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="f1468-116">A [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>

* <span data-ttu-id="f1468-117">[Apache Maven](http://maven.apache.org/), sürüm 3.0 veya üstü.</span><span class="sxs-lookup"><span data-stu-id="f1468-117">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-an-azure-cosmos-db-by-using-hello-azure-portal"></a><span data-ttu-id="f1468-118">Bir Azure Cosmos DB hello Azure portal kullanarak oluşturma</span><span class="sxs-lookup"><span data-stu-id="f1468-118">Create an Azure Cosmos DB by using hello Azure portal</span></span>

1. <span data-ttu-id="f1468-119">Toohello Azure göz atın, portal <https://portal.azure.com/> tıklatıp **+ yeni**.</span><span class="sxs-lookup"><span data-stu-id="f1468-119">Browse toohello Azure portal at <https://portal.azure.com/> and click **+New**.</span></span>

   ![Azure portalına][AZ01]

1. <span data-ttu-id="f1468-121">Tıklatın **veritabanları**ve ardından **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="f1468-121">Click **Databases**, and then click **Azure Cosmos DB**.</span></span>

   ![Azure portalına][AZ02]

1. <span data-ttu-id="f1468-123">Merhaba üzerinde **Azure Cosmos DB** sayfasında, aşağıdaki bilgilerle hello girin:</span><span class="sxs-lookup"><span data-stu-id="f1468-123">On hello **Azure Cosmos DB** page, enter hello following information:</span></span>

   * <span data-ttu-id="f1468-124">Benzersiz bir girin **kimliği**, veritabanınız için URI hello olarak kullanacağı.</span><span class="sxs-lookup"><span data-stu-id="f1468-124">Enter a unique **ID**, which you will use as hello URI for your database.</span></span> <span data-ttu-id="f1468-125">Örneğin: *wingtiptoysdata.documents.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="f1468-125">For example: *wingtiptoysdata.documents.azure.com*.</span></span>
   * <span data-ttu-id="f1468-126">Seçin **SQL (belge DB)** hello API için.</span><span class="sxs-lookup"><span data-stu-id="f1468-126">Choose **SQL (Document DB)** for hello API.</span></span>
   * <span data-ttu-id="f1468-127">Merhaba seçin **abonelik** veritabanınız için toouse istiyor.</span><span class="sxs-lookup"><span data-stu-id="f1468-127">Choose hello **Subscription** you want toouse for your database.</span></span>
   * <span data-ttu-id="f1468-128">Belirtin olup olmadığını toocreate yeni bir **kaynak grubu** , veritabanı veya varolan bir kaynak grubu seçin.</span><span class="sxs-lookup"><span data-stu-id="f1468-128">Specify whether toocreate a new **Resource group** for your database, or choose an existing resource group.</span></span>
   * <span data-ttu-id="f1468-129">Merhaba belirtin **konumu** veritabanınız için.</span><span class="sxs-lookup"><span data-stu-id="f1468-129">Specify hello **Location** for your database.</span></span>
   
   <span data-ttu-id="f1468-130">Bu seçenek belirtildiğinde tıklatın **oluşturma** toocreate veritabanınızı.</span><span class="sxs-lookup"><span data-stu-id="f1468-130">When you have specified these options, click **Create** toocreate your database.</span></span>

   ![Azure portalına][AZ03]

1. <span data-ttu-id="f1468-132">Veritabanınızı oluşturduğunuzda, Azure üzerinde listelenir **Pano**, hello gibi altında yanı **tüm kaynakları** ve **Azure Cosmos DB** sayfaları.</span><span class="sxs-lookup"><span data-stu-id="f1468-132">When your database has been created, it is listed on your Azure **Dashboard**, as well as under hello **All Resources** and **Azure Cosmos DB** pages.</span></span> <span data-ttu-id="f1468-133">Veritabanınızın herhangi bu konumları tooopen hello Özellikler sayfasının önbelleğiniz için tıklatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f1468-133">You can click on your database on any of those locations tooopen hello properties page for your cache.</span></span>

   ![Azure portalına][AZ04]

1. <span data-ttu-id="f1468-135">Veritabanınız için Hello Özellikler sayfası görüntülendiğinde tıklayın **erişim anahtarları** ve veritabanınız için URI ve erişim anahtarlarınızı kopyalayın; yay önyükleme uygulamanızda bu değerleri kullanır.</span><span class="sxs-lookup"><span data-stu-id="f1468-135">When hello properties page for your database is displayed, click **Access keys** and copy your URI and access keys for your database; you will use these values in your Spring Boot application.</span></span>

   ![Azure portalına][AZ05]

## <a name="create-a-simple-spring-boot-application-with-hello-spring-initializr"></a><span data-ttu-id="f1468-137">Yay Initializr hello ile basit bir yay önyükleme uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="f1468-137">Create a simple Spring Boot application with hello Spring Initializr</span></span>

1. <span data-ttu-id="f1468-138">Çok Gözat<https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="f1468-138">Browse too<https://start.spring.io/>.</span></span>

1. <span data-ttu-id="f1468-139">Toogenerate istediğinizi belirtin bir **Maven** ile proje **Java**, hello girin **grup** ve **yapı** , uygulamanız için adları ve ardından hello çok düğmesini**proje oluştur**.</span><span class="sxs-lookup"><span data-stu-id="f1468-139">Specify that you want toogenerate a **Maven** project with **Java**, enter hello **Group** and **Artifact** names for your application, and then click hello button too**Generate Project**.</span></span>

   ![Basic yay Initializr seçenekleri][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="f1468-141">Merhaba yay Initializr kullanan hello **grup** ve **yapı** adları toocreate hello paket adı; örneğin: *com.example.wintiptoys*.</span><span class="sxs-lookup"><span data-stu-id="f1468-141">hello Spring Initializr uses hello **Group** and **Artifact** names toocreate hello package name; for example: *com.example.wintiptoys*.</span></span>
   >

1. <span data-ttu-id="f1468-142">İstendiğinde, yerel bilgisayarınızda hello proje tooa yolu indirin.</span><span class="sxs-lookup"><span data-stu-id="f1468-142">When prompted, download hello project tooa path on your local computer.</span></span>

   ![Özel yay önyükleme projenizi indirin][SI02]

1. <span data-ttu-id="f1468-144">Yerel sisteminizde hello dosyaları ayıkladıktan sonra basit yay önyükleme uygulamanızı düzenlemek için hazır olacaktır.</span><span class="sxs-lookup"><span data-stu-id="f1468-144">After you have extracted hello files on your local system, your simple Spring Boot application will be ready for editing.</span></span>

   ![Özel yay önyükleme proje dosyaları][SI03]

## <a name="configure-your-spring-boot-app-toouse-hello-azure-spring-boot-starter"></a><span data-ttu-id="f1468-146">Yay önyükleme uygulama toouse hello Azure yay önyükleme Starter yapılandırın</span><span class="sxs-lookup"><span data-stu-id="f1468-146">Configure your Spring Boot app toouse hello Azure Spring Boot Starter</span></span>

1. <span data-ttu-id="f1468-147">Merhaba bulun *pom.xml* , uygulamanızın; hello dizindeki dosyayı örneğin:</span><span class="sxs-lookup"><span data-stu-id="f1468-147">Locate hello *pom.xml* file in hello directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoys\pom.xml`

   <span data-ttu-id="f1468-148">-veya-</span><span class="sxs-lookup"><span data-stu-id="f1468-148">-or-</span></span>

   `/users/example/home/wingtiptoys/pom.xml`

   ![Merhaba pom.xml dosyasını bulun][PM01]

1. <span data-ttu-id="f1468-150">Açık hello *pom.xml* dosyasını bir metin düzenleyicisinde ve satırları toolist, aşağıdaki hello ekleyin `<dependencies>`:</span><span class="sxs-lookup"><span data-stu-id="f1468-150">Open hello *pom.xml* file in a text editor, and add hello following lines toolist of `<dependencies>`:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-documentdb-spring-boot-starter</artifactId>
      <version>0.1.4</version>
   </dependency>
   ```

   ![Merhaba pom.xml dosyasını düzenleme][PM02]

1. <span data-ttu-id="f1468-152">Kaydet ve Kapat hello *pom.xml* dosya.</span><span class="sxs-lookup"><span data-stu-id="f1468-152">Save and close hello *pom.xml* file.</span></span>

## <a name="configure-your-spring-boot-app-toouse-your-azure-cosmos-db"></a><span data-ttu-id="f1468-153">Yay önyükleme uygulama toouse Azure Cosmos DB yapılandırın</span><span class="sxs-lookup"><span data-stu-id="f1468-153">Configure your Spring Boot app toouse your Azure Cosmos DB</span></span>

1. <span data-ttu-id="f1468-154">Merhaba bulun *application.properties* hello dosyasında *kaynakları* , uygulamanızın dizin; örneğin:</span><span class="sxs-lookup"><span data-stu-id="f1468-154">Locate hello *application.properties* file in hello *resources* directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoys\src\main\resources\application.properties`

   <span data-ttu-id="f1468-155">-veya-</span><span class="sxs-lookup"><span data-stu-id="f1468-155">-or-</span></span>

   `/users/example/home/wingtiptoys/src/main/resources/application.properties`

   ![Merhaba application.properties dosyasını bulun][RE01]

1. <span data-ttu-id="f1468-157">Açık hello *application.properties* dosyasını bir metin düzenleyicisinde ve aşağıdaki satırları toohello dosyasına hello ekleyin ve hello veritabanınız için uygun özelliklere sahip hello örnek değerleri değiştirin:</span><span class="sxs-lookup"><span data-stu-id="f1468-157">Open hello *application.properties* file in a text editor, and add hello following lines toohello file, and replace hello sample values with hello appropriate properties for your database:</span></span>

   ```yaml
   # Specify hello DNS URI of your Azure Cosmos DB.
   azure.documentdb.uri=https://wingtiptoys.documents.azure.com:443/

   # Specify hello access key for your database.
   azure.documentdb.key=57686f6120447564652c20426f6220526f636b73==

   # Specify hello name of your database.
   azure.documentdb.database=wingtiptoysdata
   ```

   ![Merhaba application.properties dosya düzenleme][RE02]

1. <span data-ttu-id="f1468-159">Kaydet ve Kapat hello *application.properties* dosya.</span><span class="sxs-lookup"><span data-stu-id="f1468-159">Save and close hello *application.properties* file.</span></span>

## <a name="add-sample-code-tooimplement-basic-database-functionality"></a><span data-ttu-id="f1468-160">Örnek kod tooimplement temel veritabanı işlevselliği ekleme</span><span class="sxs-lookup"><span data-stu-id="f1468-160">Add sample code tooimplement basic database functionality</span></span>

<span data-ttu-id="f1468-161">Bu bölümde, kullanıcı verilerini depolamak için iki Java sınıfları oluşturmak ve ardından ana uygulama sınıfı toocreate hello kullanıcı sınıfının bir örneğini değiştirmek ve tooyour veritabanına kaydedin.</span><span class="sxs-lookup"><span data-stu-id="f1468-161">In this section you create two Java classes for storing user data, and then you modify your main application class toocreate an instance of hello user class and save it tooyour database.</span></span>

### <a name="define-a-basic-class-for-storing-user-data"></a><span data-ttu-id="f1468-162">Kullanıcı verilerini depolamak için bir temel sınıf tanımlama</span><span class="sxs-lookup"><span data-stu-id="f1468-162">Define a basic class for storing user data</span></span>

1. <span data-ttu-id="f1468-163">Adlı yeni bir dosya oluşturun *User.java* hello içindeki ana uygulama Java dosyası ile aynı dizinde.</span><span class="sxs-lookup"><span data-stu-id="f1468-163">Create a new file named *User.java* in hello same directory as your main application Java file.</span></span>

1. <span data-ttu-id="f1468-164">Açık hello *User.java* dosyasını bir metin düzenleyicisinde ve hello aşağıdaki depolayan ve veritabanınızdaki değerleri almak genel kullanıcı sınıfı toohello dosya toodefine satırları ekleyin:</span><span class="sxs-lookup"><span data-stu-id="f1468-164">Open hello *User.java* file in a text editor, and add hello following lines toohello file toodefine a generic user class that stores and retrieve values in your database:</span></span>

   ```java
   package com.example.wingtiptoys;

   public class User {
      private String id;
      private String firstName;
      private String lastName;
 
      public User(String id, String firstName, String lastName) {
         this.id = id;
         this.firstName = firstName;
         this.lastName = lastName;
      }
   
      public String getId() {
         return this.id;
      }

      public void setId(String id) {
         this.id = id;
      }

      public String getFirstName() {
         return firstName;
      }

      public void setFirstName(String firstName) {
         this.firstName = firstName;
      }

      public String getLastName() {
         return lastName;
      }

      public void setLastName(String lastName) {
         this.lastName = lastName;
      }

      @Override
      public String toString() {
         return String.format("User: %s %s", firstName, lastName);
      }
   }
   ```

1. <span data-ttu-id="f1468-165">Kaydet ve Kapat hello *User.java* dosya.</span><span class="sxs-lookup"><span data-stu-id="f1468-165">Save and close hello *User.java* file.</span></span>

### <a name="define-a-data-repository-interface"></a><span data-ttu-id="f1468-166">Bir veri deposu arabirimi tanımlayın</span><span class="sxs-lookup"><span data-stu-id="f1468-166">Define a data repository interface</span></span>

1. <span data-ttu-id="f1468-167">Adlı yeni bir dosya oluşturun *UserRepository.java* hello içindeki ana uygulama Java dosyası ile aynı dizinde.</span><span class="sxs-lookup"><span data-stu-id="f1468-167">Create a new file named *UserRepository.java* in hello same directory as your main application Java file.</span></span>

1. <span data-ttu-id="f1468-168">Açık hello *UserRepository.java* dosyasını bir metin düzenleyicisinde ve hello aşağıdaki hello varsayılan DocumentDB depo arabirimi genişleten bir kullanıcı deposu arabirimi toohello dosya toodefine satırları ekleyin:</span><span class="sxs-lookup"><span data-stu-id="f1468-168">Open hello *UserRepository.java* file in a text editor, and add hello following lines toohello file toodefine a user repository interface that extends hello default DocumentDB repository interface:</span></span>

   ```java
   package com.example.wingtiptoys;

   import com.microsoft.azure.spring.data.documentdb.repository.DocumentDbRepository;
   import org.springframework.stereotype.Repository;

   @Repository
   public interface UserRepository extends DocumentDbRepository<User, String> {}   
   ```

1. <span data-ttu-id="f1468-169">Kaydet ve Kapat hello *UserRepository.java* dosya.</span><span class="sxs-lookup"><span data-stu-id="f1468-169">Save and close hello *UserRepository.java* file.</span></span>

### <a name="modify-hello-main-application-class"></a><span data-ttu-id="f1468-170">Merhaba ana uygulama sınıfını değiştirme</span><span class="sxs-lookup"><span data-stu-id="f1468-170">Modify hello main application class</span></span>

1. <span data-ttu-id="f1468-171">Merhaba ana uygulama Java dosyası, uygulamanızın paket dizinine hello bulun; Örneğin:</span><span class="sxs-lookup"><span data-stu-id="f1468-171">Locate hello main application Java file in hello package directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoys\src\main\java\com\example\wingtiptoys\WingtiptoysApplication.java`

   <span data-ttu-id="f1468-172">-veya-</span><span class="sxs-lookup"><span data-stu-id="f1468-172">-or-</span></span>

   `/users/example/home/wingtiptoys/src/main/java/com/example/wingtiptoys/WingtiptoysApplication.java`

   ![Merhaba uygulama Java dosyasını bulun][JV01]

1. <span data-ttu-id="f1468-174">Merhaba ana uygulama Java dosyası bir metin düzenleyicisinde açın ve aşağıdaki satırları toohello dosyasına hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="f1468-174">Open hello main application Java file in a text editor, and add hello following lines toohello file:</span></span>

   ```java
   package com.example.wingtiptoys;

   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.boot.CommandLineRunner;

   @SpringBootApplication
   public class WingtiptoysApplication implements CommandLineRunner {

      @Autowired
      private UserRepository repository;
    
      public static void main(String[] args) {
         SpringApplication.run(WingtiptoysApplication.class, args);
      }

      public void run(String... var1) throws Exception {
         final User testUser = new User("testId", "testFirstName", "testLastName");

         repository.deleteAll();
         repository.save(testUser);

         final User result = repository.findOne(testUser.getId());

         System.out.printf("\n\n%s\n\n",result.toString());
      }
   }
   ```

1. <span data-ttu-id="f1468-175">Merhaba ana uygulama Java dosyasını kaydedip kapatın.</span><span class="sxs-lookup"><span data-stu-id="f1468-175">Save and close hello main application Java file.</span></span>

## <a name="build-and-test-your-app"></a><span data-ttu-id="f1468-176">Derleme ve uygulamanızı test etme</span><span class="sxs-lookup"><span data-stu-id="f1468-176">Build and test your app</span></span>

1. <span data-ttu-id="f1468-177">Bir komut istemi açın ve dizin toohello klasörü Değiştir Burada, *pom.xml* dosyasının bulunduğu; örneğin:</span><span class="sxs-lookup"><span data-stu-id="f1468-177">Open a command prompt and change directory toohello folder where your *pom.xml* file is located; for example:</span></span>

   `cd C:\SpringBoot\wingtiptoys`

   <span data-ttu-id="f1468-178">-veya-</span><span class="sxs-lookup"><span data-stu-id="f1468-178">-or-</span></span>

   `cd /users/example/home/wingtiptoys`

1. <span data-ttu-id="f1468-179">Yay önyükleme uygulamanızı Maven ile ve çalıştırın; Örneğin:</span><span class="sxs-lookup"><span data-stu-id="f1468-179">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn package
   java -jar target/wingtiptoys-0.0.1-SNAPSHOT.jar
   ```

1. <span data-ttu-id="f1468-180">Uygulamanız birden fazla çalışma zamanı iletileri görüntülenir ve selamlama iletisine görmelisiniz. `User: testFirstName testLastName` değerleri başarıyla depolanan ve, veritabanından alınan olduğunu tooindicate görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="f1468-180">Your application will display several runtime messages, and you should see hello message `User: testFirstName testLastName` displayed tooindicate that values have been successfully stored and retrieved from your database.</span></span>

   ![Merhaba uygulaması başarılı çıktısı][JV02]

1. <span data-ttu-id="f1468-182">İsteğe bağlı: Hello Azure portal tooview hello hello özellikleri sayfasında, Azure Cosmos DB'den içeriğini veritabanınız için tıklayarak kullanabileceğiniz **belge Gezgini**ve ardından seçerek ve de görüntülenen hello listesi tooview hello öğesinden içeriği.</span><span class="sxs-lookup"><span data-stu-id="f1468-182">OPTIONAL: You can use hello Azure portal tooview hello contents of your Azure Cosmos DB from hello properties page for your database by clicking  **Document Explorer**, and then selecting and item from hello displayed list tooview hello contents.</span></span>

   ![Verilerinizi Hello belge Gezgini tooview kullanma][JV03]

## <a name="next-steps"></a><span data-ttu-id="f1468-184">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f1468-184">Next steps</span></span>

<span data-ttu-id="f1468-185">Azure Cosmos DB ve Java kullanma hakkında daha fazla bilgi için aşağıdaki makaleler hello bakın:</span><span class="sxs-lookup"><span data-stu-id="f1468-185">For more information about using Azure Cosmos DB and Java, see hello following articles:</span></span>

* <span data-ttu-id="f1468-186">[Azure Cosmos DB belgelerine].</span><span class="sxs-lookup"><span data-stu-id="f1468-186">[Azure Cosmos DB Documentation].</span></span>

* <span data-ttu-id="f1468-187">[Azure Cosmos DB: Java ile DocumentDB API uygulaması oluşturma ve Azure portal hello][Build a DocumentDB API app with Java]</span><span class="sxs-lookup"><span data-stu-id="f1468-187">[Azure Cosmos DB: Build a DocumentDB API app with Java and hello Azure portal][Build a DocumentDB API app with Java]</span></span>

<span data-ttu-id="f1468-188">Azure üzerinde yay önyükleme uygulamalarında kullanma hakkında daha fazla bilgi için aşağıdaki makaleler hello bakın:</span><span class="sxs-lookup"><span data-stu-id="f1468-188">For more information about using Spring Boot applications on Azure, see hello following articles:</span></span>

* [<span data-ttu-id="f1468-189">Azure için yay önyükleme DocumenDB Başlatıcı</span><span class="sxs-lookup"><span data-stu-id="f1468-189">Spring Boot DocumenDB Starter for Azure</span></span>](https://github.com/Microsoft/azure-spring-boot-starters/tree/master/azure-documentdb-spring-boot-starter-sample)

* [<span data-ttu-id="f1468-190">Yay önyükleme uygulama toohello Azure App Service'e dağıtma</span><span class="sxs-lookup"><span data-stu-id="f1468-190">Deploy a Spring Boot Application toohello Azure App Service</span></span>](../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)

* [<span data-ttu-id="f1468-191">Yay önyükleme uygulama hello Azure kapsayıcı hizmeti Kubernetes kümede çalışan</span><span class="sxs-lookup"><span data-stu-id="f1468-191">Running a Spring Boot Application on a Kubernetes Cluster in hello Azure Container Service</span></span>](../container-service/container-service-deploy-spring-boot-app-on-kubernetes.md)

<span data-ttu-id="f1468-192">Azure Java ile kullanma hakkında daha fazla bilgi için bkz: Merhaba [Azure Java Geliştirici Merkezi] ve hello [Visual Studio Team Services için Java Araçları].</span><span class="sxs-lookup"><span data-stu-id="f1468-192">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

[Azure Cosmos DB belgelerine]: /azure/cosmos-db/
[Azure Java Geliştirici Merkezi]: https://azure.microsoft.com/develop/java/
[Build a DocumentDB API app with Java]: https://docs.microsoft.com/azure/cosmos-db/create-documentdb-java
[ücretsiz Azure hesabı]: https://azure.microsoft.com/pricing/free-trial/
[Visual Studio Team Services için Java Araçları]: https://java.visualstudio.com/
[MSDN abone Avantajlarınızı]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[yay önyükleme]: http://projects.spring.io/spring-boot/
[yay Initializr]: https://start.spring.io/
[yay Framework]: https://spring.io/

<!-- IMG List -->

[AZ01]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/AZ01.png
[AZ02]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/AZ02.png
[AZ03]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/AZ03.png
[AZ04]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/AZ04.png
[AZ05]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/AZ05.png

[SI01]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/SI01.png
[SI02]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/SI02.png
[SI03]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/SI03.png

[RE01]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/RE01.png
[RE02]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/RE02.png

[PM01]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/PM01.png
[PM02]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/PM02.png

[JV01]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/JV01.png
[JV02]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/JV02.png
[JV03]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/JV03.png
