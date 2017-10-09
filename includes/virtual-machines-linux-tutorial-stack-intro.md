## <a name="create-a-resource-group"></a>Kaynak grubu oluşturma

Bir kaynak grubu ile Merhaba oluşturmak [az grubu oluşturma](/cli/azure/group#create) komutu. Azure kaynak grubu, Azure kaynaklarının dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır. 

Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroup* hello içinde *eastus* konumu.

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-virtual-machine"></a>Sanal makine oluşturma

Bir VM ile Merhaba oluşturma [az vm oluşturma](/cli/azure/vm#create) komutu. 

Merhaba aşağıdaki örnekte oluşturur adlı bir VM'den *myVM* ve zaten bir varsayılan anahtar konumda yoksa, SSH anahtarları oluşturur. toouse belirli bir ayarla anahtarları, hello kullan `--ssh-key-value` seçeneği.  

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

Merhaba VM oluşturduğunuzda hello Azure CLI örnek aşağıdaki bilgileri benzer toohello gösterir. Merhaba not edin `publicIpAddress`. Kullanılan tooaccess hello VM adresidir.

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



## <a name="open-port-80-for-web-traffic"></a>Web trafiği için 80 numaralı bağlantı noktasını açın 

Varsayılan olarak, Linux Azure üzerinde dağıtılan VM'ler içine yalnızca SSH bağlantılara izin verilir. Bu VM toobe bir web sunucusu olacağından hello gelen tooopen bağlantı noktası 80 gereksinim Internet. Kullanım hello [az vm Aç-port](/cli/azure/vm#open-port) komutu tooopen hello istenen bağlantı noktası.  
 
```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```
## <a name="ssh-into-your-vm"></a>VM’ye SSH uygulama


Zaten tanımadığınız varsa Merhaba VM genel IP adresi, hello çalıştırmak [az ağ ortak IP listesi](/cli/azure/network/public-ip#list) komutu:


```azurecli-interactive
az network public-ip list --resource-group myResourceGroup --query [].ipAddress
```

Kullanım hello aşağıdaki toocreate SSH oturumu hello sanal makineyle bir komutu. Merhaba doğru ortak IP adresi, sanal makinenin değiştirin. Bu örnekte, hello IP adresidir *40.68.254.142*.

```bash
ssh azureuser@40.68.254.142
```

