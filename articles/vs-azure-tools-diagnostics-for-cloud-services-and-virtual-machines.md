---
title: "Azure bulut Hizmetleri ve sanal makineler için tanılama yapılandırma | Microsoft Docs"
description: "Azure cloude Hizmetleri ve sanal makineleri (VM'ler) Visual Studio hata ayıklama için tanılama bilgilerinin nasıl yapılandırılacağı açıklanmaktadır."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: e70cd7b4-6298-43aa-adea-6fd618414c26
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 2516c0eb8ce470577731db9b844d5b9038465477
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="configuring-diagnostics-for-azure-cloud-services-and-virtual-machines"></a>Tanılama Azure bulut Hizmetleri ve sanal makineler için yapılandırma
Bir Azure bulut hizmeti ya da Azure sanal makine sorun giderme gerektiğinde, Visual Studio kullanarak Azure tanılama daha kolay yapılandırabilirsiniz. Azure tanılama sistem verileri ve sanal makineler ve bulut hizmeti çalıştıran sanal makine örnekleri günlük verilerini yakalar ve bu verileri tercih ettiğiniz bir depolama hesabına aktarır. Bkz: [Azure App Service'te web uygulamalarını için tanılama günlüğünü etkinleştirme](app-service-web/web-sites-enable-diagnostic-log.md) Azure'da oturum Tanılama hakkında daha fazla bilgi.

Bu konuda etkinleştirme ve Azure tanılama ve Azure sanal makinelerde aynı zamanda hem önce ve dağıtım sonra Visual Studio yapılandırma gösterilmektedir. Ayrıca, tanılama bilgilerini toplamak için türlerini seçmek nasıl ve toplandıktan sonra bilgilerinin nasıl görüntüleneceğini gösterir.

Azure tanılama aşağıdaki şekillerde yapılandırabilirsiniz:

* Tanılama yapılandırma ayarları aracılığıyla değiştirebilirsiniz **tanılama Yapılandırması** Visual Studio'da iletişim kutusu. Ayarlar diagnostics.wadcfgx (diagnostics.wadcfg Azure SDK 2.4 veya önceki) adlı bir dosyaya kaydedilir. Alternatif olarak, yapılandırma dosyasını doğrudan değiştirebilirsiniz. Dosyayı el ile güncelleştirirseniz, yapılandırma değişikliklerinin sonraki etkili bulut dağıttığınız zaman hizmeti Azure veya hizmet öykünücüsünde çalıştırın.
* Kullanım **Cloud Explorer** veya **Sunucu Gezgini** çalışan bulut hizmeti ya da sanal makine için tanılama ayarları değiştirmek için Visual Studio'da.

## <a name="azure-26-diagnostics-changes"></a>Azure 2.6 tanılama değişiklikleri
Visual Studio'da Azure SDK 2.6 projeleri için aşağıdaki değişiklikler yapıldı. (Bu değişikliklerin Azure SDK'ın sonraki sürümleri için de geçerlidir.)

* Yerel öykünücüsü artık tanılama destekler. Bu tanılama verilerini toplamak ve geliştirme ve Visual Studio'da test ederken, uygulamanızın doğru izlemeleri oluşturuyor olun anlamına gelir. Bağlantı dizesi `UseDevelopmentStorage=true` Azure storage öykünücüsü kullanarak bulut hizmeti projenizi Visual Studio'da çalıştırıyorsanız tanılama veri toplamayı etkinleştirir. Tüm tanılama verilerini (geliştirme depolama) depolama hesabında toplanır.
* Tanılama depolama hesabı bağlantı dizesi (Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString) bir kez daha hizmet yapılandırma (.cscfg) dosyasında depolanır. Azure SDK 2.5 diagnostics.wadcfgx dosyasında tanılama depolama hesabı belirtilmedi.

Azure SDK 2.4 ve önceki bağlantı dizesini nasıl çalıştığı ve nasıl Azure SDK 2.6 ve daha sonra çalıştığı arasında önemli bazı farklar vardır.

* Azure SDK 2.4 ve önceki sürümlerinde, bağlantı dizesi tanılama günlükleri aktarmak için depolama hesabı bilgilerini almak için bir çalışma zamanı tanılama eklenti tarafından kullanıldı.
* Azure SDK 2.6 ve daha sonra tanılama bağlantı dizesi yayımlama sırasında uygun depolama hesap bilgileriyle tanılama uzantısını yapılandırmak için Visual Studio tarafından kullanılır. Bağlantı dizesi, Visual Studio yayımlama için kullanacağı farklı hizmet yapılandırması için farklı depolama hesapları tanımlamanıza olanak sağlar. Ancak, tanılama eklentisi artık (sonra Azure SDK 2.5) kullanılabilir olmadığından, .cscfg dosyası tek başına tanılama uzantısını etkinleştiremezsiniz. Uzantısı ayrı olarak Visual Studio veya PowerShell gibi araçlar aracılığıyla etkinleştirmeniz gerekir.
* Tanılama uzantısını PowerShell ile yapılandırma işlemini basitleştirmek için Visual Studio Paketi çıktısını de tanılama uzantısını her rol için ortak yapılandırma XML içeriyor. Visual Studio tanılama bağlantı dizesi ortak yapılandırmada depolama hesabı bilgilerini doldurmak için kullanır. Genel yapılandırma dosyaları Uzantıları klasöründe oluşturulur ve desen PaaSDiagnostics izleyin. &lt;Rol adı >. PubConfig.xml. Tüm PowerShell tabanlı dağıtımlar, her yapılandırma bir Role eşleştirmek için bu deseni kullanabilirsiniz.
* .Cscfg dosyasındaki bağlantı dizesi tarafından da kullanılan [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) içinde görüntülenebilir tanılama verilere erişmek için **izleme** sekmesi. Bağlantı dizesi, ayrıntılı izleme verileri portalda göstermek için bu hizmeti yapılandırmak için gereklidir.

