---
title: bir bulut hizmeti aaaHow toomonitor | Microsoft Docs
description: "Nasıl toomonitor bulut hizmetlerini hello Klasik Azure portalı kullanarak öğrenin."
services: cloud-services
documentationcenter: 
author: thraka
manager: timlt
editor: 
ms.assetid: 5c48d2fb-b8ea-420f-80df-7aebe2b66b1b
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/07/2015
ms.author: adegeo
ms.openlocfilehash: ee98c56e0b98b85d75a5c1d796800069c4f06d20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomonitor-cloud-services"></a>TooMonitor Cloud Services nasıl
[!INCLUDE [disclaimer](../../includes/disclaimer.md)]

İzleyeceğiniz `key` hello Klasik Azure portalı, bulut hizmetlerinizde için performans ölçümleri. Merhaba toominimal izleme düzeyini ve her hizmeti rolü için ayrıntılı ayarlayabilirsiniz ve görüntüler izleme hello özelleştirebilirsiniz. Ayrıntılı izleme verilerini dışında hello portalına erişebilmek için bir depolama hesabında depolanır. 

Merhaba Klasik Azure portalı izleme görüntüler yüksek oranda yapılandırılabilir. Merhaba ölçümleri seçebilirsiniz toomonitor hello hello ölçümleri listesinde istediğiniz **İzleyici** sayfası ve seçim yapabileceğiniz hangi ölçümleri tooplot ölçümler grafiklerde hello üzerinde **İzleyici** sayfa ve hello Pano. 

## <a name="concepts"></a>Kavramlar
Varsayılan olarak, en az izleme hello ana bilgisayar işletim sisteminden hello rol örnekleri (sanal makineler) için toplanan performans sayaçlarını kullanarak yeni bir bulut hizmeti için sağlanır. Merhaba en az sınırlı tooCPU yüzdesi, verileri, veri çıkışı, Disk okuma performansı ve Disk yazma üretilen iş ölçümleridir. Ayrıntılı izleme yapılandırarak, ek ölçümler hello sanal makinelerdeki (Rol örnekleri) performans verileri temel alabilir. Merhaba ayrıntılı ölçümler uygulama işlemleri sırasında oluşabilecek sorunları daha yakından analizini sağlar.

Varsayılan olarak performans sayacı verilerini rol örneklerinden örneklenen ve 3 dakika aralıklarla hello rol örneğinden aktarılan. Merhaba ham performans sayacı verilerini ayrıntılı izleme etkinleştirdiğinizde, her rol örneği için ve her rol için rol örnekleri arasında 5 dakika, 1 saat ve 12 saat aralıklarla toplanır. Merhaba verileridir 10 gün sonra temizlenir.

Ayrıntılı izleme, toplanan hello etkinleştirildikten sonra izleme verileri depolama hesabınıza tablolarında depolanır. rolü için izleme ayrıntılı tooenable, toohello depolama hesabı bağlanan bir tanılama bağlantı dizesi yapılandırmanız gerekir. Farklı depolama hesapları için farklı roller kullanabilirsiniz.

Ayrıntılı izleme artar etkinleştirme depolama maliyetleriniz toodata depolama, veri aktarımı ve depolama işlemleri ilgili. İzleme en az bir depolama hesabı gerektirmez. İzleme düzeyi tooverbose hello ayarlasanız bile hello izleme en az düzeyde gösterilen hello ölçümleri hello veri depolama hesabınızdaki depolanmaz.

## <a name="how-to-configure-monitoring-for-cloud-services"></a>Nasıl yapılır: Bulut Hizmetleri için izlemeyi Yapılandır
Aşağıdaki yordamlar tooconfigure ayrıntılı veya en az hello Klasik Azure portalı izleme hello kullanın. 

