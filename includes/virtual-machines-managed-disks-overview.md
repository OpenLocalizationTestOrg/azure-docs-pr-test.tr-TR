# <a name="azure-managed-disks-overview"></a>Azure yönetilen diskleri genel bakış

Azure yönetilen diskleri hello yöneterek Azure Iaas VM'ler için disk yönetimi basitleştirir [depolama hesapları](../articles/storage/common/storage-introduction.md) hello VM disklerle ilişkilendirilmiş. Yalnızca toospecify hello türüne sahip ([Premium](../articles/storage/common/storage-premium-storage.md) veya [standart](../articles/storage/common/storage-standard-storage.md)) ve hello boyutu duyduğunuz disk ve Azure oluşturur ve hello disk tarafından yönetilir.

## <a name="benefits-of-managed-disks"></a>Yönetilen diskleri yararları

Bazı hello avantajları elde yönetilen diskleri kullanarak bu Channel 9 video ile başlayan bir göz atalım [daha iyi Azure VM dayanıklılık yönetilen disklerle](https://channel9.msdn.com/Blogs/Azure/Managed-Disks-for-Azure-Resiliency).
<br/>
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Managed-Disks-for-Azure-Resiliency/player]

### <a name="simple-and-scalable-vm-deployment"></a>Basit ve ölçeklenebilir VM dağıtımı

Diskleri tanıtıcılarını depolama sizin için hello arka planda yönetilen. Daha önce Azure Vm'leriniz için toocreate depolama hesapları toohold hello diskleri (VHD dosyaları) sahip. Yukarı ölçeklendirilirken toomake tüm disklerinizi depolama hello IOPS sınırı aşan kaydetmedi için ek depolama hesapları oluşturulan emin vardı. Yönetilen depolama işleme diskler ile Merhaba depolama hesabı sınırları tarafından artık sınırlıdır (20.000 IOPS gibi / hesabını). Ayrıca artık özel görüntülerini (VHD dosyaları) toomultiple depolama hesaplarınızı toocopy yok. Bunları merkezi bir konumda – Azure bölgesi başına bir depolama hesabı – yönetmek ve bunları toocreate yüzlerce VM'lerin bir abonelikte kullanın.

Yönetilen diskleri etmenizi sağlar toocreate too10, 000 VM yukarı **diskleri** bir abonelikte hangi etkinleştirmenizi sağlar, binlerce toocreate **VM'ler** içinde tek bir abonelik. Bu özellik ayrıca hello ölçeklenebilirliğini artırır [sanal makine ölçek kümeleri (VMSS)](../articles/virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) bir Market görüntüsü kullanarak bir VMSS toocreate tooa bin Vm'leri yedekleme sağlayarak.

### <a name="better-reliability-for-availability-sets"></a>Kullanılabilirlik kümeleri için daha iyi güvenilirlik

