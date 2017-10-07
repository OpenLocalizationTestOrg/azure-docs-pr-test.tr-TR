---
title: "aaaPublish kullanarak bir Docker kapsayıcısı hello Azure Araç Seti için Intellij | Microsoft Docs"
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
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: bee94cb269ea707ae7ad55232e23e915aec48c34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-hello-azure-toolkit-for-intellij"></a>Intellij için hello Azure Araç Seti kullanarak bir web uygulaması Docker kapsayıcısı Yayımla

Docker, web uygulamalarını dağıtmak için yaygın olarak kullanılan bir yöntem kapsayıcılardır. Docker kapsayıcıları kullanarak, geliştiricilerin kendi tüm proje dosyalarını ve dağıtım tooa sunucusu için tek bir paket bağımlılıkları birleştirebilir. Merhaba Intellij için Azure Araç Seti basitleştirir bu işlem için Java geliştiricilerinin ekleyerek *Docker kapsayıcısı olarak Yayımla* dağıtım tooMicrosoft Azure özellikleri. Bu makalede hello adımları gerekli toopublish Docker kapsayıcılar olarak uygulamaları tooAzure anlatılmaktadır.

> [!NOTE]
>
> Docker hakkında daha fazla bilgi hello üzerinde kullanılabilir [Docker Web sitesi].
>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a>Web uygulaması tooAzure Docker kapsayıcısı kullanarak yayımlama