## <a name="migrating-projects-to-azure-sdk-26-and-later"></a>Azure SDK 2.6 ve daha sonra geçirme projeleri
Ardından .wadcfgx dosyasında belirtilen tanılama depolama hesabı varsa Azure SDK 2.5-Azure SDK 2.6 veya sonraki sürümleri geçirilirken var. kalır. Farklı depolama hesapları farklı depolama yapılandırmaları için kullanma esnekliğini yararlanmak için bağlantı dizesi projenize el ile eklemeniz gerekir. Azure SDK 2.4 veya daha önceki Azure SDK 2.6 proje geçiş, tanılama bağlantı dizeleri korunur. Ancak, nasıl bağlantı dizeleri Azure SDK 2.6 belirtildiği şekilde önceki bölümde davranılır değişiklikler lütfen unutmayın.

### <a name="how-visual-studio-determines-the-diagnostics-storage-account"></a>Visual Studio tanılama depolama hesabı nasıl belirler
* Bir tanılama bağlantı dizesi .cscfg dosyasında belirtilmediği takdirde, Visual Studio yayımlarken ve genel yapılandırma xml dosyalarını paketlemesi sırasında oluştururken tanılama uzantısını yapılandırmak için kullanır.
* Bir tanılama bağlantı dizesi .cscfg dosyasında belirtilirse, ardından Visual Studio .wadcfgx dosyasında belirtilen depolama hesabı yayımlama ve genel yapılandırma xml dosyalarını oluşturmak tanılama uzantısını yapılandırmak üzere kullanmaya geri döner paketleme olduğunda.
* .Cscfg dosyası tanılama bağlantı dizesinde .wadcfgx dosya depolama hesabında daha önceliklidir. Bir tanılama bağlantı dizesi .cscfg dosyasında belirtilmediği takdirde, Visual Studio kullanan ve .wadcfgx depolama hesabında yok sayar.

### <a name="what-does-the-update-development-storage-connection-strings-checkbox-do"></a>"Güncelleştirme geliştirme storage bağlantı dizelerini..." yaptığı onay kutusu musunuz?
Onay kutusunu **güncelleştirme geliştirme storage bağlantı dizelerini tanılama ve önbelleğe alma için Microsoft Azure depolama hesabı kimlik bilgileriyle Microsoft Azure yayımlama sırasında** tüm geliştirme güncelleştirmek için kullanışlı bir yöntem sunar Yayımlama sırasında belirtilen Azure depolama hesabı ile depolama hesabı bağlantı dizeleri.

Örneğin, bu onay kutusunu seçin ve tanılama bağlantı dizesini belirtir varsayalım `UseDevelopmentStorage=true`. Projeyi Azure'da yayımlarken, Visual Studio Yayımlama Sihirbazı'nda belirtilen depolama hesabıyla tanılama bağlantı dizesi otomatik olarak güncelleştirir. Gerçek depolama hesabı tanılama bağlantı dizesi olarak belirtilmişse, ancak, ardından o hesabı yerine kullanılır.

## <a name="diagnostics-functionality-differences-between-azure-sdk-24-and-earlier-and-azure-sdk-25-and-later"></a>Tanılama işlevleri farklılıkları Azure SDK 2.4 ve önceki ve Azure SDK 2,5 ve üzeri
Projenizi Azure SDK 2.4 Azure SDK 2.5 veya sonraki bir sürümüne yükseltiyorsanız, aşağıdaki tanılama işlevleri farklılıkları göz önünde bulundurmanız gerekir.

* **Yapılandırma API'leri dışıdır** – tanılama program yapılandırması Azure SDK 2.4 veya önceki sürümlerde kullanılabilir, ancak Azure SDK 2.5 ve daha sonra kullanım dışı bırakılmıştır. Tanılama yapılandırmanızı kodda şu anda tanımlanmış olması durumunda, bu ayarları çalışmaya devam Diagnostics sırayla geçirilen proje en baştan yeniden yapılandırmanız gerekir. Tanılama yapılandırması için Azure SDK 2.4 diagnostics.wadcfg ve diagnostics.wadcfgx ve sonraki sürümler için Azure SDK 2.5 dosyasıdır.
* **Bulut hizmeti uygulamaları için tanılama yalnızca rol düzeyinde örnek düzeyinde yapılandırılabilir.**
* **Uygulamanızı dağıtma her zaman, tanılama yapılandırması güncelleştirilir** – tanılama yapılandırmanızı Server Explorer'dan değiştirirseniz ve uygulamanızı yeniden dağıtın bu eşlik sorunlara neden olabilir.
* **Azure SDK 2.5 ve daha sonra kilitlenme bilgi dökümleri tanılama yapılandırma dosyasındaki kodu değil, yapılandırılan** – kodda yapılandırılmış kilitlenme bilgi dökümleri varsa, el ile yapılandırma koddan yapılandırma dosyasına aktarmak çünkü gerekir kilitlenme bilgi dökümleri geçiş sırasında Azure SDK 2.6 aktarılmaz.

