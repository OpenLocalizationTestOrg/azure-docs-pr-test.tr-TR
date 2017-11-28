---
title: "HDInsight'ta R Server ile çalışmaya başlama - Azure | Microsoft Docs"
description: "HDInsight kümesi üzerinde R Server içeren bir Apache Spark oluşturma ve küme üzerinde bir R betiği gönderme hakkında bilgi edinin."
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
ms.openlocfilehash: 14e2a14c74e00709e18a80325fbdd3cbcd71da37
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-using-r-server-on-hdinsight"></a><span data-ttu-id="2a3a8-103">HDInsight üzerinde R Server kullanmaya başlayın</span><span class="sxs-lookup"><span data-stu-id="2a3a8-103">Get started using R Server on HDInsight</span></span>

<span data-ttu-id="2a3a8-104">HDInsight, HDInsight kümenizle tümleştirilecek bir R Server seçeneği içerir.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-104">HDInsight includes an R Server option to be integrated into your HDInsight cluster.</span></span> <span data-ttu-id="2a3a8-105">Bu seçenek, R betiklerinin dağıtılmış hesaplamaları çalıştırmak için Spark ve MapReduce kullanmasına olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-105">This option allows R scripts to use Spark and MapReduce to run distributed computations.</span></span> <span data-ttu-id="2a3a8-106">Bu belgede, HDInsight kümesi üzerinde bir R Server oluşturma ve ardından dağıtılmış R hesaplamaları için Spark kullanmayı gönderen bir R betiği çalıştırma hakkında bilgi alacaksınız.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-106">In this document, you learn how to create an R Server on HDInsight cluster and then run an R script that demonstrates using Spark for distributed R computations.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="2a3a8-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="2a3a8-107">Prerequisites</span></span>

* <span data-ttu-id="2a3a8-108">**Bir Azure aboneliği**: Bu öğreticiye başlamadan önce bir Azure aboneliğinizin olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-108">**An Azure subscription**: Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="2a3a8-109">Daha fazla bilgi için [Microsoft Azure ücretsiz denemesi edinin](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/) makalesine gidin.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-109">Go to the article [Get Microsoft Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/) for more information.</span></span>
* <span data-ttu-id="2a3a8-110">**Güvenli Kabuk (SSH) istemcisi**: HDInsight kümesine uzaktan bağlanmak ve komutları doğrudan küme üzerinde çalıştırmak için bir SSH istemcisi kullanılır.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-110">**A Secure Shell (SSH) client**: An SSH client is used to remotely connect to the HDInsight cluster and run commands directly on the cluster.</span></span> <span data-ttu-id="2a3a8-111">Daha fazla bilgi için bkz. [HDInsight ile SSH kullanma.](hdinsight-hadoop-linux-use-ssh-unix.md)</span><span class="sxs-lookup"><span data-stu-id="2a3a8-111">For more information, see [Use SSH with HDInsight.](hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>
* <span data-ttu-id="2a3a8-112">**SSH anahtarları (isteğe bağlı)**: Bir parola veya ortak anahtar kullanarak, kümeye bağlanmak için kullanılan SSH hesabını güvenli hale getirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-112">**SSH keys (optional)**: You can secure the SSH account used to connect to the cluster using either a password or a public key.</span></span> <span data-ttu-id="2a3a8-113">Bir parola kullanılması daha kolaydır ve ortak/özel anahtar çifti oluşturmak zorunda kalmadan çalışmaya başlamanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-113">Using a password is easier, and allows you to get started without having to create a public/private key pair.</span></span> <span data-ttu-id="2a3a8-114">Ancak, bir anahtar kullanılması daha güvenlidir.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-114">However, using a key is more secure.</span></span>

> [!NOTE]
> <span data-ttu-id="2a3a8-115">Bu belgedeki adımlarda parola kullandığınız kabul edilmiştir.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-115">The steps in this document assume that you are using a password.</span></span>


## <a name="automated-cluster-creation"></a><span data-ttu-id="2a3a8-116">Otomatik küme oluşturma</span><span class="sxs-lookup"><span data-stu-id="2a3a8-116">Automated cluster creation</span></span>

<span data-ttu-id="2a3a8-117">HDInsight R Server oluşturma işlemini Azure Resource Manager şablonları, SDK ve aynı zamanda PowerShell kullanarak otomatik hale getirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-117">You can automate the creation of HDInsight R Servers using Azure Resource Manager templates, the SDK, and also PowerShell.</span></span>

