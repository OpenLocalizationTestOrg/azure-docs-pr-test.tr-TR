---
title: aaaSQL Server Business Intelligence | Microsoft Docs
description: "Bu konuda hello Klasik dağıtım modeli kullanılarak oluşturulmuş kaynaklarını kullanır ve Azure sanal makineleri (VM'ler) üzerinde çalışan SQL Server için kullanılabilen hello iş zekası (BI) özellikleri açıklar."
services: virtual-machines-windows
documentationcenter: na
author: guyinacube
manager: erikre
editor: monicar
tags: azure-service-management
ms.assetid: c681e7a7-eeda-48aa-bc35-6277f4828244
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/30/2017
ms.author: asaxton
ms.openlocfilehash: e3288f0835d6c4a19baeeea5f6b65fec16cd751f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-server-business-intelligence-in-azure-virtual-machines"></a>Azure Sanal Makinelerde SQL Server İş Zekası
> [!IMPORTANT] 
> Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../azure-resource-manager/resource-manager-deployment-model.md). Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır. Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.

Merhaba Microsoft Azure sanal makine Galerisi SQL Server yüklemelerini içeren resimler içerir. Merhaba hello galeri görüntüleri desteklenen sürümleri SQL Server hello aynı yükleme dosyalarını tooon içi bilgisayarlar ve sanal makinelere yükleyebilirsiniz. Bu konuda hello SQL Server Business Intelligence (BI) özetlenmektedir hello görüntülerinde yüklü özellikleri ve bir sanal makine sağlandıktan sonra gerekli yapılandırma adımları. Bu konu ayrıca BI özellikleri ve en iyi uygulamalar için desteklenen dağıtım topolojileri açıklanır.

## <a name="license-considerations"></a>Lisans konuları
İki yolu toolicense Microsoft Azure Virtual Machines'de SQL Server vardır:

