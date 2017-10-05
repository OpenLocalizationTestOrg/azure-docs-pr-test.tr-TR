---
title: "Power BI - Azure Hdınsight Apache Storm kullanın | Microsoft Docs"
description: "Hdınsight'ta bir Apache Storm kümesi üzerinde çalışan bir C# topolojisi gelen verileri kullanarak bir Power BI raporu oluşturun."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 36fe3b9c-5232-4464-8d75-95403b6da7a1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/31/2017
ms.author: larryfr
ms.openlocfilehash: 36487c0c34e5a4bb955bbc15c8c96b9e838aeb44
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-power-bi-to-visualize-data-from-an-apache-storm-topology"></a><span data-ttu-id="104d4-103">Apache Storm topolojisini verilerini görselleştirmek için Power BI kullanın</span><span class="sxs-lookup"><span data-stu-id="104d4-103">Use Power BI to visualize data from an Apache Storm topology</span></span>

<span data-ttu-id="104d4-104">Power BI, raporları gibi veri görsel olarak görüntülemenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="104d4-104">Power BI allows you to visually display data as reports.</span></span> <span data-ttu-id="104d4-105">Bu belge, Hdınsight üzerinde Apache Storm için Power BI veri oluşturmak nasıl bir örnek sağlar.</span><span class="sxs-lookup"><span data-stu-id="104d4-105">This document provides an example of how to use Apache Storm on HDInsight to generate data for Power BI.</span></span>

