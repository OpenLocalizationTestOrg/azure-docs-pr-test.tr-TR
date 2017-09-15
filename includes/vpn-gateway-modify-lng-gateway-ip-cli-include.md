### <a name="to-modify-the-local-network-gateway-gatewayipaddress"></a><span data-ttu-id="1fa0c-101">Yerel ağ geçidini değiştirmek için 'gatewayIpAddress'</span><span class="sxs-lookup"><span data-stu-id="1fa0c-101">To modify the local network gateway 'gatewayIpAddress'</span></span>

<span data-ttu-id="1fa0c-102">Bağlanmak istediğiniz VPN cihazının genel IP adresi değiştiyse, yerel ağ geçidini bu değişikliği yansıtacak şekilde değiştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1fa0c-102">If the VPN device that you want to connect to has changed its public IP address, you need to modify the local network gateway to reflect that change.</span></span> <span data-ttu-id="1fa0c-103">Ağ geçidi IP adresi, mevcut bir VPN ağ geçidi bağlantısı (varsa) kaldırılmadan değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="1fa0c-103">The gateway IP address can be changed without removing an existing VPN gateway connection (if you have one).</span></span> <span data-ttu-id="1fa0c-104">Ağ geçidi IP adresini değiştirmek için 'Site2' ve 'TestRG1' değerlerini [az network local-gateway update](https://docs.microsoft.com/cli/azure/network/local-gateway#update) komutunu kullanarak istediğiniz değerlerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="1fa0c-104">To modify the gateway IP address, replace the values 'Site2' and 'TestRG1' with your own using the [az network local-gateway update](https://docs.microsoft.com/cli/azure/network/local-gateway#update) command.</span></span>

```azurecli
az network local-gateway update --gateway-ip-address 23.99.222.170 --name Site2 --resource-group TestRG1
```

<span data-ttu-id="1fa0c-105">Çıktıda IP adresinin doğru olduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="1fa0c-105">Verify that the IP address is correct in the output:</span></span>

```
"gatewayIpAddress": "23.99.222.170",
```