---
title: "R Server hdınsight'ta - Azure ile Rstudio'dan yükleme | Microsoft Docs"
description: "Rstudio'dan hdınsight'ta R Server ile yükleme."
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
ms.openlocfilehash: 416420d855505508735ebd8526e93efdb230ad53
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="installing-rstudio-with-r-server-on-hdinsight"></a><span data-ttu-id="ee2fa-103">Hdınsight'ta R Server ile Rstudio'dan yükleme</span><span class="sxs-lookup"><span data-stu-id="ee2fa-103">Installing RStudio with R Server on HDInsight</span></span>

<span data-ttu-id="ee2fa-104">Bu makalede community (ücretsiz) sürümünü yüklemek nasıl [Rstudio'dan Server](https://www.rstudio.com/products/rstudio-server/) özel bir komut dosyası kullanarak bir küme kenar düğümü üzerinde.</span><span class="sxs-lookup"><span data-stu-id="ee2fa-104">This article describes how to install the community (free) version of [RStudio Server](https://www.rstudio.com/products/rstudio-server/) on the edge node of a cluster using a custom script.</span></span> <span data-ttu-id="ee2fa-105">Rstudio'dan sunucusu, uzak istemciler tarafından kullanılacak tarayıcı tabanlı bir IDE sağlar ve Linux üzerinde yaygın olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ee2fa-105">RStudio Server provides a browser-based IDE for use by remote clients and is widely used on Linux.</span></span> <span data-ttu-id="ee2fa-106">Dahil olmak üzere birden çok tümleşik geliştirme ortamı (IDE) R için kullanılabilir bugün vardır:</span><span class="sxs-lookup"><span data-stu-id="ee2fa-106">There are multiple integrated development environments (IDEs) available for R today, including:</span></span>

- <span data-ttu-id="ee2fa-107">Microsoft'un [R araçları Visual Studio için](https://www.visualstudio.com/en-us/features/rtvs-vs.aspx) (RTVS)</span><span class="sxs-lookup"><span data-stu-id="ee2fa-107">Microsoft’s  [R Tools for Visual Studio](https://www.visualstudio.com/en-us/features/rtvs-vs.aspx) (RTVS)</span></span> 
- [<span data-ttu-id="ee2fa-108">Rstudio'dan sunucu</span><span class="sxs-lookup"><span data-stu-id="ee2fa-108">RStudio Server</span></span>](https://www.rstudio.com/products/rstudio-server/) 
- <span data-ttu-id="ee2fa-109">Walware Eclipse tabanlı [StatET](http://www.walware.de/goto/statet).</span><span class="sxs-lookup"><span data-stu-id="ee2fa-109">Walware’s Eclipse-based [StatET](http://www.walware.de/goto/statet).</span></span>

<span data-ttu-id="ee2fa-110">Hdınsight kümesi kenar düğümüne Rstudio'dan sunucusu yükleme gibi bir avantajı, tam IDE Deneyimi Geliştirme ve R betiklerinin yürütülmesi için R sunucusuyla kümede sağlamasıdır.</span><span class="sxs-lookup"><span data-stu-id="ee2fa-110">The advantage of installing RStudio Server on the edge node of an HDInsight cluster is that it provides a full IDE experience for the development and execution of R scripts with R Server on the cluster.</span></span> <span data-ttu-id="ee2fa-111">Bu yapılandırma önemli ölçüde daha üretken R konsol varsayılan kullanımını olabilir.</span><span class="sxs-lookup"><span data-stu-id="ee2fa-111">This configuration can be considerably more productive than default use of the R Console.</span></span>

> [!NOTE]
> <span data-ttu-id="ee2fa-112">Bu makalede açıklanan yordam, yalnızca kümenizi sağlamada Rstudio'dan Server community sürümü yüklemek için seçmediyseniz geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="ee2fa-112">The procedure described in this article is only relevant if you did not select to install RStudio Server community edition when provisioning your cluster.</span></span> <span data-ttu-id="ee2fa-113">Sağlama işlemi sırasında eklenen sonra erişmek için tıklatılan **R Server panolar** kutucuğunu, kümeniz için Azure portal girişi sonra **R Studio Server** döşeme.</span><span class="sxs-lookup"><span data-stu-id="ee2fa-113">If you added it during provisioning, then to access it you click on the **R Server Dashboards** tile in the Azure portal entry for your cluster, then on the **R Studio Server** tile.</span></span> 

<span data-ttu-id="ee2fa-114">Ticari olarak lisanslı Pro Server sürümü Rstudio'dan kullanmayı tercih ederseniz, yükleme yönergeleri izlemeniz gereken [Rstudio'dan Server](https://www.rstudio.com/products/rstudio/download-server/).</span><span class="sxs-lookup"><span data-stu-id="ee2fa-114">If you prefer to use the commercially licensed Pro version of RStudio Server, you must follow the installation instructions from [RStudio Server](https://www.rstudio.com/products/rstudio/download-server/).</span></span>

> [!NOTE]
> <span data-ttu-id="ee2fa-115">İçin R yüklenen kullanarak bir Hdınsight kümesi kullanıyorsanız [yükleme R betik eylemi](hdinsight-hadoop-r-scripts-linux.md), bu belgede yer alan adımlar çalışmaz doğru Hdınsight kümesinde bir R Server gerektirir.</span><span class="sxs-lookup"><span data-stu-id="ee2fa-115">If you are using an HDInsight cluster for which R was installed using the [Install R Script Action](hdinsight-hadoop-r-scripts-linux.md), the steps in this document will not work correctly as they require an R Server on the HDInsight cluster.</span></span>
>
> 

## <a name="prerequisites"></a><span data-ttu-id="ee2fa-116">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="ee2fa-116">Prerequisites</span></span>

* <span data-ttu-id="ee2fa-117">Azure Hdınsight kümesi R Server yüklü.</span><span class="sxs-lookup"><span data-stu-id="ee2fa-117">An Azure HDInsight cluster with R Server installed.</span></span> <span data-ttu-id="ee2fa-118">Yönergeler için bkz: [Hdınsight kümelerinde R Server ile çalışmaya başlama](hdinsight-hadoop-r-server-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ee2fa-118">For instructions, see [Get started with R Server on HDInsight clusters](hdinsight-hadoop-r-server-get-started.md).</span></span>
* <span data-ttu-id="ee2fa-119">Bir SSH istemcisi.</span><span class="sxs-lookup"><span data-stu-id="ee2fa-119">An SSH client.</span></span> <span data-ttu-id="ee2fa-120">Linux ve UNIX dağıtımlarının veya Macintosh OS X için `ssh` komutu, işletim sistemiyle birlikte sağlanır.</span><span class="sxs-lookup"><span data-stu-id="ee2fa-120">For Linux and Unix distributions or Macintosh OS X, the `ssh` command is provided with the operating system.</span></span> <span data-ttu-id="ee2fa-121">Windows için öneririz [Cygwin](http://www.redhat.com/services/custom/cygwin/) ile [OpenSSH seçeneği](https://www.youtube.com/watch?v=CwYSvvGaiWU), veya [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span><span class="sxs-lookup"><span data-stu-id="ee2fa-121">For Windows, we recommend [Cygwin](http://www.redhat.com/services/custom/cygwin/) with the [OpenSSH option](https://www.youtube.com/watch?v=CwYSvvGaiWU), or [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>  

## <a name="install-rstudio-on-the-cluster-using-a-custom-script"></a><span data-ttu-id="ee2fa-122">Özel bir komut dosyası kullanarak kümede Rstudio'dan yüklemek</span><span class="sxs-lookup"><span data-stu-id="ee2fa-122">Install RStudio on the cluster using a custom script</span></span>

<span data-ttu-id="ee2fa-123">Adımlar aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="ee2fa-123">Here are the steps:</span></span>

1. <span data-ttu-id="ee2fa-124">Kümenin kenar düğümüne tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="ee2fa-124">Identify the edge node of the cluster.</span></span> <span data-ttu-id="ee2fa-125">R Server ile bir Hdınsight kümesi için baş düğümü ve kenar düğümü için adlandırma kuralı aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ee2fa-125">For an HDInsight cluster with R Server, following is the naming convention for head node and edge node.</span></span>
   * <span data-ttu-id="ee2fa-126">Baş düğüm`CLUSTERNAME-ssh.azurehdinsight.net`</span><span class="sxs-lookup"><span data-stu-id="ee2fa-126">Head node `CLUSTERNAME-ssh.azurehdinsight.net`</span></span>
   * <span data-ttu-id="ee2fa-127">Kenar düğümüne`CLUSTERNAME-ed-ssh.azurehdinsight.net`</span><span class="sxs-lookup"><span data-stu-id="ee2fa-127">Edge node `CLUSTERNAME-ed-ssh.azurehdinsight.net`</span></span> 

2. <span data-ttu-id="ee2fa-128">1. adımda sağlanan adlandırma desenini kullanarak küme kenar düğümüne içine SSH.</span><span class="sxs-lookup"><span data-stu-id="ee2fa-128">SSH into the edge node of the cluster using the naming pattern provided in step 1.</span></span> <span data-ttu-id="ee2fa-129">Daha fazla bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="ee2fa-129">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="ee2fa-130">Bağlandıktan sonra küme üzerinde bir kök kullanıcı haline gelir.</span><span class="sxs-lookup"><span data-stu-id="ee2fa-130">Once you are connected, become a root user on the cluster.</span></span> <span data-ttu-id="ee2fa-131">SSH oturumunda aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="ee2fa-131">In the SSH session, use the following command:</span></span>

        sudo su -

4. <span data-ttu-id="ee2fa-132">Rstudio'dan yüklemek için özel bir komut dosyası yükleyin.</span><span class="sxs-lookup"><span data-stu-id="ee2fa-132">Download the custom script to install RStudio.</span></span> <span data-ttu-id="ee2fa-133">Aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="ee2fa-133">Use the following command:</span></span>

        wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/InstallRStudio.sh

5. <span data-ttu-id="ee2fa-134">Özel komut dosyası izinleri değiştirmek ve betiği çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ee2fa-134">Change the permissions on the custom script file and run the script.</span></span> <span data-ttu-id="ee2fa-135">Aşağıdaki komutları kullanın:</span><span class="sxs-lookup"><span data-stu-id="ee2fa-135">Use the following commands:</span></span>

        chmod 755 InstallRStudio.sh
        ./InstallRStudio.sh

6. <span data-ttu-id="ee2fa-136">R Server ile bir Hdınsight kümesi oluştururken bir SSH parola kullandıysanız, bu adımı atlayın ve sonraki devam edin.</span><span class="sxs-lookup"><span data-stu-id="ee2fa-136">If you used an SSH password while creating an HDInsight cluster with R Server, you can skip this step and proceed to the next.</span></span> <span data-ttu-id="ee2fa-137">Bir SSH anahtarı yerine küme oluşturmak için kullandıysanız, SSH kullanıcı için bir parola ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ee2fa-137">If you used an SSH key instead to create the cluster, you must set a password for your SSH user.</span></span> <span data-ttu-id="ee2fa-138">Bu parola için Rstudio'dan bağlanırken gerekir.</span><span class="sxs-lookup"><span data-stu-id="ee2fa-138">You need this password when connecting to RStudio.</span></span> <span data-ttu-id="ee2fa-139">Aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="ee2fa-139">Run the following commands:</span></span>

        passwd USERNAME
        Current Kerberos password:
        New password:
        Retype new password:
        Current Kerberos password:


7. <span data-ttu-id="ee2fa-140">İstendiğinde **geçerli Kerberos Parola**, basın **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="ee2fa-140">When prompted for **Current Kerberos password**, press **ENTER**.</span></span>  <span data-ttu-id="ee2fa-141">Değiştirmeniz gereken Not `USERNAME` Hdınsight kümenizle bir SSH kullanıcıyla.</span><span class="sxs-lookup"><span data-stu-id="ee2fa-141">Note that you must replace `USERNAME` with an SSH user for your HDInsight cluster.</span></span> <span data-ttu-id="ee2fa-142">Parolanızı başarıyla ayarlarsanız, şu iletiyi görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="ee2fa-142">If your password is successfully set, you should see the following message:</span></span>

        passwd: password updated successfully

    <span data-ttu-id="ee2fa-143">SSH oturumu çıkın.</span><span class="sxs-lookup"><span data-stu-id="ee2fa-143">Exit the SSH session.</span></span>

8. <span data-ttu-id="ee2fa-144">Eşleme tarafından kümeye SSH tüneli oluşturma `ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` istemci makineye Hdınsight kümesinde.</span><span class="sxs-lookup"><span data-stu-id="ee2fa-144">Create an SSH tunnel to the cluster by mapping `ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` on the HDInsight cluster to the client machine.</span></span> <span data-ttu-id="ee2fa-145">Yeni bir tarayıcı oturum açmadan önce bir SSH tüneli oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ee2fa-145">You must create an SSH tunnel before opening a new browser session.</span></span>

   * <span data-ttu-id="ee2fa-146">Linux istemci veya bir Windows İstemcisi ile [Cygwin](http://www.redhat.com/services/custom/cygwin/), bir terminal oturumu açın ve aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="ee2fa-146">On a Linux client or a Windows client with [Cygwin](http://www.redhat.com/services/custom/cygwin/), open a terminal session and use the following command:</span></span>

             ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

       <span data-ttu-id="ee2fa-147">Değiştir **kullanıcıadı** Hdınsight kümesi ve değiştirmek için bir SSH kullanıcıyla **CLUSTERNAME** Hdınsight kümenizin adıyla.</span><span class="sxs-lookup"><span data-stu-id="ee2fa-147">Replace **USERNAME** with an SSH user for your HDInsight cluster, and replace **CLUSTERNAME** with the name of your HDInsight cluster.</span></span>
       <span data-ttu-id="ee2fa-148">Ayrıca bir parola yerine bir SSH anahtarı ekleyerek kullanabileceğiniz `-i id_rsa_key`.</span><span class="sxs-lookup"><span data-stu-id="ee2fa-148">You can also use an SSH key rather than a password by adding `-i id_rsa_key`.</span></span>        
   * <span data-ttu-id="ee2fa-149">Windows İstemcisi ile PuTTY sonra kullanıyorsanız</span><span class="sxs-lookup"><span data-stu-id="ee2fa-149">If using a Windows client with PuTTY then</span></span>

     1. <span data-ttu-id="ee2fa-150">Putty'yi açın ve bağlantı bilgilerinizi girin.</span><span class="sxs-lookup"><span data-stu-id="ee2fa-150">Open PuTTY, and enter your connection information.</span></span>
     2. <span data-ttu-id="ee2fa-151">İçinde **kategori** iletişim kutusunun solundaki bölümünde, genişletmek **bağlantı**, genişletin **SSH**ve ardından **tüneller**.</span><span class="sxs-lookup"><span data-stu-id="ee2fa-151">In the **Category** section to the left of the dialog, expand **Connection**, expand **SSH**, and then select **Tunnels**.</span></span>
     3. <span data-ttu-id="ee2fa-152">Üzerinde aşağıdaki bilgileri sağlayın **SSH denetleme seçenekleri bağlantı noktası iletme** form:</span><span class="sxs-lookup"><span data-stu-id="ee2fa-152">Provide the following information on the **Options controlling SSH port forwarding** form:</span></span>

        * <span data-ttu-id="ee2fa-153">**Kaynak bağlantı noktası** - İletmek istediğiniz istemci üzerindeki bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="ee2fa-153">**Source port** - The port on the client that you wish to forward.</span></span> <span data-ttu-id="ee2fa-154">Örneğin, **8787**.</span><span class="sxs-lookup"><span data-stu-id="ee2fa-154">For example, **8787**.</span></span>
        * <span data-ttu-id="ee2fa-155">**Hedef** -yerel istemci makineye eşlenmelidir hedef.</span><span class="sxs-lookup"><span data-stu-id="ee2fa-155">**Destination** - The destination that must be mapped to the local client machine.</span></span> <span data-ttu-id="ee2fa-156">Örneğin, **localhost:8787**.</span><span class="sxs-lookup"><span data-stu-id="ee2fa-156">For example, **localhost:8787**.</span></span>

            <span data-ttu-id="ee2fa-157">![SSH tüneli oluşturma](./media/hdinsight-hadoop-r-server-install-r-studio/createsshtunnel.png "SSH tüneli oluşturma")</span><span class="sxs-lookup"><span data-stu-id="ee2fa-157">![Create an SSH tunnel](./media/hdinsight-hadoop-r-server-install-r-studio/createsshtunnel.png "Create an SSH tunnel")</span></span>

     4. <span data-ttu-id="ee2fa-158">Tıklatın **Ekle** ayarları ekleyin ve ardından **açmak** bir SSH bağlantısı açılamıyor.</span><span class="sxs-lookup"><span data-stu-id="ee2fa-158">Click **Add** to add the settings, and then click **Open** to open an SSH connection.</span></span>
     5. <span data-ttu-id="ee2fa-159">İstendiğinde, bir SSH oturumu oluşturur ve tüneli etkinleştirmek için sunucuya oturum açın.</span><span class="sxs-lookup"><span data-stu-id="ee2fa-159">When prompted, log in to the server to establish an SSH session and enable the tunnel.</span></span>

9. <span data-ttu-id="ee2fa-160">Bir web tarayıcısı açın ve için tünel girdiğiniz bağlantı noktası göre aşağıdaki URL'yi girin:</span><span class="sxs-lookup"><span data-stu-id="ee2fa-160">Open a web browser and enter the following URL based on the port you entered for the tunnel:</span></span>

        http://localhost:8787/ 

10. <span data-ttu-id="ee2fa-161">SSH kullanıcı adı ve kümeye bağlanmak için parola girmeniz istenir.</span><span class="sxs-lookup"><span data-stu-id="ee2fa-161">You are prompted to enter the SSH username and password to connect to the cluster.</span></span> <span data-ttu-id="ee2fa-162">Küme oluştururken bir SSH anahtarı kullandıysanız, 5. adımda oluşturduğunuz parola girmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ee2fa-162">If you used an SSH key while creating the cluster, you must enter the password you created in step 5.</span></span>

    <span data-ttu-id="ee2fa-163">![R Studio'ya bağlanın](./media/hdinsight-hadoop-r-server-install-r-studio/connecttostudio.png "SSH tüneli oluşturma")</span><span class="sxs-lookup"><span data-stu-id="ee2fa-163">![Connect to R Studio](./media/hdinsight-hadoop-r-server-install-r-studio/connecttostudio.png "Create an SSH tunnel")</span></span>

11. <span data-ttu-id="ee2fa-164">Rstudio'dan yüklemenin başarılı olup olmadığını sınamak için küme üzerinde R tabanlı MapReduce ve Spark işlerini yürütür test betiğini çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ee2fa-164">To test whether the RStudio installation was successful, you can run a test script that executes R-based MapReduce and Spark jobs on the cluster.</span></span> <span data-ttu-id="ee2fa-165">Rstudio'dan içinde çalıştırmak için test komut dosyasını indirmek için SSH konsola geri dönün ve aşağıdaki komutları girin:</span><span class="sxs-lookup"><span data-stu-id="ee2fa-165">To download the test script to run in RStudio, go back to the SSH console and enter the following commands:</span></span>

    *    <span data-ttu-id="ee2fa-166">R ile Hadoop kümesi oluşturduysanız, bu komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="ee2fa-166">If you created a Hadoop cluster with R, use this command:</span></span>

            <span data-ttu-id="ee2fa-167">wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi.r</span><span class="sxs-lookup"><span data-stu-id="ee2fa-167">wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi.r</span></span>
    *    <span data-ttu-id="ee2fa-168">R ile Spark kümesi oluşturduysanız, bu komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="ee2fa-168">If you created a Spark cluster with R, use this command:</span></span>

            <span data-ttu-id="ee2fa-169">wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi_spark.r</span><span class="sxs-lookup"><span data-stu-id="ee2fa-169">wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi_spark.r</span></span>

12. <span data-ttu-id="ee2fa-170">Rstudio'dan içinde indirdiğiniz test komut dosyasına bakın.</span><span class="sxs-lookup"><span data-stu-id="ee2fa-170">In RStudio, you see the test script you downloaded.</span></span> <span data-ttu-id="ee2fa-171">Açmak, dosyanın içeriğini seçin ve ardından dosyasına çift tıklayarak **çalıştırmak**.</span><span class="sxs-lookup"><span data-stu-id="ee2fa-171">Double-click the file to open it, select the contents of the file, and then click **Run**.</span></span> <span data-ttu-id="ee2fa-172">Bir çıktı görmeniz gerekir **konsol** bölmesi:</span><span class="sxs-lookup"><span data-stu-id="ee2fa-172">You should see the output in the **Console** pane:</span></span>

   <span data-ttu-id="ee2fa-173">![Yükleme testi](./media/hdinsight-hadoop-r-server-install-r-studio/test-r-script.png "Test yüklemesi")</span><span class="sxs-lookup"><span data-stu-id="ee2fa-173">![Test the installation](./media/hdinsight-hadoop-r-server-install-r-studio/test-r-script.png "Test the installation")</span></span>

<span data-ttu-id="ee2fa-174">Türü için başka bir seçenek olabilir `source(testhdi.r)` veya `source(testhdi_spark.r)` komut dosyası yürütme.</span><span class="sxs-lookup"><span data-stu-id="ee2fa-174">Another option would be to type `source(testhdi.r)` or `source(testhdi_spark.r)` to execute the script.</span></span>

## <a name="see-also"></a><span data-ttu-id="ee2fa-175">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="ee2fa-175">See also</span></span>

* [<span data-ttu-id="ee2fa-176">Hdınsight kümelerinde R Server için içerik seçeneklerini işlem</span><span class="sxs-lookup"><span data-stu-id="ee2fa-176">Compute context options for R Server on HDInsight clusters</span></span>](hdinsight-hadoop-r-server-compute-contexts.md)
* [<span data-ttu-id="ee2fa-177">HDInsight üzerinde R Server için Azure Depolama seçenekleri</span><span class="sxs-lookup"><span data-stu-id="ee2fa-177">Azure Storage options for R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-storage.md)

