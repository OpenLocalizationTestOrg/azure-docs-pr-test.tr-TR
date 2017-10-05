---
title: "StorSimple anlık görüntü Yöneticisi ile cihazları yönetme | Microsoft Docs"
description: "StorSimple Snapshot Manager MMC ek bileşenini bağlanmak ve StorSimple cihazları yönetmek için nasıl kullanılacağını açıklar."
services: storsimple
documentationcenter: 
author: SharS
manager: timlt
editor: 
ms.assetid: 966ecbe3-a7fa-4752-825f-6694dd949946
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: f5e3186a4271e0be781f367fa75ada195c58c960
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-storsimple-snapshot-manager-to-connect-and-manage-storsimple-devices"></a><span data-ttu-id="3bf8c-103">StorSimple Snapshot Manager bağlanmak ve StorSimple cihazları yönetmek için kullanın</span><span class="sxs-lookup"><span data-stu-id="3bf8c-103">Use StorSimple Snapshot Manager to connect and manage StorSimple devices</span></span>
## <a name="overview"></a><span data-ttu-id="3bf8c-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="3bf8c-104">Overview</span></span>
<span data-ttu-id="3bf8c-105">StorSimple anlık görüntü Yöneticisi'nde düğümlerini kullanabilirsiniz **kapsam** alınan StorSimple cihaz verileri doğrulayın ve bağlı depolama cihazları yenilemek için bölmesi.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-105">You can use nodes in the StorSimple Snapshot Manager **Scope** pane to verify imported StorSimple device data and refresh connected storage devices.</span></span> <span data-ttu-id="3bf8c-106">Ek olarak, tıkladığınızda, **aygıtları** düğümü, bağlı cihazlarınız ve ilgili durum bilgileri listesini görebilirsiniz **sonuçları** bölmesi.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-106">Additionally, when you click the **Devices** node, you can see a list of connected devices and corresponding status information in the **Results** pane.</span></span>

![Bağlı aygıtlar](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_connect_devices.png)

<span data-ttu-id="3bf8c-108">**Şekil 1: Cihaz StorSimple Snapshot Manager bağlı**</span><span class="sxs-lookup"><span data-stu-id="3bf8c-108">**Figure 1: StorSimple Snapshot Manager connected device**</span></span> 

<span data-ttu-id="3bf8c-109">Bağlı olarak, **Görünüm** seçimleri **sonuçları** bölmesinde her bir cihaz hakkında aşağıdaki bilgileri gösterir.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-109">Depending on your **View** selections, the **Results** pane shows the following information about each device.</span></span> <span data-ttu-id="3bf8c-110">(Bir görünüm yapılandırma hakkında daha fazla bilgi için Git [Görünüm menüsünde](storsimple-use-snapshot-manager.md#view-menu).</span><span class="sxs-lookup"><span data-stu-id="3bf8c-110">(For more information about configuring a view, go to [View menu](storsimple-use-snapshot-manager.md#view-menu).</span></span>

| <span data-ttu-id="3bf8c-111">Sonuçları sütun</span><span class="sxs-lookup"><span data-stu-id="3bf8c-111">Results column</span></span> | <span data-ttu-id="3bf8c-112">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3bf8c-112">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="3bf8c-113">Ad</span><span class="sxs-lookup"><span data-stu-id="3bf8c-113">Name</span></span> |<span data-ttu-id="3bf8c-114">Azure Klasik Portalı'nda yapılandırılan aygıt adı</span><span class="sxs-lookup"><span data-stu-id="3bf8c-114">The name of the device as configured in the Azure classic portal</span></span> |
| <span data-ttu-id="3bf8c-115">modeli</span><span class="sxs-lookup"><span data-stu-id="3bf8c-115">Model</span></span> |<span data-ttu-id="3bf8c-116">Cihazın model numarası</span><span class="sxs-lookup"><span data-stu-id="3bf8c-116">The model number of the device</span></span> |
| <span data-ttu-id="3bf8c-117">Sürüm</span><span class="sxs-lookup"><span data-stu-id="3bf8c-117">Version</span></span> |<span data-ttu-id="3bf8c-118">Cihazda yüklü olan yazılım sürümü</span><span class="sxs-lookup"><span data-stu-id="3bf8c-118">The version of the software installed on the device</span></span> |
| <span data-ttu-id="3bf8c-119">Durum</span><span class="sxs-lookup"><span data-stu-id="3bf8c-119">Status</span></span> |<span data-ttu-id="3bf8c-120">Cihazın kullanılabilir olup olmadığı</span><span class="sxs-lookup"><span data-stu-id="3bf8c-120">Whether the device is available</span></span> |
| <span data-ttu-id="3bf8c-121">Son eşitlendi</span><span class="sxs-lookup"><span data-stu-id="3bf8c-121">Last Synced</span></span> |<span data-ttu-id="3bf8c-122">Tarih ve saat aygıt en son ne zaman eşitlendiği</span><span class="sxs-lookup"><span data-stu-id="3bf8c-122">Date and time when the device was last synchronized</span></span> |
| <span data-ttu-id="3bf8c-123">Seri No</span><span class="sxs-lookup"><span data-stu-id="3bf8c-123">Serial No.</span></span> |<span data-ttu-id="3bf8c-124">Cihaz seri numarası</span><span class="sxs-lookup"><span data-stu-id="3bf8c-124">The serial number for the device</span></span> |

