
## <a name="about-vhds"></a>VHD'ler hakkında

Sayfa bloblarını Azure standart veya premium storage hesabında depolanan .vhd dosyaları Hello Azure içinde kullanılan VHD'ler var. Sayfa blobları hakkında bilgi için bkz. [Blok bloblarını ve sayfa bloblarını anlama](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs/). Premium depolama hakkında daha fazla ayrıntı için bkz. [Yüksek performanslı premium depolama ve Azure VM'leri](../articles/storage/common/storage-premium-storage.md).

Azure sabit disk VHD biçiminde hello destekler. Bu disk uzaklığı X X blob uzaklığı depolanan şekilde biçimi sabit hello yerleştirir doğrusal olarak hello dosyası içinde kullanıma mantıksal disk hello. Merhaba blob hello sonunda küçük altbilgi hello VHD hello özelliklerini açıklar. Genellikle, çoğu diskleri büyük kullanılmayan aralıkları olması nedeniyle hello sabit bir biçime alanı boşa harcar. Ancak, Azure .vhd dosyaları seyrek bir biçimde sabit hem hello hello yararları almak ve dinamik diskler hello aynı depolar; böylece zaman. Daha ayrıntılı bilgi için bkz. [Sanal sabit diskleri kullanmaya başlama](https://technet.microsoft.com/library/dd979539.aspx).

Bir kaynak toocreate diskleri olarak toouse istediğiniz veya salt okunur görüntüleri Azure tüm .vhd dosyaları. Bir disk veya görüntü oluşturduğunuzda, Azure .vhd dosyaları hello kopyalarını oluşturur. Bu kopyalar salt okunur veya okuma-ve-yazma, hello VHD nasıl kullandığınıza bağlı olarak yüklenebilir.

Bir görüntüden sanal makine oluşturduğunuzda, Azure hello kaynak .vhd dosyasının bir kopyasını hello sanal makine için bir disk oluşturur. tooprotect yanlışlıkla silinmeye karşı Azure toocreate bir görüntü, bir işletim sistemi diski veya veri diski kullanılan tüm kaynak .vhd dosyası bir kira yerleştirir.

Bir kaynak .vhd dosyası silmeden önce hello disk veya görüntü silerek tooremove hello kira gerekir. bir işletim sistemi diski olarak bir sanal makine tarafından kullanılan bir .vhd dosyası toodelete, hello sanal makine, hello işletim sistemi diski ve hello kaynak .vhd dosyası tümünü bir defada hello sanal makinesi siliniyor ve tüm ilişkili diskleri silme silebilirsiniz. Ancak, bir veri diskinin kaynağı olan .vhd dosyasının silinmesi, belirli bir sırada birkaç adımın uygulanmasını gerektirir. İlk olarak hello disk hello sanal makine, sonra da delete hello disk ayırma ve hello .vhd dosyasını silin.

> [!WARNING]
> Kaynak .vhd dosyasını depolama alanından silerseniz veya depolama hesabınızı silerseniz, Microsoft bu verileri kurtaramaz.
> 

## <a name="types-of-disks"></a>Disk türleri 

Azure Diskleri %99,999 kullanılabilirlik sunacak şekilde tasarlanmıştır. Azure diskleri tutarlı bir şekilde endüstri lideri ile Kurumsal düzeyde dayanıklılık sıfır % Annualized hata oranı teslim.

Disklerinizi oluştururken depolama için seçebileceğiniz iki performans katmanı mevcuttur: Standart Depolama ve Premium Depolama. Ayrıca, yönetilmeyen ve yönetilen olmak üzere iki tür disk mevcuttur ve bunlar herhangi bir performans katmanın bulunabilir.


### <a name="standard-storage"></a>Standart depolama 

Standart Depolama, HDD’ler ile desteklenir ve yüksek performans sunarken uygun maliyetli depolama sağlar. Standart depolama bir veri merkezine yerel olarak çoğaltılabilir veya birincil ve ikincil veri merkezleri ile coğrafi yedekleri olabilir. Depolama çoğaltma hakkında daha fazla bilgi için bkz. [Azure Depolama çoğaltma](../articles/storage/common/storage-redundancy.md). 

VM diskleri ile Standart Depolama kullanma hakkında daha fazla bilgi için lütfen bkz. [Standart Depolama ve Diskler](../articles/storage/common/storage-standard-storage.md).

### <a name="premium-storage"></a>Premium depolama 

Premium Depolama, SSD’ler ile desteklenir ve G/Ç yoğunluklu iş yükleri için yüksek performanslı, düşük gecikme süresine sahip disk desteği sunar. Premium depolama DS, DSv2, GS, Ls veya FS serisi Azure VM'ler ile kullanabilirsiniz. Daha fazla bilgi için bkz. [Premium Depolama](../articles/storage/common/storage-premium-storage.md).

### <a name="unmanaged-disks"></a>Yönetilmeyen diskler

Yönetilmeyen diskleri hello geleneksel VM'ler tarafından kullanılan diskler türüdür. Bu, kendi depolama hesabı oluşturun ve hello disk oluşturduğunuzda, bu depolama hesabı belirtin. Toomake yok içine çok sayıda disk emin olduğunuz hello aştığından aynı depolama hesabını hello [ölçeklenebilirlik hedefleri](../articles/storage/common/storage-scalability-targets.md) hello depolama hesabını (örneğin 20.000 IOPS), sanal makineleri karşılaşıldığı hello sonuçlanır. Yönetilmeyen disklerle toomaximize hello nasıl kullandığı bir veya daha fazla depolama hesapları tooget hello en iyi performansı Vm'leriniz dışında çıkışı toofigure sahip.

### <a name="managed-disks"></a>Yönetilen diskler 

Merhaba depolama oluşturma/yönetim hello arka planda sizin için hesap ve tooworry hello hello depolama hesabı ölçeklenebilirlik sınırları hakkında sahip olmayan sağlar diskleri tanıtıcıları yönetilen. Yalnızca hello disk boyutu ve hello performans Katmanı (standart/Premium) belirtin ve Azure oluşturur ve hello disk tarafından yönetilir. Disk ekleyin veya hello VM yukarı ve aşağı doğru ölçeklendirme gibi bile, kullanılan hello depolama hakkında tooworry yok. 

Ayrıca, kendi özel görüntülerinizi Azure bölgesi başına bir depolama hesabındaki yönetmek ve toocreate yüzlerce VM'lerin hello içinde kullanabilirsiniz aynı abonelik. Yönetilen diskler hakkında daha fazla bilgi için lütfen hello bakın [yönetilen diskleri genel bakış](../articles/virtual-machines/windows/managed-disks-overview.md).

Azure yönetilen diskleri yeni VM'ler için kullanın ve birçok özellik yönetilen diskleri kullanılabilir önceki yönetilmeyen diskleri toomanaged disklerinizi hello tootake avantajlarından Dönüştür öneririz.

### <a name="disk-comparison"></a>Disk karşılaştırması

Aşağıdaki tablonun hello hem de yönetilmeyen ve hangi toouse karar diskleri toohelp yönetilen Premium vs standart karşılaştırması sağlar.

|    | Azure Premium Disk | Azure Standart Disk |
|--- | ------------------ | ------------------- |
| Disk Türü | Katı Hal Sürücüleri (SSD) | Sabit Disk Sürücüleri (HDD)  |
| Genel Bakış  | G/Ç yoğunluklu iş yükleri çalıştıran veya görev açısından kritik üretim ortamı barındıran VM’ler için SSD tabanlı, yüksek performans ve düşük gecikme süresi sunan disk desteği | Geliştirme/Test VM senaryoları için HDD tabanlı, uygun maliyetli disk desteği |
| Senaryo  | Üretim ve performansa duyarlı iş yükleri | Geliştirme/Test, kritik olmayan, <br>Nadir erişim |
| Disk Boyutu | P4: 32 GB (yalnızca yönetilen diskleri)<br>P6: 64 GB (yalnızca yönetilen diskleri)<br>P10: 128 GB<br>P20: 512 GB<br>P30: 1024 GB<br>P40: 2048 GB<br>P50: 4095 GB | Yönetilmeyen diskler: 1 GB – 4 TB (4095 GB) <br><br>Yönetilen Diskler:<br> S4: 32 GB <br>S6: 64 GB <br>S10: 128 GB <br>S20: 512 GB <br>S30: 1024 GB <br>S40: 2048 GB<br>S50: 4095 GB| 
| Disk Başına En Fazla Aktarım Hızı | 250 MB/sn | 60 MB/sn | 
| Disk başına en fazla IOPS | 7500 IOPS | 500 IOPS | 

