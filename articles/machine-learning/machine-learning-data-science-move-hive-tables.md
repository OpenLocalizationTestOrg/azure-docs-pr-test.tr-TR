---
title: "aaaCreate Hive tabloları ve Azure Blob depolama alanından veri yükleme | Microsoft Docs"
description: "Hive tabloları oluşturma ve blob toohive tablolarındaki verileri yükleme"
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: cff9280d-18ce-4b66-a54f-19f358d1ad90
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 09622972bcac31c2971858393a8340f24e4b7390
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-hive-tables-and-load-data-from-azure-blob-storage"></a><span data-ttu-id="aaf90-103">Hive tabloları oluşturma ve Azure Blob depolama alanından veri yükleme</span><span class="sxs-lookup"><span data-stu-id="aaf90-103">Create Hive tables and load data from Azure Blob Storage</span></span>
<span data-ttu-id="aaf90-104">Bu konu, Hive tabloları oluşturma ve Azure blob depolama alanından veri yükleme genel Hive sorguları gösterir.</span><span class="sxs-lookup"><span data-stu-id="aaf90-104">This topic presents generic Hive queries that create Hive tables and load data from Azure blob storage.</span></span> <span data-ttu-id="aaf90-105">Bazı yönergeler de Hive tablolarını bölümlendirme ve hello en iyi duruma getirilmiş satır sütunlu (ORC) biçimlendirme tooimprove sorgu performansı kullanılarak sağlanır.</span><span class="sxs-lookup"><span data-stu-id="aaf90-105">Some guidance is also provided on partitioning Hive tables and on using hello Optimized Row Columnar (ORC) formatting tooimprove query performance.</span></span>

<span data-ttu-id="aaf90-106">Bu **menü** nasıl burada hello veri depolanabilir ve sırasında işlenen hedef ortamları tooingest verisine takım veri bilimi işlem (TDSP) hello açıklamak tootopics bağlar.</span><span class="sxs-lookup"><span data-stu-id="aaf90-106">This **menu** links tootopics that describe how tooingest data into target environments where hello data can be stored and processed during hello Team Data Science Process (TDSP).</span></span>

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

## <a name="prerequisites"></a><span data-ttu-id="aaf90-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="aaf90-107">Prerequisites</span></span>
<span data-ttu-id="aaf90-108">Bu makalede, sahip olduğunuz varsayılmaktadır:</span><span class="sxs-lookup"><span data-stu-id="aaf90-108">This article assumes that you have:</span></span>

