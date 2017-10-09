---
title: Azure portal kullanarak Azure Data Lake Analytics aaaManage hello | Microsoft Docs
description: "Bilgi nasıl toomanage Data Lake Analytics sayılarının, veri kaynakları, kullanıcılar ve işler."
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: jhubbard
editor: cgronlun
ms.assetid: a0e045f1-73d6-427f-868d-7b55c10f811b
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: f63ccdfae79772c92e92462194e8cdc636a73dc6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-by-using-hello-azure-portal"></a><span data-ttu-id="d594a-103">Hello Azure portal kullanarak Azure Data Lake Analytics'i yönetme</span><span class="sxs-lookup"><span data-stu-id="d594a-103">Manage Azure Data Lake Analytics by using hello Azure portal</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="d594a-104">Azure portal toomanage Azure Data Lake Analytics hesapları, hesap veri kaynakları, kullanıcılar ve kullanarak işleri nasıl hello öğrenin.</span><span class="sxs-lookup"><span data-stu-id="d594a-104">Learn how toomanage Azure Data Lake Analytics accounts, account data sources, users, and jobs by using hello Azure portal.</span></span> <span data-ttu-id="d594a-105">diğer araçları kullanarak hakkında toosee yönetimi konuları hello sayfanın üst kısmındaki hello bir sekmesini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="d594a-105">toosee management topics about using other tools, click a tab at hello top of hello page.</span></span>

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-data-lake-analytics-accounts"></a><span data-ttu-id="d594a-106">Data Lake Analytics hesaplarını yönetme</span><span class="sxs-lookup"><span data-stu-id="d594a-106">Manage Data Lake Analytics accounts</span></span>

### <a name="create-an-account"></a><span data-ttu-id="d594a-107">Bir hesap oluşturun</span><span class="sxs-lookup"><span data-stu-id="d594a-107">Create an account</span></span>

1. <span data-ttu-id="d594a-108">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d594a-108">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="d594a-109">**Yeni** > **Zeka + analiz** > **Data Lake Analytics**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d594a-109">Click **New** > **Intelligence + analytics** > **Data Lake Analytics**.</span></span>
3. <span data-ttu-id="d594a-110">Aşağıdaki öğelerindeki hello için değerleri seçin:</span><span class="sxs-lookup"><span data-stu-id="d594a-110">Select values for hello following items:</span></span> 
   1. <span data-ttu-id="d594a-111">**Ad**: hello Data Lake Analytics hesabı hello adı.</span><span class="sxs-lookup"><span data-stu-id="d594a-111">**Name**: hello name of hello Data Lake Analytics account.</span></span>
   2. <span data-ttu-id="d594a-112">**Abonelik**: hello hesabı için kullanılan Azure aboneliği hello.</span><span class="sxs-lookup"><span data-stu-id="d594a-112">**Subscription**: hello Azure subscription used for hello account.</span></span>
   3. <span data-ttu-id="d594a-113">**Kaynak grubu**: hello Azure kaynak grubu toocreate hello hesap.</span><span class="sxs-lookup"><span data-stu-id="d594a-113">**Resource Group**: hello Azure resource group in which toocreate hello account.</span></span> 
   4. <span data-ttu-id="d594a-114">**Konum**: hello Data Lake Analytics hesabı için Azure veri merkezi hello.</span><span class="sxs-lookup"><span data-stu-id="d594a-114">**Location**: hello Azure datacenter for hello Data Lake Analytics account.</span></span> 
   5. <span data-ttu-id="d594a-115">**Data Lake Store**: hello Data Lake Analytics hesabı için kullanılan varsayılan deposu toobe hello.</span><span class="sxs-lookup"><span data-stu-id="d594a-115">**Data Lake Store**: hello default store toobe used for hello Data Lake Analytics account.</span></span> <span data-ttu-id="d594a-116">Hello Azure Data Lake Store hesabı ve hello Data Lake Analytics hesabı olmalıdır aynı konuma hello.</span><span class="sxs-lookup"><span data-stu-id="d594a-116">hello Azure Data Lake Store account and hello Data Lake Analytics account must be in hello same location.</span></span>
4. <span data-ttu-id="d594a-117">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d594a-117">Click **Create**.</span></span> 

### <a name="delete-a-data-lake-analytics-account"></a><span data-ttu-id="d594a-118">Bir Data Lake Analytics hesabı silme</span><span class="sxs-lookup"><span data-stu-id="d594a-118">Delete a Data Lake Analytics account</span></span>

<span data-ttu-id="d594a-119">Bir Data Lake Analytics hesabı silmeden önce varsayılan Data Lake Store hesabını silin.</span><span class="sxs-lookup"><span data-stu-id="d594a-119">Before you delete a Data Lake Analytics account, delete its default Data Lake Store account.</span></span>

1. <span data-ttu-id="d594a-120">Hello Azure portal, tooyour Data Lake Analytics hesabı gidin.</span><span class="sxs-lookup"><span data-stu-id="d594a-120">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="d594a-121">**Sil**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d594a-121">Click **Delete**.</span></span>
3. <span data-ttu-id="d594a-122">Tür hello hesap adı.</span><span class="sxs-lookup"><span data-stu-id="d594a-122">Type hello account name.</span></span>
4. <span data-ttu-id="d594a-123">**Sil**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d594a-123">Click **Delete**.</span></span>

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-data-sources"></a><span data-ttu-id="d594a-124">Veri kaynaklarını yönet</span><span class="sxs-lookup"><span data-stu-id="d594a-124">Manage data sources</span></span>

<span data-ttu-id="d594a-125">Data Lake Analytics veri kaynakları aşağıdaki hello destekler:</span><span class="sxs-lookup"><span data-stu-id="d594a-125">Data Lake Analytics supports hello following data sources:</span></span>

* <span data-ttu-id="d594a-126">Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="d594a-126">Data Lake Store</span></span>
* <span data-ttu-id="d594a-127">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="d594a-127">Azure Storage</span></span>

