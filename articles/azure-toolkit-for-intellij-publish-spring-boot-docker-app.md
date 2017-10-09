---
title: "aaaPublish yay önyükleme uygulama kullanarak bir Docker kapsayıcısı olarak hello Azure Araç Seti için Intellij | Microsoft Docs"
description: "Bilgi nasıl toopublish bir web uygulaması tooMicrosoft kullanarak bir Docker kapsayıcısı olarak Azure hello Azure Araç Seti Intellij için."
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
ms.openlocfilehash: 8964cb33fd8f61a39f091633ae9074d9658232fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-spring-boot-app-as-a-docker-container-by-using-hello-azure-toolkit-for-intellij"></a>Intellij için hello Azure Araç Seti kullanarak Docker kapsayıcısı yay önyükleme uygulama yayımlama

Merhaba [yay Framework] Java geliştiriciler kuruluş düzeyinde uygulamalar oluşturmanıza yardımcı olan bir açık kaynaklı bir çözümdür. Yerleşik hello daha popüler projelerden biri üzerinde üst o platformudur [yay önyükleme], tek başına Java uygulamaları oluşturmak için basitleştirilmiş bir yaklaşım sağlar.

[Docker] geliştiricilere yardımcı olan bir açık kaynak çözümü hello dağıtımını, ölçeklendirme ve kapsayıcılarında çalışan kendi uygulamalarını yönetimini otomatikleştirmek olduğu.

Bu öğreticide Intellij için hello Azure Araç Seti kullanarak bir yay önyükleme uygulama Docker kapsayıcısı tooMicrosoft Azure olarak hello adımları toodeploy açıklanmaktadır.

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="clone-hello-default-spring-boot-docker-repo"></a>Merhaba varsayılan yay önyükleme Docker depoyu kopyalama

