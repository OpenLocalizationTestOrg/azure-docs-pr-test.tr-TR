---
title: StorSimple 8000 serisi bir birimde kopyalama | Microsoft Docs
description: "Farklı kopya türleri ve kullanım tanımlar ve tek tek bir birim bir StorSimple 8000 serisi cihazda kopyalamak için bir yedek nasıl kullanabileceğinizi açıklar."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/26/2017
ms.author: alkohli
ms.openlocfilehash: 70c85bcb2c26d2ad3d0515d24e028f84495634c0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="use-the-storsimple-device-manager-service-in-azure-portal-to-clone-a-volume"></a><span data-ttu-id="caccc-103">StorSimple cihaz Yöneticisi hizmeti Azure portalında bir birim kopyalamak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="caccc-103">Use the StorSimple Device Manager service in Azure portal to clone a volume</span></span>

## <a name="overview"></a><span data-ttu-id="caccc-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="caccc-104">Overview</span></span>

<span data-ttu-id="caccc-105">Bu öğretici bir yedekleme kümesi aracılığıyla tek bir birim kopyalamak için nasıl kullanabileceğinizi açıklar **yedekleme kataloğu** dikey.</span><span class="sxs-lookup"><span data-stu-id="caccc-105">This tutorial describes how you can use a backup set to clone an individual volume via the **Backup catalog** blade.</span></span> <span data-ttu-id="caccc-106">Ayrıca arasındaki farkı açıklar *geçici* ve *kalıcı* klonlar.</span><span class="sxs-lookup"><span data-stu-id="caccc-106">It also explains the difference between *transient* and *permanent* clones.</span></span> <span data-ttu-id="caccc-107">Bu öğreticideki yönergeler güncelleştirme 3 veya sonraki sürümünü çalıştıran tüm StorSimple 8000 serisi aygıta uygular.</span><span class="sxs-lookup"><span data-stu-id="caccc-107">The guidance in this tutorial applies to all the StorSimple 8000 series device running Update 3 or later.</span></span>

<span data-ttu-id="caccc-108">StorSimple cihaz Yöneticisi hizmeti **yedekleme kataloğu** dikey penceresinde el ile veya otomatik yedeklemeler durumdayken, oluşturulan tüm yedekleme kümelerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="caccc-108">The StorSimple Device Manager service **Backup catalog** blade displays all the backup sets that are created when manual or automated backups are taken.</span></span> <span data-ttu-id="caccc-109">Bu gibi durumlarda, bir birim sonra bir yedekleme kopyalama kümesi seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="caccc-109">You can then select a volume in a backup set to clone.</span></span>

 ![Yedekleme kümesi listesi](./media/storsimple-8000-clone-volume-u2/bucatalog.png)

## <a name="considerations-for-cloning-a-volume"></a><span data-ttu-id="caccc-111">Bir birim kopyalama dikkat edilmesi gereken noktalar</span><span class="sxs-lookup"><span data-stu-id="caccc-111">Considerations for cloning a volume</span></span>

<span data-ttu-id="caccc-112">Aşağıdaki bilgiler bir birim kopyalarken göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="caccc-112">Consider the following information when cloning a volume.</span></span>

- <span data-ttu-id="caccc-113">Bir kopya normal birimi olarak aynı şekilde davranır.</span><span class="sxs-lookup"><span data-stu-id="caccc-113">A clone behaves in the same way as a regular volume.</span></span> <span data-ttu-id="caccc-114">Bir birimde mümkündür herhangi bir işlem kopya için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="caccc-114">Any operation that is possible on a volume is available for the clone.</span></span>

- <span data-ttu-id="caccc-115">İzleme ve varsayılan yedekleme otomatik olarak kopyalanan bir birimde devre dışı.</span><span class="sxs-lookup"><span data-stu-id="caccc-115">Monitoring and default backup are automatically disabled on a cloned volume.</span></span> <span data-ttu-id="caccc-116">Kopyalanan bir birimi tüm yedeklemeler için gerekir.</span><span class="sxs-lookup"><span data-stu-id="caccc-116">You would need to configure a cloned volume for any backups.</span></span>

