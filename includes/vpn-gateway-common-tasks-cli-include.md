### <a name="tooview-local-network-gateways"></a>tooview yerel ağ geçitleri

tooview hello yerel ağ geçitleri, kullanım hello listesini [az ağ yerel ağ geçidi listesi](https://docs.microsoft.com/cli/azure/network/local-gateway#list) komutu.

```azurecli
az network local-gateway list --resource-group TestRG1
```

[!INCLUDE [modify-prefix](vpn-gateway-modify-ip-prefix-cli-include.md)]

[!INCLUDE [modify-gateway-IP](vpn-gateway-modify-lng-gateway-ip-cli-include.md)]

### <a name="tooverify-hello-shared-key-values"></a>tooverify hello paylaşılan anahtar değerleri

Merhaba paylaşılan anahtar değeri hello olduğunu doğrulayın, VPN cihazınızın yapılandırması için kullandığınız aynı değeri. Değilse, hello bağlantı hello değerinden hello cihaza ya da güncelleştirme hello hello dönüş hello değerinden ile kullanarak yeniden çalıştırın. Merhaba değerler eşleşmelidir. tooview hello paylaşılan anahtar, kullanım hello [az ağ vpn bağlantı listesi](https://docs.microsoft.com/cli/azure/network/vpn-connection#list).

```azurecli
az network vpn-connection shared-key show --connection-name VNet1toSite2 --resource-group TestRG1
```
### <a name="tooview-hello-vpn-gateway-public-ip-address"></a>tooview hello VPN ağ geçidi genel IP adresi

sanal ağ geçidinizi kullanın hello toofind hello genel IP adresi [az ağ ortak IP listesi](https://docs.microsoft.com/cli/azure/network/public-ip#list) komutu. Kolay okuma için bu örnek için hello çıktı biçimlendirilmiş toodisplay hello genel IP'ler, tablo biçiminde listesidir.

```azurecli
az network public-ip list --resource-group TestRG1 --output table
```
