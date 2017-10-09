---
title: "bir Azure içeri/dışarı aktarma dışarı aktarma işinin - v1 aaaRepairing | Microsoft Docs"
description: "Nasıl toorepair oluşturulmuş ve kullanarak çalışan bir dışarı aktarma işinin hello Azure içeri/dışarı aktarma bilgi hizmeti."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 728e2a42-04ce-4be8-9375-e9e2bc6827a5
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 96c674fc7c697c37882fb2980c340303896ac6c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="repairing-an-export-job"></a>Bir dışarı aktarma işini onarma
Bir dışarı aktarma işi tamamlandıktan sonra Microsoft Azure içeri/dışarı aktarma aracı şirket içi hello çalıştırabilirsiniz:  
  
1.  Hello Azure içeri/dışarı aktarma hizmeti oluşturamıyor tooexport olduğunu dosyalarını indirin.  
  
2.  Merhaba dosyaları hello sürücüye doğru şekilde aktarılmış doğrulayın.  
  
Bu işlev bağlantısı tooAzure depolama toouse olması gerekir.  
  
içe aktarma işi onarmak için hello komutu **RepairExport**.

## <a name="repairexport-parameters"></a>RepairExport parametreleri

Merhaba aşağıdaki parametreleri ile belirtilebilir **RepairExport**:  
  
|Parametre|Açıklama|  
|---------------|-----------------|  
|**/ r: < RepairFile\>**|Gereklidir. Hello onarım hello ilerleyişini izler ve tooresume kesintiye uğramış bir onarım veren yolu toohello onarım dosyası. Her bir sürücü bir ve yalnızca bir onarım dosyası olması gerekir. Belirli bir sürücü için onarım başlattığınızda, henüz var olmayan hello yolu tooa onarım dosyasında geçer. tooresume kesintiye uğramış bir onarım, varolan bir onarma dosyasını hello adlarında geçirmelisiniz. Merhaba onarım dosya karşılık gelen toohello hedef sürücüde her zaman belirtilmesi gerekir.|  
|**/ LOGDIR: < LogDirectory\>**|İsteğe bağlı. Merhaba günlük dosyası dizini. Ayrıntılı günlük dosyalarını toothis dizin yazılır. Günlük dizini belirtilirse, hello geçerli dizin hello günlük dizini kullanılır.|  
|**/ d: < TargetDirectory\>**|Gereklidir. Merhaba dizin toovalidate ve Onar. Bu genellikle hello verme sürücüsünün kök dizinindeki hello olmakla birlikte, bir ağ dosya paylaşımına dışarı hello dosyalarının bir kopyasını da içeren.|  
|**/BK: < BitLockerKey\>**|İsteğe bağlı. Bir şifrelenmiş dosyaların nerede hello dışarı depolanır hello aracı toounlock istiyorsanız hello BitLocker anahtar belirtmeniz gerekir.|  
|**/sn: < StorageAccountName\>**|Gereklidir. Merhaba depolama hesabının adını Hello hello için iş verin.|  
|**/SK: < StorageAccountKey\>**|**Gerekli** bir kapsayıcı SAS varsa ve yalnızca belirtilmezse. Merhaba hesap anahtarı hello depolama hesabı hello için iş verin.|  
|**/csas: < ContainerSas\>**|**Gerekli** hello depolama hesabı anahtarı belirtilmezse varsa ve yalnızca. Merhaba kapsayıcı SAS hello hello dışa aktarma işi ile ilişkili BLOB'ları erişmek için.|  
|**/ CopyLogFile: < DriveCopyLogFile\>**|Gereklidir. Merhaba yol toohello sürücü kopyalama günlük dosyası. Merhaba dosya hello Windows Azure içeri/dışarı aktarma hizmeti tarafından oluşturulan ve hello işle ilişkili hello blob depolama biriminden indirilebilir. Merhaba kopyalama günlük dosyası başarısız BLOB veya onarıldı toobe dosyaları hakkında bilgi içerir.|  
|**/ Manıfestfıle: < DriveManifestFile\>**|İsteğe bağlı. Merhaba yolu toohello verme sürücünün bildirim dosyası. Bu dosya hello Windows Azure içeri/dışarı aktarma hizmeti tarafından oluşturulan ve hello verme sürücüsünde ve isteğe bağlı olarak hello işle ilişkili hello depolama hesabındaki blob içinde depolanır.<br /><br /> Merhaba hello verme sürücüde hello dosyaların içeriğini bu dosyada bulunan hello MD5 karma ile doğrulanır. Bozuk belirlendiği toobe tüm dosyalar indirildi ve yeniden toohello hedef dizinleri olacaktır.|  
  
