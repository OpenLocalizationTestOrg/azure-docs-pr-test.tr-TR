---
title: "Azure App Service ile Çevik Yazılım Geliştirme"
description: "Çevik Yazılım Geliştirme destekleyen bir şekilde Azure App Service ile yüksek ölçekli karmaşık uygulamaları oluşturmayı öğrenin."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: c0fdb676-36a6-4738-925f-65b4835d187f
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/01/2016
ms.author: cephalin
ms.openlocfilehash: 5ed888cbb422766cf2094f5980dfd1c599bd431c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="agile-software-development-with-azure-app-service"></a>Azure App Service ile Çevik Yazılım Geliştirme
Bu öğreticide, ile yüksek ölçekli karmaşık uygulamalarının nasıl oluşturulacağını öğreneceksiniz [Azure App Service](/azure/app-service/) destekler şekilde [Çevik Yazılım Geliştirme](https://en.wikipedia.org/wiki/Agile_software_development). Zaten bildiğinizi varsayar nasıl [beklendiği Azure karmaşık uygulamalar dağıtmak](app-service-deploy-complex-application-predictably.md).

Teknik işlemlerde sınırlamaları genellikle uygulamasının başarılı çevik yöntemlerden in the way of bildirimde bulunabilir. Azure uygulama hizmeti gibi özelliklerle [sürekli yayımlama](app-service-continuous-deployment.md), [hazırlık ortamları](web-sites-staged-publishing.md) (yuvası) ve [izleme](web-sites-monitor.md)akıllıca düzenlemesini bağlı olduğunda, ve dağıtımda yönetimini [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md), Çevik Yazılım Geliştirme çekirdeğin geliştiriciler için harika bir çözümdür parçası olabilir.

Aşağıdaki tabloda Çevik Geliştirme ile ilgili gereksinimler kısa listesidir ve Azure Hizmetleri bunların her birini etkinleştirmek nasıl.

| Gereksinim | Azure nasıl sağlar |
| --- | --- |
| -Her işleme ile derleme<br>-Otomatik olarak oluşturabilir ve hızlı |Sürekli dağıtımı ile yapılandırıldığında, Azure App Service geliştirme şubeyi temel alarak Canlı çalışan derlemeleri olarak işlev görebilir. Kod dala gönderilen her zaman otomatik olarak oluşturulan ve Azure çalışan Canlı. |
| -Kendi kendine test yapma derlemeler |Yük testleri, web testleri, vb., Azure Resource Manager şablonu ile dağıtılabilir. |
| -Üretim ortamında bir kopyasını testleri gerçekleştirme |Azure Resource Manager şablonları kopyalarını hızla ve öngörülebilir bir şekilde test (uygulama ayarları, bağlantı dizesi şablonları, ölçekleme, vb. dahil) Azure üretim ortamı oluşturmak için kullanılabilir. |
| -En son derleme sonucu kolayca görüntüleme |Azure için sürekli dağıtım bir depodan değişikliklerinizi uygulamak hemen sonra canlı bir uygulamada yeni kod test edebilirsiniz anlamına gelir. |
| -Her gün ana dala Yürüt<br>-Dağıtımı otomatik hale getir |Bir deponun ana dala olan üretim uygulama sürekli tümleştirme her yürütme/merge ana dala üretim için otomatik olarak dağıtır. |

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="what-you-will-do"></a>Ne yapacağını
Yeni değişiklikler yayımlamak için normal bir test aşaması üretim geliştirme iş akışı yükselteceğinizi [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) iki oluşur örnek uygulama [web uygulamaları](/services/app-service/web/), bir ön uç (FE) olması ve başka bir Web API arka uç (BE) olan ve bir [SQL veritabanı](/services/sql-database/). Aşağıdaki dağıtım mimarisi ile çalışır:

![](./media/app-service-agile-software-development/what-1-architecture.png)

Resmi sözcükler halinde yerine koymak için:

* Dağıtım mimarisi üç ayrı ortamlara ayrılmış (veya [kaynak grupları](../azure-resource-manager/resource-group-overview.md) azure'da), her biri kendi [uygulama hizmeti planı](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md), [ölçeklendirme](web-sites-scale.md) ayarları ve SQL veritabanı. 
* Her ortam ayrı olarak yönetilebilir. Bunlar, hatta farklı Aboneliklerde bulunabilir.
* Hazırlama ve üretim aynı App Service uygulaması iki yuvası uygulanır. Ana dala hazırlama yuvası ile sürekli tümleştirme için ayarlanır.
* Ana dal için bir kaydetme, hazırlama yuvası (üretim verileriyle) doğrulandığında, doğrulanmış hazırlama uygulamayı üretim yuvasına [kapalı kalma süresi olmadan](web-sites-staged-publishing.md).

Üretim ve hazırlama ortamına şablon tarafından tanımlanan [  *&lt;repository_root >*/ARMTemplates/ProdandStage.json](https://github.com/azure-appservice-samples/ToDoApp/blob/master/ARMTemplates/ProdAndStage.json).

Geliştirme ve test ortamları şablon tarafından tanımlanan [  *&lt;repository_root >*/ARMTemplates/Dev.json](https://github.com/azure-appservice-samples/ToDoApp/blob/master/ARMTemplates/Dev.json).

Test şube kadar geliştirme şube sonra (kalite speak kadar çok yukarı taşınması) ana dala geçiş koduyla tipik dallanma strateji de kullanır.

![](./media/app-service-agile-software-development/what-2-branches.png) 

## <a name="what-you-need"></a>Ne gerekiyor
* Bir Azure hesabı
* A [GitHub](https://github.com/) hesabı
* Git Kabuğu (yüklenmiş [Windows için GitHub](https://windows.github.com/))-aynı oturum Git ve PowerShell komutlarını çalıştırmanıza olanak sağlar 
* En son [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps) BITS
* Temel anlamak için aşağıdaki araçlardan birini:
  * [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) şablon dağıtımı (Ayrıca bkz. [beklendiği azure'da karmaşık bir uygulama dağıtmak](app-service-deploy-complex-application-predictably.md))
  * [Git](http://git-scm.com/documentation)
  * [PowerShell](https://technet.microsoft.com/library/bb978526.aspx)

> [!NOTE]
> Bu öğreticiyi tamamlamak için bir Azure hesabınızın olması gerekir:
> 
> * Yapabilecekleriniz [ücretsiz bir Azure hesabı açabilirsiniz](https://azure.microsoft.com/pricing/free-trial/) -krediler alırsınız, ücretli Azure hizmetlerini denemek için kullanabileceğiniz ve bunlar bitmiş bile hesabı sürdürebilir ve ücretsiz Web uygulamaları gibi Azure hizmetlerini kullanabilirsiniz.
> * Yapabilecekleriniz [Visual Studio abone Avantajlarınızı etkinleştirebilir](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) -bilgisayarınızı Visual Studio abonelik size kredi verir Ücretli Azure hizmetlerinizi kullanabildiğiniz her ay.
> 
> Azure hesabı için kaydolmadan önce Azure App Service’i kullanmaya başlamak isterseniz, App Service’te hemen kısa süreli bir başlangıç web uygulaması oluşturabileceğiniz [App Service’i Deneyin](https://azure.microsoft.com/try/app-service/) sayfasına gidin. Kredi kartı ve taahhüt gerekmez.
> 
> 

## <a name="set-up-your-production-environment"></a>Üretim ortamınızı ayarlama
> [!NOTE]
> Bu öğreticide otomatik olarak kullanılan komut dosyası, GitHub deposunu sürekli yayımlama yapılandırır. Bu, GitHub kimlik bilgilerinizi zaten Azure, aksi takdirde komut dosyalı dağıtım web uygulamaları için kaynak denetim ayarları yapılandırmak çalışırken başarısız saklanacağını gerektirir. 
> 
> Azure'da GitHub kimlik bilgilerinizi depolamak için bir web uygulaması oluşturmak [Azure portal](https://portal.azure.com/) ve [GitHub dağıtımını yapılandırma](app-service-continuous-deployment.md). Yalnızca bu kez yapmanız gerekir. 
> 
> 

Tipik bir DevOps senaryo azure'da çalışan bir uygulamanız varsa ve kullanarak sürekli yayımlama değişiklik istiyor. Bu senaryoda, geliştirilmiş, test ve üretim ortamında dağıtmak için kullanılan bir şablon vardır. Bu bölümde kurar.

1. Kendi çatalı oluşturma [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) deposu. Çatalı oluşturma hakkında daha fazla bilgi için bkz: [bir depoyu Çatallaştırma](https://help.github.com/articles/fork-a-repo/). Çatalı oluşturulduktan sonra tarayıcınızı görebilirsiniz.
   
    ![](./media/app-service-agile-software-development/production-1-private-repo.png)
2. Git kabuk oturumu açın. Git Kabuk henüz yoksa, yükleme [Windows için GitHub](https://windows.github.com/) şimdi.
3. Aşağıdaki komutu çalıştırarak, çatalı yerel bir kopyasını oluşturun:

        git clone https://github.com/<your_fork>/ToDoApp.git 
4. Yerel kopya oluşturduktan sonra gidin  *&lt;repository_root >*\ARMTemplates ve deploy.ps1 komut aşağıdaki gibi çalıştırın:
   
        .\deploy.ps1 –RepoUrl https://github.com/<your_fork>/todoapp.git
5. İstendiğinde, istenilen kullanıcı adı ve veritabanı erişimi için parolayı yazın.
   
   Çeşitli Azure kaynaklarını hazırlama sürecini görmeniz gerekir. Dağıtım tamamlandığında, komut dosyası tarayıcıda uygulama başlatır ve kolay bip sesi verin.
   
    ![](./media/app-service-agile-software-development/production-2-app-in-browser.png)
   
   > [!TIP]
   > Bir göz atalım  *&lt;repository_root >*nasıl benzersiz kimlikler kaynaklarla oluşturur görmek için \ARMTemplates\Deploy.ps1. Çakışan kaynak adları hakkında endişelenmeden klonlar aynı dağıtım oluşturmak için aynı yaklaşımı kullanın.
   > 
   > 
6. Geri Git Kabuk oturumunuzda çalıştırın:
   
        .\swap –Name ToDoApp<unique_string>master
   
    ![](./media/app-service-agile-software-development/production-4-swap.png)
7. Komut tamamlandığında, ön uç'ın adresine göz atın dönün (http://ToDoApp*&lt;unique_string >*master.azurewebsites.net/) üretimde çalışan uygulama görmek için.
8. Oturum [Azure portal](https://portal.azure.com/) ve ne oluşturulan bir göz atalım.
   
   Aynı kaynak grubunda biriyle iki web uygulamaları görmeye olmalıdır `Api` adı soneki. Kaynak grubu görünümü bakarsanız, SQL veritabanı ve sunucu, uygulama hizmeti planı ve hazırlık yuvaları web uygulamaları için Ayrıca bkz. Farklı kaynaklara göz atın ve bunlarla karşılaştırmak  *&lt;repository_root >*\ARMTemplates\ProdAndStage.json şablonda nasıl yapılandırıldıklarına bakın.
   
    ![](./media/app-service-agile-software-development/production-3-resource-group-view.png)

Artık üretim ortamını ayarlamanız gerekir. Ardından, uygulama için yeni bir güncelleştirme kapalı tetiklersiniz.

## <a name="create-dev-and-test-branches"></a>Geliştirici oluşturma ve dalları sınama
Azure'da üretimde çalışan karmaşık bir uygulamaya sahip olduğunuza göre uygulamanıza çevik yöntem uygun bir güncelleştirme hale getirir. Bu bölümde, geliştirici oluşturma ve gerekli güncelleştirmeleri yapmanız gerekecektir dalları sınayın.

1. Sınama ortamı ilk oluşturun. Git Kabuk oturumunuzda adlı yeni bir dal için bir ortam oluşturmak için aşağıdaki komutları çalıştırın **NewUpdate**. 
   
        git checkout -b NewUpdate
        git push origin NewUpdate 
        .\deploy.ps1 -TemplateFile .\Dev.json -RepoUrl https://github.com/<your_fork>/ToDoApp.git -Branch NewUpdate
2. İstendiğinde, istenilen kullanıcı adı ve veritabanı erişimi için parolayı yazın. 
   
   Dağıtım tamamlandığında, komut dosyası tarayıcıda uygulama başlatır ve kolay bip sesi verin. Artık kendi test ortamı ile yeni bir dalı var. Bu test ortamı hakkında birkaç şey gözden geçirmek için bir dakikanızı ayırın:
   
   * Tüm Azure aboneliklerinden oluşturabilirsiniz. Üretim ortamında test ortamınızdan ayrı olarak yönetilebilir anlamına gelir.
   * Test ortamınızı Azure'da Canlı çalışıyor.
   * Sınama ortamınızda, üretim ortamında, hazırlama yuvaları ve ölçeklendirme ayarlarını dışında aynıdır. ProdandStage.json ve Dev.json arasındaki tek fark, olduklarından bildirin.
   * Farklı fiyat katmanı ile kendi uygulama hizmeti planındaki test ortamınızı yönetmek (gibi **serbest**).
   * Bu test ortamı silinmesi, kaynak grubunun silinmesi kadar basittir. Bunun nasıl bulacaksınız [daha sonra](#delete).
3. Aşağıdaki komutları çalıştırarak bir geliştirme dalı oluşturmak için geçin:
   
        git checkout -b Dev
        git push origin Dev
        .\deploy.ps1 -TemplateFile .\Dev.json -RepoUrl https://github.com/<your_fork>/ToDoApp.git -Branch Dev
4. İstendiğinde, istenilen kullanıcı adı ve veritabanı erişimi için parolayı yazın. 
   
   Bu geliştirme ortamı hakkında birkaç şey gözden geçirmek için bir dakikanızı ayırın: 
   
   * Aynı şablon kullanılarak dağıtıldığı için geliştirme ortamınızı yapılandırma sınama ortamında aynı vardır.
   * Her bir geliştirme ortamı ayrı olarak yönetilmesi için test ortamını bırakarak geliştiricinin kendi Azure aboneliğindeki oluşturulabilir.
   * Geliştirme ortamınız ile Azure Canlı çalışıyor.
   * Geliştirme ortamı siliniyor, kaynak grubunun silinmesi kadar basittir. Bunun nasıl bulacaksınız [daha sonra](#delete).

> [!NOTE]
> Yeni güncelleştirmeye çalışan birden çok geliştiriciler varsa, bunların her birini kolayca dal ve ayrılmış geliştirme ortamı aşağıdaki adımlarla oluşturabilirsiniz:
> 
> 1. Github'da kendi çatalı depo oluşturma (bkz [bir depoyu Çatallaştırma](https://help.github.com/articles/fork-a-repo/)).
> 2. Kendi yerel makinedeki çatalı kopyalama
> 3. Kendi geliştirme şube ve ortam oluşturmak için aynı komutları çalıştırın.
> 
> 

İşiniz bittiğinde, GitHub çatalı üç dalları olmalıdır:

![](./media/app-service-agile-software-development/test-1-github-view.png)

Ve altı web uygulamaları (iki üç kümeleri) üç ayrı kaynak grubunda olması gerekir:

![](./media/app-service-agile-software-development/test-2-all-webapps.png)

> [!NOTE]
> ProdandStage.json belirtir kullanmak üzere üretim ortamına **standart** fiyatlandırma üretim uygulama ölçeklenebilirlik için uygun olan katmanı.
> 
> 

## <a name="build-and-test-every-commit"></a>Derleme ve test her işleme
Şablon dosyalarını ProdAndStage.json ve Dev.json zaten varsayılan web uygulaması için yayımlama sürekli ayarlayan kaynak denetim parametrelerini belirtin. Bu nedenle, her işleme GitHub dal, bir otomatik dağıtım için Azure o daldan tetikler. Kurulumunuzu şimdi işleyişi görelim.

1. Yerel deposu geliştirme dalı olduğunuzdan emin olun. Bunu yapmak için Git Kabuğu'nda aşağıdaki komutu çalıştırın:
   
        git checkout Dev
2. Bir uygulamanın UI katmana kullanılacak kodunu değiştirerek değişiklik [önyükleme](http://getbootstrap.com/components/) listeler. Açık  *&lt;repository_root >*\src\MultiChannelToDo.Web\index.cshtml ve marka vurgulanmış şu değiştirin:
   
    ![](./media/app-service-agile-software-development/commit-1-changes.png)
   
    > [!NOTE]
    > Önceki görüntünün okuyamadığında: 
    > 
    > * Satır 18'de, değiştirme `check-list` için `list-group`.
    > * 19. satırda değiştirme `class="check-list-item"` için `class="list-group-item"`.
    > 
    > 
3. Yaptığınız değişikliği kaydedin. Geri Git Kabuğu'nda aşağıdaki komutları çalıştırın:
   
        cd <repository_root>
        git add .
        git commit -m "changed to bootstrap style"
        git push origin Dev
   
   Bu git komutları "kodunuzda TFS gibi başka bir kaynak denetimi sistemindeki denetim için" benzerdir. Çalıştırdığınızda `git push`, otomatik bir kodun uygulamayı geliştirme ortamında değişikliği yansıtacak şekilde yeniden oluşturur Azure yeni tamamlama tetikler.
4. Bu kodun geliştirme ortamınıza oluştuğunu doğrulamak için geliştirme ortamı web uygulaması sayfasına gidin ve bakmak **dağıtım** bölümü. En son, yürütme iletinizi görebilmeniz gerekir.
   
    ![](./media/app-service-agile-software-development/commit-2-deployed.png)
5. Buradan, tıklatın **Gözat** Azure Canlı uygulamada yeni değişikliği görmek için.
   
    ![](./media/app-service-agile-software-development/commit-3-webapp-in-browser.png)
   
   Uygulama için ikincil bir değişikliktir. Bununla birlikte, çoğu kez bir karmaşık web uygulaması için yeni değişiklikler sahip istenmeyen ve istenmeyen yan etkiler. Her işleme dinamik derlemelerde kolayca test yapamamasına görebileceği, müşterilerinizin önce bu sorunların catch olanak tanır.

Artık, gerçekleştirme ile rahat olmalıdır, yer alan bir geliştirici olarak **NewUpdate** proje, kendiniz için geliştirme ortamı oluşturmak daha sonra her işleme yapı ve her yapı test.

## <a name="merge-code-into-test-environment"></a>Kodu test ortamına Birleştir
Bu, geliştirici şube NewUpdate şube kadar gelen kodunuzu göndermek hazır olduğunuzda, standart git işlemdir:

1. GitHub, Geliştirme dalında diğer geliştiriciler tarafından oluşturulan yürütme gibi tüm yeni tamamlama NewUpdate birleştirin. Herhangi yeni bir kodun GitHub tetikleyiciler, yürütme ve geliştirme ortamında oluşturun. Ardından kodunuzu geliştirme dal hala NewUpdate şube son bitten çalışır emin olabilirsiniz.
2. Github'da NewUpdate şube geliştirme şube gelen tüm yeni işlemeleri birleştirin. Bu eylem bir kodun ve test ortamında yapı tetikler. 

Not sürekli dağıtım zaten bu git dal ayarlandığından, tümleştirme çalıştıran gibi diğer herhangi bir eylemde bulunmanız gerekmez yeniden oluşturur. Standart kaynak denetimi yöntemler git kullanarak gerçekleştirmek yeterlidir ve Azure tüm oluşturma işlemlerini sizin için gerçekleştirir.

Şimdi, şimdi kodunuzu anında **NewUpdate** dal. Git Kabuğu'nda aşağıdaki komutları çalıştırın:

    git checkout NewUpdate
    git pull origin NewUpdate
    git merge Dev
    git push origin NewUpdate

Bu kadar! 

Şimdi sınama ortamında gönderilen (NewUpdate dala birleştirilmiş), yeni tamamlama görmek test ortamınız için web uygulaması sayfasına gidin. Ardından **Gözat** stil değişikliği artık azure'da çalıştığını görmek için.

## <a name="deploy-update-to-production"></a>Güncelleştirme üretime dağıtma
Hazırlama ve üretim ortamına kod Ftp'den test ortamına kod basıldığında ne zaten yaptığınızı daha farklı geliyor olmalıdır. Gerçekten bu basit bir işlemdir. 

Git Kabuğu'nda aşağıdaki komutları çalıştırın:

    git checkout master
    git pull origin master
    git merge NewUpdate
    git push origin master

Hazırlama ve üretim ortamı ayarlandığından içinde ProdandStage.json biçimini temel unutmayın, yeni kodunuz için gönderilen **hazırlama** yuva ve orada çalışıyor. Bu nedenle hazırlama yuvanın URL'sine gidin, var. çalışan yeni kodu konusuna bakın. Bunu yapmak için Git Kabuğu'nda aşağıdaki cmdlet'i çalıştırın.

    Start-Process -FilePath "http://ToDoApp<unique_string>master-Staging.azurewebsites.net"

Ve hazırlama yuvası güncelleştirmede doğrulandıktan sonra artık, geriye kalan tek şey üretime değiştirilecek. Git Kabuğu'nda, yalnızca aşağıdaki komutları çalıştırın:

    cd <repository_root>\ARMTemplates
    .\swap.ps1 -Name ToDoApp<unique_string>master

Tebrikler! Üretim web uygulamanız için yeni bir güncelleştirme başarıyla oluşturdunuz. Daha, bunu kolayca geliştirme ve test ortamları oluşturma ve derleme ve her işleme sınama olmuştur. Çevik Yazılım Geliştirme için kritik önem taşıyan yapı taşları bunlar.

<a name="delete"></a>

## <a name="delete-dev-and-test-environments"></a>Geliştirme silin ve test ortamları
Kendi içinde bulunan kaynak gruplarının olarak geliştirme ve test ortamları kasıtlı olarak tasarlanmış olduğundan, bunları silin kolaydır. Olanları silmek için Bu öğreticide GitHub dalları ve yalnızca Git Kabuğu'nda aşağıdaki komutları çalıştırın Azure yapıları oluşturuldu:

    git branch -d Dev
    git push origin :Dev
    git branch -d NewUpdate
    git push origin :NewUpdate
    Remove-AzureRmResourceGroup -Name ToDoApp<unique_string>dev-group -Force -Verbose
    Remove-AzureRmResourceGroup -Name ToDoApp<unique_string>newupdate-group -Force -Verbose

## <a name="summary"></a>Özet
Çevik Yazılım Geliştirme bir gereken kendi uygulama platformu olarak Azure benimsemeyi almak isteyen çok sayıda şirketler için ' dir. Bu öğreticide, oluşturma ve karmaşık uygulamalar için bile kolaylıkla tam çoğaltmaları aşağı veya üretim ortamının çoğaltmaları yakın kesmeden öğrendiniz. Ayrıca, yapı ve Azure'da tek her işleme test bir geliştirme işlemi oluşturmak için bu özelliği kullanabilmeniz öğrendiniz. Bu öğretici umarız nasıl en iyi Azure App Service ve Azure Resource Manager birlikte çevik yöntemlerden caters bir DevOps çözümü oluşturmak için kullanabileceğiniz göstermiştir. Ardından, bu senaryonun DevOps teknikleri gibi gelişmiş gerçekleştirerek oluşturabileceğiniz [üretimde test](app-service-web-test-in-production-get-start.md). Ortak bir sınama üretim senaryosu için bkz: [(Azure App Service'te test beta) Flighting dağıtım](app-service-web-test-in-production-controlled-test-flight.md).

## <a name="more-resources"></a>Diğer kaynaklar
* [Azure'nın beklendiği karmaşık bir uygulama dağıtma](app-service-deploy-complex-application-predictably.md)
* [Çevik Geliştirme uygulamada: ipuçları ve püf noktaları Modernized geliştirme döngüsü için](http://channel9.msdn.com/Events/Ignite/2015/BRK3707)
* [Resource Manager şablonları kullanarak Azure Web uygulamaları için gelişmiş dağıtım stratejileri](http://channel9.msdn.com/Events/Build/2015/2-620)
* [Azure Resource Manager şablonları yazma](../azure-resource-manager/resource-group-authoring-templates.md)
* [JSONLint - JSON Doğrulayıcı](http://jsonlint.com/)
* [Site için GitHub yayımlama ARMClient – ayarlama](https://github.com/projectKudu/ARMClient/wiki/Setup-GitHub-publishing-to-Site)
* [Git dallanma – temel dallandırma ve birleştirme](http://www.git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)
* [David Ebbo'nın blogu](http://blog.davidebbo.com/)
* [Azure PowerShell](/powershell/azure/overview)
* [Azure platformlar arası komut satırı araçları](../cli-install-nodejs.md)
* [Kullanıcı oluşturma veya Azure AD içinde düzenleme](https://msdn.microsoft.com/library/azure/hh967632.aspx#BKMK_1)
* [Proje Kudu Wiki](https://github.com/projectkudu/kudu/wiki)

