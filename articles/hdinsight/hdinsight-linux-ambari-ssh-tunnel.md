---
title: "Azure Hdınsight erişmek için tünel SSH kullanma | Microsoft Docs"
description: "Linux tabanlı Hdınsight düğümler üzerinde barındırılan web kaynaklarına güvenli bir şekilde göz atmak için SSH tüneli kullanmayı öğrenin."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 879834a4-52d0-499c-a3ae-8d28863abf65
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/21/2017
ms.author: larryfr
ms.openlocfilehash: 4b606ea3797d685b9deacf72f1bd31e0ef007f98
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="use-ssh-tunneling-to-access-ambari-web-ui-jobhistory-namenode-oozie-and-other-web-uis"></a><span data-ttu-id="4a25d-103">Ambari web kullanıcı Arabirimi, kaynak, iş, Oozie ve diğer web Uı'lar erişmek için SSH tünel kullan</span><span class="sxs-lookup"><span data-stu-id="4a25d-103">Use SSH Tunneling to access Ambari web UI, JobHistory, NameNode, Oozie, and other web UIs</span></span>

<span data-ttu-id="4a25d-104">Linux tabanlı Hdınsight kümeleri Internet üzerinden erişebilmesi için Ambari web kullanıcı Arabirimi, ancak bazı özellikler UI değildir.</span><span class="sxs-lookup"><span data-stu-id="4a25d-104">Linux-based HDInsight clusters provide access to Ambari web UI over the Internet, but some features of the UI are not.</span></span> <span data-ttu-id="4a25d-105">Örneğin, web kullanıcı Arabirimi Ambari ortaya çıkmış diğer hizmetler için.</span><span class="sxs-lookup"><span data-stu-id="4a25d-105">For example, the web UI for other services that are surfaced through Ambari.</span></span> <span data-ttu-id="4a25d-106">Ambari web kullanıcı Arabirimi tam işlevsellik için küme head için SSH tüneli kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="4a25d-106">For full functionality of the Ambari web UI, you must use an SSH tunnel to the cluster head.</span></span>

## <a name="why-use-an-ssh-tunnel"></a><span data-ttu-id="4a25d-107">SSH tüneli neden kullanılır?</span><span class="sxs-lookup"><span data-stu-id="4a25d-107">Why use an SSH tunnel</span></span>

<span data-ttu-id="4a25d-108">Ambari menülerde çeşitli yalnızca SSH tüneli çalışır.</span><span class="sxs-lookup"><span data-stu-id="4a25d-108">Several of the menus in Ambari only work through an SSH tunnel.</span></span> <span data-ttu-id="4a25d-109">Bu menüler web siteleri ve alt düğümleri gibi diğer düğüm türleri üzerinde çalışan hizmetleri kullanır.</span><span class="sxs-lookup"><span data-stu-id="4a25d-109">These menus rely on web sites and services running on other node types, such as worker nodes.</span></span> <span data-ttu-id="4a25d-110">Doğrudan internet'te kullanıma sunmak güvenli değildir genellikle, bu web sitelerinin, sağlanmaz.</span><span class="sxs-lookup"><span data-stu-id="4a25d-110">Often, these web sites are not secured, so it is not safe to directly expose them on the internet.</span></span>

<span data-ttu-id="4a25d-111">Aşağıdaki Web kullanıcı arabirimleri SSH tüneli gerektirir:</span><span class="sxs-lookup"><span data-stu-id="4a25d-111">The following Web UIs require an SSH tunnel:</span></span>

* <span data-ttu-id="4a25d-112">Kaynak</span><span class="sxs-lookup"><span data-stu-id="4a25d-112">JobHistory</span></span>
* <span data-ttu-id="4a25d-113">İş</span><span class="sxs-lookup"><span data-stu-id="4a25d-113">NameNode</span></span>
* <span data-ttu-id="4a25d-114">İş parçacığı yığınları</span><span class="sxs-lookup"><span data-stu-id="4a25d-114">Thread Stacks</span></span>
* <span data-ttu-id="4a25d-115">Oozie web kullanıcı Arabirimi</span><span class="sxs-lookup"><span data-stu-id="4a25d-115">Oozie web UI</span></span>
* <span data-ttu-id="4a25d-116">HBase ana ve günlükleri kullanıcı Arabirimi</span><span class="sxs-lookup"><span data-stu-id="4a25d-116">HBase Master and Logs UI</span></span>

