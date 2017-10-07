---
title: "bir Azure içeri/dışarı aktarma alma işi - v1 aaaRepairing | Microsoft Docs"
description: "Nasıl toorepair oluşturulmuş ve kullanarak çalışan bir alma işi hello Azure içeri/dışarı aktarma bilgi hizmeti."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 38cc16bd-ad55-4625-9a85-e1726c35fd1b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: b1cb7d7832276a05c0912cf57505e2a5d79e7846
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="repairing-an-import-job"></a>Bir içeri aktarma işini onarma
Microsoft Azure içeri/dışarı aktarma hizmeti Hello toocopy başarısız olabilir bazı dosyaları veya bir dosya toohello Windows Azure Blob hizmeti bölümlerini. Hataları görmek için bazı nedenler şunlardır:  
  
-   Bozuk dosyaları  
  
-   Bozuk sürücüler  
  
-   Merhaba depolama hesabı anahtarı Hello dosya aktarılırken değiştirildi.  
  
Merhaba Microsoft Azure içeri/dışarı aktarma aracı hello alma işin kopyalama günlük dosyaları ve hello aracı yüklemeleri hello eksik dosyaları (veya, bir dosyanın parçalarını) ile tooyour Windows Azure depolama hesabı toocomplete hello alma işi çalıştırabilirsiniz.  
  
## <a name="repairimport-parameters"></a>RepairImport parametreleri

Merhaba aşağıdaki parametreleri ile belirtilebilir **RepairImport**: 
  
|||  
|-|-|  
|**/ r:**< RepairFile\>|**Gerekli.** Hello onarım hello ilerleyişini izler ve tooresume kesintiye uğramış bir onarım veren yolu toohello onarım dosyası. Her bir sürücü bir ve yalnızca bir onarım dosyası olması gerekir. Belirli bir sürücü için onarım başlattığınızda, henüz var olmayan hello yolu tooa onarım dosyası, geçirin. tooresume kesintiye uğramış bir onarım, varolan bir onarma dosyasını hello adlarında geçirmelisiniz. Merhaba onarım dosya karşılık gelen toohello hedef sürücüde her zaman belirtilmesi gerekir.|  
|**/ LOGDIR:**< LogDirectory\>|**İsteğe bağlı.** Merhaba günlük dosyası dizini. Ayrıntılı günlük dosyaları toothis dizin yazılır. Günlük dizini belirtilirse, hello geçerli dizin hello günlük dizini olarak kullanılır.|  
|**/ d:**< TargetDirectories\>|**Gerekli.** İçe aktarılan özgün dosyaları içeren bir veya daha çok noktalı virgülle ayrılmış dizinleri hello. Merhaba alma sürücü de kullanılabilir, ancak özgün dosyaları alternatif konumlara kullanılabilir, gerekli değildir.|  
|**/BK:**< BitLockerKey\>|**İsteğe bağlı.** Merhaba aracı toounlock hello özgün dosyaları kullanılabildiği şifrelenmiş sürücünün istiyorsanız hello BitLocker anahtar belirtmeniz gerekir.|  
|**/sn:**< StorageAccountName\>|**Gerekli.** Merhaba hello için hello depolama hesabı adını alma işi.|  
|**/SK:**< StorageAccountKey\>|**Gerekli** bir kapsayıcı SAS varsa ve yalnızca belirtilmezse. Merhaba hesap anahtarı hello depolama hesabı hello için alma işi.|  
|**/csas:**< ContainerSas\>|**Gerekli** hello depolama hesabı anahtarı belirtilmezse varsa ve yalnızca. Merhaba kapsayıcı SAS hello hello içe aktarma işi ile ilişkili BLOB'ları erişmek için.|  
|**/ CopyLogFile:**< DriveCopyLogFile\>|**Gerekli.** Yol toohello sürücü kopyalama günlük dosyası (ayrıntılı günlük ya da hata günlüğü). Merhaba dosya hello Windows Azure içeri/dışarı aktarma hizmeti tarafından oluşturulan ve hello işle ilişkili hello blob depolama biriminden indirilebilir. Merhaba kopyalama günlük dosyası başarısız BLOB'lar ya da onarılması toobe olan dosyalar hakkında bilgi içerir.|  
|**/ PathMapFile:**< DrivePathMapFile\>|**İsteğe bağlı.** Kullanılabilir yol tooa metin dosyası ile aynı ad içinde almakta hello birden fazla dosya varsa tooresolve belirsizlikleri hello aynı iş. Merhaba ilk saat hello aracı çalıştırın, tüm hello belirsiz adları bu dosyayla doldurabilirsiniz. Hello aracının sonraki çalışır, bu dosya tooresolve hello belirsizlikleri kullanın.|  
  
## <a name="using-hello-repairimport-command"></a>Merhaba RepairImport komutunu kullanma  
Merhaba ağ üzerinden hello veri akış tarafından toorepair veri içeri aktar alma kullanarak hello özgün dosyaları içeren hello dizinleri hello belirtmelisiniz `/d` parametresi. Depolama hesabınızdan indirdiğiniz hello kopyalama günlük dosyası da belirtmeniz gerekir. Tipik komut satırı toorepair içe aktarma işi kısmi hatalarıyla şuna benzer:  
  
