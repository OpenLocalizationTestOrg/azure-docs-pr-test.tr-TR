1. <span data-ttu-id="0a378-101">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0a378-101">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="0a378-102">Merhaba üst sol başlayarak, tıklatın **yeni > işlem > Windows Server 2016 Datacenter**.</span><span class="sxs-lookup"><span data-stu-id="0a378-102">Starting in hello upper left, click **New > Compute > Windows Server 2016 Datacenter**.</span></span>

    ![Merhaba portalında toohello Azure VM görüntülerini gidin](./media/virtual-machines-common-portal-create-fqdn/marketplace-new.png)

3. <span data-ttu-id="0a378-104">Windows Server 2016 Datacenter Hello üzerinde hello Klasik dağıtım modeli seçin.</span><span class="sxs-lookup"><span data-stu-id="0a378-104">On hello Windows Server 2016 Datacenter, select hello Classic deployment model.</span></span> <span data-ttu-id="0a378-105">Oluştur’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0a378-105">Click Create.</span></span>

    ![Merhaba Portalı'nda kullanılabilir hello Azure VM görüntülerini gösteren ekran görüntüsü](./media/virtual-machines-common-portal-create-fqdn/deployment-classic-model.png)

## <a name="1-basics-blade"></a><span data-ttu-id="0a378-107">1. Temel Bilgiler dikey penceresi</span><span class="sxs-lookup"><span data-stu-id="0a378-107">1. Basics blade</span></span>

<span data-ttu-id="0a378-108">Merhaba temel bilgileri dikey penceresinde hello sanal makine için yönetim bilgi ister.</span><span class="sxs-lookup"><span data-stu-id="0a378-108">hello Basics blade requests administrative information for hello virtual machine.</span></span>

1. <span data-ttu-id="0a378-109">Girin bir **adı** hello sanal makine için.</span><span class="sxs-lookup"><span data-stu-id="0a378-109">Enter a **Name** for hello virtual machine.</span></span> <span data-ttu-id="0a378-110">Merhaba örnekte _HeroVM_ hello sanal makinenin hello adıdır.</span><span class="sxs-lookup"><span data-stu-id="0a378-110">In hello example, _HeroVM_ is hello name of hello virtual machine.</span></span> <span data-ttu-id="0a378-111">Merhaba adı 1-15 karakter uzunluğunda olmalıdır ve özel karakterler içeremez.</span><span class="sxs-lookup"><span data-stu-id="0a378-111">hello name must be 1-15 characters long and it cannot contain special characters.</span></span>

2. <span data-ttu-id="0a378-112">Girin bir **kullanıcı adı** ve güçlü **parola** kullanılan toocreate hello VM üzerindeki yerel bir hesap olan.</span><span class="sxs-lookup"><span data-stu-id="0a378-112">Enter a **User name** and a strong **Password** that are used toocreate a local account on hello VM.</span></span> <span data-ttu-id="0a378-113">Merhaba yerel hesap kullanılan tooand toosign hello VM yönetin.</span><span class="sxs-lookup"><span data-stu-id="0a378-113">hello local account is used toosign in tooand manage hello VM.</span></span> <span data-ttu-id="0a378-114">Merhaba örnekte _azureuser_ hello kullanıcı adıdır.</span><span class="sxs-lookup"><span data-stu-id="0a378-114">In hello example, _azureuser_ is hello user name.</span></span>

 <span data-ttu-id="0a378-115">Merhaba parola 8-123 karakter uzunluğunda olmalıdır ve üç dışında hello dört aşağıdaki karmaşıklık gereksinimlerini karşılayacak: bir küçük harf karakter, bir büyük harf karakter, bir sayı ve bir özel karakter.</span><span class="sxs-lookup"><span data-stu-id="0a378-115">hello password must be 8-123 characters long and meet three out of hello four following complexity requirements: one lower case character, one upper case character, one number, and one special character.</span></span> <span data-ttu-id="0a378-116">[Kullanıcı adı ve parola gereksinimleri](../articles/virtual-machines/windows/faq.md) hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="0a378-116">See more about [username and password requirements](../articles/virtual-machines/windows/faq.md).</span></span>

3. <span data-ttu-id="0a378-117">Merhaba **abonelik** isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="0a378-117">hello **Subscription** is optional.</span></span> <span data-ttu-id="0a378-118">Yaygın olarak kullanılan bir ayar "Kullandıkça Öde"dir.</span><span class="sxs-lookup"><span data-stu-id="0a378-118">One common setting is "Pay-As-You-Go".</span></span>

4. <span data-ttu-id="0a378-119">Var olan seçin **kaynak grubu** veya yeni bir hello adını yazın.</span><span class="sxs-lookup"><span data-stu-id="0a378-119">Select an existing **Resource group** or type hello name for a new one.</span></span> <span data-ttu-id="0a378-120">Merhaba örnekte _HeroVMRG_ hello hello kaynak grubunun adıdır.</span><span class="sxs-lookup"><span data-stu-id="0a378-120">In hello example, _HeroVMRG_ is hello name of hello resource group.</span></span>

5. <span data-ttu-id="0a378-121">Azure veri merkezi seçin **konumu** hello VM toorun istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="0a378-121">Select an Azure datacenter **Location** where you want hello VM toorun.</span></span> <span data-ttu-id="0a378-122">Merhaba örnekte **Doğu ABD** hello konumdur.</span><span class="sxs-lookup"><span data-stu-id="0a378-122">In hello example, **East US** is hello location.</span></span>

6. <span data-ttu-id="0a378-123">İşiniz bittiğinde tıklatın **sonraki** toocontinue toohello sonraki dikey.</span><span class="sxs-lookup"><span data-stu-id="0a378-123">When you are done, click **Next** toocontinue toohello next blade.</span></span>

    ![Bir Azure VM'yi yapılandırmak için hello temel bilgileri dikey penceresinde hello ayarları gösteren ekran görüntüsü](./media/virtual-machines-common-portal-create-fqdn/basics-blade-classic.png)

## <a name="2-size-blade"></a><span data-ttu-id="0a378-125">2. Boyut dikey penceresi</span><span class="sxs-lookup"><span data-stu-id="0a378-125">2. Size blade</span></span>

<span data-ttu-id="0a378-126">Hello boyutu dikey penceresinde hello VM hello yapılandırma ayrıntılarını tanımlar ve işletim sistemi, işlemciler, disk depolama türü ve tahmini aylık kullanım maliyetleri sayısı dahil çeşitli seçenekler listeler.</span><span class="sxs-lookup"><span data-stu-id="0a378-126">hello Size blade identifies hello configuration details of hello VM, and lists various choices that include OS, number of processors, disk storage type, and estimated monthly usage costs.</span></span>  

<span data-ttu-id="0a378-127">Bir VM boyutu seçin ve ardından **seçin** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="0a378-127">Choose a VM size, and then click **Select** toocontinue.</span></span> <span data-ttu-id="0a378-128">Bu örnekte, _DS1_\__V2 standart_ hello VM boyutu.</span><span class="sxs-lookup"><span data-stu-id="0a378-128">In this example, _DS1_\__V2 Standard_ is hello VM size.</span></span>

  ![Merhaba seçebileceğiniz Azure VM boyutlarını gösteren hello boyutu dikey penceresinin ekran görüntüsü](./media/virtual-machines-common-portal-create-fqdn/vm-size-classic.png)


## <a name="3-settings-blade"></a><span data-ttu-id="0a378-130">3. Ayarlar dikey penceresi</span><span class="sxs-lookup"><span data-stu-id="0a378-130">3. Settings blade</span></span>

<span data-ttu-id="0a378-131">Hello ayarları dikey penceresinde, depolama ve ağ seçenekleri ister.</span><span class="sxs-lookup"><span data-stu-id="0a378-131">hello Settings blade requests storage and network options.</span></span> <span data-ttu-id="0a378-132">Merhaba varsayılan ayarları kabul edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0a378-132">You can accept hello default settings.</span></span> <span data-ttu-id="0a378-133">Azure, gerekli durumlarda uygun girişleri oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0a378-133">Azure creates appropriate entries where necessary.</span></span>

<span data-ttu-id="0a378-134">Bunu destekleyen bir sanal makine boyutu seçtiyseniz, Disk türü altında Premium (SSD) seçeneğini belirleyerek Azure Premium Depolama’yı deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0a378-134">If you selected a virtual machine size that supports it, you can try Azure Premium Storage by selecting Premium (SSD) in Disk type.</span></span>

<span data-ttu-id="0a378-135">Değişiklikleriniz bittiğinde **Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0a378-135">When you're done making changes, click **OK**.</span></span>

## <a name="4-summary-blade"></a><span data-ttu-id="0a378-136">4. Özet dikey penceresi</span><span class="sxs-lookup"><span data-stu-id="0a378-136">4. Summary blade</span></span>

<span data-ttu-id="0a378-137">Merhaba Özet dikey penceresinde hello önceki tüm dikey pencereleri içinde belirtilen hello ayarları listeler.</span><span class="sxs-lookup"><span data-stu-id="0a378-137">hello Summary blade lists hello settings specified in hello previous blades.</span></span> <span data-ttu-id="0a378-138">Tıklatın **Tamam** hazır toomake hello görüntü olduğunuzda.</span><span class="sxs-lookup"><span data-stu-id="0a378-138">Click **OK** when you're ready toomake hello image.</span></span>

 ![Merhaba sanal makinenin belirtilen ayarlarını vermiş Özet dikey raporu](./media/virtual-machines-common-portal-create-fqdn/summary-blade-classic.png)

<span data-ttu-id="0a378-140">Merhaba sanal makine oluşturulduktan sonra hello portal hello yeni sanal makinenin altında listeler **tüm kaynakları**ve hello Panoda bir kutucuğu hello sanal makinenin görüntüler.</span><span class="sxs-lookup"><span data-stu-id="0a378-140">After hello virtual machine is created, hello portal lists hello new virtual machine under **All resources**, and displays a tile of hello virtual machine on hello dashboard.</span></span> <span data-ttu-id="0a378-141">Hello karşılık gelen bulut hizmeti ve depolama hesabı aynı zamanda oluşturulur ve listelenir.</span><span class="sxs-lookup"><span data-stu-id="0a378-141">hello corresponding cloud service and storage account also are created and listed.</span></span> <span data-ttu-id="0a378-142">Merhaba sanal makine ve bulut hizmeti başlatıldığında otomatik olarak ve durumlarını olarak listelenen **çalıştıran**.</span><span class="sxs-lookup"><span data-stu-id="0a378-142">Both hello virtual machine and cloud service are started automatically and their status is listed as **Running**.</span></span>

 ![Merhaba sanal makinesinin VM aracısı ve hello uç noktalarını yapılandırma](./media/virtual-machines-common-portal-create-fqdn/portal-with-new-vm.png)
