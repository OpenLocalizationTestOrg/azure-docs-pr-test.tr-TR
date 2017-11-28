<span data-ttu-id="f8827-101">[az group create](/cli/azure/group#create) komutuyla bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f8827-101">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span>

[!INCLUDE [resource group intro text](resource-group.md)]

<span data-ttu-id="f8827-102">Aşağıdaki örnek *westeurope* konumunda *myResourceGroup* adlı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f8827-102">The following example creates a resource group named *myResourceGroup* in the *westeurope* location.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="f8827-103">Seçebileceğiniz konumları görmek için `az appservice list-locations` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="f8827-103">To see the available locations, run the `az appservice list-locations` command.</span></span> <span data-ttu-id="f8827-104">Genellikle kaynakları kendinize yakın bir bölgede oluşturmanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="f8827-104">You generally create resources in a region near you.</span></span>