<span data-ttu-id="d594a-128">Veri Gezgini toobrowse veri kaynakları ve temel dosya yönetimi işlemleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d594a-128">You can use Data Explorer toobrowse data sources and perform basic file management operations.</span></span> 

### <a name="add-a-data-source"></a><span data-ttu-id="d594a-129">Veri kaynağı ekleme</span><span class="sxs-lookup"><span data-stu-id="d594a-129">Add a data source</span></span>

1. <span data-ttu-id="d594a-130">Hello Azure portal, tooyour Data Lake Analytics hesabı gidin.</span><span class="sxs-lookup"><span data-stu-id="d594a-130">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="d594a-131">Tıklatın **veri kaynakları**.</span><span class="sxs-lookup"><span data-stu-id="d594a-131">Click **Data Sources**.</span></span>
3. <span data-ttu-id="d594a-132">Tıklatın **veri kaynağı ekleme**.</span><span class="sxs-lookup"><span data-stu-id="d594a-132">Click **Add Data Source**.</span></span>
    
   * <span data-ttu-id="d594a-133">tooadd bir Data Lake Store hesabı, gereksinim duyduğunuz hello hesap adı ve erişim toohello hesap toobe mümkün tooquery onu.</span><span class="sxs-lookup"><span data-stu-id="d594a-133">tooadd a Data Lake Store account, you need hello account name and access toohello account toobe able tooquery it.</span></span>
   * <span data-ttu-id="d594a-134">Azure Blob Depolama tooadd hello depolama hesabı ve hello hesap anahtarı gerekir.</span><span class="sxs-lookup"><span data-stu-id="d594a-134">tooadd Azure Blob storage, you need hello storage account and hello account key.</span></span> <span data-ttu-id="d594a-135">toofind hello Portal'da bunları, Git toohello depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="d594a-135">toofind them, go toohello storage account in hello portal.</span></span>

## <a name="set-up-firewall-rules"></a><span data-ttu-id="d594a-136">Güvenlik duvarı kuralları ayarlamak</span><span class="sxs-lookup"><span data-stu-id="d594a-136">Set up firewall rules</span></span>

<span data-ttu-id="d594a-137">Data Lake Analytics toofurther erişim tooyour Data Lake Analytics hesabı kilitleme hello ağ düzeyinde kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d594a-137">You can use Data Lake Analytics toofurther lock down access tooyour Data Lake Analytics account at hello network level.</span></span> <span data-ttu-id="d594a-138">Bir güvenlik duvarını etkinleştir, bir IP adresi belirtin veya güvenilen istemcileriniz için bir IP adresi aralığı tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="d594a-138">You can enable a firewall, specify an IP address, or define an IP address range for your trusted clients.</span></span> <span data-ttu-id="d594a-139">Bu ölçüleri etkinleştirdikten sonra tanımlanan hello aralıkta hello IP adresine sahip yalnızca istemcileri toohello deposu bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="d594a-139">After you enable these measures, only clients that have hello IP addresses within hello defined range can connect toohello store.</span></span>

<span data-ttu-id="d594a-140">Azure Data Factory veya VM gibi diğer Azure hizmetleriyle toohello Data Lake Analytics hesabı bağlanıyorsanız, emin olun **izin Azure Hizmetleri** açık **üzerinde**.</span><span class="sxs-lookup"><span data-stu-id="d594a-140">If other Azure services, like Azure Data Factory or VMs, connect toohello Data Lake Analytics account, make sure that **Allow Azure Services** is turned **On**.</span></span> 

### <a name="set-up-a-firewall-rule"></a><span data-ttu-id="d594a-141">Bir güvenlik duvarı kuralı ayarlamak</span><span class="sxs-lookup"><span data-stu-id="d594a-141">Set up a firewall rule</span></span>

1. <span data-ttu-id="d594a-142">Hello Azure portal, tooyour Data Lake Analytics hesabı gidin.</span><span class="sxs-lookup"><span data-stu-id="d594a-142">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="d594a-143">Merhaba hello soldaki menüsünde **Güvenlik Duvarı**.</span><span class="sxs-lookup"><span data-stu-id="d594a-143">On hello menu on hello left, click **Firewall**.</span></span>

## <a name="add-a-new-user"></a><span data-ttu-id="d594a-144">Yeni kullanıcı ekleme</span><span class="sxs-lookup"><span data-stu-id="d594a-144">Add a new user</span></span>

<span data-ttu-id="d594a-145">Merhaba kullanabilirsiniz **Kullanıcı Ekleme Sihirbazı** tooeasily yeni Data Lake kullanıcı sağlama.</span><span class="sxs-lookup"><span data-stu-id="d594a-145">You can use hello **Add User Wizard** tooeasily provision new Data Lake users.</span></span>

