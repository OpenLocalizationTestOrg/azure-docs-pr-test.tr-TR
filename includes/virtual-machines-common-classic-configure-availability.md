


<span data-ttu-id="535f3-101">Yardımcı bir kullanılabilirlik kümesi sanal makinelerinizin kapalı kalma süresi sırasında kullanılabilir gibi tutmak bakımı sırasında.</span><span class="sxs-lookup"><span data-stu-id="535f3-101">An availability set helps keep your virtual machines available during downtime, such as during maintenance.</span></span> <span data-ttu-id="535f3-102">Bir kullanılabilirlik kümesinde iki veya daha fazla benzer şekilde yapılandırılmış sanal makine yerleştirme hello gerekli artıklık toomaintain kullanılabilirliğini sanal makineniz çalıştıran hello uygulamalar veya hizmetler oluşturur.</span><span class="sxs-lookup"><span data-stu-id="535f3-102">Placing two or more similarly configured virtual machines in an availability set creates hello redundancy needed toomaintain availability of hello applications or services that your virtual machine runs.</span></span> <span data-ttu-id="535f3-103">Bunun nasıl çalıştığı hakkında daha fazla bilgi için bkz [hello sanal makinelerin kullanılabilirliğini yönetme][Manage hello availability of virtual machines].</span><span class="sxs-lookup"><span data-stu-id="535f3-103">For details about how this works, see [Manage hello availability of virtual machines][Manage hello availability of virtual machines].</span></span>

<span data-ttu-id="535f3-104">En iyi yöntem toouse olan kullanılabilirlik kümeleri ve Yük Dengeleme uç noktaları toohelp uygulamanızın her zaman verimli bir şekilde kullanılabilir ve çalışıyor olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="535f3-104">It's a best practice toouse both availability sets and load-balancing endpoints toohelp ensure that your application is always available and running efficiently.</span></span> <span data-ttu-id="535f3-105">Yük dengeli uç noktalar hakkında daha fazla ayrıntı için bkz: [Yük Dengeleme için Azure altyapı hizmetleri][Load balancing for Azure infrastructure services].</span><span class="sxs-lookup"><span data-stu-id="535f3-105">For details about load-balanced endpoints, see [Load balancing for Azure infrastructure services][Load balancing for Azure infrastructure services].</span></span>

<span data-ttu-id="535f3-106">Kullanılabilirlik kümesi iki seçenekten birini kullanarak içine Klasik sanal makineleri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="535f3-106">You can add classic virtual machines into an availability set by using one of two options:</span></span>

* <span data-ttu-id="535f3-107">[Seçenek 1: bir sanal makine oluşturun ve aynı hello kullanılabilirlik kümesi zaman][Option 1: Create a virtual machine and an availability set at hello same time].</span><span class="sxs-lookup"><span data-stu-id="535f3-107">[Option 1: Create a virtual machine and an availability set at hello same time][Option 1: Create a virtual machine and an availability set at hello same time].</span></span> <span data-ttu-id="535f3-108">Ardından, bu sanal makineleri oluşturduğunuzda yeni sanal makineler toohello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="535f3-108">Then, add new virtual machines toohello set when you create those virtual machines.</span></span>
* <span data-ttu-id="535f3-109">[Seçenek 2: varolan bir sanal makine tooan kullanılabilirlik kümesini ekleme][Option 2: Add an existing virtual machine tooan availability set].</span><span class="sxs-lookup"><span data-stu-id="535f3-109">[Option 2: Add an existing virtual machine tooan availability set][Option 2: Add an existing virtual machine tooan availability set].</span></span>

> [!NOTE]
> <span data-ttu-id="535f3-110">Merhaba Klasik modelde tooput istediğiniz sanal makineleri hello aynı kullanılabilirlik kümesi toohello ait olmalıdır aynı bulut hizmeti.</span><span class="sxs-lookup"><span data-stu-id="535f3-110">In hello classic model, virtual machines that you want tooput in hello same availability set must belong toohello same cloud service.</span></span>
> 
> 

## <span data-ttu-id="535f3-111"><a id="createset"></a>Seçenek 1: bir sanal makine oluşturun ve aynı hello kullanılabilirlik kümesi süresi</span><span class="sxs-lookup"><span data-stu-id="535f3-111"><a id="createset"> </a>Option 1: Create a virtual machine and an availability set at hello same time</span></span>
<span data-ttu-id="535f3-112">Azure PowerShell toodo bu komutları veya ya da hello Azure portalını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="535f3-112">You can use either hello Azure portal or Azure PowerShell commands toodo this.</span></span>

