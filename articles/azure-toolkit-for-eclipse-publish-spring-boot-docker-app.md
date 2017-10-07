---
title: "aaaPublish yay önyükleme uygulama kullanarak bir Docker kapsayıcısı olarak hello Eclipse için Azure Araç Seti | Microsoft Docs"
description: "Bilgi nasıl toopublish bir web uygulaması tooMicrosoft kullanarak bir Docker kapsayıcısı olarak Azure hello Eclipse için Azure Araç Seti."
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
ms.openlocfilehash: 29390c49c339a1ebb87cb3951b21cea01c0da15f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-spring-boot-app-as-a-docker-container-by-using-hello-azure-toolkit-for-eclipse"></a>Eclipse için hello Azure Araç Seti kullanarak Docker kapsayıcısı yay önyükleme uygulama yayımlama

Merhaba [yay Framework] Java geliştiriciler kuruluş düzeyinde uygulamalar oluşturmanıza yardımcı olan bir açık kaynaklı bir çözümdür. Yerleşik hello daha popüler projelerden biri üzerinde üst o platformudur [yay önyükleme], tek başına Java uygulamaları oluşturmak için basitleştirilmiş bir yaklaşım sağlar.

[Docker] geliştiricilere yardımcı olan bir açık kaynak çözümü hello dağıtımını, ölçeklendirme ve kapsayıcılarında çalışan kendi uygulamalarını yönetimini otomatikleştirmek olduğu.

Bu öğreticide Eclipse için hello Azure Araç Seti kullanarak bir yay önyükleme uygulama Docker kapsayıcısı tooMicrosoft Azure olarak hello adımları toodeploy açıklanmaktadır.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="clone-hello-default-spring-boot-docker-repository"></a>Merhaba varsayılan yay önyükleme Docker depoyu kopyalayın

### <a name="import-hello-public-repository"></a>İçeri aktarma hello genel depo

