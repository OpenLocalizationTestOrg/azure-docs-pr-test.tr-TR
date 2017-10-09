<span data-ttu-id="6fc92-101">Bağlantınızı ile veya olmadan hello 'Get-AzureRmVirtualNetworkGatewayConnection' cmdlet'ini kullanarak başarılı olduğunu doğrulayabilirsiniz '-Debug'.</span><span class="sxs-lookup"><span data-stu-id="6fc92-101">You can verify that your connection succeeded by using hello 'Get-AzureRmVirtualNetworkGatewayConnection' cmdlet, with or without '-Debug'.</span></span> 

1. <span data-ttu-id="6fc92-102">Aşağıdaki cmdlet'i örneğine, hello değerleri toomatch yapılandırma kullanım hello kendi.</span><span class="sxs-lookup"><span data-stu-id="6fc92-102">Use hello following cmdlet example, configuring hello values toomatch your own.</span></span> <span data-ttu-id="6fc92-103">İstenirse, sipariş toorun Seç 'A' 'All'.</span><span class="sxs-lookup"><span data-stu-id="6fc92-103">If prompted, select 'A' in order toorun 'All'.</span></span> <span data-ttu-id="6fc92-104">Merhaba örnekte, '-Name' hello bağlantı tootest istediğiniz toohello adını gösterir.</span><span class="sxs-lookup"><span data-stu-id="6fc92-104">In hello example, '-Name' refers toohello name of hello connection that you want tootest.</span></span>

  ```powershell
  Get-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnection -ResourceGroupName MyRG
  ```
2. <span data-ttu-id="6fc92-105">Merhaba cmdlet tamamlandıktan sonra hello değerlerini görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="6fc92-105">After hello cmdlet has finished, view hello values.</span></span> <span data-ttu-id="6fc92-106">'Bağlı' ve giriş ve çıkış baytlarını görebilirsiniz gibi hello aşağıdaki örnekte, hello bağlantı durumunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="6fc92-106">In hello example below, hello connection status shows as 'Connected' and you can see ingress and egress bytes.</span></span>
   
  ```
  "connectionStatus": "Connected",
  "ingressBytesTransferred": 33509044,
  "egressBytesTransferred": 4142431
  ```