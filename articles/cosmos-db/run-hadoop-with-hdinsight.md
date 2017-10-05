---
title: "Azure Cosmos DB ile Hdınsight Hadoop işini çalıştır | Microsoft Docs"
description: "Azure Cosmos DB ve Azure Hdınsight ile basit bir Hive, Pig ve MapReduce işi çalıştıran öğrenin."
services: cosmos-db
author: dennyglee
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: 06f0ea9d-07cb-4593-a9c5-ab912b62ac42
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 06/08/2017
ms.author: denlee
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 427864fc4e494c19fcda4cfd454a9923499f6337
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <span data-ttu-id="710cd-103"><a name="Azure Cosmos DB-HDInsight"></a>Azure Cosmos DB ve Hdınsight kullanarak bir Apache Hive, Pig veya Hadoop işini çalıştır</span><span class="sxs-lookup"><span data-stu-id="710cd-103"><a name="Azure Cosmos DB-HDInsight"></a>Run an Apache Hive, Pig, or Hadoop job using Azure Cosmos DB and HDInsight</span></span>
<span data-ttu-id="710cd-104">Bu öğretici nasıl çalıştırılacağını gösterir [Apache Hive][apache-hive], [Apache Pig][apache-pig], ve [Apache Hadoop] [ apache-hadoop] Cosmos veritabanı Hadoop Bağlayıcısı ile MapReduce işleri Azure hdınsight'ta.</span><span class="sxs-lookup"><span data-stu-id="710cd-104">This tutorial shows you how to run [Apache Hive][apache-hive], [Apache Pig][apache-pig], and [Apache Hadoop][apache-hadoop] MapReduce jobs on Azure HDInsight with Cosmos DB's Hadoop connector.</span></span> <span data-ttu-id="710cd-105">Cosmos veritabanı Hadoop Bağlayıcısı Cosmos hem kaynak hem de Hive, Pig ve MapReduce işleri için havuz olarak davranacak şekilde DB sağlar.</span><span class="sxs-lookup"><span data-stu-id="710cd-105">Cosmos DB's Hadoop connector allows Cosmos DB to act as both a source and sink for Hive, Pig, and MapReduce jobs.</span></span> <span data-ttu-id="710cd-106">Bu öğretici Cosmos DB Hadoop işleri veri kaynağı ve hedef kullanır.</span><span class="sxs-lookup"><span data-stu-id="710cd-106">This tutorial will use Cosmos DB as both the data source and destination for Hadoop jobs.</span></span>

<span data-ttu-id="710cd-107">Bu öğreticiyi tamamladıktan sonra aşağıdaki soruları yanıtlayın mümkün olacaktır:</span><span class="sxs-lookup"><span data-stu-id="710cd-107">After completing this tutorial, you'll be able to answer the following questions:</span></span>

* <span data-ttu-id="710cd-108">Cosmos Hive, Pig ve MapReduce işi kullanılarak DB'den nasıl veri yükleme?</span><span class="sxs-lookup"><span data-stu-id="710cd-108">How do I load data from Cosmos DB using a Hive, Pig, or MapReduce job?</span></span>
* <span data-ttu-id="710cd-109">Cosmos Hive, Pig ve MapReduce işi kullanılarak DB'de nasıl veri depoluyor?</span><span class="sxs-lookup"><span data-stu-id="710cd-109">How do I store data in Cosmos DB using a Hive, Pig, or MapReduce job?</span></span>

<span data-ttu-id="710cd-110">Biz Cosmos DB Hdınsight ile Hive işi çalıştırdığı aşağıdaki videoyu izleyerek çalışmaya başlamanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="710cd-110">We recommend getting started by watching the following video, where we run through a Hive job using Cosmos DB and HDInsight.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Use-Azure-DocumentDB-Hadoop-Connector-with-Azure-HDInsight/player]
>
>

<span data-ttu-id="710cd-111">Ardından, bu makalede, burada nasıl Cosmos DB verilerinizde analytics işlerine çalıştırabilirsiniz tam Ayrıntılar alırsınız döndür.</span><span class="sxs-lookup"><span data-stu-id="710cd-111">Then, return to this article, where you'll receive the full details on how you can run analytics jobs on your Cosmos DB data.</span></span>

> [!TIP]
> <span data-ttu-id="710cd-112">Bu öğretici, Apache Hadoop, Hive ve/veya Pig kullanma konusunda deneyim sahibi olduğunuzu varsayar.</span><span class="sxs-lookup"><span data-stu-id="710cd-112">This tutorial assumes that you have prior experience using Apache Hadoop, Hive, and/or Pig.</span></span> <span data-ttu-id="710cd-113">Apache Hadoop, Hive ve Pig yeniyseniz, ziyaret öneririz [Apache Hadoop belgeleri][apache-hadoop-doc].</span><span class="sxs-lookup"><span data-stu-id="710cd-113">If you are new to Apache Hadoop, Hive, and Pig, we recommend visiting the [Apache Hadoop documentation][apache-hadoop-doc].</span></span> <span data-ttu-id="710cd-114">Bu öğreticinin ayrıca Cosmos DB ile konusunda deneyim sahibi ve bir Cosmos DB hesabına sahip olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="710cd-114">This tutorial also assumes that you have prior experience with Cosmos DB and have a Cosmos DB account.</span></span> <span data-ttu-id="710cd-115">Cosmos DB yeni veya Cosmos DB hesap yok, lütfen kullanıma bizim [Başlarken] [ getting-started] sayfası.</span><span class="sxs-lookup"><span data-stu-id="710cd-115">If you are new to Cosmos DB or you do not have a Cosmos DB account, please check out our [Getting Started][getting-started] page.</span></span>
>
>

<span data-ttu-id="710cd-116">Yoksa öğreticiyi tamamlamak için saat ve Hive, Pig ve MapReduce için tam örnek PowerShell komut dosyalarını almak istediğiniz?</span><span class="sxs-lookup"><span data-stu-id="710cd-116">Don't have time to complete the tutorial and just want to get the full sample PowerShell scripts for Hive, Pig, and MapReduce?</span></span> <span data-ttu-id="710cd-117">Bir sorun bunları getirmek [burada][hdinsight-samples].</span><span class="sxs-lookup"><span data-stu-id="710cd-117">Not a problem, get them [here][hdinsight-samples].</span></span> <span data-ttu-id="710cd-118">İndirme Ayrıca bu örnekleri için hql, pig ve java dosyaları içerir.</span><span class="sxs-lookup"><span data-stu-id="710cd-118">The download also contains the hql, pig, and java files for these samples.</span></span>

## <span data-ttu-id="710cd-119"><a name="NewestVersion"></a>En yeni sürümü</span><span class="sxs-lookup"><span data-stu-id="710cd-119"><a name="NewestVersion"></a>Newest Version</span></span>
<table border='1'>
    <tr><th><span data-ttu-id="710cd-120">Hadoop Bağlayıcısı sürüm</span><span class="sxs-lookup"><span data-stu-id="710cd-120">Hadoop Connector Version</span></span></th>
        <td><span data-ttu-id="710cd-121">1.2.0</span><span class="sxs-lookup"><span data-stu-id="710cd-121">1.2.0</span></span></td></tr>
    <tr><th><span data-ttu-id="710cd-122">Betik URI'si</span><span class="sxs-lookup"><span data-stu-id="710cd-122">Script Uri</span></span></th>
        <td><span data-ttu-id="710cd-123">https://portalcontent.BLOB.Core.Windows.NET/scriptaction/documentdb-hadoop-installer-v04.ps1</span><span class="sxs-lookup"><span data-stu-id="710cd-123">https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</span></span></td></tr>
    <tr><th><span data-ttu-id="710cd-124">Değiştirilme tarihi</span><span class="sxs-lookup"><span data-stu-id="710cd-124">Date Modified</span></span></th>
        <td><span data-ttu-id="710cd-125">04/26/2016</span><span class="sxs-lookup"><span data-stu-id="710cd-125">04/26/2016</span></span></td></tr>
    <tr><th><span data-ttu-id="710cd-126">Desteklenen Hdınsight sürümleri</span><span class="sxs-lookup"><span data-stu-id="710cd-126">Supported HDInsight Versions</span></span></th>
        <td><span data-ttu-id="710cd-127">3.1, 3.2</span><span class="sxs-lookup"><span data-stu-id="710cd-127">3.1, 3.2</span></span></td></tr>
    <tr><th><span data-ttu-id="710cd-128">Değişiklik günlüğü</span><span class="sxs-lookup"><span data-stu-id="710cd-128">Change Log</span></span></th>
        <td><span data-ttu-id="710cd-129">Güncelleştirilmiş Azure Cosmos DB Java SDK'sı 1.6.0 için</span><span class="sxs-lookup"><span data-stu-id="710cd-129">Updated Azure Cosmos DB Java SDK to 1.6.0</span></span></br>
            <span data-ttu-id="710cd-130">Bir kaynak ve havuz olarak bölümlenmiş koleksiyonlar için destek eklendi</span><span class="sxs-lookup"><span data-stu-id="710cd-130">Added support for partitioned collections as both a source and sink</span></span></br>
        </td></tr>
