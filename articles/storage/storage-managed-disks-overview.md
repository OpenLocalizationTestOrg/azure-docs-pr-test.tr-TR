---
title: "Azure Premium ve standart yönetilen disk genel bakış | Microsoft Docs"
description: "Azure yönetilen depolama hesaplarını Azure VM'ler kullanırken işler diskler, genel bakış"
services: storage
documentationcenter: na
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 272250b3-fd4e-41d2-8e34-fd8cc341ec87
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: robinsh
ms.openlocfilehash: b9bc70ec9e271a8e0b34ed415e27cd350390b21d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-managed-disks-overview"></a>Azure yönetilen diskleri genel bakış

Azure yönetilen diskleri yöneterek Azure Iaas VM'ler için disk yönetimi basitleştirir [depolama hesapları](storage-introduction.md) VM disklerle ilişkilendirilmiş. Yalnızca türü belirtmek zorunda ([Premium](storage-premium-storage.md) veya [standart](storage-standard-storage.md)) ihtiyacınız diskin boyutunu ve Azure oluşturur ve disk tarafından yönetilir.

## <a name="benefits-of-managed-disks"></a>Yönetilen diskleri yararları

Geçirmesine yönetilen diskleri kullanarak bu Channel 9 video ile başlayan avantajlarından bazıları bir göz atalım [daha iyi Azure VM dayanıklılık yönetilen disklerle](https://channel9.msdn.com/Blogs/Azure/Managed-Disks-for-Azure-Resiliency).
<br/>
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Managed-Disks-for-Azure-Resiliency/player]

### <a name="simple-and-scalable-vm-deployment"></a>Basit ve ölçeklenebilir VM dağıtımı

Diskleri tanıtıcılarını depolama sizin için arka planda yönetilen. Daha önce Azure Vm'leriniz için diskleri (VHD dosyaları) tutmak için storage hesapları oluşturmanız gerekirdi. Yukarı ölçeklendirilirken tüm disklerinizi depolama IOPS sınırı aşan kaydetmedi için ek depolama hesapları oluşturulan emin olmak zorunda kaldı. Yönetilen depolama işleme diskler ile depolama hesabı sınırları tarafından artık sınırlıdır (20.000 IOPS gibi / hesabını). Ayrıca artık birden çok depolama hesabı için kendi özel görüntülerinizi (VHD dosyaları) kopyalamanız gerekir. Bunları merkezi bir konumda – Azure bölgesi başına bir depolama hesabı – yönetebilir ve bunları bir abonelikte VM'ler yüzlerce oluşturmak için kullanın.

Yönetilen diskleri etmenizi sağlar 10.000 VM oluşturmak **diskleri** bir abonelikte hangi etkinleştirecek binlerce oluşturmanızı **VM'ler** içinde tek bir abonelik. Bu özellik ayrıca ölçeklenebilirliğini artırır [sanal makine ölçek kümeleri (VMSS)](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) bir Market görüntüsü kullanarak bir VMSS kadar binlerce VM'ler oluşturmanızı sağlayarak.

### <a name="better-reliability-for-availability-sets"></a>Kullanılabilirlik kümeleri için daha iyi güvenilirlik

