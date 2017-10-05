---
title: "Etki alanına katılmış Hdınsight kümelerini - Azure yönetme | Microsoft Docs"
description: "Etki alanına katılmış Hdınsight kümeleri yönetmeyi öğrenin"
services: hdinsight
documentationcenter: 
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: 6ebc4d2f-2f6a-4e1e-ab6d-af4db6b4c87c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 10/25/2016
ms.author: saurinsh
ms.openlocfilehash: 9b56ce6cc5bdd3b8d48d047751e978cad08598e1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-domain-joined-hdinsight-clusters-preview"></a><span data-ttu-id="c6437-103">Etki alanına katılmış Hdınsight kümeleri (Önizleme) yönetme</span><span class="sxs-lookup"><span data-stu-id="c6437-103">Manage Domain-joined HDInsight clusters (Preview)</span></span>
<span data-ttu-id="c6437-104">Kullanıcılar ve roller etki alanına katılmış ve etki alanına katılmış Hdınsight kümelerini yönetme konusunda bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="c6437-104">Learn the users and the roles in Domain-joined HDInsight, and how to manage domain-joined HDInsight clusters.</span></span>

## <a name="users-of-domain-joined-hdinsight-clusters"></a><span data-ttu-id="c6437-105">Kullanıcıları etki alanına katılmış Hdınsight kümeleri</span><span class="sxs-lookup"><span data-stu-id="c6437-105">Users of Domain-joined HDInsight clusters</span></span>
<span data-ttu-id="c6437-106">Küme oluşturma sırasında oluşturulan iki kullanıcı hesapları olmayan etki alanına katılmış bir Hdınsight kümesi vardır:</span><span class="sxs-lookup"><span data-stu-id="c6437-106">An HDInsight cluster that is not domain-joined has two user accounts that are created during the cluster creation:</span></span>

* <span data-ttu-id="c6437-107">**Ambari yönetici**: Bu hesap olarak da bilinen, *Hadoop kullanıcı* veya *HTTP kullanıcı*.</span><span class="sxs-lookup"><span data-stu-id="c6437-107">**Ambari admin**: This account is also known as *Hadoop user* or *HTTP user*.</span></span> <span data-ttu-id="c6437-108">Bu hesap için Ambari https:// sırasında oturum açmak için kullanılan&lt;clustername >. azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="c6437-108">This account can be used to log on to Ambari at https://&lt;clustername>.azurehdinsight.net.</span></span> <span data-ttu-id="c6437-109">Ayrıca, Ambari görünümleri sorguları çalıştırmak için harici araçlar (yani PowerShell, Templeton, Visual Studio) aracılığıyla işleri çalıştırıp BI Araçları (yani Excel, Powerbı veya Tableau) ve Hive ODBC sürücüsü ile kimlik doğrulaması için de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="c6437-109">It can also be used to run queries on Ambari views, execute jobs via external tools (i.e. PowerShell, Templeton, Visual Studio), and authenticate with the Hive ODBC driver and BI tools (i.e. Excel, PowerBI, or Tableau).</span></span>
* <span data-ttu-id="c6437-110">**SSH kullanıcı**: Bu hesap ile SSH kullanılabilir ve sudo komutları yürütün.</span><span class="sxs-lookup"><span data-stu-id="c6437-110">**SSH user**:  This account can be used with SSH, and execute sudo commands.</span></span> <span data-ttu-id="c6437-111">Linux VM'ler için kök ayrıcalıklarına sahiptir.</span><span class="sxs-lookup"><span data-stu-id="c6437-111">It has root privileges to the Linux VMs.</span></span>

<span data-ttu-id="c6437-112">Bir etki alanına katılmış Hdınsight kümesi üç Ambari yönetici yanı sıra yeni kullanıcılar ve SSH kullanıcı sahiptir.</span><span class="sxs-lookup"><span data-stu-id="c6437-112">A domain-joined HDInsight cluster has three new users in addition to Ambari Admin and SSH user.</span></span>

