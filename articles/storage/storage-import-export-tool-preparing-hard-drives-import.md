---
title: "aaaPreparing sabit sürücüler için bir Azure içeri/dışarı aktarma alma işi | Microsoft Docs"
description: "Nasıl tooprepare sabit sürücüleri kullanarak WAImportExport aracı toocreate hello Azure içeri/dışarı aktarma hizmeti için bir içeri aktarma işi hello öğrenin."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: muralikk
ms.openlocfilehash: 3f247a9efee29da2d18140353edc9dd7103a0761
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="preparing-hard-drives-for-an-import-job"></a>Sabit sürücüler için içeri aktarma işi hazırlama

Merhaba WAImportExport hello sürücü hazırlama ve hello ile kullanabileceğiniz Onarım Aracı araçtır [Microsoft Azure içeri/dışarı aktarma hizmeti](storage-import-export-service.md). Tooship tooan Azure veri merkezine giderek bu aracı toocopy veri toohello sabit sürücüleri kullanabilirsiniz. İçe aktarma işi tamamlandıktan sonra bu aracı toorepair bozuldu, eksik olan veya çakışan BLOB diğer BLOB'lar ile kullanabilirsiniz. Tamamlanan dışa aktarma işleminden hello sürücüleri aldıktan sonra bu aracı toorepair bozuldu herhangi bir dosya ya da hello sürücülerde eksik kullanabilirsiniz. Bu makalede, bu aracın hello kullanımı gidin.

## <a name="prerequisites"></a>Ön koşullar

### <a name="requirements-for-waimportexportexe"></a>WAImportExport.exe gereksinimleri

