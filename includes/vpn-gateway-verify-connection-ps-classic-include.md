<span data-ttu-id="c71da-101">Bağlantınızı 'Get-AzureVNetConnection' cmdlet'ini kullanarak başarılı olduğunu doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c71da-101">You can verify that your connection succeeded by using the 'Get-AzureVNetConnection' cmdlet.</span></span>

1. <span data-ttu-id="c71da-102">Aşağıdaki cmdlet örneğini kullanın ve değerleri, kendi değerlerinizle eşleşecek şekilde yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="c71da-102">Use the following cmdlet example, configuring the values to match your own.</span></span> <span data-ttu-id="c71da-103">Sanal ağın adı boşluk içeriyorsa tırnak içine olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c71da-103">The name of the virtual network must be in quotes if it contains spaces.</span></span>

  ```powershell
  Get-AzureVNetConnection "Group ClassicRG ClassicVNet"
  ```
2. <span data-ttu-id="c71da-104">cmdlet tamamlandıktan sonra değerleri görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="c71da-104">After the cmdlet has finished, view the values.</span></span> <span data-ttu-id="c71da-105">Aşağıdaki örnekte, bağlantı durumu 'Bağlı ' gösterir ve giriş ve çıkış baytlarını görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c71da-105">In the example below, the Connectivity State shows as 'Connected' and you can see ingress and egress bytes.</span></span>

        ConnectivityState         : Connected
        EgressBytesTransferred    : 181664
        IngressBytesTransferred   : 182080
        LastConnectionEstablished : 1/7/2016 12:40:54 AM
        LastEventID               : 24401
        LastEventMessage          : The connectivity state for the local network site 'RMVNetLocal' changed from Connecting to
                                    Connected.
        LastEventTimeStamp        : 1/7/2016 12:40:54 AM
        LocalNetworkSiteName      : RMVNetLocal