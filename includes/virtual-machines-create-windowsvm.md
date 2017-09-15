1. <span data-ttu-id="63632-101">[Azure portalında](https://portal.azure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="63632-101">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="63632-102">Sol üstten başlayarak sırasıyla **Yeni > İşlem > Windows Server 2016 Datacenter**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="63632-102">Starting in the upper left, click **New > Compute > Windows Server 2016 Datacenter**.</span></span>

    ![Portaldaki Azure sanal makine görüntülerine gitme](./media/virtual-machines-common-portal-create-fqdn/marketplace-new.png)

3. <span data-ttu-id="63632-104">Windows Server 2016 Datacenter’da Klasik dağıtım modelini seçin.</span><span class="sxs-lookup"><span data-stu-id="63632-104">On the Windows Server 2016 Datacenter, select the Classic deployment model.</span></span> <span data-ttu-id="63632-105">Oluştur’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="63632-105">Click Create.</span></span>

    ![Portalda kullanılabilecek Azure VM görüntülerini gösteren ekran görüntüsü](./media/virtual-machines-common-portal-create-fqdn/deployment-classic-model.png)

## <a name="1-basics-blade"></a><span data-ttu-id="63632-107">1. Temel Bilgiler dikey penceresi</span><span class="sxs-lookup"><span data-stu-id="63632-107">1. Basics blade</span></span>

<span data-ttu-id="63632-108">Temel Bilgiler dikey penceresi, sanal makine için yönetim bilgileri ister.</span><span class="sxs-lookup"><span data-stu-id="63632-108">The Basics blade requests administrative information for the virtual machine.</span></span>

1. <span data-ttu-id="63632-109">Sanal makine için bir **Ad** girin.</span><span class="sxs-lookup"><span data-stu-id="63632-109">Enter a **Name** for the virtual machine.</span></span> <span data-ttu-id="63632-110">Bu örnekte, sanal makinenin adı _HeroVM_’dir.</span><span class="sxs-lookup"><span data-stu-id="63632-110">In the example, _HeroVM_ is the name of the virtual machine.</span></span> <span data-ttu-id="63632-111">Ad, 1-15 karakter uzunluğunda olmalıdır ve özel karakterler içeremez.</span><span class="sxs-lookup"><span data-stu-id="63632-111">The name must be 1-15 characters long and it cannot contain special characters.</span></span>

2. <span data-ttu-id="63632-112">Sanal makinede yerel hesap oluşturmak için kullanılan bir **Kullanıcı adı** ve güçlü bir **Parola** girin.</span><span class="sxs-lookup"><span data-stu-id="63632-112">Enter a **User name** and a strong **Password** that are used to create a local account on the VM.</span></span> <span data-ttu-id="63632-113">Yerel hesap VM’de oturum açmak ve VM’yi yönetmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="63632-113">The local account is used to sign in to and manage the VM.</span></span> <span data-ttu-id="63632-114">Bu örnekte, kullanıcı adı _azureuser_’dır.</span><span class="sxs-lookup"><span data-stu-id="63632-114">In the example, _azureuser_ is the user name.</span></span>

 <span data-ttu-id="63632-115">Parola 8-123 karakter uzunluğunda olmalıdır ve en az şu dört karmaşıklık gereksinimini karşılamalıdır: bir küçük harf karakter, bir büyük harf karakter, bir sayı ve bir özel karakter.</span><span class="sxs-lookup"><span data-stu-id="63632-115">The password must be 8-123 characters long and meet three out of the four following complexity requirements: one lower case character, one upper case character, one number, and one special character.</span></span> <span data-ttu-id="63632-116">[Kullanıcı adı ve parola gereksinimleri](../articles/virtual-machines/windows/faq.md) hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="63632-116">See more about [username and password requirements](../articles/virtual-machines/windows/faq.md).</span></span>

3. <span data-ttu-id="63632-117">**Abonelik** isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="63632-117">The **Subscription** is optional.</span></span> <span data-ttu-id="63632-118">Yaygın olarak kullanılan bir ayar "Kullandıkça Öde"dir.</span><span class="sxs-lookup"><span data-stu-id="63632-118">One common setting is "Pay-As-You-Go".</span></span>

4. <span data-ttu-id="63632-119">Varolan **Kaynak grubunu** seçin veya yenisi için adı yazın.</span><span class="sxs-lookup"><span data-stu-id="63632-119">Select an existing **Resource group** or type the name for a new one.</span></span> <span data-ttu-id="63632-120">Bu örnekte, kaynak grubunun adı _HeroVMRG_’dir.</span><span class="sxs-lookup"><span data-stu-id="63632-120">In the example, _HeroVMRG_ is the name of the resource group.</span></span>

5. <span data-ttu-id="63632-121">Sanal makinenin çalışmasını istediğiniz bir Azure veri merkezi **Konumu** seçin.</span><span class="sxs-lookup"><span data-stu-id="63632-121">Select an Azure datacenter **Location** where you want the VM to run.</span></span> <span data-ttu-id="63632-122">Bu örnekte konum **Doğu ABD**’dir.</span><span class="sxs-lookup"><span data-stu-id="63632-122">In the example, **East US** is the location.</span></span>

6. <span data-ttu-id="63632-123">İşiniz bittiğinde, sonraki dikey pencereye geçmek için **İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="63632-123">When you are done, click **Next** to continue to the next blade.</span></span>

    ![Bir Azure VM’yi yapılandırmak için Temel Bilgiler dikey penceresindeki ayarları gösteren ekran görüntüsü](./media/virtual-machines-common-portal-create-fqdn/basics-blade-classic.png)

## <a name="2-size-blade"></a><span data-ttu-id="63632-125">2. Boyut dikey penceresi</span><span class="sxs-lookup"><span data-stu-id="63632-125">2. Size blade</span></span>

<span data-ttu-id="63632-126">Boyut dikey penceresi sanal makinenin yapılandırma ayrıntılarını tanımlar ve işletim sistemi, işlemci sayısı, disk depolama türü ve tahmini aylık kullanım maliyeti gibi çeşitli seçenekleri listeler.</span><span class="sxs-lookup"><span data-stu-id="63632-126">The Size blade identifies the configuration details of the VM, and lists various choices that include OS, number of processors, disk storage type, and estimated monthly usage costs.</span></span>  

<span data-ttu-id="63632-127">Bir sanal makine boyutu seçin ve devam etmek için **Seç**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="63632-127">Choose a VM size, and then click **Select** to continue.</span></span> <span data-ttu-id="63632-128">Bu örnekte VM boyutu _DS1_\__V2 Standart_ olarak seçilmiştir.</span><span class="sxs-lookup"><span data-stu-id="63632-128">In this example, _DS1_\__V2 Standard_ is the VM size.</span></span>

  ![Seçebileceğiniz Azure VM boyutlarını gösteren Boyut dikey penceresi ekran görüntüsü](./media/virtual-machines-common-portal-create-fqdn/vm-size-classic.png)


## <a name="3-settings-blade"></a><span data-ttu-id="63632-130">3. Ayarlar dikey penceresi</span><span class="sxs-lookup"><span data-stu-id="63632-130">3. Settings blade</span></span>

<span data-ttu-id="63632-131">Ayarlar dikey penceresi depolama ve ağ seçeneklerini ister.</span><span class="sxs-lookup"><span data-stu-id="63632-131">The Settings blade requests storage and network options.</span></span> <span data-ttu-id="63632-132">Varsayılan ayarları kabul edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="63632-132">You can accept the default settings.</span></span> <span data-ttu-id="63632-133">Azure, gerekli durumlarda uygun girişleri oluşturur.</span><span class="sxs-lookup"><span data-stu-id="63632-133">Azure creates appropriate entries where necessary.</span></span>

<span data-ttu-id="63632-134">Bunu destekleyen bir sanal makine boyutu seçtiyseniz, Disk türü altında Premium (SSD) seçeneğini belirleyerek Azure Premium Depolama’yı deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="63632-134">If you selected a virtual machine size that supports it, you can try Azure Premium Storage by selecting Premium (SSD) in Disk type.</span></span>

<span data-ttu-id="63632-135">Değişiklikleriniz bittiğinde **Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="63632-135">When you're done making changes, click **OK**.</span></span>

## <a name="4-summary-blade"></a><span data-ttu-id="63632-136">4. Özet dikey penceresi</span><span class="sxs-lookup"><span data-stu-id="63632-136">4. Summary blade</span></span>

<span data-ttu-id="63632-137">Özet dikey penceresinde, önceki dikey pencerelerde belirtilen ayarlar listelenir.</span><span class="sxs-lookup"><span data-stu-id="63632-137">The Summary blade lists the settings specified in the previous blades.</span></span> <span data-ttu-id="63632-138">Görüntüyü oluşturmaya hazır olduğunuzda **Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="63632-138">Click **OK** when you're ready to make the image.</span></span>

 ![Sanal makine için belirtilen ayarları gösteren Özet dikey penceresi raporu](./media/virtual-machines-common-portal-create-fqdn/summary-blade-classic.png)

<span data-ttu-id="63632-140">Sanal makine oluşturulduktan sonra portal tarafından **Tüm kaynaklar** altında listelenir ve panoda sanal makine için bir kutucuk görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="63632-140">After the virtual machine is created, the portal lists the new virtual machine under **All resources**, and displays a tile of the virtual machine on the dashboard.</span></span> <span data-ttu-id="63632-141">Ayrıca, sanal makineye karşılık gelen bulut hizmeti ve depolama hesabı da oluşturulur ve listelenir.</span><span class="sxs-lookup"><span data-stu-id="63632-141">The corresponding cloud service and storage account also are created and listed.</span></span> <span data-ttu-id="63632-142">Hem sanal makine hem de bulut hizmeti otomatik olarak başlatılır ve durumları **Çalışıyor** olarak listelenir.</span><span class="sxs-lookup"><span data-stu-id="63632-142">Both the virtual machine and cloud service are started automatically and their status is listed as **Running**.</span></span>

 ![Sanal makinenin VM Aracısı’nı ve uç noktalarını yapılandırma](./media/virtual-machines-common-portal-create-fqdn/portal-with-new-vm.png)
