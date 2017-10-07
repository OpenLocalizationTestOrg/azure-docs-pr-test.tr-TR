---
title: "aaaPreparing sabit sürücüler için bir Azure içeri/dışarı aktarma alma işi - v1 | Microsoft Docs"
description: "Nasıl tooprepare sabit sürücüleri kullanarak WAImportExport v1 aracı toocreate hello Azure içeri/dışarı aktarma hizmeti için bir alma işi hello öğrenin."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 3d818245-8b1b-4435-a41f-8e5ec1f194b2
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: 1eb0c3c51e984e2869b5268254f468d4b43e9d85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="preparing-hard-drives-for-an-import-job"></a>Sabit sürücüleri içeri aktarma işine hazırlama
tooprepare bir veya daha fazla sabit sürücüler içeri aktarma işi için şu adımları izleyin:

-   Blob hizmeti hello Hello veri tooimport tanımlayın

-   Hedef sanal dizinleri ve blobları hello Blob hizmeti tanımlayın

-   Kaç tane sürücüler, gerekir belirleme

-   Merhaba veri tooeach sürücünüzde kopyalayın

 Örnek iş akışı için bkz: [örnek iş akışı tooPrepare sabit sürücüler içeri aktarma işi için](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow-v1.md).

## <a name="identify-hello-data-toobe-imported"></a>İçeri aktarılan hello veri toobe tanımlayın
 Merhaba ilk adım toocreating alma işi toodetermine hangi dizinleri olduğunu ve dosyaları tooimport geçiyor. Bu dizinlerin listesini, benzersiz dosyaların listesini veya bu iki bir birleşimi olabilir. Bir dizin dahil edildiğinde hello dizin ve alt dizinlerinde tüm dosyaları hello Alma işinin bir parçası olur.

> [!NOTE]
>  Bir üst dizine dahil edildiğinde alt dizinleri birlikte yinelemeli olarak olduğundan, yalnızca hello üst dizini belirtin. Ayrıca dizinlerinden hiçbirini belirtmeyin.
>
>  Şu anda hello Microsoft Azure içeri/dışarı aktarma aracı sınırlaması aşağıdaki hello vardır: bir dizin bir sabit sürücü içeren daha fazla veri içeriyorsa, daha küçük dizinlere bozuk toobe hello dizin gerekiyor. Örneğin, bir dizin 2,5 TB içeriyorsa veri ve hello sabit diskin kapasitesini yalnızca 2 TB'tır sonra küçük dizinlere toobreak hello 2,5 TB dizin gerekir. Bu sınırlama hello aracının daha sonraki bir sürümde ele alınacaktır.

## <a name="identify-hello-destination-locations-in-hello-blob-service"></a>Merhaba blob hizmetinde Hello hedef konumları tanımlayın
 Her dizin veya içeri aktarılacak dosya için tooidentify hedef sanal dizini veya blob hello Azure Blob hizmeti de gerekir. Bu hedeflerde girişleri toohello Azure içeri/dışarı aktarma aracı kullanır. Dizinleri Merhaba Öne eğik çizgi karakteri ile sınırlı olduğunu unutmayın "/".

 Aşağıdaki tablonun hello blob hedefler bazı örnekler gösterilmektedir:

|Kaynak dosya veya dizin|Hedef blob veya sanal dizin|
|------------------------------|-------------------------------------------|
|H:\Video|https://mystorageaccount.BLOB.Core.Windows.NET/video|
|H:\Photo|https://mystorageaccount.BLOB.Core.Windows.NET/Photo|
|K:\Temp\FavoriteVideo.ISO|https://mystorageaccount.BLOB.Core.Windows.NET/favorite/FavoriteVideo.ISO|
|\\\myshare\john\music|https://mystorageaccount.BLOB.Core.Windows.NET/Music|

## <a name="determine-how-many-drives-are-needed"></a>Kaç tane sürücüler gerekli belirleme
 Ardından, toodetermine gerekir:

-   sabit sürücü sayısı Hello toostore hello veri gerekli.

-   Merhaba dizinler ve/veya sabit, kopyalanan tooeach olacaktır bağımsız dosyalar.

 Merhaba toostore hello veri aktarımını gerekir sabit sürücü sayısı olduğundan emin olun.

