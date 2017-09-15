## <a name="set-up-azure-cli-for-azure-dns"></a><span data-ttu-id="62b8e-101">Azure DNS için Azure CLI'yi ayarlama</span><span class="sxs-lookup"><span data-stu-id="62b8e-101">Set up Azure CLI for Azure DNS</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="62b8e-102">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="62b8e-102">Before you begin</span></span>

<span data-ttu-id="62b8e-103">Yapılandırmanıza başlamadan önce aşağıdaki öğelerin bulunduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="62b8e-103">Verify that you have the following items before beginning your configuration.</span></span>

* <span data-ttu-id="62b8e-104">Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="62b8e-104">An Azure subscription.</span></span> <span data-ttu-id="62b8e-105">Henüz Azure aboneliğiniz yoksa [MSDN abonelik avantajlarınızı](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) etkinleştirebilir veya [ücretsiz bir hesap](https://azure.microsoft.com/pricing/free-trial/) için kaydolabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="62b8e-105">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="62b8e-106">Windows, Linux veya Mac için Azure CLI'nin son sürümünü yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="62b8e-106">Install the latest version of the Azure CLI, available for Windows, Linux, or MAC.</span></span> <span data-ttu-id="62b8e-107">Daha fazla bilgi için bkz. [Azure CLI'yı yükleme](../articles/cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="62b8e-107">More information is available at [Install the Azure CLI](../articles/cli-install-nodejs.md).</span></span>

### <a name="sign-in-to-your-azure-account"></a><span data-ttu-id="62b8e-108">Azure hesabınızda oturum açma</span><span class="sxs-lookup"><span data-stu-id="62b8e-108">Sign in to your Azure account</span></span>

<span data-ttu-id="62b8e-109">Bir konsol penceresi açın ve kimlik bilgilerinizi girerek kimliğinizi doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="62b8e-109">Open a console window and authenticate with your credentials.</span></span> <span data-ttu-id="62b8e-110">Daha fazla bilgi için bkz. [Azure CLI üzerinden Azure’da oturum açma](../articles/xplat-cli-connect.md)</span><span class="sxs-lookup"><span data-stu-id="62b8e-110">For more information, see [Log in to Azure from the Azure CLI](../articles/xplat-cli-connect.md)</span></span>

```azurecli
azure login
```

### <a name="switch-cli-mode"></a><span data-ttu-id="62b8e-111">CLI moduna geçme</span><span class="sxs-lookup"><span data-stu-id="62b8e-111">Switch CLI mode</span></span>

<span data-ttu-id="62b8e-112">Azure DNS, Azure Resource Manager'ı kullanır.</span><span class="sxs-lookup"><span data-stu-id="62b8e-112">Azure DNS uses Azure Resource Manager.</span></span> <span data-ttu-id="62b8e-113">Azure Resource Manager komutlarını kullanmak için CLI moduna geçtiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="62b8e-113">Make sure you switch CLI mode to use Azure Resource Manager commands.</span></span>

```azurecli
azure config mode arm
```

### <a name="select-the-subscription"></a><span data-ttu-id="62b8e-114">Aboneliği seçme</span><span class="sxs-lookup"><span data-stu-id="62b8e-114">Select the subscription</span></span>

<span data-ttu-id="62b8e-115">Hesapla ilişkili abonelikleri kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="62b8e-115">Check the subscriptions for the account.</span></span>

```azurecli
azure account list
```

<span data-ttu-id="62b8e-116">Hangi Azure aboneliğinizin kullanılacağını seçin.</span><span class="sxs-lookup"><span data-stu-id="62b8e-116">Choose which of your Azure subscriptions to use.</span></span>

```azurecli
azure account set "subscription name"
```

### <a name="create-a-resource-group"></a><span data-ttu-id="62b8e-117">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="62b8e-117">Create a resource group</span></span>

<span data-ttu-id="62b8e-118">Azure Resource Manager, tüm kaynak gruplarının bir konum belirtmesini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="62b8e-118">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="62b8e-119">Bu, kaynak grubunda kaynaklar için varsayılan konum olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="62b8e-119">This is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="62b8e-120">Ancak tüm DNS kaynakları bölgesel değil de global olduğundan, kaynak grubu konumu seçiminin Azure DNS üzerinde hiçbir etkisi yoktur.</span><span class="sxs-lookup"><span data-stu-id="62b8e-120">However, because all DNS resources are global, not regional, the choice of resource group location has no impact on Azure DNS.</span></span>

<span data-ttu-id="62b8e-121">Var olan bir kaynak grubunu kullanıyorsanız bu adımı atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="62b8e-121">You can skip this step if you are using an existing resource group.</span></span>

```azurecli
azure group create -n myresourcegroup --location "West US"
```

### <a name="register-resource-provider"></a><span data-ttu-id="62b8e-122">Kaynak sağlayıcısını kaydetme</span><span class="sxs-lookup"><span data-stu-id="62b8e-122">Register resource provider</span></span>

<span data-ttu-id="62b8e-123">Azure DNS hizmeti, Microsoft.Network kaynak sağlayıcısı tarafından yönetilir.</span><span class="sxs-lookup"><span data-stu-id="62b8e-123">The Azure DNS service is managed by the Microsoft.Network resource provider.</span></span> <span data-ttu-id="62b8e-124">Azure DNS'yi kullanabilmeniz için, Azure aboneliğinizin bu kaynak sağlayıcısını kullanmak üzere kayıtlı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="62b8e-124">Your Azure subscription must be registered to use this resource provider before you can use Azure DNS.</span></span> <span data-ttu-id="62b8e-125">Bu, her bir abonelik için tek seferlik bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="62b8e-125">This is a one-time operation for each subscription.</span></span>

```azurecli
azure provider register --namespace Microsoft.Network
```

