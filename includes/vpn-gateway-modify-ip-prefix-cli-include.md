### <a name="noconnection"></a>toomodify yerel ağ geçidi IP adresi öneklerini - ağ geçidi bağlantısı yok

Bir ağ geçidi bağlantısı yoktur ve tooadd istediğiniz ya da IP adresi öneklerini kaldırmak, hello kullanın aynı toocreate hello yerel ağ geçidi, kullandığınız komut [az ağ yerel-ağ geçidi oluşturmak](https://docs.microsoft.com/cli/azure/network/local-gateway#create). Bu komut tooupdate hello ağ geçidi IP adresi hello VPN cihazı için de kullanabilirsiniz. toooverwrite hello geçerli ayarları, yerel ağ geçidinizin hello var olan adını kullanın. Farklı bir ad kullanırsanız, yeni bir yerel ağ geçidi oluşturma, üzerine yerine var olan bir hello.

Bir değişiklik, hello öneklerini tam listesini yaptığınız her zaman belirtilmesi gerekir, yalnızca hello toochange istediğiniz ekler. Yalnızca hello öneklerini tookeep istediğinizi belirtin. Bu durumda, söz konusu ön ekler 10.0.0.0/24 ve 20.0.0.0/24’tür.

```azurecli
az network local-gateway create --gateway-ip-address 23.99.221.164 --name Site2 --connection-name TestRG1 --local-address-prefixes 10.0.0.0/24 20.0.0.0/24
```

### <a name="withconnection"></a>ağ geçidi bağlantısı varolan toomodify yerel ağ geçidi IP adresi öneklerini-

Bir ağ geçidi bağlantısına sahip ve tooadd istediğiniz veya IP adresi öneklerini kaldırırsanız, kullanarak hello öneklerini güncelleştirebilirsiniz [az ağ yerel ağ geçidi güncelleştirmesi](https://docs.microsoft.com/cli/azure/network/local-gateway#update). Bunun sonucunda, VPN bağlantınızda kesinti oluşur. Başlangıç IP adresi değiştirme önekleri, toodelete hello VPN ağ geçidi gerekmez.

Bir değişiklik, hello öneklerini tam listesini yaptığınız her zaman belirtilmesi gerekir, yalnızca hello toochange istediğiniz ekler. Bu örnekte, 10.0.0.0/24 ve 20.0.0.0/24 zaten mevcuttur. Biz hello öneklerini 30.0.0.0/24 ve 40.0.0.0/24 ekleyin ve güncelleştirirken tüm 4 hello öneklerini belirtin.

```azurecli
az network local-gateway update --local-address-prefixes 10.0.0.0/24 20.0.0.0/24 30.0.0.0/24 40.0.0.0/24 --name VNet1toSite2 --connection-name TestRG1
```