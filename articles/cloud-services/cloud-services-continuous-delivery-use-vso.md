---
title: "Visual Studio Team Services içinde Azure ile sürekli teslim | Microsoft Docs"
description: "Otomatik olarak oluşturmak ve Web uygulaması özellikle Azure uygulama hizmeti veya Bulut hizmetlerini dağıtmak için Visual Studio Team Services takım projeleriniz yapılandırmayı öğrenin."
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
ms.openlocfilehash: d80ce63eb7ddfd7c45726be887a772f9a7594b28
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="continuous-delivery-to-azure-using-visual-studio-team-services"></a>Visual Studio Team Services'ı kullanarak Azure'a sürekli teslim
Otomatik olarak oluşturabilir ve Azure web uygulamaları dağıtma veya Bulut Hizmetleri için Visual Studio Team Services takım projeleriniz yapılandırabilirsiniz.  (Sürekli bir yapı ayarlayın ve sistem kullanarak dağıtma hakkında bilgi için bir *şirket içi* Team Foundation Server, bkz: [Azure bulut Hizmetleri için devamlı teslim](cloud-services-dotnet-continuous-delivery.md).)

Bu öğreticide Visual Studio 2013 ve Azure SDK'ın yüklü olduğunu varsayar. Visual Studio 2013 yoksa seçerek karşıdan **ücretsiz olarak başlayın** adresindeki bağlantı [www.visualstudio.com](http://www.visualstudio.com). Azure SDK yüklemek [burada](http://go.microsoft.com/fwlink/?LinkId=239540).

