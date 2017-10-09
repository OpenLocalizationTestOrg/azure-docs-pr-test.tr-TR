### <span data-ttu-id="fbfe0-101"><a name="noconnection"></a>toomodify yerel ağ geçidi IP adresi öneklerini - ağ geçidi bağlantısı yok</span><span class="sxs-lookup"><span data-stu-id="fbfe0-101"><a name="noconnection"></a>toomodify local network gateway IP address prefixes - no gateway connection</span></span>

#### <a name="tooadd-additional-address-prefixes"></a><span data-ttu-id="fbfe0-102">tooadd ek adres öneklerini:</span><span class="sxs-lookup"><span data-stu-id="fbfe0-102">tooadd additional address prefixes:</span></span>

1. <span data-ttu-id="fbfe0-103">Merhaba yerel ağ geçidi kaynağında hello üzerinde **ayarları** 'yi tıklatın **yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="fbfe0-103">On hello Local Network Gateway resource, in hello **Settings** section, click **Configuration**.</span></span>
2. <span data-ttu-id="fbfe0-104">Hello Hello IP adres alanı Ekle *ek adres aralığı Ekle* kutusu.</span><span class="sxs-lookup"><span data-stu-id="fbfe0-104">Add hello IP address space in hello *Add additional address range* box.</span></span>
3. <span data-ttu-id="fbfe0-105">Tıklatın **kaydetmek** toosave ayarlarınızı.</span><span class="sxs-lookup"><span data-stu-id="fbfe0-105">Click **Save** toosave your settings.</span></span>

#### <a name="tooremove-address-prefixes"></a><span data-ttu-id="fbfe0-106">tooremove adres öneklerini:</span><span class="sxs-lookup"><span data-stu-id="fbfe0-106">tooremove address prefixes:</span></span>

1. <span data-ttu-id="fbfe0-107">Merhaba yerel ağ geçidi kaynağında hello üzerinde **ayarları** 'yi tıklatın **yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="fbfe0-107">On hello Local Network Gateway resource, in hello **Settings** section, click **Configuration**.</span></span>
2. <span data-ttu-id="fbfe0-108">Merhaba tıklatın **'...'** hello önek içeren hello satırda tooremove istiyor.</span><span class="sxs-lookup"><span data-stu-id="fbfe0-108">Click hello **'...'** on hello line containing hello prefix you want tooremove.</span></span>
3. <span data-ttu-id="fbfe0-109">Tıklatın **kaldırmak**.</span><span class="sxs-lookup"><span data-stu-id="fbfe0-109">Click **Remove**.</span></span>
4. <span data-ttu-id="fbfe0-110">Tıklatın **kaydetmek** toosave ayarlarınızı.</span><span class="sxs-lookup"><span data-stu-id="fbfe0-110">Click **Save** toosave your settings.</span></span>

### <span data-ttu-id="fbfe0-111"><a name="withconnection"></a>ağ geçidi bağlantısı varolan toomodify yerel ağ geçidi IP adresi öneklerini-</span><span class="sxs-lookup"><span data-stu-id="fbfe0-111"><a name="withconnection"></a>toomodify local network gateway IP address prefixes - existing gateway connection</span></span>

<span data-ttu-id="fbfe0-112">Bir ağ geçidi bağlantısına sahip ve tooadd istediğiniz veya yerel ağ geçidinizinde başlangıç IP adresi öneklerini kaldırırsanız, aşağıdaki adımları sırayla toodo hello gerekir.</span><span class="sxs-lookup"><span data-stu-id="fbfe0-112">If you have a gateway connection and want tooadd or remove hello IP address prefixes contained in your local network gateway, you need toodo hello following steps, in order.</span></span> <span data-ttu-id="fbfe0-113">Bunun sonucunda, VPN bağlantınızda kesinti oluşur.</span><span class="sxs-lookup"><span data-stu-id="fbfe0-113">This results in some downtime for your VPN connection.</span></span> <span data-ttu-id="fbfe0-114">IP adres öneklerini değiştirirken toodelete hello VPN ağ geçidi gerekmez.</span><span class="sxs-lookup"><span data-stu-id="fbfe0-114">When modifying IP address prefixes, you don't need toodelete hello VPN gateway.</span></span> <span data-ttu-id="fbfe0-115">Yalnızca tooremove hello bağlantı gerekir.</span><span class="sxs-lookup"><span data-stu-id="fbfe0-115">You only need tooremove hello connection.</span></span>

#### <a name="1-remove-hello-connection"></a><span data-ttu-id="fbfe0-116">1. Merhaba bağlantısını kaldırın.</span><span class="sxs-lookup"><span data-stu-id="fbfe0-116">1. Remove hello connection.</span></span>

