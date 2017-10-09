### <a name="toomodify-hello-local-network-gateway-gatewayipaddress"></a>toomodify hello yerel ağ geçidi 'Gatewayıpaddress'

Tooconnect toohas istediğiniz hello VPN cihazının genel IP adresini değiştirdiyseniz, değişiklik toomodify hello yerel ağ geçidi tooreflect gerekir. Merhaba ağ geçidi IP adresi, (varsa) olan bir VPN ağ geçidi bağlantısını kaldırmadan değiştirilebilir. toomodify hello ağ geçidi IP adresi, Değiştir hello değerleri 'Site2' ve 'TestRG1' kullanarak kendi hello [az ağ yerel ağ geçidi güncelleştirmesi](https://docs.microsoft.com/cli/azure/network/local-gateway#update) komutu.

```azurecli
az network local-gateway update --gateway-ip-address 23.99.222.170 --name Site2 --resource-group TestRG1
```

Başlangıç IP adresi hello çıktısında doğru olduğundan emin olun:

```
"gatewayIpAddress": "23.99.222.170",
```