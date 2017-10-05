---
title: "Eclipse kullanarak bir temel Azure web uygulaması oluşturma | Microsoft Docs"
description: "Bu öğretici bir Hello World Web uygulaması için Azure oluşturmak için Eclipse için Azure Araç Seti kullanmayı gösterir."
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
ms.openlocfilehash: 683d6828546995a4dc60d8cac0669f356501c723
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-basic-azure-web-app-using-eclipse"></a>Eclipse kullanarak bir temel Azure web uygulaması oluşturma
Bu öğretici oluşturmak ve Azure Web uygulaması olarak temel bir Hello World uygulamayı kullanarak dağıtmak nasıl gösterir [Eclipse için Azure Araç Takımı]. Kolaylık olması için temel bir JSP örneği gösterilir, ancak Azure dağıtım ilgili olduğu kadar benzer adımlar bir Java servlet için uygun olacaktır.

Bu öğreticiyi tamamladıktan sonra bir web tarayıcısında görüntülediğinizde, uygulamanızın aşağıdaki çizime benzer görünür:

![Önizleme Hello, World uygulama][01]

## <a name="prerequisites"></a>Ön koşullar
* Bir Java Geliştirme Seti (JDK), v 1.8 veya üzeri.
* Luna olan Java EE geliştiricileri için Eclipse IDE veya sonraki bir sürümü. Bu adresten yüklenebilir <http://www.eclipse.org/downloads/>.
* Dağıtım bir Java tabanlı web sunucusu veya uygulama sunucusu gibi [Apache Tomcat] veya [Jetty].
* Öğesinden alınan bir Azure aboneliği <https://azure.microsoft.com/free/> veya <http://azure.microsoft.com/pricing/purchase-options/>.
* [Eclipse için Azure Araç Takımı]. Azure araç setini yükleme hakkında daha fazla bilgi için bkz: [Azure araç setini Eclipse için yükleme].

## <a name="to-create-a-hello-world-application"></a>Merhaba Dünya uygulaması oluşturmak için
İlk olarak, bir Java projesi oluşturma ile başlayacağız devre dışı.

