---
title: "toouse Azure BLOB'olduğunda aaaDeciding, Azure dosyaları ya da Azure veri diski"
description: "Hangi teknoloji toouse karar hello farklı şekillerde toostore ve erişim verilerinizi Azure toohelp öğrenin."
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: robinsh
ms.openlocfilehash: 6109affe41e98ed459616a4f91064ded0c74428d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deciding-when-toouse-azure-blobs-azure-files-or-azure-data-disks"></a>Toouse Azure BLOB'olduğunda karar verme, Azure dosyaları ya da Azure veri diski

Microsoft Azure, verilerinizi hello bulutta erişmek ve depolamak için Azure storage'da çeşitli özellikler sağlar. Bu makalede, Azure dosyaları, Blobları ve veri diskleri kapsar ve bu özellikler arasında seçtiğiniz tasarlanmış toohelp olduğu.

## <a name="scenarios"></a>Senaryolar

Aşağıdaki tablonun hello dosyaları, Blobları ve veri diskleri karşılaştırır ve örnek senaryolar her biri için uygun gösterir.

| Özellik | Açıklama | Zaman toouse |
|--------------|-------------|-------------|
| **Azure dosyaları** | İstemci kitaplıkları, bir SMB arabirim sağlar ve bir [REST arabirimi](/rest/api/storageservices/file-service-rest-api) toostored dosyaları, her yerden erişim sağlar. | Çok "kaldırın ve shift" istediğiniz zaten hello yerel dosya sistemi API'leri tooshare verilerini ve Azure'da çalışan diğer uygulamalar arasındaki kullanan bir uygulama toohello bulut.<br/><br/>Toostore geliştirme ve hata ayıklama birçok sanal makinelerden erişilen toobe gereken araçları istiyor. |
| **Azure BLOB'ları** | İstemci kitaplıkları sağlar ve bir [REST arabirimi](/rest/api/storageservices/blob-service-rest-api) yapılandırılmamış verileri sağlayan çok saklanabilir ve blok blobları, büyük bir ölçekte erişilebilir. | Uygulama toosupport akış ve rastgele erişim senaryoları istiyor.<br/><br/>Toobe mümkün tooaccess uygulama verilerini yerden istiyor. |
| **Azure veri diski** | İstemci kitaplıkları sağlar ve bir [REST arabirimi](/rest/api/compute/virtualmachines/virtualmachines-create-or-update) kalıcı olarak depolanır ve bir bağlı sanal sabit diskten erişilen veri toobe sağlar. | Yerel dosya sistemi API'leri tooread kullanın ve veri toopersistent diskleri yazma uygulamaları kaydırma ve toolift istiyorsunuz.<br/><br/>Dış hello sanal makine toowhich hello diskten erişilen gerekli toobe değil toostore veri bağlantılı istiyor. |

## <a name="comparison-files-and-blobs"></a>Karşılaştırma: Dosyaları ve BLOB'ları

Aşağıdaki tablonun hello Azure dosyaları Azure BLOB'ları ile karşılaştırır.  
  
||||  
|-|-|-|  
|**Özniteliği**|**Azure BLOB'ları**|**Azure dosyaları**|  
|Dayanıklılık seçenekleri|LRS, ZRS, GRS (ve RA-GRS yüksek kullanılabilirlik için)|LRS, GRS|  
|Erişilebilirlik|REST API'leri|REST API'leri<br /><br /> SMB 2.1 ve SMB 3.0 (standart dosya sistemi API'leri)|  
|Bağlantı|REST API'leri--dünya çapında|REST API'leri - dünya çapında<br /><br /> SMB 2.1--bölge içinde<br /><br /> SMB 3.0--dünya çapında|  
|Uç Noktalar|`http://myaccount.blob.core.windows.net/mycontainer/myblob`|`\\myaccount.file.core.windows.net\myshare\myfile.txt`<br /><br /> `http://myaccount.file.core.windows.net/myshare/myfile.txt`|  
|Dizinler|Düz ad alanı|Doğru dizin nesneleri|  
|Adları büyük/küçük harfe duyarlılık|Büyük küçük harfe duyarlı|Servis talebi küçük harflere duyarlı değildir, ancak servis talebi koruma|  
|Kapasite|Too500 TB kapsayıcıları|5 TB dosya paylaşımları|  
|Aktarım hızı|Too60 MB/sn blok blobu başına|Too60 MB/sn paylaşım başına|  
|Nesne boyutu|Too200 GB/blok blobu|Too1TB/dosyasını yedekleyin|  
|Faturalanan kapasite|Yazılan bayt dayalı|Dosya boyutuna göre|  
|İstemci kitaplıkları|Birden çok dil|Birden çok dil|  
  
## <a name="comparison-files-and-data-disks"></a>Karşılaştırma: Dosyaları ve veri diskleri

Azure dosyaları Azure veri diski tamamlar. Bir veri diski yalnızca aynı anda ekli tooone Azure sanal makine olabilir. Veri diskleri sayfa bloblar olarak Azure Storage'da depolanan sabit biçimli VHD'lerin ve hello sanal makine toostore dayanıklı veri tarafından kullanılır. Azure dosyaları dosya paylaşımları erişilebilir hello yerel disk (yerel dosya sistemi API'lerini kullanarak) yolu erişildiği gibi aynı hello ve çok sayıda sanal makine genelinde paylaşılabilir.  
 
Aşağıdaki tablonun hello Azure dosyaları Azure veri diski ile karşılaştırır.  
 
||||  
|-|-|-|  
|**Özniteliği**|**Azure veri diski**|**Azure dosyaları**|  
|Kapsam|Özel tooa tek bir sanal makine|Birden çok sanal makine arasında paylaşılan erişim|  
|Anlık görüntüler ve kopyalama|Evet|Hayır|  
|Yapılandırma|Merhaba sanal makine başlangıçta bağlı|Merhaba sanal makine başlatıldıktan sonra bağlı|  
|Kimlik Doğrulaması|Yerleşik|NET kullanmak üzere ayarlanmış|  
|Temizleme|Otomatik|El ile|  
|REST kullanarak erişimi|Merhaba VHD içindeki dosyaları erişilemiyor|Bir paylaşımda depolanan dosyalara erişilebilir|  
|En büyük boyutu|1 TB disk|5 TB dosya paylaşımı ve 1 TB Dosya paylaşımındaki|  
|En fazla 8KB IOPS|500 IOPS|1000 IOPS|  
|Aktarım hızı|Too60 MB/sn Disk başına|Too60 MB/sn her dosya paylaşımına|  

## <a name="next-steps"></a>Sonraki adımlar

Nasıl depolandığını ve erişilen hakkında kararları verirken de hello maliyetleri söz konusu dikkate almalısınız. Daha fazla bilgi için bkz: [Azure Storage fiyatlandırması](https://azure.microsoft.com/pricing/details/storage/).
  
SMB özelliklerinden bazıları geçerli toohello bulut olup olmadığı. Daha fazla bilgi için bkz: [hello Azure dosya hizmeti tarafından desteklenmeyen özellikleri](/rest/api/storageservices/features-not-supported-by-the-azure-file-service).
  
Veri diskleri hakkında daha fazla bilgi için bkz: [diskleri ve görüntüleri yönetme](storage-about-disks-and-vhds-linux.md) ve [nasıl tooAttach veri diski tooa Windows sanal makine](../virtual-machines/windows/classic/attach-disk.md).
