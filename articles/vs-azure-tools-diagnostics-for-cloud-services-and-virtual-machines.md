---
title: "aaaConfiguring Azure Cloud Services ve sanal makineler için tanılama | Microsoft Docs"
description: "Açıklar nasıl Azure cloude Hizmetleri ve sanal makineleri (VM'ler) Visual Studio hata ayıklama için tooconfigure tanılama bilgileri."
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
ms.openlocfilehash: 74cdf49413d6d89a84195070dd9d817da2463373
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-diagnostics-for-azure-cloud-services-and-virtual-machines"></a>Tanılama Azure bulut Hizmetleri ve sanal makineler için yapılandırma
Bir Azure bulut hizmeti ya da Azure sanal makineyi tootroubleshoot gerektiğinde, Visual Studio kullanarak Azure tanılama daha kolay yapılandırabilirsiniz. Azure tanılama sistem verileri ve günlük verilerini hello sanal makineler ve bulut hizmeti çalıştıran sanal makine örnekleri yakalar ve bu verileri tercih ettiğiniz bir depolama hesabına aktarır. Bkz: [Azure App Service'te web uygulamalarını için tanılama günlüğünü etkinleştirme](app-service-web/web-sites-enable-diagnostic-log.md) Azure'da oturum Tanılama hakkında daha fazla bilgi.

Bu konu, nasıl gösterir tooenable ve Azure tanılama ve Azure sanal makinelerde aynı zamanda hem önce ve dağıtım sonra Visual Studio yapılandırın. Ayrıca, nasıl gösterir tooselect hello türlerini tanılama bilgileri toocollect ve sonraki tooview hello bilgileri nasıl toplanır.

Azure tanılama yolu izleyerek hello yapılandırabilirsiniz:

* Merhaba aracılığıyla tanılama yapılandırma ayarlarını değiştirebilirsiniz **tanılama Yapılandırması** Visual Studio'da iletişim kutusu. Hello ayarları diagnostics.wadcfgx (diagnostics.wadcfg Azure SDK 2.4 veya önceki) adlı bir dosyaya kaydedilir. Alternatif olarak, hello yapılandırma dosyasını doğrudan değiştirebilirsiniz. Hello dosyayı el ile güncelleştirirseniz, hello yapılandırma değişikliklerinin etkili hello hello bulut hizmeti tooAzure veya hello öykünücüsü çalışma hello hizmetinde dağıtmak sonraki zaman alır.
* Kullanım **Cloud Explorer** veya **Sunucu Gezgini** çalışan bulut hizmeti ya da sanal makine için Visual Studio toochange hello tanılama ayarları içinde.

## <a name="azure-26-diagnostics-changes"></a>Azure 2.6 tanılama değişiklikleri
Visual Studio'da Azure SDK 2.6 projelerde hello aşağıdaki değişiklikler yapıldı. (Bu değişikliklerin Azure SDK'ın toolater sürümleri de geçerlidir.)

* Merhaba yerel öykünücüsü artık tanılama destekler. Bu tanılama verilerini toplamak ve geliştirme ve Visual Studio'da test ederken, uygulamanızın doğru izlemeleri hello oluşturuyor olun anlamına gelir. Merhaba bağlantı dizesi `UseDevelopmentStorage=true` hello Azure storage öykünücüsü kullanarak bulut hizmeti projenizi Visual Studio'da çalıştırıyorsanız tanılama veri toplamayı etkinleştirir. Tüm tanılama verilerini hello (geliştirme depolama) depolama hesabında toplanır.
* Merhaba tanılama depolama hesabı bağlantı dizesi (Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString) bir kez daha hello hizmet yapılandırma (.cscfg) dosyasında depolanır. Azure SDK 2.5 hello diagnostics.wadcfgx dosyasında hello tanılama depolama hesabı belirtilmedi.

Azure SDK 2.4 ve önceki hello bağlantı dizesini nasıl çalıştığı ve nasıl Azure SDK 2.6 ve daha sonra çalıştığı arasında önemli bazı farklar vardır.

* Azure SDK 2.4 ve önceki sürümlerinde, hello bağlantı dizesi çalışma zamanı tanılama günlükleri aktarmak için hello tanılama eklentisi tooget hello depolama hesabı bilgilerini tarafından kullanıldı.
* Azure SDK 2.6 ve daha sonra hello tanılama bağlantı dizesi Visual Studio tooconfigure hello tanılama uzantısını yayımlama sırasında hello uygun depolama hesabı bilgileri ile tarafından kullanılır. Merhaba bağlantı dizesi, Visual Studio yayımlama için kullanacağı farklı hizmet yapılandırması için farklı depolama hesapları tanımlamanıza olanak sağlar. Ancak, Hello tanılama eklentisi artık (sonra Azure SDK 2.5) kullanılabilir olmadığından, hello .cscfg dosyası tek başına hello tanılama uzantısını etkinleştiremezsiniz. Tooenable hello uzantısı ayrı olarak Visual Studio veya PowerShell gibi araçlar aracılığıyla var.
* PowerShell ile Merhaba tanılama uzantısını yapılandırma toosimplify hello işlemi, hello paket çıktı Visual Studio'dan hello genel yapılandırması XML hello tanılama uzantısını her rol için de içerir. Visual Studio hello tanılama bağlantı dizesi toopopulate hello depolama hesabı bilgilerini hello ortak yapılandırmada mevcut kullanır. Merhaba ortak yapılandırma dosyaları hello Uzantıları klasöründe oluşturulur ve hello düzeni PaaSDiagnostics izleyin. &lt;Rol adı >. PubConfig.xml. Tüm temel PowerShell dağıtımları her yapılandırma tooa rolü bu deseni toomap kullanabilirsiniz.
* Merhaba bağlantı dizesi hello .cscfg dosyasında hello tarafından da kullanılan [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) tooaccess hello tanılama verilerini hello görüntülenebilir **izleme** sekmesini hello bağlantı dizesi gereklidir tooconfigure hello hizmet tooshow izleme verilerini hello Portalı'nda ayrıntılı.

