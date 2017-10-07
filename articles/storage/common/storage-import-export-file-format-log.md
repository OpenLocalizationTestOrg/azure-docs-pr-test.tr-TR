---
title: "aaaAzure içeri/dışarı aktarma günlük dosyası biçimi | Microsoft Docs"
description: "İçeri/dışarı aktarma hizmeti işi için adımları çalıştırıldığında oluşturulan hello günlük dosyalarını hello biçimi hakkında bilgi edinin."
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
ms.openlocfilehash: 15a652455aa947922af0aa39ccefe68811a3db19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-importexport-service-log-file-format"></a>Azure içeri/dışarı aktarma hizmeti günlük dosyası biçimi
Merhaba Microsoft Azure içeri/dışarı aktarma hizmeti bir alma işi veya bir dışarı aktarma işinin parçası olarak bir sürücüde bir eylem gerçekleştirdiğinde, günlükleri hello depolama hesabındaki bu işle ilişkili tooblock BLOB'lar yazılır.  
  
İçeri/dışarı aktarma hizmeti hello tarafından yazılan iki günlükleri şunlardır:  
  
-   Merhaba hata günlüğü her zaman bir hata hello olayda oluşturulur.  
  
-   Merhaba ayrıntılı günlük varsayılan olarak etkin değildir, ancak ayarı hello tarafından etkinleştirilebilir `EnableVerboseLog` özelliği bir [Put işlemini](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) veya [güncelleştirme işi özellikleri](/rest/api/storageimportexport/jobs#Jobs_Update) işlemi.  
  
## <a name="log-file-location"></a>Günlük dosyası konumu  
Merhaba günlükleri tooblock BLOB'lar hello kapsayıcı veya hello tarafından belirtilen sanal dizin yazılır `ImportExportStatesPath` üzerinde ayarlayabilirsiniz ayarı bir `Put Job` işlemi. Merhaba konumu toowhich hello günlükleri bağlıdır nasıl kimlik doğrulaması için belirtilen başlangıç değeri ile birlikte hello işi için belirtilen üzerine yazılır `ImportExportStatesPath`. Kimlik doğrulaması hello işi için bir depolama hesabı anahtarı ya da bir kapsayıcı SAS (paylaşılan erişim imzası) belirtilebilir.  
  
Merhaba hello kapsayıcı veya sanal dizin adını olabilir ya da olması hello varsayılan adını `waimportexport`, veya başka bir kapsayıcı veya sanal dizin adı.  
  
Merhaba tabloda hello olası seçenekleri gösterir:  
  
|Kimlik Doğrulama Yöntemi|Değeri `ImportExportStatesPath`öğesi|Günlük BLOB'lar konumu|  
|---------------------------|----------------------------------------------|---------------------------|  
|Depolama hesabı anahtarı|Varsayılan değer|Adlı bir kapsayıcı `waimportexport`, hello varsayılan kapsayıcı olduğu. Örneğin:<br /><br /> `https://myaccount.blob.core.windows.net/waimportexport`|  
|Depolama hesabı anahtarı|Kullanıcı tarafından belirtilen değeri|Merhaba kullanıcı tarafından adlı bir kapsayıcı. Örneğin:<br /><br /> `https://myaccount.blob.core.windows.net/mylogcontainer`|  
|Kapsayıcı SAS|Varsayılan değer|Adlı bir sanal dizini `waimportexport`, hello SAS belirtilen hello kapsayıcısı altında hello varsayılan adı olduğu.<br /><br /> Örneğin, hello SAS belirtilen hello iş ise `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, hello günlük konumu şu şekilde olacaktır`https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport`|  
|Kapsayıcı SAS|Kullanıcı tarafından belirtilen değeri|Merhaba SAS belirtilen hello kapsayıcısı altında hello kullanıcı tarafından adlı bir sanal dizini.<br /><br /> Örneğin, hello SAS belirtilen hello iş ise `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, ve hello belirtilen sanal dizin adlandırılan `mylogblobs`, hello günlük konumu şu şekilde olacaktır `https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport/mylogblobs`.|  
  
Arama hello tarafından hello URL'sini hello hata ve ayrıntılı günlükleri alabilirsiniz [alma işi](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) işlemi. Merhaba günlüklerini hello sürücü işlenmesini tamamlandıktan sonra kullanılabilir.  
  
## <a name="log-file-format"></a>Günlük dosyası biçimi  
Merhaba her iki günlük biçimi olan hello aynı: hello sabit sürücü ve hello müşterinin hesabına arasında BLOB'ları kopyalanırken oluştu hello olayları XML açıklamaları içeren blob.  
  
Hello hata günlüğü yalnızca hello bilgi BLOB veya hello sırasında hatalarla karşılaştı dosyaları için içerirken hello ayrıntılı günlüğü, her blob (için içeri aktarma işi için) veya dosyası (bir dışarı aktarma işinin), başlangıç kopyalama işlemi hello durumu hakkında tam bilgi içerir. içeri veya dışarı aktarma işi.  
  
Merhaba ayrıntılı günlük biçimi aşağıda gösterilmiştir. Merhaba hata günlüğü aynı yapısı, ancak başarılı işlemleri filtreler hello vardır.  

```xml
<DriveLog Version="2014-11-01">  
  <DriveId>drive-id</DriveId>  
  [<Blob Status="blob-status">  
   <BlobPath>blob-path</BlobPath>  
   <FilePath>file-path</FilePath>  
   [<Snapshot>snapshot</Snapshot>]  
   <Length>length</Length>  
   [<LastModified>last-modified</LastModified>]  
   [<ImportDisposition Status="import-disposition-status">import-disposition</ImportDisposition>]  
   [page-range-list-or-block-list]  
   [metadata-status]  
   [properties-status]  
  </Blob>]  
  [<Blob>  
    . . .  
  </Blob>]  
  <Status>drive-status</Status>  
</DriveLog>  
  
page-range-list-or-block-list ::= 
  page-range-list | block-list  
  
page-range-list ::=   
<PageRangeList>  
      [<PageRange Offset="page-range-offset" Length="page-range-length"   
       [Hash="md5-hash"] Status="page-range-status"/>]  
      [<PageRange Offset="page-range-offset" Length="page-range-length"   
       [Hash="md5-hash"] Status="page-range-status"/>]  
</PageRangeList>  
  
block-list ::=  
<BlockList>  
      [<Block Offset="block-offset" Length="block-length" [Id="block-id"]  
       [Hash="md5-hash"] Status="block-status"/>]  
      [<Block Offset="block-offset" Length="block-length" [Id="block-id"]   
       [Hash="md5-hash"] Status="block-status"/>]  
</BlockList>  
  
metadata-status ::=  
<Metadata Status="metadata-status">  
   [<GlobalPath Hash="md5-hash">global-metadata-file-path</GlobalPath>]  
   [<Path Hash="md5-hash">metadata-file-path</Path>]  
</Metadata>  
  
properties-status ::=  
<Properties Status="properties-status">  
   [<GlobalPath Hash="md5-hash">global-properties-file-path</GlobalPath>]  
   [<Path Hash="md5-hash">properties-file-path</Path>]  
</Properties>  
```

Merhaba aşağıdaki tabloda hello günlük dosyasının hello öğelerini açıklar.  
  
|XML öğesi|Tür|Açıklama|  
|-----------------|----------|-----------------|  
|`DriveLog`|XML öğesi|Bir sürücü günlük temsil eder.|  
|`Version`|Öznitelik, dize|Merhaba günlük biçimi Hello sürümü.|  
|`DriveId`|Dize|sürücünün donanım seri numarası hello.|  
|`Status`|Dize|Merhaba sürücü işlem durumu. Merhaba bkz `Drive Status Codes` daha fazla bilgi için tablo aşağıda.|  
|`Blob`|İç içe geçmiş XML öğesi|Bir blob temsil eder.|  
|`Blob/BlobPath`|Dize|Merhaba hello blob URI'si.|  
|`Blob/FilePath`|Dize|Merhaba sürücüde Hello göreli yol toohello dosyası.|  
|`Blob/Snapshot`|Tarih saat|Anlık görüntü sürümü yalnızca bir dışa aktarma işi için hello blob Hello.|  
|`Blob/Length`|Tamsayı|Merhaba toplam hello blob bayt cinsinden uzunluğu.|  
|`Blob/LastModified`|Tarih saat|Merhaba tarih o hello blob son, yalnızca bir dışarı aktarma işinin değiştirildi.|  
|`Blob/ImportDisposition`|Dize|Merhaba, yalnızca bir içeri aktarma işi için hello blob eğilimini alın.|  
|`Blob/ImportDisposition/@Status`|Öznitelik, dize|Merhaba Hello durumunu değerlendirme içeri aktarın.|  
|`PageRangeList`|İç içe geçmiş XML öğesi|Bir sayfa blob'u için sayfa aralıklarını listesini temsil eder.|  
|`PageRange`|XML öğesi|Sayfa aralığını temsil eder.|  
|`PageRange/@Offset`|Öznitelik, tamsayı|Merhaba sayfa aralığı uzaklığı hello blob başlatılıyor.|  
|`PageRange/@Length`|Öznitelik, tamsayı|Merhaba sayfa aralığının bayt cinsinden uzunluğu.|  
|`PageRange/@Hash`|Öznitelik, dize|Base16 kodlanmış MD5 karması hello sayfa aralığı.|  
|`PageRange/@Status`|Öznitelik, dize|Merhaba sayfa aralığı işlem durumu.|  
|`BlockList`|İç içe geçmiş XML öğesi|Bir blok blobu için blok listesini temsil eder.|  
|`Block`|XML öğesi|Bloğunu temsil eder.|  
|`Block/@Offset`|Öznitelik, tamsayı|Merhaba blob hello bloğunda başlangıç uzaklığı.|  
|`Block/@Length`|Öznitelik, tamsayı|Merhaba bloğunun bayt cinsinden uzunluğu.|  
|`Block/@Id`|Öznitelik, dize|Merhaba blok kimliği|  
|`Block/@Hash`|Öznitelik, dize|Base16 kodlu MD5 karması hello bloğu.|  
|`Block/@Status`|Öznitelik, dize|Merhaba blok işlem durumu.|  
|`Metadata`|İç içe geçmiş XML öğesi|Merhaba blob'un meta verileri temsil eder.|  
|`Metadata/@Status`|Öznitelik, dize|Merhaba blob meta verileri işlenmesini durumu.|  
|`Metadata/GlobalPath`|Dize|Göreli yol toohello genel meta veri dosyası.|  
|`Metadata/GlobalPath/@Hash`|Öznitelik, dize|Base16 kodlu MD5 karması hello genel meta veri dosyası.|  
|`Metadata/Path`|Dize|Göreli yol toohello meta veri dosyası.|  
|`Metadata/Path/@Hash`|Öznitelik, dize|Base16 kodlu MD5 karması hello meta veri dosyası.|  
|`Properties`|İç içe geçmiş XML öğesi|Merhaba blob özelliklerini temsil eder.|  
|`Properties/@Status`|Öznitelik, dize|Merhaba blob özellikleri, örneğin dosya bulunamadı, işleme durumunu tamamlandı.|  
|`Properties/GlobalPath`|Dize|Göreli yol toohello genel özellikleri dosya.|  
|`Properties/GlobalPath/@Hash`|Öznitelik, dize|Base16 kodlu MD5 karma değeri hello genel özellikleri dosyasının.|  
|`Properties/Path`|Dize|Göreli yol toohello özellikleri dosya.|  
|`Properties/Path/@Hash`|Öznitelik, dize|Base16 kodlu MD5 karma değeri hello özellikleri dosyasının.|  
|`Blob/Status`|Dize|Merhaba blob işlem durumu.|  
  
# <a name="drive-status-codes"></a>Sürücü durum kodları  
Merhaba aşağıdaki tabloda bir sürücü işlemeye hello durum kodlarını listeler.  
  
|Durum kodu|Açıklama|  
|-----------------|-----------------|  
|`Completed`|Merhaba sürücü hatasız işleme tamamlandı.|  
|`CompletedWithWarnings`|Merhaba sürücü işleme hello BLOB'lar için belirtilen hello alma değerlendirmeleri başına bir veya daha fazla BLOB uyarılarla tamamlandı.|  
|`CompletedWithErrors`|Merhaba sürücü bir veya daha fazla BLOB veya öbekleri hatalarla tamamlandı.|  
|`DiskNotFound`|Hello sürücüsünde hiçbir disk bulunamadı.|  
|`VolumeNotNtfs`|Merhaba disk üzerindeki Hello ilk veri birimi NTFS biçiminde değil.|  
|`DiskOperationFailed`|Merhaba sürücü üzerinde işlem gerçekleştirilirken bilinmeyen bir hata oluştu.|  
|`BitLockerVolumeNotFound`|BitLocker encryptable birim bulunamadı.|  
|`BitLockerNotActivated`|Merhaba birimde BitLocker etkin değil.|  
|`BitLockerProtectorNotFound`|Merhaba sayısal parola anahtar koruyucusu hello birimde yok.|  
|`BitLockerKeyInvalid`|sağlanan hello sayısal parola hello birimin kilidi açılamıyor.|  
|`BitLockerUnlockVolumeFailed`|Toounlock hello birim çalışırken bilinmeyen bir hata oluştu.|  
|`BitLockerFailed`|BitLocker işlem gerçekleştirilirken bilinmeyen bir hata oluştu.|  
|`ManifestNameInvalid`|Merhaba yayılma dosyası adı geçersiz.|  
|`ManifestNameTooLong`|Merhaba yayılma dosyası adı çok uzun.|  
|`ManifestNotFound`|Merhaba bildirim dosyası bulunamadı.|  
|`ManifestAccessDenied`|Bildirim toohello dosyası, erişim reddedildi.|  
|`ManifestCorrupted`|Merhaba bildirim dosyası bozuk (Merhaba içerik karması eşleşmiyor).|  
|`ManifestFormatInvalid`|Merhaba bildirim içerik toohello gerekli biçime uymuyor.|  
|`ManifestDriveIdMismatch`|Sürücü Kimliği hello bildirim dosyasında bir hello sürücüden okumayı hello eşleşmiyor hello.|  
|`ReadManifestFailed`|Merhaba bildirimindeki okunurken bir disk g/ç hatası oluştu.|  
|`BlobListFormatInvalid`|Merhaba verme blob listesi blob toohello gerekli biçime uymuyor.|  
|`BlobRequestForbidden`|Merhaba depolama hesabındaki toohello blob'lara erişim yasaklandı. Bu tooinvalid depolama hesabı anahtarı veya kapsayıcı SAS olabilir.|  
|`InternalError`|Ve hello sürücü işlenirken iç hata oluştu.|  
  
## <a name="blob-status-codes"></a>BLOB durum kodları  
Merhaba aşağıdaki tabloda bir blob işlemeye hello durum kodlarını listeler.  
  
|Durum kodu|Açıklama|  
|-----------------|-----------------|  
|`Completed`|Merhaba blob hatasız işleme tamamlandı.|  
|`CompletedWithErrors`|Merhaba blob işleme bir veya daha fazla sayfa aralıklarını veya blokları, meta verileri veya özellikler hatalarla tamamlandı.|  
|`FileNameInvalid`|Merhaba dosya adı geçersiz.|  
|`FileNameTooLong`|Merhaba dosya adı çok uzun.|  
|`FileNotFound`|Merhaba dosyası bulunamadı.|  
|`FileAccessDenied`|Toohello dosyasına erişim engellendi.|  
|`BlobRequestFailed`|blob tooaccess hello hello Blob hizmeti isteği başarısız oldu.|  
|`BlobRequestForbidden`|blob tooaccess hello hello Blob hizmet isteği izin verilmiyor. Bu tooinvalid depolama hesabı anahtarı veya kapsayıcı SAS olabilir.|  
|`RenameFailed`|(İçin bir alma işi) toorename hello blob veya hello dosyası (bir dışarı aktarma işinin) başarısız oldu.|  
|`BlobUnexpectedChange`|Beklenmedik bir değişikliği (için bir dışarı aktarma işinin) hello blob ile oluştu.|  
|`LeasePresent`|Merhaba blob üzerindeki mevcut bir kira var.|  
|`IOFailed`|Bir disk veya ağ g/ç hatası hello blob işlenirken hata oluştu.|  
|`Failed`|Merhaba blob işlenirken bilinmeyen bir hata oluştu.|  
  
## <a name="import-disposition-status-codes"></a>İçeri aktarma değerlendirme durum kodları  
Merhaba aşağıdaki tabloda bir alma değerlendirme çözmek için hello durum kodlarını listeler.  
  
|Durum kodu|Açıklama|  
|-----------------|-----------------|  
|`Created`|Merhaba blob oluşturuldu.|  
|`Renamed`|Merhaba blob adlandırma alma değerlendirme adlandırıldı. Merhaba `Blob/BlobPath` öğe yeniden adlandırılmış hello blob Merhaba URI içeriyor.|  
|`Skipped`|Merhaba blob atlandı başına `no-overwrite` değerlendirme içeri aktarın.|  
|`Overwritten`|Merhaba blob bir blob başına üzerine `overwrite` değerlendirme içeri aktarın.|  
|`Cancelled`|Önceki bir hata hello alma eğilimini işlenmesi durduruldu.|  
  
## <a name="page-rangeblock-status-codes"></a>Sayfa aralık/blok durum kodları  
Merhaba aşağıdaki tabloda bir sayfa aralığı veya bir blok işlemeye hello durum kodlarını listeler.  
  
|Durum kodu|Açıklama|  
|-----------------|-----------------|  
|`Completed`|Başlangıç sayfası aralık veya blok hatasız işleme tamamlandı.|  
|`Committed`|Merhaba blok kaydedildi, ancak değil hello tam engelleme listesi diğer blokları başarısız oldu veya tam engelleme listesi kendisini put başarısız oldu.|  
|`Uncommitted`|Merhaba blok karşıya ancak edilmemiş.|  
|`Corrupted`|Başlangıç sayfası aralık veya blok bozuk (Merhaba içerik karması eşleşmiyor).|  
|`FileUnexpectedEnd`|Bir beklenmeyen dosya sonu karşılaşıldı.|  
|`BlobUnexpectedEnd`|Blob beklenmeyen dosya sonuyla karşılaşıldı.|  
|`BlobRequestFailed`|Blob hizmeti isteği tooaccess sayfa aralığı hello hello veya blok başarısız oldu.|  
|`IOFailed`|Bir disk veya ağ g/ç hatası hello sayfası aralık veya blok işlenirken hata oluştu.|  
|`Failed`|Başlangıç sayfası aralık veya blok işlenirken bilinmeyen bir hata oluştu.|  
|`Cancelled`|Önceki bir hata hello sayfası aralık veya blok işlenmesi durduruldu.|  
  
## <a name="metadata-status-codes"></a>Meta veriler durum kodları  
Merhaba aşağıdaki tabloda işleme blob meta verileri için hello durum kodları listelenmektedir.  
  
|Durum kodu|Açıklama|  
|-----------------|-----------------|  
|`Completed`|Merhaba meta veri işleme hatasız bitirdi.|  
|`FileNameInvalid`|Merhaba meta veri dosyası adı geçersiz.|  
|`FileNameTooLong`|Merhaba meta veri dosya adı çok uzun.|  
|`FileNotFound`|Merhaba meta veri dosyası bulunamadı.|  
|`FileAccessDenied`|Erişim toohello meta veri dosyası reddedildi.|  
|`Corrupted`|Merhaba meta veri dosyası bozuk (Merhaba içerik karması eşleşmiyor).|  
|`XmlReadFailed`|Merhaba meta veri içeriği toohello gerekli biçime uymuyor.|  
|`XmlWriteFailed`|Yazma hello meta veri XML başarısız oldu.|  
|`BlobRequestFailed`|meta veri tooaccess hello hello Blob hizmeti isteği başarısız oldu.|  
|`IOFailed`|Bir disk veya ağ g/ç hatası hello meta verileri işlenirken hata oluştu.|  
|`Failed`|Merhaba meta verileri işlenirken bilinmeyen bir hata oluştu.|  
|`Cancelled`|Önceki bir hata hello meta verilerinin işlenmesi durduruldu.|  
  
## <a name="properties-status-codes"></a>Özellikler durum kodları  
Merhaba aşağıdaki tabloda blob özellikleri işlemeye hello durum kodlarını listeler.  
  
|Durum kodu|Açıklama|  
|-----------------|-----------------|  
|`Completed`|Merhaba özellikleri işleme hatasız bitti.|  
|`FileNameInvalid`|Merhaba özellikleri dosya adı geçersiz.|  
|`FileNameTooLong`|Merhaba özellikleri dosya adı çok uzun.|  
|`FileNotFound`|Merhaba özellikleri dosyası bulunamadı.|  
|`FileAccessDenied`|Toohello özellikleri dosyasına erişim engellendi.|  
|`Corrupted`|Merhaba özellikleri dosya bozuk (Merhaba içerik karması eşleşmiyor).|  
|`XmlReadFailed`|Merhaba özellikleri içerik toohello gerekli biçime uymuyor.|  
|`XmlWriteFailed`|XML başarısız oldu hello özellikleri yazma.|  
|`BlobRequestFailed`|Özellikler tooaccess hello hello Blob hizmeti isteği başarısız oldu.|  
|`IOFailed`|Merhaba özellikleri işlenirken bir disk veya ağ g/ç hatası oluştu.|  
|`Failed`|Merhaba özellikleri işlenirken bilinmeyen bir hata oluştu.|  
|`Cancelled`|Önceki bir hata hello özelliklerini işlenmesi durduruldu.|  
  
## <a name="sample-logs"></a>Örnek günlükleri  
Merhaba, ayrıntılı günlüğü örneği verilmiştir.  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<DriveLog Version="2014-11-01">  
    <DriveId>WD-WMATV123456</DriveId>  
    <Blob Status="Completed">  
       <BlobPath>pictures/bob/wild/desert.jpg</BlobPath>  
       <FilePath>\Users\bob\Pictures\wild\desert.jpg</FilePath>  
       <Length>98304</Length>  
       <ImportDisposition Status="Created">overwrite</ImportDisposition>  
       <BlockList>  
          <Block Offset="0" Length="65536" Id="AAAAAA==" Hash=" 9C8AE14A55241F98533C4D80D85CDC68" Status="Completed"/>  
          <Block Offset="65536" Length="32768" Id="AQAAAA==" Hash=" DF54C531C9B3CA2570FDDDB3BCD0E27D" Status="Completed"/>  
       </BlockList>  
       <Metadata Status="Completed">  
          <GlobalPath Hash=" E34F54B7086BCF4EC1601D056F4C7E37">\Users\bob\Pictures\wild\metadata.xml</GlobalPath>  
       </Metadata>  
    </Blob>  
    <Blob Status="CompletedWithErrors">  
       <BlobPath>pictures/bob/animals/koala.jpg</BlobPath>  
       <FilePath>\Users\bob\Pictures\animals\koala.jpg</FilePath>  
       <Length>163840</Length>  
       <ImportDisposition Status="Overwritten">overwrite</ImportDisposition>  
       <PageRangeList>  
          <PageRange Offset="0" Length="65536" Hash="19701B8877418393CB3CB567F53EE225" Status="Completed"/>  
          <PageRange Offset="65536" Length="65536" Hash="AA2585F6F6FD01C4AD4256E018240CD4" Status="Corrupted"/>  
          <PageRange Offset="131072" Length="4096" Hash="9BA552E1C3EEAFFC91B42B979900A996" Status="Completed"/>  
       </PageRangeList>  
       <Properties Status="Completed">  
          <Path Hash="38D7AE80653F47F63C0222FEE90EC4E7">\Users\bob\Pictures\animals\koala.jpg.properties</Path>  
       </Properties>  
    </Blob>  
    <Status>CompletedWithErrors</Status>  
</DriveLog>  
```  
  
Merhaba karşılık gelen hata günlüğü aşağıda gösterilmiştir.  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<DriveLog Version="2014-11-01">  
    <DriveId>WD-WMATV6965824</DriveId>  
    <Blob Status="CompletedWithErrors">  
       <BlobPath>pictures/bob/animals/koala.jpg</BlobPath>  
       <FilePath>\Users\bob\Pictures\animals\koala.jpg</FilePath>  
       <Length>163840</Length>  
       <ImportDisposition Status="Overwritten">overwrite</ImportDisposition>  
       <PageRangeList>  
          <PageRange Offset="65536" Length="65536" Hash="AA2585F6F6FD01C4AD4256E018240CD4" Status="Corrupted"/>  
       </PageRangeList>  
    </Blob>  
    <Status>CompletedWithErrors</Status>  
</DriveLog>  
```

 Merhaba izleyin hata günlüğü içe aktarma işi için bir dosya hello alma sürücüde bulunamadı hakkında bir hata içerir. Sonraki bileşenleri Hello durumunu olduğuna dikkat edin `Cancelled`.  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog Version="2014-11-01">  
  <DriveId>9WM35C2V</DriveId>  
  <Blob Status="FileNotFound">  
    <BlobPath>pictures/animals/koala.jpg</BlobPath>  
    <FilePath>\animals\koala.jpg</FilePath>  
    <Length>30310</Length>  
    <ImportDisposition Status="Cancelled">rename</ImportDisposition>  
    <BlockList>  
      <Block Offset="0" Length="6062" Id="MD5/cAzn4h7VVSWXf696qp5Uaw==" Hash="700CE7E21ED55525977FAF7AAA9E546B" Status="Cancelled" />  
      <Block Offset="6062" Length="6062" Id="MD5/PEnGwYOI8LPLNYdfKr7kAg==" Hash="3C49C6C18388F0B3CB35875F2ABEE402" Status="Cancelled" />  
      <Block Offset="12124" Length="6062" Id="MD5/FG4WxqfZKuUWZ2nGTU2qVA==" Hash="146E16C6A7D92AE5166769C64D4DAA54" Status="Cancelled" />  
      <Block Offset="18186" Length="6062" Id="MD5/ZzibNDzr3IRBQENRyegeXQ==" Hash="67389B343CEBDC8441404351C9E81E5D" Status="Cancelled" />  
      <Block Offset="24248" Length="6062" Id="MD5/ZzibNDzr3IRBQENRyegeXQ==" Hash="67389B343CEBDC8441404351C9E81E5D" Status="Cancelled" />  
    </BlockList>  
  </Blob>  
  <Status>CompletedWithErrors</Status>  
</DriveLog>  
```

Merhaba bir dışa aktarma işi için aşağıdaki hata günlüğünü hello blob içeriğinin toohello sürücü yazıldı, ancak hello blob'un özellikleri dışarı aktarılırken bir hata oluştu gösterir.  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog Version="2014-11-01">  
  <DriveId>9WM35C3U</DriveId>  
  <Blob Status="CompletedWithErrors">  
    <BlobPath>pictures/wild/canyon.jpg</BlobPath>  
    <FilePath>\pictures\wild\canyon.jpg</FilePath>  
    <LastModified>2012-09-18T23:47:08Z</LastModified>  
    <Length>163840</Length>  
    <BlockList />  
    <Properties Status="Failed" />  
  </Blob>  
  <Status>CompletedWithErrors</Status>  
</DriveLog>  
```
  
## <a name="next-steps"></a>Sonraki adımlar
 
* [Depolama içeri/dışarı aktarma REST API'si](/rest/api/storageimportexport/)
