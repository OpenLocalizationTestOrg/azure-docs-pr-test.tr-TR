<!--author=alkohli last changed: 01/12/17-->

### <a name="to-take-a-backup"></a><span data-ttu-id="08421-101">Yedek almak için</span><span class="sxs-lookup"><span data-stu-id="08421-101">To take a backup</span></span>

1. <span data-ttu-id="08421-102">StorSimple Cihaz Yöneticisi hizmetinize gidin.</span><span class="sxs-lookup"><span data-stu-id="08421-102">Go to your StorSimple Device Manager service.</span></span> <span data-ttu-id="08421-103">Tablosal cihaz listesinden cihazınızı seçmek için tıklayın ve **Tüm ayarlar**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="08421-103">From the tabular listing of devices, select and click your device and then click **All settings**.</span></span> <span data-ttu-id="08421-104">**Ayarlar** dikey penceresinde **Ayarlar > Yönet > Yedekleme ilkesi**’ne gidin.</span><span class="sxs-lookup"><span data-stu-id="08421-104">In the **Settings** blade, go to **Settings > Manage > Backup policy**.</span></span>

    ![Add-backup-policy](./media/storsimple-8000-take-backup/step8takebu1.png)

2. <span data-ttu-id="08421-106">**Yedekleme ilkesi** dikey penceresinde **+ İlke ekle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="08421-106">In the **Backup policy** blade, click **+ Add policy**.</span></span>

    ![Add-backup-policy](./media/storsimple-8000-take-backup/step8takebu2.png)

3. <span data-ttu-id="08421-108">**Yedekleme ilkesi oluştur** dikey penceresinde, yedekleme ilkenize 3 - 150 arası karakterden oluşan bir ad verin.</span><span class="sxs-lookup"><span data-stu-id="08421-108">In the **Create backup policy** blade, supply a name that contains between 3 and 150 characters for your backup policy.</span></span>

4. <span data-ttu-id="08421-109">Yedeği alınacak birimleri seçin.</span><span class="sxs-lookup"><span data-stu-id="08421-109">Select the volumes to be backed up.</span></span> <span data-ttu-id="08421-110">Birden fazla birim seçerseniz, kilitlenmeyle tutarlı yedek oluşturmak için bu birimler birlikte gruplandırılır.</span><span class="sxs-lookup"><span data-stu-id="08421-110">If you select more than one volume, these volumes are grouped together to create a crash-consistent backup.</span></span>

    ![Add-backup-policy](./media/storsimple-8000-take-backup/step8takebu4.png)

5. <span data-ttu-id="08421-112">**İlk zamanlamayı ekle** dikey penceresinde:</span><span class="sxs-lookup"><span data-stu-id="08421-112">On **Add first schedule** blade:</span></span>

    1. <span data-ttu-id="08421-113">Yedekleme türünü seçin.</span><span class="sxs-lookup"><span data-stu-id="08421-113">Select the type of backup.</span></span> <span data-ttu-id="08421-114">Daha hızlı geri yükleme gerçekleştirebilmek için **Yerel** anlık görüntüyü seçin.</span><span class="sxs-lookup"><span data-stu-id="08421-114">For faster restores, select **Local** snapshot.</span></span> <span data-ttu-id="08421-115">Veri dayanıklılığı için **Bulut** anlık görüntüsünü seçin.</span><span class="sxs-lookup"><span data-stu-id="08421-115">For data resiliency, select **Cloud** snapshot.</span></span>
    2. <span data-ttu-id="08421-116">Yedekleme sıklığını dakika, saat, gün veya hafta cinsinden belirtin.</span><span class="sxs-lookup"><span data-stu-id="08421-116">Specify the backup frequency in minutes, hours, days, or weeks.</span></span>
    3. <span data-ttu-id="08421-117">Elde tutma süresini seçin.</span><span class="sxs-lookup"><span data-stu-id="08421-117">Select a retention time.</span></span> <span data-ttu-id="08421-118">Elde tutma seçimleri yedekleme sıklığına bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="08421-118">The retention choices depend on the backup frequency.</span></span> <span data-ttu-id="08421-119">Örneğin, günlük ilkesi için elde tutma İlkesi hafta cinsinden belirtilebilirken, aylık ilkesi için elde tutma ay cinsindendir.</span><span class="sxs-lookup"><span data-stu-id="08421-119">For example, for a daily policy, the retention can be specified in weeks, whereas retention for a monthly policy is in months.</span></span>
    4. <span data-ttu-id="08421-120">Yedekleme ilkesinin başlangıç saatini ve tarihini seçin.</span><span class="sxs-lookup"><span data-stu-id="08421-120">Select the starting time and date for the backup policy.</span></span>
    5. <span data-ttu-id="08421-121">Yedekleme ilkesini oluşturmak için **Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="08421-121">Click **OK** to create the backup policy.</span></span>

        ![Add-backup-policy](./media/storsimple-8000-take-backup/step8takebu5.png) 

6. <span data-ttu-id="08421-123">Yedekleme ilkesi oluşturma işlemini başlatmak için **Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="08421-123">Click **Create** to start the backup policy creation.</span></span> <span data-ttu-id="08421-124">Yedekleme ilkesi başarıyla oluşturulduğunda size bildirilir.</span><span class="sxs-lookup"><span data-stu-id="08421-124">You are notified when the backup policy is successfully created.</span></span> <span data-ttu-id="08421-125">Yedekleme ilkeleri listesi de güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="08421-125">The list of backup policies is also updated.</span></span>
      
      ![Add-backup-policy](./media/storsimple-8000-take-backup/step8takebu9.png)
      
      <span data-ttu-id="08421-127">Artık, birim verilerinizin zamanlanmış yedeklerini oluşturan bir yedekleme ilkesine sahipsiniz.</span><span class="sxs-lookup"><span data-stu-id="08421-127">You now have a backup policy that creates scheduled backups of your volume data.</span></span>




