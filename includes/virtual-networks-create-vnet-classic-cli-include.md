## <a name="how-toocreate-a-classic-vnet-using-azure-cli"></a><span data-ttu-id="4ea9e-101">Nasıl toocreate Azure CLI kullanarak Klasik VNet</span><span class="sxs-lookup"><span data-stu-id="4ea9e-101">How toocreate a classic VNet using Azure CLI</span></span>
<span data-ttu-id="4ea9e-102">Windows, Linux veya OSX çalıştıran herhangi bir bilgisayardan hello komut isteminden Azure kaynaklarınızı hello Azure CLI toomanage kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-102">You can use hello Azure CLI toomanage your Azure resources from hello command prompt from any computer running Windows, Linux, or OSX.</span></span> <span data-ttu-id="4ea9e-103">toocreate hello Azure CLI kullanarak VNet hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-103">toocreate a VNet by using hello Azure CLI, follow hello steps below.</span></span>

1. <span data-ttu-id="4ea9e-104">Azure CLI hiç kullanmadıysanız bkz [hello Azure CLI yükleyip](../articles/cli-install-nodejs.md) ve sonra Azure hesabınızı ve aboneliğinizi toohello noktaya hello talimatlarını izleyin.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-104">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../articles/cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="4ea9e-105">Merhaba çalıştırmak **azure ağ vnet oluşturma** komut toocreate VNet ve alt ağ, aşağıda gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-105">Run hello **azure network vnet create** command toocreate a VNet and a subnet, as shown below.</span></span> <span data-ttu-id="4ea9e-106">Merhaba çıktıdan sonra gösterilen hello listede kullanılan hello parametreler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-106">hello list shown after hello output explains hello parameters used.</span></span>
   
            azure network vnet create --vnet TestVNet -e 192.168.0.0 -i 16 -n FrontEnd -p 192.168.1.0 -r 24 -l "Central US"
   
    <span data-ttu-id="4ea9e-107">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="4ea9e-107">Expected output:</span></span>
   
            info:    Executing command network vnet create
            + Looking up network configuration
            + Looking up locations
            + Setting network configuration
            info:    network vnet create command OK
   
   * <span data-ttu-id="4ea9e-108">**--vnet**.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-108">**--vnet**.</span></span> <span data-ttu-id="4ea9e-109">Merhaba VNet toobe oluşturulan adı.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-109">Name of hello VNet toobe created.</span></span> <span data-ttu-id="4ea9e-110">Bizim senaryomuz için bu *TestVNet* ’tir.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-110">For our scenario, *TestVNet*</span></span>
   * <span data-ttu-id="4ea9e-111">**-e (veya--adres alanı)**.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-111">**-e (or --address-space)**.</span></span> <span data-ttu-id="4ea9e-112">VNet adres alanı.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-112">VNet address space.</span></span> <span data-ttu-id="4ea9e-113">Bizim senaryomuz için *192.168.0.0*</span><span class="sxs-lookup"><span data-stu-id="4ea9e-113">For our scenario, *192.168.0.0*</span></span>
   * <span data-ttu-id="4ea9e-114">**-i (veya - CIDR)**.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-114">**-i (or -cidr)**.</span></span> <span data-ttu-id="4ea9e-115">Ağ maskesi CIDR biçiminde.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-115">Network mask in CIDR format.</span></span> <span data-ttu-id="4ea9e-116">Bizim senaryomuz için *16*.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-116">For our scenario, *16*.</span></span>
   * <span data-ttu-id="4ea9e-117">**-n (veya--alt ağ adı**).</span><span class="sxs-lookup"><span data-stu-id="4ea9e-117">**-n (or --subnet-name**).</span></span> <span data-ttu-id="4ea9e-118">Merhaba ilk alt ağ adı.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-118">Name of hello first subnet.</span></span> <span data-ttu-id="4ea9e-119">Bizim senaryomuz için bu *FrontEnd* ’dir.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-119">For our scenario, *FrontEnd*.</span></span>
   * <span data-ttu-id="4ea9e-120">**-p (veya--alt başlangıç IP'sini)**.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-120">**-p (or --subnet-start-ip)**.</span></span> <span data-ttu-id="4ea9e-121">Alt ağ veya alt ağ adres alanı için başlangıç IP adresi.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-121">Starting IP address for subnet, or subnet address space.</span></span> <span data-ttu-id="4ea9e-122">Bizim senaryomuz için *192.168.1.0*.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-122">For our scenario, *192.168.1.0*.</span></span>
   * <span data-ttu-id="4ea9e-123">**-r (veya--alt ağ CIDR)**.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-123">**-r (or --subnet-cidr)**.</span></span> <span data-ttu-id="4ea9e-124">Alt ağ için CIDR biçiminde ağ maskesi.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-124">Network mask in CIDR format for subnet.</span></span> <span data-ttu-id="4ea9e-125">Bizim senaryomuz için *24*.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-125">For our scenario, *24*.</span></span>
   * <span data-ttu-id="4ea9e-126">**-l (veya --location)**.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-126">**-l (or --location)**.</span></span> <span data-ttu-id="4ea9e-127">Merhaba Vnet'in oluşturulacağı azure bölgesi.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-127">Azure region where hello VNet will be created.</span></span> <span data-ttu-id="4ea9e-128">Bizim senaryomuz için *Orta ABD*.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-128">For our scenario, *Central US*.</span></span>
3. <span data-ttu-id="4ea9e-129">Merhaba çalıştırmak **azure ağ sanal alt ağ oluşturmak** komutu toocreate aşağıda gösterildiği gibi bir alt ağ.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-129">Run hello **azure network vnet subnet create** command toocreate a subnet as shown below.</span></span> <span data-ttu-id="4ea9e-130">Merhaba çıktıdan sonra gösterilen hello listede kullanılan hello parametreler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-130">hello list shown after hello output explains hello parameters used.</span></span>
   
            azure network vnet subnet create -t TestVNet -n BackEnd -a 192.168.2.0/24
   
    <span data-ttu-id="4ea9e-131">Yukarıdaki hello komut için beklenen hello çıktı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="4ea9e-131">Here is hello expected output for hello command above:</span></span>
   
            info:    Executing command network vnet subnet create
            + Looking up network configuration
            + Creating subnet "BackEnd"
            + Setting network configuration
            + Looking up hello subnet "BackEnd"
            + Looking up network configuration
            data:    Name                            : BackEnd
            data:    Address prefix                  : 192.168.2.0/24
            info:    network vnet subnet create command OK
   
   * <span data-ttu-id="4ea9e-132">**-t (veya--vnet-ad**.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-132">**-t (or --vnet-name**.</span></span> <span data-ttu-id="4ea9e-133">Merhaba hello alt oluşturulacağı Vnet'in adı.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-133">Name of hello VNet where hello subnet will be created.</span></span> <span data-ttu-id="4ea9e-134">Bizim senaryomuz için bu *TestVNet* ’tir.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-134">For our scenario, *TestVNet*.</span></span>
   * <span data-ttu-id="4ea9e-135">**-n (veya --name)**.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-135">**-n (or --name)**.</span></span> <span data-ttu-id="4ea9e-136">Merhaba yeni alt ağ adı.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-136">Name of hello new subnet.</span></span> <span data-ttu-id="4ea9e-137">Bizim senaryomuz için *arka uç*.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-137">For our scenario, *BackEnd*.</span></span>
   * <span data-ttu-id="4ea9e-138">**-a (veya--adres-önek)**.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-138">**-a (or --address-prefix)**.</span></span> <span data-ttu-id="4ea9e-139">Alt ağ CIDR bloğu.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-139">Subnet CIDR block.</span></span> <span data-ttu-id="4ea9e-140">Dört bizim senaryomuz *192.168.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-140">Four our scenario, *192.168.2.0/24*.</span></span>
4. <span data-ttu-id="4ea9e-141">Merhaba çalıştırmak **azure ağ vnet show** aşağıda gösterildiği gibi tooview hello hello yeni vnet'in özelliklerini komutu.</span><span class="sxs-lookup"><span data-stu-id="4ea9e-141">Run hello **azure network vnet show** command tooview hello properties of hello new vnet, as shown below.</span></span>
   
            azure network vnet show
   
    <span data-ttu-id="4ea9e-142">Yukarıdaki hello komut için beklenen hello çıktı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="4ea9e-142">Here is hello expected output for hello command above:</span></span>
   
            info:    Executing command network vnet show
            Virtual network name: TestVNet
            + Looking up hello virtual network sites
            data:    Name                            : TestVNet
            data:    Location                        : Central US
            data:    State                           : Created
            data:    Address space                   : 192.168.0.0/16
            data:    Subnets:
            data:      Name                          : FrontEnd
            data:      Address prefix                : 192.168.1.0/24
            data:
            data:      Name                          : BackEnd
            data:      Address prefix                : 192.168.2.0/24
            data:
            info:    network vnet show command OK

