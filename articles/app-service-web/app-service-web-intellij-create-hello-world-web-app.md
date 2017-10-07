---
title: "aaaCreate Intellij temel Azure web uygulamasında | Microsoft Docs"
description: "Bu öğretici nasıl toouse hello Azure Araç Seti için Intellij toocreate bir Hello World Web uygulaması için Azure gösterir."
services: app-service\web
documentationcenter: java
author: selvasingh
manager: erikre
editor: 
ms.assetid: 75ce7b36-e3ae-491d-8305-4b42ce37db4e
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 4667497213cac3ddf754d164e614c809f338cce5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-basic-azure-web-app-in-intellij"></a>Intellij içinde bir temel Azure web uygulaması oluşturma
Bu öğreticide gösterilmiştir nasıl toocreate ve hello kullanarak bir Web uygulaması gibi temel bir Hello World uygulama tooAzure dağıtma [Intellij için Azure Araç Seti]. Kolaylık olması için temel bir JSP örneği gösterilir, ancak Azure dağıtım ilgili olduğu kadar benzer adımlar bir Java servlet için uygun olacaktır.

Bu öğreticiyi tamamladıktan sonra uygulamanızı bir web tarayıcısında görüntülediğinizde çizim aşağıdaki benzer toohello görünür:

![Örnek bir Web sayfası][01]

## <a name="prerequisites"></a>Ön koşullar
* Bir Java Geliştirme Seti (JDK), v 1.8 veya üzeri.
* Intellij Idea Ultimate Edition. Bu adresten yüklenebilir <https://www.jetbrains.com/idea/download/index.html>.
* Dağıtım bir Java tabanlı web sunucusu veya uygulama sunucusu gibi [Apache Tomcat] veya [Jetty].
* Öğesinden alınan bir Azure aboneliği <https://azure.microsoft.com/free/> veya <http://azure.microsoft.com/pricing/purchase-options/>.
* Merhaba [Intellij için Azure Araç Seti]. Hello Azure araç setini yükleme hakkında daha fazla bilgi için bkz: [yükleme hello Intellij için Azure Araç Seti].

## <a name="toocreate-a-hello-world-application"></a>toocreate Merhaba Dünya uygulaması
İlk olarak, bir Java projesi oluşturma ile başlayacağız devre dışı.

1. Intellij başlatın ve hello tıklatın **dosya** menüsünde, ardından **yeni**ve ardından **proje**.
   
    ![Dosya yeni proje][02]
2. Merhaba yeni proje iletişim kutusunda seçin **Java**, ardından **Web uygulaması**ve ardından **yeni** tooadd proje SDK.
   
    ![Yeni Proje İletişim Kutusu][03a]
   
3. JDK iletişim kutusu için Hello giriş dizini seçin, select Merhaba, JDK yüklendiği klasörü ve ardından **Tamam**. Tıklatın **sonraki** hello yeni proje iletişim kutusu toocontinue içinde.
   
    ![JDK giriş dizini belirtin][03b]
4. Bu öğreticinin amaçları doğrultusunda hello proje adı **Java-Web-App-üzerinde-Azure**ve ardından **son**.
   
    ![Yeni Proje İletişim Kutusu][04]
5. Intellij'ın Proje Gezgini görünümü içinde genişletmek **Java-Web-App-üzerinde-Azure**, ardından **web**, çift tıklayın ve ardından **index.jsp**.
   
    ![Açık dizin sayfası][05c]
6. İndex.jsp dosyası içinde Intellij açıldığında, metin toodynamically görünümünde eklemek **Merhaba Dünya!** Merhaba varolan içinde `<body>` öğesi. Güncelleştirilmiş `<body>` içeriği aşağıdaki örneğine hello benzer:
   
    `<body><b><% out.println("Hello World!"); %></b></body>` 
7. İndex.jsp kaydedin.

