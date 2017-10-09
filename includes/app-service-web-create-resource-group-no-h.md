<span data-ttu-id="f337f-101">Bir kaynak grubu ile Merhaba oluşturmak [az grubu oluşturma](/cli/azure/group#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="f337f-101">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span>

[!INCLUDE [resource group intro text](resource-group.md)]

<span data-ttu-id="f337f-102">Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroup* hello içinde *westeurope* konumu.</span><span class="sxs-lookup"><span data-stu-id="f337f-102">hello following example creates a resource group named *myResourceGroup* in hello *westeurope* location.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="f337f-103">Genellikle yakın bir bölgede, kaynak grubu ve hello kaynakları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f337f-103">You generally create your resource group and hello resources in a region near you.</span></span> <span data-ttu-id="f337f-104">Azure Web Apps, hello çalıştırmak için toosee tüm desteklenen Konumlar `az appservice list-locations` komutu.</span><span class="sxs-lookup"><span data-stu-id="f337f-104">toosee all supported locations for Azure Web Apps, run hello `az appservice list-locations` command.</span></span> 
