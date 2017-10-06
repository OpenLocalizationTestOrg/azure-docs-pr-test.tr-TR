---
title: aaaVisual Studio Azure kaynak grubu projeleri | Microsoft Docs
description: "Visual Studio toocreate bir Azure kaynak grubu projesi kullanabilir ve hello kaynakları tooAzure dağıtabilirsiniz."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 4bd084c8-0842-4a10-8460-080c6a085bec
ms.service: azure-resource-manager
ms.devlang: multiple
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/10/2017
ms.author: tomfitz
ms.openlocfilehash: 672c1e71fb809b3b547f0fad30240d45de1ba923
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-and-deploying-azure-resource-groups-through-visual-studio"></a>Visual Studio aracılığıyla Azure kaynak grupları oluşturma ve dağıtma
Visual Studio ve hello [Azure SDK'sı](https://azure.microsoft.com/downloads/), altyapı ve kod tooAzure dağıtan bir proje oluşturabilirsiniz. Örneğin, hello web ana bilgisayarı, web sitesi ve veritabanını tanımlayabilir ve bu altyapıyı hello kod ile birlikte. Ayrıca, bir Sanal Makine, Sanal Ağ ve Depolama Hesabı tanımlayabilir ve bu altyapıyı ve Sanal Makinede yürütülen betiği dağıtabilirsiniz. Merhaba **Azure kaynak grubu** dağıtım projesi, toodeploy tek, tekrarlanabilir bir işlemde tüm gerekli hello kaynakları sağlar. Kaynakların dağıtılması ve yönetilmesi hakkında daha fazla bilgi için bkz. [Azure Resource Manager’a genel bakış](resource-group-overview.md).

Azure kaynak grubu projeleri tooAzure dağıtmak hello kaynakları tanımlayan Azure Resource Manager JSON şablonları içerir. toolearn hello Resource Manager şablonu hello öğeleri hakkında bkz [Azure Resource Manager şablonları yazma](resource-group-authoring-templates.md). Visual Studio, tooedit bu şablonları sağlar ve şablonları ile çalışma kolaylaştıran araçlar sağlar.

Bu makalede bir web uygulaması ve SQL Veritabanı dağıtacaksınız. Ancak, hello adımları olan neredeyse hello herhangi bir türdeki kaynağı için aynı. Bir Sanal Makineyi ve ilgili kaynaklarını da kolayca dağıtabilirsiniz. Visual Studio genelde karşılaşılan senaryoların dağıtılması için birçok farklı başlangıç şablonu sağlar.

Bu makalede Visual Studio 2017 gösterilmektedir. .NET 2.9 için Visual Studio 2015 güncelleştirme 2 ve Microsoft Azure SDK'sını kullanın ya da Visual Studio 2013 Azure SDK 2.9, deneyiminiz büyük ölçüde ise aynı hello. Hello Azure SDK 2.6 veya sonraki sürümlerini kullanabilirsiniz; ancak deneyiminiz hello kullanıcı arabiriminin bu makalede gösterilen hello kullanıcı arabirimi farklı olabilir. Merhaba hello en son sürümünü yüklemeniz önerilir [Azure SDK'sı](https://azure.microsoft.com/downloads/) hello adımları başlamadan önce. 

## <a name="create-azure-resource-group-project"></a>Azure Kaynak Grubu projesi oluşturma
Bu yordamda, bir **Web uygulaması + SQL** şablonu ile Azure Kaynak Grubu projesi oluşturacaksınız.

1. Visual Studio’da, **Dosya**, **Yeni Proje**’yi ve ardından **C#** veya **Visual Basic** seçeneğini belirleyin. Daha sonra **Bulut** ve **Azure Kaynak Grubu** projesini seçin.
   
    ![Bulut Dağıtım Projesi](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/create-project.png)
2. Merhaba şablonu seçme toodeploy tooAzure Resource Manager istiyor. Bildirim vardır üzerinde hello dayalı çok sayıda farklı seçeneğiniz projesi yazdığınız toodeploy istiyor. Bu makalede, hello seçin **Web uygulaması + SQL** şablonu.
   
    ![Şablon seçme](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/select-project.png)
   
    Seçtiğiniz hello yalnızca bir başlangıç noktası şablonudur; kaynakları toofulfill senaryonuz ekleyip çıkarabilirsiniz.
   
   > [!NOTE]
   > Visual Studio, çevrimiçi kullanılabilir şablonların listesini alır. Merhaba listesi değişebilir.
   > 
   > 
   
    Visual Studio Başlangıç web uygulaması ve SQL veritabanı için bir kaynak grubu dağıtım projesi oluşturur.
3. toosee, arama hello düğümde hello dağıtım projesindeki oluşturduğunuzu.
   
    ![düğümleri gösterme](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-items.png)
   
    Seçtiğimiz hello Web uygulaması + SQL şablonunu bu örnek için aşağıdaki dosyaları hello bakın: 
   
   | Dosya adı | Açıklama |
   | --- | --- |
   | Deploy-AzureResourceGroup.ps1 |PowerShell komutları toodeploy tooAzure Resource Manager çağıran PowerShell Betiği.<br />**Not** Visual Studio bu PowerShell Betiği toodeploy şablonunuzu kullanır. Tüm değişiklikleri Visual Studio'daki dağıtımı etkiler, bu nedenle dikkatli olun toothis betik yapın. |
   | WebSiteSQLDatabase.json |tooAzure dağıtmak istediğiniz hello altyapı ve dağıtım sırasında sağlayabileceğiniz hello parametreleri tanımlar hello Resource Manager şablonu. Ayrıca, Resource Manager hello kaynakları hello doğru sırayla dağıtır şekilde hello kaynakları arasındaki bağımlılıkların hello tanımlar. |
   | WebSiteSQLDatabase.parameters.json |Merhaba şablon tarafından gereken değerleri içeren bir parametre dosyası. Her dağıtım parametre değerlerini toocustomize geçirin. |
   
    Tüm kaynak grubu dağıtım projeleri bu temel dosyaları içerir. Diğer projeler diğer işlevleri ek dosyalar toosupport içerebilir.

## <a name="customize-hello-resource-manager-template"></a>Merhaba Resource Manager şablonunu özelleştirme
Toodeploy istediğiniz hello kaynakları tanımlayan hello JSON şablonlarını değiştirerek dağıtım projesi özelleştirebilirsiniz. JSON, JavaScript nesne gösterimi anlamına gelir ve kolay toowork sahip olan bir sıralanmış veri biçimidir. Merhaba JSON dosyaları her dosyanın hello üstünde başvuran bir şema kullanın. Toounderstand hello şema istiyorsanız, indirin ve analiz edin. Merhaba şema hangi öğeleri geçerli tanımlar, hello türlerini ve biçimlerini, numaralandırılmış değerlerin olası değerlerini hello ve benzeri. toolearn hello Resource Manager şablonu hello öğeleri hakkında bkz [Azure Resource Manager şablonları yazma](resource-group-authoring-templates.md).

şablonunuzda, toowork açmak **WebSiteSQLDatabase.json**.

düzenleme sizinle Resource Manager şablonu hello tooassist Hello Düzenleyici sunar Visual Studio Araçları. Merhaba **JSON ana hattı** penceresi, şablonunuzda tanımlanan kolay toosee hello öğeleri sağlar.

![JSON ana hattını göster](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-json-outline.png)

Hello öğelerini hello anahat seçerek toothat hello şablonunun parçası alır ve JSON karşılık gelen hello vurgular.

![JSON’a gitme](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/navigate-json.png)

Bir kaynak tarafından seçme ya da hello ekleyebilirsiniz **kaynak ekleme** hello üst hello JSON ana hattı penceresinin veya sağ tıklanarak düğmesini **kaynakları** ve seçerek **yeni kaynak ekleme**.

![kaynak ekle](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-resource.png)

Bu öğreticide, **Depolama Hesabı**’nı seçin ve bir ad verin. 11 karakterden uzun olmayan ve yalnızca sayı ile küçük harf içeren bir ad belirtin.

![depolama ekleme](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-storage.png)

Yalnızca hello kaynak eklendi ancak aynı zamanda bir hello için tür parametresi depolama hesabı ve hello depolama hesabının hello adı için bir değişken dikkat edin.

![ana hattı göster](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-new-items.png)

Merhaba **storageType** parametresi izin verilen türler ve varsayılan tür ile önceden tanımlanmış. Bu değerleri bırakabilir veya senaryonuz için düzenleyebilirsiniz. Herkes istemiyorsanız toodeploy bir **Premium_LRS** depolama hesabı bu şablon aracılığıyla türlerine izin hello kaldırın. 

```json
"storageType": {
  "type": "string",
  "defaultValue": "Standard_LRS",
  "allowedValues": [
    "Standard_LRS",
    "Standard_ZRS",
    "Standard_GRS",
    "Standard_RAGRS"
  ]
}
```

Visual Studio hello şablonu düzenlerken hangi özellikleri anlamak IntelliSense toohelp kullanılabilir de sağlar. Örneğin, uygulama hizmeti planınızı tooedit hello özelliklerini gidin toohello **HostingPlan** kaynak ve hello için bir değer ekleyin **özellikleri**. IntelliSense'in hello kullanılabilir değerleri gösterdiğini ve bu değer bir açıklaması verilmiştir dikkat edin.

![IntelliSense’i göster](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-intellisense.png)

Ayarlayabileceğiniz **numberOfWorkers** too1.

```json
"properties": {
  "name": "[parameters('hostingPlanName')]",
  "numberOfWorkers": 1
}
```

## <a name="deploy-hello-resource-group-project-tooazure"></a>Merhaba kaynak grubu projesi tooAzure dağıtma
Artık hazır toodeploy projenizi şunlardır. Bir Azure kaynak grubu projesi dağıttığınızda, tooan Azure kaynak grubu dağıtın. Hello kaynak grubu ortak yaşam döngüsü paylaşmak kaynakları mantıksal bir gruplandırmasıdır.

1. Merhaba kısayol menüsünde hello dağıtım proje düğümünün seçin **dağıtma** > **yeni**.
   
    ![Dağıt, Yeni Dağıtım menü öğesi](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/deploy.png)
   
    Merhaba **tooResource grubu dağıtma** iletişim kutusu görüntülenir.
   
    ![TooResource grubu iletişim kutusu dağıtma](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-deployment.png)
2. Merhaba, **kaynak grubu** açılır kutusunda, varolan bir kaynak grubu seçin veya yeni bir tane oluşturun. toocreate bir kaynak grubu açık hello **kaynak grubu** açılır kutusuna ve seçin **Yeni Oluştur**.
   
    ![TooResource grubu iletişim kutusu dağıtma](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/create-new-group.png)
   
    Merhaba **kaynak grubu oluştur** iletişim kutusu görüntülenir. Grubunuzun adını ve konumunu verin ve seçin hello **oluşturma** düğmesi.
   
    ![Kaynak Grubu Oluştur İletişim Kutusu](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/create-resource-group.png)
3. Merhaba seçerek hello dağıtım Hello parametrelerini düzenlemek **parametreleri Düzenle** düğmesi.
   
    ![Parametreleri Düzenle düğmesi](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/edit-parameters.png)
4. Merhaba boş parametreler için değerler sağlayın ve seçin hello **kaydetmek** düğmesi. Merhaba boş parametreleri **hostingPlanName**, **Admınıstratorlogın**, **Admınıstratorlogınpassword**, ve **databaseName**.
   
    **hostingPlanName** hello için bir ad belirtir [uygulama hizmeti planı](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) toocreate. 
   
    **Admınıstratorlogın** hello Merhaba SQL Server yönetici kullanıcı adını belirtir. **sa** veya **admin** gibi yaygın yönetici adlarını kullanmayın. 
   
    Merhaba **Admınıstratorlogınpassword** SQL Server Yönetici parolasını belirtir. Merhaba **parolaları düz metin hello parametreler dosyası olarak kaydetmek** seçeneği güvenli; bu nedenle, bu seçeneği belirlemeyin. Merhaba parola düz metin olarak kaydedilmiyor beri tooprovide yeniden dağıtımı sırasında bu parola gerekir. 
   
    **databaseName** hello veritabanı toocreate için bir ad belirtir. 
   
    ![Parametreleri Düzenle İletişim Kutusu](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/provide-parameters.png)
5. Merhaba seçin **dağıtma** düğmesini toodeploy hello proje tooAzure. Merhaba Visual Studio örneği dışında bir PowerShell konsolu açılır. Merhaba SQL Server Yönetici parolası istendiğinde hello PowerShell konsolunda da girin. **PowerShell Konsolunuzu diğer öğeleri gizli veya hello görev çubuğunda simge durumuna küçültülmüş.** Bu konsol için bakın ve tooprovide hello parola seçin.
   
   > [!NOTE]
   > Visual Studio tooinstall hello Azure PowerShell cmdlet'lerini isteyebilir. Azure PowerShell hello cmdlet'leri toosuccessfully kaynak gruplarına dağıtın. İstenirse, bunları yükleyin.
   > 
   > 
6. Merhaba dağıtım birkaç dakika sürebilir. Merhaba, **çıkış** windows hello hello dağıtım durumunu görebilir. Merhaba dağıtım tamamlandığında hello son ileti şuna benzer bir öğe ile başarılı bir dağıtımı gösterir:
   
        ... 
        18:00:58 - Successfully deployed template 'websitesqldatabase.json' tooresource group 'DemoSiteGroup'.
7. Merhaba bir tarayıcıda açın [Azure portal](https://portal.azure.com/) ve tooyour hesabında oturum açın. toosee hello kaynak grubu, select **kaynak grupları** ve dağıttığınız hello kaynak grubu.
   
    ![grup seçme](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/select-group.png)
8. Tüm dağıtılan hello kaynaklara bakın. Depolama hesabı tam olarak hangi, o kaynak eklenirken belirtilen değil hello bu hello adını dikkat edin. Merhaba depolama hesabı benzersiz olması gerekir. Merhaba şablonu otomatik olarak bir dize ekler karakter toohello adı benzersiz bir ad tooprovide sağlanan. 
   
    ![kaynakları göster](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-deployed-resources.png)
9. Değişiklik ve projenizin tooredeploy istiyorsanız Azure kaynak grubu projesinin kısayol menüsünden hello hello var olan kaynak grubunu seçin. Merhaba kısayol menüsünden seçin **dağıtma**ve ardından, dağıtılan hello kaynak grubunu seçin.
   
    ![Dağıtılan Azure kaynak grubu](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/redeploy.png)

## <a name="deploy-code-with-your-infrastructure"></a>Altyapınızla kodları dağıtma
Bu noktada, uygulamanız için hello altyapı dağıttınız, ancak hello proje ile dağıtılan gerçek bir kod yoktur. Bu makalede nasıl toodeploy bir web uygulaması ve SQL Database tablolarını dağıtım sırasında gösterilmektedir. Bir web uygulaması yerine bir sanal makine dağıtıyorsanız, dağıtımının bir parçası olarak hello makinede bazı kodu toorun istiyor. bir web uygulaması için kod dağıtma işlemi hello veya bir sanal makine ayarlıyor neredeyse için aynı hello.

1. Proje tooyour Visual Studio çözümü ekleyin. Merhaba çözüme sağ tıklayın ve seçin **Ekle** > **yeni proje**.
   
    ![proje ekleme](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-project.png)
2. Bir **ASP.NET Web Uygulaması** oluşturun. 
   
    ![web uygulaması ekleme](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-app.png)
3. **MVC** öğesini seçin.
   
    ![MVC’yi seçme](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/select-mvc.png)
4. Visual Studio web uygulamanızı oluşturduktan sonra hello çözümde iki proje bakın.
   
    ![projeleri göster](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-projects.png)
5. Şimdi, kaynak grubu projenizi hello yeni projenin farkında olduğundan emin toomake gerekir. Tooyour kaynak grubu projesi (AzureResourceGroup1) geri dönün. **Başvurular**’a sağ tıklayın ve **Başvuru Ekle**’yi seçin.
   
    ![başvuru ekleme](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-new-reference.png)
6. Oluşturduğunuz hello web uygulama projesini seçin.
   
    ![başvuru ekleme](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-reference.png)
   
    Bir başvuru ekleyerek hello web uygulama projesi toohello kaynak grubu projesi bağlamak ve otomatik olarak üç anahtar özelliklerini ayarlayın. Bu özellikler Merhaba, gördüğünüz **özellikleri** penceresinde hello başvuru.
   
      ![başvuruya bakma](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/see-reference.png)
   
    Merhaba özellikleri şunlardır:
   
   * Merhaba **ek özellikler** hello web dağıtımı paketi hazırlama toohello Azure Storage gönderilen konumuna içerir. Merhaba klasör (ExampleApp) ve dosya (package.zip) unutmayın. Uygulama dağıtımı sırasında parametreleri hello olarak sağlamak için bu değerleri tooknow gerekiyor. 
   * Merhaba **dosya yolu Ekle** hello paketinin oluşturulduğu hello yolunu içerir. Merhaba **hedefleri Ekle** dağıtım yürütür hello komutu içerir. 
   * Merhaba varsayılan değerini **oluşturun; Paket** dağıtım toobuild hello ve web dağıtım paketi (package.zip) oluşturmak sağlar.  
     
     Merhaba dağıtım hello özellikleri toocreate hello paketinden hello gerekli bilgileri elde ettiği bir yayımlama profili gerekmez.
7. TooWebSiteSQLDatabase.json geri dönün ve kaynak toohello şablonu ekleyin.
   
    ![kaynak ekle](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-resource-2.png)
8. Bu kez **Web Apps için Web Dağıtımı**’nı seçin. 
   
    ![web dağıtımı ekleme](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-web-deploy.png)
9. Kaynak grubu projesi toohello kaynak grubu yeniden dağıtın. Bu defa, bazı yeni parametre bulunur. Tooprovide değerlerini gerekmez **_artifactsLocation** veya **_artifactsLocationSasToken** için Visual Studio bu değerleri otomatik olarak oluşturur. Ancak, tooset hello klasörüne ve hello dağıtım paketini içeren dosya adı toohello yoluna sahip (olarak gösterilen **ExampleAppPackageFolder** ve **ExampleAppPackageFileName** görüntü aşağıdaki hello içinde ). Daha önce gördüğünüz hello değerleri hello başvuru özellikleri sağlayın (**ExampleApp** ve **package.zip**).
   
    ![web dağıtımı ekleme](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/set-new-parameters.png)
   
    Hello için **Yapıt depolama hesabı**, biri bu kaynak grubu ile dağıtılan hello seçin.
10. Merhaba dağıtım tamamlandıktan sonra web uygulamanızı hello Portalı'nda seçin. Merhaba URL toobrowse toohello siteyi seçin.
    
     ![siteye göz atma](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/browse-site.png)
11. Merhaba varsayılan ASP.NET uygulamasının başarıyla dağıttıysanız dikkat edin.
    
     ![dağıtılmış uygulamayı gösterme](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-deployed-app.png)

## <a name="next-steps"></a>Sonraki adımlar
* Merhaba portalı kullanarak kaynaklarınızı yönetme hakkında toolearn bkz [kullanarak Azure kaynaklarınızı Azure portal toomanage hello](resource-group-portal.md).
* Şablonlar hakkında daha fazla toolearn bkz [Azure Resource Manager şablonları yazma](resource-group-authoring-templates.md).

