---
title: "İzleme ve Azure Hdınsight Ambari Web kullanıcı arabirimini kullanarak yönetme | Microsoft Docs"
description: "Linux tabanlı Hdınsight kümelerini yönetmek ve izlemek için Ambari kullanmayı öğrenin. Bu belgede, Ambari Web kullanıcı arabirimini Hdınsight kümeleri ile dahil kullanmayı öğrenin."
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
ms.openlocfilehash: dc0f9ff030f70985dad0f3b74ba0ee3dda1d9f4b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="manage-hdinsight-clusters-by-using-the-ambari-web-ui"></a><span data-ttu-id="7952e-104">Ambari Web kullanıcı arabirimini kullanarak Hdınsight kümelerini yönetme</span><span class="sxs-lookup"><span data-stu-id="7952e-104">Manage HDInsight clusters by using the Ambari Web UI</span></span>

[!INCLUDE [ambari-selector](../../includes/hdinsight-ambari-selector.md)]

<span data-ttu-id="7952e-105">Apache Ambari, yönetim ve kolay bir web kullanıcı Arabirimi ve REST API kullanmayı sağlayarak Hadoop kümesi izleme basitleştirir.</span><span class="sxs-lookup"><span data-stu-id="7952e-105">Apache Ambari simplifies the management and monitoring of a Hadoop cluster by providing an easy to use web UI and REST API.</span></span> <span data-ttu-id="7952e-106">Ambari, Linux tabanlı Hdınsight kümelerine dahil ve kümeyi izlemek ve yapılandırma değişiklikleri yapmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7952e-106">Ambari is included on Linux-based HDInsight clusters, and is used to monitor the cluster and make configuration changes.</span></span>

<span data-ttu-id="7952e-107">Bu belgede, Ambari Web kullanıcı arabirimini bir Hdınsight kümesini kullanmayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="7952e-107">In this document, you learn how to use the Ambari Web UI with an HDInsight cluster.</span></span>

## <span data-ttu-id="7952e-108"><a id="whatis"></a>Ambari nedir?</span><span class="sxs-lookup"><span data-stu-id="7952e-108"><a id="whatis"></a>What is Ambari?</span></span>

