<span data-ttu-id="7dfad-101">VNet ve bir ağ geçidi alt ağı önce görevleri aşağıdaki hello üzerinde çalışmaya başlamadan önce oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7dfad-101">You must create a VNet and a gateway subnet first, before working on hello following tasks.</span></span> <span data-ttu-id="7dfad-102">Merhaba makalesine bakın [hello Klasik portalı kullanarak bir sanal ağ yapılandırma](../articles/expressroute/expressroute-howto-vnet-portal-classic.md) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="7dfad-102">See hello article [Configure a Virtual Network using hello classic portal](../articles/expressroute/expressroute-howto-vnet-portal-classic.md) for more information.</span></span>   

## <a name="add-a-gateway"></a><span data-ttu-id="7dfad-103">Bir ağ geçidi Ekle</span><span class="sxs-lookup"><span data-stu-id="7dfad-103">Add a gateway</span></span>
<span data-ttu-id="7dfad-104">Bir ağ geçidi toocreate aşağıdaki Hello komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="7dfad-104">Use hello command below toocreate a gateway.</span></span> <span data-ttu-id="7dfad-105">Emin toosubstitute kendi için herhangi bir değer olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7dfad-105">Be sure toosubstitute any values for your own.</span></span>

    New-AzureVirtualNetworkGateway -VNetName "MyAzureVNET" -GatewayName "ERGateway" -GatewayType Dedicated -GatewaySKU  Standard

## <a name="verify-hello-gateway-was-created"></a><span data-ttu-id="7dfad-106">Merhaba ağ geçidinin oluşturulduğunu doğrulayın</span><span class="sxs-lookup"><span data-stu-id="7dfad-106">Verify hello gateway was created</span></span>
<span data-ttu-id="7dfad-107">Ağ geçidi hello tooverify aşağıdaki kullanım hello komutunu oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="7dfad-107">Use hello command below tooverify that hello gateway has been created.</span></span> <span data-ttu-id="7dfad-108">Bu komut ayrıca diğer işlemler için gereksinim duyduğunuz hello ağ geçidi kimliği alır.</span><span class="sxs-lookup"><span data-stu-id="7dfad-108">This command also retrieves hello gateway ID, which you need for other operations.</span></span>

    Get-AzureVirtualNetworkGateway

## <a name="resize-a-gateway"></a><span data-ttu-id="7dfad-109">Bir ağ geçidi yeniden boyutlandırma</span><span class="sxs-lookup"><span data-stu-id="7dfad-109">Resize a gateway</span></span>
<span data-ttu-id="7dfad-110">Bir dizi vardır [ağ geçidi SKU'ları](../articles/expressroute/expressroute-about-virtual-network-gateways.md).</span><span class="sxs-lookup"><span data-stu-id="7dfad-110">There are a number of [Gateway SKUs](../articles/expressroute/expressroute-about-virtual-network-gateways.md).</span></span> <span data-ttu-id="7dfad-111">Herhangi bir zamanda komutu toochange hello ağ geçidi SKU'su aşağıdaki hello kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7dfad-111">You can use hello following command toochange hello Gateway SKU at any time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7dfad-112">Bu komut için UltraPerformance ağ geçidi çalışmıyor.</span><span class="sxs-lookup"><span data-stu-id="7dfad-112">This command doesn't work for UltraPerformance gateway.</span></span> <span data-ttu-id="7dfad-113">toochange ağ geçidi tooan UltraPerformance ağ geçidiniz, önce ExpressRoute ağ geçidi mevcut hello kaldırın ve yeni UltraPerformance ağ geçidi oluşturmak.</span><span class="sxs-lookup"><span data-stu-id="7dfad-113">toochange your gateway tooan UltraPerformance gateway, first remove hello existing ExpressRoute gateway, and then create a new UltraPerformance gateway.</span></span> <span data-ttu-id="7dfad-114">toodowngrade önce bir UltraPerformance ağ geçidi, ağ geçidinden Kaldır UltraPerformance ağ geçidi hello ve ardından yeni bir ağ geçidi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7dfad-114">toodowngrade your gateway from an UltraPerformance gateway, first remove hello UltraPerformance gateway, and then create a new gateway.</span></span> 
> 
> 

    Resize-AzureVirtualNetworkGateway -GatewayId <Gateway ID> -GatewaySKU HighPerformance

## <a name="remove-a-gateway"></a><span data-ttu-id="7dfad-115">Bir ağ geçidi kaldırma</span><span class="sxs-lookup"><span data-stu-id="7dfad-115">Remove a gateway</span></span>
<span data-ttu-id="7dfad-116">Bir ağ geçidi tooremove aşağıdaki Hello komutunu kullanın</span><span class="sxs-lookup"><span data-stu-id="7dfad-116">Use hello command below tooremove a gateway</span></span>

    Remove-AzureVirtualNetworkGateway -GatewayId <Gateway ID>