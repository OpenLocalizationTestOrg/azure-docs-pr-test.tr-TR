---
title: "aaaBottle ve Visual Studio için Python araçları 2.2 ile azure'da Azure tablo depolaması"
description: "Merhaba web uygulama tooAzure App Service Web Apps dağıtmak ve nasıl toouse hello Python araçları için Visual Studio toocreate verileri Azure tablo depolama alanında depolar Bottle uygulama öğrenin."
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
ms.openlocfilehash: 25b9eb002b8748483d5b9458b7b5860a958b4bb3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="bottle-and-azure-table-storage-on-azure-with-python-tools-22-for-visual-studio"></a>Bottle ve Visual Studio için Python araçları 2.2 ile azure'da Azure tablo depolaması
Bu öğreticide, kullanacağız [Visual Studio için Python Araçları] toocreate basit bir web uygulamasına hello PTVS örnek şablonlarından birini kullanarak yoklar. Bu öğretici olarak da kullanılabilir bir [video](https://www.youtube.com/watch?v=GJXDGaEPy94).

depoları (bellek içi, Azure Table Storage, MongoDB) farklı türleri arasında kolayca geçebilirsiniz şekilde hello yoklamalar web uygulaması, havuz için bir Özet tanımlar.

Biz nasıl toocreate bir Azure depolama hesabı, tooconfigure hello nasıl web uygulama toouse Azure tablo depolaması ve nasıl öğreneceksiniz toopublish hello web uygulaması çok[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).

Merhaba bkz [Python Geliştirici Merkezi] Bottle kullanarak PTVS ile Azure App Service Web Apps geliştirmeyi kapsayan diğer makaleler için Flask ve Django web altyapılarını MongoDB, Azure Table Storage, MySQL ve SQL Database hizmetleriyle. Bu makale App Service'e odaklanmakla birlikte hello adımlar geliştirirken benzer [Azure Cloud Services].

## <a name="prerequisites"></a>Ön koşullar
* Visual Studio 2015
* [Visual Studio için Python Araçları 2.2]
* [Visual Studio Örnekleri VSIX için Python araçları 2.2]
* [VS 2015 için Azure SDK Araçları]
* [Python 2.7 32 bit] veya [Python 3.4 32 bit]

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> Azure hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git[App Service'i deneyin](https://azure.microsoft.com/try/app-service/), burada hemen bir kısa süreli başlangıç web uygulaması App Service'te oluşturabilirsiniz. Kredi kartı ve taahhüt gerekmez.
> 
> 

## <a name="create-hello-project"></a>Başlangıç projesi oluşturma
Bu bölümde, örnek şablonu kullanarak bir Visual Studio projesi oluşturacağız. Biz sanal ortam oluşturacak ve gerekli paketleri yükleyeceksiniz. Ardından biz hello uygulaması hello varsayılan bellek içi depoya kullanarak yerel olarak çalıştıracaksınız.

1. Visual Studio'da, **Dosya**, **Yeni Proje**’yi seçin.
2. Proje şablonlarını hello hello [Visual Studio Örnekleri VSIX için Python araçları 2.2] altında kullanılabilir **Python**, **örnekleri**. Seçin **yoklamalar Bottle Web projesi** ve Tamam toocreate hello proje'yi tıklatın.
   
     ![Yeni Proje İletişim Kutusu](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleNewProject.png)
3. İstendiğinde tooinstall dış paketler olacaktır. **Sanal bir ortama yükle**’yi seçin.
   
     ![Dış Paketler İletişim Kutusu](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleExternalPackages.png)
4. Seçin **Python 2.7** veya **Python 3.4** hello temel yorumlayıcı olarak.
   
     ![Sanal Ortama Ekle İletişim Kutusu](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonAddVirtualEnv.png)
5. Merhaba uygulaması tuşlarına basarak çalıştığını onaylayın `F5`. Varsayılan olarak, herhangi bir yapılandırma gerektirmeyen bir bellek içi depoya hello uygulama kullanır. Tüm veriler kaybolur hello web sunucusu durdurulduğunda.
6. Tıklatın **örnek yoklamalar Oluştur**, ardından bir yoklamaya tıklayın ve oy verin.
   
     ![Web Tarayıcısı](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleInMemoryBrowser.png)

## <a name="create-an-azure-storage-account"></a>Bir Azure depolama hesabı oluşturma
toouse depolama işlemleri, bir Azure depolama hesabınızın olması gerekir. Aşağıdaki adımları izleyerek bir depolama hesabı oluşturabilirsiniz.

1. Merhaba günlüğüne [Azure Portal](https://portal.azure.com/).
2. Merhaba tıklatın **yeni** hello üst simgesine sol hello Portal ', ardından **veri + depolama** > **depolama hesabı**.  Merhaba tıklatın **oluşturma** düğmesine tıklayın, ardından hello depolama hesabı benzersiz bir ad verin ve yeni bir [kaynak grubu](../azure-resource-manager/resource-group-overview.md) onun için.
   
      ![Hızlı oluştur](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonAzureStorageCreate.png)
   
    Merhaba depolama hesabı oluşturduğunuzda hello **bildirimleri** düğmesi yeşil flash **başarı** ve hello depolama hesabının dikey penceresi açık toohello yeni kaynak ait tooshow grubunu oluşturulur.
3. Merhaba tıklatın **erişim anahtarları** hello depolama hesabı dikey penceresinde parçası. Merhaba hesap adı ve key1 not edin.
   
      ![Anahtarlar](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonAzureStorageKeys.png)
   
    Biz bu bilgileri tooconfigure hello sonraki bölümde projenizde gerekir.

## <a name="configure-hello-project"></a>Merhaba projeyi yapılandırma
Bu bölümde, yeni oluşturduğumuz bizim uygulama toouse hello depolama hesabı yapılandıracağız. Ardından hello uygulama yerel olarak çalıştıracaksınız.

1. Visual Studio'da, Çözüm Gezgini'nde, proje düğümüne sağ tıklayın ve seçin **özellikleri**. Tıklatın hello üzerinde **hata ayıklama** sekmesi.
   
     ![Proje hata ayıklama ayarları](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleAzureTableStorageProjectDebugSettings.png)
2. Merhaba değerlerini hello uygulamada gerekli ortam değişkenleri **Debug sunucu komutunu**, **ortam**.
   
       REPOSITORY_NAME=azuretablestorage
       STORAGE_NAME=<storage account name>
       STORAGE_KEY=<primary access key>
   
   Bu hello ortam değişkenleri ayarlar olduğunda, **hata ayıklamayı Başlat**. İsterseniz hello değişkenleri toobe ne zaman ayarlayın, **hata ayıklama olmadan Başlat**, aynı değerleri kümesi hello **sunucu komutu Çalıştır** de.
   
   Alternatif olarak, Windows Denetim Masası hello kullanarak ortam değişkenlerini tanımlayabilirsiniz. Kaynak kodunda kimlik bilgilerini depolama tooavoid istediğiniz / proje dosyası, daha iyi bir seçenektir. Merhaba yeni ortam değerleri toobe kullanılabilir toohello uygulaması için Visual Studio toorestart gerektiğine dikkat edin.
3. hello Azure Table Storage deposu uygulayan hello kodudur içinde **models/azuretablestorage.py**. Merhaba bkz [belgelerine] hakkında daha fazla bilgi için toouse Python tablo hizmetinden.
4. Merhaba uygulamayla çalıştırmak `F5`. İle oluşturulan yoklamalar **örnek yoklamalar Oluştur** ve oy vermeyle gönderilen hello veri Azure tablo Depolama'da seri.
   
   > [!NOTE]
   > Merhaba Python 2.7 sanal ortamı Visual Studio'da bir özel durum sonu neden olabilir.  Tuşuna `F5` toocontinue hello web projesi yükleniyor.
   > 
   > 
5. Toohello Gözat **hakkında** uygulama hello sayfa tooverify hello kullanarak **Azure Table Storage** deposu.
   
     ![Web Tarayıcısı](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleAzureTableStorageAbout.png)

## <a name="explore-hello-azure-table-storage"></a>Hello Azure Table Storage keşfedin
Bu kolay tooview ve Visual Studio Cloud Explorer kullanarak depolama tabloları düzenleyin. Bu bölümde Sunucu Gezgini tooview hello hello yoklamalar uygulama tabloların içeriğini kullanacağız.

> [!NOTE]
> Bu, kullanılabilir olan yüklü Microsoft Azure Araçları toobe gerektirir hello bir parçası olarak [.NET için Azure SDK].
> 
> 

1. Açık **Cloud Explorer**. Genişletme **depolama hesapları**, depolama hesabınızın sonra **tabloları**.
   
     ![Bulut Gezgini](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorer.png)
2. Merhaba üzerinde çift **yoklamalar** veya **seçenekleri** tablo tooview hello Ekle/Kaldır/Düzenle varlıklar yanı sıra, bir belge penceresinde hello tablosunun içeriğini.
   
     ![Tablo sorgusu sonuçları](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorerTable.png)

## <a name="publish-hello-web-app-tooazure-app-service"></a>Yayımlama Hello web uygulama tooAzure uygulama hizmeti
Hello Azure .NET SDK'sını kolay bir yolu toodeploy web uygulama tooAzure uygulama hizmeti sağlar.

1. İçinde **Çözüm Gezgini**, hello proje düğümüne sağ tıklayın ve seçin **Yayımla**.
   
     ![Web Yayımlama İletişim Kutusu](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonPublishWebSiteDialog.png)
2. **Microsoft Azure Web Apps** ’e tıklayın.
3. Tıklayın **yeni** toocreate yeni bir web uygulaması.
4. Hello aşağıdaki alanları doldurun ve **oluşturma**.
   
   * **Web Uygulaması adı**
   * **App Service planı**
   * **Kaynak grubu**
   * **Bölge**
   * Bırakın **veritabanı sunucusu** çok ayarlamak**veritabanı yok**
5. Diğer tüm varsayılanları kabul edin ve **Yayımla**’ya tıklayın.
6. Web tarayıcınız toohello yayımlanan web uygulamasına otomatik olarak açılır. Sayfa hakkında toohello göz atarsanız, hello kullandığını görürsünüz **bellek içi** deposu, değil hello **Azure Table Storage** deposu.
   
   Merhaba ortam değişkenleri hello Azure App Service'te Web Apps örneğinde ayarlanmamış belirtilen hello varsayılan değerleri kullanan çünkü **ProjectName**.

## <a name="configure-hello-web-apps-instance"></a>Merhaba Web uygulamaları örnek yapılandırma
Bu bölümde, hello Web Apps örneği için ortam değişkenleri yapılandıracağız.

1. İçinde [Azure Portal], tıklayarak hello web uygulamanızın dikey penceresini açmak **Gözat** > **uygulama hizmetleri** >, web uygulaması adı.
2. Web uygulamanızın dikey penceresinde tıklayın **tüm ayarları**, ardından **uygulama ayarları**.
3. Toohello aşağı **uygulama ayarları** bölümünde ve hello değerlerini ayarlayabilirsiniz **deposu\_adı**, **depolama\_adı** ve  **Depolama\_anahtar** hello açıklandığı gibi **yapılandırma hello proje** yukarıdaki bölümde.
   
     ![Uygulama ayarları](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonWebSiteConfigureSettingsTableStorage.png)
4. **Kaydet**'e tıklayın. Merhaba değişiklikleri uygulandı hello bildirimleri aldığınız sonra tıklayın **Gözat** hello Web uygulama ana dikey penceresinden.
5. Hello kullanarak, beklendiği gibi hello web uygulama çalışma görmelisiniz **Azure Table Storage** deposu.
   
   Tebrikler!
   
     ![Web Tarayıcısı](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleAzureBrowser.png)

## <a name="next-steps"></a>Sonraki adımlar
Visual Studio, Bottle ve Azure tablo depolaması için Python araçları hakkında daha fazla bu bağlantılar toolearn izleyin.

* [Visual Studio için Python Araçları Belgeleri]
  * [Web Projeleri]
  * [Bulut Hizmeti Projeleri]
  * [Microsoft Azure’da Uzaktan Hata Ayıklama]
* [Bottle belgeleri]
* [Azure Depolama]
* [Python için Azure SDK]
* [Nasıl tooUse hello Python tablo Depolama hizmetinden]

## <a name="whats-changed"></a>Yapılan değişiklikler
* Web siteleri tooApp hizmet değişikliği Kılavuzu toohello için bkz: [Azure App Service ve mevcut Azure hizmetlerine etkileri](http://go.microsoft.com/fwlink/?LinkId=529714)

<!--Link references-->
[Python Geliştirici Merkezi]: /develop/python/
[Azure Cloud Services]: ../cloud-services/cloud-services-python-ptvs.md
[belgelerine]:../cosmos-db/table-storage-how-to-use-python.md
[Nasıl tooUse hello Python tablo Depolama hizmetinden]:../cosmos-db/table-storage-how-to-use-python.md


<!--External Link references-->
[Azure Portal]: https://portal.azure.com
[.NET için Azure SDK]: http://azure.microsoft.com/downloads/
[Visual Studio için Python Araçları]: http://aka.ms/ptvs
[Visual Studio için Python Araçları 2.2]: http://go.microsoft.com/fwlink/?LinkId=624025
[Visual Studio Örnekleri VSIX için Python araçları 2.2]: http://go.microsoft.com/fwlink/?LinkId=624025
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