## <a name="copy-data-tooyour-hard-drive"></a>Veri tooyour sabit diske kopyalama
 Bu bölümde, nasıl toocall hello Azure içeri/dışarı aktarma aracı toocopy veri tooone ya da daha fazla sabit disk sürücüler açıklanmaktadır. Hello Azure içeri/dışarı aktarma aracı çağrısı, her bir yeni oluşturduğunuz *kopyalama oturum*. En az bir kopya oturumu oluşturmak için her sürücü toowhich veri; kopyalama Bazı durumlarda, birden fazla kopya oturum toocopy gerekebilir tüm veri toosingle sürücünüzün. Birden çok kopya oturumu gerekebilir bazı nedenler şunlardır:

-   Kopyaladığınız her sürücü için ayrı kopya oturumu oluşturmanız gerekir.

-   Kopya oturumu tek bir dizin ya da bir tek blob toohello sürücü kopyalayabilirsiniz. Birden çok dizin, birden çok BLOB veya her ikisinin birleşimini kopyalıyorsanız birden çok kopya oturumu toocreate gerekir.

-   Özellikler ve alma işinin bir parçası olarak alınan hello BLOB'ları üzerinde ayarlanacak meta veriler belirtebilirsiniz. Hello özellikleri ya da kopyalama oturum açmak için belirttiğiniz meta verileri bu kopya oturumu tarafından belirtilen tooall BLOB'ları uygulanır. Bazı BLOB'lar için toospecify farklı özellikleri veya meta veriler isterseniz ayrı bir kopyalama oturum toocreate gerekir. Bkz: [özelliklerini ayarlama ve meta veri hello içeri aktarma işlemi sırasında](storage-import-export-tool-setting-properties-metadata-import-v1.md)daha fazla bilgi için.

> [!NOTE]
>  Özetlenen hello gereksinimleri karşılayan birden çok makine varsa [Kurulum Azure içeri/dışarı aktarma aracı hello](storage-import-export-tool-setup-v1.md), bu aracı örneği her makinede çalıştırarak paralel olarak veri toomultiple sabit sürücüleri kopyalayabilirsiniz.

 Azure içeri/dışarı aktarma aracı hello ile hazırlama her sabit sürücü için hello aracı tek bir günlük dosyası oluşturur. Tüm sürücüleri toocreate hello Alma işinizin hello günlük dosyaları gerekir. Merhaba aracı kesintiye uğrarsa hello günlük dosyası da kullanılan tooresume sürücü hazırlama olabilir.

### <a name="azure-importexport-tool-syntax-for-an-import-job"></a>İçe aktarma işi için Azure içeri/dışarı aktarma aracı söz dizimi
 tooprepare sürücüler içeri aktarma işi için çağrı hello Azure içeri/dışarı aktarma aracı hello ile **PrepImport** komutu. Eklediğiniz hangi parametreleri bağlıdır olup bu olduğu hello üzerinde ilk kopya oturumu veya bir sonraki kopya oturumu.

 Merhaba ilk kopyalama oturum bir sürücü için bazı ek parametreler toospecify hello depolama hesabı anahtarı gerektirir; Merhaba hedef sürücü harfi; Sürücü Merhaba biçimlendirilmiş olması gerekir; Hello sürücü şifrelenmelidir olup olmadığını ve bu durumda, BitLocker anahtar hello; ve hello günlük dizini. Bir dizin veya tek bir dosyayı bir ilk kopyalama oturum toocopy hello sözdizimi şöyledir:

 **İlk oturum toocopy tek bir dizin kopyalama**

 `WAImportExport PrepImport /sk:<StorageAccountKey> /csas:<ContainerSas> /t: <TargetDriveLetter> [/format] [/silentmode] [/encrypt] [/bk:<BitLockerKey>] [/logdir:<LogDirectory>] /j:<JournalFile> /id:<SessionId> /srcdir:<SourceDirectory> /dstdir:<DestinationBlobVirtualDirectory> [/Disposition:<Disposition>] [/BlobType:<BlockBlob|PageBlob>] [/PropertyFile:<PropertyFile>] [/MetadataFile:<MetadataFile>]`

 **İlk oturum toocopy tek bir dosya kopyalama**

 `WAImportExport PrepImport /sk:<StorageAccountKey> /csas:<ContainerSas> /t: <TargetDriveLetter> [/format] [/silentmode] [/encrypt] [/bk:<BitLockerKey>] [/logdir:<LogDirectory>] /j:<JournalFile> /id:<SessionId> /srcfile:<SourceFile> /dstblob:<DestinationBlobPath> [/Disposition:<Disposition>] [/BlobType:<BlockBlob|PageBlob>] [/PropertyFile:<PropertyFile>] [/MetadataFile:<MetadataFile>]`

 Sonraki kopyalama oturumlarında toospecify hello başlangıç parametreleri gerekmez. Bir dizin veya tek bir dosya için bir sonraki kopyalama oturum toocopy hello sözdizimi şöyledir:

 **Sonraki kopyalama oturumları toocopy tek bir dizin**

 `WAImportExport PrepImport /j:<JournalFile> /id:<SessionId> /srcdir:<SourceDirectory> /dstdir:<DestinationBlobVirtualDirectory> [/Disposition:<Disposition>] [/BlobType:<BlockBlob|PageBlob>] [/PropertyFile:<PropertyFile>] [/MetadataFile:<MetadataFile>]`

 **Sonraki kopyalama oturumları toocopy tek bir dosya**

 `WAImportExport PrepImport /j:<JournalFile> /id:<SessionId> /srcfile:<SourceFile> /dstblob:<DestinationBlobPath> [/Disposition:<Disposition>] [/BlobType:<BlockBlob|PageBlob>] [/PropertyFile:<PropertyFile>] [/MetadataFile:<MetadataFile>]`