> [!NOTE]
> <span data-ttu-id="104d4-106">Bu belgede yer alan adımlar Visual Studio ile Windows geliştirme ortamına dayanır.</span><span class="sxs-lookup"><span data-stu-id="104d4-106">The steps in this document rely on a Windows development environment with Visual Studio.</span></span> <span data-ttu-id="104d4-107">Linux tabanlı Hdınsight kümesi için derlenmiş proje gönderilebilir.</span><span class="sxs-lookup"><span data-stu-id="104d4-107">The compiled project can be submitted to a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="104d4-108">Yalnızca Linux tabanlı kümelerde sonra 10/28/2016 desteği SCP.NET topolojileri oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="104d4-108">Only Linux-based clusters created after 10/28/2016 support SCP.NET topologies.</span></span>
>
> <span data-ttu-id="104d4-109">Bir C# topolojisi Linux tabanlı bir küme ile kullanmak için sürüm 0.10.0.6 için projeniz tarafından kullanılan ya da daha yüksek Microsoft.SCP.Net.SDK NuGet paketi güncelleştirme.</span><span class="sxs-lookup"><span data-stu-id="104d4-109">To use a C# topology with a Linux-based cluster, update the Microsoft.SCP.Net.SDK NuGet package used by your project to version 0.10.0.6 or higher.</span></span> <span data-ttu-id="104d4-110">Paketin sürümünün ayrıca HDInsight üzerinde yüklü olan Storm ana sürümüyle eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="104d4-110">The version of the package must also match the major version of Storm installed on HDInsight.</span></span> <span data-ttu-id="104d4-111">Örneğin, HDInsight sürüm 3.3 ve 3.4 üzerindeki Strom bileşenleri, Storm 0.10.x sürümünü kullanırken HDInsight 3.5 ile Storm 1.0.x kullanılır.</span><span class="sxs-lookup"><span data-stu-id="104d4-111">For example, Storm on HDInsight versions 3.3 and 3.4 use Storm version 0.10.x, while HDInsight 3.5 uses Storm 1.0.x.</span></span>
>
> <span data-ttu-id="104d4-112">Linux tabanlı kümelerdeki C# topolojilerinin .NET 4.5 kullanması ve HDInsight kümesi üzerinde çalışması için Mono kullanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="104d4-112">C# topologies on Linux-based clusters must use .NET 4.5, and use Mono to run on the HDInsight cluster.</span></span> <span data-ttu-id="104d4-113">Çoğu şeyler çalışır.</span><span class="sxs-lookup"><span data-stu-id="104d4-113">Most things work.</span></span> <span data-ttu-id="104d4-114">Ancak denetlemelisiniz [Mono Uyumluluk](http://www.mono-project.com/docs/about-mono/compatibility/) olası uyumsuzlukları belge.</span><span class="sxs-lookup"><span data-stu-id="104d4-114">However you should check the [Mono Compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) document for potential incompatibilities.</span></span>
>
> <span data-ttu-id="104d4-115">Windows tabanlı veya Linux tabanlı Hdınsight ile çalışır, bu proje için bir Java sürümü için bkz: [işlem Azure Event Hubs (Java) hdınsight'ta Storm olaylarından](hdinsight-storm-develop-java-event-hub-topology.md).</span><span class="sxs-lookup"><span data-stu-id="104d4-115">For a Java version of this project, which works with Linux-based or Windows-based HDInsight, see [Process events from Azure Event Hubs with Storm on HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="104d4-116">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="104d4-116">Prerequisites</span></span>

* <span data-ttu-id="104d4-117">Bir Azure Active Directory kullanıcı ile [Power BI](https://powerbi.com) erişim.</span><span class="sxs-lookup"><span data-stu-id="104d4-117">An Azure Active Directory user with [Power BI](https://powerbi.com) access.</span></span>
* <span data-ttu-id="104d4-118">Hdınsight kümesi.</span><span class="sxs-lookup"><span data-stu-id="104d4-118">An HDInsight cluster.</span></span> <span data-ttu-id="104d4-119">Daha fazla bilgi için bkz: [Hdınsight üzerinde Storm kullanmaya başlama](hdinsight-apache-storm-tutorial-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="104d4-119">For more information, see [Get started with Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="104d4-120">Linux, HDInsight sürüm 3.4 ve üzerinde kullanılan tek işletim sistemidir.</span><span class="sxs-lookup"><span data-stu-id="104d4-120">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="104d4-121">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="104d4-121">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="104d4-122">Visual Studio (aşağıdaki sürümlerinden biri)</span><span class="sxs-lookup"><span data-stu-id="104d4-122">Visual Studio (one of the following versions)</span></span>

  * <span data-ttu-id="104d4-123">Visual Studio 2012 ile [güncelleştirme 4](http://www.microsoft.com/download/details.aspx?id=39305)</span><span class="sxs-lookup"><span data-stu-id="104d4-123">Visual Studio 2012 with [update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span></span>
  * <span data-ttu-id="104d4-124">Visual Studio 2013 [güncelleştirme 4](http://www.microsoft.com/download/details.aspx?id=44921) veya [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?linkid=517284&clcid=0x409)</span><span class="sxs-lookup"><span data-stu-id="104d4-124">Visual Studio 2013 with [update 4](http://www.microsoft.com/download/details.aspx?id=44921) or [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?linkid=517284&clcid=0x409)</span></span>
  * [<span data-ttu-id="104d4-125">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="104d4-125">Visual Studio 2015</span></span>](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
  * <span data-ttu-id="104d4-126">Visual Studio 2017 (herhangi bir sürümünü)</span><span class="sxs-lookup"><span data-stu-id="104d4-126">Visual Studio 2017 (any edition)</span></span>

* <span data-ttu-id="104d4-127">Visual Studio için Hdınsight araçları: bkz [Visual Studio için Hdınsight araçları kullanarak çalışmaya başlama](hdinsight-hadoop-visual-studio-tools-get-started.md) yükleme bilgileri hakkında bilgi için.</span><span class="sxs-lookup"><span data-stu-id="104d4-127">The HDInsight Tools for Visual Studio: See [Get started using the HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) for information on installation information.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="104d4-128">Nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="104d4-128">How it works</span></span>

<span data-ttu-id="104d4-129">Bu örnek, rasgele Internet Information Services (IIS) günlük verileri oluşturur bir C# Storm topolojisinin içerir.</span><span class="sxs-lookup"><span data-stu-id="104d4-129">This example contains a C# Storm topology that randomly generates Internet Information Services (IIS) log data.</span></span> <span data-ttu-id="104d4-130">Bu veriler daha sonra bir SQL veritabanına yazılır ve buradan Power BI'da raporlar üretmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="104d4-130">This data is then written to a SQL Database, and from there it is used to generate reports in Power BI.</span></span>

<span data-ttu-id="104d4-131">Aşağıdaki dosyaları bu örnek ana işlevlerini uygular:</span><span class="sxs-lookup"><span data-stu-id="104d4-131">The following files implement the main functionality of this example:</span></span>

* <span data-ttu-id="104d4-132">**SqlAzureBolt.cs**: SQL veritabanı için Storm topolojisinde üretilen bilgilerini yazar.</span><span class="sxs-lookup"><span data-stu-id="104d4-132">**SqlAzureBolt.cs**: Writes information produced in the Storm topology to SQL Database.</span></span>
* <span data-ttu-id="104d4-133">**IISLogsTable.sql**: verileri depolanan veritabanı oluşturmak için kullanılan Transact-SQL deyimleri.</span><span class="sxs-lookup"><span data-stu-id="104d4-133">**IISLogsTable.sql**: The Transact-SQL statements used to generate the database that the data is stored in.</span></span>

> [!WARNING]
> <span data-ttu-id="104d4-134">Tablo, SQL veritabanında topoloji Hdınsight kümenize başlatmadan önce oluşturun.</span><span class="sxs-lookup"><span data-stu-id="104d4-134">Create the table in SQL Database before starting the topology on your HDInsight cluster.</span></span>

## <a name="download-the-example"></a><span data-ttu-id="104d4-135">Örnek indirme</span><span class="sxs-lookup"><span data-stu-id="104d4-135">Download the example</span></span>

<span data-ttu-id="104d4-136">Karşıdan [Hdınsight C# Storm Power BI örnek](https://github.com/Azure-Samples/hdinsight-dotnet-storm-powerbi).</span><span class="sxs-lookup"><span data-stu-id="104d4-136">Download the [HDInsight C# Storm Power BI example](https://github.com/Azure-Samples/hdinsight-dotnet-storm-powerbi).</span></span> <span data-ttu-id="104d4-137">İndirmek için ya da çatalı/kullanarak kopya [git](http://git-scm.com/), veya **karşıdan** arşivin bir .zip indirmek için bağlantı.</span><span class="sxs-lookup"><span data-stu-id="104d4-137">To download it, either fork/clone it using [git](http://git-scm.com/), or use the **Download** link to download a .zip of the archive.</span></span>

## <a name="create-a-database"></a><span data-ttu-id="104d4-138">Veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="104d4-138">Create a database</span></span>

1. <span data-ttu-id="104d4-139">Bir veritabanı oluşturmak için adımlarda kullanmak [SQL Database Öğreticisi](../sql-database/sql-database-get-started.md) belge.</span><span class="sxs-lookup"><span data-stu-id="104d4-139">To create a database, use the steps in the [SQL Database tutorial](../sql-database/sql-database-get-started.md) document.</span></span>

2. <span data-ttu-id="104d4-140">İçindeki adımları izleyerek veritabanına bağlan [Visual Studio ile SQL veritabanına bağlanma](../sql-database/sql-database-connect-query.md) belge.</span><span class="sxs-lookup"><span data-stu-id="104d4-140">Connect to the database by following the steps in the [Connect to a SQL Database with Visual Studio](../sql-database/sql-database-connect-query.md) document.</span></span>

3. <span data-ttu-id="104d4-141">Nesne Gezgini'nde veritabanını sağ tıklatın ve seçin **yeni sorgu**.</span><span class="sxs-lookup"><span data-stu-id="104d4-141">In Object Explorer, right-click the database and select  **New Query**.</span></span> <span data-ttu-id="104d4-142">İçeriğini Yapıştır **IISLogsTable.sql** dosya sorgu penceresine indirilen projeye dahil ve ardından sorguyu yürütmek için Ctrl + Shift + E kullanın.</span><span class="sxs-lookup"><span data-stu-id="104d4-142">Paste the contents of the **IISLogsTable.sql** file included in the downloaded project into the query window, and then use Ctrl + Shift + E to execute the query.</span></span> <span data-ttu-id="104d4-143">Komutların başarıyla tamamlandığını bir ileti alırsınız.</span><span class="sxs-lookup"><span data-stu-id="104d4-143">You should receive a message that the commands completed successfully.</span></span>

## <a name="configure-the-sample"></a><span data-ttu-id="104d4-144">Örnek yapılandırma</span><span class="sxs-lookup"><span data-stu-id="104d4-144">Configure the sample</span></span>

1. <span data-ttu-id="104d4-145">Gelen [Azure portal](https://portal.azure.com), SQL veritabanınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="104d4-145">From the [Azure portal](https://portal.azure.com), select your SQL database.</span></span> <span data-ttu-id="104d4-146">Gelen **Essentials** select SQL veritabanı dikey bölümünü **veritabanı bağlantı dizelerini Göster**.</span><span class="sxs-lookup"><span data-stu-id="104d4-146">From the **Essentials** section of the SQL database blade, select **Show database connection strings**.</span></span> <span data-ttu-id="104d4-147">Görüntülenen listesinden kopyalama **ADO.NET (SQL kimlik doğrulaması)** bilgi.</span><span class="sxs-lookup"><span data-stu-id="104d4-147">From the list that appears, copy the **ADO.NET (SQL authentication)** information.</span></span>

2. <span data-ttu-id="104d4-148">Örnek Visual Studio'da açın.</span><span class="sxs-lookup"><span data-stu-id="104d4-148">Open the sample in Visual Studio.</span></span> <span data-ttu-id="104d4-149">Gelen **Çözüm Gezgini**, açık **App.config** dosya ve şu girişi bulun:</span><span class="sxs-lookup"><span data-stu-id="104d4-149">From **Solution Explorer**, open the **App.config** file, and then find the following entry:</span></span>

        <add key="SqlAzureConnectionString" value="##TOBEFILLED##" />

    <span data-ttu-id="104d4-150">Değiştir **TOBEFILLED ##** veritabanı bağlantı dizesi değerle önceki adımda kopyaladığınız.</span><span class="sxs-lookup"><span data-stu-id="104d4-150">Replace the **##TOBEFILLED##** value with the database connection string copied in the previous step.</span></span> <span data-ttu-id="104d4-151">Değiştir **{,\_kullanıcı adı}** ve **{,\_parola}** kullanıcı adı ve parola veritabanı için.</span><span class="sxs-lookup"><span data-stu-id="104d4-151">Replace **{your\_username}** and **{your\_password}** with the username and password for the database.</span></span>

3. <span data-ttu-id="104d4-152">Kaydedin ve dosyaları kapatın.</span><span class="sxs-lookup"><span data-stu-id="104d4-152">Save and close the files.</span></span>

## <a name="deploy-the-sample"></a><span data-ttu-id="104d4-153">Örnek dağıtma</span><span class="sxs-lookup"><span data-stu-id="104d4-153">Deploy the sample</span></span>

1. <span data-ttu-id="104d4-154">Gelen **Çözüm Gezgini**, sağ **StormToSQL** proje ve seçin **Hdınsight üzerinde Storm Gönder**.</span><span class="sxs-lookup"><span data-stu-id="104d4-154">From **Solution Explorer**, right-click the **StormToSQL** project and select **Submit to Storm on HDInsight**.</span></span> <span data-ttu-id="104d4-155">Hdınsight küme seçin **Storm kümesi** iletişim kutusu açılır.</span><span class="sxs-lookup"><span data-stu-id="104d4-155">Select the HDInsight cluster from the **Storm Cluster** dropdown dialog.</span></span>

   > [!NOTE]
   > <span data-ttu-id="104d4-156">Bu işlem birkaç saniye sürebilir **Storm kümesi** sunucu adlarıyla doldurmak için açılır.</span><span class="sxs-lookup"><span data-stu-id="104d4-156">It may take a few seconds for the **Storm Cluster** dropdown to populate with server names.</span></span>
   >
   > <span data-ttu-id="104d4-157">İstenirse, Azure aboneliğiniz için oturum açma kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="104d4-157">If prompted, enter the login credentials for your Azure subscription.</span></span> <span data-ttu-id="104d4-158">Birden fazla aboneliğiniz varsa, Hdınsight kümesi üzerinde Storm'a içeren oturum açın.</span><span class="sxs-lookup"><span data-stu-id="104d4-158">If you have more than one subscription, log in to the one that contains your Storm on HDInsight cluster.</span></span>

2. <span data-ttu-id="104d4-159">Topoloji gönderildiğinde __topoloji Görüntüleyicisi__ görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="104d4-159">When the topology has been submitted, the __Topology Viewer__ appears.</span></span> <span data-ttu-id="104d4-160">Bu topoloji görüntülemek için listeden SqlAzureWriterTopology girişi seçin.</span><span class="sxs-lookup"><span data-stu-id="104d4-160">To view this topology, select the SqlAzureWriterTopology entry from the list.</span></span>

    ![Seçili topolojisi ile topolojileri](./media/hdinsight-storm-power-bi-topology/topologyview.png)

    <span data-ttu-id="104d4-162">Topolojisi hakkında bilgi için bu görünümü kullanın veya bir bileşen topolojisinde özgü bilgileri görmek için bir giriş (örneğin, SqlAzureBolt) çift tıklatın.</span><span class="sxs-lookup"><span data-stu-id="104d4-162">You can use this view to see information on the topology, or double-click an entry (such as the SqlAzureBolt) to see information specific to a component in the topology.</span></span>

3. <span data-ttu-id="104d4-163">Birkaç dakika, veritabanı oluşturmak için kullanılan SQL sorgu penceresine dönüş topolojisine sahip sonra verdi.</span><span class="sxs-lookup"><span data-stu-id="104d4-163">After the topology has ran for a few minutes, return to the SQL query window you used to create the database.</span></span> <span data-ttu-id="104d4-164">Varolan deyimleri aşağıdaki sorguyla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="104d4-164">Replace the existing statements with the following query:</span></span>

        select * from iislogs;

    <span data-ttu-id="104d4-165">Kullanım Ctrl + Shift + E sorgu ve çalıştırmak için aşağıdaki veri benzer sonuçlar almanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="104d4-165">Use Ctrl + Shift + E to execute the query, and you should receive results similar to the following data:</span></span>

        1    2016-05-27 17:57:14.797    255.255.255.255    /bar    GET    200
        2    2016-05-27 17:57:14.843    127.0.0.1    /spam/eggs    POST    500
        3    2016-05-27 17:57:14.850    123.123.123.123    /eggs    DELETE    200
        4    2016-05-27 17:57:14.853    127.0.0.1    /foo    POST    404
        5    2016-05-27 17:57:14.853    10.9.8.7    /bar    GET    200
        6    2016-05-27 17:57:14.857    192.168.1.1    /spam    DELETE    200

    <span data-ttu-id="104d4-166">Bu veri Storm topolojisini yazılmış.</span><span class="sxs-lookup"><span data-stu-id="104d4-166">This data has been written from the Storm topology.</span></span>

## <a name="create-a-report"></a><span data-ttu-id="104d4-167">Bir rapor oluşturun</span><span class="sxs-lookup"><span data-stu-id="104d4-167">Create a report</span></span>

1. <span data-ttu-id="104d4-168">Bağlanmak [Azure SQL Veritabanı Bağlayıcısı](https://app.powerbi.com/getdata/bigdata/azure-sql-database-with-live-connect) Power BI için.</span><span class="sxs-lookup"><span data-stu-id="104d4-168">Connect to the [Azure SQL Database connector](https://app.powerbi.com/getdata/bigdata/azure-sql-database-with-live-connect) for Power BI.</span></span> 

2. <span data-ttu-id="104d4-169">İçinde **veritabanları**seçin **almak**.</span><span class="sxs-lookup"><span data-stu-id="104d4-169">Within **Databases**, select **Get**.</span></span>

3. <span data-ttu-id="104d4-170">Seçin **Azure SQL veritabanı**ve ardından **Bağlan**.</span><span class="sxs-lookup"><span data-stu-id="104d4-170">Select **Azure SQL Database**, and then select **Connect**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="104d4-171">Devam etmek için Power BI Desktop'u indirin istenebilir.</span><span class="sxs-lookup"><span data-stu-id="104d4-171">You may be asked to download the Power BI Desktop to continue.</span></span> <span data-ttu-id="104d4-172">Bu durumda, bağlanmak için aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="104d4-172">If so, use the following steps to connect:</span></span>
    >
    > 1. <span data-ttu-id="104d4-173">Power BI Desktop açıp seçin __Veri Al__.</span><span class="sxs-lookup"><span data-stu-id="104d4-173">Open Power BI Desktop and select __Get Data__.</span></span>
    > <span data-ttu-id="104d4-174">2 seçin __Azure__ve ardından __Azure SQL veritabanı__.</span><span class="sxs-lookup"><span data-stu-id="104d4-174">2  Select __Azure__, and then __Azure SQL database__.</span></span>

4. <span data-ttu-id="104d4-175">Azure SQL veritabanınıza bağlanmak için gereken bilgileri girin.</span><span class="sxs-lookup"><span data-stu-id="104d4-175">Enter the information to connect to your Azure SQL Database.</span></span> <span data-ttu-id="104d4-176">Ziyaret ederek bu bilgiyi bulabilirsiniz [Azure portal](https://portal.azure.com) ve SQL veritabanınız seçme.</span><span class="sxs-lookup"><span data-stu-id="104d4-176">You can find this information by visiting the [Azure portal](https://portal.azure.com) and selecting your SQL database.</span></span>

   > [!NOTE]
   > <span data-ttu-id="104d4-177">Kullanarak yenileme aralığı ve özel filtreler de ayarlayabilirsiniz **Gelişmiş Seçenekler etkinleştirmek** Bağlan iletişim kutusundan.</span><span class="sxs-lookup"><span data-stu-id="104d4-177">You can also set the refresh interval and custom filters by using **Enable Advanced Options** from the connect dialog.</span></span>

5. <span data-ttu-id="104d4-178">Bağlı sonra bağlı veritabanı olarak aynı ada sahip yeni bir veri kümesi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="104d4-178">After you've connected, you will see a new dataset with the same name as the database you connected to.</span></span> <span data-ttu-id="104d4-179">Bir rapor tasarlamaya başlamak için veri kümesini seçin.</span><span class="sxs-lookup"><span data-stu-id="104d4-179">Select the dataset to begin designing a report.</span></span>

6. <span data-ttu-id="104d4-180">Gelen **alanları**, genişletin **IISLOGS** girişi.</span><span class="sxs-lookup"><span data-stu-id="104d4-180">From **Fields**, expand the **IISLOGS** entry.</span></span> <span data-ttu-id="104d4-181">URI gövdelerini listeleyen bir rapor oluşturmak için onay kutusunu seçin **bulunamadı.%N**.</span><span class="sxs-lookup"><span data-stu-id="104d4-181">To create a report that lists the URI stems, select the checkbox for **URISTEM**.</span></span>

    ![Rapor oluşturma](./media/hdinsight-storm-power-bi-topology/createreport.png)

7. <span data-ttu-id="104d4-183">Ardından, sürükleyin **yöntemi** rapor.</span><span class="sxs-lookup"><span data-stu-id="104d4-183">Next, drag **METHOD** to the report.</span></span> <span data-ttu-id="104d4-184">Gövdelerini ve HTTP isteği için kullanılan karşılık gelen HTTP yöntemini listelemek için rapor güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="104d4-184">The report updates to list the stems and the corresponding HTTP method used for the HTTP request.</span></span>

    ![yöntem veri ekleme](./media/hdinsight-storm-power-bi-topology/uristemandmethod.png)

8. <span data-ttu-id="104d4-186">Gelen **görselleştirmeleri** sütun seçin **alanları** simgesini ve sonra aşağı oka yanına seçin **yöntemi** içinde **değerleri** bölümü.</span><span class="sxs-lookup"><span data-stu-id="104d4-186">From the **Visualizations** column, select the **Fields** icon, and then select the down arrow next to **METHOD** in the **Values** section.</span></span> <span data-ttu-id="104d4-187">Bir URI erişilen kaç kez sayısını görüntülemek için seçin **sayısı**.</span><span class="sxs-lookup"><span data-stu-id="104d4-187">To display a count of how many times a URI has been accessed, select **Count**.</span></span>

    ![İçin yöntemleri sayısını değiştirme](./media/hdinsight-storm-power-bi-topology/count.png)

9. <span data-ttu-id="104d4-189">Ardından, **yığılmış sütun grafiği** bilgilerin nasıl görüntüleneceğini değiştirmek için.</span><span class="sxs-lookup"><span data-stu-id="104d4-189">Next, select the **Stacked column chart** to change how the information is displayed.</span></span>

    ![Yığılmış grafiğe değiştirme](./media/hdinsight-storm-power-bi-topology/stackedcolumn.png)

10. <span data-ttu-id="104d4-191">Raporu kaydetmek için seçin **kaydetmek** ve rapor için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="104d4-191">To save the report, select **Save** and enter a name for the report.</span></span>

## <a name="stop-the-topology"></a><span data-ttu-id="104d4-192">Topolojiyi durdurma</span><span class="sxs-lookup"><span data-stu-id="104d4-192">Stop the topology</span></span>

<span data-ttu-id="104d4-193">Topoloji, durdurmak veya Hdınsight kümesinde Storm silmek kadar çalışmaya devam eder.</span><span class="sxs-lookup"><span data-stu-id="104d4-193">The topology continues to run until you stop it or delete the Storm on HDInsight cluster.</span></span> <span data-ttu-id="104d4-194">Topoloji durdurmak için aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="104d4-194">To stop the topology, perform the following steps:</span></span>

1. <span data-ttu-id="104d4-195">Visual Studio'da topoloji görüntüleyiciye dönün ve topolojiyi seçin.</span><span class="sxs-lookup"><span data-stu-id="104d4-195">In Visual Studio, return to the topology viewer and select the topology.</span></span>

2. <span data-ttu-id="104d4-196">Seçin **KILL** topolojiyi durdurma düğmesi.</span><span class="sxs-lookup"><span data-stu-id="104d4-196">Select the **Kill** button to stop the topology.</span></span>

    ![Özet topoloji düğmesini KILL](./media/hdinsight-storm-power-bi-topology/killtopology.png)

## <a name="delete-your-cluster"></a><span data-ttu-id="104d4-198">Kümenizi Sil</span><span class="sxs-lookup"><span data-stu-id="104d4-198">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="104d4-199">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="104d4-199">Next steps</span></span>

<span data-ttu-id="104d4-200">Bu belgede, bir Storm topolojisinin SQL veritabanına veri göndermek ve Power BI kullanarak verileri Görselleştir öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="104d4-200">In this document, you learned how to send data from a Storm topology to SQL Database, then visualize the data using Power BI.</span></span> <span data-ttu-id="104d4-201">Hdınsight üzerinde Storm kullanarak diğer Azure teknolojileri ile çalışma konusunda daha fazla bilgi için aşağıdaki belgesine bakın:</span><span class="sxs-lookup"><span data-stu-id="104d4-201">For information on how to work with other Azure technologies using Storm on HDInsight, see the following document:</span></span>

* [<span data-ttu-id="104d4-202">HDInsight üzerinde Storm için örnek topolojiler</span><span class="sxs-lookup"><span data-stu-id="104d4-202">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)
