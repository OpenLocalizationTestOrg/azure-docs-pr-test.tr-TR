---
title: "Data Lake Analytics kota sınırları aaaAzure | Microsoft Docs"
description: "Azure Data Lake Analytics (ADLA) hesaplarında nasıl tooadjust ve artış kota sınırları hakkında bilgi edinin."
services: data-lake-analytics
keywords: Azure Data Lake Analytics
documentationcenter: 
author: omidm1
editor: omidm1
ms.assetid: 49416f38-fcc7-476f-a55e-d67f3f9c1d34
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/18/2017
ms.author: omidm
ms.openlocfilehash: 875c4d00e0c57414031e50754495c02162bdca48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-lake-analytics-quota-limits"></a>Azure Data Lake Analytics kota sınırları

Azure Data Lake Analytics (ADLA) hesaplarında nasıl tooadjust ve artış kota sınırları hakkında bilgi edinin. Bu sınırlar bilerek, U-SQL işi davranışı anlamanıza yardımcı olabilir. Tüm kota sınırları yumuşak, olduğundan toous ulaşmasını tarafından hello maksimum sınırı artırabilirsiniz.

## <a name="azure-subscriptions-limits"></a>Azure abonelikleri sınırları

**ADLA en fazla abonelik başına hesapları:** 5

 Abonelik başına oluşturabileceğiniz ADLA hesapları hello sayısının budur. Toocreate altıncı ADLA hesap çalışırsanız, "Merhaba en fazla izin Data Lake Analytics hesabı sayısını (5) altında abonelik adını bölgesindeki ulaştığınız" bir hata alırsınız. Bu durumda, tüm kullanılmayan ADLA hesapları silmek ya da tarafından toous ulaşmak [bir destek bileti açmadan](#increase-maximum-quota-limits).

## <a name="adla-account-limits"></a>ADLA hesabı sınırları

**Hesap başına en fazla Analytics birimi (Avustralya) sayısı:** 250

Hesabınızı çalışabilir Avustralya hello sayısının budur. Avustralya toplam tüm işleri arasında bu sınırı aşarsa, yeni işleri otomatik olarak kuyruğa alınır. Örneğin:

* Yalnızca bir işe varsa 250 ile ikinci bir gönderdiğinizde Avustralya, işi çalıştırılırken hello iş kuyruğundaki hello ilk iş tamamlanana kadar bekler.
* Çalışan beş işleri zaten varsa ve her 50 kullanarak 20 gereken altıncı bir işi gönderdiğinizde Avustralya kalmayana kadar 20 hello iş kuyruğundaki bekler Avustralya Avustralya kullanılabilir.

**Hesap başına eşzamanlı U-SQL işi sayısı üst sınırı:** 20

Bu hello maksimum hesabınızda eşzamanlı olarak çalışabilecek iş sayısıdır. Bu değer yeni işleri otomatik olarak kuyruğa alınır.

## <a name="adjust-adla-quota-limits-per-account"></a>Hesap başına ADLA kota sınırları ayarlama

1. Toohello üzerinde oturum [Azure portal](https://portal.azure.com).
2. Varolan ADLA hesabı seçin.
3. **Özellikler**'e tıklayın.
4. Ayarlama **paralellik** ve **eşzamanlı iş** toosuit gereksinimlerinizi.

    ![Azure Data Lake Analytics portalı dikey penceresi](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-properties.png)

## <a name="increase-maximum-quota-limits"></a>En yüksek kota sınırları artırmak

1. Azure portalında bir destek isteği açın.

    ![Azure Data Lake Analytics portalı dikey penceresi](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-help-support.png)

    ![Azure Data Lake Analytics portalı dikey penceresi](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request.png)
2. Merhaba sorun türü seçin **kota**.
3. Seçin, **abonelik** ("Deneme" aboneliği olmadığından emin olun).
4. Kota türü seçin **Data Lake Analytics**.

    ![Azure Data Lake Analytics portalı dikey penceresi](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request-basics.png)

5. Merhaba sorun dikey penceresinde istenen artış sınırınızı açıklayan **ayrıntıları** bu ek kapasite neden ihtiyacınız olan.

    ![Azure Data Lake Analytics portalı dikey penceresi](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request-details.png)

6. İletişim bilgilerinizi doğrulayın ve hello destek isteği oluşturun.

Microsoft, isteğinizi gözden geçirir ve mümkün olan en kısa sürede uygulamasını iş gereksinimleriniz tooaccommodate çalışır.

## <a name="next-steps"></a>Sonraki adımlar

* [Microsoft Azure Data Lake Analytics'e genel bakış](data-lake-analytics-overview.md)
* [Azure Data Lake Analytics'i Azure PowerShell'i kullanarak yönetme](data-lake-analytics-manage-use-powershell.md)
* [Azure portalını kullanarak Azure Data Lake Analytics işlerini izleme ve sorun giderme](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
