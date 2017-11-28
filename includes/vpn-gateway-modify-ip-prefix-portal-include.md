### <span data-ttu-id="7f2d7-101"><a name="noconnection"></a>Yerel ağ geçidinin IP adresi ön eklerini değiştirmek için - ağ geçidi bağlantısı yok</span><span class="sxs-lookup"><span data-stu-id="7f2d7-101"><a name="noconnection"></a>To modify local network gateway IP address prefixes - no gateway connection</span></span>

#### <a name="to-add-additional-address-prefixes"></a><span data-ttu-id="7f2d7-102">Başka adres ön ekleri eklemek için:</span><span class="sxs-lookup"><span data-stu-id="7f2d7-102">To add additional address prefixes:</span></span>

1. <span data-ttu-id="7f2d7-103">Yerel ağ geçidi kaynağına içinde **ayarları** 'yi tıklatın **yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="7f2d7-103">On the Local Network Gateway resource, in the **Settings** section, click **Configuration**.</span></span>
2. <span data-ttu-id="7f2d7-104">IP adres alanı Ekle *ek adres aralığı Ekle* kutusu.</span><span class="sxs-lookup"><span data-stu-id="7f2d7-104">Add the IP address space in the *Add additional address range* box.</span></span>
3. <span data-ttu-id="7f2d7-105">Tıklatın **kaydetmek** ayarlarınızı kaydetmek için.</span><span class="sxs-lookup"><span data-stu-id="7f2d7-105">Click **Save** to save your settings.</span></span>

#### <a name="to-remove-address-prefixes"></a><span data-ttu-id="7f2d7-106">Adres ön eklerini kaldırmak için:</span><span class="sxs-lookup"><span data-stu-id="7f2d7-106">To remove address prefixes:</span></span>

1. <span data-ttu-id="7f2d7-107">Yerel ağ geçidi kaynağına içinde **ayarları** 'yi tıklatın **yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="7f2d7-107">On the Local Network Gateway resource, in the **Settings** section, click **Configuration**.</span></span>
2. <span data-ttu-id="7f2d7-108">Tıklatın **'...'**</span><span class="sxs-lookup"><span data-stu-id="7f2d7-108">Click the **'...'**</span></span> <span data-ttu-id="7f2d7-109">kaldırmak istediğiniz önek içeren satırı.</span><span class="sxs-lookup"><span data-stu-id="7f2d7-109">on the line containing the prefix you want to remove.</span></span>
3. <span data-ttu-id="7f2d7-110">Tıklatın **kaldırmak**.</span><span class="sxs-lookup"><span data-stu-id="7f2d7-110">Click **Remove**.</span></span>
4. <span data-ttu-id="7f2d7-111">Tıklatın **kaydetmek** ayarlarınızı kaydetmek için.</span><span class="sxs-lookup"><span data-stu-id="7f2d7-111">Click **Save** to save your settings.</span></span>

### <span data-ttu-id="7f2d7-112"><a name="withconnection"></a>Yerel ağ geçidinin IP adresi ön eklerini değiştirmek için - ağ geçidi bağlantısı var</span><span class="sxs-lookup"><span data-stu-id="7f2d7-112"><a name="withconnection"></a>To modify local network gateway IP address prefixes - existing gateway connection</span></span>

<span data-ttu-id="7f2d7-113">Ağ geçidi bağlantınız varsa ve yerel ağ geçidinizde bulunan IP adresi ön eklerini eklemek veya kaldırmak istiyorsanız aşağıdaki adımları sırasıyla uygulamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7f2d7-113">If you have a gateway connection and want to add or remove the IP address prefixes contained in your local network gateway, you need to do the following steps, in order.</span></span> <span data-ttu-id="7f2d7-114">Bunun sonucunda, VPN bağlantınızda kesinti oluşur.</span><span class="sxs-lookup"><span data-stu-id="7f2d7-114">This results in some downtime for your VPN connection.</span></span> <span data-ttu-id="7f2d7-115">IP adresi öneklerini değiştirirken, VPN ağ geçidini silmeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="7f2d7-115">When modifying IP address prefixes, you don't need to delete the VPN gateway.</span></span> <span data-ttu-id="7f2d7-116">Yalnızca bağlantıyı kaldırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7f2d7-116">You only need to remove the connection.</span></span>

#### <a name="1-remove-the-connection"></a><span data-ttu-id="7f2d7-117">1. Bağlantıyı kaldırın.</span><span class="sxs-lookup"><span data-stu-id="7f2d7-117">1. Remove the connection.</span></span>

