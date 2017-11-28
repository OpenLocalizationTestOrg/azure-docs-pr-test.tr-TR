


<span data-ttu-id="6e7b0-101">Yardımcı bir kullanılabilirlik kümesi sanal makinelerinizin kapalı kalma süresi sırasında kullanılabilir gibi tutmak bakımı sırasında.</span><span class="sxs-lookup"><span data-stu-id="6e7b0-101">An availability set helps keep your virtual machines available during downtime, such as during maintenance.</span></span> <span data-ttu-id="6e7b0-102">Bir kullanılabilirlik kümesinde iki veya daha fazla benzer şekilde yapılandırılmış sanal makine yerleştirme uygulamalar veya sanal makinenize çalışan hizmetleri kullanılabilirliğini sürdürmek için gerekli artıklık oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6e7b0-102">Placing two or more similarly configured virtual machines in an availability set creates the redundancy needed to maintain availability of the applications or services that your virtual machine runs.</span></span> <span data-ttu-id="6e7b0-103">Bunun nasıl çalıştığı hakkında daha fazla bilgi için bkz [sanal makinelerin kullanılabilirliğini yönetme][Manage the availability of virtual machines].</span><span class="sxs-lookup"><span data-stu-id="6e7b0-103">For details about how this works, see [Manage the availability of virtual machines][Manage the availability of virtual machines].</span></span>

<span data-ttu-id="6e7b0-104">Uygulamanızın her zaman verimli bir şekilde kullanılabilir olduğundan ve çalıştığından emin olmak için kullanılabilirlik kümeleri ve Yük Dengeleme uç noktaları kullanmak için en iyi bir uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="6e7b0-104">It's a best practice to use both availability sets and load-balancing endpoints to help ensure that your application is always available and running efficiently.</span></span> <span data-ttu-id="6e7b0-105">Yük dengeli uç noktalar hakkında daha fazla ayrıntı için bkz: [Yük Dengeleme için Azure altyapı hizmetleri][Load balancing for Azure infrastructure services].</span><span class="sxs-lookup"><span data-stu-id="6e7b0-105">For details about load-balanced endpoints, see [Load balancing for Azure infrastructure services][Load balancing for Azure infrastructure services].</span></span>

<span data-ttu-id="6e7b0-106">Kullanılabilirlik kümesi iki seçenekten birini kullanarak içine Klasik sanal makineleri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="6e7b0-106">You can add classic virtual machines into an availability set by using one of two options:</span></span>

* <span data-ttu-id="6e7b0-107">[Seçenek 1: bir sanal makine kullanılabilirlik aynı anda kümesi oluşturup][Option 1: Create a virtual machine and an availability set at the same time].</span><span class="sxs-lookup"><span data-stu-id="6e7b0-107">[Option 1: Create a virtual machine and an availability set at the same time][Option 1: Create a virtual machine and an availability set at the same time].</span></span> <span data-ttu-id="6e7b0-108">Ardından, bu sanal makineleri oluşturduğunuzda, yeni sanal makineler kümeye ekleyin.</span><span class="sxs-lookup"><span data-stu-id="6e7b0-108">Then, add new virtual machines to the set when you create those virtual machines.</span></span>
* <span data-ttu-id="6e7b0-109">[Seçenek 2: var olan bir sanal makine bir kullanılabilirlik kümesine ekleme][Option 2: Add an existing virtual machine to an availability set].</span><span class="sxs-lookup"><span data-stu-id="6e7b0-109">[Option 2: Add an existing virtual machine to an availability set][Option 2: Add an existing virtual machine to an availability set].</span></span>

> [!NOTE]
> <span data-ttu-id="6e7b0-110">Klasik modelde aynı kullanılabilirlik kümesinde yerleştirmek istediğiniz sanal makineleri aynı bulut hizmetine ait olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="6e7b0-110">In the classic model, virtual machines that you want to put in the same availability set must belong to the same cloud service.</span></span>
> 
> 

## <span data-ttu-id="6e7b0-111"><a id="createset"></a>Seçenek 1: bir sanal makine ve kullanılabilirlik aynı anda kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="6e7b0-111"><a id="createset"> </a>Option 1: Create a virtual machine and an availability set at the same time</span></span>
<span data-ttu-id="6e7b0-112">Bunu yapmak için Azure portalında veya Azure PowerShell komutlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6e7b0-112">You can use either the Azure portal or Azure PowerShell commands to do this.</span></span>

<span data-ttu-id="6e7b0-113">Azure Portalı'nı kullanmak için:</span><span class="sxs-lookup"><span data-stu-id="6e7b0-113">To use the Azure portal:</span></span>