## <a name="toodeploy-your-application-tooan-azure-web-app-container"></a>toodeploy, uygulama tooan Azure Web uygulaması kapsayıcısı
Java web uygulaması tooAzure dağıtabilir miyim birkaç yolu vardır. Bu öğretici hello basit açıklar: uygulamanızı dağıtılan tooan Azure Web uygulaması kapsayıcı olacaktır - hiçbir özel Proje türü ya da ek araçlar gereklidir. Merhaba JDK ve hello web kapsayıcısı yazılım; böylece hiçbir gerek tooupload kendi sizin için Azure tarafından sağlanacak; ihtiyacınız olan tek şey, Java Web uygulaması. Sonuç olarak, uygulamanız için yayımlama işlemi hello saniye, dakika sürer.

Uygulamanızı yayınlamadan önce modülü ayarlarınızı ilk tooconfigure gerekir. toodo, bu nedenle, hello aşağıdaki adımları kullanın:

1. Intellij'ın Proje Gezgini'nde hello sağ **Java-Web-App-üzerinde-Azure** projesi. Merhaba bağlam menüsü görüntülendiğinde **açık modülü ayarları**.

    ![Modül Ayarları'nı açın][05a]
2. Merhaba Proje Yapısı iletişim kutusu görüntülendiğinde:

   a. Tıklatın **yapıları** hello listesinde **proje ayarları**.
   b. Merhaba hello yapı adını değiştir **adı** boşluk veya özel karakterler içermiyor kutusuna; hello adı hello Tekdüzen Kaynak Tanımlayıcısı (URI) kullanılacağından bu gereklidir.
   c. Değişiklik hello **türü** çok**Web uygulaması: Arşiv**.
   d. Tıklatın **Tamam** tooclose hello Proje Yapısı iletişim kutusu.

    ![Modül Ayarları'nı açın][05b]

Modül ayarlarınızı yapılandırdığınızda, aşağıdaki adımları hello kullanarak uygulama tooAzure yayımlayabilirsiniz:

1. Intellij'ın Proje Gezgini'nde hello sağ **Java-Web-App-üzerinde-Azure** projesi. Merhaba bağlam menüsü görüntülendiğinde seçin **Azure**ve ardından **Azure Web uygulaması olarak Yayımla...**
   
    ![Azure yayımlama bağlam menüsü][06]
2. Zaten Intellij Azure'dan oturum açmış değil, Azure hesabınızda istendiğinde toosign olacaktır. (Birden çok Azure hesabınız yoksa, toobe göründükleri olsa bile bazı hello istemleri hello oturum açma işlemi sırasında birden fazla kez gösterilebilir aynı hello. Bu durumda, yönergeleri toofollow hello oturum devam.)
   
    ![Azure oturum açma iletişim kutusu][07]
3. Azure hesabınızda oturumu başarıyla sonra hello **Aboneliklerini Yönet** iletişim kutusunda kimlik bilgilerinizle ilişkili Aboneliklerin listesini görüntüler. (Listelenen birden çok abonelik ve yalnızca belirli bir alt kümesini ile toowork istiyorsanız, isteğe bağlı olarak toouse istemediğiniz hello abonelikleri temizleyin.) Aboneliklerinizi seçildiğinde tıklatın **Kapat**.
   
    ![Aboneliklerini Yönetme][08]
4. Ne zaman hello **tooAzure Web uygulaması kapsayıcı dağıtma** iletişim kutusu görüntülenirse, daha önce oluşturduğunuz herhangi bir Web uygulaması kapsayıcıdaki görüntülenir; herhangi bir kapsayıcıdaki oluşturmadıysanız hello listesi boş olur.
   
    ![Uygulama kapsayıcıları][09]
5. Bir Azure Web uygulaması kapsayıcısı önce ya da toopublish isterseniz, uygulama tooa yeni kapsayıcı oluşturmadıysanız, hello aşağıdaki adımları kullanın. Aksi takdirde, var olan bir Web uygulaması kapsayıcıyı seçin ve toostep aşağıda 6 atlayın.
   
   1. ' I tıklatın**+**
      
       ![Uygulama kapsayıcısı Ekle][10]
   2. Merhaba **yeni Web uygulaması kapsayıcı** iletişim kutusu görüntülenir, olacağı Merhaba sonraki birkaç adım kullanılır.
      
       ![Yeni uygulama kapsayıcısı][11a]
   3. Girin bir **DNS etiketi** Web uygulama kapsayıcısı için; bu hello yaprak DNS etiketi hello konak URL'nin, web uygulamanız için Azure içinde oluşturacak. Bu hello adı kullanılabilir ve tooAzure Web uygulaması adlandırma gereksinimlerini uygun unutmayın.
   4. Hello içinde **Web kapsayıcısına** açılır menü, uygulamanız için uygun yazılım select hello.
      
       Şu anda, Tomcat 8, Tomcat 7 veya Jetty 9 seçebilirsiniz. Seçili hello yazılım yeni bir dağıtımını Azure tarafından sağlanacak ve JDK Oracle tarafından oluşturulan ve Azure tarafından sağlanan 8'in yeni bir dağıtım çalıştırılır.
   5. Merhaba, **abonelik** açılır menü, bu dağıtım için kullanmak istediğiniz toouse select hello abonelik.
   6. Merhaba, **kaynak grubu** açılır menüsünde, istediğiniz tooassociate Web uygulamanızı seçin hello kaynak grubu. (Örneğin, bunlar birlikte silinebilir böylece, toogroup kaynakları birlikte ilgili azure kaynak gruplarını izin.)
      
       Atla toostep g veya kullanım hello aşağıdaki yeni bir kaynak grubu toocreate adımlar ve (varsa), var olan bir kaynak grubunu seçebilirsiniz:
      
      * Seçin  **&lt; &lt; yeni kaynak grubu oluştur &gt; &gt;**  hello içinde **kaynak grubu** açılır menü.
      * Merhaba **yeni kaynak grubu** iletişim kutusu görüntülenir:
        
          ![Yeni kaynak grubu][12]
      * Merhaba hello içinde **adı** metin kutusuna, yeni kaynak grubunuz için bir ad belirtin.
      * Merhaba hello içinde **bölge** açılır menüsünde, select hello uygun Azure veri merkezi kaynak grubunuz için konum.
      * **Tamam** düğmesine tıklayın.
   7. Merhaba **App Service planı** açılır menü Merhaba, seçili kaynak grubu ile ilişkili hello uygulama hizmeti planları listeler. (Web uygulamanızı, fiyatlandırma katmanı ve hello işlem örnek boyutu hello hello konumunu gibi bilgileri belirtir bir uygulama hizmeti planı. Tek bir uygulama hizmeti planı ayrı olarak belirli bir Web uygulaması dağıtımından korunan neden olan ve birden çok Web uygulamaları için kullanılabilir.)
      
       (Varsa) var olan bir uygulama hizmeti planı seçebilirsiniz ve toostep h aşağıdaki atlayacak veya adımları toocreate yeni bir uygulama hizmeti planı aşağıdaki hello kullanın:
      
      * Seçin  **&lt; &lt; yeni uygulama hizmeti planı oluştur &gt; &gt;**  hello içinde **App Service planı** açılır menü.
      * Merhaba **yeni uygulama hizmeti planı** iletişim kutusu görüntülenir:
        
          ![Yeni uygulama hizmeti planı][13]
      * Merhaba hello içinde **adı** metin kutusuna, yeni uygulama hizmeti planınız için bir ad belirtin.
      * Merhaba hello içinde **konumu** açılır menüsünde, select hello uygun Azure veri merkezi hello planı için konum.
      * Merhaba hello içinde **fiyatlandırma katmanı** açılır menüsünde, select hello hello planlama fiyatlandırma uygun. Test amacıyla seçebileceğiniz **serbest**.
      * Merhaba hello içinde **örnek boyutu** açılır menü, hello planı için seçme hello uygun örnek boyutu. Test amacıyla seçebileceğiniz **küçük**.
      * **Tamam** düğmesine tıklayın.
   8. (İsteğe bağlı) Varsayılan olarak, Java 8 yeni bir dağıtımını otomatik, JVM Azure tooyour web uygulaması kapsayıcı tarafından dağıtılır. Ancak, farklı sürüm ve hello JVM dağıtımını seçebilirsiniz. toodo, bu nedenle, hello aşağıdaki adımları kullanın:
      
      * Merhaba tıklatın **JDK** hello sekmesinde **yeni Web uygulaması kapsayıcı** iletişim kutusu.
      * Seçenekler aşağıdaki hello birini seçebilirsiniz:
        
        * Merhaba varsayılan Azure tarafından sunulan JDK dağıtma
        * Bir 3. taraf JDK Azure üzerinde kullanılabilir olan ek JDKs aşağı açılan listesinden dağıtma
        * ZIP dosyası olarak ve ya da paketlenmesi gereken özel bir JDK dağıtımı Azure depolama hesabınızdaki veya genel olarak kullanılabilir
        
        ![Yeni uygulama kapsayıcı JDK sekmesi][11b]
   9. Tüm hello yukarıdaki adımları tamamladıktan sonra hello yeni Web uygulaması kapsayıcısı iletişim kutusunda aşağıdaki çizimde hello benzemelidir:
      
       ![Yeni uygulama kapsayıcısı][14]
   10. Tıklatın **Tamam** yeni Web uygulaması kapsayıcısının toocomplete hello oluşturma.
       
        Merhaba Web uygulaması kapsayıcıları toobe hello listesi için birkaç saniye bekleyin yenilenir ve hello listesinde yeni oluşturulan web uygulaması kapsayıcınız artık seçili olmalıdır.
6. Hazır toocomplete hello ilk dağıtımı, Web uygulaması tooAzure sunulmuştur; tıklatın **Tamam** toodeploy, Java uygulama toohello seçili Web uygulaması kapsayıcı. Varsayılan olarak, uygulamanızı bir alt dizin hello uygulama sunucusu dağıtılır. Merhaba kök uygulaması dağıtılan toobe istiyorsanız hello denetleyin **tooroot dağıtmak** tıklatmadan önce onay kutusunu **Tamam**.
   
    ![TooAzure dağıtma][15]
7. Ardından, hello görmelisiniz **Azure etkinlik günlüğü** hello dağıtım durumu, Web uygulamanızın gösterecektir görünümü.
   
    ![İlerleme göstergesi][16]
   
    Merhaba, Web uygulaması tooAzure dağıtma işlemi, yalnızca birkaç saniye almalıdır toocomplete. Uygulama hazır gördüğünüzde adlı bir bağlantı **yayımlanan** hello içinde **durum** sütun. Hello bağlantısını tıklattığınızda sizi tooyour dağıtılmış Web uygulamanızın giriş sayfasına götürür veya bölüm toobrowse tooyour web uygulama aşağıdaki hello hello adımları kullanabilirsiniz.

## <a name="browsing-tooyour-web-app-on-azure"></a>Gözatma tooyour Azure üzerinde Web uygulaması
toobrowse tooyour Azure Web uygulamasında, kullanabileceğiniz hello **Azure Gezgini** görünümü.

Merhaba, **Azure Gezgini** görünüm zaten açık, ardından tıklayarak açabilirsiniz **Görünüm** Intellij, menüde ardından **aracı Windows**ve ardından  **Hizmet Explorer**. Daha önce oturum açmamış olan, bu toodo şekilde ister.

Ne zaman hello **Azure Gezgini** görünümü görüntülenir, kullanma, bu adımları toobrowse tooyour Web uygulaması izleyin: 

1. Merhaba genişletin **Azure** düğümü.
2. Merhaba genişletin **Web Apps** düğümü. 
3. Web uygulaması sağ hello istenen.
4. Merhaba bağlam menüsü görüntülendiğinde **tarayıcıda aç**.
   
    ![Web uygulaması Gözat][17]

## <a name="updating-your-web-app"></a>Web uygulamanızı güncelleştirme
Azure Web uygulaması çalıştıran var olan bir güncelleştirme hızlı ve kolay bir işlemdir ve güncelleştirmek için iki seçeneğiniz vardır:

* Varolan bir Java Web uygulaması dağıtımını hello güncelleştirebilirsiniz.
* Ek bir Java uygulaması toohello yayımlayabilirsiniz aynı Web uygulama kapsayıcısı.

Her iki durumda da hello işlemi aynıdır ve yalnızca birkaç saniye sürer:

1. Merhaba Intellij proje Gezgini'nde tooupdate istediğiniz ya da Web uygulaması kapsayıcı varolan tooan eklemek Merhaba Java uygulaması sağ tıklayın.
2. Merhaba bağlam menüsü görüntülendiğinde seçin **Azure** ve ardından **Azure Web uygulaması olarak Yayımla...**
3. Zaten daha önce oturum açtıktan sonra var olan Web uygulaması kapsayıcıları listesini görürsünüz. Select toopublish istediğiniz ya da Java uygulama tooand tıklatmanız yeniden yayımlama hello **Tamam**.

Daha sonra birkaç saniye hello **Azure etkinlik günlüğü** görünümü güncelleştirilmiş dağıtımınız olarak göster **yayımlanan** ve mümkün tooverify güncelleştirilmiş uygulamanız bir web tarayıcısında olacaktır.

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a>Başlatma, durdurma veya var olan bir web uygulamasının yeniden başlatma
toostart veya mevcut bir Azure Web uygulaması kapsayıcısı (tüm dağıtılan hello Java uygulamaları içine dahil), durdurmak, hello kullanabilirsiniz **Azure Gezgini** görünümü.

Merhaba, **Azure Gezgini** görünüm zaten açık, ardından tıklayarak açabilirsiniz **Görünüm** Intellij, menüde ardından **aracı Windows**ve ardından  **Hizmet Explorer**. Daha önce oturum açmamış olan, bu toodo şekilde ister.

Ne zaman hello **Azure Gezgini** görünümü görüntülenir, kullanım bu adımları toostart izleyin veya Web uygulamanızı durdurun: 

1. Merhaba genişletin **Azure** düğümü.
2. Merhaba genişletin **Web Apps** düğümü. 
3. Web uygulaması sağ hello istenen.
4. Merhaba bağlam menüsü görüntülendiğinde **Başlat**, **durdurmak**, veya **yeniden**. Yalnızca çalışan bir web uygulamasına durdurmak veya şu anda çalışmıyor bir web uygulamasını başlatmak için hello menü seçeneklerine Bağlam duyarlı olduğunu unutmayın.
   
    ![Web uygulamasını Durdur][18]

## <a name="next-steps"></a>Sonraki Adımlar
Java IDE hello Azure araç takımları hakkında daha fazla bilgi için bağlantılar aşağıdaki hello bakın:

* [Eclipse için Azure Araç Seti]
  * [Yükleme hello Eclipse için Azure Araç Seti]
  * [Eclipse Azure'da Hello World Web uygulaması oluşturun]
  * [Yeni hello Eclipse için Azure Araç Seti nedir]
* [Intellij için Azure Araç Seti]
  * [yükleme hello Intellij için Azure Araç Seti]
  * *Intellij (Bu makalede) Azure'da Hello World Web uygulaması oluşturun*
  * [Yeni hello Intellij için Azure Araç Seti nedir]

<a name="see-also"></a>

## <a name="see-also"></a>Ayrıca Bkz.
Azure Java ile kullanma hakkında daha fazla bilgi için bkz: Merhaba [Azure Java Geliştirici Merkezi].

Azure Web uygulamaları oluşturma hakkında ek bilgi için bkz: Merhaba [Web Apps'e genel bakış].

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[Eclipse için Azure Araç Seti]: ../azure-toolkit-for-eclipse.md
[Intellij için Azure Araç Seti]: ../azure-toolkit-for-intellij.md
[Eclipse Azure'da Hello World Web uygulaması oluşturun]: ./app-service-web-eclipse-create-hello-world-web-app.md
[Create a Hello World Web App for Azure in IntelliJ]: ./app-service-web-intellij-create-hello-world-web-app.md
[Yükleme hello Eclipse için Azure Araç Seti]: ../azure-toolkit-for-eclipse-installation.md
[yükleme hello Intellij için Azure Araç Seti]: ../azure-toolkit-for-intellij-installation.md
[Yeni hello Eclipse için Azure Araç Seti nedir]: ../azure-toolkit-for-eclipse-whats-new.md
[Yeni hello Intellij için Azure Araç Seti nedir]: ../azure-toolkit-for-intellij-whats-new.md

[Azure Java Geliştirici Merkezi]: https://azure.microsoft.com/develop/java/
[Web Apps'e genel bakış]: ./app-service-web-overview.md
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/

<!-- IMG List -->

[01]: ./media/app-service-web-intellij-create-hello-world-web-app/01-Web-Page.png
[02]: ./media/app-service-web-intellij-create-hello-world-web-app/02-File-New-Project.png
[03a]: ./media/app-service-web-intellij-create-hello-world-web-app/03-New-Project-Dialog.png
[03b]: ./media/app-service-web-intellij-create-hello-world-web-app/03-New-Project-SDK-Dialog.png
[04]: ./media/app-service-web-intellij-create-hello-world-web-app/04-New-Project-Dialog.png
[05a]: ./media/app-service-web-intellij-create-hello-world-web-app/05-Open-Module-Settings.png
[05b]: ./media/app-service-web-intellij-create-hello-world-web-app/05-Project-Structure-Dialog.png
[05c]: ./media/app-service-web-intellij-create-hello-world-web-app/05-Open-Index-Page.png
[06]: ./media/app-service-web-intellij-create-hello-world-web-app/06-Azure-Publish-Context-Menu.png
[07]: ./media/app-service-web-intellij-create-hello-world-web-app/07-Azure-Log-In-Dialog.png
[08]: ./media/app-service-web-intellij-create-hello-world-web-app/08-Manage-Subscriptions.png
[09]: ./media/app-service-web-intellij-create-hello-world-web-app/09-App-Containers.png
[10]: ./media/app-service-web-intellij-create-hello-world-web-app/10-Add-App-Container.png
[11a]: ./media/app-service-web-intellij-create-hello-world-web-app/11-New-App-Container.png
[11b]: ./media/app-service-web-intellij-create-hello-world-web-app/11-New-App-Container-JDK-Tab.png
[12]: ./media/app-service-web-intellij-create-hello-world-web-app/12-New-Resource-Group.png
[13]: ./media/app-service-web-intellij-create-hello-world-web-app/13-New-App-Service-Plan.png
[14]: ./media/app-service-web-intellij-create-hello-world-web-app/14-New-App-Container.png
[15]: ./media/app-service-web-intellij-create-hello-world-web-app/15-Deploy-To-Azure.png
[16]: ./media/app-service-web-intellij-create-hello-world-web-app/16-Progress-Indicator.png
[17]: ./media/app-service-web-intellij-create-hello-world-web-app/17-Browse-Web-App.png
[18]: ./media/app-service-web-intellij-create-hello-world-web-app/18-Stop-Web-App.png
