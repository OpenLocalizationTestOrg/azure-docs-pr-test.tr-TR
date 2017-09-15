<!--author=alkohli last changed: 01/18/17 -->

#### <a name="to-install-updates-via-the-azure-portal"></a><span data-ttu-id="65305-101">Azure portalı aracılığıyla güncelleştirmeleri yüklemek için</span><span class="sxs-lookup"><span data-stu-id="65305-101">To install updates via the Azure portal</span></span>

1. <span data-ttu-id="65305-102">StorSimple Cihaz Yöneticinize gidip **Cihazlar**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="65305-102">Go to your StorSimple Device Manager and select **Devices**.</span></span> <span data-ttu-id="65305-103">Hizmetinize bağlı cihazların listesinden güncelleştirmek istediğiniz cihazı seçip tıklayın.</span><span class="sxs-lookup"><span data-stu-id="65305-103">From the list of devices connected to your service, select and click the device you want to update.</span></span> 

    ![cihaz güncelleştirme](../includes/media/storsimple-virtual-array-install-update-via-portal-04/azupdate1m.png) 

2. <span data-ttu-id="65305-105">**Ayarlar** dikey penceresinde **Cihaz güncelleştirmeleri**'ne tıklayın.</span><span class="sxs-lookup"><span data-stu-id="65305-105">In the **Settings** blade, click **Device updates**.</span></span> 

    ![cihaz güncelleştirme](../includes/media/storsimple-virtual-array-install-update-via-portal-04/azupdate2m.png)  

3. <span data-ttu-id="65305-107">Yazılım güncelleştirmeleri varsa bir ileti görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="65305-107">You see a message if the software updates are available.</span></span> <span data-ttu-id="65305-108">Güncelleştirmeleri denetlemek için **Tara**’ya da tıklayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="65305-108">To check for updates, you can also click **Scan**.</span></span>

    ![cihaz güncelleştirme](../includes/media/storsimple-virtual-array-install-update-via-portal-04/azupdate3m1.png)

    <span data-ttu-id="65305-110">Tarama başlayıp başarıyla tamamlandığında size bildirilir.</span><span class="sxs-lookup"><span data-stu-id="65305-110">You will be notified when the scan starts and completes successfully.</span></span>

    ![cihaz güncelleştirme](../includes/media/storsimple-virtual-array-install-update-via-portal-04/azupdate5m.png)

4. <span data-ttu-id="65305-112">Güncelleştirmeleri tarandıktan sonra **Güncelleştirmeleri indir**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="65305-112">Once the updates are scanned, click **Download updates**.</span></span> 

    ![cihaz güncelleştirme](../includes/media/storsimple-virtual-array-install-update-via-portal-04/azupdate6m.png)

5. <span data-ttu-id="65305-114">**Yeni güncelleştirmeler** dikey penceresinde güncelleştirmeler indirildikten sonra bilgileri gözden geçirin; yüklemeyi onaylamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="65305-114">In the **New updates** blade, review the information that after the updates are downloaded, you need to confirm the installation.</span></span> <span data-ttu-id="65305-115">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="65305-115">Click **OK**.</span></span>

    ![cihaz güncelleştirme](../includes/media/storsimple-virtual-array-install-update-via-portal-04/azupdate7m.png)

6. <span data-ttu-id="65305-117">Karşıya yükleme başlayıp başarıyla tamamlandığında size bildirilir.</span><span class="sxs-lookup"><span data-stu-id="65305-117">You are notified when the upload starts and completes successfully.</span></span>

     ![cihaz güncelleştirme](../includes/media/storsimple-virtual-array-install-update-via-portal-04/azupdate8m.png)

5. <span data-ttu-id="65305-119">**Cihaz güncelleştirmeleri** dikey penceresinde **Yükle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="65305-119">In the **Device updates** blade, click **Install**.</span></span>

     ![cihaz güncelleştirme](../includes/media/storsimple-virtual-array-install-update-via-portal-04/azupdate11m1.png)   

6. <span data-ttu-id="65305-121">**Yeni güncelleştirmeler** dikey penceresinde güncelleştirmenin kesintiye uğratacağı konusunda uyarı alırsınız.</span><span class="sxs-lookup"><span data-stu-id="65305-121">In the **New updates** blade, you are warned that the update is disruptive.</span></span> <span data-ttu-id="65305-122">Sanal dizi tek düğümlü bir cihaz olduğundan, cihaz güncelleştirildikten sonra yeniden başlatılır.</span><span class="sxs-lookup"><span data-stu-id="65305-122">As virtual array is a single node device, the device restarts after it is updated.</span></span> <span data-ttu-id="65305-123">Bu işlem devam eden G/Ç işlemlerini kesintiye uğratır.</span><span class="sxs-lookup"><span data-stu-id="65305-123">This disrupts any IO in progress.</span></span> <span data-ttu-id="65305-124">Güncelleştirmeleri yüklemek için **Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="65305-124">Click **OK** to install the updates.</span></span> 

    ![cihaz güncelleştirme](../includes/media/storsimple-virtual-array-install-update-via-portal-04/azupdate12m.png) 

7. <span data-ttu-id="65305-126">Yükleme işi başladığında size bildirilir.</span><span class="sxs-lookup"><span data-stu-id="65305-126">You are notified when the install job starts.</span></span> 

    ![cihaz güncelleştirme](../includes/media/storsimple-virtual-array-install-update-via-portal-04/azupdate13m.png)

8.  <span data-ttu-id="65305-128">Yükleme işi başarıyla tamamlandıktan sonra yüklemeyi izlemek için **Cihaz güncelleştirmeleri** dikey penceresindeki **İşi Görüntüle** bağlantısına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="65305-128">After the install job completes successfully, click **View Job** link in the **Device updates** blade to monitor the installation.</span></span> 

    ![cihaz güncelleştirme](../includes/media/storsimple-virtual-array-install-update-via-portal-04/azupdate15m1.png)

    <span data-ttu-id="65305-130">Bu işlem sizi **Güncelleştirmeleri Yükle** dikey penceresine götürür.</span><span class="sxs-lookup"><span data-stu-id="65305-130">This takes you to the **Install Updates** blade.</span></span> <span data-ttu-id="65305-131">İşle ilgili ayrıntılı bilgileri burada görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="65305-131">You can view detailed information about the job here.</span></span>

    ![cihaz güncelleştirme](../includes/media/storsimple-virtual-array-install-update-via-portal-04/azupdate16m1.png)

9. <span data-ttu-id="65305-133">Güncelleştirmeler başarıyla yüklendikten sonra **Cihaz güncelleştirmeleri** dikey penceresinde bununla ilgili bir ileti görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="65305-133">After the updates are successfully installed, you see a message to this effect in the **Device updates** blade.</span></span> 