Yönetilen diskleri sağlar daha iyi güvenilirlik için kullanılabilirlik kümesi o hello sağlayarak diskleri [bir kullanılabilirlik kümesindeki sanal makineleri](../articles/virtual-machines/windows/manage-availability.md#use-managed-disks-for-vms-in-an-availability-set) birbirine tooavoid tek hata noktaları yeterince yalıtılır. Bunu otomatik olarak farklı depolama ölçek birimlerinin (Damgalar) hello diskleri koyarak yapar. Bir damga toohardware veya yazılım hatası başarısız olursa, yalnızca hello VM örnekleri bu Damgalar disklerle başarısız. Örneğin, beş Vm'lerinde çalışan bir uygulamanız varsa ve bir kullanılabilirlik kümesinde hello VM'ler olan varsayalım. bir damga kullanılamaz hale gelirse hello hello uygulamanın diğer örneklerini toorun devam şekilde hello diskleri bu VM'ler için tüm aynı Damga, hello kaydedilmeyecektir.

### <a name="highly-durable-and-available"></a>Yüksek oranda dayanıklı ve kullanılabilir

Azure Diskleri %99,999 kullanılabilirlik sunacak şekilde tasarlanmıştır. Daha kolay verilerinizin yüksek dayanıklılık sağlayan üç çoğaltmaları olduğunu bilmek bekletin. Bir veya iki bile çoğaltmaları sorunlarla karşılaşırsanız, hello kalan çoğaltmaları veri ve yüksek dayanıklılık hatalarına karşı kalıcılığı sağlamaya yardımcı olur. Azure bu mimari sayesinde IaaS diskleri için tutarlı bir şekilde kurumsal düzeyde dayanıklılık sunarak sektördeki en başarılı %SIFIR Yıllık Hata Oranını elde etmektedir. 

### <a name="granular-access-control"></a>Ayrıntılı erişim denetimi

Kullanabileceğiniz [Azure rol tabanlı erişim denetimi (RBAC)](../articles/active-directory/role-based-access-control-what-is.md) tooassign yönetilen disk tooone ya da daha fazla kullanıcı için belirli izinleri. Yönetilen diskleri işlemleri dahil olmak üzere, çeşitli okuma çıkarır, yazma (oluşturma/güncelleştirme), silme ve alınırken bir [paylaşılan erişim imzası (SAS) URI](../articles/storage/common/storage-dotnet-shared-access-signature-part-1.md) hello disk için. Bir kişi tooperform işi duyar erişim tooonly hello işlemleri verebilirsiniz. Örneğin, bir kişinin toocopy yönetilen disk tooa depolama hesabı istemiyorsanız, değil toogrant erişim toohello verme eylemi, yönetilen disk için seçebilirsiniz. Bir kişinin toouse SAS URI'sini toocopy yönetilen bir disk istemiyorsanız, benzer şekilde, değil toogrant bu izni toohello seçebileceğiniz yönetilen disk.

### <a name="azure-backup-service-support"></a>Azure yedekleme hizmeti desteği
Azure Backup hizmeti, yönetilen diskleri toocreate bir yedekleme işi zaman tabanlı yedeklemeler, kolay VM geri yükleme ve yedekleme bekletme ilkeleri ile birlikte kullanın. Yönetilen diskler, yalnızca yerel olarak yedekli depolama (LRS) hello çoğaltma seçeneği olarak destekler; başka bir deyişle, tek bir bölge içinde hello veri üç kopyasını tutar. Bölgesel olağanüstü durum kurtarma için farklı bir bölgeye kullanarak VM disklerinizi yedekleme gerekir [Azure Backup hizmeti](../articles/backup/backup-introduction-to-azure-backup.md) ve yedekleme kasası olarak GRS depolama hesabı. Şu anda Azure yedekleme veri disk boyutları too1TB yedeklemek için yedekleme destekler. Şu anda hakkında daha fazla bilgiyi [kullanarak Azure Backup hizmeti yönetilen diskleri olan VM'ler için](../articles/backup/backup-introduction-to-azure-backup.md#using-managed-disk-vms-with-azure-backup).

## <a name="pricing-and-billing"></a>Fiyatlandırma ve Faturalama

Yönetilen diskleri kullanırken hello aşağıdaki fatura değerlendirmeleri geçerlidir:
* Depolama türü

* Disk Boyutu

* İşlem sayısı

* Giden veri aktarımları

* Disk anlık görüntüler (tam disk kopyası) yönetilen

Bunlar daha yakın bir göz atalım.

**Depolama türü:** yönetilen diskleri 2 performans katmanı sunar: [Premium](../articles/storage/common/storage-premium-storage.md) (SSD tabanlı) ve [standart](../articles/storage/common/storage-standard-storage.md) (HDD tabanlı). yönetilen bir diskin Hello faturalama depolama türünü hello disk için seçtiğiniz üzerinde bağlıdır.


**Disk boyutu**: yönetilen diskleri için fatura sağlanan hello hello disk boyutuna bağlıdır. Azure eşlemeleri (yuvarlanan) sağlanan boyutu toohello hello tablolar aşağıda belirtildiği gibi yönetilen diskleri seçeneği en yakın hello. Merhaba, her yönetilen disk eşlemeleri tooone sağlanan boyutları desteklenir ve buna göre faturalandırılır. Örneğin, standart yönetilen disk oluşturma ve 200 GB sağlanan boyutunu belirtirseniz, hello hello S20'in Disk türü fiyatlandırma başına faturalandırılır.

Premium yönetilen disk için kullanılabilir hello disk boyutları şunlardır:

| **Yönetilen premium <br>Disk türü** | **P4** | **P6** |**P10** | **P20** | **P30** | **P40** | **P50** | 
|------------------|---------|---------|---------|---------|----------------|----------------|----------------|  
| Disk Boyutu        | 32 GB   | 64 GB   | 128 GB  | 512 GB  | 1024 GB (1 TB) | 2048 GB (2 TB) | 4095 GB (4 TB) | 


Standart yönetilen disk için kullanılabilir hello disk boyutları şunlardır:

| **Standart yönetilen <br>Disk türü** | **S4** | **S6** | **S10** | **S20'NİN** | **S30** | **S40** | **S50** |
|------------------|---------|---------|--------|--------|----------------|----------------|----------------| 
| Disk Boyutu        | 32 GB   | 64 GB   | 128 GB | 512 GB | 1024 GB (1 TB) | 2048 GB (2 TB) | 4095 GB (4 TB) | 


**İşlem sayısı**: standart yönetilen disk üzerinde gerçekleştirdiğiniz işlem hello sayısı için faturalandırılır. Premium yönetilen disk işlemleri için ücret ödemeden yoktur.

**Giden veri aktarımları**: [giden veri aktarımları](https://azure.microsoft.com/pricing/details/data-transfers/) (Azure veri merkezlerinde dışında giderek veri) bant genişliği kullanımı için fatura doğurur.

Yönetilen diskler için fiyatlandırma hakkında ayrıntılı bilgi için bkz: [yönetilen diskleri fiyatlandırma](https://azure.microsoft.com/pricing/details/managed-disks).


## <a name="managed-disk-snapshots"></a>Yönetilen Disk anlık görüntüler

Salt okunur tam bir kopyasını, varsayılan olarak standart yönetilen disk olarak depolanan yönetilen bir disk yönetilen anlık görüntüsüdür. Anlık görüntüleri ile yönetilen disklerinizi herhangi bir noktada zamanında yedekleyebilirsiniz. Bu anlık görüntüleri hello kaynak disk bağımsız var ve kullanılan toocreate yeni yönetilen diskleri olabilir. Bunlar, kullanılan hello boyutuna göre faturalandırılır. Sağlanan kapasite 64 GB ve 10 GB gerçek kullanılan veri boyutunu ile yönetilen bir disk görüntüsünü oluşturursanız, örneğin, anlık görüntü yalnızca kullanılan hello veri boyutu 10 GB için faturalandırılır.  

[Artımlı anlık görüntüleri](../articles/virtual-machines/windows/incremental-snapshots.md) şu anda yönetilen disklerde desteklenmez, ancak hello gelecekte desteklenecektir.

nasıl toocreate anlık görüntüleri yönetilen disklerle danışın bu kaynakları toolearn hakkında daha fazla bilgi:

* [Windows’da Anlık Görüntüler kullanılarak Yönetilen Disk olarak depolanmış VHD kopyası oluşturma](../articles/virtual-machines/windows/snapshot-copy-managed-disk.md)
* [Linux’ta Anlık Görüntüler kullanılarak Yönetilen Disk olarak depolanmış VHD kopyası oluşturma](../articles/virtual-machines/windows/snapshot-copy-managed-disk.md)


## <a name="images"></a>Görüntüler

Yönetilen özel görüntü oluşturma yönetilen diskleri de destekler. Genelleştirilmiş bir (sys prepped) VM, özel bir VHD bir depolama hesabında ya da doğrudan bir görüntü oluşturabilirsiniz. Bu diskleri hello işletim sistemi ve veri diskleri dahil olmak üzere bir VM ile ilişkili tüm yönetilen tek bir görüntü yakalar. Özel görüntünüzü hello olmadan kullanarak VM'ler yüzlerce oluşturma bu etkinleştirir toocopy gerekir veya tüm depolama hesaplarını yönetin.

Görüntüleri oluşturma hakkında daha fazla bilgi için lütfen makaleler hello denetleyin:
* [Nasıl toocapture yönetilen bir Azure genelleştirilmiş bir VM görüntüsü](../articles/virtual-machines/windows/capture-image-resource.md)
* [Azure CLI 2.0 toogeneralize ve kullanarak bir Linux sanal makine yakalama nasıl hello](../articles/virtual-machines/linux/capture-image.md)

## <a name="images-versus-snapshots"></a>Görüntüleri anlık görüntüleri karşılaştırması

Genellikle hello word "VM ile birlikte kullanılan görüntü" konusuna bakın ve şimdi "anlık" de görebilirsiniz. Bunlar arasında önemli toounderstand hello fark kaynaklanır. Yönetilen disklerle serbest bıraktı genelleştirilmiş bir VM görüntüsü alabilir. Bu görüntü hello bağlı diskler toohello VM hepsini içerir. Merhaba disklerin tümü dahil edilir ve bu görüntüyü toocreate yeni bir VM kullanabilirsiniz.

Bir anlık görüntü bir hello noktada bir disk, geçen süre içinde kopyasıdır. Yalnızca tooone disk de geçerlidir. Yalnızca tek bir disk (Merhaba işletim sistemi) sahip bir VM'niz varsa, bir anlık görüntüsü veya bir görüntüsü alın ve hello anlık görüntü veya hello görüntüsünden bir VM oluşturun.

Ne VM beş disk vardır ve bunlar şeritli? Bir anlık görüntü her bir hello diskleri sürebilir ancak VM hello diskleri – hello anlık görüntüleri hello durumunun yalnızca tek bir disk hakkında bilmeniz hiçbir şeyin hello içinde yok. Bu durumda, hello anlık görüntüleri birbirleri ile eşgüdümlü toobe gerekir ve bu şu anda desteklenmiyor.

## <a name="managed-disks-and-encryption"></a>Yönetilen diskleri ve şifreleme

İki tür şifreleme toodiscuss başvuru toomanaged diskler vardır. Merhaba ilk hello depolama hizmeti tarafından gerçekleştirilen depolama hizmeti Şifrelemesi'ne (SSE) biridir. Merhaba ikinci hello işletim sistemi ve veri diskleri VM'ler için etkinleştirebilirsiniz Azure Disk şifrelemesi adrestir.

### <a name="storage-service-encryption-sse"></a>Depolama hizmeti şifrelemesi (SSE)

[Azure depolama hizmeti şifrelemesi](../articles/storage/common/storage-service-encryption.md) rest sırasında şifreleme sağlar ve veri toomeet, kuruluş güvenlik ve uyumluluk taahhüt koruma. SSE tüm yönetilen diskler, anlık görüntüler ve yönetilen diskleri olduğu kullanılabilir tüm hello bölgelerde görüntüleri için varsayılan olarak etkindir. 10 Haziran 2017 başlayan tüm yeni disk/anlık görüntüler/görüntüleri yönetilen ve otomatik olarak şifrelenmiş çalışmıyorken-Microsoft tarafından yönetilen anahtarlarla yönetilen tooexisting diskleri yazılan yeni veriler.  Merhaba ziyaret [yönetilen diskleri SSS sayfasını](../articles/virtual-machines/windows/faq-for-disks.md#managed-disks-and-storage-service-encryption) daha fazla ayrıntı için.


### <a name="azure-disk-encryption-ade"></a>Azure Disk şifrelemesi (ADE)

Azure Disk şifrelemesi tooencrypt hello işletim sistemi ve veri diskleri bir Iaas sanal makine tarafından kullanılan sağlar. Bu yönetilen disklerini de içerir. Windows için hello sürücüler, endüstri standardı BitLocker şifreleme teknolojisi kullanılarak şifrelenir. Linux için hello diskleri hello DM-Crypt teknolojisi kullanılarak şifrelenir. Bu Azure anahtar kasası tooallow ile toocontrol tümleşik ve hello disk şifreleme anahtarlarını yönetme. Daha fazla bilgi için lütfen bkz [için Azure Disk şifrelemesi Windows ve Linux Iaas VM'ler](../articles/security/azure-security-disk-encryption.md).

## <a name="next-steps"></a>Sonraki adımlar

Yönetilen diskler hakkında daha fazla bilgi için lütfen aşağıdaki makaleleri toohello bakın.

### <a name="get-started-with-managed-disks"></a>Yönetilen Diskler’i kullanmaya başlama

* [Resource Manager ve PowerShell kullanarak VM oluşturma](../articles/virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm.md)

* [Hello Azure CLI 2.0 kullanarak bir Linux VM oluşturma](../articles/virtual-machines/linux/quick-create-cli.md)

* [Yönetilen veri diski tooa Windows VM ekleme PowerShell'i kullanma](../articles/virtual-machines/windows/attach-disk-ps.md)

* [Yönetilen disk tooa Linux VM ekleme](../articles/virtual-machines/linux/add-disk.md)

* [Diskler PowerShell örnek betikler yönetilen](https://github.com/Azure-Samples/managed-disks-powershell-getting-started)

* [Azure Resource Manager şablonlarını yönetilen diskleri kullanın](../articles/virtual-machines/windows/using-managed-disks-template-deployments.md)

### <a name="compare-managed-disks-storage-options"></a>Yönetilen diskleri depolama seçenekleri Karşılaştır

* [Premium depolama ve diskleri](../articles/storage/common/storage-premium-storage.md)

* [Standart depolama ve diskleri](../articles/storage/common/storage-standard-storage.md)

### <a name="operational-guidance"></a>İşlemsel kılavuz

* [AWS ve diğer platformlar Azure tooManaged diskleri geçirme](../articles/virtual-machines/windows/on-prem-to-azure.md)

* [Azure VM'ler toomanaged diskleri Azure Dönüştür](../articles/virtual-machines/windows/migrate-to-managed-disks.md)