Merhaba aşağıdaki adımlar Intellij kullanarak hello yay önyükleme Docker depoyu kopyalama aracılığıyla yol. Bir komut satırı toouse istiyorsanız, bkz: [Linux Azure kapsayıcı Hizmeti'nde bir yay önyükleme uygulamasını dağıtmak][Deploy Spring Boot on Linux in ACS].

1. Intellij açın.

1. Merhaba Hoş Geldiniz ekranında hello seçin **GitHub** hello seçeneğinde **sürüm denetiminden kullanıma** listesi.

   ![Sürüm denetimi için GitHub seçeneği][CL01]

1. İstendiğinde toolog içinde olması durumunda kimlik bilgilerinizi girin.

   * Bir kullanıcı adı/parola toolog tooGitHub içinde kullanıyorsanız:

      ![GitHub kullanıcı adı ve parola girme iletişim kutusu][CL02a]

   * İçinde tooGitHub belirteci toolog kullanıyorsanız:

      ![Bir GitHub belirteci girmek için iletişim kutusu][CL02b]

1. Girin **https://github.com/spring-guides/gs-spring-boot-docker.git** hello depo URL'si için yerel yolu ve klasör bilgileri belirtin ve ardından **kopya**.

   ![Kopya Deposu iletişim kutusu][CL03]

1. Sorulduğunda toocreate Intellij projesinde, select **Hayır**.

   ![Toocreate Intellij projesinde reddetme][CL04]

1. Merhaba Hoş Geldiniz sayfasında, tıklatın **projeyi içeri aktarma**.

   ![Proje Seçimi alma][CL05]

1. Merhaba yay önyükleme depodaki kopyaladığınız hello yolu bulun, seçin hello **tam** hello kök ve ardından altında bir klasör **Tamam**.

   ![İçeri aktarma için bir klasör seçin][CL06]

1. İstendiğinde, seçin **mevcut kaynaklardan proje oluştur**.

   ![Seçenek toocreate mevcut kaynaklardan bir proje][CL07]

1. Proje adı belirtin veya hello varsayılanı kabul etmek, hello doğru yolu toohello doğrulayın **tam** klasörünü ve ardından **sonraki**.

   ![Merhaba proje adı belirtin][CL08]

1. Alma için herhangi bir dizin özelleştirmek ve ardından **sonraki**.

   ![Dizinleri seçin][CL09]

1. Merhaba kitaplıkları tooimport gözden geçirin ve ardından **sonraki**.

   ![Proje kitaplıkları gözden geçirin][CL10]

1. Merhaba modül yapısı gözden geçirin ve ardından **sonraki**.

   ![Modül yapısı gözden geçirin][CL11]

1. JDK belirtin ve ardından **sonraki**.

   ![Bir JDK belirtin][CL12]

1. **Son**'a tıklayın.

   ![Son düğmesine][CL13]

Intellij hello yay önyükleme uygulama projesi alır ve hello alma sona erdiğinde hello yapısını görüntüler.

![Yay önyükleme Intellij uygulamada][CL14]

## <a name="build-your-spring-boot-app"></a>Yay önyükleme derleme uygulama

### <a name="build-hello-app-by-using-hello-maven-pom"></a>Merhaba Maven POM kullanarak Hello uygulaması oluşturma

1. Zaten açık değilse hello Maven araç penceresi açın. Tıklatın **Görünüm** > **aracı Windows** > **Maven projelerini**.

   ![Araç pencereleri ve Maven projelerini komutları][BU01]

1. Merhaba Maven araç penceresinde sağ **paket** seçip **çalıştırmak Maven derleme**. (Maven projenize otomatik olarak gösterilmez, hello tıklatın **yeniden içeri aktarın** hello Maven araç çubuğundaki simgesini.)

   ![Maven derleme komutunu çalıştırın][BU02]

1. Intellij görüntülemesi gereken bir **Yapı Başarısı** iletisi yay önyükleme uygulamanız başarıyla oluşturuldu.

   ![Yapı Başarı iletisi][BU03]

### <a name="create-a-deployment-ready-artifact"></a>Bir dağıtım için hazır yapı oluşturma

toopublish yay önyükleme uygulamanızı toocreate bir dağıtım için hazır yapı gerekir. Merhaba aşağıdaki adımları kullanın:

1. Web uygulaması projenizin Intellij içinde açın.

1. Tıklatın **dosya**ve ardından **proje yapısını**.

   ![Proje yapısı komutu][ART01]

1. Merhaba artı yeşil tıklayın (**+**) sembol tooadd bir yapı, tıklatın **JAR**ve ardından **boş**.

   ![Bir yapı ekleyin][ART02]

1. Değil tooadd ".jar" uzantısı hello ve Maven çıktı hello hello hedef klasör belirtin emin olmasını sağlarken, yapı adı.

   ![Yapı özelliklerini belirtin][ART03]

1. Bir bildirimi, yapı (isteğe bağlı) oluşturun:

   a. Tıklatın **bildirimi oluşturma**.

      ![Merhaba oluşturmak bildirim düğmesini tıklatın][ART04a]

   b. Merhaba yapı için Hello varsayılan yolu seçin ve ardından **Tamam**.

      ![Yapı yolu belirtin][ART04b]

   c. Merhaba üç nokta düğmesine (**...** ) toolocate hello ana sınıfı.

      ![Ana sınıf bulunamadı][ART04c]

   d. Ana sınıfınız seçin ve ardından **Tamam**.

      ![Ana sınıf belirtin][ART04d]

1. **Tamam** düğmesine tıklayın.

   ![Merhaba proje yapısını iletişim kutusunu kapatın][ART05]

> [!NOTE]
> Intellij yapıları oluşturma hakkında daha fazla bilgi için bkz: [yapılandırma yapıları] hello JetBrains Web sitesinde.
>

### <a name="build-hello-artifact-for-deployment"></a>Merhaba yapı dağıtımı için derleme

1. Tıklatın **yapı**ve ardından **yapıları**.

   ![Yapıları komutu derleme][BU04]

1. Ne zaman hello **yapı yapı** bağlam menüsü görüntülendikten sonra **yapı**.

   ![Yapı bağlam menüsü oluşturma][BU05]

Intellij yay önyükleme uygulamanız için tamamlanan hello yapı hello proje araç penceresinde görüntülemelidir.

   ![Oluşturulan yapı][BU06]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a>Web uygulaması tooAzure Docker kapsayıcısı kullanarak yayımlama

1. Tooyour Azure hesabı imzalanmamış, hello adımları [oturum açma ilişkin yönergeler için hello Azure Araç Seti Intellij][Azure Sign In for IntelliJ].

1. Merhaba Proje Gezgini aracı penceresinde hello projesine sağ tıklayın ve ardından **Azure** > **Docker kapsayıcısı olarak Yayımla**.

   ![Docker kapsayıcısı komut olarak Yayımla][PU01]

1. Ne zaman hello **azure'da dağıtmak Docker kapsayıcısı** iletişim kutusu görüntülenirse, varolan herhangi Docker konağına görüntülenir. Toodeploy tooan var olan konak seçerseniz, toostep 4 atlayabilirsiniz. Aksi takdirde, aşağıdaki adımları toocreate bir ana bilgisayar hello kullanın:

   a. Merhaba artı yeşil tıklayın (**+**) simgesi.

      ![Yeni bir Docker ana bilgisayar Ekle][PU02]

   b. Ne zaman hello **oluşturma Docker ana** iletişim kutusu görüntülenirse, tooaccept hello Varsayılanları seçin veya yeni Docker ana bilgisayarınız için özel ayarlar belirtebilirsiniz. (Merhaba ayrıntılı açıklamaları için bkz: çeşitli ayarlar, [Intellij için hello Azure Araç Seti kullanarak bir web uygulaması Docker kapsayıcısı yayımlama][Publish Container with Azure Toolkit].) Tıklatın **sonraki** zaman belirttiğiniz hangi ayarları toouse.

      ![Docker ana bilgisayar seçeneklerini belirtin][PU03a]

   c. Azure anahtar Kasası'nı toouse varolan oturum açma kimlik bilgilerini seçin veya yeni Docker oturum açma kimlik bilgileri tooenter seçebilirsiniz. Tıklatın **son** zaman belirttiğiniz seçeneklerinizi.

      ![Docker ana bilgisayar kimlik bilgilerini belirtin][PU03b]

1. Docker ana bilgisayarınız seçin ve ardından **sonraki**.

   ![Merhaba Docker ana toouse seçin][PU04]

1. Merhaba hello son sayfasında **azure'da dağıtmak Docker kapsayıcısı** iletişim kutusunda, aşağıdaki seçenekleri şu hello belirtin:

   a. Merhaba varsayılan kabul edebilir veya toospecify, Docker kapsayıcısı barındıracak hello kapsayıcı için bir özel ad seçebilirsiniz.

   b. Merhaba TCP bağlantı noktaları docker ana bilgisayarınız için sözdizimi aşağıdaki hello kullanarak girin: *[dış bağlantı noktası]*:*[iç bağlantı noktası]*. Örneğin, **80:8080** bir dış bağlantı noktası 80 ve hello varsayılan iç yay önyükleme bağlantı noktası 8080 belirtir.
   
      İç bağlantı noktası (örneğin, hello application.yml dosyasını düzenleyerek) özelleştirdiyseniz, azure'da hello doğru yönlendirme toooccur için toospecify hello bağlantı noktası numarası gerekir.

   c. Bu seçenekleri yapılandırdıktan sonra tıklayın **son**.

   ![Azure üzerinde bir Docker kapsayıcısı dağıtma][PU05]

1. Yayımlama Hello Azure Araç Seti sona erdiğinde hello Azure etkinlik günlüğü görüntüler **yayımlanan** hello durumu.

   ![Docker ana başarıyla dağıtıldı][PU06]

## <a name="next-steps"></a>Sonraki adımlar

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

toolearn Intellij, kullanarak yay önyükleme uygulamaları oluşturmak için ek yöntemleri hakkında bkz [yay önyükleme projeleri oluşturma](https://www.jetbrains.com/help/idea/creating-spring-boot-projects.html) hello JetBrains Web sitesinde.

<!-- URL List -->

[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Sign In for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[yapılandırma yapıları]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html
[Deploy Spring Boot on Linux in ACS]:container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux.md
[Docker]: https://www.docker.com/
[Publish Container with Azure Toolkit]: ./azure-toolkit-for-intellij-publish-as-docker-container.md
[yay önyükleme]: http://projects.spring.io/spring-boot/
[yay Framework]: https://spring.io/

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