<span data-ttu-id="3bf8c-125">Sağ tıklattığınızda, **aygıtları** düğümünde **kapsam** bölmesinde, aşağıdaki eylemler seçebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="3bf8c-125">If you right-click the **Devices** node in the **Scope** pane, you can select from the following actions:</span></span>

* <span data-ttu-id="3bf8c-126">Ekleme veya bir aygıt değiştirme</span><span class="sxs-lookup"><span data-stu-id="3bf8c-126">Add or replace a device</span></span>
* <span data-ttu-id="3bf8c-127">Bir aygıtı bağlayın ve içeri aktarmalar doğrulayın</span><span class="sxs-lookup"><span data-stu-id="3bf8c-127">Connect a device and verify imports</span></span>
* <span data-ttu-id="3bf8c-128">Bağlı aygıtlar Yenile</span><span class="sxs-lookup"><span data-stu-id="3bf8c-128">Refresh connected devices</span></span>

<span data-ttu-id="3bf8c-129">Tıklatırsanız **aygıtları** düğümünü ve ardından sağ tıklayarak bir aygıt adı **sonuçları** bölmesinde, aşağıdaki eylemler seçebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="3bf8c-129">If you click the **Devices** node and then right-click a device name in the **Results** pane, you can select from the following actions:</span></span>

* <span data-ttu-id="3bf8c-130">Bir cihaz kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="3bf8c-130">Authenticate a device</span></span>
* <span data-ttu-id="3bf8c-131">Cihaz ayrıntıları görüntüle</span><span class="sxs-lookup"><span data-stu-id="3bf8c-131">View device details</span></span>
* <span data-ttu-id="3bf8c-132">Bir cihaz yenileme</span><span class="sxs-lookup"><span data-stu-id="3bf8c-132">Refresh a device</span></span>
* <span data-ttu-id="3bf8c-133">Cihaz yapılandırmasını Sil</span><span class="sxs-lookup"><span data-stu-id="3bf8c-133">Delete a device configuration</span></span>
* <span data-ttu-id="3bf8c-134">Aygıt parola değiştirme</span><span class="sxs-lookup"><span data-stu-id="3bf8c-134">Change a device password</span></span>

> [!NOTE]
> <span data-ttu-id="3bf8c-135">Tüm bu eylemleri mevcuttur **Eylemler** bölmesi.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-135">All of these actions are also available in the **Actions** pane.</span></span>


<span data-ttu-id="3bf8c-136">Bu öğretici StorSimple Snapshot Manager bağlanmak ve cihazları yönetmek ve aşağıdaki görevleri gerçekleştirmek için nasıl kullanılacağını açıklamaktadır:</span><span class="sxs-lookup"><span data-stu-id="3bf8c-136">This tutorial explains how to use StorSimple Snapshot Manager to connect and manage devices and perform the following tasks:</span></span>

* <span data-ttu-id="3bf8c-137">Ekleme veya bir aygıt değiştirme</span><span class="sxs-lookup"><span data-stu-id="3bf8c-137">Add or replace a device</span></span>
* <span data-ttu-id="3bf8c-138">Bir aygıtı bağlayın ve içeri aktarmalar doğrulayın</span><span class="sxs-lookup"><span data-stu-id="3bf8c-138">Connect a device and verify imports</span></span>
* <span data-ttu-id="3bf8c-139">Bağlı aygıtlar Yenile</span><span class="sxs-lookup"><span data-stu-id="3bf8c-139">Refresh connected devices</span></span>
* <span data-ttu-id="3bf8c-140">Bir cihaz kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="3bf8c-140">Authenticate a device</span></span>
* <span data-ttu-id="3bf8c-141">Cihaz ayrıntıları görüntüle</span><span class="sxs-lookup"><span data-stu-id="3bf8c-141">View device details</span></span>
* <span data-ttu-id="3bf8c-142">Tek bir cihaza Yenile</span><span class="sxs-lookup"><span data-stu-id="3bf8c-142">Refresh an individual device</span></span>
* <span data-ttu-id="3bf8c-143">Cihaz yapılandırmasını Sil</span><span class="sxs-lookup"><span data-stu-id="3bf8c-143">Delete a device configuration</span></span>
* <span data-ttu-id="3bf8c-144">Süresi dolan cihaz parolasını değiştirme</span><span class="sxs-lookup"><span data-stu-id="3bf8c-144">Change an expired device password</span></span>
* <span data-ttu-id="3bf8c-145">Başarısız aygıt değiştirin</span><span class="sxs-lookup"><span data-stu-id="3bf8c-145">Replace a failed device</span></span>

