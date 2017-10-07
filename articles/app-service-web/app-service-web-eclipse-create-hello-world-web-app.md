---
title: "temel Azure web uygulamasını kullanarak aaaCreate Tutulma | Microsoft Docs"
description: "Bu öğretici nasıl toouse hello Azure araç setini Eclipse toocreate için bir Hello World Web uygulaması için Azure gösterir."
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 20d41e88-9eab-462e-8ee3-89da71e7a33f
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm;asirveda
ms.openlocfilehash: b2f42e0e7a5b98760ec02fab2fc38f9f07b1156b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-basic-azure-web-app-using-eclipse"></a>Eclipse kullanarak bir temel Azure web uygulaması oluşturma
Bu öğreticide gösterilmiştir nasıl toocreate ve hello kullanarak bir Web uygulaması gibi temel bir Hello World uygulama tooAzure dağıtma [Eclipse için Azure Araç Seti]. Kolaylık olması için temel bir JSP örneği gösterilir, ancak Azure dağıtım ilgili olduğu kadar benzer adımlar bir Java servlet için uygun olacaktır.

Bu öğreticiyi tamamladıktan sonra uygulamanızı bir web tarayıcısında görüntülediğinizde çizim aşağıdaki benzer toohello görünür:

![Önizleme Hello, World uygulama][01]

## <a name="prerequisites"></a>Ön koşullar
* Bir Java Geliştirme Seti (JDK), v 1.8 veya üzeri.
* Luna olan Java EE geliştiricileri için Eclipse IDE veya sonraki bir sürümü. Bu adresten yüklenebilir <http://www.eclipse.org/downloads/>.
* Dağıtım bir Java tabanlı web sunucusu veya uygulama sunucusu gibi [Apache Tomcat] veya [Jetty].
* Öğesinden alınan bir Azure aboneliği <https://azure.microsoft.com/free/> veya <http://azure.microsoft.com/pricing/purchase-options/>.
* Merhaba [Eclipse için Azure Araç Seti]. Hello Azure araç setini yükleme hakkında daha fazla bilgi için bkz: [yükleme hello Eclipse için Azure Araç Seti].

## <a name="toocreate-a-hello-world-application"></a>toocreate Merhaba Dünya uygulaması
İlk olarak, bir Java projesi oluşturma ile başlayacağız devre dışı.

1. Eclipse başlatın ve başlangıç menüsünde tıklatın **dosya**, tıklatın **yeni**ve ardından **dinamik Web projesi**. (Görmüyorsanız **dinamik Web projesi** tıkladıktan sonra kullanılabilir bir proje listelenen **dosya** ve **yeni**, ardından aşağıdaki hello: tıklatın **dosya**, tıklatın **yeni**, tıklatın **proje...** , genişletin **Web**, tıklatın **dinamik Web projesi**, tıklatıp **sonraki**.)
2. Bu öğreticinin amaçları doğrultusunda hello proje adı **mywebapp şeklindedir**. Ekranınızın benzer toohello aşağıdaki görünür:
   
    ![Yeni bir dinamik Web projesi oluşturma][02]
3. **Son**'a tıklayın.
4. Eclipse'nın Proje Gezgini görünümü içinde genişletmek **mywebapp şeklindedir**. **WebContent**'e sağ tıklayın, **Yeni**'ye tıklayın ve ardından **JSP Dosyası**'na tıklayın.
5. Merhaba, **yeni JSP dosyası** iletişim kutusu, ad hello dosyası **index.jsp**, hello üst klasörünü olarak **mywebapp şeklindedir/WebContent**ve ardından **sonraki**.
6. Merhaba, **JSP şablon seç** amacıyla Bu öğretici Seç iletişim kutusu **yeni JSP dosyası (html)**ve ardından **son**.
7. İndex.jsp dosyası Eclipse'te açıldığında, metin toodynamically görünümünde eklemek **Merhaba Dünya!** Merhaba varolan içinde `<body>` öğesi. Güncelleştirilmiş `<body>` içeriği aşağıdaki örneğine hello benzer:
   
    `<body><b><% out.println("Hello World!"); %></b></body>` 
8. İndex.jsp kaydedin.

