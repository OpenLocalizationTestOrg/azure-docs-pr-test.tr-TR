### <span data-ttu-id="63aad-101"><a name="noconnection"></a>Yerel ağ geçidinin IP adresi ön eklerini değiştirmek için - ağ geçidi bağlantısı yok</span><span class="sxs-lookup"><span data-stu-id="63aad-101"><a name="noconnection"></a>To modify local network gateway IP address prefixes - no gateway connection</span></span>

<span data-ttu-id="63aad-102">Başka adres ön ekleri eklemek için:</span><span class="sxs-lookup"><span data-stu-id="63aad-102">To add additional address prefixes:</span></span>

```powershell
$local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
-AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24')
```

<span data-ttu-id="63aad-103">Adres ön eklerini kaldırmak için:</span><span class="sxs-lookup"><span data-stu-id="63aad-103">To remove address prefixes:</span></span><br>
<span data-ttu-id="63aad-104">Artık gereği olmayan önekleri bırakın.</span><span class="sxs-lookup"><span data-stu-id="63aad-104">Leave out the prefixes that you no longer need.</span></span> <span data-ttu-id="63aad-105">Bu örnekte, 20.0.0.0/24 (önceki örnekten) ön eki artık bize gerekmiyor; bu nedenle, yerel ağ geçidini güncelleştiriyor ve bu ön eki hariç tutuyoruz.</span><span class="sxs-lookup"><span data-stu-id="63aad-105">In this example, we no longer need prefix 20.0.0.0/24 (from the previous example), so we update the local network gateway, excluding that prefix.</span></span>

```powershell
$local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
-AddressPrefix @('10.0.0.0/24','30.0.0.0/24')
```

### <span data-ttu-id="63aad-106"><a name="withconnection"></a>Yerel ağ geçidinin IP adresi ön eklerini değiştirmek için - ağ geçidi bağlantısı var</span><span class="sxs-lookup"><span data-stu-id="63aad-106"><a name="withconnection"></a>To modify local network gateway IP address prefixes - existing gateway connection</span></span>

<span data-ttu-id="63aad-107">Ağ geçidi bağlantınız varsa ve yerel ağ geçidinizde bulunan IP adresi ön eklerini eklemek veya kaldırmak istiyorsanız aşağıdaki adımları sırasıyla uygulamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="63aad-107">If you have a gateway connection and want to add or remove the IP address prefixes contained in your local network gateway, you need to do the following steps, in order.</span></span> <span data-ttu-id="63aad-108">Bunun sonucunda, VPN bağlantınızda kesinti oluşur.</span><span class="sxs-lookup"><span data-stu-id="63aad-108">This results in some downtime for your VPN connection.</span></span> <span data-ttu-id="63aad-109">IP adresi öneklerini değiştirirken, VPN ağ geçidini silmeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="63aad-109">When modifying IP address prefixes, you don't need to delete the VPN gateway.</span></span> <span data-ttu-id="63aad-110">Yalnızca bağlantıyı kaldırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="63aad-110">You only need to remove the connection.</span></span>


1. <span data-ttu-id="63aad-111">Bağlantıyı kaldırın.</span><span class="sxs-lookup"><span data-stu-id="63aad-111">Remove the connection.</span></span>

  ```powershell
  Remove-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName -ResourceGroupName MyRGName
  ```
2. <span data-ttu-id="63aad-112">Yerel ağ geçidiniz için adres ön eklerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="63aad-112">Modify the address prefixes for your local network gateway.</span></span>
   
  <span data-ttu-id="63aad-113">LocalNetworkGateway için değişkeni ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="63aad-113">Set the variable for the LocalNetworkGateway.</span></span>

  ```powershell
  $local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName
  ```
   
  <span data-ttu-id="63aad-114">Ön ekleri değiştirin.</span><span class="sxs-lookup"><span data-stu-id="63aad-114">Modify the prefixes.</span></span>
   
  ```powershell
  Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
  -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24')
  ```
3. <span data-ttu-id="63aad-115">Bağlantıyı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="63aad-115">Create the connection.</span></span> <span data-ttu-id="63aad-116">Bu örnekte bir IPsec bağlantı türü yapılandırıyoruz.</span><span class="sxs-lookup"><span data-stu-id="63aad-116">In this example, we configure an IPsec connection type.</span></span> <span data-ttu-id="63aad-117">Bağlantınızı yeniden oluşturduktan sonra, yapılandırmanız için belirtilen bağlantı türünü kullanın.</span><span class="sxs-lookup"><span data-stu-id="63aad-117">When you recreate your connection, use the connection type that is specified for your configuration.</span></span> <span data-ttu-id="63aad-118">Ek bağlantı türleri için [PowerShell cmdlet](https://msdn.microsoft.com/library/mt603611.aspx) sayfasına bakın.</span><span class="sxs-lookup"><span data-stu-id="63aad-118">For additional connection types, see the [PowerShell cmdlet](https://msdn.microsoft.com/library/mt603611.aspx) page.</span></span>
   
  <span data-ttu-id="63aad-119">VirtualNetworkGateway için değişkeni ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="63aad-119">Set the variable for the VirtualNetworkGateway.</span></span>

  ```powershell
  $gateway1 = Get-AzureRmVirtualNetworkGateway -Name RMGateway  -ResourceGroupName MyRGName
  ```
   
  <span data-ttu-id="63aad-120">Bağlantıyı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="63aad-120">Create the connection.</span></span> <span data-ttu-id="63aad-121">Bu örnek 2. adımda ayarladığınız $local değişkenini kullanır.</span><span class="sxs-lookup"><span data-stu-id="63aad-121">This example uses the variable $local that you set in step 2.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName `
  -ResourceGroupName MyRGName -Location 'West US' `
  -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
  -ConnectionType IPsec `
  -RoutingWeight 10 -SharedKey 'abc123'
  ```