## <a name="migrating-projects-tooazure-sdk-26-and-later"></a>Geçirme projeleri tooAzure SDK 2.6 ve sonrası
Ardından Azure SDK 2.5 tooAzure SDK 2.6 den geçirme veya daha sonra hello .wadcfgx dosyasında belirtilen tanılama depolama hesabı olsaydı var. kalır. farklı depolama yapılandırmaları için farklı depolama kullanmanın hello esneklik tootake avantajlarından hesapları, hello bağlantı dizesi tooyour projesi eklemek toomanually sahip olacaksınız. Azure SDK 2.4 veya önceki tooAzure SDK 2.6 proje geçiş, bağlantı dizeleri korunur tanılama hello. Ancak, nasıl bağlantı dizeleri Azure SDK 2.6 belirtildiği şekilde hello önceki bölümde davranılır hello değişiklikler lütfen unutmayın.

### <a name="how-visual-studio-determines-hello-diagnostics-storage-account"></a>Visual Studio hello tanılama depolama hesabı nasıl belirler
* Bir tanılama bağlantı dizesi hello .cscfg dosyasında belirtilmediği takdirde, Visual Studio tooconfigure hello tanılama uzantısını yayımlarken ve hello ortak yapılandırma xml dosyalarını paketlemesi sırasında oluştururken kullanır.
* Bir tanılama bağlantı dizesi hello .cscfg dosyasında belirtilirse, ardından Visual Studio geri yayımlama ve hello ortak oluşturma hello .wadcfgx dosya tooconfigure hello tanılama uzantısını belirtilen toousing hello depolama hesabı döner paketleme yapılandırma xml dosyaları.
* Merhaba tanılama bağlantı dizesi hello .cscfg dosyasında hello depolama hesabı hello .wadcfgx dosyasında daha önceliklidir. Bir tanılama bağlantı dizesi ise hello .cscfg dosyasında belirtilen sonra Visual Studio kullanan ve .wadcfgx hello depolama hesabında yok sayar.

### <a name="what-does-hello-update-development-storage-connection-strings-checkbox-do"></a>Ne "geliştirme storage bağlantı dizelerini güncelleştir..." Merhaba onay kutusu musunuz?
onay kutusunu hello **güncelleştirme geliştirme storage bağlantı dizelerini tanılama ve önbelleğe alma için Microsoft Azure depolama hesabı kimlik bilgilerinizle tooMicrosoft Azure yayımlarken** herhangi bir yöntemdir tooupdate sağlar Yayımlama sırasında belirtilen hello Azure depolama hesabı ile geliştirme depolama hesabı bağlantı dizeleri.

Örneğin, bu onay kutusunu seçin ve hello tanılama bağlantı dizesini belirtir varsayalım `UseDevelopmentStorage=true`. Merhaba proje tooAzure yayımladığınızda, Visual Studio hello tanılama bağlantı dizesi hello Yayımlama Sihirbazı'nda belirtilen hello depolama hesabıyla otomatik olarak güncelleştirir. Gerçek depolama hesabı hello tanılama bağlantı dizesi olarak belirtilmişse, ancak, ardından o hesabı yerine kullanılır.

## <a name="diagnostics-functionality-differences-between-azure-sdk-24-and-earlier-and-azure-sdk-25-and-later"></a>Tanılama işlevleri farklılıkları Azure SDK 2.4 ve önceki ve Azure SDK 2,5 ve üzeri
Projenizi Azure SDK 2.4 tooAzure SDK 2.5 veya sonraki ' yükseltiyorsanız, Tanılama işlevleri farklılıkları aşağıdaki göz hello bulundurmanız gerekir.

* **Yapılandırma API'leri dışıdır** – tanılama program yapılandırması Azure SDK 2.4 veya önceki sürümlerde kullanılabilir, ancak Azure SDK 2.5 ve daha sonra kullanım dışı bırakılmıştır. Tanılama yapılandırmanızı kodda şu anda tanımlanmış olması durumunda, bu ayarları hello geçirilen proje sırada tanılama tookeep çalışmak için en baştan tooreconfigure gerekir. Merhaba tanılama yapılandırması için Azure SDK 2.4 diagnostics.wadcfg ve diagnostics.wadcfgx ve sonraki sürümler için Azure SDK 2.5 dosyasıdır.
* **Bulut hizmeti uygulamaları için tanılama hello rol düzeyinde hello örnek düzeyinde değil yalnızca yapılandırılabilir.**
* **Uygulamanızı dağıtma her zaman hello tanılama yapılandırması güncelleştirilir** – tanılama yapılandırmanızı Server Explorer'dan değiştirirseniz ve uygulamanızı yeniden dağıtın bu eşlik sorunlara neden olabilir.
* **Azure SDK 2.5 ve daha sonra kilitlenme bilgi dökümleri değil kodda hello tanılama yapılandırma dosyasındaki yapılandırılan** – kodda yapılandırılmış kilitlenme bilgi dökümleri varsa, kodu toohello yapılandırma dosyasından toomanually aktarımı hello yapılandırma gerekir. Merhaba kilitlenme dökümleri çünkü hello geçiş tooAzure SDK 2.6 sırasında aktarılmaz.

