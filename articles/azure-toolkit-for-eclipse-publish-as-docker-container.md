---
title: "Eclipse için Azure araç setini kullanarak bir Docker kapsayıcısı yayımlama | Microsoft Docs"
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
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 746bb0a073396b84fa8592adda6748a2a5692ee8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-the-azure-toolkit-for-eclipse"></a>Eclipse için Azure araç setini kullanarak bir web uygulaması Docker kapsayıcısı Yayımla

Docker, web uygulamalarını dağıtmak için yaygın olarak kullanılan bir yöntem kapsayıcılardır. Docker kapsayıcıları kullanarak, geliştiricilerin kendi tüm proje dosyalarını ve tek bir paket için bir sunucu dağıtımı için bağımlılıkları birleştirebilir. Eclipse için Azure araç seti, ekleyerek Java geliştiriciler için bu işlemi basitleştirir *Docker kapsayıcısı olarak Yayımla* Microsoft Azure dağıtım özellikleri. Bu makalede, Azure, uygulamalarınızı Docker kapsayıcı olarak yayımlamak için gereken adımları açıklanmaktadır.

> [!NOTE]
> Docker hakkında daha fazla bilgi edinilebilir [Docker Web sitesi].
>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="publish-your-web-app-to-azure-by-using-a-docker-container"></a>Docker kapsayıcısı kullanarak Azure için web uygulamanızı yayınlama

1. Web uygulaması projenizin Eclipse'te açın.

2. Başlatmak için **Docker kapsayıcısı olarak Yayımla** Sihirbazı, aşağıdakilerden birini yapın:

   * İçinde **Gezgini** görüntülemek, projenize sağ tıklayın, **Azure**ve ardından **Docker kapsayıcısı olarak Yayımla**.

      ![Gezgin Görünümü Docker kapsayıcısı komut olarak Yayımla][PUB01]

   * Eclipse araç çubuğunda tıklatın **Yayımla** düğmesine tıklayın ve ardından **Docker kapsayıcısı olarak Yayımla**.

      ![Eclipse araç Docker kapsayıcısı komut olarak Yayımla][PUB02]
      
    **Azure'da dağıtmak Docker kapsayıcısı** Sihirbazı açılır.

    ![Azure Sihirbazı dağıtmak Docker kapsayıcısı][PUB03]

