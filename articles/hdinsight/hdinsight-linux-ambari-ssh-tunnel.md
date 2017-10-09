---
title: "aaaUse SSH tünel tooaccess Azure Hdınsight | Microsoft Docs"
description: "Nasıl toouse bir SSH tünel toosecurely Gözat, Linux tabanlı Hdınsight düğümler üzerinde barındırılan web kaynaklar hakkında bilgi edinin."
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
ms.openlocfilehash: 8a315c53751bbe6950a182674f4108c67c2f2f8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-ssh-tunneling-tooaccess-ambari-web-ui-jobhistory-namenode-oozie-and-other-web-uis"></a><span data-ttu-id="57064-103">SSH tünel tooaccess Ambari web kullanıcı Arabirimi, kaynak, iş, Oozie ve diğer web Uı'lar kullanın</span><span class="sxs-lookup"><span data-stu-id="57064-103">Use SSH Tunneling tooaccess Ambari web UI, JobHistory, NameNode, Oozie, and other web UIs</span></span>

<span data-ttu-id="57064-104">Linux tabanlı Hdınsight kümeleri hello Internet üzerinden erişim tooAmbari web kullanıcı Arabirimi sağlar, ancak hello UI özelliklerinden bazıları değildir.</span><span class="sxs-lookup"><span data-stu-id="57064-104">Linux-based HDInsight clusters provide access tooAmbari web UI over hello Internet, but some features of hello UI are not.</span></span> <span data-ttu-id="57064-105">Örneğin, hello web kullanıcı Arabirimi Ambari ortaya çıkmış diğer hizmetler için.</span><span class="sxs-lookup"><span data-stu-id="57064-105">For example, hello web UI for other services that are surfaced through Ambari.</span></span> <span data-ttu-id="57064-106">Merhaba Ambari web kullanıcı Arabirimi tam işlevsellik için bir SSH tünel toohello küme baş kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="57064-106">For full functionality of hello Ambari web UI, you must use an SSH tunnel toohello cluster head.</span></span>

## <a name="why-use-an-ssh-tunnel"></a><span data-ttu-id="57064-107">SSH tüneli neden kullanılır?</span><span class="sxs-lookup"><span data-stu-id="57064-107">Why use an SSH tunnel</span></span>

<span data-ttu-id="57064-108">Ambari hello menülerde çeşitli yalnızca SSH tüneli çalışır.</span><span class="sxs-lookup"><span data-stu-id="57064-108">Several of hello menus in Ambari only work through an SSH tunnel.</span></span> <span data-ttu-id="57064-109">Bu menüler web siteleri ve alt düğümleri gibi diğer düğüm türleri üzerinde çalışan hizmetleri kullanır.</span><span class="sxs-lookup"><span data-stu-id="57064-109">These menus rely on web sites and services running on other node types, such as worker nodes.</span></span> <span data-ttu-id="57064-110">Genellikle, bu web sitelerinin güvenli değildir, güvenli toodirectly sunmaya olmadığı için kendilerine Internet hello.</span><span class="sxs-lookup"><span data-stu-id="57064-110">Often, these web sites are not secured, so it is not safe toodirectly expose them on hello internet.</span></span>

<span data-ttu-id="57064-111">Web Uı'lar aşağıdaki hello SSH tüneli gerektirir:</span><span class="sxs-lookup"><span data-stu-id="57064-111">hello following Web UIs require an SSH tunnel:</span></span>

* <span data-ttu-id="57064-112">Kaynak</span><span class="sxs-lookup"><span data-stu-id="57064-112">JobHistory</span></span>
* <span data-ttu-id="57064-113">İş</span><span class="sxs-lookup"><span data-stu-id="57064-113">NameNode</span></span>
* <span data-ttu-id="57064-114">İş parçacığı yığınları</span><span class="sxs-lookup"><span data-stu-id="57064-114">Thread Stacks</span></span>
* <span data-ttu-id="57064-115">Oozie web kullanıcı Arabirimi</span><span class="sxs-lookup"><span data-stu-id="57064-115">Oozie web UI</span></span>
* <span data-ttu-id="57064-116">HBase ana ve günlükleri kullanıcı Arabirimi</span><span class="sxs-lookup"><span data-stu-id="57064-116">HBase Master and Logs UI</span></span>