## <a name="enable-diagnostics-in-cloud-service-projects-before-deploying-them"></a>Dağıtmadan önce bulut hizmeti projelerinde tanılamayı etkinleştirin
Visual Studio'da dağıtmadan önce hizmet öykünücüsünde çalıştırdığınızda, Azure'da çalışan rolleri tanılama verilerini toplamak seçebilirsiniz. Visual Studio tanılama ayarlarında yapılan tüm değişiklikler diagnostics.wadcfgx yapılandırma dosyasında kaydedilir. Bu yapılandırma ayarları, bulut hizmetinizin dağıttığınızda tanılama verilerini kaydedildiği depolama hesabı belirtin.

[!INCLUDE [cloud-services-wad-warning](../includes/cloud-services-wad-warning.md)]

### <a name="to-enable-diagnostics-in-visual-studio-before-deployment"></a>Visual Studio tanılama dağıtmadan önce etkinleştirmek için
1. İlginizi çeken rolü için kısayol menüsünden seçin **özellikleri**ve ardından **yapılandırma** rolün sekmesinde **özellikleri** penceresi.
2. İçinde **tanılama** bölümünde, olduğundan emin olun **tanılamayı etkinleştir** onay kutusu seçilidir.
   
    ![Tanılamayı etkinleştir seçeneğine erişme](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796660.png)
3. Tanılama verilerin depolanmasını istediğiniz depolama hesabını belirtmek için üç nokta (...) düğmesini seçin. Seçtiğiniz depolama hesabı tanılama verilerinin depolandığı konumun olacaktır.
   
    ![Depolama hesabı belirtin](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796661.png)
4. İçinde **depolama bağlantı dizesi oluştur** iletişim kutusunda, bir Azure aboneliğine Azure Storage öykünücüsü kullanarak bağlanmak istediğiniz veya kimlik bilgileri'el ile girilen olup olmadığını belirtin.
   
    ![Depolama hesabı iletişim kutusu](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796662.png)
   
   * Azure Storage öykünücüsü, bağlantı dizesi için UseDevelopmentStorage ayarlama seçeneğidir Microsoft seçerseniz = true.
   * İsterseniz, abonelik seçeneği, kullanmak istediğiniz Azure aboneliği ve hesap adını seçebilirsiniz. Azure Aboneliklerini yönetmek üzere hesapları Yönet düğmesini seçebilirsiniz.
   * El ile girilen kimlik bilgileri seçeneği seçerseniz, kullanmak istediğiniz Azure hesabı anahtarı ve adını girmeniz istenir.
5. Seçin **yapılandırma** görüntülemek için düğmesini **tanılama Yapılandırması** iletişim kutusu. Her sekme (dışında **genel** ve **günlük dizinleri**) toplamak bir tanılama veri kaynağını temsil eder. Varsayılan sekme **genel**, aşağıdaki tanılama veri toplama seçeneklerini sunar: **yalnızca hatalar**, **tüm bilgileri**, ve **özel plan**. Varsayılan seçenek **yalnızca hatalar**, uyarı veya izleme iletileri aktarmaz çünkü en az miktarda depolama alır. Tüm bilgileri seçeneği bilgilerin çoğu aktarır ve, bu nedenle, en pahalı depolama açısından seçenektir.
   
    ![Azure tanılama ve yapılandırma etkinleştir](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758144.png)
6. Bu örnek için select **özel plan** toplanan verileri özelleştirebileceğiniz şekilde seçeneği.
7. **MB Disk kotası** kutusu ayırmak istediğiniz depolama hesabınız için Tanılama verileri ne kadar alan belirtir. İsterseniz varsayılan değeri değiştirebilirsiniz.
8. Her bir sekmede diagnostics veri toplamak istediğiniz seçin, **etkinleştirmek Aktarım, <log type>**  onay kutusu. Örneğin, uygulama günlüklerini toplamak istiyorsanız seçin **etkinleştirmek uygulama günlüklerini aktarımını** onay kutusunu **uygulama günlüklerini** sekmesi. Ayrıca, her bir tanılama veri türü tarafından gerekli diğer bilgileri belirtin. Bölümüne bakın **tanılama veri kaynakları yapılandırma** bu konuda daha sonra her bir sekmede yapılandırma bilgileri.
9. İstediğiniz tüm Tanılama verileri koleksiyonu etkinleştirdikten sonra Seç **Tamam** düğmesi.
10. Azure bulut hizmeti projenizi Visual Studio'da her zamanki gibi çalıştırın. Uygulamanızı kullanırken, etkin günlük bilgilerini belirttiğiniz Azure depolama hesabı kaydedilir.

## <a name="enable-diagnostics-in-azure-virtual-machines"></a>Azure sanal makinelerde tanılamayı etkinleştirin
Visual Studio'da Azure sanal makineleri için tanılama verilerini toplamak seçebilirsiniz.

### <a name="to-enable-diagnostics-in-azure-virtual-machines"></a>Azure sanal makinelerde tanılama etkinleştirmek için
1. İçinde **Sunucu Gezgini**, Azure düğümü seçin ve henüz bağlıysanız Azure aboneliğinize bağlanma.
2. Genişletme **sanal makineleri** düğümü. Yeni bir sanal makine oluşturun veya zaten var olan birini seçin.
3. İlginizi çeken sanal makine için kısayol menüsünden seçin **yapılandırma**. Bu sanal makine yapılandırma iletişim kutusu gösterir.
   
    ![Bir Azure sanal makinesini yapılandırma](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796663.png)
