# <a name="frequently-asked-questions-about-azure-iaas-vm-disks-and-managed-and-unmanaged-premium-disks"></a>Azure Iaas sanal diskler ve yönetilen ve yönetilmeyen premium diskler hakkında sık sorulan sorular

Bu makalede Azure yönetilen diskleri ve Azure Premium Storage hakkında sık sorulan bazı sorular yanıtlanmaktadır.

## <a name="managed-disks"></a>Yönetilen Diskler

**Azure yönetilen diskleri nedir?**

Yönetilen diskleri depolama hesabı yönetimini işleyerek Azure Iaas VM'ler için disk yönetimi basitleştiren bir özelliktir. Daha fazla bilgi için bkz: Merhaba [yönetilen diskleri genel bakış](../articles/virtual-machines/windows/managed-disks-overview.md).

**Standart yönetilen disk 80 GB olan varolan bir VHD'yi oluşturursanız, ne kadar bana maliyeti ne olacak?**

80 GB VHD'den oluşturulan standart yönetilen disk S10 disk hello sonraki kullanılabilir standart disk boyutu kabul edilir. According toohello S10 disk fiyatlandırma ücret ödersiniz. Daha fazla bilgi için bkz: Merhaba [fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/storage).

**Standart yönetilen disk için herhangi bir işlem maliyetleri vardır?**

Evet. Her işlem için ücret ödersiniz. Daha fazla bilgi için bkz: Merhaba [fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/storage).

**Standart yönetilen disk için sağlanan hello hello disk kapasitesini veya hello gerçek hello diskteki hello verilerin boyutunu için t ücretlendirilir?**

Sağlanan hello hello disk kapasitesine göre ücret ödersiniz. Daha fazla bilgi için bkz: Merhaba [fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/storage).

**Nasıl yönetilen premium diskleri yönetilmeyen disklerden farklı fiyatlandırma olduğu?**

Yönetilen premium diskleri Hello fiyatlandırma olduğu hello yönetilmeyen premium diskler ile aynı.

**Merhaba depolama hesabı türü (standart veya Premium) yönetilen disklerim değiştirebilir miyim?**

Evet. Hello Azure portal, PowerShell veya hello Azure CLI kullanarak yönetilen disklerinizi hello depolama hesabı türünü değiştirebilirsiniz.

**I kopyalayın veya böylelikle yönetilen disk tooa özel depolama hesabını verme bir yolu var mı?**

Evet. Hello Azure portal, PowerShell veya hello Azure CLI kullanarak yönetilen disklerinizi dışarı aktarabilirsiniz.

**Bir Azure depolama hesabı toocreate yönetilen bir disk VHD dosyasında farklı bir aboneliğe kullanabilir miyim?**

Hayır.

**Farklı bir bölgede bir Azure depolama hesabı toocreate yönetilen bir disk VHD dosyasında kullanabilir miyim?**

Hayır.

**Yönetilen diskler kullanan müşteriler için ölçek sınırlamalar var mı?**

Yönetilen diskleri depolama hesaplarıyla ilişkili hello sınırları ortadan kaldırır. Ancak, hello yönetilen diskleri abonelik başına sınırlı too2, varsayılan olarak 000 sayısıdır. Bu sayı destek tooincrease çağırabilirsiniz.

**Yönetilen bir diskin artımlı bir anlık görüntüsünü alın?**

Hayır. Merhaba geçerli anlık görüntü özelliği yönetilen bir disk tam bir kopyasını oluşturur. Ancak, biz toosupport artımlı anlık görüntülerini hello gelecekteki planladığınıza.

**Sanal makineleri bir kullanılabilirlik kümesinde yönetilen ve yönetilmeyen diskleri birleşiminden oluşabilir?**

Hayır. Merhaba sanal makineleri bir kullanılabilirlik kümesinde, tüm yönetilen diskleri veya tüm yönetilmeyen diskler kullanmanız gerekir. Bir kullanılabilirlik kümesi oluşturduğunuzda, disk türünü seçebilirsiniz toouse istiyor.

**Yönetilen diskleri hello varsayılan seçeneği hello Azure portal mi?**