<span data-ttu-id="535f3-113">toouse hello Azure portalı:</span><span class="sxs-lookup"><span data-stu-id="535f3-113">toouse hello Azure portal:</span></span>

1. <span data-ttu-id="535f3-114">Zaten yapmadıysanız, toohello içinde oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="535f3-114">If you haven't already done so, sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="535f3-115">Merhaba hub menüsünde **+ yeni**ve ardından **sanal makine**.</span><span class="sxs-lookup"><span data-stu-id="535f3-115">On hello hub menu, click **+ New**, and then click **Virtual Machine**.</span></span>
   
    ![Alt görüntü metin](./media/virtual-machines-common-classic-configure-availability/ChooseVMImage.png)
3. <span data-ttu-id="535f3-117">Toouse istediğiniz hello Market sanal makine görüntüsü seçin.</span><span class="sxs-lookup"><span data-stu-id="535f3-117">Select hello Marketplace virtual machine image you wish toouse.</span></span> <span data-ttu-id="535f3-118">Bir Linux veya Windows sanal makine toocreate seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="535f3-118">You can choose toocreate a Linux or Windows virtual machine.</span></span>
4. <span data-ttu-id="535f3-119">Sanal makine Hello seçilen için o hello dağıtım modeli olarak ayarlanmış çok doğrulayın**Klasik** ve ardından **oluştur**</span><span class="sxs-lookup"><span data-stu-id="535f3-119">For hello selected virtual machine, verify that hello deployment model is set too**Classic** and then click **Create**</span></span>
   
    ![Alt görüntü metin](./media/virtual-machines-common-classic-configure-availability/ChooseClassicModel.png)
5. <span data-ttu-id="535f3-121">Bir sanal makine adı, kullanıcı adı ve parolası (Windows makineler) veya SSH ortak anahtarı (Linux makinelerde) girin.</span><span class="sxs-lookup"><span data-stu-id="535f3-121">Enter a virtual machine name, user name and password (for Windows machines) or SSH public key (for Linux machines).</span></span> 
6. <span data-ttu-id="535f3-122">Merhaba VM boyutunu seçin ve ardından **seçin** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="535f3-122">Choose hello VM size and then click **Select** toocontinue.</span></span>
7. <span data-ttu-id="535f3-123">Seçin **isteğe bağlı yapılandırma > kullanılabilirlik kümesi**ve tooadd hello sanal makineye istediğiniz hello kullanılabilirlik kümesi seçin.</span><span class="sxs-lookup"><span data-stu-id="535f3-123">Choose **Optional Configuration > Availability set**, and select hello availability set you wish tooadd hello virtual machine to.</span></span>
   
    ![Alt görüntü metin](./media/virtual-machines-common-classic-configure-availability/ChooseAvailabilitySet.png) 
8. <span data-ttu-id="535f3-125">Yapılandırma ayarlarınızı gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="535f3-125">Review your configuration settings.</span></span> <span data-ttu-id="535f3-126">İşiniz bittiğinde tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="535f3-126">When you're done, click **Create**.</span></span>
9. <span data-ttu-id="535f3-127">Azure sanal makine oluştururken altında hello ilerleme durumunu izleyebilirsiniz **sanal makineleri** hello hub menüsünde.</span><span class="sxs-lookup"><span data-stu-id="535f3-127">While Azure creates your virtual machine, you can track hello progress under **Virtual Machines** in hello hub menu.</span></span>

