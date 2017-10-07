---
title: "R Server hdınsight'ta - Azure ile Rstudio'dan aaaInstall | Microsoft Docs"
description: "Nasıl tooinstall Rstudio'dan hdınsight'ta R Server ile."
services: hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 918abb0d-8248-4bc5-98dc-089c0e007d49
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/19/2017
ms.author: bradsev
ms.openlocfilehash: b3a23021fcf99217e8f551f8b2e89bf1f1e5b967
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="installing-rstudio-with-r-server-on-hdinsight"></a><span data-ttu-id="f38b9-103">Hdınsight'ta R Server ile Rstudio'dan yükleme</span><span class="sxs-lookup"><span data-stu-id="f38b9-103">Installing RStudio with R Server on HDInsight</span></span>

<span data-ttu-id="f38b9-104">Nasıl tooinstall hello community (ücretsiz) sürümünü bu makalede [Rstudio'dan Server](https://www.rstudio.com/products/rstudio-server/) özel bir komut dosyası kullanarak bir kümesinin hello kenar düğümüne.</span><span class="sxs-lookup"><span data-stu-id="f38b9-104">This article describes how tooinstall hello community (free) version of [RStudio Server](https://www.rstudio.com/products/rstudio-server/) on hello edge node of a cluster using a custom script.</span></span> <span data-ttu-id="f38b9-105">Rstudio'dan sunucusu, uzak istemciler tarafından kullanılacak tarayıcı tabanlı bir IDE sağlar ve Linux üzerinde yaygın olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f38b9-105">RStudio Server provides a browser-based IDE for use by remote clients and is widely used on Linux.</span></span> <span data-ttu-id="f38b9-106">Dahil olmak üzere birden çok tümleşik geliştirme ortamı (IDE) R için kullanılabilir bugün vardır:</span><span class="sxs-lookup"><span data-stu-id="f38b9-106">There are multiple integrated development environments (IDEs) available for R today, including:</span></span>

- <span data-ttu-id="f38b9-107">Microsoft'un [R araçları Visual Studio için](https://www.visualstudio.com/en-us/features/rtvs-vs.aspx) (RTVS)</span><span class="sxs-lookup"><span data-stu-id="f38b9-107">Microsoft’s  [R Tools for Visual Studio](https://www.visualstudio.com/en-us/features/rtvs-vs.aspx) (RTVS)</span></span> 
- [<span data-ttu-id="f38b9-108">Rstudio'dan sunucu</span><span class="sxs-lookup"><span data-stu-id="f38b9-108">RStudio Server</span></span>](https://www.rstudio.com/products/rstudio-server/) 
- <span data-ttu-id="f38b9-109">Walware Eclipse tabanlı [StatET](http://www.walware.de/goto/statet).</span><span class="sxs-lookup"><span data-stu-id="f38b9-109">Walware’s Eclipse-based [StatET](http://www.walware.de/goto/statet).</span></span>

<span data-ttu-id="f38b9-110">Merhaba kenar düğümüne Hdınsight kümesi Rstudio'dan sunucusu yükleme hello avantajı, tam IDE deneyimi hello geliştirme ve R betiklerinin yürütülmesi için R Server ile Merhaba kümede sağlamasıdır.</span><span class="sxs-lookup"><span data-stu-id="f38b9-110">hello advantage of installing RStudio Server on hello edge node of an HDInsight cluster is that it provides a full IDE experience for hello development and execution of R scripts with R Server on hello cluster.</span></span> <span data-ttu-id="f38b9-111">Bu yapılandırma önemli ölçüde daha üretken hello R konsol varsayılan kullanımını olabilir.</span><span class="sxs-lookup"><span data-stu-id="f38b9-111">This configuration can be considerably more productive than default use of hello R Console.</span></span>

> [!NOTE]
> <span data-ttu-id="f38b9-112">Bu makalede açıklanan hello yordamı yalnızca kümeniz sağlamada tooinstall Rstudio'dan Server community edition seçmediğiniz geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="f38b9-112">hello procedure described in this article is only relevant if you did not select tooinstall RStudio Server community edition when provisioning your cluster.</span></span> <span data-ttu-id="f38b9-113">Sağlama işlemi sırasında eklediyseniz sonra onu tıklattığınız hello üzerinde tooaccess **R Server panolar** hello Azure portal giriş kümenizin sonra hello parçasında **R Studio Server** döşeme.</span><span class="sxs-lookup"><span data-stu-id="f38b9-113">If you added it during provisioning, then tooaccess it you click on hello **R Server Dashboards** tile in hello Azure portal entry for your cluster, then on hello **R Studio Server** tile.</span></span> 

<span data-ttu-id="f38b9-114">Toouse ticari lisanslı hello Pro Rstudio'dan Server sürümünü tercih ederseniz, hello yükleme yönergeleri izlemeniz gereken [Rstudio'dan Server](https://www.rstudio.com/products/rstudio/download-server/).</span><span class="sxs-lookup"><span data-stu-id="f38b9-114">If you prefer toouse hello commercially licensed Pro version of RStudio Server, you must follow hello installation instructions from [RStudio Server](https://www.rstudio.com/products/rstudio/download-server/).</span></span>

> [!NOTE]
> <span data-ttu-id="f38b9-115">İçin R yüklenen hello kullanarak bir Hdınsight kümesi kullanıyorsanız [yükleme R betik eylemi](hdinsight-hadoop-r-scripts-linux.md), hello adımları bu belgede çalışmaz doğru hello Hdınsight kümesinde bir R Server gerektirir.</span><span class="sxs-lookup"><span data-stu-id="f38b9-115">If you are using an HDInsight cluster for which R was installed using hello [Install R Script Action](hdinsight-hadoop-r-scripts-linux.md), hello steps in this document will not work correctly as they require an R Server on hello HDInsight cluster.</span></span>
>
> 

## <a name="prerequisites"></a><span data-ttu-id="f38b9-116">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="f38b9-116">Prerequisites</span></span>

* <span data-ttu-id="f38b9-117">Azure Hdınsight kümesi R Server yüklü.</span><span class="sxs-lookup"><span data-stu-id="f38b9-117">An Azure HDInsight cluster with R Server installed.</span></span> <span data-ttu-id="f38b9-118">Yönergeler için bkz: [Hdınsight kümelerinde R Server ile çalışmaya başlama](hdinsight-hadoop-r-server-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f38b9-118">For instructions, see [Get started with R Server on HDInsight clusters](hdinsight-hadoop-r-server-get-started.md).</span></span>
* <span data-ttu-id="f38b9-119">Bir SSH istemcisi.</span><span class="sxs-lookup"><span data-stu-id="f38b9-119">An SSH client.</span></span> <span data-ttu-id="f38b9-120">Linux ve UNIX dağıtımlarının ya da Macintosh OS X için hello `ssh` komutu hello işletim sistemiyle sağlanan.</span><span class="sxs-lookup"><span data-stu-id="f38b9-120">For Linux and Unix distributions or Macintosh OS X, hello `ssh` command is provided with hello operating system.</span></span> <span data-ttu-id="f38b9-121">Windows için öneririz [Cygwin](http://www.redhat.com/services/custom/cygwin/) hello ile [OpenSSH seçeneği](https://www.youtube.com/watch?v=CwYSvvGaiWU), veya [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span><span class="sxs-lookup"><span data-stu-id="f38b9-121">For Windows, we recommend [Cygwin](http://www.redhat.com/services/custom/cygwin/) with hello [OpenSSH option](https://www.youtube.com/watch?v=CwYSvvGaiWU), or [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>  

## <a name="install-rstudio-on-hello-cluster-using-a-custom-script"></a><span data-ttu-id="f38b9-122">Özel bir komut dosyası kullanarak hello kümede Rstudio'dan yüklemek</span><span class="sxs-lookup"><span data-stu-id="f38b9-122">Install RStudio on hello cluster using a custom script</span></span>

<span data-ttu-id="f38b9-123">Merhaba adımlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="f38b9-123">Here are hello steps:</span></span>

1. <span data-ttu-id="f38b9-124">Merhaba kenar düğümüne hello kümesinin tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="f38b9-124">Identify hello edge node of hello cluster.</span></span> <span data-ttu-id="f38b9-125">R Server ile bir Hdınsight kümesi için baş düğümü ve kenar düğümü için adlandırma kuralı hello aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="f38b9-125">For an HDInsight cluster with R Server, following is hello naming convention for head node and edge node.</span></span>
   * <span data-ttu-id="f38b9-126">Baş düğüm`CLUSTERNAME-ssh.azurehdinsight.net`</span><span class="sxs-lookup"><span data-stu-id="f38b9-126">Head node `CLUSTERNAME-ssh.azurehdinsight.net`</span></span>
   * <span data-ttu-id="f38b9-127">Kenar düğümüne`CLUSTERNAME-ed-ssh.azurehdinsight.net`</span><span class="sxs-lookup"><span data-stu-id="f38b9-127">Edge node `CLUSTERNAME-ed-ssh.azurehdinsight.net`</span></span> 

2. <span data-ttu-id="f38b9-128">1. adımda sağlanan hello adlandırma desenini kullanarak hello kümesinin hello kenar düğümüne içine SSH.</span><span class="sxs-lookup"><span data-stu-id="f38b9-128">SSH into hello edge node of hello cluster using hello naming pattern provided in step 1.</span></span> <span data-ttu-id="f38b9-129">Daha fazla bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="f38b9-129">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="f38b9-130">Bağlandıktan sonra kök kullanıcının hello kümede haline gelir.</span><span class="sxs-lookup"><span data-stu-id="f38b9-130">Once you are connected, become a root user on hello cluster.</span></span> <span data-ttu-id="f38b9-131">Merhaba SSH oturumunda hello aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="f38b9-131">In hello SSH session, use hello following command:</span></span>

        sudo su -

4. <span data-ttu-id="f38b9-132">Merhaba özel komut dosyası tooinstall Rstudio'dan indirin.</span><span class="sxs-lookup"><span data-stu-id="f38b9-132">Download hello custom script tooinstall RStudio.</span></span> <span data-ttu-id="f38b9-133">Merhaba aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="f38b9-133">Use hello following command:</span></span>

        wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/InstallRStudio.sh

5. <span data-ttu-id="f38b9-134">Merhaba özel komut dosyası Hello izinlerini değiştirin ve hello komut dosyasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="f38b9-134">Change hello permissions on hello custom script file and run hello script.</span></span> <span data-ttu-id="f38b9-135">Merhaba aşağıdaki komutları kullanın:</span><span class="sxs-lookup"><span data-stu-id="f38b9-135">Use hello following commands:</span></span>

        chmod 755 InstallRStudio.sh
        ./InstallRStudio.sh

6. <span data-ttu-id="f38b9-136">R Server ile bir Hdınsight kümesi oluştururken bir SSH parola kullandıysanız, bu adımı atlayın ve toohello sonraki devam edin.</span><span class="sxs-lookup"><span data-stu-id="f38b9-136">If you used an SSH password while creating an HDInsight cluster with R Server, you can skip this step and proceed toohello next.</span></span> <span data-ttu-id="f38b9-137">Bir SSH anahtarı toocreate hello küme yerine kullandıysanız, SSH kullanıcı için bir parola ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f38b9-137">If you used an SSH key instead toocreate hello cluster, you must set a password for your SSH user.</span></span> <span data-ttu-id="f38b9-138">Bu parolayı tooRStudio bağlanırken gerekir.</span><span class="sxs-lookup"><span data-stu-id="f38b9-138">You need this password when connecting tooRStudio.</span></span> <span data-ttu-id="f38b9-139">Merhaba aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="f38b9-139">Run hello following commands:</span></span>

        passwd USERNAME
        Current Kerberos password:
        New password:
        Retype new password:
        Current Kerberos password:


7. <span data-ttu-id="f38b9-140">İstendiğinde **geçerli Kerberos Parola**, basın **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="f38b9-140">When prompted for **Current Kerberos password**, press **ENTER**.</span></span>  <span data-ttu-id="f38b9-141">Değiştirmeniz gereken Not `USERNAME` Hdınsight kümenizle bir SSH kullanıcıyla.</span><span class="sxs-lookup"><span data-stu-id="f38b9-141">Note that you must replace `USERNAME` with an SSH user for your HDInsight cluster.</span></span> <span data-ttu-id="f38b9-142">Parolanızı başarıyla ayarlarsanız, iletiden hello görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="f38b9-142">If your password is successfully set, you should see hello following message:</span></span>

        passwd: password updated successfully

    <span data-ttu-id="f38b9-143">Merhaba SSH oturumu çıkın.</span><span class="sxs-lookup"><span data-stu-id="f38b9-143">Exit hello SSH session.</span></span>

8. <span data-ttu-id="f38b9-144">Eşleme tarafından bir SSH tünel toohello kümesi oluşturmayı `ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` toohello istemci makine üzerinde hello Hdınsight küme.</span><span class="sxs-lookup"><span data-stu-id="f38b9-144">Create an SSH tunnel toohello cluster by mapping `ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` on hello HDInsight cluster toohello client machine.</span></span> <span data-ttu-id="f38b9-145">Yeni bir tarayıcı oturum açmadan önce bir SSH tüneli oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f38b9-145">You must create an SSH tunnel before opening a new browser session.</span></span>

   * <span data-ttu-id="f38b9-146">Linux istemci veya bir Windows İstemcisi ile [Cygwin](http://www.redhat.com/services/custom/cygwin/), bir terminal oturumu açın ve hello aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="f38b9-146">On a Linux client or a Windows client with [Cygwin](http://www.redhat.com/services/custom/cygwin/), open a terminal session and use hello following command:</span></span>

             ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

       <span data-ttu-id="f38b9-147">Değiştir **kullanıcı adı** Hdınsight kümesi ve değiştirmek için bir SSH kullanıcıyla **CLUSTERNAME** Hdınsight kümenize hello adı.</span><span class="sxs-lookup"><span data-stu-id="f38b9-147">Replace **USERNAME** with an SSH user for your HDInsight cluster, and replace **CLUSTERNAME** with hello name of your HDInsight cluster.</span></span>
       <span data-ttu-id="f38b9-148">Ayrıca bir parola yerine bir SSH anahtarı ekleyerek kullanabileceğiniz `-i id_rsa_key`.</span><span class="sxs-lookup"><span data-stu-id="f38b9-148">You can also use an SSH key rather than a password by adding `-i id_rsa_key`.</span></span>        
   * <span data-ttu-id="f38b9-149">Windows İstemcisi ile PuTTY sonra kullanıyorsanız</span><span class="sxs-lookup"><span data-stu-id="f38b9-149">If using a Windows client with PuTTY then</span></span>

     1. <span data-ttu-id="f38b9-150">Putty'yi açın ve bağlantı bilgilerinizi girin.</span><span class="sxs-lookup"><span data-stu-id="f38b9-150">Open PuTTY, and enter your connection information.</span></span>
     2. <span data-ttu-id="f38b9-151">Merhaba, **kategori** bölüm toohello sol hello iletişim, genişletin **bağlantı**, genişletin **SSH**ve ardından **tüneller**.</span><span class="sxs-lookup"><span data-stu-id="f38b9-151">In hello **Category** section toohello left of hello dialog, expand **Connection**, expand **SSH**, and then select **Tunnels**.</span></span>
     3. <span data-ttu-id="f38b9-152">Merhaba üzerinde aşağıdaki bilgilerle hello sağlamak **SSH denetleme seçenekleri bağlantı noktası iletme** form:</span><span class="sxs-lookup"><span data-stu-id="f38b9-152">Provide hello following information on hello **Options controlling SSH port forwarding** form:</span></span>

        * <span data-ttu-id="f38b9-153">**Kaynak bağlantı noktası** -hello hello istemci tooforward istediğiniz bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="f38b9-153">**Source port** - hello port on hello client that you wish tooforward.</span></span> <span data-ttu-id="f38b9-154">Örneğin, **8787**.</span><span class="sxs-lookup"><span data-stu-id="f38b9-154">For example, **8787**.</span></span>
        * <span data-ttu-id="f38b9-155">**Hedef** - hello olmalıdır hedef toohello yerel istemci makine eşlenmiş.</span><span class="sxs-lookup"><span data-stu-id="f38b9-155">**Destination** - hello destination that must be mapped toohello local client machine.</span></span> <span data-ttu-id="f38b9-156">Örneğin, **localhost:8787**.</span><span class="sxs-lookup"><span data-stu-id="f38b9-156">For example, **localhost:8787**.</span></span>

            <span data-ttu-id="f38b9-157">![SSH tüneli oluşturma](./media/hdinsight-hadoop-r-server-install-r-studio/createsshtunnel.png "SSH tüneli oluşturma")</span><span class="sxs-lookup"><span data-stu-id="f38b9-157">![Create an SSH tunnel](./media/hdinsight-hadoop-r-server-install-r-studio/createsshtunnel.png "Create an SSH tunnel")</span></span>

     4. <span data-ttu-id="f38b9-158">Tıklatın **Ekle** tooadd hello ayarları ve ardından **açık** tooopen bir SSH bağlantısı.</span><span class="sxs-lookup"><span data-stu-id="f38b9-158">Click **Add** tooadd hello settings, and then click **Open** tooopen an SSH connection.</span></span>
     5. <span data-ttu-id="f38b9-159">İstendiğinde, toohello sunucu tooestablish SSH oturumu ve etkinleştir hello tüneli oturum açın.</span><span class="sxs-lookup"><span data-stu-id="f38b9-159">When prompted, log in toohello server tooestablish an SSH session and enable hello tunnel.</span></span>

9. <span data-ttu-id="f38b9-160">Bir web tarayıcısı açın ve hello bağlantı noktası için hello tünel girdiğiniz temel URL aşağıdaki hello girin:</span><span class="sxs-lookup"><span data-stu-id="f38b9-160">Open a web browser and enter hello following URL based on hello port you entered for hello tunnel:</span></span>

        http://localhost:8787/ 

10. <span data-ttu-id="f38b9-161">İstendiğinde tooenter hello SSH kullanıcı adı ve parola tooconnect toohello küme var.</span><span class="sxs-lookup"><span data-stu-id="f38b9-161">You are prompted tooenter hello SSH username and password tooconnect toohello cluster.</span></span> <span data-ttu-id="f38b9-162">Merhaba küme oluştururken bir SSH anahtarı kullandıysanız, 5. adımda oluşturduğunuz hello parola girmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f38b9-162">If you used an SSH key while creating hello cluster, you must enter hello password you created in step 5.</span></span>

    <span data-ttu-id="f38b9-163">![TooR Studio bağlanmak](./media/hdinsight-hadoop-r-server-install-r-studio/connecttostudio.png "SSH tüneli oluşturma")</span><span class="sxs-lookup"><span data-stu-id="f38b9-163">![Connect tooR Studio](./media/hdinsight-hadoop-r-server-install-r-studio/connecttostudio.png "Create an SSH tunnel")</span></span>

11. <span data-ttu-id="f38b9-164">tootest hello Rstudio'dan yükleme başarılı olup olmadığını R tabanlı MapReduce ve Spark işlerinin hello kümesinde yürütülür bir test betiğini çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f38b9-164">tootest whether hello RStudio installation was successful, you can run a test script that executes R-based MapReduce and Spark jobs on hello cluster.</span></span> <span data-ttu-id="f38b9-165">toodownload hello test betik toorun Rstudio'dan içinde toohello SSH konsol geri dönün ve aşağıdaki komutları hello girin:</span><span class="sxs-lookup"><span data-stu-id="f38b9-165">toodownload hello test script toorun in RStudio, go back toohello SSH console and enter hello following commands:</span></span>

    *    <span data-ttu-id="f38b9-166">R ile Hadoop kümesi oluşturduysanız, bu komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="f38b9-166">If you created a Hadoop cluster with R, use this command:</span></span>

            <span data-ttu-id="f38b9-167">wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi.r</span><span class="sxs-lookup"><span data-stu-id="f38b9-167">wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi.r</span></span>
    *    <span data-ttu-id="f38b9-168">R ile Spark kümesi oluşturduysanız, bu komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="f38b9-168">If you created a Spark cluster with R, use this command:</span></span>

            <span data-ttu-id="f38b9-169">wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi_spark.r</span><span class="sxs-lookup"><span data-stu-id="f38b9-169">wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi_spark.r</span></span>

12. <span data-ttu-id="f38b9-170">Rstudio'dan içinde indirdiğiniz betiğini sınamak hello bakın.</span><span class="sxs-lookup"><span data-stu-id="f38b9-170">In RStudio, you see hello test script you downloaded.</span></span> <span data-ttu-id="f38b9-171">Hello hello dosyasının içeriğini seçin ve ardından hello dosya tooopen çift **çalıştırmak**.</span><span class="sxs-lookup"><span data-stu-id="f38b9-171">Double-click hello file tooopen it, select hello contents of hello file, and then click **Run**.</span></span> <span data-ttu-id="f38b9-172">Merhaba hello çıktısında görmelisiniz **konsol** bölmesi:</span><span class="sxs-lookup"><span data-stu-id="f38b9-172">You should see hello output in hello **Console** pane:</span></span>

   <span data-ttu-id="f38b9-173">![Test hello yükleme](./media/hdinsight-hadoop-r-server-install-r-studio/test-r-script.png "Test hello yükleme")</span><span class="sxs-lookup"><span data-stu-id="f38b9-173">![Test hello installation](./media/hdinsight-hadoop-r-server-install-r-studio/test-r-script.png "Test hello installation")</span></span>

<span data-ttu-id="f38b9-174">Başka bir seçenek tootype olabilir `source(testhdi.r)` veya `source(testhdi_spark.r)` tooexecute hello komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="f38b9-174">Another option would be tootype `source(testhdi.r)` or `source(testhdi_spark.r)` tooexecute hello script.</span></span>

## <a name="see-also"></a><span data-ttu-id="f38b9-175">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="f38b9-175">See also</span></span>

* [<span data-ttu-id="f38b9-176">Hdınsight kümelerinde R Server için içerik seçeneklerini işlem</span><span class="sxs-lookup"><span data-stu-id="f38b9-176">Compute context options for R Server on HDInsight clusters</span></span>](hdinsight-hadoop-r-server-compute-contexts.md)
* [<span data-ttu-id="f38b9-177">HDInsight üzerinde R Server için Azure Depolama seçenekleri</span><span class="sxs-lookup"><span data-stu-id="f38b9-177">Azure Storage options for R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-storage.md)