<span data-ttu-id="57064-117">Betik eylemleri toocustomize kümenizi kullanırsanız, herhangi bir hizmet veya bir web kullanıcı arabirimini kullanıma yüklediğiniz utilities SSH tüneli gerektirir.</span><span class="sxs-lookup"><span data-stu-id="57064-117">If you use Script Actions toocustomize your cluster, any services or utilities that you install that expose a web UI require an SSH tunnel.</span></span> <span data-ttu-id="57064-118">Örneğin, bir betik eylemi kullanarak ton yüklerseniz, bir SSH tünel tooaccess hello Hue web kullanıcı arabirimini kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="57064-118">For example, if you install Hue using a Script Action, you must use an SSH tunnel tooaccess hello Hue web UI.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="57064-119">Bir sanal ağ üzerinden doğrudan erişim tooHDInsight varsa, toouse SSH tünelleri gerekmez.</span><span class="sxs-lookup"><span data-stu-id="57064-119">If you have direct access tooHDInsight through a virtual network, you do not need toouse SSH tunnels.</span></span> <span data-ttu-id="57064-120">Merhaba doğrudan Hdınsight aracılığıyla bir sanal ağ erişimini ilişkin bir örnek için bkz: [bağlanmak Hdınsight tooyour şirket içi ağ](connect-on-premises-network.md) belge.</span><span class="sxs-lookup"><span data-stu-id="57064-120">For an example of directly accessing HDInsight through a virtual network, see hello [Connect HDInsight tooyour on-premises network](connect-on-premises-network.md) document.</span></span>

## <a name="what-is-an-ssh-tunnel"></a><span data-ttu-id="57064-121">SSH tüneli nedir</span><span class="sxs-lookup"><span data-stu-id="57064-121">What is an SSH tunnel</span></span>

