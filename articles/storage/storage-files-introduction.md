---
title: Dosya depolama aaaIntroduction tooAzure | Microsoft Docs
description: "Azure File storage genel bakış, toocreate ve kullanım ağ dosyası sağlayan bir hizmet hello hello endüstri standardı kullanarak Microsoft bulut paylaşır."
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
ms.topic: get-started-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: a0a6a80a2ccd9742aa470bdd02ff375387a1629b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-file-storage"></a>Giriş tooAzure dosya depolama
Azure File storage sağlar ağ dosya paylaşımları hello endüstri standardı kullanarak hello bulutta [sunucu ileti bloğu (SMB) Protokolü](https://msdn.microsoft.com/library/windows/desktop/aa365233.aspx) ve [ortak Internet dosya sistemi (CIFS)](https://technet.microsoft.com/library/cc939973.aspx). Azure Dosya paylaşımları, Windows, macOS, Linux’ın şirket içi dağıtımları gibi istemciler veya Azure Sanal Makineleri tarafından eşzamanlı olarak bağlanabilir. TooAzure dosya depolama ve BLOB'ları, Azure sanal makine disklerini, tek bir hesap altında sıraları gibi başka hizmetleri erişim genel amaçlı depolama hesabı sağlar.



## <a name="videos"></a>Videolar
| Azure Dosya depolamaya giriş (27 dakika) | Azure Dosya depolama Öğreticisi (5 dakika)  |
|-|-|
| [![Merhaba Tanıtımı Azure File storage video - Screencap tooplay tıklayın!](media/storage-file-storage/azure-files-introduction-video-snapshot1.png)](https://www.youtube.com/watch?v=zlrpomv5RLs) | [![Hello Azure File storage Öğreticisi - Screencap tooplay tıklayın!](media/storage-file-storage/azure-files-introduction-video-snapshot2.png)](https://channel9.msdn.com/Blogs/Azure/Azure-File-storage-with-Windows/) |

## <a name="why-azure-file-storage-is-useful"></a>Azure Dosya depolama neden yararlıdır
Azure File storage tooreplace Windows Server, Linux, izin verir veya NAS tabanlı dosya sunucuları şirket içi barındırılan veya bir işletim sistemi serbest bulut dosyasıyla hello bulutta paylaşabilirsiniz. Hello aşağıdaki faydaları vardır:

* **Paylaşılan erişim:**. Azure dosya başka bir deyişle, standart SMB protokolü sorunsuz bir şekilde şirket içi dosya paylaşımları Azure dosya paylaşımları ile uygulama uyumluluğu hakkında endişelenmeden değiştirebilirsiniz destek hello endüstri paylaşır. Mümkün tooshare birden fazla makine arasında bir dosya sistemi olmasının, uygulamalar/örnekler önemli bir avantajı shareability gereken uygulamalar için Azure File storage ile geçerlidir. 
* **Tam Olarak Yönetilir**. Azure dosya paylaşımları hello gerek toomanage donanım veya bir işletim sistemi oluşturulabilir. Bu kritik güvenlik yükseltmeleri ile Merhaba sunucu işletim sistemi düzeltme eki uygulama veya hatalı sabit disklerin yerini toodeal yok anlamına gelir.
* **Betik ve Araç Sağlama**. PowerShell cmdlet'leri ve Azure CLI kullanılan toocreate olabilir bağlayın ve Azure uygulamalarının hello yönetiminin bir parçası File storage paylaşımlarını yönetin. Oluşturun ve Azure portalı ve Azure Depolama Gezgini kullanarak Azure dosya paylaşımlarını yönetin. 
* **Dayanıklılık**. Azure File storage toobe her zaman kullanılabilir plan hello gelen oluşturulmadı. Depolama, şirket içi dosya paylaşımları Azure dosyasıyla değiştirme işlemi artık yerel güç kesintileri veya ağ sorunları toodeal yukarı toowake gerektiği anlamına gelir. 
* **Tanıdık Programlanabilirlik**. Azure'da çalışan uygulamalar, veri dosyası aracılığıyla hello paylaşımda erişebilir [sistemi g/ç API'lerini](https://msdn.microsoft.com/library/system.io.file.aspx). Geliştiriciler, bu nedenle becerileri toomigrate uygulamalarınız ve var olan kodu yararlanabilirsiniz. Ayrıca tooSystem g/ç API'leri, kullanabileceğiniz [Azure Storage istemcisi kitaplıklarını](https://msdn.microsoft.com/library/azure/dn261237.aspx) veya hello [Azure Storage REST API'sini](/rest/api/storageservices/file-service-rest-api).

Azure Dosya paylaşımları şunları yapmak için kullanılabilir:

* **Şirket içi dosya sunucularını değiştirme**:  
    Azure File storage kullanılan toocompletely Değiştir dosya paylaşımlarında geleneksel şirket içi dosya sunucularında veya NAS cihazları olabilir. Hello world olsunlar Windows, macOS ve Linux gibi yaygın işletim sistemlerini kolayca bir Azure dosya paylaşımı bağlayabilir.

* **Uygulamaları "kaldırma ve kaydırma"**:  
    Azure File storage çok şirket içi dosya kullanma "kaldırın ve shift" uygulamaları toohello bulut hello uygulama bölümleri arasında tooshare veri paylaşır kolaylaştırır. Bu durum, toomake her VM toohello dosya paylaşımı bağlanır ve ardından onu okuyabilir ve bir şirket içi dosya karşı paylaştığınız gibi dosyaları yazma.

* **Bulut Geliştirmeyi Basitleştirme**:  
    Azure File storage farklı şekillerde toosimplify yeni bulut geliştirme projelerini sayısında kullanılabilir.
    * **Paylaşılan Uygulama Ayarları**:  
        Dağıtılmış uygulamalar için genel bir desen toohave yapılandırma dosyaları burada Bunlar pek çok farklı Vm'lerden erişilip merkezi bir konumda'dır. Bu tür yapılandırma dosyaları artık Azure Dosya paylaşımında depolanabilir ve tüm uygulama örnekleri tarafından okunabilir. Bu ayarları da toohello yapılandırma dosyalarını dünya çapında erişime hello REST arabirimi, yönetilebilir.

    * **Tanılama Paylaşımı**:  
        Bir Azure dosya paylaşımı kullanılan toosave günlükler, Ölçümler ve kilitlenme bilgi dökümleri gibi Tanılama dosyalarını da olabilir. Bu kullanılabilir hello SMB ve REST arabirimi aracılığıyla sahip uygulamalar toobuild izin verir veya çeşitli işleme ve hello tanılama verilerini çözümleme analiz araçları yararlanın.

    * **Geliştirme/Test/Hata Ayıklama**:  
        Geliştiriciler veya Yöneticiler hello bulutta sanal makineleri üzerinde çalışırken, genellikle birtakım Araçlar ve yardımcı programlar ihtiyaç duyar. Bu yardımcı programların gerekli oldukları her sanal makineye yüklenmesi ve dağıtılması, çok zaman alan bir çalışma olabilir. Azure File storage ile bir geliştirici veya yönetici, sık kullandığınız araçları kolayca bağlı toofrom olabilen bir dosya paylaşımında herhangi bir sanal makine depolayabilirsiniz.
        
## <a name="how-does-it-work"></a>Nasıl çalışır?
Azure Dosya paylaşımlarını yönetmek, şirket içi dosya paylaşımlarını yönetmekten çok daha basittir. Aşağıdaki diyagramda hello hello Azure dosya depolama yönetimi yapıları gösterilmektedir:

![Dosya Yapısı](../../includes/media/storage-file-concepts-include/files-concepts.png)

* **Depolama hesabı**: üzerinden depolama hesabı tüm erişim tooAzure depolama yapılır. Depolama hesabı kapasitesi hakkında ayrıntılı bilgi için, Azure Depolama Ölçeklenebilirlik ve Performans Hedefleri konusuna bakın.
* **Paylaşım**: Dosya Depolama paylaşımı Azure’daki bir SMB dosyası paylaşımıdır. Tüm dizinler ve dosyalar üst paylaşımda oluşturulmalıdır. Bir hesapta sınırsız sayıda paylaşım olabilir ve bir paylaşım dosyaları, toohello 5 TB toplam kapasiteye hello dosya paylaşımının sınırsız sayıda depolayabilirsiniz.
* **Dizin:** Dizinlerin isteğe bağlı hiyerarşisi.
* **Dosya**: hello paylaşımda bir dosya. Bir dosya boyutu too1 TB yukarı olabilir.
* **URL biçimi**: dosyaları hello şu URL biçimi kullanılarak adreslenebilir:  

    ```
    https://<storage account>.file.core.windows.net/<share>/<directory/directories>/<file>
    ```
## <a name="next-steps"></a>Sonraki Adımlar
* [Azure Dosya Paylaşımı Oluşturma](storage-file-how-to-create-file-share.md)
* [Windows’da Bağlama](storage-file-how-to-use-files-windows.md)
* [Linux’ta Bağlama](storage-how-to-use-files-linux.md)
* [macOS’ta Bağlama](storage-file-how-to-use-files-mac.md)
* [SSS](storage-files-faq.md)
* [Sorun giderme](storage-troubleshoot-file-connection-problems.md)

### <a name="conceptual-articles-and-videos"></a>Kavramsal makaleler ve videolar
* [Azure Dosya depolama: Windows ve Linux için uyumlu bulut SMB dosya sistemi](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)

### <a name="tooling-support-for-azure-file-storage"></a>Azure Dosya depolama için araç desteği
* [Azure Depolama ile Azure PowerShell’i kullanma](storage-powershell-guide-full.md)
* [Nasıl toouse Microsoft Azure Storage ile AzCopy](storage-use-azcopy.md)
* [Azure Storage ile Hello Azure CLI kullanma](storage-azure-cli.md#create-and-manage-file-shares)

### <a name="blog-posts"></a>Blog yazıları
* [Azure Dosya Depolama genel kullanıma sunulmuştur](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [Azure Dosya depolama incelemesi](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [Microsoft Azure Dosya Hizmeti’ne Giriş](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [Geçirme verilerini tooAzure dosyası](https://azure.microsoft.com/blog/migrating-data-to-microsoft-azure-files/)

### <a name="reference"></a>Başvuru
* [.NET için Depolama İstemci Kitaplığı başvurusu](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [Dosya Hizmeti REST API başvurusu](http://msdn.microsoft.com/library/azure/dn167006.aspx)
