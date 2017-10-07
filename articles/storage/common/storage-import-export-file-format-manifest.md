---
title: "aaaAzure içeri/dışarı aktarma bildirim dosyasının biçimi | Microsoft Docs"
description: "Azure Blob storage blobları ve dosyaları hello içeri/dışarı aktarma hizmeti içeri veya dışarı bir işlemde bir sürücüde arasında hello eşleme açıklayan Hello hello sürücü bildirim dosyası biçimi hakkında öğrenin."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: f3119e1c-2c25-48ad-8752-a6ed4adadbb0
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: d7e5e1990482916f7ff5f891c97343b52e82b2f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-importexport-service-manifest-file-format"></a>Azure içeri/dışarı aktarma hizmeti bildirim dosyası biçimi
Merhaba sürücü bildirim dosyası Azure Blob storage blobları ve içe veya dışa aktarma işi kapsayan sürücüsündeki dosyaları arasında hello eşleme açıklar. Bir alma işlemi için hello bildirim dosyası hello sürücü hazırlama işleminin bir parçası olarak oluşturulur ve hello sürücü toohello Azure veri merkezine gönderilmeden önce hello sürücüsünde depolanır. Bir dışa aktarma işlemi sırasında hello bildirimi oluşturulur ve hello Azure içeri/dışarı aktarma hizmeti tarafından hello sürücüde depolanan.  
  
Her ikisi de içeri ve dışarı aktarma işleri, hello sürücü bildirim dosyasının depolandığı için üzerinde hello alma veya sürücü verme; olmayan herhangi bir API işlemi aracılığıyla toohello hizmet aktarılan.  
  
Merhaba hello genel sürücü bildirim dosyasının biçimi açıklanmıştır:  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<DriveManifest Version="2014-11-01">  
  <Drive>  
    <DriveId>drive-id</DriveId>  
    import-export-credential  
  
    <!-- First Blob List -->  
    <BlobList>  
      <!-- Global properties and metadata that applies tooall blobs -->  
      [<MetadataPath Hash="md5-hash">global-metadata-file-path</MetadataPath>]  
      [<PropertiesPath   
        Hash="md5-hash">global-properties-file-path</PropertiesPath>]  
  
      <!-- First Blob -->  
      <Blob>  
        <BlobPath>blob-path-relative-to-account</BlobPath>  
        <FilePath>file-path-relative-to-transfer-disk</FilePath>  
        [<ClientData>client-data</ClientData>]  
        [<Snapshot>snapshot</Snapshot>]  
        <Length>content-length</Length>  
        [<ImportDisposition>import-disposition</ImportDisposition>]  
        page-range-list-or-block-list          
        [<MetadataPath Hash="md5-hash">metadata-file-path</MetadataPath>]  
        [<PropertiesPath Hash="md5-hash">properties-file-path</PropertiesPath>]  
      </Blob>  
  
      <!-- Second Blob -->  
      <Blob>  
      . . .  
      </Blob>  
    </BlobList>  
  
    <!-- Second Blob List -->  
    <BlobList>  
    . . .  
    </BlobList>  
  </Drive>  
</DriveManifest>  
  
import-export-credential ::=   
  <StorageAccountKey>storage-account-key</StorageAccountKey> | <ContainerSas>container-sas</ContainerSas>  
  
page-range-list-or-block-list ::=   
  page-range-list | block-list  
  
page-range-list ::=   
    <PageRangeList>  
      [<PageRange Offset="page-range-offset" Length="page-range-length"   
       Hash="md5-hash"/>]  
      [<PageRange Offset="page-range-offset" Length="page-range-length"   
       Hash="md5-hash"/>]  
    </PageRangeList>  
  
block-list ::=  
    <BlockList>  
      [<Block Offset="block-offset" Length="block-length" [Id="block-id"]  
       Hash="md5-hash"/>]  
      [<Block Offset="block-offset" Length="block-length" [Id="block-id"]   
       Hash="md5-hash"/>]  
    </BlockList>  