* <span data-ttu-id="2a3a8-118">Azure Kaynak Yönetimi şablonu ile R Server oluşturmak için bkz. [R Server HDInsight kümesi dağıtma](https://azure.microsoft.com/resources/templates/101-hdinsight-rserver/).</span><span class="sxs-lookup"><span data-stu-id="2a3a8-118">To create an R Server using an Azure Resource Management template, see [Deploy an R server HDInsight cluster](https://azure.microsoft.com/resources/templates/101-hdinsight-rserver/).</span></span>
* <span data-ttu-id="2a3a8-119">.NET SDK kullanarak R Server oluşturmak için bkz. [HDInsight’ta .NET SDK kullanarak Linux tabanlı kümeler oluşturma.](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="2a3a8-119">To create an R Server using the .NET SDK, see [create Linux-based clusters in HDInsight using the .NET SDK.](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span></span>
* <span data-ttu-id="2a3a8-120">PowerShell kullanarak R Server dağıtmak için [HDInsight'ta PowerShell ile R Server oluşturma](hdinsight-hadoop-create-linux-clusters-azure-powershell.md) makalesine bakın.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-120">To deploy R Server using powershell, see the article on [creating an R Server on HDInsight with PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md).</span></span>


<a name="create-hdi-custer-with-aure-portal"></a>
## <a name="create-the-cluster-using-the-azure-portal"></a><span data-ttu-id="2a3a8-121">Azure portalını kullanarak küme oluşturma</span><span class="sxs-lookup"><span data-stu-id="2a3a8-121">Create the cluster using the Azure portal</span></span>

1. <span data-ttu-id="2a3a8-122">[Azure Portal](https://portal.azure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-122">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="2a3a8-123">**YENİ** -> **Zeka + Analiz**, -> **HDInsight** seçeneklerini belirtin.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-123">Select **NEW** -> **Intelligence + Analytics**, -> **HDInsight**.</span></span>

    ![Yeni küme oluşturma görüntüsü](./media/hdinsight-hadoop-r-server-get-started/newcluster.png)

3. <span data-ttu-id="2a3a8-125">**Hızlı oluşturma** deneyiminde **Küme Adı** alanına küme için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-125">In the **Quick create** experience, enter a name for the cluster in the **Cluster Name** field.</span></span> <span data-ttu-id="2a3a8-126">Birden fazla Azure aboneliğiniz varsa, kullanmak istediğiniz aboneliği seçmek için **Abonelik** girişini kullanın.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-126">If you have multiple Azure subscriptions, use the **Subscription** entry to select the one you want to use.</span></span>

    ![Küme adı ve abonelik seçimleri](./media/hdinsight-hadoop-r-server-get-started/clustername.png)

4. <span data-ttu-id="2a3a8-128">**Küme yapılandırması** dikey penceresini açmak için **Küme türü**’nü seçin.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-128">Select **Cluster type** to open the **Cluster configuration** blade.</span></span> <span data-ttu-id="2a3a8-129">**Küme Yapılandırması** dikey penceresinde aşağıdaki seçenekleri belirleyin:</span><span class="sxs-lookup"><span data-stu-id="2a3a8-129">On the **Cluster Configuration** blade, select the following options:</span></span>

    * <span data-ttu-id="2a3a8-130">**Küme Türü**: R Server</span><span class="sxs-lookup"><span data-stu-id="2a3a8-130">**Cluster Type**: R Server</span></span>
    * <span data-ttu-id="2a3a8-131">**Sürüm**: Kümeye yüklenecek R Server sürümünü seçin.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-131">**Version**: select the version of R Server to install on the cluster.</span></span> <span data-ttu-id="2a3a8-132">Şu anda kullanılabilir sürüm: ***R Server 9.1 (HDI 3.6)***.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-132">The version currently available is ***R Server 9.1 (HDI 3.6)***.</span></span> <span data-ttu-id="2a3a8-133">Kullanılabilir R Server sürümlerinin sürüm notları [burada](https://msdn.microsoft.com/microsoft-r/notes/r-server-notes) bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-133">Release notes for the available versions of R Server are available [here](https://msdn.microsoft.com/microsoft-r/notes/r-server-notes).</span></span>
    * <span data-ttu-id="2a3a8-134">**R Server için R Studio topluluk sürümü**: tarayıcı tabanlı bu IDE, kenar düğümüne varsayılan olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-134">**R Studio community edition for R Server**: this browser-based IDE is installed by default on the edge node.</span></span> <span data-ttu-id="2a3a8-135">Yüklememeyi tercih ederseniz, onay kutusunun işaretini kaldırın.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-135">If you would prefer to not have it installed, then uncheck the check box.</span></span> <span data-ttu-id="2a3a8-136">Yüklemeyi seçerseniz, RStudio Server oturum açma sayfasına erişim URL'si, oluşturulan kümenizin portal uygulaması dikey penceresinde bulunur.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-136">If you choose to have it installed, the URL for accessing the RStudio Server login is found on a portal application blade for your cluster once it’s been created.</span></span>
    * <span data-ttu-id="2a3a8-137">Diğer seçenekleri varsayılan değerlerinde bırakın ve küme türünü kaydetmek için **Seç** düğmesini kullanın.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-137">Leave the other options at the default values and use the **Select** button to save the cluster type.</span></span>

        ![Küme türü dikey penceresi ekran görüntüsü](./media/hdinsight-hadoop-r-server-get-started/clustertypeconfig.png)

5. <span data-ttu-id="2a3a8-139">Bir **Küme oturum açma kullanıcı adı** ve **Küme oturum açma parolası** girin.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-139">Enter a **Cluster login username** and **Cluster login password**.</span></span>

    <span data-ttu-id="2a3a8-140">Bir **SSH Kullanıcı Adı** belirtin.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-140">Specify an **SSH Username**.</span></span> <span data-ttu-id="2a3a8-141">SSH, bir **Güvenli Kabuk (SSH)** istemcisi kullanarak kümeye uzaktan bağlanmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-141">SSH is used to remotely connect to the cluster using a **Secure Shell (SSH)** client.</span></span> <span data-ttu-id="2a3a8-142">SSH kullanıcısını bu iletişim kutusunda veya küme oluşturulduktan sonra (kümenin Yapılandırma sekmesinde) belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-142">You can either specify the SSH user in this dialog or after the cluster has been created (in the Configuration tab for the cluster).</span></span> <span data-ttu-id="2a3a8-143">R Server, “remoteuser” şeklinde bir **SSH kullanıcı adı** bekleyecek şekilde yapılandırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-143">R Server is configured to expect an **SSH username** of “remoteuser”.</span></span>  <span data-ttu-id="2a3a8-144">**Farklı bir kullanıcı adı kullanırsanız, küme oluşturulduktan sonra ek bir adım gerçekleştirmeniz gerekir.**</span><span class="sxs-lookup"><span data-stu-id="2a3a8-144">**If you use a different username, you must perform an additional step after the cluster is created.**</span></span>

    <span data-ttu-id="2a3a8-145">Bir ortak anahtarın kullanılmasını tercih etmiyorsanız, kimlik doğrulama türü olarak **PAROLA** kullanmak için **Kümede oturum açarken kullanılan parolayı kullan** kutusunun işaretini kaldırmayın.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-145">Leave the box checked for **Use same password as cluster login** to use **PASSWORD** as the authentication type unless you prefer use of a public key.</span></span>  <span data-ttu-id="2a3a8-146">Küme üzerindeki R Server'a RTVS, RStudio veya başka bir masaüstü IDE gibi bir uzak istemci üzerinden erişmek için ortak/özel anahtar çifti gerekir.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-146">You need a public/private key pair to access R Server on the cluster via a remote client as, for example, RTVS, RStudio or another desktop IDE.</span></span> <span data-ttu-id="2a3a8-147">RStudio Server topluluk sürümünü yüklerseniz bir SSH parolası seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-147">If you install the RStudio Server community edition, you need to choose an SSH password.</span></span>     

    <span data-ttu-id="2a3a8-148">Bir ortak/özel anahtar çifti oluşturmak için **Kümede oturum açarken kullanılan parolayı kullan** kutusunun işaretini kaldırın ve **ORTAK ANAHTAR**'ı seçip aşağıdaki işlemlerle devam edin.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-148">To create and use a public/private key pair, uncheck **Use same password as cluster login** and then select **PUBLIC KEY** and proceed as follows.</span></span> <span data-ttu-id="2a3a8-149">Bu yönergelerde, ssh-keygen veya eşdeğeri ile birlikte Cygwin'in yüklü olduğu varsayılır.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-149">These instructions assume that you have Cygwin with ssh-keygen or an equivalent installed.</span></span>

    * <span data-ttu-id="2a3a8-150">Dizüstü bilgisayarınızda komut isteminden bir genel/özel anahtar çifti oluşturun:</span><span class="sxs-lookup"><span data-stu-id="2a3a8-150">Generate a public/private key pair from the command prompt on your laptop:</span></span>

        <span data-ttu-id="2a3a8-151">ssh-keygen -t rsa -b 2048</span><span class="sxs-lookup"><span data-stu-id="2a3a8-151">ssh-keygen -t rsa -b 2048</span></span>

    * <span data-ttu-id="2a3a8-152">Anahtar dosyasını adlandırmak için istemleri izleyin ve daha fazla güvenlik için bir şifre girin.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-152">Follow the prompt to name a key file and then enter a passphrase for added security.</span></span> <span data-ttu-id="2a3a8-153">Ekranınız aşağıdaki görüntü gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="2a3a8-153">Your screen should look something like the following image:</span></span>

        ![Windows'da SSH cmd satırı](./media/hdinsight-hadoop-r-server-get-started/sshcmdline.png)

    * <span data-ttu-id="2a3a8-155">Bu komut <private-key-filename>.pub adıyla bir özel anahtar dosyası ve ortak anahtar dosyası oluşturur, örneğin furiosa ve furiosa.pub.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-155">This command creates a private key file and a public key file under the name <private-key-filename>.pub, for example furiosa and furiosa.pub.</span></span>

        ![SSH dir](./media/hdinsight-hadoop-r-server-get-started/dir.png)

    * <span data-ttu-id="2a3a8-157">HDI küme kimlik bilgilerini atarken ortak anahtar dosyasını (&#42;.pub) belirtin ve son olarak kaynak grubunuz ile bölgenizi onaylayıp **İleri**'yi seçin.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-157">Then specify the public key file (&#42;.pub) when assigning HDI cluster credentials and finally confirm your resource group and region and select **Next**.</span></span>

        ![Kimlik Bilgileri dikey penceresi](./media/hdinsight-hadoop-r-server-get-started/publickeyfile.png)  

   * <span data-ttu-id="2a3a8-159">Dizüstü bilgisayarınızda özel anahtar dosyasına ilişkin izinleri değiştirin:</span><span class="sxs-lookup"><span data-stu-id="2a3a8-159">Change permissions on the private keyfile on your laptop:</span></span>

        <span data-ttu-id="2a3a8-160">chmod 600 <private-key-filename></span><span class="sxs-lookup"><span data-stu-id="2a3a8-160">chmod 600 <private-key-filename></span></span>

   * <span data-ttu-id="2a3a8-161">Özel anahtar dosyasını uzaktan oturum açma için SSH ile birlikte kullanın:</span><span class="sxs-lookup"><span data-stu-id="2a3a8-161">Use the private key file with SSH for remote login:</span></span>

        <span data-ttu-id="2a3a8-162">ssh –i <private-key-filename> remoteuser@<hostname public ip></span><span class="sxs-lookup"><span data-stu-id="2a3a8-162">ssh –i <private-key-filename> remoteuser@<hostname public ip></span></span>

      <span data-ttu-id="2a3a8-163">Ya da istemci üzerindeki R Server için Hadoop Spark işlem bağlamınız.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-163">Or, as part the definition of your Hadoop Spark compute context for R Server on the client.</span></span> <span data-ttu-id="2a3a8-164">[Spark için İşlem Bağlamı Oluşturma](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started#creating-a-compute-context-for-spark) bölümündeki **Microsoft R Server'ı Hadoop İstemcisi Olarak Kullanma** alt bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-164">See the **Using Microsoft R Server as a Hadoop Client** subsection in [Create a Compute Context for Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started#creating-a-compute-context-for-spark).</span></span>

6. <span data-ttu-id="2a3a8-165">Hızlı oluşturma işlemi, küme tarafından kullanılan HDFS dosya sisteminin birincil konumu olarak kullanılacak depolama hesabı ayarlarını seçmek için sizi **Depolama** dikey penceresine geçirir.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-165">The quick create transitions you to the **Storage** blade to select the storage account settings to be used for the primary location of the HDFS file system used by the cluster.</span></span> <span data-ttu-id="2a3a8-166">Yeni veya mevcut bir Azure Depolama hesabını ya da mevcut bir Data Lake Storage hesabını seçin.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-166">Select either a new or existing Azure Storage account or an existing Data Lake Storage account.</span></span>

    - <span data-ttu-id="2a3a8-167">Bir Azure Depolama hesabı seçerseniz, **Depolama hesabı seçin** öğesini ve ardından ilgili hesabı seçerek mevcut bir depolama hesabını seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-167">If you select an Azure Storage account, an existing storage account is selected by choosing **Select a storage account** and then selecting the relevant account.</span></span> <span data-ttu-id="2a3a8-168">**Depolama hesabı seçin** bölümündeki **Yeni Oluştur** bağlantısını kullanarak yeni bir hesap oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-168">Create a new account using the **Create New** link in the **Select a storage account** section.</span></span>

      > [!NOTE]
      > <span data-ttu-id="2a3a8-169">**Yeni**’yi seçerseniz, yeni depolama hesabınız için bir ad girmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-169">If you select **New** you must enter a name for the new storage account.</span></span> <span data-ttu-id="2a3a8-170">Ad kabul edilirse yeşil bir onay işareti görünür.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-170">A green check appears if the name is accepted.</span></span>

      <span data-ttu-id="2a3a8-171">**Varsayılan Kapsayıcı**, varsayılan olarak kümenin adıdır.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-171">The **Default Container** defaults to the name of the cluster.</span></span> <span data-ttu-id="2a3a8-172">Varsayılan değeri bırakın.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-172">Leave this default as the value.</span></span>

      <span data-ttu-id="2a3a8-173">Yeni depolama hesabı seçeneği belirlendiyse, depolama hesabının oluşturulacağı bölgeyi seçmek için **Konum** belirlemeniz istenir.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-173">If a new storage account option was selected a prompt to select **Location** is given to select which region to create the storage account.</span></span>  

         ![Veri kaynağı dikey penceresi](./media/hdinsight-getting-started-with-r/datastore.png)  

      > [!IMPORTANT]
      > <span data-ttu-id="2a3a8-175">Varsayılan veri kaynağı için konum seçildiğinde, HDInsight kümesinin konumu da ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-175">Selecting the location for the default data source  also sets the location of the HDInsight cluster.</span></span> <span data-ttu-id="2a3a8-176">Küme ve varsayılan veri kaynağı aynı bölgede olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-176">The cluster and default data source must be in the same region.</span></span>

    - <span data-ttu-id="2a3a8-177">Mevcut bir Data Lake Store hesabını kullanmak isterseniz, kullanılacak ADLS depolama hesabını belirleyin ve depo erişimine izin vermek üzere küme *ADD* kimliğini kümenize ekleyin.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-177">If you want to use an existing Data Lake Store, then select the ADLS storage account to use and add the cluster *ADD* identity to your cluster to allow access to the store.</span></span> <span data-ttu-id="2a3a8-178">Bu işlem hakkında daha fazla bilgi için [Azure portalı kullanarak Data Lake Store ile HDInsight kümesi oluşturma](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-hdinsight-hadoop-use-portal) bölümünü inceleyin.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-178">For more information on this process, see [Creating HDInsight cluster with Data Lake Store using Azure portal](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-hdinsight-hadoop-use-portal).</span></span>

    <span data-ttu-id="2a3a8-179">Veri kaynağı yapılandırmasını kaydetmek için **Seç** düğmesini kullanın.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-179">Use the **Select** button to save the data source configuration.</span></span>


7. <span data-ttu-id="2a3a8-180">Bu durumda tüm ayarlarınızı doğrulamak için **Özet** dikey penceresi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-180">The **Summary** blade then displays to validate all your settings.</span></span> <span data-ttu-id="2a3a8-181">Bu pencerede, kümenizdeki sunucu sayısını değiştirmek ve aynı zamanda çalıştırmak istediğiniz **Betik eylemlerini** belirtmek için **Küme boyutunuzu** değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-181">Here you can change your **Cluster size** to modify the number of servers in your cluster and also specify any **Script actions** you want to run.</span></span> <span data-ttu-id="2a3a8-182">Daha büyük bir kümeye ihtiyaç duymadıkça, çalışan düğümleri sayısını varsayılan `4` değerinde bırakın.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-182">Unless you know that you need a larger cluster, leave the number of worker nodes at the default of `4`.</span></span> <span data-ttu-id="2a3a8-183">Kümenin tahmini maliyeti, dikey pencerede gösterilir.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-183">The estimated cost of the cluster is shown within the blade.</span></span>

    ![küme özeti](./media/hdinsight-hadoop-r-server-get-started/clustersummary.png)

   > [!NOTE]
   > <span data-ttu-id="2a3a8-185">Gerekirse, çalışan düğümlerinin sayısını artırmak veya azaltmak üzere Portal üzerinden (**Küme** -> **Ayarlar** -> **Küme Ölçeklendirme**) kümenizi yeniden boyutlandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-185">If needed, you can resize your cluster later through the Portal (**Cluster** -> **Settings** -> **Scale Cluster**) to increase or decrease the number of worker nodes.</span></span>  <span data-ttu-id="2a3a8-186">Yeniden boyutlandırma yapılması, kullanımda olmadığında kümeyi boşa almak veya daha büyük görev gereksinimlerini karşılamak üzere kapasite artırmak için faydalı olabilir.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-186">This resizing can be useful for idling down the cluster when not in use, or for adding capacity to meet the needs of larger tasks.</span></span>
   >
   >

   <span data-ttu-id="2a3a8-187">Kümenizi, veri düğümlerini ve kenar düğümünü boyutlandırırken göz önünde bulundurulması gereken bazı faktörler aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="2a3a8-187">Some factors to keep in mind when sizing your cluster, the data nodes, and the edge node include:</span></span>  

   * <span data-ttu-id="2a3a8-188">Spark üzerinde dağıtılmış R Server analizlerinin performansı, veriler büyük olduğunda çalışan düğümlerinin sayısıyla doğru orantılıdır.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-188">The performance of distributed R Server analyses on Spark is proportional to the number of worker nodes when the data is large.</span></span>  

   * <span data-ttu-id="2a3a8-189">R Server analizlerinin performansı, analiz edilmekte olan verilerin boyutu ile doğrusal yönde ilerler.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-189">The performance of R Server analyses is linear in the size of data being analyzed.</span></span> <span data-ttu-id="2a3a8-190">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="2a3a8-190">For example:</span></span>  

     * <span data-ttu-id="2a3a8-191">Küçük ila orta büyüklükteki veriler için performans, kenar düğümündeki yerel bir işlem bağlamında analiz edildiğinde en üst seviyededir.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-191">For small to modest data, performance is best when analyzed in a local compute context on the edge node.</span></span>  <span data-ttu-id="2a3a8-192">Yerel ve Spark işlem bağlamlarının en iyi şekilde çalıştığı senaryolar hakkında daha fazla bilgi için bkz. HDInsight üzerinde R Server için işlem bağlamı seçenekleri.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-192">For more information on the scenarios under which the local and Spark compute contexts work best, see  Compute context options for R Server on HDInsight.</span></span><br>
     * <span data-ttu-id="2a3a8-193">Kenar düğümünde oturum açıp R betiğinizi çalıştırırsanız kenar düğümde ScaleR rx-işlevleri hariç tüm işlevler <strong>yerel olarak</strong> yürütülür.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-193">If you log in to the edge node and run your R script, then all but the ScaleR rx-functions are executed <strong>locally</strong> on the edge node.</span></span> <span data-ttu-id="2a3a8-194">Kenar düğüm üzerindeki bellek ve çekirdek sayısı ayarlanırken bu durum dikkate alınmalıdır.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-194">So the memory and number of cores of the edge node should be sized accordingly.</span></span> <span data-ttu-id="2a3a8-195">Aynı durum, HDI üzerinde R Server’ı dizüstü bilgisayarınızdan uzak bir işlem bağlamı olarak çalıştırdığınızda geçerli olur.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-195">The same applies if you use R Server on HDI as a remote compute context from your laptop.</span></span>

     ![Düğüm fiyatlandırma katmanları dikey penceresi](./media/hdinsight-hadoop-r-server-get-started/pricingtier.png)

     <span data-ttu-id="2a3a8-197">Düğüm fiyatlandırma yapılandırmasını kaydetmek için **Seç** düğmesini kullanın.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-197">Use the **Select** button to save the node pricing configuration.</span></span>

   <span data-ttu-id="2a3a8-198">**Şablon ve parametreleri indirme** bağlantısı da yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-198">There is also a link for **Download template and parameters**.</span></span> <span data-ttu-id="2a3a8-199">Bu bağlantıya tıkladığınızda, seçili yapılandırma ile küme oluşturma işlemini otomatik hale getirmek için kullanılabilecek betikler gösterilir.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-199">Click on this link to display scripts that can be used to automate the creation of a cluster with the selected configuration.</span></span> <span data-ttu-id="2a3a8-200">Bu betikler, kümeniz oluşturulduktan sonra Azure portalı girişinde de bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-200">These scripts are also available from the Azure portal entry for your cluster once it has been created.</span></span>

   > [!NOTE]
   > <span data-ttu-id="2a3a8-201">Kümenin oluşturulması genellikle yaklaşık 20 dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-201">It takes some time for the cluster to be created, usually around 20 minutes.</span></span> <span data-ttu-id="2a3a8-202">Oluşturma işlemini denetlemek için Başlangıç Panosu’ndaki kutucuğu veya sayfanın solundaki **Bildirimler** girişini kullanın.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-202">Use the tile on the Startboard, or the **Notifications** entry on the left of the page to check on the creation process.</span></span>
   >
   >

<a name="connect-to-rstudio-server"></a>
## <a name="connect-to-rstudio-server"></a><span data-ttu-id="2a3a8-203">RStudio Server’a bağlanma</span><span class="sxs-lookup"><span data-stu-id="2a3a8-203">Connect to RStudio Server</span></span>

<span data-ttu-id="2a3a8-204">Yüklemenize RStudio Server topluluk sürümünü eklemeyi seçtiyseniz, RStudio oturum açma sayfasına iki farklı yöntemle erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-204">If you’ve chosen to include RStudio Server community edition in your installation, then you can access the RStudio login via two different methods.</span></span>

1. <span data-ttu-id="2a3a8-205">Aşağıdaki URL'ye gidin (burada **CLUSTERNAME**, oluşturduğunuz kümenin adıdır):</span><span class="sxs-lookup"><span data-stu-id="2a3a8-205">Go to the following URL (where **CLUSTERNAME** is the name of the cluster you've created):</span></span>

    <span data-ttu-id="2a3a8-206">https://**CLUSTERNAME**.azurehdinsight.net/rstudio/</span><span class="sxs-lookup"><span data-stu-id="2a3a8-206">https://**CLUSTERNAME**.azurehdinsight.net/rstudio/</span></span>

2. <span data-ttu-id="2a3a8-207">Azure portalında kümenizin girişini açıp, **R Server Panoları** hızlı bağlantısını seçip, **R Studio Panosu**'nu seçin:</span><span class="sxs-lookup"><span data-stu-id="2a3a8-207">Open the entry for your cluster in the Azure portal, select the **R Server Dashboards** quick link and then selecting the **R Studio Dashboard**:</span></span>

     ![R studio panosuna erişim](./media/hdinsight-getting-started-with-r/rstudiodashboard1.png)

     ![R studio panosuna erişim](./media/hdinsight-getting-started-with-r/rstudiodashboard2.png)

   > [!IMPORTANT]
   > <span data-ttu-id="2a3a8-210">Kullanılan yöntem ne olursa olsun, ilk kez oturum açtığınızda iki kez kimlik doğrulaması yapmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-210">Regardless of the method used, the first time you log in you need to authenticate twice.</span></span>  <span data-ttu-id="2a3a8-211">İlk kimlik doğrulamasında kümenin *Yönetici kullanıcı kimliğini* ve *parolasını* belirtin.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-211">At the first authentication, provide the *cluster Admin userid* and *password*.</span></span> <span data-ttu-id="2a3a8-212">İkinci istemde *SSH kullanıcı kimliği* ve *parolasını* sağlayın.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-212">At the second prompt, provide the *SSH userid* and *password*.</span></span> <span data-ttu-id="2a3a8-213">Sonraki oturumlarda yalnızca *SSH parolası* ve *kullanıcı kimliği* gerekli olacaktır.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-213">Subsequent log ins only require the *SSH password* and *userid*.</span></span>

<a name="connect-to-edge-node"></a>
## <a name="connect-to-the-r-server-edge-node"></a><span data-ttu-id="2a3a8-214">R Server kenar düğümüne bağlanma</span><span class="sxs-lookup"><span data-stu-id="2a3a8-214">Connect to the R Server edge node</span></span>

<span data-ttu-id="2a3a8-215">Şu komutla HDInsight kümesinin R Server kenar düğümüne SSH kullanarak bağlanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="2a3a8-215">Connect to R Server edge node of the HDInsight cluster using SSH with the command:</span></span>

   `ssh USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net`

> [!NOTE]
> <span data-ttu-id="2a3a8-216">Kümenizi ve ardından **Tüm Ayarlar** -> **Uygulamalar** -> **RServer**'ı seçerek `USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` adresini Azure portalında bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-216">You can find the `USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` address in the Azure portal by selecting your cluster then **All Settings** -> **Apps** -> **RServer**.</span></span> <span data-ttu-id="2a3a8-217">Bu seçim, kenar düğümünün SSH Uç Noktası bilgilerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-217">This displays the SSH Endpoint information for the edge node.</span></span>
>
> ![Kenar düğümünün SSH Uç Noktası görüntüsü](./media/hdinsight-hadoop-r-server-get-started/sshendpoint.png)
>
>

<span data-ttu-id="2a3a8-219">SSH kullanıcı hesabınızın güvenliğini sağlamak için parola kullandıysanız parolayı girmeniz istenir.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-219">If you used a password to secure your SSH user account, you are prompted to enter it.</span></span> <span data-ttu-id="2a3a8-220">Bir ortak anahtar kullandıysanız eşleşen özel anahtarı belirtmek için `-i` parametresini kullanmanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-220">If you used a public key, you may have to use the `-i` parameter to specify the matching private key.</span></span> <span data-ttu-id="2a3a8-221">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="2a3a8-221">For example:</span></span>

    ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

<span data-ttu-id="2a3a8-222">Daha fazla bilgi için bkz. [SSH kullanarak HDInsight'a (Hadoop) bağlanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="2a3a8-222">For more information, see [Connect to HDInsight (Hadoop) using SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="2a3a8-223">Bağlantı kurulduktan sonra aşağıdakine benzer bir isteme ulaşırsınız:</span><span class="sxs-lookup"><span data-stu-id="2a3a8-223">Once connected, you arrive at a prompt similar to the following:</span></span>

    sername@ed00-myrser:~$

<a name="enable-concurrent-users"></a>
## <a name="enable-multiple-concurrent-users"></a><span data-ttu-id="2a3a8-224">Birden çok eş zamanlı kullanıcı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="2a3a8-224">Enable multiple concurrent users</span></span>

<span data-ttu-id="2a3a8-225">RStudio topluluk sürümünün çalıştığı kenar düğümüne daha fazla kullanıcı ekleyerek aynı anda birden fazla eşzamanlı kullanıcıyı etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-225">You can enable multiple concurrent users by adding more users for the edge node on which the RStudio community version runs.</span></span>

<span data-ttu-id="2a3a8-226">Bir HDInsight kümesi oluşturduğunuzda bir HTTP kullanıcısı ve bir SSH kullanıcısı olmak üzere iki kullanıcı sağlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="2a3a8-226">When you create an HDInsight cluster, you must provide two users, an HTTP user and an SSH user:</span></span>

![Eşzamanlı kullanıcı 1](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-1.png)

- <span data-ttu-id="2a3a8-228">**Küme oturum açma kullanıcı adı**: Oluşturduğunuz HDInsight kümelerini korumak için kullanılan HDInsight ağ geçidinden kimlik doğrulaması yapmak için kullanılan HTTP kullanıcısı.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-228">**Cluster login username**: an HTTP user for authentication through the HDInsight gateway that is used to protect the HDInsight clusters you created.</span></span> <span data-ttu-id="2a3a8-229">Bu HTTP kullanıcısı Ambari UI, YARN UI ve diğer UI bileşenlerine erişmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-229">This HTTP user is used to access the Ambari UI, YARN UI, as well as other UI components.</span></span>
- <span data-ttu-id="2a3a8-230">**Secure Shell (SSH) kullanıcı adı**: Kümeye Secure Shell üzerinden erişmek için kullanılan SSH kullanıcısı.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-230">**Secure Shell (SSH) username**: an SSH user to access the cluster through secure shell.</span></span> <span data-ttu-id="2a3a8-231">Bu kullanıcı Linux sisteminde tüm baş düğümler, çalışan düğümleri ve kenar düğümler için kullanılan kullanıcıdır.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-231">This user is a user in the Linux system for all the head nodes, worker nodes, and edge nodes.</span></span> <span data-ttu-id="2a3a8-232">Bu sayede uzak kümedeki düğümlere erişmek için Secure Shell kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-232">So you can use secure shell to access any of the nodes in a remote cluster.</span></span>

<span data-ttu-id="2a3a8-233">HDInsight türü küme üzerindeki Microsoft R Server'da kullanılan R Studio Server topluluk sürümü, oturum açma sistemi olarak yalnızca Linux kullanıcı adı ve parolasını kabul eder.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-233">The R Studio Server Community version used in the Microsoft R Server on HDInsight type cluster accepts only Linux username and password as a login mechanism.</span></span> <span data-ttu-id="2a3a8-234">Belirteç iletmeyi desteklemez.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-234">It does not support passing tokens.</span></span> <span data-ttu-id="2a3a8-235">Bu nedenle yeni bir küme oluşturduysanız ve buna erişmek için R Studio kullanmak istiyorsanız iki kez oturum açmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-235">So if you have created a new cluster and want to use R Studio to access it, you need to log in twice.</span></span>

- <span data-ttu-id="2a3a8-236">İlk olarak HTTP kullanıcısı kimlik bilgilerini kullanarak HDInsight Ağ Geçidi üzerinden oturum açın:</span><span class="sxs-lookup"><span data-stu-id="2a3a8-236">First log in using the HTTP user credentials through the HDInsight Gateway:</span></span> 

    ![Eşzamanlı kullanıcı 2a](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-2a.png)

- <span data-ttu-id="2a3a8-238">Ardından SSH kullanıcısı kimlik bilgilerini kullanarak RStudio oturumu açın:</span><span class="sxs-lookup"><span data-stu-id="2a3a8-238">Then use the SSH user credentials to log in to RStudio:</span></span>
  
    ![Eşzamanlı kullanıcı 2b](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-2b.png)

<span data-ttu-id="2a3a8-240">Şu anda bir HDInsight kümesi sağlanırken yalnızca bir SSH kullanıcı hesabı oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-240">Currently, only one SSH user account can be created when provisioning an HDInsight cluster.</span></span> <span data-ttu-id="2a3a8-241">Bu nedenle birden fazla kullanıcının HDInsight kümeleri üzerindeki Microsoft R Server'a erişmesini sağlamak için Linux sisteminde ek kullanıcılar oluşturmamız gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-241">So to enable multiple users to access Microsoft R Server on HDInsight clusters, we need to create additional users in the Linux system.</span></span>

<span data-ttu-id="2a3a8-242">Kümenin kenar düğümünde RStudio Server Topluluk sürümü çalıştığı için burada birden fazla adım mevcuttur:</span><span class="sxs-lookup"><span data-stu-id="2a3a8-242">Because RStudio Server Community is running on the cluster’s edge node, there are several steps here:</span></span>

1. <span data-ttu-id="2a3a8-243">Kenar düğümde oturum açmak için oluşturulan SSH kullanıcısını kullanma</span><span class="sxs-lookup"><span data-stu-id="2a3a8-243">Use the created SSH user to log in to the edge node</span></span>
2. <span data-ttu-id="2a3a8-244">Kenar düğümüne daha fazla Linux kullanıcısı ekleme</span><span class="sxs-lookup"><span data-stu-id="2a3a8-244">Add more Linux users in edge node</span></span>
3. <span data-ttu-id="2a3a8-245">RStudio Topluluk sürümünü oluşturulan kullanıcıyla kullanma</span><span class="sxs-lookup"><span data-stu-id="2a3a8-245">Use RStudio Community version with the user created</span></span>

### <a name="step-1-use-the-created-ssh-user-to-log-in-to-the-edge-node"></a><span data-ttu-id="2a3a8-246">1. Adım: Kenar düğümde oturum açmak için oluşturulan SSH kullanıcısını kullanma</span><span class="sxs-lookup"><span data-stu-id="2a3a8-246">Step 1: Use the created SSH user to log in to the edge node</span></span>

<span data-ttu-id="2a3a8-247">Herhangi bir SSH aracını (Putty gibi) indirin ve var olan SSH kullanıcısıyla oturum açın.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-247">Download any SSH tool (such as Putty) and use the existing SSH user to log in.</span></span> <span data-ttu-id="2a3a8-248">Ardından [SSH kullanarak HDInsight'a (Hadoop) bağlanma](hdinsight-hadoop-linux-use-ssh-unix.md) bölümündeki yönergeleri izleyerek kenar düğümüne erişin.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-248">Then follow the instructions provided in [Connect to HDInsight (Hadoop) using SSH](hdinsight-hadoop-linux-use-ssh-unix.md) to access the edge node.</span></span> <span data-ttu-id="2a3a8-249">HDInsight kümesi üzerindeki Microsoft R Server için kenar düğümü adresi: *clustername-ed-ssh.azurehdinsight.net*</span><span class="sxs-lookup"><span data-stu-id="2a3a8-249">The edge node address for R Server on HDInsight cluster is: *clustername-ed-ssh.azurehdinsight.net*</span></span>


### <a name="step-2-add-more-linux-users-in-edge-node"></a><span data-ttu-id="2a3a8-250">2. Adım: Kenar düğümüne daha fazla Linux kullanıcısı ekleme</span><span class="sxs-lookup"><span data-stu-id="2a3a8-250">Step 2: Add more Linux users in edge node</span></span>

<span data-ttu-id="2a3a8-251">Kenar düğümüne bir kullanıcı eklemek için şu komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="2a3a8-251">To add a user to the edge node, execute the commands:</span></span>

    sudo useradd yournewusername -m
    sudo passwd yourusername

<span data-ttu-id="2a3a8-252">Aşağıdaki öğelerin döndürülmesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="2a3a8-252">You should see the following items returned:</span></span> 

![Eşzamanlı kullanıcı 3](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-3.png)

<span data-ttu-id="2a3a8-254">"Geçerli Kerberos parolası:" sorulduğunda **Enter** tuşuna basarak atlayın.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-254">When prompted for “Current Kerberos password:”, just press **Enter** to ignore it.</span></span> <span data-ttu-id="2a3a8-255">`useradd` komutundaki `-m` seçeneği, sistemin RStudio Topluluk sürümü için gerekli olan kullanıcı ana klasörünü oluşturacağını belirtir.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-255">The `-m` option in `useradd` command indicates that the system will create a home folder for the user, which is required for RStudio Community version.</span></span>


### <a name="step-3-use-rstudio-community-version-with-the-user-created"></a><span data-ttu-id="2a3a8-256">3. Adım: RStudio Topluluk sürümünü oluşturulan kullanıcıyla kullanma</span><span class="sxs-lookup"><span data-stu-id="2a3a8-256">Step 3: Use RStudio Community version with the user created</span></span>

<span data-ttu-id="2a3a8-257">RStudio oturumu açmak için oluşturulan kullanıcıyı kullanın:</span><span class="sxs-lookup"><span data-stu-id="2a3a8-257">Use the user created to log in to RStudio:</span></span>

![Eşzamanlı kullanıcı 4](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-4.png)

<span data-ttu-id="2a3a8-259">RStudio, kümede oturum açmak için yeni kullanıcıyı (örneğin burada *sshuser6*) kullanmakta olduğunuzu belirtir:</span><span class="sxs-lookup"><span data-stu-id="2a3a8-259">Notice that RStudio indicates that you are using the new user (here, for example, *sshuser6*) to log in the cluster:</span></span> 

![Eşzamanlı kullanıcı 5](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-5.png)

<span data-ttu-id="2a3a8-261">Dilerseniz eşzamanlı olarak başka bir tarayıcı penceresinden özgün kimlik bilgilerini (varsayılan olarak *sshuser* şeklindedir) kullanarak da oturum açabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-261">You can also log in using the original credentials (by default, it is *sshuser*) concurrently from another browser window.</span></span>

<span data-ttu-id="2a3a8-262">scaleR işlevlerini kullanarak bir iş gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-262">You can submit a job using scaleR functions.</span></span> <span data-ttu-id="2a3a8-263">Bir işi çalıştırmak için kullanılan örnek komutlar burada verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="2a3a8-263">Here is an example of the commands used to run a job:</span></span>

    # Set the HDFS (WASB) location of example data.
    bigDataDirRoot <- "/example/data"

    # Create a local folder for storaging data temporarily.
    source <- "/tmp/AirOnTimeCSV2012"
    dir.create(source)

    # Download data to the tmp folder.
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

    # Set directory in bigDataDirRoot to load the data.
    inputDir <- file.path(bigDataDirRoot,"AirOnTimeCSV2012")

    # Create the directory.
    rxHadoopMakeDir(inputDir)

    # Copy the data from source to input.
    rxHadoopCopyFromLocal(source, bigDataDirRoot)

    # Define the HDFS (WASB) file system.
    hdfsFS <- RxHdfsFileSystem()

    # Create info list for the airline data.
    airlineColInfo <- list(
    DAY_OF_WEEK = list(type = "factor"),
    ORIGIN = list(type = "factor"),
    DEST = list(type = "factor"),
    DEP_TIME = list(type = "integer"),
    ARR_DEL15 = list(type = "logical"))

    # Get all the column names.
    varNames <- names(airlineColInfo)

    # Define the text data source in HDFS.
    airOnTimeData <- RxTextData(inputDir, colInfo = airlineColInfo, varsToKeep = varNames, fileSystem = hdfsFS)

    # Define the text data source in local system.
    airOnTimeDataLocal <- RxTextData(source, colInfo = airlineColInfo, varsToKeep = varNames)

    # Specify the formula to use.
    formula = "ARR_DEL15 ~ ORIGIN + DAY_OF_WEEK + DEP_TIME + DEST"

    # Define the Spark compute context.
    mySparkCluster <- RxSpark()

    # Set the compute context.
    rxSetComputeContext(mySparkCluster)

    # Run a logistic regression.
    system.time(
        modelSpark <- rxLogit(formula, data = airOnTimeData)
    )

    # Display a summary.
    summary(modelSpark)


<span data-ttu-id="2a3a8-264">Gönderilen işlerin farklı YARN UI kullanıcı adları altında olduğuna dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="2a3a8-264">Notice that the jobs submitted are under different user names in YARN UI:</span></span>

![Eşzamanlı kullanıcı 6](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-6.png)

<span data-ttu-id="2a3a8-266">Ayrıca yeni eklenen kullanıcıların Linux sisteminde kök ayrıcalıklarına sahip olmadığına ancak uzak HDFS ve WASB depolama alanındaki tüm dosyalara aynı düzeyde erişime sahip olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-266">Note also that the newly added users do not have root privileges in Linux system, but they do have the same access to all the files in the remote HDFS and WASB storage.</span></span>


<a name="use-r-console"></a>
## <a name="use-the-r-console"></a><span data-ttu-id="2a3a8-267">R konsolunu kullanma</span><span class="sxs-lookup"><span data-stu-id="2a3a8-267">Use the R console</span></span>

1. <span data-ttu-id="2a3a8-268">R konsolunu başlatmak için SSH oturumunda aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="2a3a8-268">From the SSH session, use the following command to start the R console:</span></span>  

        R

2. <span data-ttu-id="2a3a8-269">Aşağıdakine benzer bir çıktı görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="2a3a8-269">You should see output similar to the following:</span></span>
    
    <span data-ttu-id="2a3a8-270">R sürüm 3.2.2 (2015-08-14) -- "Fire Safety" Telif Hakkı (C) 2015 The R Foundation for Statistical Computing Platform: x86_64-pc-linux-gnu (64 bit)</span><span class="sxs-lookup"><span data-stu-id="2a3a8-270">R version 3.2.2 (2015-08-14) -- "Fire Safety"  Copyright (C) 2015 The R Foundation for Statistical Computing  Platform: x86_64-pc-linux-gnu (64-bit)</span></span>

    <span data-ttu-id="2a3a8-271">R ücretsiz bir yazılımdır ve HİÇBİR GARANTİ verilmemektedir.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-271">R is free software and comes with ABSOLUTELY NO WARRANTY.</span></span>
    <span data-ttu-id="2a3a8-272">Yazılımı belirli koşullar altında dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-272">You are welcome to redistribute it under certain conditions.</span></span>
    <span data-ttu-id="2a3a8-273">Dağıtım ayrıntıları için "license()" veya "licence()" yazın.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-273">Type 'license()' or 'licence()' for distribution details.</span></span>

    <span data-ttu-id="2a3a8-274">Doğal dil desteği yalnızca İngilizce için mevcuttur</span><span class="sxs-lookup"><span data-stu-id="2a3a8-274">Natural language support but running in an English locale</span></span>

    <span data-ttu-id="2a3a8-275">R birçok katılımcının rol aldığı ortak bir projedir.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-275">R is a collaborative project with many contributors.</span></span>
    <span data-ttu-id="2a3a8-276">Daha fazla bilgi için "contributors()", R veya R paketlerine atıfta bulunmak için ise "citation()" yazın.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-276">Type 'contributors()' for more information and 'citation()' on how to cite R or R packages in publications.</span></span>

    <span data-ttu-id="2a3a8-277">Demolar için "demo()", çevrimiçi yardım için "help()" veya yardım bilgilerini içeren HTML tarayıcı arayüzü açmak için "help.start()" yazın.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-277">Type 'demo()' for some demos, 'help()' for on-line help, or 'help.start()' for an HTML browser interface to help.</span></span>
    <span data-ttu-id="2a3a8-278">R'den çıkmak için "q()" yazın.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-278">Type 'q()' to quit R.</span></span>

    <span data-ttu-id="2a3a8-279">Microsoft R Server sürüm 8.0: R Microsoft paketlerinin gelişmiş dağıtımı Telif Hakkı (C) 2016 Microsoft Corporation</span><span class="sxs-lookup"><span data-stu-id="2a3a8-279">Microsoft R Server version 8.0: an enhanced distribution of R  Microsoft packages Copyright (C) 2016 Microsoft Corporation</span></span>

    <span data-ttu-id="2a3a8-280">Sürüm notları için "readme()" yazın.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-280">Type 'readme()' for release notes.</span></span>
    >

3. <span data-ttu-id="2a3a8-281">`>` isteminde R kodunu girebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-281">From the `>` prompt, you can enter R code.</span></span> <span data-ttu-id="2a3a8-282">R server, Hadoop ile kolayca etkileşim kurup dağıtılmış hesaplamaları çalıştırmanıza olanak tanıyan paketler içerir.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-282">R server includes packages that allow you to easily interact with Hadoop and run distributed computations.</span></span> <span data-ttu-id="2a3a8-283">Örneğin, HDInsight kümesinin varsayılan dosya sisteminin kökünü görüntülemek için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="2a3a8-283">For example, use the following command to view the root of the default file system for the HDInsight cluster:</span></span>

    <span data-ttu-id="2a3a8-284">rxHadoopListFiles("/")</span><span class="sxs-lookup"><span data-stu-id="2a3a8-284">rxHadoopListFiles("/")</span></span>

4. <span data-ttu-id="2a3a8-285">WASB stil adreslemesini de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-285">You can also use the WASB style addressing.</span></span>

    <span data-ttu-id="2a3a8-286">rxHadoopListFiles("wasb:///")</span><span class="sxs-lookup"><span data-stu-id="2a3a8-286">rxHadoopListFiles("wasb:///")</span></span>


## <a name="using-r-server-on-hdi-from-a-remote-instance-of-microsoft-r-server-or-microsoft-r-client"></a><span data-ttu-id="2a3a8-287">Microsoft R Server veya Microsoft R Client uzak örneğinden HDI üzerinde R Server kullanma</span><span class="sxs-lookup"><span data-stu-id="2a3a8-287">Using R Server on HDI from a remote instance of Microsoft R Server or Microsoft R Client</span></span>

<span data-ttu-id="2a3a8-288">Masaüstü veya dizüstü bilgisayarda çalışan uzak Microsoft R Server veya Microsoft R Client örneğinden HDI Hadoop Spark işlem bağlamına erişim sağlamak mümkündür.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-288">It is possible to set up access to the HDI Hadoop Spark compute context from a remote instance of Microsoft R Server or Microsoft R Client running on a desktop or laptop.</span></span> <span data-ttu-id="2a3a8-289">[Spark için İşlem Bağlamı Oluşturma](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started.md) bölümündeki **Microsoft R Server'ı Hadoop İstemcisi Olarak Kullanma** alt bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-289">See **Using Microsoft R Server as a Hadoop Client** subsection in the [Creating a Compute Context for Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started.md).</span></span> <span data-ttu-id="2a3a8-290">Bunu yapmak için dizüstü bilgisayarınızda RxSpark işlem bağlamını tanımlarken şu seçenekleri belirtmeniz gerekir: hdfsShareDir, shareDir, sshUsername, sshHostname, sshSwitches ve sshProfileScript.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-290">To do so, you need to specify the following options when defining the RxSpark compute context on your laptop: hdfsShareDir, shareDir, sshUsername, sshHostname, sshSwitches, and sshProfileScript.</span></span> <span data-ttu-id="2a3a8-291">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="2a3a8-291">For example:</span></span>


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


## <a name="use-a-compute-context"></a><span data-ttu-id="2a3a8-292">İşlem bağlamı kullanma</span><span class="sxs-lookup"><span data-stu-id="2a3a8-292">Use a compute context</span></span>

<span data-ttu-id="2a3a8-293">Bir işlem bağlamı, hesaplamanın kenar düğümünde yerel olarak yapılmasını veya HDInsight kümesindeki düğümlere dağıtılmasını denetlemenize olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-293">A compute context allows you to control whether computation is performed locally on the edge node or distributed across the nodes in the HDInsight cluster.</span></span>

1. <span data-ttu-id="2a3a8-294">RStudio Server veya R konsolundan (bir SSH oturumunda), varsayılan HDInsight depolama alanına örnek verileri yüklemek için aşağıdaki kodu kullanın:</span><span class="sxs-lookup"><span data-stu-id="2a3a8-294">From RStudio Server or the R console (in an SSH session), use the following code to load example data into the default storage for HDInsight:</span></span>

        # Set the HDFS (WASB) location of example data
        bigDataDirRoot <- "/example/data"

        # create a local folder for storaging data temporarily
        source <- "/tmp/AirOnTimeCSV2012"
        dir.create(source)

        # Download data to the tmp folder
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

        # Set directory in bigDataDirRoot to load the data into
        inputDir <- file.path(bigDataDirRoot,"AirOnTimeCSV2012")

        # Make the directory
        rxHadoopMakeDir(inputDir)

        # Copy the data from source to input
        rxHadoopCopyFromLocal(source, bigDataDirRoot)

2. <span data-ttu-id="2a3a8-295">Bundan sonra, verilerle çalışabilmek için bazı veri bilgileri oluşturup iki veri kaynağı tanımlayabiliriz.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-295">Next, let's create some data info and define two data sources so that we can work with the data.</span></span>

        # Define the HDFS (WASB) file system
        hdfsFS <- RxHdfsFileSystem()

        # Create info list for the airline data
        airlineColInfo <- list(
             DAY_OF_WEEK = list(type = "factor"),
             ORIGIN = list(type = "factor"),
             DEST = list(type = "factor"),
             DEP_TIME = list(type = "integer"),
             ARR_DEL15 = list(type = "logical"))

        # get all the column names
        varNames <- names(airlineColInfo)

        # Define the text data source in hdfs
        airOnTimeData <- RxTextData(inputDir, colInfo = airlineColInfo, varsToKeep = varNames, fileSystem = hdfsFS)

        # Define the text data source in local system
        airOnTimeDataLocal <- RxTextData(source, colInfo = airlineColInfo, varsToKeep = varNames)

        # formula to use
        formula = "ARR_DEL15 ~ ORIGIN + DAY_OF_WEEK + DEP_TIME + DEST"

3. <span data-ttu-id="2a3a8-296">Yerel işlem bağlamını kullanarak, veriler üzerinde lojistik regresyon gerçekleştirelim.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-296">Let's run a logistic regression over the data using the local compute context.</span></span>

        # Set a local compute context
        rxSetComputeContext("local")

        # Run a logistic regression
        system.time(
           modelLocal <- rxLogit(formula, data = airOnTimeDataLocal)
        )

        # Display a summary
        summary(modelLocal)

    <span data-ttu-id="2a3a8-297">Aşağıdakilere benzer satırlarla sona eren bir çıktı görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="2a3a8-297">You should see output that ends with lines similar to the following:</span></span>

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

4. <span data-ttu-id="2a3a8-298">Şimdi de Spark bağlamını kullanarak aynı lojistik regresyonu gerçekleştirelim.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-298">Next, let's run the same logistic regression using the Spark context.</span></span> <span data-ttu-id="2a3a8-299">Spark bağlamı, işlemi HDInsight kümesindeki tüm çalışan düğümlerine dağıtır.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-299">The Spark context distributes the processing over all the worker nodes in the HDInsight cluster.</span></span>

        # Define the Spark compute context
        mySparkCluster <- RxSpark()

        # Set the compute context
        rxSetComputeContext(mySparkCluster)

        # Run a logistic regression
        system.time(  
           modelSpark <- rxLogit(formula, data = airOnTimeData)
        )
        
        # Display a summary
        summary(modelSpark)


   > [!NOTE]
   > <span data-ttu-id="2a3a8-300">Ayrıca, MapReduce kullanarak hesaplamayı küme düğümleri arasında dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-300">You can also use MapReduce to distribute computation across cluster nodes.</span></span> <span data-ttu-id="2a3a8-301">İşlem bağlamı hakkında daha fazla bilgi için bkz. [HDInsight üzerinde R Server için işlem bağlamı seçenekleri](hdinsight-hadoop-r-server-compute-contexts.md).</span><span class="sxs-lookup"><span data-stu-id="2a3a8-301">For more information on compute context, see [Compute context options for R Server on HDInsight](hdinsight-hadoop-r-server-compute-contexts.md).</span></span>


## <a name="distribute-r-code-to-multiple-nodes"></a><span data-ttu-id="2a3a8-302">R kodunu birden fazla düğüme dağıtma</span><span class="sxs-lookup"><span data-stu-id="2a3a8-302">Distribute R code to multiple nodes</span></span>

<span data-ttu-id="2a3a8-303">R Server ile mevcut R kodunu kolayca alabilir ve `rxExec` kullanarak kümedeki birden fazla düğümde çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-303">With R Server, you can easily take existing R code and run it across multiple nodes in the cluster by using `rxExec`.</span></span> <span data-ttu-id="2a3a8-304">Bu işlev bir parametre tarama veya benzetme işlemi sırasında yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-304">This function is useful when doing a parameter sweep or simulations.</span></span> <span data-ttu-id="2a3a8-305">`rxExec` kullanımını gösteren bir kod örneği aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="2a3a8-305">The following code is an example of how to use `rxExec`:</span></span>

    rxExec( function() {Sys.info()["nodename"]}, timesToRun = 4 )

<span data-ttu-id="2a3a8-306">Hala Spark veya MapReduce bağlamını kullanıyorsanız bu komut, üzerinde `(Sys.info()["nodename"])` kodunun çalıştığı çalışan düğümleri için nodename değerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-306">If you are still using the Spark or MapReduce context, this  command returns the nodename value for the worker nodes that the code `(Sys.info()["nodename"])` is run on.</span></span> <span data-ttu-id="2a3a8-307">Örneğin, dört düğümlü bir kümede aşağıdakine benzer bir çıktı beklenir:</span><span class="sxs-lookup"><span data-stu-id="2a3a8-307">For example, on a four node cluster, you expect to receive output similar to the following:</span></span>

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


## <a name="accessing-data-in-hive-and-parquet"></a><span data-ttu-id="2a3a8-308">Hive ve Parquet Verilerine Erişim</span><span class="sxs-lookup"><span data-stu-id="2a3a8-308">Accessing Data in Hive and Parquet</span></span>

<span data-ttu-id="2a3a8-309">R Server 9.1 sürümünde sunulan bir özellik, Spark işlem bağlamındaki ScaleR işlevleri tarafından kullanım için Hive ve Parquet içindeki verilere doğrudan erişime olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-309">A feature available in R Server 9.1 allows direct access to data in Hive and Parquet for use by ScaleR functions in the Spark compute context.</span></span> <span data-ttu-id="2a3a8-310">Bu özellikler, ScaleR tarafından analiz edilmek üzere bir Spart DataFrame’e doğrudan veri yüklemek için Spark SQL kullanarak çalışan RxHiveData ve RxParquetData adlı yeni ScaleR veri kaynağı işlevleriyle kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-310">These capabilities are available through new ScaleR data source functions called RxHiveData and RxParquetData that work through use of Spark SQL to load data directly into a Spark DataFrame for analysis by ScaleR.</span></span>  

<span data-ttu-id="2a3a8-311">Yeni işlevlerin kullanımına ilişkin bazı örnek kodlar aşağıdaki kod ile verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="2a3a8-311">The following code provides some sample code on use of the new functions:</span></span>

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

    #Check on Spark data objects, cleanup, and close the Spark session:
    lsObj <- rxSparkListData() # two data objs are cached
    lsObj
    rxSparkRemoveData(lsObj)
    rxSparkListData() # it should show empty list
    rxSparkDisconnect(myHadoopCluster)


<span data-ttu-id="2a3a8-312">Bu yeni işlevlerin kullanımına ilişkin ek bilgi için, `?RxHivedata` ve `?RxParquetData` komutlarını kullanarak R Server içindeki çevrimiçi yardıma bakın.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-312">For additional info on use of these new functions see the online help in R Server through use of the `?RxHivedata` and `?RxParquetData` commands.</span></span>  


## <a name="install-additional-r-packages-on-the-edge-node"></a><span data-ttu-id="2a3a8-313">Kenar düğümüne ek R paketleri yükleme</span><span class="sxs-lookup"><span data-stu-id="2a3a8-313">Install additional R packages on the edge node</span></span>

<span data-ttu-id="2a3a8-314">Kenar düğümüne ek R paketleri yüklemek isterseniz, SSH ile kenar düğümüne bağlı olduğunda doğrudan R konsolu içinden `install.packages()` kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-314">If you would like to install additional R packages on the edge node, you can use `install.packages()` directly from within the R console when connected to the edge node through SSH.</span></span> <span data-ttu-id="2a3a8-315">Ancak, kümenin çalışan düğümlerine R paketleri yüklemeniz gerekiyorsa bir Betik Eylemi kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-315">However, if you need to install R packages on the worker nodes of the cluster, you must use a Script Action.</span></span>

<span data-ttu-id="2a3a8-316">Betik Eylemleri, HDInsight kümesinde yapılandırma değişiklikleri yapmak veya ek R paketleri gibi ek yazılımlar yüklemek için kullanılan Bash betikleridir.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-316">Script Actions are Bash scripts that are used to make configuration changes to the HDInsight cluster or to install additional software, such as additional R packages.</span></span> <span data-ttu-id="2a3a8-317">Betik Eylemi kullanarak ek paketler yüklemek için aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="2a3a8-317">To install additional packages using a Script Action, use the following steps:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2a3a8-318">Ek R paketleri yüklemek için Betik Eylemleri yalnızca küme oluşturulduktan sonra kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-318">Using Script Actions to install additional R packages can only be used after the cluster has been created.</span></span> <span data-ttu-id="2a3a8-319">Betik R Server'ın tamamen yüklü ve yapılandırılmış olmasına bağlı olduğundan, bu yordamı küme oluşturma sırasında kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-319">Do not use this procedure during cluster creation, as the script relies on R Server being completely installed and configured.</span></span>
>
>

1. <span data-ttu-id="2a3a8-320">[Azure portalı](https://portal.azure.com)’ndan, HDInsight kümesindeki R Server’ınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-320">From the [Azure portal](https://portal.azure.com), select your R Server on HDInsight cluster.</span></span>

2. <span data-ttu-id="2a3a8-321">**Ayarlar** dikey penceresinde **Betik Eylemleri** ve ardından **Yeni Gönder**'i seçerek yeni Betik Eylemini gönderin.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-321">From the **Settings** blade, select **Script Actions** and then **Submit New** to submit a new Script Action.</span></span>

   ![Betik eylemleri dikey penceresinin görüntüsü](./media/hdinsight-hadoop-r-server-get-started/scriptaction.png)

3. <span data-ttu-id="2a3a8-323">**Betik eylemini gönder** dikey penceresinde aşağıdaki bilgileri sağlayın:</span><span class="sxs-lookup"><span data-stu-id="2a3a8-323">From the **Submit script action** blade, provide the following information:</span></span>

   * <span data-ttu-id="2a3a8-324">**Ad**: Betiği tanımlayan kolay ad</span><span class="sxs-lookup"><span data-stu-id="2a3a8-324">**Name**: A friendly name to identify this script</span></span>

   * <span data-ttu-id="2a3a8-325">**Bash betiği URI’si**: `http://mrsactionscripts.blob.core.windows.net/rpackages-v01/InstallRPackages.sh`</span><span class="sxs-lookup"><span data-stu-id="2a3a8-325">**Bash script URI**: `http://mrsactionscripts.blob.core.windows.net/rpackages-v01/InstallRPackages.sh`</span></span>

   * <span data-ttu-id="2a3a8-326">**Başlık**: Bu öğenin **işareti kaldırılmış** olmalıdır</span><span class="sxs-lookup"><span data-stu-id="2a3a8-326">**Head**: This item should be **unchecked**</span></span>

   * <span data-ttu-id="2a3a8-327">**Çalışan**: Bu öğe **işaretlenmiş** olmalıdır</span><span class="sxs-lookup"><span data-stu-id="2a3a8-327">**Worker**: This item should be **checked**</span></span>

   * <span data-ttu-id="2a3a8-328">**Kenar düğümleri**: Bu öğenin **işareti kaldırılmış** olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-328">**Edge nodes**: This item should be **unchecked**.</span></span>

   * <span data-ttu-id="2a3a8-329">**Zookeeper**: Bu öğenin **işareti kaldırılmış** olmalıdır</span><span class="sxs-lookup"><span data-stu-id="2a3a8-329">**Zookeeper**: This item should be **unchecked**</span></span>

   * <span data-ttu-id="2a3a8-330">**Parametreler**: Yüklenecek R paketleri.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-330">**Parameters**: The R packages to be installed.</span></span> <span data-ttu-id="2a3a8-331">Örneğin, `bitops stringr arules`</span><span class="sxs-lookup"><span data-stu-id="2a3a8-331">For example, `bitops stringr arules`</span></span>

   * <span data-ttu-id="2a3a8-332">**Bu betiği kalıcı yap...** : Bu öğe **İşaretlenmiş** olmalıdır</span><span class="sxs-lookup"><span data-stu-id="2a3a8-332">**Persist this script...**: This item should be **Checked**</span></span>  

   > [!NOTE]
   > 1. <span data-ttu-id="2a3a8-333">Varsayılan olarak, tüm R paketleri Microsoft MRAN deposunun yüklü olan R Server sürümüyle tutarlı bir anlık görüntüsünden yüklenir.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-333">By default, all R packages are installed from a snapshot of the Microsoft MRAN repository consistent with the version of R Server that has been installed.</span></span> <span data-ttu-id="2a3a8-334">Paketlerin daha yeni sürümlerini yüklemek istiyorsanız uyumsuzluk riskiyle karşı karşıya kalabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-334">If you want to install newer versions of packages, then there is some risk of incompatibility.</span></span> <span data-ttu-id="2a3a8-335">Ancak bu tür yüklemeleri paket listesinin ilk öğesi olarak `useCRAN` belirleyerek mümkün kılabilirsiniz, örneğin `useCRAN bitops, stringr, arules`.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-335">However this kind of install is possible by specifying `useCRAN` as the first element of the package list, for example `useCRAN bitops, stringr, arules`.</span></span>  
   > 2. <span data-ttu-id="2a3a8-336">Bazı R paketleri için ek Linux sistem kitaplıkları gerekir.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-336">Some R packages require additional Linux system libraries.</span></span> <span data-ttu-id="2a3a8-337">Kolaylık olması için en popüler 100 R paketi için gerekli olan bağımlılıklar önceden yüklenmiştir.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-337">For convenience, we have pre-installed the dependencies needed by the top 100 most popular R packages.</span></span> <span data-ttu-id="2a3a8-338">Ancak, yüklediğiniz R paketleri bunların dışında kitaplıklar gerektirirse, burada kullanılan temel betiği indirmeniz ve adımları ekleyerek sistem kitaplıklarını yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-338">However, if the R package(s) you install require libraries beyond these then you must download the base script used here and add steps to install the system libraries.</span></span> <span data-ttu-id="2a3a8-339">Ardından, değiştirilmiş betiği Azure depolama hizmetindeki ortak bir blob kapsayıcıya yüklemeniz ve değiştirilmiş betiği kullanarak paketleri yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-339">You must then upload the modified script to a public blob container in Azure storage and use the modified script to install the packages.</span></span>
   >    <span data-ttu-id="2a3a8-340">Betik Eylemleri geliştirme hakkında bilgi için bkz. [Betik Eylemi geliştirme](hdinsight-hadoop-script-actions-linux.md).</span><span class="sxs-lookup"><span data-stu-id="2a3a8-340">For more information on developing Script Actions, see [Script Action development](hdinsight-hadoop-script-actions-linux.md).</span></span>  
   >
   >

   ![Betik eylemi ekleme](./media/hdinsight-getting-started-with-r/submitscriptaction.png)

4. <span data-ttu-id="2a3a8-342">Betiği çalıştırmak için **Oluştur**’u seçin.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-342">Select **Create** to run the script.</span></span> <span data-ttu-id="2a3a8-343">Betik tamamlandıktan sonra R paketleri tüm çalışan düğümlerinde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-343">Once the script completes, the R packages are available on all worker nodes.</span></span>


## <a name="using-microsoft-r-server-operationalization"></a><span data-ttu-id="2a3a8-344">Microsoft R Server ile Kullanıma Hazır Hale Getirme</span><span class="sxs-lookup"><span data-stu-id="2a3a8-344">Using Microsoft R Server Operationalization</span></span>

<span data-ttu-id="2a3a8-345">Veri modellemesi tamamlandığında, tahminlerde bulunmak üzere modelinizi kullanıma hazır hale getirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-345">When your data modeling is complete, you can operationalize the model to make predictions.</span></span> <span data-ttu-id="2a3a8-346">Microsoft R Server ile kullanıma hazır hale getirme özelliğini yapılandırmak için aşağıdaki adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="2a3a8-346">To configure for Microsoft R Server operationalization, perform the following steps:</span></span>

<span data-ttu-id="2a3a8-347">İlk olarak, ssh’yi Kenar düğümüne gönderin.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-347">First, ssh into the Edge node.</span></span> <span data-ttu-id="2a3a8-348">Örneğin,</span><span class="sxs-lookup"><span data-stu-id="2a3a8-348">For example,</span></span> 

    ssh -L USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

<span data-ttu-id="2a3a8-349">Ssh kullandıktan sonra dizini değiştirip ilgili sürüme geçin dotnet dll dosyasına sudo uygulayın:</span><span class="sxs-lookup"><span data-stu-id="2a3a8-349">After using ssh, change directory for the relevant version and sudo the dotnet dll:</span></span> 

- <span data-ttu-id="2a3a8-350">Microsoft R Server 9.1 için:</span><span class="sxs-lookup"><span data-stu-id="2a3a8-350">For Microsoft R Server 9.1:</span></span>

    <span data-ttu-id="2a3a8-351">cd /usr/lib64/microsoft-r/rserver/o16n/9.1.0   sudo dotnet Microsoft.RServer.Utils.AdminUtil/Microsoft.RServer.Utils.AdminUtil.dll</span><span class="sxs-lookup"><span data-stu-id="2a3a8-351">cd /usr/lib64/microsoft-r/rserver/o16n/9.1.0   sudo dotnet Microsoft.RServer.Utils.AdminUtil/Microsoft.RServer.Utils.AdminUtil.dll</span></span>

- <span data-ttu-id="2a3a8-352">Microsoft R Server 9.0 için:</span><span class="sxs-lookup"><span data-stu-id="2a3a8-352">For Microsoft R Server 9.0:</span></span>

    <span data-ttu-id="2a3a8-353">cd /usr/lib64/microsoft-deployr/9.0.1   sudo dotnet Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll</span><span class="sxs-lookup"><span data-stu-id="2a3a8-353">cd /usr/lib64/microsoft-deployr/9.0.1   sudo dotnet Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll</span></span>

<span data-ttu-id="2a3a8-354">Microsoft R Server ile kullanıma hazır hale getirme özelliğini One-box yapılandırması ile yapılandırmak için aşağıdaki işlemleri yapın:</span><span class="sxs-lookup"><span data-stu-id="2a3a8-354">To configure Microsoft R Server operationalization with a One-box configuration do the following:</span></span>

1. <span data-ttu-id="2a3a8-355">"R Server'ı Kullanıma Hazır Hale Getirmek için Yapılandır" seçeneğini belirleyin</span><span class="sxs-lookup"><span data-stu-id="2a3a8-355">Select “Configure R Server for Operationalization”</span></span>
2. <span data-ttu-id="2a3a8-356">“A.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-356">Select “A.</span></span> <span data-ttu-id="2a3a8-357">One-box (web + işlem düğümleri)” öğesini seçin</span><span class="sxs-lookup"><span data-stu-id="2a3a8-357">One-box (web + compute nodes)”</span></span>
3. <span data-ttu-id="2a3a8-358">**Yönetici** kullanıcı için bir parola girin</span><span class="sxs-lookup"><span data-stu-id="2a3a8-358">Enter a password for the **admin** user</span></span>

![one box işlemi](./media/hdinsight-hadoop-r-server-get-started/admin-util-one-box-.png)

<span data-ttu-id="2a3a8-360">İsteğe bağlı bir adım olarak aşağıdaki şekilde bir tanılama testi çalıştırarak Tanılama denetimleri gerçekleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="2a3a8-360">As an optional step you can perform Diagnostic checks by running a diagnostic test as follows:</span></span>

1. <span data-ttu-id="2a3a8-361">“6.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-361">Select “6.</span></span> <span data-ttu-id="2a3a8-362">Tanılama testleri çalıştır” öğesini seçin</span><span class="sxs-lookup"><span data-stu-id="2a3a8-362">Run diagnostic tests”</span></span>
2. <span data-ttu-id="2a3a8-363">“A.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-363">Select “A.</span></span> <span data-ttu-id="2a3a8-364">Test yapılandırması” öğesini seçin</span><span class="sxs-lookup"><span data-stu-id="2a3a8-364">Test configuration”</span></span>
3. <span data-ttu-id="2a3a8-365">Kullanıcı adı olarak "admin" değerini ve önceki yapılandırma adımında belirtilen parolayı girin</span><span class="sxs-lookup"><span data-stu-id="2a3a8-365">Enter Username = “admin” and password from previous configuration step</span></span>
4. <span data-ttu-id="2a3a8-366">Genel Sistem Durumunu Onayla = başarılı</span><span class="sxs-lookup"><span data-stu-id="2a3a8-366">Confirm Overall Health = pass</span></span>
5. <span data-ttu-id="2a3a8-367">Yönetim Yardımcı Programından çıkın</span><span class="sxs-lookup"><span data-stu-id="2a3a8-367">Exit the Admin Utility</span></span>
6. <span data-ttu-id="2a3a8-368">SSH’den çıkın</span><span class="sxs-lookup"><span data-stu-id="2a3a8-368">Exit SSH</span></span>

![İşlem için tanılama](./media/hdinsight-hadoop-r-server-get-started/admin-util-diagnostics.png)


>[!NOTE]
><span data-ttu-id="2a3a8-370">**Spark’ta web hizmeti tüketilirken uzun gecikmeler**</span><span class="sxs-lookup"><span data-stu-id="2a3a8-370">**Long delays when consuming web service on Spark**</span></span>
>
><span data-ttu-id="2a3a8-371">Bir Spark işlem bağlamında mrsdeploy ile oluşturulmuş bir web hizmetini tüketmeye çalışırken uzun gecikmeler yaşıyorsanız bazı eksik klasörleri eklemeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-371">If you encounter long delays when trying to consume a web service created with mrsdeploy functions in a Spark compute context, you may need to add some missing folders.</span></span> <span data-ttu-id="2a3a8-372">Spark uygulaması mrsdeoploy işlevleri kullanılarak bir web hizmetinden çağrıldığında '*rserve2*' adlı bir kullanıcıya ait oluyor.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-372">The Spark application belongs to a user called '*rserve2*' whenever it is invoked from a web service using mrsdeploy functions.</span></span> <span data-ttu-id="2a3a8-373">Bu soruna geçici bir çözüm olarak:</span><span class="sxs-lookup"><span data-stu-id="2a3a8-373">To work around this issue:</span></span>

    # Create these required folders for user 'rserve2' in local and hdfs:

    hadoop fs -mkdir /user/RevoShare/rserve2
    hadoop fs -chmod 777 /user/RevoShare/rserve2

    mkdir /var/RevoShare/rserve2
    chmod 777 /var/RevoShare/rserve2


    # Next, create a new Spark compute context:
 
    rxSparkConnect(reset = TRUE)


<span data-ttu-id="2a3a8-374">Bu aşamada kullanıma hazır hale getirme yapılandırması tamamlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-374">At this stage, the configuration for Operationalization is complete.</span></span> <span data-ttu-id="2a3a8-375">Bundan sonra kenar düğümünde Kullanıma Hazır Hale Getirmeye bağlanmak üzere RClient üzerindeki "mrsdeploy" paketini kullanabilir ve [uzaktan yürütme](https://msdn.microsoft.com/microsoft-r/operationalize/remote-execution) ile [web hizmetleri](https://msdn.microsoft.com/microsoft-r/mrsdeploy/mrsdeploy-websrv-vignette) gibi özellikleri kullanmaya başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-375">Now you can use the ‘mrsdeploy’ package on your RClient to connect to the Operationalization on edge node and start using its features like [remote execution](https://msdn.microsoft.com/microsoft-r/operationalize/remote-execution) and [web-services](https://msdn.microsoft.com/microsoft-r/mrsdeploy/mrsdeploy-websrv-vignette).</span></span> <span data-ttu-id="2a3a8-376">Kümenizin bir sanal ağda ayarlanıp ayarlanmamasına bağlı olarak, SSH oturumu aracılığıyla bağlantı noktası iletme tüneli ayarlamanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-376">Depending on whether your cluster is set up on a virtual network or not, you may need to set up port forward tunneling through SSH login.</span></span> <span data-ttu-id="2a3a8-377">Aşağıdaki bölümlerde bu tüneli nasıl kuracağınız açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-377">The following sections explain how to set up this tunnel.</span></span>

### <a name="rserver-cluster-on-virtual-network"></a><span data-ttu-id="2a3a8-378">Sanal ağda RServer Kümesi</span><span class="sxs-lookup"><span data-stu-id="2a3a8-378">RServer Cluster on virtual network</span></span>

<span data-ttu-id="2a3a8-379">12800 numaralı bağlantı noktası üzerinden kenar düğümüne trafik akışına izin verdiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-379">Make sure you allow traffic through port 12800 to the edge node.</span></span> <span data-ttu-id="2a3a8-380">Bu şekilde, Kullanıma Hazır Hale Getirme özelliğine bağlanmak için kenar düğümünü kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-380">That way, you can use the edge node to connect to the Operationalization feature.</span></span>


    library(mrsdeploy)

    remoteLogin(
        deployr_endpoint = "http://[your-cluster-name]-ed-ssh.azurehdinsight.net:12800",
        username = "admin",
        password = "xxxxxxx"
    )


<span data-ttu-id="2a3a8-381">`remoteLogin()` kenar düğümüne bağlanamadığı halde kenar düğümüne SSH uygulayabiliyorsanız, 12800 numaralı bağlantı noktası üzerinde trafiğe izin veren kuralın doğru şekilde ayarlanıp ayarlanmadığını doğrulamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-381">If the `remoteLogin()` cannot connect to the edge node, but you can SSH to the edge node, then you need to verify whether the rule to allow traffic on port 12800 has been set properly or not.</span></span> <span data-ttu-id="2a3a8-382">Sorunla karşılaşmaya devam ederseniz, SSH üzerinden bağlantı noktası iletme tüneli oluşturarak bir geçici çözüm uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-382">If you continue to face the issue, you can work around it by setting up port forward tunneling through SSH.</span></span> <span data-ttu-id="2a3a8-383">Yönergeler için aşağıdaki bölüme bakın.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-383">For instructions, see the following section.</span></span>

### <a name="rserver-cluster-not-set-up-on-virtual-network"></a><span data-ttu-id="2a3a8-384">Sanal ağda RServer Kümesi ayarlanmamış</span><span class="sxs-lookup"><span data-stu-id="2a3a8-384">RServer Cluster not set up on virtual network</span></span>

<span data-ttu-id="2a3a8-385">Kümeniz sanal üzerinde ayarlanmamışsa veya sanal ağ üzerinden bağlantı kurma sorunları yaşıyorsanız, SSH bağlantı noktası iletme tünelini kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="2a3a8-385">If your cluster is not set up on vnet or if you are having troubles with connectivity through vnet, you can use SSH port forward tunneling:</span></span>

    ssh -L localhost:12800:localhost:12800 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

<span data-ttu-id="2a3a8-386">Putty üzerinde de bu ayarı yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-386">On Putty, you can set it up as well.</span></span>

![putty ssh bağlantısı](./media/hdinsight-hadoop-r-server-get-started/putty.png)

<span data-ttu-id="2a3a8-388">SSH oturumunuz etkin hale geldikten sonra, makinenizin 12800 numaralı bağlantı noktasından giden trafik, SSH aracılığıyla kenar düğümünün 12800 numaralı bağlantı noktasına iletilir.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-388">Once your SSH session is active, the traffic from your machine’s port 12800 is forwarded to the edge node’s port 12800 through SSH session.</span></span> <span data-ttu-id="2a3a8-389">`remoteLogin()` yönteminizde `127.0.0.1:12800` kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-389">Make sure you use `127.0.0.1:12800` in your `remoteLogin()` method.</span></span> <span data-ttu-id="2a3a8-390">Bunun yapılması, bağlantı noktası iletme yoluyla kenar düğümünün kullanıma hazır hale getirme özelliğinde oturum açar.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-390">This logs in to the edge node’s operationalization through port forwarding.</span></span>


    library(mrsdeploy)

    remoteLogin(
        deployr_endpoint = "http://127.0.0.1:12800",
        username = "admin",
        password = "xxxxxxx"
    )


## <a name="how-to-scale-microsoft-r-server-operationalization-compute-nodes-on-hdinsight-worker-nodes"></a><span data-ttu-id="2a3a8-391">HDInsight çalışan düğümlerinde Microsoft R Server Kullanıma Hazır Hale Getirme işlem düğümleri nasıl ölçeklendirilir?</span><span class="sxs-lookup"><span data-stu-id="2a3a8-391">How to scale Microsoft R Server Operationalization compute nodes on HDInsight worker nodes</span></span>

### <a name="decommission-the-worker-nodes"></a><span data-ttu-id="2a3a8-392">Çalışan düğümlerinin yetkisini alma</span><span class="sxs-lookup"><span data-stu-id="2a3a8-392">Decommission the worker node(s)</span></span>

<span data-ttu-id="2a3a8-393">Microsoft R Server şu anda Yarn üzerinden yönetilmemektedir.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-393">Microsoft R Server is currently not managed through Yarn.</span></span> <span data-ttu-id="2a3a8-394">Çalışan düğümlerinin yetkisi alınmazsa, Yarn Kaynak Yöneticisi sunucu tarafından alınan kaynakları fark edemeyeceği için beklendiği gibi çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-394">If the worker nodes are not decommissioned, the Yarn Resource Manager will not work as expected because it will not be aware of the resources being taken up by the server.</span></span> <span data-ttu-id="2a3a8-395">Bu durumu önlemek için, işlem düğümlerini ölçeklendirmeden önce çalışan düğümlerinin yetkisinin alınması önerilir.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-395">In order to avoid this situation, we recommend decommissioning the worker nodes before you scale out the compute nodes.</span></span>

<span data-ttu-id="2a3a8-396">Çalışan düğümlerinin yetkisini alma adımları:</span><span class="sxs-lookup"><span data-stu-id="2a3a8-396">Steps to decommissioning worker nodes:</span></span>

* <span data-ttu-id="2a3a8-397">HDI kümesinin Ambari konsolunda oturum açıp "ana bilgisayarlar" sekmesine tıklayın</span><span class="sxs-lookup"><span data-stu-id="2a3a8-397">Log in to HDI cluster's Ambari console and click on "hosts" tab</span></span>
* <span data-ttu-id="2a3a8-398">Çalışan düğümlerini (yetkisi alınacak olanlar) seçin, "Eylemler" > "Seçili Ana Bilgisayarlar" > "Ana Bilgisayarlar" > "Bakım Modunu Aç" öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-398">Select worker nodes (to be decommissioned), Click on "Actions" > "Selected Hosts" > "Hosts" > click on "Turn ON Maintenance Mode".</span></span> <span data-ttu-id="2a3a8-399">Örneğin, aşağıdaki görüntüde yetkisini almak üzere wn3 ve wn4 seçilmiştir.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-399">For example, in the following image we have selected wn3 and wn4 to decommission.</span></span>  

   ![çalışan düğümlerinin yetkisini alma](./media/hdinsight-hadoop-r-server-get-started/get-started-operationalization.png)  

* <span data-ttu-id="2a3a8-401">**Eylemler** > **Seçili Ana Bilgisayarlar** > **DataNodes** > öğesini seçip **Yetkisini Al** öğesine tıklayın</span><span class="sxs-lookup"><span data-stu-id="2a3a8-401">Select **Actions** > **Selected Hosts** > **DataNodes** > click **Decommission**</span></span>
* <span data-ttu-id="2a3a8-402">**Eylemler** > **Seçili Ana Bilgisayarlar** > **NodeManagers** > öğesini seçip **Yetkisini Al** öğesine tıklayın</span><span class="sxs-lookup"><span data-stu-id="2a3a8-402">Select **Actions** > **Selected Hosts** > **NodeManagers** > click **Decommission**</span></span>
* <span data-ttu-id="2a3a8-403">**Eylemler** > **Seçili Ana Bilgisayarlar** > **DataNodes** > öğesini seçip **Durdur** öğesine tıklayın</span><span class="sxs-lookup"><span data-stu-id="2a3a8-403">Select **Actions** > **Selected Hosts** > **DataNodes** > click **Stop**</span></span>
* <span data-ttu-id="2a3a8-404">**Eylemler** > **Seçili Ana Bilgisayarlar** > **NodeManagers** > öğesini seçip **Durdur** öğesine tıklayın</span><span class="sxs-lookup"><span data-stu-id="2a3a8-404">Select **Actions** > **Selected Hosts** > **NodeManagers** > click on **Stop**</span></span>
* <span data-ttu-id="2a3a8-405">**Eylemler** > **Seçili Ana Bilgisayarlar** > **Ana Bilgisayarlar** > öğesini seçip **Tüm Bileşenleri Durdur** öğesine tıklayın</span><span class="sxs-lookup"><span data-stu-id="2a3a8-405">Select **Actions** > **Selected Hosts** > **Hosts** > click **Stop All Components**</span></span>
* <span data-ttu-id="2a3a8-406">Çalışan düğümlerinin seçimini kaldırın ve baş düğümleri seçin</span><span class="sxs-lookup"><span data-stu-id="2a3a8-406">Unselect the worker nodes and select the head nodes</span></span>
* <span data-ttu-id="2a3a8-407">**Eylemler** > **Seçili Ana Bilgisayarlar** > **Ana Bilgisayarlar** > **Tüm Bileşenleri Yeniden Başlat** öğesini seçin</span><span class="sxs-lookup"><span data-stu-id="2a3a8-407">Select **Actions** > **Selected Hosts** > "**Hosts** > **Restart All Components**</span></span>

### <a name="configure-compute-nodes-on-each-decommissioned-worker-nodes"></a><span data-ttu-id="2a3a8-408">Yetkisi alınan her çalışan düğümü üzerinde İşlem düğümlerini yapılandırın</span><span class="sxs-lookup"><span data-stu-id="2a3a8-408">Configure Compute nodes on each decommissioned worker node(s)</span></span>

1. <span data-ttu-id="2a3a8-409">Yetkisi alınan her çalışan düğümüne SSH uygulayın.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-409">SSH into each decommissioned worker node.</span></span>
2. <span data-ttu-id="2a3a8-410">`dotnet /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll` kullanarak yönetici yardımcı programını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-410">Run admin utility using `dotnet /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll`.</span></span>
3. <span data-ttu-id="2a3a8-411">"R Server'ı Kullanıma Hazır Hale Getirmek için Yapılandır" seçeneğini belirlemek için "1" yazın.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-411">Enter "1" to select option "Configure R Server for Operationalization".</span></span>
4. <span data-ttu-id="2a3a8-412">"c" girerek "C.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-412">Enter "c" to select option "C.</span></span> <span data-ttu-id="2a3a8-413">İşlem düğümü" öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-413">Compute node".</span></span> <span data-ttu-id="2a3a8-414">Bu işlem çalışan düğümündeki işlem düğümünü yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-414">This configures the compute node on the worker node.</span></span>
5. <span data-ttu-id="2a3a8-415">Yönetim Yardımcı Programından çıkın.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-415">Exit the Admin Utility.</span></span>

### <a name="add-compute-nodes-details-on-web-node"></a><span data-ttu-id="2a3a8-416">Web Düğümüne işlem düğümleri ekleme</span><span class="sxs-lookup"><span data-stu-id="2a3a8-416">Add compute nodes details on Web Node</span></span>

<span data-ttu-id="2a3a8-417">Yetkisi alınan tüm çalışan düğümleri işlem düğümü üzerinde çalışacak şekilde yapılandırıldıktan sonra, kenar düğümüne geri dönün ve yetkisi alınmış çalışan düğümlerinin IP adreslerini Microsoft R Server web düğümünün yapılandırmasına ekleyin:</span><span class="sxs-lookup"><span data-stu-id="2a3a8-417">Once all decommissioned worker nodes have been configured to run compute node, come back on the edge node and add decommissioned worker nodes' IP addresses in the Microsoft R Server web node's configuration:</span></span>

* <span data-ttu-id="2a3a8-418">Kenar düğümüne SSH uygulayın.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-418">SSH into the edge node.</span></span>
* <span data-ttu-id="2a3a8-419">`vi /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Server.WebAPI/appsettings.json` öğesini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-419">Run `vi /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Server.WebAPI/appsettings.json`.</span></span>
* <span data-ttu-id="2a3a8-420">"URI’ler" bölümüne bakın ve çalışan düğümünün IP ve bağlantı noktası bilgilerini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-420">Look for the "URIs" section, and add worker node's IP and port details.</span></span>

    ![çalışan düğümlerinin yetkisini alma komut satırı](./media/hdinsight-hadoop-r-server-get-started/get-started-op-cmd.png)


## <a name="troubleshoot"></a><span data-ttu-id="2a3a8-422">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="2a3a8-422">Troubleshoot</span></span>

<span data-ttu-id="2a3a8-423">HDInsight kümeleri oluştururken sorun yaşarsanız bkz. [erişim denetimi gereksinimleri](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="2a3a8-423">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>


## <a name="next-steps"></a><span data-ttu-id="2a3a8-424">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2a3a8-424">Next steps</span></span>

<span data-ttu-id="2a3a8-425">R Server içeren yeni bir HDInsight kümesi oluşturmayı ve SSH oturumuyla R konsolunu kullanmanın temel adımlarını kavramış olmanız gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="2a3a8-425">Now you should understand how to create a new HDInsight cluster that includes the R Server and the basics of using the R console from an SSH session.</span></span> <span data-ttu-id="2a3a8-426">Aşağıdaki konularda HDInsight üzerinde R Server yönetimi ve çalışması için diğer yöntemler açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="2a3a8-426">The following topics explain other ways of managing and working with R Server on HDInsight:</span></span>

* [<span data-ttu-id="2a3a8-427">HDInsight’a RStudio Server Ekleme (küme oluşturma sırasında yüklenmediyse)</span><span class="sxs-lookup"><span data-stu-id="2a3a8-427">Add RStudio Server to HDInsight (if not installed during cluster creation)</span></span>](hdinsight-hadoop-r-server-install-r-studio.md)
* [<span data-ttu-id="2a3a8-428">HDInsight üzerinde R Server için işlem bağlamı seçenekleri</span><span class="sxs-lookup"><span data-stu-id="2a3a8-428">Compute context options for R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-compute-contexts.md)
* [<span data-ttu-id="2a3a8-429">HDInsight üzerinde R Server için Azure Depolama seçenekleri</span><span class="sxs-lookup"><span data-stu-id="2a3a8-429">Azure Storage options for R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-storage.md)
