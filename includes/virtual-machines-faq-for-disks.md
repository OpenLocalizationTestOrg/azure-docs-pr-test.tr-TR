# <a name="frequently-asked-questions-about-azure-iaas-vm-disks-and-managed-and-unmanaged-premium-disks"></a><span data-ttu-id="b58fb-101">Azure Iaas sanal diskler ve yönetilen ve yönetilmeyen premium diskler hakkında sık sorulan sorular</span><span class="sxs-lookup"><span data-stu-id="b58fb-101">Frequently asked questions about Azure IaaS VM disks and managed and unmanaged premium disks</span></span>

<span data-ttu-id="b58fb-102">Bu makalede Azure yönetilen diskleri ve Azure Premium Storage hakkında sık sorulan bazı sorular yanıtlanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="b58fb-102">This article answers some frequently asked questions about Azure Managed Disks and Azure Premium Storage.</span></span>

## <a name="managed-disks"></a><span data-ttu-id="b58fb-103">Yönetilen Diskler</span><span class="sxs-lookup"><span data-stu-id="b58fb-103">Managed Disks</span></span>

<span data-ttu-id="b58fb-104">**Azure yönetilen diskleri nedir?**</span><span class="sxs-lookup"><span data-stu-id="b58fb-104">**What is Azure Managed Disks?**</span></span>

<span data-ttu-id="b58fb-105">Yönetilen diskleri depolama hesabı yönetimini işleyerek Azure Iaas VM'ler için disk yönetimi basitleştiren bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="b58fb-105">Managed Disks is a feature that simplifies disk management for Azure IaaS VMs by handling storage account management for you.</span></span> <span data-ttu-id="b58fb-106">Daha fazla bilgi için bkz: Merhaba [yönetilen diskleri genel bakış](../articles/virtual-machines/windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b58fb-106">For more information, see hello [Managed Disks overview](../articles/virtual-machines/windows/managed-disks-overview.md).</span></span>

<span data-ttu-id="b58fb-107">**Standart yönetilen disk 80 GB olan varolan bir VHD'yi oluşturursanız, ne kadar bana maliyeti ne olacak?**</span><span class="sxs-lookup"><span data-stu-id="b58fb-107">**If I create a standard managed disk from an existing VHD that's 80 GB, how much will that cost me?**</span></span>

