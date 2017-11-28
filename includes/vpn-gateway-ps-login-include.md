<span data-ttu-id="50752-101">Bu yapılandırmaya başlamadan önce Azure hesabınızda oturum açmalısınız.</span><span class="sxs-lookup"><span data-stu-id="50752-101">Before beginning this configuration, you must log in to your Azure account.</span></span> <span data-ttu-id="50752-102">Bu cmdlet, Azure hesabınıza ilişkin oturum açma kimlik bilgilerinizi girmenizi ister.</span><span class="sxs-lookup"><span data-stu-id="50752-102">The cmdlet prompts you for the login credentials for your Azure account.</span></span> <span data-ttu-id="50752-103">Oturum açtıktan sonra, Azure PowerShell'de kullanabilmeniz için hesap ayarlarınızı indirir.</span><span class="sxs-lookup"><span data-stu-id="50752-103">After logging in, it downloads your account settings so they are available to Azure PowerShell.</span></span> <span data-ttu-id="50752-104">Daha fazla bilgi için [Windows PowerShell’i Resource Manager ile kullanma](../articles/powershell-azure-resource-manager.md) konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="50752-104">For more information, see [Using Windows PowerShell with Resource Manager](../articles/powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="50752-105">Oturum açmak için PowerShell konsolunuzu yükseltilmiş ayrıcalıklarla açın ve hesabınıza bağlanın.</span><span class="sxs-lookup"><span data-stu-id="50752-105">To log in, open your PowerShell console with elevated privileges, and connect to your account.</span></span> <span data-ttu-id="50752-106">Bağlanmanıza yardımcı olması için aşağıdaki örneği kullanın:</span><span class="sxs-lookup"><span data-stu-id="50752-106">Use the following example to help you connect:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="50752-107">Birden çok Azure aboneliğiniz varsa, hesabın aboneliklerini denetleyin.</span><span class="sxs-lookup"><span data-stu-id="50752-107">If you have multiple Azure subscriptions, check the subscriptions for the account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="50752-108">Kullanmak istediğiniz aboneliği belirtin.</span><span class="sxs-lookup"><span data-stu-id="50752-108">Specify the subscription that you want to use.</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
 ```