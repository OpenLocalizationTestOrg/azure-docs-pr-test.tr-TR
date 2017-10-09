### <a name="gwipnoconnection"></a>toomodify hello yerel ağ geçidi 'Gatewayıpaddress' - ağ geçidi bağlantısı yok

Tooconnect toohas istediğiniz hello VPN cihazının genel IP adresini değiştirdiyseniz, değişiklik toomodify hello yerel ağ geçidi tooreflect gerekir. Merhaba örnek toomodify bir ağ geçidi bağlantısı olmayan yerel ağ geçidi kullanın.

Bu değer değiştirirken hello adres öneklerini hello adresindeki de değiştirebilirsiniz aynı anda. Yerel ağ geçidinizin emin toouse hello varolan adı sipariş toooverwrite hello geçerli ayarları olması. Farklı bir ad kullanırsanız, yeni bir yerel ağ geçidi oluşturma, üzerine yerine var olan bir hello.

```powershell
New-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName `
-Location "West US" -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24') `
-GatewayIpAddress "5.4.3.2" -ResourceGroupName MyRGName
```

### <a name="gwipwithconnection"></a>toomodify hello yerel ağ geçidi 'Gatewayıpaddress' - var olan ağ geçidi bağlantısı

Tooconnect toohas istediğiniz hello VPN cihazının genel IP adresini değiştirdiyseniz, değişiklik toomodify hello yerel ağ geçidi tooreflect gerekir. Bir ağ geçidi bağlantı zaten varsa, ilk tooremove hello bağlantı gerekir. Merhaba bağlantı kaldırıldıktan sonra hello ağ geçidi IP adresi değiştirebilir ve yeni bir bağlantı oluşturun. Merhaba adres öneklerini hello adresindeki değiştirebilirsiniz aynı anda. Bunun sonucunda, VPN bağlantınızda kesinti oluşur. Merhaba ağ geçidi IP adresi değiştirirken toodelete hello VPN ağ geçidi gerekmez. Yalnızca tooremove hello bağlantı gerekir.
 

1. Merhaba bağlantısını kaldırın. 'Get-AzureRmVirtualNetworkGatewayConnection' hello cmdlet'ini kullanarak bağlantınızı hello adını bulabilirsiniz.

  ```powershell
  Remove-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName `
  -ResourceGroupName MyRGName
  ```
2. Merhaba 'Gatewayıpaddress' değerini değiştirin. Merhaba adres öneklerini hello adresindeki değiştirebilirsiniz aynı anda. Yerel ağ geçidi toooverwrite hello geçerli ayarlarınız emin toouse hello varolan adı olması. Bunu yapmazsanız, yeni bir yerel ağ geçidi oluşturma, varolan bir hello üzerine yerine.

  ```powershell
  New-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName `
  -Location "West US" -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24') `
  -GatewayIpAddress "104.40.81.124" -ResourceGroupName MyRGName
  ```
3. Merhaba bağlantı oluşturun. Bu örnekte bir IPsec bağlantı türü yapılandırıyoruz. Bağlantınızı yeniden oluşturduğunuzda yapılandırmanızla ilgili belirtilen hello bağlantı türünü kullanın. Merhaba ek bağlantı türleri için bkz: [PowerShell cmdlet'ini](https://msdn.microsoft.com/library/mt603611.aspx) sayfası.  tooobtain hello VirtualNetworkGateway adı hello 'Get-AzureRmVirtualNetworkGateway' cmdlet'i çalıştırabilirsiniz.
   
    Merhaba değişkenleri ayarlayın.

  ```powershell
  $local = Get-AzureRMLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
  $vnetgw = Get-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName MyRGName
  ```
   
    Merhaba bağlantı oluşturun.

  ```powershell 
  New-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName -ResourceGroupName MyRGName `
  -Location "West US" `
  -VirtualNetworkGateway1 $vnetgw `
  -LocalNetworkGateway2 $local `
  -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```