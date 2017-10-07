---
title: "bir bulut hizmeti aaaTesting hello performansını | Microsoft Docs"
description: "Merhaba Visual Studio profil oluşturucu kullanılarak bir bulut hizmeti Hello performansını test etme"
services: visual-studio-online
documentationcenter: n/a
author: kraigb
manager: ghogen
editor: 
ms.assetid: 7a5501aa-f92c-457c-af9b-92ea50914e24
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 98bd775e6ffcf948e737c5ec26399c81f4770fe3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="testing-hello-performance-of-a-cloud-service"></a>Bir bulut hizmeti Hello performansını test etme
## <a name="overview"></a>Genel Bakış
Aşağıdaki şekilde hello bir bulut hizmeti hello performansını test edebilirsiniz:

* İstekleri ve bağlantıları ve hello hizmet Müşteri açısından nasıl gerçekleştireceğini Göster tooreview site İstatistikler hakkında Azure tanılama toocollect bilgileri kullanın. kullanmaya tooget bkz [tanılama Azure Cloud Services ve sanal makineler için yapılandırma](http://go.microsoft.com/fwlink/p/?LinkId=623009).
* Merhaba Visual Studio profil oluşturucu tooget hello hizmeti nasıl çalışacağını hello hesaplama yönlerini ayrıntılı analizini kullanın. Bu konuda açıklandığı gibi bir hizmet Azure'da çalışan hello profil oluşturucu toomeasure performans kullanabilirsiniz. Toouse hello profil oluşturucu toomeasure performans hizmet olarak bir işlem öykünücüsü yerel olarak nasıl çalıştığı hakkında daha fazla bilgi için bkz: [test hello performansını bir Azure bulut hizmeti yerel olarak hello işlem öykünücüsü kullanarak hello Visual Studio profil oluşturucu içinde ](http://go.microsoft.com/fwlink/p/?LinkId=262845).

## <a name="choosing-a-performance-testing-method"></a>Bir performans testi yöntemi seçme
### <a name="use-azure-diagnostics-toocollect"></a>Azure tanılama toocollect kullanın:
* Web sayfaları veya istekler ve bağlantılar gibi Hizmetleri istatistikleri.
* Roller, rol ne sıklıkta yeniden gibi istatistikleri.
* Genel hello zamanın yüzde olarak atık toplayıcı alır hello veya bellek hello gibi bellek kullanımı hakkında bilgi çalışan rolü ayarlayın.

### <a name="use-hello-visual-studio-profiler-to"></a>Merhaba Visual Studio profil oluşturucu için kullanın:
* Hangi işlevleri hello çoğu zaman belirler.
* Her bir pkı'ya yoğun programının parçası tamamlanma süresini ölçün.
* Bir hizmet iki sürümü için ayrıntılı performans raporları karşılaştırın.
* Bellek ayırma tek tek bellek ayırmaları hello düzeyini'den daha ayrıntılı analiz edin.
* Birden çok iş parçacıklı kodda eşzamanlılık sorunları çözümleyin.

Hello profil oluşturucu kullandığınızda, bir bulut hizmeti yerel olarak veya Azure içinde çalıştığında verileri toplayabilir.

### <a name="collect-profiling-data-locally-to"></a>Profil oluşturma verileri yerel olarak Topla:
* Gerçekçi benzetilmiş yük gerektirmeyen belirli çalışan rolü yürütülmesi hello gibi bir bulut hizmeti parçası Hello performansını test etme.
* Bir bulut hizmeti Hello performansını denetimli koşullarda yalıtım test.
* Bir bulut hizmetinin, önce hello performansını test etme tooAzure dağıtın.
* Bir bulut hizmeti Hello performansını özel olarak, rahatsız edici hello var olan dağıtımlar test edin.
* Merhaba hizmet Hello performansını test etmek için Azure'da çalışan ücretlerinin yansıtılmasını olmadan.

### <a name="collect-profiling-data-in-azure-to"></a>Azure için profil oluşturma veri toplama:
* Bir bulut hizmeti benzetimli veya gerçek bir yük altında Hello performansını test etme.
* Bu konuda daha sonra açıklandığı gibi profil oluşturma verilerini toplamanın hello izleme yöntemini kullanın.
* Hello hello hizmetinin hello performansını test hello hizmet üretimde çalıştığında olarak aynı ortamı.

Normal yük tootest bulut Hizmetler genellikle benzetimini veya stres koşulları.

## <a name="profiling-a-cloud-service-in-azure"></a>Azure bulut hizmetinde profil oluşturma
Visual Studio bulut hizmetinizden yayımladığınızda, hello hizmet profilini ve istediğiniz bilgileri hello bu verin ayarları profil hello belirtin. Her bir rol örneği için bir profil oluşturma oturumu başlatıldı. Toopublish hizmetinizi Visual Studio'dan nasıl görürüm hakkında daha fazla bilgi için [tooan Azure bulut hizmeti Visual Studio'da yayımlama](https://msdn.microsoft.com/library/azure/ee460772.aspx).

Visual Studio'da performans profili oluşturma hakkında daha fazla toounderstand bkz [Başlangıç Kılavuzu tooPerformance profil oluşturma](https://msdn.microsoft.com/library/azure/ms182372.aspx) ve [profil oluşturma araçları kullanarak uygulama performansını analiz etme](https://msdn.microsoft.com/library/azure/z9z62c29.aspx).

> [!NOTE]
> IntelliTrace veya Bulut hizmetiniz yayımladığınızda, profil etkinleştirebilirsiniz. Her ikisi de etkinleştiremezsiniz.
> 
> 

### <a name="profiler-collection-methods"></a>Profil Oluşturucu koleksiyon yöntemleri
Farklı koleksiyon yöntemleri performans sorunları hakkında temel profil oluşturma için kullanabilirsiniz:

* **CPU örnekleme** -bu yöntem ilk CPU kullanım sorunları analiz için yararlı olan uygulama istatistikleri toplar. CPU örnekleme çoğu performans araştırmalar başlatmak için önerilen yöntem hello. CPU örnekleme verileri toplarken, profil Merhaba uygulaması düşük bir etkisi yoktur.
* **İzleme** -bu yöntem, odaklı analiz ve giriş/çıkış performans sorunlarını çözümlemek için yararlı olan ayrıntılı zamanlama verileri toplar. Merhaba izleme yöntemi her giriş, çıkış ve işlev çağrısı hello işlevlerin bir modüldeki bir çalıştırma profili oluşturma sırasında kaydeder. Bu yöntem, kodunuzu bir bölümünü hakkında ayrıntılı zamanlama bilgi toplama ve hello girdi ve çıktı işlemleri uygulama performansı üzerindeki etkisini anlamak için kullanışlıdır. Bu yöntem, 32-bit işletim sistemi çalıştıran bir bilgisayar için devre dışı bırakılır. Bu seçenek yalnızca hello bulut hizmeti çalıştırdığınızda Azure, yerel olarak hello işlem öykünücüsü kullanılabilir.
* **.NET bellek ayırma** -hello örnekleme profili oluşturma yöntemi kullanarak bu yöntem .NET Framework bellek ayırma verileri toplar. Merhaba toplanan verileri hello sayısını ve boyutunu ayrılmış nesneleri içerir.
* **Eşzamanlılık** -bu yöntem kaynak çakışması veri ve çok kanallı ve birden çok işlem uygulamaları çözümlenmesinde kullanışlıdır işlemi ve iş parçacığı yürütme verileri toplar. Merhaba eşzamanlılık yöntemi gibi bir iş parçacığı zaman bekler, kodunuzu blokları yürütme erişimi tooan uygulama kaynak toobe serbest kilitli her olay için verileri toplar. Bu yöntem, çok iş parçacıklı uygulamalar çözümlemek için kullanışlıdır.
* Etkinleştirebilirsiniz **katman etkileşim profil**, zaman uyumlu ADO.NET hello yürütme sürelerinin hakkında ek bilgi sağlayan bir veya daha fazla iletişim çok katmanlı uygulamaların işlevlerinde çağırır veritabanları. Herhangi bir profil oluşturma yöntemlerini hello ile Katman etkileşim verileri toplayabilir. Katman etkileşimli profil oluşturma hakkında daha fazla bilgi için bkz: [katman etkileşimleri görünümü](https://msdn.microsoft.com/library/azure/dd557764.aspx).

## <a name="configuring-profiling-settings"></a>Profil oluşturma ayarlarını yapılandırma
gösterildiği nasıl aşağıdaki hello tooconfigure hello Azure uygulamasını Yayımla iletişim kutusu, profil ayarları.

![Profil ayarlarını yapılandır](./media/vs-azure-tools-performance-profiling-cloud-services/IC526984.png)

> [!NOTE]
> tooenable hello **profil oluşturmayı etkinleştirmek** onay kutusunu hello profil oluşturucu, bulut hizmetinizin toopublish kullanarak hello yerel bilgisayarda yüklü olması gerekir. Visual Studio yüklediğinizde varsayılan olarak, hello profil oluşturucu yüklenir.
> 
> 

### <a name="tooconfigure-profiling-settings"></a>tooconfigure ayarları profili oluşturma
1. Çözüm Gezgini'nde, Azure projeniz için hello kısayol menüsünü açın ve ardından **Yayımla**. Ayrıntılı adımlar için toopublish bir bulut hizmeti bkz [Bulutu yayımlama hello Azure araçları kullanarak hizmet](http://go.microsoft.com/fwlink/p?LinkId=623012).
2. Merhaba, **Azure uygulamasını Yayımla** iletişim kutusu, seçtiğiniz hello **Gelişmiş ayarları** sekmesi.
3. Profil oluşturma, tooenable seçin hello **profil oluşturmayı etkinleştirmek** onay kutusu.
4. tooconfigure profil ayarlarınızı seçin hello **ayarları** köprü. Hello profil ayarları iletişim kutusu görüntülenir.
5. Merhaba gelen **hangi profil oluşturma yöntemini yaptığınız gibi toouse** seçenek düğmeleri, gerektiğini bildiren profil hello türünü seçin.
6. toocollect hello katman etkileşimli profil oluşturma verilerini, select hello **etkinleştirmek katman etkileşim profil** onay kutusu.
7. toosave hello ayarları seçebilirsiniz hello **Tamam** düğmesi.
   
    Bu uygulama yayımladığınızda, bu profil oluşturma oturumu her rol için kullanılan toocreate hello ayarlardır.

## <a name="viewing-profiling-reports"></a>Profil oluşturma raporları görüntüleme
Bulut hizmetinizde rolünün her örneği için bir profil oluşturma oturumu oluşturulur. Visual Studio'dan her oturumun, profil tooview raporları, hello Sunucu Gezgini penceresini görüntülemek ve bir rol örneği hello Azure işlem düğümü tooselect'ı seçin. Profil oluşturma raporu hello aşağıdaki çizimde gösterildiği gibi hello sonra görüntüleyebilirsiniz.

![Azure'dan profil oluşturma raporunu görüntüleyin](./media/vs-azure-tools-performance-profiling-cloud-services/IC748914.png)

### <a name="tooview-profiling-reports"></a>Profil oluşturma raporları tooview
1. tooview hello Sunucu Gezgini penceresinde Visual Studio'da hello menü çubuğu seç görünümü, Sunucu Gezgini.
2. Hello Azure işlem düğümü seçin ve ardından Visual Studio'dan yayımlandığında tooprofile seçili hello Azure dağıtım düğümü hello bulut hizmeti için seçin.
3. tooview profil oluşturma raporları için bir örneği, hello hizmetinde, belirli bir örneği için açık hello kısayol menüsü hello rolünü seçin ve ardından **profil oluşturma raporunu görüntüle**.
   
    Merhaba rapor, bir .vsp dosyası artık Azure'dan indirilir ve hello Azure etkinlik günlüğü hello indirme hello durumu görüntülenir. Hello yükleme tamamlandığında, profil oluşturma raporu hello hello Düzenleyicisi adlı Visual Studio için bir sekmede görünür <Role name>  *<Instance Number>*  <identifier>.vsp. Merhaba rapor için Özet veriler görüntülenir.
4. Merhaba Geçerli Görünüm listesinde hello raporu farklı görünümlerini toodisplay hello istediğiniz görünümü seçin. Daha fazla bilgi için bkz: [profil oluşturma Araçlar rapor görünümlerini](https://msdn.microsoft.com/library/azure/bb385755.aspx).

## <a name="next-steps"></a>Sonraki adımlar
[Hata ayıklama bulut Hizmetleri](https://msdn.microsoft.com/library/azure/ee405479.aspx)

[Yayımlama tooan Visual Studio'dan Azure bulut hizmeti](https://msdn.microsoft.com/library/azure/ee460772.aspx)