```  
WAImportExport.exe RepairImport /r:C:\WAImportExport\9WM35C2V.rep /d:C:\Users\bob\Pictures;X:\BobBackup\photos /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C2V.log  
```  
  
Hello hello içe aktarma işi için sevk edilen hello sürücüde aşağıdaki örnekte bir kopya günlük dosyası, dosya bir 64 K parçası bozulmuş. Belirtilen hello yalnızca hatası olduğundan hello rest hello BLOB hello işi başarıyla içeri aktarıldı.  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog>  
 <DriveId>9WM35C2V</DriveId>  
 <Blob Status="CompletedWithErrors">  
 <BlobPath>pictures/animals/koala.jpg</BlobPath>  
 <FilePath>\animals\koala.jpg</FilePath>  
 <Length>163840</Length>  
 <ImportDisposition Status="Overwritten">overwrite</ImportDisposition>  
 <PageRangeList>  
  <PageRange Offset="65536" Length="65536" Hash="AA2585F6F6FD01C4AD4256E018240CD4" Status="Corrupted" />  
 </PageRangeList>  
 </Blob>  
 <Status>CompletedWithErrors</Status>  
</DriveLog>  
```
  
Bu kopyalama günlük toohello Azure içeri/dışarı aktarma aracı geçirildiğinde hello aracı hello ağ üzerinden hello eksik içeriği kopyalayarak toofinish hello alma bu dosya için çalışır. Yukarıdaki Hello örnek hello aracı görünmesi için hello özgün dosya `\animals\koala.jpg` hello iki dizinleri içinde `C:\Users\bob\Pictures` ve `X:\BobBackup\photos`. Merhaba, dosya `C:\Users\bob\Pictures\animals\koala.jpg` yoksa, hello Azure içeri/dışarı aktarma aracı kopyaları hello eksik aralığını veri toohello karşılık gelen blob `http://bobmediaaccount.blob.core.windows.net/pictures/animals/koala.jpg`.  
  
## <a name="resolving-conflicts-when-using-repairimport"></a>RepairImport kullanırken çakışmalarını çözme  
Bazı durumlarda, hello aracı mümkün toofind veya açık hello gerekli dosyası hello aşağıdaki nedenlerden biri olabilir: hello dosya bulunamadı, hello dosyası erişilebilir değil, hello dosya adı belirsiz veya hello dosyanın Merhaba içeriğine doğru artık.  
  
Merhaba aracı toolocate çalışıyor belirsiz bir hata oluşabilir `\animals\koala.jpg` ve her ikisi de altında bu ada sahip bir dosya `C:\Users\bob\pictures` ve `X:\BobBackup\photos`. Diğer bir deyişle, her ikisi de `C:\Users\bob\pictures\animals\koala.jpg` ve `X:\BobBackup\photos\animals\koala.jpg` hello alma işi sürücülerinde mevcut.  
  
Merhaba `/PathMapFile` seçenek sağlar, tooresolve bu hatalar. Merhaba aracı hello dosyaların listesini içeren hello dosyasının hello adı kullanamadı belirtebilirsiniz toocorrectly tanımlayın. Merhaba aşağıdaki komut satırı örnek doldurur `9WM35C2V_pathmap.txt`:  
  
```
WAImportExport.exe RepairImport /r:C:\WAImportExport\9WM35C2V.rep /d:C:\Users\bob\Pictures;X:\BobBackup\photos /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C2V.log /PathMapFile:C:\WAImportExport\9WM35C2V_pathmap.txt  
```
  
Merhaba aracı sonra yazacak hello sorunlu dosya yolları çok`9WM35C2V_pathmap.txt`, her satırda bir tane. Örneğin, hello dosyası girdileri hello komutu çalıştırdıktan sonra aşağıdaki hello içerebilir:  
 
```
\animals\koala.jpg  
\animals\kangaroo.jpg  
```
  
 Merhaba listesindeki her dosya için toolocate denemek ve kullanılabilir toohello araçtır hello dosya tooensure açın. Tootell hello aracı istiyorsanız açıkça toofind bir dosya, değiştirebileceğiniz hello yolu eşleme dosyası ve hello yolu tooeach hello dosyada Ekle sekmesinde karakteriyle ayrılmış aynı satır:  
  
```
\animals\koala.jpg           C:\Users\bob\Pictures\animals\koala.jpg  
\animals\kangaroo.jpg        X:\BobBackup\photos\animals\kangaroo.jpg  
```
  
Yapmayı hello gerekli dosyaları kullanılabilir toohello aracını veya güncelleştirme hello yol haritası sonra hello aracı toocomplete hello içeri aktarma işlemi çalıştırabilirsiniz.  
  
## <a name="next-steps"></a>Sonraki adımlar
 
* [Kurulum hello Azure içeri/dışarı aktarma aracı](storage-import-export-tool-setup-v1.md)   
* [Sabit sürücüleri içeri aktarma işine hazırlama](../storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [Kopyalama günlük dosyalarıyla iş durumunu gözden geçirme](storage-import-export-tool-reviewing-job-status-v1.md)   
* [Bir dışarı aktarma işini onarma](../storage-import-export-tool-repairing-an-export-job-v1.md)   
* [Sorun giderme hello Azure içeri/dışarı aktarma aracı](storage-import-export-tool-troubleshooting-v1.md)