### <a name="parameters-for-hello-first-copy-session-for-a-hard-drive"></a>Parametreler hello için önce bir sabit sürücü için oturumu kopyalayın
 Hello Azure içeri/dışarı aktarma aracı toocopy dosyaları toohello sabit sürücü, her çalıştırdığınızda hello aracı kopya oturumu oluşturur. Her bir kopya oturumu tek bir dizin ya da tek bir dosya tooa sabit sürücü kopyalar. Merhaba kopya oturumu Hello durumunu toohello günlük dosyası yazılır. (Örneğin, tooa sistem güç kaybı) bir kopyası oturumu kesintiye uğrarsa hello Aracı'nı yeniden çalıştırmayı ve hello günlük dosyası hello komut satırında belirterek ettirilebilir.

> [!WARNING]
>  Merhaba belirtirseniz **/format** parametresi hello ilk kopya oturumu için hello sürücü biçimlendirilir ve hello sürücüdeki tüm veriler silinecek. Boş sürücüleri yalnızca kopya oturumunuz için kullanmak önerilir.

 her sürücü için ilk kopyalama oturum Hello için kullanılan hello komutu hello komutları sayısından farklı parametre sonraki kopyalama oturumlarına gerektirir. Merhaba aşağıdaki tabloda ilk kopya oturumu hello için kullanılabilir olan hello ek parametreler listelenmektedir:

