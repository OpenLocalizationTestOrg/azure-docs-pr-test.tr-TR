---
title: "aaaSample iş akışı tooprep sabit sürücüler için bir Azure içeri/dışarı aktarma alma işi - v1 | Microsoft Docs"
description: "Sürücüleri hello Azure içeri/dışarı aktarma hizmeti, bir içeri aktarma işi hazırlama hello tam işlemi için bkz."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 6eb1b1b7-c69f-4365-b5ef-3cd5e05eb72a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: eb77831a88c16c14838179a6432ddb06503067dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sample-workflow-tooprepare-hard-drives-for-an-import-job"></a>Örnek iş akışı tooprepare sabit sürücüler içeri aktarma işi için
Bu konu, sürücüler için içeri aktarma işi hazırlama hello tam işlemi açıklanmaktadır.  
  
Bu örnek veri adlı bir Windows Azure depolama hesabı aşağıdaki hello alır `mystorageaccount`:  
  
|Konum|Açıklama|  
|--------------|-----------------|  
|H:\Video|Bir koleksiyonu videoları, 5 TB toplam.|  
|H:\Photo|Bir koleksiyonu fotoğrafları, toplam 30 GB.|  
|K:\Temp\FavoriteMovie.ISO|A Blu-ray™ disk görüntüsü, 25 GB.|  
|\\\bigshare\john\music|Müzik dosyalarının toplam 10 GB bir ağ paylaşımında koleksiyonu.|  
  
Merhaba alma işi hello hello depolama hesabındaki hedeflerini izleyerek bu veri aktarır:  
  
|Kaynak|Hedef sanal dizin veya blob|  
|------------|-------------------------------------------|  
|H:\Video|https://mystorageaccount.BLOB.Core.Windows.NET/video|  
|H:\Photo|https://mystorageaccount.BLOB.Core.Windows.NET/Photo|  
|K:\Temp\FavoriteMovie.ISO|https://mystorageaccount.BLOB.Core.Windows.NET/favorite/FavoriteMovies.ISO|  
|\\\bigshare\john\music|https://mystorageaccount.BLOB.Core.Windows.NET/Music|  
  
Bu eşleme ile dosya hello `H:\Video\Drama\GreatMovie.mov` alınan toohello blobu `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.  
  
Ardından, toodetermine işlem hello hello verilerin boyutunu kaç sabit sürücüler gerekli değildir:  
  
`5TB + 30GB + 25GB + 10GB = 5TB + 65GB`  
  
Bu örnekte, iki 3 TB sabit sürücü yeterli olacaktır. Ancak hello kaynak dizin itibaren `H:\Video` 5 TB'lık veriyi varsa ve yalnızca 3 TB, tek sabit diskin kapasitesini gerekli toobreak olan `H:\Video` iki küçük dizini içine: `H:\Video1` ve `H:\Video2`çalışan hello önce Microsoft Azure içeri/dışarı aktarma aracı. Bu adım, kaynak dizinleri izleyen hello verir:  
  
|Konum|Boyut|Hedef sanal dizin veya blob|  
|--------------|----------|-------------------------------------------|  
|H:\Video1|2,5 TB|https://mystorageaccount.BLOB.Core.Windows.NET/video|  
|H:\Video2|2,5 TB|https://mystorageaccount.BLOB.Core.Windows.NET/video|  
|H:\Photo|30 GB|https://mystorageaccount.BLOB.Core.Windows.NET/Photo|  
|K:\Temp\FavoriteMovies.ISO|25 GB|https://mystorageaccount.BLOB.Core.Windows.NET/favorite/FavoriteMovies.ISO|  
|\\\bigshare\john\music|10 GB|https://mystorageaccount.BLOB.Core.Windows.NET/Music|  
  
 Rağmen hello `H:\Video`dizin, tootwo dizinleri bölme, toohello noktası aynı hedef sanal dizinde hello depolama hesabı. Bu şekilde tüm video dosyaları altında tek bir korunur `video` hello depolama hesabındaki kapsayıcı.  
  
 Ardından, hello önceki kaynak dizinleri eşit olarak dağıtılmış toohello iki sabit sürücü şunlardır:  
  
||||  
|-|-|-|  
|Sabit sürücü|Kaynak dizinler|Toplam boyutu|  
|İlk sürücü|H:\Video1|2.5 TB + 30 GB|  
||H:\Photo||  
|İkinci sürücü|H:\Video2|2.5 TB + 35 GB|  
||K:\Temp\BlueRay.ISO||  
||\\\bigshare\john\music||  
  
Ayrıca, tüm dosyalar için meta veriler aşağıdaki hello ayarlayabilirsiniz:  
  
-   **UploadMethod:** Windows Azure içeri/dışarı aktarma hizmeti  
  
-   **DataSetName:** SampleData  
  
-   **CreationDate:** 1/10/2013  
  
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
  
-   **Content-Type:** application/octet-stream,  
  
-   **Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ ==  
  
-   **Cache-Control:** no cache  
  
tooset bu özellikler bir metin dosyası oluşturma `c:\WAImportExport\SampleProperties.txt`:  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
    <Content-Type>application/octet-stream</Content-Type>  
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>  
    <Cache-Control>no-cache</Cache-Control>  
</Properties>  
```
  