```

## <a name="manifest-xml-elements-and-attributes"></a>Bildirim XML öğeleri ve öznitelikleri

Aşağıdaki tablonun hello Hello veri öğeleri ve öznitelikleri hello sürücü bildirim XML biçimi belirtilir.  
  
|XML öğesi|Tür|Açıklama|  
|-----------------|----------|-----------------|  
|`DriveManifest`|Kök öğesi|Merhaba bildirim dosyasının kök öğesinin Hello. Diğer tüm öğeleri hello dosyasındaki altında bu öğesidir.|  
|`Version`|Öznitelik, dize|Merhaba bildirim dosyası Hello sürümü.|  
|`Drive`|İç içe geçmiş XML öğesi|Her sürücü için Hello bildirimi içerir.|  
|`DriveId`|Dize|Merhaba sürücü Hello benzersiz sürücü tanımlayıcısı. Merhaba sürücü tanımlayıcı hello sürücü seri numarası için sorgulanarak bulunur. Merhaba sürücü seri numarası genellikle hello sürücü dışında hello yazılır. Merhaba `DriveID` öğesi önce görünmelidir `BlobList` hello bildirim dosyasında öğesi.|  
|`StorageAccountKey`|Dize|İçeri aktarma bulunuyorsa ve yalnızca iş için gereken `ContainerSas` belirtilmedi. Merhaba hesap anahtarı hello Azure depolama hesabı için hello işle ilişkili.<br /><br /> Bu öğe bir verme işlemi için hello bildirimindeki atlanır.|  
|`ContainerSas`|Dize|İçeri aktarma bulunuyorsa ve yalnızca iş için gereken `StorageAccountKey` belirtilmedi. Merhaba kapsayıcı SAS hello işle ilişkili hello BLOB'ları erişmek için. Bkz: [Put işlemini](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) , biçimi için. Bu öğe bir verme işlemi için hello bildirimindeki atlanır.|  
|`ClientCreator`|Dize|Merhaba XML dosyası oluşturulan hello istemci belirtir. Bu değer hello içeri/dışarı aktarma hizmeti tarafından yorumlanmaz.|  
|`BlobList`|İç içe geçmiş XML öğesi|Merhaba alma parçası olan veya iş verme BLOB listesini içerir. Bir blob listedeki her bir blob paylaşımları hello aynı meta verileri ve özellikleri.|  
|`BlobList/MetadataPath`|Dize|İsteğe bağlı. BLOB alma işlemi için hello blob listesinde üzerinde ayarlanacak hello varsayılan meta verileri içeren hello diskteki dosyasının Hello göreli yolunu belirtir. Bu meta veriler isteğe bağlı olarak bir blob tarafından blob temelinde geçersiz kılınabilir.<br /><br /> Bu öğe bir verme işlemi için hello bildirimindeki atlanır.|  
|`BlobList/MetadataPath/@Hash`|Öznitelik, dize|Merhaba meta veri dosyası için Hello Base16 kodlu MD5 karma değeri belirtir.|  
|`BlobList/PropertiesPath`|Dize|İsteğe bağlı. BLOB alma işlemi için hello blob listesinde üzerinde ayarlanacak hello varsayılan özelliklerini içeren hello diskteki dosyasının Hello göreli yolunu belirtir. Bu özellikleri isteğe bağlı olarak bir blob tarafından blob temelinde geçersiz kılınabilir.<br /><br /> Bu öğe bir verme işlemi için hello bildirimindeki atlanır.|  
|`BlobList/PropertiesPath/@Hash`|Öznitelik, dize|Merhaba özellikleri dosya için Hello Base16 kodlu MD5 karma değeri belirtir.|  
|`Blob`|İç içe geçmiş XML öğesi|Her bir blob listedeki her bir blob hakkında bilgiler içerir.|  
|`Blob/BlobPath`|Dize|Merhaba kapsayıcı adı ile başlayan hello göreli URI toohello blob. Merhaba blob kök kapsayıcısında ise, ile başlamalıdır `$root`.|  
|`Blob/FilePath`|Dize|Merhaba sürücüde Hello göreli yol toohello dosyası belirtir. Dışarı aktarma işleri için hello blob yolu mümkünse hello dosya yolu için kullanılır; *örneğin*, `pictures/bob/wild/desert.jpg` çok verilecek`\pictures\bob\wild\desert.jpg`. Ancak, NTFS adları toohello sınırlamaları, bir blob dışarı aktarılan tooa dosya hello blob yolu benzer olmayan bir yola sahip olabilir.|  
|`Blob/ClientData`|Dize|İsteğe bağlı. Merhaba müşteriden açıklamaları içerir. Bu değer hello içeri/dışarı aktarma hizmeti tarafından yorumlanmaz.|  
|`Blob/Snapshot`|Tarih saat|Dışarı aktarma işleri için isteğe bağlıdır. Dışarı aktarılan blob anlık görüntü için başlangıç anlık görüntü tanımlayıcısını belirtir.|  
|`Blob/Length`|Tamsayı|Merhaba toplam hello blob uzunluğu bayt cinsinden belirtir. Merhaba değeri bir blok blobu için too200 GB ve bir sayfa blob'u too1 TB yukarı olabilir. Bir sayfa blob'u için bu değer 512 birden fazla olmalıdır.|  
|`Blob/ImportDisposition`|Dize|Dışarı aktarma işleri için atlanmış içeri aktarma işi için isteğe bağlıdır. Bu, bir blob zaten aynı adı hello bulunduğu hello içeri/dışarı aktarma hizmeti hello durum içe aktarma işi için nasıl yöneteceğini belirtir. Bu değer hello alma bildirimden atlanırsa hello varsayılan değerdir `rename`.<br /><br /> Bu öğe için Hello değerleri şunlardır:<br /><br /> -   `no-overwrite`: Hedef blob zaten ile hello varsa aynı ada hello içeri aktarma işlemi atlar bu dosyayı içeri aktarma.<br />-   `overwrite`: Tüm var olan hedef blob tamamen hello yeni içeri aktarılan dosya tarafından üzerine yazılır.<br />-   `rename`: hello yeni blob karşıya değiştirilmiş bir ada sahip olur.<br /><br /> yeniden adlandırma kuralı hello aşağıdaki gibidir:<br /><br /> -Hello blob adı noktayla içermiyorsa, yeni bir ad eklenerek oluşturulur `(2)` bu yeni ad Ayrıca varolan bir blob adla sonra çakışırsa toohello özgün blob adı; `(3)` yerine eklenen `(2)`; ve benzeri.<br />Merhaba blob adı noktayla içeriyorsa hello son nokta aşağıdaki hello bölümü hello uzantı adı olarak kabul edilir. Yordam, yukarıda benzer toohello `(2)` önce eklenen son nokta toogenerate yeni bir ad hello; hello yeni adı hala varolan bir blob adla çakışırsa, hello hizmeti çalışır `(3)`, `(4)`ve benzeri bir çakışmayan kadar ad bulunamadı.<br /><br /> Bazı örnekler:<br /><br /> Merhaba blob `BlobNameWithoutDot` adlandırılacak:<br /><br /> `BlobNameWithoutDot (2)  // if BlobNameWithoutDot exists`<br /><br /> `BlobNameWithoutDot (3)  // if both BlobNameWithoutDot and BlobNameWithoutDot (2) exist`<br /><br /> Merhaba blob `Seattle.jpg` adlandırılacak:<br /><br /> `Seattle (2).jpg  // if Seattle.jpg exists`<br /><br /> `Seattle (3).jpg  // if both Seattle.jpg and Seattle (2).jpg exist`|  
|`PageRangeList`|İç içe geçmiş XML öğesi|Bir sayfa blob'u için gereklidir.<br /><br /> İçin alma işlemi, içe aktarılan dosya toobe bayt aralıkları listesi belirtir. Her sayfası aralık bir uzaklık ve uzunluk hello bölgesinin bir MD5 karma değeri ile birlikte hello sayfa aralığını açıklayan hello kaynak dosyasında tarafından tanımlanır. Merhaba `Hash` bir sayfa aralığının özniteliği gereklidir. Merhaba hizmet hello blob hello verilerde hello karmasını hesaplanan hello MD5 karma değeri hello sayfa aralığından eşleştiğini doğrular. Herhangi bir sayıda sayfa aralıklarını kullanılan toodescribe too1 TB toplam boyutu hello ile içeri aktarma için bir dosya olabilir. Tüm sayfa aralıklarını tarafından uzaklığı sıralanmalıdır ve hiçbir üst üste geliyor verilir.<br /><br /> Bir verme işlemi için henüz bir blob bayt aralığı kümesi toohello sürücü dışarı belirtir.<br /><br /> Hello sayfa aralıklarını birlikte bir blob veya dosya yalnızca alt aralığını kapsayan.  herhangi bir sayfa aralığı tarafından kapsanmayan hello dosyasının Hello geri kalan bölümü beklenen ve içeriği tanımlanmamış olabilir.|  
|`PageRange`|XML öğesi|Sayfa aralığını temsil eder.|  
|`PageRange/@Offset`|Öznitelik, tamsayı|Merhaba uzaklığı hello aktarımı dosya ve burada hello sayfa aralığı belirtilen hello blob başlar belirtir. Bu değer 512'ın katları olmalıdır.|  
|`PageRange/@Length`|Öznitelik, tamsayı|Merhaba sayfa aralığı Hello uzunluğunu belirtir. Bu değer birden fazla 512 ve en fazla 4 MB olmalıdır.|  
|`PageRange/@Hash`|Öznitelik, dize|Merhaba sayfa aralığı için Hello Base16 kodlu MD5 karma değeri belirtir.|  
|`BlockList`|İç içe geçmiş XML öğesi|Adlandırılmış bloklara sahip bir blok blobu için gereklidir.<br /><br /> Bir alma işlemi için bir Azure depolama alanına içeri aktarılacak blokları kümesi hello engelleme listesini belirtir. Bir dışarı aktarma işlemi için burada her bloğu hello verme diskteki hello dosyasındaki zamandır saklanan hello engelleme listesi belirtir. Her blok uzaklığı hello dosya ve blok uzunluğu tarafından açıklanan; Her blok blok Kimliği özniteliği tarafından ayrıca adlandırılır ve hello bloğu için MD5 karma değeri içerir. Too50 000 blokları kullanılan toodescribe blob olabilir.  Tüm bloklar gerekir sıralı uzaklık ve birlikte kapak hello eksiksiz hello dosyasının *yani*, blokları boşluksuz olmalıdır. Her bloğu olmalıdır en fazla 64 MB, hello blok kimliği hello blob ise tüm yok veya tüm sunmak. Blok kimlikleri gerekli toobe Base64 ile kodlanmış dizelerdir. Bkz: [yerleştirme blok](/rest/api/storageservices/put-block) daha fazla blok kimliği için gereksinimleri için.|  
|`Block`|XML öğesi|Bloğunu temsil eder.|  
|`Block/@Offset`|Öznitelik, tamsayı|Belirtilen blok hello başladığı hello uzaklığını belirtir.|  
|`Block/@Length`|Öznitelik, tamsayı|Merhaba bloğunda Hello bayt belirtir; Bu değer, en fazla 4 MB olmalıdır.|  
|`Block/@Id`|Öznitelik, dize|Merhaba hello bloğu için blok Kimliğini temsil eden bir dize belirtir.|  
|`Block/@Hash`|Öznitelik, dize|Merhaba Base16 kodlu MD5 karma hello bloğunun belirtir.|  
|`Blob/MetadataPath`|Dize|İsteğe bağlı. Meta veri dosyasının Hello göreli yolunu belirtir. Bir içeri aktarma sırasında hello meta verileri hello hedef blob üzerinde ayarlanır. Bir dışa aktarma işlemi sırasında hello blob'un meta verileri hello meta veri dosyası hello sürücüsünde depolanır.|  
|`Blob/MetadataPath/@Hash`|Öznitelik, dize|Merhaba Base16 kodlu MD5 karma hello blob'un meta veri dosyasının belirtir.|  
|`Blob/PropertiesPath`|Dize|İsteğe bağlı. Özellikler dosyasının Hello göreli yolunu belirtir. Bir içeri aktarma sırasında hello özellikleri hello hedef blob üzerinde ayarlanır. Bir dışa aktarma işlemi sırasında hello blob özellikleri hello özellikleri dosya hello sürücüsünde depolanır.|  
|`Blob/PropertiesPath/@Hash`|Öznitelik, dize|Merhaba Base16 kodlu MD5 karması hello blob'un özellikleri dosyasının belirtir.|  
  
## <a name="next-steps"></a>Sonraki adımlar
 
* [Depolama içeri/dışarı aktarma REST API'si](/rest/api/storageimportexport/)
