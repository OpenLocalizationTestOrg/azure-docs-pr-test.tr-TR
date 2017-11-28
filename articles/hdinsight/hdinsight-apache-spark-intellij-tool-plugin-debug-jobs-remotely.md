---
title: "aaaAzure Intellij - Hdınsight Spark üzerinde uzaktan hata ayıklama uygulamalar için araç seti | Microsoft Docs"
description: "Bilgi nasıl vpn aracılığıyla Hdınsight Spark kümeleri üzerinde çalışan Intellij tooremotely hata ayıklama uygulamaları için Azure araç setindeki Hdınsight araçlarını kullanın."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 55fb454f-c7dc-46de-a978-e242e9a94f4c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: ad67d23bf609d0a7afb38b2acb110062f8b27b39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-toolkit-for-intellij-toodebug-applications-remotely-on-hdinsight-spark-through-vpn"></a><span data-ttu-id="a4b8c-103">VPN üzerinden Hdınsight Spark üzerinde uzaktan Intellij toodebug uygulamalar için Azure araç kullanma</span><span class="sxs-lookup"><span data-stu-id="a4b8c-103">Use Azure Toolkit for IntelliJ toodebug applications remotely on HDInsight Spark through VPN</span></span>

<span data-ttu-id="a4b8c-104">Spark applicaltion uzaktan ile ssh ayıklama hello şekilde öneririz.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-104">We recommend hello way of debugging spark applicaltion remotely through ssh.</span></span> <span data-ttu-id="a4b8c-105">Yönergeler için bkz: [SSH aracılığıyla Intellij için Hdınsight kümesinde Azure araç seti ile Spark uygulamalarında uzaktan hata ayıklama](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).</span><span class="sxs-lookup"><span data-stu-id="a4b8c-105">For instructions, see [Remotely debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).</span></span>

<span data-ttu-id="a4b8c-106">Bu makalede, nasıl toouse Intellij toosubmit Hdınsight Spark kümesi üzerinde Spark iş için Hdınsight araçları Azure Araç Seti hello ve masaüstü bilgisayarınızdan uzaktan debug hakkında adım adım yönergeler sağlar.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-106">This article provides step-by-step guidance on how toouse hello HDInsight Tools in Azure Toolkit for IntelliJ toosubmit a Spark job on HDInsight Spark cluster and then debug it remotely from your desktop computer.</span></span> <span data-ttu-id="a4b8c-107">toodo bu nedenle, aşağıdaki üst düzey adımları hello gerçekleştirmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="a4b8c-107">toodo so, you must perform hello following high-level steps:</span></span>

