---
title: "aaaUse Azure şablonları toocreate Hdınsight ve Data Lake Store | Microsoft Docs"
description: "Azure Resource Manager şablonları toocreate kullanın ve Hdınsight kümeleri Azure Data Lake Store ile kullanma"
services: data-lake-store,hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 8ef8152f-2121-461e-956c-51c55144919d
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/04/2017
ms.author: nitinme
ms.openlocfilehash: eb88a626f2837dcc29295f3f73a91757059c3bb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-hdinsight-cluster-with-data-lake-store-using-azure-resource-manager-template"></a><span data-ttu-id="c13a6-103">Azure Resource Manager şablonunu kullanarak Data Lake Store ile Hdınsight kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="c13a6-103">Create an HDInsight cluster with Data Lake Store using Azure Resource Manager template</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c13a6-104">Portalı kullanma</span><span class="sxs-lookup"><span data-stu-id="c13a6-104">Using Portal</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [<span data-ttu-id="c13a6-105">(Varsayılan depolama için) PowerShell'i kullanma</span><span class="sxs-lookup"><span data-stu-id="c13a6-105">Using PowerShell (for default storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [<span data-ttu-id="c13a6-106">PowerShell kullanarak (için ek depolama alanı)</span><span class="sxs-lookup"><span data-stu-id="c13a6-106">Using PowerShell (for additional storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [<span data-ttu-id="c13a6-107">Kaynak Yöneticisi'ni kullanma</span><span class="sxs-lookup"><span data-stu-id="c13a6-107">Using Resource Manager</span></span>](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

<span data-ttu-id="c13a6-108">Azure Data Lake Store ile toouse Azure PowerShell tooconfigure bir Hdınsight kümesi nasıl öğrenin **ek depolama alanı olarak**.</span><span class="sxs-lookup"><span data-stu-id="c13a6-108">Learn how toouse Azure PowerShell tooconfigure an HDInsight cluster with Azure Data Lake Store, **as additional storage**.</span></span>

<span data-ttu-id="c13a6-109">Desteklenen küme türleri için Data Lake Store bir varsayılan depolama veya ek depolama alanı hesabı olarak kullanılması.</span><span class="sxs-lookup"><span data-stu-id="c13a6-109">For supported cluster types, Data Lake Store be used as an default storage or additional storage account.</span></span> <span data-ttu-id="c13a6-110">Data Lake Store ek depolama alanı olarak kullanıldığında, hello varsayılan depolama hesabı hello kümeleri için Azure Storage Blobları (WASB) çıkarılsın ve hello küme ilgili dosyalar (örneğin, günlükleri, vb.) hello veriler toohello varsayılan depolama yazılmış, bir Data Lake Store hesabında tooprocess depolanabilir istiyor.</span><span class="sxs-lookup"><span data-stu-id="c13a6-110">When Data Lake Store is used as additional storage, hello default storage account for hello clusters will still be Azure Storage Blobs (WASB) and hello cluster-related files (such as logs, etc.) are still written toohello default storage, while hello data that you want tooprocess can be stored in a Data Lake Store account.</span></span> <span data-ttu-id="c13a6-111">Data Lake Store ek depolama alanı hesabı olarak kullanarak performans veya hello özelliği tooread/yazma toohello depolama hello kümeden etkilemez.</span><span class="sxs-lookup"><span data-stu-id="c13a6-111">Using Data Lake Store as an additional storage account does not impact performance or hello ability tooread/write toohello storage from hello cluster.</span></span>

## <a name="using-data-lake-store-for-hdinsight-cluster-storage"></a><span data-ttu-id="c13a6-112">Hdınsight küme depolaması için Data Lake Store kullanma</span><span class="sxs-lookup"><span data-stu-id="c13a6-112">Using Data Lake Store for HDInsight cluster storage</span></span>

<span data-ttu-id="c13a6-113">Hdınsight Data Lake Store ile kullanmak için bazı önemli noktalar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="c13a6-113">Here are some important considerations for using HDInsight with Data Lake Store:</span></span>

* <span data-ttu-id="c13a6-114">Seçenek toocreate Hdınsight kümeleri erişimi olan Hdınsight sürüm 3.5 ve 3.6 tooData Lake deposu varsayılan depolama olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="c13a6-114">Option toocreate HDInsight clusters with access tooData Lake Store as default storage is available for HDInsight version 3.5 and 3.6.</span></span>

* <span data-ttu-id="c13a6-115">Seçenek toocreate Hdınsight kümeleri erişimi olan tooData Lake deposu ek depolama alanı olarak Hdınsight sürüm 3.2, 3.4, 3.5 ve 3.6 için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="c13a6-115">Option toocreate HDInsight clusters with access tooData Lake Store as additional storage is available for HDInsight versions 3.2, 3.4, 3.5, and 3.6.</span></span>

<span data-ttu-id="c13a6-116">Bu makalede, sizi ek depolama alanı olarak Data Lake Store ile Hadoop kümesi sağlayın.</span><span class="sxs-lookup"><span data-stu-id="c13a6-116">In this article, we provision a Hadoop cluster with Data Lake Store as additional storage.</span></span> <span data-ttu-id="c13a6-117">Data Lake Store varsayılan depolama toocreate bir Hadoop nasıl kümesi ile ilgili yönergeler için bkz: [Azure Portal'ı kullanarak Data Lake Store ile bir Hdınsight kümesi oluşturmayı](data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c13a6-117">For instructions on how toocreate a Hadoop cluster with Data Lake Store as default storage, see [Create an HDInsight cluster with Data Lake Store using Azure Portal](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c13a6-118">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="c13a6-118">Prerequisites</span></span>
<span data-ttu-id="c13a6-119">Bu öğreticiye başlamadan önce hello şunlara sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="c13a6-119">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="c13a6-120">**Bir Azure aboneliği**.</span><span class="sxs-lookup"><span data-stu-id="c13a6-120">**An Azure subscription**.</span></span> <span data-ttu-id="c13a6-121">Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c13a6-121">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="c13a6-122">**Azure PowerShell 1.0 veya üstü**.</span><span class="sxs-lookup"><span data-stu-id="c13a6-122">**Azure PowerShell 1.0 or greater**.</span></span> <span data-ttu-id="c13a6-123">Bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c13a6-123">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="c13a6-124">**Azure Active Directory hizmet asıl**.</span><span class="sxs-lookup"><span data-stu-id="c13a6-124">**Azure Active Directory Service Principal**.</span></span> <span data-ttu-id="c13a6-125">Bu öğreticideki adımlardan hakkında yönergeler sağlayan bir hizmet sorumlusu Azure AD'de toocreate.</span><span class="sxs-lookup"><span data-stu-id="c13a6-125">Steps in this tutorial provide instructions on how toocreate a service principal in Azure AD.</span></span> <span data-ttu-id="c13a6-126">Ancak, bir Azure AD yönetici toobe mümkün toocreate bir hizmet sorumlusu olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c13a6-126">However, you must be an Azure AD administrator toobe able toocreate a service principal.</span></span> <span data-ttu-id="c13a6-127">Azure AD Yöneticiyseniz, bu önkoşulu atlayın ve hello eğitici devam edin.</span><span class="sxs-lookup"><span data-stu-id="c13a6-127">If you are an Azure AD administrator, you can skip this prerequisite and proceed with hello tutorial.</span></span>

    <span data-ttu-id="c13a6-128">**Azure AD Yönetici değilseniz**, mümkün tooperform hello adımları gerekli toocreate bir hizmet sorumlusu olmaz.</span><span class="sxs-lookup"><span data-stu-id="c13a6-128">**If you are not an Azure AD administrator**, you will not be able tooperform hello steps required toocreate a service principal.</span></span> <span data-ttu-id="c13a6-129">Data Lake Store ile Hdınsight kümesi oluşturmadan önce böyle bir durumda, Azure AD yöneticinizin önce bir hizmet sorumlusu oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c13a6-129">In such a case, your Azure AD administrator must first create a service principal before you can create an HDInsight cluster with Data Lake Store.</span></span> <span data-ttu-id="c13a6-130">Ayrıca, hello hizmet sorumlusu bir sertifika kullanılarak konusunda açıklandığı gibi oluşturulmalıdır [sertifikayla bir hizmet sorumlusu oluşturma](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span><span class="sxs-lookup"><span data-stu-id="c13a6-130">Also, hello service principal must be created using a certificate, as described at [Create a service principal with certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span></span>

## <a name="create-an-hdinsight-cluster-with-azure-data-lake-store"></a><span data-ttu-id="c13a6-131">Azure Data Lake Store ile Hdınsight kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="c13a6-131">Create an HDInsight cluster with Azure Data Lake Store</span></span>
<span data-ttu-id="c13a6-132">Merhaba Resource Manager şablonu ve hello önkoşulları hello şablonunu kullanarak github'da kullanılabilir [yeni Data Lake Store ile Hdınsight Linux kümesi dağıtma](https://github.com/Azure/azure-quickstart-templates/tree/master/201-hdinsight-datalake-store-azure-storage).</span><span class="sxs-lookup"><span data-stu-id="c13a6-132">hello Resource Manager template, and hello prerequisites for using hello template, are available on GitHub at [Deploy a HDInsight Linux cluster with new Data Lake Store](https://github.com/Azure/azure-quickstart-templates/tree/master/201-hdinsight-datalake-store-azure-storage).</span></span> <span data-ttu-id="c13a6-133">Bu bağlantıyı toocreate Hdınsight kümesi hello ek depolama alanı olarak Azure Data Lake Store ile Merhaba yönergelerini izleyin.</span><span class="sxs-lookup"><span data-stu-id="c13a6-133">Follow hello instructions provided at this link toocreate an HDInsight cluster with Azure Data Lake Store as hello additional storage.</span></span>

<span data-ttu-id="c13a6-134">Yukarıda belirtilen hello bağlantı Hello yönergeleri PowerShell gerektirir.</span><span class="sxs-lookup"><span data-stu-id="c13a6-134">hello instructions at hello link mentioned above require PowerShell.</span></span> <span data-ttu-id="c13a6-135">Bu yönergeler içeren başlamadan önce tooyour Azure hesabı oturum emin olun.</span><span class="sxs-lookup"><span data-stu-id="c13a6-135">Before you start with those instructions, make sure you log in tooyour Azure account.</span></span> <span data-ttu-id="c13a6-136">Masaüstünüzde yeni bir Azure PowerShell penceresi açın ve aşağıdaki kod parçacıkları hello girin.</span><span class="sxs-lookup"><span data-stu-id="c13a6-136">From your desktop, open a new Azure PowerShell window, and enter hello following snippets.</span></span> <span data-ttu-id="c13a6-137">' De, istendiğinde toolog emin yaptığınızda, bir hello Abonelik Yöneticisi/sahibi oturum açın:</span><span class="sxs-lookup"><span data-stu-id="c13a6-137">When prompted toolog in, make sure you log in as one of hello subscription admininistrators/owner:</span></span>

```
# Log in tooyour Azure account
Login-AzureRmAccount

# List all hello subscriptions associated tooyour account
Get-AzureRmSubscription

# Select a subscription
Set-AzureRmContext -SubscriptionId <subscription ID>
```

## <a name="upload-sample-data-toohello-azure-data-lake-store"></a><span data-ttu-id="c13a6-138">Örnek veri toohello Azure Data Lake Store karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="c13a6-138">Upload sample data toohello Azure Data Lake Store</span></span>
<span data-ttu-id="c13a6-139">Merhaba Resource Manager şablonu yeni bir Data Lake Store hesabı oluşturur ve hello Hdınsight küme ile ilişkilendirir.</span><span class="sxs-lookup"><span data-stu-id="c13a6-139">hello Resource Manager template creates a new Data Lake Store account and associates it with hello HDInsight cluster.</span></span> <span data-ttu-id="c13a6-140">Şimdi bazı örnek veri toohello Data Lake Store yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="c13a6-140">You must now upload some sample data toohello Data Lake Store.</span></span> <span data-ttu-id="c13a6-141">Bu veriler, daha sonra hello Data Lake Store verilerine erişmek hello öğretici toorun işlerini bir Hdınsight kümesine ait gerekir.</span><span class="sxs-lookup"><span data-stu-id="c13a6-141">You'll need this data later in hello tutorial toorun jobs from an HDInsight cluster that access data in hello Data Lake Store.</span></span> <span data-ttu-id="c13a6-142">Yönergeler için tooupload verileri, görmek [dosya tooyour Data Lake Store karşıya](data-lake-store-get-started-portal.md#uploaddata).</span><span class="sxs-lookup"><span data-stu-id="c13a6-142">For instructions on how tooupload data, see [Upload a file tooyour Data Lake Store](data-lake-store-get-started-portal.md#uploaddata).</span></span> <span data-ttu-id="c13a6-143">Bazı örnek veri tooupload için arıyorsanız, hello alabilirsiniz **Ambulance Data** hello klasöründen [Azure Data Lake Git deposu](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span><span class="sxs-lookup"><span data-stu-id="c13a6-143">If you are looking for some sample data tooupload, you can get hello **Ambulance Data** folder from hello [Azure Data Lake Git Repository](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span>

## <a name="set-relevant-acls-on-hello-sample-data"></a><span data-ttu-id="c13a6-144">İlgili ACL'leri hello örnek verilere ayarlayın</span><span class="sxs-lookup"><span data-stu-id="c13a6-144">Set relevant ACLs on hello sample data</span></span>
<span data-ttu-id="c13a6-145">karşıya yüklediğiniz hello örnek verileri hello Hdınsight kümeden erişilebilir olduğundan emin toomake, kullanılan tooestablish kimlik hello Hdınsight kümesi ve Data Lake Store arasında hello Azure AD uygulama erişim toohello dosya/klasör olduğunuz olduğundan emin olmalısınız tooaccess çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="c13a6-145">toomake sure hello sample data you upload is accessible from hello HDInsight cluster, you must ensure that hello Azure AD application that is used tooestablish identity between hello HDInsight cluster and Data Lake Store has access toohello file/folder you are trying tooaccess.</span></span> <span data-ttu-id="c13a6-146">toodo bunu hello aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="c13a6-146">toodo this, perform hello following steps.</span></span>

1. <span data-ttu-id="c13a6-147">Merhaba Hdınsight kümesi ile ilişkili Azure AD uygulaması ve hello Data Lake Store Hello adını bulun.</span><span class="sxs-lookup"><span data-stu-id="c13a6-147">Find hello name of hello Azure AD application that is associated with HDInsight cluster and hello Data Lake Store.</span></span> <span data-ttu-id="c13a6-148">Hello adı için tek yönlü toolook hello Resource Manager şablonu kullanılarak oluşturulan tooopen hello Hdınsight küme dikey penceresinde, hello tıklatın **kümeye özgü AAD kimliği** sekmesini tıklatın ve değeri hello Ara **hizmet sorumlusu Görünen ad**.</span><span class="sxs-lookup"><span data-stu-id="c13a6-148">One way toolook for hello name is tooopen hello HDInsight cluster blade that you created using hello Resource Manager template, click hello **Cluster AAD Identity** tab, and look for hello value of **Service Principal Display Name**.</span></span>
2. <span data-ttu-id="c13a6-149">Şimdi, erişim toothis hello dosya/klasör hello Hdınsight kümeden tooaccess istediğiniz Azure AD uygulaması sağlar.</span><span class="sxs-lookup"><span data-stu-id="c13a6-149">Now, provide access toothis Azure AD application on hello file/folder that you want tooaccess from hello HDInsight cluster.</span></span> <span data-ttu-id="c13a6-150">tooset hello sağda ACL'ler hello dosya/klasör Data Lake Store'da görmek [Data Lake Store'da verilerin güvenliğini sağlama](data-lake-store-secure-data.md#filepermissions).</span><span class="sxs-lookup"><span data-stu-id="c13a6-150">tooset hello right ACLs on hello file/folder in Data Lake Store, see [Securing data in Data Lake Store](data-lake-store-secure-data.md#filepermissions).</span></span>

## <a name="run-test-jobs-on-hello-hdinsight-cluster-toouse-hello-data-lake-store"></a><span data-ttu-id="c13a6-151">Merhaba Hdınsight küme toouse hello Data Lake Store üzerinde test işleri çalıştırma</span><span class="sxs-lookup"><span data-stu-id="c13a6-151">Run test jobs on hello HDInsight cluster toouse hello Data Lake Store</span></span>
<span data-ttu-id="c13a6-152">Hdınsight kümesi yapılandırdıktan sonra o hello Hdınsight test işleri hello küme tootest üzerinde çalıştırabilirsiniz küme, Data Lake Store erişebilir.</span><span class="sxs-lookup"><span data-stu-id="c13a6-152">After you have configured an HDInsight cluster, you can run test jobs on hello cluster tootest that hello HDInsight cluster can access Data Lake Store.</span></span> <span data-ttu-id="c13a6-153">toodo bu nedenle, biz önceki tooyour Data Lake Store karşıya hello örnek verileri kullanarak bir tablo oluşturur bir örnek Hive işi çalışır.</span><span class="sxs-lookup"><span data-stu-id="c13a6-153">toodo so, we will run a sample Hive job that creates a table using hello sample data that you uploaded earlier tooyour Data Lake Store.</span></span>

<span data-ttu-id="c13a6-154">Bu bölümde, SSH Hdınsight Linux kümesi ve çalışma hello halinde örnek Hive sorgusu olur.</span><span class="sxs-lookup"><span data-stu-id="c13a6-154">In this section you will SSH into an HDInsight Linux cluster and run hello a sample Hive query.</span></span> <span data-ttu-id="c13a6-155">Windows istemcisi kullanıyorsanız, kullanmanızı öneririz **PuTTY**, hangi adresinden yüklenebilir [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span><span class="sxs-lookup"><span data-stu-id="c13a6-155">If you are using a Windows client, we recommend using **PuTTY**, which can be downloaded from [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>

<span data-ttu-id="c13a6-156">PuTTY kullanma hakkında daha fazla bilgi için bkz: [Windows'dan hdınsight'ta Linux tabanlı Hadoop ile SSH kullanma ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="c13a6-156">For more information on using PuTTY, see [Use SSH with Linux-based Hadoop on HDInsight from Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>

1. <span data-ttu-id="c13a6-157">Bağlandıktan sonra komutu aşağıdaki hello kullanarak hello Hive CLI başlatın:</span><span class="sxs-lookup"><span data-stu-id="c13a6-157">Once connected, start hello Hive CLI by using hello following command:</span></span>

   ```
   hive
   ```
2. <span data-ttu-id="c13a6-158">Merhaba, CLI kullanarak girin deyimleri toocreate adlı yeni bir tablo aşağıdaki hello **taşıtlardan** hello Data Lake Store hello örnek verileri kullanarak:</span><span class="sxs-lookup"><span data-stu-id="c13a6-158">Using hello CLI, enter hello following statements toocreate a new table named **vehicles** by using hello sample data in hello Data Lake Store:</span></span>

   ```
   DROP TABLE vehicles;
   CREATE EXTERNAL TABLE vehicles (str string) LOCATION 'adl://<mydatalakestore>.azuredatalakestore.net:443/';
   SELECT * FROM vehicles LIMIT 10;
   ```

   <span data-ttu-id="c13a6-159">Bir çıkış benzer toohello aşağıdaki görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="c13a6-159">You should see an output similar toohello following:</span></span>

   ```
   1,1,2014-09-14 00:00:03,46.81006,-92.08174,51,S,1
   1,2,2014-09-14 00:00:06,46.81006,-92.08174,13,NE,1
   1,3,2014-09-14 00:00:09,46.81006,-92.08174,48,NE,1
   1,4,2014-09-14 00:00:12,46.81006,-92.08174,30,W,1
   1,5,2014-09-14 00:00:15,46.81006,-92.08174,47,S,1
   1,6,2014-09-14 00:00:18,46.81006,-92.08174,9,S,1
   1,7,2014-09-14 00:00:21,46.81006,-92.08174,53,N,1
   1,8,2014-09-14 00:00:24,46.81006,-92.08174,63,SW,1
   1,9,2014-09-14 00:00:27,46.81006,-92.08174,4,NE,1
   1,10,2014-09-14 00:00:30,46.81006,-92.08174,31,N,1
   ```


## <a name="access-data-lake-store-using-hdfs-commands"></a><span data-ttu-id="c13a6-160">HDFS komutları kullanarak erişim Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="c13a6-160">Access Data Lake Store using HDFS commands</span></span>
<span data-ttu-id="c13a6-161">Merhaba Hdınsight küme toouse Data Lake Store yapılandırdıktan sonra hello HDFS Kabuk komutları tooaccess hello deposu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c13a6-161">Once you have configured hello HDInsight cluster toouse Data Lake Store, you can use hello HDFS shell commands tooaccess hello store.</span></span>

<span data-ttu-id="c13a6-162">Bu bölümde, SSH Hdınsight Linux kümesi ve çalışma hello halinde HDFS komutu olur.</span><span class="sxs-lookup"><span data-stu-id="c13a6-162">In this section you will SSH into an HDInsight Linux cluster and run hello HDFS commands.</span></span> <span data-ttu-id="c13a6-163">Windows istemcisi kullanıyorsanız, kullanmanızı öneririz **PuTTY**, hangi adresinden yüklenebilir [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span><span class="sxs-lookup"><span data-stu-id="c13a6-163">If you are using a Windows client, we recommend using **PuTTY**, which can be downloaded from [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>

<span data-ttu-id="c13a6-164">PuTTY kullanma hakkında daha fazla bilgi için bkz: [Windows'dan hdınsight'ta Linux tabanlı Hadoop ile SSH kullanma ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="c13a6-164">For more information on using PuTTY, see [Use SSH with Linux-based Hadoop on HDInsight from Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>

<span data-ttu-id="c13a6-165">Bağlantı kurulduktan sonra aşağıdaki hello Data Lake Store, HDFS filesystem komutu toolist hello dosyaları hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="c13a6-165">Once connected, use hello following HDFS filesystem command toolist hello files in hello Data Lake Store.</span></span>

```
hdfs dfs -ls adl://<Data Lake Store account name>.azuredatalakestore.net:443/
```

<span data-ttu-id="c13a6-166">Bu, önceki toohello Data Lake Store karşıya hello dosya listelenmelidir.</span><span class="sxs-lookup"><span data-stu-id="c13a6-166">This should list hello file that you uploaded earlier toohello Data Lake Store.</span></span>

```
15/09/17 21:41:15 INFO web.CaboWebHdfsFileSystem: Replacing original urlConnectionFactory with org.apache.hadoop.hdfs.web.URLConnectionFactory@21a728d6
Found 1 items
-rwxrwxrwx   0 NotSupportYet NotSupportYet     671388 2015-09-16 22:16 adl://mydatalakestore.azuredatalakestore.net:443/mynewfolder
```

<span data-ttu-id="c13a6-167">Merhaba de kullanabilirsiniz `hdfs dfs -put` tooupload bazı dosyaları toohello Data Lake Store komutunu ve ardından `hdfs dfs -ls` tooverify hello dosyaları başarıyla karşıya yüklendi.</span><span class="sxs-lookup"><span data-stu-id="c13a6-167">You can also use hello `hdfs dfs -put` command tooupload some files toohello Data Lake Store, and then use `hdfs dfs -ls` tooverify whether hello files were successfully uploaded.</span></span>


## <a name="next-steps"></a><span data-ttu-id="c13a6-168">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c13a6-168">Next steps</span></span>
* [<span data-ttu-id="c13a6-169">Azure Storage Blobları tooData Lake Mağazası'ndan veri kopyalama</span><span class="sxs-lookup"><span data-stu-id="c13a6-169">Copy data from Azure Storage Blobs tooData Lake Store</span></span>](data-lake-store-copy-data-wasb-distcp.md)