Merhaba aşağıdaki adımlar Intellij kullanarak hello yay önyükleme Docker depo tooyour yerel bilgisayar kopyalama aracılığıyla yol. Bir komut satırı toouse istiyorsanız, bkz: [Linux Azure kapsayıcı Hizmeti'nde bir yay önyükleme uygulamasını dağıtmak][Deploy Spring Boot on Linux in ACS].

1. Eclipse açın.

1. Tıklatın **dosya** > **alma**.

   ![Dosya alma menüsü][CL01]

1. Ne zaman hello **alma** iletişim kutusunu açar:

   a. Genişletme **Git**.

   b. Seçin **Git projeleri**.
   
   c. **İleri**’ye tıklayın.

   ![İçeri aktarma iletişim kutusu][CL02]

1. Merhaba üzerinde **depo kaynağı seçin** sayfa:

   a. Seçin **kopyalama URI**.
   
   b. **İleri**’ye tıklayın.

   ![Depo Kaynağı Seç sayfası][CL03]

1. Merhaba üzerinde **kaynak Git deposu** sayfa:

   a. İçin **URI**, girin `https://github.com/spring-guides/gs-spring-boot-docker.git`. Bu adım hello otomatik olarak doldurur **konak** ve **deposu yolu** hello alanlarla değerleri düzeltin.
   
   b. Merhaba yay önyükleme deposu ortak olduğundan Git kullanıcı adı ve parola tooenter olmamalıdır.
   
   c. **İleri**’ye tıklayın.

   ![Kaynak Git deposu sayfası][CL04]

1. Merhaba üzerinde **dal seçimi** sayfasında, **sonraki**.

   ![Dal seçimi sayfası][CL05]

1. Merhaba üzerinde **yerel hedef** sayfa:

   a. Merhaba yerel klasör, Yerel Depodaki istediğiniz yeri belirtin.
   
   b. **İleri**’ye tıklayın.

   ![Yerel hedef sayfası][CL06]

1. Merhaba üzerinde **projeleri İçeri Aktarma Sihirbazı'nı toouse seçin** sayfa:

   a. Seçin **genel bir proje olarak içe aktar**.
   
   b. **İleri**’ye tıklayın.

   !["Projeleri İçeri Aktarma Sihirbazı'nı toouse Seç" sayfasını][CL07]

1. Merhaba üzerinde **projeleri içeri aktar** sayfa:

   a. Proje adı belirtin.
   
   b. **Son**'a tıklayın.

   ![Projeleri sayfasını içeri aktarma][CL08]

1. Merhaba deposu başarıyla kopyalandı, Eclipse'te listelenen tüm hello dosyalarına bakın.

   ![Yerel deposu][CL09]

### <a name="create-a-maven-project-from-your-local-repository"></a>Yerel depodan bir Maven projesi oluşturun

Bu öğretici için kullanacağınız tamamlanmış bir Maven projesi Hello yay önyükleme Docker depo içerir. 

1. Tıklatın **dosya** > **alma**.

   ![Merhaba Dosya menüsünde komutunu alma][CL01]

1. Ne zaman hello **alma** iletişim kutusunu açar:

   a. Genişletme **Maven**.
   
   b. Seçin **varolan Maven projelerini**.
   
   c. **İleri**’ye tıklayın.

   ![İçeri aktarma iletişim kutusu][MV01]

1. Merhaba üzerinde **Maven projelerini** sayfa:

   a. İçin **kök dizini**, hello belirtin **tam** yerel deponuza klasöründe.
   
   b. Merhaba genişletin **Gelişmiş** bölümünde ve özel bir adı **adı şablonu**.
   
   c. Merhaba SELECT hello kutusunu **pom.xml** hello proje dosyasında.
   
   d. **Son**'a tıklayın.

   ![Maven Projeler sayfası][MV02]

1. Merhaba Maven projesine başarıyla açıldığında, Eclipse'te listelenen ikinci bir proje bakın.

   ![Yerel bir Maven projesi][MV03]

## <a name="build-your-spring-boot-app-by-using-maven"></a>Maven kullanarak yay önyükleme uygulamanızı oluşturun

1. Hello Eclipse Proje Gezgini, hello Maven projesini seçin.

1. Tıklatın **çalıştırmak** > **Çalıştır** > **Maven derleme**.

   ![Maven derleme olarak komutları toorun][BU01]

1. Uygulamanız başarılı bir şekilde yapılandırıldığında, hello konsol penceresinde hello durumunu gösterir.

   ![Başarılı Maven derleme][BU02]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a>Web uygulaması tooAzure Docker kapsayıcısı kullanarak yayımlama

1. Hello Eclipse Proje Gezgini, hello Maven projesini seçin.

1. Hello Azure'ı tıklatın **Yayımla** menüsüne ve ardından **Docker kapsayıcısı olarak Yayımla**.

   ![Docker kapsayıcısı komut olarak Yayımla][PU01]

1. Ne zaman hello **dağıtma Docker kapsayıcısı Azure üzerinde** iletişim kutusu görüntülenir:

   a. Özel bir Docker görüntü adı girin.
   
   b. İçin **yapı toodeploy**, hello yolu toohello belirtin **gs-yay-önyükleme-docker-0.1.0.jar** dosyası yalnızca oluşturuldu.

   ![Docker seçeneklerini belirtin][PU02]

   Herhangi bir varolan Docker ana bilgisayar görüntülenir. 

1. Toodeploy tooan var olan konak seçerseniz, toostep 5 atlayabilirsiniz. Aksi takdirde, aşağıdaki adımları toocreate bir ana bilgisayar hello kullanın:

   a. **Ekle**'ye tıklayın.

      ![Yeni bir Docker ana bilgisayar Ekle][PU03]

   b. Ne zaman hello **oluşturma Docker ana** iletişim kutusu görüntülenirse, tooaccept hello Varsayılanları seçin veya yeni Docker ana bilgisayarınız için özel ayarlar belirtebilirsiniz. (Merhaba ayrıntılı açıklamaları için bkz: çeşitli ayarlar, [Intellij için hello Azure Araç Seti kullanarak bir web uygulaması Docker kapsayıcısı yayımlama][Publish Container with Azure Toolkit].) Tıklatın **sonraki** zaman belirttiğiniz hangi ayarları toouse.

      ![Docker ana bilgisayar seçeneklerini belirtin][PU04]

   c. Azure anahtar Kasası'nı toouse varolan oturum açma kimlik bilgilerini seçin veya yeni Docker oturum açma kimlik bilgileri tooenter seçebilirsiniz. Tıklatın **son** zaman belirttiğiniz seçeneklerinizi.

      ![Docker ana bilgisayar kimlik bilgilerini belirtin][PU05]

1. Docker ana bilgisayarınız seçin ve ardından **sonraki**.

   ![Docker ana toouse seçin][PU06]

1. Merhaba hello son sayfasında **dağıtma Docker kapsayıcısı Azure üzerinde** iletişim kutusunda, aşağıdaki seçenekleri şu hello belirtin:

   a. Merhaba varsayılan kabul edebilir veya toospecify, Docker kapsayıcısı barındıracak hello kapsayıcı için bir özel ad seçebilirsiniz.

   b. Merhaba TCP bağlantı noktaları docker ana bilgisayarınız için sözdizimi aşağıdaki hello kullanarak girin: *[dış bağlantı noktası]*:*[iç bağlantı noktası]*. Örneğin, **80:8080** bir dış bağlantı noktası 80 ve hello varsayılan iç yay önyükleme bağlantı noktası 8080 belirtir.
   
      İç bağlantı noktası (örneğin, hello application.yml dosyasını düzenleyerek) özelleştirdiyseniz, azure'da hello doğru yönlendirme toooccur için toospecify hello bağlantı noktası numarası gerekir.

   c. Bu seçenekleri yapılandırdıktan sonra tıklatın **son**.

   ![Azure üzerinde bir Docker kapsayıcısı dağıtma][PU07]

1. Yayımlama Hello Azure Araç Seti sona erdiğinde hello Azure etkinlik günlüğü görüntüler **yayımlanan** hello durumu.

   ![Docker ana başarıyla dağıtıldı][PU08]

## <a name="next-steps"></a>Sonraki adımlar

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<!-- URL List -->

[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Deploy Spring Boot on Linux in ACS]:container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux.md
[Docker]: https://www.docker.com/
[Publish Container with Azure Toolkit]: ./azure-toolkit-for-intellij-publish-as-docker-container.md
[yay önyükleme]: http://projects.spring.io/spring-boot/
[yay Framework]: https://spring.io/

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
