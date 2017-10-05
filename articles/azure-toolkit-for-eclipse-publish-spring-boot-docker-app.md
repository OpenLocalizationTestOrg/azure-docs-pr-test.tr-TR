---
title: "Eclipse için Azure araç setini kullanarak bir Docker kapsayıcısı yay önyükleme uygulama yayımlama | Microsoft Docs"
description: "Eclipse için Azure araç setini kullanarak bir web uygulaması için Microsoft Azure Docker kapsayıcısı yayımlamak öğrenin."
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
ms.openlocfilehash: fcb60fcfbda26f5f37bfb0edcb01f8737188b6bc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="publish-a-spring-boot-app-as-a-docker-container-by-using-the-azure-toolkit-for-eclipse"></a>Eclipse için Azure araç setini kullanarak bir Docker kapsayıcısı yay önyükleme uygulama yayımlama

[Yay Framework] Java geliştiriciler kuruluş düzeyinde uygulamalar oluşturmanıza yardımcı olan bir açık kaynaklı bir çözümdür. Yerleşik daha popüler projelerden biri üzerinde üst o platformudur [yay önyükleme], tek başına Java uygulamaları oluşturmak için basitleştirilmiş bir yaklaşım sağlar.

[Docker] geliştiricilere yardımcı olan bir açık kaynak çözümü dağıtımını, ölçeklendirme ve kapsayıcılarında çalışan kendi uygulamalarını yönetimini otomatikleştirmek olduğu.

Bu öğreticide, Eclipse için Azure Araç Seti kullanarak Microsoft Azure için Docker kapsayıcısı olarak yay önyükleme uygulama dağıtma adımları açıklanmaktadır.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="clone-the-default-spring-boot-docker-repository"></a>Varsayılan yay önyükleme Docker depoyu kopyalayın

### <a name="import-the-public-repository"></a>Genel depo alma