<span data-ttu-id="57064-122">[Güvenli Kabuk (SSH) tüneli](https://en.wikipedia.org/wiki/Tunneling_protocol#Secure_Shell_tunneling) tooa bağlantı yerel iş istasyonunda gönderilen trafiğini yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="57064-122">[Secure Shell (SSH) tunneling](https://en.wikipedia.org/wiki/Tunneling_protocol#Secure_Shell_tunneling) routes traffic sent tooa port on your local workstation.</span></span> <span data-ttu-id="57064-123">Merhaba trafik bir SSH bağlantısı tooyour Hdınsight küme baş düğümüne yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="57064-123">hello traffic is routed through an SSH connection tooyour HDInsight cluster head node.</span></span> <span data-ttu-id="57064-124">Merhaba baş düğümünde geldiyse gibi hello isteği çözümlenir.</span><span class="sxs-lookup"><span data-stu-id="57064-124">hello request is resolved as if it originated on hello head node.</span></span> <span data-ttu-id="57064-125">Merhaba yanıt sonra geri hello tünel tooyour iş istasyonu yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="57064-125">hello response is then routed back through hello tunnel tooyour workstation.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="57064-126">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="57064-126">Prerequisites</span></span>

* <span data-ttu-id="57064-127">Bir SSH istemcisi.</span><span class="sxs-lookup"><span data-stu-id="57064-127">An SSH client.</span></span> <span data-ttu-id="57064-128">Daha fazla bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="57064-128">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="57064-129">Olabilir bir web tarayıcısı toouse SOCKS5 proxy yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="57064-129">A web browser that can be configured toouse a SOCKS5 proxy.</span></span>

    > [!WARNING]
    > <span data-ttu-id="57064-130">Windows'da yerleşik hello SOCKS proxy desteği SOCKS5 desteklemez ve bu belgedeki hello adımlara çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="57064-130">hello SOCKS proxy support built into Windows does not support SOCKS5, and does not work with hello steps in this document.</span></span> <span data-ttu-id="57064-131">Hello aşağıdaki tarayıcılardan Windows proxy ayarlarını kullanır ve hello adımları bu belgede çalışmak desteklemez:</span><span class="sxs-lookup"><span data-stu-id="57064-131">hello following browsers rely on Windows proxy settings, and do not currently work with hello steps in this document:</span></span>
    >
    > * <span data-ttu-id="57064-132">Microsoft Edge</span><span class="sxs-lookup"><span data-stu-id="57064-132">Microsoft Edge</span></span>
    > * <span data-ttu-id="57064-133">Microsoft Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="57064-133">Microsoft Internet Explorer</span></span>
    >
    > <span data-ttu-id="57064-134">Google Chrome ayrıca hello Windows proxy ayarlarını kullanır.</span><span class="sxs-lookup"><span data-stu-id="57064-134">Google Chrome also relies on hello Windows proxy settings.</span></span> <span data-ttu-id="57064-135">Ancak, SOCKS5 Destek Uzantıları yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="57064-135">However, you can install extensions that support SOCKS5.</span></span> <span data-ttu-id="57064-136">Öneririz [FoxyProxy standart](https://chrome.google.com/webstore/detail/foxyproxy-standard/gcknhkkoolaabfmlnjonogaaifnjlfnp).</span><span class="sxs-lookup"><span data-stu-id="57064-136">We recommend [FoxyProxy Standard](https://chrome.google.com/webstore/detail/foxyproxy-standard/gcknhkkoolaabfmlnjonogaaifnjlfnp).</span></span>

## <span data-ttu-id="57064-137"><a name="usessh"></a>Merhaba SSH komutunu kullanarak bir tünel oluşturma</span><span class="sxs-lookup"><span data-stu-id="57064-137"><a name="usessh"></a>Create a tunnel using hello SSH command</span></span>

<span data-ttu-id="57064-138">Kullanım hello şu komutu toocreate hello kullanarak SSH tüneli `ssh` komutu.</span><span class="sxs-lookup"><span data-stu-id="57064-138">Use hello following command toocreate an SSH tunnel using hello `ssh` command.</span></span> <span data-ttu-id="57064-139">Değiştir **kullanıcı adı** Hdınsight kümesi ve değiştirmek için bir SSH kullanıcıyla **CLUSTERNAME** Hdınsight kümenize hello adı:</span><span class="sxs-lookup"><span data-stu-id="57064-139">Replace **USERNAME** with an SSH user for your HDInsight cluster, and replace **CLUSTERNAME** with hello name of your HDInsight cluster:</span></span>

```bash
ssh -C2qTnNf -D 9876 USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
```

<span data-ttu-id="57064-140">Bu komut, SSH üzerinden trafik toolocal bağlantı noktası 9876 toohello küme yönlendiren bir bağlantı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="57064-140">This command creates a connection that routes traffic toolocal port 9876 toohello cluster over SSH.</span></span> <span data-ttu-id="57064-141">Başlangıç seçenekleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="57064-141">hello options are:</span></span>

* <span data-ttu-id="57064-142">**D 9876** -hello hello tüneli üzerinden trafiğini yönlendiren yerel bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="57064-142">**D 9876** - hello local port that routes traffic through hello tunnel.</span></span>
* <span data-ttu-id="57064-143">**C** -web trafiği çoğunlukla metin olduğundan tüm verileri sıkıştırmak.</span><span class="sxs-lookup"><span data-stu-id="57064-143">**C** - Compress all data, because web traffic is mostly text.</span></span>
* <span data-ttu-id="57064-144">**2** -force SSH tootry Protokolü sürüm 2 yalnızca.</span><span class="sxs-lookup"><span data-stu-id="57064-144">**2** - Force SSH tootry protocol version 2 only.</span></span>
* <span data-ttu-id="57064-145">**q** -Sessiz mod.</span><span class="sxs-lookup"><span data-stu-id="57064-145">**q** - Quiet mode.</span></span>
* <span data-ttu-id="57064-146">**T** -biz yalnızca bir bağlantı noktası iletme beri sözde tty ayırma, devre dışı.</span><span class="sxs-lookup"><span data-stu-id="57064-146">**T** - Disable pseudo-tty allocation, since we are just forwarding a port.</span></span>
* <span data-ttu-id="57064-147">**n**-STDIN, okunması biz yalnızca bir bağlantı noktası iletme beri engelleyin.</span><span class="sxs-lookup"><span data-stu-id="57064-147">**n** - Prevent reading of STDIN, since we are just forwarding a port.</span></span>
* <span data-ttu-id="57064-148">**N** -biz yalnızca bir bağlantı noktası iletme olduğundan bir uzak komutu yürütülmez.</span><span class="sxs-lookup"><span data-stu-id="57064-148">**N** - Do not execute a remote command, since we are just forwarding a port.</span></span>
* <span data-ttu-id="57064-149">**f** -hello arka planda çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="57064-149">**f** - Run in hello background.</span></span>

<span data-ttu-id="57064-150">Merhaba komut bittikten sonra gönderilen trafiğin tooport 9876 hello yerel bilgisayarda yönlendirilmiş toohello küme baş düğümüne ' dir.</span><span class="sxs-lookup"><span data-stu-id="57064-150">Once hello command finishes, traffic sent tooport 9876 on hello local computer is routed toohello cluster head node.</span></span>

## <span data-ttu-id="57064-151"><a name="useputty"></a>PuTTY kullanarak bir tünel oluşturma</span><span class="sxs-lookup"><span data-stu-id="57064-151"><a name="useputty"></a>Create a tunnel using PuTTY</span></span>

<span data-ttu-id="57064-152">[PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty) Windows için grafik SSH istemcidir.</span><span class="sxs-lookup"><span data-stu-id="57064-152">[PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty) is a graphical SSH client for Windows.</span></span> <span data-ttu-id="57064-153">PuTTY kullanarak SSH tüneli adımları toocreate aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="57064-153">Use hello following steps toocreate an SSH tunnel using PuTTY:</span></span>

1. <span data-ttu-id="57064-154">Putty'yi açın ve bağlantı bilgilerinizi girin.</span><span class="sxs-lookup"><span data-stu-id="57064-154">Open PuTTY, and enter your connection information.</span></span> <span data-ttu-id="57064-155">Merhaba PuTTY ile bilmiyorsanız bkz [PuTTY belgeleri (http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html)](http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html).</span><span class="sxs-lookup"><span data-stu-id="57064-155">If you are not familiar with PuTTY, see hello [PuTTY documentation (http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html)](http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html).</span></span>

2. <span data-ttu-id="57064-156">Merhaba, **kategori** bölüm toohello sol hello iletişim, genişletin **bağlantı**, genişletin **SSH**ve ardından **tüneller**.</span><span class="sxs-lookup"><span data-stu-id="57064-156">In hello **Category** section toohello left of hello dialog, expand **Connection**, expand **SSH**, and then select **Tunnels**.</span></span>

3. <span data-ttu-id="57064-157">Merhaba üzerinde aşağıdaki bilgilerle hello sağlamak **SSH denetleme seçenekleri bağlantı noktası iletme** form:</span><span class="sxs-lookup"><span data-stu-id="57064-157">Provide hello following information on hello **Options controlling SSH port forwarding** form:</span></span>
   
   * <span data-ttu-id="57064-158">**Kaynak bağlantı noktası** -hello hello istemci tooforward istediğiniz bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="57064-158">**Source port** - hello port on hello client that you wish tooforward.</span></span> <span data-ttu-id="57064-159">Örneğin, **9876**.</span><span class="sxs-lookup"><span data-stu-id="57064-159">For example, **9876**.</span></span>

   * <span data-ttu-id="57064-160">**Hedef** -hello Linux tabanlı Hdınsight kümesi için SSH adresi hello.</span><span class="sxs-lookup"><span data-stu-id="57064-160">**Destination** - hello SSH address for hello Linux-based HDInsight cluster.</span></span> <span data-ttu-id="57064-161">Örneğin, **mycluster-ssh.azurehdinsight.net**.</span><span class="sxs-lookup"><span data-stu-id="57064-161">For example, **mycluster-ssh.azurehdinsight.net**.</span></span>

   * <span data-ttu-id="57064-162">**Dinamik** - Dinamik SOCKS proxy yönlendirmesini etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="57064-162">**Dynamic** - Enables dynamic SOCKS proxy routing.</span></span>
     
     ![Görüntü seçenekleri tünel](./media/hdinsight-linux-ambari-ssh-tunnel/puttytunnel.png)

4. <span data-ttu-id="57064-164">Tıklatın **Ekle** tooadd hello ayarları ve ardından **açık** tooopen bir SSH bağlantısı.</span><span class="sxs-lookup"><span data-stu-id="57064-164">Click **Add** tooadd hello settings, and then click **Open** tooopen an SSH connection.</span></span>

5. <span data-ttu-id="57064-165">İstendiğinde, toohello Server'da oturum açın.</span><span class="sxs-lookup"><span data-stu-id="57064-165">When prompted, log in toohello server.</span></span>

## <a name="use-hello-tunnel-from-your-browser"></a><span data-ttu-id="57064-166">Merhaba tünel tarayıcınızdan kullanın</span><span class="sxs-lookup"><span data-stu-id="57064-166">Use hello tunnel from your browser</span></span>

> [!IMPORTANT]
> <span data-ttu-id="57064-167">aynı proxy ayarları tüm platformlarda hello sağladığı gibi hello bu bölümü kullanın hello Mozilla FireFox tarayıcı adımlar.</span><span class="sxs-lookup"><span data-stu-id="57064-167">hello steps in this section use hello Mozilla FireFox browser, as it provides hello same proxy settings across all platforms.</span></span> <span data-ttu-id="57064-168">Google Chrome gibi modern tarayıcılar uzantı hello tünel ile FoxyProxy toowork gibi gerektirebilir.</span><span class="sxs-lookup"><span data-stu-id="57064-168">Other modern browsers, such as Google Chrome, may require an extension such as FoxyProxy toowork with hello tunnel.</span></span>

1. <span data-ttu-id="57064-169">Merhaba tarayıcı toouse yapılandırma **localhost** ve ne zaman kullanılan başlangıç bağlantı noktası olarak hello tünel oluşturma bir **SOCKS v5** proxy.</span><span class="sxs-lookup"><span data-stu-id="57064-169">Configure hello browser toouse **localhost** and hello port you used when creating hello tunnel as a **SOCKS v5** proxy.</span></span> <span data-ttu-id="57064-170">İşte hello Firefox ayarlarını gibi arayın.</span><span class="sxs-lookup"><span data-stu-id="57064-170">Here's what hello Firefox settings look like.</span></span> <span data-ttu-id="57064-171">Farklı bir bağlantı noktasıyla 9876 kullandıysanız, başlangıç bağlantı noktası toohello hangisini kullanılan değiştirin:</span><span class="sxs-lookup"><span data-stu-id="57064-171">If you used a different port than 9876, change hello port toohello one you used:</span></span>
   
    ![Firefox ayarlarının görüntüsü](./media/hdinsight-linux-ambari-ssh-tunnel/firefoxproxy.png)
   
   > [!NOTE]
   > <span data-ttu-id="57064-173">Seçme **uzak DNS** hello Hdınsight kümesi kullanarak etki alanı adı sistemi (DNS) isteklerinin giderir.</span><span class="sxs-lookup"><span data-stu-id="57064-173">Selecting **Remote DNS** resolves Domain Name System (DNS) requests by using hello HDInsight cluster.</span></span> <span data-ttu-id="57064-174">Bu ayar hello küme baş düğümüne hello kullanarak DNS çözümler.</span><span class="sxs-lookup"><span data-stu-id="57064-174">This setting resolves DNS using hello head node of hello cluster.</span></span>

2. <span data-ttu-id="57064-175">Merhaba tünel çalıştığını gibi bir siteyi ziyaret ederek doğrula [http://www.whatismyip.com/](http://www.whatismyip.com/).</span><span class="sxs-lookup"><span data-stu-id="57064-175">Verify that hello tunnel works by visiting a site such as [http://www.whatismyip.com/](http://www.whatismyip.com/).</span></span> <span data-ttu-id="57064-176">Merhaba IP bir hello Microsoft Azure veri merkezi tarafından kullanılması gereken döndürdü.</span><span class="sxs-lookup"><span data-stu-id="57064-176">hello IP returned should be one used by hello Microsoft Azure datacenter.</span></span>

## <a name="verify-with-ambari-web-ui"></a><span data-ttu-id="57064-177">Ambari web kullanıcı Arabirimi ile doğrulayın</span><span class="sxs-lookup"><span data-stu-id="57064-177">Verify with Ambari web UI</span></span>

<span data-ttu-id="57064-178">Merhaba küme kurulduktan sonra hello Ambari Web hizmeti web Uı'lar erişebilirsiniz adımları tooverify aşağıdaki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="57064-178">Once hello cluster has been established, use hello following steps tooverify that you can access service web UIs from hello Ambari Web:</span></span>

1. <span data-ttu-id="57064-179">Tarayıcınızda, toohttp://headnodehost:8080 gidin.</span><span class="sxs-lookup"><span data-stu-id="57064-179">In your browser, go toohttp://headnodehost:8080.</span></span> <span data-ttu-id="57064-180">Merhaba `headnodehost` adresi hello tünel toohello küme gönderilir ve ambarı üzerinde çalıştığı toohello headnode çözümleyin.</span><span class="sxs-lookup"><span data-stu-id="57064-180">hello `headnodehost` address is sent over hello tunnel toohello cluster and resolve toohello headnode that Ambari is running on.</span></span> <span data-ttu-id="57064-181">İstendiğinde, kümeniz için hello yönetici kullanıcı adı (Yönetici) ve parola girin.</span><span class="sxs-lookup"><span data-stu-id="57064-181">When prompted, enter hello admin user name (admin) and password for your cluster.</span></span> <span data-ttu-id="57064-182">Merhaba Ambari web kullanıcı Arabirimi tarafından ikinci kez istenebilir.</span><span class="sxs-lookup"><span data-stu-id="57064-182">You may be prompted a second time by hello Ambari web UI.</span></span> <span data-ttu-id="57064-183">Bu durumda, hello bilgileri yeniden girin.</span><span class="sxs-lookup"><span data-stu-id="57064-183">If so, reenter hello information.</span></span>

   > [!NOTE]
   > <span data-ttu-id="57064-184">Merhaba http://headnodehost:8080 adresi tooconnect toohello küme kullanırken hello tünelinden bağlanırsınız.</span><span class="sxs-lookup"><span data-stu-id="57064-184">When using hello http://headnodehost:8080 address tooconnect toohello cluster, you are connecting through hello tunnel.</span></span> <span data-ttu-id="57064-185">İletişim HTTPS yerine hello SSH tüneli kullanılarak güvenli hale getirilir.</span><span class="sxs-lookup"><span data-stu-id="57064-185">Communication is secured using hello SSH tunnel instead of HTTPS.</span></span> <span data-ttu-id="57064-186">tooconnect üzerinde HTTPS kullanarak Internet Merhaba, https://CLUSTERNAME.azurehdinsight.net, kullanın nerede **CLUSTERNAME** hello küme hello adıdır.</span><span class="sxs-lookup"><span data-stu-id="57064-186">tooconnect over hello internet using HTTPS, use https://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is hello name of hello cluster.</span></span>

2. <span data-ttu-id="57064-187">Ambari Web kullanıcı arabirimini Hello HDFS hello sayfasının hello soldaki hello listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="57064-187">From hello Ambari Web UI, select HDFS from hello list on hello left of hello page.</span></span>

    ![Seçili HDFS görüntüsüyle](./media/hdinsight-linux-ambari-ssh-tunnel/hdfsservice.png)

3. <span data-ttu-id="57064-189">Merhaba HDFS hizmet bilgileri görüntülendiğinde seçin **hızlı bağlantılar**.</span><span class="sxs-lookup"><span data-stu-id="57064-189">When hello HDFS service information is displayed, select **Quick Links**.</span></span> <span data-ttu-id="57064-190">Merhaba küme baş düğümler listesi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="57064-190">A list of hello cluster head nodes appears.</span></span> <span data-ttu-id="57064-191">Merhaba baş düğümler birini seçin ve ardından **iş UI**.</span><span class="sxs-lookup"><span data-stu-id="57064-191">Select one of hello head nodes, and then select **NameNode UI**.</span></span>

    ![Görüntü hello QuickLinks menüsü ile genişletilmiş](./media/hdinsight-linux-ambari-ssh-tunnel/namenodedropdown.png)

   > [!NOTE]
   > <span data-ttu-id="57064-193">Seçtiğinizde, __hızlı bağlantılar__, bekleme göstergesi alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="57064-193">When you select __Quick Links__, you may get a wait indicator.</span></span> <span data-ttu-id="57064-194">Yavaş bir internet bağlantınız varsa, bu durum oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="57064-194">This condition can occur if you have a slow internet connection.</span></span> <span data-ttu-id="57064-195">Bir veya iki hello sunucudan alınan hello veri toobe için dakika bekleyin ve sonra hello listesi tekrar deneyin.</span><span class="sxs-lookup"><span data-stu-id="57064-195">Wait a minute or two for hello data toobe received from hello server, then try hello list again.</span></span>
   >
   > <span data-ttu-id="57064-196">Merhaba, bazı girişler **hızlı bağlantılar** menü hello ekranın sağ tarafında hello tarafından kesilmiş.</span><span class="sxs-lookup"><span data-stu-id="57064-196">Some entries in hello **Quick Links** menu may be cut off by hello right side of hello screen.</span></span> <span data-ttu-id="57064-197">Bu durumda, farenizi kullanarak hello menüsünü genişletin ve hello sağ ok anahtar tooscroll hello ekran toohello sağ toosee hello geri kalanı hello menüsünü kullanın.</span><span class="sxs-lookup"><span data-stu-id="57064-197">If so, expand hello menu using your mouse and use hello right arrow key tooscroll hello screen toohello right toosee hello rest of hello menu.</span></span>

4. <span data-ttu-id="57064-198">Aşağıdaki görüntü bir sayfa benzer toohello görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="57064-198">A page similar toohello following image is displayed:</span></span>

    ![Merhaba iş UI görüntüsü](./media/hdinsight-linux-ambari-ssh-tunnel/namenode.png)

   > [!NOTE]
   > <span data-ttu-id="57064-200">Bu sayfa için Hello URL dikkat edin. çok benzer olmalıdır**http://hn1-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8088/küme**.</span><span class="sxs-lookup"><span data-stu-id="57064-200">Notice hello URL for this page; it should be similar too**http://hn1-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8088/cluster**.</span></span> <span data-ttu-id="57064-201">Bu URI hello iç hello düğümün tam etki alanı adı (FQDN) kullanıyor ve SSH tüneli kullanırken, yalnızca erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="57064-201">This URI is using hello internal fully qualified domain name (FQDN) of hello node, and is only accessible when using an SSH tunnel.</span></span>

## <a name="next-steps"></a><span data-ttu-id="57064-202">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="57064-202">Next steps</span></span>

<span data-ttu-id="57064-203">Nasıl toocreate ve kullanım SSH tüneli bkz belge diğer yolları toouse Ambari için aşağıdaki hello öğrendiğinize göre:</span><span class="sxs-lookup"><span data-stu-id="57064-203">Now that you have learned how toocreate and use an SSH tunnel, see hello following document for other ways toouse Ambari:</span></span>

* [<span data-ttu-id="57064-204">Ambari kullanarak Hdınsight kümelerini yönetme</span><span class="sxs-lookup"><span data-stu-id="57064-204">Manage HDInsight clusters by using Ambari</span></span>](hdinsight-hadoop-manage-ambari.md)

<span data-ttu-id="57064-205">Hdınsight ile SSH kullanma hakkında daha fazla bilgi için bkz: [Hdınsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="57064-205">For more information on using SSH with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