## <a name="enable-diagnostics-in-cloud-service-projects-before-deploying-them"></a>Dağıtmadan önce bulut hizmeti projelerinde tanılamayı etkinleştirin
Visual Studio'da toocollect tanılama verilerini dağıtmadan önce hello hizmet hello öykünücüsünde çalıştırdığınızda, Azure'da çalışan rolleri için seçebilirsiniz. Visual Studio'da tüm değişiklikleri toodiagnostics ayarlar hello diagnostics.wadcfgx yapılandırma dosyasına kaydedilir. Bu yapılandırma ayarları, bulut hizmetinizin dağıttığınızda tanılama verilerini kaydedildiği hello depolama hesabı belirtin.

[!INCLUDE [cloud-services-wad-warning](../includes/cloud-services-wad-warning.md)]

### <a name="tooenable-diagnostics-in-visual-studio-before-deployment"></a>dağıtımdan önce Visual Studio tooenable tanılama
1. Hello kısayol menüsünde, sizi ilgilendiren hello rol seçin **özellikleri**ve ardından hello seçin **yapılandırma** hello rolün sekmesinde **özellikleri** penceresi.
2. Merhaba, **tanılama** bölümünde, o hello emin olun **tanılamayı etkinleştir** onay kutusu seçilidir.
   
    ![Merhaba tanılamayı etkinleştir seçeneğine erişme](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796660.png)
3. Merhaba üç nokta (...) düğmesini toospecify hello depolama hesabını depolanan hello tanılama veri toobe istediğiniz yeri seçin. Seçtiğiniz hello depolama hesabına tanılama verilerinin depolandığı hello konum olacaktır.
   
    ![Merhaba depolama hesabı toouse belirtin](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796661.png)
4. Merhaba, **depolama bağlantı dizesi oluştur** iletişim kutusunda, istediğiniz hello Azure Storage öykünücüsü, bir Azure aboneliği kullanarak tooconnect veya kimlik bilgileri'el ile girilen olup olmadığını belirtin.
   
    ![Depolama hesabı iletişim kutusu](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796662.png)
   
   * Merhaba Microsoft Azure Storage öykünücüsü seçeneği belirlerseniz, hello bağlantı dizesi tooUseDevelopmentStorage ayarlanır = true.
   * Merhaba, abonelik seçeneği seçerseniz, hello toouse ve hello hesap adı istediğiniz Azure aboneliği seçebilirsiniz. Merhaba hesaplarını yönetme, Azure aboneliklerinize toomanage düğmesi seçebilirsiniz.
   * Merhaba el ile girilen kimlik bilgileri seçeneği seçerseniz, istendiğinde tooenter hello adı ve hello toouse istediğiniz Azure hesabı anahtarı demektir.
5. Merhaba seçin **yapılandırma** düğmesini tooview hello **tanılama Yapılandırması** iletişim kutusu. Her sekme (dışında **genel** ve **günlük dizinleri**) toplamak bir tanılama veri kaynağını temsil eder. Merhaba varsayılan sekmesi, **genel**, tanılama veri toplama seçeneklerini hello sunar: **yalnızca hatalar**, **tüm bilgileri**, ve **özel planı** . Merhaba, varsayılan seçeneği **yalnızca hatalar**, uyarı veya izleme iletileri aktarmaz çünkü alır hello az miktarda depolama. Tüm bilgi seçeneği aktarımları bilgilerin çoğu hello ve olan hello, bu nedenle, depolama açısından en ucuz seçeneği hello.
   
    ![Azure tanılama ve yapılandırma etkinleştir](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758144.png)
6. Bu örnekte, hello seçin **özel plan** hello veri özelleştirebileceğiniz şekilde seçeneği toplanır.
7. Merhaba **MB Disk kotası** kutusu istediğiniz tooallocate ne kadar alan depolama hesabı için tanılama verilerini belirtir. İsterseniz hello varsayılan değerini değiştirebilirsiniz.
8. Tanılama verilerini her bir sekmede istediğiniz toocollect, select kendi **etkinleştirmek Aktarım, <log type>**  onay kutusu. Toocollect uygulama günlüklerini isterseniz, örneğin, hello seçin **etkinleştirmek uygulama günlüklerini aktarımını** hello onay kutusunu **uygulama günlüklerini** sekmesi. Ayrıca, her bir tanılama veri türü tarafından gerekli diğer bilgileri belirtin. Merhaba bölümüne bakın **tanılama veri kaynakları yapılandırma** bu konuda daha sonra her bir sekmede yapılandırma bilgileri.
9. İstediğiniz tüm hello Tanılama verileri koleksiyonu etkinleştirdikten sonra hello seçin **Tamam** düğmesi.
10. Azure bulut hizmeti projenizi Visual Studio'da her zamanki gibi çalıştırın. Uygulamanızı kullanırken, etkinleştirilmiş hello günlük bilgilerini toohello Azure depolama hesabı, belirttiğiniz kaydedilir.

## <a name="enable-diagnostics-in-azure-virtual-machines"></a>Azure sanal makinelerde tanılamayı etkinleştirin
Visual Studio'da Azure sanal makineleri için toocollect tanılama verilerini seçebilirsiniz.

### <a name="tooenable-diagnostics-in-azure-virtual-machines"></a>Azure sanal makinelerde tooenable tanılama
1. İçinde **Sunucu Gezgini**, hello Azure düğümü seçin ve zaten bağlıysanız tooyour Azure aboneliğine bağlayın.
2. Merhaba genişletin **sanal makineleri** düğümü. Yeni bir sanal makine oluşturun veya zaten var olan birini seçin.
3. Merhaba kısayol menüsünde ilginizi çeken hello sanal makine için **yapılandırma**. Bu hello sanal makine yapılandırması iletişim kutusunu gösterir.
   
    ![Bir Azure sanal makinesini yapılandırma](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796663.png)