<span data-ttu-id="b58fb-108">80 GB VHD'den oluşturulan standart yönetilen disk S10 disk hello sonraki kullanılabilir standart disk boyutu kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="b58fb-108">A standard managed disk created from an 80-GB VHD is treated as hello next available standard disk size, which is an S10 disk.</span></span> <span data-ttu-id="b58fb-109">According toohello S10 disk fiyatlandırma ücret ödersiniz.</span><span class="sxs-lookup"><span data-stu-id="b58fb-109">You're charged according toohello S10 disk pricing.</span></span> <span data-ttu-id="b58fb-110">Daha fazla bilgi için bkz: Merhaba [fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="b58fb-110">For more information, see hello [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="b58fb-111">**Standart yönetilen disk için herhangi bir işlem maliyetleri vardır?**</span><span class="sxs-lookup"><span data-stu-id="b58fb-111">**Are there any transaction costs for standard managed disks?**</span></span>

<span data-ttu-id="b58fb-112">Evet.</span><span class="sxs-lookup"><span data-stu-id="b58fb-112">Yes.</span></span> <span data-ttu-id="b58fb-113">Her işlem için ücret ödersiniz.</span><span class="sxs-lookup"><span data-stu-id="b58fb-113">You're charged for each transaction.</span></span> <span data-ttu-id="b58fb-114">Daha fazla bilgi için bkz: Merhaba [fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="b58fb-114">For more information, see hello [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="b58fb-115">**Standart yönetilen disk için sağlanan hello hello disk kapasitesini veya hello gerçek hello diskteki hello verilerin boyutunu için t ücretlendirilir?**</span><span class="sxs-lookup"><span data-stu-id="b58fb-115">**For a standard managed disk, will I be charged for hello actual size of hello data on hello disk or for hello provisioned capacity of hello disk?**</span></span>

<span data-ttu-id="b58fb-116">Sağlanan hello hello disk kapasitesine göre ücret ödersiniz.</span><span class="sxs-lookup"><span data-stu-id="b58fb-116">You're charged based on hello provisioned capacity of hello disk.</span></span> <span data-ttu-id="b58fb-117">Daha fazla bilgi için bkz: Merhaba [fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="b58fb-117">For more information, see hello [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="b58fb-118">**Nasıl yönetilen premium diskleri yönetilmeyen disklerden farklı fiyatlandırma olduğu?**</span><span class="sxs-lookup"><span data-stu-id="b58fb-118">**How is pricing of premium managed disks different from unmanaged disks?**</span></span>

<span data-ttu-id="b58fb-119">Yönetilen premium diskleri Hello fiyatlandırma olduğu hello yönetilmeyen premium diskler ile aynı.</span><span class="sxs-lookup"><span data-stu-id="b58fb-119">hello pricing of premium managed disks is hello same as unmanaged premium disks.</span></span>

<span data-ttu-id="b58fb-120">**Merhaba depolama hesabı türü (standart veya Premium) yönetilen disklerim değiştirebilir miyim?**</span><span class="sxs-lookup"><span data-stu-id="b58fb-120">**Can I change hello storage account type (Standard or Premium) of my managed disks?**</span></span>

<span data-ttu-id="b58fb-121">Evet.</span><span class="sxs-lookup"><span data-stu-id="b58fb-121">Yes.</span></span> <span data-ttu-id="b58fb-122">Hello Azure portal, PowerShell veya hello Azure CLI kullanarak yönetilen disklerinizi hello depolama hesabı türünü değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b58fb-122">You can change hello storage account type of your managed disks by using hello Azure portal, PowerShell, or hello Azure CLI.</span></span>

<span data-ttu-id="b58fb-123">**I kopyalayın veya böylelikle yönetilen disk tooa özel depolama hesabını verme bir yolu var mı?**</span><span class="sxs-lookup"><span data-stu-id="b58fb-123">**Is there a way that I can copy or export a managed disk tooa private storage account?**</span></span>

<span data-ttu-id="b58fb-124">Evet.</span><span class="sxs-lookup"><span data-stu-id="b58fb-124">Yes.</span></span> <span data-ttu-id="b58fb-125">Hello Azure portal, PowerShell veya hello Azure CLI kullanarak yönetilen disklerinizi dışarı aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b58fb-125">You can export your managed disks by using hello Azure portal, PowerShell, or hello Azure CLI.</span></span>

<span data-ttu-id="b58fb-126">**Bir Azure depolama hesabı toocreate yönetilen bir disk VHD dosyasında farklı bir aboneliğe kullanabilir miyim?**</span><span class="sxs-lookup"><span data-stu-id="b58fb-126">**Can I use a VHD file in an Azure storage account toocreate a managed disk with a different subscription?**</span></span>

<span data-ttu-id="b58fb-127">Hayır.</span><span class="sxs-lookup"><span data-stu-id="b58fb-127">No.</span></span>

<span data-ttu-id="b58fb-128">**Farklı bir bölgede bir Azure depolama hesabı toocreate yönetilen bir disk VHD dosyasında kullanabilir miyim?**</span><span class="sxs-lookup"><span data-stu-id="b58fb-128">**Can I use a VHD file in an Azure storage account toocreate a managed disk in a different region?**</span></span>

<span data-ttu-id="b58fb-129">Hayır.</span><span class="sxs-lookup"><span data-stu-id="b58fb-129">No.</span></span>

<span data-ttu-id="b58fb-130">**Yönetilen diskler kullanan müşteriler için ölçek sınırlamalar var mı?**</span><span class="sxs-lookup"><span data-stu-id="b58fb-130">**Are there any scale limitations for customers that use managed disks?**</span></span>

<span data-ttu-id="b58fb-131">Yönetilen diskleri depolama hesaplarıyla ilişkili hello sınırları ortadan kaldırır.</span><span class="sxs-lookup"><span data-stu-id="b58fb-131">Managed Disks eliminates hello limits associated with storage accounts.</span></span> <span data-ttu-id="b58fb-132">Ancak, hello yönetilen diskleri abonelik başına sınırlı too2, varsayılan olarak 000 sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="b58fb-132">However, hello number of managed disks per subscription is limited too2,000 by default.</span></span> <span data-ttu-id="b58fb-133">Bu sayı destek tooincrease çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b58fb-133">You can call support tooincrease this number.</span></span>

<span data-ttu-id="b58fb-134">**Yönetilen bir diskin artımlı bir anlık görüntüsünü alın?**</span><span class="sxs-lookup"><span data-stu-id="b58fb-134">**Can I take an incremental snapshot of a managed disk?**</span></span>

<span data-ttu-id="b58fb-135">Hayır.</span><span class="sxs-lookup"><span data-stu-id="b58fb-135">No.</span></span> <span data-ttu-id="b58fb-136">Merhaba geçerli anlık görüntü özelliği yönetilen bir disk tam bir kopyasını oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b58fb-136">hello current snapshot capability makes a full copy of a managed disk.</span></span> <span data-ttu-id="b58fb-137">Ancak, biz toosupport artımlı anlık görüntülerini hello gelecekteki planladığınıza.</span><span class="sxs-lookup"><span data-stu-id="b58fb-137">However, we are planning toosupport incremental snapshots in hello future.</span></span>

<span data-ttu-id="b58fb-138">**Sanal makineleri bir kullanılabilirlik kümesinde yönetilen ve yönetilmeyen diskleri birleşiminden oluşabilir?**</span><span class="sxs-lookup"><span data-stu-id="b58fb-138">**Can VMs in an availability set consist of a combination of managed and unmanaged disks?**</span></span>

<span data-ttu-id="b58fb-139">Hayır.</span><span class="sxs-lookup"><span data-stu-id="b58fb-139">No.</span></span> <span data-ttu-id="b58fb-140">Merhaba sanal makineleri bir kullanılabilirlik kümesinde, tüm yönetilen diskleri veya tüm yönetilmeyen diskler kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b58fb-140">hello VMs in an availability set must use either all managed disks or all unmanaged disks.</span></span> <span data-ttu-id="b58fb-141">Bir kullanılabilirlik kümesi oluşturduğunuzda, disk türünü seçebilirsiniz toouse istiyor.</span><span class="sxs-lookup"><span data-stu-id="b58fb-141">When you create an availability set, you can choose which type of disks you want toouse.</span></span>

<span data-ttu-id="b58fb-142">**Yönetilen diskleri hello varsayılan seçeneği hello Azure portal mi?**</span><span class="sxs-lookup"><span data-stu-id="b58fb-142">**Is Managed Disks hello default option in hello Azure portal?**</span></span>

<span data-ttu-id="b58fb-143">Şu anda değil ancak gelecekteki hello hello varsayılan olur.</span><span class="sxs-lookup"><span data-stu-id="b58fb-143">Not currently, but it will become hello default in hello future.</span></span>

<span data-ttu-id="b58fb-144">**Boş bir yönetilen diski oluşturabilir miyim?**</span><span class="sxs-lookup"><span data-stu-id="b58fb-144">**Can I create an empty managed disk?**</span></span>

<span data-ttu-id="b58fb-145">Evet.</span><span class="sxs-lookup"><span data-stu-id="b58fb-145">Yes.</span></span> <span data-ttu-id="b58fb-146">Boş bir disk oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b58fb-146">You can create an empty disk.</span></span> <span data-ttu-id="b58fb-147">Yönetilen bir disk tooa VM eklemeden VM bağımsız olarak, örneğin, oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="b58fb-147">A managed disk can be created independently of a VM, for example, without attaching it tooa VM.</span></span>

<span data-ttu-id="b58fb-148">**Yönetilen diskleri kullanan bir kullanılabilirlik kümesi için desteklenen hello hata etki alanı sayısı nedir?**</span><span class="sxs-lookup"><span data-stu-id="b58fb-148">**What is hello supported fault domain count for an availability set that uses Managed Disks?**</span></span>

<span data-ttu-id="b58fb-149">Yönetilen diskleri kullanan hello kullanılabilirlik kümesi bulunduğu hello bağlı olarak, desteklenen hello hata etki alanı sayısı 2 veya 3 bölgedir.</span><span class="sxs-lookup"><span data-stu-id="b58fb-149">Depending on hello region where hello availability set that uses Managed Disks is located, hello supported fault domain count is 2 or 3.</span></span>

<span data-ttu-id="b58fb-150">**Nasıl ayarlanan diagnostics hello standart depolama hesabı mı?**</span><span class="sxs-lookup"><span data-stu-id="b58fb-150">**How is hello standard storage account for diagnostics set up?**</span></span>

<span data-ttu-id="b58fb-151">VM tanılama için özel depolama hesabı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="b58fb-151">You set up a private storage account for VM diagnostics.</span></span> <span data-ttu-id="b58fb-152">Hello gelecekteki, biz tooswitch tanılama planlama tooManaged diskler.</span><span class="sxs-lookup"><span data-stu-id="b58fb-152">In hello future, we plan tooswitch diagnostics tooManaged Disks as well.</span></span>

<span data-ttu-id="b58fb-153">**Ne tür bir rol tabanlı erişim denetimi desteğini yönetilen disklerde var mı?**</span><span class="sxs-lookup"><span data-stu-id="b58fb-153">**What kind of Role-Based Access Control support is available for Managed Disks?**</span></span>

<span data-ttu-id="b58fb-154">Diskleri desteklediği üç anahtar varsayılan rol yönetilen:</span><span class="sxs-lookup"><span data-stu-id="b58fb-154">Managed Disks supports three key default roles:</span></span>

* <span data-ttu-id="b58fb-155">Sahibi: erişim dahil her şeyi yönetebilir</span><span class="sxs-lookup"><span data-stu-id="b58fb-155">Owner: Can manage everything, including access</span></span>
* <span data-ttu-id="b58fb-156">Katkıda bulunan: erişim dışında her şeyi yönetebilir</span><span class="sxs-lookup"><span data-stu-id="b58fb-156">Contributor: Can manage everything except access</span></span>
* <span data-ttu-id="b58fb-157">Okuyucu: her şeyi görüntüleyebilir ancak değişiklik yapamaz</span><span class="sxs-lookup"><span data-stu-id="b58fb-157">Reader: Can view everything, but can't make changes</span></span>

<span data-ttu-id="b58fb-158">**I kopyalayın veya böylelikle yönetilen disk tooa özel depolama hesabını verme bir yolu var mı?**</span><span class="sxs-lookup"><span data-stu-id="b58fb-158">**Is there a way that I can copy or export a managed disk tooa private storage account?**</span></span>

<span data-ttu-id="b58fb-159">Hesap ya da şirket içi toocopy hello içeriği tooa özel depolama depolama URI yönetilen hello için disk ve kullanacak salt okunur paylaşılan erişim imzası elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b58fb-159">You can get a read-only shared access signature URI for hello managed disk and use it toocopy hello contents tooa private storage account or on-premises storage.</span></span>

<span data-ttu-id="b58fb-160">**Yönetilen my disk kopyasını oluşturabilir miyim?**</span><span class="sxs-lookup"><span data-stu-id="b58fb-160">**Can I create a copy of my managed disk?**</span></span>

<span data-ttu-id="b58fb-161">Müşteriler, kendi yönetilen diskleri bir anlık görüntüsünü ve ardından başka bir yönetilen disk hello anlık görüntü toocreate kullanın.</span><span class="sxs-lookup"><span data-stu-id="b58fb-161">Customers can take a snapshot of their managed disks and then use hello snapshot toocreate another managed disk.</span></span>

<span data-ttu-id="b58fb-162">**Yönetilmeyen diskleri hala desteklenmektedir?**</span><span class="sxs-lookup"><span data-stu-id="b58fb-162">**Are unmanaged disks still supported?**</span></span>

<span data-ttu-id="b58fb-163">Evet.</span><span class="sxs-lookup"><span data-stu-id="b58fb-163">Yes.</span></span> <span data-ttu-id="b58fb-164">Yönetilen ve yönetilmeyen diskleri destekliyoruz.</span><span class="sxs-lookup"><span data-stu-id="b58fb-164">We support unmanaged and managed disks.</span></span> <span data-ttu-id="b58fb-165">Yeni iş yükleri için yönetilen diskleri kullanın ve geçerli iş yükleri toomanaged disklerinizi geçirmenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="b58fb-165">We recommend that you use managed disks for new workloads and migrate your current workloads toomanaged disks.</span></span>


<span data-ttu-id="b58fb-166">**128 GB disk oluşturma ve hello boyutu too130 GB artırın, ı hello sonraki için disk boyutu (512 GB) ücretlendirilir?**</span><span class="sxs-lookup"><span data-stu-id="b58fb-166">**If I create a 128-GB disk and then increase hello size too130 GB, will I be charged for hello next disk size (512 GB)?**</span></span>

<span data-ttu-id="b58fb-167">Evet.</span><span class="sxs-lookup"><span data-stu-id="b58fb-167">Yes.</span></span>

<span data-ttu-id="b58fb-168">**Yerel olarak yedekli depolama, coğrafi olarak yedekli depolama, oluşturabiliyorum ve bölge olarak yedekli depolama yönetilen disklerde?**</span><span class="sxs-lookup"><span data-stu-id="b58fb-168">**Can I create locally redundant storage, geo-redundant storage, and zone-redundant storage managed disks?**</span></span>

<span data-ttu-id="b58fb-169">Azure yönetilen diskleri şu anda yönetilen yalnızca yerel olarak yedekli depolama disklerini destekler.</span><span class="sxs-lookup"><span data-stu-id="b58fb-169">Azure Managed Disks currently supports only locally redundant storage managed disks.</span></span>

<span data-ttu-id="b58fb-170">**Daraltma veya miyim yönetilen disklerim downsize?**</span><span class="sxs-lookup"><span data-stu-id="b58fb-170">**Can I shrink or downsize my managed disks?**</span></span>

<span data-ttu-id="b58fb-171">Hayır.</span><span class="sxs-lookup"><span data-stu-id="b58fb-171">No.</span></span> <span data-ttu-id="b58fb-172">Bu özellik şu anda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="b58fb-172">This feature is not supported currently.</span></span> 

<span data-ttu-id="b58fb-173">**Merhaba bilgisayar adı özelliği, özelleştirilmiş (Merhaba Sistem Hazırlama aracı kullanılarak oluşturulan veya genelleştirilmiş) işletim sistemi diski kullanılan tooprovision VM olduğunda değiştirebilir miyim?**</span><span class="sxs-lookup"><span data-stu-id="b58fb-173">**Can I change hello computer name property when a specialized (not created by using hello System Preparation tool or generalized) operating system disk is used tooprovision a VM?**</span></span>

<span data-ttu-id="b58fb-174">Hayır.</span><span class="sxs-lookup"><span data-stu-id="b58fb-174">No.</span></span> <span data-ttu-id="b58fb-175">Merhaba bilgisayar adı özelliği güncelleştirilemiyor.</span><span class="sxs-lookup"><span data-stu-id="b58fb-175">You can't update hello computer name property.</span></span> <span data-ttu-id="b58fb-176">Merhaba yeni VM hello üst kullanılan toocreate hello işletim sistemi disk VM devralır.</span><span class="sxs-lookup"><span data-stu-id="b58fb-176">hello new VM inherits it from hello parent VM, which was used toocreate hello operating system disk.</span></span> 

<span data-ttu-id="b58fb-177">**Yönetilen disklerle örnek Azure Resource Manager şablonları toocreate VM'ler nereden bulabilirim?**</span><span class="sxs-lookup"><span data-stu-id="b58fb-177">**Where can I find sample Azure Resource Manager templates toocreate VMs with managed disks?**</span></span>
* [<span data-ttu-id="b58fb-178">Yönetilen diskleri kullanarak şablonları</span><span class="sxs-lookup"><span data-stu-id="b58fb-178">List of templates using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)
* <span data-ttu-id="b58fb-179">https://github.com/chagarw/MDPP</span><span class="sxs-lookup"><span data-stu-id="b58fb-179">https://github.com/chagarw/MDPP</span></span>

## <a name="managed-disks-and-storage-service-encryption"></a><span data-ttu-id="b58fb-180">Diskler ve depolama hizmeti şifrelemesi yönetilen</span><span class="sxs-lookup"><span data-stu-id="b58fb-180">Managed Disks and Storage Service Encryption</span></span> 

<span data-ttu-id="b58fb-181">**Azure depolama hizmeti şifrelemesi, yönetilen bir disk oluşturduğunuzda, varsayılan olarak etkindir?**</span><span class="sxs-lookup"><span data-stu-id="b58fb-181">**Is Azure Storage Service Encryption enabled by default when I create a managed disk?**</span></span>

<span data-ttu-id="b58fb-182">Evet.</span><span class="sxs-lookup"><span data-stu-id="b58fb-182">Yes.</span></span>

<span data-ttu-id="b58fb-183">**Merhaba şifreleme anahtarları yöneten?**</span><span class="sxs-lookup"><span data-stu-id="b58fb-183">**Who manages hello encryption keys?**</span></span>

<span data-ttu-id="b58fb-184">Microsoft hello şifreleme anahtarları yönetir.</span><span class="sxs-lookup"><span data-stu-id="b58fb-184">Microsoft manages hello encryption keys.</span></span>

<span data-ttu-id="b58fb-185">**I depolama hizmeti şifrelemesi yönetilen disklerim için devre dışı bırakabilirim?**</span><span class="sxs-lookup"><span data-stu-id="b58fb-185">**Can I disable Storage Service Encryption for my managed disks?**</span></span>

<span data-ttu-id="b58fb-186">Hayır.</span><span class="sxs-lookup"><span data-stu-id="b58fb-186">No.</span></span>

<span data-ttu-id="b58fb-187">**Depolama hizmeti şifrelemesi, yalnızca belirli bölgelerde kullanılabilir?**</span><span class="sxs-lookup"><span data-stu-id="b58fb-187">**Is Storage Service Encryption only available in specific regions?**</span></span>

<span data-ttu-id="b58fb-188">Hayır.</span><span class="sxs-lookup"><span data-stu-id="b58fb-188">No.</span></span> <span data-ttu-id="b58fb-189">Tarafından yönetilen diskleri kullanılabilir olduğu tüm hello bölgelerde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="b58fb-189">It's available in all hello regions where Managed Disks is available.</span></span> <span data-ttu-id="b58fb-190">Yönetilen diskleri kullanılabilir tüm genel bölgeler ve Almanya.</span><span class="sxs-lookup"><span data-stu-id="b58fb-190">Managed Disks is available in all public regions and Germany.</span></span>

<span data-ttu-id="b58fb-191">**Nasıl ı yönetilen my disk şifrelenir öğrenebilirsiniz?**</span><span class="sxs-lookup"><span data-stu-id="b58fb-191">**How can I find out if my managed disk is encrypted?**</span></span>

<span data-ttu-id="b58fb-192">Yönetilen bir disk hello Azure portal, hello Azure CLI ve PowerShell oluşturulduğu hello zaman bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b58fb-192">You can find out hello time when a managed disk was created from hello Azure portal, hello Azure CLI, and PowerShell.</span></span> <span data-ttu-id="b58fb-193">Merhaba saat 9 Haziran 2017 sonra ise, disk şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="b58fb-193">If hello time is after June 9, 2017, then your disk is encrypted.</span></span> 

<span data-ttu-id="b58fb-194">**10 Haziran 2017 önce oluşturulan mevcut disklerim nasıl şifreleyebilir mi?**</span><span class="sxs-lookup"><span data-stu-id="b58fb-194">**How can I encrypt my existing disks that were created before June 10, 2017?**</span></span>

<span data-ttu-id="b58fb-195">10 Haziran 2017 itibariyle yönetilen tooexisting diskleri yazılan yeni veriler otomatik olarak şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="b58fb-195">As of June 10, 2017, new data written tooexisting managed disks is automatically encrypted.</span></span> <span data-ttu-id="b58fb-196">Biz de tooencrypt var olan verileri planlama ve hello şifreleme zaman uyumsuz olarak hello arka planda gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="b58fb-196">We are also planning tooencrypt existing data, and hello encryption will happen asynchronously in hello background.</span></span> <span data-ttu-id="b58fb-197">Var olan verileri artık şifrelemeniz gerekir, diskinizin bir kopyasını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b58fb-197">If you must encrypt existing data now, create a copy of your disk.</span></span> <span data-ttu-id="b58fb-198">Yeni disk şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="b58fb-198">New disks will be encrypted.</span></span>

* [<span data-ttu-id="b58fb-199">Hello Azure CLI kullanarak yönetilen diskleri kopyalama</span><span class="sxs-lookup"><span data-stu-id="b58fb-199">Copy managed disks by using hello Azure CLI</span></span>](../articles/virtual-machines/scripts/virtual-machines-linux-cli-sample-copy-managed-disks-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json)
* [<span data-ttu-id="b58fb-200">PowerShell kullanarak yönetilen diskleri kopyalama</span><span class="sxs-lookup"><span data-stu-id="b58fb-200">Copy managed disks by using PowerShell</span></span>](../articles/virtual-machines/scripts/virtual-machines-windows-powershell-sample-copy-managed-disks-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="b58fb-201">**Yönetilen anlık görüntüler ve şifrelenmiş görüntüleri misiniz?**</span><span class="sxs-lookup"><span data-stu-id="b58fb-201">**Are managed snapshots and images encrypted?**</span></span>

<span data-ttu-id="b58fb-202">Evet.</span><span class="sxs-lookup"><span data-stu-id="b58fb-202">Yes.</span></span> <span data-ttu-id="b58fb-203">Yönetilen tüm anlık görüntüler ve 9 Haziran 2017 sonra oluşturulan görüntüleri otomatik olarak şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="b58fb-203">All managed snapshots and images created after June 9, 2017, are automatically encrypted.</span></span> 

<span data-ttu-id="b58fb-204">**Sanal makineleri olan veya önceden şifrelenmiş toomanaged diskleri depolama hesaplarında yer alan yönetilmeyen disklerle dönüştürebilirsiniz?**</span><span class="sxs-lookup"><span data-stu-id="b58fb-204">**Can I convert VMs with unmanaged disks that are located on storage accounts that are or were previously encrypted toomanaged disks?**</span></span>

<span data-ttu-id="b58fb-205">Evet</span><span class="sxs-lookup"><span data-stu-id="b58fb-205">Yes</span></span>

<span data-ttu-id="b58fb-206">**Yönetilen bir disk veya bir anlık görüntü dışarı aktarılan bir VHD'den de şifrelenir mi?**</span><span class="sxs-lookup"><span data-stu-id="b58fb-206">**Will an exported VHD from a managed disk or a snapshot also be encrypted?**</span></span>

<span data-ttu-id="b58fb-207">Hayır.</span><span class="sxs-lookup"><span data-stu-id="b58fb-207">No.</span></span> <span data-ttu-id="b58fb-208">Ancak, bir VHD tooan dışa depolama hesabından bir şifrelenmiş yönetilen disk veya anlık görüntü şifrelenmiş sonra şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="b58fb-208">But if you export a VHD tooan encrypted storage account from an encrypted managed disk or snapshot, then it's encrypted.</span></span> 

## <a name="premium-disks-managed-and-unmanaged"></a><span data-ttu-id="b58fb-209">Premium diskler: yönetilen ve yönetilmeyen</span><span class="sxs-lookup"><span data-stu-id="b58fb-209">Premium disks: Managed and unmanaged</span></span>

<span data-ttu-id="b58fb-210">**VM bir DSv2 gibi Premium Storage destekleyen bir boyutu serisi kullanıyorsa ı premium ve standart veri diskleri ekleyebilir miyim?**</span><span class="sxs-lookup"><span data-stu-id="b58fb-210">**If a VM uses a size series that supports Premium Storage, such as a DSv2, can I attach both premium and standard data disks?**</span></span> 

<span data-ttu-id="b58fb-211">Evet.</span><span class="sxs-lookup"><span data-stu-id="b58fb-211">Yes.</span></span>

<span data-ttu-id="b58fb-212">**Premium ve Premium depolama D, Dv2, G veya F serisi gibi desteklemiyor standart veri diskleri tooa boyutu serisi ekleyebilir miyim?**</span><span class="sxs-lookup"><span data-stu-id="b58fb-212">**Can I attach both premium and standard data disks tooa size series that doesn't support Premium Storage, such as D, Dv2, G, or F series?**</span></span>

<span data-ttu-id="b58fb-213">Hayır.</span><span class="sxs-lookup"><span data-stu-id="b58fb-213">No.</span></span> <span data-ttu-id="b58fb-214">Premium Storage destekleyen bir boyutu serisi kullanmayan standart veri diskleri tooVMs ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b58fb-214">You can attach only standard data disks tooVMs that don't use a size series that supports Premium Storage.</span></span>

<span data-ttu-id="b58fb-215">**80 GB varolan bir VHD'den premium veri diski oluşturursanız, ne kadar maliyeti ne olacak?**</span><span class="sxs-lookup"><span data-stu-id="b58fb-215">**If I create a premium data disk from an existing VHD that was 80 GB, how much will that cost?**</span></span>

<span data-ttu-id="b58fb-216">80 GB VHD'den oluşturulan bir premium veri diski P10 disk hello sonraki kullanılabilir premium disk boyutu kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="b58fb-216">A premium data disk created from an 80-GB VHD is treated as hello next-available premium disk size, which is a P10 disk.</span></span> <span data-ttu-id="b58fb-217">According toohello P10 disk fiyatlandırma ücret ödersiniz.</span><span class="sxs-lookup"><span data-stu-id="b58fb-217">You're charged according toohello P10 disk pricing.</span></span>

<span data-ttu-id="b58fb-218">**İşlem maliyetleri toouse Premium depolama var mı?**</span><span class="sxs-lookup"><span data-stu-id="b58fb-218">**Are there transaction costs toouse Premium Storage?**</span></span>

<span data-ttu-id="b58fb-219">IOPS ve üretilen iş ile belirli sınırları sağlanan gelen her disk boyutu için sabit bir maliyeti yoktur.</span><span class="sxs-lookup"><span data-stu-id="b58fb-219">There is a fixed cost for each disk size, which comes provisioned with specific limits on IOPS and throughput.</span></span> <span data-ttu-id="b58fb-220">Merhaba diğer maliyetlerin giden bant genişliği ve anlık görüntü kapasite varsa markalarıdır.</span><span class="sxs-lookup"><span data-stu-id="b58fb-220">hello other costs are outbound bandwidth and snapshot capacity, if applicable.</span></span> <span data-ttu-id="b58fb-221">Daha fazla bilgi için bkz: Merhaba [fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="b58fb-221">For more information, see hello [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="b58fb-222">**IOPS ve hello disk önbellekten elde edebilirsiniz işleme için hello sınırları nelerdir?**</span><span class="sxs-lookup"><span data-stu-id="b58fb-222">**What are hello limits for IOPS and throughput that I can get from hello disk cache?**</span></span>

<span data-ttu-id="b58fb-223">önbellek için birleşik sınırları hello ve DS serisi için yerel SSD: çekirdek başına 4.000 IOPS ve çekirdek saniyede 33 MB.</span><span class="sxs-lookup"><span data-stu-id="b58fb-223">hello combined limits for cache and local SSD for a DS series are 4,000 IOPS per core and 33 MB per second per core.</span></span> <span data-ttu-id="b58fb-224">Merhaba GS serisi çekirdek başına 5.000 IOPS'yi ve çekirdek saniyede 50 MB sunar.</span><span class="sxs-lookup"><span data-stu-id="b58fb-224">hello GS series offers 5,000 IOPS per core and 50 MB per second per core.</span></span>

<span data-ttu-id="b58fb-225">**Yerel SSD yönetilen diskleri VM için desteklenen hello mi?**</span><span class="sxs-lookup"><span data-stu-id="b58fb-225">**Is hello local SSD supported for a Managed Disks VM?**</span></span>

<span data-ttu-id="b58fb-226">Merhaba yerel SSD yönetilen diskleri VM ile birlikte sağlanan geçici depolama olur.</span><span class="sxs-lookup"><span data-stu-id="b58fb-226">hello local SSD is temporary storage that is included with a Managed Disks VM.</span></span> <span data-ttu-id="b58fb-227">Var. ek bu geçici depolama için bir maliyeti yoktur.</span><span class="sxs-lookup"><span data-stu-id="b58fb-227">There is no extra cost for this temporary storage.</span></span> <span data-ttu-id="b58fb-228">Azure Blob depolama alanına kalıcı değildir çünkü bu yerel SSD toostore'ı uygulama verilerinizi kullanmamanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="b58fb-228">We recommend that you do not use this local SSD toostore your application data because it isn't persisted in Azure Blob storage.</span></span>

<span data-ttu-id="b58fb-229">**Var. herhangi varsa hello için kullanacağı KIRPMA premium disklerde?**</span><span class="sxs-lookup"><span data-stu-id="b58fb-229">**Are there any repercussions for hello use of TRIM on premium disks?**</span></span>

<span data-ttu-id="b58fb-230">Hiçbir KIRPMA ya da premium Azure disklerde veya standart diskler dezavantajı toohello kullanımını yoktur.</span><span class="sxs-lookup"><span data-stu-id="b58fb-230">There is no downside toohello use of TRIM on Azure disks on either premium or standard disks.</span></span>

## <a name="new-disk-sizes-managed-and-unmanaged"></a><span data-ttu-id="b58fb-231">Yeni disk boyutları: yönetilen ve yönetilmeyen</span><span class="sxs-lookup"><span data-stu-id="b58fb-231">New disk sizes: Managed and unmanaged</span></span>

<span data-ttu-id="b58fb-232">**Merhaba işletim sistemi ve veri diskleri için desteklenen en büyük disk boyutu nedir?**</span><span class="sxs-lookup"><span data-stu-id="b58fb-232">**What is hello largest disk size supported for operating system and data disks?**</span></span>

<span data-ttu-id="b58fb-233">bir işletim sistemi diski için Azure destekleyen hello bölüm hello ana önyükleme kaydı (MBR) türüdür.</span><span class="sxs-lookup"><span data-stu-id="b58fb-233">hello partition type that Azure supports for an operating system disk is hello master boot record (MBR).</span></span> <span data-ttu-id="b58fb-234">Merhaba MBR biçimi too2 TB bir disk boyutunu destekler.</span><span class="sxs-lookup"><span data-stu-id="b58fb-234">hello MBR format supports a disk size up too2 TB.</span></span> <span data-ttu-id="b58fb-235">bir işletim sistemi diski için Azure destekleyen hello en büyük boyutu 2 TB ' dir.</span><span class="sxs-lookup"><span data-stu-id="b58fb-235">hello largest size that Azure supports for an operating system disk is 2 TB.</span></span> <span data-ttu-id="b58fb-236">Veri diskleri too4 TB yukarı Azure destekler.</span><span class="sxs-lookup"><span data-stu-id="b58fb-236">Azure supports up too4 TB for data disks.</span></span> 

<span data-ttu-id="b58fb-237">**Desteklenen hello büyük sayfa blob boyutu nedir?**</span><span class="sxs-lookup"><span data-stu-id="b58fb-237">**What is hello largest page blob size that's supported?**</span></span>

<span data-ttu-id="b58fb-238">Azure destekleyen hello büyük sayfa blob boyutu 8 TB (8191 GB) ' dir.</span><span class="sxs-lookup"><span data-stu-id="b58fb-238">hello largest page blob size that Azure supports is 8 TB (8,191 GB).</span></span> <span data-ttu-id="b58fb-239">Sayfa bloblarını veri veya işletim sistemi diskler olarak 4 TB (4.095 GB) bağlı tooa VM büyük desteklemiyoruz.</span><span class="sxs-lookup"><span data-stu-id="b58fb-239">We don't support page blobs larger than 4 TB (4,095 GB) attached tooa VM as data or operating system disks.</span></span>

<span data-ttu-id="b58fb-240">**Toouse yeni bir sürüm gerekiyor mu Azure Araçları toocreate ekleme, yeniden boyutlandırma ve 1 TB'den büyük olan diskler karşıya?**</span><span class="sxs-lookup"><span data-stu-id="b58fb-240">**Do I need toouse a new version of Azure tools toocreate, attach, resize, and upload disks larger than 1 TB?**</span></span>

<span data-ttu-id="b58fb-241">Var olan Azure Araçları toocreate tooupgrade gerekmez, ekleme ya da 1 TB'den büyük diskleri yeniden boyutlandırma.</span><span class="sxs-lookup"><span data-stu-id="b58fb-241">You don't need tooupgrade your existing Azure tools toocreate, attach, or resize disks larger than 1 TB.</span></span> <span data-ttu-id="b58fb-242">VHD dosyası tooupload doğrudan tooAzure bir sayfa blobu veya yönetilmeyen disk olarak şirket içi, toouse hello en son aracı kümeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="b58fb-242">tooupload your VHD file from on-premises directly tooAzure as a page blob or unmanaged disk, you need toouse hello latest tool sets:</span></span>

|<span data-ttu-id="b58fb-243">Azure Araçları</span><span class="sxs-lookup"><span data-stu-id="b58fb-243">Azure tools</span></span>      | <span data-ttu-id="b58fb-244">Desteklenen sürümler</span><span class="sxs-lookup"><span data-stu-id="b58fb-244">Supported versions</span></span>                                |
|-----------------|---------------------------------------------------|
|<span data-ttu-id="b58fb-245">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b58fb-245">Azure PowerShell</span></span> | <span data-ttu-id="b58fb-246">Sürüm numarası 4.1.0'da: Haziran 2017 sürüm veya daha yenisi</span><span class="sxs-lookup"><span data-stu-id="b58fb-246">Version number 4.1.0: June 2017 release or later</span></span>|
|<span data-ttu-id="b58fb-247">Azure CLI v1</span><span class="sxs-lookup"><span data-stu-id="b58fb-247">Azure CLI v1</span></span>     | <span data-ttu-id="b58fb-248">Sürüm numarası 0.10.13: May 2017 sürüm veya daha yenisi</span><span class="sxs-lookup"><span data-stu-id="b58fb-248">Version number 0.10.13: May 2017 release or later</span></span>|
|<span data-ttu-id="b58fb-249">AzCopy</span><span class="sxs-lookup"><span data-stu-id="b58fb-249">AzCopy</span></span>           | <span data-ttu-id="b58fb-250">Sürüm numarası 6.1.0: Haziran 2017 sürüm veya daha yenisi</span><span class="sxs-lookup"><span data-stu-id="b58fb-250">Version number 6.1.0: June 2017 release or later</span></span>|

<span data-ttu-id="b58fb-251">Azure CLI v2 ve Azure Storage Gezgini Hello desteği yakında geliyor.</span><span class="sxs-lookup"><span data-stu-id="b58fb-251">hello support for Azure CLI v2 and Azure Storage Explorer is coming soon.</span></span> 

<span data-ttu-id="b58fb-252">**P4 ve P6 disk boyutları yönetilmeyen diskleri veya sayfa BLOB'ları için destekleniyor mu?**</span><span class="sxs-lookup"><span data-stu-id="b58fb-252">**Are P4 and P6 disk sizes supported for unmanaged disks or page blobs?**</span></span>

<span data-ttu-id="b58fb-253">Hayır.</span><span class="sxs-lookup"><span data-stu-id="b58fb-253">No.</span></span> <span data-ttu-id="b58fb-254">P4 (32 GB) ve P6 (64 GB) disk boyutları, yalnızca yönetilen diskler için desteklenir.</span><span class="sxs-lookup"><span data-stu-id="b58fb-254">P4 (32 GB) and P6 (64 GB) disk sizes are supported only for managed disks.</span></span> <span data-ttu-id="b58fb-255">Yönetilmeyen diskleri ve sayfa bloblarını desteği yakında geliyor.</span><span class="sxs-lookup"><span data-stu-id="b58fb-255">Support for unmanaged disks and page blobs is coming soon.</span></span>

<span data-ttu-id="b58fb-256">**Nasıl yönetilen my varolan premium hello küçük bir disk (15 Haziran 2017) etkinleştirilmeden önce 64 GB oluşturulduğu daha az disk varsa, onu faturalandırılır?**</span><span class="sxs-lookup"><span data-stu-id="b58fb-256">**If my existing premium managed disk less than 64 GB was created before hello small disk was enabled (around June 15, 2017), how is it billed?**</span></span>

<span data-ttu-id="b58fb-257">64 GB'den küçük var olan küçük premium disklerin faturalandırılır toobe according toohello P10 fiyatlandırma katmanı devam edin.</span><span class="sxs-lookup"><span data-stu-id="b58fb-257">Existing small premium disks less than 64 GB continue toobe billed according toohello P10 pricing tier.</span></span> 

<span data-ttu-id="b58fb-258">**Merhaba disk katmanını 64 GB'den küçük küçük premium diskleri P10 tooP4 veya P6 nasıl geçiş yapabilirim?**</span><span class="sxs-lookup"><span data-stu-id="b58fb-258">**How can I switch hello disk tier of small premium disks less than 64 GB from P10 tooP4 or P6?**</span></span>

<span data-ttu-id="b58fb-259">Küçük disklerinizi bir anlık görüntüsünü ve fiyatlandırma katmanı tooP4 disk tooautomatically anahtar hello oluşturmak veya P6 sağlanan hello boyutuna göre.</span><span class="sxs-lookup"><span data-stu-id="b58fb-259">You can take a snapshot of your small disks and then create a disk tooautomatically switch hello pricing tier tooP4 or P6 based on hello provisioned size.</span></span> 


## <a name="what-if-my-question-isnt-answered-here"></a><span data-ttu-id="b58fb-260">Ne sorumun cevabı burada cevaplanıp değil mi?</span><span class="sxs-lookup"><span data-stu-id="b58fb-260">What if my question isn't answered here?</span></span>

<span data-ttu-id="b58fb-261">Sorunuzun yanıtını burada listelenmiyorsa, bize bildirin ve yanıt bulmanıza yardımcı olacağız.</span><span class="sxs-lookup"><span data-stu-id="b58fb-261">If your question isn't listed here, let us know and we'll help you find an answer.</span></span> <span data-ttu-id="b58fb-262">Bu makalenin hello sonunda bir soru hello açıklamaları nakledebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b58fb-262">You can post a question at hello end of this article in hello comments.</span></span> <span data-ttu-id="b58fb-263">hello Azure depolama ekibi ile tooengage ve diğer topluluk üyeleri bu makale hakkında kullanmak hello MSDN [Azure depolama Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata).</span><span class="sxs-lookup"><span data-stu-id="b58fb-263">tooengage with hello Azure Storage team and other community members about this article, use hello MSDN [Azure Storage forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata).</span></span>

<span data-ttu-id="b58fb-264">toorequest özellikleri gönderme istekleri ve fikir toohello [Azure Storage geri bildirim Forumunda](https://feedback.azure.com/forums/217298-storage).</span><span class="sxs-lookup"><span data-stu-id="b58fb-264">toorequest features, submit your requests and ideas toohello [Azure Storage feedback forum](https://feedback.azure.com/forums/217298-storage).</span></span>
