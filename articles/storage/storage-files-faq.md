---
title: "Azure File storage hakkında sorular aaaFrequently | Microsoft Docs"
description: "Bul toofrequently Azure File storage hakkında sorular yanıtlanmaktadır."
services: storage
documentationcenter: 
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 07/19/2017
ms.author: renash
ms.openlocfilehash: ecd685b3094f51e998bbf5dd0567a20732757015
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-about-azure-file-storage"></a>Azure File storage hakkında sık sorulan sorular

## <a name="general"></a>Genel
* **Q. Azure File storage nedir?**  
   
    Azure File storage, Azure içinde dağıtılmış dosya sistemidir. Desteklenen Azure sanal makine veya şirket içi makinede yerel bir paylaşım olarak kullanıcılar toomount hello depolama sağlayan bir SMB protokolü arabirim sağlar.

* **Q. Azure File storage neden yararlıdır?**  
   
    Azure File storage, birden çok sanal makineleri ve platformlar arasında paylaşılan verilere erişim sağlar. Çok başvuran[neden Azure File storage yararlıdır](storage-files-introduction.md#why-azure-file-storage-is-useful).

* **Q. Azure dosya vs Azure Blob vs Azure diski ne zaman kullanmalıyım?**  
   
    Microsoft Azure çeşitli yollar hello bulutta toostore ve erişim verilerini sağlar.  
   
    Azure File storage - SMB arabirim, istemci kitaplıkları ve toostored dosyaları yerden kolay erişim veren bir REST arabirimini sağlar.  
   
    Azure BLOB'ların-istemci kitaplıkları ve depolanır ve blok blobları, büyük bir ölçekte erişilen yapılandırılmamış veri toobe veren bir REST arabirimini sağlar.  
   
    Azure veri diskleri - istemci kitaplıkları ve kalıcı olarak depolanır ve bir bağlı sanal sabit diskten erişilen veri toobe veren bir REST arabirimini sağlar.  
   
    Daha fazla bilgi almak [toouse Azure BLOB'olduğunda Deciding, Azure dosyaları ya da Azure veri diski](storage-decide-blobs-files-disks.md)

* **Q. Azure File storage kullanarak çalışmaya nasıl?**  
   
    Azure dosya paylaşımının oluşturarak başlatabilirsiniz. Azure portalı, hello Azure Storage PowerShell cmdlet'lerini, hello Azure Storage istemcisi kitaplıklarını veya hello Azure Storage REST API'sini kullanarak Azure dosya paylaşımları oluşturabilirsiniz. Bu öğreticide şunları öğreneceksiniz:

    * [Nasıl toocreate Azure dosya paylaşımı hello Portal kullanarak bilgi edinin](storage-file-how-to-create-file-share.md#create-file-share-through-the-portal)
    * [Nasıl toocreate Azure dosya paylaşımı Powershell kullanarak bilgi edinin](storage-file-how-to-create-file-share.md#create-file-share-through-powershell)
    * [Nasıl toocreate Azure dosya paylaşımı CLI kullanarak bilgi edinin](storage-file-how-to-create-file-share.md#create-file-share-through-command-line-interface-cli)

* **Q. Hangi çoğaltmalar Azure File storage tarafından destekleniyor mu?**  
   
    Azure File storage yalnızca LRS veya GRS şu anda destekler. Biz toosupport RA-GRS planlama ancak hiçbir zaman çizelgesi tooshare henüz var.

## <a name="security-authentication-and-access-control"></a>Güvenlik, kimlik doğrulama ve erişim denetimi

* **Q. Azure File storage tooaccess dosyalarında farklı şekilde nelerdir?**
    
    SMB 3.0 protokolünü kullanarak yerel makinenizde hello dosya paylaşımı bağlayabilir veya araçlarını kullanın ister [Depolama Gezgini](http://storageexplorer.com/) dosya paylaşımınızı tooaccess dosyaları. Uygulamanızdan depolama istemci kitaplığı, REST API'leri veya Powershell tooaccess dosyalarınızı Azure dosya paylaşımı kullanabilirsiniz.

* **Q. Bir web tarayıcısı kullanarak erişim tooa belirli dosya nasıl sağlayabilir miyim?**
    
    SAS kullanarak, belirtilen zaman aralığı için geçerli olan özel izinlere sahip belirteçler oluşturabilirsiniz. Örneğin, bir belirteç salt okunur erişim tooa belirli dosya ile belirli bir süre için oluşturabilirsiniz. Geçerli olduğu halde bu url sahip olan herkes hello dosya tüm web tarayıcılarından doğrudan erişebilirsiniz. SAS anahtarları, Depolama Gezgini gibi bir kullanıcı arabiriminden kolayca oluşturulabilir.

* **Q. Bu, olası toospecify salt okunur veya sadece yazılabilir izinleri hello paylaşımı klasörlere mi?**
    
    Merhaba dosya paylaşımını SMB aracılığıyla bağlamanız halinde bu üzerinde denetim düzeyi izinleri yok. Ancak, bu hello REST API aracılığıyla paylaşılan erişim imzası (SAS) veya istemci kitaplıkları oluşturarak elde edebilirsiniz.  

* **Q. Azure File storage için sunucu tarafı şifrelemesi nasıl etkinleştirebilirim?**

    [Sunucu tarafı şifrelemesi](storage-service-encryption.md) için Azure dosya depolama tüm bölgeler ve ortak ve Ulusal Bulutlar genel olarak kullanılabilir. Azure dosya depolama kullanmak için SSE etkinleştirebilirsiniz [Azure portal](https://portal.azure.com/),[Microsoft Azure depolama kaynak sağlayıcısı API](/rest/api/storagerp/storageaccounts), [Azure Powershell](https://msdn.microsoft.com/library/azure/mt607151.aspx) veya [Azure CLI](storage-azure-cli.md).
    
    Azure File storage'ı SSE etkinleştirdikten sonra bu depolama hesabında toohello dosya depolama yazılan yeni verileri otomatik olarak şifrelenir. Bu özellik tooexisting veya yeni paylaşımlar mevcut veya yeni bir depolama hesabında yazılan tüm yeni veriler kullanılabilir. Bu özelliği etkinleştirmek için ek bir ücret uygulanmamaktadır. Daha fazla bilgi almak [nasıl tooenable SSE Azure dosya depolama](storage-service-encryption.md).

* **Q. Active Directory tabanlı kimlik doğrulaması Azure File storage tarafından destekleniyor mu?**
   
    Şu anda AD tabanlı kimlik doğrulamasını veya ACL’leri desteklemiyoruz. Ancak, bunu özellik istekleri listemize ekledik. Şimdilik, hello Azure depolama hesabı anahtarlarını kullanılan tooprovide kimlik doğrulaması toohello Dosya Paylaşımı ' dir. Merhaba REST API veya hello istemci kitaplıkları aracılığıyla paylaşılan erişim imzaları (SAS) kullanarak geçici bir çözüm sunuyoruz. SAS kullanarak, belirtilen zaman aralığı için geçerli olan özel izinlere sahip belirteçler oluşturabilirsiniz. Örneğin, 10 dakika süre sonu dosyasıyla verilen salt okunur erişim tooa ile bir belirteç oluşturabilirsiniz. Herkes geçerli olduğu halde bu belirtece sahip, bu 10 dakika için salt okunur erişim toothat dosya vardır.
   
    SAS yalnızca hello REST API veya istemci kitaplıkları aracılığıyla desteklenir. Merhaba dosya paylaşımını hello SMB protokolü aracılığıyla bağladığınızda, SAS toodelegate erişim tooits içeriği kullanamazsınız. 
    
* **Q. Azure File storage için desteklenen hello veri uyumluluk ilkeleri nelerdir?**

   Azure File Storage çalıştıran üstünde diğer depolama hizmetleri Azure Storage'da ve hello geçerlidir gibi aynı depolama mimarisi hello aynı veri uyumluluk ilkeleri. Azure Storage veri uyumluluğu hakkında daha fazla bilgi indirmek ve çok başvuran[Microsoft Azure veri koruması belge](http://go.microsoft.com/fwlink/?LinkID=398382&clcid=0x409).

## <a name="on-premises-access"></a>Şirket içi erişim

* **Toouse Azure ExpressRoute tooconnect tooAzure dosya depolama biriminden bir şirket içi VM sahip Q.Do?**
   
    Hayır. ExpressRoute yoksa, bağlantı noktası 445 (TCP Giden) için Internet erişimi açık olduğu sürece hello dosya paylaşımı şirket içi erişmeye devam edebilirsiniz. Bununla birlikte, ExpressRoute Azure File storage ile isterseniz kullanabilirsiniz.

* **Q. Nasıl ı my yerel makinede bir Azure dosya paylaşımı bağlayabilir?** 
    
    Bağlantı noktası 445 (TCP Giden) olduğu ve istemcinizi hello SMB 3.0 protokolünü destekleyen sürece hello SMB protokolü aracılığıyla hello dosya paylaşımı bağlayabilir (örneğin, Windows 10 veya Windows Server 2012 kullanmakta olduğunuz). Lütfen yerel ISS sağlayıcısı toounblock hello bağlantı noktanızın ile çalışır. Hello geçici, kullanarak dosyalarınızı görüntüleyebilirsiniz [Depolama Gezgini](../vs-azure-tools-storage-explorer-files.md#view-a-file-shares-contents).


## <a name="billing-and-pricing"></a>Faturalama ve fiyatlandırma
* **Q. Bir Azure VM ve bir dosya paylaşımı sayısı arasındaki ağ trafiğini toohello abonelik doludur harici bant genişliği olarak hello mu?**
   
    Merhaba dosya paylaşımı ve VM olsalar aynı Azure bölgesinde hello hello aralarındaki trafik boş. Bunlar farklı bölgelerde bulunuyorsa, aralarındaki hello trafik harici bant genişliği olarak ücretlendirilir.

## <a name="backup"></a>Backup

* **Q. My Azure dosya paylaşımı nasıl yedekleme?**
    
    AzCopy, RoboCopy, veya bir bağlı dosya paylaşımı yedekleyebilirsiniz yedekleme aracı bir 3. taraf kullanabilirsiniz. Merhaba yakın zaman içinde dosya paylaşımları toohave hello özelliği tootake anlık görüntülerini bekliyoruz; mümkün toouse olacaktır bu özellik toobackup, Azure dosya paylaşımı.

## <a name="performance"></a>Performans

* **Q. Azure File storage hello ölçek sınırları nelerdir?**
    Azure File storage ölçeklenebilirlik ve performans hedefleri hakkında daha fazla bilgi için bkz: [Azure Storage ölçeklenebilirlik ve performans hedefleri](storage-scalability-targets.md#scalability-targets-for-blobs-queues-tables-and-files).

* **Q. Toounzip dosyaları Azure dosya depolama alanına çalışırken performansta yavaşlama oluyor? Ne yapmalıyım?**
    
    Azure File storage dosyalarıyla çok sayıda tootransfer, ağ aktarımı için bu araçları için iyileştirilmiş gibi AzCopy (Windows, Linux/Unix için Önizleme) veya Azure Powershell kullanmanızı öneririz.

* **Q. Düzeltme ekleri süredir ne toofix yavaş performans sorunu Azure File storage ile serbest?**
    
    Hello müşteri, Windows 8.1 veya Windows Server 2012 R2 üzerinden Azure File Storage'a eriştiğinde hello Windows ekibi yakın zamanda düzeltme eki toofix yavaş performans sorunu yayımladı. Daha fazla bilgi için lütfen hello kullanıma BB makalesi, ilişkili [Windows 8.1 veya Server 2012 R2 üzerinden Azure File storage eriştiğinizde yavaş performans](https://support.microsoft.com/kb/3114025).

## <a name="features-and-interoperability-with-other-services"></a>Özellikleri ve diğer hizmetleri ile birlikte çalışabilirlik
* **Q. "Dosya paylaşım tanığı" bir yük devretme kümesi hello biri için kullanım örnekleri Azure File storage için mi?**
   
    Bu şu anda desteklenmiyor.

* **Q. Yeniden adlandırma işlemi hello REST API de var mı?**
   
    Şu anda değil.

* **Q. Paylaşımlar, diğer bir deyişle, bir paylaşım kapsamında içe?**
    
    Hayır. Merhaba dosya paylaşımı bağlayabileceğiniz sanal sürücüsü hello kitabıdır iç içe paylaşımlar desteklenmez.

* **Q. Azure File storage'ı IBM MQ ile kullanma**
    
    IBM belge tooguide IBM MQ müşterileri Azure File storage kendi hizmetiyle yapılandırırken yayımladı. Daha fazla bilgi için lütfen kullanıma [toosetup IBM MQ çok örnek Sıra Yöneticisi Microsoft Azure dosya hizmeti ile nasıl](https://github.com/ibm-messaging/mq-azure/wiki/How-to-setup-IBM-MQ-Multi-instance-queue-manager-with-Microsoft-Azure-File-Service).


## <a name="troubleshooting"></a>Sorun giderme
* **Q. Azure dosya depolama hatalarında nasıl sorun giderme?**
    
    Çok başvurabilir[Azure File storage sorun giderme makalesi](storage-troubleshoot-file-connection-problems.md) uçtan uca sorun giderme kılavuzu için. 


## <a name="see-also"></a>Ayrıca bkz.
Azure File Storage hakkında daha fazla bilgi edinmek için şu bağlantılara göz atın.

### <a name="conceptual-articles-and-videos"></a>Kavramsal makaleler ve videolar
* [Azure Dosya depolama: Windows ve Linux için uyumlu bulut SMB dosya sistemi](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)
* [Nasıl toouse Linux Azure File storage](storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-file-storage"></a>File Storage için araç desteği
* [Azure Depolama ile Azure PowerShell’i kullanma](storage-powershell-guide-full.md)
* [Nasıl toouse Microsoft Azure Storage ile AzCopy](storage-use-azcopy.md)
* [Azure Storage ile Hello Azure CLI kullanma](storage-azure-cli.md)
* [Azure Dosya depolama sorunlarını giderme](storage-troubleshoot-file-connection-problems.md)

### <a name="blog-posts"></a>Blog yazıları
* [Azure Dosya Depolama genel kullanıma sunulmuştur](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [Azure Dosya depolama incelemesi](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [Microsoft Azure Dosya Hizmeti’ne Giriş](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [Geçirme verilerini tooAzure dosya depolama](https://azure.microsoft.com/blog/migrating-data-to-microsoft-azure-files/)

### <a name="reference"></a>Başvuru
* [.NET başvurusu için Depolama İstemci Kitaplığı](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [Dosya Hizmeti REST API başvurusu](http://msdn.microsoft.com/library/azure/dn167006.aspx)
