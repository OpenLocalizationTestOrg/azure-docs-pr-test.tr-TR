Bu yapılandırmaya başlamadan önce tooyour Azure hesabı oturum açmanız gerekir. Merhaba cmdlet hello Azure hesabınızda oturum açma kimlik bilgilerini ister. Kullanılabilir tooAzure PowerShell şekilde oturum açtıktan sonra hesap ayarlarınızı indirir. Daha fazla bilgi için [Windows PowerShell’i Resource Manager ile kullanma](../articles/powershell-azure-resource-manager.md) konusuna bakın.

toolog, yükseltilmiş ayrıcalıklarla PowerShell Konsolunuzu açın ve tooyour hesap bağlanın. Bağlandığınız örnek toohelp aşağıdaki hello kullan:

```powershell
Login-AzureRmAccount
```

Birden çok Azure aboneliğiniz varsa, hello hesabının hello abonelikleri kontrol edin.

```powershell
Get-AzureRmSubscription
```

Merhaba abonelik toouse istediğinizi belirtin.

```powershell
Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
 ```