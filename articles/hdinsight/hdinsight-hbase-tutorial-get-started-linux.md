---
title: "hdınsight'ta - Azure HBase örnek aaaGet Başlarken | Microsoft Docs"
description: "Hdınsight'ta hadoop kullanarak bu Apache HBase örnek toostart izleyin. Hello HBase Kabuğu ' tablolar oluşturmak ve bunları sorgulayabilirsiniz Hive kullanma."
keywords: "hbase komutu,hbase örneği"
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 4d6a2658-6b19-4268-95ee-822890f5a33a
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: jgao
ms.openlocfilehash: 43419780142b320b16180a2b1f25020dee2f7a11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-an-apache-hbase-example-in-hdinsight"></a><span data-ttu-id="931ce-105">HDInsight'ta Apache HBase örneğiyle çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="931ce-105">Get started with an Apache HBase example in HDInsight</span></span>

<span data-ttu-id="931ce-106">Toocreate bir HBase kümesi, hdınsight'ta HBase tabloları oluşturma ve tabloları Hive kullanarak sorgulama öğrenin.</span><span class="sxs-lookup"><span data-stu-id="931ce-106">Learn how toocreate an HBase cluster in HDInsight, create HBase tables, and query tables by using Hive.</span></span> <span data-ttu-id="931ce-107">Genel HBase bilgileri için bkz. [HDInsight HBase’e genel bakış][hdinsight-hbase-overview].</span><span class="sxs-lookup"><span data-stu-id="931ce-107">For general HBase information, see [HDInsight HBase overview][hdinsight-hbase-overview].</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="prerequisites"></a><span data-ttu-id="931ce-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="931ce-108">Prerequisites</span></span>
<span data-ttu-id="931ce-109">Bu HBase örnek çalışırken başlamadan önce aşağıdaki öğelerindeki hello sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="931ce-109">Before you begin trying this HBase example, you must have hello following items:</span></span>

