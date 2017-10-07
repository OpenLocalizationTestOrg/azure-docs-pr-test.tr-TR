---
title: "aaaInstall güncelleştirme 0,6 StorSimple sanal dizisindeki | Microsoft Docs"
description: "Azure portal ve düzeltme yöntemi toouse hello StorSimple sanal dizinin web kullanıcı Arabirimi tooapply güncelleştirmeleri kullanarak nasıl hello açıklar"
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
ms.date: 05/18/2017
ms.author: alkohli
ms.openlocfilehash: 2ccd1b5fc1957c35ebec35aa947d331b3ff05464
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-06-on-your-storsimple-virtual-array"></a><span data-ttu-id="cc6f6-103">StorSimple sanal dizinizi üzerinde güncelleştirme 0,6 yükleyin</span><span class="sxs-lookup"><span data-stu-id="cc6f6-103">Install Update 0.6 on your StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="cc6f6-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="cc6f6-104">Overview</span></span>

<span data-ttu-id="cc6f6-105">Bu makalede, StorSimple sanal dizisindeki hello yerel web kullanıcı Arabirimi aracılığıyla ve hello Azure portal aracılığıyla hello adımları gerekli tooinstall güncelleştirme 0,6 açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="cc6f6-105">This article describes hello steps required tooinstall Update 0.6 on your StorSimple Virtual Array via hello local web UI and via hello Azure portal.</span></span> <span data-ttu-id="cc6f6-106">StorSimple sanal dizinizi güncel hello yazılım güncelleştirmeleri veya düzeltmeleri tookeep uygulayın.</span><span class="sxs-lookup"><span data-stu-id="cc6f6-106">You apply hello software updates or hotfixes tookeep your StorSimple Virtual Array up-to-date.</span></span>

<span data-ttu-id="cc6f6-107">Bir güncelleştirmeyi uygulamadan önce hello birimlerinin almak veya paylaşımlarında çevrimdışı hello ilk ana bilgisayar ve aygıt hello öneririz.</span><span class="sxs-lookup"><span data-stu-id="cc6f6-107">Before you apply an update, we recommend that you take hello volumes or shares offline on hello host first and then hello device.</span></span> <span data-ttu-id="cc6f6-108">Bu veri bozulması olasılığını en aza indirir.</span><span class="sxs-lookup"><span data-stu-id="cc6f6-108">This minimizes any possibility of data corruption.</span></span> <span data-ttu-id="cc6f6-109">Merhaba birimler veya paylaşımlar çevrimdışı olduktan sonra aynı zamanda el ile Merhaba aygıtına yedekleme almalıdır.</span><span class="sxs-lookup"><span data-stu-id="cc6f6-109">After hello volumes or shares are offline, you should also take a manual backup of hello device.</span></span>