3. İçinde **bir görüntü adı yazın, yapı'nın yolu seçin ve kullanılacak bir Docker ana denetleyin** penceresinde aşağıdakileri yapın:

    a. İçinde **Docker görüntü adı** kutusuna, Docker ana bilgisayar için benzersiz bir ad girin. (Sihirbaz otomatik olarak bir ad oluşturur, ancak bunu değiştirebilirsiniz.)

    b. **Ana** alanı önceden oluşturmuş olduğunuz tüm Docker ana bilgisayarlarını görüntüler. Aşağıdakilerden birini yapın:

    * Varolan bir Docker ana bilgisayara varsa, web uygulamanızı dağıtabilirsiniz.
    * Yeni bir Docker ana bilgisayar oluşturmak için tıklatın **Ekle**.  
      
    **Oluşturma Docker ana** iletişim kutusu açılır.

    ![Docker kapsayıcısı üzerinde Azure Sihirbazı'nı dağıtma][PUB04a]

4. İçinde **yeni sanal makine yapılandırma** penceresinde, Docker ana bilgisayarınız için aşağıdaki seçenekleri belirtin. (Sihirbaz için seçenekler çoğunu otomatik olarak oluşturur, ancak herhangi birini değiştirebilirsiniz.)

   a. **Ad**: Docker ana bilgisayar için benzersiz bir ad girin. (Bu, daha önce belirttiğiniz Docker görüntü adı ile aynı değildir.)

   b. **Abonelik**: ana bilgisayarınız için kullandığınız Azure aboneliğini girin.

   c. **Bölge**: ana bilgisayarınız bulunduğu coğrafi bölge girin.

   d. Üzerinde **ana bilgisayar işletim sistemi ve boyutu** sekmesi:
     * **Ana bilgisayar işletim sistemi**: ana bilgisayarınız içeren sanal makine için işletim sistemi girin.
     * **Boyutu**: ana bilgisayarınız için sanal makine boyutu girin.

   e. Üzerinde **kaynak grubu** sekmesi:
     * **Yeni kaynak grubu**: ana bilgisayarınız için yeni bir kaynak grubu oluşturun.
     * **Varolan bir kaynak grubu**: Azure hesabınızdan varolan bir kaynak grubu girin.

   f. Üzerinde **ağ** sekmesi:
     * **Yeni sanal ağ**: ana bilgisayarınız için yeni bir sanal ağ oluşturun.
     * **Varolan bir sanal ağı**: varolan bir sanal ağı Azure hesabınızı girin.

   g. Üzerinde **depolama** sekmesi:
     * **Yeni depolama hesabı**: ana bilgisayarınız için yeni bir depolama hesabı oluşturun.
     * **Varolan bir depolama hesabı**: Azure hesabınızdan mevcut bir depolama hesabını girin.

5. **İleri**’ye tıklayın.

6. İçinde **günlük kimlik bilgilerini yapılandırın ve bağlantı noktası ayarları** penceresinde, aşağıdaki seçeneklerden birini belirleyin:

    * **Azure anahtar Kasası'kimlik bilgileri içe**: önceden kaydedilen bir Azure aboneliğinizde depolanan kimlik bilgileri kümesi belirtir.

      >[!NOTE]
      >Bir hesabın veya hizmet sorumlusu ile oluşturulan bir Azure anahtar kasası başka bir hesap veya abonelik paylaşan hizmet sorumlusu tarafından otomatik olarak erişilebilir değil. Başka bir hesap veya hizmet asıl anahtar kasası kullanmaya izin vermek için hesabı veya hizmet sorumlusu eklemek için Azure Portalı'nı kullanmanız gerekir.

    * **Yeni oturum açma kimlik bilgileri**: yeni bir oturum açma kimlik bilgileri kümesi oluşturur. Bu seçeneği seçerseniz, aşağıdakileri yapın:
    
      * Üzerinde **VM kimlik** sekmesinde, aşağıdaki seçenekler, Docker ana bilgisayar sanal makinesi oturum açma kimlik bilgilerini seçin:

          * **Kullanıcı adı**: kullanıcı için sanal makine oturum açma kimlik bilgilerinizi girin.
          * **Parola** ve **Onayla**: parola için sanal makine oturum açma kimlik bilgilerinizi girin.
          * **SSH**: Docker ana bilgisayarınız Güvenli Kabuk (SSH) ayarlarını girin. Aşağıdaki seçenekler arasından seçim yapabilirsiniz:
            * **Hiçbiri**: sanal makineniz SSH bağlantılara izin vermez belirtir.
            * **Otomatik oluşturma**: SSH yoluyla bağlanmak için gerekli ayarları otomatik olarak oluşturur.
            * **Dizine alma**: önceden kaydedilmiş SSH ayarları kümesini içeren bir dizini belirtir. Dizin, aşağıdaki iki dosyada içermelidir:
                * *id_rsa*: bir kullanıcı için RSA kimliğini içerir.
                * *id_rsa.pub*: kimlik doğrulaması için kullanılan RSA ortak anahtarı içerir.
        
        ![Docker konak oluştur][PUB05]

      * Üzerinde **Docker arka plan programı kimlik** sekmesinde, aşağıdaki seçenekleri belirtin:

          * **Docker arka plan programı bağlantı noktası**: Docker ana bilgisayarınız için benzersiz TCP bağlantı noktasını girin.
          * **TLS güvenlik**: Docker ana bilgisayarınız için Aktarım Katmanı Güvenliği ayarlarını girin. Aşağıdaki seçenekler arasından seçim yapabilirsiniz:
            * **Hiçbiri**: sanal makineniz TLS bağlantılara izin vermez belirtir.
            * **Otomatik oluşturma**: TLS bağlanmak için gerekli ayarları otomatik olarak oluşturur.
            * **Dizine alma**: önceden kaydedilmiş TLS ayarları kümesini içeren bir dizini belirtir. Daha açık belirtmek gerekirse dizin aşağıdaki altı dosyaları içermelidir:
                * *CA.pem* ve *ca key.pem*: TLS sertifika yetkilisi sertifika ve ortak anahtarı içerir.
                * *CERT.pem* ve *key.pem*: istemci sertifikası ve TLS kimlik doğrulaması için kullanılan ortak anahtar içerir.
                * *Server.pem* ve *server key.pem*: ana bilgisayar için sunucu sertifikası ve ortak anahtar içerir.

        ![Docker konak oluştur][PUB06]

7. Yukarıdaki bilgilerin tümünü girdikten sonra tıklatın **son**.

8. İçinde **dağıtmak Docker kapsayıcısı Azure üzerinde** Sihirbazı'nı tıklatın **sonraki**.

   ![Azure Sihirbazı dağıtmak Docker kapsayıcısı][PUB07]

9. İçinde **oluşturulacak Docker kapsayıcısı yapılandırma** penceresinde aşağıdakileri yapın:

   a. İçinde **Docker kapsayıcısı adı** kutusuna, Docker kapsayıcısı için benzersiz bir ad girin.

   b. Aşağıdaki Docker görüntülerden birini seçin:
     * **Önceden tanımlanmış Docker görüntü**: Azure önceden var olan bir Docker görüntüsünden belirtir.

       >[!NOTE]
       >Bu kutu Docker görüntülerinde listesi, Azure Araç Seti için yapılandırılmış birden fazla görüntülerinin oluşur, yapı otomatik olarak dağıtılır böylece düzeltme eki.

     * **Özel Dockerfile**: yerel bilgisayarınızdan önceden kaydedilmiş bir Dockerfile belirtir.

       >[!NOTE]
       >Bu, kendi Dockerfile dağıtmak isteyen geliştiriciler için daha gelişmiş bir özelliktir. Ancak, kendi Dockerfile doğru bir şekilde yapıldığından emin olmak için bu seçeneği kullanın geliştiriciler kadar olur. Dockerfile sorunları varsa dağıtım başarısız olabilir şekilde Azure Araç Seti özel bir Dockerfile içeriği doğrulamaz. Ayrıca, bir web uygulaması yapı içerecek şekilde özel Dockerfile Azure Araç Seti bekliyor ve bir HTTP bağlantısı açmayı dener. Geliştiriciler farklı türde bir yapı yayımlarsanız, bunlar dağıtım sonrası zararsız hatalar alabilirsiniz.

   c. **Bağlantı noktası ayarları**: Docker kapsayıcısı için benzersiz TCP bağlantı noktası bağlama girin.

     ![Pencere oluşturulması için Docker kapsayıcısı Yapılandır][PUB08]

10. Önceki tüm adımları tamamladıktan sonra tıklatın **son**.

Azure Araç Seti Azure Docker kapsayıcısı içinde web uygulamanızı dağıtmaya başlar. 

## <a name="next-steps"></a>Sonraki adımlar
Java IDE Azure araç takımları hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

* [Eclipse için Azure Araç Seti]
  * [Eclipse için Azure Araç Seti yenilikleri]
  * [Eclipse için Azure Araç Setini Yükleme]
  * [Eclipse için Azure Araç Seti için oturum açma yönergeleri]
  * [Eclipse'te Azure Hello World web uygulaması oluşturma]
* [IntelliJ için Azure Araç Seti]
  * [Intellij için Azure Araç Seti yenilikleri]
  * [IntelliJ için Azure Araç Setini Yükleme]
  * [Oturum açma Azure Araç Seti için Intellij için yönergeler]
  * [Intellij Azure'da Hello World web uygulaması oluşturun]

Azure Java ile kullanma hakkında daha fazla bilgi için bkz: [Azure Java Geliştirici Merkezi] ve [Visual Studio Team Services için Java Araçları].

Resmi Docker için ek kaynaklar için bkz: [Docker Web sitesi].

<!-- URL List -->

[Eclipse için Azure Araç Seti]: ./azure-toolkit-for-eclipse.md
[IntelliJ için Azure Araç Seti]: ./azure-toolkit-for-intellij.md
[Eclipse'te Azure Hello World web uygulaması oluşturma]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Intellij Azure'da Hello World web uygulaması oluşturun]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Eclipse için Azure Araç Setini Yükleme]: ./azure-toolkit-for-eclipse-installation.md
[IntelliJ için Azure Araç Setini Yükleme]: ./azure-toolkit-for-intellij-installation.md
[Eclipse için Azure Araç Seti için oturum açma yönergeleri]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Oturum açma Azure Araç Seti için Intellij için yönergeler]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Eclipse için Azure Araç Seti yenilikleri]: ./azure-toolkit-for-eclipse-whats-new.md
[Intellij için Azure Araç Seti yenilikleri]: ./azure-toolkit-for-intellij-whats-new.md

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