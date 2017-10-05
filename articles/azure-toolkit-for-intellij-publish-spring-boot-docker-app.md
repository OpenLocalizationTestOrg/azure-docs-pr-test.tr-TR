---
title: "Intellij için Azure araç setini kullanarak bir Docker kapsayıcısı yay önyükleme uygulama yayımlama | Microsoft Docs"
description: "Docker kapsayıcısı Microsoft Azure Intellij için Azure araç setini kullanarak bir web uygulaması yayımlama öğrenin."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 06/21/2017
ms.author: robmcm
ms.openlocfilehash: b771238934183c953615ac33c42a275d80657556
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="publish-a-spring-boot-app-as-a-docker-container-by-using-the-azure-toolkit-for-intellij"></a>Intellij için Azure araç setini kullanarak bir Docker kapsayıcısı yay önyükleme uygulama yayımlama

[Yay Framework] Java geliştiriciler kuruluş düzeyinde uygulamalar oluşturmanıza yardımcı olan bir açık kaynaklı bir çözümdür. Yerleşik daha popüler projelerden biri üzerinde üst o platformudur [yay önyükleme], tek başına Java uygulamaları oluşturmak için basitleştirilmiş bir yaklaşım sağlar.

[Docker] geliştiricilere yardımcı olan bir açık kaynak çözümü dağıtımını, ölçeklendirme ve kapsayıcılarında çalışan kendi uygulamalarını yönetimini otomatikleştirmek olduğu.

Bu öğreticide, bir yay önyükleme uygulama Docker kapsayıcısı olarak Intellij için Azure Araç Seti kullanarak Microsoft Azure'a dağıtma adımları açıklanmaktadır.

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="clone-the-default-spring-boot-docker-repo"></a>Varsayılan yay önyükleme Docker depoyu kopyalama

