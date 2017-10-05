---
title: "Azure Hdınsight (Hadoop) ile Apache Sqoop işleri çalıştırma | Microsoft Docs"
description: "Azure PowerShell bir iş istasyonundan Sqoop alma çalıştırın ve bir Hadoop kümesi ve bir Azure SQL veritabanı arasında dışa aktarmak için nasıl kullanılacağını öğrenin."
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
ms.openlocfilehash: 8e77153493b6f37f5f48116b86bad6b25a50d1a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-sqoop-with-hadoop-in-hdinsight"></a><span data-ttu-id="46c1f-103">Hdınsight'ta Hadoop ile Sqoop kullanma</span><span class="sxs-lookup"><span data-stu-id="46c1f-103">Use Sqoop with Hadoop in HDInsight</span></span>
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="46c1f-104">Sqoop Hdınsight'ta içeri ve dışarı aktarma Hdınsight kümesi ve Azure SQL veritabanı veya SQL Server veritabanı arasında nasıl kullanılacağını öğrenin.</span><span class="sxs-lookup"><span data-stu-id="46c1f-104">Learn how to use Sqoop in HDInsight to import and export between HDInsight cluster and Azure SQL database or SQL Server database.</span></span>

<span data-ttu-id="46c1f-105">Hadoop günlükleri ve dosyaları gibi yapılandırılmamış ve yarı yapılandırılmış veri işleme için doğal bir seçim olsa da olabilir ilişkisel veritabanlarında depolanan yapılandırılmış verileri işlemek için gerek.</span><span class="sxs-lookup"><span data-stu-id="46c1f-105">Although Hadoop is a natural choice for processing unstructured and semistructured data, such as logs and files, there may also be a need to process structured data that is stored in relational databases.</span></span>

<span data-ttu-id="46c1f-106">[Sqoop] [ sqoop-user-guide-1.4.4] Hadoop kümeleri ve ilişkisel veritabanları arasında veri aktarmak için tasarlanmış bir araçtır.</span><span class="sxs-lookup"><span data-stu-id="46c1f-106">[Sqoop][sqoop-user-guide-1.4.4] is a tool designed to transfer data between Hadoop clusters and relational databases.</span></span> <span data-ttu-id="46c1f-107">SQL Server, MySQL ve Oracle Hadoop dağıtılmış dosya sistemi (HDFS) içine Hadoop ile MapReduce veya Hive verilerde dönüştürme ve bir RDBMS verileri dışarı aktarma gibi bir ilişkisel veritabanı yönetim sistemine (RDBMS) verileri almak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46c1f-107">You can use it to import data from a relational database management system (RDBMS) such as SQL Server, MySQL, or Oracle into the Hadoop distributed file system (HDFS), transform the data in Hadoop with MapReduce or Hive, and then export the data back into an RDBMS.</span></span> <span data-ttu-id="46c1f-108">Bu öğreticide, ilişkisel veritabanı için SQL Server veritabanını kullanıyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="46c1f-108">In this tutorial, you are using a SQL Server database for your relational database.</span></span>

