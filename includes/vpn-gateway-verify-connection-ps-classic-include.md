<span data-ttu-id="84df1-101">Bağlantınızı hello 'Get-AzureVNetConnection' cmdlet'ini kullanarak başarılı olduğunu doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="84df1-101">You can verify that your connection succeeded by using hello 'Get-AzureVNetConnection' cmdlet.</span></span>

1. <span data-ttu-id="84df1-102">Aşağıdaki cmdlet'i örneğine, hello değerleri toomatch yapılandırma kullanım hello kendi.</span><span class="sxs-lookup"><span data-stu-id="84df1-102">Use hello following cmdlet example, configuring hello values toomatch your own.</span></span> <span data-ttu-id="84df1-103">hello hello sanal ağın adını, boşluk içeriyorsa tırnak içine olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="84df1-103">hello name of hello virtual network must be in quotes if it contains spaces.</span></span>

  ```powershell
  Get-AzureVNetConnection "Group ClassicRG ClassicVNet"
  ```
2. <span data-ttu-id="84df1-104">Merhaba cmdlet tamamlandıktan sonra hello değerlerini görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="84df1-104">After hello cmdlet has finished, view hello values.</span></span> <span data-ttu-id="84df1-105">Merhaba aşağıdaki örnek, giriş ve çıkış baytlarını görebilirsiniz ve 'Bağlı ' hello bağlantı durumu gösterir.</span><span class="sxs-lookup"><span data-stu-id="84df1-105">In hello example below, hello Connectivity State shows as 'Connected' and you can see ingress and egress bytes.</span></span>

        ConnectivityState         : Connected
        EgressBytesTransferred    : 181664
        IngressBytesTransferred   : 182080
        LastConnectionEstablished : 1/7/2016 12:40:54 AM
        LastEventID               : 24401
        LastEventMessage          : hello connectivity state for hello local network site 'RMVNetLocal' changed from Connecting to
                                    Connected.
        LastEventTimeStamp        : 1/7/2016 12:40:54 AM
        LocalNetworkSiteName      : RMVNetLocal