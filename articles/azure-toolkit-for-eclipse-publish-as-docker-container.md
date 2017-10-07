---
title: "aaaPublish kullanarak bir Docker kapsayıcısı hello Eclipse için Azure Araç Seti | Microsoft Docs"
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
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 53ec3a7f7a171691024e03622fd48d6f1e257b50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-hello-azure-toolkit-for-eclipse"></a>Eclipse için hello Azure Araç Seti kullanarak bir web uygulaması Docker kapsayıcısı Yayımla

Docker, web uygulamalarını dağıtmak için yaygın olarak kullanılan bir yöntem kapsayıcılardır. Docker kapsayıcıları kullanarak, geliştiricilerin kendi tüm proje dosyalarını ve dağıtım tooa sunucusu için tek bir paket bağımlılıkları birleştirebilir. Merhaba Eclipse için Azure Araç Seti basitleştirir bu işlem için Java geliştiricilerinin ekleyerek *Docker kapsayıcısı olarak Yayımla* dağıtım tooMicrosoft Azure özellikleri. Bu makalede hello adımları gerekli toopublish Docker kapsayıcılar olarak uygulamaları tooAzure anlatılmaktadır.

> [!NOTE]
> Docker hakkında daha fazla bilgi hello üzerinde kullanılabilir [Docker Web sitesi].
>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a>Web uygulaması tooAzure Docker kapsayıcısı kullanarak yayımlama

1. Web uygulaması projenizin Eclipse'te açın.

2. toostart hello **Docker kapsayıcısı olarak Yayımla** Sihirbazı'nı hello aşağıdakilerden birini yapın:

   * Merhaba, **Gezgini** görüntülemek, projenize sağ tıklayın, **Azure**ve ardından **Docker kapsayıcısı olarak Yayımla**.

      ![Gezgin Görünümü Docker kapsayıcısı komut olarak Yayımla][PUB01]

   * Merhaba Hello Eclipse araç çubuğunda tıklatın **Yayımla** düğmesine tıklayın ve ardından **Docker kapsayıcısı olarak Yayımla**.

      ![Eclipse araç Docker kapsayıcısı komut olarak Yayımla][PUB02]
      
    Merhaba **azure'da dağıtmak Docker kapsayıcısı** Sihirbazı açılır.

    ![Merhaba dağıtma Docker kapsayıcısı Azure Sihirbazı][PUB03]

