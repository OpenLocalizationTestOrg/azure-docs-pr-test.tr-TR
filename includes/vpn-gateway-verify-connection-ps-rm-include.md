Bağlantınızı ile veya olmadan hello 'Get-AzureRmVirtualNetworkGatewayConnection' cmdlet'ini kullanarak başarılı olduğunu doğrulayabilirsiniz '-Debug'. 

1. Aşağıdaki cmdlet'i örneğine, hello değerleri toomatch yapılandırma kullanım hello kendi. İstenirse, sipariş toorun Seç 'A' 'All'. Merhaba örnekte, '-Name' hello bağlantı tootest istediğiniz toohello adını gösterir.

  ```powershell
  Get-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnection -ResourceGroupName MyRG
  ```
2. Merhaba cmdlet tamamlandıktan sonra hello değerlerini görüntüleyin. 'Bağlı' ve giriş ve çıkış baytlarını görebilirsiniz gibi hello aşağıdaki örnekte, hello bağlantı durumunu gösterir.
   
  ```
  "connectionStatus": "Connected",
  "ingressBytesTransferred": 33509044,
  "egressBytesTransferred": 4142431
  ```