Hazır toorun hello Azure içeri/dışarı aktarma aracı tooprepare hello iki sabit sürücü sunulmuştur. Şunlara dikkat edin:  
  
-   Merhaba ilk sürücü X sürücü olarak bağlı.  
  
-   Merhaba ikinci sürücü Y sürücü olarak bağlı.  
  
-   Merhaba depolama hesabının Hello anahtarı `mystorageaccount` olan `8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg==`.  

## <a name="preparing-disk-for-import-when-data-is-pre-loaded"></a>Veri önceden yüklendiğinde disk alma işlemi için hazırlanıyor
 
 İçeri aktarılan hello veri toobe hello diskte zaten hello bayrağı /skipwrite kullanın. Merhaba değeri /t ve /srcdir alma için hazırlanan iki nokta toohello disk gerekir. Alınan hello veri toobe tümünün değil olduğuna varsa toohello aynı hedef sanal dizin veya hello depolama hesabı, aynı komut her hedef dizin için ayrı olarak, çalışma hello kökündeki /ID hello değerini tutma hello aynı tüm çalıştırmaları arasında.

>[!NOTE] 
>Bunu hello diskte hello verileri silme şekilde Format belirtmeyin. Belirtin / şifrelemek veya olup hello disk zaten veya şifrelenmiş bağlı olarak /bk. 
>

```
    When data is already present on hello disk for each drive run hello following command.
    WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Video1 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:x:\Video1 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt /skipwrite
```

## <a name="copy-sessions---first-drive"></a>Oturumlarını - Kopyala ilk sürücü

Merhaba ilk sürücü dizinleri hello Azure içeri/dışarı aktarma iki kez toocopy hello iki kaynak aracı çalıştırın:  

**İlk kopya oturumu**
  
```
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Video1 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:H:\Video1 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```

**İkinci kopya oturumu**

```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Photo /srcdir:H:\Photo /dstdir:photo/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt
```

## <a name="copy-sessions---second-drive"></a>Oturumlarını - Kopyala ikinci sürücü
 
Merhaba çalıştırmak ikinci sürücü hello Azure içeri/dışarı aktarma aracı üç kez, her hello için dizinler kaynağı ve bir kez hello tek başına Blu-Ray™ dosya görüntü bir kez):  
  
**İlk kopya oturumu** 

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:Video2 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:y /format /encrypt /srcdir:H:\Video2 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```
  
**İkinci kopya oturumu**

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:Music /srcdir:\\bigshare\john\music /dstdir:music/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```  
  
**Üçüncü kopya oturumu**  

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:BlueRayIso /srcfile:K:\Temp\BlueRay.ISO /dstblob:favorite/BlueRay.ISO /MetadataFile:c:\WAImportExport\SampleMetadata.txt /PropertyFile:c:\WAImportExport\SampleProperties.txt  
```

## <a name="copy-session-completion"></a>Kopya oturum tamamlama

Hello kopyalama oturumları tamamladıktan sonra hello iki sürücüsü hello kopyalama bilgisayardan bağlantısını kesmek ve toohello uygun Windows Azure veri merkezi sevk. Merhaba iki günlük dosyaları, karşıya yükleme `FirstDrive.jrn` ve `SecondDrive.jrn`, hello hello alma işi oluşturduğunuzda [Windows Azure portalında](https://manage.windowsazure.com/).  
  
## <a name="next-steps"></a>Sonraki adımlar

* [Sabit sürücüleri içeri aktarma işine hazırlama](../storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [Sık kullanılan komutlar için hızlı başvuru](../storage-import-export-tool-quick-reference-v1.md) 
