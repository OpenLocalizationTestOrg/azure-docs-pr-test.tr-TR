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
# <a name="analyze-website-logs-using-azure-data-lake-analytics"></a><span data-ttu-id="fecfa-103">Azure Data Lake Analytics'i kullanarak Web sitesi günlüklerini çözümleme</span><span class="sxs-lookup"><span data-stu-id="fecfa-103">Analyze Website logs using Azure Data Lake Analytics</span></span>
<span data-ttu-id="fecfa-104">Bunlar toovisit hello Web sitesi nasıl Data Lake Analytics özellikle hangi başvuran bulunması kullanarak tooanalyze Web sitesi günlüklerini hatalarla karşılaşırsanız karşılaştık öğrenin.</span><span class="sxs-lookup"><span data-stu-id="fecfa-104">Learn how tooanalyze website logs using Data Lake Analytics, especially on finding out which referrers ran into errors when they tried toovisit hello website.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fecfa-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="fecfa-105">Prerequisites</span></span>
* <span data-ttu-id="fecfa-106">**Visual Studio 2015 veya Visual Studio 2013**.</span><span class="sxs-lookup"><span data-stu-id="fecfa-106">**Visual Studio 2015 or Visual Studio 2013**.</span></span>
* <span data-ttu-id="fecfa-107">**[Visual Studio için Data Lake Araçları](http://aka.ms/adltoolsvs)**.</span><span class="sxs-lookup"><span data-stu-id="fecfa-107">**[Data Lake Tools for Visual Studio](http://aka.ms/adltoolsvs)**.</span></span>

    <span data-ttu-id="fecfa-108">Visual Studio için Data Lake araçları yüklendikten sonra göreceğiniz bir **Data Lake** hello öğesinde **Araçları** Visual Studio menüsünde:</span><span class="sxs-lookup"><span data-stu-id="fecfa-108">Once Data Lake Tools for Visual Studio is installed, you will see a **Data Lake** item in hello **Tools** menu in Visual Studio:</span></span>

    ![U-SQL Visual Studio menü](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-menu.png)
* <span data-ttu-id="fecfa-110">**Data Lake Analytics ve hello Visual Studio için Data Lake araçları temel bilgiye**.</span><span class="sxs-lookup"><span data-stu-id="fecfa-110">**Basic knowledge of Data Lake Analytics and hello Data Lake Tools for Visual Studio**.</span></span> <span data-ttu-id="fecfa-111">başlatıldı, tooget bakın:</span><span class="sxs-lookup"><span data-stu-id="fecfa-111">tooget started, see:</span></span>

  * <span data-ttu-id="fecfa-112">[Visual Studio için Data Lake Araçları'nı kullanarak U-SQL betiği geliştirmeye](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="fecfa-112">[Develop U-SQL script using Data Lake tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
* <span data-ttu-id="fecfa-113">**Bir Data Lake Analytics hesabı.**</span><span class="sxs-lookup"><span data-stu-id="fecfa-113">**A Data Lake Analytics account.**</span></span>  <span data-ttu-id="fecfa-114">Bkz: [bir Azure Data Lake Analytics hesabı oluşturma](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="fecfa-114">See [Create an Azure Data Lake Analytics account](data-lake-analytics-get-started-portal.md).</span></span>
* <span data-ttu-id="fecfa-115">**Merhaba örnek veri toohello Data Lake Analytics hesabı karşıya yükleyin.**</span><span class="sxs-lookup"><span data-stu-id="fecfa-115">**Upload hello sample data toohello Data Lake Analytics account.**</span></span> <span data-ttu-id="fecfa-116">Bkz: [toocopy örnek veri dosyalarını](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="fecfa-116">See [toocopy sample data files](data-lake-analytics-get-started-portal.md).</span></span>

    <span data-ttu-id="fecfa-117">toorun Data Lake Analytics işi, bazı verilere ihtiyaç duyarsınız.</span><span class="sxs-lookup"><span data-stu-id="fecfa-117">toorun a Data Lake Analytics job, you will need some data.</span></span> <span data-ttu-id="fecfa-118">Merhaba Data Lake araçları veri yüklemeyi desteklese de Bu öğretici daha kolay toofollow hello portal tooupload hello örnek veri toomake kullanır.</span><span class="sxs-lookup"><span data-stu-id="fecfa-118">Even though hello Data Lake Tools supports uploading data, you will use hello portal tooupload hello sample data toomake this tutorial easier toofollow.</span></span>

## <a name="connect-tooazure"></a><span data-ttu-id="fecfa-119">TooAzure Bağlan</span><span class="sxs-lookup"><span data-stu-id="fecfa-119">Connect tooAzure</span></span>
<span data-ttu-id="fecfa-120">Derleme ve herhangi bir U-SQL betiği test önce tooAzure bağlanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="fecfa-120">Before you can build and test any U-SQL scripts, you must first connect tooAzure.</span></span>

<span data-ttu-id="fecfa-121">**tooconnect tooData Gölü analizi**</span><span class="sxs-lookup"><span data-stu-id="fecfa-121">**tooconnect tooData Lake Analytics**</span></span>

1. <span data-ttu-id="fecfa-122">Visual Studio'yu açın.</span><span class="sxs-lookup"><span data-stu-id="fecfa-122">Open Visual Studio.</span></span>
2. <span data-ttu-id="fecfa-123">Tıklatın **Data Lake > Seçenekler ve ayarlar**.</span><span class="sxs-lookup"><span data-stu-id="fecfa-123">Click **Data Lake > Options and Settings**.</span></span>
3. <span data-ttu-id="fecfa-124">Tıklatın **oturum**, veya **Kullanıcı Değiştir** birisi oturum açtığı ve hello yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="fecfa-124">Click **Sign In**, or **Change User** if someone has signed in, and follow hello instructions.</span></span>
4. <span data-ttu-id="fecfa-125">Tıklatın **Tamam** tooclose hello seçenekleri ve Ayarları iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="fecfa-125">Click **OK** tooclose hello Options and Settings dialog.</span></span>

<span data-ttu-id="fecfa-126">**toobrowse, Data Lake Analytics hesapları**</span><span class="sxs-lookup"><span data-stu-id="fecfa-126">**toobrowse your Data Lake Analytics accounts**</span></span>

1. <span data-ttu-id="fecfa-127">Visual Studio'dan açmak **Sunucu Gezgini** basın tarafından **CTRL + ALT + S**.</span><span class="sxs-lookup"><span data-stu-id="fecfa-127">From Visual Studio, open **Server Explorer** by press **CTRL+ALT+S**.</span></span>
2. <span data-ttu-id="fecfa-128">**Sunucu Gezgini**'nden, **Azure** seçeneğini ve ardından **Data Lake Analytics** seçeneğini genişletin.</span><span class="sxs-lookup"><span data-stu-id="fecfa-128">From **Server Explorer**, expand **Azure**, and then expand **Data Lake Analytics**.</span></span> <span data-ttu-id="fecfa-129">Varsa Data Lake Analytics hesaplarınızın listesini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="fecfa-129">You shall see a list of your Data Lake Analytics accounts if there are any.</span></span> <span data-ttu-id="fecfa-130">Merhaba Studio'dan Data Lake Analytics hesapları oluşturamazsınız.</span><span class="sxs-lookup"><span data-stu-id="fecfa-130">You cannot create Data Lake Analytics accounts from hello studio.</span></span> <span data-ttu-id="fecfa-131">hesabı, bir toocreate bkz [Azure Portal kullanarak Azure Data Lake Analytics ile çalışmaya başlama](data-lake-analytics-get-started-portal.md) veya [Azure PowerShell kullanarak Azure Data Lake Analytics ile çalışmaya başlama](data-lake-analytics-get-started-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="fecfa-131">toocreate an account, see [Get Started with Azure Data Lake Analytics using Azure Portal](data-lake-analytics-get-started-portal.md) or [Get Started with Azure Data Lake Analytics using Azure PowerShell](data-lake-analytics-get-started-powershell.md).</span></span>

## <a name="develop-u-sql-application"></a><span data-ttu-id="fecfa-132">U-SQL uygulama geliştirme</span><span class="sxs-lookup"><span data-stu-id="fecfa-132">Develop U-SQL application</span></span>
<span data-ttu-id="fecfa-133">U-SQL betiği çoğunlukla bir U-SQL uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="fecfa-133">A U-SQL application is mostly a U-SQL script.</span></span> <span data-ttu-id="fecfa-134">U-SQL hakkında daha fazla toolearn bkz [U-SQL ile çalışmaya başlama](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="fecfa-134">toolearn more about U-SQL, see [Get started with U-SQL](data-lake-analytics-u-sql-get-started.md).</span></span>

<span data-ttu-id="fecfa-135">Ek kullanıcı tanımlı işleçler toohello uygulama ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fecfa-135">You can add addition user-defined operators toohello application.</span></span>  <span data-ttu-id="fecfa-136">Daha fazla bilgi için bkz: [geliştirmek U-SQL kullanıcı tanımlı işleçler Data Lake Analytics işleri için](data-lake-analytics-u-sql-develop-user-defined-operators.md).</span><span class="sxs-lookup"><span data-stu-id="fecfa-136">For more information, see [Develop U-SQL user defined operators for Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-user-defined-operators.md).</span></span>

<span data-ttu-id="fecfa-137">**toocreate ve Data Lake Analytics işi Gönder**</span><span class="sxs-lookup"><span data-stu-id="fecfa-137">**toocreate and submit a Data Lake Analytics job**</span></span>

1. <span data-ttu-id="fecfa-138">Merhaba tıklatın **Dosya > Yeni > Proje**.</span><span class="sxs-lookup"><span data-stu-id="fecfa-138">Click hello **File > New > Project**.</span></span>
2. <span data-ttu-id="fecfa-139">Merhaba U-SQL proje türü seçin.</span><span class="sxs-lookup"><span data-stu-id="fecfa-139">Select hello U-SQL Project type.</span></span>

    ![yeni U-SQL Visual Studio projesi](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-new-project.png)
3. <span data-ttu-id="fecfa-141">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fecfa-141">Click **OK**.</span></span> <span data-ttu-id="fecfa-142">Visual studio Script.usql dosyası ile çözüm oluşturur.</span><span class="sxs-lookup"><span data-stu-id="fecfa-142">Visual studio creates a solution with a Script.usql file.</span></span>
4. <span data-ttu-id="fecfa-143">Komut dosyası hello Script.usql dosyasına aşağıdaki hello girin:</span><span class="sxs-lookup"><span data-stu-id="fecfa-143">Enter hello following script into hello Script.usql file:</span></span>

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

    <span data-ttu-id="fecfa-144">U-SQL, toounderstand hello bkz [Data Lake Analytics U-SQL dili ile çalışmaya başlama](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="fecfa-144">toounderstand hello U-SQL, see [Get started with Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>    
5. <span data-ttu-id="fecfa-145">Yeni bir U-SQL komut dosyası tooyour proje ekleyin ve hello aşağıdakileri girin:</span><span class="sxs-lookup"><span data-stu-id="fecfa-145">Add a new U-SQL script tooyour project and enter hello following:</span></span>

        // Query hello referrers that ran into errors
        @content =
            SELECT *
            FROM SampleDBTutorials.dbo.ReferrersPerDay
            WHERE sc_status >=400 AND sc_status < 500;

        OUTPUT @content
        too@"/Samples/Outputs/UnsuccessfulResponses.log"
        USING Outputters.Tsv();
6. <span data-ttu-id="fecfa-146">Geçiş geri toohello ilk U-SQL betiği ve sonraki toohello **gönderme** düğmesini tıklatın, Analytics hesabınızı belirtin.</span><span class="sxs-lookup"><span data-stu-id="fecfa-146">Switch back toohello first U-SQL script and next toohello **Submit** button, specify your Analytics account.</span></span>
7. <span data-ttu-id="fecfa-147">**Çözüm Gezgini**'nden, **Script.usql** öğesine sağ tıklayın ve ardından **Betik Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fecfa-147">From **Solution Explorer**, right click **Script.usql**, and then click **Build Script**.</span></span> <span data-ttu-id="fecfa-148">Merhaba çıkış bölmesinde Hello sonuçlarını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="fecfa-148">Verify hello results in hello Output pane.</span></span>
8. <span data-ttu-id="fecfa-149">**Çözüm Gezgini**'nden, **Script.usql** öğesine sağ tıklayın ve ardından **Betiği Gönder**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fecfa-149">From **Solution Explorer**, right click **Script.usql**, and then click **Submit Script**.</span></span>
9. <span data-ttu-id="fecfa-150">Merhaba doğrulayın **Analytics hesabı** hello bir yere, toorun hello iş istediğiniz ve ardından olan **gönderme**.</span><span class="sxs-lookup"><span data-stu-id="fecfa-150">Verify hello **Analytics Account** is hello one where you want toorun hello job, and then click **Submit**.</span></span> <span data-ttu-id="fecfa-151">Merhaba gönderim tamamlandığında gönderme işleminin sonuçları ve iş bağlantısı hello Data Lake araçları Visual Studio sonuçları penceresi için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="fecfa-151">Submission results and job link are available in hello Data Lake Tools for Visual Studio Results window when hello submission is completed.</span></span>
10. <span data-ttu-id="fecfa-152">Merhaba işi başarıyla tamamlanana kadar bekleyin.</span><span class="sxs-lookup"><span data-stu-id="fecfa-152">Wait until hello job is completed successfully.</span></span>  <span data-ttu-id="fecfa-153">Merhaba işi başarısız olursa, büyük olasılıkla hello kaynak dosyası eksik.</span><span class="sxs-lookup"><span data-stu-id="fecfa-153">If hello job failed, it is most likely missing hello source file.</span></span>  <span data-ttu-id="fecfa-154">Lütfen bu öğreticinin hello önkoşul bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="fecfa-154">Please see hello Prerequisite section of this tutorial.</span></span> <span data-ttu-id="fecfa-155">Ek sorun giderme bilgileri için bkz: [İzleyici ve Azure Data Lake Analytics işlerini sorun giderme](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="fecfa-155">For additional troubleshooting information, see [Monitor and troubleshoot Azure Data Lake Analytics jobs](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).</span></span>

    <span data-ttu-id="fecfa-156">Merhaba iş tamamlandığında, ekran aşağıdaki hello göreceksiniz:</span><span class="sxs-lookup"><span data-stu-id="fecfa-156">When hello job is completed, you shall see hello following screen:</span></span>

    ![Data lake analytics Web günlüklerini Web sitesi günlüklerini çözümleme](./media/data-lake-analytics-analyze-weblogs/data-lake-analytics-analyze-weblogs-job-completed.png)
11. <span data-ttu-id="fecfa-158">Şimdi için 7 - 10 adımı tekrarlayın **Script1.usql**.</span><span class="sxs-lookup"><span data-stu-id="fecfa-158">Now repeat steps 7- 10 for **Script1.usql**.</span></span>

<span data-ttu-id="fecfa-159">**toosee hello iş çıktısı**</span><span class="sxs-lookup"><span data-stu-id="fecfa-159">**toosee hello job output**</span></span>

1. <span data-ttu-id="fecfa-160">Gelen **Sunucu Gezgini**, genişletin **Azure**, genişletin **Data Lake Analytics**, Data Lake Analytics hesabınızı genişletin, **depolama hesapları**hello varsayılan Data Lake Store hesabına sağ tıklayın ve ardından **Explorer**.</span><span class="sxs-lookup"><span data-stu-id="fecfa-160">From **Server Explorer**, expand **Azure**, expand **Data Lake Analytics**, expand your Data Lake Analytics account, expand **Storage Accounts**, right-click hello default Data Lake Storage account, and then click **Explorer**.</span></span>
2. <span data-ttu-id="fecfa-161">Çift **örnekleri** tooopen hello klasörü, çift tıklayın ve ardından **çıkışları**.</span><span class="sxs-lookup"><span data-stu-id="fecfa-161">Double-click **Samples** tooopen hello folder, and then double-click **Outputs**.</span></span>
3. <span data-ttu-id="fecfa-162">Çift **UnsuccessfulResponsees.log**.</span><span class="sxs-lookup"><span data-stu-id="fecfa-162">Double-click **UnsuccessfulResponsees.log**.</span></span>
4. <span data-ttu-id="fecfa-163">Toohello çıkış doğrudan sipariş toonavigate hello işinde hello grafik görünümü içinde hello çıktı dosyasına çift tıklayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fecfa-163">You can also double-click hello output file inside hello graph view of hello job in order toonavigate directly toohello output.</span></span>

## <a name="see-also"></a><span data-ttu-id="fecfa-164">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="fecfa-164">See also</span></span>
<span data-ttu-id="fecfa-165">farklı araçları kullanarak Data Lake Analytics ile çalışmaya tooget bakın:</span><span class="sxs-lookup"><span data-stu-id="fecfa-165">tooget started with Data Lake Analytics using different tools, see:</span></span>

* [<span data-ttu-id="fecfa-166">Azure Portal'ı kullanarak Data Lake Analytics ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="fecfa-166">Get started with Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="fecfa-167">Azure PowerShell'i kullanarak Data Lake Analytics ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="fecfa-167">Get started with Data Lake Analytics using Azure PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="fecfa-168">.NET SDK'yı kullanarak Data Lake Analytics ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="fecfa-168">Get started with Data Lake Analytics using .NET SDK</span></span>](data-lake-analytics-get-started-net-sdk.md)
