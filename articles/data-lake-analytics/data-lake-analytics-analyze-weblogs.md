---
title: "Azure Data Lake Analytics kullanarak aaaAnalyze Web sitesi günlüklerini | Microsoft Docs"
description: "Data Lake Analytics'i kullanarak tooanalyze Web sitesi nasıl günlüklerini öğrenin. "
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 3a196735-d0d9-4deb-ba68-c4b3f3be8403
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: saveenr
ms.openlocfilehash: d27aaca95ed2b643cfed7a17b0066bf7fa4a1bf5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-website-logs-using-azure-data-lake-analytics"></a>Azure Data Lake Analytics'i kullanarak Web sitesi günlüklerini çözümleme
Bunlar toovisit hello Web sitesi nasıl Data Lake Analytics özellikle hangi başvuran bulunması kullanarak tooanalyze Web sitesi günlüklerini hatalarla karşılaşırsanız karşılaştık öğrenin.

## <a name="prerequisites"></a>Ön koşullar
* **Visual Studio 2015 veya Visual Studio 2013**.
* **[Visual Studio için Data Lake Araçları](http://aka.ms/adltoolsvs)**.

    Visual Studio için Data Lake araçları yüklendikten sonra göreceğiniz bir **Data Lake** hello öğesinde **Araçları** Visual Studio menüsünde:

    ![U-SQL Visual Studio menü](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-menu.png)
* **Data Lake Analytics ve hello Visual Studio için Data Lake araçları temel bilgiye**. başlatıldı, tooget bakın:

  * [Visual Studio için Data Lake Araçları'nı kullanarak U-SQL betiği geliştirmeye](data-lake-analytics-data-lake-tools-get-started.md).
* **Bir Data Lake Analytics hesabı.**  Bkz: [bir Azure Data Lake Analytics hesabı oluşturma](data-lake-analytics-get-started-portal.md).
* **Merhaba örnek veri toohello Data Lake Analytics hesabı karşıya yükleyin.** Bkz: [toocopy örnek veri dosyalarını](data-lake-analytics-get-started-portal.md).

    toorun Data Lake Analytics işi, bazı verilere ihtiyaç duyarsınız. Merhaba Data Lake araçları veri yüklemeyi desteklese de Bu öğretici daha kolay toofollow hello portal tooupload hello örnek veri toomake kullanır.

## <a name="connect-tooazure"></a>TooAzure Bağlan
Derleme ve herhangi bir U-SQL betiği test önce tooAzure bağlanmanız gerekir.

**tooconnect tooData Gölü analizi**

1. Visual Studio'yu açın.
2. Tıklatın **Data Lake > Seçenekler ve ayarlar**.
3. Tıklatın **oturum**, veya **Kullanıcı Değiştir** birisi oturum açtığı ve hello yönergeleri izleyin.
4. Tıklatın **Tamam** tooclose hello seçenekleri ve Ayarları iletişim kutusu.

**toobrowse, Data Lake Analytics hesapları**

1. Visual Studio'dan açmak **Sunucu Gezgini** basın tarafından **CTRL + ALT + S**.
2. **Sunucu Gezgini**'nden, **Azure** seçeneğini ve ardından **Data Lake Analytics** seçeneğini genişletin. Varsa Data Lake Analytics hesaplarınızın listesini görürsünüz. Merhaba Studio'dan Data Lake Analytics hesapları oluşturamazsınız. hesabı, bir toocreate bkz [Azure Portal kullanarak Azure Data Lake Analytics ile çalışmaya başlama](data-lake-analytics-get-started-portal.md) veya [Azure PowerShell kullanarak Azure Data Lake Analytics ile çalışmaya başlama](data-lake-analytics-get-started-powershell.md).

## <a name="develop-u-sql-application"></a>U-SQL uygulama geliştirme
U-SQL betiği çoğunlukla bir U-SQL uygulamasıdır. U-SQL hakkında daha fazla toolearn bkz [U-SQL ile çalışmaya başlama](data-lake-analytics-u-sql-get-started.md).

Ek kullanıcı tanımlı işleçler toohello uygulama ekleyebilirsiniz.  Daha fazla bilgi için bkz: [geliştirmek U-SQL kullanıcı tanımlı işleçler Data Lake Analytics işleri için](data-lake-analytics-u-sql-develop-user-defined-operators.md).

**toocreate ve Data Lake Analytics işi Gönder**

1. Merhaba tıklatın **Dosya > Yeni > Proje**.
2. Merhaba U-SQL proje türü seçin.

    ![yeni U-SQL Visual Studio projesi](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-new-project.png)
3. **Tamam** düğmesine tıklayın. Visual studio Script.usql dosyası ile çözüm oluşturur.
4. Komut dosyası hello Script.usql dosyasına aşağıdaki hello girin:

        // Create a database for easy reuse, so you don't need tooread from a file every time.
        CREATE DATABASE IF NOT EXISTS SampleDBTutorials;

        // Create a Table valued function. TVF ensures that your jobs fetch data from hello weblog file with hello correct schema.
        DROP FUNCTION IF EXISTS SampleDBTutorials.dbo.WeblogsView;
        CREATE FUNCTION SampleDBTutorials.dbo.WeblogsView()
        RETURNS @result TABLE
        (
            s_date DateTime,
            s_time string,
            s_sitename string,
            cs_method string,
            cs_uristem string,
            cs_uriquery string,
            s_port int,
            cs_username string,
            c_ip string,
            cs_useragent string,
            cs_cookie string,
            cs_referer string,
            cs_host string,
            sc_status int,
            sc_substatus int,
            sc_win32status int,
            sc_bytes int,
            cs_bytes int,
            s_timetaken int
        )
        AS
        BEGIN

            @result = EXTRACT
                s_date DateTime,
                s_time string,
                s_sitename string,
                cs_method string,
                cs_uristem string,
                cs_uriquery string,
                s_port int,
                cs_username string,
                c_ip string,
                cs_useragent string,
                cs_cookie string,
                cs_referer string,
                cs_host string,
                sc_status int,
                sc_substatus int,
                sc_win32status int,
                sc_bytes int,
                cs_bytes int,
                s_timetaken int
            FROM @"/Samples/Data/WebLog.log"
            USING Extractors.Text(delimiter:' ');
            RETURN;
        END;

        // Create a table for storing referrers and status
        DROP TABLE IF EXISTS SampleDBTutorials.dbo.ReferrersPerDay;
        @weblog = SampleDBTutorials.dbo.WeblogsView();
        CREATE TABLE SampleDBTutorials.dbo.ReferrersPerDay
        (
            INDEX idx1
            CLUSTERED(Year ASC)
            DISTRIBUTED BY HASH(Year)
        ) AS

        SELECT s_date.Year AS Year,
            s_date.Month AS Month,
            s_date.Day AS Day,
            cs_referer,
            sc_status,
            COUNT(DISTINCT c_ip) AS cnt
        FROM @weblog
        GROUP BY s_date,
                cs_referer,
                sc_status;

    U-SQL, toounderstand hello bkz [Data Lake Analytics U-SQL dili ile çalışmaya başlama](data-lake-analytics-u-sql-get-started.md).    
5. Yeni bir U-SQL komut dosyası tooyour proje ekleyin ve hello aşağıdakileri girin:

        // Query hello referrers that ran into errors
        @content =
            SELECT *
            FROM SampleDBTutorials.dbo.ReferrersPerDay
            WHERE sc_status >=400 AND sc_status < 500;

        OUTPUT @content
        too@"/Samples/Outputs/UnsuccessfulResponses.log"
        USING Outputters.Tsv();
6. Geçiş geri toohello ilk U-SQL betiği ve sonraki toohello **gönderme** düğmesini tıklatın, Analytics hesabınızı belirtin.
7. **Çözüm Gezgini**'nden, **Script.usql** öğesine sağ tıklayın ve ardından **Betik Oluştur**'a tıklayın. Merhaba çıkış bölmesinde Hello sonuçlarını doğrulayın.
8. **Çözüm Gezgini**'nden, **Script.usql** öğesine sağ tıklayın ve ardından **Betiği Gönder**'e tıklayın.
9. Merhaba doğrulayın **Analytics hesabı** hello bir yere, toorun hello iş istediğiniz ve ardından olan **gönderme**. Merhaba gönderim tamamlandığında gönderme işleminin sonuçları ve iş bağlantısı hello Data Lake araçları Visual Studio sonuçları penceresi için kullanılabilir.
10. Merhaba işi başarıyla tamamlanana kadar bekleyin.  Merhaba işi başarısız olursa, büyük olasılıkla hello kaynak dosyası eksik.  Lütfen bu öğreticinin hello önkoşul bölümüne bakın. Ek sorun giderme bilgileri için bkz: [İzleyici ve Azure Data Lake Analytics işlerini sorun giderme](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).

    Merhaba iş tamamlandığında, ekran aşağıdaki hello göreceksiniz:

    ![Data lake analytics Web günlüklerini Web sitesi günlüklerini çözümleme](./media/data-lake-analytics-analyze-weblogs/data-lake-analytics-analyze-weblogs-job-completed.png)
11. Şimdi için 7 - 10 adımı tekrarlayın **Script1.usql**.

**toosee hello iş çıktısı**

1. Gelen **Sunucu Gezgini**, genişletin **Azure**, genişletin **Data Lake Analytics**, Data Lake Analytics hesabınızı genişletin, **depolama hesapları**hello varsayılan Data Lake Store hesabına sağ tıklayın ve ardından **Explorer**.
2. Çift **örnekleri** tooopen hello klasörü, çift tıklayın ve ardından **çıkışları**.
3. Çift **UnsuccessfulResponsees.log**.
4. Toohello çıkış doğrudan sipariş toonavigate hello işinde hello grafik görünümü içinde hello çıktı dosyasına çift tıklayabilirsiniz.

## <a name="see-also"></a>Ayrıca bkz.
farklı araçları kullanarak Data Lake Analytics ile çalışmaya tooget bakın:

* [Azure Portal'ı kullanarak Data Lake Analytics ile çalışmaya başlama](data-lake-analytics-get-started-portal.md)
* [Azure PowerShell'i kullanarak Data Lake Analytics ile çalışmaya başlama](data-lake-analytics-get-started-powershell.md)
* [.NET SDK'yı kullanarak Data Lake Analytics ile çalışmaya başlama](data-lake-analytics-get-started-net-sdk.md)
