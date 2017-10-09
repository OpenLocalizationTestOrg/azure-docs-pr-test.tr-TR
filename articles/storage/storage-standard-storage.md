---
title: "aaaHD tabanlı düşük maliyetli standart depolama ve Azure VM diskleri | Microsoft Docs"
description: "Düşük maliyetli standart depolama ve yönetilen ve yönetilmeyen VM diskleri tartışın."
services: storage
documentationcenter: 
author: yuemlu
manager: aungoo-msft
editor: tysonn
ms.assetid: e2a20625-6224-4187-8401-abadc8f1de91
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: yuemlu
ms.openlocfilehash: c454c61254c6b160bdf2cd39ea3319452e3e4898
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="cost-effective-standard-storage-and-unmanaged-and-managed-azure-vm-disks"></a>Düşük maliyetli standart depolama ve yönetilen ve yönetilmeyen Azure VM diskleri

Azure Standard Storage, gecikmeye duyarlı olmayan iş yükleri çalıştıran VM'ler için güvenilir, düşük maliyetli disk desteği sunar. Ayrıca, BLOB'lar, tablolar, kuyruklar ve dosyaları destekler. Standart depolama ile Merhaba verileri sabit disk sürücülerinin (HDD'ler) depolanır. VM ile birlikte çalışırken, geliştirme ve Test senaryoları ve daha az önemli iş yüklerine ve kritik üretim uygulamaları için premium depolama diskleri için standart depolama diskleri kullanabilirsiniz. Standart depolama Azure tüm bölgelerde kullanılabilir. 

Bu makalede, VM diskleri için standart depolama hello kullanımı üzerinde odaklanır. BLOB'lar, tablolar, kuyruklar ve dosyaları depolamada hello kullanımı hakkında daha fazla bilgi için lütfen toohello bakın [giriş tooStorage](storage-introduction.md).

## <a name="disk-types"></a>Disk türleri

Azure VM'ler için standart diskler toocreate iki yolu vardır:

**Yönetilmeyen diskleri**: toohello VM diskleri karşılık gelen hello depolama kullanılan hesaplar toostore hello VHD dosyaları yöneteceğiniz hello özgün yöntem budur. VHD dosyaları, sayfa bloblarını depolama hesaplarındaki olarak depolanır. Yönetilmeyen diskleri ekli tooany Azure VM boyutu, öncelikle hello DSv2 ve GS serisi gibi Premium depolama kullanın hello VM'ler dahil olabilir. Azure VM'ler birkaç standart diskler ekleme too256 TB depolama alanı VM başına izin destekler.

[**Azure yönetilen diskleri**](storage-managed-disks-overview.md): Bu özellik hello VM diskleri için kullandığınız hello depolama hesapları yönetir. Merhaba türü (Premium veya standart) ve boyutunu belirtebilir duyduğunuz disk ve Azure oluşturur ve hello disk tarafından yönetilir. Merhaba depolama hesapları için hello ölçeklenebilirlik sınırları içinde kalmasını birden çok depolama hesaplarında sipariş tooensure arasında hello diskleri yerleştirme hakkında tooworry yok--Azure, sizin için işler.

Her iki disk türleri için kullanılabilir olsa bile yönetilen diskleri tootake kendi birçok özelliğinden kullanmanızı öneririz.

Azure Standard Storage ile başlatılan tooget ziyaret [ücretsiz olarak başlayın](https://azure.microsoft.com/pricing/free-trial/). 

Nasıl toocreate VM yönetilen disklerle Lütfen birine bakın aşağıdaki hello bilgi makaleleri.

* [Resource Manager ve PowerShell kullanarak VM oluşturma](../virtual-machines/virtual-machines-windows-ps-create.md)
* [Hello Azure CLI 2.0 kullanarak bir Linux VM oluşturma](../virtual-machines/linux/quick-create-cli.md)

## <a name="standard-storage-features"></a>Standart depolama özellikleri 

Standart depolama hello özelliklerden bazıları bir göz atalım. Daha fazla ayrıntı için lütfen bkz. [giriş tooAzure depolama](storage-introduction.md).

**Standart depolama**: Azure Standard Storage destekleyen Azure diskleri, Azure BLOB'ları, Azure dosya depolama, Azure tabloları ve Azure sıralar. toouse standart depolama hizmetleri, başlayarak [bir Azure depolama hesabı oluşturma](storage-create-storage-account.md#create-a-storage-account).

**Standart depolama diskleri:** diskleri olabilir standart depolama tooall Azure Premium Storage ile gibi hello DSv2 ve GS serisi kullanılan boyutu-serisi VM'ler dahil olmak üzere sanal makineleri bağlı. Bir standart depolama diski yalnızca ekli tooone VM olabilir. Ancak, bir veya daha fazla VM toohello maksimum disk sayısı bu VM boyutu için tanımlanan yukarı bu diskleri tooa ekleyebilirsiniz. Standart depolama ölçeklenebilirlik ve performans hedefleri bölümü aşağıdaki hello biz hello belirtimleri daha ayrıntılı açıklanmıştır. 

**Standart sayfa blobu**: Standart sayfa bloblarını kalıcı diskler VM'ler için kullanılan toohold olan ve doğrudan Azure BLOB'ları diğer türleri gibi REST aracılığıyla da erişilebilir. [Sayfa blobları](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs) rastgele okuma ve yazma işlemleri için en iyi duruma getirilmiş 512 baytlık sayfaların koleksiyonudur. 

**Depolama çoğaltma:** çoğu bölgede bir standart depolama hesabı verilerde birden çok veri merkezleri arasında yerel olarak çoğaltılmış veya coğrafi olarak çoğaltılmış olabilir. Merhaba dört çoğaltma kullanılabilir yerel olarak yedekli depolama (LRS), bölge olarak yedekli depolama (ZRS), coğrafi olarak yedekli depolama (GRS) ve okuma erişimli coğrafi olarak yedekli depolama (RA-GRS) türleridir. Standart depolama yönetilen diskleri şu anda yalnızca yerel olarak yedekli depolama (LRS) destekler. Daha fazla bilgi için lütfen bkz [depolama çoğaltma](storage-redundancy.md).

## <a name="scalability-and-performance-targets"></a>Ölçeklenebilirlik ve Performans Hedefleri

Bu bölümde, biz tooconsider standart depolama kullanırken gereken hello ölçeklenebilirlik ve performans hedefleri anlatmaktadır.

### <a name="account-limits--does-not-apply-toomanaged-disks"></a>Sınırları hesap – toomanaged diskleri geçerli değildir

| **Kaynak** | **Varsayılan Sınır** |
|--------------|-------------------|
| Depolama hesabı başına  | 500 TB |
| En fazla giriş<sup>1</sup> her depolama hesabı (BİZE bölgelerde) | GRS/ZRS etkinleştirilirse, 20 GB/sn LRS için 10 GB/sn |
| En büyük çıkış<sup>1</sup> her depolama hesabı (BİZE bölgelerde) | RA-GRS/GRS/ZRS etkinleştirilirse, LRS için 30 GB/sn 20 GB/sn |
| En fazla giriş<sup>1</sup> her depolama hesabı (Avrupa ve Asya bölgeleri) | GRS/ZRS etkinleştirilirse, 10 GB/sn LRS için 5 GB/sn |
| En büyük çıkış<sup>1</sup> her depolama hesabı (Avrupa ve Asya bölgeleri) | RA-GRS/GRS/ZRS etkinleştirilirse, 15 GB/sn LRS için 10 GB/sn |
| Toplam istek (1 KB nesne boyutu varsayılarak) başına hızını depolama hesabı | Too20, 000 IOPS, saniye başına varlıklar veya saniye başına ileti |

<sup>1</sup> giriş tooa depolama hesabı gönderilen tooall veriler (istek) başvuruyor. Çıkış tooall veri depolama hesabından alınan (yanıtları) ifade eder.

Daha fazla bilgi için bkz: [Azure Storage ölçeklenebilirlik ve performans hedefleri](storage-scalability-targets.md).

Hello uygulamanızın veya tek bir depolama hesabına hello ölçeklenebilirlik hedefleri aşarsanız, uygulama toouse birden çok depolama hesabı oluşturun ve bu depolama hesaplarında verilerinizi bölüm. Alternatif olarak, Azure yönetilen diskleri birleştirebilirsiniz ve Azure hello bölümlendirme ve verilerinizi yerleştirme sizin için yönetir.

### <a name="standard-disks-limits"></a>Standart diskler sınırları

Premium diskleri hello girdi/çıktı işlemleri / saniye (IOPS) ve standart diskler (bant) verimini sağlanmayan. Merhaba standart diskler performansını değişir hello ile VM boyutu toowhich hello disk bağlı değil toohello hello diskin boyutunu. Merhaba aşağıdaki tabloda listelenen toohello performans sınırı yukarı tooachieve beklediğiniz.

**Standart diskler sınırları (yönetilen ve yönetilmeyen)**

| **VM katmanı**            | **Temel katman VM** | **Standart katmanı VM** |
|------------------------|-------------------|----------------------|
| En büyük Disk boyutu          | 4095 GB           | 4095 GB              |
| Disk başına maksimum 8 KB IOPS | Too300         | Too500            |
| Disk başına en fazla bant genişliği | Too60 MB/sn     | Too60 MB/sn        |

Yüksek performanslı, düşük gecikmeli disk desteği İş yükünüzün gerektirdiği Premium Storage kullanmayı düşünmelisiniz. Premium depolama, daha fazla yararları tooknow ziyaret [yüksek performanslı Premium depolama ve Azure VM diskleri](storage-premium-storage.md). 

## <a name="snapshots-and-copy-blob"></a>Anlık görüntüler ve kopyalama blob

toohello Depolama Birimi hizmetini hello VHD dosyasını sayfa blob ' dir. Sayfa bloblarını anlık görüntülerini almak ve bunları farklı bir depolama hesabı gibi tooanother konuma kopyalayın.

### <a name="unmanaged-disks"></a>Yönetilmeyen diskler

Oluşturabileceğiniz [artımlı anlık görüntüleri](storage-incremental-snapshots.md) hello aynı yönetilmeyen standart diskler için yolu ile standart depolama anlık görüntüleri kullanın. Anlık görüntü oluşturma ve yerel olarak yedekli depolama hesabı, kaynak disk ise, bu anlık görüntüleri tooa standart coğrafi olarak yedekli depolama hesabı kopyalama öneririz. Daha fazla bilgi için bkz: [Azure depolama artıklığı seçeneği](storage-redundancy.md).

Bir disk ekli tooa VM ise, bazı API işlemleri hello disklerde izin verilmez. Örneğin, gerçekleştiremezsiniz bir [kopyalama Blob](/rest/api/storageservices/Copy-Blob) hello disk olduğu sürece bu blob işlemi tooa VM bağlı. Bunun yerine, önce bir anlık görüntüsünü o blob hello kullanarak oluşturmak [anlık görüntü Blob](/rest/api/storageservices/Snapshot-Blob) REST API yöntemi ve hello gerçekleştirmek [kopyalama Blob](/rest/api/storageservices/Copy-Blob) hello anlık görüntü toocopy Merhaba disk eklendi. Alternatif olarak, hello disk ayırma ve gerekli işlemleri gerçekleştirin.

toomaintain coğrafi olarak yedekli, anlık görüntü kopyalarını, AzCopy veya kopya Blob kullanarak bir yerel olarak yedekli depolama hesabı tooa standart coğrafi olarak yedekli depolama hesabından anlık görüntüleri kopyalayabilirsiniz. Daha fazla bilgi için bkz: [hello AzCopy komut satırı yardımcı programı ile veri aktarma](storage-use-azcopy.md) ve [kopyalama Blob](/rest/api/storageservices/Copy-Blob).

Standart depolama hesapları sayfa bloblarını karşı REST işlemlerini gerçekleştirme hakkında ayrıntılı bilgi için bkz: [Azure Storage Hizmetleri REST API'sini](/rest/api/storageservices/Azure-Storage-Services-REST-API-Reference).

### <a name="managed-disks"></a>Yönetilen diskler

Yönetilen bir disk için bir anlık görüntü, standart yönetilen disk olarak depolanan hello yönetilen diskin salt okunur bir kopyasıdır. Artımlı anlık görüntüler şu anda yönetilen disklerde desteklenmez ancak hello gelecekte desteklenecektir.

Yönetilen bir disk ekli tooa VM ise, bazı API işlemleri hello disklerde izin verilmez. Örneğin, Hello disk ekli tooa VM olsa da bir paylaşılan erişim imzası (SAS) tooperform bir kopyalama işlemi oluşturulamıyor. Bunun yerine, önce hello diskin anlık görüntüsünü oluşturabilir ve sonra hello anlık görüntü hello kopyasını gerçekleştirin. Alternatif olarak, başlangıç diski çıkarıp bir paylaşılan erişim imzası (SAS) tooperform hello kopyalama işlemi oluşturur.

## <a name="pricing-and-billing"></a>Fiyatlandırma ve Faturalama

Standart depolama kullanırken hello aşağıdaki fatura değerlendirmeleri geçerlidir:

* Yönetilmeyen standart depolama diskleri/veri boyutu 
* Standart yönetilen disk
* Standart depolama anlık görüntüleri
* Giden veri aktarımları
* İşlemler

**Yönetilmeyen depolama diski ve veri boyutu:** yönetilmeyen diskleri ve diğer verileri (BLOB'lar, tablolar, kuyruklar ve dosyaları) için alan kullandığınızı yalnızca hello miktarı için ücretlendirilirsiniz. Örneğin, sayfa blobu 127 GB sağlanan bir VM olan hello VM gerçekten varsa, 10 GB alanı kullanarak yalnızca için 10 GB alanı faturalandırılacaksınız. Standart depolama too8191 GB ayarlama ve too4095 GB standart yönetilmeyen diskleri destekliyoruz. 

**Yönetilen diskleri:** yönetilen diskleri sağlanan hello boyutuna göre faturalandırılır. Diskinizin 10 GB disk olarak sağlanır ve yalnızca 5 GB kullanıyorsanız, hello sağlama boyutu 10 GB için tutar alınacaktır.

**Anlık Görüntü**: standart disklerin anlık görüntüleri hello anlık görüntüleri tarafından kullanılan hello ek kapasite için faturalandırılır. Anlık görüntüler hakkında daha fazla bilgi için bkz: [Blob anlık görüntüsünün oluşturulmasına](/rest/api/storageservices/Creating-a-Snapshot-of-a-Blob).

**Giden veri aktarımları**: [giden veri aktarımları](https://azure.microsoft.com/pricing/details/data-transfers/) (Azure veri merkezlerinde dışında giderek veri) bant genişliği kullanımı için fatura doğurur.

**İşlem**: Azure 0.0036 100.000 işlemleri için standart depolama başına ücretlendirilen. İşlemler ve işlem toostorage yazma hem de okuma içerir.

Standart depolama, sanal makineler ve yönetilen diskleri için fiyatlandırma hakkında ayrıntılı bilgi için bkz:

* [Azure Storage fiyatlandırması](https://azure.microsoft.com/pricing/details/storage/)
* [Sanal makineler fiyatlandırma](https://azure.microsoft.com/pricing/details/virtual-machines/)
* [Fiyatlandırma yönetilen diskleri](https://azure.microsoft.com/pricing/details/managed-disks)

## <a name="azure-backup-service-support"></a>Azure yedekleme hizmeti desteği 

Sanal makineler yönetilmeyen disklerle Azure Yedekleme kullanılarak yedeklenebilir. [Daha fazla ayrıntı](../backup/backup-azure-vms-first-look-arm.md).

Yönetilen diskleri toocreate bir yedekleme işi zaman tabanlı yedeklemeler, kolay VM geri yükleme ve yedekleme bekletme ilkeleri ile hello Azure Backup hizmeti kullanabilirsiniz. Daha fazla bilgiyi bu hakkında [kullanarak Azure Backup hizmeti yönetilen diskleri olan VM'ler için](../backup/backup-introduction-to-azure-backup.md#using-managed-disk-vms-with-azure-backup).

## <a name="next-steps"></a>Sonraki adımlar

* [Giriş tooAzure depolama](storage-introduction.md)

* [Depolama hesabı oluşturma](storage-create-storage-account.md)

* [Yönetilen Disklere Genel Bakış](storage-managed-disks-overview.md)

* [Resource Manager ve PowerShell kullanarak VM oluşturma](../virtual-machines/virtual-machines-windows-ps-create.md)

* [Hello Azure CLI 2.0 kullanarak bir Linux VM oluşturma](../virtual-machines/linux/quick-create-cli.md)
