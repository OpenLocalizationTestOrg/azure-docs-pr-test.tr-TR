---
title: "aaaMonitor ve Azure Hdınsight Ambari Web kullanıcı arabirimini kullanarak yönetme | Microsoft Docs"
description: "Bilgi nasıl toouse Ambari toomonitor ve Linux tabanlı Hdınsight kümelerini yönetme. Bu belgede nasıl toouse hello Ambari Web kullanıcı arabirimini Hdınsight ile dahil kümeleri öğrenin."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 4787f3cc-a650-4dc3-9d96-a19a67aad046
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: d422c40e63345d7054839a625e115c50dad040f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hdinsight-clusters-by-using-hello-ambari-web-ui"></a><span data-ttu-id="aad6a-104">Merhaba Ambari Web kullanıcı arabirimini kullanarak Hdınsight kümelerini yönetme</span><span class="sxs-lookup"><span data-stu-id="aad6a-104">Manage HDInsight clusters by using hello Ambari Web UI</span></span>

[!INCLUDE [ambari-selector](../../includes/hdinsight-ambari-selector.md)]

<span data-ttu-id="aad6a-105">Apache Ambari hello yönetimi ve Hadoop kümesi kolay toouse web kullanıcı Arabirimi ve REST API'si sağlayarak izlemenin basitleştirir.</span><span class="sxs-lookup"><span data-stu-id="aad6a-105">Apache Ambari simplifies hello management and monitoring of a Hadoop cluster by providing an easy toouse web UI and REST API.</span></span> <span data-ttu-id="aad6a-106">Ambari Linux tabanlı Hdınsight kümelerine dahil ve kullanılan toomonitor hello olan küme yapılandırması değişiklikler yapın.</span><span class="sxs-lookup"><span data-stu-id="aad6a-106">Ambari is included on Linux-based HDInsight clusters, and is used toomonitor hello cluster and make configuration changes.</span></span>

<span data-ttu-id="aad6a-107">Bu belgede nasıl toouse hello Ambari Web kullanıcı Arabirimi bir Hdınsight kümesini öğrenin.</span><span class="sxs-lookup"><span data-stu-id="aad6a-107">In this document, you learn how toouse hello Ambari Web UI with an HDInsight cluster.</span></span>

## <span data-ttu-id="aad6a-108"><a id="whatis"></a>Ambari nedir?</span><span class="sxs-lookup"><span data-stu-id="aad6a-108"><a id="whatis"></a>What is Ambari?</span></span>