> [!NOTE]
> <span data-ttu-id="3bf8c-146">StorSimple Snapshot Manager arabirimini kullanma hakkında genel bilgi için Git [StorSimple Snapshot Manager kullanıcı arabirimini](storsimple-use-snapshot-manager.md).</span><span class="sxs-lookup"><span data-stu-id="3bf8c-146">For general information about using the StorSimple Snapshot Manager interface, go to [StorSimple Snapshot Manager user interface](storsimple-use-snapshot-manager.md).</span></span>


## <a name="add-or-replace-a-device"></a><span data-ttu-id="3bf8c-147">Ekleme veya bir aygıt değiştirme</span><span class="sxs-lookup"><span data-stu-id="3bf8c-147">Add or replace a device</span></span>
<span data-ttu-id="3bf8c-148">Eklemek veya bir StorSimple cihazı değiştirmek için aşağıdaki yordamı kullanın.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-148">Use the following procedure to add or replace a StorSimple device.</span></span>

#### <a name="to-add-or-replace-a-device"></a><span data-ttu-id="3bf8c-149">Eklemek veya bir aygıt değiştirmek için</span><span class="sxs-lookup"><span data-stu-id="3bf8c-149">To add or replace a device</span></span>
1. <span data-ttu-id="3bf8c-150">StorSimple anlık görüntü Yöneticisi'ni başlatmak için Masaüstü simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-150">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="3bf8c-151">İçinde **kapsam** bölmesinde sağ **aygıtları** düğümünü ve ardından **bir aygıt yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-151">In the **Scope** pane, right-click the **Devices** node, and then click **Configure a device**.</span></span> <span data-ttu-id="3bf8c-152">**Bir aygıt yapılandırma** iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-152">The **Configure a Device** dialog box appears.</span></span>
   
    ![Bir StorSimple cihazını Yapılandır](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_config_device.png) 
3. <span data-ttu-id="3bf8c-154">İçinde **aygıt** açılır kutusunda, cihaz veya sanal aygıt IP adresi seçin.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-154">In the **Device** drop-down box, select the IP address of the device or virtual device.</span></span> 
4. <span data-ttu-id="3bf8c-155">İçinde **parola** metin kutusuna, Klasik Azure portalı cihazı için oluşturduğunuz StorSimple Snapshot Manager parolasını yazın.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-155">In the **Password** text box, type the StorSimple Snapshot Manager password that you created for the device in the Azure classic portal.</span></span> <span data-ttu-id="3bf8c-156">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-156">Click **OK**.</span></span> <span data-ttu-id="3bf8c-157">StorSimple Snapshot Manager tanımladığınız cihaz için arar.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-157">StorSimple Snapshot Manager searches for the device that you identified.</span></span> 
   
   * <span data-ttu-id="3bf8c-158">Cihaz kullanılabilir değilse, StorSimple Snapshot Manager bağlantı ekler.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-158">If the device is available, StorSimple Snapshot Manager adds a connection.</span></span>
   * <span data-ttu-id="3bf8c-159">Aygıt için herhangi bir nedenle kullanılamıyorsa, StorSimple Snapshot Manager bir hata iletisi döndürür.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-159">If the device is unavailable for any reason, StorSimple Snapshot Manager returns an error message.</span></span> <span data-ttu-id="3bf8c-160">Tıklatın **Tamam** hata iletisini kapatın ve ardından **iptal** kapatmak için **bir aygıt yapılandırma** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-160">Click **OK** to close the error message, and then click **Cancel** to close the **Configure a Device** dialog box.</span></span>

## <a name="connect-a-device-and-verify-imports"></a><span data-ttu-id="3bf8c-161">Bir aygıtı bağlayın ve içeri aktarmalar doğrulayın</span><span class="sxs-lookup"><span data-stu-id="3bf8c-161">Connect a device and verify imports</span></span>
<span data-ttu-id="3bf8c-162">StorSimple cihazı bağlayın ve yedeklemeleri ilişkilendirdiğiniz varolan birim gruplarda alınır doğrulamak için aşağıdaki yordamı kullanın.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-162">Use the following procedure to connect a StorSimple device and verify that any existing volume groups that have associated backups are imported.</span></span>

