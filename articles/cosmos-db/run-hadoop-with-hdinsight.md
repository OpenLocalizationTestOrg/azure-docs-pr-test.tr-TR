---
title: "bir Hadoop aaaRun iş Azure Cosmos DB ve Hdınsight kullanarak | Microsoft Docs"
description: "Azure Cosmos DB ve Azure Hdınsight ile nasıl toorun basit bir Hive, Pig ve MapReduce işi öğrenin."
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
ms.openlocfilehash: 2e27499f2c4ba951af9a1ade1bcc9c1b6d298fcd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="3a8f1-103"><a name="Azure Cosmos DB-HDInsight"></a>Azure Cosmos DB ve Hdınsight kullanarak bir Apache Hive, Pig veya Hadoop işini çalıştır</span><span class="sxs-lookup"><span data-stu-id="3a8f1-103"><a name="Azure Cosmos DB-HDInsight"></a>Run an Apache Hive, Pig, or Hadoop job using Azure Cosmos DB and HDInsight</span></span>
<span data-ttu-id="3a8f1-104">Bu öğretici şunların nasıl yapıldığını gösterir toorun [Apache Hive][apache-hive], [Apache Pig][apache-pig], ve [Apache Hadoop] [ apache-hadoop] Cosmos veritabanı Hadoop Bağlayıcısı ile MapReduce işleri Azure hdınsight'ta.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-104">This tutorial shows you how toorun [Apache Hive][apache-hive], [Apache Pig][apache-pig], and [Apache Hadoop][apache-hadoop] MapReduce jobs on Azure HDInsight with Cosmos DB's Hadoop connector.</span></span> <span data-ttu-id="3a8f1-105">Cosmos veritabanı Hadoop Bağlayıcısı Cosmos DB tooact hem kaynak hem de Hive, Pig ve MapReduce işleri için havuz olarak sağlar.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-105">Cosmos DB's Hadoop connector allows Cosmos DB tooact as both a source and sink for Hive, Pig, and MapReduce jobs.</span></span> <span data-ttu-id="3a8f1-106">Bu öğretici için Hadoop işlerini Cosmos DB hello veri kaynağı ve hedef kullanır.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-106">This tutorial will use Cosmos DB as both hello data source and destination for Hadoop jobs.</span></span>

<span data-ttu-id="3a8f1-107">Bu öğreticiyi tamamladıktan sonra aşağıdaki soruları mümkün tooanswer hello olması:</span><span class="sxs-lookup"><span data-stu-id="3a8f1-107">After completing this tutorial, you'll be able tooanswer hello following questions:</span></span>

* <span data-ttu-id="3a8f1-108">Cosmos Hive, Pig ve MapReduce işi kullanılarak DB'den nasıl veri yükleme?</span><span class="sxs-lookup"><span data-stu-id="3a8f1-108">How do I load data from Cosmos DB using a Hive, Pig, or MapReduce job?</span></span>
* <span data-ttu-id="3a8f1-109">Cosmos Hive, Pig ve MapReduce işi kullanılarak DB'de nasıl veri depoluyor?</span><span class="sxs-lookup"><span data-stu-id="3a8f1-109">How do I store data in Cosmos DB using a Hive, Pig, or MapReduce job?</span></span>

<span data-ttu-id="3a8f1-110">Video, biz Cosmos DB Hdınsight ile Hive işi çalıştırdığı aşağıdaki hello izleyerek çalışmaya başlamanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-110">We recommend getting started by watching hello following video, where we run through a Hive job using Cosmos DB and HDInsight.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Use-Azure-DocumentDB-Hadoop-Connector-with-Azure-HDInsight/player]
>
>

<span data-ttu-id="3a8f1-111">Ardından, toothis makalesi, nasıl Cosmos DB verilerinizde analytics işlerine çalıştırabilirsiniz hello tam Ayrıntılar burada alırsınız döndür.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-111">Then, return toothis article, where you'll receive hello full details on how you can run analytics jobs on your Cosmos DB data.</span></span>

> [!TIP]
> <span data-ttu-id="3a8f1-112">Bu öğretici, Apache Hadoop, Hive ve/veya Pig kullanma konusunda deneyim sahibi olduğunuzu varsayar.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-112">This tutorial assumes that you have prior experience using Apache Hadoop, Hive, and/or Pig.</span></span> <span data-ttu-id="3a8f1-113">Yeni tooApache Hadoop, Hive veya Pig varsa, hello ziyaret öneririz [Apache Hadoop belgeleri][apache-hadoop-doc].</span><span class="sxs-lookup"><span data-stu-id="3a8f1-113">If you are new tooApache Hadoop, Hive, and Pig, we recommend visiting hello [Apache Hadoop documentation][apache-hadoop-doc].</span></span> <span data-ttu-id="3a8f1-114">Bu öğreticinin ayrıca Cosmos DB ile konusunda deneyim sahibi ve bir Cosmos DB hesabına sahip olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-114">This tutorial also assumes that you have prior experience with Cosmos DB and have a Cosmos DB account.</span></span> <span data-ttu-id="3a8f1-115">Lütfen yeni tooCosmos DB ya Cosmos DB hesabınız varsa kullanıma bizim [Başlarken] [ getting-started] sayfası.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-115">If you are new tooCosmos DB or you do not have a Cosmos DB account, please check out our [Getting Started][getting-started] page.</span></span>
>
>

<span data-ttu-id="3a8f1-116">Öğretici hello ve Hive, Pig ve MapReduce tooget hello tam örnek PowerShell komut dosyaları yalnızca istediğiniz zaman toocomplete yok mu?</span><span class="sxs-lookup"><span data-stu-id="3a8f1-116">Don't have time toocomplete hello tutorial and just want tooget hello full sample PowerShell scripts for Hive, Pig, and MapReduce?</span></span> <span data-ttu-id="3a8f1-117">Bir sorun bunları getirmek [burada][hdinsight-samples].</span><span class="sxs-lookup"><span data-stu-id="3a8f1-117">Not a problem, get them [here][hdinsight-samples].</span></span> <span data-ttu-id="3a8f1-118">Merhaba indirme Ayrıca bu örnekleri için hello hql, pig ve java dosyaları içerir.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-118">hello download also contains hello hql, pig, and java files for these samples.</span></span>

## <span data-ttu-id="3a8f1-119"><a name="NewestVersion"></a>En yeni sürümü</span><span class="sxs-lookup"><span data-stu-id="3a8f1-119"><a name="NewestVersion"></a>Newest Version</span></span>
<table border='1'>
    <tr><th><span data-ttu-id="3a8f1-120">Hadoop Bağlayıcısı sürüm</span><span class="sxs-lookup"><span data-stu-id="3a8f1-120">Hadoop Connector Version</span></span></th>
        <td><span data-ttu-id="3a8f1-121">1.2.0</span><span class="sxs-lookup"><span data-stu-id="3a8f1-121">1.2.0</span></span></td></tr>
    <tr><th><span data-ttu-id="3a8f1-122">Betik URI'si</span><span class="sxs-lookup"><span data-stu-id="3a8f1-122">Script Uri</span></span></th>
        <td><span data-ttu-id="3a8f1-123">https://portalcontent.BLOB.Core.Windows.NET/scriptaction/documentdb-hadoop-installer-v04.ps1</span><span class="sxs-lookup"><span data-stu-id="3a8f1-123">https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</span></span></td></tr>
    <tr><th><span data-ttu-id="3a8f1-124">Değiştirilme tarihi</span><span class="sxs-lookup"><span data-stu-id="3a8f1-124">Date Modified</span></span></th>
        <td><span data-ttu-id="3a8f1-125">04/26/2016</span><span class="sxs-lookup"><span data-stu-id="3a8f1-125">04/26/2016</span></span></td></tr>
    <tr><th><span data-ttu-id="3a8f1-126">Desteklenen Hdınsight sürümleri</span><span class="sxs-lookup"><span data-stu-id="3a8f1-126">Supported HDInsight Versions</span></span></th>
        <td><span data-ttu-id="3a8f1-127">3.1, 3.2</span><span class="sxs-lookup"><span data-stu-id="3a8f1-127">3.1, 3.2</span></span></td></tr>
    <tr><th><span data-ttu-id="3a8f1-128">Değişiklik günlüğü</span><span class="sxs-lookup"><span data-stu-id="3a8f1-128">Change Log</span></span></th>
        <td><span data-ttu-id="3a8f1-129">Güncelleştirilmiş Azure Cosmos DB Java SDK too1.6.0</span><span class="sxs-lookup"><span data-stu-id="3a8f1-129">Updated Azure Cosmos DB Java SDK too1.6.0</span></span></br>
            <span data-ttu-id="3a8f1-130">Bir kaynak ve havuz olarak bölümlenmiş koleksiyonlar için destek eklendi</span><span class="sxs-lookup"><span data-stu-id="3a8f1-130">Added support for partitioned collections as both a source and sink</span></span></br>
        </td></tr>
