Bu görev kullanılacak bir VNet Hello adımları yapılandırma başvuru listesi aşağıdaki hello başlangıç değerleri temel. Ayrıca ek ayarlar ve adları bu listede özetlenmiştir. Bu listedeki hello değerlere göre değişkenler eklediğimiz ancak Biz bu listeyi hello adımlar, doğrudan hiçbirinde kullanmayın. Merhaba değerleri kendi değerlerinizle değiştirerek bir başvuru olarak hello listesi toouse kopyalayabilirsiniz.

**Yapılandırma başvuru listesi**

* Sanal ağ adı "TestVNet" =
* Sanal ağ adres alanı 192.168.0.0/16 =
* Kaynak grubu "TestRG" =
* Subnet1 Name = "Ön uç" 
* Subnet1 adres alanı "192.168.1.0/24" =
* Ağ geçidi alt ağ adı: "GatewaySubnet gerekir her zaman adını bir ağ geçidi alt ağı" *GatewaySubnet*.
* Ağ geçidi alt ağ adres alanının "192.168.200.0/26" =
* Bölge "Doğu ABD" =
* Ağ geçidi adı "GW" =
* Ağ geçidi IP adı "GWIP" =
* Ağ geçidi IP Yapılandırması adı "gwipconf" =
* Tür = "ExpressRoute" Bu tür bir ExpressRoute yapılandırma için gereklidir.
* Ağ geçidi genel IP adı "gwpip" =

## <a name="add-a-gateway"></a>Bir ağ geçidi Ekle
1. Tooyour Azure aboneliğine bağlayın.

  ```powershell 
  Login-AzureRmAccount
  Get-AzureRmSubscription 
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
2. Bu alıştırma için değişkenleri bildirin. Emin tooedit toouse istediğiniz hello örnek tooreflect hello ayarlarını olabilir.

  ```powershell 
  $RG = "TestRG"
  $Location = "East US"
  $GWName = "GW"
  $GWIPName = "GWIP"
  $GWIPconfName = "gwipconf"
  $VNetName = "TestVNet"
  ```
3. Merhaba sanal ağ nesnesini bir değişken olarak depolar.

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
  ```
4. Bir ağ geçidi alt ağı tooyour sanal ağ ekleyin. Merhaba ağ geçidi alt ağı "GatewaySubnet" şeklinde adlandırılmalıdır. / 27 bir ağ geçidi alt ağı oluşturmanız gerekir veya daha büyük (/ 26, / 25 vb..).

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet -VirtualNetwork $vnet -AddressPrefix 192.168.200.0/26
  ```
5. Merhaba yapılandırmasını ayarlayın.

  ```powershell
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
6. Merhaba ağ geçidi alt ağı bir değişken olarak depolar.

  ```powershell
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
  ```
7. Genel bir IP adresi isteyin. Başlangıç IP adresi hello ağ geçidi oluşturmadan önce isteniyor. Başlangıç IP adresi toouse istediğiniz belirtemezsiniz; dinamik olarak ayrılır. Merhaba sonraki yapılandırma bölümünde bu IP adresini kullanacaksınız. Merhaba AllocationMethod dinamik olması gerekir.

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name $GWIPName  -ResourceGroupName $RG -Location $Location -AllocationMethod Dynamic
  ```
8. Ağ geçidiniz için başlangıç yapılandırmasını oluşturun. Merhaba ağ geçidi yapılandırmasını hello alt ağı ve hello ortak IP adresi toouse tanımlar. Bu adımda, hello ağ geçidi oluşturduğunuzda, kullanılacak hello yapılandırma belirtiyorsanız. Bu adım hello ağ geçidi nesnesi oluşturmaz. Hello örnek toocreate altında ağ geçidi yapılandırmasını kullanın.

  ```powershell
  $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName -Subnet $subnet -PublicIpAddress $pip
  ```
9. Merhaba ağ geçidi oluşturun. Bu adımda, hello **- GatewayType** özellikle önemlidir. Merhaba değer kullanmalıdır **ExpressRoute**. Bu cmdlet'ler çalıştırdıktan sonra 45 dakika veya daha fazla toocreate hello ağ geçidi alabilir.

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG -Location $Location -IpConfigurations $ipconf -GatewayType Expressroute -GatewaySku Standard
  ```

## <a name="verify-hello-gateway-was-created"></a>Merhaba ağ geçidinin oluşturulduğunu doğrulayın
Ağ geçidi hello tooverify oluşturulan komutlar aşağıdaki hello kullan:

```powershell
Get-AzureRmVirtualNetworkGateway -ResourceGroupName $RG
```

## <a name="resize-a-gateway"></a>Bir ağ geçidi yeniden boyutlandırma
Bir dizi vardır [ağ geçidi SKU'ları](../articles/expressroute/expressroute-about-virtual-network-gateways.md). Herhangi bir zamanda komutu toochange hello ağ geçidi SKU'su aşağıdaki hello kullanabilirsiniz.

> [!IMPORTANT]
> Bu komut için UltraPerformance ağ geçidi çalışmıyor. toochange ağ geçidi tooan UltraPerformance ağ geçidiniz, önce ExpressRoute ağ geçidi mevcut hello kaldırın ve yeni UltraPerformance ağ geçidi oluşturmak. toodowngrade önce bir UltraPerformance ağ geçidi, ağ geçidinden Kaldır UltraPerformance ağ geçidi hello ve ardından yeni bir ağ geçidi oluşturun.
> 
> 

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku HighPerformance
```

## <a name="remove-a-gateway"></a>Bir ağ geçidi kaldırma
Komut tooremove bir ağ geçidi aşağıdaki hello kullan:

```powershell
Remove-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
```