## <a name="using-repairexport-mode-toocorrect-failed-exports"></a>RepairExport kullanarak modu toocorrect dışarı aktarma başarısız oldu  
Tooexport başarısız hello Azure içeri/dışarı aktarma aracı toodownload dosyalarını kullanabilirsiniz. Merhaba kopyalama günlük dosyası tooexport başarısız dosyaların bir listesini içerir.  
  
Merhaba dışa aktarma hatalarının olasılıklar aşağıdaki hello nedenler:  
  
-   Bozuk sürücüler  
  
-   Merhaba depolama hesabı anahtarı Hello aktarma işlemi sırasında değiştirildi  
  
toorun hello aracında **RepairExport** modu, ilk ihtiyacınız hello dışa aktarılan dosyaları tooyour bilgisayar içeren tooconnect hello sürücü. Ardından, hello hello yolu toothat sürücünün ile Merhaba belirtilmesi Azure içeri/dışarı aktarma aracı çalıştırın `/d` parametresi. İndirdiğiniz toospecify hello yolu toohello sürücünün kopyalama günlük dosyası da gerekir. Merhaba aşağıdaki aşağıdaki komut satırı örnek hello aracı toorepair tooexport başarısız herhangi bir dosya çalıştırır:  
  
```  
WAImportExport.exe RepairExport /r:C:\WAImportExport\9WM35C3U.rep /d:G:\ /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C3U.log  
```  
  
Merhaba, bu bir blok hello başarısız blob tooexport gösteren günlük dosya Kopyala örneği aşağıdadır:  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog>  
  <DriveId>9WM35C2V</DriveId>  
  <Blob Status="CompletedWithErrors">  
    <BlobPath>pictures/wild/desert.jpg</BlobPath>  
    <FilePath>\pictures\wild\desert.jpg</FilePath>  
    <LastModified>2012-09-18T23:47:08Z</LastModified>  
    <Length>163840</Length>  
    <BlockList>  
      <Block Offset="65536" Length="65536" Id="AQAAAA==" Status="Failed" />  
    </BlockList>  
  </Blob>  
  <Status>CompletedWithErrors</Status>  
