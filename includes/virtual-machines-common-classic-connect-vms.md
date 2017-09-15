

![Sanal makinelerde tek başına bulut hizmeti](./media/virtual-machines-common-classic-connect-vms/CloudServiceExample.png)

<span data-ttu-id="d2655-102">Bir sanal ağ, sanal makineleriniz yerleştirirseniz kaç bulut Hizmetleri için kullanmak istediğiniz yük dengeleme ve kullanılabilirlik kümeleri karar verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d2655-102">If you place your virtual machines in a virtual network, you can decide how many cloud services you want to use for load balancing and availability sets.</span></span> <span data-ttu-id="d2655-103">Ayrıca, şirket içi ağ ve sanal ağı şirket içi ağınıza bağlanmak ağlardaki sanal makineler aynı şekilde düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d2655-103">Additionally, you can organize the virtual machines on subnets in the same way as your on-premises network and connect the virtual network to your on-premises network.</span></span> <span data-ttu-id="d2655-104">Örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="d2655-104">Here's an example:</span></span>

![Bir sanal ağdaki sanal makineler](./media/virtual-machines-common-classic-connect-vms/VirtualNetworkExample.png)

<span data-ttu-id="d2655-106">Sanal ağlar, Azure sanal makinelere bağlanmak için önerilen yoldur.</span><span class="sxs-lookup"><span data-stu-id="d2655-106">Virtual networks are the recommended way to connect virtual machines in Azure.</span></span> <span data-ttu-id="d2655-107">En iyi uygulama olarak, her katman, uygulamanızın ayrı bulut hizmetinde yapılandırmaktır.</span><span class="sxs-lookup"><span data-stu-id="d2655-107">The best practice is to configure each tier of your application in a separate cloud service.</span></span> <span data-ttu-id="d2655-108">Ancak, en fazla abonelik başına 200 bulut Hizmetleri içinde kalması için aynı bulut hizmetine bazı sanal makinelerden farklı bir uygulama katmanları birleştirebilirsiniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="d2655-108">However, you may need to combine some virtual machines from different application tiers into the same cloud service to remain within the maximum of 200 cloud services per subscription.</span></span> <span data-ttu-id="d2655-109">Bu ve diğer sınırları gözden geçirmek için bkz: [Azure aboneliği ve hizmet sınırları, kotaları ve kısıtlamaları](../articles/azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="d2655-109">To review this and other limits, see [Azure Subscription and Service Limits, Quotas, and Constraints](../articles/azure-subscription-service-limits.md).</span></span>

## <a name="connect-vms-in-a-virtual-network"></a><span data-ttu-id="d2655-110">Sanal makineleri sanal bir ağa bağlan</span><span class="sxs-lookup"><span data-stu-id="d2655-110">Connect VMs in a virtual network</span></span>
<span data-ttu-id="d2655-111">Bir sanal ağdaki sanal makinelere bağlanmak için:</span><span class="sxs-lookup"><span data-stu-id="d2655-111">To connect virtual machines in a virtual network:</span></span>

1. <span data-ttu-id="d2655-112">Sanal ağ oluşturma [Azure portal](../articles/virtual-network/virtual-networks-create-vnet-classic-pportal.md) ve 'Klasik dağıtım' belirtin.</span><span class="sxs-lookup"><span data-stu-id="d2655-112">Create the virtual network in the [Azure portal](../articles/virtual-network/virtual-networks-create-vnet-classic-pportal.md) and specify 'classic deployment'.</span></span>
2. <span data-ttu-id="d2655-113">Bulut Hizmetleri ve Yük Dengeleme tasarımınız kullanılabilirlik kümeleri için yansıtmak üzere dağıtımınız için kümesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d2655-113">Create the set of cloud services for your deployment to reflect your design for availability sets and load balancing.</span></span> <span data-ttu-id="d2655-114">Azure portalında tıklatın **yeni > işlem > bulut hizmeti** her bir bulut hizmeti için.</span><span class="sxs-lookup"><span data-stu-id="d2655-114">In the Azure portal, click **New > Compute > Cloud service** for each cloud service.</span></span>

  <span data-ttu-id="d2655-115">Bulut hizmetinin ayrıntılarını dolgu olarak aynı seçin _kaynak grubu_ sanal ağ ile kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d2655-115">As you fill out the cloud service details, choose the same _resource group_ used with the virtual network.</span></span>

3. <span data-ttu-id="d2655-116">Her yeni bir sanal makine oluşturmak için tıklatın **yeni > işlem**, ardından uygun VM görüntüsünü seçin **öne çıkan uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="d2655-116">To create each new virtual machine, click **New > Compute**, then select the appropriate VM image from the **Featured apps**.</span></span>

  <span data-ttu-id="d2655-117">VM'deki **Temelleri** dikey penceresinde, aynı seçin _kaynak grubu_ sanal ağ ile kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d2655-117">In the VM **Basics** blade, choose the same _resource group_ used with the virtual network.</span></span>

  ![Bir sanal ağ kullanırken VM temel bilgileri dikey penceresi](./media/virtual-machines-common-classic-connect-vms/CreateVM_Basics_VN.png)

4. <span data-ttu-id="d2655-119">VM'i dolgu olarak **ayarları**, doğru seçin _bulut hizmeti_ veya _sanal ağ_ VM için.</span><span class="sxs-lookup"><span data-stu-id="d2655-119">As you fill out the VM **Settings**, choose the correct _Cloud service_ or _virtual network_ for the VM.</span></span>

  <span data-ttu-id="d2655-120">Azure seçiminize bağlı diğer öğesini seçer.</span><span class="sxs-lookup"><span data-stu-id="d2655-120">Azure will select the other item based on your selection.</span></span>

  ![Bir sanal ağ kullanırken VM ayarlar dikey penceresi](./media/virtual-machines-common-classic-connect-vms/CreateVM_Settings_VN.png)


## <a name="connect-vms-in-a-standalone-cloud-service"></a><span data-ttu-id="d2655-122">Sanal makineleri bir tek başına bulut hizmetine bağlanmak</span><span class="sxs-lookup"><span data-stu-id="d2655-122">Connect VMs in a standalone cloud service</span></span>
<span data-ttu-id="d2655-123">Bir tek başına bulut hizmeti sanal makinelere bağlanmak için:</span><span class="sxs-lookup"><span data-stu-id="d2655-123">To connect virtual machines in a standalone cloud service:</span></span>

1. <span data-ttu-id="d2655-124">Bulut hizmeti oluşturma [Azure portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d2655-124">Create the cloud service in the [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="d2655-125">Tıklatın **yeni > işlem > bulut hizmeti**.</span><span class="sxs-lookup"><span data-stu-id="d2655-125">Click **New > Compute > Cloud service**.</span></span> <span data-ttu-id="d2655-126">Veya, ilk sanal makine oluşturduğunuzda, dağıtımınız için bulut hizmeti oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="d2655-126">Or, you can create the cloud service for your deployment when you create your first virtual machine.</span></span>
2. <span data-ttu-id="d2655-127">Sanal makine oluşturduğunuzda, bulut hizmeti ile kullanılan aynı kaynak grubunu seçin.</span><span class="sxs-lookup"><span data-stu-id="d2655-127">When you create the virtual machines, choose the same resource group used with the cloud service.</span></span>

  ![Bir sanal makine var olan bir bulut hizmetine Ekle](./media/virtual-machines-common-classic-connect-vms/CreateVM_Basics_SA.png)

3.  <span data-ttu-id="d2655-129">VM ayrıntılarını doldurun gibi ilk adımda oluşturduğunuz bulut hizmeti adını seçin.</span><span class="sxs-lookup"><span data-stu-id="d2655-129">As you fill out the VM details, choose the name of cloud service created in the first step.</span></span>

  ![Bir sanal makine için bir bulut hizmeti seçme](./media/virtual-machines-common-classic-connect-vms/CreateVM_Settings_SA.png)
