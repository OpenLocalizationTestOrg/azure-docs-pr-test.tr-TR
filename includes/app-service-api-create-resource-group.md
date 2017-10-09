Bir kaynak grubu ile Merhaba oluşturmak [az grubu oluşturma](/cli/azure/group#create) komutu.

[!INCLUDE [resource group intro text](resource-group.md)]

Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroup* hello içinde *westeurope* konumu.

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

Merhaba çalıştırmak toosee hello kullanılabilir konumlarını `az appservice list-locations` komutu. Genellikle kaynakları kendinize yakın bir bölgede oluşturmanız önerilir.
