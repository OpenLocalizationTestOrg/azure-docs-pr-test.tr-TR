<span data-ttu-id="e9715-101">Bu görev kullanılacak bir VNet Hello adımları yapılandırma başvuru listesi aşağıdaki hello başlangıç değerleri temel.</span><span class="sxs-lookup"><span data-stu-id="e9715-101">hello steps for this task use a VNet based on hello values in hello following configuration reference list.</span></span> <span data-ttu-id="e9715-102">Ayrıca ek ayarlar ve adları bu listede özetlenmiştir.</span><span class="sxs-lookup"><span data-stu-id="e9715-102">Additional settings and names are also outlined in this list.</span></span> <span data-ttu-id="e9715-103">Bu listedeki hello değerlere göre değişkenler eklediğimiz ancak Biz bu listeyi hello adımlar, doğrudan hiçbirinde kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="e9715-103">We don't use this list directly in any of hello steps, although we do add variables based on hello values in this list.</span></span> <span data-ttu-id="e9715-104">Merhaba değerleri kendi değerlerinizle değiştirerek bir başvuru olarak hello listesi toouse kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e9715-104">You can copy hello list toouse as a reference, replacing hello values with your own.</span></span>

<span data-ttu-id="e9715-105">**Yapılandırma başvuru listesi**</span><span class="sxs-lookup"><span data-stu-id="e9715-105">**Configuration reference list**</span></span>

* <span data-ttu-id="e9715-106">Sanal ağ adı "TestVNet" =</span><span class="sxs-lookup"><span data-stu-id="e9715-106">Virtual Network Name = "TestVNet"</span></span>
* <span data-ttu-id="e9715-107">Sanal ağ adres alanı 192.168.0.0/16 =</span><span class="sxs-lookup"><span data-stu-id="e9715-107">Virtual Network address space = 192.168.0.0/16</span></span>
* <span data-ttu-id="e9715-108">Kaynak grubu "TestRG" =</span><span class="sxs-lookup"><span data-stu-id="e9715-108">Resource Group = "TestRG"</span></span>
* <span data-ttu-id="e9715-109">Subnet1 Name = "Ön uç"</span><span class="sxs-lookup"><span data-stu-id="e9715-109">Subnet1 Name = "FrontEnd"</span></span> 
* <span data-ttu-id="e9715-110">Subnet1 adres alanı "192.168.1.0/24" =</span><span class="sxs-lookup"><span data-stu-id="e9715-110">Subnet1 address space = "192.168.1.0/24"</span></span>
* <span data-ttu-id="e9715-111">Ağ geçidi alt ağ adı: "GatewaySubnet gerekir her zaman adını bir ağ geçidi alt ağı" *GatewaySubnet*.</span><span class="sxs-lookup"><span data-stu-id="e9715-111">Gateway Subnet name: "GatewaySubnet" You must always name a gateway subnet *GatewaySubnet*.</span></span>
* <span data-ttu-id="e9715-112">Ağ geçidi alt ağ adres alanının "192.168.200.0/26" =</span><span class="sxs-lookup"><span data-stu-id="e9715-112">Gateway Subnet address space = "192.168.200.0/26"</span></span>
* <span data-ttu-id="e9715-113">Bölge "Doğu ABD" =</span><span class="sxs-lookup"><span data-stu-id="e9715-113">Region = "East US"</span></span>
* <span data-ttu-id="e9715-114">Ağ geçidi adı "GW" =</span><span class="sxs-lookup"><span data-stu-id="e9715-114">Gateway Name = "GW"</span></span>
* <span data-ttu-id="e9715-115">Ağ geçidi IP adı "GWIP" =</span><span class="sxs-lookup"><span data-stu-id="e9715-115">Gateway IP Name = "GWIP"</span></span>
* <span data-ttu-id="e9715-116">Ağ geçidi IP Yapılandırması adı "gwipconf" =</span><span class="sxs-lookup"><span data-stu-id="e9715-116">Gateway IP configuration Name = "gwipconf"</span></span>
* <span data-ttu-id="e9715-117">Tür = "ExpressRoute" Bu tür bir ExpressRoute yapılandırma için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="e9715-117">Type = "ExpressRoute" This type is required for an ExpressRoute configuration.</span></span>
* <span data-ttu-id="e9715-118">Ağ geçidi genel IP adı "gwpip" =</span><span class="sxs-lookup"><span data-stu-id="e9715-118">Gateway Public IP Name = "gwpip"</span></span>

