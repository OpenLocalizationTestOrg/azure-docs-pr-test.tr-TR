<!--author=alkohli last changed: 08/04/17-->

#### <a name="tooinstall-an-update-from-hello-azure-portal"></a><span data-ttu-id="c4364-101">tooinstall hello Azure portal gelen güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="c4364-101">tooinstall an update from hello Azure portal</span></span>

1. <span data-ttu-id="c4364-102">Merhaba StorSimple hizmeti sayfasında Cihazınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="c4364-102">On hello StorSimple service page, select your device.</span></span>

    ![Cihazı seçin](./media/storsimple-8000-install-update5-via-portal/update1.png)

2. <span data-ttu-id="c4364-104">Çok gidin**aygıt ayarları** > **aygıt güncelleştirmeleri**.</span><span class="sxs-lookup"><span data-stu-id="c4364-104">Navigate too**Device settings** > **Device updates**.</span></span>

    ![Cihaz güncelleştirmeleri tıklatın](./media/storsimple-8000-install-update5-via-portal/update2.png)

2. <span data-ttu-id="c4364-106">Yeni güncelleştirmeler varsa bir bildirim görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="c4364-106">A notification appears if new updates are available.</span></span> <span data-ttu-id="c4364-107">Alternatif olarak, hello içinde **cihaz güncelleştirmeleri** dikey penceresinde tıklatın **Güncelleştirmeleri tara**.</span><span class="sxs-lookup"><span data-stu-id="c4364-107">Alternatively, in hello **Device updates** blade, click **Scan Updates**.</span></span> <span data-ttu-id="c4364-108">Bir iş için kullanılabilir güncelleştirmeleri tooscan oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="c4364-108">A job is created tooscan for available updates.</span></span> <span data-ttu-id="c4364-109">Merhaba işi başarıyla tamamlandığında size bildirilir.</span><span class="sxs-lookup"><span data-stu-id="c4364-109">You are notified when hello job completes successfully.</span></span>

    ![Cihaz güncelleştirmeleri tıklatın](./media/storsimple-8000-install-update5-via-portal/update3.png)

3. <span data-ttu-id="c4364-111">Cihazınızda bir güncelleştirmeyi uygulamadan önce hello sürüm notlarını gözden geçirmenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="c4364-111">We recommend that you review hello release notes before you apply an update on your device.</span></span> <span data-ttu-id="c4364-112">tooapply güncelleştirmeler **güncelleştirmelerini yükleme**.</span><span class="sxs-lookup"><span data-stu-id="c4364-112">tooapply updates, click **Install updates**.</span></span> <span data-ttu-id="c4364-113">Merhaba, **düzenli olarak güncelleştirmeleri Onayla** dikey penceresinde, güncelleştirmeleri uygulamadan önce gözden geçirme hello Önkoşullar toocomplete.</span><span class="sxs-lookup"><span data-stu-id="c4364-113">In hello **Confirm regular updates** blade, review hello prerequisites toocomplete before you apply updates.</span></span> <span data-ttu-id="c4364-114">Hazır tooupdate hello aygıta ve ardından hello onay kutusunu tooindicate seçin **yükleme**.</span><span class="sxs-lookup"><span data-stu-id="c4364-114">Select hello checkbox tooindicate that you are ready tooupdate hello device and then click **Install**.</span></span>

    ![Cihaz güncelleştirmeleri tıklatın](./media/storsimple-8000-install-update5-via-portal/update4.png)

