---
title: "Java'da Azure Search ile çalışmaya aaaGet | Microsoft Docs"
description: "Nasıl toobuild barındırılan bir bulut uygulama programlama diliniz olarak Java kullanarak Azure üzerinde arayın."
services: search
documentationcenter: 
author: EvanBoyle
manager: pablocas
editor: v-lincan
ms.assetid: 8b4df3c9-3ae5-4e3a-b4bb-74b516a91c8e
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.date: 07/14/2016
ms.author: evboyle
ms.openlocfilehash: 5476a2103f3b60fe6ec78ff3d3fdba9fcff55c37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-search-in-java"></a>Java'da Azure Search kullanmaya başlama
> [!div class="op_single_selector"]
> * [Portal](search-get-started-portal.md)
> * [.NET](search-howto-dotnet-sdk.md)
> 
> 

Nasıl toobuild özel bir Java arama arama deneyimi için Azure Search kullanan uygulamayı öğrenin. Bu öğretici hello kullanır [Azure Search Hizmeti REST API'si](https://msdn.microsoft.com/library/dn798935.aspx) tooconstruct hello nesneleri ve bu alıştırmada kullanılan işlemleri.

toorun hello için kaydolabilirsiniz bir Azure Search hizmeti bu örnek olmalıdır [Azure Portal](https://portal.azure.com). Bkz: [hello portalda Azure Search hizmeti oluşturma](search-create-service-portal.md) adım adım yönergeler için.

Biz yazılım toobuild aşağıdaki hello kullanılan ve bu örnek test edin:

* [Java EE Geliştiricileri için Eclipse IDE](https://eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunar). Toodownload hello EE sürümünü emin olun. Hello doğrulama adımlardan biri, yalnızca bu sürümde bulunan bir özelliği gerektirir.
* [JDK 8u40](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [Apache Tomcat 8.0](http://tomcat.apache.org/download-80.cgi)

## <a name="about-hello-data"></a>Merhaba veri hakkında
Bu örnek uygulama hello verileri kullanan [Birleşik Devletler Jeoloji Hizmetleri (USGS)](http://geonames.usgs.gov/domestic/download_data.htm), filtrelenmiş hello Rhode Island eyaleti tooreduce hello veri kümesi boyutu. Bu veri toobuild akışlar, Göller ve zirveler gibi jeolojik özelliklerin yanı sıra hastaneler ve okullar gibi önemli binaları döndüren bir arama uygulaması kullanacağız.

Bu uygulamada hello **SearchServlet.java** programı oluşturup yükleri hello dizini kullanarak bir [dizin oluşturucu](https://msdn.microsoft.com/library/azure/dn798918.aspx) hello alma yapısı, filtrelenmiş USGS veri kümesini ortak bir Azure SQL veritabanından. Önceden tanımlanmış kimlik bilgileri ve bağlantı bilgileri toohello çevrimiçi veri kaynağı hello program kodu içinde sağlanır. Veri erişimi açısından ek yapılandırma gerekli değildir.

> [!NOTE]
> Bu veri kümesi toostay hello 10.000 belge limiti hello ücretsiz fiyatlandırma katmanı altında üzerinde bir filtre uygulanmış. Merhaba standart katmanı kullanırsanız bu limit uygulanmaz ve bu kodu toouse büyük bir veri kümesini değiştirebilirsiniz. Her fiyatlandırma katmanının kapasitesi hakkında ayrıntılı bilgi için bkz: [Limitler ve kısıtlamalar](search-limits-quotas-capacity.md).
> 
> 

## <a name="about-hello-program-files"></a>Merhaba program dosyaları hakkında
Merhaba aşağıdaki listede ilgili toothis örnek hello dosyaları açıklanmaktadır.

* Search.jsp: hello kullanıcı arabirimi sağlar
* SearchServlet.java: yöntemler (benzer tooa denetleyicisi MVC) sağlar
* SearchServiceClient.java: HTTP isteklerini işler
* SearchServiceHelper.java: Statik yöntemler sağlayan bir yardımcı sınıfı
* Document.Java: hello veri modeli sağlar
* Config.Properties: hello Search Hizmeti URL'sini ve api anahtarını ayarlar
* Pom.xml: Maven bağımlılığı

<a id="sub-2"></a>

## <a name="find-hello-service-name-and-api-key-of-your-azure-search-service"></a>Merhaba hizmet adı ve Azure Search hizmetinizin api anahtarını bulma
Azure Search tüm REST API çağrıları hello hizmet URL'sini ve api anahtarı sağlamanızı gerektirir. 

1. İçinde toohello oturum [Azure Portal](https://portal.azure.com).
2. Merhaba atlama çubuğunda, **Search Hizmeti** aboneliğiniz için sağlanan tüm hello Azure arama hizmetleri toolist.
3. Toouse istediğiniz hello hizmeti seçin.
4. Merhaba hizmet panosunda yanı sıra hello yönetici anahtarlarına erişim için anahtar simgesine hello önemli bilgiler için kutucuklar görürsünüz.
   
      ![][3]
5. Merhaba hizmet URL'sini ve bir yönetici anahtarını kopyalayın. Toohello eklediğinizde, bunları daha sonra gerekecektir **config.properties** dosya.

## <a name="download-hello-sample-files"></a>Merhaba örnek dosyalarını indirme
1. Çok Git[AzureSearchJavaDemo](https://github.com/AzureSearch/AzureSearchJavaIndexerDemo) github'da.
2. Tıklatın **ZIP'i indir**hello .zip dosyası toodisk kaydedin ve ardından içerdiği tüm hello dosyaları ayıklayın. Ayıklamayı göz önünde bulundurun hello dosyalarının, Java Çalışma toomake daha kolay toofind hello proje daha sonra.
3. Merhaba örnek dosyaları salt okunurdur. Klasör özelliklerini ve Temizle hello salt okunur özniteliğini sağ tıklatın.

Sonraki tüm dosya değişiklikleri ve çalıştırma deyimleri bu klasördeki dosyalara uygulanır.  

## <a name="import-project"></a>Projeyi içeri aktarma
1. Eclipse'te, **File (Dosya)** > **Import (İçeri Aktar)** > **General (Genel)** > **Existing Projects into Workspace (Var olan Projeleri Çalışma Alanına)** seçeneğini belirleyin.
   
    ![][4]
2. İçinde **Select kök dizini**, örnek dosyaları içeren toohello klasörüne göz atın. Merhaba proje klasörünü içeren hello klasörü seçin. Merhaba proje hello görünmelidir **projeleri** seçili öğe olarak listesi.
   
    ![][12]
3. **Son**'a tıklayın.
4. Kullanım **Proje Gezgini** tooview ve düzenleme hello dosyaları. Zaten açık değilse, tıklatın **penceresi** > **görünümü göster** > **Proje Gezgini** veya hello kısayol tooopen kullanın.

## <a name="configure-hello-service-url-and-api-key"></a>Merhaba hizmet URL'si ve api anahtarını yapılandırın
1. İçinde **Proje Gezgini**, çift **config.properties** hello sunucu adını ve api anahtarını içeren tooedit hello yapılandırma ayarları.
2. Burada bulunan hello hizmet URL'sini ve api anahtarını hello daha önce bu makalede toohello adımları başvurun [Azure Portal](https://portal.azure.com), tooget hello değerleri şimdi girdiğiniz içine **config.properties**.
3. İçinde **config.properties**, "Api anahtarı" Merhaba hizmetinizin api anahtarı ile değiştirin. Ardından, hizmet adı (Merhaba URL http://servicename.search.windows.net hello ilk bileşeni) "hizmet adı" hello yerine geçer aynı dosya.
   
    ![][5]

## <a name="configure-hello-project-build-and-runtime-environments"></a>Merhaba proje, derleme ve çalışma zamanı ortamları yapılandırma
1. Eclipse'te, proje Gezgini'nde hello projesine sağ tıklayın > **özellikleri** > **proje modelleri**.
2. **Dynamic Web Module (Dinamik Web Modülü)** öğesini, **Java**'yı ve **JavaScript**'i seçin.
   
    ![][6]
3. **Apply (Uygula)** düğmesine tıklayın.
4. **Window (Pencere)** > **Preferences (Tercihler)** > **Server (Sunucu)** > **Runtime Environments (Çalışma Zamanı Ortamları)** > **Add... (Ekle...)** öğesini seçin.
5. Apache genişletin ve daha önce yüklediğiniz hello Apache Tomcat sunucusunu hello sürümünü seçin. Sistemimizde sürüm 8 yüklüdür.
   
    ![][7]
6. Merhaba sonraki sayfada hello Tomcat yükleme dizinini belirtin. Windows bilgisayarda, bu büyük olasılıkla C:\Program Files\Apache Software Foundation\Tomcat *sürüm* olacaktır.
7. **Finish (Son)** düğmesine tıklayın.
8. **Window (Pencere)** > **Preferences (Tercihler)** > **Java** > **Installed JREs (Yüklü JRE'ler)** > **Add (Ekle)** seçeneğini belirleyin.
9. **Add JRE (JRE Ekle)** bölümünde **Standard VM (Standart VM)** öğesini seçin.
10. **İleri**’ye tıklayın.
11. JRE Tanımı'nda, JRE giriş alanında **Directory (Dizin)** seçeneğine tıklayın.
12. Çok gidin**Program Files** > **Java** ve hello daha önce yüklediğiniz JDK seçin. Bu önemli tooselect hello JDK hello JRE gösterir.
13. Yüklü Jre'ler içinde hello seçin **JDK**. Ayarlarınız aşağıdaki ekran görüntüsüne benzer toohello görünmelidir.
    
    ![][9]
14. İsteğe bağlı olarak, seçin **penceresi** > **Web tarayıcısı** > **Internet Explorer** tooopen Merhaba uygulaması bir dış tarayıcı penceresinde. Dış tarayıcı kullanmanız daha iyi bir Web uygulaması deneyimi sağlar.
    
    ![][8]

Merhaba yapılandırma görevlerini tamamladınız. Ardından, yapı ve Merhaba projeyi çalıştırın.

## <a name="build-hello-project"></a>Merhaba projeyi derleme
1. Proje Gezgini'nde hello proje adına sağ tıklayın ve seçin **Çalıştır** > **Maven build...**  tooconfigure hello projesi.
   
    ![][10]
2. Edit Configuration (Yapılandırmayı Düzenle) alanında Targets (Hedefler) için "clean install" ("temiz yükleme") yazın ve ardından **Run (Çalıştır)** düğmesine tıklayın.

Durum iletileri çıktı toohello konsol penceresi açılır. Yapı Başarısı hatasız yerleşik belirten hello proje görmeniz gerekir.

## <a name="run-hello-app"></a>Merhaba uygulamayı çalıştırma
Bu son adımda, bir yerel sunucu çalışma zamanı ortamında hello uygulama çalışacaktır.

Eclipse'te henüz bir sunucu çalışma zamanı ortamı belirtmediyseniz öncelikle toodo gerekir.

1. Proje Gezgini'nde **WebContent**'i genişletin.
2. **Search.jsp** > **Run As (Farklı Çalıştır)** > **Run on Server (Sunucuda Çalıştır)** öğesine sağ tıklayın. Merhaba Apache Tomcat sunucusunu seçin ve ardından **çalıştırmak**.

> [!TIP]
> Varsayılan olmayan çalışma toostore projenizi kullandıysanız, toomodify gerekir **yapılandırma Çalıştır** toopoint toohello proje konumu tooavoid sunucu başlangıç hatasını. Proje Gezgini'nde **Search.jsp** > **Run As (Farklı Çalıştır)** > **Run Configurations (Yapılandırmaları Çalıştır)** öğesine sağ tıklayın. Merhaba Apache Tomcat sunucusunu seçin. **Arguments (Bağımsız Değişkenler)** seçeneğine tıklayın. Tıklatın **çalışma** veya **dosya sistemi** Merhaba projeyi içeren tooset hello klasör.
> 
> 

Merhaba uygulamayı çalıştırdığınızda, koşulları girmeniz için bir arama kutusu sağlayan bir tarayıcı penceresi görmeniz gerekir.

Seçeneğine tıklamadan önce yaklaşık bir dakika bekleyin **arama** toogive hello hizmeti zaman toocreate ve yük başlangıç dizini. HTTP 404 hatası alırsanız yeniden denemeden önce biraz daha uzun toowait yeterlidir.

## <a name="search-on-usgs-data"></a>USGS verilerinde arama
Merhaba USGS veri kümesini ilgili toohello Rhode Island eyaleti kayıtları içerir. Tıklatırsanız **arama** bir boş arama kutusunda hello varsayılan olduğu hello ilk 50 girişi alırsınız.

Bir arama terimi girerek hello arama motoru bir şey toogo üzerinde verecektir. Bölgesel bir ad girmeyi deneyin. "Roger Williams", Rhode Island hello ilk İdarecisi oluştu. Çok sayıda parka, binaya ve okula onun adı verildi.

![][11]

Ayrıca, bu terimlerden herhangi birini de deneyebilirsiniz:

* Pawtucket
* Pembroke
* kaz + şapka

## <a name="next-steps"></a>Sonraki adımlar
Bu Java ve USGS veri kümesini hello hello ilk Azure Search öğreticisidir. Zaman içinde biz özel çözümlerinizde toouse isteyebilirsiniz ek arama özellikleri Bu öğretici toodemonstrate genişletmeniz.

Bazı arka plan Azure Search'te zaten varsa, bu örneği dayanak olarak daha fazla deneyim için hello kullanabilirsiniz [arama sayfası](search-pagination-page-layout.md), veya uygulama [modellenmiş bir gezinmede](search-faceted-navigation.md). Ayrıca, numaralar ekleyerek ve böylece kullanıcılar hello sonuçları belgeleri toplu işleme hello arama sonuçları sayfasını artırabilir.

Yeni tooAzure arama? Diğer öğreticiler toodevelop bir neler yapabileceğinizi anlamak çalışırken öneririz. Ziyaret bizim [belge sayfasının](https://azure.microsoft.com/documentation/services/search/) toofind daha fazla kaynak. Merhaba bağlantılar da görüntüleyebilirsiniz bizim [Video ve öğretici listemiz](search-video-demo-tutorial-list.md) tooaccess daha fazla bilgi.

<!--Image references-->
[1]: ./media/search-get-started-java/create-search-portal-1.PNG
[2]: ./media/search-get-started-java/create-search-portal-21.PNG
[3]: ./media/search-get-started-java/create-search-portal-31.PNG
[4]: ./media/search-get-started-java/AzSearch-Java-Import1.PNG
[5]: ./media/search-get-started-java/AzSearch-Java-config1.PNG
[6]: ./media/search-get-started-java/AzSearch-Java-ProjectFacets1.PNG
[7]: ./media/search-get-started-java/AzSearch-Java-runtime1.PNG
[8]: ./media/search-get-started-java/AzSearch-Java-Browser1.PNG
[9]: ./media/search-get-started-java/AzSearch-Java-JREPref1.PNG
[10]: ./media/search-get-started-java/AzSearch-Java-BuildProject1.PNG
[11]: ./media/search-get-started-java/rogerwilliamsschool1.PNG
[12]: ./media/search-get-started-java/AzSearch-Java-SelectProject.png
