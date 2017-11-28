### <span data-ttu-id="19067-101"><a name="gwipnoconnection"></a> 'GatewayIpAddress' yerel ağ geçidini değiştirmek için - ağ geçidi bağlantısı yok</span><span class="sxs-lookup"><span data-stu-id="19067-101"><a name="gwipnoconnection"></a> To modify the local network gateway 'GatewayIpAddress' - no gateway connection</span></span>

<span data-ttu-id="19067-102">Bağlanmak istediğiniz VPN cihazının genel IP adresi değiştiyse, yerel ağ geçidini bu değişikliği yansıtacak şekilde değiştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="19067-102">If the VPN device that you want to connect to has changed its public IP address, you need to modify the local network gateway to reflect that change.</span></span> <span data-ttu-id="19067-103">Ağ geçidi bağlantısı olmayan bir yerel ağ geçidini değiştirmek için örneği kullanın.</span><span class="sxs-lookup"><span data-stu-id="19067-103">Use the example to modify a local network gateway that does not have a gateway connection.</span></span>

<span data-ttu-id="19067-104">Bu değeri değiştirirken aynı zamanda adres ön eklerini de değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="19067-104">When modifying this value, you can also modify the address prefixes at the same time.</span></span> <span data-ttu-id="19067-105">Geçerli ayarların üzerine yazmak için yerel ağ geçidinizin mevcut adını kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="19067-105">Be sure to use the existing name of your local network gateway in order to overwrite the current settings.</span></span> <span data-ttu-id="19067-106">Farklı bir ad kullanırsanız mevcut olanın üzerine yazmak yerine yeni bir yerel ağ geçidi oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="19067-106">If you use a different name, you create a new local network gateway, instead of overwriting the existing one.</span></span>

```powershell
New-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName `
-Location "West US" -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24') `
-GatewayIpAddress "5.4.3.2" -ResourceGroupName MyRGName
```

### <span data-ttu-id="19067-107"><a name="gwipwithconnection"></a> 'GatewayIpAddress' yerel ağ geçidini değiştirmek için - ağ geçidi bağlantısı var</span><span class="sxs-lookup"><span data-stu-id="19067-107"><a name="gwipwithconnection"></a>To modify the local network gateway 'GatewayIpAddress' - existing gateway connection</span></span>

<span data-ttu-id="19067-108">Bağlanmak istediğiniz VPN cihazının genel IP adresi değiştiyse, yerel ağ geçidini bu değişikliği yansıtacak şekilde değiştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="19067-108">If the VPN device that you want to connect to has changed its public IP address, you need to modify the local network gateway to reflect that change.</span></span> <span data-ttu-id="19067-109">Zaten bir ağ geçidi bağlantısı varsa öncelikle bu bağlantıyı kaldırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="19067-109">If a gateway connection already exists, you first need to remove the connection.</span></span> <span data-ttu-id="19067-110">Bağlantı kaldırıldıktan sonra ağ geçidi IP adresini değiştirebilir ve yeni bir bağlantı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="19067-110">After the connection is removed, you can modify the gateway IP address and recreate a new connection.</span></span> <span data-ttu-id="19067-111">Aynı zamanda adres ön eklerini de değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="19067-111">You can also modify the address prefixes at the same time.</span></span> <span data-ttu-id="19067-112">Bunun sonucunda, VPN bağlantınızda kesinti oluşur.</span><span class="sxs-lookup"><span data-stu-id="19067-112">This results in some downtime for your VPN connection.</span></span> <span data-ttu-id="19067-113">Ağ geçidi IP adresini değiştirirken, VPN ağ geçidini silmeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="19067-113">When modifying the gateway IP address, you don't need to delete the VPN gateway.</span></span> <span data-ttu-id="19067-114">Yalnızca bağlantıyı kaldırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="19067-114">You only need to remove the connection.</span></span>
 

1. <span data-ttu-id="19067-115">Bağlantıyı kaldırın.</span><span class="sxs-lookup"><span data-stu-id="19067-115">Remove the connection.</span></span> <span data-ttu-id="19067-116">'Get-AzureRmVirtualNetworkGatewayConnection' cmdlet’ini kullanarak bağlantınızın adını bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="19067-116">You can find the name of your connection by using the 'Get-AzureRmVirtualNetworkGatewayConnection' cmdlet.</span></span>

  ```powershell
  Remove-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName `
  -ResourceGroupName MyRGName
  ```
2. <span data-ttu-id="19067-117">'GatewayIpAddress' değerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="19067-117">Modify the 'GatewayIpAddress' value.</span></span> <span data-ttu-id="19067-118">Aynı zamanda adres ön eklerini de değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="19067-118">You can also modify the address prefixes at the same time.</span></span> <span data-ttu-id="19067-119">Geçerli ayarların üzerine yazmak için yerel ağ geçidinizin mevcut adını kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="19067-119">Be sure to use the existing name of your local network gateway to overwrite the current settings.</span></span> <span data-ttu-id="19067-120">Bunu kullanmazsanız, mevcut olanın üzerine yazmak yerine yeni bir yerel ağ geçidi oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="19067-120">If you don't, you create a new local network gateway, instead of overwriting the existing one.</span></span>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName `
  -Location "West US" -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24') `
  -GatewayIpAddress "104.40.81.124" -ResourceGroupName MyRGName
  ```
3. <span data-ttu-id="19067-121">Bağlantıyı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="19067-121">Create the connection.</span></span> <span data-ttu-id="19067-122">Bu örnekte bir IPsec bağlantı türü yapılandırıyoruz.</span><span class="sxs-lookup"><span data-stu-id="19067-122">In this example, we configure an IPsec connection type.</span></span> <span data-ttu-id="19067-123">Bağlantınızı yeniden oluşturduktan sonra, yapılandırmanız için belirtilen bağlantı türünü kullanın.</span><span class="sxs-lookup"><span data-stu-id="19067-123">When you recreate your connection, use the connection type that is specified for your configuration.</span></span> <span data-ttu-id="19067-124">Ek bağlantı türleri için [PowerShell cmdlet](https://msdn.microsoft.com/library/mt603611.aspx) sayfasına bakın.</span><span class="sxs-lookup"><span data-stu-id="19067-124">For additional connection types, see the [PowerShell cmdlet](https://msdn.microsoft.com/library/mt603611.aspx) page.</span></span>  <span data-ttu-id="19067-125">VirtualNetworkGateway adını almak için 'Get-AzureRmVirtualNetworkGateway' cmdlet'ini çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="19067-125">To obtain the VirtualNetworkGateway name, you can run the 'Get-AzureRmVirtualNetworkGateway' cmdlet.</span></span>
   
    <span data-ttu-id="19067-126">Değişkenleri ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="19067-126">Set the variables.</span></span>

  ```powershell
  $local = Get-AzureRMLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
  $vnetgw = Get-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName MyRGName
  ```
   
    <span data-ttu-id="19067-127">Bağlantıyı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="19067-127">Create the connection.</span></span>

  ```powershell 
  New-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName -ResourceGroupName MyRGName `
  -Location "West US" `
  -VirtualNetworkGateway1 $vnetgw `
  -LocalNetworkGateway2 $local `
  -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```