Şu anda değil ancak gelecekteki hello hello varsayılan olur.

**Boş bir yönetilen diski oluşturabilir miyim?**

Evet. Boş bir disk oluşturabilirsiniz. Yönetilen bir disk tooa VM eklemeden VM bağımsız olarak, örneğin, oluşturulabilir.

**Yönetilen diskleri kullanan bir kullanılabilirlik kümesi için desteklenen hello hata etki alanı sayısı nedir?**

Yönetilen diskleri kullanan hello kullanılabilirlik kümesi bulunduğu hello bağlı olarak, desteklenen hello hata etki alanı sayısı 2 veya 3 bölgedir.

**Nasıl ayarlanan diagnostics hello standart depolama hesabı mı?**

VM tanılama için özel depolama hesabı ayarlayın. Hello gelecekteki, biz tooswitch tanılama planlama tooManaged diskler.

**Ne tür bir rol tabanlı erişim denetimi desteğini yönetilen disklerde var mı?**

Diskleri desteklediği üç anahtar varsayılan rol yönetilen:

* Sahibi: erişim dahil her şeyi yönetebilir
* Katkıda bulunan: erişim dışında her şeyi yönetebilir
* Okuyucu: her şeyi görüntüleyebilir ancak değişiklik yapamaz

**I kopyalayın veya böylelikle yönetilen disk tooa özel depolama hesabını verme bir yolu var mı?**

Hesap ya da şirket içi toocopy hello içeriği tooa özel depolama depolama URI yönetilen hello için disk ve kullanacak salt okunur paylaşılan erişim imzası elde edebilirsiniz.

**Yönetilen my disk kopyasını oluşturabilir miyim?**

Müşteriler, kendi yönetilen diskleri bir anlık görüntüsünü ve ardından başka bir yönetilen disk hello anlık görüntü toocreate kullanın.

**Yönetilmeyen diskleri hala desteklenmektedir?**

Evet. Yönetilen ve yönetilmeyen diskleri destekliyoruz. Yeni iş yükleri için yönetilen diskleri kullanın ve geçerli iş yükleri toomanaged disklerinizi geçirmenizi öneririz.


**128 GB disk oluşturma ve hello boyutu too130 GB artırın, ı hello sonraki için disk boyutu (512 GB) ücretlendirilir?**

Evet.

**Yerel olarak yedekli depolama, coğrafi olarak yedekli depolama, oluşturabiliyorum ve bölge olarak yedekli depolama yönetilen disklerde?**

Azure yönetilen diskleri şu anda yönetilen yalnızca yerel olarak yedekli depolama disklerini destekler.

**Daraltma veya miyim yönetilen disklerim downsize?**

Hayır. Bu özellik şu anda desteklenmiyor. 

**Merhaba bilgisayar adı özelliği, özelleştirilmiş (Merhaba Sistem Hazırlama aracı kullanılarak oluşturulan veya genelleştirilmiş) işletim sistemi diski kullanılan tooprovision VM olduğunda değiştirebilir miyim?**

Hayır. Merhaba bilgisayar adı özelliği güncelleştirilemiyor. Merhaba yeni VM hello üst kullanılan toocreate hello işletim sistemi disk VM devralır. 

**Yönetilen disklerle örnek Azure Resource Manager şablonları toocreate VM'ler nereden bulabilirim?**
* [Yönetilen diskleri kullanarak şablonları](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)
* https://github.com/chagarw/MDPP

## <a name="managed-disks-and-storage-service-encryption"></a>Diskler ve depolama hizmeti şifrelemesi yönetilen 

**Azure depolama hizmeti şifrelemesi, yönetilen bir disk oluşturduğunuzda, varsayılan olarak etkindir?**

Evet.

**Merhaba şifreleme anahtarları yöneten?**

Microsoft hello şifreleme anahtarları yönetir.

**I depolama hizmeti şifrelemesi yönetilen disklerim için devre dışı bırakabilirim?**

Hayır.

**Depolama hizmeti şifrelemesi, yalnızca belirli bölgelerde kullanılabilir?**