|Komut satırı parametresi|Açıklama|
|-----------------------------|-----------------|
|**/SK:**< StorageAccountKey\>|`Optional.`Merhaba depolama hesabı anahtarı hello depolama hesabı toowhich hello veriler için içeri aktarılacak. Ya da içermelidir **/sk:**< StorageAccountKey\> veya **/csas:**< ContainerSas\> hello komutu.|
|**/csas:**< ContainerSas\>|`Optional`. Merhaba kapsayıcı SAS toouse tooimport veri toohello depolama hesabı. Ya da içermelidir **/sk:**< StorageAccountKey\> veya **/csas:**< ContainerSas\> hello komutu.<br /><br /> Bu parametre için değer Hello hello kapsayıcı adı, ardından bir soru işareti (?) ve hello SAS belirteci ile başlaması gerekir. Örneğin:<br /><br /> `mycontainer?sv=2014-02-14&sr=c&si=abcde&sig=LiqEmV%2Fs1LF4loC%2FJs9ZM91%2FkqfqHKhnz0JM6bqIqN0%3D&se=2014-11-20T23%3A54%3A14Z&sp=rwdl`<br /><br /> Merhaba izinleri hello URL veya bir saklı erişim ilkesinde belirtilen, okuma, içermelidir olup olmadığını yazma ve içeri aktarma işi ve okuma, yazma ve liste için dışarı aktarma işleri silin.<br /><br /> Bu parametre belirtilmediğinde, dışarı veya içeri aktarılan tüm BLOB'ları toobe hello paylaşılan erişim imzasını belirtilen hello kapsayıcısı içinde olmalıdır.|
|**/ t:**< TargetDriveLetter\>|`Required.`Merhaba hello hedef sabit sürücünün harfini hello geçerli kopyalama oturumu için iki nokta üst üste sondaki hello olmadan.|
|**Format**|`Optional.`Sürücü Merhaba biçimlendirilmiş toobe gerektiğinde bu parametreyi belirtin; Aksi takdirde yok sayın. Merhaba aracı hello sürücü biçimleri önce konsolundan onay ister. toosuppress hello onay hello /silentmode parametresini belirtin.|
|**/silentmode**|`Optional.`Bu parametre toosuppress hello onay'hello targert sürücü biçimlendirme için belirtin.|
|**/ şifrele**|`Optional.`Merhaba sürücü henüz hello aracı tarafından şifrelenmiş BitLocker ve gereksinimlerini toobe ile şifrelenmiş değil, bu parametre belirtildi. Merhaba sürücüsü BitLocker ile şifrelenmiş durumunda bu parametreyi atlayın ve hello belirtin `/bk` hello varolan BitLocker anahtar sağlama parametresi.<br /><br /> Merhaba belirtirseniz `/format` parametresi, sonra da belirtmeniz gerekir hello `/encrypt` parametresi.|
|**/BK:**< BitLockerKey\>|`Optional.`Varsa `/encrypt` olduğu belirtilen, bu parametreyi atlayın. Varsa `/encrypt` olan atlandığında toohave gereksinim zaten hello sürücüsü BitLocker ile şifrelenmiş. Bu parametre toospecify hello BitLocker anahtarını kullanın. İçeri aktarma işi için tüm sabit sürücülere yönelik BitLocker şifrelemesi gereklidir.|
|**/ LOGDIR:**< LogDirectory\>|`Optional.`bir dizin toobe toostore ayrıntılı günlükleri ve bunun yanı sıra geçici bildirim dosyalarını kullanılan Hello günlük dizini belirtir. Belirtilmezse, geçerli dizin hello hello günlük dizini kullanılır.|

### <a name="parameters-required-for-all-copy-sessions"></a>Tüm kopyalama oturumları için gerekli parametreleri
 Merhaba günlük dosyası, bir sabit sürücü için tüm kopyalama oturumlarını hello durumunu içerir. Toocreate hello iş alma hello bilgileri de içerir. Çalışan hello Azure içeri/dışarı aktarma aracı gibi bir kopyalama oturum kimliği, her zaman bir günlük dosyası belirtmeniz gerekir:

|||
|-|-|
|Komut satırı parametresi|Açıklama|
|**/j:**< JournalFile\>|`Required.`Merhaba yol toohello günlük dosyası. Her bir sürücü tam olarak bir günlük dosyası olmalıdır. Bu hello günlük dosyası hello hedef sürücüde bulunmalıdır değil unutmayın. Merhaba günlük dosya uzantısı `.jrn`.|
|**/ID:**< SessionID\>|`Required.`Merhaba oturum kimliği kopyalama oturumu tanımlar. Bu, kullanılan tooensure doğru kurtarma kesintiye uğramış kopyalama oturumu olur. Bir kopyalama oturumda kopyalanır dosyaları hello oturum kimliği hello hedef sürücüde sonra adlı bir dizinde depolanır.|

### <a name="parameters-for-copying-a-single-directory"></a>Tek bir dizin kopyalama için parametreler
 Tek bir dizin kopyalarken hello aşağıdaki gerekli ve isteğe bağlı parametreler geçerlidir:

|Komut satırı parametresi|Açıklama|
|----------------------------|-----------------|
|**/srcdir:**< SourceDirectory\>|`Required.`dosyaları toobe içeren hello kaynak dizin toohello hedef sürücü kopyalanır. Merhaba dizin yolu mutlak bir yol (göreli bir yol değil) olması gerekir.|
|**/dstdir:**< DestinationBlobVirtualDirectory\>|`Required.`Merhaba yolu toohello hedef sanal dizin Windows Azure depolama hesabınızdaki. Merhaba sanal dizin olabilir veya zaten mevcut olmayabilir.<br /><br /> Bir kapsayıcı belirtebilir veya bir blob öneki ister `music/70s/`. Merhaba hedef dizinin hello kapsayıcı adını, ardından bir eğik çizgi ile başlaması gerekir "/" ve isteğe bağlı olarak ile biten bir sanal blob dizin içerebilir "/".<br /><br /> Merhaba hedef kapsayıcı hello kök kapsayıcı olduğunda, hello kök kapsayıcı Merhaba Öne eğik çizgi dahil olmak üzere, açıkça belirtmelisiniz `$root/`. BLOB'ları hello kök kapsayıcısı altında içeremez "/" Merhaba hedef dizinin hello kök kapsayıcı olduğunda adlarında, tüm dizinlerde hello kaynak dizin kopyalanmaz beri.<br /><br /> Emin toouse hedef sanal dizinleri ve blobları belirtirken geçerli kapsayıcı adları olabilir. Kapsayıcı adları küçük harfli olması gerektiğini unutmayın. Kapsayıcı adlandırma kuralları için bkz: [adlandırma ve başvuran kapsayıcıları, Blobları ve meta veri](/rest/api/storageservices/naming-and-referencing-containers--blobs--and-metadata).|
|**/ Değerlendirme:**< yeniden adlandırmak &#124; Hayır üzerine &#124; üzerine >|`Optional.`Merhaba bir blob adresi zaten belirtildiğinde hello davranışını belirtir. Bu parametre için geçerli değerler şunlardır: `rename`, `no-overwrite` ve `overwrite`. Bu değerleri büyük küçük harfe duyarlı olduğunu unutmayın. Herhangi bir değer belirtilirse, hello varsayılandır `rename`.<br /><br /> Bu parametre hello tarafından belirtilen hello dizinindeki tüm hello dosyalarını etkiler için belirtilen değer Hello `/srcdir` parametresi.|
|**/ BlobType:**< BlockBlob &#124; PageBlob >|`Optional.`Merhaba hedef BLOB'ları Hello blob türünü belirtir. Geçerli değerler: `BlockBlob` ve `PageBlob`. Bu değerleri büyük küçük harfe duyarlı olduğunu unutmayın. Herhangi bir değer belirtilirse, hello varsayılandır `BlockBlob`.<br /><br /> Çoğu durumda, `BlockBlob` önerilir. Belirtirseniz `PageBlob`, her dosya hello dizininde hello uzunluğu hello sayfa BLOB'ları için bir sayfa boyutunu 512, birden fazla olmalıdır.|
|**/ PropertyFile:**< PropertyFile\>|`Optional.`Merhaba hedef BLOB'ları için yol toohello özelliği dosya. Bkz: [içeri/dışarı aktarma hizmeti meta verileri ve özellikleri dosya biçimi](../storage-import-export-file-format-metadata-and-properties.md) daha fazla bilgi için.|
|**/ MetadataFile:**< MetadataFile\>|`Optional.`Merhaba hedef BLOB'ları için yol toohello meta veri dosyası. Bkz: [içeri/dışarı aktarma hizmeti meta verileri ve özellikleri dosya biçimi](../storage-import-export-file-format-metadata-and-properties.md) daha fazla bilgi için.|

### <a name="parameters-for-copying-a-single-file"></a>Tek bir dosya kopyalama için parametreler
 Tek bir dosya kopyalarken hello aşağıdaki gerekli ve isteğe bağlı parametreleri geçerlidir:

|Komut satırı parametresi|Açıklama|
|----------------------------|-----------------|
|**/srcfile:**< SourceFile\>|`Required.`Merhaba tam yolu toohello dosya toobe kopyalanır. Merhaba dizin yolu mutlak bir yol (göreli bir yol değil) olması gerekir.|
|**/dstblob:**< DestinationBlobPath\>|`Required.`Windows Azure depolama hesabınızdaki Hello yolu toohello hedef blob. Merhaba blob olabilir veya zaten mevcut olmayabilir.<br /><br /> Hello kapsayıcı adı ile başlayan Hello blob adı belirtin. Merhaba blob adı ile başlatılamıyor "/" veya hello depolama hesabı adı. BLOB adlandırma kuralları için bkz: [adlandırma ve başvuran kapsayıcıları, Blobları ve meta veri](/rest/api/storageservices/naming-and-referencing-containers--blobs--and-metadata).<br /><br /> Merhaba hedef kapsayıcı hello kök kapsayıcı olduğunda, açıkça belirtmeniz gerekir `$root` kapsayıcı gibi hello gibi `$root/sample.txt`. BLOB'hello kök kapsayıcısı altında Not içeremez "/" adlarında.|
|**/ Değerlendirme:**< yeniden adlandırmak &#124; Hayır üzerine &#124; üzerine >|`Optional.`Merhaba bir blob adresi zaten belirtildiğinde hello davranışını belirtir. Bu parametre için geçerli değerler şunlardır: `rename`, `no-overwrite` ve `overwrite`. Bu değerleri büyük küçük harfe duyarlı olduğunu unutmayın. Herhangi bir değer belirtilirse, hello varsayılandır `rename`.|
|**/ BlobType:**< BlockBlob &#124; PageBlob >|`Optional.`Merhaba hedef BLOB'ları Hello blob türünü belirtir. Geçerli değerler: `BlockBlob` ve `PageBlob`. Bu değerleri büyük küçük harfe duyarlı olduğunu unutmayın. Herhangi bir değer belirtilirse, hello varsayılandır `BlockBlob`.<br /><br /> Çoğu durumda, `BlockBlob` önerilir. Belirtirseniz `PageBlob`, her dosya hello dizininde hello uzunluğu hello sayfa BLOB'ları için bir sayfa boyutunu 512, birden fazla olmalıdır.|
|**/ PropertyFile:**< PropertyFile\>|`Optional.`Merhaba hedef BLOB'ları için yol toohello özelliği dosya. Bkz: [içeri/dışarı aktarma hizmeti meta verileri ve özellikleri dosya biçimi](../storage-import-export-file-format-metadata-and-properties.md) daha fazla bilgi için.|
|**/ MetadataFile:**< MetadataFile\>|`Optional.`Merhaba hedef BLOB'ları için yol toohello meta veri dosyası. Bkz: [içeri/dışarı aktarma hizmeti meta verileri ve özellikleri dosya biçimi](../storage-import-export-file-format-metadata-and-properties.md) daha fazla bilgi için.|

### <a name="resuming-an-interrupted-copy-session"></a>Bir kesintiye uğramış kopyalama oturum sürdürme
 Herhangi bir nedenle bir kopya oturumu kesintiye uğrarsa, belirtilen yalnızca hello günlük dosyasıyla hello aracını çalıştırarak devam edebilirsiniz:

```
WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> /ResumeSession
```

 Yalnızca hello en son kopyasını oturumu, anormal varsa ettirilebilir.

> [!IMPORTANT]
>  Kopya oturumu sürdürdüğünüzde hello kaynak veri dosyaları ve dizinleri ekleyerek veya kaldırarak dosyaları değiştirmeyin.

### <a name="aborting-an-interrupted-copy-session"></a>Bir kesintiye uğramış kopya oturumu durduruluyor
 Kopya oturumu kesintiye ve (örneğin, bir kaynak dizin erişilemez oluyor uygulamasına yol açıyordu), olası tooresume değilse, böylece geri alınması hello geçerli oturum iptal gerekir ve yeni kopya oturumları geri başlatılabilir:

```
WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> /AbortSession
```

 Yalnızca hello son kopya oturumu, anormal olursa iptal. Bir sürücü için ilk kopyalama oturumu hello iptal edilemiyor unutmayın. Bunun yerine yeni bir günlük dosyasıyla hello kopyalama oturumlarını yeniden başlatmalısınız.

## <a name="next-steps"></a>Sonraki adımlar

* [Kurulum hello Azure içeri/dışarı aktarma aracı](storage-import-export-tool-setup-v1.md)
* [Özellikleri ayarlama ve hello sırasında meta veri alma işlemi](storage-import-export-tool-setting-properties-metadata-import-v1.md)
* [Örnek iş akışı tooprepare sabit sürücüler içeri aktarma işi için](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow-v1.md)
* [Sık kullanılan komutlar için hızlı başvuru](storage-import-export-tool-quick-reference-v1.md) 
* [Kopyalama günlük dosyalarıyla iş durumunu gözden geçirme](storage-import-export-tool-reviewing-job-status-v1.md)
* [Bir içeri aktarma işini onarma](storage-import-export-tool-repairing-an-import-job-v1.md)
* [Bir dışarı aktarma işini onarma](storage-import-export-tool-repairing-an-export-job-v1.md)
* [Sorun giderme hello Azure içeri/dışarı aktarma aracı](storage-import-export-tool-troubleshooting-v1.md)
