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
# <a name="how-toouse-hello-spring-boot-starter-with-azure-cosmos-db-documentdb-api"></a>Nasıl toouse hello Azure Cosmos DB DocumentDB API ile yay önyükleme Başlatıcı

## <a name="overview"></a>Genel Bakış

Merhaba  **[yay Framework]**  Java geliştiriciler kuruluş düzeyinde uygulamalar oluşturmanıza yardımcı olan bir açık kaynaklı bir çözümdür. Yerleşik hello daha popüler projelerden biri üzerinde üst o platformudur [yay önyükleme], tek başına Java uygulamaları oluşturmak için basitleştirilmiş bir yaklaşım sağlar. toohelp geliştiriciler yay önyüklemesini Başlarken, birkaç örnek yay önyükleme paketleri kullanılabilir <https://github.com/spring-guides/>. Buna ek olarak temel yay önyükleme hello listesinden toochoosing, hello projeleri  **[yay Initializr]**  özel yay önyükleme uygulamalar oluşturmaya başlamak geliştiricilere yardımcı olur.

Azure Cosmos DB, geliştiricilerin sağlayan bir genel dağıtılmış veritabanı hizmetidir toowork DocumentDB, MongoDB, grafik ve tablo API'leri gibi standart API'leri çeşitli kullanarak verileri. Microsoft'un yay önyükleme Starter kolayca DocumentDB API'lerini kullanarak Azure Cosmos DB ile tümleştirmek geliştiriciler toouse yay önyükleme uygulamaları etkinleştirir.

Bu makale bir Azure Cosmos hello Azure portal kullanarak, daha sonra hello kullanarak DB oluşturmayı gösterir **yay Initializr** toocreate özel java uygulaması ve hello yay önyükleme Starter işlevselliği tooyour özel ekleyin Uygulama toostore verileri ve DB'den, Azure Cosmos hello DocumentDB API kullanarak verileri almak.

## <a name="prerequisites"></a>Ön koşullar

Önkoşullar aşağıdaki hello bu makaledeki sipariş toofollow hello adımlar gereklidir:

* Bir Azure aboneliği; bir Azure aboneliği zaten sahip değilseniz, etkinleştirebilir, [MSDN abone Avantajlarınızı] veya kaydolun bir [ücretsiz Azure hesabı].

