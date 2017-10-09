---
title: "Azure Storage kesinti hello olayı içinde aaaWhat toodo | Microsoft Docs"
description: "Azure Storage kesinti hello olayı içinde hangi toodo"
services: storage
documentationcenter: .net
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 8f040b0f-8926-4831-ac07-79f646f31926
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 1/19/2017
ms.author: robinsh
ms.openlocfilehash: 93e1e831c35b96b8bf190fa2b56ab89350bbac13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="what-toodo-if-an-azure-storage-outage-occurs"></a>Bir Azure Storage kesinti oluşursa hangi toodo
Microsoft, sabit toomake hizmetlerimizle her zaman kullanılabilir olduğundan emin çalışır. Bazen bizim denetim etkisi bize bir veya daha fazla bölgelerde planlanmayan hizmet kesintileri neden yolla zorlar. Bu nadir örnekleri ele toohelp, Azure Storage Hizmetleri için üst düzey yönergeleri izleyerek hello sunuyoruz.

## <a name="how-tooprepare"></a>Nasıl tooprepare
Her müşteri tooprepare için kritik kendi olağanüstü durum kurtarma planı. Merhaba çaba toorecover depolama kesinti gelen genellikle çalışır duruma uygulamalarınızda işlem personeli ve sipariş tooreactivate otomatik yordamları içerir. Lütfen kendi olağanüstü durum kurtarma planı toohello toobuild aşağıda Azure belgelerine bakın:

