<!--author=alkohli last changed: 9/16/15-->


#### <a name="to-cable-your-device-for-power"></a><span data-ttu-id="d835f-101">Cihazınızı güç kablosu için</span><span class="sxs-lookup"><span data-stu-id="d835f-101">To cable your device for power</span></span>
> [!NOTE]
> <span data-ttu-id="d835f-102">StorSimple Cihazınızda iki kasaları yedekli PCMs içerir.</span><span class="sxs-lookup"><span data-stu-id="d835f-102">Both enclosures on your StorSimple device include redundant PCMs.</span></span> <span data-ttu-id="d835f-103">Her kasa için PCMs yüklü ve yüksek kullanılabilirlik sağlamak için farklı güç kaynaklarına bağlandınız.</span><span class="sxs-lookup"><span data-stu-id="d835f-103">For each enclosure, the PCMs must be installed and connected to different power sources to ensure high availability.</span></span>
> 
> 

1. <span data-ttu-id="d835f-104">Tüm PCMs güç anahtarlarda OFF konumunda olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="d835f-104">Make sure that the power switches on all the PCMs are in the OFF position.</span></span>
2. <span data-ttu-id="d835f-105">Birincil muhafaza güç kablosu her iki PCMs bağlayın.</span><span class="sxs-lookup"><span data-stu-id="d835f-105">On the primary enclosure, connect the power cords to both PCMs.</span></span> <span data-ttu-id="d835f-106">Güç kablosu altına güç kablo diyagramdaki kırmızı tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="d835f-106">The power cords are identified in red in the power cabling diagram, below.</span></span>
3. <span data-ttu-id="d835f-107">Birincil kasada iki PCMs ayrı güç kaynakları kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="d835f-107">Make sure that the two PCMs on the primary enclosure use separate power sources.</span></span>
4. <span data-ttu-id="d835f-108">Güç kablosu raf dağıtım birimleri açma diyagramı kablo güç gösterildiği gibi iliştirin.</span><span class="sxs-lookup"><span data-stu-id="d835f-108">Attach the power cords to the power on the rack distribution units as shown in the power cabling diagram.</span></span>
5. <span data-ttu-id="d835f-109">EBOD muhafazası için 2-4 arasındaki adımları yineleyin.</span><span class="sxs-lookup"><span data-stu-id="d835f-109">Repeat steps 2 through 4 for the EBOD enclosure.</span></span>
6. <span data-ttu-id="d835f-110">EBOD muhafazası ON konumuna her PCM üzerinde güç düğmesi döndürerek açın.</span><span class="sxs-lookup"><span data-stu-id="d835f-110">Turn on the EBOD enclosure by flipping the power switch on each PCM to the ON position.</span></span>
7. <span data-ttu-id="d835f-111">EBOD muhafazası EBOD denetleyicisi arkasında yeşil LED'leri ON işaretlidir denetleyerek açık olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="d835f-111">Verify that the EBOD enclosure is turned on by checking that the green LEDs on the back of the EBOD controller are turned ON.</span></span>
8. <span data-ttu-id="d835f-112">Birincil muhafaza ON konuma her PCM anahtar döndürerek açın.</span><span class="sxs-lookup"><span data-stu-id="d835f-112">Turn on the primary enclosure by flipping each PCM switch to the ON position.</span></span>
9. <span data-ttu-id="d835f-113">Sistem üzerinde LED'leri açık olan aygıt denetleyicisi sağlayarak olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="d835f-113">Verify that the system is on by ensuring the device controller LEDs have turned ON.</span></span>
10. <span data-ttu-id="d835f-114">Dört LED'leri EBOD denetleyicisi SAS bağlantı noktasını yanındaki yeşil olup olmadığını doğrulayarak EBOD denetleyicisi ve cihaz denetleyicisi arasındaki bağlantıyı etkin olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="d835f-114">Make sure that the connection between the EBOD controller and the device controller is active by verifying that the four LEDs next to the SAS port on the EBOD controller are green.</span></span>
    
    > [!IMPORTANT]
    > <span data-ttu-id="d835f-115">Sisteminiz için yüksek kullanılabilirlik sağlamak için kesinlikle Aşağıdaki diyagramda gösterildiği düzeni kablo güç izliyor olduğunuz olmasını öneririz.</span><span class="sxs-lookup"><span data-stu-id="d835f-115">To ensure high availability for your system, we recommend that you strictly adhere to the power cabling scheme shown in the following diagram.</span></span>
    > 
    > 
    
    ![Kabloyla 4U cihazınızın güç bağlantısını yapma](./media/storsimple-cable-8600-for-power/HCSCableYour4UDeviceforPower.png)
    
    <span data-ttu-id="d835f-117">**Güç kabloları**</span><span class="sxs-lookup"><span data-stu-id="d835f-117">**Power cabling**</span></span>
    
    | <span data-ttu-id="d835f-118">Etiket</span><span class="sxs-lookup"><span data-stu-id="d835f-118">Label</span></span> | <span data-ttu-id="d835f-119">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d835f-119">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="d835f-120">1</span><span class="sxs-lookup"><span data-stu-id="d835f-120">1</span></span> |<span data-ttu-id="d835f-121">Birincil kasası</span><span class="sxs-lookup"><span data-stu-id="d835f-121">Primary enclosure</span></span> |
    | <span data-ttu-id="d835f-122">2</span><span class="sxs-lookup"><span data-stu-id="d835f-122">2</span></span> |<span data-ttu-id="d835f-123">PCM 0</span><span class="sxs-lookup"><span data-stu-id="d835f-123">PCM 0</span></span> |
    | <span data-ttu-id="d835f-124">3</span><span class="sxs-lookup"><span data-stu-id="d835f-124">3</span></span> |<span data-ttu-id="d835f-125">PCM 1</span><span class="sxs-lookup"><span data-stu-id="d835f-125">PCM 1</span></span> |
    | <span data-ttu-id="d835f-126">4</span><span class="sxs-lookup"><span data-stu-id="d835f-126">4</span></span> |<span data-ttu-id="d835f-127">Denetleyici 0</span><span class="sxs-lookup"><span data-stu-id="d835f-127">Controller 0</span></span> |
    | <span data-ttu-id="d835f-128">5</span><span class="sxs-lookup"><span data-stu-id="d835f-128">5</span></span> |<span data-ttu-id="d835f-129">Denetleyici 1</span><span class="sxs-lookup"><span data-stu-id="d835f-129">Controller 1</span></span> |
    | <span data-ttu-id="d835f-130">6</span><span class="sxs-lookup"><span data-stu-id="d835f-130">6</span></span> |<span data-ttu-id="d835f-131">EBOD denetleyici 0</span><span class="sxs-lookup"><span data-stu-id="d835f-131">EBOD controller 0</span></span> |
    | <span data-ttu-id="d835f-132">7</span><span class="sxs-lookup"><span data-stu-id="d835f-132">7</span></span> |<span data-ttu-id="d835f-133">EBOD Denetleyici 1</span><span class="sxs-lookup"><span data-stu-id="d835f-133">EBOD controller 1</span></span> |
    | <span data-ttu-id="d835f-134">8</span><span class="sxs-lookup"><span data-stu-id="d835f-134">8</span></span> |<span data-ttu-id="d835f-135">EBOD muhafazası</span><span class="sxs-lookup"><span data-stu-id="d835f-135">EBOD enclosure</span></span> |
    | <span data-ttu-id="d835f-136">9</span><span class="sxs-lookup"><span data-stu-id="d835f-136">9</span></span> |<span data-ttu-id="d835f-137">PDU</span><span class="sxs-lookup"><span data-stu-id="d835f-137">PDUs</span></span> |