* <span data-ttu-id="c6437-113">**Bırakabilmenizi yönetici**: Bu hesap yerel Apache bırakabilmenizi yönetici hesabıdır.</span><span class="sxs-lookup"><span data-stu-id="c6437-113">**Ranger admin**:  This account is the local Apache Ranger admin account.</span></span> <span data-ttu-id="c6437-114">Bir active directory etki alanı kullanıcısı değil.</span><span class="sxs-lookup"><span data-stu-id="c6437-114">It is not an active directory domain user.</span></span> <span data-ttu-id="c6437-115">Bu hesap ilkeleri kurulumu ve diğer kullanıcıların yöneticileri veya temsilci olarak atanan Yöneticiler (kullanıcılarla ilkeleri yönetebilmeniz için) yapmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="c6437-115">This account can be used to setup policies and make other users admins or delegated admins (so that those users can manage policies).</span></span> <span data-ttu-id="c6437-116">Varsayılan olarak, kullanıcı adı olan *yönetici* ve parola Ambari yönetici parolası ile aynıdır.</span><span class="sxs-lookup"><span data-stu-id="c6437-116">By default, the username is *admin* and the password is the same as the Ambari admin password.</span></span> <span data-ttu-id="c6437-117">Parola bırakabilmenizi Ayarları sayfasından güncelleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="c6437-117">The password can be updated from the Settings page in Ranger.</span></span>
* <span data-ttu-id="c6437-118">**Küme Yöneticisi etki alanı kullanıcısı**: Ambari ve bırakabilmenizi gibi Hadoop Küme Yöneticisi olarak atanmış bir active directory etki alanı kullanıcısı bu hesabıdır.</span><span class="sxs-lookup"><span data-stu-id="c6437-118">**Cluster admin domain user**: This account is an active directory domain user designated as the Hadoop cluster admin including Ambari and Ranger.</span></span> <span data-ttu-id="c6437-119">Küme oluşturma sırasında bu kullanıcının kimlik bilgilerini sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c6437-119">You must provide this user’s credentials during cluster creation.</span></span> <span data-ttu-id="c6437-120">Bu kullanıcı aşağıdaki ayrıcalıklara sahiptir:</span><span class="sxs-lookup"><span data-stu-id="c6437-120">This user has the following privileges:</span></span>

  * <span data-ttu-id="c6437-121">Makine etki alanına ve küme oluşturma sırasında belirttiğiniz OU içinde yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="c6437-121">Join machines to the domain and place them within the OU that you specify during cluster creation.</span></span>
  * <span data-ttu-id="c6437-122">Küme oluşturma sırasında belirttiğiniz OU içinde hizmet asıl adı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c6437-122">Create service principals within the OU that you specify during cluster creation.</span></span>
  * <span data-ttu-id="c6437-123">Geriye doğru DNS girdilerini oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c6437-123">Create reverse DNS entries.</span></span>

    <span data-ttu-id="c6437-124">Diğer AD kullanıcılar da bu ayrıcalıklarına sahip unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c6437-124">Note the other AD users also have these privileges.</span></span>

    <span data-ttu-id="c6437-125">Bırakabilmenizi tarafından yönetilmeyen ve bu nedenle güvenli olmayan bazı bitiş noktaları (örneğin, Templeton) kümedeki vardır.</span><span class="sxs-lookup"><span data-stu-id="c6437-125">There are some end points within the cluster (for example, Templeton) which are not managed by Ranger, and hence are not secure.</span></span> <span data-ttu-id="c6437-126">Bu uç noktaları, küme yönetim etki alanı kullanıcısı dışındaki tüm kullanıcılar için kilitlendiğini.</span><span class="sxs-lookup"><span data-stu-id="c6437-126">These end points are locked down for all users except the cluster admin domain user.</span></span>
* <span data-ttu-id="c6437-127">**Normal**: küme oluşturma sırasında birden çok active directory grupları sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="c6437-127">**Regular**: During cluster creation, you can provide multiple active directory groups.</span></span> <span data-ttu-id="c6437-128">Bu gruplardaki kullanıcıların bırakabilmenizi ve Ambari senkronize edilir.</span><span class="sxs-lookup"><span data-stu-id="c6437-128">The users in these groups will be synced to Ranger and Ambari.</span></span> <span data-ttu-id="c6437-129">Bu kullanıcılar etki alanı kullanıcıları ve yalnızca bırakabilmenizi yönetilen uç noktaları (örneğin, Hiveserver2) erişebilir.</span><span class="sxs-lookup"><span data-stu-id="c6437-129">These users are domain users and will have access to only Ranger-managed endpoints (for example, Hiveserver2).</span></span> <span data-ttu-id="c6437-130">RBAC ilkeleri ve bu kullanıcılara uygulanabilir denetim sağlar.</span><span class="sxs-lookup"><span data-stu-id="c6437-130">All the RBAC policies and auditing will be applicable to these users.</span></span>

