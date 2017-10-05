---
title: "Intellij için Azure araç setini kullanarak bir Docker kapsayıcısı yayımlama | Microsoft Docs"
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
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 96680319a6c4c0f0a4673cd6303a5b172f428797
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-the-azure-toolkit-for-intellij"></a>Intellij için Azure araç setini kullanarak bir web uygulaması Docker kapsayıcısı Yayımla

Docker, web uygulamalarını dağıtmak için yaygın olarak kullanılan bir yöntem kapsayıcılardır. Docker kapsayıcıları kullanarak, geliştiricilerin kendi tüm proje dosyalarını ve tek bir paket için bir sunucu dağıtımı için bağımlılıkları birleştirebilir. Intellij için Azure araç seti, ekleyerek Java geliştiriciler için bu işlemi basitleştirir *Docker kapsayıcısı olarak Yayımla* Microsoft Azure dağıtım özellikleri. Bu makalede, Azure, uygulamalarınızı Docker kapsayıcı olarak yayımlamak için gereken adımları açıklanmaktadır.

> [!NOTE]
>
> Docker hakkında daha fazla bilgi edinilebilir [Docker Web sitesi].
>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="publish-your-web-app-to-azure-by-using-a-docker-container"></a>Docker kapsayıcısı kullanarak Azure için web uygulamanızı yayınlama

