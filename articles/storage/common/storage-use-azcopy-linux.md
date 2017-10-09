---
title: "aaaCopy veya taşıma veri tooAzure Storage ile AzCopy Linux'ta | Microsoft Docs"
description: "Merhaba AzCopy blob ve dosya içerikten Linux yardımcı programı toomove veya kopya veri tooor kullanın. Yerel dosyalarından veri tooAzure depolama kopyalayın veya içinde veya depolama hesapları arasında veri kopyalayın. Kolayca, veri tooAzure depolama geçirin."
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
ms.date: 05/11/2017
ms.author: seguler
ms.openlocfilehash: ee39c311d996a046999b7fd4a4eb873f25b4eb86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="transfer-data-with-azcopy-on-linux"></a>Linux'ta AzCopy ile veri aktarımı
Linux üzerinde AzCopy en uygun performans ile basit komutları kullanarak Microsoft Azure Blob ve dosya depolama biriminden veri tooand kopyalanması için tasarlanmış bir komut satırı yardımcı programıdır. Bir nesne tooanother veri depolama hesabınızda veya depolama hesapları arasında kopyalayabilirsiniz.

İndirebilirsiniz AzCopy iki sürümü vardır. Linux üzerinde AzCopy .NET Core POSIX stili komut satırı seçenekleri sunan Linux platformlar hedefler Framework ile yerleşik olarak bulunur. [AzCopy Windows](../storage-use-azcopy.md) .NET Framework ile oluşturulan ve Windows stili komut satırı seçenekleri sunar. Bu makalede, AzCopy Linux üzerinde yer almaktadır.

## <a name="download-and-install-azcopy"></a>AzCopy yükleyip
### <a name="installation-on-linux"></a>Linux üzerinde yükleme

AzCopy Linux'ta hello platformunda .NET Core framework gerektirir. Merhaba üzerinde Hello yükleme yönergelerine bakın [.NET Core](https://www.microsoft.com/net/core#linuxubuntu) sayfası.

