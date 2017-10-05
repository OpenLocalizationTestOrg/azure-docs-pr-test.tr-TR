---
title: "Apache kullanın ve Windows tabanlı Azure Hdınsight ile SQuirreL | Microsoft Docs"
description: "Hdınsight'ta Apache Phoenix kullanmayı ve yüklemek ve hdınsight'ta HBase kümesi bağlanmak için istasyonunuzda SQuirreL yapılandırmak nasıl öğrenin."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 1a756e98-75c1-44cd-a178-c5119683b7b7
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 024b70df99fdefa1598225ebb1fbfee85ea375d0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="use-apache-phoenix-and-squirrel-with-windows-based-hbase-clusters-in-hdinsight"></a><span data-ttu-id="27def-103">Hdınsight'ta Windows tabanlı HBase kümeleriyle Apache ve SQuirreL kullanma</span><span class="sxs-lookup"><span data-stu-id="27def-103">Use Apache Phoenix and SQuirreL with Windows-based HBase clusters in HDInsight</span></span>
<span data-ttu-id="27def-104">Nasıl kullanacağınızı öğrenin [Apache Phoenix](http://phoenix.apache.org/) ve yükleme ve SQuirreL istasyonunuzu hdınsight'ta HBase kümesi bağlanmak için yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="27def-104">Learn how to use [Apache Phoenix](http://phoenix.apache.org/) in HDInsight, and how to install and configure SQuirreL on your workstation to connect to an HBase cluster in HDInsight.</span></span> <span data-ttu-id="27def-105">Phoenix hakkında daha fazla bilgi için bkz: [Phoenix 15 dakika veya daha az](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html).</span><span class="sxs-lookup"><span data-stu-id="27def-105">For more information about Phoenix, see [Phoenix in 15 minutes or less](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html).</span></span> <span data-ttu-id="27def-106">Phoenix dilbilgisi için bkz: [Phoenix Dilbilgisi](http://phoenix.apache.org/language/index.html).</span><span class="sxs-lookup"><span data-stu-id="27def-106">For the Phoenix grammar, see [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

> [!NOTE]
> <span data-ttu-id="27def-107">Phoenix sürümünü hdınsight'ta bilgi için [Hdınsight tarafından sağlanan Hadoop küme sürümlerindeki yenilikler nelerdir?](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="27def-107">For the Phoenix version information in HDInsight, see [What's new in the Hadoop cluster versions provided by HDInsight?](hdinsight-component-versioning.md).</span></span>
>

> [!IMPORTANT]
> <span data-ttu-id="27def-108">Bu belgede yer alan adımlar, yalnızca Windows tabanlı Hdınsight kümeleri için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="27def-108">The steps in this document only work for Windows-based HDInsight clusters.</span></span> <span data-ttu-id="27def-109">Hdınsight yalnızca Windows'da Hdınsight 3.4 ' düşük sürümleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="27def-109">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="27def-110">Linux, HDInsight sürüm 3.4 ve üzerinde kullanılan tek işletim sistemidir.</span><span class="sxs-lookup"><span data-stu-id="27def-110">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="27def-111">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="27def-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="27def-112">Phoenix Linux tabanlı Hdınsight kullanma hakkında daha fazla bilgi için bkz: [Hdınsight'ta Linux tabanlı HBase ile kullanım Apache Phoenix kümeleri](hdinsight-hbase-phoenix-squirrel-linux.md).</span><span class="sxs-lookup"><span data-stu-id="27def-112">For information on using Phoenix on Linux-based HDInsight, see [Use Apache Phoenix with Linux-based HBase clusters in HDInsight](hdinsight-hbase-phoenix-squirrel-linux.md).</span></span>
>



## <a name="use-sqlline"></a><span data-ttu-id="27def-113">SQLLine kullanın</span><span class="sxs-lookup"><span data-stu-id="27def-113">Use SQLLine</span></span>
<span data-ttu-id="27def-114">[SQLLine](http://sqlline.sourceforge.net/) SQL yürütülecek bir komut satırı yardımcı programıdır.</span><span class="sxs-lookup"><span data-stu-id="27def-114">[SQLLine](http://sqlline.sourceforge.net/) is a command line utility to execute SQL.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="27def-115">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="27def-115">Prerequisites</span></span>
<span data-ttu-id="27def-116">SQLLine kullanmadan önce aşağıdakilere sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="27def-116">Before you can use SQLLine, you must have the following:</span></span>

* <span data-ttu-id="27def-117">**Hdınsight'ta HBase kümesi**.</span><span class="sxs-lookup"><span data-stu-id="27def-117">**A HBase cluster in HDInsight**.</span></span> <span data-ttu-id="27def-118">Küme hazırlama HBase hakkında bilgi için bkz: [hdınsight'ta Apache HBase kullanmaya başlama][hdinsight-hbase-get-started].</span><span class="sxs-lookup"><span data-stu-id="27def-118">For information on provision HBase cluster, see [Get started with Apache HBase in HDInsight][hdinsight-hbase-get-started].</span></span>
* <span data-ttu-id="27def-119">**Uzak Masaüstü Protokolü aracılığıyla HBase kümesi bağlanmak**.</span><span class="sxs-lookup"><span data-stu-id="27def-119">**Connect to the HBase cluster via the remote desktop protocol**.</span></span> <span data-ttu-id="27def-120">Yönergeler için bkz: [yönetmek Hdınsight'ta Hadoop kümeleri Azure Klasik Portalı'nı kullanarak][hdinsight-manage-portal].</span><span class="sxs-lookup"><span data-stu-id="27def-120">For instructions, see [Manage Hadoop clusters in HDInsight by using the Azure Classic Portal][hdinsight-manage-portal].</span></span>

<span data-ttu-id="27def-121">**Ana bilgisayar adı bulunamıyor**</span><span class="sxs-lookup"><span data-stu-id="27def-121">**To find out the host name**</span></span>

