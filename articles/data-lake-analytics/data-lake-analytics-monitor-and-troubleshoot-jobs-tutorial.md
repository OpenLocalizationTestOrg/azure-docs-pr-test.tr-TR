---
title: "Azure Portal kullanarak aaaTroubleshoot Azure Data Lake Analytics işlerini | Microsoft Docs"
description: "Nasıl toouse hello Azure Portal tootroubleshoot Data Lake Analytics işlerini öğrenin. "
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: b7066d81-3142-474f-8a34-32b0b39656dc
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: e810d56bab8f1a8254721ec9906bb6a4508dc22a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-data-lake-analytics-jobs-using-azure-portal"></a>Azure Portal kullanarak Azure Data Lake Analytics işlerini sorun giderme
Nasıl toouse hello Azure Portal tootroubleshoot Data Lake Analytics işlerini öğrenin.

Bu öğreticide, bir eksik kaynak dosyası sorunu Kurulum ve hello Azure Portal tootroubleshoot hello sorun kullanın.

## <a name="submit-a-data-lake-analytics-job"></a>Data Lake Analytics işi gönderme

U-SQL işi aşağıdaki hello gönder:

```
@searchlog =
   EXTRACT UserId          int,
           Start           DateTime,
           Region          string,
           Query           string,
           Duration        int?,
           Urls            string,
           ClickedUrls     string
   FROM "/Samples/Data/SearchLog.tsv1"
   USING Extractors.Tsv();

OUTPUT @searchlog   
   too"/output/SearchLog-from-adls.csv"
   USING Outputters.Csv();
```
    
Merhaba kaynak dosyası hello komut dosyasında tanımlı olan **/Samples/Data/SearchLog.tsv1**, burada olmalıdır **/Samples/Data/SearchLog.tsv**.


## <a name="troubleshoot-hello-job"></a>Merhaba işi sorunlarını giderme

**toosee tüm işleri hello**

1. Hello ifadesini Azure portal'ı tıklatın **Microsoft Azure** hello sol üst köşedeki.
2. Data Lake Analytics hesap adınızı içeren Hello kutucuğa tıklayın.  Merhaba işi Özet hello üzerinde gösterilen **iş yönetimi** döşeme.

    ![Azure Data Lake Analytics iş yönetimi](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-job-management.png)

    Merhaba iş yönetimi hello iş durumunu bir bakışta sağlar. Başarısız bir işi olduğuna dikkat edin.
3. Merhaba tıklatın **iş yönetimi** toosee hello işleri kutucuğu. Merhaba işleri kategorilere içinde **çalıştıran**, **sıraya alınan**, ve **sona erdi**. Merhaba başarısız işinizde göreceksiniz **sona erdi** bölümü. Birincisi hello listesinde olacaktır. İşlerini çok sahip olduğunuzda, tıklayabilirsiniz **filtre** toohelp, toolocate işler.

    ![Azure Data Lake Analytics işleri filtreleyin](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-filter-jobs.png)
4. Yeni bir dikey penceresinde hello listesi tooopen hello iş ayrıntıları Hello başarısız işi tıklayın:

    ![Azure Data Lake Analytics işi başarısız oldu](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-failed-job.png)

    Bildirim hello **yeniden gönderin** düğmesi. Merhaba sorunu düzelttikten sonra hello işi yeniden gönderebilirsiniz.
5. Vurgulanan bölümünden hello önceki ekran tooopen hello hata ayrıntıları'ı tıklatın.  Benzer bir şey göreceksiniz:

    ![Azure Data Lake Analytics işi ayrıntıları ile başarısız oldu.](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-failed-job-details.png)

    Merhaba kaynak klasörü bulunamadı söyler.
6. Tıklatın **yinelenen komut dosyası**.
7. Güncelleştirme hello **FROM** yolu toohello aşağıdaki:

    "/ Samples/Data/SearchLog.tsv"
8. **İşi Gönder**'e tıklayın.

## <a name="see-also"></a>Ayrıca bkz.
* [Azure Data Lake Analytics'e genel bakış](data-lake-analytics-overview.md)
* [Azure Data Lake Azure PowerShell kullanarak Analytics ile çalışmaya başlama](data-lake-analytics-get-started-powershell.md)
* [Azure Data Lake Analytics ve U-SQL Visual Studio kullanarak kullanmaya başlama](data-lake-analytics-u-sql-get-started.md)
* [Azure Data Lake Analytics'i Azure Portal'ı kullanarak yönetme](data-lake-analytics-manage-use-portal.md)
