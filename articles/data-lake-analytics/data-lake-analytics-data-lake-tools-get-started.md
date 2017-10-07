---
title: "Visual Studio için Data Lake araçları kullanarak aaaDevelop U-SQL komut dosyalarını | Microsoft Docs"
description: "Visual Studio için tooinstall Data Lake araçları nasıl ve ne öğrenin toodevelop ve test U-SQL komut dosyaları."
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: jhubbard
editor: cgronlun
ms.assetid: ad8a6992-02c7-47d4-a108-62fc5a0777a3
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/28/2017
ms.author: saveenr, yanacai
ms.openlocfilehash: 7a0c02c275b8cefecbe784ba63969cbf24a150d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-u-sql-scripts-by-using-data-lake-tools-for-visual-studio"></a>Visual Studio için Data Lake Araçları'nı kullanarak U-SQL betikleri geliştirme
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]


Bilgi nasıl toouse Visual Studio toocreate Azure Data Lake Analytics hesapları tanımlayın işler [U-SQL](data-lake-analytics-u-sql-get-started.md)ve işleri toohello Data Lake Analytics hizmeti gönderin. Data Lake Analytics hakkında daha fazla bilgi için bkz. [Azure Data Lake Analytics'e genel bakış](data-lake-analytics-overview.md).


## <a name="prerequisites"></a>Ön koşullar

* **Visual Studio**: Express dışında tüm sürümler desteklenir.
    * Visual Studio 2017
    * Visual Studio 2015
    * Visual Studio 2013
* **.NET için Microsoft Azure SDK** 2.7.1 sürümü veya sonraki sürümleri.  Hello kullanarak yükleme [Web Platformu yükleyicisi](http://www.microsoft.com/web/downloads/platform.aspx).
* **Data Lake Analytics** hesabı. hesabı, bir toocreate bkz [Azure portal kullanarak Azure Data Lake Analytics ile çalışmaya başlama](data-lake-analytics-get-started-portal.md).

## <a name="install-azure-data-lake-tools-for-visual-studio"></a>Visual Studio için Azure Data Lake Araçları’nı yükleme 

Azure Data Lake araçları Visual Studio için yükleyip [hello İndirme Merkezi gelen](http://aka.ms/adltoolsvs). Yükleme işleminden sonra şunları kontrol edin:
* Merhaba **Sunucu Gezgini** > **Azure** düğümü içeren bir **Data Lake Analytics** düğümü. 
* Merhaba **Araçları** menü sahip bir **Data Lake** öğesi.

## <a name="connect-tooan-azure-data-lake-analytics-account"></a>Tooan Azure Data Lake Analytics hesabı Bağlan

1. Visual Studio'yu açın.
2. **Görünüm** > **Sunucu Gezgini**’ni seçerek Sunucu Gezgini’ni açın.
3. **Azure**’a sağ tıklayın. Ardından **tooMicrosoft Azure aboneliğine bağlanma** ve hello yönergeleri izleyin.
4. Sunucu Gezgini'nde **Azure** > **Data Lake Analytics**’i seçin. Data Lake Analytics hesaplarınızın listesini görürsünüz.


## <a name="write-your-first-u-sql-script"></a>İlk U-SQL betiğinizi yazma

metin aşağıdaki hello basit bir U-SQL komut dosyasıdır. Küçük bir veri kümesini ve bir dosya olarak dataset toohello varsayılan Data Lake Store adlı yazma tanımlar `/data.csv`.

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

### <a name="submit-a-data-lake-analytics-job"></a>Data Lake Analytics işi gönderme

1. **Dosya** > **Yeni** > **Proje**’yi seçin.

2. Select hello **U-SQL projesi** yazın ve ardından **Tamam**. Visual Studio, **Script.usql** dosyasıyla bir çözüm oluşturur.

3. Hello önceki betik hello yapıştırma **Script.usql** penceresi.

4. Merhaba hello sol üst köşesindeki **Script.usql** penceresinde hello Data Lake Analytics hesabı belirtin.

    ![U-SQL Visual Studio projesini gönderme](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-submit-job.png)

5. Merhaba hello sol üst köşesindeki **Script.usql** penceresinde, seçin **gönderme**.
6. Merhaba doğrulayın **Analytics hesabı**ve ardından **gönderme**. Merhaba gönderimi tamamlandıktan sonra gönderme işleminin sonuçları hello Data Lake araçları Visual Studio sonuçlar için kullanılabilir.

    ![U-SQL Visual Studio projesini gönderme](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-submit-job-advanced.png)
7. toosee hello en son iş durumunu ve yenileme Merhaba ekranında tıklatın **yenileme**. Merhaba iş başarılı olduğunda hello gösterir **iş grafiği**, **meta veri işlemleri**, **Durum geçmişi**, ve **tanılama**:

    ![U-SQL Visual Studio Data Lake Analytics iş performans grafiği](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-performance-graph.png)

   * **İş özeti** hello hello iş özetini gösterir.   
   * **İş ayrıntılarını** hello komut dosyası, kaynakları ve köşeleri dahil olmak üzere hello iş hakkında daha ayrıntılı bilgileri gösterir.
   * **İş grafiğinin** hello işinin ilerleme durumunu hello visualizes.
   * **Meta veri işlemleri** hello U-SQL kataloğunu üzerinde gerçekleştirilen tüm hello eylemleri gösterir.
   * **Veri** tüm hello girişleri ve çıkışları gösterir.
   * **Tanılama**, iş yürütme ve performans iyileştirme için gelişmiş bir analiz sağlar.

### <a name="toocheck-job-state"></a>toocheck iş durumu

1. Sunucu Gezgini'nde **Azure** > **Data Lake Analytics**’i seçin. 
2. Merhaba Data Lake Analytics hesap adını genişletin.
3. **İşler**’e çift tıklayın.
4. Daha önce gönderilen hello işi seçin.

### <a name="toosee-hello-output-of-a-job"></a>İş toosee hello çıktısı

1. Server Explorer'da gönderdiğiniz toohello işi bulun.
2. Merhaba tıklatın **veri** sekmesi.
3. Merhaba, **iş çıkışları** sekmesi, select hello `"/data.csv"` dosya.

## <a name="next-steps"></a>Sonraki adımlar

* [Test etmek ve hata ayıklamak için kendi iş istasyonunuzda U-SQL betiklerini çalıştırma](data-lake-analytics-data-lake-tools-local-run.md)
* [U-SQL işlerinde C# kodu hatalarını ayıklama](data-lake-analytics-debug-u-sql-jobs.md)
* [Hello Azure Data Lake araçları Visual Studio kodunu kullanın](data-lake-analytics-data-lake-tools-for-vscode.md)