<span data-ttu-id="7952e-109">[Apache Ambari](http://ambari.apache.org) kullanımı kolay web kullanıcı Arabirimi sağlayarak Hadoop yönetimini basitleştirir.</span><span class="sxs-lookup"><span data-stu-id="7952e-109">[Apache Ambari](http://ambari.apache.org) simplifies Hadoop management by providing an easy-to-use web UI.</span></span> <span data-ttu-id="7952e-110">Ambari kullanabileceğiniz oluşturmak, yönetmek ve Hadoop kümelerini izleme.</span><span class="sxs-lookup"><span data-stu-id="7952e-110">You can use Ambari create, manage, and monitor Hadoop clusters.</span></span> <span data-ttu-id="7952e-111">Geliştiriciler tümleştirebilir Bu yetenekler uygulamalarına kullanarak [Ambari REST API'leri](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span><span class="sxs-lookup"><span data-stu-id="7952e-111">Developers can integrate these capabilities into their applications by using the [Ambari REST APIs](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

<span data-ttu-id="7952e-112">Ambari Web kullanıcı Arabirimi, varsayılan olarak Linux işletim sistemini Hdınsight kümeleri ile sağlanır.</span><span class="sxs-lookup"><span data-stu-id="7952e-112">The Ambari Web UI is provided by default with HDInsight clusters that use the Linux operating system.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7952e-113">Linux, HDInsight sürüm 3.4 ve üzerinde kullanılan tek işletim sistemidir.</span><span class="sxs-lookup"><span data-stu-id="7952e-113">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="7952e-114">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="7952e-114">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> 

## <a name="connectivity"></a><span data-ttu-id="7952e-115">Bağlantı</span><span class="sxs-lookup"><span data-stu-id="7952e-115">Connectivity</span></span>

<span data-ttu-id="7952e-116">Ambari Web kullanıcı arabirimini HTTPS://CLUSTERNAME.azurehdidnsight.net, konumunda Hdınsight kümenize kullanılabilir olduğu **CLUSTERNAME** kümenizin adıdır.</span><span class="sxs-lookup"><span data-stu-id="7952e-116">The Ambari Web UI is available on your HDInsight cluster at HTTPS://CLUSTERNAME.azurehdidnsight.net, where **CLUSTERNAME** is the name of your cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7952e-117">Hdınsight üzerinde Ambari bağlanma HTTPS gerektirir.</span><span class="sxs-lookup"><span data-stu-id="7952e-117">Connecting to Ambari on HDInsight requires HTTPS.</span></span> <span data-ttu-id="7952e-118">Kimlik doğrulaması için istendiğinde, Yönetici hesap adı ve küme oluştururken verdiğiniz parolası'nı kullanın.</span><span class="sxs-lookup"><span data-stu-id="7952e-118">When prompted for authentication, use the admin account name and password you provided when the cluster was created.</span></span>

## <a name="ssh-tunnel-proxy"></a><span data-ttu-id="7952e-119">SSH tüneli (proxy)</span><span class="sxs-lookup"><span data-stu-id="7952e-119">SSH tunnel (proxy)</span></span>

<span data-ttu-id="7952e-120">Kümeniz için Ambari doğrudan Internet üzerinden erişilebilir olsa da, bazı bağlantılar Ambari Web kullanıcı arabirimini (Jobtracker'a gibi) internet'te sunulmaz.</span><span class="sxs-lookup"><span data-stu-id="7952e-120">While Ambari for your cluster is accessible directly over the Internet, some links from the Ambari Web UI (such as to the JobTracker) are not exposed on the internet.</span></span> <span data-ttu-id="7952e-121">Bu hizmetlere erişmek için bir SSH tüneli oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7952e-121">To access these services, you must create an SSH tunnel.</span></span> <span data-ttu-id="7952e-122">Daha fazla bilgi için bkz: [kullanım SSH tünel Hdınsight ile](hdinsight-linux-ambari-ssh-tunnel.md).</span><span class="sxs-lookup"><span data-stu-id="7952e-122">For more information, see [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md).</span></span>

## <a name="ambari-web-ui"></a><span data-ttu-id="7952e-123">Ambari Web kullanıcı Arabirimi</span><span class="sxs-lookup"><span data-stu-id="7952e-123">Ambari Web UI</span></span>

<span data-ttu-id="7952e-124">Ambari Web kullanıcı Arabirimi için bağlanırken sayfasına kimlik doğrulaması yapmak istenir.</span><span class="sxs-lookup"><span data-stu-id="7952e-124">When connecting to the Ambari Web UI, you are prompted to authenticate to the page.</span></span> <span data-ttu-id="7952e-125">Küme oluşturma sırasında kullanılan parola ve küme yönetici kullanıcı (varsayılan Yönetici) kullanın.</span><span class="sxs-lookup"><span data-stu-id="7952e-125">Use the cluster admin user (default Admin) and password you used during cluster creation.</span></span>

<span data-ttu-id="7952e-126">Sayfayı açtığında çubuğunun üstündeki unutmayın.</span><span class="sxs-lookup"><span data-stu-id="7952e-126">When the page opens, note the bar at the top.</span></span> <span data-ttu-id="7952e-127">Bu çubuğu, aşağıdaki bilgileri ve denetimleri içerir:</span><span class="sxs-lookup"><span data-stu-id="7952e-127">This bar contains the following information and controls:</span></span>

![ambari nav](./media/hdinsight-hadoop-manage-ambari/ambari-nav.png)

* <span data-ttu-id="7952e-129">**Ambari logosu** -küme izlemek için kullanılan Pano açar.</span><span class="sxs-lookup"><span data-stu-id="7952e-129">**Ambari logo** - Opens the dashboard, which can be used to monitor the cluster.</span></span>

* <span data-ttu-id="7952e-130">**Küme adı # ops** -devam eden ambarı işlemler sayısını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="7952e-130">**Cluster name # ops** - Displays the number of ongoing Ambari operations.</span></span> <span data-ttu-id="7952e-131">Küme adı seçerek veya **# ops** arka plan işlemleri listesini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="7952e-131">Selecting the cluster name or **# ops** displays a list of background operations.</span></span>

* <span data-ttu-id="7952e-132">**# Uyarıları** -görüntüler uyarı veya kritik uyarılar, küme.</span><span class="sxs-lookup"><span data-stu-id="7952e-132">**# alerts** - Displays warnings or critical alerts, if any, for the cluster.</span></span>

* <span data-ttu-id="7952e-133">**Pano** -Pano görüntüler.</span><span class="sxs-lookup"><span data-stu-id="7952e-133">**Dashboard** - Displays the dashboard.</span></span>

* <span data-ttu-id="7952e-134">**Hizmetleri** -kümedeki hizmetleri için bilgi ve yapılandırma ayarları.</span><span class="sxs-lookup"><span data-stu-id="7952e-134">**Services** - Information and configuration settings for the services in the cluster.</span></span>

* <span data-ttu-id="7952e-135">**Ana bilgisayar** -kümedeki düğümler için bilgileri ve yapılandırma ayarları.</span><span class="sxs-lookup"><span data-stu-id="7952e-135">**Hosts** - Information and configuration settings for the nodes in the cluster.</span></span>

* <span data-ttu-id="7952e-136">**Uyarıları** -günlük bilgi, uyarı ve kritik uyarılar.</span><span class="sxs-lookup"><span data-stu-id="7952e-136">**Alerts** - A log of information, warnings, and critical alerts.</span></span>

* <span data-ttu-id="7952e-137">**Yönetici** -küme, hizmet hesabı bilgilerini ve Kerberos güvenlik yüklü yazılım yığını/Hizmetleri.</span><span class="sxs-lookup"><span data-stu-id="7952e-137">**Admin** - Software stack/services that are installed on the cluster, service account information, and Kerberos security.</span></span>

* <span data-ttu-id="7952e-138">**Yönetici düğmesi** -ambarı yönetimi, kullanıcı ayarlarını ve oturum kapatma.</span><span class="sxs-lookup"><span data-stu-id="7952e-138">**Admin button** - Ambari management, user settings, and logout.</span></span>

## <a name="monitoring"></a><span data-ttu-id="7952e-139">İzleme</span><span class="sxs-lookup"><span data-stu-id="7952e-139">Monitoring</span></span>

### <a name="alerts"></a><span data-ttu-id="7952e-140">Uyarılar</span><span class="sxs-lookup"><span data-stu-id="7952e-140">Alerts</span></span>

<span data-ttu-id="7952e-141">Aşağıdaki liste, Ambari tarafından kullanılan ortak uyarı durumlarını içerir:</span><span class="sxs-lookup"><span data-stu-id="7952e-141">The following list contains the common alert statuses used by Ambari:</span></span>

* <span data-ttu-id="7952e-142">**TAMAM**</span><span class="sxs-lookup"><span data-stu-id="7952e-142">**OK**</span></span>
* <span data-ttu-id="7952e-143">**Uyarı**</span><span class="sxs-lookup"><span data-stu-id="7952e-143">**Warning**</span></span>
* <span data-ttu-id="7952e-144">**KRİTİK**</span><span class="sxs-lookup"><span data-stu-id="7952e-144">**CRITICAL**</span></span>
* <span data-ttu-id="7952e-145">**BİLİNMEYEN**</span><span class="sxs-lookup"><span data-stu-id="7952e-145">**UNKNOWN**</span></span>

<span data-ttu-id="7952e-146">Dışındaki uyarıları **Tamam** neden **# uyarıları** uyarı sayısını görüntülemek için sayfanın üstündeki girişi.</span><span class="sxs-lookup"><span data-stu-id="7952e-146">Alerts other than **OK** cause the **# alerts** entry at the top of the page to display the number of alerts.</span></span> <span data-ttu-id="7952e-147">Bu girişi seçerseniz, uyarıları ve bunların durumunu görüntüler.</span><span class="sxs-lookup"><span data-stu-id="7952e-147">Selecting this entry displays the alerts and their status.</span></span>

<span data-ttu-id="7952e-148">Uyarıları görüntülenebilir birkaç varsayılan gruplar halinde düzenlenir **uyarıları** sayfası.</span><span class="sxs-lookup"><span data-stu-id="7952e-148">Alerts are organized into several default groups, which can be viewed from the **Alerts** page.</span></span>

![Uyarılar sayfası](./media/hdinsight-hadoop-manage-ambari/alerts.png)

<span data-ttu-id="7952e-150">Grupları kullanarak yönetebileceğiniz **Eylemler** menü ve seçerek **uyarı grupları yönet**.</span><span class="sxs-lookup"><span data-stu-id="7952e-150">You can manage the groups by using the **Actions** menu and selecting **Manage Alert Groups**.</span></span>

![Uyarı gruplar iletişim yönetme](./media/hdinsight-hadoop-manage-ambari/manage-alerts.png)

<span data-ttu-id="7952e-152">Ayrıca, uyarı yöntemleri yönetmek ve uyarı bildirimleri oluşturma **Eylemler** seçerek menü __yönetmek uyarı bildirimleri__.</span><span class="sxs-lookup"><span data-stu-id="7952e-152">You can also manage alerting methods, and create alert notifications from the **Actions** menu by selecting __Manage Alert Notifications__.</span></span> <span data-ttu-id="7952e-153">Geçerli herhangi bir bildirim görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="7952e-153">Any current notifications are displayed.</span></span> <span data-ttu-id="7952e-154">Ayrıca, buradan bildirimler de oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7952e-154">You can also create notifications from here.</span></span> <span data-ttu-id="7952e-155">Bildirimler, üzerinden gönderilebilir **e-posta** veya **SNMP** belirli uyarı önem birleşimleri olduğunda.</span><span class="sxs-lookup"><span data-stu-id="7952e-155">Notifications can be sent via **EMAIL** or **SNMP** when specific alert/severity combinations occur.</span></span> <span data-ttu-id="7952e-156">Örneğin, bir e-posta uyarıları biri gönderebilirsiniz **YARN varsayılan** Grup ayarlanmış **kritik**.</span><span class="sxs-lookup"><span data-stu-id="7952e-156">For example, you can send an email message when any of the alerts in the **YARN Default** group is set to **Critical**.</span></span>

![Uyarı iletişim kutusu oluşturma](./media/hdinsight-hadoop-manage-ambari/create-alert-notification.png)

<span data-ttu-id="7952e-158">Son olarak, seçme __uyarı ayarlarını Yönet__ gelen __Eylemler__ menüsü bir bildirim gönderilmeden önce bir uyarı ortaya gerekir sayısı ayarlamanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="7952e-158">Finally, selecting __Manage Alert Settings__ from the __Actions__ menu allows you to set the number of times an alert must occur before a notification is sent.</span></span> <span data-ttu-id="7952e-159">Bu ayar, bildirimleri geçici hataları önlemek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="7952e-159">This setting can be used to prevent notifications for transient errors.</span></span>

### <a name="cluster"></a><span data-ttu-id="7952e-160">Küme</span><span class="sxs-lookup"><span data-stu-id="7952e-160">Cluster</span></span>

<span data-ttu-id="7952e-161">**Ölçümleri** Pano sekmesi kolaylaştıran bir bakışta, küme durumunu izlemek pencere öğeleri, bir dizi içerir.</span><span class="sxs-lookup"><span data-stu-id="7952e-161">The **Metrics** tab of the dashboard contains a series of widgets that make it easy to monitor the status of your cluster at a glance.</span></span> <span data-ttu-id="7952e-162">Birkaç pencere öğeleri gibi **CPU kullanımı**, tıklatıldığında ek bilgileri sağlayın.</span><span class="sxs-lookup"><span data-stu-id="7952e-162">Several widgets, such as **CPU Usage**, provide additional information when clicked.</span></span>

![Pano ölçümlerle](./media/hdinsight-hadoop-manage-ambari/metrics.png)

<span data-ttu-id="7952e-164">**Heatmaps** sekmesi ölçümleri yeşilden kırmızı giderek renkli heatmaps olarak görüntüler.</span><span class="sxs-lookup"><span data-stu-id="7952e-164">The **Heatmaps** tab displays metrics as colored heatmaps, going from green to red.</span></span>

![Pano heatmaps ile](./media/hdinsight-hadoop-manage-ambari/heatmap.png)

<span data-ttu-id="7952e-166">Küme içindeki düğümler üzerinde daha fazla bilgi için seçin **ana**.</span><span class="sxs-lookup"><span data-stu-id="7952e-166">For more information on the nodes within the cluster, select **Hosts**.</span></span> <span data-ttu-id="7952e-167">Daha sonra ilgilendiğiniz belirli düğümünü seçin.</span><span class="sxs-lookup"><span data-stu-id="7952e-167">Then select the specific node you are interested in.</span></span>

![ana bilgisayar ayrıntıları](./media/hdinsight-hadoop-manage-ambari/host-details.png)

### <a name="services"></a><span data-ttu-id="7952e-169">Hizmetler</span><span class="sxs-lookup"><span data-stu-id="7952e-169">Services</span></span>

<span data-ttu-id="7952e-170">**Hizmetleri** kenar Panoda küme üzerinde çalışan hizmetleri durumunu hızlı fikir sağlar.</span><span class="sxs-lookup"><span data-stu-id="7952e-170">The **Services** sidebar on the dashboard provides quick insight into the status of the services running on the cluster.</span></span> <span data-ttu-id="7952e-171">Çeşitli simgeleri durumu veya alınması gereken eylemleri belirtmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7952e-171">Various icons are used to indicate status or actions that should be taken.</span></span> <span data-ttu-id="7952e-172">Örneğin, bir hizmet geri dönüştürülmesi gerekiyorsa sarı geri dönüşüm simgesi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="7952e-172">For example, a yellow recycle symbol is displayed if a service needs to be recycled.</span></span>

![Hizmetleri yan çubuğu](./media/hdinsight-hadoop-manage-ambari/service-bar.png)

> [!NOTE]
> <span data-ttu-id="7952e-174">Görüntülenen hizmetler Hdınsight küme türleri ve sürümleri arasında farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="7952e-174">The services displayed differ between HDInsight cluster types and versions.</span></span> <span data-ttu-id="7952e-175">Burada görüntülenen hizmetler, kümeniz için görüntülenen hizmetler farklı olabilir.</span><span class="sxs-lookup"><span data-stu-id="7952e-175">The services displayed here may be different than the services displayed for your cluster.</span></span>

<span data-ttu-id="7952e-176">Bir hizmet seçmeden hizmette daha ayrıntılı bilgiler görüntüler.</span><span class="sxs-lookup"><span data-stu-id="7952e-176">Selecting a service displays more detailed information on the service.</span></span>

![Hizmet özet bilgileri](./media/hdinsight-hadoop-manage-ambari/service-details.png)

#### <a name="quick-links"></a><span data-ttu-id="7952e-178">Hızlı bağlantılar</span><span class="sxs-lookup"><span data-stu-id="7952e-178">Quick links</span></span>

<span data-ttu-id="7952e-179">Bazı Hizmetleri görünen bir **hızlı bağlantılar** sayfanın üst kısmındaki bağlantı.</span><span class="sxs-lookup"><span data-stu-id="7952e-179">Some services display a **Quick Links** link at the top of the page.</span></span> <span data-ttu-id="7952e-180">Bu hizmete özgü web Uı'lar, gibi erişmek için kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="7952e-180">This can be used to access service-specific web UIs, such as:</span></span>

* <span data-ttu-id="7952e-181">**İş Geçmişi** -MapReduce iş geçmişi.</span><span class="sxs-lookup"><span data-stu-id="7952e-181">**Job History** - MapReduce job history.</span></span>
* <span data-ttu-id="7952e-182">**Resource Manager** -YARN ResourceManager UI.</span><span class="sxs-lookup"><span data-stu-id="7952e-182">**Resource Manager** - YARN ResourceManager UI.</span></span>
* <span data-ttu-id="7952e-183">**İş** -Hadoop dağıtılmış dosya sistemi (HDFS) iş UI.</span><span class="sxs-lookup"><span data-stu-id="7952e-183">**NameNode** - Hadoop Distributed File System (HDFS) NameNode UI.</span></span>
* <span data-ttu-id="7952e-184">**Oozie Web kullanıcı Arabirimi** -Oozie UI.</span><span class="sxs-lookup"><span data-stu-id="7952e-184">**Oozie Web UI** - Oozie UI.</span></span>

<span data-ttu-id="7952e-185">Aşağıdaki bağlantılardan birini seçerek yeni bir sekmede seçilen sayfasını görüntüler, tarayıcınızda açılır.</span><span class="sxs-lookup"><span data-stu-id="7952e-185">Selecting any of these links opens a new tab in your browser, which displays the selected page.</span></span>

> [!NOTE]
> <span data-ttu-id="7952e-186">Seçme **hızlı bağlantılar** girişi bir hizmet için "Sunucu bulunamadı" hata döndürebilir.</span><span class="sxs-lookup"><span data-stu-id="7952e-186">Selecting the **Quick Links** entry for a service may return a "server not found" error.</span></span> <span data-ttu-id="7952e-187">Bu hatayla karşılaşırsanız, kullanırken SSH tüneli kullanmalısınız **hızlı bağlantılar** bu hizmet için girişi.</span><span class="sxs-lookup"><span data-stu-id="7952e-187">If you encounter this error, you must use an SSH tunnel when using the **Quick Links** entry for this service.</span></span> <span data-ttu-id="7952e-188">Bilgi için bkz: [kullanım SSH tünel Hdınsight ile](hdinsight-linux-ambari-ssh-tunnel.md)</span><span class="sxs-lookup"><span data-stu-id="7952e-188">For information, see [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md)</span></span>

## <a name="management"></a><span data-ttu-id="7952e-189">Yönetim</span><span class="sxs-lookup"><span data-stu-id="7952e-189">Management</span></span>

### <a name="ambari-users-groups-and-permissions"></a><span data-ttu-id="7952e-190">Ambari kullanıcılar, gruplar ve izinler</span><span class="sxs-lookup"><span data-stu-id="7952e-190">Ambari users, groups, and permissions</span></span>

<span data-ttu-id="7952e-191">Kullanıcılar, gruplar ve izinler ile çalışma kullanılırken desteklenir bir [etki alanına katılmış](hdinsight-domain-joined-introduction.md) Hdınsight kümesi.</span><span class="sxs-lookup"><span data-stu-id="7952e-191">Working with users, groups, and permissions are supported when using a [domain joined](hdinsight-domain-joined-introduction.md) HDInsight cluster.</span></span> <span data-ttu-id="7952e-192">Etki alanına katılmış bir kümede ambarı Yönetimi kullanıcı arabirimini kullanma hakkında daha fazla bilgi için bkz: [etki alanına katılmış Hdınsight kümelerini yönetme](hdinsight-domain-joined-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7952e-192">For information on using the Ambari Management UI on a domain-joined cluster, see [Manage domain-joined HDInsight clusters](hdinsight-domain-joined-introduction.md).</span></span>

> [!WARNING]
> <span data-ttu-id="7952e-193">Linux tabanlı Hdınsight kümenizdeki Ambari izleme (hdinsightwatchdog) parolasını değiştirmeyin.</span><span class="sxs-lookup"><span data-stu-id="7952e-193">Do not change the password of the Ambari watchdog (hdinsightwatchdog) on your Linux-based HDInsight cluster.</span></span> <span data-ttu-id="7952e-194">Parola değiştirme betik eylemleri kullanın veya kümeniz ile ölçeklendirme işlemleri olanağı keser.</span><span class="sxs-lookup"><span data-stu-id="7952e-194">Changing the password breaks the ability to use script actions or perform scaling operations with your cluster.</span></span>

### <a name="hosts"></a><span data-ttu-id="7952e-195">Ana bilgisayarlar</span><span class="sxs-lookup"><span data-stu-id="7952e-195">Hosts</span></span>

<span data-ttu-id="7952e-196">**Ana** sayfası, kümedeki tüm konaklarda listeler.</span><span class="sxs-lookup"><span data-stu-id="7952e-196">The **Hosts** page lists all hosts in the cluster.</span></span> <span data-ttu-id="7952e-197">Ana bilgisayarları yönetmek için aşağıdaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="7952e-197">To manage hosts, follow these steps.</span></span>

![ana sayfa](./media/hdinsight-hadoop-manage-ambari/hosts.png)

> [!NOTE]
> <span data-ttu-id="7952e-199">Ekleme, yetkisini alma ve bir ana bilgisayar recommissioning Hdınsight kümeleri ile kullanılmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="7952e-199">Adding, decommissioning, and recommissioning a host should not be used with HDInsight clusters.</span></span>

1. <span data-ttu-id="7952e-200">Yönetmek istediğiniz konağı seçin.</span><span class="sxs-lookup"><span data-stu-id="7952e-200">Select the host that you wish to manage.</span></span>

2. <span data-ttu-id="7952e-201">Kullanım **Eylemler** menü gerçekleştirmek istediğiniz eylemi seçin:</span><span class="sxs-lookup"><span data-stu-id="7952e-201">Use the **Actions** menu to select the action that you wish to perform:</span></span>

   * <span data-ttu-id="7952e-202">**Tüm bileşenleri başlatın** -konakta tüm bileşenleri başlatın.</span><span class="sxs-lookup"><span data-stu-id="7952e-202">**Start all components** - Start all components on the host.</span></span>

   * <span data-ttu-id="7952e-203">**Tüm bileşenleri Durdur** -konakta tüm bileşenleri durdurun.</span><span class="sxs-lookup"><span data-stu-id="7952e-203">**Stop all components** - Stop all components on the host.</span></span>

   * <span data-ttu-id="7952e-204">**Tüm bileşenleri yeniden** - Dur ve tüm bileşenleri konakta başlatın.</span><span class="sxs-lookup"><span data-stu-id="7952e-204">**Restart all components** - Stop and start all components on the host.</span></span>

   * <span data-ttu-id="7952e-205">**Bakım modunu açmak** -ana bilgisayar için uyarıları bastırır.</span><span class="sxs-lookup"><span data-stu-id="7952e-205">**Turn on maintenance mode** - Suppresses alerts for the host.</span></span> <span data-ttu-id="7952e-206">Uyarıları oluşturan eylemleri gerçekleştiriyorsanız Bu mod etkinleştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="7952e-206">This mode should be enabled if you are performing actions that generate alerts.</span></span> <span data-ttu-id="7952e-207">Örneğin, bir Hizmeti'ni durdurma ve başlatma.</span><span class="sxs-lookup"><span data-stu-id="7952e-207">For example, stopping and starting a service.</span></span>

   * <span data-ttu-id="7952e-208">**Bakım modunu devre dışı bırakmak** -normal uyarmak için ana döndürür.</span><span class="sxs-lookup"><span data-stu-id="7952e-208">**Turn off maintenance mode** - Returns the host to normal alerting.</span></span>

   * <span data-ttu-id="7952e-209">**Durdur** -durakları DataNode veya ana bilgisayarda NodeManagers.</span><span class="sxs-lookup"><span data-stu-id="7952e-209">**Stop** - Stops DataNode or NodeManagers on the host.</span></span>

   * <span data-ttu-id="7952e-210">**Başlat** -DataNode başlatır veya ana bilgisayarda NodeManagers.</span><span class="sxs-lookup"><span data-stu-id="7952e-210">**Start** - Starts DataNode or NodeManagers on the host.</span></span>

   * <span data-ttu-id="7952e-211">**Yeniden** -durur ve ana bilgisayarda DataNode veya NodeManagers başlatır.</span><span class="sxs-lookup"><span data-stu-id="7952e-211">**Restart** - Stops and starts DataNode or NodeManagers on the host.</span></span>

   * <span data-ttu-id="7952e-212">**Yetkisini** -kümeden bir ana bilgisayarı kaldırır.</span><span class="sxs-lookup"><span data-stu-id="7952e-212">**Decommission** - Removes a host from the cluster.</span></span>

     > [!NOTE]
     > <span data-ttu-id="7952e-213">Bu eylem, Hdınsight kümelerinde kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="7952e-213">Do not use this action on HDInsight clusters.</span></span>

   * <span data-ttu-id="7952e-214">**Recommission** -önceden yetkisi alınmış bir konak kümesine ekler.</span><span class="sxs-lookup"><span data-stu-id="7952e-214">**Recommission** - Adds a previously decommissioned host to the cluster.</span></span>

     > [!NOTE]
     > <span data-ttu-id="7952e-215">Bu eylem, Hdınsight kümelerinde kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="7952e-215">Do not use this action on HDInsight clusters.</span></span>

### <span data-ttu-id="7952e-216"><a id="service"></a>Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="7952e-216"><a id="service"></a>Services</span></span>

<span data-ttu-id="7952e-217">Gelen **Pano** veya **Hizmetleri** sayfasında, kullanmak **Eylemler** tüm hizmetlerini durdurmak ve başlatmak için hizmetler listesinin altındaki düğmesini.</span><span class="sxs-lookup"><span data-stu-id="7952e-217">From the **Dashboard** or **Services** page, use the **Actions** button at the bottom of the list of services to stop and start all services.</span></span>

![Hizmet eylemleri](./media/hdinsight-hadoop-manage-ambari/service-actions.png)

> [!WARNING]
> <span data-ttu-id="7952e-219">Sırada **Hizmet Ekle** listelenen bu menüde, bu hizmetleri Hdınsight kümesine eklemek için kullanılmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="7952e-219">While **Add Service** is listed in this menu, it should not be used to add services to the HDInsight cluster.</span></span> <span data-ttu-id="7952e-220">Küme hazırlama sırasında bir betik eylemi kullanarak yeni hizmetlerin eklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="7952e-220">New services should be added using a Script Action during cluster provisioning.</span></span> <span data-ttu-id="7952e-221">Betik eylemleri kullanma hakkında daha fazla bilgi için bkz: [özelleştirme Hdınsight kümeleri betik eylemleri kullanılarak](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="7952e-221">For more information on using Script Actions, see [Customize HDInsight clusters using Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

<span data-ttu-id="7952e-222">Sırada **Eylemler** düğmesi tüm hizmetleri yeniden başlatın, başlatma, durdurma veya belirli bir hizmeti yeniden başlatmak istediğiniz sıklığı.</span><span class="sxs-lookup"><span data-stu-id="7952e-222">While the **Actions** button can restart all services, often you want to start, stop, or restart a specific service.</span></span> <span data-ttu-id="7952e-223">Bireysel bir hizmet eylemleri gerçekleştirmek için aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="7952e-223">Use the following steps to perform actions on an individual service:</span></span>

1. <span data-ttu-id="7952e-224">Gelen **Pano** veya **Hizmetleri** sayfasında, bir hizmet seçin.</span><span class="sxs-lookup"><span data-stu-id="7952e-224">From the **Dashboard** or **Services** page, select a service.</span></span>

2. <span data-ttu-id="7952e-225">Üstünden **Özet** sekmesinde, kullanmak **hizmet eylemleri** düğmesini tıklatın ve gerçekleştirilecek eylemi seçin.</span><span class="sxs-lookup"><span data-stu-id="7952e-225">From the top of the **Summary** tab, use the **Service Actions** button and select the action to take.</span></span> <span data-ttu-id="7952e-226">Bu, tüm düğümlerde hizmetini yeniden başlatır.</span><span class="sxs-lookup"><span data-stu-id="7952e-226">This restarts the service on all nodes.</span></span>

    ![hizmet eylemi](./media/hdinsight-hadoop-manage-ambari/individual-service-actions.png)

   > [!NOTE]
   > <span data-ttu-id="7952e-228">Küme çalışırken bazı hizmetleri yeniden uyarılar oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="7952e-228">Restarting some services while the cluster is running may generate alerts.</span></span> <span data-ttu-id="7952e-229">Uyarıları önlemek için kullanabileceğiniz **hizmet eylemleri** etkinleştirmek için düğmeyi **Bakım modu** yeniden gerçekleştirmeden önce hizmeti.</span><span class="sxs-lookup"><span data-stu-id="7952e-229">To avoid alerts, you can use the **Service Actions** button to enable **Maintenance mode** for the service before performing the restart.</span></span>

3. <span data-ttu-id="7952e-230">Bir eylem seçildikten sonra **# op** arka plan işlemi gerçekleşmekte olduğunu göstermek için sayfa artışlarla üstündeki girişi.</span><span class="sxs-lookup"><span data-stu-id="7952e-230">Once an action has been selected, the **# op** entry at the top of the page increments to show that a background operation is occurring.</span></span> <span data-ttu-id="7952e-231">Görüntüleyecek şekilde yapılandırılmış olsa arka plan işlemleri listesi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="7952e-231">If configured to display, the list of background operations is displayed.</span></span>

   > [!NOTE]
   > <span data-ttu-id="7952e-232">Etkinleştirmiş olmanız durumunda **Bakım modu** kullanarak devre dışı bırakmak hizmet için unutmayın **hizmet eylemleri** işlemi tamamlandıktan sonra düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7952e-232">If you enabled **Maintenance mode** for the service, remember to disable it by using the **Service Actions** button once the operation has finished.</span></span>

<span data-ttu-id="7952e-233">Bir hizmeti yapılandırmak için aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="7952e-233">To configure a service, use the following steps:</span></span>

1. <span data-ttu-id="7952e-234">Gelen **Pano** veya **Hizmetleri** sayfasında, bir hizmet seçin.</span><span class="sxs-lookup"><span data-stu-id="7952e-234">From the **Dashboard** or **Services** page, select a service.</span></span>

2. <span data-ttu-id="7952e-235">Seçin **yapılandırmalar** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="7952e-235">Select the **Configs** tab.</span></span> <span data-ttu-id="7952e-236">Geçerli yapılandırması görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="7952e-236">The current configuration is displayed.</span></span> <span data-ttu-id="7952e-237">Önceki yapılandırmaların listesi de görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="7952e-237">A list of previous configurations is also displayed.</span></span>

    ![Yapılandırmaları](./media/hdinsight-hadoop-manage-ambari/service-configs.png)

3. <span data-ttu-id="7952e-239">Yapılandırmasını değiştirin ve ardından görüntülenen alanları kullanın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="7952e-239">Use the fields displayed to modify the configuration, and then select **Save**.</span></span> <span data-ttu-id="7952e-240">Veya önceki bir yapılandırma seçin ve ardından **geçerli hale** önceki ayarlarına geri almak için.</span><span class="sxs-lookup"><span data-stu-id="7952e-240">Or select a previous configuration and then select **Make current** to roll back to the previous settings.</span></span>

## <a name="ambari-views"></a><span data-ttu-id="7952e-241">Ambari görünümleri</span><span class="sxs-lookup"><span data-stu-id="7952e-241">Ambari views</span></span>

<span data-ttu-id="7952e-242">Ambari görünümleri izin Ambari Web kullanıcı arabirimini kullanarak kullanıcı Arabirimi öğeleri takın geliştiricilerin [Ambari görünümleri Framework](https://cwiki.apache.org/confluence/display/AMBARI/Views).</span><span class="sxs-lookup"><span data-stu-id="7952e-242">Ambari Views allow developers to plug UI elements into the Ambari Web UI using the [Ambari Views Framework](https://cwiki.apache.org/confluence/display/AMBARI/Views).</span></span> <span data-ttu-id="7952e-243">Hdınsight Hadoop küme türü ile aşağıdaki görünümleri sağlar:</span><span class="sxs-lookup"><span data-stu-id="7952e-243">HDInsight provides the following views with Hadoop cluster types:</span></span>

* <span data-ttu-id="7952e-244">Yarn sıra Yöneticisi: sıra yöneticisini görüntüleme ve değiştirme YARN sıralar için basit bir kullanıcı Arabirimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="7952e-244">Yarn Queue Manager: The queue manager provides a simple UI for viewing and modifying YARN queues.</span></span>

* <span data-ttu-id="7952e-245">Hive görünümü: Hive görünümü doğrudan web tarayıcınızdan Hive sorguları çalıştırmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="7952e-245">Hive View: The Hive View allows you to run Hive queries directly from your web browser.</span></span> <span data-ttu-id="7952e-246">Sorguları Kaydet, sonuçları görüntülemek, küme depolama alanına sonuçları kaydetmek veya sonuçları yerel sisteminize indirin.</span><span class="sxs-lookup"><span data-stu-id="7952e-246">You can save queries, view results, save results to the cluster storage, or download results to your local system.</span></span> <span data-ttu-id="7952e-247">Hive görünümleri kullanma hakkında daha fazla bilgi için bkz: [Hdınsight ile kullanım Hive görünümleri](hdinsight-hadoop-use-hive-ambari-view.md).</span><span class="sxs-lookup"><span data-stu-id="7952e-247">For more information on using Hive Views, see [Use Hive Views with HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).</span></span>

* <span data-ttu-id="7952e-248">Tez görünümü: Tez View daha iyi anlamak ve işleri en iyi duruma getirmek sağlar.</span><span class="sxs-lookup"><span data-stu-id="7952e-248">Tez View: The Tez View allows you to better understand and optimize jobs.</span></span> <span data-ttu-id="7952e-249">Tez işlerinde nasıl yürütülür ve hangi kaynaklara kullanılan bilgileri görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7952e-249">You can view information on how Tez jobs are executed and what resources are used.</span></span>