</table>

## <span data-ttu-id="710cd-131"><a name="Prerequisites"></a>Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="710cd-131"><a name="Prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="710cd-132">Bu öğreticide yönergeleri izlemeden önce aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="710cd-132">Before following the instructions in this tutorial, ensure that you have the following:</span></span>

* <span data-ttu-id="710cd-133">Cosmos DB hesabı, bir veritabanı ve belgeleri içinde ile bir koleksiyon.</span><span class="sxs-lookup"><span data-stu-id="710cd-133">A Cosmos DB account, a database, and a collection with documents inside.</span></span> <span data-ttu-id="710cd-134">Daha fazla bilgi için bkz: [Cosmos DB ile çalışmaya başlama][getting-started].</span><span class="sxs-lookup"><span data-stu-id="710cd-134">For more information, see [Getting Started with Cosmos DB][getting-started].</span></span> <span data-ttu-id="710cd-135">Cosmos DB hesabınızla örnek veri aktarmak [Cosmos DB içeri aktarma aracını][import-data].</span><span class="sxs-lookup"><span data-stu-id="710cd-135">Import sample data into your Cosmos DB account with the [Cosmos DB import tool][import-data].</span></span>
* <span data-ttu-id="710cd-136">Üretilen iş.</span><span class="sxs-lookup"><span data-stu-id="710cd-136">Throughput.</span></span> <span data-ttu-id="710cd-137">Okuma ve yazma hdınsight'tan sayılır, Koleksiyonlarınız için ayrılan isteği birimlerinizi bulunun.</span><span class="sxs-lookup"><span data-stu-id="710cd-137">Reads and writes from HDInsight will be counted towards your allotted request units for your collections.</span></span>
* <span data-ttu-id="710cd-138">Ek bir saklı yordam içinde her kapasiteyi koleksiyonu çıktı.</span><span class="sxs-lookup"><span data-stu-id="710cd-138">Capacity for an additional stored procedure within each output collection.</span></span> <span data-ttu-id="710cd-139">Saklı yordamlar, sonuçta elde edilen belgeler aktarmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="710cd-139">The stored procedures are used for transferring resulting documents.</span></span>
* <span data-ttu-id="710cd-140">Hive, Pig ve MapReduce işleri elde edilen belgelerden kapasitesi.</span><span class="sxs-lookup"><span data-stu-id="710cd-140">Capacity for the resulting documents from the Hive, Pig, or MapReduce jobs.</span></span>
* <span data-ttu-id="710cd-141">[*İsteğe bağlı*] kapasite için ek bir koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="710cd-141">[*Optional*] Capacity for an additional collection.</span></span>

> [!WARNING]
> <span data-ttu-id="710cd-142">İşleri hiçbirini sırasında yeni bir koleksiyon oluşturulmasını önlemek için stdout sonuçları yazdırma, WASB kapsayıcıya çıkış kaydedin ve zaten mevcut bir koleksiyonu belirtin.</span><span class="sxs-lookup"><span data-stu-id="710cd-142">In order to avoid the creation of a new collection during any of the jobs, you can either print the results to stdout, save the output to your WASB container, or specify an already existing collection.</span></span> <span data-ttu-id="710cd-143">Mevcut bir koleksiyonu belirtme söz konusu olduğunda, yeni belgeler koleksiyon içinde oluşturulur ve zaten var olan belgeler, yalnızca bir çakışma varsa etkilenir *kimlikleri*.</span><span class="sxs-lookup"><span data-stu-id="710cd-143">In the case of specifying an existing collection, new documents will be created inside the collection and already existing documents will only be affected if there is a conflict in *ids*.</span></span> <span data-ttu-id="710cd-144">**Bağlayıcı kimliği çakışıyor varolan belgeleri otomatik olarak kılacak**.</span><span class="sxs-lookup"><span data-stu-id="710cd-144">**The connector will automatically overwrite existing documents with id conflicts**.</span></span> <span data-ttu-id="710cd-145">Upsert seçeneği false olarak ayarlayarak bu özelliği devre dışı bırakabilir.</span><span class="sxs-lookup"><span data-stu-id="710cd-145">You can turn off this feature by setting the upsert option to false.</span></span> <span data-ttu-id="710cd-146">Upsert false ise ve bir çakışma oluşur, Hadoop işi başarısız olur; bir kimliği çakışma hata raporlama.</span><span class="sxs-lookup"><span data-stu-id="710cd-146">If upsert is false and a conflict occurs, the Hadoop job will fail; reporting an id conflict error.</span></span>
>
>

## <span data-ttu-id="710cd-147"><a name="ProvisionHDInsight"></a>1. adım: yeni bir Hdınsight kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="710cd-147"><a name="ProvisionHDInsight"></a>Step 1: Create a new HDInsight cluster</span></span>
<span data-ttu-id="710cd-148">Bu öğretici Azure Portal'dan betik eylemi Hdınsight kümenize özelleştirmek için kullanır.</span><span class="sxs-lookup"><span data-stu-id="710cd-148">This tutorial uses Script Action from the Azure Portal to customize your HDInsight cluster.</span></span> <span data-ttu-id="710cd-149">Bu öğreticide, Hdınsight kümesi oluşturmak için Azure Portalı'nı kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="710cd-149">In this tutorial, we will use the Azure Portal to create your HDInsight cluster.</span></span> <span data-ttu-id="710cd-150">PowerShell cmdlet'lerini veya Hdınsight .NET SDK'sını kullanma hakkında daha fazla yönerge için kullanıma [özelleştirme Hdınsight kümeleri betik eylemi kullanarak] [ hdinsight-custom-provision] makalesi.</span><span class="sxs-lookup"><span data-stu-id="710cd-150">For instructions on how to use PowerShell cmdlets or the HDInsight .NET SDK, check out the [Customize HDInsight clusters using Script Action][hdinsight-custom-provision] article.</span></span>

