---
title: "Azure App Service ile aaaAgile yazılım geliştirme"
description: "Bilgi nasıl toocreate büyük ölçekli karmaşık uygulamalar Azure uygulama hizmeti ile bir yolla Çevik Yazılım Geliştirme destekler."
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
ms.openlocfilehash: a1c1c78cfff711774943b0235ed762f03f48fc6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="agile-software-development-with-azure-app-service"></a>Azure App Service ile Çevik Yazılım Geliştirme
Bu öğreticide şunları öğreneceksiniz nasıl toocreate büyük ölçekli karmaşık uygulamalarla [Azure App Service](/azure/app-service/) destekler şekilde [Çevik Yazılım Geliştirme](https://en.wikipedia.org/wiki/Agile_software_development). Bu, zaten nasıl çok bildiğinizi varsayar[beklendiği Azure karmaşık uygulamalar dağıtmak](app-service-deploy-complex-application-predictably.md).

Teknik işlemlerde sınırlamaları genellikle hello çevik yöntemlerden uygulamasının başarılı biçimde bildirimde bulunabilir. Azure uygulama hizmeti gibi özelliklerle [sürekli yayımlama](app-service-continuous-deployment.md), [hazırlık ortamları](web-sites-staged-publishing.md) (yuvası) ve [izleme](web-sites-monitor.md)akıllıca hello düzenlemesini bağlı olduğunda, ve dağıtımda yönetimini [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md), Çevik Yazılım Geliştirme çekirdeğin geliştiriciler için harika bir çözümdür parçası olabilir.

Merhaba aşağıdaki tabloda kısa Çevik Geliştirme ile ilgili gereksinimler listesidir ve Azure Hizmetleri bunların her birini etkinleştirmek nasıl.

| Gereksinim | Azure nasıl sağlar |
| --- | --- |
| -Her işleme ile derleme<br>-Otomatik olarak oluşturabilir ve hızlı |Sürekli dağıtımı ile yapılandırıldığında, Azure App Service geliştirme şubeyi temel alarak Canlı çalışan derlemeleri olarak işlev görebilir. Kod toohello şube gönderilen her zaman, bu Canlı Azure içinde otomatik olarak yerleşik ve çalışır durumdadır. |
| -Kendi kendine test yapma derlemeler |Yük testleri, web testleri, vb., hello Azure Resource Manager şablonu ile dağıtılabilir. |
| -Üretim ortamında bir kopyasını testleri gerçekleştirme |Azure Resource Manager şablonları kullanılan toocreate kopyalarını hızla ve öngörülebilir bir şekilde test hello Azure üretim ortamının (uygulama ayarları, bağlantı dizesi şablonları, ölçekleme, vb. dahil) olabilir. |
| -En son derleme sonucu kolayca görüntüleme |Sürekli dağıtım tooAzure bir depodan değişikliklerinizi uygulamak hemen sonra canlı bir uygulamada yeni kod test edebilirsiniz anlamına gelir. |
| -Her gün toohello ana dala Yürüt<br>-Dağıtımı otomatik hale getir |Bir deponun ana dala olan üretim uygulama sürekli tümleştirme her yürütme/merge toohello ana dala tooproduction otomatik olarak dağıtır. |

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="what-you-will-do"></a>Ne yapacağını
Bir genel test aşaması üretim geliştirme iş akışında sipariş toopublish yeni değişiklikleri toohello size yol gösterecek [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) iki oluşur örnek uygulama [web uygulamaları](/services/app-service/web/), bir ön uç (FE) olması ve başka bir Web API arka uç (BE) olan hello ve [SQL veritabanı](/services/sql-database/). Dağıtım mimarisi aşağıdaki hello ile çalışır:

![](./media/app-service-agile-software-development/what-1-architecture.png)

Merhaba resme sözcükleri tooput:

* Merhaba dağıtım mimarisi üç ayrı ortamlara ayrılmış (veya [kaynak grupları](../azure-resource-manager/resource-group-overview.md) azure'da), her biri kendi [uygulama hizmeti planı](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md), [ölçeklendirme](web-sites-scale.md) ayarları ve SQL veritabanı. 
* Her ortam ayrı olarak yönetilebilir. Bunlar, hatta farklı Aboneliklerde bulunabilir.
* Hazırlama ve üretim hello iki yuvası uygulanır aynı App Service uygulaması. Merhaba ana dala sürekli tümleştirme için hazırlık yuvasındaki hello ile ayarlanır.
* Yürütme toomaster dal, hazırlık yuvasındaki (üretim verileriyle) hello doğrulandığında, hazırlama uygulama hello üretim yuvasına takas hello doğrulandı [kapalı kalma süresi olmadan](web-sites-staged-publishing.md).

Merhaba üretim ve hazırlama ortamına hello şablon tarafından tanımlanan [  *&lt;repository_root >*/ARMTemplates/ProdandStage.json](https://github.com/azure-appservice-samples/ToDoApp/blob/master/ARMTemplates/ProdAndStage.json).

Merhaba geliştirme ve test ortamları hello şablon tarafından tanımlanan [  *&lt;repository_root >*/ARMTemplates/Dev.json](https://github.com/azure-appservice-samples/ToDoApp/blob/master/ARMTemplates/Dev.json).

Merhaba geliştirme dalını toohello test şube yedeklemek sonra toohello ana dala (kalite, bunu toospeak taşıma) geçiş koduyla hello tipik dallanma strateji de kullanır.

![](./media/app-service-agile-software-development/what-2-branches.png) 

## <a name="what-you-need"></a>Ne gerekiyor
* Bir Azure hesabı
* A [GitHub](https://github.com/) hesabı
* Git Kabuğu (yüklenmiş [Windows için GitHub](https://windows.github.com/))-etkinleştirir, toorun her ikisi de hello Git ve PowerShell komutlarını hello aynı oturum 
* En son [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps) BITS
* Araçlar aşağıdaki hello ilgili temel bilgilere:
  * [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) şablon dağıtımı (Ayrıca bkz. [beklendiği azure'da karmaşık bir uygulama dağıtmak](app-service-deploy-complex-application-predictably.md))
  * [Git](http://git-scm.com/documentation)
  * [PowerShell](https://technet.microsoft.com/library/bb978526.aspx)

> [!NOTE]
> Bu öğretici bir Azure hesabı toocomplete gerekir:
> 
> * Yapabilecekleriniz [ücretsiz bir Azure hesabı açabilirsiniz](https://azure.microsoft.com/pricing/free-trial/) -krediler alırsınız Ücretli Azure hizmetlerini tootry çıkışı kullanabilirsiniz ve hatta kullanıldıktan sonra hello hesabı tutabilir ve ücretsiz Web uygulamaları gibi Azure hizmetlerini kullanabilirsiniz.
> * Yapabilecekleriniz [Visual Studio abone Avantajlarınızı etkinleştirebilir](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) -bilgisayarınızı Visual Studio abonelik size kredi verir Ücretli Azure hizmetlerinizi kullanabildiğiniz her ay.
> 
> Azure hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git[App Service'i deneyin](https://azure.microsoft.com/try/app-service/), burada hemen bir kısa süreli başlangıç web uygulaması App Service'te oluşturabilirsiniz. Kredi kartı ve taahhüt gerekmez.
> 
> 

## <a name="set-up-your-production-environment"></a>Üretim ortamınızı ayarlama
> [!NOTE]
> GitHub havuzunuzdan sürekli yayımlama hello komut dosyası otomatik olarak Bu öğreticide kullanılan yapılandırır. Bu, GitHub kimlik bilgileri zaten Azure'da depolanır, aksi takdirde hello dağıtım başarısız tooconfigure kaynak denetim ayarları hello web uygulamaları için çalışırken komut dosyası gerektirir. 
> 
> toostore, GitHub kimlik bilgileri, Azure'da hello bir web uygulaması oluşturma [Azure portal](https://portal.azure.com/) ve [GitHub dağıtımını yapılandırma](app-service-continuous-deployment.md). Toodo yalnızca bu kez gerekir. 
> 
> 

Tipik bir DevOps senaryo azure'da çalışan bir uygulamanız varsa ve sürekli yayımı üzerinden toomake değişiklikleri tooit istiyor. Bu senaryoda, bir şablon bu, geliştirilmiş, test edilmiş ve kullanılan toodeploy hello üretim ortamına sahip. Bu bölümde kurar.

1. Merhaba, kendi çatalı oluşturma [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) deposu. Çatalı oluşturma hakkında daha fazla bilgi için bkz: [bir depoyu Çatallaştırma](https://help.github.com/articles/fork-a-repo/). Çatalı oluşturulduktan sonra tarayıcınızı görebilirsiniz.
   
    ![](./media/app-service-agile-software-development/production-1-private-repo.png)
2. Git kabuk oturumu açın. Git Kabuk henüz yoksa, yükleme [Windows için GitHub](https://windows.github.com/) şimdi.
3. Merhaba aşağıdaki komutu çalıştırarak, çatalı yerel bir kopyasını oluşturun:

        git clone https://github.com/<your_fork>/ToDoApp.git 
4. Yerel kopya sahip olduğunda, çok gidin*&lt;repository_root >*\ARMTemplates ve çalışma hello deploy.ps1 komut aşağıdaki gibi:
   
        .\deploy.ps1 –RepoUrl https://github.com/<your_fork>/todoapp.git
5. İstendiğinde, istenen hello kullanıcı adı ve veritabanı erişimi için parola yazın.
   
   Çeşitli Azure kaynaklarını ilerlemesini sağlama hello görmeniz gerekir. Dağıtım tamamlandığında hello betik hello tarayıcıda hello uygulamasını başlatır ve kolay bip sesi verin.
   
    ![](./media/app-service-agile-software-development/production-2-app-in-browser.png)
   
   > [!TIP]
   > Bir göz atalım  *&lt;repository_root >*\ARMTemplates\Deploy.ps1, toosee nasıl benzersiz kimlikler kaynaklarla oluşturur. Aynı yaklaşımı toocreate klonlar, hello kullanabilirsiniz çakışan kaynak adları hakkında endişelenmeden aynı dağıtım hello.
   > 
   > 
6. Geri Git Kabuk oturumunuzda çalıştırın:
   
        .\swap –Name ToDoApp<unique_string>master
   
    ![](./media/app-service-agile-software-development/production-4-swap.png)
7. Merhaba betik tamamlandığında toobrowse toohello frontend'ın adresi geri dönün (http://ToDoApp*&lt;unique_string >*master.azurewebsites.net/) üretimde çalışan toosee Merhaba uygulaması.
8. İçinde toohello oturum [Azure portal](https://portal.azure.com/) ve ne oluşturulan bir göz atalım.
   
   Merhaba mümkün toosee iki web uygulamalarında olmalıdır aynı kaynak grubu, hello biriyle `Api` hello adı soneki. Merhaba kaynak grubu görünümü bakarsanız, hello SQL veritabanı ve sunucu, hello uygulama hizmeti planı ve hello hazırlık yuvaları hello web uygulamaları için Ayrıca bkz. Üzerinden Hello farklı kaynaklara göz atın ve bunlarla karşılaştırmak  *&lt;repository_root >*yapılandırmaya hello şablonunda \ARMTemplates\ProdAndStage.json toosee.
   
    ![](./media/app-service-agile-software-development/production-3-resource-group-view.png)

Şimdi hello üretim ortamını ayarlama. Ardından, yeni bir güncelleştirme toohello uygulama devre dışı tetiklersiniz.

## <a name="create-dev-and-test-branches"></a>Geliştirici oluşturma ve dalları sınama
Azure'da üretimde çalışan karmaşık bir uygulamaya sahip olduğunuza göre bir güncelleştirme tooyour uygulama çevik yöntem uygun hale getirir. Bu bölümde, toomake hello gerekli güncelleştirmeler gerekir geliştirme ve test dalları hello oluşturur.

1. İlk Hello test ortamı oluşturun. Git Kabuk oturumunuzda çalışma hello aşağıdaki komutları toocreate hello ortamı olarak adlandırılan yeni bir dalı için **NewUpdate**. 
   
        git checkout -b NewUpdate
        git push origin NewUpdate 
        .\deploy.ps1 -TemplateFile .\Dev.json -RepoUrl https://github.com/<your_fork>/ToDoApp.git -Branch NewUpdate
2. İstendiğinde, istenen hello kullanıcı adı ve veritabanı erişimi için parola yazın. 
   
   Dağıtım tamamlandığında hello betik hello tarayıcıda hello uygulamasını başlatır ve kolay bip sesi verin. Artık kendi test ortamı ile yeni bir dalı var. Şu anda tooreview bu test ortamı hakkında birkaç şey alın:
   
   * Tüm Azure aboneliklerinden oluşturabilirsiniz. Merhaba üretim ortamında test ortamınızdan ayrı olarak yönetilebilir anlamına gelir.
   * Test ortamınızı Azure'da Canlı çalışıyor.
   * Test ortamınızı yuvaları hazırlama hello ve ayarları ölçeklendirme hello dışında aynı toohello üretim ortamı alır. Merhaba ProdandStage.json ve Dev.json arasındaki tek fark olduklarından bildirin.
   * Farklı fiyat katmanı ile kendi uygulama hizmeti planındaki test ortamınızı yönetmek (gibi **serbest**).
   * Bu test ortamı siliniyor hello kaynak grubunun silinmesi gibi basit bir işlemdir. Nasıl bulacaksınız toodo bu [daha sonra](#delete).
3. Çalıştırarak geliştirme dal hello komutları aşağıdaki toocreate üzerinde gidin:
   
        git checkout -b Dev
        git push origin Dev
        .\deploy.ps1 -TemplateFile .\Dev.json -RepoUrl https://github.com/<your_fork>/ToDoApp.git -Branch Dev
4. İstendiğinde, istenen hello kullanıcı adı ve veritabanı erişimi için parola yazın. 
   
   Şu anda tooreview bu geliştirme ortamı hakkında birkaç şey alın: 
   
   * Geliştirme ortamınızı yapılandırma aynı toohello test ortamı sahip hello kullanılarak dağıtıldığında olduğundan aynı şablonu.
   * Her bir geliştirme ortamı ayrı olarak yönetilen hello test ortamı toobe bırakarak hello geliştiricinin kendi Azure aboneliğindeki, oluşturulabilir.
   * Geliştirme ortamınız ile Azure Canlı çalışıyor.
   * Merhaba geliştirme silme ortamı hello kaynak grubunun silinmesi kadar basittir. Nasıl bulacaksınız toodo bu [daha sonra](#delete).

> [!NOTE]
> Merhaba yeni güncelleştirme üzerinde çalışan birden çok geliştiriciler varsa, bunların her birini kolayca dal ve ayrılmış geliştirme ortamı adımları izleyerek hello ile oluşturabilirsiniz:
> 
> 1. Github'da kendi çatalı hello depo oluşturma (bkz [bir depoyu Çatallaştırma](https://help.github.com/articles/fork-a-repo/)).
> 2. Kopya hello çatalı kendi yerel makinede
> 3. Merhaba çalıştırmak kendi geliştirme şube ve ortam aynı toocreate komutları.
> 
> 

İşiniz bittiğinde, GitHub çatalı üç dalları olmalıdır:

![](./media/app-service-agile-software-development/test-1-github-view.png)

Ve altı web uygulamaları (iki üç kümeleri) üç ayrı kaynak grubunda olması gerekir:

![](./media/app-service-agile-software-development/test-2-all-webapps.png)

> [!NOTE]
> ProdandStage.json belirtir hello üretim ortamı toouse hello **standart** fiyatlandırma hello üretim uygulama ölçeklenebilirlik için uygun olan katmanı.
> 
> 

## <a name="build-and-test-every-commit"></a>Derleme ve test her işleme
Şablon dosyalarını ProdAndStage.json hello ve Dev.json zaten varsayılan olarak sürekli yayımlama hello web uygulaması için ayarlar hello kaynak denetimi parametreleri belirtin. Bu nedenle, her yürütme toohello GitHub şube o şubedeki gelen bir otomatik dağıtım tooAzure tetikler. Kurulumunuzu şimdi işleyişi görelim.

1. Merhaba geliştirme dalındaki hello yerel deposu olduğunuzdan emin olun. toodo Git Kabuk komutu aşağıdaki Bu, çalışma hello:
   
        git checkout Dev
2. Merhaba kod toouse değiştirerek bir değişiklik toohello uygulamanın UI katmanında duruma [önyükleme](http://getbootstrap.com/components/) listeler. Açık  *&lt;repository_root >*\src\MultiChannelToDo.Web\index.cshtml ve marka vurgulanan değişikliğinden sonra hello:
   
    ![](./media/app-service-agile-software-development/commit-1-changes.png)
   
    > [!NOTE]
    > Görüntü önceki hello okuyamadığında: 
    > 
    > * Satır 18'de, değiştirme `check-list` çok`list-group`.
    > * 19. satırda değiştirme `class="check-list-item"` çok`class="list-group-item"`.
    > 
    > 
3. Merhaba değişikliği kaydedin. Geri Git Kabuğu'nda hello aşağıdaki komutları çalıştırın:
   
        cd <repository_root>
        git add .
        git commit -m "changed toobootstrap style"
        git push origin Dev
   
   Bu git komutları çok "kodunuzda TFS gibi başka bir kaynak denetimi sistemindeki denetim" benzerdir. Çalıştırdığınızda `git push`, hello yeni tamamlama hangi sonra yeniden hello uygulama tooreflect hello değişikliği hello geliştirme ortamında bir otomatik kod itme tooAzure tetikler.
4. Bu kod itme tooyour geliştirme ortamı oluştu, tooverify tooyour geliştirme ortamı web uygulama sayfasına gidin ve hello bakın **dağıtım** bölümü. En son yürütme ileti var. mümkün toosee olmalıdır.
   
    ![](./media/app-service-agile-software-development/commit-2-deployed.png)
5. Buradan, tıklatın **Gözat** toosee hello azure'da hello Canlı uygulamasındaki yeni değişiklik.
   
    ![](./media/app-service-agile-software-development/commit-3-webapp-in-browser.png)
   
   Bu, bir küçük değişiklik toohello uygulamasıdır. Bununla birlikte, çoğu kez yeni değişiklikleri tooa karmaşık web uygulaması sahip istenmeyen ve istenmeyen yan etkiler. Müşterilerinize görebileceği önce mümkün tooeasily test edilen her işleme dinamik derlemelerde, toocatch bu sorunları sağlar.

Artık, hello gerçekleştirme ile rahat olmalıdır, hello yer alan bir geliştirici olarak **NewUpdate** proje, kendiniz için geliştirme ortamı oluşturmak daha sonra her işleme yapı ve her yapı test.

## <a name="merge-code-into-test-environment"></a>Kodu test ortamına Birleştir
Geliştirme kodunuzdan dal tooNewUpdate dalını yedeklemek hazır toopush olduğunuzda, bu hello standart git bir işlemdir:

1. Merhaba Geliştirme dalında GitHub, diğer geliştiriciler tarafından oluşturulan yürütme gibi tüm yeni işlemeleri tooNewUpdate birleştirin. Tüm yeni tamamlama github'da bir kodun ve yapı hello geliştirme ortamında tetikler. Ardından kodunuzu geliştirme dal hala hello son NewUpdate şube bitten çalışır emin olabilirsiniz.
2. Github'da NewUpdate şube geliştirme şube gelen tüm yeni işlemeleri birleştirin. Bu eylem bir kodun ve yapı hello test ortamında tetikler. 

Yeniden sürekli dağıtım zaten bu git dal ayarlandığından, tümleştirme çalıştıran gibi başka bir eylem oluşturur tootake gerekmeyen unutmayın. Git kullanarak tooperform standart kaynak denetimi yöntemler yeterlidir ve Azure tüm hello oluşturma işlemlerini sizin için gerçekleştirir.

Şimdi, şimdi kodunuzu çok anında**NewUpdate** dal. Git Kabuğu'nda hello aşağıdaki komutları çalıştırın:

    git checkout NewUpdate
    git pull origin NewUpdate
    git merge Dev
    git push origin NewUpdate

Bu kadar! 

Git toohello web uygulama sayfası, test ortamı toosee için (NewUpdate dala birleştirilmiş), yeni tamamlama toohello test ortamı artık gönderilir. Ardından **Gözat** stil değişikliği hello toosee artık Azure'da Canlı çalışıyor.

## <a name="deploy-update-tooproduction"></a>Güncelleştirme tooproduction dağıtma
Kod toohello Ftp'den hazırlama ve üretim ortamı kod toohello test ortamı basıldığında ne zaten yaptığınızı daha farklı geliyor olmalıdır. Gerçekten bu basit bir işlemdir. 

Git Kabuğu'nda hello aşağıdaki komutları çalıştırın:

    git checkout master
    git pull origin master
    git merge NewUpdate
    git push origin master

Merhaba şekilde hello hazırlama ve üretim ortamı ayarlandığından içinde ProdandStage.json temel unutmayın, yeni kodunuz toohello gönderilen **hazırlama** yuva ve orada çalışıyor. Bu nedenle toohello hazırlama yuvanın URL'si giderseniz, var. çalışan hello yeni kodu bakın. toodo cmdlet Git Kabuğu'nda aşağıdaki Bu, çalışma hello.

    Start-Process -FilePath "http://ToDoApp<unique_string>master-Staging.azurewebsites.net"

Ve hazırlık yuvasındaki hello hello güncelleştirmede doğrulandıktan sonra yalnızca bir şey toodo sol tooswap şimdi hello üretim içine. Git Kabuğu'nda yalnızca hello aşağıdaki komutları çalıştırın:

    cd <repository_root>\ARMTemplates
    .\swap.ps1 -Name ToDoApp<unique_string>master

Tebrikler! Yeni bir güncelleştirme tooyour üretim web uygulaması başarıyla oluşturdunuz. Daha, bunu kolayca geliştirme ve test ortamları oluşturma ve derleme ve her işleme sınama olmuştur. Çevik Yazılım Geliştirme için kritik önem taşıyan yapı taşları bunlar.

<a name="delete"></a>

## <a name="delete-dev-and-test-environments"></a>Geliştirme silin ve test ortamları
Çünkü, geliştirme kasıtlı olarak tasarlanmış ve test ortamları toobe kendi içinde bulunan kaynak gruplarının kolay toodelete olduğundan bunları. Bu öğreticide, hello GitHub dal ve Azure yapıları oluşturulan olanları toodelete hello yalnızca Git Kabuk komutları aşağıdaki hello çalıştırın:

    git branch -d Dev
    git push origin :Dev
    git branch -d NewUpdate
    git push origin :NewUpdate
    Remove-AzureRmResourceGroup -Name ToDoApp<unique_string>dev-group -Force -Verbose
    Remove-AzureRmResourceGroup -Name ToDoApp<unique_string>newupdate-group -Force -Verbose

## <a name="summary"></a>Özet
Çevik Yazılım Geliştirme tooadopt kendi uygulama platformu olarak Azure almak isteyen çok sayıda şirketler için gereken sahip olur. Bu öğreticide, nasıl toocreate ve kapatmayı tam çoğaltmaları aşağı veya çoğaltmalarını yakın üretim ortamına karmaşık uygulamalar için bile kolaylıkla hello öğrendiniz. Tooleverage bu yeteneği toocreate bir geliştirme işleminin nasıl öğrendiniz, derleme ve Azure'da tek her işleme test. Bu öğretici umarız nasıl en iyi Azure App Service ve Azure Resource Manager birlikte toocreate tooagile yöntemlerini caters bir DevOps çözümü kullanabileceğiniz göstermiştir. Ardından, bu senaryonun DevOps teknikleri gibi gelişmiş gerçekleştirerek oluşturabileceğiniz [üretimde test](app-service-web-test-in-production-get-start.md). Ortak bir sınama üretim senaryosu için bkz: [(Azure App Service'te test beta) Flighting dağıtım](app-service-web-test-in-production-controlled-test-flight.md).

## <a name="more-resources"></a>Diğer kaynaklar
* [Azure'nın beklendiği karmaşık bir uygulama dağıtma](app-service-deploy-complex-application-predictably.md)
* [Çevik Geliştirme uygulamada: ipuçları ve püf noktaları Modernized geliştirme döngüsü için](http://channel9.msdn.com/Events/Ignite/2015/BRK3707)
* [Resource Manager şablonları kullanarak Azure Web uygulamaları için gelişmiş dağıtım stratejileri](http://channel9.msdn.com/Events/Build/2015/2-620)
* [Azure Resource Manager şablonları yazma](../azure-resource-manager/resource-group-authoring-templates.md)
* [JSONLint - hello JSON Doğrulayıcı](http://jsonlint.com/)
* [ARMClient – GitHub yayımlama toosite ayarlayın](https://github.com/projectKudu/ARMClient/wiki/Setup-GitHub-publishing-to-Site)
* [Git dallanma – temel dallandırma ve birleştirme](http://www.git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)
* [David Ebbo'nın blogu](http://blog.davidebbo.com/)
* [Azure PowerShell](/powershell/azure/overview)
* [Azure platformlar arası komut satırı araçları](../cli-install-nodejs.md)
* [Kullanıcı oluşturma veya Azure AD içinde düzenleme](https://msdn.microsoft.com/library/azure/hh967632.aspx#BKMK_1)
* [Proje Kudu Wiki](https://github.com/projectkudu/kudu/wiki)

