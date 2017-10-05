<span data-ttu-id="b3ad6-101">Bu görev için adımlar aşağıdaki yapılandırma başvuru listesinde değerlere dayalı bir sanal ağ kullanın.</span><span class="sxs-lookup"><span data-stu-id="b3ad6-101">The steps for this task use a VNet based on the values in the following configuration reference list.</span></span> <span data-ttu-id="b3ad6-102">Ayrıca ek ayarlar ve adları bu listede özetlenmiştir.</span><span class="sxs-lookup"><span data-stu-id="b3ad6-102">Additional settings and names are also outlined in this list.</span></span> <span data-ttu-id="b3ad6-103">Bu listedeki değerlerin temelinde değişkenleri eklediğimiz ancak Biz bu listeyi adımları, doğrudan hiçbirinde kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="b3ad6-103">We don't use this list directly in any of the steps, although we do add variables based on the values in this list.</span></span> <span data-ttu-id="b3ad6-104">Değerleri kendinizinkilerle değiştirerek bir başvuru olarak kullanılacak listesini kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b3ad6-104">You can copy the list to use as a reference, replacing the values with your own.</span></span>

<span data-ttu-id="b3ad6-105">**Yapılandırma başvuru listesi**</span><span class="sxs-lookup"><span data-stu-id="b3ad6-105">**Configuration reference list**</span></span>

* <span data-ttu-id="b3ad6-106">Sanal ağ adı "TestVNet" =</span><span class="sxs-lookup"><span data-stu-id="b3ad6-106">Virtual Network Name = "TestVNet"</span></span>
* <span data-ttu-id="b3ad6-107">Sanal ağ adres alanı 192.168.0.0/16 =</span><span class="sxs-lookup"><span data-stu-id="b3ad6-107">Virtual Network address space = 192.168.0.0/16</span></span>
* <span data-ttu-id="b3ad6-108">Kaynak grubu "TestRG" =</span><span class="sxs-lookup"><span data-stu-id="b3ad6-108">Resource Group = "TestRG"</span></span>
* <span data-ttu-id="b3ad6-109">Subnet1 Name = "Ön uç"</span><span class="sxs-lookup"><span data-stu-id="b3ad6-109">Subnet1 Name = "FrontEnd"</span></span> 
* <span data-ttu-id="b3ad6-110">Subnet1 adres alanı "192.168.1.0/24" =</span><span class="sxs-lookup"><span data-stu-id="b3ad6-110">Subnet1 address space = "192.168.1.0/24"</span></span>
* <span data-ttu-id="b3ad6-111">Ağ geçidi alt ağ adı: "GatewaySubnet gerekir her zaman adını bir ağ geçidi alt ağı" *GatewaySubnet*.</span><span class="sxs-lookup"><span data-stu-id="b3ad6-111">Gateway Subnet name: "GatewaySubnet" You must always name a gateway subnet *GatewaySubnet*.</span></span>
* <span data-ttu-id="b3ad6-112">Ağ geçidi alt ağ adres alanının "192.168.200.0/26" =</span><span class="sxs-lookup"><span data-stu-id="b3ad6-112">Gateway Subnet address space = "192.168.200.0/26"</span></span>
* <span data-ttu-id="b3ad6-113">Bölge "Doğu ABD" =</span><span class="sxs-lookup"><span data-stu-id="b3ad6-113">Region = "East US"</span></span>
* <span data-ttu-id="b3ad6-114">Ağ geçidi adı "GW" =</span><span class="sxs-lookup"><span data-stu-id="b3ad6-114">Gateway Name = "GW"</span></span>
* <span data-ttu-id="b3ad6-115">Ağ geçidi IP adı "GWIP" =</span><span class="sxs-lookup"><span data-stu-id="b3ad6-115">Gateway IP Name = "GWIP"</span></span>
* <span data-ttu-id="b3ad6-116">Ağ geçidi IP Yapılandırması adı "gwipconf" =</span><span class="sxs-lookup"><span data-stu-id="b3ad6-116">Gateway IP configuration Name = "gwipconf"</span></span>
* <span data-ttu-id="b3ad6-117">Tür = "ExpressRoute" Bu tür bir ExpressRoute yapılandırma için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="b3ad6-117">Type = "ExpressRoute" This type is required for an ExpressRoute configuration.</span></span>
* <span data-ttu-id="b3ad6-118">Ağ geçidi genel IP adı "gwpip" =</span><span class="sxs-lookup"><span data-stu-id="b3ad6-118">Gateway Public IP Name = "gwpip"</span></span>