> [!IMPORTANT]
> - <span data-ttu-id="cc6f6-110">Güncelleştirme 0,6 karşılık gelen çok**10.0.10293.0** Cihazınızda yazılımı sürümü.</span><span class="sxs-lookup"><span data-stu-id="cc6f6-110">Update 0.6 corresponds too**10.0.10293.0** software version on your device.</span></span> <span data-ttu-id="cc6f6-111">Bu güncelleştirmede yenilikler hakkında daha fazla bilgi için çok gidin[0,6 güncelleştirmesi sürüm notları](storsimple-virtual-array-update-06-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="cc6f6-111">For information on what is new in this update, go too[Release notes for Update 0.6](storsimple-virtual-array-update-06-release-notes.md).</span></span>
>
> - <span data-ttu-id="cc6f6-112">Daha sonra öneririz veya güncelleştirme 0.2 çalıştırıyorsanız hello Azure portal aracılığıyla hello güncelleştirmeleri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="cc6f6-112">If you are running Update 0.2 or later, we recommend that you install hello updates via hello Azure portal.</span></span> <span data-ttu-id="cc6f6-113">Güncelleştirme 0.1 veya GA yazılım sürümleri çalıştırıyorsanız, hello düzeltme hello yerel web kullanıcı Arabirimi tooinstall güncelleştirme 0,6 yöntemiyle kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="cc6f6-113">If you are running Update 0.1 or GA software versions, you must use hello hotfix method via hello local web UI tooinstall Update 0.6.</span></span>
>
> - <span data-ttu-id="cc6f6-114">Bir güncelleştirme veya düzeltme yükleme, aygıt yeniden unutmayın.</span><span class="sxs-lookup"><span data-stu-id="cc6f6-114">Keep in mind that installing an update or hotfix restarts your device.</span></span> <span data-ttu-id="cc6f6-115">Verilen Hello StorSimple sanal dizinin bir tek düğümlü aygıt olduğundan, devam eden tüm g/ç kesintiye ve kapalı kalma süresi Cihazınızı karşılaştığında.</span><span class="sxs-lookup"><span data-stu-id="cc6f6-115">Given that hello StorSimple Virtual Array is a single node device, any I/O in progress is disrupted and your device experiences downtime.</span></span>

## <a name="use-hello-azure-portal"></a><span data-ttu-id="cc6f6-116">Hello Azure portalını kullanın</span><span class="sxs-lookup"><span data-stu-id="cc6f6-116">Use hello Azure portal</span></span>

<span data-ttu-id="cc6f6-117">Güncelleştirme 0.2 ve sonraki sürümleri çalışıyorsa hello Azure portal aracılığıyla güncelleştirmeleri yüklemenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="cc6f6-117">If running Update 0.2 and later, we recommend that you install updates through hello Azure portal.</span></span> <span data-ttu-id="cc6f6-118">Merhaba kullanıcı tooscan Hello portal yordamı gerektirir, indirin ve ardından hello güncelleştirmeleri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="cc6f6-118">hello portal procedure requires hello user tooscan, download, and then install hello updates.</span></span> <span data-ttu-id="cc6f6-119">Bu yordamı yaklaşık 7 dakika toocomplete alır.</span><span class="sxs-lookup"><span data-stu-id="cc6f6-119">This procedure takes around 7 minutes toocomplete.</span></span> <span data-ttu-id="cc6f6-120">Hello aşağıdaki gerçekleştirme adımları tooinstall hello güncelleştirme veya düzeltme.</span><span class="sxs-lookup"><span data-stu-id="cc6f6-120">Perform hello following steps tooinstall hello update or hotfix.</span></span>

[!INCLUDE [storsimple-virtual-array-install-update-via-portal](../../includes/storsimple-virtual-array-install-update-via-portal-04.md)]

<span data-ttu-id="cc6f6-121">Merhaba sonra tam, Git tooyour StorSimple cihaz Yöneticisi hizmeti bir yüklemedir.</span><span class="sxs-lookup"><span data-stu-id="cc6f6-121">After hello installation is complete, go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="cc6f6-122">Seçin **aygıtları** seçin ve güncelleştirdiğiniz hello cihaz seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="cc6f6-122">Select **Devices** and then select and click hello device you just updated.</span></span> <span data-ttu-id="cc6f6-123">Çok Git**ayarlar > Yönet > aygıt güncelleştirmeleri**.</span><span class="sxs-lookup"><span data-stu-id="cc6f6-123">Go too**Settings > Manage > Device Updates**.</span></span> <span data-ttu-id="cc6f6-124">Görüntülenen hello yazılım sürüm olmalıdır **10.0.10293.0**.</span><span class="sxs-lookup"><span data-stu-id="cc6f6-124">hello displayed software version should be **10.0.10293.0**.</span></span>

## <a name="use-hello-local-web-ui"></a><span data-ttu-id="cc6f6-125">Merhaba yerel web kullanıcı arabirimini kullanın</span><span class="sxs-lookup"><span data-stu-id="cc6f6-125">Use hello local web UI</span></span>

<span data-ttu-id="cc6f6-126">Merhaba yerel web kullanıcı arabirimini kullanırken iki adımı vardır:</span><span class="sxs-lookup"><span data-stu-id="cc6f6-126">There are two steps when using hello local web UI:</span></span>

* <span data-ttu-id="cc6f6-127">Merhaba update veya hello düzeltmeyi yükleyin</span><span class="sxs-lookup"><span data-stu-id="cc6f6-127">Download hello update or hello hotfix</span></span>
* <span data-ttu-id="cc6f6-128">Merhaba güncelleştirme veya hello düzeltmeyi yükleyin</span><span class="sxs-lookup"><span data-stu-id="cc6f6-128">Install hello update or hello hotfix</span></span>

### <a name="download-hello-update-or-hello-hotfix"></a><span data-ttu-id="cc6f6-129">Merhaba update veya hello düzeltmeyi yükleyin</span><span class="sxs-lookup"><span data-stu-id="cc6f6-129">Download hello update or hello hotfix</span></span>

<span data-ttu-id="cc6f6-130">Hello Microsoft Update Kataloğu ' adımları toodownload hello yazılım güncelleştirmesi aşağıdaki hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="cc6f6-130">Perform hello following steps toodownload hello software update from hello Microsoft Update Catalog.</span></span>

#### <a name="toodownload-hello-update-or-hello-hotfix"></a><span data-ttu-id="cc6f6-131">toodownload hello güncelleştirme veya hello düzeltme</span><span class="sxs-lookup"><span data-stu-id="cc6f6-131">toodownload hello update or hello hotfix</span></span>

1. <span data-ttu-id="cc6f6-132">Internet Explorer'ı başlatın ve çok gidin[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="cc6f6-132">Start Internet Explorer and navigate too[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>

2. <span data-ttu-id="cc6f6-133">Merhaba Microsoft Update Kataloğu hello için bu bilgisayarda ilk kez kullanıyorsanız **yükleme** zaman istendiğinde tooinstall hello Microsoft Update Kataloğu eklentisi.</span><span class="sxs-lookup"><span data-stu-id="cc6f6-133">If you are using hello Microsoft Update Catalog for hello first time on this computer, click **Install** when prompted tooinstall hello Microsoft Update Catalog add-on.</span></span>

3. <span data-ttu-id="cc6f6-134">Merhaba arama kutusuna hello Microsoft Update Kataloğu hello Bilgi Bankası (KB) numarasını girin hello düzeltme toodownload istiyor.</span><span class="sxs-lookup"><span data-stu-id="cc6f6-134">In hello search box of hello Microsoft Update Catalog, enter hello Knowledge Base (KB) number of hello hotfix you want toodownload.</span></span> <span data-ttu-id="cc6f6-135">Girin **4023268** 0,6 güncelleştirmesi için ve ardından **arama**.</span><span class="sxs-lookup"><span data-stu-id="cc6f6-135">Enter **4023268** for Update 0.6, and then click **Search**.</span></span>
   
    <span data-ttu-id="cc6f6-136">Merhaba düzeltme listesi, örneğin, göründüğünde **StorSimple sanal dizinin güncelleştirme 0,6**.</span><span class="sxs-lookup"><span data-stu-id="cc6f6-136">hello hotfix listing appears, for example, **StorSimple Virtual Array Update 0.6**.</span></span>
   
    ![Katalogda arama](./media/storsimple-virtual-array-install-update-06/download1.png)

4. <span data-ttu-id="cc6f6-138">**İndir**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="cc6f6-138">Click **Download**.</span></span>

5. <span data-ttu-id="cc6f6-139">Beş dosyaları toodownload görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="cc6f6-139">You should see five files toodownload.</span></span> <span data-ttu-id="cc6f6-140">Her bu dosyaları tooa klasörünün indirin.</span><span class="sxs-lookup"><span data-stu-id="cc6f6-140">Download each of those files tooa folder.</span></span> <span data-ttu-id="cc6f6-141">Merhaba klasör de hello aygıttan ulaşılabilir kopyalanan tooa ağ paylaşımı olabilir.</span><span class="sxs-lookup"><span data-stu-id="cc6f6-141">hello folder can also be copied tooa network share that is reachable from hello device.</span></span>

6. <span data-ttu-id="cc6f6-142">Merhaba dosyalarının bulunduğu hello klasörünü açın.</span><span class="sxs-lookup"><span data-stu-id="cc6f6-142">Open hello folder where hello files are located.</span></span>
    <span data-ttu-id="cc6f6-143">![Merhaba paket dosyaları](./media/storsimple-virtual-array-install-update-06/update06folder.png)</span><span class="sxs-lookup"><span data-stu-id="cc6f6-143">![Files in hello package](./media/storsimple-virtual-array-install-update-06/update06folder.png)</span></span>

    <span data-ttu-id="cc6f6-144">Görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="cc6f6-144">You see:</span></span>
    -  <span data-ttu-id="cc6f6-145">Microsoft Update tek başına paket dosyası `WindowsTH-KB3011067-x64`.</span><span class="sxs-lookup"><span data-stu-id="cc6f6-145">A Microsoft Update Standalone Package file `WindowsTH-KB3011067-x64`.</span></span> <span data-ttu-id="cc6f6-146">Bu dosya kullanılan tooupdate hello aygıt yazılımdır.</span><span class="sxs-lookup"><span data-stu-id="cc6f6-146">This file is used tooupdate hello device software.</span></span>
    - <span data-ttu-id="cc6f6-147">Geneva İzleme Aracısı paket dosyası `GenevaMonitoringAgentPackageInstaller`.</span><span class="sxs-lookup"><span data-stu-id="cc6f6-147">A Geneva Monitoring Agent Package file `GenevaMonitoringAgentPackageInstaller`.</span></span> <span data-ttu-id="cc6f6-148">Kullanılan tooupdate hello izleme ve Tanılama Hizmeti (MDS) aracısı dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="cc6f6-148">This file is used tooupdate hello Monitoring and Diagnostics service (MDS) agent.</span></span> <span data-ttu-id="cc6f6-149">Merhaba cab dosyasını çift tıklatın.</span><span class="sxs-lookup"><span data-stu-id="cc6f6-149">Double-click hello cab file.</span></span> <span data-ttu-id="cc6f6-150">A _.msi_ görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="cc6f6-150">A _.msi_ is displayed.</span></span> <span data-ttu-id="cc6f6-151">Select hello dosyasını sağ tıklatın ve ardından **ayıklamak** hello dosya.</span><span class="sxs-lookup"><span data-stu-id="cc6f6-151">Select hello file, right-click, and then **Extract** hello file.</span></span> <span data-ttu-id="cc6f6-152">Merhaba kullandığınız _.msi_ dosya tooupdate hello Aracısı.</span><span class="sxs-lookup"><span data-stu-id="cc6f6-152">You use hello _.msi_ file tooupdate hello agent.</span></span>

        ![MDS aracı güncelleştirme dosyasını ayıklayın](./media/storsimple-virtual-array-install-update-06/extract-geneva-monitoring-agent-installer.png)

        > [!IMPORTANT]
        > <span data-ttu-id="cc6f6-154">StorSimple güncelleştirme 0,5 (0.0.10293.0) çalıştırıyorsanız, tooupdate hello MDS Aracısı gerekmez.</span><span class="sxs-lookup"><span data-stu-id="cc6f6-154">You do not need tooupdate hello MDS agent if you are running StorSimple Update 0.5 (0.0.10293.0).</span></span>

    - <span data-ttu-id="cc6f6-155">Kritik Windows Güvenlik güncelleştirmeleri içeren üç dosyaları `windows8.1-kb4012213-x64`,`windows8.1-kb3205400-x64`, ve `windows8.1-kb4019213-x64`.</span><span class="sxs-lookup"><span data-stu-id="cc6f6-155">Three files that contain critical Windows security updates, `windows8.1-kb4012213-x64`,`windows8.1-kb3205400-x64`, and `windows8.1-kb4019213-x64`.</span></span>


### <a name="install-hello-update-or-hello-hotfix"></a><span data-ttu-id="cc6f6-156">Merhaba güncelleştirme veya hello düzeltmeyi yükleyin</span><span class="sxs-lookup"><span data-stu-id="cc6f6-156">Install hello update or hello hotfix</span></span>

<span data-ttu-id="cc6f6-157">Önceki toohello güncelleştirme veya düzeltme yükleme, bir ağ paylaşımı üzerinden erişilebilir veya hello güncelleştirmeye sahip veya hello düzeltmeyi indirdiğiniz, ana bilgisayarda yerel olarak ya da emin olun.</span><span class="sxs-lookup"><span data-stu-id="cc6f6-157">Prior toohello update or hotfix installation, make sure that you have hello update or hello hotfix downloaded either locally on your host or accessible via a network share.</span></span>

<span data-ttu-id="cc6f6-158">Bu yöntem tooinstall güncelleştirmeleri GA çalıştıran bir cihazda kullanmayı veya 0,1 yazılım sürümleri güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="cc6f6-158">Use this method tooinstall updates on a device running GA or Update 0.1 software versions.</span></span> <span data-ttu-id="cc6f6-159">Bu yordam, yaklaşık olarak 12 dakika toocomplete alır.</span><span class="sxs-lookup"><span data-stu-id="cc6f6-159">This procedure takes approximately 12 minutes toocomplete.</span></span> <span data-ttu-id="cc6f6-160">Hello aşağıdaki gerçekleştirme adımları tooinstall hello güncelleştirme veya düzeltme.</span><span class="sxs-lookup"><span data-stu-id="cc6f6-160">Perform hello following steps tooinstall hello update or hotfix.</span></span>

#### <a name="tooinstall-hello-update-or-hello-hotfix"></a><span data-ttu-id="cc6f6-161">tooinstall hello güncelleştirme veya hello düzeltme</span><span class="sxs-lookup"><span data-stu-id="cc6f6-161">tooinstall hello update or hello hotfix</span></span>

1. <span data-ttu-id="cc6f6-162">Merhaba yerel web kullanıcı Arabirimi, çok Git**Bakım** > **yazılım güncelleştirmesi**.</span><span class="sxs-lookup"><span data-stu-id="cc6f6-162">In hello local web UI, go too**Maintenance** > **Software Update**.</span></span> <span data-ttu-id="cc6f6-163">Çalıştırmakta olduğunuz hello yazılım sürümü not edin.</span><span class="sxs-lookup"><span data-stu-id="cc6f6-163">Make a note of hello software version that you are running.</span></span> <span data-ttu-id="cc6f6-164">Çalıştırıyorsanız, **10.0.10290.0**, adım 6 tooupdate hello MDS Aracısı gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="cc6f6-164">If you are running **10.0.10290.0**, you do not need tooupdate hello MDS agent in step 6.</span></span>
   
    ![cihaz güncelleştirme](./media/storsimple-virtual-array-install-update-05/update1m.png)

2. <span data-ttu-id="cc6f6-166">İçinde **güncelleştirme dosya yolu**, hello güncelleştirmesi hello dosya adı girin veya düzeltme hello.</span><span class="sxs-lookup"><span data-stu-id="cc6f6-166">In **Update file path**, enter hello file name for hello update or hello hotfix.</span></span> <span data-ttu-id="cc6f6-167">Ayrıca, bir ağ paylaşımında girdiyseniz toohello güncelleştirme veya düzeltme yükleme dosyası göz atabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cc6f6-167">You can also browse toohello update or hotfix installation file if placed on a network share.</span></span> <span data-ttu-id="cc6f6-168">**Uygula**'ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="cc6f6-168">Click **Apply**.</span></span>
   
    ![cihaz güncelleştirme](./media/storsimple-virtual-array-install-update-05/update2m.png)

3. <span data-ttu-id="cc6f6-170">Bir uyarı görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="cc6f6-170">A warning is displayed.</span></span> <span data-ttu-id="cc6f6-171">Hello sanal bir tek düğümlü aygıt hello güncelleştirme uygulanana, hello aygıt yeniden başladıktan sonra kapalı kalma süresi dizisidir.</span><span class="sxs-lookup"><span data-stu-id="cc6f6-171">Given hello virtual array is a single node device, after hello update is applied, hello device restarts and there is downtime.</span></span> <span data-ttu-id="cc6f6-172">Merhaba onay simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="cc6f6-172">Click hello check icon.</span></span>
   
   ![cihaz güncelleştirme](./media/storsimple-virtual-array-install-update-05/update3m.png)

4. <span data-ttu-id="cc6f6-174">Merhaba güncelleştirme başlatır.</span><span class="sxs-lookup"><span data-stu-id="cc6f6-174">hello update starts.</span></span> <span data-ttu-id="cc6f6-175">Merhaba cihaz başarıyla güncelleştirildikten sonra yeniden başlatır.</span><span class="sxs-lookup"><span data-stu-id="cc6f6-175">After hello device is successfully updated, it restarts.</span></span> <span data-ttu-id="cc6f6-176">Merhaba yerel UI bu süre içinde erişilebilir durumda değil.</span><span class="sxs-lookup"><span data-stu-id="cc6f6-176">hello local UI is not accessible in this duration.</span></span>
   
    ![cihaz güncelleştirme](./media/storsimple-virtual-array-install-update-05/update5m.png)

5. <span data-ttu-id="cc6f6-178">Merhaba yeniden başlatma tamamlandıktan sonra toohello gerçekleştirilen **oturum** sayfası.</span><span class="sxs-lookup"><span data-stu-id="cc6f6-178">After hello restart is complete, you are taken toohello **Sign in** page.</span></span> <span data-ttu-id="cc6f6-179">Merhaba aygıt yazılımı güncelleştirdi, hello yerel web kullanıcı Arabirimi, tooverify Git çok**Bakım** > **yazılım güncelleştirmesi**.</span><span class="sxs-lookup"><span data-stu-id="cc6f6-179">tooverify that hello device software has updated, in hello local web UI, go too**Maintenance** > **Software Update**.</span></span> <span data-ttu-id="cc6f6-180">Görüntülenen hello yazılım sürüm olmalıdır **10.0.0.0.0.10293** 0,6 güncelleştirmesi.</span><span class="sxs-lookup"><span data-stu-id="cc6f6-180">hello displayed software version should be **10.0.0.0.0.10293** for Update 0.6.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="cc6f6-181">Biz hello yerel web kullanıcı Arabirimi biraz farklı bir yolla hello yazılım sürümleri rapor ve Azure portal hello.</span><span class="sxs-lookup"><span data-stu-id="cc6f6-181">We report hello software versions in a slightly different way in hello local web UI and hello Azure portal.</span></span> <span data-ttu-id="cc6f6-182">Örneğin, yerel web kullanıcı Arabirimi raporları'nı hello **10.0.0.0.0.10293** ve Azure portal raporları hello **10.0.10293.0** hello için aynı sürüm.</span><span class="sxs-lookup"><span data-stu-id="cc6f6-182">For example, hello local web UI reports **10.0.0.0.0.10293** and hello Azure portal reports **10.0.10293.0** for hello same version.</span></span>
   
    ![cihaz güncelleştirme](./media/storsimple-virtual-array-install-update-06/update6m.png)

6. <span data-ttu-id="cc6f6-184">StorSimple sanal dizinin güncelleştirme 0,5 çalışıyormuş bu adımı atla (**10.0.10290.0**) bu güncelleştirmeyi uygulamadan önce.</span><span class="sxs-lookup"><span data-stu-id="cc6f6-184">Skip this step if you were running StorSimple Virtual Array Update 0.5 (**10.0.10290.0**) before you applied this update.</span></span> <span data-ttu-id="cc6f6-185">Tooupdate başlamadan önce 1. adımda not hello yazılım sürümü yaptığınız.</span><span class="sxs-lookup"><span data-stu-id="cc6f6-185">You made a note of hello software version in step 1 before you began tooupdate.</span></span> <span data-ttu-id="cc6f6-186">Güncelleştirme 0,5 çalışıyormuş MDS aracı zaten güncel.</span><span class="sxs-lookup"><span data-stu-id="cc6f6-186">If you were running Update 0.5, your MDS agent is already up-to-date .</span></span>

    <span data-ttu-id="cc6f6-187">Bir yazılım sürüm önceki tooUpdate 0,5 çalıştırıyorsanız, hello sonraki adımda, tooupdate hello MDS aracısıdır.</span><span class="sxs-lookup"><span data-stu-id="cc6f6-187">If you are running a software version prior tooUpdate 0.5, hello next step for you is tooupdate hello MDS agent.</span></span> <span data-ttu-id="cc6f6-188">Merhaba, **yazılım güncelleştirmesi** sayfasında, Git toohello **güncelleştirme dosya yolu** ve toohello Gözat `GenevaMonitoringAgentPackageInstaller.msi` dosya.</span><span class="sxs-lookup"><span data-stu-id="cc6f6-188">In hello **Software Update** page, go toohello **Update file path** and browse toohello `GenevaMonitoringAgentPackageInstaller.msi` file.</span></span> <span data-ttu-id="cc6f6-189">2-4 arası adımları yineleyin.</span><span class="sxs-lookup"><span data-stu-id="cc6f6-189">Repeat steps 2-4.</span></span> <span data-ttu-id="cc6f6-190">Merhaba sanal dizinin yeniden başlatıldıktan sonra hello yerel web kullanıcı Arabirimi ile oturum açın.</span><span class="sxs-lookup"><span data-stu-id="cc6f6-190">After hello virtual array restarts, sign into hello local web UI.</span></span>

7. <span data-ttu-id="cc6f6-191">2-4 tooinstall hello Windows güvenlik düzeltmelerini dosyalarını kullanarak adımı yineleyin `windows8.1-kb4012213-x64`,`windows8.1-kb3205400-x64`, ve `windows8.1-kb4019213-x64`.</span><span class="sxs-lookup"><span data-stu-id="cc6f6-191">Repeat step 2-4 tooinstall hello Windows security fixes using files `windows8.1-kb4012213-x64`,`windows8.1-kb3205400-x64`, and `windows8.1-kb4019213-x64`.</span></span> <span data-ttu-id="cc6f6-192">Merhaba sanal dizinin her yüklendikten sonra yeniden başlatılır ve hello yerel web kullanıcı Arabirimi toosign gerekir.</span><span class="sxs-lookup"><span data-stu-id="cc6f6-192">hello virtual array restarts after each install and you need toosign into hello local web UI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cc6f6-193">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="cc6f6-193">Next steps</span></span>

<span data-ttu-id="cc6f6-194">Daha fazla bilgi edinmek [StorSimple sanal dizinizi yönetme](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="cc6f6-194">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

