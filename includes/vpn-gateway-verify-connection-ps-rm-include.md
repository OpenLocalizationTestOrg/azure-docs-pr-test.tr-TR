<span data-ttu-id="ff107-101">Bağlantınızın başarılı olduğunu, 'Get-AzureRmVirtualNetworkGatewayConnection' cmdlet’ini '-Debug' ile veya '-Debug' olmadan kullanarak doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ff107-101">You can verify that your connection succeeded by using the 'Get-AzureRmVirtualNetworkGatewayConnection' cmdlet, with or without '-Debug'.</span></span> 

1. <span data-ttu-id="ff107-102">Aşağıdaki cmdlet örneğini kullanın ve değerleri, kendi değerlerinizle eşleşecek şekilde yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="ff107-102">Use the following cmdlet example, configuring the values to match your own.</span></span> <span data-ttu-id="ff107-103">İstendiğinde "Tümünü" çalıştırmak için "A" seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="ff107-103">If prompted, select 'A' in order to run 'All'.</span></span> <span data-ttu-id="ff107-104">Örnekte bulunan "-Name", test etmek istediğiniz bağlantının adıdır.</span><span class="sxs-lookup"><span data-stu-id="ff107-104">In the example, '-Name' refers to the name of the connection that you want to test.</span></span>

  ```powershell
  Get-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnection -ResourceGroupName MyRG
  ```
2. <span data-ttu-id="ff107-105">cmdlet tamamlandıktan sonra değerleri görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="ff107-105">After the cmdlet has finished, view the values.</span></span> <span data-ttu-id="ff107-106">Aşağıdaki örnekte, bağlantı durumu "Bağlandı" olarak gösterilir; ayrıca giriş ve çıkış baytlarını görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ff107-106">In the example below, the connection status shows as 'Connected' and you can see ingress and egress bytes.</span></span>
   
  ```
  "connectionStatus": "Connected",
  "ingressBytesTransferred": 33509044,
  "egressBytesTransferred": 4142431
  ```