### <span data-ttu-id="42596-101"><a name="noconnection"></a>toomodify yerel ağ geçidi IP adresi öneklerini - ağ geçidi bağlantısı yok</span><span class="sxs-lookup"><span data-stu-id="42596-101"><a name="noconnection"></a>toomodify local network gateway IP address prefixes - no gateway connection</span></span>

<span data-ttu-id="42596-102">tooadd ek adres öneklerini:</span><span class="sxs-lookup"><span data-stu-id="42596-102">tooadd additional address prefixes:</span></span>

```powershell
$local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
-AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24')
```

<span data-ttu-id="42596-103">tooremove adres öneklerini:</span><span class="sxs-lookup"><span data-stu-id="42596-103">tooremove address prefixes:</span></span><br>
<span data-ttu-id="42596-104">Artık ihtiyaç duymadığınız hello önekleri bırakın.</span><span class="sxs-lookup"><span data-stu-id="42596-104">Leave out hello prefixes that you no longer need.</span></span> <span data-ttu-id="42596-105">Bu örnekte, biz artık 20.0.0.0/24 öneki hello yerel ağ geçidi güncelleştiriyoruz şekilde bu önek (Merhaba önceki örnekten) dışında.</span><span class="sxs-lookup"><span data-stu-id="42596-105">In this example, we no longer need prefix 20.0.0.0/24 (from hello previous example), so we update hello local network gateway, excluding that prefix.</span></span>

```powershell
$local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
-AddressPrefix @('10.0.0.0/24','30.0.0.0/24')
```

### <span data-ttu-id="42596-106"><a name="withconnection"></a>ağ geçidi bağlantısı varolan toomodify yerel ağ geçidi IP adresi öneklerini-</span><span class="sxs-lookup"><span data-stu-id="42596-106"><a name="withconnection"></a>toomodify local network gateway IP address prefixes - existing gateway connection</span></span>

<span data-ttu-id="42596-107">Bir ağ geçidi bağlantısına sahip ve tooadd istediğiniz veya yerel ağ geçidinizinde başlangıç IP adresi öneklerini kaldırırsanız, aşağıdaki adımları sırayla toodo hello gerekir.</span><span class="sxs-lookup"><span data-stu-id="42596-107">If you have a gateway connection and want tooadd or remove hello IP address prefixes contained in your local network gateway, you need toodo hello following steps, in order.</span></span> <span data-ttu-id="42596-108">Bunun sonucunda, VPN bağlantınızda kesinti oluşur.</span><span class="sxs-lookup"><span data-stu-id="42596-108">This results in some downtime for your VPN connection.</span></span> <span data-ttu-id="42596-109">IP adres öneklerini değiştirirken toodelete hello VPN ağ geçidi gerekmez.</span><span class="sxs-lookup"><span data-stu-id="42596-109">When modifying IP address prefixes, you don't need toodelete hello VPN gateway.</span></span> <span data-ttu-id="42596-110">Yalnızca tooremove hello bağlantı gerekir.</span><span class="sxs-lookup"><span data-stu-id="42596-110">You only need tooremove hello connection.</span></span>


1. <span data-ttu-id="42596-111">Merhaba bağlantısını kaldırın.</span><span class="sxs-lookup"><span data-stu-id="42596-111">Remove hello connection.</span></span>

  ```powershell
  Remove-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName -ResourceGroupName MyRGName
  ```
2. <span data-ttu-id="42596-112">Yerel ağ geçidinizin Hello adres öneklerini değiştirme.</span><span class="sxs-lookup"><span data-stu-id="42596-112">Modify hello address prefixes for your local network gateway.</span></span>
   
  <span data-ttu-id="42596-113">Merhaba LocalNetworkGateway Hello değişken ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="42596-113">Set hello variable for hello LocalNetworkGateway.</span></span>

  ```powershell
  $local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName
  ```
   
  <span data-ttu-id="42596-114">Hello öneklerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="42596-114">Modify hello prefixes.</span></span>
   
  ```powershell
  Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
  -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24')
  ```
3. <span data-ttu-id="42596-115">Merhaba bağlantı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="42596-115">Create hello connection.</span></span> <span data-ttu-id="42596-116">Bu örnekte bir IPsec bağlantı türü yapılandırıyoruz.</span><span class="sxs-lookup"><span data-stu-id="42596-116">In this example, we configure an IPsec connection type.</span></span> <span data-ttu-id="42596-117">Bağlantınızı yeniden oluşturduğunuzda yapılandırmanızla ilgili belirtilen hello bağlantı türünü kullanın.</span><span class="sxs-lookup"><span data-stu-id="42596-117">When you recreate your connection, use hello connection type that is specified for your configuration.</span></span> <span data-ttu-id="42596-118">Merhaba ek bağlantı türleri için bkz: [PowerShell cmdlet'ini](https://msdn.microsoft.com/library/mt603611.aspx) sayfası.</span><span class="sxs-lookup"><span data-stu-id="42596-118">For additional connection types, see hello [PowerShell cmdlet](https://msdn.microsoft.com/library/mt603611.aspx) page.</span></span>
   
  <span data-ttu-id="42596-119">Merhaba VirtualNetworkGateway Hello değişken ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="42596-119">Set hello variable for hello VirtualNetworkGateway.</span></span>

  ```powershell
  $gateway1 = Get-AzureRmVirtualNetworkGateway -Name RMGateway  -ResourceGroupName MyRGName
  ```
   
  <span data-ttu-id="42596-120">Merhaba bağlantı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="42596-120">Create hello connection.</span></span> <span data-ttu-id="42596-121">Bu örnek hello değişkeni 2. adımda ayarladığınız $local kullanır.</span><span class="sxs-lookup"><span data-stu-id="42596-121">This example uses hello variable $local that you set in step 2.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName `
  -ResourceGroupName MyRGName -Location 'West US' `
  -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
  -ConnectionType IPsec `
  -RoutingWeight 10 -SharedKey 'abc123'
  ```