1. Eclipse başlatın ve menüsünde tıklatın **dosya**, tıklatın **yeni**ve ardından **dinamik Web projesi**. (Görmüyorsanız **dinamik Web projesi** tıkladıktan sonra kullanılabilir bir proje listelenen **dosya** ve **yeni**, aşağıdakileri yapın: tıklatın **dosya**,'ı tıklatın **yeni**, tıklatın **proje...** , genişletin **Web**, tıklatın **dinamik Web projesi**, tıklatıp **sonraki**.)
2. Bu öğreticinin amaçları doğrultusunda, proje adı **mywebapp şeklindedir**. Ekranınızın aşağıdakine benzer görünür:
   
    ![Yeni bir dinamik Web projesi oluşturma][02]
3. **Son**'a tıklayın.
4. Eclipse'nın Proje Gezgini görünümü içinde genişletmek **mywebapp şeklindedir**. **WebContent**'e sağ tıklayın, **Yeni**'ye tıklayın ve ardından **JSP Dosyası**'na tıklayın.
5. İçinde **yeni JSP dosyası** iletişim kutusunda, dosya adı **index.jsp**, üst klasör olarak tutun **mywebapp şeklindedir/WebContent**ve ardından **sonraki**.
6. İçinde **JSP şablon seç** amacıyla Bu öğretici Seç iletişim kutusu **yeni JSP dosyası (html)**ve ardından **son**.
7. İndex.jsp dosyası Eclipse'te açıldığında, dinamik olarak görüntülenecek metni eklemek **Merhaba Dünya!** `<body>`Hello World! (Merhaba Dünya!) ifadesinin görüntülenmesi için metni ekleyin. Güncelleştirilmiş `<body>` içerik, aşağıdaki örnekte benzer:
   
    `<body><b><% out.println("Hello World!"); %></b></body>` 
8. İndex.jsp kaydedin.

## <a name="to-deploy-your-application-to-an-azure-web-app-container"></a>Bir Azure Web uygulaması kapsayıcısına uygulamanızı dağıtmak için
Bir Java web uygulaması azure'a dağıtabilir miyim birkaç yolu vardır. Bu öğreticide en basit açıklar: uygulamanızı Azure Web uygulaması kapsayıcıya dağıtılacak - hiçbir özel Proje türü ya da ek araçlar gereklidir. Bu yüzden karşıya yüklemek için gerekli kendi JDK ve web kapsayıcısı yazılım sizin için Azure tarafından sağlanacak; ihtiyacınız olan tek şey, Java Web uygulaması. Sonuç olarak, uygulamanız için yayımlama işlemi saniye, dakika sürer.

1. Eclipse'nın Proje Gezgini'nde sağ **mywebapp şeklindedir**.
2. Bağlam menüsünü **Azure**, ardından **Azure Web uygulaması olarak Yayımla...**
   
    ![Olarak Azure Web uygulaması yayımlama][03]
   
    Alternatif olarak, web uygulama projesi Proje Gezgini'nde seçiliyken tıklayabilirsiniz **Yayımla** seçin ve araç çubuğundaki açılır düğmesini **Azure Web uygulaması olarak Yayımla** buradan:
   
    ![Olarak Azure Web uygulaması yayımlama][14]
3. Zaten Eclipse Azure'dan oturum açmış değil, Azure hesabınızda oturum açın istenir:
   
    ![Azure oturum açma iletişim kutusu][04]
   
    Birden çok Azure hesabınız yoksa, oturum açma işlemi sırasında istemleri bazıları aynı olması göründükleri olsa bile birden fazla kez gösterilebilir. Bu gerçekleştiğinde, oturum açma yönergeleri izleyerek devam edin.
4. Azure hesabınızda oturumu başarıyla sonra **Aboneliklerini Yönet** iletişim kutusunda kimlik bilgilerinizle ilişkili Aboneliklerin listesini görüntüler. Birden çok abonelik listelenir ve bunların yalnızca belirli bir alt kümesiyle çalışmak istediğiniz varsa, isteğe bağlı olarak kullanmak istediğiniz olanları işaretini. Aboneliklerinizi seçildiğinde tıklatın **Kapat**.
   
    ![Yönet abonelikleri iletişim kutusu][05]
5. Zaman **Azure Web uygulaması kapsayıcı Dağıt** iletişim kutusu görüntülenirse, daha önce oluşturduğunuz herhangi bir Web uygulaması kapsayıcıdaki görüntülenir; herhangi bir kapsayıcıdaki oluşturmadıysanız listesi boş olur.
   
    ![Dağıt Azure Web uygulaması kapsayıcı iletişim kutusu][06]
6. Bir Azure Web uygulaması kapsayıcısı önce oluşturmadıysanız veya yeni bir kapsayıcı uygulamanıza yayımlamak isterseniz, aşağıdaki adımları kullanın. Aksi takdirde, var olan bir Web uygulaması kapsayıcıyı seçin ve adım 7'ye atlayın.
   
   1. Tıklatın **yeni...**
      
       ![Dağıt Azure Web uygulaması kapsayıcı iletişim kutusu][15]
   2. **Yeni Web uygulaması kapsayıcı** iletişim kutusu görüntülenir:
      
       ![Yeni Web uygulaması kapsayıcı iletişim kutusu][07a]
   3. Girin bir **DNS etiketi** Web uygulama kapsayıcısı için; bu, web uygulamanız için ana bilgisayar URL'si yaprak DNS etiketini Azure'da oluşturacak. (Ad kullanılabilir ve adlandırma gereksinimlerini Azure Web uygulaması için uygun olduğunu unutmayın.)
   4. İçinde **Web kapsayıcısına** açılır menüsünde, uygulamanız için uygun yazılım seçin.
      
       Şu anda, Tomcat 8, Tomcat 7 veya Jetty 9 seçebilirsiniz. Seçilen yazılım yeni bir dağıtımını Azure tarafından sağlanacak ve JDK Oracle tarafından oluşturulan ve Azure tarafından sağlanan 8'in yeni bir dağıtım çalıştırılır.
   5. İçinde **abonelik** açılır menüsünde, bu dağıtım için kullanmak istediğiniz aboneliği seçin.
   6. İçinde **kaynak grubu** açılır menüsünde, istediğiniz Web uygulamanızı ilişkilendirmek kaynak grubunu seçin. (Azure kaynak grupları, örneğin, bunlar birlikte silinebilir böylece ilgili kaynaklar gruplamak izin verir.)
      
       Mevcut kaynak (varsa) grubu ve Atla g aşağıdaki adım seçin veya aşağıdaki yeni bir kaynak grubu oluşturmak üzere şu adımları kullanın:
      
      * Tıklatın **yeni...**
      * **Yeni kaynak grubu** iletişim kutusu görüntülenir:
        
          ![Yeni kaynak grubu iletişim kutusu][08]
      * İçinde **adı** metin kutusuna, yeni kaynak grubunuz için bir ad belirtin.
      * İçinde **bölge** açılır menüsünde, select uygun Azure veri merkezi kaynak grubunuz için konum.
      * İsteğe bağlı: varsayılan olarak, yeni bir Java 8 dağıtımını Azure tarafından otomatik olarak, web app kapsayıcıya, JVM dağıtılır. Ancak, Web uygulamanızı gerektiriyorsa, farklı sürüm ve JVM dağıtımını belirtebilirsiniz. Web uygulamanız için JDK belirtmek için tıklatın **JDK** sekmesini tıklatın ve aşağıdaki seçeneklerden birini seçin:
        
        * **Azure Web uygulamaları hizmeti tarafından sunulan JDK varsayılan dağıtmak**: Bu seçenek Java 8 yeni bir dağıtımını dağıtır.
        * **Bir 3. taraf JDK Azure üzerinde kullanılabilir dağıtmak**: Bu seçenek, Microsoft Azure tarafından sağlanan JDKs listesinden seçim yapmanızı sağlar.
        * **Bu yükleme konumdan kendi JDK dağıtımı**: Bu seçenek, bir ZIP dosyası olarak paketlenir ve genel kullanıma açık indirme konumu ya da erişim elinizde bir Azure depolama hesabı karşıya kendi JDK dağıtım belirtmenize olanak tanır.
          
          ![Yeni Web uygulaması kapsayıcı iletişim kutusu][07b]
   7. **Tamam** düğmesine tıklayın.
   8. **App Service planı** açılır menü, seçtiğiniz kaynak grubuyla ilişkili olan uygulama hizmeti planları listeler. (Uygulama hizmeti planları, Web uygulamanızın, fiyatlandırma katmanı ve işlem örnek boyutu konumu gibi bilgileri belirtin. Tek bir uygulama hizmeti planı ayrı olarak belirli bir Web uygulaması dağıtımından korunan neden olan ve birden çok Web uygulamaları için kullanılabilir.)
      
       Bir var olan App Service (varsa) planı ve Atla h aşağıdaki adım seçin veya yeni bir uygulama hizmeti planı oluşturmak üzere şu adımları aşağıdakileri kullanın:
      
      * Tıklatın **yeni...**
      * **Yeni uygulama hizmeti planı** iletişim kutusu görüntülenir:
        
          ![Yeni uygulama hizmeti planı iletişim kutusu][09]
      * İçinde **adı** metin kutusuna, yeni uygulama hizmeti planınız için bir ad belirtin.
      * İçinde **konumu** açılır menüsünde, select uygun Azure veri merkezi plan için konum.
      * İçinde **fiyatlandırma katmanı** açılır menüsünde, uygun fiyatlandırma planı seçin. Test amacıyla seçebileceğiniz **serbest**.
      * İçinde **örnek boyutu** uygun örneğini boyut plan için aşağı açılan menüsünde seçin. Test amacıyla seçebileceğiniz **küçük**.
   9. Yukarıdaki adımları tamamladıktan sonra yeni Web uygulaması kapsayıcısı iletişim kutusunda aşağıdaki çizimde benzemelidir:
      
       ![Yeni Web uygulaması kapsayıcı iletişim kutusu][10]
   10. Tıklatın **Tamam** yeni Web uygulaması kapsayıcı oluşturma işlemini tamamlamak için.
       
        Web uygulaması kapsayıcılar listesi yenilenmesi birkaç saniye bekleyin ve listesinde yeni oluşturulan web uygulaması kapsayıcınız artık seçili olmalıdır.
7. Şimdi Web uygulamanızı azure'a ilk dağıtımını tamamlamak hazırsınız:
   
    ![Dağıt Azure Web uygulaması kapsayıcı iletişim kutusu][11]
   
    Tıklatın **Tamam** seçili Web uygulaması kapsayıcısı Java uygulamanızı dağıtmak için.
   
    Varsayılan olarak, uygulamanızın uygulama sunucusunun bir alt dizini olarak dağıtılır. Kök uygulaması olarak dağıtılmasını istiyorsanız, denetleme **kök Dağıt** tıklatmadan önce onay kutusunu **Tamam**.
8. Ardından, görmelisiniz **Azure etkinlik günlüğü** Görünümü Web uygulamanızı dağıtım durumunu gösterir.
   
    ![Azure etkinlik günlüğü][12]
   
    Web uygulamanızı Azure'a dağıtma işlemini tamamlamak için yalnızca birkaç saniye sürer. Uygulama hazır gördüğünüzde adlı bir bağlantı **yayımlanan** içinde **durum** sütun. Bağlantıya tıkladığında, dağıtılan Web uygulamanızın giriş sayfasına gideceksiniz.

## <a name="updating-your-web-app"></a>Web uygulamanızı güncelleştirme
Azure Web uygulaması çalıştıran var olan bir güncelleştirme hızlı ve kolay bir işlemdir ve güncelleştirmek için iki seçeneğiniz vardır:

* Varolan bir Java Web uygulaması dağıtımını güncelleştirebilirsiniz.
* Aynı Web uygulama kapsayıcısı için ek bir Java uygulama yayımlayabilirsiniz.

Her iki durumda da işlemi aynıdır ve yalnızca birkaç saniye sürer:

1. Eclipse proje Gezgini'nde, güncelleştirmek veya var olan bir Web uygulaması kapsayıcıyı eklemek istediğiniz Java uygulaması sağ tıklayın.
2. Bağlam menüsü görüntülendiğinde seçin **Azure** ve ardından **Azure Web uygulaması olarak Yayımla...**
3. Zaten daha önce oturum açtıktan sonra var olan Web uygulaması kapsayıcıları listesini görürsünüz. Yayımlama veya Java uygulamanızı yeniden yayımlayın ve istediğiniz bir tanesini seçin **Tamam**.

Daha sonra birkaç saniye **Azure etkinlik günlüğü** görünümü güncelleştirilmiş dağıtımınız olarak göster **yayımlanan** ve güncelleştirilmiş uygulamanız bir web tarayıcısında doğrulayamazsınız olacaktır.

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a>Başlatma, durdurma veya var olan bir web uygulamasının yeniden başlatma
Başlat veya Durdur (içinde dağıtılan tüm Java uygulamaları dahil), mevcut bir Azure Web uygulaması kapsayıcısı için kullanabileceğiniz **Azure Gezgini** görünümü.

Varsa **Azure Gezgini** görünüm zaten açık, ardından tıklayarak açabilirsiniz **penceresi** eclipse'te, ardından menüsünü **görünümü göster**, ardından **diğer...** , ardından **Azure**ve ardından **Azure Gezgini**. Daha önce oturum açmamış olan, bunu yapmanızı ister.

Zaman **Azure Gezgini** görünümü görüntülenir, kullanım başlatmak veya Web uygulamanızı durdurmak için aşağıdaki adımları izleyin: 

1. Genişletme **Azure** düğümü.
2. Genişletme **Web Apps** düğümü. 
3. İstediğiniz Web uygulamasını sağ tıklayın.
4. Bağlam menüsü görüntülendiğinde **Başlat**, **durdurmak**, veya **yeniden**. Yalnızca çalışan bir web uygulamasına durdurmak veya şu anda çalışmıyor bir web uygulamasını başlatmak için menü seçeneklerini Bağlam duyarlı olduğunu unutmayın.
   
    ![Var olan bir Web uygulamasının durdurma][13]

## <a name="next-steps"></a>Sonraki Adımlar
Java IDE’leri için Azure Araç Setleri hakkında daha fazla bilgi için aşağıdaki bağlantılara bakın:

* [Eclipse için Azure Araç Takımı]
  * [Azure araç setini Eclipse için yükleme]
  * *Eclipse (Bu makalede) Azure'da Hello World Web uygulaması oluşturun*
  * [Eclipse için Azure Araç Seti Yenilikleri]
* [IntelliJ için Azure Araç Seti]
  * [IntelliJ için Azure Araç Setini Yükleme]
  * [Intellij Azure'da Hello World Web uygulaması oluşturun]
  * [IntelliJ için Azure Araç Seti Yenilikleri]

Azure’u Java ile kullanma hakkında daha fazla bilgi edinmek için bkz. [Azure Java Geliştirici Merkezi].

Azure Web uygulamaları oluşturma hakkında ek bilgi için bkz: [Web Apps'e genel bakış].

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[Eclipse için Azure Araç Takımı]: ../azure-toolkit-for-eclipse.md
[IntelliJ için Azure Araç Seti]: ../azure-toolkit-for-intellij.md
[Create a Hello World Web App for Azure in Eclipse]: ./app-service-web-eclipse-create-hello-world-web-app.md
[Intellij Azure'da Hello World Web uygulaması oluşturun]: ./app-service-web-intellij-create-hello-world-web-app.md
[Azure araç setini Eclipse için yükleme]: ../azure-toolkit-for-eclipse-installation.md
[IntelliJ için Azure Araç Setini Yükleme]: ../azure-toolkit-for-intellij-installation.md
[Eclipse için Azure Araç Seti Yenilikleri]: ../azure-toolkit-for-eclipse-whats-new.md
[IntelliJ için Azure Araç Seti Yenilikleri]: ../azure-toolkit-for-intellij-whats-new.md

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
