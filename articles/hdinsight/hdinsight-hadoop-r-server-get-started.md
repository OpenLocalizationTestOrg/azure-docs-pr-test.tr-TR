---
title: "hdınsight'ta - Azure R Server aaaGet Başlarken | Microsoft Docs"
description: "Merhaba kümesinde bir R betiği göndermek ve nasıl toocreate bir Apache Spark R Server içeren Hdınsight kümesinde öğrenin."
services: HDInsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: b5e111f3-c029-436c-ba22-c54a4a3016e3
ms.service: HDInsight
ms.custom: hdinsightactive
ms.devlang: R
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 08/14/2017
ms.author: bradsev
ms.openlocfilehash: f7e418bbac48eee080a4b4cfbb33e246324ea5c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-using-r-server-on-hdinsight"></a><span data-ttu-id="13f6b-103">HDInsight üzerinde R Server kullanmaya başlayın</span><span class="sxs-lookup"><span data-stu-id="13f6b-103">Get started using R Server on HDInsight</span></span>

<span data-ttu-id="13f6b-104">Hdınsight Hdınsight kümenize tümleşik bir R Server seçeneği toobe içerir.</span><span class="sxs-lookup"><span data-stu-id="13f6b-104">HDInsight includes an R Server option toobe integrated into your HDInsight cluster.</span></span> <span data-ttu-id="13f6b-105">Bu seçenek R betiklerini toouse Spark ve MapReduce dağıtılmış toorun hesaplamalar sağlar.</span><span class="sxs-lookup"><span data-stu-id="13f6b-105">This option allows R scripts toouse Spark and MapReduce toorun distributed computations.</span></span> <span data-ttu-id="13f6b-106">Bu belgede nasıl toocreate Hdınsight kümesi ve için Spark kullanarak gösteren Çalıştır bir R betiği bir R Server'a R hesaplamaları dağıtılmış öğrenin.</span><span class="sxs-lookup"><span data-stu-id="13f6b-106">In this document, you learn how toocreate an R Server on HDInsight cluster and then run an R script that demonstrates using Spark for distributed R computations.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="13f6b-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="13f6b-107">Prerequisites</span></span>

