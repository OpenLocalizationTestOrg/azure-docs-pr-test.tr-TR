---
title: "SQL Server'dan Azure SQL veri ambarı (SSIS) içine aaaLoad veri | Microsoft Docs"
description: "Toocreate çok çeşitli verileri bir SQL Server Integration Services (SSIS) paketi toomove verilerinden tooSQL veri ambarına nasıl kaynakları gösterir."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: e2c252e9-0828-47c2-a808-e3bea46c134a
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 03/30/2017
ms.author: cakarst;douglasl;barbkess
ms.openlocfilehash: bb28a08807a5b07832b85f2f074c2acf912c1dc3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-sql-server-into-azure-sql-data-warehouse-ssis"></a><span data-ttu-id="32a03-103">SQL Server'dan Azure SQL veri ambarı (SSIS) içine veri yükleme</span><span class="sxs-lookup"><span data-stu-id="32a03-103">Load data from SQL Server into Azure SQL Data Warehouse (SSIS)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="32a03-104">SSIS</span><span class="sxs-lookup"><span data-stu-id="32a03-104">SSIS</span></span>](sql-data-warehouse-load-from-sql-server-with-integration-services.md)
> * [<span data-ttu-id="32a03-105">PolyBase</span><span class="sxs-lookup"><span data-stu-id="32a03-105">PolyBase</span></span>](sql-data-warehouse-load-from-sql-server-with-polybase.md)
> * [<span data-ttu-id="32a03-106">bcp</span><span class="sxs-lookup"><span data-stu-id="32a03-106">bcp</span></span>](sql-data-warehouse-load-from-sql-server-with-bcp.md)
> 
> 

<span data-ttu-id="32a03-107">SQL Server Integration Services (SSIS) paket tooload verileri SQL Server'dan Azure SQL Data Warehouse'a oluşturun.</span><span class="sxs-lookup"><span data-stu-id="32a03-107">Create a SQL Server Integration Services (SSIS) package tooload data from SQL Server into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="32a03-108">İsteğe bağlı olarak, yapılandırmayı, dönüştürme ve hello SSIS veri akışı geçerken hello verilerini temizlemek.</span><span class="sxs-lookup"><span data-stu-id="32a03-108">You can optionally restructure, transform, and cleanse hello data as it passes through hello SSIS data flow.</span></span>

<span data-ttu-id="32a03-109">Bu öğreticide şunları yapacaksınız:</span><span class="sxs-lookup"><span data-stu-id="32a03-109">In this tutorial, you will:</span></span>

* <span data-ttu-id="32a03-110">Visual Studio'da yeni bir Integration Services projesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="32a03-110">Create a new Integration Services project in Visual Studio.</span></span>
* <span data-ttu-id="32a03-111">(Kaynak) olarak SQL Server ve SQL Data Warehouse (hedef) olarak da dahil olmak üzere toodata kaynaklar bağlayın.</span><span class="sxs-lookup"><span data-stu-id="32a03-111">Connect toodata sources, including SQL Server (as a source) and SQL Data Warehouse (as a destination).</span></span>
* <span data-ttu-id="32a03-112">Merhaba hedefe hello kaynaktan verileri yükler bir SSIS paketi tasarlayın.</span><span class="sxs-lookup"><span data-stu-id="32a03-112">Design an SSIS package that loads data from hello source into hello destination.</span></span>
* <span data-ttu-id="32a03-113">Merhaba SSIS paketi tooload hello veri çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="32a03-113">Run hello SSIS package tooload hello data.</span></span>

<span data-ttu-id="32a03-114">Bu öğretici, SQL Server hello veri kaynağı olarak kullanır.</span><span class="sxs-lookup"><span data-stu-id="32a03-114">This tutorial uses SQL Server as hello data source.</span></span> <span data-ttu-id="32a03-115">SQL Server, şirket içinde veya bir Azure sanal makinesi çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="32a03-115">SQL Server could be running on premises or in an Azure virtual machine.</span></span>

## <a name="basic-concepts"></a><span data-ttu-id="32a03-116">Temel kavramlar</span><span class="sxs-lookup"><span data-stu-id="32a03-116">Basic concepts</span></span>
<span data-ttu-id="32a03-117">Merhaba paket hello SSIS iş birimidir.</span><span class="sxs-lookup"><span data-stu-id="32a03-117">hello package is hello unit of work in SSIS.</span></span> <span data-ttu-id="32a03-118">İlişkili paketleri projelerinde gruplandırılır.</span><span class="sxs-lookup"><span data-stu-id="32a03-118">Related packages are grouped in projects.</span></span> <span data-ttu-id="32a03-119">SQL Server veri araçları ile Visual Studio'da projeler ve tasarım paketler oluşturun.</span><span class="sxs-lookup"><span data-stu-id="32a03-119">You create projects and design packages in Visual Studio with SQL Server Data Tools.</span></span> <span data-ttu-id="32a03-120">işlem, sürükleyip bileşenleri hello araç toohello tasarım yüzeyden bir görsel işlemidir hello tasarım bunları bağlamak ve özelliklerini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="32a03-120">hello design process is a visual process in which you drag and drop components from hello Toolbox toohello design surface, connect them, and set their properties.</span></span> <span data-ttu-id="32a03-121">Paketinizi tamamladıktan sonra isteğe bağlı olarak tooSQL sunucu kapsamlı yönetim, izleme ve güvenlik dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="32a03-121">After you finish your package, you can optionally deploy it tooSQL Server for comprehensive management, monitoring, and security.</span></span>

