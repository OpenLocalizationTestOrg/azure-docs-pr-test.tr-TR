
<!--author=alkohli last changed: 01/20/2017-->

#### <a name="toocreate-a-manual-backup"></a><span data-ttu-id="da8f8-101">toocreate el ile yedekleme</span><span class="sxs-lookup"><span data-stu-id="da8f8-101">toocreate a manual backup</span></span>

1. <span data-ttu-id="da8f8-102">Tooyour StorSimple cihaz Yöneticisi hizmeti gidin ve ardından **aygıtları**.</span><span class="sxs-lookup"><span data-stu-id="da8f8-102">Go tooyour StorSimple Device Manager service and then click **Devices**.</span></span> <span data-ttu-id="da8f8-103">Aygıtları listeleme tablo Hello, Cihazınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="da8f8-103">From hello tabular listing of devices, select your device.</span></span> <span data-ttu-id="da8f8-104">Çok Git**ayarlar > Yönet > Yedekleme ilkeleri**.</span><span class="sxs-lookup"><span data-stu-id="da8f8-104">Go too**Settings > Manage > Backup policies**.</span></span>

2. <span data-ttu-id="da8f8-105">Merhaba **yedekleme ilkeleri** dikey penceresinde tüm hello yedekleme ilkeleri hello İlkesi tooback yedeklemek istediğiniz hello birim için de dahil olmak üzere bir tablo biçiminde listelenir.</span><span class="sxs-lookup"><span data-stu-id="da8f8-105">hello **Backup policies** blade lists all hello backup policies in a tabular format, including hello policy for hello volume that you want tooback up.</span></span> <span data-ttu-id="da8f8-106">Tooback yedeklemek istediğiniz hello birim ve sağ tıklatma tooinvoke hello bağlam menüsü ile ilişkili hello ilkesi seçin.</span><span class="sxs-lookup"><span data-stu-id="da8f8-106">Select hello policy associated with hello volume you want tooback up and right-click tooinvoke hello context menu.</span></span> <span data-ttu-id="da8f8-107">Merhaba açılır listeden seçin **Şimdi Yedekle**.</span><span class="sxs-lookup"><span data-stu-id="da8f8-107">From hello dropdown list, select **Back up now**.</span></span>

    ![El ile yedekleme oluşturma](./media/storsimple-8000-create-manual-backup/createmanualbu1.png)

3. <span data-ttu-id="da8f8-109">Merhaba, **Şimdi Yedekle** dikey penceresinde, adımları hello:</span><span class="sxs-lookup"><span data-stu-id="da8f8-109">In hello **Back up now** blade, do hello following steps:</span></span>

    1. <span data-ttu-id="da8f8-110">Merhaba uygun seçin **anlık görüntü türünde** hello aşağı açılan listeden: **yerel** anlık görüntü veya **bulut** anlık görüntü.</span><span class="sxs-lookup"><span data-stu-id="da8f8-110">Choose hello appropriate **Snapshot type** from hello dropdown list: **Local** snapshot or **Cloud** snapshot.</span></span> <span data-ttu-id="da8f8-111">Yedekleme ve geri yükleme işlemlerinin hızlı olması için yerel anlık görüntüyü, veri dayanıklılığı için bulut anlık görüntüsünü seçin.</span><span class="sxs-lookup"><span data-stu-id="da8f8-111">Select local snapshot for fast backups or restores, and cloud snapshot for data resiliency.</span></span>

        ![El ile yedekleme oluşturma](./media/storsimple-8000-create-manual-backup/createmanualbu2.png)

    2. <span data-ttu-id="da8f8-113">Tıklatın **Tamam** toostart iş toocreate bir anlık görüntü.</span><span class="sxs-lookup"><span data-stu-id="da8f8-113">Click **OK** toostart a job toocreate a snapshot.</span></span> <span data-ttu-id="da8f8-114">Hello iş başarıyla oluşturulduktan sonra hello sayfanın üst kısmındaki hello bir bildirim görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="da8f8-114">You will see a notification at hello top of hello page after hello job is successfully created.</span></span>

        ![El ile yedekleme oluşturma](./media/storsimple-8000-create-manual-backup/createmanualbu4.png)

    3. <span data-ttu-id="da8f8-116">toomonitor hello işi, hello bildirime tıklayın.</span><span class="sxs-lookup"><span data-stu-id="da8f8-116">toomonitor hello job, click hello notification.</span></span> <span data-ttu-id="da8f8-117">Bu toohello sürer **işleri** dikey penceresinde hello ilerleyişini görüntüleyebileceğiniz.</span><span class="sxs-lookup"><span data-stu-id="da8f8-117">This takes you toohello **Jobs** blade where you can view hello job progress.</span></span>


5. <span data-ttu-id="da8f8-118">Merhaba yedekleme işi tamamlandıktan sonra toohello gidin **yedekleme kataloğu** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="da8f8-118">After hello backup job is finished, go toohello **Backup catalog** tab.</span></span>

6. <span data-ttu-id="da8f8-119">Merhaba filtre seçimlerini toohello uygun aygıt, yedekleme İlkesi ve zaman aralığını ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="da8f8-119">Set hello filter selections toohello appropriate device, backup policy, and time range.</span></span> <span data-ttu-id="da8f8-120">Merhaba yedekleme hello hello kataloğunda görüntülenen yedekleme ayarları listesinde görüntülenmelidir.</span><span class="sxs-lookup"><span data-stu-id="da8f8-120">hello backup should appear in hello list of backup sets that is displayed in hello catalog.</span></span>

