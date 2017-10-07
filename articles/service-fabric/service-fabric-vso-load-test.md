---
title: "aaaLoad, Visual Studio Team Services kullanarak uygulamanızı test etme | Microsoft Docs"
description: "Visual Studio Team Services kullanarak toostress Azure Service Fabric uygulamalarınızı nasıl test öğrenin."
services: service-fabric
documentationcenter: na
author: cawams
manager: timlt
editor: 
ms.assetid: fc743585-0d1b-483f-981d-493f4552ac07
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/18/2016
ms.author: cawa
ms.openlocfilehash: 663cf8db5e8f0a4d0d7f27b585645d7f776392f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="load-test-your-application-by-using-visual-studio-team-services"></a>Yük, Visual Studio Team Services kullanarak uygulamanızı test etme
Bu makalede, bir uygulamanın nasıl toouse Microsoft Visual Studio Yük Testi özellikleri toostress test gösterilmektedir. Bir Azure Service Fabric durum bilgisi olan hizmet arka uç ve bir durum bilgisi olmayan web ön uç kullanır. Merhaba burada kullanılan örnek bir uçak konumu simulator uygulamasıdır. Bir uçak kimliği, ayrılma süresi ve hedef sağlayın. Merhaba uygulamanın arka uç hello isteklerini işler ve hello ön uç hello ölçütlerle eşleşen bir harita hello uçak görüntüler.

Merhaba Aşağıdaki diyagramda, test Merhaba Service Fabric uygulaması gösterilmektedir.

![Merhaba örnek uçak konumu uygulama diyagramı][0]

## <a name="prerequisites"></a>Ön koşullar
Başlamadan önce toodo hello aşağıdaki gerekir:

* Visual Studio Team Services hesabı edinin. Ücretsiz adresindeki edinebilirsiniz [Visual Studio Team Services](https://www.visualstudio.com).
* Alma ve Visual Studio 2013 veya Visual Studio 2015 yükleyin. Bu makalede Visual Studio 2015 Enterprise edition kullanır, ancak Visual Studio 2013 ve diğer sürümleri benzer şekilde çalışması gerekir.
* Ortamı hazırlama, uygulama tooa dağıtın. Bkz: [toodeploy uygulamaları tooa uzaktan nasıl küme Visual Studio kullanarak](service-fabric-publish-app-remote-cluster.md) bu hakkında bilgi için.
* Uygulamanızın kullanım deseniyle anlayın. Bu bilgiler kullanılan toosimulate hello yük düzeni olur.
* Yük testi için hello hedef anlayın. Bu, yorumlar ve hello yük testi sonuçlarını analiz yardımcı olur.

## <a name="create-and-run-hello-web-performance-and-load-test-project"></a>Oluşturma ve hello proje Web performansı ve yük testi çalıştırma
### <a name="create-a-web-performance-and-load-test-project"></a>Bir Web performansı ve yük testi projesi oluşturma
1. Visual Studio 2015’i açın. Seçin **dosya** > **yeni** > **proje** hello menü çubuğundan tooopen hello **yeni proje** iletişim kutusu.
2. Merhaba genişletin **Visual C#** düğümü seçin **Test** > **Web performansı ve yük testi projesi**. Merhaba proje bir ad verin ve ardından hello **Tamam** düğmesi.

    ![Merhaba yeni proje iletişim kutusunun ekran görüntüsü][1]

    Çözüm Gezgini'nde yeni bir Web performansı ve yük testi projesi görmeniz gerekir.

    ![Çözüm Gezgini hello yeni proje gösteren ekran görüntüsü][2]

### <a name="record-a-web-performance-test"></a>Web performans testini kaydetme
1. Açık hello .webtest projesi.
2. Merhaba seçin **ekleme kaydı** simgesi toostart tarayıcınızda kaydı oturumu.

    ![Bir tarayıcıda hello kayıt Ekle simgesinin ekran görüntüsü][3]

    ![Bir tarayıcıda hello kayıt düğmesinin Ekran görüntüsü][4]
3. Toohello Service Fabric uygulaması göz atın. Merhaba kaydı paneli hello web istekleri göstermelidir.

    ![Panel kaydı hello web isteklerini ekran görüntüsü][5]
4. Bir dizi hello kullanıcılar tooperform beklediğiniz eylemi gerçekleştirin. Bu eylemler bir desen toogenerate hello yük kullanılır.
5. İşiniz bittiğinde, hello seçin **durdurmak** düğmesini toostop kaydı.

    ![Merhaba Durdur düğmesinin Ekran görüntüsü][6]

    Visual Studio'da .webtest projesi Hello isteklerini bir dizi yakalanan. Dinamik parametreleri otomatik olarak değiştirilir. Bu noktada, test senaryonuz parçası olmayan herhangi bir ek, yinelenen bağımlılık isteğinin silebilirsiniz.
6. Merhaba projeyi kaydedin ve ardından hello **testi Çalıştır** komutu toorun hello web performansı yerel olarak test ve doğru şekilde her şeyi çalıştığından emin olun.

    ![Merhaba testi komutu ekran görüntüsü][7]

### <a name="parameterize-hello-web-performance-test"></a>Merhaba web performans testini Parametreleştirme
Tooa kodlanmış web performans testi dönüştürme ve hello kod düzenleme hello web performans testini Parametreleştirme. Alternatif olarak, böylece Hello test tekrarlanan hello verilerine hello web performans testi tooa veri listesi bağlayabilirsiniz. Bkz: [oluşturma ve çalıştırma kodlanmış web performans testine](https://msdn.microsoft.com/library/ms182552.aspx) nasıl tooconvert hello web performans testi tooa Kodlanmış testi hakkında ayrıntılar için. Bkz: [veri kaynağı tooa web performans testine ekleme](https://msdn.microsoft.com/library/ms243142.aspx) nasıl toobind veri tooa web performansı hakkında bilgi için test edin.

Hello uçak kimliği oluşturulan GUID ile değiştirin ve daha fazla istekleri toosend uçuşlar toodifferent konum eklemek için bu örnekte, biz hello web performans testi kodlanmış tooa test dönüştürmeniz.

### <a name="create-a-load-test-project"></a>Bir yük testi projesi oluşturma
Merhaba web performans testi ve ek belirtilen yük test ayarları ile birlikte birim testi tarafından açıklanan bir veya daha fazla senaryo, bir yük testi projesi oluşur. Aşağıdaki adımları hello nasıl toocreate bir yük testi projesi göster:

1. Merhaba kısayol menüsünde Web performansı ve yük testi projenizin, **Ekle** > **yük testi**. Merhaba, **yük testi** Sihirbazı'nı hello seçin **sonraki** düğmesini tooconfigure hello test ayarları.
2. Merhaba, **yük düzeni** bölümünde, bir sabit kullanıcı yük veya birkaç kullanıcı ile başlayan bir adım yük istediğiniz ve zamanla artar hello kullanıcıları seçin.

    İyi bir kullanıcı yük hello miktarı tahmin varsa ve hello geçerli sistem nasıl gerçekleştireceğini toosee istediğiniz seçin **sabit yük**. Amacınız toolearn ise Hello sistem sürekli olarak çeşitli yük altında gerçekleştiğini seçmeniz **Adım yük**.
3. Merhaba, **Test karışımı** bölümünde, hello seçin **Ekle** düğmesine ve ardından hello test hello yük testinde tooinclude istiyor. Merhaba kullanabilirsiniz **dağıtım** sütun toospecify hello toplam testleri her test için Çalıştır yüzdesi.
4. Merhaba, **çalıştırma ayarları** bölümünde, hello yük test süresi belirtin.

   > [!NOTE]
   > Merhaba **Test Yinelemeleri** seçenek, kullanılabilir yerel olarak Visual Studio kullanarak bir yük testi çalıştırdığınızda.
   >
   >
5. Merhaba, **konumu** bölümünü **çalıştırma ayarları**, yük testi istekleri üretilen burada hello konumu belirtin. Başlangıç Sihirbazı'nı tooyour Team Services hesabı toolog isteyebilir. Oturum açın ve ardından bir coğrafi konumu seçin. İşiniz bittiğinde, hello seçin **son** düğmesi.
6. Merhaba yük testi oluşturulduktan sonra hello .loadtest projeyi açın ve ayarı çalıştırmak hello geçerli seçin **çalıştırma ayarları** > **çalıştırma Ayarları1 [etkin]**. Hello çalıştırmak hello ayarları açılır **özellikleri** penceresi.
7. Merhaba, **sonuçları** hello bölümünü **çalıştırma ayarları** Özellikleri penceresinde, hello **zamanlama ayrıntıları depolama** ayarı olmalıdır **hiçbiri** olarak Varsayılan değer. Bu değeri çok değiştirmek**Tüm Bireysel Ayrıntılar** tooget hello yük testi sonuçlarını hakkında daha fazla bilgi. Bkz: [yük testi](https://www.visualstudio.com/load-testing.aspx) nasıl tooconnect tooVisual Studio Team Services ve Çalıştır bir yük testi hakkında daha fazla bilgi.

### <a name="run-hello-load-test-by-using-visual-studio-team-services"></a>Visual Studio Team Services kullanarak Hello yük testi çalıştırma
Merhaba seçin **yük testi Çalıştır** komutu toostart hello testi çalıştırma.

![Yük testi çalıştırma komutu hello ekran görüntüsü][8]

## <a name="view-and-analyze-hello-load-test-results"></a>Görüntüleme ve hello yük testi sonuçlarını çözümleme
Test ilerlemesi Hello yüklenemedi, hello performans bilgileri grafiği çizilecek. Grafik aşağıdaki benzeri toohello görmeniz gerekir.

![Yük testi sonuçlarını performans grafiği ekran görüntüsü][9]

1. Merhaba seçin **karşıdan rapor** hello sayfasının hello üstüne yakın bağlantı. Merhaba rapor İndirildikten sonra hello seçin **görüntülemek rapor** düğmesi.

    Merhaba üzerinde **grafik** sekmesini çeşitli performans sayaçları için grafikleri görebilirsiniz. Merhaba üzerinde **Özet** sekmesinde, hello genel test sonuçları görüntülenir. Merhaba **tabloları** sekmesi hello başarılı ve başarısız yük testleri toplam sayısını gösterir.
2. Merhaba Hello sayı bağlantıları seçin **Test** > **başarısız** ve hello **hataları** > **sayısı** sütunlar toosee hata ayrıntıları.

    Merhaba **ayrıntı** sekmesi başarısız istekler için sanal kullanıcı ve test senaryosu bilgilerini gösterir. Bu veriler birden çok senaryolar hello yük testi içeriyorsa, yararlı olabilir.

Bkz: [çözümleme yük testi sonuçlarında hello Grafik görünümünde Yük Testi Çözümleyicisi hello](https://www.visualstudio.com/load-testing.aspx) yük görüntüleme hakkında daha fazla bilgi için test sonuçları.

## <a name="automate-your-load-test"></a>Yük testlerini otomatikleştirme
Visual Studio Team Services yük sınama yük testleri yönetmek ve bir Team Services hesabında sonuçlarını analiz API'leri toohelp sağlar. Bkz: [bulut yük test etme Rest API'leri](http://blogs.msdn.com/b/visualstudioalm/archive/2014/11/03/cloud-load-testing-rest-apis-are-here.aspx) daha fazla bilgi için.

## <a name="next-steps"></a>Sonraki adımlar
* [İzleme ve yerel makine geliştirme Kurulum Hizmetleri'nde tanılama](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[0]: ./media/service-fabric-vso-load-test/OverviewDiagram.png
[1]: ./media/service-fabric-vso-load-test/NewProjectDialog.png
[2]: ./media/service-fabric-vso-load-test/Project.png
[3]: ./media/service-fabric-vso-load-test/AddRecording.png
[4]: ./media/service-fabric-vso-load-test/AddRecording2.png
[5]: ./media/service-fabric-vso-load-test/ActionSequence.png
[6]: ./media/service-fabric-vso-load-test/StopRecording.png
[7]: ./media/service-fabric-vso-load-test/RunTest.png
[8]: ./media/service-fabric-vso-load-test/RunTest2.png
[9]: ./media/service-fabric-vso-load-test/Graph.png