1. <span data-ttu-id="d594a-146">Hello Azure portal, tooyour Data Lake Analytics hesabı gidin.</span><span class="sxs-lookup"><span data-stu-id="d594a-146">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="d594a-147">Sol, altında hello üzerinde **Başlarken**, tıklatın **Kullanıcı Ekleme Sihirbazı**.</span><span class="sxs-lookup"><span data-stu-id="d594a-147">On hello left, under **Getting Started**, click **Add User Wizard**.</span></span>
3. <span data-ttu-id="d594a-148">Bir kullanıcı seçin ve ardından **seçin**.</span><span class="sxs-lookup"><span data-stu-id="d594a-148">Select a user, and then click **Select**.</span></span>
4. <span data-ttu-id="d594a-149">Bir rol seçin ve ardından **seçin**.</span><span class="sxs-lookup"><span data-stu-id="d594a-149">Select a role, and then click **Select**.</span></span> <span data-ttu-id="d594a-150">Yeni bir geliştirici toouse Azure Data Lake, select hello yukarı tooset **Data Lake Analytics Geliştirici** rol.</span><span class="sxs-lookup"><span data-stu-id="d594a-150">tooset up a new developer toouse Azure Data Lake, select hello **Data Lake Analytics Developer** role.</span></span>
5. <span data-ttu-id="d594a-151">Merhaba U-SQL veritabanları için Hello erişim denetim listelerini (ACL'ler) seçin.</span><span class="sxs-lookup"><span data-stu-id="d594a-151">Select hello access control lists (ACLs) for hello U-SQL databases.</span></span> <span data-ttu-id="d594a-152">Seçimlerinizi yaptıktan sonra tıklatın **seçin**.</span><span class="sxs-lookup"><span data-stu-id="d594a-152">When you're satisfied with your choices, click **Select**.</span></span>
6. <span data-ttu-id="d594a-153">Merhaba ACL'ler dosyaları için seçin.</span><span class="sxs-lookup"><span data-stu-id="d594a-153">Select hello ACLs for files.</span></span> <span data-ttu-id="d594a-154">Merhaba varsayılan deposu için hello kök klasör için hello ACL'ler değişmez "/" ve hello/sistem klasörü için.</span><span class="sxs-lookup"><span data-stu-id="d594a-154">For hello default store, don't change hello ACLs for hello root folder "/" and for hello /system folder.</span></span> <span data-ttu-id="d594a-155">**Seç**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d594a-155">Click **Select**.</span></span>
7. <span data-ttu-id="d594a-156">Tüm seçili değişikliklerinizi gözden geçirin ve ardından **çalıştırmak**.</span><span class="sxs-lookup"><span data-stu-id="d594a-156">Review all your selected changes, and then click **Run**.</span></span>
8. <span data-ttu-id="d594a-157">Merhaba sihirbaz tamamlandığında tıklatın **Bitti**.</span><span class="sxs-lookup"><span data-stu-id="d594a-157">When hello wizard is finished, click **Done**.</span></span>

## <a name="manage-role-based-access-control"></a><span data-ttu-id="d594a-158">Rol tabanlı erişim denetimini yönetmek</span><span class="sxs-lookup"><span data-stu-id="d594a-158">Manage Role-Based Access Control</span></span>

<span data-ttu-id="d594a-159">Diğer Azure hizmetleriyle gibi hello hizmeti ile kullanıcıların nasıl etkileşim rol tabanlı erişim denetimi (RBAC) toocontrol kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d594a-159">Like other Azure services, you can use Role-Based Access Control (RBAC) toocontrol how users interact with hello service.</span></span>

<span data-ttu-id="d594a-160">Hello standart RBAC rolleri, özellikleri aşağıdaki hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="d594a-160">hello standard RBAC roles have hello following capabilities:</span></span>
* <span data-ttu-id="d594a-161">**Sahibi**: iş göndermek, izleyebilir işleri, herhangi bir kullanıcı işlerini iptal edin ve hello hesabı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="d594a-161">**Owner**: Can submit jobs, monitor jobs, cancel jobs from any user, and configure hello account.</span></span>
* <span data-ttu-id="d594a-162">**Katkıda bulunan**: iş göndermek, izleyebilir işleri, herhangi bir kullanıcı işlerini iptal edin ve hello hesabı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="d594a-162">**Contributor**: Can submit jobs, monitor jobs, cancel jobs from any user, and configure hello account.</span></span>
* <span data-ttu-id="d594a-163">**Okuyucu**: işleri izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d594a-163">**Reader**: Can monitor jobs.</span></span>

<span data-ttu-id="d594a-164">Merhaba Data Lake Analytics geliştirici, rol, tooenable, U-SQL, geliştiriciler, toouse, Merhaba, Data Lake Analytics, hizmeti kullanın.</span><span class="sxs-lookup"><span data-stu-id="d594a-164">Use hello Data Lake Analytics Developer role tooenable U-SQL developers toouse hello Data Lake Analytics service.</span></span> <span data-ttu-id="d594a-165">Merhaba Data Lake Analytics Geliştirici rolüne kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d594a-165">You can use hello Data Lake Analytics Developer role to:</span></span>
* <span data-ttu-id="d594a-166">İşlerini gönderin.</span><span class="sxs-lookup"><span data-stu-id="d594a-166">Submit jobs.</span></span>
* <span data-ttu-id="d594a-167">Herhangi bir kullanıcı tarafından gönderilen işlerin iş durumunu ve hello ilerleme izleyin.</span><span class="sxs-lookup"><span data-stu-id="d594a-167">Monitor job status and hello progress of jobs submitted by any user.</span></span>
* <span data-ttu-id="d594a-168">Merhaba U-SQL betikleri herhangi bir kullanıcı tarafından gönderilen işlerine bakın.</span><span class="sxs-lookup"><span data-stu-id="d594a-168">See hello U-SQL scripts from jobs submitted by any user.</span></span>
* <span data-ttu-id="d594a-169">Yalnızca kendi işlerini iptal edin.</span><span class="sxs-lookup"><span data-stu-id="d594a-169">Cancel only your own jobs.</span></span>

### <a name="add-users-or-security-groups-tooa-data-lake-analytics-account"></a><span data-ttu-id="d594a-170">Kullanıcı veya güvenlik grupları tooa Data Lake Analytics hesabı ekleme</span><span class="sxs-lookup"><span data-stu-id="d594a-170">Add users or security groups tooa Data Lake Analytics account</span></span>

1. <span data-ttu-id="d594a-171">Hello Azure portal, tooyour Data Lake Analytics hesabı gidin.</span><span class="sxs-lookup"><span data-stu-id="d594a-171">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="d594a-172">Tıklatın **erişim denetimi (IAM)** > **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="d594a-172">Click **Access control (IAM)** > **Add**.</span></span>
3. <span data-ttu-id="d594a-173">Bir rol seçin.</span><span class="sxs-lookup"><span data-stu-id="d594a-173">Select a role.</span></span>
4. <span data-ttu-id="d594a-174">Bir kullanıcı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d594a-174">Add a user.</span></span>
5. <span data-ttu-id="d594a-175">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d594a-175">Click **OK**.</span></span>

>[!NOTE]
><span data-ttu-id="d594a-176">Bir kullanıcı veya güvenlik grubu toosubmit işleri gerekiyorsa, bunlar da hello depolama hesabındaki izni gerekir.</span><span class="sxs-lookup"><span data-stu-id="d594a-176">If a user or a security group needs toosubmit jobs, they also need permission on hello store account.</span></span> <span data-ttu-id="d594a-177">Daha fazla bilgi için bkz: [güvenli Data Lake Store içinde depolanan verileri](../data-lake-store/data-lake-store-secure-data.md).</span><span class="sxs-lookup"><span data-stu-id="d594a-177">For more information, see [Secure data stored in Data Lake Store](../data-lake-store/data-lake-store-secure-data.md).</span></span>
>

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-jobs"></a><span data-ttu-id="d594a-178">İşleri yönetme</span><span class="sxs-lookup"><span data-stu-id="d594a-178">Manage jobs</span></span>

### <a name="submit-a-job"></a><span data-ttu-id="d594a-179">Bir işi gönderin</span><span class="sxs-lookup"><span data-stu-id="d594a-179">Submit a job</span></span>

1. <span data-ttu-id="d594a-180">Hello Azure portal, tooyour Data Lake Analytics hesabı gidin.</span><span class="sxs-lookup"><span data-stu-id="d594a-180">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>

2. <span data-ttu-id="d594a-181">Tıklatın **yeni iş**.</span><span class="sxs-lookup"><span data-stu-id="d594a-181">Click **New Job**.</span></span> <span data-ttu-id="d594a-182">Her bir iş yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="d594a-182">For each job,  configure:</span></span>

    1. <span data-ttu-id="d594a-183">**İş adı**: hello işinin hello adı.</span><span class="sxs-lookup"><span data-stu-id="d594a-183">**Job Name**: hello name of hello job.</span></span>
    2. <span data-ttu-id="d594a-184">**Öncelik**: alt numaraları yüksek önceliği vardır.</span><span class="sxs-lookup"><span data-stu-id="d594a-184">**Priority**: Lower numbers have higher priority.</span></span> <span data-ttu-id="d594a-185">İki işi sıraya alınmışsa, düşük öncelik değerine sahip hello ilk çalışır.</span><span class="sxs-lookup"><span data-stu-id="d594a-185">If two jobs are queued, hello one with lower priority value runs first.</span></span>
    3. <span data-ttu-id="d594a-186">**Paralellik**: hello en fazla işlem sayısı bu işin tooreserve işler.</span><span class="sxs-lookup"><span data-stu-id="d594a-186">**Parallelism**: hello maximum number of compute processes tooreserve for this job.</span></span>

3. <span data-ttu-id="d594a-187">**İşi Gönder**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d594a-187">Click **Submit Job**.</span></span>

### <a name="monitor-jobs"></a><span data-ttu-id="d594a-188">İşleri izleme</span><span class="sxs-lookup"><span data-stu-id="d594a-188">Monitor jobs</span></span>

1. <span data-ttu-id="d594a-189">Hello Azure portal, tooyour Data Lake Analytics hesabı gidin.</span><span class="sxs-lookup"><span data-stu-id="d594a-189">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="d594a-190">Tıklatın **tüm işleri görüntüleyin**.</span><span class="sxs-lookup"><span data-stu-id="d594a-190">Click **View All Jobs**.</span></span> <span data-ttu-id="d594a-191">Merhaba hesaptaki tüm hello etkin ve en son bitmiş işlerin bir listesini gösterilir.</span><span class="sxs-lookup"><span data-stu-id="d594a-191">A list of all hello active and recently finished jobs in hello account is shown.</span></span>
3. <span data-ttu-id="d594a-192">İsteğe bağlı olarak, tıklayın **filtre** hello işleri tarafından bulduğunuz toohelp **zaman aralığı**, **iş adı**, ve **Yazar** değerleri.</span><span class="sxs-lookup"><span data-stu-id="d594a-192">Optionally, click **Filter** toohelp you find hello jobs by **Time Range**, **Job Name**, and **Author** values.</span></span> 

### <a name="monitoring-pipeline-jobs"></a><span data-ttu-id="d594a-193">Ardışık Düzen işlerini izleme</span><span class="sxs-lookup"><span data-stu-id="d594a-193">Monitoring pipeline jobs</span></span>
<span data-ttu-id="d594a-194">Bir işlem hattı parçası olan birlikte, genellikle bir sırayla tooaccomplish belirli bir senaryoyu işler.</span><span class="sxs-lookup"><span data-stu-id="d594a-194">Jobs that are part of a pipeline work together, usually sequentially, tooaccomplish a specific scenario.</span></span> <span data-ttu-id="d594a-195">Örneğin, temizler, ayıklar, dönüşümleri, müşteri Öngörüler için kullanım toplayan bir ardışık düzen olabilir.</span><span class="sxs-lookup"><span data-stu-id="d594a-195">For example, you can have a pipeline that cleans, extracts, transforms, aggregates usage for customer insights.</span></span> <span data-ttu-id="d594a-196">Ardışık Düzen işleri hello iş gönderildiğinde hello "Ardışık düzen" özelliği kullanılarak tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="d594a-196">Pipeline jobs are identified using hello "Pipeline" property when hello job was submitted.</span></span> <span data-ttu-id="d594a-197">ADF V2 kullanılarak zamanlanan işleri otomatik olarak doldurulmuş bu özelliğe sahip.</span><span class="sxs-lookup"><span data-stu-id="d594a-197">Jobs scheduled using ADF V2 will automatically have this property populated.</span></span> 

<span data-ttu-id="d594a-198">Ardışık Düzen parçası olan U-SQL işlerin bir listesini tooview:</span><span class="sxs-lookup"><span data-stu-id="d594a-198">tooview a list of U-SQL jobs that are part of pipelines:</span></span> 

1. <span data-ttu-id="d594a-199">Hello Azure portal, tooyour Data Lake Analytics hesapları gidin.</span><span class="sxs-lookup"><span data-stu-id="d594a-199">In hello Azure portal, go tooyour Data Lake Analytics accounts.</span></span>
2. <span data-ttu-id="d594a-200">Tıklatın **iş Öngörüler**.</span><span class="sxs-lookup"><span data-stu-id="d594a-200">Click **Job Insights**.</span></span> <span data-ttu-id="d594a-201">"Tüm işleri" sekmesi, çalışan, listesini gösteren varsayılan olacak hello sıraya ve işleri sona erdi.</span><span class="sxs-lookup"><span data-stu-id="d594a-201">hello "All Jobs" tab will be defaulted, showing a list of running, queued, and ended jobs.</span></span>
3. <span data-ttu-id="d594a-202">Merhaba tıklatın **ardışık düzen işleri** sekmesi. Ardışık Düzen işlerin bir listesini her ardışık düzeni için toplu istatistikler birlikte gösterilir.</span><span class="sxs-lookup"><span data-stu-id="d594a-202">Click hello **Pipeline Jobs** tab. A list of pipeline jobs will be shown along with aggregated statistics for each pipeline.</span></span>

### <a name="monitoring-recurring-jobs"></a><span data-ttu-id="d594a-203">Yinelenen işlerini izleme</span><span class="sxs-lookup"><span data-stu-id="d594a-203">Monitoring recurring jobs</span></span>
<span data-ttu-id="d594a-204">Yinelenen bir işi hello sahip biridir aynı iş mantığı her çalıştığında farklı giriş verisi ancak kullanır.</span><span class="sxs-lookup"><span data-stu-id="d594a-204">A recurring job is one that has hello same business logic but uses different input data every time it runs.</span></span> <span data-ttu-id="d594a-205">İdeal olarak, yinelenen işleri her zaman başarılı ve göreceli olarak tutarlı yürütme süresi vardır; Bu davranışların izleme hello iş sağlıklı olduğundan emin olun yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="d594a-205">Ideally, recurring jobs should always succeed, and have relatively stable execution time; monitoring these behaviors will help ensure hello job is healthy.</span></span> <span data-ttu-id="d594a-206">Yinelenen işleri hello "Recurrence" özelliği kullanılarak tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="d594a-206">Recurring jobs are identified using hello "Recurrence" property.</span></span> <span data-ttu-id="d594a-207">ADF V2 kullanılarak zamanlanan işleri otomatik olarak doldurulmuş bu özelliğe sahip.</span><span class="sxs-lookup"><span data-stu-id="d594a-207">Jobs scheduled using ADF V2 will automatically have this property populated.</span></span>

<span data-ttu-id="d594a-208">tooview yinelenen U-SQL işleri listesi:</span><span class="sxs-lookup"><span data-stu-id="d594a-208">tooview a list of U-SQL jobs that are recurring:</span></span> 

1. <span data-ttu-id="d594a-209">Hello Azure portal, tooyour Data Lake Analytics hesapları gidin.</span><span class="sxs-lookup"><span data-stu-id="d594a-209">In hello Azure portal, go tooyour Data Lake Analytics accounts.</span></span>
2. <span data-ttu-id="d594a-210">Tıklatın **iş Öngörüler**.</span><span class="sxs-lookup"><span data-stu-id="d594a-210">Click **Job Insights**.</span></span> <span data-ttu-id="d594a-211">"Tüm işleri" sekmesi, çalışan, listesini gösteren varsayılan olacak hello sıraya ve işleri sona erdi.</span><span class="sxs-lookup"><span data-stu-id="d594a-211">hello "All Jobs" tab will be defaulted, showing a list of running, queued, and ended jobs.</span></span>
3. <span data-ttu-id="d594a-212">Merhaba tıklatın **yinelenen işleri** sekmesi. Yinelenen işlerin bir listesini, yinelenen her iş için toplu istatistikler birlikte gösterilir.</span><span class="sxs-lookup"><span data-stu-id="d594a-212">Click hello **Recurring Jobs** tab. A list of recurring jobs will be shown along with aggregated statistics for each recurring job.</span></span>

## <a name="manage-policies"></a><span data-ttu-id="d594a-213">İlkeleri yönetme</span><span class="sxs-lookup"><span data-stu-id="d594a-213">Manage policies</span></span>

### <a name="account-level-policies"></a><span data-ttu-id="d594a-214">Hesap düzeyinde ilkeleri</span><span class="sxs-lookup"><span data-stu-id="d594a-214">Account-level policies</span></span>

<span data-ttu-id="d594a-215">Bu ilkeler, bir Data Lake Analytics hesabı tooall işleri geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="d594a-215">These policies apply tooall jobs in a Data Lake Analytics account.</span></span>

#### <a name="maximum-number-of-aus-in-a-data-lake-analytics-account"></a><span data-ttu-id="d594a-216">En fazla Avustralya numarasında Data Lake Analytics hesabı</span><span class="sxs-lookup"><span data-stu-id="d594a-216">Maximum number of AUs in a Data Lake Analytics account</span></span>
<span data-ttu-id="d594a-217">Bir ilke hello Analytics Data Lake Analytics hesabınızı kullanabilirsiniz birimlerin (Avustralya) toplam sayısını denetler.</span><span class="sxs-lookup"><span data-stu-id="d594a-217">A policy controls hello total number of Analytics Units (AUs) your Data Lake Analytics account can use.</span></span> <span data-ttu-id="d594a-218">Varsayılan olarak, too250 hello değer ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="d594a-218">By default, hello value is set too250.</span></span> <span data-ttu-id="d594a-219">Bu değer too250 Avustralya ayarlanırsa, örneğin, 250 atanan Avustralya tooit ile çalışan bir iş ya da 25 ile çalışan 10 işleri olabilir Avustralya her.</span><span class="sxs-lookup"><span data-stu-id="d594a-219">For example, if this value is set too250 AUs, you can have one job running with 250 AUs assigned tooit, or 10 jobs running with 25 AUs each.</span></span> <span data-ttu-id="d594a-220">Hello çalışan işler tamamlanana kadar gönderilen ek işler kuyruğa alınır.</span><span class="sxs-lookup"><span data-stu-id="d594a-220">Additional jobs that are submitted are queued until hello running jobs are finished.</span></span> <span data-ttu-id="d594a-221">Çalışan işleri tamamlandığında, Avustralya kaydınızı hello kurtulurlar işleri toorun sıraya alındı.</span><span class="sxs-lookup"><span data-stu-id="d594a-221">When running jobs are finished, AUs are freed up for hello queued jobs toorun.</span></span>

<span data-ttu-id="d594a-222">toochange hello sayısı Avustralya, Data Lake Analytics hesabı için:</span><span class="sxs-lookup"><span data-stu-id="d594a-222">toochange hello number of AUs for your Data Lake Analytics account:</span></span>

1. <span data-ttu-id="d594a-223">Hello Azure portal, tooyour Data Lake Analytics hesabı gidin.</span><span class="sxs-lookup"><span data-stu-id="d594a-223">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="d594a-224">**Özellikler**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d594a-224">Click **Properties**.</span></span>
3. <span data-ttu-id="d594a-225">Altında **maksimum Avustralya**hello kaydırıcı tooselect bir değer taşımak veya hello değeri hello metin kutusuna girin.</span><span class="sxs-lookup"><span data-stu-id="d594a-225">Under **Maximum AUs**, move hello slider tooselect a value, or enter hello value in hello text box.</span></span> 
4. <span data-ttu-id="d594a-226">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d594a-226">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="d594a-227">Size gereken birden çok hello varsayılan (250) Avustralya, hello Portalı'nda tıklatın **Yardım + Destek** toosubmit bir destek isteği.</span><span class="sxs-lookup"><span data-stu-id="d594a-227">If you need more than hello default (250) AUs, in hello portal, click **Help+Support** toosubmit a support request.</span></span> <span data-ttu-id="d594a-228">Avustralya Data Lake Analytics hesabınızı kullanılabilir Hello sayısı artırılabilir.</span><span class="sxs-lookup"><span data-stu-id="d594a-228">hello number of AUs available in your Data Lake Analytics account can be increased.</span></span>
>

#### <a name="maximum-number-of-jobs-that-can-run-simultaneously"></a><span data-ttu-id="d594a-229">Aynı anda çalışabilir işi sayısı üst sınırı</span><span class="sxs-lookup"><span data-stu-id="d594a-229">Maximum number of jobs that can run simultaneously</span></span>
<span data-ttu-id="d594a-230">Bir ilke kaç işleri hello çalıştırabilirsiniz denetimleri aynı anda.</span><span class="sxs-lookup"><span data-stu-id="d594a-230">A policy controls how many jobs can run at hello same time.</span></span> <span data-ttu-id="d594a-231">Varsayılan olarak, bu değer too20 ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="d594a-231">By default, this value is set too20.</span></span> <span data-ttu-id="d594a-232">Data Lake Analytics Avustralya kullanılabilir olan yeni işleri hemen işleri çalıştırma hello toplam sayısı bu ilkenin hello değere ulaşana kadar zamanlanmış toorun demektir.</span><span class="sxs-lookup"><span data-stu-id="d594a-232">If your Data Lake Analytics has AUs available, new jobs are scheduled toorun immediately until hello total number of running jobs reaches hello value of this policy.</span></span> <span data-ttu-id="d594a-233">Merhaba iş sayısı üst sınırını aynı anda çalışabilecek ulaştığında, sonraki işleri (AU kullanılabilirliğine bağlı olarak) bir veya daha fazla çalışan iş tamamlanana kadar öncelik sırasına göre sıralanır.</span><span class="sxs-lookup"><span data-stu-id="d594a-233">When you reach hello maximum number of jobs that can run simultaneously, subsequent jobs are queued in priority order until one or more running jobs complete (depending on AU availability).</span></span>

<span data-ttu-id="d594a-234">aynı anda çalışabilecek iş toochange hello sayısı:</span><span class="sxs-lookup"><span data-stu-id="d594a-234">toochange hello number of jobs that can run simultaneously:</span></span>

1. <span data-ttu-id="d594a-235">Hello Azure portal, tooyour Data Lake Analytics hesabı gidin.</span><span class="sxs-lookup"><span data-stu-id="d594a-235">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="d594a-236">**Özellikler**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d594a-236">Click **Properties**.</span></span>
3. <span data-ttu-id="d594a-237">Altında **en büyük sayı, çalışan işleri**hello kaydırıcı tooselect bir değer taşımak veya hello değeri hello metin kutusuna girin.</span><span class="sxs-lookup"><span data-stu-id="d594a-237">Under **Maximum Number of Running Jobs**, move hello slider tooselect a value, or enter hello value in hello text box.</span></span> 
4. <span data-ttu-id="d594a-238">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d594a-238">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="d594a-239">Daha fazla varsayılan (20) hello portalında, iş sayısı hello daha tıklatın toorun gerekiyorsa **Yardım + Destek** toosubmit bir destek isteği.</span><span class="sxs-lookup"><span data-stu-id="d594a-239">If you need toorun more than hello default (20) number of jobs, in hello portal, click **Help+Support** toosubmit a support request.</span></span> <span data-ttu-id="d594a-240">Data Lake Analytics hesabınızı eşzamanlı olarak çalışabilecek iş Hello sayısı artırılabilir.</span><span class="sxs-lookup"><span data-stu-id="d594a-240">hello number of jobs that can run simultaneously in your Data Lake Analytics account can be increased.</span></span>
>

#### <a name="how-long-tookeep-job-metadata-and-resources"></a><span data-ttu-id="d594a-241">Ne kadar süreyle tookeep işi meta verileri ve kaynaklar</span><span class="sxs-lookup"><span data-stu-id="d594a-241">How long tookeep job metadata and resources</span></span> 
<span data-ttu-id="d594a-242">Kullanıcılarınızın U-SQL işleri çalıştırdığınızda, hello Data Lake Analytics hizmeti ilişkili tüm dosyaları korur.</span><span class="sxs-lookup"><span data-stu-id="d594a-242">When your users run U-SQL jobs, hello Data Lake Analytics service retains all related files.</span></span> <span data-ttu-id="d594a-243">İlgili dosyalar hello U-SQL komut dosyası, hello U-SQL komut dosyası, derlenmiş kaynaklar ve İstatistikler başvurulan hello DLL dosyaları içerir.</span><span class="sxs-lookup"><span data-stu-id="d594a-243">Related files include hello U-SQL script, hello DLL files referenced in hello U-SQL script, compiled resources, and statistics.</span></span> <span data-ttu-id="d594a-244">Merhaba, hello /system/ klasöründe hello varsayılan Azure Data Lake Store hesabına dosyalarıdır.</span><span class="sxs-lookup"><span data-stu-id="d594a-244">hello files are in hello /system/ folder of hello default Azure Data Lake Storage account.</span></span> <span data-ttu-id="d594a-245">Bu ilke, bu kaynakları otomatik olarak silinmeden önce ne kadar süreyle depolanır denetler (Merhaba varsayılan olarak 30 gün).</span><span class="sxs-lookup"><span data-stu-id="d594a-245">This policy controls how long these resources are stored before they are automatically deleted (hello default is 30 days).</span></span> <span data-ttu-id="d594a-246">Hata ayıklama ve hello gelecekteki yeniden işleri için performans ayarlama, bu dosyaları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d594a-246">You can use these files for debugging, and for performance-tuning of jobs that you'll rerun in hello future.</span></span>

<span data-ttu-id="d594a-247">toochange ne kadar süreyle tookeep işi meta verileri ve kaynaklar:</span><span class="sxs-lookup"><span data-stu-id="d594a-247">toochange how long tookeep job metadata and resources:</span></span>

1. <span data-ttu-id="d594a-248">Hello Azure portal, tooyour Data Lake Analytics hesabı gidin.</span><span class="sxs-lookup"><span data-stu-id="d594a-248">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="d594a-249">**Özellikler**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d594a-249">Click **Properties**.</span></span>
3. <span data-ttu-id="d594a-250">Altında **gün tooRetain iş sorguları**hello kaydırıcı tooselect bir değer taşımak veya hello değeri hello metin kutusuna girin.</span><span class="sxs-lookup"><span data-stu-id="d594a-250">Under **Days tooRetain Job Queries**, move hello slider tooselect a value, or enter hello value in hello text box.</span></span>  
4. <span data-ttu-id="d594a-251">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d594a-251">Click **Save**.</span></span>

### <a name="job-level-policies"></a><span data-ttu-id="d594a-252">Proje düzeyi ilkeleri</span><span class="sxs-lookup"><span data-stu-id="d594a-252">Job-level policies</span></span>
<span data-ttu-id="d594a-253">İş düzeyinde ilkeleriyle kontrol edebilirsiniz maksimum Avustralya hello ve hello bireysel kullanıcılar (veya belirli güvenlik gruplarının üyeleri) bunlar gönderme işlere ayarlayabilirsiniz en yüksek öncelik.</span><span class="sxs-lookup"><span data-stu-id="d594a-253">With job-level policies, you can control hello maximum AUs and hello maximum priority that individual users (or members of specific security groups) can set on jobs that they submit.</span></span> <span data-ttu-id="d594a-254">Bu kullanıcılar tarafından hello maliyetleri kontrol etmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="d594a-254">This lets you control hello costs incurred by users.</span></span> <span data-ttu-id="d594a-255">Ayrıca sağlar zamanlanmış iş denetim hello etkisi, yüksek öncelikli olabilir çalışmakta olan üretim işlerini hello aynı Data Lake Analytics hesabı.</span><span class="sxs-lookup"><span data-stu-id="d594a-255">It also lets you control hello effect that scheduled jobs might have on high-priority production jobs that are running in hello same Data Lake Analytics account.</span></span>

<span data-ttu-id="d594a-256">Data Lake Analytics hello iş düzeyinde ayarlayabilirsiniz iki ilke vardır:</span><span class="sxs-lookup"><span data-stu-id="d594a-256">Data Lake Analytics has two policies that you can set at hello job level:</span></span>

* <span data-ttu-id="d594a-257">**İş başına AU sınırı**: kullanıcılar yalnızca Avustralya toothis sayıda işleri gönderme.</span><span class="sxs-lookup"><span data-stu-id="d594a-257">**AU limit per job**: Users can only submit jobs that have up toothis number of AUs.</span></span> <span data-ttu-id="d594a-258">Varsayılan olarak, bu sınır olan hello hello AU sınırını hello hesabı ile aynı.</span><span class="sxs-lookup"><span data-stu-id="d594a-258">By default, this limit is hello same as hello maximum AU limit for hello account.</span></span>
* <span data-ttu-id="d594a-259">**Öncelik**: kullanıcıların yalnızca bir öncelik eşit veya değerinden daha düşük toothis değerine sahip işlerin gönderin.</span><span class="sxs-lookup"><span data-stu-id="d594a-259">**Priority**: Users can only submit jobs that have a priority lower than or equal toothis value.</span></span> <span data-ttu-id="d594a-260">Daha yüksek bir sayı daha düşük bir öncelik anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="d594a-260">Note that a higher number means a lower priority.</span></span> <span data-ttu-id="d594a-261">Varsayılan olarak, bu too1, hello olası en yüksek öncelikli olduğu ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="d594a-261">By default, this is set too1, which is hello highest possible priority.</span></span>

<span data-ttu-id="d594a-262">Varsayılan ilke her hesabında kümesi yok.</span><span class="sxs-lookup"><span data-stu-id="d594a-262">There is a default policy set on every account.</span></span> <span data-ttu-id="d594a-263">Merhaba varsayılan ilke tooall kullanıcılar hello hesabının geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="d594a-263">hello default policy applies tooall users of hello account.</span></span> <span data-ttu-id="d594a-264">Ek ilkeler belirli kullanıcılar ve gruplar için ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d594a-264">You can set additional policies for specific users and groups.</span></span> 

> [!NOTE]
> <span data-ttu-id="d594a-265">Hesap düzeyinde ilkeler ve iş düzeyinde ilkeleri aynı anda uygulayın.</span><span class="sxs-lookup"><span data-stu-id="d594a-265">Account-level policies and job-level policies apply simultaneously.</span></span>
>

#### <a name="add-a-policy-for-a-specific-user-or-group"></a><span data-ttu-id="d594a-266">Belirli bir kullanıcı veya grup için bir ilke ekleme</span><span class="sxs-lookup"><span data-stu-id="d594a-266">Add a policy for a specific user or group</span></span>

1. <span data-ttu-id="d594a-267">Hello Azure portal, tooyour Data Lake Analytics hesabı gidin.</span><span class="sxs-lookup"><span data-stu-id="d594a-267">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="d594a-268">**Özellikler**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d594a-268">Click **Properties**.</span></span>
3. <span data-ttu-id="d594a-269">Altında **iş gönderim sınırları**, hello tıklatın **ilke Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="d594a-269">Under **Job Submission Limits**, click hello **Add Policy** button.</span></span> <span data-ttu-id="d594a-270">Ardından, seçin veya ayarları aşağıdaki hello girin:</span><span class="sxs-lookup"><span data-stu-id="d594a-270">Then, select or enter hello following settings:</span></span>
    1. <span data-ttu-id="d594a-271">**İlke adı işlem**: tooremind İlkesi bir ad girin, hello İlkesi hello amacı.</span><span class="sxs-lookup"><span data-stu-id="d594a-271">**Compute Policy Name**: Enter a policy name, tooremind you of hello purpose of hello policy.</span></span>
    2. <span data-ttu-id="d594a-272">**Kullanıcı veya Grup Seç**: hello kullanıcı veya bu ilkenin uygulandığı grup seçin.</span><span class="sxs-lookup"><span data-stu-id="d594a-272">**Select User or Group**: Select hello user or group this policy applies to.</span></span>
    3. <span data-ttu-id="d594a-273">**Merhaba iş AU sınırını ayarlama**: toohello geçerlidir hello AU sınırını ayarlama seçili kullanıcı veya grup.</span><span class="sxs-lookup"><span data-stu-id="d594a-273">**Set hello Job AU Limit**: Set hello AU limit that applies toohello selected user or group.</span></span>
    4. <span data-ttu-id="d594a-274">**Merhaba öncelik sınırı ayarlama**: toohello geçerlidir hello öncelik sınırını ayarlama seçili kullanıcı veya grup.</span><span class="sxs-lookup"><span data-stu-id="d594a-274">**Set hello Priority Limit**: Set hello priority limit that applies toohello selected user or group.</span></span>

4. <span data-ttu-id="d594a-275">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d594a-275">Click **Ok**.</span></span>

5. <span data-ttu-id="d594a-276">Merhaba yeni ilke hello listelenen **varsayılan** altında İlkesi tablo **iş gönderim sınırları**.</span><span class="sxs-lookup"><span data-stu-id="d594a-276">hello new policy is listed in hello **Default** policy table, under **Job Submission Limits**.</span></span> 

#### <a name="delete-or-edit-an-existing-policy"></a><span data-ttu-id="d594a-277">Silin veya mevcut bir ilkeyi Düzenle</span><span class="sxs-lookup"><span data-stu-id="d594a-277">Delete or edit an existing policy</span></span>

1. <span data-ttu-id="d594a-278">Hello Azure portal, tooyour Data Lake Analytics hesabı gidin.</span><span class="sxs-lookup"><span data-stu-id="d594a-278">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="d594a-279">**Özellikler**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d594a-279">Click **Properties**.</span></span>
3. <span data-ttu-id="d594a-280">Altında **iş gönderim sınırları**, tooedit istediğiniz Bul hello ilkesi.</span><span class="sxs-lookup"><span data-stu-id="d594a-280">Under **Job Submission Limits**, find hello policy you want tooedit.</span></span>
4.  <span data-ttu-id="d594a-281">toosee hello **silmek** ve **Düzenle** Merhaba tablonun hello en sağdaki sütundaki seçenekleri **...** .</span><span class="sxs-lookup"><span data-stu-id="d594a-281">toosee hello **Delete** and **Edit** options, in hello rightmost column of hello table, click **...**.</span></span>

### <a name="additional-resources-for-job-policies"></a><span data-ttu-id="d594a-282">İş ilkeleri için ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="d594a-282">Additional resources for job policies</span></span>
* [<span data-ttu-id="d594a-283">İlke genel bakış blog gönderisi</span><span class="sxs-lookup"><span data-stu-id="d594a-283">Policy overview blog post</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-overview/)
* [<span data-ttu-id="d594a-284">Hesap düzeyinde ilkeler blog gönderisi</span><span class="sxs-lookup"><span data-stu-id="d594a-284">Account-level policies blog post</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-account-level-policy/)
* [<span data-ttu-id="d594a-285">Proje düzeyi ilkeleri blog gönderisi</span><span class="sxs-lookup"><span data-stu-id="d594a-285">Job-level policies blog post</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-job-level-policy/)

## <a name="next-steps"></a><span data-ttu-id="d594a-286">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d594a-286">Next steps</span></span>

* [<span data-ttu-id="d594a-287">Azure Data Lake Analytics'e genel bakış</span><span class="sxs-lookup"><span data-stu-id="d594a-287">Overview of Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="d594a-288">Hello Azure portal kullanarak Data Lake Analytics ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="d594a-288">Get started with Data Lake Analytics by using hello Azure portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="d594a-289">Azure PowerShell kullanarak Azure Data Lake Analytics'i yönetme</span><span class="sxs-lookup"><span data-stu-id="d594a-289">Manage Azure Data Lake Analytics by using Azure PowerShell</span></span>](data-lake-analytics-manage-use-powershell.md)