## <a name="add-a-gateway"></a><span data-ttu-id="e9715-119">Bir ağ geçidi Ekle</span><span class="sxs-lookup"><span data-stu-id="e9715-119">Add a gateway</span></span>
1. <span data-ttu-id="e9715-120">Tooyour Azure aboneliğine bağlayın.</span><span class="sxs-lookup"><span data-stu-id="e9715-120">Connect tooyour Azure Subscription.</span></span>

  ```powershell 
  Login-AzureRmAccount
  Get-AzureRmSubscription 
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
2. <span data-ttu-id="e9715-121">Bu alıştırma için değişkenleri bildirin.</span><span class="sxs-lookup"><span data-stu-id="e9715-121">Declare your variables for this exercise.</span></span> <span data-ttu-id="e9715-122">Emin tooedit toouse istediğiniz hello örnek tooreflect hello ayarlarını olabilir.</span><span class="sxs-lookup"><span data-stu-id="e9715-122">Be sure tooedit hello sample tooreflect hello settings that you want toouse.</span></span>

  ```powershell 
  $RG = "TestRG"
  $Location = "East US"
  $GWName = "GW"
  $GWIPName = "GWIP"
  $GWIPconfName = "gwipconf"
  $VNetName = "TestVNet"
  ```
3. <span data-ttu-id="e9715-123">Merhaba sanal ağ nesnesini bir değişken olarak depolar.</span><span class="sxs-lookup"><span data-stu-id="e9715-123">Store hello virtual network object as a variable.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
  ```
4. <span data-ttu-id="e9715-124">Bir ağ geçidi alt ağı tooyour sanal ağ ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e9715-124">Add a gateway subnet tooyour Virtual Network.</span></span> <span data-ttu-id="e9715-125">Merhaba ağ geçidi alt ağı "GatewaySubnet" şeklinde adlandırılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="e9715-125">hello gateway subnet must be named "GatewaySubnet".</span></span> <span data-ttu-id="e9715-126">/ 27 bir ağ geçidi alt ağı oluşturmanız gerekir veya daha büyük (/ 26, / 25 vb..).</span><span class="sxs-lookup"><span data-stu-id="e9715-126">You should create a gateway subnet that is /27 or larger (/26, /25, etc.).</span></span>

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet -VirtualNetwork $vnet -AddressPrefix 192.168.200.0/26
  ```
5. <span data-ttu-id="e9715-127">Merhaba yapılandırmasını ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="e9715-127">Set hello configuration.</span></span>

  ```powershell
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
6. <span data-ttu-id="e9715-128">Merhaba ağ geçidi alt ağı bir değişken olarak depolar.</span><span class="sxs-lookup"><span data-stu-id="e9715-128">Store hello gateway subnet as a variable.</span></span>

  ```powershell
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
  ```
7. <span data-ttu-id="e9715-129">Genel bir IP adresi isteyin.</span><span class="sxs-lookup"><span data-stu-id="e9715-129">Request a public IP address.</span></span> <span data-ttu-id="e9715-130">Başlangıç IP adresi hello ağ geçidi oluşturmadan önce isteniyor.</span><span class="sxs-lookup"><span data-stu-id="e9715-130">hello IP address is requested before creating hello gateway.</span></span> <span data-ttu-id="e9715-131">Başlangıç IP adresi toouse istediğiniz belirtemezsiniz; dinamik olarak ayrılır.</span><span class="sxs-lookup"><span data-stu-id="e9715-131">You cannot specify hello IP address that you want toouse; it’s dynamically allocated.</span></span> <span data-ttu-id="e9715-132">Merhaba sonraki yapılandırma bölümünde bu IP adresini kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="e9715-132">You'll use this IP address in hello next configuration section.</span></span> <span data-ttu-id="e9715-133">Merhaba AllocationMethod dinamik olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="e9715-133">hello AllocationMethod must be Dynamic.</span></span>

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name $GWIPName  -ResourceGroupName $RG -Location $Location -AllocationMethod Dynamic
  ```
8. <span data-ttu-id="e9715-134">Ağ geçidiniz için başlangıç yapılandırmasını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e9715-134">Create hello configuration for your gateway.</span></span> <span data-ttu-id="e9715-135">Merhaba ağ geçidi yapılandırmasını hello alt ağı ve hello ortak IP adresi toouse tanımlar.</span><span class="sxs-lookup"><span data-stu-id="e9715-135">hello gateway configuration defines hello subnet and hello public IP address toouse.</span></span> <span data-ttu-id="e9715-136">Bu adımda, hello ağ geçidi oluşturduğunuzda, kullanılacak hello yapılandırma belirtiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="e9715-136">In this step, you are specifying hello configuration that will be used when you create hello gateway.</span></span> <span data-ttu-id="e9715-137">Bu adım hello ağ geçidi nesnesi oluşturmaz.</span><span class="sxs-lookup"><span data-stu-id="e9715-137">This step does not actually create hello gateway object.</span></span> <span data-ttu-id="e9715-138">Hello örnek toocreate altında ağ geçidi yapılandırmasını kullanın.</span><span class="sxs-lookup"><span data-stu-id="e9715-138">Use hello sample below toocreate your gateway configuration.</span></span>

  ```powershell
  $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName -Subnet $subnet -PublicIpAddress $pip
  ```
9. <span data-ttu-id="e9715-139">Merhaba ağ geçidi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e9715-139">Create hello gateway.</span></span> <span data-ttu-id="e9715-140">Bu adımda, hello **- GatewayType** özellikle önemlidir.</span><span class="sxs-lookup"><span data-stu-id="e9715-140">In this step, hello **-GatewayType** is especially important.</span></span> <span data-ttu-id="e9715-141">Merhaba değer kullanmalıdır **ExpressRoute**.</span><span class="sxs-lookup"><span data-stu-id="e9715-141">You must use hello value **ExpressRoute**.</span></span> <span data-ttu-id="e9715-142">Bu cmdlet'ler çalıştırdıktan sonra 45 dakika veya daha fazla toocreate hello ağ geçidi alabilir.</span><span class="sxs-lookup"><span data-stu-id="e9715-142">After running these cmdlets, hello gateway can take 45 minutes or more toocreate.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG -Location $Location -IpConfigurations $ipconf -GatewayType Expressroute -GatewaySku Standard
  ```

