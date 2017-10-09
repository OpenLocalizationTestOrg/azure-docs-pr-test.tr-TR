

![Sanal makinelerde tek başına bulut hizmeti](./media/virtual-machines-common-classic-connect-vms/CloudServiceExample.png)

<span data-ttu-id="a0964-102">Bir sanal ağ, sanal makineleriniz yerleştirirseniz toouse için istediğiniz kaç bulut Hizmetleri Yük Dengeleme ve kullanılabilirlik kümeleri karar verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a0964-102">If you place your virtual machines in a virtual network, you can decide how many cloud services you want toouse for load balancing and availability sets.</span></span> <span data-ttu-id="a0964-103">Ayrıca, hello sanal makineleri düzenleyebilirsiniz hello ağlardaki aynı şekilde şirket içi ağ ve hello sanal ağ tooyour bağlanın ağ şirket.</span><span class="sxs-lookup"><span data-stu-id="a0964-103">Additionally, you can organize hello virtual machines on subnets in hello same way as your on-premises network and connect hello virtual network tooyour on-premises network.</span></span> <span data-ttu-id="a0964-104">Örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="a0964-104">Here's an example:</span></span>

![Bir sanal ağdaki sanal makineler](./media/virtual-machines-common-classic-connect-vms/VirtualNetworkExample.png)

<span data-ttu-id="a0964-106">Azure'da yolu tooconnect sanal makineler önerilen hello sanal ağlardır.</span><span class="sxs-lookup"><span data-stu-id="a0964-106">Virtual networks are hello recommended way tooconnect virtual machines in Azure.</span></span> <span data-ttu-id="a0964-107">Merhaba en iyi uygulama her katman ayrı bulut hizmetinde, uygulamanızın tooconfigure olduğu.</span><span class="sxs-lookup"><span data-stu-id="a0964-107">hello best practice is tooconfigure each tier of your application in a separate cloud service.</span></span> <span data-ttu-id="a0964-108">Ancak, bazı sanal makineler toocombine gerekebilir farklı uygulama katmanlarındaki hello içine hizmet tooremain hello en fazla abonelik başına 200 bulut Hizmetleri içinde aynı bulut.</span><span class="sxs-lookup"><span data-stu-id="a0964-108">However, you may need toocombine some virtual machines from different application tiers into hello same cloud service tooremain within hello maximum of 200 cloud services per subscription.</span></span> <span data-ttu-id="a0964-109">Bu ve diğer sınırları tooreview bkz [Azure aboneliği ve hizmet sınırları, kotaları ve kısıtlamaları](../articles/azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="a0964-109">tooreview this and other limits, see [Azure Subscription and Service Limits, Quotas, and Constraints](../articles/azure-subscription-service-limits.md).</span></span>

## <a name="connect-vms-in-a-virtual-network"></a><span data-ttu-id="a0964-110">Sanal makineleri sanal bir ağa bağlan</span><span class="sxs-lookup"><span data-stu-id="a0964-110">Connect VMs in a virtual network</span></span>
<span data-ttu-id="a0964-111">bir sanal ağdaki sanal makinelerden tooconnect:</span><span class="sxs-lookup"><span data-stu-id="a0964-111">tooconnect virtual machines in a virtual network:</span></span>

1. <span data-ttu-id="a0964-112">Hello Hello sanal ağ oluşturma [Azure portal](../articles/virtual-network/virtual-networks-create-vnet-classic-pportal.md) ve 'Klasik dağıtım' belirtin.</span><span class="sxs-lookup"><span data-stu-id="a0964-112">Create hello virtual network in hello [Azure portal](../articles/virtual-network/virtual-networks-create-vnet-classic-pportal.md) and specify 'classic deployment'.</span></span>
2. <span data-ttu-id="a0964-113">Tasarımınız kullanılabilirlik kümeleri için dağıtım tooreflect için bulut hizmetlerini Hello kümesi oluşturun ve Yük Dengeleme.</span><span class="sxs-lookup"><span data-stu-id="a0964-113">Create hello set of cloud services for your deployment tooreflect your design for availability sets and load balancing.</span></span> <span data-ttu-id="a0964-114">Hello Azure portal'ı tıklatın **yeni > işlem > bulut hizmeti** her bir bulut hizmeti için.</span><span class="sxs-lookup"><span data-stu-id="a0964-114">In hello Azure portal, click **New > Compute > Cloud service** for each cloud service.</span></span>

  <span data-ttu-id="a0964-115">Merhaba bulut hizmetinin ayrıntılarını dolgu olarak seçin aynı hello _kaynak grubu_ hello sanal ağ ile kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a0964-115">As you fill out hello cloud service details, choose hello same _resource group_ used with hello virtual network.</span></span>

