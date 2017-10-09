<span data-ttu-id="987b4-101">Bu yapılandırmaya başlamadan önce tooyour Azure hesabı oturum açmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="987b4-101">Before beginning this configuration, you must log in tooyour Azure account.</span></span> <span data-ttu-id="987b4-102">Merhaba cmdlet hello Azure hesabınızda oturum açma kimlik bilgilerini ister.</span><span class="sxs-lookup"><span data-stu-id="987b4-102">hello cmdlet prompts you for hello login credentials for your Azure account.</span></span> <span data-ttu-id="987b4-103">Kullanılabilir tooAzure PowerShell şekilde oturum açtıktan sonra hesap ayarlarınızı indirir.</span><span class="sxs-lookup"><span data-stu-id="987b4-103">After logging in, it downloads your account settings so they are available tooAzure PowerShell.</span></span> <span data-ttu-id="987b4-104">Daha fazla bilgi için [Windows PowerShell’i Resource Manager ile kullanma](../articles/powershell-azure-resource-manager.md) konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="987b4-104">For more information, see [Using Windows PowerShell with Resource Manager](../articles/powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="987b4-105">toolog, yükseltilmiş ayrıcalıklarla PowerShell Konsolunuzu açın ve tooyour hesap bağlanın.</span><span class="sxs-lookup"><span data-stu-id="987b4-105">toolog in, open your PowerShell console with elevated privileges, and connect tooyour account.</span></span> <span data-ttu-id="987b4-106">Bağlandığınız örnek toohelp aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="987b4-106">Use hello following example toohelp you connect:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="987b4-107">Birden çok Azure aboneliğiniz varsa, hello hesabının hello abonelikleri kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="987b4-107">If you have multiple Azure subscriptions, check hello subscriptions for hello account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="987b4-108">Merhaba abonelik toouse istediğinizi belirtin.</span><span class="sxs-lookup"><span data-stu-id="987b4-108">Specify hello subscription that you want toouse.</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
 ```