3. Merhaba, **bir görüntü adı yazın, hello yapı'nın yolu seçin ve kullanılan Docker ana toobe denetleyin** penceresinde, aşağıdaki hello:

    a. Merhaba, **Docker görüntü adı** kutusuna, Docker ana bilgisayar için benzersiz bir ad girin. (Merhaba Sihirbazı otomatik olarak bir ad oluşturur, ancak bunu değiştirebilirsiniz.)

    b. Merhaba **ana** alanı önceden oluşturmuş olduğunuz tüm Docker ana bilgisayarlarını görüntüler. Merhaba aşağıdakilerden birini yapın:

    * Varolan bir Docker ana bilgisayara varsa, web uygulaması tooit dağıtabilirsiniz.
    * Yeni bir Docker ana bilgisayar toocreate tıklatın **Ekle**.  
      
    Merhaba **oluşturma Docker ana** iletişim kutusu açılır.

    ![Docker kapsayıcısı üzerinde Azure Sihirbazı'nı dağıtma][PUB04a]

4. Merhaba, **hello yeni sanal makine yapılandırma** penceresinde, aşağıdaki seçenekleri, Docker ana bilgisayar için şu hello belirtin. (Merhaba seçenekler çoğunu hello Sihirbazı otomatik olarak oluşturur, ancak herhangi birini değiştirebilirsiniz.)

   a. **Ad**: Merhaba Docker ana bilgisayar için benzersiz bir ad girin. (Bu, hello almak için değil, daha önce belirtilen Docker görüntü adı hello aynı olur.)

   b. **Abonelik**: hello ana bilgisayarınız için kullandığınız Azure aboneliğini girin.

   c. **Bölge**: ana bilgisayarınız bulunduğu hello coğrafi girin.

   d. Merhaba üzerinde **ana bilgisayar işletim sistemi ve boyutu** sekmesi:
     * **Ana bilgisayar işletim sistemi**: hello işletim sistemi hello sanal makine için ana bilgisayarınız içeren girin.
     * **Boyutu**: ana bilgisayarınız için hello sanal makine boyutu girin.

   e. Merhaba üzerinde **kaynak grubu** sekmesi:
     * **Yeni kaynak grubu**: ana bilgisayarınız için yeni bir kaynak grubu oluşturun.
     * **Varolan bir kaynak grubu**: Azure hesabınızdan varolan bir kaynak grubu girin.

   f. Merhaba üzerinde **ağ** sekmesi:
     * **Yeni sanal ağ**: ana bilgisayarınız için yeni bir sanal ağ oluşturun.
     * **Varolan bir sanal ağı**: varolan bir sanal ağı Azure hesabınızı girin.

   g. Merhaba üzerinde **depolama** sekmesi:
     * **Yeni depolama hesabı**: ana bilgisayarınız için yeni bir depolama hesabı oluşturun.
     * **Varolan bir depolama hesabı**: Azure hesabınızdan mevcut bir depolama hesabını girin.

5. **İleri**’ye tıklayın.

6. Merhaba, **günlük kimlik bilgilerini yapılandırın ve bağlantı noktası ayarları** penceresinde, aşağıdaki seçenekleri şu hello birini seçin:

    * **Azure anahtar Kasası'kimlik bilgileri içe**: önceden kaydedilen bir Azure aboneliğinizde depolanan kimlik bilgileri kümesi belirtir.

      >[!NOTE]
      >Bir hesabın veya hizmet sorumlusu ile oluşturulan bir Azure anahtar kasası başka bir hesap veya hello abonelik paylaşan hizmet sorumlusu tarafından otomatik olarak erişilebilir değil. tooallow başka bir hesap veya hizmet asıl toouse anahtar kasası Merhaba, hello Azure portal tooadd hello hesabı ya da hizmet sorumlusu kullanmanız gerekir.

    * **Yeni oturum açma kimlik bilgileri**: yeni bir oturum açma kimlik bilgileri kümesi oluşturur. Bu seçeneği seçerseniz, aşağıdaki hello:
    
      * Merhaba üzerinde **VM kimlik** sekmesinde, hello sanal makinesi oturum açma kimlik bilgileri, Docker ana bilgisayarın seçenekleri hello aşağıdakilerden birini seçin:

          * **Kullanıcı adı**: hello kullanıcı için sanal makine oturum açma kimlik bilgilerinizi girin.
          * **Parola** ve **Onayla**: hello parola için sanal makine oturum açma kimlik bilgilerinizi girin.
          * **SSH**: Docker ana bilgisayarınız hello güvenli Kabuk (SSH) ayarlarını girin. Seçenekler aşağıdaki hello seçebilirsiniz:
            * **Hiçbiri**: sanal makineniz SSH bağlantılara izin vermez belirtir.
            * **Otomatik oluşturma**: hello SSH yoluyla bağlanmak için gerekli ayarları otomatik olarak oluşturur.
            * **Dizine alma**: önceden kaydedilmiş SSH ayarları kümesini içeren bir dizini belirtir. Merhaba dizin, aşağıdaki iki dosyaları hello içermelidir:
                * *id_rsa*: bir kullanıcı için hello RSA kimliğini içerir.
                * *id_rsa.pub*: kimlik doğrulaması için kullanılan hello RSA ortak anahtarı içerir.
        
        ![Docker konak oluştur][PUB05]

      * Merhaba üzerinde **Docker arka plan programı kimlik** sekmesinde, aşağıdaki seçenekleri şu hello belirtin:

          * **Docker arka plan programı bağlantı noktası**: Docker ana bilgisayarınız için hello benzersiz TCP bağlantı noktası girin.
          * **TLS güvenlik**: Docker ana bilgisayarınız hello Aktarım Katmanı Güvenliği ayarlarını girin. Seçenekler aşağıdaki hello seçebilirsiniz:
            * **Hiçbiri**: sanal makineniz TLS bağlantılara izin vermez belirtir.
            * **Otomatik oluşturma**: hello TLS bağlanmak için gerekli ayarları otomatik olarak oluşturur.
            * **Dizine alma**: önceden kaydedilmiş TLS ayarları kümesini içeren bir dizini belirtir. Daha açık belirtmek gerekirse hello dizini aşağıdaki altı dosyaları hello içermelidir:
                * *CA.pem* ve *ca key.pem*: hello sertifika ve ortak anahtar hello TLS sertifika yetkilisi için içerir.
                * *CERT.pem* ve *key.pem*: hello istemci sertifikası ve TLS kimlik doğrulaması için kullanılan ortak anahtar içerir.
                * *Server.pem* ve *server key.pem*: hello sunucu sertifikası ve hello ana bilgisayarı için ortak anahtar içerir.

        ![Docker konak oluştur][PUB06]

7. Tüm önceki bilgilere hello girdikten sonra tıklatın **son**.

8. Merhaba, **dağıtmak Docker kapsayıcısı Azure üzerinde** Sihirbazı'nı tıklatın **sonraki**.

   ![Merhaba dağıtma Docker kapsayıcısı Azure Sihirbazı][PUB07]

9. Merhaba, **oluşturulan hello Docker kapsayıcısı toobe yapılandırma** penceresinde, aşağıdaki hello:

   a. Merhaba, **Docker kapsayıcısı adı** kutusuna, Docker kapsayıcısı için benzersiz bir ad girin.

   b. Docker görüntüleri aşağıdaki hello birini seçin:
     * **Önceden tanımlanmış Docker görüntü**: Azure önceden var olan bir Docker görüntüsünden belirtir.

       >[!NOTE]
       >Bu kutu Docker görüntülerinde Hello listesi, birkaç görüntülerini oluşur Azure Araç Seti açıldı, hello toopatch yapılandırılmış, yapı otomatik olarak dağıtılır.

     * **Özel Dockerfile**: yerel bilgisayarınızdan önceden kaydedilmiş bir Dockerfile belirtir.

       >[!NOTE]
       >Bu, kendi Dockerfile toodeploy isteyen geliştiriciler için daha gelişmiş bir özelliktir. Ancak, kendi Dockerfile doğru bir şekilde yapıldığından bu seçeneği tooensure kullanan toodevelopers değildir. Merhaba Dockerfile sorunları varsa hello dağıtım başarısız olabilir şekilde hello Azure Araç Seti özel bir Dockerfile hello içeriği doğrulamaz. Ayrıca, hello Azure Araç Seti hello özel Dockerfile toocontain bir web uygulaması yapı bekler ve tooopen bir HTTP bağlantısı deneyecek. Geliştiriciler farklı türde bir yapı yayımlarsanız, bunlar dağıtım sonrası zararsız hatalar alabilirsiniz.

   c. **Bağlantı noktası ayarları**: hello benzersiz TCP bağlantı noktası için bağlama, Docker kapsayıcısı girin.

     ![Merhaba yapılandırma hello Docker kapsayıcısı oluşturulan toobe penceresi][PUB08]

10. Tüm adımları önceki hello tamamladıktan sonra tıklatın **son**.

Hello Azure araç seti, web uygulama tooAzure Docker kapsayıcısı içinde dağıtmaya başlar. 

## <a name="next-steps"></a>Sonraki adımlar
Java IDE hello Azure araç takımları hakkında daha fazla bilgi için kaynakları aşağıdaki hello bakın:

* [Eclipse için Azure Araç Seti]
  * [Merhaba Eclipse için Azure Araç Seti yenilikleri]
  * [Yükleme hello Eclipse için Azure Araç Seti]
  * [Oturum açma hello Eclipse için Azure Araç Seti için yönergeler]
  * [Eclipse'te Azure Hello World web uygulaması oluşturma]
* [IntelliJ için Azure Araç Seti]
  * [Merhaba Intellij için Azure Araç Seti yenilikleri]
  * [Yükleme hello Intellij için Azure Araç Seti]
  * [Oturum açma hello Azure Araç Seti için Intellij için yönergeler]
  * [Intellij Azure'da Hello World web uygulaması oluşturun]

Azure Java ile kullanma hakkında daha fazla bilgi için bkz: [Azure Java Geliştirici Merkezi] ve [Visual Studio Team Services için Java Araçları].

Merhaba resmi Docker için ek kaynaklar için bkz: [Docker Web sitesi].

<!-- URL List -->

[Eclipse için Azure Araç Seti]: ./azure-toolkit-for-eclipse.md
[IntelliJ için Azure Araç Seti]: ./azure-toolkit-for-intellij.md
[Eclipse'te Azure Hello World web uygulaması oluşturma]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Intellij Azure'da Hello World web uygulaması oluşturun]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Yükleme hello Eclipse için Azure Araç Seti]: ./azure-toolkit-for-eclipse-installation.md
[Yükleme hello Intellij için Azure Araç Seti]: ./azure-toolkit-for-intellij-installation.md
[Oturum açma hello Eclipse için Azure Araç Seti için yönergeler]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Oturum açma hello Azure Araç Seti için Intellij için yönergeler]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Merhaba Eclipse için Azure Araç Seti yenilikleri]: ./azure-toolkit-for-eclipse-whats-new.md
[Merhaba Intellij için Azure Araç Seti yenilikleri]: ./azure-toolkit-for-intellij-whats-new.md

[Azure Java Geliştirici Merkezi]: https://azure.microsoft.com/develop/java/
[Visual Studio Team Services için Java Araçları]: https://java.visualstudio.com/

[Docker Web sitesi]: https://www.docker.com/

<!-- IMG List -->

[PUB01]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB01.png
[PUB02]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB02.png
[PUB03]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB03.png
[PUB04a]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04a.png
[PUB04b]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04b.png
[PUB04c]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04c.png
[PUB04d]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04d.png
[PUB05]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB05.png
[PUB06]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB06.png
[PUB07]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB07.png
[PUB08]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB08.png