- <span data-ttu-id="caccc-117">Yerel olarak sabitlenmiş bir birim katmanlı birim kopyalandı.</span><span class="sxs-lookup"><span data-stu-id="caccc-117">A locally pinned volume is cloned as a tiered volume.</span></span> <span data-ttu-id="caccc-118">Yerel olarak sabitlenmiş için kopyalanan birimi gerekiyorsa, kopyalama işlemi başarıyla tamamlandıktan sonra kopyanın yerel olarak sabitlenmiş bir birim dönüştürebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="caccc-118">If you need the cloned volume to be locally pinned, you can convert the clone to a locally pinned volume after the clone operation is successfully completed.</span></span> <span data-ttu-id="caccc-119">Yerel olarak sabitlenmiş bir birim için katmanlı birim dönüştürme hakkında daha fazla bilgi için Git [birim türünü değiştirme](storsimple-8000-manage-volumes-u2.md#change-the-volume-type).</span><span class="sxs-lookup"><span data-stu-id="caccc-119">For information about converting a tiered volume to a locally pinned volume, go to [Change the volume type](storsimple-8000-manage-volumes-u2.md#change-the-volume-type).</span></span>

- <span data-ttu-id="caccc-120">Kopyalanan bir birimden dönüştürmeyi deneyin (Bunu yine bir geçici kopya olduğunda) hemen kopyalandıktan sonra yerel olarak sabitlenmiş katmanlı dönüştürme şu hata iletisiyle başarısız olur:</span><span class="sxs-lookup"><span data-stu-id="caccc-120">If you try to convert a cloned volume from tiered to locally pinned immediately after cloning (when it is still a transient clone), the conversion fails with the following error message:</span></span>

    `Unable to modify the usage type for volume {0}. This can happen if the volume being modified is a transient clone and hasn’t been made permanent. Take a cloud snapshot of this volume and then retry the modify operation.`

    <span data-ttu-id="caccc-121">Yalnızca farklı bir cihaz açın kopyalama, bu hata alınır.</span><span class="sxs-lookup"><span data-stu-id="caccc-121">This error is received only if you are cloning on to a different device.</span></span> <span data-ttu-id="caccc-122">Yerel olarak sabitlenmiş geçici kopya kalıcı bir kopya ilk dönüştürürseniz birimi başarıyla dönüştürebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="caccc-122">You can successfully convert the volume to locally pinned if you first convert the transient clone to a permanent clone.</span></span> <span data-ttu-id="caccc-123">Kalıcı bir kopya dönüştürmek için geçici kopya bir bulut anlık görüntüsünü.</span><span class="sxs-lookup"><span data-stu-id="caccc-123">Take a cloud snapshot of the transient clone to convert it to a permanent clone.</span></span>

## <a name="create-a-clone-of-a-volume"></a><span data-ttu-id="caccc-124">Bir birimin bir kopyasını oluşturun</span><span class="sxs-lookup"><span data-stu-id="caccc-124">Create a clone of a volume</span></span>

<span data-ttu-id="caccc-125">Yerel kullanarak aynı aygıt, başka bir aygıt veya Bulut uygulaması bir kopya oluşturabilirsiniz veya Bulut anlık görüntüsü.</span><span class="sxs-lookup"><span data-stu-id="caccc-125">You can create a clone on the same device, another device, or even a cloud appliance by using a local or cloud snapshot.</span></span>

<span data-ttu-id="caccc-126">Aşağıdaki yordamda bir kopya yedekleme Kataloğu'ndan oluşturmayı açıklar.</span><span class="sxs-lookup"><span data-stu-id="caccc-126">The procedure below describes how to create a clone from the backup catalog.</span></span>  <span data-ttu-id="caccc-127">Gitmek için kopya başlatmak için alternatif bir yöntemi olan **birimleri**, bir birim seçin, sağ tıklatarak bağlam menüsü çağırma ve seçmek için **kopya**.</span><span class="sxs-lookup"><span data-stu-id="caccc-127">An alternative method to initiate clone is to go to **Volumes**, select a volume, then right-click to invoke the context menu and select **Clone**.</span></span>

<span data-ttu-id="caccc-128">Yedekleme Kataloğu'ndan biriminiz bir kopyasını oluşturmak için aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="caccc-128">Perform the following steps to create a clone of your volume from the backup catalog.</span></span>

#### <a name="to-clone-a-volume"></a><span data-ttu-id="caccc-129">Birim kopyalama</span><span class="sxs-lookup"><span data-stu-id="caccc-129">To clone a volume</span></span>

1. <span data-ttu-id="caccc-130">StorSimple cihaz Yöneticisi hizmetinize gidin ve ardından **yedekleme kataloğu**.</span><span class="sxs-lookup"><span data-stu-id="caccc-130">Go to your StorSimple Device Manager service and then click **Backup catalog**.</span></span>

2. <span data-ttu-id="caccc-131">Bir yedekleme kümesi aşağıdaki gibi seçin:</span><span class="sxs-lookup"><span data-stu-id="caccc-131">Select a backup set as follows:</span></span>
   
   1. <span data-ttu-id="caccc-132">Uygun cihazı seçin.</span><span class="sxs-lookup"><span data-stu-id="caccc-132">Select the appropriate device.</span></span>
   2. <span data-ttu-id="caccc-133">Aşağı açılan listesinde, seçmek istediğiniz yedekleme için birim veya yedekleme ilkesini seçin.</span><span class="sxs-lookup"><span data-stu-id="caccc-133">In the drop-down list, choose the volume or backup policy for the backup that you wish to select.</span></span>
   3. <span data-ttu-id="caccc-134">Zaman aralığı belirtin.</span><span class="sxs-lookup"><span data-stu-id="caccc-134">Specify the time range.</span></span>
   4. <span data-ttu-id="caccc-135">Tıklatın **Uygula** bu sorguyu yürütmek için.</span><span class="sxs-lookup"><span data-stu-id="caccc-135">Click **Apply** to execute this query.</span></span>

    <span data-ttu-id="caccc-136">Yedekleme seçili birimle ilişkilendirilen veya yedekleme İlkesi yedekleme kümelerini listesinde görüntülenmelidir.</span><span class="sxs-lookup"><span data-stu-id="caccc-136">The backups associated with the selected volume or backup policy should appear in the list of backup sets.</span></span>
   
    ![Yedekleme kümesi listesi](./media/storsimple-8000-clone-volume-u2/bucatalog.png)
     
3. <span data-ttu-id="caccc-138">İlişkili birimleri görüntülemek için yedekleme kümesini genişletin.</span><span class="sxs-lookup"><span data-stu-id="caccc-138">Expand the backup set to view the associated volumes.</span></span> <span data-ttu-id="caccc-139">Geri yüklemeden önce bu birimleri ana bilgisayar ve aygıt çevrimdışına alınması gerekir.</span><span class="sxs-lookup"><span data-stu-id="caccc-139">These volumes must be taken offline on the host and device before you can restore them.</span></span> <span data-ttu-id="caccc-140">Birimleri erişimi **birimleri** Cihazınızı dikey ve adımları izleyin [bir birim çevrimdışına](storsimple-8000-manage-volumes-u2.md#take-a-volume-offline) çevrimdışı duruma getirmek için.</span><span class="sxs-lookup"><span data-stu-id="caccc-140">Access the volumes on the **Volumes** blade of your device, and then follow the steps in [Take a volume offline](storsimple-8000-manage-volumes-u2.md#take-a-volume-offline) to take them offline.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="caccc-141">Çevrimdışı birimler cihazda olabilmesi birimlerde çevrimdışı konak ilk olarak, gerçekleştirdiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="caccc-141">Make sure that you have taken the volumes offline on the host first, before you take the volumes offline on the device.</span></span> <span data-ttu-id="caccc-142">Konakta birimler çevrimdışı almazsanız, olası veri bozulmasına yol açabilir.</span><span class="sxs-lookup"><span data-stu-id="caccc-142">If you do not take the volumes offline on the host, it could potentially lead to data corruption.</span></span>
   
4. <span data-ttu-id="caccc-143">Geri gidin **yedekleme kataloğu** ve yedekleme kümesinde bir birim seçin.</span><span class="sxs-lookup"><span data-stu-id="caccc-143">Navigate back to the **Backup catalog** and select a volume in a backup set.</span></span> <span data-ttu-id="caccc-144">Sağ tıklayın ve ardından bağlam menüsünden seçin **kopya**.</span><span class="sxs-lookup"><span data-stu-id="caccc-144">Right-click and then from the context menu, select **Clone**.</span></span>

   ![Yedekleme kümesi listesi](./media/storsimple-8000-clone-volume-u2/clonevol3b.png) 

3. <span data-ttu-id="caccc-146">İçinde **kopya** dikey penceresinde, aşağıdaki adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="caccc-146">In the **Clone** blade, do the following steps:</span></span>
   
    1. <span data-ttu-id="caccc-147">Bir hedef cihaz tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="caccc-147">Identify a target device.</span></span> <span data-ttu-id="caccc-148">Bu, kopyanın oluşturulacağı konumdur.</span><span class="sxs-lookup"><span data-stu-id="caccc-148">This is the location where the clone will be created.</span></span> <span data-ttu-id="caccc-149">Aynı aygıt seçin veya başka bir aygıt belirtin.</span><span class="sxs-lookup"><span data-stu-id="caccc-149">You can choose the same device or specify another device.</span></span>

      > [!NOTE]
      > <span data-ttu-id="caccc-150">Kopya için gereken kapasiteyi hedef cihazda kullanılabilir kapasiteden daha düşük olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="caccc-150">Make sure that the capacity required for the clone is lower than the capacity available on the target device.</span></span>
       
    2. <span data-ttu-id="caccc-151">Kopya için benzersiz birim adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="caccc-151">Specify a unique volume name for your clone.</span></span> <span data-ttu-id="caccc-152">Adı 3 ile 127 karakter içermelidir.</span><span class="sxs-lookup"><span data-stu-id="caccc-152">The name must contain between 3 and 127 characters.</span></span>
      
        > [!NOTE]
        > <span data-ttu-id="caccc-153">**Kopya birim olarak** alan **katmanlı** yerel olarak sabitlenmiş bir birim kopyalama olsa bile.</span><span class="sxs-lookup"><span data-stu-id="caccc-153">The **Clone Volume As** field will be **Tiered** even if you are cloning a locally pinned volume.</span></span> <span data-ttu-id="caccc-154">Bu ayarı değiştiremezsiniz; Ancak, yerel olarak da sabitlenmelidir kopyalanan birimi gerekiyorsa, kopya yerel olarak sabitlenmiş bir birim dönüştürebilir, kopya başarıyla oluşturduktan sonra.</span><span class="sxs-lookup"><span data-stu-id="caccc-154">You cannot change this setting; however, if you need the cloned volume to be locally pinned as well, you can convert the clone to a locally pinned volume after you successfully create the clone.</span></span> <span data-ttu-id="caccc-155">Yerel olarak sabitlenmiş bir birim için katmanlı birim dönüştürme hakkında daha fazla bilgi için Git [birim türünü değiştirme](storsimple-8000-manage-volumes-u2.md#change-the-volume-type).</span><span class="sxs-lookup"><span data-stu-id="caccc-155">For information about converting a tiered volume to a locally pinned volume, go to [Change the volume type](storsimple-8000-manage-volumes-u2.md#change-the-volume-type).</span></span>
          
    3. <span data-ttu-id="caccc-156">Altında **bağlı Konaklar**, kopya için bir erişim denetimi kaydı (ACR) belirtin.</span><span class="sxs-lookup"><span data-stu-id="caccc-156">Under **Connected hosts**, specify an access control record (ACR) for the clone.</span></span> <span data-ttu-id="caccc-157">Yeni bir ACR ekleyebilir veya var olan listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="caccc-157">You can add a new ACR or choose from the existing list.</span></span> <span data-ttu-id="caccc-158">ACR hangi ana bilgisayarların bu kopya erişebilirsiniz belirler.</span><span class="sxs-lookup"><span data-stu-id="caccc-158">The ACR will determine which hosts can access this clone.</span></span>
      
        ![Yedekleme kümesi listesi](./media/storsimple-8000-clone-volume-u2/clonevol3a.png) 

    4. <span data-ttu-id="caccc-160">Tıklatın **kopya** işlem tamamlanamadı.</span><span class="sxs-lookup"><span data-stu-id="caccc-160">Click **Clone** to complete the operation.</span></span>

4. <span data-ttu-id="caccc-161">Bir kopya iş başlatılır ve kopya başarıyla oluşturulduğunda size bildirilir.</span><span class="sxs-lookup"><span data-stu-id="caccc-161">A clone job is initiated and you are notified when the clone is successfully created.</span></span> <span data-ttu-id="caccc-162">İş bildirimi tıklatın veya gitmek **işleri** kopya işi izlemek için dikey penceresini.</span><span class="sxs-lookup"><span data-stu-id="caccc-162">Click the job notification or go to **Jobs** blade to monitor the clone job.</span></span>

    ![Yedekleme kümesi listesi](./media/storsimple-8000-clone-volume-u2/clonevol5.png)

7. <span data-ttu-id="caccc-164">Kopya işi tamamlandıktan sonra aygıtınıza gidin ve ardından **birimleri**.</span><span class="sxs-lookup"><span data-stu-id="caccc-164">After the clone job is complete, go to your device and then click **Volumes**.</span></span> <span data-ttu-id="caccc-165">Birimleri listesinde, yeni kaynak biriminin aynı birim kapsayıcısı oluşturuldu kopya görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="caccc-165">In the list of volumes, you should see the clone that was just created in the same volume container that has the source volume.</span></span>

    ![Yedekleme kümesi listesi](./media/storsimple-8000-clone-volume-u2/clonevol6.png)

<span data-ttu-id="caccc-167">Bu yolla oluşturulan bir kopya geçici kopya ' dir.</span><span class="sxs-lookup"><span data-stu-id="caccc-167">A clone that is created this way is a transient clone.</span></span> <span data-ttu-id="caccc-168">Kopya türleri hakkında daha fazla bilgi için bkz: [geçici ve kalıcı klonlar](#transient-vs-permanent-clones).</span><span class="sxs-lookup"><span data-stu-id="caccc-168">For more information about clone types, see [Transient vs. permanent clones](#transient-vs-permanent-clones).</span></span>


## <a name="transient-vs-permanent-clones"></a><span data-ttu-id="caccc-169">Geçici ve kalıcı klonlar karşılaştırması</span><span class="sxs-lookup"><span data-stu-id="caccc-169">Transient vs. permanent clones</span></span>
<span data-ttu-id="caccc-170">Yalnızca başka bir cihaza kopyaladığınızda geçici klonlar oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="caccc-170">Transient clones are created only when you clone to another device.</span></span> <span data-ttu-id="caccc-171">Bir yedekleme kümesi için farklı bir cihaz StorSimple cihaz Yöneticisi tarafından yönetilen belirli bir birimden kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="caccc-171">You can clone a specific volume from a backup set to a different device managed by the StorSimple Device Manager.</span></span> <span data-ttu-id="caccc-172">Geçici kopya özgün birimin verilere başvuru vardır ve okuma ve yerel olarak hedef cihazda yazmak için bu verileri kullanır.</span><span class="sxs-lookup"><span data-stu-id="caccc-172">The transient clone has references to the data in the original volume and uses that data to read and write locally on the target device.</span></span>

<span data-ttu-id="caccc-173">Bir geçici kopya bir bulut anlık görüntüsünü sonra sonuçta elde edilen kopya olan bir *kalıcı* kopya.</span><span class="sxs-lookup"><span data-stu-id="caccc-173">After you take a cloud snapshot of a transient clone, the resulting clone is a *permanent* clone.</span></span> <span data-ttu-id="caccc-174">Bu işlem sırasında verilerin bir kopyasını Bulutu üzerinde oluşturulur ve bu verileri kopyalamak için saat veri ve (bir Azure Azure kopyalama budur) Azure gecikmeleri boyutu tarafından belirlenir.</span><span class="sxs-lookup"><span data-stu-id="caccc-174">During this process, a copy of the data is created on the cloud and the time to copy this data is determined by the size of the data and the Azure latencies (this is an Azure-to-Azure copy).</span></span> <span data-ttu-id="caccc-175">Bu işlem için hafta gün sürebilir.</span><span class="sxs-lookup"><span data-stu-id="caccc-175">This process can take days to weeks.</span></span> <span data-ttu-id="caccc-176">Geçici kopya kalıcı bir kopya olur ve tüm başvuruları gelen kopyalandı özgün birimin verilere sahip değil.</span><span class="sxs-lookup"><span data-stu-id="caccc-176">The transient clone becomes a permanent clone and doesn’t have any references to the original volume data that it was cloned from.</span></span>

## <a name="scenarios-for-transient-and-permanent-clones"></a><span data-ttu-id="caccc-177">Geçici ve kalıcı klonlar senaryoları</span><span class="sxs-lookup"><span data-stu-id="caccc-177">Scenarios for transient and permanent clones</span></span>
<span data-ttu-id="caccc-178">Aşağıdaki bölümlerde geçici ve kalıcı klonlar kullanılabilir örnek durumlar açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="caccc-178">The following sections describe example situations in which transient and permanent clones can be used.</span></span>

### <a name="item-level-recovery-with-a-transient-clone"></a><span data-ttu-id="caccc-179">Geçici bir kopya ile öğe düzeyinde kurtarma</span><span class="sxs-lookup"><span data-stu-id="caccc-179">Item-level recovery with a transient clone</span></span>
<span data-ttu-id="caccc-180">Bir yıl eski Microsoft PowerPoint sunusu dosyası kurtarmak gerekir.</span><span class="sxs-lookup"><span data-stu-id="caccc-180">You need to recover a one-year-old Microsoft PowerPoint presentation file.</span></span> <span data-ttu-id="caccc-181">BT yöneticiniz bu süre belirli yedekten tanımlar ve birim filtreler.</span><span class="sxs-lookup"><span data-stu-id="caccc-181">Your IT administrator identifies the specific backup from that time, and then filters the volume.</span></span> <span data-ttu-id="caccc-182">Yönetici daha sonra birim klonlar, aradığınız dosya bulur ve olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="caccc-182">The administrator then clones the volume, locates the file that you are looking for, and provides it to you.</span></span> <span data-ttu-id="caccc-183">Bu senaryoda, bir geçici kopya kullanılır.</span><span class="sxs-lookup"><span data-stu-id="caccc-183">In this scenario, a transient clone is used.</span></span>

### <a name="testing-in-the-production-environment-with-a-permanent-clone"></a><span data-ttu-id="caccc-184">Kalıcı bir kopya ile üretim ortamında test etme</span><span class="sxs-lookup"><span data-stu-id="caccc-184">Testing in the production environment with a permanent clone</span></span>
<span data-ttu-id="caccc-185">Üretim ortamında test hata doğrulamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="caccc-185">You need to verify a testing bug in the production environment.</span></span> <span data-ttu-id="caccc-186">Üretim ortamında birimin bir kopyasını oluşturun ve sonra bu kopya bağımsız kopyalanan birim oluşturmak için bir bulut anlık görüntüsünü.</span><span class="sxs-lookup"><span data-stu-id="caccc-186">You create a clone of the volume in the production environment and then take a cloud snapshot of this clone to create an independent cloned volume.</span></span> <span data-ttu-id="caccc-187">Bu senaryoda, kalıcı bir kopya kullanılır.</span><span class="sxs-lookup"><span data-stu-id="caccc-187">In this scenario, a permanent clone is used.</span></span>

## <a name="next-steps"></a><span data-ttu-id="caccc-188">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="caccc-188">Next steps</span></span>
* <span data-ttu-id="caccc-189">Bilgi edinmek için nasıl [bir yedeklemek kümesinden StorSimple birimini geri](storsimple-8000-restore-from-backup-set-u2.md).</span><span class="sxs-lookup"><span data-stu-id="caccc-189">Learn how to [restore a StorSimple volume from a backup set](storsimple-8000-restore-from-backup-set-u2.md).</span></span>
* <span data-ttu-id="caccc-190">Bilgi edinmek için nasıl [StorSimple Cihazınızı yönetmek için StorSimple cihaz Yöneticisi hizmetini kullanma](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="caccc-190">Learn how to [use the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