<span data-ttu-id="535f3-128">toouse Azure PowerShell toocreate bir Azure sanal makinesi komutları ve tooa yeni veya var olan kullanılabilirlik kümesi ekleme, bkz: [kullanım Azure PowerShell toocreate ve Windows tabanlı sanal makineleri önceden yapılandırın](../articles/virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="535f3-128">toouse Azure PowerShell commands toocreate an Azure virtual machine and add it tooa new or existing availability set, see [Use Azure PowerShell toocreate and preconfigure Windows-based virtual machines](../articles/virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

## <span data-ttu-id="535f3-129"><a id="addmachine"></a>Seçenek 2: varolan bir sanal makine tooan kullanılabilirlik kümesini ekleyin</span><span class="sxs-lookup"><span data-stu-id="535f3-129"><a id="addmachine"> </a>Option 2: Add an existing virtual machine tooan availability set</span></span>
<span data-ttu-id="535f3-130">Hello Azure portal, kullanılabilirlik kümesi varolan varolan Klasik sanal makineleri tooan ekleyin veya onları için yeni bir tane oluşturun.</span><span class="sxs-lookup"><span data-stu-id="535f3-130">In hello Azure portal, you can add existing classic virtual machines tooan existing availability set or create a new one for them.</span></span> <span data-ttu-id="535f3-131">(Merhaba sanal makineler aynı kullanılabilirlik kümesinde hello unutmayın toohello ait olmalıdır aynı bulut hizmetine.) Merhaba adımları olan neredeyse hello aynı.</span><span class="sxs-lookup"><span data-stu-id="535f3-131">(Keep in mind that hello virtual machines in hello same availability set must belong toohello same cloud service.) hello steps are almost hello same.</span></span> <span data-ttu-id="535f3-132">Azure PowerShell ile Merhaba sanal makine tooan varolan kullanılabilirlik kümesi ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="535f3-132">With Azure PowerShell, you can add hello virtual machine tooan existing availability set.</span></span>

1. <span data-ttu-id="535f3-133">Zaten yapmadıysanız, toohello içinde oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="535f3-133">If you have not already done so, sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="535f3-134">Merhaba Hub menüsünde **sanal makineleri (Klasik)**.</span><span class="sxs-lookup"><span data-stu-id="535f3-134">On hello Hub menu, click **Virtual Machines (classic)**.</span></span>
   
    ![Alt görüntü metin](./media/virtual-machines-common-classic-configure-availability/ChooseClassicVM.png)
3. <span data-ttu-id="535f3-136">Sanal makineler Hello listeden hello tooadd toohello kümesi istediğiniz hello sanal makinenin adını seçin.</span><span class="sxs-lookup"><span data-stu-id="535f3-136">From hello list of virtual machines, select hello name of hello virtual machine that you want tooadd toohello set.</span></span>
4. <span data-ttu-id="535f3-137">Seçin **kullanılabilirlik kümesi** hello sanal makineden **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="535f3-137">Choose **Availability set** from hello virtual machine **Settings**.</span></span>
   
    ![Alt görüntü metin](./media/virtual-machines-common-classic-configure-availability/AvailabilitySetSettings.png)
5. <span data-ttu-id="535f3-139">Tooadd hello sanal makineye istediğiniz hello kullanılabilirlik kümesi seçin.</span><span class="sxs-lookup"><span data-stu-id="535f3-139">Select hello availability set you wish tooadd hello virtual machine to.</span></span> <span data-ttu-id="535f3-140">Merhaba sanal makine toohello ait olmalıdır hello kullanılabilirlik kümesi aynı bulut hizmeti.</span><span class="sxs-lookup"><span data-stu-id="535f3-140">hello virtual machine must belong toohello same cloud service as hello availability set.</span></span>
   
    ![Alt görüntü metin](./media/virtual-machines-common-classic-configure-availability/AvailabilitySetPicker.png)
6. <span data-ttu-id="535f3-142">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="535f3-142">Click **Save**.</span></span>

<span data-ttu-id="535f3-143">toouse Azure PowerShell komutları, bir yönetici düzeyi Azure PowerShell oturumu açın ve hello aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="535f3-143">toouse Azure PowerShell commands, open an administrator-level Azure PowerShell session and run hello following command.</span></span> <span data-ttu-id="535f3-144">Merhaba yer tutucuları için (gibi &lt;VmCloudServiceName&gt;), merhaba < ve > karakterleri dahil olmak üzere hello tırnak içindeki her şeyi değiştirin, adları ile Merhaba düzeltin.</span><span class="sxs-lookup"><span data-stu-id="535f3-144">For hello placeholders (such as &lt;VmCloudServiceName&gt;), replace everything within hello quotes, including hello < and > characters, with hello correct names.</span></span>

    Get-AzureVM -ServiceName "<VmCloudServiceName>" -Name "<VmName>" | Set-AzureAvailabilitySet -AvailabilitySetName "<AvSetName>" | Update-AzureVM

> [!NOTE]
> <span data-ttu-id="535f3-145">Merhaba sanal makine yeniden toobe toofinish toohello kullanılabilirlik kümesi ekleme sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="535f3-145">hello virtual machine might have toobe restarted toofinish adding it toohello availability set.</span></span>
> 
> 

<!-- LINKS -->
[Option 1: Create a virtual machine and an availability set at hello same time]: #createset
[Option 2: Add an existing virtual machine tooan availability set]: #addmachine

[Load balancing for Azure infrastructure services]: ../articles/virtual-machines/virtual-machines-linux-load-balance.md
[Manage hello availability of virtual machines]:../articles/virtual-machines/linux/manage-availability.md

[Create a virtual machine running Windows]: ../articles/virtual-machines/virtual-machines-windows-hero-tutorial.md
[Virtual Network overview]: ../articles/virtual-network/virtual-networks-overview.md