</table>

## <span data-ttu-id="3a8f1-131"><a name="Prerequisites"></a>Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="3a8f1-131"><a name="Prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="3a8f1-132">Bu öğreticide Hello yönergeleri izlemeden önce hello aşağıdaki sahip olduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="3a8f1-132">Before following hello instructions in this tutorial, ensure that you have hello following:</span></span>

* <span data-ttu-id="3a8f1-133">Cosmos DB hesabı, bir veritabanı ve belgeleri içinde ile bir koleksiyon.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-133">A Cosmos DB account, a database, and a collection with documents inside.</span></span> <span data-ttu-id="3a8f1-134">Daha fazla bilgi için bkz: [Cosmos DB ile çalışmaya başlama][getting-started].</span><span class="sxs-lookup"><span data-stu-id="3a8f1-134">For more information, see [Getting Started with Cosmos DB][getting-started].</span></span> <span data-ttu-id="3a8f1-135">Cosmos DB hesabınızla hello örnek veri aktarmak [Cosmos DB içeri aktarma aracını][import-data].</span><span class="sxs-lookup"><span data-stu-id="3a8f1-135">Import sample data into your Cosmos DB account with hello [Cosmos DB import tool][import-data].</span></span>
* <span data-ttu-id="3a8f1-136">Üretilen iş.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-136">Throughput.</span></span> <span data-ttu-id="3a8f1-137">Okuma ve yazma hdınsight'tan sayılır, Koleksiyonlarınız için ayrılan isteği birimlerinizi bulunun.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-137">Reads and writes from HDInsight will be counted towards your allotted request units for your collections.</span></span>
* <span data-ttu-id="3a8f1-138">Ek bir saklı yordam içinde her kapasiteyi koleksiyonu çıktı.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-138">Capacity for an additional stored procedure within each output collection.</span></span> <span data-ttu-id="3a8f1-139">Merhaba depolanan yordamlar, sonuçta elde edilen belgeler aktarmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-139">hello stored procedures are used for transferring resulting documents.</span></span>
* <span data-ttu-id="3a8f1-140">Merhaba elde edilen hello Hive, Pig ve MapReduce işleri belgelerden kapasitesi.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-140">Capacity for hello resulting documents from hello Hive, Pig, or MapReduce jobs.</span></span>
* <span data-ttu-id="3a8f1-141">[*İsteğe bağlı*] kapasite için ek bir koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-141">[*Optional*] Capacity for an additional collection.</span></span>

> [!WARNING]
> <span data-ttu-id="3a8f1-142">Sipariş tooavoid hello oluşturulmasında hello işleri hiçbirini sırasında yeni bir koleksiyon, hello sonuçları toostdout yazdırma, hello çıktı tooyour WASB kapsayıcısını kaydedin veya zaten mevcut bir koleksiyonu belirtin.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-142">In order tooavoid hello creation of a new collection during any of hello jobs, you can either print hello results toostdout, save hello output tooyour WASB container, or specify an already existing collection.</span></span> <span data-ttu-id="3a8f1-143">Mevcut bir koleksiyonu belirtmenin hello durumda da, yeni belgeler hello koleksiyon içinde oluşturulur ve zaten var olan belgeler, yalnızca bir çakışma varsa etkilenir *kimlikleri*.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-143">In hello case of specifying an existing collection, new documents will be created inside hello collection and already existing documents will only be affected if there is a conflict in *ids*.</span></span> <span data-ttu-id="3a8f1-144">**Merhaba bağlayıcı otomatik olarak üzerine yazılacak varolan belgeleri kimliği çakışıyor**.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-144">**hello connector will automatically overwrite existing documents with id conflicts**.</span></span> <span data-ttu-id="3a8f1-145">Merhaba upsert seçeneği toofalse ayarlayarak bu özelliği devre dışı bırakabilir.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-145">You can turn off this feature by setting hello upsert option toofalse.</span></span> <span data-ttu-id="3a8f1-146">Upsert false ise ve bir çakışma oluşur, hello Hadoop işi başarısız olur; bir kimliği çakışma hata raporlama.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-146">If upsert is false and a conflict occurs, hello Hadoop job will fail; reporting an id conflict error.</span></span>
>
>

## <span data-ttu-id="3a8f1-147"><a name="ProvisionHDInsight"></a>1. adım: yeni bir Hdınsight kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="3a8f1-147"><a name="ProvisionHDInsight"></a>Step 1: Create a new HDInsight cluster</span></span>
<span data-ttu-id="3a8f1-148">Bu öğretici, Hdınsight kümenize hello Azure Portal toocustomize betik eylemi kullanır.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-148">This tutorial uses Script Action from hello Azure Portal toocustomize your HDInsight cluster.</span></span> <span data-ttu-id="3a8f1-149">Bu öğreticide, Hdınsight kümenize hello Azure Portal toocreate kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-149">In this tutorial, we will use hello Azure Portal toocreate your HDInsight cluster.</span></span> <span data-ttu-id="3a8f1-150">Yönergeler için nasıl toouse PowerShell cmdlet'lerini veya Hdınsight .NET SDK'sı, hello kullanıma [özelleştirme Hdınsight kümeleri betik eylemi kullanarak] [ hdinsight-custom-provision] makalesi.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-150">For instructions on how toouse PowerShell cmdlets or hello HDInsight .NET SDK, check out the [Customize HDInsight clusters using Script Action][hdinsight-custom-provision] article.</span></span>