### <a name="before-you-begin"></a>Başlamadan önce
* Oluşturma bir *Klasik* izleme verilerini depolama hesabı toostore hello. Farklı depolama hesapları için farklı roller kullanabilirsiniz. Daha fazla bilgi için bkz: [nasıl toocreate bir depolama hesabı](../storage/common/storage-create-storage-account.md#create-a-storage-account).
* Azure tanılama bulut hizmeti rollerinizi için etkinleştirin. Bkz: [tanılama bulut Hizmetleri için yapılandırma](cloud-services-dotnet-diagnostics.md).

Merhaba tanılama bağlantı dizesi hello rolü yapılandırmasında mevcut olduğundan emin olun. Azure Tanılama'yı etkinleştirmek ve hello rolü yapılandırmasında bir tanılama bağlantı dizesi içeren kadar ayrıntılı izlemesini etkinleştiremiyor.   

> [!NOTE]
> Azure SDK 2.5 hedefleyen projeler hello proje şablonu hello tanılama bağlantı dizesi otomatik olarak içermiyordu. Bu projeler için toomanually gereksinim duyduğunuz hello tanılama bağlantı dizesi toohello rol yapılandırması ekleyin.
> 
> 

**toomanually tanılama bağlantı dizesi tooRole Yapılandırması Ekle**

1. Visual Studio'da Aç hello bulut hizmeti projesi
2. Hello üzerinde çift **rol** tooopen rol Tasarımcısı hello ve Başlangıç'ı seçin **ayarları** sekmesi
3. Adlı bir ayar için Ara **Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString**. 
4. Bu ayar mevcut değilse, üzerinde hello tıklatın **ayar Ekle** düğmesini tooadd, toohello yapılandırma ve değişiklik hello hello çok yeni ayarlama türü**ConnectionString**
5. Merhaba üzerinde tıklayarak bağlantı dizesini hello için hello değerini ayarla **...**  düğmesi. Bu, bir depolama hesabı tooselect sağlayan bir iletişim kutusunu açar.
   
    ![Visual Studio ayarları](./media/cloud-services-how-to-monitor/CloudServices_Monitor_VisualStudioDiagnosticsConnectionString.png)

### <a name="toochange-hello-monitoring-level-tooverbose-or-minimal"></a>İzleme düzeyi tooverbose toochange hello veya en az
1. Merhaba, [Klasik Azure portalı](https://manage.windowsazure.com/)açın hello **yapılandırma** hello bulut hizmeti dağıtımı için sayfa.
2. İçinde **düzeyi**, tıklatın **ayrıntılı** veya **en az**. 
3. **Kaydet** düğmesine tıklayın.

Ayrıntılı izleme etkinleştirdikten sonra hello Klasik Azure portalı verilerde hello saat içinde izleme hello görmeye başlayacaksınız.

Merhaba ham performans sayacı verileri ve toplanan izleme verilerini hello dağıtım kimliği hello rolleri için nitelenen tablolardaki hello depolama hesabında depolanır. 

## <a name="how-to-receive-alerts-for-cloud-service-metrics"></a>Nasıl yapılır: Bulut hizmeti ölçümleri için uyarılar almak
Bulut hizmetinizde ölçümleri izleme göre uyarıları alabilirsiniz. Merhaba üzerinde **Yönetim Hizmetleri** sayfasında Merhaba Klasik Azure portalı, seçtiğiniz hello ölçüm belirttiğiniz bir değer ulaştığında bir uyarı kuralı tootrigger oluşturabilirsiniz. E-posta hello uyarı tetiklendiğinde gönderilen toohave de seçebilirsiniz. Daha fazla bilgi için bkz: [nasıl yapılır: uyarı bildirimleri alma ve Azure uyarı kurallarını yönet](http://go.microsoft.com/fwlink/?LinkId=309356).

## <a name="how-to-add-metrics-toohello-metrics-table"></a>Nasıl yapılır: ölçümleri toohello ölçümleri tablo ekleme
1. Merhaba, [Klasik Azure portalı](http://manage.windowsazure.com/)açın hello **İzleyici** hello bulut hizmeti için sayfa.
   
    Varsayılan olarak, hello ölçüm tablosunda hello kullanılabilir ölçüler kümesini görüntüler. Merhaba çizim sınırlı toohello Bellek\Kullanılabilir MBayt performans sayacı olan bir bulut hizmeti için varsayılan ayrıntılı ölçümler hello hello rol düzeyinde toplanan verilerle göstermektedir. Kullanım **ölçüm Ekle** tooselect ek toplama ve rol düzeyi ölçümlerini toomonitor hello Klasik Azure portalı.
   
    ![Ayrıntılı görüntüleme](./media/cloud-services-how-to-monitor/CloudServices_DefaultVerboseDisplay.png)
2. tooadd ölçümleri toohello ölçüm tablosunda:
   
   1. Tıklatın **ölçüm Ekle** tooopen **ölçüm Seç**, aşağıda gösterilen.
      
       Merhaba ilk kullanılabilir genişletilmiş tooshow seçenekleri ölçümüdür. Her ölçüm için hello üst seçeneği tüm rolleri için toplanan izleme verilerini görüntüler. Ayrıca, bireysel rolleri için toodisplay verileri seçebilirsiniz.
      
       ![Ölçüm Ekle](./media/cloud-services-how-to-monitor/CloudServices_AddMetrics.png)
   2. tooselect ölçümleri toodisplay
      
      * İzleme seçenekleri hello ölçüm tooexpand hello tarafından aşağı ok Hello'ı tıklatın.
      * Select hello onay kutusu her toodisplay istediğiniz seçeneği izleme.
        
        Merhaba ölçüm tablosunda too50 ölçümleri yukarı görüntüleyebilirsiniz.
        
        > [!TIP]
        > Ayrıntılı izlemede hello ölçümleri listesi ölçümleri düzinelerce içerebilir. toodisplay bir scrollbar hello iletişim kutusunun sağ tarafında hello üzerine getirin. toofilter hello listesi, hello arama simgesine tıklayın ve aşağıda gösterildiği gibi hello arama kutusunda, metin girin.
        > 
        > 
        
        ![Ölçümleri arama ekleyin](./media/cloud-services-how-to-monitor/CloudServices_AddMetrics_Search.png)
3. Ölçümleri seçtikten sonra Tamam'a (onay işareti) tıklayın.
   
    Merhaba seçilen ölçümleri toohello ölçüm tablosunda, aşağıda gösterildiği gibi eklenir.
   
    ![İzleyici ölçümleri](./media/cloud-services-how-to-monitor/CloudServices_Monitor_UpdatedMetrics.png)
4. ve ardından toodelete ölçüm hello ölçümleri tablosundan tıklatın hello ölçüm tooselect **silmek ölçüm**. (Yalnızca gördüğünüz **silmek ölçüm** bir ölçüm seçili olduğunda,.)

### <a name="tooadd-custom-metrics-toohello-metrics-table"></a>tooadd özel ölçümleri toohello ölçümleri tablosu
Merhaba **ayrıntılı** düzeyi izleme, hello portalında izleyebilirsiniz varsayılan ölçümleri listesini sağlar. Ayrıca toothese herhangi bir özel ölçümleri veya uygulamanızın hello portal üzerinden tarafından tanımlanan performans sayaçlarını izleyebilirsiniz.

Merhaba aşağıdaki adımlarda, açık olan varsayılmaktadır **ayrıntılı** düzeyi izleme ve uygulama toocollect ve aktarım özel performans sayaçları yapılandırdınız. 

toodisplay hello özel performans sayaçları tooupdate hello wad denetimi kapsayıcısı yapılandırmasında ihtiyacınız portal hello:

1. Merhaba wad denetimi kapsayıcısı blob tanılama depolama hesabınızı açın. Visual Studio ya da başka bir Depolama Gezgini toodo kullanabileceğiniz bu.
   
    ![Visual Studio Sunucu Gezgini](./media/cloud-services-how-to-monitor/CloudServices_Monitor_VisualStudioBlobExplorer.png)
2. Merhaba düzeni kullanarak hello blob yolu gidin **RoleName/Deploymentıd/RoleInstance** toofind hello yapılandırma rol örneği. 
   
    ![Visual Studio Depolama Gezgini](./media/cloud-services-how-to-monitor/CloudServices_Monitor_VisualStudioStorage.png)
3. Rol örneği Hello yapılandırma dosyasını indirin ve tooinclude güncelleştirme herhangi bir özel performans sayacı. Örneğin toomonitor *Disk Yazma Bayt/sn* hello için *C sürücüsü* altında hello aşağıdakileri ekleyin **PerformanceCounters\Subscriptions** düğümü
   
    ```xml
    <PerformanceCounterConfiguration>
    <CounterSpecifier>\LogicalDisk(C:)\Disk Write Bytes/sec</CounterSpecifier>
    <SampleRateInSeconds>180</SampleRateInSeconds>
    </PerformanceCounterConfiguration>
    ```
4. Merhaba değişiklikleri ve karşıya yükleme hello yapılandırma dosyasını geri toohello hello blob mevcut dosyasında hello aynı konuma üzerine.
5. Hello Azure Klasik portalı yapılandırma tooVerbose modunda Değiştir. Ayrıntılı modda zaten olsaydı tootoggle toominimal ve geri tooverbose sahip olur.
6. Merhaba özel performans sayacı şimdi kullanılabilir hello **ölçüm Ekle** iletişim kutusu. 

## <a name="how-to-customize-hello-metrics-chart"></a>Nasıl yapılır: hello ölçümleri grafiği özelleştirme
1. Merhaba ölçümleri tablosuna too6 ölçümleri tooplot hello ölçümleri grafik seçin. tooselect bir ölçüm hello onay kutusunu sol tarafında tıklatın. tooremove hello ölçümleri grafik, gelen bir ölçüm hello ölçüm tablosunda, onay kutusunu temizleyin.
   
    Merhaba ölçümleri tablosuna ölçümleri seçerken hello ölçümleri toohello ölçümleri grafik eklenir. Dar bir görüntü üzerinde bir **n daha fazla** aşağı açılan liste hello görüntü sığmayan Metrik üstbilgileri içerir.
2. göreli (her ölçüm için yalnızca son değer) ve mutlak değerleri (Y ekseni görüntülenen), görüntüleme arasında tooswitch göreli veya mutlak hello grafik hello üstündeki seçin.
   
    ![Göreli veya mutlak](./media/cloud-services-how-to-monitor/CloudServices_Monitor_RelativeAbsolute.png)
3. toochange hello zaman aralığı hello ölçümleri grafik görüntüler, hello grafik hello üstünde 1 saat, 24 saat veya 7 gün seçin.
   
    ![İzleyici görüntüleme süresi](./media/cloud-services-how-to-monitor/CloudServices_Monitor_DisplayPeriod.png)
   
    Merhaba Pano ölçümleri grafikte hello için çizim ölçümleri farklı yöntemidir. Ölçümleri standart bir dizi kullanılabilir ve ölçümleri eklenir veya hello ölçüm üstbilgi seçerek kaldırılır.

### <a name="toocustomize-hello-metrics-chart-on-hello-dashboard"></a>Merhaba Panoda toocustomize hello ölçümleri grafik
1. Merhaba bulut hizmeti için Hello panosunu açın.
2. Ekleyebilir veya ölçümleri hello grafikten Kaldır:
   
   * tooplot hello grafik üstbilgilerindeki hello ölçümü için yeni bir ölçüm, select hello onay kutusu. Aşağı ok tarafından hello dar bir ekranda tıklatın  ***n* ?? Ölçümleri** tooplot ölçüm hello grafik üstbilgi alanı görüntüleyemiyor.
   * toodelete hello grafikte Temizle hello onay kutusu üstbilgisi tarafından çizilen bir ölçümü.
   
3. Arasında geçiş **göreli** ve **mutlak** görüntüler.
4. 1 saat, 24 saat veya veri toodisplay 7 gün seçin.

## <a name="how-to-access-verbose-monitoring-data-outside-hello-azure-classic-portal"></a>Nasıl yapılır: erişim hello Klasik Azure portalı dışında ayrıntılı izleme verileri
Ayrıntılı izleme verilerini her rol için belirttiğiniz hello depolama hesapları tablolarında depolanır. Her bulut hizmeti dağıtım için altı tablolar hello rolü için oluşturulur. İki tablo her biri için (5 dakika, 1 saat ve 12 saat) oluşturulur. Bu tablolar rol düzeyinde toplamalar depolar; Rol örnekleri için diğer tablo depoları toplamaları hello. 

Merhaba tablo adları biçimini izleyen hello vardır:

```
WAD*deploymentID*PT*aggregation_interval*[R|RI]Table
```

Burada:

* *Deploymentıd* olan hello toohello bulut hizmeti dağıtımı atanan GUID
* *aggregation_interval* 5 M, 1 H veya 12 H =
* rol düzeyinde toplamalar R =
* Rol örnekleri için toplamaları RI =

Örneğin, hello aşağıdaki tablolarda 1 saatlik aralıklarla toplanan ayrıntılı izleme verilerini saklayacağından:

```
WAD8b7c4233802442b494d0cc9eb9d8dd9fPT1HRTable (hourly aggregations for hello role)

WAD8b7c4233802442b494d0cc9eb9d8dd9fPT1HRITable (hourly aggregations for role instances)
```
