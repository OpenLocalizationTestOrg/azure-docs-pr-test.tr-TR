<!--author=alkohli last changed: 9/16/15-->


#### <a name="toocable-your-device-for-power"></a><span data-ttu-id="b7195-101">toocable güç aygıtınızın</span><span class="sxs-lookup"><span data-stu-id="b7195-101">toocable your device for power</span></span>
> [!NOTE]
> <span data-ttu-id="b7195-102">StorSimple Cihazınızda iki kasaları yedekli PCMs içerir.</span><span class="sxs-lookup"><span data-stu-id="b7195-102">Both enclosures on your StorSimple device include redundant PCMs.</span></span> <span data-ttu-id="b7195-103">Her kasa için hello PCMs yüklenmelidir ve toodifferent güç kaynakları tooensure yüksek kullanılabilirlik bağlı.</span><span class="sxs-lookup"><span data-stu-id="b7195-103">For each enclosure, hello PCMs must be installed and connected toodifferent power sources tooensure high availability.</span></span>
> 
> 

1. <span data-ttu-id="b7195-104">Tüm hello PCMs Hello güç anahtarlar hello OFF konumunda olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="b7195-104">Make sure that hello power switches on all hello PCMs are in hello OFF position.</span></span>
2. <span data-ttu-id="b7195-105">Merhaba birincil muhafaza, hello güç kablosu tooboth PCMs bağlayın.</span><span class="sxs-lookup"><span data-stu-id="b7195-105">On hello primary enclosure, connect hello power cords tooboth PCMs.</span></span> <span data-ttu-id="b7195-106">Aşağıdaki diyagram, kablolama hello güç kırmızıyla Hello güç kablosu tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="b7195-106">hello power cords are identified in red in hello power cabling diagram, below.</span></span>
3. <span data-ttu-id="b7195-107">Merhaba birincil muhafaza kullanım ayrı güç kaynaklarında iki PCMs hello emin olun.</span><span class="sxs-lookup"><span data-stu-id="b7195-107">Make sure that hello two PCMs on hello primary enclosure use separate power sources.</span></span>
4. <span data-ttu-id="b7195-108">Merhaba güç kablosu toohello güç diyagramı kablo hello gücünden gösterildiği gibi hello raf dağıtım birimlerine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b7195-108">Attach hello power cords toohello power on hello rack distribution units as shown in hello power cabling diagram.</span></span>
5. <span data-ttu-id="b7195-109">EBOD muhafazası hello için 2-4 arasındaki adımları yineleyin.</span><span class="sxs-lookup"><span data-stu-id="b7195-109">Repeat steps 2 through 4 for hello EBOD enclosure.</span></span>
6. <span data-ttu-id="b7195-110">Merhaba EBOD muhafazası üzerinde her PCM toohello ON konumuna hello güç anahtarı döndürerek açın.</span><span class="sxs-lookup"><span data-stu-id="b7195-110">Turn on hello EBOD enclosure by flipping hello power switch on each PCM toohello ON position.</span></span>
7. <span data-ttu-id="b7195-111">Bu hello EBOD muhafazası hello yeşil LED'leri hello EBOD denetleyicisi arkasına hello üzerinde ON işaretlidir denetleyerek açık olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="b7195-111">Verify that hello EBOD enclosure is turned on by checking that hello green LEDs on hello back of hello EBOD controller are turned ON.</span></span>
8. <span data-ttu-id="b7195-112">Merhaba birincil muhafaza her PCM anahtar toohello ON konumunu döndürerek açın.</span><span class="sxs-lookup"><span data-stu-id="b7195-112">Turn on hello primary enclosure by flipping each PCM switch toohello ON position.</span></span>
9. <span data-ttu-id="b7195-113">Merhaba sistem üzerinde LED'leri etkinleştirdiniz hello aygıt denetleyicisi sağlayarak olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="b7195-113">Verify that hello system is on by ensuring hello device controller LEDs have turned ON.</span></span>
10. <span data-ttu-id="b7195-114">Merhaba dört LED'leri sonraki toohello SAS bağlantı noktasına hello EBOD denetleyicisi yeşil olup olmadığını doğrulayarak hello EBOD denetleyicisi hello aygıt denetleyicisi arasındaki Hello bağlantı etkin olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="b7195-114">Make sure that hello connection between hello EBOD controller and hello device controller is active by verifying that hello four LEDs next toohello SAS port on hello EBOD controller are green.</span></span>
    
    > [!IMPORTANT]
    > <span data-ttu-id="b7195-115">tooensure sisteminiz için yüksek kullanılabilirlik, kesinlikle toohello güç düzeni diyagramı aşağıdaki hello gösterilen kablolama uyması öneririz.</span><span class="sxs-lookup"><span data-stu-id="b7195-115">tooensure high availability for your system, we recommend that you strictly adhere toohello power cabling scheme shown in hello following diagram.</span></span>
    > 
    > 
    
    ![Kabloyla 4U cihazınızın güç bağlantısını yapma](./media/storsimple-cable-8600-for-power/HCSCableYour4UDeviceforPower.png)
    
    <span data-ttu-id="b7195-117">**Güç kabloları**</span><span class="sxs-lookup"><span data-stu-id="b7195-117">**Power cabling**</span></span>
    
    | <span data-ttu-id="b7195-118">Etiket</span><span class="sxs-lookup"><span data-stu-id="b7195-118">Label</span></span> | <span data-ttu-id="b7195-119">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b7195-119">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="b7195-120">1</span><span class="sxs-lookup"><span data-stu-id="b7195-120">1</span></span> |<span data-ttu-id="b7195-121">Birincil kasası</span><span class="sxs-lookup"><span data-stu-id="b7195-121">Primary enclosure</span></span> |
    | <span data-ttu-id="b7195-122">2</span><span class="sxs-lookup"><span data-stu-id="b7195-122">2</span></span> |<span data-ttu-id="b7195-123">PCM 0</span><span class="sxs-lookup"><span data-stu-id="b7195-123">PCM 0</span></span> |
    | <span data-ttu-id="b7195-124">3</span><span class="sxs-lookup"><span data-stu-id="b7195-124">3</span></span> |<span data-ttu-id="b7195-125">PCM 1</span><span class="sxs-lookup"><span data-stu-id="b7195-125">PCM 1</span></span> |
    | <span data-ttu-id="b7195-126">4</span><span class="sxs-lookup"><span data-stu-id="b7195-126">4</span></span> |<span data-ttu-id="b7195-127">Denetleyici 0</span><span class="sxs-lookup"><span data-stu-id="b7195-127">Controller 0</span></span> |
    | <span data-ttu-id="b7195-128">5</span><span class="sxs-lookup"><span data-stu-id="b7195-128">5</span></span> |<span data-ttu-id="b7195-129">Denetleyici 1</span><span class="sxs-lookup"><span data-stu-id="b7195-129">Controller 1</span></span> |
    | <span data-ttu-id="b7195-130">6</span><span class="sxs-lookup"><span data-stu-id="b7195-130">6</span></span> |<span data-ttu-id="b7195-131">EBOD denetleyici 0</span><span class="sxs-lookup"><span data-stu-id="b7195-131">EBOD controller 0</span></span> |
    | <span data-ttu-id="b7195-132">7</span><span class="sxs-lookup"><span data-stu-id="b7195-132">7</span></span> |<span data-ttu-id="b7195-133">EBOD Denetleyici 1</span><span class="sxs-lookup"><span data-stu-id="b7195-133">EBOD controller 1</span></span> |
    | <span data-ttu-id="b7195-134">8</span><span class="sxs-lookup"><span data-stu-id="b7195-134">8</span></span> |<span data-ttu-id="b7195-135">EBOD muhafazası</span><span class="sxs-lookup"><span data-stu-id="b7195-135">EBOD enclosure</span></span> |
    | <span data-ttu-id="b7195-136">9</span><span class="sxs-lookup"><span data-stu-id="b7195-136">9</span></span> |<span data-ttu-id="b7195-137">PDU</span><span class="sxs-lookup"><span data-stu-id="b7195-137">PDUs</span></span> |