6. <span data-ttu-id="c4364-116">Bir dizi önkoşul denetimi başlatılır.</span><span class="sxs-lookup"><span data-stu-id="c4364-116">A set of prerequisite checks starts.</span></span> <span data-ttu-id="c4364-117">Bu denetimler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="c4364-117">These checks include:</span></span>
   
   * <span data-ttu-id="c4364-118">**Denetleyici durumu denetimleri** hem de aygıt denetleyicileri hello tooverify sağlıklı ve çevrimiçi.</span><span class="sxs-lookup"><span data-stu-id="c4364-118">**Controller health checks** tooverify that both hello device controllers are healthy and online.</span></span>
   * <span data-ttu-id="c4364-119">**Donanım bileşeni durumu denetimleri** tüm donanım bileşenleri, StorSimple Cihazınızda hello tooverify sağlıklı.</span><span class="sxs-lookup"><span data-stu-id="c4364-119">**Hardware component health checks** tooverify that all hello hardware components on your StorSimple device are healthy.</span></span>
   * <span data-ttu-id="c4364-120">**Veri 0 denetler** tooverify veri 0 aygıtınızda etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="c4364-120">**DATA 0 checks** tooverify that DATA 0 is enabled on your device.</span></span> <span data-ttu-id="c4364-121">Bu arabirim etkin değilse etkinleştirmeniz ve sonra yeniden denemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="c4364-121">If this interface is not enabled, you must enable it and then retry.</span></span>

    <span data-ttu-id="c4364-122">Merhaba güncelleştirme indirilir ve yüklü değilse yalnızca hello denetimlerinin tümünün başarıyla tamamlanır.</span><span class="sxs-lookup"><span data-stu-id="c4364-122">hello update is downloaded and installed only if all hello checks are successfully completed.</span></span> <span data-ttu-id="c4364-123">Merhaba denetimleri devam ederken size bildirilir.</span><span class="sxs-lookup"><span data-stu-id="c4364-123">You are notified when hello checks are in progress.</span></span> <span data-ttu-id="c4364-124">Ardından Hello prechecks başarısız olursa, hello nedenler ile sağlanacaktır.</span><span class="sxs-lookup"><span data-stu-id="c4364-124">If hello prechecks fail, then you will be provided with hello reasons for failure.</span></span> <span data-ttu-id="c4364-125">Bu sorunları gidermek ve hello işlemi yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="c4364-125">Address those issues and then retry hello operation.</span></span> <span data-ttu-id="c4364-126">Kendiniz tarafından bu sorunları gidermek olamaz, toocontact Microsoft Support gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="c4364-126">You may need toocontact Microsoft Support if you cannot address these issues by yourself.</span></span>

7. <span data-ttu-id="c4364-127">Merhaba prechecks başarıyla tamamlandıktan sonra bir güncelleştirme işi oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="c4364-127">After hello prechecks are successfully completed, an update job is created.</span></span> <span data-ttu-id="c4364-128">Merhaba güncelleştirme işi başarıyla oluşturulduğunda size bildirilir.</span><span class="sxs-lookup"><span data-stu-id="c4364-128">You are notified when hello update job is successfully created.</span></span>
   
    ![Güncelleştirme işi oluşturma](./media/storsimple-8000-install-update5-via-portal/update6.png)
   
    <span data-ttu-id="c4364-130">Merhaba güncelleştirme aygıtınızda sonra uygulanır.</span><span class="sxs-lookup"><span data-stu-id="c4364-130">hello update is then applied on your device.</span></span>

9. <span data-ttu-id="c4364-131">Merhaba güncelleştirme birkaç saat toocomplete alır.</span><span class="sxs-lookup"><span data-stu-id="c4364-131">hello update takes a few hours toocomplete.</span></span> <span data-ttu-id="c4364-132">Merhaba güncelleştirme işi seçin ve tıklatın **ayrıntıları** hello işin herhangi bir zamanda tooview hello ayrıntılarını.</span><span class="sxs-lookup"><span data-stu-id="c4364-132">Select hello update job and click **Details** tooview hello details of hello job at any time.</span></span>

    ![Güncelleştirme işi oluşturma](./media/storsimple-8000-install-update5-via-portal/update8.png)

     <span data-ttu-id="c4364-134">Ayrıca hello güncelleştirme işten hello ilerlemesini izleyebilirsiniz **Aygıt Ayarları > işleri**.</span><span class="sxs-lookup"><span data-stu-id="c4364-134">You can also monitor hello progress of hello update job from **Device settings > Jobs**.</span></span> <span data-ttu-id="c4364-135">Merhaba üzerinde **işleri** dikey penceresinde, devam eden güncelleştirme hello görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c4364-135">On hello **Jobs** blade, you can see hello update progress.</span></span>

     ![Güncelleştirme işi oluşturma](./media/storsimple-8000-install-update5-via-portal/update7.png)

10. <span data-ttu-id="c4364-137">Merhaba işi tamamlandıktan sonra toohello gidin **Aygıt Ayarları > aygıt güncelleştirmeleri**.</span><span class="sxs-lookup"><span data-stu-id="c4364-137">After hello job is complete, navigate toohello **Device settings > Device updates**.</span></span> <span data-ttu-id="c4364-138">Merhaba yazılım sürümü şimdi güncelleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="c4364-138">hello software version should now be updated.</span></span>

