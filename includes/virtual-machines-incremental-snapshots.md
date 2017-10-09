# <a name="back-up-azure-unmanaged-vm-disks-with-incremental-snapshots"></a>Artımlı anlık görüntüleri ile Azure yönetilmeyen VM diskleri yedekleyin
## <a name="overview"></a>Genel Bakış
Azure Storage blobları tootake anlık görüntülerini hello yeteneği sağlar. Anlık görüntüler zamandaki o noktada hello blob durumu yakalayın. Bu makalede, anlık görüntülerini kullanarak sanal makine disklerinin yedeklerini bulundurabilirsiniz bir senaryo açıklanmaktadır. Değil toouse seçtiğinizde, bu yöntemi kullanabilirsiniz Azure yedekleme ve kurtarma hizmeti ve istek toocreate, sanal makine diskleriniz için özel bir yedekleme stratejisi.

Azure virtual machine diskleri sayfa blobları Azure storage'da olarak depolanır. Sanal makine disklerini bu makalede bir yedekleme stratejisi tanımlamakta olduğunuz olduğundan, biz sayfa bloblarını hello bağlamında toosnapshots bakın. Anlık görüntüler hakkında daha fazla toolearn başvurmak çok[Blob anlık görüntüsünün oluşturulmasına](https://docs.microsoft.com/rest/api/storageservices/Creating-a-Snapshot-of-a-Blob).

## <a name="what-is-a-snapshot"></a>Bir anlık görüntü nedir?
Bir blob anlık bir noktada zamanında yakalanan bir blob, salt okunur bir sürümüdür. Bir anlık görüntü oluşturulduktan sonra okumak, kopyalanan, veya silinmiş, ancak değişiklik. Bir anda göründüğü gibi anlık bir blob yukarı şekilde tooback sağlar. REST sürüm 2015-04-05 kadar hello özelliği toocopy tam anlık görüntüleri içeriyor. Ayrıca hello REST sürüm 2015-07-08 ve üstü ile, artımlı anlık görüntüleri kopyalayabilirsiniz.

## <a name="full-snapshot-copy"></a>Tam anlık görüntü kopyalama
Anlık görüntü olabilir tooanother depolama hesabı hello temel blobu blob tookeep yedeklerini kopyalanır. Merhaba blob tooan geri yüklemeyi gibi kendi temel blob üzerinden bir anlık görüntü kopyalayabilirsiniz önceki sürümü. Bir anlık görüntü bir depolama hesabı tooanother kopyalandığında, aynı hello temel sayfa blob'u olarak boşluk hello kaplar. Bu nedenle, bir depolama hesabı tooanother tüm anlık görüntüleri kopyalama yavaş ve hello hedef depolama hesabı kadar alan kullanır.

> [!NOTE]
> Merhaba temel blob tooanother hedef kopyalarsanız, hello blob hello anlık görüntüleri onunla birlikte kopyalanmaz. Benzer şekilde, bir kopya ile temel bir blob üzerine hello temel blob ile ilişkili anlık görüntüleri etkilenmez ve hello temel blob adı altında olduğu gibi kalır.
> 
> 