1. <span data-ttu-id="27def-122">Açık **Hadoop komut satırı** masaüstünden.</span><span class="sxs-lookup"><span data-stu-id="27def-122">Open **Hadoop Command Line** from the desktop.</span></span>
2. <span data-ttu-id="27def-123">DNS soneki almak için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="27def-123">Run the following command to get the DNS suffix:</span></span>

        ipconfig

    <span data-ttu-id="27def-124">Yazma **bağlantıya özgü DNS soneki**.</span><span class="sxs-lookup"><span data-stu-id="27def-124">Write down **Connection-specific DNS Suffix**.</span></span> <span data-ttu-id="27def-125">Örneğin, *myhbasecluster.f5.internal.cloudapp.net*.</span><span class="sxs-lookup"><span data-stu-id="27def-125">For example, *myhbasecluster.f5.internal.cloudapp.net*.</span></span> <span data-ttu-id="27def-126">Bir HBase kümesi bağlandığınızda, FQDN kullanarak Zookeepers birine bağlanabilmeleri gerekir.</span><span class="sxs-lookup"><span data-stu-id="27def-126">When you connect to an HBase cluster, you will need to connect to one of the Zookeepers using FQDN.</span></span> <span data-ttu-id="27def-127">Her Hdınsight kümesi 3 Zookeepers sahiptir.</span><span class="sxs-lookup"><span data-stu-id="27def-127">Each HDInsight cluster has 3 Zookeepers.</span></span> <span data-ttu-id="27def-128">Bunlar *zookeeper0*, *zookeeper1*, ve *zookeeper2*.</span><span class="sxs-lookup"><span data-stu-id="27def-128">They are *zookeeper0*, *zookeeper1*, and *zookeeper2*.</span></span> <span data-ttu-id="27def-129">FQDN şöyle olacaktır *zookeeper2.myhbasecluster.f5.internal.cloudapp.net*.</span><span class="sxs-lookup"><span data-stu-id="27def-129">The FQDN will be something like *zookeeper2.myhbasecluster.f5.internal.cloudapp.net*.</span></span>

<span data-ttu-id="27def-130">**SQLLine kullanmak için**</span><span class="sxs-lookup"><span data-stu-id="27def-130">**To use SQLLine**</span></span>

1. <span data-ttu-id="27def-131">Açık **Hadoop komut satırı** masaüstünden.</span><span class="sxs-lookup"><span data-stu-id="27def-131">Open **Hadoop Command Line** from the desktop.</span></span>
2. <span data-ttu-id="27def-132">SQLLine açmak için aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="27def-132">Run the following commands to open SQLLine:</span></span>

        cd %phoenix_home%\bin
        sqlline.py [The FQDN of one of the Zookeepers]

    ![Hdınsight hbase phoenix sqlline][hdinsight-hbase-phoenix-sqlline]

    <span data-ttu-id="27def-134">Aşağıdaki örnekte kullanılan komutlar:</span><span class="sxs-lookup"><span data-stu-id="27def-134">The commands used in the sample:</span></span>

        CREATE TABLE Company (COMPANY_ID INTEGER PRIMARY KEY, NAME VARCHAR(225));

        !tables

        UPSERT INTO Company VALUES(1, 'Microsoft');

        SELECT * FROM Company;