1. <span data-ttu-id="710cd-151">Oturum [Azure Portal][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="710cd-151">Sign in to the [Azure Portal][azure-portal].</span></span>
2. <span data-ttu-id="710cd-152">Tıklatın **+ yeni** sol gezinti üst kısmındaki arama **Hdınsight** yeni bir dikey pencere en üstteki arama çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="710cd-152">Click **+ New** on the top of the left navigation, search for **HDInsight** in the top search bar on the New blade.</span></span>
3. <span data-ttu-id="710cd-153">**Hdınsight** tarafından yayımlanan **Microsoft** sonuçları üstünde görünür.</span><span class="sxs-lookup"><span data-stu-id="710cd-153">**HDInsight** published by **Microsoft** will appear at the top of the Results.</span></span> <span data-ttu-id="710cd-154">Tıklayın ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="710cd-154">Click on it and then click **Create**.</span></span>
4. <span data-ttu-id="710cd-155">Yeni Hdınsight kümesinde oluştur dikey penceresi, girin, **küme adı** seçip **abonelik** altında bu kaynak sağlamak istiyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="710cd-155">On the New HDInsight Cluster create blade, enter your **Cluster Name** and select the **Subscription** you want to provision this resource under.</span></span>

    <table border='1'>
        <tr><td><span data-ttu-id="710cd-156">Küme adı</span><span class="sxs-lookup"><span data-stu-id="710cd-156">Cluster name</span></span></td><td><span data-ttu-id="710cd-157">Küme adı.</span><span class="sxs-lookup"><span data-stu-id="710cd-157">Name the cluster.</span></span><br/>
<span data-ttu-id="710cd-158">DNS adı olmalıdır başlangıç ve bitiş bir alfasayısal karakter ile ve kısa çizgi içerebilir.</span><span class="sxs-lookup"><span data-stu-id="710cd-158">DNS name must start and end with an alpha numeric character, and may contain dashes.</span></span><br/>
<span data-ttu-id="710cd-159">Alan 3 ile 63 karakter arasında bir dize olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="710cd-159">The field must be a string between 3 and 63 characters.</span></span></td></tr>
        <tr><td><span data-ttu-id="710cd-160">Abonelik adı</span><span class="sxs-lookup"><span data-stu-id="710cd-160">Subscription Name</span></span></td>
            <td><span data-ttu-id="710cd-161">Birden fazla Azure aboneliğiniz varsa, Hdınsight kümenize barındıracak aboneliği seçin.</span><span class="sxs-lookup"><span data-stu-id="710cd-161">If you have more than one Azure Subscription, select the subscription that will host your HDInsight cluster.</span></span> </td></tr>
    </table><span data-ttu-id="710cd-162">
5.Tıklatın **küme türü seçin** ve aşağıdaki özellikleri belirtilen değerlere ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="710cd-162">
5. Click **Select Cluster Type** and set the following properties to the specified values.</span></span>

    <table border='1'>
        <tr><td><span data-ttu-id="710cd-163">Küme türü</span><span class="sxs-lookup"><span data-stu-id="710cd-163">Cluster type</span></span></td><td><span data-ttu-id="710cd-164"><strong>Hadoop</strong></span><span class="sxs-lookup"><span data-stu-id="710cd-164"><strong>Hadoop</strong></span></span></td></tr>
        <tr><td><span data-ttu-id="710cd-165">Küme katmanı</span><span class="sxs-lookup"><span data-stu-id="710cd-165">Cluster tier</span></span></td><td><span data-ttu-id="710cd-166"><strong>Standart</strong></span><span class="sxs-lookup"><span data-stu-id="710cd-166"><strong>Standard</strong></span></span></td></tr>
        <tr><td><span data-ttu-id="710cd-167">İşletim Sistemi</span><span class="sxs-lookup"><span data-stu-id="710cd-167">Operating System</span></span></td><td><span data-ttu-id="710cd-168"><strong>Windows</strong></span><span class="sxs-lookup"><span data-stu-id="710cd-168"><strong>Windows</strong></span></span></td></tr>
        <tr><td><span data-ttu-id="710cd-169">Sürüm</span><span class="sxs-lookup"><span data-stu-id="710cd-169">Version</span></span></td><td><span data-ttu-id="710cd-170">En son sürümü</span><span class="sxs-lookup"><span data-stu-id="710cd-170">latest version</span></span></td></tr>
    </table>

    <span data-ttu-id="710cd-171">Şimdi, **seçin**.</span><span class="sxs-lookup"><span data-stu-id="710cd-171">Now, click **SELECT**.</span></span>

    ![Hadoop Hdınsight ilk küme ayrıntılarını sağlayın][image-customprovision-page1]
6. <span data-ttu-id="710cd-173">Tıklayın **kimlik bilgileri** oturum açma ve Uzaktan erişim kimlik bilgilerini ayarlamak için.</span><span class="sxs-lookup"><span data-stu-id="710cd-173">Click on **Credentials** to set your login and remote access credentials.</span></span> <span data-ttu-id="710cd-174">Seçin, **küme oturum açma kullanıcı** ve **küme oturum açma parolası**.</span><span class="sxs-lookup"><span data-stu-id="710cd-174">Choose your **Cluster Login Username** and **Cluster Login Password**.</span></span>

    <span data-ttu-id="710cd-175">Kümenizi uzaktan istiyorsanız seçin *Evet* dikey pencerenin altındaki bir kullanıcı adı ve parolasını girin.</span><span class="sxs-lookup"><span data-stu-id="710cd-175">If you want to remote into your cluster, select *yes* at the bottom of the blade and provide a username and password.</span></span>
7. <span data-ttu-id="710cd-176">Tıklayın **veri kaynağı** birincil konumunuz veri erişimi için ayarlanacak.</span><span class="sxs-lookup"><span data-stu-id="710cd-176">Click on **Data Source** to set your primary location for data access.</span></span> <span data-ttu-id="710cd-177">Seçin **seçim yöntemini** ve zaten varolan bir depolama hesabını belirtin veya yeni bir tane oluşturun.</span><span class="sxs-lookup"><span data-stu-id="710cd-177">Choose the **Selection Method** and specify an already existing storage account or create a new one.</span></span>
8. <span data-ttu-id="710cd-178">Aynı dikey penceresinde belirtin bir **varsayılan kapsayıcı** ve **konumu**.</span><span class="sxs-lookup"><span data-stu-id="710cd-178">On the same blade, specify a **Default Container** and a **Location**.</span></span> <span data-ttu-id="710cd-179">Ve tıklayın **seçin**.</span><span class="sxs-lookup"><span data-stu-id="710cd-179">And, click **SELECT**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="710cd-180">Cosmos DB hesap bölgeniz daha iyi performans için yakın bir konum seçin</span><span class="sxs-lookup"><span data-stu-id="710cd-180">Select a location close to your Cosmos DB account region for better performance</span></span>
   >
   >
9. <span data-ttu-id="710cd-181">Tıklayın **fiyatlandırma** sayısını ve düğümlerinin türünü seçin.</span><span class="sxs-lookup"><span data-stu-id="710cd-181">Click on **Pricing** to select the number and type of nodes.</span></span> <span data-ttu-id="710cd-182">Varsayılan yapılandırmayı korumak ve daha sonra çalışan düğüm sayısı ölçeklendirin.</span><span class="sxs-lookup"><span data-stu-id="710cd-182">You can keep the default configuration and scale the number of Worker nodes later on.</span></span>
10. <span data-ttu-id="710cd-183">Tıklatın **isteğe bağlı yapılandırma**, ardından **betik eylemleri** isteğe bağlı yapılandırma dikey penceresinde.</span><span class="sxs-lookup"><span data-stu-id="710cd-183">Click **Optional Configuration**, then **Script Actions** in the Optional Configuration Blade.</span></span>

     <span data-ttu-id="710cd-184">Betik eylemleri Hdınsight kümenize özelleştirmek için aşağıdaki bilgileri girin.</span><span class="sxs-lookup"><span data-stu-id="710cd-184">In Script Actions, enter the following information to customize your HDInsight cluster.</span></span>

     <table border='1'>
         <tr><th><span data-ttu-id="710cd-185">Özellik</span><span class="sxs-lookup"><span data-stu-id="710cd-185">Property</span></span></th><th><span data-ttu-id="710cd-186">Değer</span><span class="sxs-lookup"><span data-stu-id="710cd-186">Value</span></span></th></tr>
         <tr><td><span data-ttu-id="710cd-187">Ad</span><span class="sxs-lookup"><span data-stu-id="710cd-187">Name</span></span></td>
             <td><span data-ttu-id="710cd-188">Betik eylemi için bir ad belirtin.</span><span class="sxs-lookup"><span data-stu-id="710cd-188">Specify a name for the script action.</span></span></td></tr>
         <tr><td><span data-ttu-id="710cd-189">Betik URI'si</span><span class="sxs-lookup"><span data-stu-id="710cd-189">Script URI</span></span></td>
             <td><span data-ttu-id="710cd-190">Küme özelleştirmek için çağrılan betik URI'si belirtin.</span><span class="sxs-lookup"><span data-stu-id="710cd-190">Specify the URI to the script that is invoked to customize the cluster.</span></span></br></br>
<span data-ttu-id="710cd-191">Lütfen girin:</span><span class="sxs-lookup"><span data-stu-id="710cd-191">Please enter:</span></span> </br> <span data-ttu-id="710cd-192"><strong>https://portalcontent.BLOB.Core.Windows.NET/scriptaction/documentdb-hadoop-installer-v04.ps1</strong>.</span><span class="sxs-lookup"><span data-stu-id="710cd-192"><strong>https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</strong>.</span></span></td></tr>
         <tr><td><span data-ttu-id="710cd-193">Baş</span><span class="sxs-lookup"><span data-stu-id="710cd-193">Head</span></span></td>
             <td><span data-ttu-id="710cd-194">Baş düğüm PowerShell betiğini çalıştırmak için onay kutusuna tıklayın.</span><span class="sxs-lookup"><span data-stu-id="710cd-194">Click the checkbox to run the PowerShell script onto the Head node.</span></span></br></br><span data-ttu-id="710cd-195">
             <strong>Bu onay kutusunu işaretleyin</strong>.</span><span class="sxs-lookup"><span data-stu-id="710cd-195">
             <strong>Check this checkbox</strong>.</span></span></td></tr>
         <tr><td><span data-ttu-id="710cd-196">Çalışan</span><span class="sxs-lookup"><span data-stu-id="710cd-196">Worker</span></span></td>
             <td><span data-ttu-id="710cd-197">Çalışan düğümüne PowerShell betiğini çalıştırmak için onay kutusuna tıklayın.</span><span class="sxs-lookup"><span data-stu-id="710cd-197">Click the checkbox to run the PowerShell script onto the Worker node.</span></span></br></br><span data-ttu-id="710cd-198">
             <strong>Bu onay kutusunu işaretleyin</strong>.</span><span class="sxs-lookup"><span data-stu-id="710cd-198">
             <strong>Check this checkbox</strong>.</span></span></td></tr>
         <tr><td><span data-ttu-id="710cd-199">Zookeeper</span><span class="sxs-lookup"><span data-stu-id="710cd-199">Zookeeper</span></span></td>
             <td><span data-ttu-id="710cd-200">Zookeeper PowerShell betiğini çalıştırmak için onay kutusuna tıklayın.</span><span class="sxs-lookup"><span data-stu-id="710cd-200">Click the checkbox to run the PowerShell script onto the Zookeeper.</span></span></br></br><span data-ttu-id="710cd-201">
             <strong>Gerekli</strong>.</span><span class="sxs-lookup"><span data-stu-id="710cd-201">
             <strong>Not needed</strong>.</span></span>
             </td></tr>
         <tr><td><span data-ttu-id="710cd-202">Parametreler</span><span class="sxs-lookup"><span data-stu-id="710cd-202">Parameters</span></span></td>
             <td><span data-ttu-id="710cd-203">Komut dosyası tarafından gerekli parametreleri belirtin.</span><span class="sxs-lookup"><span data-stu-id="710cd-203">Specify the parameters, if required by the script.</span></span></br></br><span data-ttu-id="710cd-204">
             <strong>Gerekli parametre</strong>.</span><span class="sxs-lookup"><span data-stu-id="710cd-204">
             <strong>No Parameters needed</strong>.</span></span></td></tr>
     </table><span data-ttu-id="710cd-205">
11.Ya da oluşturma yeni bir **kaynak grubu** veya varolan bir kaynak grubunu Azure aboneliğinizdeki kullanın.</span><span class="sxs-lookup"><span data-stu-id="710cd-205">
11. Create either a new **Resource Group** or use an existing Resource Group under your Azure Subscription.</span></span>
<span data-ttu-id="710cd-206">12.</span><span class="sxs-lookup"><span data-stu-id="710cd-206">12.</span></span> <span data-ttu-id="710cd-207">Şimdi denetleyin **panoya Sabitle** kendi dağıtımını izlemeye tıklatıp **oluşturma**!</span><span class="sxs-lookup"><span data-stu-id="710cd-207">Now, check **Pin to dashboard** to track its deployment and click **Create**!</span></span>

## <span data-ttu-id="710cd-208"><a name="InstallCmdlets"></a>Azure PowerShell'i 2. adım: Yükleme ve yapılandırma</span><span class="sxs-lookup"><span data-stu-id="710cd-208"><a name="InstallCmdlets"></a>Step 2: Install and configure Azure PowerShell</span></span>
1. <span data-ttu-id="710cd-209">Azure PowerShell'i yükleyin.</span><span class="sxs-lookup"><span data-stu-id="710cd-209">Install Azure PowerShell.</span></span> <span data-ttu-id="710cd-210">Yönergeler için bkz [burada][powershell-install-configure].</span><span class="sxs-lookup"><span data-stu-id="710cd-210">Instructions can be found [here][powershell-install-configure].</span></span>

   > [!NOTE]
   > <span data-ttu-id="710cd-211">Alternatif olarak, Hive sorguları olduğu için Hdınsight'ın çevrimiçi Hive Düzenleyicisi'ni kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="710cd-211">Alternatively, just for Hive queries, you can use HDInsight's online Hive Editor.</span></span> <span data-ttu-id="710cd-212">Bunu yapmak için oturumu [Azure Portal][azure-portal], tıklatın **Hdınsight** Hdınsight kümelerinizi listesini görüntülemek için sol bölmede.</span><span class="sxs-lookup"><span data-stu-id="710cd-212">To do so, sign in to the [Azure Portal][azure-portal], click **HDInsight** on the left pane to view a list of your HDInsight clusters.</span></span> <span data-ttu-id="710cd-213">Hive sorgularını çalıştırmak ve ardından istediğiniz kümeyi tıklatın **sorgu konsol**.</span><span class="sxs-lookup"><span data-stu-id="710cd-213">Click the cluster you want to run Hive queries on, and then click **Query Console**.</span></span>
   >
   >
2. <span data-ttu-id="710cd-214">Azure PowerShell Tümleşik komut dosyası ortamı açın:</span><span class="sxs-lookup"><span data-stu-id="710cd-214">Open the Azure PowerShell Integrated Scripting Environment:</span></span>

   * <span data-ttu-id="710cd-215">Windows 8 veya Windows Server 2012 veya sonraki sürümlerini çalıştıran bir bilgisayarda, yerleşik aramayı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="710cd-215">On a computer running Windows 8 or Windows Server 2012 or higher, you can use the built-in Search.</span></span> <span data-ttu-id="710cd-216">Başlangıç ekranından yazın **powershell ISE** tıklatıp **Enter**.</span><span class="sxs-lookup"><span data-stu-id="710cd-216">From the Start screen, type **powershell ise** and click **Enter**.</span></span>
   * <span data-ttu-id="710cd-217">Windows 8 veya Windows Server 2012'den önceki bir sürümünü çalıştıran bir bilgisayarda Başlat menüsünü kullanın.</span><span class="sxs-lookup"><span data-stu-id="710cd-217">On a computer running a version earlier than Windows 8 or Windows Server 2012, use the Start menu.</span></span> <span data-ttu-id="710cd-218">Başlat menüsünden yazın **komut istemi** arama kutusuna ardından sonuçlar listesinde tıklatın **komut istemi**.</span><span class="sxs-lookup"><span data-stu-id="710cd-218">From the Start menu, type **Command Prompt** in the search box, then in the list of results, click **Command Prompt**.</span></span> <span data-ttu-id="710cd-219">Komut istemine yazın **powershell_ise** tıklatıp **Enter**.</span><span class="sxs-lookup"><span data-stu-id="710cd-219">In the Command Prompt, type **powershell_ise** and click **Enter**.</span></span>
3. <span data-ttu-id="710cd-220">Azure hesabınızda ekleyin.</span><span class="sxs-lookup"><span data-stu-id="710cd-220">Add your Azure Account.</span></span>

   1. <span data-ttu-id="710cd-221">Konsol bölmesinde yazın **Add-AzureAccount** tıklatıp **Enter**.</span><span class="sxs-lookup"><span data-stu-id="710cd-221">In the Console Pane, type **Add-AzureAccount** and click **Enter**.</span></span>
   2. <span data-ttu-id="710cd-222">Azure aboneliğinizle ilişkili e-posta adresini yazın ve tıklatın **devam**.</span><span class="sxs-lookup"><span data-stu-id="710cd-222">Type in the email address associated with your Azure subscription and click **Continue**.</span></span>
   3. <span data-ttu-id="710cd-223">Azure aboneliğiniz için parolayı yazın.</span><span class="sxs-lookup"><span data-stu-id="710cd-223">Type in the password for your Azure subscription.</span></span>
   4. <span data-ttu-id="710cd-224">Tıklatın **oturum**.</span><span class="sxs-lookup"><span data-stu-id="710cd-224">Click **Sign in**.</span></span>
4. <span data-ttu-id="710cd-225">Aşağıdaki diyagramda, Azure PowerShell komut dosyası ortamı önemli bölümleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="710cd-225">The following diagram identifies the important parts of your Azure PowerShell Scripting Environment.</span></span>

    ![Azure PowerShell diyagramı][azure-powershell-diagram]

## <span data-ttu-id="710cd-227"><a name="RunHive"></a>3. adım: Cosmos DB Hdınsight ile Hive işi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="710cd-227"><a name="RunHive"></a>Step 3: Run a Hive job using Cosmos DB and HDInsight</span></span>
> [!IMPORTANT]
> <span data-ttu-id="710cd-228">Yapılandırma ayarlarınızı kullanarak < > tarafından belirtilen tüm değişkenleri doldurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="710cd-228">All variables indicated by < > must be filled in using your configuration settings.</span></span>
>
>

1. <span data-ttu-id="710cd-229">PowerShell betik bölmesinde aşağıdaki değişkenleri ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="710cd-229">Set the following variables in your PowerShell Script pane.</span></span>

        # Provide Azure subscription name, the Azure Storage account and container that is used for the default HDInsight file system.
        $subscriptionName = "<SubscriptionName>"
        $storageAccountName = "<AzureStorageAccountName>"
        $containerName = "<AzureStorageContainerName>"

        # Provide the HDInsight cluster name where you want to run the Hive job.
        $clusterName = "<HDInsightClusterName>"
2. <p><span data-ttu-id="710cd-230">Sorgu dizesi oluşturma başlayalım.</span><span class="sxs-lookup"><span data-stu-id="710cd-230">Let's begin constructing your query string.</span></span> <span data-ttu-id="710cd-231">Biz tüm belgeleri sistem tarafından oluşturulan zaman damgaları (_ts) ve bir Azure Cosmos DB koleksiyonundan benzersiz kimlikler (_rid) alır, tüm belgeleri dakikaya göre hesaplar ve ardından sonuçları geri yeni bir Azure Cosmos DB koleksiyona depolayan bir Hive sorgusu yazacaksınız.</span><span class="sxs-lookup"><span data-stu-id="710cd-231">We'll write a Hive query that takes all documents' system generated timestamps (_ts) and unique ids (_rid) from an Azure Cosmos DB collection, tallies all documents by the minute, and then stores the results back into a new Azure Cosmos DB collection.</span></span></p>

    <p><span data-ttu-id="710cd-232">İlk olarak, bir Hive tablosu bizim Azure Cosmos DB koleksiyonundan oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="710cd-232">First, let's create a Hive table from our Azure Cosmos DB collection.</span></span> <span data-ttu-id="710cd-233">Aşağıdaki kod parçacığını PowerShell betik bölmesine eklemek <strong>sonra</strong> kod parçacığı # 1.</span><span class="sxs-lookup"><span data-stu-id="710cd-233">Add the following code snippet to the PowerShell Script pane <strong>after</strong> the code snippet from #1.</span></span> <span data-ttu-id="710cd-234">Bizim belgelere yalnızca _ts isteğe bağlı DocumentDB.query t parametresi kırpma eklediğinizden emin olun ve _rid.</span><span class="sxs-lookup"><span data-stu-id="710cd-234">Make sure you include the optional DocumentDB.query parameter t trim our documents to just _ts and _rid.</span></span></p>

   > [!NOTE]
   > <span data-ttu-id="710cd-235">**DocumentDB.inputCollections adlandırma bir hata oldu.**</span><span class="sxs-lookup"><span data-stu-id="710cd-235">**Naming DocumentDB.inputCollections was not a mistake.**</span></span> <span data-ttu-id="710cd-236">Evet, bir giriş olarak birden çok koleksiyon ekleme ver:</span><span class="sxs-lookup"><span data-stu-id="710cd-236">Yes, we allow adding multiple collections as an input:</span></span> </br>
   >
   >

        '*DocumentDB.inputCollections*' = '*\<DocumentDB Input Collection Name 1\>*,*\<DocumentDB Input Collection Name 2\>*' A1A</br> The collection names are separated without spaces, using only a single comma.

        # Create a Hive table using data from DocumentDB. Pass DocumentDB the query to filter transferred data to _rid and _ts.
        $queryStringPart1 = "drop table DocumentDB_timestamps; "  +
                            "create external table DocumentDB_timestamps(id string, ts BIGINT) "  +
                            "stored by 'com.microsoft.azure.documentdb.hive.DocumentDBStorageHandler' "  +
                            "tblproperties ( " +
                                "'DocumentDB.endpoint' = '<DocumentDB Endpoint>', " +
                                "'DocumentDB.key' = '<DocumentDB Primary Key>', " +
                                "'DocumentDB.db' = '<DocumentDB Database Name>', " +
                                "'DocumentDB.inputCollections' = '<DocumentDB Input Collection Name>', " +
                                "'DocumentDB.query' = 'SELECT r._rid AS id, r._ts AS ts FROM root r' ); "

1. <span data-ttu-id="710cd-237">Ardından, çıktı koleksiyon için bir Hive tablosu oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="710cd-237">Next, let's create a Hive table for the output collection.</span></span> <span data-ttu-id="710cd-238">Çıktı belge özellikleri, ay, gün, saat, dakika ve yineleme toplam sayısı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="710cd-238">The output document properties will be the month, day, hour, minute, and the total number of occurrences.</span></span>

   > [!NOTE]
   > <span data-ttu-id="710cd-239">**Henüz bir yeniden adlandırma DocumentDB.outputCollections bir hata oldu.**</span><span class="sxs-lookup"><span data-stu-id="710cd-239">**Yet again, naming DocumentDB.outputCollections was not a mistake.**</span></span> <span data-ttu-id="710cd-240">Evet, çıkış olarak birden çok koleksiyon ekleme ver:</span><span class="sxs-lookup"><span data-stu-id="710cd-240">Yes, we allow adding multiple collections as an output:</span></span> </br>
   > <span data-ttu-id="710cd-241">'*DocumentDB.outputCollections*'='*\<DocumentDB çıkış koleksiyon adı 1\>*,*\<DocumentDB çıkış koleksiyon adı 2\>* '</span><span class="sxs-lookup"><span data-stu-id="710cd-241">'*DocumentDB.outputCollections*' = '*\<DocumentDB Output Collection Name 1\>*,*\<DocumentDB Output Collection Name 2\>*'</span></span> </br> <span data-ttu-id="710cd-242">Koleksiyon adları, boşluk, yalnızca tek bir virgül kullanarak ayrılır.</span><span class="sxs-lookup"><span data-stu-id="710cd-242">The collection names are separated without spaces, using only a single comma.</span></span> </br></br>
   > <span data-ttu-id="710cd-243">Belgeler arasında birden çok koleksiyon dağıtılmış hepsini olacaktır.</span><span class="sxs-lookup"><span data-stu-id="710cd-243">Documents will be distributed round-robin across multiple collections.</span></span> <span data-ttu-id="710cd-244">Belgeleri toplu bir koleksiyonda depolanan ve ardından belgeleri ikinci toplu sonraki toplanması ve benzeri içinde depolanır.</span><span class="sxs-lookup"><span data-stu-id="710cd-244">A batch of documents will be stored in one collection, then a second batch of documents will be stored in the next collection, and so forth.</span></span>
   >
   >

       # Create a Hive table for the output data to DocumentDB.
       $queryStringPart2 = "drop table DocumentDB_analytics; " +
                             "create external table DocumentDB_analytics(Month INT, Day INT, Hour INT, Minute INT, Total INT) " +
                             "stored by 'com.microsoft.azure.documentdb.hive.DocumentDBStorageHandler' " +
                             "tblproperties ( " +
                                 "'DocumentDB.endpoint' = '<DocumentDB Endpoint>', " +
                                 "'DocumentDB.key' = '<DocumentDB Primary Key>', " +  
                                 "'DocumentDB.db' = '<DocumentDB Database Name>', " +
                                 "'DocumentDB.outputCollections' = '<DocumentDB Output Collection Name>' ); "
2. <span data-ttu-id="710cd-245">Son olarak, şirketinizdeki belgeleri ay, gün, saat ve dakika kaydetmesini ve sonuçları çıktısına dönüştüren eklemek Hive tablosu.</span><span class="sxs-lookup"><span data-stu-id="710cd-245">Finally, let's tally the documents by month, day, hour, and minute and insert the results back into the output Hive table.</span></span>

        # GROUP BY minute, COUNT entries for each, INSERT INTO output Hive table.
        $queryStringPart3 = "INSERT INTO table DocumentDB_analytics " +
                              "SELECT month(from_unixtime(ts)) as Month, day(from_unixtime(ts)) as Day, " +
                              "hour(from_unixtime(ts)) as Hour, minute(from_unixtime(ts)) as Minute, " +
                              "COUNT(*) AS Total " +
                              "FROM DocumentDB_timestamps " +
                              "GROUP BY month(from_unixtime(ts)), day(from_unixtime(ts)), " +
                              "hour(from_unixtime(ts)) , minute(from_unixtime(ts)); "
3. <span data-ttu-id="710cd-246">Önceki sorgudan bir Hive işi tanımı oluşturmak için aşağıdaki kod parçacığını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="710cd-246">Add the following script snippet to create a Hive job definition from the previous query.</span></span>

        # Create a Hive job definition.
        $queryString = $queryStringPart1 + $queryStringPart2 + $queryStringPart3
        $hiveJobDefinition = New-AzureHDInsightHiveJobDefinition -Query $queryString

    <span data-ttu-id="710cd-247">Aynı zamanda HDFS üzerinde HiveQL komut dosyasını belirtmek için dosyası anahtarı.</span><span class="sxs-lookup"><span data-stu-id="710cd-247">You can also use the -File switch to specify a HiveQL script file on HDFS.</span></span>
4. <span data-ttu-id="710cd-248">Başlangıç saati kaydetmek ve Hive işi göndermek için aşağıdaki kod parçacığını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="710cd-248">Add the following snippet to save the start time and submit the Hive job.</span></span>

        # Save the start time and submit the job to the cluster.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $hiveJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $hiveJobDefinition
5. <span data-ttu-id="710cd-249">Hive işi tamamlanmasını beklemek için aşağıdakileri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="710cd-249">Add the following to wait for the Hive job to complete.</span></span>

        # Wait for the Hive job to complete.
        Wait-AzureHDInsightJob -Job $hiveJob -WaitTimeoutInSeconds 3600
6. <span data-ttu-id="710cd-250">Standart çıktı ve başlangıç ve bitiş zamanlarını yazdırmak için aşağıdakileri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="710cd-250">Add the following to print the standard output and the start and end times.</span></span>

        # Print the standard error, the standard output of the Hive job, and the start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $hiveJob.JobId -StandardOutput
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
7. <span data-ttu-id="710cd-251">**Çalıştırma** yeni kodunuzu!</span><span class="sxs-lookup"><span data-stu-id="710cd-251">**Run** your new script!</span></span> <span data-ttu-id="710cd-252">**Tıklatın** yeşil YÜRÜT düğmesine.</span><span class="sxs-lookup"><span data-stu-id="710cd-252">**Click** the green execute button.</span></span>
8. <span data-ttu-id="710cd-253">Sonuçları denetleyin.</span><span class="sxs-lookup"><span data-stu-id="710cd-253">Check the results.</span></span> <span data-ttu-id="710cd-254">Oturum [Azure Portal][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="710cd-254">Sign into the [Azure Portal][azure-portal].</span></span>

   1. <span data-ttu-id="710cd-255">Tıklatın <strong>Gözat</strong> sol taraftaki paneldeki.</span><span class="sxs-lookup"><span data-stu-id="710cd-255">Click <strong>Browse</strong> on the left-side panel.</span></span> </br>
   2. <span data-ttu-id="710cd-256">Tıklatın <strong>her şeyi</strong> Gözat bölmenin sağ üst adresindeki.</span><span class="sxs-lookup"><span data-stu-id="710cd-256">Click <strong>everything</strong> at the top-right of the browse panel.</span></span> </br>
   3. <span data-ttu-id="710cd-257">Bulun ve tıklatın <strong>Azure Cosmos DB hesapları</strong>.</span><span class="sxs-lookup"><span data-stu-id="710cd-257">Find and click <strong>Azure Cosmos DB Accounts</strong>.</span></span> </br>
   4. <span data-ttu-id="710cd-258">Ardından, bulma, <strong>Azure Cosmos DB hesabı</strong>, ardından <strong>Azure Cosmos DB veritabanı</strong> ve <strong>Azure Cosmos DB koleksiyonu</strong> belirtilen çıkış derlemesiyle ilişkilendirilmiş, Hive sorgusu.</span><span class="sxs-lookup"><span data-stu-id="710cd-258">Next, find your <strong>Azure Cosmos DB Account</strong>, then <strong>Azure Cosmos DB Database</strong> and your <strong>Azure Cosmos DB Collection</strong> associated with the output collection specified in your Hive query.</span></span></br>
   5. <span data-ttu-id="710cd-259">Son olarak, tıklatın <strong>belge Gezgini</strong> altında <strong>Geliştirici Araçları</strong>.</span><span class="sxs-lookup"><span data-stu-id="710cd-259">Finally, click <strong>Document Explorer</strong> underneath <strong>Developer Tools</strong>.</span></span></br></p>

   <span data-ttu-id="710cd-260">Hive Sorgunuzun sonuçlarını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="710cd-260">You will see the results of your Hive query.</span></span>

   ![Hive sorgusu sonuçları][image-hive-query-results]

## <span data-ttu-id="710cd-262"><a name="RunPig"></a>Adım 4: Cosmos DB Hdınsight ile Pig işi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="710cd-262"><a name="RunPig"></a>Step 4: Run a Pig job using Cosmos DB and HDInsight</span></span>
> [!IMPORTANT]
> <span data-ttu-id="710cd-263">Yapılandırma ayarlarınızı kullanarak < > tarafından belirtilen tüm değişkenleri doldurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="710cd-263">All variables indicated by < > must be filled in using your configuration settings.</span></span>
>
>

1. <span data-ttu-id="710cd-264">PowerShell betik bölmesinde aşağıdaki değişkenleri ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="710cd-264">Set the following variables in your PowerShell Script pane.</span></span>

        # Provide Azure subscription name.
        $subscriptionName = "Azure Subscription Name"

        # Provide HDInsight cluster name where you want to run the Pig job.
        $clusterName = "Azure HDInsight Cluster Name"
2. <p><span data-ttu-id="710cd-265">Sorgu dizesi oluşturma başlayalım.</span><span class="sxs-lookup"><span data-stu-id="710cd-265">Let's begin constructing your query string.</span></span> <span data-ttu-id="710cd-266">Biz tüm belgeleri sistem tarafından oluşturulan zaman damgaları (_ts) ve bir Azure Cosmos DB koleksiyonundan benzersiz kimlikler (_rid) alır, tüm belgeleri dakikaya göre hesaplar ve ardından sonuçları geri yeni bir Azure Cosmos DB koleksiyona depolayan bir Pig sorgu yazacaksınız.</span><span class="sxs-lookup"><span data-stu-id="710cd-266">We'll write a Pig query that takes all documents' system generated timestamps (_ts) and unique ids (_rid) from an Azure Cosmos DB collection, tallies all documents by the minute, and then stores the results back into a new Azure Cosmos DB collection.</span></span></p>
    <p><span data-ttu-id="710cd-267">İlk olarak, belge Hdınsight'a Cosmos DB'den yükleme.</span><span class="sxs-lookup"><span data-stu-id="710cd-267">First, load documents from Cosmos DB into HDInsight.</span></span> <span data-ttu-id="710cd-268">Aşağıdaki kod parçacığını PowerShell betik bölmesine eklemek <strong>sonra</strong> kod parçacığı # 1.</span><span class="sxs-lookup"><span data-stu-id="710cd-268">Add the following code snippet to the PowerShell Script pane <strong>after</strong> the code snippet from #1.</span></span> <span data-ttu-id="710cd-269">Bizim belgelere yalnızca _ts kırpma için isteğe bağlı DocumentDB sorgu parametresi için bir DocumentDB sorgu eklediğinizden emin olun ve _rid.</span><span class="sxs-lookup"><span data-stu-id="710cd-269">Make sure to add a DocumentDB query to the optional DocumentDB query parameter to trim our documents to just _ts and _rid.</span></span></p>

   > [!NOTE]
   > <span data-ttu-id="710cd-270">Evet, bir giriş olarak birden çok koleksiyon ekleme ver:</span><span class="sxs-lookup"><span data-stu-id="710cd-270">Yes, we allow adding multiple collections as an input:</span></span> </br>
   > <span data-ttu-id="710cd-271">'*\<DocumentDB giriş koleksiyon adı 1\>*,*\<DocumentDB giriş koleksiyon adı 2\>*'</span><span class="sxs-lookup"><span data-stu-id="710cd-271">'*\<DocumentDB Input Collection Name 1\>*,*\<DocumentDB Input Collection Name 2\>*'</span></span></br> <span data-ttu-id="710cd-272">Koleksiyon adları, boşluk, yalnızca tek bir virgül kullanarak ayrılır.</span><span class="sxs-lookup"><span data-stu-id="710cd-272">The collection names are separated without spaces, using only a single comma.</span></span> </b>
   >
   >

    <span data-ttu-id="710cd-273">Belgeler arasında birden çok koleksiyon dağıtılmış hepsini olacaktır.</span><span class="sxs-lookup"><span data-stu-id="710cd-273">Documents will be distributed round-robin across multiple collections.</span></span> <span data-ttu-id="710cd-274">Belgeleri toplu bir koleksiyonda depolanan ve ardından belgeleri ikinci toplu sonraki toplanması ve benzeri içinde depolanır.</span><span class="sxs-lookup"><span data-stu-id="710cd-274">A batch of documents will be stored in one collection, then a second batch of documents will be stored in the next collection, and so forth.</span></span>

        # Load data from Cosmos DB. Pass DocumentDB query to filter transferred data to _rid and _ts.
        $queryStringPart1 = "DocumentDB_timestamps = LOAD '<DocumentDB Endpoint>' USING com.microsoft.azure.documentdb.pig.DocumentDBLoader( " +
                                                        "'<DocumentDB Primary Key>', " +
                                                        "'<DocumentDB Database Name>', " +
                                                        "'<DocumentDB Input Collection Name>', " +
                                                        "'SELECT r._rid AS id, r._ts AS ts FROM root r' ); "
3. <span data-ttu-id="710cd-275">Ardından, ay, gün, saat, dakika ve yineleme toplam sayısı tarafından belgeleri şimdi kaydetmesini.</span><span class="sxs-lookup"><span data-stu-id="710cd-275">Next, let's tally the documents by the month, day, hour, minute, and the total number of occurrences.</span></span>

       # GROUP BY minute and COUNT entries for each.
       $queryStringPart2 = "timestamp_record = FOREACH DocumentDB_timestamps GENERATE `$0#'id' as id:int, ToDate((long)(`$0#'ts') * 1000) as timestamp:datetime; " +
                           "by_minute = GROUP timestamp_record BY (GetYear(timestamp), GetMonth(timestamp), GetDay(timestamp), GetHour(timestamp), GetMinute(timestamp)); " +
                           "by_minute_count = FOREACH by_minute GENERATE FLATTEN(group) as (Year:int, Month:int, Day:int, Hour:int, Minute:int), COUNT(timestamp_record) as Total:int; "
4. <span data-ttu-id="710cd-276">Son olarak, şirketinizdeki sonuçları bizim yeni çıkış koleksiyona depolar.</span><span class="sxs-lookup"><span data-stu-id="710cd-276">Finally, let's store the results into our new output collection.</span></span>

   > [!NOTE]
   > <span data-ttu-id="710cd-277">Evet, çıkış olarak birden çok koleksiyon ekleme ver:</span><span class="sxs-lookup"><span data-stu-id="710cd-277">Yes, we allow adding multiple collections as an output:</span></span> </br>
   > <span data-ttu-id="710cd-278">'\<DocumentDB çıkış koleksiyon adı 1\>,\<DocumentDB çıkış koleksiyon adı 2\>'</span><span class="sxs-lookup"><span data-stu-id="710cd-278">'\<DocumentDB Output Collection Name 1\>,\<DocumentDB Output Collection Name 2\>'</span></span></br> <span data-ttu-id="710cd-279">Koleksiyon adları, boşluk, yalnızca tek bir virgül kullanarak ayrılır.</span><span class="sxs-lookup"><span data-stu-id="710cd-279">The collection names are separated without spaces, using only a single comma.</span></span></br>
   > <span data-ttu-id="710cd-280">Belgeler arasında birden çok koleksiyon dağıtılmış hepsini olacaktır.</span><span class="sxs-lookup"><span data-stu-id="710cd-280">Documents will be distributed round-robin across the multiple collections.</span></span> <span data-ttu-id="710cd-281">Belgeleri toplu bir koleksiyonda depolanan ve ardından belgeleri ikinci toplu sonraki toplanması ve benzeri içinde depolanır.</span><span class="sxs-lookup"><span data-stu-id="710cd-281">A batch of documents will be stored in one collection, then a second batch of documents will be stored in the next collection, and so forth.</span></span>
   >
   >

        # Store output data to Cosmos DB.
        $queryStringPart3 = "STORE by_minute_count INTO '<DocumentDB Endpoint>' " +
                            "USING com.microsoft.azure.documentdb.pig.DocumentDBStorage( " +
                                "'<DocumentDB Primary Key>', " +
                                "'<DocumentDB Database Name>', " +
                                "'<DocumentDB Output Collection Name>'); "
5. <span data-ttu-id="710cd-282">Önceki sorgudan bir Pig proje tanımı oluşturmak için aşağıdaki kod parçacığını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="710cd-282">Add the following script snippet to create a Pig job definition from the previous query.</span></span>

        # Create a Pig job definition.
        $queryString = $queryStringPart1 + $queryStringPart2 + $queryStringPart3
        $pigJobDefinition = New-AzureHDInsightPigJobDefinition -Query $queryString -StatusFolder $statusFolder

    <span data-ttu-id="710cd-283">Aynı zamanda HDFS üzerinde Pig betiği belirtmek için dosyası anahtarı.</span><span class="sxs-lookup"><span data-stu-id="710cd-283">You can also use the -File switch to specify a Pig script file on HDFS.</span></span>
6. <span data-ttu-id="710cd-284">Başlangıç saati kaydetmek ve Pig işi göndermek için aşağıdaki kod parçacığını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="710cd-284">Add the following snippet to save the start time and submit the Pig job.</span></span>

        # Save the start time and submit the job to the cluster.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $pigJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $pigJobDefinition
7. <span data-ttu-id="710cd-285">Pig işi tamamlamak beklenecek aşağıdakileri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="710cd-285">Add the following to wait for the Pig job to complete.</span></span>

        # Wait for the Pig job to complete.
        Wait-AzureHDInsightJob -Job $pigJob -WaitTimeoutInSeconds 3600
8. <span data-ttu-id="710cd-286">Standart çıktı ve başlangıç ve bitiş zamanlarını yazdırmak için aşağıdakileri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="710cd-286">Add the following to print the standard output and the start and end times.</span></span>

        # Print the standard error, the standard output of the Hive job, and the start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $pigJob.JobId -StandardOutput
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
9. <span data-ttu-id="710cd-287">**Çalıştırma** yeni kodunuzu!</span><span class="sxs-lookup"><span data-stu-id="710cd-287">**Run** your new script!</span></span> <span data-ttu-id="710cd-288">**Tıklatın** yeşil YÜRÜT düğmesine.</span><span class="sxs-lookup"><span data-stu-id="710cd-288">**Click** the green execute button.</span></span>
10. <span data-ttu-id="710cd-289">Sonuçları denetleyin.</span><span class="sxs-lookup"><span data-stu-id="710cd-289">Check the results.</span></span> <span data-ttu-id="710cd-290">Oturum [Azure Portal][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="710cd-290">Sign into the [Azure Portal][azure-portal].</span></span>

    1. <span data-ttu-id="710cd-291">Tıklatın <strong>Gözat</strong> sol taraftaki paneldeki.</span><span class="sxs-lookup"><span data-stu-id="710cd-291">Click <strong>Browse</strong> on the left-side panel.</span></span> </br>
    2. <span data-ttu-id="710cd-292">Tıklatın <strong>her şeyi</strong> Gözat bölmenin sağ üst adresindeki.</span><span class="sxs-lookup"><span data-stu-id="710cd-292">Click <strong>everything</strong> at the top-right of the browse panel.</span></span> </br>
    3. <span data-ttu-id="710cd-293">Bulun ve tıklatın <strong>Azure Cosmos DB hesapları</strong>.</span><span class="sxs-lookup"><span data-stu-id="710cd-293">Find and click <strong>Azure Cosmos DB Accounts</strong>.</span></span> </br>
    4. <span data-ttu-id="710cd-294">Ardından, bulma, <strong>Azure Cosmos DB hesabı</strong>, ardından <strong>Azure Cosmos DB veritabanı</strong> ve <strong>Azure Cosmos DB koleksiyonu</strong> belirtilen çıkış derlemesiyle ilişkilendirilmiş, Pig sorgu.</span><span class="sxs-lookup"><span data-stu-id="710cd-294">Next, find your <strong>Azure Cosmos DB Account</strong>, then <strong>Azure Cosmos DB Database</strong> and your <strong>Azure Cosmos DB Collection</strong> associated with the output collection specified in your Pig query.</span></span></br>
    5. <span data-ttu-id="710cd-295">Son olarak, tıklatın <strong>belge Gezgini</strong> altında <strong>Geliştirici Araçları</strong>.</span><span class="sxs-lookup"><span data-stu-id="710cd-295">Finally, click <strong>Document Explorer</strong> underneath <strong>Developer Tools</strong>.</span></span></br></p>

    <span data-ttu-id="710cd-296">Pig Sorgunuzun sonuçlarını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="710cd-296">You will see the results of your Pig query.</span></span>

    ![Pig sorgu sonuçları][image-pig-query-results]

## <span data-ttu-id="710cd-298"><a name="RunMapReduce"></a>5. adım: Azure Cosmos DB Hdınsight ile MapReduce işi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="710cd-298"><a name="RunMapReduce"></a>Step 5: Run a MapReduce job using Azure Cosmos DB and HDInsight</span></span>
1. <span data-ttu-id="710cd-299">PowerShell betik bölmesinde aşağıdaki değişkenleri ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="710cd-299">Set the following variables in your PowerShell Script pane.</span></span>

        $subscriptionName = "<SubscriptionName>"   # Azure subscription name
        $clusterName = "<ClusterName>"             # HDInsight cluster name
2. <span data-ttu-id="710cd-300">Biz, Azure Cosmos DB koleksiyondaki her bir belge özellik için yineleme sayısı hesaplayan bir MapReduce işi yürüteceksiniz.</span><span class="sxs-lookup"><span data-stu-id="710cd-300">We'll execute a MapReduce job that tallies the number of occurrences for each Document property from your Azure Cosmos DB collection.</span></span> <span data-ttu-id="710cd-301">Bu kod parçacığını ekleyin **sonra** Yukarıdaki kod parçacığında.</span><span class="sxs-lookup"><span data-stu-id="710cd-301">Add this script snippet **after** the snippet above.</span></span>

        # Define the MapReduce job.
        $TallyPropertiesJobDefinition = New-AzureHDInsightMapReduceJobDefinition -JarFile "wasb:///example/jars/TallyProperties-v01.jar" -ClassName "TallyProperties" -Arguments "<DocumentDB Endpoint>","<DocumentDB Primary Key>", "<DocumentDB Database Name>","<DocumentDB Input Collection Name>","<DocumentDB Output Collection Name>","<[Optional] DocumentDB Query>"

   > [!NOTE]
   > <span data-ttu-id="710cd-302">TallyProperties v01.jar Cosmos DB Hadoop bağlayıcı özel yüklenmesiyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="710cd-302">TallyProperties-v01.jar comes with the custom installation of the Cosmos DB Hadoop Connector.</span></span>
   >
   >
3. <span data-ttu-id="710cd-303">MapReduce işi göndermek için aşağıdaki komutu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="710cd-303">Add the following command to submit the MapReduce job.</span></span>

        # Save the start time and submit the job.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $TallyPropertiesJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $TallyPropertiesJobDefinition | Wait-AzureHDInsightJob -WaitTimeoutInSeconds 3600  

    <span data-ttu-id="710cd-304">MapReduce işi tanım yanı sıra, aynı zamanda MapReduce işi ve kimlik bilgileri çalıştırmak istediğiniz Hdınsight küme adı sağlayın.</span><span class="sxs-lookup"><span data-stu-id="710cd-304">In addition to the MapReduce job definition, you also provide the HDInsight cluster name where you want to run the MapReduce job, and the credentials.</span></span> <span data-ttu-id="710cd-305">Başlangıç AzureHDInsightJob zaman bir çağrıdır.</span><span class="sxs-lookup"><span data-stu-id="710cd-305">The Start-AzureHDInsightJob is an asynchronized call.</span></span> <span data-ttu-id="710cd-306">İş tamamlandığında denetlemek için kullanın *bekleme AzureHDInsightJob* cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="710cd-306">To check the completion of the job, use the *Wait-AzureHDInsightJob* cmdlet.</span></span>
4. <span data-ttu-id="710cd-307">MapReduce işi çalıştıran ile hataları denetlemek için aşağıdaki komutu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="710cd-307">Add the following command to check any errors with running the MapReduce job.</span></span>

        # Get the job output and print the start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $TallyPropertiesJob.JobId -StandardError
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
5. <span data-ttu-id="710cd-308">**Çalıştırma** yeni kodunuzu!</span><span class="sxs-lookup"><span data-stu-id="710cd-308">**Run** your new script!</span></span> <span data-ttu-id="710cd-309">**Tıklatın** yeşil YÜRÜT düğmesine.</span><span class="sxs-lookup"><span data-stu-id="710cd-309">**Click** the green execute button.</span></span>
6. <span data-ttu-id="710cd-310">Sonuçları denetleyin.</span><span class="sxs-lookup"><span data-stu-id="710cd-310">Check the results.</span></span> <span data-ttu-id="710cd-311">Oturum [Azure Portal][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="710cd-311">Sign into the [Azure Portal][azure-portal].</span></span>

   1. <span data-ttu-id="710cd-312">Tıklatın <strong>Gözat</strong> sol taraftaki paneldeki.</span><span class="sxs-lookup"><span data-stu-id="710cd-312">Click <strong>Browse</strong> on the left-side panel.</span></span>
   2. <span data-ttu-id="710cd-313">Tıklatın <strong>her şeyi</strong> Gözat bölmenin sağ üst adresindeki.</span><span class="sxs-lookup"><span data-stu-id="710cd-313">Click <strong>everything</strong> at the top-right of the browse panel.</span></span>
   3. <span data-ttu-id="710cd-314">Bulun ve tıklatın <strong>Azure Cosmos DB hesapları</strong>.</span><span class="sxs-lookup"><span data-stu-id="710cd-314">Find and click <strong>Azure Cosmos DB Accounts</strong>.</span></span>
   4. <span data-ttu-id="710cd-315">Ardından, bulma, <strong>Azure Cosmos DB hesabı</strong>, ardından <strong>Azure Cosmos DB veritabanı</strong> ve <strong>Azure Cosmos DB koleksiyonu</strong> belirtilen çıkış derlemesiyle ilişkilendirilmiş, MapReduce işi.</span><span class="sxs-lookup"><span data-stu-id="710cd-315">Next, find your <strong>Azure Cosmos DB Account</strong>, then <strong>Azure Cosmos DB Database</strong> and your <strong>Azure Cosmos DB Collection</strong> associated with the output collection specified in your MapReduce job.</span></span>
   5. <span data-ttu-id="710cd-316">Son olarak, tıklatın <strong>belge Gezgini</strong> altında <strong>Geliştirici Araçları</strong>.</span><span class="sxs-lookup"><span data-stu-id="710cd-316">Finally, click <strong>Document Explorer</strong> underneath <strong>Developer Tools</strong>.</span></span>

      <span data-ttu-id="710cd-317">MapReduce işinizin sonuçları görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="710cd-317">You will see the results of your MapReduce job.</span></span>

      ![MapReduce sorgu sonuçları][image-mapreduce-query-results]

## <span data-ttu-id="710cd-319"><a name="NextSteps"></a>Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="710cd-319"><a name="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="710cd-320">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="710cd-320">Congratulations!</span></span> <span data-ttu-id="710cd-321">Yalnızca Azure Cosmos DB ve Hdınsight kullanarak, ilk Hive, Pig ve MapReduce işleri çalıştırdığınız.</span><span class="sxs-lookup"><span data-stu-id="710cd-321">You just ran your first Hive, Pig, and MapReduce jobs using Azure Cosmos DB and HDInsight.</span></span>

<span data-ttu-id="710cd-322">Bizim açık kaynaklıdır bizim Hadoop bağlayıcı.</span><span class="sxs-lookup"><span data-stu-id="710cd-322">We have open sourced our Hadoop Connector.</span></span> <span data-ttu-id="710cd-323">İlginizi çekiyorsa üzerinde katkıda bulunabilirsiniz [GitHub][github].</span><span class="sxs-lookup"><span data-stu-id="710cd-323">If you're interested, you can contribute on [GitHub][github].</span></span>

<span data-ttu-id="710cd-324">Daha fazla bilgi için aşağıdaki makalelere bakın:</span><span class="sxs-lookup"><span data-stu-id="710cd-324">To learn more, see the following articles:</span></span>

* <span data-ttu-id="710cd-325">[Documentdb ile bir Java uygulaması geliştirme][documentdb-java-application]</span><span class="sxs-lookup"><span data-stu-id="710cd-325">[Develop a Java application with Documentdb][documentdb-java-application]</span></span>
* <span data-ttu-id="710cd-326">[Hdınsight'ta Hadoop için Java MapReduce programlar geliştirmek][hdinsight-develop-deploy-java-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="710cd-326">[Develop Java MapReduce programs for Hadoop in HDInsight][hdinsight-develop-deploy-java-mapreduce]</span></span>
* <span data-ttu-id="710cd-327">[Hadoop ile hdınsight'ta Hive mobil ahize kullanımını çözümleme için kullanmaya başlama][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="710cd-327">[Get started using Hadoop with Hive in HDInsight to analyze mobile handset use][hdinsight-get-started]</span></span>
* <span data-ttu-id="710cd-328">[Hdınsight ile MapReduce kullanma][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="710cd-328">[Use MapReduce with HDInsight][hdinsight-use-mapreduce]</span></span>
* <span data-ttu-id="710cd-329">[HDInsight ile Hive kullanma][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="710cd-329">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="710cd-330">[HDInsight ile Pig kullanma][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="710cd-330">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="710cd-331">[Betik eylemi kullanarak Hdınsight kümelerini özelleştirme][hdinsight-hadoop-customize-cluster]</span><span class="sxs-lookup"><span data-stu-id="710cd-331">[Customize HDInsight clusters using Script Action][hdinsight-hadoop-customize-cluster]</span></span>

[apache-hadoop]: http://hadoop.apache.org/
[apache-hadoop-doc]: http://hadoop.apache.org/docs/current/
[apache-hive]: http://hive.apache.org/
[apache-pig]: http://pig.apache.org/
[getting-started]: documentdb-get-started.md

[azure-portal]: https://portal.azure.com/
[azure-powershell-diagram]: ./media/run-hadoop-with-hdinsight/azurepowershell-diagram-med.png

[hdinsight-samples]: http://portalcontent.blob.core.windows.net/samples/documentdb-hdinsight-samples.zip
[github]: https://github.com/Azure/azure-documentdb-hadoop
[documentdb-java-application]: documentdb-java-application.md
[import-data]: import-data.md

[hdinsight-custom-provision]: ../hdinsight/hdinsight-provision-clusters.md
[hdinsight-develop-deploy-java-mapreduce]: ../hdinsight/hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-hadoop-customize-cluster]: ../hdinsight/hdinsight-hadoop-customize-cluster.md
[hdinsight-get-started]: ../hdinsight/hdinsight-hadoop-tutorial-get-started-windows.md
[hdinsight-storage]: ../hdinsight/hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-hive]: ../hdinsight/hdinsight-use-hive.md
[hdinsight-use-mapreduce]: ../hdinsight/hdinsight-use-mapreduce.md
[hdinsight-use-pig]: ../hdinsight/hdinsight-use-pig.md

[image-customprovision-page1]: ./media/run-hadoop-with-hdinsight/customprovision-page1.png
[image-hive-query-results]: ./media/run-hadoop-with-hdinsight/hivequeryresults.PNG
[image-mapreduce-query-results]: ./media/run-hadoop-with-hdinsight/mapreducequeryresults.PNG
[image-pig-query-results]: ./media/run-hadoop-with-hdinsight/pigqueryresults.PNG

[powershell-install-configure]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0