1. <span data-ttu-id="a4b8c-108">Siteden siteye veya noktadan siteye Azure sanal ağı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-108">Create a site-to-site or point-to-site Azure Virtual Network.</span></span> <span data-ttu-id="a4b8c-109">Bu belgedeki Hello adımlar bir siteden siteye ağ kullandığınızı varsayar.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-109">hello steps in this document assume that you use a site-to-site network.</span></span>
2. <span data-ttu-id="a4b8c-110">Merhaba-siteye Azure sanal ağı parçası olan Azure Hdınsight'ta Spark kümesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-110">Create a Spark cluster in Azure HDInsight that is part of hello site-to-site Azure Virtual Network.</span></span>
3. <span data-ttu-id="a4b8c-111">Merhaba küme headnode ve masaüstünüzü arasında Hello bağlanabildiğini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-111">Verify hello connectivity between hello cluster headnode and your desktop.</span></span>
4. <span data-ttu-id="a4b8c-112">Intellij Idea Scala uygulama oluşturun ve uzaktan hata ayıklama için yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-112">Create a Scala application in IntelliJ IDEA and configure it for remote debugging.</span></span>
5. <span data-ttu-id="a4b8c-113">Merhaba uygulamada hata ayıklama ve çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-113">Run and debug hello application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a4b8c-114">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="a4b8c-114">Prerequisites</span></span>
* <span data-ttu-id="a4b8c-115">Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-115">An Azure subscription.</span></span> <span data-ttu-id="a4b8c-116">Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="a4b8c-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="a4b8c-117">Hdınsight'ta bir Apache Spark kümesi.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="a4b8c-118">Yönergeler için bkz: [Azure Hdınsight'ta Apache Spark oluşturmak kümeleri](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="a4b8c-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
* <span data-ttu-id="a4b8c-119">Oracle Java Geliştirme Seti.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-119">Oracle Java Development kit.</span></span> <span data-ttu-id="a4b8c-120">Şuradan yükleyebilirsiniz [burada](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="a4b8c-120">You can install it from [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
* <span data-ttu-id="a4b8c-121">Intellij Idea.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-121">IntelliJ IDEA.</span></span> <span data-ttu-id="a4b8c-122">Bu makalede sürümünü 2017.1 kullanır.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-122">This article uses version 2017.1.</span></span> <span data-ttu-id="a4b8c-123">Şuradan yükleyebilirsiniz [burada](https://www.jetbrains.com/idea/download/).</span><span class="sxs-lookup"><span data-stu-id="a4b8c-123">You can install it from [here](https://www.jetbrains.com/idea/download/).</span></span>
* <span data-ttu-id="a4b8c-124">Azure Araç Seti Intellij için Hdınsight araçları.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-124">HDInsight Tools in Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="a4b8c-125">Intellij için Hdınsight araçları kullanılabilir hello Intellij için Azure araç seti bir parçası olarak.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-125">HDInsight tools for IntelliJ are available as part of hello Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="a4b8c-126">Nasıl tooinstall hello Azure araç seti ile ilgili yönergeler için bkz: [yükleme hello Intellij için Azure Araç Seti](../azure-toolkit-for-intellij-installation.md).</span><span class="sxs-lookup"><span data-stu-id="a4b8c-126">For instructions on how tooinstall hello Azure Toolkit, see [Installing hello Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md).</span></span>
* <span data-ttu-id="a4b8c-127">Intellij Idea Azure aboneliğinizden günlüğüne.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-127">Log into your Azure Subscription from IntelliJ IDEA.</span></span> <span data-ttu-id="a4b8c-128">Merhaba yönergeleri izleyerek [burada](hdinsight-apache-spark-intellij-tool-plugin.md).</span><span class="sxs-lookup"><span data-stu-id="a4b8c-128">Follow hello instructions [here](hdinsight-apache-spark-intellij-tool-plugin.md).</span></span>
* <span data-ttu-id="a4b8c-129">Bir Windows bilgisayarda uzaktan hata ayıklama için Spark Scala uygulama çalışırken, bir özel durum açıklandığı gibi alabilirsiniz [SPARK 2356](https://issues.apache.org/jira/browse/SPARK-2356) tooa eksik nedeniyle oluşan Windows WinUtils.exe.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-129">While running Spark Scala application for remote debugging on a Windows computer, you might get an exception as explained in [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356) that occurs due tooa missing WinUtils.exe on Windows.</span></span> <span data-ttu-id="a4b8c-130">Bu hata geçici toowork, şunları yapmalısınız [hello yürütülebilir buradan indirin](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) tooa konumu ister **C:\WinUtils\bin**.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-130">toowork around this error, you must [download hello executable from here](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) tooa location like **C:\WinUtils\bin**.</span></span> <span data-ttu-id="a4b8c-131">Bir ortam değişkeni sonra eklemelisiniz **HADOOP_HOME** ve çok hello hello değişkenin değerini ayarlamak**C\WinUtils**.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-131">You must then add an environment variable **HADOOP_HOME** and set hello value of hello variable too**C\WinUtils**.</span></span>

## <a name="step-1-create-an-azure-virtual-network"></a><span data-ttu-id="a4b8c-132">1. adım: Azure sanal ağı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a4b8c-132">Step 1: Create an Azure Virtual Network</span></span>
<span data-ttu-id="a4b8c-133">Bağlantılar toocreate bir Azure sanal ağı aşağıda hello Hello yönergeleri takip ederek ve hello Masaüstü ve Azure sanal ağ arasında hello bağlantısını kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-133">Follow hello instructions from hello below links toocreate an Azure Virtual Network and then verify hello connectivity between hello desktop and Azure Virtual Network.</span></span>

* [<span data-ttu-id="a4b8c-134">Azure Portal kullanarak siteden siteye VPN bağlantısı olan bir VNet oluşturma</span><span class="sxs-lookup"><span data-stu-id="a4b8c-134">Create a VNet with a site-to-site VPN connection using Azure Portal</span></span>](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)
* [<span data-ttu-id="a4b8c-135">PowerShell kullanarak siteden siteye VPN bağlantısı olan bir VNet oluşturma</span><span class="sxs-lookup"><span data-stu-id="a4b8c-135">Create a VNet with a site-to-site VPN connection using PowerShell</span></span>](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)
* [<span data-ttu-id="a4b8c-136">PowerShell kullanarak bir noktadan siteye bağlantı tooa sanal bir ağ yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a4b8c-136">Configure a point-to-site connection tooa virtual network using PowerShell</span></span>](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

## <a name="step-2-create-an-hdinsight-spark-cluster"></a><span data-ttu-id="a4b8c-137">2. adım: bir Hdınsight Spark kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="a4b8c-137">Step 2: Create an HDInsight Spark cluster</span></span>
<span data-ttu-id="a4b8c-138">Merhaba, oluşturduğunuz Azure Virtual Network parçası olan Azure Hdınsight'ta Apache Spark kümesi da oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-138">You should also create an Apache Spark cluster on Azure HDInsight that is part of hello Azure Virtual Network that you created.</span></span> <span data-ttu-id="a4b8c-139">Merhaba bilgileri adresinde kullanın [Hdınsight oluşturma Linux tabanlı kümelerde](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="a4b8c-139">Use hello information available at [Create Linux-based clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="a4b8c-140">İsteğe bağlı yapılandırmasının bir parçası olarak hello hello önceki adımda oluşturduğunuz Azure sanal ağı seçin.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-140">As part of optional configuration, select hello Azure Virtual Network that you created in hello previous step.</span></span>

## <a name="step-3-verify-hello-connectivity-between-hello-cluster-headnode-and-your-desktop"></a><span data-ttu-id="a4b8c-141">Adım 3: hello küme headnode ve masaüstünüzü arasında hello bağlantısını doğrulama</span><span class="sxs-lookup"><span data-stu-id="a4b8c-141">Step 3: Verify hello connectivity between hello cluster headnode and your desktop</span></span>
1. <span data-ttu-id="a4b8c-142">Merhaba headnode Hello IP adresini alın.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-142">Get hello IP address of hello headnode.</span></span> <span data-ttu-id="a4b8c-143">Ambari UI hello küme için açın.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-143">Open Ambari UI for hello cluster.</span></span> <span data-ttu-id="a4b8c-144">Merhaba küme dikey penceresinden tıklayın **Pano**.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-144">From hello cluster blade, click **Dashboard**.</span></span>

    ![Headnode IP Bul](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/launch-ambari-ui.png)
2. <span data-ttu-id="a4b8c-146">Merhaba sağ üst köşesinden hello Ambari UI'ı tıklatın **ana**.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-146">From hello Ambari UI, from hello top-right corner, click **Hosts**.</span></span>

    ![Headnode IP Bul](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/ambari-hosts.png)
3. <span data-ttu-id="a4b8c-148">Headnodes, çalışan düğümleri ve zookeeper düğümleri listesini görmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-148">You should see a list of headnodes, worker nodes, and zookeeper nodes.</span></span> <span data-ttu-id="a4b8c-149">Merhaba headnodes sahip hello **hn*** öneki.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-149">hello headnodes have hello **hn*** prefix.</span></span> <span data-ttu-id="a4b8c-150">Merhaba ilk headnode'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-150">Click hello first headnode.</span></span>

    ![Headnode IP Bul](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/cluster-headnodes.png)
4. <span data-ttu-id="a4b8c-152">Açılır ve hello hello sayfanın hello sonundaki **Özet** kutusunda kopyalama hello IP adresi hello headnode ve hello ana bilgisayar adı.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-152">At hello bottom of hello page that opens, from hello **Summary** box, copy hello IP address of hello headnode and hello host name.</span></span>

    ![Headnode IP Bul](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/headnode-ip-address.png)
5. <span data-ttu-id="a4b8c-154">Başlangıç IP adresi ve hello headnode toohello hello ana bilgisayar adını içeren **ana** nerede toorun istediğiniz ve hello Spark işleri uzaktan hata ayıklama hello bilgisayarda dosya.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-154">Include hello IP address and hello host name of hello headnode toohello **hosts** file on hello computer from where you want toorun and remotely debug hello Spark jobs.</span></span> <span data-ttu-id="a4b8c-155">Bu, toocommunicate ile başlangıç IP adresi gibi hello ana bilgisayar adı kullanarak hello headnode olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-155">This will enable you toocommunicate with hello headnode using hello IP address as well as hello hostname.</span></span>

   1. <span data-ttu-id="a4b8c-156">Yükseltilmiş izinleri olan bir Not Defteri'ni açın.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-156">Open a notepad with elevated permissions.</span></span> <span data-ttu-id="a4b8c-157">Merhaba Dosya menüsünde tıklatın **açık** ve hello hosts dosyasını toohello konumuna gidin.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-157">From hello file menu, click **Open** and then navigate toohello location of hello hosts file.</span></span> <span data-ttu-id="a4b8c-158">Bir Windows bilgisayarda olmasından `C:\Windows\System32\Drivers\etc\hosts`.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-158">On a Windows computer, it is `C:\Windows\System32\Drivers\etc\hosts`.</span></span>
   2. <span data-ttu-id="a4b8c-159">Toohello aşağıdaki hello eklemek **ana** dosyası.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-159">Add hello following toohello **hosts** file.</span></span>

           # For headnode0
           192.xxx.xx.xx hn0-nitinp
           192.xxx.xx.xx hn0-nitinp.lhwwghjkpqejawpqbwcdyp3.gx.internal.cloudapp.net

           # For headnode1
           192.xxx.xx.xx hn1-nitinp
           192.xxx.xx.xx hn1-nitinp.lhwwghjkpqejawpqbwcdyp3.gx.internal.cloudapp.net
6. <span data-ttu-id="a4b8c-160">Toohello hello Hdınsight küme tarafından kullanılan Azure Virtual Network bağlı hello bilgisayardan hello IP adresi gibi hello ana bilgisayar adı kullanarak her iki hello headnodes ping atabildiğinizi doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-160">From hello computer that you connected toohello Azure Virtual Network that is used by hello HDInsight cluster, verify that you can ping both hello headnodes using hello IP address as well as hello hostname.</span></span>
7. <span data-ttu-id="a4b8c-161">Merhaba yönergeleri kullanarak hello küme headnode içine SSH [SSH kullanarak bağlan tooan Hdınsight kümesi](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="a4b8c-161">SSH into hello cluster headnode using hello instructions at [Connect tooan HDInsight cluster using SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span> <span data-ttu-id="a4b8c-162">Merhaba küme headnode hello masaüstü bilgisayar hello IP adresine ping komutu.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-162">From hello cluster headnode, ping hello IP address of hello desktop computer.</span></span> <span data-ttu-id="a4b8c-163">Bağlantı tooboth hello IP adreslerini hello ağ bağlantısı için bir tane toohello bilgisayar atanan test etmeniz gerekir ve hello hello bilgisayar hello Azure sanal ağ için diğer bağlı.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-163">You should test connectivity tooboth hello IP addresses assigned toohello computer, one for hello network connection and hello other for hello Azure Virtual Network that hello computer is connected to.</span></span>
8. <span data-ttu-id="a4b8c-164">Merhaba adımları da diğer headnode hello için yineleyin.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-164">Repeat hello steps for hello other headnode as well.</span></span>

## <a name="step-4-create-a-spark-scala-application-using-hello-hdinsight-tools-in-azure-toolkit-for-intellij-and-configure-it-for-remote-debugging"></a><span data-ttu-id="a4b8c-165">4. adım: Intellij için Azure araç setindeki hello Hdınsight araçları kullanarak Spark Scala uygulama oluşturma ve uzaktan hata ayıklama için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a4b8c-165">Step 4: Create a Spark Scala application using hello HDInsight Tools in Azure Toolkit for IntelliJ and configure it for remote debugging</span></span>
1. <span data-ttu-id="a4b8c-166">Intellij Idea başlatın ve yeni bir proje oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-166">Launch IntelliJ IDEA and create a new project.</span></span> <span data-ttu-id="a4b8c-167">Merhaba yeni proje iletişim kutusunda, aşağıdaki seçimleri hello ve ardından olun **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-167">In hello new project dialog box, make hello following choices, and then click **Next**.</span></span>

    ![Spark Scala uygulaması oluşturma](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-hdi-scala-app.png)

   * <span data-ttu-id="a4b8c-169">Merhaba sol bölmeden seçin **Hdınsight**.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-169">From hello left pane, select **HDInsight**.</span></span>
   * <span data-ttu-id="a4b8c-170">Merhaba sağ bölmeden seçin **(Scala) hdınsight'ta Spark**.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-170">From hello right pane, select **Spark on HDInsight (Scala)**.</span></span>
   * <span data-ttu-id="a4b8c-171">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-171">Click **Next**.</span></span>
2. <span data-ttu-id="a4b8c-172">Proje ayrıntılarını aşağıdaki hello Hello sonraki penceresinde sağlayın ve ardından **son**.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-172">In hello next window, provide hello following project details, and then click **Finish**.</span></span>  
   - <span data-ttu-id="a4b8c-173">Bir proje adı ve proje konumunu belirtin.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-173">Provide a project name and project location.</span></span>
   - <span data-ttu-id="a4b8c-174">İçin **proje SDK**, spark 2.x küme, Java 1.7 spark 1.x kümesi için kullanım Java 1.8.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-174">For **Project SDK**, Use Java 1.8 for spark 2.x cluster, Java 1.7 for spark 1.x cluster.</span></span>
   - <span data-ttu-id="a4b8c-175">İçin **Spark sürüm**, Scala Proje Oluşturma Sihirbazı'nı Spark SDK ve Scala SDK için uygun sürüm tümleştirir.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-175">For **Spark Version**, Scala project creation wizard integrates proper version for Spark SDK and Scala SDK.</span></span> <span data-ttu-id="a4b8c-176">Merhaba spark küme sürümü alt 2.0 ise seçmeniz 1.x spark.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-176">If hello spark cluster version is lower 2.0, choose spark 1.x.</span></span> <span data-ttu-id="a4b8c-177">Aksi takdirde spark2.x seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-177">Otherwise, you should select spark2.x.</span></span> <span data-ttu-id="a4b8c-178">Bu örnek Spark2.0.2 (Scala 2.11.8) kullanır.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-178">This example uses Spark2.0.2(Scala 2.11.8).</span></span>
       <span data-ttu-id="a4b8c-179">![Spark Scala uygulaması oluşturma](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-scala-project-details.png)</span><span class="sxs-lookup"><span data-stu-id="a4b8c-179">![Create Spark Scala application](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-scala-project-details.png)</span></span>
  
3. <span data-ttu-id="a4b8c-180">Merhaba Spark proje bir yapı sizin için otomatik olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-180">hello Spark project will automatically create an artifact for you.</span></span> <span data-ttu-id="a4b8c-181">toosee hello yapı, şu adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-181">toosee hello artifact, follow these steps.</span></span>

   1. <span data-ttu-id="a4b8c-182">Merhaba gelen **dosya** menüsünde tıklatın **proje yapısını**.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-182">From hello **File** menu, click **Project Structure**.</span></span>
   2. <span data-ttu-id="a4b8c-183">Merhaba, **Proje yapısı** iletişim kutusu, tıklatın **yapıları** oluşturulan toosee hello varsayılan yapı.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-183">In hello **Project Structure** dialog box, click **Artifacts** toosee hello default artifact that is created.</span></span>
   <span data-ttu-id="a4b8c-184">![JAR oluşturma](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/default-artifact.png)</span><span class="sxs-lookup"><span data-stu-id="a4b8c-184">![Create JAR](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/default-artifact.png)</span></span>

      <span data-ttu-id="a4b8c-185">Kendi yapı oluşturabilirsiniz hello üzerinde tıklatarak bly  **+**  yukarıdaki hello görüntü vurgulanmış simgesi.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-185">You can also create your own artifact bly clicking on hello **+** icon, highlighted in hello image above.</span></span>

4. <span data-ttu-id="a4b8c-186">Kitaplıkları tooyour projeye ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-186">Add libraries tooyour project.</span></span> <span data-ttu-id="a4b8c-187">bir kitaplık tooadd hello proje ağacında hello proje adına sağ tıklayın ve ardından **açık modülü ayarları**.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-187">tooadd a library, right-click hello project name in hello project tree, and then click **Open Module Settings**.</span></span> <span data-ttu-id="a4b8c-188">Merhaba, **proje yapısını** hello sol bölmesinde, iletişim kutusu **kitaplıkları**hello (+) simgesine tıklayın ve ardından **gelen Maven**.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-188">In hello **Project Structure** dialog box, from hello left pane, click **Libraries**, click hello (+) symbol, and then click **From Maven**.</span></span>

    ![Kitaplığı ekleyin](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/add-library.png)

    <span data-ttu-id="a4b8c-190">Merhaba, **Uzaktan Yükleme Kitaplığı Maven depodan** iletişim kutusuna, aramak ve kitaplıkları aşağıdaki hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-190">In hello **Download Library from Maven Repository** dialog box, search and add hello following libraries.</span></span>

   * `org.scalatest:scalatest_2.10:2.2.1`
   * `org.apache.hadoop:hadoop-azure:2.7.1`
5. <span data-ttu-id="a4b8c-191">Kopya `yarn-site.xml` ve `core-site.xml` hello gelen headnode küme ve toohello proje ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-191">Copy `yarn-site.xml` and `core-site.xml` from hello cluster headnode and add it toohello project.</span></span> <span data-ttu-id="a4b8c-192">Aşağıdaki komutları toocopy hello dosyaları hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-192">Use hello following commands toocopy hello files.</span></span> <span data-ttu-id="a4b8c-193">Kullanabileceğiniz [Cygwin](https://cygwin.com/install.html) toorun hello aşağıdaki `scp` toocopy hello hello küme headnodes dosyalarından komutları.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-193">You can use [Cygwin](https://cygwin.com/install.html) toorun hello following `scp` commands toocopy hello files from hello cluster headnodes.</span></span>

        scp <ssh user name>@<headnode IP address or host name>://etc/hadoop/conf/core-site.xml .

    <span data-ttu-id="a4b8c-194">Zaten hello küme headnode IP adresi ve ana bilgisayar adları fo hello hosts dosyasını hello masaüstünde eklediğimiz olduğundan, biz hello kullanabilirsiniz **scp** hello şekilde aşağıdaki komutlarda.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-194">Because we already added hello cluster headnode IP address and hostnames fo hello hosts file on hello desktop, we can use hello **scp** commands in hello following manner.</span></span>

        scp sshuser@hn0-nitinp:/etc/hadoop/conf/core-site.xml .
        scp sshuser@hn0-nitinp:/etc/hadoop/conf/yarn-site.xml .

    <span data-ttu-id="a4b8c-195">Merhaba altında kopyalayarak bu dosyaları tooyour projesi eklemek **/src** , proje ağacında, örneğin klasör `<your project directory>\src`.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-195">Add these files tooyour project by copying them under hello **/src** folder in your project tree, for example `<your project directory>\src`.</span></span>
6. <span data-ttu-id="a4b8c-196">Güncelleştirme hello `core-site.xml` toomake hello aşağıdaki değişiklikler.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-196">Update hello `core-site.xml` toomake hello following changes.</span></span>

   1. <span data-ttu-id="a4b8c-197">`core-site.xml`Merhaba kümesi ile ilişkili hello şifrelenmiş anahtar toohello depolama hesabını içerir.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-197">`core-site.xml` includes hello encrypted key toohello storage account associated with hello cluster.</span></span> <span data-ttu-id="a4b8c-198">Merhaba, `core-site.xml` toohello projesi Değiştir hello şifrelenmiş anahtar hello varsayılan depolama hesabıyla ilişkili hello gerçek depolama anahtarı eklendi.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-198">In hello `core-site.xml` that you added toohello project, replace hello encrypted key with hello actual storage key associated with hello default storage account.</span></span> <span data-ttu-id="a4b8c-199">Bkz: [depolama erişim tuşlarınızı yönetme](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="a4b8c-199">See [Manage your storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>

           <property>
                 <name>fs.azure.account.key.hdistoragecentral.blob.core.windows.net</name>
                 <value>access-key-associated-with-the-account</value>
           </property>
   2. <span data-ttu-id="a4b8c-200">Hello girişleri aşağıdaki hello kaldırmak `core-site.xml`.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-200">Remove hello following entries from hello `core-site.xml`.</span></span>

           <property>
                 <name>fs.azure.account.keyprovider.hdistoragecentral.blob.core.windows.net</name>
                 <value>org.apache.hadoop.fs.azure.ShellDecryptionKeyProvider</value>
           </property>

           <property>
                 <name>fs.azure.shellkeyprovider.script</name>
                 <value>/usr/lib/python2.7/dist-packages/hdinsight_common/decrypt.sh</value>
           </property>

           <property>
                 <name>net.topology.script.file.name</name>
                 <value>/etc/hadoop/conf/topology_script.py</value>
           </property>
   3. <span data-ttu-id="a4b8c-201">Merhaba dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-201">Save hello file.</span></span>
7. <span data-ttu-id="a4b8c-202">Uygulamanız için Hello ana sınıf ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-202">Add hello Main class for your application.</span></span> <span data-ttu-id="a4b8c-203">Merhaba gelen **Proje Gezgini**, sağ **src**, çok noktası**yeni**ve ardından **Scala sınıfı**.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-203">From hello **Project Explorer**, right-click **src**, point too**New**, and then click **Scala class**.</span></span>

    ![Kaynak kodu ekleyin](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-spark-scala-code.png)
8. <span data-ttu-id="a4b8c-205">Merhaba, **yeni Scala Sınıf Oluştur** iletişim kutusunda, için bir ad sağlayın **türü** seçin **nesne**ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-205">In hello **Create New Scala Class** dialog box, provide a name, for **Kind** select **Object**, and then click **OK**.</span></span>

    ![Kaynak kodu ekleyin](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-spark-scala-code-object.png)
9. <span data-ttu-id="a4b8c-207">Merhaba, `MyClusterAppMain.scala` dosya, hello aşağıdaki kodu yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-207">In hello `MyClusterAppMain.scala` file, paste hello following code.</span></span> <span data-ttu-id="a4b8c-208">Bu kod hello Spark bağlam oluşturur ve başlatır bir `executeJob` hello yönteminden `SparkSample` nesnesi.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-208">This code creates hello Spark context and launches an `executeJob` method from hello `SparkSample` object.</span></span>

        import org.apache.spark.{SparkConf, SparkContext}

        object SparkSampleMain {
          def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("SparkSample")
                                      .set("spark.hadoop.validateOutputSpecs", "false")
            val sc = new SparkContext(conf)

            SparkSample.executeJob(sc,
                                   "wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv",
                                   "wasb:///HVACOut")
          }
        }

10. <span data-ttu-id="a4b8c-209">Yeni bir Scala nesnesi adlı tooadd yukarıdaki adımları 8 ve 9 `SparkSample`.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-209">Repeat steps 8 and 9 above tooadd a new Scala object called `SparkSample`.</span></span> <span data-ttu-id="a4b8c-210">toothis sınıf hello aşağıdaki kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-210">toothis class add hello following code.</span></span> <span data-ttu-id="a4b8c-211">Bu kod hello HVAC.csv (tüm Hdınsight Spark kümeleri üzerinde kullanılabilir) hello verileri okur, yalnızca bir rakam hello yedinci hello CSV sütununda hello satırları alır ve hello çıkış çok yazar**/HVACOut** hello varsayılan altında Merhaba küme depolama kapsayıcısı.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-211">This code reads hello data from hello HVAC.csv (available on all HDInsight Spark clusters), retrieves hello rows that only have one digit in hello seventh column in hello CSV, and writes hello output too**/HVACOut** under hello default storage container for hello cluster.</span></span>

        import org.apache.spark.SparkContext

        object SparkSample {
         def executeJob (sc: SparkContext, input: String, output: String): Unit = {
           val rdd = sc.textFile(input)

           //find hello rows which have only one digit in hello 7th column in hello CSV
           val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)

           val s = sc.parallelize(rdd.take(5)).cartesian(rdd).count()
           println(s)

           rdd1.saveAsTextFile(output)
           //rdd1.collect().foreach(println)
         }
        }
11. <span data-ttu-id="a4b8c-212">8. ve 9 adlı yeni bir sınıf tooadd yukarıdaki adımları yineleyin `RemoteClusterDebugging`.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-212">Repeat steps 8 and 9 above tooadd a new class called `RemoteClusterDebugging`.</span></span> <span data-ttu-id="a4b8c-213">Bu sınıf uygulamalarında hata ayıklama için kullanılan hello Spark test çerçevesi uygular.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-213">This class implements hello Spark test framework that is used for debugging applications.</span></span> <span data-ttu-id="a4b8c-214">Aşağıdaki kodu toohello hello eklemek `RemoteClusterDebugging` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-214">Add hello following code toohello `RemoteClusterDebugging` class.</span></span>

        import org.apache.spark.{SparkConf, SparkContext}
        import org.scalatest.FunSuite

        class RemoteClusterDebugging extends FunSuite {

         test("Remote run") {
           val conf = new SparkConf().setAppName("SparkSample")
                                     .setMaster("yarn-client")
                                     .set("spark.yarn.am.extraJavaOptions", "-Dhdp.version=2.4")
                                     .set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")
                                     .setJars(Seq("""C:\workspace\IdeaProjects\MyClusterApp\out\artifacts\MyClusterApp_DefaultArtifact\default_artifact.jar"""))
                                     .set("spark.hadoop.validateOutputSpecs", "false")
           val sc = new SparkContext(conf)

           SparkSample.executeJob(sc,
             "wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv",
             "wasb:///HVACOut")
         }
        }

     <span data-ttu-id="a4b8c-215">Önemli noktalar toonote burada birkaç:</span><span class="sxs-lookup"><span data-stu-id="a4b8c-215">Couple of important things toonote here:</span></span>

   * <span data-ttu-id="a4b8c-216">İçin `.set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")`, hello Spark derleme JAR hello küme depolama hello belirtilen yolda kullanılabilir olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-216">For `.set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")`, make sure hello Spark assembly JAR is available on hello cluster storage at hello specified path.</span></span>
   * <span data-ttu-id="a4b8c-217">İçin `setJars`, burada hello yapı jar oluşturulacak hello konumu belirtin.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-217">For `setJars`, specify hello location where hello artifact jar will be created.</span></span> <span data-ttu-id="a4b8c-218">Genellikle `<Your IntelliJ project directory>\out\<project name>_DefaultArtifact\default_artifact.jar`.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-218">Typically it is `<Your IntelliJ project directory>\out\<project name>_DefaultArtifact\default_artifact.jar`.</span></span>
12. <span data-ttu-id="a4b8c-219">Merhaba, `RemoteClusterDebugging` sınıfı, hello sağ `test` anahtar sözcüğü ve seçin **RemoteClusterDebugging yapılandırma oluşturmak**.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-219">In hello `RemoteClusterDebugging` class, right-click hello `test` keyword and select **Create RemoteClusterDebugging Configuration**.</span></span>

    ![Uzaktan yapılandırma oluşturma](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-remote-config.png)

13. <span data-ttu-id="a4b8c-221">Hello iletişim kutusunda, hello yapılandırması için bir ad sağlayın ve seçin hello **Test türü** olarak **Test adı**.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-221">In hello dialog box, provide a name for hello configuration, and select hello **Test kind** as **Test name**.</span></span> <span data-ttu-id="a4b8c-222">Diğer tüm değerler varsayılan olarak bırakın, tıklatın **Uygula**ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-222">Leave all other values as default, click **Apply**, and then click **OK**.</span></span>

    ![Uzaktan yapılandırma oluşturma](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/provide-config-value.png)
14. <span data-ttu-id="a4b8c-224">Artık görmelisiniz bir **uzaktan çalıştırmak** yapılandırma açılan hello menü çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-224">You should now see a **Remote Run** configuration drop-down in hello menu bar.</span></span>

    ![Uzaktan yapılandırma oluşturma](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/config-run.png)

## <a name="step-5-run-hello-application-in-debug-mode"></a><span data-ttu-id="a4b8c-226">5. adım: hello uygulamayı hata ayıklama modunda çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-226">Step 5: Run hello application in debug mode</span></span>
1. <span data-ttu-id="a4b8c-227">Intellij Idea projenizi açın `SparkSample.scala` ve bir kesme noktası sonraki too'val rdd1 Oluştur '.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-227">In your IntelliJ IDEA project, open `SparkSample.scala` and create a breakpoint next too\`val rdd1'.</span></span> <span data-ttu-id="a4b8c-228">Bir kesme noktası oluşturmak için hello açılır menüsünden seçin **işlevi executeJob satırında**.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-228">In hello pop-up menu for creating a breakpoint, select **line in function executeJob**.</span></span>

    ![Kesme noktası ekleme](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-breakpoint.png)
2. <span data-ttu-id="a4b8c-230">Merhaba tıklatın **hata ayıklama çalıştırmak** düğmesine bir sonraki toohello **uzaktan çalıştırmak** yapılandırma açılan toostart Merhaba uygulaması çalıştıran.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-230">Click hello **Debug Run** button next toohello **Remote Run** configuration drop-down toostart running hello application.</span></span>

    ![Hata ayıklama modunda Hello programı çalıştır](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-run-mode.png)
3. <span data-ttu-id="a4b8c-232">Merhaba program yürütme hello kesme noktasına ulaştığında, görmelisiniz bir **hata ayıklayıcı** hello alt bölmedeki sekmesi.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-232">When hello program execution reaches hello breakpoint, you should see a **Debugger** tab in hello bottom pane.</span></span>

    ![Hata ayıklama modunda Hello programı çalıştır](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch.png)
4. <span data-ttu-id="a4b8c-234">Merhaba tıklayın (**+**) simgesi tooadd hello resimde gösterildiği gibi bir izleme.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-234">Click hello (**+**) icon tooadd a watch as shown in hello image below.</span></span>

    ![Hata ayıklama modunda Hello programı çalıştır](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch-variable.png)

    <span data-ttu-id="a4b8c-236">Burada, önce hello değişkeni Merhaba uygulaması ihlal çünkü `rdd1` , biz hello değişkeninde ilk 5 satırları hello ne görebilirsiniz bu izleme kullanılarak oluşturulmuş `rdd`.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-236">Here, because hello application broke before hello variable `rdd1` was created, using this watch we can see what are hello first 5 rows in hello variable `rdd`.</span></span> <span data-ttu-id="a4b8c-237">**ENTER**'a basın.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-237">Press **ENTER**.</span></span>

    ![Hata ayıklama modunda Hello programı çalıştır](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch-variable-value.png)

    <span data-ttu-id="a4b8c-239">Yukarıdaki hello resimde gördüğünüz çalışma zamanında veri ve hata ayıklama terrabytes sorgulayabilir olduğunu nasıl uygulama ilerler.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-239">What you see in hello image above is that at runtime, you could query terrabytes of data and debug how your application progresses.</span></span> <span data-ttu-id="a4b8c-240">Örneğin, yukarıdaki hello resimde gösterilen hello çıktısında bu hello gördüğünüz ilk hello çıktı satırıdır üstbilgi.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-240">For example, in hello output shown in hello image above, you can see that hello first row of hello output is a header.</span></span> <span data-ttu-id="a4b8c-241">Bunu temel alarak, gerekirse, uygulama kodu tooskip hello başlık satırı değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-241">Based on this, you can modify your application code tooskip hello header row if required.</span></span>
5. <span data-ttu-id="a4b8c-242">Merhaba artık tıklatabilir **Sürdür Program** simgesi tooproceed ile uygulamanızı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-242">You can now click hello **Resume Program** icon tooproceed with your application run.</span></span>

    ![Hata ayıklama modunda Hello programı çalıştır](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-continue-run.png)
6. <span data-ttu-id="a4b8c-244">Merhaba uygulaması başarıyla tamamlarsa, hello aşağıdaki gibi bir çıktı görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-244">If hello application completes successfully, you should see an output like hello following.</span></span>

    ![Hata ayıklama modunda Hello programı çalıştır](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-complete.png)

## <span data-ttu-id="a4b8c-246"><a name="seealso"></a>Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="a4b8c-246"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="a4b8c-247">Genel Bakış: Azure HDInsight’ta Apache Spark</span><span class="sxs-lookup"><span data-stu-id="a4b8c-247">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="demo"></a><span data-ttu-id="a4b8c-248">Tanıtım</span><span class="sxs-lookup"><span data-stu-id="a4b8c-248">Demo</span></span>
* <span data-ttu-id="a4b8c-249">Scala projesi (Video) oluşturun: [Spark Scala uygulamaları oluşturma](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="a4b8c-249">Create Scala Project (Video): [Create Spark Scala Applications](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span></span>
* <span data-ttu-id="a4b8c-250">Uzaktan hata ayıklama (Video): [Intellij toodebug Spark uygulamalarında uzaktan Hdınsight kümesinde için kullanım Azure Araç Seti](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="a4b8c-250">Remote Debug (Video): [Use Azure Toolkit for IntelliJ toodebug Spark applications remotely on HDInsight Cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span></span>

### <a name="scenarios"></a><span data-ttu-id="a4b8c-251">Senaryolar</span><span class="sxs-lookup"><span data-stu-id="a4b8c-251">Scenarios</span></span>
* [<span data-ttu-id="a4b8c-252">BI ile Spark: BI araçlarıyla HDInsight’ta Spark kullanarak etkileşimli veri çözümlemesi gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="a4b8c-252">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="a4b8c-253">Machine Learning ile Spark: HVAC verilerini kullanarak bina sıcaklığını çözümlemek için HDInsight’ta Spark kullanma</span><span class="sxs-lookup"><span data-stu-id="a4b8c-253">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="a4b8c-254">Machine Learning ile Spark: Spark Hdınsight toopredict yemek İnceleme sonuçlarını içinde kullanma</span><span class="sxs-lookup"><span data-stu-id="a4b8c-254">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="a4b8c-255">Spark Akış: Gerçek zamanlı akış uygulamaları oluşturmak için HDInsight’ta Spark kullanma</span><span class="sxs-lookup"><span data-stu-id="a4b8c-255">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="a4b8c-256">HDInsight’ta Spark kullanarak Web sitesi günlüğü çözümlemesi</span><span class="sxs-lookup"><span data-stu-id="a4b8c-256">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="a4b8c-257">Uygulamaları oluşturma ve çalıştırma</span><span class="sxs-lookup"><span data-stu-id="a4b8c-257">Create and run applications</span></span>
* [<span data-ttu-id="a4b8c-258">Scala kullanarak tek başına uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="a4b8c-258">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="a4b8c-259">Livy kullanarak Spark kümesinde işleri uzaktan çalıştırma</span><span class="sxs-lookup"><span data-stu-id="a4b8c-259">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="a4b8c-260">Araçlar ve uzantılar</span><span class="sxs-lookup"><span data-stu-id="a4b8c-260">Tools and extensions</span></span>
* [<span data-ttu-id="a4b8c-261">Intellij toocreate için Hdınsight Araçları'nı Azure araç setindeki kullanın ve Spark Scala uygulamaları gönderin</span><span class="sxs-lookup"><span data-stu-id="a4b8c-261">Use HDInsight Tools in Azure Toolkit for IntelliJ toocreate and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="a4b8c-262">SSH üzerinden uzaktan Intellij toodebug Spark uygulamaları için Azure araç kullanma</span><span class="sxs-lookup"><span data-stu-id="a4b8c-262">Use Azure Toolkit for IntelliJ toodebug Spark applications remotely through SSH</span></span>](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [<span data-ttu-id="a4b8c-263">Korumalı alan Hortonworks ile Intellij için Hdınsight araçları kullanma</span><span class="sxs-lookup"><span data-stu-id="a4b8c-263">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [<span data-ttu-id="a4b8c-264">Azure araç setini Eclipse toocreate Spark uygulamaları için Hdınsight araçları kullanın</span><span class="sxs-lookup"><span data-stu-id="a4b8c-264">Use HDInsight Tools in Azure Toolkit for Eclipse toocreate Spark applications</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [<span data-ttu-id="a4b8c-265">HDInsight’ta Spark kümesi ile Zeppelin not defterlerini kullanma</span><span class="sxs-lookup"><span data-stu-id="a4b8c-265">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="a4b8c-266">HDInsight için Spark kümesinde Jupyter not defteri için kullanılabilir çekirdekler</span><span class="sxs-lookup"><span data-stu-id="a4b8c-266">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="a4b8c-267">Jupyter not defterleri ile dış paketleri kullanma</span><span class="sxs-lookup"><span data-stu-id="a4b8c-267">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="a4b8c-268">Jupyter bilgisayarınıza yüklemek ve tooan Hdınsight Spark kümesi bağlanın</span><span class="sxs-lookup"><span data-stu-id="a4b8c-268">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="a4b8c-269">Kaynakları yönetme</span><span class="sxs-lookup"><span data-stu-id="a4b8c-269">Manage resources</span></span>
* [<span data-ttu-id="a4b8c-270">Hello Azure hdınsight'ta Apache Spark küme kaynaklarını yönetme</span><span class="sxs-lookup"><span data-stu-id="a4b8c-270">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="a4b8c-271">HDInsight’ta bir Apache Spark kümesinde çalışan işleri izleme ve hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="a4b8c-271">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
