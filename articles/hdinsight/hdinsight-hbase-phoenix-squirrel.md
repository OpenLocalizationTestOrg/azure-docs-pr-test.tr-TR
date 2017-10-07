---
title: "Apache Phoenix aaaUse ve Windows tabanlı Azure Hdınsight ile SQuirreL | Microsoft Docs"
description: "Bilgi nasıl toouse, hdınsight'ta Apache Phoenix ve nasıl tooinstall ve SQuirreL iş istasyonu tooconnect tooan HBase kümeniz hdınsight'ta yapılandırın."
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
ms.openlocfilehash: 147ac35fa882fd1bedbc5361ac804c36a4d56de1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-phoenix-and-squirrel-with-windows-based-hbase-clusters-in-hdinsight"></a><span data-ttu-id="2b698-103">Hdınsight'ta Windows tabanlı HBase kümeleriyle Apache ve SQuirreL kullanma</span><span class="sxs-lookup"><span data-stu-id="2b698-103">Use Apache Phoenix and SQuirreL with Windows-based HBase clusters in HDInsight</span></span>
<span data-ttu-id="2b698-104">Bilgi nasıl toouse [Apache Phoenix](http://phoenix.apache.org/) , hdınsight'ta ve nasıl tooinstall ve SQuirreL iş istasyonu tooconnect tooan HBase kümeniz hdınsight'ta yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="2b698-104">Learn how toouse [Apache Phoenix](http://phoenix.apache.org/) in HDInsight, and how tooinstall and configure SQuirreL on your workstation tooconnect tooan HBase cluster in HDInsight.</span></span> <span data-ttu-id="2b698-105">Phoenix hakkında daha fazla bilgi için bkz: [Phoenix 15 dakika veya daha az](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html).</span><span class="sxs-lookup"><span data-stu-id="2b698-105">For more information about Phoenix, see [Phoenix in 15 minutes or less](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html).</span></span> <span data-ttu-id="2b698-106">Hello Phoenix dilbilgisi için bkz: [Phoenix Dilbilgisi](http://phoenix.apache.org/language/index.html).</span><span class="sxs-lookup"><span data-stu-id="2b698-106">For hello Phoenix grammar, see [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

> [!NOTE]
> <span data-ttu-id="2b698-107">Hello hdınsight'ta Phoenix sürüm bilgileri için bkz: [Hdınsight tarafından sağlanan hello Hadoop küme sürümlerindeki yenilikler nelerdir?](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="2b698-107">For hello Phoenix version information in HDInsight, see [What's new in hello Hadoop cluster versions provided by HDInsight?](hdinsight-component-versioning.md).</span></span>
>

> [!IMPORTANT]
> <span data-ttu-id="2b698-108">Bu belge yalnızca iş için Windows tabanlı Hdınsight kümeleri Hello adımları.</span><span class="sxs-lookup"><span data-stu-id="2b698-108">hello steps in this document only work for Windows-based HDInsight clusters.</span></span> <span data-ttu-id="2b698-109">Hdınsight yalnızca Windows'da Hdınsight 3.4 ' düşük sürümleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="2b698-109">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="2b698-110">Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir.</span><span class="sxs-lookup"><span data-stu-id="2b698-110">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="2b698-111">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="2b698-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="2b698-112">Phoenix Linux tabanlı Hdınsight kullanma hakkında daha fazla bilgi için bkz: [Hdınsight'ta Linux tabanlı HBase ile kullanım Apache Phoenix kümeleri](hdinsight-hbase-phoenix-squirrel-linux.md).</span><span class="sxs-lookup"><span data-stu-id="2b698-112">For information on using Phoenix on Linux-based HDInsight, see [Use Apache Phoenix with Linux-based HBase clusters in HDInsight](hdinsight-hbase-phoenix-squirrel-linux.md).</span></span>
>



