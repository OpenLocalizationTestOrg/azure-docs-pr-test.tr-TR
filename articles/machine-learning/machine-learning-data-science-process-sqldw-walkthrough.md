---
title: "eylemin Hello takım veri bilimi işlemi: SQL Data Warehouse kullanarak | Microsoft Docs"
description: "Gelişmiş analizler işlemi ve eylem teknoloji"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 88ba8e28-0bd7-49fe-8320-5dfa83b65724
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;hangzh;weig
ms.openlocfilehash: b1b6371583a023d32e33db59464cafd8c3b767d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action-using-sql-data-warehouse"></a><span data-ttu-id="1c7d3-103">eylemin Hello takım veri bilimi işlemi: SQL Data Warehouse kullanma</span><span class="sxs-lookup"><span data-stu-id="1c7d3-103">hello Team Data Science Process in action: using SQL Data Warehouse</span></span>
<span data-ttu-id="1c7d3-104">Bu öğreticide, biz, oluşturma ve dağıtma SQL veri ambarı (SQL DW) kullanarak bir makine öğrenimi modeline aracılığıyla genel kullanıma açık bir veri kümesi için--hello yol [NYC ücreti dönüşleri](http://www.andresmh.com/nyctaxitrips/) veri kümesi.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-104">In this tutorial, we walk you through building and deploying a machine learning model using SQL Data Warehouse (SQL DW) for a publicly available dataset -- hello [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset.</span></span> <span data-ttu-id="1c7d3-105">Merhaba ikili sınıflandırma model oluşturulmuş bir ipucu seyahat için ödeme ve çok sınıflı sınıflandırma ve regresyon modeli de, ücretli hello ipucu tutarlarının hello dağıtım tahmin açıklanan olup olmadığını tahmin eder.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-105">hello binary classification model constructed predicts whether or not a tip is paid for a trip, and models for multiclass classification and regression are also discussed that predict hello distribution for hello tip amounts paid.</span></span>

<span data-ttu-id="1c7d3-106">Merhaba yordamdan sonraki hello [takım veri bilimi işlem (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) iş akışı.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-106">hello procedure follows hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) workflow.</span></span> <span data-ttu-id="1c7d3-107">Gösteriyoruz nasıl toosetup veri bilimi ortamı nasıl tooload SQL DW veri hello ve nasıl SQL DW ya da bir IPython dizüstü tooexplore hello veri ve mühendislik özellikleri toomodel kullanın.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-107">We show how toosetup a data science environment, how tooload hello data into SQL DW, and how use either SQL DW or an IPython Notebook tooexplore hello data and engineer features toomodel.</span></span> <span data-ttu-id="1c7d3-108">Ardından gösteriyoruz nasıl toobuild ve Azure Machine Learning ile bir model dağıtın.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-108">We then show how toobuild and deploy a model with Azure Machine Learning.</span></span>

## <span data-ttu-id="1c7d3-109"><a name="dataset"></a>Merhaba NYC ücreti dönüşleri veri kümesi</span><span class="sxs-lookup"><span data-stu-id="1c7d3-109"><a name="dataset"></a>hello NYC Taxi Trips dataset</span></span>
<span data-ttu-id="1c7d3-110">Merhaba NYC ücreti seyahat veri yaklaşık 20 GB sıkıştırılmış CSV dosyalarının (sıkıştırılmamış ~ 48 GB) oluşan, 173 milyondan fazla kaydı tek tek dönüşleri ve hello fares her seyahat için ücretli.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-110">hello NYC Taxi Trip data consists of about 20GB of compressed CSV files (~48GB uncompressed), recording more than 173 million individual trips and hello fares paid for each trip.</span></span> <span data-ttu-id="1c7d3-111">Zaman, anonim hale getirilen (sürücü) lisans numarası korsan saldırılarına ve medallion (ücreti'nın benzersiz kimliği) numarası hello ve her seyahat kayıt hello alma ve teslim konumları içerir.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-111">Each trip record includes hello pickup and drop-off locations and times, anonymized hack (driver's) license number, and hello medallion (taxi’s unique id) number.</span></span> <span data-ttu-id="1c7d3-112">Merhaba veri hello yıl 2013 tüm dönüşleri kapsayan ve her ay için iki veri kümesi aşağıdaki hello sağlanır:</span><span class="sxs-lookup"><span data-stu-id="1c7d3-112">hello data covers all trips in hello year 2013 and is provided in hello following two datasets for each month:</span></span>

1. <span data-ttu-id="1c7d3-113">Merhaba **trip_data.csv** dosyası yolcu, toplama ve dropoff noktaları, seyahat süresi ve seyahat Uzunluk sayısı gibi seyahat ayrıntılarını içerir.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-113">hello **trip_data.csv** file contains trip details, such as number of passengers, pickup and dropoff points, trip duration, and trip length.</span></span> <span data-ttu-id="1c7d3-114">Birkaç örnek kayıt şunlardır:</span><span class="sxs-lookup"><span data-stu-id="1c7d3-114">Here are a few sample records:</span></span>
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. <span data-ttu-id="1c7d3-115">Merhaba **trip_fare.csv** dosyası ödeme türü, ücreti tutarı, ek ücret ve vergileri, ipuçları ve tolls ve Ücretli hello toplam miktarı gibi her seyahat için ücretli hello ücreti ayrıntılarını içerir.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-115">hello **trip_fare.csv** file contains details of hello fare paid for each trip, such as payment type, fare amount, surcharge and taxes, tips and tolls, and hello total amount paid.</span></span> <span data-ttu-id="1c7d3-116">Birkaç örnek kayıt şunlardır:</span><span class="sxs-lookup"><span data-stu-id="1c7d3-116">Here are a few sample records:</span></span>
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

<span data-ttu-id="1c7d3-117">Merhaba **benzersiz anahtar** toojoin seyahat kullanılan\_veri ve seyahat\_ücreti aşağıdaki üç alanı hello oluşur:</span><span class="sxs-lookup"><span data-stu-id="1c7d3-117">hello **unique key** used toojoin trip\_data and trip\_fare is composed of hello following three fields:</span></span>

* <span data-ttu-id="1c7d3-118">medallion,</span><span class="sxs-lookup"><span data-stu-id="1c7d3-118">medallion,</span></span>
* <span data-ttu-id="1c7d3-119">korsan saldırılarına\_lisans ve</span><span class="sxs-lookup"><span data-stu-id="1c7d3-119">hack\_license and</span></span>
* <span data-ttu-id="1c7d3-120">Toplama\_datetime.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-120">pickup\_datetime.</span></span>

## <span data-ttu-id="1c7d3-121"><a name="mltasks"></a>Üç tür tahmin görevleri adres</span><span class="sxs-lookup"><span data-stu-id="1c7d3-121"><a name="mltasks"></a>Address three types of prediction tasks</span></span>
<span data-ttu-id="1c7d3-122">Biz hello üzerinde temel üç tahmin sorunları formüle *İpucu\_tutar* görevleri modelleme tooillustrate üç tür:</span><span class="sxs-lookup"><span data-stu-id="1c7d3-122">We formulate three prediction problems based on hello *tip\_amount* tooillustrate three kinds of modeling tasks:</span></span>

1. <span data-ttu-id="1c7d3-123">**İkili sınıflandırma**: toopredict olsun veya olmasın bir ipucu Ücretli bir seyahat, yani bir *İpucu\_tutar* büyük $0 pozitif bir örnektir küçük, ancak bir *İpucu\_tutar* 0 / negatif bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-123">**Binary classification**: toopredict whether or not a tip was paid for a trip, i.e. a *tip\_amount* that is greater than $0 is a positive example, while a *tip\_amount* of $0 is a negative example.</span></span>
2. <span data-ttu-id="1c7d3-124">**Çok sınıflı sınıflandırma**: toopredict hello ipucu aralığını Ücretli hello seyahat için.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-124">**Multiclass classification**: toopredict hello range of tip paid for hello trip.</span></span> <span data-ttu-id="1c7d3-125">Biz hello bölmek *İpucu\_tutar* beş depo veya sınıfları:</span><span class="sxs-lookup"><span data-stu-id="1c7d3-125">We divide hello *tip\_amount* into five bins or classes:</span></span>
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. <span data-ttu-id="1c7d3-126">**Regresyon görev**: seyahat için ödenen ucunun toopredict hello tutar.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-126">**Regression task**: toopredict hello amount of tip paid for a trip.</span></span>  

## <span data-ttu-id="1c7d3-127"><a name="setup"></a>Hello Azure veri bilimi ortamı gelişmiş analizler için ayarlama</span><span class="sxs-lookup"><span data-stu-id="1c7d3-127"><a name="setup"></a>Set up hello Azure data science environment for advanced analytics</span></span>
<span data-ttu-id="1c7d3-128">Azure veri bilimi ortamınızı tooset şu adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-128">tooset up your Azure Data Science environment, follow these steps.</span></span>

<span data-ttu-id="1c7d3-129">**Kendi Azure blob storage hesabı oluşturma**</span><span class="sxs-lookup"><span data-stu-id="1c7d3-129">**Create your own Azure blob storage account**</span></span>

* <span data-ttu-id="1c7d3-130">Kendi Azure blob depolama sağlamak için Azure blob depolama içinde veya mümkün olduğunca yakın bir coğrafi konum çok seçin**Orta Güney ABD**, hello NYC ücreti verileri depolandığı olduğu.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-130">When you provision your own Azure blob storage, choose a geo-location for your Azure blob storage in or as close as possible too**South Central US**, which is where hello NYC Taxi data is stored.</span></span> <span data-ttu-id="1c7d3-131">Merhaba veri kendi depolama hesabında hello ortak blob depolama kapsayıcısını tooa kapsayıcısından AzCopy kullanarak kopyalanacak.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-131">hello data will be copied using AzCopy from hello public blob storage container tooa container in your own storage account.</span></span> <span data-ttu-id="1c7d3-132">Merhaba yakın Azure blob depolama alanınızın tooSouth Orta ABD, hello daha hızlı bu görevi (4. adım) tamamlanacaktır.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-132">hello closer your Azure blob storage is tooSouth Central US, hello faster this task (Step 4) will be completed.</span></span>
* <span data-ttu-id="1c7d3-133">toocreate Azure depolama hesabı, adımları özetlenen adresindeki izleyin hello [Azure storage hesapları hakkında](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="1c7d3-133">toocreate your own Azure storage account, follow hello steps outlined at [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="1c7d3-134">Bu kılavuzda daha sonra gerekecek emin toomake notları hello değerleri aşağıdaki depolama hesabı kimlik bilgileri olması.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-134">Be sure toomake notes on hello values for following storage account credentials as they will be needed later in this walkthrough.</span></span>
  
  * <span data-ttu-id="1c7d3-135">**Depolama hesabı adı**</span><span class="sxs-lookup"><span data-stu-id="1c7d3-135">**Storage Account Name**</span></span>
  * <span data-ttu-id="1c7d3-136">**Depolama hesabı anahtarı**</span><span class="sxs-lookup"><span data-stu-id="1c7d3-136">**Storage Account Key**</span></span>
  * <span data-ttu-id="1c7d3-137">**Kapsayıcı adı** (hangi hello Azure blob depolamada depolanan hello veri toobe istediğiniz)</span><span class="sxs-lookup"><span data-stu-id="1c7d3-137">**Container Name** (which you want hello data toobe stored in hello Azure blob storage)</span></span>

<span data-ttu-id="1c7d3-138">**Azure SQL DW örneğinizi sağlayın.**</span><span class="sxs-lookup"><span data-stu-id="1c7d3-138">**Provision your Azure SQL DW instance.**</span></span>
<span data-ttu-id="1c7d3-139">Merhaba belgelerine izleyin [SQL Data Warehouse oluşturma](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) tooprovision bir SQL Data Warehouse örneğine.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-139">Follow hello documentation at [Create a SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) tooprovision a SQL Data Warehouse instance.</span></span> <span data-ttu-id="1c7d3-140">Sonraki adımlarda kullanılacak olan SQL Data Warehouse kimlik bilgilerini aşağıdaki hello üzerinde gösterimler yaptığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-140">Make sure that you make notations on hello following SQL Data Warehouse credentials which will be used in later steps.</span></span>

* <span data-ttu-id="1c7d3-141">**Sunucu adı**: <server Name>. database.windows.net</span><span class="sxs-lookup"><span data-stu-id="1c7d3-141">**Server Name**: <server Name>.database.windows.net</span></span>
* <span data-ttu-id="1c7d3-142">**SQLDW (veritabanı) adı**</span><span class="sxs-lookup"><span data-stu-id="1c7d3-142">**SQLDW (Database) Name**</span></span>
* <span data-ttu-id="1c7d3-143">**Kullanıcı Adı**</span><span class="sxs-lookup"><span data-stu-id="1c7d3-143">**Username**</span></span>
* <span data-ttu-id="1c7d3-144">**Parola**</span><span class="sxs-lookup"><span data-stu-id="1c7d3-144">**Password**</span></span>

<span data-ttu-id="1c7d3-145">**Visual Studio ve SQL Server veri araçları yükleyin.**</span><span class="sxs-lookup"><span data-stu-id="1c7d3-145">**Install Visual Studio and SQL Server Data Tools.**</span></span> <span data-ttu-id="1c7d3-146">Yönergeler için bkz: [yükleme Visual Studio 2015 ve/veya SQL Data Warehouse için SSDT (SQL Server veri araçları)](../sql-data-warehouse/sql-data-warehouse-install-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="1c7d3-146">For instructions, see [Install Visual Studio 2015 and/or SSDT (SQL Server Data Tools) for SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-install-visual-studio.md).</span></span>

<span data-ttu-id="1c7d3-147">**Azure SQL DW tooyour Visual Studio'ya bağlanın.**</span><span class="sxs-lookup"><span data-stu-id="1c7d3-147">**Connect tooyour Azure SQL DW with Visual Studio.**</span></span> <span data-ttu-id="1c7d3-148">1. ve 2. adımları yönergeler için bkz [tooAzure SQL Data Warehouse ile Visual Studio bağlanmak](../sql-data-warehouse/sql-data-warehouse-connect-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1c7d3-148">For instructions, see steps 1 & 2 in [Connect tooAzure SQL Data Warehouse with Visual Studio](../sql-data-warehouse/sql-data-warehouse-connect-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="1c7d3-149">Çalışma Merhaba, oluşturduğunuz SQL Data Warehouse'da SQL sorgusu hello veritabanında aşağıdaki (Merhaba 3. adımında sağlanan hello sorgu yerine konusuna bağlanmak) çok**bir ana anahtar oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-149">Run hello following SQL query on hello database you created in your SQL Data Warehouse (instead of hello query provided in step 3 of hello connect topic,) too**create a master key**.</span></span>
> 
> 

    BEGIN TRY
           --Try toocreate hello master key
        CREATE MASTER KEY
    END TRY
    BEGIN CATCH
           --If hello master key exists, do nothing
    END CATCH;

<span data-ttu-id="1c7d3-150">**Azure aboneliğiniz altında bir Azure Machine Learning çalışma alanı oluşturun.**</span><span class="sxs-lookup"><span data-stu-id="1c7d3-150">**Create an Azure Machine Learning workspace under your Azure subscription.**</span></span> <span data-ttu-id="1c7d3-151">Yönergeler için bkz: [bir Azure Machine Learning çalışma alanı oluşturma](machine-learning-create-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="1c7d3-151">For instructions, see [Create an Azure Machine Learning workspace](machine-learning-create-workspace.md).</span></span>

## <span data-ttu-id="1c7d3-152"><a name="getdata"></a>Merhaba verileri SQL Data Warehouse'a veri yükleme</span><span class="sxs-lookup"><span data-stu-id="1c7d3-152"><a name="getdata"></a>Load hello data into SQL Data Warehouse</span></span>
<span data-ttu-id="1c7d3-153">Bir Windows PowerShell komut konsolunu açın.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-153">Open a Windows PowerShell command console.</span></span> <span data-ttu-id="1c7d3-154">Merhaba aşağıdaki komutu çalıştırarak PowerShell biz ile Merhaba parametresiyle belirttiğiniz GitHub tooa yerel dizin üzerinde paylaştığınız toodownload hello örnek SQL komut dosyaları komutları *- DestDir*.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-154">Run hello following PowerShell commands toodownload hello example SQL script files that we share with you on GitHub tooa local directory that you specify with hello parameter *-DestDir*.</span></span> <span data-ttu-id="1c7d3-155">Parametre hello değerini değiştirebilir *- DestDir* tooany yerel dizin.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-155">You can change hello value of parameter *-DestDir* tooany local directory.</span></span> <span data-ttu-id="1c7d3-156">Varsa *- DestDir* yok, hello PowerShell betiği tarafından oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-156">If *-DestDir* does not exist, it will be created by hello PowerShell script.</span></span>

> [!NOTE]
> <span data-ttu-id="1c7d3-157">Çok gerekebilecek**yönetici olarak çalıştır** , PowerShell Betiği aşağıdaki hello yürütürken, *DestDir* directory yönetici ayrıcalığı toocreate veya toowrite tooit gerekir.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-157">You might need too**Run as Administrator** when executing hello following PowerShell script if your *DestDir* directory needs Administrator privilege toocreate or toowrite tooit.</span></span>
> 
> 

    $source = "https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/SQLDW/Download_Scripts_SQLDW_Walkthrough.ps1"
    $ps1_dest = "$pwd\Download_Scripts_SQLDW_Walkthrough.ps1"
    $wc = New-Object System.Net.WebClient
    $wc.DownloadFile($source, $ps1_dest)
    .\Download_Scripts_SQLDW_Walkthrough.ps1 –DestDir 'C:\tempSQLDW'

<span data-ttu-id="1c7d3-158">Başarılı yürütme sonrasında, geçerli çalışma dizini değiştirir çok*- DestDir*.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-158">After successful execution, your current working directory changes too*-DestDir*.</span></span> <span data-ttu-id="1c7d3-159">Görüyor olmalısınız gibi toosee ekranın altına:</span><span class="sxs-lookup"><span data-stu-id="1c7d3-159">You should be able toosee screen like below:</span></span>

![][19]

<span data-ttu-id="1c7d3-160">İçinde *- DestDir*, Yönetici modunda PowerShell Betiği aşağıdaki hello yürütün:</span><span class="sxs-lookup"><span data-stu-id="1c7d3-160">In your *-DestDir*, execute hello following PowerShell script in administrator mode:</span></span>

    ./SQLDW_Data_Import.ps1

<span data-ttu-id="1c7d3-161">Merhaba PowerShell Betiği hello için ilk kez çalıştığında, tooinput hello bilgileri, Azure SQL DW ve Azure blob depolama hesabınız istenir.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-161">When hello PowerShell script runs for hello first time, you will be asked tooinput hello information from your Azure SQL DW and your Azure blob storage account.</span></span> <span data-ttu-id="1c7d3-162">Bu PowerShell betik tamamlandığında, ilk kez, hello kimlik Merhaba çalıştıran, giriş tooa yapılandırma dosyası SQLDW.conf hello mevcut çalışma dizini içinde yazılan.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-162">When this PowerShell script completes running for hello first time, hello credentials you input will have been written tooa configuration file SQLDW.conf in hello present working directory.</span></span> <span data-ttu-id="1c7d3-163">Merhaba bu PowerShell komut dosyası gelecekteki yürütülmesi hello seçeneği tooread tüm gerekli parametreleri bu yapılandırma dosyasından sahiptir.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-163">hello future run of this PowerShell script file has hello option tooread all needed parameters from this configuration file.</span></span> <span data-ttu-id="1c7d3-164">Bazı parametreler toochange gerekiyorsa, tooinput hello parametreleri Merhaba ekranında bu yapılandırma dosyasını silerek ve istendiğinde hello parametre değerlerinden giriş yapma istemi veya toochange hello parametre değerlerini bağlı hello SQLDW.conf dosyasını düzenleyerek seçebilirsiniz içinde *- DestDir* dizini.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-164">If you need toochange some parameters, you can choose tooinput hello parameters on hello screen upon prompt by deleting this configuration file and inputting hello parameters values as prompted or toochange hello parameter values by editing hello SQLDW.conf file in your *-DestDir* directory.</span></span>

> [!NOTE]
> <span data-ttu-id="1c7d3-165">Parametreleri doğrudan hello SQLDW.conf dosyasından okurken, Azure SQL DW zaten mevcut olanla sipariş tooavoid şema adı çakışmaları içinde 3 basamaklı bir rastgele sayı toohello şema adı hello SQLDW.conf dosyasından hello varsayılan şema adı olarak eklenir Her Çalıştır.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-165">In order tooavoid schema name conflicts with those that already exist in your Azure SQL DW, when reading parameters directly from hello SQLDW.conf file, a 3-digit random number is added toohello schema name from hello SQLDW.conf file as hello default schema name for each run.</span></span> <span data-ttu-id="1c7d3-166">Merhaba PowerShell Betiği isteminde bir şema adı: Merhaba adı kullanıcı kümeleri belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-166">hello PowerShell script may prompt you for a schema name: hello name may be specified at user discretion.</span></span>
> 
> 

<span data-ttu-id="1c7d3-167">Bu **PowerShell Betiği** dosya hello aşağıdaki görevleri tamamlar:</span><span class="sxs-lookup"><span data-stu-id="1c7d3-167">This **PowerShell script** file completes hello following tasks:</span></span>

* <span data-ttu-id="1c7d3-168">**İndirir ve AzCopy yükler**, AzCopy zaten yüklü değilse</span><span class="sxs-lookup"><span data-stu-id="1c7d3-168">**Downloads and installs AzCopy**, if AzCopy is not already installed</span></span>
  
        $AzCopy_path = SearchAzCopy
        if ($AzCopy_path -eq $null){
               Write-Host "AzCopy.exe is not found in C:\Program Files*. Now, start installing AzCopy..." -ForegroundColor "Yellow"
            InstallAzCopy
            $AzCopy_path = SearchAzCopy
        }
            $env_path = $env:Path
            for ($i=0; $i -lt $AzCopy_path.count; $i++){
                if ($AzCopy_path.count -eq 1){
                    $AzCopy_path_i = $AzCopy_path
                } else {
                    $AzCopy_path_i = $AzCopy_path[$i]
                }
                if ($env_path -notlike '*' +$AzCopy_path_i+'*'){
                    Write-Host $AzCopy_path_i 'not in system path, add it...'
                    [Environment]::SetEnvironmentVariable("Path", "$AzCopy_path_i;$env_path", "Machine")
                    $env:Path = [System.Environment]::GetEnvironmentVariable("Path","Machine")
                    $env_path = $env:Path
                }
* <span data-ttu-id="1c7d3-169">**Kopyalar veri tooyour özel blob storage hesabı** hello ortak blob AzCopy ile gelen</span><span class="sxs-lookup"><span data-stu-id="1c7d3-169">**Copies data tooyour private blob storage account** from hello public blob with AzCopy</span></span>
  
        Write-Host "AzCopy is copying data from public blob tooyo storage account. It may take a while..." -ForegroundColor "Yellow"
        $start_time = Get-Date
        AzCopy.exe /Source:$Source /Dest:$DestURL /DestKey:$StorageAccountKey /S
        $end_time = Get-Date
        $time_span = $end_time - $start_time
        $total_seconds = [math]::Round($time_span.TotalSeconds,2)
        Write-Host "AzCopy finished copying data. Please check your storage account tooverify." -ForegroundColor "Yellow"
        Write-Host "This step (copying data from public blob tooyour storage account) takes $total_seconds seconds." -ForegroundColor "Green"
* <span data-ttu-id="1c7d3-170">**(LoadDataToSQLDW.sql çalıştırarak) Polybase tooyour Azure SQL DW kullanarak verileri yükler** komutları aşağıdaki hello ile özel blob depolama hesabınızdan.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-170">**Loads data using Polybase (by executing LoadDataToSQLDW.sql) tooyour Azure SQL DW** from your private blob storage account with hello following commands.</span></span>
  
  * <span data-ttu-id="1c7d3-171">Bir şema oluşturun</span><span class="sxs-lookup"><span data-stu-id="1c7d3-171">Create a schema</span></span>
    
          EXEC (''CREATE SCHEMA {schemaname};'');
  * <span data-ttu-id="1c7d3-172">Bir veritabanı kapsamlı kimlik bilgisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="1c7d3-172">Create a database scoped credential</span></span>
    
          CREATE DATABASE SCOPED CREDENTIAL {KeyAlias}
          WITH IDENTITY = ''asbkey'' ,
          Secret = ''{StorageAccountKey}''
  * <span data-ttu-id="1c7d3-173">Bir Azure depolama blob için bir dış veri kaynağı oluşturun</span><span class="sxs-lookup"><span data-stu-id="1c7d3-173">Create an external data source for an Azure storage blob</span></span>
    
          CREATE EXTERNAL DATA SOURCE {nyctaxi_trip_storage}
          WITH
          (
              TYPE = HADOOP,
              LOCATION =''wasbs://{ContainerName}@{StorageAccountName}.blob.core.windows.net'',
              CREDENTIAL = {KeyAlias}
          )
          ;
    
          CREATE EXTERNAL DATA SOURCE {nyctaxi_fare_storage}
          WITH
          (
              TYPE = HADOOP,
              LOCATION =''wasbs://{ContainerName}@{StorageAccountName}.blob.core.windows.net'',
              CREDENTIAL = {KeyAlias}
          )
          ;
  * <span data-ttu-id="1c7d3-174">Bir csv dosyası için bir dış dosya biçimi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-174">Create an external file format for a csv file.</span></span> <span data-ttu-id="1c7d3-175">Veri sıkıştırılmamış ve alanlar hello dikey çizgi karakteriyle ayrılır.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-175">Data is uncompressed and fields are separated with hello pipe character.</span></span>
    
          CREATE EXTERNAL FILE FORMAT {csv_file_format}
          WITH
          (   
              FORMAT_TYPE = DELIMITEDTEXT,
              FORMAT_OPTIONS  
              (
                  FIELD_TERMINATOR ='','',
                  USE_TYPE_DEFAULT = TRUE
              )
          )
          ;
  * <span data-ttu-id="1c7d3-176">Dış ücreti ve seyahat tabloları NYC ücreti veri kümesi için Azure blob depolama alanına oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-176">Create external fare and trip tables for NYC taxi dataset in Azure blob storage.</span></span>
    
          CREATE EXTERNAL TABLE {external_nyctaxi_fare}
          (
              medallion varchar(50) not null,
              hack_license varchar(50) not null,
              vendor_id char(3),
              pickup_datetime datetime not null,
              payment_type char(3),
              fare_amount float,
              surcharge float,
              mta_tax float,
              tip_amount float,
              tolls_amount float,
              total_amount float
          )
          with (
              LOCATION    = ''/nyctaxifare/'',
              DATA_SOURCE = {nyctaxi_fare_storage},
              FILE_FORMAT = {csv_file_format},
              REJECT_TYPE = VALUE,
              REJECT_VALUE = 12     
          )  

            CREATE EXTERNAL TABLE {external_nyctaxi_trip}
            (
                   medallion varchar(50) not null,
                   hack_license varchar(50)  not null,
                   vendor_id char(3),
                   rate_code char(3),
                   store_and_fwd_flag char(3),
                   pickup_datetime datetime  not null,
                   dropoff_datetime datetime,
                   passenger_count int,
                   trip_time_in_secs bigint,
                   trip_distance float,
                   pickup_longitude varchar(30),
                   pickup_latitude varchar(30),
                   dropoff_longitude varchar(30),
                   dropoff_latitude varchar(30)
            )
            with (
                LOCATION    = ''/nyctaxitrip/'',
                DATA_SOURCE = {nyctaxi_trip_storage},
                FILE_FORMAT = {csv_file_format},
                REJECT_TYPE = VALUE,
                REJECT_VALUE = 12         
            )

    - <span data-ttu-id="1c7d3-177">Dış tablolarda bulunan Azure blob depolama tooSQL veri ambarı veri yükleme</span><span class="sxs-lookup"><span data-stu-id="1c7d3-177">Load data from external tables in Azure blob storage tooSQL Data Warehouse</span></span>

            CREATE TABLE {schemaname}.{nyctaxi_fare}
            WITH
            (   
                CLUSTERED COLUMNSTORE INDEX,
                DISTRIBUTION = HASH(medallion)
            )
            AS
            SELECT *
            FROM   {external_nyctaxi_fare}
            ;

            CREATE TABLE {schemaname}.{nyctaxi_trip}
            WITH
            (   
                CLUSTERED COLUMNSTORE INDEX,
                DISTRIBUTION = HASH(medallion)
            )
            AS
            SELECT *
            FROM   {external_nyctaxi_trip}
            ;

    - <span data-ttu-id="1c7d3-178">Örnek veri tablosu (NYCTaxi_Sample) oluşturma ve veri tooit SQL sorguları hello seyahat ve ücreti tablolarda seçerek ekleyin.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-178">Create a sample data table (NYCTaxi_Sample) and insert data tooit from selecting SQL queries on hello trip and fare tables.</span></span> <span data-ttu-id="1c7d3-179">(Bu kılavuzun bazı adımlar gerekir toouse Bu örnek tablo.)</span><span class="sxs-lookup"><span data-stu-id="1c7d3-179">(Some steps of this walkthrough needs toouse this sample table.)</span></span>

            CREATE TABLE {schemaname}.{nyctaxi_sample}
            WITH
            (   
                CLUSTERED COLUMNSTORE INDEX,
                DISTRIBUTION = HASH(medallion)
            )
            AS
            (
                SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount, f.total_amount, f.tip_amount,
                tipped = CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END,
                tip_class = CASE
                        WHEN (tip_amount = 0) THEN 0
                        WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
                        WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
                        WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
                        ELSE 4
                    END
                FROM {schemaname}.{nyctaxi_trip} t, {schemaname}.{nyctaxi_fare} f
                WHERE datepart("mi",t.pickup_datetime) = 1
                AND t.medallion = f.medallion
                AND   t.hack_license = f.hack_license
                AND   t.pickup_datetime = f.pickup_datetime
                AND   pickup_longitude <> ''0''
                AND   dropoff_longitude <> ''0''
            )
            ;

<span data-ttu-id="1c7d3-180">Depolama hesaplarınızı coğrafi konumunu Hello yükleme süreleri etkiler.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-180">hello geographic location of your storage accounts affects load times.</span></span>

> [!NOTE]
> <span data-ttu-id="1c7d3-181">Merhaba coğrafi konumunu özel blob depolama hesabınıza bağlı olarak, bir ortak blob tooyour özel depolama hesabından veri kopyalama işleminin hello yaklaşık 15 dakika alabilir, ya da daha uzun ve hello işlem depolama hesabınızdan veri yükleme Azure SQL DW tooyour 20 dakika sürebilir veya daha uzun.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-181">Depending on hello geographical location of your private blob storage account, hello process of copying data from a public blob tooyour private storage account can take about 15 minutes, or even longer,and hello process of loading data from your storage account tooyour Azure SQL DW could take 20 minutes or longer.</span></span>  
> 
> 

<span data-ttu-id="1c7d3-182">Yinelenen kaynak ve hedef dosya varsa ne toodecide sahip olur.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-182">You will have toodecide what do if you have duplicate source and destination files.</span></span>

> [!NOTE]
> <span data-ttu-id="1c7d3-183">Merhaba ortak blob depolama tooyour özel blob depolama hesabından zaten kopyalanan hello .csv dosyaları toobe özel blob depolama hesabınız yoksa, AzCopy, toooverwrite isteyip istemediğinizi sorar bunları.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-183">If hello .csv files toobe copied from hello public blob storage tooyour private blob storage account already exist in your private blob storage account, AzCopy will ask you whether you want toooverwrite them.</span></span> <span data-ttu-id="1c7d3-184">Toooverwrite istemiyorsanız, bunları, giriş  **n**  istendiğinde.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-184">If you do not want toooverwrite them, input **n** when prompted.</span></span> <span data-ttu-id="1c7d3-185">Toooverwrite istiyorsanız **tüm** birini giriş **bir** istendiğinde.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-185">If you want toooverwrite **all** of them, input **a** when prompted.</span></span> <span data-ttu-id="1c7d3-186">Ayrıca giriş **y** toooverwrite .csv dosyalarını tek tek.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-186">You can also input **y** toooverwrite .csv files individually.</span></span>
> 
> 

![#21 Çiz][21]

<span data-ttu-id="1c7d3-188">Kendi verilerinizi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-188">You can use your own data.</span></span> <span data-ttu-id="1c7d3-189">Verilerinizi şirket içi makinenizdeki gerçek hayatta uygulamanızda ise, AzCopy tooupload şirket içi veri tooyour özel Azure blob depolama kullanmaya devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-189">If your data is in your on-premises machine in your real life application, you can still use AzCopy tooupload on-premises data tooyour private Azure blob storage.</span></span> <span data-ttu-id="1c7d3-190">Toochange hello yeterlidir **kaynak** konumu, `$Source = "http://getgoing.blob.core.windows.net/public/nyctaxidataset"`, hello verilerinizi içeren hello PowerShell komut dosyası toohello yerel dizinin AzCopy komut içinde.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-190">You only need toochange hello **Source** location, `$Source = "http://getgoing.blob.core.windows.net/public/nyctaxidataset"`, in hello AzCopy command of hello PowerShell script file toohello local directory that contains your data.</span></span>

> [!TIP]
> <span data-ttu-id="1c7d3-191">Verilerinizi gerçek hayatta uygulamanızda özel Azure blob depolama alanınızın zaten kullanılıyor AzCopy hello PowerShell Betiği adım ve doğrudan hello veri tooAzure SQL DW karşıya hello atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-191">If your data is already in your private Azure blob storage in your real life application, you can skip hello AzCopy step in hello PowerShell script and directly upload hello data tooAzure SQL DW.</span></span> <span data-ttu-id="1c7d3-192">Bu ek hello betik tootailor onu verilerinizi toohello biçimlerinin düzenler gerektirir.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-192">This will require additional edits of hello script tootailor it toohello format of your data.</span></span>
> 
> 

<span data-ttu-id="1c7d3-193">Bu üç dosya anında çalıştı hazır toobe; böylece bu Powershell betiğini de hello Azure SQL DW bilgi hello veri araştırması örnek dosyalara SQLDW_Explorations.sql, SQLDW_Explorations.ipynb ve SQLDW_Explorations_Scripts.py içinde takılan Merhaba PowerShell komut dosyası tamamlandıktan sonra.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-193">This Powershell script also plugs in hello Azure SQL DW information into hello data exploration example files SQLDW_Explorations.sql, SQLDW_Explorations.ipynb, and SQLDW_Explorations_Scripts.py so that these three files are ready toobe tried out instantly after hello PowerShell script completes.</span></span>

<span data-ttu-id="1c7d3-194">Başarılı bir yürütme sonrasında ekran görürsünüz aşağıdaki gibi:</span><span class="sxs-lookup"><span data-stu-id="1c7d3-194">After a successful execution, you will see screen like below:</span></span>

![][20]

## <span data-ttu-id="1c7d3-195"><a name="dbexplore"></a>Veri keşfi ve Azure SQL Data Warehouse özellik Mühendisliği</span><span class="sxs-lookup"><span data-stu-id="1c7d3-195"><a name="dbexplore"></a>Data exploration and feature engineering in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="1c7d3-196">Bu bölümde, biz veri keşfi ve özellik nesil SQL sorgularını kullanarak doğrudan Azure SQL DW karşı çalıştırarak gerçekleştirebilirsiniz **Visual Studio veri Araçları**.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-196">In this section, we perform data exploration and feature generation by running SQL queries against Azure SQL DW directly using **Visual Studio Data Tools**.</span></span> <span data-ttu-id="1c7d3-197">Bu bölümde kullanılan tüm SQL sorguları adlı hello örnek komut dosyasında bulunabilir *SQLDW_Explorations.sql*.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-197">All SQL queries used in this section can be found in hello sample script named *SQLDW_Explorations.sql*.</span></span> <span data-ttu-id="1c7d3-198">Bu dosya indirilen tooyour yerel dizin hello PowerShell komut dosyası tarafından zaten etkinleştirilmiş.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-198">This file has already been downloaded tooyour local directory by hello PowerShell script.</span></span> <span data-ttu-id="1c7d3-199">Buradan da alabilir [GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/SQLDW/SQLDW_Explorations.sql).</span><span class="sxs-lookup"><span data-stu-id="1c7d3-199">You can also retrieve it from [GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/SQLDW/SQLDW_Explorations.sql).</span></span> <span data-ttu-id="1c7d3-200">Ancak GitHub hello dosyasında prize takılı hello Azure SQL DW bilgileri yok.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-200">But hello file in GitHub does not have hello Azure SQL DW information plugged in.</span></span>

<span data-ttu-id="1c7d3-201">Tooyour hello SQL DW oturum açma adı ve parola ile Visual Studio kullanarak Azure SQL DW bağlanmak ve hello açın **SQL Nesne Gezgini** tooconfirm hello veritabanını ve tabloları içe aktarıldı.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-201">Connect tooyour Azure SQL DW using Visual Studio with hello SQL DW login name and password and open up hello **SQL Object Explorer** tooconfirm hello database and tables have been imported.</span></span> <span data-ttu-id="1c7d3-202">Merhaba almak *SQLDW_Explorations.sql* dosya.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-202">Retrieve hello *SQLDW_Explorations.sql* file.</span></span>

> [!NOTE]
> <span data-ttu-id="1c7d3-203">tooopen paralel veri ambarı (PDW) sorgu düzenleyicisi kullanın hello **yeni sorgu** , PDW hello seçiliyken komut **SQL Nesne Gezgini**.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-203">tooopen a Parallel Data Warehouse (PDW) query editor, use hello **New Query** command while your PDW is selected in hello **SQL Object Explorer**.</span></span> <span data-ttu-id="1c7d3-204">Merhaba standart SQL sorgu Düzenleyicisi'ni PDW tarafından desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-204">hello standard SQL query editor is not supported by PDW.</span></span>
> 
> 

<span data-ttu-id="1c7d3-205">Veri türünü hello İşte araştırması ve özellik oluşturma görevleri gerçekleştirilen Bu bölümde:</span><span class="sxs-lookup"><span data-stu-id="1c7d3-205">Here are hello type of data exploration and feature generation tasks performed in this section:</span></span>

* <span data-ttu-id="1c7d3-206">Veri dağıtımları değişen zaman pencereleri birkaç alanların keşfedin.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-206">Explore data distributions of a few fields in varying time windows.</span></span>
* <span data-ttu-id="1c7d3-207">Veri Kalitesi hello boylam ve enlem alanlarının araştırın.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-207">Investigate data quality of hello longitude and latitude fields.</span></span>
* <span data-ttu-id="1c7d3-208">Merhaba üzerinde dayalı çok sınıflı ve ikili sınıflandırma etiketleri oluşturmak **İpucu\_tutar**.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-208">Generate binary and multiclass classification labels based on hello **tip\_amount**.</span></span>
* <span data-ttu-id="1c7d3-209">Özellikler oluşturmak ve işlem/seyahat uzaklıklar karşılaştırın.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-209">Generate features and compute/compare trip distances.</span></span>
* <span data-ttu-id="1c7d3-210">Merhaba iki tabloları birleştirme ve kullanılan toobuild modelleri olacaktır rasgele bir örnek ayıklayın.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-210">Join hello two tables and extract a random sample that will be used toobuild models.</span></span>

### <a name="data-import-verification"></a><span data-ttu-id="1c7d3-211">Veri alma doğrulama</span><span class="sxs-lookup"><span data-stu-id="1c7d3-211">Data import verification</span></span>
<span data-ttu-id="1c7d3-212">Bu sorguları hello sayısı daha önce Polybase'nın Paralel toplu kullanarak doldurulmuş tabloları hello sayfasındaki satır ve sütunları hızlı doğrulanmasını sağlar,</span><span class="sxs-lookup"><span data-stu-id="1c7d3-212">These queries provide a quick verification of hello number of rows and columns in hello tables populated earlier using Polybase's parallel bulk import,</span></span>

    -- Report number of rows in table <nyctaxi_trip> without table scan
    SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_trip>')

    -- Report number of columns in table <nyctaxi_trip>
    SELECT COUNT(*) FROM information_schema.columns WHERE table_name = '<nyctaxi_trip>' AND table_schema = '<schemaname>'

<span data-ttu-id="1c7d3-213">**Çıkış:** 173,179,759 satırları ve sütunları 14 almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-213">**Output:** You should get 173,179,759 rows and 14 columns.</span></span>

### <a name="exploration-trip-distribution-by-medallion"></a><span data-ttu-id="1c7d3-214">Araştırması: Medallion seyahat dağıtım</span><span class="sxs-lookup"><span data-stu-id="1c7d3-214">Exploration: Trip distribution by medallion</span></span>
<span data-ttu-id="1c7d3-215">Bu örnekte sorgu, belirtilen bir süre içinde 100'den fazla dönüşleri tamamlandı hello medallions (ücreti sayılar) tanımlar.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-215">This example query identifies hello medallions (taxi numbers) that completed more than 100 trips within a specified time period.</span></span> <span data-ttu-id="1c7d3-216">Hello sorgu tarafından hello bölümleme düzeni söylediğinizde bu yana bölümlenmiş hello tablo erişimden yararlanan **toplama\_datetime**.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-216">hello query would benefit from hello partitioned table access since it is conditioned by hello partition scheme of **pickup\_datetime**.</span></span> <span data-ttu-id="1c7d3-217">Merhaba tam veri kümesini sorgulama hello bölümlenmiş tablosu kullanın ve/veya dizin tarama ayrıca olun.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-217">Querying hello full dataset will also make use of hello partitioned table and/or index scan.</span></span>

    SELECT medallion, COUNT(*)
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    GROUP BY medallion
    HAVING COUNT(*) > 100

<span data-ttu-id="1c7d3-218">**Çıkış:** hello sorgu hello 13,369 medallions (taksiler) belirtme satırları bir tablo döndürür ve hello 2013'te tarafından tamamladığınız seyahat sayısı.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-218">**Output:** hello query should return a table with rows specifying hello 13,369 medallions (taxis) and hello number of trip completed by them in 2013.</span></span> <span data-ttu-id="1c7d3-219">Merhaba son sütun tamamlandı dönüş hello sayısı hello sayısını içerir.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-219">hello last column contains hello count of hello number of trips completed.</span></span>

### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a><span data-ttu-id="1c7d3-220">Keşfetme: dağıtım medallion ve hack_license tarafından seyahat</span><span class="sxs-lookup"><span data-stu-id="1c7d3-220">Exploration: Trip distribution by medallion and hack_license</span></span>
<span data-ttu-id="1c7d3-221">Bu örnek hello medallions (ücreti sayılar) tanımlar ve hack_license (sürücüler) tamamlanan birden fazla 100 dönüşleri belirtilen süre içinde numaralandırır.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-221">This example identifies hello medallions (taxi numbers) and hack_license numbers (drivers) that completed more than 100 trips within a specified time period.</span></span>

    SELECT medallion, hack_license, COUNT(*)
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130131'
    GROUP BY medallion, hack_license
    HAVING COUNT(*) > 100

<span data-ttu-id="1c7d3-222">**Çıkış:** hello sorgu hello 13,369 araba/sürücü, 100 dönüşleri 2013'te daha tamamladınız kimlikleri belirtme 13,369 satırları içeren bir tablo döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-222">**Output:** hello query should return a table with 13,369 rows specifying hello 13,369 car/driver IDs that have completed more that 100 trips in 2013.</span></span> <span data-ttu-id="1c7d3-223">Merhaba son sütun tamamlandı dönüş hello sayısı hello sayısını içerir.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-223">hello last column contains hello count of hello number of trips completed.</span></span>

### <a name="data-quality-assessment-verify-records-with-incorrect-longitude-andor-latitude"></a><span data-ttu-id="1c7d3-224">Veri Kalitesi değerlendirmesi: yanlış boylam ve/veya enlem ile kayıtlarını doğrulama</span><span class="sxs-lookup"><span data-stu-id="1c7d3-224">Data quality assessment: Verify records with incorrect longitude and/or latitude</span></span>
<span data-ttu-id="1c7d3-225">Merhaba boylam ve/veya enlem alanların hiçbirini ya da geçersiz bir değer içeriyorsa, bu örnek araştırır (radian derece -90 ile 90 arasında olmalıdır), ya da sahip (0, 0) koordinatları.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-225">This example investigates if any of hello longitude and/or latitude fields either contain an invalid value (radian degrees should be between -90 and 90), or have (0, 0) coordinates.</span></span>

    SELECT COUNT(*) FROM <schemaname>.<nyctaxi_trip>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(pickup_latitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_latitude AS float) NOT BETWEEN -90 AND 90
    OR    (pickup_longitude = '0' AND pickup_latitude = '0')
    OR    (dropoff_longitude = '0' AND dropoff_latitude = '0'))

<span data-ttu-id="1c7d3-226">**Çıkış:** hello sorgu geçersiz boylam ve/veya enlem alanınız 837,467 dönüşleri döndürür.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-226">**Output:** hello query returns 837,467 trips that have invalid longitude and/or latitude fields.</span></span>

### <a name="exploration-tipped-vs-not-tipped-trips-distribution"></a><span data-ttu-id="1c7d3-227">Keşfetme: eğimli değil Eğimli dönüşleri dağıtım</span><span class="sxs-lookup"><span data-stu-id="1c7d3-227">Exploration: Tipped vs. not tipped trips distribution</span></span>
<span data-ttu-id="1c7d3-228">Bu örnek belirtilen bir süre içinde (veya burada ayarlanır gibi hello tam yıl kapsayan varsa hello tam veri kümesi) Eğimli değil hello numarası Eğimli dönüş hello sayısı bulur.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-228">This example finds hello number of trips that were tipped vs. hello number that were not tipped in a specified time period (or in hello full dataset if covering hello full year as it is set up here).</span></span> <span data-ttu-id="1c7d3-229">Bu dağıtım için ikili sınıflandırma modelleme daha sonra kullanılan hello ikili etiket dağıtım toobe yansıtır.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-229">This distribution reflects hello binary label distribution toobe later used for binary classification modeling.</span></span>

    SELECT tipped, COUNT(*) AS tip_freq FROM (
      SELECT CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped, tip_amount
      FROM <schemaname>.<nyctaxi_fare>
      WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tipped

<span data-ttu-id="1c7d3-230">**Çıkış:** hello sorgu dönüş hello aşağıdaki ipucu sıklıklarını hello yıl 2013: 90,447,622 Eğimli ve 82,264,709 değil Eğimli için.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-230">**Output:** hello query should return hello following tip frequencies for hello year 2013: 90,447,622 tipped and 82,264,709 not-tipped.</span></span>

### <a name="exploration-tip-classrange-distribution"></a><span data-ttu-id="1c7d3-231">Keşfetme: İpucu sınıfı/range dağıtım</span><span class="sxs-lookup"><span data-stu-id="1c7d3-231">Exploration: Tip class/range distribution</span></span>
<span data-ttu-id="1c7d3-232">Bu örnek hello dağıtımlarında ipucu aralıklarının belirli bir zaman aralığı (veya hello tam yıl kapsayan varsa hello tam veri kümesi) hesaplar.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-232">This example computes hello distribution of tip ranges in a given time period (or in hello full dataset if covering hello full year).</span></span> <span data-ttu-id="1c7d3-233">Daha sonra çok sınıflı sınıflandırma model için kullanılacak hello etiket sınıfların hello dağıtım budur.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-233">This is hello distribution of hello label classes that will be used later for multiclass classification modeling.</span></span>

    SELECT tip_class, COUNT(*) AS tip_freq FROM (
        SELECT CASE
            WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tip_class

<span data-ttu-id="1c7d3-234">**Çıktı:**</span><span class="sxs-lookup"><span data-stu-id="1c7d3-234">**Output:**</span></span>

| <span data-ttu-id="1c7d3-235">tip_class</span><span class="sxs-lookup"><span data-stu-id="1c7d3-235">tip_class</span></span> | <span data-ttu-id="1c7d3-236">tip_freq</span><span class="sxs-lookup"><span data-stu-id="1c7d3-236">tip_freq</span></span> |
| --- | --- |
| <span data-ttu-id="1c7d3-237">1</span><span class="sxs-lookup"><span data-stu-id="1c7d3-237">1</span></span> |<span data-ttu-id="1c7d3-238">82230915</span><span class="sxs-lookup"><span data-stu-id="1c7d3-238">82230915</span></span> |
| <span data-ttu-id="1c7d3-239">2</span><span class="sxs-lookup"><span data-stu-id="1c7d3-239">2</span></span> |<span data-ttu-id="1c7d3-240">6198803</span><span class="sxs-lookup"><span data-stu-id="1c7d3-240">6198803</span></span> |
| <span data-ttu-id="1c7d3-241">3</span><span class="sxs-lookup"><span data-stu-id="1c7d3-241">3</span></span> |<span data-ttu-id="1c7d3-242">1932223</span><span class="sxs-lookup"><span data-stu-id="1c7d3-242">1932223</span></span> |
| <span data-ttu-id="1c7d3-243">0</span><span class="sxs-lookup"><span data-stu-id="1c7d3-243">0</span></span> |<span data-ttu-id="1c7d3-244">82264625</span><span class="sxs-lookup"><span data-stu-id="1c7d3-244">82264625</span></span> |
| <span data-ttu-id="1c7d3-245">4</span><span class="sxs-lookup"><span data-stu-id="1c7d3-245">4</span></span> |<span data-ttu-id="1c7d3-246">85765</span><span class="sxs-lookup"><span data-stu-id="1c7d3-246">85765</span></span> |

### <a name="exploration-compute-and-compare-trip-distance"></a><span data-ttu-id="1c7d3-247">Keşfetme: İşlem ve seyahat uzaklığı karşılaştırma</span><span class="sxs-lookup"><span data-stu-id="1c7d3-247">Exploration: Compute and compare trip distance</span></span>
<span data-ttu-id="1c7d3-248">Bu örnek hello alma ve teslim boylam dönüştürür ve enlem tooSQL Coğrafya noktaları, SQL Coğrafya noktaları fark kullanarak hello seyahat uzaklığı hesaplar ve hello sonuçları karşılaştırma için rastgele bir örneğini döndürür.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-248">This example converts hello pickup and drop-off longitude and latitude tooSQL geography points, computes hello trip distance using SQL geography points difference, and returns a random sample of hello results for comparison.</span></span> <span data-ttu-id="1c7d3-249">Merhaba örneği yalnızca daha önce ele hello veri kalitesi değerlendirme sorgu kullanarak toovalid koordinatları hello sonuçlarını sınırlandırır.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-249">hello example limits hello results toovalid coordinates only using hello data quality assessment query covered earlier.</span></span>

    /****** Object:  UserDefinedFunction [dbo].[fnCalculateDistance] ******/
    SET ANSI_NULLS ON
    GO

    SET QUOTED_IDENTIFIER ON
    GO

    IF EXISTS (SELECT * FROM sys.objects WHERE type IN ('FN', 'IF') AND name = 'fnCalculateDistance')
      DROP FUNCTION fnCalculateDistance
    GO

    -- User-defined function toocalculate hello direct distance  in mile between two geographical coordinates.
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)

    RETURNS float
    AS
    BEGIN
          DECLARE @distance decimal(28, 10)
          -- Convert tooradians
          SET @Lat1 = @Lat1 / 57.2958
          SET @Long1 = @Long1 / 57.2958
          SET @Lat2 = @Lat2 / 57.2958
          SET @Long2 = @Long2 / 57.2958
          -- Calculate distance
          SET @distance = (SIN(@Lat1) * SIN(@Lat2)) + (COS(@Lat1) * COS(@Lat2) * COS(@Long2 - @Long1))
          --Convert toomiles
          IF @distance <> 0
          BEGIN
            SET @distance = 3958.75 * ATAN(SQRT(1 - POWER(@distance, 2)) / @distance);
          END
          RETURN @distance
    END
    GO

    SELECT pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS DirectDistance
    FROM <schemaname>.<nyctaxi_trip>
    WHERE datepart("mi",pickup_datetime)=1
    AND CAST(pickup_latitude AS float) BETWEEN -90 AND 90
    AND CAST(dropoff_latitude AS float) BETWEEN -90 AND 90
    AND pickup_longitude != '0' AND dropoff_longitude != '0'

### <a name="feature-engineering-using-sql-functions"></a><span data-ttu-id="1c7d3-250">Özellik Mühendisliği SQL işlevlerini kullanma</span><span class="sxs-lookup"><span data-stu-id="1c7d3-250">Feature engineering using SQL functions</span></span>
<span data-ttu-id="1c7d3-251">Bazı durumlarda SQL işlevleri özellik Mühendisliği için verimli bir seçenek olabilir.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-251">Sometimes SQL functions can be an efficient option for feature engineering.</span></span> <span data-ttu-id="1c7d3-252">Bu kılavuzda, bir SQL işlevi toocalculate hello doğrudan arasındaki uzaklığı hello alımı ve dropoff konumları tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-252">In this walkthrough, we defined a SQL function toocalculate hello direct distance between hello pickup and dropoff locations.</span></span> <span data-ttu-id="1c7d3-253">SQL komut dosyalarında aşağıdaki hello çalıştırabilirsiniz **Visual Studio veri Araçları**.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-253">You can run hello following SQL scripts in **Visual Studio Data Tools**.</span></span>

<span data-ttu-id="1c7d3-254">Başlangıç uzaklığı işlevi tanımlar hello SQL komut dosyası aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-254">Here is hello SQL script that defines hello distance function.</span></span>

    SET ANSI_NULLS ON
    GO

    SET QUOTED_IDENTIFIER ON
    GO

    IF EXISTS (SELECT * FROM sys.objects WHERE type IN ('FN', 'IF') AND name = 'fnCalculateDistance')
      DROP FUNCTION fnCalculateDistance
    GO

    -- User-defined function calculate hello direct distance between two geographical coordinates.
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)

    RETURNS float
    AS
    BEGIN
          DECLARE @distance decimal(28, 10)
          -- Convert tooradians
          SET @Lat1 = @Lat1 / 57.2958
          SET @Long1 = @Long1 / 57.2958
          SET @Lat2 = @Lat2 / 57.2958
          SET @Long2 = @Long2 / 57.2958
          -- Calculate distance
          SET @distance = (SIN(@Lat1) * SIN(@Lat2)) + (COS(@Lat1) * COS(@Lat2) * COS(@Long2 - @Long1))
          --Convert toomiles
          IF @distance <> 0
          BEGIN
            SET @distance = 3958.75 * ATAN(SQRT(1 - POWER(@distance, 2)) / @distance);
          END
          RETURN @distance
    END
    GO

<span data-ttu-id="1c7d3-255">SQL sorgusunda bu işlevi toogenerate özelliğe bir örnek toocall şöyledir:</span><span class="sxs-lookup"><span data-stu-id="1c7d3-255">Here is an example toocall this function toogenerate features in your SQL query:</span></span>

    -- Sample query toocall hello function toocreate features
    SELECT pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS DirectDistance
    FROM <schemaname>.<nyctaxi_trip>
    WHERE datepart("mi",pickup_datetime)=1
    AND CAST(pickup_latitude AS float) BETWEEN -90 AND 90
    AND CAST(dropoff_latitude AS float) BETWEEN -90 AND 90
    AND pickup_longitude != '0' AND dropoff_longitude != '0'

<span data-ttu-id="1c7d3-256">**Çıkış:** bu sorgu ile alımı ve dropoff latitudes (2,803,538 satırlar) içeren bir tablo oluşturur ve longitudes ve hello karşılık gelen doğrudan mil cinsinden.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-256">**Output:** This query generates a table (with 2,803,538 rows) with pickup and dropoff latitudes and longitudes and hello corresponding direct distances in miles.</span></span> <span data-ttu-id="1c7d3-257">İlk 3 satırların hello sonuçları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="1c7d3-257">Here are hello results for first 3 rows:</span></span>

|  | <span data-ttu-id="1c7d3-258">pickup_latitude</span><span class="sxs-lookup"><span data-stu-id="1c7d3-258">pickup_latitude</span></span> | <span data-ttu-id="1c7d3-259">pickup_longitude</span><span class="sxs-lookup"><span data-stu-id="1c7d3-259">pickup_longitude</span></span> | <span data-ttu-id="1c7d3-260">dropoff_latitude</span><span class="sxs-lookup"><span data-stu-id="1c7d3-260">dropoff_latitude</span></span> | <span data-ttu-id="1c7d3-261">dropoff_longitude</span><span class="sxs-lookup"><span data-stu-id="1c7d3-261">dropoff_longitude</span></span> | <span data-ttu-id="1c7d3-262">DirectDistance</span><span class="sxs-lookup"><span data-stu-id="1c7d3-262">DirectDistance</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="1c7d3-263">1</span><span class="sxs-lookup"><span data-stu-id="1c7d3-263">1</span></span> |<span data-ttu-id="1c7d3-264">40.731804</span><span class="sxs-lookup"><span data-stu-id="1c7d3-264">40.731804</span></span> |<span data-ttu-id="1c7d3-265">-74.001083</span><span class="sxs-lookup"><span data-stu-id="1c7d3-265">-74.001083</span></span> |<span data-ttu-id="1c7d3-266">40.736622</span><span class="sxs-lookup"><span data-stu-id="1c7d3-266">40.736622</span></span> |<span data-ttu-id="1c7d3-267">-73.988953</span><span class="sxs-lookup"><span data-stu-id="1c7d3-267">-73.988953</span></span> |<span data-ttu-id="1c7d3-268">.7169601222</span><span class="sxs-lookup"><span data-stu-id="1c7d3-268">.7169601222</span></span> |
| <span data-ttu-id="1c7d3-269">2</span><span class="sxs-lookup"><span data-stu-id="1c7d3-269">2</span></span> |<span data-ttu-id="1c7d3-270">40.715794</span><span class="sxs-lookup"><span data-stu-id="1c7d3-270">40.715794</span></span> |<span data-ttu-id="1c7d3-271">-74,010635</span><span class="sxs-lookup"><span data-stu-id="1c7d3-271">-74,010635</span></span> |<span data-ttu-id="1c7d3-272">40.725338</span><span class="sxs-lookup"><span data-stu-id="1c7d3-272">40.725338</span></span> |<span data-ttu-id="1c7d3-273">-74.00399</span><span class="sxs-lookup"><span data-stu-id="1c7d3-273">-74.00399</span></span> |<span data-ttu-id="1c7d3-274">.7448343721</span><span class="sxs-lookup"><span data-stu-id="1c7d3-274">.7448343721</span></span> |
| <span data-ttu-id="1c7d3-275">3</span><span class="sxs-lookup"><span data-stu-id="1c7d3-275">3</span></span> |<span data-ttu-id="1c7d3-276">40.761456</span><span class="sxs-lookup"><span data-stu-id="1c7d3-276">40.761456</span></span> |<span data-ttu-id="1c7d3-277">-73.999886</span><span class="sxs-lookup"><span data-stu-id="1c7d3-277">-73.999886</span></span> |<span data-ttu-id="1c7d3-278">40.766544</span><span class="sxs-lookup"><span data-stu-id="1c7d3-278">40.766544</span></span> |<span data-ttu-id="1c7d3-279">-73.988228</span><span class="sxs-lookup"><span data-stu-id="1c7d3-279">-73.988228</span></span> |<span data-ttu-id="1c7d3-280">0.7037227967</span><span class="sxs-lookup"><span data-stu-id="1c7d3-280">0.7037227967</span></span> |

### <a name="prepare-data-for-model-building"></a><span data-ttu-id="1c7d3-281">Model oluşturmanın için verileri hazırlama</span><span class="sxs-lookup"><span data-stu-id="1c7d3-281">Prepare data for model building</span></span>
<span data-ttu-id="1c7d3-282">Merhaba aşağıdaki birleşimler hello sorgu **nyctaxi\_seyahat** ve **nyctaxi\_ücreti** tabloları, ikili sınıflandırma etiketini oluşturur **Eğimli**, birden çok sınıf sınıflandırma etiketini **İpucu\_sınıfı**ve bir örnek hello tam birleştirilmiş kümesinden ayıklar.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-282">hello following query joins hello **nyctaxi\_trip** and **nyctaxi\_fare** tables, generates a binary classification label **tipped**, a multi-class classification label **tip\_class**, and extracts a sample from hello full joined dataset.</span></span> <span data-ttu-id="1c7d3-283">Merhaba örnekleme hello dönüşleri toplama zamana dayalı bir kısmı alarak yapılır.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-283">hello sampling is done by retrieving a subset of hello trips based on pickup time.</span></span>  <span data-ttu-id="1c7d3-284">Bu sorgu kopyalanır, ardından doğrudan hello yapıştırılan [Azure Machine Learning Studio](https://studio.azureml.net) [veri içeri aktarma] [ import-data] hello SQL veritabanı örneğinden doğrudan veri alımı için Modülü Azure'da.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-284">This query can be copied then pasted directly in hello [Azure Machine Learning Studio](https://studio.azureml.net) [Import Data][import-data] module for direct data ingestion from hello SQL database instance in Azure.</span></span> <span data-ttu-id="1c7d3-285">Merhaba sorgu dışlar yanlış kayıtlarıyla (0, 0) koordinatları.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-285">hello query excludes records with incorrect (0, 0) coordinates.</span></span>

    SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount,     f.total_amount, f.tip_amount,
        CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped,
        CASE WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM <schemaname>.<nyctaxi_trip> t, <schemaname>.<nyctaxi_fare> f
    WHERE datepart("mi",t.pickup_datetime) = 1
    AND   t.medallion = f.medallion
    AND   t.hack_license = f.hack_license
    AND   t.pickup_datetime = f.pickup_datetime
    AND   pickup_longitude != '0' AND dropoff_longitude != '0'

<span data-ttu-id="1c7d3-286">Hazır tooproceed tooAzure Machine Learning olduğunda ya da görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="1c7d3-286">When you are ready tooproceed tooAzure Machine Learning, you may either:</span></span>  

1. <span data-ttu-id="1c7d3-287">Merhaba nihai SQL sorgu tooextract ve örnek hello veri ve kopyala-yapıştır hello sorguyu doğrudan kaydetmek bir [veri içeri aktarma] [ import-data] Azure Machine Learning modülünde veya</span><span class="sxs-lookup"><span data-stu-id="1c7d3-287">Save hello final SQL query tooextract and sample hello data and copy-paste hello query directly into a [Import Data][import-data] module in Azure Machine Learning, or</span></span>
2. <span data-ttu-id="1c7d3-288">Örneklenen hello kalıcı toouse içinde yeni bir SQL DW oluşturma modeli için planlama tasarlanan veri tablo hello yeni tablo hello kullanılacağını ve [veri içeri aktarma] [ import-data] Azure Machine Learning modülünde.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-288">Persist hello sampled and engineered data you plan toouse for model building in a new SQL DW table and use hello new table in hello [Import Data][import-data] module in Azure Machine Learning.</span></span> <span data-ttu-id="1c7d3-289">Merhaba PowerShell Betiği önceki adımda bunu sizin için yapmıştır.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-289">hello PowerShell script in earlier step has done this for you.</span></span> <span data-ttu-id="1c7d3-290">Bu tabloda hello veri içeri aktarma modülü doğrudan okuyabilir.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-290">You can read directly from this table in hello Import Data module.</span></span>

## <span data-ttu-id="1c7d3-291"><a name="ipnb"></a>Veri keşfi ve özellik Mühendisliği IPython Not</span><span class="sxs-lookup"><span data-stu-id="1c7d3-291"><a name="ipnb"></a>Data exploration and feature engineering in IPython notebook</span></span>
<span data-ttu-id="1c7d3-292">Bu bölümde, veri keşfi ve her iki Python kullanarak özellik oluşturma gerçekleştiririz ve hello SQL DW SQL sorguları daha önce oluşturduğunuz.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-292">In this section, we will perform data exploration and feature generation using both Python and SQL queries against hello SQL DW created earlier.</span></span> <span data-ttu-id="1c7d3-293">Adlandırılmış bir örnek IPython not defteri **SQLDW_Explorations.ipynb** ve Python komut dosyası **SQLDW_Explorations_Scripts.py** indirilen tooyour yerel dizin olmuştur.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-293">A sample IPython notebook named **SQLDW_Explorations.ipynb** and a Python script file **SQLDW_Explorations_Scripts.py** have been downloaded tooyour local directory.</span></span> <span data-ttu-id="1c7d3-294">Ayrıca üzerinde kullanılabilir [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/SQLDW).</span><span class="sxs-lookup"><span data-stu-id="1c7d3-294">They are also available on [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/SQLDW).</span></span> <span data-ttu-id="1c7d3-295">Bu iki dosyayı Python komut dosyalarında aynıdır.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-295">These two files are identical in Python scripts.</span></span> <span data-ttu-id="1c7d3-296">bir IPython dizüstü sunucusu olmayan olasılığına hello Python komut dosyası tooyou sağlanır.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-296">hello Python script file is provided tooyou in case you do not have an IPython Notebook server.</span></span> <span data-ttu-id="1c7d3-297">Bu iki örnek dosyaları altında tasarlanmıştır Python **Python 2.7**.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-297">These two sample Python files are designed under **Python 2.7**.</span></span>

<span data-ttu-id="1c7d3-298">Merhaba örnek IPython dizüstü gerekli Azure SQL DW bilgileri hello ve Python komut dosyası indirilen tooyour yerel makine hello PowerShell betiği tarafından daha önce takıldığını hello.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-298">hello needed Azure SQL DW information in hello sample IPython Notebook and hello Python script file downloaded tooyour local machine has been plugged in by hello PowerShell script previously.</span></span> <span data-ttu-id="1c7d3-299">Bunlar herhangi bir değişiklik yapılmadan çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-299">They are executable without any modification.</span></span>

<span data-ttu-id="1c7d3-300">Bir AzureML çalışma alanı zaten ayarladıysanız, doğrudan hello örnek IPython dizüstü toohello AzureML IPython Not Defteri hizmetini yükleyin ve çalışan başlatın.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-300">If you have already set up an AzureML workspace, you can directly upload hello sample IPython Notebook toohello AzureML IPython Notebook service and start running it.</span></span> <span data-ttu-id="1c7d3-301">Merhaba adımları tooupload tooAzureML IPython dizüstü hizmet şunlardır:</span><span class="sxs-lookup"><span data-stu-id="1c7d3-301">Here are hello steps tooupload tooAzureML IPython Notebook service:</span></span>

1. <span data-ttu-id="1c7d3-302">Tooyour AzureML çalışma alanında oturum, hello üstünde "Studio'nun"'i tıklatın ve hello web sayfasının sol tarafında hello "dizüstü bilgisayarlar"'i tıklatın.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-302">Log in tooyour AzureML workspace, click "Studio" at hello top, and click "NOTEBOOKS" on hello left side of hello web page.</span></span>
   
    ![#22 Çiz][22]
2. <span data-ttu-id="1c7d3-304">"Yeni" Merhaba sol alt köşesindeki hello web sayfası'ni tıklatın ve seçin "Python 2".</span><span class="sxs-lookup"><span data-stu-id="1c7d3-304">Click "NEW" on hello left bottom corner of hello web page, and select "Python 2".</span></span> <span data-ttu-id="1c7d3-305">Ardından, bir ad toohello not defteri sağlayın ve hello onay işareti toocreate hello yeni boş IPython dizüstü bilgisayar'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-305">Then, provide a name toohello notebook and click hello check mark toocreate hello new blank IPython Notebook.</span></span>
   
    ![#23 Çiz][23]
3. <span data-ttu-id="1c7d3-307">Merhaba sol üst köşesindeki hello Hello "Jupyter" simgesine tıklayın yeni IPython not defteri.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-307">Click hello "Jupyter" symbol on hello left top corner of hello new IPython Notebook.</span></span>
   
    ![#24 Çiz][24]
4. <span data-ttu-id="1c7d3-309">Sürükleme ve bırakma hello örnek IPython dizüstü toohello **ağaç** sayfasında AzureML IPython dizüstü hizmet ve tıklatın **karşıya**.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-309">Drag and drop hello sample IPython Notebook toohello **tree** page of your AzureML IPython Notebook service, and click **Upload**.</span></span> <span data-ttu-id="1c7d3-310">Ardından, hello örnek IPython dizüstü karşıya yüklenen toohello AzureML IPython dizüstü hizmet olacaktır.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-310">Then, hello sample IPython Notebook will be uploaded toohello AzureML IPython Notebook service.</span></span>
   
    ![#25 Çiz][25]

<span data-ttu-id="1c7d3-312">Sipariş toorun hello IPython Not örnek veya Python komut dosyası Merhaba, hello aşağıdaki Python paketlerini gereklidir.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-312">In order toorun hello sample IPython Notebook or hello Python script file, hello following Python packages are needed.</span></span> <span data-ttu-id="1c7d3-313">Merhaba AzureML IPython dizüstü hizmeti kullanıyorsanız, bu paketleri önceden yüklendi.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-313">If you are using hello AzureML IPython Notebook service, these packages have been pre-installed.</span></span>

    - <span data-ttu-id="1c7d3-314">pandas</span><span class="sxs-lookup"><span data-stu-id="1c7d3-314">pandas</span></span>
    - <span data-ttu-id="1c7d3-315">numpy</span><span class="sxs-lookup"><span data-stu-id="1c7d3-315">numpy</span></span>
    - <span data-ttu-id="1c7d3-316">matplotlib</span><span class="sxs-lookup"><span data-stu-id="1c7d3-316">matplotlib</span></span>
    - <span data-ttu-id="1c7d3-317">pyodbc</span><span class="sxs-lookup"><span data-stu-id="1c7d3-317">pyodbc</span></span>
    - <span data-ttu-id="1c7d3-318">PyTables</span><span class="sxs-lookup"><span data-stu-id="1c7d3-318">PyTables</span></span>

<span data-ttu-id="1c7d3-319">Gelişmiş analitik çözümler ile büyük veri üzerinde AzureML oluştururken dizisi önerilen hello hello aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="1c7d3-319">hello recommended sequence when building advanced analytical solutions on AzureML with large data is hello following:</span></span>

* <span data-ttu-id="1c7d3-320">Merhaba veri küçük bir örnek, bir bellek içi veri çerçeveye okuyun.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-320">Read in a small sample of hello data into an in-memory data frame.</span></span>
* <span data-ttu-id="1c7d3-321">Bazı Görselleştirme ve explorations hello örneklenen verileri kullanarak gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-321">Perform some visualizations and explorations using hello sampled data.</span></span>
* <span data-ttu-id="1c7d3-322">Merhaba örneklenen verileri kullanarak özellik Mühendisliği ile deneyin.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-322">Experiment with feature engineering using hello sampled data.</span></span>
* <span data-ttu-id="1c7d3-323">Büyük veri keşfi, veri işleme ve özellik Mühendisliği, Python tooissue SQL sorguları doğrudan hello SQL DW kullanın.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-323">For larger data exploration, data manipulation and feature engineering, use Python tooissue SQL Queries directly against hello SQL DW.</span></span>
* <span data-ttu-id="1c7d3-324">Merhaba örnek boyutu toobe Azure Machine Learning modeli oluşturma için uygun karar verin.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-324">Decide hello sample size toobe suitable for Azure Machine Learning model building.</span></span>

<span data-ttu-id="1c7d3-325">Merhaba aşağıdakilere birkaç veri keşfi, veri Görselleştirme ve özellik Mühendisliği örnekleri ' dir.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-325">hello followings are a few data exploration, data visualization, and feature engineering examples.</span></span> <span data-ttu-id="1c7d3-326">Daha fazla veri explorations hello örnek IPython not defteri ve hello örnek Python komut dosyası bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-326">More data explorations can be found in hello sample IPython Notebook and hello sample Python script file.</span></span>

### <a name="initialize-database-credentials"></a><span data-ttu-id="1c7d3-327">Veritabanı kimlik bilgileri başlatma</span><span class="sxs-lookup"><span data-stu-id="1c7d3-327">Initialize database credentials</span></span>
<span data-ttu-id="1c7d3-328">Veritabanı bağlantı ayarlarınızda değişkenleri aşağıdaki hello başlatın:</span><span class="sxs-lookup"><span data-stu-id="1c7d3-328">Initialize your database connection settings in hello following variables:</span></span>

    SERVER_NAME=<server name>
    DATABASE_NAME=<database name>
    USERID=<user name>
    PASSWORD=<password>
    DB_DRIVER = <database driver>

### <a name="create-database-connection"></a><span data-ttu-id="1c7d3-329">Veritabanı bağlantısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="1c7d3-329">Create database connection</span></span>
<span data-ttu-id="1c7d3-330">Merhaba bağlantı toohello veritabanı oluşturur hello bağlantı dizesi değil.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-330">Here is hello connection string that creates hello connection toohello database.</span></span>

    CONNECTION_STRING = 'DRIVER={'+DRIVER+'};SERVER='+SERVER_NAME+';DATABASE='+DATABASE_NAME+';UID='+USERID+';PWD='+PASSWORD
    conn = pyodbc.connect(CONNECTION_STRING)

### <a name="report-number-of-rows-and-columns-in-table-nyctaxitrip"></a><span data-ttu-id="1c7d3-331">Satırları ve sütunları < nyctaxi_trip > tablosundaki rapor sayısı</span><span class="sxs-lookup"><span data-stu-id="1c7d3-331">Report number of rows and columns in table <nyctaxi_trip></span></span>
    nrows = pd.read_sql('''
        SELECT SUM(rows) FROM sys.partitions
        WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_trip>')
    ''', conn)

    print 'Total number of rows = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''
        SELECT COUNT(*) FROM information_schema.columns
        WHERE table_name = ('<nyctaxi_trip>') AND table_schema = ('<schemaname>')
    ''', conn)

    print 'Total number of columns = %d' % ncols.iloc[0,0]

* <span data-ttu-id="1c7d3-332">Toplam satır sayısı 173179759 =</span><span class="sxs-lookup"><span data-stu-id="1c7d3-332">Total number of rows = 173179759</span></span>  
* <span data-ttu-id="1c7d3-333">Toplam sütun sayısı = 14</span><span class="sxs-lookup"><span data-stu-id="1c7d3-333">Total number of columns = 14</span></span>

### <a name="report-number-of-rows-and-columns-in-table-nyctaxifare"></a><span data-ttu-id="1c7d3-334">Satırları ve sütunları < nyctaxi_fare > tablosundaki rapor sayısı</span><span class="sxs-lookup"><span data-stu-id="1c7d3-334">Report number of rows and columns in table <nyctaxi_fare></span></span>
    nrows = pd.read_sql('''
        SELECT SUM(rows) FROM sys.partitions
        WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_fare>')
    ''', conn)

    print 'Total number of rows = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''
        SELECT COUNT(*) FROM information_schema.columns
        WHERE table_name = ('<nyctaxi_fare>') AND table_schema = ('<schemaname>')
    ''', conn)

    print 'Total number of columns = %d' % ncols.iloc[0,0]

* <span data-ttu-id="1c7d3-335">Toplam satır sayısı 173179759 =</span><span class="sxs-lookup"><span data-stu-id="1c7d3-335">Total number of rows = 173179759</span></span>  
* <span data-ttu-id="1c7d3-336">Toplam sütun sayısı = 11</span><span class="sxs-lookup"><span data-stu-id="1c7d3-336">Total number of columns = 11</span></span>

### <a name="read-in-a-small-data-sample-from-hello-sql-data-warehouse-database"></a><span data-ttu-id="1c7d3-337">Okuma bileşenini hello SQL veri ambarı veritabanı küçük veri örnekten</span><span class="sxs-lookup"><span data-stu-id="1c7d3-337">Read-in a small data sample from hello SQL Data Warehouse Database</span></span>
    t0 = time.time()

    query = '''
        SELECT TOP 10000 t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax,
            f.tolls_amount, f.total_amount, f.tip_amount
        FROM <schemaname>.<nyctaxi_trip> t, <schemaname>.<nyctaxi_fare> f
        WHERE datepart("mi",t.pickup_datetime) = 1
        AND   t.medallion = f.medallion
        AND   t.hack_license = f.hack_license
        AND   t.pickup_datetime = f.pickup_datetime
    '''

    df1 = pd.read_sql(query, conn)

    t1 = time.time()
    print 'Time tooread hello sample table is %f seconds' % (t1-t0)

    print 'Number of rows and columns retrieved = (%d, %d)' % (df1.shape[0], df1.shape[1])

<span data-ttu-id="1c7d3-338">Zaman tooread hello örnek Tablo 14.096495 saniyedir.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-338">Time tooread hello sample table is 14.096495 seconds.</span></span>  
<span data-ttu-id="1c7d3-339">Satır ve sütunların sayısı, alınan = (1000 21).</span><span class="sxs-lookup"><span data-stu-id="1c7d3-339">Number of rows and columns retrieved = (1000, 21).</span></span>

### <a name="descriptive-statistics"></a><span data-ttu-id="1c7d3-340">Açıklayıcı istatistikleri</span><span class="sxs-lookup"><span data-stu-id="1c7d3-340">Descriptive statistics</span></span>
<span data-ttu-id="1c7d3-341">Hazır tooexplore örneklenen hello veri sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-341">Now you are ready tooexplore hello sampled data.</span></span> <span data-ttu-id="1c7d3-342">Bazı tanımlayıcı istatistik hello için bakarak ile başlangıç **seyahat\_uzaklığı** (veya diğer alanlar toospecify seçin).</span><span class="sxs-lookup"><span data-stu-id="1c7d3-342">We start with looking at some descriptive statistics for hello **trip\_distance** (or any other fields you choose toospecify).</span></span>

    df1['trip_distance'].describe()

### <a name="visualization-box-plot-example"></a><span data-ttu-id="1c7d3-343">Görselleştirme: Kutusu çizim örneği</span><span class="sxs-lookup"><span data-stu-id="1c7d3-343">Visualization: Box plot example</span></span>
<span data-ttu-id="1c7d3-344">Sonraki hello Kutu Çizimi hello seyahat uzaklığı toovisualize hello quantiles için ele.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-344">Next we look at hello box plot for hello trip distance toovisualize hello quantiles.</span></span>

    df1.boxplot(column='trip_distance',return_type='dict')

![#1 Çiz][1]

### <a name="visualization-distribution-plot-example"></a><span data-ttu-id="1c7d3-346">Görselleştirme: Dağıtım çizim örneği</span><span class="sxs-lookup"><span data-stu-id="1c7d3-346">Visualization: Distribution plot example</span></span>
<span data-ttu-id="1c7d3-347">Merhaba dağıtım ve hello için bir histogram görselleştirmek çizimleri seyahat uzaklıklar örneklenen.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-347">Plots that visualize hello distribution and a histogram for hello sampled trip distances.</span></span>

    fig = plt.figure()
    ax1 = fig.add_subplot(1,2,1)
    ax2 = fig.add_subplot(1,2,2)
    df1['trip_distance'].plot(ax=ax1,kind='kde', style='b-')
    df1['trip_distance'].hist(ax=ax2, bins=100, color='k')

![#2 Çiz][2]

### <a name="visualization-bar-and-line-plots"></a><span data-ttu-id="1c7d3-349">Görselleştirme: Çubuk ve çizgi çizer</span><span class="sxs-lookup"><span data-stu-id="1c7d3-349">Visualization: Bar and line plots</span></span>
<span data-ttu-id="1c7d3-350">Bu örnekte, beş depo içine hello seyahat uzaklığı bin ve sonuçları binning hello görselleştirin.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-350">In this example, we bin hello trip distance into five bins and visualize hello binning results.</span></span>

    trip_dist_bins = [0, 1, 2, 4, 10, 1000]
    df1['trip_distance']
    trip_dist_bin_id = pd.cut(df1['trip_distance'], trip_dist_bins)
    trip_dist_bin_id

<span data-ttu-id="1c7d3-351">Depo dağıtım çubuğundaki yukarıda hello çizmek veya çizim ile satır:</span><span class="sxs-lookup"><span data-stu-id="1c7d3-351">We can plot hello above bin distribution in a bar or line plot with:</span></span>

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='bar')

![#3 Çiz][3]

<span data-ttu-id="1c7d3-353">ve</span><span class="sxs-lookup"><span data-stu-id="1c7d3-353">and</span></span>

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='line')

![#4 Çiz][4]

### <a name="visualization-scatterplot-examples"></a><span data-ttu-id="1c7d3-355">Görselleştirme: Scatterplot örnekleri</span><span class="sxs-lookup"><span data-stu-id="1c7d3-355">Visualization: Scatterplot examples</span></span>
<span data-ttu-id="1c7d3-356">Dağılım çizim arasında gösteriyoruz **seyahat\_zaman\_içinde\_saniye** ve **seyahat\_uzaklığı** herhangi bağıntı ise toosee</span><span class="sxs-lookup"><span data-stu-id="1c7d3-356">We show scatter plot between **trip\_time\_in\_secs** and **trip\_distance** toosee if there is any correlation</span></span>

    plt.scatter(df1['trip_time_in_secs'], df1['trip_distance'])

![#6 Çiz][6]

<span data-ttu-id="1c7d3-358">Benzer şekilde biz hello ilişkisi denetleyebilirsiniz **oranı\_kod** ve **seyahat\_uzaklığı**.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-358">Similarly we can check hello relationship between **rate\_code** and **trip\_distance**.</span></span>

    plt.scatter(df1['passenger_count'], df1['trip_distance'])

![#8 Çiz][8]

### <a name="data-exploration-on-sampled-data-using-sql-queries-in-ipython-notebook"></a><span data-ttu-id="1c7d3-360">Veri keşfi IPython not defterinde SQL sorgularını kullanarak örneklenen verileri</span><span class="sxs-lookup"><span data-stu-id="1c7d3-360">Data exploration on sampled data using SQL queries in IPython notebook</span></span>
<span data-ttu-id="1c7d3-361">Bu bölümde, yukarıda oluşturduğumuz hello yeni tabloda kalıcı hello örneklenen verileri kullanarak veri dağıtımları keşfedin.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-361">In this section, we explore data distributions using hello sampled data which is persisted in hello new table we created above.</span></span> <span data-ttu-id="1c7d3-362">Not benzer explorations hello özgün tabloları kullanılarak gerçekleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-362">Note that similar explorations can be performed using hello original tables.</span></span>

#### <a name="exploration-report-number-of-rows-and-columns-in-hello-sampled-table"></a><span data-ttu-id="1c7d3-363">Keşfetme: Rapor sayısı hello sayfasındaki satır ve sütunları tablo örneklenen</span><span class="sxs-lookup"><span data-stu-id="1c7d3-363">Exploration: Report number of rows and columns in hello sampled table</span></span>
    nrows = pd.read_sql('''SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_sample>')''', conn)
    print 'Number of rows in sample = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''SELECT count(*) FROM information_schema.columns WHERE table_name = ('<nyctaxi_sample>') AND table_schema = '<schemaname>'''', conn)
    print 'Number of columns in sample = %d' % ncols.iloc[0,0]

#### <a name="exploration-tippednot-tripped-distribution"></a><span data-ttu-id="1c7d3-364">Keşfetme: Eğimli olmayan dağıtım dönüş</span><span class="sxs-lookup"><span data-stu-id="1c7d3-364">Exploration: Tipped/not tripped Distribution</span></span>
    query = '''
        SELECT tipped, count(*) AS tip_freq
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY tipped
        '''

    pd.read_sql(query, conn)

#### <a name="exploration-tip-class-distribution"></a><span data-ttu-id="1c7d3-365">Keşfetme: İpucu sınıfı dağıtım</span><span class="sxs-lookup"><span data-stu-id="1c7d3-365">Exploration: Tip class distribution</span></span>
    query = '''
        SELECT tip_class, count(*) AS tip_freq
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY tip_class
    '''

    tip_class_dist = pd.read_sql(query, conn)

#### <a name="exploration-plot-hello-tip-distribution-by-class"></a><span data-ttu-id="1c7d3-366">Araştırması: sınıfı tarafından hello ipucu dağıtım çizim</span><span class="sxs-lookup"><span data-stu-id="1c7d3-366">Exploration: Plot hello tip distribution by class</span></span>
    tip_class_dist['tip_freq'].plot(kind='bar')

![#26 Çiz][26]

#### <a name="exploration-daily-distribution-of-trips"></a><span data-ttu-id="1c7d3-368">Araştırması: Dönüş günlük dağıtımını</span><span class="sxs-lookup"><span data-stu-id="1c7d3-368">Exploration: Daily distribution of trips</span></span>
    query = '''
        SELECT CONVERT(date, dropoff_datetime) AS date, COUNT(*) AS c
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY CONVERT(date, dropoff_datetime)
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-per-medallion"></a><span data-ttu-id="1c7d3-369">Keşfetme: medallion başına dağıtım seyahat</span><span class="sxs-lookup"><span data-stu-id="1c7d3-369">Exploration: Trip distribution per medallion</span></span>
    query = '''
        SELECT medallion,count(*) AS c
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY medallion
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-by-medallion-and-hack-license"></a><span data-ttu-id="1c7d3-370">Keşfetme: dağıtım medallion ve korsan lisansla seyahat</span><span class="sxs-lookup"><span data-stu-id="1c7d3-370">Exploration: Trip distribution by medallion and hack license</span></span>
    query = '''select medallion, hack_license,count(*) from <schemaname>.<nyctaxi_sample> group by medallion, hack_license'''
    pd.read_sql(query,conn)


#### <a name="exploration-trip-time-distribution"></a><span data-ttu-id="1c7d3-371">Keşfetme: Seyahat süresi dağılımı</span><span class="sxs-lookup"><span data-stu-id="1c7d3-371">Exploration: Trip time distribution</span></span>
    query = '''select trip_time_in_secs, count(*) from <schemaname>.<nyctaxi_sample> group by trip_time_in_secs order by count(*) desc'''
    pd.read_sql(query,conn)

#### <a name="exploration-trip-distance-distribution"></a><span data-ttu-id="1c7d3-372">Keşfetme: Seyahat uzaklığı dağıtım</span><span class="sxs-lookup"><span data-stu-id="1c7d3-372">Exploration: Trip distance distribution</span></span>
    query = '''select floor(trip_distance/5)*5 as tripbin, count(*) from <schemaname>.<nyctaxi_sample> group by floor(trip_distance/5)*5 order by count(*) desc'''
    pd.read_sql(query,conn)

#### <a name="exploration-payment-type-distribution"></a><span data-ttu-id="1c7d3-373">Keşfetme: Ödeme türü dağıtımı</span><span class="sxs-lookup"><span data-stu-id="1c7d3-373">Exploration: Payment type distribution</span></span>
    query = '''select payment_type,count(*) from <schemaname>.<nyctaxi_sample> group by payment_type'''
    pd.read_sql(query,conn)

#### <a name="verify-hello-final-form-of-hello-featurized-table"></a><span data-ttu-id="1c7d3-374">Merhaba featurized tablosunun son form Hello doğrulayın</span><span class="sxs-lookup"><span data-stu-id="1c7d3-374">Verify hello final form of hello featurized table</span></span>
    query = '''SELECT TOP 100 * FROM <schemaname>.<nyctaxi_sample>'''
    pd.read_sql(query,conn)

## <span data-ttu-id="1c7d3-375"><a name="mlmodel"></a>Azure Machine Learning modellerini Derleme</span><span class="sxs-lookup"><span data-stu-id="1c7d3-375"><a name="mlmodel"></a>Build models in Azure Machine Learning</span></span>
<span data-ttu-id="1c7d3-376">Şimdi hazır tooproceed toomodel yapı ve model dağıtımda duyuyoruz [Azure Machine Learning](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="1c7d3-376">We are now ready tooproceed toomodel building and model deployment in [Azure Machine Learning](https://studio.azureml.net).</span></span> <span data-ttu-id="1c7d3-377">Merhaba, daha önce yani tanımlanan hello tahmin sorunları hiçbirinde kullanılan hazır toobe verilerdir:</span><span class="sxs-lookup"><span data-stu-id="1c7d3-377">hello data is ready toobe used in any of hello prediction problems identified earlier, namely:</span></span>

1. <span data-ttu-id="1c7d3-378">**İkili sınıflandırma**: olsun veya olmasın bir ipucu Ücretli bir seyahat için toopredict.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-378">**Binary classification**: toopredict whether or not a tip was paid for a trip.</span></span>
2. <span data-ttu-id="1c7d3-379">**Çok sınıflı sınıflandırma**: Ücretli, ipucu önceden tanımlanmış sınıfları toohello göre toopredict hello aralığı.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-379">**Multiclass classification**: toopredict hello range of tip paid, according toohello previously defined classes.</span></span>
3. <span data-ttu-id="1c7d3-380">**Regresyon görev**: seyahat için ödenen ucunun toopredict hello tutar.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-380">**Regression task**: toopredict hello amount of tip paid for a trip.</span></span>  

<span data-ttu-id="1c7d3-381">toobegin alıştırma modelleme Merhaba, tooyour içinde oturum **Azure Machine Learning** çalışma.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-381">toobegin hello modeling exercise, log in tooyour **Azure Machine Learning** workspace.</span></span> <span data-ttu-id="1c7d3-382">Machine learning çalışma alanı henüz oluşturmadıysanız, bkz: [Azure ML çalışma alanı oluşturma](machine-learning-create-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="1c7d3-382">If you have not yet created a machine learning workspace, see [Create an Azure ML workspace](machine-learning-create-workspace.md).</span></span>

1. <span data-ttu-id="1c7d3-383">Azure Machine Learning ile başlatılan tooget bakın [Azure Machine Learning Studio nedir?](machine-learning-what-is-ml-studio.md)</span><span class="sxs-lookup"><span data-stu-id="1c7d3-383">tooget started with Azure Machine Learning, see [What is Azure Machine Learning Studio?](machine-learning-what-is-ml-studio.md)</span></span>
2. <span data-ttu-id="1c7d3-384">Çok oturum[Azure Machine Learning Studio](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="1c7d3-384">Log in too[Azure Machine Learning Studio](https://studio.azureml.net).</span></span>
3. <span data-ttu-id="1c7d3-385">Merhaba Studio giriş sayfası bol miktarda bilgi, videoları, öğreticiler, bağlantılar toohello modülleri başvurusu ve diğer kaynakları sağlar.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-385">hello Studio Home page provides a wealth of information, videos, tutorials, links toohello Modules Reference, and other resources.</span></span> <span data-ttu-id="1c7d3-386">Azure Machine Learning hakkında daha fazla bilgi için hello başvurun [Azure Machine Learning Belge Merkezi](https://azure.microsoft.com/documentation/services/machine-learning/).</span><span class="sxs-lookup"><span data-stu-id="1c7d3-386">For more information about Azure Machine Learning, consult hello [Azure Machine Learning Documentation Center](https://azure.microsoft.com/documentation/services/machine-learning/).</span></span>

<span data-ttu-id="1c7d3-387">Tipik eğitim denemenizi Merhaba aşağıdaki adımları içerir:</span><span class="sxs-lookup"><span data-stu-id="1c7d3-387">A typical training experiment consists of hello following steps:</span></span>

1. <span data-ttu-id="1c7d3-388">Oluşturma bir **+ yeni** deneyin.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-388">Create a **+NEW** experiment.</span></span>
2. <span data-ttu-id="1c7d3-389">Merhaba verileri Azure ML alın.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-389">Get hello data into Azure ML.</span></span>
3. <span data-ttu-id="1c7d3-390">Önceden işler, dönüştürme ve gerektiği gibi hello veri arabirimidir.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-390">Pre-process, transform and manipulate hello data as needed.</span></span>
4. <span data-ttu-id="1c7d3-391">Özellikler gerektiği şekilde oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-391">Generate features as needed.</span></span>
5. <span data-ttu-id="1c7d3-392">Eğitim/doğrulama/test kümelerine Hello veri bölme (veya ayrı veri kümeleri her).</span><span class="sxs-lookup"><span data-stu-id="1c7d3-392">Split hello data into training/validation/testing datasets(or have separate datasets for each).</span></span>
6. <span data-ttu-id="1c7d3-393">Bir veya daha fazla makine öğrenimi algoritmaları sorun toosolve öğrenme hello bağlı olarak seçin.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-393">Select one or more machine learning algorithms depending on hello learning problem toosolve.</span></span> <span data-ttu-id="1c7d3-394">Örneğin, ikili Sınıflandırma, çok sınıflı Sınıflandırma, regresyon.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-394">E.g., binary classification, multiclass classification, regression.</span></span>
7. <span data-ttu-id="1c7d3-395">Merhaba eğitim veri kümesini kullanarak bir veya daha fazla modelleri eğitme.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-395">Train one or more models using hello training dataset.</span></span>
8. <span data-ttu-id="1c7d3-396">Merhaba, eğitilen modellerini kullanarak hello doğrulama dataset puan.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-396">Score hello validation dataset using hello trained model(s).</span></span>
9. <span data-ttu-id="1c7d3-397">Merhaba modellere toocompute hello ilgili ölçümlerini sorun öğrenme hello değerlendirin.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-397">Evaluate hello model(s) toocompute hello relevant metrics for hello learning problem.</span></span>
10. <span data-ttu-id="1c7d3-398">Merhaba modellerini ve select hello en iyi modeli toodeploy ince.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-398">Fine tune hello model(s) and select hello best model toodeploy.</span></span>

<span data-ttu-id="1c7d3-399">Bu alıştırmada, biz zaten incelediniz hello verileri SQL Data Warehouse mühendislik ve hello örnek boyutu tooingest Azure ML içinde karar.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-399">In this exercise, we have already explored and engineered hello data in SQL Data Warehouse, and decided on hello sample size tooingest in Azure ML.</span></span> <span data-ttu-id="1c7d3-400">Bir veya daha fazla hello tahmin modellerinin hello yordamı toobuild şöyledir:</span><span class="sxs-lookup"><span data-stu-id="1c7d3-400">Here is hello procedure toobuild one or more of hello prediction models:</span></span>

1. <span data-ttu-id="1c7d3-401">Azure hello kullanarak ML Hello Veri Al [veri içeri aktarma] [ import-data] modülü, hello kullanılabilir **veri giriş ve çıkış** bölümü.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-401">Get hello data into Azure ML using hello [Import Data][import-data] module, available in hello **Data Input and Output** section.</span></span> <span data-ttu-id="1c7d3-402">Merhaba daha fazla bilgi için bkz: [veri içeri aktarma] [ import-data] modül başvuru sayfası.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-402">For more information, see hello [Import Data][import-data] module reference page.</span></span>
   
    ![Verileri Azure ML İçeri Aktar][17]
2. <span data-ttu-id="1c7d3-404">Seçin **Azure SQL veritabanı** hello olarak **veri kaynağı** hello içinde **özellikleri** paneli.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-404">Select **Azure SQL Database** as hello **Data source** in hello **Properties** panel.</span></span>
3. <span data-ttu-id="1c7d3-405">Hello Hello veritabanı DNS adını girin **veritabanı sunucusu adı** alan.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-405">Enter hello database DNS name in hello **Database server name** field.</span></span> <span data-ttu-id="1c7d3-406">Biçimi:`tcp:<your_virtual_machine_DNS_name>,1433`</span><span class="sxs-lookup"><span data-stu-id="1c7d3-406">Format: `tcp:<your_virtual_machine_DNS_name>,1433`</span></span>
4. <span data-ttu-id="1c7d3-407">Merhaba girin **veritabanı adı** hello karşılık gelen alandaki.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-407">Enter hello **Database name** in hello corresponding field.</span></span>
5. <span data-ttu-id="1c7d3-408">Merhaba girin *SQL kullanıcı adı* hello içinde **Server kullanıcı hesabı adı**ve hello *parola* hello içinde **Server kullanıcı hesabı parolasını**.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-408">Enter hello *SQL user name* in hello **Server user account name**, and hello *password* in hello **Server user account password**.</span></span>
6. <span data-ttu-id="1c7d3-409">Merhaba denetleyin **herhangi bir sunucu sertifikayı kabul** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-409">Check hello **Accept any server certificate** option.</span></span>
7. <span data-ttu-id="1c7d3-410">Merhaba, **veritabanı sorgusu** metin alanı düzenleme, hello gerekli veritabanı (Merhaba etiketler gibi hesaplanan alanları dahil) alanları ve aşağı hangi ayıklar örnekleri hello veri istenen toohello örnek boyutu hello sorguyu yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-410">In hello **Database query** edit text area, paste hello query which extracts hello necessary database fields (including any computed fields such as hello labels) and down samples hello data toohello desired sample size.</span></span>

<span data-ttu-id="1c7d3-411">Verileri doğrudan hello SQL veri ambarı veritabanından okunurken bir ikili sınıflandırma deneme hello aşağıdaki çizimde örneğidir (tooreplace hello tablo içinde kullanılan adını ve hello tablo adları nyctaxi_trip ve nyctaxi_fare hello şeması tarafından adları unutmayın, izlenecek yol).</span><span class="sxs-lookup"><span data-stu-id="1c7d3-411">An example of a binary classification experiment reading data directly from hello SQL Data Warehouse database is in hello figure below (remember tooreplace hello table names nyctaxi_trip and nyctaxi_fare by hello schema name and hello table names you used in your walkthrough).</span></span> <span data-ttu-id="1c7d3-412">Benzer denemeler, çok sınıflı sınıflandırma ve regresyon sorunları için oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-412">Similar experiments can be constructed for multiclass classification and regression problems.</span></span>

![Azure ML eğitimi][10]

> [!IMPORTANT]
> <span data-ttu-id="1c7d3-414">Veri ayıklama modelleme ve önceki bölümlerde verilen sorgu örnekler örnekleme hello içinde **hello üç modelleme alıştırmaları için tüm etiketleri hello sorguya dahil**.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-414">In hello modeling data extraction and sampling query examples provided in previous sections, **all labels for hello three modeling exercises are included in hello query**.</span></span> <span data-ttu-id="1c7d3-415">Önemli bir (gerekli) her alıştırmaları modelleme hello çok adımdır**hariç** gereksiz etiketler Merhaba için iki diğer sorunlar ve diğer hello **hedef sızıntıları**.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-415">An important (required) step in each of hello modeling exercises is too**exclude** hello unnecessary labels for hello other two problems, and any other **target leaks**.</span></span> <span data-ttu-id="1c7d3-416">Örneğin, ikili Sınıflandırma, hello etiket kullanırken **Eğimli** ve hello alanları dışarıda **İpucu\_sınıfı**, **İpucu\_tutar**, ve **toplam\_tutar**.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-416">For example, when using binary classification, use hello label **tipped** and exclude hello fields **tip\_class**, **tip\_amount**, and **total\_amount**.</span></span> <span data-ttu-id="1c7d3-417">Merhaba ikinci hello ipucu kapsıyor beri hedef sızıntıları Ücretli.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-417">hello latter are target leaks since they imply hello tip paid.</span></span>
> 
> <span data-ttu-id="1c7d3-418">tooexclude tüm gereksiz sütunları ya da hedef sızıntıları hello kullanabilir [Select Columns in Dataset sütun] [ select-columns] modül veya hello [Düzenle meta veri] [ edit-metadata].</span><span class="sxs-lookup"><span data-stu-id="1c7d3-418">tooexclude any unnecessary columns or target leaks, you may use hello [Select Columns in Dataset][select-columns] module or hello [Edit Metadata][edit-metadata].</span></span> <span data-ttu-id="1c7d3-419">Daha fazla bilgi için bkz: [Select Columns in Dataset sütun] [ select-columns] ve [Düzenle meta veri] [ edit-metadata] başvuru sayfaları.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-419">For more information, see [Select Columns in Dataset][select-columns] and [Edit Metadata][edit-metadata] reference pages.</span></span>
> 
> 

## <span data-ttu-id="1c7d3-420"><a name="mldeploy"></a>Azure Machine Learning modellerini dağıtma</span><span class="sxs-lookup"><span data-stu-id="1c7d3-420"><a name="mldeploy"></a>Deploy models in Azure Machine Learning</span></span>
<span data-ttu-id="1c7d3-421">Modeliniz hazır olduğunda, kolayca onu hello deneme doğrudan bir web hizmeti olarak dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-421">When your model is ready, you can easily deploy it as a web service directly from hello experiment.</span></span> <span data-ttu-id="1c7d3-422">Azure ML web hizmetleri dağıtma hakkında daha fazla bilgi için bkz: [bir Azure Machine Learning web hizmetini dağıtma](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="1c7d3-422">For more information about deploying Azure ML web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

<span data-ttu-id="1c7d3-423">toodeploy yeni bir web hizmeti, şunları yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="1c7d3-423">toodeploy a new web service, you need to:</span></span>

1. <span data-ttu-id="1c7d3-424">Puanlama bir deneme oluşturma.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-424">Create a scoring experiment.</span></span>
2. <span data-ttu-id="1c7d3-425">Merhaba web hizmetini dağıtın.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-425">Deploy hello web service.</span></span>

<span data-ttu-id="1c7d3-426">bir Puanlama denemeler toocreate bir **tamamlandı** deneme eğitim, tıklatın **oluşturma PUANLAMA DENEMELER** hello alt eylem çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-426">toocreate a scoring experiment from a **Finished** training experiment, click **CREATE SCORING EXPERIMENT** in hello lower action bar.</span></span>

![Azure Puanlama][18]

<span data-ttu-id="1c7d3-428">Azure Machine Learning toocreate hello eğitim denemenizi hello bileşenlerini temel alan bir Puanlama deneme deneyecek.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-428">Azure Machine Learning will attempt toocreate a scoring experiment based on hello components of hello training experiment.</span></span> <span data-ttu-id="1c7d3-429">Özellikle, çıkarır:</span><span class="sxs-lookup"><span data-stu-id="1c7d3-429">In particular, it will:</span></span>

1. <span data-ttu-id="1c7d3-430">Merhaba, eğitilen model kaydetmek ve hello model eğitim modüllerini kaldırın.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-430">Save hello trained model and remove hello model training modules.</span></span>
2. <span data-ttu-id="1c7d3-431">Bir mantıksal tanımlamak **giriş bağlantı noktası** toorepresent hello giriş veri şeması bekleniyordu.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-431">Identify a logical **input port** toorepresent hello expected input data schema.</span></span>
3. <span data-ttu-id="1c7d3-432">Bir mantıksal tanımlamak **çıkış bağlantı noktasına** toorepresent hello beklenen web hizmeti çıkış şeması.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-432">Identify a logical **output port** toorepresent hello expected web service output schema.</span></span>

<span data-ttu-id="1c7d3-433">Deneme Puanlama hello oluşturulduğunda, gözden geçirin ve gerektiği gibi ayarlayın olun.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-433">When hello scoring experiment is created, review it and make adjust as needed.</span></span> <span data-ttu-id="1c7d3-434">Merhaba hizmeti çağrıldığında bunlar kullanılamaz tipik ayarlama tooreplace hello girdi veri kümesi ve/veya sorgu etiket alanları hariç biri ile aynıdır.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-434">A typical adjustment is tooreplace hello input dataset and/or query with one which excludes label fields, as these will not be available when hello service is called.</span></span> <span data-ttu-id="1c7d3-435">Ayrıca, hello iyi bir uygulama tooreduce hello boyutunu veri kümesi ve/veya sorgu tooa birkaç kayıtları, yeterli tooindicate hello giriş şemasını giriş unutulmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-435">It is also a good practice tooreduce hello size of hello input dataset and/or query tooa few records, just enough tooindicate hello input schema.</span></span> <span data-ttu-id="1c7d3-436">Merhaba çıkış bağlantı noktasına ilişkin tüm giriş alanları ortak tooexclude olduğundan ve yalnızca hello dahil **skoru etiketleri** ve **skoru olasılıklar** hello kullanarak çıktıyı hello içinde [veri kümesinde Sütun Seç ] [ select-columns] modülü.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-436">For hello output port, it is common tooexclude all input fields and only include hello **Scored Labels** and **Scored Probabilities** in hello output using hello [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="1c7d3-437">Bir örnek denemeyi Puanlama aşağıdaki hello şekilde sağlanır.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-437">A sample scoring experiment is provided in hello figure below.</span></span> <span data-ttu-id="1c7d3-438">Ne zaman toodeploy, hazır hello tıklatın **yayımlama WEB hizmeti** hello alt eylem çubuğunda düğmesi.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-438">When ready toodeploy, click hello **PUBLISH WEB SERVICE** button in hello lower action bar.</span></span>

![Azure ML yayımlama][11]

## <a name="summary"></a><span data-ttu-id="1c7d3-440">Özet</span><span class="sxs-lookup"><span data-stu-id="1c7d3-440">Summary</span></span>
<span data-ttu-id="1c7d3-441">toorecap ne biz yapılan bu gözden geçirme öğreticide, hello takım veri bilimi işlemi, veri alım toomodel eğitim, tüm hello şekilde aracılığıyla alma büyük ortak sahip bir veri kümesi, çalışan bir Azure veri bilimi ortam oluşturdunuz ve ardından bir Azure Machine Learning web hizmetini toohello dağıtımı.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-441">toorecap what we have done in this walkthrough tutorial, you have created an Azure data science environment, worked with a large public dataset, taking it through hello Team Data Science Process, all hello way from data acquisition toomodel training, and then toohello deployment of an Azure Machine Learning web service.</span></span>

### <a name="license-information"></a><span data-ttu-id="1c7d3-442">Lisans bilgileri</span><span class="sxs-lookup"><span data-stu-id="1c7d3-442">License information</span></span>
<span data-ttu-id="1c7d3-443">Bu örnek gözden geçirme ve kendi eşlik eden komut dosyaları ve IPython notebook(s) paylaşıldığı Microsoft tarafından hello MIT lisansı altında.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-443">This sample walkthrough and its accompanying scripts and IPython notebook(s) are shared by Microsoft under hello MIT license.</span></span> <span data-ttu-id="1c7d3-444">Lütfen hello LICENSE.txt dosyayı daha fazla ayrıntı için GitHub üzerindeki hello örnek kodu hello dizininde iade edin.</span><span class="sxs-lookup"><span data-stu-id="1c7d3-444">Please check hello LICENSE.txt file in in hello directory of hello sample code on GitHub for more details.</span></span>

## <a name="references"></a><span data-ttu-id="1c7d3-445">Başvurular</span><span class="sxs-lookup"><span data-stu-id="1c7d3-445">References</span></span>
<span data-ttu-id="1c7d3-446">• [Andrés Monroy NYC ücreti dönüşleri indirme sayfası](http://www.andresmh.com/nyctaxitrips/)</span><span class="sxs-lookup"><span data-stu-id="1c7d3-446">•    [Andrés Monroy NYC Taxi Trips Download Page](http://www.andresmh.com/nyctaxitrips/)</span></span>  
<span data-ttu-id="1c7d3-447">• [FOILing NYC ait ücreti seyahat veri Chris Whong tarafından](http://chriswhong.com/open-data/foil_nyc_taxi/) </span><span class="sxs-lookup"><span data-stu-id="1c7d3-447">•    [FOILing NYC’s Taxi Trip Data by Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span></span>  
<span data-ttu-id="1c7d3-448">• [NYC ücreti ve Limousine devreye sokmak araştırma ve istatistikleri](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span><span class="sxs-lookup"><span data-stu-id="1c7d3-448">•    [NYC Taxi and Limousine Commission Research and Statistics](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span></span>

[1]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_26_1.png
[2]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_28_1.png
[3]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_35_1.png
[4]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_36_1.png
[5]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_39_1.png
[6]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_42_1.png
[7]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_44_1.png
[8]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_46_1.png
[9]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_71_1.png
[10]: ./media/machine-learning-data-science-process-sqldw-walkthrough/azuremltrain.png
[11]: ./media/machine-learning-data-science-process-sqldw-walkthrough/azuremlpublish.png
[12]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ssmsconnect.png
[13]: ./media/machine-learning-data-science-process-sqldw-walkthrough/executescript.png
[14]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sqlserverproperties.png
[15]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sqldefaultdirs.png
[16]: ./media/machine-learning-data-science-process-sqldw-walkthrough/bulkimport.png
[17]: ./media/machine-learning-data-science-process-sqldw-walkthrough/amlreader.png
[18]: ./media/machine-learning-data-science-process-sqldw-walkthrough/amlscoring.png
[19]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ps_download_scripts.png
[20]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ps_load_data.png
[21]: ./media/machine-learning-data-science-process-sqldw-walkthrough/azcopy-overwrite.png
[22]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-1.png
[23]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-2.png
[24]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-3.png
[25]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-4.png
[26]: ./media/machine-learning-data-science-process-sqldw-walkthrough/tip_class_hist_1.png


<!-- Module References -->
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