4. Henüz yüklü değilse hello Microsoft İzleme Aracısı tanılama uzantısını ekleyin. Bu uzantı hello Azure sanal makinesi için tanılama veri toplamak olanak sağlar. Merhaba yüklü uzantıları listesinde hello seçin bir kullanılabilir uzantı açılan menüsünü seçin ve Microsoft İzleme Aracısı Tanılama'yı seçin.
   
    ![Bir Azure sanal makine uzantısı yükleniyor](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC766024.png)
   
   > [!NOTE]
   > Diğer tanılama uzantıları, sanal makineleriniz için kullanılabilir. Daha fazla bilgi için bkz: Azure VM uzantıları ve özellikleri.
   > 
   > 
5. Merhaba seçin **Ekle** düğmesini tooadd hello uzantısı ve görünüm kendi **tanılama Yapılandırması** iletişim kutusu.
6. Merhaba seçin **yapılandırma** düğmesini toospecify bir depolama hesabı ve ardından hello **Tamam** düğmesi.
   
    Her sekme (dışında **genel** ve **günlük dizinleri**) toplamak bir tanılama veri kaynağını temsil eder.
   
    ![Azure tanılama ve yapılandırma etkinleştir](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758144.png)
   
    Merhaba varsayılan sekmesi, **genel**, tanılama veri toplama seçeneklerini hello sunar: **yalnızca hatalar**, **tüm bilgileri**, ve **özel planı** . Merhaba, varsayılan seçeneği **yalnızca hatalar**, uyarı veya izleme iletileri aktarmaz çünkü alır hello az miktarda depolama. Merhaba **tüm bilgileri** seçeneği aktarımları bilgilerin çoğu hello ve, bu nedenle, hello en pahalı depolama açısından seçenektir.
7. Bu örnekte, hello seçin **özel plan** hello veri özelleştirebileceğiniz şekilde seçeneği toplanır.
8. Merhaba **MB Disk kotası** kutusu istediğiniz tooallocate ne kadar alan depolama hesabı için tanılama verilerini belirtir. İsterseniz hello varsayılan değerini değiştirebilirsiniz.
9. Tanılama verilerini her bir sekmede istediğiniz toocollect, select kendi **etkinleştirmek Aktarım, <log type>**  onay kutusu.
   
    Toocollect uygulama günlüklerini isterseniz, örneğin, hello seçin **etkinleştirmek uygulama günlüklerini aktarımını** hello onay kutusunu **uygulama günlüklerini** sekmesi. Ayrıca, her bir tanılama veri türü tarafından gerekli diğer bilgileri belirtin. Merhaba bölümüne bakın **tanılama veri kaynakları yapılandırma** bu konuda daha sonra her bir sekmede yapılandırma bilgileri.
10. İstediğiniz tüm hello Tanılama verileri koleksiyonu etkinleştirdikten sonra hello seçin **Tamam** düğmesi.
11. Güncelleştirilmiş Merhaba projeyi kaydedin.
    
     Merhaba içinde bir ileti görürsünüz **Microsoft Azure etkinlik günlüğü** sanal makine hello penceresi güncelleştirilmiştir.

## <a name="configure-diagnostics-data-sources"></a>Tanılama veri kaynaklarını yapılandırma
Tanılama veri toplama etkinleştirdikten sonra toocollect ve hangi bilgilerin toplandığı tam olarak hangi veri kaynaklarını seçebilirsiniz. Merhaba hello sekmeleri listesi aşağıdadır **tanılama Yapılandırması** iletişim kutusu ve her hangi bir yapılandırma seçeneği anlamına gelir.

