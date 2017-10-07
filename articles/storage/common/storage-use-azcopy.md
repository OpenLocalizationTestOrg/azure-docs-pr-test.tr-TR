---
title: "aaaCopy veya taşıma veri tooAzure Storage ile AzCopy Windows | Microsoft Docs"
description: "Blob, tablo ve dosya içeriği Windows yardımcı programı toomove veya kopya veri tooor Hello AzCopy kullanın. Yerel dosyalarından veri tooAzure depolama kopyalayın veya içinde veya depolama hesapları arasında veri kopyalayın. Kolayca, veri tooAzure depolama geçirin."
services: storage
documentationcenter: 
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: aa155738-7c69-4a83-94f8-b97af4461274
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/14/2017
ms.author: seguler
ms.openlocfilehash: a063a0380b7b8e6b212d0cec276f7d0f421936ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="transfer-data-with-hello-azcopy-on-windows"></a>Windows hello AzCopy ile veri aktarımı
AzCopy en uygun performans ile basit komutları kullanarak Microsoft Azure Blob, dosya ve tablo depolama biriminden veri tooand kopyalanması için tasarlanmış bir komut satırı yardımcı programıdır. Bir nesne tooanother veri depolama hesabınızda veya depolama hesapları arasında kopyalayabilirsiniz.

İndirebilirsiniz AzCopy iki sürümü vardır. AzCopy Windows .NET Framework ile oluşturulur ve Windows stili komut satırı seçenekleri sunar. [Linux üzerinde AzCopy](storage-use-azcopy-linux.md) çekirdek, POSIX stili komut satırı seçenekleri sunan Linux platformlar hedefler ile .NET Framework yerleşik olarak bulunur. Bu makalede Windows AzCopy kapsar.