#### <a name="to-connect-a-device-and-verify-imports"></a><span data-ttu-id="3bf8c-163">Bir aygıtı bağlayın ve içeri aktarmalar doğrulamak için</span><span class="sxs-lookup"><span data-stu-id="3bf8c-163">To connect a device and verify imports</span></span>
1. <span data-ttu-id="3bf8c-164">StorSimple Snapshot Manager bir aygıtı bağlamak için Ekle'ndaki yönergeleri izleyin veya bir aygıt değiştirin.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-164">To connect a device to StorSimple Snapshot Manager, follow the instructions in Add or replace a device.</span></span> <span data-ttu-id="3bf8c-165">Bir aygıta bağlandığında, StorSimple Snapshot Manager şu şekilde yanıt verir:</span><span class="sxs-lookup"><span data-stu-id="3bf8c-165">When it connects to a device, StorSimple Snapshot Manager responds as follows:</span></span>
   
   * <span data-ttu-id="3bf8c-166">Aygıt için herhangi bir nedenle kullanılamıyorsa, StorSimple Snapshot Manager bir hata iletisi döndürür.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-166">If the device is unavailable for any reason, StorSimple Snapshot Manager returns an error message.</span></span> 
   
   * <span data-ttu-id="3bf8c-167">Cihaz kullanılabilir değilse, StorSimple Snapshot Manager bağlantı ekler.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-167">If the device is available, StorSimple Snapshot Manager adds a connection.</span></span> <span data-ttu-id="3bf8c-168">Cihaz seçtiğinizde görünür **sonuçları** bölmesinde ve durum alanı cihaz olduğunu gösterir **kullanılabilir**.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-168">When you select the device, it appears in the **Results** pane, and the status field indicates that the device is **Available**.</span></span> <span data-ttu-id="3bf8c-169">Birim grupları yedeklemeleri ilişkili sahip olması koşuluyla StorSimple Snapshot Manager aygıt için yapılandırılmış herhangi bir birim grubu içeri aktarır.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-169">StorSimple Snapshot Manager imports any volume groups configured for the device, provided that the volume groups have associated backups.</span></span> <span data-ttu-id="3bf8c-170">Yedekleme ilkeleri içeri aktarılmadı.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-170">Backup policies are not imported.</span></span> <span data-ttu-id="3bf8c-171">İlişkili yedeklemelerinizi olmayan birim grupları içeri aktarılmadı.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-171">Volume groups that do not have associated backups are not imported.</span></span>
