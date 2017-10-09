Bir kaynak grubu ile Merhaba oluşturmak [az grubu oluşturma](/cli/azure/group#create) komutu.

[!INCLUDE [resource group intro text](resource-group.md)]

Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroup* hello içinde *westeurope* konumu.

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

Genellikle yakın bir bölgede, kaynak grubu ve hello kaynakları oluşturun. Azure Web Apps, hello çalıştırmak için toosee tüm desteklenen Konumlar `az appservice list-locations` komutu. 
