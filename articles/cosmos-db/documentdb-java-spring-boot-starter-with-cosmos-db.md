---
title: "Yay önyükleme Starter bir Azure Cosmos DB DocumentDB API'si ile kullanma"
description: "Yay Önyükleme Başlatıcısı Azure Cosmos DB DocumentDB API'si ile oluşturulan bir uygulama yapılandırma konusunda bilgi edinin."
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
ms.openlocfilehash: 273cc750857c5e466882060a38ac0f3475811e98
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-the-spring-boot-starter-with-azure-cosmos-db-documentdb-api"></a><span data-ttu-id="e3ac3-104">Yay önyükleme Starter Azure Cosmos DB DocumentDB API'si ile kullanma</span><span class="sxs-lookup"><span data-stu-id="e3ac3-104">How to use the Spring Boot Starter with Azure Cosmos DB DocumentDB API</span></span>

## <a name="overview"></a><span data-ttu-id="e3ac3-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="e3ac3-105">Overview</span></span>

<span data-ttu-id="e3ac3-106"> **[Yay Framework]**  Java geliştiriciler kuruluş düzeyinde uygulamalar oluşturmanıza yardımcı olan bir açık kaynaklı bir çözümdür.</span><span class="sxs-lookup"><span data-stu-id="e3ac3-106">The **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="e3ac3-107">Yerleşik daha popüler projelerden biri üzerinde üst o platformudur [yay önyükleme], tek başına Java uygulamaları oluşturmak için basitleştirilmiş bir yaklaşım sağlar.</span><span class="sxs-lookup"><span data-stu-id="e3ac3-107">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="e3ac3-108">Yay önyükleme ile çalışmaya başlama geliştiricilerin yardımcı olmak için birkaç örnek yay önyükleme paketleri kullanılabilir <https://github.com/spring-guides/>.</span><span class="sxs-lookup"><span data-stu-id="e3ac3-108">To help developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="e3ac3-109">Temel yay önyükleme projeleri, listeden seçerek ek olarak  **[yay Initializr]**  özel yay önyükleme uygulamalar oluşturmaya başlamak geliştiricilere yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="e3ac3-109">In addition to choosing from the list of basic Spring Boot projects, the **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<span data-ttu-id="e3ac3-110">Azure Cosmos DB DocumentDB, MongoDB, grafik ve tablo API'leri gibi standart API'leri çeşitli kullanarak verileri geliştiricilerin izin veren bir genel dağıtılmış veritabanı hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="e3ac3-110">Azure Cosmos DB is a globally-distributed database service that allows developers to work with data using a variety of standard APIs, such as DocumentDB, MongoDB, Graph, and Table APIs.</span></span> <span data-ttu-id="e3ac3-111">Microsoft'un yay önyükleme Starter kolayca DocumentDB API'lerini kullanarak Azure Cosmos DB ile tümleştirmek yay önyükleme uygulamaları kullanmak geliştiricilere sağlar.</span><span class="sxs-lookup"><span data-stu-id="e3ac3-111">Microsoft's Spring Boot Starter enables developers to use Spring Boot applications that easily integrate with Azure Cosmos DB by using DocumentDB APIs.</span></span>

<span data-ttu-id="e3ac3-112">Bu makale bir Azure Cosmos Azure Portalı'nı kullanarak, daha sonra kullanarak DB oluşturmayı gösterir **yay Initializr** özel java uygulaması oluşturmak ve özel uygulamanızı yay önyükleme Starter işlevselliği eklemek için verileri depolamak ve DocumentDB API'sini kullanarak Azure Cosmos Veritabanından veri alın.</span><span class="sxs-lookup"><span data-stu-id="e3ac3-112">This article demonstrates creating an Azure Cosmos DB using the Azure portal, then using the **Spring Initializr** to create a custom java application, and then add the Spring Boot Starter functionality to your custom application to store data in and retrieve data from your Azure Cosmos DB by using the DocumentDB API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e3ac3-113">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="e3ac3-113">Prerequisites</span></span>