<span data-ttu-id="46c1f-109">Hdınsight kümelerinde desteklenir Sqoop sürümleri için bkz: [Hdınsight tarafından sağlanan küme sürümlerindeki yenilikler nelerdir?][hdinsight-versions]</span><span class="sxs-lookup"><span data-stu-id="46c1f-109">For Sqoop versions that are supported on HDInsight clusters, see [What's new in the cluster versions provided by HDInsight?][hdinsight-versions]</span></span>

## <a name="understand-the-scenario"></a><span data-ttu-id="46c1f-110">Senaryo anlama</span><span class="sxs-lookup"><span data-stu-id="46c1f-110">Understand the scenario</span></span>

<span data-ttu-id="46c1f-111">Hdınsight kümesi bazı örnek verilerle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="46c1f-111">HDInsight cluster comes with some sample data.</span></span> <span data-ttu-id="46c1f-112">Aşağıdaki iki örnek kullanın:</span><span class="sxs-lookup"><span data-stu-id="46c1f-112">You use the following two samples:</span></span>

* <span data-ttu-id="46c1f-113">Konumda bulunan bir log4j günlük dosyası */example/data/sample.log*.</span><span class="sxs-lookup"><span data-stu-id="46c1f-113">A log4j log file, which is located at */example/data/sample.log*.</span></span> <span data-ttu-id="46c1f-114">Günlükleri dosyasından ayıklanan:</span><span class="sxs-lookup"><span data-stu-id="46c1f-114">The following logs are extracted from the file:</span></span>
  
        2012-02-03 18:35:34 SampleClass6 [INFO] everything normal for id 577725851
        2012-02-03 18:35:34 SampleClass4 [FATAL] system problem at id 1991281254
        2012-02-03 18:35:34 SampleClass3 [DEBUG] detail for id 1304807656
        ...
* <span data-ttu-id="46c1f-115">Adlı bir Hive tablosu *hivesampletable*, veri dosyası konumunda bulunan başvuran */hive/warehouse/hivesampletable*.</span><span class="sxs-lookup"><span data-stu-id="46c1f-115">A Hive table named *hivesampletable*, which references the data file located at */hive/warehouse/hivesampletable*.</span></span> <span data-ttu-id="46c1f-116">Tablo bazı mobil cihaz verileri içerir.</span><span class="sxs-lookup"><span data-stu-id="46c1f-116">The table contains some mobile device data.</span></span> 
  
  | <span data-ttu-id="46c1f-117">Alan</span><span class="sxs-lookup"><span data-stu-id="46c1f-117">Field</span></span> | <span data-ttu-id="46c1f-118">Veri türü</span><span class="sxs-lookup"><span data-stu-id="46c1f-118">Data type</span></span> |
  | --- | --- |
  | <span data-ttu-id="46c1f-119">istemci kimliği</span><span class="sxs-lookup"><span data-stu-id="46c1f-119">clientid</span></span> |<span data-ttu-id="46c1f-120">Dize</span><span class="sxs-lookup"><span data-stu-id="46c1f-120">string</span></span> |
  | <span data-ttu-id="46c1f-121">querytime</span><span class="sxs-lookup"><span data-stu-id="46c1f-121">querytime</span></span> |<span data-ttu-id="46c1f-122">Dize</span><span class="sxs-lookup"><span data-stu-id="46c1f-122">string</span></span> |
  | <span data-ttu-id="46c1f-123">Pazar</span><span class="sxs-lookup"><span data-stu-id="46c1f-123">market</span></span> |<span data-ttu-id="46c1f-124">Dize</span><span class="sxs-lookup"><span data-stu-id="46c1f-124">string</span></span> |
  | <span data-ttu-id="46c1f-125">deviceplatform</span><span class="sxs-lookup"><span data-stu-id="46c1f-125">deviceplatform</span></span> |<span data-ttu-id="46c1f-126">Dize</span><span class="sxs-lookup"><span data-stu-id="46c1f-126">string</span></span> |
  | <span data-ttu-id="46c1f-127">devicemake</span><span class="sxs-lookup"><span data-stu-id="46c1f-127">devicemake</span></span> |<span data-ttu-id="46c1f-128">Dize</span><span class="sxs-lookup"><span data-stu-id="46c1f-128">string</span></span> |
  | <span data-ttu-id="46c1f-129">devicemodel</span><span class="sxs-lookup"><span data-stu-id="46c1f-129">devicemodel</span></span> |<span data-ttu-id="46c1f-130">Dize</span><span class="sxs-lookup"><span data-stu-id="46c1f-130">string</span></span> |
  | <span data-ttu-id="46c1f-131">durum</span><span class="sxs-lookup"><span data-stu-id="46c1f-131">state</span></span> |<span data-ttu-id="46c1f-132">Dize</span><span class="sxs-lookup"><span data-stu-id="46c1f-132">string</span></span> |
  | <span data-ttu-id="46c1f-133">Ülke</span><span class="sxs-lookup"><span data-stu-id="46c1f-133">country</span></span> |<span data-ttu-id="46c1f-134">Dize</span><span class="sxs-lookup"><span data-stu-id="46c1f-134">string</span></span> |
  | <span data-ttu-id="46c1f-135">querydwelltime</span><span class="sxs-lookup"><span data-stu-id="46c1f-135">querydwelltime</span></span> |<span data-ttu-id="46c1f-136">Çift</span><span class="sxs-lookup"><span data-stu-id="46c1f-136">double</span></span> |
  | <span data-ttu-id="46c1f-137">SessionID</span><span class="sxs-lookup"><span data-stu-id="46c1f-137">sessionid</span></span> |<span data-ttu-id="46c1f-138">bigint</span><span class="sxs-lookup"><span data-stu-id="46c1f-138">bigint</span></span> |
  | <span data-ttu-id="46c1f-139">sessionpagevieworder</span><span class="sxs-lookup"><span data-stu-id="46c1f-139">sessionpagevieworder</span></span> |<span data-ttu-id="46c1f-140">bigint</span><span class="sxs-lookup"><span data-stu-id="46c1f-140">bigint</span></span> |

<span data-ttu-id="46c1f-141">İlk olarak, verdiğiniz *sample.log* ve *hivesampletable* Azure SQL veritabanına veya SQL Server ve mobil cihaz verileri içeren tablo aşağıdaki yolu kullanarak Hdınsight'a geri alın:</span><span class="sxs-lookup"><span data-stu-id="46c1f-141">First, you export *sample.log* and *hivesampletable* to the Azure SQL database or to SQL Server, and then import the table that contains the mobile device data back to HDInsight by using the following path:</span></span>

    /tutorials/usesqoop/importeddata

## <a name="create-cluster-and-sql-database"></a><span data-ttu-id="46c1f-142">Küme ve SQL veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="46c1f-142">Create cluster and SQL database</span></span>
<span data-ttu-id="46c1f-143">Bu bölümde bir küme, bir SQL Database ve Azure portalı ve Azure Resource Manager şablonu kullanarak öğreticiyi çalıştırmak için SQL veritabanı şemalarını nasıl oluşturulacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="46c1f-143">This section shows you how to create a cluster, a SQL Database, and the SQL database schemas for running the tutorial using the Azure portal and an Azure Resource Manager template.</span></span> <span data-ttu-id="46c1f-144">Şablon bulunabilir [Azure hızlı başlangıç şablonlarını](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-sql-database/).</span><span class="sxs-lookup"><span data-stu-id="46c1f-144">The template can be found in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-sql-database/).</span></span> <span data-ttu-id="46c1f-145">Resource Manager şablonu tablo şemalarını SQL veritabanına dağıtım yapmak için bir bacpac paketi çağırır.</span><span class="sxs-lookup"><span data-stu-id="46c1f-145">The Resource Manager template calls a bacpac package to deploy the table schemas to SQL database.</span></span>  <span data-ttu-id="46c1f-146">Bacpac paketi bir ortak blob kapsayıcısında, https://hditutorialdata.blob.core.windows.net/usesqoop/SqoopTutorial-2016-2-23-11-2.bacpac bulunur.</span><span class="sxs-lookup"><span data-stu-id="46c1f-146">The bacpac package is located in a public blob container, https://hditutorialdata.blob.core.windows.net/usesqoop/SqoopTutorial-2016-2-23-11-2.bacpac.</span></span> <span data-ttu-id="46c1f-147">Özel bir kapsayıcı bacpac dosyalarını kullanmak istiyorsanız, şablonda aşağıdaki değerleri kullanın:</span><span class="sxs-lookup"><span data-stu-id="46c1f-147">If you want to use a private container for the bacpac files, use the following values in the template:</span></span>
   
        "storageKeyType": "Primary",
        "storageKey": "<TheAzureStorageAccountKey>",

