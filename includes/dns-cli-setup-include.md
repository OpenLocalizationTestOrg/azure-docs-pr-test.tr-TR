## <a name="set-up-azure-cli-for-azure-dns"></a><span data-ttu-id="d0933-101">Azure DNS için Azure CLI'yi ayarlama</span><span class="sxs-lookup"><span data-stu-id="d0933-101">Set up Azure CLI for Azure DNS</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="d0933-102">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="d0933-102">Before you begin</span></span>

<span data-ttu-id="d0933-103">Yapılandırmanıza başlamadan önce aşağıdaki öğelerindeki hello sahip olduğunuzu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="d0933-103">Verify that you have hello following items before beginning your configuration.</span></span>

* <span data-ttu-id="d0933-104">Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="d0933-104">An Azure subscription.</span></span> <span data-ttu-id="d0933-105">Henüz Azure aboneliğiniz yoksa [MSDN abonelik avantajlarınızı](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) etkinleştirebilir veya [ücretsiz bir hesap](https://azure.microsoft.com/pricing/free-trial/) için kaydolabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0933-105">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="d0933-106">Merhaba hello Azure CLI, Windows, Linux veya Mac için kullanılabilir en son sürümünü yükleyin</span><span class="sxs-lookup"><span data-stu-id="d0933-106">Install hello latest version of hello Azure CLI, available for Windows, Linux, or MAC.</span></span> <span data-ttu-id="d0933-107">Daha fazla bilgi için bkz. [yükleme hello Azure CLI](../articles/cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="d0933-107">More information is available at [Install hello Azure CLI](../articles/cli-install-nodejs.md).</span></span>

### <a name="sign-in-tooyour-azure-account"></a><span data-ttu-id="d0933-108">Azure hesabı tooyour içinde oturum</span><span class="sxs-lookup"><span data-stu-id="d0933-108">Sign in tooyour Azure account</span></span>

<span data-ttu-id="d0933-109">Bir konsol penceresi açın ve kimlik bilgilerinizi girerek kimliğinizi doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="d0933-109">Open a console window and authenticate with your credentials.</span></span> <span data-ttu-id="d0933-110">Daha fazla bilgi için bkz: [tooAzure hello Azure CLI gelen oturum](../articles/xplat-cli-connect.md)</span><span class="sxs-lookup"><span data-stu-id="d0933-110">For more information, see [Log in tooAzure from hello Azure CLI](../articles/xplat-cli-connect.md)</span></span>

```azurecli
azure login
```

### <a name="switch-cli-mode"></a><span data-ttu-id="d0933-111">CLI moduna geçme</span><span class="sxs-lookup"><span data-stu-id="d0933-111">Switch CLI mode</span></span>

<span data-ttu-id="d0933-112">Azure DNS, Azure Resource Manager'ı kullanır.</span><span class="sxs-lookup"><span data-stu-id="d0933-112">Azure DNS uses Azure Resource Manager.</span></span> <span data-ttu-id="d0933-113">CLI moduna toouse Azure Resource Manager komutları geçtiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="d0933-113">Make sure you switch CLI mode toouse Azure Resource Manager commands.</span></span>

```azurecli
azure config mode arm
```

### <a name="select-hello-subscription"></a><span data-ttu-id="d0933-114">Merhaba aboneliği seçin</span><span class="sxs-lookup"><span data-stu-id="d0933-114">Select hello subscription</span></span>

<span data-ttu-id="d0933-115">Merhaba hesabının Hello abonelikleri kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="d0933-115">Check hello subscriptions for hello account.</span></span>

```azurecli
azure account list
```

<span data-ttu-id="d0933-116">Azure abonelikleri toouse hangisinin seçin.</span><span class="sxs-lookup"><span data-stu-id="d0933-116">Choose which of your Azure subscriptions toouse.</span></span>

```azurecli
azure account set "subscription name"
```

### <a name="create-a-resource-group"></a><span data-ttu-id="d0933-117">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="d0933-117">Create a resource group</span></span>

<span data-ttu-id="d0933-118">Azure Resource Manager, tüm kaynak gruplarının bir konum belirtmesini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="d0933-118">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="d0933-119">Bu kaynak grubundaki kaynaklar için hello varsayılan konum olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d0933-119">This is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="d0933-120">Ancak, tüm DNS kaynakları global olduğundan, bölgesel değil, kaynak grubu konumu hello seçimine Azure DNS üzerinde hiçbir etkisi olmaz.</span><span class="sxs-lookup"><span data-stu-id="d0933-120">However, because all DNS resources are global, not regional, hello choice of resource group location has no impact on Azure DNS.</span></span>

<span data-ttu-id="d0933-121">Var olan bir kaynak grubunu kullanıyorsanız bu adımı atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0933-121">You can skip this step if you are using an existing resource group.</span></span>

```azurecli
azure group create -n myresourcegroup --location "West US"
```

### <a name="register-resource-provider"></a><span data-ttu-id="d0933-122">Kaynak sağlayıcısını kaydetme</span><span class="sxs-lookup"><span data-stu-id="d0933-122">Register resource provider</span></span>

<span data-ttu-id="d0933-123">Hello Azure DNS hizmeti hello Microsoft.Network kaynak sağlayıcısı tarafından yönetilir.</span><span class="sxs-lookup"><span data-stu-id="d0933-123">hello Azure DNS service is managed by hello Microsoft.Network resource provider.</span></span> <span data-ttu-id="d0933-124">Azure aboneliğinizde Azure DNS'yi kullanmadan önce bu kaynak sağlayıcısı kayıtlı toouse olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d0933-124">Your Azure subscription must be registered toouse this resource provider before you can use Azure DNS.</span></span> <span data-ttu-id="d0933-125">Bu, her bir abonelik için tek seferlik bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="d0933-125">This is a one-time operation for each subscription.</span></span>

```azurecli
azure provider register --namespace Microsoft.Network
```

