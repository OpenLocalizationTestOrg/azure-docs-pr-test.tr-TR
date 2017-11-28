
* [<span data-ttu-id="e56a4-101">Azure’da hızlı bir şekilde sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="e56a4-101">Quick-create a virtual machine in Azure</span></span>](#quick-create-a-vm-in-azure)
* [<span data-ttu-id="e56a4-102">Azure’da bir sanal makineyi şablondan dağıtma</span><span class="sxs-lookup"><span data-stu-id="e56a4-102">Deploy a virtual machine in Azure from a template</span></span>](#deploy-a-vm-in-azure-from-a-template)
* [<span data-ttu-id="e56a4-103">Özel bir görüntüden sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="e56a4-103">Create a virtual machine from a custom image</span></span>](#create-a-custom-vm-image)
* [<span data-ttu-id="e56a4-104">Sanal ağ ve yük dengeleyicisi kullanan bir sanal makine dağıtma</span><span class="sxs-lookup"><span data-stu-id="e56a4-104">Deploy a virtual machine that uses a virtual network and a load balancer</span></span>](#deploy-a-multi-vm-application-that-uses-a-virtual-network-and-an-external-load-balancer)
* [<span data-ttu-id="e56a4-105">Kaynak grubunu kaldırma</span><span class="sxs-lookup"><span data-stu-id="e56a4-105">Remove a resource group</span></span>](#remove-a-resource-group)
* [<span data-ttu-id="e56a4-106">Bir kaynak grubu dağıtımının günlüğünü görüntüleme</span><span class="sxs-lookup"><span data-stu-id="e56a4-106">Show the log for a resource group deployment</span></span>](#show-the-log-for-a-resource-group-deployment)
* [<span data-ttu-id="e56a4-107">Bir sanal makine hakkında bilgi görüntüleme</span><span class="sxs-lookup"><span data-stu-id="e56a4-107">Display information about a virtual machine</span></span>](#display-information-about-a-virtual-machine)
* [<span data-ttu-id="e56a4-108">Linux tabanlı sanal makineye bağlanma</span><span class="sxs-lookup"><span data-stu-id="e56a4-108">Connect to a Linux-based virtual machine</span></span>](#log-on-to-a-linux-based-virtual-machine)
* [<span data-ttu-id="e56a4-109">Sanal makineyi durdurma</span><span class="sxs-lookup"><span data-stu-id="e56a4-109">Stop a virtual machine</span></span>](#stop-a-virtual-machine)
* [<span data-ttu-id="e56a4-110">Sanal makineyi başlatma</span><span class="sxs-lookup"><span data-stu-id="e56a4-110">Start a virtual machine</span></span>](#start-a-virtual-machine)
* [<span data-ttu-id="e56a4-111">Veri diski ekleme</span><span class="sxs-lookup"><span data-stu-id="e56a4-111">Attach a data disk</span></span>](#attach-a-data-disk)

## <a name="getting-ready"></a><span data-ttu-id="e56a4-112">Hazırlanma</span><span class="sxs-lookup"><span data-stu-id="e56a4-112">Getting ready</span></span>
<span data-ttu-id="e56a4-113">Azure CLI’yi Azure kaynak gruplarıyla kullanabilmeniz için doğru Azure CLI sürümüne ve bir Azure hesabına sahip olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e56a4-113">Before you can use the Azure CLI with Azure resource groups, you need to have the right Azure CLI version and an Azure account.</span></span> <span data-ttu-id="e56a4-114">Azure CLI yoksa [yükleyin](../articles/cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="e56a4-114">If you don't have the Azure CLI, [install it](../articles/cli-install-nodejs.md).</span></span>

### <a name="update-your-azure-cli-version-to-090-or-later"></a><span data-ttu-id="e56a4-115">Azure CLI sürümünüzü 0.9.0 veya sonraki bir sürüme güncelleştirin</span><span class="sxs-lookup"><span data-stu-id="e56a4-115">Update your Azure CLI version to 0.9.0 or later</span></span>
<span data-ttu-id="e56a4-116">0.9.0 veya sonraki sürümün yüklü olup olmadığını görmek için `azure --version` yazın.</span><span class="sxs-lookup"><span data-stu-id="e56a4-116">Type `azure --version` to see whether you have already installed version 0.9.0 or later.</span></span>

```azurecli
azure --version
0.9.0 (node: 0.10.25)
```

<span data-ttu-id="e56a4-117">Sürümünüz 0.9.0 veya üzeri değilse, yerel yükleyicilerden biriyle ya da `npm update -g azure-cli` yazarak **npm** aracılığıyla güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e56a4-117">If your version is not 0.9.0 or later, you need to update it by using one of the native installers or through **npm** by typing `npm update -g azure-cli`.</span></span>

<span data-ttu-id="e56a4-118">Aşağıdaki [Docker görüntüsünü](https://registry.hub.docker.com/u/microsoft/azure-cli/) kullanarak Azure CLI’yi bir Docker kapsayıcısı olarak da çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e56a4-118">You can also run Azure CLI as a Docker container by using the following [Docker image](https://registry.hub.docker.com/u/microsoft/azure-cli/).</span></span> <span data-ttu-id="e56a4-119">Docker ana bilgisayarından aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="e56a4-119">From a Docker host, run the following command:</span></span>

```bash
docker run -it microsoft/azure-cli
```

### <a name="set-your-azure-account-and-subscription"></a><span data-ttu-id="e56a4-120">Azure hesabınızı ve aboneliğinizi ayarlama</span><span class="sxs-lookup"><span data-stu-id="e56a4-120">Set your Azure account and subscription</span></span>
<span data-ttu-id="e56a4-121">Henüz bir Azure aboneliğiniz olmamasına rağmen bir MSDN aboneliğiniz varsa [MSDN abone avantajlarınızı](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e56a4-121">If you don't already have an Azure subscription but you do have an MSDN subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span> <span data-ttu-id="e56a4-122">Veya [ücretsiz deneme sürümü](https://azure.microsoft.com/pricing/free-trial/) için kaydolabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e56a4-122">Or you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

<span data-ttu-id="e56a4-123">`azure login` yazarak ve Azure hesabınızda etkileşimli oturum açma deneyimine yönelik istemleri izleyerek [Azure hesabınızda etkileşimli bir oturum açın](../articles/xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login).</span><span class="sxs-lookup"><span data-stu-id="e56a4-123">Now [log in to your Azure account interactively](../articles/xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login) by typing `azure login` and following the prompts for an interactive login experience to your Azure account.</span></span> 

> [!NOTE]
> <span data-ttu-id="e56a4-124">İş veya okul kimliğiniz varsa ve iki faktörlü kimlik doğrulamasının etkin olmadığını biliyorsanız, iş veya okul kimlik numaranıza **ek olarak** `azure login -u` kullanabilir ve etkileşimli bir oturum *olmadan* oturum açabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e56a4-124">If you have a work or school ID and you know you do not have two-factor authentication enabled, you can **also** use `azure login -u` along with the work or school ID to log in *without* an interactive session.</span></span> <span data-ttu-id="e56a4-125">İş veya okul kimliğiniz yoksa, aynı şekilde oturum açmak için [kişisel Microsoft hesabınızdan iş veya okul kimliği oluşturabilirsiniz](../articles/virtual-machines/windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e56a4-125">If you don't have a work or school ID, you can [create a work or school id from your personal Microsoft account](../articles/virtual-machines/windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) to log in the same way.</span></span>
>
>

<span data-ttu-id="e56a4-126">Hesabınızın birden fazla aboneliği olabilir.</span><span class="sxs-lookup"><span data-stu-id="e56a4-126">Your account may have more than one subscription.</span></span> <span data-ttu-id="e56a4-127">`azure account list` yazarak aboneliklerinizin aşağıdakine benzer bir listesini görüntüleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e56a4-127">You can list your subscriptions by typing `azure account list`, which might look something like this:</span></span>

```azurecli
azure account list
info:    Executing command account list
data:    Name                              Id                                    Tenant Id                            Current
data:    --------------------------------  ------------------------------------  ------------------------------------  -------
data:    Contoso Admin                     xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  true
data:    Fabrikam dev                      xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  false  
data:    Fabrikam test                     xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  false  
data:    Contoso production                xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  false  
```

<span data-ttu-id="e56a4-128">Aşağıdaki komutu yazarak geçerli Azure aboneliğinizi ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e56a4-128">You can set the current Azure subscription by typing the following.</span></span> <span data-ttu-id="e56a4-129">Yönetmek istediğiniz kaynaklara sahip abonelik adını veya kimliği kullanın.</span><span class="sxs-lookup"><span data-stu-id="e56a4-129">Use the subscription name or the ID that has the resources you want to manage.</span></span>

```azurecli
azure account set <subscription name or ID> true
```

### <a name="switch-to-the-azure-cli-resource-group-mode"></a><span data-ttu-id="e56a4-130">Azure CLI kaynak grubu moduna geçme</span><span class="sxs-lookup"><span data-stu-id="e56a4-130">Switch to the Azure CLI resource group mode</span></span>
<span data-ttu-id="e56a4-131">Varsayılan olarak, Azure CLI hizmet yönetimi modunda başlatılır (**asm** modu).</span><span class="sxs-lookup"><span data-stu-id="e56a4-131">By default, the Azure CLI starts in the service management mode (**asm** mode).</span></span> <span data-ttu-id="e56a4-132">Kaynak grubu moduna geçmek için aşağıdaki komutu yazın.</span><span class="sxs-lookup"><span data-stu-id="e56a4-132">Type the following to switch to resource group mode.</span></span>

```azurecli
azure config mode arm
```

## <a name="understanding-azure-resource-templates-and-resource-groups"></a><span data-ttu-id="e56a4-133">Azure kaynak şablonlarını ve kaynak gruplarını anlama</span><span class="sxs-lookup"><span data-stu-id="e56a4-133">Understanding Azure resource templates and resource groups</span></span>
<span data-ttu-id="e56a4-134">Çoğu uygulama farklı kaynak türlerinin bir birleşiminden oluşturulur (bir veya daha fazla VM ve depolama hesabı, bir SQL veritabanı, bir sanal ağ ya da içerik teslim ağı gibi).</span><span class="sxs-lookup"><span data-stu-id="e56a4-134">Most applications are built from a combination of different resource types (such as one or more VMs and storage accounts, a SQL database, a virtual network, or a content delivery network).</span></span> <span data-ttu-id="e56a4-135">Varsayılan Azure hizmet yönetim API’si ve klasik Azure portalı, hizmete göre yaklaşım kullanarak bu öğeleri temsil eder.</span><span class="sxs-lookup"><span data-stu-id="e56a4-135">The default Azure service management API and the Azure classic portal represented these items by using a service-by-service approach.</span></span> <span data-ttu-id="e56a4-136">Bu yaklaşım, belirli hizmetleri tek bir dağıtım mantıksal birim olarak değil ayrı ayrı dağıtıp yönetmenizi (veya bunu yapan başka araçlar bulmanızı) gerektirir.</span><span class="sxs-lookup"><span data-stu-id="e56a4-136">This approach requires you to deploy and manage the individual services individually (or find other tools that do so), and not as a single logical unit of deployment.</span></span>

<span data-ttu-id="e56a4-137">Ancak *Azure Resource Manager şablonları*, bu farklı kaynakları bildirim temelli olarak tek bir mantıksal dağıtım birimi halinde dağıtıp yönetmenizi mümkün hale getirir.</span><span class="sxs-lookup"><span data-stu-id="e56a4-137">*Azure Resource Manager templates*, however, make it possible for you to deploy and manage these different resources as one logical deployment unit in a declarative fashion.</span></span> <span data-ttu-id="e56a4-138">Her komuttan sonra Azure’a neyi dağıtacağını zorunlu olarak belirtmek yerine, tüm dağıtımınızı (tüm kaynaklar ve ilişkili yapılandırma ile dağıtım parametreleri) bir JSON dosyasında açıklar ve Azure’a bu kaynakları tek grup haline dağıtmasını söylersiniz.</span><span class="sxs-lookup"><span data-stu-id="e56a4-138">Instead of imperatively telling Azure what to deploy one command after another, you describe your entire deployment in a JSON file -- all of the resources and associated configuration and deployment parameters -- and tell Azure to deploy those resources as one group.</span></span>

<span data-ttu-id="e56a4-139">Bundan sonra Azure CLI kaynak yönetimi komutlarını kullanarak grup kaynaklarının genel yaşam döngüsünü aşağıdaki işlemlerle yönetebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e56a4-139">You can then manage the overall life cycle of the group's resources by using Azure CLI resource management commands to:</span></span>

* <span data-ttu-id="e56a4-140">Gruptaki tüm kaynakları tek seferde durdurma, başlatma veya silme.</span><span class="sxs-lookup"><span data-stu-id="e56a4-140">Stop, start, or delete all of the resources within the group at once.</span></span>
* <span data-ttu-id="e56a4-141">Kaynaklar üzerindeki izinleri kilitlemek için Rol Tabanlı Access Control (RBAC) kuralları uygulama.</span><span class="sxs-lookup"><span data-stu-id="e56a4-141">Apply Role-Based Access Control (RBAC) rules to lock down security permissions on them.</span></span>
* <span data-ttu-id="e56a4-142">İşlemleri denetleme.</span><span class="sxs-lookup"><span data-stu-id="e56a4-142">Audit operations.</span></span>
* <span data-ttu-id="e56a4-143">Daha iyi izleme için ek meta verilerle kaynakları etiketleme.</span><span class="sxs-lookup"><span data-stu-id="e56a4-143">Tag resources with additional metadata for better tracking.</span></span>

<span data-ttu-id="e56a4-144">Azure kaynak grupları ve size sunabilecekleri hakkında daha fazla bilgiyi [Azure Resource Manager’a genel bakış](../articles/azure-resource-manager/resource-group-overview.md) bölümünde bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e56a4-144">You can learn lots more about Azure resource groups and what they can do for you in the [Azure Resource Manager overview](../articles/azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="e56a4-145">Şablon yazmak istiyorsanız bkz. [Azure Resource Manager şablonları yazma](../articles/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="e56a4-145">If you're interested in authoring templates, see [Authoring Azure Resource Manager templates](../articles/resource-group-authoring-templates.md).</span></span>

## <span data-ttu-id="e56a4-146"><a id="quick-create-a-vm-in-azure"></a>Görev: Azure’da hızlı bir şekilde VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="e56a4-146"><a id="quick-create-a-vm-in-azure"></a>Task: Quick-create a VM in Azure</span></span>
<span data-ttu-id="e56a4-147">Bazı durumlarda gerekli olan görüntüyü bilirsiniz ve bu görüntüden hemen bir VM oluşturmanız gerekirken altyapıyı fazla önemsemezsiniz; belki de temiz bir VM üzerinde bir test yapmanız gerekiyordur.</span><span class="sxs-lookup"><span data-stu-id="e56a4-147">Sometimes you know what image you need, and you need a VM from that image right now and you don't care too much about the infrastructure -- maybe you have to test something on a clean VM.</span></span> <span data-ttu-id="e56a4-148">Bu durumda `azure vm quick-create` komutunu kullanmanız ve bir VM ile altyapısını oluşturmak için gerekli bağımsız değişkenleri geçirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e56a4-148">That's when you want to use the `azure vm quick-create` command, and pass the arguments necessary to create a VM and its infrastructure.</span></span>

<span data-ttu-id="e56a4-149">İlk olarak kaynak grubunuzu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e56a4-149">First, create your resource group.</span></span>

```azurecli
azure group create coreos-quick westus
info:    Executing command group create
+ Getting resource group coreos-quick
+ Creating resource group coreos-quick
info:    Created resource group coreos-quick
data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/coreos-quick
data:    Name:                coreos-quick
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags:
data:
info:    group create command OK
```

<span data-ttu-id="e56a4-150">İkinci olarak, bir görüntü gereklidir.</span><span class="sxs-lookup"><span data-stu-id="e56a4-150">Second, you'll need an image.</span></span> <span data-ttu-id="e56a4-151">Azure CLI ile bir görüntü bulmak için bkz. [PowerShell ve Azure CLI ile Azure sanal makine görüntülerine gitme ve görüntüyü seçme](../articles/virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e56a4-151">To find an image with the Azure CLI, see [Navigating and selecting Azure virtual machine images with PowerShell and the Azure CLI](../articles/virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="e56a4-152">Ancak bu makalede popüler görüntülerin kısa bir listesi verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="e56a4-152">But for this article, here's a short list of popular images.</span></span> <span data-ttu-id="e56a4-153">Bu hızlı oluşturma işlemi için CoreOS Kararlı görüntüsü kullanılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="e56a4-153">We'll use CoreOS's Stable image for this quick-create.</span></span>

> [!NOTE]
> <span data-ttu-id="e56a4-154">ComputeImageVersion için ayrıca hem şablon dilinde hem de Azure CLI’da yalnızca 'latest' parametresini belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e56a4-154">For ComputeImageVersion, you can also simply supply 'latest' as the parameter in both the template language and in the Azure CLI.</span></span> <span data-ttu-id="e56a4-155">Bunun yapılması, betikleri veya şablonları değiştirmek zorunda olmadan görüntünün her zaman en son ve düzeltme eki uygulanmış sürümünü kullanmanıza olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="e56a4-155">This will allow you to always use the latest and patched version of the image without having to modify your scripts or templates.</span></span> <span data-ttu-id="e56a4-156">Bu örnek aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="e56a4-156">This is shown below.</span></span>
>
>

| <span data-ttu-id="e56a4-157">PublisherName</span><span class="sxs-lookup"><span data-stu-id="e56a4-157">PublisherName</span></span> | <span data-ttu-id="e56a4-158">Sunduğu</span><span class="sxs-lookup"><span data-stu-id="e56a4-158">Offer</span></span> | <span data-ttu-id="e56a4-159">Sku</span><span class="sxs-lookup"><span data-stu-id="e56a4-159">Sku</span></span> | <span data-ttu-id="e56a4-160">Sürüm</span><span class="sxs-lookup"><span data-stu-id="e56a4-160">Version</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="e56a4-161">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="e56a4-161">OpenLogic</span></span> |<span data-ttu-id="e56a4-162">CentOS</span><span class="sxs-lookup"><span data-stu-id="e56a4-162">CentOS</span></span> |<span data-ttu-id="e56a4-163">7</span><span class="sxs-lookup"><span data-stu-id="e56a4-163">7</span></span> |<span data-ttu-id="e56a4-164">7.0.201503</span><span class="sxs-lookup"><span data-stu-id="e56a4-164">7.0.201503</span></span> |
| <span data-ttu-id="e56a4-165">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="e56a4-165">OpenLogic</span></span> |<span data-ttu-id="e56a4-166">CentOS</span><span class="sxs-lookup"><span data-stu-id="e56a4-166">CentOS</span></span> |<span data-ttu-id="e56a4-167">7.1</span><span class="sxs-lookup"><span data-stu-id="e56a4-167">7.1</span></span> |<span data-ttu-id="e56a4-168">7.1.201504</span><span class="sxs-lookup"><span data-stu-id="e56a4-168">7.1.201504</span></span> |
| <span data-ttu-id="e56a4-169">CoreOS</span><span class="sxs-lookup"><span data-stu-id="e56a4-169">CoreOS</span></span> |<span data-ttu-id="e56a4-170">CoreOS</span><span class="sxs-lookup"><span data-stu-id="e56a4-170">CoreOS</span></span> |<span data-ttu-id="e56a4-171">Beta</span><span class="sxs-lookup"><span data-stu-id="e56a4-171">Beta</span></span> |<span data-ttu-id="e56a4-172">647.0.0</span><span class="sxs-lookup"><span data-stu-id="e56a4-172">647.0.0</span></span> |
| <span data-ttu-id="e56a4-173">CoreOS</span><span class="sxs-lookup"><span data-stu-id="e56a4-173">CoreOS</span></span> |<span data-ttu-id="e56a4-174">CoreOS</span><span class="sxs-lookup"><span data-stu-id="e56a4-174">CoreOS</span></span> |<span data-ttu-id="e56a4-175">Dengeli</span><span class="sxs-lookup"><span data-stu-id="e56a4-175">Stable</span></span> |<span data-ttu-id="e56a4-176">633.1.0</span><span class="sxs-lookup"><span data-stu-id="e56a4-176">633.1.0</span></span> |
| <span data-ttu-id="e56a4-177">MicrosoftDynamicsNAV</span><span class="sxs-lookup"><span data-stu-id="e56a4-177">MicrosoftDynamicsNAV</span></span> |<span data-ttu-id="e56a4-178">DynamicsNAV</span><span class="sxs-lookup"><span data-stu-id="e56a4-178">DynamicsNAV</span></span> |<span data-ttu-id="e56a4-179">2015</span><span class="sxs-lookup"><span data-stu-id="e56a4-179">2015</span></span> |<span data-ttu-id="e56a4-180">8.0.40459</span><span class="sxs-lookup"><span data-stu-id="e56a4-180">8.0.40459</span></span> |
| <span data-ttu-id="e56a4-181">MicrosoftSharePoint</span><span class="sxs-lookup"><span data-stu-id="e56a4-181">MicrosoftSharePoint</span></span> |<span data-ttu-id="e56a4-182">MicrosoftSharePointServer</span><span class="sxs-lookup"><span data-stu-id="e56a4-182">MicrosoftSharePointServer</span></span> |<span data-ttu-id="e56a4-183">2013</span><span class="sxs-lookup"><span data-stu-id="e56a4-183">2013</span></span> |<span data-ttu-id="e56a4-184">1.0.0</span><span class="sxs-lookup"><span data-stu-id="e56a4-184">1.0.0</span></span> |
| <span data-ttu-id="e56a4-185">msopentech</span><span class="sxs-lookup"><span data-stu-id="e56a4-185">msopentech</span></span> |<span data-ttu-id="e56a4-186">Oracle-Database-12c-Weblogic-Server-12c</span><span class="sxs-lookup"><span data-stu-id="e56a4-186">Oracle-Database-12c-Weblogic-Server-12c</span></span> |<span data-ttu-id="e56a4-187">Standart</span><span class="sxs-lookup"><span data-stu-id="e56a4-187">Standard</span></span> |<span data-ttu-id="e56a4-188">1.0.0</span><span class="sxs-lookup"><span data-stu-id="e56a4-188">1.0.0</span></span> |
| <span data-ttu-id="e56a4-189">msopentech</span><span class="sxs-lookup"><span data-stu-id="e56a4-189">msopentech</span></span> |<span data-ttu-id="e56a4-190">Oracle-Database-12c-Weblogic-Server-12c</span><span class="sxs-lookup"><span data-stu-id="e56a4-190">Oracle-Database-12c-Weblogic-Server-12c</span></span> |<span data-ttu-id="e56a4-191">Enterprise</span><span class="sxs-lookup"><span data-stu-id="e56a4-191">Enterprise</span></span> |<span data-ttu-id="e56a4-192">1.0.0</span><span class="sxs-lookup"><span data-stu-id="e56a4-192">1.0.0</span></span> |
| <span data-ttu-id="e56a4-193">MicrosoftSQLServer</span><span class="sxs-lookup"><span data-stu-id="e56a4-193">MicrosoftSQLServer</span></span> |<span data-ttu-id="e56a4-194">SQL2014-WS2012R2</span><span class="sxs-lookup"><span data-stu-id="e56a4-194">SQL2014-WS2012R2</span></span> |<span data-ttu-id="e56a4-195">Enterprise-Optimized-for-DW</span><span class="sxs-lookup"><span data-stu-id="e56a4-195">Enterprise-Optimized-for-DW</span></span> |<span data-ttu-id="e56a4-196">12.0.2430</span><span class="sxs-lookup"><span data-stu-id="e56a4-196">12.0.2430</span></span> |
| <span data-ttu-id="e56a4-197">MicrosoftSQLServer</span><span class="sxs-lookup"><span data-stu-id="e56a4-197">MicrosoftSQLServer</span></span> |<span data-ttu-id="e56a4-198">SQL2014-WS2012R2</span><span class="sxs-lookup"><span data-stu-id="e56a4-198">SQL2014-WS2012R2</span></span> |<span data-ttu-id="e56a4-199">Enterprise-Optimized-for-OLTP</span><span class="sxs-lookup"><span data-stu-id="e56a4-199">Enterprise-Optimized-for-OLTP</span></span> |<span data-ttu-id="e56a4-200">12.0.2430</span><span class="sxs-lookup"><span data-stu-id="e56a4-200">12.0.2430</span></span> |
| <span data-ttu-id="e56a4-201">Canonical</span><span class="sxs-lookup"><span data-stu-id="e56a4-201">Canonical</span></span> |<span data-ttu-id="e56a4-202">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="e56a4-202">UbuntuServer</span></span> |<span data-ttu-id="e56a4-203">12.04.5-LTS</span><span class="sxs-lookup"><span data-stu-id="e56a4-203">12.04.5-LTS</span></span> |<span data-ttu-id="e56a4-204">12.04.201504230</span><span class="sxs-lookup"><span data-stu-id="e56a4-204">12.04.201504230</span></span> |
| <span data-ttu-id="e56a4-205">Canonical</span><span class="sxs-lookup"><span data-stu-id="e56a4-205">Canonical</span></span> |<span data-ttu-id="e56a4-206">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="e56a4-206">UbuntuServer</span></span> |<span data-ttu-id="e56a4-207">14.04.2-LTS</span><span class="sxs-lookup"><span data-stu-id="e56a4-207">14.04.2-LTS</span></span> |<span data-ttu-id="e56a4-208">14.04.201503090</span><span class="sxs-lookup"><span data-stu-id="e56a4-208">14.04.201503090</span></span> |
| <span data-ttu-id="e56a4-209">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="e56a4-209">MicrosoftWindowsServer</span></span> |<span data-ttu-id="e56a4-210">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="e56a4-210">WindowsServer</span></span> |<span data-ttu-id="e56a4-211">2012-Datacenter</span><span class="sxs-lookup"><span data-stu-id="e56a4-211">2012-Datacenter</span></span> |<span data-ttu-id="e56a4-212">3.0.201503</span><span class="sxs-lookup"><span data-stu-id="e56a4-212">3.0.201503</span></span> |
| <span data-ttu-id="e56a4-213">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="e56a4-213">MicrosoftWindowsServer</span></span> |<span data-ttu-id="e56a4-214">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="e56a4-214">WindowsServer</span></span> |<span data-ttu-id="e56a4-215">2012-R2-Datacenter</span><span class="sxs-lookup"><span data-stu-id="e56a4-215">2012-R2-Datacenter</span></span> |<span data-ttu-id="e56a4-216">4.0.201503</span><span class="sxs-lookup"><span data-stu-id="e56a4-216">4.0.201503</span></span> |
| <span data-ttu-id="e56a4-217">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="e56a4-217">MicrosoftWindowsServer</span></span> |<span data-ttu-id="e56a4-218">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="e56a4-218">WindowsServer</span></span> |<span data-ttu-id="e56a4-219">Windows-Server-Technical-Preview</span><span class="sxs-lookup"><span data-stu-id="e56a4-219">Windows-Server-Technical-Preview</span></span> |<span data-ttu-id="e56a4-220">5.0.201504</span><span class="sxs-lookup"><span data-stu-id="e56a4-220">5.0.201504</span></span> |
| <span data-ttu-id="e56a4-221">MicrosoftWindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="e56a4-221">MicrosoftWindowsServerEssentials</span></span> |<span data-ttu-id="e56a4-222">WindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="e56a4-222">WindowsServerEssentials</span></span> |<span data-ttu-id="e56a4-223">WindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="e56a4-223">WindowsServerEssentials</span></span> |<span data-ttu-id="e56a4-224">1.0.141204</span><span class="sxs-lookup"><span data-stu-id="e56a4-224">1.0.141204</span></span> |
| <span data-ttu-id="e56a4-225">MicrosoftWindowsServerHPCPack</span><span class="sxs-lookup"><span data-stu-id="e56a4-225">MicrosoftWindowsServerHPCPack</span></span> |<span data-ttu-id="e56a4-226">WindowsServerHPCPack</span><span class="sxs-lookup"><span data-stu-id="e56a4-226">WindowsServerHPCPack</span></span> |<span data-ttu-id="e56a4-227">2012R2</span><span class="sxs-lookup"><span data-stu-id="e56a4-227">2012R2</span></span> |<span data-ttu-id="e56a4-228">4.3.4665</span><span class="sxs-lookup"><span data-stu-id="e56a4-228">4.3.4665</span></span> |

<span data-ttu-id="e56a4-229">Yalnızca `azure vm quick-create` komutunu girip istemlere hazır olarak VM’nizi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e56a4-229">Just create your VM by entering the `azure vm quick-create` command and being ready for the prompts.</span></span> <span data-ttu-id="e56a4-230">Şuna benzer şekilde görünecektir:</span><span class="sxs-lookup"><span data-stu-id="e56a4-230">It should look something like this:</span></span>

```azurecli
azure vm quick-create
info:    Executing command vm quick-create
Resource group name: coreos-quick
Virtual machine name: coreos
Location name: westus
Operating system Type [Windows, Linux]: linux
ImageURN (format: "publisherName:offer:skus:version"): coreos:coreos:stable:latest
User name: ops
Password: *********
Confirm password: *********
+ Looking up the VM "coreos"
info:    Using the VM Size "Standard_A1"
info:    The [OS, Data] Disk or image configuration requires storage account
+ Retrieving storage accounts
info:    Could not find any storage accounts in the region "westus", trying to create new one
+ Creating storage account "cli9fd3fce49e9a9b3d14302" in "westus"
+ Looking up the storage account cli9fd3fce49e9a9b3d14302
+ Looking up the NIC "coreo-westu-1430261891570-nic"
info:    An nic with given name "coreo-westu-1430261891570-nic" not found, creating a new one
+ Looking up the virtual network "coreo-westu-1430261891570-vnet"
info:    Preparing to create new virtual network and subnet
/ Creating a new virtual network "coreo-westu-1430261891570-vnet" [address prefix: "10.0.0.0/16"] with subnet "coreo-westu-1430261891570-sne+" [address prefix: "10.0.1.0/24"]
+ Looking up the virtual network "coreo-westu-1430261891570-vnet"
+ Looking up the subnet "coreo-westu-1430261891570-snet" under the virtual network "coreo-westu-1430261891570-vnet"
info:    Found public ip parameters, trying to setup PublicIP profile
+ Looking up the public ip "coreo-westu-1430261891570-pip"
info:    PublicIP with given name "coreo-westu-1430261891570-pip" not found, creating a new one
+ Creating public ip "coreo-westu-1430261891570-pip"
+ Looking up the public ip "coreo-westu-1430261891570-pip"
+ Creating NIC "coreo-westu-1430261891570-nic"
+ Looking up the NIC "coreo-westu-1430261891570-nic"
+ Creating VM "coreos"
+ Looking up the VM "coreos"
+ Looking up the NIC "coreo-westu-1430261891570-nic"
+ Looking up the public ip "coreo-westu-1430261891570-pip"
data:    Id                              :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/coreos-quick/providers/Microsoft.Compute/virtualMachines/coreos
data:    ProvisioningState               :Succeeded
data:    Name                            :coreos
data:    Location                        :westus
data:    FQDN                            :coreo-westu-1430261891570-pip.westus.cloudapp.azure.com
data:    Type                            :Microsoft.Compute/virtualMachines
data:
data:    Hardware Profile:
data:      Size                          :Standard_A1
data:
data:    Storage Profile:
data:      Image reference:
data:        Publisher                   :coreos
data:        Offer                       :coreos
data:        Sku                         :stable
data:        Version                     :633.1.0
data:
data:      OS Disk:
data:        OSType                      :Linux
data:        Name                        :cli9fd3fce49e9a9b3d-os-1430261892283
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :https://cli9fd3fce49e9a9b3d14302.blob.core.windows.net/vhds/cli9fd3fce49e9a9b3d-os-1430261892283.vhd
data:
data:    OS Profile:
data:      Computer Name                 :coreos
data:      User Name                     :ops
data:      Linux Configuration:
data:        Disable Password Auth       :false
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Id                        :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/coreos-quick/providers/Microsoft.Network/networkInterfaces/coreo-westu-1430261891570-nic
data:          Primary                   :true
data:          MAC Address               :00-0D-3A-30-72-E3
data:          Provisioning State        :Succeeded
data:          Name                      :coreo-westu-1430261891570-nic
data:          Location                  :westus
data:            Private IP alloc-method :Dynamic
data:            Private IP address      :10.0.1.4
data:            Public IP address       :104.40.24.124
data:            FQDN                    :coreo-westu-1430261891570-pip.westus.cloudapp.azure.com
info:    vm quick-create command OK
```

<span data-ttu-id="e56a4-231">Yeni VM’niz hazırdır.</span><span class="sxs-lookup"><span data-stu-id="e56a4-231">And away you go with your new VM.</span></span>

## <span data-ttu-id="e56a4-232"><a id="deploy-a-vm-in-azure-from-a-template"></a>Görev: Azure’da şablondan VM dağıtma</span><span class="sxs-lookup"><span data-stu-id="e56a4-232"><a id="deploy-a-vm-in-azure-from-a-template"></a>Task: Deploy a VM in Azure from a template</span></span>
<span data-ttu-id="e56a4-233">Azure CLI ile bir şablon kullanarak yeni bir Azure VM dağıtmak için bu bölümlerdeki yönergeleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="e56a4-233">Use the instructions in these sections to deploy a new Azure VM by using a template with the Azure CLI.</span></span> <span data-ttu-id="e56a4-234">Bu şablon tek bir alt ağa sahip yeni bir sanal ağda tek bir sanal makine oluşturur ve `azure vm quick-create` seçeneğinin aksine, tam olarak ne istediğinizi açıklamanıza ve hata olmadan tekrarlamanıza olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="e56a4-234">This template creates a single virtual machine in a new virtual network with a single subnet, and unlike `azure vm quick-create`, enables you to describe what you want precisely and repeat it without errors.</span></span> <span data-ttu-id="e56a4-235">Bu şablon aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="e56a4-235">Here's what this template creates:</span></span>

![](./media/virtual-machines-common-cli-deploy-templates/new-vm.png)

### <a name="step-1-examine-the-json-file-for-the-template-parameters"></a><span data-ttu-id="e56a4-236">Adım 1: Şablon parametreleri için JSON dosyasını inceleme</span><span class="sxs-lookup"><span data-stu-id="e56a4-236">Step 1: Examine the JSON file for the template parameters</span></span>
<span data-ttu-id="e56a4-237">Şablon için JSON dosyasının içeriği aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="e56a4-237">Here are the contents of the JSON file for the template.</span></span> <span data-ttu-id="e56a4-238">(Şablon [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-linux/azuredeploy.json) içinde de bulunur.)</span><span class="sxs-lookup"><span data-stu-id="e56a4-238">(The template is also located in [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-linux/azuredeploy.json).)</span></span>

<span data-ttu-id="e56a4-239">Şablonlar esnektir, bu nedenle tasarımcı size çok sayıda parametre sunmayı veya daha sabit bir şablon oluşturarak az sayıda parametre sunmayı seçmiş olabilir.</span><span class="sxs-lookup"><span data-stu-id="e56a4-239">Templates are flexible, so the designer may have chosen to give you lots of parameters or chosen to offer only a few by creating a template that is more fixed.</span></span> <span data-ttu-id="e56a4-240">Bilgileri toplamak için şablonu parametre olarak geçirmeniz, şablon dosyasını açmanız (bu konunun sonraki kısımlarında bir şablon satır içi mevcuttur) ve **parameters** değerlerini incelemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e56a4-240">In order to collect the information you need to pass the template as parameters, open the template file (this topic has a template inline, below) and examine the **parameters** values.</span></span>

<span data-ttu-id="e56a4-241">Bu durumda aşağıdaki şablon şunları ister:</span><span class="sxs-lookup"><span data-stu-id="e56a4-241">In this case, the template below will ask for:</span></span>

* <span data-ttu-id="e56a4-242">Benzersiz bir depolama hesabı adı.</span><span class="sxs-lookup"><span data-stu-id="e56a4-242">A unique storage account name.</span></span>
* <span data-ttu-id="e56a4-243">VM için bir yönetici kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="e56a4-243">An admin user name for the VM.</span></span>
* <span data-ttu-id="e56a4-244">Parola.</span><span class="sxs-lookup"><span data-stu-id="e56a4-244">A password.</span></span>
* <span data-ttu-id="e56a4-245">Dış dünyada kullanmak bir etki alanı adı.</span><span class="sxs-lookup"><span data-stu-id="e56a4-245">A domain name for the outside world to use.</span></span>
* <span data-ttu-id="e56a4-246">Ubuntu Server sürüm numarası -- ancak yalnızca bir listesini kabul eder.</span><span class="sxs-lookup"><span data-stu-id="e56a4-246">An Ubuntu Server version number -- but it will accept only one of a list.</span></span>

<span data-ttu-id="e56a4-247">[Kullanıcı adı ve parola gereksinimleri](../articles/virtual-machines/linux/faq.md#what-are-the-username-requirements-when-creating-a-vm) hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="e56a4-247">See more about [username and password requirements](../articles/virtual-machines/linux/faq.md#what-are-the-username-requirements-when-creating-a-vm).</span></span>

<span data-ttu-id="e56a4-248">Bu değerlere karar verdikten sonra bir grup oluşturmaya ve bu şablonu Azure aboneliğinize dağıtmaya hazır olursunuz.</span><span class="sxs-lookup"><span data-stu-id="e56a4-248">Once you decide on these values, you're ready to create a group for and deploy this template into your Azure subscription.</span></span>

```json
{
"$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
"contentVersion": "1.0.0.0",
"parameters": {
    "newStorageAccountName": {
    "type": "string",
    "metadata": {
        "description": "Unique DNS name for the storage account where the virtual machine's disks will be placed."
    }
    },
    "adminUsername": {
    "type": "string",
    "metadata": {
        "description": "User name for the virtual machine."
    }
    },
    "adminPassword": {
    "type": "securestring",
    "metadata": {
        "description": "Password for the virtual machine."
    }
    },
    "dnsNameForPublicIP": {
    "type": "string",
    "metadata": {
        "description": "Unique DNS name for the public IP used to access the virtual machine."
    }
    },
    "ubuntuOSVersion": {
    "type": "string",
    "defaultValue": "14.04.2-LTS",
    "allowedValues": [
        "12.04.5-LTS",
        "14.04.2-LTS",
        "15.04"
    ],
    "metadata": {
        "description": "The Ubuntu version for the VM. This will pick a fully patched image of this given Ubuntu version. Allowed values: 12.04.5-LTS, 14.04.2-LTS, 15.04."
    }
    }
},
"variables": {
    "location": "West US",
    "imagePublisher": "Canonical",
    "imageOffer": "UbuntuServer",
    "OSDiskName": "osdiskforlinuxsimple",
    "nicName": "myVMNic",
    "addressPrefix": "10.0.0.0/16",
    "subnetName": "Subnet",
    "subnetPrefix": "10.0.0.0/24",
    "storageAccountType": "Standard_LRS",
    "publicIPAddressName": "myPublicIP",
    "publicIPAddressType": "Dynamic",
    "vmStorageAccountContainerName": "vhds",
    "vmName": "MyUbuntuVM",
    "vmSize": "Standard_D1",
    "virtualNetworkName": "MyVNET",
    "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',variables('virtualNetworkName'))]",
    "subnetRef": "[concat(variables('vnetID'),'/subnets/',variables('subnetName'))]"
},
"resources": [
    {
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[parameters('newStorageAccountName')]",
    "apiVersion": "2015-05-01-preview",
    "location": "[variables('location')]",
    "properties": {
        "accountType": "[variables('storageAccountType')]"
    }
    },
    {
    "apiVersion": "2015-05-01-preview",
    "type": "Microsoft.Network/publicIPAddresses",
    "name": "[variables('publicIPAddressName')]",
    "location": "[variables('location')]",
    "properties": {
        "publicIPAllocationMethod": "[variables('publicIPAddressType')]",
        "dnsSettings": {
        "domainNameLabel": "[parameters('dnsNameForPublicIP')]"
        }
    }
    },
    {
    "apiVersion": "2015-05-01-preview",
    "type": "Microsoft.Network/virtualNetworks",
    "name": "[variables('virtualNetworkName')]",
    "location": "[variables('location')]",
    "properties": {
        "addressSpace": {
        "addressPrefixes": [
            "[variables('addressPrefix')]"
        ]
        },
        "subnets": [
        {
            "name": "[variables('subnetName')]",
            "properties": {
            "addressPrefix": "[variables('subnetPrefix')]"
            }
        }
        ]
    }
    },
    {
    "apiVersion": "2015-05-01-preview",
    "type": "Microsoft.Network/networkInterfaces",
    "name": "[variables('nicName')]",
    "location": "[variables('location')]",
    "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'))]",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
    ],
    "properties": {
        "ipConfigurations": [
        {
            "name": "ipconfig1",
            "properties": {
            "privateIPAllocationMethod": "Dynamic",
            "publicIPAddress": {
                "id": "[resourceId('Microsoft.Network/publicIPAddresses',variables('publicIPAddressName'))]"
            },
            "subnet": {
                "id": "[variables('subnetRef')]"
            }
            }
        }
        ]
    }
    },
    {
    "apiVersion": "2015-05-01-preview",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[variables('vmName')]",
    "location": "[variables('location')]",
    "dependsOn": [
        "[concat('Microsoft.Storage/storageAccounts/', parameters('newStorageAccountName'))]",
        "[concat('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
    ],
    "properties": {
        "hardwareProfile": {
        "vmSize": "[variables('vmSize')]"
        },
        "osProfile": {
        "computername": "[variables('vmName')]",
        "adminUsername": "[parameters('adminUsername')]",
        "adminPassword": "[parameters('adminPassword')]"
        },
        "storageProfile": {
        "imageReference": {
            "publisher": "[variables('imagePublisher')]",
            "offer": "[variables('imageOffer')]",
            "sku": "[parameters('ubuntuOSVersion')]",
            "version": "latest"
        },
        "osDisk": {
            "name": "osdisk",
            "vhd": {
            "uri": "[concat('http://',parameters('newStorageAccountName'),'.blob.core.windows.net/',variables('vmStorageAccountContainerName'),'/',variables('OSDiskName'),'.vhd')]"
            },
            "caching": "ReadWrite",
            "createOption": "FromImage"
        }
        },
        "networkProfile": {
        "networkInterfaces": [
            {
            "id": "[resourceId('Microsoft.Network/networkInterfaces',variables('nicName'))]"
            }
        ]
        }
    }
    }
]
}
```

### <a name="step-2-create-the-virtual-machine-by-using-the-template"></a><span data-ttu-id="e56a4-249">Adım 2: Şablon kullanarak sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="e56a4-249">Step 2: Create the virtual machine by using the template</span></span>
<span data-ttu-id="e56a4-250">Parametre değerleriniz hazır olduktan sonra şablon dağıtımınıza yönelik bir kaynak grubu oluşturmanız ve ardından şablonu dağıtmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e56a4-250">Once you have your parameter values ready, you must create a resource group for your template deployment and then deploy the template.</span></span>

<span data-ttu-id="e56a4-251">Kaynak grubu oluşturmak için istediğiniz grubun adı ve dağıtımı yapmak istediğiniz veri merkezinin konumu ile birlikte `azure group create <group name> <location>` yazın.</span><span class="sxs-lookup"><span data-stu-id="e56a4-251">To create the resource group, type `azure group create <group name> <location>` with the name of the group you want and the datacenter location into which you want to deploy.</span></span> <span data-ttu-id="e56a4-252">Bu işlem hızlı bir şekilde yapılır:</span><span class="sxs-lookup"><span data-stu-id="e56a4-252">This happens quickly:</span></span>

```azurecli
azure group create myResourceGroup westus
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Creating resource group myResourceGroup
info:    Created resource group myResourceGroup
data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags:
data:
info:    group create command OK
```

<span data-ttu-id="e56a4-253">Şimdi dağıtımı oluşturmak için `azure group deployment create` öğesini çağırıp şu komutu geçirin:</span><span class="sxs-lookup"><span data-stu-id="e56a4-253">Now to create the deployment, call `azure group deployment create` and pass:</span></span>

* <span data-ttu-id="e56a4-254">Şablon dosyası (yukarıdaki JSON şablonunu bir yerel dosyaya kaydettiyseniz).</span><span class="sxs-lookup"><span data-stu-id="e56a4-254">The template file (if you saved the above JSON template to a local file).</span></span>
* <span data-ttu-id="e56a4-255">Bir şablon URI’si (GitHub veya diğer bazı web adreslerinde dosyayı işaret etmek istiyorsanız).</span><span class="sxs-lookup"><span data-stu-id="e56a4-255">A template URI (if you want to point at the file in GitHub or some other web address).</span></span>
* <span data-ttu-id="e56a4-256">Dağıtımı yapmak istediğiniz kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="e56a4-256">The resource group into which you want to deploy.</span></span>
* <span data-ttu-id="e56a4-257">İsteğe bağlı dağıtım adı.</span><span class="sxs-lookup"><span data-stu-id="e56a4-257">An optional deployment name.</span></span>

<span data-ttu-id="e56a4-258">JSON dosyasının "parameters" bölümünde parametrelerin değerlerini belirtmeniz istenir.</span><span class="sxs-lookup"><span data-stu-id="e56a4-258">You will be prompted to supply the values of parameters in the "parameters" section of the JSON file.</span></span> <span data-ttu-id="e56a4-259">Tüm parametre değerlerini belirttiğinizde dağıtımınız başlar.</span><span class="sxs-lookup"><span data-stu-id="e56a4-259">When you have specified all the parameter values, your deployment will begin.</span></span>

<span data-ttu-id="e56a4-260">Örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="e56a4-260">Here is an example:</span></span>

```azurecli
azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-linux/azuredeploy.json myResourceGroup firstDeployment
info:    Executing command group deployment create
info:    Supply values for the following parameters
newStorageAccountName: storageaccount
adminUsername: ops
adminPassword: password
dnsNameForPublicIP: newdomainname
```

<span data-ttu-id="e56a4-261">Aşağıdaki türde bilgiler alırsınız:</span><span class="sxs-lookup"><span data-stu-id="e56a4-261">You will receive the following type of information:</span></span>

```azurecli
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "firstDeployment"
+ Registering providers
info:    Registering provider microsoft.storage
info:    Registering provider microsoft.network
info:    Registering provider microsoft.compute
+ Waiting for deployment to complete
data:    DeploymentName     : firstDeployment
data:    ResourceGroupName  : myResourceGroup
data:    ProvisioningState  : Succeeded
data:    Timestamp          : 2015-04-28T07:53:55.1828878Z
data:    Mode               : Incremental
data:    TemplateLink       : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-simple-linux-vm/azuredeploy.json
data:    ContentVersion     : 1.0.0.0
data:    Name                   Type          Value
data:    ---------------------  ------------  -------------
data:    newStorageAccountName  String        storageaccount
data:    adminUsername          String        ops
data:    adminPassword          SecureString  undefined
data:    dnsNameForPublicIP     String        newdomainname
data:    ubuntuOSVersion        String        14.10
info:    group deployment create command OK
```


## <span data-ttu-id="e56a4-262"><a id="create-a-custom-vm-image"></a>Görev: Özel bir VM görüntüsü oluşturma</span><span class="sxs-lookup"><span data-stu-id="e56a4-262"><a id="create-a-custom-vm-image"></a>Task: Create a custom VM image</span></span>
<span data-ttu-id="e56a4-263">Şablonların temel kullanımını yukarıda gördünüz; bu nedenle, Azure CLI üzerinden bir şablon kullanarak Azure’daki belirli bir .vhd dosyasından özel bir VM oluşturmak için benzer yönergeler kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="e56a4-263">You've seen the basic usage of templates above, so now we can use similar instructions to create a custom VM from a specific .vhd file in Azure by using a template via the Azure CLI.</span></span> <span data-ttu-id="e56a4-264">Buradaki farklılık, bu şablonun belirli bir sanal sabit diskten (VHD) tek bir sanal makine oluşturmasıdır.</span><span class="sxs-lookup"><span data-stu-id="e56a4-264">The difference here is that this template creates a single virtual machine from a specified virtual hard disk (VHD).</span></span>

### <a name="step-1-examine-the-json-file-for-the-template"></a><span data-ttu-id="e56a4-265">Adım 1: Şablon için JSON dosyasını inceleme</span><span class="sxs-lookup"><span data-stu-id="e56a4-265">Step 1: Examine the JSON file for the template</span></span>
<span data-ttu-id="e56a4-266">Bu bölümde örnek olarak kullanılan şablon için JSON dosyasının içeriği aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="e56a4-266">Here are the contents of the JSON file for the template that this section uses as an example.</span></span> <span data-ttu-id="e56a4-267">(Şablon [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json) içinde de bulunur.)</span><span class="sxs-lookup"><span data-stu-id="e56a4-267">(The template is also located in [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json).)</span></span>

<span data-ttu-id="e56a4-268">Burada da, varsayılan değerlere sahip olmayan parametreler için girmek istediğiniz değerleri bulmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e56a4-268">Again, you will need to find the values you want to enter for the parameters that do not have default values.</span></span> <span data-ttu-id="e56a4-269">`azure group deployment create` komutunu çalıştırdığınızda Azure CLI bu değerleri girmenizi ister.</span><span class="sxs-lookup"><span data-stu-id="e56a4-269">When you run the `azure group deployment create` command, the Azure CLI will prompt you to enter those values.</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
    "contentVersion": "1.0.0.0",
    "parameters" : {
        "userImageStorageAccountName": {
            "type": "string",
            "defaultValue" : "userImageStorageAccountName"
        },
        "userImageStorageContainerName" : {
            "type" : "string",
            "defaultValue" : "userImageStorageContainerName"
        },
        "userImageVhdName" : {
            "type" : "string",
            "defaultValue" : "userImageVhdName"
        },
        "dnsNameForPublicIP" : {
            "type" : "string",
            "defaultValue": "uniqueDnsNameForPublicIP"
        },
        "adminUserName": {
            "type": "string"
        },
        "adminPassword": {
            "type": "securestring"
        },
        "osType" : {
            "type" : "string",
            "allowedValues" : [
                "windows",
                "linux"
            ]
        },
        "subscriptionId":{
            "type" : "string"
        },
        "location": {
            "type": "String",
            "defaultValue" : "West US"
        },
        "vmSize": {
            "type": "string",
            "defaultValue": "Standard_A2"
        },
        "publicIPAddressName": {
            "type": "string",
            "defaultValue" : "myPublicIP"
        },
        "vmName": {
            "type": "string",
            "defaultValue" : "myVM"
        },
        "virtualNetworkName":{
            "type" : "string",
            "defaultValue" : "myVNET"
        },
        "nicName":{
            "type" : "string",
            "defaultValue":"myNIC"
        }
    },
    "variables": {
        "addressPrefix":"10.0.0.0/16",
        "subnet1Name": "Subnet-1",
        "subnet2Name": "Subnet-2",
        "subnet1Prefix" : "10.0.0.0/24",
        "subnet2Prefix" : "10.0.1.0/24",
        "publicIPAddressType" : "Dynamic",
        "vnetID":"[resourceId('Microsoft.Network/virtualNetworks',parameters('virtualNetworkName'))]",
        "subnet1Ref" : "[concat(variables('vnetID'),'/subnets/',variables('subnet1Name'))]",
        "userImageName" : "[concat('http://',parameters('userImageStorageAccountName'),'.blob.core.windows.net/',parameters('userImageStorageContainerName'),'/',parameters('userImageVhdName'))]",
        "osDiskVhdName" : "[concat('http://',parameters('userImageStorageAccountName'),'.blob.core.windows.net/',parameters('userImageStorageContainerName'),'/',parameters('vmName'),'osDisk.vhd')]"
    },
    "resources": [
    {
        "apiVersion": "2014-12-01-preview",
        "type": "Microsoft.Network/publicIPAddresses",
        "name": "[parameters('publicIPAddressName')]",
        "location": "[parameters('location')]",
        "properties": {
            "publicIPAllocationMethod": "[variables('publicIPAddressType')]",
            "dnsSettings": {
                "domainNameLabel": "[parameters('dnsNameForPublicIP')]"
            }
        }
    },
    {
        "apiVersion": "2014-12-01-preview",
        "type": "Microsoft.Network/virtualNetworks",
        "name": "[parameters('virtualNetworkName')]",
        "location": "[parameters('location')]",
        "properties": {
        "addressSpace": {
            "addressPrefixes": [
            "[variables('addressPrefix')]"
            ]
        },
        "subnets": [
            {
            "name": "[variables('subnet1Name')]",
            "properties" : {
                "addressPrefix": "[variables('subnet1Prefix')]"
            }
            },
            {
            "name": "[variables('subnet2Name')]",
            "properties" : {
                "addressPrefix": "[variables('subnet2Prefix')]"
            }
            }
        ]
        }
    },
    {
        "apiVersion": "2014-12-01-preview",
        "type": "Microsoft.Network/networkInterfaces",
        "name": "[parameters('nicName')]",
        "location": "[parameters('location')]",
        "dependsOn": [
            "[concat('Microsoft.Network/publicIPAddresses/', parameters('publicIPAddressName'))]",
            "[concat('Microsoft.Network/virtualNetworks/', parameters('virtualNetworkName'))]"
        ],
        "properties": {
            "ipConfigurations": [
            {
                "name": "ipconfig1",
                "properties": {
                    "privateIPAllocationMethod": "Dynamic",
                    "publicIPAddress": {
                        "id": "[resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName'))]"
                    },
                    "subnet": {
                        "id": "[variables('subnet1Ref')]"
                    }
                }
            }
            ]
        }
    },
    {
        "apiVersion": "2014-12-01-preview",
        "type": "Microsoft.Compute/virtualMachines",
        "name": "[parameters('vmName')]",
        "location": "[parameters('location')]",
        "dependsOn": [
            "[concat('Microsoft.Network/networkInterfaces/', parameters('nicName'))]"
        ],
        "properties": {
            "hardwareProfile": {
                "vmSize": "[parameters('vmSize')]"
            },
            "osProfile": {
                "computername": "[parameters('vmName')]",
                "adminUsername": "[parameters('adminUsername')]",
                "adminPassword": "[parameters('adminPassword')]"
            },
            "storageProfile": {
                "osDisk" : {
                    "name" : "[concat(parameters('vmName'),'-osDisk')]",
                    "osType" : "[parameters('osType')]",
                    "caching" : "ReadWrite",
                    "image" : {
                        "uri" : "[variables('userImageName')]"
                    },
                    "vhd" : {
                        "uri" : "[variables('osDiskVhdName')]"
                    }
                }
            },
            "networkProfile": {
                "networkInterfaces" : [
                {
                    "id": "[resourceId('Microsoft.Network/networkInterfaces',parameters('nicName'))]"
                }
                ]
            }
        }
    }
    ]
}
```

### <a name="step-2-obtain-the-vhd"></a><span data-ttu-id="e56a4-270">Adım 2: VHD alma</span><span class="sxs-lookup"><span data-stu-id="e56a4-270">Step 2: Obtain the VHD</span></span>
<span data-ttu-id="e56a4-271">Bunun için bir .vhd dosyasının gerekli olduğu açıktır.</span><span class="sxs-lookup"><span data-stu-id="e56a4-271">Obviously, you'll need a .vhd for this.</span></span> <span data-ttu-id="e56a4-272">Azure’da zaten sahip olduğunuz dosyayı kullanabilir veya bir tane yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e56a4-272">You can use one you already have in Azure, or you can upload one.</span></span>

<span data-ttu-id="e56a4-273">Windows tabanlı bir sanal makine için bkz. [Windows Server VHD’si oluşturup Azure’a yükleme](../articles/virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e56a4-273">For a Windows-based virtual machine, see [Create and upload a Windows Server VHD to Azure](../articles/virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="e56a4-274">Linux tabanlı sanal makine için bkz. [Linux işletim sistemi içeren bir sanal sabit disk oluşturma ve karşıya yükleme](../articles/virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e56a4-274">For a Linux-based virtual machine, see [Creating and uploading a virtual hard disk that contains the Linux operating system](../articles/virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

### <a name="step-3-create-the-virtual-machine-by-using-the-template"></a><span data-ttu-id="e56a4-275">Adım 3: Şablon kullanarak sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="e56a4-275">Step 3: Create the virtual machine by using the template</span></span>
<span data-ttu-id="e56a4-276">Şu anda .vhd’yi temel alan yeni bir sanal makine oluşturmaya hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="e56a4-276">Now you're ready to create a new virtual machine based on the .vhd.</span></span> <span data-ttu-id="e56a4-277">`azure group create <location>` komutunu kullanarak dağıtımın yapılacağı grubu oluşturun:</span><span class="sxs-lookup"><span data-stu-id="e56a4-277">Create a group to deploy into, by using `azure group create <location>`:</span></span>

```azurecli
azure group create myResourceGroupUser eastus
info:    Executing command group create
+ Getting resource group myResourceGroupUser
+ Creating resource group myResourceGroupUser
info:    Created resource group myResourceGroupUser
data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroupUser
data:    Name:                myResourceGroupUser
data:    Location:            eastus
data:    Provisioning State:  Succeeded
data:    Tags:
data:
info:    group create command OK
```

<span data-ttu-id="e56a4-278">Ardından `--template-uri` seçeneğini kullanarak şablonu doğrudan çağırmak için dağıtımı oluşturun (veya `--template-file` seçeneğini kullanarak yerel olarak kaydettiğiniz bir dosyayı kullanabilirsiniz).</span><span class="sxs-lookup"><span data-stu-id="e56a4-278">Then create the deployment by using the `--template-uri` option to call in the template directly (or you can use the `--template-file` option to use a file that you have saved locally).</span></span> <span data-ttu-id="e56a4-279">Şablonun varsayılan değerleri belirtildiği için sizden yalnızca birkaç şey istenir.</span><span class="sxs-lookup"><span data-stu-id="e56a4-279">Note that because the template has defaults specified, you are prompted for only a few things.</span></span> <span data-ttu-id="e56a4-280">Şablonu farklı yerlere dağıtırsanız, varsayılan değerlerle bazı adlandırma çakışmalarının oluştuğunu görebilirsiniz (özellikle oluşturduğunuz DNS adı).</span><span class="sxs-lookup"><span data-stu-id="e56a4-280">If you deploy the template in different places, you may find that some naming collisions occur with the default values (particularly the DNS name you create).</span></span>

```azurecli
azure group deployment create \
> --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json \
> myResourceGroup \
> customVhdDeployment
info:    Executing command group deployment create
info:    Supply values for the following parameters
adminUserName: ops
adminPassword: password
osType: linux
subscriptionId: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```

<span data-ttu-id="e56a4-281">Çıktı aşağıdakine benzer olacaktır:</span><span class="sxs-lookup"><span data-stu-id="e56a4-281">Output looks something like the following:</span></span>

```azurecli
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "customVhdDeployment"
+ Registering providers
info:    Registering provider microsoft.network
info:    Registering provider microsoft.compute
+ Waiting for deployment to complete
error:   Deployment provisioning state was not successful
data:    DeploymentName     : customVhdDeployment
data:    ResourceGroupName  : myResourceGroupUser
data:    ProvisioningState  : Succeeded
data:    Timestamp          : 2015-04-28T14:55:48.0963829Z
data:    Mode               : Incremental
data:    TemplateLink       : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json
data:    ContentVersion     : 1.0.0.0
data:    Name                           Type          Value
data:    -----------------------------  ------------  ------------------------------------
data:    userImageStorageAccountName    String        userImageStorageAccountName
data:    userImageStorageContainerName  String        userImageStorageContainerName
data:    userImageVhdName               String        userImageVhdName
data:    dnsNameForPublicIP             String        uniqueDnsNameForPublicIP
data:    adminUserName                  String        ops
data:    adminPassword                  SecureString  undefined
data:    osType                         String        linux
data:    subscriptionId                 String        xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
data:    location                       String        West US
data:    vmSize                         String        Standard_A2
data:    publicIPAddressName            String        myPublicIP
data:    vmName                         String        myVM
data:    virtualNetworkName             String        myVNET
data:    nicName                        String        myNIC
info:    group deployment create command OK
```

## <span data-ttu-id="e56a4-282"><a id="deploy-a-multi-vm-application-that-uses-a-virtual-network-and-an-external-load-balancer"></a>Görev: Sanal ağ ve dış yük dengeleyici kullanan çok sanal makineli uygulama dağıtma</span><span class="sxs-lookup"><span data-stu-id="e56a4-282"><a id="deploy-a-multi-vm-application-that-uses-a-virtual-network-and-an-external-load-balancer"></a>Task: Deploy a multi-VM application that uses a virtual network and an external load balancer</span></span>
<span data-ttu-id="e56a4-283">Bu şablon bir yük dengeleyici altında iki sanal makine oluşturmanıza ve Bağlantı Noktası 80 üzerinde bir yük dengeleme kuralı yapılandırmanıza olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="e56a4-283">This template allows you to create two virtual machines under a load balancer and configure a load-balancing rule on Port 80.</span></span> <span data-ttu-id="e56a4-284">Bu şablon ayrıca bir depolama hesabı, sanal ağ, genel IP adresi, kullanılabilirlik kümesi ve ağ arabirimleri dağıtır.</span><span class="sxs-lookup"><span data-stu-id="e56a4-284">This template also deploys a storage account, virtual network, public IP address, availability set, and network interfaces.</span></span>

![](./media/virtual-machines-common-cli-deploy-templates/multivmextlb.png)

<span data-ttu-id="e56a4-285">GitHub şablon deposunda Azure PowerShell komutları aracılığıyla Resource Manager şablonu kullanarak, sanal ağ ve yük dengeleyicisi kullanan çok sanal makineli bir uygulama dağıtmak için bu adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="e56a4-285">Follow these steps to deploy a multi-VM application that uses a virtual network and a load balancer by using a Resource Manager template in the GitHub template repository via Azure PowerShell commands.</span></span>

### <a name="step-1-examine-the-json-file-for-the-template"></a><span data-ttu-id="e56a4-286">Adım 1: Şablon için JSON dosyasını inceleme</span><span class="sxs-lookup"><span data-stu-id="e56a4-286">Step 1: Examine the JSON file for the template</span></span>
<span data-ttu-id="e56a4-287">Şablon için JSON dosyasının içeriği aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="e56a4-287">Here are the contents of the JSON file for the template.</span></span> <span data-ttu-id="e56a4-288">En son sürümü istiyorsanız bunu bulunduktan [şablonları için GitHub deposunda](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="e56a4-288">If you want the most recent version, it's located [at the GitHub repository for templates](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json).</span></span> <span data-ttu-id="e56a4-289">Bu konu başlığında şablonu çağırmak için `--template-uri` anahtarı kullanılır, ancak yerel bir sürüm geçirmek için `--template-file` anahtarını da kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e56a4-289">This topic uses the `--template-uri` switch to call in the template, but you can also use the `--template-file` switch to pass a local version.</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "location": {
            "type": "string",
            "metadata": {
                "description": "Location of resources"
            }
        },
        "storageAccountName": {
            "type": "string",
            "metadata": {
                "description": "Name of storage account"
            }
        },
        "adminUsername": {
            "type": "string",
            "metadata": {
                "description": "Admin user name"
            }
        },
        "adminPassword": {
            "type": "securestring",
            "metadata": {
                "description": "Admin password"
            }
        },
        "dnsNameforLBIP": {
            "type": "string",
            "metadata": {
                "description": "DNS for load balancer IP"
            }
        },
        "backendPort": {
            "type": "int",
            "defaultValue": 3389,
            "metadata": {
                "description": "Back-end port"
            }
        },
        "vmNamePrefix": {
            "type": "string",
            "defaultValue": "myVM",
            "metadata": {
                "description": "Prefix to use for VM names"
            }
        },
        "vmSourceImageName": {
            "type": "string",
            "defaultValue": "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-201412.01-en.us-127GB.vhd"
        },
        "lbName": {
            "type": "string",
            "defaultValue": "myLB",
            "metadata": {
                "description": "Load balancer name"
            }
        },
        "nicNamePrefix": {
            "type": "string",
            "defaultValue": "nic",
            "metadata": {
                "description": "Network interface name prefix"
            }
        },
        "publicIPAddressName": {
            "type": "string",
            "defaultValue": "myPublicIP",
            "metadata": {
                "description": "Public IP name"
            }
        },
        "vnetName": {
            "type": "string",
            "defaultValue": "myVNET",
            "metadata": {
                "description": "Virtual network name"
            }
        },
        "vmSize": {
            "type": "string",
            "defaultValue": "Standard_A1",
            "metadata": {
                "description": "Size of the VM"
            }
        }
    },
    "variables": {
        "storageAccountType": "Standard_LRS",
        "vmStorageAccountContainerName": "vhds",
        "availabilitySetName": "myAvSet",
        "addressPrefix": "10.0.0.0/16",
        "subnetName": "Subnet-1",
        "subnetPrefix": "10.0.0.0/24",
        "publicIPAddressType": "Dynamic",
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',parameters('vnetName'))]",
        "subnetRef": "[concat(variables('vnetID'),'/subnets/',variables ('subnetName'))]",
        "publicIPAddressID": "[resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName'))]",
        "lbID": "[resourceId('Microsoft.Network/loadBalancers',parameters('lbName'))]",
        "numberOfInstances": 2,
        "nicId1": "[resourceId('Microsoft.Network/networkInterfaces',concat(parameters('nicNamePrefix'), 0))]",
        "nicId2": "[resourceId('Microsoft.Network/networkInterfaces',concat(parameters('nicNamePrefix'), 1))]",
        "frontEndIPConfigID": "[concat(variables('lbID'),'/frontendIPConfigurations/LBFE')]",
        "backEndIPConfigID1": "[concat(variables('nicId1'),'/ipConfigurations/ipconfig1')]",
        "backEndIPConfigID2": "[concat(variables('nicId2'),'/ipConfigurations/ipconfig1')]",
        "sourceImageName": "[concat('/', subscription().subscriptionId,'/services/images/',parameters('vmSourceImageName'))]",
        "lbPoolID": "[concat(variables('lbID'),'/backendAddressPools/LBBE')]",
        "lbProbeID": "[concat(variables('lbID'),'/probes/tcpProbe')]"
    },
    "resources": [
        {
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[parameters('storageAccountName')]",
            "apiVersion": "2015-05-01-preview",
            "location": "[parameters('location')]",
            "properties": {
                "accountType": "[variables('storageAccountType')]"
            }
        },
        {
            "type": "Microsoft.Compute/availabilitySets",
            "name": "[variables('availabilitySetName')]",
            "apiVersion": "2015-05-01-preview",
            "location": "[parameters('location')]",
            "properties": { }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "type": "Microsoft.Network/publicIPAddresses",
            "name": "[parameters('publicIPAddressName')]",
            "location": "[parameters('location')]",
            "properties": {
                "publicIPAllocationMethod": "[variables('publicIPAddressType')]",
                "dnsSettings": {
                    "domainNameLabel": "[parameters('dnsNameforLBIP')]"
                }
            }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "type": "Microsoft.Network/virtualNetworks",
            "name": "[parameters('vnetName')]",
            "location": "[parameters('location')]",
            "properties": {
                "addressSpace": {
                    "addressPrefixes": [
                        "[variables('addressPrefix')]"
                    ]
                },
                "subnets": [
                    {
                        "name": "[variables('subnetName')]",
                        "properties": {
                            "addressPrefix": "[variables('subnetPrefix')]"
                        }
                    }
                ]
            }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "type": "Microsoft.Network/networkInterfaces",
            "name": "[concat(parameters('nicNamePrefix'), copyindex())]",
            "location": "[parameters('location')]",
            "copy": {
                "name": "nicLoop",
                "count": "[variables('numberOfInstances')]"
            },
            "dependsOn": [
                "[concat('Microsoft.Network/virtualNetworks/', parameters('vnetName'))]"
            ],
            "properties": {
                "ipConfigurations": [
                    {
                        "name": "ipconfig1",
                        "properties": {
                            "privateIPAllocationMethod": "Dynamic",
                            "subnet": {
                                "id": "[variables('subnetRef')]"
                            }
                        },
                        "loadBalancerBackendAddressPools": [
                            {
                                "id": "[concat('Microsoft.Network/loadBalancers/',parameters('lbName'),'/backendAddressPools/LBBE')]"
                            }
                        ],
                        "loadBalancerInboundNatRules": [
                            {
                                "id": "[concat('Microsoft.Network/loadBalancers/',parameters('lbName'),'/inboundNatRule/RDP-VM', copyindex())]"
                            }
                        ]


                    }
                ]

            }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "name": "[parameters('lbName')]",
            "type": "Microsoft.Network/loadBalancers",
            "location": "[parameters('location')]",
            "dependsOn": [
                "nicLoop",
                "[concat('Microsoft.Network/publicIPAddresses/', parameters('publicIPAddressName'))]"
            ],
            "properties": {
                "frontendIPConfigurations": [
                    {
                        "name": "LBFE",
                        "properties": {
                            "publicIPAddress": {
                                "id": "[variables('publicIPAddressID')]"
                            }
                        }
                    }
                ],
                "backendAddressPools": [
                    {
                        "name": "LBBE"

                    }
                ],
                "inboundNatRules": [
                    {
                        "name": "RDP-VM1",
                        "properties": {
                            "frontendIPConfiguration":
                                {
                                    "id": "[variables('frontEndIPConfigID')]"
                                },
                            "protocol": "tcp",
                            "frontendPort": 50001,
                            "backendPort": 3389,
                            "enableFloatingIP": false
                        }
                    },
                    {
                        "name": "RDP-VM2",
                        "properties": {
                            "frontendIPConfiguration":
                                {
                                    "id": "[variables('frontEndIPConfigID')]"
                                },
                            "protocol": "tcp",
                            "frontendPort": 50002,
                            "backendPort": 3389,
                            "enableFloatingIP": false
                        }
                    }
                ],
                "loadBalancingRules": [
                    {
                        "name": "LBRule",
                        "properties": {
                            "frontendIPConfiguration": {
                                "id": "[variables('frontEndIPConfigID')]"
                            },
                            "backendAddressPool": {
                                "id": "[variables('lbPoolID')]"
                            },
                            "protocol": "tcp",
                            "frontendPort": 80,
                            "backendPort": 80,
                            "enableFloatingIP": false,
                            "idleTimeoutInMinutes": 5,
                            "probe": {
                                "id": "[variables('lbProbeID')]"
                            }
                        }
                    }
                ],
                "probes": [
                    {
                        "name": "tcpProbe",
                        "properties": {
                            "protocol": "tcp",
                            "port": 80,
                            "intervalInSeconds": "5",
                            "numberOfProbes": "2"
                        }
                    }
                ]
            }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "type": "Microsoft.Compute/virtualMachines",
            "name": "[concat(parameters('vmNamePrefix'), copyindex())]",
            "copy": {
                "name": "virtualMachineLoop",
                "count": "[variables('numberOfInstances')]"
            },
            "location": "[parameters('location')]",
            "dependsOn": [
                "[concat('Microsoft.Storage/storageAccounts/', parameters('storageAccountName'))]",
                "[concat('Microsoft.Network/networkInterfaces/', parameters('nicNamePrefix'), copyindex())]",
                "[concat('Microsoft.Compute/availabilitySets/', variables('availabilitySetName'))]"
            ],
            "properties": {
                "availabilitySet": {
                    "id": "[resourceId('Microsoft.Compute/availabilitySets',variables('availabilitySetName'))]"
                },
                "hardwareProfile": {
                    "vmSize": "[parameters('vmSize')]"
                },
                "osProfile": {
                    "computername": "[concat(parameters('vmNamePrefix'), copyIndex())]",
                    "adminUsername": "[parameters('adminUsername')]",
                    "adminPassword": "[parameters('adminPassword')]"
                },
                "storageProfile": {
                    "sourceImage": {
                        "id": "[variables('sourceImageName')]"
                    },
                    "destinationVhdsContainer": "[concat('http://',parameters('storageAccountName'),'.blob.core.windows.net/',variables('vmStorageAccountContainerName'),'/')]"
                },
                "networkProfile": {
                    "networkInterfaces": [
                        {
                            "id": "[resourceId('Microsoft.Network/networkInterfaces',concat(parameters('nicNamePrefix'),copyindex()))]"
                        }
                    ]
                }
            }
        }
    ]
}
```

### <a name="step-2-create-the-deployment-by-using-the-template"></a><span data-ttu-id="e56a4-290">Adım 2: Şablon kullanarak dağıtım oluşturma</span><span class="sxs-lookup"><span data-stu-id="e56a4-290">Step 2: Create the deployment by using the template</span></span>
<span data-ttu-id="e56a4-291">`azure group create <location>` kullanarak şablon için bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e56a4-291">Create a resource group for the template by using `azure group create <location>`.</span></span> <span data-ttu-id="e56a4-292">Ardından, `azure group deployment create` komutunu kullanıp kaynak grubunu geçirerek, bir dağıtım adı geçirerek ve varsayılan değerlere sahip olmayan şablondaki parametrelere yönelik istemleri yanıtlayarak bu kaynak grubunda bir dağıtım oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e56a4-292">Then, create a deployment into that resource group by using `azure group deployment create` and passing the resource group, passing a deployment name, and answering the prompts for parameters in the template that did not have default values.</span></span>

```azurecli
azure group create lbgroup westus
info:    Executing command group create
+ Getting resource group lbgroup
+ Creating resource group lbgroup
info:    Created resource group lbgroup
data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/lbgroup
data:    Name:                lbgroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags:
data:
info:    group create command OK
```

<span data-ttu-id="e56a4-293">Şimdi `azure group deployment create` komutu ile `--template-uri` seçeneğini kullanarak şablonu dağıtın.</span><span class="sxs-lookup"><span data-stu-id="e56a4-293">Now use the `azure group deployment create` command and the `--template-uri` option to deploy the template.</span></span> <span data-ttu-id="e56a4-294">Aşağıda gösterildiği gibi sizden istediğinde parametre değerlerini belirtmeye hazır olun.</span><span class="sxs-lookup"><span data-stu-id="e56a4-294">Be ready with your parameter values when it prompts you, as shown below.</span></span>

```azurecli
azure group deployment create \
> --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json \
> lbgroup \
> newdeployment
info:    Executing command group deployment create
info:    Supply values for the following parameters
location: westus
newStorageAccountName: storagename
adminUsername: ops
adminPassword: password
dnsNameforLBIP: lbdomainname
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "newdeployment"
+ Registering providers
info:    Registering provider microsoft.storage
info:    Registering provider microsoft.compute
info:    Registering provider microsoft.network
+ Waiting for deployment to complete
data:    DeploymentName     : newdeployment
data:    ResourceGroupName  : lbgroup
data:    ProvisioningState  : Succeeded
data:    Timestamp          : 2015-04-28T20:58:40.1678876Z
data:    Mode               : Incremental
data:    TemplateLink       : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json
data:    ContentVersion     : 1.0.0.0
data:    Name                   Type          Value
data:    ---------------------  ------------  ----------------------
data:    location               String        westus
data:    newStorageAccountName  String        storagename
data:    adminUsername          String        ops
data:    adminPassword          SecureString  undefined
data:    dnsNameforLBIP         String        lbdomainname
data:    backendPort            Int           3389
data:    vmNamePrefix           String        myVM
data:    imagePublisher         String        MicrosoftWindowsServer
data:    imageOffer             String        WindowsServer
data:    imageSKU               String        2012-R2-Datacenter
data:    lbName                 String        myLB
data:    nicNamePrefix          String        nic
data:    publicIPAddressName    String        myPublicIP
data:    vnetName               String        myVNET
data:    vmSize                 String        Standard_A1
info:    group deployment create command OK
```

<span data-ttu-id="e56a4-295">Bu şablon bir Windows Server görüntüsünü dağıtır; ancak herhangi bir Linux görüntüsü ile kolayca değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="e56a4-295">Note that this template deploys a Windows Server image; however, it could easily be replaced by any Linux image.</span></span> <span data-ttu-id="e56a4-296">Birden fazla swarm yöneticisine sahip bir Docker kümesi mi oluşturmak istiyorsunuz?</span><span class="sxs-lookup"><span data-stu-id="e56a4-296">Want to create a Docker cluster with multiple swarm managers?</span></span> <span data-ttu-id="e56a4-297">[Bunu yapabilirsiniz](https://azure.microsoft.com/documentation/templates/docker-swarm-cluster/).</span><span class="sxs-lookup"><span data-stu-id="e56a4-297">[You can do it](https://azure.microsoft.com/documentation/templates/docker-swarm-cluster/).</span></span>

## <span data-ttu-id="e56a4-298"><a id="remove-a-resource-group"></a>Görev: Kaynak grubunu kaldırma</span><span class="sxs-lookup"><span data-stu-id="e56a4-298"><a id="remove-a-resource-group"></a>Task: Remove a resource group</span></span>
<span data-ttu-id="e56a4-299">Bir kaynak grubuna yeniden dağıtım yapabilirsiniz, ancak bir kaynak grubuyla işiniz bittiyse `azure group delete <group name>` komutunu kullanarak kaynak grubunu silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e56a4-299">Remember that you can redeploy to a resource group, but if you are done with one, you can delete it by using `azure group delete <group name>`.</span></span>

```azurecli
azure group delete myResourceGroup
info:    Executing command group delete
Delete resource group myResourceGroup? [y/n] y
+ Deleting resource group myResourceGroup
info:    group delete command OK
```

## <span data-ttu-id="e56a4-300"><a id="show-the-log-for-a-resource-group-deployment"></a>Görev: Bir kaynak grubu dağıtımının günlüğünü görüntüleme</span><span class="sxs-lookup"><span data-stu-id="e56a4-300"><a id="show-the-log-for-a-resource-group-deployment"></a>Task: Show the log for a resource group deployment</span></span>
<span data-ttu-id="e56a4-301">Şablon oluştururken veya kullanırken bu işlem yaygın olarak yapılır.</span><span class="sxs-lookup"><span data-stu-id="e56a4-301">This one is common while you're creating or using templates.</span></span> <span data-ttu-id="e56a4-302">Bir grubun dağıtım günlüklerini görüntüleme çağrısı, bir olayın neden gerçekleştiğini (veya gerçekleşmediğini) anlamak için yararlı olabilecek bilgileri `azure group log show <groupname>` komutudur.</span><span class="sxs-lookup"><span data-stu-id="e56a4-302">The call to display the deployment logs for a group is `azure group log show <groupname>`, which displays quite a bit of information that's useful for understanding why something happened -- or didn't.</span></span> <span data-ttu-id="e56a4-303">(Dağıtımlarınızla ilgili daha fazla sorun giderme bilgisi ve sorunlar hakkında diğer bilgiler için bkz. [Azure Resource Manager ile yaygın Azure dağıtım hatalarını giderme](../articles/azure-resource-manager/resource-manager-common-deployment-errors.md).)</span><span class="sxs-lookup"><span data-stu-id="e56a4-303">(For more information on troubleshooting your deployments, as well as other information about issues, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](../articles/azure-resource-manager/resource-manager-common-deployment-errors.md).)</span></span>

<span data-ttu-id="e56a4-304">Örneğin, belirli hataları hedeflemek için **jq** gibi araçlar kullanarak, düzeltmeniz gereken belirli hatalar gibi sorunları daha kesin bir şekilde sorgulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e56a4-304">To target specific failures, for example, you might use tools like **jq** to query things a bit more precisely, such as which individual failures you need to correct.</span></span> <span data-ttu-id="e56a4-305">Aşağıdaki örnekte hatalar aranırken **lbgroup** dağıtım günlüğünü ayrıştırmak için **jq** kullanılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="e56a4-305">The following example uses **jq** to parse a deployment log for **lbgroup**, looking for failures.</span></span>

```azurecli
azure group log show lbgroup -l --json | jq '.[] | select(.status.value == "Failed") | .properties'
```
<span data-ttu-id="e56a4-306">Neyin yanlış gittiğini hızlıca bulabilir, düzeltebilir ve yeniden deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e56a4-306">You can discover very quickly what went wrong, fix, and retry.</span></span> <span data-ttu-id="e56a4-307">Aşağıdaki örnekte, şablon aynı anda iki VM oluşturmuş ve .vhd üzerinde bir kilit oluşturmuştur.</span><span class="sxs-lookup"><span data-stu-id="e56a4-307">In the following case, the template had been creating two VMs at the same time, which created a lock on the .vhd.</span></span> <span data-ttu-id="e56a4-308">(Şablon değiştirildikten sonra dağıtım hızlıca başarılı olmuştur.)</span><span class="sxs-lookup"><span data-stu-id="e56a4-308">(After we modified the template, the deployment succeeded quickly.)</span></span>

```json
{
    "statusCode": "Conflict",
    "statusMessage": "{\"status\":\"Failed\",\"error\":{\"code\":\"ResourceDeploymentFailure\",\"message\":\"The resource operation completed with terminal provisioning state 'Failed'.\",\"details\":[{\"code\":\"AcquireDiskLeaseFailed\",\"message\":\"Failed to acquire lease while creating disk 'osdisk' using blob with URI http://storage.blob.core.windows.net/vhds/osdisk.vhd.\"}]}}"
}
```

## <span data-ttu-id="e56a4-309"><a id="display-information-about-a-virtual-machine"></a>Görev: Bir sanal makine hakkında bilgi görüntüleme</span><span class="sxs-lookup"><span data-stu-id="e56a4-309"><a id="display-information-about-a-virtual-machine"></a>Task: Display information about a virtual machine</span></span>
<span data-ttu-id="e56a4-310">`azure vm show <groupname> <vmname>` komutunu kullanarak kaynak grubunuzdaki belirli VM’ler hakkındaki bilgileri görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e56a4-310">You can see information about specific VMs in your resource group by using the `azure vm show <groupname> <vmname>` command.</span></span> <span data-ttu-id="e56a4-311">Grubunuzda birden fazla VM varsa, ilk olarak `azure vm list <groupname>` ile gruptaki VM’leri listelemeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="e56a4-311">If you have more than one VM in your group, you might first need to list the VMs in a group by using `azure vm list <groupname>`.</span></span>

```azurecli
azure vm list zoo
info:    Executing command vm list
+ Getting virtual machines
data:    Name   ProvisioningState  Location  Size
data:    -----  -----------------  --------  -----------
data:    myVM0  Succeeded          westus    Standard_A1
data:    myVM1  Failed             westus    Standard_A1
```

<span data-ttu-id="e56a4-312">Ardından, myVM1 öğesini arayın:</span><span class="sxs-lookup"><span data-stu-id="e56a4-312">And then, looking up myVM1:</span></span>

```azurecli
azure vm show zoo myVM1
info:    Executing command vm show
+ Looking up the VM "myVM1"
+ Looking up the NIC "nic1"
data:    Id                              :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/zoo/providers/Microsoft.Compute/virtualMachines/myVM1
data:    ProvisioningState               :Failed
data:    Name                            :myVM1
data:    Location                        :westus
data:    Type                            :Microsoft.Compute/virtualMachines
data:
data:    Hardware Profile:
data:      Size                          :Standard_A1
data:
data:    Storage Profile:
data:      Image reference:
data:        Publisher                   :MicrosoftWindowsServer
data:        Offer                       :WindowsServer
data:        Sku                         :2012-R2-Datacenter
data:        Version                     :latest
data:
data:      OS Disk:
data:        OSType                      :Windows
data:        Name                        :osdisk
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :http://zoostorageralph.blob.core.windows.net/vhds/osdisk.vhd
data:
data:    OS Profile:
data:      Computer Name                 :myVM1
data:      User Name                     :ops
data:      Windows Configuration:
data:        Provision VM Agent          :true
data:        Enable automatic updates    :true
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Id                        :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/zoo/providers/Microsoft.Network/networkInterfaces/nic1
data:          Primary                   :false
data:          Provisioning State        :Succeeded
data:          Name                      :nic1
data:          Location                  :westus
data:            Private IP alloc-method :Dynamic
data:            Private IP address      :10.0.0.5
data:
data:    AvailabilitySet:
data:      Id                            :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/zoo/providers/Microsoft.Compute/availabilitySets/MYAVSET
info:    vm show command OK
```

> [!NOTE]
> <span data-ttu-id="e56a4-313">Konsol komutlarınızın çıktısını programlı olarak depolamak ve yönlendirmek istiyorsanız **[jq](https://github.com/stedolan/jq)** veya **[jsawk](https://github.com/micha/jsawk)** gibi bir JSON ayrıştırma aracı ya da görev için yararlı dil kitaplıkları kullanmak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e56a4-313">If you want to programmatically store and manipulate the output of your console commands, you may want to use a JSON parsing tool such as **[jq](https://github.com/stedolan/jq)** or **[jsawk](https://github.com/micha/jsawk)**, or language libraries that are good for the task.</span></span>
>
>

## <span data-ttu-id="e56a4-314"><a id="log-on-to-a-linux-based-virtual-machine"></a>Görev: Linux tabanlı sanal makinede oturum açma</span><span class="sxs-lookup"><span data-stu-id="e56a4-314"><a id="log-on-to-a-linux-based-virtual-machine"></a>Task: Log on to a Linux-based virtual machine</span></span>
<span data-ttu-id="e56a4-315">Linux makinelerine genellikle SSH aracılığıyla bağlanılır.</span><span class="sxs-lookup"><span data-stu-id="e56a4-315">Typically Linux machines are connected to through SSH.</span></span> <span data-ttu-id="e56a4-316">Daha fazla bilgi için bkz. [Azure’da Linux ile SSH kullanma](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e56a4-316">For more information, see [How to use SSH with Linux on Azure](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <span data-ttu-id="e56a4-317"><a id="stop-a-virtual-machine"></a>Görev: VM durdurma</span><span class="sxs-lookup"><span data-stu-id="e56a4-317"><a id="stop-a-virtual-machine"></a>Task: Stop a VM</span></span>
<span data-ttu-id="e56a4-318">Şu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="e56a4-318">Run this command:</span></span>

```azurecli
azure vm stop <group name> <virtual machine name>
```

> [!IMPORTANT]
> <span data-ttu-id="e56a4-319">Bir sanal ağ içindeki son VM olması durumunda sanal ağın sanal IP’sini (VIP) saklamak için bu parametreyi kullanın.</span><span class="sxs-lookup"><span data-stu-id="e56a4-319">Use this parameter to keep the virtual IP (VIP) of the vnet in case it's the last VM in that vnet.</span></span> <br><br> <span data-ttu-id="e56a4-320">`StayProvisioned` parametresini kullansanız bile VM için fatura almaya devam edersiniz.</span><span class="sxs-lookup"><span data-stu-id="e56a4-320">If you use the `StayProvisioned` parameter, you'll still be billed for the VM.</span></span>
>
>

## <span data-ttu-id="e56a4-321"><a id="start-a-virtual-machine"></a>Görev: VM başlatma</span><span class="sxs-lookup"><span data-stu-id="e56a4-321"><a id="start-a-virtual-machine"></a>Task: Start a VM</span></span>
<span data-ttu-id="e56a4-322">Şu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="e56a4-322">Run this command:</span></span>

```azurecli
azure vm start <group name> <virtual machine name>
```

## <span data-ttu-id="e56a4-323"><a id="attach-a-data-disk"></a>Görev: Veri diski ekleme</span><span class="sxs-lookup"><span data-stu-id="e56a4-323"><a id="attach-a-data-disk"></a>Task: Attach a data disk</span></span>
<span data-ttu-id="e56a4-324">Ayrıca yeni bir disk veya veri içeren bir disk eklemeye karar vermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e56a4-324">You'll also need to decide whether to attach a new disk or one that contains data.</span></span> <span data-ttu-id="e56a4-325">Yeni bir disk için komut .vhd dosyasını oluşturup aynı komuta ekler.</span><span class="sxs-lookup"><span data-stu-id="e56a4-325">For a new disk, the command creates the .vhd file and attaches it in the same command.</span></span>

<span data-ttu-id="e56a4-326">Yeni bir disk eklemek için şu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="e56a4-326">To attach a new disk, run this command:</span></span>

```azurecli
    azure vm disk attach-new <resource-group> <vm-name> <size-in-gb>
```

<span data-ttu-id="e56a4-327">Var olan bir veri diski eklemek için şu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="e56a4-327">To attach an existing data disk, run this command:</span></span>

```azurecli
azure vm disk attach <resource-group> <vm-name> [vhd-url]
```

<span data-ttu-id="e56a4-328">Ardından Linux’ta yaptığınız gibi diski bağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e56a4-328">Then you'll need to mount the disk, as you normally would in Linux.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e56a4-329">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e56a4-329">Next steps</span></span>
<span data-ttu-id="e56a4-330">**Arm** modu ile Azure CLI kullanımı hakkında çok daha fazla örnek için bkz. [Azure Resource Manager ile Mac, Linux ve Windows için Azure CLI kullanma](../articles/xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="e56a4-330">For far more examples of Azure CLI usage with the **arm** mode, see [Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](../articles/xplat-cli-azure-resource-manager.md).</span></span> <span data-ttu-id="e56a4-331">Azure kaynakları ile kavramları hakkında daha fazla bilgi için bkz. [Azure Resource Manager'a genel bakış](../articles/azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e56a4-331">To learn more about Azure resources and their concepts, see [Azure Resource Manager overview](../articles/azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="e56a4-332">Kullanabileceğiniz diğer şablonlar için bkz. [Azure Hızlı Başlangıç şablonları](https://azure.microsoft.com/documentation/templates/) ve [Şablon kullanan uygulama çerçeveleri](../articles/virtual-machines/linux/app-frameworks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e56a4-332">For more templates you can use, see [Azure Quickstart templates](https://azure.microsoft.com/documentation/templates/) and [Application frameworks using templates](../articles/virtual-machines/linux/app-frameworks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
