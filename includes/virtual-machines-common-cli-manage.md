<span data-ttu-id="9a222-101">Hello Azure CLI 2.0 macOS, Linux ve Windows Azure kaynaklarınızı yönetmek ve toocreate sağlar.</span><span class="sxs-lookup"><span data-stu-id="9a222-101">hello Azure CLI 2.0 allows you toocreate and manage your Azure resources on macOS, Linux, and Windows.</span></span> <span data-ttu-id="9a222-102">Bu makalede hello en yaygın komutları toocreate bazıları ayrıntıları ve sanal makineleri (VM'ler) yönetme.</span><span class="sxs-lookup"><span data-stu-id="9a222-102">This article details some of hello most common commands toocreate and manage virtual machines (VMs).</span></span>

<span data-ttu-id="9a222-103">Bu makale hello Azure CLI Sürüm 2.0.4 gerektirir veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="9a222-103">This article requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="9a222-104">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="9a222-104">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="9a222-105">Tooupgrade gerekirse bkz [Azure CLI 2.0 yükleme](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="9a222-105">If you need tooupgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="9a222-106">Aynı zamanda [bulut Kabuk](/azure/cloud-shell/quickstart) tarayıcınızdan.</span><span class="sxs-lookup"><span data-stu-id="9a222-106">You can also use [Cloud Shell](/azure/cloud-shell/quickstart) from your browser.</span></span>

## <a name="basic-azure-resource-manager-commands-in-azure-cli"></a><span data-ttu-id="9a222-107">Azure CLI’daki Temel Azure Resource Manager komutları</span><span class="sxs-lookup"><span data-stu-id="9a222-107">Basic Azure Resource Manager commands in Azure CLI</span></span>
<span data-ttu-id="9a222-108">Daha ayrıntılı belirli komut satırı anahtarları ve seçenekleri ile ilgili Yardım için hello çevrimiçi komut Yardımı ve Seçenekler yazarak kullanabileceğiniz `az <command> <subcommand> --help`.</span><span class="sxs-lookup"><span data-stu-id="9a222-108">For more detailed help with specific command line switches and options, you can use hello online command help and options by typing `az <command> <subcommand> --help`.</span></span>

### <a name="create-vms"></a><span data-ttu-id="9a222-109">VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="9a222-109">Create VMs</span></span>
| <span data-ttu-id="9a222-110">Görev</span><span class="sxs-lookup"><span data-stu-id="9a222-110">Task</span></span> | <span data-ttu-id="9a222-111">Azure CLI komutları</span><span class="sxs-lookup"><span data-stu-id="9a222-111">Azure CLI commands</span></span> |
| --- | --- |
| <span data-ttu-id="9a222-112">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="9a222-112">Create a resource group</span></span> | `az group create --name myResourceGroup --location eastus` |
| <span data-ttu-id="9a222-113">Linux VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="9a222-113">Create a Linux VM</span></span> | `az vm create --resource-group myResourceGroup --name myVM --image ubuntults` |
| <span data-ttu-id="9a222-114">Windows VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="9a222-114">Create a Windows VM</span></span> | `az vm create --resource-group myResourceGroup --name myVM --image win2016datacenter` |

### <a name="manage-vm-state"></a><span data-ttu-id="9a222-115">VM durumunu yönetme</span><span class="sxs-lookup"><span data-stu-id="9a222-115">Manage VM state</span></span>
| <span data-ttu-id="9a222-116">Görev</span><span class="sxs-lookup"><span data-stu-id="9a222-116">Task</span></span> | <span data-ttu-id="9a222-117">Azure CLI komutları</span><span class="sxs-lookup"><span data-stu-id="9a222-117">Azure CLI commands</span></span> |
| --- | --- |
| <span data-ttu-id="9a222-118">VM başlatma</span><span class="sxs-lookup"><span data-stu-id="9a222-118">Start a VM</span></span> | `az vm start --resource-group myResourceGroup --name myVM` |
| <span data-ttu-id="9a222-119">VM durdurma</span><span class="sxs-lookup"><span data-stu-id="9a222-119">Stop a VM</span></span> | `az vm stop --resource-group myResourceGroup --name myVM` |
| <span data-ttu-id="9a222-120">Bir VM’yi serbest bırakma</span><span class="sxs-lookup"><span data-stu-id="9a222-120">Deallocate a VM</span></span> | `az vm deallocate --resource-group myResourceGroup --name myVM` |
| <span data-ttu-id="9a222-121">Bir VM’yi yeniden başlatma</span><span class="sxs-lookup"><span data-stu-id="9a222-121">Restart a VM</span></span> | `az vm restart --resource-group myResourceGroup --name myVM` |
| <span data-ttu-id="9a222-122">Bir VM’yi yeniden dağıtma</span><span class="sxs-lookup"><span data-stu-id="9a222-122">Redeploy a VM</span></span> | `az vm redeploy --resource-group myResourceGroup --name myVM` |
| <span data-ttu-id="9a222-123">VM silme</span><span class="sxs-lookup"><span data-stu-id="9a222-123">Delete a VM</span></span> | `az vm delete --resource-group myResourceGroup --name myVM` |

### <a name="get-vm-info"></a><span data-ttu-id="9a222-124">VM bilgilerini al</span><span class="sxs-lookup"><span data-stu-id="9a222-124">Get VM info</span></span>
| <span data-ttu-id="9a222-125">Görev</span><span class="sxs-lookup"><span data-stu-id="9a222-125">Task</span></span> | <span data-ttu-id="9a222-126">Azure CLI komutları</span><span class="sxs-lookup"><span data-stu-id="9a222-126">Azure CLI commands</span></span> |
| --- | --- |
| <span data-ttu-id="9a222-127">VM'leri listeleme</span><span class="sxs-lookup"><span data-stu-id="9a222-127">List VMs</span></span> | `az vm list` |
| <span data-ttu-id="9a222-128">VM hakkında bilgi alma</span><span class="sxs-lookup"><span data-stu-id="9a222-128">Get information about a VM</span></span> | `az vm show --resource-group myResourceGroup --name myVM` |
| <span data-ttu-id="9a222-129">VM kaynaklarının kullanımını alma</span><span class="sxs-lookup"><span data-stu-id="9a222-129">Get usage of VM resources</span></span> | `az vm list-usage --location eastus` |
| <span data-ttu-id="9a222-130">Tüm kullanılabilir VM boyutlarını alma</span><span class="sxs-lookup"><span data-stu-id="9a222-130">Get all available VM sizes</span></span> | `az vm list-sizes --location eastus` |

## <a name="disks-and-images"></a><span data-ttu-id="9a222-131">Diskleri ve görüntüleri</span><span class="sxs-lookup"><span data-stu-id="9a222-131">Disks and images</span></span>
| <span data-ttu-id="9a222-132">Görev</span><span class="sxs-lookup"><span data-stu-id="9a222-132">Task</span></span> | <span data-ttu-id="9a222-133">Azure CLI komutları</span><span class="sxs-lookup"><span data-stu-id="9a222-133">Azure CLI commands</span></span> |
| --- | --- |
| <span data-ttu-id="9a222-134">Bir veri diski tooa VM ekleme</span><span class="sxs-lookup"><span data-stu-id="9a222-134">Add a data disk tooa VM</span></span> | `az vm disk attach --resource-group myResourceGroup --vm-name myVM --disk myDataDisk --size-gb 128 --new ` |
| <span data-ttu-id="9a222-135">Bir VM’den veri diski kaldırma</span><span class="sxs-lookup"><span data-stu-id="9a222-135">Remove a data disk from a VM</span></span> | `az vm disk detach --resource-group myResourceGroup --vm-name myVM --disk myDataDisk` |
| <span data-ttu-id="9a222-136">Bir diski yeniden boyutlandırma</span><span class="sxs-lookup"><span data-stu-id="9a222-136">Resize a disk</span></span> | `az disk update --resource-group myResourceGroup --name myDataDisk --size-gb 256` |
| <span data-ttu-id="9a222-137">Bir diskin anlık görüntüsünü alma</span><span class="sxs-lookup"><span data-stu-id="9a222-137">Snapshot a disk</span></span> | `az snapshot create --resource-group myResourceGroup --name mySnapshot --source myDataDisk` |
| <span data-ttu-id="9a222-138">Bir VM görüntüsü oluşturma</span><span class="sxs-lookup"><span data-stu-id="9a222-138">Create image of a VM</span></span> | `az image create --resource-group myResourceGroup --source myVM --name myImage` |
| <span data-ttu-id="9a222-139">VM görüntüsünü oluşturma</span><span class="sxs-lookup"><span data-stu-id="9a222-139">Create VM from image</span></span> | `az vm create --resource-group myResourceGroup --name myNewVM --image myImage` |


## <a name="next-steps"></a><span data-ttu-id="9a222-140">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9a222-140">Next steps</span></span>
<span data-ttu-id="9a222-141">Merhaba hello CLI komutları ek örnekler için bkz: [oluşturma ve yönetme Linux VM'ler hello Azure CLI ile](../articles/virtual-machines/linux/tutorial-manage-vm.md) Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="9a222-141">For additional examples of hello CLI commands, see hello [Create and Manage Linux VMs with hello Azure CLI](../articles/virtual-machines/linux/tutorial-manage-vm.md) tutorial.</span></span>