1. Yazılım Güvencesi parçası olan lisans mobility avantajları. Daha fazla bilgi için bkz: [azure'da Yazılım Güvencesi ile lisans taşınabilirliği](https://azure.microsoft.com/pricing/license-mobility/).
2. Saat hızı yüklü SQL Server ile Azure sanal makineleri başına ücret ödersiniz. Bkz: Merhaba "SQL Server" bölümünde [sanal makineler fiyatlandırma](https://azure.microsoft.com/pricing/details/virtual-machines/#Sql).

Lisans ve geçerli oranları hakkında daha fazla bilgi için bkz: [sanal makineleri Lisansı hakkında SSS](https://azure.microsoft.com/pricing/licensing-faq/%20/).

## <a name="sql-server-images-available-in-azure-virtual-machine-gallery"></a>SQL Server görüntülerinde kullanılabilir Azure sanal makineye Galerisi
Hello Microsoft Azure sanal makineye Galerisi, Microsoft SQL Server içeren birkaç görüntüyü içerir. Merhaba sanal makine görüntüleri üzerinde yüklü hello yazılım hello hello işletim sistemi sürümünü ve SQL Server'ın hello sürümünü göre değişir. hello Azure sanal makinesi galerisinde görüntüleri Hello listesi sık değiştirir.

<!--![SQL image in azure VM gallery](./media/virtual-machines-windows-classic-ps-sql-bi/IC741367.png)-->
![Azure VM galerisinde SQL görüntüsü](./media/virtual-machines-windows-classic-ps-sql-bi/vm-sql-images.png)

![PowerShell](./media/virtual-machines-windows-classic-ps-sql-bi/IC660119.gif) Merhaba aşağıdaki PowerShell betiğini "SQL Server" Merhaba görüntü adı içeren Azure görüntüleri hello listesini döndürür:

    # assumes you have already uploaded a management certificate tooyour Microsoft Azure Subscription. View hello thumbprint value from hello "Subscriptions" menu in Azure portal.

    $subscriptionID = ""    # REQUIRED: Provide your subscription ID.
    $subscriptionName = "" # REQUIRED: Provide your subscription name.
    $thumbPrint = "" # REQUIRED: Provide your certificate thumbprint.
    $certificate = Get-Item cert:\currentuser\my\$thumbPrint # REQUIRED: If your certificate is in a different store, provide it here.-Ser  store is hello one specified with hello -ss parameter on MakeCert

    Set-AzureSubscription -SubscriptionName $subscriptionName -Certificate $certificate -SubscriptionID $subscriptionID

    Write-Host -foregroundcolor green "List of available gallery images where imagename contains 2016"
    Write-Host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
    get-azurevmimage | where {$_.ImageName -Like "*SQL-Server-2016*"} | select imagename,category, location, label, description

    Write-Host -foregroundcolor green "List of available gallery images where imagename contains 2014"
    Write-Host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
    get-azurevmimage | where {$_.ImageName -Like "*SQL-Server-2014*"} | select imagename,category, location, label, description

Sürümleri ve SQL Server tarafından desteklenen özellikler hakkında daha fazla bilgi için hello aşağıdakilere bakın:

* [SQL Server sürümleri](https://www.microsoft.com/server-cloud/products/sql-server-editions/#fbid=Zae0-E6r5oh)
* [Merhaba SQL Server 2016 sürümleri tarafından desteklenen özellikler](https://msdn.microsoft.com/library/cc645993.aspx)

### <a name="bi-features-installed-on-hello-sql-server-virtual-machine-gallery-images"></a>SQL Server sanal makine galeri görüntüleri hello BI yüklü Özellikler
Merhaba aşağıdaki tabloda hello genel Microsoft Azure sanal makinesi galeri görüntüleri üzerinde SQL Server için yüklü hello iş zekası özellikleri özetlenmektedir:

* SQL Server 2016 SP1 Enterprise
* SQL Server 2016 SP1 Standard
* SQL Server 2014 SP2 Enterprise
* SQL Server 2014 SP2 Standard
* SQL Server 2012 SP3 Enterprise
* SQL Server 2012 SP3 Standard

| SQL Server BI özelliği | Merhaba galeri görüntüsü üzerinde yüklü | Notlar |
| --- | --- | --- |
| **Raporlama Hizmetleri yerel modu** |Evet |Yüklü ancak hello Rapor Yöneticisi URL'si dahil olmak üzere yapılandırma gerektirir. Merhaba bölümüne bakın [Raporlama Hizmetleri Yapılandırma](#configure-reporting-services). |
| **SharePoint modu Raporlama Hizmetleri** |Hayır |Merhaba Microsoft Azure sanal makinesi galeri görüntüsü SharePoint veya SharePoint içermeyen yükleme dosyaları. <sup>1</sup> |
| **Analysis Services çok boyutlu ve veri madenciliği (OLAP)** |Evet |Yüklenmiş ve yapılandırılmış olarak hello varsayılan Analysis Services örneği |
| **Analysis Services tablo** |Hayır |SQL Server 2012'de desteklenen, 2014 ve 2016 görüntüler, ancak değil varsayılan olarak yüklenir. Analysis Services'ın başka bir örneği yükleyin. Merhaba bölümüne bakın bu konudaki diğer SQL Server hizmetlerini ve özellikleri yükleme. |
| **Analysis Services Power Pivot SharePoint için** |Hayır |Merhaba Microsoft Azure sanal makinesi galeri görüntüsü SharePoint veya SharePoint içermeyen yükleme dosyaları. <sup>1</sup> |

<sup>1</sup> SharePoint ve Azure sanal makineler hakkında ek bilgi için bkz: [SharePoint 2013 için Microsoft Azure mimariler](https://technet.microsoft.com/library/dn635309.aspx) ve [SharePoint dağıtım Microsoft Azure Virtual Machines'de](https://www.microsoft.com/download/details.aspx?id=34598).

![PowerShell](./media/virtual-machines-windows-classic-ps-sql-bi/IC660119.gif) PowerShell komut tooget aşağıdaki hello hello hizmet adını "SQL" içeren yüklü hizmetlerin listesini çalıştırın.

    get-service | Where-Object{ $_.DisplayName -like '*SQL*' } | Select DisplayName, status, servicetype, dependentservices | format-Table -AutoSize

## <a name="general-recommendations-and-best-practices"></a>Genel öneriler ve en iyi yöntemler
* Merhaba en az bir sanal makine için önerilen boyut **A3** SQL Server Enterprise Edition kullanırken. Merhaba **A4** sanal makine boyutu, Analysis Services ve Reporting Services SQL Server BI dağıtımları için önerilir.
  
    Merhaba geçerli VM boyutları hakkında daha fazla bilgi için bkz: [Azure için sanal makine boyutlarını](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Disk yönetimi en iyi yöntem toostore veri, günlük ve sürücülerindeki yedekleme dosyaları dışında olan **C**: ve **D**:. Örneğin, veri diskleri oluşturma **E**: ve **F**:.
  
  * ilke hello varsayılan sürücüsü için önbelleğe alma hello sürücü **C**: verilerle çalışmak için uygun değil.
  * Merhaba **D**: öncelikle başlangıç sayfa dosyası için kullanılan geçici bir sürücü sürücüdür. Merhaba **D**: sürücü kalıcı ve blob depolama alanına kaydedilmez. Yönetim görevleri gibi hello toohello sanal makine boyutunu değiştir sıfırla **D**: sürücü. Çok önerilen**değil** hello kullan **D**: tempdb dahil olmak üzere, veritabanı dosyalarının sürücü.
    
    Oluşturma ve diskleri ekleme hakkında daha fazla bilgi için bkz: [nasıl tooAttach bir sanal makine veri diski tooa](../classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
* Durdurun veya toouse planlamadığınız services'ı kaldırın. Örnek hello sanal makine yalnızca Raporlama Hizmetleri için kullanılıyorsa, durdurmak veya Analysis Services ve SQL Server Integration Services kaldırmak için. Merhaba aşağıdaki resimde, varsayılan olarak başlatılan hello hizmetler örneğidir.
  
    ![SQL Server Hizmetleri](./media/virtual-machines-windows-classic-ps-sql-bi/IC650107.gif)
  
  > [!NOTE]
  > Merhaba SQL Server veritabanı motorunun desteklenen hello BI senaryolarda gereklidir. Bir tek sunucu VM topolojisinde hello veritabanı altyapısı gereklidir üzerinde çalışan toobe hello aynı VM.
  
    Merhaba aşağıdaki daha fazla bilgi için bkz: [Raporlama hizmetlerini kaldırmak](https://msdn.microsoft.com/library/hh479745.aspx) ve [bir örneği, Analysis Services kaldırma](https://msdn.microsoft.com/library/ms143687.aspx).
* Denetleme **Windows Update** için yeni 'önemli güncelleştirmeleri'. Merhaba Microsoft Azure sanal makine görüntülerini sık yenilenmesini; Bununla birlikte önemli güncelleştirmeler kullanılabilir hale gelebilir **Windows Update** hello VM görüntüsü en son yenilendikten sonra.

## <a name="example-deployment-topologies"></a>Örnek dağıtım topolojileri
Merhaba, Microsoft Azure sanal makineler kullanan örnek dağıtımlar verilmiştir. Bu diyagramda Hello topolojileri SQL Server BI özellikleri ve Microsoft Azure sanal makineler ile kullanabileceğiniz hello olası topolojileri yalnızca bazıları yer alır.

### <a name="single-virtual-machine"></a>Tek bir sanal makine
Analysis Services, Reporting Services, SQL Server veritabanı altyapısı ve veri kaynaklarını tek bir sanal makinede.

![1 sanal makine ile bi iass senaryosu](./media/virtual-machines-windows-classic-ps-sql-bi/IC650108.gif)

### <a name="two-virtual-machines"></a>İki sanal makineler
* Analysis Services, Reporting Services ve tek bir sanal makinede SQL Server veritabanı altyapısı hello. Bu dağıtım hello rapor sunucusu veritabanı içerir.
* İkinci bir VM'de veri kaynakları. Merhaba ikinci VM SQL Server veritabanı altyapısı bir veri kaynağı olarak içerir.

![2 sanal makine ile bi iass senaryosu](./media/virtual-machines-windows-classic-ps-sql-bi/IC650109.gif)

### <a name="mixed-azure--data-on-azure-sql-database"></a>Karma Azure – veri Azure SQL veritabanı
* Analysis Services, Reporting Services ve tek bir sanal makinede SQL Server veritabanı altyapısı hello. Bu dağıtım hello rapor sunucusu veritabanı içerir.
* Azure SQL veritabanına veri kaynağıdır.

![Bi iaas senaryoları vm ve veri kaynağı olarak AzureSQL](./media/virtual-machines-windows-classic-ps-sql-bi/IC650110.gif)

### <a name="hybrid-data-on-premises"></a>Karma – veri şirket içi
* Bu örnek dağıtımda Analysis Services, Reporting Services ve SQL Server veritabanı altyapısı hello tek bir sanal makinede çalıştırın. Merhaba sanal makine konakları report server veritabanlarını hello. Azure sanal ağ üzerinden şirket içi etki alanına ya da çözüm tünel başka bir VPN birleştirilmiş tooan Hello sanal makinedir.
* Şirket içi veri kaynağıdır.

![Bi ıaas senaryoları vm ve şirket içi veri kaynakları](./media/virtual-machines-windows-classic-ps-sql-bi/IC654384.gif)

## <a name="reporting-services-native-mode-configuration"></a>Raporlama Hizmetleri yerel modu yapılandırma
Merhaba rapor sunucusu yapılandırılmamış ancak hello sanal makineye Galerisi görüntü SQL Server yüklü, Reporting Services yerel mod içerir. Bu bölümdeki Hello adımları hello Raporlama Hizmetleri rapor sunucusu yapılandırın. Raporlama Hizmetleri yerel modu yapılandırma hakkında daha ayrıntılı bilgi için bkz: [yükleme Raporlama Hizmetleri yerel modu rapor sunucusu (SSRS)](https://msdn.microsoft.com/library/ms143711.aspx).

> [!NOTE]
> Windows PowerShell komut dosyaları tooconfigure hello rapor sunucusu kullanan benzer içeriğine bakın [kullanım PowerShell tooCreate bir Azure VM ile bir yerel moddaki bir rapor sunucusunda](../classic/ps-sql-report.md).

### <a name="connect-toohello-virtual-machine-and-start-hello-reporting-services-configuration-manager"></a>Toohello sanal makineye bağlanın ve hello Raporlama Hizmetleri Yapılandırma Yöneticisi'ni başlatın
Tooan Azure sanal makinesine bağlanmak için iki ortak iş akışı vardır:

* Merhaba, tooconnect hello sanal makine hello adına tıklayın ve ardından **Bağlan**. Uzak Masaüstü Bağlantısı açar ve hello bilgisayar adı otomatik olarak doldurulur.
  
    ![tooazure sanal makineye bağlanma](./media/virtual-machines-windows-classic-ps-sql-bi/IC650112.gif)
* Windows Uzak Masaüstü Bağlantısı ile toohello sanal makineye bağlanın. Merhaba kullanıcı arabiriminde hello Uzak Masaüstü'nün:
  
  1. Türü hello **bulut hizmeti adı** hello bilgisayar adı olarak.
  2. İki nokta üst üste (:) yazın ve hello TCP Uzak Masaüstü uç noktası için yapılandırılmış ortak bağlantı noktası numarası hello.
     
      MyService.cloudapp.NET:63133
     
      Daha fazla bilgi için bkz: [bir bulut hizmeti nedir?](https://azure.microsoft.com/manage/services/cloud-services/what-is-a-cloud-service/).


**Reporting Services Configuration Manager'ı Başlat**

İçinde **Windows Server 2012/2016**:

1. Merhaba gelen **Başlat** ekranında, yazın **Reporting Services** toosee uygulamaların bir listesini.
2. Sağ **Reporting Services Configuration Manager** tıklatıp **yönetici olarak çalıştır**.

İçinde **Windows Server 2008 R2**:

1. Tıklatın **Başlat**ve ardından **tüm programlar**.
2. Tıklatın **Microsoft SQL Server 2016**.
3. Tıklatın **yapılandırma araçları**.
4. Sağ **Reporting Services Configuration Manager** tıklatıp **yönetici olarak çalıştır**.

Ya da:

1. Tıklatın **Başlat**.
2. Merhaba, **programları ve dosyaları ara** iletişim türü **Raporlama Hizmetleri**. Merhaba VM Windows Server 2012 çalıştırıyorsa, yazın **Raporlama Hizmetleri** Merhaba ekranında Windows Server 2012 Başlat.
3. Sağ **Reporting Services Configuration Manager** tıklatıp **yönetici olarak çalıştır**.
   
    ![SSRS Yapılandırma Yöneticisi için arama](./media/virtual-machines-windows-classic-ps-sql-bi/IC650113.gif)

### <a name="configure-reporting-services"></a>Raporlama hizmetlerini yapılandırma
**Hizmet hesabı ve web hizmeti URL'si:**

1. Merhaba doğrulayın **sunucu adı** hello yerel sunucu adı ve tıklatın **Bağlan**.
2. Not hello boş **rapor sunucusu veritabanı adı**. Merhaba Yapılandırma tamamlandığında hello veritabanı oluşturulur.
3. Merhaba doğrulayın **rapor sunucusu durumu** olan **başlatıldı**. Tooverify hello hizmetinin Windows Sunucu Yöneticisi'ndeki istiyorsanız, hello hello hizmetidir **SQL Server Reporting Services** Windows hizmeti.
4. Tıklatın **hizmet hesabı** ve hello hesap gerektiği gibi değiştirin. Merhaba sanal makine bir etki alanı olmayan birleştirilmiş ortamında kullanılırsa, yerleşik hello **ReportServer** hesabıdır yeterli. Merhaba hizmet hesabı hakkında daha fazla bilgi için bkz: [hizmet hesabı](https://msdn.microsoft.com/library/ms189964.aspx).
5. Tıklatın **Web hizmeti URL'si** hello sol bölmede.
6. Tıklatın **Uygula** tooconfigure hello varsayılan değerleri.
7. Not hello **rapor sunucusu Web hizmeti URL'leri**. Merhaba varsayılan TCP bağlantı noktası 80'dir ve hello URL'SİNİN bir parçası olduğunu unutmayın. Bir sonraki adımda Microsoft Azure sanal makine uç noktası başlangıç bağlantı noktası için oluşturun.
8. Merhaba, **sonuçları** bölmesinde hello Eylemler başarıyla tamamlandı doğrulayın.

**Veritabanı:**

1. Tıklatın **veritabanı** hello sol bölmede.
2. Tıklatın **değiştirmek veritabanı**.
3. Doğrulama **yeni bir rapor sunucusu veritabanı oluşturun** seçilir ve İleri'yi tıklatın.
4. Doğrulama **sunucu adı** tıklatıp **Bağlantıyı Sına**.
5. Merhaba sonuç ise **başarılı Bağlantıyı Sına**, tıklatın **Tamam** ve ardından **sonraki**.
6. Not hello veritabanı adı **ReportServer** ve hello **rapor sunucusu modu** olan **yerel** ardından **sonraki**.
7. Tıklatın **sonraki** hello üzerinde **kimlik bilgileri** sayfası.
8. Tıklatın **sonraki** hello üzerinde **Özet** sayfası.
9. Tıklatın **sonraki** hello üzerinde **ilerleme ve son** sayfası.

**2012 ve 2014 için web portalı URL'si veya Rapor Yöneticisi URL'si:**

1. Tıklatın **Web portalı URL'si**, veya **Rapor Yöneticisi URL'si** 2014 ve hello sol bölmede 2012.
2. **Uygula**'ya tıklayın.
3. Merhaba, **sonuçları** bölmesinde hello Eylemler başarıyla tamamlandı doğrulayın.
4. Tıklatın **çıkış**.

Rapor sunucusu izinleri hakkında daha fazla bilgi için bkz: [Yerel moddaki bir rapor sunucusunda izinleri verme](https://msdn.microsoft.com/library/ms156014.aspx).

### <a name="browse-toohello-local-report-manager"></a>Toohello Gözat yerel Rapor Yöneticisi
tooverify hello yapılandırma, hello VM üzerindeki Gözat tooreport Yöneticisi.

1. Hello VM, yönetici ayrıcalıklarına sahip Internet Explorer'ı başlatın.
2. Merhaba VM üzerinde toohttp://localhost/Reports göz atın.

### <a name="tooconnect-tooremote-web-portal-or-report-manager-for-2014-and-2012"></a>tooConnect tooRemote web portalı veya Rapor Yöneticisi 2014 ve 2012 için
2014 ve uzak bir bilgisayardan hello sanal makinedeki 2012 tooconnect toohello web portalı veya Rapor Yöneticisi isterseniz yeni bir sanal makine TCP uç noktası oluşturun. Merhaba rapor sunucusu varsayılan olarak, HTTP isteklerini dinler **bağlantı noktası 80**. Merhaba rapor sunucusu URL'leri toouse farklı bir bağlantı noktasını yapılandırırsanız, yönergeleri izleyerek hello bağlantı noktası numarasını belirtmeniz gerekir.

1. Merhaba TCP bağlantı noktası 80 sanal makine için bir uç nokta oluşturun. Daha fazla bilgi için bkz: Merhaba [sanal makine uç noktaları ve güvenlik duvarı bağlantı noktalarını](#virtual-machine-endpoints-and-firewall-ports) bu belgede bölüm.
2. Bağlantı noktası 80'hello sanal makinenin Güvenlik Duvarı'nı açın.
3. Toohello web portalı veya Rapor Yöneticisi, Azure sanal makine kullanmanın Gözat **DNS adı** hello URL'deki hello sunucu adı olarak. Örneğin:
   
    **Rapor sunucusu**: http://uebi.cloudapp.net/reportserver **Web portalı**: http://uebi.cloudapp.net/reports
   
    [Güvenlik duvarını rapor sunucusu erişimi için yapılandırma](https://msdn.microsoft.com/library/bb934283.aspx)

### <a name="toocreate-and-publish-reports-toohello-azure-virtual-machine"></a>tooCreate ve raporları yayımlama toohello Azure sanal makine
Merhaba aşağıdaki tabloda hello seçenekleri kullanılabilir toopublish varolan raporları hello Microsoft Azure sanal makinesi üzerinde barındırılan bir şirket içi bilgisayar toohello rapor sunucusu özetlenmektedir:

* **Rapor Oluşturucu**: hello sanal makine içeren hello tıklatın-SQL 2014 ve 2012 için Microsoft SQL Server Rapor Oluşturucusu sürümünü bir kez. toostart Rapor Oluşturucu hello hello sanal makinede SQL 2016 ile ilk kez:
  
  1. Tarayıcınız yönetici ayrıcalıklarıyla başlatın.
  2. Merhaba sanal makine de toohello web portalında göz atın ve seçim hello **karşıdan** sağ üst hello simgesi.
  3. Seçin **Rapor Oluşturucu**.
     
     Daha fazla bilgi için bkz: [rapor oluşturucusu başlatma](https://msdn.microsoft.com/library/ms159221.aspx).
* **SQL Server veri Araçları**: VM: SQL Server veri araçları hello sanal makinede yüklü ve kullanılan toocreate olabilir **rapor sunucusu projeleri** ve hello sanal makineye raporlar. SQL Server veri araçları hello raporları toohello rapor sunucusu hello sanal makineye yayımlayabilirsiniz.
* **SQL Server veri araçları: Uzaktan**: yerel bilgisayarınızda SQL Server veri araçları Raporlama Hizmetleri raporlarını içeren bir Reporting Services projesi oluşturun. Merhaba proje tooconnect toohello web hizmeti URL'si yapılandırın.
  
    ![SSRS projesi için SSDT proje özellikleri](./media/virtual-machines-windows-classic-ps-sql-bi/IC650114.gif)
* Oluşturma bir. Raporları içeren ve karşıya yükleyin ve hello sürücüsü Ekle VHD sabit sürücü.
  
  1. Oluşturma bir. VHD raporlarınızı içeren yerel bilgisayarınızdaki sabit sürücü.
  2. Oluşturun ve bir yönetim sertifikası yükleyin.
  3. Merhaba VHD dosyası tooAzure Hello Ekle-AzureVHD cmdlet'ini kullanarak karşıya [oluşturma ve karşıya yükleme Windows Server VHD tooAzure](../classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
  4. Merhaba disk toohello sanal makine ekleyin.

## <a name="install-other-sql-server-services-and-features"></a>Diğer SQL Server hizmetlerini ve özellikleri yükleme
tooinstall ek SQL Server gibi hizmetleri Analysis Services tabular modunda hello SQL server Kurulum sihirbazını çalıştırın. Merhaba sanal makinenin yerel diskte Hello Kurulum dosyalarıdır.

1. Tıklatın **Başlat** ve ardından **tüm programlar**.
2. Tıklatın **Microsoft SQL Server 2016**, **Microsoft SQL Server 2014** veya **Microsoft SQL Server 2012** ve ardından **yapılandırma araçları** .
3. Tıklatın **SQL Server Yükleme Merkezi'ni**.

Veya C:\SQLServer_13.0_full\setup.exe, C:\SQLServer_12.0_full\setup.exe veya C:\SQLServer_11.0_full\setup.exe çalıştırın

> [!NOTE]
> Merhaba ilk kez SQL Server Kurulumu, dosyaları indirilebilir ve hello sanal makinenin yeniden başlatılması ve SQL Server Kurulumu'nu yeniden başlatılmasını gerektiren daha fazla Kurulumu çalıştırın.
> 
> Toorepeatedly gerekirse Microsoft Azure sanal makinesi hello seçili hello görüntüsünü özelleştirme, kendi SQL Server görüntü oluşturmayı düşünün. Çözümleme Hizmetleri SysPrep işlevselliği ile SQL Server 2012 SP1 CU2 etkinleştirildi. Daha fazla bilgi için bkz: [SQL Server kullanarak Sysprep yükleme konuları](https://msdn.microsoft.com/library/ee210754.aspx) ve [sunucu rolleri için Sysprep desteği](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).
> 
> 

### <a name="tooinstall-analysis-services-tabular-mode"></a>tooInstall Analysis Services Tabular modda
Merhaba, bu bölümdeki adımları **özetlemek** hello Analysis Services tabular modunda yükleme. Daha fazla bilgi için hello aşağıdakilere bakın:

* [Analysis Services Tabular modunda yükleme](https://msdn.microsoft.com/library/hh231722.aspx)
* [Tablo modelleme (Adventure Works öğretici)](https://msdn.microsoft.com/library/140d0b43-9455-4907-9827-16564a904268)

**Analysis Services Tabular modunda tooInstall:**

1. Merhaba SQL Server Yükleme Sihirbazı'nda tıklatın **yükleme** hello sol bölmesinde ve ardından **yeni SQL server tek başına yükleme veya özellikler tooan mevcut yükleme eklemek**.
   
   * Merhaba görürseniz **klasöre Gözat**, tooc:\SQLServer_13.0_full, c:\SQLServer_12.0_full veya c:\SQLServer_11.0_full göz atın ve ardından **Tamam**.
2. Tıklatın **sonraki** üzerinde hello ürün güncelleştirmeleri sayfası.
3. Merhaba üzerinde **yükleme türü** sayfasında, **SQL Server'ın yeni bir yükleme gerçekleştirmek** tıklatıp **sonraki**.
4. Merhaba üzerinde **Kurulum rolü** sayfasında, **SQL Server özellikleri yükleme**.
5. Merhaba üzerinde **özellik seçimi** sayfasında, **Analysis Services**.
6. Merhaba üzerinde **örnek Yapılandırması** sayfasında, gibi açıklayıcı bir ad yazın **tablolu** içine **adlı örneği** ve **örnek kimliği** metin kutuları.
7. Merhaba üzerinde **Çözümleme Hizmetleri Yapılandırması** sayfasında, **Tabular modda**. Merhaba geçerli kullanıcı toohello yönetim izinleri listeye ekleyin.
8. Tamamlayın ve hello SQL Server Yükleme Sihirbazı'nı kapatın.

## <a name="analysis-services-configuration"></a>Çözümleme Hizmetleri Yapılandırması
### <a name="remote-access-tooanalysis-services-server"></a>Uzaktan erişim tooAnalysis Hizmetleri sunucusu
Analysis Services sunucusu, yalnızca windows kimlik doğrulamasını destekler. SQL Server Management Studio veya SQL Server veri araçları gibi istemci uygulamalardan uzaktan tooaccess Analysis Services, Azure sanal ağı kullanarak toobe birleştirilmiş tooyour yerel etki alanı, hello sanal makinenin gerekiyor. Daha fazla bilgi için [Azure Virtual Network](../../../virtual-network/virtual-networks-overview.md).

A **varsayılan örnek** Analysis Services TCP bağlantı noktasını dinler **2383**. Başlangıç bağlantı noktası hello sanal makineleri Güvenlik Duvarı'nı açın. Kümelenmiş Analysis Services örneği dinlediği bağlantı noktası adı da **2383**.

İçin bir **adlandırılmış örneği** Analysis Services SQL Server Browser hizmetini hello gereklidir toomanage bağlantı noktasına erişim. Merhaba SQL Server Browser varsayılan yapılandırmadır, bağlantı noktası **2382**.

Bağlantı noktası Hello sanal makineleri Güvenlik Duvarı'nda açmak **2382** ve statik bir Analysis Services örneğinin bağlantı noktası adlandırılmış oluşturun.

1. zaten bulunan tooverify bağlantı noktaları hello VM ve hello bağlantı noktalarını hangi işlemin kullandığını kullanın, yönetici ayrıcalıklarıyla komutu aşağıdaki hello çalıştırın:
   
        netstat /ao
2. Kullanım SQL Server Management Studio toocreate statik bir Analysis Services adlı örnek bağlantı noktası 'Bağlantı noktası' güncelleştirerek tablo AS değerinde örnek genel özellikleri. Daha fazla bilgi için "Sabit bir bağlantı noktası için bir varsayılan kullanın veya adlandırılmış örneğine" Merhaba [hello Windows Güvenlik Duvarı tooAllow Analysis Services erişimi yapılandırmak](https://msdn.microsoft.com/library/ms174937.aspx#bkmk_fixed).
3. Merhaba tablo hello Analysis Services hizmeti örneğini yeniden başlatın.

Daha fazla bilgi için bkz: Merhaba **sanal makine uç noktaları ve güvenlik duvarı bağlantı noktalarını** bu belgede bölüm.

## <a name="virtual-machine-endpoints-and-firewall-ports"></a>Sanal makine uç noktaları ve güvenlik duvarı bağlantı noktaları
Bu bölümde, Microsoft Azure sanal makine uç toocreate ve bağlantı noktaları tooopen hello sanal makine güvenlik duvarları içinde özetlenmektedir. Merhaba aşağıdaki tabloda özetlenmiştir hello **TCP** toocreate uç noktaları için ve hello bağlantı noktaları tooopen hello sanal makineleri Güvenlik Duvarı'nda bağlantı noktaları.

* Tek bir VM'ye kullanıyorsanız ve hello aşağıdaki iki öğeyi true, toocreate VM uç noktaları gerekmez ve hello güvenlik duvarı hello VM üzerinde tooopen hello bağlantı noktaları gerekmez.
  
  * Uzaktan hello VM toohello SQL Server özellikleri bağlamayın. Uzak Masaüstü Bağlantısı toohello VM oluşturma ve yerel olarak hello VM hello SQL Server özelliklerine erişme uzak bağlantı toohello SQL Server özelliklerini dikkate alınmaz.
  * Azure sanal ağ veya başka bir VPN tünel çözüm aracılığıyla hello VM tooan şirket içi etki alanına katılın değil.
* Merhaba sanal makine etki alanına katılmış tooa değildir ancak istiyorsanız tooremotely VM toohello SQL Server özellikleri Bağlan:
  
  * Merhaba VM üzerinde hello Güvenlik Duvarı'nda Hello bağlantı noktalarını açın.
  * Hello için sanal makine uç noktaları oluşturma not ettiğiniz bağlantı noktaları (*).
* Merhaba sanal makine Azure sanal ağ gibi bir VPN tüneli kullanarak birleştirilen tooa etki alanı varsa, hello uç noktaları gerekli değildir. Ancak hello VM üzerinde hello Güvenlik Duvarı'nda hello bağlantı noktalarını açın.
  
  | Bağlantı noktası | Tür | Açıklama |
  | --- | --- | --- |
  | **80** |TCP |Rapor sunucusu uzaktan erişim (*). |
  | **1433** |TCP |SQL Server Management Studio'yu (*). |
  | **1434** |UDP |SQL Server Browser. Bu VM birleştirilmiş tooa etki alanında olduğunda hello gereklidir. |
  | **2382** |TCP |SQL Server Browser. |
  | **2383** |TCP |SQL Server Analysis Services varsayılan örneği ve kümelenmiş adlandırılmış örnekleri. |
  | **Kullanıcı tanımlı** |TCP |Seçtiğiniz bir bağlantı noktası numarası için örnek bağlantı noktası adlı statik bir Analysis Services oluşturun ve hello Güvenlik Duvarı'nda bağlantı noktası başlangıç Engellemeyi Kaldır. |

Uç noktaları oluşturma hakkında daha fazla bilgi için hello aşağıdakilere bakın:

* Uç noktalar oluşturursunuz:[nasıl tooSet yukarı uç noktaları tooa sanal makine](../classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
* SQL Server: Hello "Tam yapılandırma adımları tooconnect toohello sanal makine kullanarak SQL Server Management Studio'yu" bölümüne bakın [Azure üzerinde bir SQL Server sanal makine sağlama](../sql/virtual-machines-windows-portal-sql-server-provision.md).

Merhaba Aşağıdaki diyagramda hello bağlantı noktaları tooopen hello VM Güvenlik Duvarı tooallow uzaktan erişim toofeatures içinde ve hello VM bileşenleri gösterilmektedir.

![Azure vm'lerinde bi uygulamaları için bağlantı noktalarını tooopen](./media/virtual-machines-windows-classic-ps-sql-bi/IC654385.gif)

## <a name="resources"></a>Kaynaklar
* Hello Azure sanal makine ortamında kullanılan Microsoft sunucu yazılımı için Hello destek ilkesini inceleyin. BitLocker, Yük Devretme Kümelemesi ve Ağ Yükü Dengeleme gibi özellikleri için destek bölümüne aşağıdaki hello özetler. [Microsoft sunucu yazılımı desteği için Azure sanal makineleri](http://support.microsoft.com/kb/2721672).
* [SQL Server üzerinde Azure sanal makinelere genel bakış](../sql/virtual-machines-windows-sql-server-iaas-overview.md)
* [Sanal Makineler](https://azure.microsoft.com/documentation/services/virtual-machines/)
* [Azure üzerinde bir SQL Server sanal makine sağlama](../sql/virtual-machines-windows-portal-sql-server-provision.md)
* [Nasıl bir sanal makine veri diski tooa tooAttach](../classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [Veritabanı tooSQL bir Azure VM sunucuda geçirme](../sql/virtual-machines-windows-migrate-sql.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json)
* [Merhaba sunucu modunda bir Analysis Services örneğinin belirleme](https://msdn.microsoft.com/library/gg471594.aspx)
* [Çok boyutlu modelleme (Adventure Works öğretici)](https://technet.microsoft.com/library/ms170208.aspx)
* [Azure Belge Merkezi'nde](https://azure.microsoft.com/documentation/)
* [Power BI karma bir ortamda kullanma](https://msdn.microsoft.com/library/dn798994.aspx)

> [!NOTE]
> [Geri bildirim ve Microsoft SQL Server bağlantı üzerinden iletişim bilgileri Gönder](https://connect.microsoft.com/SQLServer/Feedback)

### <a name="community-content"></a>Topluluk içeriği
* [PowerShell ile Azure SQL veritabanı yönetimi](http://blogs.msdn.com/b/windowsazure/archive/2013/02/07/windows-azure-sql-database-management-with-powershell.aspx)