## <a name="roles-of-domain-joined-hdinsight-clusters"></a><span data-ttu-id="c6437-131">Etki alanına katılmış Hdınsight kümeleri rolleri</span><span class="sxs-lookup"><span data-stu-id="c6437-131">Roles of Domain-joined HDInsight clusters</span></span>
<span data-ttu-id="c6437-132">Etki alanına katılmış Hdınsight aşağıdaki rolleri vardır:</span><span class="sxs-lookup"><span data-stu-id="c6437-132">Domain-joined HDInsight have the following roles:</span></span>

* <span data-ttu-id="c6437-133">Küme Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="c6437-133">Cluster Administrator</span></span>
* <span data-ttu-id="c6437-134">Küme işleci</span><span class="sxs-lookup"><span data-stu-id="c6437-134">Cluster Operator</span></span>
* <span data-ttu-id="c6437-135">Hizmet Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="c6437-135">Service Administrator</span></span>
* <span data-ttu-id="c6437-136">Hizmet işleci</span><span class="sxs-lookup"><span data-stu-id="c6437-136">Service Operator</span></span>
* <span data-ttu-id="c6437-137">Küme kullanıcı</span><span class="sxs-lookup"><span data-stu-id="c6437-137">Cluster User</span></span>

<span data-ttu-id="c6437-138">**Bu rolleri izinleri görmek için**</span><span class="sxs-lookup"><span data-stu-id="c6437-138">**To see the permissions of these roles**</span></span>