### <a name="application-logs"></a>Uygulama günlükleri
**Uygulama günlüklerini** bir web uygulaması tarafından üretilen tanılama bilgilerini içerir. Merhaba toocapture uygulama günlüklerini istiyorsanız seçin **etkinleştirmek uygulama günlüklerini aktarımını** onay kutusu. Artırmak veya hello hello uygulama günlüklerini aktarıldığını zaman dakika sayısını azaltmak hello değiştirerek tooyour depolama hesabı **aktarım süresi (dak)** değeri. Ayrıca hello hello günlük düzeyi değeri ayarlayarak hello günlüğünde yakalanan bilgi miktarını değiştirebilirsiniz. Örneğin, seçebileceğiniz **ayrıntılı** tooget daha fazla bilgi veya seçin **kritik** toocapture yalnızca kritik hataları. Uygulama günlüklerini yayar belirli tanılama sağlayıcısı varsa, bunları hello sağlayıcının GUID toohello ekleyerek yakalayabilirsiniz **sağlayıcı GUID** kutusu.

  ![Uygulama günlükleri](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758145.png)

  Bkz: [Azure App Service'te web uygulamalarını için tanılama günlüğünü etkinleştirme](app-service-web/web-sites-enable-diagnostic-log.md) uygulama günlükleri hakkında daha fazla bilgi.

### <a name="windows-event-logs"></a>Windows olay günlükleri
Merhaba toocapture Windows olay günlüklerini istiyorsanız seçin **etkinleştirmek aktarımı, Windows olay günlüklerini** onay kutusu. Artırmak veya hello hello olay günlüklerini aktarıldığını zaman dakika sayısını azaltmak hello değiştirerek tooyour depolama hesabı **aktarım süresi (dak)** değeri. Merhaba tootrack istediğiniz olay türlerini Hello onay kutularını seçin.

  ![Olay Günlükleri](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796664.png)

Azure SDK 2.6 veya sonraki sürümünü kullanıyorsanız ve bir özel veri kaynağı toospecify istiyorsanız hello girin  **<Data source name>**  metin kutusuna ve ardından hello **Ekle** düğmesine bir sonraki tooit. Merhaba veri kaynağı toohello diagnostics.cfcfg dosyası eklenir.

Azure SDK 2.5 kullanıyorsanız ve bir özel veri kaynağı toospecify istiyorsanız toohello ekleyebilirsiniz `WindowsEventLog` hello diagnostics.wadcfgx bölümünü dosya, aşağıdaki örneğine hello olduğu gibi.

```
<WindowsEventLog scheduledTransferPeriod="PT1M">
   <DataSource name="Application!*" />
   <DataSource name="CustomDataSource!*" />
</WindowsEventLog>
```
### <a name="performance-counters"></a>Performans sayaçları
Performans sayacı bilgileri sistem engelleri bulun ve sistem ve uygulama performansının ayarını yardımcı olabilir. Bkz: [oluşturma ve bir Azure uygulamasında performans sayaçlarını kullan](https://msdn.microsoft.com/library/azure/hh411542.aspx) daha fazla bilgi için. Merhaba toocapture performans sayaçları istiyorsanız seçin **etkinleştirmek performans sayaçları aktarımını** onay kutusu. Artırmak veya hello hello olay günlüklerini aktarıldığını zaman dakika sayısını azaltmak hello değiştirerek tooyour depolama hesabı **aktarım süresi (dak)** değeri. Merhaba performans tootrack istediğiniz sayaçları hello onay kutularını seçin.

  ![Performans Sayaçları](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758147.png)

Listede, bir performans sayacı tootrack girin kullanarak hello önerilen sözdizimi ve ardından hello **Ekle** düğmesi. Merhaba hello sanal makinedeki işletim sistemini izleyebilirsiniz hangi performans sayaçlarını belirler. Sözdizimi hakkında daha fazla bilgi için bkz: [sayaç yolu belirterek](https://msdn.microsoft.com/library/windows/desktop/aa373193.aspx).

### <a name="infrastructure-logs"></a>Altyapı günlükleri
Hello Azure tanılama altyapısı, hello RemoteAccess modülü ve hello RemoteForwarder modülü hakkında bilgi içerir, toocapture altyapı günlükleri istiyorsanız hello seçin **etkinleştirmek altyapı günlükleriaktarımını**onay kutusu. Artırmak veya hello hello günlükleri aktarıldığını zaman dakika sayısını azaltmak hello aktarım süresi (dak) değerini değiştirerek tooyour depolama hesabı.

  ![Tanılama altyapı günlükleri](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758148.png)

  Bkz: [kullanarak Azure tanılama tarafından günlüğü verilerini toplamak](https://msdn.microsoft.com/library/azure/gg433048.aspx) daha fazla bilgi için.

### <a name="log-directories"></a>Günlük dizinleri
Internet Information Services (IIS) istekleri için günlük dizinlerinden toplanan verileri içeren toocapture günlük dizinleri istiyorsanız başarısız isteklerin veya seçtiğiniz klasör hello seçin **etkinleştirmek günlük dizinleriaktarımını**onay kutusu. Artırmak veya hello hello günlükleri aktarıldığını zaman dakika sayısını azaltmak hello değiştirerek tooyour depolama hesabı **aktarım süresi (dak)** değeri.

Merhaba kutularını gibi toocollect, istediğiniz hello günlüklerinin seçebilirsiniz **IIS günlüklerini** ve **isteği başarısız oldu** günlükleri. Varsayılan depolama kapsayıcısını adları sağlanır, ancak isterseniz hello adlarını değiştirebilirsiniz.

Ayrıca, herhangi bir klasörden günlükleri yakalayabilirsiniz. Yalnızca hello hello yolu belirtin **mutlak dizin günlüğünden** bölümünde ve ardından hello **Dizin Ekle** düğmesi. Merhaba günlükleri Yakalanacak olan toohello belirtilen kapsayıcı.

  ![Günlük dizinleri](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796665.png)

### <a name="etw-logs"></a>ETW günlükleri
Kullanırsanız [Windows için olay izleme](https://msdn.microsoft.com/library/windows/desktop/bb968803\(v=vs.85\).aspx) (ETW) ve toocapture ETW günlükleri, select hello istediğiniz **etkinleştirmek ETW günlükleri aktarımını** onay kutusu. Artırmak veya hello hello günlükleri aktarıldığını zaman dakika sayısını azaltmak hello değiştirerek tooyour depolama hesabı **aktarım süresi (dak)** değeri.

Merhaba olayları olay kaynakları ve belirttiğiniz olay bildirimleri yakalanır. bir olay kaynağı toospecify hello bir ad girin **olay kaynakları** bölümünde ve ardından hello **olay kaynağı Ekle** düğmesi. Benzer şekilde, bir olay bildirimi hello belirtebilirsiniz **olay bildirimlerini** bölümünde ve ardından hello **olay bildirim eklemek** düğmesi.

  ![ETW günlükleri](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC766025.png)

  Merhaba ETW framework hello [System.Diagnostics.aspx] (https://msdn.microsoft.com/library/system.diagnostics (v=vs.110) ad alanı. sınıflarıyla ASP.NET desteklenir devralır ve standart [System.Diagnostics.aspx] (https://msdn.microsoft.com/library/system.diagnostics (v=vs.110) sınıfları, etkinleştirir hello [System.Diagnostics.aspx] (kullanımını genişleten hello Microsoft.WindowsAzure.Diagnostics ad hello Azure ortamı günlük Framework'te olarak https://msdn.microsoft.com/library/System.Diagnostics (v=vs.110). Daha fazla bilgi için bkz: [alın, Denetim günlüğü ve izleme Microsoft Azure](https://msdn.microsoft.com/magazine/ff714589.aspx) ve [Azure Cloud Services ve sanal makineleri etkinleştirme tanılamada](cloud-services/cloud-services-dotnet-diagnostics.md).

### <a name="crash-dumps"></a>Kilitlenme bilgi dökümleri
Ne zaman bir rol örneği çöküyor hakkında toocapture bilgi istiyorsanız hello seçin **etkinleştirmek kilitlenme dökümleri aktarımını** onay kutusu. (ASP.NET çoğu özel durumları işler olduğundan, bu yalnızca çalışan rolleri için genellikle kullanışlıdır.) Artırabilir ya da depolama hello yüzdesini azaltmak alanı hello değiştirerek toohello kilitlenme bilgi dökümleri ayrılan **Directory kota (%)** değeri. Burada hello kilitlenme bilgi dökümleri depolanır ve toocapture istediğinizi seçebilirsiniz hello depolama kapsayıcısı değiştirebileceğiniz bir **tam** veya **Mini** dökümü.

şu anda izleniyor hello işlemleri listelenir. Toocapture istediğiniz hello işlemler Hello onay kutularını seçin. tooadd başka bir işlem toohello listesi, hello işlem adı girin ve ardından hello **ekleme işlemi** düğmesi.

  ![Kilitlenme bilgi dökümleri](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC766026.png)

  Bkz: [alın, Denetim günlüğü ve izleme Microsoft azure'da](https://msdn.microsoft.com/magazine/ff714589.aspx) ve [Microsoft Azure tanılama bölümü 4: özel günlük kaydı bileşenleri ve Azure tanılama 1.3 değişiklikleri](http://justazure.com/microsoft-azure-diagnostics-part-4-custom-logging-components-azure-diagnostics-1-3-changes/) daha fazla bilgi için.

## <a name="view-hello-diagnostics-data"></a>Merhaba tanılama verilerini görüntüle
Bir bulut hizmeti veya bir sanal makine için hello Tanılama verileri derledik sonra görüntüleyebilirsiniz.

### <a name="tooview-cloud-service-diagnostics-data"></a>tooview bulut hizmeti Tanılama verileri
1. Normal olarak, bulut hizmetinize dağıtın ve ardından çalıştırın.
2. Depolama hesabınızı Visual Studio'nun oluşturduğu bir rapor veya tablo hello tanılama verilerini görüntüleyebilir. tooview hello verileri bir raporu açın **Cloud Explorer** veya **Sunucu Gezgini**ilginizi çeken hello rolü için hello düğümünün hello kısayol menüsünü açın ve ardından **görünüm tanılama verisi** .
   
    ![Tanılama verilerini görüntüle](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC748912.png)
   
    Merhaba kullanılabilir veri gösteren bir rapor görüntülenir.
   
    ![Visual Studio'da Microsoft Azure tanılama raporu](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796666.png)
   
    Merhaba en son veriler görüntülenmiyor hello aktarımı dönem tooelapse toowait olabilir.
   
    Merhaba seçin **yenileme** tooimmediately güncelleştirme hello verileri Bağla veya hello bir aralık seçin **otomatik yenileme** açılır liste kutusu toohave hello verileri otomatik olarak güncelleştirilir. tooexport hello hata verileri hello seçin **verme tooCSV** düğmesini toocreate bir virgülle ayrılmış değer dosyası bir elektronik tabloda açabilirsiniz.
   
    İçinde **Cloud Explorer** veya **Sunucu Gezgini**, hello dağıtımla ilişkili hello depolama hesabı açın.
3. Merhaba tablo Görüntüleyicisi'nde Hello tanılama tabloları açın ve topladığınız hello verileri gözden geçirin. Özel günlükler ve IIS günlüklerini bir blob kapsayıcısını açabilirsiniz. Aşağıdaki tablonun hello inceleyerek, sizi ilgilendiren hello verileri içeren hello tablo veya blob kapsayıcısına bulabilirsiniz. Ayrıca, toohello verileri günlük dosyası, hello tablo girişleri EventTickCount, Deploymentıd, rol ve hangi sanal makine ve rol tanımlamak RoleInstance toohelp oluşturulan hello veri ve ne zaman. 
   
   | Tanılama veri | Açıklama | Konum |
   | --- | --- | --- |
   | Uygulama günlükleri |Merhaba System.Diagnostics.Trace sınıfı yöntemlerinin çağırarak kodunuzu oluşturur günlüğe kaydedilir. |WADLogsTable |
   | Olay Günlükleri |Merhaba Windows olay günlüklerini hello sanal makinelerde bu veriler arasındadır. Windows, bu günlükler bilgileri saklar, ancak uygulamalar ve hizmetler de tooreport hataları kullanın veya bilgileri günlüğe kaydeder. |WADWindowsEventLogsTable |
   | Performans Sayaçları |Merhaba sanal makinede kullanılabilir herhangi bir performans sayacı hakkında veri toplar. Merhaba işletim sistemi, bellek kullanımı ve işlemci süresi gibi birçok istatistikleri dahil performans sayaçları sağlar. |WADPerformanceCountersTable |
   | Altyapı günlükleri |Bu günlükler hello tanılama altyapısından kendisini üretilir. |WADDiagnosticInfrastructureLogsTable |
   | IIS günlükleri |Bu günlükler web isteklerini kaydedin. Bulut hizmetiniz bir miktarda trafiği alır, bu günlükleri toplamak ve yalnızca gerektiğinde bu verileri depolamak için oldukça uzun olabilir. |IIS wad failedreqlogs bu dağıtım, rol ve örneği için bir yol altında altında hello blob kapsayıcısında isteği başarısız oldu günlüklerini bulabilirsiniz. Tam günlükleri wad IIS logfiles altında bulabilirsiniz. Merhaba WADDirectories tabloda yapılan girişler her dosya için. |
   | Kilitlenme bilgi dökümleri |Bu bilgiler ikili bulut hizmetinizin işlemin (genellikle çalışan rolü) sağlar. |wad crush dökümleri blob kapsayıcısı |
   | Özel günlük dosyaları |Günlükleri, önceden tanımlanmış veri. |Depolama hesabınızı özel günlük dosyalarının hello konuma kodu belirtebilirsiniz. Örneğin, bir özel blob kapsayıcısını belirtebilirsiniz. |
4. Herhangi bir türde veriler kesildi, bu veri türü veya hello aralığını kısaltmayı veri aktarımları hello sanal makine tooyour depolama hesabından artan hello arabellek deneyebilirsiniz.
5. (isteğe bağlı) Temizleme verileri hello depolama biriminden tooreduce genel depolama maliyetleri bazen hesap.
6. Tam bir dağıtım yaptığınızda, hello diagnostics.cscfg dosyası (.wadcfgx için Azure SDK 2.5) Azure'da güncelleştirilir ve tüm değişiklikleri tooyour tanılama yapılandırması, bulut hizmetinizin seçer. Bunun yerine, var olan bir dağıtıma güncelleştirirseniz, Azure'da hello .cscfg dosyası güncelleştirilmez. Tanılama ayarları hello sonraki bölümdeki hello adımları izleyerek, ancak hala değiştirebilirsiniz. Tam dağıtımını gerçekleştirme ve var olan bir dağıtımını güncelleştirme hakkında daha fazla bilgi için bkz: [Azure uygulaması Yayımlama Sihirbazı](vs-azure-tools-publish-azure-application-wizard.md).

### <a name="tooview-virtual-machine-diagnostics-data"></a>tooview sanal makine tanılama verisi
1. Merhaba kısayol menüsünde hello sanal makine için **tanılama verilerini görüntüle**.
   
    ![Azure sanal makinesinde tanılama verilerini görüntüle](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC766027.png)
   
    Merhaba açılır **tanılama özeti** penceresi.
   
    ![Azure sanal makinesi tanılama özeti](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796667.png)  
   
    Merhaba en son veriler görüntülenmiyor hello aktarımı dönem tooelapse toowait olabilir.
   
    Merhaba seçin **yenileme** tooimmediately güncelleştirme hello verileri Bağla veya hello bir aralık seçin **otomatik yenileme** açılır liste kutusu toohave hello verileri otomatik olarak güncelleştirilir. tooexport hello hata verileri hello seçin **verme tooCSV** düğmesini toocreate bir virgülle ayrılmış değer dosyası bir elektronik tabloda açabilirsiniz.

## <a name="configure-cloud-service-diagnostics-after-deployment"></a>Dağıtımdan sonra bulut hizmeti tanılama Yapılandır
Bu zaten çalışan bir bulut hizmeti ile ilgili bir sorun çalışıyoruz, ilk olarak dağıtılan hello rolü önce belirtmediğiniz toocollect veri isteyebilirsiniz. Bu durumda, sunucu Gezgini'nde hello ayarlarını kullanarak bu verileri toocollect başlatabilirsiniz. Tek bir örnek veya tüm hello örnekleri için tanılama hello tanılama yapılandırması iletişim kutusu hello örneği veya hello rol için hello kısayol menüsünden açmak mı bağlı olarak bir rolü yapılandırabilirsiniz. Merhaba rol düğümü yapılandırırsanız, herhangi bir değişiklik tooall örnekleri uygulayın. Merhaba örneği düğümü yapılandırırsanız, herhangi bir değişiklik toothat örneği yalnızca uygulayın.

### <a name="tooconfigure-diagnostics-for-a-running-cloud-service"></a>çalışan bir bulut hizmeti için tooconfigure tanılama
1. Sunucu Gezgini'nde hello genişletin **bulut Hizmetleri** düğümünü genişletin ve ardından düğümler toolocate hello rol veya tooinvestigate veya her ikisini de istediğiniz örneği.
   
    ![Tanılama yapılandırılıyor](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC748913.png)
2. Merhaba kısayol menüsünde bir örnek düğümü ya da rolü düğümü için **güncelleştirme tanılama ayarları**ve ardından hello toocollect istediğiniz tanılama ayarlarını seçin.
   
    Merhaba yapılandırma ayarları hakkında daha fazla bilgi için bkz: **tanılama veri kaynakları yapılandırma** bu konuda. Nasıl tooview hello tanılama verilerini hakkında daha fazla bilgi için bkz: **hello Tanılama verileri görüntüleme** bu konuda.
   
    Veri toplama işlemini değiştirirseniz **Sunucu Gezgini**, bulut hizmetinizin tam olarak yeniden kadar bu değişiklikler etkili olur. Yayımlama hello varsayılan ayarları kullanırsanız hello değişiklikler üzerine değildir, yayımlama hello varsayılan ayar tam bir yeniden dağıtım yapmak yerine tooupdate hello var olan dağıtım olduğu. toomake emin hello ayarlarını temizle dağıtım sırasında Git toohello **Gelişmiş ayarları** hello Yayımlama Sihirbazı'nı ve Temizle hello sekmesinde **dağıtım güncelleştirme** onay kutusu. Bu onay kutusu işaretli ile yeniden dağıtırken hello ayarları toothose hello .wadcfgx (veya .wadcfg) dosyasındaki hello rol için hello özellikleri Düzenleyicisi aracılığıyla olarak döner. Dağıtımınızı güncelleştirirseniz, Azure hello eski ayarları tutar.

## <a name="troubleshoot-azure-cloud-service-issues"></a>Azure bulut hizmeti sorunlarını giderme
Yaşıyorsanız "meşgul" durumunda, takılmış bir rolü gibi bulut hizmeti projeleri sorunları sürekli geri dönüştürüldüğünde veya bir iç sunucu hatası oluşturur, araçları ve toodiagnose kullanın ve bu sorunları düzeltmek teknikleri vardır. Ortak sorunlar ve çözümleri belirli örnekleri yanı sıra, hello kavramları ve araçları genel bakış toodiagnose kullanılan ve bu tür hataları düzeltmek için bkz [Azure PaaS işlem tanılama verilerini](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).

## <a name="q--a"></a>Soru-Cevap
**Merhaba arabellek boyutu nedir ve ne kadar büyük olmalıdır?**

Her sanal makine örneği, tanılama ne kadar veri hello yerel dosya sisteminde depolanabilir kotaları sınırlayın. Ayrıca, her kullanılabilir tanılama veri türü için arabellek boyutu belirtin. Bu arabellek boyutu, veri türü için ayrı bir kota gibi davranır. Merhaba hello iletişim kutusunun alt kısmındaki denetleyerek belirleyebilirsiniz genel kota ve hello kalır bellek miktarını hello. Daha büyük arabellek ya da daha fazla veri türlerini belirtirseniz, yaklaşımını hello genel kota. Merhaba değiştirebileceğiniz hello diagnostics.wadcfg/.wadcfgx yapılandırma dosyasını değiştirerek genel kota. Veri depolanmış hello tanılama hello uygulamanızın veri olarak aynı dosya sistemi uygulamanız çok miktarda disk alanı kullanıyorsa, hello artırmak döndürmemelidir şekilde genel tanılama kotasından.

**Merhaba transfer süresi nedir ve ne kadar süreyle olmalıdır?**

Merhaba transfer dönemi hello veriler arasında geçtikten yakalayan zaman miktarıdır. Her aktarım süresinden sonra bir sanal makine tootables depolama hesabınızdaki üzerinde hello yerel dosya sisteminden veri taşınmaz. Toplanan veri miktarını Hello transfer dönemi hello bitişinden önce hello kota aşarsa, eski verileri göz ardı edilir. Verilerinizi hello arabellek boyutunu aştığından veri kaybı ya da genel kota hello toodecrease hello transfer dönemi isteyebilirsiniz.

**Hangi saat dilimi zaman damgaları, hello misiniz?**

Merhaba zaman damgaları, bulut hizmeti barındıran hello veri merkezinin yerel saat dilimi hello ' dir. Merhaba hello günlük tablolardaki aşağıdaki üç zaman damgası sütunları kullanılır.

* **PreciseTimeStamp** hello olayın hello ETW zaman damgası. Diğer bir deyişle, hello zaman hello olay hello istemciden günlüğe kaydedilir.
* **Zaman damgası** PreciseTimeStamp toohello karşıya yükleme frekansı sınır yuvarlanır. Bu nedenle, karşıya yükleme frekansı saat 00:17:12 5 dakika ile Merhaba olay ise, zaman damgası 00:15:00 olacaktır.
* **Zaman damgası** hello zaman damgası hangi hello varlık hello Azure tablo oluşturuldu.

**Maliyetleri nasıl tanılama bilgisi toplarken yönetiyorsunuz?**

Merhaba varsayılan ayarları (**günlük düzeyi** çok ayarlamak**hata** ve **Transfer dönemi** çok ayarlamak**1 dakika**) maliyet tasarlanmış toominimize olan. Daha fazla tanılama verisi toplama veya hello aktarım süresini azaltmak işlem maliyetleri artırır. Gereksinim ve artık ihtiyacınız olduğunda toodisable veri toplama unutmayın daha fazla veri toplama. Her zaman yeniden bile çalışma zamanında hello önceki bölümde gösterildiği gibi etkinleştirebilirsiniz.

**IIS nasıl isteği başarısız oldu günlükleri toplamak?**

Varsayılan olarak IIS istek başarısız günlükleri toplamak değil. Bunları, düzenlerseniz, web rolü için web.config dosyasının hello IIS toocollect yapılandırabilirsiniz.

**İzleme bilgilerini RoleEntryPoint yöntemlerden OnStart gibi alıyorum değil. Ne oldu?**

RoleEntryPoint Hello yöntemlerini hello WAIISHost.exe, IIS değil bağlamında denir. Bu nedenle, normalde izlemeyi etkinleştirir uygulanmaz web.config dosyasındaki yapılandırma bilgilerini hello. tooresolve Bu sorun bir .config dosyası tooyour web rolü projesi eklemek ve hello RoleEntryPoint kodu içeren hello dosya toomatch hello çıkış derleme adı. Merhaba varsayılan web rolü projesinde WAIISHost.exe.config hello .config dosyası hello adı olacaktır. Daha sonra aşağıdaki satırları toothis dosyasına hello ekleyin:

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

Merhaba, şimdi **özellikleri** penceresinde, kümesi hello **tooOutput dizin kopyalama** özelliği çok**her zaman Kopyala**.

## <a name="next-steps"></a>Sonraki adımlar
toolearn daha Azure'da oturum Tanılama hakkında bkz [Azure Cloud Services ve sanal makineleri etkinleştirme tanılamada](cloud-services/cloud-services-dotnet-diagnostics.md) ve [Azure App Service'te web uygulamalarını için tanılama günlüğünü etkinleştirme](app-service-web/web-sites-enable-diagnostic-log.md).