2. <span data-ttu-id="3bf8c-172">StorSimple anlık görüntü Yöneticisi'ni başlatmak için Masaüstü simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-172">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
3. <span data-ttu-id="3bf8c-173">En üst düğüme sağ **kapsam** bölmesi ve ardından **içeri aktarmalar ekranını Değiştir**.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-173">Right-click the top node in the **Scope** pane, and then click **Toggle Imports Display**.</span></span>
   
    ![İçeri aktarmalar ekranını Değiştir'i seçin](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_Toggle_Imports_Display.png) 
4. <span data-ttu-id="3bf8c-175">**İçeri aktarmalar ekranını Değiştir** iletişim kutusu görüntülenirse, içeri aktarılan birim grupları ve yedeklemelerin durumunu gösteren.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-175">The **Toggle Imports Display** dialog box appears, showing the status of the imported volume groups and backups.</span></span> <span data-ttu-id="3bf8c-176">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-176">Click **OK**.</span></span>

<span data-ttu-id="3bf8c-177">Birim grupları ve yedeklemeleri başarıyla içeri aktarıldı sonra birim grupları ve oluşturulan ve StorSimple Snapshot Manager ile yapılandırılmış yedeklemeler yalnızca yönetmek gibi StorSimple Snapshot Manager bunları yönetmek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-177">After the volume groups and backups are successfully imported, you can use StorSimple Snapshot Manager to manage them, just as you would manage volume groups and backups that you created and configured with StorSimple Snapshot Manager.</span></span> 

## <a name="refresh-connected-devices"></a><span data-ttu-id="3bf8c-178">Bağlı aygıtlar Yenile</span><span class="sxs-lookup"><span data-stu-id="3bf8c-178">Refresh connected devices</span></span>
<span data-ttu-id="3bf8c-179">StorSimple Snapshot Manager ile bağlı StorSimple cihazları eşitlemek için aşağıdaki yordamı kullanın.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-179">Use the following procedure to synchronize the connected StorSimple devices with StorSimple Snapshot Manager.</span></span>

#### <a name="to-refresh-connected-devices"></a><span data-ttu-id="3bf8c-180">Bağlı aygıtlar yenilemek için</span><span class="sxs-lookup"><span data-stu-id="3bf8c-180">To refresh connected devices</span></span>
1. <span data-ttu-id="3bf8c-181">StorSimple anlık görüntü Yöneticisi'ni başlatmak için Masaüstü simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-181">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="3bf8c-182">İçinde **kapsam** bölmesinde, sağ **aygıtları**ve ardından **yenileme aygıtları**.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-182">In the **Scope** pane, right-click **Devices**, and then click **Refresh Devices**.</span></span> <span data-ttu-id="3bf8c-183">Birim grupları ve tüm sınıflarla da içeren yedeklemeler görüntüleyebilmek bu StorSimple Snapshot Manager bağlı aygıtları eşitler.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-183">This synchronizes the connected devices with StorSimple Snapshot Manager so that you can view the volume groups and backups, including any recent additions.</span></span> 
   
    ![StorSimple cihazlarını Yenile](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_Refresh_devices.png)

<span data-ttu-id="3bf8c-185">**Yenileme aygıtları** eylem bağlı aygıtlardan yeni birim grupları ve tüm ilişkili yedeklemelerinin alır.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-185">The **Refresh Devices** action retrieves any new volume groups and any associated backups from connected devices.</span></span> <span data-ttu-id="3bf8c-186">Farklı **birimleri yeniden tara** eylemi için kullanılabilir **birimleri** düğümü, **yenileme aygıtları** yedekleme kayıt defterini geri yüklemeyin.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-186">Unlike the **Rescan volumes** action available for the **Volumes** node, **Refresh Devices** does not restore the backup registry.</span></span>

## <a name="authenticate-a-device"></a><span data-ttu-id="3bf8c-187">Bir cihaz kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="3bf8c-187">Authenticate a device</span></span>
<span data-ttu-id="3bf8c-188">StorSimple cihazı ile StorSimple Snapshot Manager kimliğini doğrulamak için aşağıdaki yordamı kullanın.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-188">Use the following procedure to authenticate a StorSimple device with StorSimple Snapshot Manager.</span></span>

#### <a name="to-authenticate-a-device"></a><span data-ttu-id="3bf8c-189">Bir cihazın kimliğini doğrulamak için</span><span class="sxs-lookup"><span data-stu-id="3bf8c-189">To authenticate a device</span></span>
1. <span data-ttu-id="3bf8c-190">StorSimple anlık görüntü Yöneticisi'ni başlatmak için Masaüstü simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-190">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="3bf8c-191">İçinde **kapsam** bölmesinde tıklatın **aygıtları**.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-191">In the **Scope** pane, click **Devices**.</span></span>
3. <span data-ttu-id="3bf8c-192">İçinde **sonuçları** bölmesinde, cihaz adına sağ tıklayın ve ardından **kimlik doğrulama**.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-192">In the **Results** pane, right-click the name of the device, and then click **Authenticate**.</span></span>
4. <span data-ttu-id="3bf8c-193">**Kimlik doğrulama** iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-193">The **Authenticate** dialog box appears.</span></span> <span data-ttu-id="3bf8c-194">Cihaz parolasını yazın ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-194">Type the device password, and then click **OK**.</span></span>
   
    ![Kimlik doğrulaması iletişim kutusu](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_Authenticate.png) 

## <a name="view-device-details"></a><span data-ttu-id="3bf8c-196">Cihaz ayrıntıları görüntüle</span><span class="sxs-lookup"><span data-stu-id="3bf8c-196">View device details</span></span>
<span data-ttu-id="3bf8c-197">StorSimple cihazı ayrıntılarını görüntüleyebilir ve gerekirse, cihaz StorSimple Snapshot Manager ile eşitlemek için aşağıdaki yordamı kullanın.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-197">Use the following procedure to view the details of a StorSimple device and, if necessary, resynchronize the device with StorSimple Snapshot Manager.</span></span>

#### <a name="to-view-and-resynchronize-device-details"></a><span data-ttu-id="3bf8c-198">Ayrıntıları görüntülemek ve aygıt yeniden eşitlemek için</span><span class="sxs-lookup"><span data-stu-id="3bf8c-198">To view and resynchronize device details</span></span>
1. <span data-ttu-id="3bf8c-199">StorSimple anlık görüntü Yöneticisi'ni başlatmak için Masaüstü simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-199">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="3bf8c-200">İçinde **kapsam** bölmesinde tıklatın **aygıtları**.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-200">In the **Scope** pane, click **Devices**.</span></span>
3. <span data-ttu-id="3bf8c-201">İçinde **sonuçları** bölmesinde, cihaz adına sağ tıklayın ve ardından **ayrıntıları**.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-201">In the **Results** pane, right-click the name of the device, and then click **Details**.</span></span>

<span data-ttu-id="3bf8c-202">4 **cihaz ayrıntıları** iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-202">4.The **Device Details** dialog box appears.</span></span> <span data-ttu-id="3bf8c-203">Bu kutu gösterir adı, model, sürüm, seri numarası, durum, hedef iSCSI tam adını (IQN) ve son eşitleme tarihi ve saati.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-203">This box shows the name, model, version, serial number, status, target iSCSI Qualified Name (IQN), and last synchronization date and time.</span></span>

* <span data-ttu-id="3bf8c-204">Tıklatın **yeniden eşitleme** cihaz eşitlenecek.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-204">Click **Resync** to synchronize the device.</span></span>
* <span data-ttu-id="3bf8c-205">Tıklatın **Tamam** veya **iptal** iletişim kutusunu kapatın.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-205">Click **OK** or **Cancel** to close the dialog box.</span></span>
  
  ![Cihaz ayrıntıları](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_Device_details.png) 

## <a name="refresh-an-individual-device"></a><span data-ttu-id="3bf8c-207">Tek bir cihaza Yenile</span><span class="sxs-lookup"><span data-stu-id="3bf8c-207">Refresh an individual device</span></span>
<span data-ttu-id="3bf8c-208">Tek bir StorSimple cihazı ile StorSimple Snapshot Manager eşitlemek için aşağıdaki yordamı kullanın.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-208">Use the following procedure to resynchronize an individual StorSimple device with StorSimple Snapshot Manager.</span></span>

#### <a name="to-refresh-a-device"></a><span data-ttu-id="3bf8c-209">Bir aygıt yenilemek için</span><span class="sxs-lookup"><span data-stu-id="3bf8c-209">To refresh a device</span></span>
1. <span data-ttu-id="3bf8c-210">StorSimple anlık görüntü Yöneticisi'ni başlatmak için Masaüstü simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-210">Click the desktop icon to start StorSimple Snapshot Manager.</span></span> 
2. <span data-ttu-id="3bf8c-211">İçinde **kapsam** bölmesinde tıklatın **aygıtları**.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-211">In the **Scope** pane, click **Devices**.</span></span> 
3. <span data-ttu-id="3bf8c-212">İçinde **sonuçları** bölmesinde, cihaz adına sağ tıklayın ve ardından **yenileme aygıt**.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-212">In the **Results** pane, right-click the name of the device, and then click **Refresh Device**.</span></span> <span data-ttu-id="3bf8c-213">Bu cihaz StorSimple Snapshot Manager ile eşitler.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-213">This synchronizes the device with StorSimple Snapshot Manager.</span></span>

## <a name="delete-a-device-configuration"></a><span data-ttu-id="3bf8c-214">Cihaz yapılandırmasını Sil</span><span class="sxs-lookup"><span data-stu-id="3bf8c-214">Delete a device configuration</span></span>
<span data-ttu-id="3bf8c-215">StorSimple anlık görüntü Yöneticisi'nden bir bireysel StorSimple cihaz yapılandırma silmek için aşağıdaki yordamı kullanın.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-215">Use the following procedure to delete an individual StorSimple device configuration from StorSimple Snapshot Manager.</span></span>

#### <a name="to-delete-a-device-configuration"></a><span data-ttu-id="3bf8c-216">Bir aygıt yapılandırmasını silmek için</span><span class="sxs-lookup"><span data-stu-id="3bf8c-216">To delete a device configuration</span></span>
1. <span data-ttu-id="3bf8c-217">StorSimple anlık görüntü Yöneticisi'ni başlatmak için Masaüstü simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-217">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="3bf8c-218">İçinde **kapsam** bölmesinde tıklatın **aygıtları**.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-218">In the **Scope** pane, click **Devices**.</span></span> 
3. <span data-ttu-id="3bf8c-219">İçinde **sonuçları** bölmesinde, cihaz adına sağ tıklayın ve ardından **silmek**.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-219">In the **Results** pane, right-click the name of the device, and then click **Delete**.</span></span> 
4. <span data-ttu-id="3bf8c-220">Aşağıdaki ileti görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-220">The following message appears.</span></span> <span data-ttu-id="3bf8c-221">Tıklatın **Evet** tıklayın veya yapılandırmasını silmek **Hayır** silmeyi iptal etmek için.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-221">Click **Yes** to delete the configuration or click **No** to cancel the deletion.</span></span>
   
    ![Cihaz yapılandırmasını Sil](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_DeleteDevice.png)

## <a name="change-an-expired-device-password"></a><span data-ttu-id="3bf8c-223">Süresi dolan cihaz parolasını değiştirme</span><span class="sxs-lookup"><span data-stu-id="3bf8c-223">Change an expired device password</span></span>
<span data-ttu-id="3bf8c-224">StorSimple cihazı ile StorSimple Snapshot Manager kimlik doğrulaması için bir parola girmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-224">You must enter a password to authenticate a StorSimple device with StorSimple Snapshot Manager.</span></span> <span data-ttu-id="3bf8c-225">Aygıtı ayarlamak için Windows PowerShell arabirimini kullandığınızda bu parola yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-225">You configure this password when you use the Windows PowerShell interface to set up the device.</span></span> <span data-ttu-id="3bf8c-226">Ancak, parola süresinin dolmasını sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-226">However, the password can expire.</span></span> <span data-ttu-id="3bf8c-227">Bu durumda, parolasını değiştirmek için Klasik Azure Portalı'nı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-227">If this happens, you can use the Azure classic portal to change the password.</span></span> <span data-ttu-id="3bf8c-228">Ardından, cihaz StorSimple anlık görüntü Yöneticisi'nde yapılandırıldığından, parola süresi dolmadan önce StorSimple anlık görüntü Yöneticisi'nde aygıt yeniden doğrulaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-228">Then, because the device was configured in StorSimple Snapshot Manager before the password expired, you must re-authenticate the device in StorSimple Snapshot Manager.</span></span>

#### <a name="to-change-the-expired-password"></a><span data-ttu-id="3bf8c-229">Süresi dolan parolayı değiştirmek için</span><span class="sxs-lookup"><span data-stu-id="3bf8c-229">To change the expired password</span></span>
1. <span data-ttu-id="3bf8c-230">Klasik Azure portalında StorSimple Yöneticisi hizmetini başlatın.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-230">In the Azure classic portal, start the StorSimple Manager service.</span></span>
2. <span data-ttu-id="3bf8c-231">Tıklatın **aygıtları** > **yapılandırma** cihaz için.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-231">Click **Devices** > **Configure** for the device.</span></span>
3. <span data-ttu-id="3bf8c-232">StorSimple Snapshot Manager bölümüne gidin.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-232">Scroll down to the StorSimple Snapshot Manager section.</span></span> <span data-ttu-id="3bf8c-233">14-15 karakter olan bir parola girin.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-233">Enter a password that is 14-15 characters.</span></span> <span data-ttu-id="3bf8c-234">Parola büyük harf, küçük harfler, sayısal ve özel karakterlerin bir karışımı içerdiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-234">Make sure that the password contains a mix of uppercase, lowercase, numeric, and special characters.</span></span>
4. <span data-ttu-id="3bf8c-235">Onaylamak için parolayı yeniden girin.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-235">Re-enter the password to confirm it.</span></span>
5. <span data-ttu-id="3bf8c-236">Sayfanın alt kısmındaki **Kaydet**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-236">Click **Save** at the bottom of the page.</span></span>

#### <a name="to-re-authenticate-the-device"></a><span data-ttu-id="3bf8c-237">Cihaz yeniden doğrulamak için</span><span class="sxs-lookup"><span data-stu-id="3bf8c-237">To re-authenticate the device</span></span>
1. <span data-ttu-id="3bf8c-238">StorSimple anlık görüntü Yöneticisi'ni başlatın.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-238">Start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="3bf8c-239">İçinde **kapsam** bölmesinde tıklatın **aygıtları**.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-239">In the **Scope** pane, click **Devices**.</span></span> <span data-ttu-id="3bf8c-240">Yapılandırılmış aygıtların listesini görünür **sonuçları** bölmesi.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-240">A list of configured devices appears in the **Results** pane.</span></span>
3. <span data-ttu-id="3bf8c-241">Aygıt, sağ tıklatın ve ardından seçin **kimlik doğrulama**.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-241">Select the device, right-click, and then click **Authenticate**.</span></span>
4. <span data-ttu-id="3bf8c-242">İçinde **kimlik doğrulama** penceresinde, yeni bir parola girin.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-242">In the **Authenticate** window, enter the new password.</span></span>
5. <span data-ttu-id="3bf8c-243">Aygıt, sağ tıklatın ve seçin seçin **yenileme aygıt**.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-243">Select the device, right-click, and select **Refresh device**.</span></span> <span data-ttu-id="3bf8c-244">Bu cihaz StorSimple Snapshot Manager ile eşitler.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-244">This synchronizes the device with StorSimple Snapshot Manager.</span></span>

## <a name="replace-a-failed-device"></a><span data-ttu-id="3bf8c-245">Başarısız aygıt değiştirin</span><span class="sxs-lookup"><span data-stu-id="3bf8c-245">Replace a failed device</span></span>
<span data-ttu-id="3bf8c-246">StorSimple cihazı başarısız olur ve bekleme (yük devretme) aygıt tarafından değiştirildi, yeni cihaza bağlanın ve ilişkili yedeklemelerinizi görüntülemek için aşağıdaki adımları kullanın.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-246">If a StorSimple device fails and is replaced by a standby (failover) device, use the following steps to connect to the new device and view the associated backups.</span></span>

#### <a name="to-connect-to-a-new-device-after-failover"></a><span data-ttu-id="3bf8c-247">Yük devretme sonrasında yeni bir aygıta bağlanmayı</span><span class="sxs-lookup"><span data-stu-id="3bf8c-247">To connect to a new device after failover</span></span>
1. <span data-ttu-id="3bf8c-248">Yeni cihaz iSCSI bağlantısı yeniden yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-248">Reconfigure the iSCSI connection to the new device.</span></span> <span data-ttu-id="3bf8c-249">Yönergeler için Git "7. adım: bağlama, başlatma ve format bir birim" olarak [şirket içi StorSimple Cihazınızı dağıtma](storsimple-8000-deployment-walkthrough-u2.md).</span><span class="sxs-lookup"><span data-stu-id="3bf8c-249">For instructions, go to "Step 7: Mount, initialize, and format a volume" in [Deploy your on-premises StorSimple device](storsimple-8000-deployment-walkthrough-u2.md).</span></span>

> [!NOTE]
> <span data-ttu-id="3bf8c-250">Yeni StorSimple cihazı eskisiyle aynı IP adresi varsa, eski yapılandırmada bağlanabiliyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-250">If the new StorSimple device has the same IP address as the old one, you might be able to connect the old configuration.</span></span>


1. <span data-ttu-id="3bf8c-251">Microsoft StorSimple Yönetim hizmetini durdurun:</span><span class="sxs-lookup"><span data-stu-id="3bf8c-251">Stop the Microsoft StorSimple Management Service:</span></span>
   
   1. <span data-ttu-id="3bf8c-252">Sunucu Yöneticisi'ni başlatın.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-252">Start Server Manager.</span></span>
   2. <span data-ttu-id="3bf8c-253">Sunucu Yöneticisi panosunda üzerinde **Araçları** menüsünde, select **Hizmetleri**.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-253">On the Server Manager Dashboard, on the **Tools** menu, select **Services**.</span></span>
   3. <span data-ttu-id="3bf8c-254">Üzerinde **Hizmetleri** penceresinde, seçin **Microsoft StorSimple Yöneticisi hizmeti**.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-254">On the **Services** window, select the **Microsoft StorSimple Management Service**.</span></span>
   4. <span data-ttu-id="3bf8c-255">Sağ bölmede altında **Microsoft StorSimple Yöneticisi hizmeti**, tıklatın **hizmetini durdurun**.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-255">In the right pane, under **Microsoft StorSimple Management Service**, click **Stop the service**.</span></span>
2. <span data-ttu-id="3bf8c-256">Eski aygıtla ilgili yapılandırma bilgilerini kaldırın:</span><span class="sxs-lookup"><span data-stu-id="3bf8c-256">Remove the configuration information related to the old device:</span></span>
   
   1. <span data-ttu-id="3bf8c-257">Dosya Gezgini'nde, C:\ProgramData\Microsoft\StorSimple\BACatalog için göz atın.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-257">In File Explorer, browse to C:\ProgramData\Microsoft\StorSimple\BACatalog.</span></span>
   2. <span data-ttu-id="3bf8c-258">BACatalog klasöründeki dosyaları silin.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-258">Delete the files in the BACatalog folder.</span></span>
3. <span data-ttu-id="3bf8c-259">Microsoft StorSimple Yönetim hizmetini yeniden başlatın:</span><span class="sxs-lookup"><span data-stu-id="3bf8c-259">Restart the Microsoft StorSimple Management Service:</span></span>
   
   1. <span data-ttu-id="3bf8c-260">Sunucu Yöneticisi panosunda üzerinde **Araçları** menüsünde, select **Hizmetleri**.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-260">On the Server Manager Dashboard, on the **Tools** menu, select **Services**.</span></span>
   2. <span data-ttu-id="3bf8c-261">Üzerinde **Hizmetleri** penceresinde, seçin **Microsoft StorSimple Yöneticisi hizmeti**.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-261">On the **Services** window, select the **Microsoft StorSimple Management Service**.</span></span>
   3. <span data-ttu-id="3bf8c-262">Sağ bölmede altında **Microsoft StorSimple Yöneticisi hizmeti**, tıklatın **hizmeti yeniden**.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-262">In the right pane, under **Microsoft StorSimple Management Service**, click **Restart the service**.</span></span>
4. <span data-ttu-id="3bf8c-263">StorSimple anlık görüntü Yöneticisi'ni başlatın.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-263">Start StorSimple Snapshot Manager.</span></span>
5. <span data-ttu-id="3bf8c-264">Yeni StorSimple cihazı yapılandırma için adım 2'ndaki adımları tamamlayın: bir StorSimple cihazı bağlanmak [dağıtmak StorSimple Snapshot Manager](storsimple-snapshot-manager-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="3bf8c-264">To configure the new StorSimple device, complete the steps in Step 2: Connect a StorSimple device in [Deploy StorSimple Snapshot Manager](storsimple-snapshot-manager-deployment.md).</span></span>
6. <span data-ttu-id="3bf8c-265">Üst düzey düğümünde sağ **kapsam** bölmesinde (örnekte StorSimple Snapshot Manager) ve ardından **içeri aktarmalar ekranını Değiştir**.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-265">Right-click the top-level node in the **Scope** pane (StorSimple Snapshot Manager in the example), and then click **Toggle Imports Display**.</span></span> 
7. <span data-ttu-id="3bf8c-266">İçeri aktarılan birim grupları ve yedeklemeleri StorSimple anlık görüntü Yöneticisi'nde göründüğünden olmadığında bir ileti görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-266">A message appears when the imported volume groups and backups are visible in StorSimple Snapshot Manager.</span></span> <span data-ttu-id="3bf8c-267">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-267">Click **OK**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3bf8c-268">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3bf8c-268">Next steps</span></span>
* <span data-ttu-id="3bf8c-269">Bilgi edinmek için nasıl [StorSimple çözümünüzün yönetmek için StorSimple Snapshot Manager kullanmak](storsimple-snapshot-manager-admin.md).</span><span class="sxs-lookup"><span data-stu-id="3bf8c-269">Learn how to [use StorSimple Snapshot Manager to administer your StorSimple solution](storsimple-snapshot-manager-admin.md).</span></span>
* <span data-ttu-id="3bf8c-270">Bilgi edinmek için nasıl [görüntülemek ve birimleri yönetmek için StorSimple Snapshot Manager kullanmak](storsimple-snapshot-manager-manage-volumes.md).</span><span class="sxs-lookup"><span data-stu-id="3bf8c-270">Learn how to [use StorSimple Snapshot Manager to view and manage volumes](storsimple-snapshot-manager-manage-volumes.md).</span></span>

