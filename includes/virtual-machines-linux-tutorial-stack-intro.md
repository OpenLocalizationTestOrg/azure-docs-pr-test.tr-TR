## <a name="create-a-resource-group"></a><span data-ttu-id="d9413-101">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="d9413-101">Create a resource group</span></span>

<span data-ttu-id="d9413-102">Bir kaynak grubu ile Merhaba oluşturmak [az grubu oluşturma](/cli/azure/group#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="d9413-102">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="d9413-103">Azure kaynak grubu, Azure kaynaklarının dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="d9413-103">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="d9413-104">Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroup* hello içinde *eastus* konumu.</span><span class="sxs-lookup"><span data-stu-id="d9413-104">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-virtual-machine"></a><span data-ttu-id="d9413-105">Sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="d9413-105">Create a virtual machine</span></span>

<span data-ttu-id="d9413-106">Bir VM ile Merhaba oluşturma [az vm oluşturma](/cli/azure/vm#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="d9413-106">Create a VM with hello [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="d9413-107">Merhaba aşağıdaki örnekte oluşturur adlı bir VM'den *myVM* ve zaten bir varsayılan anahtar konumda yoksa, SSH anahtarları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d9413-107">hello following example creates a VM named *myVM* and creates SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="d9413-108">toouse belirli bir ayarla anahtarları, hello kullan `--ssh-key-value` seçeneği.</span><span class="sxs-lookup"><span data-stu-id="d9413-108">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>  

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="d9413-109">Merhaba VM oluşturduğunuzda hello Azure CLI örnek aşağıdaki bilgileri benzer toohello gösterir.</span><span class="sxs-lookup"><span data-stu-id="d9413-109">When hello VM has been created, hello Azure CLI shows information similar toohello following example.</span></span> <span data-ttu-id="d9413-110">Merhaba not edin `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="d9413-110">Take note of hello `publicIpAddress`.</span></span> <span data-ttu-id="d9413-111">Kullanılan tooaccess hello VM adresidir.</span><span class="sxs-lookup"><span data-stu-id="d9413-111">This address is used tooaccess hello VM.</span></span>

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/<subscription ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "40.68.254.142",
  "resourceGroup": "myResourceGroup"
}
```



## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="d9413-112">Web trafiği için 80 numaralı bağlantı noktasını açın</span><span class="sxs-lookup"><span data-stu-id="d9413-112">Open port 80 for web traffic</span></span> 

<span data-ttu-id="d9413-113">Varsayılan olarak, Linux Azure üzerinde dağıtılan VM'ler içine yalnızca SSH bağlantılara izin verilir.</span><span class="sxs-lookup"><span data-stu-id="d9413-113">By default, only SSH connections are allowed into Linux VMs deployed in Azure.</span></span> <span data-ttu-id="d9413-114">Bu VM toobe bir web sunucusu olacağından hello gelen tooopen bağlantı noktası 80 gereksinim Internet.</span><span class="sxs-lookup"><span data-stu-id="d9413-114">Because this VM is going toobe a web server, you need tooopen port 80 from hello internet.</span></span> <span data-ttu-id="d9413-115">Kullanım hello [az vm Aç-port](/cli/azure/vm#open-port) komutu tooopen hello istenen bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="d9413-115">Use hello [az vm open-port](/cli/azure/vm#open-port) command tooopen hello desired port.</span></span>  
 
```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```
## <a name="ssh-into-your-vm"></a><span data-ttu-id="d9413-116">VM’ye SSH uygulama</span><span class="sxs-lookup"><span data-stu-id="d9413-116">SSH into your VM</span></span>


<span data-ttu-id="d9413-117">Zaten tanımadığınız varsa Merhaba VM genel IP adresi, hello çalıştırmak [az ağ ortak IP listesi](/cli/azure/network/public-ip#list) komutu:</span><span class="sxs-lookup"><span data-stu-id="d9413-117">If you don't already know hello public IP address of your VM, run hello [az network public-ip list](/cli/azure/network/public-ip#list) command:</span></span>


```azurecli-interactive
az network public-ip list --resource-group myResourceGroup --query [].ipAddress
```

<span data-ttu-id="d9413-118">Kullanım hello aşağıdaki toocreate SSH oturumu hello sanal makineyle bir komutu.</span><span class="sxs-lookup"><span data-stu-id="d9413-118">Use hello following command toocreate an SSH session with hello virtual machine.</span></span> <span data-ttu-id="d9413-119">Merhaba doğru ortak IP adresi, sanal makinenin değiştirin.</span><span class="sxs-lookup"><span data-stu-id="d9413-119">Substitute hello correct public IP address of your virtual machine.</span></span> <span data-ttu-id="d9413-120">Bu örnekte, hello IP adresidir *40.68.254.142*.</span><span class="sxs-lookup"><span data-stu-id="d9413-120">In this example, hello IP address is *40.68.254.142*.</span></span>

```bash
ssh azureuser@40.68.254.142
```

