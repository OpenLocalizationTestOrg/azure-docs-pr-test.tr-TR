---
title: "SSIS bağlayıcıları kullanarak Azure Blob depolama biriminden aaaMove veri tooor | Microsoft Docs"
description: "Veri tooor SSIS bağlayıcıları kullanarak Azure Blob depolama alanından taşıyın."
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 96a1b5fb-34d1-4b9b-8d99-2bb8289e0398
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 15068af1c69f11e74e109ee5ae2b9f1a674ea388
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooor-from-azure-blob-storage-using-ssis-connectors"></a>SSIS bağlayıcıları kullanarak Azure Blob depolama alanından veri tooor Taşı
Merhaba [Azure için SQL Server Integration Services Feature Pack](https://msdn.microsoft.com/library/mt146770.aspx) bileşenleri tooconnect tooAzure, Azure ve şirket içi veri kaynakları ve Azure'da depolanan verileri işlemek arasında veri aktarımı sağlar.

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

Müşterilerin şirket içi veri hello bulutunu taşırken, bunlar tüm Azure hizmeti tooleverage hello tam güç Azure teknolojilerinin hello takımının erişebilir. Bu, örneğin, Azure Machine Learning veya Hdınsight kümesinde kullanılabilir.

Bu genellikle Merhaba hello ilk adım olabilir [SQL](machine-learning-data-science-process-sql-walkthrough.md) ve [Hdınsight](machine-learning-data-science-process-hive-walkthrough.md) izlenecek yollar.

Karma veri tümleştirme senaryolarına genel tartışma SSIS tooaccomplish iş kullanan kurallı senaryoları için gereken için bkz: [Bunun SQL Server Integration Services Feature Pack Azure ile daha](http://blogs.msdn.com/b/ssis/archive/2015/06/25/doing-more-with-sql-server-integration-services-feature-pack-for-azure.aspx) blogu.

> [!NOTE]
> Bir tam giriş tooAzure blob depolama çok başvuran[Azure Blob Temelleri](../storage/blobs/storage-dotnet-how-to-use-blobs.md) ve çok[Azure Blob hizmeti](https://msdn.microsoft.com/library/azure/dd179376.aspx).
> 
> 

## <a name="prerequisites"></a>Ön koşullar
tooperform başlangıç görevleri bu makalede açıklanan bir Azure aboneliği ve kurulu bir Azure depolama hesabınız olması gerekir. Azure depolama hesabı adı ve hesap anahtarı tooupload bilmeniz veya veri indirin.

* Yukarı tooset bir **Azure aboneliği**, bkz: [ücretsiz bir aylık deneme](https://azure.microsoft.com/pricing/free-trial/).
* Oluşturma yönergeleri için bir **depolama hesabı** ve hesabı ve anahtarı bilgilerini almak için bkz: [Azure storage hesapları hakkında](../storage/common/storage-create-storage-account.md).

toouse hello **SSIS Bağlayıcılar**, karşıdan yüklemeniz gerekir:

* **SQL Server 2014 veya 2016 standart (veya üstü)**: Install SQL Server Integration Services içerir.
* **Microsoft SQL Server 2014 veya 2016 tümleştirme hizmetleri özellik paketi Azure**: Bunlar, sırasıyla hello indirilebilir [SQL Server 2014 Integration Services](http://www.microsoft.com/download/details.aspx?id=47366) ve [SQL Server 2016 tümleştirmesi Hizmetleri](https://www.microsoft.com/download/details.aspx?id=49492) sayfaları.

> [!NOTE]
> SSIS SQL Server ile birlikte yüklenir, ancak hello Express sürümüne dahil değil. Hangi uygulamaların çeşitli SQL Server sürümlerinde bulunan hakkında daha fazla bilgi için bkz: [SQL Server sürümleri](http://www.microsoft.com/en-us/server-cloud/products/sql-server-editions/)
> 
> 

SSIS üzerinde eğitim malzemelerini için bkz: [SSIS üzerinde ellerini eğitim](http://www.microsoft.com/download/details.aspx?id=20766)

Hakkında bilgi için tooget yukarı ve-çalışan SISS toobuild basit ayıklama, dönüştürme ve yükleme (ETL) paketleri kullanarak bkz [SSIS Öğreticisi: basit bir ETL paket oluşturma](https://msdn.microsoft.com/library/ms169917.aspx).

## <a name="download-nyc-taxi-dataset"></a>NYC ücreti dataset indirin
Merhaba açıklanan örneği burada kullanmak genel kullanıma açık bir veri kümesi--hello [NYC ücreti dönüşleri](http://www.andresmh.com/nyctaxitrips/) veri kümesi. yaklaşık 173 milyon ücreti üstündeçalýþan NYC içinde hello yılın 2013 Hello dataset oluşur. İki tür veri vardır: seyahat ayrıntıları veri ve ücreti verileri. Her ay için bir dosya gibi her biri sıkıştırılmamış yaklaşık 2 GB ise tüm 24 dosyalarında sahibiz.

## <a name="upload-data-tooazure-blob-storage"></a>Veri tooAzure blob depolama yükleme
Merhaba SSIS kullanarak toomove veri özellik paketi şirket içi tooAzure blob depolama biriminden, hello örneği kullanırız [ **Azure Blob karşıya yükleme görev**](https://msdn.microsoft.com/library/mt146776.aspx), burada gösterilen:

![yapılandırma verileri-Bilim-vm](./media/machine-learning-data-science-move-data-to-azure-blob-using-ssis/ssis-azure-blob-upload-task.png)

Görev kullanır hello hello parametreler burada açıklanan şunlardır:

| Alan | Açıklama |
| --- | --- |
| **AzureStorageConnection** |Yeni bir toowhere hello blob dosyaları işaret tooan Azure depolama hesabı başvuran bir barındırıldığı oluşturur veya mevcut bir Azure depolama Bağlantı Yöneticisi belirtir. |
| **BlobContainer** |Karşıya hello dosyaları BLOB olarak tutun hello blob kapsayıcısı Hello adını belirtir. |
| **BlobDirectory** |Bir blok blobu olarak hello karşıya yüklenen dosyanın depolandığı hello blob dizini belirtir. Merhaba blob dizini sanal hiyerarşik bir yapıdır. Merhaba blob zaten varsa, BT IA değiştirildi. |
| **LocalDirectory** |Karşıya hello dosyaları toobe içeren hello yerel dizini belirtir. |
| **Dosya adı** |Bir ad filtre tooselect dosyaları hello belirtilen ad deseni ile belirtir. Örneğin, MySheet\*.xls\* MySheet001.xls ve MySheetABC.xlsx gibi dosyalarını içerir |
| **TimeRangeFrom/TimeRangeTo** |Bir zaman aralığı filtresini belirtir. Değiştirilen dosyaları sonra *TimeRangeFrom* ve önce *TimeRangeTo* dahil edilir. |

> [!NOTE]
> Merhaba **AzureStorageConnection** kimlik bilgilerine ihtiyacınız toobe doğru ve hello **BlobContainer** hello aktarımı denenmeden önce mevcut olması gerekir.
> 
> 

## <a name="download-data-from-azure-blob-storage"></a>Verileri Azure blob depolama alanından karşıdan yükleme
Azure blob depolama tooon içi depolama SSIS ile toodownload verileri kullan hello örneği [Azure Blob karşıya yükleme görev](https://msdn.microsoft.com/library/mt146779.aspx).

## <a name="more-advanced-ssis-azure-scenarios"></a>Daha gelişmiş SSIS Azure senaryoları
Merhaba SSIS özellik paketi için daha karmaşık akışları toobe birlikte paketleme görevler tarafından işlenen sağlar. Örneğin, hello blob verilerini çıktısı geri tooa blob ve şirket içi tooon depolama karşıdan yüklenemedi doğrudan bir Hdınsight kümesine, akış. SSIS Hive veya Pig işleri ek SSIS bağlayıcıları kullanarak bir Hdınsight kümesine çalıştırabilirsiniz:

* bir Azure hdınsight'ta Hive betiğini küme SSIS, kullanım toorun [Azure Hdınsight Hive görev](https://msdn.microsoft.com/library/mt146771.aspx).
* Pig betiği Azure hdınsight küme SSIS, kullanım toorun [Azure Hdınsight Pig görev](https://msdn.microsoft.com/library/mt146781.aspx).

