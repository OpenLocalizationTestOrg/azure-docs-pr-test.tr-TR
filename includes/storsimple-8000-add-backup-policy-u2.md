<!--author=alkohli last changed: 02/10/17-->

#### <a name="to-add-a-storsimple-backup-policy"></a><span data-ttu-id="30a52-101">Bir StorSimple yedekleme ilkesi eklemek için</span><span class="sxs-lookup"><span data-stu-id="30a52-101">To add a StorSimple backup policy</span></span>

1. <span data-ttu-id="30a52-102">StorSimple cihazınıza gidin ve **Yedekleme ilkesi**’ne tıklayın.</span><span class="sxs-lookup"><span data-stu-id="30a52-102">Go to your StorSimple device and click **Backup policy**.</span></span>

2. <span data-ttu-id="30a52-103">**Yedekleme ilkesi** dikey penceresinde komut çubuğundan **+ İlke ekle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="30a52-103">In the **Backup policy** blade, click **+ Add policy** from the command bar.</span></span>
   
    ![Yedekleme ilkesi ekleme](./media/storsimple-8000-add-backup-policy-u2/addbupol1.png)

3. <span data-ttu-id="30a52-105">**Yedekleme ilkesi oluştur** dikey penceresinde, aşağıdaki adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="30a52-105">In the **Create backup policy** blade, do the following steps:</span></span>
   
   1. <span data-ttu-id="30a52-106">**Cihazı seçin** alanı, seçtiğiniz cihaza göre otomatik olarak doldurulur.</span><span class="sxs-lookup"><span data-stu-id="30a52-106">**Select device** is automatically populated based on the device you selected.</span></span>
   
   2. <span data-ttu-id="30a52-107">3 ila 150 karakter içeren bir yedekleme **İlke adı** belirtin.</span><span class="sxs-lookup"><span data-stu-id="30a52-107">Specify a backup **Policy name** that contains between 3 and 150 characters.</span></span> <span data-ttu-id="30a52-108">İlke oluşturulduktan sonra ilkeyi yeniden adlandıramazsınız.</span><span class="sxs-lookup"><span data-stu-id="30a52-108">Once the policy is created, you cannot rename the policy.</span></span>
       
   3. <span data-ttu-id="30a52-109">Bu yedekleme ilkesine birim atamak için **Birim ekle**’yi seçin ve ardından birimlerin tablosal listesinde, bu yedekleme ilkesine bir veya daha fazla birim atamak için onay kutularına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="30a52-109">To assign volumes to this backup policy, select **Add volumes** and then from the tabular listing of volumes, click the check box(es) to assign one or more volumes to this backup policy.</span></span>

       ![Yedekleme ilkesi ekleme](./media/storsimple-8000-add-backup-policy-u2/addbupol2.png)

   4. <span data-ttu-id="30a52-111">Bu yedekleme ilkesi için bir zamanlama tanımlamak için **İlk zamanlama**’ya tıklayın ve aşağıdaki parametreleri değiştirin:</span><span class="sxs-lookup"><span data-stu-id="30a52-111">To define a schedule for this backup policy, click **First schedule** and then modify the following parameters:</span></span>

       ![Yedekleme ilkesi ekleme](./media/storsimple-8000-add-backup-policy-u2/addbupol3.png)

       1. <span data-ttu-id="30a52-113">**Anlık görüntü türü** için **Bulut** veya **Yerel**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="30a52-113">For **Snapshot type**, select **Cloud** or **Local**.</span></span>

       2. <span data-ttu-id="30a52-114">Yedekleme sıklığını belirtin (bir sayı belirtip açılan listeden **Gün** veya **Hafta** öğesini seçin).</span><span class="sxs-lookup"><span data-stu-id="30a52-114">Indicate the frequency of backups (specify a number and then choose **Days** or **Weeks** from the drop-down list.</span></span>

       3. <span data-ttu-id="30a52-115">Bir elde tutma zamanlaması girin.</span><span class="sxs-lookup"><span data-stu-id="30a52-115">Enter a retention schedule.</span></span>

       4. <span data-ttu-id="30a52-116">Yedekleme ilkesinin başlayacağı saat ve tarihi girin.</span><span class="sxs-lookup"><span data-stu-id="30a52-116">Enter a time and date for the backup policy to begin.</span></span>

       5. <span data-ttu-id="30a52-117">Zamanlamayı tanımlamak için **Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="30a52-117">Click **OK** to define the schedule.</span></span>

   5. <span data-ttu-id="30a52-118">Yedekleme ilkesi oluşturmak için **Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="30a52-118">Click **Create** to create a backup policy.</span></span>

       ![Yedekleme ilkesi ekleme](./media/storsimple-8000-add-backup-policy-u2/addbupol4.png)
   
   6. <span data-ttu-id="30a52-120">Yedekleme ilkesi oluşturulduğunda size bildirilir.</span><span class="sxs-lookup"><span data-stu-id="30a52-120">You are notified when the backup policy is created.</span></span> <span data-ttu-id="30a52-121">Yeni eklenen ilke, **Yedekleme İlkeleri** dikey penceresinin tablosal görünümünde gösterilir.</span><span class="sxs-lookup"><span data-stu-id="30a52-121">The newly added policy is displayed in the tabular view on the **Backup Policy** blade.</span></span>

       ![Yedekleme ilkesi ekleme](./media/storsimple-8000-add-backup-policy-u2/addbupol7.png)

