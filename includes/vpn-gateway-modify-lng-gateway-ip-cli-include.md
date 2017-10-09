### <a name="toomodify-hello-local-network-gateway-gatewayipaddress"></a><span data-ttu-id="65317-101">toomodify hello yerel ağ geçidi 'Gatewayıpaddress'</span><span class="sxs-lookup"><span data-stu-id="65317-101">toomodify hello local network gateway 'gatewayIpAddress'</span></span>

<span data-ttu-id="65317-102">Tooconnect toohas istediğiniz hello VPN cihazının genel IP adresini değiştirdiyseniz, değişiklik toomodify hello yerel ağ geçidi tooreflect gerekir.</span><span class="sxs-lookup"><span data-stu-id="65317-102">If hello VPN device that you want tooconnect toohas changed its public IP address, you need toomodify hello local network gateway tooreflect that change.</span></span> <span data-ttu-id="65317-103">Merhaba ağ geçidi IP adresi, (varsa) olan bir VPN ağ geçidi bağlantısını kaldırmadan değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="65317-103">hello gateway IP address can be changed without removing an existing VPN gateway connection (if you have one).</span></span> <span data-ttu-id="65317-104">toomodify hello ağ geçidi IP adresi, Değiştir hello değerleri 'Site2' ve 'TestRG1' kullanarak kendi hello [az ağ yerel ağ geçidi güncelleştirmesi](https://docs.microsoft.com/cli/azure/network/local-gateway#update) komutu.</span><span class="sxs-lookup"><span data-stu-id="65317-104">toomodify hello gateway IP address, replace hello values 'Site2' and 'TestRG1' with your own using hello [az network local-gateway update](https://docs.microsoft.com/cli/azure/network/local-gateway#update) command.</span></span>

```azurecli
az network local-gateway update --gateway-ip-address 23.99.222.170 --name Site2 --resource-group TestRG1
```

<span data-ttu-id="65317-105">Başlangıç IP adresi hello çıktısında doğru olduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="65317-105">Verify that hello IP address is correct in hello output:</span></span>

```
"gatewayIpAddress": "23.99.222.170",
```