<span data-ttu-id="4a25d-117">Kümenizi özelleştirmek için betik eylemleri kullanın, herhangi bir hizmet veya bir web kullanıcı arabirimini kullanıma yüklediğiniz utilities SSH tüneli gerektirir.</span><span class="sxs-lookup"><span data-stu-id="4a25d-117">If you use Script Actions to customize your cluster, any services or utilities that you install that expose a web UI require an SSH tunnel.</span></span> <span data-ttu-id="4a25d-118">Örneğin, ton betik eylemini kullanarak yüklerseniz, Hue web kullanıcı arabirimini erişmek için bir SSH tüneli kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="4a25d-118">For example, if you install Hue using a Script Action, you must use an SSH tunnel to access the Hue web UI.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4a25d-119">Bir sanal ağ üzerinden hdınsight'a doğrudan erişimi varsa, SSH tünelleri kullanmak gerekmez.</span><span class="sxs-lookup"><span data-stu-id="4a25d-119">If you have direct access to HDInsight through a virtual network, you do not need to use SSH tunnels.</span></span> <span data-ttu-id="4a25d-120">Hdınsight aracılığıyla bir sanal ağa doğrudan erişimini ilişkin bir örnek için bkz: [şirket içi ağınıza bağlanmak Hdınsight](connect-on-premises-network.md) belge.</span><span class="sxs-lookup"><span data-stu-id="4a25d-120">For an example of directly accessing HDInsight through a virtual network, see the [Connect HDInsight to your on-premises network](connect-on-premises-network.md) document.</span></span>

## <a name="what-is-an-ssh-tunnel"></a><span data-ttu-id="4a25d-121">SSH tüneli nedir</span><span class="sxs-lookup"><span data-stu-id="4a25d-121">What is an SSH tunnel</span></span>