<span data-ttu-id="46c1f-148">Küme ve SQL veritabanı oluşturmak için Azure PowerShell kullanmayı tercih ederseniz, [ek A](#appendix-a---a-powershell-sample).</span><span class="sxs-lookup"><span data-stu-id="46c1f-148">If you prefer to use Azure PowerShell to create the cluster and the SQL Database, see [Appendix A](#appendix-a---a-powershell-sample).</span></span>

1. <span data-ttu-id="46c1f-149">Azure portalında bir Resource Manager şablonunu açmak için aşağıdaki görüntüye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="46c1f-149">Click the following image to open a Resource Manager template in the Azure portal.</span></span>         
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-sql-database%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-use-sqoop/deploy-to-azure.png" alt="Deploy to Azure"></a>
   

2. <span data-ttu-id="46c1f-150">Aşağıdaki özellikleri girin:</span><span class="sxs-lookup"><span data-stu-id="46c1f-150">Enter the following properties:</span></span>

    - <span data-ttu-id="46c1f-151">**Abonelik**: Azure aboneliğiniz girin.</span><span class="sxs-lookup"><span data-stu-id="46c1f-151">**Subscription**: Enter your Azure subscription.</span></span>
    - <span data-ttu-id="46c1f-152">**Kaynak grubu**: yeni bir Azure kaynak grubu oluşturun veya varolan bir kaynak grubu seçin.</span><span class="sxs-lookup"><span data-stu-id="46c1f-152">**Resource Group**: Create a new Azure Resource Group, or select an existing Resource Group.</span></span>  <span data-ttu-id="46c1f-153">Bir kaynak grubu yönetim amaçla ' dir.</span><span class="sxs-lookup"><span data-stu-id="46c1f-153">A Resource Group is for management purpose.</span></span>  <span data-ttu-id="46c1f-154">Nesneler için bir kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="46c1f-154">It is a container for objects.</span></span>
    - <span data-ttu-id="46c1f-155">**Konum**: bir bölge seçin.</span><span class="sxs-lookup"><span data-stu-id="46c1f-155">**Location**: Select a region.</span></span>
    - <span data-ttu-id="46c1f-156">**ClusterName**: Hadoop kümesi için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="46c1f-156">**ClusterName**: Enter a name for the Hadoop cluster.</span></span>
    - <span data-ttu-id="46c1f-157">**Küme oturum açma adı ve parolası**: Varsayılan oturum açma adı admin şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="46c1f-157">**Cluster login name and password**: The default login name is admin.</span></span>
    - <span data-ttu-id="46c1f-158">**SSH kullanıcı adı ve parola**.</span><span class="sxs-lookup"><span data-stu-id="46c1f-158">**SSH user name and password**.</span></span>
    - <span data-ttu-id="46c1f-159">**SQL veritabanı sunucusu oturum açma adı ve parola**.</span><span class="sxs-lookup"><span data-stu-id="46c1f-159">**SQL database server login name and password**.</span></span>
    - <span data-ttu-id="46c1f-160">**_artifacts konumu**: kendi backpac dosyasını farklı bir konumda kullanmak istemediğiniz sürece varsayılan değeri kullanın.</span><span class="sxs-lookup"><span data-stu-id="46c1f-160">**_artifacts Location**: Use the default value unless you want to use your own backpac file in a different location.</span></span>
    - <span data-ttu-id="46c1f-161">**Konum Sas belirteci _artifacts**: boş bırakın.</span><span class="sxs-lookup"><span data-stu-id="46c1f-161">**_artifacts Location Sas Token**: Leave it blank.</span></span>
    - <span data-ttu-id="46c1f-162">**Bacpac dosya adı**: kendi backpac dosyanızı kullanmak istemediğiniz sürece varsayılan değeri kullanın.</span><span class="sxs-lookup"><span data-stu-id="46c1f-162">**Bacpac File Name**: Use the default value unless you want to use your own backpac file.</span></span>
     
     <span data-ttu-id="46c1f-163">Değişkenler bölümünde sabit kodlanmış değerler:</span><span class="sxs-lookup"><span data-stu-id="46c1f-163">The following values are hardcoded in the variables section:</span></span>
     
     | <span data-ttu-id="46c1f-164">Varsayılan depolama hesabı adı</span><span class="sxs-lookup"><span data-stu-id="46c1f-164">Default storage account name</span></span> | <span data-ttu-id="46c1f-165"><CluterName>Depolama</span><span class="sxs-lookup"><span data-stu-id="46c1f-165"><CluterName>store</span></span> |
     | --- | --- |
     | <span data-ttu-id="46c1f-166">Azure SQL veritabanı sunucusu adı</span><span class="sxs-lookup"><span data-stu-id="46c1f-166">Azure SQL database server name</span></span> |<span data-ttu-id="46c1f-167"><ClusterName>dbserver</span><span class="sxs-lookup"><span data-stu-id="46c1f-167"><ClusterName>dbserver</span></span> |
     | <span data-ttu-id="46c1f-168">Azure SQL veritabanı adı</span><span class="sxs-lookup"><span data-stu-id="46c1f-168">Azure SQL database name</span></span> |<span data-ttu-id="46c1f-169"><ClusterName>DB</span><span class="sxs-lookup"><span data-stu-id="46c1f-169"><ClusterName>db</span></span> |
     
     <span data-ttu-id="46c1f-170">Lütfen bu değerleri yazın.</span><span class="sxs-lookup"><span data-stu-id="46c1f-170">Please write down these values.</span></span>  <span data-ttu-id="46c1f-171">Öğreticinin sonraki bölümlerinde bunlara ihtiyacınız olacaktır.</span><span class="sxs-lookup"><span data-stu-id="46c1f-171">You need them later in the tutorial.</span></span>

<span data-ttu-id="46c1f-172">3. Parametreleri kaydetmek için **Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="46c1f-172">3.Click **OK** to save the parameters.</span></span>

<span data-ttu-id="46c1f-173">4. **Özel dağıtım** dikey penceresinde **Kaynak grubu** açılır kutusuna ve ardından **Yeni**’ye tıklayarak yeni bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="46c1f-173">4.From the **Custom deployment** blade, click **Resource group** dropdown box, and then click **New** to create a new resource group.</span></span> <span data-ttu-id="46c1f-174">Kaynak grubu; küme, bağımlı depolama hesabını ve diğer bağlı kaynağı gruplandıran bir kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="46c1f-174">The resource group is a container that groups the cluster, the dependent storage account and other linked resource.</span></span>

<span data-ttu-id="46c1f-175">5. **Yasal koşullar**’a ve ardından **Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="46c1f-175">5.Click **Legal terms**, and then click **Create**.</span></span>

<span data-ttu-id="46c1f-176">6. **Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="46c1f-176">6.Click **Create**.</span></span> <span data-ttu-id="46c1f-177">Şablon dağıtımı için dağıtım gönderme başlıklı yeni bir kutucuk görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="46c1f-177">You see a new tile titled Submitting deployment for Template deployment.</span></span> <span data-ttu-id="46c1f-178">Kümenin ve SQL veritabanının oluşturulması yaklaşık 20 dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="46c1f-178">It takes about around 20 minutes to create the cluster and SQL database.</span></span>

<span data-ttu-id="46c1f-179">Mevcut Azure SQL veritabanını veya Microsoft SQL Server kullanmayı tercih ederseniz</span><span class="sxs-lookup"><span data-stu-id="46c1f-179">If you choose to use existing Azure SQL database or Microsoft SQL Server</span></span>

* <span data-ttu-id="46c1f-180">**Azure SQL veritabanı**: iş istasyonunuzu erişime izin verecek şekilde Azure SQL veritabanı sunucusu için bir güvenlik duvarını yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="46c1f-180">**Azure SQL database**: You must configure a firewall rule for the Azure SQL database server to allow access from your workstation.</span></span> <span data-ttu-id="46c1f-181">Bir Azure SQL veritabanı oluşturma ve Güvenlik Duvarı'nı yapılandırma hakkında yönergeler için bkz: [Azure SQL veritabanını kullanmaya başlama][sqldatabase-get-started].</span><span class="sxs-lookup"><span data-stu-id="46c1f-181">For instructions about creating an Azure SQL database and configuring the firewall, see [Get started using Azure SQL database][sqldatabase-get-started].</span></span> 
  
  > [!NOTE]
  > <span data-ttu-id="46c1f-182">Varsayılan olarak Azure SQL veritabanını Azure Hdınsight gibi Azure hizmetlerden bağlantılara izin verir.</span><span class="sxs-lookup"><span data-stu-id="46c1f-182">By default an Azure SQL database allows connections from Azure services, such as Azure HDInsight.</span></span> <span data-ttu-id="46c1f-183">Bu güvenlik duvarı ayarı devre dışıysa, Azure portalından etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="46c1f-183">If this firewall setting is disabled, you need to enable it from the Azure portal.</span></span> <span data-ttu-id="46c1f-184">Bir Azure SQL veritabanı oluşturma ve güvenlik duvarı kuralları yapılandırma hakkında daha fazla yönerge için bkz: [oluşturma ve yapılandırma SQL veritabanı][sqldatabase-create-configue].</span><span class="sxs-lookup"><span data-stu-id="46c1f-184">For instruction about creating an Azure SQL database and configuring firewall rules, see [Create and Configure SQL Database][sqldatabase-create-configue].</span></span>
  > 
  > 
* <span data-ttu-id="46c1f-185">**SQL Server**: Hdınsight kümenize Azure SQL sunucusu olarak aynı sanal ağda ise, adımları bu makalede SQL Server veritabanına veri vermek ve almak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46c1f-185">**SQL Server**: If your HDInsight cluster is on the same virtual network in Azure as SQL Server, you can use the steps in this article to import and export data to a SQL Server database.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="46c1f-186">Hdınsight yalnızca konum tabanlı sanal ağları destekler ve benzeşim grubu tabanlı sanal ağlar ile şu anda çalışmıyor.</span><span class="sxs-lookup"><span data-stu-id="46c1f-186">HDInsight supports only location-based virtual networks, and it does not currently work with affinity group-based virtual networks.</span></span>
  > 
  > 
  
  * <span data-ttu-id="46c1f-187">Oluşturma ve bir sanal ağ yapılandırma için bkz: [Azure portalını kullanarak bir sanal ağ oluşturma](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="46c1f-187">To create and configure a virtual network, see [Create a virtual network using the Azure portal](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span></span>
    
    * <span data-ttu-id="46c1f-188">SQL Server, veri merkezinizde kullanırken, sanal ağ olarak yapılandırmalısınız *siteden siteye* veya *noktadan siteye*.</span><span class="sxs-lookup"><span data-stu-id="46c1f-188">When you are using SQL Server in your datacenter, you must configure the virtual network as *site-to-site* or *point-to-site*.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="46c1f-189">İçin **noktası site** sanal ağlar, SQL Server çalıştıran kullanılabilir yapılandırma uygulama VPN istemcisi gerekir **Pano** Azure sanal ağı yapılandırmanızın.</span><span class="sxs-lookup"><span data-stu-id="46c1f-189">For **point-to-site** virtual networks, SQL Server must be running the VPN client configuration application, which is available from the **Dashboard** of your Azure virtual network configuration.</span></span>
      > 
      > 
    * <span data-ttu-id="46c1f-190">Bir Azure sanal makinede SQL Server kullanırken SQL Server'ı barındıran sanal makine Hdınsight aynı sanal ağda bir üyesi ise herhangi bir sanal ağ yapılandırması kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="46c1f-190">When you are using SQL Server on an Azure virtual machine, any virtual network configuration can be used if the virtual machine hosting SQL Server is a member of the same virtual network as HDInsight.</span></span>
  * <span data-ttu-id="46c1f-191">Hdınsight kümesi üzerinde bir sanal ağ oluşturmak için bkz: [özel seçenekleri kullanarak Hdınsight'ta oluşturmak Hadoop kümeleri](hdinsight-hadoop-provision-linux-clusters.md)</span><span class="sxs-lookup"><span data-stu-id="46c1f-191">To create an HDInsight cluster on a virtual network, see [Create Hadoop clusters in HDInsight using custom options](hdinsight-hadoop-provision-linux-clusters.md)</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="46c1f-192">SQL Server kimlik doğrulaması da izin vermelidir.</span><span class="sxs-lookup"><span data-stu-id="46c1f-192">SQL Server must also allow authentication.</span></span> <span data-ttu-id="46c1f-193">Bu makaledeki adımları tamamlamak için bir SQL Server oturumu kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="46c1f-193">You must use a SQL Server login to complete the steps in this article.</span></span>
    > 
    > 

## <a name="run-sqoop-jobs"></a><span data-ttu-id="46c1f-194">Sqoop işleri çalıştırma</span><span class="sxs-lookup"><span data-stu-id="46c1f-194">Run Sqoop jobs</span></span>
<span data-ttu-id="46c1f-195">Hdınsight Sqoop işleri çeşitli yöntemler kullanarak çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46c1f-195">HDInsight can run Sqoop jobs by using a variety of methods.</span></span> <span data-ttu-id="46c1f-196">Hangi yöntemi sizin için uygun olduğuna karar vermek için aşağıdaki tabloyu kullanın, sonra bir anlatım için bağlantıyı izleyin.</span><span class="sxs-lookup"><span data-stu-id="46c1f-196">Use the following table to decide which method is right for you, then follow the link for a walkthrough.</span></span>

| <span data-ttu-id="46c1f-197">**Bu** isterseniz...</span><span class="sxs-lookup"><span data-stu-id="46c1f-197">**Use this** if you want...</span></span> | <span data-ttu-id="46c1f-198">.. .an **etkileşimli** Kabuk</span><span class="sxs-lookup"><span data-stu-id="46c1f-198">...an **interactive** shell</span></span> | <span data-ttu-id="46c1f-199">... **toplu** işleme</span><span class="sxs-lookup"><span data-stu-id="46c1f-199">...**batch** processing</span></span> | <span data-ttu-id="46c1f-200">.. hemen bu **küme işletim sistemi**</span><span class="sxs-lookup"><span data-stu-id="46c1f-200">...with this **cluster operating system**</span></span> | <span data-ttu-id="46c1f-201">.. .from bu **istemci işletim sistemi**</span><span class="sxs-lookup"><span data-stu-id="46c1f-201">...from this **client operating system**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="46c1f-202">SSH</span><span class="sxs-lookup"><span data-stu-id="46c1f-202">SSH</span></span>](hdinsight-use-sqoop-mac-linux.md) |<span data-ttu-id="46c1f-203">✔</span><span class="sxs-lookup"><span data-stu-id="46c1f-203">✔</span></span> |<span data-ttu-id="46c1f-204">✔</span><span class="sxs-lookup"><span data-stu-id="46c1f-204">✔</span></span> |<span data-ttu-id="46c1f-205">Linux</span><span class="sxs-lookup"><span data-stu-id="46c1f-205">Linux</span></span> |<span data-ttu-id="46c1f-206">Linux, UNIX, Mac OS X veya Windows</span><span class="sxs-lookup"><span data-stu-id="46c1f-206">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="46c1f-207">Hadoop için .NET SDK</span><span class="sxs-lookup"><span data-stu-id="46c1f-207">.NET SDK for Hadoop</span></span>](hdinsight-hadoop-use-sqoop-dotnet-sdk.md) |&nbsp; |<span data-ttu-id="46c1f-208">✔</span><span class="sxs-lookup"><span data-stu-id="46c1f-208">✔</span></span> |<span data-ttu-id="46c1f-209">Linux veya Windows</span><span class="sxs-lookup"><span data-stu-id="46c1f-209">Linux or Windows</span></span> |<span data-ttu-id="46c1f-210">Windows (için şimdi)</span><span class="sxs-lookup"><span data-stu-id="46c1f-210">Windows (for now)</span></span> |
| [<span data-ttu-id="46c1f-211">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="46c1f-211">Azure PowerShell</span></span>](hdinsight-hadoop-use-sqoop-powershell.md) |&nbsp; |<span data-ttu-id="46c1f-212">✔</span><span class="sxs-lookup"><span data-stu-id="46c1f-212">✔</span></span> |<span data-ttu-id="46c1f-213">Linux veya Windows</span><span class="sxs-lookup"><span data-stu-id="46c1f-213">Linux or Windows</span></span> |<span data-ttu-id="46c1f-214">Windows</span><span class="sxs-lookup"><span data-stu-id="46c1f-214">Windows</span></span> |

## <a name="limitations"></a><span data-ttu-id="46c1f-215">Sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="46c1f-215">Limitations</span></span>
* <span data-ttu-id="46c1f-216">Toplu export - ile Linux tabanlı Hdınsight, Microsoft SQL Server veya Azure SQL veritabanı için verileri dışa aktarmak için kullanılan Sqoop bağlayıcı toplu eklemeler şu anda desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="46c1f-216">Bulk export - With Linux-based HDInsight, the Sqoop connector used to export data to Microsoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>
* <span data-ttu-id="46c1f-217">-Kullanırken, Linux tabanlı Hdınsight ile toplu işleme `-batch` eklemeleri gerçekleştirirken geçiş, Sqoop gerçekleştirir INSERT işlemlerine toplu işleme yerine birden çok ekler.</span><span class="sxs-lookup"><span data-stu-id="46c1f-217">Batching - With Linux-based HDInsight, When using the `-batch` switch when performing inserts, Sqoop performs multiple inserts instead of batching the insert operations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="46c1f-218">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="46c1f-218">Next steps</span></span>
<span data-ttu-id="46c1f-219">Şimdi Sqoop kullanma öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="46c1f-219">Now you have learned how to use Sqoop.</span></span> <span data-ttu-id="46c1f-220">Daha fazla bilgi için bkz:</span><span class="sxs-lookup"><span data-stu-id="46c1f-220">To learn more, see:</span></span>

* [<span data-ttu-id="46c1f-221">HDInsight ile Hive kullanma</span><span class="sxs-lookup"><span data-stu-id="46c1f-221">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="46c1f-222">HDInsight ile Pig kullanma</span><span class="sxs-lookup"><span data-stu-id="46c1f-222">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* <span data-ttu-id="46c1f-223">[Hdınsight ile Oozie kullanma][hdinsight-use-oozie]: Oozie iş akışında kullanmak Sqoop eylem.</span><span class="sxs-lookup"><span data-stu-id="46c1f-223">[Use Oozie with HDInsight][hdinsight-use-oozie]: Use Sqoop action in an Oozie workflow.</span></span>
* <span data-ttu-id="46c1f-224">[Hdınsight kullanarak uçuş gecikme verileri analiz][hdinsight-analyze-flight-data]: uçuş çözümlemek için kullanmak Hive gecikme veri ve bir Azure SQL veritabanına veri vermek için Sqoop kullanın.</span><span class="sxs-lookup"><span data-stu-id="46c1f-224">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-data]: Use Hive to analyze flight delay data, and then use Sqoop to export data to an Azure SQL database.</span></span>
* <span data-ttu-id="46c1f-225">[Verileri Hdınsight'a yükleme][hdinsight-upload-data]: Hdınsight/Azure Blob depolama alanına veri yüklemek için diğer yöntemler bulun.</span><span class="sxs-lookup"><span data-stu-id="46c1f-225">[Upload data to HDInsight][hdinsight-upload-data]: Find other methods for uploading data to HDInsight/Azure Blob storage.</span></span>

## <a name="appendix-a---a-powershell-sample"></a><span data-ttu-id="46c1f-226">Ek A - PowerShell örnek</span><span class="sxs-lookup"><span data-stu-id="46c1f-226">Appendix A - a PowerShell sample</span></span>
<span data-ttu-id="46c1f-227">PowerShell örnek aşağıdaki adımları gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="46c1f-227">The PowerShell sample performs the following steps:</span></span>

1. <span data-ttu-id="46c1f-228">Azure'a bağlayın.</span><span class="sxs-lookup"><span data-stu-id="46c1f-228">Connect to Azure.</span></span>
2. <span data-ttu-id="46c1f-229">Bir Azure kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="46c1f-229">Create an Azure resource group.</span></span> <span data-ttu-id="46c1f-230">Daha fazla bilgi için bkz: [Azure PowerShell'i Azure Resource Manager ile kullanma](../powershell-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="46c1f-230">For more information, see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md)</span></span>
3. <span data-ttu-id="46c1f-231">Bir Azure SQL veritabanı sunucusu, Azure SQL veritabanına ve iki tablo oluşturun.</span><span class="sxs-lookup"><span data-stu-id="46c1f-231">Create an Azure SQL Database server, an Azure SQL database, and two tables.</span></span> 
   
    <span data-ttu-id="46c1f-232">Bunun yerine SQL Server kullanıyorsanız, tablolar oluşturmak için aşağıdaki ifadeleri kullanın:</span><span class="sxs-lookup"><span data-stu-id="46c1f-232">If you use SQL Server instead, use the following statements to create the tables:</span></span>
   
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
   
    <span data-ttu-id="46c1f-233">Veritabanı ve tablolar incelemek için en kolay yolu, Visual Studio kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="46c1f-233">The easiest way to examine the database and tables is to use Visual Studio.</span></span> <span data-ttu-id="46c1f-234">Veritabanı sunucusu ve veritabanı Azure portalını kullanarak incelenebilir.</span><span class="sxs-lookup"><span data-stu-id="46c1f-234">The database server and the database can be examined using the Azure portal.</span></span>
4. <span data-ttu-id="46c1f-235">Hdınsight kümesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="46c1f-235">Create an HDInsight cluster.</span></span>
   
    <span data-ttu-id="46c1f-236">Küme incelemek için Azure portalında veya Azure PowerShell'i kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46c1f-236">To examine the cluster, you can use the Azure portal or Azure PowerShell.</span></span>
5. <span data-ttu-id="46c1f-237">Kaynak veri dosyası önceden işleyebilir.</span><span class="sxs-lookup"><span data-stu-id="46c1f-237">Pre-process the source data file.</span></span>
   
    <span data-ttu-id="46c1f-238">Bu öğreticide, bir Azure SQL veritabanına log4j günlük dosyası (ayrılmış bir dosya) ve bir Hive tablosu verin.</span><span class="sxs-lookup"><span data-stu-id="46c1f-238">In this tutorial, you export a log4j log file (a delimited file) and a Hive table to an Azure SQL database.</span></span> <span data-ttu-id="46c1f-239">Ayrılmış dosya adında */example/data/sample.log*.</span><span class="sxs-lookup"><span data-stu-id="46c1f-239">The delimited file is called */example/data/sample.log*.</span></span> <span data-ttu-id="46c1f-240">Öğreticide daha önce log4j günlükler bazı örnekler gördünüz.</span><span class="sxs-lookup"><span data-stu-id="46c1f-240">Earlier in the tutorial, you saw a few samples of log4j logs.</span></span> <span data-ttu-id="46c1f-241">Günlük dosyasında bazı boş satırlar ve vardır bazı satırlar bunlara benzer:</span><span class="sxs-lookup"><span data-stu-id="46c1f-241">In the log file, there are some empty lines and some lines similar to these:</span></span>
   
        java.lang.Exception: 2012-02-03 20:11:35 SampleClass2 [FATAL] unrecoverable system problem at id 609774657
            at com.osa.mocklogger.MockLogger$2.run(MockLogger.java:83)
   
    <span data-ttu-id="46c1f-242">Bu verileri kullanan diğer örnekler için ince budur ancak biz Azure SQL veritabanı ya da SQL Server içeri aktarmadan önce bu özel durumlar kaldırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="46c1f-242">This is fine for other examples that use this data, but we must remove these exceptions before we can import into the Azure SQL database or SQL Server.</span></span> <span data-ttu-id="46c1f-243">Sqoop verme başarısız boş bir dize veya daha az sayıda olan bir satır varsa Azure SQL veritabanı tablosunda tanımlanan alanların sayısından.</span><span class="sxs-lookup"><span data-stu-id="46c1f-243">Sqoop export  fails if there is an empty string or a line with a fewer elements than the number of fields defined in the Azure SQL database table.</span></span> <span data-ttu-id="46c1f-244">Log4jlogs Tablo 7 dize türü alan yok.</span><span class="sxs-lookup"><span data-stu-id="46c1f-244">The log4jlogs table has 7 string-type fields.</span></span>
   
    <span data-ttu-id="46c1f-245">Bu yordam küme üzerinde yeni bir dosya oluşturur: tutorials/usesqoop/data/sample.log.</span><span class="sxs-lookup"><span data-stu-id="46c1f-245">This procedure creates a new file on the cluster: tutorials/usesqoop/data/sample.log.</span></span> <span data-ttu-id="46c1f-246">Değiştirilen veri dosyasını incelemek için Azure portalı, Azure Storage Gezgini aracını veya Azure PowerShell kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46c1f-246">To examine the modified data file, you can use the Azure portal, an Azure Storage explorer tool, or Azure PowerShell.</span></span> <span data-ttu-id="46c1f-247">[Hdınsight kullanmaya başlama] [ hdinsight-get-started] dosya indirme ve dosya içeriği görüntülemek için Azure PowerShell kullanarak bir kod örneği vardır.</span><span class="sxs-lookup"><span data-stu-id="46c1f-247">[Get started with HDInsight][hdinsight-get-started] has a code sample for using Azure PowerShell to download a file and display the file content.</span></span>
6. <span data-ttu-id="46c1f-248">Bir veri dosyası Azure SQL veritabanına verin.</span><span class="sxs-lookup"><span data-stu-id="46c1f-248">Export a data file to the Azure SQL database.</span></span>
   
    <span data-ttu-id="46c1f-249">Kaynak dosyası tutorials/usesqoop/data/sample.log değil.</span><span class="sxs-lookup"><span data-stu-id="46c1f-249">The source file is tutorials/usesqoop/data/sample.log.</span></span> <span data-ttu-id="46c1f-250">Veriler için dışa tablo log4jlogs adı verilir.</span><span class="sxs-lookup"><span data-stu-id="46c1f-250">The table where the data is exported to is called log4jlogs.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="46c1f-251">Bağlantı dizesi bilgilerini dışında SQL Server veya bir Azure SQL veritabanı için bu bölümdeki adımları çalışması gerekir.</span><span class="sxs-lookup"><span data-stu-id="46c1f-251">Other than connection string information, the steps in this section should work for an Azure SQL database or for SQL Server.</span></span> <span data-ttu-id="46c1f-252">Bu adımları aşağıdaki yapılandırmayı kullanarak test edilmiş:</span><span class="sxs-lookup"><span data-stu-id="46c1f-252">These steps were tested by using the following configuration:</span></span>
   > 
   > * <span data-ttu-id="46c1f-253">**Azure sanal ağı noktadan siteye Yapılandırması**: bir sanal ağ özel bir veri merkezinde bir SQL Server Hdınsight kümesi bağlanır.</span><span class="sxs-lookup"><span data-stu-id="46c1f-253">**Azure virtual network point-to-site configuration**: A virtual network connected the HDInsight cluster to a SQL Server in a private datacenter.</span></span> <span data-ttu-id="46c1f-254">Bkz: [Yönetim Portalı'nda bir noktadan siteye VPN yapılandırma](../vpn-gateway/vpn-gateway-point-to-site-create.md) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="46c1f-254">See [Configure a Point-to-Site VPN in the Management Portal](../vpn-gateway/vpn-gateway-point-to-site-create.md) for more information.</span></span>
   > * <span data-ttu-id="46c1f-255">**Azure Hdınsight 3.1**: bkz [özel seçenekleri kullanarak Hdınsight'ta oluşturmak Hadoop kümeleri](hdinsight-hadoop-provision-linux-clusters.md) bir küme üzerinde bir sanal ağ oluşturma hakkında daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="46c1f-255">**Azure HDInsight 3.1**: See [Create Hadoop clusters in HDInsight using custom options](hdinsight-hadoop-provision-linux-clusters.md) for information about creating a cluster on a virtual network.</span></span>
   > * <span data-ttu-id="46c1f-256">**SQL Server 2014**: kimlik doğrulaması ve güvenli bir şekilde sanal ağa bağlanmak için bir yapılandırma paketi VPN istemcisi çalıştıran izin verecek şekilde yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="46c1f-256">**SQL Server 2014**: Configured to allow authentication and running the VPN client configuration package to connect securely to the virtual network.</span></span>
   > 
   > 
7. <span data-ttu-id="46c1f-257">Bir Hive tablosu Azure SQL veritabanına verin.</span><span class="sxs-lookup"><span data-stu-id="46c1f-257">Export a Hive table to the Azure SQL database.</span></span>
8. <span data-ttu-id="46c1f-258">Mobiledata tablo Hdınsight kümesine içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="46c1f-258">Import the mobiledata table to the HDInsight cluster.</span></span>
   
    <span data-ttu-id="46c1f-259">Değiştirilen veri dosyasını incelemek için Azure portalı, Azure Storage Gezgini aracını veya Azure PowerShell kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46c1f-259">To examine the modified data file, you can use the Azure portal, an Azure Storage explorer tool, or Azure PowerShell.</span></span>  <span data-ttu-id="46c1f-260">[Hdınsight kullanmaya başlama] [ hdinsight-get-started] dosya indirme ve dosya içeriği görüntülemek için Azure PowerShell'i kullanma hakkında bir kod örneği vardır.</span><span class="sxs-lookup"><span data-stu-id="46c1f-260">[Get started with HDInsight][hdinsight-get-started] has a code sample about using Azure PowerShell to download a file and display the file content.</span></span>

### <a name="the-powershell-sample"></a><span data-ttu-id="46c1f-261">PowerShell örnek</span><span class="sxs-lookup"><span data-stu-id="46c1f-261">The PowerShell sample</span></span>
    # Prepare an Azure SQL database to be used by the Sqoop tutorial

    #region - provide the following values

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

    #region - Connect to Azure subscription
    Write-Host "`nConnecting to your Azure subscription ..." -ForegroundColor Green
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

        #To allow other Azure services to access the server add a firewall rule and set both the StartIpAddress and EndIpAddress to 0.0.0.0. 
        #Note that this allows Azure traffic from any Azure subscription to access the server.
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
    Write-Host "Creating the log4jlogs table and the mobiledata table ..." -ForegroundColor Green

    $conn = New-Object System.Data.SqlClient.SqlConnection
    $conn.ConnectionString = $sqlDatabaseConnectionString
    $conn.Open()

    # Create the log4jlogs table and index
    $cmd = New-Object System.Data.SqlClient.SqlCommand
    $cmd.Connection = $conn
    $cmd.CommandText = $cmdCreateLog4jTable
    $ret = $cmd.ExecuteNonQuery()
    $cmd.CommandText = $cmdCreateLog4jClusteredIndex
    $cmd.ExecuteNonQuery()

    # Create the mobiledata table and index
    $cmd.CommandText = $cmdCreateMobileTable
    $cmd.ExecuteNonQuery()
    $cmd.CommandText = $cmdCreateMobileDataClusteredIndex
    $cmd.ExecuteNonQuery()

    $conn.close()

    #endregion


    #region - Create HDInsight cluster

    Write-Host "Creating the HDInsight cluster and the dependent services ..." -ForegroundColor Green

    # Create the default storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $defaultStorageAccountName `
        -Location $location `
        -Type Standard_LRS

    # Create the default Blob container
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                    -ResourceGroupName $resourceGroupName `
                                    -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext `
                                        -StorageAccountName $defaultStorageAccountName `
                                        -StorageAccountKey $defaultStorageAccountKey 
    New-AzureStorageContainer `
        -Name $defaultBlobContainerName `
        -Context $defaultStorageAccountContext 

    # Create the HDInsight cluster
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

    # Validate the cluster
    Get-AzureRmHDInsightCluster -ClusterName $hdinsightClusterName
    #endregion

    #region - pre-process the source file

    Write-Host "Preprocessing the source file ..." -ForegroundColor Green

    # This procedure creates a new file with $destBlobName
    $sourceBlobName = "example/data/sample.log"
    $destBlobName = "tutorials/usesqoop/data/sample.log"

    # Define the connection string
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$defaultStorageAccountName;AccountKey=$defaultStorageAccountKey"

    # Create block blob objects referencing the source and destination blob.
    $storageAccount = [Microsoft.WindowsAzure.Storage.CloudStorageAccount]::Parse($storageConnectionString)
    $storageClient = $storageAccount.CreateCloudBlobClient();
    $storageContainer = $storageClient.GetContainerReference($defaultBlobContainerName)
    $sourceBlob = $storageContainer.GetBlockBlobReference($sourceBlobName)
    $destBlob = $storageContainer.GetBlockBlobReference($destBlobName)

    # Define a MemoryStream and a StreamReader for reading from the source file
    $stream = New-Object System.IO.MemoryStream
    $stream = $sourceBlob.OpenRead()
    $sReader = New-Object System.IO.StreamReader($stream)

    # Define a MemoryStream and a StreamWriter for writing into the destination file
    $memStream = New-Object System.IO.MemoryStream
    $writeStream = New-Object System.IO.StreamWriter $memStream

    # Pre-process the source blob
    $exString = "java.lang.Exception:"
    while(-Not $sReader.EndOfStream){
        $line = $sReader.ReadLine()
        $split = $line.Split(" ")

        # remove the "java.lang.Exception" from the first element of the array
        # for example: java.lang.Exception: 2012-02-03 19:11:02 SampleClass8 [WARN] problem finding id 153454612
        if ($split[0] -eq $exString){
            #create a new ArrayList to remove $split[0]
            $newArray = [System.Collections.ArrayList] $split
            $newArray.Remove($exString)

            # update $split and $line
            $split = $newArray
            $line = $newArray -join(" ")
        }

        # remove the lines that has less than 7 elements
        if ($split.count -ge 7){
            write-host $line
            $writeStream.WriteLine($line)
        }
    }

    # Write to the destination blob
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $destBlob.UploadFromStream($memStream)

    #endregion

    #region - export a log file from the cluster to the SQL database

    Write-Host "Preprocessing the source file ..." -ForegroundColor Green

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
