---
title: "Azure BLOB'ları, Azure dosyaları ya da Azure veri diski kullanmaya karar verme"
description: "Hangi teknolojinin kullanılacağını karar depolamak ve yardımcı olmak için Azure verilerine erişmek için farklı yollar öğrenin."
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
ms.openlocfilehash: 452030e2e55ebeae55be2bd858c59e45428c7621
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="deciding-when-to-use-azure-blobs-azure-files-or-azure-data-disks"></a>Azure BLOB'ları, Azure dosyaları ya da Azure veri diski kullanmaya karar verme

Microsoft Azure bulut verilerinize erişmek ve depolamak için Azure storage'da çeşitli özellikler sağlar. Bu makalede Azure dosyaları, Blobları ve veri diskleri kapsar ve bu özellikler arasında seçmenize yardımcı olmak için tasarlanmıştır.

## <a name="scenarios"></a>Senaryolar

Aşağıdaki tabloda, dosyaları, Blobları ve veri diskleri karşılaştırır ve örnek senaryolar her biri için uygun gösterir.

| Özellik | Açıklama | Kullanılması gereken durumlar |
|--------------|-------------|-------------|
| **Azure dosyaları** | İstemci kitaplıkları, bir SMB arabirim sağlar ve bir [REST arabirimi](/rest/api/storageservices/file-service-rest-api) her yerden erişim sağlayan depolanan dosyalar için. | "Kaldırın ve shift" istediğiniz bir uygulama zaten ve Azure'da çalışan diğer uygulamalar arasında veri paylaşımı için yerel dosya sistemi API'lerini kullanan bulut.<br/><br/>Geliştirme ve hata ayıklama birçok sanal makinelerden erişilmesi gereken araçları depolamak istediğiniz. |
| **Azure BLOB'ları** | İstemci kitaplıkları sağlar ve bir [REST arabirimi](/rest/api/storageservices/blob-service-rest-api) depolanabilir ve blok blobları, büyük bir ölçekte erişilen yapılandırılmamış veriler sağlar. | Akış desteklemek üzere uygulama ve rastgele erişim senaryoları istiyor.<br/><br/>Uygulama verileri her yerden erişim kullanabilmek ister. |
| **Azure veri diski** | İstemci kitaplıkları sağlar ve bir [REST arabirimi](/rest/api/compute/virtualmachines/virtualmachines-create-or-update) kalıcı olarak depolanır ve bir bağlı sanal sabit diskten erişilen veri sağlar. | Kaldırın ve okuma ve kalıcı diske veri yazmak için yerel dosya sistemi API'lerini kullanan uygulamalar shift istiyor.<br/><br/>Disk bağlı olduğu sanal makine dışında erişilebilmesi için gerekli olmayan veri depolamak istediğiniz. |

## <a name="comparison-files-and-blobs"></a>Karşılaştırma: Dosyaları ve BLOB'ları

Aşağıdaki tabloda Azure dosyaları Azure BLOB'ları ile karşılaştırır.  
  
||||  
|-|-|-|  
|**Özniteliği**|**Azure BLOB'ları**|**Azure dosyaları**|  
|Dayanıklılık seçenekleri|LRS, ZRS, GRS (ve RA-GRS yüksek kullanılabilirlik için)|LRS, GRS|  
|Erişilebilirlik|REST API'leri|REST API'leri<br /><br /> SMB 2.1 ve SMB 3.0 (standart dosya sistemi API'leri)|  
|Bağlantı|REST API'leri--dünya çapında|REST API'leri - dünya çapında<br /><br /> SMB 2.1--bölge içinde<br /><br /> SMB 3.0--dünya çapında|  
|Uç Noktalar|`http://myaccount.blob.core.windows.net/mycontainer/myblob`|`\\myaccount.file.core.windows.net\myshare\myfile.txt`<br /><br /> `http://myaccount.file.core.windows.net/myshare/myfile.txt`|  
|Dizinler|Düz ad alanı|Doğru dizin nesneleri|  
|Adları büyük/küçük harfe duyarlılık|Büyük küçük harfe duyarlı|Servis talebi küçük harflere duyarlı değildir, ancak servis talebi koruma|  
|Kapasite|En fazla 500 TB kapsayıcıları|5 TB dosya paylaşımları|  
|Aktarım hızı|Blok blobu başına en fazla 60 MB/sn|Paylaşım başına en fazla 60 MB/sn|  
|Nesne boyutu|En fazla 200 GB/blok blobu|1 TB/dosya kadar|  
|Faturalanan kapasite|Yazılan bayt dayalı|Dosya boyutuna göre|  
|İstemci kitaplıkları|Birden çok dil|Birden çok dil|  
  
## <a name="comparison-files-and-data-disks"></a>Karşılaştırma: Dosyaları ve veri diskleri

Azure dosyaları Azure veri diski tamamlar. Bir veri diski aynı anda yalnızca bir Azure sanal makineye bağlanabilir. Veri diskleri sayfa bloblar olarak Azure Storage'da depolanan sabit biçimli VHD'lerin ve sanal makine tarafından dayanıklı verileri depolamak için kullanılır. Azure dosyaları dosya paylaşımları yerel disk (yerel dosya sistemi API'lerini kullanarak) erişildiği gibi aynı şekilde erişilebilir ve çok sayıda sanal makine genelinde paylaşılabilir.  
 
Aşağıdaki tabloda Azure dosyaları Azure veri diski ile karşılaştırır.  
 
||||  
|-|-|-|  
|**Özniteliği**|**Azure veri diski**|**Azure dosyaları**|  
|Kapsam|Tek bir sanal makine için özel|Birden çok sanal makine arasında paylaşılan erişim|  
|Anlık görüntüler ve kopyalama|Evet|Hayır|  
|Yapılandırma|Sanal makine başlangıçta bağlı|Sanal makine başlatıldıktan sonra bağlı|  
|Kimlik Doğrulaması|Yerleşik|NET kullanmak üzere ayarlanmış|  
|Temizleme|Otomatik|El ile|  
|REST kullanarak erişimi|VHD içindeki dosyaları erişilemiyor|Bir paylaşımda depolanan dosyalara erişilebilir|  
|En büyük boyutu|1 TB disk|5 TB dosya paylaşımı ve 1 TB Dosya paylaşımındaki|  
|En fazla 8KB IOPS|500 IOPS|1000 IOPS|  
|Aktarım hızı|Disk başına en fazla 60 MB/sn|Dosya Paylaşımı başına en fazla 60 MB/sn|  

## <a name="next-steps"></a>Sonraki adımlar

Nasıl depolandığını ve erişilen hakkında kararları verirken ayrıca maliyetleri söz konusu düşünmeniz gerekir. Daha fazla bilgi için bkz: [Azure Storage fiyatlandırması](https://azure.microsoft.com/pricing/details/storage/).
  
SMB özelliklerinden bazıları bulut için geçerli değildir. Daha fazla bilgi için bkz: [Azure dosya hizmeti tarafından desteklenmeyen özellikleri](/rest/api/storageservices/features-not-supported-by-the-azure-file-service).
  
Veri diskleri hakkında daha fazla bilgi için bkz: [diskleri ve görüntüleri yönetme](../../virtual-machines/windows/about-disks-and-vhds.md) ve [bir Windows sanal makineye bir veri diski Ekle nasıl](../../virtual-machines/windows/classic/attach-disk.md).