## <a name="use-sqlline"></a><span data-ttu-id="2b698-113">SQLLine kullanın</span><span class="sxs-lookup"><span data-stu-id="2b698-113">Use SQLLine</span></span>
<span data-ttu-id="2b698-114">[SQLLine](http://sqlline.sourceforge.net/) bir komut satırı yardımcı programı tooexecute SQL değil.</span><span class="sxs-lookup"><span data-stu-id="2b698-114">[SQLLine](http://sqlline.sourceforge.net/) is a command line utility tooexecute SQL.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="2b698-115">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="2b698-115">Prerequisites</span></span>
<span data-ttu-id="2b698-116">SQLLine kullanmadan önce hello şunlara sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="2b698-116">Before you can use SQLLine, you must have hello following:</span></span>

* <span data-ttu-id="2b698-117">**Hdınsight'ta HBase kümesi**.</span><span class="sxs-lookup"><span data-stu-id="2b698-117">**A HBase cluster in HDInsight**.</span></span> <span data-ttu-id="2b698-118">Küme hazırlama HBase hakkında bilgi için bkz: [hdınsight'ta Apache HBase kullanmaya başlama][hdinsight-hbase-get-started].</span><span class="sxs-lookup"><span data-stu-id="2b698-118">For information on provision HBase cluster, see [Get started with Apache HBase in HDInsight][hdinsight-hbase-get-started].</span></span>
* <span data-ttu-id="2b698-119">**Toohello HBase kümesi hello Uzak Masaüstü Protokolü aracılığıyla bağlanma**.</span><span class="sxs-lookup"><span data-stu-id="2b698-119">**Connect toohello HBase cluster via hello remote desktop protocol**.</span></span> <span data-ttu-id="2b698-120">Yönergeler için bkz: [yönetmek Hdınsight'ta Hadoop kümeleri hello Klasik Azure portalı kullanarak][hdinsight-manage-portal].</span><span class="sxs-lookup"><span data-stu-id="2b698-120">For instructions, see [Manage Hadoop clusters in HDInsight by using hello Azure Classic Portal][hdinsight-manage-portal].</span></span>

<span data-ttu-id="2b698-121">**toofind hello ana bilgisayar adı çıkışı**</span><span class="sxs-lookup"><span data-stu-id="2b698-121">**toofind out hello host name**</span></span>

1. <span data-ttu-id="2b698-122">Açık **Hadoop komut satırı** hello masaüstünden.</span><span class="sxs-lookup"><span data-stu-id="2b698-122">Open **Hadoop Command Line** from hello desktop.</span></span>
2. <span data-ttu-id="2b698-123">Komut tooget hello DNS soneki aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="2b698-123">Run hello following command tooget hello DNS suffix:</span></span>

        ipconfig

    <span data-ttu-id="2b698-124">Yazma **bağlantıya özgü DNS soneki**.</span><span class="sxs-lookup"><span data-stu-id="2b698-124">Write down **Connection-specific DNS Suffix**.</span></span> <span data-ttu-id="2b698-125">Örneğin, *myhbasecluster.f5.internal.cloudapp.net*.</span><span class="sxs-lookup"><span data-stu-id="2b698-125">For example, *myhbasecluster.f5.internal.cloudapp.net*.</span></span> <span data-ttu-id="2b698-126">Tooan HBase kümesi bağlandığınızda, FQDN kullanarak hello Zookeepers, tooconnect tooone gerekir.</span><span class="sxs-lookup"><span data-stu-id="2b698-126">When you connect tooan HBase cluster, you will need tooconnect tooone of hello Zookeepers using FQDN.</span></span> <span data-ttu-id="2b698-127">Her Hdınsight kümesi 3 Zookeepers sahiptir.</span><span class="sxs-lookup"><span data-stu-id="2b698-127">Each HDInsight cluster has 3 Zookeepers.</span></span> <span data-ttu-id="2b698-128">Bunlar *zookeeper0*, *zookeeper1*, ve *zookeeper2*.</span><span class="sxs-lookup"><span data-stu-id="2b698-128">They are *zookeeper0*, *zookeeper1*, and *zookeeper2*.</span></span> <span data-ttu-id="2b698-129">Merhaba FQDN şöyle olacaktır *zookeeper2.myhbasecluster.f5.internal.cloudapp.net*.</span><span class="sxs-lookup"><span data-stu-id="2b698-129">hello FQDN will be something like *zookeeper2.myhbasecluster.f5.internal.cloudapp.net*.</span></span>

<span data-ttu-id="2b698-130">**toouse SQLLine**</span><span class="sxs-lookup"><span data-stu-id="2b698-130">**toouse SQLLine**</span></span>

1. <span data-ttu-id="2b698-131">Açık **Hadoop komut satırı** hello masaüstünden.</span><span class="sxs-lookup"><span data-stu-id="2b698-131">Open **Hadoop Command Line** from hello desktop.</span></span>
2. <span data-ttu-id="2b698-132">Aşağıdaki komutları tooopen SQLLine hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="2b698-132">Run hello following commands tooopen SQLLine:</span></span>

        cd %phoenix_home%\bin
        sqlline.py [hello FQDN of one of hello Zookeepers]

    ![Hdınsight hbase phoenix sqlline][hdinsight-hbase-phoenix-sqlline]

    <span data-ttu-id="2b698-134">Merhaba örnekte kullanılan hello komutlar:</span><span class="sxs-lookup"><span data-stu-id="2b698-134">hello commands used in hello sample:</span></span>

        CREATE TABLE Company (COMPANY_ID INTEGER PRIMARY KEY, NAME VARCHAR(225));

        !tables

        UPSERT INTO Company VALUES(1, 'Microsoft');

        SELECT * FROM Company;

<span data-ttu-id="2b698-135">Daha fazla bilgi için bkz: [SQLLine el ile](http://sqlline.sourceforge.net/#manual) ve [Phoenix Dilbilgisi](http://phoenix.apache.org/language/index.html).</span><span class="sxs-lookup"><span data-stu-id="2b698-135">For more information, see [SQLLine manual](http://sqlline.sourceforge.net/#manual) and [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

## <a name="use-squirrel"></a><span data-ttu-id="2b698-136">SQuirreL kullanma</span><span class="sxs-lookup"><span data-stu-id="2b698-136">Use SQuirreL</span></span>
<span data-ttu-id="2b698-137">[SQL istemci sQuirreL](http://squirrel-sql.sourceforge.net/) tooview hello yapısı JDBC uyumlu bir veritabanına izin, tablolardaki hello verileri göz atın, sorunu SQL komutlarını vb. grafik bir Java programdır. Kullanılan tooconnect tooApache hdınsight'ta Phoenix olabilir.</span><span class="sxs-lookup"><span data-stu-id="2b698-137">[SQuirreL SQL Client](http://squirrel-sql.sourceforge.net/) is a graphical Java program that will allow you tooview hello structure of a JDBC compliant database, browse hello data in tables, issue SQL commands etc. It can be used tooconnect tooApache Phoenix on HDInsight.</span></span>

<span data-ttu-id="2b698-138">Bu bölümde, nasıl gösterilir tooinstall ve SQuirreL iş istasyonu tooconnect tooan HBase kümeniz hdınsight'ta VPN aracılığıyla yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="2b698-138">This section shows you how tooinstall and configure SQuirreL on your workstation tooconnect tooan HBase cluster in HDInsight via VPN.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="2b698-139">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="2b698-139">Prerequisites</span></span>
<span data-ttu-id="2b698-140">Merhaba yordamları izlemeden önce hello şunlara sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="2b698-140">Before following hello procedures, you must have hello following:</span></span>

* <span data-ttu-id="2b698-141">Bir HBase kümesi tooan bir DNS sanal makineye sahip Azure sanal ağı dağıtıldı.</span><span class="sxs-lookup"><span data-stu-id="2b698-141">An HBase cluster deployed tooan Azure virtual network with a DNS virtual machine.</span></span>  <span data-ttu-id="2b698-142">Yönergeler için bkz: [oluşturma HBase kümeleri Azure sanal ağı][hdinsight-hbase-provision-vnet].</span><span class="sxs-lookup"><span data-stu-id="2b698-142">For instructions, see [Create HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet].</span></span>

* <span data-ttu-id="2b698-143">Merhaba HBase kümesi küme bağlantıya özgü DNS soneki alın.</span><span class="sxs-lookup"><span data-stu-id="2b698-143">Get hello HBase cluster cluster Connection-specific DNS suffix.</span></span> <span data-ttu-id="2b698-144">tooget, hello küme halinde RDP ve ipconfig komutunu çalıştırmak.</span><span class="sxs-lookup"><span data-stu-id="2b698-144">tooget it, RDP into hello cluster, and then run IPConfig.</span></span>  <span data-ttu-id="2b698-145">Merhaba DNS soneki benzer:</span><span class="sxs-lookup"><span data-stu-id="2b698-145">hello DNS suffix is similar to:</span></span>

        myhbase.b7.internal.cloudapp.net
* <span data-ttu-id="2b698-146">İndirme ve yükleme [Microsoft Visual Studio Express için Windows Masaüstü](https://www.visualstudio.com/products/visual-studio-express-vs.aspx) istasyonunuzda.</span><span class="sxs-lookup"><span data-stu-id="2b698-146">Download and install [Microsoft Visual Studio Express for Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx) on your workstation.</span></span> <span data-ttu-id="2b698-147">Sertifikanızı hello paket toocreate gelen makecert gerekir.</span><span class="sxs-lookup"><span data-stu-id="2b698-147">You will need makecert from hello package toocreate your certificate.</span></span>  
* <span data-ttu-id="2b698-148">İndirme ve yükleme [Java Çalışma zamanı ortamı](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html) istasyonunuzda.</span><span class="sxs-lookup"><span data-stu-id="2b698-148">Download and install [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html) on your workstation.</span></span>  <span data-ttu-id="2b698-149">SQL istemci sürüm 3.0 ve daha yüksek sQuirreL JRE 1.6 veya sonraki sürümünü gerektirir.</span><span class="sxs-lookup"><span data-stu-id="2b698-149">SQuirreL SQL client version 3.0 and higher requires JRE version 1.6 or higher.</span></span>  

### <a name="configure-a-point-to-site-vpn-connection-toohello-azure-virtual-network"></a><span data-ttu-id="2b698-150">Bir noktadan siteye VPN bağlantısı toohello Azure sanal ağı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="2b698-150">Configure a Point-to-Site VPN connection toohello Azure virtual network</span></span>
<span data-ttu-id="2b698-151">Bir noktadan siteye VPN bağlantısı yapılandırma söz konusu 3 adım vardır:</span><span class="sxs-lookup"><span data-stu-id="2b698-151">There are 3 steps involved configuring a point-to-site VPN connection:</span></span>

1. [<span data-ttu-id="2b698-152">Bir sanal ağ ve dinamik yönlendirme ağ geçidi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="2b698-152">Configure a virtual network and a dynamic routing gateway</span></span>](#Configure-a-virtual-network-and-a-dynamic-routing-gateway)
2. [<span data-ttu-id="2b698-153">Sertifikalarınızı oluşturma</span><span class="sxs-lookup"><span data-stu-id="2b698-153">Create your certificates</span></span>](#Create-your-certificates)
3. [<span data-ttu-id="2b698-154">VPN istemcinizi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="2b698-154">Configure your VPN client</span></span>](#Configure-your-VPN-client)

<span data-ttu-id="2b698-155">Bkz: [bir noktadan siteye VPN bağlantısı tooan Azure Virtual Network yapılandırma](../vpn-gateway/vpn-gateway-point-to-site-create.md) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="2b698-155">See [Configure a Point-to-Site VPN connection tooan Azure Virtual Network](../vpn-gateway/vpn-gateway-point-to-site-create.md) for more information.</span></span>

#### <a name="configure-a-virtual-network-and-a-dynamic-routing-gateway"></a><span data-ttu-id="2b698-156">Bir sanal ağ ve dinamik yönlendirme ağ geçidi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="2b698-156">Configure a virtual network and a dynamic routing gateway</span></span>
<span data-ttu-id="2b698-157">Bir Azure sanal ağındaki bir HBase kümesi sağlanan güvence altına almak (Bu bölümün hello önkoşullara bakın).</span><span class="sxs-lookup"><span data-stu-id="2b698-157">Assure you have provisioned an HBase cluster in an Azure virtual network (see hello prerequisites for this section).</span></span> <span data-ttu-id="2b698-158">Merhaba sonraki tooconfigure bir noktadan siteye bağlantı adımdır.</span><span class="sxs-lookup"><span data-stu-id="2b698-158">hello next step is tooconfigure a point-to-site connection.</span></span>

<span data-ttu-id="2b698-159">**tooconfigure hello noktadan siteye bağlantı**</span><span class="sxs-lookup"><span data-stu-id="2b698-159">**tooconfigure hello point-to-site connectivity**</span></span>

1. <span data-ttu-id="2b698-160">İçinde toohello oturum [Klasik Azure portalı][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="2b698-160">Sign in toohello [Azure Classic Portal][azure-portal].</span></span>
2. <span data-ttu-id="2b698-161">Hello solda tıklatın **ağlar**.</span><span class="sxs-lookup"><span data-stu-id="2b698-161">On hello left, click **NETWORKS**.</span></span>
3. <span data-ttu-id="2b698-162">Oluşturduğunuz hello sanal ağa tıklayın (bkz [sağlama HBase kümeleri Azure sanal ağı][hdinsight-hbase-provision-vnet]).</span><span class="sxs-lookup"><span data-stu-id="2b698-162">Click hello virtual network you have created (see [Provision HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet]).</span></span>
4. <span data-ttu-id="2b698-163">Tıklatın **yapılandırma** hello üstten.</span><span class="sxs-lookup"><span data-stu-id="2b698-163">Click **CONFIGURE** from hello top.</span></span>
5. <span data-ttu-id="2b698-164">Merhaba, **noktadan siteye bağlantı** bölümünde, select **noktadan siteye bağlantı yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="2b698-164">In hello **point-to-site connectivity** section, select **Configure point-to-site connectivity**.</span></span>
6. <span data-ttu-id="2b698-165">Yapılandırma **başlangıç IP** ve **CIDR** bağlıyken toospecify hello IP adresi aralığı, VPN istemcilerinizin alır bir IP adresi.</span><span class="sxs-lookup"><span data-stu-id="2b698-165">Configure **STARTING IP** and **CIDR** toospecify hello IP address range from which your VPN clients will receive an IP address when connected.</span></span> <span data-ttu-id="2b698-166">Merhaba aralığı aralıklar, şirket içi üzerinde bulunan Ağ ve Azure sanal ağı için bağlanırsınız hello hello biriyle çakışamaz.</span><span class="sxs-lookup"><span data-stu-id="2b698-166">hello range cannot overlap with any of hello ranges located on your on-premises network and hello Azure virtual network you will be connecting to.</span></span> <span data-ttu-id="2b698-167">Örneğin.</span><span class="sxs-lookup"><span data-stu-id="2b698-167">For example.</span></span> <span data-ttu-id="2b698-168">Merhaba sanal ağ için 10.0.0.0/20 seçtiyseniz 10.1.0.0/24 hello istemci adres alanı için seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2b698-168">if you selected 10.0.0.0/20 for hello virtual network, you can select 10.1.0.0/24 for hello client address space.</span></span> <span data-ttu-id="2b698-169">Merhaba bkz [noktadan siteye bağlantı] [ vnet-point-to-site-connectivity] daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="2b698-169">See hello [Point-To-Site Connectivity][vnet-point-to-site-connectivity] page for more information.</span></span>
7. <span data-ttu-id="2b698-170">Merhaba sanal ağ adres alanları bölümünde tıklayın **ağ geçidi alt ağı eklemek**.</span><span class="sxs-lookup"><span data-stu-id="2b698-170">In hello virtual network address spaces section, click **add gateway subnet**.</span></span>
8. <span data-ttu-id="2b698-171">Tıklatın **KAYDETMEK** hello sayfanın hello üzerinde.</span><span class="sxs-lookup"><span data-stu-id="2b698-171">Click **SAVE** on hello bottom of hello page.</span></span>
9. <span data-ttu-id="2b698-172">Tıklatın **Evet** tooconfirm hello değiştirin.</span><span class="sxs-lookup"><span data-stu-id="2b698-172">Click **YES** tooconfirm hello change.</span></span> <span data-ttu-id="2b698-173">Merhaba sistem hello toohello sonraki yordama devam etmeden önce değiştirme yapmadan tamamlanana kadar bekleyin.</span><span class="sxs-lookup"><span data-stu-id="2b698-173">Wait until hello system has finished making hello change before you proceed toohello next procedure.</span></span>

<span data-ttu-id="2b698-174">**toocreate dinamik yönlendirme ağ geçidi**</span><span class="sxs-lookup"><span data-stu-id="2b698-174">**toocreate a dynamic routing gateway**</span></span>

1. <span data-ttu-id="2b698-175">Merhaba Klasik Azure Portalı ' tıklatın **PANO** hello sayfasının hello üstten.</span><span class="sxs-lookup"><span data-stu-id="2b698-175">From hello Azure Classic Portal, click **DASHBOARD** from hello top of hello page.</span></span>
2. <span data-ttu-id="2b698-176">Tıklatın **ağ geçidi Oluştur** hello sayfasının hello Alttan.</span><span class="sxs-lookup"><span data-stu-id="2b698-176">Click **CREATE GATEWAY** from hello bottom of hello page.</span></span>
3. <span data-ttu-id="2b698-177">Tıklatın **Evet** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="2b698-177">Click **YES** tooconfirm.</span></span> <span data-ttu-id="2b698-178">Merhaba ağ geçidi oluşturulana kadar bekleyin.</span><span class="sxs-lookup"><span data-stu-id="2b698-178">Wait until hello gateway is created.</span></span>
4. <span data-ttu-id="2b698-179">Tıklatın **PANO** hello üstten.</span><span class="sxs-lookup"><span data-stu-id="2b698-179">Click **DASHBOARD** from hello top.</span></span>  <span data-ttu-id="2b698-180">Merhaba sanal ağ visual diyagramı görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="2b698-180">You will see a visual diagram of hello virtual network:</span></span>

    ![Azure sanal ağı noktadan siteye sanal diyagramı][img-vnet-diagram]

    <span data-ttu-id="2b698-182">Merhaba diyagramı 0 istemci bağlantılarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="2b698-182">hello diagram shows 0 client connections.</span></span> <span data-ttu-id="2b698-183">Bir bağlantı toohello sanal ağ yaptıktan sonra hello numarası güncelleştirilmiş tooone olacaktır.</span><span class="sxs-lookup"><span data-stu-id="2b698-183">After you make a connection toohello virtual network, hello number will be updated tooone.</span></span>

#### <a name="create-your-certificates"></a><span data-ttu-id="2b698-184">Sertifikalarınızı oluşturma</span><span class="sxs-lookup"><span data-stu-id="2b698-184">Create your certificates</span></span>
<span data-ttu-id="2b698-185">Bir X.509 sertifikası olan kullanarak tek yönlü toocreate hello ile birlikte sertifika oluşturma Aracı (makecert.exe) [Microsoft Visual Studio Express için Windows Masaüstü](https://www.visualstudio.com/products/visual-studio-express-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="2b698-185">One way toocreate an X.509 certificate is by using hello Certificate Creation Tool (makecert.exe) that comes with [Microsoft Visual Studio Express for Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx).</span></span>

<span data-ttu-id="2b698-186">**toocreate otomatik olarak imzalanan sertifika**</span><span class="sxs-lookup"><span data-stu-id="2b698-186">**toocreate a self-signed root certificate**</span></span>

1. <span data-ttu-id="2b698-187">İstasyonunuzdan, bir komut istemi penceresi açın.</span><span class="sxs-lookup"><span data-stu-id="2b698-187">From your workstation, open a command prompt window.</span></span>
2. <span data-ttu-id="2b698-188">Toohello Visual Studio Araçları klasörüne gidin.</span><span class="sxs-lookup"><span data-stu-id="2b698-188">Navigate toohello Visual Studio tools folder.</span></span>
3. <span data-ttu-id="2b698-189">Aşağıdaki hello örnek komutta aşağıdaki hello oluşturur ve istasyonunuzda hello kişisel sertifika deposunda kök sertifikasını yükleyin ve ayrıca toohello Klasik Azure portalı daha sonra yükleyeceğiniz karşılık gelen bir .cer dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2b698-189">hello following command in hello example below will create and install a root certificate in hello Personal certificate store on your workstation and also create a corresponding .cer file that you’ll later upload toohello Azure Classic Portal.</span></span>

        makecert -sky exchange -r -n "CN=HBaseVnetVPNRootCertificate" -pe -a sha1 -len 2048 -ss My "C:\Users\JohnDole\Desktop\HBaseVNetVPNRootCertificate.cer"

    <span data-ttu-id="2b698-190">Bulunan, HBaseVnetVPNRootCertificate toouse hello sertifika için istediğiniz hello adı olduğu .cer dosyasını toobe hello istediğiniz toohello dizini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="2b698-190">Change toohello directory that you want hello .cer file toobe located in, where HBaseVnetVPNRootCertificate is hello name that you want toouse for hello certificate.</span></span>

    <span data-ttu-id="2b698-191">Merhaba komut istemi kapatmayın.</span><span class="sxs-lookup"><span data-stu-id="2b698-191">Don't close hello command prompt.</span></span>  <span data-ttu-id="2b698-192">Merhaba sonraki yordamda gerekir.</span><span class="sxs-lookup"><span data-stu-id="2b698-192">You will need it in hello next procedure.</span></span>

   > [!NOTE]
   > <span data-ttu-id="2b698-193">İstemci sertifikaları oluşturulacak bir kök sertifikası oluşturduğunuzdan, bu sertifikayı ve özel anahtarını tooexport istediğiniz ve burada kurtarılabilir tooa güvenli konuma kaydedin.</span><span class="sxs-lookup"><span data-stu-id="2b698-193">Because you have created a root certificate from which client certificates will be generated, you may want tooexport this certificate along with its private key and save it tooa safe location where it may be recovered.</span></span>
   >
   >

<span data-ttu-id="2b698-194">**toocreate bir istemci sertifikası**</span><span class="sxs-lookup"><span data-stu-id="2b698-194">**toocreate a client certificate**</span></span>

* <span data-ttu-id="2b698-195">Hello aynı komut istemi (Merhaba üzerinde toobe sahip hello kök sertifikanın oluşturulduğu aynı bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="2b698-195">From hello same command prompt (It has toobe on hello same computer where you created hello root certificate.</span></span> <span data-ttu-id="2b698-196">Merhaba istemci sertifikası oluşturulmalıdır hello kök sertifikasından), çalışma hello komutu aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="2b698-196">hello client certificate must be generated from hello root certificate), run hello following command:</span></span>

          makecert.exe -n "CN=HBaseVnetVPNClientCertificate" -pe -sky exchange -m 96 -ss My -in "HBaseVnetVPNRootCertificate" -is my -a sha1

    <span data-ttu-id="2b698-197">HBaseVnetVPNRootCertificate hello kök sertifika adıdır.</span><span class="sxs-lookup"><span data-stu-id="2b698-197">HBaseVnetVPNRootCertificate is hello root certificate name.</span></span>  <span data-ttu-id="2b698-198">Toomatch hello kök sertifika adı vardır.</span><span class="sxs-lookup"><span data-stu-id="2b698-198">It has toomatch hello root certificate name.</span></span>  

    <span data-ttu-id="2b698-199">Merhaba kök sertifikasını ve hello istemci sertifikası, bilgisayarınızdaki kişisel sertifika deposunda depolanır.</span><span class="sxs-lookup"><span data-stu-id="2b698-199">Both hello root certificate and hello client certificate are stored in your Personal certificate store on your computer.</span></span> <span data-ttu-id="2b698-200">Certmgr.msc tooverify kullanın.</span><span class="sxs-lookup"><span data-stu-id="2b698-200">Use certmgr.msc tooverify.</span></span>

    ![Azure sanal ağı noktadan siteye VPN sertifikası][img-certificate]

    <span data-ttu-id="2b698-202">Bir istemci sertifikası tooconnect toohello sanal ağ istediğiniz her bilgisayara yüklenmelidir.</span><span class="sxs-lookup"><span data-stu-id="2b698-202">A client certificate must be installed on each computer that you want tooconnect toohello virtual network.</span></span> <span data-ttu-id="2b698-203">Benzersiz istemci sertifikaları tooconnect toohello sanal ağ istediğiniz her bilgisayar için oluşturmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="2b698-203">We recommend that you create unique client certificates for each computer that you want tooconnect toohello virtual network.</span></span> <span data-ttu-id="2b698-204">tooexport hello istemci sertifikaları, certmgr.msc kullanın.</span><span class="sxs-lookup"><span data-stu-id="2b698-204">tooexport hello client certificates, use certmgr.msc.</span></span>

<span data-ttu-id="2b698-205">**tooupload hello kök sertifika toohello Klasik Azure portalı**</span><span class="sxs-lookup"><span data-stu-id="2b698-205">**tooupload hello root certificate toohello Azure Classic Portal**</span></span>

1. <span data-ttu-id="2b698-206">Merhaba Klasik Azure Portalı ' tıklatın **ağ** hello soldaki.</span><span class="sxs-lookup"><span data-stu-id="2b698-206">From hello Azure Classic Portal, click **NETWORK** on hello left.</span></span>
2. <span data-ttu-id="2b698-207">HBase kümesi dağıtıldığı hello sanal ağ'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="2b698-207">Click hello virtual network where your HBase cluster is deployed to.</span></span>
3. <span data-ttu-id="2b698-208">Tıklatın **SERTİFİKALARI** hello üstten.</span><span class="sxs-lookup"><span data-stu-id="2b698-208">Click **CERTIFICATES** from hello top.</span></span>
4. <span data-ttu-id="2b698-209">Tıklatın **karşıya** hello gelen alt ve son önce hello yordamda oluşturduğunuz hello kök sertifika dosyasını belirtin.</span><span class="sxs-lookup"><span data-stu-id="2b698-209">Click **UPLOAD** from hello bottom, and specify hello root certificate file you have created in hello procedure before last.</span></span> <span data-ttu-id="2b698-210">Merhaba sertifika içeri kadar bekleyin.</span><span class="sxs-lookup"><span data-stu-id="2b698-210">Wait until hello certificate got imported.</span></span>
5. <span data-ttu-id="2b698-211">Tıklatın **PANO** hello üstte.</span><span class="sxs-lookup"><span data-stu-id="2b698-211">Click **DASHBOARD** on hello top.</span></span>  <span data-ttu-id="2b698-212">Merhaba sanal diyagramı hello durumunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="2b698-212">hello virtual diagram shows hello status.</span></span>

#### <a name="configure-your-vpn-client"></a><span data-ttu-id="2b698-213">VPN istemcinizi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="2b698-213">Configure your VPN client</span></span>
<span data-ttu-id="2b698-214">**Merhaba istemci VPN paketini toodownload ve yükle**</span><span class="sxs-lookup"><span data-stu-id="2b698-214">**toodownload and install hello client VPN package**</span></span>

1. <span data-ttu-id="2b698-215">Merhaba Hızlı Bakış bölümünde hello sanal ağın hello PANO sayfasından öğelerinden birini tıklatın **indirme hello 64-bit istemci VPN paketini** veya **indirme hello 32 bit istemci VPN paketini** göre İş istasyonu işletim sistemi sürümü.</span><span class="sxs-lookup"><span data-stu-id="2b698-215">From hello DASHBOARD page of hello virtual network, in hello quick glance section, click either **Download hello 64-bit Client VPN Package** or **Download hello 32-bit Client VPN Package** based on your workstation OS version.</span></span>
2. <span data-ttu-id="2b698-216">Tıklatın **çalıştırmak** tooinstall hello paket.</span><span class="sxs-lookup"><span data-stu-id="2b698-216">Click **Run** tooinstall hello package.</span></span>
3. <span data-ttu-id="2b698-217">Merhaba güvenlik isteminde tıklatın **daha fazla bilgi**ve ardından **yine de çalıştırmaya**.</span><span class="sxs-lookup"><span data-stu-id="2b698-217">At hello security prompt, click **More info**, and then click **Run anyway**.</span></span>
4. <span data-ttu-id="2b698-218">Tıklatın **Evet** iki kez.</span><span class="sxs-lookup"><span data-stu-id="2b698-218">Click **Yes** twice.</span></span>

<span data-ttu-id="2b698-219">**tooconnect tooVPN**</span><span class="sxs-lookup"><span data-stu-id="2b698-219">**tooconnect tooVPN**</span></span>

1. <span data-ttu-id="2b698-220">İş istasyonunuzu Hello masaüstünde hello görev çubuğunda hello ağları simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2b698-220">On hello desktop of your workstation, click hello Networks icon on hello Task bar.</span></span> <span data-ttu-id="2b698-221">Bir VPN bağlantısı, sanal ağ adıyla göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="2b698-221">You shall see a VPN connection with your virtual network name.</span></span>
2. <span data-ttu-id="2b698-222">Merhaba VPN bağlantısı adını tıklatın.</span><span class="sxs-lookup"><span data-stu-id="2b698-222">Click hello VPN connection name.</span></span>
3. <span data-ttu-id="2b698-223">**Bağlan**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2b698-223">Click **Connect**.</span></span>

<span data-ttu-id="2b698-224">**tootest hello VPN bağlantısı ve etki alanı ad çözümlemesi**</span><span class="sxs-lookup"><span data-stu-id="2b698-224">**tootest hello VPN connection and domain name resolution**</span></span>

* <span data-ttu-id="2b698-225">Merhaba iş istasyonundan, bir komut istemi açın ve hello hello HBase kümesi'nin DNS soneki verilen adlarından birini ping myhbase.b7.internal.cloudapp.net ise:</span><span class="sxs-lookup"><span data-stu-id="2b698-225">From hello workstation, open a command prompt and ping one of hello following names given hello HBase cluster's DNS suffix is myhbase.b7.internal.cloudapp.net:</span></span>

        zookeeper0.myhbase.b7.internal.cloudapp.net
        zookeeper0.myhbase.b7.internal.cloudapp.net
        zookeeper0.myhbase.b7.internal.cloudapp.net
        headnode0.myhbase.b7.internal.cloudapp.net
        headnode1.myhbase.b7.internal.cloudapp.net
        workernode0.myhbase.b7.internal.cloudapp.net

### <a name="install-and-configure-squirrel-on-your-workstation"></a><span data-ttu-id="2b698-226">Yükleme ve SQuirreL iş istasyonunuza yapılandırma</span><span class="sxs-lookup"><span data-stu-id="2b698-226">Install and configure SQuirreL on your workstation</span></span>
<span data-ttu-id="2b698-227">**tooinstall SQuirreL**</span><span class="sxs-lookup"><span data-stu-id="2b698-227">**tooinstall SQuirreL**</span></span>

1. <span data-ttu-id="2b698-228">Merhaba SQuirreL SQL istemci jar dosyasını indirin [http://squirrel-sql.sourceforge.net/#installation](http://squirrel-sql.sourceforge.net/#installation).</span><span class="sxs-lookup"><span data-stu-id="2b698-228">Download hello SQuirreL SQL client jar file from [http://squirrel-sql.sourceforge.net/#installation](http://squirrel-sql.sourceforge.net/#installation).</span></span>
2. <span data-ttu-id="2b698-229">Açma/çalıştırma hello jar dosyasını.</span><span class="sxs-lookup"><span data-stu-id="2b698-229">Open/run hello jar file.</span></span> <span data-ttu-id="2b698-230">Merhaba gerektirir [Java Çalışma zamanı ortamı](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html).</span><span class="sxs-lookup"><span data-stu-id="2b698-230">It requires hello [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html).</span></span>
3. <span data-ttu-id="2b698-231">Tıklatın **sonraki** iki kez.</span><span class="sxs-lookup"><span data-stu-id="2b698-231">Click **Next** twice.</span></span>
4. <span data-ttu-id="2b698-232">Yazma izni ve ardından hello sahip olduğu bir yol belirtin **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="2b698-232">Specify a path where you have hello write permission, and then click **Next**.</span></span>

  > [!NOTE]
  > <span data-ttu-id="2b698-233">Merhaba C:\Program Files\squirrel-sql-3.6 klasöründe Hello varsayılan yükleme klasörüdür.</span><span class="sxs-lookup"><span data-stu-id="2b698-233">hello default installation folder is in hello C:\Program Files\squirrel-sql-3.6 folder.</span></span>  <span data-ttu-id="2b698-234">Sipariş toowrite toothis yolunda hello yükleyici hello Yöneticisi ayrıcalığı verilmelidir.</span><span class="sxs-lookup"><span data-stu-id="2b698-234">In order toowrite toothis path, hello installer must be granted hello administrator privilege.</span></span> <span data-ttu-id="2b698-235">Yönetici olarak bir komut istemi açın, tooJava'nın bin klasörüne gidin ve ardından çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="2b698-235">You can open a command prompt as administrator, navigate tooJava's bin folder, and then run:</span></span>
  >
  >     <span data-ttu-id="2b698-236">Java.exe-jar [hello SQuirreL jar dosyasını hello yolu]</span><span class="sxs-lookup"><span data-stu-id="2b698-236">java.exe -jar [hello path of hello SQuirreL jar file]</span></span>
5. <span data-ttu-id="2b698-237">Tıklatın **Tamam** tooconfirm hello hedef dizin oluşturma.</span><span class="sxs-lookup"><span data-stu-id="2b698-237">Click **OK** tooconfirm creating hello target directory.</span></span>
6. <span data-ttu-id="2b698-238">Merhaba tooinstall hello temel ve standart paketleri varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="2b698-238">hello default setting is tooinstall hello Base and Standard packages.</span></span>  <span data-ttu-id="2b698-239">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2b698-239">Click **Next**.</span></span>
7. <span data-ttu-id="2b698-240">Tıklatın **sonraki** iki kez tıkladıktan sonra **Bitti**.</span><span class="sxs-lookup"><span data-stu-id="2b698-240">Click **Next** twice, and then click **Done**.</span></span>

<span data-ttu-id="2b698-241">**tooinstall hello Phoenix sürücüsü**</span><span class="sxs-lookup"><span data-stu-id="2b698-241">**tooinstall hello Phoenix driver**</span></span>

<span data-ttu-id="2b698-242">Merhaba phoenix sürücü jar dosyasını hello HBase kümesi üzerinde bulunur.</span><span class="sxs-lookup"><span data-stu-id="2b698-242">hello phoenix driver jar file is located on hello HBase cluster.</span></span> <span data-ttu-id="2b698-243">Merhaba yolu hello sürümlerine bağlı benzer toohello aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="2b698-243">hello path is similar toohello following based on hello versions:</span></span>

    C:\apps\dist\phoenix-4.0.0.2.1.11.0-2316\phoenix-4.0.0.2.1.11.0-2316-client.jar
<span data-ttu-id="2b698-244">Toocopy gerekir, tooyour iş istasyonu hello [SQuirreL yükleme klasörü] altında / lib yolu.</span><span class="sxs-lookup"><span data-stu-id="2b698-244">You need toocopy it tooyour workstation under hello [SQuirreL installation folder]/lib path.</span></span>  <span data-ttu-id="2b698-245">Merhaba kolay hello küme ve Kullan, dosyayı kopyalayıp yapıştırın (CTRL + C ve CTRL + V) toocopy tooRDP yoludur, tooyour iş istasyonu.</span><span class="sxs-lookup"><span data-stu-id="2b698-245">hello easiest way is tooRDP into hello cluster, and then use file copy/paste (CTRL+C and CTRL+V) toocopy it tooyour workstation.</span></span>

<span data-ttu-id="2b698-246">**Phoenix sürücü tooSQuirreL tooadd**</span><span class="sxs-lookup"><span data-stu-id="2b698-246">**tooadd a Phoenix driver tooSQuirreL**</span></span>

1. <span data-ttu-id="2b698-247">SQuirreL SQL istemci istasyonunuzdan açın.</span><span class="sxs-lookup"><span data-stu-id="2b698-247">Open SQuirreL SQL Client from your workstation.</span></span>
2. <span data-ttu-id="2b698-248">Merhaba tıklatın **sürücü** hello sol sekmesinde.</span><span class="sxs-lookup"><span data-stu-id="2b698-248">Click hello **Driver** tab on hello left.</span></span>
3. <span data-ttu-id="2b698-249">Merhaba gelen **sürücüleri** menüsünde tıklatın **yeni sürücü**.</span><span class="sxs-lookup"><span data-stu-id="2b698-249">From hello **Drivers** menu, click **New Driver**.</span></span>
4. <span data-ttu-id="2b698-250">Aşağıdaki bilgilerle hello girin:</span><span class="sxs-lookup"><span data-stu-id="2b698-250">Enter hello following information:</span></span>

   * <span data-ttu-id="2b698-251">**Ad**: Phoenix</span><span class="sxs-lookup"><span data-stu-id="2b698-251">**Name**: Phoenix</span></span>
   * <span data-ttu-id="2b698-252">**Örnek URL**: jdbc:phoenix:zookeeper2.contoso hbase eu.f5.internal.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="2b698-252">**Example URL**: jdbc:phoenix:zookeeper2.contoso-hbase-eu.f5.internal.cloudapp.net</span></span>
   * <span data-ttu-id="2b698-253">**Sınıf adı**: org.apache.phoenix.jdbc.PhoenixDriver</span><span class="sxs-lookup"><span data-stu-id="2b698-253">**Class Name**: org.apache.phoenix.jdbc.PhoenixDriver</span></span>

     > [!WARNING]
     > <span data-ttu-id="2b698-254">Kullanıcı hello örnek URL tüm alt durumda.</span><span class="sxs-lookup"><span data-stu-id="2b698-254">User all lower case in hello Example URL.</span></span> <span data-ttu-id="2b698-255">Kullanabileceğiniz bunlar tam zookeeper çekirdek bunlardan birini çalışmıyor durumda.</span><span class="sxs-lookup"><span data-stu-id="2b698-255">You can use they full zookeeper quorum in case one of them is down.</span></span>  <span data-ttu-id="2b698-256">Merhaba konak zookeeper0, zookeeper1 ve zookeeper2 adları.</span><span class="sxs-lookup"><span data-stu-id="2b698-256">hello hostnames are zookeeper0, zookeeper1, and zookeeper2.</span></span>
     >
     >

     ![Hdınsight HBase Phoenix SQuirreL sürücüsü][img-squirrel-driver]
5. <span data-ttu-id="2b698-258">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2b698-258">Click **OK**.</span></span>

<span data-ttu-id="2b698-259">**toocreate bir diğer ad toohello HBase kümesi**</span><span class="sxs-lookup"><span data-stu-id="2b698-259">**toocreate an alias toohello HBase cluster**</span></span>

1. <span data-ttu-id="2b698-260">Merhaba SQuirreL tıklatın **diğer adlar** hello sol sekmesinde.</span><span class="sxs-lookup"><span data-stu-id="2b698-260">From SQuirreL, Click hello **Aliases** tab on hello left.</span></span>
2. <span data-ttu-id="2b698-261">Merhaba gelen **diğer adlar** menüsünde tıklatın **yeni diğer**.</span><span class="sxs-lookup"><span data-stu-id="2b698-261">From hello **Aliases** menu, click **New Alias**.</span></span>
3. <span data-ttu-id="2b698-262">Aşağıdaki bilgilerle hello girin:</span><span class="sxs-lookup"><span data-stu-id="2b698-262">Enter hello following information:</span></span>

   * <span data-ttu-id="2b698-263">**Ad**: Merhaba HBase kümesi veya tercih ettiğiniz herhangi bir ad hello adı.</span><span class="sxs-lookup"><span data-stu-id="2b698-263">**Name**: hello name of hello HBase cluster or any name you prefer.</span></span>
   * <span data-ttu-id="2b698-264">**Sürücü**: Phoenix.</span><span class="sxs-lookup"><span data-stu-id="2b698-264">**Driver**: Phoenix.</span></span>  <span data-ttu-id="2b698-265">Bu hello son yordamda oluşturduğunuz hello sürücü adı eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="2b698-265">This must match hello driver name you created in hello last procedure.</span></span>
   * <span data-ttu-id="2b698-266">**URL**: hello URL sürücü yapılandırmasından kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="2b698-266">**URL**: hello URL is copied from your driver configuration.</span></span> <span data-ttu-id="2b698-267">Tüm küçük toouser emin olun.</span><span class="sxs-lookup"><span data-stu-id="2b698-267">Make sure toouser all lower case.</span></span>
   * <span data-ttu-id="2b698-268">**Kullanıcı adı**: herhangi bir metin olabilir.</span><span class="sxs-lookup"><span data-stu-id="2b698-268">**User name**: It can be any text.</span></span>  <span data-ttu-id="2b698-269">VPN bağlantısı burada kullandığından, hello kullanıcı adı hiç kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="2b698-269">Because you use VPN connectivity here, hello user name is not used at all.</span></span>
   * <span data-ttu-id="2b698-270">**Parola**: herhangi bir metin olabilir.</span><span class="sxs-lookup"><span data-stu-id="2b698-270">**Password**: It can be any text.</span></span>

     ![Hdınsight HBase Phoenix SQuirreL sürücüsü][img-squirrel-alias]
4. <span data-ttu-id="2b698-272">Tıklatın **Test**.</span><span class="sxs-lookup"><span data-stu-id="2b698-272">Click **Test**.</span></span>
5. <span data-ttu-id="2b698-273">**Bağlan**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2b698-273">Click **Connect**.</span></span> <span data-ttu-id="2b698-274">Merhaba bağlantı yaptığında, SQuirreL şuna benzer:</span><span class="sxs-lookup"><span data-stu-id="2b698-274">When it makes hello connection, SQuirreL looks like:</span></span>

    ![HBase Phoenix SQuirreL][img-squirrel]

<span data-ttu-id="2b698-276">**toorun test**</span><span class="sxs-lookup"><span data-stu-id="2b698-276">**toorun a test**</span></span>

1. <span data-ttu-id="2b698-277">Merhaba tıklatın **SQL** sağ sonraki toohello sekmesinde **nesneleri** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="2b698-277">Click hello **SQL** tab right next toohello **Objects** tab.</span></span>
2. <span data-ttu-id="2b698-278">Kopyalayın ve hello aşağıdaki kodu yapıştırın:</span><span class="sxs-lookup"><span data-stu-id="2b698-278">Copy and paste hello following code:</span></span>

        CREATE TABLE IF NOT EXISTS us_population (state CHAR(2) NOT NULL, city VARCHAR NOT NULL, population BIGINT  CONSTRAINT my_pk PRIMARY KEY (state, city))
3. <span data-ttu-id="2b698-279">Merhaba çalıştırma düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2b698-279">Click hello run button.</span></span>

    ![HBase Phoenix SQuirreL][img-squirrel-sql]
4. <span data-ttu-id="2b698-281">Geçiş geri toohello **nesneleri** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="2b698-281">Switch back toohello **Objects** tab.</span></span>
5. <span data-ttu-id="2b698-282">Merhaba diğer adı'nı genişletin ve ardından genişletin **tablo**.</span><span class="sxs-lookup"><span data-stu-id="2b698-282">Expand hello alias name, and then expand **TABLE**.</span></span>  <span data-ttu-id="2b698-283">Merhaba yeni tablo altında listelenen görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="2b698-283">You shall see hello new table listed under.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2b698-284">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2b698-284">Next steps</span></span>
<span data-ttu-id="2b698-285">Bu makalede, öğrendiğiniz nasıl toouse hdınsight'ta Apache Phoenix.</span><span class="sxs-lookup"><span data-stu-id="2b698-285">In this article, you have learned how toouse Apache Phoenix in HDInsight.</span></span>  <span data-ttu-id="2b698-286">toolearn daha bakın</span><span class="sxs-lookup"><span data-stu-id="2b698-286">toolearn more, see</span></span>

* <span data-ttu-id="2b698-287">[HDInsight HBase'e genel bakış][hdinsight-hbase-overview]: HBase büyük miktarda yapılandırılmamış ve yarı yapılandırılmış veri için rastgele erişim ve güçlü tutarlılık sağlayan, Hadoop'ta yerleşik bir Apache, açık kaynak, NoSQL veritabanıdır.</span><span class="sxs-lookup"><span data-stu-id="2b698-287">[HDInsight HBase overview][hdinsight-hbase-overview]: HBase is an Apache, open-source, NoSQL database built on Hadoop that provides random access and strong consistency for large amounts of unstructured and semistructured data.</span></span>
* <span data-ttu-id="2b698-288">[Azure Virtual Network HBase kümelerine sağlamak][hdinsight-hbase-provision-vnet]: sanal ağ tümleştirmesinin ile HBase kümeleri aynı sanal ağ, uygulamalarınızın böylece dağıtılan toohello olabilir uygulamalar ile iletişim kurabilir Doğrudan HBase.</span><span class="sxs-lookup"><span data-stu-id="2b698-288">[Provision HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet]: With virtual network integration, HBase clusters can be deployed toohello same virtual network as your applications so that applications can communicate with HBase directly.</span></span>
* <span data-ttu-id="2b698-289">[Hdınsight'ta HBase çoğaltmayı yapılandırma](hdinsight-hbase-replication.md): öğrenin nasıl tooconfigure HBase çoğaltmayı iki Azure veri merkezleri arasında.</span><span class="sxs-lookup"><span data-stu-id="2b698-289">[Configure HBase replication in HDInsight](hdinsight-hbase-replication.md): Learn how tooconfigure HBase replication across two Azure datacenters.</span></span>
* <span data-ttu-id="2b698-290">[Hdınsight'ta HBase ile twitter düşüncelerini çözümleme][hbase-twitter-sentiment]: öğrenin nasıl toodo gerçek zamanlı [düşünceleri analiz](http://en.wikipedia.org/wiki/Sentiment_analysis) HBase hdınsight'ta Hadoop kümesi kullanarak büyük veri.</span><span class="sxs-lookup"><span data-stu-id="2b698-290">[Analyze Twitter sentiment with HBase in HDInsight][hbase-twitter-sentiment]: Learn how toodo real-time [sentiment analysis](http://en.wikipedia.org/wiki/Sentiment_analysis) of big data by using HBase in a Hadoop cluster in HDInsight.</span></span>

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