## <a name="download-and-install-azcopy"></a>AzCopy yükleyip
### <a name="azcopy-on-windows"></a>Windows üzerinde AzCopy
Merhaba karşıdan [AzCopy Windows en son sürümünü](http://aka.ms/downloadazcopy).

#### <a name="installation-on-windows"></a>Windows yükleme
AzCopy hello Yükleyicisi'ni kullanarak Windows yükledikten sonra bir komut penceresi açın ve toohello AzCopy yükleme dizini, bilgisayarınızdaki - hello burada gidin `AzCopy.exe` yürütülebilir bulunur. İsterseniz, hello AzCopy yükleme konumu tooyour sistem yolu ekleyebilirsiniz. Varsayılan olarak, AzCopy da yüklü olduğundan`%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy` veya `%ProgramFiles%\Microsoft SDKs\Azure\AzCopy`.

## <a name="writing-your-first-azcopy-command"></a>İlk AzCopy komut yazma
AzCopy komutları Hello temel sözdizimi şöyledir:

```azcopy
AzCopy /Source:<source> /Dest:<destination> [Options]
```

Örnek hello çeşitli Microsoft Azure BLOB'ları, dosyaları ve tablolardan veri tooand kopyalama senaryoları gösterilmektedir. Toohello başvuran [AzCopy parametreleri](#azcopy-parameters) her örnekte kullanılan hello parametreler ayrıntılı bir açıklaması için bölüm.

## <a name="blob-download"></a>BLOB: karşıdan yükle
### <a name="download-single-blob"></a>Tek blob indirin

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /Pattern:"abc.txt"
```

Unutmayın hello klasörü `C:\myfolder` yok, AzCopy oluşturur ve indirme `abc.txt ` hello yeni klasöre.

### <a name="download-single-blob-from-secondary-region"></a>Tek blob ikincil bölge ' indirin

```azcopy
AzCopy /Source:https://myaccount-secondary.blob.core.windows.net/mynewcontainer /Dest:C:\myfolder /SourceKey:key /Pattern:abc.txt
```

Okuma erişimli coğrafi olarak yedekli depolama etkin olması gerektiğini unutmayın.

### <a name="download-all-blobs"></a>Tüm BLOB'ları indirme

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /S
```

Merhaba aşağıdaki varsayın BLOB'lar hello belirtilen kapsayıcısında bulunur:  

    abc.txt
    abc1.txt
    abc2.txt
    vd1\a.txt
    vd1\abcd.txt

Merhaba yükleme işleminden sonra dizin hello `C:\myfolder` hello aşağıdaki dosyaları içerir:

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\vd1\a.txt
    C:\myfolder\vd1\abcd.txt

Seçeneği belirtmezseniz, `/S`, blob yok indirilir.

### <a name="download-blobs-with-specified-prefix"></a>BLOB'lar ile belirtilen bir önek indirin

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /Pattern:a /S
```

Merhaba aşağıdaki varsayın BLOB'lar hello belirtilen kapsayıcısında bulunur. Merhaba önek ile başlayan tüm BLOB'lar `a` yüklenir:

    abc.txt
    abc1.txt
    abc2.txt
    xyz.txt
    vd1\a.txt
    vd1\abcd.txt

Merhaba yükleme işleminden sonra klasörü hello `C:\myfolder` hello aşağıdaki dosyaları içerir:

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt

Merhaba önek hello blob adı ilk kısmı hello forms toohello sanal dizini uygular. Yukarıda gösterilen hello örnekte yüklenmez şekilde hello sanal dizin hello Belirtilen önek, eşleşmiyor. Merhaba, ayrıca, seçenek `\S` belirtilmezse, AzCopy BLOB indirmek değil.

### <a name="set-hello-last-modified-time-of-exported-files-toobe-same-as-hello-source-blobs"></a>Dışa aktarılan dosyaları toobe hello son değişiklik saatini ayarlayın kaynak BLOB'ları hello aynı

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT
```

Son değiştiren bunların zamana dayalı hello indirme işlemi de BLOB'lar hariç tutabilirsiniz. Tooexclude BLOB'lar, son değişiklik zamanını hello aynı ya da hello hedef dosya daha yeni olan isterseniz, örneğin, hello ekleyin `/XN` seçeneği:

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT /XN
```

Veya, son değişiklik zamanını hello aynı ya da hello hedef dosyanın daha eski olan tooexclude BLOB'ları istiyorsanız hello ekleyin `/XO` seçeneği:

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT /XO
```

## <a name="blob-upload"></a>BLOB: karşıya yükle
### <a name="upload-single-file"></a>Tek dosya karşıya yükleme

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:"abc.txt"
```

Merhaba belirtilen hedef kapsayıcı mevcut değilse, AzCopy oluşturur ve karşıya dosya içine hello.

### <a name="upload-single-file-toovirtual-directory"></a>Tek dosya toovirtual dizin karşıya yükle

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer/vd /DestKey:key /Pattern:abc.txt
```

Merhaba belirtilen sanal dizin yok, AzCopy hello dosya tooinclude hello sanal dizin adının içinde yükler (*örneğin*, `vd/abc.txt` yukarıdaki hello örnekteki).

### <a name="upload-all-files"></a>Tüm dosyaları karşıya yükleme

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /S
```

Seçeneğini belirterek `/S` hello yüklemeleri Merhaba içeriğine belirtilen dizin tooBlob depolama yinelemeli olarak tüm alt klasörleri ve bunların dosyaları da karşıya anlamına gelir. Örneği için hello aşağıdaki varsayın dosyaları klasöründe bulunan `C:\myfolder`:

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\subfolder\a.txt
    C:\myfolder\subfolder\abcd.txt

Merhaba karşıya yükleme işleminden sonra aşağıdaki dosyaları hello hello kapsayıcı içerir:

    abc.txt
    abc1.txt
    abc2.txt
    subfolder\a.txt
    subfolder\abcd.txt

Seçeneği belirtmezseniz, `/S`, AzCopy yinelemeli olarak karşıya değil. Merhaba karşıya yükleme işleminden sonra aşağıdaki dosyaları hello hello kapsayıcı içerir:

    abc.txt
    abc1.txt
    abc2.txt

### <a name="upload-files-matching-specified-pattern"></a>Belirtilen desenle eşleşen dosyaları karşıya yükleme

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:a* /S
```

Merhaba aşağıdaki varsayın dosyaları klasöründe bulunan `C:\myfolder`:

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\xyz.txt
    C:\myfolder\subfolder\a.txt
    C:\myfolder\subfolder\abcd.txt

Merhaba karşıya yükleme işleminden sonra aşağıdaki dosyaları hello hello kapsayıcı içerir:

    abc.txt
    abc1.txt
    abc2.txt
    subfolder\a.txt
    subfolder\abcd.txt

Seçeneği belirtmezseniz, `/S`, AzCopy yalnızca sanal bir dizinde bulunan değilsiniz BLOB'ları yükler:

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt

### <a name="specify-hello-mime-content-type-of-a-destination-blob"></a>Hedef BLOB Hello MIME içerik türünü belirtin
Çok hedef blob hello içerik türü varsayılan olarak, AzCopy ayarlar`application/octet-stream`. 3.1.0 sürümünden başlayarak, hello içerik türü hello seçeneği aracılığıyla açıkça belirtebilirsiniz `/SetContentType:[content-type]`. Bu sözdiziminin hello içerik türü için tüm BLOB'ları bir karşıya yükleme işleminde ayarlar.

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.blob.core.windows.net/myContainer/ /DestKey:key /Pattern:ab /SetContentType:video/mp4
```

Belirtirseniz `/SetContentType` olmayan bir değer, AzCopy her bir blob veya dosyanın içerik türü dosya uzantısı tooits göre ayarlar.

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.blob.core.windows.net/myContainer/ /DestKey:key /Pattern:ab /SetContentType
```

## <a name="blob-copy"></a>BLOB: kopyalama
### <a name="copy-single-blob-within-storage-account"></a>Depolama hesabı içinde tek blob kopyalama

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1 /Dest:https://myaccount.blob.core.windows.net/mycontainer2 /SourceKey:key /DestKey:key /Pattern:abc.txt
```

Bir depolama hesabındaki blob kopyaladığınızda bir [sunucu tarafı kopyası](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) işlemi gerçekleştirilir.

### <a name="copy-single-blob-across-storage-accounts"></a>Tek blob depolama hesapları arasında kopyalama

```azcopy
AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt
```

Bir blob depolama hesapları arasında kopyaladığınızda, bir [sunucu tarafı kopyası](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) işlemi gerçekleştirilir.

### <a name="copy-single-blob-from-secondary-region-tooprimary-region"></a>İkincil bölge tooprimary bölgesinden tek blob kopyalama

```azcopy
AzCopy /Source:https://myaccount1-secondary.blob.core.windows.net/mynewcontainer1 /Dest:https://myaccount2.blob.core.windows.net/mynewcontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt
```

Okuma erişimli coğrafi olarak yedekli depolama etkin olması gerektiğini unutmayın.

### <a name="copy-single-blob-and-its-snapshots-across-storage-accounts"></a>Depolama hesapları arasında tek blob ve onun anlık görüntüleri kopyalama

```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt /Snapshot
```

Hello kopyalama işleminden sonra hello hedef kapsayıcı hello blob ve onun anlık görüntülerini içerir. Merhaba blob yukarıdaki hello örnekte iki anlık görüntüsü sahip olduğunu varsayarak, hello kapsayıcı hello aşağıdakileri içeren blob ve anlık görüntüler:

    abc.txt
    abc (2013-02-25 080757).txt
    abc (2014-02-21 150331).txt

### <a name="synchronously-copy-blobs-across-storage-accounts"></a>Zaman uyumlu olarak depolama hesapları arasında BLOB kopyalama
AzCopy varsayılan olarak, iki depolama uç noktaları arasında verileri zaman uyumsuz olarak kopyalar. Bu nedenle, hello kopyalama işlemi çalıştırır hiçbir SLA ne kadar hızlı blob bakımından sahip yedek bant genişliğini kapasite kullanarak hello arka planda kopyalanır ve hello kopyalama tamamlandı başarısız oldu veya kadar AzCopy düzenli aralıklarla hello kopyanın durumunu denetler.

Merhaba `/SyncCopy` seçeneği sağlar hello kopyalama işlemi tutarlı hızı alır. AzCopy hello BLOB'lar yükleyerek hello zaman uyumlu kopyası gerçekleştirir toocopy hello öğesinden belirtilen kaynak toolocal bellek ve ardından toohello Blob Depolama Hedef karşıya yükleme.

```azcopy
AzCopy /Source:https://myaccount1.blob.core.windows.net/myContainer/ /Dest:https://myaccount2.blob.core.windows.net/myContainer/ /SourceKey:key1 /DestKey:key2 /Pattern:ab /SyncCopy
```

`/SyncCopy`Karşılaştırılan tooasynchronous kopyalama hello maliyet ek çıkış önerilen yaklaşımı oluşturabilir toouse bu hello olan bir Azure VM seçenektir aynı bölgede kaynak depolama hesabı tooavoid çıkışı maliyeti.

## <a name="file-download"></a>Dosya: karşıdan yükle
### <a name="download-single-file"></a>Tek dosya indirme

```azcopy
AzCopy /Source:https://myaccount.file.core.windows.net/myfileshare/myfolder1/ /Dest:C:\myfolder /SourceKey:key /Pattern:abc.txt
```

Merhaba kaynağıdır Azure dosya paylaşımının, sonra da hello tam dosya adı belirtmelisiniz belirtilmişse (*örneğin* `abc.txt`) toodownload tek bir dosya veya seçeneğini belirtin `/S` toodownload tüm dosyaları hello paylaşımı yinelemeli olarak. Bir dosya düzeni ve seçenek toospecify çalışırken `/S` birlikte hatayla sonuçlanır.

### <a name="download-all-files"></a>Tüm dosyaları indirme

```azcopy
AzCopy /Source:https://myaccount.file.core.windows.net/myfileshare/ /Dest:C:\myfolder /SourceKey:key /S
```

Boş klasörleri indirilmez unutmayın.

## <a name="file-upload"></a>Dosya: karşıya yükle
### <a name="upload-single-file"></a>Tek dosya karşıya yükleme

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /Pattern:abc.txt
```

### <a name="upload-all-files"></a>Tüm dosyaları karşıya yükleme

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /S
```

Boş klasörleri değil karşıya unutmayın.

### <a name="upload-files-matching-specified-pattern"></a>Belirtilen desenle eşleşen dosyaları karşıya yükleme

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /Pattern:ab* /S
```

## <a name="file-copy"></a>Dosya: kopyalama
### <a name="copy-across-file-shares"></a>Dosya paylaşımlarında kopyalayın

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare1/ /Dest:https://myaccount2.file.core.windows.net/myfileshare2/ /SourceKey:key1 /DestKey:key2 /S
```
Dosya paylaşımlarında bir dosya kopyaladığınızda bir [sunucu tarafı kopyası](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) işlemi gerçekleştirilir.

### <a name="copy-from-file-share-tooblob"></a>Dosya Paylaşımı tooblob kopyalayın

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare/ /Dest:https://myaccount2.blob.core.windows.net/mycontainer/ /SourceKey:key1 /DestKey:key2 /S
```
Dosya Paylaşımı tooblob bir dosya kopyaladığınızda bir [sunucu tarafı kopyası](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) işlemi gerçekleştirilir.


### <a name="copy-from-blob-toofile-share"></a>BLOB toofile paylaşımından kopyalayın

```azcopy
AzCopy /Source:https://myaccount1.blob.core.windows.net/mycontainer/ /Dest:https://myaccount2.file.core.windows.net/myfileshare/ /SourceKey:key1 /DestKey:key2 /S
```
Blob toofile paylaşımından bir dosya kopyaladığınızda bir [sunucu tarafı kopyası](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) işlemi gerçekleştirilir.

### <a name="synchronously-copy-files"></a>Zaman uyumlu olarak dosyaları kopyalayın
Merhaba belirtebilirsiniz `/SyncCopy` seçeneğini dosya depolama tooBlob depolama alanından, depolama, File Storage tooFile toocopy verileri ve Blob Depolama tooFile depolama alanından eşzamanlı olarak, AzCopy hello kaynak veri toolocal bellek yükleyerek bunu yapar ve yükleyin yeniden toodestination. Standart çıkış maliyet geçerlidir.

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare1/ /Dest:https://myaccount2.file.core.windows.net/myfileshare2/ /SourceKey:key1 /DestKey:key2 /S /SyncCopy
```

Dosya depolama tooBlob depolama kopyalarken hello varsayılan blob türü blok blobu, kullanıcı seçeneği belirtebilirsiniz `/BlobType:page` toochange hello hedef blob türü.

Unutmayın `/SyncCopy` karşılaştırma tooasynchronous kopyalama maliyet ek çıkış oluşturabilir, hello önerilen yaklaşım ise bu seçeneği hello hello olan Azure VM toouse aynı bölgede kaynak depolama hesabı tooavoid çıkışı maliyeti.

## <a name="table-export"></a>Tablo: dışarı aktarma
### <a name="export-table"></a>Dışarı aktarma tablosu

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key
```

AzCopy bir bildirim dosyası toohello belirtilen hedef klasör yazar. Merhaba bildirim dosyası hello alma işlemi toolocate hello gerekli verileri dosyalarında kullanılır ve veri doğrulama gerçekleştirin. Merhaba bildirim dosyası adlandırma kuralı varsayılan olarak aşağıdaki hello kullanır:

    <account name>_<table name>_<timestamp>.manifest

Kullanıcı ayrıca hello seçeneği belirtin `/Manifest:<manifest file name>` tooset hello yayılma dosyası adı.

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /Manifest:abc.manifest
```

### <a name="split-export-into-multiple-files"></a>Birden çok dosyalarına bölünmüş dışarı aktarma

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/mytable/ /Dest:C:\myfolder /SourceKey:key /S /SplitSize:100
```

AzCopy kullanan bir *birim dizin* veri bölme hello dosya toodistinguish birden çok dosya adları. Merhaba birim dizini iki bölümden oluşur bir *bölüm anahtarı aralığının dizin* ve *bölünmüş dosya dizini*. Her iki dizinleri sıfır tabanlı.

Merhaba bölüm anahtarı aralığının dizinidir 0 hello kullanıcı seçeneği belirlemezse `/PKRS`.

Örneğin, AzCopy seçeneği hello kullanıcının belirttiği sonra iki veri dosyalarını oluşturur düşünelim `/SplitSize`. veri dosyası adları kaynaklanan hello olabilir:

    myaccount_mytable_20140903T051850.8128447Z_0_0_C3040FE8.json
    myaccount_mytable_20140903T051850.8128447Z_0_1_0AB9AC20.json

Bu hello olası en küçük değerin seçenek için Not `/SplitSize` 32 MB'dir. Merhaba hedef Blob Depolama belirtilirse, kendi boyutları hello blob boyutu sınırlaması (200 GB) ulaştığında AzCopy hello veri dosyası ayırır, bakılmaksızın olup seçeneği `/SplitSize` hello kullanıcı tarafından belirtilen.

### <a name="export-table-toojson-or-csv-data-file-format"></a>Dışarı aktarma tablosu tooJSON veya CSV veri dosyası biçimi
Varsayılan olarak AzCopy tabloları tooJSON veri dosyalarını dışarı aktarır. Merhaba seçeneği belirtebilirsiniz `/PayloadFormat:JSON|CSV` tooexport hello tablolar JSON veya CSV olarak.

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /PayloadFormat:CSV
```

AzCopy Hello CSV yük biçimi belirtirken, aynı zamanda dosya uzantısına sahip bir şema dosyası oluşturur. `.schema.csv` her veri dosyası için.

### <a name="export-table-entities-concurrently"></a>Tablo varlıkları eşzamanlı olarak dışarı aktarma

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /PKRS:"aa#bb"
```

AzCopy başlatır eşzamanlı işlem tooexport varlıklar hello kullanıcı seçeneği belirttiğinde `/PKRS`. Her bir işlemin bir bölüm anahtarı aralığının dışa aktarır.

Merhaba eşzamanlı işlem sayısını da seçeneği tarafından denetlendiğini unutmayın `/NC`. AzCopy kullanan çekirdekli işlemciler hello sayısı hello varsayılan değeri olarak `/NC` tablo varlıkları kopyalarken olsa bile `/NC` belirtilmedi. Merhaba kullanıcı seçeneği belirttiğinde `/PKRS`, AzCopy hello hello iki değerleri - bölüm anahtar aralıklarına karşılık örtük veya açık olarak belirtilen eşzamanlı işlemleri - toodetermine hello eşzamanlı işlem toostart sayıda küçük kullanır. Daha fazla ayrıntı için yazın `AzCopy /?:NC` hello komut satırında.

### <a name="export-table-tooblob"></a>Tablo tooblob dışarı aktarma

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:https://myaccount.blob.core.windows.net/mycontainer/ /SourceKey:key1 /Destkey:key2
```

AzCopy bir JSON veri dosyası adlandırma kuralı aşağıdaki ile Merhaba blob kapsayıcısı içinde oluşturur:

    <account name>_<table name>_<timestamp>_<volume index>_<CRC>.json

oluşturulan hello JSON veri dosyası en küçük meta verileri için hello yük biçimi izler. Bu yük biçimi hakkında daha fazla bilgi için bkz: [tablo hizmeti işlemleri için yük biçimi](http://msdn.microsoft.com/library/azure/dn535600.aspx).

Tablolar tooblobs dışarı aktarılırken AzCopy hello tablo varlıkları toolocal geçici veri dosyalarını indirir ve bu varlıkları toohello blob'u karşıya unutmayın. Bu geçici veri dosyalarını hello varsayılan yolu ile hello günlük dosyası klasörü içine konur "<code>%LocalAppData%\Microsoft\Azure\AzCopy</code>" olarak seçeneği belirtebilirsiniz/Z: [günlük dosyası klasörü] toochange hello günlük dosyası klasörü konumu ve bu nedenle hello geçici veri dosyaları konumunu değiştirin. Merhaba edildikten sonra hello geçici veri dosyasında yerel disk hemen silinir rağmen dosyalarının boyutu, tablo varlıklarınızı boyutu ve hello seçeneği /SplitSize ile belirtilen hello boyutu tarafından belirlenir geçici verileri karşıya toohello blob, lütfen sahip olduğunuzdan emin olun yeterli yerel disk alanı toostore bu geçici veri dosyalarını silinmeden önce.

## <a name="table-import"></a>Tablo: alma
### <a name="import-table"></a>Alma tablosu

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.table.core.windows.net/mytable1/ /DestKey:key /Manifest:"myaccount_mytable_20140103T112020.manifest" /EntityOperation:InsertOrReplace
```

Merhaba seçeneği `/EntityOperation` nasıl tooinsert varlıklarının içinde tablo hello gösterir. Olası değerler şunlardır:

* `InsertOrSkip`: Var olan bir varlığı atlar veya hello tabloda mevcut değilse yeni bir varlık ekler.
* `InsertOrMerge`: Birleştirir var olan bir varlığı veya hello tabloda mevcut değilse yeni bir varlık ekler.
* `InsertOrReplace`: Var olan bir varlığı değiştirir veya hello tabloda mevcut değilse yeni bir varlık ekler.

Seçeneği belirtemezsiniz Not `/PKRS` hello alma senaryoda. Merhaba verme senaryosu, hangi belirtmelisiniz seçeneği aksine `/PKRS` toostart eşzamanlı işlem, AzCopy başlatır eşzamanlı operasyonlar varsayılan olarak bir tablo içeri aktardığınızda. Merhaba varsayılan başlatılan eşzamanlı işlem sayısını eşit toohello çekirdekli işlemciler sayısıdır; Bununla birlikte, eşzamanlı seçeneğiyle farklı sayıda belirtebilirsiniz `/NC`. Daha fazla ayrıntı için yazın `AzCopy /?:NC` hello komut satırında.

AzCopy yalnızca JSON değil CSV içe aktarma desteklediğini unutmayın. AzCopy değil kullanıcı tarafından oluşturulan JSON öğesinden tablo içeri aktarmalar destekler ve dosyaları bildirimi. Bu dosyaların her ikisinin bir AzCopy tablo verme etki alanından gelmesi gerekir. tooavoid hataları, lütfen değiştirmeyin hello dışarı JSON ya da bildirim dosyası.

### <a name="import-entities-tootable-using-blobs"></a>BLOB alma varlıklar tootable kullanma
Bir Blob kapsayıcısını hello aşağıdakileri içeren varsayalım: Azure tablo ve eşlik eden bildirim dosyasını temsil eden bir JSON dosyası.

    myaccount_mytable_20140103T112020.manifest
    myaccount_mytable_20140103T112020_0_0_0AF395F1DC42E952.json

Bu blob kapsayıcısında hello bildirim dosyası kullanarak bir tabloya komutu tooimport varlıklar aşağıdaki hello çalıştırabilirsiniz:

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:https://myaccount.table.core.windows.net/mytable /SourceKey:key1 /DestKey:key2 /Manifest:"myaccount_mytable_20140103T112020.manifest" /EntityOperation:"InsertOrReplace"
```

## <a name="other-azcopy-features"></a>Diğer AzCopy özellikleri
### <a name="only-copy-data-that-doesnt-exist-in-hello-destination"></a>Merhaba hedefte mevcut olmayan veri Kopyala
Merhaba `/XO` ve `/XN` parametreler, sırasıyla kopyalanmasını tooexclude daha eski veya yeni kaynak kaynakları sağlar. Merhaba hedef yoksa toocopy kaynak kaynakları yalnızca istiyorsanız, her iki parametre hello AzCopy komut belirtebilirsiniz:

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /XO /XN

    /Source:C:\myfolder /Dest:http://myaccount.file.core.windows.net/myfileshare /DestKey:<destkey> /S /XO /XN

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:http://myaccount.blob.core.windows.net/mycontainer1 /SourceKey:<sourcekey> /DestKey:<destkey> /S /XO /XN

Merhaba kaynak veya hedef tablo olduğunda bu desteklenmediğini unutmayın.

### <a name="use-a-response-file-toospecify-command-line-parameters"></a>Bir yanıt dosyası toospecify komut satırı parametreleri kullanma

```azcopy
AzCopy /@:"C:\responsefiles\copyoperation.txt"
```

AzCopy komut satırı parametreleri bir yanıt dosyası içerebilir. Merhaba komut satırında bir hello içeriğiyle doğrudan değiştirme hello dosyasının gerçekleştirme belirtilmiş sanki AzCopy işlemleri hello dosyasındaki parametreleri hello.

Adlı bir yanıt dosyası varsayın `copyoperation.txt`, satırlardan hello içerir. Tek bir satıra her AzCopy parametresi belirtilebilir.

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /Y

veya satırları ayrı:

    /Source:http://myaccount.blob.core.windows.net/mycontainer
    /Dest:C:\myfolder
    /SourceKey:<sourcekey>
    /S
    /Y

AzCopy, iki hattında hello parametre bölerseniz hello için aşağıda gösterildiği gibi başarısız `/sourcekey` parametre:

    http://myaccount.blob.core.windows.net/mycontainer
     C:\myfolder
    /sourcekey:
    <sourcekey>
    /S
    /Y

### <a name="use-multiple-response-files-toospecify-command-line-parameters"></a>Birden çok yanıt dosyaları toospecify komut satırı parametreleri kullanma
Adlı bir yanıt dosyası varsayın `source.txt` kaynak kapsayıcı belirtir:

    /Source:http://myaccount.blob.core.windows.net/mycontainer

Ve adlı bir yanıt dosyası `dest.txt` hello dosya sisteminde bir hedef klasör belirtir:

    /Dest:C:\myfolder

Ve adlı bir yanıt dosyası `options.txt` AzCopy seçeneklerini belirtir:

    /S /Y

AzCopy toocall bu yanıt dosyaları ile her biri bulunan bir dizinde `C:\responsefiles`, bu komutu kullanın:

```azcopy
AzCopy /@:"C:\responsefiles\source.txt" /@:"C:\responsefiles\dest.txt" /SourceKey:<sourcekey> /@:"C:\responsefiles\options.txt"   
```

Tüm hello tek tek parametreleri hello komut satırında eklenirse gibi AzCopy bu komut işler:

```azcopy
AzCopy /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /Y
```

### <a name="specify-a-shared-access-signature-sas"></a>Paylaşılan erişim imzası (SAS) belirtin

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1 /Dest:https://myaccount.blob.core.windows.net/mycontainer2 /SourceSAS:SAS1 /DestSAS:SAS2 /Pattern:abc.txt
```

Ayrıca, bir SAS hello kapsayıcı URI belirtebilirsiniz:

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1/?SourceSASToken /Dest:C:\myfolder /S
```

### <a name="journal-file-folder"></a>Günlük dosyası klasörü
Bir komut tooAzCopy sorun her zaman hello varsayılan klasöründe bir günlük dosyası var olup var veya bu seçeneği belirtilen bir klasörde varolup denetler. Her iki yerde Hello günlük dosyası mevcut değilse, AzCopy hello işlemi yeni olarak değerlendirir ve yeni bir günlük dosyası oluşturur.

Merhaba günlük dosyası mevcut değilse, AzCopy girdiğiniz hello komut satırı hello komut satırı hello günlük dosyasında eşleşip eşleşmediğini denetler. Merhaba iki komut satırları eşleşirse, AzCopy hello tamamlanmamış işlemi sürdürür. Bunlar eşleşmiyorsa, istendiğinde tooeither üzerine yaz hello günlük dosyası toostart yeni işlem ya da toocancel hello geçerli işlem demektir.

Merhaba günlük dosyası için toouse hello varsayılan konum istiyorsanız:

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Z
```

Seçeneği unutursanız `/Z`, veya seçeneğini belirtin `/Z` hello klasör yolu, yukarıda gösterildiği gibi AzCopy hello günlük dosyası olan hello varsayılan konumda, oluşturur `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`. Merhaba günlük dosyası zaten varsa, AzCopy hello günlük dosyasına dayalı hello işlemi sürdürür.

Toospecify hello günlük dosyası için özel bir konum istiyorsanız:

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Z:C:\journalfolder\
```

Bu örnek, zaten yoksa, hello günlük dosyası oluşturur. Mevcut değilse, AzCopy hello günlük dosyasına dayalı hello işlemi sürdürür.

Tooresume AzCopy işlemi istiyorsanız:

```azcopy
AzCopy /Z:C:\journalfolder\
```

Bu örnek toocomplete başarısız olmuş hello son işlem sürdürür.

### <a name="generate-a-log-file"></a>Bir günlük dosyası oluşturur

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /V
```

Seçeneğini belirtirseniz `/V` bir dosya yolu toohello ayrıntılı günlüğü sağlamadan sonra AzCopy hello günlük dosyası olan hello varsayılan konumda oluşturur `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.

Aksi takdirde, özel bir konumda bir günlük dosyası oluşturabilirsiniz:

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /V:C:\myfolder\azcopy1.log
```

Seçenek aşağıdaki göreli bir yol belirtirseniz, unutmayın `/V`, gibi `/V:test/azcopy1.log`, hello ayrıntılı günlük hello geçerli çalışma dizini adlı bir alt klasör içinde oluşturulan sonra `test`.

### <a name="specify-hello-number-of-concurrent-operations-toostart"></a>Eşzamanlı operasyonlar toostart Hello sayısını belirtin
Seçenek `/NC` eşzamanlı kopyalama işlemleri hello sayısını belirtir. Varsayılan olarak, belirli bir sayıda eşzamanlı işlem tooincrease hello veri aktarımı işleme AzCopy başlatır. Tablo işlemleri için hello eşzamanlı işlem elinizde işlemci sayısına eşit toohello sayısıdır. BLOB ve dosya işlemleri, eşzamanlı işlem sayısını hello için 8 kat hello elinizde işlemci sayısına eşittir. Düşük bant genişlikli ağ üzerinden AzCopy çalıştırıyorsanız, kaynak rekabet tarafından nedeniyle /NC tooavoid hatası için daha düşük bir sayı belirtebilirsiniz.

### <a name="run-azcopy-against-azure-storage-emulator"></a>AzCopy Azure Storage öykünücüsüne karşı çalıştırma
AzCopy hello karşı çalıştırabilirsiniz [Azure Storage öykünücüsü](storage-use-emulator.md) BLOB'lar için:

```azcopy
AzCopy /Source:https://127.0.0.1:10000/myaccount/mycontainer/ /Dest:C:\myfolder /SourceKey:key /SourceType:Blob /S
```

ve tabloları:

```azcopy
AzCopy /Source:https://127.0.0.1:10002/myaccount/mytable/ /Dest:C:\myfolder /SourceKey:key /SourceType:Table
```

## <a name="azcopy-parameters"></a>AzCopy parametreleri
AzCopy için Parametreler aşağıda açıklanmıştır. AzCopy kullanma hakkında Yardım için hello komut satırından komutları aşağıdaki hello birini yazabilirsiniz:

* AzCopy için ayrıntılı komut satırı Yardım için:`AzCopy /?`
* Herhangi bir AzCopy parametre ile ilgili ayrıntılı yardım için:`AzCopy /?:SourceKey`
* Komut satırı örnekleri için:`AzCopy /?:Samples`

### <a name="sourcesource"></a>/ Kaynak: "kaynak"
Merhaba veri kaynağından hangi toocopy belirtir. Merhaba kaynak dosya sistemi dizini, bir blob kapsayıcı, blob sanal dizin, bir depolama dosya paylaşımı, bir depolama dosyası dizini veya bir Azure tablosu olabilir.

**Uygulanabilir:** BLOB'lar, dosyalar, tablolar

### <a name="destdestination"></a>/ Taşınmaya: "hedef"
Merhaba hedef toocopy belirtir. Merhaba hedef dosya sistemi dizini, bir blob kapsayıcı, blob sanal dizin, bir depolama dosya paylaşımı, bir depolama dosyası dizini veya bir Azure tablosu olabilir.

**Uygulanabilir:** BLOB'lar, dosyalar, tablolar

### <a name="patternfile-pattern"></a>/ Desen: "dosya deseni"
Hangi dosyaların toocopy belirten bir dosya düzeni belirtir. Merhaba /Pattern parametresi Hello davranışını hello kaynak verilerin hello konumunu ve hello Özyinelemeli modu seçeneği hello varlığını tarafından belirlenir. /S. seçeneği belirtilen Özyinelemeli modu

Merhaba belirtilen kaynak bir dizin hello dosya sisteminde standart joker karakterler etkindir ve hello dizini içindeki dosyaların eşleştirme hello dosya deseni sağlanan ise. /S Belirtilen seçeneği sonra AzCopy de hello dizini altındaki tüm alt klasörlerdeki tüm dosyaları karşı hello belirtilen desenle eşleşiyorsa.

Merhaba belirtilen kaynak blob kapsayıcısı veya sanal dizin ise, joker karakter uygulanmaz. /S Belirtilen seçeneği sonra AzCopy hello belirtilen dosya düzeni blob önek olarak yorumlar varsa. /S belirtilmezse, seçeneği sonra AzCopy tam blob adlarıyla hello dosya desen eşleşirse.

Merhaba kaynağıdır Azure dosya paylaşımının sonra hello tam dosya adı (örneğin abc.txt) ya da belirtmelisiniz belirtilmişse toocopy tek bir dosya veya seçeneği /S toocopy tüm dosyaları hello paylaşımı yinelemeli olarak belirtin. Toospecify hem bir dosya düzeni ve seçeneği /S birlikte sonuçlarında hatayla çalışıyor.

AzCopy büyük küçük harfe duyarlı bir blob kapsayıcı veya blob sanal dizin hello/Source olduğunda ve diğer durumlarda kullanan tüm eşleştirme büyük küçük harf duyarsız hello eşleşen kullanır.

Merhaba hiçbir dosya deseni belirtildiğinde kullanılan varsayılan dosya düzeni olan *.* bir dosya sistemi konumu veya bir Azure depolama konumu için boş bir önek. Birden çok dosya desenlerinin belirtilmesi desteklenmiyor.

**Uygulanabilir:** BLOB'ların, dosyaları

### <a name="destkeystorage-key"></a>/ DestKey: "depolama anahtar"
Merhaba depolama hesabı anahtarı hello hedef kaynak için belirtir.

**Uygulanabilir:** BLOB'lar, dosyalar, tablolar

### <a name="destsassas-token"></a>/ DestSAS: "sas belirteci"
(Eğer varsa) hello hedef için okuma ve yazma izinlerine sahip paylaşılan erişim imzası (SAS) belirtir. Surround hello SAS şekliyle çift tırnak işareti ile komut satırı özel karakterler içeriyor.

Merhaba hedef kaynak, bir blob kapsayıcısını, dosya paylaşımı veya tablo ise, bu seçenek hello SAS belirteci tarafından izlenen ya da belirtebilirsiniz veya hello hedef blob kapsayıcısını, dosya paylaşımı veya tablonun URI, bu seçeneği olmadan bir parçası olarak hello SAS belirtebilirsiniz.

Merhaba kaynak ve hedef olan hem BLOB'ları sonra hello hedef blob hello içinde aynı bulunmalıdır hello kaynak blob depolama hesabı.

**Uygulanabilir:** BLOB'lar, dosyalar, tablolar

### <a name="sourcekeystorage-key"></a>/ SourceKey: "depolama anahtar"
Merhaba depolama hesabı anahtarı hello kaynak kaynağın belirtir.

**Uygulanabilir:** BLOB'lar, dosyalar, tablolar

### <a name="sourcesassas-token"></a>/ SourceSAS: "sas belirteci"
Merhaba kaynak için okuma ve liste izinlerine sahip paylaşılan erişim imzası (varsa) belirtir. Surround hello SAS şekliyle çift tırnak işareti ile komut satırı özel karakterler içeriyor.

Bir blob kapsayıcısını Hello kaynak kaynak ise ve bir anahtar ya da SAS sağlanan hello blob kapsayıcısı anonim erişim okuyun.

Merhaba kaynağı bir dosya paylaşımı veya tablo ise, bir anahtar veya bir SAS sağlanmalıdır.

**Uygulanabilir:** BLOB'lar, dosyalar, tablolar

### <a name="s"></a>/ S
Kopyalama işlemleri için özyinelemeli modunu belirtir. Özyinelemeli modunda AzCopy tüm BLOB veya alt klasörler de dahil hello belirtilen dosya deseni ile eşleşen dosyaları kopyalar.

**Uygulanabilir:** BLOB'ların, dosyaları

### <a name="blobtypeblock--page--append"></a>/ BlobType: "blok" | "Sayfa" | "Ekle"
Merhaba hedef blob blok blobu, bir sayfa blob'u ya da bir ek blobu olup olmadığını belirtir. Bu seçenek yalnızca bir blob karşıya yüklenirken kullanılır. Aksi takdirde bir hata oluşturulur. Merhaba hedef blob ise ve bu seçenek, varsayılan olarak, belirtilmemiş bir blok blobu AzCopy oluşturur.

**Uygulanabilir:** BLOB'ları

### <a name="checkmd5"></a>/ CheckMD5
Karşıdan yüklenen veriler için MD5 karma değeri hesaplar ve hello blob depolanmış hello MD5 karma veya dosyanın içeriği MD5 özelliğini hesaplanan hello karmayla eşleşen doğrular. Bu seçenek tooperform hello MD5 denetimi verilerini yüklerken belirtmeniz gerekir böylece hello MD5 onay varsayılan olarak kapalıdır.

Azure Storage için hello blob depolanan MD5 karma değeri bu hello garanti etmez Not veya dosya güncel olduğundan. Merhaba blob veya dosya değiştirildiğinde istemcinin sorumluluk tooupdate hello MD5 var.

AzCopy her zaman bir Azure blob veya dosya için hello Content-MD5 özelliği dosyalarını karşıya yükledikten sonra toohello hizmet ayarlar.  

**Uygulanabilir:** BLOB'ların, dosyaları

### <a name="snapshot"></a>/ Anlık görüntü
Gösterir olup olmadığını tootransfer anlık görüntüler. Bu seçenek, yalnızca Hello kaynak blob olduğunda geçerlidir.

Merhaba aktarılan blob anlık görüntüler şu biçimde adlandırılır: blob adı (anlık görüntü-time) .extension

Varsayılan olarak, anlık görüntüleri kopyalanmaz.

**Uygulanabilir:** BLOB'ları

### <a name="vverbose-log-file"></a>/ V: [verbose-günlük dosyası]
Bir günlük dosyasına çıkarır ayrıntılı durum iletileri.

Varsayılan olarak, hello ayrıntılı günlük dosyası içinde AzCopyVerbose.log adlı `%LocalAppData%\Microsoft\Azure\AzCopy`. Varolan bir dosya konumu için bu seçeneği belirtirseniz, hello ayrıntılı günlük eklenmiş toothat dosyasıdır.  

**Uygulanabilir:** BLOB'lar, dosyalar, tablolar

### <a name="zjournal-file-folder"></a>/ Z: [günlük dosyası klasörü]
Bir işlemi sürdürme bir günlük dosyası klasörü belirtir.

AzCopy her zaman bir işlem yarıda kesildi durumunda sürdürme destekler.

Bu seçenek belirtilmezse ya da bir klasör yolu belirtilen AzCopy hello günlük dosyası % LocalAppData%\Microsoft\Azure\AzCopy olan hello varsayılan konumda oluşturur.

Bir komut tooAzCopy sorun her zaman hello varsayılan klasöründe bir günlük dosyası var olup var veya bu seçeneği belirtilen bir klasörde varolup denetler. Her iki yerde Hello günlük dosyası mevcut değilse, AzCopy hello işlemi yeni olarak değerlendirir ve yeni bir günlük dosyası oluşturur.

Merhaba günlük dosyası mevcut değilse, AzCopy girdiğiniz hello komut satırı hello komut satırı hello günlük dosyasında eşleşip eşleşmediğini denetler. Merhaba iki komut satırları eşleşirse, AzCopy hello tamamlanmamış işlemi sürdürür. Bunlar eşleşmiyorsa, istendiğinde tooeither üzerine yaz hello günlük dosyası toostart yeni işlem ya da toocancel hello geçerli işlem demektir.

Merhaba günlük dosyası hello işlemi başarıyla tamamlandıktan sonra silinir.

AzCopy önceki bir sürümü tarafından oluşturulmuş bir günlük dosyasından bir işlemi sürdürme desteklenmediğini unutmayın.

**Uygulanabilir:** BLOB'lar, dosyalar, tablolar

### <a name="parameter-file"></a>/@:"Parameter-File"
Parametreleri içeren dosyayı belirtir. Merhaba komut satırında bunlar yalnızca belirtilmiş sanki AzCopy işlemleri hello dosyasındaki parametreleri hello.

Bir yanıt dosyası, tek bir satıra birden çok parametreleri belirtin veya kendi satırında her parametre belirtin. Tek bir parametre birden çok satıra yayılamaz unutmayın.

Yanıt dosyaları hello # sembolü ile başlayan açıklamaları çizgiler içerebilir.

Birden çok yanıt dosyaları belirtebilirsiniz. Ancak, AzCopy iç içe yanıt dosyaları desteklemiyor unutmayın.

**Uygulanabilir:** BLOB'lar, dosyalar, tablolar

### <a name="y"></a>/Y
Tüm AzCopy onay komut istemlerini bastırır.

**Uygulanabilir:** BLOB'lar, dosyalar, tablolar

### <a name="l"></a>/L
Yalnızca bir listeleme işlemi belirtir; hiçbir veri kopyalanır.

AzCopy yorumlar hello kullanan bu seçenek bu olmadan çalışan hello komut satırı için bir benzetimi olarak seçeneği /L ve kaç tane nesneleri kopyalanır, belirleyebileceğiniz sayılar aynı zaman toocheck hangi nesnelerin hello ayrıntılı günlüğüne kopyalanır hello adresindeki /V seçeneği.

Bu seçenek Hello davranışını da hello kaynak verilerin hello konumunu ve hello Özyinelemeli modu seçeneği/s ve dosya düzeni seçeneği /Pattern hello varlığını tarafından belirlenir.

AzCopy, bu seçenek kullanıldığında bu kaynak konumunun listesi ve okuma izni gerektirir.

**Uygulanabilir:** BLOB'ların, dosyaları

### <a name="mt"></a>/ MT
Merhaba indirilen dosyanın son değiştirilme zamanı toobe Merhaba, aynı, hello kaynak blob veya dosya ayarlar.

**Uygulanabilir:** BLOB'ların, dosyaları

### <a name="xn"></a>/XN
Daha yeni bir kaynak kaynak dışlar. Merhaba hello kaynağının son değişiklik zamanını hello aynı veya daha yeni hedef ise hello kaynak kopyalanmaz.

**Uygulanabilir:** BLOB'ların, dosyaları

### <a name="xo"></a>/XO
Eski bir kaynak kaynak dışlar. Merhaba hello kaynağının son değişiklik zamanını hello aynı ya da hedef daha eski ise hello kaynak kopyalanmaz.

**Uygulanabilir:** BLOB'ların, dosyaları

### <a name="a"></a>/A
Yalnızca hello arşiv özniteliği kümesine sahip dosyaları karşıya yükleme.

**Uygulanabilir:** BLOB'ların, dosyaları

### <a name="iarashcnetoi"></a>/ IA: [RASHCNETOI]
Belirtilen öznitelikler kümesi hello olan yüklemeler yalnızca dosyaları.

Mevcut öznitelikleri şunlardır:

* R Salt okunur dosyalar =
* Arşivlenmeye hazır dosyalar bir =
* S sistem dosyaları =
* H Gizli dosyalar =
* C Sıkıştırılmış dosyaları =
* N Normal dosyalar =
* E Şifrelenmiş dosyaları =
* T = geçici dosyalar
* O çevrimdışı dosyalar =
* I dosyaları olmayan dizini =

**Uygulanabilir:** BLOB'ların, dosyaları

### <a name="xarashcnetoi"></a>/ XA: [RASHCNETOI]
Belirtilen hello olan dosyaları dışlar öznitelikleri kümesi.

Mevcut öznitelikleri şunlardır:

* R Salt okunur dosyalar =
* Arşivlenmeye hazır dosyalar bir =
* S sistem dosyaları =
* H Gizli dosyalar =
* C Sıkıştırılmış dosyaları =
* N Normal dosyalar =
* E Şifrelenmiş dosyaları =
* T = geçici dosyalar
* O çevrimdışı dosyalar =
* I dosyaları olmayan dizini =

**Uygulanabilir:** BLOB'ların, dosyaları

### <a name="delimiterdelimiter"></a>/ Sınırlayıcı: "sınırlayıcı"
Bir blob adı toodelimit sanal dizinleri Hello sınırlayıcı karakter kullanılan gösterir.

Varsayılan olarak, AzCopy kullanır / hello sınırlayıcı karakter olarak. Ancak, ortak bir karakterle kullanarak AzCopy destekler (gibi @, # ya da %) ayırıcı olarak. Tooinclude hello komut satırında şu özel karakterleri birini gerekiyorsa, hello dosya adıyla çift tırnak içine alın.

Bu seçenek, yalnızca BLOB indirmek için geçerlidir.

**Uygulanabilir:** BLOB'ları

### <a name="ncnumber-of-concurrent-operations"></a>/ NC: "numarası-in-eşzamanlı-işlemler"
Merhaba eşzamanlı işlem sayısını belirtir.

AzCopy varsayılan olarak, belirli bir sayıda eşzamanlı işlem tooincrease hello veri aktarımı işleme başlatır. Çok sayıda eş zamanlı görevleri bir düşük bant genişlikli ortamında hello ağ bağlantısı doldurmaya ve tam olarak tamamlanmasını hello işlemlerini önlemek unutmayın. Eşzamanlı operasyonlar gerçek kullanılabilir ağ bant genişliğine bağlı kısıtlama.

eşzamanlı operasyonlar için üst sınır Hello 512'dir.

**Uygulanabilir:** BLOB'lar, dosyalar, tablolar

### <a name="sourcetypeblob--table"></a>/ Kaynak türü: "Blob" | "Tablo"
Bu hello belirtir `source` kaynaktır blob hello depolama öykünücüsünde çalıştıran hello yerel geliştirme ortamında kullanılabilir.

**Uygulanabilir:** BLOB'ların, tabloları

### <a name="desttypeblob--table"></a>/ DestType: "Blob" | "Tablo"
Bu hello belirtir `destination` kaynaktır blob hello depolama öykünücüsünde çalıştıran hello yerel geliştirme ortamında kullanılabilir.

**Uygulanabilir:** BLOB'ların, tabloları

### <a name="pkrskey1key2key3"></a>/ PKRS: "anahtar&#1;key2 anahtar&#3;..."
Bölmelerini hello dışa aktarma işlemi hello hızını artırır paralel tablo verileri dışarı aktarma bölüm anahtarı aralığının tooenable hello.

Bu seçenek belirtilmezse, AzCopy tek iş parçacığı tooexport tablo varlıkları kullanır. Örneğin, hello kullanıcı /PKRS belirtir: "aa #bb" sonra AzCopy üç eşzamanlı işlem başlatır.

Her işlem, aşağıda gösterildiği gibi üç bölüm anahtarı aralıkları, birini verir:

  [ilk bölüm anahtarı, aa)

  [aa, bb)

  [bb, son bölüm anahtarı]

**Uygulanabilir:** tabloları

### <a name="splitsizefile-size"></a>/ SplitSize: "dosya boyutu"
Dışarı aktarılan dosya boyutu (MB) bölme Merhaba, izin verilen minimum değer hello 32'dir belirtir.

Bu seçenek belirtilmezse, AzCopy tablo veri tooa tek dosyalı dışa aktarır.

Bu seçenek belirtilmezse bile hello tablo verileri dışarı aktarılan tooa blob ise ve hello dışarı aktarılan dosyayı blob boyutu hello 200 GB sınırını boyutu, AzCopy hello dışarı aktarılan dosyayı, böler.

**Uygulanabilir:** tabloları

### <a name="entityoperationinsertorskip--insertormerge--insertorreplace"></a>/ EntityOperation: "InsertOrSkip" | "InsertOrMerge" | "Yerleştir veya Değiştir"
Merhaba tablo veri alma davranışını belirtir.

* InsertOrSkip - var olan bir varlığı atlar veya hello tabloda mevcut değilse yeni bir varlık ekler.
* InsertOrMerge - var olan bir varlığı birleştirir veya hello tabloda mevcut değilse yeni bir varlık ekler.
* Yerleştir veya Değiştir - var olan bir varlığı değiştirir veya hello tabloda mevcut değilse yeni bir varlık ekler.

**Uygulanabilir:** tabloları

### <a name="manifestmanifest-file"></a>/ MANIFEST: "bildirim dosyası"
Merhaba tablo dışarı ve içeri aktarma işlemi için hello bildirim dosyası belirtir.

Merhaba dışa aktarma işlemi sırasında bu seçenek isteğe bağlıdır, bu seçenek belirtilmezse, AzCopy önceden tanımlanmış ada sahip bir bildirim dosyası oluşturur.

Bu seçenek, hello veri dosyalarını bulmak için hello içeri aktarma işlemi sırasında gereklidir.

**Uygulanabilir:** tabloları

### <a name="synccopy"></a>/ SyncCopy
Gösterir toosynchronously BLOB veya iki Azure Storage uç noktalar arasında dosyaları kopyalayın.

AzCopy varsayılan olarak, sunucu tarafı zaman uyumsuz kopyayı kullanır. Bu seçenek tooperform eş zamanlı belirtin, BLOB'ları yükler veya toolocal bellek dosyaları ve bunları tooAzure depolama yükler kopyalayın.

Blob storage, dosya depolama içinde veya Blob, depolama tooFile depolama veya bunun tersini de içinde dosya kopyalarken, bu seçeneği kullanabilirsiniz.

**Uygulanabilir:** BLOB'ların, dosyaları

### <a name="setcontenttypecontent-type"></a>/ SetContentType: "content-type"
Hedef BLOB'ları veya dosyaları için içerik Hello MIME türünü belirtir.

İçerik türü için bir blob hello veya tooapplication/octet-stream, varsayılan olarak dosya AzCopy kümeleri. Bu seçenek için bir değer açıkça belirterek hello içerik türü için tüm BLOB'ları veya dosyaları ayarlayabilirsiniz.

Bu seçenek olmadan bir değer belirtirseniz, AzCopy her bir blob veya dosyanın içerik türü dosya uzantısı tooits göre ayarlar.

**Uygulanabilir:** BLOB'ların, dosyaları

### <a name="payloadformatjson--csv"></a>/ PayloadFormat: "JSON" | "CSV"
Merhaba tablo dışarı aktarılan verileri dosyası Hello biçimini belirtir.

Bu seçenek belirtilmezse, varsayılan olarak AzCopy tablo veri dosyası JSON biçiminde dışa aktarır.

**Uygulanabilir:** tabloları

## <a name="known-issues-and-best-practices"></a>Bilinen sorunlar ve en iyi uygulamalar
### <a name="limit-concurrent-writes-while-copying-data"></a>Veri kopyalama sırasında sınırı eşzamanlı yazma
BLOB veya AzCopy dosyalarıyla kopyaladığınızda, bunu kopyalamaya çalışırken, başka bir uygulama hello veri değiştirme göz önünde bulundurun. Mümkünse, Kopyalamakta olduğunuz hello veri hello kopyalama işlemi sırasında değiştirilmeyen emin olun. Örneğin, bir Azure sanal makine ile ilişkili bir VHD'nin kopyalarken, başka bir uygulama şu anda toohello VHD yazıyorsanız emin olun. Bir en iyi yolu toodo bu hello kaynak toobe kiralama tarafından kopyalanır. Alternatif olarak, bir anlık görüntüsünü hello VHD ilk oluşturun ve sonra hello anlık görüntüsü kopyalayın.

Kopyalanan sonra hello süresi hello işi tarafından bittikten unutmayın ancak diğer uygulamaların tooblobs veya dosyaları yazma önleyemez, hello kopyalanan artık hello kaynak kaynaklarla tam eşlik kaynaklarınız olabilir.

### <a name="run-one-azcopy-instance-on-one-machine"></a>Bir Azcopy'i örnek bir makinede çalıştırın.
AzCopy, makine kaynak tooaccelerate hello veri aktarımı tasarlanmış toomaximize hello kullanımı, bir makinede yalnızca bir AzCopy çalıştırır ve hello seçeneğini belirtin öneririz `/NC` fazla eşzamanlı işlem gerekiyorsa. Daha fazla ayrıntı için yazın `AzCopy /?:NC` hello komut satırında.

### <a name="enable-fips-compliant-md5-algorithms-for-azcopy-when-you-use-fips-compliant-algorithms-for-encryption-hashing-and-signing"></a>FIPS uyumlu MD5 algoritmaları etkinleştirmek için AzCopy olduğunda, "kullanım FIPS uyumlu algoritmaları şifreleme, karma ve imzalama için".
AzCopy varsayılan .NET MD5 uygulama toocalculate hello MD5 nesneleri kopyalarken kullanır, ancak AzCopy tooenable FIPS uyumlu MD5 ayarı gereken bazı güvenlik gereksinimleri vardır.

Bir app.config dosyası oluşturabilirsiniz `AzCopy.exe.config` özelliğiyle `AzureStorageUseV1MD5` ve AzCopy.exe ile kenara yerleştirin.

    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
      <appSettings>
        <add key="AzureStorageUseV1MD5" value="false"/>
      </appSettings>
    </configuration>

Özelliği "AzureStorageUseV1MD5" • hello varsayılan değer, AzCopy .NET MD5 uygulama True - kullanır.
• Yanlış – AzCopy FIPS uyumlu MD5 algoritması kullanır.

Not FIPS uyumlu algoritmaları Windows makinenizde varsayılan olarak devre dışıdır, secpol.msc, Çalıştır penceresine yazın ve denetleme bu güvenlik ayarı anahtara -> yerel ilke güvenlik -> Seçenekler -> Sistem şifrelemesi: şifreleme, karma ve imzalama için kullan FIPS uyumlu algoritmaları.

## <a name="next-steps"></a>Sonraki adımlar
Azure Storage ve AzCopy hakkında daha fazla bilgi için kaynakları aşağıdaki hello bakın:

### <a name="azure-storage-documentation"></a>Azure Storage belgeleri:
* [Giriş tooAzure depolama](../storage-introduction.md)
* [Nasıl toouse Blob depolama alanından .NET](../blobs/storage-dotnet-how-to-use-blobs.md)
* [Nasıl toouse dosya depolama biriminden .NET](../storage-dotnet-how-to-use-files.md)
* [Nasıl toouse .NET tablo depolamasından](../../cosmos-db/table-storage-how-to-use-dotnet.md)
* [Nasıl toocreate, yönetme veya bir depolama hesabı silme](../storage-create-storage-account.md)
* [Linux'ta AzCopy ile veri aktarımı](storage-use-azcopy-linux.md)

### <a name="azure-storage-blog-posts"></a>Azure depolama blog gönderileri:
* [Azure Storage veri hareketi kitaplığı Önizleme Tanıtımı](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/)
* [AzCopy: zaman uyumlu kopyası ve özelleştirilmiş içerik türü tanışın](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/01/13/azcopy-introducing-synchronous-copy-and-customized-content-type.aspx)
* [AzCopy: Genel kullanılabilirlik, AzCopy 3.0 artı AzCopy 4.0 Önizleme sürümü tablo ve dosya desteği ile tanışın](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/10/29/azcopy-announcing-general-availability-of-azcopy-3-0-plus-preview-release-of-azcopy-4-0-with-table-and-file-support.aspx)
* [AzCopy: Büyük ölçekli kopyalama senaryoları için en iyi duruma getirilmiş](http://go.microsoft.com/fwlink/?LinkId=507682)
* [AzCopy: Coğrafi olarak yedekli depolamaya okuma erişimi desteği](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/04/07/azcopy-support-for-read-access-geo-redundant-account.aspx)
* [AzCopy: yeniden başlatılabilir modu ve SAS belirteci ile veri aktarımı](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/09/07/azcopy-transfer-data-with-re-startable-mode-and-sas-token.aspx)
* [AzCopy: arası hesap kopyalama Blob kullanma](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/04/01/azcopy-using-cross-account-copy-blob.aspx)
* [AzCopy: Azure BLOB'ları karşıya yükleme ve indirme dosyaları](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx)