Hayır. Tarafından yönetilen diskleri kullanılabilir olduğu tüm hello bölgelerde kullanılabilir. Yönetilen diskleri kullanılabilir tüm genel bölgeler ve Almanya.

**Nasıl ı yönetilen my disk şifrelenir öğrenebilirsiniz?**

Yönetilen bir disk hello Azure portal, hello Azure CLI ve PowerShell oluşturulduğu hello zaman bulabilirsiniz. Merhaba saat 9 Haziran 2017 sonra ise, disk şifrelenir. 

**10 Haziran 2017 önce oluşturulan mevcut disklerim nasıl şifreleyebilir mi?**

10 Haziran 2017 itibariyle yönetilen tooexisting diskleri yazılan yeni veriler otomatik olarak şifrelenir. Biz de tooencrypt var olan verileri planlama ve hello şifreleme zaman uyumsuz olarak hello arka planda gerçekleşir. Var olan verileri artık şifrelemeniz gerekir, diskinizin bir kopyasını oluşturun. Yeni disk şifrelenir.

* [Hello Azure CLI kullanarak yönetilen diskleri kopyalama](../articles/virtual-machines/scripts/virtual-machines-linux-cli-sample-copy-managed-disks-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json)
* [PowerShell kullanarak yönetilen diskleri kopyalama](../articles/virtual-machines/scripts/virtual-machines-windows-powershell-sample-copy-managed-disks-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json)

**Yönetilen anlık görüntüler ve şifrelenmiş görüntüleri misiniz?**

Evet. Yönetilen tüm anlık görüntüler ve 9 Haziran 2017 sonra oluşturulan görüntüleri otomatik olarak şifrelenir. 

**Sanal makineleri olan veya önceden şifrelenmiş toomanaged diskleri depolama hesaplarında yer alan yönetilmeyen disklerle dönüştürebilirsiniz?**

Evet

**Yönetilen bir disk veya bir anlık görüntü dışarı aktarılan bir VHD'den de şifrelenir mi?**

Hayır. Ancak, bir VHD tooan dışa depolama hesabından bir şifrelenmiş yönetilen disk veya anlık görüntü şifrelenmiş sonra şifrelenir. 

## <a name="premium-disks-managed-and-unmanaged"></a>Premium diskler: yönetilen ve yönetilmeyen

**VM bir DSv2 gibi Premium Storage destekleyen bir boyutu serisi kullanıyorsa ı premium ve standart veri diskleri ekleyebilir miyim?** 

Evet.

**Premium ve Premium depolama D, Dv2, G veya F serisi gibi desteklemiyor standart veri diskleri tooa boyutu serisi ekleyebilir miyim?**

Hayır. Premium Storage destekleyen bir boyutu serisi kullanmayan standart veri diskleri tooVMs ekleyebilirsiniz.

**80 GB varolan bir VHD'den premium veri diski oluşturursanız, ne kadar maliyeti ne olacak?**

80 GB VHD'den oluşturulan bir premium veri diski P10 disk hello sonraki kullanılabilir premium disk boyutu kabul edilir. According toohello P10 disk fiyatlandırma ücret ödersiniz.

**İşlem maliyetleri toouse Premium depolama var mı?**

IOPS ve üretilen iş ile belirli sınırları sağlanan gelen her disk boyutu için sabit bir maliyeti yoktur. Merhaba diğer maliyetlerin giden bant genişliği ve anlık görüntü kapasite varsa markalarıdır. Daha fazla bilgi için bkz: Merhaba [fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/storage).

**IOPS ve hello disk önbellekten elde edebilirsiniz işleme için hello sınırları nelerdir?**

önbellek için birleşik sınırları hello ve DS serisi için yerel SSD: çekirdek başına 4.000 IOPS ve çekirdek saniyede 33 MB. Merhaba GS serisi çekirdek başına 5.000 IOPS'yi ve çekirdek saniyede 50 MB sunar.

**Yerel SSD yönetilen diskleri VM için desteklenen hello mi?**

Merhaba yerel SSD yönetilen diskleri VM ile birlikte sağlanan geçici depolama olur. Var. ek bu geçici depolama için bir maliyeti yoktur. Azure Blob depolama alanına kalıcı değildir çünkü bu yerel SSD toostore'ı uygulama verilerinizi kullanmamanızı öneririz.