## <a name="options-for-loading-data-with-ssis"></a><span data-ttu-id="32a03-122">SSIS ile veri yükleme seçenekleri</span><span class="sxs-lookup"><span data-stu-id="32a03-122">Options for loading data with SSIS</span></span>
<span data-ttu-id="32a03-123">SQL Server Integration Services (SSIS) bağlanan ve bu verileri SQL Data Warehouse'a, yükleme için çeşitli seçenekler sağlayan esnek araçlar kümesidir.</span><span class="sxs-lookup"><span data-stu-id="32a03-123">SQL Server Integration Services (SSIS) is a flexible set of tools that provides a variety of options for connecting to, and loading data into, SQL Data Warehouse.</span></span>

1. <span data-ttu-id="32a03-124">ADO NET hedef tooconnect tooSQL veri ambarı kullanın.</span><span class="sxs-lookup"><span data-stu-id="32a03-124">Use an ADO NET Destination tooconnect tooSQL Data Warehouse.</span></span> <span data-ttu-id="32a03-125">En az yapılandırma seçenekleri hello içerdiğinden Bu öğretici bir ADO NET hedef kullanır.</span><span class="sxs-lookup"><span data-stu-id="32a03-125">This tutorial uses an ADO NET Destination because it has hello fewest configuration options.</span></span>
2. <span data-ttu-id="32a03-126">OLE DB hedef tooconnect tooSQL veri ambarı kullanın.</span><span class="sxs-lookup"><span data-stu-id="32a03-126">Use an OLE DB Destination tooconnect tooSQL Data Warehouse.</span></span> <span data-ttu-id="32a03-127">Bu seçenek hello ADO NET hedef daha biraz daha iyi performans sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="32a03-127">This option may provide slightly better performance than hello ADO NET Destination.</span></span>
3. <span data-ttu-id="32a03-128">Hello Azure Blob karşıya yükleme görev toostage hello verileri Azure Blob depolama alanına kullanın.</span><span class="sxs-lookup"><span data-stu-id="32a03-128">Use hello Azure Blob Upload Task toostage hello data in Azure Blob Storage.</span></span> <span data-ttu-id="32a03-129">Daha sonra hello SSIS SQL Yürüt görev toolaunch hello verileri SQL Data Warehouse'a yükler Polybase komut dosyası kullanın.</span><span class="sxs-lookup"><span data-stu-id="32a03-129">Then use hello SSIS Execute SQL task toolaunch a Polybase script that loads hello data into SQL Data Warehouse.</span></span> <span data-ttu-id="32a03-130">Bu seçenek, burada listelenen hello üç seçenekten birini hello en iyi performans sağlar.</span><span class="sxs-lookup"><span data-stu-id="32a03-130">This option provides hello best performance of hello three options listed here.</span></span> <span data-ttu-id="32a03-131">tooget hello görev, Azure Blob karşıya yükle hello [Microsoft SQL Server 2016 tümleştirme hizmetleri özellik paketi Azure][Microsoft SQL Server 2016 Integration Services Feature Pack for Azure].</span><span class="sxs-lookup"><span data-stu-id="32a03-131">tooget hello Azure Blob Upload task, download hello [Microsoft SQL Server 2016 Integration Services Feature Pack for Azure][Microsoft SQL Server 2016 Integration Services Feature Pack for Azure].</span></span> <span data-ttu-id="32a03-132">Polybase, hakkında daha fazla toolearn bkz [PolyBase Kılavuzu][PolyBase Guide].</span><span class="sxs-lookup"><span data-stu-id="32a03-132">toolearn more about Polybase, see [PolyBase Guide][PolyBase Guide].</span></span>

## <a name="before-you-start"></a><span data-ttu-id="32a03-133">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="32a03-133">Before you start</span></span>
<span data-ttu-id="32a03-134">toostep Bu öğreticide, aşağıdakiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="32a03-134">toostep through this tutorial, you need:</span></span>

