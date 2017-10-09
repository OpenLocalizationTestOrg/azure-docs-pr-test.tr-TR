---
title: "aaaSample iş akışı tooprep sabit sürücüler için bir Azure içeri/dışarı aktarma alma işi | Microsoft Docs"
description: "Sürücüleri hello Azure içeri/dışarı aktarma hizmeti, bir içeri aktarma işi hazırlama hello tam işlemi için bkz."
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
ms.date: 04/07/2017
ms.author: muralikk
ms.openlocfilehash: 560220b7dc9f87416f1fec1ff30fa5cd65812ce5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sample-workflow-tooprepare-hard-drives-for-an-import-job"></a>Örnek iş akışı tooprepare sabit sürücüler içeri aktarma işi için

Bu makalede, sürücüler için içeri aktarma işi hazırlama hello tam işlemi açıklanmaktadır.

## <a name="sample-data"></a>Örnek veriler

Bu örnek veri adlı bir Azure storage hesabınıza aşağıdaki hello alır `mystorageaccount`:

|Konum|Açıklama|Veri boyutu|
|--------------|-----------------|-----|
|H:\Video\ |Videolar koleksiyonu|12 TB|
|H:\Photo\ |Fotoğraf koleksiyonu|30 GB|
|K:\Temp\FavoriteMovie.ISO|A Blu-ray™ disk görüntüsü|25 GB|
|\\\bigshare\john\music\|Müzik dosyalarını bir ağ paylaşımına koleksiyonu|10 GB|

## <a name="storage-account-destinations"></a>Depolama hesabı hedefleri

Merhaba alma işi hello depolama hesabındaki hedeflerini izleyerek hello hello veri aktarmak:

|Kaynak|Hedef sanal dizin veya blob|
|------------|-------------------------------------------|
|H:\Video\ |Video /|
|H:\Photo\ |Fotoğraf /|
|K:\Temp\FavoriteMovie.ISO|favorite/FavoriteMovies.ISO|
|\\\bigshare\john\music\ |Müzik|

Bu eşleme ile dosya hello `H:\Video\Drama\GreatMovie.mov` alınan toohello blob olacaktır `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.

## <a name="determine-hard-drive-requirements"></a>Sabit sürücü gereksinimlerini belirleyin

Ardından, toodetermine işlem hello hello verilerin boyutunu kaç sabit sürücüler gerekli değildir:

`12TB + 30GB + 25GB + 10GB = 12TB + 65GB`

Bu örnekte, iki 8TB sabit sürücü yeterli olacaktır. Ancak, hello kaynak dizin itibaren `H:\Video` 12 TB'lık veriyi varsa ve yalnızca 8 TB, tek sabit diskin kapasitesini mümkün toospecify bu olacaktır hello hello şekilde aşağıdaki **driveset.csv** dosya:

```
DriveLetter,FormatOption,SilentOrPromptOnFormat,Encryption,ExistingBitLockerKey
X,Format,SilentMode,Encrypt,
Y,Format,SilentMode,Encrypt,
```
Merhaba aracı en iyi duruma getirilmiş bir şekilde iki sabit sürücüde veri dağıtın.

## <a name="attach-drives-and-configure-hello-job"></a>Sürücüleri bağlayın ve hello iş yapılandırın
Her iki diskleri toohello makine ekleme ve birimler oluşturabilir. Ardından Yazar **dataset.csv** dosyası:
```
BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
H:\Video\,video/,BlockBlob,rename,None,H:\mydirectory\properties.xml
H:\Photo\,photo/,BlockBlob,rename,None,H:\mydirectory\properties.xml
K:\Temp\FavoriteVideo.ISO,favorite/FavoriteVideo.ISO,BlockBlob,rename,None,H:\mydirectory\properties.xml
\\myshare\john\music\,music/,BlockBlob,rename,None,H:\mydirectory\properties.xml
```

Ayrıca, tüm dosyalar için meta veriler aşağıdaki hello ayarlayabilirsiniz:

* **UploadMethod:** Windows Azure içeri/dışarı aktarma hizmeti
* **DataSetName:** SampleData
* **CreationDate:** 1/10/2013

tooset meta verileri içe hello dosyaları için bir metin dosyası oluşturma `c:\WAImportExport\SampleMetadata.txt`, içeriği aşağıdaki hello ile:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Metadata>
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>
    <DataSetName>SampleData</DataSetName>
    <CreationDate>10/1/2013</CreationDate>
</Metadata>
```

Başlangıç için bazı özellikler de ayarlayabilirsiniz `FavoriteMovie.ISO` blob:

* **Content-Type:** application/octet-stream,
* **Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ ==
* **Cache-Control:** no cache

tooset bu özellikler bir metin dosyası oluşturma `c:\WAImportExport\SampleProperties.txt`:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Properties>
    <Content-Type>application/octet-stream</Content-Type>
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>
    <Cache-Control>no-cache</Cache-Control>
</Properties>
```

## <a name="run-hello-azure-importexport-tool-waimportexportexe"></a>Çalışma hello Azure içeri/dışarı aktarma Aracı (WAImportExport.exe)

Hazır toorun hello Azure içeri/dışarı aktarma aracı tooprepare hello iki sabit sürücü sunulmuştur.

**Merhaba ilk oturum için:**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#1  /sk:************* /InitialDriveSet:driveset-1.csv /DataSet:dataset-1.csv /logdir:F:\logs
```

Daha fazla veri eklenen toobe gerekirse, başka bir veri kümesi dosyasını (Initialdataset ile aynı biçimi) oluşturun.

**Merhaba ikinci oturumu için:**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2  /DataSet:dataset-2.csv
```

Merhaba kopyalama oturumları tamamladıktan sonra hello iki sürücüsü hello kopyalama bilgisayardan çıkarın ve toohello uygun Azure veri merkezi sevk. Merhaba iki günlük dosyaları, yükleyeceğiniz `<FirstDriveSerialNumber>.xml` ve `<SecondDriveSerialNumber>.xml`, hello Azure portal hello alma işi oluşturduğunuzda.

## <a name="next-steps"></a>Sonraki adımlar

* [Sabit sürücüleri içeri aktarma işine hazırlama](storage-import-export-tool-preparing-hard-drives-import.md)
* [Sık kullanılan komutlar için hızlı başvuru](storage-import-export-tool-quick-reference.md)
