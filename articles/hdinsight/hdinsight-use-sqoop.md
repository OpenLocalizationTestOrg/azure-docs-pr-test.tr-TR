---
title: "Apache Sqoop aaaRun işleri Azure Hdınsight (Hadoop) ile | Microsoft Docs"
description: "Nasıl toouse Azure PowerShell bir iş istasyonu toorun Sqoop gelen içe ve dışa aktarma Hadoop kümesi ve bir Azure SQL veritabanı arasında bilgi edinin."
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
ms.assetid: 2fdcc6b7-6ad5-4397-a30b-e7e389b66c7a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: bdac507704937d77921c9c13d70aa2434c7e3be4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-sqoop-with-hadoop-in-hdinsight"></a><span data-ttu-id="ef8e1-103">Hdınsight'ta Hadoop ile Sqoop kullanma</span><span class="sxs-lookup"><span data-stu-id="ef8e1-103">Use Sqoop with Hadoop in HDInsight</span></span>
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="ef8e1-104">Bilgi nasıl toouse Sqoop Hdınsight tooimport ve Hdınsight kümesi ve Azure SQL database veya SQL Server veritabanı arasında verme.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-104">Learn how toouse Sqoop in HDInsight tooimport and export between HDInsight cluster and Azure SQL database or SQL Server database.</span></span>

<span data-ttu-id="ef8e1-105">Hadoop günlükleri ve dosyaları gibi yapılandırılmamış ve yarı yapılandırılmış veri işleme için doğal bir seçim olsa da olabilir ilişkisel veritabanlarında depolanan bir gereksinim tooprocess yapılandırılmış veri.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-105">Although Hadoop is a natural choice for processing unstructured and semistructured data, such as logs and files, there may also be a need tooprocess structured data that is stored in relational databases.</span></span>

<span data-ttu-id="ef8e1-106">[Sqoop] [ sqoop-user-guide-1.4.4] tasarlanmış aracı tootransfer Hadoop kümeleri ve ilişkisel veritabanları arasında verilerdir.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-106">[Sqoop][sqoop-user-guide-1.4.4] is a tool designed tootransfer data between Hadoop clusters and relational databases.</span></span> <span data-ttu-id="ef8e1-107">SQL Server, MySQL veya Oracle hello Hadoop dağıtılmış dosya sistemi (HDFS) içine dönüştürme hello verileri Hadoop ile MapReduce veya Hive ve uygulamasına geri hello verileri dışarı aktarma gibi bir ilişkisel veritabanı yönetim sistemine (RDBMS) tooimport verilerden kullanabilirsiniz bir RDBMS.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-107">You can use it tooimport data from a relational database management system (RDBMS) such as SQL Server, MySQL, or Oracle into hello Hadoop distributed file system (HDFS), transform hello data in Hadoop with MapReduce or Hive, and then export hello data back into an RDBMS.</span></span> <span data-ttu-id="ef8e1-108">Bu öğreticide, ilişkisel veritabanı için SQL Server veritabanını kullanıyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-108">In this tutorial, you are using a SQL Server database for your relational database.</span></span>

