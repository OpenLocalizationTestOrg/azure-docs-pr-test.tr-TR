---
title: "aaaCustomize Hadoop kümeleri Merhaba takım veri bilimi işlemi | Microsoft Docs"
description: "Popüler Python modülleri özel Azure Hdınsight Hadoop kümeleri kullanılabilir."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 0c115dca-2565-4e7a-9536-6002af5c786a
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: hangzh;bradsev
ms.openlocfilehash: e192542dd39f71bccbb5163382b4050d0f12ad95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-azure-hdinsight-hadoop-clusters-for-hello-team-data-science-process"></a><span data-ttu-id="815fa-103">Azure Hdınsight Hadoop kümeleri hello takım veri bilimi işlemi için özelleştirme</span><span class="sxs-lookup"><span data-stu-id="815fa-103">Customize Azure HDInsight Hadoop clusters for hello Team Data Science Process</span></span>
<span data-ttu-id="815fa-104">Merhaba küme bir Hdınsight hizmeti olarak sağlanır, bu makalede nasıl toocustomize bir Hdınsight Hadoop küme 64-bit Anaconda (Python 2.7) yükleyerek her düğümde açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="815fa-104">This article describes how toocustomize an HDInsight Hadoop cluster by installing 64-bit Anaconda (Python 2.7) on each node when hello cluster is provisioned as an HDInsight service.</span></span> <span data-ttu-id="815fa-105">Aynı zamanda, nasıl tooaccess headnode toosubmit özel işleri toohello küme hello gösterir.</span><span class="sxs-lookup"><span data-stu-id="815fa-105">It also shows how tooaccess hello headnode toosubmit custom jobs toohello cluster.</span></span> <span data-ttu-id="815fa-106">Bu özelleştirme Anaconda içinde yer alan birçok popüler Python modülleri yapar, kullanıcı için uygun şekilde kullanılabilir olan tanımlı işlevler (UDF'ler) tooprocess hello kümesindeki Hive kayıtları tasarlanmış.</span><span class="sxs-lookup"><span data-stu-id="815fa-106">This customization makes many popular Python modules, that are included in Anaconda, conveniently available for use in user defined functions (UDFs) that are designed tooprocess Hive records in hello cluster.</span></span> <span data-ttu-id="815fa-107">Bu senaryoda kullanılan hello yordamları hakkında yönergeler için bkz: [nasıl toosubmit Hive sorguları](machine-learning-data-science-move-hive-tables.md#submit).</span><span class="sxs-lookup"><span data-stu-id="815fa-107">For instructions on hello procedures used in this scenario, see [How toosubmit Hive queries](machine-learning-data-science-move-hive-tables.md#submit).</span></span>

<span data-ttu-id="815fa-108">Merhaba aşağıdaki menü bağlantılar hello yukarı tooset çeşitli veri bilimi ortamları hello tarafından nasıl kullanılacağını açıklamaktadır tootopics [takım veri bilimi işlem (TDSP)](data-science-process-overview.md).</span><span class="sxs-lookup"><span data-stu-id="815fa-108">hello following menu links tootopics that describe how tooset up hello various data science environments used by hello [Team Data Science Process (TDSP)](data-science-process-overview.md).</span></span>

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

## <span data-ttu-id="815fa-109"><a name="customize"></a>Azure Hdınsight Hadoop kümesi özelleştirme</span><span class="sxs-lookup"><span data-stu-id="815fa-109"><a name="customize"></a>Customize Azure HDInsight Hadoop Cluster</span></span>
<span data-ttu-id="815fa-110">özelleştirilmiş bir Hdınsight Hadoop kümesi toocreate Başlat çok oturum açarak[**Klasik Azure portalı**](https://manage.windowsazure.com/), tıklatın **yeni** hello sol alt köşesindeki ve veri hizmetleri seçin HDINSİGHT -> -> **özel Oluştur** hello yukarı toobring **küme ayrıntıları** penceresi.</span><span class="sxs-lookup"><span data-stu-id="815fa-110">toocreate a customized HDInsight Hadoop cluster, start by logging on too[**Azure classic portal**](https://manage.windowsazure.com/), click **New** at hello left bottom corner, and then select DATA SERVICES -> HDINSIGHT -> **CUSTOM CREATE** toobring up hello **Cluster Details** window.</span></span> 

![Çalışma alanı oluşturma](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img1.png)

<span data-ttu-id="815fa-112">Yapılandırma sayfasında 1 oluşturulan hello küme toobe Hello adını girin ve diğer alanlar hello için varsayılan değerleri kabul edin.</span><span class="sxs-lookup"><span data-stu-id="815fa-112">Input hello name of hello cluster toobe created on configuration page 1, and accept default values for hello other fields.</span></span> <span data-ttu-id="815fa-113">Merhaba ok toogo toohello sonraki yapılandırma sayfasını tıklatın.</span><span class="sxs-lookup"><span data-stu-id="815fa-113">Click hello arrow toogo toohello next configuration page.</span></span> 

![Çalışma alanı oluşturma](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img1.png)

<span data-ttu-id="815fa-115">Hello sayısı yapılandırma sayfasında 2 giriş **veri DÜĞÜMLERİNİ**seçin hello **bölge/sanal ağ**seçip hello hello boyutlarını **baş düğüm** ve hello **Veri düğümü**.</span><span class="sxs-lookup"><span data-stu-id="815fa-115">On configuration page 2, input hello number of **DATA NODES**, select hello **REGION/VIRTUAL NETWORK**, and select hello sizes of hello **HEAD NODE** and hello **DATA NODE**.</span></span> <span data-ttu-id="815fa-116">Merhaba ok toogo toohello sonraki yapılandırma sayfasını tıklatın.</span><span class="sxs-lookup"><span data-stu-id="815fa-116">Click hello arrow toogo toohello next configuration page.</span></span>

> [!NOTE]
> <span data-ttu-id="815fa-117">Merhaba **bölge/sanal ağ** aynı hello bölge hello Hdınsight Hadoop kümesi için kullanılan toobe geçiyor hello depolama hesabının olarak hello toobe sahiptir.</span><span class="sxs-lookup"><span data-stu-id="815fa-117">hello **REGION/VIRTUAL NETWORK** has toobe hello same as hello region of hello storage account that is going toobe used for hello HDInsight Hadoop cluster.</span></span> <span data-ttu-id="815fa-118">Aksi takdirde hello dördüncü yapılandırma sayfasında hello depolama hesabı hello aşağı açılan listesinde görünmez **hesap adı**.</span><span class="sxs-lookup"><span data-stu-id="815fa-118">Otherwise, in hello fourth configuration page, hello storage account will not appear on hello dropdown list of **ACCOUNT NAME**.</span></span>
> 
> 

![Çalışma alanı oluşturma](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img3.png)

<span data-ttu-id="815fa-120">Yapılandırma sayfasında 3 hello Hdınsight Hadoop kümesi için bir kullanıcı adı ve parola sağlayın.</span><span class="sxs-lookup"><span data-stu-id="815fa-120">On configuration page 3, provide a user name and password for hello HDInsight Hadoop cluster.</span></span> <span data-ttu-id="815fa-121">**Sağlamadığı** select hello *Enter hello Hive/Oozie meta depo*.</span><span class="sxs-lookup"><span data-stu-id="815fa-121">**Do not** select hello *Enter hello Hive/Oozie Metastore*.</span></span> <span data-ttu-id="815fa-122">Merhaba ok toogo toohello sonraki yapılandırma sayfası'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="815fa-122">Then, click hello arrow toogo toohello next configuration page.</span></span> 

![Çalışma alanı oluşturma](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img4.png)

<span data-ttu-id="815fa-124">Yapılandırma sayfasında 4 hello depolama hesabı adı, hello varsayılan kapsayıcı hello Hdınsight Hadoop kümesi belirtin.</span><span class="sxs-lookup"><span data-stu-id="815fa-124">On configuration page 4, specify hello storage account name, hello default container of hello HDInsight Hadoop cluster.</span></span> <span data-ttu-id="815fa-125">Seçerseniz *oluşturma varsayılan kapsayıcı* hello içinde **varsayılan KAPSAYICI** açılır listesi, bir kapsayıcı hello ile aynı adı hello küme oluşturulacak şekilde.</span><span class="sxs-lookup"><span data-stu-id="815fa-125">If you select *Create default container* in hello **DEFAULT CONTAINER** dropdown list, a container with hello same name as hello cluster will be created.</span></span> <span data-ttu-id="815fa-126">Merhaba ok toogo toohello son yapılandırma sayfasını tıklatın.</span><span class="sxs-lookup"><span data-stu-id="815fa-126">Click hello arrow toogo toohello last configuration page.</span></span>

![Çalışma alanı oluşturma](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img5.png)

<span data-ttu-id="815fa-128">Merhaba son üzerinde **betik eylemleri** yapılandırma sayfasında, tıklatın **betik eylemi eklemek** düğmesine tıklayın ve değerleri aşağıdaki hello ile Merhaba metin alanları doldurun.</span><span class="sxs-lookup"><span data-stu-id="815fa-128">On hello final **Script Actions** configuration page, click **add script action** button, and fill hello text fields with hello following values.</span></span>

* <span data-ttu-id="815fa-129">**AD** -bu komut dosyası eylemin hello adı olarak herhangi bir dize</span><span class="sxs-lookup"><span data-stu-id="815fa-129">**NAME** - any string as hello name of this script action</span></span>
* <span data-ttu-id="815fa-130">**DÜĞÜM türü** - seçin **tüm düğümler**</span><span class="sxs-lookup"><span data-stu-id="815fa-130">**NODE TYPE** - select **All nodes**</span></span>
* <span data-ttu-id="815fa-131">**BETİK URI'si** - *http://getgoing.blob.core.windows.net/publicscripts/Azure_HDI_Setup_Windows.ps1*</span><span class="sxs-lookup"><span data-stu-id="815fa-131">**SCRIPT URI** - *http://getgoing.blob.core.windows.net/publicscripts/Azure_HDI_Setup_Windows.ps1*</span></span> 
  * <span data-ttu-id="815fa-132">*publicscripts* hello depolama hesabındaki ortak bir kapsayıcı</span><span class="sxs-lookup"><span data-stu-id="815fa-132">*publicscripts* is a public container in hello storage account</span></span> 
  * <span data-ttu-id="815fa-133">*getgoing* Azure'da tooshare PowerShell komut dosyaları toofacilitate kullanıcıların çalışmalarını kullanırız</span><span class="sxs-lookup"><span data-stu-id="815fa-133">*getgoing* we use tooshare PowerShell script files toofacilitate users' work in Azure</span></span>
* <span data-ttu-id="815fa-134">**PARAMETRELERİ** -(boş bırakın)</span><span class="sxs-lookup"><span data-stu-id="815fa-134">**PARAMETERS** - (leave blank)</span></span>

<span data-ttu-id="815fa-135">Son olarak, özelleştirilmiş hello Hdınsight Hadoop küme hello onay işareti toostart hello oluşturma'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="815fa-135">Finally, click hello check mark toostart hello creation of hello customized HDInsight Hadoop cluster.</span></span> 

![Çalışma alanı oluşturma](./media/machine-learning-data-science-customize-hadoop-cluster/script-actions.png)

## <span data-ttu-id="815fa-137"><a name="headnode"></a>Erişim hello Hadoop kümesi, baş düğümü</span><span class="sxs-lookup"><span data-stu-id="815fa-137"><a name="headnode"></a> Access hello Head Node of Hadoop Cluster</span></span>
<span data-ttu-id="815fa-138">RDP hello Hadoop küme baş düğümüne hello erişmeden önce uzaktan erişim toohello Hadoop kümesi Azure etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="815fa-138">You must enable remote access toohello Hadoop cluster in Azure before you can access hello head node of hello Hadoop cluster through RDP.</span></span> 

1. <span data-ttu-id="815fa-139">İçinde toohello oturum [ **Klasik Azure portalı**](https://manage.windowsazure.com/)seçin **Hdınsight** hello sol tarafta, Hadoop kümesi hello kümeleri listesinden seçin, hello  **Yapılandırma** sekmesini ve sonra hello **etkinleştirmek uzak** hello sayfanın hello simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="815fa-139">Log in toohello [**Azure classic portal**](https://manage.windowsazure.com/), select **HDInsight** on hello left, select your Hadoop cluster from hello list of clusters, click hello **CONFIGURATION** tab, and then click hello **ENABLE REMOTE** icon at hello bottom of hello page.</span></span>
   
    ![Çalışma alanı oluşturma](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-1.png)
2. <span data-ttu-id="815fa-141">Merhaba, **Uzak Masaüstü'nü yapılandırmak** penceresinde hello kullanıcı adı ve parola alanlarına girin ve Uzaktan erişim hello sona erme tarihini seçin.</span><span class="sxs-lookup"><span data-stu-id="815fa-141">In hello **Configure Remote Desktop** window, enter hello USER NAME and PASSWORD fields, and select hello expiration date for remote access.</span></span> <span data-ttu-id="815fa-142">Merhaba onay işareti tooenable hello uzaktan erişim toohello baş düğümüne hello Hadoop kümesi'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="815fa-142">Then click hello check mark tooenable hello remote access toohello head node of hello Hadoop cluster.</span></span>
   
    ![Çalışma alanı oluşturma](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-2.png)

> [!NOTE]
> <span data-ttu-id="815fa-144">Merhaba kullanıcı adı ve parola hello uzaktan erişim için hello kullanıcı adı ve hello Hadoop küme oluştururken kullandığınız parolayı olup olmadığı.</span><span class="sxs-lookup"><span data-stu-id="815fa-144">hello user name and password for hello remote access are not hello user name and password that you use when you created hello Hadoop cluster.</span></span> <span data-ttu-id="815fa-145">Bu kimlik bilgilerini ayrı bir kümesidir.</span><span class="sxs-lookup"><span data-stu-id="815fa-145">This is a separate set of credentials.</span></span> <span data-ttu-id="815fa-146">Ayrıca, hello sona erme tarihi hello uzaktan erişim 7 gün içinde hello geçerli tarih toobe sahiptir.</span><span class="sxs-lookup"><span data-stu-id="815fa-146">Also, hello expiration date of hello remote access has toobe within 7 days from hello current date.</span></span>
> 
> 

<span data-ttu-id="815fa-147">Uzaktan erişim etkinleştirildikten sonra tıklatın **BAĞLAN** hello sayfa tooremote hello baş düğüme hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="815fa-147">After remote access is enabled, click **CONNECT** at hello bottom of hello page tooremote into hello head node.</span></span> <span data-ttu-id="815fa-148">Daha önce belirtilen hello uzaktan erişim kullanıcıdan hello kimlik bilgileri girerek toohello baş hello Hadoop küme düğümünde oturum.</span><span class="sxs-lookup"><span data-stu-id="815fa-148">You log on toohello head node of hello Hadoop cluster by entering hello credentials for hello remote access user that you specified earlier.</span></span>

![Çalışma alanı oluşturma](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-3.png)

<span data-ttu-id="815fa-150">Merhaba analytics işlem Gelişmiş hello sonraki adımlarda hello eşlenen [takım veri bilimi işlem (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) ve Hdınsight'a, veri taşıma sonra işleyen ve onu var. hello verilerden öğrenmeyi hazırlığı örnek adımlar içerebilir Azure Machine Learning ile.</span><span class="sxs-lookup"><span data-stu-id="815fa-150">hello next steps in hello advanced analytics process are mapped in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) and may include steps that move data into HDInsight, then process and sample it there in preparation for learning from hello data with Azure Machine Learning.</span></span>

<span data-ttu-id="815fa-151">Bkz: [nasıl toosubmit Hive sorguları](machine-learning-data-science-move-hive-tables.md#submit) nasıl tooaccess Anaconda içinde kullanılan tooprocess olan kullanıcı tanımlı işlevler (UDF'ler) içinde hello kümenin baş düğümünden hello dahil edilen Python modülleri hello hakkında yönergeler için saklanan kayıtlarını yığını Merhaba kümesinde.</span><span class="sxs-lookup"><span data-stu-id="815fa-151">See [How toosubmit Hive queries](machine-learning-data-science-move-hive-tables.md#submit) for instructions on how tooaccess hello Python modules that are included in Anaconda from hello head node of hello cluster in user-defined functions (UDFs) that are used tooprocess Hive records stored in hello cluster.</span></span>