Örnek olarak, .NET Core üzerinde Ubuntu 16.10 şimdi yükleyin. Merhaba son yükleme kılavuzu için ziyaret [.NET Core Linux'ta](https://www.microsoft.com/net/core#linuxubuntu) yükleme sayfası.


```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ yakkety main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
sudo apt-get update
sudo apt-get install dotnet-dev-1.0.3
```

.NET Core yüklendiğinde, indirin ve AzCopy yükleyin.

```bash
wget -O azcopy.tar.gz https://aka.ms/downloadazcopyprlinux
tar -xf azcopy.tar.gz
sudo ./install.sh
```

AzCopy Linux'ta yüklendikten sonra ayıklanan hello dosyalarını kaldırabilirsiniz. Süper kullanıcı ayrıcalıkları yoksa, alternatif olarak, aynı zamanda hello Kabuk komut dosyasını kullanarak AzCopy 'azcopy' hello ayıklanan klasöründe çalıştırabilirsiniz. 

### <a name="alternative-installation-on-ubuntu"></a>Ubuntu alternatif yükleme

**Ubuntu 14.04**

.Net için apt kaynağı Ekle Çekirdek:

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ trusty main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

Microsoft Linux ürün depo apt kaynağı ekleyin ve AzCopy yükleyin:

```bash
curl https://packages.microsoft.com/config/ubuntu/14.04/prod.list > ./microsoft-prod.list
sudo cp ./microsoft-prod.list /etc/apt/sources.list.d/
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo cp ./microsoft.gpg /etc/apt/trusted.gpg.d/
```

```bash
sudo apt-get update
sudo apt-get install azcopy
```

**Ubuntu 16.04**

.Net için apt kaynağı Ekle Çekirdek:

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ xenial main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

Microsoft Linux ürün depo apt kaynağı ekleyin ve AzCopy yükleyin:

```bash
curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list > ./microsoft-prod.list
sudo cp ./microsoft-prod.list /etc/apt/sources.list.d/
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo cp ./microsoft.gpg /etc/apt/trusted.gpg.d/
```

```bash
sudo apt-get update
sudo apt-get install azcopy
```

**Ubuntu 16.10**

.Net için apt kaynağı Ekle Çekirdek:

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ yakkety main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

Microsoft Linux ürün depo apt kaynağı ekleyin ve AzCopy yükleyin:

```bash
curl https://packages.microsoft.com/config/ubuntu/16.10/prod.list > ./microsoft-prod.list
sudo cp ./microsoft-prod.list /etc/apt/sources.list.d/
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo cp ./microsoft.gpg /etc/apt/trusted.gpg.d/
```

```bash
sudo apt-get update
sudo apt-get install azcopy
```

## <a name="writing-your-first-azcopy-command"></a>İlk AzCopy komut yazma
AzCopy komutları Hello temel sözdizimi şöyledir:

```azcopy
azcopy --source <source> --destination <destination> [Options]
```

Örnek hello veri tooand Microsoft Azure BLOB'ları ve dosyalarından kopyalamak için çeşitli senaryolar gösterilmektedir. Toohello başvuran `azcopy --help` her örnekte kullanılan hello parametrelerinin ayrıntılı bir açıklama için menüsü.

## <a name="blob-download"></a>BLOB: karşıdan yükle
### <a name="download-single-blob"></a>Tek blob indirin

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

Varsa hello klasörü `/mnt/myfiles` yok, AzCopy oluşturur ve indirir `abc.txt ` hello yeni klasöre.

### <a name="download-single-blob-from-secondary-region"></a>Tek blob ikincil bölge ' indirin

```azcopy
azcopy \
    --source https://myaccount-secondary.blob.core.windows.net/mynewcontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

Okuma erişimli coğrafi olarak yedekli depolama etkin olması gerektiğini unutmayın.

### <a name="download-all-blobs"></a>Tüm BLOB'ları indirme

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --recursive
```

Merhaba aşağıdaki varsayın BLOB'lar hello belirtilen kapsayıcısında bulunur:  

```
abc.txt
abc1.txt
abc2.txt
vd1/a.txt
vd1/abcd.txt
```

Merhaba yükleme işleminden sonra dizin hello `/mnt/myfiles` hello aşağıdaki dosyaları içerir:

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/vd1/a.txt
/mnt/myfiles/vd1/abcd.txt
```

Seçeneği belirtmezseniz, `--recursive`, hiçbir blob indirilir.

### <a name="download-blobs-with-specified-prefix"></a>BLOB'lar ile belirtilen bir önek indirin

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "a" \
    --recursive
```

Merhaba aşağıdaki varsayın BLOB'lar hello belirtilen kapsayıcısında bulunur. Merhaba önek ile başlayan tüm BLOB'lar `a` indirilir.

```
abc.txt
abc1.txt
abc2.txt
xyz.txt
vd1\a.txt
vd1\abcd.txt
```

Merhaba yükleme işleminden sonra klasörü hello `/mnt/myfiles` hello aşağıdaki dosyaları içerir:

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
```

Merhaba önek hello blob adı ilk kısmı hello forms toohello sanal dizini uygular. Yukarıda gösterilen hello örnekte hiçbir blob indirilen şekilde hello sanal dizin hello Belirtilen önek, eşleşmiyor. Merhaba, ayrıca, seçenek `--recursive` belirtilmezse, AzCopy BLOB indirmek değil.

### <a name="set-hello-last-modified-time-of-exported-files-toobe-same-as-hello-source-blobs"></a>Dışa aktarılan dosyaları toobe hello son değişiklik saatini ayarlayın kaynak BLOB'ları hello aynı

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination "/mnt/myfiles" \
    --source-key <key> \
    --preserve-last-modified-time
```

Son değiştiren bunların zamana dayalı hello indirme işlemi de BLOB'lar hariç tutabilirsiniz. Tooexclude BLOB'lar, son değişiklik zamanını hello aynı ya da hello hedef dosya daha yeni olan isterseniz, örneğin, hello ekleyin `--exclude-newer` seçeneği:

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --preserve-last-modified-time \
    --exclude-newer
```

Veya, son değişiklik zamanını hello aynı ya da hello hedef dosyanın daha eski olan tooexclude BLOB'ları istiyorsanız hello ekleyin `--exclude-older` seçeneği:

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --preserve-last-modified-time \
    --exclude-older
```

## <a name="blob-upload"></a>BLOB: karşıya yükle
### <a name="upload-single-file"></a>Tek dosya karşıya yükleme

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "abc.txt"
```

Merhaba belirtilen hedef kapsayıcı mevcut değilse, AzCopy oluşturur ve karşıya dosya içine hello.

### <a name="upload-single-file-toovirtual-directory"></a>Tek dosya toovirtual dizin karşıya yükle

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "abc.txt"
```

Merhaba belirtilen sanal dizin yok, AzCopy hello dosya tooinclude hello sanal dizinde hello blob adı yükler (*örneğin*, `vd/abc.txt` yukarıdaki hello örnekteki).

### <a name="upload-all-files"></a>Tüm dosyaları karşıya yükleme

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --recursive
```

Seçeneğini belirterek `--recursive` hello yüklemeleri Merhaba içeriğine belirtilen dizin tooBlob depolama yinelemeli olarak tüm alt klasörleri ve bunların dosyaları da karşıya anlamına gelir. Örneği için hello aşağıdaki varsayın dosyaları klasöründe bulunan `/mnt/myfiles`:

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/subfolder/a.txt
/mnt/myfiles/subfolder/abcd.txt
```

Merhaba karşıya yükleme işleminden sonra aşağıdaki dosyaları hello hello kapsayıcı içerir:

```
abc.txt
abc1.txt
abc2.txt
subfolder/a.txt
subfolder/abcd.txt
```

Seçenek'ne zaman hello `--recursive` hello aşağıdaki üç dosyayı karşıya yalnızca, belirtilmedi:

```
abc.txt
abc1.txt
abc2.txt
```

### <a name="upload-files-matching-specified-pattern"></a>Belirtilen desenle eşleşen dosyaları karşıya yükleme

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "a*" \
    --recursive
```

Merhaba aşağıdaki varsayın dosyaları klasöründe bulunan `/mnt/myfiles`:

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/xyz.txt
/mnt/myfiles/subfolder/a.txt
/mnt/myfiles/subfolder/abcd.txt
```

Merhaba karşıya yükleme işleminden sonra aşağıdaki dosyaları hello hello kapsayıcı içerir:

```
abc.txt
abc1.txt
abc2.txt
subfolder/a.txt
subfolder/abcd.txt
```

Seçenek'ne zaman hello `--recursive` belirtilmezse, AzCopy atlar alt dizinlerde olan dosyaları:

```
abc.txt
abc1.txt
abc2.txt
```

### <a name="specify-hello-mime-content-type-of-a-destination-blob"></a>Hedef BLOB Hello MIME içerik türünü belirtin
Çok hedef blob hello içerik türü varsayılan olarak, AzCopy ayarlar`application/octet-stream`. Ancak, açıkça hello seçeneği aracılığıyla hello içerik türünü belirtebilirsiniz `--set-content-type [content-type]`. Bu sözdiziminin hello içerik türü için tüm BLOB'ları bir karşıya yükleme işleminde ayarlar.

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/myContainer/ \
    --dest-key <key> \
    --include "ab" \
    --set-content-type "video/mp4"
```

Merhaba, seçenek `--set-content-type` AzCopy her bir dosya veya blob ayarlar sonra bir değer belirtilirse kullanıcının içerik türünü according tooits dosya uzantısı.

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/myContainer/ \
    --dest-key <key> \
    --include "ab" \
    --set-content-type
```

## <a name="blob-copy"></a>BLOB: kopyalama
### <a name="copy-single-blob-within-storage-account"></a>Depolama hesabı içinde tek blob kopyalama

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1 \
    --destination https://myaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key> \
    --dest-key <key> \
    --include "abc.txt"
```

Bir blob--eşitleme kopyalama seçeneği olmadan kopyaladığınızda bir [sunucu tarafı kopyası](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) işlemi gerçekleştirilir.

### <a name="copy-single-blob-across-storage-accounts"></a>Tek blob depolama hesapları arasında kopyalama

```azcopy
azcopy \
    --source https://sourceaccount.blob.core.windows.net/mycontainer1 \
    --destination https://destaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt"
```

Bir blob--eşitleme kopyalama seçeneği olmadan kopyaladığınızda bir [sunucu tarafı kopyası](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) işlemi gerçekleştirilir.

### <a name="copy-single-blob-from-secondary-region-tooprimary-region"></a>İkincil bölge tooprimary bölgesinden tek blob kopyalama

```azcopy
azcopy \
    --source https://myaccount1-secondary.blob.core.windows.net/mynewcontainer1 \
    --destination https://myaccount2.blob.core.windows.net/mynewcontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt"
```

Okuma erişimli coğrafi olarak yedekli depolama etkin olması gerektiğini unutmayın.

### <a name="copy-single-blob-and-its-snapshots-across-storage-accounts"></a>Depolama hesapları arasında tek blob ve onun anlık görüntüleri kopyalama

```azcopy
azcopy \
    --source https://sourceaccount.blob.core.windows.net/mycontainer1 \
    --destination https://destaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt" \
    --include-snapshot
```

Hello kopyalama işleminden sonra hello hedef kapsayıcı hello blob ve onun anlık görüntülerini içerir. Merhaba kapsayıcı hello aşağıdakileri içeren blob ve onun anlık görüntüler:

```
abc.txt
abc (2013-02-25 080757).txt
abc (2014-02-21 150331).txt
```

### <a name="synchronously-copy-blobs-across-storage-accounts"></a>Zaman uyumlu olarak depolama hesapları arasında BLOB kopyalama
AzCopy varsayılan olarak, iki depolama uç noktaları arasında verileri zaman uyumsuz olarak kopyalar. Bu nedenle, hiçbir SLA ne kadar hızlı blob bakımından sahip yedek bant genişliğini kapasite kullanarak hello arka planda hello kopyalama işlemi çalıştırır kopyalanır. 

Merhaba `--sync-copy` seçeneği sağlar hello kopyalama işlemi tutarlı hızı alır. AzCopy hello BLOB'lar yükleyerek hello zaman uyumlu kopyası gerçekleştirir toocopy hello öğesinden belirtilen kaynak toolocal bellek ve ardından toohello Blob Depolama Hedef karşıya yükleme.

```azcopy
azcopy \
    --source https://myaccount1.blob.core.windows.net/myContainer/ \
    --destination https://myaccount2.blob.core.windows.net/myContainer/ \
    --source-key <key1> \
    --dest-key <key2> \
    --include "ab" \
    --sync-copy
```

`--sync-copy`Ek çıkış karşılaştırıldığında maliyet tooasynchronous kopya oluşturabilir. Önerilen yaklaşımı hello toouse hello olan Azure VM'deki, bu seçenek olan aynı bölgede kaynak depolama hesabı tooavoid çıkışı maliyeti.

## <a name="file-download"></a>Dosya: karşıdan yükle
### <a name="download-single-file"></a>Tek dosya indirme

```azcopy
azcopy \
    --source https://myaccount.file.core.windows.net/myfileshare/myfolder1/ \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

Merhaba kaynağıdır Azure dosya paylaşımının, sonra da hello tam dosya adı belirtmelisiniz belirtilmişse (*örneğin* `abc.txt`) toodownload tek bir dosya veya seçeneğini belirtin `--recursive` toodownload tüm dosyaları hello paylaşımı yinelemeli olarak. Bir dosya düzeni ve seçenek toospecify çalışırken `--recursive` birlikte hatayla sonuçlanır.

### <a name="download-all-files"></a>Tüm dosyaları indirme

```azcopy
azcopy \
    --source https://myaccount.file.core.windows.net/myfileshare/ \
    --destination /mnt/myfiles \
    --source-key <key> \
    --recursive
```

Boş klasörleri indirilmez unutmayın.

## <a name="file-upload"></a>Dosya: karşıya yükle
### <a name="upload-single-file"></a>Tek dosya karşıya yükleme

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --include abc.txt
```

### <a name="upload-all-files"></a>Tüm dosyaları karşıya yükleme

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --recursive
```

Boş klasörleri değil karşıya unutmayın.

### <a name="upload-files-matching-specified-pattern"></a>Belirtilen desenle eşleşen dosyaları karşıya yükleme

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --include "ab*" \
    --recursive
```

## <a name="file-copy"></a>Dosya: kopyalama
### <a name="copy-across-file-shares"></a>Dosya paylaşımlarında kopyalayın

```azcopy
azcopy \
    --source https://myaccount1.file.core.windows.net/myfileshare1/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare2/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
Dosya paylaşımlarında bir dosya kopyaladığınızda bir [sunucu tarafı kopyası](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) işlemi gerçekleştirilir.

### <a name="copy-from-file-share-tooblob"></a>Dosya Paylaşımı tooblob kopyalayın

```azcopy
azcopy \ 
    --source https://myaccount1.file.core.windows.net/myfileshare/ \
    --destination https://myaccount2.blob.core.windows.net/mycontainer/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
Dosya Paylaşımı tooblob bir dosya kopyaladığınızda bir [sunucu tarafı kopyası](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) işlemi gerçekleştirilir.

### <a name="copy-from-blob-toofile-share"></a>BLOB toofile paylaşımından kopyalayın

```azcopy
azcopy \
    --source https://myaccount1.blob.core.windows.net/mycontainer/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
Blob toofile paylaşımından bir dosya kopyaladığınızda bir [sunucu tarafı kopyası](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) işlemi gerçekleştirilir.

### <a name="synchronously-copy-files"></a>Zaman uyumlu olarak dosyaları kopyalayın
Merhaba belirtebilirsiniz `--sync-copy` toocopy veri dosya depolama tooFile depolama, File Storage tooBlob depolama ve Blob Depolama tooFile depolama zaman uyumlu olarak seçeneği. AzCopy bu işlemi hello kaynak veri toolocal bellek indiriliyor ve toodestination karşıya yükleme çalıştırır. Bu durumda, standart çıkış maliyet geçerlidir.

```azcopy
azcopy \
    --source https://myaccount1.file.core.windows.net/myfileshare1/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare2/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive \
    --sync-copy
```

Dosya depolama tooBlob depolama kopyalarken hello varsayılan blob türü blok blobu, kullanıcı seçeneği belirtebilirsiniz `/BlobType:page` toochange hello hedef blob türü.

Unutmayın `--sync-copy` karşılaştırma tooasynchronous kopyalama maliyet ek çıkış oluşturabilir. Önerilen yaklaşımı hello toouse hello olan Azure VM'deki, bu seçenek olan aynı bölgede kaynak depolama hesabı tooavoid çıkışı maliyeti.

## <a name="other-azcopy-features"></a>Diğer AzCopy özellikleri
### <a name="only-copy-data-that-doesnt-exist-in-hello-destination"></a>Merhaba hedefte mevcut olmayan veri Kopyala
Merhaba `--exclude-older` ve `--exclude-newer` parametreler, sırasıyla kopyalanmasını tooexclude daha eski veya yeni kaynak kaynakları sağlar. Merhaba hedef yoksa toocopy kaynak kaynakları yalnızca istiyorsanız, her iki parametre hello AzCopy komut belirtebilirsiniz:

    --source http://myaccount.blob.core.windows.net/mycontainer --destination /mnt/myfiles --source-key <sourcekey> --recursive --exclude-older --exclude-newer

    --source /mnt/myfiles --destination http://myaccount.file.core.windows.net/myfileshare --dest-key <destkey> --recursive --exclude-older --exclude-newer

    --source http://myaccount.blob.core.windows.net/mycontainer --destination http://myaccount.blob.core.windows.net/mycontainer1 --source-key <sourcekey> --dest-key <destkey> --recursive --exclude-older --exclude-newer

### <a name="use-a-configuration-file-toospecify-command-line-parameters"></a>Bir yapılandırma dosyası toospecify komut satırı parametreleri kullanma

```azcopy
azcopy --config-file "azcopy-config.ini"
```

AzCopy komut satırı parametreleri herhangi bir yapılandırma dosyası içerebilir. Merhaba komut satırında bir hello içeriğiyle doğrudan değiştirme hello dosyasının gerçekleştirme belirtilmiş sanki AzCopy işlemleri hello dosyasındaki parametreleri hello.

Adlı bir yapılandırma dosyası varsayın `copyoperation`, satırlardan hello içerir. Tek bir satıra her AzCopy parametresi belirtilebilir.

    --source http://myaccount.blob.core.windows.net/mycontainer --destination /mnt/myfiles --source-key <sourcekey> --recursive --quiet

veya satırları ayrı:

    --source http://myaccount.blob.core.windows.net/mycontainer
    --destination /mnt/myfiles
    --source-key<sourcekey>
    --recursive
    --quiet

AzCopy, iki hattında hello parametre bölerseniz hello için aşağıda gösterildiği gibi başarısız `--source-key` parametre:

    http://myaccount.blob.core.windows.net/mycontainer
    /mnt/myfiles
    --sourcekey
    <sourcekey>
    --recursive
    --quiet

### <a name="specify-a-shared-access-signature-sas"></a>Paylaşılan erişim imzası (SAS) belirtin

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1 \
    --destination https://myaccount.blob.core.windows.net/mycontainer2 \
    --source-sas <SAS1> \
    --dest-sas <SAS2> \
    --include abc.txt
```

Ayrıca, bir SAS hello kapsayıcı URI belirtebilirsiniz:

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1/?SourceSASToken \
    --destination /mnt/myfiles \
    --recursive
```

AzCopy şu anda yalnızca hello desteklediğini unutmayın [hesap SAS](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-shared-access-signature-part-1).

### <a name="journal-file-folder"></a>Günlük dosyası klasörü
Bir komut tooAzCopy sorun her zaman hello varsayılan klasöründe bir günlük dosyası var olup var veya bu seçeneği belirtilen bir klasörde varolup denetler. Her iki yerde Hello günlük dosyası mevcut değilse, AzCopy hello işlemi yeni olarak değerlendirir ve yeni bir günlük dosyası oluşturur.

Merhaba günlük dosyası mevcut değilse, AzCopy girdiğiniz hello komut satırı hello komut satırı hello günlük dosyasında eşleşip eşleşmediğini denetler. Merhaba iki komut satırları eşleşirse, AzCopy hello tamamlanmamış işlemi sürdürür. Bunlar eşleşmiyorsa AzCopy kullanıcı tooeither üzerine yaz hello günlük dosyası toostart yeni işlem ya da toocancel hello geçerli işlem ister.

Merhaba günlük dosyası için toouse hello varsayılan konum istiyorsanız:

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --resume
```

Seçeneği unutursanız `--resume`, veya seçeneğini belirtin `--resume` hello klasör yolu, yukarıda gösterildiği gibi AzCopy hello günlük dosyası olan hello varsayılan konumda, oluşturur `~\Microsoft\Azure\AzCopy`. Merhaba günlük dosyası zaten varsa, AzCopy hello günlük dosyasına dayalı hello işlemi sürdürür.

Toospecify hello günlük dosyası için özel bir konum istiyorsanız:

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key key \
    --resume "/mnt/myjournal"
```

Bu örnek, zaten yoksa, hello günlük dosyası oluşturur. Mevcut değilse, AzCopy hello günlük dosyasına dayalı hello işlemi sürdürür.

Tooresume AzCopy işlemi istiyorsanız yineleyin hello aynı komutu. AzCopy sonra Linux'ta onay ister:

```azcopy
Incomplete operation with same command line detected at hello journal directory "/home/myaccount/Microsoft/Azure/AzCopy", do you want tooresume hello operation? Choose Yes tooresume, choose No toooverwrite hello journal toostart a new operation. (Yes/No)
```

### <a name="output-verbose-logs"></a>Çıktı ayrıntılı günlükleri

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --verbose
```

### <a name="specify-hello-number-of-concurrent-operations-toostart"></a>Eşzamanlı operasyonlar toostart Hello sayısını belirtin
Seçenek `--parallel-level` eşzamanlı kopyalama işlemleri hello sayısını belirtir. Varsayılan olarak, belirli bir sayıda eşzamanlı işlem tooincrease hello veri aktarımı işleme AzCopy başlatır. eşzamanlı operasyonlar Hello sayısı eşittir sekiz katı hello elinizde işlemci sayısı. Düşük bant genişlikli ağ üzerinden AzCopy çalıştırıyorsanız, daha düşük bir sayı için--kaynak rekabet tarafından nedeniyle paralel düzeyi tooavoid hatası belirtebilirsiniz.

[!TIP]
>tooview hello tam listesi 'azcopy--Yardım' AzCopy parametrelerinin denetleyin menüsü.

## <a name="known-issues-and-best-practices"></a>Bilinen sorunlar ve en iyi uygulamalar
### <a name="error-net-core-is-not-found-in-hello-system"></a>Hata: .NET Core hello sistemde bulunamadı.
.NET Core hello sistemde yüklü olmadığını belirten bir hatayla karşılaşırsanız, yol toohello .NET Core ikili hello `dotnet` eksik olabilir.

İçinde bu sorunu tooaddress sipariş, hello .NET Core ikili hello sistemde bulunamadı:
```bash
sudo find / -name dotnet
```

Bu, hello yolu toohello dotnet ikili döndürür. 

    /opt/rh/rh-dotnetcore11/root/usr/bin/dotnet
    /opt/rh/rh-dotnetcore11/root/usr/lib64/dotnetcore/dotnet
    /opt/rh/rh-dotnetcore11/root/usr/lib64/dotnetcore/shared/Microsoft.NETCore.App/1.1.2/dotnet

Şimdi bu yolu toohello PATH değişkeni ekleyin. Sudo için secure_path toocontain hello yolu toohello dotnet ikili düzenleyin:
```bash 
sudo visudo
### Append hello path found in hello preceding example too'secure_path' variable
```

Bu örnekte, secure_path değişken olarak okur:

```
secure_path = /sbin:/bin:/usr/sbin:/usr/bin:/opt/rh/rh-dotnetcore11/root/usr/bin/
```

Merhaba geçerli kullanıcı için.bash_profile/.profile tooinclude hello yolu toohello dotnet PATH değişkeni ikili düzenleme 
```bash
vi ~/.bash_profile
### Append hello path found in hello preceding example too'PATH' variable
```

.NET Core şimdi yolunda olduğundan emin olun:
```bash
which dotnet
sudo which dotnet
```

### <a name="error-installing-azcopy"></a>AzCopy yükleme hatası
AzCopy yükleme ile ilgili sorunlarla karşılaşırsanız, AzCopy hello hello bash betik kullanarak ayıklanan toorun deneyebilirsiniz `azcopy` klasör.

```bash
cd azcopy
./azcopy
```

### <a name="limit-concurrent-writes-while-copying-data"></a>Veri kopyalama sırasında sınırı eşzamanlı yazma
BLOB veya AzCopy dosyalarıyla kopyaladığınızda, bunu kopyalamaya çalışırken, başka bir uygulama hello veri değiştirme göz önünde bulundurun. Mümkünse, Kopyalamakta olduğunuz hello veri hello kopyalama işlemi sırasında değiştirilmeyen emin olun. Örneğin, bir Azure sanal makine ile ilişkili bir VHD'nin kopyalarken, başka bir uygulama şu anda toohello VHD yazıyorsanız emin olun. Bir en iyi yolu toodo bu hello kaynak toobe kiralama tarafından kopyalanır. Alternatif olarak, bir anlık görüntüsünü hello VHD ilk oluşturun ve sonra hello anlık görüntüsü kopyalayın.

Kopyalanan sonra hello süresi hello işi tarafından bittikten unutmayın ancak diğer uygulamaların tooblobs veya dosyaları yazma önleyemez, hello kopyalanan artık hello kaynak kaynaklarla tam eşlik kaynaklarınız olabilir.

### <a name="run-one-azcopy-instance-on-one-machine"></a>Bir Azcopy'i örnek bir makinede çalıştırın.
AzCopy, makine kaynak tooaccelerate hello veri aktarımı tasarlanmış toomaximize hello kullanımı, bir makinede yalnızca bir AzCopy çalıştırır ve hello seçeneğini belirtin öneririz `--parallel-level` fazla eşzamanlı işlem gerekiyorsa. Daha fazla ayrıntı için yazın `AzCopy --help parallel-level` hello komut satırında.

## <a name="next-steps"></a>Sonraki adımlar
Azure Storage ve AzCopy hakkında daha fazla bilgi için kaynakları aşağıdaki hello bakın:

### <a name="azure-storage-documentation"></a>Azure Storage belgeleri:
* [Giriş tooAzure depolama](../storage-introduction.md)
* [Depolama hesabı oluşturma](../storage-create-storage-account.md)
* [BLOB Depolama Gezgini ile yönetme](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-explorer-blobs)
* [Hello Azure CLI 2.0 Azure Storage ile kullanma](../storage-azure-cli.md)
* [Nasıl toouse Blob depolama alanından C++](../blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [Nasıl toouse Java'dan Blob storage](../blobs/storage-java-how-to-use-blob-storage.md)
* [Nasıl toouse node.js'den Blob storage](../blobs/storage-nodejs-how-to-use-blob-storage.md)
* [Nasıl toouse python'dan Blob storage](../blobs/storage-python-how-to-use-blob-storage.md)

### <a name="azure-storage-blog-posts"></a>Azure depolama blog gönderileri:
* [AzCopy Linux preview'daki tanışın](https://azure.microsoft.com/en-in/blog/announcing-azcopy-on-linux-preview/)
* [Azure Storage veri hareketi kitaplığı Önizleme Tanıtımı](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/)
* [AzCopy: zaman uyumlu kopyası ve özelleştirilmiş içerik türü tanışın](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/01/13/azcopy-introducing-synchronous-copy-and-customized-content-type.aspx)
* [AzCopy: Genel kullanılabilirlik, AzCopy 3.0 artı AzCopy 4.0 Önizleme sürümü tablo ve dosya desteği ile tanışın](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/10/29/azcopy-announcing-general-availability-of-azcopy-3-0-plus-preview-release-of-azcopy-4-0-with-table-and-file-support.aspx)
* [AzCopy: Büyük ölçekli kopyalama senaryoları için en iyi duruma getirilmiş](http://go.microsoft.com/fwlink/?LinkId=507682)
* [AzCopy: Coğrafi olarak yedekli depolamaya okuma erişimi desteği](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/04/07/azcopy-support-for-read-access-geo-redundant-account.aspx)
* [AzCopy: yeniden başlatılabilir modu ve SAS belirteci ile veri aktarımı](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/09/07/azcopy-transfer-data-with-re-startable-mode-and-sas-token.aspx)
* [AzCopy: arası hesap kopyalama Blob kullanma](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/04/01/azcopy-using-cross-account-copy-blob.aspx)
* [AzCopy: Azure BLOB'ları karşıya yükleme ve indirme dosyaları](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx)

