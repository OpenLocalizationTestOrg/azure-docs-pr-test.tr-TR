---
title: "aaaAzure Data Lake Store bölgeler arası geçiş | Microsoft Docs"
description: "Azure Data Lake Store için bölgeler arası geçiş hakkında bilgi edinin."
services: data-lake-store
documentationcenter: 
author: swums
manager: amitkul
editor: swums
ms.assetid: ebde7b9f-2e51-4d43-b7ab-566417221335
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/27/2017
ms.author: stewu
ms.openlocfilehash: 561ac821c1bd555886035867678cb685997564eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-data-lake-store-across-regions"></a>Data Lake Store bölgeler arasında geçirme

Azure Data Lake Store yeni bölgelerde kullanılabilir hale geldiğinde, bir kerelik geçiş, hello yeni bölge tootake avantajlarından toodo seçebilirsiniz. Planlama ve hello Geçişi tamamlamak hangi tooconsider öğrenin.

## <a name="prerequisites"></a>Ön koşullar

* **Bir Azure aboneliği**. Daha fazla bilgi için bkz: [ücretsiz Azure hesabınızı bugün oluşturmak](https://azure.microsoft.com/pricing/free-trial/).
* **Bir Data Lake Store hesabı iki farklı bölgelerdeki**. Daha fazla bilgi için bkz: [Azure Data Lake Store ile çalışmaya başlama](data-lake-store-get-started-portal.md).
* **Azure Data Factory**. Daha fazla bilgi için bkz: [giriş tooAzure Data Factory](../data-factory/data-factory-introduction.md).


## <a name="migration-considerations"></a>Geçiş konuları

İlk olarak, yazar okur ve Data Lake Store'da verileri işleyen uygulamanızın en iyi şekilde çalışır hello geçiş stratejisini tanımlayın. Bir strateji seçtiğinizde, uygulamanızın kullanılabilirlik gereksinimlerini ve geçiş sırasında oluşan hello kapalı kalma göz önünde bulundurun. Örneğin, kolay yaklaşım toouse hello "yükseltme ve shift" bulut geçiş modeli olabilir. Tüm verileriniz toohello yeni bölge kopyalanacak sırada bu yaklaşım, Merhaba uygulaması varolan bölgenizde duraklatın. Merhaba kopyalama işlemi tamamlandıktan sonra hello yeni bölge uygulamanızda sürdürmek ve hello eski Data Lake Store hesabı silin. Merhaba geçiş sırasında kapalı kalma süresi gereklidir.

tooreduce kapalı kalma süresi hello yeni bölgede yeni veri alma hemen başlayabilir. Gerekli hello en az veri varsa, uygulamanızı hello yeni bölgede çalıştırın. Merhaba arka planda hello varolan Data Lake Store hesabı toohello yeni Data Lake Store hesabına toocopy eski verileri hello yeni bölgede devam edin. Bu yaklaşımı kullanarak, hello anahtar toohello yeni bölge az kapalı kalma süresi ile yapabilirsiniz. Tüm hello eski verileri kopyalanır, hello eski Data Lake Store hesabı silin.

Geçiş planlaması yaparken diğer önemli ayrıntıları tooconsider şunlardır:

* **Veri birimi**. Merhaba birim verilerini (gigabayt cinsinden hello sayısı dosyaları ve klasörleri vb.), başlangıç saati ve hello geçiş için gereken kaynakları etkiler.

* **Data Lake Store hesabı adı**. Merhaba yeni hesap adını hello yeni bölgede genel olarak benzersiz olmalıdır. Örneğin, Doğu ABD 2 eski Data Lake Store hesabınızı hello adı contosoeastus2.azuredatalakestore.net olabilir. Yeni Data Lake Store hesabınızda Kuzey AB contosonortheu.azuredatalakestore.net adı.

* **Araçlar**. Merhaba kullanmanızı öneririz [Azure Data Factory kopyalama etkinliği](../data-factory/data-factory-azure-datalake-connector.md) toocopy Data Lake Store dosyaları. Veri Fabrikası yüksek performansı ve güvenilirliği ile veri hareketi destekler. Data Factory yalnızca hello klasör hiyerarşisini ve hello dosyaların içeriğini kopyalar göz önünde bulundurun. Toomanually ihtiyacınız hello eski hesabı toohello yeni hesap kullanan tüm erişim denetim listelerini (ACL'ler) uygulayın. Merhaba performans hedefleri iyi senaryolar dahil daha fazla bilgi için bkz: [kopyalama etkinliği performans ve ayarlama Kılavuzu](../data-factory/data-factory-copy-activity-performance.md). Daha hızlı kopyalanan verileri istiyorsanız toouse gerekebilecek ek bulut veri taşıma birimleri. AdlCopy gibi diğer bazı araçları bölgeler arasında veri kopyalamayı desteklemez.  

* **Bant genişliği ücretleri**. [Bant genişliği ücretleri](https://azure.microsoft.com/en-us/pricing/details/bandwidth/) bir Azure bölgesinin dışına aktarılan verileri için geçerlidir.

* **Verilerinizi ACL'lerin**. Verilerinizi hello yeni bölgede ACL'ler toofiles ve klasörleri uygulayarak güvenli hale getirin. Daha fazla bilgi için bkz: [Azure Data Lake Store içinde depolanan verilerin güvenliğini sağlama](data-lake-store-secure-data.md). Merhaba geçiş tooupdate kullanın ve, ACL'ler Ayarla öneririz. Toouse ayarları benzer tooyour geçerli ayarları isteyebilirsiniz. Uygulanan tooany dosya hello Azure portal kullanarak hello ACL'lerini görüntüleyebilirsiniz [PowerShell cmdlet'leri](/powershell/module/azurerm.datalakestore/get-azurermdatalakestoreitempermission), ya da SDK'ları.  

* **Analiz Hizmetleri konumunu**. En iyi performans için Azure Data Lake Analytics veya Azure Hdınsight gibi Analiz Hizmetleri hello olmalıdır, verilerinizin aynı bölgede.  

## <a name="next-steps"></a>Sonraki adımlar
* [Azure Data Lake Store'a Genel Bakış](data-lake-store-overview.md)