* A [Java Geliştirme Seti (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), 1,7 veya sonraki bir sürümü.

* [Apache Maven](http://maven.apache.org/), sürüm 3.0 veya üstü.

## <a name="create-an-azure-cosmos-db-by-using-hello-azure-portal"></a>Bir Azure Cosmos DB hello Azure portal kullanarak oluşturma

1. Toohello Azure göz atın, portal <https://portal.azure.com/> tıklatıp **+ yeni**.

   ![Azure portalına][AZ01]

1. Tıklatın **veritabanları**ve ardından **Azure Cosmos DB**.

   ![Azure portalına][AZ02]

1. Merhaba üzerinde **Azure Cosmos DB** sayfasında, aşağıdaki bilgilerle hello girin:

   * Benzersiz bir girin **kimliği**, veritabanınız için URI hello olarak kullanacağı. Örneğin: *wingtiptoysdata.documents.azure.com*.
   * Seçin **SQL (belge DB)** hello API için.
   * Merhaba seçin **abonelik** veritabanınız için toouse istiyor.
   * Belirtin olup olmadığını toocreate yeni bir **kaynak grubu** , veritabanı veya varolan bir kaynak grubu seçin.
   * Merhaba belirtin **konumu** veritabanınız için.
   
   Bu seçenek belirtildiğinde tıklatın **oluşturma** toocreate veritabanınızı.

   ![Azure portalına][AZ03]

1. Veritabanınızı oluşturduğunuzda, Azure üzerinde listelenir **Pano**, hello gibi altında yanı **tüm kaynakları** ve **Azure Cosmos DB** sayfaları. Veritabanınızın herhangi bu konumları tooopen hello Özellikler sayfasının önbelleğiniz için tıklatabilirsiniz.

   ![Azure portalına][AZ04]

1. Veritabanınız için Hello Özellikler sayfası görüntülendiğinde tıklayın **erişim anahtarları** ve veritabanınız için URI ve erişim anahtarlarınızı kopyalayın; yay önyükleme uygulamanızda bu değerleri kullanır.

   ![Azure portalına][AZ05]

## <a name="create-a-simple-spring-boot-application-with-hello-spring-initializr"></a>Yay Initializr hello ile basit bir yay önyükleme uygulaması oluşturma

1. Çok Gözat<https://start.spring.io/>.

1. Toogenerate istediğinizi belirtin bir **Maven** ile proje **Java**, hello girin **grup** ve **yapı** , uygulamanız için adları ve ardından hello çok düğmesini**proje oluştur**.

   ![Basic yay Initializr seçenekleri][SI01]

   > [!NOTE]
   >
   > Merhaba yay Initializr kullanan hello **grup** ve **yapı** adları toocreate hello paket adı; örneğin: *com.example.wintiptoys*.
   >

1. İstendiğinde, yerel bilgisayarınızda hello proje tooa yolu indirin.

   ![Özel yay önyükleme projenizi indirin][SI02]

1. Yerel sisteminizde hello dosyaları ayıkladıktan sonra basit yay önyükleme uygulamanızı düzenlemek için hazır olacaktır.

   ![Özel yay önyükleme proje dosyaları][SI03]

## <a name="configure-your-spring-boot-app-toouse-hello-azure-spring-boot-starter"></a>Yay önyükleme uygulama toouse hello Azure yay önyükleme Starter yapılandırın

1. Merhaba bulun *pom.xml* , uygulamanızın; hello dizindeki dosyayı örneğin:

   `C:\SpringBoot\wingtiptoys\pom.xml`

   -veya-

   `/users/example/home/wingtiptoys/pom.xml`

   ![Merhaba pom.xml dosyasını bulun][PM01]

1. Açık hello *pom.xml* dosyasını bir metin düzenleyicisinde ve satırları toolist, aşağıdaki hello ekleyin `<dependencies>`:

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-documentdb-spring-boot-starter</artifactId>
      <version>0.1.4</version>
   </dependency>
   ```

   ![Merhaba pom.xml dosyasını düzenleme][PM02]

1. Kaydet ve Kapat hello *pom.xml* dosya.

## <a name="configure-your-spring-boot-app-toouse-your-azure-cosmos-db"></a>Yay önyükleme uygulama toouse Azure Cosmos DB yapılandırın

1. Merhaba bulun *application.properties* hello dosyasında *kaynakları* , uygulamanızın dizin; örneğin:

   `C:\SpringBoot\wingtiptoys\src\main\resources\application.properties`

   -veya-

   `/users/example/home/wingtiptoys/src/main/resources/application.properties`

   ![Merhaba application.properties dosyasını bulun][RE01]

1. Açık hello *application.properties* dosyasını bir metin düzenleyicisinde ve aşağıdaki satırları toohello dosyasına hello ekleyin ve hello veritabanınız için uygun özelliklere sahip hello örnek değerleri değiştirin:

   ```yaml
   # Specify hello DNS URI of your Azure Cosmos DB.
   azure.documentdb.uri=https://wingtiptoys.documents.azure.com:443/

   # Specify hello access key for your database.
   azure.documentdb.key=57686f6120447564652c20426f6220526f636b73==

   # Specify hello name of your database.
   azure.documentdb.database=wingtiptoysdata
   ```

   ![Merhaba application.properties dosya düzenleme][RE02]

1. Kaydet ve Kapat hello *application.properties* dosya.

## <a name="add-sample-code-tooimplement-basic-database-functionality"></a>Örnek kod tooimplement temel veritabanı işlevselliği ekleme

Bu bölümde, kullanıcı verilerini depolamak için iki Java sınıfları oluşturmak ve ardından ana uygulama sınıfı toocreate hello kullanıcı sınıfının bir örneğini değiştirmek ve tooyour veritabanına kaydedin.

### <a name="define-a-basic-class-for-storing-user-data"></a>Kullanıcı verilerini depolamak için bir temel sınıf tanımlama

1. Adlı yeni bir dosya oluşturun *User.java* hello içindeki ana uygulama Java dosyası ile aynı dizinde.

1. Açık hello *User.java* dosyasını bir metin düzenleyicisinde ve hello aşağıdaki depolayan ve veritabanınızdaki değerleri almak genel kullanıcı sınıfı toohello dosya toodefine satırları ekleyin:

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

1. Kaydet ve Kapat hello *User.java* dosya.

### <a name="define-a-data-repository-interface"></a>Bir veri deposu arabirimi tanımlayın

1. Adlı yeni bir dosya oluşturun *UserRepository.java* hello içindeki ana uygulama Java dosyası ile aynı dizinde.

1. Açık hello *UserRepository.java* dosyasını bir metin düzenleyicisinde ve hello aşağıdaki hello varsayılan DocumentDB depo arabirimi genişleten bir kullanıcı deposu arabirimi toohello dosya toodefine satırları ekleyin:

   ```java
   package com.example.wingtiptoys;

   import com.microsoft.azure.spring.data.documentdb.repository.DocumentDbRepository;
   import org.springframework.stereotype.Repository;

   @Repository
   public interface UserRepository extends DocumentDbRepository<User, String> {}   
   ```

1. Kaydet ve Kapat hello *UserRepository.java* dosya.

### <a name="modify-hello-main-application-class"></a>Merhaba ana uygulama sınıfını değiştirme

1. Merhaba ana uygulama Java dosyası, uygulamanızın paket dizinine hello bulun; Örneğin:

   `C:\SpringBoot\wingtiptoys\src\main\java\com\example\wingtiptoys\WingtiptoysApplication.java`

   -veya-

   `/users/example/home/wingtiptoys/src/main/java/com/example/wingtiptoys/WingtiptoysApplication.java`

   ![Merhaba uygulama Java dosyasını bulun][JV01]

1. Merhaba ana uygulama Java dosyası bir metin düzenleyicisinde açın ve aşağıdaki satırları toohello dosyasına hello ekleyin:

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

1. Merhaba ana uygulama Java dosyasını kaydedip kapatın.

## <a name="build-and-test-your-app"></a>Derleme ve uygulamanızı test etme

1. Bir komut istemi açın ve dizin toohello klasörü Değiştir Burada, *pom.xml* dosyasının bulunduğu; örneğin:

   `cd C:\SpringBoot\wingtiptoys`

   -veya-

   `cd /users/example/home/wingtiptoys`

1. Yay önyükleme uygulamanızı Maven ile ve çalıştırın; Örneğin:

   ```shell
   mvn package
   java -jar target/wingtiptoys-0.0.1-SNAPSHOT.jar
   ```

1. Uygulamanız birden fazla çalışma zamanı iletileri görüntülenir ve selamlama iletisine görmelisiniz. `User: testFirstName testLastName` değerleri başarıyla depolanan ve, veritabanından alınan olduğunu tooindicate görüntülenir.

   ![Merhaba uygulaması başarılı çıktısı][JV02]

1. İsteğe bağlı: Hello Azure portal tooview hello hello özellikleri sayfasında, Azure Cosmos DB'den içeriğini veritabanınız için tıklayarak kullanabileceğiniz **belge Gezgini**ve ardından seçerek ve de görüntülenen hello listesi tooview hello öğesinden içeriği.

   ![Verilerinizi Hello belge Gezgini tooview kullanma][JV03]

## <a name="next-steps"></a>Sonraki adımlar

Azure Cosmos DB ve Java kullanma hakkında daha fazla bilgi için aşağıdaki makaleler hello bakın:

* [Azure Cosmos DB belgelerine].

* [Azure Cosmos DB: Java ile DocumentDB API uygulaması oluşturma ve Azure portal hello][Build a DocumentDB API app with Java]

Azure üzerinde yay önyükleme uygulamalarında kullanma hakkında daha fazla bilgi için aşağıdaki makaleler hello bakın:

* [Azure için yay önyükleme DocumenDB Başlatıcı](https://github.com/Microsoft/azure-spring-boot-starters/tree/master/azure-documentdb-spring-boot-starter-sample)

* [Yay önyükleme uygulama toohello Azure App Service'e dağıtma](../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)

* [Yay önyükleme uygulama hello Azure kapsayıcı hizmeti Kubernetes kümede çalışan](../container-service/container-service-deploy-spring-boot-app-on-kubernetes.md)

Azure Java ile kullanma hakkında daha fazla bilgi için bkz: Merhaba [Azure Java Geliştirici Merkezi] ve hello [Visual Studio Team Services için Java Araçları].

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