<span data-ttu-id="4a25d-122">[Güvenli Kabuk (SSH) tüneli](https://en.wikipedia.org/wiki/Tunneling_protocol#Secure_Shell_tunneling) yerel istasyonunuzda bir bağlantı noktasına gönderilen trafiğin yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="4a25d-122">[Secure Shell (SSH) tunneling](https://en.wikipedia.org/wiki/Tunneling_protocol#Secure_Shell_tunneling) routes traffic sent to a port on your local workstation.</span></span> <span data-ttu-id="4a25d-123">Trafik, Hdınsight küme baş düğümüne bir SSH bağlantısı üzerinden yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="4a25d-123">The traffic is routed through an SSH connection to your HDInsight cluster head node.</span></span> <span data-ttu-id="4a25d-124">İstek baş düğümünde geldiyse olarak çözümlenir.</span><span class="sxs-lookup"><span data-stu-id="4a25d-124">The request is resolved as if it originated on the head node.</span></span> <span data-ttu-id="4a25d-125">Yanıt, sonra iş istasyonunuzu için tünelinden yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="4a25d-125">The response is then routed back through the tunnel to your workstation.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4a25d-126">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="4a25d-126">Prerequisites</span></span>

* <span data-ttu-id="4a25d-127">Bir SSH istemcisi.</span><span class="sxs-lookup"><span data-stu-id="4a25d-127">An SSH client.</span></span> <span data-ttu-id="4a25d-128">Daha fazla bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="4a25d-128">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="4a25d-129">SOCKS5 proxy kullanmak üzere yapılandırılmış bir web tarayıcısı.</span><span class="sxs-lookup"><span data-stu-id="4a25d-129">A web browser that can be configured to use a SOCKS5 proxy.</span></span>

    > [!WARNING]
    > <span data-ttu-id="4a25d-130">Windows'da yerleşik SOCKS proxy desteği SOCKS5 desteklemez ve bu belgede yer alan adımlar ile çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="4a25d-130">The SOCKS proxy support built into Windows does not support SOCKS5, and does not work with the steps in this document.</span></span> <span data-ttu-id="4a25d-131">Aşağıdaki tarayıcılar Windows proxy ayarlarını kullanır ve bu belgedeki adımları şu anda çalışmıyor:</span><span class="sxs-lookup"><span data-stu-id="4a25d-131">The following browsers rely on Windows proxy settings, and do not currently work with the steps in this document:</span></span>
    >
    > * <span data-ttu-id="4a25d-132">Microsoft Edge</span><span class="sxs-lookup"><span data-stu-id="4a25d-132">Microsoft Edge</span></span>
    > * <span data-ttu-id="4a25d-133">Microsoft Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="4a25d-133">Microsoft Internet Explorer</span></span>
    >
    > <span data-ttu-id="4a25d-134">Google Chrome, aynı zamanda Windows proxy ayarlarını kullanır.</span><span class="sxs-lookup"><span data-stu-id="4a25d-134">Google Chrome also relies on the Windows proxy settings.</span></span> <span data-ttu-id="4a25d-135">Ancak, SOCKS5 Destek Uzantıları yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4a25d-135">However, you can install extensions that support SOCKS5.</span></span> <span data-ttu-id="4a25d-136">Öneririz [FoxyProxy standart](https://chrome.google.com/webstore/detail/foxyproxy-standard/gcknhkkoolaabfmlnjonogaaifnjlfnp).</span><span class="sxs-lookup"><span data-stu-id="4a25d-136">We recommend [FoxyProxy Standard](https://chrome.google.com/webstore/detail/foxyproxy-standard/gcknhkkoolaabfmlnjonogaaifnjlfnp).</span></span>

## <span data-ttu-id="4a25d-137"><a name="usessh"></a>SSH komutunu kullanarak bir tünel oluşturma</span><span class="sxs-lookup"><span data-stu-id="4a25d-137"><a name="usessh"></a>Create a tunnel using the SSH command</span></span>

<span data-ttu-id="4a25d-138">Bir SSH oluşturmak için aşağıdaki komutu kullanarak tünel kullanımı `ssh` komutu.</span><span class="sxs-lookup"><span data-stu-id="4a25d-138">Use the following command to create an SSH tunnel using the `ssh` command.</span></span> <span data-ttu-id="4a25d-139">Değiştir **kullanıcıadı** Hdınsight kümesi ve değiştirmek için bir SSH kullanıcıyla **CLUSTERNAME** Hdınsight kümenizin adıyla:</span><span class="sxs-lookup"><span data-stu-id="4a25d-139">Replace **USERNAME** with an SSH user for your HDInsight cluster, and replace **CLUSTERNAME** with the name of your HDInsight cluster:</span></span>

```bash
ssh -C2qTnNf -D 9876 USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
```

<span data-ttu-id="4a25d-140">Bu komut, bağlantı noktasına yerel 9876 kümeye SSH üzerinden trafiğini yönlendiren bir bağlantı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4a25d-140">This command creates a connection that routes traffic to local port 9876 to the cluster over SSH.</span></span> <span data-ttu-id="4a25d-141">Seçenekler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="4a25d-141">The options are:</span></span>

* <span data-ttu-id="4a25d-142">**D 9876** -Tünel üzerinden trafiğini yönlendiren yerel bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="4a25d-142">**D 9876** - The local port that routes traffic through the tunnel.</span></span>
* <span data-ttu-id="4a25d-143">**C** -web trafiği çoğunlukla metin olduğundan tüm verileri sıkıştırmak.</span><span class="sxs-lookup"><span data-stu-id="4a25d-143">**C** - Compress all data, because web traffic is mostly text.</span></span>
* <span data-ttu-id="4a25d-144">**2** -force Protokolü sürüm 2 yalnızca denemek için SSH.</span><span class="sxs-lookup"><span data-stu-id="4a25d-144">**2** - Force SSH to try protocol version 2 only.</span></span>
* <span data-ttu-id="4a25d-145">**q** -Sessiz mod.</span><span class="sxs-lookup"><span data-stu-id="4a25d-145">**q** - Quiet mode.</span></span>
* <span data-ttu-id="4a25d-146">**T** -biz yalnızca bir bağlantı noktası iletme beri sözde tty ayırma, devre dışı.</span><span class="sxs-lookup"><span data-stu-id="4a25d-146">**T** - Disable pseudo-tty allocation, since we are just forwarding a port.</span></span>
* <span data-ttu-id="4a25d-147">**n**-STDIN, okunması biz yalnızca bir bağlantı noktası iletme beri engelleyin.</span><span class="sxs-lookup"><span data-stu-id="4a25d-147">**n** - Prevent reading of STDIN, since we are just forwarding a port.</span></span>
* <span data-ttu-id="4a25d-148">**N** -biz yalnızca bir bağlantı noktası iletme olduğundan bir uzak komutu yürütülmez.</span><span class="sxs-lookup"><span data-stu-id="4a25d-148">**N** - Do not execute a remote command, since we are just forwarding a port.</span></span>
* <span data-ttu-id="4a25d-149">**f** -arka planda çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="4a25d-149">**f** - Run in the background.</span></span>

<span data-ttu-id="4a25d-150">Komut bittikten sonra yerel bilgisayarda 9876 numaralı bağlantı noktasına gönderilen trafiğin küme baş düğümüne yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="4a25d-150">Once the command finishes, traffic sent to port 9876 on the local computer is routed to the cluster head node.</span></span>

## <span data-ttu-id="4a25d-151"><a name="useputty"></a>PuTTY kullanarak bir tünel oluşturma</span><span class="sxs-lookup"><span data-stu-id="4a25d-151"><a name="useputty"></a>Create a tunnel using PuTTY</span></span>

<span data-ttu-id="4a25d-152">[PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty) Windows için grafik SSH istemcidir.</span><span class="sxs-lookup"><span data-stu-id="4a25d-152">[PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty) is a graphical SSH client for Windows.</span></span> <span data-ttu-id="4a25d-153">PuTTY kullanarak SSH tüneli oluşturmak için aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="4a25d-153">Use the following steps to create an SSH tunnel using PuTTY:</span></span>

1. <span data-ttu-id="4a25d-154">Putty'yi açın ve bağlantı bilgilerinizi girin.</span><span class="sxs-lookup"><span data-stu-id="4a25d-154">Open PuTTY, and enter your connection information.</span></span> <span data-ttu-id="4a25d-155">PuTTY ile bilmiyorsanız bkz [PuTTY belgeleri (http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html)](http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html).</span><span class="sxs-lookup"><span data-stu-id="4a25d-155">If you are not familiar with PuTTY, see the [PuTTY documentation (http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html)](http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html).</span></span>

2. <span data-ttu-id="4a25d-156">İçinde **kategori** iletişim kutusunun solundaki bölümünde, genişletmek **bağlantı**, genişletin **SSH**ve ardından **tüneller**.</span><span class="sxs-lookup"><span data-stu-id="4a25d-156">In the **Category** section to the left of the dialog, expand **Connection**, expand **SSH**, and then select **Tunnels**.</span></span>

3. <span data-ttu-id="4a25d-157">Üzerinde aşağıdaki bilgileri sağlayın **SSH denetleme seçenekleri bağlantı noktası iletme** form:</span><span class="sxs-lookup"><span data-stu-id="4a25d-157">Provide the following information on the **Options controlling SSH port forwarding** form:</span></span>
   
   * <span data-ttu-id="4a25d-158">**Kaynak bağlantı noktası** - İletmek istediğiniz istemci üzerindeki bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="4a25d-158">**Source port** - The port on the client that you wish to forward.</span></span> <span data-ttu-id="4a25d-159">Örneğin, **9876**.</span><span class="sxs-lookup"><span data-stu-id="4a25d-159">For example, **9876**.</span></span>

   * <span data-ttu-id="4a25d-160">**Hedef** -Linux tabanlı Hdınsight kümesi için SSH adresi.</span><span class="sxs-lookup"><span data-stu-id="4a25d-160">**Destination** - The SSH address for the Linux-based HDInsight cluster.</span></span> <span data-ttu-id="4a25d-161">Örneğin, **mycluster-ssh.azurehdinsight.net**.</span><span class="sxs-lookup"><span data-stu-id="4a25d-161">For example, **mycluster-ssh.azurehdinsight.net**.</span></span>

   * <span data-ttu-id="4a25d-162">**Dinamik** - Dinamik SOCKS proxy yönlendirmesini etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="4a25d-162">**Dynamic** - Enables dynamic SOCKS proxy routing.</span></span>
     
     ![Görüntü seçenekleri tünel](./media/hdinsight-linux-ambari-ssh-tunnel/puttytunnel.png)

4. <span data-ttu-id="4a25d-164">Tıklatın **Ekle** ayarları ekleyin ve ardından **açmak** bir SSH bağlantısı açılamıyor.</span><span class="sxs-lookup"><span data-stu-id="4a25d-164">Click **Add** to add the settings, and then click **Open** to open an SSH connection.</span></span>

5. <span data-ttu-id="4a25d-165">İstendiğinde, sunucuya oturum açın.</span><span class="sxs-lookup"><span data-stu-id="4a25d-165">When prompted, log in to the server.</span></span>

## <a name="use-the-tunnel-from-your-browser"></a><span data-ttu-id="4a25d-166">Tarayıcınızdan tünel kullanın</span><span class="sxs-lookup"><span data-stu-id="4a25d-166">Use the tunnel from your browser</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4a25d-167">Aynı proxy ayarları tüm platformlarda sağladığı gibi bu bölümdeki adımları Mozilla FireFox tarayıcı kullanın.</span><span class="sxs-lookup"><span data-stu-id="4a25d-167">The steps in this section use the Mozilla FireFox browser, as it provides the same proxy settings across all platforms.</span></span> <span data-ttu-id="4a25d-168">Google Chrome gibi modern tarayıcılar uzantı tünel ile çalışmak için FoxyProxy gibi gerektirebilir.</span><span class="sxs-lookup"><span data-stu-id="4a25d-168">Other modern browsers, such as Google Chrome, may require an extension such as FoxyProxy to work with the tunnel.</span></span>

1. <span data-ttu-id="4a25d-169">Kullanılacak tarayıcı yapılandırma **localhost** ve ne zaman kullanılan bağlantı noktası olarak tünel oluşturma bir **SOCKS v5** proxy.</span><span class="sxs-lookup"><span data-stu-id="4a25d-169">Configure the browser to use **localhost** and the port you used when creating the tunnel as a **SOCKS v5** proxy.</span></span> <span data-ttu-id="4a25d-170">Firefox ayarlarının nasıl göründüğünü aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="4a25d-170">Here's what the Firefox settings look like.</span></span> <span data-ttu-id="4a25d-171">Farklı bir bağlantı noktasıyla 9876 kullandıysanız, kullandığınız bir bağlantı noktasını değiştirin:</span><span class="sxs-lookup"><span data-stu-id="4a25d-171">If you used a different port than 9876, change the port to the one you used:</span></span>
   
    ![Firefox ayarlarının görüntüsü](./media/hdinsight-linux-ambari-ssh-tunnel/firefoxproxy.png)
   
   > [!NOTE]
   > <span data-ttu-id="4a25d-173">Seçme **uzak DNS** Hdınsight kümesi kullanarak etki alanı adı sistemi (DNS) isteklerinin giderir.</span><span class="sxs-lookup"><span data-stu-id="4a25d-173">Selecting **Remote DNS** resolves Domain Name System (DNS) requests by using the HDInsight cluster.</span></span> <span data-ttu-id="4a25d-174">Bu ayar kümenin baş düğümüne kullanarak DNS çözümler.</span><span class="sxs-lookup"><span data-stu-id="4a25d-174">This setting resolves DNS using the head node of the cluster.</span></span>

2. <span data-ttu-id="4a25d-175">Tünel bir siteyi ziyaret ederek gibi çalıştığını doğrulamak [http://www.whatismyip.com/](http://www.whatismyip.com/).</span><span class="sxs-lookup"><span data-stu-id="4a25d-175">Verify that the tunnel works by visiting a site such as [http://www.whatismyip.com/](http://www.whatismyip.com/).</span></span> <span data-ttu-id="4a25d-176">Döndürülen IP bir Microsoft Azure veri merkezi tarafından kullanılan olması.</span><span class="sxs-lookup"><span data-stu-id="4a25d-176">The IP returned should be one used by the Microsoft Azure datacenter.</span></span>

## <a name="verify-with-ambari-web-ui"></a><span data-ttu-id="4a25d-177">Ambari web kullanıcı Arabirimi ile doğrulayın</span><span class="sxs-lookup"><span data-stu-id="4a25d-177">Verify with Ambari web UI</span></span>

<span data-ttu-id="4a25d-178">Küme oluşturulduktan sonra hizmet web Uı'lar Ambari Web üzerinden erişebilirsiniz doğrulamak için aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="4a25d-178">Once the cluster has been established, use the following steps to verify that you can access service web UIs from the Ambari Web:</span></span>

1. <span data-ttu-id="4a25d-179">Tarayıcınızda, http://headnodehost:8080 için gidin.</span><span class="sxs-lookup"><span data-stu-id="4a25d-179">In your browser, go to http://headnodehost:8080.</span></span> <span data-ttu-id="4a25d-180">`headnodehost` Adresi ambarı üzerinde çalıştığı headnode çözümleyip ve küme için tüneli üzerinden gönderilir.</span><span class="sxs-lookup"><span data-stu-id="4a25d-180">The `headnodehost` address is sent over the tunnel to the cluster and resolve to the headnode that Ambari is running on.</span></span> <span data-ttu-id="4a25d-181">İstendiğinde, kümeniz için yönetici kullanıcı adını (Yönetici) ve parolasını girin.</span><span class="sxs-lookup"><span data-stu-id="4a25d-181">When prompted, enter the admin user name (admin) and password for your cluster.</span></span> <span data-ttu-id="4a25d-182">Ambari web kullanıcı arabirimini ikinci kez istenebilir.</span><span class="sxs-lookup"><span data-stu-id="4a25d-182">You may be prompted a second time by the Ambari web UI.</span></span> <span data-ttu-id="4a25d-183">Öyleyse, bilgileri yeniden girin.</span><span class="sxs-lookup"><span data-stu-id="4a25d-183">If so, reenter the information.</span></span>

   > [!NOTE]
   > <span data-ttu-id="4a25d-184">Http://headnodehost:8080 adresi kümeye bağlanmak için kullanırken, tünel üzerinden bağlanırsınız.</span><span class="sxs-lookup"><span data-stu-id="4a25d-184">When using the http://headnodehost:8080 address to connect to the cluster, you are connecting through the tunnel.</span></span> <span data-ttu-id="4a25d-185">İletişim HTTPS yerine SSH tüneli kullanılarak güvenli hale getirilir.</span><span class="sxs-lookup"><span data-stu-id="4a25d-185">Communication is secured using the SSH tunnel instead of HTTPS.</span></span> <span data-ttu-id="4a25d-186">HTTPS kullanarak Internet üzerinden bağlanmak için https://CLUSTERNAME.azurehdinsight.net, kullanın nerede **CLUSTERNAME** kümesinin adı.</span><span class="sxs-lookup"><span data-stu-id="4a25d-186">To connect over the internet using HTTPS, use https://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is the name of the cluster.</span></span>

2. <span data-ttu-id="4a25d-187">Ambari Web kullanıcı arabirimini HDFS sayfanın sol taraftaki listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="4a25d-187">From the Ambari Web UI, select HDFS from the list on the left of the page.</span></span>

    ![Seçili HDFS görüntüsüyle](./media/hdinsight-linux-ambari-ssh-tunnel/hdfsservice.png)

3. <span data-ttu-id="4a25d-189">HDFS hizmet bilgileri görüntülendiğinde seçin **hızlı bağlantılar**.</span><span class="sxs-lookup"><span data-stu-id="4a25d-189">When the HDFS service information is displayed, select **Quick Links**.</span></span> <span data-ttu-id="4a25d-190">Küme baş düğümler listesi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="4a25d-190">A list of the cluster head nodes appears.</span></span> <span data-ttu-id="4a25d-191">Baş düğümlerden birini seçin ve ardından **iş UI**.</span><span class="sxs-lookup"><span data-stu-id="4a25d-191">Select one of the head nodes, and then select **NameNode UI**.</span></span>

    ![Görüntü QuickLinks menüsü ile genişletilmiş](./media/hdinsight-linux-ambari-ssh-tunnel/namenodedropdown.png)

   > [!NOTE]
   > <span data-ttu-id="4a25d-193">Seçtiğinizde, __hızlı bağlantılar__, bekleme göstergesi alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4a25d-193">When you select __Quick Links__, you may get a wait indicator.</span></span> <span data-ttu-id="4a25d-194">Yavaş bir internet bağlantınız varsa, bu durum oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="4a25d-194">This condition can occur if you have a slow internet connection.</span></span> <span data-ttu-id="4a25d-195">Bir veya iki sunucudan alınacak veri için dakika bekleyin ve sonra listenin tekrar deneyin.</span><span class="sxs-lookup"><span data-stu-id="4a25d-195">Wait a minute or two for the data to be received from the server, then try the list again.</span></span>
   >
   > <span data-ttu-id="4a25d-196">Bazı girişler **hızlı bağlantılar** menü ekranın sağ tarafındaki tarafından kesilmiş.</span><span class="sxs-lookup"><span data-stu-id="4a25d-196">Some entries in the **Quick Links** menu may be cut off by the right side of the screen.</span></span> <span data-ttu-id="4a25d-197">Bu durumda, farenizi kullanarak menüsünü genişletin ve ekran menü geri kalanını görmek için sağa kaydırma için sağ ok tuşunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="4a25d-197">If so, expand the menu using your mouse and use the right arrow key to scroll the screen to the right to see the rest of the menu.</span></span>

4. <span data-ttu-id="4a25d-198">Aşağıdaki görüntüye benzer bir sayfa görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="4a25d-198">A page similar to the following image is displayed:</span></span>

    ![İş UI görüntüsü](./media/hdinsight-linux-ambari-ssh-tunnel/namenode.png)

   > [!NOTE]
   > <span data-ttu-id="4a25d-200">Bu sayfanın URL'sini dikkat edin. benzer olmalıdır **http://hn1-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8088/küme**.</span><span class="sxs-lookup"><span data-stu-id="4a25d-200">Notice the URL for this page; it should be similar to **http://hn1-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8088/cluster**.</span></span> <span data-ttu-id="4a25d-201">Bu URI düğümünün iç tam etki alanı adı (FQDN) kullanıyor ve SSH tüneli kullanırken, yalnızca erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="4a25d-201">This URI is using the internal fully qualified domain name (FQDN) of the node, and is only accessible when using an SSH tunnel.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4a25d-202">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4a25d-202">Next steps</span></span>

<span data-ttu-id="4a25d-203">SSH tüneli oluşturma ve öğrendiniz, Ambari kullanmak diğer yolları için aşağıdaki belgelere bakın:</span><span class="sxs-lookup"><span data-stu-id="4a25d-203">Now that you have learned how to create and use an SSH tunnel, see the following document for other ways to use Ambari:</span></span>

* [<span data-ttu-id="4a25d-204">Ambari kullanarak Hdınsight kümelerini yönetme</span><span class="sxs-lookup"><span data-stu-id="4a25d-204">Manage HDInsight clusters by using Ambari</span></span>](hdinsight-hadoop-manage-ambari.md)

<span data-ttu-id="4a25d-205">Hdınsight ile SSH kullanma hakkında daha fazla bilgi için bkz: [Hdınsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="4a25d-205">For more information on using SSH with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