1. <span data-ttu-id="fbfe0-117">Merhaba yerel ağ geçidi kaynağında hello üzerinde **ayarları** 'yi tıklatın **bağlantıları**.</span><span class="sxs-lookup"><span data-stu-id="fbfe0-117">On hello Local Network Gateway resource, in hello **Settings** section, click **Connections**.</span></span>
2. <span data-ttu-id="fbfe0-118">Merhaba tıklatın **...**  her bağlantı hello satırında, ardından **silmek**.</span><span class="sxs-lookup"><span data-stu-id="fbfe0-118">Click hello **...** on hello line for each connection, then click **Delete**.</span></span>
3. <span data-ttu-id="fbfe0-119">Tıklatın **kaydetmek** toosave ayarlarınızı.</span><span class="sxs-lookup"><span data-stu-id="fbfe0-119">Click **Save** toosave your settings.</span></span>

#### <a name="2-modify-hello-address-prefixes"></a><span data-ttu-id="fbfe0-120">2. Merhaba adres öneklerini değiştirme.</span><span class="sxs-lookup"><span data-stu-id="fbfe0-120">2. Modify hello address prefixes.</span></span>

<span data-ttu-id="fbfe0-121">tooadd ek adres öneklerini:</span><span class="sxs-lookup"><span data-stu-id="fbfe0-121">tooadd additional address prefixes:</span></span>

1. <span data-ttu-id="fbfe0-122">Merhaba yerel ağ geçidi kaynağında hello üzerinde **ayarları** 'yi tıklatın **yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="fbfe0-122">On hello Local Network Gateway resource, in hello **Settings** section, click **Configuration**.</span></span>
2. <span data-ttu-id="fbfe0-123">Başlangıç IP adresi alanı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="fbfe0-123">Add hello IP address space.</span></span>
3. <span data-ttu-id="fbfe0-124">Tıklatın **kaydetmek** toosave ayarlarınızı.</span><span class="sxs-lookup"><span data-stu-id="fbfe0-124">Click **Save** toosave your settings.</span></span>

<span data-ttu-id="fbfe0-125">tooremove adres öneklerini:</span><span class="sxs-lookup"><span data-stu-id="fbfe0-125">tooremove address prefixes:</span></span>

1. <span data-ttu-id="fbfe0-126">Merhaba yerel ağ geçidi kaynağında hello üzerinde **ayarları** 'yi tıklatın **yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="fbfe0-126">On hello Local Network Gateway resource, in hello **Settings** section, click **Configuration**.</span></span>
2. <span data-ttu-id="fbfe0-127">Merhaba tıklatın **...**  hello önek içeren hello satırda tooremove istiyor.</span><span class="sxs-lookup"><span data-stu-id="fbfe0-127">Click hello **...** on hello line containing hello prefix you want tooremove.</span></span>
3. <span data-ttu-id="fbfe0-128">Tıklatın **kaldırmak**.</span><span class="sxs-lookup"><span data-stu-id="fbfe0-128">Click **Remove**.</span></span>
4. <span data-ttu-id="fbfe0-129">Tıklatın **kaydetmek** toosave ayarlarınızı.</span><span class="sxs-lookup"><span data-stu-id="fbfe0-129">Click **Save** toosave your settings.</span></span>

#### <a name="3-recreate-hello-connection"></a><span data-ttu-id="fbfe0-130">3. Merhaba bağlantısını yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fbfe0-130">3. Recreate hello connection.</span></span>

1. <span data-ttu-id="fbfe0-131">Sanal ağ geçidi toohello ağınız için gidin.</span><span class="sxs-lookup"><span data-stu-id="fbfe0-131">Navigate toohello Virtual Network Gateway for your VNet.</span></span> <span data-ttu-id="fbfe0-132">(Değil hello yerel ağ geçidi.)</span><span class="sxs-lookup"><span data-stu-id="fbfe0-132">(Not hello Local Network Gateway.)</span></span>
2. <span data-ttu-id="fbfe0-133">Merhaba hello sanal ağ geçidi üzerinde **ayarları** 'yi tıklatın **bağlantıları**.</span><span class="sxs-lookup"><span data-stu-id="fbfe0-133">On hello Virtual Network Gateway, in hello **Settings** section, click **Connections**.</span></span>
3. <span data-ttu-id="fbfe0-134">Merhaba tıklatın **+ Ekle** tooopen hello **Bağlantı Ekle** dikey.</span><span class="sxs-lookup"><span data-stu-id="fbfe0-134">Click hello **+ Add** tooopen hello **Add connection** blade.</span></span>
4. <span data-ttu-id="fbfe0-135">Bağlantınızı yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fbfe0-135">Recreate your connection.</span></span>
5. <span data-ttu-id="fbfe0-136">Tıklatın **Tamam** toocreate hello bağlantı.</span><span class="sxs-lookup"><span data-stu-id="fbfe0-136">Click **OK** toocreate hello connection.</span></span>