## <a name="toodeploy-your-application-tooan-azure-web-app-container"></a>toodeploy, uygulama tooan Azure Web uygulaması kapsayıcısı
Java web uygulaması tooAzure dağıtabilir miyim birkaç yolu vardır. Bu öğretici hello basit açıklar: uygulamanızı dağıtılan tooan Azure Web uygulaması kapsayıcı olacaktır - hiçbir özel Proje türü ya da ek araçlar gereklidir. Merhaba JDK ve hello web kapsayıcısı yazılım; böylece hiçbir gerek tooupload kendi sizin için Azure tarafından sağlanacak; ihtiyacınız olan tek şey, Java Web uygulaması. Sonuç olarak, uygulamanız için yayımlama işlemi hello saniye, dakika sürer.

1. Eclipse'nın Proje Gezgini'nde sağ **mywebapp şeklindedir**.
2. Merhaba bağlam menüsünden seçin **Azure**, ardından **Azure Web uygulaması olarak Yayımla...**
   
    ![Olarak Azure Web uygulaması yayımlama][03]
   
    Alternatif olarak, web uygulaması projenize hello Proje Gezgini seçiliyken hello tıklatabilirsiniz **Yayımla** açılır liste düğmesi hello araç ve seçim **Azure Web uygulaması olarak Yayımla** buradan:
   
    ![Olarak Azure Web uygulaması yayımlama][14]
3. Zaten Eclipse Azure'dan oturum açmış değil, Azure hesabınızda istendiğinde toosign olacaktır:
   
    ![Azure oturum açma iletişim kutusu][04]
   
    Bazı hello istemleri hello sırasında oturum açmak, birden çok Azure hesabı varsa bunlar toobe görünse bile işlem birden fazla kez gösterilebilir aynı hello. Bu gerçekleştiğinde, hello oturum açma yönergeleri izleyerek devam edin.
4. Azure hesabınızda oturumu başarıyla sonra hello **Aboneliklerini Yönet** iletişim kutusunda kimlik bilgilerinizle ilişkili Aboneliklerin listesini görüntüler. Listelenen birden çok abonelik ve yalnızca belirli bir alt kümesini ile toowork istiyorsanız hello toouse istediğiniz olanları isteğe bağlı olarak işaretini. Aboneliklerinizi seçildiğinde tıklatın **Kapat**.
   
    ![Yönet abonelikleri iletişim kutusu][05]
5. Ne zaman hello **tooAzure Web uygulaması kapsayıcı dağıtma** iletişim kutusu görüntülenirse, daha önce oluşturduğunuz herhangi bir Web uygulaması kapsayıcıdaki görüntülenir; herhangi bir kapsayıcıdaki oluşturmadıysanız hello listesi boş olur.
   
    ![Dağıt tooAzure Web uygulama kapsayıcısı iletişim kutusu][06]