* [Azure uygulamaları için olağanüstü durum kurtarma ve yüksek kullanılabilirlik](/azure/architecture/resiliency/disaster-recovery-high-availability-azure-applications.md)
* [Azure dayanıklılık teknik kılavuzu](/azure/architecture/resiliency.md)
* [Azure Site Recovery hizmeti](https://azure.microsoft.com/services/site-recovery/)
* [Azure Depolama çoğaltması](storage-redundancy.md)
* [Azure yedekleme hizmeti](https://azure.microsoft.com/services/backup/)

## <a name="how-toodetect"></a>Nasıl toodetect
Merhaba önerilir yolu toodetermine hello Azure hizmet durumu toosubscribe toohello [Azure hizmet sağlığı panosunu](https://azure.microsoft.com/status/).

## <a name="what-toodo-if-a-storage-outage-occurs"></a>Bir depolama kesinti oluşursa hangi toodo
Bir veya daha fazla depolama hizmetleri bir veya daha fazla bölgelerinde aynı geçici olarak devre dışı olması durumunda, tooconsider için iki seçenek vardır. Lütfen anında erişim tooyour veri üzerinde isterse seçeneği 2 göz önünde bulundurun.

### <a name="option-1-wait-for-recovery"></a>Seçenek 1: Kurtarma için bekleyin
Bu durumda, herhangi bir eyleminiz gereklidir. Toorestore hello Azure hizmeti kullanılabilirlik titizlikle çalışıyoruz. Merhaba hello hizmet durumunu izleyebilirsiniz [Azure hizmet sağlığı panosunu](https://azure.microsoft.com/status/).

### <a name="option-2-copy-data-from-secondary"></a>Seçenek 2: ikincil veri kopyalama
Seçerseniz [okuma erişimli coğrafi olarak yedekli depolama (RA-GRS)](storage-redundancy.md#read-access-geo-redundant-storage) (depolama hesapları için önerilir) okuma erişimi tooyour verilerin hello ikincil bölgesinden gerekir. Araçları gibi kullanabilir [AzCopy](storage-use-azcopy.md), [Azure PowerShell](storage-powershell-guide-full.md)ve hello [Azure veri hareketi Kitaplığı](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/) hello ikincil bölge'nda başka bir depolama hesabında toocopy verileri bir unimpacted bölge ve ardından noktası uygulamaları toothat depolama hesabı için okuma ve yazma kullanılabilirlik.

## <a name="what-tooexpect-if-a-storage-failover-occurs"></a>Bir depolama yük devretme gerçekleşirse hangi tooexpect
Seçerseniz [coğrafi olarak yedekli depolama (GRS)](storage-redundancy.md#geo-redundant-storage) veya [okuma erişimli coğrafi olarak yedekli depolama (RA-GRS)](storage-redundancy.md#read-access-geo-redundant-storage) (önerilen), Azure Storage verilerinizin iki bölgelerde (birincil ve ikincil) dayanıklı tutar. Her iki bölgelerde, Azure Storage verilerinizin birden çok çoğaltma sürekli tutar.

Bölgesel bir olağanüstü durumda birincil bölge etkilediğinde, önce bu bölgede toorestore hello hizmeti deneyeceğiz. Merhaba niteliği hello olağanüstü durum ve bazı nadir durumlarda, kendi etkileri bağımlı biz mümkün toorestore hello birincil bölge olmayabilir. Bu noktada, biz bir coğrafi yük devretme işlemini gerçekleştirecek. Merhaba bölgeler arası veri çoğaltma henüz değişiklikleri toohello ikincil bölge kopyalandığı mümkün olacak şekilde, bir gecikme içerebileceği zaman uyumsuz bir işlem kaybolabilir ' dir. Merhaba sorgulayabilirsiniz ["Son eşitleme zamanı" değerini depolama hesabınızın](https://blogs.msdn.microsoft.com/windowsazurestorage/2013/12/11/windows-azure-storage-redundancy-options-and-read-access-geo-redundant-storage/) hello çoğaltma durumunu tooget ayrıntıları.

Birkaç noktalarının hello depolama coğrafi yük devretme deneyimi ile ilgili:

* Depolama coğrafi yük devretme yalnızca hello Azure depolama ekibi tarafından tetiklenir – gerekli müşteri eylemi yok.
* Mevcut depolama hizmetiniz BLOB'lar, tablolar, kuyruklar ve dosyalar için uç noktalar kalacak hello aynı hello yük devretme sonrasında; Merhaba DNS girişi hello birincil bölge toohello ikincil bölge güncelleştirilmiş toobe tooswitch gerekir.
* Önce ve hello coğrafi yük devretme sırasında toohello etkisini hello olağanüstü durum nedeniyle yazma erişimi tooyour depolama hesabına sahip olmaz ancak hala depolama hesabınız RA-GRS yapılandırılmışsa hello ikincil okuyabilirsiniz.
* Merhaba coğrafi-yük devretme işlemi tamamlanana ve DNS değişiklikleri yayılan Merhaba, okuma ve yazma erişimi tooyour depolama hesabı sürdürülecek; Bu, ikincil uç noktanız kullanılan toowhat toobe işaret eder. 
* GRS veya RA-GRS hello depolama hesabı için yapılandırılmış varsa yazma erişimi gerekir unutmayın. 
* Sorgulayabileceğiniz ["Son coğrafi yük devretme zaman" değerini depolama hesabınızın](https://msdn.microsoft.com/library/azure/ee460802.aspx) tooget daha ayrıntıları.
* Merhaba yük devretme sonrasında depolama hesabınız tam olarak çalışan ancak "bozuk" durumunda, olarak gerçekte hiçbir coğrafi çoğaltma olası sahip bir tek başına bölge içinde barındırılır. toomitigate Bu risk, biz hello özgün birincil bölge'yi ve ardından bir coğrafi geri dönme toorestore hello özgün durumuna geri yükler. Merhaba özgün birincil bölge kurtarılamaz ise, biz başka bir ikincil bölge ayırır.
  Azure Storage coğrafi çoğaltma hello altyapısı hakkında daha fazla ayrıntı için hello depolama ekibi blogu toohello makale hakkında başvurun [artıklık seçenekleri ve RA-GRS](https://blogs.msdn.microsoft.com/windowsazurestorage/2013/12/11/windows-azure-storage-redundancy-options-and-read-access-geo-redundant-storage/).

## <a name="best-practices-for-protecting-your-data"></a>Verilerinizi korumak için en iyi uygulamalar
Bazı önerilen yaklaşım tooback düzenli olarak depolama verilerinizi vardır.

* VM diskleri – kullanım hello [Azure Backup hizmeti](https://azure.microsoft.com/services/backup/) tooback, Azure sanal makineler tarafından kullanılan hello VM diskleri ayarlama.
* Blok blobları – Oluştur bir [anlık görüntü](https://msdn.microsoft.com/library/azure/hh488361.aspx) her bir blok blobunda veya kopyalama hello BLOB'lar tooanother depolama hesabı başka bir bölge kullanımında [AzCopy](storage-use-azcopy.md), [Azure PowerShell](storage-powershell-guide-full.md), veya hello [ Azure veri hareketi Kitaplığı](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/).
* Tabloları – kullanın [AzCopy](storage-use-azcopy.md) tooexport hello tablo verileri başka bir bölgede başka bir depolama hesabı içine.
* Dosyalar – kullanmak [AzCopy](storage-use-azcopy.md) veya [Azure PowerShell](storage-powershell-guide-full.md) dosyaları tooanother depolama hesabı başka bir bölgede toocopy.

Merhaba RA-GRS özelliğini tam olarak yararlanmasını uygulamaları oluşturma hakkında daha fazla bilgi için lütfen kullanıma [tasarlama yüksek oranda kullanılabilir RA-GRS depolama kullanan uygulamalar](../storage-designing-ha-apps-with-ragrs.md)

