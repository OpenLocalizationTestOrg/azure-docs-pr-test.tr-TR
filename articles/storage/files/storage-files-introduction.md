---
title: "Azure Dosyaları'na giriş | Microsoft Docs"
description: "Endüstri standardı SMB protokolünü kullanarak bulutta ağ dosya paylaşımları oluşturmanıza ve bunları kullanmanıza olanak tanıyan Azure Dosyaları hizmetine genel bir bakış."
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
ms.date: 10/08/2017
ms.author: renash
ms.openlocfilehash: f96aa9fe12aba28e1ac3429f012419341bdf92c1
ms.sourcegitcommit: c4cc4d76932b059f8c2657081577412e8f405478
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/11/2018
---
# <a name="introduction-to-azure-files"></a>Azure Dosyaları'na giriş
Azure Dosyaları bulutta tamamen yönetilen dosya paylaşımları sunar. Bu dosyalara sektör standardı olan [Sunucu İleti Bloğu (SMB) protokolü](https://msdn.microsoft.com/library/windows/desktop/aa365233.aspx) (Ortak İnternet Dosya Sistemi veya CIFS olarak da bilinir) aracılığıyla erişilebilir. Azure Dosya paylaşımları Windows, Linux ve macOS bulut ve şirket içi dağıtımları tarafından aynı anda bağlanabilir. Azure Dosya paylaşımları ayrıca verilerin kullanıldığı yerin yakınlarında hızlı erişim sağlamak için Azure Dosya Eşitleme (önizleme) ile Windows sunucularında önbelleğe alınabilir.

## <a name="videos"></a>Videolar
| Azure Dosya Eşitleme Tanıtımı (2 dk.) | Eşitleme ile Azure Dosyaları (Ignite 2017) (85 dk.)  |
|-|-|
| [![Azure Dosya Eşitleme'ye giriş videosunun yayını - oynatmak için tıklayın!](./media/storage-files-introduction/azure-file-sync-video-snapshot.png)](https://www.youtube.com/watch?v=Zm2w8-TRn-o) | [![Eşitleme ile Azure Dosyaları sunumunun yayını - oynatmak için tıklayın!](./media/storage-files-introduction/azure-files-ignite-2017-video.png)](https://www.youtube.com/watch?v=r26jWDGF_rg) |

## <a name="why-azure-files-is-useful"></a>Azure Dosyaları neden faydalıdır?
Azure Dosya paylaşımları şunları yapmak için kullanılabilir:

* **Şirket içi dosya sunucularını değiştirme veya destekleme**:  
    Azure Dosyaları geleneksel şirket içi dosya sunucularını veya NAS cihazlarını tamamen değiştirmek veya desteklemek için kullanılabilir. Windows, macOS ve Linux gibi yaygın işletim sistemleri, dünyanın neresinde olursa olsun Azure Dosya paylaşımlarına doğrudan bağlanabilir. Azure Dosya paylaşımları ayrıca verilerin kullanıldığı yerde performanslı ve dağıtılmış bir şekilde önbelleğe alınması için Azure Dosya Eşitleme ile şirket içi veya bulut üzerindeki Windows sunucularında çoğaltılabilir.

* **Uygulamaları "kaldırma ve kaydırma"**:  
    Azure Dosyaları dosya uygulamasını veya kullanıcı verilerini saklamak için bir dosya paylaşımı gerektiren uygulamaların buluta taşınmasını kolaylaştırır. Azure Dosyaları, uygulamanın ve verilerinin Azure'a taşındığı "klasik" taşıma senaryosunun yanı sıra uygulama verilerinin Azure Dosyaları'na taşındığı ve uygulamanın şirket içi ortamda çalışmaya devam ettiği "hibrit" taşıma senaryosunu destekler. 

* **Bulut geliştirmeyi basitleştirme**:  
    Azure Dosyaları ayrıca yeni bulut geliştirme projelerini kolaylaştırma amacıyla farklı şekillerde kullanılabilir. Örnek:
    * **Paylaşılan uygulama ayarları**:  
        Dağıtılmış uygulamalar için yaygın bir düzen, yapılandırma dosyalarının birçok uygulama örneğinin erişebildiği merkezi bir konumda tutulmasıdır. Uygulama örnekleri yapılandırmalarını Dosya REST API'si üzerinden yükleyebilir ve kullanıcılar bu verilere SMB paylaşımını yerel ortama bağlayarak erişebilir.

    * **Tanılama paylaşımı**:  
        Azure Dosya paylaşımı, bulut uygulamalarının günlük, ölçüm ve kilitlenme bilgi dökümünü kaydetmeleri için kullanışlı bir yerdir. Günlükler uygulama örnekleri tarafından Dosya REST API'si aracılığıyla yazılabilir ve geliştiriciler dosya paylaşımını yerel makinelerine bağlayarak bu verilere erişebilir. Bu durum geliştiricilerin bildikleri ve sevdikleri araçları bırakmak zorunda kalmadan bulut geliştirmeye geçmelerini sağladığından önemli bir esneklik sunar.

    * **Geliştirme/Test/Hata Ayıklama**:  
        Geliştiriciler veya yöneticiler bulutta sanal makinelerle çalışırken, sıklıkla bir dizi araca veya yardımcı programa ihtiyaçları olur. Bu tür yardımcı programları ve araçları tüm sanal makineleri kopyalamak uzun zaman alabilir. Bir Azure Dosya paylaşımını sanal makinelere yerel olarak bağlayan geliştirici ve yöneticiler kopyalamaya gerek duymadan araçlarına ve yardımcı programlarına erişebilirler.

## <a name="key-benefits"></a>Önemli avantajlar
* **Paylaşılan erişim**. Azure Dosya paylaşımları endüstri standardı SMB protokolünü destekler. Bu, şirket içi dosya paylaşımlarınızı uygulama uyumluluğu konusunda kaygılanmadan rahatça Azure Dosya paylaşımlarıyla değiştirebileceğiniz anlamına gelir. Dosya sistemini birden çok makine, uygulama/örnek arasında paylaşabilmek, paylaşılabilirlik gerektiren uygulamalarda Azure Dosyaları'nın önemli bir avantaj olmasını sağlar. 
* **Tam olarak yönetilir**. Azure Dosya paylaşımları donanım veya işletim sistemi yönetmeye gerek kalmadan oluşturulabilir. Bu, sunucu işletim sistemine kritik güvenlik yükseltmeleri için yama eklemekle veya arızalı sabit diskleri değiştirmekle uğraşmanız gerekmediği anlamına gelir.
* **Betik ve araç sağlama**. Azure uygulamalarının yönetimi kapsamında Azure Dosya paylaşımlarını oluşturmak, bağlamak ve yönetmek için PowerShell cmdlet'leri ve Azure CLI kullanılabilir. Azure portalını ve Azure Depolama Gezgini'ni kullanarak Azure dosya paylaşımlarını oluşturabilir ve yönetebilirsiniz. 
* **Dayanıklılık**. Azure Dosyaları, baştan sonra her zaman kullanılabilir olacak şekilde hazırlanmıştır. Şirket içi dosya paylaşımlarını Azure Dosyaları ile değiştirmek, artık kalkıp bölgesel elektrik kesintileriyle veya ağ sorunlarıyla uğraşmak zorunda kalmayacağınız anlamına gelir. 
* **Tanıdık programlanabilirlik**. Azure’da çalışan uygulamalar paylaşımdaki verilere [dosya sistemi G/Ç API’leri](https://msdn.microsoft.com/library/system.io.file.aspx) yoluyla erişebilir. Böylece geliştiriciler mevcut uygulamalarını taşımak üzere kullandıkları kodlar ve yeteneklerden yararlanabilir. Sistem G/Ç API’lerine ek olarak, [Azure Depolama İstemcisi Kitaplıkları](https://msdn.microsoft.com/library/azure/dn261237.aspx) veya [Azure Depolama REST API’si](/rest/api/storageservices/file-service-rest-api) de kullanılabilir.

## <a name="next-steps"></a>Sonraki Adımlar
* [Azure Dosya Paylaşımı Oluşturma](storage-how-to-create-file-share.md)
* [Windows'da bağlama](storage-how-to-use-files-windows.md)
* [Linux'ta bağlama](storage-how-to-use-files-linux.md)
* [macOS'ta bağlama](storage-how-to-use-files-mac.md)