### <a name="back-up-disks-using-snapshots"></a>Diskleri anlık görüntülerini kullanarak yedekleme
Sanal makine diskleriniz için bir yedekleme stratejisi da hello disk ya da sayfa blob düzenli anlık görüntülerini almak ve bunları gibi araçları kullanarak tooanother depolama hesabı kopyalayın [kopyalama Blob](https://docs.microsoft.com/rest/api/storageservices/Copy-Blob) işlemi veya [AzCopy](../articles/storage/common/storage-use-azcopy.md). Bir anlık görüntü tooa hedef sayfa blob'u farklı bir adla kopyalayabilirsiniz. Merhaba elde edilen hedef sayfa blobu yazılabilir sayfa blobu ve anlık görüntü olmayan ' dir. Bu makalenin sonraki bölümlerinde adımları tootake anlık görüntülerini kullanarak sanal makine disklerinin yedeklerini açıklanmaktadır.

### <a name="restore-disks-using-snapshots"></a>Anlık görüntülerini kullanarak disklerini geri yükle
Disk tooa kararlı hello yedekleme anlık görüntülerinin birini daha önce yakalanan sürüm zaman toorestore olduğunda, bir anlık görüntü hello temel sayfa blobu kopyalayabilirsiniz. Yükseltilen toohello temel sayfa blobu Hello anlık görüntü olduktan sonra anlık görüntü kalır hello ancak kaynağı, hem okuma ve yazılabilir bir kopya ile üzerine yazılır. Bu makalenin sonraki bölümlerinde adımları toorestore kendi anlık görüntüsünü diskinizden önceki bir sürümünü açıklar.

### <a name="implementing-full-snapshot-copy"></a>Tam anlık görüntü kopyalama uygulama
Merhaba aşağıdakileri yaparak tam anlık görüntü kopyalama uygulayabilir,

* İlk olarak, hello temel blob hello kullanarak bir anlık görüntüsünü [anlık görüntü Blob](https://docs.microsoft.com/rest/api/storageservices/Snapshot-Blob) işlemi.
* Ardından, kopyalama hello anlık görüntü tooa hedef depolama hesabı kullanılarak [kopyalama Blob](https://docs.microsoft.com/rest/api/storageservices/Copy-Blob).
* Bu işlem toomaintain yedek kopyalarını temel blob yineleyin.

## <a name="incremental-snapshot-copy"></a>Artımlı anlık görüntü kopyalama
Yeni özellik hello Hello [GetPageRanges](https://docs.microsoft.com/rest/api/storageservices/Get-Page-Ranges) API'si, bir çok daha iyi şekilde tooback sayfa BLOB'ları veya diskleri hello anlık görüntüleri yedekleme sağlar. Merhaba API hello listesini değişiklikleri hello temel blob ve hello anlık görüntüleri, arasında hello hello yedekleme hesabında kullanılan depolama alanı miktarını azaltır döndürür. Merhaba API standart depolama yanı sıra Premium depolama üzerinde sayfa bloblarını destekler. Bu API kullanarak Azure VM'ler için daha hızlı ve daha verimli yedekleme çözümleri oluşturabilirsiniz. Bu API hello REST sürüm 2015-07-08 ile kullanılabilir ve daha yüksek olur.

Artımlı anlık görüntü kopyalama toocopy gelen bir depolama hesabı tooanother hello arasındaki farkı verir,

* Temel blob ve onun anlık görüntü veya
* Merhaba temel BLOB iki tüm anlık görüntüleri

Aşağıdaki koşullar hello karşılandığından sağlanan

* Merhaba blob Oca 1 2016 veya sonraki bir sürümünde oluşturulmuş.
* Merhaba blob ile üzerine [PutPage](https://docs.microsoft.com/rest/api/storageservices/Put-Page) veya [kopyalama Blob](https://docs.microsoft.com/rest/api/storageservices/Copy-Blob) arasında iki anlık görüntüler.

**Not**: Bu özellik Premium ve standart Azure sayfa BLOB'ları için kullanılabilir.

Anlık görüntülerini kullanarak özel bir yedekleme stratejisi olduğunda hello anlık görüntü kopyalama bir depolama hesabı tooanother yavaş olabilir ve kadar depolama alanı kullanabilir. Merhaba tüm anlık görüntü tooa yedekleme depolama hesabı kopyalamak yerine art arda gelen anlık görüntüleri tooa yedekleme sayfa blobu hello birbirinden yazabilirsiniz. Bu şekilde hello zaman toocopy ve hello alanı toostore yedeklemelerini önemli ölçüde azaltılır.

### <a name="implementing-incremental-snapshot-copy"></a>Uygulama artımlı anlık görüntü kopyalama
Merhaba aşağıdakileri yaparak artımlı anlık görüntü kopyalama uygulayabilir,

* Temel blob hello kullanmanın bir anlık görüntüsünü [anlık görüntü Blob](https://docs.microsoft.com/rest/api/storageservices/Snapshot-Blob).
* Kopya hello anlık görüntü toohello hedef yedekleme depolama hesabı kullanılarak [kopyalama Blob](https://docs.microsoft.com/rest/api/storageservices/Copy-Blob). Merhaba yedekleme sayfa blobu budur. Merhaba yedekleme sayfa blobu bir anlık görüntüsünü ve hello yedekleme hesabında saklayın.
* Merhaba temel BLOB anlık görüntü Blob kullanarak başka bir anlık görüntü alın.
* Temel blob hello kullanmanın hello birinci ve ikinci anlık görüntüleri Hello birbirinden alma [GetPageRanges](https://docs.microsoft.com/rest/api/storageservices/Get-Page-Ranges). Merhaba yeni parametresini kullanın **prevsnapshot**, toospecify hello tooget hello farkı hello anlık görüntüsünü DateTime değeri. Bu parametre bulunduğunda hello REST yanıt hedef anlık görüntüsü ile Temizle sayfalar dahil olmak üzere önceki anlık arasında değiştirilen hello sayfalar içerir.
* Kullanım [PutPage](https://docs.microsoft.com/rest/api/storageservices/Put-Page) tooapply bu değişiklikleri toohello yedekleme sayfa blobu.
* Son olarak, hello yedekleme sayfa blobu bir anlık görüntüsünü ve hello yedekleme depolama hesabında saklayın.

Merhaba sonraki bölümde, biz daha ayrıntılı olarak artımlı anlık görüntü kopyalama kullanarak diskleri yedeklerini nasıl koruyabilirsiniz anlatmaktadır

## <a name="scenario"></a>Senaryo
Bu bölümde, sanal makine disklerini anlık görüntülerini kullanarak özel bir yedekleme stratejisi içeren bir senaryo açıklanmaktadır.

DS serisi Azure VM'ye bağlı premium depolama P30 diskle göz önünde bulundurun. adlı hello P30 diske *mypremiumdisk* adlı bir premium depolama hesabında depolanan *mypremiumaccount*. Standart depolama hesabı olarak adlandırılan *mybackupstdaccount* hello yedeğini depolamak için kullanılan *mypremiumdisk*. Tookeep bir anlık görüntü isteriz, *mypremiumdisk* 12 saatte bir.

Depolama hesabı ve diskleri oluşturma hakkında daha fazla toolearn başvurmak çok[Azure storage hesapları hakkında](../articles/storage/storage-create-storage-account.md).

Azure VM'lerin yedeklenmesi hakkında toolearn başvurmak çok[planlama Azure VM yedeklemeleri](../articles/backup/backup-azure-vms-introduction.md).

## <a name="steps-toomaintain-backups-of-a-disk-using-incremental-snapshots"></a>Artımlı anlık görüntülerini kullanarak bir disk adımları toomaintain yedekleri
Merhaba aşağıdaki adımlarda açıklanmaktadır nasıl tootake anlık görüntülerini *mypremiumdisk* ve hello yedeklemelerin sürdürmek *mybackupstdaccount*. Merhaba adlı bir standart sayfa blob'u yedeğidir *mybackupstdpageblob*. Merhaba yedekleme sayfa blobu her zaman aynı durum hello son anlık görüntüsü olarak hello yansıtır *mypremiumdisk*.

1. Bir anlık görüntüsü tarafından Hello yedekleme sayfa blobu, premium depolama diski oluşturma *mypremiumdisk* adlı *mypremiumdisk_ss1*.
2. Bu anlık görüntü toomybackupstdaccount adlı bir sayfa blob'u olarak kopyalamak *mybackupstdpageblob*.
3. Bir anlık görüntüsünü *mybackupstdpageblob* adlı *mybackupstdpageblob_ss1*kullanarak [anlık görüntü Blob](https://docs.microsoft.com/rest/api/storageservices/Snapshot-Blob) içinde depolamak ve *mybackupstdaccount*.
4. Merhaba Yedekleme penceresi sırasında başka bir anlık görüntüsünü oluşturmak *mypremiumdisk*, deyin *mypremiumdisk_ss2*, içinde depolamak ve *mypremiumaccount*.
5. Merhaba artımlı değişiklikler hello iki anlık görüntüler arasında almak *mypremiumdisk_ss2* ve *mypremiumdisk_ss1*kullanarak [GetPageRanges](https://docs.microsoft.com/rest/api/storageservices/Get-Page-Ranges) üzerinde  *mypremiumdisk_ss2* hello ile **prevsnapshot** parametre toohello zaman damgasını *mypremiumdisk_ss1*. Bu artımlı değişiklikler toohello yedekleme sayfa blobu yazma *mybackupstdpageblob* içinde *mybackupstdaccount*. Merhaba artımlı değişiklikler silinen aralık varsa hello yedekleme sayfa blobundan temizlenmelidir. Kullanım [PutPage](https://docs.microsoft.com/rest/api/storageservices/Put-Page) toowrite artımlı değişiklikler toohello yedekleme sayfa blobu.
6. Merhaba yedekleme sayfa blobu bir anlık görüntüsünü *mybackupstdpageblob*adlı *mybackupstdpageblob_ss2*. Merhaba önceki anlık görüntüyü silmek *mypremiumdisk_ss1* premium depolama hesabından.
7. Her yedekleme penceresi 4-6 adımlarını yineleyin. Bu şekilde, yedeklerini bulundurabilirsiniz *mypremiumdisk* bir standart depolama hesabı.

![Artımlı anlık görüntülerini kullanarak diski yedeklemeniz](../articles/virtual-machines/windows/media/incremental-snapshots/storage-incremental-snapshots-1.png)

## <a name="steps-toorestore-a-disk-from-snapshots"></a>Adımları toorestore bir diskten anlık görüntüler
Merhaba adımları izleyerek, nasıl toorestore hello premium disk açıklamak *mypremiumdisk* önceki hello yedekleme depolama hesabından anlık görüntü tooan *mybackupstdaccount*.

1. Toorestore hello premium disk için istediğiniz zaman Hello noktası belirleyin. Anlık görüntü olduğunu düşünelim *mybackupstdpageblob_ss2*, hello yedekleme depolama hesabında depolanan *mybackupstdaccount*.
2. Merhaba anlık görüntü mybackupstdaccount içinde Yükselt *mybackupstdpageblob_ss2* hello yeni yedekleme temel sayfa blobu olarak *mybackupstdpageblobrestored*.
3. Adlı bu geri yüklenen yedekleme sayfa blobu bir anlık görüntüsünü *mybackupstdpageblobrestored_ss1*.
4. Kopya geri hello sayfa blobu *mybackupstdpageblobrestored* gelen *mybackupstdaccount* çok*mypremiumaccount* hello yeni premium disk olarak  *mypremiumdiskrestored*.
5. Bir anlık görüntüsünü *mypremiumdiskrestored*adlı *mypremiumdiskrestored_ss1* gelecekteki artımlı yedekleme yapmak için.
6. Noktası hello DS serisi VM geri toohello disk *mypremiumdiskrestored* ve hello eski ayırma *mypremiumdisk* hello VM gelen.
7. Geri hello disk için önceki bölümde açıklanan hello yedekleme işlemine başlamak *mypremiumdiskrestored*, hello kullanarak *mybackupstdpageblobrestored* hello yedekleme sayfa blobu olarak.

![Disk anlık görüntülerden geri yükleme](../articles/virtual-machines/windows/media/incremental-snapshots/storage-incremental-snapshots-2.png)

## <a name="next-steps"></a>Sonraki Adımlar
Kullanım hello aşağıdaki toolearn blob anlık görüntülerini oluşturma ve VM yedekleme altyapınızı planlama hakkında daha fazla bağlar.

* [Bir BLOB bir anlık görüntü oluşturma](https://docs.microsoft.com/rest/api/storageservices/Creating-a-Snapshot-of-a-Blob)
* [VM yedekleme altyapınızı planlama](../articles/backup/backup-azure-vms-introduction.md)

