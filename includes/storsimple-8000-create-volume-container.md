<!--author=alkohli last changed: 06/22/17-->

#### <a name="toocreate-a-volume-container"></a><span data-ttu-id="f914c-101">toocreate birim kapsayıcısı</span><span class="sxs-lookup"><span data-stu-id="f914c-101">toocreate a volume container</span></span>
1. <span data-ttu-id="f914c-102">Tooyour StorSimple cihaz Yöneticisi hizmeti gidin ve tıklayın **aygıtları**.</span><span class="sxs-lookup"><span data-stu-id="f914c-102">Go tooyour StorSimple Device Manager service and click **Devices**.</span></span> <span data-ttu-id="f914c-103">Hello hello aygıtları listeleme tablo, seçin ve bir cihaza tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f914c-103">From hello tabular listing of hello devices, select and click a device.</span></span> 

    ![Birim kapsayıcısı dikey penceresi](./media/storsimple-8000-create-volume-container/createvolumecontainer1.png)

2. <span data-ttu-id="f914c-105">Merhaba aygıt panosunda tıklatın **+ Ekle birim kapsayıcısı**</span><span class="sxs-lookup"><span data-stu-id="f914c-105">In hello device dashboard, click **+ Add volume container**</span></span>

    ![Birim kapsayıcısı dikey penceresi](./media/storsimple-8000-create-volume-container/createvolumecontainer2.png)

3. <span data-ttu-id="f914c-107">Merhaba, **Ekle birim kapsayıcısı** dikey penceresinde:</span><span class="sxs-lookup"><span data-stu-id="f914c-107">In hello **Add volume container** blade:</span></span>
   
   1. <span data-ttu-id="f914c-108">Merhaba cihaz otomatik olarak seçilir.</span><span class="sxs-lookup"><span data-stu-id="f914c-108">hello device is automatically selected.</span></span>
   2. <span data-ttu-id="f914c-109">Birim kapsayıcınıza bir **Ad** verin.</span><span class="sxs-lookup"><span data-stu-id="f914c-109">Supply a **Name** for your volume container.</span></span> <span data-ttu-id="f914c-110">Merhaba adı 3 too32 karakter uzunluğunda olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f914c-110">hello name must be 3 too32 characters long.</span></span> <span data-ttu-id="f914c-111">Birim kapsayıcısını bir kez oluşturduktan sonra yeniden adlandıramazsınız.</span><span class="sxs-lookup"><span data-stu-id="f914c-111">You cannot rename a volume container once it is created.</span></span>
   3. <span data-ttu-id="f914c-112">Seçin **bulut depolama şifrelemesini etkinleştir** tooenable hello aygıt toohello buluttan gönderilen hello verilerin şifrelenmesi.</span><span class="sxs-lookup"><span data-stu-id="f914c-112">Select **Enable Cloud Storage Encryption** tooenable encryption of hello data sent from hello device toohello cloud.</span></span>
   4. <span data-ttu-id="f914c-113">Sağlayın ve onaylayın bir **bulut depolama şifreleme anahtarı** diğer bir deyişle 8 too32 karakterden uzun.</span><span class="sxs-lookup"><span data-stu-id="f914c-113">Provide and confirm a **Cloud Storage Encryption Key** that is 8 too32 characters long.</span></span> <span data-ttu-id="f914c-114">Bu anahtar hello cihaz tooaccess şifrelenmiş verileri tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f914c-114">This key is used by hello device tooaccess encrypted data.</span></span>
   5. <span data-ttu-id="f914c-115">Seçin bir **depolama hesabı** tooassociate bu birim kapsayıcısı ile.</span><span class="sxs-lookup"><span data-stu-id="f914c-115">Select a **Storage Account** tooassociate with this volume container.</span></span> <span data-ttu-id="f914c-116">Varolan bir depolama hesabı veya hello hizmet oluşturma zamanında oluşturulan hello varsayılan hesabı seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f914c-116">You can choose an existing storage account or hello default account that is generated at hello time of service creation.</span></span> <span data-ttu-id="f914c-117">Merhaba de kullanabilirsiniz **yeni Ekle** seçeneği toospecify olmayan bir depolama hesabı bağlı toothis hizmet aboneliği.</span><span class="sxs-lookup"><span data-stu-id="f914c-117">You can also use hello **Add new** option toospecify a storage account that is not linked toothis service subscription.</span></span>
   6. <span data-ttu-id="f914c-118">Seçin **sınırsız** hello içinde **bant genişliğini belirtin** hello kullanılabilir tüm bant genişliğini tooconsume isterseniz, aşağı açılan liste.</span><span class="sxs-lookup"><span data-stu-id="f914c-118">Select **Unlimited** in hello **Specify bandwidth** drop-down list if you wish tooconsume all hello available bandwidth.</span></span> <span data-ttu-id="f914c-119">Bu seçeneği çok ayarlayabilirsiniz**özel** tooemploy bant genişliği denetimleri ve 1 MB/sn ile 1000 MB/sn arasında bir değer belirtin.</span><span class="sxs-lookup"><span data-stu-id="f914c-119">You can also set this option too**Custom** tooemploy bandwidth controls, and specify a value between 1 Mbps and 1,000 Mbps.</span></span>
      <span data-ttu-id="f914c-120">Bant genişliği kullanım bilgileriniz kullanılabilir varsa belirterek bir zamanlamaya göre mümkün tooallocate bant genişliği olabilir **bant genişliği şablonu seçin**.</span><span class="sxs-lookup"><span data-stu-id="f914c-120">If you have your bandwidth usage information available, you may be able tooallocate bandwidth based on a schedule by specifying **Select a bandwidth template**.</span></span> <span data-ttu-id="f914c-121">Adım adım bir yordam için çok Git[bant genişliği şablonu ekleyin](../articles/storsimple/storsimple-8000-manage-bandwidth-templates.md#add-a-bandwidth-template).</span><span class="sxs-lookup"><span data-stu-id="f914c-121">For a step-by-step procedure, go too[Add a bandwidth template](../articles/storsimple/storsimple-8000-manage-bandwidth-templates.md#add-a-bandwidth-template).</span></span>

      ![Birim kapsayıcısı dikey penceresi](./media/storsimple-8000-create-volume-container/createvolumecontainer6b.png)
   7. <span data-ttu-id="f914c-123">**Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f914c-123">Click **Create**.</span></span>

        ![Birim kapsayıcısı dikey penceresi](./media/storsimple-8000-create-volume-container/createvolumecontainer6.png)
   
       <span data-ttu-id="f914c-125">Merhaba birim kapsayıcısı başarıyla oluşturulduğunda size bildirilir.</span><span class="sxs-lookup"><span data-stu-id="f914c-125">You are notified when hello volume container is successfully created.</span></span>

       ![Birim kapsayıcısı oluşturma bildirimi](./media/storsimple-8000-create-volume-container/createvolumecontainer8.png)

   <span data-ttu-id="f914c-127">Yeni oluşturulan birim kapsayıcı hello cihazınız için birim kapsayıcıları hello listesinde listelenir.</span><span class="sxs-lookup"><span data-stu-id="f914c-127">hello newly created volume container is listed in hello list of volume containers for your device.</span></span>

   ![Birim kapsayıcısı ekle dikey penceresi](./media/storsimple-8000-create-volume-container/createvolumecontainer9.png)