1. <span data-ttu-id="6e7b0-114">Önceden yapmadıysanız, [Azure portal](https://portal.azure.com)da oturum açın</span><span class="sxs-lookup"><span data-stu-id="6e7b0-114">If you haven't already done so, sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="6e7b0-115">Hub menüsünde **+ yeni**ve ardından **sanal makine**.</span><span class="sxs-lookup"><span data-stu-id="6e7b0-115">On the hub menu, click **+ New**, and then click **Virtual Machine**.</span></span>
   
    ![Alt görüntü metin](./media/virtual-machines-common-classic-configure-availability/ChooseVMImage.png)
3. <span data-ttu-id="6e7b0-117">Kullanmak istediğiniz Market sanal makine görüntüsü seçin.</span><span class="sxs-lookup"><span data-stu-id="6e7b0-117">Select the Marketplace virtual machine image you wish to use.</span></span> <span data-ttu-id="6e7b0-118">Bir Linux veya Windows sanal makine oluşturmak seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6e7b0-118">You can choose to create a Linux or Windows virtual machine.</span></span>
4. <span data-ttu-id="6e7b0-119">Seçili sanal makine için dağıtım modeli değerine ayarlandığını doğrulayın **Klasik** ve ardından **oluştur**</span><span class="sxs-lookup"><span data-stu-id="6e7b0-119">For the selected virtual machine, verify that the deployment model is set to **Classic** and then click **Create**</span></span>
   
    ![Alt görüntü metin](./media/virtual-machines-common-classic-configure-availability/ChooseClassicModel.png)
5. <span data-ttu-id="6e7b0-121">Bir sanal makine adı, kullanıcı adı ve parolası (Windows makineler) veya SSH ortak anahtarı (Linux makinelerde) girin.</span><span class="sxs-lookup"><span data-stu-id="6e7b0-121">Enter a virtual machine name, user name and password (for Windows machines) or SSH public key (for Linux machines).</span></span> 
6. <span data-ttu-id="6e7b0-122">VM boyutunu seçin ve ardından **seçin** devam etmek için.</span><span class="sxs-lookup"><span data-stu-id="6e7b0-122">Choose the VM size and then click **Select** to continue.</span></span>
7. <span data-ttu-id="6e7b0-123">Seçin **isteğe bağlı yapılandırma > kullanılabilirlik kümesi**, ve sanal makineye eklemek istediğiniz kullanılabilirlik kümesini seçin.</span><span class="sxs-lookup"><span data-stu-id="6e7b0-123">Choose **Optional Configuration > Availability set**, and select the availability set you wish to add the virtual machine to.</span></span>
   
    ![Alt görüntü metin](./media/virtual-machines-common-classic-configure-availability/ChooseAvailabilitySet.png) 
8. <span data-ttu-id="6e7b0-125">Yapılandırma ayarlarınızı gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="6e7b0-125">Review your configuration settings.</span></span> <span data-ttu-id="6e7b0-126">İşiniz bittiğinde tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="6e7b0-126">When you're done, click **Create**.</span></span>
9. <span data-ttu-id="6e7b0-127">Azure sanal makine oluştururken altında ilerleme durumunu izleyebilirsiniz **sanal makineleri** hub menüsünde.</span><span class="sxs-lookup"><span data-stu-id="6e7b0-127">While Azure creates your virtual machine, you can track the progress under **Virtual Machines** in the hub menu.</span></span>

<span data-ttu-id="6e7b0-128">Bir Azure sanal makinesi oluşturmak ve yeni veya var olan kullanılabilirlik kümesine eklemek için Azure PowerShell komutlarını kullanmak için bkz: [oluşturmak ve Windows tabanlı sanal makineleri önceden için Azure PowerShell kullanma](../articles/virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="6e7b0-128">To use Azure PowerShell commands to create an Azure virtual machine and add it to a new or existing availability set, see [Use Azure PowerShell to create and preconfigure Windows-based virtual machines](../articles/virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

## <span data-ttu-id="6e7b0-129"><a id="addmachine"></a>Seçenek 2: var olan bir sanal makine bir kullanılabilirlik kümesine ekleme</span><span class="sxs-lookup"><span data-stu-id="6e7b0-129"><a id="addmachine"> </a>Option 2: Add an existing virtual machine to an availability set</span></span>
<span data-ttu-id="6e7b0-130">Azure Portal'da, mevcut bir kullanılabilirlik Klasik varolan sanal makinelere veya bunları için yeni bir tane oluşturmak ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6e7b0-130">In the Azure portal, you can add existing classic virtual machines to an existing availability set or create a new one for them.</span></span> <span data-ttu-id="6e7b0-131">(Sanal makineler aynı kullanılabilirlik kümesindeki aynı bulut hizmetine ait olması gerektiğini aklınızda tutun.) Adımlar neredeyse aynıdır.</span><span class="sxs-lookup"><span data-stu-id="6e7b0-131">(Keep in mind that the virtual machines in the same availability set must belong to the same cloud service.) The steps are almost the same.</span></span> <span data-ttu-id="6e7b0-132">Azure PowerShell ile sanal makine var olan bir kullanılabilirlik kümesine ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6e7b0-132">With Azure PowerShell, you can add the virtual machine to an existing availability set.</span></span>

1. <span data-ttu-id="6e7b0-133">Zaten yapmadıysanız, oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6e7b0-133">If you have not already done so, sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="6e7b0-134">Hub menüsünde **sanal makineleri (Klasik)**.</span><span class="sxs-lookup"><span data-stu-id="6e7b0-134">On the Hub menu, click **Virtual Machines (classic)**.</span></span>
   
    ![Alt görüntü metin](./media/virtual-machines-common-classic-configure-availability/ChooseClassicVM.png)
3. <span data-ttu-id="6e7b0-136">Sanal makineler listesinden kümeye eklemek istediğiniz sanal makinenin adını seçin.</span><span class="sxs-lookup"><span data-stu-id="6e7b0-136">From the list of virtual machines, select the name of the virtual machine that you want to add to the set.</span></span>
4. <span data-ttu-id="6e7b0-137">Seçin **kullanılabilirlik kümesi** sanal makineden **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="6e7b0-137">Choose **Availability set** from the virtual machine **Settings**.</span></span>
   
    ![Alt görüntü metin](./media/virtual-machines-common-classic-configure-availability/AvailabilitySetSettings.png)
5. <span data-ttu-id="6e7b0-139">Sanal makineye eklemek istediğiniz kullanılabilirlik kümesi seçin.</span><span class="sxs-lookup"><span data-stu-id="6e7b0-139">Select the availability set you wish to add the virtual machine to.</span></span> <span data-ttu-id="6e7b0-140">Sanal makine kullanılabilirlik kümesi aynı bulut hizmetine ait olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="6e7b0-140">The virtual machine must belong to the same cloud service as the availability set.</span></span>
   
    ![Alt görüntü metin](./media/virtual-machines-common-classic-configure-availability/AvailabilitySetPicker.png)
6. <span data-ttu-id="6e7b0-142">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6e7b0-142">Click **Save**.</span></span>

<span data-ttu-id="6e7b0-143">Azure PowerShell komutlarını kullanmak için bir yönetici düzeyi Azure PowerShell oturumu açın ve aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="6e7b0-143">To use Azure PowerShell commands, open an administrator-level Azure PowerShell session and run the following command.</span></span> <span data-ttu-id="6e7b0-144">Yer tutucuları için (gibi &lt;VmCloudServiceName&gt;), dahil olmak üzere tırnak işaretleri içindeki her şeyi değiştirin < ve > karakterleri doğru adlara sahip.</span><span class="sxs-lookup"><span data-stu-id="6e7b0-144">For the placeholders (such as &lt;VmCloudServiceName&gt;), replace everything within the quotes, including the < and > characters, with the correct names.</span></span>

    Get-AzureVM -ServiceName "<VmCloudServiceName>" -Name "<VmName>" | Set-AzureAvailabilitySet -AvailabilitySetName "<AvSetName>" | Update-AzureVM

> [!NOTE]
> <span data-ttu-id="6e7b0-145">Sanal makine kullanılabilirlik kümesine ekleme işlemini tamamlamak için yeniden başlatılması gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="6e7b0-145">The virtual machine might have to be restarted to finish adding it to the availability set.</span></span>
> 
> 

<!-- LINKS -->
[Option 1: Create a virtual machine and an availability set at the same time]: #createset
[Option 2: Add an existing virtual machine to an availability set]: #addmachine

[Load balancing for Azure infrastructure services]: ../articles/virtual-machines/virtual-machines-linux-load-balance.md
[Manage the availability of virtual machines]:../articles/virtual-machines/linux/manage-availability.md

[Create a virtual machine running Windows]: ../articles/virtual-machines/virtual-machines-windows-hero-tutorial.md
[Virtual Network overview]: ../articles/virtual-network/virtual-networks-overview.md

