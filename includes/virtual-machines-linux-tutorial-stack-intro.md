## <a name="create-a-resource-group"></a><span data-ttu-id="da1eb-101">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="da1eb-101">Create a resource group</span></span>

<span data-ttu-id="da1eb-102">[az group create](/cli/azure/group#create) komutuyla bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="da1eb-102">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="da1eb-103">Azure kaynak grubu, Azure kaynaklarının dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="da1eb-103">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="da1eb-104">Aşağıdaki örnek *eastus* konumunda *myResourceGroup* adlı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="da1eb-104">The following example creates a resource group named *myResourceGroup* in the *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-virtual-machine"></a><span data-ttu-id="da1eb-105">Sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="da1eb-105">Create a virtual machine</span></span>

<span data-ttu-id="da1eb-106">[az vm create](/cli/azure/vm#create) komutuyla bir sanal makine oluşturun.</span><span class="sxs-lookup"><span data-stu-id="da1eb-106">Create a VM with the [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="da1eb-107">Aşağıdaki örnekte *myVM* adlı bir VM oluşturulur ve varsayılan anahtar konumunda henüz yoksa SSH anahtarları oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="da1eb-107">The following example creates a VM named *myVM* and creates SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="da1eb-108">Belirli bir anahtar kümesini kullanmak için `--ssh-key-value` seçeneğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="da1eb-108">To use a specific set of keys, use the `--ssh-key-value` option.</span></span>  

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="da1eb-109">VM oluşturulduğunda Azure CLI, aşağıdaki örneğe benzer bilgiler gösterir.</span><span class="sxs-lookup"><span data-stu-id="da1eb-109">When the VM has been created, the Azure CLI shows information similar to the following example.</span></span> <span data-ttu-id="da1eb-110">`publicIpAddress` değerini not edin.</span><span class="sxs-lookup"><span data-stu-id="da1eb-110">Take note of the `publicIpAddress`.</span></span> <span data-ttu-id="da1eb-111">Bu adres, VM’ye erişmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="da1eb-111">This address is used to access the VM.</span></span>

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



## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="da1eb-112">Web trafiği için 80 numaralı bağlantı noktasını açın</span><span class="sxs-lookup"><span data-stu-id="da1eb-112">Open port 80 for web traffic</span></span> 

<span data-ttu-id="da1eb-113">Varsayılan olarak, Linux Azure üzerinde dağıtılan VM'ler içine yalnızca SSH bağlantılara izin verilir.</span><span class="sxs-lookup"><span data-stu-id="da1eb-113">By default, only SSH connections are allowed into Linux VMs deployed in Azure.</span></span> <span data-ttu-id="da1eb-114">Bir web sunucusu olacak şekilde bu VM olacağından, internet'ten 80 numaralı bağlantı noktasını açmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="da1eb-114">Because this VM is going to be a web server, you need to open port 80 from the internet.</span></span> <span data-ttu-id="da1eb-115">İstediğiniz bağlantı noktasını açmak için [az vm open-port](/cli/azure/vm#open-port) komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="da1eb-115">Use the [az vm open-port](/cli/azure/vm#open-port) command to open the desired port.</span></span>  
 
```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```
## <a name="ssh-into-your-vm"></a><span data-ttu-id="da1eb-116">VM’ye SSH uygulama</span><span class="sxs-lookup"><span data-stu-id="da1eb-116">SSH into your VM</span></span>


<span data-ttu-id="da1eb-117">VM genel IP adresi zaten bilmiyorsanız, çalıştırmak [az ağ ortak IP listesi](/cli/azure/network/public-ip#list) komutu:</span><span class="sxs-lookup"><span data-stu-id="da1eb-117">If you don't already know the public IP address of your VM, run the [az network public-ip list](/cli/azure/network/public-ip#list) command:</span></span>


```azurecli-interactive
az network public-ip list --resource-group myResourceGroup --query [].ipAddress
```

<span data-ttu-id="da1eb-118">Sanal makine ile bir SSH oturumu oluşturmak için aşağıdaki komutu kullanın.</span><span class="sxs-lookup"><span data-stu-id="da1eb-118">Use the following command to create an SSH session with the virtual machine.</span></span> <span data-ttu-id="da1eb-119">Sanal makineniz doğru ortak IP adresini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="da1eb-119">Substitute the correct public IP address of your virtual machine.</span></span> <span data-ttu-id="da1eb-120">Bu örnekte IP adresidir *40.68.254.142*.</span><span class="sxs-lookup"><span data-stu-id="da1eb-120">In this example, the IP address is *40.68.254.142*.</span></span>

```bash
ssh azureuser@40.68.254.142
```