3. <span data-ttu-id="a0964-116">toocreate her yeni sanal makine, tıklatın **yeni > işlem**, hello uygun VM görüntüsünü seçin hello sonra **öne çıkan uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="a0964-116">toocreate each new virtual machine, click **New > Compute**, then select hello appropriate VM image from hello **Featured apps**.</span></span>

  <span data-ttu-id="a0964-117">Merhaba VM içinde **Temelleri** dikey penceresinde, seçin aynı hello _kaynak grubu_ hello sanal ağ ile kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a0964-117">In hello VM **Basics** blade, choose hello same _resource group_ used with hello virtual network.</span></span>

  ![Bir sanal ağ kullanırken VM temel bilgileri dikey penceresi](./media/virtual-machines-common-classic-connect-vms/CreateVM_Basics_VN.png)

4. <span data-ttu-id="a0964-119">VM hello dolgu olarak **ayarları**, doğru hello seçin _bulut hizmeti_ veya _sanal ağ_ hello VM için.</span><span class="sxs-lookup"><span data-stu-id="a0964-119">As you fill out hello VM **Settings**, choose hello correct _Cloud service_ or _virtual network_ for hello VM.</span></span>

  <span data-ttu-id="a0964-120">Azure öğesi seçiminize göre hello diğer seçer.</span><span class="sxs-lookup"><span data-stu-id="a0964-120">Azure will select hello other item based on your selection.</span></span>

  ![Bir sanal ağ kullanırken VM ayarlar dikey penceresi](./media/virtual-machines-common-classic-connect-vms/CreateVM_Settings_VN.png)


## <a name="connect-vms-in-a-standalone-cloud-service"></a><span data-ttu-id="a0964-122">Sanal makineleri bir tek başına bulut hizmetine bağlanmak</span><span class="sxs-lookup"><span data-stu-id="a0964-122">Connect VMs in a standalone cloud service</span></span>
<span data-ttu-id="a0964-123">tooconnect sanal makinelerde tek başına bulut hizmeti:</span><span class="sxs-lookup"><span data-stu-id="a0964-123">tooconnect virtual machines in a standalone cloud service:</span></span>

1. <span data-ttu-id="a0964-124">Hello Hello bulut hizmeti Oluştur [Azure portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a0964-124">Create hello cloud service in hello [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="a0964-125">Tıklatın **yeni > işlem > bulut hizmeti**.</span><span class="sxs-lookup"><span data-stu-id="a0964-125">Click **New > Compute > Cloud service**.</span></span> <span data-ttu-id="a0964-126">Veya, ilk sanal makine oluşturduğunuzda, dağıtımınız için hello bulut hizmeti oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="a0964-126">Or, you can create hello cloud service for your deployment when you create your first virtual machine.</span></span>
2. <span data-ttu-id="a0964-127">Merhaba sanal makineleri oluştururken hello bulut hizmetiyle aynı kaynak grubunda kullanılan hello seçin.</span><span class="sxs-lookup"><span data-stu-id="a0964-127">When you create hello virtual machines, choose hello same resource group used with hello cloud service.</span></span>

  ![Bir sanal makine tooan mevcut bulut hizmeti Ekle](./media/virtual-machines-common-classic-connect-vms/CreateVM_Basics_SA.png)

3.  <span data-ttu-id="a0964-129">Merhaba VM ayrıntılarını doldukça hello hello ilk adımda oluşturduğunuz bulut hizmeti adını seçin.</span><span class="sxs-lookup"><span data-stu-id="a0964-129">As you fill out hello VM details, choose hello name of cloud service created in hello first step.</span></span>

  ![Bir sanal makine için bir bulut hizmeti seçme](./media/virtual-machines-common-classic-connect-vms/CreateVM_Settings_SA.png)