1. <span data-ttu-id="32a03-135">**SQL Server Integration Services (SSIS)**.</span><span class="sxs-lookup"><span data-stu-id="32a03-135">**SQL Server Integration Services (SSIS)**.</span></span> <span data-ttu-id="32a03-136">SSIS SQL Server'ın bir bileşenidir ve bir değerlendirme sürümü veya SQL Server'ın lisanslı bir sürüm gerektirir.</span><span class="sxs-lookup"><span data-stu-id="32a03-136">SSIS is a component of SQL Server and requires an evaluation version or a licensed version of SQL Server.</span></span> <span data-ttu-id="32a03-137">tooget SQL Server 2016 Önizleme'nin değerlendirme sürümünü bkz [SQL Server değerlendirme][SQL Server Evaluations].</span><span class="sxs-lookup"><span data-stu-id="32a03-137">tooget an evaluation version of SQL Server 2016 Preview, see [SQL Server Evaluations][SQL Server Evaluations].</span></span>
2. <span data-ttu-id="32a03-138">**Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="32a03-138">**Visual Studio**.</span></span> <span data-ttu-id="32a03-139">tooget ücretsiz Visual Studio Community Edition Merhaba, bkz: [Visual Studio Community][Visual Studio Community].</span><span class="sxs-lookup"><span data-stu-id="32a03-139">tooget hello free Visual Studio Community Edition, see [Visual Studio Community][Visual Studio Community].</span></span>
3. <span data-ttu-id="32a03-140">**SQL Server veri araçları Visual Studio (SSDT) için**.</span><span class="sxs-lookup"><span data-stu-id="32a03-140">**SQL Server Data Tools for Visual Studio (SSDT)**.</span></span> <span data-ttu-id="32a03-141">tooget SQL Server veri araçları Visual Studio için bkz: [karşıdan SQL Server veri Araçları'nı (SSDT)][Download SQL Server Data Tools (SSDT)].</span><span class="sxs-lookup"><span data-stu-id="32a03-141">tooget SQL Server Data Tools for Visual Studio, see [Download SQL Server Data Tools (SSDT)][Download SQL Server Data Tools (SSDT)].</span></span>
4. <span data-ttu-id="32a03-142">**Örnek veri**.</span><span class="sxs-lookup"><span data-stu-id="32a03-142">**Sample data**.</span></span> <span data-ttu-id="32a03-143">Bu öğretici, SQL Server'da SQL Data Warehouse'a yüklenen kaynak veri toobe hello gibi hello AdventureWorks örnek veritabanında depolanan örnek verileri kullanır.</span><span class="sxs-lookup"><span data-stu-id="32a03-143">This tutorial uses sample data stored in SQL Server in hello AdventureWorks sample database as hello source data toobe loaded into SQL Data Warehouse.</span></span> <span data-ttu-id="32a03-144">tooget hello AdventureWorks örnek veritabanı bkz [AdventureWorks 2014 örnek veritabanları][AdventureWorks 2014 Sample Databases].</span><span class="sxs-lookup"><span data-stu-id="32a03-144">tooget hello AdventureWorks sample database, see [AdventureWorks 2014 Sample Databases][AdventureWorks 2014 Sample Databases].</span></span>
5. <span data-ttu-id="32a03-145">**SQL veri ambarı veritabanı ve izinleri**.</span><span class="sxs-lookup"><span data-stu-id="32a03-145">**A SQL Data Warehouse database and permissions**.</span></span> <span data-ttu-id="32a03-146">Bu öğretici tooa SQL Data Warehouse örneğine bağlanır ve verileri içine yükler.</span><span class="sxs-lookup"><span data-stu-id="32a03-146">This tutorial connects tooa SQL Data Warehouse instance and loads data into it.</span></span> <span data-ttu-id="32a03-147">Bir tablo ve tooload veri toohave izinleri toocreate var.</span><span class="sxs-lookup"><span data-stu-id="32a03-147">You have toohave permissions toocreate a table and tooload data.</span></span>
6. <span data-ttu-id="32a03-148">**Bir güvenlik duvarı kuralı**.</span><span class="sxs-lookup"><span data-stu-id="32a03-148">**A firewall rule**.</span></span> <span data-ttu-id="32a03-149">SQL veri ambarı veri toohello karşıya yüklemeden önce toocreate bir güvenlik duvarı kuralı SQL Data Warehouse, yerel bilgisayarınızın başlangıç IP adresi ile sahip.</span><span class="sxs-lookup"><span data-stu-id="32a03-149">You have toocreate a firewall rule on SQL Data Warehouse with hello IP address of your local computer before you can upload data toohello SQL Data Warehouse.</span></span>

## <a name="step-1-create-a-new-integration-services-project"></a><span data-ttu-id="32a03-150">1. adım: yeni bir Integration Services projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="32a03-150">Step 1: Create a new Integration Services project</span></span>
1. <span data-ttu-id="32a03-151">Visual Studio'yu başlatın.</span><span class="sxs-lookup"><span data-stu-id="32a03-151">Launch Visual Studio.</span></span>
2. <span data-ttu-id="32a03-152">Merhaba üzerinde **dosya** menüsünde, select **yeni | Proje**.</span><span class="sxs-lookup"><span data-stu-id="32a03-152">On hello **File** menu, select **New | Project**.</span></span>
3. <span data-ttu-id="32a03-153">Toohello gidin **yüklü | Şablonları | İş Zekası | Integration Services** proje türleri.</span><span class="sxs-lookup"><span data-stu-id="32a03-153">Navigate toohello **Installed | Templates | Business Intelligence | Integration Services** project types.</span></span>
4. <span data-ttu-id="32a03-154">Seçin **Integration Services proje**.</span><span class="sxs-lookup"><span data-stu-id="32a03-154">Select **Integration Services Project**.</span></span> <span data-ttu-id="32a03-155">İçin değerler sağlayın **adı** ve **konumu**ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="32a03-155">Provide values for **Name** and **Location**, and then select **OK**.</span></span>

<span data-ttu-id="32a03-156">Visual Studio açar ve yeni bir Integration Services (SSIS) projesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="32a03-156">Visual Studio opens and creates a new Integration Services (SSIS) project.</span></span> <span data-ttu-id="32a03-157">Ardından Visual Studio hello projesinde hello Tasarımcısı hello tek yeni SSIS paketi için (Package.dtsx) açar.</span><span class="sxs-lookup"><span data-stu-id="32a03-157">Then Visual Studio opens hello designer for hello single new SSIS package (Package.dtsx) in hello project.</span></span> <span data-ttu-id="32a03-158">Ekran alanları aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="32a03-158">You see hello following screen areas:</span></span>

* <span data-ttu-id="32a03-159">Merhaba solda hello **araç** SSIS bileşenlerinin.</span><span class="sxs-lookup"><span data-stu-id="32a03-159">On hello left, hello **Toolbox** of SSIS components.</span></span>
* <span data-ttu-id="32a03-160">Merhaba ortadaki birden çok sekmelerle tasarım yüzeyi hello.</span><span class="sxs-lookup"><span data-stu-id="32a03-160">In hello middle, hello design surface, with multiple tabs.</span></span> <span data-ttu-id="32a03-161">Genellikle en az kullandığınız hello **akış denetimi** ve hello **veri akışını** sekmeleri.</span><span class="sxs-lookup"><span data-stu-id="32a03-161">You typically use at least hello **Control Flow** and hello **Data Flow** tabs.</span></span>
* <span data-ttu-id="32a03-162">Sağ Hello üzerinde hello **Çözüm Gezgini** ve hello **özellikleri** bölmeleri.</span><span class="sxs-lookup"><span data-stu-id="32a03-162">On hello right, hello **Solution Explorer** and hello **Properties** panes.</span></span>
  
    ![][01]

## <a name="step-2-create-hello-basic-data-flow"></a><span data-ttu-id="32a03-163">2. adım: hello temel veri akışı oluşturma</span><span class="sxs-lookup"><span data-stu-id="32a03-163">Step 2: Create hello basic data flow</span></span>
1. <span data-ttu-id="32a03-164">Bir veri akış görevi hello araç toohello merkezinden hello tasarım yüzeyine sürükleyin (Merhaba üzerinde **akış denetimi** sekmesi).</span><span class="sxs-lookup"><span data-stu-id="32a03-164">Drag a Data Flow Task from hello Toolbox toohello center of hello design surface (on hello **Control Flow** tab).</span></span>
   
    ![][02]
2. <span data-ttu-id="32a03-165">Merhaba veri akış görevi tooswitch toohello veri akışı sekmesini çift tıklatın.</span><span class="sxs-lookup"><span data-stu-id="32a03-165">Double-click hello Data Flow Task tooswitch toohello Data Flow tab.</span></span>
3. <span data-ttu-id="32a03-166">Merhaba diğer kaynakları listesinde hello araç kutusu, bir ADO.NET kaynak toohello tasarım yüzeyine sürükleyin.</span><span class="sxs-lookup"><span data-stu-id="32a03-166">From hello Other Sources list in hello Toolbox, drag an ADO.NET Source toohello design surface.</span></span> <span data-ttu-id="32a03-167">Halen seçili hello kaynak bağdaştırıcısıyla çok adını değiştirin**SQL Server Kaynak** hello içinde **özellikleri** bölmesi.</span><span class="sxs-lookup"><span data-stu-id="32a03-167">With hello source adapter still selected, change its name too**SQL Server source** in hello **Properties** pane.</span></span>
4. <span data-ttu-id="32a03-168">Merhaba diğer hedefler listesinden hello araç kutusu içinde hello ADO.NET kaynak altında bir ADO.NET hedef toohello tasarım yüzeyine sürükleyin.</span><span class="sxs-lookup"><span data-stu-id="32a03-168">From hello Other Destinations list in hello Toolbox, drag an ADO.NET Destination toohello design surface under hello ADO.NET Source.</span></span> <span data-ttu-id="32a03-169">Halen seçili hello hedef bağdaştırıcısıyla çok adını değiştirin**SQL DW hedef** hello içinde **özellikleri** bölmesi.</span><span class="sxs-lookup"><span data-stu-id="32a03-169">With hello destination adapter still selected, change its name too**SQL DW destination** in hello **Properties** pane.</span></span>
   
    ![][09]

## <a name="step-3-configure-hello-source-adapter"></a><span data-ttu-id="32a03-170">3. adım: hello kaynak bağdaştırıcısını yapılandırın</span><span class="sxs-lookup"><span data-stu-id="32a03-170">Step 3: Configure hello source adapter</span></span>
1. <span data-ttu-id="32a03-171">Merhaba kaynak bağdaştırıcısı tooopen hello çift **ADO.NET Kaynak Düzenleyici**.</span><span class="sxs-lookup"><span data-stu-id="32a03-171">Double-click hello source adapter tooopen hello **ADO.NET Source Editor**.</span></span>
   
    ![][03]
2. <span data-ttu-id="32a03-172">Merhaba üzerinde **Bağlantı Yöneticisi** hello sekmesinde **ADO.NET Kaynak Düzenleyici**, hello tıklatın **yeni** düğmesine bir sonraki toohello **ADO.NET Bağlantı Yöneticisi**listesi tooopen hello **ADO.NET Bağlantı Yöneticisi'ni yapılandırma** iletişim kutusuna ve bu öğreticinin yükler veri hello SQL Server veritabanı için bağlantı ayarlarını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="32a03-172">On hello **Connection Manager** tab of hello **ADO.NET Source Editor**, click hello **New** button next toohello **ADO.NET connection manager** list tooopen hello **Configure ADO.NET Connection Manager** dialog box and create connection settings for hello SQL Server database from which this tutorial loads data.</span></span>
   
    ![][04]
3. <span data-ttu-id="32a03-173">Merhaba, **ADO.NET Bağlantı Yöneticisi'ni yapılandırmak** iletişim kutusunda, hello **yeni** düğmesi tooopen hello **Bağlantı Yöneticisi** iletişim kutusuna ve yeni bir veri bağlantısı oluştur.</span><span class="sxs-lookup"><span data-stu-id="32a03-173">In hello **Configure ADO.NET Connection Manager** dialog box, click hello **New** button tooopen hello **Connection Manager** dialog box and create a new data connection.</span></span>
   
    ![][05]
4. <span data-ttu-id="32a03-174">Merhaba, **Bağlantı Yöneticisi** iletişim kutusunda, öğeleri hello.</span><span class="sxs-lookup"><span data-stu-id="32a03-174">In hello **Connection Manager** dialog box, do hello following things.</span></span>
   
   1. <span data-ttu-id="32a03-175">İçin **sağlayıcısı**, hello SqlClient veri sağlayıcısı seçin.</span><span class="sxs-lookup"><span data-stu-id="32a03-175">For **Provider**, select hello SqlClient Data Provider.</span></span>
   2. <span data-ttu-id="32a03-176">İçin **sunucu adı**, hello SQL Server adı girin.</span><span class="sxs-lookup"><span data-stu-id="32a03-176">For **Server name**, enter hello SQL Server name.</span></span>
   3. <span data-ttu-id="32a03-177">Merhaba, **toohello sunucuda oturum** bölümünde, seçin veya kimlik doğrulama bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="32a03-177">In hello **Log on toohello server** section, select or enter authentication information.</span></span>
   4. <span data-ttu-id="32a03-178">Merhaba, **Bağlan tooa veritabanı** bölümünde, hello AdventureWorks örnek veritabanını seçin.</span><span class="sxs-lookup"><span data-stu-id="32a03-178">In hello **Connect tooa database** section, select hello AdventureWorks sample database.</span></span>
   5. <span data-ttu-id="32a03-179">Tıklatın **Bağlantıyı Sına**.</span><span class="sxs-lookup"><span data-stu-id="32a03-179">Click **Test Connection**.</span></span>
      
       ![][06]
   6. <span data-ttu-id="32a03-180">Merhaba hello bağlantı testi sonuçlarını raporlar hello iletişim kutusunda, tıklatın **Tamam** tooreturn toohello **Bağlantı Yöneticisi** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="32a03-180">In hello dialog box that reports hello results of hello connection test, click **OK** tooreturn toohello **Connection Manager** dialog box.</span></span>
   7. <span data-ttu-id="32a03-181">Merhaba, **Bağlantı Yöneticisi** iletişim kutusu, tıklatın **Tamam** tooreturn toohello **ADO.NET Bağlantı Yöneticisi'ni yapılandırma** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="32a03-181">In hello **Connection Manager** dialog box, click **OK** tooreturn toohello **Configure ADO.NET Connection Manager** dialog box.</span></span>
5. <span data-ttu-id="32a03-182">Merhaba, **ADO.NET Bağlantı Yöneticisi'ni yapılandırma** iletişim kutusu, tıklatın **Tamam** tooreturn toohello **ADO.NET Kaynak Düzenleyici**.</span><span class="sxs-lookup"><span data-stu-id="32a03-182">In hello **Configure ADO.NET Connection Manager** dialog box, click **OK** tooreturn toohello **ADO.NET Source Editor**.</span></span>
6. <span data-ttu-id="32a03-183">Merhaba, **ADO.NET Kaynak Düzenleyici**, hello içinde **Merhaba tablonun veya hello Görünüm adı** listesi, select hello **Sales.SalesOrderDetail** tablo.</span><span class="sxs-lookup"><span data-stu-id="32a03-183">In hello **ADO.NET Source Editor**, in hello **Name of hello table or hello view** list, select hello **Sales.SalesOrderDetail** table.</span></span>
   
    ![][07]
7. <span data-ttu-id="32a03-184">Tıklatın **Önizleme** toosee hello hello hello kaynak tablodaki veri ilk 200 satırı **Önizleme sorgu sonuçları** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="32a03-184">Click **Preview** toosee hello first 200 rows of data in hello source table in hello **Preview Query Results** dialog box.</span></span>
   
    ![][08]
8. <span data-ttu-id="32a03-185">Merhaba, **Önizleme sorgu sonuçları** iletişim kutusu, tıklatın **Kapat** tooreturn toohello **ADO.NET Kaynak Düzenleyici**.</span><span class="sxs-lookup"><span data-stu-id="32a03-185">In hello **Preview Query Results** dialog box, click **Close** tooreturn toohello **ADO.NET Source Editor**.</span></span>
9. <span data-ttu-id="32a03-186">Merhaba, **ADO.NET Kaynak Düzenleyici**, tıklatın **Tamam** toofinish hello veri kaynağını yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="32a03-186">In hello **ADO.NET Source Editor**, click **OK** toofinish configuring hello data source.</span></span>

## <a name="step-4-connect-hello-source-adapter-toohello-destination-adapter"></a><span data-ttu-id="32a03-187">4. adım: hello kaynak bağdaştırıcısı toohello hedef bağdaştırıcı bağlanma</span><span class="sxs-lookup"><span data-stu-id="32a03-187">Step 4: Connect hello source adapter toohello destination adapter</span></span>
1. <span data-ttu-id="32a03-188">Merhaba kaynak hello tasarım yüzeyi bağdaştırıcısında seçin.</span><span class="sxs-lookup"><span data-stu-id="32a03-188">Select hello source adapter on hello design surface.</span></span>
2. <span data-ttu-id="32a03-189">Merhaba kaynağı bağdaştırıcısından genişletir hello mavi oku seçin ve yerine tutturur kadar toohello hedef Düzenleyicisi sürükleyin.</span><span class="sxs-lookup"><span data-stu-id="32a03-189">Select hello blue arrow that extends from hello source adapter and drag it toohello destination editor until it snaps into place.</span></span>
   
    ![][10]
   
    <span data-ttu-id="32a03-190">Tipik bir SSIS paketi diğer bileşenlerini hello SSIS araç hello kaynak ve hedef toorestructure Merhaba, dönüştürme arasında bir sayı kullanın ve hello SSIS veri akışı geçerken verilerinizi temizler.</span><span class="sxs-lookup"><span data-stu-id="32a03-190">In a typical SSIS package, you use a number of other components from hello SSIS Toolbox in between hello source and hello destination toorestructure, transform, and cleanse your data as it passes through hello SSIS data flow.</span></span> <span data-ttu-id="32a03-191">tookeep kadar basit Bu örnekte, biz bağlandığınız hello kaynak doğrudan toohello hedef.</span><span class="sxs-lookup"><span data-stu-id="32a03-191">tookeep this example as simple as possible, we’re connecting hello source directly toohello destination.</span></span>

## <a name="step-5-configure-hello-destination-adapter"></a><span data-ttu-id="32a03-192">5. adım: hello hedef bağdaştırıcısını yapılandırın</span><span class="sxs-lookup"><span data-stu-id="32a03-192">Step 5: Configure hello destination adapter</span></span>
1. <span data-ttu-id="32a03-193">Merhaba hedef bağdaştırıcı tooopen hello çift **ADO.NET hedef Düzenleyicisi**.</span><span class="sxs-lookup"><span data-stu-id="32a03-193">Double-click hello destination adapter tooopen hello **ADO.NET Destination Editor**.</span></span>
   
    ![][11]
2. <span data-ttu-id="32a03-194">Merhaba üzerinde **Bağlantı Yöneticisi** hello sekmesinde **ADO.NET hedef Düzenleyicisi**, hello tıklatın **yeni** düğmesine bir sonraki toohello **Bağlantı Yöneticisi**listesi tooopen hello **ADO.NET Bağlantı Yöneticisi'ni yapılandırma** iletişim kutusuna ve bu öğreticinin veri yükler hello Azure SQL veri ambarı veritabanı için bağlantı ayarlarını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="32a03-194">On hello **Connection Manager** tab of hello **ADO.NET Destination Editor**, click hello **New** button next toohello **Connection manager** list tooopen hello **Configure ADO.NET Connection Manager** dialog box and create connection settings for hello Azure SQL Data Warehouse database into which this tutorial loads data.</span></span>
3. <span data-ttu-id="32a03-195">Merhaba, **ADO.NET Bağlantı Yöneticisi'ni yapılandırmak** iletişim kutusunda, hello **yeni** düğmesi tooopen hello **Bağlantı Yöneticisi** iletişim kutusuna ve yeni bir veri bağlantısı oluştur.</span><span class="sxs-lookup"><span data-stu-id="32a03-195">In hello **Configure ADO.NET Connection Manager** dialog box, click hello **New** button tooopen hello **Connection Manager** dialog box and create a new data connection.</span></span>
4. <span data-ttu-id="32a03-196">Merhaba, **Bağlantı Yöneticisi** iletişim kutusunda, öğeleri hello.</span><span class="sxs-lookup"><span data-stu-id="32a03-196">In hello **Connection Manager** dialog box, do hello following things.</span></span>
   1. <span data-ttu-id="32a03-197">İçin **sağlayıcısı**, hello SqlClient veri sağlayıcısı seçin.</span><span class="sxs-lookup"><span data-stu-id="32a03-197">For **Provider**, select hello SqlClient Data Provider.</span></span>
   2. <span data-ttu-id="32a03-198">İçin **sunucu adı**, hello SQL veri ambarı adını girin.</span><span class="sxs-lookup"><span data-stu-id="32a03-198">For **Server name**, enter hello SQL Data Warehouse name.</span></span>
   3. <span data-ttu-id="32a03-199">Merhaba, **toohello sunucuda oturum** bölümünde, select **kullanım SQL Server kimlik doğrulaması** ve kimlik doğrulama bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="32a03-199">In hello **Log on toohello server** section, select **Use SQL Server authentication** and enter authentication information.</span></span>
   4. <span data-ttu-id="32a03-200">Merhaba, **Bağlan tooa veritabanı** bölümünde, var olan bir SQL veri ambarı veritabanını seçin.</span><span class="sxs-lookup"><span data-stu-id="32a03-200">In hello **Connect tooa database** section, select an existing SQL Data Warehouse database.</span></span>
   5. <span data-ttu-id="32a03-201">Tıklatın **Bağlantıyı Sına**.</span><span class="sxs-lookup"><span data-stu-id="32a03-201">Click **Test Connection**.</span></span>
   6. <span data-ttu-id="32a03-202">Merhaba hello bağlantı testi sonuçlarını raporlar hello iletişim kutusunda, tıklatın **Tamam** tooreturn toohello **Bağlantı Yöneticisi** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="32a03-202">In hello dialog box that reports hello results of hello connection test, click **OK** tooreturn toohello **Connection Manager** dialog box.</span></span>
   7. <span data-ttu-id="32a03-203">Merhaba, **Bağlantı Yöneticisi** iletişim kutusu, tıklatın **Tamam** tooreturn toohello **ADO.NET Bağlantı Yöneticisi'ni yapılandırma** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="32a03-203">In hello **Connection Manager** dialog box, click **OK** tooreturn toohello **Configure ADO.NET Connection Manager** dialog box.</span></span>
5. <span data-ttu-id="32a03-204">Merhaba, **ADO.NET Bağlantı Yöneticisi'ni yapılandırma** iletişim kutusu, tıklatın **Tamam** tooreturn toohello **ADO.NET hedef Düzenleyicisi**.</span><span class="sxs-lookup"><span data-stu-id="32a03-204">In hello **Configure ADO.NET Connection Manager** dialog box, click **OK** tooreturn toohello **ADO.NET Destination Editor**.</span></span>
6. <span data-ttu-id="32a03-205">Merhaba, **ADO.NET hedef Düzenleyicisi**, tıklatın **yeni** sonraki toohello **tablo veya görünüm kullanın** listesi tooopen hello **Create Table** iletişim kutusu toocreate hello kaynak tablosu ile eşleşen bir sütun listesi ile yeni bir hedef tablo.</span><span class="sxs-lookup"><span data-stu-id="32a03-205">In hello **ADO.NET Destination Editor**, click **New** next toohello **Use a table or view** list tooopen hello **Create Table** dialog box toocreate a new destination table with a column list that matches hello source table.</span></span>
   
    ![][12a]
7. <span data-ttu-id="32a03-206">Merhaba, **Create Table** iletişim kutusunda, öğeleri hello.</span><span class="sxs-lookup"><span data-stu-id="32a03-206">In hello **Create Table** dialog box, do hello following things.</span></span>
   
   1. <span data-ttu-id="32a03-207">Merhaba hello hedef tablo adını da değiştirmem**satış siparişi ayrıntısını**.</span><span class="sxs-lookup"><span data-stu-id="32a03-207">Change hello name of hello destination table too**SalesOrderDetail**.</span></span>
   2. <span data-ttu-id="32a03-208">Merhaba kaldırmak **ROWGUID** sütun.</span><span class="sxs-lookup"><span data-stu-id="32a03-208">Remove hello **rowguid** column.</span></span> <span data-ttu-id="32a03-209">Merhaba **uniqueidentifier** veri türü, SQL veri ambarı'nda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="32a03-209">hello **uniqueidentifier** data type is not supported in SQL Data Warehouse.</span></span>
   3. <span data-ttu-id="32a03-210">Merhaba hello veri türünü değiştirmek **LineTotal** sütun çok**para**.</span><span class="sxs-lookup"><span data-stu-id="32a03-210">Change hello data type of hello **LineTotal** column too**money**.</span></span> <span data-ttu-id="32a03-211">Merhaba **ondalık** veri türü, SQL veri ambarı'nda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="32a03-211">hello **decimal** data type is not supported in SQL Data Warehouse.</span></span> <span data-ttu-id="32a03-212">Desteklenen veri türleri hakkında daha fazla bilgi için bkz: [CREATE TABLE (Azure SQL Data Warehouse, paralel veri ambarı)][CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)].</span><span class="sxs-lookup"><span data-stu-id="32a03-212">For info about supported data types, see [CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)][CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)].</span></span>
      
       ![][12b]
   4. <span data-ttu-id="32a03-213">Tıklatın **Tamam** toocreate hello tablo ve return toohello **ADO.NET hedef Düzenleyicisi**.</span><span class="sxs-lookup"><span data-stu-id="32a03-213">Click **OK** toocreate hello table and return toohello **ADO.NET Destination Editor**.</span></span>
8. <span data-ttu-id="32a03-214">Merhaba, **ADO.NET hedef Düzenleyicisi**seçin hello **eşlemeleri** toosee sekmesinde nasıl hello kaynağındaki sütunları hello hedef toocolumns eşlendi.</span><span class="sxs-lookup"><span data-stu-id="32a03-214">In hello **ADO.NET Destination Editor**, select hello **Mappings** tab toosee how columns in hello source are mapped toocolumns in hello destination.</span></span>
   
    ![][13]
9. <span data-ttu-id="32a03-215">Tıklatın **Tamam** toofinish hello veri kaynağını yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="32a03-215">Click **OK** toofinish configuring hello data source.</span></span>

## <a name="step-6-run-hello-package-tooload-hello-data"></a><span data-ttu-id="32a03-216">6. adım: hello paket tooload hello verileri çalıştırma</span><span class="sxs-lookup"><span data-stu-id="32a03-216">Step 6: Run hello package tooload hello data</span></span>
<span data-ttu-id="32a03-217">Merhaba tıklatarak çalışma hello paket **Başlat** düğmesi hello araç çubuğunda veya hello birini seçerek **çalıştırmak** hello seçenekleri **hata ayıklama** menüsü.</span><span class="sxs-lookup"><span data-stu-id="32a03-217">Run hello package by clicking hello **Start** button on hello toolbar or by selecting one of hello **Run** options on hello **Debug** menu.</span></span>

<span data-ttu-id="32a03-218">Merhaba paket toorun başladığında, o ana kadarki işlenen satır sayısı hello yanı sıra sarı dönen Tekerlek tooindicate etkinlik bakın.</span><span class="sxs-lookup"><span data-stu-id="32a03-218">As hello package begins toorun, you see yellow spinning wheels tooindicate activity as well as hello number of rows processed so far.</span></span>

![][14]

<span data-ttu-id="32a03-219">Merhaba paket çalışması sona erdiğinde, yeşil onay işareti tooindicate başarı bkz yanı sıra hello kaynak toohello hedef yüklenen veri satırı toplam sayısı hello.</span><span class="sxs-lookup"><span data-stu-id="32a03-219">When hello package has finished running, you see green check marks tooindicate success as well as hello total number of rows of data loaded from hello source toohello destination.</span></span>

![][15]

<span data-ttu-id="32a03-220">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="32a03-220">Congratulations!</span></span> <span data-ttu-id="32a03-221">SQL Server Integration Services tooload verileri Azure SQL Data Warehouse'a başarıyla kullandığınız.</span><span class="sxs-lookup"><span data-stu-id="32a03-221">You’ve successfully used SQL Server Integration Services tooload data into Azure SQL Data Warehouse.</span></span>

## <a name="next-steps"></a><span data-ttu-id="32a03-222">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="32a03-222">Next steps</span></span>
* <span data-ttu-id="32a03-223">Merhaba SSIS veri akışı hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="32a03-223">Learn more about hello SSIS data flow.</span></span> <span data-ttu-id="32a03-224">Buradan başlayın: [veri akışını][Data Flow].</span><span class="sxs-lookup"><span data-stu-id="32a03-224">Start here: [Data Flow][Data Flow].</span></span>
* <span data-ttu-id="32a03-225">Bilgi nasıl toodebug ve paketleri hak hello tasarım ortamında sorun giderme.</span><span class="sxs-lookup"><span data-stu-id="32a03-225">Learn how toodebug and troubleshoot your packages right in hello design environment.</span></span> <span data-ttu-id="32a03-226">Buradan başlayın: [paket geliştirme için sorun giderme araçları][Troubleshooting Tools for Package Development].</span><span class="sxs-lookup"><span data-stu-id="32a03-226">Start here: [Troubleshooting Tools for Package Development][Troubleshooting Tools for Package Development].</span></span>
* <span data-ttu-id="32a03-227">Nasıl toodeploy, SSIS projeleri ve paketleri öğrenin tooIntegration Hizmetleri sunucusu veya tooanother depolama konumu.</span><span class="sxs-lookup"><span data-stu-id="32a03-227">Learn how toodeploy your SSIS projects and packages tooIntegration Services Server or tooanother storage location.</span></span> <span data-ttu-id="32a03-228">Buradan başlayın: [, dağıtım projeleri ve paketleri][Deployment of Projects and Packages].</span><span class="sxs-lookup"><span data-stu-id="32a03-228">Start here: [Deployment of Projects and Packages][Deployment of Projects and Packages].</span></span>

<!-- Image references -->
[01]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ssis-designer-01.png
[02]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ssis-data-flow-task-02.png
[03]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-source-03.png
[04]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-connection-manager-04.png
[05]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-connection-05.png
[06]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/test-connection-06.png
[07]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-source-07.png
[08]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/preview-data-08.png
[09]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/source-destination-09.png
[10]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/connect-source-destination-10.png
[11]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-destination-11.png
[12a]: ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/destination-query-before-12a.png
[12b]: ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/destination-query-after-12b.png
[13]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/column-mapping-13.png
[14]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/package-running-14.png
[15]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/package-success-15.png

<!-- Article references -->

<!-- MSDN references -->
[PolyBase Guide]: https://msdn.microsoft.com/library/mt143171.aspx
[Download SQL Server Data Tools (SSDT)]: https://msdn.microsoft.com/library/mt204009.aspx
[CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)]: https://msdn.microsoft.com/library/mt203953.aspx
[Data Flow]: https://msdn.microsoft.com/library/ms140080.aspx
[Troubleshooting Tools for Package Development]: https://msdn.microsoft.com/library/ms137625.aspx
[Deployment of Projects and Packages]: https://msdn.microsoft.com/library/hh213290.aspx

<!--Other Web references-->
[Microsoft SQL Server 2016 Integration Services Feature Pack for Azure]: http://go.microsoft.com/fwlink/?LinkID=626967
[SQL Server Evaluations]: https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016
[Visual Studio Community]: https://www.visualstudio.com/en-us/products/visual-studio-community-vs.aspx
[AdventureWorks 2014 Sample Databases]: https://msftdbprodsamples.codeplex.com/releases/view/125550
