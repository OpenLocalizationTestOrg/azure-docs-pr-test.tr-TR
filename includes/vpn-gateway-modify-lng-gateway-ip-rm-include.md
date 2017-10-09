### <span data-ttu-id="3b7cb-101"><a name="gwipnoconnection"></a>toomodify hello yerel ağ geçidi 'Gatewayıpaddress' - ağ geçidi bağlantısı yok</span><span class="sxs-lookup"><span data-stu-id="3b7cb-101"><a name="gwipnoconnection"></a> toomodify hello local network gateway 'GatewayIpAddress' - no gateway connection</span></span>

<span data-ttu-id="3b7cb-102">Tooconnect toohas istediğiniz hello VPN cihazının genel IP adresini değiştirdiyseniz, değişiklik toomodify hello yerel ağ geçidi tooreflect gerekir.</span><span class="sxs-lookup"><span data-stu-id="3b7cb-102">If hello VPN device that you want tooconnect toohas changed its public IP address, you need toomodify hello local network gateway tooreflect that change.</span></span> <span data-ttu-id="3b7cb-103">Merhaba örnek toomodify bir ağ geçidi bağlantısı olmayan yerel ağ geçidi kullanın.</span><span class="sxs-lookup"><span data-stu-id="3b7cb-103">Use hello example toomodify a local network gateway that does not have a gateway connection.</span></span>

<span data-ttu-id="3b7cb-104">Bu değer değiştirirken hello adres öneklerini hello adresindeki de değiştirebilirsiniz aynı anda.</span><span class="sxs-lookup"><span data-stu-id="3b7cb-104">When modifying this value, you can also modify hello address prefixes at hello same time.</span></span> <span data-ttu-id="3b7cb-105">Yerel ağ geçidinizin emin toouse hello varolan adı sipariş toooverwrite hello geçerli ayarları olması.</span><span class="sxs-lookup"><span data-stu-id="3b7cb-105">Be sure toouse hello existing name of your local network gateway in order toooverwrite hello current settings.</span></span> <span data-ttu-id="3b7cb-106">Farklı bir ad kullanırsanız, yeni bir yerel ağ geçidi oluşturma, üzerine yerine var olan bir hello.</span><span class="sxs-lookup"><span data-stu-id="3b7cb-106">If you use a different name, you create a new local network gateway, instead of overwriting hello existing one.</span></span>

```powershell
New-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName `
-Location "West US" -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24') `
-GatewayIpAddress "5.4.3.2" -ResourceGroupName MyRGName
```

### <span data-ttu-id="3b7cb-107"><a name="gwipwithconnection"></a>toomodify hello yerel ağ geçidi 'Gatewayıpaddress' - var olan ağ geçidi bağlantısı</span><span class="sxs-lookup"><span data-stu-id="3b7cb-107"><a name="gwipwithconnection"></a>toomodify hello local network gateway 'GatewayIpAddress' - existing gateway connection</span></span>

<span data-ttu-id="3b7cb-108">Tooconnect toohas istediğiniz hello VPN cihazının genel IP adresini değiştirdiyseniz, değişiklik toomodify hello yerel ağ geçidi tooreflect gerekir.</span><span class="sxs-lookup"><span data-stu-id="3b7cb-108">If hello VPN device that you want tooconnect toohas changed its public IP address, you need toomodify hello local network gateway tooreflect that change.</span></span> <span data-ttu-id="3b7cb-109">Bir ağ geçidi bağlantı zaten varsa, ilk tooremove hello bağlantı gerekir.</span><span class="sxs-lookup"><span data-stu-id="3b7cb-109">If a gateway connection already exists, you first need tooremove hello connection.</span></span> <span data-ttu-id="3b7cb-110">Merhaba bağlantı kaldırıldıktan sonra hello ağ geçidi IP adresi değiştirebilir ve yeni bir bağlantı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3b7cb-110">After hello connection is removed, you can modify hello gateway IP address and recreate a new connection.</span></span> <span data-ttu-id="3b7cb-111">Merhaba adres öneklerini hello adresindeki değiştirebilirsiniz aynı anda.</span><span class="sxs-lookup"><span data-stu-id="3b7cb-111">You can also modify hello address prefixes at hello same time.</span></span> <span data-ttu-id="3b7cb-112">Bunun sonucunda, VPN bağlantınızda kesinti oluşur.</span><span class="sxs-lookup"><span data-stu-id="3b7cb-112">This results in some downtime for your VPN connection.</span></span> <span data-ttu-id="3b7cb-113">Merhaba ağ geçidi IP adresi değiştirirken toodelete hello VPN ağ geçidi gerekmez.</span><span class="sxs-lookup"><span data-stu-id="3b7cb-113">When modifying hello gateway IP address, you don't need toodelete hello VPN gateway.</span></span> <span data-ttu-id="3b7cb-114">Yalnızca tooremove hello bağlantı gerekir.</span><span class="sxs-lookup"><span data-stu-id="3b7cb-114">You only need tooremove hello connection.</span></span>
 

1. <span data-ttu-id="3b7cb-115">Merhaba bağlantısını kaldırın.</span><span class="sxs-lookup"><span data-stu-id="3b7cb-115">Remove hello connection.</span></span> <span data-ttu-id="3b7cb-116">'Get-AzureRmVirtualNetworkGatewayConnection' hello cmdlet'ini kullanarak bağlantınızı hello adını bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3b7cb-116">You can find hello name of your connection by using hello 'Get-AzureRmVirtualNetworkGatewayConnection' cmdlet.</span></span>

  ```powershell
  Remove-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName `
  -ResourceGroupName MyRGName
  ```
