


## <a name="attach-an-empty-disk"></a><span data-ttu-id="980ea-101">Boş disk ekleme</span><span class="sxs-lookup"><span data-stu-id="980ea-101">Attach an empty disk</span></span>
<span data-ttu-id="980ea-102">Boş disk ekleme veri disk, çünkü Azure hello .vhd dosyası sizin için oluşturur ve hello depolama hesabında depolayan basit bir yol tooadd olur.</span><span class="sxs-lookup"><span data-stu-id="980ea-102">Attaching an empty disk is a simple way tooadd a data disk, because Azure creates hello .vhd file for you and stores it in hello storage account.</span></span>

1. <span data-ttu-id="980ea-103">Tıklatın **sanal makineleri (Klasik)**, ve ardından uygun VM seçin hello.</span><span class="sxs-lookup"><span data-stu-id="980ea-103">Click **Virtual Machines (classic)**, and then select hello appropriate VM.</span></span>

2. <span data-ttu-id="980ea-104">Merhaba ayarlar menüsünü tıklatın **diskleri**.</span><span class="sxs-lookup"><span data-stu-id="980ea-104">In hello Settings menu, click **Disks**.</span></span>

   ![Yeni bir boş diski kullanıma açın](./media/howto-attach-disk-windows-linux/menudisksattachnew.png)

3. <span data-ttu-id="980ea-106">Merhaba komut çubuğunda **Attach yeni**.</span><span class="sxs-lookup"><span data-stu-id="980ea-106">On hello command bar, click **Attach new**.</span></span>  
    <span data-ttu-id="980ea-107">Merhaba **Attach yeni disk** iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="980ea-107">hello **Attach new disk** dialog box appears.</span></span>

    ![Yeni bir diski kullanıma açın](./media/howto-attach-disk-windows-linux/newdiskdetail.png)

    <span data-ttu-id="980ea-109">Hello aşağıdaki bilgilerle doldurun:</span><span class="sxs-lookup"><span data-stu-id="980ea-109">Fill in hello following information:</span></span>
    - <span data-ttu-id="980ea-110">İçinde **dosya adı**, hello varsayılan adı kabul edin veya başka bir hello .vhd dosyası için yazın.</span><span class="sxs-lookup"><span data-stu-id="980ea-110">In **File Name**, accept hello default name or type another one for hello .vhd file.</span></span> <span data-ttu-id="980ea-111">Merhaba .vhd dosyası için başka bir ad yazın olsa bile hello veri diski otomatik olarak oluşturulan bir ad kullanır.</span><span class="sxs-lookup"><span data-stu-id="980ea-111">hello data disk uses an automatically generated name, even if you type another name for hello .vhd file.</span></span>
    - <span data-ttu-id="980ea-112">Select hello **türü** hello veri diski.</span><span class="sxs-lookup"><span data-stu-id="980ea-112">Select hello **Type** of hello data disk.</span></span> <span data-ttu-id="980ea-113">Tüm sanal makineler standart diskler destekler.</span><span class="sxs-lookup"><span data-stu-id="980ea-113">All virtual machines support standard disks.</span></span> <span data-ttu-id="980ea-114">Çok sayıda sanal makineler ayrıca premium diskleri destekler.</span><span class="sxs-lookup"><span data-stu-id="980ea-114">Many virtual machines also support premium disks.</span></span>
    - <span data-ttu-id="980ea-115">Select hello **boyutu (GB)** hello veri diski.</span><span class="sxs-lookup"><span data-stu-id="980ea-115">Select hello **Size (GB)** of hello data disk.</span></span>
    - <span data-ttu-id="980ea-116">İçin **ana bilgisayar önbelleğe alma**, hiçbiri seçin veya salt okunur.</span><span class="sxs-lookup"><span data-stu-id="980ea-116">For **Host caching**, choose none or Read Only.</span></span>
    - <span data-ttu-id="980ea-117">Tamam toofinish'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="980ea-117">Click OK toofinish.</span></span>

4. <span data-ttu-id="980ea-118">Merhaba veri diski oluşturduktan ve bağlı sonra hello diskleri bölümünde hello VM listelenir.</span><span class="sxs-lookup"><span data-stu-id="980ea-118">After hello data disk is created and attached, it's listed in hello disks section of hello VM.</span></span>

   ![Yeni ve boş veri diski başarıyla eklendi](./media/howto-attach-disk-windows-linux/newdiskemptysuccessful.png)

> [!NOTE]
> <span data-ttu-id="980ea-120">Bir veri diski ekledikten sonra toohello VM üzerinde toolog gerekir ve böylece bu kullanılabilir hello diski başlatın.</span><span class="sxs-lookup"><span data-stu-id="980ea-120">After you add a data disk, you need toolog on toohello VM and initialize hello disk so that it can be used.</span></span>