> [!NOTE]
> * toopublish web uygulamanızı bir dağıtım için hazır yapı oluşturmanız gerekir. toolearn daha, hello fazla [yapıları oluşturma hakkında ek bilgi](#artifacts) bölümü.
>
> * En az bir kez hello Dağıtım Sihirbazı'nı tamamladıktan sonra ayarlarınızı çoğunu hello Sihirbazı'nı yeniden çalıştırdığınızda varsayılan olarak kullanılır.
>

1. Web uygulaması projenizin Intellij içinde açın.

2. toostart hello **Docker kapsayıcısı olarak Yayımla** Sihirbazı'nı hello aşağıdakilerden birini yapın:

   * Merhaba, **proje** araç penceresi, projenize sağ tıklayın, **Azure**ve ardından **Docker kapsayıcısı olarak Yayımla**:

      ![Merhaba Docker kapsayıcısı komut olarak Yayımla][PUB01]

   * Merhaba Intellij araç çubuğunda hello tıklatın **Yayımla grup** düğmesine tıklayın ve ardından **Docker kapsayıcısı olarak Yayımla**:

      ![Merhaba Docker kapsayıcısı komut olarak Yayımla][PUB02]  
    Merhaba **azure'da dağıtmak Docker kapsayıcısı** Sihirbazı açılır.

   ![Merhaba dağıtma Docker kapsayıcısı Azure Sihirbazı][PUB03]

3. Merhaba, **bir görüntü adı yazın, hello yapı'nın yolu seçin ve kullanılan Docker ana toobe denetleyin** penceresinde, aşağıdaki hello: 

   a. Merhaba, **Docker görüntü adı** kutusuna, Docker ana bilgisayar için benzersiz bir ad girin. (Merhaba Sihirbazı otomatik olarak bir ad oluşturur, ancak bunu değiştirebilirsiniz.) 

   b. Merhaba **ana** alanı önceden oluşturmuş olduğunuz tüm Docker ana bilgisayarlarını görüntüler. Merhaba aşağıdakilerden birini yapın: 
      * Varolan bir Docker ana bilgisayara varsa, web uygulaması tooit dağıtabilirsiniz.
      * toocreate Docker ana hello yeşil artı işaretini tıklatın (**+**).  
       Merhaba **oluşturma Docker ana** iletişim kutusu açılır. 

      ![Docker kapsayıcısı üzerinde Azure Sihirbazı'nı dağıtma][PUB04a]

4. Merhaba, **hello yeni sanal makine yapılandırma** penceresinde hello aşağıdaki Docker ana bilgisayarınız hakkında bilgi sağlar. (hello sihirbaz sizin için hello bilgilerin çoğunu otomatik olarak oluşturur, ancak herhangi birini değiştirebilirsiniz.) 

   a. Merhaba, **adı** kutusuna, hello Docker ana bilgisayar için benzersiz bir ad girin. (Bu, hello almak için değil, daha önce belirtilen Docker görüntü adı hello aynı olur.) 
    
   b. Merhaba, **abonelik** kutusuna, hello ana bilgisayarınız için kullandığınız Azure aboneliğini girin. 
      
   c. Merhaba, **bölge** kutusuna, ana bilgisayarınız bulunduğu hello coğrafi girin.
      
   d. Merhaba üzerinde **işletim sistemi ve boyutu** sekmesinde, aşağıdaki hello:      
      * **Ana bilgisayar işletim sistemi**: hello işletim sistemi hello sanal makine için ana bilgisayarınız içeren girin. 
      * **Boyutu**: ana bilgisayarınız için hello sanal makine boyutu girin.   
       
   e. Merhaba üzerinde **kaynak grubu** sekmesinde, hello aşağıdakilerden birini seçin:      
      * **Yeni kaynak grubu**: konağınız için bir kaynak grubu oluşturun.
      * **Varolan bir kaynak grubu**: Azure hesabınızdan var olan bir kaynak grubu belirtin. 
       
   f. Merhaba üzerinde **ağ** sekmesinde, hello aşağıdakilerden birini seçin:      
      * **Yeni sanal ağ**: konağınız için bir sanal ağ oluşturun.
      * **Varolan bir sanal ağı**: Azure hesabınızdan var olan bir sanal ağ belirtin. 
       
   g. Merhaba üzerinde **depolama** sekmesinde, hello aşağıdakilerden birini seçin:      
      * **Yeni depolama hesabı**: konağınız için bir depolama hesabı oluşturun.
      * **Varolan bir depolama hesabı**: Azure hesabınızdan mevcut bir depolama hesabını belirtin.
       
5. **İleri**’ye tıklayın.  
     Merhaba **günlük kimlik bilgilerini yapılandırın ve bağlantı noktası ayarları** penceresi açılır.

      ![kimlik bilgileri ve bağlantı noktası ayarları penceresinde Hello Yapılandır günlük][PUB05]

6. Seçenekler aşağıdaki hello birini seçin:

      * **Azure anahtar Kasası'kimlik bilgileri içe**: önceden kaydedilen bir Azure aboneliğinizde depolanan kimlik bilgileri kümesi belirtin.

          > [!NOTE]
          > Bir hesabın veya hizmet sorumlusu ile oluşturulan bir Azure anahtar kasası başka bir hesap veya hello abonelik paylaşan hizmet sorumlusu tarafından otomatik olarak erişilebilir değil. tooallow başka bir hesap veya hizmet asıl toouse hello anahtar kasası, hello Azure portal tooadd hello hesabı ya da hizmet sorumlusu kullanmanız gerekir.

      * **Yeni oturum açma kimlik bilgileri**: yeni bir oturum açma kimlik bilgileri kümesi oluşturun. Bu seçeneği seçerseniz, aşağıdaki hello:

        a. Hello üzerinde **VM kimlik** sekmesinde, Docker ana bilgisayarınız hello sanal makinesi oturum açma kimlik bilgilerini aşağıdaki hello sağlayın: * **kullanıcıadı**: sanal makine oturumunuzla hello kullanıcı adı girin kimlik bilgileri.
             * **Parola** ve **Onayla**: hello parola için sanal makine oturum açma kimlik bilgilerinizi girin.
             * **SSH**: Docker ana bilgisayarınız hello güvenli Kabuk (SSH) ayarlarını girin. Seçenekler aşağıdaki hello birini seçebilirsiniz: * **hiçbiri**: sanal makineniz SSH bağlantılara izin vermiyor belirtir.
                * **Otomatik oluşturma**: hello SSH yoluyla bağlanmak için gerekli ayarları otomatik olarak oluşturur.
                * **Dizine alma**: toospecify önceden kaydedilmiş SSH ayarları kümesini içeren bir dizini sağlar. Merhaba dizin, aşağıdaki iki dosyaları hello içermelidir:
                
                  * *id_rsa*: Contains hello RSA identification for a user.
                  * *id_rsa.pub*: Contains hello RSA public key that is used for authentication.
            
        b. Merhaba üzerinde **Docker arka plan programı erişim** sekmesinde, aşağıdaki bilgilerle hello sağlayın:

          ![Docker konak oluştur][PUB06]
    
             * **Docker Daemon port**: Enter hello unique TCP port for your Docker host.
             * **TLS Security**: Enter hello Transport Layer Security settings for your Docker host. You can choose from hello following options:
                * **None**: Specifies that your virtual machine does not allow TLS connections.
                * **Auto-generate**: Automatically creates hello requisite settings for connecting via TLS.
                * **Import from directory**: Specifies a directory that contains a set of previously saved TLS settings. hello directory must contain hello following six files: 
                   * *ca.pem* and *ca-key.pem*: Contain hello certificate and public key for hello TLS Certificate Authority.
                   * *cert.pem* and *key.pem*: Contain client certificate and public key which will be used for TLS authentication.
                   * *server.pem* and *server-key.pem*: Contain hello client certificate and public key that is used for TLS authentication.

7. Merhaba gerekli bilgileri girdikten sonra tıklatın **son**.  
    Merhaba **azure'da dağıtmak Docker kapsayıcısı** Sihirbazı görüntülenir.

   ![Docker kapsayıcısı üzerinde Azure Sihirbazı'nı dağıtma][PUB07]

8. **İleri**’ye tıklayın.  
    Merhaba **oluşturulan hello Docker kapsayıcısı toobe yapılandırma** penceresi açılır.

   ![Merhaba yapılandırma hello Docker kapsayıcısı oluşturulan toobe penceresi][PUB08]

9. Merhaba, **oluşturulan hello Docker kapsayıcısı toobe yapılandırma** penceresinde, aşağıdaki bilgilerle hello sağlayın: 

   a. Merhaba, **Docker kapsayıcısı adı** kutusuna, Docker kapsayıcısı için benzersiz bir ad girin.

   b. Docker görüntüleri aşağıdaki hello birini seçin: 

      * **Önceden tanımlanmış Docker görüntü**: azure'dan önceden var olan bir Docker görüntüsü belirtin. 

        > [!NOTE]
        > Bu kutu Docker görüntülerinde Hello listesi, birkaç görüntülerini oluşur Azure Araç Seti açıldı, hello toopatch yapılandırılmış, yapı otomatik olarak dağıtılır. 

      * **Özel Dockerfile**: yerel bilgisayarınızdan önceden kaydedilmiş bir Dockerfile belirtin.

        > [!NOTE]
        > Bu, kendi Dockerfile toodeploy isteyen geliştiriciler için daha gelişmiş bir özelliktir. Ancak, kendi Dockerfile doğru bir şekilde yapıldığından bu seçeneği tooensure kullanan toodevelopers değildir. Hello Azure Araç Seti özel bir Dockerfile hello içeriği doğrulamaz çünkü hello Dockerfile sorunları varsa hello dağıtım başarısız olabilir. Ayrıca, Hello Azure Araç Seti hello özel Dockerfile toocontain bir web uygulaması yapı beklediği tooopen bir HTTP bağlantısı çalışır. Geliştiriciler farklı türde bir yapı yayımlarsanız, bunlar dağıtım sonrası zararsız hatalar alabilirsiniz.

   c. Merhaba, **bağlantı noktası ayarları** kutusuna, hello benzersiz TCP bağlantı noktası için bağlama, Docker kapsayıcısı girin. 

10. Merhaba önceki adımları tamamladıktan sonra tıklatın **son**. 

Hello Azure araç seti, web uygulama tooAzure Docker kapsayıcısı içinde dağıtmaya başlar. Dağıtılan hello arka planda Intellij toobe yapılandırmadığınız sürece bir **tooAzure dağıtma** ilerleme çubuğu görüntülenir. 

![Merhaba dağıtım ilerleme çubuğu][PUB09]

<a name="artifacts"></a>
## <a name="additional-information-about-creating-artifacts"></a>Yapıları oluşturma hakkında ek bilgi

bir dağıtım için hazır yapı toocreate hello aşağıdaki:

1. Web uygulaması projenizin Intellij içinde açın.

2. Tıklatın **dosya**ve ardından **proje yapısını**.

   ![Merhaba proje yapısını komutu][ART01]

3. tooadd yapı bir hello yeşil artı işaretini tıklatın (**+**) ve ardından **Web uygulaması: Arşiv**.

   ![Merhaba "Web uygulaması: arşivi" komutu][ART02]

4. Merhaba, **adı** kutusuna, yapı için bir ad girin (Merhaba içermez *.war* uzantısı) ve ardından **Tamam**.

   ![Merhaba yapı adı kutusu][ART03]

Intellij yapıları oluşturma hakkında daha fazla bilgi için bkz: [yapıları yapılandırma] hello JetBrains Web sitesinde.

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

Azure Java ile kullanma hakkında daha fazla bilgi için bkz: Merhaba [Azure Java Geliştirici Merkezi] ve hello [Visual Studio Team Services için Java Araçları].

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
[yapıları yapılandırma]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html

<!-- IMG List -->

[PUB01]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB01.png
[PUB02]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB02.png
[PUB03]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB03.png
[PUB04a]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04a.png
[PUB04b]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04b.png
[PUB04c]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04c.png
[PUB04d]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04d.png
[PUB05]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB05.png
[PUB06]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB06.png
[PUB07]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB07.png
[PUB08]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB08.png
[PUB09]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB09.png

[ART01]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/ART01.png
[ART02]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/ART02.png
[ART03]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/ART03.png