<span data-ttu-id="e3ac3-114">Bu makaledeki adımları için aşağıdaki önkoşullar gereklidir:</span><span class="sxs-lookup"><span data-stu-id="e3ac3-114">The following prerequisites are required in order to follow the steps in this article:</span></span>

* <span data-ttu-id="e3ac3-115">Bir Azure aboneliği; bir Azure aboneliği zaten sahip değilseniz, etkinleştirebilir, [MSDN abone Avantajlarınızı] veya kaydolun bir [ücretsiz Azure hesabı].</span><span class="sxs-lookup"><span data-stu-id="e3ac3-115">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>

* <span data-ttu-id="e3ac3-116">A [Java Geliştirme Seti (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), 1,7 veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="e3ac3-116">A [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>

* <span data-ttu-id="e3ac3-117">[Apache Maven](http://maven.apache.org/), sürüm 3.0 veya üstü.</span><span class="sxs-lookup"><span data-stu-id="e3ac3-117">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-an-azure-cosmos-db-by-using-the-azure-portal"></a><span data-ttu-id="e3ac3-118">Azure portalı kullanarak bir Azure Cosmos DB oluştur</span><span class="sxs-lookup"><span data-stu-id="e3ac3-118">Create an Azure Cosmos DB by using the Azure portal</span></span>

1. <span data-ttu-id="e3ac3-119">Azure portalında göz <https://portal.azure.com/> tıklatıp **+ yeni**.</span><span class="sxs-lookup"><span data-stu-id="e3ac3-119">Browse to the Azure portal at <https://portal.azure.com/> and click **+New**.</span></span>

   ![Azure portalına][AZ01]

1. <span data-ttu-id="e3ac3-121">Tıklatın **veritabanları**ve ardından **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="e3ac3-121">Click **Databases**, and then click **Azure Cosmos DB**.</span></span>

   ![Azure portalına][AZ02]

1. <span data-ttu-id="e3ac3-123">Üzerinde **Azure Cosmos DB** sayfasında, aşağıdaki bilgileri girin:</span><span class="sxs-lookup"><span data-stu-id="e3ac3-123">On the **Azure Cosmos DB** page, enter the following information:</span></span>

   * <span data-ttu-id="e3ac3-124">Benzersiz bir girin **kimliği**, veritabanınız için URI olarak kullanacağı.</span><span class="sxs-lookup"><span data-stu-id="e3ac3-124">Enter a unique **ID**, which you will use as the URI for your database.</span></span> <span data-ttu-id="e3ac3-125">Örneğin: *wingtiptoysdata.documents.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="e3ac3-125">For example: *wingtiptoysdata.documents.azure.com*.</span></span>
   * <span data-ttu-id="e3ac3-126">Seçin **SQL (belge DB)** API'si.</span><span class="sxs-lookup"><span data-stu-id="e3ac3-126">Choose **SQL (Document DB)** for the API.</span></span>
   * <span data-ttu-id="e3ac3-127">Seçin **abonelik** veritabanınız için kullanmak istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="e3ac3-127">Choose the **Subscription** you want to use for your database.</span></span>
   * <span data-ttu-id="e3ac3-128">Yeni bir oluşturulup oluşturulmayacağını belirtin **kaynak grubu** , veritabanı veya varolan bir kaynak grubu seçin.</span><span class="sxs-lookup"><span data-stu-id="e3ac3-128">Specify whether to create a new **Resource group** for your database, or choose an existing resource group.</span></span>
   * <span data-ttu-id="e3ac3-129">Belirtin **konumu** veritabanınız için.</span><span class="sxs-lookup"><span data-stu-id="e3ac3-129">Specify the **Location** for your database.</span></span>
   
   <span data-ttu-id="e3ac3-130">Bu seçenek belirtildiğinde tıklatın **oluşturma** veritabanınızı oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="e3ac3-130">When you have specified these options, click **Create** to create your database.</span></span>

   ![Azure portalına][AZ03]

1. <span data-ttu-id="e3ac3-132">Veritabanınızı oluşturduğunuzda, Azure üzerinde listelenir **Pano**altında da olarak **tüm kaynakları** ve **Azure Cosmos DB** sayfaları.</span><span class="sxs-lookup"><span data-stu-id="e3ac3-132">When your database has been created, it is listed on your Azure **Dashboard**, as well as under the **All Resources** and **Azure Cosmos DB** pages.</span></span> <span data-ttu-id="e3ac3-133">Veritabanınızı önbelleğiniz için Özellikler sayfasını açmak için bu konumların hiçbirinde tıklatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e3ac3-133">You can click on your database on any of those locations to open the properties page for your cache.</span></span>

   ![Azure portalına][AZ04]

1. <span data-ttu-id="e3ac3-135">Özellikler sayfasında Veritabanınızı görüntülenen için tıklattığınızda **erişim anahtarları** ve veritabanınız için URI ve erişim anahtarlarınızı kopyalayın; yay önyükleme uygulamanızda bu değerleri kullanır.</span><span class="sxs-lookup"><span data-stu-id="e3ac3-135">When the properties page for your database is displayed, click **Access keys** and copy your URI and access keys for your database; you will use these values in your Spring Boot application.</span></span>

   ![Azure portalına][AZ05]

## <a name="create-a-simple-spring-boot-application-with-the-spring-initializr"></a><span data-ttu-id="e3ac3-137">Yay Initializr ile basit bir yay önyükleme uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="e3ac3-137">Create a simple Spring Boot application with the Spring Initializr</span></span>

1. <span data-ttu-id="e3ac3-138">Gözat <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="e3ac3-138">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="e3ac3-139">Oluşturmak istediğiniz belirtin bir **Maven** ile proje **Java**, girin **grup** ve **yapı** adları, uygulamanız için ve düğmesini tıklatıp **proje oluştur**.</span><span class="sxs-lookup"><span data-stu-id="e3ac3-139">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Artifact** names for your application, and then click the button to **Generate Project**.</span></span>

   ![Basic yay Initializr seçenekleri][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="e3ac3-141">Yay Initializr kullanır **grup** ve **yapı** paket adı; oluşturmak için adlarını, örneğin: *com.example.wintiptoys*.</span><span class="sxs-lookup"><span data-stu-id="e3ac3-141">The Spring Initializr uses the **Group** and **Artifact** names to create the package name; for example: *com.example.wintiptoys*.</span></span>
   >

1. <span data-ttu-id="e3ac3-142">İstendiğinde, yerel bilgisayarınızda bir yola projenizi indirin.</span><span class="sxs-lookup"><span data-stu-id="e3ac3-142">When prompted, download the project to a path on your local computer.</span></span>

   ![Özel yay önyükleme projenizi indirin][SI02]

1. <span data-ttu-id="e3ac3-144">Yerel sisteminizde dosyaları ayıkladıktan sonra basit yay önyükleme uygulamanızı düzenlemek için hazır olacaktır.</span><span class="sxs-lookup"><span data-stu-id="e3ac3-144">After you have extracted the files on your local system, your simple Spring Boot application will be ready for editing.</span></span>

   ![Özel yay önyükleme proje dosyaları][SI03]

## <a name="configure-your-spring-boot-app-to-use-the-azure-spring-boot-starter"></a><span data-ttu-id="e3ac3-146">Yay önyükleme uygulamanızı Azure yay önyükleme Starter kullanacak şekilde yapılandırma</span><span class="sxs-lookup"><span data-stu-id="e3ac3-146">Configure your Spring Boot app to use the Azure Spring Boot Starter</span></span>

1. <span data-ttu-id="e3ac3-147">Bulun *pom.xml* , uygulamanızın; dizindeki dosyayı örneğin:</span><span class="sxs-lookup"><span data-stu-id="e3ac3-147">Locate the *pom.xml* file in the directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoys\pom.xml`

   <span data-ttu-id="e3ac3-148">-veya-</span><span class="sxs-lookup"><span data-stu-id="e3ac3-148">-or-</span></span>

   `/users/example/home/wingtiptoys/pom.xml`

   ![Pom.xml dosyasını bulun][PM01]

1. <span data-ttu-id="e3ac3-150">Açık *pom.xml* dosyasını bir metin düzenleyicisinde açın ve aşağıdaki satırları listesine eklemek `<dependencies>`:</span><span class="sxs-lookup"><span data-stu-id="e3ac3-150">Open the *pom.xml* file in a text editor, and add the following lines to list of `<dependencies>`:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-documentdb-spring-boot-starter</artifactId>
      <version>0.1.4</version>
   </dependency>
   ```

   ![Pom.xml dosyasını düzenleme][PM02]

1. <span data-ttu-id="e3ac3-152">Kaydet ve Kapat *pom.xml* dosya.</span><span class="sxs-lookup"><span data-stu-id="e3ac3-152">Save and close the *pom.xml* file.</span></span>

## <a name="configure-your-spring-boot-app-to-use-your-azure-cosmos-db"></a><span data-ttu-id="e3ac3-153">Yay önyükleme uygulamanızı Azure Cosmos DB kullanacak şekilde yapılandırma</span><span class="sxs-lookup"><span data-stu-id="e3ac3-153">Configure your Spring Boot app to use your Azure Cosmos DB</span></span>

1. <span data-ttu-id="e3ac3-154">Bulun *application.properties* dosyasını *kaynakları* , uygulamanızın dizin; örneğin:</span><span class="sxs-lookup"><span data-stu-id="e3ac3-154">Locate the *application.properties* file in the *resources* directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoys\src\main\resources\application.properties`

   <span data-ttu-id="e3ac3-155">-veya-</span><span class="sxs-lookup"><span data-stu-id="e3ac3-155">-or-</span></span>

   `/users/example/home/wingtiptoys/src/main/resources/application.properties`

   ![Application.properties dosyasını bulun][RE01]

1. <span data-ttu-id="e3ac3-157">Açık *application.properties* dosyasını bir metin düzenleyicisinde dosyasına aşağıdaki satırları ekleyin ve veritabanınız için uygun özelliklere sahip örnek değerleri değiştirin:</span><span class="sxs-lookup"><span data-stu-id="e3ac3-157">Open the *application.properties* file in a text editor, and add the following lines to the file, and replace the sample values with the appropriate properties for your database:</span></span>

   ```yaml
   # Specify the DNS URI of your Azure Cosmos DB.
   azure.documentdb.uri=https://wingtiptoys.documents.azure.com:443/

   # Specify the access key for your database.
   azure.documentdb.key=57686f6120447564652c20426f6220526f636b73==

   # Specify the name of your database.
   azure.documentdb.database=wingtiptoysdata
   ```

   ![Application.properties dosya düzenleme][RE02]

1. <span data-ttu-id="e3ac3-159">Kaydet ve Kapat *application.properties* dosya.</span><span class="sxs-lookup"><span data-stu-id="e3ac3-159">Save and close the *application.properties* file.</span></span>

## <a name="add-sample-code-to-implement-basic-database-functionality"></a><span data-ttu-id="e3ac3-160">Temel veritabanı işlevselliği uygulamak için örnek kod ekleme</span><span class="sxs-lookup"><span data-stu-id="e3ac3-160">Add sample code to implement basic database functionality</span></span>

<span data-ttu-id="e3ac3-161">Bu bölümde kullanıcı verilerini depolamak için iki Java sınıf oluşturun ve ardından kullanıcı sınıfının bir örneğini oluşturup, veritabanına kaydetmek için ana uygulama sınıfı değiştirin.</span><span class="sxs-lookup"><span data-stu-id="e3ac3-161">In this section you create two Java classes for storing user data, and then you modify your main application class to create an instance of the user class and save it to your database.</span></span>

### <a name="define-a-basic-class-for-storing-user-data"></a><span data-ttu-id="e3ac3-162">Kullanıcı verilerini depolamak için bir temel sınıf tanımlama</span><span class="sxs-lookup"><span data-stu-id="e3ac3-162">Define a basic class for storing user data</span></span>

1. <span data-ttu-id="e3ac3-163">Adlı yeni bir dosya oluşturun *User.java* ana uygulama Java dosyası ile aynı dizinde.</span><span class="sxs-lookup"><span data-stu-id="e3ac3-163">Create a new file named *User.java* in the same directory as your main application Java file.</span></span>

1. <span data-ttu-id="e3ac3-164">Açık *User.java* dosyasını bir metin düzenleyicisinde ve dosyasını depolayan ve veritabanınızdaki değerleri almak genel kullanıcı sınıfı tanımlamak için aşağıdaki satırları ekleyin:</span><span class="sxs-lookup"><span data-stu-id="e3ac3-164">Open the *User.java* file in a text editor, and add the following lines to the file to define a generic user class that stores and retrieve values in your database:</span></span>

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

1. <span data-ttu-id="e3ac3-165">Kaydet ve Kapat *User.java* dosya.</span><span class="sxs-lookup"><span data-stu-id="e3ac3-165">Save and close the *User.java* file.</span></span>

### <a name="define-a-data-repository-interface"></a><span data-ttu-id="e3ac3-166">Bir veri deposu arabirimi tanımlayın</span><span class="sxs-lookup"><span data-stu-id="e3ac3-166">Define a data repository interface</span></span>

1. <span data-ttu-id="e3ac3-167">Adlı yeni bir dosya oluşturun *UserRepository.java* ana uygulama Java dosyası ile aynı dizinde.</span><span class="sxs-lookup"><span data-stu-id="e3ac3-167">Create a new file named *UserRepository.java* in the same directory as your main application Java file.</span></span>

1. <span data-ttu-id="e3ac3-168">Açık *UserRepository.java* dosyasını bir metin düzenleyicisinde açın ve dosyanın varsayılan DocumentDB depo arabirimi genişleten bir kullanıcı deposu arabirimi tanımlamak için aşağıdaki satırları ekleyin:</span><span class="sxs-lookup"><span data-stu-id="e3ac3-168">Open the *UserRepository.java* file in a text editor, and add the following lines to the file to define a user repository interface that extends the default DocumentDB repository interface:</span></span>

   ```java
   package com.example.wingtiptoys;

   import com.microsoft.azure.spring.data.documentdb.repository.DocumentDbRepository;
   import org.springframework.stereotype.Repository;

   @Repository
   public interface UserRepository extends DocumentDbRepository<User, String> {}   
   ```

1. <span data-ttu-id="e3ac3-169">Kaydet ve Kapat *UserRepository.java* dosya.</span><span class="sxs-lookup"><span data-stu-id="e3ac3-169">Save and close the *UserRepository.java* file.</span></span>

### <a name="modify-the-main-application-class"></a><span data-ttu-id="e3ac3-170">Ana uygulama sınıfını değiştirme</span><span class="sxs-lookup"><span data-stu-id="e3ac3-170">Modify the main application class</span></span>

1. <span data-ttu-id="e3ac3-171">Ana uygulama Java dosyası, uygulamanızın paket dizinini bulun; Örneğin:</span><span class="sxs-lookup"><span data-stu-id="e3ac3-171">Locate the main application Java file in the package directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoys\src\main\java\com\example\wingtiptoys\WingtiptoysApplication.java`

   <span data-ttu-id="e3ac3-172">-veya-</span><span class="sxs-lookup"><span data-stu-id="e3ac3-172">-or-</span></span>

   `/users/example/home/wingtiptoys/src/main/java/com/example/wingtiptoys/WingtiptoysApplication.java`

   ![Uygulama Java dosyasını bulun][JV01]

1. <span data-ttu-id="e3ac3-174">Ana uygulama Java dosyasını bir metin düzenleyicisinde açın ve aşağıdaki satırları dosyaya ekleyin:</span><span class="sxs-lookup"><span data-stu-id="e3ac3-174">Open the main application Java file in a text editor, and add the following lines to the file:</span></span>

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

1. <span data-ttu-id="e3ac3-175">Ana uygulama Java dosyasını kaydedip kapatın.</span><span class="sxs-lookup"><span data-stu-id="e3ac3-175">Save and close the main application Java file.</span></span>

## <a name="build-and-test-your-app"></a><span data-ttu-id="e3ac3-176">Derleme ve uygulamanızı test etme</span><span class="sxs-lookup"><span data-stu-id="e3ac3-176">Build and test your app</span></span>

1. <span data-ttu-id="e3ac3-177">Bir komut istemi açın ve dizin klasörüne geçin Burada, *pom.xml* dosyasının bulunduğu; örneğin:</span><span class="sxs-lookup"><span data-stu-id="e3ac3-177">Open a command prompt and change directory to the folder where your *pom.xml* file is located; for example:</span></span>

   `cd C:\SpringBoot\wingtiptoys`

   <span data-ttu-id="e3ac3-178">-veya-</span><span class="sxs-lookup"><span data-stu-id="e3ac3-178">-or-</span></span>

   `cd /users/example/home/wingtiptoys`

1. <span data-ttu-id="e3ac3-179">Yay önyükleme uygulamanızı Maven ile ve çalıştırın; Örneğin:</span><span class="sxs-lookup"><span data-stu-id="e3ac3-179">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn package
   java -jar target/wingtiptoys-0.0.1-SNAPSHOT.jar
   ```

1. <span data-ttu-id="e3ac3-180">Uygulamanız birden fazla çalışma zamanı iletileri görüntülenir ve iletiyi görmelisiniz. `User: testFirstName testLastName` değerleri başarıyla depolanan ve, veritabanından alınan olduğunu belirtmek için görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="e3ac3-180">Your application will display several runtime messages, and you should see the message `User: testFirstName testLastName` displayed to indicate that values have been successfully stored and retrieved from your database.</span></span>

   ![Uygulama başarılı çıktısı][JV02]

1. <span data-ttu-id="e3ac3-182">İsteğe bağlı: Tıklayarak veritabanınız için Özellikler sayfasında, Azure Cosmos DB'den içeriğini görüntülemek için Azure portalını kullanabilirsiniz **belge Gezgini**ve ardından seçerek ve görüntülenen listeyi öğesinden içeriği görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="e3ac3-182">OPTIONAL: You can use the Azure portal to view the contents of your Azure Cosmos DB from the properties page for your database by clicking  **Document Explorer**, and then selecting and item from the displayed list to view the contents.</span></span>

   ![Verilerinizi görüntülemek için belge Gezgini kullanma][JV03]

## <a name="next-steps"></a><span data-ttu-id="e3ac3-184">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e3ac3-184">Next steps</span></span>

<span data-ttu-id="e3ac3-185">Azure Cosmos DB ve Java kullanma hakkında daha fazla bilgi için aşağıdaki makalelere bakın:</span><span class="sxs-lookup"><span data-stu-id="e3ac3-185">For more information about using Azure Cosmos DB and Java, see the following articles:</span></span>

* <span data-ttu-id="e3ac3-186">[Azure Cosmos DB belgelerine].</span><span class="sxs-lookup"><span data-stu-id="e3ac3-186">[Azure Cosmos DB Documentation].</span></span>

* <span data-ttu-id="e3ac3-187">[Azure Cosmos DB: Java ve Azure portal ile bir DocumentDB API uygulaması oluşturma][Build a DocumentDB API app with Java]</span><span class="sxs-lookup"><span data-stu-id="e3ac3-187">[Azure Cosmos DB: Build a DocumentDB API app with Java and the Azure portal][Build a DocumentDB API app with Java]</span></span>

<span data-ttu-id="e3ac3-188">Azure üzerinde yay önyükleme uygulamalarında kullanma hakkında daha fazla bilgi için aşağıdaki makalelere bakın:</span><span class="sxs-lookup"><span data-stu-id="e3ac3-188">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="e3ac3-189">Azure için yay önyükleme DocumenDB Başlatıcı</span><span class="sxs-lookup"><span data-stu-id="e3ac3-189">Spring Boot DocumenDB Starter for Azure</span></span>](https://github.com/Microsoft/azure-spring-boot-starters/tree/master/azure-documentdb-spring-boot-starter-sample)

* [<span data-ttu-id="e3ac3-190">Yay önyükleme uygulamasını Azure App Service'e dağıtma</span><span class="sxs-lookup"><span data-stu-id="e3ac3-190">Deploy a Spring Boot Application to the Azure App Service</span></span>](../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)

* [<span data-ttu-id="e3ac3-191">Azure kapsayıcı hizmeti Kubernetes kümesinde bir yay önyükleme uygulama çalıştıran</span><span class="sxs-lookup"><span data-stu-id="e3ac3-191">Running a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](../container-service/container-service-deploy-spring-boot-app-on-kubernetes.md)

<span data-ttu-id="e3ac3-192">Azure’u Java ile kullanma hakkında daha fazla bilgi edinmek için bkz. [Azure Java Geliştirici Merkezi] ve [Visual Studio Team Services için Java Araçları].</span><span class="sxs-lookup"><span data-stu-id="e3ac3-192">For more information about using Azure with Java, see the [Azure Java Developer Center] and the [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

<span data-ttu-id="e3ac3-193">[Azure Cosmos DB belgelerine]: /azure/cosmos-db/</span><span class="sxs-lookup"><span data-stu-id="e3ac3-193">[Azure Cosmos DB Documentation]: /azure/cosmos-db/</span></span>
<span data-ttu-id="e3ac3-194">[Azure Java Geliştirici Merkezi]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="e3ac3-194">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
[Build a DocumentDB API app with Java]: https://docs.microsoft.com/azure/cosmos-db/create-documentdb-java
<span data-ttu-id="e3ac3-195">[ücretsiz Azure hesabı]: https://azure.microsoft.com/pricing/free-trial/</span><span class="sxs-lookup"><span data-stu-id="e3ac3-195">[free Azure account]: https://azure.microsoft.com/pricing/free-trial/</span></span>
<span data-ttu-id="e3ac3-196">[Visual Studio Team Services için Java Araçları]: https://java.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="e3ac3-196">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span></span>
<span data-ttu-id="e3ac3-197">[MSDN abone Avantajlarınızı]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/</span><span class="sxs-lookup"><span data-stu-id="e3ac3-197">[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/</span></span>
<span data-ttu-id="e3ac3-198">[yay önyükleme]: http://projects.spring.io/spring-boot/</span><span class="sxs-lookup"><span data-stu-id="e3ac3-198">[Spring Boot]: http://projects.spring.io/spring-boot/</span></span>
<span data-ttu-id="e3ac3-199">[yay Initializr]: https://start.spring.io/</span><span class="sxs-lookup"><span data-stu-id="e3ac3-199">[Spring Initializr]: https://start.spring.io/</span></span>
<span data-ttu-id="e3ac3-200">[Yay Framework]: https://spring.io/</span><span class="sxs-lookup"><span data-stu-id="e3ac3-200">[Spring Framework]: https://spring.io/</span></span>

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