<span data-ttu-id="ef8e1-109">Hdınsight kümelerinde desteklenir Sqoop sürümleri için bkz: [Hdınsight tarafından sağlanan hello küme sürümlerindeki yenilikler nelerdir?][hdinsight-versions]</span><span class="sxs-lookup"><span data-stu-id="ef8e1-109">For Sqoop versions that are supported on HDInsight clusters, see [What's new in hello cluster versions provided by HDInsight?][hdinsight-versions]</span></span>

## <a name="understand-hello-scenario"></a><span data-ttu-id="ef8e1-110">Merhaba senaryo anlama</span><span class="sxs-lookup"><span data-stu-id="ef8e1-110">Understand hello scenario</span></span>

<span data-ttu-id="ef8e1-111">Hdınsight kümesi bazı örnek verilerle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-111">HDInsight cluster comes with some sample data.</span></span> <span data-ttu-id="ef8e1-112">Aşağıdaki iki örnek hello kullan:</span><span class="sxs-lookup"><span data-stu-id="ef8e1-112">You use hello following two samples:</span></span>

* <span data-ttu-id="ef8e1-113">Konumda bulunan bir log4j günlük dosyası */example/data/sample.log*.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-113">A log4j log file, which is located at */example/data/sample.log*.</span></span> <span data-ttu-id="ef8e1-114">günlükleri aşağıdaki hello hello dosyasından ayıklanan:</span><span class="sxs-lookup"><span data-stu-id="ef8e1-114">hello following logs are extracted from hello file:</span></span>
  
        2012-02-03 18:35:34 SampleClass6 [INFO] everything normal for id 577725851
        2012-02-03 18:35:34 SampleClass4 [FATAL] system problem at id 1991281254
        2012-02-03 18:35:34 SampleClass3 [DEBUG] detail for id 1304807656
        ...
* <span data-ttu-id="ef8e1-115">Adlı bir Hive tablosu *hivesampletable*, hangi başvuruları hello veri dosyası konumunda bulunan */hive/warehouse/hivesampletable*.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-115">A Hive table named *hivesampletable*, which references hello data file located at */hive/warehouse/hivesampletable*.</span></span> <span data-ttu-id="ef8e1-116">Merhaba tablo bazı mobil cihaz verileri içerir.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-116">hello table contains some mobile device data.</span></span> 
  
  | <span data-ttu-id="ef8e1-117">Alan</span><span class="sxs-lookup"><span data-stu-id="ef8e1-117">Field</span></span> | <span data-ttu-id="ef8e1-118">Veri türü</span><span class="sxs-lookup"><span data-stu-id="ef8e1-118">Data type</span></span> |
  | --- | --- |
  | <span data-ttu-id="ef8e1-119">istemci kimliği</span><span class="sxs-lookup"><span data-stu-id="ef8e1-119">clientid</span></span> |<span data-ttu-id="ef8e1-120">Dize</span><span class="sxs-lookup"><span data-stu-id="ef8e1-120">string</span></span> |
  | <span data-ttu-id="ef8e1-121">querytime</span><span class="sxs-lookup"><span data-stu-id="ef8e1-121">querytime</span></span> |<span data-ttu-id="ef8e1-122">Dize</span><span class="sxs-lookup"><span data-stu-id="ef8e1-122">string</span></span> |
  | <span data-ttu-id="ef8e1-123">Pazar</span><span class="sxs-lookup"><span data-stu-id="ef8e1-123">market</span></span> |<span data-ttu-id="ef8e1-124">Dize</span><span class="sxs-lookup"><span data-stu-id="ef8e1-124">string</span></span> |
  | <span data-ttu-id="ef8e1-125">deviceplatform</span><span class="sxs-lookup"><span data-stu-id="ef8e1-125">deviceplatform</span></span> |<span data-ttu-id="ef8e1-126">Dize</span><span class="sxs-lookup"><span data-stu-id="ef8e1-126">string</span></span> |
  | <span data-ttu-id="ef8e1-127">devicemake</span><span class="sxs-lookup"><span data-stu-id="ef8e1-127">devicemake</span></span> |<span data-ttu-id="ef8e1-128">Dize</span><span class="sxs-lookup"><span data-stu-id="ef8e1-128">string</span></span> |
  | <span data-ttu-id="ef8e1-129">devicemodel</span><span class="sxs-lookup"><span data-stu-id="ef8e1-129">devicemodel</span></span> |<span data-ttu-id="ef8e1-130">Dize</span><span class="sxs-lookup"><span data-stu-id="ef8e1-130">string</span></span> |
  | <span data-ttu-id="ef8e1-131">durum</span><span class="sxs-lookup"><span data-stu-id="ef8e1-131">state</span></span> |<span data-ttu-id="ef8e1-132">Dize</span><span class="sxs-lookup"><span data-stu-id="ef8e1-132">string</span></span> |
  | <span data-ttu-id="ef8e1-133">Ülke</span><span class="sxs-lookup"><span data-stu-id="ef8e1-133">country</span></span> |<span data-ttu-id="ef8e1-134">Dize</span><span class="sxs-lookup"><span data-stu-id="ef8e1-134">string</span></span> |
  | <span data-ttu-id="ef8e1-135">querydwelltime</span><span class="sxs-lookup"><span data-stu-id="ef8e1-135">querydwelltime</span></span> |<span data-ttu-id="ef8e1-136">Çift</span><span class="sxs-lookup"><span data-stu-id="ef8e1-136">double</span></span> |
  | <span data-ttu-id="ef8e1-137">SessionID</span><span class="sxs-lookup"><span data-stu-id="ef8e1-137">sessionid</span></span> |<span data-ttu-id="ef8e1-138">bigint</span><span class="sxs-lookup"><span data-stu-id="ef8e1-138">bigint</span></span> |
  | <span data-ttu-id="ef8e1-139">sessionpagevieworder</span><span class="sxs-lookup"><span data-stu-id="ef8e1-139">sessionpagevieworder</span></span> |<span data-ttu-id="ef8e1-140">bigint</span><span class="sxs-lookup"><span data-stu-id="ef8e1-140">bigint</span></span> |

<span data-ttu-id="ef8e1-141">İlk olarak, verdiğiniz *sample.log* ve *hivesampletable* toohello Azure SQL veritabanı veya tooSQL sunucu ve içeri aktarma hello hello mobil cihaz verileri içeren bir tabloda geri tooHDInsight hello kullanarak Aşağıdaki yolu:</span><span class="sxs-lookup"><span data-stu-id="ef8e1-141">First, you export *sample.log* and *hivesampletable* toohello Azure SQL database or tooSQL Server, and then import hello table that contains hello mobile device data back tooHDInsight by using hello following path:</span></span>

    /tutorials/usesqoop/importeddata

## <a name="create-cluster-and-sql-database"></a><span data-ttu-id="ef8e1-142">Küme ve SQL veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="ef8e1-142">Create cluster and SQL database</span></span>
<span data-ttu-id="ef8e1-143">Bu bölümde Azure portalı ve Azure Resource Manager şablonu nasıl toocreate bir küme, bir SQL veritabanı ve çalışan hello öğreticisi kullanma hello SQL veritabanı şemalarını hello gösterir.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-143">This section shows you how toocreate a cluster, a SQL Database, and hello SQL database schemas for running hello tutorial using hello Azure portal and an Azure Resource Manager template.</span></span> <span data-ttu-id="ef8e1-144">Merhaba şablonu bulunabilir [Azure hızlı başlangıç şablonlarını](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-sql-database/).</span><span class="sxs-lookup"><span data-stu-id="ef8e1-144">hello template can be found in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-sql-database/).</span></span> <span data-ttu-id="ef8e1-145">Merhaba Resource Manager şablonu bir bacpac paket toodeploy hello tablo şemalarını tooSQL veritabanı çağırır.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-145">hello Resource Manager template calls a bacpac package toodeploy hello table schemas tooSQL database.</span></span>  <span data-ttu-id="ef8e1-146">bir ortak blob kapsayıcısında, https://hditutorialdata.blob.core.windows.net/usesqoop/SqoopTutorial-2016-2-23-11-2.bacpac bulunan Hello bacpac paket.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-146">hello bacpac package is located in a public blob container, https://hditutorialdata.blob.core.windows.net/usesqoop/SqoopTutorial-2016-2-23-11-2.bacpac.</span></span> <span data-ttu-id="ef8e1-147">Merhaba bacpac dosyaları için özel bir kapsayıcı toouse istiyorsanız, değerleri hello şablonda aşağıdaki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="ef8e1-147">If you want toouse a private container for hello bacpac files, use hello following values in hello template:</span></span>
   
        "storageKeyType": "Primary",
        "storageKey": "<TheAzureStorageAccountKey>",

<span data-ttu-id="ef8e1-148">Toouse Azure PowerShell toocreate hello küme ve hello SQL veritabanı tercih ederseniz, bkz. [ek A](#appendix-a---a-powershell-sample).</span><span class="sxs-lookup"><span data-stu-id="ef8e1-148">If you prefer toouse Azure PowerShell toocreate hello cluster and hello SQL Database, see [Appendix A](#appendix-a---a-powershell-sample).</span></span>

1. <span data-ttu-id="ef8e1-149">Görüntü tooopen hello Azure portalında bir Resource Manager şablonu aşağıdaki hello'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-149">Click hello following image tooopen a Resource Manager template in hello Azure portal.</span></span>         
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-sql-database%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-use-sqoop/deploy-to-azure.png" alt="Deploy tooAzure"></a>
   

2. <span data-ttu-id="ef8e1-150">Aşağıdaki özelliklere hello girin:</span><span class="sxs-lookup"><span data-stu-id="ef8e1-150">Enter hello following properties:</span></span>

    - <span data-ttu-id="ef8e1-151">**Abonelik**: Azure aboneliğiniz girin.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-151">**Subscription**: Enter your Azure subscription.</span></span>
    - <span data-ttu-id="ef8e1-152">**Kaynak grubu**: yeni bir Azure kaynak grubu oluşturun veya varolan bir kaynak grubu seçin.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-152">**Resource Group**: Create a new Azure Resource Group, or select an existing Resource Group.</span></span>  <span data-ttu-id="ef8e1-153">Bir kaynak grubu yönetim amaçla ' dir.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-153">A Resource Group is for management purpose.</span></span>  <span data-ttu-id="ef8e1-154">Nesneler için bir kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-154">It is a container for objects.</span></span>
    - <span data-ttu-id="ef8e1-155">**Konum**: bir bölge seçin.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-155">**Location**: Select a region.</span></span>
    - <span data-ttu-id="ef8e1-156">**ClusterName**: Merhaba Hadoop kümesi için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-156">**ClusterName**: Enter a name for hello Hadoop cluster.</span></span>
    - <span data-ttu-id="ef8e1-157">**Küme oturum açma adı ve parola**: hello varsayılan oturum açma adıdır, yönetici</span><span class="sxs-lookup"><span data-stu-id="ef8e1-157">**Cluster login name and password**: hello default login name is admin.</span></span>
    - <span data-ttu-id="ef8e1-158">**SSH kullanıcı adı ve parola**.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-158">**SSH user name and password**.</span></span>
    - <span data-ttu-id="ef8e1-159">**SQL veritabanı sunucusu oturum açma adı ve parola**.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-159">**SQL database server login name and password**.</span></span>
    - <span data-ttu-id="ef8e1-160">**_artifacts konumu**: kendi backpac dosyayı farklı bir konumda toouse istemediğiniz sürece hello varsayılan değeri kullanın.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-160">**_artifacts Location**: Use hello default value unless you want toouse your own backpac file in a different location.</span></span>
    - <span data-ttu-id="ef8e1-161">**Konum Sas belirteci _artifacts**: boş bırakın.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-161">**_artifacts Location Sas Token**: Leave it blank.</span></span>
    - <span data-ttu-id="ef8e1-162">**Bacpac dosya adı**: kendi backpac dosya toouse istemediğiniz sürece hello varsayılan değeri kullanın.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-162">**Bacpac File Name**: Use hello default value unless you want toouse your own backpac file.</span></span>
     
     <span data-ttu-id="ef8e1-163">değerleri aşağıdaki hello sabit kodlanmış hello değişkenler bölümünde şunlardır:</span><span class="sxs-lookup"><span data-stu-id="ef8e1-163">hello following values are hardcoded in hello variables section:</span></span>
     
     | <span data-ttu-id="ef8e1-164">Varsayılan depolama hesabı adı</span><span class="sxs-lookup"><span data-stu-id="ef8e1-164">Default storage account name</span></span> | <span data-ttu-id="ef8e1-165"><CluterName>Depolama</span><span class="sxs-lookup"><span data-stu-id="ef8e1-165"><CluterName>store</span></span> |
     | --- | --- |
     | <span data-ttu-id="ef8e1-166">Azure SQL veritabanı sunucusu adı</span><span class="sxs-lookup"><span data-stu-id="ef8e1-166">Azure SQL database server name</span></span> |<span data-ttu-id="ef8e1-167"><ClusterName>dbserver</span><span class="sxs-lookup"><span data-stu-id="ef8e1-167"><ClusterName>dbserver</span></span> |
     | <span data-ttu-id="ef8e1-168">Azure SQL veritabanı adı</span><span class="sxs-lookup"><span data-stu-id="ef8e1-168">Azure SQL database name</span></span> |<span data-ttu-id="ef8e1-169"><ClusterName>DB</span><span class="sxs-lookup"><span data-stu-id="ef8e1-169"><ClusterName>db</span></span> |
     
     <span data-ttu-id="ef8e1-170">Lütfen bu değerleri yazın.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-170">Please write down these values.</span></span>  <span data-ttu-id="ef8e1-171">Bunları daha sonra hello öğreticide gerekir.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-171">You need them later in hello tutorial.</span></span>

<span data-ttu-id="ef8e1-172">3. tıklatın **Tamam** toosave hello parametreleri.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-172">3.Click **OK** toosave hello parameters.</span></span>

<span data-ttu-id="ef8e1-173">4 gelen hello **özel dağıtım** dikey penceresinde tıklatın **kaynak grubu** açılır kutusuna ve ardından **yeni** toocreate yeni bir kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-173">4.From hello **Custom deployment** blade, click **Resource group** dropdown box, and then click **New** toocreate a new resource group.</span></span> <span data-ttu-id="ef8e1-174">Merhaba kaynak grubu hello küme, hello bağımlı depolama hesabı ve diğer bağlı kaynağı gruplandıran bir kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-174">hello resource group is a container that groups hello cluster, hello dependent storage account and other linked resource.</span></span>

<span data-ttu-id="ef8e1-175">5. **Yasal koşullar**’a ve ardından **Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-175">5.Click **Legal terms**, and then click **Create**.</span></span>

<span data-ttu-id="ef8e1-176">6. **Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-176">6.Click **Create**.</span></span> <span data-ttu-id="ef8e1-177">Şablon dağıtımı için dağıtım gönderme başlıklı yeni bir kutucuk görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-177">You see a new tile titled Submitting deployment for Template deployment.</span></span> <span data-ttu-id="ef8e1-178">Yaklaşık 20 dakika toocreate hello küme ve SQL veritabanı hakkında alır.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-178">It takes about around 20 minutes toocreate hello cluster and SQL database.</span></span>

<span data-ttu-id="ef8e1-179">Toouse mevcut Azure SQL veritabanını veya Microsoft SQL Server'ı seçerseniz</span><span class="sxs-lookup"><span data-stu-id="ef8e1-179">If you choose toouse existing Azure SQL database or Microsoft SQL Server</span></span>

* <span data-ttu-id="ef8e1-180">**Azure SQL veritabanı**: istasyonunuzdan hello Azure SQL veritabanı sunucusu tooallow erişimi için bir güvenlik duvarı kuralı yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-180">**Azure SQL database**: You must configure a firewall rule for hello Azure SQL database server tooallow access from your workstation.</span></span> <span data-ttu-id="ef8e1-181">Bir Azure SQL veritabanı oluşturma ve hello güvenlik duvarını yapılandırma hakkında yönergeler için bkz: [Azure SQL veritabanını kullanmaya başlama][sqldatabase-get-started].</span><span class="sxs-lookup"><span data-stu-id="ef8e1-181">For instructions about creating an Azure SQL database and configuring hello firewall, see [Get started using Azure SQL database][sqldatabase-get-started].</span></span> 
  
  > [!NOTE]
  > <span data-ttu-id="ef8e1-182">Varsayılan olarak Azure SQL veritabanını Azure Hdınsight gibi Azure hizmetlerden bağlantılara izin verir.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-182">By default an Azure SQL database allows connections from Azure services, such as Azure HDInsight.</span></span> <span data-ttu-id="ef8e1-183">Bu güvenlik duvarı ayarı devre dışıysa, tooenable gereken hello Azure portalı şuradan.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-183">If this firewall setting is disabled, you need tooenable it from hello Azure portal.</span></span> <span data-ttu-id="ef8e1-184">Bir Azure SQL veritabanı oluşturma ve güvenlik duvarı kuralları yapılandırma hakkında daha fazla yönerge için bkz: [oluşturma ve yapılandırma SQL veritabanı][sqldatabase-create-configue].</span><span class="sxs-lookup"><span data-stu-id="ef8e1-184">For instruction about creating an Azure SQL database and configuring firewall rules, see [Create and Configure SQL Database][sqldatabase-create-configue].</span></span>
  > 
  > 
* <span data-ttu-id="ef8e1-185">**SQL Server**: Hdınsight kümenize hello üzerinde ise, aynı sanal ağ Azure SQL sunucusu olarak, bu makale tooimport ve dışarı aktarma veri tooa SQL Server veritabanında hello adımları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-185">**SQL Server**: If your HDInsight cluster is on hello same virtual network in Azure as SQL Server, you can use hello steps in this article tooimport and export data tooa SQL Server database.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="ef8e1-186">Hdınsight yalnızca konum tabanlı sanal ağları destekler ve benzeşim grubu tabanlı sanal ağlar ile şu anda çalışmıyor.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-186">HDInsight supports only location-based virtual networks, and it does not currently work with affinity group-based virtual networks.</span></span>
  > 
  > 
  
  * <span data-ttu-id="ef8e1-187">toocreate ve sanal ağ yapılandırma, bkz: [hello Azure portal kullanarak bir sanal ağ oluşturma](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="ef8e1-187">toocreate and configure a virtual network, see [Create a virtual network using hello Azure portal](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span></span>
    
    * <span data-ttu-id="ef8e1-188">SQL Server, veri merkezinizde kullanırken, hello sanal ağ olarak yapılandırmalısınız *siteden siteye* veya *noktadan siteye*.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-188">When you are using SQL Server in your datacenter, you must configure hello virtual network as *site-to-site* or *point-to-site*.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="ef8e1-189">İçin **noktası site** sanal ağlar, SQL Server çalıştırmalıdır hello VPN istemcisi hello kullanılabilir yapılandırma uygulama **Pano** Azure sanal ağı yapılandırmanızın.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-189">For **point-to-site** virtual networks, SQL Server must be running hello VPN client configuration application, which is available from hello **Dashboard** of your Azure virtual network configuration.</span></span>
      > 
      > 
    * <span data-ttu-id="ef8e1-190">Bir Azure sanal makinede SQL Server kullanırken SQL Server barındırma hello sanal makine hello üyesi ise herhangi bir sanal ağ yapılandırması kullanılabilir Hdınsight aynı sanal ağ.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-190">When you are using SQL Server on an Azure virtual machine, any virtual network configuration can be used if hello virtual machine hosting SQL Server is a member of hello same virtual network as HDInsight.</span></span>
  * <span data-ttu-id="ef8e1-191">toocreate bir sanal ağ Hdınsight kümesinde bkz [özel seçenekleri kullanarak Hdınsight'ta oluşturmak Hadoop kümeleri](hdinsight-hadoop-provision-linux-clusters.md)</span><span class="sxs-lookup"><span data-stu-id="ef8e1-191">toocreate an HDInsight cluster on a virtual network, see [Create Hadoop clusters in HDInsight using custom options](hdinsight-hadoop-provision-linux-clusters.md)</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="ef8e1-192">SQL Server kimlik doğrulaması da izin vermelidir.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-192">SQL Server must also allow authentication.</span></span> <span data-ttu-id="ef8e1-193">Bir SQL Server oturum açma toocomplete hello bu makaledeki adımları kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-193">You must use a SQL Server login toocomplete hello steps in this article.</span></span>
    > 
    > 

## <a name="run-sqoop-jobs"></a><span data-ttu-id="ef8e1-194">Sqoop işleri çalıştırma</span><span class="sxs-lookup"><span data-stu-id="ef8e1-194">Run Sqoop jobs</span></span>
<span data-ttu-id="ef8e1-195">Hdınsight Sqoop işleri çeşitli yöntemler kullanarak çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-195">HDInsight can run Sqoop jobs by using a variety of methods.</span></span> <span data-ttu-id="ef8e1-196">Hangi yöntemi sizin için uygun olan tablo toodecide aşağıdaki hello kullanın ve sonra kılavuz hello bağlantıyı izleyin.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-196">Use hello following table toodecide which method is right for you, then follow hello link for a walkthrough.</span></span>

| <span data-ttu-id="ef8e1-197">**Bu** isterseniz...</span><span class="sxs-lookup"><span data-stu-id="ef8e1-197">**Use this** if you want...</span></span> | <span data-ttu-id="ef8e1-198">.. .an **etkileşimli** Kabuk</span><span class="sxs-lookup"><span data-stu-id="ef8e1-198">...an **interactive** shell</span></span> | <span data-ttu-id="ef8e1-199">... **toplu** işleme</span><span class="sxs-lookup"><span data-stu-id="ef8e1-199">...**batch** processing</span></span> | <span data-ttu-id="ef8e1-200">.. hemen bu **küme işletim sistemi**</span><span class="sxs-lookup"><span data-stu-id="ef8e1-200">...with this **cluster operating system**</span></span> | <span data-ttu-id="ef8e1-201">.. .from bu **istemci işletim sistemi**</span><span class="sxs-lookup"><span data-stu-id="ef8e1-201">...from this **client operating system**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="ef8e1-202">SSH</span><span class="sxs-lookup"><span data-stu-id="ef8e1-202">SSH</span></span>](hdinsight-use-sqoop-mac-linux.md) |<span data-ttu-id="ef8e1-203">✔</span><span class="sxs-lookup"><span data-stu-id="ef8e1-203">✔</span></span> |<span data-ttu-id="ef8e1-204">✔</span><span class="sxs-lookup"><span data-stu-id="ef8e1-204">✔</span></span> |<span data-ttu-id="ef8e1-205">Linux</span><span class="sxs-lookup"><span data-stu-id="ef8e1-205">Linux</span></span> |<span data-ttu-id="ef8e1-206">Linux, UNIX, Mac OS X veya Windows</span><span class="sxs-lookup"><span data-stu-id="ef8e1-206">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="ef8e1-207">Hadoop için .NET SDK</span><span class="sxs-lookup"><span data-stu-id="ef8e1-207">.NET SDK for Hadoop</span></span>](hdinsight-hadoop-use-sqoop-dotnet-sdk.md) |&nbsp; |<span data-ttu-id="ef8e1-208">✔</span><span class="sxs-lookup"><span data-stu-id="ef8e1-208">✔</span></span> |<span data-ttu-id="ef8e1-209">Linux veya Windows</span><span class="sxs-lookup"><span data-stu-id="ef8e1-209">Linux or Windows</span></span> |<span data-ttu-id="ef8e1-210">Windows (için şimdi)</span><span class="sxs-lookup"><span data-stu-id="ef8e1-210">Windows (for now)</span></span> |
| [<span data-ttu-id="ef8e1-211">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="ef8e1-211">Azure PowerShell</span></span>](hdinsight-hadoop-use-sqoop-powershell.md) |&nbsp; |<span data-ttu-id="ef8e1-212">✔</span><span class="sxs-lookup"><span data-stu-id="ef8e1-212">✔</span></span> |<span data-ttu-id="ef8e1-213">Linux veya Windows</span><span class="sxs-lookup"><span data-stu-id="ef8e1-213">Linux or Windows</span></span> |<span data-ttu-id="ef8e1-214">Windows</span><span class="sxs-lookup"><span data-stu-id="ef8e1-214">Windows</span></span> |

## <a name="limitations"></a><span data-ttu-id="ef8e1-215">Sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="ef8e1-215">Limitations</span></span>
* <span data-ttu-id="ef8e1-216">Toplu export - ile Linux tabanlı Hdınsight, hello Sqoop kullanılan bağlayıcı tooexport veri tooMicrosoft SQL Server ya da Azure SQL veritabanı toplu eklemeler şu anda desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-216">Bulk export - With Linux-based HDInsight, hello Sqoop connector used tooexport data tooMicrosoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>
* <span data-ttu-id="ef8e1-217">-Hello kullanırken, Linux tabanlı Hdınsight ile toplu işleme `-batch` eklemeleri gerçekleştirirken geçiş, Sqoop gerçekleştirir hello INSERT işlemlerine toplu işleme yerine birden çok ekler.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-217">Batching - With Linux-based HDInsight, When using hello `-batch` switch when performing inserts, Sqoop performs multiple inserts instead of batching hello insert operations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ef8e1-218">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ef8e1-218">Next steps</span></span>
<span data-ttu-id="ef8e1-219">Öğrendiğiniz artık nasıl toouse Sqoop.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-219">Now you have learned how toouse Sqoop.</span></span> <span data-ttu-id="ef8e1-220">toolearn daha bakın:</span><span class="sxs-lookup"><span data-stu-id="ef8e1-220">toolearn more, see:</span></span>

* [<span data-ttu-id="ef8e1-221">HDInsight ile Hive kullanma</span><span class="sxs-lookup"><span data-stu-id="ef8e1-221">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="ef8e1-222">HDInsight ile Pig kullanma</span><span class="sxs-lookup"><span data-stu-id="ef8e1-222">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* <span data-ttu-id="ef8e1-223">[Hdınsight ile Oozie kullanma][hdinsight-use-oozie]: Oozie iş akışında kullanmak Sqoop eylem.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-223">[Use Oozie with HDInsight][hdinsight-use-oozie]: Use Sqoop action in an Oozie workflow.</span></span>
* <span data-ttu-id="ef8e1-224">[Hdınsight kullanarak uçuş gecikme verileri analiz][hdinsight-analyze-flight-data]: kullanmak Hive tooanalyze uçuş gecikme veri ve Sqoop tooexport veri tooan Azure SQL veritabanını kullanın.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-224">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-data]: Use Hive tooanalyze flight delay data, and then use Sqoop tooexport data tooan Azure SQL database.</span></span>
* <span data-ttu-id="ef8e1-225">[Veri tooHDInsight karşıya][hdinsight-upload-data]: veri tooHDInsight/Azure Blob Depolama yüklemek için diğer yöntemler bulun.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-225">[Upload data tooHDInsight][hdinsight-upload-data]: Find other methods for uploading data tooHDInsight/Azure Blob storage.</span></span>

## <a name="appendix-a---a-powershell-sample"></a><span data-ttu-id="ef8e1-226">Ek A - PowerShell örnek</span><span class="sxs-lookup"><span data-stu-id="ef8e1-226">Appendix A - a PowerShell sample</span></span>
<span data-ttu-id="ef8e1-227">Merhaba PowerShell örnek hello aşağıdaki adımları gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="ef8e1-227">hello PowerShell sample performs hello following steps:</span></span>

1. <span data-ttu-id="ef8e1-228">TooAzure bağlanın.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-228">Connect tooAzure.</span></span>
2. <span data-ttu-id="ef8e1-229">Bir Azure kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-229">Create an Azure resource group.</span></span> <span data-ttu-id="ef8e1-230">Daha fazla bilgi için bkz: [Azure PowerShell'i Azure Resource Manager ile kullanma](../powershell-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="ef8e1-230">For more information, see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md)</span></span>
3. <span data-ttu-id="ef8e1-231">Bir Azure SQL veritabanı sunucusu, Azure SQL veritabanına ve iki tablo oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-231">Create an Azure SQL Database server, an Azure SQL database, and two tables.</span></span> 
   
    <span data-ttu-id="ef8e1-232">Bunun yerine SQL Server kullanıyorsanız, aşağıdaki deyimleri toocreate hello tabloları hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="ef8e1-232">If you use SQL Server instead, use hello following statements toocreate hello tables:</span></span>
   
        CREATE TABLE [dbo].[log4jlogs](
         [t1] [nvarchar](50),
         [t2] [nvarchar](50),
         [t3] [nvarchar](50),
         [t4] [nvarchar](50),
         [t5] [nvarchar](50),
         [t6] [nvarchar](50),
         [t7] [nvarchar](50))
   
        CREATE TABLE [dbo].[mobiledata](
         [clientid] [nvarchar](50),
         [querytime] [nvarchar](50),
         [market] [nvarchar](50),
         [deviceplatform] [nvarchar](50),
         [devicemake] [nvarchar](50),
         [devicemodel] [nvarchar](50),
         [state] [nvarchar](50),
         [country] [nvarchar](50),
         [querydwelltime] [float],
         [sessionid] [bigint],
         [sessionpagevieworder][bigint])
   
    <span data-ttu-id="ef8e1-233">Merhaba en kolay yolu tooexamine hello veritabanını ve tabloları toouse Visual Studio olur.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-233">hello easiest way tooexamine hello database and tables is toouse Visual Studio.</span></span> <span data-ttu-id="ef8e1-234">Merhaba veritabanı sunucusu ve hello veritabanı hello Azure portal kullanarak incelenebilir.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-234">hello database server and hello database can be examined using hello Azure portal.</span></span>
4. <span data-ttu-id="ef8e1-235">Hdınsight kümesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-235">Create an HDInsight cluster.</span></span>
   
    <span data-ttu-id="ef8e1-236">tooexamine hello küme hello Azure portalında veya Azure PowerShell'i kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-236">tooexamine hello cluster, you can use hello Azure portal or Azure PowerShell.</span></span>
5. <span data-ttu-id="ef8e1-237">Merhaba kaynak veri dosyası önceden işleyebilir.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-237">Pre-process hello source data file.</span></span>
   
    <span data-ttu-id="ef8e1-238">Bu öğreticide, log4j günlük dosyası (ayrılmış bir dosya) ve bir Hive tablosu tooan Azure SQL veritabanı verin.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-238">In this tutorial, you export a log4j log file (a delimited file) and a Hive table tooan Azure SQL database.</span></span> <span data-ttu-id="ef8e1-239">Merhaba sınırlanmış dosya olarak adlandırılır */example/data/sample.log*.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-239">hello delimited file is called */example/data/sample.log*.</span></span> <span data-ttu-id="ef8e1-240">Öğreticide daha önce Merhaba, log4j günlükler bazı örnekler gördünüz.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-240">Earlier in hello tutorial, you saw a few samples of log4j logs.</span></span> <span data-ttu-id="ef8e1-241">Merhaba günlük dosyasında bazı boş satırlar ve bazı satırlar benzer toothese vardır:</span><span class="sxs-lookup"><span data-stu-id="ef8e1-241">In hello log file, there are some empty lines and some lines similar toothese:</span></span>
   
        java.lang.Exception: 2012-02-03 20:11:35 SampleClass2 [FATAL] unrecoverable system problem at id 609774657
            at com.osa.mocklogger.MockLogger$2.run(MockLogger.java:83)
   
    <span data-ttu-id="ef8e1-242">Bu verileri kullanan diğer örnekler için ince budur ancak biz hello Azure SQL database veya SQL Server içeri aktarmadan önce bu özel durumlar kaldırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-242">This is fine for other examples that use this data, but we must remove these exceptions before we can import into hello Azure SQL database or SQL Server.</span></span> <span data-ttu-id="ef8e1-243">Sqoop verme başarısız boş bir dize veya daha az sayıda satırıyla ise hello Azure SQL veritabanı tablosunda tanımlı alanları hello sayısından öğeleri.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-243">Sqoop export  fails if there is an empty string or a line with a fewer elements than hello number of fields defined in hello Azure SQL database table.</span></span> <span data-ttu-id="ef8e1-244">Merhaba log4jlogs Tablo 7 dize türü alan yok.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-244">hello log4jlogs table has 7 string-type fields.</span></span>
   
    <span data-ttu-id="ef8e1-245">Bu yordamı hello kümesinde yeni bir dosya oluşturur: tutorials/usesqoop/data/sample.log.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-245">This procedure creates a new file on hello cluster: tutorials/usesqoop/data/sample.log.</span></span> <span data-ttu-id="ef8e1-246">tooexamine hello değiştirilmiş veri dosyası, hello Azure portal, Azure Storage Gezgini aracını veya Azure PowerShell kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-246">tooexamine hello modified data file, you can use hello Azure portal, an Azure Storage explorer tool, or Azure PowerShell.</span></span> <span data-ttu-id="ef8e1-247">[Hdınsight kullanmaya başlama] [ hdinsight-get-started] hello dosya içeriği görüntülemek ve örnek Azure PowerShell toodownload bir dosyayı kullanmak için bir kod sahiptir.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-247">[Get started with HDInsight][hdinsight-get-started] has a code sample for using Azure PowerShell toodownload a file and display hello file content.</span></span>
6. <span data-ttu-id="ef8e1-248">Bir veri dosyası toohello Azure SQL veritabanına verin.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-248">Export a data file toohello Azure SQL database.</span></span>
   
    <span data-ttu-id="ef8e1-249">Merhaba kaynak tutorials/usesqoop/data/sample.log dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-249">hello source file is tutorials/usesqoop/data/sample.log.</span></span> <span data-ttu-id="ef8e1-250">Merhaba veri dışa aktarılan toois nerede hello tablo log4jlogs çağrılır.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-250">hello table where hello data is exported toois called log4jlogs.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="ef8e1-251">Dışında bir bağlantı dizesi bilgisi, SQL Server veya bir Azure SQL veritabanı için bu bölümdeki hello adımları çalışması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-251">Other than connection string information, hello steps in this section should work for an Azure SQL database or for SQL Server.</span></span> <span data-ttu-id="ef8e1-252">Bu adımları yapılandırma aşağıdaki hello kullanarak test edilmiş:</span><span class="sxs-lookup"><span data-stu-id="ef8e1-252">These steps were tested by using hello following configuration:</span></span>
   > 
   > * <span data-ttu-id="ef8e1-253">**Azure sanal ağı noktadan siteye Yapılandırması**: bir sanal ağa bağlı özel bir veri merkezinde hello Hdınsight küme tooa SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-253">**Azure virtual network point-to-site configuration**: A virtual network connected hello HDInsight cluster tooa SQL Server in a private datacenter.</span></span> <span data-ttu-id="ef8e1-254">Bkz: [noktadan siteye VPN hello Yönetim Portalı yapılandırma](../vpn-gateway/vpn-gateway-point-to-site-create.md) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-254">See [Configure a Point-to-Site VPN in hello Management Portal](../vpn-gateway/vpn-gateway-point-to-site-create.md) for more information.</span></span>
   > * <span data-ttu-id="ef8e1-255">**Azure Hdınsight 3.1**: bkz [özel seçenekleri kullanarak Hdınsight'ta oluşturmak Hadoop kümeleri](hdinsight-hadoop-provision-linux-clusters.md) bir küme üzerinde bir sanal ağ oluşturma hakkında daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-255">**Azure HDInsight 3.1**: See [Create Hadoop clusters in HDInsight using custom options](hdinsight-hadoop-provision-linux-clusters.md) for information about creating a cluster on a virtual network.</span></span>
   > * <span data-ttu-id="ef8e1-256">**SQL Server 2014**: tooallow kimlik doğrulaması ve çalışan hello VPN istemci yapılandırma paketi tooconnect güvenli bir şekilde yapılandırılmış toohello sanal ağ.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-256">**SQL Server 2014**: Configured tooallow authentication and running hello VPN client configuration package tooconnect securely toohello virtual network.</span></span>
   > 
   > 
7. <span data-ttu-id="ef8e1-257">Bir Hive tablosu toohello Azure SQL veritabanı dışarı aktarın.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-257">Export a Hive table toohello Azure SQL database.</span></span>
8. <span data-ttu-id="ef8e1-258">Merhaba mobiledata tablo toohello Hdınsight kümesi içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-258">Import hello mobiledata table toohello HDInsight cluster.</span></span>
   
    <span data-ttu-id="ef8e1-259">tooexamine hello değiştirilmiş veri dosyası, hello Azure portal, Azure Storage Gezgini aracını veya Azure PowerShell kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-259">tooexamine hello modified data file, you can use hello Azure portal, an Azure Storage explorer tool, or Azure PowerShell.</span></span>  <span data-ttu-id="ef8e1-260">[Hdınsight kullanmaya başlama] [ hdinsight-get-started] hello dosya içeriği görüntülemek ve Azure PowerShell toodownload bir dosyayı kullanma hakkında örnek koduna sahip.</span><span class="sxs-lookup"><span data-stu-id="ef8e1-260">[Get started with HDInsight][hdinsight-get-started] has a code sample about using Azure PowerShell toodownload a file and display hello file content.</span></span>

### <a name="hello-powershell-sample"></a><span data-ttu-id="ef8e1-261">Merhaba PowerShell örnek</span><span class="sxs-lookup"><span data-stu-id="ef8e1-261">hello PowerShell sample</span></span>
    # Prepare an Azure SQL database toobe used by hello Sqoop tutorial

    #region - provide hello following values

    $subscriptionID = "<Enter your Azure Subscription ID>"

    $sqlDatabaseLogin = "<Enter a SQL Database Login name>" #SQL Database server login
    $sqlDatabasePassword = "<Enter a Password>"

    $httpUserName = "admin"  #HDInsight cluster username
    $httpPassword = "<Enter a Password>"

    # used for creating Azure service names
    $nameToken = "<Enter an alias>" 
    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")
    #endregion

    #region - variables

    # Resource group variables
    $resourceGroupName = $namePrefix + "rg"
    $location = "East US 2" # used by all Azure services defined in this tutorial

    # SQL database varialbes
    $sqlDatabaseServerName = $namePrefix + "sqldbserver"
    $sqlDatabaseName = $namePrefix + "sqldb"
    $sqlDatabaseConnectionString = "Data Source=$sqlDatabaseServerName.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabasePassword;Encrypt=true;Trusted_Connection=false;"
    $sqlDatabaseMaxSizeGB = 10

    # Used for retrieving external IP address and creating firewall rules
    $ipAddressRestService = "http://bot.whatismyipaddress.com"
    $fireWallRuleName = "UseSqoop"

    # Used for creating tables and clustered indexes
    $cmdCreateLog4jTable = "CREATE TABLE [dbo].[log4jlogs](
        [t1] [nvarchar](50),
        [t2] [nvarchar](50),
        [t3] [nvarchar](50),
        [t4] [nvarchar](50),
        [t5] [nvarchar](50),
        [t6] [nvarchar](50),
        [t7] [nvarchar](50))"

    $cmdCreateLog4jClusteredIndex = "CREATE CLUSTERED INDEX log4jlogs_clustered_index on log4jlogs(t1)"

    $cmdCreateMobileTable = " CREATE TABLE [dbo].[mobiledata](
    [clientid] [nvarchar](50),
    [querytime] [nvarchar](50),
    [market] [nvarchar](50),
    [deviceplatform] [nvarchar](50),
    [devicemake] [nvarchar](50),
    [devicemodel] [nvarchar](50),
    [state] [nvarchar](50),
    [country] [nvarchar](50),
    [querydwelltime] [float],
    [sessionid] [bigint],
    [sessionpagevieworder][bigint])"

    $cmdCreateMobileDataClusteredIndex = "CREATE CLUSTERED INDEX mobiledata_clustered_index on mobiledata(clientid)"

    # HDInsight variables
    $hdinsightClusterName = $namePrefix + "hdi"
    $defaultStorageAccountName = $namePrefix + "store"
    $defaultBlobContainerName = $hdinsightClusterName
    #endregion

    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    #region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #endregion

    #region - Create Azure resouce group
    Write-Host "`nCreating an Azure resource group ..." -ForegroundColor Green
    try{
        Get-AzureRmResourceGroup -Name $resourceGroupName
    }
    catch{
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
    }
    #endregion

    #region - Create Azure SQL database server
    Write-Host "`nCreating an Azure SQL Database server ..." -ForegroundColor Green
    try{
        Get-AzureRmSqlServer -ServerName $sqlDatabaseServerName -ResourceGroupName $resourceGroupName}
    catch{
        Write-Host "`nCreating SQL Database server ..."  -ForegroundColor Green

        $sqlDatabasePW = ConvertTo-SecureString -String $sqlDatabasePassword -AsPlainText -Force
        $credential = New-Object System.Management.Automation.PSCredential($sqlDatabaseLogin,$sqlDatabasePW)

        $sqlDatabaseServerName = (New-AzureRmSqlServer `
                                    -ResourceGroupName $resourceGroupName `
                                    -ServerName $sqlDatabaseServerName `
                                    -SqlAdministratorCredentials $credential `
                                    -Location $location).ServerName
        Write-Host "`tThe new SQL database server name is $sqlDatabaseServerName." -ForegroundColor Cyan

        Write-Host "`nCreating firewall rule, $fireWallRuleName ..." -ForegroundColor Green
        $workstationIPAddress = Invoke-RestMethod $ipAddressRestService
        New-AzureRmSqlServerFirewallRule `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -FirewallRuleName "$fireWallRuleName-workstation" `
            -StartIpAddress $workstationIPAddress `
            -EndIpAddress $workstationIPAddress

        #tooallow other Azure services tooaccess hello server add a firewall rule and set both hello StartIpAddress and EndIpAddress too0.0.0.0. 
        #Note that this allows Azure traffic from any Azure subscription tooaccess hello server.
        New-AzureRmSqlServerFirewallRule `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -FirewallRuleName "$fireWallRuleName-Azureservices" `
            -StartIpAddress "0.0.0.0" `
            -EndIpAddress "0.0.0.0"
    }

    #endregion

    #region - Create and validate Azure SQL database
    Write-Host "`nCreating an Azure SQL database ..." -ForegroundColor Green

    try {
        Get-AzureRmSqlDatabase `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -DatabaseName $sqlDatabaseName
    }
    catch {
        Write-Host "`nCreating SQL Database, $sqlDatabaseName ..."  -ForegroundColor Green
        New-AzureRMSqlDatabase `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -DatabaseName $sqlDatabaseName `
            -Edition "Standard" `
            -RequestedServiceObjectiveName "S1"
    }

    #endregion

    #region - Create tables
    Write-Host "Creating hello log4jlogs table and hello mobiledata table ..." -ForegroundColor Green

    $conn = New-Object System.Data.SqlClient.SqlConnection
    $conn.ConnectionString = $sqlDatabaseConnectionString
    $conn.Open()

    # Create hello log4jlogs table and index
    $cmd = New-Object System.Data.SqlClient.SqlCommand
    $cmd.Connection = $conn
    $cmd.CommandText = $cmdCreateLog4jTable
    $ret = $cmd.ExecuteNonQuery()
    $cmd.CommandText = $cmdCreateLog4jClusteredIndex
    $cmd.ExecuteNonQuery()

    # Create hello mobiledata table and index
    $cmd.CommandText = $cmdCreateMobileTable
    $cmd.ExecuteNonQuery()
    $cmd.CommandText = $cmdCreateMobileDataClusteredIndex
    $cmd.ExecuteNonQuery()

    $conn.close()

    #endregion


    #region - Create HDInsight cluster

    Write-Host "Creating hello HDInsight cluster and hello dependent services ..." -ForegroundColor Green

    # Create hello default storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $defaultStorageAccountName `
        -Location $location `
        -Type Standard_LRS

    # Create hello default Blob container
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                    -ResourceGroupName $resourceGroupName `
                                    -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext `
                                        -StorageAccountName $defaultStorageAccountName `
                                        -StorageAccountKey $defaultStorageAccountKey 
    New-AzureStorageContainer `
        -Name $defaultBlobContainerName `
        -Context $defaultStorageAccountContext 

    # Create hello HDInsight cluster
    $pw = ConvertTo-SecureString -String $httpPassword -AsPlainText -Force
    $httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$pw)

    New-AzureRmHDInsightCluster `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $HDInsightClusterName `
        -Location $location `
        -ClusterType Hadoop `
        -OSType Windows `
        -ClusterSizeInNodes 2 `
        -HttpCredential $httpCredential `
        -DefaultStorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultStorageContainer $defaultBlobContainerName 

    # Validate hello cluster
    Get-AzureRmHDInsightCluster -ClusterName $hdinsightClusterName
    #endregion

    #region - pre-process hello source file

    Write-Host "Preprocessing hello source file ..." -ForegroundColor Green

    # This procedure creates a new file with $destBlobName
    $sourceBlobName = "example/data/sample.log"
    $destBlobName = "tutorials/usesqoop/data/sample.log"

    # Define hello connection string
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$defaultStorageAccountName;AccountKey=$defaultStorageAccountKey"

    # Create block blob objects referencing hello source and destination blob.
    $storageAccount = [Microsoft.WindowsAzure.Storage.CloudStorageAccount]::Parse($storageConnectionString)
    $storageClient = $storageAccount.CreateCloudBlobClient();
    $storageContainer = $storageClient.GetContainerReference($defaultBlobContainerName)
    $sourceBlob = $storageContainer.GetBlockBlobReference($sourceBlobName)
    $destBlob = $storageContainer.GetBlockBlobReference($destBlobName)

    # Define a MemoryStream and a StreamReader for reading from hello source file
    $stream = New-Object System.IO.MemoryStream
    $stream = $sourceBlob.OpenRead()
    $sReader = New-Object System.IO.StreamReader($stream)

    # Define a MemoryStream and a StreamWriter for writing into hello destination file
    $memStream = New-Object System.IO.MemoryStream
    $writeStream = New-Object System.IO.StreamWriter $memStream

    # Pre-process hello source blob
    $exString = "java.lang.Exception:"
    while(-Not $sReader.EndOfStream){
        $line = $sReader.ReadLine()
        $split = $line.Split(" ")

        # remove hello "java.lang.Exception" from hello first element of hello array
        # for example: java.lang.Exception: 2012-02-03 19:11:02 SampleClass8 [WARN] problem finding id 153454612
        if ($split[0] -eq $exString){
            #create a new ArrayList tooremove $split[0]
            $newArray = [System.Collections.ArrayList] $split
            $newArray.Remove($exString)

            # update $split and $line
            $split = $newArray
            $line = $newArray -join(" ")
        }

        # remove hello lines that has less than 7 elements
        if ($split.count -ge 7){
            write-host $line
            $writeStream.WriteLine($line)
        }
    }

    # Write toohello destination blob
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $destBlob.UploadFromStream($memStream)

    #endregion

    #region - export a log file from hello cluster toohello SQL database

    Write-Host "Preprocessing hello source file ..." -ForegroundColor Green

    $tableName_log4j = "log4jlogs"

    # Connection string for Azure SQL Database.
    # Comment if using SQL Server
    $connectionString = "jdbc:sqlserver://$sqlDatabaseServerName.database.windows.net;user=$sqlDatabaseLogin@$sqlDatabaseServerName;password=$sqlDatabasePassword;database=$sqlDatabaseName"
    # Connection string for SQL Server.
    # Uncomment if using SQL Server.
    #$connectionString = "jdbc:sqlserver://$sqlDatabaseServerName;user=$sqlDatabaseLogin;password=$sqlDatabasePassword;database=$sqlDatabaseName"

    $exportDir_log4j = "/tutorials/usesqoop/data"

    # Submit a Sqoop job
    $sqoopDef = New-AzureRmHDInsightSqoopJobDefinition `
        -Command "export --connect $connectionString --table $tableName_log4j --export-dir $exportDir_log4j --input-fields-terminated-by \0x20 -m 1"
    $sqoopJob = Start-AzureRmHDInsightJob `
                    -ClusterName $hdinsightClusterName `
                    -HttpCredential $httpCredential `
                    -JobDefinition $sqoopDef #-Debug -Verbose
    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId

    Write-Host "Standard Error" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -DefaultContainer $defaultBlobContainerName -HttpCredential $httpCredential -JobId $sqoopJob.JobId -DisplayOutputType StandardError
    Write-Host "Standard Output" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -DefaultContainer $defaultBlobContainerName -HttpCredential $httpCredential -JobId $sqoopJob.JobId -DisplayOutputType StandardOutput

    #endregion

    #region - export a Hive table

    $tableName_mobile = "mobiledata"
    $exportDir_mobile = "/hive/warehouse/hivesampletable"

    $sqoopDef = New-AzureRmHDInsightSqoopJobDefinition `
        -Command "export --connect $connectionString --table $tableName_mobile --export-dir $exportDir_mobile --fields-terminated-by \t -m 1"
    $sqoopJob = Start-AzureRmHDInsightJob `
                    -ClusterName $hdinsightClusterName `
                    -HttpCredential $httpCredential `
                    -JobDefinition $sqoopDef #-Debug -Verbose

    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId

    Write-Host "Standard Error" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultBlobContainerName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardError

    Write-Host "Standard Output" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultBlobContainerName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardOutput

    #endregion

    #region - import a database

    $targetDir_mobile = "/tutorials/usesqoop/importeddata/"

    $sqoopDef = New-AzureRmHDInsightSqoopJobDefinition `
        -Command "import --connect $connectionString --table $tableName_mobile --target-dir $targetDir_mobile --fields-terminated-by \t --lines-terminated-by \n -m 1"

    $sqoopJob = Start-AzureRmHDInsightJob `
                    -ClusterName $hdinsightClusterName `
                    -HttpCredential $httpCredential `
                    -JobDefinition $sqoopDef #-Debug -Verbose

    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId

    Write-Host "Standard Error" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultBlobContainerName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardError

    Write-Host "Standard Output" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultBlobContainerName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardOutput

    #endregion



[azure-management-portal]: https://portal.azure.com/

[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage]: ../hdinsight-hadoop-use-blob-storage.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md

[sqldatabase-get-started]: ../sql-database/sql-database-get-started.md
[sqldatabase-create-configue]: ../sql-database/sql-database-get-started.md

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-install]: /powershell/azureps-cmdlets-docs
[powershell-script]: http://technet.microsoft.com/library/ee176949.aspx

[sqoop-user-guide-1.4.4]: https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html