1. <span data-ttu-id="c6437-139">Ambari Yönetimi kullanıcı arabirimini açın.</span><span class="sxs-lookup"><span data-stu-id="c6437-139">Open the Ambari Management UI.</span></span>  <span data-ttu-id="c6437-140">Bkz: [ambarı Yönetimi kullanıcı arabirimini açın](#open-the-ambari-management-ui).</span><span class="sxs-lookup"><span data-stu-id="c6437-140">See [Open the Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="c6437-141">Sol menüden **rolleri**.</span><span class="sxs-lookup"><span data-stu-id="c6437-141">From the left menu, click **Roles**.</span></span>
3. <span data-ttu-id="c6437-142">İzinleri görmek üzere mavi soru işareti tıklatın:</span><span class="sxs-lookup"><span data-stu-id="c6437-142">Click the blue question mark to see the permissions:</span></span>

    ![Etki alanına katılmış Hdınsight rolleri izinleri](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-roles-permissions.png)

## <a name="open-the-ambari-management-ui"></a><span data-ttu-id="c6437-144">Ambari Yönetimi kullanıcı arabirimini açın</span><span class="sxs-lookup"><span data-stu-id="c6437-144">Open the Ambari Management UI</span></span>
1. <span data-ttu-id="c6437-145">[Azure portalı](https://portal.azure.com) üzerinde oturum açın.</span><span class="sxs-lookup"><span data-stu-id="c6437-145">Sign on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="c6437-146">Hdınsight kümenize bir dikey pencerede açın.</span><span class="sxs-lookup"><span data-stu-id="c6437-146">Open your HDInsight cluster in a blade.</span></span> <span data-ttu-id="c6437-147">Bkz: [listesi ve Göster kümeleri](hdinsight-administer-use-management-portal.md#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="c6437-147">See [List and show clusters](hdinsight-administer-use-management-portal.md#list-and-show-clusters).</span></span>
3. <span data-ttu-id="c6437-148">Tıklatın **Pano** Ambari'yi açmak için üstteki menüden.</span><span class="sxs-lookup"><span data-stu-id="c6437-148">Click **Dashboard** from the top menu to open Ambari.</span></span>
4. <span data-ttu-id="c6437-149">Ambari için Küme Yöneticisi etki alanı kullanıcı adı ve parola kullanarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="c6437-149">Log on to Ambari using the cluster administrator domain user name and password.</span></span>
5. <span data-ttu-id="c6437-150">Tıklatın **yönetici** üst açılır menüsünden sağ köşesindeki ve ardından **yönetmek Ambari**.</span><span class="sxs-lookup"><span data-stu-id="c6437-150">Click the **Admin** dropdown menu from the upper right corner, and then click **Manage Ambari**.</span></span>

    ![Etki alanına katılmış Hdınsight Ambari yönetme](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-manage-ambari.png)

    <span data-ttu-id="c6437-152">Kullanıcı arabirimini şuna benzer:</span><span class="sxs-lookup"><span data-stu-id="c6437-152">The UI looks like:</span></span>

    ![Etki alanına katılmış Hdınsight Ambari yönetim kullanıcı Arabirimi](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui.png)

## <a name="list-the-domain-users-synchronized-from-your-active-directory"></a><span data-ttu-id="c6437-154">Active Directory'nizden eşitlenen etki alanı kullanıcıları listele</span><span class="sxs-lookup"><span data-stu-id="c6437-154">List the domain users synchronized from your Active Directory</span></span>
1. <span data-ttu-id="c6437-155">Ambari Yönetimi kullanıcı arabirimini açın.</span><span class="sxs-lookup"><span data-stu-id="c6437-155">Open the Ambari Management UI.</span></span>  <span data-ttu-id="c6437-156">Bkz: [ambarı Yönetimi kullanıcı arabirimini açın](#open-the-ambari-management-ui).</span><span class="sxs-lookup"><span data-stu-id="c6437-156">See [Open the Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="c6437-157">Sol menüden **kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="c6437-157">From the left menu, click **Users**.</span></span> <span data-ttu-id="c6437-158">Hdınsight kümesine Active Directory'nizden eşitlenen tüm kullanıcılar göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="c6437-158">You shall see all the users synced from your Active Directory to the HDInsight cluster.</span></span>

    ![Etki alanına katılmış Hdınsight Ambari yönetim kullanıcı Arabirimi kullanıcıları listele](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-users.png)

## <a name="list-the-domain-groups-synchronized-from-your-active-directory"></a><span data-ttu-id="c6437-160">Active Directory'nizden eşitlenen etki alanı grupları listesi</span><span class="sxs-lookup"><span data-stu-id="c6437-160">List the domain groups synchronized from your Active Directory</span></span>
1. <span data-ttu-id="c6437-161">Ambari Yönetimi kullanıcı arabirimini açın.</span><span class="sxs-lookup"><span data-stu-id="c6437-161">Open the Ambari Management UI.</span></span>  <span data-ttu-id="c6437-162">Bkz: [ambarı Yönetimi kullanıcı arabirimini açın](#open-the-ambari-management-ui).</span><span class="sxs-lookup"><span data-stu-id="c6437-162">See [Open the Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="c6437-163">Sol menüden **grupları**.</span><span class="sxs-lookup"><span data-stu-id="c6437-163">From the left menu, click **Groups**.</span></span> <span data-ttu-id="c6437-164">Hdınsight kümesine Active Directory'nizden eşitlenen tüm grupları göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="c6437-164">You shall see all the groups synced from your Active Directory to the HDInsight cluster.</span></span>

    ![Etki alanına katılmış Hdınsight Ambari yönetim kullanıcı Arabirimi listesi grupları](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-groups.png)

## <a name="configure-hive-views-permissions"></a><span data-ttu-id="c6437-166">Hive görünümleri izinlerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="c6437-166">Configure Hive Views permissions</span></span>
1. <span data-ttu-id="c6437-167">Ambari Yönetimi kullanıcı arabirimini açın.</span><span class="sxs-lookup"><span data-stu-id="c6437-167">Open the Ambari Management UI.</span></span>  <span data-ttu-id="c6437-168">Bkz: [ambarı Yönetimi kullanıcı arabirimini açın](#open-the-ambari-management-ui).</span><span class="sxs-lookup"><span data-stu-id="c6437-168">See [Open the Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="c6437-169">Sol menüden **görünümleri**.</span><span class="sxs-lookup"><span data-stu-id="c6437-169">From the left menu, click **Views**.</span></span>
3. <span data-ttu-id="c6437-170">Tıklatın **HIVE** ayrıntılarını görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="c6437-170">Click **HIVE** to show the details.</span></span>

    ![Etki alanına katılmış Hdınsight Ambari yönetim kullanıcı Arabirimi Hive görünümleri](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-hive-views.png)
4. <span data-ttu-id="c6437-172">Tıklatın **Hive görünümü** Hive görünümleri yapılandırmak için bağlantı.</span><span class="sxs-lookup"><span data-stu-id="c6437-172">Click the **Hive View** link to configure Hive Views.</span></span>
5. <span data-ttu-id="c6437-173">Ekranı aşağı kaydırarak **izinleri** bölümü.</span><span class="sxs-lookup"><span data-stu-id="c6437-173">Scroll down to the **Permissions** section.</span></span>

    ![Etki alanına katılmış Hdınsight ambarı Yönetimi UI Hive görünümleri izinleri yapılandırma](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-hive-views-permissions.png)
6. <span data-ttu-id="c6437-175">Tıklatın **Kullanıcı Ekle** veya **Grup Ekle**ve ardından kullanıcılar veya Hive görünümleri grupları belirtin.</span><span class="sxs-lookup"><span data-stu-id="c6437-175">Click **Add User** or **Add Group**, and then specify the users or groups that can use Hive Views.</span></span>

## <a name="configure-users-for-the-roles"></a><span data-ttu-id="c6437-176">Kullanıcı rolleri için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="c6437-176">Configure users for the roles</span></span>
 <span data-ttu-id="c6437-177">Rolleri ve izinlerini listesini görmek için bkz: [rolleri, etki alanına katılmış Hdınsight kümeleri](#roles-of-domain---joined-hdinsight-clusters).</span><span class="sxs-lookup"><span data-stu-id="c6437-177">To see a list of roles and their permissions, see [Roles of Domain-joined HDInsight clusters](#roles-of-domain---joined-hdinsight-clusters).</span></span>

1. <span data-ttu-id="c6437-178">Ambari Yönetimi kullanıcı arabirimini açın.</span><span class="sxs-lookup"><span data-stu-id="c6437-178">Open the Ambari Management UI.</span></span>  <span data-ttu-id="c6437-179">Bkz: [ambarı Yönetimi kullanıcı arabirimini açın](#open-the-ambari-management-ui).</span><span class="sxs-lookup"><span data-stu-id="c6437-179">See [Open the Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="c6437-180">Sol menüden **rolleri**.</span><span class="sxs-lookup"><span data-stu-id="c6437-180">From the left menu, click **Roles**.</span></span>
3. <span data-ttu-id="c6437-181">Tıklatın **Kullanıcı Ekle** veya **Grup Ekle** kullanıcılar ve gruplar farklı rollere atamak için.</span><span class="sxs-lookup"><span data-stu-id="c6437-181">Click **Add User** or **Add Group** to assign users and groups to different roles.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c6437-182">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c6437-182">Next steps</span></span>
* <span data-ttu-id="c6437-183">Etki alanına katılmış HDInsight kümesini yapılandırmak için bkz. [Etki alanına katılmış HDInsight kümelerini yapılandırma](hdinsight-domain-joined-configure.md).</span><span class="sxs-lookup"><span data-stu-id="c6437-183">For configuring a Domain-joined HDInsight cluster, see [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md).</span></span>
* <span data-ttu-id="c6437-184">Hive ilkelerini yapılandırmak ve Hive sorgularını çalıştırmak için bkz. [Etki alanına katılmış HDInsight kümeleri için Hive ilkelerini yapılandırma](hdinsight-domain-joined-run-hive.md).</span><span class="sxs-lookup"><span data-stu-id="c6437-184">For configuring Hive policies and run Hive queries, see [Configure Hive policies for Domain-joined HDInsight clusters](hdinsight-domain-joined-run-hive.md).</span></span>
* <span data-ttu-id="c6437-185">Etki alanına katılmış Hdınsight kümelerinde SSH kullanarak Hive sorguları çalıştırmak için bkz: [Hdınsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).</span><span class="sxs-lookup"><span data-stu-id="c6437-185">For running Hive queries using SSH on Domain-joined HDInsight clusters, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).</span></span>