2. <span data-ttu-id="3b7cb-117">Merhaba 'Gatewayıpaddress' değerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="3b7cb-117">Modify hello 'GatewayIpAddress' value.</span></span> <span data-ttu-id="3b7cb-118">Merhaba adres öneklerini hello adresindeki değiştirebilirsiniz aynı anda.</span><span class="sxs-lookup"><span data-stu-id="3b7cb-118">You can also modify hello address prefixes at hello same time.</span></span> <span data-ttu-id="3b7cb-119">Yerel ağ geçidi toooverwrite hello geçerli ayarlarınız emin toouse hello varolan adı olması.</span><span class="sxs-lookup"><span data-stu-id="3b7cb-119">Be sure toouse hello existing name of your local network gateway toooverwrite hello current settings.</span></span> <span data-ttu-id="3b7cb-120">Bunu yapmazsanız, yeni bir yerel ağ geçidi oluşturma, varolan bir hello üzerine yerine.</span><span class="sxs-lookup"><span data-stu-id="3b7cb-120">If you don't, you create a new local network gateway, instead of overwriting hello existing one.</span></span>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName `
  -Location "West US" -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24') `
  -GatewayIpAddress "104.40.81.124" -ResourceGroupName MyRGName
  ```
3. <span data-ttu-id="3b7cb-121">Merhaba bağlantı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3b7cb-121">Create hello connection.</span></span> <span data-ttu-id="3b7cb-122">Bu örnekte bir IPsec bağlantı türü yapılandırıyoruz.</span><span class="sxs-lookup"><span data-stu-id="3b7cb-122">In this example, we configure an IPsec connection type.</span></span> <span data-ttu-id="3b7cb-123">Bağlantınızı yeniden oluşturduğunuzda yapılandırmanızla ilgili belirtilen hello bağlantı türünü kullanın.</span><span class="sxs-lookup"><span data-stu-id="3b7cb-123">When you recreate your connection, use hello connection type that is specified for your configuration.</span></span> <span data-ttu-id="3b7cb-124">Merhaba ek bağlantı türleri için bkz: [PowerShell cmdlet'ini](https://msdn.microsoft.com/library/mt603611.aspx) sayfası.</span><span class="sxs-lookup"><span data-stu-id="3b7cb-124">For additional connection types, see hello [PowerShell cmdlet](https://msdn.microsoft.com/library/mt603611.aspx) page.</span></span>  <span data-ttu-id="3b7cb-125">tooobtain hello VirtualNetworkGateway adı hello 'Get-AzureRmVirtualNetworkGateway' cmdlet'i çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3b7cb-125">tooobtain hello VirtualNetworkGateway name, you can run hello 'Get-AzureRmVirtualNetworkGateway' cmdlet.</span></span>
   
    <span data-ttu-id="3b7cb-126">Merhaba değişkenleri ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="3b7cb-126">Set hello variables.</span></span>

  ```powershell
  $local = Get-AzureRMLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
  $vnetgw = Get-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName MyRGName
  ```
   
    <span data-ttu-id="3b7cb-127">Merhaba bağlantı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3b7cb-127">Create hello connection.</span></span>

  ```powershell 
  New-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName -ResourceGroupName MyRGName `
  -Location "West US" `
  -VirtualNetworkGateway1 $vnetgw `
  -LocalNetworkGateway2 $local `
  -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```