> [!NOTE]
> Bu öğreticiyi tamamlamak için bir Visual Studio Team Services hesabınızın olması gerekir: yapabilecekleriniz [ücretsiz bir Visual Studio Team Services hesabı açabilirsiniz](http://go.microsoft.com/fwlink/p/?LinkId=512979).
> 
> 

Otomatik olarak oluşturmak ve Visual Studio Team Services kullanarak Azure'a dağıtmak için bir bulut hizmeti ayarlamak için aşağıdaki adımları izleyin.

## <a name="1-create-a-team-project"></a>1: takım projesi oluşturma
Yönergeleri izleyerek [burada](http://go.microsoft.com/fwlink/?LinkId=512980) takım projesi oluşturmak ve Visual Studio bağlamak için. Bu kılavuz, kaynak denetim çözümü Team Foundation sürüm denetimi (TFVC'yi) kullandığınızı varsayar. Git sürüm denetimi için kullanmak istiyorsanız, bkz: [bu kılavuzun Git sürüm](http://go.microsoft.com/fwlink/p/?LinkId=397358).

## <a name="2-check-in-a-project-to-source-control"></a>2: kaynak denetimi projesindeki denetleyin
1. Visual Studio'da, dağıtmak istediğiniz çözümü açın veya yeni bir tane oluşturun.
   Bu izlenecek adımları izleyerek bir web uygulaması veya bir bulut hizmeti (Azure uygulaması) dağıtabilirsiniz.
   Yeni bir çözüm oluşturmak istiyorsanız, yeni bir Azure bulut hizmeti projesi ya da yeni bir ASP.NET MVC projesi oluşturun. Proje .NET Framework 4 veya 4.5 hedefler emin olun ve bir bulut hizmeti projesini oluşturuyorsanız, bir ASP.NET MVC web rolü ve çalışan rolü eklemek ve Internet uygulamasını web rolü seçin. İstendiğinde, seçin **Internet uygulama**.
   Bir web uygulaması oluşturmak istiyorsanız, ASP.NET Web uygulaması proje şablonunu seçin ve ardından MVC seçin. Bkz: [Azure App Service'te bir ASP.NET web uygulaması oluşturma](../app-service-web/app-service-web-get-started-dotnet.md).
   
   > [!NOTE]
   > Visual Studio Team Services, şu anda yalnızca Visual Studio Web uygulamalarının CI dağıtımları destekler. Web sitesi projeleri kapsamının dışında ' dir.
   > 
   > 
2. Çözüm için bağlam menüsünü açın ve seçin **kaynak denetimine Çözüm Ekle**.
   
    ![][5]
3. Kabul etmek veya varsayılanları değiştirmek ve seçin **Tamam** düğmesi. İşlem tamamlandıktan sonra kaynak denetim simgelerini görünür **Çözüm Gezgini**.
   
    ![][6]
4. Çözüm için kısayol menüsünü açın ve seçin **iade**.
   
    ![][7]
5. İçinde **bekleyen değişiklikleri** alanı **Takım Gezgini**iade için bir açıklama yazın ve seçin **iade** düğmesi.
   
    ![][8]
   
    Dahil etmek veya belirli değişiklikler, iade ettiğinizde hariç seçenekleri not edin. Değişiklikleri dışlanır isterseniz seçin **dahil tüm** bağlantı.
   
    ![][9]

## <a name="3-connect-the-project-to-azure"></a>3: Proje için Azure connect
1. Bazı kaynak kodu ile VS Team Services takım projesi içine sahip olduğunuza göre takım projenize Azure'a bağlanmak hazır olursunuz.  İçinde [Klasik Azure portalı](http://go.microsoft.com/fwlink/?LinkID=213885), bulut hizmeti veya web uygulamanızı seçin veya seçerek yeni bir tane oluşturun  **+**  simgesini seçerek ve sol alt **bulut hizmeti**veya **Web uygulaması** ve ardından **hızlı Oluştur**. Seçin **Visual Studio Team Services ile yayımlamayı ayarlayın** bağlantı.
   
    ![][10]
2. Sihirbazı'nda tıklatın ve metin kutusuna, Visual Studio Team Services hesabınızın adını yazın **şimdi Yetkilendir** bağlantı. Oturum açmak için istenebilir.
   
    ![][11]
3. İçinde **bağlantı isteği** açılan iletişim kutusunda, seçin **kabul** VS Team Services içinde takım projenizin yapılandırmak için Azure yetkilendirmek için düğmesi.
   
    ![][12]
4. Yetkilendirme başarılı olduğunda, Visual Studio Team Services takım projelerinin listesini içeren bir açılır bakın. Önceki adımlarda oluşturduğunuz takım projesi adını seçin ve ardından sihirbazın onay düğmesini seçin.
   
    ![][13]
5. Projenizi bağlandıktan sonra Visual Studio Team Services takım projenize değişiklikleri denetlemek için bazı yönergeler görürsünüz.  Sonraki iade, Visual Studio Team Services oluşturup projenize Azure'a dağıtacak.  Bu artık tıklayarak deneyin **Visual Studio'dan iade** bağlantı ve ardından **başlatma Visual Studio** bağlantı (veya eşdeğer **Visual Studio** alt kısmındaki düğmesi Portal ekran).
   
    ![][14]

## <a name="4-trigger-a-rebuild-and-redeploy-your-project"></a>4: yeniden tetikleyebilir ve projenizi yeniden dağıtmak
1. Visual Studio'nun içinde **Takım Gezgini**, seçin **Kaynak Denetim Gezgini** bağlantı.
   
    ![][15]
2. Çözüm dosyasına gidin ve açın.
   
    ![][16]
3. İçinde **Çözüm Gezgini**, bir dosyasını açın ve değiştirin. Örneğin, dosyayı değiştirmek `_Layout.cshtml` görünümleri altında\\paylaşılan klasöründe bir MVC web rolü.
   
    ![][17]
4. Site için logo düzenleyin ve seçin **Ctrl + S** dosyayı kaydetmek için.
   
    ![][18]
5. İçinde **Takım Gezgini**, seçin **bekleyen değişiklikleri** bağlantı.
   
    ![][19]
6. Bir açıklama girin ve ardından **iade** düğmesi.
   
    ![][20]
7. Seçin **ev** geri dönmek için düğmesini **Takım Gezgini** giriş sayfası.
   
    ![][21]
8. Seçin **derlemeler** ediyor yapıları görüntülemek için bağlantı.
   
    ![][22]
   
    **Takım Gezgini** bir yapı için iade tetiklenen gösterir.
   
    ![][23]
9. Yapı Yapılandırma sürerken ayrıntılı bir günlüğünü görüntülemek için devam eden adına çift tıklayın.
   
    ![][24]
10. Derleme Sürüyor olsa da, Sihirbazı'nı kullanarak TFS Azure'a bağlandığında, oluşturulan derleme tanımını göz atın.  Derleme tanımı için kısayol menüsünü açın ve seçin **derleme tanımını Düzenle**.
    
     ![][25]
    
     İçinde **tetikleyici** sekmesinde derleme tanımını her iade oluşturmak için varsayılan olarak ayarlandığını görürsünüz.
    
     ![][26]
    
     İçinde **işlem** sekmesinde, dağıtım ortamı bulut hizmeti veya web uygulamasının adına ayarlayın görebilirsiniz. Web uygulamaları ile çalışıyorsanız, gördüğünüz özellikleri burada gösterilen olanlardan farklı olacaktır.
    
     ![][27]
11. Varsayılanları farklı değerler istiyorsanız özelliklerinin değerlerini belirtin. Azure yayımlama özelliklerini bulunan **dağıtım** bölümü.
    
     Kullanılabilir özellikler aşağıdaki tabloda gösterilmektedir **dağıtım** bölümü:
    
    | Özellik | Varsayılan değer |
    | --- | --- |
    | Güvenilmeyen Sertifikalar izin ver |SSL sertifikaları yanlışsa, bir kök yetkilisi tarafından imzalanması gerekir. |
    | Yükseltme izin ver |Yeni bir tane oluşturmak yerine var olan bir dağıtıma güncelleştirmek dağıtım sağlar. IP adresi korur. |
    | Silmeyin |TRUE ise, var olan bir ilgisiz dağıtımını üzerine yazma (yükseltme izin verilir). |
    | Dağıtım ayarları yolu |Depo kök klasörüne göreli bir web uygulaması için .pubxml dosyanızın yolu. Bulut Hizmetleri için yoksayıldı. |
    | SharePoint dağıtım ortamı |Aynı hizmet adı. |
    | Azure dağıtım ortamı |Web uygulaması veya Bulut hizmeti adı. |
12. Birden fazla hizmet yapılandırma (.cscfg dosyaları) kullanıyorsanız, istenen hizmet yapılandırmasında belirtebilirsiniz **MSBuild bağımsız değişkenleri Gelişmiş, yapı** ayarı. Örneğin, ServiceConfiguration.Test.cscfg kullanmak için çizgi seçenek MSBuild bağımsız değişkenleri ayarlayın `/p:TargetProfile=Test`.
    
     ![][38]
    
     Bu zamana kadar yapınızın başarıyla tamamlanmalıdır.
    
     ![][28]
13. Derleme adına çift tıklayın, Visual Studio gösterir. bir **Yapı Özeti**, tüm test sonuçlarını da dahil olmak üzere, birim testi projelerini ilişkilendirilmiş.
    
     ![][29]
14. İçinde [Klasik Azure portalı](http://go.microsoft.com/fwlink/?LinkID=213885), ilişkili dağıtım görüntüleyebilirsiniz **dağıtımları** hazırlık ortamı seçildiğinde sekme.
    
     ![][30]
15. Sitenizin URL'ye gidin. Bir web uygulaması için tıklatmanız **Gözat** komut çubuğundan düğme. Bir bulut hizmeti için URL seçin **Hızlı Bakış** bölümünü **Pano** bir bulut hizmeti için hazırlama ortamını gösteren sayfası. Bulut Hizmetleri için sürekli tümleştirme dağıtımlarından hazırlama ortamına varsayılan olarak yayımlanır. Bu ayarı değiştirebilirsiniz **alternatif bir bulut hizmeti ortamını** özelliğine **üretim**. Bu ekran, site URL'si bulut hizmetin panosu sayfasında nerede olduğunu gösterir.
    
    ![][31]
    
    Çalışan sitenizi ortaya çıkarmak için yeni bir tarayıcı sekmesi açar.
    
    ![][32]
    
    Bulut Hizmetleri için projenize başka değişiklikler yapmak isterseniz, tetikleyici daha oluşturur ve birden çok dağıtım toplanacaktır. En son etkin olarak işaretlenmiş.
    
    ![][33]

## <a name="5-redeploy-an-earlier-build"></a>5: önceki bir yapı yeniden dağıtın
Bu adım isteğe bağlıdır ve bulut Hizmetleri için geçerlidir. Azure Klasik portalında, önceki bir dağıtıma seçin ve ardından **dağıtmanız** önceki bir iade sitenize geri sarma düğmesi.  Bu TFS'de yeni bir derlemeyi tetiklemeyi ve yeni bir giriş dağıtım geçmişiniz oluşturmak, unutmayın.

![][34]

## <a name="6-change-the-production-deployment"></a>6: Üretim dağıtımı değiştirme
Bu adım yalnızca bulut Hizmetleri için web uygulamaları geçerlidir. Hazır olduğunuzda belirleyerek üretim ortamına hazırlama ortamını yükseltebilirsiniz **takas** Klasik Azure portalındaki düğmesi. Yeni dağıtılan hazırlama ortamını üretime yükseltilir ve önceki üretim ortamında, varsa, bir hazırlama ortamını olur. Etkin dağıtım üretim ve hazırlık ortamları için farklı olabilir, ancak son yapılar dağıtım geçmişini ortamı bakılmaksızın aynı olacak.

![][35]

## <a name="7-run-unit-tests"></a>7: birim testleri çalıştırma
Bu adım yalnızca web uygulamaları, bulut olmayan hizmetleri için geçerlidir. Kalite kapısı dağıtımınızı üzerinde koymak için birim testleri çalıştırabilirsiniz ve başarısız olursa, dağıtım durdurabilirsiniz.

1. Visual Studio'da birim testi projesi ekleyin.
   
   ![][39]
2. Proje başvurularını test etmek istediğiniz projeye ekleyin.
   
   ![][40]
3. Bazı birim testleri ekleme. Başlamak için her zaman geçirir kukla bir test deneyin.
   
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
4. Yapı tanımı düzenleme, seçin **işlem** sekmesini tıklatın ve genişletin **Test** düğümü.
5. Ayarlama **başarısız yapı test hatasında** true. Bu testleri geçirmezseniz dağıtım karşılaşılmaz anlamına gelir.
   
   ![][41]
6. Yeni bir derleme sırası.
   
   ![][42]
   
   ![][43]
7. Derleme devam ederken üzerinde ilerleme durumunu denetleyin.
   
    ![][44]
   
    ![][45]
8. Yapı işiniz bittiğinde, test sonuçlarını denetleyin.
   
    ![][46]
   
    ![][47]
9. Başarısız olacak bir test oluşturmayı deneyin. Birinci kopyalayarak yeni bir test eklemek, yeniden adlandırın ve beklenen bir özel durum NotImplementedException olduğunu bildiren kod satırını açıklama.
   
       ```
       [TestMethod]
       //[ExpectedException(typeof(NotImplementedException))]
       public void TestMethod2()
       {
           throw new NotImplementedException();
       }
       ```
10. Yeni bir yapıyı sıraya değişiklik denetleyin.
    
     ![][48]
11. Hata ayrıntılarını görmek için test sonuçlarını görüntüleyin.
    
     ![][49]
    
     ![][50]

## <a name="next-steps"></a>Sonraki adımlar
Birim testi Visual Studio Team Services içinde hakkında daha fazla bilgi için bkz: [birim testleri, derlemede çalıştırılan](http://go.microsoft.com/fwlink/p/?LinkId=510474). Git kullanıyorsanız, bkz: [Git kodunuzda paylaşmak](http://www.visualstudio.com/get-started/share-your-code-in-git-vs.aspx) ve [Azure App Service için sürekli dağıtım](../app-service-web/app-service-continuous-deployment.md).  Visual Studio Team Services hakkında daha fazla bilgi için bkz: [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).

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