## <a name="verify-hello-gateway-was-created"></a><span data-ttu-id="e9715-143">Merhaba ağ geçidinin oluşturulduğunu doğrulayın</span><span class="sxs-lookup"><span data-stu-id="e9715-143">Verify hello gateway was created</span></span>
<span data-ttu-id="e9715-144">Ağ geçidi hello tooverify oluşturulan komutlar aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="e9715-144">Use hello following commands tooverify that hello gateway has been created:</span></span>

```powershell
Get-AzureRmVirtualNetworkGateway -ResourceGroupName $RG
```

## <a name="resize-a-gateway"></a><span data-ttu-id="e9715-145">Bir ağ geçidi yeniden boyutlandırma</span><span class="sxs-lookup"><span data-stu-id="e9715-145">Resize a gateway</span></span>
<span data-ttu-id="e9715-146">Bir dizi vardır [ağ geçidi SKU'ları](../articles/expressroute/expressroute-about-virtual-network-gateways.md).</span><span class="sxs-lookup"><span data-stu-id="e9715-146">There are a number of [Gateway SKUs](../articles/expressroute/expressroute-about-virtual-network-gateways.md).</span></span> <span data-ttu-id="e9715-147">Herhangi bir zamanda komutu toochange hello ağ geçidi SKU'su aşağıdaki hello kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e9715-147">You can use hello following command toochange hello Gateway SKU at any time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e9715-148">Bu komut için UltraPerformance ağ geçidi çalışmıyor.</span><span class="sxs-lookup"><span data-stu-id="e9715-148">This command doesn't work for UltraPerformance gateway.</span></span> <span data-ttu-id="e9715-149">toochange ağ geçidi tooan UltraPerformance ağ geçidiniz, önce ExpressRoute ağ geçidi mevcut hello kaldırın ve yeni UltraPerformance ağ geçidi oluşturmak.</span><span class="sxs-lookup"><span data-stu-id="e9715-149">toochange your gateway tooan UltraPerformance gateway, first remove hello existing ExpressRoute gateway, and then create a new UltraPerformance gateway.</span></span> <span data-ttu-id="e9715-150">toodowngrade önce bir UltraPerformance ağ geçidi, ağ geçidinden Kaldır UltraPerformance ağ geçidi hello ve ardından yeni bir ağ geçidi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e9715-150">toodowngrade your gateway from an UltraPerformance gateway, first remove hello UltraPerformance gateway, and then create a new gateway.</span></span>
> 
> 

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku HighPerformance
```

## <a name="remove-a-gateway"></a><span data-ttu-id="e9715-151">Bir ağ geçidi kaldırma</span><span class="sxs-lookup"><span data-stu-id="e9715-151">Remove a gateway</span></span>
<span data-ttu-id="e9715-152">Komut tooremove bir ağ geçidi aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="e9715-152">Use hello following command tooremove a gateway:</span></span>

```powershell
Remove-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
```