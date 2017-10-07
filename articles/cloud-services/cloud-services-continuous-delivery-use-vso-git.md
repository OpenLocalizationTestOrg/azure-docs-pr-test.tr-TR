---
title: Git ve Azure Visual Studio Team Services ile aaaContinuous teslim | Microsoft Docs
description: "Nasıl tooconfigure toouse Git tooautomatically ve toohello Web uygulamasını Azure App Service veya Bulut hizmetlerini özelliğinde dağıtacak projeleri, Visual Studio Team Services ekip öğrenin."
services: cloud-services
documentationcenter: .net
author: mlearned
manager: douge
editor: 
ms.assetid: 4b3297ef-0de6-4d5f-925c-fcdacc3085ac
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/06/2016
ms.author: mlearned
ms.openlocfilehash: 936c42194f45be55597a77f9a3a6deb4480ed94b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-delivery-tooazure-using-visual-studio-team-services-and-git"></a>Visual Studio Team Services ve Git kullanarak sürekli teslim tooAzure
Visual Studio Team Services ekip projeleri toohost bir Git deposu kaynak kodunuz için kullanabilir ve otomatik olarak oluşturun ve tooAzure web uygulamaları dağıtma veya bir yürütme toohello deposu itme her bulut Hizmetleri.

Visual Studio 2013 ve Azure SDK'sını hello gerekir. Visual Studio 2013 zaten yoksa, hello seçerek karşıdan **ücretsiz olarak başlayın** adresindeki bağlantı [www.visualstudio.com](http://www.visualstudio.com). Yükleme hello Azure SDK [burada](http://go.microsoft.com/fwlink/?LinkId=239540).

