## <a name="set-up-azure-powershell-for-azure-dns"></a><span data-ttu-id="43bed-101">Azure DNS için Azure PowerShell ayarlayın</span><span class="sxs-lookup"><span data-stu-id="43bed-101">Set up Azure PowerShell for Azure DNS</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="43bed-102">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="43bed-102">Before you begin</span></span>

<span data-ttu-id="43bed-103">Yapılandırmanıza başlamadan önce aşağıdaki öğelerindeki hello sahip olduğunuzu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="43bed-103">Verify that you have hello following items before beginning your configuration.</span></span>

* <span data-ttu-id="43bed-104">Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="43bed-104">An Azure subscription.</span></span> <span data-ttu-id="43bed-105">Henüz Azure aboneliğiniz yoksa [MSDN abonelik avantajlarınızı](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) etkinleştirebilir veya [ücretsiz bir hesap](https://azure.microsoft.com/pricing/free-trial/) için kaydolabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="43bed-105">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="43bed-106">Tooinstall hello en son sürümünü hello Azure Resource Manager PowerShell cmdlet'lerini gerekir.</span><span class="sxs-lookup"><span data-stu-id="43bed-106">You need tooinstall hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="43bed-107">Daha fazla bilgi için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="43bed-107">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>

### <a name="sign-in-tooyour-azure-account"></a><span data-ttu-id="43bed-108">Azure hesabı tooyour içinde oturum</span><span class="sxs-lookup"><span data-stu-id="43bed-108">Sign in tooyour Azure account</span></span>

<span data-ttu-id="43bed-109">PowerShell Konsolunuzu açın ve tooyour hesap bağlanın.</span><span class="sxs-lookup"><span data-stu-id="43bed-109">Open your PowerShell console and connect tooyour account.</span></span> <span data-ttu-id="43bed-110">Daha fazla bilgi için bkz: [PowerShell kullanarak Resource Manager ile](../articles/azure-resource-manager/powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="43bed-110">For more information, see [Using PowerShell with Resource Manager](../articles/azure-resource-manager/powershell-azure-resource-manager.md).</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="select-hello-subscription"></a><span data-ttu-id="43bed-111">Merhaba aboneliği seçin</span><span class="sxs-lookup"><span data-stu-id="43bed-111">Select hello subscription</span></span>
 
<span data-ttu-id="43bed-112">Merhaba hesabının Hello abonelikleri kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="43bed-112">Check hello subscriptions for hello account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="43bed-113">Azure abonelikleri toouse hangisinin seçin.</span><span class="sxs-lookup"><span data-stu-id="43bed-113">Choose which of your Azure subscriptions toouse.</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionName "your_subscription_name"
```

### <a name="create-a-resource-group"></a><span data-ttu-id="43bed-114">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="43bed-114">Create a resource group</span></span>

<span data-ttu-id="43bed-115">Azure Resource Manager, tüm kaynak gruplarının bir konum belirtmesini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="43bed-115">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="43bed-116">Bu konum, kaynak grubundaki kaynaklar için hello varsayılan konum olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="43bed-116">This location is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="43bed-117">Ancak, tüm DNS kaynakları global olduğundan, bölgesel değil, kaynak grubu konumu hello seçimine Azure DNS üzerinde hiçbir etkisi olmaz.</span><span class="sxs-lookup"><span data-stu-id="43bed-117">However, because all DNS resources are global, not regional, hello choice of resource group location has no impact on Azure DNS.</span></span>

<span data-ttu-id="43bed-118">Var olan bir kaynak grubunu kullanıyorsanız bu adımı atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="43bed-118">You can skip this step if you are using an existing resource group.</span></span>

```powershell
New-AzureRmResourceGroup -Name MyAzureResourceGroup -location "West US"
```

### <a name="register-resource-provider"></a><span data-ttu-id="43bed-119">Kaynak sağlayıcısını kaydetme</span><span class="sxs-lookup"><span data-stu-id="43bed-119">Register resource provider</span></span>

<span data-ttu-id="43bed-120">Hello Azure DNS hizmeti hello Microsoft.Network kaynak sağlayıcısı tarafından yönetilir.</span><span class="sxs-lookup"><span data-stu-id="43bed-120">hello Azure DNS service is managed by hello Microsoft.Network resource provider.</span></span> <span data-ttu-id="43bed-121">Azure aboneliğinizde Azure DNS'yi kullanmadan önce bu kaynak sağlayıcısı kayıtlı toouse olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="43bed-121">Your Azure subscription must be registered toouse this resource provider before you can use Azure DNS.</span></span> <span data-ttu-id="43bed-122">Bu, her bir abonelik için tek seferlik bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="43bed-122">This is a one-time operation for each subscription.</span></span>

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Network
```