1. <span data-ttu-id="3a8f1-151">İçinde toohello oturum [Azure Portal][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="3a8f1-151">Sign in toohello [Azure Portal][azure-portal].</span></span>
2. <span data-ttu-id="3a8f1-152">Tıklatın **+ yeni** sol gezinti hello hello üstte arama **Hdınsight** hello yeni dikey penceresinde hello en üstteki arama çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-152">Click **+ New** on hello top of hello left navigation, search for **HDInsight** in hello top search bar on hello New blade.</span></span>
3. <span data-ttu-id="3a8f1-153">**Hdınsight** tarafından yayımlanan **Microsoft** hello sonuçları hello üstünde görünür.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-153">**HDInsight** published by **Microsoft** will appear at hello top of hello Results.</span></span> <span data-ttu-id="3a8f1-154">Tıklayın ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-154">Click on it and then click **Create**.</span></span>
4. <span data-ttu-id="3a8f1-155">Merhaba yeni Hdınsight kümesi üzerinde oluştur dikey penceresi, girin, **küme adı** ve select hello **abonelik** altında bu kaynak tooprovision istiyor.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-155">On hello New HDInsight Cluster create blade, enter your **Cluster Name** and select hello **Subscription** you want tooprovision this resource under.</span></span>

    <table border='1'>
        <tr><td><span data-ttu-id="3a8f1-156">Küme adı</span><span class="sxs-lookup"><span data-stu-id="3a8f1-156">Cluster name</span></span></td><td><span data-ttu-id="3a8f1-157">Merhaba küme adı.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-157">Name hello cluster.</span></span><br/>
<span data-ttu-id="3a8f1-158">DNS adı olmalıdır başlangıç ve bitiş bir alfasayısal karakter ile ve kısa çizgi içerebilir.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-158">DNS name must start and end with an alpha numeric character, and may contain dashes.</span></span><br/>
<span data-ttu-id="3a8f1-159">Merhaba alan 3 ile 63 karakter arasında bir dize olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-159">hello field must be a string between 3 and 63 characters.</span></span></td></tr>
        <tr><td><span data-ttu-id="3a8f1-160">Abonelik adı</span><span class="sxs-lookup"><span data-stu-id="3a8f1-160">Subscription Name</span></span></td>
            <td><span data-ttu-id="3a8f1-161">Birden fazla Azure aboneliğiniz varsa, Hdınsight kümenize barındıracak hello aboneliği seçin.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-161">If you have more than one Azure Subscription, select hello subscription that will host your HDInsight cluster.</span></span> </td></tr>
    </table><span data-ttu-id="3a8f1-162">
5.Tıklatın **küme türü seçin** ve Özellikler toohello aşağıdaki kümesi hello belirtilen değerleri.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-162">
5. Click **Select Cluster Type** and set hello following properties toohello specified values.</span></span>

    <table border='1'>
        <tr><td><span data-ttu-id="3a8f1-163">Küme türü</span><span class="sxs-lookup"><span data-stu-id="3a8f1-163">Cluster type</span></span></td><td><span data-ttu-id="3a8f1-164"><strong>Hadoop</strong></span><span class="sxs-lookup"><span data-stu-id="3a8f1-164"><strong>Hadoop</strong></span></span></td></tr>
        <tr><td><span data-ttu-id="3a8f1-165">Küme katmanı</span><span class="sxs-lookup"><span data-stu-id="3a8f1-165">Cluster tier</span></span></td><td><span data-ttu-id="3a8f1-166"><strong>Standart</strong></span><span class="sxs-lookup"><span data-stu-id="3a8f1-166"><strong>Standard</strong></span></span></td></tr>
        <tr><td><span data-ttu-id="3a8f1-167">İşletim Sistemi</span><span class="sxs-lookup"><span data-stu-id="3a8f1-167">Operating System</span></span></td><td><span data-ttu-id="3a8f1-168"><strong>Windows</strong></span><span class="sxs-lookup"><span data-stu-id="3a8f1-168"><strong>Windows</strong></span></span></td></tr>
        <tr><td><span data-ttu-id="3a8f1-169">Sürüm</span><span class="sxs-lookup"><span data-stu-id="3a8f1-169">Version</span></span></td><td><span data-ttu-id="3a8f1-170">En son sürümü</span><span class="sxs-lookup"><span data-stu-id="3a8f1-170">latest version</span></span></td></tr>
    </table>

    <span data-ttu-id="3a8f1-171">Şimdi, **seçin**.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-171">Now, click **SELECT**.</span></span>

    ![Hadoop Hdınsight ilk küme ayrıntılarını sağlayın][image-customprovision-page1]
6. <span data-ttu-id="3a8f1-173">Tıklayın **kimlik bilgileri** tooset oturum açma ve Uzaktan erişim kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-173">Click on **Credentials** tooset your login and remote access credentials.</span></span> <span data-ttu-id="3a8f1-174">Seçin, **küme oturum açma kullanıcı** ve **küme oturum açma parolası**.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-174">Choose your **Cluster Login Username** and **Cluster Login Password**.</span></span>

    <span data-ttu-id="3a8f1-175">Kümenizi tooremote istiyorsanız seçin *Evet* hello dikey penceresinde hello altındaki bir kullanıcı adı ve parolasını girin.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-175">If you want tooremote into your cluster, select *yes* at hello bottom of hello blade and provide a username and password.</span></span>
7. <span data-ttu-id="3a8f1-176">Tıklayın **veri kaynağı** tooset birincil konumunuz verileri için erişim.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-176">Click on **Data Source** tooset your primary location for data access.</span></span> <span data-ttu-id="3a8f1-177">Merhaba seçin **seçim yöntemini** ve zaten varolan bir depolama hesabını belirtin veya yeni bir tane oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-177">Choose hello **Selection Method** and specify an already existing storage account or create a new one.</span></span>
8. <span data-ttu-id="3a8f1-178">Üzerinde Merhaba aynı dikey penceresinde, belirtin bir **varsayılan kapsayıcı** ve **konumu**.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-178">On hello same blade, specify a **Default Container** and a **Location**.</span></span> <span data-ttu-id="3a8f1-179">Ve tıklayın **seçin**.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-179">And, click **SELECT**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="3a8f1-180">Bir konumu Kapat tooyour Cosmos DB hesap bölge daha iyi performans için seçin</span><span class="sxs-lookup"><span data-stu-id="3a8f1-180">Select a location close tooyour Cosmos DB account region for better performance</span></span>
   >
   >
9. <span data-ttu-id="3a8f1-181">Tıklayın **fiyatlandırma** tooselect hello sayısı ve düğüm türü.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-181">Click on **Pricing** tooselect hello number and type of nodes.</span></span> <span data-ttu-id="3a8f1-182">Merhaba varsayılan yapılandırması ve ölçek hello çalışan düğüm sayısı daha sonra tutabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-182">You can keep hello default configuration and scale hello number of Worker nodes later on.</span></span>
10. <span data-ttu-id="3a8f1-183">Tıklatın **isteğe bağlı yapılandırma**, ardından **betik eylemleri** hello isteğe bağlı yapılandırma dikey olarak.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-183">Click **Optional Configuration**, then **Script Actions** in hello Optional Configuration Blade.</span></span>

     <span data-ttu-id="3a8f1-184">Betik eylemleri bilgi toocustomize aşağıdaki hello Hdınsight kümenize girin.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-184">In Script Actions, enter hello following information toocustomize your HDInsight cluster.</span></span>

     <table border='1'>
         <tr><th><span data-ttu-id="3a8f1-185">Özellik</span><span class="sxs-lookup"><span data-stu-id="3a8f1-185">Property</span></span></th><th><span data-ttu-id="3a8f1-186">Değer</span><span class="sxs-lookup"><span data-stu-id="3a8f1-186">Value</span></span></th></tr>
         <tr><td><span data-ttu-id="3a8f1-187">Ad</span><span class="sxs-lookup"><span data-stu-id="3a8f1-187">Name</span></span></td>
             <td><span data-ttu-id="3a8f1-188">Merhaba betik eylemi için bir ad belirtin.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-188">Specify a name for hello script action.</span></span></td></tr>
         <tr><td><span data-ttu-id="3a8f1-189">Betik URI'si</span><span class="sxs-lookup"><span data-stu-id="3a8f1-189">Script URI</span></span></td>
             <td><span data-ttu-id="3a8f1-190">Çağrılan toocustomize hello küme hello URI toohello komut dosyasını belirtin.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-190">Specify hello URI toohello script that is invoked toocustomize hello cluster.</span></span></br></br>
<span data-ttu-id="3a8f1-191">Lütfen girin:</span><span class="sxs-lookup"><span data-stu-id="3a8f1-191">Please enter:</span></span> </br> <span data-ttu-id="3a8f1-192"><strong>https://portalcontent.BLOB.Core.Windows.NET/scriptaction/documentdb-hadoop-installer-v04.ps1</strong>.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-192"><strong>https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</strong>.</span></span></td></tr>
         <tr><td><span data-ttu-id="3a8f1-193">Baş</span><span class="sxs-lookup"><span data-stu-id="3a8f1-193">Head</span></span></td>
             <td><span data-ttu-id="3a8f1-194">Merhaba onay kutusunu toorun hello PowerShell betiğini hello baş düğümü tıklatın.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-194">Click hello checkbox toorun hello PowerShell script onto hello Head node.</span></span></br></br><span data-ttu-id="3a8f1-195">
             <strong>Bu onay kutusunu işaretleyin</strong>.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-195">
             <strong>Check this checkbox</strong>.</span></span></td></tr>
         <tr><td><span data-ttu-id="3a8f1-196">Çalışan</span><span class="sxs-lookup"><span data-stu-id="3a8f1-196">Worker</span></span></td>
             <td><span data-ttu-id="3a8f1-197">Merhaba onay kutusunu toorun hello PowerShell betiğini hello çalışan düğümüne tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-197">Click hello checkbox toorun hello PowerShell script onto hello Worker node.</span></span></br></br><span data-ttu-id="3a8f1-198">
             <strong>Bu onay kutusunu işaretleyin</strong>.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-198">
             <strong>Check this checkbox</strong>.</span></span></td></tr>
         <tr><td><span data-ttu-id="3a8f1-199">Zookeeper</span><span class="sxs-lookup"><span data-stu-id="3a8f1-199">Zookeeper</span></span></td>
             <td><span data-ttu-id="3a8f1-200">Merhaba onay kutusunu toorun hello PowerShell betiğini hello Zookeeper'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-200">Click hello checkbox toorun hello PowerShell script onto hello Zookeeper.</span></span></br></br><span data-ttu-id="3a8f1-201">
             <strong>Gerekli</strong>.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-201">
             <strong>Not needed</strong>.</span></span>
             </td></tr>
         <tr><td><span data-ttu-id="3a8f1-202">Parametreler</span><span class="sxs-lookup"><span data-stu-id="3a8f1-202">Parameters</span></span></td>
             <td><span data-ttu-id="3a8f1-203">Merhaba komut dosyası için gereken Hello parametreleri belirtin.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-203">Specify hello parameters, if required by hello script.</span></span></br></br><span data-ttu-id="3a8f1-204">
             <strong>Gerekli parametre</strong>.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-204">
             <strong>No Parameters needed</strong>.</span></span></td></tr>
     </table><span data-ttu-id="3a8f1-205">
11.Ya da oluşturma yeni bir **kaynak grubu** veya varolan bir kaynak grubunu Azure aboneliğinizdeki kullanın.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-205">
11. Create either a new **Resource Group** or use an existing Resource Group under your Azure Subscription.</span></span>
<span data-ttu-id="3a8f1-206">12.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-206">12.</span></span> <span data-ttu-id="3a8f1-207">Şimdi, denetleme **PIN toodashboard** tootrack tıklatın ve dağıtım **oluşturma**!</span><span class="sxs-lookup"><span data-stu-id="3a8f1-207">Now, check **Pin toodashboard** tootrack its deployment and click **Create**!</span></span>

## <span data-ttu-id="3a8f1-208"><a name="InstallCmdlets"></a>Azure PowerShell'i 2. adım: Yükleme ve yapılandırma</span><span class="sxs-lookup"><span data-stu-id="3a8f1-208"><a name="InstallCmdlets"></a>Step 2: Install and configure Azure PowerShell</span></span>
1. <span data-ttu-id="3a8f1-209">Azure PowerShell'i yükleyin.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-209">Install Azure PowerShell.</span></span> <span data-ttu-id="3a8f1-210">Yönergeler için bkz [burada][powershell-install-configure].</span><span class="sxs-lookup"><span data-stu-id="3a8f1-210">Instructions can be found [here][powershell-install-configure].</span></span>

   > [!NOTE]
   > <span data-ttu-id="3a8f1-211">Alternatif olarak, Hive sorguları olduğu için Hdınsight'ın çevrimiçi Hive Düzenleyicisi'ni kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-211">Alternatively, just for Hive queries, you can use HDInsight's online Hive Editor.</span></span> <span data-ttu-id="3a8f1-212">toodo toohello bu nedenle, oturum [Azure Portal][azure-portal], tıklatın **Hdınsight** üzerinde hello sol bölmede tooview Hdınsight kümelerinizi listesi.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-212">toodo so, sign in toohello [Azure Portal][azure-portal], click **HDInsight** on hello left pane tooview a list of your HDInsight clusters.</span></span> <span data-ttu-id="3a8f1-213">Toorun Hive sorguları istiyor ve ardından hello kümesine tıklayın **sorgu konsol**.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-213">Click hello cluster you want toorun Hive queries on, and then click **Query Console**.</span></span>
   >
   >
2. <span data-ttu-id="3a8f1-214">Hello Azure PowerShell Tümleşik komut dosyası ortamı açın:</span><span class="sxs-lookup"><span data-stu-id="3a8f1-214">Open hello Azure PowerShell Integrated Scripting Environment:</span></span>

   * <span data-ttu-id="3a8f1-215">Windows 8 veya Windows Server 2012 veya sonraki sürümlerini çalıştıran bir bilgisayarda hello yerleşik kullanabilirsiniz arama.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-215">On a computer running Windows 8 or Windows Server 2012 or higher, you can use hello built-in Search.</span></span> <span data-ttu-id="3a8f1-216">Merhaba başlangıç ekranından yazın **powershell ISE** tıklatıp **Enter**.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-216">From hello Start screen, type **powershell ise** and click **Enter**.</span></span>
   * <span data-ttu-id="3a8f1-217">Windows 8 veya Windows Server 2012'den önceki bir sürümünü çalıştıran bir bilgisayarda, hello Başlat menüsünü kullanın.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-217">On a computer running a version earlier than Windows 8 or Windows Server 2012, use hello Start menu.</span></span> <span data-ttu-id="3a8f1-218">Merhaba Başlat menüsünden yazın **komut istemi** hello arama kutusunda sonra sonuçları hello listesini tıklatın **komut istemi**.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-218">From hello Start menu, type **Command Prompt** in hello search box, then in hello list of results, click **Command Prompt**.</span></span> <span data-ttu-id="3a8f1-219">Hello komut istemi, yazın **powershell_ise** tıklatıp **Enter**.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-219">In hello Command Prompt, type **powershell_ise** and click **Enter**.</span></span>
3. <span data-ttu-id="3a8f1-220">Azure hesabınızda ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-220">Add your Azure Account.</span></span>

   1. <span data-ttu-id="3a8f1-221">Hello Konsol bölmesinde, yazın **Add-AzureAccount** tıklatıp **Enter**.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-221">In hello Console Pane, type **Add-AzureAccount** and click **Enter**.</span></span>
   2. <span data-ttu-id="3a8f1-222">Azure aboneliğinizle ilişkili hello e-posta adresini yazın ve tıklatın **devam**.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-222">Type in hello email address associated with your Azure subscription and click **Continue**.</span></span>
   3. <span data-ttu-id="3a8f1-223">Azure aboneliğiniz hello parolasını yazın.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-223">Type in hello password for your Azure subscription.</span></span>
   4. <span data-ttu-id="3a8f1-224">Tıklatın **oturum**.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-224">Click **Sign in**.</span></span>
4. <span data-ttu-id="3a8f1-225">Diyagram aşağıdaki hello Azure PowerShell komut dosyası ortamınızın hello önemli bölümleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-225">hello following diagram identifies hello important parts of your Azure PowerShell Scripting Environment.</span></span>

    ![Azure PowerShell diyagramı][azure-powershell-diagram]

## <span data-ttu-id="3a8f1-227"><a name="RunHive"></a>3. adım: Cosmos DB Hdınsight ile Hive işi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="3a8f1-227"><a name="RunHive"></a>Step 3: Run a Hive job using Cosmos DB and HDInsight</span></span>
> [!IMPORTANT]
> <span data-ttu-id="3a8f1-228">Yapılandırma ayarlarınızı kullanarak < > tarafından belirtilen tüm değişkenleri doldurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-228">All variables indicated by < > must be filled in using your configuration settings.</span></span>
>
>

1. <span data-ttu-id="3a8f1-229">PowerShell betik bölmesinde değişkenleri aşağıdaki hello ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-229">Set hello following variables in your PowerShell Script pane.</span></span>

        # Provide Azure subscription name, hello Azure Storage account and container that is used for hello default HDInsight file system.
        $subscriptionName = "<SubscriptionName>"
        $storageAccountName = "<AzureStorageAccountName>"
        $containerName = "<AzureStorageContainerName>"

        # Provide hello HDInsight cluster name where you want toorun hello Hive job.
        $clusterName = "<HDInsightClusterName>"
2. <p><span data-ttu-id="3a8f1-230">Sorgu dizesi oluşturma başlayalım.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-230">Let's begin constructing your query string.</span></span> <span data-ttu-id="3a8f1-231">Biz tüm belgeleri sistem tarafından oluşturulan zaman damgaları (_ts) ve bir Azure Cosmos DB koleksiyonundan benzersiz kimlikler (_rid) alır, tüm belgeleri hello dakikaya göre hesaplar ve ardından geri yeni bir Azure Cosmos DB koleksiyona hello sonuçları depolayan bir Hive sorgusu yazacaksınız.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-231">We'll write a Hive query that takes all documents' system generated timestamps (_ts) and unique ids (_rid) from an Azure Cosmos DB collection, tallies all documents by hello minute, and then stores hello results back into a new Azure Cosmos DB collection.</span></span></p>

    <p><span data-ttu-id="3a8f1-232">İlk olarak, bir Hive tablosu bizim Azure Cosmos DB koleksiyonundan oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-232">First, let's create a Hive table from our Azure Cosmos DB collection.</span></span> <span data-ttu-id="3a8f1-233">Aşağıdaki kod parçacığını toohello PowerShell betik bölmesine hello eklemek <strong>sonra</strong> hello kod parçacığı # 1.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-233">Add hello following code snippet toohello PowerShell Script pane <strong>after</strong> hello code snippet from #1.</span></span> <span data-ttu-id="3a8f1-234">Bizim belgeleri toojust _ts ve _rid hello isteğe bağlı DocumentDB.query t parametresi kırpma eklediğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-234">Make sure you include hello optional DocumentDB.query parameter t trim our documents toojust _ts and _rid.</span></span></p>

   > [!NOTE]
   > <span data-ttu-id="3a8f1-235">**DocumentDB.inputCollections adlandırma bir hata oldu.**</span><span class="sxs-lookup"><span data-stu-id="3a8f1-235">**Naming DocumentDB.inputCollections was not a mistake.**</span></span> <span data-ttu-id="3a8f1-236">Evet, bir giriş olarak birden çok koleksiyon ekleme ver:</span><span class="sxs-lookup"><span data-stu-id="3a8f1-236">Yes, we allow adding multiple collections as an input:</span></span> </br>
   >
   >

        '*DocumentDB.inputCollections*' = '*\<DocumentDB Input Collection Name 1\>*,*\<DocumentDB Input Collection Name 2\>*' A1A</br> hello collection names are separated without spaces, using only a single comma.

        # Create a Hive table using data from DocumentDB. Pass DocumentDB hello query toofilter transferred data too_rid and _ts.
        $queryStringPart1 = "drop table DocumentDB_timestamps; "  +
                            "create external table DocumentDB_timestamps(id string, ts BIGINT) "  +
                            "stored by 'com.microsoft.azure.documentdb.hive.DocumentDBStorageHandler' "  +
                            "tblproperties ( " +
                                "'DocumentDB.endpoint' = '<DocumentDB Endpoint>', " +
                                "'DocumentDB.key' = '<DocumentDB Primary Key>', " +
                                "'DocumentDB.db' = '<DocumentDB Database Name>', " +
                                "'DocumentDB.inputCollections' = '<DocumentDB Input Collection Name>', " +
                                "'DocumentDB.query' = 'SELECT r._rid AS id, r._ts AS ts FROM root r' ); "

1. <span data-ttu-id="3a8f1-237">Ardından, bir Hive tablosu hello çıkış koleksiyon için oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-237">Next, let's create a Hive table for hello output collection.</span></span> <span data-ttu-id="3a8f1-238">Merhaba çıkış belge özellikleri hello ay, gün, saat, dakika ve hello toplam sayısı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-238">hello output document properties will be hello month, day, hour, minute, and hello total number of occurrences.</span></span>

   > [!NOTE]
   > <span data-ttu-id="3a8f1-239">**Henüz bir yeniden adlandırma DocumentDB.outputCollections bir hata oldu.**</span><span class="sxs-lookup"><span data-stu-id="3a8f1-239">**Yet again, naming DocumentDB.outputCollections was not a mistake.**</span></span> <span data-ttu-id="3a8f1-240">Evet, çıkış olarak birden çok koleksiyon ekleme ver:</span><span class="sxs-lookup"><span data-stu-id="3a8f1-240">Yes, we allow adding multiple collections as an output:</span></span> </br>
   > <span data-ttu-id="3a8f1-241">'*DocumentDB.outputCollections*'='*\<DocumentDB çıkış koleksiyon adı 1\>*,*\<DocumentDB çıkış koleksiyon adı 2\>* '</span><span class="sxs-lookup"><span data-stu-id="3a8f1-241">'*DocumentDB.outputCollections*' = '*\<DocumentDB Output Collection Name 1\>*,*\<DocumentDB Output Collection Name 2\>*'</span></span> </br> <span data-ttu-id="3a8f1-242">Merhaba koleksiyon adları, boşluk, yalnızca tek bir virgül kullanarak ayrılır.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-242">hello collection names are separated without spaces, using only a single comma.</span></span> </br></br>
   > <span data-ttu-id="3a8f1-243">Belgeler arasında birden çok koleksiyon dağıtılmış hepsini olacaktır.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-243">Documents will be distributed round-robin across multiple collections.</span></span> <span data-ttu-id="3a8f1-244">Belgeleri toplu bir koleksiyonda depolanacak sonra ikinci bir toplu iş belgelerin hello sonraki koleksiyonu ve benzeri depolanır.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-244">A batch of documents will be stored in one collection, then a second batch of documents will be stored in hello next collection, and so forth.</span></span>
   >
   >

       # Create a Hive table for hello output data tooDocumentDB.
       $queryStringPart2 = "drop table DocumentDB_analytics; " +
                             "create external table DocumentDB_analytics(Month INT, Day INT, Hour INT, Minute INT, Total INT) " +
                             "stored by 'com.microsoft.azure.documentdb.hive.DocumentDBStorageHandler' " +
                             "tblproperties ( " +
                                 "'DocumentDB.endpoint' = '<DocumentDB Endpoint>', " +
                                 "'DocumentDB.key' = '<DocumentDB Primary Key>', " +  
                                 "'DocumentDB.db' = '<DocumentDB Database Name>', " +
                                 "'DocumentDB.outputCollections' = '<DocumentDB Output Collection Name>' ); "
2. <span data-ttu-id="3a8f1-245">Son olarak, şirketinizdeki ay, gün, saat ve dakika ve INSERT hello sonuçları hello uygulamasına geri tarafından tally hello belge Hive tablosu çıktı.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-245">Finally, let's tally hello documents by month, day, hour, and minute and insert hello results back into hello output Hive table.</span></span>

        # GROUP BY minute, COUNT entries for each, INSERT INTO output Hive table.
        $queryStringPart3 = "INSERT INTO table DocumentDB_analytics " +
                              "SELECT month(from_unixtime(ts)) as Month, day(from_unixtime(ts)) as Day, " +
                              "hour(from_unixtime(ts)) as Hour, minute(from_unixtime(ts)) as Minute, " +
                              "COUNT(*) AS Total " +
                              "FROM DocumentDB_timestamps " +
                              "GROUP BY month(from_unixtime(ts)), day(from_unixtime(ts)), " +
                              "hour(from_unixtime(ts)) , minute(from_unixtime(ts)); "
3. <span data-ttu-id="3a8f1-246">Kod parçacığı toocreate bir Hive işi tanımı hello önceki sorgu aşağıdaki hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-246">Add hello following script snippet toocreate a Hive job definition from hello previous query.</span></span>

        # Create a Hive job definition.
        $queryString = $queryStringPart1 + $queryStringPart2 + $queryStringPart3
        $hiveJobDefinition = New-AzureHDInsightHiveJobDefinition -Query $queryString

    <span data-ttu-id="3a8f1-247">Aynı zamanda hello - dosya geçiş toospecify HDFS üzerinde HiveQL komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-247">You can also use hello -File switch toospecify a HiveQL script file on HDFS.</span></span>
4. <span data-ttu-id="3a8f1-248">Aşağıdaki kod parçacığında toosave hello başlangıç saati hello ekleyin ve hello Hive işi göndermek.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-248">Add hello following snippet toosave hello start time and submit hello Hive job.</span></span>

        # Save hello start time and submit hello job toohello cluster.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $hiveJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $hiveJobDefinition
5. <span data-ttu-id="3a8f1-249">Merhaba Hive işi toocomplete toowait aşağıdaki hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-249">Add hello following toowait for hello Hive job toocomplete.</span></span>

        # Wait for hello Hive job toocomplete.
        Wait-AzureHDInsightJob -Job $hiveJob -WaitTimeoutInSeconds 3600
6. <span data-ttu-id="3a8f1-250">Tooprint hello standart çıktı hello başlatın ve aşağıdaki hello ekleyin ve bitiş saatlerini.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-250">Add hello following tooprint hello standard output and hello start and end times.</span></span>

        # Print hello standard error, hello standard output of hello Hive job, and hello start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $hiveJob.JobId -StandardOutput
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
7. <span data-ttu-id="3a8f1-251">**Çalıştırma** yeni kodunuzu!</span><span class="sxs-lookup"><span data-stu-id="3a8f1-251">**Run** your new script!</span></span> <span data-ttu-id="3a8f1-252">**Tıklatın** hello yeşil düğmesi yürütün.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-252">**Click** hello green execute button.</span></span>
8. <span data-ttu-id="3a8f1-253">Merhaba sonuçlarını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-253">Check hello results.</span></span> <span data-ttu-id="3a8f1-254">Merhaba içine oturum [Azure Portal][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="3a8f1-254">Sign into hello [Azure Portal][azure-portal].</span></span>

   1. <span data-ttu-id="3a8f1-255">Tıklatın <strong>Gözat</strong> hello sol taraftaki panelindeki.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-255">Click <strong>Browse</strong> on hello left-side panel.</span></span> </br>
   2. <span data-ttu-id="3a8f1-256">Tıklatın <strong>her şeyi</strong> hello üst-panelin sağ tarafındaki hello göz atın.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-256">Click <strong>everything</strong> at hello top-right of hello browse panel.</span></span> </br>
   3. <span data-ttu-id="3a8f1-257">Bulun ve tıklatın <strong>Azure Cosmos DB hesapları</strong>.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-257">Find and click <strong>Azure Cosmos DB Accounts</strong>.</span></span> </br>
   4. <span data-ttu-id="3a8f1-258">Ardından, bulma, <strong>Azure Cosmos DB hesabı</strong>, ardından <strong>Azure Cosmos DB veritabanı</strong> ve <strong>Azure Cosmos DB koleksiyonu</strong> belirtilen hello çıkış koleksiyonu ile ilişkili Hive sorgunuzu.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-258">Next, find your <strong>Azure Cosmos DB Account</strong>, then <strong>Azure Cosmos DB Database</strong> and your <strong>Azure Cosmos DB Collection</strong> associated with hello output collection specified in your Hive query.</span></span></br>
   5. <span data-ttu-id="3a8f1-259">Son olarak, tıklatın <strong>belge Gezgini</strong> altında <strong>Geliştirici Araçları</strong>.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-259">Finally, click <strong>Document Explorer</strong> underneath <strong>Developer Tools</strong>.</span></span></br></p>

   <span data-ttu-id="3a8f1-260">Hive sorgunuzu hello sonuçları görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-260">You will see hello results of your Hive query.</span></span>

   ![Hive sorgusu sonuçları][image-hive-query-results]

## <span data-ttu-id="3a8f1-262"><a name="RunPig"></a>Adım 4: Cosmos DB Hdınsight ile Pig işi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="3a8f1-262"><a name="RunPig"></a>Step 4: Run a Pig job using Cosmos DB and HDInsight</span></span>
> [!IMPORTANT]
> <span data-ttu-id="3a8f1-263">Yapılandırma ayarlarınızı kullanarak < > tarafından belirtilen tüm değişkenleri doldurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-263">All variables indicated by < > must be filled in using your configuration settings.</span></span>
>
>

1. <span data-ttu-id="3a8f1-264">PowerShell betik bölmesinde değişkenleri aşağıdaki hello ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-264">Set hello following variables in your PowerShell Script pane.</span></span>

        # Provide Azure subscription name.
        $subscriptionName = "Azure Subscription Name"

        # Provide HDInsight cluster name where you want toorun hello Pig job.
        $clusterName = "Azure HDInsight Cluster Name"
2. <p><span data-ttu-id="3a8f1-265">Sorgu dizesi oluşturma başlayalım.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-265">Let's begin constructing your query string.</span></span> <span data-ttu-id="3a8f1-266">Biz tüm belgeleri sistem tarafından oluşturulan zaman damgaları (_ts) ve bir Azure Cosmos DB koleksiyonundan benzersiz kimlikler (_rid) alır, tüm belgeleri hello dakikaya göre hesaplar ve ardından geri yeni bir Azure Cosmos DB koleksiyona hello sonuçları depolayan bir Pig sorgu yazacaksınız.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-266">We'll write a Pig query that takes all documents' system generated timestamps (_ts) and unique ids (_rid) from an Azure Cosmos DB collection, tallies all documents by hello minute, and then stores hello results back into a new Azure Cosmos DB collection.</span></span></p>
    <p><span data-ttu-id="3a8f1-267">İlk olarak, belge Hdınsight'a Cosmos DB'den yükleme.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-267">First, load documents from Cosmos DB into HDInsight.</span></span> <span data-ttu-id="3a8f1-268">Aşağıdaki kod parçacığını toohello PowerShell betik bölmesine hello eklemek <strong>sonra</strong> hello kod parçacığı # 1.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-268">Add hello following code snippet toohello PowerShell Script pane <strong>after</strong> hello code snippet from #1.</span></span> <span data-ttu-id="3a8f1-269">Tooadd bir DocumentDB sorgu toohello isteğe bağlı DocumentDB sorgu parametresi tootrim bizim belgeleri toojust _ts ve _rid emin olun.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-269">Make sure tooadd a DocumentDB query toohello optional DocumentDB query parameter tootrim our documents toojust _ts and _rid.</span></span></p>

   > [!NOTE]
   > <span data-ttu-id="3a8f1-270">Evet, bir giriş olarak birden çok koleksiyon ekleme ver:</span><span class="sxs-lookup"><span data-stu-id="3a8f1-270">Yes, we allow adding multiple collections as an input:</span></span> </br>
   > <span data-ttu-id="3a8f1-271">'*\<DocumentDB giriş koleksiyon adı 1\>*,*\<DocumentDB giriş koleksiyon adı 2\>*'</span><span class="sxs-lookup"><span data-stu-id="3a8f1-271">'*\<DocumentDB Input Collection Name 1\>*,*\<DocumentDB Input Collection Name 2\>*'</span></span></br> <span data-ttu-id="3a8f1-272">Merhaba koleksiyon adları, boşluk, yalnızca tek bir virgül kullanarak ayrılır.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-272">hello collection names are separated without spaces, using only a single comma.</span></span> </b>
   >
   >

    <span data-ttu-id="3a8f1-273">Belgeler arasında birden çok koleksiyon dağıtılmış hepsini olacaktır.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-273">Documents will be distributed round-robin across multiple collections.</span></span> <span data-ttu-id="3a8f1-274">Belgeleri toplu bir koleksiyonda depolanacak sonra ikinci bir toplu iş belgelerin hello sonraki koleksiyonu ve benzeri depolanır.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-274">A batch of documents will be stored in one collection, then a second batch of documents will be stored in hello next collection, and so forth.</span></span>

        # Load data from Cosmos DB. Pass DocumentDB query toofilter transferred data too_rid and _ts.
        $queryStringPart1 = "DocumentDB_timestamps = LOAD '<DocumentDB Endpoint>' USING com.microsoft.azure.documentdb.pig.DocumentDBLoader( " +
                                                        "'<DocumentDB Primary Key>', " +
                                                        "'<DocumentDB Database Name>', " +
                                                        "'<DocumentDB Input Collection Name>', " +
                                                        "'SELECT r._rid AS id, r._ts AS ts FROM root r' ); "
3. <span data-ttu-id="3a8f1-275">Ardından, şimdi hello belgeleri hello ay, gün, saat, dakika ve hello toplam sayısı tarafından tally.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-275">Next, let's tally hello documents by hello month, day, hour, minute, and hello total number of occurrences.</span></span>

       # GROUP BY minute and COUNT entries for each.
       $queryStringPart2 = "timestamp_record = FOREACH DocumentDB_timestamps GENERATE `$0#'id' as id:int, ToDate((long)(`$0#'ts') * 1000) as timestamp:datetime; " +
                           "by_minute = GROUP timestamp_record BY (GetYear(timestamp), GetMonth(timestamp), GetDay(timestamp), GetHour(timestamp), GetMinute(timestamp)); " +
                           "by_minute_count = FOREACH by_minute GENERATE FLATTEN(group) as (Year:int, Month:int, Day:int, Hour:int, Minute:int), COUNT(timestamp_record) as Total:int; "
4. <span data-ttu-id="3a8f1-276">Son olarak, şirketinizdeki hello sonuçları bizim yeni çıkış koleksiyona depolar.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-276">Finally, let's store hello results into our new output collection.</span></span>

   > [!NOTE]
   > <span data-ttu-id="3a8f1-277">Evet, çıkış olarak birden çok koleksiyon ekleme ver:</span><span class="sxs-lookup"><span data-stu-id="3a8f1-277">Yes, we allow adding multiple collections as an output:</span></span> </br>
   > <span data-ttu-id="3a8f1-278">'\<DocumentDB çıkış koleksiyon adı 1\>,\<DocumentDB çıkış koleksiyon adı 2\>'</span><span class="sxs-lookup"><span data-stu-id="3a8f1-278">'\<DocumentDB Output Collection Name 1\>,\<DocumentDB Output Collection Name 2\>'</span></span></br> <span data-ttu-id="3a8f1-279">Merhaba koleksiyon adları, boşluk, yalnızca tek bir virgül kullanarak ayrılır.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-279">hello collection names are separated without spaces, using only a single comma.</span></span></br>
   > <span data-ttu-id="3a8f1-280">Belgeleri dağıtılmış hepsini birden çok koleksiyon hello arasında olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-280">Documents will be distributed round-robin across hello multiple collections.</span></span> <span data-ttu-id="3a8f1-281">Belgeleri toplu bir koleksiyonda depolanacak sonra ikinci bir toplu iş belgelerin hello sonraki koleksiyonu ve benzeri depolanır.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-281">A batch of documents will be stored in one collection, then a second batch of documents will be stored in hello next collection, and so forth.</span></span>
   >
   >

        # Store output data tooCosmos DB.
        $queryStringPart3 = "STORE by_minute_count INTO '<DocumentDB Endpoint>' " +
                            "USING com.microsoft.azure.documentdb.pig.DocumentDBStorage( " +
                                "'<DocumentDB Primary Key>', " +
                                "'<DocumentDB Database Name>', " +
                                "'<DocumentDB Output Collection Name>'); "
5. <span data-ttu-id="3a8f1-282">Kod parçacığı toocreate Pig iş tanımı hello önceki sorgu aşağıdaki hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-282">Add hello following script snippet toocreate a Pig job definition from hello previous query.</span></span>

        # Create a Pig job definition.
        $queryString = $queryStringPart1 + $queryStringPart2 + $queryStringPart3
        $pigJobDefinition = New-AzureHDInsightPigJobDefinition -Query $queryString -StatusFolder $statusFolder

    <span data-ttu-id="3a8f1-283">Aynı zamanda hello - dosya geçiş toospecify HDFS üzerinde Pig betiği.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-283">You can also use hello -File switch toospecify a Pig script file on HDFS.</span></span>
6. <span data-ttu-id="3a8f1-284">Aşağıdaki kod parçacığında toosave hello başlangıç saati hello ekleyin ve hello Pig işi göndermek.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-284">Add hello following snippet toosave hello start time and submit hello Pig job.</span></span>

        # Save hello start time and submit hello job toohello cluster.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $pigJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $pigJobDefinition
7. <span data-ttu-id="3a8f1-285">Merhaba Pig işi toocomplete toowait aşağıdaki hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-285">Add hello following toowait for hello Pig job toocomplete.</span></span>

        # Wait for hello Pig job toocomplete.
        Wait-AzureHDInsightJob -Job $pigJob -WaitTimeoutInSeconds 3600
8. <span data-ttu-id="3a8f1-286">Tooprint hello standart çıktı hello başlatın ve aşağıdaki hello ekleyin ve bitiş saatlerini.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-286">Add hello following tooprint hello standard output and hello start and end times.</span></span>

        # Print hello standard error, hello standard output of hello Hive job, and hello start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $pigJob.JobId -StandardOutput
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
9. <span data-ttu-id="3a8f1-287">**Çalıştırma** yeni kodunuzu!</span><span class="sxs-lookup"><span data-stu-id="3a8f1-287">**Run** your new script!</span></span> <span data-ttu-id="3a8f1-288">**Tıklatın** hello yeşil düğmesi yürütün.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-288">**Click** hello green execute button.</span></span>
10. <span data-ttu-id="3a8f1-289">Merhaba sonuçlarını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-289">Check hello results.</span></span> <span data-ttu-id="3a8f1-290">Merhaba içine oturum [Azure Portal][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="3a8f1-290">Sign into hello [Azure Portal][azure-portal].</span></span>

    1. <span data-ttu-id="3a8f1-291">Tıklatın <strong>Gözat</strong> hello sol taraftaki panelindeki.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-291">Click <strong>Browse</strong> on hello left-side panel.</span></span> </br>
    2. <span data-ttu-id="3a8f1-292">Tıklatın <strong>her şeyi</strong> hello üst-panelin sağ tarafındaki hello göz atın.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-292">Click <strong>everything</strong> at hello top-right of hello browse panel.</span></span> </br>
    3. <span data-ttu-id="3a8f1-293">Bulun ve tıklatın <strong>Azure Cosmos DB hesapları</strong>.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-293">Find and click <strong>Azure Cosmos DB Accounts</strong>.</span></span> </br>
    4. <span data-ttu-id="3a8f1-294">Ardından, bulma, <strong>Azure Cosmos DB hesabı</strong>, ardından <strong>Azure Cosmos DB veritabanı</strong> ve <strong>Azure Cosmos DB koleksiyonu</strong> belirtilen hello çıkış koleksiyonu ile ilişkili Pig sorgunuzu.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-294">Next, find your <strong>Azure Cosmos DB Account</strong>, then <strong>Azure Cosmos DB Database</strong> and your <strong>Azure Cosmos DB Collection</strong> associated with hello output collection specified in your Pig query.</span></span></br>
    5. <span data-ttu-id="3a8f1-295">Son olarak, tıklatın <strong>belge Gezgini</strong> altında <strong>Geliştirici Araçları</strong>.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-295">Finally, click <strong>Document Explorer</strong> underneath <strong>Developer Tools</strong>.</span></span></br></p>

    <span data-ttu-id="3a8f1-296">Pig sorgunuzu hello sonuçları görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-296">You will see hello results of your Pig query.</span></span>

    ![Pig sorgu sonuçları][image-pig-query-results]

## <span data-ttu-id="3a8f1-298"><a name="RunMapReduce"></a>5. adım: Azure Cosmos DB Hdınsight ile MapReduce işi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="3a8f1-298"><a name="RunMapReduce"></a>Step 5: Run a MapReduce job using Azure Cosmos DB and HDInsight</span></span>
1. <span data-ttu-id="3a8f1-299">PowerShell betik bölmesinde değişkenleri aşağıdaki hello ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-299">Set hello following variables in your PowerShell Script pane.</span></span>

        $subscriptionName = "<SubscriptionName>"   # Azure subscription name
        $clusterName = "<ClusterName>"             # HDInsight cluster name
2. <span data-ttu-id="3a8f1-300">Biz hello Azure Cosmos DB koleksiyondaki her bir belge özellik için yineleme sayısı hesaplayan bir MapReduce işi yürüteceksiniz.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-300">We'll execute a MapReduce job that tallies hello number of occurrences for each Document property from your Azure Cosmos DB collection.</span></span> <span data-ttu-id="3a8f1-301">Bu kod parçacığını ekleyin **sonra** yukarıdaki hello parçacığında.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-301">Add this script snippet **after** hello snippet above.</span></span>

        # Define hello MapReduce job.
        $TallyPropertiesJobDefinition = New-AzureHDInsightMapReduceJobDefinition -JarFile "wasb:///example/jars/TallyProperties-v01.jar" -ClassName "TallyProperties" -Arguments "<DocumentDB Endpoint>","<DocumentDB Primary Key>", "<DocumentDB Database Name>","<DocumentDB Input Collection Name>","<DocumentDB Output Collection Name>","<[Optional] DocumentDB Query>"

   > [!NOTE]
   > <span data-ttu-id="3a8f1-302">TallyProperties v01.jar hello özel yüklemesi hello Cosmos DB Hadoop bağlayıcı ile gelir.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-302">TallyProperties-v01.jar comes with hello custom installation of hello Cosmos DB Hadoop Connector.</span></span>
   >
   >
3. <span data-ttu-id="3a8f1-303">Komut toosubmit hello MapReduce işi aşağıdaki hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-303">Add hello following command toosubmit hello MapReduce job.</span></span>

        # Save hello start time and submit hello job.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $TallyPropertiesJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $TallyPropertiesJobDefinition | Wait-AzureHDInsightJob -WaitTimeoutInSeconds 3600  

    <span data-ttu-id="3a8f1-304">Ayrıca toohello MapReduce iş tanımı, size ayrıca toorun hello MapReduce işi ve hello kimlik bilgilerini istediğiniz yere hello Hdınsight küme adını belirtin.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-304">In addition toohello MapReduce job definition, you also provide hello HDInsight cluster name where you want toorun hello MapReduce job, and hello credentials.</span></span> <span data-ttu-id="3a8f1-305">Merhaba başlangıç AzureHDInsightJob zaman bir çağrıdır.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-305">hello Start-AzureHDInsightJob is an asynchronized call.</span></span> <span data-ttu-id="3a8f1-306">Merhaba işin kullanım hello toocheck hello tamamlama *bekleme AzureHDInsightJob* cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-306">toocheck hello completion of hello job, use hello *Wait-AzureHDInsightJob* cmdlet.</span></span>
4. <span data-ttu-id="3a8f1-307">Komut toocheck aşağıdaki hello hatalarını çalışan hello MapReduce işi ile ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-307">Add hello following command toocheck any errors with running hello MapReduce job.</span></span>

        # Get hello job output and print hello start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $TallyPropertiesJob.JobId -StandardError
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
5. <span data-ttu-id="3a8f1-308">**Çalıştırma** yeni kodunuzu!</span><span class="sxs-lookup"><span data-stu-id="3a8f1-308">**Run** your new script!</span></span> <span data-ttu-id="3a8f1-309">**Tıklatın** hello yeşil düğmesi yürütün.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-309">**Click** hello green execute button.</span></span>
6. <span data-ttu-id="3a8f1-310">Merhaba sonuçlarını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-310">Check hello results.</span></span> <span data-ttu-id="3a8f1-311">Merhaba içine oturum [Azure Portal][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="3a8f1-311">Sign into hello [Azure Portal][azure-portal].</span></span>

   1. <span data-ttu-id="3a8f1-312">Tıklatın <strong>Gözat</strong> hello sol taraftaki panelindeki.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-312">Click <strong>Browse</strong> on hello left-side panel.</span></span>
   2. <span data-ttu-id="3a8f1-313">Tıklatın <strong>her şeyi</strong> hello üst-panelin sağ tarafındaki hello göz atın.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-313">Click <strong>everything</strong> at hello top-right of hello browse panel.</span></span>
   3. <span data-ttu-id="3a8f1-314">Bulun ve tıklatın <strong>Azure Cosmos DB hesapları</strong>.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-314">Find and click <strong>Azure Cosmos DB Accounts</strong>.</span></span>
   4. <span data-ttu-id="3a8f1-315">Ardından, bulma, <strong>Azure Cosmos DB hesabı</strong>, ardından <strong>Azure Cosmos DB veritabanı</strong> ve <strong>Azure Cosmos DB koleksiyonu</strong> belirtilen hello çıkış koleksiyonu ile ilişkili MapReduce işi.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-315">Next, find your <strong>Azure Cosmos DB Account</strong>, then <strong>Azure Cosmos DB Database</strong> and your <strong>Azure Cosmos DB Collection</strong> associated with hello output collection specified in your MapReduce job.</span></span>
   5. <span data-ttu-id="3a8f1-316">Son olarak, tıklatın <strong>belge Gezgini</strong> altında <strong>Geliştirici Araçları</strong>.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-316">Finally, click <strong>Document Explorer</strong> underneath <strong>Developer Tools</strong>.</span></span>

      <span data-ttu-id="3a8f1-317">MapReduce işi hello sonuçları görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-317">You will see hello results of your MapReduce job.</span></span>

      ![MapReduce sorgu sonuçları][image-mapreduce-query-results]

## <span data-ttu-id="3a8f1-319"><a name="NextSteps"></a>Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="3a8f1-319"><a name="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="3a8f1-320">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="3a8f1-320">Congratulations!</span></span> <span data-ttu-id="3a8f1-321">Yalnızca Azure Cosmos DB ve Hdınsight kullanarak, ilk Hive, Pig ve MapReduce işleri çalıştırdığınız.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-321">You just ran your first Hive, Pig, and MapReduce jobs using Azure Cosmos DB and HDInsight.</span></span>

<span data-ttu-id="3a8f1-322">Bizim açık kaynaklıdır bizim Hadoop bağlayıcı.</span><span class="sxs-lookup"><span data-stu-id="3a8f1-322">We have open sourced our Hadoop Connector.</span></span> <span data-ttu-id="3a8f1-323">İlginizi çekiyorsa üzerinde katkıda bulunabilirsiniz [GitHub][github].</span><span class="sxs-lookup"><span data-stu-id="3a8f1-323">If you're interested, you can contribute on [GitHub][github].</span></span>

<span data-ttu-id="3a8f1-324">toolearn daha makaleler hello bakın:</span><span class="sxs-lookup"><span data-stu-id="3a8f1-324">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="3a8f1-325">[Documentdb ile bir Java uygulaması geliştirme][documentdb-java-application]</span><span class="sxs-lookup"><span data-stu-id="3a8f1-325">[Develop a Java application with Documentdb][documentdb-java-application]</span></span>
* <span data-ttu-id="3a8f1-326">[Hdınsight'ta Hadoop için Java MapReduce programlar geliştirmek][hdinsight-develop-deploy-java-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="3a8f1-326">[Develop Java MapReduce programs for Hadoop in HDInsight][hdinsight-develop-deploy-java-mapreduce]</span></span>
* <span data-ttu-id="3a8f1-327">[Hadoop ile Hive Hdınsight tooanalyze mobil ahize kullanımda kullanmaya başlama][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="3a8f1-327">[Get started using Hadoop with Hive in HDInsight tooanalyze mobile handset use][hdinsight-get-started]</span></span>
* <span data-ttu-id="3a8f1-328">[Hdınsight ile MapReduce kullanma][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="3a8f1-328">[Use MapReduce with HDInsight][hdinsight-use-mapreduce]</span></span>
* <span data-ttu-id="3a8f1-329">[HDInsight ile Hive kullanma][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="3a8f1-329">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="3a8f1-330">[HDInsight ile Pig kullanma][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="3a8f1-330">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="3a8f1-331">[Betik eylemi kullanarak Hdınsight kümelerini özelleştirme][hdinsight-hadoop-customize-cluster]</span><span class="sxs-lookup"><span data-stu-id="3a8f1-331">[Customize HDInsight clusters using Script Action][hdinsight-hadoop-customize-cluster]</span></span>

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