Aşağıdaki adımlar, yerel bilgisayarınızın yay önyükleme Docker depoya Intellij kullanarak kopyalama aracılığıyla yol. Bir komut satırı kullanmak istiyorsanız, bkz: [Linux Azure kapsayıcı Hizmeti'nde bir yay önyükleme uygulamasını dağıtmak][Deploy Spring Boot on Linux in ACS].

1. Eclipse açın.

1. Tıklatın **dosya** > **alma**.

   ![Dosya alma menüsü][CL01]

1. Zaman **alma** iletişim kutusunu açar:

   a. Genişletme **Git**.

   b. Seçin **Git projeleri**.
   
   c. **İleri**’ye tıklayın.

   ![İçeri aktarma iletişim kutusu][CL02]

1. Üzerinde **depo kaynağı seçin** sayfa:

   a. Seçin **kopyalama URI**.
   
   b. **İleri**’ye tıklayın.

   ![Depo Kaynağı Seç sayfası][CL03]

1. Üzerinde **kaynak Git deposu** sayfa:

   a. İçin **URI**, girin `https://github.com/spring-guides/gs-spring-boot-docker.git`. Bu adımı otomatik olarak doldurur **konak** ve **deposu yolu** alanları doğru değerlere sahip.
   
   b. Yay önyükleme depo ortak olduğundan Git kullanıcı adı ve parola girmeniz gerekmez.
   
   c. **İleri**’ye tıklayın.

   ![Kaynak Git deposu sayfası][CL04]

1. Üzerinde **dal seçimi** sayfasında, **sonraki**.

   ![Dal seçimi sayfası][CL05]

1. Üzerinde **yerel hedef** sayfa:

   a. Yerel klasör, Yerel Depodaki istediğiniz yeri belirtin.
   
   b. **İleri**’ye tıklayın.

   ![Yerel hedef sayfası][CL06]

1. Üzerinde **projeleri içeri aktarmada kullanmak için sihirbaz seçin** sayfa:

   a. Seçin **genel bir proje olarak içe aktar**.
   
   b. **İleri**’ye tıklayın.

   !["Projeleri içeri aktarmada kullanmak için bir sihirbaz Seç" sayfasını][CL07]

1. Üzerinde **projeleri içeri aktar** sayfa:

   a. Proje adı belirtin.
   
   b. **Son**'a tıklayın.

   ![Projeleri sayfasını içeri aktarma][CL08]

1. Depo başarıyla kopyalanması için Eclipse'te listelenen tüm dosyaları görürsünüz.

   ![Yerel deposu][CL09]

### <a name="create-a-maven-project-from-your-local-repository"></a>Yerel depodan bir Maven projesi oluşturun

Yay önyükleme Docker deposu, Bu öğretici için kullanacağınız tamamlanmış bir Maven projesi içerir. 

1. Tıklatın **dosya** > **alma**.

   ![Dosya menüsünde Import komutu][CL01]

1. Zaman **alma** iletişim kutusunu açar:

   a. Genişletme **Maven**.
   
   b. Seçin **varolan Maven projelerini**.
   
   c. **İleri**’ye tıklayın.

   ![İçeri aktarma iletişim kutusu][MV01]

1. Üzerinde **Maven projelerini** sayfa:

   a. İçin **kök dizini**, belirtin **tam** yerel deponuza klasöründe.
   
   b. Genişletme **Gelişmiş** bölümünde ve özel bir adı **adı şablonu**.
   
   c. Kutusunu seçin **pom.xml** proje dosyasında.
   
   d. **Son**'a tıklayın.

   ![Maven Projeler sayfası][MV02]

1. Bir Maven projesi başarıyla açıldığında, Eclipse'te listelenen ikinci bir proje bakın.

   ![Yerel bir Maven projesi][MV03]

## <a name="build-your-spring-boot-app-by-using-maven"></a>Maven kullanarak yay önyükleme uygulamanızı oluşturun

1. Eclipse proje Gezgini'nde bir Maven projesi seçin.

1. Tıklatın **çalıştırmak** > **Çalıştır** > **Maven derleme**.

   ![Maven çalıştırılacak komutları derleme][BU01]

1. Uygulamanız başarılı bir şekilde yapılandırıldığında, konsol penceresi durumunu gösterir.

   ![Başarılı Maven derleme][BU02]

## <a name="publish-your-web-app-to-azure-by-using-a-docker-container"></a>Docker kapsayıcısı kullanarak Azure için web uygulamanızı yayınlama

1. Eclipse proje Gezgini'nde bir Maven projesi seçin.

1. Azure'ı tıklatın **Yayımla** menüsüne ve ardından **Docker kapsayıcısı olarak Yayımla**.

   ![Docker kapsayıcısı komut olarak Yayımla][PU01]

1. Zaman **dağıtma Docker kapsayıcısı Azure üzerinde** iletişim kutusu görüntülenir:

   a. Özel bir Docker görüntü adı girin.
   
   b. İçin **dağıtmak için yapı**, yolunu belirtin **gs-yay-önyükleme-docker-0.1.0.jar** dosyası yalnızca oluşturuldu.

   ![Docker seçeneklerini belirtin][PU02]

   Herhangi bir varolan Docker ana bilgisayar görüntülenir. 

1. Varolan bir ana bilgisayara dağıtmak isterseniz, 5. adıma atlayabilirsiniz. Aksi halde, bir ana bilgisayar oluşturmak için aşağıdaki adımları kullanın:

   a. **Ekle**'ye tıklayın.

      ![Yeni bir Docker ana bilgisayar Ekle][PU03]

   b. Zaman **oluşturma Docker ana** iletişim kutusu görüntülenirse, varsayılan değerleri kabul etmeyi tercih edebilirsiniz veya yeni Docker ana bilgisayarınız için özel ayarlar belirtebilirsiniz. (Çeşitli ayarları ayrıntılı açıklamaları için bkz: [Intellij için Azure araç setini kullanarak bir web uygulaması Docker kapsayıcısı yayımlama][Publish Container with Azure Toolkit].) Tıklatın **sonraki** zaman belirttiğiniz kullanmak için hangi ayarları.

      ![Docker ana bilgisayar seçeneklerini belirtin][PU04]

   c. Azure anahtar Kasası'ndan varolan oturum açma kimlik bilgilerini kullanmayı seçebilirsiniz veya yeni Docker oturum açma kimlik bilgilerini girmeyi seçebilirsiniz. Tıklatın **son** zaman belirttiğiniz seçeneklerinizi.

      ![Docker ana bilgisayar kimlik bilgilerini belirtin][PU05]

1. Docker ana bilgisayarınız seçin ve ardından **sonraki**.

   ![Kullanmak için Docker ana bilgisayar seçin][PU06]

1. Sihirbazın son sayfasında **dağıtma Docker kapsayıcısı Azure üzerinde** iletişim kutusunda, aşağıdaki seçenekleri belirtin:

   a. Varsayılan ayarı kabul edebilirsiniz veya özel bir Docker kapsayıcısı barındıracak kapsayıcının adını belirtmek seçebilirsiniz.

   b. TCP bağlantı noktaları docker ana bilgisayarınız için aşağıdaki sözdizimini kullanarak girin: *[dış bağlantı noktası]*:*[iç bağlantı noktası]*. Örneğin, **80:8080** bir dış bağlantı noktası 80 ve varsayılan iç yay önyükleme bağlantı noktası 8080 belirtir.
   
      İç bağlantı noktası (örneğin, application.yml dosyasını düzenleyerek) özelleştirdiyseniz, doğru Azure üzerinde gerçekleşmesi için yönlendirme için bağlantı noktası numarasını belirtmeniz gerekir.

   c. Bu seçenekleri yapılandırdıktan sonra tıklatın **son**.

   ![Azure üzerinde bir Docker kapsayıcısı dağıtma][PU07]

1. Azure Araç Seti yayımlama tamamlandığında, Azure etkinlik günlüğü görüntüler **yayımlanan** durum.

   ![Docker ana başarıyla dağıtıldı][PU08]

## <a name="next-steps"></a>Sonraki adımlar

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<!-- URL List -->

[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Deploy Spring Boot on Linux in ACS]:container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux.md
[Docker]: https://www.docker.com/
[Publish Container with Azure Toolkit]: ./azure-toolkit-for-intellij-publish-as-docker-container.md
[yay önyükleme]: http://projects.spring.io/spring-boot/
[Yay Framework]: https://spring.io/

<!-- IMG List -->

[CL01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL01.png
[CL02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL02.png
[CL03]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL03.png
[CL04]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL04.png
[CL05]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL05.png
[CL06]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL06.png
[CL07]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL07.png
[CL08]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL08.png
[CL09]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL09.png

[MV01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV01.png
[MV02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV02.png
[MV03]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV03.png

[BU01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/BU01.png
[BU02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/BU02.png

[PU01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU01.png
[PU02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU02.png
[PU03]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU03.png
[PU04]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU04.png
[PU05]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU05.png
[PU06]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU06.png
[PU07]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU07.png
[PU08]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU08.png
