---
title: "aaaManage etki alanına katılmış Hdınsight kümeleri - Azure | Microsoft Docs"
description: "Nasıl toomanage etki alanına katılmış Hdınsight kümeleri öğrenin"
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
ms.openlocfilehash: 233ddf0953e981f9a24b77d9dde194d590e5e6d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-domain-joined-hdinsight-clusters-preview"></a><span data-ttu-id="733b0-103">Etki alanına katılmış Hdınsight kümeleri (Önizleme) yönetme</span><span class="sxs-lookup"><span data-stu-id="733b0-103">Manage Domain-joined HDInsight clusters (Preview)</span></span>
<span data-ttu-id="733b0-104">Merhaba kullanıcılar ve etki alanına katılmış ve nasıl toomanage etki alanına katılmış Hdınsight kümeleri hello roller öğrenin.</span><span class="sxs-lookup"><span data-stu-id="733b0-104">Learn hello users and hello roles in Domain-joined HDInsight, and how toomanage domain-joined HDInsight clusters.</span></span>

## <a name="users-of-domain-joined-hdinsight-clusters"></a><span data-ttu-id="733b0-105">Kullanıcıları etki alanına katılmış Hdınsight kümeleri</span><span class="sxs-lookup"><span data-stu-id="733b0-105">Users of Domain-joined HDInsight clusters</span></span>
<span data-ttu-id="733b0-106">Merhaba küme oluşturma sırasında oluşturulan iki kullanıcı hesapları olmayan etki alanına katılmış bir Hdınsight kümesi vardır:</span><span class="sxs-lookup"><span data-stu-id="733b0-106">An HDInsight cluster that is not domain-joined has two user accounts that are created during hello cluster creation:</span></span>

* <span data-ttu-id="733b0-107">**Ambari yönetici**: Bu hesap olarak da bilinen, *Hadoop kullanıcı* veya *HTTP kullanıcı*.</span><span class="sxs-lookup"><span data-stu-id="733b0-107">**Ambari admin**: This account is also known as *Hadoop user* or *HTTP user*.</span></span> <span data-ttu-id="733b0-108">Bu hesap https:// adresindeki tooAmbari üzerinde kullanılan toolog olabilir&lt;clustername >. azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="733b0-108">This account can be used toolog on tooAmbari at https://&lt;clustername>.azurehdinsight.net.</span></span> <span data-ttu-id="733b0-109">Bu da kullanılan toorun sorgu Ambari görünümleri, harici araçlar (yani PowerShell, Templeton, Visual Studio) aracılığıyla işleri yürütmek ve hello Hive ODBC sürücüsü ve BI Araçları (yani Excel, Powerbı veya Tableau) ile kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="733b0-109">It can also be used toorun queries on Ambari views, execute jobs via external tools (i.e. PowerShell, Templeton, Visual Studio), and authenticate with hello Hive ODBC driver and BI tools (i.e. Excel, PowerBI, or Tableau).</span></span>
* <span data-ttu-id="733b0-110">**SSH kullanıcı**: Bu hesap ile SSH kullanılabilir ve sudo komutları yürütün.</span><span class="sxs-lookup"><span data-stu-id="733b0-110">**SSH user**:  This account can be used with SSH, and execute sudo commands.</span></span> <span data-ttu-id="733b0-111">Kök ayrıcalıkları toohello Linux VM'ler sahiptir.</span><span class="sxs-lookup"><span data-stu-id="733b0-111">It has root privileges toohello Linux VMs.</span></span>

<span data-ttu-id="733b0-112">Bir etki alanına katılmış Hdınsight kümesi üç yeni kullanıcı eklenmesi tooAmbari yönetici ve SSH kullanıcı sahiptir.</span><span class="sxs-lookup"><span data-stu-id="733b0-112">A domain-joined HDInsight cluster has three new users in addition tooAmbari Admin and SSH user.</span></span>