1. <span data-ttu-id="7f2d7-118">Yerel ağ geçidi kaynağına içinde **ayarları** 'yi tıklatın **bağlantıları**.</span><span class="sxs-lookup"><span data-stu-id="7f2d7-118">On the Local Network Gateway resource, in the **Settings** section, click **Connections**.</span></span>
2. <span data-ttu-id="7f2d7-119">Tıklatın **...**  her bağlantı için satırda ardından **silmek**.</span><span class="sxs-lookup"><span data-stu-id="7f2d7-119">Click the **...** on the line for each connection, then click **Delete**.</span></span>
3. <span data-ttu-id="7f2d7-120">Tıklatın **kaydetmek** ayarlarınızı kaydetmek için.</span><span class="sxs-lookup"><span data-stu-id="7f2d7-120">Click **Save** to save your settings.</span></span>

#### <a name="2-modify-the-address-prefixes"></a><span data-ttu-id="7f2d7-121">2. Adres öneklerini değiştirme.</span><span class="sxs-lookup"><span data-stu-id="7f2d7-121">2. Modify the address prefixes.</span></span>

<span data-ttu-id="7f2d7-122">Başka adres ön ekleri eklemek için:</span><span class="sxs-lookup"><span data-stu-id="7f2d7-122">To add additional address prefixes:</span></span>

1. <span data-ttu-id="7f2d7-123">Yerel ağ geçidi kaynağına içinde **ayarları** 'yi tıklatın **yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="7f2d7-123">On the Local Network Gateway resource, in the **Settings** section, click **Configuration**.</span></span>
2. <span data-ttu-id="7f2d7-124">IP adres alanı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="7f2d7-124">Add the IP address space.</span></span>
3. <span data-ttu-id="7f2d7-125">Tıklatın **kaydetmek** ayarlarınızı kaydetmek için.</span><span class="sxs-lookup"><span data-stu-id="7f2d7-125">Click **Save** to save your settings.</span></span>

<span data-ttu-id="7f2d7-126">Adres ön eklerini kaldırmak için:</span><span class="sxs-lookup"><span data-stu-id="7f2d7-126">To remove address prefixes:</span></span>

1. <span data-ttu-id="7f2d7-127">Yerel ağ geçidi kaynağına içinde **ayarları** 'yi tıklatın **yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="7f2d7-127">On the Local Network Gateway resource, in the **Settings** section, click **Configuration**.</span></span>
2. <span data-ttu-id="7f2d7-128">Tıklatın **...**  kaldırmak istediğiniz önek içeren satırı üzerinde.</span><span class="sxs-lookup"><span data-stu-id="7f2d7-128">Click the **...** on the line containing the prefix you want to remove.</span></span>
3. <span data-ttu-id="7f2d7-129">Tıklatın **kaldırmak**.</span><span class="sxs-lookup"><span data-stu-id="7f2d7-129">Click **Remove**.</span></span>
4. <span data-ttu-id="7f2d7-130">Tıklatın **kaydetmek** ayarlarınızı kaydetmek için.</span><span class="sxs-lookup"><span data-stu-id="7f2d7-130">Click **Save** to save your settings.</span></span>

#### <a name="3-recreate-the-connection"></a><span data-ttu-id="7f2d7-131">3. Bağlantısını yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7f2d7-131">3. Recreate the connection.</span></span>

1. <span data-ttu-id="7f2d7-132">Sanal ağ geçidi için sanal ağınızı gidin.</span><span class="sxs-lookup"><span data-stu-id="7f2d7-132">Navigate to the Virtual Network Gateway for your VNet.</span></span> <span data-ttu-id="7f2d7-133">(Olmayan yerel ağ geçidi.)</span><span class="sxs-lookup"><span data-stu-id="7f2d7-133">(Not the Local Network Gateway.)</span></span>
2. <span data-ttu-id="7f2d7-134">Sanal ağ geçidi olarak **ayarları** 'yi tıklatın **bağlantıları**.</span><span class="sxs-lookup"><span data-stu-id="7f2d7-134">On the Virtual Network Gateway, in the **Settings** section, click **Connections**.</span></span>
3. <span data-ttu-id="7f2d7-135">Tıklatın **+ Ekle** açmak için **Bağlantı Ekle** dikey.</span><span class="sxs-lookup"><span data-stu-id="7f2d7-135">Click the **+ Add** to open the **Add connection** blade.</span></span>
4. <span data-ttu-id="7f2d7-136">Bağlantınızı yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7f2d7-136">Recreate your connection.</span></span>
5. <span data-ttu-id="7f2d7-137">Tıklatın **Tamam** bağlantı oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="7f2d7-137">Click **OK** to create the connection.</span></span>