## <a name="add-a-gateway"></a><span data-ttu-id="b3ad6-119">Bir ağ geçidi Ekle</span><span class="sxs-lookup"><span data-stu-id="b3ad6-119">Add a gateway</span></span>
1. <span data-ttu-id="b3ad6-120">Azure aboneliğinize bağlanma.</span><span class="sxs-lookup"><span data-stu-id="b3ad6-120">Connect to your Azure Subscription.</span></span>

  ```powershell 
  Login-AzureRmAccount
  Get-AzureRmSubscription 
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
2. <span data-ttu-id="b3ad6-121">Bu alıştırma için değişkenleri bildirin.</span><span class="sxs-lookup"><span data-stu-id="b3ad6-121">Declare your variables for this exercise.</span></span> <span data-ttu-id="b3ad6-122">Kullanmak istediğiniz ayarları yansıtacak şekilde örneği düzenlemek emin olun.</span><span class="sxs-lookup"><span data-stu-id="b3ad6-122">Be sure to edit the sample to reflect the settings that you want to use.</span></span>

  ```powershell 
  $RG = "TestRG"
  $Location = "East US"
  $GWName = "GW"
  $GWIPName = "GWIP"
  $GWIPconfName = "gwipconf"
  $VNetName = "TestVNet"
  ```
3. <span data-ttu-id="b3ad6-123">Sanal ağ nesnesini bir değişken olarak depolar.</span><span class="sxs-lookup"><span data-stu-id="b3ad6-123">Store the virtual network object as a variable.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
  ```
4. <span data-ttu-id="b3ad6-124">Bir ağ geçidi alt ağı, sanal ağınıza ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b3ad6-124">Add a gateway subnet to your Virtual Network.</span></span> <span data-ttu-id="b3ad6-125">Ağ geçidi alt ağı "GatewaySubnet" şeklinde adlandırılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b3ad6-125">The gateway subnet must be named "GatewaySubnet".</span></span> <span data-ttu-id="b3ad6-126">/ 27 bir ağ geçidi alt ağı oluşturmanız gerekir veya daha büyük (/ 26, / 25 vb..).</span><span class="sxs-lookup"><span data-stu-id="b3ad6-126">You should create a gateway subnet that is /27 or larger (/26, /25, etc.).</span></span>

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet -VirtualNetwork $vnet -AddressPrefix 192.168.200.0/26
  ```
5. <span data-ttu-id="b3ad6-127">Yapılandırmayı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="b3ad6-127">Set the configuration.</span></span>

  ```powershell
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
6. <span data-ttu-id="b3ad6-128">Ağ geçidi alt ağı bir değişken olarak depolar.</span><span class="sxs-lookup"><span data-stu-id="b3ad6-128">Store the gateway subnet as a variable.</span></span>

  ```powershell
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
  ```
7. <span data-ttu-id="b3ad6-129">Genel bir IP adresi isteyin.</span><span class="sxs-lookup"><span data-stu-id="b3ad6-129">Request a public IP address.</span></span> <span data-ttu-id="b3ad6-130">IP adresi ağ geçidi oluşturmadan önce isteniyor.</span><span class="sxs-lookup"><span data-stu-id="b3ad6-130">The IP address is requested before creating the gateway.</span></span> <span data-ttu-id="b3ad6-131">Kullanmak istediğiniz IP adresini belirtemezsiniz; dinamik olarak ayrılır.</span><span class="sxs-lookup"><span data-stu-id="b3ad6-131">You cannot specify the IP address that you want to use; it’s dynamically allocated.</span></span> <span data-ttu-id="b3ad6-132">Sonraki yapılandırma bölümünde bu IP adresini kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="b3ad6-132">You'll use this IP address in the next configuration section.</span></span> <span data-ttu-id="b3ad6-133">AllocationMethod dinamik olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b3ad6-133">The AllocationMethod must be Dynamic.</span></span>

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name $GWIPName  -ResourceGroupName $RG -Location $Location -AllocationMethod Dynamic
  ```
8. <span data-ttu-id="b3ad6-134">Ağ geçidi yapılandırmasını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b3ad6-134">Create the configuration for your gateway.</span></span> <span data-ttu-id="b3ad6-135">Ağ geçidi yapılandırması, kullanılacak alt ağı ve genel IP adresini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="b3ad6-135">The gateway configuration defines the subnet and the public IP address to use.</span></span> <span data-ttu-id="b3ad6-136">Bu adımda, ağ geçidi oluşturduğunuzda, kullanılacak yapılandırma belirtiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="b3ad6-136">In this step, you are specifying the configuration that will be used when you create the gateway.</span></span> <span data-ttu-id="b3ad6-137">Bu adım ağ geçidi nesnesi oluşturmaz.</span><span class="sxs-lookup"><span data-stu-id="b3ad6-137">This step does not actually create the gateway object.</span></span> <span data-ttu-id="b3ad6-138">Aşağıdaki örneği kullanarak kendi ağ geçidi yapılandırmanızı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b3ad6-138">Use the sample below to create your gateway configuration.</span></span>

  ```powershell
  $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName -Subnet $subnet -PublicIpAddress $pip
  ```
9. <span data-ttu-id="b3ad6-139">Ağ geçidi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b3ad6-139">Create the gateway.</span></span> <span data-ttu-id="b3ad6-140">Bu adımda, **- GatewayType** özellikle önemlidir.</span><span class="sxs-lookup"><span data-stu-id="b3ad6-140">In this step, the **-GatewayType** is especially important.</span></span> <span data-ttu-id="b3ad6-141">Değer kullanmalıdır **ExpressRoute**.</span><span class="sxs-lookup"><span data-stu-id="b3ad6-141">You must use the value **ExpressRoute**.</span></span> <span data-ttu-id="b3ad6-142">Bu cmdlet'ler çalıştırdıktan sonra ağ geçidi 45 dakika veya oluşturmak için daha fazla sürebilir.</span><span class="sxs-lookup"><span data-stu-id="b3ad6-142">After running these cmdlets, the gateway can take 45 minutes or more to create.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG -Location $Location -IpConfigurations $ipconf -GatewayType Expressroute -GatewaySku Standard
  ```