> [!NOTE]
> * Web uygulamanızı yayımlamak için bir dağıtım için hazır yapı oluşturmanız gerekir. Daha fazla bilgi için bkz: [yapıları oluşturma hakkında ek bilgi](#artifacts) bölümü.
>
> * En az bir kez Dağıtım Sihirbazı'nı tamamladıktan sonra sihirbazı yeniden çalıştırın, ayarların çoğu varsayılanları olarak kullanılır.
>

1. Web uygulaması projenizin Intellij içinde açın.

2. Başlatmak için **Docker kapsayıcısı olarak Yayımla** Sihirbazı, aşağıdakilerden birini yapın:

   * İçinde **proje** araç penceresi, projenize sağ tıklayın, **Azure**ve ardından **Docker kapsayıcısı olarak Yayımla**:

      ![Docker kapsayıcısı komut olarak Yayımla][PUB01]

   * Intellij araç çubuğunda tıklatın **Yayımla grup** düğmesine tıklayın ve ardından **Docker kapsayıcısı olarak Yayımla**:

      ![Docker kapsayıcısı komut olarak Yayımla][PUB02]  
    **Azure'da dağıtmak Docker kapsayıcısı** Sihirbazı açılır.

   ![Azure Sihirbazı dağıtmak Docker kapsayıcısı][PUB03]

3. İçinde **bir görüntü adı yazın, yapı'nın yolu seçin ve kullanılacak bir Docker ana denetleyin** penceresinde aşağıdakileri yapın: 

   a. İçinde **Docker görüntü adı** kutusuna, Docker ana bilgisayar için benzersiz bir ad girin. (Sihirbaz otomatik olarak bir ad oluşturur, ancak bunu değiştirebilirsiniz.) 

   b. **Ana** alanı önceden oluşturmuş olduğunuz tüm Docker ana bilgisayarlarını görüntüler. Aşağıdakilerden birini yapın: 
      * Varolan bir Docker ana bilgisayara varsa, web uygulamanızı dağıtabilirsiniz.
      * Docker ana bilgisayar oluşturmak için yeşil artı işaretini tıklatın (**+**).  
       **Oluşturma Docker ana** iletişim kutusu açılır. 

      ![Docker kapsayıcısı üzerinde Azure Sihirbazı'nı dağıtma][PUB04a]

4. İçinde **yeni sanal makine yapılandırma** penceresinde, Docker ana bilgisayarınız hakkında aşağıdaki bilgileri sağlayın. (Sihirbaz için bu bilgileri çoğunu otomatik olarak oluşturur, ancak herhangi birini değiştirebilirsiniz.) 

   a. İçinde **adı** kutusuna, Docker ana bilgisayar için benzersiz bir ad girin. (Bu, daha önce belirttiğiniz Docker görüntü adı ile aynı değildir.) 
    
   b. İçinde **abonelik** kutusuna, ana bilgisayarınız için kullandığınız Azure aboneliğini girin. 
      
   c. İçinde **bölge** kutusuna, ana bilgisayarınız bulunduğu coğrafi bölge girin.
      
   d. Üzerinde **işletim sistemi ve boyutu** sekmesinde, aşağıdakileri yapın:      
      * **Ana bilgisayar işletim sistemi**: ana bilgisayarınız içeren sanal makine için işletim sistemi girin. 
      * **Boyutu**: ana bilgisayarınız için sanal makine boyutu girin.   
       
   e. Üzerinde **kaynak grubu** sekmesinde, aşağıdakilerden birini seçin:      
      * **Yeni kaynak grubu**: konağınız için bir kaynak grubu oluşturun.
      * **Varolan bir kaynak grubu**: Azure hesabınızdan var olan bir kaynak grubu belirtin. 
       
   f. Üzerinde **ağ** sekmesinde, aşağıdakilerden birini seçin:      
      * **Yeni sanal ağ**: konağınız için bir sanal ağ oluşturun.
      * **Varolan bir sanal ağı**: Azure hesabınızdan var olan bir sanal ağ belirtin. 
       
   g. Üzerinde **depolama** sekmesinde, aşağıdakilerden birini seçin:      
      * **Yeni depolama hesabı**: konağınız için bir depolama hesabı oluşturun.
      * **Varolan bir depolama hesabı**: Azure hesabınızdan mevcut bir depolama hesabını belirtin.
       
5. **İleri**’ye tıklayın.  
     **Günlük kimlik bilgilerini yapılandırın ve bağlantı noktası ayarları** penceresi açılır.

      ![Yapılandırma oturum açma kimlik bilgileri ve bağlantı noktası ayarları penceresi][PUB05]

6. Aşağıdaki seçeneklerden birini seçin:

      * **Azure anahtar Kasası'kimlik bilgileri içe**: önceden kaydedilen bir Azure aboneliğinizde depolanan kimlik bilgileri kümesi belirtin.

          > [!NOTE]
          > Bir hesabın veya hizmet sorumlusu ile oluşturulan bir Azure anahtar kasası başka bir hesap veya abonelik paylaşan hizmet sorumlusu tarafından otomatik olarak erişilebilir değil. Başka bir hesap veya hizmet asıl anahtar kasası kullanmaya izin vermek için hesabı veya hizmet sorumlusu eklemek için Azure Portalı'nı kullanmanız gerekir.

      * **Yeni oturum açma kimlik bilgileri**: yeni bir oturum açma kimlik bilgileri kümesi oluşturun. Bu seçeneği seçerseniz, aşağıdakileri yapın:

        a. Üzerinde **VM kimlik** sekmesinde, Docker ana bilgisayarın sanal makine oturum açma kimlik bilgileri için aşağıdaki bilgileri sağlayın: * **kullanıcıadı**: kullanıcı için sanal makine oturum açma kimlik bilgilerinizi girin.
             * **Parola** ve **Onayla**: parola için sanal makine oturum açma kimlik bilgilerinizi girin.
             * **SSH**: Docker ana bilgisayarınız Güvenli Kabuk (SSH) ayarlarını girin. Aşağıdaki seçeneklerden birini seçebilirsiniz: * **hiçbiri**: sanal makineniz SSH bağlantılara izin vermiyor belirtir.
                * **Otomatik oluşturma**: SSH yoluyla bağlanmak için gerekli ayarları otomatik olarak oluşturur.
                * **Dizine alma**: önceden kaydedilmiş SSH ayarları kümesini içeren bir dizini belirtmenize olanak tanır. Dizin, aşağıdaki iki dosyada içermelidir:
                
                  * *id_rsa*: Contains the RSA identification for a user.
                  * *id_rsa.pub*: Contains the RSA public key that is used for authentication.
            
        b. Üzerinde **Docker arka plan programı erişim** sekmesinde, aşağıdaki bilgileri sağlayın:

          ![Docker konak oluştur][PUB06]
    
             * **Docker Daemon port**: Enter the unique TCP port for your Docker host.
             * **TLS Security**: Enter the Transport Layer Security settings for your Docker host. You can choose from the following options:
                * **None**: Specifies that your virtual machine does not allow TLS connections.
                * **Auto-generate**: Automatically creates the requisite settings for connecting via TLS.
                * **Import from directory**: Specifies a directory that contains a set of previously saved TLS settings. The directory must contain the following six files: 
                   * *ca.pem* and *ca-key.pem*: Contain the certificate and public key for the TLS Certificate Authority.
                   * *cert.pem* and *key.pem*: Contain client certificate and public key which will be used for TLS authentication.
                   * *server.pem* and *server-key.pem*: Contain the client certificate and public key that is used for TLS authentication.

7. Gerekli bilgileri girdikten sonra tıklatın **son**.  
    **Azure'da dağıtmak Docker kapsayıcısı** Sihirbazı görüntülenir.

   ![Docker kapsayıcısı üzerinde Azure Sihirbazı'nı dağıtma][PUB07]

8. **İleri**’ye tıklayın.  
    **Oluşturulacak Docker kapsayıcısı yapılandırma** penceresi açılır.

   ![Pencere oluşturulması için Docker kapsayıcısı Yapılandır][PUB08]

9. İçinde **oluşturulacak Docker kapsayıcısı yapılandırma** penceresinde, aşağıdaki bilgileri sağlayın: 

   a. İçinde **Docker kapsayıcısı adı** kutusuna, Docker kapsayıcısı için benzersiz bir ad girin.

   b. Aşağıdaki Docker görüntülerden birini seçin: 

      * **Önceden tanımlanmış Docker görüntü**: azure'dan önceden var olan bir Docker görüntüsü belirtin. 

        > [!NOTE]
        > Bu kutu Docker görüntülerinde listesi, Azure Araç Seti için yapılandırılmış birden fazla görüntülerinin oluşur, yapı otomatik olarak dağıtılır böylece düzeltme eki. 

      * **Özel Dockerfile**: yerel bilgisayarınızdan önceden kaydedilmiş bir Dockerfile belirtin.

        > [!NOTE]
        > Bu, kendi Dockerfile dağıtmak isteyen geliştiriciler için daha gelişmiş bir özelliktir. Ancak, kendi Dockerfile doğru bir şekilde yapıldığından emin olmak için bu seçeneği kullanın geliştiriciler kadar olur. Azure Araç Seti özel bir Dockerfile içeriği doğrulamaz çünkü Dockerfile sorunları varsa dağıtım başarısız olabilir. Ayrıca, Azure Araç Seti web uygulama yapı içerecek şekilde özel Dockerfile beklediği bir HTTP bağlantısı açmaya çalışır. Geliştiriciler farklı türde bir yapı yayımlarsanız, bunlar dağıtım sonrası zararsız hatalar alabilirsiniz.

   c. İçinde **bağlantı noktası ayarları** kutusuna, Docker kapsayıcısı için benzersiz TCP bağlantı noktası bağlama girin. 

10. Yukarıdaki adımları tamamladıktan sonra tıklatın **son**. 

Azure Araç Seti Azure Docker kapsayıcısı içinde web uygulamanızı dağıtmaya başlar. Arka planda dağıtılacak Intellij yapılandırmadığınız sürece bir **Azure'a dağıtan** ilerleme çubuğu görüntülenir. 

![Dağıtım ilerleme çubuğu][PUB09]

<a name="artifacts"></a>
## <a name="additional-information-about-creating-artifacts"></a>Yapıları oluşturma hakkında ek bilgi

Bir dağıtım için hazır yapı oluşturmak için aşağıdakileri yapın:

1. Web uygulaması projenizin Intellij içinde açın.

2. Tıklatın **dosya**ve ardından **proje yapısını**.

   ![Proje yapısı komutu][ART01]

3. Bir yapı eklemek için yeşil artı işaretini tıklatın (**+**) ve ardından **Web uygulaması: Arşiv**.

   !["Web uygulaması: arşivi" komutu][ART02]

4. İçinde **adı** kutusuna, yapı için bir ad girin (içermeyen *.war* uzantısı) ve ardından **Tamam**.

   ![Yapı adı kutusu][ART03]

Intellij yapıları oluşturma hakkında daha fazla bilgi için bkz: [yapıları yapılandırma] JetBrains Web sitesinde.

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

Azure’u Java ile kullanma hakkında daha fazla bilgi edinmek için bkz. [Azure Java Geliştirici Merkezi] ve [Visual Studio Team Services için Java Araçları].

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
