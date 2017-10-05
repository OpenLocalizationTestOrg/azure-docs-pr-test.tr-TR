---
title: "Intellij içinde bir temel Azure web uygulaması oluşturma | Microsoft Docs"
description: "Bu öğretici bir Hello World Web uygulaması Azure için oluşturmak üzere Intellij için Azure Araç Seti kullanmayı gösterir."
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
ms.openlocfilehash: 20b2c3d86f5bde9302647f345aa99b030d78613a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-basic-azure-web-app-in-intellij"></a>Intellij içinde bir temel Azure web uygulaması oluşturma
Bu öğretici oluşturmak ve Azure Web uygulaması olarak temel bir Hello World uygulamayı kullanarak dağıtmak nasıl gösterir [Intellij için Azure Araç Seti]. Kolaylık olması için temel bir JSP örneği gösterilir, ancak Azure dağıtım ilgili olduğu kadar benzer adımlar bir Java servlet için uygun olacaktır.

Bu öğreticiyi tamamladıktan sonra bir web tarayıcısında görüntülediğinizde, uygulamanızın aşağıdaki çizime benzer görünür:

![Örnek bir Web sayfası][01]

## <a name="prerequisites"></a>Ön koşullar
* Bir Java Geliştirme Seti (JDK), v 1.8 veya üzeri.
* Intellij Idea Ultimate Edition. Bu adresten yüklenebilir <https://www.jetbrains.com/idea/download/index.html>.
* Dağıtım bir Java tabanlı web sunucusu veya uygulama sunucusu gibi [Apache Tomcat] veya [Jetty].
* Öğesinden alınan bir Azure aboneliği <https://azure.microsoft.com/free/> veya <http://azure.microsoft.com/pricing/purchase-options/>.
* [Intellij için Azure Araç Seti]. Azure araç setini yükleme hakkında daha fazla bilgi için bkz: [Intellij için Azure araç setini yükleme].

## <a name="to-create-a-hello-world-application"></a>Merhaba Dünya uygulaması oluşturmak için
İlk olarak, bir Java projesi oluşturma ile başlayacağız devre dışı.

1. Intellij başlatır ve **dosya** menüsünde, ardından **yeni**ve ardından **proje**.
   
    ![Dosya yeni proje][02]
2. Yeni Proje iletişim kutusunda seçin **Java**, ardından **Web uygulaması**ve ardından **yeni** proje SDK eklemek için.
   
    ![Yeni Proje İletişim Kutusu][03a]
   
3. Seçin giriş dizinini JDK iletişim kutusu, JDK yüklendiği klasörü ve ardından seçin **Tamam**. Tıklatın **sonraki** devam etmek için yeni proje iletişim kutusunda.
   
    ![JDK giriş dizini belirtin][03b]
4. Bu öğreticinin amaçları doğrultusunda, proje adı **Java-Web-App-üzerinde-Azure**ve ardından **son**.
   
    ![Yeni Proje İletişim Kutusu][04]
5. Intellij'ın Proje Gezgini görünümü içinde genişletmek **Java-Web-App-üzerinde-Azure**, ardından **web**, çift tıklayın ve ardından **index.jsp**.
   
    ![Açık dizin sayfası][05c]
6. İndex.jsp dosyası içinde Intellij açıldığında, dinamik olarak görüntülenecek metni eklemek **Merhaba Dünya!** `<body>`Hello World! (Merhaba Dünya!) ifadesinin görüntülenmesi için metni ekleyin. Güncelleştirilmiş `<body>` içerik, aşağıdaki örnekte benzer:
   
    `<body><b><% out.println("Hello World!"); %></b></body>` 
7. İndex.jsp kaydedin.