* <span data-ttu-id="931ce-110">**Bir Azure aboneliği**.</span><span class="sxs-lookup"><span data-stu-id="931ce-110">**An Azure subscription**.</span></span> <span data-ttu-id="931ce-111">Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="931ce-111">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="931ce-112">[Secure Shell(SSH)](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="931ce-112">[Secure Shell(SSH)](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span> 
* <span data-ttu-id="931ce-113">[curl](http://curl.haxx.se/download.html).</span><span class="sxs-lookup"><span data-stu-id="931ce-113">[curl](http://curl.haxx.se/download.html).</span></span>

## <a name="create-hbase-cluster"></a><span data-ttu-id="931ce-114">HBase kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="931ce-114">Create HBase cluster</span></span>
<span data-ttu-id="931ce-115">Merhaba aşağıdaki yordam bir Azure Resource Manager şablonu toocreate sürüm 3.4 Linux tabanlı HBase kümesi ve hello bağımlı varsayılan bir Azure depolama hesabı kullanır.</span><span class="sxs-lookup"><span data-stu-id="931ce-115">hello following procedure uses an Azure Resource Manager template toocreate a version 3.4 Linux-based HBase cluster and hello dependent default Azure Storage account.</span></span> <span data-ttu-id="931ce-116">Merhaba yordam ve diğer küme oluşturma yöntemlerinde kullanılan toounderstand hello parametreler bkz [Hdınsight oluşturma Linux tabanlı Hadoop kümeleri](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="931ce-116">toounderstand hello parameters used in hello procedure and other cluster creation methods, see [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

1. <span data-ttu-id="931ce-117">Görüntü tooopen hello hello Azure portal şablonda aşağıdaki hello'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="931ce-117">Click hello following image tooopen hello template in hello Azure portal.</span></span> <span data-ttu-id="931ce-118">Merhaba şablonu bir ortak blob kapsayıcısında bulunur.</span><span class="sxs-lookup"><span data-stu-id="931ce-118">hello template is located in a public blob container.</span></span> 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-linux%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-tutorial-get-started-linux/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. <span data-ttu-id="931ce-119">Merhaba gelen **özel dağıtım** dikey penceresinde hello aşağıdaki değerleri girin:</span><span class="sxs-lookup"><span data-stu-id="931ce-119">From hello **Custom deployment** blade, enter hello following values:</span></span>
   
   * <span data-ttu-id="931ce-120">**Abonelik**: kullanılan toocreate hello küme Azure aboneliğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="931ce-120">**Subscription**: Select your Azure subscription that is used toocreate hello cluster.</span></span>
   * <span data-ttu-id="931ce-121">**Kaynak grubu**: Bir Azure Resource Management grubu oluşturun veya var olan gruplardan birini kullanın.</span><span class="sxs-lookup"><span data-stu-id="931ce-121">**Resource group**: Create an Azure Resource Management group or use an existing one.</span></span>
   * <span data-ttu-id="931ce-122">**Konum**: hello hello kaynak grubu konumunu belirtin.</span><span class="sxs-lookup"><span data-stu-id="931ce-122">**Location**: Specify hello location of hello resource group.</span></span> 
   * <span data-ttu-id="931ce-123">**ClusterName**: Merhaba HBase kümesi için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="931ce-123">**ClusterName**: Enter a name for hello HBase cluster.</span></span>
   * <span data-ttu-id="931ce-124">**Küme oturum açma adı ve parola**: hello varsayılan oturum açma adı **yönetici**.</span><span class="sxs-lookup"><span data-stu-id="931ce-124">**Cluster login name and password**: hello default login name is **admin**.</span></span>
   * <span data-ttu-id="931ce-125">**SSH kullanıcı adı ve parola**: hello varsayılan kullanıcı adı **sshuser**.</span><span class="sxs-lookup"><span data-stu-id="931ce-125">**SSH username and password**: hello default username is **sshuser**.</span></span>  <span data-ttu-id="931ce-126">Bunu yeniden adlandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="931ce-126">You can rename it.</span></span>
     
     <span data-ttu-id="931ce-127">Diğer parametreler isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="931ce-127">Other parameters are optional.</span></span>  
     
     <span data-ttu-id="931ce-128">Her kümenin bir Azure Depolama hesabı bağımlılığı vardır.</span><span class="sxs-lookup"><span data-stu-id="931ce-128">Each cluster has an Azure Storage account dependency.</span></span> <span data-ttu-id="931ce-129">Bir küme silindikten sonra hello veri hello depolama hesabında saklanır.</span><span class="sxs-lookup"><span data-stu-id="931ce-129">After you delete a cluster, hello data retains in hello storage account.</span></span> <span data-ttu-id="931ce-130">Merhaba kümenin varsayılan depolama hesabı adı hello küme depo"ifadesi eklenmiş" adıdır.</span><span class="sxs-lookup"><span data-stu-id="931ce-130">hello cluster default storage account name is hello cluster name with "store" appended.</span></span> <span data-ttu-id="931ce-131">Bu, sabit kodlanmış hello şablon değişkenler bölümünde olur.</span><span class="sxs-lookup"><span data-stu-id="931ce-131">It is hardcoded in hello template variables section.</span></span>
3. <span data-ttu-id="931ce-132">Seçin **toohello hüküm ve koşullar yukarıda belirtildiği kabul**ve ardından **satın alma**.</span><span class="sxs-lookup"><span data-stu-id="931ce-132">Select **I agree toohello terms and conditions stated above**, and then click **Purchase**.</span></span> <span data-ttu-id="931ce-133">Bir küme toocreate yaklaşık 20 dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="931ce-133">It takes about 20 minutes toocreate a cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="931ce-134">Bir HBase kümesi silindikten sonra hello kullanarak başka bir HBase kümesi oluşturabilirsiniz aynı varsayılan blob kapsayıcısı.</span><span class="sxs-lookup"><span data-stu-id="931ce-134">After an HBase cluster is deleted, you can create another HBase cluster by using hello same default blob container.</span></span> <span data-ttu-id="931ce-135">Merhaba yeni küme hello özgün kümede oluşturduğunuz hello HBase tablolarını seçer.</span><span class="sxs-lookup"><span data-stu-id="931ce-135">hello new cluster picks up hello HBase tables you created in hello original cluster.</span></span> <span data-ttu-id="931ce-136">tooavoid tutarsızlıklar hello küme silmeden önce hello HBase tablolarını devre dışı bırakmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="931ce-136">tooavoid inconsistencies, we recommend that you disable hello HBase tables before you delete hello cluster.</span></span>
> 
> 

## <a name="create-tables-and-insert-data"></a><span data-ttu-id="931ce-137">Tablo oluşturma ve veri ekleme</span><span class="sxs-lookup"><span data-stu-id="931ce-137">Create tables and insert data</span></span>
<span data-ttu-id="931ce-138">SSH tooconnect tooHBase kümeleri kullanan ve HBase Kabuğu toocreate HBase tablolarını kullanın, veri ve sorgu veri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="931ce-138">You can use SSH tooconnect tooHBase clusters and then use HBase Shell toocreate HBase tables, insert data, and query data.</span></span> <span data-ttu-id="931ce-139">Daha fazla bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="931ce-139">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="931ce-140">Çoğu kişi için veriler hello tablo biçiminde görünür:</span><span class="sxs-lookup"><span data-stu-id="931ce-140">For most people, data appears in hello tabular format:</span></span>

![HDInsight HBase tablo verileri][img-hbase-sample-data-tabular]

<span data-ttu-id="931ce-142">HBase (BigTable uygulaması), hello aynı veri gibi görünüyor:</span><span class="sxs-lookup"><span data-stu-id="931ce-142">In HBase (an implementation of BigTable), hello same data looks like:</span></span>

![HDInsight HBase BigTable verileri][img-hbase-sample-data-bigtable]


<span data-ttu-id="931ce-144">**toouse hello HBase Kabuğu**</span><span class="sxs-lookup"><span data-stu-id="931ce-144">**toouse hello HBase shell**</span></span>

1. <span data-ttu-id="931ce-145">SSH, HBase komutu aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="931ce-145">From SSH, run hello following HBase command:</span></span>
   
    ```bash
    hbase shell
    ```

2. <span data-ttu-id="931ce-146">İki sütun ailesi ile bir HBase oluşturun:</span><span class="sxs-lookup"><span data-stu-id="931ce-146">Create an HBase with two-column families:</span></span>

    ```hbaseshell   
    create 'Contacts', 'Personal', 'Office'
    list
    ```
3. <span data-ttu-id="931ce-147">Bazı verileri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="931ce-147">Insert some data:</span></span>
    
    ```hbaseshell   
    put 'Contacts', '1000', 'Personal:Name', 'John Dole'
    put 'Contacts', '1000', 'Personal:Phone', '1-425-000-0001'
    put 'Contacts', '1000', 'Office:Phone', '1-425-000-0002'
    put 'Contacts', '1000', 'Office:Address', '1111 San Gabriel Dr.'
    scan 'Contacts'
    ```
   
    ![HDInsight Hadoop HBase kabuğu][img-hbase-shell]
4. <span data-ttu-id="931ce-149">Tek bir satır alın</span><span class="sxs-lookup"><span data-stu-id="931ce-149">Get a single row</span></span>
   
    ```hbaseshell
    get 'Contacts', '1000'
    ```
   
    <span data-ttu-id="931ce-150">Yalnızca bir satır olduğundan hello tarama komutunu kullanmanızla aynı sonuçları hello göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="931ce-150">You shall see hello same results as using hello scan command because there is only one row.</span></span>
   
    <span data-ttu-id="931ce-151">Merhaba HBase tablo şeması hakkında daha fazla bilgi için bkz: [şema tasarımına giriş tooHBase][hbase-schema].</span><span class="sxs-lookup"><span data-stu-id="931ce-151">For more information about hello HBase table schema, see [Introduction tooHBase Schema Design][hbase-schema].</span></span> <span data-ttu-id="931ce-152">HBase komutları hakkında daha fazla bilgi için bkz. [Apache HBase başvuru kılavuzu][hbase-quick-start].</span><span class="sxs-lookup"><span data-stu-id="931ce-152">For more HBase commands, see [Apache HBase reference guide][hbase-quick-start].</span></span>
5. <span data-ttu-id="931ce-153">Merhaba kabuktan çıkış yapma</span><span class="sxs-lookup"><span data-stu-id="931ce-153">Exit hello shell</span></span>
   
    ```hbaseshell
    exit
    ```

<span data-ttu-id="931ce-154">**toobulk hello kişiler HBase tablosuna veri yükleme**</span><span class="sxs-lookup"><span data-stu-id="931ce-154">**toobulk load data into hello contacts HBase table**</span></span>

<span data-ttu-id="931ce-155">HBase’de verileri tablolara yüklemek için bazı yöntemler vardır.</span><span class="sxs-lookup"><span data-stu-id="931ce-155">HBase includes several methods of loading data into tables.</span></span>  <span data-ttu-id="931ce-156">Daha fazla bilgi için bkz. [Toplu yükleme](http://hbase.apache.org/book.html#arch.bulk.load).</span><span class="sxs-lookup"><span data-stu-id="931ce-156">For more information, see [Bulk loading](http://hbase.apache.org/book.html#arch.bulk.load).</span></span>

<span data-ttu-id="931ce-157">Örnek veri dosyası, ortak blob kapsayıcısı *wasb://hbasecontacts@hditutorialdata.blob.core.windows.net/contacts.txt* içinde bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="931ce-157">A sample data file can be found in a public blob container, *wasb://hbasecontacts@hditutorialdata.blob.core.windows.net/contacts.txt*.</span></span>  <span data-ttu-id="931ce-158">Merhaba veri dosyası Merhaba içeriğine şöyledir:</span><span class="sxs-lookup"><span data-stu-id="931ce-158">hello content of hello data file is:</span></span>

    8396    Calvin Raji      230-555-0191    230-555-0191    5415 San Gabriel Dr.
    16600   Karen Wu         646-555-0113    230-555-0192    9265 La Paz
    4324    Karl Xie         508-555-0163    230-555-0193    4912 La Vuelta
    16891   Jonn Jackson     674-555-0110    230-555-0194    40 Ellis St.
    3273    Miguel Miller    397-555-0155    230-555-0195    6696 Anchor Drive
    3588    Osa Agbonile     592-555-0152    230-555-0196    1873 Lion Circle
    10272   Julia Lee        870-555-0110    230-555-0197    3148 Rose Street
    4868    Jose Hayes       599-555-0171    230-555-0198    793 Crawford Street
    4761    Caleb Alexander  670-555-0141    230-555-0199    4775 Kentucky Dr.
    16443   Terry Chander    998-555-0171    230-555-0200    771 Northridge Drive

<span data-ttu-id="931ce-159">İsteğe bağlı olarak, bir metin dosyası oluşturun ve hello dosya tooyour kendi depolama hesabı yükleyin.</span><span class="sxs-lookup"><span data-stu-id="931ce-159">You can optionally create a text file and upload hello file tooyour own storage account.</span></span> <span data-ttu-id="931ce-160">Merhaba yönergeler için bkz: [hdınsight'ta Hadoop işleri için verileri karşıya yükleme][hdinsight-upload-data].</span><span class="sxs-lookup"><span data-stu-id="931ce-160">For hello instructions, see [Upload data for Hadoop jobs in HDInsight][hdinsight-upload-data].</span></span>

> [!NOTE]
> <span data-ttu-id="931ce-161">Bu yordam hello son yordamda oluşturduğunuz hello kişiler HBase tablosunu kullanır.</span><span class="sxs-lookup"><span data-stu-id="931ce-161">This procedure uses hello Contacts HBase table you have created in hello last procedure.</span></span>
> 

1. <span data-ttu-id="931ce-162">SSH, verileri tooStoreFiles dosya ve Dimporttsv.bulk.output tarafından belirtilen göreli bir yola depolamak komutu tootransform hello aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="931ce-162">From SSH, run hello following command tootransform hello data file tooStoreFiles and store at a relative path specified by Dimporttsv.bulk.output.</span></span>  <span data-ttu-id="931ce-163">HBase Kabuğu'nda varsa, hello çıkış komut tooexit kullanın.</span><span class="sxs-lookup"><span data-stu-id="931ce-163">If you are in HBase Shell, use hello exit command tooexit.</span></span>

    ```bash   
    hbase org.apache.hadoop.hbase.mapreduce.ImportTsv -Dimporttsv.columns="HBASE_ROW_KEY,Personal:Name,Personal:Phone,Office:Phone,Office:Address" -Dimporttsv.bulk.output="/example/data/storeDataFileOutput" Contacts wasb://hbasecontacts@hditutorialdata.blob.core.windows.net/contacts.txt
    ```

2. <span data-ttu-id="931ce-164">Komut tooupload hello veri /example/data/storeDataFileOutput toohello HBase tablosundan aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="931ce-164">Run hello following command tooupload hello data from  /example/data/storeDataFileOutput toohello HBase table:</span></span>
   
    ```bash
    hbase org.apache.hadoop.hbase.mapreduce.LoadIncrementalHFiles /example/data/storeDataFileOutput Contacts
    ```

3. <span data-ttu-id="931ce-165">Merhaba HBase Kabuğu'nu açın ve hello tarama komutunu toolist hello tablo içeriğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="931ce-165">You can open hello HBase shell, and use hello scan command toolist hello table content.</span></span>

## <a name="use-hive-tooquery-hbase"></a><span data-ttu-id="931ce-166">Hive tooquery HBase kullanın</span><span class="sxs-lookup"><span data-stu-id="931ce-166">Use Hive tooquery HBase</span></span>

<span data-ttu-id="931ce-167">Hive kullanarak HBase tablolarındaki verileri sorgulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="931ce-167">You can query data in HBase tables by using Hive.</span></span> <span data-ttu-id="931ce-168">Bu bölümde, bir Hive tablosu, oluşturduğunuz toohello HBase tablo eşler ve HBase tablosunda tooquery hello verileri kullanır.</span><span class="sxs-lookup"><span data-stu-id="931ce-168">In this section, you create a Hive table that maps toohello HBase table and uses it tooquery hello data in your HBase table.</span></span>

1. <span data-ttu-id="931ce-169">Açık **PuTTY**ve toohello kümesine bağlanın.</span><span class="sxs-lookup"><span data-stu-id="931ce-169">Open **PuTTY**, and connect toohello cluster.</span></span>  <span data-ttu-id="931ce-170">Merhaba önceki yordamda bulunan Hello yönergelere bakın.</span><span class="sxs-lookup"><span data-stu-id="931ce-170">See hello instructions in hello previous procedure.</span></span>
2. <span data-ttu-id="931ce-171">Merhaba SSH oturumunda, aşağıdaki komut toostart Beeline hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="931ce-171">From hello SSH session, use hello following command toostart Beeline:</span></span>

    ```bash
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -n admin
    ```

    <span data-ttu-id="931ce-172">Beeline hakkında daha fazla bilgi için bkz. [Beeline ile HDInsight’ta Hadoop ile Hive kullanma](hdinsight-hadoop-use-hive-beeline.md).</span><span class="sxs-lookup"><span data-stu-id="931ce-172">For more information about Beeline, see [Use Hive with Hadoop in HDInsight with Beeline](hdinsight-hadoop-use-hive-beeline.md).</span></span>
       
3. <span data-ttu-id="931ce-173">Aşağıdaki HiveQL betiğini toocreate hello toohello HBase tablosuyla eşlenen bir Hive tablosu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="931ce-173">Run hello following HiveQL script  toocreate a Hive table that maps toohello HBase table.</span></span> <span data-ttu-id="931ce-174">Bu öğreticide daha önce bu deyimi çalıştırmadan önce hello HBase Kabuğu'nu kullanarak tarafından başvurulan hello örnek tablosunu oluşturduğunuzdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="931ce-174">Make sure that you have created hello sample table referenced earlier in this tutorial by using hello HBase shell before you run this statement.</span></span>

    ```hiveql   
    CREATE EXTERNAL TABLE hbasecontacts(rowkey STRING, name STRING, homephone STRING, officephone STRING, officeaddress STRING)
    STORED BY 'org.apache.hadoop.hive.hbase.HBaseStorageHandler'
    WITH SERDEPROPERTIES ('hbase.columns.mapping' = ':key,Personal:Name,Personal:Phone,Office:Phone,Office:Address')
    TBLPROPERTIES ('hbase.table.name' = 'Contacts');
    ```

4. <span data-ttu-id="931ce-175">Aşağıdaki HiveQL betiğini tooquery hello veri hello HBase tablosundaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="931ce-175">Run hello following HiveQL script tooquery hello data in hello HBase table:</span></span>

    ```hiveql   
    SELECT count(rowkey) FROM hbasecontacts;
    ```

## <a name="use-hbase-rest-apis-using-curl"></a><span data-ttu-id="931ce-176">Curl kullanarak HBase REST API’lerini kullanma</span><span class="sxs-lookup"><span data-stu-id="931ce-176">Use HBase REST APIs using Curl</span></span>

<span data-ttu-id="931ce-177">Merhaba REST API aracılığıyla güvenli [temel kimlik doğrulaması](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="931ce-177">hello REST API is secured via [basic authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="931ce-178">Her zaman güvenli HTTP (toohelp olun kimlik bilgilerinizi toohello sunucu güvenli bir şekilde gönderilir HTTPS) kullanarak isteğini hale.</span><span class="sxs-lookup"><span data-stu-id="931ce-178">You shall always make requests by using Secure HTTP (HTTPS) toohelp ensure that your credentials are securely sent toohello server.</span></span>

2. <span data-ttu-id="931ce-179">Komut toolist hello var olan HBase tablolarını aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="931ce-179">Use hello following command toolist hello existing HBase tables:</span></span>

    ```bash
    curl -u <UserName>:<Password> \
    -G https://<ClusterName>.azurehdinsight.net/hbaserest/
    ```

3. <span data-ttu-id="931ce-180">Komut toocreate iki sütun ailesi ile yeni bir HBase tablosu aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="931ce-180">Use hello following command toocreate a new HBase table with two-column families:</span></span>

    ```bash   
    curl -u <UserName>:<Password> \
    -X PUT "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/schema" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    -d "{\"@name\":\"Contact1\",\"ColumnSchema\":[{\"name\":\"Personal\"},{\"name\":\"Office\"}]}" \
    -v
    ```

    <span data-ttu-id="931ce-181">Merhaba şema hello JSon biçiminde sağlanır.</span><span class="sxs-lookup"><span data-stu-id="931ce-181">hello schema is provided in hello JSon format.</span></span>
4. <span data-ttu-id="931ce-182">Komut tooinsert aşağıdaki hello bazı veriler kullanın:</span><span class="sxs-lookup"><span data-stu-id="931ce-182">Use hello following command tooinsert some data:</span></span>

    ```bash   
    curl -u <UserName>:<Password> \
    -X PUT "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/false-row-key" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    -d "{\"Row\":[{\"key\":\"MTAwMA==\",\"Cell\": [{\"column\":\"UGVyc29uYWw6TmFtZQ==\", \"$\":\"Sm9obiBEb2xl\"}]}]}" \
    -v
    ```
   
    <span data-ttu-id="931ce-183">Base64 gerekir hello -d anahtarda belirtilen hello değerleri kodlayın.</span><span class="sxs-lookup"><span data-stu-id="931ce-183">You must base64 encode hello values specified in hello -d switch.</span></span> <span data-ttu-id="931ce-184">Merhaba örnekte:</span><span class="sxs-lookup"><span data-stu-id="931ce-184">In hello example:</span></span>
   
   * <span data-ttu-id="931ce-185">MTAwMA==: 1000</span><span class="sxs-lookup"><span data-stu-id="931ce-185">MTAwMA==: 1000</span></span>
   * <span data-ttu-id="931ce-186">UGVyc29uYWw6TmFtZQ==: Personal:Name</span><span class="sxs-lookup"><span data-stu-id="931ce-186">UGVyc29uYWw6TmFtZQ==: Personal:Name</span></span>
   * <span data-ttu-id="931ce-187">Sm9obiBEb2xl: John Dole</span><span class="sxs-lookup"><span data-stu-id="931ce-187">Sm9obiBEb2xl: John Dole</span></span>
     
     <span data-ttu-id="931ce-188">[false satır anahtarını](https://hbase.apache.org/apidocs/org/apache/hadoop/hbase/rest/package-summary.html#operation_cell_store_single) tooinsert sağlar (toplu) birden çok değer.</span><span class="sxs-lookup"><span data-stu-id="931ce-188">[false-row-key](https://hbase.apache.org/apidocs/org/apache/hadoop/hbase/rest/package-summary.html#operation_cell_store_single) allows you tooinsert multiple (batched) values.</span></span>
5. <span data-ttu-id="931ce-189">Komut tooget bir satır aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="931ce-189">Use hello following command tooget a row:</span></span>
   
    ```bash 
    curl -u <UserName>:<Password> \
    -X GET "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/1000" \
    -H "Accept: application/json" \
    -v
    ```

<span data-ttu-id="931ce-190">HBase Rest hakkında daha fazla bilgi için bkz. [Apache HBase Başvuru Kılavuzu](https://hbase.apache.org/book.html#_rest).</span><span class="sxs-lookup"><span data-stu-id="931ce-190">For more information about HBase Rest, see [Apache HBase Reference Guide](https://hbase.apache.org/book.html#_rest).</span></span>

> [!NOTE]
> <span data-ttu-id="931ce-191">Thrift, HDInsight’ta HBase tarafından desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="931ce-191">Thrift is not supported by HBase in HDInsight.</span></span>
>
> <span data-ttu-id="931ce-192">Curl'ü veya başka bir REST iletişimini WebHCat ile kullanırken, hello kullanıcı adı ve parola hello Hdınsight küme yöneticisinin sağlayarak hello istekleri kimliğini doğrulaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="931ce-192">When using Curl or any other REST communication with WebHCat, you must authenticate hello requests by providing hello user name and password for hello HDInsight cluster administrator.</span></span> <span data-ttu-id="931ce-193">Merhaba Tekdüzen Kaynak Tanımlayıcısı (URI) bir parçası toosend hello istekleri toohello sunucu kullanılan gibi hello küme adını kullanmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="931ce-193">You must also use hello cluster name as part of hello Uniform Resource Identifier (URI) used toosend hello requests toohello server:</span></span>
> 
>   
>        curl -u <UserName>:<Password> \
>        -G https://<ClusterName>.azurehdinsight.net/templeton/v1/status
>   
>    <span data-ttu-id="931ce-194">Yanıt aşağıdaki yanıt benzer toohello almanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="931ce-194">You should receive a response similar toohello following response:</span></span>
>   
>        {"status":"ok","version":"v1"}
   


## <a name="check-cluster-status"></a><span data-ttu-id="931ce-195">Küme durumunu denetleme</span><span class="sxs-lookup"><span data-stu-id="931ce-195">Check cluster status</span></span>
<span data-ttu-id="931ce-196">HDInsight içinde HBase, kümelerin izlenmesi için bir Web Kullanıcı Arabirimi ile birlikte gönderilir.</span><span class="sxs-lookup"><span data-stu-id="931ce-196">HBase in HDInsight ships with a Web UI for monitoring clusters.</span></span> <span data-ttu-id="931ce-197">Merhaba Web kullanıcı arabirimini kullanarak istatistikler veya bölgeler hakkında bilgi isteyebilir.</span><span class="sxs-lookup"><span data-stu-id="931ce-197">Using hello Web UI, you can request statistics or information about regions.</span></span>

<span data-ttu-id="931ce-198">**tooaccess hello HBase ana kullanıcı Arabirimi**</span><span class="sxs-lookup"><span data-stu-id="931ce-198">**tooaccess hello HBase Master UI**</span></span>

1. <span data-ttu-id="931ce-199">Merhaba içine oturum hello Ambari Web kullanıcı Arabirimi https://&lt;Clustername >. azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="931ce-199">Sign into hello hello Ambari Web UI at https://&lt;Clustername>.azurehdinsight.net.</span></span>
2. <span data-ttu-id="931ce-200">Tıklatın **HBase** hello sol menüden.</span><span class="sxs-lookup"><span data-stu-id="931ce-200">Click **HBase** from hello left menu.</span></span>
3. <span data-ttu-id="931ce-201">Tıklatın **hızlı bağlantılar** hello noktası toohello etkin Zookeeper düğüm bağlantı hello Sayfanın üstü ve ardından **HBase ana UI**.</span><span class="sxs-lookup"><span data-stu-id="931ce-201">Click **Quick links** on hello top of hello page, point toohello active Zookeeper node link, and then click **HBase Master UI**.</span></span>  <span data-ttu-id="931ce-202">başka bir tarayıcı sekmesinde Hello kullanıcı Arabirimi açılır:</span><span class="sxs-lookup"><span data-stu-id="931ce-202">hello UI is opened in another browser tab:</span></span>

  ![HDInsight HBase HMaster Kullanıcı Arabirimi](./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-hmaster-ui.png)

  <span data-ttu-id="931ce-204">Merhaba HBase ana UI hello aşağıdaki bölümleri içerir:</span><span class="sxs-lookup"><span data-stu-id="931ce-204">hello HBase Master UI contains hello following sections:</span></span>

  - <span data-ttu-id="931ce-205">Bölge sunucuları</span><span class="sxs-lookup"><span data-stu-id="931ce-205">region servers</span></span>
  - <span data-ttu-id="931ce-206">Yedekleme yöneticileri</span><span class="sxs-lookup"><span data-stu-id="931ce-206">backup masters</span></span>
  - <span data-ttu-id="931ce-207">Tablolar</span><span class="sxs-lookup"><span data-stu-id="931ce-207">tables</span></span>
  - <span data-ttu-id="931ce-208">Görevler</span><span class="sxs-lookup"><span data-stu-id="931ce-208">tasks</span></span>
  - <span data-ttu-id="931ce-209">Yazılım öznitelikleri</span><span class="sxs-lookup"><span data-stu-id="931ce-209">software attributes</span></span>

## <a name="delete-hello-cluster"></a><span data-ttu-id="931ce-210">Merhaba küme silme</span><span class="sxs-lookup"><span data-stu-id="931ce-210">Delete hello cluster</span></span>
<span data-ttu-id="931ce-211">tooavoid tutarsızlıklar hello küme silmeden önce hello HBase tablolarını devre dışı bırakmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="931ce-211">tooavoid inconsistencies, we recommend that you disable hello HBase tables before you delete hello cluster.</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a><span data-ttu-id="931ce-212">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="931ce-212">Troubleshoot</span></span>

<span data-ttu-id="931ce-213">HDInsight kümeleri oluştururken sorun yaşarsanız bkz. [erişim denetimi gereksinimleri](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="931ce-213">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="931ce-214">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="931ce-214">Next steps</span></span>
<span data-ttu-id="931ce-215">Bu makalede, nasıl toocreate bir HBase kümesi ve toocreate tablo ve görünüm bu tablolardaki verileri nasıl hello HBase kabuğunu hello öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="931ce-215">In this article, you learned how toocreate an HBase cluster and how toocreate tables and view hello data in those tables from hello HBase shell.</span></span> <span data-ttu-id="931ce-216">Ayrıca nasıl toouse bir Hive HBase tabloları ve nasıl toouse hello HBase C# REST API'lerini toocreate veriler üzerinde bir HBase tablosu sorgulama ve hello tablosundan verileri öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="931ce-216">You also learned how toouse a Hive query on data in HBase tables and how toouse hello HBase C# REST APIs toocreate an HBase table and retrieve data from hello table.</span></span>

<span data-ttu-id="931ce-217">toolearn daha bakın:</span><span class="sxs-lookup"><span data-stu-id="931ce-217">toolearn more, see:</span></span>

* <span data-ttu-id="931ce-218">[HDInsight HBase'e genel bakış][hdinsight-hbase-overview]: HBase büyük miktarda yapılandırılmamış ve yarı yapılandırılmış veri için rastgele erişim ve güçlü tutarlılık sağlayan, Hadoop'ta yerleşik bir Apache, açık kaynak, NoSQL veritabanıdır.</span><span class="sxs-lookup"><span data-stu-id="931ce-218">[HDInsight HBase overview][hdinsight-hbase-overview]: HBase is an Apache, open-source, NoSQL database built on Hadoop that provides random access and strong consistency for large amounts of unstructured and semistructured data.</span></span>

[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hbase-reference]: http://hbase.apache.org/book.html#importtsv
[hbase-schema]: http://0b4af6cdc2f0c5998459-c0245c5c937c5dedcca3f1764ecc9b2f.r43.cf2.rackcdn.com/9353-login1210_khurana.pdf
[hbase-quick-start]: http://hbase.apache.org/book.html#quickstart





[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
[hdinsight-versions]: hdinsight-component-versioning.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-portal]: https://portal.azure.com/
[azure-create-storageaccount]: http://azure.microsoft.com/documentation/articles/storage-create-storage-account/

[img-hdinsight-hbase-cluster-quick-create]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-quick-create.png
[img-hdinsight-hbase-hive-editor]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-hive-editor.png
[img-hdinsight-hbase-file-browser]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-file-browser.png
[img-hbase-shell]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-shell.png
[img-hbase-sample-data-tabular]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-contacts-tabular.png
[img-hbase-sample-data-bigtable]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-contacts-bigtable.png