* <span data-ttu-id="733b0-113">**Bırakabilmenizi yönetici**: Bu hesap hello yerel Apache bırakabilmenizi yönetici hesabıdır.</span><span class="sxs-lookup"><span data-stu-id="733b0-113">**Ranger admin**:  This account is hello local Apache Ranger admin account.</span></span> <span data-ttu-id="733b0-114">Bir active directory etki alanı kullanıcısı değil.</span><span class="sxs-lookup"><span data-stu-id="733b0-114">It is not an active directory domain user.</span></span> <span data-ttu-id="733b0-115">Bu hesap, kullanılan toosetup ilkelerine ve diğer kullanıcıların yöneticileri veya temsilci olarak atanan Yöneticiler (kullanıcılarla ilkeleri yönetebilmeniz için) hale getirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="733b0-115">This account can be used toosetup policies and make other users admins or delegated admins (so that those users can manage policies).</span></span> <span data-ttu-id="733b0-116">Varsayılan olarak, hello kullanıcı adınızdır *yönetici* ve hello parola Ambari yönetici parolası hello aynı hello değil.</span><span class="sxs-lookup"><span data-stu-id="733b0-116">By default, hello username is *admin* and hello password is hello same as hello Ambari admin password.</span></span> <span data-ttu-id="733b0-117">Merhaba parola hello Ayarları sayfasından bırakabilmenizi güncelleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="733b0-117">hello password can be updated from hello Settings page in Ranger.</span></span>
* <span data-ttu-id="733b0-118">**Küme Yöneticisi etki alanı kullanıcısı**: Hadoop küme yönetim Ambari ve bırakabilmenizi gibi hello olarak atanmış bir active directory etki alanı kullanıcısı bu hesabıdır.</span><span class="sxs-lookup"><span data-stu-id="733b0-118">**Cluster admin domain user**: This account is an active directory domain user designated as hello Hadoop cluster admin including Ambari and Ranger.</span></span> <span data-ttu-id="733b0-119">Küme oluşturma sırasında bu kullanıcının kimlik bilgilerini sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="733b0-119">You must provide this user’s credentials during cluster creation.</span></span> <span data-ttu-id="733b0-120">Bu kullanıcı ayrıcalıkları aşağıdaki hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="733b0-120">This user has hello following privileges:</span></span>

  * <span data-ttu-id="733b0-121">Makineler toohello etki alanına katılma ve hello küme oluşturma sırasında belirttiğiniz OU içinde yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="733b0-121">Join machines toohello domain and place them within hello OU that you specify during cluster creation.</span></span>
  * <span data-ttu-id="733b0-122">Hizmet sorumluları hello küme oluşturma sırasında belirttiğiniz OU içinde oluşturun.</span><span class="sxs-lookup"><span data-stu-id="733b0-122">Create service principals within hello OU that you specify during cluster creation.</span></span>
  * <span data-ttu-id="733b0-123">Geriye doğru DNS girdilerini oluşturun.</span><span class="sxs-lookup"><span data-stu-id="733b0-123">Create reverse DNS entries.</span></span>

    <span data-ttu-id="733b0-124">Not hello diğer AD kullanıcılar da bu ayrıcalıklarına sahiptir.</span><span class="sxs-lookup"><span data-stu-id="733b0-124">Note hello other AD users also have these privileges.</span></span>

    <span data-ttu-id="733b0-125">Bırakabilmenizi tarafından yönetilmeyen ve bu nedenle güvenli olmayan bazı bitiş noktalarını hello küme (örneğin, Templeton) içinde vardır.</span><span class="sxs-lookup"><span data-stu-id="733b0-125">There are some end points within hello cluster (for example, Templeton) which are not managed by Ranger, and hence are not secure.</span></span> <span data-ttu-id="733b0-126">Bu uç noktaları, hello küme yönetici etki alanı kullanıcısı dışındaki tüm kullanıcılar için kilitlendiğini.</span><span class="sxs-lookup"><span data-stu-id="733b0-126">These end points are locked down for all users except hello cluster admin domain user.</span></span>
* <span data-ttu-id="733b0-127">**Normal**: küme oluşturma sırasında birden çok active directory grupları sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="733b0-127">**Regular**: During cluster creation, you can provide multiple active directory groups.</span></span> <span data-ttu-id="733b0-128">Bu gruplardaki kullanıcıların Hello eşitlenen tooRanger ve Ambari olacaktır.</span><span class="sxs-lookup"><span data-stu-id="733b0-128">hello users in these groups will be synced tooRanger and Ambari.</span></span> <span data-ttu-id="733b0-129">Bu kullanıcılar etki alanı kullanıcıları ve erişim tooonly bırakabilmenizi yönetilen uç noktaları (örneğin, Hiveserver2) sahip olacaktır.</span><span class="sxs-lookup"><span data-stu-id="733b0-129">These users are domain users and will have access tooonly Ranger-managed endpoints (for example, Hiveserver2).</span></span> <span data-ttu-id="733b0-130">Tüm RBAC ilkeleri hello ve denetim geçerli toothese kullanıcılar olacaktır.</span><span class="sxs-lookup"><span data-stu-id="733b0-130">All hello RBAC policies and auditing will be applicable toothese users.</span></span>

