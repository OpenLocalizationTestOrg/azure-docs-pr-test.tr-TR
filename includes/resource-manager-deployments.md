## <a name="incremental-and-complete-deployments"></a><span data-ttu-id="35779-101">Artımlı ve tam dağıtımları</span><span class="sxs-lookup"><span data-stu-id="35779-101">Incremental and complete deployments</span></span>
<span data-ttu-id="35779-102">Kaynaklarınızın dağıtırken dağıtım Artımlı güncelleştirme ya da tam güncelleştirme olduğunu belirtin.</span><span class="sxs-lookup"><span data-stu-id="35779-102">When deploying your resources, you specify that the deployment is either an incremental update or a complete update.</span></span> <span data-ttu-id="35779-103">Bu iki mod arasındaki birincil fark, Resource Manager şablonunda olmayan mevcut kaynakları kaynak grubunda nasıl işlediğini şöyledir:</span><span class="sxs-lookup"><span data-stu-id="35779-103">The primary difference between these two modes is how Resource Manager handles existing resources in the resource group that are not in the template:</span></span>

* <span data-ttu-id="35779-104">Tam modunda Resource Manager **siler** kaynak grubunda var, ancak şablonda belirtilmeyen kaynakları.</span><span class="sxs-lookup"><span data-stu-id="35779-104">In complete mode, Resource Manager **deletes** resources that exist in the resource group but are not specified in the template.</span></span> 
* <span data-ttu-id="35779-105">Artımlı modunda Resource Manager **değişmeden bırakır** kaynak grubunda var, ancak şablonda belirtilmeyen kaynakları.</span><span class="sxs-lookup"><span data-stu-id="35779-105">In incremental mode, Resource Manager **leaves unchanged** resources that exist in the resource group but are not specified in the template.</span></span>

<span data-ttu-id="35779-106">Her iki mod için Resource Manager şablonunda belirtilen tüm kaynakları sağlamak üzere çalışır.</span><span class="sxs-lookup"><span data-stu-id="35779-106">For both modes, Resource Manager attempts to provision all resources specified in the template.</span></span> <span data-ttu-id="35779-107">Kaynak kaynak grubunda zaten mevcut ve ayarlarını aynıdır, işlemi hiçbir değişikliğe neden olur.</span><span class="sxs-lookup"><span data-stu-id="35779-107">If the resource already exists in the resource group and its settings are unchanged, the operation results in no change.</span></span> <span data-ttu-id="35779-108">Kaynak bir kaynağın ayarlarını değiştirirseniz, bu yeni ayarlarla sağlanır.</span><span class="sxs-lookup"><span data-stu-id="35779-108">If you change the settings for a resource, the resource is provisioned with those new settings.</span></span> <span data-ttu-id="35779-109">Konum veya varolan bir kaynak türü güncelleştirme denemesi dağıtımı bir hatayla başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="35779-109">If you attempt to update the location or type of an existing resource, the deployment fails with an error.</span></span> <span data-ttu-id="35779-110">Bunun yerine, yeni bir kaynak konumu ile dağıtabilir veya gerektiğini bildiren yazın.</span><span class="sxs-lookup"><span data-stu-id="35779-110">Instead, deploy a new resource with the location or type that you need.</span></span>

<span data-ttu-id="35779-111">Varsayılan olarak, artımlı modu Kaynak Yöneticisi'ni kullanır.</span><span class="sxs-lookup"><span data-stu-id="35779-111">By default, Resource Manager uses the incremental mode.</span></span>

<span data-ttu-id="35779-112">Artımlı ve tam modları arasındaki farkı anlamak için aşağıdaki senaryoyu göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="35779-112">To illustrate the difference between incremental and complete modes, consider the following scenario.</span></span>

<span data-ttu-id="35779-113">**Varolan bir kaynak grubu** içerir:</span><span class="sxs-lookup"><span data-stu-id="35779-113">**Existing Resource Group** contains:</span></span>

* <span data-ttu-id="35779-114">Kaynak</span><span class="sxs-lookup"><span data-stu-id="35779-114">Resource A</span></span>
* <span data-ttu-id="35779-115">Kaynak B</span><span class="sxs-lookup"><span data-stu-id="35779-115">Resource B</span></span>
* <span data-ttu-id="35779-116">Kaynak C</span><span class="sxs-lookup"><span data-stu-id="35779-116">Resource C</span></span>

<span data-ttu-id="35779-117">**Şablon** tanımlar:</span><span class="sxs-lookup"><span data-stu-id="35779-117">**Template** defines:</span></span>

* <span data-ttu-id="35779-118">Kaynak</span><span class="sxs-lookup"><span data-stu-id="35779-118">Resource A</span></span>
* <span data-ttu-id="35779-119">Kaynak B</span><span class="sxs-lookup"><span data-stu-id="35779-119">Resource B</span></span>
* <span data-ttu-id="35779-120">Kaynak D</span><span class="sxs-lookup"><span data-stu-id="35779-120">Resource D</span></span>

<span data-ttu-id="35779-121">İçinde dağıtıldığında **artımlı** modu, kaynak grubu içerir:</span><span class="sxs-lookup"><span data-stu-id="35779-121">When deployed in **incremental** mode, the resource group contains:</span></span>

* <span data-ttu-id="35779-122">Kaynak</span><span class="sxs-lookup"><span data-stu-id="35779-122">Resource A</span></span>
* <span data-ttu-id="35779-123">Kaynak B</span><span class="sxs-lookup"><span data-stu-id="35779-123">Resource B</span></span>
* <span data-ttu-id="35779-124">Kaynak C</span><span class="sxs-lookup"><span data-stu-id="35779-124">Resource C</span></span>
* <span data-ttu-id="35779-125">Kaynak D</span><span class="sxs-lookup"><span data-stu-id="35779-125">Resource D</span></span>

<span data-ttu-id="35779-126">İçinde dağıtıldığında **tam** modu, kaynak C silinir.</span><span class="sxs-lookup"><span data-stu-id="35779-126">When deployed in **complete** mode, Resource C is deleted.</span></span> <span data-ttu-id="35779-127">Kaynak grubu içerir:</span><span class="sxs-lookup"><span data-stu-id="35779-127">The resource group contains:</span></span>

* <span data-ttu-id="35779-128">Kaynak</span><span class="sxs-lookup"><span data-stu-id="35779-128">Resource A</span></span>
* <span data-ttu-id="35779-129">Kaynak B</span><span class="sxs-lookup"><span data-stu-id="35779-129">Resource B</span></span>
* <span data-ttu-id="35779-130">Kaynak D</span><span class="sxs-lookup"><span data-stu-id="35779-130">Resource D</span></span>