## <a name="verify-the-gateway-was-created"></a><span data-ttu-id="b3ad6-143">Ağ geçidinin oluşturulduğunu doğrulayın</span><span class="sxs-lookup"><span data-stu-id="b3ad6-143">Verify the gateway was created</span></span>
<span data-ttu-id="b3ad6-144">Ağ geçidinin oluşturulduğunu doğrulamak için aşağıdaki komutları kullanın:</span><span class="sxs-lookup"><span data-stu-id="b3ad6-144">Use the following commands to verify that the gateway has been created:</span></span>

```powershell
Get-AzureRmVirtualNetworkGateway -ResourceGroupName $RG
```

## <a name="resize-a-gateway"></a><span data-ttu-id="b3ad6-145">Bir ağ geçidi yeniden boyutlandırma</span><span class="sxs-lookup"><span data-stu-id="b3ad6-145">Resize a gateway</span></span>
<span data-ttu-id="b3ad6-146">Bir dizi vardır [ağ geçidi SKU'ları](../articles/expressroute/expressroute-about-virtual-network-gateways.md).</span><span class="sxs-lookup"><span data-stu-id="b3ad6-146">There are a number of [Gateway SKUs](../articles/expressroute/expressroute-about-virtual-network-gateways.md).</span></span> <span data-ttu-id="b3ad6-147">Ağ geçidi SKU'su herhangi bir zamanda değiştirmek için aşağıdaki komutu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b3ad6-147">You can use the following command to change the Gateway SKU at any time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b3ad6-148">Bu komut için UltraPerformance ağ geçidi çalışmıyor.</span><span class="sxs-lookup"><span data-stu-id="b3ad6-148">This command doesn't work for UltraPerformance gateway.</span></span> <span data-ttu-id="b3ad6-149">UltraPerformance ağ geçidi için ağ geçidiniz değiştirmek için önce varolan ExpressRoute ağ geçidi kaldırın ve yeni UltraPerformance ağ geçidi oluşturmak.</span><span class="sxs-lookup"><span data-stu-id="b3ad6-149">To change your gateway to an UltraPerformance gateway, first remove the existing ExpressRoute gateway, and then create a new UltraPerformance gateway.</span></span> <span data-ttu-id="b3ad6-150">Ağ geçidiniz UltraPerformance geçidinden düşürmek için ilk UltraPerformance ağ geçidi kaldırın ve ardından yeni bir ağ geçidi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b3ad6-150">To downgrade your gateway from an UltraPerformance gateway, first remove the UltraPerformance gateway, and then create a new gateway.</span></span>
> 
> 

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku HighPerformance
```

## <a name="remove-a-gateway"></a><span data-ttu-id="b3ad6-151">Bir ağ geçidi kaldırma</span><span class="sxs-lookup"><span data-stu-id="b3ad6-151">Remove a gateway</span></span>
<span data-ttu-id="b3ad6-152">Bir ağ geçidini kaldırmak için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="b3ad6-152">Use the following command to remove a gateway:</span></span>

```powershell
Remove-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
```