---
title: Dosya depolama aaaIntroduction tooAzure | Microsoft Docs
description: "Giriş tooAzure ağ dosyası sağlar dosya depolama hello Microsoft Cloud paylaşır"
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
ms.openlocfilehash: fe6826e79c364a6956831d2e273c4342a5fd47f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-file-storage"></a>Giriş tooAzure dosya depolama

Azure File storage sağlar ağ dosya paylaşımları hello endüstri standardı kullanarak hello bulutta [sunucu ileti bloğu (SMB) Protokolü](https://msdn.microsoft.com/library/windows/desktop/aa365233.aspx) ve [ortak Internet dosya sistemi (CIFS)](https://technet.microsoft.com/library/cc939973.aspx). Azure Dosya paylaşımları, Windows, macOS, Linux’ın şirket içi dağıtımlarında ve Azure Sanal Makineleri tarafından eşzamanlı olarak bağlanabilir. Bir genel amaçlı depolama hesabı tooAzure File storage, Azure Blob Depolama ve Azure kuyruk depolama erişim sağlar.

## <a name="videos"></a>Videolar
| Azure Dosya depolamaya giriş (27 dakika) | Azure Dosya depolama Öğreticisi (5 dakika)  |
|-|-|
| [![Merhaba Tanıtımı Azure File storage video - ekran kaydı tooplay tıklayın!](./media/storage-files-introduction/azure-files-introduction-video-snapshot1.png)](https://www.youtube.com/watch?v=zlrpomv5RLs) | [![Ekran kaydı hello Azure File Storage Öğreticisi - tooplay tıklayın!](./media/storage-files-introduction/azure-files-introduction-video-snapshot2.png)](https://channel9.msdn.com/Blogs/Azure/Azure-File-storage-with-Windows/) |

## <a name="why-azure-file-storage-is-useful"></a>Azure Dosya depolama neden yararlıdır

Azure File storage tooreplace Windows Server, Linux, izin verir veya NAS tabanlı dosya sunucuları şirket içi barındırılan veya bir işletim sistemi serbest bulut dosyasıyla hello bulutta paylaşabilirsiniz. Azure File storage hello aşağıdaki faydaları vardır:

* **Paylaşılan erişim** Azure dosya paylaşımları desteği hello endüstri standart SMB protokolü, başka bir deyişle, sorunsuz bir şekilde yerine, şirket içi dosya paylaşımları Azure dosya paylaşımları ile uygulama uyumluluğu hakkında endişelenmeden. Mümkün tooaccess olan önemli bir avantajı Azure File storage ile birden çok makinelerden ve uygulamalar/örnekleri bir dosya paylaşımı olması.

* **Tam olarak yönetilen** Azure dosya paylaşımları, hello gerek toomanage donanım ya da hello sunucu işletim sistemi kritik güvenlik yükseltme düzeltme eki uygulama veya hatalı sabit disklerin yerini toodeal sahip olmayan anlamına gelir. bir işletim sistemi olmadan oluşturulabilir.

* **Komut dosyası çalıştırma ve Tooling** PowerShell cmdlet'leri ve Azure CLI kullanılan toocreate olabilir bağlayın ve Azure uygulamalarının hello yönetiminin bir parçası Azure dosya paylaşımlarını yönetmek. Oluşturma ve hello kullanarak Azure dosya paylaşımlarını yönetmek [Azure portal](https://portal.azure.com) ve hello [Azure Storage Gezgini](https://storageexplorer.com). 

* **Dayanıklılık** Azure File storage, her zaman kullanılabilir toobe plan hello gelen derlendiğinden. Depolama, şirket içi dosya paylaşımları Azure dosyasıyla değiştirme işlemi artık yerel güç kesintileri veya ağ sorunları toodeal yukarı toowake gerektiği anlamına gelir. 

* **Tanıdık programlama** Azure'da çalışan uygulamalar, veri hello paylaşımında erişebilir [dosya sistemi g/ç API'leri](https://msdn.microsoft.com/library/system.io.file.aspx). Geliştiriciler, bu nedenle becerileri toomigrate uygulamalarınız ve var olan kodu yararlanabilirsiniz. Ayrıca tooSystem g/ç API'leri, herhangi bir hello gibi hello Azure storage istemci kitaplıkları için kullanabileceğiniz [.NET](/dotnet/api/overview/azure/storage?view=azure-dotnet), veya hello [Azure Storage REST API'sini](/rest/api/storageservices/file-service-rest-api).

Azure Dosya paylaşımları şunları yapmak için kullanılabilir:

* **Değiştir şirket içi dosya sunucuları** Azure File storage kullanılan toocompletely Değiştir dosya paylaşımlarında geleneksel şirket içi dosya sunucularında veya NAS cihazları olabilir. Hello world olsunlar Windows, macOS ve Linux gibi yaygın işletim sistemlerini kolayca bir Azure dosya paylaşımı bağlayabilir.

* **Uygulamaları "kaldırma ve kaydırma"**

    Azure File storage çok şirket içi dosya kullanma "kaldırın ve shift" uygulamaları toohello bulut hello uygulama bölümleri arasında tooshare veri paylaşır kolaylaştırır. tooimplement Bu, her bir VM toohello dosya paylaşımı bağlanır ve ardından onu okuyabilir ve bir şirket içi dosya karşı paylaştığınız gibi dosyaları yazma.

* **Bulut Geliştirmeyi Basitleştirme**
    
    Azure File storage farklı şekillerde toosimplify yeni bulut geliştirme projelerini sayısında kullanılabilir.
    
    * **Paylaşılan Uygulama Ayarları**
    
        Dağıtılmış uygulamalar için genel bir desen toohave yapılandırma dosyaları burada Bunlar pek çok farklı Vm'lerden erişilip merkezi bir konumda'dır. Bu tür yapılandırma dosyaları artık Azure Dosya paylaşımında depolanabilir ve tüm uygulama örnekleri tarafından okunabilir. Bu ayarları da toohello yapılandırma dosyalarını dünya çapında erişime hello REST arabirimi, yönetilebilir.

    * **Tanılama Paylaşımı**
    
        Bir Azure dosya paylaşımı kullanılan toosave günlükler, Ölçümler ve kilitlenme bilgi dökümleri gibi Tanılama dosyalarını da olabilir. Dosya paylaşımları hello SMB ve REST arabirimi kullanılabilir olan uygulamalar toobuild izin verir veya çeşitli işleme ve hello tanılama verilerini çözümleme analiz araçları yararlanın.

    * **Geliştirme/Test/Hata Ayıklama**

        Geliştiriciler veya Yöneticiler hello bulutta sanal makineleri üzerinde çalışırken, genellikle birtakım Araçlar ve yardımcı programlar ihtiyaç duyar. Bu yardımcı programların gerekli oldukları her sanal makineye yüklenmesi ve dağıtılması, çok zaman alan bir çalışma olabilir. Azure File storage ile bir geliştirici veya yönetici, sık kullandığınız araçları kolayca bağlı toofrom olabilen bir dosya paylaşımında herhangi bir sanal makine depolayabilirsiniz.
        
## <a name="how-does-it-work"></a>Nasıl çalışır?

Azure Dosya paylaşımlarını yönetmek, şirket içi dosya paylaşımlarını yönetmekten çok daha basittir. Aşağıdaki diyagramda hello hello Azure dosya depolama yönetimi yapıları gösterilmektedir:

![Dosya Yapısı](./media/storage-files-introduction/files-concepts.png)

* **Depolama hesabı** üzerinden depolama hesabı tüm erişim tooAzure depolama yapılır. Depolama hesabı kapasitesi hakkında ayrıntılı bilgi için, [Ölçeklenebilirlik ve Performans Hedefleri](../common/storage-scalability-targets.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json) konusuna bakın.

* **Paylaşım** Dosya Depolama paylaşımı Azure’daki bir SMB dosyası paylaşımıdır. Tüm dizinler ve dosyalar üst paylaşımda oluşturulmalıdır. Bir hesapta sınırsız sayıda paylaşım olabilir ve bir paylaşım dosyaları, toohello 5 TB toplam kapasiteye hello dosya paylaşımının sınırsız sayıda depolayabilirsiniz.

* **Dizin** Dizinlerin isteğe bağlı hiyerarşisi.

* **Dosya** hello paylaşımda bir dosya. Bir dosya boyutu too1 TB yukarı olabilir.

* **URL biçimi** dosyaları hello şu URL biçimi kullanılarak adreslenebilir:  

    ```
    https://<storage account>.file.core.windows.net/<share>/<directory/directories>/<file>
    ```

## <a name="next-steps"></a>Sonraki adımlar

* [Azure Dosya Paylaşımı Oluşturma](storage-how-to-create-file-share.md)
* [Windows’da Bağlama](storage-how-to-use-files-windows.md)
* [Linux’ta Bağlama](storage-how-to-use-files-linux.md)
* [macOS’ta Bağlama](storage-how-to-use-files-mac.md)
* [SSS](../storage-files-faq.md)
* [Windows’da sorun giderme](storage-troubleshoot-windows-file-connection-problems.md)   
* [Linux’ta sorun giderme](storage-troubleshoot-linux-file-connection-problems.md)   

<!-- Rena I would remove any articles from here that are more than a year old. - Robin-->
### <a name="conceptual-articles-and-videos"></a>Kavramsal makaleler ve videolar
* [Azure Dosya depolama: Windows ve Linux için uyumlu bulut SMB dosya sistemi](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)

### <a name="tooling-support-for-azure-file-storage"></a>Azure Dosya depolama için araç desteği
* [Nasıl toouse Microsoft Azure Storage ile AzCopy](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)
* [Azure Storage ile Hello Azure CLI kullanma](../common/storage-azure-cli.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#create-and-manage-file-shares)

### <a name="blog-posts"></a>Blog yazıları
* [Azure Dosya Depolama genel kullanıma sunulmuştur](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [Azure Dosya depolama incelemesi](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [Microsoft Azure Dosya Hizmeti’ne Giriş](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [Geçirme verilerini tooAzure dosyası](https://azure.microsoft.com/blog/migrating-data-to-microsoft-azure-files/)

### <a name="reference"></a>Başvuru
* [.NET başvurusu için Depolama İstemci Kitaplığı](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [Dosya Hizmeti REST API başvurusu](http://msdn.microsoft.com/library/azure/dn167006.aspx)