4. Henüz yüklü değilse, Microsoft İzleme Aracısı tanılama uzantısını ekleyin. Bu uzantı, Azure sanal makinesi için tanılama veri toplamak olanak tanır. Yüklü uzantınız listede kullanılabilir uzantı açılır menü Seç ve Microsoft İzleme Aracısı Tanılama'yı seçin.
   
    ![Bir Azure sanal makine uzantısı yükleniyor](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC766024.png)
   
   > [!NOTE]
   > Diğer tanılama uzantıları, sanal makineleriniz için kullanılabilir. Daha fazla bilgi için bkz: Azure VM uzantıları ve özellikleri.
   > 
   > 
5. Seçin **Ekle** uzantısı ve görünüm eklemek için düğmeyi kendi **tanılama Yapılandırması** iletişim kutusu.
6. Seçin **yapılandırma** bir depolama hesabı belirtin ve ardından düğmesini **Tamam** düğmesi.
   
    Her sekme (dışında **genel** ve **günlük dizinleri**) toplamak bir tanılama veri kaynağını temsil eder.
   
    ![Azure tanılama ve yapılandırma etkinleştir](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758144.png)
   
    Varsayılan sekme **genel**, aşağıdaki tanılama veri toplama seçeneklerini sunar: **yalnızca hatalar**, **tüm bilgileri**, ve **özel plan**. Varsayılan seçenek **yalnızca hatalar**, uyarı veya izleme iletileri aktarmaz çünkü en az miktarda depolama alır. **Tüm bilgileri** seçeneği en bilgileri aktarır ve bu nedenle, depolama açısından en ucuz seçeneği oluşur.
7. Bu örnek için select **özel plan** toplanan verileri özelleştirebileceğiniz şekilde seçeneği.
8. **MB Disk kotası** kutusu ayırmak istediğiniz depolama hesabınız için Tanılama verileri ne kadar alan belirtir. İsterseniz varsayılan değeri değiştirebilirsiniz.
9. Her bir sekmede diagnostics veri toplamak istediğiniz seçin, **etkinleştirmek Aktarım, <log type>**  onay kutusu.
   
    Örneğin, uygulama günlüklerini toplamak istiyorsanız seçin **etkinleştirmek uygulama günlüklerini aktarımını** onay kutusunu **uygulama günlüklerini** sekmesi. Ayrıca, her bir tanılama veri türü tarafından gerekli diğer bilgileri belirtin. Bölümüne bakın **tanılama veri kaynakları yapılandırma** bu konuda daha sonra her bir sekmede yapılandırma bilgileri.
10. İstediğiniz tüm Tanılama verileri koleksiyonu etkinleştirdikten sonra Seç **Tamam** düğmesi.
11. Güncelleştirilmiş Projeyi kaydedin.
    
     Bir ileti görürsünüz **Microsoft Azure etkinlik günlüğü** penceresi sanal makine güncelleştirildi.

## <a name="configure-diagnostics-data-sources"></a>Tanılama veri kaynaklarını yapılandırma
Tanılama veri toplama etkinleştirdikten sonra toplamak istediğiniz tam olarak hangi veri kaynaklarını ve hangi bilgilerin toplandığı seçebilirsiniz. Aşağıdaki sekmeleri listesidir **tanılama Yapılandırması** iletişim kutusu ve her hangi bir yapılandırma seçeneği anlamına gelir.

