<span data-ttu-id="76b87-101">Bir kaynak grubu ile Merhaba oluşturmak [az grubu oluşturma](/cli/azure/group#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="76b87-101">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span>

[!INCLUDE [resource group intro text](resource-group.md)]

<span data-ttu-id="76b87-102">Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroup* hello içinde *westeurope* konumu.</span><span class="sxs-lookup"><span data-stu-id="76b87-102">hello following example creates a resource group named *myResourceGroup* in hello *westeurope* location.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="76b87-103">Merhaba çalıştırmak toosee hello kullanılabilir konumlarını `az appservice list-locations` komutu.</span><span class="sxs-lookup"><span data-stu-id="76b87-103">toosee hello available locations, run hello `az appservice list-locations` command.</span></span> <span data-ttu-id="76b87-104">Genellikle kaynakları kendinize yakın bir bölgede oluşturmanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="76b87-104">You generally create resources in a region near you.</span></span>
