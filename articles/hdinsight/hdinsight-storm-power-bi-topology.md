---
title: "Power BI - Azure Hdınsight'ta Apache Storm aaaUse | Microsoft Docs"
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
ms.openlocfilehash: 194cd8220bd60475af1d64a110e4b23ef92e1bc8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-power-bi-toovisualize-data-from-an-apache-storm-topology"></a><span data-ttu-id="b64cb-103">Power BI toovisualize veri bir Apache Storm topolojisini kullanma</span><span class="sxs-lookup"><span data-stu-id="b64cb-103">Use Power BI toovisualize data from an Apache Storm topology</span></span>

<span data-ttu-id="b64cb-104">Power BI raporları gibi toovisually görüntü verileri sağlar.</span><span class="sxs-lookup"><span data-stu-id="b64cb-104">Power BI allows you toovisually display data as reports.</span></span> <span data-ttu-id="b64cb-105">Bu belgede nasıl bir örnek sağlanmaktadır toogenerate verilerini Power BI Hdınsight üzerinde Apache Storm toouse.</span><span class="sxs-lookup"><span data-stu-id="b64cb-105">This document provides an example of how toouse Apache Storm on HDInsight toogenerate data for Power BI.</span></span>

> [!NOTE]
> <span data-ttu-id="b64cb-106">Merhaba bu belgedeki adımları Visual Studio ile Windows geliştirme ortamına dayanır.</span><span class="sxs-lookup"><span data-stu-id="b64cb-106">hello steps in this document rely on a Windows development environment with Visual Studio.</span></span> <span data-ttu-id="b64cb-107">Merhaba derlenmiş proje gönderilen tooa Linux tabanlı Hdınsight kümesi olabilir.</span><span class="sxs-lookup"><span data-stu-id="b64cb-107">hello compiled project can be submitted tooa Linux-based HDInsight cluster.</span></span> <span data-ttu-id="b64cb-108">Yalnızca Linux tabanlı kümelerde sonra 10/28/2016 desteği SCP.NET topolojileri oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="b64cb-108">Only Linux-based clusters created after 10/28/2016 support SCP.NET topologies.</span></span>
>
> <span data-ttu-id="b64cb-109">toouse güncelleştirme hello Microsoft.SCP.Net.SDK NuGet paketi, proje tooversion 0.10.0.6 tarafından kullanılan ya da daha yüksek bir Linux tabanlı kümesi içeren bir C# topolojisi.</span><span class="sxs-lookup"><span data-stu-id="b64cb-109">toouse a C# topology with a Linux-based cluster, update hello Microsoft.SCP.Net.SDK NuGet package used by your project tooversion 0.10.0.6 or higher.</span></span> <span data-ttu-id="b64cb-110">Merhaba hello paketin sürümü yüklü Hdınsight üzerinde Storm hello ana sürümüne de eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="b64cb-110">hello version of hello package must also match hello major version of Storm installed on HDInsight.</span></span> <span data-ttu-id="b64cb-111">Örneğin, HDInsight sürüm 3.3 ve 3.4 üzerindeki Strom bileşenleri, Storm 0.10.x sürümünü kullanırken HDInsight 3.5 ile Storm 1.0.x kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b64cb-111">For example, Storm on HDInsight versions 3.3 and 3.4 use Storm version 0.10.x, while HDInsight 3.5 uses Storm 1.0.x.</span></span>
>
> <span data-ttu-id="b64cb-112">C# topolojileri Linux tabanlı kümelerde .NET 4.5 kullanın ve hello Hdınsight kümesinde Mono toorun kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b64cb-112">C# topologies on Linux-based clusters must use .NET 4.5, and use Mono toorun on hello HDInsight cluster.</span></span> <span data-ttu-id="b64cb-113">Çoğu şeyler çalışır.</span><span class="sxs-lookup"><span data-stu-id="b64cb-113">Most things work.</span></span> <span data-ttu-id="b64cb-114">Merhaba ancak denetlemelisiniz [Mono Uyumluluk](http://www.mono-project.com/docs/about-mono/compatibility/) olası uyumsuzlukları belge.</span><span class="sxs-lookup"><span data-stu-id="b64cb-114">However you should check hello [Mono Compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) document for potential incompatibilities.</span></span>
>
> <span data-ttu-id="b64cb-115">Windows tabanlı veya Linux tabanlı Hdınsight ile çalışır, bu proje için bir Java sürümü için bkz: [işlem Azure Event Hubs (Java) hdınsight'ta Storm olaylarından](hdinsight-storm-develop-java-event-hub-topology.md).</span><span class="sxs-lookup"><span data-stu-id="b64cb-115">For a Java version of this project, which works with Linux-based or Windows-based HDInsight, see [Process events from Azure Event Hubs with Storm on HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b64cb-116">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="b64cb-116">Prerequisites</span></span>

* <span data-ttu-id="b64cb-117">Bir Azure Active Directory kullanıcı ile [Power BI](https://powerbi.com) erişim.</span><span class="sxs-lookup"><span data-stu-id="b64cb-117">An Azure Active Directory user with [Power BI](https://powerbi.com) access.</span></span>
* <span data-ttu-id="b64cb-118">Hdınsight kümesi.</span><span class="sxs-lookup"><span data-stu-id="b64cb-118">An HDInsight cluster.</span></span> <span data-ttu-id="b64cb-119">Daha fazla bilgi için bkz: [Hdınsight üzerinde Storm kullanmaya başlama](hdinsight-apache-storm-tutorial-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="b64cb-119">For more information, see [Get started with Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="b64cb-120">Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir.</span><span class="sxs-lookup"><span data-stu-id="b64cb-120">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="b64cb-121">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="b64cb-121">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="b64cb-122">Visual Studio (sürümleri aşağıdaki hello biri)</span><span class="sxs-lookup"><span data-stu-id="b64cb-122">Visual Studio (one of hello following versions)</span></span>

  * <span data-ttu-id="b64cb-123">Visual Studio 2012 ile [güncelleştirme 4](http://www.microsoft.com/download/details.aspx?id=39305)</span><span class="sxs-lookup"><span data-stu-id="b64cb-123">Visual Studio 2012 with [update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span></span>
  * <span data-ttu-id="b64cb-124">Visual Studio 2013 [güncelleştirme 4](http://www.microsoft.com/download/details.aspx?id=44921) veya [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?linkid=517284&clcid=0x409)</span><span class="sxs-lookup"><span data-stu-id="b64cb-124">Visual Studio 2013 with [update 4](http://www.microsoft.com/download/details.aspx?id=44921) or [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?linkid=517284&clcid=0x409)</span></span>
  * [<span data-ttu-id="b64cb-125">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="b64cb-125">Visual Studio 2015</span></span>](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
  * <span data-ttu-id="b64cb-126">Visual Studio 2017 (herhangi bir sürümünü)</span><span class="sxs-lookup"><span data-stu-id="b64cb-126">Visual Studio 2017 (any edition)</span></span>

* <span data-ttu-id="b64cb-127">Visual Studio için Hdınsight araçları Hello: bkz [hello Hdınsight araçları Visual Studio için kullanmaya başlama](hdinsight-hadoop-visual-studio-tools-get-started.md) yükleme bilgileri hakkında bilgi için.</span><span class="sxs-lookup"><span data-stu-id="b64cb-127">hello HDInsight Tools for Visual Studio: See [Get started using hello HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) for information on installation information.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="b64cb-128">Nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="b64cb-128">How it works</span></span>

<span data-ttu-id="b64cb-129">Bu örnek, rasgele Internet Information Services (IIS) günlük verileri oluşturur bir C# Storm topolojisinin içerir.</span><span class="sxs-lookup"><span data-stu-id="b64cb-129">This example contains a C# Storm topology that randomly generates Internet Information Services (IIS) log data.</span></span> <span data-ttu-id="b64cb-130">Bu veri sonra tooa SQL veritabanına yazılır ve isteğe bağlı olarak buradan kullanılan toogenerate raporlar Power bı'da değildir.</span><span class="sxs-lookup"><span data-stu-id="b64cb-130">This data is then written tooa SQL Database, and from there it is used toogenerate reports in Power BI.</span></span>

<span data-ttu-id="b64cb-131">dosyalar uygulama hello ana işlevi bu örnekte aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="b64cb-131">hello following files implement hello main functionality of this example:</span></span>

* <span data-ttu-id="b64cb-132">**SqlAzureBolt.cs**: hello Storm topolojisini tooSQL veritabanı üretilen bilgilerini yazar.</span><span class="sxs-lookup"><span data-stu-id="b64cb-132">**SqlAzureBolt.cs**: Writes information produced in hello Storm topology tooSQL Database.</span></span>
* <span data-ttu-id="b64cb-133">**IISLogsTable.sql**: hello veriler depolanır hello Transact-SQL deyimleri kullanılan toogenerate hello veritabanı.</span><span class="sxs-lookup"><span data-stu-id="b64cb-133">**IISLogsTable.sql**: hello Transact-SQL statements used toogenerate hello database that hello data is stored in.</span></span>

> [!WARNING]
> <span data-ttu-id="b64cb-134">Hdınsight kümenize hello topoloji başlatmadan önce SQL veritabanında Hello tablo oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b64cb-134">Create hello table in SQL Database before starting hello topology on your HDInsight cluster.</span></span>

## <a name="download-hello-example"></a><span data-ttu-id="b64cb-135">Merhaba örneği indirin</span><span class="sxs-lookup"><span data-stu-id="b64cb-135">Download hello example</span></span>

<span data-ttu-id="b64cb-136">Merhaba karşıdan [Hdınsight C# Storm Power BI örnek](https://github.com/Azure-Samples/hdinsight-dotnet-storm-powerbi).</span><span class="sxs-lookup"><span data-stu-id="b64cb-136">Download hello [HDInsight C# Storm Power BI example](https://github.com/Azure-Samples/hdinsight-dotnet-storm-powerbi).</span></span> <span data-ttu-id="b64cb-137">toodownload, ya da çatalı/kullanarak kopya [git](http://git-scm.com/), veya hello **karşıdan** bağlantı toodownload hello arşiv .zip.</span><span class="sxs-lookup"><span data-stu-id="b64cb-137">toodownload it, either fork/clone it using [git](http://git-scm.com/), or use hello **Download** link toodownload a .zip of hello archive.</span></span>

## <a name="create-a-database"></a><span data-ttu-id="b64cb-138">Veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="b64cb-138">Create a database</span></span>

1. <span data-ttu-id="b64cb-139">bir veritabanı toocreate hello hello adımları kullanın [SQL Database Öğreticisi](../sql-database/sql-database-get-started.md) belge.</span><span class="sxs-lookup"><span data-stu-id="b64cb-139">toocreate a database, use hello steps in hello [SQL Database tutorial](../sql-database/sql-database-get-started.md) document.</span></span>

2. <span data-ttu-id="b64cb-140">Connect toohello veritabanı aşağıdaki hello tarafından adımları hello [tooa SQL veritabanı ile Visual Studio bağlanmak](../sql-database/sql-database-connect-query.md) belge.</span><span class="sxs-lookup"><span data-stu-id="b64cb-140">Connect toohello database by following hello steps in hello [Connect tooa SQL Database with Visual Studio](../sql-database/sql-database-connect-query.md) document.</span></span>

3. <span data-ttu-id="b64cb-141">Nesne Gezgini'nde hello veritabanını sağ tıklatın ve seçin **yeni sorgu**.</span><span class="sxs-lookup"><span data-stu-id="b64cb-141">In Object Explorer, right-click hello database and select  **New Query**.</span></span> <span data-ttu-id="b64cb-142">Yapıştır hello Merhaba içeriğine **IISLogsTable.sql** hello dahil dosya hello sorgu penceresine proje indirilir ve ardından kullanın Ctrl + Shift + E tooexecute hello sorgu.</span><span class="sxs-lookup"><span data-stu-id="b64cb-142">Paste hello contents of hello **IISLogsTable.sql** file included in hello downloaded project into hello query window, and then use Ctrl + Shift + E tooexecute hello query.</span></span> <span data-ttu-id="b64cb-143">Komutlar başarıyla tamamlandı hello bir ileti alırsınız.</span><span class="sxs-lookup"><span data-stu-id="b64cb-143">You should receive a message that hello commands completed successfully.</span></span>

## <a name="configure-hello-sample"></a><span data-ttu-id="b64cb-144">Merhaba örnek yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b64cb-144">Configure hello sample</span></span>

1. <span data-ttu-id="b64cb-145">Merhaba gelen [Azure portal](https://portal.azure.com), SQL veritabanınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="b64cb-145">From hello [Azure portal](https://portal.azure.com), select your SQL database.</span></span> <span data-ttu-id="b64cb-146">Merhaba gelen **Essentials** hello SQL veritabanı dikey, select bölümünü **veritabanı bağlantı dizelerini Göster**.</span><span class="sxs-lookup"><span data-stu-id="b64cb-146">From hello **Essentials** section of hello SQL database blade, select **Show database connection strings**.</span></span> <span data-ttu-id="b64cb-147">Görüntülenen hello listesinden hello kopyalama **ADO.NET (SQL kimlik doğrulaması)** bilgi.</span><span class="sxs-lookup"><span data-stu-id="b64cb-147">From hello list that appears, copy hello **ADO.NET (SQL authentication)** information.</span></span>

2. <span data-ttu-id="b64cb-148">Merhaba örnek Visual Studio'da açın.</span><span class="sxs-lookup"><span data-stu-id="b64cb-148">Open hello sample in Visual Studio.</span></span> <span data-ttu-id="b64cb-149">Gelen **Çözüm Gezgini**açın hello **App.config** dosya ve giriş aşağıdaki hello bulun:</span><span class="sxs-lookup"><span data-stu-id="b64cb-149">From **Solution Explorer**, open hello **App.config** file, and then find hello following entry:</span></span>

        <add key="SqlAzureConnectionString" value="##TOBEFILLED##" />

    <span data-ttu-id="b64cb-150">Hello yerine **TOBEFILLED ##** hello veritabanı bağlantı dizesi değerle hello önceki adımda kopyaladığınız.</span><span class="sxs-lookup"><span data-stu-id="b64cb-150">Replace hello **##TOBEFILLED##** value with hello database connection string copied in hello previous step.</span></span> <span data-ttu-id="b64cb-151">Değiştir **{,\_kullanıcı adı}** ve **{,\_parola}** hello kullanıcı adı ve parola hello veritabanı için.</span><span class="sxs-lookup"><span data-stu-id="b64cb-151">Replace **{your\_username}** and **{your\_password}** with hello username and password for hello database.</span></span>

3. <span data-ttu-id="b64cb-152">Kaydedin ve hello dosyaları kapatın.</span><span class="sxs-lookup"><span data-stu-id="b64cb-152">Save and close hello files.</span></span>

## <a name="deploy-hello-sample"></a><span data-ttu-id="b64cb-153">Merhaba örnek dağıtma</span><span class="sxs-lookup"><span data-stu-id="b64cb-153">Deploy hello sample</span></span>

1. <span data-ttu-id="b64cb-154">Gelen **Çözüm Gezgini**, sağ hello **StormToSQL** proje ve seçin **hdınsight'ta tooStorm gönderme**.</span><span class="sxs-lookup"><span data-stu-id="b64cb-154">From **Solution Explorer**, right-click hello **StormToSQL** project and select **Submit tooStorm on HDInsight**.</span></span> <span data-ttu-id="b64cb-155">Select hello Hdınsight hello kümeden **Storm kümesi** iletişim kutusu açılır.</span><span class="sxs-lookup"><span data-stu-id="b64cb-155">Select hello HDInsight cluster from hello **Storm Cluster** dropdown dialog.</span></span>

   > [!NOTE]
   > <span data-ttu-id="b64cb-156">Merhaba birkaç saniye sürebilir **Storm kümesi** açılır toopopulate sunucu adları ile.</span><span class="sxs-lookup"><span data-stu-id="b64cb-156">It may take a few seconds for hello **Storm Cluster** dropdown toopopulate with server names.</span></span>
   >
   > <span data-ttu-id="b64cb-157">İstenirse, Azure aboneliğinizin hello oturum açma kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="b64cb-157">If prompted, enter hello login credentials for your Azure subscription.</span></span> <span data-ttu-id="b64cb-158">Birden fazla aboneliğiniz varsa, toohello Hdınsight kümesi üzerinde Storm'a içeren bir oturum açın.</span><span class="sxs-lookup"><span data-stu-id="b64cb-158">If you have more than one subscription, log in toohello one that contains your Storm on HDInsight cluster.</span></span>

2. <span data-ttu-id="b64cb-159">Merhaba topoloji gönderildiğinde hello __topoloji Görüntüleyicisi__ görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="b64cb-159">When hello topology has been submitted, hello __Topology Viewer__ appears.</span></span> <span data-ttu-id="b64cb-160">tooview bu topoloji, hello listesinden seçim hello SqlAzureWriterTopology girişi.</span><span class="sxs-lookup"><span data-stu-id="b64cb-160">tooview this topology, select hello SqlAzureWriterTopology entry from hello list.</span></span>

    ![Seçili hello topolojisi ile Merhaba topolojileri](./media/hdinsight-storm-power-bi-topology/topologyview.png)

    <span data-ttu-id="b64cb-162">Bu görünüm toosee bilgileri hello topolojisine kullanın veya bir giriş (örneğin, hello SqlAzureBolt) toosee bilgi belirli tooa bileşeni hello topolojisinde çift tıklatın.</span><span class="sxs-lookup"><span data-stu-id="b64cb-162">You can use this view toosee information on hello topology, or double-click an entry (such as hello SqlAzureBolt) toosee information specific tooa component in hello topology.</span></span>

3. <span data-ttu-id="b64cb-163">Merhaba sonra topoloji sahip başlattıysanız birkaç dakika toocreate hello veritabanı kullanılan dönüş toohello SQL sorgu penceresi.</span><span class="sxs-lookup"><span data-stu-id="b64cb-163">After hello topology has ran for a few minutes, return toohello SQL query window you used toocreate hello database.</span></span> <span data-ttu-id="b64cb-164">Merhaba varolan deyimleri sorgu aşağıdaki hello ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="b64cb-164">Replace hello existing statements with hello following query:</span></span>

        select * from iislogs;

    <span data-ttu-id="b64cb-165">Kullanın Ctrl + Shift + E tooexecute hello sorgu ve veri aşağıdaki sonuçları benzer toohello alırsınız:</span><span class="sxs-lookup"><span data-stu-id="b64cb-165">Use Ctrl + Shift + E tooexecute hello query, and you should receive results similar toohello following data:</span></span>

        1    2016-05-27 17:57:14.797    255.255.255.255    /bar    GET    200
        2    2016-05-27 17:57:14.843    127.0.0.1    /spam/eggs    POST    500
        3    2016-05-27 17:57:14.850    123.123.123.123    /eggs    DELETE    200
        4    2016-05-27 17:57:14.853    127.0.0.1    /foo    POST    404
        5    2016-05-27 17:57:14.853    10.9.8.7    /bar    GET    200
        6    2016-05-27 17:57:14.857    192.168.1.1    /spam    DELETE    200

    <span data-ttu-id="b64cb-166">Bu veriler hello Storm topolojisini yazılmış.</span><span class="sxs-lookup"><span data-stu-id="b64cb-166">This data has been written from hello Storm topology.</span></span>

## <a name="create-a-report"></a><span data-ttu-id="b64cb-167">Bir rapor oluşturun</span><span class="sxs-lookup"><span data-stu-id="b64cb-167">Create a report</span></span>

1. <span data-ttu-id="b64cb-168">Toohello bağlanmak [Azure SQL Veritabanı Bağlayıcısı](https://app.powerbi.com/getdata/bigdata/azure-sql-database-with-live-connect) Power BI için.</span><span class="sxs-lookup"><span data-stu-id="b64cb-168">Connect toohello [Azure SQL Database connector](https://app.powerbi.com/getdata/bigdata/azure-sql-database-with-live-connect) for Power BI.</span></span> 

2. <span data-ttu-id="b64cb-169">İçinde **veritabanları**seçin **almak**.</span><span class="sxs-lookup"><span data-stu-id="b64cb-169">Within **Databases**, select **Get**.</span></span>

3. <span data-ttu-id="b64cb-170">Seçin **Azure SQL veritabanı**ve ardından **Bağlan**.</span><span class="sxs-lookup"><span data-stu-id="b64cb-170">Select **Azure SQL Database**, and then select **Connect**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b64cb-171">Toodownload hello Power BI Desktop toocontinue istenebilir.</span><span class="sxs-lookup"><span data-stu-id="b64cb-171">You may be asked toodownload hello Power BI Desktop toocontinue.</span></span> <span data-ttu-id="b64cb-172">Bu durumda, aşağıdaki adımları tooconnect hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="b64cb-172">If so, use hello following steps tooconnect:</span></span>
    >
    > 1. <span data-ttu-id="b64cb-173">Power BI Desktop açıp seçin __Veri Al__.</span><span class="sxs-lookup"><span data-stu-id="b64cb-173">Open Power BI Desktop and select __Get Data__.</span></span>
    > <span data-ttu-id="b64cb-174">2 seçin __Azure__ve ardından __Azure SQL veritabanı__.</span><span class="sxs-lookup"><span data-stu-id="b64cb-174">2  Select __Azure__, and then __Azure SQL database__.</span></span>

4. <span data-ttu-id="b64cb-175">Merhaba bilgi tooconnect tooyour Azure SQL veritabanı girin.</span><span class="sxs-lookup"><span data-stu-id="b64cb-175">Enter hello information tooconnect tooyour Azure SQL Database.</span></span> <span data-ttu-id="b64cb-176">Merhaba ziyaret ederek bu bilgiyi bulabilirsiniz [Azure portal](https://portal.azure.com) ve SQL veritabanınız seçme.</span><span class="sxs-lookup"><span data-stu-id="b64cb-176">You can find this information by visiting hello [Azure portal](https://portal.azure.com) and selecting your SQL database.</span></span>

   > [!NOTE]
   > <span data-ttu-id="b64cb-177">Kullanarak hello yenileme aralığı ve özel filtreler de ayarlayabilirsiniz **Gelişmiş Seçenekler etkinleştirmek** iletişim hello bağlantı.</span><span class="sxs-lookup"><span data-stu-id="b64cb-177">You can also set hello refresh interval and custom filters by using **Enable Advanced Options** from hello connect dialog.</span></span>

5. <span data-ttu-id="b64cb-178">Bağlandıktan sonra yeni bir veri kümesi ile aynı hello veritabanı olarak bağlı adını hello görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="b64cb-178">After you've connected, you will see a new dataset with hello same name as hello database you connected to.</span></span> <span data-ttu-id="b64cb-179">Bir rapor tasarlama hello dataset toobegin seçin.</span><span class="sxs-lookup"><span data-stu-id="b64cb-179">Select hello dataset toobegin designing a report.</span></span>

6. <span data-ttu-id="b64cb-180">Gelen **alanları**, hello genişletin **IISLOGS** girişi.</span><span class="sxs-lookup"><span data-stu-id="b64cb-180">From **Fields**, expand hello **IISLOGS** entry.</span></span> <span data-ttu-id="b64cb-181">listeleri URI hello rapor kaynaklandığını, toocreate hello onay kutusunu seçin **bulunamadı.%N**.</span><span class="sxs-lookup"><span data-stu-id="b64cb-181">toocreate a report that lists hello URI stems, select hello checkbox for **URISTEM**.</span></span>

    ![Rapor oluşturma](./media/hdinsight-storm-power-bi-topology/createreport.png)

7. <span data-ttu-id="b64cb-183">Ardından, sürükleyin **yöntemi** toohello rapor.</span><span class="sxs-lookup"><span data-stu-id="b64cb-183">Next, drag **METHOD** toohello report.</span></span> <span data-ttu-id="b64cb-184">Merhaba rapor güncelleştirmeleri toolist hello kaynaklandığını ve hello karşılık gelen HTTP yöntemini hello HTTP isteği için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b64cb-184">hello report updates toolist hello stems and hello corresponding HTTP method used for hello HTTP request.</span></span>

    ![Merhaba yöntemi veri ekleme](./media/hdinsight-storm-power-bi-topology/uristemandmethod.png)

8. <span data-ttu-id="b64cb-186">Merhaba gelen **görselleştirmeleri** sütun, select hello **alanları** simgesine ve ardından hello aşağı ok sonraki çok**yöntemi** hello içinde **değerleri**bölümü.</span><span class="sxs-lookup"><span data-stu-id="b64cb-186">From hello **Visualizations** column, select hello **Fields** icon, and then select hello down arrow next too**METHOD** in hello **Values** section.</span></span> <span data-ttu-id="b64cb-187">bir URI kaç kez sayısına erişilmeden, toodisplay seçin **sayısı**.</span><span class="sxs-lookup"><span data-stu-id="b64cb-187">toodisplay a count of how many times a URI has been accessed, select **Count**.</span></span>

    ![Yöntemleri tooa sayısını değiştirme](./media/hdinsight-storm-power-bi-topology/count.png)

9. <span data-ttu-id="b64cb-189">Ardından, hello'ı seçin **yığılmış sütun grafiği** toochange hello bilgileri nasıl görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="b64cb-189">Next, select hello **Stacked column chart** toochange how hello information is displayed.</span></span>

    ![Değişen tooa yığın grafik](./media/hdinsight-storm-power-bi-topology/stackedcolumn.png)

10. <span data-ttu-id="b64cb-191">toosave hello raporu, select **kaydetmek** ve hello rapor için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="b64cb-191">toosave hello report, select **Save** and enter a name for hello report.</span></span>

## <a name="stop-hello-topology"></a><span data-ttu-id="b64cb-192">Merhaba topolojiyi durdurma</span><span class="sxs-lookup"><span data-stu-id="b64cb-192">Stop hello topology</span></span>

<span data-ttu-id="b64cb-193">durdurmak veya Hdınsight kümesinde Storm hello silme kadar hello topoloji toorun devam eder.</span><span class="sxs-lookup"><span data-stu-id="b64cb-193">hello topology continues toorun until you stop it or delete hello Storm on HDInsight cluster.</span></span> <span data-ttu-id="b64cb-194">toostop topoloji Merhaba, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="b64cb-194">toostop hello topology, perform hello following steps:</span></span>

1. <span data-ttu-id="b64cb-195">Visual Studio'da toohello topoloji Görüntüleyicisi dönün ve hello topoloji seçin.</span><span class="sxs-lookup"><span data-stu-id="b64cb-195">In Visual Studio, return toohello topology viewer and select hello topology.</span></span>

2. <span data-ttu-id="b64cb-196">Select hello **KILL** düğmesini toostop hello topolojisi.</span><span class="sxs-lookup"><span data-stu-id="b64cb-196">Select hello **Kill** button toostop hello topology.</span></span>

    ![Merhaba topoloji özeti düğmesini KILL](./media/hdinsight-storm-power-bi-topology/killtopology.png)

## <a name="delete-your-cluster"></a><span data-ttu-id="b64cb-198">Kümenizi Sil</span><span class="sxs-lookup"><span data-stu-id="b64cb-198">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="b64cb-199">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b64cb-199">Next steps</span></span>

<span data-ttu-id="b64cb-200">Bu belgede, öğrenilen nasıl toosend verilerini bir Storm topolojisini tooSQL veritabanını, sonra görselleştirmek Power BI kullanarak hello verileri.</span><span class="sxs-lookup"><span data-stu-id="b64cb-200">In this document, you learned how toosend data from a Storm topology tooSQL Database, then visualize hello data using Power BI.</span></span> <span data-ttu-id="b64cb-201">Hakkında bilgi için Hdınsight üzerinde Storm kullanarak diğer Azure teknolojileriyle toowork belge aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="b64cb-201">For information on how toowork with other Azure technologies using Storm on HDInsight, see hello following document:</span></span>

* [<span data-ttu-id="b64cb-202">HDInsight üzerinde Storm için örnek topolojiler</span><span class="sxs-lookup"><span data-stu-id="b64cb-202">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)
