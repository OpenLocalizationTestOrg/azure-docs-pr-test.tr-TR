
* [<span data-ttu-id="b91fc-101">Azure’da hızlı bir şekilde sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="b91fc-101">Quick-create a virtual machine in Azure</span></span>](#quick-create-a-vm-in-azure)
* [<span data-ttu-id="b91fc-102">Azure’da bir sanal makineyi şablondan dağıtma</span><span class="sxs-lookup"><span data-stu-id="b91fc-102">Deploy a virtual machine in Azure from a template</span></span>](#deploy-a-vm-in-azure-from-a-template)
* [<span data-ttu-id="b91fc-103">Özel bir görüntüden sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="b91fc-103">Create a virtual machine from a custom image</span></span>](#create-a-custom-vm-image)
* [<span data-ttu-id="b91fc-104">Sanal ağ ve yük dengeleyicisi kullanan bir sanal makine dağıtma</span><span class="sxs-lookup"><span data-stu-id="b91fc-104">Deploy a virtual machine that uses a virtual network and a load balancer</span></span>](#deploy-a-multi-vm-application-that-uses-a-virtual-network-and-an-external-load-balancer)
* [<span data-ttu-id="b91fc-105">Kaynak grubunu kaldırma</span><span class="sxs-lookup"><span data-stu-id="b91fc-105">Remove a resource group</span></span>](#remove-a-resource-group)
* [<span data-ttu-id="b91fc-106">Bir kaynak grubu dağıtımı için Hello günlüklerini göster</span><span class="sxs-lookup"><span data-stu-id="b91fc-106">Show hello log for a resource group deployment</span></span>](#show-the-log-for-a-resource-group-deployment)
* [<span data-ttu-id="b91fc-107">Bir sanal makine hakkında bilgi görüntüleme</span><span class="sxs-lookup"><span data-stu-id="b91fc-107">Display information about a virtual machine</span></span>](#display-information-about-a-virtual-machine)
* [<span data-ttu-id="b91fc-108">Tooa Linux tabanlı sanal makineye bağlanmak</span><span class="sxs-lookup"><span data-stu-id="b91fc-108">Connect tooa Linux-based virtual machine</span></span>](#log-on-to-a-linux-based-virtual-machine)
* [<span data-ttu-id="b91fc-109">Sanal makineyi durdurma</span><span class="sxs-lookup"><span data-stu-id="b91fc-109">Stop a virtual machine</span></span>](#stop-a-virtual-machine)
* [<span data-ttu-id="b91fc-110">Sanal makineyi başlatma</span><span class="sxs-lookup"><span data-stu-id="b91fc-110">Start a virtual machine</span></span>](#start-a-virtual-machine)
* [<span data-ttu-id="b91fc-111">Veri diski ekleme</span><span class="sxs-lookup"><span data-stu-id="b91fc-111">Attach a data disk</span></span>](#attach-a-data-disk)

## <a name="getting-ready"></a><span data-ttu-id="b91fc-112">Hazırlanma</span><span class="sxs-lookup"><span data-stu-id="b91fc-112">Getting ready</span></span>
<span data-ttu-id="b91fc-113">Hello Azure CLI ile Azure kaynak gruplarını kullanabilmeniz için önce toohave hello sağ Azure CLI Sürüm ve bir Azure hesabı gerekir.</span><span class="sxs-lookup"><span data-stu-id="b91fc-113">Before you can use hello Azure CLI with Azure resource groups, you need toohave hello right Azure CLI version and an Azure account.</span></span> <span data-ttu-id="b91fc-114">Hello Azure CLI yoksa [yüklemek](../articles/cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="b91fc-114">If you don't have hello Azure CLI, [install it](../articles/cli-install-nodejs.md).</span></span>

### <a name="update-your-azure-cli-version-too090-or-later"></a><span data-ttu-id="b91fc-115">Azure CLI Sürüm too0.9.0 güncelleştirmek veya daha yenisi</span><span class="sxs-lookup"><span data-stu-id="b91fc-115">Update your Azure CLI version too0.9.0 or later</span></span>
<span data-ttu-id="b91fc-116">Tür `azure --version` toosee yüklü sürüm 0.9.0'dan zaten var olup olmadığını veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="b91fc-116">Type `azure --version` toosee whether you have already installed version 0.9.0 or later.</span></span>

```azurecli
azure --version
0.9.0 (node: 0.10.25)
```

<span data-ttu-id="b91fc-117">Aşağıdakilerden birini kullanarak, sürüm 0.9.0'dan değilse veya daha sonra tooupdate ihtiyacınız yerel yükleyicileri hello aracılığıyla veya **npm** yazarak `npm update -g azure-cli`.</span><span class="sxs-lookup"><span data-stu-id="b91fc-117">If your version is not 0.9.0 or later, you need tooupdate it by using one of hello native installers or through **npm** by typing `npm update -g azure-cli`.</span></span>

<span data-ttu-id="b91fc-118">Merhaba aşağıdakileri kullanarak Docker kapsayıcısı Azure CLI çalıştırabilirsiniz [Docker görüntü](https://registry.hub.docker.com/u/microsoft/azure-cli/).</span><span class="sxs-lookup"><span data-stu-id="b91fc-118">You can also run Azure CLI as a Docker container by using hello following [Docker image](https://registry.hub.docker.com/u/microsoft/azure-cli/).</span></span> <span data-ttu-id="b91fc-119">Docker ana bilgisayardan hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="b91fc-119">From a Docker host, run hello following command:</span></span>

```bash
docker run -it microsoft/azure-cli
```

### <a name="set-your-azure-account-and-subscription"></a><span data-ttu-id="b91fc-120">Azure hesabınızı ve aboneliğinizi ayarlama</span><span class="sxs-lookup"><span data-stu-id="b91fc-120">Set your Azure account and subscription</span></span>
<span data-ttu-id="b91fc-121">Henüz bir Azure aboneliğiniz olmamasına rağmen bir MSDN aboneliğiniz varsa [MSDN abone avantajlarınızı](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b91fc-121">If you don't already have an Azure subscription but you do have an MSDN subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span> <span data-ttu-id="b91fc-122">Veya [ücretsiz deneme sürümü](https://azure.microsoft.com/pricing/free-trial/) için kaydolabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b91fc-122">Or you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

<span data-ttu-id="b91fc-123">Şimdi [tooyour Azure hesabı etkileşimli olarak oturum](../articles/xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login) yazarak `azure login` ve etkileşimli oturum açma deneyimi tooyour Azure hesabı için hello ister.</span><span class="sxs-lookup"><span data-stu-id="b91fc-123">Now [log in tooyour Azure account interactively](../articles/xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login) by typing `azure login` and following hello prompts for an interactive login experience tooyour Azure account.</span></span> 

> [!NOTE]
> <span data-ttu-id="b91fc-124">Bir iş veya Okul kimlik ve iki faktörlü kimlik doğrulaması etkin sahip değilse, yapabilecekleriniz biliyorsanız **de** kullanmak `azure login -u` hello yanı sıra iş veya Okul kimliği toolog *olmadan* etkileşimli oturum.</span><span class="sxs-lookup"><span data-stu-id="b91fc-124">If you have a work or school ID and you know you do not have two-factor authentication enabled, you can **also** use `azure login -u` along with hello work or school ID toolog in *without* an interactive session.</span></span> <span data-ttu-id="b91fc-125">Bir iş veya Okul kimliği yok, şunları yapabilirsiniz [bir iş veya Okul kimlik kişisel Microsoft hesabınızı oluşturma](../articles/virtual-machines/windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) hello toolog aynı şekilde.</span><span class="sxs-lookup"><span data-stu-id="b91fc-125">If you don't have a work or school ID, you can [create a work or school id from your personal Microsoft account](../articles/virtual-machines/windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toolog in hello same way.</span></span>
>
>

<span data-ttu-id="b91fc-126">Hesabınızın birden fazla aboneliği olabilir.</span><span class="sxs-lookup"><span data-stu-id="b91fc-126">Your account may have more than one subscription.</span></span> <span data-ttu-id="b91fc-127">`azure account list` yazarak aboneliklerinizin aşağıdakine benzer bir listesini görüntüleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b91fc-127">You can list your subscriptions by typing `azure account list`, which might look something like this:</span></span>

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

<span data-ttu-id="b91fc-128">Merhaba aşağıdakileri yazarak hello geçerli Azure aboneliği ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b91fc-128">You can set hello current Azure subscription by typing hello following.</span></span> <span data-ttu-id="b91fc-129">Toomanage istediğiniz hello kaynaklara sahip hello abonelik adı veya hello kimliği kullanın.</span><span class="sxs-lookup"><span data-stu-id="b91fc-129">Use hello subscription name or hello ID that has hello resources you want toomanage.</span></span>

```azurecli
azure account set <subscription name or ID> true
```

### <a name="switch-toohello-azure-cli-resource-group-mode"></a><span data-ttu-id="b91fc-130">Toohello Azure CLI kaynak grubu moduna geç</span><span class="sxs-lookup"><span data-stu-id="b91fc-130">Switch toohello Azure CLI resource group mode</span></span>
<span data-ttu-id="b91fc-131">Varsayılan olarak, hello Azure CLI hello Hizmet Yönetimi modunda başlatır (**asm** modu).</span><span class="sxs-lookup"><span data-stu-id="b91fc-131">By default, hello Azure CLI starts in hello service management mode (**asm** mode).</span></span> <span data-ttu-id="b91fc-132">Tooswitch tooresource Grup modu aşağıdaki hello yazın.</span><span class="sxs-lookup"><span data-stu-id="b91fc-132">Type hello following tooswitch tooresource group mode.</span></span>

```azurecli
azure config mode arm
```

## <a name="understanding-azure-resource-templates-and-resource-groups"></a><span data-ttu-id="b91fc-133">Azure kaynak şablonlarını ve kaynak gruplarını anlama</span><span class="sxs-lookup"><span data-stu-id="b91fc-133">Understanding Azure resource templates and resource groups</span></span>
<span data-ttu-id="b91fc-134">Çoğu uygulama farklı kaynak türlerinin bir birleşiminden oluşturulur (bir veya daha fazla VM ve depolama hesabı, bir SQL veritabanı, bir sanal ağ ya da içerik teslim ağı gibi).</span><span class="sxs-lookup"><span data-stu-id="b91fc-134">Most applications are built from a combination of different resource types (such as one or more VMs and storage accounts, a SQL database, a virtual network, or a content delivery network).</span></span> <span data-ttu-id="b91fc-135">Varsayılan Azure Hizmet Yönetimi API hello ve hello Klasik Azure portalı bu öğeler hizmeti tarafından bir yaklaşım kullanarak gösterilir.</span><span class="sxs-lookup"><span data-stu-id="b91fc-135">hello default Azure service management API and hello Azure classic portal represented these items by using a service-by-service approach.</span></span> <span data-ttu-id="b91fc-136">Bu yaklaşım toodeploy gerektirir ve hello ayrı ayrı hizmetlerini tek tek yönetme (veya bunu diğer araçları Bul), dağıtım tek bir mantıksal birim olarak değil.</span><span class="sxs-lookup"><span data-stu-id="b91fc-136">This approach requires you toodeploy and manage hello individual services individually (or find other tools that do so), and not as a single logical unit of deployment.</span></span>

<span data-ttu-id="b91fc-137">*Azure Resource Manager şablonları*, ancak, toodeploy mümkün kılar ve bildirim temelli bir şekilde bir mantıksal dağıtım birimi olarak farklı bu kaynakları yönetin.</span><span class="sxs-lookup"><span data-stu-id="b91fc-137">*Azure Resource Manager templates*, however, make it possible for you toodeploy and manage these different resources as one logical deployment unit in a declarative fashion.</span></span> <span data-ttu-id="b91fc-138">İmperatively Azure hangi toodeploy bir komut sonra başka bir belirten, yerine tüm bir JSON dosyası--tüm hello kaynakları ve ilişkili yapılandırma ve dağıtım parametreleri--dağıtımınızda açıklamak ve biri olarak bu kaynakları Azure toodeploy söyleyin Grup.</span><span class="sxs-lookup"><span data-stu-id="b91fc-138">Instead of imperatively telling Azure what toodeploy one command after another, you describe your entire deployment in a JSON file -- all of hello resources and associated configuration and deployment parameters -- and tell Azure toodeploy those resources as one group.</span></span>

<span data-ttu-id="b91fc-139">Ardından hello yönetebilmeniz için Azure CLI kaynak yönetimi komutları kullanarak hello grubun kaynakları genel yaşam döngüsünü:</span><span class="sxs-lookup"><span data-stu-id="b91fc-139">You can then manage hello overall life cycle of hello group's resources by using Azure CLI resource management commands to:</span></span>

* <span data-ttu-id="b91fc-140">Durdurun, başlatın veya hello grubundaki hello kaynakların tümünü bir defada silme.</span><span class="sxs-lookup"><span data-stu-id="b91fc-140">Stop, start, or delete all of hello resources within hello group at once.</span></span>
* <span data-ttu-id="b91fc-141">Rol tabanlı erişim denetimi (RBAC) kuralları toolock güvenlik izinleri aşağı üzerlerinde uygulayın.</span><span class="sxs-lookup"><span data-stu-id="b91fc-141">Apply Role-Based Access Control (RBAC) rules toolock down security permissions on them.</span></span>
* <span data-ttu-id="b91fc-142">İşlemleri denetleme.</span><span class="sxs-lookup"><span data-stu-id="b91fc-142">Audit operations.</span></span>
* <span data-ttu-id="b91fc-143">Daha iyi izleme için ek meta verilerle kaynakları etiketleme.</span><span class="sxs-lookup"><span data-stu-id="b91fc-143">Tag resources with additional metadata for better tracking.</span></span>

<span data-ttu-id="b91fc-144">Birçok Azure kaynak gruplarını ve bunlar için hello yapabilecekleriniz hakkında daha fazla bilgi edinebilirsiniz [Azure Resource Manager'a genel bakış](../articles/azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b91fc-144">You can learn lots more about Azure resource groups and what they can do for you in hello [Azure Resource Manager overview](../articles/azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="b91fc-145">Şablon yazmak istiyorsanız bkz. [Azure Resource Manager şablonları yazma](../articles/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="b91fc-145">If you're interested in authoring templates, see [Authoring Azure Resource Manager templates](../articles/resource-group-authoring-templates.md).</span></span>

## <span data-ttu-id="b91fc-146"><a id="quick-create-a-vm-in-azure"></a>Görev: Azure’da hızlı bir şekilde VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="b91fc-146"><a id="quick-create-a-vm-in-azure"></a>Task: Quick-create a VM in Azure</span></span>
<span data-ttu-id="b91fc-147">Gereksinim duyduğunuz, hangi görüntü bazen bildiğiniz ve, görüntü bir VM'den şimdi gerekir ve çok hello altyapı hakkında önemli değil--olabilir, tootest bir şey temiz bir VM'ye sahip.</span><span class="sxs-lookup"><span data-stu-id="b91fc-147">Sometimes you know what image you need, and you need a VM from that image right now and you don't care too much about hello infrastructure -- maybe you have tootest something on a clean VM.</span></span> <span data-ttu-id="b91fc-148">Ne zaman olan toouse hello istediğiniz `azure vm quick-create` komut ve bir VM ve alt yapısına hello bağımsız değişkenler gerekli toocreate geçirin.</span><span class="sxs-lookup"><span data-stu-id="b91fc-148">That's when you want toouse hello `azure vm quick-create` command, and pass hello arguments necessary toocreate a VM and its infrastructure.</span></span>

<span data-ttu-id="b91fc-149">İlk olarak kaynak grubunuzu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b91fc-149">First, create your resource group.</span></span>

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

<span data-ttu-id="b91fc-150">İkinci olarak, bir görüntü gereklidir.</span><span class="sxs-lookup"><span data-stu-id="b91fc-150">Second, you'll need an image.</span></span> <span data-ttu-id="b91fc-151">Resmin hello Azure CLI ile toofind bkz [gezinme ve PowerShell ve hello Azure CLI ile Azure sanal makine görüntüleri seçme](../articles/virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b91fc-151">toofind an image with hello Azure CLI, see [Navigating and selecting Azure virtual machine images with PowerShell and hello Azure CLI](../articles/virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="b91fc-152">Ancak bu makalede popüler görüntülerin kısa bir listesi verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="b91fc-152">But for this article, here's a short list of popular images.</span></span> <span data-ttu-id="b91fc-153">Bu hızlı oluşturma işlemi için CoreOS Kararlı görüntüsü kullanılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="b91fc-153">We'll use CoreOS's Stable image for this quick-create.</span></span>

> [!NOTE]
> <span data-ttu-id="b91fc-154">ComputeImageVersion için kısaca 'Son' parametresi hem hello şablon dili ve hello Azure CLI hello olarak sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b91fc-154">For ComputeImageVersion, you can also simply supply 'latest' as hello parameter in both hello template language and in hello Azure CLI.</span></span> <span data-ttu-id="b91fc-155">Bu, tooalways hello son ve düzeltme eki sürümü hello görüntü komut dosyaları veya şablonları toomodify gerek kalmadan kullandığınız olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="b91fc-155">This will allow you tooalways use hello latest and patched version of hello image without having toomodify your scripts or templates.</span></span> <span data-ttu-id="b91fc-156">Bu örnek aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="b91fc-156">This is shown below.</span></span>
>
>

| <span data-ttu-id="b91fc-157">PublisherName</span><span class="sxs-lookup"><span data-stu-id="b91fc-157">PublisherName</span></span> | <span data-ttu-id="b91fc-158">Sunduğu</span><span class="sxs-lookup"><span data-stu-id="b91fc-158">Offer</span></span> | <span data-ttu-id="b91fc-159">Sku</span><span class="sxs-lookup"><span data-stu-id="b91fc-159">Sku</span></span> | <span data-ttu-id="b91fc-160">Sürüm</span><span class="sxs-lookup"><span data-stu-id="b91fc-160">Version</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b91fc-161">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="b91fc-161">OpenLogic</span></span> |<span data-ttu-id="b91fc-162">CentOS</span><span class="sxs-lookup"><span data-stu-id="b91fc-162">CentOS</span></span> |<span data-ttu-id="b91fc-163">7</span><span class="sxs-lookup"><span data-stu-id="b91fc-163">7</span></span> |<span data-ttu-id="b91fc-164">7.0.201503</span><span class="sxs-lookup"><span data-stu-id="b91fc-164">7.0.201503</span></span> |
| <span data-ttu-id="b91fc-165">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="b91fc-165">OpenLogic</span></span> |<span data-ttu-id="b91fc-166">CentOS</span><span class="sxs-lookup"><span data-stu-id="b91fc-166">CentOS</span></span> |<span data-ttu-id="b91fc-167">7.1</span><span class="sxs-lookup"><span data-stu-id="b91fc-167">7.1</span></span> |<span data-ttu-id="b91fc-168">7.1.201504</span><span class="sxs-lookup"><span data-stu-id="b91fc-168">7.1.201504</span></span> |
| <span data-ttu-id="b91fc-169">CoreOS</span><span class="sxs-lookup"><span data-stu-id="b91fc-169">CoreOS</span></span> |<span data-ttu-id="b91fc-170">CoreOS</span><span class="sxs-lookup"><span data-stu-id="b91fc-170">CoreOS</span></span> |<span data-ttu-id="b91fc-171">Beta</span><span class="sxs-lookup"><span data-stu-id="b91fc-171">Beta</span></span> |<span data-ttu-id="b91fc-172">647.0.0</span><span class="sxs-lookup"><span data-stu-id="b91fc-172">647.0.0</span></span> |
| <span data-ttu-id="b91fc-173">CoreOS</span><span class="sxs-lookup"><span data-stu-id="b91fc-173">CoreOS</span></span> |<span data-ttu-id="b91fc-174">CoreOS</span><span class="sxs-lookup"><span data-stu-id="b91fc-174">CoreOS</span></span> |<span data-ttu-id="b91fc-175">Dengeli</span><span class="sxs-lookup"><span data-stu-id="b91fc-175">Stable</span></span> |<span data-ttu-id="b91fc-176">633.1.0</span><span class="sxs-lookup"><span data-stu-id="b91fc-176">633.1.0</span></span> |
| <span data-ttu-id="b91fc-177">MicrosoftDynamicsNAV</span><span class="sxs-lookup"><span data-stu-id="b91fc-177">MicrosoftDynamicsNAV</span></span> |<span data-ttu-id="b91fc-178">DynamicsNAV</span><span class="sxs-lookup"><span data-stu-id="b91fc-178">DynamicsNAV</span></span> |<span data-ttu-id="b91fc-179">2015</span><span class="sxs-lookup"><span data-stu-id="b91fc-179">2015</span></span> |<span data-ttu-id="b91fc-180">8.0.40459</span><span class="sxs-lookup"><span data-stu-id="b91fc-180">8.0.40459</span></span> |
| <span data-ttu-id="b91fc-181">MicrosoftSharePoint</span><span class="sxs-lookup"><span data-stu-id="b91fc-181">MicrosoftSharePoint</span></span> |<span data-ttu-id="b91fc-182">MicrosoftSharePointServer</span><span class="sxs-lookup"><span data-stu-id="b91fc-182">MicrosoftSharePointServer</span></span> |<span data-ttu-id="b91fc-183">2013</span><span class="sxs-lookup"><span data-stu-id="b91fc-183">2013</span></span> |<span data-ttu-id="b91fc-184">1.0.0</span><span class="sxs-lookup"><span data-stu-id="b91fc-184">1.0.0</span></span> |
| <span data-ttu-id="b91fc-185">msopentech</span><span class="sxs-lookup"><span data-stu-id="b91fc-185">msopentech</span></span> |<span data-ttu-id="b91fc-186">Oracle-Database-12c-Weblogic-Server-12c</span><span class="sxs-lookup"><span data-stu-id="b91fc-186">Oracle-Database-12c-Weblogic-Server-12c</span></span> |<span data-ttu-id="b91fc-187">Standart</span><span class="sxs-lookup"><span data-stu-id="b91fc-187">Standard</span></span> |<span data-ttu-id="b91fc-188">1.0.0</span><span class="sxs-lookup"><span data-stu-id="b91fc-188">1.0.0</span></span> |
| <span data-ttu-id="b91fc-189">msopentech</span><span class="sxs-lookup"><span data-stu-id="b91fc-189">msopentech</span></span> |<span data-ttu-id="b91fc-190">Oracle-Database-12c-Weblogic-Server-12c</span><span class="sxs-lookup"><span data-stu-id="b91fc-190">Oracle-Database-12c-Weblogic-Server-12c</span></span> |<span data-ttu-id="b91fc-191">Enterprise</span><span class="sxs-lookup"><span data-stu-id="b91fc-191">Enterprise</span></span> |<span data-ttu-id="b91fc-192">1.0.0</span><span class="sxs-lookup"><span data-stu-id="b91fc-192">1.0.0</span></span> |
| <span data-ttu-id="b91fc-193">MicrosoftSQLServer</span><span class="sxs-lookup"><span data-stu-id="b91fc-193">MicrosoftSQLServer</span></span> |<span data-ttu-id="b91fc-194">SQL2014-WS2012R2</span><span class="sxs-lookup"><span data-stu-id="b91fc-194">SQL2014-WS2012R2</span></span> |<span data-ttu-id="b91fc-195">Enterprise-Optimized-for-DW</span><span class="sxs-lookup"><span data-stu-id="b91fc-195">Enterprise-Optimized-for-DW</span></span> |<span data-ttu-id="b91fc-196">12.0.2430</span><span class="sxs-lookup"><span data-stu-id="b91fc-196">12.0.2430</span></span> |
| <span data-ttu-id="b91fc-197">MicrosoftSQLServer</span><span class="sxs-lookup"><span data-stu-id="b91fc-197">MicrosoftSQLServer</span></span> |<span data-ttu-id="b91fc-198">SQL2014-WS2012R2</span><span class="sxs-lookup"><span data-stu-id="b91fc-198">SQL2014-WS2012R2</span></span> |<span data-ttu-id="b91fc-199">Enterprise-Optimized-for-OLTP</span><span class="sxs-lookup"><span data-stu-id="b91fc-199">Enterprise-Optimized-for-OLTP</span></span> |<span data-ttu-id="b91fc-200">12.0.2430</span><span class="sxs-lookup"><span data-stu-id="b91fc-200">12.0.2430</span></span> |
| <span data-ttu-id="b91fc-201">Canonical</span><span class="sxs-lookup"><span data-stu-id="b91fc-201">Canonical</span></span> |<span data-ttu-id="b91fc-202">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="b91fc-202">UbuntuServer</span></span> |<span data-ttu-id="b91fc-203">12.04.5-LTS</span><span class="sxs-lookup"><span data-stu-id="b91fc-203">12.04.5-LTS</span></span> |<span data-ttu-id="b91fc-204">12.04.201504230</span><span class="sxs-lookup"><span data-stu-id="b91fc-204">12.04.201504230</span></span> |
| <span data-ttu-id="b91fc-205">Canonical</span><span class="sxs-lookup"><span data-stu-id="b91fc-205">Canonical</span></span> |<span data-ttu-id="b91fc-206">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="b91fc-206">UbuntuServer</span></span> |<span data-ttu-id="b91fc-207">14.04.2-LTS</span><span class="sxs-lookup"><span data-stu-id="b91fc-207">14.04.2-LTS</span></span> |<span data-ttu-id="b91fc-208">14.04.201503090</span><span class="sxs-lookup"><span data-stu-id="b91fc-208">14.04.201503090</span></span> |
| <span data-ttu-id="b91fc-209">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="b91fc-209">MicrosoftWindowsServer</span></span> |<span data-ttu-id="b91fc-210">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="b91fc-210">WindowsServer</span></span> |<span data-ttu-id="b91fc-211">2012-Datacenter</span><span class="sxs-lookup"><span data-stu-id="b91fc-211">2012-Datacenter</span></span> |<span data-ttu-id="b91fc-212">3.0.201503</span><span class="sxs-lookup"><span data-stu-id="b91fc-212">3.0.201503</span></span> |
| <span data-ttu-id="b91fc-213">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="b91fc-213">MicrosoftWindowsServer</span></span> |<span data-ttu-id="b91fc-214">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="b91fc-214">WindowsServer</span></span> |<span data-ttu-id="b91fc-215">2012-R2-Datacenter</span><span class="sxs-lookup"><span data-stu-id="b91fc-215">2012-R2-Datacenter</span></span> |<span data-ttu-id="b91fc-216">4.0.201503</span><span class="sxs-lookup"><span data-stu-id="b91fc-216">4.0.201503</span></span> |
| <span data-ttu-id="b91fc-217">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="b91fc-217">MicrosoftWindowsServer</span></span> |<span data-ttu-id="b91fc-218">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="b91fc-218">WindowsServer</span></span> |<span data-ttu-id="b91fc-219">Windows-Server-Technical-Preview</span><span class="sxs-lookup"><span data-stu-id="b91fc-219">Windows-Server-Technical-Preview</span></span> |<span data-ttu-id="b91fc-220">5.0.201504</span><span class="sxs-lookup"><span data-stu-id="b91fc-220">5.0.201504</span></span> |
| <span data-ttu-id="b91fc-221">MicrosoftWindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="b91fc-221">MicrosoftWindowsServerEssentials</span></span> |<span data-ttu-id="b91fc-222">WindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="b91fc-222">WindowsServerEssentials</span></span> |<span data-ttu-id="b91fc-223">WindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="b91fc-223">WindowsServerEssentials</span></span> |<span data-ttu-id="b91fc-224">1.0.141204</span><span class="sxs-lookup"><span data-stu-id="b91fc-224">1.0.141204</span></span> |
| <span data-ttu-id="b91fc-225">MicrosoftWindowsServerHPCPack</span><span class="sxs-lookup"><span data-stu-id="b91fc-225">MicrosoftWindowsServerHPCPack</span></span> |<span data-ttu-id="b91fc-226">WindowsServerHPCPack</span><span class="sxs-lookup"><span data-stu-id="b91fc-226">WindowsServerHPCPack</span></span> |<span data-ttu-id="b91fc-227">2012R2</span><span class="sxs-lookup"><span data-stu-id="b91fc-227">2012R2</span></span> |<span data-ttu-id="b91fc-228">4.3.4665</span><span class="sxs-lookup"><span data-stu-id="b91fc-228">4.3.4665</span></span> |

<span data-ttu-id="b91fc-229">Yalnızca hello girerek, VM oluşturma `azure vm quick-create` komut ve hazır hello ister.</span><span class="sxs-lookup"><span data-stu-id="b91fc-229">Just create your VM by entering hello `azure vm quick-create` command and being ready for hello prompts.</span></span> <span data-ttu-id="b91fc-230">Şuna benzer şekilde görünecektir:</span><span class="sxs-lookup"><span data-stu-id="b91fc-230">It should look something like this:</span></span>

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
+ Looking up hello VM "coreos"
info:    Using hello VM Size "Standard_A1"
info:    hello [OS, Data] Disk or image configuration requires storage account
+ Retrieving storage accounts
info:    Could not find any storage accounts in hello region "westus", trying toocreate new one
+ Creating storage account "cli9fd3fce49e9a9b3d14302" in "westus"
+ Looking up hello storage account cli9fd3fce49e9a9b3d14302
+ Looking up hello NIC "coreo-westu-1430261891570-nic"
info:    An nic with given name "coreo-westu-1430261891570-nic" not found, creating a new one
+ Looking up hello virtual network "coreo-westu-1430261891570-vnet"
info:    Preparing toocreate new virtual network and subnet
/ Creating a new virtual network "coreo-westu-1430261891570-vnet" [address prefix: "10.0.0.0/16"] with subnet "coreo-westu-1430261891570-sne+" [address prefix: "10.0.1.0/24"]
+ Looking up hello virtual network "coreo-westu-1430261891570-vnet"
+ Looking up hello subnet "coreo-westu-1430261891570-snet" under hello virtual network "coreo-westu-1430261891570-vnet"
info:    Found public ip parameters, trying toosetup PublicIP profile
+ Looking up hello public ip "coreo-westu-1430261891570-pip"
info:    PublicIP with given name "coreo-westu-1430261891570-pip" not found, creating a new one
+ Creating public ip "coreo-westu-1430261891570-pip"
+ Looking up hello public ip "coreo-westu-1430261891570-pip"
+ Creating NIC "coreo-westu-1430261891570-nic"
+ Looking up hello NIC "coreo-westu-1430261891570-nic"
+ Creating VM "coreos"
+ Looking up hello VM "coreos"
+ Looking up hello NIC "coreo-westu-1430261891570-nic"
+ Looking up hello public ip "coreo-westu-1430261891570-pip"
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

<span data-ttu-id="b91fc-231">Yeni VM’niz hazırdır.</span><span class="sxs-lookup"><span data-stu-id="b91fc-231">And away you go with your new VM.</span></span>

## <span data-ttu-id="b91fc-232"><a id="deploy-a-vm-in-azure-from-a-template"></a>Görev: Azure’da şablondan VM dağıtma</span><span class="sxs-lookup"><span data-stu-id="b91fc-232"><a id="deploy-a-vm-in-azure-from-a-template"></a>Task: Deploy a VM in Azure from a template</span></span>
<span data-ttu-id="b91fc-233">Azure CLI hello bir şablon kullanarak bu bölümleri toodeploy yeni bir Azure VM Hello yönergeleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="b91fc-233">Use hello instructions in these sections toodeploy a new Azure VM by using a template with hello Azure CLI.</span></span> <span data-ttu-id="b91fc-234">Bu şablon, yeni bir sanal ağ ile tek bir alt ağ ve farklı olarak, tek bir sanal makine oluşturur `azure vm quick-create`, tam olarak istediğiniz, toodescribe sağlar ve hatasız yineleyin.</span><span class="sxs-lookup"><span data-stu-id="b91fc-234">This template creates a single virtual machine in a new virtual network with a single subnet, and unlike `azure vm quick-create`, enables you toodescribe what you want precisely and repeat it without errors.</span></span> <span data-ttu-id="b91fc-235">Bu şablon aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="b91fc-235">Here's what this template creates:</span></span>

![](./media/virtual-machines-common-cli-deploy-templates/new-vm.png)

### <a name="step-1-examine-hello-json-file-for-hello-template-parameters"></a><span data-ttu-id="b91fc-236">1. adım: hello şablon parametreleri için hello JSON dosyasını inceleyin</span><span class="sxs-lookup"><span data-stu-id="b91fc-236">Step 1: Examine hello JSON file for hello template parameters</span></span>
<span data-ttu-id="b91fc-237">Burada, hello şablonunun hello JSON dosyasının hello içeriği bulunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="b91fc-237">Here are hello contents of hello JSON file for hello template.</span></span> <span data-ttu-id="b91fc-238">(Merhaba şablonu bulunan de [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-linux/azuredeploy.json).)</span><span class="sxs-lookup"><span data-stu-id="b91fc-238">(hello template is also located in [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-linux/azuredeploy.json).)</span></span>

<span data-ttu-id="b91fc-239">Merhaba Tasarımcısı, çok parametrelerden biri toogive seçilen veya olabilir daha sabit bir şablon oluşturarak yalnızca birkaç toooffer seçilen şekilde şablonları esnektir.</span><span class="sxs-lookup"><span data-stu-id="b91fc-239">Templates are flexible, so hello designer may have chosen toogive you lots of parameters or chosen toooffer only a few by creating a template that is more fixed.</span></span> <span data-ttu-id="b91fc-240">Sipariş toocollect hello bilgileri, parametre olarak toopass hello şablonu gerekir (Bu konuda sahip bir şablon satır içi aşağıda) hello şablon dosyasını açın ve hello inceleyin **parametreleri** değerleri.</span><span class="sxs-lookup"><span data-stu-id="b91fc-240">In order toocollect hello information you need toopass hello template as parameters, open hello template file (this topic has a template inline, below) and examine hello **parameters** values.</span></span>

<span data-ttu-id="b91fc-241">Bu durumda, hello şablonu için ister:</span><span class="sxs-lookup"><span data-stu-id="b91fc-241">In this case, hello template below will ask for:</span></span>

* <span data-ttu-id="b91fc-242">Benzersiz bir depolama hesabı adı.</span><span class="sxs-lookup"><span data-stu-id="b91fc-242">A unique storage account name.</span></span>
* <span data-ttu-id="b91fc-243">Merhaba VM için bir yönetici kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="b91fc-243">An admin user name for hello VM.</span></span>
* <span data-ttu-id="b91fc-244">Parola.</span><span class="sxs-lookup"><span data-stu-id="b91fc-244">A password.</span></span>
* <span data-ttu-id="b91fc-245">Hello world toouse dışında bir etki alanı adı.</span><span class="sxs-lookup"><span data-stu-id="b91fc-245">A domain name for hello outside world toouse.</span></span>
* <span data-ttu-id="b91fc-246">Ubuntu Server sürüm numarası -- ancak yalnızca bir listesini kabul eder.</span><span class="sxs-lookup"><span data-stu-id="b91fc-246">An Ubuntu Server version number -- but it will accept only one of a list.</span></span>

<span data-ttu-id="b91fc-247">[Kullanıcı adı ve parola gereksinimleri](../articles/virtual-machines/linux/faq.md#what-are-the-username-requirements-when-creating-a-vm) hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="b91fc-247">See more about [username and password requirements](../articles/virtual-machines/linux/faq.md#what-are-the-username-requirements-when-creating-a-vm).</span></span>

<span data-ttu-id="b91fc-248">Bu değerleri karar verdiğinizde bir grup için hazır toocreate olduğunuz ve Azure aboneliğinize bu şablonu dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b91fc-248">Once you decide on these values, you're ready toocreate a group for and deploy this template into your Azure subscription.</span></span>

```json
{
"$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
"contentVersion": "1.0.0.0",
"parameters": {
    "newStorageAccountName": {
    "type": "string",
    "metadata": {
        "description": "Unique DNS name for hello storage account where hello virtual machine's disks will be placed."
    }
    },
    "adminUsername": {
    "type": "string",
    "metadata": {
        "description": "User name for hello virtual machine."
    }
    },
    "adminPassword": {
    "type": "securestring",
    "metadata": {
        "description": "Password for hello virtual machine."
    }
    },
    "dnsNameForPublicIP": {
    "type": "string",
    "metadata": {
        "description": "Unique DNS name for hello public IP used tooaccess hello virtual machine."
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
        "description": "hello Ubuntu version for hello VM. This will pick a fully patched image of this given Ubuntu version. Allowed values: 12.04.5-LTS, 14.04.2-LTS, 15.04."
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

### <a name="step-2-create-hello-virtual-machine-by-using-hello-template"></a><span data-ttu-id="b91fc-249">2. adım: hello şablonu kullanarak hello sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="b91fc-249">Step 2: Create hello virtual machine by using hello template</span></span>
<span data-ttu-id="b91fc-250">Parametre değerlerinizi hazır olduktan sonra şablonu dağıtımınız için bir kaynak grubu oluşturun ve ardından hello şablonunu dağıtın.</span><span class="sxs-lookup"><span data-stu-id="b91fc-250">Once you have your parameter values ready, you must create a resource group for your template deployment and then deploy hello template.</span></span>

<span data-ttu-id="b91fc-251">toocreate hello kaynak grubu, türü `azure group create <group name> <location>` istediğiniz hello grup ve toodeploy istediğiniz hello veri merkezi konum hello adı.</span><span class="sxs-lookup"><span data-stu-id="b91fc-251">toocreate hello resource group, type `azure group create <group name> <location>` with hello name of hello group you want and hello datacenter location into which you want toodeploy.</span></span> <span data-ttu-id="b91fc-252">Bu işlem hızlı bir şekilde yapılır:</span><span class="sxs-lookup"><span data-stu-id="b91fc-252">This happens quickly:</span></span>

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

<span data-ttu-id="b91fc-253">Şimdi toocreate hello dağıtım, çağrı `azure group deployment create` ve geçirin:</span><span class="sxs-lookup"><span data-stu-id="b91fc-253">Now toocreate hello deployment, call `azure group deployment create` and pass:</span></span>

* <span data-ttu-id="b91fc-254">(JSON şablonu tooa yerel dosya yukarıda hello kaydettiyseniz) hello şablon dosyası.</span><span class="sxs-lookup"><span data-stu-id="b91fc-254">hello template file (if you saved hello above JSON template tooa local file).</span></span>
* <span data-ttu-id="b91fc-255">Bir şablonu (Merhaba dosyasına GitHub ya da başka bir web adresini toopoint istiyorsanız) URI.</span><span class="sxs-lookup"><span data-stu-id="b91fc-255">A template URI (if you want toopoint at hello file in GitHub or some other web address).</span></span>
* <span data-ttu-id="b91fc-256">Merhaba kaynak grubu toodeploy istiyor.</span><span class="sxs-lookup"><span data-stu-id="b91fc-256">hello resource group into which you want toodeploy.</span></span>
* <span data-ttu-id="b91fc-257">İsteğe bağlı dağıtım adı.</span><span class="sxs-lookup"><span data-stu-id="b91fc-257">An optional deployment name.</span></span>

<span data-ttu-id="b91fc-258">Merhaba JSON dosyasının hello "parametreleri" bölümüne parametrelerinin istendiğinde toosupply hello değerleri olacaktır.</span><span class="sxs-lookup"><span data-stu-id="b91fc-258">You will be prompted toosupply hello values of parameters in hello "parameters" section of hello JSON file.</span></span> <span data-ttu-id="b91fc-259">Tüm hello parametre değerlerini belirledikten sonra dağıtımınız başlar.</span><span class="sxs-lookup"><span data-stu-id="b91fc-259">When you have specified all hello parameter values, your deployment will begin.</span></span>

<span data-ttu-id="b91fc-260">Örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="b91fc-260">Here is an example:</span></span>

```azurecli
azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-linux/azuredeploy.json myResourceGroup firstDeployment
info:    Executing command group deployment create
info:    Supply values for hello following parameters
newStorageAccountName: storageaccount
adminUsername: ops
adminPassword: password
dnsNameForPublicIP: newdomainname
```

<span data-ttu-id="b91fc-261">Tür bilgileri aşağıdaki hello alırsınız:</span><span class="sxs-lookup"><span data-stu-id="b91fc-261">You will receive hello following type of information:</span></span>

```azurecli
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "firstDeployment"
+ Registering providers
info:    Registering provider microsoft.storage
info:    Registering provider microsoft.network
info:    Registering provider microsoft.compute
+ Waiting for deployment toocomplete
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


## <span data-ttu-id="b91fc-262"><a id="create-a-custom-vm-image"></a>Görev: Özel bir VM görüntüsü oluşturma</span><span class="sxs-lookup"><span data-stu-id="b91fc-262"><a id="create-a-custom-vm-image"></a>Task: Create a custom VM image</span></span>
<span data-ttu-id="b91fc-263">Hello temel kullanım şablonlarının yukarıdaki gördünüz, böylece biz benzer yönergeler toocreate özel bir VM Azure belirli .vhd dosyasından aracılığıyla bir şablon kullanarak artık kullanarak Azure CLI hello.</span><span class="sxs-lookup"><span data-stu-id="b91fc-263">You've seen hello basic usage of templates above, so now we can use similar instructions toocreate a custom VM from a specific .vhd file in Azure by using a template via hello Azure CLI.</span></span> <span data-ttu-id="b91fc-264">Merhaba burada bu şablon bir belirtilen sanal sabit diskten (VHD) tek bir sanal makine oluşturur farktır.</span><span class="sxs-lookup"><span data-stu-id="b91fc-264">hello difference here is that this template creates a single virtual machine from a specified virtual hard disk (VHD).</span></span>

### <a name="step-1-examine-hello-json-file-for-hello-template"></a><span data-ttu-id="b91fc-265">1. adım: hello şablonu için başlangıç JSON dosyasını inceleyin</span><span class="sxs-lookup"><span data-stu-id="b91fc-265">Step 1: Examine hello JSON file for hello template</span></span>
<span data-ttu-id="b91fc-266">Bu bölümde örnek olarak kullanılmıştır hello şablonu için başlangıç JSON dosyası hello içeriğini aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="b91fc-266">Here are hello contents of hello JSON file for hello template that this section uses as an example.</span></span> <span data-ttu-id="b91fc-267">(Merhaba şablonu bulunan de [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json).)</span><span class="sxs-lookup"><span data-stu-id="b91fc-267">(hello template is also located in [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json).)</span></span>

<span data-ttu-id="b91fc-268">Yeniden, varsayılan değerleri olmayan hello parametrelerini tooenter istediğiniz toofind hello değerler gerekir.</span><span class="sxs-lookup"><span data-stu-id="b91fc-268">Again, you will need toofind hello values you want tooenter for hello parameters that do not have default values.</span></span> <span data-ttu-id="b91fc-269">Merhaba çalıştırdığınızda `azure group deployment create` komutunu hello Azure CLI, bu değerler, tooenter sorar.</span><span class="sxs-lookup"><span data-stu-id="b91fc-269">When you run hello `azure group deployment create` command, hello Azure CLI will prompt you tooenter those values.</span></span>

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

### <a name="step-2-obtain-hello-vhd"></a><span data-ttu-id="b91fc-270">Adım 2: hello VHD alın</span><span class="sxs-lookup"><span data-stu-id="b91fc-270">Step 2: Obtain hello VHD</span></span>
<span data-ttu-id="b91fc-271">Bunun için bir .vhd dosyasının gerekli olduğu açıktır.</span><span class="sxs-lookup"><span data-stu-id="b91fc-271">Obviously, you'll need a .vhd for this.</span></span> <span data-ttu-id="b91fc-272">Azure’da zaten sahip olduğunuz dosyayı kullanabilir veya bir tane yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b91fc-272">You can use one you already have in Azure, or you can upload one.</span></span>

<span data-ttu-id="b91fc-273">Bir Windows tabanlı sanal makine için bkz: [oluşturma ve karşıya yükleme Windows Server VHD tooAzure](../articles/virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b91fc-273">For a Windows-based virtual machine, see [Create and upload a Windows Server VHD tooAzure](../articles/virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="b91fc-274">Linux tabanlı sanal makine için bkz: [oluşturma ve hello Linux işletim sistemini içeren bir sanal sabit disk karşıya](../articles/virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b91fc-274">For a Linux-based virtual machine, see [Creating and uploading a virtual hard disk that contains hello Linux operating system](../articles/virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

### <a name="step-3-create-hello-virtual-machine-by-using-hello-template"></a><span data-ttu-id="b91fc-275">3. adım: hello şablonu kullanarak hello sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="b91fc-275">Step 3: Create hello virtual machine by using hello template</span></span>
<span data-ttu-id="b91fc-276">Şimdi hazır toocreate hello .vhd üzerinde dayalı yeni bir sanal makine demektir.</span><span class="sxs-lookup"><span data-stu-id="b91fc-276">Now you're ready toocreate a new virtual machine based on hello .vhd.</span></span> <span data-ttu-id="b91fc-277">Kullanarak, bir grup toodeploy oluşturma `azure group create <location>`:</span><span class="sxs-lookup"><span data-stu-id="b91fc-277">Create a group toodeploy into, by using `azure group create <location>`:</span></span>

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

<span data-ttu-id="b91fc-278">Sonra hello kullanarak hello dağıtım oluşturun `--template-uri` seçeneği toocall doğrudan hello şablonunda (veya hello kullanabilirsiniz `--template-file` seçeneği toouse yerel olarak kaydettiğiniz dosya).</span><span class="sxs-lookup"><span data-stu-id="b91fc-278">Then create hello deployment by using hello `--template-uri` option toocall in hello template directly (or you can use hello `--template-file` option toouse a file that you have saved locally).</span></span> <span data-ttu-id="b91fc-279">Merhaba şablonunda belirtilen Varsayılanları olduğundan, yalnızca birkaç için istenir unutmayın.</span><span class="sxs-lookup"><span data-stu-id="b91fc-279">Note that because hello template has defaults specified, you are prompted for only a few things.</span></span> <span data-ttu-id="b91fc-280">Merhaba şablonu farklı yerlerde dağıtırsanız, bazı adlandırma çakışmaları hello varsayılan değerlerle (oluşturduğunuz özellikle hello DNS adı) ortaya bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b91fc-280">If you deploy hello template in different places, you may find that some naming collisions occur with hello default values (particularly hello DNS name you create).</span></span>

```azurecli
azure group deployment create \
> --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json \
> myResourceGroup \
> customVhdDeployment
info:    Executing command group deployment create
info:    Supply values for hello following parameters
adminUserName: ops
adminPassword: password
osType: linux
subscriptionId: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```

<span data-ttu-id="b91fc-281">Çıktı hello aşağıdaki şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="b91fc-281">Output looks something like hello following:</span></span>

```azurecli
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "customVhdDeployment"
+ Registering providers
info:    Registering provider microsoft.network
info:    Registering provider microsoft.compute
+ Waiting for deployment toocomplete
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

## <span data-ttu-id="b91fc-282"><a id="deploy-a-multi-vm-application-that-uses-a-virtual-network-and-an-external-load-balancer"></a>Görev: Sanal ağ ve dış yük dengeleyici kullanan çok sanal makineli uygulama dağıtma</span><span class="sxs-lookup"><span data-stu-id="b91fc-282"><a id="deploy-a-multi-vm-application-that-uses-a-virtual-network-and-an-external-load-balancer"></a>Task: Deploy a multi-VM application that uses a virtual network and an external load balancer</span></span>
<span data-ttu-id="b91fc-283">Bu şablon toocreate iki sanal makine bir yük dengeleyici altındaki sağlar ve bağlantı noktası 80 üzerinde bir Yük Dengeleme kuralı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="b91fc-283">This template allows you toocreate two virtual machines under a load balancer and configure a load-balancing rule on Port 80.</span></span> <span data-ttu-id="b91fc-284">Bu şablon ayrıca bir depolama hesabı, sanal ağ, genel IP adresi, kullanılabilirlik kümesi ve ağ arabirimleri dağıtır.</span><span class="sxs-lookup"><span data-stu-id="b91fc-284">This template also deploys a storage account, virtual network, public IP address, availability set, and network interfaces.</span></span>

![](./media/virtual-machines-common-cli-deploy-templates/multivmextlb.png)

<span data-ttu-id="b91fc-285">Bu adımları toodeploy hello GitHub şablonu deposunu Azure PowerShell komutları aracılığıyla bir Resource Manager şablonu kullanarak bir sanal ağ ve bir yük dengeleyici kullanan bir çoklu VM uygulamayı izleyin.</span><span class="sxs-lookup"><span data-stu-id="b91fc-285">Follow these steps toodeploy a multi-VM application that uses a virtual network and a load balancer by using a Resource Manager template in hello GitHub template repository via Azure PowerShell commands.</span></span>

### <a name="step-1-examine-hello-json-file-for-hello-template"></a><span data-ttu-id="b91fc-286">1. adım: hello şablonu için başlangıç JSON dosyasını inceleyin</span><span class="sxs-lookup"><span data-stu-id="b91fc-286">Step 1: Examine hello JSON file for hello template</span></span>
<span data-ttu-id="b91fc-287">Burada, hello şablonunun hello JSON dosyasının hello içeriği bulunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="b91fc-287">Here are hello contents of hello JSON file for hello template.</span></span> <span data-ttu-id="b91fc-288">Merhaba en son sürüm, isterseniz bunu bulunduktan [şablonları için hello GitHub deposunda](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="b91fc-288">If you want hello most recent version, it's located [at hello GitHub repository for templates](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json).</span></span> <span data-ttu-id="b91fc-289">Bu konuda hello kullanır `--template-uri` hello şablonu, ancak anahtar toocall hello de kullanabilir `--template-file` geçiş toopass yerel bir sürüm.</span><span class="sxs-lookup"><span data-stu-id="b91fc-289">This topic uses hello `--template-uri` switch toocall in hello template, but you can also use hello `--template-file` switch toopass a local version.</span></span>

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
                "description": "Prefix toouse for VM names"
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
                "description": "Size of hello VM"
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

### <a name="step-2-create-hello-deployment-by-using-hello-template"></a><span data-ttu-id="b91fc-290">2. adım: hello dağıtım hello şablonu kullanarak oluşturma</span><span class="sxs-lookup"><span data-stu-id="b91fc-290">Step 2: Create hello deployment by using hello template</span></span>
<span data-ttu-id="b91fc-291">Kullanarak hello şablonu için bir kaynak grubu oluşturma `azure group create <location>`.</span><span class="sxs-lookup"><span data-stu-id="b91fc-291">Create a resource group for hello template by using `azure group create <location>`.</span></span> <span data-ttu-id="b91fc-292">Sonra bu kaynak grubuna bir dağıtım kullanarak oluşturun `azure group deployment create` ve hello kaynak grubu geçirme, dağıtım adı geçirme ve varsayılan değerlere sahip değilse hello şablondaki parametreler için hello istemleri yanıtlama.</span><span class="sxs-lookup"><span data-stu-id="b91fc-292">Then, create a deployment into that resource group by using `azure group deployment create` and passing hello resource group, passing a deployment name, and answering hello prompts for parameters in hello template that did not have default values.</span></span>

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

<span data-ttu-id="b91fc-293">Şimdi hello kullan `azure group deployment create` komut ve hello `--template-uri` seçenek toodeploy hello şablonu.</span><span class="sxs-lookup"><span data-stu-id="b91fc-293">Now use hello `azure group deployment create` command and hello `--template-uri` option toodeploy hello template.</span></span> <span data-ttu-id="b91fc-294">Aşağıda gösterildiği gibi sizden istediğinde parametre değerlerini belirtmeye hazır olun.</span><span class="sxs-lookup"><span data-stu-id="b91fc-294">Be ready with your parameter values when it prompts you, as shown below.</span></span>

```azurecli
azure group deployment create \
> --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json \
> lbgroup \
> newdeployment
info:    Executing command group deployment create
info:    Supply values for hello following parameters
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
+ Waiting for deployment toocomplete
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

<span data-ttu-id="b91fc-295">Bu şablon bir Windows Server görüntüsünü dağıtır; ancak herhangi bir Linux görüntüsü ile kolayca değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="b91fc-295">Note that this template deploys a Windows Server image; however, it could easily be replaced by any Linux image.</span></span> <span data-ttu-id="b91fc-296">Toocreate Docker küme birden çok swarm yöneticilerine istiyorsunuz?</span><span class="sxs-lookup"><span data-stu-id="b91fc-296">Want toocreate a Docker cluster with multiple swarm managers?</span></span> <span data-ttu-id="b91fc-297">[Bunu yapabilirsiniz](https://azure.microsoft.com/documentation/templates/docker-swarm-cluster/).</span><span class="sxs-lookup"><span data-stu-id="b91fc-297">[You can do it](https://azure.microsoft.com/documentation/templates/docker-swarm-cluster/).</span></span>

## <span data-ttu-id="b91fc-298"><a id="remove-a-resource-group"></a>Görev: Kaynak grubunu kaldırma</span><span class="sxs-lookup"><span data-stu-id="b91fc-298"><a id="remove-a-resource-group"></a>Task: Remove a resource group</span></span>
<span data-ttu-id="b91fc-299">Tooa kaynak grubu yeniden dağıtabilirsiniz, ancak biriyle bittiğinde kullanarak silebilirsiniz unutmayın `azure group delete <group name>`.</span><span class="sxs-lookup"><span data-stu-id="b91fc-299">Remember that you can redeploy tooa resource group, but if you are done with one, you can delete it by using `azure group delete <group name>`.</span></span>

```azurecli
azure group delete myResourceGroup
info:    Executing command group delete
Delete resource group myResourceGroup? [y/n] y
+ Deleting resource group myResourceGroup
info:    group delete command OK
```

## <span data-ttu-id="b91fc-300"><a id="show-the-log-for-a-resource-group-deployment"></a>Görev: bir kaynak grubu dağıtımı için hello günlük Göster</span><span class="sxs-lookup"><span data-stu-id="b91fc-300"><a id="show-the-log-for-a-resource-group-deployment"></a>Task: Show hello log for a resource group deployment</span></span>
<span data-ttu-id="b91fc-301">Şablon oluştururken veya kullanırken bu işlem yaygın olarak yapılır.</span><span class="sxs-lookup"><span data-stu-id="b91fc-301">This one is common while you're creating or using templates.</span></span> <span data-ttu-id="b91fc-302">Merhaba çağrısı toodisplay hello Dağıtımı günlüklerini bir grup için `azure group log show <groupname>`, oldukça biraz neden oldu--veya bir şeyin kaydetmedi anlamak için yararlı olan bilgiler görüntüler.</span><span class="sxs-lookup"><span data-stu-id="b91fc-302">hello call toodisplay hello deployment logs for a group is `azure group log show <groupname>`, which displays quite a bit of information that's useful for understanding why something happened -- or didn't.</span></span> <span data-ttu-id="b91fc-303">(Dağıtımlarınızla ilgili daha fazla sorun giderme bilgisi ve sorunlar hakkında diğer bilgiler için bkz. [Azure Resource Manager ile yaygın Azure dağıtım hatalarını giderme](../articles/azure-resource-manager/resource-manager-common-deployment-errors.md).)</span><span class="sxs-lookup"><span data-stu-id="b91fc-303">(For more information on troubleshooting your deployments, as well as other information about issues, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](../articles/azure-resource-manager/resource-manager-common-deployment-errors.md).)</span></span>

<span data-ttu-id="b91fc-304">tootarget özel hatalar, örneğin, kullandığınız araçlarla **jq** tooquery şeyler biraz daha hassas bir şekilde, tek tek hangi hataları gibi ihtiyacınız toocorrect.</span><span class="sxs-lookup"><span data-stu-id="b91fc-304">tootarget specific failures, for example, you might use tools like **jq** tooquery things a bit more precisely, such as which individual failures you need toocorrect.</span></span> <span data-ttu-id="b91fc-305">Merhaba aşağıdaki örnek kullanır **jq** bir dağıtım oturum için tooparse **lbgroup**, hataları arayanlar.</span><span class="sxs-lookup"><span data-stu-id="b91fc-305">hello following example uses **jq** tooparse a deployment log for **lbgroup**, looking for failures.</span></span>

```azurecli
azure group log show lbgroup -l --json | jq '.[] | select(.status.value == "Failed") | .properties'
```
<span data-ttu-id="b91fc-306">Neyin yanlış gittiğini hızlıca bulabilir, düzeltebilir ve yeniden deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b91fc-306">You can discover very quickly what went wrong, fix, and retry.</span></span> <span data-ttu-id="b91fc-307">Durumda aşağıdaki hello hello şablon iki VM hello oluşturma hello .vhd üzerinde bir kilit oluşturulan aynı anda.</span><span class="sxs-lookup"><span data-stu-id="b91fc-307">In hello following case, hello template had been creating two VMs at hello same time, which created a lock on hello .vhd.</span></span> <span data-ttu-id="b91fc-308">(Biz hello şablonunu değiştiren sonra hello hızlı bir şekilde dağıtıldı.)</span><span class="sxs-lookup"><span data-stu-id="b91fc-308">(After we modified hello template, hello deployment succeeded quickly.)</span></span>

```json
{
    "statusCode": "Conflict",
    "statusMessage": "{\"status\":\"Failed\",\"error\":{\"code\":\"ResourceDeploymentFailure\",\"message\":\"hello resource operation completed with terminal provisioning state 'Failed'.\",\"details\":[{\"code\":\"AcquireDiskLeaseFailed\",\"message\":\"Failed tooacquire lease while creating disk 'osdisk' using blob with URI http://storage.blob.core.windows.net/vhds/osdisk.vhd.\"}]}}"
}
```

## <span data-ttu-id="b91fc-309"><a id="display-information-about-a-virtual-machine"></a>Görev: Bir sanal makine hakkında bilgi görüntüleme</span><span class="sxs-lookup"><span data-stu-id="b91fc-309"><a id="display-information-about-a-virtual-machine"></a>Task: Display information about a virtual machine</span></span>
<span data-ttu-id="b91fc-310">Hello kullanarak kaynak grubunuzdaki belirli VM'ler hakkındaki bilgileri görebilirsiniz `azure vm show <groupname> <vmname>` komutu.</span><span class="sxs-lookup"><span data-stu-id="b91fc-310">You can see information about specific VMs in your resource group by using hello `azure vm show <groupname> <vmname>` command.</span></span> <span data-ttu-id="b91fc-311">Grubunuzda birden fazla VM varsa, ilk grubundaki toolist hello VM'ler kullanarak gerekebilir `azure vm list <groupname>`.</span><span class="sxs-lookup"><span data-stu-id="b91fc-311">If you have more than one VM in your group, you might first need toolist hello VMs in a group by using `azure vm list <groupname>`.</span></span>

```azurecli
azure vm list zoo
info:    Executing command vm list
+ Getting virtual machines
data:    Name   ProvisioningState  Location  Size
data:    -----  -----------------  --------  -----------
data:    myVM0  Succeeded          westus    Standard_A1
data:    myVM1  Failed             westus    Standard_A1
```

<span data-ttu-id="b91fc-312">Ardından, myVM1 öğesini arayın:</span><span class="sxs-lookup"><span data-stu-id="b91fc-312">And then, looking up myVM1:</span></span>

```azurecli
azure vm show zoo myVM1
info:    Executing command vm show
+ Looking up hello VM "myVM1"
+ Looking up hello NIC "nic1"
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
> <span data-ttu-id="b91fc-313">Tooprogrammatically deposu istiyorsanız ve konsol komutlarınızı hello çıktısını işlemek gibi JSON ayrıştırma aracı toouse isteyebilirsiniz  **[jq](https://github.com/stedolan/jq)**  veya  **[jsawk](https://github.com/micha/jsawk)** , ya da hello görev için iyi dil kitaplıkları.</span><span class="sxs-lookup"><span data-stu-id="b91fc-313">If you want tooprogrammatically store and manipulate hello output of your console commands, you may want toouse a JSON parsing tool such as **[jq](https://github.com/stedolan/jq)** or **[jsawk](https://github.com/micha/jsawk)**, or language libraries that are good for hello task.</span></span>
>
>

## <span data-ttu-id="b91fc-314"><a id="log-on-to-a-linux-based-virtual-machine"></a>Görev: tooa Linux tabanlı sanal makinede oturum açın</span><span class="sxs-lookup"><span data-stu-id="b91fc-314"><a id="log-on-to-a-linux-based-virtual-machine"></a>Task: Log on tooa Linux-based virtual machine</span></span>
<span data-ttu-id="b91fc-315">Genellikle bağlı toothrough SSH Linux makinelerdir.</span><span class="sxs-lookup"><span data-stu-id="b91fc-315">Typically Linux machines are connected toothrough SSH.</span></span> <span data-ttu-id="b91fc-316">Daha fazla bilgi için bkz: [nasıl toouse Linux Azure üzerinde SSH](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b91fc-316">For more information, see [How toouse SSH with Linux on Azure](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <span data-ttu-id="b91fc-317"><a id="stop-a-virtual-machine"></a>Görev: VM durdurma</span><span class="sxs-lookup"><span data-stu-id="b91fc-317"><a id="stop-a-virtual-machine"></a>Task: Stop a VM</span></span>
<span data-ttu-id="b91fc-318">Şu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="b91fc-318">Run this command:</span></span>

```azurecli
azure vm stop <group name> <virtual machine name>
```

> [!IMPORTANT]
> <span data-ttu-id="b91fc-319">Bu durumda bu parametre tookeep hello sanal IP (VIP) hello vnet'in kullanın, vnet içinde son VM hello.</span><span class="sxs-lookup"><span data-stu-id="b91fc-319">Use this parameter tookeep hello virtual IP (VIP) of hello vnet in case it's hello last VM in that vnet.</span></span> <br><br> <span data-ttu-id="b91fc-320">Merhaba kullanırsanız `StayProvisioned` parametresi, hala hello VM için faturalandırılırsınız.</span><span class="sxs-lookup"><span data-stu-id="b91fc-320">If you use hello `StayProvisioned` parameter, you'll still be billed for hello VM.</span></span>
>
>

## <span data-ttu-id="b91fc-321"><a id="start-a-virtual-machine"></a>Görev: VM başlatma</span><span class="sxs-lookup"><span data-stu-id="b91fc-321"><a id="start-a-virtual-machine"></a>Task: Start a VM</span></span>
<span data-ttu-id="b91fc-322">Şu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="b91fc-322">Run this command:</span></span>

```azurecli
azure vm start <group name> <virtual machine name>
```

## <span data-ttu-id="b91fc-323"><a id="attach-a-data-disk"></a>Görev: Veri diski ekleme</span><span class="sxs-lookup"><span data-stu-id="b91fc-323"><a id="attach-a-data-disk"></a>Task: Attach a data disk</span></span>
<span data-ttu-id="b91fc-324">Ayrıca tooattach yeni bir disk veya bir içeren olup olmadığını toodecide gerekir veri.</span><span class="sxs-lookup"><span data-stu-id="b91fc-324">You'll also need toodecide whether tooattach a new disk or one that contains data.</span></span> <span data-ttu-id="b91fc-325">Yeni bir disk hello komutu hello .vhd dosyası oluşturur ve bunları hello ekler aynı komutu.</span><span class="sxs-lookup"><span data-stu-id="b91fc-325">For a new disk, hello command creates hello .vhd file and attaches it in hello same command.</span></span>

<span data-ttu-id="b91fc-326">Yeni bir disk tooattach bu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="b91fc-326">tooattach a new disk, run this command:</span></span>

```azurecli
    azure vm disk attach-new <resource-group> <vm-name> <size-in-gb>
```

<span data-ttu-id="b91fc-327">Varolan bir veri diski tooattach bu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="b91fc-327">tooattach an existing data disk, run this command:</span></span>

```azurecli
azure vm disk attach <resource-group> <vm-name> [vhd-url]
```

<span data-ttu-id="b91fc-328">Ardından Linux normalde yaptığınız gibi toomount hello disk gerekir.</span><span class="sxs-lookup"><span data-stu-id="b91fc-328">Then you'll need toomount hello disk, as you normally would in Linux.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b91fc-329">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b91fc-329">Next steps</span></span>
<span data-ttu-id="b91fc-330">Merhaba ile Azure CLI kullanımı çok daha fazla örnekleri için **arm** modu, bkz: [kullanma hello Mac, Linux ve Windows Azure Resource Manager ile Azure CLI](../articles/xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="b91fc-330">For far more examples of Azure CLI usage with hello **arm** mode, see [Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](../articles/xplat-cli-azure-resource-manager.md).</span></span> <span data-ttu-id="b91fc-331">Azure kaynaklarını ve bunların kavramları hakkında daha fazla toolearn bkz [Azure Resource Manager'a genel bakış](../articles/azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b91fc-331">toolearn more about Azure resources and their concepts, see [Azure Resource Manager overview](../articles/azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="b91fc-332">Kullanabileceğiniz diğer şablonlar için bkz. [Azure Hızlı Başlangıç şablonları](https://azure.microsoft.com/documentation/templates/) ve [Şablon kullanan uygulama çerçeveleri](../articles/virtual-machines/linux/app-frameworks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b91fc-332">For more templates you can use, see [Azure Quickstart templates](https://azure.microsoft.com/documentation/templates/) and [Application frameworks using templates](../articles/virtual-machines/linux/app-frameworks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