6. Bir Azure Web uygulaması kapsayıcısı önce ya da toopublish isterseniz, uygulama tooa yeni kapsayıcı oluşturmadıysanız, hello aşağıdaki adımları kullanın. Aksi takdirde, var olan bir Web uygulaması kapsayıcıyı seçin ve toostep 7 aşağıdaki atlayın.
   
   1. Tıklatın **yeni...**
      
       ![Dağıt tooAzure Web uygulama kapsayıcısı iletişim kutusu][15]
   2. Merhaba **yeni Web uygulaması kapsayıcı** iletişim kutusu görüntülenir:
      
       ![Yeni Web uygulaması kapsayıcı iletişim kutusu][07a]
   3. Girin bir **DNS etiketi** Web uygulama kapsayıcısı için; bu hello yaprak DNS etiketi hello konak URL'nin, web uygulamanız için Azure içinde oluşturacak. (Bu hello adı kullanılabilir ve tooAzure Web uygulaması adlandırma gereksinimlerini uygun unutmayın.)
   4. Hello içinde **Web kapsayıcısına** açılır menü, uygulamanız için uygun yazılım select hello.
      
       Şu anda, Tomcat 8, Tomcat 7 veya Jetty 9 seçebilirsiniz. Seçili hello yazılım yeni bir dağıtımını Azure tarafından sağlanacak ve JDK Oracle tarafından oluşturulan ve Azure tarafından sağlanan 8'in yeni bir dağıtım çalıştırılır.
   5. Merhaba, **abonelik** açılır menü, bu dağıtım için kullanmak istediğiniz toouse select hello abonelik.
   6. Merhaba, **kaynak grubu** açılır menüsünde, istediğiniz tooassociate Web uygulamanızı seçin hello kaynak grubu. (Örneğin, bunlar birlikte silinebilir böylece, toogroup kaynakları birlikte ilgili azure kaynak gruplarını izin.)
      
       Atla toostep g veya bunlar aşağıdaki kullanım hello toocreate yeni bir kaynak grubu adımlar ve (varsa), var olan bir kaynak grubunu seçebilirsiniz:
      
      * Tıklatın **yeni...**
      * Merhaba **yeni kaynak grubu** iletişim kutusu görüntülenir:
        
          ![Yeni kaynak grubu iletişim kutusu][08]
      * Merhaba hello içinde **adı** metin kutusuna, yeni kaynak grubunuz için bir ad belirtin.
      * Merhaba hello içinde **bölge** açılır menüsünde, select hello uygun Azure veri merkezi kaynak grubunuz için konum.
      * İsteğe bağlı: varsayılan olarak, yeni bir Java 8 dağıtımını Azure tarafından otomatik olarak dağıtılacak tooyour web uygulaması kapsayıcı, JVM olarak. Ancak, Web uygulamanızı gerektiriyorsa, farklı sürüm ve hello JVM dağıtımını belirtebilirsiniz. toospecify hello JDK Web uygulamanız için tıklatın hello **JDK** sekmesini tıklatın ve aşağıdaki seçenekleri şu hello birini seçin:
        
        * **Merhaba varsayılan Azure Web uygulamaları hizmeti tarafından sunulan JDK dağıtımı**: Bu seçenek Java 8 yeni bir dağıtımını dağıtır.
        * **Bir 3. taraf JDK Azure üzerinde kullanılabilir dağıtmak**: Bu seçenek, Microsoft Azure tarafından sağlanan JDKs hello listesinden toochoose sağlar.
        * **Bu yükleme konumdan kendi JDK dağıtımı**: Bu seçenek, toospecify tanır bir ZIP dosyası olarak paketlenmesi gerekir ve bir genel kullanıma açık indirme konumu veya bir Azure depolama hesabı için tooeither karşıya kendi JDK dağıtımı, erişimi vardır.
          
          ![Yeni Web uygulaması kapsayıcı iletişim kutusu][07b]
   7. **Tamam** düğmesine tıklayın.
   8. Merhaba **App Service planı** açılır menü Merhaba, seçili kaynak grubu ile ilişkili hello uygulama hizmeti planları listeler. (Uygulama hizmeti planları, Web uygulamanızın, fiyatlandırma katmanı ve hello işlem örnek boyutu hello hello konum gibi bilgileri belirtin. Tek bir uygulama hizmeti planı ayrı olarak belirli bir Web uygulaması dağıtımından korunan neden olan ve birden çok Web uygulamaları için kullanılabilir.)
      
       (Varsa) var olan bir uygulama hizmeti planı seçebilirsiniz ve toostep h aşağıdaki atlayacak veya bu adımları toocreate yeni bir uygulama hizmeti planı aşağıdaki hello kullanın:
      
      * Tıklatın **yeni...**
      * Merhaba **yeni uygulama hizmeti planı** iletişim kutusu görüntülenir:
        
          ![Yeni uygulama hizmeti planı iletişim kutusu][09]
      * Merhaba hello içinde **adı** metin kutusuna, yeni uygulama hizmeti planınız için bir ad belirtin.
      * Merhaba hello içinde **konumu** açılır menüsünde, select hello uygun Azure veri merkezi hello planı için konum.
      * Merhaba hello içinde **fiyatlandırma katmanı** açılır menüsünde, select hello hello planlama fiyatlandırma uygun. Test amacıyla seçebileceğiniz **serbest**.
      * Merhaba hello içinde **örnek boyutu** açılır menü, hello planı için seçme hello uygun örnek boyutu. Test amacıyla seçebileceğiniz **küçük**.
   9. Tüm hello yukarıdaki adımları tamamladıktan sonra hello yeni Web uygulaması kapsayıcısı iletişim kutusunda aşağıdaki çizimde hello benzemelidir:
      
       ![Yeni Web uygulaması kapsayıcı iletişim kutusu][10]
   10. Tıklatın **Tamam** yeni Web uygulaması kapsayıcısının toocomplete hello oluşturma.
       
        Merhaba Web uygulaması kapsayıcıları toobe hello listesi için birkaç saniye bekleyin yenilenir ve hello listesinde yeni oluşturulan web uygulaması kapsayıcınız artık seçili olmalıdır.
