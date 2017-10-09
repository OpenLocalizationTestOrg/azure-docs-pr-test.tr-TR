---
title: "Visual Studio Team Services Azure içinde aaaContinuous teslimiyle | Microsoft Docs"
description: "Nasıl tooconfigure tooautomatically ve toohello Web uygulamasını Azure App Service veya Bulut hizmetlerini özelliğinde dağıtacak projeleri, Visual Studio Team Services ekip öğrenin."
services: cloud-services
documentationcenter: .net
author: mlearned
manager: douge
editor: 
ms.assetid: 797f67ad-e4d4-4063-ae91-41cbdf154191
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/06/2016
ms.author: mlearned
ms.openlocfilehash: eae75729e1c1a55f9bc3375604a8192f329d0042
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-delivery-tooazure-using-visual-studio-team-services"></a>Visual Studio Team Services kullanarak kesintisiz teslim tooAzure
Visual Studio Team Services takım projeleri tooautomatically yapınızı yapılandırın ve tooAzure web uygulamaları dağıtma veya Bulut Hizmetleri.  (Nasıl tooset yukarı sürekli bir yapı ve sistem kullanarak dağıtma hakkında bilgi için bir *şirket içi* Team Foundation Server, bkz: [Azure bulut Hizmetleri için devamlı teslim](cloud-services-dotnet-continuous-delivery.md).)

Bu öğreticide Visual Studio 2013 ve Azure SDK'sını hello olduğunu varsayar. Visual Studio 2013 zaten yoksa, hello seçerek karşıdan **ücretsiz olarak başlayın** adresindeki bağlantı [www.visualstudio.com](http://www.visualstudio.com). Yükleme hello Azure SDK [burada](http://go.microsoft.com/fwlink/?LinkId=239540).

