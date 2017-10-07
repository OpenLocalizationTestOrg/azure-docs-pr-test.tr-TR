---
title: "aaaProvision ve mikro beklendiği azure'da dağıtma"
description: "Mikro tek bir birim olarak Azure App Service ve JSON kaynak grubu şablonları ve PowerShell komut dosyası kullanarak tahmin edilebilir bir şekilde nasıl toodeploy uygulamanın oluşan öğrenin."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: bb51e565-e462-4c60-929a-2ff90121f41d
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2016
ms.author: cephalin
ms.openlocfilehash: d32c2fc82a8b09e89224ec437e5819b65b2e9e78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="provision-and-deploy-microservices-predictably-in-azure"></a>Sağlama ve mikro beklendiği azure'da dağıtma
Bu öğreticide gösterilmiştir nasıl tooprovision ve oluşan bir uygulamayı dağıtmak [mikro](https://en.wikipedia.org/wiki/Microservices) içinde [Azure App Service](/services/app-service/) tek bir birim olarak ve JSON kaynak grubu şablonları kullanarak tahmin edilebilir bir şekilde ve PowerShell komut dosyası. 

Sağlama ve yüksek oranda ayrılmış mikro oluşan büyük ölçekli uygulamalara dağıtma, Yinelenebilirlik ve öngörülebilirlik önemli toosuccess alındığında. [Azure uygulama hizmeti](/services/app-service/) web uygulamaları, mobil uygulamalar, API apps ve logic apps dahil toocreate mikro hizmetler sağlar. [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) , toomanage veritabanı ve kaynak denetim ayarları gibi kaynak bağımlılıkları ile birlikte bir birim olarak tüm hello mikro hizmetler sağlar. Şimdi, JSON şablonları ve basit PowerShell komut dosyası kullanarak bu tür bir uygulama dağıtabilirsiniz. 

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="what-you-will-do"></a>Ne yapacağını
Merhaba öğreticide içeren bir uygulama dağıtır:

* İki web uygulamaları (yani, iki mikro)
* Arka uç SQL veritabanı
* Uygulama ayarları, bağlantı dizeleri ve kaynak denetimi
* Application ınsights, uyarılar, otomatik ölçeklendirmeyi ayarları

## <a name="tools-you-will-use"></a>Kullanacağınız araçları
Bu öğreticide, araçları aşağıdaki hello kullanır. Araçlar ile ilgili kapsamlı tartışma olmadığından, t toostick toohello uçtan uca senaryoyu ayarlayacağım ve kısa giriş tooeach size ve burada bulabilirsiniz, hakkında daha fazla bilgi. 

### <a name="azure-resource-manager-templates-json"></a>Azure Resource Manager şablonları (JSON)
Örneğin, Azure App Service'te bir web uygulaması oluşturma her zaman, Azure Resource Manager bir JSON şablon toocreate hello tüm kaynak grubu ile Merhaba bileşen kaynakları kullanır. Merhaba karmaşık bir şablondan [Azure Marketi](/marketplace) hello gibi [ölçeklenebilir WordPress](/marketplace/partners/wordpress/scalablewordpress/) uygulama hello MySQL veritabanı, depolama hesapları, hello uygulama hizmeti planı, hello web uygulaması kendisi, uyarı kuralları, uygulama içerebilir ayarları, otomatik ölçeklendirme ayarlarını ve daha fazla ve tüm bu şablonları PowerShell aracılığıyla kullanılabilir tooyou verilebilir. Bu şablonları toodownload ve kullanım nasıl görürüm hakkında bilgi için [Azure PowerShell kullanarak Azure Resource Manager ile](../powershell-azure-resource-manager.md).

Hello Azure Resource Manager şablonları hakkında daha fazla bilgi için bkz: [Azure Resource Manager şablonları yazma](../azure-resource-manager/resource-group-authoring-templates.md)

### <a name="azure-sdk-26-for-visual-studio"></a>Visual Studio için Azure SDK 2.6
Merhaba en yeni SDK geliştirmeleri toohello hello JSON Düzenleyicisi'nde Resource Manager şablonu desteği içerir. Bu tooquickly kullanabileceğiniz sıfırdan bir kaynak grubu şablonu oluşturmak veya var olan değişiklik JSON şablonunu (örneğin, indirilen galeri şablonu) açın, hello parametreler dosyası doldurmak ve hatta hello doğrudan Azure kaynak grubu dağıtma Kaynak grubu çözümü.

Daha fazla bilgi için bkz: [Visual Studio için Azure SDK 2.6](https://azure.microsoft.com/blog/2015/04/29/announcing-the-azure-sdk-2-6-for-net/).

### <a name="azure-powershell-080-or-later"></a>Azure PowerShell 0.8.0 veya daha yenisi
Sürüm 0.8.0'den başlayarak, hello Azure PowerShell'i yükleme toplama toohello Azure modülü hello Azure Resource Manager modülü içerir. Bu yeni modül tooscript hello dağıtımı kaynak gruplarının sağlar.

Daha fazla bilgi için bkz: [Azure PowerShell'i Azure Resource Manager ile kullanma](../powershell-azure-resource-manager.md)

### <a name="azure-resource-explorer"></a>Azure Resource Manager
Bu [önizleme aracını](https://resources.azure.com) hello kaynak aboneliği ve hello tek tek kaynaklarınızı alt gruplarda tooexplore hello JSON tanımlarını sağlar. Merhaba aracında bir kaynağın hello JSON tanımlarını düzenleme, kaynakların tüm bir hiyerarşiye silin ve yeni kaynaklar oluşturun.  Bu aracı kullanıma hazır Hello bilgi ne size gösterir olduğundan şablon yazmak için çok yararlı gereksinim tooset belirli bir kaynak türü için hello özellikleri değerleri, vb. düzeltin. Kaynak grubunuzun hello bile oluşturabilirsiniz [Azure Portal](https://portal.azure.com/), kendi JSON tanımlarını incelemek hello Gezgini aracı toohelp hello kaynak grubu templatize.

### <a name="deploy-tooazure-button"></a>Dağıt tooAzure düğmesi
Kaynak denetimi için GitHub kullanırsanız, koyabilirsiniz bir [dağıtma tooAzure düğmesini](https://azure.microsoft.com/blog/2014/11/13/deploy-to-azure-button-for-azure-websites-2/) halinde, Benioku. MD, bir anahtar teslim dağıtım UI tooAzure sağlar. Tüm basit web uygulaması için bunu yapabilirsiniz olsa da, tüm kaynak grubunuzun hello depo kök dizininde azuredeploy.json dosyasını koyarak dağıtma bu tooenable genişletebilirsiniz. Merhaba kaynak grup şablonu içerir, bu JSON dosyası hello dağıtma tooAzure düğmesini toocreate hello kaynak grubu tarafından kullanılır. Merhaba bir örnek için bkz: [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) Bu öğreticide kullanacaksınız örnek.

## <a name="get-hello-sample-resource-group-template"></a>Merhaba örnek kaynak grubunu Şablon Al
Böylece artık doğru tooit'şimdi alın.

1. Toohello gidin [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) uygulama hizmeti örnek.
2. Readme.MD içinde tıklatın **tooAzure dağıtmak**.
3. Toohello yönlendirilirsiniz [azure ile dağıtma](https://deploy.azure.com) site ve sorulan tooinput dağıtım parametreleri. Merhaba alanları çoğunu hello havuz adı ve bazı rastgele dizeleri ile sizin için doldurulacağı dikkat edin. İstediğiniz, ancak tooenter sahip hello tek şey hello SQL Server yönetici oturum açma ve hello parola ve ardından tüm hello alanları değiştirebilirsiniz **sonraki**.
   
   ![](./media/app-service-deploy-complex-application-predictably/gettemplate-1-deploybuttonui.png)
4. Bundan sonra öğesini **dağıtma** toostart hello dağıtım işlemi. Merhaba işlemi toocompletion çalıştırılan sonra hello http://todoapp tıklayın*XXXX*. azurewebsites.net bağlantı toobrowse hello dağıtılan uygulama. 
   
   ![](./media/app-service-deploy-complex-application-predictably/gettemplate-2-deployprogress.png)
   
   Merhaba uygulamaları hemen başlamasını olan, ancak kendiniz tam olarak işlevsel bir uygulaması olduğunu ikna tooit ilk göz attığınızda hello UI biraz yavaş olacaktır.
5. Merhaba geri hello dağıtma sayfasında tıklatın **Yönet** bağlantı toosee hello yeni uygulamada hello Azure Portal.
6. Merhaba, **Essentials** açılan listesinde, hello kaynak grubunu bağlantısını tıklatın. Ayrıca bu hello web uygulaması zaten Not bağlı toohello GitHub deposunu altında **harici proje**. 
   
   ![](./media/app-service-deploy-complex-application-predictably/gettemplate-3-portalresourcegroup.png)
7. Merhaba kaynak grubu dikey penceresinde olduğunu zaten iki web uygulamaları ve hello kaynak grubu bir SQL veritabanında unutmayın.
   
   ![](./media/app-service-deploy-complex-application-predictably/gettemplate-4-portalresourcegroupclicked.png)

Hemen bir kısa süre içinde tüm hello bileşenleri, bağımlılıkları, ayarları, veritabanı ve sürekli yayımlama ile bir tam olarak dağıtılan iki mikro hizmet uygulaması tarafından bir otomatikleştirilmiş düzenlemesi Azure Kaynak Yöneticisi'nde ayarlanır gördüğünüz her şey. Tüm bu iki şey tarafından yapılmıştır:

* Merhaba dağıtma tooAzure düğmesi
* azuredeploy.JSON hello depo kök

Aynı uygulama dağıtabilirsiniz onlarca, yüzlerce veya binlerce kez ve hello tam aynı yapılandırmayı her zaman sahip. Bu yaklaşımın Hello Yinelenebilirlik ve hello öngörülebilirlik toodeploy büyük ölçekli uygulamalar kolaylığı ve güvenilirlik sağlar.

## <a name="examine-or-edit-azuredeployjson"></a>AZUREDEPLOY inceleyin (veya Düzenle). JSON
Şimdi hello GitHub deposunu nasıl ayarlandığı bakalım. Merhaba JSON Düzenleyicisi hello Azure .NET SDK kullanarak bunu henüz yüklemediyseniz [Azure .NET SDK 2.6](/downloads/), şimdi yapın.

1. Kopya hello [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) , sık kullanılan git aracını kullanarak deposu. Merhaba ekran görüntüsünde, ı hello Visual Studio 2013'te Takım Gezgini, bunu.
   
   ![](./media/app-service-deploy-complex-application-predictably/examinejson-1-vsclone.png)
2. Merhaba deposu kökünden azuredeploy.json Visual Studio'da açın. Merhaba JSON ana hattı bölmesini göremiyorsanız, tooinstall Azure .NET SDK'sı gerekir.
   
   ![](./media/app-service-deploy-complex-application-predictably/examinejson-2-vsjsoneditor.png)

I her ayrıntı hello JSON biçiminde değil giderek toodescribe istiyorum ancak hello [daha kaynakları](#resources) bölüm hello kaynak grubunu şablon dili öğrenme için bağlantılar içeriyor. Burada, yalnızca yapacağım hello yardımcı olabilecek özellikler ilginç tooshow, kendi özel şablonunuzu uygulama dağıtımını yaparken başlayın.

### <a name="parameters"></a>Parametreler
Bu parametreler çoğunu hangi hello olduğunu göz atın hello parametreleri bölüm toosee **tooAzure dağıtmak** düğmesini tooinput ister. Merhaba site hello arkasında **tooAzure dağıtmak** düğmesi doldurur hello giriş UI azuredeploy.json içinde tanımlanan hello parametrelerini kullanarak. Bu parametreleri kaynak adları, özellik değerleri, vb. gibi hello kaynak tanımları boyunca kullanılır.

### <a name="resources"></a>Kaynaklar
Merhaba kaynakları düğümünde 4 en üst düzey kaynakları, bir SQL Server örneği, bir uygulama hizmeti planı ve iki web uygulamaları gibi tanımlandığından emin görebilirsiniz. 

#### <a name="app-service-plan"></a>App Service planı
Merhaba JSON içinde basit bir kök düzeyinde kaynakla başlayalım tıklatın. Adlı uygulama hizmeti planı hello Hello JSON ana hattı, tıklatın **[hostingPlanName]** toohighlight hello karşılık gelen JSON kodunu. 

![](./media/app-service-deploy-complex-application-predictably/examinejson-3-appserviceplan.png)

Bu hello Not `type` öğesi belirtir (Bu çağrıldı bir sunucu grubu bir uzun, uzun zaman önce) bir uygulama hizmeti planının hello dize ve diğer öğeleri ve özellikleri hello JSON dosyasında tanımlanan hello parametreleri kullanarak doldurulur ve bu kaynak yok Tüm iç içe kaynaklar.

> [!NOTE]
> Ayrıca bu hello değeri Not `apiVersion` hello REST API toouse hello JSON kaynak tanımıyla ve hangi sürümü hello kaynak hello içinde nasıl biçimlendirilmelidir etkileyebilecek Azure söyler `{}`. 
> 
> 

#### <a name="sql-server"></a>SQL Server
Bundan sonra adlı hello SQL Server kaynak üzerinde öğesini **SQLServer** hello JSON ana hattı içinde.

![](./media/app-service-deploy-complex-application-predictably/examinejson-4-sqlserver.png)

Not hello Hello hakkında aşağıdaki JSON kodunu vurgulanmış:

* Merhaba kullanılması parametreleri, oluşturulan hello kaynakları adlı ve birbiriyle tutarlı hale getirir şekilde yapılandırılmış sağlar.
* Merhaba SQLServer kaynak sahip iki iç içe geçmiş kaynakların, her için farklı bir değere sahip `type`.
* Merhaba, kaynakları içinde iç içe geçmiş `“resources”: […]`hello veritabanı ve hello güvenlik duvarı kuralları tanımlandığı, sahip bir `dependsOn` öğesi hello kök düzeyinde SQLServer kaynak hello kaynak Kimliğini belirtir. "Başka kaynağı zaten var olması gerekir; bu kaynak, oluşturmadan önce bu Azure Resource Manager bildirir. ve bu kaynağın hello şablonunda tanımlanırsa, bir ilk oluşturma".
  
  > [!NOTE]
  > Hakkında ayrıntılı bilgi için toouse hello `resourceId()` işlev, bkz: [Azure Resource Manager şablonu işlevleri](../azure-resource-manager/resource-group-template-functions-resource.md#resourceid).
  > 
  > 
* Merhaba hello etkisini `dependsOn` öğesidir Azure Resource Manager kaynakları paralel olarak oluşturulabilir ve hangi kaynaklara sırayla oluşturulmalıdır bilebilirsiniz. 

#### <a name="web-app"></a>Web uygulaması
Şimdi, şimdi daha karmaşık olan toohello gerçek web uygulamalarında kendileri taşıyın. Merhaba JSON ana hattı toohighlight Hello [variables('apiSiteName')] web uygulamasında JSON kodunu'ı tıklatın. İşleri çok daha ilginç aldıklarından fark edeceksiniz. Bu amaçla ı hello özellikleri tek tek hakkında konuşma:

##### <a name="root-resource"></a>Kök kaynak
Merhaba web uygulama iki farklı kaynaklarına bağlıdır. Bu, Azure Resource Manager App Service planı ve SQL Server örneği hello oluşturulan yalnızca her iki hello sonra hello web uygulaması oluşturma anlamına gelir.

![](./media/app-service-deploy-complex-application-predictably/examinejson-5-webapproot.png)

##### <a name="app-settings"></a>Uygulama ayarları
Merhaba uygulama ayarları da iç içe geçmiş bir kaynak olarak tanımlanır.

![](./media/app-service-deploy-complex-application-predictably/examinejson-6-webappsettings.png)

Merhaba, `properties` öğesi için `config/appsettings`, iki uygulama ayarları hello biçiminde sahip `“<name>” : “<value>”`.

* `PROJECT`olan bir [KUDU ayarı](https://github.com/projectkudu/kudu/wiki/Customizing-deployments) , Azure dağıtım hangi proje toouse birden çok proje Visual Studio çözümünde söyler. T, kaynak denetimi daha sonra nasıl yapılandırıldığını gösterir, ancak hello ToDoApp kodu birden çok proje Visual Studio çözümünde olduğundan, bu ayar ihtiyacımız.
* `clientUrl`Bu hello uygulama kodu ayarı olarak yalnızca bir uygulama kullanılır.

##### <a name="connection-strings"></a>Bağlantı dizeleri
Merhaba bağlantı dizeleri de iç içe geçmiş bir kaynak olarak tanımlanır.

![](./media/app-service-deploy-complex-application-predictably/examinejson-7-webappconnstr.png)

Merhaba, `properties` öğesi için `config/connectionstrings`, her bir bağlantı dizesini de hello belirli biçimi ile ad: değer çifti olarak tanımlanan `“<name>” : {“value”: “…”, “type”: “…”}`. Hello için `type` öğesi, olası değerler şunlardır: `MySql`, `SQLServer`, `SQLAzure`, ve `Custom`.

> [!TIP]
> Azure PowerShell komutunda aşağıdaki hello hello bağlantı dizesi türleri kesin bir listesi için çalıştırın: \[Enum]::GetNames("Microsoft.WindowsAzure.Commands.Utilities.Websites.Services.WebEntities.DatabaseType")
> 
> 

##### <a name="source-control"></a>Kaynak denetimi
Merhaba kaynak denetim ayarları da iç içe geçmiş bir kaynak olarak tanımlanır. Azure Resource Manager bu kaynak tooconfigure sürekli yayımlama kullanır (uyarısıyla bakın `IsManualIntegration` daha sonra) ve ayrıca tookick uygulama kodu hello dağıtım hello JSON dosyası hello işlenmesi sırasında otomatik olarak devre dışı.

![](./media/app-service-deploy-complex-application-predictably/examinejson-8-webappsourcecontrol.png)

`RepoUrl`ve `branch` oldukça sezgisel olmalıdır ve toohello Git deposu ve hello adını hello şube toopublish işaret etmelidir. Yeniden, bu giriş parametreleri tarafından tanımlanır. 

Merhaba notta `dependsOn` , toplama toohello içinde uygulama kaynak kendisini web öğesi `sourcecontrols/web` de bağlıdır `config/appsettings` ve `config/connectionstrings`. Bunun nedeni, bir kez `sourcecontrols/web` olan yapılandırılmış, hello Azure dağıtım işlemi otomatik olarak toodeploy, deneyecek oluşturun ve hello uygulama kodu başlatın. Bu nedenle, Hello uygulama kodu çalıştırmadan önce bu bağımlılık yardımcı olur emin olun. ekleme hello uygulama erişim gerekli toohello uygulama ayarlarının ve bağlantı dizeleri vardır. 

> [!NOTE]
> Ayrıca `IsManualIntegration` çok ayarlanır`true`. Merhaba GitHub deposunu gerçekte sahibi olmadığınız ve böylece izni tooAzure tooconfigure sürekli yayımlama aslında veremezsiniz bu özellik Bu öğreticide gereklidir çünkü [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) (yani otomatik bildirme Depo güncelleştirmeleri tooAzure). Merhaba varsayılan değer kullandığınız `false` yalnızca hello hello sahibin GitHub kimlik bilgilerinin yapılandırdıysanız hello belirtilen depo [Azure portal](https://portal.azure.com/) önce. Diğer bir deyişle, hello herhangi bir uygulama için kaynak denetimi tooGitHub veya BitBucket yukarı ayarladıysanız, [Azure Portal](https://portal.azure.com/) Azure hello kimlik bilgilerini Hatırla ve tüm uygulamasını dağıtın olduğunda bunları kullanın. ardından daha önce kullanarak, kullanıcı, kimlik bilgileri GitHub veya BitBucket hello gelecekteki içinde. Ancak, bunu zaten yapmadıysanız, GitHub veya BitBucket hello depo sahibinin kimlik bilgileriyle oturum açamıyor çünkü Azure Resource Manager tooconfigure hello web uygulamanızın kaynak denetim ayarları çalıştığında hello JSON şablon dağıtımı başarısız olur.
> 
> 

## <a name="compare-hello-json-template-with-deployed-resource-group"></a>Merhaba JSON şablonunu dağıtılmış kaynak grubu ile karşılaştırın
Burada, tüm hello web uygulamanızın dikey hello içinde aracılığıyla gidebilirsiniz [Azure Portal](https://portal.azure.com/), ancak yalnızca yararlı, Eğer daha değil başka bir aracı yoktur. Toohello Git [Azure kaynak Gezgini](https://resources.azure.com) hello Azure arka uç gerçekte oldukları gibi tüm hello kaynak grupları JSON gösterimi, Aboneliklerde imkanı sağlayan Önizleme aracı. Ayrıca, nasıl Azure hello kaynak grubun JSON hiyerarşisinde hello hiyerarşisiyle toocreate kullandı hello şablon dosyası, karşılık gelen görebilirsiniz.

Örneğin, ne zaman ı Git toohello [Azure kaynak Gezgini](https://resources.azure.com) aracı ve hello Explorer'da hello düğümleri genişletin, hello kaynak grubu ve ilgili kaynak türlerine altında toplanan hello kök düzeyinde kaynak görebilirsiniz.

![](./media/app-service-deploy-complex-application-predictably/ARM-1-treeview.png)

Tooa web uygulamasını ayrıntıya mümkün toosee web uygulamasını yapılandırma ayrıntıları benzer toohello ekran görüntüsü aşağıda olmalıdır:

![](./media/app-service-deploy-complex-application-predictably/ARM-2-jsonview.png)

Yeniden hello iç içe geçmiş kaynakların bir hiyerarşi çok benzer toothose JSON şablon dosyanızın sahip olmalıdır ve görmelisiniz hello uygulama ayarları, bağlantı dizeleri, vb., düzgün şekilde hello JSON bölmesinde yansıtılır. Burada ayarlarını Hello yokluğu JSON dosyanız bir sorunu gösterebilir ve JSON şablon dosyanızın gidermenize yardımcı olabilir.

## <a name="deploy-hello-resource-group-template-yourself"></a>Kendiniz Hello kaynak grup şablonu dağıtma
Merhaba **tooAzure dağıtmak** düğmesi harika olmakla birlikte, yalnızca zaten azuredeploy.json tooGitHub gönderilen durumunda toodeploy hello kaynak grup şablonu azuredeploy.json sağlar. Hello Azure .NET SDK'sı, tüm JSON şablon dosyasından doğrudan yerel makinenize, toodeploy hello araçlar da sağlar. toodo Bu, başlangıç adımları aşağıdaki:

1. Visual Studio'da sırasıyla **dosya** > **yeni** > **proje**.
2. Tıklatın **Visual C#** > **bulut** > **Azure kaynak grubu**, ardından **Tamam**.
   
   ![](./media/app-service-deploy-complex-application-predictably/deploy-1-vsproject.png)
3. İçinde **Azure Şablonu Seç**seçin **boş şablon** tıklatıp **Tamam**.
4. Azuredeploy.JSON hello sürükleyin **şablonu** yeni projenizin klasör.
   
   ![](./media/app-service-deploy-complex-application-predictably/deploy-2-copyjson.png)
5. Kopyalanan hello azuredeploy.json Çözüm Gezgini'nden açın.
6. Yalnızca hello artırmak amacıyla, hello tanıtım için bazı standart uygulama Insight kaynakları tooour JSON dosyası, tıklayarak ekleyelim **kaynak ekleme**. Merhaba JSON dosyası dağıtmada yalnızca ilginizi çekiyorsa Atla toohello dağıtma adımları.
   
   ![](./media/app-service-deploy-complex-application-predictably/deploy-3-newresource.png)
7. Seçin **Web uygulamaları için Application Insights**, var olan bir App Service planı ve web uygulaması seçili olduğundan emin olun ve ardından **Ekle**.
   
   ![](./media/app-service-deploy-complex-application-predictably/deploy-4-newappinsight.png)
   
   Şimdi gerekir mümkün toosee birkaç yeni kaynaklar olması hello kaynak ve ne yaptığını bağlı olarak, bağımlılıklar ya da hello App Service planı ya da hello web uygulaması olduğundan,. Bu kaynaklar, varolan tanımı tarafından etkin değildir ve toochange oluşturacağız.
   
   ![](./media/app-service-deploy-complex-application-predictably/deploy-5-appinsightresources.png)
8. Hello JSON ana hattı, tıklatın **Appınsights'dan otomatik ölçeklendirme** toohighlight kendi JSON kodunu. Uygulama hizmeti planınız için ayar ölçeklendirme hello budur.
9. Buna Merhaba vurgulanan JSON kodunu, hello bulun `location` ve `enabled` özellikleri aşağıda gösterilen şekilde ayarlayın.
   
   ![](./media/app-service-deploy-complex-application-predictably/deploy-6-autoscalesettings.png)
10. Hello JSON ana hattı, tıklatın **CPUHigh Appınsights'dan** toohighlight kendi JSON kodunu. Bu bir uyarıdır.
11. Merhaba bulun `location` ve `isEnabled` özellikleri aşağıda gösterilen şekilde ayarlayın. Aynı Merhaba diğer üç uyarı (mor bulbs) hello.
    
    ![](./media/app-service-deploy-complex-application-predictably/deploy-7-alerts.png)
12. Şimdi hazır toodeploy olduğunuz. Merhaba projesine sağ tıklatın ve **dağıtma** > **yeni dağıtım**.
    
    ![](./media/app-service-deploy-complex-application-predictably/deploy-8-newdeployment.png)
13. Önceden yapmadıysanız Azure hesabınızda oturum açın.
14. Aboneliğinizde var olan bir kaynak grubunu seçin veya yeni bir select oluşturun **azuredeploy.json**ve ardından **parametreleri Düzenle**.
    
    ![](./media/app-service-deploy-complex-application-predictably/deploy-9-deployconfig.png)
    
    Artık tüm hello parametreleri hello şablon dosyası iyi bir tabloda tanımlanan mümkün tooedit olması. Varsayılanları tanımlayan parametreleri zaten varsayılan değerlerine sahip ve izin verilen değerler listesini tanımlayan parametreleri bırakmalar gösterilir.
    
    ![](./media/app-service-deploy-complex-application-predictably/deploy-10-parametereditor.png)
15. Tüm hello boş parametrelerinde doldurun ve hello kullanın [ToDoApp için GitHub deposuna adresi](https://github.com/azure-appservice-samples/ToDoApp.git) içinde **repoUrl**. Ardından **kaydetmek**.
    
    ![](./media/app-service-deploy-complex-application-predictably/deploy-11-parametereditorfilled.png)
    
    > [!NOTE]
    > Otomatik ölçeklendirme, içinde sunulan bir özelliktir **standart** katmanı ya da daha yüksek ve plan düzeyinde uyarılar özelliklerdir içinde sunulan **temel** katmanı veya üzeri, tooset hello gerekir **sku** parametre çok**standart** veya **Premium** içindeki tüm yeni App Insights kaynaklarınızı yukarı hafif toosee sipariş.
    > 
    > 
16. Tıklatın **dağıtmak**. Seçtiyseniz **parolaları kaydetme**, hello parola hello parametre dosyasında kaydedilecek **düz metin**. Aksi takdirde tooinput hello veritabanı parolasını hello dağıtım işlemi sırasında istenir.

Bu kadar! Toogo toohello yeterlidir artık [Azure Portal](https://portal.azure.com/) ve hello [Azure kaynak Gezgini](https://resources.azure.com) aracı toosee hello yeni uyarılar ve otomatik ölçeklendirme ayarlarını eklenen tooyour JSON dağıtılan uygulama.

Bu bölümdeki adımları uygulamanıza çoğunlukla hello aşağıdaki gerçekleştirdiniz:

1. Hazırlanan hello şablon dosyası
2. Bir parametre dosyası toogo hello şablon dosyası ile oluşturulan
3. Merhaba parametre dosyası ile dağıtılan hello şablon dosyası

Merhaba son adımı kolayca PowerShell cmdlet tarafından gerçekleştirilir. toosee Visual Studio, uygulama, açık Scripts\Deploy AzureResourceGroup.ps1 dağıtıldığında ne yaptığını. Çok fazla kod var. yoktur, ancak toodeploy hello şablon dosyası hello parametre dosyasıyla gereksinim duyduğunuz tüm hello ilgili kod yalnızca toohighlight kullanacağım.

![](./media/app-service-deploy-complex-application-predictably/deploy-12-powershellsnippet.png)

Son cmdlet hello `New-AzureResourceGroup`, hello hello eylem gerçekleştiren bir olduğu. Tüm bu araç hello yardımıyla, görece basit toodeploy olduğunu, tooyou göstermek, uygulama beklendiği bulut. Merhaba üzerinde hello cmdlet'i çalıştırmak her zaman aynı şablonuyla aynı hello parametre dosyası giderek tooget hello aynı sonucu.

## <a name="summary"></a>Özet
İçinde DevOps, Yinelenebilirlik ve öngörülebilirlik anahtarları tooany başarılı dağıtımı mikro oluşan büyük ölçekli uygulama var. Bu öğreticide, iki mikro hizmet uygulama tooAzure hello Azure Resource Manager şablonu kullanarak tek bir kaynak grubu dağıttıysanız. Neyse ki, verdiği hello Azure uygulamanızı bir şablona dönüştürme sırası toostart gereksinim ve sağlayabilir ve beklendiği dağıtmak bilgi. 

## <a name="next-steps"></a>Sonraki Adımlar
Çok öğrenin[Çevik yöntemlerini uygulamak ve sürekli olarak kolayca mikro uygulamanızı yayımlamak](app-service-agile-software-development.md) ve gelişmiş dağıtım teknikleri gibi [flighting dağıtım](app-service-web-test-in-production-controlled-test-flight.md) kolayca.

<a name="resources"></a>

## <a name="more-resources"></a>Diğer kaynaklar
* [Azure Resource Manager şablonu dili](../azure-resource-manager/resource-group-authoring-templates.md)
* [Azure Resource Manager şablonları yazma](../azure-resource-manager/resource-group-authoring-templates.md)
* [Azure Resource Manager şablonu işlevleri](../azure-resource-manager/resource-group-template-functions.md)
* [Azure Resource Manager şablonu ile bir uygulamayı dağıtma](../azure-resource-manager/resource-group-template-deploy.md)
* [Azure PowerShell’i Azure Resource Manager ile kullanma](../azure-resource-manager/powershell-azure-resource-manager.md)
* [Azure kaynak grubu dağıtım sorunlarını giderme](../azure-resource-manager/resource-manager-common-deployment-errors.md)

