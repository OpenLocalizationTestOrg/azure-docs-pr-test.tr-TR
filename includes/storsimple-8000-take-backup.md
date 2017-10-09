<!--author=alkohli last changed: 01/12/17-->

### <a name="tootake-a-backup"></a><span data-ttu-id="e320b-101">tootake bir yedekleme</span><span class="sxs-lookup"><span data-stu-id="e320b-101">tootake a backup</span></span>

1. <span data-ttu-id="e320b-102">Tooyour StorSimple cihaz Yöneticisi hizmeti gidin.</span><span class="sxs-lookup"><span data-stu-id="e320b-102">Go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="e320b-103">Tablo listesi cihazların Merhaba, seçin ve aygıtınızı tıklatın ve ardından **tüm ayarları**.</span><span class="sxs-lookup"><span data-stu-id="e320b-103">From hello tabular listing of devices, select and click your device and then click **All settings**.</span></span> <span data-ttu-id="e320b-104">Merhaba, **ayarları** dikey penceresinde çok Git**ayarlar > Yönet > Yedekleme İlkesi**.</span><span class="sxs-lookup"><span data-stu-id="e320b-104">In hello **Settings** blade, go too**Settings > Manage > Backup policy**.</span></span>

    ![Add-backup-policy](./media/storsimple-8000-take-backup/step8takebu1.png)

2. <span data-ttu-id="e320b-106">Merhaba, **yedekleme İlkesi** dikey penceresinde tıklatın **+ ilke Ekle**.</span><span class="sxs-lookup"><span data-stu-id="e320b-106">In hello **Backup policy** blade, click **+ Add policy**.</span></span>

    ![Add-backup-policy](./media/storsimple-8000-take-backup/step8takebu2.png)

3. <span data-ttu-id="e320b-108">Merhaba, **yedekleme ilkesi oluşturmak** dikey penceresinde, bir yedekleme ilkenizi için 3 ila 150 karakter içeren bir ad sağlayın.</span><span class="sxs-lookup"><span data-stu-id="e320b-108">In hello **Create backup policy** blade, supply a name that contains between 3 and 150 characters for your backup policy.</span></span>

4. <span data-ttu-id="e320b-109">Yedeklenen hello birimleri toobe seçin.</span><span class="sxs-lookup"><span data-stu-id="e320b-109">Select hello volumes toobe backed up.</span></span> <span data-ttu-id="e320b-110">Birden fazla birim seçerseniz, bu birimleri gruplandırılmış birlikte toocreate kilitlenme tutarlı yedekleme olur.</span><span class="sxs-lookup"><span data-stu-id="e320b-110">If you select more than one volume, these volumes are grouped together toocreate a crash-consistent backup.</span></span>

    ![Add-backup-policy](./media/storsimple-8000-take-backup/step8takebu4.png)

5. <span data-ttu-id="e320b-112">**İlk zamanlamayı ekle** dikey penceresinde:</span><span class="sxs-lookup"><span data-stu-id="e320b-112">On **Add first schedule** blade:</span></span>

    1. <span data-ttu-id="e320b-113">Merhaba yedekleme türünü seçin.</span><span class="sxs-lookup"><span data-stu-id="e320b-113">Select hello type of backup.</span></span> <span data-ttu-id="e320b-114">Daha hızlı geri yükleme gerçekleştirebilmek için **Yerel** anlık görüntüyü seçin.</span><span class="sxs-lookup"><span data-stu-id="e320b-114">For faster restores, select **Local** snapshot.</span></span> <span data-ttu-id="e320b-115">Veri dayanıklılığı için **Bulut** anlık görüntüsünü seçin.</span><span class="sxs-lookup"><span data-stu-id="e320b-115">For data resiliency, select **Cloud** snapshot.</span></span>
    2. <span data-ttu-id="e320b-116">Merhaba yedekleme sıklığını dakika, saat, gün veya hafta belirtin.</span><span class="sxs-lookup"><span data-stu-id="e320b-116">Specify hello backup frequency in minutes, hours, days, or weeks.</span></span>
    3. <span data-ttu-id="e320b-117">Elde tutma süresini seçin.</span><span class="sxs-lookup"><span data-stu-id="e320b-117">Select a retention time.</span></span> <span data-ttu-id="e320b-118">Merhaba elde tutma seçimleri hello yedekleme sıklığına bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="e320b-118">hello retention choices depend on hello backup frequency.</span></span> <span data-ttu-id="e320b-119">Aylık ilkesi için elde tutma ay içinde iken Örneğin, bir günlük ilkesi için hafta içinde hello bekletme belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="e320b-119">For example, for a daily policy, hello retention can be specified in weeks, whereas retention for a monthly policy is in months.</span></span>
    4. <span data-ttu-id="e320b-120">Başlangıç saatini ve tarihini hello yedekleme ilkesi seçin.</span><span class="sxs-lookup"><span data-stu-id="e320b-120">Select hello starting time and date for hello backup policy.</span></span>
    5. <span data-ttu-id="e320b-121">Tıklatın **Tamam** toocreate hello yedekleme ilkesi.</span><span class="sxs-lookup"><span data-stu-id="e320b-121">Click **OK** toocreate hello backup policy.</span></span>

        ![Add-backup-policy](./media/storsimple-8000-take-backup/step8takebu5.png) 

6. <span data-ttu-id="e320b-123">Tıklatın **oluşturma** toostart hello yedekleme ilkesi oluşturma.</span><span class="sxs-lookup"><span data-stu-id="e320b-123">Click **Create** toostart hello backup policy creation.</span></span> <span data-ttu-id="e320b-124">Merhaba yedekleme ilkesi başarıyla oluşturulduğunda size bildirilir.</span><span class="sxs-lookup"><span data-stu-id="e320b-124">You are notified when hello backup policy is successfully created.</span></span> <span data-ttu-id="e320b-125">Yedekleme ilkeleri Hello listesini de güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="e320b-125">hello list of backup policies is also updated.</span></span>
      
      ![Add-backup-policy](./media/storsimple-8000-take-backup/step8takebu9.png)
      
      <span data-ttu-id="e320b-127">Artık, birim verilerinizin zamanlanmış yedeklerini oluşturan bir yedekleme ilkesine sahipsiniz.</span><span class="sxs-lookup"><span data-stu-id="e320b-127">You now have a backup policy that creates scheduled backups of your volume data.</span></span>




