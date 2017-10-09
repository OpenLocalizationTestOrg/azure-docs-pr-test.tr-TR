### <a name="noconnection"></a>toomodify yerel ağ geçidi IP adresi öneklerini - ağ geçidi bağlantısı yok

tooadd ek adres öneklerini:

```powershell
$local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
-AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24')
```

tooremove adres öneklerini:<br>
Artık ihtiyaç duymadığınız hello önekleri bırakın. Bu örnekte, biz artık 20.0.0.0/24 öneki hello yerel ağ geçidi güncelleştiriyoruz şekilde bu önek (Merhaba önceki örnekten) dışında.

```powershell
$local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
-AddressPrefix @('10.0.0.0/24','30.0.0.0/24')
```

### <a name="withconnection"></a>ağ geçidi bağlantısı varolan toomodify yerel ağ geçidi IP adresi öneklerini-

Bir ağ geçidi bağlantısına sahip ve tooadd istediğiniz veya yerel ağ geçidinizinde başlangıç IP adresi öneklerini kaldırırsanız, aşağıdaki adımları sırayla toodo hello gerekir. Bunun sonucunda, VPN bağlantınızda kesinti oluşur. IP adres öneklerini değiştirirken toodelete hello VPN ağ geçidi gerekmez. Yalnızca tooremove hello bağlantı gerekir.


1. Merhaba bağlantısını kaldırın.

  ```powershell
  Remove-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName -ResourceGroupName MyRGName
  ```
2. Yerel ağ geçidinizin Hello adres öneklerini değiştirme.
   
  Merhaba LocalNetworkGateway Hello değişken ayarlayın.

  ```powershell
  $local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName
  ```
   
  Hello öneklerini değiştirin.
   
  ```powershell
  Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
  -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24')
  ```
3. Merhaba bağlantı oluşturun. Bu örnekte bir IPsec bağlantı türü yapılandırıyoruz. Bağlantınızı yeniden oluşturduğunuzda yapılandırmanızla ilgili belirtilen hello bağlantı türünü kullanın. Merhaba ek bağlantı türleri için bkz: [PowerShell cmdlet'ini](https://msdn.microsoft.com/library/mt603611.aspx) sayfası.
   
  Merhaba VirtualNetworkGateway Hello değişken ayarlayın.

  ```powershell
  $gateway1 = Get-AzureRmVirtualNetworkGateway -Name RMGateway  -ResourceGroupName MyRGName
  ```
   
  Merhaba bağlantı oluşturun. Bu örnek hello değişkeni 2. adımda ayarladığınız $local kullanır.

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName `
  -ResourceGroupName MyRGName -Location 'West US' `
  -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
  -ConnectionType IPsec `
  -RoutingWeight 10 -SharedKey 'abc123'
  ```