## <a name="roles-of-domain-joined-hdinsight-clusters"></a><span data-ttu-id="733b0-131">Etki alanına katılmış Hdınsight kümeleri rolleri</span><span class="sxs-lookup"><span data-stu-id="733b0-131">Roles of Domain-joined HDInsight clusters</span></span>
<span data-ttu-id="733b0-132">Etki alanına katılmış Hdınsight rolleri aşağıdaki hello vardır:</span><span class="sxs-lookup"><span data-stu-id="733b0-132">Domain-joined HDInsight have hello following roles:</span></span>

* <span data-ttu-id="733b0-133">Küme Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="733b0-133">Cluster Administrator</span></span>
* <span data-ttu-id="733b0-134">Küme işleci</span><span class="sxs-lookup"><span data-stu-id="733b0-134">Cluster Operator</span></span>
* <span data-ttu-id="733b0-135">Hizmet Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="733b0-135">Service Administrator</span></span>
* <span data-ttu-id="733b0-136">Hizmet işleci</span><span class="sxs-lookup"><span data-stu-id="733b0-136">Service Operator</span></span>
* <span data-ttu-id="733b0-137">Küme kullanıcı</span><span class="sxs-lookup"><span data-stu-id="733b0-137">Cluster User</span></span>

<span data-ttu-id="733b0-138">**Bu rolleri toosee hello izinleri**</span><span class="sxs-lookup"><span data-stu-id="733b0-138">**toosee hello permissions of these roles**</span></span>

