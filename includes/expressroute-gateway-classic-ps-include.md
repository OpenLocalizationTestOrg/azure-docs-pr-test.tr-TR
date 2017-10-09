VNet ve bir ağ geçidi alt ağı önce görevleri aşağıdaki hello üzerinde çalışmaya başlamadan önce oluşturmanız gerekir. Merhaba makalesine bakın [hello Klasik portalı kullanarak bir sanal ağ yapılandırma](../articles/expressroute/expressroute-howto-vnet-portal-classic.md) daha fazla bilgi için.   

## <a name="add-a-gateway"></a>Bir ağ geçidi Ekle
Bir ağ geçidi toocreate aşağıdaki Hello komutunu kullanın. Emin toosubstitute kendi için herhangi bir değer olmalıdır.

    New-AzureVirtualNetworkGateway -VNetName "MyAzureVNET" -GatewayName "ERGateway" -GatewayType Dedicated -GatewaySKU  Standard

## <a name="verify-hello-gateway-was-created"></a>Merhaba ağ geçidinin oluşturulduğunu doğrulayın
Ağ geçidi hello tooverify aşağıdaki kullanım hello komutunu oluşturuldu. Bu komut ayrıca diğer işlemler için gereksinim duyduğunuz hello ağ geçidi kimliği alır.

    Get-AzureVirtualNetworkGateway

## <a name="resize-a-gateway"></a>Bir ağ geçidi yeniden boyutlandırma
Bir dizi vardır [ağ geçidi SKU'ları](../articles/expressroute/expressroute-about-virtual-network-gateways.md). Herhangi bir zamanda komutu toochange hello ağ geçidi SKU'su aşağıdaki hello kullanabilirsiniz.

> [!IMPORTANT]
> Bu komut için UltraPerformance ağ geçidi çalışmıyor. toochange ağ geçidi tooan UltraPerformance ağ geçidiniz, önce ExpressRoute ağ geçidi mevcut hello kaldırın ve yeni UltraPerformance ağ geçidi oluşturmak. toodowngrade önce bir UltraPerformance ağ geçidi, ağ geçidinden Kaldır UltraPerformance ağ geçidi hello ve ardından yeni bir ağ geçidi oluşturun. 
> 
> 

    Resize-AzureVirtualNetworkGateway -GatewayId <Gateway ID> -GatewaySKU HighPerformance

## <a name="remove-a-gateway"></a>Bir ağ geçidi kaldırma
Bir ağ geçidi tooremove aşağıdaki Hello komutunu kullanın

    Remove-AzureVirtualNetworkGateway -GatewayId <Gateway ID>