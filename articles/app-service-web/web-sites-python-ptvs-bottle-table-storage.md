---
title: "Bottle ve Visual Studio için Python araçları 2.2 ile azure'da Azure tablo depolaması"
description: "Verileri Azure tablo depolama alanında depolar Bottle uygulaması oluşturmak için Visual Studio için Python araçlarını kullanmayı öğrenin ve Azure App Service Web Apps için web uygulaması dağıtma."
services: app-service\web
documentationcenter: python
author: huguesv
manager: erikre
editor: 
ms.assetid: f075124b-db79-4e51-b394-09187dd6c634
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/07/2016
ms.author: huvalo
ms.openlocfilehash: fb25f03607ac6e9af46b47f54e830e0283dd1b0a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="bottle-and-azure-table-storage-on-azure-with-python-tools-22-for-visual-studio"></a>Bottle ve Visual Studio için Python araçları 2.2 ile azure'da Azure tablo depolaması
Bu öğreticide, kullanacağız [Visual Studio için Python Araçları] yoklamalar web uygulaması PTVS örnek şablonlarından birini kullanarak basit bir oluşturmak için. Bu öğretici olarak da kullanılabilir bir [video](https://www.youtube.com/watch?v=GJXDGaEPy94).

Depoları (bellek içi, Azure Table Storage, MongoDB) farklı türleri arasında kolayca geçebilirsiniz şekilde yoklamalar web uygulaması, havuz için bir Özet tanımlar.

Size bir Azure depolama hesabının nasıl oluşturulacağını, Azure Table Storage kullanmak için web uygulamasını yapılandırma ve web uygulaması'na yayımlamak nasıl öğreneceksiniz [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).

Bkz: [Python Geliştirici Merkezi] Bottle kullanarak PTVS ile Azure App Service Web Apps geliştirmeyi kapsayan diğer makaleler için Flask ve Django web altyapılarını MongoDB, Azure Table Storage, MySQL ve SQL Database hizmetleriyle. Bu makale App Service’e odaklanmakla birlikte, [Azure Cloud Services]’i geliştirirken adımlar benzerdir.

## <a name="prerequisites"></a>Ön koşullar
* Visual Studio 2015
* [Visual Studio için Python Araçları 2.2]
* [Visual Studio Örnekleri VSIX için Python Tools 2.2]
* [VS 2015 için Azure SDK Araçları]
* [Python 2.7 32 bit] veya [Python 3.4 32 bit]

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> Azure hesabı için kaydolmadan önce Azure App Service’i kullanmaya başlamak isterseniz, App Service’te hemen kısa süreli bir başlangıç web uygulaması oluşturabileceğiniz [App Service’i Deneyin](https://azure.microsoft.com/try/app-service/) sayfasına gidin. Kredi kartı ve taahhüt gerekmez.
> 
> 

## <a name="create-the-project"></a>Proje oluşturma
Bu bölümde, örnek şablonu kullanarak bir Visual Studio projesi oluşturacağız. Biz sanal ortam oluşturacak ve gerekli paketleri yükleyeceksiniz. Ardından biz varsayılan bellek içi depoya kullanarak yerel olarak uygulaması çalıştıracaksınız.

1. Visual Studio'da, **Dosya**, **Yeni Proje**’yi seçin.
2. [Visual Studio Örnekleri VSIX için Python Tools 2.2] proje şablonlarını **Python**, **Örnekler** altında bulabilirsiniz. Seçin **yoklamalar Bottle Web projesi** ve projeyi oluşturmak için Tamam'ı tıklatın.
   
     ![Yeni Proje İletişim Kutusu](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleNewProject.png)
3. Dış paketleri yüklemeniz istenir. **Sanal bir ortama yükle**’yi seçin.
   
     ![Dış Paketler İletişim Kutusu](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleExternalPackages.png)
4. Temel yorumlayıcı olarak **Python 2.7** veya **Python 3.4**’ü seçin.
   
     ![Sanal Ortama Ekle İletişim Kutusu](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonAddVirtualEnv.png)
5. `F5` tuşuna basarak uygulamanın çalıştığını doğrulayın. Varsayılan olarak, uygulama herhangi bir yapılandırma gerektirmeyen bir bellek içi depoya kullanır. Tüm veriler kaybolur web sunucusu durdurulduğunda.
6. Tıklatın **örnek yoklamalar Oluştur**, ardından bir yoklamaya tıklayın ve oy verin.
   
     ![Web Tarayıcısı](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleInMemoryBrowser.png)

## <a name="create-an-azure-storage-account"></a>Bir Azure depolama hesabı oluşturma
Depolama işlemlerini kullanmak için bir Azure depolama hesabınızın olması gerekir. Aşağıdaki adımları izleyerek bir depolama hesabı oluşturabilirsiniz.

1. İçine oturum [Azure Portal](https://portal.azure.com/).
2. Tıklatın **yeni** üst simgesine portalın sol, ardından **veri + depolama** > **depolama hesabı**.  Tıklatın **oluşturma** düğmesine tıklayın, ardından depolama hesabı benzersiz bir ad verin ve yeni bir [kaynak grubu](../azure-resource-manager/resource-group-overview.md) onun için.
   
      ![Hızlı oluştur](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonAzureStorageCreate.png)
   
    Depolama hesabı oluşturduğunuzda **bildirimleri** düğmesi yeşil flash **başarı** ve depolama hesabı dikey penceresinde, oluşturduğunuz yeni kaynak grubuna ait olduğunu göstermek için açık.
3. Tıklatın **erişim anahtarları** depolama hesabı dikey penceresinde parçası. Hesap adı ve key1 not edin.
   
      ![Anahtarlar](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonAzureStorageKeys.png)
   
    Sonraki bölümde projenizi yapılandırmak için bu bilgileri ihtiyacımız.

## <a name="configure-the-project"></a>Projeyi Yapılandırma
Bu bölümde, yeni oluşturduğumuz depolama hesabı kullanmak üzere uygulamamız yapılandıracağız. Sonra uygulamayı yerel olarak çalıştıracaksınız.

1. Visual Studio'da, Çözüm Gezgini'nde, proje düğümüne sağ tıklayın ve seçin **özellikleri**. Tıklayın **hata ayıklama** sekmesi.
   
     ![Proje hata ayıklama ayarları](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleAzureTableStorageProjectDebugSettings.png)
2. Uygulama tarafından gerekli ortam değişkenlerinin değerlerini ayarlamak **Debug sunucu komutunu**, **ortam**.
   
       REPOSITORY_NAME=azuretablestorage
       STORAGE_NAME=<storage account name>
       STORAGE_KEY=<primary access key>
   
   Bu ortam değişkenleri ayarlar olduğunda, **hata ayıklamayı Başlat**. Ne zaman ayarlanacak değişkenleri istiyorsanız, **hata ayıklama olmadan Başlat**, altında aynı değerlere ayarlamak **sunucu komutu Çalıştır** de.
   
   Alternatif olarak, Windows Denetim Masası'nı kullanarak ortam değişkenlerini tanımlayabilirsiniz. Proje dosyası kaynak kodunda kimlik bilgilerini depolama önlemek istiyorsanız, daha iyi bir seçenektir. Uygulama için kullanılabilir olması için Visual Studio yeni ortam değerleri için yeniden başlatmanız gerekecektir unutmayın.
3. Azure Table Storage depo uygulayan kod **models/azuretablestorage.py**. Bkz: [belgelerine] Python tablo hizmetinden kullanma hakkında daha fazla bilgi için.
4. Uygulamayı `F5` ile çalıştırın. İle oluşturulan yoklamalar **örnek yoklamalar Oluştur** ve oy vermeyle gönderilen veriler Azure tablo Depolama'da seri hale getirilir.
   
   > [!NOTE]
   > Python 2.7 sanal ortamı Visual Studio'da bir özel durum sonu neden olabilir.  Tuşuna `F5` web projesi yüklemeye devam etmek için.
   > 
   > 
5. Gözat **hakkında** uygulama kullandığını doğrulamak için sayfa **Azure Table Storage** deposu.
   
     ![Web Tarayıcısı](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleAzureTableStorageAbout.png)

## <a name="explore-the-azure-table-storage"></a>Azure Table Storage keşfedin
Visual Studio Cloud Explorer kullanarak depolama tabloları görüntüleyip kolaydır. Bu bölümde yoklamalar uygulama tabloların içeriğini görüntülemek için Sunucu Gezgini kullanacağız.

> [!NOTE]
> Bu Microsoft Azure yüklenmek üzere olarak kullanılabilir olan araçları gerektirir parçası [.NET için Azure SDK].
> 
> 

1. Açık **Cloud Explorer**. Genişletme **depolama hesapları**, depolama hesabınızın sonra **tabloları**.
   
     ![Bulut Gezgini](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorer.png)
2. Çift **yoklamalar** veya **seçimler** bir belge penceresi, aynı zamanda Ekle/Kaldır/Düzenle varlıklar tablosunun içeriğini görüntülemek için tablo.
   
     ![Tablo sorgusu sonuçları](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorerTable.png)

## <a name="publish-the-web-app-to-azure-app-service"></a>Web uygulamasını Azure App Service’te yayımlama
Azure .NET SDK’sı web uygulamanızı Azure App Service’te dağıtmanız için kolay bir yol sağlar.

1. **Çözüm Gezgini**’nde, proje düğümüne sağ tıklayın ve **Yayımla**’yı seçin.
   
     ![Web Yayımlama İletişim Kutusu](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonPublishWebSiteDialog.png)
2. **Microsoft Azure Web Apps** ’e tıklayın.
3. Yeni bir web uygulaması oluşturmak için **Yeni**’ye tıklayın.
4. Aşağıdaki alanları doldurun ve **oluşturma**.
   
   * **Web Uygulaması adı**
   * **App Service planı**
   * **Kaynak grubu**
   * **Bölge**
   * **Veritabanı sunucusu**nu **Veritabanı yok** olarak bırakın.
5. Diğer tüm varsayılanları kabul edin ve **Yayımla**’ya tıklayın.
6. Web tarayıcınız yayımlanan web uygulamasına otomatik olarak açılır. Üzere göz atarsanız sayfası hakkında bunu kullandığını görürsünüz **bellek içi** deposunu değil **Azure Table Storage** deposu.
   
   Ortam değişkenleri Azure App Service'te Web Apps örneğinde ayarlanmamış belirtilen varsayılan değerleri kullanan çünkü **ProjectName**.

## <a name="configure-the-web-apps-instance"></a>Web uygulamaları örnek yapılandırma
Bu bölümde, Web uygulamaları örneği için ortam değişkenleri yapılandıracağız.

1. İçinde [Azure Portal], web uygulamanızın dikey tıklayarak açın **Gözat** > **uygulama hizmetleri** >, web uygulaması adı.
2. Web uygulamanızın dikey penceresinde tıklayın **tüm ayarları**, ardından **uygulama ayarları**.
3. Ekranı aşağı kaydırarak **uygulama ayarları** bölümünde ve değerlerini ayarlayın **deposu\_adı**, **depolama\_adı** ve **depolama \_Anahtar** açıklandığı gibi **projeyi yapılandırma** yukarıdaki bölümde.
   
     ![Uygulama ayarları](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonWebSiteConfigureSettingsTableStorage.png)
4. **Kaydet**'e tıklayın. Değişiklikleri uygulandı bildirimleri aldığınız sonra tıklayın **Gözat** Web uygulama ana dikey penceresinden.
5. Web uygulaması kullanarak, beklendiği gibi çalıştığını görmelisiniz **Azure Table Storage** deposu.
   
   Tebrikler!
   
     ![Web Tarayıcısı](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleAzureBrowser.png)

## <a name="next-steps"></a>Sonraki adımlar
Visual Studio, Bottle ve Azure tablo depolaması için Python araçları hakkında daha fazla bilgi için aşağıdaki bağlantıları izleyin.

* [Visual Studio için Python Araçları Belgeleri]
  * [Web Projeleri]
  * [Bulut Hizmeti Projeleri]
  * [Microsoft Azure’da Uzaktan Hata Ayıklama]
* [Bottle belgeleri]
* [Azure Depolama]
* [Python için Azure SDK]
* [Python'dan Table depolama hizmetini kullanma]

## <a name="whats-changed"></a>Yapılan değişiklikler
* Web Sitelerinden App Service’e kadar değiştirme kılavuzu için bkz. [Azure App Service ve Mevcut Azure Hizmetlerine Etkileri](http://go.microsoft.com/fwlink/?LinkId=529714)

<!--Link references-->
[Python Geliştirici Merkezi]: /develop/python/
[Azure Cloud Services]: ../cloud-services/cloud-services-python-ptvs.md
[belgelerine]:../cosmos-db/table-storage-how-to-use-python.md
[Python'dan Table depolama hizmetini kullanma]:../cosmos-db/table-storage-how-to-use-python.md


<!--External Link references-->
[Azure Portal]: https://portal.azure.com
[.NET için Azure SDK]: http://azure.microsoft.com/downloads/
[Visual Studio için Python Araçları]: http://aka.ms/ptvs
[Visual Studio için Python Araçları 2.2]: http://go.microsoft.com/fwlink/?LinkId=624025
[Visual Studio Örnekleri VSIX için Python Tools 2.2]: http://go.microsoft.com/fwlink/?LinkId=624025
[VS 2015 için Azure SDK Araçları]: http://go.microsoft.com/fwlink/?LinkId=518003
[Python 2.7 32 bit]: http://go.microsoft.com/fwlink/?LinkId=517190
[Python 3.4 32 bit]: http://go.microsoft.com/fwlink/?LinkId=517191
[Visual Studio için Python Araçları Belgeleri]: http://aka.ms/ptvsdocs
[Bottle belgeleri]: http://bottlepy.org/docs/dev/index.html
[Microsoft Azure’da Uzaktan Hata Ayıklama]: http://go.microsoft.com/fwlink/?LinkId=624026
[Web Projeleri]: http://go.microsoft.com/fwlink/?LinkId=624027
[Bulut Hizmeti Projeleri]: http://go.microsoft.com/fwlink/?LinkId=624028
[Azure Depolama]: http://azure.microsoft.com/documentation/services/storage/
[Python için Azure SDK]: https://github.com/Azure/azure-sdk-for-python
