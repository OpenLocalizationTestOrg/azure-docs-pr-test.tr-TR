---
title: Azure Data Lake Store sorular aaaFrequently | Microsoft Docs
description: "Azure Data Lake Store ile ilgili sorunları giderme veya azaltma kılavuzu"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: bf7fd555-3e30-43ce-b28c-c3ad0a241fdb
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: eeabdeef18f3b72901bd1a14283f85dd9c0ead44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-azure-data-lake-store"></a>Azure Data Lake Store için sık sorulan sorular
Bu makalede SSS ilgili tooAzure Data Lake Store hakkında bilgi edineceksiniz.

## <a name="how-can-i-further-protect-my-data-from-region-wide-disasters-or-accidental-deletions"></a>Verilerimi bölge çapındaki afetlerden veya yanlışlıkla silinmekten nasıl daha iyi koruyabilirim?
Azure Data Lake Store hesabınızdaki Hello veri otomatik çoğaltmaları aracılığıyla bir bölge içinde dayanıklı tootransient donanım hataları var. Bu, dayanıklılık ve yüksek kullanılabilirlik, toplantı hello Azure veri Gölü deposu SLA'sı sağlar. İşte bazı yönergeler korunmasına nasıl yardımcı toofurther verilerinizi nadir bölge genelinde kesintileri ya da yanlışlıkla silme.

### <a name="disaster-recovery-guidance"></a>Olağanüstü durum kurtarma kılavuzu
Her müşteri tooprepare için kritik kendi olağanüstü durum kurtarma planı. Lütfen olağanüstü durum kurtarma planınızı toohello toobuild aşağıda Azure belgelerine bakın. Kendi planınızı oluşturmanıza yardımcı olabilecek bazı kaynaklar aşağıda verilmiştir.

* [Azure uygulamaları için olağanüstü durum kurtarma ve yüksek kullanılabilirlik](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md)
* [Azure dayanıklılık teknik kılavuzu](../resiliency/resiliency-technical-guidance.md)

#### <a name="best-practices"></a>En iyi uygulamalar
Olağanüstü durum kurtarma planınızı hizalı sıklığı toohello gereksinimlerine sahip başka bir bölgede, kritik verilerin tooanother Data Lake Store hesabına kopyalamak öneririz. Yöntemleri toocopy verileri dahil olmak üzere, çeşitli vardır [ADLCopy](data-lake-store-copy-data-azure-storage-blob.md), [Azure PowerShell](data-lake-store-get-started-powershell.md) veya [Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md). Azure Data Factory, yinelenen bir düzende veri taşıma işlem hatları oluşturmak ve dağıtmak için kullanışlı bir hizmettir.

Bölgesel bir kesintinin meydana gelirse, daha sonra verilerinizi burada hello veri kopyalanmıştır hello bölgede erişebilirsiniz. Merhaba izleyebilirsiniz [Azure hizmet sağlığı panosunu](https://azure.microsoft.com/status/) toodetermine hello Merhaba dünya genelinde Azure hizmet durumu.

### <a name="data-corruption-or-accidental-deletion-recovery-guidance"></a>Verilerin bozulması veya yanlışlıkla silinmesi durumunda kurtarma kılavuzu
Azure Data Lake Store otomatik çoğaltmalar aracılığıyla veri dayanıklılığı sağlasa da bu önlem uygulamanızın (veya geliştiricilerin/kullanıcıların) verileri bozmasına ya da yanlışlıkla silmesine engel olmaz.

#### <a name="best-practices"></a>En iyi uygulamalar
tooprevent yanlışlıkla silinmesi, Data Lake Store hesabınız için bir hello doğru erişim ilkeleri ayarlamanızı öneririz.  Bu uygulama içerir [Azure kaynak kilitleri](../azure-resource-manager/resource-group-lock-resources.md) hello kullanılabilir kullanarak uygulama hesabı ve dosya düzeyinde erişim denetimini yanı sıra önemli kaynaklara aşağı toolock [Data Lake Store güvenlik özellikleri](data-lake-store-security-overview.md). Ayrıca, [ADLCopy](data-lake-store-copy-data-azure-storage-blob.md), [Azure PowerShell](data-lake-store-get-started-powershell.md) veya [Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md)’yi kullanarak başka bir Data Lake Store hesabında, klasörde veya Azure aboneliğinde düzenli olarak kritik verilerinizin kopyalarını oluşturmanızı da öneririz.  Bu veri bozulması veya silinmesi olay gelen kullanılan toorecover olabilir. Azure Data Factory, yinelenen bir düzende veri taşıma işlem hatları oluşturmak ve dağıtmak için kullanışlı bir hizmettir.

Kuruluşlar da etkinleştirebilir [tanılama günlük](data-lake-store-diagnostic-logs.md) kimin silinmiş veya olabilir bir dosyayı güncelleştirilmiş hakkında bilgi sağlayan veri erişimi denetim izleri toocollect kendi Azure Data Lake Store hesabı için.

## <a name="next-steps"></a>Sonraki adımlar
* [Azure Data Lake Store ile Çalışmaya Başlama](data-lake-store-get-started-portal.md)
* [Data Lake Store'da verilerin güvenliğini sağlama](data-lake-store-secure-data.md)

