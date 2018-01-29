---
title: Visual Studio Azure kaynak grubu projeleri | Microsoft Belgeleri
description: "Azure kaynak grubu projesi oluşturmak ve kaynakları Azure'a dağıtmak için Visual Studio'yu kullanın."
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
ms.openlocfilehash: d647206b882059e0651223dc84f2ad2a314f8a87
ms.sourcegitcommit: 933af6219266cc685d0c9009f533ca1be03aa5e9
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/18/2017
---
# <a name="creating-and-deploying-azure-resource-groups-through-visual-studio"></a>Visual Studio aracılığıyla Azure kaynak grupları oluşturma ve dağıtma
Visual Studio ve [Azure SDK](https://azure.microsoft.com/downloads/) ile altyapınızı ve kodlarınızı Azure’a dağıtan bir proje oluşturabilirsiniz. Örneğin, uygulamanızın web ana bilgisayarını, web sitesini ve veritabanını tanımlayabilir ve kodlarını ve altyapısını dağıtabilirsiniz. Ayrıca, bir Sanal Makine, Sanal Ağ ve Depolama Hesabı tanımlayabilir ve bu altyapıyı ve Sanal Makinede yürütülen betiği dağıtabilirsiniz. **Azure Kaynak Grubu** dağıtım projesi gerekli tüm kaynakları tek, tekrarlanabilir bir işlemde dağıtmanıza olanak tanır. Kaynakların dağıtılması ve yönetilmesi hakkında daha fazla bilgi için bkz. [Azure Resource Manager’a genel bakış](resource-group-overview.md).

Azure Kaynak Grubu projeleri, Azure’da dağıttığınız kaynakları tanımlayan Azure Resource Manager JSON şablonlarını içerir. Resource Manager şablonu bileşenleri hakkında daha fazla bilgi edinmek için [Azure Resource Manager şablonları yazma](resource-group-authoring-templates.md). Visual Studio bu şablonları düzenlemenize olanak tanır ve şablonlarla çalışmayı basitleştiren araçlar sunar.

Bu makalede bir web uygulaması ve SQL Veritabanı dağıtacaksınız. Ancak, adımlar tüm kaynak türleri için neredeyse aynıdır. Bir Sanal Makineyi ve ilgili kaynaklarını da kolayca dağıtabilirsiniz. Visual Studio genelde karşılaşılan senaryoların dağıtılması için birçok farklı başlangıç şablonu sağlar.

Bu makalede Visual Studio 2017 gösterilmektedir. Visual Studio 2015 Güncelleştirme 2 ve .NET 2.9 için Microsoft Azure SDK veya Azure SDK 2.9 ile Visual Studio 2013 kullanıyorsanız, deneyiminiz büyük ölçüde aynıdır. Azure SDK 2.6 veya sonraki sürümlerini kullanabilirsiniz. Ancak, kullanıcı arabirimindeki deneyiminiz bu makalede gösterilenden farklı olabilir. Adımları uygulamaya başlamadan önce [Azure SDK](https://azure.microsoft.com/downloads/)’nın en son sürümünü yüklemenizi kesinlikle öneririz. 

## <a name="create-azure-resource-group-project"></a>Azure Kaynak Grubu projesi oluşturma
Bu yordamda, bir **Web uygulaması + SQL** şablonu ile Azure Kaynak Grubu projesi oluşturacaksınız.

1. Visual Studio’da **Dosya**, **Yeni Proje**’yi ve **C#** veya **Visual Basic**’i seçin (bu projeler yalnızca JSON ve PowerShell içeriğine sahip olduğundan hangi dili seçtiğiniz sonraki aşamaları etkilemez). Daha sonra **Bulut** ve **Azure Kaynak Grubu** projesini seçin.
   
    ![Bulut Dağıtım Projesi](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/create-project.png)
2. Azure Resource Manager’da dağıtmak istediğiniz şablonu seçin. Dağıtmak istediğiniz proje türüne bağlı olarak çok sayıda farklı seçeneğiniz olduğunu unutmayın. Bu makale için **Web uygulaması + SQL** şablonunu seçin.
   
    ![Şablon seçme](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/select-project.png)
   
    Seçtiğiniz şablon sadece başlangıçtır; senaryonuzun gereksinimlerini karşılamak üzere kaynak ekleyebilir ve kaldırabilirsiniz.
   
   > [!NOTE]
   > Visual Studio, çevrimiçi kullanılabilir şablonların listesini alır. Liste değişebilir.
   > 
   > 
   
    Visual Studio, web uygulaması ve SQL Database için bir kaynak grubu dağıtım projesi oluşturur.
3. Oluşturduğunuz öğeleri görmek için dağıtım projesindeki düğümlere bakın.
   
    ![düğümleri gösterme](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-items.png)
   
    Bu örnek için Web uygulaması + SQL şablonunu seçtiğimiz için aşağıdaki dosyaları göreceksiniz: 
   
   | Dosya adı | Açıklama |
   | --- | --- |
   | Deploy-AzureResourceGroup.ps1 |Azure Resource Manager’da dağıtılacak PowerShell komutlarını çağıran PowerShell betiği.<br />**Not** Visual Studio, şablonunuzu dağıtmak için bu PowerShell betiğini kullanır. Bu betikte yaptığınız tüm değişiklikler Visual Studio’daki dağıtımı da etkiler, bu nedenle dikkatli olun. |
   | WebSiteSQLDatabase.json |Azure’da dağıtmak istediğiniz altyapıyı tanımlayan Resource Manager şablonu ve dağıtım sırasında sağlayabileceğiniz parametreler. Resource Manager’ın kaynakları doğru sırayla dağıtmasını sağlamak için kaynaklarınız arasındaki bağımlılıkları da tanımlar. |
   | WebSiteSQLDatabase.parameters.json |Şablon tarafından gereken değerleri içeren bir parametre dosyası. Her bir dağıtımı özelleştirmek için parametre değerlerini geçirirsiniz. |
   
    Tüm kaynak grubu dağıtım projeleri bu temel dosyaları içerir. Diğer projeler diğer işlevleri desteklemek için ek dosyalar içerebilir.

## <a name="customize-the-resource-manager-template"></a>Resource Manager şablonunu özelleştirme
Dağıtmak istediğiniz kaynakları tanımlayan JSON şablonlarını değiştirerek dağıtım projesini özelleştirebilirsiniz. JSON, JavaScript Nesne Gösterimi anlamına gelir ve birlikte çalışması kolay bir sıralanmış veri biçimidir. JSON dosyaları dosyaların üst kısmında başvurduğunuz şemayı kullanır. Şemayı anlamak istiyorsanız indirip analiz edebilirsiniz. Şema, hangi öğelerin geçerli olduğunu, alan türlerini ve biçimlerini, numaralandırılmış değerlerin olası değerlerini ve benzer konuları tanımlar. Resource Manager şablonu bileşenleri hakkında daha fazla bilgi edinmek için [Azure Resource Manager şablonları yazma](resource-group-authoring-templates.md).

Şablonunuzda çalışmak için **WebSiteSQLDatabase.json** dosyasını açın.

Visual Studio düzenleyicisi, Resource Manager şablonu düzenleme konusunda size yardımcı olan araçlar sağlar. **JSON Ana Hattı** penceresi, şablonunuzda tanımlanan bileşenleri görmenizi kolaylaştırır.

![JSON ana hattını göster](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-json-outline.png)

Ana hattaki herhangi bir bileşeni seçtiğinizde, şablonun ilgili parçasına gidersiniz ve ilgili JSON vurgulanır.

![JSON’a gitme](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/navigate-json.png)

JSON Ana Hattı penceresinin üst tarafında bulunan **Kaynak Ekle** düğmesini seçerek veya **kaynaklar**’a sağ tıklayıp **Yeni Kaynak Ekle**’yi seçerek yeni kaynak ekleyebilirsiniz.

![kaynak ekle](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-resource.png)

Bu öğreticide, **Depolama Hesabı**’nı seçin ve bir ad verin. 11 karakterden uzun olmayan ve yalnızca sayı ile küçük harf içeren bir ad belirtin.

![depolama ekleme](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-storage.png)

Yalnızca kaynak eklenmediğini, aynı zamanda depolama hesabı türü için bir parametre ve depolama hesabı adı bir değişken eklendiğini unutmayın.

![ana hattı göster](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-new-items.png)

**storageType** parametresi izin verilen türler ve varsayılan tür ile önceden tanımlanmıştır. Bu değerleri bırakabilir veya senaryonuz için düzenleyebilirsiniz. Bu şablon aracılığıyla herkesin **Premium_LRS** depolama hesabı dağıtmasını istemiyorsanız izin verilen türlerden bunu kaldırın. 

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

Visual Studio, şablonu düzenlerken hangi özellikleri kullanabileceğinizi anlamanıza yardımcı olmak için IntelliSense’i kullanmanıza da olanak tanır. Örneğin, App Service planınızın özelliklerini düzenlemek için **HostingPlan** kaynağına gidin ve **resources** için bir değer ekleyin. IntelliSense’in kullanılabilir değerleri gösterdiğini ve bu değerler için bir açıklama sunduğunu unutmayın.

![IntelliSense’i göster](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-intellisense.png)

**numberOfWorkers** değerini 1 olarak ayarlayabilirsiniz.

```json
"properties": {
  "name": "[parameters('hostingPlanName')]",
  "numberOfWorkers": 1
}
```

## <a name="deploy-the-resource-group-project-to-azure"></a>Azure’da Kaynak Grubu projesi dağıtma
Artık, projenizi dağıtmaya hazırsınız. Bir Azure Kaynak Grubu projesi dağıttığınızda, bunu bir Azure kaynak grubuna dağıtırsınız. Kaynak grubu, ortak bir yaşam döngüsünü paylaşan kaynakların mantıksal bir gruplandırmasıdır.

1. Dağıtım proje düğümünün kısayol menüsünde **Dağıt** > **Yeni** seçeneklerini belirleyin.
   
    ![Dağıt, Yeni Dağıtım menü öğesi](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/deploy.png)
   
    **Kaynak Grubuna Dağıt** iletişim kutusu görüntülenir.
   
    ![Kaynak Grubuna Dağıt İletişim Kutusu](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-deployment.png)
2. **Kaynak Grubu** açılır kutusunda, mevcut bir kaynak grubu seçin veya yeni bir tane oluşturun. Bir kaynak grubu oluşturmak için **Kaynak Grubu** açılır kutusunu açın **Yeni Oluştur** seçeneğini belirleyin.
   
    ![Kaynak Grubuna Dağıt İletişim Kutusu](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/create-new-group.png)
   
    **Kaynak Grubu Oluştur** iletişim kutusu görüntülenir. Grubunuz için bir ad ve konum girin ve **Oluştur** düğmesini seçin.
   
    ![Kaynak Grubu Oluştur İletişim Kutusu](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/create-resource-group.png)
3. **Parametreleri Düzenle** düğmesini seçerek dağıtım parametrelerini düzenleyin.
   
    ![Parametreleri Düzenle düğmesi](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/edit-parameters.png)
4. Boş parametreler için değerleri belirtin ve **Kaydet** düğmesini seçin. **hostingPlanName**, **administratorLogin**, **administratorLoginPassword** ve **databaseName** boş parametrelerdir.
   
    **hostingPlanName**, oluşturulacak [App Service planı](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) için bir ad belirtir. 
   
    **administratorLogin**, SQL Server yöneticisinin kullanıcı adını belirtir. **sa** veya **admin** gibi yaygın yönetici adlarını kullanmayın. 
   
    **administratorLoginPassword**, SQL Server yöneticisi için bir parola belirtir. **Parolaları parametre dosyasına düz metin olarak kaydet** seçeneği güvenli değildir; bu nedenle bu seçeneği belirlemeyin. Parola düz metin olarak kaydedilmediğinden dağıtım sırasında bu parolayı yeniden belirtmeniz gerekecektir. 
   
    **databaseName**, oluşturulacak veritabanı için bir ad belirtir. 
   
    ![Parametreleri Düzenle İletişim Kutusu](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/provide-parameters.png)
5. Projeyi Azure’da dağıtmak için **Dağıt** düğmesini seçin. Visual Studio örneğinin dışında bir PowerShell konsolu açılır. İstendiğinde PowerShell konsolunda SQL Server yönetici parolasını girin. **PowerShell konsolunuz, diğer öğelerin arkasına gizlenmiş veya görev çubuğunda simge haline getirilmiş olabilir.** Bu konsolu arayın ve parolayı belirtmek için seçin.
   
   > [!NOTE]
   > Visual Studio, Azure PowerShell cmdlet'lerini yüklemenizi isteyebilir. Kaynak gruplarını başarıyla dağıtmak için Azure PowerShell cmdlet'lerini ihtiyacınız vardır. İstenirse, bunları yükleyin.
   > 
   > 
6. Dağıtım birkaç dakika sürebilir. **Çıktı** pencerelerinde dağıtımın durumunu görürsünüz. Dağıtım tamamlandığında son ileti aşağıdakine benzer bir ifadeyle dağıtımın başarılı olduğunu belirtir:
   
        ... 
        18:00:58 - Successfully deployed template 'websitesqldatabase.json' to resource group 'DemoSiteGroup'.
7. Bir tarayıcıda [Azure portal](https://portal.azure.com/)’ı açın ve hesabınızda oturum açın. Kaynak grubunu görmek için **Kaynak grupları**’nu ve dağıttığınız kaynak grubunu seçin.
   
    ![grup seçme](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/select-group.png)
8. Dağıtılan tüm kaynakları görürsünüz. Depolama hesabı adının, ilgili kaynağı eklerken belirttiğiniz adla tam olarak aynı olmadığına dikkat edin. Depolama hesabı benzersiz olmalıdır. Şablon benzer bir ad belirtmek üzere belirttiğiniz ada otomatik olarak bir karakter dizesi ekler. 
   
    ![kaynakları göster](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-deployed-resources.png)
9. Değişiklik yapar ve projenizi yeniden dağıtmak isterseniz, Azure kaynak grubu projesinin kısayol menüsünden mevcut kaynak grubunu seçin. Kısayol menüsünde, **Dağıt**’ı ve ardından dağıttığınız kaynak grubunu seçin.
   
    ![Dağıtılan Azure kaynak grubu](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/redeploy.png)

## <a name="deploy-code-with-your-infrastructure"></a>Altyapınızla kodları dağıtma
Bu noktada, uygulamanız için altyapı dağıttınız, ancak proje ile dağıtılan gerçek bir kod yoktur. Bu makalede bir web uygulaması ve SQL Database tablolarını dağıtım sırasında nasıl dağıtacağınız gösterilir. Bir web uygulaması yerine bir Sanal Makine dağıtıyorsanız, dağıtımının bir parçası olarak bazı kodlar çalıştırmak isteyebilirsiniz. Bir web uygulaması için kod dağıtma veya Sanal Makine kurma işlemi neredeyse aynıdır.

1. Visual Studio çözümünüze bir proje ekleyin. Çözüme sağ tıklayın ve **Ekle** > **Yeni Proje** öğesini seçin.
   
    ![proje ekleme](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-project.png)
2. Bir **ASP.NET Web Uygulaması** oluşturun. 
   
    ![web uygulaması ekleme](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-app.png)
3. **MVC** öğesini seçin.
   
    ![MVC’yi seçme](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/select-mvc.png)
4. Visual Studio web uygulamanızı oluşturduktan sonra her iki projeyi de çözümde görürsünüz.
   
    ![projeleri göster](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-projects.png)
5. Bundan böyle kaynak grubu projenizin yeni projeyi tanıdığından emin olmanız gerekir. Kaynak grubu projenize (AzureResourceGroup1) geri dönün. **Başvurular**’a sağ tıklayın ve **Başvuru Ekle**’yi seçin.
   
    ![başvuru ekleme](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-new-reference.png)
6. Oluşturduğunuz web uygulaması projesini seçin.
   
    ![başvuru ekleme](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-reference.png)
   
    Bir başvuru ekleyerek, web uygulama projesini kaynak grubu projesine bağlar ve otomatik olarak üç anahtar özellik ayarlamış olursunuz. Bu özellikleri başvurunun **Özellikler** penceresinde görürsünüz.
   
      ![başvuruya bakma](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/see-reference.png)
   
    Özellikler şunlardır:
   
   * **Ek Özellikler**, Azure Depolama’ya gönderilen web dağıtımı paketini hazırlama konumunu içerir. Klasörü (ExampleApp) ve dosyayı (package.zip) not edin. Uygulamayı dağıtırken parametre olarak ileteceğiniz için bu değerleri bilmeniz gerekir. 
   * **Dosya Yolu Ekle** paketin oluşturulduğu yerin yolunu içerir. **Hedefleri Ekle** dağıtımın yürüttüğü komutu içerir. 
   * **Build;Package** varsayılan değeri, dağıtımın bir web dağıtımı paketi (package.zip) oluşturmasını sağlar.  
     
     Dağıtım paketi oluşturmak için gereken bilgileri özelliklerden elde ettiği için bir yayımlama profili gerekmez.
7. WebSiteSQLDatabase.json dosyasına geri dönüp şablona bir kaynak ekleyin.
   
    ![kaynak ekle](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-resource-2.png)
8. Bu kez **Web Apps için Web Dağıtımı**’nı seçin. 
   
    ![web dağıtımı ekleme](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-web-deploy.png)
9. Kaynak grubu projenizi kaynak grubuna yeniden dağıtın. Bu defa, bazı yeni parametre bulunur. **_artifactsLocation** ve **_artifactsLocationSasToken** değerleri Visual Studio tarafından otomatik olarak oluşturulduğundan, bunlar için değer girmeniz gerekmez. Ancak, klasör ve dosya adını, dağıtım paketini içeren yola ayarlamanız gerekir (aşağıdaki görüntüde **ExampleAppPackageFolder** ve **ExampleAppPackageFileName** olarak gösterilmiştir). Daha önce başvuru özelliklerinde gördüğünüz değerleri belirtin (**ExampleApp** ve **package.zip**).
   
    ![web dağıtımı ekleme](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/set-new-parameters.png)
   
    Bu kaynak grubu ile dağıtılmış bir **Yapıt depolama hesabı** seçin.
10. Dağıtım tamamlandıktan sonra portalda web uygulamanızı seçin. Yeni siteye göz atmak için URL’yi seçin.
    
     ![siteye göz atma](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/browse-site.png)
11. Varsayılan ASP.NET uygulamasını başarıyla dağıttığınızdan emin olun.
    
     ![dağıtılmış uygulamayı gösterme](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-deployed-app.png)

## <a name="next-steps"></a>Sonraki adımlar
* Portalı kullanarak kaynaklarınızı yönetme hakkında daha fazla bilgi için bkz. [Azure portalı kullanarak Azure kaynaklarınızı yönetme](resource-group-portal.md).
* Şablonlar hakkında daha fazla bilgi edinmek için bkz. [Azure Resource Manager şablonları yazma](resource-group-authoring-templates.md).