* <span data-ttu-id="aaf90-109">Bir Azure depolama hesabı oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="aaf90-109">Created an Azure storage account.</span></span> <span data-ttu-id="aaf90-110">Yönergeler gerekiyorsa bkz [Azure storage hesapları hakkında](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="aaf90-110">If you need instructions, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>
* <span data-ttu-id="aaf90-111">Özelleştirilmiş bir Hadoop kümesine hello Hdınsight hizmeti ile sağlandı.</span><span class="sxs-lookup"><span data-stu-id="aaf90-111">Provisioned a customized Hadoop cluster with hello HDInsight service.</span></span>  <span data-ttu-id="aaf90-112">Yönergeler gerekiyorsa bkz [özelleştirme Azure Hdınsight Hadoop kümeleri için Gelişmiş analiz](machine-learning-data-science-customize-hadoop-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="aaf90-112">If you need instructions, see [Customize Azure HDInsight Hadoop clusters for advanced analytics](machine-learning-data-science-customize-hadoop-cluster.md).</span></span>
* <span data-ttu-id="aaf90-113">Etkin uzaktan erişim toohello küme, oturum açmış ve hello Hadoop komut satırı konsolu açılır.</span><span class="sxs-lookup"><span data-stu-id="aaf90-113">Enabled remote access toohello cluster, logged in, and opened hello Hadoop Command-Line console.</span></span> <span data-ttu-id="aaf90-114">Yönergeler gerekiyorsa bkz [erişim hello Hadoop kümesi, baş düğüm](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span><span class="sxs-lookup"><span data-stu-id="aaf90-114">If you need instructions, see [Access hello Head Node of Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span></span>

## <a name="upload-data-tooazure-blob-storage"></a><span data-ttu-id="aaf90-115">Veri tooAzure blob depolama yükleme</span><span class="sxs-lookup"><span data-stu-id="aaf90-115">Upload data tooAzure blob storage</span></span>
<span data-ttu-id="aaf90-116">Sağlanan hello yönergeleri izleyerek bir Azure sanal makinesi oluşturduysanız [Gelişmiş analiz için Azure sanal makinesi ayarlama](machine-learning-data-science-setup-virtual-machine.md), bu komut dosyası indirilen toohello olması gereken *C:\\ Kullanıcıların\\\<kullanıcı adı\>\\belgeleri\\veri bilimi betikleri* hello sanal makine üzerinde dizin.</span><span class="sxs-lookup"><span data-stu-id="aaf90-116">If you created an Azure virtual machine by following hello instructions provided in [Set up an Azure virtual machine for advanced analytics](machine-learning-data-science-setup-virtual-machine.md), this script file should have been downloaded toohello *C:\\Users\\\<user name\>\\Documents\\Data Science Scripts* directory on hello virtual machine.</span></span> <span data-ttu-id="aaf90-117">Bu Hive sorguları yalnızca kendi veri şeması ve Azure blob depolama hello uygun alanları toobe gönderimi için hazır yapılandırmasında takın gerektirir.</span><span class="sxs-lookup"><span data-stu-id="aaf90-117">These Hive queries only require that you plug in your own data schema and Azure blob storage configuration in hello appropriate fields toobe ready for submission.</span></span>

<span data-ttu-id="aaf90-118">Hive tablolarını hello veri olduğunu varsayıyoruz bir **sıkıştırılmamış** tablo biçiminde ve hello verileri karşıya yüklenen toohello varsayılan (veya tooan ek) kaldırıldı hello Hadoop küme tarafından kullanılan hello depolama hesabının kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="aaf90-118">We assume that hello data for Hive tables is in an **uncompressed** tabular format, and that hello data has been uploaded toohello default (or tooan additional) container of hello storage account used by hello Hadoop cluster.</span></span>

<span data-ttu-id="aaf90-119">Merhaba üzerinde toopractice istiyorsanız **NYC ücreti seyahat veri**, gerekir:</span><span class="sxs-lookup"><span data-stu-id="aaf90-119">If you want toopractice on hello **NYC Taxi Trip Data**, you need to:</span></span>

* <span data-ttu-id="aaf90-120">**karşıdan** hello 24 [NYC ücreti seyahat veri](http://www.andresmh.com/nyctaxitrips) (12 seyahat dosyalar ve 12 ücreti dosyaları)</span><span class="sxs-lookup"><span data-stu-id="aaf90-120">**download** hello 24 [NYC Taxi Trip Data](http://www.andresmh.com/nyctaxitrips) files (12 Trip files and 12 Fare files),</span></span>
* <span data-ttu-id="aaf90-121">**Unzip** .csv dosyalarına tüm dosyaları ve ardından</span><span class="sxs-lookup"><span data-stu-id="aaf90-121">**unzip** all files into .csv files, and then</span></span>
* <span data-ttu-id="aaf90-122">**karşıya yükleme** bunları toohello varsayılan (veya uygun bir kapsayıcı) hello hello özetlenen hello yordamı tarafından oluşturulan Azure depolama hesabı [özelleştirme Azure Hdınsight Hadoop kümeleri Advanced Analytics işlem ve teknoloji ](machine-learning-data-science-customize-hadoop-cluster.md) konu.</span><span class="sxs-lookup"><span data-stu-id="aaf90-122">**upload** them toohello default (or appropriate container) of hello Azure storage account that was created by hello procedure outlined in hello [Customize Azure HDInsight Hadoop clusters for Advanced Analytics Process and Technology](machine-learning-data-science-customize-hadoop-cluster.md) topic.</span></span> <span data-ttu-id="aaf90-123">Bu bilgisayarda Hello işlem tooupload hello .csv dosyaları toohello varsayılan kapsayıcı hello depolama hesabında bulunabilir [sayfa](machine-learning-data-science-process-hive-walkthrough.md#upload).</span><span class="sxs-lookup"><span data-stu-id="aaf90-123">hello process tooupload hello .csv files toohello default container on hello storage account can be found on this [page](machine-learning-data-science-process-hive-walkthrough.md#upload).</span></span>

## <span data-ttu-id="aaf90-124"><a name="submit"></a>Nasıl toosubmit Hive sorguları</span><span class="sxs-lookup"><span data-stu-id="aaf90-124"><a name="submit"></a>How toosubmit Hive queries</span></span>
<span data-ttu-id="aaf90-125">Hive sorgularını kullanarak gönderilebilir:</span><span class="sxs-lookup"><span data-stu-id="aaf90-125">Hive queries can be submitted by using:</span></span>

1. [<span data-ttu-id="aaf90-126">Hadoop kümesi headnode Hive sorguları Hadoop komut satırı aracılığıyla gönderme</span><span class="sxs-lookup"><span data-stu-id="aaf90-126">Submit Hive queries through Hadoop Command Line in headnode of Hadoop cluster</span></span>](#headnode)
2. [<span data-ttu-id="aaf90-127">Hive sorguları hello Hive Düzenleyicisi ile gönderme</span><span class="sxs-lookup"><span data-stu-id="aaf90-127">Submit Hive queries with hello Hive Editor</span></span>](#hive-editor)
3. [<span data-ttu-id="aaf90-128">Azure PowerShell komutlarıyla Hive sorguları gönderme</span><span class="sxs-lookup"><span data-stu-id="aaf90-128">Submit Hive queries with Azure PowerShell Commands</span></span>](#ps)

<span data-ttu-id="aaf90-129">Hive sorguları SQL benzeri.</span><span class="sxs-lookup"><span data-stu-id="aaf90-129">Hive queries are SQL-like.</span></span> <span data-ttu-id="aaf90-130">SQL ile bilginiz varsa, hello bulabilirsiniz [Hive SQL kullanıcılar kopya sayfası](http://hortonworks.com/wp-content/uploads/2013/05/hql_cheat_sheet.pdf) yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="aaf90-130">If you are familiar with SQL, you may find hello [Hive for SQL Users Cheat Sheet](http://hortonworks.com/wp-content/uploads/2013/05/hql_cheat_sheet.pdf) useful.</span></span>

<span data-ttu-id="aaf90-131">Bir Hive sorgusu gönderirken, ayrıca hello hedef Hive sorguları hello çıktısı, dosyada Merhaba ekranında veya tooa yerel hello baş düğüme veya tooan Azure blob olması olup olmadığını kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aaf90-131">When submitting a Hive query, you can also control hello destination of hello output from Hive queries, whether it be on hello screen or tooa local file on hello head node or tooan Azure blob.</span></span>

### <span data-ttu-id="aaf90-132"><a name="headnode"></a> 1. Hadoop kümesi headnode Hive sorguları Hadoop komut satırı aracılığıyla gönderme</span><span class="sxs-lookup"><span data-stu-id="aaf90-132"><a name="headnode"></a> 1. Submit Hive queries through Hadoop Command Line in headnode of Hadoop cluster</span></span>
<span data-ttu-id="aaf90-133">Sorgu doğrudan hello Hadoop küme baş düğümüne hello içinde genellikle bir Hive düzenleyicisinde veya Azure PowerShell komut dosyaları ile gönderme daha toofaster dönüş müşteri adayları gönderme karmaşık ise Hello yığını.</span><span class="sxs-lookup"><span data-stu-id="aaf90-133">If hello Hive query is complex, submitting it directly in hello head node of hello Hadoop cluster typically leads toofaster turn around than submitting it with a Hive Editor or Azure PowerShell scripts.</span></span>

<span data-ttu-id="aaf90-134">Toohello baş hello Hadoop küme düğümünde oturum, hello baş düğümü hello masaüstünde hello Hadoop komut satırı açın ve komutu girin `cd %hive_home%\bin`.</span><span class="sxs-lookup"><span data-stu-id="aaf90-134">Log in toohello head node of hello Hadoop cluster, open hello Hadoop Command Line on hello desktop of hello head node, and enter command `cd %hive_home%\bin`.</span></span>

<span data-ttu-id="aaf90-135">Üç yolu toosubmit Hive sorguları hello Hadoop komut satırı vardır:</span><span class="sxs-lookup"><span data-stu-id="aaf90-135">You have three ways toosubmit Hive queries in hello Hadoop Command Line:</span></span>

* <span data-ttu-id="aaf90-136">doğrudan</span><span class="sxs-lookup"><span data-stu-id="aaf90-136">directly</span></span>
* <span data-ttu-id="aaf90-137">.hql dosyalarını kullanma</span><span class="sxs-lookup"><span data-stu-id="aaf90-137">using .hql files</span></span>
* <span data-ttu-id="aaf90-138">komut konsolundan ile Merhaba yığını</span><span class="sxs-lookup"><span data-stu-id="aaf90-138">with hello Hive command console</span></span>

#### <a name="submit-hive-queries-directly-in-hadoop-command-line"></a><span data-ttu-id="aaf90-139">Hive sorguları doğrudan içinde Hadoop komut satırı gönderin.</span><span class="sxs-lookup"><span data-stu-id="aaf90-139">Submit Hive queries directly in Hadoop Command Line.</span></span>
<span data-ttu-id="aaf90-140">Komutu gibi çalıştırabilirsiniz `hive -e "<your hive query>;` toosubmit basit Hive sorguları doğrudan içinde Hadoop komut satırı.</span><span class="sxs-lookup"><span data-stu-id="aaf90-140">You can run command like `hive -e "<your hive query>;` toosubmit simple Hive queries directly in Hadoop Command Line.</span></span> <span data-ttu-id="aaf90-141">Burada, burada hello kırmızı kutusunu ana hatlarını hello Hive sorgusu gönderdiğinde komutu hello ve yeşil kutusu anahatları hello hello Hive sorgusu çıktısını hello bir örnek verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="aaf90-141">Here is an example, where hello red box outlines hello command that submits hello Hive query, and hello green box outlines hello output from hello Hive query.</span></span>

![Çalışma alanı oluşturma](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-1.png)

#### <a name="submit-hive-queries-in-hql-files"></a><span data-ttu-id="aaf90-143">Hive sorguları .hql dosyalarında gönderme</span><span class="sxs-lookup"><span data-stu-id="aaf90-143">Submit Hive queries in .hql files</span></span>
<span data-ttu-id="aaf90-144">Komut satırı ya da Hive komut konsolundan sorguları düzenleme, Hello Hive sorgusu daha karmaşık ve birden fazla satır olduğunda, pratik değil.</span><span class="sxs-lookup"><span data-stu-id="aaf90-144">When hello Hive query is more complicated and has multiple lines, editing queries in command line or Hive command console is not practical.</span></span> <span data-ttu-id="aaf90-145">Bir metin düzenleyicisi toouse hello Hadoop küme toosave hello Hive sorguları hello baş düğümü yerel bir dizine .hql dosyasında baş düğümünde hello alternatiftir.</span><span class="sxs-lookup"><span data-stu-id="aaf90-145">An alternative is toouse a text editor in hello head node of hello Hadoop cluster toosave hello Hive queries in a .hql file in a local directory of hello head node.</span></span> <span data-ttu-id="aaf90-146">Hello Hive sorgusu hello .hql dosyasında hello kullanarak gönderilebilir sonra `-f` bağımsız değişken olarak aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="aaf90-146">Then hello Hive query in hello .hql file can be submitted by using hello `-f` argument as follows:</span></span>

    hive -f "<path toohello .hql file>"

![Çalışma alanı oluşturma](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-3.png)

<span data-ttu-id="aaf90-148">**İlerleme durumu ekranı yazdırma Hive sorgularının gösterme**</span><span class="sxs-lookup"><span data-stu-id="aaf90-148">**Suppress progress status screen print of Hive queries**</span></span>

<span data-ttu-id="aaf90-149">Hive sorgusu Hadoop komutu gönderildikten sonra varsayılan olarak, hello işinin ilerleme durumunu hello harita/azaltın ekranda yazdırılır.</span><span class="sxs-lookup"><span data-stu-id="aaf90-149">By default, after Hive query is submitted in Hadoop Command Line, hello progress of hello Map/Reduce job is printed out on screen.</span></span> <span data-ttu-id="aaf90-150">toosuppress Merhaba hello harita/azaltın ilerleyişini ekran Yazdır, bağımsız değişken kullanabilirsiniz `-S` (büyük harflerle "S") gibi komut satırı hello:</span><span class="sxs-lookup"><span data-stu-id="aaf90-150">toosuppress hello screen print of hello Map/Reduce job progress, you can use an argument `-S` ("S" in upper case) in hello command line as follows:</span></span>

    hive -S -f "<path toohello .hql file>"
<span data-ttu-id="aaf90-151">.</span><span class="sxs-lookup"><span data-stu-id="aaf90-151">.</span></span>    <span data-ttu-id="aaf90-152">-S -e hive "<Hive queries>"</span><span class="sxs-lookup"><span data-stu-id="aaf90-152">hive -S -e "<Hive queries>"</span></span>

#### <a name="submit-hive-queries-in-hive-command-console"></a><span data-ttu-id="aaf90-153">Hive komut konsolunda Hive sorguları göndermek.</span><span class="sxs-lookup"><span data-stu-id="aaf90-153">Submit Hive queries in Hive command console.</span></span>
<span data-ttu-id="aaf90-154">Komutunu çalıştırarak da ilk hello Hive komut konsolundan girebilirsiniz `hive` Hadoop komut satırı ve Hive komut konsolunda Hive sorguları göndermek.</span><span class="sxs-lookup"><span data-stu-id="aaf90-154">You can also first enter hello Hive command console by running command `hive` in Hadoop Command Line, and then submit Hive queries in Hive command console.</span></span> <span data-ttu-id="aaf90-155">Bir örnek verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="aaf90-155">Here is an example.</span></span> <span data-ttu-id="aaf90-156">Bu örnekte, hello iki kırmızı kutuları Vurgu hello kullanılan komutlar tooenter Hive komut konsolundan hello ve Hive sorgusu Hive komut konsolunda sırasıyla gönderilen Merhaba.</span><span class="sxs-lookup"><span data-stu-id="aaf90-156">In this example, hello two red boxes highlight hello commands used tooenter hello Hive command console, and hello Hive query submitted in Hive command console, respectively.</span></span> <span data-ttu-id="aaf90-157">Merhaba yeşil kutusunu hello Hive sorgusu hello çıktısını vurgular.</span><span class="sxs-lookup"><span data-stu-id="aaf90-157">hello green box highlights hello output from hello Hive query.</span></span>

![Çalışma alanı oluşturma](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-2.png)

<span data-ttu-id="aaf90-159">Önceki örneklerde Hello doğrudan hello Hive sorgu sonuçları ekranda çıktı.</span><span class="sxs-lookup"><span data-stu-id="aaf90-159">hello previous examples directly output hello Hive query results on screen.</span></span> <span data-ttu-id="aaf90-160">Merhaba çıktı tooa yerel dosya hello baş düğüme veya tooan Azure blob de yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aaf90-160">You can also write hello output tooa local file on hello head node, or tooan Azure blob.</span></span> <span data-ttu-id="aaf90-161">Sonra diğer araçlarını kullanabilirsiniz toofurther analiz Hive sorguları hello çıktısı.</span><span class="sxs-lookup"><span data-stu-id="aaf90-161">Then, you can use other tools toofurther analyze hello output of Hive queries.</span></span>

<span data-ttu-id="aaf90-162">**Hive sorgusu sonuçları tooa yerel dosya çıktı.**</span><span class="sxs-lookup"><span data-stu-id="aaf90-162">**Output Hive query results tooa local file.**</span></span>
<span data-ttu-id="aaf90-163">toooutput Hive sorgusu sonuçları tooa yerel dizin hello baş düğümünde, toosubmit hello Hive sorgusu hello Hadoop komut satırı aşağıdaki gibi vardır:</span><span class="sxs-lookup"><span data-stu-id="aaf90-163">toooutput Hive query results tooa local directory on hello head node, you have toosubmit hello Hive query in hello Hadoop Command Line as follows:</span></span>

    hive -e "<hive query>" > <local path in hello head node>

<span data-ttu-id="aaf90-164">Aşağıdaki örneğine hello Hive sorgusu hello çıktısını bir dosyaya yazılır `hivequeryoutput.txt` dizininde `C:\apps\temp`.</span><span class="sxs-lookup"><span data-stu-id="aaf90-164">In hello following example, hello output of Hive query is written into a file `hivequeryoutput.txt` in directory `C:\apps\temp`.</span></span>

![Çalışma alanı oluşturma](./media/machine-learning-data-science-move-hive-tables/output-hive-results-1.png)

<span data-ttu-id="aaf90-166">**Hive sorgusu sonuçları tooan Azure blob çıkış**</span><span class="sxs-lookup"><span data-stu-id="aaf90-166">**Output Hive query results tooan Azure blob**</span></span>

<span data-ttu-id="aaf90-167">Ayrıca hello Hive sorgusu sonuçları tooan hello varsayılan kapsayıcı hello Hadoop kümesi içindeki Azure blob çıkarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aaf90-167">You can also output hello Hive query results tooan Azure blob, within hello default container of hello Hadoop cluster.</span></span> <span data-ttu-id="aaf90-168">Bu Hello Hive sorgusu aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="aaf90-168">hello Hive query for this is as follows:</span></span>

    insert overwrite directory wasb:///<directory within hello default container> <select clause from ...>

<span data-ttu-id="aaf90-169">Aşağıdaki örneğine hello Hive sorgusu hello çıktısını tooa blob dizin yazılır `queryoutputdir` hello varsayılan kapsayıcı hello Hadoop kümesi içinde.</span><span class="sxs-lookup"><span data-stu-id="aaf90-169">In hello following example, hello output of Hive query is written tooa blob directory `queryoutputdir` within hello default container of hello Hadoop cluster.</span></span> <span data-ttu-id="aaf90-170">Burada, yalnızca hello blob adı olmadan tooprovide hello dizin adı gerekir.</span><span class="sxs-lookup"><span data-stu-id="aaf90-170">Here, you only need tooprovide hello directory name, without hello blob name.</span></span> <span data-ttu-id="aaf90-171">Dizin ve blob adları gibi sağlarsanız, bir hata atılır `wasb:///queryoutputdir/queryoutput.txt`.</span><span class="sxs-lookup"><span data-stu-id="aaf90-171">An error is thrown if you provide both directory and blob names, such as `wasb:///queryoutputdir/queryoutput.txt`.</span></span>

![Çalışma alanı oluşturma](./media/machine-learning-data-science-move-hive-tables/output-hive-results-2.png)

<span data-ttu-id="aaf90-173">Azure Storage Gezgini kullanarak hello Hadoop kümesi hello varsayılan kapsayıcı açarsanız, hello aşağıdaki şekilde gösterildiği gibi hello Hive sorgusu hello çıktısını görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aaf90-173">If you open hello default container of hello Hadoop cluster using Azure Storage Explorer, you can see hello output of hello Hive query as shown in hello following figure.</span></span> <span data-ttu-id="aaf90-174">Merhaba (kırmızı kutu ile vurgulanan) filtre tooonly alma hello blob adlarındaki belirtilen harflerle uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aaf90-174">You can apply hello filter (highlighted by red box) tooonly retrieve hello blob with specified letters in names.</span></span>

![Çalışma alanı oluşturma](./media/machine-learning-data-science-move-hive-tables/output-hive-results-3.png)

### <span data-ttu-id="aaf90-176"><a name="hive-editor"></a> 2. Hive sorguları hello Hive Düzenleyicisi ile gönderme</span><span class="sxs-lookup"><span data-stu-id="aaf90-176"><a name="hive-editor"></a> 2. Submit Hive queries with hello Hive Editor</span></span>
<span data-ttu-id="aaf90-177">Merhaba form URL'sini girerek hello sorgu konsol (Düzenleyicisi Hive) de kullanabilirsiniz *https://&#60; Hadoop küme adı >.azurehdinsight.net/Home/HiveEditor* bir web tarayıcısı içine.</span><span class="sxs-lookup"><span data-stu-id="aaf90-177">You can also use hello Query Console (Hive Editor) by entering a URL of hello form *https://&#60;Hadoop cluster name>.azurehdinsight.net/Home/HiveEditor* into a web browser.</span></span> <span data-ttu-id="aaf90-178">Olması gerekir bu konsolu hello bakın oturum ve gereken şekilde, Hadoop küme kimlik.</span><span class="sxs-lookup"><span data-stu-id="aaf90-178">You must be logged in hello see this console and so you need your Hadoop cluster credentials here.</span></span>

### <span data-ttu-id="aaf90-179"><a name="ps"></a> 3. Azure PowerShell komutlarıyla Hive sorguları gönderme</span><span class="sxs-lookup"><span data-stu-id="aaf90-179"><a name="ps"></a> 3. Submit Hive queries with Azure PowerShell Commands</span></span>
<span data-ttu-id="aaf90-180">PowerShell toosubmit Hive sorguları de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aaf90-180">You can also use PowerShell toosubmit Hive queries.</span></span> <span data-ttu-id="aaf90-181">Yönergeler için bkz: [gönderme Hive işleri PowerShell kullanarak](../hdinsight/hdinsight-hadoop-use-hive-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="aaf90-181">For instructions, see [Submit Hive jobs using PowerShell](../hdinsight/hdinsight-hadoop-use-hive-powershell.md).</span></span>

## <span data-ttu-id="aaf90-182"><a name="create-tables"></a>Hive veritabanı ve tablo oluşturma</span><span class="sxs-lookup"><span data-stu-id="aaf90-182"><a name="create-tables"></a>Create Hive database and tables</span></span>
<span data-ttu-id="aaf90-183">Merhaba Hive sorguları hello paylaşılan [GitHub deposunu](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_db_tbls_load_data_generic.hql) ve buradan yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="aaf90-183">hello Hive queries are shared in hello [GitHub repository](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_db_tbls_load_data_generic.hql) and can be downloaded from there.</span></span>

<span data-ttu-id="aaf90-184">Bir Hive tablosu oluşturur hello Hive sorgusu aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="aaf90-184">Here is hello Hive query that creates a Hive table.</span></span>

    create database if not exists <database name>;
    CREATE EXTERNAL TABLE if not exists <database name>.<table name>
    (
        field1 string,
        field2 int,
        field3 float,
        field4 double,
        ...,
        fieldN string
    )
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>' lines terminated by '<line separator>'
    STORED AS TEXTFILE LOCATION '<storage location>' TBLPROPERTIES("skip.header.line.count"="1");

<span data-ttu-id="aaf90-185">Merhaba, tooplug gereken hello alanlarının açıklamaları ve diğer yapılandırmalar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="aaf90-185">Here are hello descriptions of hello fields that you need tooplug in and other configurations:</span></span>

* <span data-ttu-id="aaf90-186">**&#60; veritabanı adı >**: toocreate istediğiniz hello veritabanının hello adı.</span><span class="sxs-lookup"><span data-stu-id="aaf90-186">**&#60;database name>**: hello name of hello database that you want toocreate.</span></span> <span data-ttu-id="aaf90-187">Yalnızca toouse hello varsayılan veritabanı istiyorsanız, sorgu hello *veritabanı oluştur...*  atlanabilir.</span><span class="sxs-lookup"><span data-stu-id="aaf90-187">If you just want toouse hello default database, hello query *create database...* can be omitted.</span></span>
* <span data-ttu-id="aaf90-188">**&#60; tablo adı >**: hello belirtilen veritabanı içinde toocreate istediğiniz Merhaba tablonun hello adı.</span><span class="sxs-lookup"><span data-stu-id="aaf90-188">**&#60;table name>**: hello name of hello table that you want toocreate within hello specified database.</span></span> <span data-ttu-id="aaf90-189">Toouse hello varsayılan veritabanı istiyorsanız hello tablo doğrudan göre başvurulabilen *&#60; tablo adı >* olmadan &#60; veritabanı adı >.</span><span class="sxs-lookup"><span data-stu-id="aaf90-189">If you want toouse hello default database, hello table can be directly referred by *&#60;table name>* without &#60;database name>.</span></span>
* <span data-ttu-id="aaf90-190">**&#60; alan ayırıcı >**: hello veri dosyası toobe alanlarında sınırlandıran hello ayırıcı karşıya toohello Hive tablosu.</span><span class="sxs-lookup"><span data-stu-id="aaf90-190">**&#60;field separator>**: hello separator that delimits fields in hello data file toobe uploaded toohello Hive table.</span></span>
* <span data-ttu-id="aaf90-191">**&#60; satır ayırıcı >**: hello veri dosyasındaki satır sınırlandıran hello ayırıcı.</span><span class="sxs-lookup"><span data-stu-id="aaf90-191">**&#60;line separator>**: hello separator that delimits lines in hello data file.</span></span>
* <span data-ttu-id="aaf90-192">**&#60; depolama konumu >**: Azure depolama konumu toosave hello veri Hive tablolarını hello.</span><span class="sxs-lookup"><span data-stu-id="aaf90-192">**&#60;storage location>**: hello Azure storage location toosave hello data of Hive tables.</span></span> <span data-ttu-id="aaf90-193">Belirtmezseniz, *konum &#60; depolama konumu >*hello veritabanı ve hello tabloları depolanmış *hive/ambarı/* hello varsayılan kapsayıcısında hello Hive kümenin varsayılan dizin.</span><span class="sxs-lookup"><span data-stu-id="aaf90-193">If you do not specify *LOCATION &#60;storage location>*, hello database and hello tables are stored in *hive/warehouse/* directory in hello default container of hello Hive cluster by default.</span></span> <span data-ttu-id="aaf90-194">Merhaba depolama konumu hello varsayılan kapsayıcı hello veritabanı ve tablo içindeki toobe içeriyor, bu toospecify hello depolama konumu istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="aaf90-194">If you want toospecify hello storage location, hello storage location has toobe within hello default container for hello database and tables.</span></span> <span data-ttu-id="aaf90-195">Bu konum hello biçiminde hello kümesinin konumu göreli toohello varsayılan kapsayıcı olarak adlandırılan toobe sahip *' wasb: / / / &#60; 1 dizini > /'* veya *' wasb: / / / &#60; 1 dizini > / &#60; 2 dizini > /'*, vb.. Merhaba sorgu yürütüldükten sonra hello göreli dizinleri hello varsayılan kapsayıcı içinde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="aaf90-195">This location has toobe referred as location relative toohello default container of hello cluster in hello format of *'wasb:///&#60;directory 1>/'* or *'wasb:///&#60;directory 1>/&#60;directory 2>/'*, etc. After hello query is executed, hello relative directories are created within hello default container.</span></span>
* <span data-ttu-id="aaf90-196">**TBLPROPERTIES("Skip.header.Line.Count"="1")**: hello veri dosyası bir başlık satırı varsa, bu özellik tooadd sahip **hello sonunda** Merhaba, *tablo oluşturma* sorgu.</span><span class="sxs-lookup"><span data-stu-id="aaf90-196">**TBLPROPERTIES("skip.header.line.count"="1")**: If hello data file has a header line, you have tooadd this property **at hello end** of hello *create table* query.</span></span> <span data-ttu-id="aaf90-197">Aksi takdirde hello başlık satırı kayıt toohello tablo olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="aaf90-197">Otherwise, hello header line is loaded as a record toohello table.</span></span> <span data-ttu-id="aaf90-198">Merhaba veri dosyası bir başlık satırı yok, bu yapılandırma hello Sorguda atlanabilir.</span><span class="sxs-lookup"><span data-stu-id="aaf90-198">If hello data file does not have a header line, this configuration can be omitted in hello query.</span></span>

## <span data-ttu-id="aaf90-199"><a name="load-data"></a>Yük veri tooHive tabloları</span><span class="sxs-lookup"><span data-stu-id="aaf90-199"><a name="load-data"></a>Load data tooHive tables</span></span>
<span data-ttu-id="aaf90-200">Burada, Hive tabloya veri yükler hello Hive sorgusu verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="aaf90-200">Here is hello Hive query that loads data into a Hive table.</span></span>

    LOAD DATA INPATH '<path tooblob data>' INTO TABLE <database name>.<table name>;

* <span data-ttu-id="aaf90-201">**&#60; yolu tooblob veri >**: hello blob dosya karşıya toobe toohello Hive tablosu hello varsayılan kapsayıcının hello Hdınsight Hadoop kümesi içinde ise, hello *&#60; yolu tooblob veri >* hello biçiminde olmalıdır *' wasb: / / / &#60; bu kapsayıcıda dizini > / &#60; blob dosya adı >'*.</span><span class="sxs-lookup"><span data-stu-id="aaf90-201">**&#60;path tooblob data>**: If hello blob file toobe uploaded toohello Hive table is in hello default container of hello HDInsight Hadoop cluster, hello *&#60;path tooblob data>* should be in hello format *'wasb:///&#60;directory in this container>/&#60;blob file name>'*.</span></span> <span data-ttu-id="aaf90-202">Merhaba blob dosya da hello Hdınsight Hadoop kümesi ek bir kapsayıcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="aaf90-202">hello blob file can also be in an additional container of hello HDInsight Hadoop cluster.</span></span> <span data-ttu-id="aaf90-203">Bu durumda, *&#60; yolu tooblob veri >* hello biçiminde olmalıdır *' wasb: / / &#60; kapsayıcı adı > @&#60; depolama hesabı adı >.blob.core.windows.net/ &#60; blob dosya adı >'*.</span><span class="sxs-lookup"><span data-stu-id="aaf90-203">In this case, *&#60;path tooblob data>* should be in hello format *'wasb://&#60;container name>@&#60;storage account name>.blob.core.windows.net/&#60;blob file name>'*.</span></span>

  > [!NOTE]
  > <span data-ttu-id="aaf90-204">Merhaba blob veri karşıya toobe tooHive tablosu toobe hello varsayılan veya hello depolama hesabının hello Hadoop kümesi için ek kapsayıcı vardır.</span><span class="sxs-lookup"><span data-stu-id="aaf90-204">hello blob data toobe uploaded tooHive table has toobe in hello default or additional container of hello storage account for hello Hadoop cluster.</span></span> <span data-ttu-id="aaf90-205">Aksi takdirde hello *veri yükleme* sorgu başarısız şikayetçi hello veri erişemiyor.</span><span class="sxs-lookup"><span data-stu-id="aaf90-205">Otherwise, hello *LOAD DATA* query fails complaining that it cannot access hello data.</span></span>
  >
  >

## <span data-ttu-id="aaf90-206"><a name="partition-orc"></a>Gelişmiş konular: Tablo ve Depolama yığını verileri ORC biçiminde bölümlenmiş</span><span class="sxs-lookup"><span data-stu-id="aaf90-206"><a name="partition-orc"></a>Advanced topics: partitioned table and store Hive data in ORC format</span></span>
<span data-ttu-id="aaf90-207">Merhaba veri büyükse hello tablo bölümleme yalnızca birkaç bölümleri Merhaba tablonun tooscan gerektiren sorgular için faydalıdır.</span><span class="sxs-lookup"><span data-stu-id="aaf90-207">If hello data is large, partitioning hello table is beneficial for queries that only need tooscan a few partitions of hello table.</span></span> <span data-ttu-id="aaf90-208">Örneğin, tarih tarafından makul toopartition hello günlük verileri bir web sitesinin olabilir.</span><span class="sxs-lookup"><span data-stu-id="aaf90-208">For instance, it is reasonable toopartition hello log data of a web site by dates.</span></span>

<span data-ttu-id="aaf90-209">Toplama toopartitioning tabloları Hive, ayrıca yararlı toostore hello Hive verileri hello en iyi duruma getirilmiş satır sütunlu (ORC) biçiminde olur.</span><span class="sxs-lookup"><span data-stu-id="aaf90-209">In addition toopartitioning Hive tables, it is also beneficial toostore hello Hive data in hello Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="aaf90-210">ORC biçimlendirme daha fazla bilgi için bkz: <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC#LanguageManualORC-ORCFiles" target="_blank">kullanarak ORC dosyaları Hive okuma, yazma ve verileri işlerken performansını artırır</a>.</span><span class="sxs-lookup"><span data-stu-id="aaf90-210">For more information on ORC formatting, see <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC#LanguageManualORC-ORCFiles" target="_blank">Using ORC files improves performance when Hive is reading, writing, and processing data</a>.</span></span>

### <a name="partitioned-table"></a><span data-ttu-id="aaf90-211">Bölümlenmiş bir tablo</span><span class="sxs-lookup"><span data-stu-id="aaf90-211">Partitioned table</span></span>
<span data-ttu-id="aaf90-212">Bölümlenmiş bir tablo oluşturur ve veri içine yükler hello Hive sorgusu aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="aaf90-212">Here is hello Hive query that creates a partitioned table and loads data into it.</span></span>

    CREATE EXTERNAL TABLE IF NOT EXISTS <database name>.<table name>
    (field1 string,
    ...
    fieldN string
    )
    PARTITIONED BY (<partitionfieldname> vartype) ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>'
         lines terminated by '<line separator>' TBLPROPERTIES("skip.header.line.count"="1");
    LOAD DATA INPATH '<path toohello source file>' INTO TABLE <database name>.<partitioned table name>
        PARTITION (<partitionfieldname>=<partitionfieldvalue>);

<span data-ttu-id="aaf90-213">Bölümlenmiş tablolar sorgulanırken tooadd hello bölüm hello koşulunda önerilir **başına** Merhaba, `where` yan tümcesi bu olarak önemli ölçüde arama hello sürecinin artırır.</span><span class="sxs-lookup"><span data-stu-id="aaf90-213">When querying partitioned tables, it is recommended tooadd hello partition condition in hello **beginning** of hello `where` clause as this improves hello efficacy of searching significantly.</span></span>

    select
        field1, field2, ..., fieldN
    from <database name>.<partitioned table name>
    where <partitionfieldname>=<partitionfieldvalue> and ...;

### <span data-ttu-id="aaf90-214"><a name="orc"></a>Hive verileri ORC biçiminde depolayan</span><span class="sxs-lookup"><span data-stu-id="aaf90-214"><a name="orc"></a>Store Hive data in ORC format</span></span>
<span data-ttu-id="aaf90-215">Merhaba ORC biçiminde depolanan Hive tablolara blob depolama alanından verileri doğrudan yüklenemiyor.</span><span class="sxs-lookup"><span data-stu-id="aaf90-215">You cannot directly load data from blob storage into Hive tables that is stored in hello ORC format.</span></span> <span data-ttu-id="aaf90-216">Merhaba adımlar şunlardır tootake tooload verileri azure'dan ihtiyacınız o hello ORC biçiminde depolanan tooHive tabloları BLOB '.</span><span class="sxs-lookup"><span data-stu-id="aaf90-216">Here are hello steps that hello you need tootake tooload data from Azure blobs tooHive tables stored in ORC format.</span></span>

<span data-ttu-id="aaf90-217">Bir dış tablo oluşturma **DEPOLANAN AS TEXTFILE** ve blob depolama toohello tablodan veri yükleme.</span><span class="sxs-lookup"><span data-stu-id="aaf90-217">Create an external table **STORED AS TEXTFILE** and load data from blob storage toohello table.</span></span>

        CREATE EXTERNAL TABLE IF NOT EXISTS <database name>.<external textfile table name>
        (
            field1 string,
            field2 int,
            ...
            fieldN date
        )
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>'
            lines terminated by '<line separator>' STORED AS TEXTFILE
            LOCATION 'wasb:///<directory in Azure blob>' TBLPROPERTIES("skip.header.line.count"="1");

        LOAD DATA INPATH '<path toohello source file>' INTO TABLE <database name>.<table name>;

<span data-ttu-id="aaf90-218">Bir iç tablosu oluşturma hello ile aynı alan sınırlayıcı ve depolamak hello ile adım 1 ' hello dış tablo olarak aynı şema hello hello ORC biçiminde Hive veri.</span><span class="sxs-lookup"><span data-stu-id="aaf90-218">Create an internal table with hello same schema as hello external table in step 1, with hello same field delimiter, and store hello Hive data in hello ORC format.</span></span>

        CREATE TABLE IF NOT EXISTS <database name>.<ORC table name>
        (
            field1 string,
            field2 int,
            ...
            fieldN date
        )
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>' STORED AS ORC;

<span data-ttu-id="aaf90-219">1. adımda hello dış tablodan veri seçin ve hello ORC tablosuna Ekle</span><span class="sxs-lookup"><span data-stu-id="aaf90-219">Select data from hello external table in step 1 and insert into hello ORC table</span></span>

        INSERT OVERWRITE TABLE <database name>.<ORC table name>
            SELECT * FROM <database name>.<external textfile table name>;

> [!NOTE]
> <span data-ttu-id="aaf90-220">Varsa hello TEXTFILE tablo *&#60; veritabanı adı >. &#60; dış textfile tablo adı >* bölümler, adım 3'te hello içeren `SELECT * FROM <database name>.<external textfile table name>` seçer hello bölüm değişken veri kümesi hello alanında döndürülen komutu.</span><span class="sxs-lookup"><span data-stu-id="aaf90-220">If hello TEXTFILE table *&#60;database name>.&#60;external textfile table name>* has partitions, in STEP 3, hello `SELECT * FROM <database name>.<external textfile table name>` command selects hello partition variable as a field in hello returned data set.</span></span> <span data-ttu-id="aaf90-221">Merhaba ekleme *&#60; veritabanı adı >. &#60; ORC tablo adı >* bu yana başarısız *&#60; veritabanı adı >. &#60; ORC tablo adı >* hello bölüm değişken olarak yok bir Merhaba tablo şemasını alanında.</span><span class="sxs-lookup"><span data-stu-id="aaf90-221">Inserting it into hello *&#60;database name>.&#60;ORC table name>* fails since *&#60;database name>.&#60;ORC table name>* does not have hello partition variable as a field in hello table schema.</span></span> <span data-ttu-id="aaf90-222">Bu durumda, çok eklenen toospecifically select hello alanları toobe gerek*&#60; veritabanı adı >. &#60; ORC tablo adı >* gibi:</span><span class="sxs-lookup"><span data-stu-id="aaf90-222">In this case, you need toospecifically select hello fields toobe inserted too*&#60;database name>.&#60;ORC table name>* as follows:</span></span>
>
>

        INSERT OVERWRITE TABLE <database name>.<ORC table name> PARTITION (<partition variable>=<partition value>)
           SELECT field1, field2, ..., fieldN
           FROM <database name>.<external textfile table name>
           WHERE <partition variable>=<partition value>;

<span data-ttu-id="aaf90-223">Güvenli toodrop hello olan *&#60; dış textfile tablo adı >* zaman sorgu tüm veri sonra aşağıdaki hello kullanarak ekledi içine *&#60; veritabanı adı >. &#60; ORC tablo adı >*:</span><span class="sxs-lookup"><span data-stu-id="aaf90-223">It is safe toodrop hello *&#60;external textfile table name>* when using hello following query after all data has been inserted into *&#60;database name>.&#60;ORC table name>*:</span></span>

        DROP TABLE IF EXISTS <database name>.<external textfile table name>;

<span data-ttu-id="aaf90-224">Bu yordamı tamamladıktan sonra hello ORC biçimi hazır toouse verileri içeren bir tablo olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="aaf90-224">After following this procedure, you should have a table with data in hello ORC format ready toouse.</span></span>  