7. Hazır toocomplete hello ilk dağıtımı, Web uygulaması tooAzure sunulmuştur:
   
    ![Dağıt tooAzure Web uygulama kapsayıcısı iletişim kutusu][11]
   
    Tıklatın **Tamam** toodeploy, Java uygulama toohello seçili Web uygulaması kapsayıcı.
   
    Varsayılan olarak, uygulamanızı bir alt dizin hello uygulama sunucusu dağıtılır. Merhaba kök uygulaması dağıtılan toobe istiyorsanız hello denetleyin **tooroot dağıtmak** tıklatmadan önce onay kutusunu **Tamam**.
8. Ardından, hello görmelisiniz **Azure etkinlik günlüğü** hello dağıtım durumu, Web uygulamanızın gösterecektir görünümü.
   
    ![Azure etkinlik günlüğü][12]
   
    Merhaba, Web uygulaması tooAzure dağıtma işlemi, yalnızca birkaç saniye almalıdır toocomplete. Uygulama hazır gördüğünüzde adlı bir bağlantı **yayımlanan** hello içinde **durum** sütun. Merhaba bağlantısını tıklattığınızda sizi tooyour dağıtılmış Web uygulamanızın giriş sayfasına götürür.

## <a name="updating-your-web-app"></a>Web uygulamanızı güncelleştirme
Azure Web uygulaması çalıştıran var olan bir güncelleştirme hızlı ve kolay bir işlemdir ve güncelleştirmek için iki seçeneğiniz vardır:

* Varolan bir Java Web uygulaması dağıtımını hello güncelleştirebilirsiniz.
* Ek bir Java uygulaması toohello yayımlayabilirsiniz aynı Web uygulama kapsayıcısı.

Her iki durumda da hello işlemi aynıdır ve yalnızca birkaç saniye sürer:

1. Merhaba Eclipse proje Gezgini'nde tooupdate istediğiniz ya da Web uygulaması kapsayıcı varolan tooan eklemek Merhaba Java uygulaması sağ tıklayın.
2. Merhaba bağlam menüsü görüntülendiğinde seçin **Azure** ve ardından **Azure Web uygulaması olarak Yayımla...**
3. Zaten daha önce oturum açtıktan sonra var olan Web uygulaması kapsayıcıları listesini görürsünüz. Select toopublish istediğiniz ya da Java uygulama tooand tıklatmanız yeniden yayımlama hello **Tamam**.

Daha sonra birkaç saniye hello **Azure etkinlik günlüğü** görünümü güncelleştirilmiş dağıtımınız olarak göster **yayımlanan** ve mümkün tooverify güncelleştirilmiş uygulamanız bir web tarayıcısında olacaktır.

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a>Başlatma, durdurma veya var olan bir web uygulamasının yeniden başlatma
toostart veya mevcut bir Azure Web uygulaması kapsayıcısı (tüm dağıtılan hello Java uygulamaları içine dahil), durdurmak, hello kullanabilirsiniz **Azure Gezgini** görünümü.

Merhaba, **Azure Gezgini** görünüm zaten açık, ardından tıklayarak açabilirsiniz **penceresi** eclipse'te, ardından menüsünü **görünümü göster**, ardından **diğer...** , ardından **Azure**ve ardından **Azure Gezgini**. Daha önce oturum açmamış olan, bu toodo şekilde ister.

Ne zaman hello **Azure Gezgini** görünümü görüntülenir, kullanım bu adımları toostart izleyin veya Web uygulamanızı durdurun: 

1. Merhaba genişletin **Azure** düğümü.
2. Merhaba genişletin **Web Apps** düğümü. 
3. Web uygulaması sağ hello istenen.
4. Merhaba bağlam menüsü görüntülendiğinde **Başlat**, **durdurmak**, veya **yeniden**. Yalnızca çalışan bir web uygulamasına durdurmak veya şu anda çalışmıyor bir web uygulamasını başlatmak için hello menü seçeneklerine Bağlam duyarlı olduğunu unutmayın.
   
    ![Var olan bir Web uygulamasının durdurma][13]