Aşağıdaki adımlar Intellij kullanarak yay önyükleme Docker depoyu kopyalama aracılığıyla yol. Bir komut satırı kullanmak istiyorsanız, bkz: [Linux Azure kapsayıcı Hizmeti'nde bir yay önyükleme uygulamasını dağıtmak][Deploy Spring Boot on Linux in ACS].

1. Intellij açın.

1. Hoş Geldiniz ekranında seçin **GitHub** seçeneğini **sürüm denetiminden kullanıma** listesi.

   ![Sürüm denetimi için GitHub seçeneği][CL01]

1. Oturum açmak için istenirse kimlik bilgilerinizi girin.

   * GitHub için oturum açmak için bir kullanıcı adı/parola kullanıyorsanız:

      ![GitHub kullanıcı adı ve parola girme iletişim kutusu][CL02a]

   * GitHub için oturum açmak için bir belirteç kullanıyorsanız:

      ![Bir GitHub belirteci girmek için iletişim kutusu][CL02b]

1. Girin **https://github.com/spring-guides/gs-spring-boot-docker.git** deposu URL'sini yerel yolu ve klasör bilgileri belirtin ve ardından **kopya**.

   ![Kopya Deposu iletişim kutusu][CL03]

1. Intellij projesi oluşturmak için istendiğinde seçin **Hayır**.

   ![Intellij projesi oluşturmak reddetme][CL04]

1. Hoş Geldiniz sayfasında, tıklatın **projeyi içeri aktarma**.

   ![Proje Seçimi alma][CL05]

1. Yay önyükleme depoyu kopyaladığınız yolu bulun, seçin **tam** kök ve ardından altında bir klasör **Tamam**.

   ![İçeri aktarma için bir klasör seçin][CL06]

1. İstendiğinde, seçin **mevcut kaynaklardan proje oluştur**.

   ![Mevcut kaynaklardan bir proje oluşturmak için seçeneği][CL07]

1. Proje adı belirtin veya varsayılanı kabul etmek, doğru yolunu doğrulayın **tam** klasörünü ve ardından **sonraki**.

   ![Proje adı belirtin][CL08]

1. Alma için herhangi bir dizin özelleştirmek ve ardından **sonraki**.

   ![Dizinleri seçin][CL09]

1. Kitaplıkları içeri aktarın ve ardından gözden **sonraki**.

   ![Proje kitaplıkları gözden geçirin][CL10]

1. Modül yapısı gözden geçirin ve ardından **sonraki**.

   ![Modül yapısı gözden geçirin][CL11]

1. JDK belirtin ve ardından **sonraki**.

   ![Bir JDK belirtin][CL12]

1. **Son**'a tıklayın.

   ![Son düğmesine][CL13]

Intellij yay önyükleme uygulamayı bir proje olarak içe aktarır ve alma işlemini tamamladığında yapısını görüntüler.

![Yay önyükleme Intellij uygulamada][CL14]

## <a name="build-your-spring-boot-app"></a>Yay önyükleme derleme uygulama

### <a name="build-the-app-by-using-the-maven-pom"></a>Maven POM kullanarak uygulaması oluşturma

1. Zaten açık değilse Maven aracı penceresini açın. Tıklatın **Görünüm** > **aracı Windows** > **Maven projelerini**.

   ![Araç pencereleri ve Maven projelerini komutları][BU01]

1. Maven araç penceresinde sağ **paket** seçip **çalıştırmak Maven derleme**. (Maven projenize otomatik olarak gösterilmez, tıklatın **yeniden içeri aktarın** Maven araç çubuğundaki simgeye.)

   ![Maven derleme komutunu çalıştırın][BU02]

1. Intellij görüntülemesi gereken bir **Yapı Başarısı** iletisi yay önyükleme uygulamanız başarıyla oluşturuldu.

   ![Yapı Başarı iletisi][BU03]

### <a name="create-a-deployment-ready-artifact"></a>Bir dağıtım için hazır yapı oluşturma

Yay önyükleme uygulamanızı yayımlamak için bir dağıtım için hazır yapı oluşturmanız gerekir. Aşağıdaki adımları kullanın:

1. Web uygulaması projenizin Intellij içinde açın.

1. Tıklatın **dosya**ve ardından **proje yapısını**.

   ![Proje yapısı komutu][ART01]

1. Yeşil artı (**+**) bir yapı eklemek için Sembol **JAR**ve ardından **boş**.

   ![Bir yapı ekleyin][ART02]

1. ".Jar" uzantısı eklememek emin olmasını sağlarken, yapı adlandırın ve ardından Maven çıktısı için hedef klasör belirtin.

   ![Yapı özelliklerini belirtin][ART03]

1. Bir bildirimi, yapı (isteğe bağlı) oluşturun:

   a. Tıklatın **bildirimi oluşturma**.

      ![Oluşturma bildirim düğmesini tıklatın][ART04a]

   b. Yapı için varsayılan yolu seçin ve ardından **Tamam**.

      ![Yapı yolu belirtin][ART04b]

   c. Üç nokta işaretine (**...** ) ana sınıf bulunamadı.

      ![Ana sınıf bulunamadı][ART04c]

   d. Ana sınıfınız seçin ve ardından **Tamam**.

      ![Ana sınıf belirtin][ART04d]

1. **Tamam** düğmesine tıklayın.

   ![Proje Yapısı iletişim kutusunu kapatın][ART05]

> [!NOTE]
> Intellij yapıları oluşturma hakkında daha fazla bilgi için bkz: [yapılandırma yapıları] JetBrains Web sitesinde.
>

### <a name="build-the-artifact-for-deployment"></a>Dağıtım için yapı derleme

1. Tıklatın **yapı**ve ardından **yapıları**.

   ![Yapıları komutu derleme][BU04]

1. Zaman **yapı yapı** bağlam menüsü görüntülendikten sonra **yapı**.

   ![Yapı bağlam menüsü oluşturma][BU05]

Intellij yay önyükleme uygulamanız için tamamlanan yapı proje araç penceresinde görüntülemelidir.

   ![Oluşturulan yapı][BU06]

## <a name="publish-your-web-app-to-azure-by-using-a-docker-container"></a>Docker kapsayıcısı kullanarak Azure için web uygulamanızı yayınlama

1. Azure hesabınızda oturum açmanızdan değil, adımları [oturum açma ilişkin yönergeler için Azure Araç Seti Intellij][Azure Sign In for IntelliJ].

1. Proje Gezgini araç penceresi projeye sağ tıklayın ve ardından **Azure** > **Docker kapsayıcısı olarak Yayımla**.

   ![Docker kapsayıcısı komut olarak Yayımla][PU01]

1. Zaman **azure'da dağıtmak Docker kapsayıcısı** iletişim kutusu görüntülenirse, varolan herhangi Docker konağına görüntülenir. Varolan bir ana bilgisayara dağıtmak isterseniz, 4. adıma atlayabilirsiniz. Aksi halde, bir ana bilgisayar oluşturmak için aşağıdaki adımları kullanın:

   a. Yeşil artı (**+**) simgesi.

      ![Yeni bir Docker ana bilgisayar Ekle][PU02]

   b. Zaman **oluşturma Docker ana** iletişim kutusu görüntülenirse, varsayılan değerleri kabul etmeyi tercih edebilirsiniz veya yeni Docker ana bilgisayarınız için özel ayarlar belirtebilirsiniz. (Çeşitli ayarları ayrıntılı açıklamaları için bkz: [Intellij için Azure araç setini kullanarak bir web uygulaması Docker kapsayıcısı yayımlama][Publish Container with Azure Toolkit].) Tıklatın **sonraki** zaman belirttiğiniz kullanmak için hangi ayarları.

      ![Docker ana bilgisayar seçeneklerini belirtin][PU03a]

   c. Azure anahtar Kasası'ndan varolan oturum açma kimlik bilgilerini kullanmayı seçebilirsiniz veya yeni Docker oturum açma kimlik bilgilerini girmeyi seçebilirsiniz. Tıklatın **son** zaman belirttiğiniz seçeneklerinizi.

      ![Docker ana bilgisayar kimlik bilgilerini belirtin][PU03b]

1. Docker ana bilgisayarınız seçin ve ardından **sonraki**.

   ![Kullanmak için Docker konağı seçin][PU04]

1. Sihirbazın son sayfasında **azure'da dağıtmak Docker kapsayıcısı** iletişim kutusunda, aşağıdaki seçenekleri belirtin:

   a. Varsayılan ayarı kabul edebilirsiniz veya özel bir Docker kapsayıcısı barındıracak kapsayıcının adını belirtmek seçebilirsiniz.

   b. TCP bağlantı noktaları docker ana bilgisayarınız için aşağıdaki sözdizimini kullanarak girin: *[dış bağlantı noktası]*:*[iç bağlantı noktası]*. Örneğin, **80:8080** bir dış bağlantı noktası 80 ve varsayılan iç yay önyükleme bağlantı noktası 8080 belirtir.
   
      İç bağlantı noktası (örneğin, application.yml dosyasını düzenleyerek) özelleştirdiyseniz, doğru Azure üzerinde gerçekleşmesi için yönlendirme için bağlantı noktası numarasını belirtmeniz gerekir.

   c. Bu seçenekleri yapılandırdıktan sonra tıklayın **son**.

   ![Azure üzerinde bir Docker kapsayıcısı dağıtma][PU05]

1. Azure Araç Seti yayımlama tamamlandığında, Azure etkinlik günlüğü görüntüler **yayımlanan** durum.

   ![Docker ana başarıyla dağıtıldı][PU06]

## <a name="next-steps"></a>Sonraki adımlar

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

Intellij kullanarak yay önyükleme uygulamaları oluşturmak için ek yöntemleri hakkında bilgi edinmek için [yay önyükleme projeleri oluşturma](https://www.jetbrains.com/help/idea/creating-spring-boot-projects.html) JetBrains Web sitesinde.

<!-- URL List -->

[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Sign In for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[yapılandırma yapıları]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html
[Deploy Spring Boot on Linux in ACS]:container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux.md
[Docker]: https://www.docker.com/
[Publish Container with Azure Toolkit]: ./azure-toolkit-for-intellij-publish-as-docker-container.md
[yay önyükleme]: http://projects.spring.io/spring-boot/
[Yay Framework]: https://spring.io/

<!-- IMG List -->

[CL01]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL01.png
[CL02a]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL02a.png
[CL02b]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL02b.png
[CL03]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL03.png
[CL04]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL04.png
[CL05]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL05.png
[CL06]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL06.png
[CL07]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL07.png
[CL08]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL08.png
[CL09]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL09.png
[CL10]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL10.png
[CL11]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL11.png
[CL12]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL12.png
[CL13]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL13.png
[CL14]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL14.png

[ART01]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART01.png
[ART02]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART02.png
[ART03]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART03.png
[ART04a]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04a.png
[ART04b]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04b.png
[ART04c]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04c.png
[ART04d]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04d.png
[ART05]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART05.png

[BU01]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU01.png
[BU02]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU02.png
[BU03]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU03.png
[BU04]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU04.png
[BU05]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU05.png
[BU06]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU06.png

[PU01]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU01.png
[PU02]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU02.png
[PU03a]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU03a.png
[PU03b]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU03b.png
[PU04]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU04.png
[PU05]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU05.png
[PU06]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU06.png