> [!NOTE]
> Bu öğretici bir Visual Studio Team Services hesabı toocomplete gerekir: yapabilecekleriniz [ücretsiz bir Visual Studio Team Services hesabı açabilirsiniz](http://go.microsoft.com/fwlink/p/?LinkId=512979).
> 
> 

bir bulut hizmeti tooautomatically yukarı tooset derleme ve Visual Studio Team Services kullanarak tooAzure dağıtma, şu adımları izleyin.

## <a name="1-create-a-team-project"></a>1: takım projesi oluşturma
Hello yönergeleri izleyerek [burada](http://go.microsoft.com/fwlink/?LinkId=512980) toocreate ekibinizin proje ve tooVisual Studio bağlayın. Bu kılavuz, kaynak denetim çözümü Team Foundation sürüm denetimi (TFVC'yi) kullandığınızı varsayar. Sürüm denetimi için toouse Git istiyorsanız, bkz: [hello Git sürüm bu kılavuzun](http://go.microsoft.com/fwlink/p/?LinkId=397358).

## <a name="2-check-in-a-project-toosource-control"></a>2: bir proje toosource denetiminde denetleyin
1. Visual Studio'da toodeploy istediğiniz ya da yeni bir tane oluşturun hello çözümü açın.
   Bir web uygulaması dağıtma veya Bulut hizmeti (Azure uygulaması) aşağıdaki hello tarafından bu izlenecek adımları.
   Yeni bir çözüm toocreate istiyorsanız, yeni bir Azure bulut hizmeti projesi ya da yeni bir ASP.NET MVC projesi oluşturun. Proje hedefleri .NET Framework 4 veya 4.5 hello ve bir bulut hizmeti projesini oluşturuyorsanız, bir ASP.NET MVC web rolü ve çalışan rolü eklemek ve hello web rolü için Internet uygulamasını seçin emin olun. İstendiğinde, seçin **Internet uygulama**.
   Toocreate bir web uygulaması istiyorsanız hello ASP.NET Web uygulaması proje şablonunu seçin ve ardından MVC seçin. Bkz: [Azure App Service'te bir ASP.NET web uygulaması oluşturma](../app-service-web/app-service-web-get-started-dotnet.md).
   
   > [!NOTE]
   > Visual Studio Team Services, şu anda yalnızca Visual Studio Web uygulamalarının CI dağıtımları destekler. Web sitesi projeleri kapsamının dışında ' dir.
   > 
   > 
2. Merhaba çözüm hello bağlam menüsünü açın ve seçin **Çözüm Ekle tooSource denetim**.
   
    ![][5]
3. Kabul etmek veya hello varsayılanları değiştirmek ve hello seçin **Tamam** düğmesi. Kaynak Denetim simgelerini Hello işlemi tamamlandıktan sonra görünür **Çözüm Gezgini**.
   
    ![][6]
4. Merhaba çözüm hello kısayol menüsünü açın ve seçin **iade**.
   
    ![][7]
5. Merhaba, **bekleyen değişiklikleri** alanı **Takım Gezgini**hello iade için bir açıklama yazın ve hello seçin **iade** düğmesi.
   
    ![][8]
   
    Merhaba seçenekleri tooinclude dikkat edin veya belirli değişiklikleri, iade ettiğinizde dışlayın. Değişiklikleri dışlanır isterseniz, hello seçin **dahil tüm** bağlantı.
   
    ![][9]

## <a name="3-connect-hello-project-tooazure"></a>3: hello proje tooAzure Bağlan
1. Bazı kaynak kodu ile VS Team Services takım projesi içine sahip olduğunuza göre hazır tooconnect olan ekibinizin proje tooAzure.  Merhaba, [Klasik Azure portalı](http://go.microsoft.com/fwlink/?LinkID=213885), bulut hizmeti veya web uygulamanızı seçin veya hello seçerek yeni bir tane oluşturun  **+**  hello sol alt ve seçme simgesine **bulut hizmeti** veya **Web uygulaması** ve ardından **hızlı Oluştur**. Merhaba seçin **Visual Studio Team Services ile yayımlamayı ayarlayın** bağlantı.
   
    ![][10]
2. Hello sihirbazında, hello metin kutusuna hello Visual Studio Team Services hesabınızın adını yazın ve hello **şimdi Yetkilendir** bağlantı. İçinde toosign istenebilir.
   
    ![][11]
3. Merhaba, **bağlantı isteği** açılan iletişim kutusunda, hello seçin **kabul** düğmesini tooauthorize ekibinizin proje VS Team Services içinde Azure tooconfigure.
   
    ![][12]
4. Yetkilendirme başarılı olduğunda, Visual Studio Team Services takım projelerinin listesini içeren bir açılır bakın. Merhaba önceki adımlarda oluşturduğunuz takım projesi Hello adını seçin ve ardından hello sihirbazın onay düğmesini seçin.
   
    ![][13]
5. Projenizi bağlandıktan sonra değişiklikler tooyour Visual Studio Team Services takım projesinde denetleme bazı yönergeler görürsünüz.  Sonraki iade, Visual Studio Team Services oluşturup, proje tooAzure dağıtacak.  Try hello tıklatarak bunu şimdi **Visual Studio'dan iade** bağlamak ve ardından hello **başlatma Visual Studio** bağlantı (veya eşdeğer hello **Visual Studio** hello altındaki düğmesi Merhaba portal ekran).
   
    ![][14]

## <a name="4-trigger-a-rebuild-and-redeploy-your-project"></a>4: yeniden tetikleyebilir ve projenizi yeniden dağıtmak
1. Visual Studio'nun içinde **Takım Gezgini**, hello seçin **Kaynak Denetim Gezgini** bağlantı.
   
    ![][15]
2. Tooyour çözüm dosyasını gidin ve açın.
   
    ![][16]
3. İçinde **Çözüm Gezgini**, bir dosyasını açın ve değiştirin. Örneğin, hello dosya değişiklik `_Layout.cshtml` hello görünümleri altında\\paylaşılan klasöründe bir MVC web rolü.
   
    ![][17]
4. Merhaba logosu hello site için düzenleyin ve seçin **Ctrl + S** toosave hello dosya.
   
    ![][18]
5. İçinde **Takım Gezgini**, hello seçin **bekleyen değişiklikleri** bağlantı.
   
    ![][19]
6. Bir açıklama girin ve ardından hello **iade** düğmesi.
   
    ![][20]
7. Merhaba seçin **ev** düğmesini tooreturn toohello **Takım Gezgini** giriş sayfası.
   
    ![][21]
8. Merhaba seçin **derlemeler** bağlantı tooview hello derlemeler sürüyor.
   
    ![][22]
   
    **Takım Gezgini** bir yapı için iade tetiklenen gösterir.
   
    ![][23]
9. İlerleme tooview ayrıntılı günlüğü hello derlemede Hello adını hello yapı ilerledikçe çift tıklatın.
   
    ![][24]
10. Merhaba derleme sürüyor olsa da, Başlangıç Sihirbazı'nı kullanarak TFS tooAzure bağlandığında, oluşturulan hello derleme tanımı göz atın.  Merhaba derleme tanımı için hello kısayol menüsünü açın ve seçin **derleme tanımını Düzenle**.
    
     ![][25]
    
     Merhaba, **tetikleyici** sekmesinde hello derleme tanımı toobuild her iade varsayılan olarak ayarlandığını görürsünüz.
    
     ![][26]
    
     Merhaba, **işlem** sekmesinde, bulut hizmeti veya web uygulamasının adını toohello hello dağıtım ortamı ayarlayın görebilirsiniz. Web uygulamaları ile çalışıyorsanız, gördüğünüz hello özellikleri burada gösterilen olanlardan farklı olacaktır.
    
     ![][27]
11. Merhaba Varsayılanları farklı değerler istiyorsanız hello özelliklerinin değerlerini belirtin. Hello Azure yayımlama hello özelliklerdir **dağıtım** bölümü.
    
     Merhaba aşağıdaki tabloda hello kullanılabilir özellikler hello gösterilmektedir **dağıtım** bölümü:
    
    | Özellik | Varsayılan değer |
    | --- | --- |
    | Güvenilmeyen Sertifikalar izin ver |SSL sertifikaları yanlışsa, bir kök yetkilisi tarafından imzalanması gerekir. |
    | Yükseltme izin ver |Merhaba dağıtım tooupdate yeni bir tane oluşturmak yerine var olan bir dağıtımını sağlar. Başlangıç IP adresi korur. |
    | Silmeyin |TRUE ise, var olan bir ilgisiz dağıtımını üzerine yazma (yükseltme izin verilir). |
    | Yol tooDeployment ayarları |Merhaba yol tooyour .pubxml dosya hello depodaki göreli toohello kök klasöründe bir web uygulaması için. Bulut Hizmetleri için yoksayıldı. |
    | SharePoint dağıtım ortamı |aynı hello hizmet adı olarak hello. |
    | Azure dağıtım ortamı |Merhaba web uygulaması veya Bulut hizmeti adı. |
12. Birden fazla hizmet yapılandırma (.cscfg dosyaları) kullanıyorsanız, hello istenen hizmet yapılandırmasını hello belirtebilirsiniz **MSBuild bağımsız değişkenleri Gelişmiş, yapı** ayarı. Örneğin, toouse ServiceConfiguration.Test.cscfg, ayarlar MSBuild bağımsız değişkenleri satırı seçeneği `/p:TargetProfile=Test`.
    
     ![][38]
    
     Bu zamana kadar yapınızın başarıyla tamamlanmalıdır.
    
     ![][28]
13. Merhaba derleme adına çift tıklayın, Visual Studio gösterir. bir **Yapı Özeti**, tüm test sonuçlarını da dahil olmak üzere, birim testi projelerini ilişkilendirilmiş.
    
     ![][29]
14. Merhaba, [Klasik Azure portalı](http://go.microsoft.com/fwlink/?LinkID=213885), ilişkili hello dağıtım üzerinde hello görüntüleyebilirsiniz **dağıtımları** ortam hazırlama hello seçildiğinde sekme.
    
     ![][30]
15. Tooyour sitenin URL'sini göz atın. Bir web uygulaması için hello tıklatmanız **Gözat** düğmesi hello komut çubuğunda. Bir bulut hizmeti için hello URL'si hello seçin **Hızlı Bakış** hello bölümünü **Pano** hello hazırlama ortamını bir bulut hizmeti için gösteren sayfası. Bulut Hizmetleri için sürekli tümleştirme dağıtımlarından yayımlanan toohello hazırlama ortamını varsayılan olarak ' dir. Bu ayarı hello tarafından değiştirebilirsiniz **alternatif bir bulut hizmeti ortamını** özelliği çok**üretim**. Bu ekran hello burada site URL'si hello bulut hizmetin panosu sayfasında gösterilir.
    
    ![][31]
    
    Yeni bir tarayıcı sekmesi tooreveal çalışan sitenizi açılır.
    
    ![][32]
    
    Bulut Hizmetleri için diğer değişiklikleri tooyour proje yaparsanız, tetikleyici daha oluşturur ve birden çok dağıtım toplanacaktır. Merhaba en son etkin olarak işaretlenmiş.
    
    ![][33]

## <a name="5-redeploy-an-earlier-build"></a>5: önceki bir yapı yeniden dağıtın
Bu adım isteğe bağlıdır ve toocloud Hizmetleri geçerlidir. Klasik Azure portalı Merhaba, önceki bir dağıtıma seçin ve hello seçin **dağıtmanız** toorewind, site tooan önceki iade düğmesine tıklayın.  Bu TFS'de yeni bir derlemeyi tetiklemeyi ve yeni bir giriş dağıtım geçmişiniz oluşturmak, unutmayın.

![][34]

## <a name="6-change-hello-production-deployment"></a>6: hello Üretim dağıtımı değiştirme
Bu adım yalnızca toocloud Hizmetleri, web uygulamaları geçerlidir. Hazır olduğunuzda hello seçerek hello hazırlama ortamı toohello üretim ortamını yükseltebilirsiniz **takas** hello Klasik Azure portalı düğmesini. Yeni dağıtılan hello hazırlama ortamıdır yükseltilen tooProduction ve hello önceki üretim ortamında, varsa, bir hazırlama ortamını olur. Hello etkin dağıtım hello üretim ve hazırlama ortamları için farklı olabilir, ancak son yapılar hello dağıtım geçmişini olduğu hello aynı ne olursa olsun, ortam.

![][35]

## <a name="7-run-unit-tests"></a>7: birim testleri çalıştırma
Bu adım, bulut Hizmetleri yalnızca tooweb uygulamaları geçerlidir. dağıtımınızdaki kalite kapısı tooput, birim testleri çalıştırabilirsiniz ve başarısız olursa hello dağıtım durdurabilirsiniz.

1. Visual Studio'da birim testi projesi ekleyin.
   
   ![][39]
2. Proje başvuruları toohello proje tootest istediğiniz ekleyin.
   
   ![][40]
3. Bazı birim testleri ekleme. tooget başlatıldı, her zaman geçirir kukla bir test deneyin.
   
       ```
       using System;
       using Microsoft.VisualStudio.TestTools.UnitTesting;
   
       namespace UnitTestProject1
       {
           [TestClass]
           public class UnitTest1
           {
               [TestMethod]
               [ExpectedException(typeof(NotImplementedException))]
               public void TestMethod1()
               {
                   throw new NotImplementedException();
               }
           }
       }
       ```
4. Merhaba derleme tanımı düzenleme, hello seçin **işlem** sekmesini tıklatın ve hello genişletin **Test** düğümü.
5. Set hello **başarısız yapı test hatasında** tooTrue. Bu, hello testleri geçilir sürece hello dağıtım karşılaşılmaz anlamına gelir.
   
   ![][41]
6. Yeni bir derleme sırası.
   
   ![][42]
   
   ![][43]
7. Merhaba derleme devam ederken üzerinde ilerleme durumunu denetleyin.
   
    ![][44]
   
    ![][45]
8. Merhaba yapı yapıldığında hello test sonuçlarını denetleyin.
   
    ![][46]
   
    ![][47]
9. Başarısız olacak bir test oluşturmayı deneyin. Yeni bir test hello kopyalayarak birinci eklemek, yeniden adlandırın ve beklenen bir özel durum NotImplementedException olduğunu bildiren kod hello satırını açıklama.
   
       ```
       [TestMethod]
       //[ExpectedException(typeof(NotImplementedException))]
       public void TestMethod2()
       {
           throw new NotImplementedException();
       }
       ```
10. Merhaba iade tooqueue yeni bir yapı değiştirin.
    
     ![][48]
11. Merhaba test sonuçları toosee hello hata ayrıntılarını görüntüleyin.
    
     ![][49]
    
     ![][50]

## <a name="next-steps"></a>Sonraki adımlar
Birim testi Visual Studio Team Services içinde hakkında daha fazla bilgi için bkz: [birim testleri, derlemede çalıştırılan](http://go.microsoft.com/fwlink/p/?LinkId=510474). Git kullanıyorsanız, bkz: [Git kodunuzda paylaşmak](http://www.visualstudio.com/get-started/share-your-code-in-git-vs.aspx) ve [sürekli dağıtım tooAzure uygulama hizmeti](../app-service-web/app-service-continuous-deployment.md).  Visual Studio Team Services hakkında daha fazla bilgi için bkz: [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).

[0]: ./media/cloud-services-continuous-delivery-use-vso/tfs0.PNG
[1]: ./media/cloud-services-continuous-delivery-use-vso/tfs1.png
[2]: ./media/cloud-services-continuous-delivery-use-vso/tfs2.png

[5]: ./media/cloud-services-continuous-delivery-use-vso/tfs5.png
[6]: ./media/cloud-services-continuous-delivery-use-vso/tfs6.png
[7]: ./media/cloud-services-continuous-delivery-use-vso/tfs7.png
[8]: ./media/cloud-services-continuous-delivery-use-vso/tfs8.png
[9]: ./media/cloud-services-continuous-delivery-use-vso/tfs9.png
[10]: ./media/cloud-services-continuous-delivery-use-vso/tfs10.png
[11]: ./media/cloud-services-continuous-delivery-use-vso/tfs11.png
[12]: ./media/cloud-services-continuous-delivery-use-vso/tfs12.png
[13]: ./media/cloud-services-continuous-delivery-use-vso/tfs13.png
[14]: ./media/cloud-services-continuous-delivery-use-vso/tfs14.png
[15]: ./media/cloud-services-continuous-delivery-use-vso/tfs15.png
[16]: ./media/cloud-services-continuous-delivery-use-vso/tfs16.png
[17]: ./media/cloud-services-continuous-delivery-use-vso/tfs17.png
[18]: ./media/cloud-services-continuous-delivery-use-vso/tfs18.png
[19]: ./media/cloud-services-continuous-delivery-use-vso/tfs19.png
[20]: ./media/cloud-services-continuous-delivery-use-vso/tfs20.png
[21]: ./media/cloud-services-continuous-delivery-use-vso/tfs21.png
[22]: ./media/cloud-services-continuous-delivery-use-vso/tfs22.png
[23]: ./media/cloud-services-continuous-delivery-use-vso/tfs23.png
[24]: ./media/cloud-services-continuous-delivery-use-vso/tfs24.png
[25]: ./media/cloud-services-continuous-delivery-use-vso/tfs25.png
[26]: ./media/cloud-services-continuous-delivery-use-vso/tfs26.png
[27]: ./media/cloud-services-continuous-delivery-use-vso/tfs27.png
[28]: ./media/cloud-services-continuous-delivery-use-vso/tfs28.png
[29]: ./media/cloud-services-continuous-delivery-use-vso/tfs29.png
[30]: ./media/cloud-services-continuous-delivery-use-vso/tfs30.png
[31]: ./media/cloud-services-continuous-delivery-use-vso/tfs31.png
[32]: ./media/cloud-services-continuous-delivery-use-vso/tfs32.png
[33]: ./media/cloud-services-continuous-delivery-use-vso/tfs33.png
[34]: ./media/cloud-services-continuous-delivery-use-vso/tfs34.png
[35]: ./media/cloud-services-continuous-delivery-use-vso/tfs35.png
[36]: ./media/cloud-services-continuous-delivery-use-vso/tfs36.PNG
[37]: ./media/cloud-services-continuous-delivery-use-vso/tfs37.PNG
[38]: ./media/cloud-services-continuous-delivery-use-vso/AdvancedMSBuildSettings.PNG
[39]: ./media/cloud-services-continuous-delivery-use-vso/AddUnitTestProject.PNG
[40]: ./media/cloud-services-continuous-delivery-use-vso/AddProjectReferences.PNG
[41]: ./media/cloud-services-continuous-delivery-use-vso/EditBuildDefinitionForTest.PNG
[42]: ./media/cloud-services-continuous-delivery-use-vso/QueueNewBuild.PNG
[43]: ./media/cloud-services-continuous-delivery-use-vso/QueueBuildDialog.PNG
[44]: ./media/cloud-services-continuous-delivery-use-vso/BuildInTeamExplorer.PNG
[45]: ./media/cloud-services-continuous-delivery-use-vso/BuildRequestInfo.PNG
[46]: ./media/cloud-services-continuous-delivery-use-vso/BuildSucceeded.PNG
[47]: ./media/cloud-services-continuous-delivery-use-vso/TestResultsPassed.PNG
[48]: ./media/cloud-services-continuous-delivery-use-vso/CheckInChangeToMakeTestsFail.PNG
[49]: ./media/cloud-services-continuous-delivery-use-vso/TestsFailed.PNG
[50]: ./media/cloud-services-continuous-delivery-use-vso/TestsResultsFailed.PNG