## <a name="next-steps"></a>Sonraki Adımlar
Java IDE hello Azure araç takımları hakkında daha fazla bilgi için bağlantılar aşağıdaki hello bakın:

* [Eclipse için Azure Araç Seti]
  * [yükleme hello Eclipse için Azure Araç Seti]
  * *Eclipse (Bu makalede) Azure'da Hello World Web uygulaması oluşturun*
  * [Yeni hello Eclipse için Azure Araç Seti nedir]
* [IntelliJ için Azure Araç Seti]
  * [Yükleme hello Intellij için Azure Araç Seti]
  * [Intellij Azure'da Hello World Web uygulaması oluşturun]
  * [Yeni hello Intellij için Azure Araç Seti nedir]

Azure Java ile kullanma hakkında daha fazla bilgi için bkz: Merhaba [Azure Java Geliştirici Merkezi].

Azure Web uygulamaları oluşturma hakkında ek bilgi için bkz: Merhaba [Web Apps'e genel bakış].

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[Eclipse için Azure Araç Seti]: ../azure-toolkit-for-eclipse.md
[IntelliJ için Azure Araç Seti]: ../azure-toolkit-for-intellij.md
[Create a Hello World Web App for Azure in Eclipse]: ./app-service-web-eclipse-create-hello-world-web-app.md
[Intellij Azure'da Hello World Web uygulaması oluşturun]: ./app-service-web-intellij-create-hello-world-web-app.md
[yükleme hello Eclipse için Azure Araç Seti]: ../azure-toolkit-for-eclipse-installation.md
[Yükleme hello Intellij için Azure Araç Seti]: ../azure-toolkit-for-intellij-installation.md
[Yeni hello Eclipse için Azure Araç Seti nedir]: ../azure-toolkit-for-eclipse-whats-new.md
[Yeni hello Intellij için Azure Araç Seti nedir]: ../azure-toolkit-for-intellij-whats-new.md

[Azure Java Geliştirici Merkezi]: https://azure.microsoft.com/develop/java/
[Web Apps'e genel bakış]: ./app-service-web-overview.md
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/

<!-- IMG List -->

[01]: ./media/app-service-web-eclipse-create-hello-world-web-app/01-Web-Page.png
[02]: ./media/app-service-web-eclipse-create-hello-world-web-app/02-Dynamic-Web-Project.png
[03]: ./media/app-service-web-eclipse-create-hello-world-web-app/03-Context-Menu.png
[04]: ./media/app-service-web-eclipse-create-hello-world-web-app/04-Log-In-Dialog.png
[05]: ./media/app-service-web-eclipse-create-hello-world-web-app/05-Manage-Subscriptions-Dialog.png
[06]: ./media/app-service-web-eclipse-create-hello-world-web-app/06-Deploy-To-Azure-Web-Container.png
[07a]: ./media/app-service-web-eclipse-create-hello-world-web-app/07a-New-Web-App-Container-Dialog.png
[07b]: ./media/app-service-web-eclipse-create-hello-world-web-app/07b-New-Web-App-Container-Dialog.png
[08]: ./media/app-service-web-eclipse-create-hello-world-web-app/08-New-Resource-Group-Dialog.png
[09]: ./media/app-service-web-eclipse-create-hello-world-web-app/09-New-Service-Plan-Dialog.png
[10]: ./media/app-service-web-eclipse-create-hello-world-web-app/10-Completed-Web-App-Container-Dialog.png
[11]: ./media/app-service-web-eclipse-create-hello-world-web-app/11-Completed-Deploy-Dialog.png
[12]: ./media/app-service-web-eclipse-create-hello-world-web-app/12-Activity-Log-View.png
[13]: ./media/app-service-web-eclipse-create-hello-world-web-app/13-Azure-Explorer-Web-App.png
[14]: ./media/app-service-web-eclipse-create-hello-world-web-app/14-publishDropdownButton.png
[15]: ./media/app-service-web-eclipse-create-hello-world-web-app/15-New-Azure-Web-Container.png