Yönetilen diskleri sağlar daha iyi güvenilirlik için kullanılabilirlik kümesi, disklerinin sağlayarak [bir kullanılabilirlik kümesindeki sanal makineleri](../virtual-machines/windows/manage-availability.md#use-managed-disks-for-vms-in-an-availability-set) yeterince tek hata noktaları bulundurmaktan önlemek için birbirinden yalıtılır. Bunu diskleri otomatik olarak farklı depolama ölçek birimlerinin (Damgalar) koyarak yapar. Bir damga donanım veya yazılım arızasından dolayı başarısız olursa bu Damgalar disklerde yalnızca VM örnekleriyle başarısız. Örneğin, beş Vm'lerinde çalışan bir uygulamanız varsa ve bir kullanılabilirlik kümesindeki sanal makineleri olan varsayalım. Bu VM'lerin tümü aynı damgaya kaydedilmeyecektir için bir damga uygulamanın diğer örnekleri aşağı kalırsa diskleri kadar çalışmaya devam eder.

### <a name="highly-durable-and-available"></a>Yüksek oranda dayanıklı ve kullanılabilir

Azure Diskleri %99,999 kullanılabilirlik sunacak şekilde tasarlanmıştır. Daha kolay verilerinizin yüksek dayanıklılık sağlayan üç çoğaltmaları olduğunu bilmek bekletin. Çoğaltmaların birinde hatta ikisinde sorunlarla karşılaşılırsa, kalan çoğaltmalar verilerinizin kalıcı olmasını ve başarısızlıklara karşı yüksek tolerans gösterilmesini sağlar. Azure bu mimari sayesinde IaaS diskleri için tutarlı bir şekilde kurumsal düzeyde dayanıklılık sunarak sektördeki en başarılı %SIFIR Yıllık Hata Oranını elde etmektedir. 

### <a name="granular-access-control"></a>Ayrıntılı erişim denetimi

Kullanabileceğiniz [Azure rol tabanlı erişim denetimi (RBAC)](../active-directory/role-based-access-control-what-is.md) bir veya daha fazla kullanıcılara yönetilen bir disk için belirli izinler atamak için. Yönetilen diskleri işlemleri dahil olmak üzere, çeşitli okuma çıkarır, yazma (oluşturma/güncelleştirme), silme ve alınırken bir [paylaşılan erişim imzası (SAS) URI](storage-dotnet-shared-access-signature-part-1.md) disk. Yalnızca bir kişinin işini gerçekleştirmek için gereken işlemleri için erişim izni verebilir. Örneğin, yönetilen bir disk bir depolama hesabına kopyalamak için bir kişinin istemiyorsanız, bu yönetilen disk verme eylemi için erişim vermek seçebilirsiniz. Benzer şekilde, yönetilen bir diske kopyalamak için bir SAS URI'sini kullanmak için bir kişinin istemiyorsanız, bu yönetilen disk izni olmayan seçebilirsiniz.

### <a name="azure-backup-service-support"></a>Azure yedekleme hizmeti desteği
Azure Backup hizmeti yönetilen disklerle zaman tabanlı yedeklemeler, kolay VM geri yükleme ve yedekleme bekletme ilkeleri ile bir yedekleme işi oluşturmak için kullanın. Yönetilen diskler, yalnızca yerel olarak yedekli depolama (LRS) çoğaltma seçeneği olarak destekler; başka bir deyişle, tek bir bölge içinde verileri üç kopyasını tutar. Bölgesel olağanüstü durum kurtarma için farklı bir bölgeye kullanarak VM disklerinizi yedekleme gerekir [Azure Backup hizmeti](../backup/backup-introduction-to-azure-backup.md) ve yedekleme kasası olarak GRS depolama hesabı. Şu anda Azure yedekleme desteklediği veri diski yedekleme için 1 TB'ye kadar boyutları. Şu anda hakkında daha fazla bilgiyi [kullanarak Azure Backup hizmeti yönetilen diskleri olan VM'ler için](../backup/backup-introduction-to-azure-backup.md#using-managed-disk-vms-with-azure-backup).

## <a name="pricing-and-billing"></a>Fiyatlandırma ve Faturalama

Yönetilen diskleri kullanırken, aşağıdaki fatura değerlendirmeleri geçerlidir:
* Depolama türü

* Disk Boyutu

* İşlem sayısı

* Giden veri aktarımları

* Disk anlık görüntüler (tam disk kopyası) yönetilen

Bunlar daha yakın bir göz atalım.

**Depolama türü:** yönetilen diskleri 2 performans katmanı sunar: [Premium](storage-premium-storage.md) (SSD tabanlı) ve [standart](storage-standard-storage.md) (HDD tabanlı). Hangi tür depolama için disk üzerinde seçmiş olduğunuz yönetilen bir disk faturalama bağlıdır.


**Disk boyutu**: yönetilen diskleri için fatura sağlanan disk boyutuna bağlıdır. Azure, aşağıdaki tabloda belirtildiği gibi yakın yönetilen diskleri seçeneğine (yuvarlanan) sağlanan boyutu eşler. Yönetilen her disk desteklenen sağlanan boyutlarından birini eşler ve buna göre faturalandırılır. Örneğin, standart yönetilen disk oluşturma ve 200 GB sağlanan boyutunu belirtirseniz, fiyatlandırma S20'in Disk türüne göre faturalandırılır.

Premium yönetilen disk için kullanılabilir disk boyutları şunlardır:

| **Yönetilen premium <br>Disk türü** | **P4** | **P6** |**P10** | **P20** | **P30** | **P40** | **P50** | 
|------------------|---------|---------|---------|---------|----------------|----------------|----------------|  
| Disk Boyutu        | 32 GB   | 64 GB   | 128 GB  | 512 GB  | 1024 GB (1 TB) | 2048 GB (2 TB) | 4095 GB (4 TB) | 


Standart yönetilen disk için kullanılabilir disk boyutları şunlardır:

| **Standart yönetilen <br>Disk türü** | **S4** | **S6** | **S10** | **S20'NİN** | **S30** | **S40** | **S50** |
|------------------|---------|---------|--------|--------|----------------|----------------|----------------| 
| Disk Boyutu        | 32 GB   | 64 GB   | 128 GB | 512 GB | 1024 GB (1 TB) | 2048 GB (2 TB) | 4095 GB (4 TB) | 


**İşlem sayısı**: standart yönetilen disk üzerinde gerçekleştirdiğiniz işlem sayısı için faturalandırılır. Premium yönetilen disk işlemleri için ücret ödemeden yoktur.

**Giden veri aktarımları**: [giden veri aktarımları](https://azure.microsoft.com/pricing/details/data-transfers/) (Azure veri merkezlerinde dışında giderek veri) bant genişliği kullanımı için fatura doğurur.

Yönetilen diskler için fiyatlandırma hakkında ayrıntılı bilgi için bkz: [yönetilen diskleri fiyatlandırma](https://azure.microsoft.com/pricing/details/managed-disks).


## <a name="managed-disk-snapshots"></a>Yönetilen Disk anlık görüntüler

Salt okunur tam bir kopyasını, varsayılan olarak standart yönetilen disk olarak depolanan yönetilen bir disk yönetilen anlık görüntüsüdür. Anlık görüntüleri ile yönetilen disklerinizi herhangi bir noktada zamanında yedekleyebilirsiniz. Bu anlık görüntüler kaynak disk bağımsız var ve yeni yönetilen diskleri oluşturmak için kullanılabilir. Bunlar, kullanılan boyutuna göre faturalandırılır. Sağlanan kapasite 64 GB ve 10 GB gerçek kullanılan veri boyutunu ile yönetilen bir disk görüntüsünü oluşturursanız, örneğin, anlık görüntü yalnızca kullanılan veri boyutu 10 GB için faturalandırılır.  

[Artımlı anlık görüntüleri](storage-incremental-snapshots.md) şu anda yönetilen disklerde desteklenmez, ancak gelecekte desteklenecektir.

Yönetilen disklerle anlık görüntüleri oluşturma hakkında daha fazla bilgi için aşağıdaki kaynaklara gözatın:

* [Windows’da Anlık Görüntüler kullanılarak Yönetilen Disk olarak depolanmış VHD kopyası oluşturma](../virtual-machines/windows/snapshot-copy-managed-disk.md)
* [Linux’ta Anlık Görüntüler kullanılarak Yönetilen Disk olarak depolanmış VHD kopyası oluşturma](../virtual-machines/linux/snapshot-copy-managed-disk.md)


## <a name="images"></a>Görüntüler

Yönetilen özel görüntü oluşturma yönetilen diskleri de destekler. Genelleştirilmiş bir (sys prepped) VM, özel bir VHD bir depolama hesabında ya da doğrudan bir görüntü oluşturabilirsiniz. Bu işletim sistemi ve veri diskleri de dahil olmak üzere bir VM ile ilişkili disk tüm yönetilen tek bir görüntü yakalar. Bu, kopyalama veya herhangi bir depolama hesabı yönetmek için özel görüntünüzü gerek kalmadan kullanarak VM'ler oluşturma yüzlerce sağlar.

Görüntüleri oluşturma hakkında daha fazla bilgi için lütfen aşağıdaki makalelere bakın:
* [Genelleştirilmiş bir Azure VM'de yönetilen bir görüntüsünü yakalama](../virtual-machines/windows/capture-image-resource.md)
* [Generalize ve Azure CLI 2.0 kullanarak bir Linux sanal makine yakalama](../virtual-machines/linux/capture-image.md)

## <a name="images-versus-snapshots"></a>Görüntüleri anlık görüntüleri karşılaştırması

Genellikle "VM ile birlikte kullanılan görüntü" word bakın ve şimdi "anlık" de görebilirsiniz. Bunlar arasındaki farkı anlamak önemlidir. Yönetilen disklerle serbest bıraktı genelleştirilmiş bir VM görüntüsü alabilir. Bu görüntü VM'ye bağlı disklerin tümünü içerir. Yeni bir VM oluşturmak için bu görüntüyü kullanabilirsiniz ve tüm diskler dahil edilir.

Bir anlık görüntü bir noktada bir disk, geçen süre içinde kopyasıdır. Yalnızca bir diske uygulanır. Yalnızca tek bir disk (OS) sahip bir VM'niz varsa, bir anlık görüntüsü veya bir görüntüsü alın ve anlık görüntü veya görüntü bir VM oluşturun.

Ne VM beş disk vardır ve bunlar şeritli? Disklerin her biri bir anlık görüntüsünü, ancak anlık görüntülerin yalnızca tek bir disk hakkında bilmeniz hiçbir şeyin – disklerin durumunu VM dahilinde olduğu. Bu durumda, anlık görüntüleri birbirleri ile uyumlu olması gerekir ve bu şu anda desteklenmiyor.

## <a name="managed-disks-and-encryption"></a>Yönetilen diskleri ve şifreleme

Şifreleme bağlamında yönetilen diskleri tartışmak için iki tür vardır. İlk Depolama hizmeti tarafından gerçekleştirilen depolama hizmeti Şifrelemesi'ne (SSE) sağlayıcıdır. İkincisi, işletim sistemi ve veri diskleri VM'ler için etkinleştirebilirsiniz Azure Disk Şifrelemesi ' dir.

### <a name="storage-service-encryption-sse"></a>Depolama hizmeti şifrelemesi (SSE)

[Azure depolama hizmeti şifrelemesi](storage-service-encryption.md) rest sırasında şifreleme sağlar ve Kuruluş güvenliği ve uyumluluğu taahhüt karşılamak için verilerinizi koruyun. SSE tüm yönetilen diskler, anlık görüntüler ve yönetilen diskleri olduğu kullanılabilir tüm bölgelerde görüntüleri için varsayılan olarak etkindir. 10 Haziran 2017 başlayan tüm yeni disk/anlık görüntüler/görüntüleri yönetilen ve otomatik olarak şifrelenmiş çalışmıyorken-Microsoft tarafından yönetilen anahtarlarla varolan yönetilen diske yazılan yeni veriler.  Ziyaret [yönetilen diskleri SSS sayfasını](storage-faq-for-disks.md#managed-disks-and-storage-service-encryption) daha fazla ayrıntı için.


### <a name="azure-disk-encryption-ade"></a>Azure Disk şifrelemesi (ADE)

Azure Disk şifrelemesi bir Iaas sanal makine tarafından kullanılan işletim sistemi ve veri diskleri şifrelemenizi sağlar. Bu yönetilen disklerini de içerir. Windows için sürücüleri, endüstri standardı BitLocker şifreleme teknolojisi kullanılarak şifrelenir. Linux için DM-Crypt teknolojisini kullanan diskleri şifrelenir. Bu, denetlemek ve disk şifreleme anahtarlarını yönetmek izin vermek için Azure anahtar kasası ile tümleşiktir. Daha fazla bilgi için lütfen bkz [için Azure Disk şifrelemesi Windows ve Linux Iaas VM'ler](../security/azure-security-disk-encryption.md).

## <a name="next-steps"></a>Sonraki adımlar

Yönetilen diskler hakkında daha fazla bilgi için lütfen aşağıdaki makalelere bakın.

### <a name="get-started-with-managed-disks"></a>Yönetilen Diskler’i kullanmaya başlama

* [Resource Manager ve PowerShell kullanarak VM oluşturma](../virtual-machines/virtual-machines-windows-ps-create.md)

* [Azure CLI 2.0 kullanarak bir Linux VM oluşturma](../virtual-machines/linux/quick-create-cli.md)

* [Bir Windows PowerShell kullanarak bir VM için bir yönetilen veri diski Ekle](../virtual-machines/windows/attach-disk-ps.md)

* [Linux VM’ye yönetilen disk ekleme](../virtual-machines/linux/add-disk.md)

* [Diskler PowerShell örnek betikler yönetilen](https://github.com/Azure-Samples/managed-disks-powershell-getting-started)

* [Azure Resource Manager şablonlarını yönetilen diskleri kullanın](storage-using-managed-disks-template-deployments.md)

### <a name="compare-managed-disks-storage-options"></a>Yönetilen diskleri depolama seçenekleri Karşılaştır

* [Premium depolama ve diskleri](storage-premium-storage.md)

* [Standart depolama ve diskleri](storage-standard-storage.md)

### <a name="operational-guidance"></a>İşlemsel kılavuz

* [Azure yönetilen disklere AWS ve diğer platformlar geçirme](../virtual-machines/windows/on-prem-to-azure.md)

* [Azure yönetilen diskleri Azure VM'ler Dönüştür](../virtual-machines/windows/migrate-to-managed-disks.md)