<span data-ttu-id="aad6a-109">[Apache Ambari](http://ambari.apache.org) kullanımı kolay web kullanıcı Arabirimi sağlayarak Hadoop yönetimini basitleştirir.</span><span class="sxs-lookup"><span data-stu-id="aad6a-109">[Apache Ambari](http://ambari.apache.org) simplifies Hadoop management by providing an easy-to-use web UI.</span></span> <span data-ttu-id="aad6a-110">Ambari kullanabileceğiniz oluşturmak, yönetmek ve Hadoop kümelerini izleme.</span><span class="sxs-lookup"><span data-stu-id="aad6a-110">You can use Ambari create, manage, and monitor Hadoop clusters.</span></span> <span data-ttu-id="aad6a-111">Geliştiriciler tümleştirebilir Bu yetenekler uygulamalarına hello kullanarak [Ambari REST API'leri](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span><span class="sxs-lookup"><span data-stu-id="aad6a-111">Developers can integrate these capabilities into their applications by using hello [Ambari REST APIs](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

<span data-ttu-id="aad6a-112">Merhaba Ambari Web kullanıcı Arabirimi, varsayılan olarak hello Linux işletim sistemi kullanmak Hdınsight kümeleri ile sağlanır.</span><span class="sxs-lookup"><span data-stu-id="aad6a-112">hello Ambari Web UI is provided by default with HDInsight clusters that use hello Linux operating system.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="aad6a-113">Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir.</span><span class="sxs-lookup"><span data-stu-id="aad6a-113">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="aad6a-114">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="aad6a-114">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> 

## <a name="connectivity"></a><span data-ttu-id="aad6a-115">Bağlantı</span><span class="sxs-lookup"><span data-stu-id="aad6a-115">Connectivity</span></span>

<span data-ttu-id="aad6a-116">Merhaba Ambari Web kullanıcı Arabirimi, HTTPS://CLUSTERNAME.azurehdidnsight.net, konumunda Hdınsight kümenize kullanılabilir olduğu **CLUSTERNAME** hello kümenizin adıdır.</span><span class="sxs-lookup"><span data-stu-id="aad6a-116">hello Ambari Web UI is available on your HDInsight cluster at HTTPS://CLUSTERNAME.azurehdidnsight.net, where **CLUSTERNAME** is hello name of your cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="aad6a-117">Hdınsight üzerinde tooAmbari bağlanırken HTTPS gerektirir.</span><span class="sxs-lookup"><span data-stu-id="aad6a-117">Connecting tooAmbari on HDInsight requires HTTPS.</span></span> <span data-ttu-id="aad6a-118">Kimlik doğrulaması için istendiğinde hello Yönetici hesap adı ve parola hello küme oluştururken verdiğiniz kullanın.</span><span class="sxs-lookup"><span data-stu-id="aad6a-118">When prompted for authentication, use hello admin account name and password you provided when hello cluster was created.</span></span>

## <a name="ssh-tunnel-proxy"></a><span data-ttu-id="aad6a-119">SSH tüneli (proxy)</span><span class="sxs-lookup"><span data-stu-id="aad6a-119">SSH tunnel (proxy)</span></span>

<span data-ttu-id="aad6a-120">Kümeniz için Ambari hello doğrudan Internet erişilebilir olsa da, bazı Ambari Web kullanıcı Arabirimi (örneğin, toohello Jobtracker'a) üzerinde gösterilmez hello bağlantılarından Internet hello.</span><span class="sxs-lookup"><span data-stu-id="aad6a-120">While Ambari for your cluster is accessible directly over hello Internet, some links from hello Ambari Web UI (such as toohello JobTracker) are not exposed on hello internet.</span></span> <span data-ttu-id="aad6a-121">Bu hizmetleri tooaccess SSH tüneli oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="aad6a-121">tooaccess these services, you must create an SSH tunnel.</span></span> <span data-ttu-id="aad6a-122">Daha fazla bilgi için bkz: [kullanım SSH tünel Hdınsight ile](hdinsight-linux-ambari-ssh-tunnel.md).</span><span class="sxs-lookup"><span data-stu-id="aad6a-122">For more information, see [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md).</span></span>

## <a name="ambari-web-ui"></a><span data-ttu-id="aad6a-123">Ambari Web kullanıcı Arabirimi</span><span class="sxs-lookup"><span data-stu-id="aad6a-123">Ambari Web UI</span></span>

<span data-ttu-id="aad6a-124">Toohello Ambari Web kullanıcı arabirimini bağlanırken istendiğinde tooauthenticate toohello sayfa görünüyor.</span><span class="sxs-lookup"><span data-stu-id="aad6a-124">When connecting toohello Ambari Web UI, you are prompted tooauthenticate toohello page.</span></span> <span data-ttu-id="aad6a-125">Merhaba küme yönetici kullanıcı (varsayılan Yönetici) ve küme oluşturma sırasında kullanılan parola kullanın.</span><span class="sxs-lookup"><span data-stu-id="aad6a-125">Use hello cluster admin user (default Admin) and password you used during cluster creation.</span></span>

<span data-ttu-id="aad6a-126">Başlangıç sayfası açıldığında, hello çubuğu hello üstünde unutmayın.</span><span class="sxs-lookup"><span data-stu-id="aad6a-126">When hello page opens, note hello bar at hello top.</span></span> <span data-ttu-id="aad6a-127">Bu çubuğu hello aşağıdakileri içeren bilgileri ve denetimleri:</span><span class="sxs-lookup"><span data-stu-id="aad6a-127">This bar contains hello following information and controls:</span></span>

![ambari nav](./media/hdinsight-hadoop-manage-ambari/ambari-nav.png)

* <span data-ttu-id="aad6a-129">**Ambari logosu** -açılır hello Pano kullanılan toomonitor hello kümesi olabilir.</span><span class="sxs-lookup"><span data-stu-id="aad6a-129">**Ambari logo** - Opens hello dashboard, which can be used toomonitor hello cluster.</span></span>

* <span data-ttu-id="aad6a-130">**Küme adı # ops** -devam eden ambarı işlemler hello sayısını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="aad6a-130">**Cluster name # ops** - Displays hello number of ongoing Ambari operations.</span></span> <span data-ttu-id="aad6a-131">Seçme hello küme adı veya **# ops** arka plan işlemleri listesini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="aad6a-131">Selecting hello cluster name or **# ops** displays a list of background operations.</span></span>

* <span data-ttu-id="aad6a-132">**# Uyarıları** -görüntüler uyarı veya kritik uyarı durumunda hello küme.</span><span class="sxs-lookup"><span data-stu-id="aad6a-132">**# alerts** - Displays warnings or critical alerts, if any, for hello cluster.</span></span>

* <span data-ttu-id="aad6a-133">**Pano** -görüntüler hello Pano.</span><span class="sxs-lookup"><span data-stu-id="aad6a-133">**Dashboard** - Displays hello dashboard.</span></span>

* <span data-ttu-id="aad6a-134">**Hizmetleri** -hello kümedeki hello Hizmetleri için bilgi ve yapılandırma ayarları.</span><span class="sxs-lookup"><span data-stu-id="aad6a-134">**Services** - Information and configuration settings for hello services in hello cluster.</span></span>

* <span data-ttu-id="aad6a-135">**Ana bilgisayar** -hello küme hello düğümler için bilgileri ve yapılandırma ayarları.</span><span class="sxs-lookup"><span data-stu-id="aad6a-135">**Hosts** - Information and configuration settings for hello nodes in hello cluster.</span></span>

* <span data-ttu-id="aad6a-136">**Uyarıları** -günlük bilgi, uyarı ve kritik uyarılar.</span><span class="sxs-lookup"><span data-stu-id="aad6a-136">**Alerts** - A log of information, warnings, and critical alerts.</span></span>

* <span data-ttu-id="aad6a-137">**Yönetici** -hello küme, hizmet hesabı bilgilerini ve Kerberos güvenlik yüklü yazılım yığını/Hizmetleri.</span><span class="sxs-lookup"><span data-stu-id="aad6a-137">**Admin** - Software stack/services that are installed on hello cluster, service account information, and Kerberos security.</span></span>

* <span data-ttu-id="aad6a-138">**Yönetici düğmesi** -ambarı yönetimi, kullanıcı ayarlarını ve oturum kapatma.</span><span class="sxs-lookup"><span data-stu-id="aad6a-138">**Admin button** - Ambari management, user settings, and logout.</span></span>

## <a name="monitoring"></a><span data-ttu-id="aad6a-139">İzleme</span><span class="sxs-lookup"><span data-stu-id="aad6a-139">Monitoring</span></span>

### <a name="alerts"></a><span data-ttu-id="aad6a-140">Uyarılar</span><span class="sxs-lookup"><span data-stu-id="aad6a-140">Alerts</span></span>

<span data-ttu-id="aad6a-141">Merhaba aşağıdaki listede hello ortak uyarı durumları Ambari tarafından kullanılan içerir:</span><span class="sxs-lookup"><span data-stu-id="aad6a-141">hello following list contains hello common alert statuses used by Ambari:</span></span>

* <span data-ttu-id="aad6a-142">**TAMAM**</span><span class="sxs-lookup"><span data-stu-id="aad6a-142">**OK**</span></span>
* <span data-ttu-id="aad6a-143">**Uyarı**</span><span class="sxs-lookup"><span data-stu-id="aad6a-143">**Warning**</span></span>
* <span data-ttu-id="aad6a-144">**KRİTİK**</span><span class="sxs-lookup"><span data-stu-id="aad6a-144">**CRITICAL**</span></span>
* <span data-ttu-id="aad6a-145">**BİLİNMEYEN**</span><span class="sxs-lookup"><span data-stu-id="aad6a-145">**UNKNOWN**</span></span>

<span data-ttu-id="aad6a-146">Dışındaki uyarıları **Tamam** hello neden **# uyarıları** girişi hello üstünde hello sayfa toodisplay hello uyarı sayısı.</span><span class="sxs-lookup"><span data-stu-id="aad6a-146">Alerts other than **OK** cause hello **# alerts** entry at hello top of hello page toodisplay hello number of alerts.</span></span> <span data-ttu-id="aad6a-147">Bu girdi seçerek hello uyarıları ve bunların durumunu görüntüler.</span><span class="sxs-lookup"><span data-stu-id="aad6a-147">Selecting this entry displays hello alerts and their status.</span></span>

<span data-ttu-id="aad6a-148">Uyarıları hello görüntülenebilir birkaç varsayılan gruplar halinde düzenlenir **uyarıları** sayfası.</span><span class="sxs-lookup"><span data-stu-id="aad6a-148">Alerts are organized into several default groups, which can be viewed from hello **Alerts** page.</span></span>

![Uyarılar sayfası](./media/hdinsight-hadoop-manage-ambari/alerts.png)

<span data-ttu-id="aad6a-150">Merhaba grupları hello kullanarak yönetebileceğiniz **Eylemler** menü ve seçerek **uyarı grupları yönet**.</span><span class="sxs-lookup"><span data-stu-id="aad6a-150">You can manage hello groups by using hello **Actions** menu and selecting **Manage Alert Groups**.</span></span>

![Uyarı gruplar iletişim yönetme](./media/hdinsight-hadoop-manage-ambari/manage-alerts.png)

<span data-ttu-id="aad6a-152">Ayrıca, uyarı yöntemleri yönetmek ve uyarı bildirimleri hello oluşturabilirsiniz **Eylemler** seçerek menü __yönetmek uyarı bildirimleri__.</span><span class="sxs-lookup"><span data-stu-id="aad6a-152">You can also manage alerting methods, and create alert notifications from hello **Actions** menu by selecting __Manage Alert Notifications__.</span></span> <span data-ttu-id="aad6a-153">Geçerli herhangi bir bildirim görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="aad6a-153">Any current notifications are displayed.</span></span> <span data-ttu-id="aad6a-154">Ayrıca, buradan bildirimler de oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aad6a-154">You can also create notifications from here.</span></span> <span data-ttu-id="aad6a-155">Bildirimler, üzerinden gönderilebilir **e-posta** veya **SNMP** belirli uyarı önem birleşimleri olduğunda.</span><span class="sxs-lookup"><span data-stu-id="aad6a-155">Notifications can be sent via **EMAIL** or **SNMP** when specific alert/severity combinations occur.</span></span> <span data-ttu-id="aad6a-156">Örneğin, bir e-posta iletisi hello uyarıların hiçbirini zaman hello gönderebilirsiniz **YARN varsayılan** grubunu çok Ayarla**kritik**.</span><span class="sxs-lookup"><span data-stu-id="aad6a-156">For example, you can send an email message when any of hello alerts in hello **YARN Default** group is set too**Critical**.</span></span>

![Uyarı iletişim kutusu oluşturma](./media/hdinsight-hadoop-manage-ambari/create-alert-notification.png)

<span data-ttu-id="aad6a-158">Son olarak, seçme __uyarı ayarlarını Yönet__ hello gelen __Eylemler__ menü tooset hello kaç kez bir uyarı gerekir görünmesi bir bildirim gönderilmeden önce sağlar.</span><span class="sxs-lookup"><span data-stu-id="aad6a-158">Finally, selecting __Manage Alert Settings__ from hello __Actions__ menu allows you tooset hello number of times an alert must occur before a notification is sent.</span></span> <span data-ttu-id="aad6a-159">Bu ayar, geçici hataları için kullanılan tooprevent bildirimleri olabilir.</span><span class="sxs-lookup"><span data-stu-id="aad6a-159">This setting can be used tooprevent notifications for transient errors.</span></span>

### <a name="cluster"></a><span data-ttu-id="aad6a-160">Küme</span><span class="sxs-lookup"><span data-stu-id="aad6a-160">Cluster</span></span>

<span data-ttu-id="aad6a-161">Merhaba **ölçümleri** hello Pano sekmesi kolay toomonitor hello kümenizi durumunu bir bakışta olun pencere öğeleri, bir dizi içerir.</span><span class="sxs-lookup"><span data-stu-id="aad6a-161">hello **Metrics** tab of hello dashboard contains a series of widgets that make it easy toomonitor hello status of your cluster at a glance.</span></span> <span data-ttu-id="aad6a-162">Birkaç pencere öğeleri gibi **CPU kullanımı**, tıklatıldığında ek bilgileri sağlayın.</span><span class="sxs-lookup"><span data-stu-id="aad6a-162">Several widgets, such as **CPU Usage**, provide additional information when clicked.</span></span>

![Pano ölçümlerle](./media/hdinsight-hadoop-manage-ambari/metrics.png)

<span data-ttu-id="aad6a-164">Merhaba **Heatmaps** sekmesi ölçümleri yeşil toored giderek renkli heatmaps olarak görüntüler.</span><span class="sxs-lookup"><span data-stu-id="aad6a-164">hello **Heatmaps** tab displays metrics as colored heatmaps, going from green toored.</span></span>

![Pano heatmaps ile](./media/hdinsight-hadoop-manage-ambari/heatmap.png)

<span data-ttu-id="aad6a-166">Merhaba kümede hello düğüm üzerinde daha fazla bilgi için seçin **ana**.</span><span class="sxs-lookup"><span data-stu-id="aad6a-166">For more information on hello nodes within hello cluster, select **Hosts**.</span></span> <span data-ttu-id="aad6a-167">Daha sonra ilgilendiğiniz hello belirli düğümünü seçin.</span><span class="sxs-lookup"><span data-stu-id="aad6a-167">Then select hello specific node you are interested in.</span></span>

![ana bilgisayar ayrıntıları](./media/hdinsight-hadoop-manage-ambari/host-details.png)

### <a name="services"></a><span data-ttu-id="aad6a-169">Hizmetler</span><span class="sxs-lookup"><span data-stu-id="aad6a-169">Services</span></span>

<span data-ttu-id="aad6a-170">Merhaba **Hizmetleri** kenar hello Panoda hello hello kümede çalışan hello hizmetlerinin durumunu hızlı fikir sağlar.</span><span class="sxs-lookup"><span data-stu-id="aad6a-170">hello **Services** sidebar on hello dashboard provides quick insight into hello status of hello services running on hello cluster.</span></span> <span data-ttu-id="aad6a-171">Çeşitli simgeler kullanılan tooindicate durumu veya alınması gereken eylemler olacaktır.</span><span class="sxs-lookup"><span data-stu-id="aad6a-171">Various icons are used tooindicate status or actions that should be taken.</span></span> <span data-ttu-id="aad6a-172">Örneğin, bir hizmet geri dönüşüm toobe gerekiyorsa sarı geri dönüşüm simgesi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="aad6a-172">For example, a yellow recycle symbol is displayed if a service needs toobe recycled.</span></span>

![Hizmetleri yan çubuğu](./media/hdinsight-hadoop-manage-ambari/service-bar.png)

> [!NOTE]
> <span data-ttu-id="aad6a-174">Görüntülenen hello Hizmetleri Hdınsight küme türleri ve sürümleri arasında farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="aad6a-174">hello services displayed differ between HDInsight cluster types and versions.</span></span> <span data-ttu-id="aad6a-175">Burada görüntülenen hello Hizmetleri kümeniz için görüntülenen hello Hizmetleri farklı olabilir.</span><span class="sxs-lookup"><span data-stu-id="aad6a-175">hello services displayed here may be different than hello services displayed for your cluster.</span></span>

<span data-ttu-id="aad6a-176">Bir hizmet seçmeden hello hizmette daha ayrıntılı bilgiler görüntüler.</span><span class="sxs-lookup"><span data-stu-id="aad6a-176">Selecting a service displays more detailed information on hello service.</span></span>

![Hizmet özet bilgileri](./media/hdinsight-hadoop-manage-ambari/service-details.png)

#### <a name="quick-links"></a><span data-ttu-id="aad6a-178">Hızlı bağlantılar</span><span class="sxs-lookup"><span data-stu-id="aad6a-178">Quick links</span></span>

<span data-ttu-id="aad6a-179">Bazı Hizmetleri görünen bir **hızlı bağlantılar** hello sayfanın üst kısmındaki hello bağlantı.</span><span class="sxs-lookup"><span data-stu-id="aad6a-179">Some services display a **Quick Links** link at hello top of hello page.</span></span> <span data-ttu-id="aad6a-180">Bu kullanılan tooaccess hizmete özgü web Uı'lar, aşağıdaki gibi olabilir:</span><span class="sxs-lookup"><span data-stu-id="aad6a-180">This can be used tooaccess service-specific web UIs, such as:</span></span>

* <span data-ttu-id="aad6a-181">**İş Geçmişi** -MapReduce iş geçmişi.</span><span class="sxs-lookup"><span data-stu-id="aad6a-181">**Job History** - MapReduce job history.</span></span>
* <span data-ttu-id="aad6a-182">**Resource Manager** -YARN ResourceManager UI.</span><span class="sxs-lookup"><span data-stu-id="aad6a-182">**Resource Manager** - YARN ResourceManager UI.</span></span>
* <span data-ttu-id="aad6a-183">**İş** -Hadoop dağıtılmış dosya sistemi (HDFS) iş UI.</span><span class="sxs-lookup"><span data-stu-id="aad6a-183">**NameNode** - Hadoop Distributed File System (HDFS) NameNode UI.</span></span>
* <span data-ttu-id="aad6a-184">**Oozie Web kullanıcı Arabirimi** -Oozie UI.</span><span class="sxs-lookup"><span data-stu-id="aad6a-184">**Oozie Web UI** - Oozie UI.</span></span>

<span data-ttu-id="aad6a-185">Aşağıdaki bağlantılardan birini seçerek yeni bir sekme hello seçili sayfasını görüntüler, tarayıcıda açılır.</span><span class="sxs-lookup"><span data-stu-id="aad6a-185">Selecting any of these links opens a new tab in your browser, which displays hello selected page.</span></span>

> [!NOTE]
> <span data-ttu-id="aad6a-186">Seçme hello **hızlı bağlantılar** girişi bir hizmet için "Sunucu bulunamadı" hata döndürebilir.</span><span class="sxs-lookup"><span data-stu-id="aad6a-186">Selecting hello **Quick Links** entry for a service may return a "server not found" error.</span></span> <span data-ttu-id="aad6a-187">Bu hatayla karşılaşırsanız, hello kullanırken SSH tüneli kullanmalısınız **hızlı bağlantılar** bu hizmet için girişi.</span><span class="sxs-lookup"><span data-stu-id="aad6a-187">If you encounter this error, you must use an SSH tunnel when using hello **Quick Links** entry for this service.</span></span> <span data-ttu-id="aad6a-188">Bilgi için bkz: [kullanım SSH tünel Hdınsight ile](hdinsight-linux-ambari-ssh-tunnel.md)</span><span class="sxs-lookup"><span data-stu-id="aad6a-188">For information, see [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md)</span></span>

## <a name="management"></a><span data-ttu-id="aad6a-189">Yönetim</span><span class="sxs-lookup"><span data-stu-id="aad6a-189">Management</span></span>

### <a name="ambari-users-groups-and-permissions"></a><span data-ttu-id="aad6a-190">Ambari kullanıcılar, gruplar ve izinler</span><span class="sxs-lookup"><span data-stu-id="aad6a-190">Ambari users, groups, and permissions</span></span>

<span data-ttu-id="aad6a-191">Kullanıcılar, gruplar ve izinler ile çalışma kullanılırken desteklenir bir [etki alanına katılmış](hdinsight-domain-joined-introduction.md) Hdınsight kümesi.</span><span class="sxs-lookup"><span data-stu-id="aad6a-191">Working with users, groups, and permissions are supported when using a [domain joined](hdinsight-domain-joined-introduction.md) HDInsight cluster.</span></span> <span data-ttu-id="aad6a-192">Etki alanına katılmış bir kümede hello ambarı Yönetimi kullanıcı arabirimini kullanma hakkında daha fazla bilgi için bkz: [etki alanına katılmış Hdınsight kümelerini yönetme](hdinsight-domain-joined-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="aad6a-192">For information on using hello Ambari Management UI on a domain-joined cluster, see [Manage domain-joined HDInsight clusters](hdinsight-domain-joined-introduction.md).</span></span>

> [!WARNING]
> <span data-ttu-id="aad6a-193">Linux tabanlı Hdınsight kümenizdeki hello Ambari izleme (hdinsightwatchdog) Hello parolasını değiştirmeyin.</span><span class="sxs-lookup"><span data-stu-id="aad6a-193">Do not change hello password of hello Ambari watchdog (hdinsightwatchdog) on your Linux-based HDInsight cluster.</span></span> <span data-ttu-id="aad6a-194">Merhaba parola sonları değiştirme özelliği toouse betik eylemleri hello veya kümeniz ile ölçeklendirme işlemleri gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="aad6a-194">Changing hello password breaks hello ability toouse script actions or perform scaling operations with your cluster.</span></span>

### <a name="hosts"></a><span data-ttu-id="aad6a-195">Ana bilgisayarlar</span><span class="sxs-lookup"><span data-stu-id="aad6a-195">Hosts</span></span>

<span data-ttu-id="aad6a-196">Merhaba **ana** sayfası hello kümedeki tüm konaklarda listeler.</span><span class="sxs-lookup"><span data-stu-id="aad6a-196">hello **Hosts** page lists all hosts in hello cluster.</span></span> <span data-ttu-id="aad6a-197">toomanage ana bilgisayarlar, aşağıdaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="aad6a-197">toomanage hosts, follow these steps.</span></span>

![ana sayfa](./media/hdinsight-hadoop-manage-ambari/hosts.png)

> [!NOTE]
> <span data-ttu-id="aad6a-199">Ekleme, yetkisini alma ve bir ana bilgisayar recommissioning Hdınsight kümeleri ile kullanılmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="aad6a-199">Adding, decommissioning, and recommissioning a host should not be used with HDInsight clusters.</span></span>

1. <span data-ttu-id="aad6a-200">Toomanage istediğiniz hello konağı seçin.</span><span class="sxs-lookup"><span data-stu-id="aad6a-200">Select hello host that you wish toomanage.</span></span>

2. <span data-ttu-id="aad6a-201">Kullanım hello **Eylemler** menü tooselect hello eylem tooperform istiyor:</span><span class="sxs-lookup"><span data-stu-id="aad6a-201">Use hello **Actions** menu tooselect hello action that you wish tooperform:</span></span>

   * <span data-ttu-id="aad6a-202">**Tüm bileşenleri başlatın** -hello konakta tüm bileşenleri başlatın.</span><span class="sxs-lookup"><span data-stu-id="aad6a-202">**Start all components** - Start all components on hello host.</span></span>

   * <span data-ttu-id="aad6a-203">**Tüm bileşenleri Durdur** -hello konakta tüm bileşenleri durdurun.</span><span class="sxs-lookup"><span data-stu-id="aad6a-203">**Stop all components** - Stop all components on hello host.</span></span>

   * <span data-ttu-id="aad6a-204">**Tüm bileşenleri yeniden** - Dur ve tüm bileşenleri hello konakta başlatın.</span><span class="sxs-lookup"><span data-stu-id="aad6a-204">**Restart all components** - Stop and start all components on hello host.</span></span>

   * <span data-ttu-id="aad6a-205">**Bakım modunu açmak** -hello ana bilgisayar için uyarıları bastırır.</span><span class="sxs-lookup"><span data-stu-id="aad6a-205">**Turn on maintenance mode** - Suppresses alerts for hello host.</span></span> <span data-ttu-id="aad6a-206">Uyarıları oluşturan eylemleri gerçekleştiriyorsanız Bu mod etkinleştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="aad6a-206">This mode should be enabled if you are performing actions that generate alerts.</span></span> <span data-ttu-id="aad6a-207">Örneğin, bir Hizmeti'ni durdurma ve başlatma.</span><span class="sxs-lookup"><span data-stu-id="aad6a-207">For example, stopping and starting a service.</span></span>

   * <span data-ttu-id="aad6a-208">**Bakım modunu devre dışı bırakmak** -döndürür hello konak toonormal uyarı.</span><span class="sxs-lookup"><span data-stu-id="aad6a-208">**Turn off maintenance mode** - Returns hello host toonormal alerting.</span></span>

   * <span data-ttu-id="aad6a-209">**Durdur** -durakları DataNode veya hello ana bilgisayarda NodeManagers.</span><span class="sxs-lookup"><span data-stu-id="aad6a-209">**Stop** - Stops DataNode or NodeManagers on hello host.</span></span>

   * <span data-ttu-id="aad6a-210">**Başlat** -DataNode başlatır veya hello ana bilgisayarda NodeManagers.</span><span class="sxs-lookup"><span data-stu-id="aad6a-210">**Start** - Starts DataNode or NodeManagers on hello host.</span></span>

   * <span data-ttu-id="aad6a-211">**Yeniden** -durur ve hello ana bilgisayarda DataNode veya NodeManagers başlatır.</span><span class="sxs-lookup"><span data-stu-id="aad6a-211">**Restart** - Stops and starts DataNode or NodeManagers on hello host.</span></span>

   * <span data-ttu-id="aad6a-212">**Yetkisini** -hello kümeden bir ana bilgisayarı kaldırır.</span><span class="sxs-lookup"><span data-stu-id="aad6a-212">**Decommission** - Removes a host from hello cluster.</span></span>

     > [!NOTE]
     > <span data-ttu-id="aad6a-213">Bu eylem, Hdınsight kümelerinde kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="aad6a-213">Do not use this action on HDInsight clusters.</span></span>

   * <span data-ttu-id="aad6a-214">**Recommission** -daha önce yetkisi alınmış konak toohello kümesi ekler.</span><span class="sxs-lookup"><span data-stu-id="aad6a-214">**Recommission** - Adds a previously decommissioned host toohello cluster.</span></span>

     > [!NOTE]
     > <span data-ttu-id="aad6a-215">Bu eylem, Hdınsight kümelerinde kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="aad6a-215">Do not use this action on HDInsight clusters.</span></span>

### <span data-ttu-id="aad6a-216"><a id="service"></a>Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="aad6a-216"><a id="service"></a>Services</span></span>

<span data-ttu-id="aad6a-217">Merhaba gelen **Pano** veya **Hizmetleri** sayfasında, hello kullanın **Eylemler** düğme services toostop hello listesi hello altındaki ve tüm hizmetleri başlatın.</span><span class="sxs-lookup"><span data-stu-id="aad6a-217">From hello **Dashboard** or **Services** page, use hello **Actions** button at hello bottom of hello list of services toostop and start all services.</span></span>

![Hizmet eylemleri](./media/hdinsight-hadoop-manage-ambari/service-actions.png)

> [!WARNING]
> <span data-ttu-id="aad6a-219">Sırada **Hizmet Ekle** listelenen bu menüde, kullanılan tooadd Hizmetleri toohello Hdınsight kümesi olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="aad6a-219">While **Add Service** is listed in this menu, it should not be used tooadd services toohello HDInsight cluster.</span></span> <span data-ttu-id="aad6a-220">Küme hazırlama sırasında bir betik eylemi kullanarak yeni hizmetlerin eklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="aad6a-220">New services should be added using a Script Action during cluster provisioning.</span></span> <span data-ttu-id="aad6a-221">Betik eylemleri kullanma hakkında daha fazla bilgi için bkz: [özelleştirme Hdınsight kümeleri betik eylemleri kullanılarak](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="aad6a-221">For more information on using Script Actions, see [Customize HDInsight clusters using Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

<span data-ttu-id="aad6a-222">Merhaba sırasında **Eylemler** düğmesi tüm hizmetleri yeniden başlatın, genellikle toostart, Dur veya yeniden başlatma belirli bir hizmet istiyor.</span><span class="sxs-lookup"><span data-stu-id="aad6a-222">While hello **Actions** button can restart all services, often you want toostart, stop, or restart a specific service.</span></span> <span data-ttu-id="aad6a-223">Bireysel bir hizmet adımları tooperform eylemleri aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="aad6a-223">Use hello following steps tooperform actions on an individual service:</span></span>

1. <span data-ttu-id="aad6a-224">Merhaba gelen **Pano** veya **Hizmetleri** sayfasında, bir hizmet seçin.</span><span class="sxs-lookup"><span data-stu-id="aad6a-224">From hello **Dashboard** or **Services** page, select a service.</span></span>

2. <span data-ttu-id="aad6a-225">Merhaba, hello üstten **Özet** sekmesinde, hello kullan **hizmet eylemleri** düğmesi ve select hello eylem tootake.</span><span class="sxs-lookup"><span data-stu-id="aad6a-225">From hello top of hello **Summary** tab, use hello **Service Actions** button and select hello action tootake.</span></span> <span data-ttu-id="aad6a-226">Bu, tüm düğümlerde hello hizmetini yeniden başlatır.</span><span class="sxs-lookup"><span data-stu-id="aad6a-226">This restarts hello service on all nodes.</span></span>

    ![hizmet eylemi](./media/hdinsight-hadoop-manage-ambari/individual-service-actions.png)

   > [!NOTE]
   > <span data-ttu-id="aad6a-228">Merhaba küme çalışırken bazı hizmetleri yeniden uyarılar oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="aad6a-228">Restarting some services while hello cluster is running may generate alerts.</span></span> <span data-ttu-id="aad6a-229">tooavoid uyarıları, hello kullanabileceğiniz **hizmet eylemleri** düğmesini tooenable **Bakım modu** hello yeniden başlatma işlemini gerçekleştirmeden önce hello hizmeti.</span><span class="sxs-lookup"><span data-stu-id="aad6a-229">tooavoid alerts, you can use hello **Service Actions** button tooenable **Maintenance mode** for hello service before performing hello restart.</span></span>

3. <span data-ttu-id="aad6a-230">Bir eylem seçildikten sonra hello **# op** arka plan işlemi gerçekleştirildiği hello sayfa artışlarla tooshow hello üstündeki girişi.</span><span class="sxs-lookup"><span data-stu-id="aad6a-230">Once an action has been selected, hello **# op** entry at hello top of hello page increments tooshow that a background operation is occurring.</span></span> <span data-ttu-id="aad6a-231">Toodisplay yapılandırdıysanız, arka plan işlemleri hello listesi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="aad6a-231">If configured toodisplay, hello list of background operations is displayed.</span></span>

   > [!NOTE]
   > <span data-ttu-id="aad6a-232">Etkinleştirmiş olmanız durumunda **Bakım modu** toodisable hello hizmeti için unutmayın hello kullanarak **hizmet eylemleri** hello işlemi tamamlandıktan sonra düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="aad6a-232">If you enabled **Maintenance mode** for hello service, remember toodisable it by using hello **Service Actions** button once hello operation has finished.</span></span>

<span data-ttu-id="aad6a-233">bir hizmet tooconfigure hello aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="aad6a-233">tooconfigure a service, use hello following steps:</span></span>

1. <span data-ttu-id="aad6a-234">Merhaba gelen **Pano** veya **Hizmetleri** sayfasında, bir hizmet seçin.</span><span class="sxs-lookup"><span data-stu-id="aad6a-234">From hello **Dashboard** or **Services** page, select a service.</span></span>

2. <span data-ttu-id="aad6a-235">Select hello **yapılandırmalar** sekmesini hello geçerli yapılandırması görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="aad6a-235">Select hello **Configs** tab. hello current configuration is displayed.</span></span> <span data-ttu-id="aad6a-236">Önceki yapılandırmaların listesi de görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="aad6a-236">A list of previous configurations is also displayed.</span></span>

    ![Yapılandırmaları](./media/hdinsight-hadoop-manage-ambari/service-configs.png)

3. <span data-ttu-id="aad6a-238">Merhaba görüntülenen alanları toomodify hello yapılandırmasını kullanın ve ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="aad6a-238">Use hello fields displayed toomodify hello configuration, and then select **Save**.</span></span> <span data-ttu-id="aad6a-239">Veya önceki bir yapılandırma seçin ve ardından **geçerli hale** tooroll toohello önceki ayarlarını yedekleyin.</span><span class="sxs-lookup"><span data-stu-id="aad6a-239">Or select a previous configuration and then select **Make current** tooroll back toohello previous settings.</span></span>

## <a name="ambari-views"></a><span data-ttu-id="aad6a-240">Ambari görünümleri</span><span class="sxs-lookup"><span data-stu-id="aad6a-240">Ambari views</span></span>

<span data-ttu-id="aad6a-241">Ambari görünümleri tooplug kullanıcı Arabirimi öğeleri geliştiriciler Ambari Web kullanıcı arabirimini hello izin hello kullanarak [Ambari görünümleri Framework](https://cwiki.apache.org/confluence/display/AMBARI/Views).</span><span class="sxs-lookup"><span data-stu-id="aad6a-241">Ambari Views allow developers tooplug UI elements into hello Ambari Web UI using hello [Ambari Views Framework](https://cwiki.apache.org/confluence/display/AMBARI/Views).</span></span> <span data-ttu-id="aad6a-242">Hdınsight Hadoop küme türü görünümlerle aşağıdaki hello sağlar:</span><span class="sxs-lookup"><span data-stu-id="aad6a-242">HDInsight provides hello following views with Hadoop cluster types:</span></span>

* <span data-ttu-id="aad6a-243">Yarn sıra Yöneticisi: hello sıra yöneticisi görüntüleme ve değiştirme YARN sıraları için basit bir kullanıcı Arabirimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="aad6a-243">Yarn Queue Manager: hello queue manager provides a simple UI for viewing and modifying YARN queues.</span></span>

* <span data-ttu-id="aad6a-244">Hive görünümü: hello Hive görünümü toorun Hive sorguları doğrudan web tarayıcınızdan sağlar.</span><span class="sxs-lookup"><span data-stu-id="aad6a-244">Hive View: hello Hive View allows you toorun Hive queries directly from your web browser.</span></span> <span data-ttu-id="aad6a-245">Sorguları Kaydet, sonuçları görüntülemek, toohello küme depolama sonuçları kaydetmek veya sonuçları tooyour yerel sistem indirin.</span><span class="sxs-lookup"><span data-stu-id="aad6a-245">You can save queries, view results, save results toohello cluster storage, or download results tooyour local system.</span></span> <span data-ttu-id="aad6a-246">Hive görünümleri kullanma hakkında daha fazla bilgi için bkz: [Hdınsight ile kullanım Hive görünümleri](hdinsight-hadoop-use-hive-ambari-view.md).</span><span class="sxs-lookup"><span data-stu-id="aad6a-246">For more information on using Hive Views, see [Use Hive Views with HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).</span></span>

* <span data-ttu-id="aad6a-247">Tez görünümü: toobetter sağlar hello Tez görünüm anlamak ve işleri en iyi duruma getirme.</span><span class="sxs-lookup"><span data-stu-id="aad6a-247">Tez View: hello Tez View allows you toobetter understand and optimize jobs.</span></span> <span data-ttu-id="aad6a-248">Tez işlerinde nasıl yürütülür ve hangi kaynaklara kullanılan bilgileri görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aad6a-248">You can view information on how Tez jobs are executed and what resources are used.</span></span>
