## <a name="incremental-and-complete-deployments"></a><span data-ttu-id="fe151-101">Artımlı ve tam dağıtımları</span><span class="sxs-lookup"><span data-stu-id="fe151-101">Incremental and complete deployments</span></span>
<span data-ttu-id="fe151-102">Kaynaklarınızın dağıtırken hello dağıtım Artımlı güncelleştirme ya da tam güncelleştirme olduğunu belirtin.</span><span class="sxs-lookup"><span data-stu-id="fe151-102">When deploying your resources, you specify that hello deployment is either an incremental update or a complete update.</span></span> <span data-ttu-id="fe151-103">Bu iki mod arasındaki birincil fark Hello Resource Manager hello şablonunda olmayan mevcut kaynakları hello kaynak grubunda nasıl işlediğini şöyledir:</span><span class="sxs-lookup"><span data-stu-id="fe151-103">hello primary difference between these two modes is how Resource Manager handles existing resources in hello resource group that are not in hello template:</span></span>

* <span data-ttu-id="fe151-104">Tam modunda Resource Manager **siler** hello kaynak grubunda var, ancak hello şablonda belirtilmeyen kaynakları.</span><span class="sxs-lookup"><span data-stu-id="fe151-104">In complete mode, Resource Manager **deletes** resources that exist in hello resource group but are not specified in hello template.</span></span> 
* <span data-ttu-id="fe151-105">Artımlı modunda Resource Manager **değişmeden bırakır** hello kaynak grubunda var, ancak hello şablonda belirtilmeyen kaynakları.</span><span class="sxs-lookup"><span data-stu-id="fe151-105">In incremental mode, Resource Manager **leaves unchanged** resources that exist in hello resource group but are not specified in hello template.</span></span>

<span data-ttu-id="fe151-106">Her iki mod için Resource Manager tooprovision hello şablonunda belirtilen tüm kaynakların çalışır.</span><span class="sxs-lookup"><span data-stu-id="fe151-106">For both modes, Resource Manager attempts tooprovision all resources specified in hello template.</span></span> <span data-ttu-id="fe151-107">Hello kaynak hello kaynak grubunda zaten varsa ve ayarlarına aynıdır, hello işlemi hiçbir değişikliğe neden olur.</span><span class="sxs-lookup"><span data-stu-id="fe151-107">If hello resource already exists in hello resource group and its settings are unchanged, hello operation results in no change.</span></span> <span data-ttu-id="fe151-108">Bir kaynağın hello ayarlarını değiştirirseniz, bu yeni ayarlarla hello kaynak sağlanır.</span><span class="sxs-lookup"><span data-stu-id="fe151-108">If you change hello settings for a resource, hello resource is provisioned with those new settings.</span></span> <span data-ttu-id="fe151-109">Merhaba dağıtımı tooupdate hello konumu veya varolan bir kaynak türü çalışırsanız, bir hata ile başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="fe151-109">If you attempt tooupdate hello location or type of an existing resource, hello deployment fails with an error.</span></span> <span data-ttu-id="fe151-110">Bunun yerine, hello konumuna sahip yeni bir kaynak dağıtabilir veya gerektiğini bildiren yazın.</span><span class="sxs-lookup"><span data-stu-id="fe151-110">Instead, deploy a new resource with hello location or type that you need.</span></span>

<span data-ttu-id="fe151-111">Varsayılan olarak, Resource Manager hello artımlı modunu kullanır.</span><span class="sxs-lookup"><span data-stu-id="fe151-111">By default, Resource Manager uses hello incremental mode.</span></span>

<span data-ttu-id="fe151-112">Artımlı ve tam modlar arasında tooillustrate hello fark senaryo aşağıdaki hello göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="fe151-112">tooillustrate hello difference between incremental and complete modes, consider hello following scenario.</span></span>

<span data-ttu-id="fe151-113">**Varolan bir kaynak grubu** içerir:</span><span class="sxs-lookup"><span data-stu-id="fe151-113">**Existing Resource Group** contains:</span></span>

* <span data-ttu-id="fe151-114">Kaynak</span><span class="sxs-lookup"><span data-stu-id="fe151-114">Resource A</span></span>
* <span data-ttu-id="fe151-115">Kaynak B</span><span class="sxs-lookup"><span data-stu-id="fe151-115">Resource B</span></span>
* <span data-ttu-id="fe151-116">Kaynak C</span><span class="sxs-lookup"><span data-stu-id="fe151-116">Resource C</span></span>

<span data-ttu-id="fe151-117">**Şablon** tanımlar:</span><span class="sxs-lookup"><span data-stu-id="fe151-117">**Template** defines:</span></span>

* <span data-ttu-id="fe151-118">Kaynak</span><span class="sxs-lookup"><span data-stu-id="fe151-118">Resource A</span></span>
* <span data-ttu-id="fe151-119">Kaynak B</span><span class="sxs-lookup"><span data-stu-id="fe151-119">Resource B</span></span>
* <span data-ttu-id="fe151-120">Kaynak D</span><span class="sxs-lookup"><span data-stu-id="fe151-120">Resource D</span></span>

<span data-ttu-id="fe151-121">İçinde dağıtıldığında **artımlı** modu, hello kaynak grubu içerir:</span><span class="sxs-lookup"><span data-stu-id="fe151-121">When deployed in **incremental** mode, hello resource group contains:</span></span>

* <span data-ttu-id="fe151-122">Kaynak</span><span class="sxs-lookup"><span data-stu-id="fe151-122">Resource A</span></span>
* <span data-ttu-id="fe151-123">Kaynak B</span><span class="sxs-lookup"><span data-stu-id="fe151-123">Resource B</span></span>
* <span data-ttu-id="fe151-124">Kaynak C</span><span class="sxs-lookup"><span data-stu-id="fe151-124">Resource C</span></span>
* <span data-ttu-id="fe151-125">Kaynak D</span><span class="sxs-lookup"><span data-stu-id="fe151-125">Resource D</span></span>

<span data-ttu-id="fe151-126">İçinde dağıtıldığında **tam** modu, kaynak C silinir.</span><span class="sxs-lookup"><span data-stu-id="fe151-126">When deployed in **complete** mode, Resource C is deleted.</span></span> <span data-ttu-id="fe151-127">Merhaba kaynak grubu içerir:</span><span class="sxs-lookup"><span data-stu-id="fe151-127">hello resource group contains:</span></span>

* <span data-ttu-id="fe151-128">Kaynak</span><span class="sxs-lookup"><span data-stu-id="fe151-128">Resource A</span></span>
* <span data-ttu-id="fe151-129">Kaynak B</span><span class="sxs-lookup"><span data-stu-id="fe151-129">Resource B</span></span>
* <span data-ttu-id="fe151-130">Kaynak D</span><span class="sxs-lookup"><span data-stu-id="fe151-130">Resource D</span></span>
