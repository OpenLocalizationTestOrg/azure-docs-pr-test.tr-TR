### <a name="tooview-local-network-gateways"></a><span data-ttu-id="f8ebc-101">tooview yerel ağ geçitleri</span><span class="sxs-lookup"><span data-stu-id="f8ebc-101">tooview local network gateways</span></span>

<span data-ttu-id="f8ebc-102">tooview hello yerel ağ geçitleri, kullanım hello listesini [az ağ yerel ağ geçidi listesi](https://docs.microsoft.com/cli/azure/network/local-gateway#list) komutu.</span><span class="sxs-lookup"><span data-stu-id="f8ebc-102">tooview a list of hello local network gateways, use hello [az network local-gateway list](https://docs.microsoft.com/cli/azure/network/local-gateway#list) command.</span></span>

```azurecli
az network local-gateway list --resource-group TestRG1
```

[!INCLUDE [modify-prefix](vpn-gateway-modify-ip-prefix-cli-include.md)]

[!INCLUDE [modify-gateway-IP](vpn-gateway-modify-lng-gateway-ip-cli-include.md)]

### <a name="tooverify-hello-shared-key-values"></a><span data-ttu-id="f8ebc-103">tooverify hello paylaşılan anahtar değerleri</span><span class="sxs-lookup"><span data-stu-id="f8ebc-103">tooverify hello shared key values</span></span>

<span data-ttu-id="f8ebc-104">Merhaba paylaşılan anahtar değeri hello olduğunu doğrulayın, VPN cihazınızın yapılandırması için kullandığınız aynı değeri.</span><span class="sxs-lookup"><span data-stu-id="f8ebc-104">Verify that hello shared key value is hello same value that you used for your VPN device configuration.</span></span> <span data-ttu-id="f8ebc-105">Değilse, hello bağlantı hello değerinden hello cihaza ya da güncelleştirme hello hello dönüş hello değerinden ile kullanarak yeniden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="f8ebc-105">If it is not, either run hello connection again using hello value from hello device, or update hello device with hello value from hello return.</span></span> <span data-ttu-id="f8ebc-106">Merhaba değerler eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="f8ebc-106">hello values must match.</span></span> <span data-ttu-id="f8ebc-107">tooview hello paylaşılan anahtar, kullanım hello [az ağ vpn bağlantı listesi](https://docs.microsoft.com/cli/azure/network/vpn-connection#list).</span><span class="sxs-lookup"><span data-stu-id="f8ebc-107">tooview hello shared key, use hello [az network vpn-connection-list](https://docs.microsoft.com/cli/azure/network/vpn-connection#list).</span></span>

```azurecli
az network vpn-connection shared-key show --connection-name VNet1toSite2 --resource-group TestRG1
```
### <a name="tooview-hello-vpn-gateway-public-ip-address"></a><span data-ttu-id="f8ebc-108">tooview hello VPN ağ geçidi genel IP adresi</span><span class="sxs-lookup"><span data-stu-id="f8ebc-108">tooview hello VPN gateway Public IP address</span></span>

<span data-ttu-id="f8ebc-109">sanal ağ geçidinizi kullanın hello toofind hello genel IP adresi [az ağ ortak IP listesi](https://docs.microsoft.com/cli/azure/network/public-ip#list) komutu.</span><span class="sxs-lookup"><span data-stu-id="f8ebc-109">toofind hello public IP address of your virtual network gateway, use hello [az network public-ip list](https://docs.microsoft.com/cli/azure/network/public-ip#list) command.</span></span> <span data-ttu-id="f8ebc-110">Kolay okuma için bu örnek için hello çıktı biçimlendirilmiş toodisplay hello genel IP'ler, tablo biçiminde listesidir.</span><span class="sxs-lookup"><span data-stu-id="f8ebc-110">For easy reading, hello output for this example is formatted toodisplay hello list of public IPs in table format.</span></span>

```azurecli
az network public-ip list --resource-group TestRG1 --output table
```