<span data-ttu-id="27def-135">Daha fazla bilgi için bkz: [SQLLine el ile](http://sqlline.sourceforge.net/#manual) ve [Phoenix Dilbilgisi](http://phoenix.apache.org/language/index.html).</span><span class="sxs-lookup"><span data-stu-id="27def-135">For more information, see [SQLLine manual](http://sqlline.sourceforge.net/#manual) and [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

## <a name="use-squirrel"></a><span data-ttu-id="27def-136">SQuirreL kullanma</span><span class="sxs-lookup"><span data-stu-id="27def-136">Use SQuirreL</span></span>
<span data-ttu-id="27def-137">[SQL istemci sQuirreL](http://squirrel-sql.sourceforge.net/) JDBC uyumlu bir veritabanına yapısını görüntüleme, tablolardaki verileri göz atın, SQL komutlarını vb. sorun sağlayacak bir grafik Java programdır. Hdınsight üzerinde Apache Phoenix bağlanmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="27def-137">[SQuirreL SQL Client](http://squirrel-sql.sourceforge.net/) is a graphical Java program that will allow you to view the structure of a JDBC compliant database, browse the data in tables, issue SQL commands etc. It can be used to connect to Apache Phoenix on HDInsight.</span></span>

<span data-ttu-id="27def-138">Bu bölümde yükleme ve hdınsight'ta HBase kümesi VPN aracılığıyla bağlanmak için istasyonunuzda SQuirreL yapılandırma gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="27def-138">This section shows you how to install and configure SQuirreL on your workstation to connect to an HBase cluster in HDInsight via VPN.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="27def-139">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="27def-139">Prerequisites</span></span>
<span data-ttu-id="27def-140">Yordamları izlemeden önce aşağıdakilerin olması gerekir:</span><span class="sxs-lookup"><span data-stu-id="27def-140">Before following the procedures, you must have the following:</span></span>

* <span data-ttu-id="27def-141">Azure sanal ağını DNS sanal makine ile dağıtılan bir HBase kümesi.</span><span class="sxs-lookup"><span data-stu-id="27def-141">An HBase cluster deployed to an Azure virtual network with a DNS virtual machine.</span></span>  <span data-ttu-id="27def-142">Yönergeler için bkz: [oluşturma HBase kümeleri Azure sanal ağı][hdinsight-hbase-provision-vnet].</span><span class="sxs-lookup"><span data-stu-id="27def-142">For instructions, see [Create HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet].</span></span>

* <span data-ttu-id="27def-143">HBase kümesi küme bağlantıya özgü DNS soneki alın.</span><span class="sxs-lookup"><span data-stu-id="27def-143">Get the HBase cluster cluster Connection-specific DNS suffix.</span></span> <span data-ttu-id="27def-144">Bu, küme halinde RDP almak ve ipconfig komutunu çalıştırmak için.</span><span class="sxs-lookup"><span data-stu-id="27def-144">To get it, RDP into the cluster, and then run IPConfig.</span></span>  <span data-ttu-id="27def-145">DNS soneki benzer:</span><span class="sxs-lookup"><span data-stu-id="27def-145">The DNS suffix is similar to:</span></span>

        myhbase.b7.internal.cloudapp.net
* <span data-ttu-id="27def-146">İndirme ve yükleme [Microsoft Visual Studio Express için Windows Masaüstü](https://www.visualstudio.com/products/visual-studio-express-vs.aspx) istasyonunuzda.</span><span class="sxs-lookup"><span data-stu-id="27def-146">Download and install [Microsoft Visual Studio Express for Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx) on your workstation.</span></span> <span data-ttu-id="27def-147">Makecert, bir sertifika oluşturmak için paketten gerekir.</span><span class="sxs-lookup"><span data-stu-id="27def-147">You will need makecert from the package to create your certificate.</span></span>  
* <span data-ttu-id="27def-148">İndirme ve yükleme [Java Çalışma zamanı ortamı](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html) istasyonunuzda.</span><span class="sxs-lookup"><span data-stu-id="27def-148">Download and install [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html) on your workstation.</span></span>  <span data-ttu-id="27def-149">SQL istemci sürüm 3.0 ve daha yüksek sQuirreL JRE 1.6 veya sonraki sürümünü gerektirir.</span><span class="sxs-lookup"><span data-stu-id="27def-149">SQuirreL SQL client version 3.0 and higher requires JRE version 1.6 or higher.</span></span>  

### <a name="configure-a-point-to-site-vpn-connection-to-the-azure-virtual-network"></a><span data-ttu-id="27def-150">Azure sanal ağa noktadan siteye VPN bağlantısı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="27def-150">Configure a Point-to-Site VPN connection to the Azure virtual network</span></span>
<span data-ttu-id="27def-151">Bir noktadan siteye VPN bağlantısı yapılandırma söz konusu 3 adım vardır:</span><span class="sxs-lookup"><span data-stu-id="27def-151">There are 3 steps involved configuring a point-to-site VPN connection:</span></span>

1. [<span data-ttu-id="27def-152">Bir sanal ağ ve dinamik yönlendirme ağ geçidi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="27def-152">Configure a virtual network and a dynamic routing gateway</span></span>](#Configure-a-virtual-network-and-a-dynamic-routing-gateway)
2. [<span data-ttu-id="27def-153">Sertifikalarınızı oluşturma</span><span class="sxs-lookup"><span data-stu-id="27def-153">Create your certificates</span></span>](#Create-your-certificates)
3. [<span data-ttu-id="27def-154">VPN istemcinizi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="27def-154">Configure your VPN client</span></span>](#Configure-your-VPN-client)

<span data-ttu-id="27def-155">Bkz: [bir Azure sanal ağa noktadan siteye VPN bağlantısı yapılandırma](../vpn-gateway/vpn-gateway-point-to-site-create.md) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="27def-155">See [Configure a Point-to-Site VPN connection to an Azure Virtual Network](../vpn-gateway/vpn-gateway-point-to-site-create.md) for more information.</span></span>

#### <a name="configure-a-virtual-network-and-a-dynamic-routing-gateway"></a><span data-ttu-id="27def-156">Bir sanal ağ ve dinamik yönlendirme ağ geçidi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="27def-156">Configure a virtual network and a dynamic routing gateway</span></span>
<span data-ttu-id="27def-157">Bir Azure sanal ağındaki bir HBase kümesi sağlanan güvence altına almak (Bu bölümün önkoşullara bakın).</span><span class="sxs-lookup"><span data-stu-id="27def-157">Assure you have provisioned an HBase cluster in an Azure virtual network (see the prerequisites for this section).</span></span> <span data-ttu-id="27def-158">Sonraki adım, bir noktadan siteye bağlantı yapılandırmaktır.</span><span class="sxs-lookup"><span data-stu-id="27def-158">The next step is to configure a point-to-site connection.</span></span>

<span data-ttu-id="27def-159">**Noktadan siteye bağlantı yapılandırmak için**</span><span class="sxs-lookup"><span data-stu-id="27def-159">**To configure the point-to-site connectivity**</span></span>

1. <span data-ttu-id="27def-160">Oturum [Klasik Azure portalı][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="27def-160">Sign in to the [Azure Classic Portal][azure-portal].</span></span>
2. <span data-ttu-id="27def-161">Sol bölmede, tıklatın **ağlar**.</span><span class="sxs-lookup"><span data-stu-id="27def-161">On the left, click **NETWORKS**.</span></span>
3. <span data-ttu-id="27def-162">Oluşturduğunuz sanal ağa tıklayın (bkz [sağlama HBase kümeleri Azure sanal ağı][hdinsight-hbase-provision-vnet]).</span><span class="sxs-lookup"><span data-stu-id="27def-162">Click the virtual network you have created (see [Provision HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet]).</span></span>
4. <span data-ttu-id="27def-163">Tıklatın **yapılandırma** üstten.</span><span class="sxs-lookup"><span data-stu-id="27def-163">Click **CONFIGURE** from the top.</span></span>
5. <span data-ttu-id="27def-164">İçinde **noktadan siteye bağlantı** bölümünde, select **noktadan siteye bağlantı yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="27def-164">In the **point-to-site connectivity** section, select **Configure point-to-site connectivity**.</span></span>
6. <span data-ttu-id="27def-165">Yapılandırma **başlangıç IP** ve **CIDR** içinden VPN istemcilerinizin bağlıyken bir IP adresi alacağı IP adresi aralığı belirtmek için.</span><span class="sxs-lookup"><span data-stu-id="27def-165">Configure **STARTING IP** and **CIDR** to specify the IP address range from which your VPN clients will receive an IP address when connected.</span></span> <span data-ttu-id="27def-166">Aralığın, şirket içi ağınız ve Azure sanal ağı için bağlanırsınız bulunan aralıklardan herhangi biriyle çakışamaz.</span><span class="sxs-lookup"><span data-stu-id="27def-166">The range cannot overlap with any of the ranges located on your on-premises network and the Azure virtual network you will be connecting to.</span></span> <span data-ttu-id="27def-167">Örneğin.</span><span class="sxs-lookup"><span data-stu-id="27def-167">For example.</span></span> <span data-ttu-id="27def-168">sanal ağ için 10.0.0.0/20 seçtiyseniz, istemci adres alanı için 10.1.0.0/24 seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="27def-168">if you selected 10.0.0.0/20 for the virtual network, you can select 10.1.0.0/24 for the client address space.</span></span> <span data-ttu-id="27def-169">Bkz: [noktadan siteye bağlantı] [ vnet-point-to-site-connectivity] daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="27def-169">See the [Point-To-Site Connectivity][vnet-point-to-site-connectivity] page for more information.</span></span>
7. <span data-ttu-id="27def-170">Sanal ağ adres alanları bölümünde tıklayın **ağ geçidi alt ağı eklemek**.</span><span class="sxs-lookup"><span data-stu-id="27def-170">In the virtual network address spaces section, click **add gateway subnet**.</span></span>
8. <span data-ttu-id="27def-171">Tıklatın **KAYDETMEK** sayfanın üzerinde.</span><span class="sxs-lookup"><span data-stu-id="27def-171">Click **SAVE** on the bottom of the page.</span></span>
9. <span data-ttu-id="27def-172">Tıklatın **Evet** Değişikliği onaylamak için.</span><span class="sxs-lookup"><span data-stu-id="27def-172">Click **YES** to confirm the change.</span></span> <span data-ttu-id="27def-173">Sistem sonraki yordama devam etmeden önce değişikliği yapmadan tamamlanana kadar bekleyin.</span><span class="sxs-lookup"><span data-stu-id="27def-173">Wait until the system has finished making the change before you proceed to the next procedure.</span></span>

<span data-ttu-id="27def-174">**Dinamik yönlendirme ağ geçidi oluşturmak için**</span><span class="sxs-lookup"><span data-stu-id="27def-174">**To create a dynamic routing gateway**</span></span>

1. <span data-ttu-id="27def-175">Azure Klasik portalından tıklatın **PANO** sayfasının üstten.</span><span class="sxs-lookup"><span data-stu-id="27def-175">From the Azure Classic Portal, click **DASHBOARD** from the top of the page.</span></span>
2. <span data-ttu-id="27def-176">Tıklatın **ağ geçidi Oluştur** sayfanın en altındaki.</span><span class="sxs-lookup"><span data-stu-id="27def-176">Click **CREATE GATEWAY** from the bottom of the page.</span></span>
3. <span data-ttu-id="27def-177">Tıklatın **Evet** onaylamak için.</span><span class="sxs-lookup"><span data-stu-id="27def-177">Click **YES** to confirm.</span></span> <span data-ttu-id="27def-178">Ağ geçidi oluşturulana kadar bekleyin.</span><span class="sxs-lookup"><span data-stu-id="27def-178">Wait until the gateway is created.</span></span>
4. <span data-ttu-id="27def-179">Tıklatın **PANO** üstten.</span><span class="sxs-lookup"><span data-stu-id="27def-179">Click **DASHBOARD** from the top.</span></span>  <span data-ttu-id="27def-180">Sanal ağ visual diyagramı görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="27def-180">You will see a visual diagram of the virtual network:</span></span>

    ![Azure sanal ağı noktadan siteye sanal diyagramı][img-vnet-diagram]

    <span data-ttu-id="27def-182">Diyagram 0 istemci bağlantılarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="27def-182">The diagram shows 0 client connections.</span></span> <span data-ttu-id="27def-183">Sanal ağa bir bağlantı yaptıktan sonra bir sayı güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="27def-183">After you make a connection to the virtual network, the number will be updated to one.</span></span>

#### <a name="create-your-certificates"></a><span data-ttu-id="27def-184">Sertifikalarınızı oluşturma</span><span class="sxs-lookup"><span data-stu-id="27def-184">Create your certificates</span></span>
<span data-ttu-id="27def-185">Bir X.509 sertifikası oluşturmanın yollarından biri olan sertifika oluşturma ile birlikte gelen Aracı (makecert.exe) kullanarak [Microsoft Visual Studio Express için Windows Masaüstü](https://www.visualstudio.com/products/visual-studio-express-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="27def-185">One way to create an X.509 certificate is by using the Certificate Creation Tool (makecert.exe) that comes with [Microsoft Visual Studio Express for Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx).</span></span>

<span data-ttu-id="27def-186">**Bir otomatik olarak imzalanan sertifika oluşturmak için**</span><span class="sxs-lookup"><span data-stu-id="27def-186">**To create a self-signed root certificate**</span></span>

1. <span data-ttu-id="27def-187">İstasyonunuzdan, bir komut istemi penceresi açın.</span><span class="sxs-lookup"><span data-stu-id="27def-187">From your workstation, open a command prompt window.</span></span>
2. <span data-ttu-id="27def-188">Visual Studio Araçları klasörüne gidin.</span><span class="sxs-lookup"><span data-stu-id="27def-188">Navigate to the Visual Studio tools folder.</span></span>
3. <span data-ttu-id="27def-189">Aşağıdaki komutu aşağıdaki örnekte oluşturur ve istasyonunuzda kişisel sertifika deposunda kök sertifikasını yükleyin ve daha sonra Azure Klasik Portalı'na yükleyeceksiniz karşılık gelen bir .cer dosyası oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="27def-189">The following command in the example below will create and install a root certificate in the Personal certificate store on your workstation and also create a corresponding .cer file that you’ll later upload to the Azure Classic Portal.</span></span>

        makecert -sky exchange -r -n "CN=HBaseVnetVPNRootCertificate" -pe -a sha1 -len 2048 -ss My "C:\Users\JohnDole\Desktop\HBaseVNetVPNRootCertificate.cer"

    <span data-ttu-id="27def-190">.Cer dosyasının, HBaseVnetVPNRootCertificate sertifika için kullanmak istediğiniz adı olduğu yer istediğiniz dizine geçin.</span><span class="sxs-lookup"><span data-stu-id="27def-190">Change to the directory that you want the .cer file to be located in, where HBaseVnetVPNRootCertificate is the name that you want to use for the certificate.</span></span>

    <span data-ttu-id="27def-191">Komut istemi kapatmayın.</span><span class="sxs-lookup"><span data-stu-id="27def-191">Don't close the command prompt.</span></span>  <span data-ttu-id="27def-192">Sonraki yordamda gerekir.</span><span class="sxs-lookup"><span data-stu-id="27def-192">You will need it in the next procedure.</span></span>

   > [!NOTE]
   > <span data-ttu-id="27def-193">Kendisinden istemci sertifikaları oluşturulacak bir kök sertifikası oluşturduğunuzdan, bu sertifikayı ve özel anahtarını dışarı aktarıp ileride kurtarma amaçlı kullanabileceğiniz güvenli bir konuma kaydetmek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="27def-193">Because you have created a root certificate from which client certificates will be generated, you may want to export this certificate along with its private key and save it to a safe location where it may be recovered.</span></span>
   >
   >

<span data-ttu-id="27def-194">**Bir istemci sertifikası oluşturmak için**</span><span class="sxs-lookup"><span data-stu-id="27def-194">**To create a client certificate**</span></span>

* <span data-ttu-id="27def-195">Aynı komut istemini (Bu bilgisayarın kök sertifikanın oluşturulduğu bilgisayarda olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="27def-195">From the same command prompt (It has to be on the same computer where you created the root certificate.</span></span> <span data-ttu-id="27def-196">İstemci sertifikası oluşturulmalıdır kök sertifikası), aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="27def-196">The client certificate must be generated from the root certificate), run the following command:</span></span>

          makecert.exe -n "CN=HBaseVnetVPNClientCertificate" -pe -sky exchange -m 96 -ss My -in "HBaseVnetVPNRootCertificate" -is my -a sha1

    <span data-ttu-id="27def-197">HBaseVnetVPNRootCertificate kök sertifika addır.</span><span class="sxs-lookup"><span data-stu-id="27def-197">HBaseVnetVPNRootCertificate is the root certificate name.</span></span>  <span data-ttu-id="27def-198">Bu kök sertifika adı eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="27def-198">It has to match the root certificate name.</span></span>  

    <span data-ttu-id="27def-199">Kök sertifikayı ve istemci sertifikası, bilgisayarınızdaki kişisel sertifika deposunda depolanır.</span><span class="sxs-lookup"><span data-stu-id="27def-199">Both the root certificate and the client certificate are stored in your Personal certificate store on your computer.</span></span> <span data-ttu-id="27def-200">Certmgr.msc doğrulamak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="27def-200">Use certmgr.msc to verify.</span></span>

    ![Azure sanal ağı noktadan siteye VPN sertifikası][img-certificate]

    <span data-ttu-id="27def-202">Sanal ağa bağlamak istediğiniz her bilgisayara bir istemci sertifikası yüklenmelidir.</span><span class="sxs-lookup"><span data-stu-id="27def-202">A client certificate must be installed on each computer that you want to connect to the virtual network.</span></span> <span data-ttu-id="27def-203">Sanal ağa bağlamak istediğiniz her bilgisayar için benzersiz istemci sertifikaları oluşturmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="27def-203">We recommend that you create unique client certificates for each computer that you want to connect to the virtual network.</span></span> <span data-ttu-id="27def-204">İstemci sertifikaları vermek için certmgr.msc kullanın.</span><span class="sxs-lookup"><span data-stu-id="27def-204">To export the client certificates, use certmgr.msc.</span></span>

<span data-ttu-id="27def-205">**Klasik Azure portalı kök sertifikayı karşıya yüklemek için**</span><span class="sxs-lookup"><span data-stu-id="27def-205">**To upload the root certificate to the Azure Classic Portal**</span></span>

1. <span data-ttu-id="27def-206">Azure Klasik portalından tıklatın **ağ** soldaki.</span><span class="sxs-lookup"><span data-stu-id="27def-206">From the Azure Classic Portal, click **NETWORK** on the left.</span></span>
2. <span data-ttu-id="27def-207">HBase kümesi dağıtıldığı sanal ağ'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="27def-207">Click the virtual network where your HBase cluster is deployed to.</span></span>
3. <span data-ttu-id="27def-208">Tıklatın **SERTİFİKALARI** üstten.</span><span class="sxs-lookup"><span data-stu-id="27def-208">Click **CERTIFICATES** from the top.</span></span>
4. <span data-ttu-id="27def-209">Tıklatın **karşıya** Alttan ve son önce yordamda oluşturduğunuz kök sertifika dosyasını belirtin.</span><span class="sxs-lookup"><span data-stu-id="27def-209">Click **UPLOAD** from the bottom, and specify the root certificate file you have created in the procedure before last.</span></span> <span data-ttu-id="27def-210">Sertifika içeri kadar bekleyin.</span><span class="sxs-lookup"><span data-stu-id="27def-210">Wait until the certificate got imported.</span></span>
5. <span data-ttu-id="27def-211">Tıklatın **PANO** üstte.</span><span class="sxs-lookup"><span data-stu-id="27def-211">Click **DASHBOARD** on the top.</span></span>  <span data-ttu-id="27def-212">Sanal diyagramı durumu gösterilir.</span><span class="sxs-lookup"><span data-stu-id="27def-212">The virtual diagram shows the status.</span></span>

#### <a name="configure-your-vpn-client"></a><span data-ttu-id="27def-213">VPN istemcinizi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="27def-213">Configure your VPN client</span></span>
<span data-ttu-id="27def-214">**İndirmek ve istemci VPN paketini yüklemek için**</span><span class="sxs-lookup"><span data-stu-id="27def-214">**To download and install the client VPN package**</span></span>

1. <span data-ttu-id="27def-215">Hızlı Bakış bölümünde, sanal ağ PANOSU sayfasından tıklayın **64-bit istemci VPN paketini indir** veya **32 bit istemci VPN paketini indir** , iş istasyonunuzu işletim sistemi tabanlı Sürüm.</span><span class="sxs-lookup"><span data-stu-id="27def-215">From the DASHBOARD page of the virtual network, in the quick glance section, click either **Download the 64-bit Client VPN Package** or **Download the 32-bit Client VPN Package** based on your workstation OS version.</span></span>
2. <span data-ttu-id="27def-216">Tıklatın **çalıştırmak** paketi yüklemek için.</span><span class="sxs-lookup"><span data-stu-id="27def-216">Click **Run** to install the package.</span></span>
3. <span data-ttu-id="27def-217">Güvenlik isteminde tıklatın **daha fazla bilgi**ve ardından **yine de çalıştırmaya**.</span><span class="sxs-lookup"><span data-stu-id="27def-217">At the security prompt, click **More info**, and then click **Run anyway**.</span></span>
4. <span data-ttu-id="27def-218">Tıklatın **Evet** iki kez.</span><span class="sxs-lookup"><span data-stu-id="27def-218">Click **Yes** twice.</span></span>

<span data-ttu-id="27def-219">**VPN'ye bağlanmak için**</span><span class="sxs-lookup"><span data-stu-id="27def-219">**To connect to VPN**</span></span>

1. <span data-ttu-id="27def-220">İş istasyonunuzu masaüstünde, görev çubuğunda ağ simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="27def-220">On the desktop of your workstation, click the Networks icon on the Task bar.</span></span> <span data-ttu-id="27def-221">Bir VPN bağlantısı, sanal ağ adıyla göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="27def-221">You shall see a VPN connection with your virtual network name.</span></span>
2. <span data-ttu-id="27def-222">VPN bağlantısı adını tıklatın.</span><span class="sxs-lookup"><span data-stu-id="27def-222">Click the VPN connection name.</span></span>
3. <span data-ttu-id="27def-223">**Bağlan**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="27def-223">Click **Connect**.</span></span>

<span data-ttu-id="27def-224">**VPN bağlantısı ve etki alanı ad çözümlemesini test etmek için**</span><span class="sxs-lookup"><span data-stu-id="27def-224">**To test the VPN connection and domain name resolution**</span></span>

* <span data-ttu-id="27def-225">İş istasyonundan, bir komut istemi açın ve ping HBase kümenin DNS soneki verilen aşağıdaki adlarından birini myhbase.b7.internal.cloudapp.net ise:</span><span class="sxs-lookup"><span data-stu-id="27def-225">From the workstation, open a command prompt and ping one of the following names given the HBase cluster's DNS suffix is myhbase.b7.internal.cloudapp.net:</span></span>

        zookeeper0.myhbase.b7.internal.cloudapp.net
        zookeeper0.myhbase.b7.internal.cloudapp.net
        zookeeper0.myhbase.b7.internal.cloudapp.net
        headnode0.myhbase.b7.internal.cloudapp.net
        headnode1.myhbase.b7.internal.cloudapp.net
        workernode0.myhbase.b7.internal.cloudapp.net

### <a name="install-and-configure-squirrel-on-your-workstation"></a><span data-ttu-id="27def-226">Yükleme ve SQuirreL iş istasyonunuza yapılandırma</span><span class="sxs-lookup"><span data-stu-id="27def-226">Install and configure SQuirreL on your workstation</span></span>
<span data-ttu-id="27def-227">**SQuirreL yüklemek için**</span><span class="sxs-lookup"><span data-stu-id="27def-227">**To install SQuirreL**</span></span>

1. <span data-ttu-id="27def-228">SQuirreL SQL istemci jar dosyasını indirin [http://squirrel-sql.sourceforge.net/#installation](http://squirrel-sql.sourceforge.net/#installation).</span><span class="sxs-lookup"><span data-stu-id="27def-228">Download the SQuirreL SQL client jar file from [http://squirrel-sql.sourceforge.net/#installation](http://squirrel-sql.sourceforge.net/#installation).</span></span>
2. <span data-ttu-id="27def-229">Jar dosyasını açma veya çalıştırma.</span><span class="sxs-lookup"><span data-stu-id="27def-229">Open/run the jar file.</span></span> <span data-ttu-id="27def-230">Gerektirdiği [Java Çalışma zamanı ortamı](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html).</span><span class="sxs-lookup"><span data-stu-id="27def-230">It requires the [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html).</span></span>
3. <span data-ttu-id="27def-231">Tıklatın **sonraki** iki kez.</span><span class="sxs-lookup"><span data-stu-id="27def-231">Click **Next** twice.</span></span>
4. <span data-ttu-id="27def-232">Burada, yazma izni ve ardından bir yol belirtin **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="27def-232">Specify a path where you have the write permission, and then click **Next**.</span></span>

  > [!NOTE]
  > <span data-ttu-id="27def-233">Varsayılan yükleme klasörü C:\Program Files\squirrel-sql-3.6 klasöründe bulunur.</span><span class="sxs-lookup"><span data-stu-id="27def-233">The default installation folder is in the C:\Program Files\squirrel-sql-3.6 folder.</span></span>  <span data-ttu-id="27def-234">Bu yolu yazmak için yükleyici yönetici ayrıcalığı verilmelidir.</span><span class="sxs-lookup"><span data-stu-id="27def-234">In order to write to this path, the installer must be granted the administrator privilege.</span></span> <span data-ttu-id="27def-235">Yönetici olarak bir komut istemi açın, Java'nın depo klasörüne gidin ve ardından çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="27def-235">You can open a command prompt as administrator, navigate to Java's bin folder, and then run:</span></span>
  >
  >     <span data-ttu-id="27def-236">Java.exe-jar [SQuirreL jar dosyasının yolu]</span><span class="sxs-lookup"><span data-stu-id="27def-236">java.exe -jar [the path of the SQuirreL jar file]</span></span>
5. <span data-ttu-id="27def-237">Tıklatın **Tamam** hedef dizin oluşturma onaylamak için.</span><span class="sxs-lookup"><span data-stu-id="27def-237">Click **OK** to confirm creating the target directory.</span></span>
6. <span data-ttu-id="27def-238">Temel ve standart paketleri yüklemek için varsayılan ayardır.</span><span class="sxs-lookup"><span data-stu-id="27def-238">The default setting is to install the Base and Standard packages.</span></span>  <span data-ttu-id="27def-239">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="27def-239">Click **Next**.</span></span>
7. <span data-ttu-id="27def-240">Tıklatın **sonraki** iki kez tıkladıktan sonra **Bitti**.</span><span class="sxs-lookup"><span data-stu-id="27def-240">Click **Next** twice, and then click **Done**.</span></span>

<span data-ttu-id="27def-241">**Phoenix sürücüyü yüklemek için**</span><span class="sxs-lookup"><span data-stu-id="27def-241">**To install the Phoenix driver**</span></span>

<span data-ttu-id="27def-242">Phoenix sürücü jar dosyasını HBase kümesi bulunur.</span><span class="sxs-lookup"><span data-stu-id="27def-242">The phoenix driver jar file is located on the HBase cluster.</span></span> <span data-ttu-id="27def-243">Yolu sürümlerine bağlı aşağıdakine benzer:</span><span class="sxs-lookup"><span data-stu-id="27def-243">The path is similar to the following based on the versions:</span></span>

    C:\apps\dist\phoenix-4.0.0.2.1.11.0-2316\phoenix-4.0.0.2.1.11.0-2316-client.jar
<span data-ttu-id="27def-244">İhtiyacınız olan [SQuirreL yükleme klasörü] altında iş istasyonunuzu kopyalayın / lib yolu.</span><span class="sxs-lookup"><span data-stu-id="27def-244">You need to copy it to your workstation under the [SQuirreL installation folder]/lib path.</span></span>  <span data-ttu-id="27def-245">En kolay yolu için RDP kümesine olduğundan ve dosya kopyalayıp yapıştırın (CTRL + C ve CTRL + V) istasyonunuza kopyalamak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="27def-245">The easiest way is to RDP into the cluster, and then use file copy/paste (CTRL+C and CTRL+V) to copy it to your workstation.</span></span>

<span data-ttu-id="27def-246">**Phoenix sürücüsü için SQuirreL eklemek için**</span><span class="sxs-lookup"><span data-stu-id="27def-246">**To add a Phoenix driver to SQuirreL**</span></span>

1. <span data-ttu-id="27def-247">SQuirreL SQL istemci istasyonunuzdan açın.</span><span class="sxs-lookup"><span data-stu-id="27def-247">Open SQuirreL SQL Client from your workstation.</span></span>
2. <span data-ttu-id="27def-248">Tıklatın **sürücü** sol sekmesinde.</span><span class="sxs-lookup"><span data-stu-id="27def-248">Click the **Driver** tab on the left.</span></span>
3. <span data-ttu-id="27def-249">Gelen **sürücüleri** menüsünde tıklatın **yeni sürücü**.</span><span class="sxs-lookup"><span data-stu-id="27def-249">From the **Drivers** menu, click **New Driver**.</span></span>
4. <span data-ttu-id="27def-250">Aşağıdaki bilgileri girin:</span><span class="sxs-lookup"><span data-stu-id="27def-250">Enter the following information:</span></span>

   * <span data-ttu-id="27def-251">**Ad**: Phoenix</span><span class="sxs-lookup"><span data-stu-id="27def-251">**Name**: Phoenix</span></span>
   * <span data-ttu-id="27def-252">**Örnek URL**: jdbc:phoenix:zookeeper2.contoso hbase eu.f5.internal.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="27def-252">**Example URL**: jdbc:phoenix:zookeeper2.contoso-hbase-eu.f5.internal.cloudapp.net</span></span>
   * <span data-ttu-id="27def-253">**Sınıf adı**: org.apache.phoenix.jdbc.PhoenixDriver</span><span class="sxs-lookup"><span data-stu-id="27def-253">**Class Name**: org.apache.phoenix.jdbc.PhoenixDriver</span></span>

     > [!WARNING]
     > <span data-ttu-id="27def-254">Kullanıcı örnek URL tüm alt durumda.</span><span class="sxs-lookup"><span data-stu-id="27def-254">User all lower case in the Example URL.</span></span> <span data-ttu-id="27def-255">Kullanabileceğiniz bunlar tam zookeeper çekirdek bunlardan birini çalışmıyor durumda.</span><span class="sxs-lookup"><span data-stu-id="27def-255">You can use they full zookeeper quorum in case one of them is down.</span></span>  <span data-ttu-id="27def-256">Konak zookeeper0, zookeeper1 ve zookeeper2 adları.</span><span class="sxs-lookup"><span data-stu-id="27def-256">The hostnames are zookeeper0, zookeeper1, and zookeeper2.</span></span>
     >
     >

     ![Hdınsight HBase Phoenix SQuirreL sürücüsü][img-squirrel-driver]
5. <span data-ttu-id="27def-258">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="27def-258">Click **OK**.</span></span>

<span data-ttu-id="27def-259">**HBase kümesi için bir diğer adı oluşturmak için**</span><span class="sxs-lookup"><span data-stu-id="27def-259">**To create an alias to the HBase cluster**</span></span>

1. <span data-ttu-id="27def-260">SQuirreL tıklatın **diğer adlar** sol sekmesinde.</span><span class="sxs-lookup"><span data-stu-id="27def-260">From SQuirreL, Click the **Aliases** tab on the left.</span></span>
2. <span data-ttu-id="27def-261">Gelen **diğer adlar** menüsünde tıklatın **yeni diğer**.</span><span class="sxs-lookup"><span data-stu-id="27def-261">From the **Aliases** menu, click **New Alias**.</span></span>
3. <span data-ttu-id="27def-262">Aşağıdaki bilgileri girin:</span><span class="sxs-lookup"><span data-stu-id="27def-262">Enter the following information:</span></span>

   * <span data-ttu-id="27def-263">**Ad**: HBase kümesi veya tercih ettiğiniz herhangi bir ad adı.</span><span class="sxs-lookup"><span data-stu-id="27def-263">**Name**: The name of the HBase cluster or any name you prefer.</span></span>
   * <span data-ttu-id="27def-264">**Sürücü**: Phoenix.</span><span class="sxs-lookup"><span data-stu-id="27def-264">**Driver**: Phoenix.</span></span>  <span data-ttu-id="27def-265">Bu son yordamda oluşturduğunuz sürücü adı eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="27def-265">This must match the driver name you created in the last procedure.</span></span>
   * <span data-ttu-id="27def-266">**URL**: URL, sürücü yapılandırmasından kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="27def-266">**URL**: The URL is copied from your driver configuration.</span></span> <span data-ttu-id="27def-267">Kullanıcı için tüm küçük emin olun.</span><span class="sxs-lookup"><span data-stu-id="27def-267">Make sure to user all lower case.</span></span>
   * <span data-ttu-id="27def-268">**Kullanıcı adı**: herhangi bir metin olabilir.</span><span class="sxs-lookup"><span data-stu-id="27def-268">**User name**: It can be any text.</span></span>  <span data-ttu-id="27def-269">VPN bağlantısı burada kullandığından, kullanıcı adı hiç kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="27def-269">Because you use VPN connectivity here, the user name is not used at all.</span></span>
   * <span data-ttu-id="27def-270">**Parola**: herhangi bir metin olabilir.</span><span class="sxs-lookup"><span data-stu-id="27def-270">**Password**: It can be any text.</span></span>

     ![Hdınsight HBase Phoenix SQuirreL sürücüsü][img-squirrel-alias]
4. <span data-ttu-id="27def-272">Tıklatın **Test**.</span><span class="sxs-lookup"><span data-stu-id="27def-272">Click **Test**.</span></span>
5. <span data-ttu-id="27def-273">**Bağlan**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="27def-273">Click **Connect**.</span></span> <span data-ttu-id="27def-274">Bağlantı yaptığında, SQuirreL şuna benzer:</span><span class="sxs-lookup"><span data-stu-id="27def-274">When it makes the connection, SQuirreL looks like:</span></span>

    ![HBase Phoenix SQuirreL][img-squirrel]

<span data-ttu-id="27def-276">**Bir test çalıştırmak için**</span><span class="sxs-lookup"><span data-stu-id="27def-276">**To run a test**</span></span>

1. <span data-ttu-id="27def-277">Tıklatın **SQL** sekmesinde İleri sağa **nesneleri** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="27def-277">Click the **SQL** tab right next to the **Objects** tab.</span></span>
2. <span data-ttu-id="27def-278">Aşağıdaki kodu kopyalayıp yapıştırın:</span><span class="sxs-lookup"><span data-stu-id="27def-278">Copy and paste the following code:</span></span>

        CREATE TABLE IF NOT EXISTS us_population (state CHAR(2) NOT NULL, city VARCHAR NOT NULL, population BIGINT  CONSTRAINT my_pk PRIMARY KEY (state, city))
3. <span data-ttu-id="27def-279">Çalıştırma düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="27def-279">Click the run button.</span></span>

    ![HBase Phoenix SQuirreL][img-squirrel-sql]
4. <span data-ttu-id="27def-281">Dönmek **nesneleri** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="27def-281">Switch back to the **Objects** tab.</span></span>
5. <span data-ttu-id="27def-282">Diğer adı'nı genişletin ve ardından genişletin **tablo**.</span><span class="sxs-lookup"><span data-stu-id="27def-282">Expand the alias name, and then expand **TABLE**.</span></span>  <span data-ttu-id="27def-283">Altında listelenen yeni tablo görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="27def-283">You shall see the new table listed under.</span></span>

## <a name="next-steps"></a><span data-ttu-id="27def-284">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="27def-284">Next steps</span></span>
<span data-ttu-id="27def-285">Bu makalede, Hdınsight'ta Apache Phoenix kullanmayı öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="27def-285">In this article, you have learned how to use Apache Phoenix in HDInsight.</span></span>  <span data-ttu-id="27def-286">Daha fazla bilgi için bkz:</span><span class="sxs-lookup"><span data-stu-id="27def-286">To learn more, see</span></span>

* <span data-ttu-id="27def-287">[HDInsight HBase'e genel bakış][hdinsight-hbase-overview]: HBase büyük miktarda yapılandırılmamış ve yarı yapılandırılmış veri için rastgele erişim ve güçlü tutarlılık sağlayan, Hadoop'ta yerleşik bir Apache, açık kaynak, NoSQL veritabanıdır.</span><span class="sxs-lookup"><span data-stu-id="27def-287">[HDInsight HBase overview][hdinsight-hbase-overview]: HBase is an Apache, open-source, NoSQL database built on Hadoop that provides random access and strong consistency for large amounts of unstructured and semistructured data.</span></span>
* <span data-ttu-id="27def-288">[Azure Virtual Network HBase kümelerine sağlamak][hdinsight-hbase-provision-vnet]: uygulamalar HBase ile iletişim kurabilmesi için sanal ağ tümleştirmesinin ile HBase kümeleri aynı sanal ağ, uygulamalarınızın dağıtılabilir doğrudan.</span><span class="sxs-lookup"><span data-stu-id="27def-288">[Provision HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet]: With virtual network integration, HBase clusters can be deployed to the same virtual network as your applications so that applications can communicate with HBase directly.</span></span>
* <span data-ttu-id="27def-289">[Hdınsight'ta HBase çoğaltmayı yapılandırma](hdinsight-hbase-replication.md): HBase çoğaltmayı iki Azure veri merkezi arasında yapılandırmayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="27def-289">[Configure HBase replication in HDInsight](hdinsight-hbase-replication.md): Learn how to configure HBase replication across two Azure datacenters.</span></span>
* <span data-ttu-id="27def-290">[Hdınsight'ta HBase ile twitter düşüncelerini çözümleme][hbase-twitter-sentiment]: Gerçek zamanlı nasıl [düşünceleri analiz](http://en.wikipedia.org/wiki/Sentiment_analysis) HBase hdınsight'ta Hadoop kümesi kullanarak büyük veri.</span><span class="sxs-lookup"><span data-stu-id="27def-290">[Analyze Twitter sentiment with HBase in HDInsight][hbase-twitter-sentiment]: Learn how to do real-time [sentiment analysis](http://en.wikipedia.org/wiki/Sentiment_analysis) of big data by using HBase in a Hadoop cluster in HDInsight.</span></span>

[azure-portal]: https://portal.azure.com
[vnet-point-to-site-connectivity]: https://msdn.microsoft.com/library/azure/09926218-92ab-4f43-aa99-83ab4d355555#BKMK_VNETPT

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-hbase-get-started]: hdinsight-hbase-tutorial-get-started.md
[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md

[hdinsight-hbase-phoenix-sqlline]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-phoenix-sqlline.png
[img-certificate]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vpn-certificate.png
[img-vnet-diagram]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vnet-point-to-site.png
[img-squirrel-driver]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-driver.png
[img-squirrel-alias]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-alias.png
[img-squirrel]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel.png
[img-squirrel-sql]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-sql.png
