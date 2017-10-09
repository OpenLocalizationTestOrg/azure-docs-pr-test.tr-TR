#### <a name="toocreate-public-endpoints-on-hello-cloud-appliance"></a><span data-ttu-id="a70da-101">toocreate genel Uç noktalara hello bulut uygulaması</span><span class="sxs-lookup"><span data-stu-id="a70da-101">toocreate public endpoints on hello cloud appliance</span></span>

1. <span data-ttu-id="a70da-102">Toohello Azure portalında oturum açın.</span><span class="sxs-lookup"><span data-stu-id="a70da-102">Sign in toohello Azure portal.</span></span>
2. <span data-ttu-id="a70da-103">Çok Git**sanal makineleri**, seçin ve bulut uygulaması olarak kullanılan hello sanal makineye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a70da-103">Go too**Virtual Machines**, and then select and click hello virtual machine that is being used as your cloud appliance.</span></span>
    
3. <span data-ttu-id="a70da-104">Sanal makineniz ve bu moddan toocreate bir ağ güvenlik grubu (NSG) kural toocontrol hello trafik akışını gerekir.</span><span class="sxs-lookup"><span data-stu-id="a70da-104">You need toocreate a network security group (NSG) rule toocontrol hello flow of traffic in and out of your virtual machine.</span></span> <span data-ttu-id="a70da-105">Aşağıdaki adımları toocreate bir NSG kuralı hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="a70da-105">Perform hello following steps toocreate an NSG rule.</span></span>
    1. <span data-ttu-id="a70da-106">**Ağ güvenlik grubu**’nu seçin.</span><span class="sxs-lookup"><span data-stu-id="a70da-106">Select **Network security group**.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt1.png)

    2. <span data-ttu-id="a70da-107">Sunulan hello varsayılan ağ güvenlik grubunu tıklatın.</span><span class="sxs-lookup"><span data-stu-id="a70da-107">Click hello default network security group that is presented.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt2.png)

    3. <span data-ttu-id="a70da-108">**Gelen güvenlik kuralları**’nı seçin.</span><span class="sxs-lookup"><span data-stu-id="a70da-108">Select **Inbound security rules**.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt3.png)

    4. <span data-ttu-id="a70da-109">Tıklatın **+ Ekle** toocreate bir gelen güvenlik kuralı.</span><span class="sxs-lookup"><span data-stu-id="a70da-109">Click **+ Add** toocreate an inbound security rule.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt4.png)

        <span data-ttu-id="a70da-110">Merhaba Ekle gelen güvenlik kuralı dikey penceresinde:</span><span class="sxs-lookup"><span data-stu-id="a70da-110">In hello Add inbound security rule blade:</span></span>

        1. <span data-ttu-id="a70da-111">Hello için **adı**, türü hello aşağıdaki hello uç noktası için ad: WinRMHttps.</span><span class="sxs-lookup"><span data-stu-id="a70da-111">For hello **Name**, type hello following name for hello endpoint: WinRMHttps.</span></span>
        
        2. <span data-ttu-id="a70da-112">Hello için **öncelik**seçin (Merhaba varsayılan kural hello önceliği olan) bir sayı 1000'den küçük.</span><span class="sxs-lookup"><span data-stu-id="a70da-112">For hello **Priority**, select a number lesser than 1000 (which is hello priority for hello default rule).</span></span> <span data-ttu-id="a70da-113">Daha yüksek hello değeri, düşük hello önceliği.</span><span class="sxs-lookup"><span data-stu-id="a70da-113">Higher hello value, lower hello priority.</span></span>

        3. <span data-ttu-id="a70da-114">Set hello **kaynak** çok**herhangi**.</span><span class="sxs-lookup"><span data-stu-id="a70da-114">Set hello **Source** too**Any**.</span></span>

        4. <span data-ttu-id="a70da-115">Hello için **hizmet**seçin **WinRM**.</span><span class="sxs-lookup"><span data-stu-id="a70da-115">For hello **Service**, select **WinRM**.</span></span> <span data-ttu-id="a70da-116">Merhaba **Protokolü** otomatik olarak çok ayarlanır**TCP** ve hello **bağlantı noktası aralığı** çok ayarlanır**5986**.</span><span class="sxs-lookup"><span data-stu-id="a70da-116">hello **Protocol** is automatically set too**TCP** and hello **Port range** is set too**5986**.</span></span>

        5. <span data-ttu-id="a70da-117">Tıklatın **Tamam** toocreate hello kuralı.</span><span class="sxs-lookup"><span data-stu-id="a70da-117">Click **OK** toocreate hello rule.</span></span>

            ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt5.png)

4. <span data-ttu-id="a70da-118">Ağınızda güvenlik grubunun bir alt ağ veya belirli bir ağ arabiriminde tooassociate, son adımdır.</span><span class="sxs-lookup"><span data-stu-id="a70da-118">Your final step is tooassociate your network security group with a subnet or a specific network interface.</span></span> <span data-ttu-id="a70da-119">Aşağıdaki adımları tooassociate hello bir alt ağ, ağ güvenlik grubuyla gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="a70da-119">Perform hello following steps tooassociate your network security group with a subnet.</span></span>
    1. <span data-ttu-id="a70da-120">Çok Git**alt ağlar**.</span><span class="sxs-lookup"><span data-stu-id="a70da-120">Go too**Subnets**.</span></span>
    2. <span data-ttu-id="a70da-121">**+ İlişkilendir**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a70da-121">Click **+ Associate**.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt7.png)

    3. <span data-ttu-id="a70da-122">Sanal ağınızı seçin ve ardından hello uygun alt ağ seçin.</span><span class="sxs-lookup"><span data-stu-id="a70da-122">Select your virtual network, and then select hello appropriate subnet.</span></span>
    4. <span data-ttu-id="a70da-123">Tıklatın **Tamam** toocreate hello kuralı.</span><span class="sxs-lookup"><span data-stu-id="a70da-123">Click **OK** toocreate hello rule.</span></span>

        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt11.png)

<span data-ttu-id="a70da-124">Merhaba kural oluşturulduktan sonra ayrıntıları toodetermine hello ortak sanal IP (VIP) adresini görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a70da-124">After hello rule is created, you can view its details toodetermine hello Public Virtual IP (VIP) address.</span></span> <span data-ttu-id="a70da-125">Bu adresini kaydedin.</span><span class="sxs-lookup"><span data-stu-id="a70da-125">Record this address.</span></span>