</DriveLog>  
```  
  
Merhaba kopyalama günlük dosyası hello Windows Azure içeri/dışarı aktarma hizmeti hello verme sürücüde hello blob'un blokları toohello dosyası birini indirme uygulanırken bir hata oluştu gösterir. diğer bileşenleri başarıyla indirildi hello dosyasının hello ve hello dosya uzunluğunu doğru şekilde ayarlandı. Bu durumda, hello aracı hello sürücüde hello dosyasını açın, hello blok hello depolama hesabından karşıdan yükle ve toohello dosya aralık uzaklığı 65536 uzunluğu 65536 ile başlayarak yazma.  
  
## <a name="using-repairexport-toovalidate-drive-contents"></a>RepairExport toovalidate sürücü içeriğini kullanma  
Azure içeri/dışarı aktarma ile Merhaba kullanabilirsiniz **RepairExport** hello sürücü seçeneği toovalidate Merhaba içeriğine doğru. Merhaba bildirim dosyası her dışarı aktarma sürücüde MD5s hello hello sürücü içeriğini içerir.  
  
Hello Azure içeri/dışarı aktarma hizmeti ayrıca hello bildirim dosyaları tooa depolama hesabı hello dışa aktarma işlemi sırasında kaydedebilirsiniz. Merhaba hello bildirim dosyalarının konumu hello kullanılabilir [alma işi](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) hello iş tamamlandığında işlemi. Bkz: [içeri/dışarı aktarma hizmeti bildirim dosyası biçimi](storage-import-export-file-format-metadata-and-properties.md) sürücü bildirim dosyası hello biçimi hakkında daha fazla bilgi için.  
  
Merhaba aşağıdaki örnekte nasıl toorun hello Azure içeri/dışarı aktarma aracı ile Merhaba gösterir **/ManifestFile** ve **/CopyLogFile** Parametreler:  
  
```  
WAImportExport.exe RepairExport /r:C:\WAImportExport\9WM35C3U.rep /d:G:\ /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C3U.log /ManifestFile:G:\9WM35C3U.manifest  
```  
  
Merhaba, bir bildirim dosyası örneği verilmiştir:  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveManifest Version="2011-10-01">  
  <Drive>  
    <DriveId>9WM35C3U</DriveId>  
    <ClientCreator>Windows Azure Import/Export service</ClientCreator>  
    <BlobList>
      <Blob>  
        <BlobPath>pictures/city/redmond.jpg</BlobPath>  
        <FilePath>\pictures\city\redmond.jpg</FilePath>  
        <Length>15360</Length>  
        <PageRangeList>  
          <PageRange Offset="0" Length="3584" Hash="72FC55ED9AFDD40A0C8D5C4193208416" />  
          <PageRange Offset="3584" Length="3584" Hash="68B28A561B73D1DA769D4C24AA427DB8" />  
          <PageRange Offset="7168" Length="512" Hash="F521DF2F50C46BC5F9EA9FB787A23EED" />  
        </PageRangeList>  
        <PropertiesPath Hash="E72A22EA959566066AD89E3B49020C0A">\pictures\city\redmond.jpg.properties</PropertiesPath>  
      </Blob>  
      <Blob>  
        <BlobPath>pictures/wild/canyon.jpg</BlobPath>  
        <FilePath>\pictures\wild\canyon.jpg</FilePath>  
        <Length>10884</Length>  
        <BlockList>  
          <Block Offset="0" Length="2721" Id="AAAAAA==" Hash="263DC9C4B99C2177769C5EBE04787037" />  
          <Block Offset="2721" Length="2721" Id="AQAAAA==" Hash="0C52BAE2CC20EFEC15CC1E3045517AA6" />  
          <Block Offset="5442" Length="2721" Id="AgAAAA==" Hash="73D1CB62CB426230C34C9F57B7148F10" />  
          <Block Offset="8163" Length="2721" Id="AwAAAA==" Hash="11210E665C5F8E7E4F136D053B243E6A" />  
        </BlockList>  
        <PropertiesPath Hash="81D7F81B2C29F10D6E123D386C3A4D5A">\pictures\wild\canyon.jpg.properties</PropertiesPath>  
      </Blob> 
    </BlobList>  
 </Drive>  
</DriveManifest>  
``` 
  
Sonlandırma hello Onarım işleminden sonra hello aracı hello bildirim dosyasında başvurulan her bir dosya üzerinden okuma ve hello MD5 karma ile Merhaba dosyanın bütünlüğünü doğrular. Yukarıdaki Hello bildirimi için bileşenleri aşağıdaki hello geçer.  

```  
G:\pictures\city\redmond.jpg, offset 0, length 3584  
  
G:\pictures\city\redmond.jpg, offset 3584, length 3584  
  
G:\pictures\city\redmond.jpg, offset 7168, length 3584  
  
G:\pictures\city\redmond.jpg.properties  
  
G:\pictures\wild\canyon.jpg, offset 0, length 2721  
  
G:\pictures\wild\canyon.jpg, offset 2721, length 2721  
  
G:\pictures\wild\canyon.jpg, offset 5442, length 2721  
  
G:\pictures\wild\canyon.jpg, offset 8163, length 2721  
  
G:\pictures\wild\canyon.jpg.properties  
```

Merhaba doğrulama başarısız olan herhangi bir bileşeni hello aracı tarafından indirilir ve yeniden yazılmıştır hello sürücüde dosya aynı toohello.  
  
## <a name="next-steps"></a>Sonraki adımlar
 
* [Kurulum hello Azure içeri/dışarı aktarma aracı](storage-import-export-tool-setup-v1.md)   
* [Sabit sürücüleri içeri aktarma işine hazırlama](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [Kopyalama günlük dosyalarıyla iş durumunu gözden geçirme](storage-import-export-tool-reviewing-job-status-v1.md)   
* [Bir içeri aktarma işini onarma](storage-import-export-tool-repairing-an-import-job-v1.md)   
* [Sorun giderme hello Azure içeri/dışarı aktarma aracı](storage-import-export-tool-troubleshooting-v1.md)