* <span data-ttu-id="13f6b-108">**Bir Azure aboneliği**: Bu öğreticiye başlamadan önce bir Azure aboneliğinizin olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="13f6b-108">**An Azure subscription**: Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="13f6b-109">Git toohello makale [alma Microsoft Azure ücretsiz deneme sürümü](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="13f6b-109">Go toohello article [Get Microsoft Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/) for more information.</span></span>
* <span data-ttu-id="13f6b-110">**Bir güvenli Kabuk (SSH) istemcisi**: bir SSH istemcisi kullanılır tooremotely toohello Hdınsight kümesine bağlanın ve doğrudan hello kümede komutları çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="13f6b-110">**A Secure Shell (SSH) client**: An SSH client is used tooremotely connect toohello HDInsight cluster and run commands directly on hello cluster.</span></span> <span data-ttu-id="13f6b-111">Daha fazla bilgi için bkz. [HDInsight ile SSH kullanma.](hdinsight-hadoop-linux-use-ssh-unix.md)</span><span class="sxs-lookup"><span data-stu-id="13f6b-111">For more information, see [Use SSH with HDInsight.](hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>
* <span data-ttu-id="13f6b-112">**SSH anahtarları (isteğe bağlı)**: hello SSH kullanılan hesap tooconnect toohello küme bir parola veya ortak anahtar kullanılarak güvenli hale getirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="13f6b-112">**SSH keys (optional)**: You can secure hello SSH account used tooconnect toohello cluster using either a password or a public key.</span></span> <span data-ttu-id="13f6b-113">Bir parola kullanarak kolaydır ve bir genel/özel anahtar çifti toocreate gerek kalmadan, tooget başlatılan sağlar.</span><span class="sxs-lookup"><span data-stu-id="13f6b-113">Using a password is easier, and allows you tooget started without having toocreate a public/private key pair.</span></span> <span data-ttu-id="13f6b-114">Ancak, bir anahtar kullanılması daha güvenlidir.</span><span class="sxs-lookup"><span data-stu-id="13f6b-114">However, using a key is more secure.</span></span>

> [!NOTE]
> <span data-ttu-id="13f6b-115">Bu belgedeki Hello adımlar bir parola kullandığınızı varsayar.</span><span class="sxs-lookup"><span data-stu-id="13f6b-115">hello steps in this document assume that you are using a password.</span></span>


## <a name="automated-cluster-creation"></a><span data-ttu-id="13f6b-116">Otomatik küme oluşturma</span><span class="sxs-lookup"><span data-stu-id="13f6b-116">Automated cluster creation</span></span>

<span data-ttu-id="13f6b-117">Azure Resource Manager şablonları, hello SDK ve aynı zamanda PowerShell kullanarak, Hdınsight R sunucularını hello oluşturulmasını otomatik hale getirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="13f6b-117">You can automate hello creation of HDInsight R Servers using Azure Resource Manager templates, hello SDK, and also PowerShell.</span></span>

* <span data-ttu-id="13f6b-118">bir Azure kaynak yönetimi şablonu kullanarak bir R Server toocreate bkz [R server Hdınsight kümesi dağıtma](https://azure.microsoft.com/resources/templates/101-hdinsight-rserver/).</span><span class="sxs-lookup"><span data-stu-id="13f6b-118">toocreate an R Server using an Azure Resource Management template, see [Deploy an R server HDInsight cluster](https://azure.microsoft.com/resources/templates/101-hdinsight-rserver/).</span></span>
* <span data-ttu-id="13f6b-119">R Server hello .NET SDK kullanarak bir toocreate bakın [hello .NET SDK kullanarak Hdınsight'ta Linux tabanlı kümelerde oluşturma.](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="13f6b-119">toocreate an R Server using hello .NET SDK, see [create Linux-based clusters in HDInsight using hello .NET SDK.](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span></span>
* <span data-ttu-id="13f6b-120">R Server toodeploy powershell kullanarak hello makaleye bakın üzerinde [PowerShell ile hdınsight'ta R Server oluşturma](hdinsight-hadoop-create-linux-clusters-azure-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="13f6b-120">toodeploy R Server using powershell, see hello article on [creating an R Server on HDInsight with PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md).</span></span>


<a name="create-hdi-custer-with-aure-portal"></a>
## <a name="create-hello-cluster-using-hello-azure-portal"></a><span data-ttu-id="13f6b-121">Hello Azure portal kullanarak hello kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="13f6b-121">Create hello cluster using hello Azure portal</span></span>

1. <span data-ttu-id="13f6b-122">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="13f6b-122">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="13f6b-123">**YENİ** -> **Zeka + Analiz**, -> **HDInsight** seçeneklerini belirtin.</span><span class="sxs-lookup"><span data-stu-id="13f6b-123">Select **NEW** -> **Intelligence + Analytics**, -> **HDInsight**.</span></span>

    ![Yeni küme oluşturma görüntüsü](./media/hdinsight-hadoop-r-server-get-started/newcluster.png)

3. <span data-ttu-id="13f6b-125">Merhaba, **hızlı Oluştur** deneyimi, hello hello küme adı **küme adı** alan.</span><span class="sxs-lookup"><span data-stu-id="13f6b-125">In hello **Quick create** experience, enter a name for hello cluster in hello **Cluster Name** field.</span></span> <span data-ttu-id="13f6b-126">Birden çok Azure aboneliğiniz varsa, hello kullan **abonelik** toouse istediğiniz girişi tooselect hello biri.</span><span class="sxs-lookup"><span data-stu-id="13f6b-126">If you have multiple Azure subscriptions, use hello **Subscription** entry tooselect hello one you want toouse.</span></span>

    ![Küme adı ve abonelik seçimleri](./media/hdinsight-hadoop-r-server-get-started/clustername.png)

4. <span data-ttu-id="13f6b-128">Seçin **küme türü** tooopen hello **küme yapılandırması** dikey.</span><span class="sxs-lookup"><span data-stu-id="13f6b-128">Select **Cluster type** tooopen hello **Cluster configuration** blade.</span></span> <span data-ttu-id="13f6b-129">Merhaba üzerinde **küme yapılandırması** dikey penceresinde, aşağıdaki seçenekleri şu select hello:</span><span class="sxs-lookup"><span data-stu-id="13f6b-129">On hello **Cluster Configuration** blade, select hello following options:</span></span>

    * <span data-ttu-id="13f6b-130">**Küme Türü**: R Server</span><span class="sxs-lookup"><span data-stu-id="13f6b-130">**Cluster Type**: R Server</span></span>
    * <span data-ttu-id="13f6b-131">**Sürüm**: R Server tooinstall hello kümede select hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="13f6b-131">**Version**: select hello version of R Server tooinstall on hello cluster.</span></span> <span data-ttu-id="13f6b-132">şu anda kullanılabilir Hello sürüm ***R Server 9.1 (HDI 3.6)***.</span><span class="sxs-lookup"><span data-stu-id="13f6b-132">hello version currently available is ***R Server 9.1 (HDI 3.6)***.</span></span> <span data-ttu-id="13f6b-133">Sürüm Notları hello kullanılabilir R Server sürümleri için kullanılabilir [burada](https://msdn.microsoft.com/microsoft-r/notes/r-server-notes).</span><span class="sxs-lookup"><span data-stu-id="13f6b-133">Release notes for hello available versions of R Server are available [here](https://msdn.microsoft.com/microsoft-r/notes/r-server-notes).</span></span>
    * <span data-ttu-id="13f6b-134">**R Server için R Studio community edition**: Bu tarayıcı tabanlı IDE hello edge düğüm üzerinde varsayılan olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="13f6b-134">**R Studio community edition for R Server**: this browser-based IDE is installed by default on hello edge node.</span></span> <span data-ttu-id="13f6b-135">Toonot tercih ederseniz yüklemediyseniz, ardından hello onay kutusunun işaretini kaldırın.</span><span class="sxs-lookup"><span data-stu-id="13f6b-135">If you would prefer toonot have it installed, then uncheck hello check box.</span></span> <span data-ttu-id="13f6b-136">Toohave seçerseniz yüklü, bir kez oluşturulduğunda Rstudio'dan sunucu oturum açma kümeniz için bir portal uygulaması dikey penceresinde bulunur hello erişmek için hello URL.</span><span class="sxs-lookup"><span data-stu-id="13f6b-136">If you choose toohave it installed, hello URL for accessing hello RStudio Server login is found on a portal application blade for your cluster once it’s been created.</span></span>
    * <span data-ttu-id="13f6b-137">Bırakın hello diğer seçenekleri hello varsayılan değerlerinde ve hello kullan **seçin** düğme toosave hello küme türü.</span><span class="sxs-lookup"><span data-stu-id="13f6b-137">Leave hello other options at hello default values and use hello **Select** button toosave hello cluster type.</span></span>

        ![Küme türü dikey penceresi ekran görüntüsü](./media/hdinsight-hadoop-r-server-get-started/clustertypeconfig.png)

5. <span data-ttu-id="13f6b-139">Bir **Küme oturum açma kullanıcı adı** ve **Küme oturum açma parolası** girin.</span><span class="sxs-lookup"><span data-stu-id="13f6b-139">Enter a **Cluster login username** and **Cluster login password**.</span></span>

    <span data-ttu-id="13f6b-140">Bir **SSH Kullanıcı Adı** belirtin.</span><span class="sxs-lookup"><span data-stu-id="13f6b-140">Specify an **SSH Username**.</span></span> <span data-ttu-id="13f6b-141">SSH kullanılan tooremotely Bağlan toohello küme kullanarak bir **güvenli Kabuk (SSH)** istemci.</span><span class="sxs-lookup"><span data-stu-id="13f6b-141">SSH is used tooremotely connect toohello cluster using a **Secure Shell (SSH)** client.</span></span> <span data-ttu-id="13f6b-142">Merhaba SSH kullanıcı ya da, bu iletişim kutusunda veya (içinde Merhaba yapılandırma sekmesi hello küme için) hello Küme oluşturulduktan sonra da belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="13f6b-142">You can either specify hello SSH user in this dialog or after hello cluster has been created (in hello Configuration tab for hello cluster).</span></span> <span data-ttu-id="13f6b-143">R sunucusudur yapılandırılmış tooexpect bir **SSH kullanıcı adı** "remoteuser" olarak.</span><span class="sxs-lookup"><span data-stu-id="13f6b-143">R Server is configured tooexpect an **SSH username** of “remoteuser”.</span></span>  <span data-ttu-id="13f6b-144">**Farklı bir kullanıcı adı kullanırsanız, hello Küme oluşturulduktan sonra ek bir adım gerçekleştirmeniz gerekir.**</span><span class="sxs-lookup"><span data-stu-id="13f6b-144">**If you use a different username, you must perform an additional step after hello cluster is created.**</span></span>

    <span data-ttu-id="13f6b-145">İçin işaretli bırakın hello kutusunda **küme oturum açma aynı parolayı kullanın** toouse **parola** hello kimlik doğrulaması türü olarak bir ortak anahtar kullanımını tercih sürece.</span><span class="sxs-lookup"><span data-stu-id="13f6b-145">Leave hello box checked for **Use same password as cluster login** toouse **PASSWORD** as hello authentication type unless you prefer use of a public key.</span></span>  <span data-ttu-id="13f6b-146">Örneğin, RTVS, Rstudio'dan veya başka bir masaüstü IDE olarak uzak istemciye aracılığıyla hello kümede ortak/özel anahtar çifti tooaccess R Server gerekir.</span><span class="sxs-lookup"><span data-stu-id="13f6b-146">You need a public/private key pair tooaccess R Server on hello cluster via a remote client as, for example, RTVS, RStudio or another desktop IDE.</span></span> <span data-ttu-id="13f6b-147">Merhaba Rstudio'dan Server community edition yüklerseniz, toochoose bir SSH parolası gerekir.</span><span class="sxs-lookup"><span data-stu-id="13f6b-147">If you install hello RStudio Server community edition, you need toochoose an SSH password.</span></span>     

    <span data-ttu-id="13f6b-148">toocreate ve kullanım bir genel/özel anahtar çifti işaretini **küme oturum açma aynı parolayı kullanın** ve ardından **ortak anahtar** ve aşağıdaki gibi ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="13f6b-148">toocreate and use a public/private key pair, uncheck **Use same password as cluster login** and then select **PUBLIC KEY** and proceed as follows.</span></span> <span data-ttu-id="13f6b-149">Bu yönergelerde, ssh-keygen veya eşdeğeri ile birlikte Cygwin'in yüklü olduğu varsayılır.</span><span class="sxs-lookup"><span data-stu-id="13f6b-149">These instructions assume that you have Cygwin with ssh-keygen or an equivalent installed.</span></span>

    * <span data-ttu-id="13f6b-150">Dizüstü bilgisayarınızda hello komut isteminden bir genel/özel anahtar çifti oluşturur:</span><span class="sxs-lookup"><span data-stu-id="13f6b-150">Generate a public/private key pair from hello command prompt on your laptop:</span></span>

        <span data-ttu-id="13f6b-151">ssh-keygen -t rsa -b 2048</span><span class="sxs-lookup"><span data-stu-id="13f6b-151">ssh-keygen -t rsa -b 2048</span></span>

    * <span data-ttu-id="13f6b-152">Merhaba komut istemi tooname bir anahtar dosyası izleyin ve sonra ek güvenlik için bir parola girin.</span><span class="sxs-lookup"><span data-stu-id="13f6b-152">Follow hello prompt tooname a key file and then enter a passphrase for added security.</span></span> <span data-ttu-id="13f6b-153">Ekranınızın hello görüntü aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="13f6b-153">Your screen should look something like hello following image:</span></span>

        ![Windows'da SSH cmd satırı](./media/hdinsight-hadoop-r-server-get-started/sshcmdline.png)

    * <span data-ttu-id="13f6b-155">Bu komut, özel bir anahtar dosyası ve hello ad < özel anahtarı dosyaadı > .pub, örneğin furiosa ve furiosa.pub altında ortak bir anahtar dosyası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="13f6b-155">This command creates a private key file and a public key file under hello name <private-key-filename>.pub, for example furiosa and furiosa.pub.</span></span>

        ![SSH dir](./media/hdinsight-hadoop-r-server-get-started/dir.png)

    * <span data-ttu-id="13f6b-157">Merhaba ortak anahtar dosyası (&#42;. belirtin HDI atama ve kimlik bilgilerinin küme kaynak grubu ve bölge ve select onaylamadan pub) **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="13f6b-157">Then specify hello public key file (&#42;.pub) when assigning HDI cluster credentials and finally confirm your resource group and region and select **Next**.</span></span>

        ![Kimlik Bilgileri dikey penceresi](./media/hdinsight-hadoop-r-server-get-started/publickeyfile.png)  

   * <span data-ttu-id="13f6b-159">Dizüstü bilgisayarınızda hello özel keyfile üzerindeki izinleri değiştirin:</span><span class="sxs-lookup"><span data-stu-id="13f6b-159">Change permissions on hello private keyfile on your laptop:</span></span>

        <span data-ttu-id="13f6b-160">chmod 600 <private-key-filename></span><span class="sxs-lookup"><span data-stu-id="13f6b-160">chmod 600 <private-key-filename></span></span>

   * <span data-ttu-id="13f6b-161">Merhaba özel anahtar dosyası SSH ile uzaktan oturum açma için kullanın:</span><span class="sxs-lookup"><span data-stu-id="13f6b-161">Use hello private key file with SSH for remote login:</span></span>

        <span data-ttu-id="13f6b-162">ssh –i <private-key-filename> remoteuser@<hostname public ip></span><span class="sxs-lookup"><span data-stu-id="13f6b-162">ssh –i <private-key-filename> remoteuser@<hostname public ip></span></span>

      <span data-ttu-id="13f6b-163">Ya da bölümü hello tanımı, Hadoop Spark olarak bağlamı için R Server hello istemcide işlem.</span><span class="sxs-lookup"><span data-stu-id="13f6b-163">Or, as part hello definition of your Hadoop Spark compute context for R Server on hello client.</span></span> <span data-ttu-id="13f6b-164">Merhaba bkz **kullanarak Microsoft R Server Hadoop istemcisi olarak** içinde alt bölüm [bir işlem bağlamı için Spark oluşturma](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started#creating-a-compute-context-for-spark).</span><span class="sxs-lookup"><span data-stu-id="13f6b-164">See hello **Using Microsoft R Server as a Hadoop Client** subsection in [Create a Compute Context for Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started#creating-a-compute-context-for-spark).</span></span>

6. <span data-ttu-id="13f6b-165">Merhaba hızlı Oluştur toohello geçişleri **depolama** hello birincil konumunu hello için kullanılan ayarları toobe HDFS dosya sistemi hello küme tarafından kullanılan dikey tooselect hello depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="13f6b-165">hello quick create transitions you toohello **Storage** blade tooselect hello storage account settings toobe used for hello primary location of hello HDFS file system used by hello cluster.</span></span> <span data-ttu-id="13f6b-166">Yeni veya mevcut bir Azure Depolama hesabını ya da mevcut bir Data Lake Storage hesabını seçin.</span><span class="sxs-lookup"><span data-stu-id="13f6b-166">Select either a new or existing Azure Storage account or an existing Data Lake Storage account.</span></span>

    - <span data-ttu-id="13f6b-167">Bir Azure depolama hesabı seçin, mevcut bir depolama hesabını seçerek seçilirse **bir depolama hesabı seçin** ve hello ilgili hesabı seçme.</span><span class="sxs-lookup"><span data-stu-id="13f6b-167">If you select an Azure Storage account, an existing storage account is selected by choosing **Select a storage account** and then selecting hello relevant account.</span></span> <span data-ttu-id="13f6b-168">Hello kullanarak yeni bir hesap oluşturma **Yeni Oluştur** hello bağlantıyı **bir depolama hesabı seçin** bölümü.</span><span class="sxs-lookup"><span data-stu-id="13f6b-168">Create a new account using hello **Create New** link in hello **Select a storage account** section.</span></span>

      > [!NOTE]
      > <span data-ttu-id="13f6b-169">Seçerseniz **yeni** hello yeni depolama hesabı için bir ad girmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="13f6b-169">If you select **New** you must enter a name for hello new storage account.</span></span> <span data-ttu-id="13f6b-170">Merhaba adı kabul edilirse yeşil bir onay işareti görünür.</span><span class="sxs-lookup"><span data-stu-id="13f6b-170">A green check appears if hello name is accepted.</span></span>

      <span data-ttu-id="13f6b-171">Merhaba **varsayılan kapsayıcı** Varsayılanları toohello hello kümenin adını.</span><span class="sxs-lookup"><span data-stu-id="13f6b-171">hello **Default Container** defaults toohello name of hello cluster.</span></span> <span data-ttu-id="13f6b-172">Bu varsayılan hello değeri bırakın.</span><span class="sxs-lookup"><span data-stu-id="13f6b-172">Leave this default as hello value.</span></span>

      <span data-ttu-id="13f6b-173">Yeni bir depolama hesabı seçeneği seçildiyse, bir komut istemi tooselect **konumu** olan tooselect hangi bölge toocreate hello depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="13f6b-173">If a new storage account option was selected a prompt tooselect **Location** is given tooselect which region toocreate hello storage account.</span></span>  

         ![Veri kaynağı dikey penceresi](./media/hdinsight-getting-started-with-r/datastore.png)  

      > [!IMPORTANT]
      > <span data-ttu-id="13f6b-175">Merhaba varsayılan veri kaynağı için başlangıç konumu seçerek hello Hdınsight kümesi hello konumunu ayarlar.</span><span class="sxs-lookup"><span data-stu-id="13f6b-175">Selecting hello location for hello default data source  also sets hello location of hello HDInsight cluster.</span></span> <span data-ttu-id="13f6b-176">Merhaba küme ve varsayılan veri kaynağı hello olmalıdır aynı bölgede.</span><span class="sxs-lookup"><span data-stu-id="13f6b-176">hello cluster and default data source must be in hello same region.</span></span>

    - <span data-ttu-id="13f6b-177">Toouse mevcut bir Data Lake Store istiyorsanız, seçip hello ADLS depolama hesabı toouse ve hello küme eklemek *Ekle* kimlik tooyour küme tooallow erişim toohello deposu.</span><span class="sxs-lookup"><span data-stu-id="13f6b-177">If you want toouse an existing Data Lake Store, then select hello ADLS storage account toouse and add hello cluster *ADD* identity tooyour cluster tooallow access toohello store.</span></span> <span data-ttu-id="13f6b-178">Bu işlem hakkında daha fazla bilgi için [Azure portalı kullanarak Data Lake Store ile HDInsight kümesi oluşturma](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-hdinsight-hadoop-use-portal) bölümünü inceleyin.</span><span class="sxs-lookup"><span data-stu-id="13f6b-178">For more information on this process, see [Creating HDInsight cluster with Data Lake Store using Azure portal](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-hdinsight-hadoop-use-portal).</span></span>

    <span data-ttu-id="13f6b-179">Kullanım hello **seçin** düğmesini toosave hello veri kaynağı yapılandırması.</span><span class="sxs-lookup"><span data-stu-id="13f6b-179">Use hello **Select** button toosave hello data source configuration.</span></span>


7. <span data-ttu-id="13f6b-180">Merhaba **Özet** dikey penceresinde tüm ayarlarınızı sonra toovalidate görüntüler.</span><span class="sxs-lookup"><span data-stu-id="13f6b-180">hello **Summary** blade then displays toovalidate all your settings.</span></span> <span data-ttu-id="13f6b-181">Burada değiştirebilirsiniz, **küme boyutu** toomodify hello Kümenizdeki sunucuların sayısını ve ayrıca herhangi belirtmek **betik eylemleri** toorun istiyor.</span><span class="sxs-lookup"><span data-stu-id="13f6b-181">Here you can change your **Cluster size** toomodify hello number of servers in your cluster and also specify any **Script actions** you want toorun.</span></span> <span data-ttu-id="13f6b-182">Daha büyük bir küme gerekir bilmiyorsanız, çalışan düğüm sayısı hello hello varsayılan olarak bırakın `4`.</span><span class="sxs-lookup"><span data-stu-id="13f6b-182">Unless you know that you need a larger cluster, leave hello number of worker nodes at hello default of `4`.</span></span> <span data-ttu-id="13f6b-183">Merhaba hello küme maliyetini hello Dikey içinde gösterilen tahmin.</span><span class="sxs-lookup"><span data-stu-id="13f6b-183">hello estimated cost of hello cluster is shown within hello blade.</span></span>

    ![küme özeti](./media/hdinsight-hadoop-r-server-get-started/clustersummary.png)

   > [!NOTE]
   > <span data-ttu-id="13f6b-185">Gerekirse, kümenizi hello Portal aracılığıyla daha sonra yeniden boyutlandırabilirsiniz (**küme** -> **ayarları** -> **ölçekte küme**) tooincrease veya Merhaba çalışan düğümü sayısını azaltın.</span><span class="sxs-lookup"><span data-stu-id="13f6b-185">If needed, you can resize your cluster later through hello Portal (**Cluster** -> **Settings** -> **Scale Cluster**) tooincrease or decrease hello number of worker nodes.</span></span>  <span data-ttu-id="13f6b-186">Bu yeniden boyutlandırma hello küme kullanılmadığında aşağı idling için ya da kapasite toomeet hello büyük görevleri ihtiyaçlarını eklemek için yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="13f6b-186">This resizing can be useful for idling down hello cluster when not in use, or for adding capacity toomeet hello needs of larger tasks.</span></span>
   >
   >

   <span data-ttu-id="13f6b-187">Küme, hello veri düğümlerini ve hello kenar düğümüne boyutlandırma zaman aklınızda bazı etkenler tookeep şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="13f6b-187">Some factors tookeep in mind when sizing your cluster, hello data nodes, and hello edge node include:</span></span>  

   * <span data-ttu-id="13f6b-188">Merhaba veriler büyük olduğunda Spark üzerinde dağıtılmış R Server çözümlemeler hello performansını orantılı toohello çalışan düğümlerinin sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="13f6b-188">hello performance of distributed R Server analyses on Spark is proportional toohello number of worker nodes when hello data is large.</span></span>  

   * <span data-ttu-id="13f6b-189">R Server çözümlemeler Hello performansını çözümlenmekte veri hello boyutunda doğrusal ' dir.</span><span class="sxs-lookup"><span data-stu-id="13f6b-189">hello performance of R Server analyses is linear in hello size of data being analyzed.</span></span> <span data-ttu-id="13f6b-190">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="13f6b-190">For example:</span></span>  

     * <span data-ttu-id="13f6b-191">Küçük toomodest verileri için performans yerel işlem bağlamda hello kenar düğümü üzerindeki analiz olduğunda en iyisidir.</span><span class="sxs-lookup"><span data-stu-id="13f6b-191">For small toomodest data, performance is best when analyzed in a local compute context on hello edge node.</span></span>  <span data-ttu-id="13f6b-192">Bağlamları hello yerel ve Spark altında işlem hello senaryoları hakkında daha fazla bilgi için en iyi şekilde çalışır, Hdınsight'ta R Server için işlem bağlamı seçenekleri konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="13f6b-192">For more information on hello scenarios under which hello local and Spark compute contexts work best, see  Compute context options for R Server on HDInsight.</span></span><br>
     * <span data-ttu-id="13f6b-193">Toohello kenar düğümünde oturum açın ve R betiği çalıştırın, ardından hello ScaleR rx-işlevleri dışındaki tüm yürütülen varsa <strong>yerel olarak</strong> hello edge düğüm üzerinde.</span><span class="sxs-lookup"><span data-stu-id="13f6b-193">If you log in toohello edge node and run your R script, then all but hello ScaleR rx-functions are executed <strong>locally</strong> on hello edge node.</span></span> <span data-ttu-id="13f6b-194">Bu nedenle bellek hello ve hello kenar düğümüne çekirdek sayısı buna göre boyutlandırılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="13f6b-194">So hello memory and number of cores of hello edge node should be sized accordingly.</span></span> <span data-ttu-id="13f6b-195">Merhaba R Server HDI üzerinde uzak işlem bağlamı olarak dizüstü bilgisayarınızdan kullanıyorsanız aynı durum geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="13f6b-195">hello same applies if you use R Server on HDI as a remote compute context from your laptop.</span></span>

     ![Düğüm fiyatlandırma katmanları dikey penceresi](./media/hdinsight-hadoop-r-server-get-started/pricingtier.png)

     <span data-ttu-id="13f6b-197">Kullanım hello **seçin** yapılandırma fiyatlandırma düğmesi toosave hello düğümü.</span><span class="sxs-lookup"><span data-stu-id="13f6b-197">Use hello **Select** button toosave hello node pricing configuration.</span></span>

   <span data-ttu-id="13f6b-198">**Şablon ve parametreleri indirme** bağlantısı da yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="13f6b-198">There is also a link for **Download template and parameters**.</span></span> <span data-ttu-id="13f6b-199">Bir küme hello seçili yapılandırma ile kullanılan tooautomate hello oluşturma olabilir Bu bağlantı toodisplay betikleri tıklayın.</span><span class="sxs-lookup"><span data-stu-id="13f6b-199">Click on this link toodisplay scripts that can be used tooautomate hello creation of a cluster with hello selected configuration.</span></span> <span data-ttu-id="13f6b-200">Oluşturulduktan sonra bu komut dosyalarını da hello kümeniz için Azure portal giriş mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="13f6b-200">These scripts are also available from hello Azure portal entry for your cluster once it has been created.</span></span>

   > [!NOTE]
   > <span data-ttu-id="13f6b-201">Oluşturulan, genellikle yaklaşık 20 dakika hello küme toobe için biraz zaman alabilir.</span><span class="sxs-lookup"><span data-stu-id="13f6b-201">It takes some time for hello cluster toobe created, usually around 20 minutes.</span></span> <span data-ttu-id="13f6b-202">Merhaba döşeme Sabitle hello üzerinde kullanın ya da hello **bildirimleri** hello girişinde sol hello sayfa toocheck hello oluşturma işlemi.</span><span class="sxs-lookup"><span data-stu-id="13f6b-202">Use hello tile on hello Startboard, or hello **Notifications** entry on hello left of hello page toocheck on hello creation process.</span></span>
   >
   >

<a name="connect-to-rstudio-server"></a>
## <a name="connect-toorstudio-server"></a><span data-ttu-id="13f6b-203">TooRStudio sunucusuna bağlan</span><span class="sxs-lookup"><span data-stu-id="13f6b-203">Connect tooRStudio Server</span></span>

<span data-ttu-id="13f6b-204">Daha sonra tooinclude Rstudio'dan Server community edition yüklemenizde seçtiyseniz hello Rstudio'dan oturum açma iki farklı yöntem aracılığıyla erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="13f6b-204">If you’ve chosen tooinclude RStudio Server community edition in your installation, then you can access hello RStudio login via two different methods.</span></span>

1. <span data-ttu-id="13f6b-205">URL aşağıdaki toohello gidin (burada **CLUSTERNAME** oluşturduğunuz hello küme hello adıdır):</span><span class="sxs-lookup"><span data-stu-id="13f6b-205">Go toohello following URL (where **CLUSTERNAME** is hello name of hello cluster you've created):</span></span>

    <span data-ttu-id="13f6b-206">https://**CLUSTERNAME**.azurehdinsight.net/rstudio/</span><span class="sxs-lookup"><span data-stu-id="13f6b-206">https://**CLUSTERNAME**.azurehdinsight.net/rstudio/</span></span>

2. <span data-ttu-id="13f6b-207">Kümeniz için hello girişi hello Azure portal, select hello açmak **R Server panolar** hızlı bağlantıyı ve hello seçme **R Studio Pano**:</span><span class="sxs-lookup"><span data-stu-id="13f6b-207">Open hello entry for your cluster in hello Azure portal, select hello **R Server Dashboards** quick link and then selecting hello **R Studio Dashboard**:</span></span>

     ![Erişim hello R studio Panosu](./media/hdinsight-getting-started-with-r/rstudiodashboard1.png)

     ![Erişim hello R studio Panosu](./media/hdinsight-getting-started-with-r/rstudiodashboard2.png)

   > [!IMPORTANT]
   > <span data-ttu-id="13f6b-210">Kullanılan hello yönteminden bağımsız olarak hello ilk kez oturum açtığınızda, tooauthenticate iki kez gerekir.</span><span class="sxs-lookup"><span data-stu-id="13f6b-210">Regardless of hello method used, hello first time you log in you need tooauthenticate twice.</span></span>  <span data-ttu-id="13f6b-211">Merhaba ilk kimlik doğrulaması sırasında hello sağlamak *yönetici UserID küme* ve *parola*.</span><span class="sxs-lookup"><span data-stu-id="13f6b-211">At hello first authentication, provide hello *cluster Admin userid* and *password*.</span></span> <span data-ttu-id="13f6b-212">Merhaba ikinci isteminde hello sağlamak *SSH UserID* ve *parola*.</span><span class="sxs-lookup"><span data-stu-id="13f6b-212">At hello second prompt, provide hello *SSH userid* and *password*.</span></span> <span data-ttu-id="13f6b-213">Sonraki günlüğü bileşenler yalnızca hello gerektiren *SSH parolası* ve *UserID*.</span><span class="sxs-lookup"><span data-stu-id="13f6b-213">Subsequent log ins only require hello *SSH password* and *userid*.</span></span>

<a name="connect-to-edge-node"></a>
## <a name="connect-toohello-r-server-edge-node"></a><span data-ttu-id="13f6b-214">Toohello R Server edge düğümüne bağlanma</span><span class="sxs-lookup"><span data-stu-id="13f6b-214">Connect toohello R Server edge node</span></span>

<span data-ttu-id="13f6b-215">TooR Server edge düğümüne hello Hdınsight kümesinin hello komutuyla SSH kullanarak bağlanın:</span><span class="sxs-lookup"><span data-stu-id="13f6b-215">Connect tooR Server edge node of hello HDInsight cluster using SSH with hello command:</span></span>

   `ssh USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net`

> [!NOTE]
> <span data-ttu-id="13f6b-216">Merhaba bulabilirsiniz `USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` hello sonra kümenizi seçerek Azure portal adresi **tüm ayarları** -> **uygulamaları** -> **RServer**.</span><span class="sxs-lookup"><span data-stu-id="13f6b-216">You can find hello `USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` address in hello Azure portal by selecting your cluster then **All Settings** -> **Apps** -> **RServer**.</span></span> <span data-ttu-id="13f6b-217">Merhaba hello kenar düğümüne SSH uç nokta bilgileri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="13f6b-217">This displays hello SSH Endpoint information for hello edge node.</span></span>
>
> ![Merhaba SSH uç noktası hello kenar düğümüne görüntüsü](./media/hdinsight-hadoop-r-server-get-started/sshendpoint.png)
>
>

<span data-ttu-id="13f6b-219">SSH kullanıcı hesabınızın parolası toosecure kullandıysanız, istendiğinde tooenter olan bu.</span><span class="sxs-lookup"><span data-stu-id="13f6b-219">If you used a password toosecure your SSH user account, you are prompted tooenter it.</span></span> <span data-ttu-id="13f6b-220">Bir ortak anahtar kullandıysanız, toouse hello olabilir `-i` parametresi toospecify hello eşleşen özel anahtarı.</span><span class="sxs-lookup"><span data-stu-id="13f6b-220">If you used a public key, you may have toouse hello `-i` parameter toospecify hello matching private key.</span></span> <span data-ttu-id="13f6b-221">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="13f6b-221">For example:</span></span>

    ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

<span data-ttu-id="13f6b-222">Daha fazla bilgi için bkz: [tooHDInsight (Hadoop) SSH kullanarak bağlanmak](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="13f6b-222">For more information, see [Connect tooHDInsight (Hadoop) using SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="13f6b-223">Bağlantı kurulduktan sonra bir komut istemi benzer toohello şu ulaşır:</span><span class="sxs-lookup"><span data-stu-id="13f6b-223">Once connected, you arrive at a prompt similar toohello following:</span></span>

    sername@ed00-myrser:~$

<a name="enable-concurrent-users"></a>
## <a name="enable-multiple-concurrent-users"></a><span data-ttu-id="13f6b-224">Birden çok eş zamanlı kullanıcı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="13f6b-224">Enable multiple concurrent users</span></span>

<span data-ttu-id="13f6b-225">Daha fazla kullanıcıları için hangi hello Rstudio'dan topluluk sürümünü çalıştıran hello kenar düğümüne ekleyerek, birden çok eşzamanlı kullanıcı etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="13f6b-225">You can enable multiple concurrent users by adding more users for hello edge node on which hello RStudio community version runs.</span></span>

<span data-ttu-id="13f6b-226">Bir HDInsight kümesi oluşturduğunuzda bir HTTP kullanıcısı ve bir SSH kullanıcısı olmak üzere iki kullanıcı sağlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="13f6b-226">When you create an HDInsight cluster, you must provide two users, an HTTP user and an SSH user:</span></span>

![Eşzamanlı kullanıcı 1](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-1.png)

- <span data-ttu-id="13f6b-228">**Oturum açma kullanıcı küme**: kullanılan tooprotect hello Hdınsight olan hello Hdınsight ağ geçidi üzerinden kimlik doğrulaması için bir HTTP kullanıcı oluşturduğunuz kümeleri.</span><span class="sxs-lookup"><span data-stu-id="13f6b-228">**Cluster login username**: an HTTP user for authentication through hello HDInsight gateway that is used tooprotect hello HDInsight clusters you created.</span></span> <span data-ttu-id="13f6b-229">Bu HTTP kullanılan tooaccess hello Ambari UI, YARN kullanıcı Arabiriminde yanı sıra, diğer kullanıcı Arabirimi bileşenlerini kullanıcıdır.</span><span class="sxs-lookup"><span data-stu-id="13f6b-229">This HTTP user is used tooaccess hello Ambari UI, YARN UI, as well as other UI components.</span></span>
- <span data-ttu-id="13f6b-230">**Güvenli Kabuk (SSH) kullanıcıadı**: Güvenli Kabuk aracılığıyla bir SSH kullanıcı tooaccess hello kümesi.</span><span class="sxs-lookup"><span data-stu-id="13f6b-230">**Secure Shell (SSH) username**: an SSH user tooaccess hello cluster through secure shell.</span></span> <span data-ttu-id="13f6b-231">Bu kullanıcı hello Linux sistemi tüm hello baş düğümler, çalışan düğümlerine ve kenar düğümler için de bir kullanıcıdır.</span><span class="sxs-lookup"><span data-stu-id="13f6b-231">This user is a user in hello Linux system for all hello head nodes, worker nodes, and edge nodes.</span></span> <span data-ttu-id="13f6b-232">Bu nedenle, güvenli Kabuk tooaccess hello düğümün herhangi birinden uzak bir kümede kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="13f6b-232">So you can use secure shell tooaccess any of hello nodes in a remote cluster.</span></span>

<span data-ttu-id="13f6b-233">Merhaba Microsoft R Server Hdınsight türü kümede kullanılan hello R Studio Server Community sürümü yalnızca Linux kullanıcı adı ve parola oturum açma mekanizması olarak kabul eder.</span><span class="sxs-lookup"><span data-stu-id="13f6b-233">hello R Studio Server Community version used in hello Microsoft R Server on HDInsight type cluster accepts only Linux username and password as a login mechanism.</span></span> <span data-ttu-id="13f6b-234">Belirteç iletmeyi desteklemez.</span><span class="sxs-lookup"><span data-stu-id="13f6b-234">It does not support passing tokens.</span></span> <span data-ttu-id="13f6b-235">Yeni bir küme oluşturduktan ve toouse R Studio tooaccess istiyorsanız bunu, toolog içinde iki kez gerekir.</span><span class="sxs-lookup"><span data-stu-id="13f6b-235">So if you have created a new cluster and want toouse R Studio tooaccess it, you need toolog in twice.</span></span>

- <span data-ttu-id="13f6b-236">İlk hello Hdınsight ağ geçidi üzerinden hello HTTP kullanıcı kimlik bilgilerini kullanarak oturum açın:</span><span class="sxs-lookup"><span data-stu-id="13f6b-236">First log in using hello HTTP user credentials through hello HDInsight Gateway:</span></span> 

    ![Eşzamanlı kullanıcı 2a](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-2a.png)

- <span data-ttu-id="13f6b-238">Ardından hello SSH kullanıcı kimlik bilgilerini toolog içinde tooRStudio kullanın:</span><span class="sxs-lookup"><span data-stu-id="13f6b-238">Then use hello SSH user credentials toolog in tooRStudio:</span></span>
  
    ![Eşzamanlı kullanıcı 2b](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-2b.png)

<span data-ttu-id="13f6b-240">Şu anda bir HDInsight kümesi sağlanırken yalnızca bir SSH kullanıcı hesabı oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="13f6b-240">Currently, only one SSH user account can be created when provisioning an HDInsight cluster.</span></span> <span data-ttu-id="13f6b-241">Birden çok kullanıcı tooaccess Microsoft hdınsight'ta R Server tooenable kümeleri şekilde hello Linux sistem toocreate ek kullanıcılar ihtiyacımız var.</span><span class="sxs-lookup"><span data-stu-id="13f6b-241">So tooenable multiple users tooaccess Microsoft R Server on HDInsight clusters, we need toocreate additional users in hello Linux system.</span></span>

<span data-ttu-id="13f6b-242">Rstudio'dan Server Topluluğu hello kümenin kenar düğümüne üzerinde çalıştığı için burada birkaç adım vardır:</span><span class="sxs-lookup"><span data-stu-id="13f6b-242">Because RStudio Server Community is running on hello cluster’s edge node, there are several steps here:</span></span>

1. <span data-ttu-id="13f6b-243">Oluşturulan hello SSH kullanıcı toolog toohello kenar düğümünü kullanın</span><span class="sxs-lookup"><span data-stu-id="13f6b-243">Use hello created SSH user toolog in toohello edge node</span></span>
2. <span data-ttu-id="13f6b-244">Kenar düğümüne daha fazla Linux kullanıcısı ekleme</span><span class="sxs-lookup"><span data-stu-id="13f6b-244">Add more Linux users in edge node</span></span>
3. <span data-ttu-id="13f6b-245">Oluşturulan hello kullanıcıyla Rstudio'dan topluluk sürümünü kullanın</span><span class="sxs-lookup"><span data-stu-id="13f6b-245">Use RStudio Community version with hello user created</span></span>

### <a name="step-1-use-hello-created-ssh-user-toolog-in-toohello-edge-node"></a><span data-ttu-id="13f6b-246">1. adım: hello oluşturulan SSH kullanıcı toolog toohello kenar düğümünü kullanın.</span><span class="sxs-lookup"><span data-stu-id="13f6b-246">Step 1: Use hello created SSH user toolog in toohello edge node</span></span>

<span data-ttu-id="13f6b-247">Herhangi bir SSH Aracı (örneğin, Putty) indirin ve hello varolan SSH kullanıcı toolog içinde kullanın.</span><span class="sxs-lookup"><span data-stu-id="13f6b-247">Download any SSH tool (such as Putty) and use hello existing SSH user toolog in.</span></span> <span data-ttu-id="13f6b-248">Sağlanan hello yönergeleri izleyin [tooHDInsight (Hadoop) SSH kullanarak bağlanmak](hdinsight-hadoop-linux-use-ssh-unix.md) tooaccess hello kenar düğümüne.</span><span class="sxs-lookup"><span data-stu-id="13f6b-248">Then follow hello instructions provided in [Connect tooHDInsight (Hadoop) using SSH](hdinsight-hadoop-linux-use-ssh-unix.md) tooaccess hello edge node.</span></span> <span data-ttu-id="13f6b-249">Itanium tabanlı sistemler için Hello edge düğüm adresi R Server için Hdınsight kümesinde: *clustername ed ssh.azurehdinsight.net*</span><span class="sxs-lookup"><span data-stu-id="13f6b-249">hello edge node address for R Server on HDInsight cluster is: *clustername-ed-ssh.azurehdinsight.net*</span></span>


### <a name="step-2-add-more-linux-users-in-edge-node"></a><span data-ttu-id="13f6b-250">2. Adım: Kenar düğümüne daha fazla Linux kullanıcısı ekleme</span><span class="sxs-lookup"><span data-stu-id="13f6b-250">Step 2: Add more Linux users in edge node</span></span>

<span data-ttu-id="13f6b-251">bir kullanıcı toohello kenar düğümüne tooadd hello komutları yürütün:</span><span class="sxs-lookup"><span data-stu-id="13f6b-251">tooadd a user toohello edge node, execute hello commands:</span></span>

    sudo useradd yournewusername -m
    sudo passwd yourusername

<span data-ttu-id="13f6b-252">Döndürülen öğe aşağıdaki hello görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="13f6b-252">You should see hello following items returned:</span></span> 

![Eşzamanlı kullanıcı 3](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-3.png)

<span data-ttu-id="13f6b-254">İstendiğinde "geçerli Kerberos Parola:", yalnızca basın **Enter** tooignore onu.</span><span class="sxs-lookup"><span data-stu-id="13f6b-254">When prompted for “Current Kerberos password:”, just press **Enter** tooignore it.</span></span> <span data-ttu-id="13f6b-255">Merhaba `-m` seçeneğini `useradd` komutu gösterir hello sistem Rstudio'dan topluluğu sürümü için gerekli olan hello kullanıcı için giriş klasörü oluşturur.</span><span class="sxs-lookup"><span data-stu-id="13f6b-255">hello `-m` option in `useradd` command indicates that hello system will create a home folder for hello user, which is required for RStudio Community version.</span></span>


### <a name="step-3-use-rstudio-community-version-with-hello-user-created"></a><span data-ttu-id="13f6b-256">3. adım: Oluşturulan hello kullanıcıyla kullanım Rstudio'dan topluluğu sürümü</span><span class="sxs-lookup"><span data-stu-id="13f6b-256">Step 3: Use RStudio Community version with hello user created</span></span>

<span data-ttu-id="13f6b-257">Merhaba kullanıcı tarafından oluşturulmuş toolog içinde tooRStudio kullanın:</span><span class="sxs-lookup"><span data-stu-id="13f6b-257">Use hello user created toolog in tooRStudio:</span></span>

![Eşzamanlı kullanıcı 4](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-4.png)

<span data-ttu-id="13f6b-259">Bildirim Rstudio'dan hello yeni kullanıcı kullandığınızı gösterir (burada, örneğin, *sshuser6*) hello kümedeki toolog:</span><span class="sxs-lookup"><span data-stu-id="13f6b-259">Notice that RStudio indicates that you are using hello new user (here, for example, *sshuser6*) toolog in hello cluster:</span></span> 

![Eşzamanlı kullanıcı 5](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-5.png)

<span data-ttu-id="13f6b-261">Merhaba özgün kimlik bilgilerini kullanarak da oturum açabilir (varsayılan olarak, olmasından *sshuser*) aynı anda başka bir tarayıcı penceresi öğesinden.</span><span class="sxs-lookup"><span data-stu-id="13f6b-261">You can also log in using hello original credentials (by default, it is *sshuser*) concurrently from another browser window.</span></span>

<span data-ttu-id="13f6b-262">scaleR işlevlerini kullanarak bir iş gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="13f6b-262">You can submit a job using scaleR functions.</span></span> <span data-ttu-id="13f6b-263">Bir işi hello kullanılan komutlar toorun örneği şöyledir:</span><span class="sxs-lookup"><span data-stu-id="13f6b-263">Here is an example of hello commands used toorun a job:</span></span>

    # Set hello HDFS (WASB) location of example data.
    bigDataDirRoot <- "/example/data"

    # Create a local folder for storaging data temporarily.
    source <- "/tmp/AirOnTimeCSV2012"
    dir.create(source)

    # Download data toohello tmp folder.
    remoteDir <- "http://packages.revolutionanalytics.com/datasets/AirOnTimeCSV2012"
    download.file(file.path(remoteDir, "airOT201201.csv"), file.path(source, "airOT201201.csv"))
    download.file(file.path(remoteDir, "airOT201202.csv"), file.path(source, "airOT201202.csv"))
    download.file(file.path(remoteDir, "airOT201203.csv"), file.path(source, "airOT201203.csv"))
    download.file(file.path(remoteDir, "airOT201204.csv"), file.path(source, "airOT201204.csv"))
    download.file(file.path(remoteDir, "airOT201205.csv"), file.path(source, "airOT201205.csv"))
    download.file(file.path(remoteDir, "airOT201206.csv"), file.path(source, "airOT201206.csv"))
    download.file(file.path(remoteDir, "airOT201207.csv"), file.path(source, "airOT201207.csv"))
    download.file(file.path(remoteDir, "airOT201208.csv"), file.path(source, "airOT201208.csv"))
    download.file(file.path(remoteDir, "airOT201209.csv"), file.path(source, "airOT201209.csv"))
    download.file(file.path(remoteDir, "airOT201210.csv"), file.path(source, "airOT201210.csv"))
    download.file(file.path(remoteDir, "airOT201211.csv"), file.path(source, "airOT201211.csv"))
    download.file(file.path(remoteDir, "airOT201212.csv"), file.path(source, "airOT201212.csv"))

    # Set directory in bigDataDirRoot tooload hello data.
    inputDir <- file.path(bigDataDirRoot,"AirOnTimeCSV2012")

    # Create hello directory.
    rxHadoopMakeDir(inputDir)

    # Copy hello data from source tooinput.
    rxHadoopCopyFromLocal(source, bigDataDirRoot)

    # Define hello HDFS (WASB) file system.
    hdfsFS <- RxHdfsFileSystem()

    # Create info list for hello airline data.
    airlineColInfo <- list(
    DAY_OF_WEEK = list(type = "factor"),
    ORIGIN = list(type = "factor"),
    DEST = list(type = "factor"),
    DEP_TIME = list(type = "integer"),
    ARR_DEL15 = list(type = "logical"))

    # Get all hello column names.
    varNames <- names(airlineColInfo)

    # Define hello text data source in HDFS.
    airOnTimeData <- RxTextData(inputDir, colInfo = airlineColInfo, varsToKeep = varNames, fileSystem = hdfsFS)

    # Define hello text data source in local system.
    airOnTimeDataLocal <- RxTextData(source, colInfo = airlineColInfo, varsToKeep = varNames)

    # Specify hello formula toouse.
    formula = "ARR_DEL15 ~ ORIGIN + DAY_OF_WEEK + DEP_TIME + DEST"

    # Define hello Spark compute context.
    mySparkCluster <- RxSpark()

    # Set hello compute context.
    rxSetComputeContext(mySparkCluster)

    # Run a logistic regression.
    system.time(
        modelSpark <- rxLogit(formula, data = airOnTimeData)
    )

    # Display a summary.
    summary(modelSpark)


<span data-ttu-id="13f6b-264">Gönderilen Merhaba işleri YARN kullanıcı arabiriminde farklı kullanıcı adları altında olduğuna dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="13f6b-264">Notice that hello jobs submitted are under different user names in YARN UI:</span></span>

![Eşzamanlı kullanıcı 6](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-6.png)

<span data-ttu-id="13f6b-266">Ayrıca bu hello yeni kullanıcılar Linux sistemde kök ayrıcalıkları olmayan, ancak bunlar sahip hello aynı eklenen not tooall hello hello uzak HDFS ve WASB depolama dosyalarında erişin.</span><span class="sxs-lookup"><span data-stu-id="13f6b-266">Note also that hello newly added users do not have root privileges in Linux system, but they do have hello same access tooall hello files in hello remote HDFS and WASB storage.</span></span>


<a name="use-r-console"></a>
## <a name="use-hello-r-console"></a><span data-ttu-id="13f6b-267">Merhaba R Konsolu'nu kullanma</span><span class="sxs-lookup"><span data-stu-id="13f6b-267">Use hello R console</span></span>

1. <span data-ttu-id="13f6b-268">Merhaba SSH oturumundan komut toostart hello R konsolundan aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="13f6b-268">From hello SSH session, use hello following command toostart hello R console:</span></span>  

        R

2. <span data-ttu-id="13f6b-269">Çıktı benzer toohello aşağıdaki görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="13f6b-269">You should see output similar toohello following:</span></span>
    
    <span data-ttu-id="13f6b-270">R sürüm 3.2.2 (2015-08-14)--"Yangın güvenliği" Telif Hakkı (C) 2015 hello R Foundation istatistiksel bilgi işlem platformu: pc x86_64 için linux gnu (64 bit)</span><span class="sxs-lookup"><span data-stu-id="13f6b-270">R version 3.2.2 (2015-08-14) -- "Fire Safety"  Copyright (C) 2015 hello R Foundation for Statistical Computing  Platform: x86_64-pc-linux-gnu (64-bit)</span></span>

    <span data-ttu-id="13f6b-271">R ücretsiz bir yazılımdır ve HİÇBİR GARANTİ verilmemektedir.</span><span class="sxs-lookup"><span data-stu-id="13f6b-271">R is free software and comes with ABSOLUTELY NO WARRANTY.</span></span>
    <span data-ttu-id="13f6b-272">Hoş Geldiniz tooredistribute olduğunuz belirli koşullar altında.</span><span class="sxs-lookup"><span data-stu-id="13f6b-272">You are welcome tooredistribute it under certain conditions.</span></span>
    <span data-ttu-id="13f6b-273">Dağıtım ayrıntıları için "license()" veya "licence()" yazın.</span><span class="sxs-lookup"><span data-stu-id="13f6b-273">Type 'license()' or 'licence()' for distribution details.</span></span>

    <span data-ttu-id="13f6b-274">Doğal dil desteği yalnızca İngilizce için mevcuttur</span><span class="sxs-lookup"><span data-stu-id="13f6b-274">Natural language support but running in an English locale</span></span>

    <span data-ttu-id="13f6b-275">R birçok katılımcının rol aldığı ortak bir projedir.</span><span class="sxs-lookup"><span data-stu-id="13f6b-275">R is a collaborative project with many contributors.</span></span>
    <span data-ttu-id="13f6b-276">'Contributors()' toocite R veya R yayınlarda nasıl paketler daha fazla bilgi ve 'citation()' yazın.</span><span class="sxs-lookup"><span data-stu-id="13f6b-276">Type 'contributors()' for more information and 'citation()' on how toocite R or R packages in publications.</span></span>

    <span data-ttu-id="13f6b-277">Bazı gösterileri, çevrimiçi Yardım ' help()' veya 'help.start()' için bir HTML tarayıcı arabirimi toohelp 'demo()' türü.</span><span class="sxs-lookup"><span data-stu-id="13f6b-277">Type 'demo()' for some demos, 'help()' for on-line help, or 'help.start()' for an HTML browser interface toohelp.</span></span>
    <span data-ttu-id="13f6b-278">'Q()' tooquit r yazın</span><span class="sxs-lookup"><span data-stu-id="13f6b-278">Type 'q()' tooquit R.</span></span>

    <span data-ttu-id="13f6b-279">Microsoft R Server sürüm 8.0: R Microsoft paketlerinin gelişmiş dağıtımı Telif Hakkı (C) 2016 Microsoft Corporation</span><span class="sxs-lookup"><span data-stu-id="13f6b-279">Microsoft R Server version 8.0: an enhanced distribution of R  Microsoft packages Copyright (C) 2016 Microsoft Corporation</span></span>

    <span data-ttu-id="13f6b-280">Sürüm notları için "readme()" yazın.</span><span class="sxs-lookup"><span data-stu-id="13f6b-280">Type 'readme()' for release notes.</span></span>
    >

3. <span data-ttu-id="13f6b-281">Merhaba gelen `>` komut istemi, R kodu girin.</span><span class="sxs-lookup"><span data-stu-id="13f6b-281">From hello `>` prompt, you can enter R code.</span></span> <span data-ttu-id="13f6b-282">R server içerir tooeasily izin paketleri Hadoop ile etkileşim kurmanızı ve dağıtılmış hesaplamalar çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="13f6b-282">R server includes packages that allow you tooeasily interact with Hadoop and run distributed computations.</span></span> <span data-ttu-id="13f6b-283">Örneğin, komut tooview hello kök hello varsayılan dosya sistemi hello Hdınsight kümesi için aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="13f6b-283">For example, use hello following command tooview hello root of hello default file system for hello HDInsight cluster:</span></span>

    <span data-ttu-id="13f6b-284">rxHadoopListFiles("/")</span><span class="sxs-lookup"><span data-stu-id="13f6b-284">rxHadoopListFiles("/")</span></span>

4. <span data-ttu-id="13f6b-285">Merhaba WASB stili adresleme de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="13f6b-285">You can also use hello WASB style addressing.</span></span>

    <span data-ttu-id="13f6b-286">rxHadoopListFiles("wasb:///")</span><span class="sxs-lookup"><span data-stu-id="13f6b-286">rxHadoopListFiles("wasb:///")</span></span>


## <a name="using-r-server-on-hdi-from-a-remote-instance-of-microsoft-r-server-or-microsoft-r-client"></a><span data-ttu-id="13f6b-287">Microsoft R Server veya Microsoft R Client uzak örneğinden HDI üzerinde R Server kullanma</span><span class="sxs-lookup"><span data-stu-id="13f6b-287">Using R Server on HDI from a remote instance of Microsoft R Server or Microsoft R Client</span></span>

<span data-ttu-id="13f6b-288">Erişim toohello HDI Hadoop Spark işlem bağlamı Microsoft R Server ya da Microsoft R Masaüstü veya dizüstü bilgisayar üzerinde çalışan istemci uzak bir örnekten olası tooset olur.</span><span class="sxs-lookup"><span data-stu-id="13f6b-288">It is possible tooset up access toohello HDI Hadoop Spark compute context from a remote instance of Microsoft R Server or Microsoft R Client running on a desktop or laptop.</span></span> <span data-ttu-id="13f6b-289">Bkz: **kullanarak Microsoft R Server Hadoop istemcisi olarak** alt bölümde hello [bir işlem bağlamı için Spark oluşturma](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="13f6b-289">See **Using Microsoft R Server as a Hadoop Client** subsection in hello [Creating a Compute Context for Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started.md).</span></span> <span data-ttu-id="13f6b-290">toodo toospecify hello hello RxSpark işlem bağlamı dizüstü bilgisayarınızda tanımlarken, aşağıdaki seçenekleri şu nedenle ihtiyacınız: hdfsShareDir, shareDir, sshUsername, sshHostname, sshSwitches ve sshProfileScript.</span><span class="sxs-lookup"><span data-stu-id="13f6b-290">toodo so, you need toospecify hello following options when defining hello RxSpark compute context on your laptop: hdfsShareDir, shareDir, sshUsername, sshHostname, sshSwitches, and sshProfileScript.</span></span> <span data-ttu-id="13f6b-291">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="13f6b-291">For example:</span></span>


    myNameNode <- "default"
    myPort <- 0

    mySshHostname  <- 'rkrrehdi1-ed-ssh.azurehdinsight.net'  # HDI secure shell hostname
    mySshUsername  <- 'remoteuser'# HDI SSH username
    mySshSwitches  <- '-i /cygdrive/c/Data/R/davec'   # HDI SSH private key

    myhdfsShareDir <- paste("/user/RevoShare", mySshUsername, sep="/")
    myShareDir <- paste("/var/RevoShare" , mySshUsername, sep="/")

    mySparkCluster <- RxSpark(
      hdfsShareDir = myhdfsShareDir,
      shareDir     = myShareDir,
      sshUsername  = mySshUsername,
      sshHostname  = mySshHostname,
      sshSwitches  = mySshSwitches,
      sshProfileScript = '/etc/profile',
      nameNode     = myNameNode,
      port         = myPort,
      consoleOutput= TRUE
    )


## <a name="use-a-compute-context"></a><span data-ttu-id="13f6b-292">İşlem bağlamı kullanma</span><span class="sxs-lookup"><span data-stu-id="13f6b-292">Use a compute context</span></span>

<span data-ttu-id="13f6b-293">Hesaplama yerel olarak hello edge düğüm üzerinde gerçekleştirilen ya da hello Hdınsight kümesi hello düğümler dağıtılmış bir işlem bağlamında toocontrol sağlar.</span><span class="sxs-lookup"><span data-stu-id="13f6b-293">A compute context allows you toocontrol whether computation is performed locally on hello edge node or distributed across hello nodes in hello HDInsight cluster.</span></span>

1. <span data-ttu-id="13f6b-294">Rstudio'dan sunucu veya hello R konsolunda (bir SSH oturumu), kod tooload örnek verileri hello varsayılan depolama alanına Hdınsight için aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="13f6b-294">From RStudio Server or hello R console (in an SSH session), use hello following code tooload example data into hello default storage for HDInsight:</span></span>

        # Set hello HDFS (WASB) location of example data
        bigDataDirRoot <- "/example/data"

        # create a local folder for storaging data temporarily
        source <- "/tmp/AirOnTimeCSV2012"
        dir.create(source)

        # Download data toohello tmp folder
        remoteDir <- "http://packages.revolutionanalytics.com/datasets/AirOnTimeCSV2012"
        download.file(file.path(remoteDir, "airOT201201.csv"), file.path(source, "airOT201201.csv"))
        download.file(file.path(remoteDir, "airOT201202.csv"), file.path(source, "airOT201202.csv"))
        download.file(file.path(remoteDir, "airOT201203.csv"), file.path(source, "airOT201203.csv"))
        download.file(file.path(remoteDir, "airOT201204.csv"), file.path(source, "airOT201204.csv"))
        download.file(file.path(remoteDir, "airOT201205.csv"), file.path(source, "airOT201205.csv"))
        download.file(file.path(remoteDir, "airOT201206.csv"), file.path(source, "airOT201206.csv"))
        download.file(file.path(remoteDir, "airOT201207.csv"), file.path(source, "airOT201207.csv"))
        download.file(file.path(remoteDir, "airOT201208.csv"), file.path(source, "airOT201208.csv"))
        download.file(file.path(remoteDir, "airOT201209.csv"), file.path(source, "airOT201209.csv"))
        download.file(file.path(remoteDir, "airOT201210.csv"), file.path(source, "airOT201210.csv"))
        download.file(file.path(remoteDir, "airOT201211.csv"), file.path(source, "airOT201211.csv"))
        download.file(file.path(remoteDir, "airOT201212.csv"), file.path(source, "airOT201212.csv"))

        # Set directory in bigDataDirRoot tooload hello data into
        inputDir <- file.path(bigDataDirRoot,"AirOnTimeCSV2012")

        # Make hello directory
        rxHadoopMakeDir(inputDir)

        # Copy hello data from source tooinput
        rxHadoopCopyFromLocal(source, bigDataDirRoot)

2. <span data-ttu-id="13f6b-295">Ardından, şimdi bazı veri bilgileri oluşturun ve biz hello verilerle çalışmak için iki veri kaynaklarını tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="13f6b-295">Next, let's create some data info and define two data sources so that we can work with hello data.</span></span>

        # Define hello HDFS (WASB) file system
        hdfsFS <- RxHdfsFileSystem()

        # Create info list for hello airline data
        airlineColInfo <- list(
             DAY_OF_WEEK = list(type = "factor"),
             ORIGIN = list(type = "factor"),
             DEST = list(type = "factor"),
             DEP_TIME = list(type = "integer"),
             ARR_DEL15 = list(type = "logical"))

        # get all hello column names
        varNames <- names(airlineColInfo)

        # Define hello text data source in hdfs
        airOnTimeData <- RxTextData(inputDir, colInfo = airlineColInfo, varsToKeep = varNames, fileSystem = hdfsFS)

        # Define hello text data source in local system
        airOnTimeDataLocal <- RxTextData(source, colInfo = airlineColInfo, varsToKeep = varNames)

        # formula toouse
        formula = "ARR_DEL15 ~ ORIGIN + DAY_OF_WEEK + DEP_TIME + DEST"

3. <span data-ttu-id="13f6b-296">Şimdi Lojistik regresyon hello yerel işlem bağlamı kullanarak hello verileri çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="13f6b-296">Let's run a logistic regression over hello data using hello local compute context.</span></span>

        # Set a local compute context
        rxSetComputeContext("local")

        # Run a logistic regression
        system.time(
           modelLocal <- rxLogit(formula, data = airOnTimeDataLocal)
        )

        # Display a summary
        summary(modelLocal)

    <span data-ttu-id="13f6b-297">Satırları benzer toohello aşağıdaki ile biten bir çıktı görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="13f6b-297">You should see output that ends with lines similar toohello following:</span></span>

        Data: airOnTimeDataLocal (RxTextData Data Source)
        File name: /tmp/AirOnTimeCSV2012
        Dependent variable(s): ARR_DEL15
        Total independent variables: 634 (Including number dropped: 3)
        Number of valid observations: 6005381
        Number of missing observations: 91381
        -2*LogLikelihood: 5143814.1504 (Residual deviance on 6004750 degrees of freedom)

        Coefficients:
                         Estimate Std. Error z value Pr(>|z|)
         (Intercept)   -3.370e+00  1.051e+00  -3.208  0.00134 **
         ORIGIN=JFK     4.549e-01  7.915e-01   0.575  0.56548
         ORIGIN=LAX     5.265e-01  7.915e-01   0.665  0.50590
         ......
         DEST=SHD       5.975e-01  9.371e-01   0.638  0.52377
         DEST=TTN       4.563e-01  9.520e-01   0.479  0.63172
         DEST=LAR      -1.270e+00  7.575e-01  -1.676  0.09364 .
         DEST=BPT         Dropped    Dropped Dropped  Dropped

         ---

         Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

         Condition number of final variance-covariance matrix: 11904202
         Number of iterations: 7

4. <span data-ttu-id="13f6b-298">Ardından, Şimdi Çalıştır hello hello Spark bağlamını kullanarak aynı Lojistik regresyon.</span><span class="sxs-lookup"><span data-stu-id="13f6b-298">Next, let's run hello same logistic regression using hello Spark context.</span></span> <span data-ttu-id="13f6b-299">Merhaba Spark bağlam hello Hdınsight kümesindeki tüm hello alt düğümler üzerinden işleme hello dağıtır.</span><span class="sxs-lookup"><span data-stu-id="13f6b-299">hello Spark context distributes hello processing over all hello worker nodes in hello HDInsight cluster.</span></span>

        # Define hello Spark compute context
        mySparkCluster <- RxSpark()

        # Set hello compute context
        rxSetComputeContext(mySparkCluster)

        # Run a logistic regression
        system.time(  
           modelSpark <- rxLogit(formula, data = airOnTimeData)
        )
        
        # Display a summary
        summary(modelSpark)


   > [!NOTE]
   > <span data-ttu-id="13f6b-300">Küme düğümleri arasında MapReduce toodistribute hesaplama de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="13f6b-300">You can also use MapReduce toodistribute computation across cluster nodes.</span></span> <span data-ttu-id="13f6b-301">İşlem bağlamı hakkında daha fazla bilgi için bkz. [HDInsight üzerinde R Server için işlem bağlamı seçenekleri](hdinsight-hadoop-r-server-compute-contexts.md).</span><span class="sxs-lookup"><span data-stu-id="13f6b-301">For more information on compute context, see [Compute context options for R Server on HDInsight](hdinsight-hadoop-r-server-compute-contexts.md).</span></span>


## <a name="distribute-r-code-toomultiple-nodes"></a><span data-ttu-id="13f6b-302">R kodu toomultiple düğümleri Dağıt</span><span class="sxs-lookup"><span data-stu-id="13f6b-302">Distribute R code toomultiple nodes</span></span>

<span data-ttu-id="13f6b-303">R Server ile kolayca var olan R kodu alın ve çalıştırın hello kümedeki birden çok düğüm arasında kullanarak `rxExec`.</span><span class="sxs-lookup"><span data-stu-id="13f6b-303">With R Server, you can easily take existing R code and run it across multiple nodes in hello cluster by using `rxExec`.</span></span> <span data-ttu-id="13f6b-304">Bu işlev bir parametre tarama veya benzetme işlemi sırasında yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="13f6b-304">This function is useful when doing a parameter sweep or simulations.</span></span> <span data-ttu-id="13f6b-305">Merhaba aşağıdaki kodu nasıl örneğidir toouse `rxExec`:</span><span class="sxs-lookup"><span data-stu-id="13f6b-305">hello following code is an example of how toouse `rxExec`:</span></span>

    rxExec( function() {Sys.info()["nodename"]}, timesToRun = 4 )

<span data-ttu-id="13f6b-306">Merhaba Spark veya MapReduce bağlamı hala kullanıyorsanız, bu komut hello nodename değeri hello çalışan düğümleri için bu hello kodu döndürür. `(Sys.info()["nodename"])` çalıştırıldığı.</span><span class="sxs-lookup"><span data-stu-id="13f6b-306">If you are still using hello Spark or MapReduce context, this  command returns hello nodename value for hello worker nodes that hello code `(Sys.info()["nodename"])` is run on.</span></span> <span data-ttu-id="13f6b-307">Örneğin, dört düğümlü bir küme üzerinde tooreceive benzer toohello şu çıktıları bekler:</span><span class="sxs-lookup"><span data-stu-id="13f6b-307">For example, on a four node cluster, you expect tooreceive output similar toohello following:</span></span>

    $rxElem1
        nodename
    "wn3-myrser"

    $rxElem2
        nodename
    "wn0-myrser"

    $rxElem3
        nodename
    "wn3-myrser"

    $rxElem4
        nodename
    "wn3-myrser"


## <a name="accessing-data-in-hive-and-parquet"></a><span data-ttu-id="13f6b-308">Hive ve Parquet Verilerine Erişim</span><span class="sxs-lookup"><span data-stu-id="13f6b-308">Accessing Data in Hive and Parquet</span></span>

<span data-ttu-id="13f6b-309">R Server 9.1 içinde kullanılabilecek bir özellik hello Spark işlem bağlamında ScaleR işlevleri tarafından kullanım için doğrudan erişim toodata Hive ve Parquet sağlar.</span><span class="sxs-lookup"><span data-stu-id="13f6b-309">A feature available in R Server 9.1 allows direct access toodata in Hive and Parquet for use by ScaleR functions in hello Spark compute context.</span></span> <span data-ttu-id="13f6b-310">Bu özellikler, Spark SQL tooload verileri kullanarak Spark DataFrame ScaleR göre Analiz için doğrudan çalışan RxHiveData ve RxParquetData adlı yeni ScaleR veri kaynağı işlevler aracılığıyla kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="13f6b-310">These capabilities are available through new ScaleR data source functions called RxHiveData and RxParquetData that work through use of Spark SQL tooload data directly into a Spark DataFrame for analysis by ScaleR.</span></span>  

<span data-ttu-id="13f6b-311">koddan hello bazı örnek kod kullanımda hello yeni işlevleri sağlar:</span><span class="sxs-lookup"><span data-stu-id="13f6b-311">hello following code provides some sample code on use of hello new functions:</span></span>

    #Create a Spark compute context:
    myHadoopCluster <- rxSparkConnect(reset = TRUE)

    #Retrieve some sample data from Hive and run a model:
    hiveData <- RxHiveData("select * from hivesampletable",
                     colInfo = list(devicemake = list(type = "factor")))
    rxGetInfo(hiveData, getVarInfo = TRUE)

    rxLinMod(querydwelltime ~ devicemake, data=hiveData)

    #Retrieve some sample data from Parquet and run a model:
    rxHadoopMakeDir('/share')
    rxHadoopCopyFromLocal(file.path(rxGetOption('sampleDataDir'), 'claimsParquet/'), '/share/')
    pqData <- RxParquetData('/share/claimsParquet',
                     colInfo = list(
                age    = list(type = "factor"),
               car.age = list(type = "factor"),
                  type = list(type = "factor")
             ) )
    rxGetInfo(pqData, getVarInfo = TRUE)

    rxNaiveBayes(type ~ age + cost, data = pqData)

    #Check on Spark data objects, cleanup, and close hello Spark session:
    lsObj <- rxSparkListData() # two data objs are cached
    lsObj
    rxSparkRemoveData(lsObj)
    rxSparkListData() # it should show empty list
    rxSparkDisconnect(myHadoopCluster)


<span data-ttu-id="13f6b-312">Bu yeni işlevler kullanımı ile ilgili ek bilgi için hello hello aracılığıyla R Server'ın çevrimiçi yardımına bakın `?RxHivedata` ve `?RxParquetData` komutları.</span><span class="sxs-lookup"><span data-stu-id="13f6b-312">For additional info on use of these new functions see hello online help in R Server through use of hello `?RxHivedata` and `?RxParquetData` commands.</span></span>  


## <a name="install-additional-r-packages-on-hello-edge-node"></a><span data-ttu-id="13f6b-313">Ek R paketleri hello kenar düğümüne yükleyin</span><span class="sxs-lookup"><span data-stu-id="13f6b-313">Install additional R packages on hello edge node</span></span>

<span data-ttu-id="13f6b-314">Merhaba kenar düğümüne tooinstall ek R paketlerini istiyorsanız kullanabileceğiniz `install.packages()` doğrudan bağlı toohello kenar zaman SSH düğümünden içinden R konsol hello.</span><span class="sxs-lookup"><span data-stu-id="13f6b-314">If you would like tooinstall additional R packages on hello edge node, you can use `install.packages()` directly from within hello R console when connected toohello edge node through SSH.</span></span> <span data-ttu-id="13f6b-315">Ancak, tooinstall R paketleri hello kümenin hello alt düğümlerinde gerekiyorsa, bir komut dosyası eylemi kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="13f6b-315">However, if you need tooinstall R packages on hello worker nodes of hello cluster, you must use a Script Action.</span></span>

<span data-ttu-id="13f6b-316">Betik eylemleri kullanılan toomake yapılandırma değişiklikleri toohello Hdınsight küme veya tooinstall ek yazılım, ek R paketleri gibi olan Bash betikleridir.</span><span class="sxs-lookup"><span data-stu-id="13f6b-316">Script Actions are Bash scripts that are used toomake configuration changes toohello HDInsight cluster or tooinstall additional software, such as additional R packages.</span></span> <span data-ttu-id="13f6b-317">Betik eylemi kullanarak ek paketleri tooinstall hello aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="13f6b-317">tooinstall additional packages using a Script Action, use hello following steps:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="13f6b-318">Merhaba Küme oluşturulduktan sonra betik eylemleri tooinstall ek R paketlerini kullanma yalnızca kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="13f6b-318">Using Script Actions tooinstall additional R packages can only be used after hello cluster has been created.</span></span> <span data-ttu-id="13f6b-319">Merhaba betik R Server tamamen yüklenmiş ve yapılandırılmış dayanır olarak küme oluşturma sırasında bu yordamı kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="13f6b-319">Do not use this procedure during cluster creation, as hello script relies on R Server being completely installed and configured.</span></span>
>
>

1. <span data-ttu-id="13f6b-320">Merhaba gelen [Azure portal](https://portal.azure.com), Hdınsight kümesinde R sunucunuzu seçin.</span><span class="sxs-lookup"><span data-stu-id="13f6b-320">From hello [Azure portal](https://portal.azure.com), select your R Server on HDInsight cluster.</span></span>

2. <span data-ttu-id="13f6b-321">Merhaba gelen **ayarları** dikey penceresinde, select **betik eylemleri** ve ardından **gönderme yeni** toosubmit yeni betik eylemi.</span><span class="sxs-lookup"><span data-stu-id="13f6b-321">From hello **Settings** blade, select **Script Actions** and then **Submit New** toosubmit a new Script Action.</span></span>

   ![Betik eylemleri dikey penceresinin görüntüsü](./media/hdinsight-hadoop-r-server-get-started/scriptaction.png)

3. <span data-ttu-id="13f6b-323">Merhaba gelen **betik eylemi Gönder** dikey penceresinde, aşağıdaki bilgilerle hello sağlayın:</span><span class="sxs-lookup"><span data-stu-id="13f6b-323">From hello **Submit script action** blade, provide hello following information:</span></span>

   * <span data-ttu-id="13f6b-324">**Ad**: kolay bir tooidentify bu komut dosyası adı</span><span class="sxs-lookup"><span data-stu-id="13f6b-324">**Name**: A friendly name tooidentify this script</span></span>

   * <span data-ttu-id="13f6b-325">**Bash betiği URI’si**: `http://mrsactionscripts.blob.core.windows.net/rpackages-v01/InstallRPackages.sh`</span><span class="sxs-lookup"><span data-stu-id="13f6b-325">**Bash script URI**: `http://mrsactionscripts.blob.core.windows.net/rpackages-v01/InstallRPackages.sh`</span></span>

   * <span data-ttu-id="13f6b-326">**Başlık**: Bu öğenin **işareti kaldırılmış** olmalıdır</span><span class="sxs-lookup"><span data-stu-id="13f6b-326">**Head**: This item should be **unchecked**</span></span>

   * <span data-ttu-id="13f6b-327">**Çalışan**: Bu öğe **işaretlenmiş** olmalıdır</span><span class="sxs-lookup"><span data-stu-id="13f6b-327">**Worker**: This item should be **checked**</span></span>

   * <span data-ttu-id="13f6b-328">**Kenar düğümleri**: Bu öğenin **işareti kaldırılmış** olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="13f6b-328">**Edge nodes**: This item should be **unchecked**.</span></span>

   * <span data-ttu-id="13f6b-329">**Zookeeper**: Bu öğenin **işareti kaldırılmış** olmalıdır</span><span class="sxs-lookup"><span data-stu-id="13f6b-329">**Zookeeper**: This item should be **unchecked**</span></span>

   * <span data-ttu-id="13f6b-330">**Parametreleri**: hello R paketleri yüklü toobe.</span><span class="sxs-lookup"><span data-stu-id="13f6b-330">**Parameters**: hello R packages toobe installed.</span></span> <span data-ttu-id="13f6b-331">Örneğin, `bitops stringr arules`</span><span class="sxs-lookup"><span data-stu-id="13f6b-331">For example, `bitops stringr arules`</span></span>

   * <span data-ttu-id="13f6b-332">**Bu betiği kalıcı yap...** : Bu öğe **İşaretlenmiş** olmalıdır</span><span class="sxs-lookup"><span data-stu-id="13f6b-332">**Persist this script...**: This item should be **Checked**</span></span>  

   > [!NOTE]
   > 1. <span data-ttu-id="13f6b-333">Varsayılan olarak, tüm R paketleri hello Microsoft MRAN depo hello yüklü R Server sürümüyle tutarlı bir anlık yüklenir.</span><span class="sxs-lookup"><span data-stu-id="13f6b-333">By default, all R packages are installed from a snapshot of hello Microsoft MRAN repository consistent with hello version of R Server that has been installed.</span></span> <span data-ttu-id="13f6b-334">Paketler daha yeni sürümleri tooinstall istiyorsanız, bazı riskini uyumsuzluk yoktur.</span><span class="sxs-lookup"><span data-stu-id="13f6b-334">If you want tooinstall newer versions of packages, then there is some risk of incompatibility.</span></span> <span data-ttu-id="13f6b-335">Ancak bu tür bir yükleme belirterek mümkündür `useCRAN` hello ilk hello paketinin liste öğesi, örneğin `useCRAN bitops, stringr, arules`.</span><span class="sxs-lookup"><span data-stu-id="13f6b-335">However this kind of install is possible by specifying `useCRAN` as hello first element of hello package list, for example `useCRAN bitops, stringr, arules`.</span></span>  
   > 2. <span data-ttu-id="13f6b-336">Bazı R paketleri için ek Linux sistem kitaplıkları gerekir.</span><span class="sxs-lookup"><span data-stu-id="13f6b-336">Some R packages require additional Linux system libraries.</span></span> <span data-ttu-id="13f6b-337">Kolaylık olması için biz hello ilk 100 en popüler R paketi tarafından gerekli hello bağımlılıkları önceden yüklediniz.</span><span class="sxs-lookup"><span data-stu-id="13f6b-337">For convenience, we have pre-installed hello dependencies needed by hello top 100 most popular R packages.</span></span> <span data-ttu-id="13f6b-338">Ancak, bunlar dışında kitaplıkları hello R paketleri yüklemeniz gerekiyorsa ardından burada kullanılan hello temel komut dosyasını karşıdan yükleyin ve adımları tooinstall hello sistem kitaplıkları eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="13f6b-338">However, if hello R package(s) you install require libraries beyond these then you must download hello base script used here and add steps tooinstall hello system libraries.</span></span> <span data-ttu-id="13f6b-339">Karşıya yükleme değiştiren hello betik tooa genel Azure depolama kapsayıcıda blob ve değiştiren hello betik tooinstall hello paketlerini kullanma sonra yapmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="13f6b-339">You must then upload hello modified script tooa public blob container in Azure storage and use hello modified script tooinstall hello packages.</span></span>
   >    <span data-ttu-id="13f6b-340">Betik Eylemleri geliştirme hakkında bilgi için bkz. [Betik Eylemi geliştirme](hdinsight-hadoop-script-actions-linux.md).</span><span class="sxs-lookup"><span data-stu-id="13f6b-340">For more information on developing Script Actions, see [Script Action development](hdinsight-hadoop-script-actions-linux.md).</span></span>  
   >
   >

   ![Betik eylemi ekleme](./media/hdinsight-getting-started-with-r/submitscriptaction.png)

4. <span data-ttu-id="13f6b-342">Seçin **oluşturma** toorun hello komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="13f6b-342">Select **Create** toorun hello script.</span></span> <span data-ttu-id="13f6b-343">Merhaba betik tamamlandıktan sonra tüm çalışan düğümleri üzerinde hello R paketleri kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="13f6b-343">Once hello script completes, hello R packages are available on all worker nodes.</span></span>


## <a name="using-microsoft-r-server-operationalization"></a><span data-ttu-id="13f6b-344">Microsoft R Server ile Kullanıma Hazır Hale Getirme</span><span class="sxs-lookup"><span data-stu-id="13f6b-344">Using Microsoft R Server Operationalization</span></span>

<span data-ttu-id="13f6b-345">Veri modellemesi tamamlandığında hello modeli toomake tahminleri faaliyete geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="13f6b-345">When your data modeling is complete, you can operationalize hello model toomake predictions.</span></span> <span data-ttu-id="13f6b-346">Microsoft R Server operationalization tooconfigure hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="13f6b-346">tooconfigure for Microsoft R Server operationalization, perform hello following steps:</span></span>

<span data-ttu-id="13f6b-347">İlk olarak, ssh hello kenar düğümüne içine.</span><span class="sxs-lookup"><span data-stu-id="13f6b-347">First, ssh into hello Edge node.</span></span> <span data-ttu-id="13f6b-348">Örneğin,</span><span class="sxs-lookup"><span data-stu-id="13f6b-348">For example,</span></span> 

    ssh -L USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

<span data-ttu-id="13f6b-349">SSH kullandıktan sonra hello ilgili sürümü ve sudo hello dotnet dll dizini değiştirin:</span><span class="sxs-lookup"><span data-stu-id="13f6b-349">After using ssh, change directory for hello relevant version and sudo hello dotnet dll:</span></span> 

- <span data-ttu-id="13f6b-350">Microsoft R Server 9.1 için:</span><span class="sxs-lookup"><span data-stu-id="13f6b-350">For Microsoft R Server 9.1:</span></span>

    <span data-ttu-id="13f6b-351">cd /usr/lib64/microsoft-r/rserver/o16n/9.1.0   sudo dotnet Microsoft.RServer.Utils.AdminUtil/Microsoft.RServer.Utils.AdminUtil.dll</span><span class="sxs-lookup"><span data-stu-id="13f6b-351">cd /usr/lib64/microsoft-r/rserver/o16n/9.1.0   sudo dotnet Microsoft.RServer.Utils.AdminUtil/Microsoft.RServer.Utils.AdminUtil.dll</span></span>

- <span data-ttu-id="13f6b-352">Microsoft R Server 9.0 için:</span><span class="sxs-lookup"><span data-stu-id="13f6b-352">For Microsoft R Server 9.0:</span></span>

    <span data-ttu-id="13f6b-353">cd /usr/lib64/microsoft-deployr/9.0.1   sudo dotnet Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll</span><span class="sxs-lookup"><span data-stu-id="13f6b-353">cd /usr/lib64/microsoft-deployr/9.0.1   sudo dotnet Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll</span></span>

<span data-ttu-id="13f6b-354">Bir çalıştırma yapılandırmasıyla tooconfigure Microsoft R Server operationalization hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="13f6b-354">tooconfigure Microsoft R Server operationalization with a One-box configuration do hello following:</span></span>

1. <span data-ttu-id="13f6b-355">"R Server'ı Kullanıma Hazır Hale Getirmek için Yapılandır" seçeneğini belirleyin</span><span class="sxs-lookup"><span data-stu-id="13f6b-355">Select “Configure R Server for Operationalization”</span></span>
2. <span data-ttu-id="13f6b-356">“A.</span><span class="sxs-lookup"><span data-stu-id="13f6b-356">Select “A.</span></span> <span data-ttu-id="13f6b-357">One-box (web + işlem düğümleri)” öğesini seçin</span><span class="sxs-lookup"><span data-stu-id="13f6b-357">One-box (web + compute nodes)”</span></span>
3. <span data-ttu-id="13f6b-358">Hello için bir parola girmenizi **yönetici** kullanıcı</span><span class="sxs-lookup"><span data-stu-id="13f6b-358">Enter a password for hello **admin** user</span></span>

![one box işlemi](./media/hdinsight-hadoop-r-server-get-started/admin-util-one-box-.png)

<span data-ttu-id="13f6b-360">İsteğe bağlı bir adım olarak aşağıdaki şekilde bir tanılama testi çalıştırarak Tanılama denetimleri gerçekleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="13f6b-360">As an optional step you can perform Diagnostic checks by running a diagnostic test as follows:</span></span>

1. <span data-ttu-id="13f6b-361">“6.</span><span class="sxs-lookup"><span data-stu-id="13f6b-361">Select “6.</span></span> <span data-ttu-id="13f6b-362">Tanılama testleri çalıştır” öğesini seçin</span><span class="sxs-lookup"><span data-stu-id="13f6b-362">Run diagnostic tests”</span></span>
2. <span data-ttu-id="13f6b-363">“A.</span><span class="sxs-lookup"><span data-stu-id="13f6b-363">Select “A.</span></span> <span data-ttu-id="13f6b-364">Test yapılandırması” öğesini seçin</span><span class="sxs-lookup"><span data-stu-id="13f6b-364">Test configuration”</span></span>
3. <span data-ttu-id="13f6b-365">Kullanıcı adı olarak "admin" değerini ve önceki yapılandırma adımında belirtilen parolayı girin</span><span class="sxs-lookup"><span data-stu-id="13f6b-365">Enter Username = “admin” and password from previous configuration step</span></span>
4. <span data-ttu-id="13f6b-366">Genel Sistem Durumunu Onayla = başarılı</span><span class="sxs-lookup"><span data-stu-id="13f6b-366">Confirm Overall Health = pass</span></span>
5. <span data-ttu-id="13f6b-367">Çıkış hello yönetim yardımcı programı</span><span class="sxs-lookup"><span data-stu-id="13f6b-367">Exit hello Admin Utility</span></span>
6. <span data-ttu-id="13f6b-368">SSH’den çıkın</span><span class="sxs-lookup"><span data-stu-id="13f6b-368">Exit SSH</span></span>

![İşlem için tanılama](./media/hdinsight-hadoop-r-server-get-started/admin-util-diagnostics.png)


>[!NOTE]
><span data-ttu-id="13f6b-370">**Spark’ta web hizmeti tüketilirken uzun gecikmeler**</span><span class="sxs-lookup"><span data-stu-id="13f6b-370">**Long delays when consuming web service on Spark**</span></span>
>
><span data-ttu-id="13f6b-371">Tooconsume bir web hizmeti çalışıyor Spark işlem bağlamda mrsdeploy işlevlerle oluşturduğunuzda gecikmelere karşılaşırsanız, bazı eksik klasörler tooadd gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="13f6b-371">If you encounter long delays when trying tooconsume a web service created with mrsdeploy functions in a Spark compute context, you may need tooadd some missing folders.</span></span> <span data-ttu-id="13f6b-372">Merhaba Spark uygulama ait tooa kullanıcı olarak adlandırılır ve '*rserve2*' ne zaman onu çağrılır mrsdeploy işlevleri kullanarak bir web hizmetinden.</span><span class="sxs-lookup"><span data-stu-id="13f6b-372">hello Spark application belongs tooa user called '*rserve2*' whenever it is invoked from a web service using mrsdeploy functions.</span></span> <span data-ttu-id="13f6b-373">Bu soruna geçici bir çözüm toowork:</span><span class="sxs-lookup"><span data-stu-id="13f6b-373">toowork around this issue:</span></span>

    # Create these required folders for user 'rserve2' in local and hdfs:

    hadoop fs -mkdir /user/RevoShare/rserve2
    hadoop fs -chmod 777 /user/RevoShare/rserve2

    mkdir /var/RevoShare/rserve2
    chmod 777 /var/RevoShare/rserve2


    # Next, create a new Spark compute context:
 
    rxSparkConnect(reset = TRUE)


<span data-ttu-id="13f6b-374">Bu aşamada Operationalization hello yapılandırması tamamlanır.</span><span class="sxs-lookup"><span data-stu-id="13f6b-374">At this stage, hello configuration for Operationalization is complete.</span></span> <span data-ttu-id="13f6b-375">Kullanabileceğiniz artık hello 'mrsdeploy' paketini kenar düğümünü, RClient tooconnect toohello Operationalization üzerinde ve özellikleri gibi kullanmaya başlamak [uzaktan yürütme](https://msdn.microsoft.com/microsoft-r/operationalize/remote-execution) ve [web Hizmetleri](https://msdn.microsoft.com/microsoft-r/mrsdeploy/mrsdeploy-websrv-vignette).</span><span class="sxs-lookup"><span data-stu-id="13f6b-375">Now you can use hello ‘mrsdeploy’ package on your RClient tooconnect toohello Operationalization on edge node and start using its features like [remote execution](https://msdn.microsoft.com/microsoft-r/operationalize/remote-execution) and [web-services](https://msdn.microsoft.com/microsoft-r/mrsdeploy/mrsdeploy-websrv-vignette).</span></span> <span data-ttu-id="13f6b-376">Olup, küme üzerinde bir sanal ağ veya kurulduğuna bağlı olarak, yukarı bağlantı noktası aracılığıyla SSH oturum iletme tünel tooset gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="13f6b-376">Depending on whether your cluster is set up on a virtual network or not, you may need tooset up port forward tunneling through SSH login.</span></span> <span data-ttu-id="13f6b-377">Merhaba aşağıdaki bölümlerde açıklanmıştır nasıl tooset bu tünel ayarlama.</span><span class="sxs-lookup"><span data-stu-id="13f6b-377">hello following sections explain how tooset up this tunnel.</span></span>

### <a name="rserver-cluster-on-virtual-network"></a><span data-ttu-id="13f6b-378">Sanal ağda RServer Kümesi</span><span class="sxs-lookup"><span data-stu-id="13f6b-378">RServer Cluster on virtual network</span></span>

<span data-ttu-id="13f6b-379">Bağlantı noktası 12800 toohello kenar düğümüne üzerinden trafiğe izin emin olun.</span><span class="sxs-lookup"><span data-stu-id="13f6b-379">Make sure you allow traffic through port 12800 toohello edge node.</span></span> <span data-ttu-id="13f6b-380">Bu şekilde hello kenar düğümü tooconnect toohello Operationalization özelliğini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="13f6b-380">That way, you can use hello edge node tooconnect toohello Operationalization feature.</span></span>


    library(mrsdeploy)

    remoteLogin(
        deployr_endpoint = "http://[your-cluster-name]-ed-ssh.azurehdinsight.net:12800",
        username = "admin",
        password = "xxxxxxx"
    )


<span data-ttu-id="13f6b-381">Merhaba, `remoteLogin()` olamaz toohello kenar düğümüne bağlanmak ancak SSH toohello kenar düğümünü kullanabilirsiniz, ardından bağlantı noktası 12800 hello kural tooallow trafiğine düzgün ya da olmasın ayarlanmış olup olmadığını tooverify gerekir.</span><span class="sxs-lookup"><span data-stu-id="13f6b-381">If hello `remoteLogin()` cannot connect toohello edge node, but you can SSH toohello edge node, then you need tooverify whether hello rule tooallow traffic on port 12800 has been set properly or not.</span></span> <span data-ttu-id="13f6b-382">Tooface hello sorunu devam ederseniz, bu bağlantı noktası iletme SSH tünel yukarı ayarlayarak çalışabilir.</span><span class="sxs-lookup"><span data-stu-id="13f6b-382">If you continue tooface hello issue, you can work around it by setting up port forward tunneling through SSH.</span></span> <span data-ttu-id="13f6b-383">Merhaba bölümü aşağıdaki yönergeler için bkz.</span><span class="sxs-lookup"><span data-stu-id="13f6b-383">For instructions, see hello following section.</span></span>

### <a name="rserver-cluster-not-set-up-on-virtual-network"></a><span data-ttu-id="13f6b-384">Sanal ağda RServer Kümesi ayarlanmamış</span><span class="sxs-lookup"><span data-stu-id="13f6b-384">RServer Cluster not set up on virtual network</span></span>

<span data-ttu-id="13f6b-385">Kümeniz sanal üzerinde ayarlanmamışsa veya sanal ağ üzerinden bağlantı kurma sorunları yaşıyorsanız, SSH bağlantı noktası iletme tünelini kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="13f6b-385">If your cluster is not set up on vnet or if you are having troubles with connectivity through vnet, you can use SSH port forward tunneling:</span></span>

    ssh -L localhost:12800:localhost:12800 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

<span data-ttu-id="13f6b-386">Putty üzerinde de bu ayarı yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="13f6b-386">On Putty, you can set it up as well.</span></span>

![putty ssh bağlantısı](./media/hdinsight-hadoop-r-server-get-started/putty.png)

<span data-ttu-id="13f6b-388">SSH oturumunuzun etkinleştirildikten sonra makinenizin bağlantı noktası 12800 hello trafiğinden toohello kenar düğümün bağlantı noktası 12800 SSH oturumu üzerinden iletilir.</span><span class="sxs-lookup"><span data-stu-id="13f6b-388">Once your SSH session is active, hello traffic from your machine’s port 12800 is forwarded toohello edge node’s port 12800 through SSH session.</span></span> <span data-ttu-id="13f6b-389">`remoteLogin()` yönteminizde `127.0.0.1:12800` kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="13f6b-389">Make sure you use `127.0.0.1:12800` in your `remoteLogin()` method.</span></span> <span data-ttu-id="13f6b-390">Bu bağlantı noktası iletme aracılığıyla toohello kenar düğümün operationalization kaydeder.</span><span class="sxs-lookup"><span data-stu-id="13f6b-390">This logs in toohello edge node’s operationalization through port forwarding.</span></span>


    library(mrsdeploy)

    remoteLogin(
        deployr_endpoint = "http://127.0.0.1:12800",
        username = "admin",
        password = "xxxxxxx"
    )


## <a name="how-tooscale-microsoft-r-server-operationalization-compute-nodes-on-hdinsight-worker-nodes"></a><span data-ttu-id="13f6b-391">Nasıl tooscale Microsoft R Server Operationalization işlem düğümleri Hdınsight çalışan düğümleri üzerinde</span><span class="sxs-lookup"><span data-stu-id="13f6b-391">How tooscale Microsoft R Server Operationalization compute nodes on HDInsight worker nodes</span></span>

### <a name="decommission-hello-worker-nodes"></a><span data-ttu-id="13f6b-392">Merhaba çalışan düğümü yetkisini alma</span><span class="sxs-lookup"><span data-stu-id="13f6b-392">Decommission hello worker node(s)</span></span>

<span data-ttu-id="13f6b-393">Microsoft R Server şu anda Yarn üzerinden yönetilmemektedir.</span><span class="sxs-lookup"><span data-stu-id="13f6b-393">Microsoft R Server is currently not managed through Yarn.</span></span> <span data-ttu-id="13f6b-394">Merhaba çalışan düğümleri yetkisi alınmış emin değilseniz, hello Yarn Kaynak Yöneticisi'ni hello sunucu tarafından gerçekleştirilecek hello kaynakları farkında olmayacağı için beklendiği gibi çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="13f6b-394">If hello worker nodes are not decommissioned, hello Yarn Resource Manager will not work as expected because it will not be aware of hello resources being taken up by hello server.</span></span> <span data-ttu-id="13f6b-395">Sipariş tooavoid bu durum hello işlem düğümleri ölçeklendirme önce hello çalışan düğümleri yetkisini öneririz.</span><span class="sxs-lookup"><span data-stu-id="13f6b-395">In order tooavoid this situation, we recommend decommissioning hello worker nodes before you scale out hello compute nodes.</span></span>

<span data-ttu-id="13f6b-396">Adımları toodecommissioning alt düğümleri:</span><span class="sxs-lookup"><span data-stu-id="13f6b-396">Steps toodecommissioning worker nodes:</span></span>

* <span data-ttu-id="13f6b-397">TooHDI kümenin Ambari konsolunda oturum açın ve "ana" sekmesini tıklatın</span><span class="sxs-lookup"><span data-stu-id="13f6b-397">Log in tooHDI cluster's Ambari console and click on "hosts" tab</span></span>
* <span data-ttu-id="13f6b-398">Çalışan düğümü (kullanımdan toobe) seçin, "Eylemler" > "Seçilen konaklar" > "Ana" > "Kapatma üzerinde Bakım modu üzerinde"'i tıklatın.</span><span class="sxs-lookup"><span data-stu-id="13f6b-398">Select worker nodes (toobe decommissioned), Click on "Actions" > "Selected Hosts" > "Hosts" > click on "Turn ON Maintenance Mode".</span></span> <span data-ttu-id="13f6b-399">Örneğin, görüntü aşağıdaki hello biz wn3 ve wn4 toodecommission seçtiniz.</span><span class="sxs-lookup"><span data-stu-id="13f6b-399">For example, in hello following image we have selected wn3 and wn4 toodecommission.</span></span>  

   ![çalışan düğümlerinin yetkisini alma](./media/hdinsight-hadoop-r-server-get-started/get-started-operationalization.png)  

* <span data-ttu-id="13f6b-401">**Eylemler** > **Seçili Ana Bilgisayarlar** > **DataNodes** > öğesini seçip **Yetkisini Al** öğesine tıklayın</span><span class="sxs-lookup"><span data-stu-id="13f6b-401">Select **Actions** > **Selected Hosts** > **DataNodes** > click **Decommission**</span></span>
* <span data-ttu-id="13f6b-402">**Eylemler** > **Seçili Ana Bilgisayarlar** > **NodeManagers** > öğesini seçip **Yetkisini Al** öğesine tıklayın</span><span class="sxs-lookup"><span data-stu-id="13f6b-402">Select **Actions** > **Selected Hosts** > **NodeManagers** > click **Decommission**</span></span>
* <span data-ttu-id="13f6b-403">**Eylemler** > **Seçili Ana Bilgisayarlar** > **DataNodes** > öğesini seçip **Durdur** öğesine tıklayın</span><span class="sxs-lookup"><span data-stu-id="13f6b-403">Select **Actions** > **Selected Hosts** > **DataNodes** > click **Stop**</span></span>
* <span data-ttu-id="13f6b-404">**Eylemler** > **Seçili Ana Bilgisayarlar** > **NodeManagers** > öğesini seçip **Durdur** öğesine tıklayın</span><span class="sxs-lookup"><span data-stu-id="13f6b-404">Select **Actions** > **Selected Hosts** > **NodeManagers** > click on **Stop**</span></span>
* <span data-ttu-id="13f6b-405">**Eylemler** > **Seçili Ana Bilgisayarlar** > **Ana Bilgisayarlar** > öğesini seçip **Tüm Bileşenleri Durdur** öğesine tıklayın</span><span class="sxs-lookup"><span data-stu-id="13f6b-405">Select **Actions** > **Selected Hosts** > **Hosts** > click **Stop All Components**</span></span>
* <span data-ttu-id="13f6b-406">Merhaba çalışan düğümleri seçimini kaldırın ve hello baş düğümler seçin</span><span class="sxs-lookup"><span data-stu-id="13f6b-406">Unselect hello worker nodes and select hello head nodes</span></span>
* <span data-ttu-id="13f6b-407">**Eylemler** > **Seçili Ana Bilgisayarlar** > **Ana Bilgisayarlar** > **Tüm Bileşenleri Yeniden Başlat** öğesini seçin</span><span class="sxs-lookup"><span data-stu-id="13f6b-407">Select **Actions** > **Selected Hosts** > "**Hosts** > **Restart All Components**</span></span>

### <a name="configure-compute-nodes-on-each-decommissioned-worker-nodes"></a><span data-ttu-id="13f6b-408">Yetkisi alınan her çalışan düğümü üzerinde İşlem düğümlerini yapılandırın</span><span class="sxs-lookup"><span data-stu-id="13f6b-408">Configure Compute nodes on each decommissioned worker node(s)</span></span>

1. <span data-ttu-id="13f6b-409">Yetkisi alınan her çalışan düğümüne SSH uygulayın.</span><span class="sxs-lookup"><span data-stu-id="13f6b-409">SSH into each decommissioned worker node.</span></span>
2. <span data-ttu-id="13f6b-410">`dotnet /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll` kullanarak yönetici yardımcı programını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="13f6b-410">Run admin utility using `dotnet /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll`.</span></span>
3. <span data-ttu-id="13f6b-411">"1" tooselect seçeneği "R Server Operationalization için yapılandırma" girin.</span><span class="sxs-lookup"><span data-stu-id="13f6b-411">Enter "1" tooselect option "Configure R Server for Operationalization".</span></span>
4. <span data-ttu-id="13f6b-412">"C"c"tooselect seçeneği girin</span><span class="sxs-lookup"><span data-stu-id="13f6b-412">Enter "c" tooselect option "C.</span></span> <span data-ttu-id="13f6b-413">İşlem düğümü" öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="13f6b-413">Compute node".</span></span> <span data-ttu-id="13f6b-414">Bu, hello çalışan düğümünde hello işlem düğümü yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="13f6b-414">This configures hello compute node on hello worker node.</span></span>
5. <span data-ttu-id="13f6b-415">Çıkış hello yönetim yardımcı programı.</span><span class="sxs-lookup"><span data-stu-id="13f6b-415">Exit hello Admin Utility.</span></span>

### <a name="add-compute-nodes-details-on-web-node"></a><span data-ttu-id="13f6b-416">Web Düğümüne işlem düğümleri ekleme</span><span class="sxs-lookup"><span data-stu-id="13f6b-416">Add compute nodes details on Web Node</span></span>

<span data-ttu-id="13f6b-417">Tüm yetkisi alınmış çalışan düğümleri yapılandırdıktan sonra toorun işlem düğümü, hello kenar düğümüne geri dönün ve hello Microsoft R Server web düğümün yapılandırmasında yetkisi alınmış çalışan düğümleri IP adreslerini ekleyin:</span><span class="sxs-lookup"><span data-stu-id="13f6b-417">Once all decommissioned worker nodes have been configured toorun compute node, come back on hello edge node and add decommissioned worker nodes' IP addresses in hello Microsoft R Server web node's configuration:</span></span>

* <span data-ttu-id="13f6b-418">Merhaba kenar düğümüne içine SSH.</span><span class="sxs-lookup"><span data-stu-id="13f6b-418">SSH into hello edge node.</span></span>
* <span data-ttu-id="13f6b-419">`vi /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Server.WebAPI/appsettings.json` öğesini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="13f6b-419">Run `vi /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Server.WebAPI/appsettings.json`.</span></span>
* <span data-ttu-id="13f6b-420">Merhaba "URI'ler" bölümüne bakın ve alt düğümün IP ve bağlantı noktası ayrıntıları ekleyin.</span><span class="sxs-lookup"><span data-stu-id="13f6b-420">Look for hello "URIs" section, and add worker node's IP and port details.</span></span>

    ![çalışan düğümlerinin yetkisini alma komut satırı](./media/hdinsight-hadoop-r-server-get-started/get-started-op-cmd.png)


## <a name="troubleshoot"></a><span data-ttu-id="13f6b-422">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="13f6b-422">Troubleshoot</span></span>

<span data-ttu-id="13f6b-423">HDInsight kümeleri oluştururken sorun yaşarsanız bkz. [erişim denetimi gereksinimleri](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="13f6b-423">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>


## <a name="next-steps"></a><span data-ttu-id="13f6b-424">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="13f6b-424">Next steps</span></span>

<span data-ttu-id="13f6b-425">Şimdi nasıl toocreate kullanarak hello R Server ve hello temellerini içeren yeni bir Hdınsight kümesi hello bir SSH oturumu R konsolundan anlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="13f6b-425">Now you should understand how toocreate a new HDInsight cluster that includes hello R Server and hello basics of using hello R console from an SSH session.</span></span> <span data-ttu-id="13f6b-426">Merhaba aşağıdaki konularda yönetme ve hdınsight'ta R Server ile çalışma diğer yolları açıklanır:</span><span class="sxs-lookup"><span data-stu-id="13f6b-426">hello following topics explain other ways of managing and working with R Server on HDInsight:</span></span>

* [<span data-ttu-id="13f6b-427">(Küme oluşturma sırasında yüklü değilse) Rstudio'dan sunucu tooHDInsight Ekle</span><span class="sxs-lookup"><span data-stu-id="13f6b-427">Add RStudio Server tooHDInsight (if not installed during cluster creation)</span></span>](hdinsight-hadoop-r-server-install-r-studio.md)
* [<span data-ttu-id="13f6b-428">HDInsight üzerinde R Server için işlem bağlamı seçenekleri</span><span class="sxs-lookup"><span data-stu-id="13f6b-428">Compute context options for R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-compute-contexts.md)
* [<span data-ttu-id="13f6b-429">HDInsight üzerinde R Server için Azure Depolama seçenekleri</span><span class="sxs-lookup"><span data-stu-id="13f6b-429">Azure Storage options for R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-storage.md)