**Var. herhangi varsa hello için kullanacağı KIRPMA premium disklerde?**

Hiçbir KIRPMA ya da premium Azure disklerde veya standart diskler dezavantajı toohello kullanımını yoktur.

## <a name="new-disk-sizes-managed-and-unmanaged"></a>Yeni disk boyutları: yönetilen ve yönetilmeyen

**Merhaba işletim sistemi ve veri diskleri için desteklenen en büyük disk boyutu nedir?**

bir işletim sistemi diski için Azure destekleyen hello bölüm hello ana önyükleme kaydı (MBR) türüdür. Merhaba MBR biçimi too2 TB bir disk boyutunu destekler. bir işletim sistemi diski için Azure destekleyen hello en büyük boyutu 2 TB ' dir. Veri diskleri too4 TB yukarı Azure destekler. 

**Desteklenen hello büyük sayfa blob boyutu nedir?**

Azure destekleyen hello büyük sayfa blob boyutu 8 TB (8191 GB) ' dir. Sayfa bloblarını veri veya işletim sistemi diskler olarak 4 TB (4.095 GB) bağlı tooa VM büyük desteklemiyoruz.

**Toouse yeni bir sürüm gerekiyor mu Azure Araçları toocreate ekleme, yeniden boyutlandırma ve 1 TB'den büyük olan diskler karşıya?**

Var olan Azure Araçları toocreate tooupgrade gerekmez, ekleme ya da 1 TB'den büyük diskleri yeniden boyutlandırma. VHD dosyası tooupload doğrudan tooAzure bir sayfa blobu veya yönetilmeyen disk olarak şirket içi, toouse hello en son aracı kümeleri gerekir:

|Azure Araçları      | Desteklenen sürümler                                |
|-----------------|---------------------------------------------------|
|Azure PowerShell | Sürüm numarası 4.1.0'da: Haziran 2017 sürüm veya daha yenisi|
|Azure CLI v1     | Sürüm numarası 0.10.13: May 2017 sürüm veya daha yenisi|
|AzCopy           | Sürüm numarası 6.1.0: Haziran 2017 sürüm veya daha yenisi|

Azure CLI v2 ve Azure Storage Gezgini Hello desteği yakında geliyor. 

**P4 ve P6 disk boyutları yönetilmeyen diskleri veya sayfa BLOB'ları için destekleniyor mu?**

Hayır. P4 (32 GB) ve P6 (64 GB) disk boyutları, yalnızca yönetilen diskler için desteklenir. Yönetilmeyen diskleri ve sayfa bloblarını desteği yakında geliyor.

**Nasıl yönetilen my varolan premium hello küçük bir disk (15 Haziran 2017) etkinleştirilmeden önce 64 GB oluşturulduğu daha az disk varsa, onu faturalandırılır?**

64 GB'den küçük var olan küçük premium disklerin faturalandırılır toobe according toohello P10 fiyatlandırma katmanı devam edin. 

**Merhaba disk katmanını 64 GB'den küçük küçük premium diskleri P10 tooP4 veya P6 nasıl geçiş yapabilirim?**

Küçük disklerinizi bir anlık görüntüsünü ve fiyatlandırma katmanı tooP4 disk tooautomatically anahtar hello oluşturmak veya P6 sağlanan hello boyutuna göre. 


## <a name="what-if-my-question-isnt-answered-here"></a>Ne sorumun cevabı burada cevaplanıp değil mi?

Sorunuzun yanıtını burada listelenmiyorsa, bize bildirin ve yanıt bulmanıza yardımcı olacağız. Bu makalenin hello sonunda bir soru hello açıklamaları nakledebilirsiniz. hello Azure depolama ekibi ile tooengage ve diğer topluluk üyeleri bu makale hakkında kullanmak hello MSDN [Azure depolama Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata).

toorequest özellikleri gönderme istekleri ve fikir toohello [Azure Storage geri bildirim Forumunda](https://feedback.azure.com/forums/217298-storage).
