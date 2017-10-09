Bağlantınızı hello 'Get-AzureVNetConnection' cmdlet'ini kullanarak başarılı olduğunu doğrulayabilirsiniz.

1. Aşağıdaki cmdlet'i örneğine, hello değerleri toomatch yapılandırma kullanım hello kendi. hello hello sanal ağın adını, boşluk içeriyorsa tırnak içine olması gerekir.

  ```powershell
  Get-AzureVNetConnection "Group ClassicRG ClassicVNet"
  ```
2. Merhaba cmdlet tamamlandıktan sonra hello değerlerini görüntüleyin. Merhaba aşağıdaki örnek, giriş ve çıkış baytlarını görebilirsiniz ve 'Bağlı ' hello bağlantı durumu gösterir.

        ConnectivityState         : Connected
        EgressBytesTransferred    : 181664
        IngressBytesTransferred   : 182080
        LastConnectionEstablished : 1/7/2016 12:40:54 AM
        LastEventID               : 24401
        LastEventMessage          : hello connectivity state for hello local network site 'RMVNetLocal' changed from Connecting to
                                    Connected.
        LastEventTimeStamp        : 1/7/2016 12:40:54 AM
        LocalNetworkSiteName      : RMVNetLocal