> [!NOTE]
> Bu öğretici bir Visual Studio Team Services hesabı toocomplete gerekir: yapabilecekleriniz [ücretsiz bir Visual Studio Team Services hesabı açabilirsiniz](http://go.microsoft.com/fwlink/p/?LinkId=512979).
> 
> 

bir bulut hizmeti tooautomatically yukarı tooset derleme ve Visual Studio Team Services kullanarak tooAzure dağıtma, şu adımları izleyin.

## <a name="1-create-a-git-repository"></a>1: bir Git deposu oluşturma
1. Visual Studio Team Services hesabı zaten yoksa, edinebilirsiniz [burada](http://go.microsoft.com/fwlink/?LinkId=397665). Takım projesi oluşturduğunuzda, Git kaynak denetim sisteminiz seçin. Merhaba yönergeleri tooconnect Visual Studio tooyour takım projesi izleyin.
2. İçinde **Takım Gezgini**, hello seçin **bu depoyu kopyalayın** bağlantı.
   
    ![][3]
3. Merhaba yerel kopyasını Hello konumunu belirtin ve ardından hello **kopya** düğmesi.

## <a name="2-create-a-project-and-commit-it-toohello-repository"></a>2: Proje oluşturma ve toohello depo yürütme
1. İçinde **Takım Gezgini**, hello içinde **çözümleri** bölümünde, hello seçin **yeni** toocreate yeni bir proje hello yerel deposu ile bağlantı.
   
    ![][4]
2. Bir web uygulaması dağıtma veya Bulut hizmeti (Azure uygulaması) aşağıdaki hello tarafından bu izlenecek adımları. Yeni bir Azure bulut hizmeti projesi ya da yeni bir ASP.NET MVC projesi oluşturun. Sonraki veya hello Proje hedefleri .NET Framework 4 hello emin olun. Bir bulut hizmeti projesini oluşturuyorsanız, bir ASP.NET MVC web rolü ve çalışan rolü ekleyin.
   Bir web uygulaması toocreate istiyorsanız, hello tercih **ASP.NET Web uygulaması** proje şablonu ve ardından **MVC**. Bkz: [Azure App Service'te bir ASP.NET web uygulaması oluşturma](../app-service-web/app-service-web-get-started-dotnet.md) daha fazla bilgi için.
3. Merhaba çözüm hello kısayol menüsünü açın ve seçin **yürütme**.
   
    ![][7]
4. Bu hello Git Visual Studio Team Services içinde kullanmış olduğunuz ilk kez kullanıyorsanız, tooprovide bazı bilgileri tooidentify kendiniz Git içinde ihtiyacınız vardır. Merhaba, **bekleyen değişiklikleri** alanı **Takım Gezgini**, kullanıcı adınızı girin ve e-posta adresi. Merhaba yürütülmesi için bir açıklama girin ve ardından hello **tamamlama** düğmesi.
   
    ![][8]
5. Merhaba seçenekleri tooinclude dikkat edin veya belirli değişiklikleri, iade ettiğinizde dışlayın. Merhaba, değişirse istediğiniz dışlanır, seçin **dahil tüm**.
6. Yerel hello deposu kopyanızda taahhüt hello değişiklikleri şimdi seçtiğiniz. Ardından, hello seçerek değişiklikleri hello server ile eşitleme **eşitleme** bağlantı.

## <a name="3-connect-hello-project-tooazure"></a>3: hello proje tooAzure Bağlan
1. Bazı kaynak kodu ile Visual Studio Team Services bir Git deposu var, hazır tooconnect olan git deposu tooAzure.  Merhaba, [Klasik Azure portalı](http://go.microsoft.com/fwlink/?LinkID=213885), bulut hizmeti veya web uygulamanızı seçin veya hello + sol hello alt ve seçme simgesini seçerek yeni bir tane oluşturun **bulut hizmeti** veya **Web uygulaması**ve ardından **hızlı Oluştur**.
   
    ![][9]
2. Bulut Hizmetleri için hello seçin **Visual Studio Team Services ile yayımlamayı ayarlayın** bağlantı. Web uygulamaları için hello seçin **kaynak denetiminden dağıtım Ayarla** bağlantı.
   
    ![][10]
3. Merhaba sihirbazında, Visual Studio Team Services hesabınızın adını hello hello metin kutusuna yazın ve hello **şimdi Yetkilendir** bağlantı. İçinde toosign istenebilir.
   
    ![][11]
4. Merhaba, **bağlantı isteği** açılan iletişim kutusunda, seçin **kabul** tooauthorize ekibinizin proje Visual Studio Team Services içinde Azure tooconfigure.
   
    ![][12]
5. Yetkilendirme başarılı olduktan sonra Visual Studio Team Services takım projeleriniz içeren bir açılır liste bakın.  Merhaba önceki adımlarda oluşturduğunuz takım projesi Hello adını seçin ve hello sihirbazın onay düğmesini seçin.
   
    ![][13]
   
    Merhaba yürütme tooyour depo, Visual Studio Team Services itme sonraki sefer yapı ve proje tooAzure dağıtın.

## <a name="4-trigger-a-rebuild-and-redeploy-your-project"></a>4: yeniden tetikleyebilir ve projenizi yeniden dağıtmak
1. Visual Studio'da bir dosyasını açın ve onu değiştirin. Örneğin, hello dosya değişiklik `_Layout.cshtml` hello görünümleri altında\\paylaşılan klasöründe bir MVC web rolü.
   
    ![][17]
2. Hello site için Hello altbilgi metni düzenleyin ve hello dosyasını kaydedin.
   
    ![][18]
3. İçinde **Çözüm Gezgini**hello çözüm düğümü, proje düğümüne veya hello dosya için değiştirdiğiniz hello kısayol menüsünü açın ve ardından **yürütme**.
4. Bir yorum yazın ve seçin **yürütme**.
   
    ![][20]
5. Merhaba seçin **eşitleme** bağlantı.
   
    ![][38]
6. Merhaba seçin **anında** toopush Visual Studio Team Services yürütme toohello deponuza bağlayın. (Merhaba de kullanabilirsiniz **eşitleme** toocopy işlemeleri toohello deponuz düğmesi. Merhaba fark vardır **eşitleme** çeken hello depodan en son değişiklikleri de hello.)
   
    ![][39]
7. Merhaba seçin **ev** düğmesini tooreturn toohello **Takım Gezgini** giriş sayfası.
   
    ![][21]
8. Seçin **derlemeler** tooview hello derlemeler sürüyor.
   
    ![][22]
   
    **Takım Gezgini** bir yapı için iade tetiklenen gösterir.
   
    ![][23]
9. tooview ayrıntılı günlüğü hello yapı olarak ilerledikçe, devam eden hello yapı hello adını çift.
10. Merhaba derleme sürüyor olsa da, Başlangıç Sihirbazı toolink tooAzure kullanıldığında, oluşturulan hello derleme tanımı göz atın.  Merhaba derleme tanımı için hello kısayol menüsünü açın ve seçin **derleme tanımını Düzenle**.
    
    ![][25]
11. Merhaba, **tetikleyici** sekmesinde hello derleme tanımı toobuild her iade, varsayılan olarak ayarlandığını görürsünüz. (Bir bulut hizmeti için Visual Studio Team Services oluşturur ve ortam otomatik olarak hazırlama hello ana dala toohello dağıtır. El ile adım toodeploy toohello Canlı site toodo etmesi gerekir. Ortamı hazırlama sahip olmayan bir web uygulaması için toohello Canlı doğrudan site hello ana dala dağıtır.
    
    ![][26]
12. Merhaba, **işlem** sekmesinde, bulut hizmeti veya web uygulamasının adını toohello hello dağıtım ortamı ayarlayın görebilirsiniz.
    
     ![][27]
13. Merhaba Varsayılanları farklı değerler istiyorsanız hello özelliklerinin değerlerini belirtin. Hello Azure yayımlama hello özelliklerdir **dağıtım** bölümü ve ayrıca gerekebilir tooset MSBuild parametreleri. Örneğin, bir bulut hizmeti projesini toospecify "Bulut" dışında bir hizmet yapılandırması hello MSbuild parametreler çok kümesindeki`/p:TargetProfile=[YourProfile]` nerede *[YourProfile]* hizmet yapılandırma dosyası gibi bir ad ile eşleşir ServiceConfiguration. *YourProfile*.cscfg.
    
     Merhaba aşağıdaki tabloda hello kullanılabilir özellikler hello gösterilmektedir **dağıtım** bölümü:
    
    | Özellik | Varsayılan değer |
    | --- | --- |
    | Güvenilmeyen Sertifikalar izin ver |SSL sertifikaları yanlışsa, bir kök yetkilisi tarafından imzalanması gerekir. |
    | Yükseltme izin ver |Merhaba dağıtım tooupdate yeni bir tane oluşturmak yerine var olan bir dağıtımını sağlar. Başlangıç IP adresi korur. |
    | Silmeyin |TRUE ise, var olan bir ilgisiz dağıtımını üzerine yazma (yükseltme izin verilir). |
    | Yol tooDeployment ayarları |Merhaba yol tooyour .pubxml dosya hello depodaki göreli toohello kök klasöründe bir web uygulaması için. Bulut Hizmetleri için yoksayıldı. |
    | SharePoint dağıtım ortamı |aynı hello hizmet adı olarak hello. |
    | Azure dağıtım ortamı |Merhaba web uygulaması veya Bulut hizmeti adı. |
14. Bu zamana kadar yapınızın başarıyla tamamlanmalıdır.
    
     ![][28]
15. Merhaba derleme adına çift tıklayın, Visual Studio gösterir. bir **Yapı Özeti**, tüm test sonuçlarını da dahil olmak üzere, birim testi projelerini ilişkilendirilmiş.
    
     ![][29]
16. Merhaba, [Klasik Azure portalı](http://go.microsoft.com/fwlink/?LinkID=213885), ilişkili hello dağıtım üzerinde hello görüntüleyebilirsiniz **dağıtımları** ortam hazırlama hello seçildiğinde sekme.
    
     ![][30]
17. Tooyour sitenin URL'sini göz atın. Bir web uygulaması için yalnızca hello seçme **Gözat** hello portalda düğmesine. Bir bulut hizmeti için hello URL'si hello seçin **Hızlı Bakış** hello bölümünü **Pano** hello hazırlama ortamını gösteren sayfası.
    
    Bulut Hizmetleri için sürekli tümleştirme dağıtımlarından yayımlanan toohello hazırlama ortamını varsayılan olarak ' dir. Bu ayarı hello tarafından değiştirebilirsiniz **alternatif bir bulut hizmeti ortamını** özelliği çok**üretim**. İşte hello site URL'si hello bulut hizmetin panosu sayfasında olduğu.
    
    ![][31]
    
    Yeni bir tarayıcı sekmesi tooreveal çalışan sitenizi açılır.
    
    ![][32]
18. Yaptığınız diğer tooyour proje değişikliklerini, tetikleyici daha oluşturur ve birden çok dağıtım toplanacaktır. Etkin olarak işaretli olduğundan hello son.
    
    ![][33]

## <a name="5-redeploy-an-earlier-build"></a>5: önceki bir yapı yeniden dağıtın
Bu adım isteğe bağlıdır. Klasik Azure portalı Merhaba, önceki bir dağıtıma seçin ve seçin **dağıtmanız** toorewind, site tooan önceki iade etme. Bu TFS'de yeni bir derlemeyi tetiklemeyi ve yeni bir giriş dağıtım geçmişiniz oluşturmak, unutmayın.

![][34]

## <a name="6-change-hello-production-deployment"></a>6: hello Üretim dağıtımı değiştirme
Hazır olduğunuzda seçerek hello hazırlama ortamı toohello üretim ortamını yükseltebilirsiniz **takas** hello Klasik Azure Portalı'nda. Yeni dağıtılan hello hazırlama ortamıdır yükseltilen tooProduction ve hello önceki üretim ortamında, varsa, bir hazırlama ortamını olur. Hello etkin dağıtım hello üretim ve hazırlama ortamları için farklı olabilir, ancak son yapılar hello dağıtım geçmişini olduğu hello aynı ne olursa olsun, ortam.

![][35]

## <a name="7-deploy-from-a-working-branch"></a>7: bir çalışma dalı dağıtın.
Git kullandığınızda, genellikle bir çalışma dalı değişiklikleri yapın ve geliştirme tamamlanmış durumuna ulaştığında hello ana dala tümleştirebilirsiniz. Merhaba geliştirme aşamasında bir proje toobuild istediğiniz ve hello çalışma dalı tooAzure dağıtın.

1. İçinde **Takım Gezgini**, hello seçin **giriş** düğmesine ve ardından hello **dalları** düğmesi.
   
    ![][40]
2. Merhaba seçin **dalı** bağlantı.
   
    ![][41]
3. "Çalışıyor" gibi hello dalın Hello adı girin ve seçin **oluşturma şube**. Bu, yeni bir yerel dalı oluşturur.
   
    ![][42]
4. Merhaba şube yayımlayın. Merhaba şube adlarında seçin **yayımlanmamış dalları**ve seçin **Yayımla**.
   
    ![][44]
5. Varsayılan olarak, yalnızca toohello ana dala tetikleyici sürekli bir yapı değiştirir. bir çalışma dalı için sürekli derlemesi tooset seçin hello **derlemeler** sayfasındaki **Takım Gezgini**ve seçin **derleme tanımını Düzenle**.
6. Açık hello **kaynak ayarları** sekmesi. Altında **izlenen dalları sürekli tümleştirme ve yapı**, seçin **tooadd yeni bir satır burayı**.
   
    ![][47]
7. Uyarı/refs/çalışma gibi oluşturulan hello şube belirtin.
   
    ![][48]
8. Hello kodda, açık hello kısayol menüsünü hello değiştirilen dosya için bir değişiklik yapın ve ardından **yürütme**.
   
    ![][43]
9. Merhaba seçin **eşitlenmemiş işlemeleri** hello seçin ve bağlama **eşitleme** düğmesini veya hello **anında** bağlantı toocopy hello hello çalışma dalı Visual Studio'da toohello kopyasını değiştirir Team Services.
   
   ![][45]
10. Toohello gidin **derlemeler** görüntülemek ve hemen tetiklenen hello yapı hello çalışma dalı için bulabilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar
Git Visual Studio Team Services ile kullanma hakkında daha fazla ipucu toolearn bkz [geliştirme ve Visual Studio kullanarak Git kodunuzda paylaşmak](https://www.visualstudio.com/en-us/docs/git/share-your-code-in-git-vs-2017) ve Visual Studio Team Services toopublish tarafından yönetilmeyen bir Git deposu kullanma hakkında bilgi için tooAzure, bkz: [sürekli dağıtım tooAzure uygulama hizmeti](../app-service-web/app-service-continuous-deployment.md). Visual Studio Team Services hakkında daha fazla bilgi için bkz: [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).

[0]: ./media/cloud-services-continuous-delivery-use-vso/tfs0.PNG
[1]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateTeamProjectInGit.PNG
[2]: ./media/cloud-services-continuous-delivery-use-vso/tfs2.png
[3]: ./media/cloud-services-continuous-delivery-use-vso-git/CloneThisRepository.PNG
[4]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateNewSolutionInClonedRepo.PNG
[7]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitMenuItem.PNG
[8]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitAChange2.PNG
[9]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateCloudService.PNG
[10]: ./media/cloud-services-continuous-delivery-use-vso-git/SetUpPublishingWithVSO.PNG
[11]: ./media/cloud-services-continuous-delivery-use-vso-git/AuthorizeConnection.PNG
[12]: ./media/cloud-services-continuous-delivery-use-vso-git/ConnectionRequest.PNG
[13]: ./media/cloud-services-continuous-delivery-use-vso-git/ChooseARepo3.PNG
[14]: ./media/cloud-services-continuous-delivery-use-vso/tfs14.png
[15]: ./media/cloud-services-continuous-delivery-use-vso/tfs15.png
[16]: ./media/cloud-services-continuous-delivery-use-vso/tfs16.png
[17]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs17.png
[18]: ./media/cloud-services-continuous-delivery-use-vso-git/MakeACodeChange.PNG
[20]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitAChange2.PNG
[21]: ./media/cloud-services-continuous-delivery-use-vso-git/TeamExplorerHome.png
[22]: ./media/cloud-services-continuous-delivery-use-vso-git/TeamExplorerBuilds.PNG
[23]: ./media/cloud-services-continuous-delivery-use-vso-git/BuildInQueue.png
[24]: ./media/cloud-services-continuous-delivery-use-vso/tfs24.png
[25]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs25.png
[26]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs26.png
[27]: ./media/cloud-services-continuous-delivery-use-vso-git/ProcessTab.PNG
[28]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs28.png
[29]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs29.png
[30]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs30.png
[31]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs31.png
[32]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs32.png
[33]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs33.png
[34]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs34.png
[35]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs35.png
[36]: ./media/cloud-services-continuous-delivery-use-vso/tfs36.PNG
[37]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateANewAccount.PNG
[38]: ./media/cloud-services-continuous-delivery-use-vso-git/SyncChanges2.PNG
[39]: ./media/cloud-services-continuous-delivery-use-vso-git/PushCurrentBranch.PNG
[40]: ./media/cloud-services-continuous-delivery-use-vso-git/BranchesInTeamExplorer.PNG
[41]: ./media/cloud-services-continuous-delivery-use-vso-git/NewBranch.PNG
[42]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateBranch.PNG
[43]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitAChange2.PNG
[44]: ./media/cloud-services-continuous-delivery-use-vso-git/PublishBranch.PNG
[45]: ./media/cloud-services-continuous-delivery-use-vso-git/SyncChanges2.PNG
[47]: ./media/cloud-services-continuous-delivery-use-vso-git/SourceSettingsPage.PNG
[48]: ./media/cloud-services-continuous-delivery-use-vso-git/IncludeWorkingBranch.PNG
