>[!NOTE]
> Bu sayfadaki geri bildirim veya aracılığıyla açıklamaları bırakabilirsiniz [Azure geri bildirim](https://feedback.azure.com/forums/216843-virtual-machines) #azerrormessage etiketi.

## <a name="error-response-format"></a>Hata yanıt biçimi 
Azure VM'ler hata yanıtı için JSON biçimi aşağıdaki hello kullan:

```json
{
  "status": "status code",
  "error": {
    "code":"Top level error code",
    "message":"Top level error message",
    "details":[
     {
      "code":"Inner evel error code",
      "message":"Inner level error message"
     }
    ]
   }
}
```

Bir hata yanıtı her zaman bir durum kodu ve hata nesnesi içerir. Her hata nesnesi her zaman bir hata kodu ve bir ileti içerir. Merhaba VM şablonu ile oluşturulmuşsa, hello hata nesnesi iç düzeyde hata kodları ve iletisi içeren bir ayrıntıları bölümü de içerir. Normalde, hello çoğu iç hata iletisi hello kök hatası düzeyidir.


## <a name="common-virtual-machine-management-errors"></a>Genel sanal makine Yönetimi hataları

Bu bölümde, sanal makineleri yönetirken karşılaşabileceğiniz hello genel hata iletileri listelenir:

|  Hata kodu  |  Hata iletisi  |  
|  :------| :-------------|  
|  AcquireDiskLeaseFailed  |  Tooacquire kira disk URI {1} blob kullanılarak ' {0}' oluşturulurken başarısız oldu. BLOB zaten kullanılıyor.  |  
|  AllocationFailed  |  Ayırma başarısız oldu. Lütfen hello VM boyutu veya VM sayısını azaltmayı deneyin, daha sonra yeniden deneyin veya tooa dağıtmayı deneyin farklı bir kullanılabilirlik kümesine ya da farklı Azure konumu.  |  
|  AllocationFailed  |  Merhaba VM ayırma tooan iç hata başarısız oldu. Lütfen daha sonra yeniden deneyin veya tooa farklı bir konuma dağıtmayı deneyin.  |
|  ArtifactNotFound  |  Merhaba VM uzantısı Yayımcı '{0}' ve türü '{1}' ile '{2}' konumunda bulunamadı.  |
|  ArtifactNotFound  |  Uzantısı ile Yayımcı '{0}', '{1}' yazın ve tür işleyicisi sürümü '{2}' hello uzantı deposunda bulunamadı.  |
|  ArtifactVersionNotFound  |  Hiçbir sürüm hello karşılayan hello yapıt deposunda bulunan sürüm '{0}' istedi.  |
|  ArtifactVersionNotFound  |  Merhaba karşılayan hello yapıt deposunda bulunan hiçbir sürüm sürümüyle '{0}' VM uzantısı için yayımcı '{1}' ve türü '{2}' istedi.  |
|  AttachDiskWhileBeingDetached  |  Veri disk '{0}' tooVM '{1}' Hello disk şu anda ayrılmakta olduğundan eklenemiyor. Merhaba disk tamamen ayrılana kadar bekleyin ve yeniden deneyin.  |
|  BadRequest  |  Hizalı ' kullanılabilirlik kümeleri henüz bu bölgede desteklenmiyor.  |
|  BadRequest  |  Ayrıca bir VM'in yönetilen diskleri toonon yönetilen kullanılabilirlik kümesi veya blob tabanlı disklerin toomanaged kullanılabilirlik kümesi'yle bir VM'yi eklenmesi desteklenmiyor. Lütfen bir kullanılabilirlik kümesi 'yönetilen' özellik kümesi ile yönetilen diskleri tooit'yle bir VM'yi sipariş tooadd oluşturun.  |
|  BadRequest  |  Yönetilen diskleri bu bölgede desteklenmiyor.  |
|  BadRequest  |  İşletim sistemi için desteklenmeyen işleyici başına birden çok Vmextension türü: '{0}'. VMExtension '{1}' işleyicisi '{2}' ile zaten eklendi veya girişinde belirtildi.  |
|  BadRequest  |  Kaynak yönetilen disklerle ' {1}' {0}' işlemi desteklenmiyor.  |
|  CertificateImproperlyFormatted  |  Merhaba {0} alınan parolanın JSON gösterimi, düzgün şekilde biçimlendirilmemiş bir PFX dosyası olan bir veri alanı içeriyor veya hello parolası hello PFX dosyasını doğru şekilde çözmüyor.  |
|  CertificateImproperlyFormatted  |  {0} alınan hello veri serisi JSON içinde değil.  |
|  Çakışma  |  Disk yeniden boyutlandırması, yalnızca bir VM oluşturulurken veya VM hello deallocated olduğunda izin verilir.  |
|  ConflictingUserInput  |  Disk '{0}' Hello disk zaten VM '{1}' tarafından sahiplenilmiş olarak eklenemiyor.  |
|  ConflictingUserInput  |  Kaynak ve hedef kaynak grupları olan hello aynı.  |
|  ConflictingUserInput  |  {0} diskinin kaynak ve hedef depolama hesapları farklı.  |
|  ContainerAlreadyOnLease  |  Merhaba depolama kapsayıcısı hello blob URI'si {0} olan bulunduran bir kira var..  |
|  CrossSubscriptionMoveWithKeyVaultResources  |  kaynakları taşıma isteği Hello hello istekteki bir veya daha fazla {0} s tarafından başvurulan KeyVault kaynakları içeriyor. Bu çapraz abonelik taşıma şu anda desteklenmiyor. Merhaba hello KeyVault kaynak kimlikleri için hata ayrıntılarını gözden geçirin.  |
|  DiagnosticsOperationInternalError  |  VM {0} tanılama profili işlenirken bir iç hata oluştu.  |
|  DiskBlobAlreadyInUseByAnotherDisk  |  BLOB {0} tooVM '{1}' ait başka bir disk tarafından zaten kullanılıyor. Merhaba disk başvuru bilgisi hello blob meta verilerini inceleyebilirsiniz.  |
|  DiskBlobNotFound  |  Yüklenemiyor toofind VHD blob URI'si {0} disk '{1}'.  |
|  DiskBlobNotFound  |  Yüklenemiyor toofind VHD blob URI'si ile {0}.  |
|  DiskEncryptionKeySecretMissingTags  |  {0} gizli hello {1} etiketleri sahip değil. Lütfen hello parolanın sürümünü güncelleştirin, hello gerekli etiketleri ekleyip yeniden deneyin.  |
|  DiskEncryptionKeySecretUnwrapFailed  |  Başarısız anahtar {1} kullanarak gizli {0} değerini açılacak.  |
|  DiskImageNotReady  |  Disk görüntüsü {0} {1} durumda. Görüntü hazır olduğunda lütfen yeniden deneyin.  |
|  DiskPreparationError  |  VM diskleri hazırlanırken bir veya daha fazla hata oluştu. Ayrıntılar için disk örneği görünümüne bakın.  |
|  DiskProcessingError  |  Merhaba VM başarısız olan disklerle diğer diskler içerdiğinden disk işleme işlemi durduruldu.  |
|  ImageBlobNotFound  |  Yüklenemiyor toofind VHD blob URI'si {0} disk '{1}'.  |
|  ImageBlobNotFound  |  Yüklenemiyor toofind VHD blob URI'si ile {0}.  |
|  IncorrectDiskBlobType  |  Disk blobları yalnızca türü sayfa blobu olabilir. Disk '{1}' için BLOB {0} ise blok blobu türünde değil.  |
|  IncorrectDiskBlobType  |  Disk blobları yalnızca türü sayfa blobu olabilir. BLOB {0} '{1}' türünde.  |
|  IncorrectImageBlobType  |  Disk blobları yalnızca türü sayfa blobu olabilir. Disk '{1}' için BLOB {0} ise blok blobu türünde değil.  |
|  IncorrectImageBlobType  |  Disk blobları yalnızca türü sayfa blobu olabilir. BLOB {0} '{1}' türünde.  |
|  InternalOperationError  |  Depolama hesabı {0} çözümlenemedi. Lütfen oluşturulduğu hello depolama kaynak sağlayıcısı hello aynı olduğundan emin olun konumu hello olarak işlem kaynağı.  |
|  InternalOperationError  |  {0} hedef arama görevi başarısız oldu.  |
|  InternalOperationError  |  VM '{0}' hello ağ profili doğrulanırken hata oluştu.  |
|  InvalidAccountType  |  Merhaba AccountType {0} geçersiz.  |
|  InvalidParameter  |  Parametre {0} Hello değeri geçersiz.  |
|  InvalidParameter  |  Belirtilen hello yönetici parolası izin verilmiyor.  |
|  InvalidParameter  |  "hello sağlanan parola olmalıdır. {0} arasında-\ {1\} karakter uzunluğunda ve en az getirmelidir hello şu parola karmaşıklık gereksinimlerinden {2}: <ol><li> Büyük bir karakter içeriyor</li><li>Küçük bir karakter içeriyor</li><li>Sayısal hane içerir</li><li>Özel bir karakter içeriyor.</li></ol>  |
|  InvalidParameter  |  Merhaba belirtilen yönetici kullanıcı adı geçerli değil.  |
|  InvalidParameter  |  Merhaba VM bir platform veya kullanıcı görüntüsünden oluşturulduysa var olan bir işletim sistemi diski eklenemiyor.  |
|  InvalidParameter  |  {0} kapsayıcı adı geçersiz. Kapsayıcı adları 3-63 karakter uzunluğunda olmalıdır ve yalnızca küçük harf alfasayısal karakterler ve tire içerebilir. Tire başında olmalıdır ve bir alfasayısal karakter.  |
|  InvalidParameter  |  Kapsayıcı {0} URL {1} adı geçersiz. Kapsayıcı adları 3-63 karakter uzunluğunda olmalıdır ve yalnızca küçük harf alfasayısal karakterler ve tire içerebilir. Tire başında olmalıdır ve bir alfasayısal karakter.  |
|  InvalidParameter  |  URL {0} Hello blob adı bir eğik çizgi içerir. Bu diskleri için şu anda desteklenmiyor.  |
|  InvalidParameter  |  Merhaba URI {0} toobe doğru blob URI'si aramaz.  |
|  InvalidParameter  |  Bir disk '{0}' zaten kullanıyor adlı aynı LUN'u hello: {1}.  |
|  InvalidParameter  |  '{0}' adlı bir disk yok.  |
|  InvalidParameter  |  Kullanıcı görüntüsü geçersiz kılmaları hello belirtilen önceden tanımlanmış bir disk için belirtilemez görüntü başvurusu.  |
|  InvalidParameter  |  Bir disk '{0}' zaten kullanıyor adlı aynı VHD URL'si {1} hello.  |
|  InvalidParameter  |  Merhaba belirtilen hata etki alanı sayısı {0} hello aralığı {1} too\ {2\} olmalıdır.  |
|  InvalidParameter  |  {0} Hello lisans türü geçersiz. Geçerli lisans türleri: Windows_Client ve Windows_Server, büyük küçük harfe duyarlı.  |
|  InvalidParameter  |  Linux ana bilgisayar adı en fazla {0} karakter uzunluğunda veya hello aşağıdaki karakterleri içeremez: {1}.  |
|  InvalidParameter  |  Ssh ortak anahtarları için hedef yolu olan şu anda sınırlı tooits varsayılan değer {0} sorunu Linux sağlama aracısındaki bilinen son tooa.  |
|  InvalidParameter  |  {0} adlı LUN'da zaten bir disk var.  |
|  InvalidParameter  |  Merhaba isteği abonelik {0} hello yönetilen disk kimliğindeki hello abonelik {1} eşleşmesi gerekir.  |
|  InvalidParameter  |  OSProfile özel verileri Base64 ile kodlanmalı ve en fazla {0} karakter uzunluğunda olmalıdır.  |
|  InvalidParameter  |  URL {0} BLOB adı '{1}' uzantısıyla bitmelidir.  |
|  InvalidParameter  |  {0}' geçerli bir yakalanmış VHD blob adı öneki değil. Geçerli bir önek regex '{1}' ile eşleşir.  |
|  InvalidParameter  |  Merhaba VM Aracısı sağlanmadan sertifikaları tooyour VM eklenemez.  |
|  InvalidParameter  |  {0} adlı LUN'da zaten bir disk var.  |
|  InvalidParameter  |  Merhaba boyutu {0} istediğinden oluşturulamıyor toocreate hello VM burada hello kullanılabilirlik kümesi şu anda ayrılan hello kümede kullanılabilir değil. Merhaba kullanılabilir boyutları: {1}. Daha fazla üzerinde VM stratejisi https://aka.ms/azure-resizevm adresindeki yeniden boyutlandırma okuyun.  |
|  InvalidParameter  |  VM boyutu ' {0} hello geçerli bölgede kullanılamıyor Hello istedi. Merhaba geçerli bölgede kullanılabilen Hello boyutu: {1}. Merhaba kullanılabilir VM boyutları hakkında daha fazla bilgi https://aka.ms/azure-regions adresindeki her bölgede öğrenin.  |
|  InvalidParameter  |  VM boyutu ' {0} hello geçerli bölgede kullanılamıyor Hello istedi. Merhaba kullanılabilir VM boyutları hakkında daha fazla bilgi https://aka.ms/azure-regions adresindeki her bölgede öğrenin.  |
|  InvalidParameter  |  Windows yönetici kullanıcı adı olamaz fazlasını {0} karakterden uzun, ile bitemez veya hello aşağıdaki karakterleri içeremez: {1}.  |
|  InvalidParameter  |  Windows bilgisayar adı {0} karakterden uzun, tamamen sayısal veya aşağıdaki karakterleri hello içeren sayısından daha fazla olamaz: {1}.  |
|  MissingMoveDependentResources  |  Merhaba kaynakları taşıma isteği tüm hello bağımlı kaynakları içermiyor. Eksik kaynak kimlikleri için hata ayrıntılarını gözden geçirin.  |
|  MoveResourcesHaveInvalidState  |  Merhaba kaynakları taşıma isteği geçersiz depolama hesaplarıyla ilişkili VM'ler içerir. Bu kaynak kimlikleri ve başvurulan depolama hesabı adları ayrıntılarını gözden geçirin.  |
|  MoveResourcesHavePendingOperations  |  Merhaba kaynakları taşıma isteği, bir işlemi bekliyor kaynaklar içeriyor. Bu kaynak kimliklerinin ayrıntılarını gözden geçirin. Merhaba bekleyen işlemleri tamamladıktan sonra işlemi yeniden deneyin.  |
|  MoveResourcesNotFound  |  Merhaba isteği bulunamayan kaynaklar içeriyor kaynakları taşıyın. Bu kaynak kimliklerinin ayrıntılarını gözden geçirin.  |
|  NetworkingInternalOperationError  |  Bilinmeyen ağ ayırma hatası.  |
|  NetworkingInternalOperationError  |  Bilinmeyen ağ ayırma hatası  |
|  NetworkingInternalOperationError  |  Merhaba VM ağ profili işlenirken bir iç hata oluştu.  |
|  notFound  |  Merhaba {0} kullanılabilirlik kümesi bulunamıyor.  |
|  notFound  |  Kaynak sanal makine '{0}' hello istekte belirtilen Azure bu konumda mevcut değil.  |
|  notFound  |  {0} kimlikli kiracı bulunamadı.  |
|  notFound  |  Merhaba görüntüsü {0} bulunamıyor.  |
|  NotSupported  |  Merhaba lisans türü {0}, ancak hello görüntü blob {1} şirket içinden değil.  |
|  OperationNotAllowed  |  Kullanılabilirlik kümesi {0} silinemez. Bir kullanılabilirlik kümesi silmeden önce lütfen tüm VM içermediğinden emin olun.  |
|  OperationNotAllowed  |  Kullanılabilirlik değiştirme SKU 'Hizalı' too'Classic Ayarla ' verilmez.  |
|  OperationNotAllowed  |  Merhaba VM çalışmadığı zaman hello VM uzantıları değiştirilemez.  |
|  OperationNotAllowed  |  Merhaba yakalama eylem yalnızca blob tabanlı disklerin sahip bir sanal makine üzerinde desteklenir. Lütfen hello 'Image' kaynak API'leri toocreate yönetilen bir sanal makineden bir görüntü kullanın.  |
|  OperationNotAllowed  |  Görüntüsü başarıyla oluşturuldu kadar görüntü {1} hello {0} kaynağı oluşturulamıyor.  |
|  OperationNotAllowed  |  VM ayrılır olduğunda VM serbest bırakıldıktan sonra lütfen yeniden deneyin güncelleştirmeleri tooencryptionSettings izin verilmez  |
|  OperationNotAllowed  |  Blob tabanlı disklerin yönetilen disk tooa VM eklenmesi desteklenmiyor.  |
|  OperationNotAllowed  |  veri diski maksimum sayısı Hello bağlı toobe tooa bu boyutu VM'i {0} izin verilir.  |
|  OperationNotAllowed  |  Bir blob tabanlı disk tooVM yönetilen disklerle eklenmesi desteklenmiyor.  |
|  OperationNotAllowed  |  '{0}' işlemi '{1}' görüntüde, görüntü silinmek üzere işaretlenmiş hello itibaren izin verilmiyor. Yalnızca hello silme işlemini yeniden deneyin (veya bir devam eden bir toocomplete için bekleyin).  |
|  OperationNotAllowed  |  '{0}' işlemi '{1}' VM VM genelleştirilmiş hello bu yana izin verilmiyor.  |
|  OperationNotAllowed  |  Geri yükleme noktası koleksiyonu '{1}' silinmek üzere işaretlenmiş şekilde işlemi '{0}' izin verilmiyor.  |
|  OperationNotAllowed  |  '{0}' işlemi silinmek için işaretlendiğinden VM uzantısı '{1}' izin verilmiyor. Yalnızca hello silme işlemini yeniden deneyin (veya bir devam eden bir toocomplete için bekleyin).  |
|  OperationNotAllowed  |  Merhaba sanal makineleri '{1}' hello Görüntü '{2}' kullanılarak sağlanır beri işlemi '{0}' izin verilmiyor.  |
|  OperationNotAllowed  |  Sanal makine ScaleSet '{1}' Hello hello Görüntü '{2}' şu anda kullanıldığından işlemi '{0}' izin verilmiyor.  |
|  OperationNotAllowed  |  '{0}' işlemi VM '{1}', VM silinmek üzere işaretlenmiş hello itibaren izin verilmiyor. Yalnızca hello silme işlemini yeniden deneyin (veya bir devam eden bir toocomplete için bekleyin).  |
|  OperationNotAllowed  |  Merhaba VM serbest kaldırıldığından veya işaretli toobe olduğundan '{0}' işlemi '{1}' VM üzerinde izin verilmiyor.  |
|  OperationNotAllowed  |  '{0}' işlemi VM '{1}' hello VM çalıştıran bu yana izin verilmiyor. Lütfen kapatma açıkça kapattığınız durumda hello VM'den hello konuk işletim sistemi içinde.  |
|  OperationNotAllowed  |  '{0}' işlemi VM '{1}' VM değil serbest hello itibaren izin verilmiyor.  |
|  OperationNotAllowed  |  VM uzantısı '{2}' başarısız durumda olduğundan '{0}' işlemi '{1}' VM üzerinde izin verilmiyor.  |
|  OperationNotAllowed  |  Başka bir işlem sürmekte olduğundan işlem '{0}' VM '{1}' izin verilmiyor.  |
|  OperationNotAllowed  |  Merhaba işlemi '{0}' hello sanal makine '{1}' toobe Genelleştirmiş gerektirir.  |
|  OperationNotAllowed  |  Merhaba işlemi çalıştıran hello VM toobe gerektirir (veya toorun ayarlayın).  |
|  OperationNotAllowed  |  Olan hello daha küçük {1}GB görüntüsündeki karşılık gelen disk boyutu, izin disk boyutu {0} GB.  |
|  OperationNotAllowed  |  '{0}' işleyicisinin VM ölçek kümesi uzantıları yalnızca VM ölçek kümesi oluşturma hello aynı anda eklenebilir.  |
|  OperationNotAllowed  |  '{0}' işleyicisinin VM ölçek kümesi uzantıları yalnızca VM ölçek kümesi silme hello aynı anda silinebilir.  |
|  OperationNotAllowed  |  VM '{0}', yönetilen diskleri zaten kullanıyor.  |
|  OperationNotAllowed  |  VM '{0}' ait too'Classic' kullanılabilirlik kümesi '{1}'. Lütfen güncelleştirme hello kullanılabilirlik toouse 'Hizalı' SKU ayarlayın ve sonra hello dönüştürme işlemini yeniden deneyin.  |
|  OperationNotAllowed  |  Görüntüden oluşturulan VM blob tabanlı disklerin sahip olamaz. Tüm diskleri yönetilen toobe diskler vardır.  |
|  OperationNotAllowed  |  Yakalama hello VM genelleştirilmiş olmadığından işlem tamamlanamıyor.  |
|  OperationNotAllowed  |  VM diskleri dönüştürülmüş toomanaged diskleri yükleniyor olduğundan VM '{0}' yönetim işlemlerini izin verilmez.  |
|  OperationNotAllowed  |  Devam eden bir işlem sanal makine {0} too\ {1\} güç durumunu değiştirme. Lütfen bir süre sonra işlemi {2} gerçekleştirin.  |
|  OperationNotAllowed  |  %S tooadd veya güncelleştirme hello VM. VM boyutu {0} hello varolan ayırma biriminde kullanılamayabilir Hello istedi. Daha fazla üzerinde VM stratejisi https://aka.ms/azure-resizevm adresindeki yeniden boyutlandırma okuyun.  |
|  OperationNotAllowed  |  Merhaba boyutu {0} istediğinden oluşturulamıyor tooresize hello VM burada hello kullanılabilirlik kümesi şu anda ayrılan hello kümede kullanılabilir değil. Merhaba kullanılabilir boyutları: {1}. Daha fazla üzerinde VM stratejisi https://aka.ms/azure-resizevm adresindeki yeniden boyutlandırma okuyun.  |
|  OperationNotAllowed  |  Merhaba boyutu {0} istediğinden oluşturulamıyor tooresize hello VM burada hello VM şu anda ayrılmış hello kümede kullanılabilir değil. Lütfen, VM too\ {1\} ayırması tooresize (hello Azure portal'ın durdurma işlemi budur) hello yeniden boyutlandırma işlemi yeniden deneyin. Daha fazla üzerinde VM stratejisi https://aka.ms/azure-resizevm adresindeki yeniden boyutlandırma okuyun.  |
|  OSProvisioningClientError  |  Şu anda Hello konuk işletim sistemi sağlanmakta olduğundan VM için '{0}' işletim sistemi sağlama işlemi başarısız oldu.  |
|  OSProvisioningClientError  |  VM için '{0}' işletim sistemi sağlama başarısız oldu. Hata ayrıntıları: {1} (genelleştirildiğinden) emin hello görüntü düzgün hazırlanmış olun. <ul><li>Windows için yönergeler: https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/  </li></ul> |
|  OSProvisioningClientError  |  SSH ana anahtar oluşturma işlemi başarısız oldu. Hata ayrıntıları: {0}. Bu sorunu doğrulamak Linux Aracısı düzgün bir şekilde ayarlanırsa tooresolve. <ul><li>Merhaba yönergeleri denetleyebilirsiniz: https://azure.microsoft.com/documentation/articles/virtual-machines-linux-agent-user-guide/ </li></ul> |
|  OSProvisioningClientError  |  Kullanıcı adı, hello için belirtilen VM bu Linux dağıtım için geçersiz. Hata ayrıntıları: {0}.  |
|  OSProvisioningInternalError  |  İşletim sistemi sağlama VM için '{0}' tooan iç hata başarısız oldu.  |
|  OSProvisioningTimedOut  |  İşletim sistemi sağlama VM '{0}' için zaman ayrılan hello tamamlamadı. Merhaba VM hala başarıyla sağlama işlemi tamamlanmamış olabilir. Lütfen sağlama durumunu daha sonra denetleyin.  |
|  OSProvisioningTimedOut  |  İşletim sistemi sağlama VM '{0}' için zaman ayrılan hello tamamlamadı. Merhaba VM hala başarıyla sağlama işlemi tamamlanmamış olabilir. Lütfen sağlama durumunu daha sonra denetleyin. Ayrıca, hello görüntü düzgün hazırlanmış emin olun (genelleştirildiğinden).   <ul><li>Windows için yönergeler: https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/ </li><li> Linux için yönergeler: https://azure.microsoft.com/documentation/articles/virtual-machines-linux-capture-image/</li></ul>  |
|  OSProvisioningTimedOut  |  İşletim sistemi sağlama VM '{0}' için zaman ayrılan hello tamamlamadı. Ancak, hello VM Konuk Aracısı çalıştıran algılandı. Bu hello konuk işletim sistemi olmayan süredir düzgün şekilde hazırlanmış bir VM görüntüsü olarak kullanılan toobe öneren (CreateOption ile FromImage =). tooresolve Bu sorun, ya da kullanım hello CreateOption ile olduğu gibi VHD Attach = ya da bir görüntü olarak kullanmak için düzgün şekilde hazırlayın:   <ul><li>Windows için yönergeler: https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/ </li><li> Linux için yönergeler: https://azure.microsoft.com/documentation/articles/virtual-machines-linux-capture-image/</li></ul>  |
|  OverConstrainedAllocationRequest  |  Merhaba gereken VM boyutu hello Seçilen konumda şu anda kullanılabilir değil.  |
|  ResourceUpdateBlockedOnPlatformUpdate  |  Kaynak tooongoing platform güncelleştirmesi nedeniyle şu anda güncelleştirilemiyor. Lütfen daha sonra tekrar deneyin.  |
|  StorageAccountLimitation  |  Depolama hesabı '{0}' gerekli toocreate diskleri olan sayfa bloblarını desteklemez.  |
|  StorageAccountLimitation  |  '{0}' adlı depolama hesabı, ayrılmış kotasını aştı.  |
|  StorageAccountLocationMismatch  |  Depolama hesabı {0} çözümlenemedi. Lütfen oluşturulduğu hello depolama kaynak sağlayıcısı hello aynı olduğundan emin olun konumu hello olarak işlem kaynağı.  |
|  StorageAccountNotFound  |  Bulunamadı depolama hesabı {0}. Depolama hesabı silinmez ve toohello ait olun hello VM aynı Azure konumunda.  |
|  StorageAccountNotRecognized  |  Lütfen depolama kaynağı sağlayıcısı tarafından yönetilen bir depolama hesabı kullanın. {0} kullanımı desteklenmiyor.  |
|  StorageAccountOperationInternalError  |  {0} adlı depolama hesabına erişilirken bir iç hata oluştu.  |
|  StorageAccountSubscriptionMismatch  |  Depolama hesabı {0} toosubscription {1} ait değil.  |
|  StorageAccountTooBusy  |  '{0}' depolama hesabı şu anda çok meşgul. Başka bir hesabı kullanmayı deneyin.  |
|  StorageAccountTypeNotSupported  |  Disk {0} bir Blob Depolama hesabı olan {1} kullanır. Lütfen genel amaçlı depolama hesabıyla yeniden deneyin.  |
|  StorageAccountTypeNotSupported  |  Depolama hesabı {0} {1} türü değil. Önyükleme tanılaması {2} depolama hesabı türlerini destekler.  |
|  SubscriptionNotAuthorizedForImage  |  Merhaba abonelik yetkilendirilmemiş.  |
|  TargetDiskBlobAlreadyExists  |  BLOB {0} zaten var. Lütfen farklı bir blob URI'si toocreate yeni boş veri diski '{1}' belirtin.  |
|  TargetDiskBlobAlreadyExists  |  Yakalama işlemine devam edilemiyor çünkü hedef görüntü blobu {0} zaten var ve hello bayrağı toooverwrite VHD BLOB'ları ayarlı değil. Merhaba blobu silin veya toooverwrite VHD BLOB'ları hello bayrağını ayarlayın ve yeniden deneyin.  |
|  TargetDiskBlobAlreadyExists  |  {0} hedef görüntü blobunun üzerinde etkin bir kira olduğundan yakalama işlemine devam edilemiyor.   |
|  TargetDiskBlobAlreadyExists  |  BLOB {0} zaten var. Lütfen farklı bir blob URI'si '{1}' diski için hedef olarak belirtin.  |
|  TooManyVMRedeploymentRequests  |  VM için '{0}' çok fazla yeniden dağıtım isteği alındı veya bu VM ile aynı kullanılabilirlik hello Vm'lerde hello. Lütfen daha sonra yeniden deneyin.  |
|  VHDSizeInvalid  |  Merhaba belirtilen {0} disk blob {2} ile ' {1}' için disk boyutu değeri geçersiz. Disk boyutu {3} ve {4} arasında olmalıdır.  |
|  VMAgentStatusCommunicationError  |  VM '{0}', VM aracısının veya uzantılarının durumunu bildirmedi. Lütfen hello VM çalışan bir VM Aracısı olduğunu doğrulayın ve giden bağlantılar tooAzure depolama kurabilirsiniz.  |
|  VMArtifactRepositoryInternalError  |  Merhaba yapıt deposu tooretrieve VM yapıt ayrıntılarını ile iletişim kurulurken bir hata oluştu.  |
|  VMArtifactRepositoryInternalError  |  Merhaba yapıt deposundan hello VM yapıt verileri alınırken bir iç hata oluştu.  |
|  VMExtensionHandlerNonTransientError  |  İşleyici '{0}' bildirdi hatası VM uzantısı '{1}' terminal hata kodu '{2}' ve hata iletisi: '{3}'  |
|  VMExtensionManagementInternalError  |  '{0}' VM uzantısı işlenirken iç hata oluştu.  |
|  VMExtensionManagementInternalError  |  Merhaba VM uzantıları hazırlanırken birden çok hata oluştu. Ayrıntılar için VM uzantısı örnek görünümüne bakın.  |
|  VMExtensionProvisioningError  |  VM uzantısı '{0}' işlenirken bir hata bildirdi. Hata iletisi: "{1}".  |
|  VMExtensionProvisioningError  |  Birden çok VM uzantıları hello VM üzerinde sağlanan toobe başarısız oldu. Lütfen ayrıntılar için hello VM uzantısı örnek görünümüne bakın.  |
|  VMExtensionProvisioningTimeout  |  '{0}' VM uzantısının sağlanması zaman aşımına uğradı. Genişletme yüklemesinin çok uzun sürüyor veya uzantı durumu sağlanamadı.  |
|  VMMarketplaceInvalidInput  |  Olmayan Market görüntüsünden sanal makine oluşturma bilgi planlama değil, lütfen hello Plan bilgileri hello istekte kaldırın. İşletim sistemi disk adı {0} ' dir.  |
|  VMMarketplaceInvalidInput  |  Merhaba satın alma bilgileri eşleşmiyor. Merhaba Market görüntüsünden toodeploy oluşturulamıyor. İşletim sistemi disk adı {0} ' dir.  |
|  VMMarketplaceInvalidInput  |  Market görüntüsünden sanal makine oluşturulurken Plan bilgisi hello isteği gerektirir. İşletim sistemi disk adı {0} ' dir.  |
|  VMNotFound  |  '{0}' Hello VM bulunamıyor.  |
|  VMRedeploymentFailed  |  VM '{0}' vm'inin yeniden dağıtımı tooan iç hata başarısız oldu. Lütfen daha sonra yeniden deneyin.  |
|  VMRedeploymentTimedOut  |  Yeniden dağıtım VM '{0}' zaman ayrılan hello bitmedi. Başarıyla içinde süre bitirmek. Aksi takdirde, hello isteği yeniden deneyebilirsiniz.  |
|  VMStartTimedOut  |  VM '{0}' zaman ayrılan hello başlatılmadı. Merhaba VM hala başarıyla başlatılabilir. Lütfen daha sonra hello güç durumunu denetleyin.  |


## <a name="next-steps"></a>Sonraki adımlar
Daha fazla yardıma gereksinim duyarsanız, başvurabilirsiniz üzerinde Azure uzmanlar hello [MSDN Azure ve yığın taşması forumları hello](https://azure.microsoft.com/support/forums/). Alternatif olarak, Azure destek olay dosya. Toohello Git [Azure Destek sitesi](https://azure.microsoft.com/support/options/) seçip **alma desteği**.
