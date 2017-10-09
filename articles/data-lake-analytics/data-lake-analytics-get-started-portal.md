---
title: "Azure portal kullanarak Azure Data Lake Analytics ile başlatıldı aaaGet | Microsoft Docs"
description: "Toouse hello Azure portal toocreate Data Lake Analytics hesabı, U-SQL'yi kullanarak Data Lake Analytics işi oluşturma ve hello işi göndermek öğrenin. "
services: data-lake-analytics
documentationcenter: 
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: b1584d16-e0d2-4019-ad1f-f04be8c5b430
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/21/2017
ms.author: edmaca
ms.openlocfilehash: 6bb54404fa42cfed25b18bc2bfb7c72e6c361149
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-portal"></a>Azure portalı kullanarak Azure Data Lake Analytics ile çalışmaya başlama
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

Nasıl toouse hello Azure portal toocreate Azure Data Lake Analytics hesapları öğrenin, işleri tanımlayın [U-SQL](data-lake-analytics-u-sql-get-started.md)ve işleri toohello Data Lake Analytics hizmeti gönderin. Data Lake Analytics hakkında daha fazla bilgi için bkz. [Azure Data Lake Analytics'e genel bakış](data-lake-analytics-overview.md).

## <a name="prerequisites"></a>Ön koşullar

Bu öğreticiye başlamadan önce bir **Azure aboneliğinizin** olması gerekir. Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/pricing/free-trial/).

## <a name="create-a-data-lake-analytics-account"></a>Data Lake Analytics hesabı oluşturma

Şimdi, bir Data Lake Analytics oluşturacak ve bir Data Lake Store hesabı hello aynı saat.  Bu adım, basit bir işlemdir ve yalnızca 60 saniye toofinish alır.

1. Toohello üzerinde oturum [Azure portal](https://portal.azure.com).
2. **Yeni** >  **Veri + Analiz** > **Data Lake Analytics**’e tıklayın.
3. Aşağıdaki öğelerindeki hello için değerleri seçin:
   * **Ad**: Data Lake Analytics hesabınızı adlandırın (Yalnızca küçük harf ve sayı kullanılabilir).
   * **Abonelik**: hello hello Analytics hesabı için kullanılan Azure aboneliğini seçin.
   * **Kaynak Grubu**. Var olan bir Azure Kaynak Grubu'nu seçin veya yeni bir grup oluşturun.
   * **Konum**. Merhaba Data Lake Analytics hesabı için bir Azure veri merkezi seçin.
   * **Data Lake Store**: hello yönerge toocreate yeni bir Data Lake Store hesabı izleyin veya varolan bir tanesini seçin. 
4. İsteğe bağlı olarak Data Lake Analytics hesabınıza yönelik bir fiyatlandırma katmanı seçebilirsiniz.
5. **Oluştur**'a tıklayın. 


## <a name="your-first-u-sql-script"></a>İlk U-SQL betiğiniz

metin aşağıdaki hello çok basit bir U-SQL komut dosyasıdır. Tüm mevcut olan hello komut içinde küçük bir veri kümesini tanımlayın ve ardından bu veri kümesi toohello varsayılan Data Lake Store çıkışı adlı bir dosya yazma `/data.csv`.

```
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    too"/data.csv"
    USING Outputters.Csv();
```

## <a name="submit-a-u-sql-job"></a>U-SQL işi gönderme

1. Data Lake Analytics hesabı Hello tıklatın **yeni iş**.
2. Merhaba Hello metinde yukarıda gösterilen U-SQL betiğini yapıştırın. 
3. **İşi Gönder**'e tıklayın.   
4. Merhaba iş durumu değişinceye kadar çok bekleyin**başarılı**.
5. Merhaba işi başarısız olduysa bkz [İzleyici ve Data Lake Analytics işlerini sorun giderme](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).
6. Merhaba tıklatın **çıkış** sekmesini ve ardından `data.csv`. 

## <a name="see-also"></a>Ayrıca bkz.

* U-SQL uygulamalarını geliştirmeye başlatılan tooget bkz [Visual Studio için Data Lake Araçları'nı kullanarak geliştirme U-SQL betikleri](data-lake-analytics-data-lake-tools-get-started.md).
* U-SQL, toolearn bkz [Azure Data Lake Analytics U-SQL dili ile çalışmaya başlama](data-lake-analytics-u-sql-get-started.md).
* Yönetim görevleri için bkz. [Azure portalı kullanarak Azure Data Lake Analytics'i yönetme](data-lake-analytics-manage-use-portal.md).