### <a name="application-logs"></a>Uygulama günlükleri
**Uygulama günlüklerini** bir web uygulaması tarafından üretilen tanılama bilgilerini içerir. Uygulama günlüklerini yakalama isteyip istemediğinizi seçin **etkinleştirmek uygulama günlüklerini aktarımını** onay kutusu. Artırabilir ya da depolama hesabınıza değiştirerek uygulama günlüklerini aktarıldığını zaman dakika sayısını azaltmak **aktarım süresi (dak)** değeri. Ayrıca, günlük düzeyi değeri ayarlayarak günlüğünde yakalanan bilgi miktarını değiştirebilirsiniz. Örneğin, seçebileceğiniz **ayrıntılı** seçin ya da daha fazla bilgi almak için **kritik** yalnızca kritik hataları yakalamak için. Uygulama günlüklerini yayar belirli tanılama sağlayıcısı varsa, bunları sağlayıcının GUID olarak ekleyerek yakalayabilirsiniz **sağlayıcı GUID** kutusu.

  ![Uygulama günlükleri](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758145.png)

  Bkz: [Azure App Service'te web uygulamalarını için tanılama günlüğünü etkinleştirme](app-service-web/web-sites-enable-diagnostic-log.md) uygulama günlükleri hakkında daha fazla bilgi.

### <a name="windows-event-logs"></a>Windows olay günlükleri
Windows olay günlüklerini yakalama isteyip istemediğinizi seçin **etkinleştirmek aktarımı, Windows olay günlüklerini** onay kutusu. Artırabilir ya da depolama hesabınıza değiştirerek olay günlüklerini aktarıldığını zaman dakika sayısını azaltmak **aktarım süresi (dak)** değeri. İzlemek istediğiniz olay türleri için onay kutularını seçin.

  ![Olay Günlükleri](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796664.png)

Azure SDK 2.6 veya sonraki sürümünü kullanıyorsanız ve bir özel veri kaynağı belirtmek istiyorsanız bu alana giriş  **<Data source name>**  metin kutusuna ve ardından **Ekle** yanında düğmesi. Veri kaynağı diagnostics.cfcfg dosyasına eklenir.

Azure SDK 2.5 kullanıyorsanız ve bir özel veri kaynağı belirtmek istiyorsanız, ona ekleyebilirsiniz `WindowsEventLog` diagnostics.wadcfgx bölümünü dosya, aşağıdaki örnekte olduğu gibi.

```
<WindowsEventLog scheduledTransferPeriod="PT1M">
   <DataSource name="Application!*" />
   <DataSource name="CustomDataSource!*" />
</WindowsEventLog>
```
### <a name="performance-counters"></a>Performans sayaçları
Performans sayacı bilgileri sistem engelleri bulun ve sistem ve uygulama performansının ayarını yardımcı olabilir. Bkz: [oluşturma ve bir Azure uygulamasında performans sayaçlarını kullan](https://msdn.microsoft.com/library/azure/hh411542.aspx) daha fazla bilgi için. Performans sayaçlarını yakalamak isteyip istemediğinizi seçin **etkinleştirmek performans sayaçları aktarımını** onay kutusu. Artırabilir ya da depolama hesabınıza değiştirerek olay günlüklerini aktarıldığını zaman dakika sayısını azaltmak **aktarım süresi (dak)** değeri. İzlemek istediğiniz performans sayaçları için onay kutularını seçin.

  ![Performans Sayaçları](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758147.png)

Listede bir performans sayacı izlemek için önerilen sözdizimini kullanarak girin ve ardından **Ekle** düğmesi. Sanal makinedeki işletim sistemini izleyebilirsiniz hangi performans sayaçlarını belirler. Sözdizimi hakkında daha fazla bilgi için bkz: [sayaç yolu belirterek](https://msdn.microsoft.com/library/windows/desktop/aa373193.aspx).

### <a name="infrastructure-logs"></a>Altyapı günlükleri
Uzaktan erişim modülü ve RemoteForwarder modülünün Azure Tanılama Altyapısı hakkında bilgiler içeren, altyapı günlükleri yakalama isteyip istemediğinizi seçin **etkinleştirmek altyapı günlükleri aktarımını** denetleyin bir kutu. Artırabilir ya da aktarım süresi (dak) değerini değiştirerek depolama hesabınıza günlükleri zaman aktarılır dakika sayısını azaltın.

  ![Tanılama altyapı günlükleri](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758148.png)

  Bkz: [kullanarak Azure tanılama tarafından günlüğü verilerini toplamak](https://msdn.microsoft.com/library/azure/gg433048.aspx) daha fazla bilgi için.

### <a name="log-directories"></a>Günlük dizinleri
Internet Information Services (IIS) istekleri için günlük dizinlerinden toplanan verileri içeren, günlük dizinleri yakalamak istiyorsanız başarısız isteklerin veya seçtiğiniz klasörleri seçin **etkinleştirmek günlük dizinleri aktarımını** onay kutusunu seçin. Artırabilir ya da depolama hesabınıza değiştirerek günlükleri aktarıldığını zaman dakika sayısını azaltmak **aktarım süresi (dak)** değeri.

Gibi toplamak istediğiniz günlükleri kutuları seçebileceğiniz **IIS günlüklerini** ve **isteği başarısız oldu** günlükleri. Varsayılan depolama kapsayıcısını adları sağlanır, ancak isterseniz adlarını değiştirebilirsiniz.

Ayrıca, herhangi bir klasörden günlükleri yakalayabilirsiniz. Yalnızca yolu belirtin **mutlak dizin günlüğünden** bölümünde ve ardından **Dizin Ekle** düğmesi. Belirtilen kapsayıcı günlükleri yakalanan.

  ![Günlük dizinleri](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796665.png)

### <a name="etw-logs"></a>ETW günlükleri
Kullanırsanız [Windows için olay izleme](https://msdn.microsoft.com/library/windows/desktop/bb968803\(v=vs.85\).aspx) (ETW) ve ETW günlükleri yakalamak istediğiniz seçin **etkinleştirmek ETW günlükleri aktarımını** onay kutusu. Artırabilir ya da depolama hesabınıza değiştirerek günlükleri aktarıldığını zaman dakika sayısını azaltmak **aktarım süresi (dak)** değeri.

Olaylar, olay kaynakları ve belirttiğiniz olay bildirimleri yakalanır. Bir olay kaynağı belirtmek için bir ad girin **olay kaynakları** bölümünde ve ardından **olay kaynağı Ekle** düğmesi. Benzer şekilde, bir olay bildiriminde belirtebilirsiniz **olay bildirimlerini** bölümünde ve ardından **ekleme olay bildirimi** düğmesi.

  ![ETW günlükleri](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC766025.png)

  ETW framework [System.Diagnostics.aspx] (https://msdn.microsoft.com/library/system.diagnostics (v=vs.110) ad alanı. sınıflarıyla ASP.NET desteklenir Devralır ve standart [System.Diagnostics.aspx] genişletir Microsoft.WindowsAzure.Diagnostics ad alanı (https://msdn.microsoft.com/library/system.diagnostics (v=vs.110) sınıfları, [System.Diagnostics.aspx] (https kullanımını etkinleştirir : Azure ortamı günlük Framework'te olarak //msdn.microsoft.com/library/system.diagnostics(v=vs.110). Daha fazla bilgi için bkz: [alın, Denetim günlüğü ve izleme Microsoft Azure](https://msdn.microsoft.com/magazine/ff714589.aspx) ve [Azure Cloud Services ve sanal makineleri etkinleştirme tanılamada](cloud-services/cloud-services-dotnet-diagnostics.md).

### <a name="crash-dumps"></a>Kilitlenme bilgi dökümleri
Hakkında bilgi yakalamak istiyorsanız rol örneği zaman çöküyor, seçin **etkinleştirmek kilitlenme dökümleri aktarımını** onay kutusu. (ASP.NET çoğu özel durumları işler olduğundan, bu yalnızca çalışan rolleri için genellikle kullanışlıdır.) Artırabilir ya da değiştirerek kilitlenme bilgi dökümleri için ayrılan depolama alanı yüzdesini azaltmak **Directory kota (%)** değeri. Burada kilitlenme bilgi dökümleri depolanır ve yakalamak istediğiniz seçebilirsiniz depolama kapsayıcısı değiştirebileceğiniz bir **tam** veya **Mini** dökümü.

Şu anda izlenmekte olan işlemler listelenmiştir. Yakalamak istediğiniz işlemler için onay kutularını seçin. Başka bir işlem listesine eklemek için işlem adı girin ve ardından **ekleme işlemi** düğmesi.

  ![Kilitlenme bilgi dökümleri](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC766026.png)

  Bkz: [alın, Denetim günlüğü ve izleme Microsoft azure'da](https://msdn.microsoft.com/magazine/ff714589.aspx) ve [Microsoft Azure tanılama bölümü 4: özel günlük kaydı bileşenleri ve Azure tanılama 1.3 değişiklikleri](http://justazure.com/microsoft-azure-diagnostics-part-4-custom-logging-components-azure-diagnostics-1-3-changes/) daha fazla bilgi için.

## <a name="view-the-diagnostics-data"></a>Tanılama verilerini görüntüleyin
Bir bulut hizmeti veya bir sanal makine için tanılama verilerini derledik sonra görüntüleyebilirsiniz.

### <a name="to-view-cloud-service-diagnostics-data"></a>Bulut hizmeti tanılama verilerini görüntülemek için
1. Normal olarak, bulut hizmetinize dağıtın ve ardından çalıştırın.
2. Tanılama veri depolama hesabınızdaki Visual Studio'nun oluşturduğu bir rapor veya tablolar içinde görüntüleyebilirsiniz. Verileri bir raporu görüntülemek için açın **Cloud Explorer** veya **Sunucu Gezgini**ilginizi çeken rolü için düğümünün kısayol menüsünü açın ve ardından **görünüm tanılama verilerini**.
   
    ![Tanılama verilerini görüntüle](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC748912.png)
   
    Kullanılabilir veri gösteren bir rapor görüntülenir.
   
    ![Visual Studio'da Microsoft Azure tanılama raporu](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796666.png)
   
    En son verileri görünmüyorsa, geçmesini transfer dönemi için beklemeniz gerekebilir.
   
    Seçin **yenileme** hemen verileri güncelleştirmek için bağlantı veya bir zaman aralığı seçin **otomatik yenileme** açılır liste kutusunu otomatik olarak güncelleştirilen verileri. Hata verileri dışa aktarmayı seçin **CSV'ye aktar** elektronik tabloda açabilir bir virgülle ayrılmış değer dosyası oluşturmak için düğmesi.
   
    İçinde **Cloud Explorer** veya **Sunucu Gezgini**, dağıtımla ilişkili depolama hesabını açın.
3. Tanılama tabloları Tablo Görüntüleyicisi'nde açın ve toplanan verileri gözden geçirin. Özel günlükler ve IIS günlüklerini bir blob kapsayıcısını açabilirsiniz. Aşağıdaki tabloda inceleyerek, sizi ilgilendiren verileri içeren tablo veya blob kapsayıcısına bulabilirsiniz. Bu günlük dosyası için veri yanı sıra tablo EventTickCount, Deploymentıd, rol ve RoleInstance hangi sanal makine ve rol verileri oluşturulan tanımlamanıza yardımcı olması için girişleri ve ne zaman. 
   
   | Tanılama veri | Açıklama | Konum |
   | --- | --- | --- |
   | Uygulama günlükleri |System.Diagnostics.Trace sınıfı yöntemlerinin çağırarak kodunuzu oluşturur günlüğe kaydedilir. |WADLogsTable |
   | Olay Günlükleri |Windows olay günlüklerini sanal makinelerde bu veriler arasındadır. Windows bu günlüklerinde bilgilerini saklar, ancak uygulamalar ve hizmetler de hatalarını raporlamak için kullanın veya bilgileri günlüğe kaydeder. |WADWindowsEventLogsTable |
   | Performans Sayaçları |Sanal makinede kullanılabilir herhangi bir performans sayacı hakkında veri toplar. İşletim sistemi, bellek kullanımı ve işlemci süresi gibi birçok istatistikleri dahil performans sayaçları sağlar. |WADPerformanceCountersTable |
   | Altyapı günlükleri |Bu günlükler, tanılama altyapı kendisini üretilir. |WADDiagnosticInfrastructureLogsTable |
   | IIS günlükleri |Bu günlükler web isteklerini kaydedin. Bulut hizmetiniz bir miktarda trafiği alır, bu günlükleri toplamak ve yalnızca gerektiğinde bu verileri depolamak için oldukça uzun olabilir. |İsteği başarısız oldu blob kapsayıcısı IIS wad failedreqlogs bu dağıtım, rol ve örneği için bir yol altında altında kaydeder bulabilirsiniz. Tam günlükleri wad IIS logfiles altında bulabilirsiniz. Her dosya için girişler WADDirectories tablosunda oluşturulur. |
   | Kilitlenme bilgi dökümleri |Bu bilgiler ikili bulut hizmetinizin işlemin (genellikle çalışan rolü) sağlar. |wad crush dökümleri blob kapsayıcısı |
   | Özel günlük dosyaları |Günlükleri, önceden tanımlanmış veri. |Depolama hesabınızı kodda özel günlük dosyalarının konumu belirtebilirsiniz. Örneğin, bir özel blob kapsayıcısını belirtebilirsiniz. |
4. Herhangi bir türde veriler kesildi, bu verileri için arabellek boyutu artırmayı deneyebilirsiniz türü veya veri depolama hesabınıza aktarımları sanal makineden arasındaki aralığı kısaltmayı.
5. (isteğe bağlı) Bazen genel depolama maliyetleri azaltmak için depolama hesabından verilerini temizle.
6. Tam bir dağıtım yaptığınızda, diagnostics.cscfg dosyası (.wadcfgx için Azure SDK 2.5) Azure'da güncelleştirilir ve bulut hizmetiniz tanılama yapılandırması değişiklikleri alır. .Cscfg dosyası, bunun yerine, var olan bir dağıtıma güncelleştirirseniz, Azure'da güncelleştirilmez. Tanılama ayarları, sonraki bölümde yer alan adımları izleyerek, ancak hala değiştirebilirsiniz. Tam dağıtımını gerçekleştirme ve var olan bir dağıtımını güncelleştirme hakkında daha fazla bilgi için bkz: [Azure uygulaması Yayımlama Sihirbazı](vs-azure-tools-publish-azure-application-wizard.md).

### <a name="to-view-virtual-machine-diagnostics-data"></a>Sanal makine tanılama verilerini görüntülemek için
1. Sanal makine için kısayol menüsünden seçin **tanılama verilerini görüntüle**.
   
    ![Azure sanal makinesinde tanılama verilerini görüntüle](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC766027.png)
   
    Bu açılır **tanılama özeti** penceresi.
   
    ![Azure sanal makinesi tanılama özeti](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796667.png)  
   
    En son verileri görünmüyorsa, geçmesini transfer dönemi için beklemeniz gerekebilir.
   
    Seçin **yenileme** hemen verileri güncelleştirmek için bağlantı veya bir zaman aralığı seçin **otomatik yenileme** açılır liste kutusunu otomatik olarak güncelleştirilen verileri. Hata verileri dışa aktarmayı seçin **CSV'ye aktar** elektronik tabloda açabilir bir virgülle ayrılmış değer dosyası oluşturmak için düğmesi.

## <a name="configure-cloud-service-diagnostics-after-deployment"></a>Dağıtımdan sonra bulut hizmeti tanılama Yapılandır
Hizmet, zaten çalışıyor, belirtmediğiniz veri toplamak isteyebilirsiniz Bulutu ile ilgili bir sorun çalışıyoruz, ilk olarak rolü dağıttığınız önce. Bu durumda, sunucu Gezgini'nde ayarları kullanarak bu verileri toplamak için başlatabilirsiniz. Tek bir örnek veya tüm örnekleri için tanılama tanılama yapılandırması iletişim kutusu örneği veya rol için kısayol menüsünden açmak mı bağlı olarak bir rolü yapılandırabilirsiniz. Rol düğümü yapılandırırsanız, herhangi bir değişiklik tüm örneklerine uygulanır. Örnek düğüm yapılandırırsanız, herhangi bir değişiklik yalnızca bu örnek için geçerlidir.

### <a name="to-configure-diagnostics-for-a-running-cloud-service"></a>Çalışan bir bulut hizmeti için tanılama yapılandırmak için
1. Server Explorer'da genişletin **bulut Hizmetleri** düğümünü ve ardından rolü veya incelemek istediğiniz örneği veya her ikisi de bulmaya düğümlerini genişletin.
   
    ![Tanılama yapılandırılıyor](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC748913.png)
2. Bir örnek düğümü ya da rolü düğümü için kısayol menüsünden seçin **güncelleştirme tanılama ayarları**ve toplamak istediğiniz tanılama Ayarları'nı seçin.
   
    Yapılandırma ayarları hakkında daha fazla bilgi için bkz: **tanılama veri kaynakları yapılandırma** bu konuda. Tanılama verilerini görüntüleme hakkında daha fazla bilgi için bkz: **tanılama verilerini görüntülemek** bu konuda.
   
    Veri toplama işlemini değiştirirseniz **Sunucu Gezgini**, bulut hizmetinizin tam olarak yeniden kadar bu değişiklikler etkili olur. Varsayılan kullanırsanız, yayımlama ayarları, değişiklikleri geçersiz kılınmaz, varsayılan yayımlama beri yerine var olan dağıtım güncelleştirme tam yeniden dağıtım yapmak için bir ayardır. Ayarları temizleyin dağıtım sırasında emin olmak için Git **Gelişmiş ayarları** sekmesinde Yayımlama Sihirbazı'nda ve temizleyin **dağıtım güncelleştirme** onay kutusu. Bu onay kutusu işaretli ile yeniden dağıtırken ayarları için olanlar .wadcfgx (veya .wadcfg) dosyasındaki rol için özellikleri Düzenleyicisi aracılığıyla olarak geri. Dağıtımınızı güncelleştirirseniz, Azure eski ayarları tutar.

## <a name="troubleshoot-azure-cloud-service-issues"></a>Azure bulut hizmeti sorunlarını giderme
Yaşıyorsanız "meşgul" durumunda, takılmış bir rolü gibi bulut hizmeti projeleri sorunları sürekli geri dönüştürüldüğünde veya bir iç sunucu hatası oluşturur, araçları ve teknikleri tanılamak ve bu sorunları düzeltmek için kullanabileceğiniz vardır. Ortak sorunlar ve çözümleri belirli örnekleri, yanı sıra bir genel bakış, kavramlar ve tanılamak ve bu tür hataları düzeltmek için kullanılan araçlar, bkz: [Azure PaaS işlem tanılama verilerini](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).

## <a name="q--a"></a>Soru-Cevap
**Arabellek boyutu nedir ve ne kadar büyük olmalıdır?**

Her sanal makine örneği, yerel dosya sisteminde tanılama ne kadar veri depolanabilir kotaları sınırlayın. Ayrıca, her kullanılabilir tanılama veri türü için arabellek boyutu belirtin. Bu arabellek boyutu, veri türü için ayrı bir kota gibi davranır. İletişim kutusunun alt kısmındaki denetleyerek genel kota ve kalan belleğin belirleyebilirsiniz. Daha büyük arabellek ya da daha fazla veri türlerini belirtirseniz, genel kota yaklaşımını. Genel kota diagnostics.wadcfg/.wadcfgx yapılandırma dosyasını değiştirerek değiştirebilirsiniz. Tanılama verileri aynı dosya sistemi, uygulamanızın veri olarak depolanır, uygulamanız çok disk alanı kullanıyorsa, genel tanılama kotasından artırmak döndürmemelidir şekilde.

**Transfer süresi nedir ve ne kadar süreyle olmalıdır?**

Transfer süresi dolduktan veriler arasında yakalar zaman miktarıdır. Her aktarım süresinden sonra verileri yerel dosya sisteminden bir sanal makinede depolama hesabınızdaki tablolara taşınır. Toplanan veri miktarını transfer dönemi sona önce kotayı aşarsa, eski verileri göz ardı edilir. Verilerinizi arabellek boyutu veya genel kota sınırını aştığı için veri kaybı varsa aktarım süresini azaltmak isteyebilirsiniz.

**Hangi saat dilimi zaman damgaları, misiniz?**

Zaman damgaları, bulut hizmeti barındıran veri merkezi yerel saat dilimindedir. Aşağıdaki üç zaman damgası sütunları günlük tablolarda kullanılır.

* **PreciseTimeStamp** olayın ETW zaman damgası. Diğer bir deyişle, istemciden olayı günlüğe kaydeden saati.
* **Zaman damgası** PreciseTimeStamp karşıya yükleme frekansı sınırına yuvarlanır. Bu nedenle, karşıya yükleme frekansı saat 00:17:12 5 dakika ve olay ise, zaman damgası 00:15:00 olacaktır.
* **Zaman damgası** hangi varlık Azure tablosunda oluşturulduğu zaman damgası.

**Maliyetleri nasıl tanılama bilgisi toplarken yönetiyorsunuz?**

Varsayılan ayarları (**günlük düzeyi** kümesine **hata** ve **Transfer dönemi** kümesine **1 dakika**) maliyeti en aza indirmek için tasarlanmıştır. Daha fazla tanılama verisi toplama ya da aktarım süresini azaltmak işlem maliyetleri artırır. Gereksinim ve artık ihtiyacınız olduğunda veri toplamayı devre dışı bırakmak unutmayın daha fazla veri toplama. Her zaman yeniden bile çalışma zamanında önceki bölümde gösterildiği gibi etkinleştirebilirsiniz.

**IIS nasıl isteği başarısız oldu günlükleri toplamak?**

Varsayılan olarak IIS istek başarısız günlükleri toplamak değil. IIS web rolünüz için web.config dosyasını düzenleyin, bunları toplamak üzere yapılandırabilirsiniz.

**İzleme bilgilerini RoleEntryPoint yöntemlerden OnStart gibi alıyorum değil. Ne oldu?**

RoleEntryPoint yöntemlerinin WAIISHost.exe, IIS değil bağlamında denir. Bu nedenle, normalde izlemeyi etkinleştirir uygulanmaz web.config dosyasındaki yapılandırma bilgileri. Bu sorunu çözmek için web rolü projenize .config dosyasına ekleyin ve RoleEntryPoint kodu içeren çıkış bütünleştirilmiş kodun eşleştirilecek dosya adı. Varsayılan web rolü projesinde .config dosyası adı WAIISHost.exe.config olacaktır. Daha sonra bu dosyayı aşağıdaki satırları ekleyin:

```
<system.diagnostics>
  <trace>
      <listeners>
          <add name “AzureDiagnostics” type=”Microsoft.WindowsAzure.Diagnostics.DiagnosticMonitorTraceListener”>
              <filter type=”” />
          </add>
      </listeners>
  </trace>
</system.diagnostics>
```

Şimdi **özellikleri** penceresindeki ayarlayın **çıktı dizinine Kopyala** özelliğine **her zaman Kopyala**.

## <a name="next-steps"></a>Sonraki adımlar
Azure'da oturum Tanılama hakkında daha fazla bilgi için bkz: [Azure Cloud Services ve sanal makineleri etkinleştirme tanılamada](cloud-services/cloud-services-dotnet-diagnostics.md) ve [Azure App Service'te web uygulamalarını için tanılama günlüğünü etkinleştirme](app-service-web/web-sites-enable-diagnostic-log.md).