1. <span data-ttu-id="733b0-139">Merhaba ambarı Yönetimi kullanıcı arabirimini açın.</span><span class="sxs-lookup"><span data-stu-id="733b0-139">Open hello Ambari Management UI.</span></span>  <span data-ttu-id="733b0-140">Bkz: [açık hello ambarı Yönetimi Arabirimi](#open-the-ambari-management-ui).</span><span class="sxs-lookup"><span data-stu-id="733b0-140">See [Open hello Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="733b0-141">Merhaba sol menüden **rolleri**.</span><span class="sxs-lookup"><span data-stu-id="733b0-141">From hello left menu, click **Roles**.</span></span>
3. <span data-ttu-id="733b0-142">Merhaba mavi soru işareti toosee hello izinler'i tıklatın:</span><span class="sxs-lookup"><span data-stu-id="733b0-142">Click hello blue question mark toosee hello permissions:</span></span>

    ![Etki alanına katılmış Hdınsight rolleri izinleri](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-roles-permissions.png)

## <a name="open-hello-ambari-management-ui"></a><span data-ttu-id="733b0-144">Açık hello ambarı Yönetimi Arabirimi</span><span class="sxs-lookup"><span data-stu-id="733b0-144">Open hello Ambari Management UI</span></span>
1. <span data-ttu-id="733b0-145">Toohello üzerinde oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="733b0-145">Sign on toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="733b0-146">Hdınsight kümenize bir dikey pencerede açın.</span><span class="sxs-lookup"><span data-stu-id="733b0-146">Open your HDInsight cluster in a blade.</span></span> <span data-ttu-id="733b0-147">Bkz: [listesi ve Göster kümeleri](hdinsight-administer-use-management-portal.md#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="733b0-147">See [List and show clusters](hdinsight-administer-use-management-portal.md#list-and-show-clusters).</span></span>
3. <span data-ttu-id="733b0-148">Tıklatın **Pano** hello üst menü tooopen Ambari gelen.</span><span class="sxs-lookup"><span data-stu-id="733b0-148">Click **Dashboard** from hello top menu tooopen Ambari.</span></span>
4. <span data-ttu-id="733b0-149">Üzerinde tooAmbari Hello Küme Yöneticisi etki alanı kullanıcı adı ve parola kullanarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="733b0-149">Log on tooAmbari using hello cluster administrator domain user name and password.</span></span>
5. <span data-ttu-id="733b0-150">Merhaba tıklatın **yönetici** hello sağ üst köşedeki ve ardından açılır menüsünden **yönetmek Ambari**.</span><span class="sxs-lookup"><span data-stu-id="733b0-150">Click hello **Admin** dropdown menu from hello upper right corner, and then click **Manage Ambari**.</span></span>

    ![Etki alanına katılmış Hdınsight Ambari yönetme](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-manage-ambari.png)

    <span data-ttu-id="733b0-152">Merhaba UI şuna benzer:</span><span class="sxs-lookup"><span data-stu-id="733b0-152">hello UI looks like:</span></span>

    ![Etki alanına katılmış Hdınsight Ambari yönetim kullanıcı Arabirimi](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui.png)

## <a name="list-hello-domain-users-synchronized-from-your-active-directory"></a><span data-ttu-id="733b0-154">Active Directory'nizden eşitlenen hello etki alanı kullanıcıları listele</span><span class="sxs-lookup"><span data-stu-id="733b0-154">List hello domain users synchronized from your Active Directory</span></span>
1. <span data-ttu-id="733b0-155">Merhaba ambarı Yönetimi kullanıcı arabirimini açın.</span><span class="sxs-lookup"><span data-stu-id="733b0-155">Open hello Ambari Management UI.</span></span>  <span data-ttu-id="733b0-156">Bkz: [açık hello ambarı Yönetimi Arabirimi](#open-the-ambari-management-ui).</span><span class="sxs-lookup"><span data-stu-id="733b0-156">See [Open hello Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="733b0-157">Merhaba sol menüden **kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="733b0-157">From hello left menu, click **Users**.</span></span> <span data-ttu-id="733b0-158">Active Directory toohello Hdınsight kümenizden eşitlenen tüm hello kullanıcılar göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="733b0-158">You shall see all hello users synced from your Active Directory toohello HDInsight cluster.</span></span>

    ![Etki alanına katılmış Hdınsight Ambari yönetim kullanıcı Arabirimi kullanıcıları listele](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-users.png)

## <a name="list-hello-domain-groups-synchronized-from-your-active-directory"></a><span data-ttu-id="733b0-160">Active Directory'nizden eşitlenen hello etki alanı grupları listesi</span><span class="sxs-lookup"><span data-stu-id="733b0-160">List hello domain groups synchronized from your Active Directory</span></span>
1. <span data-ttu-id="733b0-161">Merhaba ambarı Yönetimi kullanıcı arabirimini açın.</span><span class="sxs-lookup"><span data-stu-id="733b0-161">Open hello Ambari Management UI.</span></span>  <span data-ttu-id="733b0-162">Bkz: [açık hello ambarı Yönetimi Arabirimi](#open-the-ambari-management-ui).</span><span class="sxs-lookup"><span data-stu-id="733b0-162">See [Open hello Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="733b0-163">Merhaba sol menüden **grupları**.</span><span class="sxs-lookup"><span data-stu-id="733b0-163">From hello left menu, click **Groups**.</span></span> <span data-ttu-id="733b0-164">Active Directory toohello Hdınsight kümenizden eşitlenen tüm hello grupları göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="733b0-164">You shall see all hello groups synced from your Active Directory toohello HDInsight cluster.</span></span>

    ![Etki alanına katılmış Hdınsight Ambari yönetim kullanıcı Arabirimi listesi grupları](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-groups.png)

## <a name="configure-hive-views-permissions"></a><span data-ttu-id="733b0-166">Hive görünümleri izinlerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="733b0-166">Configure Hive Views permissions</span></span>
1. <span data-ttu-id="733b0-167">Merhaba ambarı Yönetimi kullanıcı arabirimini açın.</span><span class="sxs-lookup"><span data-stu-id="733b0-167">Open hello Ambari Management UI.</span></span>  <span data-ttu-id="733b0-168">Bkz: [açık hello ambarı Yönetimi Arabirimi](#open-the-ambari-management-ui).</span><span class="sxs-lookup"><span data-stu-id="733b0-168">See [Open hello Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="733b0-169">Merhaba sol menüden **görünümleri**.</span><span class="sxs-lookup"><span data-stu-id="733b0-169">From hello left menu, click **Views**.</span></span>
3. <span data-ttu-id="733b0-170">Tıklatın **HIVE** tooshow hello ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="733b0-170">Click **HIVE** tooshow hello details.</span></span>

    ![Etki alanına katılmış Hdınsight Ambari yönetim kullanıcı Arabirimi Hive görünümleri](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-hive-views.png)
4. <span data-ttu-id="733b0-172">Merhaba tıklatın **Hive görünümü** tooconfigure Hive görünümleri bağlantı.</span><span class="sxs-lookup"><span data-stu-id="733b0-172">Click hello **Hive View** link tooconfigure Hive Views.</span></span>
5. <span data-ttu-id="733b0-173">Toohello aşağı **izinleri** bölümü.</span><span class="sxs-lookup"><span data-stu-id="733b0-173">Scroll down toohello **Permissions** section.</span></span>

    ![Etki alanına katılmış Hdınsight ambarı Yönetimi UI Hive görünümleri izinleri yapılandırma](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-hive-views-permissions.png)
6. <span data-ttu-id="733b0-175">Tıklatın **Kullanıcı Ekle** veya **Grup Ekle**ve ardından hello kullanıcılar veya Hive görünümleri grupları belirtin.</span><span class="sxs-lookup"><span data-stu-id="733b0-175">Click **Add User** or **Add Group**, and then specify hello users or groups that can use Hive Views.</span></span>

## <a name="configure-users-for-hello-roles"></a><span data-ttu-id="733b0-176">Kullanıcılar hello rolleri için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="733b0-176">Configure users for hello roles</span></span>
 <span data-ttu-id="733b0-177">toosee roller ve onların izinlerini listesini görmek [rolleri, etki alanına katılmış Hdınsight kümeleri](#roles-of-domain---joined-hdinsight-clusters).</span><span class="sxs-lookup"><span data-stu-id="733b0-177">toosee a list of roles and their permissions, see [Roles of Domain-joined HDInsight clusters](#roles-of-domain---joined-hdinsight-clusters).</span></span>

1. <span data-ttu-id="733b0-178">Merhaba ambarı Yönetimi kullanıcı arabirimini açın.</span><span class="sxs-lookup"><span data-stu-id="733b0-178">Open hello Ambari Management UI.</span></span>  <span data-ttu-id="733b0-179">Bkz: [açık hello ambarı Yönetimi Arabirimi](#open-the-ambari-management-ui).</span><span class="sxs-lookup"><span data-stu-id="733b0-179">See [Open hello Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="733b0-180">Merhaba sol menüden **rolleri**.</span><span class="sxs-lookup"><span data-stu-id="733b0-180">From hello left menu, click **Roles**.</span></span>
3. <span data-ttu-id="733b0-181">Tıklatın **Kullanıcı Ekle** veya **Grup Ekle** tooassign kullanıcılar ve gruplar toodifferent rolleri.</span><span class="sxs-lookup"><span data-stu-id="733b0-181">Click **Add User** or **Add Group** tooassign users and groups toodifferent roles.</span></span>

## <a name="next-steps"></a><span data-ttu-id="733b0-182">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="733b0-182">Next steps</span></span>
* <span data-ttu-id="733b0-183">Etki alanına katılmış HDInsight kümesini yapılandırmak için bkz. [Etki alanına katılmış HDInsight kümelerini yapılandırma](hdinsight-domain-joined-configure.md).</span><span class="sxs-lookup"><span data-stu-id="733b0-183">For configuring a Domain-joined HDInsight cluster, see [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md).</span></span>
* <span data-ttu-id="733b0-184">Hive ilkelerini yapılandırmak ve Hive sorgularını çalıştırmak için bkz. [Etki alanına katılmış HDInsight kümeleri için Hive ilkelerini yapılandırma](hdinsight-domain-joined-run-hive.md).</span><span class="sxs-lookup"><span data-stu-id="733b0-184">For configuring Hive policies and run Hive queries, see [Configure Hive policies for Domain-joined HDInsight clusters](hdinsight-domain-joined-run-hive.md).</span></span>
* <span data-ttu-id="733b0-185">Etki alanına katılmış Hdınsight kümelerinde SSH kullanarak Hive sorguları çalıştırmak için bkz: [Hdınsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).</span><span class="sxs-lookup"><span data-stu-id="733b0-185">For running Hive queries using SSH on Domain-joined HDInsight clusters, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).</span></span>