## <a name="to-deploy-your-application-to-an-azure-web-app-container"></a>Bir Azure Web uygulaması kapsayıcısına uygulamanızı dağıtmak için
Bir Java web uygulaması azure'a dağıtabilir miyim birkaç yolu vardır. Bu öğreticide en basit açıklar: uygulamanızı Azure Web uygulaması kapsayıcıya dağıtılacak - hiçbir özel Proje türü ya da ek araçlar gereklidir. Bu yüzden karşıya yüklemek için gerekli kendi JDK ve web kapsayıcısı yazılım sizin için Azure tarafından sağlanacak; ihtiyacınız olan tek şey, Java Web uygulaması. Sonuç olarak, uygulamanız için yayımlama işlemi saniye, dakika sürer.

Uygulamanızı yayınlamadan önce ilk modülü ayarlarını yapılandırmanız gerekir. Bunu yapmak için aşağıdaki adımları kullanın:

1. Intellij'ın Proje Gezgini'nde sağ **Java-Web-App-üzerinde-Azure** projesi. Bağlam menüsü görüntülendiğinde **açık modülü ayarları**.

    ![Modül Ayarları'nı açın][05a]
2. Proje Yapısı iletişim kutusu görüntülendiğinde:

   a. Tıklatın **yapıları** listesinde **proje ayarları**.
   b. Yapı adını değiştirmek **adı** boşluk veya özel karakterler içermiyor kutusuna; adı Tekdüzen Kaynak Tanımlayıcısı (URI) kullanılacağından bu gereklidir.
   c. Değişiklik **türü** için **Web uygulaması: Arşiv**.
   d. Tıklatın **Tamam** proje yapısını iletişim kutusunu kapatın.

    ![Modül Ayarları'nı açın][05b]

Modül ayarlarınızı yapılandırdığınızda, aşağıdaki adımları kullanarak uygulamanızı Azure'a yayımlayabilirsiniz:

1. Intellij'ın Proje Gezgini'nde sağ **Java-Web-App-üzerinde-Azure** projesi. Bağlam menüsü görüntülendiğinde seçin **Azure**ve ardından **Azure Web uygulaması olarak Yayımla...**
   
    ![Azure yayımlama bağlam menüsü][06]
2. Zaten Intellij Azure'dan oturum açmış değil, Azure hesabınızda oturum açın istenir. (Birden çok Azure hesabınız yoksa, bunlar aynı olması görünse bile oturum açma işlemi sırasında istemleri bazıları birden fazla kez gösterilebilir. Bu gerçekleştiğinde, oturum açma yönergelerini izlemeye devam edin.)
   
    ![Azure oturum açma iletişim kutusu][07]
3. Azure hesabınızda oturumu başarıyla sonra **Aboneliklerini Yönet** iletişim kutusunda kimlik bilgilerinizle ilişkili Aboneliklerin listesini görüntüler. (Var olan ve birden çok abonelik listelenen yalnızca belirli bir alt kümesini bunları çalışmak istediğiniz, isteğe bağlı olarak kullanmak istemediğiniz abonelikleri kutusunun işaretini.) Aboneliklerinizi seçildiğinde tıklatın **Kapat**.
   
    ![Aboneliklerini Yönetme][08]
4. Zaman **Azure Web uygulaması kapsayıcı Dağıt** iletişim kutusu görüntülenirse, daha önce oluşturduğunuz herhangi bir Web uygulaması kapsayıcıdaki görüntülenir; herhangi bir kapsayıcıdaki oluşturmadıysanız listesi boş olur.
   
    ![Uygulama kapsayıcıları][09]
5. Bir Azure Web uygulaması kapsayıcısı önce oluşturmadıysanız veya yeni bir kapsayıcı uygulamanıza yayımlamak isterseniz, aşağıdaki adımları kullanın. Aksi takdirde, var olan bir Web uygulaması kapsayıcı seçin ve adım 6 atlayın.
   
   1. ' I tıklatın**+**
      
       ![Uygulama kapsayıcısı Ekle][10]
   2. **Yeni Web uygulaması kapsayıcı** iletişim kutusu görüntülenir, sonraki birkaç adımlar için kullanılır.
      
       ![Yeni uygulama kapsayıcısı][11a]
   3. Girin bir **DNS etiketi** Web uygulama kapsayıcısı için; bu, web uygulamanız için ana bilgisayar URL'si yaprak DNS etiketini Azure'da oluşturacak. Ad kullanılabilir ve adlandırma gereksinimlerini Azure Web uygulaması için uygun olduğunu unutmayın.
   4. İçinde **Web kapsayıcısına** açılır menüsünde, uygulamanız için uygun yazılım seçin.
      
       Şu anda, Tomcat 8, Tomcat 7 veya Jetty 9 seçebilirsiniz. Seçilen yazılım yeni bir dağıtımını Azure tarafından sağlanacak ve JDK Oracle tarafından oluşturulan ve Azure tarafından sağlanan 8'in yeni bir dağıtım çalıştırılır.
   5. İçinde **abonelik** açılır menüsünde, bu dağıtım için kullanmak istediğiniz aboneliği seçin.
   6. İçinde **kaynak grubu** açılır menüsünde, istediğiniz Web uygulamanızı ilişkilendirmek kaynak grubunu seçin. (Azure kaynak grupları, örneğin, bunlar birlikte silinebilir böylece ilgili kaynaklar gruplamak izin verir.)
      
       Mevcut kaynak (varsa) grubu ve Atla g aşağıdaki adım seçin veya yeni bir kaynak grubu oluşturmak için aşağıdaki adımları kullanın:
      
      * Seçin  **&lt; &lt; yeni kaynak grubu oluştur &gt; &gt;**  içinde **kaynak grubu** açılır menü.
      * **Yeni kaynak grubu** iletişim kutusu görüntülenir:
        
          ![Yeni kaynak grubu][12]
      * İçinde **adı** metin kutusuna, yeni kaynak grubunuz için bir ad belirtin.
      * İçinde **bölge** açılır menüsünde, select uygun Azure veri merkezi kaynak grubunuz için konum.
      * **Tamam** düğmesine tıklayın.
   7. **App Service planı** açılır menü, seçtiğiniz kaynak grubuyla ilişkili olan uygulama hizmeti planları listeler. (Konum, Web uygulamanızın fiyatlandırma katmanı ve işlem örnek boyutu gibi bilgileri belirtir bir uygulama hizmeti planı. Tek bir uygulama hizmeti planı ayrı olarak belirli bir Web uygulaması dağıtımından korunan neden olan ve birden çok Web uygulamaları için kullanılabilir.)
      
       Bir var olan App Service (varsa) planı ve Atla h aşağıdaki adım seçin veya yeni bir uygulama hizmeti planı oluşturmak için aşağıdaki adımları kullanın:
      
      * Seçin  **&lt; &lt; yeni uygulama hizmeti planı oluştur &gt; &gt;**  içinde **App Service planı** açılır menü.
      * **Yeni uygulama hizmeti planı** iletişim kutusu görüntülenir:
        
          ![Yeni uygulama hizmeti planı][13]
      * İçinde **adı** metin kutusuna, yeni uygulama hizmeti planınız için bir ad belirtin.
      * İçinde **konumu** açılır menüsünde, select uygun Azure veri merkezi plan için konum.
      * İçinde **fiyatlandırma katmanı** açılır menüsünde, uygun fiyatlandırma planı seçin. Test amacıyla seçebileceğiniz **serbest**.
      * İçinde **örnek boyutu** uygun örneğini boyut plan için aşağı açılan menüsünde seçin. Test amacıyla seçebileceğiniz **küçük**.
      * **Tamam** düğmesine tıklayın.
   8. (İsteğe bağlı) Varsayılan olarak, Java 8 yeni bir dağıtımını otomatik, JVM Azure tarafından web uygulaması kapsayıcıya dağıtılır. Ancak, farklı sürüm ve JVM dağıtımını seçebilirsiniz. Bunu yapmak için aşağıdaki adımları kullanın:
      
      * Tıklatın **JDK** sekmesinde **yeni Web uygulaması kapsayıcı** iletişim kutusu.
      * Aşağıdaki seçeneklerden birini seçebilirsiniz:
        
        * Varsayılan Azure tarafından sunulan JDK dağıtma
        * Bir 3. taraf JDK Azure üzerinde kullanılabilir olan ek JDKs aşağı açılan listesinden dağıtma
        * ZIP dosyası olarak ve ya da paketlenmesi gereken özel bir JDK dağıtımı Azure depolama hesabınızdaki veya genel olarak kullanılabilir
        
        ![Yeni uygulama kapsayıcı JDK sekmesi][11b]
   9. Yukarıdaki adımları tamamladıktan sonra yeni Web uygulaması kapsayıcısı iletişim kutusunda aşağıdaki çizimde benzemelidir:
      
       ![Yeni uygulama kapsayıcısı][14]
   10. Tıklatın **Tamam** yeni Web uygulaması kapsayıcı oluşturma işlemini tamamlamak için.
       
        Web uygulaması kapsayıcılar listesi yenilenmesi birkaç saniye bekleyin ve listesinde yeni oluşturulan web uygulaması kapsayıcınız artık seçili olmalıdır.
6. Şimdi Web uygulamanızı azure'a ilk dağıtımını tamamlamak hazır olursunuz; tıklatın **Tamam** seçili Web uygulaması kapsayıcısı Java uygulamanızı dağıtmak için. Varsayılan olarak, uygulamanızın uygulama sunucusunun bir alt dizini olarak dağıtılır. Kök uygulaması olarak dağıtılmasını istiyorsanız, denetleme **kök Dağıt** tıklatmadan önce onay kutusunu **Tamam**.
   
    ![Azure'a dağıtma][15]
7. Ardından, görmelisiniz **Azure etkinlik günlüğü** Görünümü Web uygulamanızı dağıtım durumunu gösterir.
   
    ![İlerleme göstergesi][16]
   
    Web uygulamanızı Azure'a dağıtma işlemini tamamlamak için yalnızca birkaç saniye sürer. Uygulama hazır gördüğünüzde adlı bir bağlantı **yayımlanan** içinde **durum** sütun. Bağlantıya tıkladığında, dağıtılan Web uygulamanızın giriş sayfasına gideceksiniz ya da web uygulamanıza göz atmak için aşağıdaki bölümdeki adımları kullanabilirsiniz.

## <a name="browsing-to-your-web-app-on-azure"></a>Azure üzerinde Web uygulamanıza gözatma
Azure üzerinde Web uygulamanıza göz atmak için kullanabileceğiniz **Azure Gezgini** görünümü.

Varsa **Azure Gezgini** görünüm zaten açık, ardından tıklayarak açabilirsiniz **Görünüm** Intellij, menüde ardından **aracı Windows**ve ardından  **Hizmet Explorer**. Daha önce oturum açmamış olan, bunu yapmanızı ister.

Zaman **Azure Gezgini** görünümü görüntülenir, kullanma, Web uygulamanızın gözatmak için şu adımları izleyin: 

1. Genişletme **Azure** düğümü.
2. Genişletme **Web Apps** düğümü. 
3. İstediğiniz Web uygulamasını sağ tıklayın.
4. Bağlam menüsü görüntülendiğinde **tarayıcıda aç**.
   
    ![Web uygulaması Gözat][17]

## <a name="updating-your-web-app"></a>Web uygulamanızı güncelleştirme
Azure Web uygulaması çalıştıran var olan bir güncelleştirme hızlı ve kolay bir işlemdir ve güncelleştirmek için iki seçeneğiniz vardır:

* Varolan bir Java Web uygulaması dağıtımını güncelleştirebilirsiniz.
* Aynı Web uygulama kapsayıcısı için ek bir Java uygulama yayımlayabilirsiniz.

Her iki durumda da işlemi aynıdır ve yalnızca birkaç saniye sürer:

1. Intellij proje Gezgini'nde, güncelleştirmek veya var olan bir Web uygulaması kapsayıcıyı eklemek istediğiniz Java uygulaması sağ tıklayın.
2. Bağlam menüsü görüntülendiğinde seçin **Azure** ve ardından **Azure Web uygulaması olarak Yayımla...**
3. Zaten daha önce oturum açtıktan sonra var olan Web uygulaması kapsayıcıları listesini görürsünüz. Yayımlama veya Java uygulamanızı yeniden yayımlayın ve istediğiniz bir tanesini seçin **Tamam**.

Daha sonra birkaç saniye **Azure etkinlik günlüğü** görünümü güncelleştirilmiş dağıtımınız olarak göster **yayımlanan** ve güncelleştirilmiş uygulamanız bir web tarayıcısında doğrulayamazsınız olacaktır.

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a>Başlatma, durdurma veya var olan bir web uygulamasının yeniden başlatma
Başlat veya Durdur (içinde dağıtılan tüm Java uygulamaları dahil), mevcut bir Azure Web uygulaması kapsayıcısı için kullanabileceğiniz **Azure Gezgini** görünümü.

Varsa **Azure Gezgini** görünüm zaten açık, ardından tıklayarak açabilirsiniz **Görünüm** Intellij, menüde ardından **aracı Windows**ve ardından  **Hizmet Explorer**. Daha önce oturum açmamış olan, bunu yapmanızı ister.

Zaman **Azure Gezgini** görünümü görüntülenir, kullanım başlatmak veya Web uygulamanızı durdurmak için aşağıdaki adımları izleyin: 

1. Genişletme **Azure** düğümü.
2. Genişletme **Web Apps** düğümü. 
3. İstediğiniz Web uygulamasını sağ tıklayın.
4. Bağlam menüsü görüntülendiğinde **Başlat**, **durdurmak**, veya **yeniden**. Yalnızca çalışan bir web uygulamasına durdurmak veya şu anda çalışmıyor bir web uygulamasını başlatmak için menü seçeneklerini Bağlam duyarlı olduğunu unutmayın.
   
    ![Web uygulamasını Durdur][18]

## <a name="next-steps"></a>Sonraki Adımlar
Java IDE’leri için Azure Araç Setleri hakkında daha fazla bilgi için aşağıdaki bağlantılara bakın:

* [Eclipse için Azure Araç Seti]
  * [Eclipse için Azure Araç Setini Yükleme]
  * [Eclipse Azure'da Hello World Web uygulaması oluşturun]
  * [Eclipse için Azure Araç Seti Yenilikleri]
* [Intellij için Azure Araç Seti]
  * [Intellij için Azure araç setini yükleme]
  * *Intellij (Bu makalede) Azure'da Hello World Web uygulaması oluşturun*
  * [IntelliJ için Azure Araç Seti Yenilikleri]

<a name="see-also"></a>

## <a name="see-also"></a>Ayrıca Bkz.
Azure’u Java ile kullanma hakkında daha fazla bilgi edinmek için bkz. [Azure Java Geliştirici Merkezi].

Azure Web uygulamaları oluşturma hakkında ek bilgi için bkz: [Web Apps'e genel bakış].

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[Eclipse için Azure Araç Seti]: ../azure-toolkit-for-eclipse.md
[Intellij için Azure Araç Seti]: ../azure-toolkit-for-intellij.md
[Eclipse Azure'da Hello World Web uygulaması oluşturun]: ./app-service-web-eclipse-create-hello-world-web-app.md
[Create a Hello World Web App for Azure in IntelliJ]: ./app-service-web-intellij-create-hello-world-web-app.md
[Eclipse için Azure Araç Setini Yükleme]: ../azure-toolkit-for-eclipse-installation.md
[Intellij için Azure araç setini yükleme]: ../azure-toolkit-for-intellij-installation.md
[Eclipse için Azure Araç Seti Yenilikleri]: ../azure-toolkit-for-eclipse-whats-new.md
[IntelliJ için Azure Araç Seti Yenilikleri]: ../azure-toolkit-for-intellij-whats-new.md

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