## <a name="how-to-attach-an-existing-disk"></a><span data-ttu-id="980ea-121">Nasıl yapılır: varolan bir diski kullanıma açın</span><span class="sxs-lookup"><span data-stu-id="980ea-121">How to: Attach an existing disk</span></span>
<span data-ttu-id="980ea-122">Var olan bir diskin eklenmesi için depolama hesabında bir .vhd olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="980ea-122">Attaching an existing disk requires that you have a .vhd available in a storage account.</span></span> <span data-ttu-id="980ea-123">Kullanım hello [Ekle AzureVhd](https://msdn.microsoft.com/library/azure/dn495173.aspx) cmdlet tooupload hello .vhd dosyası toohello depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="980ea-123">Use hello [Add-AzureVhd](https://msdn.microsoft.com/library/azure/dn495173.aspx) cmdlet tooupload hello .vhd file toohello storage account.</span></span> <span data-ttu-id="980ea-124">Oluşturulan ve hello .vhd dosyası karşıya sonra tooa VM ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="980ea-124">After you've created and uploaded hello .vhd file, you can attach it tooa VM.</span></span>

1. <span data-ttu-id="980ea-125">Tıklatın **sanal makineleri (Klasik)**, ve ardından uygun sanal makine seçin hello.</span><span class="sxs-lookup"><span data-stu-id="980ea-125">Click **Virtual Machines (classic)**, and then select hello appropriate virtual machine.</span></span>

2. <span data-ttu-id="980ea-126">Merhaba ayarlar menüsünü tıklatın **diskleri**.</span><span class="sxs-lookup"><span data-stu-id="980ea-126">In hello Settings menu, click **Disks**.</span></span>

3. <span data-ttu-id="980ea-127">Merhaba komut çubuğunda **Attach varolan**.</span><span class="sxs-lookup"><span data-stu-id="980ea-127">On hello command bar, click **Attach existing**.</span></span>

    ![Veri diski ekleme](./media/howto-attach-disk-windows-linux/menudisksattachexisting.png)

4. <span data-ttu-id="980ea-129">Tıklatın **konumu**.</span><span class="sxs-lookup"><span data-stu-id="980ea-129">Click **Location**.</span></span> <span data-ttu-id="980ea-130">Merhaba kullanılabilir depolama hesaplarını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="980ea-130">hello available storage accounts display.</span></span> <span data-ttu-id="980ea-131">Ardından, uygun depolama hesabı listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="980ea-131">Next, select an appropriate storage account from those listed.</span></span>

    ![Disk depolama hesabı sağlayın](./media/howto-attach-disk-windows-linux/existdiskstorageaccounts.png)

5. <span data-ttu-id="980ea-133">A **depolama hesabı** disk sürücülerini (VHD) içeren bir veya daha fazla kapsayıcıları tutar.</span><span class="sxs-lookup"><span data-stu-id="980ea-133">A **Storage account** holds one or more containers that contain disk drives (vhds).</span></span> <span data-ttu-id="980ea-134">Merhaba uygun bir kapsayıcı listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="980ea-134">Select hello appropriate container from those listed.</span></span>

    ![Makineler windows sanal kapsayıcının sağlayın](./media/howto-attach-disk-windows-linux/existdiskcontainers.png)

6. <span data-ttu-id="980ea-136">Merhaba **VHD'ler** paneli hello disk hello kapsayıcısında tutulan sürücüleri listeler.</span><span class="sxs-lookup"><span data-stu-id="980ea-136">hello **vhds** panel lists hello disk drives held in hello container.</span></span> <span data-ttu-id="980ea-137">Merhaba disklerden birini tıklatın ve Seç'i tıklatın.</span><span class="sxs-lookup"><span data-stu-id="980ea-137">Click one of hello disks, and then click Select.</span></span>

    ![Sanal makineler-windows için disk görüntüsü belirtin](./media/howto-attach-disk-windows-linux/existdiskvhds.png)

7. <span data-ttu-id="980ea-139">Hello **varolan bir diski İlişti** paneli hello depolama hesabı, kapsayıcı ve seçilen sabit disk (vhd) tooadd toohello sanal makine içeren hello konumla yeniden görüntüler.</span><span class="sxs-lookup"><span data-stu-id="980ea-139">hello **Attach existing disk** panel displays again, with hello location containing hello storage account, container, and selected hard disk (vhd) tooadd toohello virtual machine.</span></span>

  <span data-ttu-id="980ea-140">Ayarlama **ana bilgisayar önbelleğe alma** toonone veya okuma yalnızca, ardından Tamam'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="980ea-140">Set **Host caching** toonone or Read only, then click OK.</span></span>

    ![Veri diski başarıyla eklendi](./media/howto-attach-disk-windows-linux/exisitingdisksuccessful.png)