- **Makine Yapılandırması**
  - Windows 7, Windows Server 2008 R2 veya daha yeni Windows işletim sistemi
  - .NET framework 4 yüklü olması gerekir. Bkz: [SSS](#faq) nasıl .net Framework ise toocheck hello makinede yüklü.
- **Depolama hesabı anahtarı** -hello hesabı anahtarları en az biri için hello depolama hesabı gerekir.

### <a name="preparing-disk-for-import-job"></a>Disk için içeri aktarma işi hazırlama

- **BitLocker -** BitLocker hello makine çalışan hello WAImportExport aracı üzerinde etkinleştirilmesi gerekir. Merhaba bkz [SSS](#faq) nasıl tooenable BitLocker.
- **Diskleri** WAImportExport aracın çalıştığı makineden erişilebilir. Bkz: [SSS](#faq) disk belirtimi için.
- **Kaynak dosyaları** -bir ağ paylaşımına veya yerel bir sabit sürücü üzerinde olup tooimport planladığınız hello dosyaları hello kopyalama makinesinden erişilebilir olmalıdır.

### <a name="repairing-a-partially-failed-import-job"></a>Kısmen başarısız alma işi onarma

- **Günlük Dosya Kopyala** Azure içeri/dışarı aktarma hizmeti depolama hesabı ve Disk arasında veri kopyalarken oluşturulur. Hedef depolama hesabınızdaki bulunur.

### <a name="repairing-a-partially-failed-export-job"></a>Kısmen başarısız dışarı aktarma işini onarma

- **Günlük Dosya Kopyala** Azure içeri/dışarı aktarma hizmeti depolama hesabı ve Disk arasında veri kopyalarken oluşturulur. Kaynak depolama hesabınızdaki bulunur.
- **Bildirim dosyası** -Microsoft tarafından döndürülen dışarı aktarılan sürücüde [isteğe bağlı] Located.

## <a name="download-and-install-waimportexport"></a>WAImportExport yükleyip

Merhaba karşıdan [WAImportExport.exe en son sürümünü](https://www.microsoft.com/download/details.aspx?id=55280). Bilgisayarınızda Hello sıkıştırılmış içerik tooa dizin ayıklayın.

Sonraki göreviniz toocreate CSV dosya sayısıdır.

## <a name="prepare-hello-dataset-csv-file"></a>Merhaba dataset CSV dosyasını hazırlama

### <a name="what-is-dataset-csv"></a>Veri kümesi CSV nedir

Veri kümesi CSV dosyası /dataset bayrağı hello değerine dizinlerin listesini ve/veya dosyaları kopyalanan toobe tootarget sürücülerin listesini içeren bir CSV dosyası numarasıdır. Merhaba ilk adım toocreating alma işi toodetermine hangi dizinleri olduğunu ve dosyaları tooimport geçiyor. Bu dizinlerin listesini, benzersiz dosyaların listesini veya bu iki bir birleşimi olabilir. Bir dizin dahil edildiğinde hello dizin ve alt dizinlerinde tüm dosyaları hello Alma işinin bir parçası olur.

Alınan her dizin veya dosya toobe için hedef sanal dizin veya hello Azure Blob hizmeti blob tanımlamanız gerekir. Bu hedeflerde girişleri toohello WAImportExport aracı olarak kullanır. Dizinleri Merhaba Öne eğik çizgi karakteriyle ayrılmış "/".

Aşağıdaki tablonun hello blob hedefler bazı örnekler gösterilmektedir:

| Kaynak dosya veya dizin | Hedef blob veya sanal dizin |
| --- | --- |
| H:\Video | https://mystorageaccount.BLOB.Core.Windows.NET/video |
| H:\Photo | https://mystorageaccount.BLOB.Core.Windows.NET/Photo |
| K:\Temp\FavoriteVideo.ISO | https://mystorageaccount.BLOB.Core.Windows.NET/favorite/FavoriteVideo.ISO |
| \\myshare\john\music | https://mystorageaccount.BLOB.Core.Windows.NET/Music |

### <a name="sample-datasetcsv"></a>Örnek dataset.csv

```
BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
"F:\50M_original\100M_1.csv.txt","containername/100M_1.csv.txt",BlockBlob,rename,"None",None
"F:\50M_original\","containername/",BlockBlob,rename,"None",None
```

### <a name="dataset-csv-file-fields"></a>Veri kümesi CSV dosyası alanları

| Alan | Açıklama |
| --- | --- |
| Ana yolu | **[Gerekli]**<br/>Bu parametrenin değerini Hello içeri hello veri toobe bulunduğu hello kaynağını temsil eder. Merhaba aracı bu yolu altında bulunan tüm veriler yinelemeli olarak kopyalama olur.<br><br/>**İzin verilen değerler**: Bu toobe yerel bilgisayardaki geçerli bir yol veya geçerli bir paylaşım yolu vardır ve hello kullanıcı tarafından erişilebilir olması gerekir. Merhaba dizin yolu mutlak bir yol (göreli bir yol değil) olması gerekir. Merhaba yolu ile bitiyorsa "\\", başka bir dizin olmadan bitiş yolu temsil eder"\\" bir dosyayı temsil eder.<br/>Hiçbir regex bu alana izin verilir. Merhaba yol boşluk içeriyorsa, içine "".<br><br/>**Örnek**: "c:\Directory\c\Directory\File.txt"<br>"\\\\FBaseFilesharePath.domain.net\sharename\directory\"  |
| DstBlobPathOrPrefix | **[Gerekli]**<br/> Merhaba yolu toohello hedef sanal dizin Windows Azure depolama hesabınızdaki. Merhaba sanal dizin olabilir veya zaten mevcut olmayabilir. Yoksa, içeri/dışarı aktarma hizmeti bir oluşturacak.<br/><br/>Emin toouse hedef sanal dizinleri ve blobları belirtirken geçerli kapsayıcı adları olabilir. Kapsayıcı adları küçük harfli olması gerektiğini unutmayın. Kapsayıcı adlandırma kuralları için bkz: [adlandırma ve başvuran kapsayıcıları, Blobları ve meta veri](/rest/api/storageservices/naming-and-referencing-containers--blobs--and-metadata). Yalnızca kök belirtilen hello kaynak hello dizin yapısını hello hedef blob kapsayıcısında çoğaltılır. Farklı dizin yapısını daha istenirse kaynak, CSV eşlemesindeki birden çok satır birinde hello<br/><br/>Bir kapsayıcı veya müzik/70s gibi bir blob öneki belirtebilirsiniz /. Merhaba hedef dizinin hello kapsayıcı adını, ardından bir eğik çizgi ile başlaması gerekir "/" ve isteğe bağlı olarak ile biten bir sanal blob dizin içerebilir "/".<br/><br/>Merhaba hedef kapsayıcı hello kök kapsayıcı olduğunda, hello kök kapsayıcı Merhaba Öne eğik çizgi, $root dahil olmak üzere, açıkça belirtmelisiniz /. BLOB'ları hello kök kapsayıcısı altında içeremez "/" Merhaba hedef dizinin hello kök kapsayıcı olduğunda adlarında, tüm dizinlerde hello kaynak dizin kopyalanmaz beri.<br/><br/>**Örnek**<br/>Merhaba hedef blob yolu https://mystorageaccount.blob.core.windows.net/video ise, bu alanın değeri hello video olabilir /  |
| BlobType | **[İsteğe bağlı]**  Blok &#124; sayfası<br/>Şu anda içeri/dışarı aktarma hizmeti BLOB'lar 2 türlerini destekler. Sayfa blobları ve blok BlobsBy varsayılan tüm dosyaları blok Blobları içeri aktarılacak. Ve \*.vhd ve \*sayfa BlobsThere hello blok-blob ve sayfa blob boyutu izin verilen üst sınırı olarak .vhdx alınır. Bkz: [depolama ölçeklenebilirlik hedefleri](storage-scalability-targets.md#scalability-targets-for-blobs-queues-tables-and-files) daha fazla bilgi için.  |
| Değerlendirme | **[İsteğe bağlı]**  yeniden adlandırmak &#124; Hayır üzerine &#124; üzerine yaz <br/> Bu alan hello kopyalama-davranışını alma yani sırasında belirtir. Veri yükleniyor zaman hello disk toohello depolama hesabından karşıya. Kullanılabilir seçenekler şunlardır: yeniden adlandırma &#124; üzerine yazılsın mı &#124; Hayır üzerine. Varsayılanları çok "hiçbir şey, belirtilen rename". <br/><br/>**Yeniden Adlandır**: aynı ada sahip bir nesne varsa, hedef bir kopyasını oluşturur.<br/>Üzerine yaz: yeni dosyasıyla hello dosyasının üzerine yazar. son değiştirilen WINS dosyasıyla Hello.<br/>**Hayır üzerine**: hello yazma atlar dosya zaten varsa.|
| MetadataFile | **[İsteğe bağlı]** <br/>Merhaba değer toothis alanı hello bir hello nesnelerin toopreserve hello meta verileri gerekiyorsa sağlanan veya özel meta verilerini sağlamak hello meta veri dosyasıdır. Merhaba hedef BLOB'ları için yol toohello meta veri dosyası. Bkz: [içeri/dışarı aktarma hizmeti meta verileri ve özellikleri dosya biçimi](storage-import-export-file-format-metadata-and-properties.md) daha fazla bilgi için |
| PropertiesFile | **[İsteğe bağlı]** <br/>Merhaba hedef BLOB'ları için yol toohello özelliği dosya. Bkz: [içeri/dışarı aktarma hizmeti meta verileri ve özellikleri dosya biçimi](storage-import-export-file-format-metadata-and-properties.md) daha fazla bilgi için. |

## <a name="prepare-initialdriveset-or-additionaldriveset-csv-file"></a>InitialDriveSet veya AdditionalDriveSet CSV dosyasını hazırlama

### <a name="what-is-driveset-csv"></a>Driveset CSV nedir

Merhaba hello /InitialDriveSet veya /AdditionalDriveSet bayrağı hello hello aracı doğru hazır diskler toobe hello listesi seçebilirsiniz böylece toowhich hello sürücü harflerini eşlenmiş disklerin listesini içeren bir CSV dosyası değeridir. Merhaba veri boyutu tek disk boyutundan daha büyükse hello WAImportExport aracı bu CSV dosyasında en iyi duruma getirilmiş bir şekilde kayıtlı birden çok disklere hello veri dağıtır.

Yoktur diskleri hello veri hello sayısına bir sınır yoktur tek oturumu tooin yazılabilir. Merhaba aracı disk boyutu ve klasör boyutunu temel alan veri dağıtır. Çoğu hello disk seçer hello nesne-boyutu için en iyi duruma getirilmiş. Merhaba karşıya olduğunda veri toohello depolama hesabı, veri kümesi dosyasında belirtilen yakınsanmış geri toohello dizin yapısını olacaktır. Sipariş toocreate driveset CSV, hello adımları izleyin.

### <a name="create-basic-volume-and-assign-drive-letter"></a>Temel birim oluşturun ve sürücü harfi atama

Temel birim toocreate sipariş ve "daha basit bölüm oluşturma sırasında verilen" Merhaba yönergeleri izleyerek bir sürücü harfi atamak [Disk Yönetimi'ne genel bakış](https://technet.microsoft.com/library/cc754936.aspx).

### <a name="sample-initialdriveset-and-additionaldriveset-csv-file"></a>Örnek InitialDriveSet ve AdditionalDriveSet CSV dosyası

```
DriveLetter,FormatOption,SilentOrPromptOnFormat,Encryption,ExistingBitLockerKey
G,AlreadyFormatted,SilentMode,AlreadyEncrypted,060456-014509-132033-080300-252615-584177-672089-411631
H,Format,SilentMode,Encrypt,
```

### <a name="driveset-csv-file-fields"></a>Driveset CSV dosyası alanları

| Alanları | Değer |
| --- | --- |
| SürücüHarfi | **[Gerekli]**<br/> Basit bir NTFS birimi üzerinde sahip toohello aracı hello hedef olarak sağlanan her sürücü gerekir ve bir sürücü harfi tooit atanır.<br/> <br/>**Örnek**: R veya r |
| FormatOption | **[Gerekli]**  Biçimi &#124; AlreadyFormatted<br/><br/> **Biçim**: Bu belirtme hello diskteki tüm hello veriler biçimlendirecek. <br/>**AlreadyFormatted**: hello aracı, bu değeri belirtildiğinde biçimlendirme atlar. |
| SilentOrPromptOnFormat | **[Gerekli]**  SilentMode &#124; PromptOnFormat<br/><br/>**SilentMode**: Bu değer sağlayan kullanıcı toorun hello Aracı sessiz modda etkinleştirir. <br/>**PromptOnFormat**: hello eylem gerçekten her biçiminde istenip istenmediğini hello aracı hello kullanıcı tooconfirm sorar.<br/><br/>Ayarlanmadı, komut iptal etmek ve hata iletisini görüntüler: "SilentOrPromptOnFormat için geçersiz değer: yok" |
| Şifreleme | **[Gerekli]**  Şifrelemek &#124; AlreadyEncrypted<br/> Bu alanın Hello değeri, hangi disk tooencrypt ve hangi değil karar verir. <br/><br/>**Şifreleme**: aracı hello sürücüsünü Biçimlendir. "FormatOption" alanının değerini "Biçim" ise, bu değer gerekli toobe "Şifrele" olur. "AlreadyEncrypted" Bu durumda belirtilirse, "Biçimi belirtildiğinde şifrele de belirtilmesi gerekir" bir hatayla sonuçlanır.<br/>**AlreadyEncrypted**: aracı hello "ExistingBitLockerKey" alanında sağlanan BitLockerKey kullanarak hello sürücü şifresini. "FormatOption" alanının değerini "AlreadyFormatted" ise, ardından bu değer, "Şifrele" veya "AlreadyEncrypted" olabilir |
| ExistingBitLockerKey | **[Gerekli]**  "Şifreleme" alanının değerini "AlreadyEncrypted" ise<br/> Bu alanın değeri Hello hello belirli diskle ilişkili hello BitLocker anahtardır. <br/><br/>Bu alan, "Şifrele" hello "Şifreleme" alanının değerini ise, boş bırakılmalıdır.  BitLocker anahtar bu durumda belirtilirse, "Bitlocker anahtarını belirtilmemesi gerekir" bir hatayla sonuçlanır.<br/>  **Örnek**: 060456-014509-132033-080300-252615-584177-672089-411631|

##  <a name="preparing-disk-for-import-job"></a>Disk için içeri aktarma işi hazırlama

tooprepare sürücüler içeri aktarma işi için çağrı hello WAImportExport hello aracıyla **PrepImport** komutu. Eklediğiniz hangi parametreleri bağlıdır olup bu olduğu hello üzerinde ilk kopya oturumu veya bir sonraki kopya oturumu.

### <a name="first-session"></a>İlk oturumun

İlk kopya oturumu tooCopy bir Single/Multiple Directory tooa tek/birden çok Disk (bağlı olarak hangi CSV dosyasında belirtilir) WAImportExport Aracı'nı PrepImport komutu hello için oturumu toocopy dizinler ve/veya yeni bir kopya oturum dosyalarıyla ilk kopyalayın:

```
WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> [/logdir:<LogDirectory>] [/sk:<StorageAccountKey>] [/silentmode] [/InitialDriveSet:<driveset.csv>] DataSet:<dataset.csv>
```

**Örnek:**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#1  /sk:\*\*\*\*\*\*\*\*\*\*\*\*\* /InitialDriveSet:driveset-1.csv /DataSet:dataset-1.csv /logdir:F:\logs
```

### <a name="add-data-in-subsequent-session"></a>Sonraki oturumunda veri ekleme

Sonraki kopyalama oturumlarında toospecify hello başlangıç parametreleri gerekmez. Toouse ihtiyacınız hello kaldığı hello önceki oturum aynı günlük dosyası hello aracı tooremember. Merhaba kopya oturumu Hello durumunu toohello günlük dosyası yazılır. Sonraki bir kopya hello sözdizimi şöyledir oturum toocopy ek dizinler ve/veya dosyaları:

```
WAImportExport.exe PrepImport /j:<SameJournalFile> /id:<DifferentSessionId>  [DataSet:<differentdataset.csv>]
```

**Örnek:**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2  /DataSet:dataset-2.csv
```

### <a name="add-drives-toolatest-session"></a>Sürücüleri toolatest oturumu ekleme

Merhaba veri InitialDriveset belirtilen sürücüleri sığmadı bir hello aracı tooadd ek sürücüler toosame kopya oturumu kullanabilirsiniz. 

>[!NOTE] 
>Merhaba oturum kimliği hello önceki oturum kimliği ile eşleşmesi gerekir. Günlük dosyası, bir önceki oturumunda belirtilen hello eşleşmesi gerekir.
>
```
WAImportExport.exe PrepImport /j:<SameJournalFile> /id:<SameSessionId> /AdditionalDriveSet:<newdriveset.csv>
```

**Örnek:**

```
WAImportExport.exe PrepImport /j:SameJournalTest.jrn /id:session#2  /AdditionalDriveSet:driveset-2.csv
```

### <a name="abort-hello-latest-session"></a>Merhaba, son oturum iptal:

Kopya oturumu kesintiye ve (örneğin, bir kaynak dizin erişilemez oluyor uygulamasına yol açıyordu), olası tooresume değilse, böylece geri alınması hello geçerli oturum iptal gerekir ve yeni kopya oturumları geri başlatılabilir:

```
WAImportExport.exe PrepImport /j:<SameJournalFile> /id:<SameSessionId> /AbortSession
```

**Örnek:**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2  /AbortSession
```

Yalnızca hello son kopya oturumu, anormal olursa iptal. Bir sürücü için ilk kopyalama oturumu hello iptal edilemiyor unutmayın. Bunun yerine yeni bir günlük dosyasıyla hello kopyalama oturumlarını yeniden başlatmalısınız.

### <a name="resume-a-latest-interrupted-session"></a>Bir son kesintiye uğramış oturum sürdürme

Herhangi bir nedenle bir kopya oturumu kesintiye uğrarsa, belirtilen yalnızca hello günlük dosyasıyla hello aracını çalıştırarak devam edebilirsiniz:

```
WAImportExport.exe PrepImport /j:<SameJournalFile> /id:<SameSessionId> /ResumeSession
```

**Örnek:**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2 /ResumeSession
```

> [!IMPORTANT] 
> Kopya oturumu sürdürdüğünüzde hello kaynak veri dosyaları ve dizinleri ekleyerek veya kaldırarak dosyaları değiştirmeyin.

## <a name="waimportexport-parameters"></a>WAImportExport parametreleri

| Parametreler | Açıklama |
| --- | --- |
|     /j:&lt;JournalFile&gt;  | **Gerekli**<br/> Yol toohello günlük dosyası. Bir günlük dosyası sürücüleri kümesini izler ve bu sürücüler hazırlama sürüyor kayıtları hello. Merhaba günlük dosyası her zaman belirtilmesi gerekir.  |
|     / LOGDIR:&lt;LogDirectory&gt;  | **İsteğe bağlı**. Merhaba günlük dosyası dizini.<br/> Ayrıntılı günlük dosyaları gibi bazı geçici dosyaları toothis dizin yazılır. Aksi durumda belirtilmezse, geçerli dizin hello günlük dizini kullanılır. Merhaba günlük dizini yalnızca bir kez Merhaba belirtilebilir aynı günlük dosyası.  |
|     /ID:&lt;SessionID&gt;  | **Gerekli**<br/> hello oturumu kopyalama oturumu kullanılan tooidentify kimliğidir. Bu, kullanılan tooensure doğru kurtarma kesintiye uğramış kopyalama oturumu olur.  |
|     / ResumeSession  | İsteğe bağlı. Merhaba son kopya oturumu aşırı sonlandırıldı, bu parametre belirtilen tooresume hello oturum olabilir.   |
|     / AbortSession  | İsteğe bağlı. Merhaba son kopya oturumu aşırı sonlandırıldı, bu parametre belirtilen tooabort hello oturum olabilir.  |
|     /sn:&lt;StorageAccountName&gt;  | **Gerekli**<br/> Yalnızca, RepairImport ve RepairExport için de geçerlidir. Merhaba hello depolama hesabının adıdır.  |
|     /SK:&lt;StorageAccountKey&gt;  | **Gerekli**<br/> Merhaba depolama hesabı anahtarı Hello. |
|     / InitialDriveSet:&lt;driveset.csv&gt;  | **Gerekli** ilk kopya oturumu hello çalışırken<br/> Sürücüleri tooprepare listesini içeren bir CSV dosyası.  |
|     / AdditionalDriveSet:&lt;driveset.csv&gt; | **Gerekli**. Sürücüleri toocurrent kopya oturumu eklerken. <br/> Eklenen ek sürücüler toobe listesini içeren bir CSV dosyası.  |
|      / r:&lt;RepairFile&gt; | **Gerekli** yalnızca RepairImport ve RepairExport için geçerlidir.<br/> Onarım ilerleme durumunu izlemek için toohello dosya yolu. Her bir sürücü bir ve yalnızca bir onarım dosyası olması gerekir.  |
|     / d:&lt;TargetDirectories&gt; | **Gerekli**. Yalnızca, RepairImport ve RepairExport için de geçerlidir. RepairImport için bir veya daha çok noktalı virgülle ayrılmış dizinleri toorepair; Bir dizin toorepair RepairExport için örneğin dizin hello sürücüsünün kök.  |
|     / CopyLogFile:&lt;DriveCopyLogFile&gt; | **Gerekli** yalnızca RepairImport ve RepairExport için geçerlidir. Yol toohello sürücü kopyalama günlük dosyası (ayrıntılı veya hata).  |
|     / Manıfestfıle:&lt;DriveManifestFile&gt; | **Gerekli** RepairExport yalnızca uygulanabilir.<br/> Yol toohello sürücü bildirim dosyası.  |
|     / PathMapFile:&lt;DrivePathMapFile&gt; | **İsteğe bağlı**. Yalnızca RepairImport için geçerlidir.<br/> Dosya yolu göreli toohello sürücü kök toolocations (sekmeyle sınırlı) gerçek dosya eşlemelerini içeren yolu toohello dosyası. İlk belirtildiğinde, bu dosya yolları boş hedefler ile TargetDirectories, erişim reddedildi, geçersiz bir ada içinde bulunmayan ya da birden fazla dizinde mevcut yani doldurulur. Merhaba yol haritası yeniden hello aracı tooresolve hello dosya yolları için doğru belirtildiğinden ve el ile düzenlenmiş tooinclude hello doğru hedef yollarını olabilir.  |
|     / ExportBlobListFile:&lt;ExportBlobListFile&gt; | **Gerekli**. Yalnızca PreviewExport için geçerlidir.<br/> Yol toohello XML içeren blob yollar listesi dosya veya yol önekleri dışarı hello BLOB'lar toobe için blob. Merhaba dosya biçimi olan hello aynı hello blob listesi blob hello hello içeri/dışarı aktarma hizmeti REST API'si iş Put işlemini biçiminde olarak.  |
|     / DriveSize:&lt;DriveSize&gt; | **Gerekli**. Yalnızca PreviewExport için geçerlidir.<br/>  Dışarı aktarma için kullanılan sürücü toobe boyutu. Örneğin, 500 GB 1,5 TB. Not: 1 GB = 1.000.000.000 bytes1 TB = 1,000,000,000,000 bayt  |
|     / DataSet:&lt;dataset.csv&gt; | **Gerekli**<br/> Dizinlerin listesini ve/veya dosyaları toobe listesini içeren bir CSV dosyası tootarget sürücüleri kopyalanır.  |
|     /silentmode  | **İsteğe bağlı**.<br/> Belirtilmezse, sürücüler gereksinimi hello ve onay toocontinue gereksinim anımsatır.  |

## <a name="tool-output"></a>Araç çıktısı

### <a name="sample-drive-manifest-file"></a>Örnek sürücü bildirim dosyası

```xml
<?xml version="1.0" encoding="UTF-8"?>
<DriveManifest Version="2011-MM-DD">
   <Drive>
      <DriveId>drive-id</DriveId>
      <StorageAccountKey>storage-account-key</StorageAccountKey>
      <ClientCreator>client-creator</ClientCreator>
      <!-- First Blob List -->
      <BlobList Id="session#1-0">
         <!-- Global properties and metadata that applies tooall blobs -->
         <MetadataPath Hash="md5-hash">global-metadata-file-path</MetadataPath>
         <PropertiesPath Hash="md5-hash">global-properties-file-path</PropertiesPath>
         <!-- First Blob -->
         <Blob>
            <BlobPath>blob-path-relative-to-account</BlobPath>
            <FilePath>file-path-relative-to-transfer-disk</FilePath>
            <ClientData>client-data</ClientData>
            <Length>content-length</Length>
            <ImportDisposition>import-disposition</ImportDisposition>
            <!-- page-range-list-or-block-list -->
            <!-- page-range-list -->
            <PageRangeList>
               <PageRange Offset="1073741824" Length="512" Hash="md5-hash" />
               <PageRange Offset="1073741824" Length="512" Hash="md5-hash" />
            </PageRangeList>
            <!-- block-list -->
            <BlockList>
               <Block Offset="1073741824" Length="4194304" Id="block-id" Hash="md5-hash" />
               <Block Offset="1073741824" Length="4194304" Id="block-id" Hash="md5-hash" />
            </BlockList>
            <MetadataPath Hash="md5-hash">metadata-file-path</MetadataPath>
            <PropertiesPath Hash="md5-hash">properties-file-path</PropertiesPath>
         </Blob>
      </BlobList>
   </Drive>
</DriveManifest>
```

### <a name="sample-journal-file-xml-for-each-drive"></a>Her sürücü için örnek günlük dosyası (XML)

```xml
[BeginUpdateRecord][2016/11/01 21:22:25.379][Type:ActivityRecord]
ActivityId: DriveInfo
DriveState: [BeginValue]
<?xml version="1.0" encoding="UTF-8"?>
<Drive>
   <DriveId>drive-id</DriveId>
   <BitLockerKey>*******</BitLockerKey>
   <ManifestFile>\DriveManifest.xml</ManifestFile>
   <ManifestHash>D863FE44F861AE0DA4DCEAEEFFCCCE68</ManifestHash> </Drive>
[EndValue]
SaveCommandOutput: Completed
[EndUpdateRecord]
```

### <a name="sample-journal-file-jrn-for-session-that-records-hello-trail-of-sessions"></a>Oturumları hello izi kayıtları oturumu için örnek günlük dosyası (JRN)

```
[BeginUpdateRecord][2016/11/02 18:24:14.735][Type:NewJournalFile]
VocabularyVersion: 2013-02-01
[EndUpdateRecord]
[BeginUpdateRecord][2016/11/02 18:24:14.749][Type:ActivityRecord]
ActivityId: PrepImportDriveCommandContext
LogDirectory: F:\logs
[EndUpdateRecord]
[BeginUpdateRecord][2016/11/02 18:24:14.754][Type:ActivityRecord]
ActivityId: PrepImportDriveCommandContext
StorageAccountKey: *******
[EndUpdateRecord]
```

## <a name="faq"></a>SSS

### <a name="general"></a>Genel

#### <a name="what-is-waimportexport-tool"></a>WAImportExport Aracı nedir?

Merhaba WAImportExport hello sürücü hazırlama ve Microsoft Azure içeri/dışarı aktarma hizmeti hello ile kullanabileceğiniz Onarım Aracı aracıdır. Tooship tooan Azure veri merkezine giderek bu aracı toocopy veri toohello sabit sürücüleri kullanabilirsiniz. İçe aktarma işi tamamlandıktan sonra bu aracı toorepair bozuldu, eksik olan veya çakışan BLOB diğer BLOB'lar ile kullanabilirsiniz. Tamamlanan dışa aktarma işleminden hello sürücüleri aldıktan sonra bu aracı toorepair bozuldu herhangi bir dosya ya da hello sürücülerde eksik kullanabilirsiniz.

#### <a name="how-does-hello-waimportexport-tool-work-on-multiple-source-dir-and-disks"></a>Nasıl mu hello WAImportExport aracı birden çok kaynak dizini ve diskleri çalışır?

Hello veri boyutu hello disk boyutundan daha büyükse hello WAImportExport aracı hello disklerde hello veri iyileştirilmiş bir şekilde dağıtın. diskleri Hello veri kopyalama toomultiple paralel veya sıralı olarak yapılabilir. Var olan diskleri hello veri hello sayısına bir sınır yoktur toosimultaneously yazılabilir. Merhaba aracı disk boyutu ve klasör boyutunu temel alan veri dağıtır. Çoğu hello disk seçer hello nesne-boyutu için en iyi duruma getirilmiş. Merhaba karşıya olduğunda veri toohello depolama hesabı Yakınsanan geri toohello belirtilen dizin yapısı.

#### <a name="where-can-i-find-previous-version-of-waimportexport-tool"></a>WAImportExport aracının önceki sürümünü nereden bulabilirim?

WAImportExport aracı WAImportExport V1 aracı olan tüm işlevler içerir. WAImportExport aracı birden çok kaynakları ve yazma toomultiple sürücüleri kullanıcılar toospecify sağlar. Ayrıca, bir içinden hello verilerin tek bir CSV dosyasında kopyalanan toobe gereken birden çok kaynak konumlarını kolayca yönetebilirsiniz. Ancak, SAS gerekir durumda desteklemiyor veya toocopy tek kaynak toosingle disk, size [yükleyebilir WAImportExport V1 aracı] istediğiniz (http://go.microsoft.com/fwlink/? LinkId 301900 =&amp;clcid = 0x409) ve çok başvuruda[WAImportExport V1 başvuru](storage-import-export-tool-how-to-v1.md) WAImportExport V1 kullanımı ile ilgili Yardım.

#### <a name="what-is-a-session-id"></a>Bir oturum kimliği nedir?

Merhaba aracı hello kopya oturumu bekliyor (/ kimliği) parametre toobe Merhaba, aynı, birden çok diskte hello hedefi toospread hello veri varsa. Koruma, hello aynı hello kopya oturumu adını kullanıcı toocopy verileri bir veya birden çok hedef diskleri/dizinler içine bir veya birden çok kaynak konumlarını etkinleştirir. Aynı oturum kimliği koruma hello aracı toopick hello son zamanı kaldığı dosyaları hello kopyasını sağlar.

Ancak, aynı kopya oturumu kullanılan tooimport veri toodifferent depolama hesapları olamaz.

Kopya oturumu adı hello aracı birden çok çalıştırmaları arasında aynı olduğunda, günlük dosyası hello (/ logdir) ve depolama hesabı anahtarı (/ sk) olan de beklenen toobe hello aynı.

SessionID harfler, 0 oluşabilir ~ 9, understore (\_), tire (-) ya da karma (#), ve uzunluğu 3 olmalıdır ~ 30.

Örneğin oturum-1 veya oturum #1 veya oturum\_1

#### <a name="what-is-a-journal-file"></a>Bir günlük dosyası nedir?

Merhaba WAImportExport aracı toocopy dosyaları toohello sabit sürücü, her çalıştırdığınızda hello aracı kopya oturumu oluşturur. Merhaba kopya oturumu Hello durumunu toohello günlük dosyası yazılır. (Örneğin, tooa sistem güç kaybı) bir kopyası oturumu kesintiye uğrarsa hello Aracı'nı yeniden çalıştırmayı ve hello günlük dosyası hello komut satırında belirterek ettirilebilir.

Azure içeri/dışarı aktarma aracı hello ile hazırlama her sabit sürücü için hello aracı adla tek bir günlük dosyası oluşturur "&lt;DriveID&gt;.xml" aracı hello toohello sürücü sürücü kimliği hello seri numarası ilişkili olduğu okur Merhaba disk. Tüm sürücüleri toocreate hello Alma işinizin hello günlük dosyaları gerekir. Merhaba aracı kesintiye uğrarsa hello günlük dosyası da kullanılan tooresume sürücü hazırlama olabilir.

#### <a name="what-is-a-log-directory"></a>Bir günlük dizini nedir?

bir dizin toobe toostore ayrıntılı günlükleri ve bunun yanı sıra geçici bildirim dosyalarını kullanılan Hello günlük dizini belirtir. Belirtilmezse, geçerli dizin hello hello günlük dizini kullanılır. Merhaba, ayrıntılı günlükleri günlüklerin.

### <a name="prerequisites"></a>Ön koşullar

#### <a name="what-are-hello-specifications-of-my-disk"></a>My disk hello belirtimlerini nelerdir?

Bir veya daha fazla boş 2,5 inç veya 3,5 inç SATAII veya III veya SSD sabit bağlı toohello kopyalama makine sürücüleri.

#### <a name="how-can-i-enable-bitlocker-on-my-machine"></a>My makinede BitLocker nasıl etkinleştirebilirim?

Basit bir yol toocheck sistem sürücüsünde sağ tıklayarak ' dir. Merhaba özelliği açıksa, Bitlocker seçeneklerini gösterir. Kapalı ise, görmezsiniz.

![BitLocker'ı denetleyin](./media/storage-import-export-tool-preparing-hard-drives-import/BitLocker.png)

Üzerinde bir makale işte [nasıl tooenable BitLocker](https://technet.microsoft.com/library/cc766295.aspx)

Bu, makinenize TPM yongası yok mümkündür. Tpm.msc kullanarak bir çıktı alamazsanız hello sonraki SSS arayın.

#### <a name="how-toodisable-trusted-platform-module-tpm-in-bitlocker"></a>Nasıl toodisable BitLocker Güvenilen Platform Modülü (TPM)?
> [!NOTE]
> Yalnızca varsa hiçbir TPM kendi sunucuları, toodisable TPM İlkesi gerekir. Kullanıcının Server'da güvenilir bir TPM varsa gerekli toodisable TPM değil. 
> 

Sipariş toodisable BitLocker TPM'DE'da, aşağıdaki adımları hello gidin:<br/>
1. Başlatma **Grup İlkesi Düzenleyicisi'ni** bir komut istemi gpedit.msc yazarak. Varsa **Grup İlkesi Düzenleyicisi'ni** toobe kullanılamıyor, BitLocker'ı etkinleştirmek için önce görüntülenir. Önceki SSS bakın.
2. Açık **yerel bilgisayar ilkesi &gt; Bilgisayar Yapılandırması &gt; Yönetim Şablonları &gt; Windows bileşenleri&gt; BitLocker Sürücü Şifrelemesi &gt; işletim sistemi sürücüleri**.
3. Düzen **başlangıçta ek kimlik doğrulamasını gerektiren** ilkesi.
4. Hello İlkesi çok ayarlamak**etkin** ve emin olun **izin olmadan BitLocker'ı uyumlu bir TPM** denetlenir.

####  <a name="how-toocheck-if-net-4-or-higher-version-is-installed-on-my-machine"></a>Nasıl my makinede .NET 4 veya daha yüksek bir sürümü yüklüyse toocheck?

Tüm Microsoft .NET Framework sürümleri şu dizine yüklenir: %windir%\Microsoft.NET\Framework\

Yukarıda sözü edilen bölümü burada hello aracı toorun gereken hedef makinedeki toohello gidin. Klasör adı "v4" ile başlayan arayın. Böyle bir dizin olmaması anlamına gelir, makinenizde .NET 4 yüklü değil. .Net 4, makine kullanarak indirebilirsiniz [Microsoft .NET Framework 4 (Web Yükleyicisi)](https://www.microsoft.com/download/details.aspx?id=17851).

### <a name="limits"></a>Sınırlar

#### <a name="how-many-drives-can-i-preparesend-at-hello-same-time"></a>Kaç tane sürücüleri ı hazırlama/hello gönderme aynı anda?

Yoktur hello aracı hello disk sayısını bir sınırlama yoktur hazırlayın. Ancak, hello aracı sürücü harflerini girdi olarak bekliyor. Bu too25 eşzamanlı disk hazırlık sınırlar. Tek bir işi aynı anda en fazla 10 diskleri işleyebilir. 10'dan fazla diskleri hazırlıyorsanız hedefleme Merhaba aynı depolama hesabı, hello diskler arasında birden çok iş dağıtılabilir.

#### <a name="can-i-target-more-than-one-storage-account"></a>Birden fazla depolama hesabı hedefleyebilir miyim?

Yalnızca bir depolama hesabı, iş başına ve tek bir kopya oturumunda gönderilebilir.

### <a name="capabilities"></a>Özellikler

#### <a name="does-waimportexportexe-encrypt-my-data"></a>WAImportExport.exe verilerimi şifreleyebilir mi?

Evet. BitLocker şifrelemesi etkin ve bu işlemi için gereklidir.

#### <a name="what-will-be-hello-hierarchy-of-my-data-when-it-appears-in-hello-storage-account"></a>Merhaba depolama hesabında görüntülendiğinde ne verilerimi hello hiyerarşisini olacak?

Veri disklerde dağıtılmış rağmen karşıya verilerinin hello toohello depolama hesabı Yakınsanan geri hello dataset CSV dosyasında belirtilen toohello dizin yapısı.

#### <a name="how-many-of-hello-input-disks-will-have-active-io-in-parallel-when-copy-is-in-progress"></a>Merhaba kaç kopyalama devam ederken diskleri paralel olarak etkin GÇ sahip giriş?

Merhaba aracı veri hello hello girdi dosyalarının boyutuna göre hello giriş diskler arasında dağıtır. Bu, etkin diskleri paralel hello sayısı tamamen hello giriş verisi hello yapısını delends belirtti. Hello girdi veri kümesi içinde tek tek dosyaların Hello boyutuna bağlı olarak, bir veya daha fazla diski etkin GÇ paralel olarak gösterebilir. Daha fazla ayrıntı için sonraki soruya bakın.

#### <a name="how-does-hello-tool-distribute-hello-files-across-hello-disks"></a>Nasıl hello aracı hello dosyaları dağıtmak ve bu da hello disklerde?

WAImportExport aracı okur ve tek bir toplu 100000 dosyaların maksimum içeren dosyaları toplu toplu yazar. Bu paralel max 100000 dosyalar yazılabilir anlamına gelir. Birden çok disk toomulti sürücüleri 100000 bu dosyalar toosimultaneously dağıtılmış yazılır. Ancak olup hello aracı toomultiple diskleri aynı anda yazar veya tek bir disk hello toplu hello toplu boyutuna bağlıdır. 10,0000 dosyaların tümünü tek bir sürücüye mümkün toofit varsa örneği için daha küçük dosyalar halinde aracı tooonly bir disk hello bu toplu iş işlenirken yazacaksınız.

### <a name="waimportexport-output"></a>WAImportExport çıkış

#### <a name="there-are-two-journal-files-which-one-should-i-upload-tooazure-portal"></a>Hangisinin gereken iki günlük dosyası tooAzure portal karşıya?

**.xml** -hello WAImportExport aracıyla hazırlama her sabit sürücü için hello aracı adla bir tek günlük dosyası oluşturulur `<DriveID>.xml` DriveID hello seri numarası ilişkili olduğu aracı hello toohello sürücü hello diskten okur. Tüm sürücüleri toocreate hello Alma işinin hello Azure portal'ın hello günlük dosyaları gerekir. Bu günlük dosyası kullanılan tooresume sürücü hazırlama Hello kesilene de olabilir.

**.jrn** -hello günlük dosyası sonekiyle `.jrn` bir sabit sürücü için tüm kopyalama oturumlarını hello durumunu içerir. Toocreate hello iş alma hello bilgileri de içerir. Çalışan hello WAImportExport aracı gibi bir kopya oturum kimliği her zaman bir günlük dosyası belirtmeniz gerekir

## <a name="next-steps"></a>Sonraki adımlar

* [Kurulum hello Azure içeri/dışarı aktarma aracı](storage-import-export-tool-setup.md)
* [Özellikleri ayarlama ve hello sırasında meta veri alma işlemi](storage-import-export-tool-setting-properties-metadata-import.md)
* [Örnek iş akışı tooprepare sabit sürücüler içeri aktarma işi için](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow.md)
* [Sık kullanılan komutlar için hızlı başvuru](storage-import-export-tool-quick-reference.md) 
* [Kopyalama günlük dosyalarıyla iş durumunu gözden geçirme](storage-import-export-tool-reviewing-job-status-v1.md)
* [Bir içeri aktarma işini onarma](storage-import-export-tool-repairing-an-import-job-v1.md)
* [Bir dışarı aktarma işini onarma](storage-import-export-tool-repairing-an-export-job-v1.md)
* [Sorun giderme hello Azure içeri/dışarı aktarma aracı](storage-import-export-tool-troubleshooting-v1.md)
