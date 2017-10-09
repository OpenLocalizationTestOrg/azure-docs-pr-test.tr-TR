<span data-ttu-id="ef72e-101">Azure Resource Manager ile tanımladığınız parametreler için değerler hello şablon dağıtıldığında toospecify istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="ef72e-101">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="ef72e-102">Merhaba şablonu tüm hello parametre değerlerini içeren parametreleri adlı bir bölüm içerir.</span><span class="sxs-lookup"><span data-stu-id="ef72e-102">hello template includes a section called Parameters that contains all of hello parameter values.</span></span>
<span data-ttu-id="ef72e-103">Dağıttığınız hello projesini temel alan veya dağıttığınız hello ortamı dayanarak değişir bu değerleri için bir parametre tanımlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ef72e-103">You should define a parameter for those values that will vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="ef72e-104">Her zaman kalacak değerleri aynı hello için parametreleri tanımlamayın.</span><span class="sxs-lookup"><span data-stu-id="ef72e-104">Do not define parameters for values that will always stay hello same.</span></span> <span data-ttu-id="ef72e-105">Her parametre değeri dağıtılan hello şablonu toodefine hello kaynaklarında kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ef72e-105">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span> 

<span data-ttu-id="ef72e-106">Parametreleri tanımlarken hello kullanın **allowedValues** kullanıcı değerleri alan toospecify dağıtımı sırasında sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="ef72e-106">When defining parameters, use hello **allowedValues** field toospecify which values a user can provide during deployment.</span></span> <span data-ttu-id="ef72e-107">Kullanım hello **defaultValue** alan tooassign dağıtımı sırasında herhangi bir değer sağlanmazsa bir değer toohello parametresi.</span><span class="sxs-lookup"><span data-stu-id="ef72e-107">Use hello **defaultValue** field tooassign a value toohello parameter, if no value is provided during deployment.</span></span>

<span data-ttu-id="ef72e-108">Biz hello şablonundaki her bir parametreyi anlatmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ef72e-108">We will describe each parameter in hello template.</span></span>

### <a name="sitename"></a><span data-ttu-id="ef72e-109">SiteName</span><span class="sxs-lookup"><span data-stu-id="ef72e-109">siteName</span></span>
<span data-ttu-id="ef72e-110">Merhaba web uygulamasının toocreate istediğiniz Hello adı.</span><span class="sxs-lookup"><span data-stu-id="ef72e-110">hello name of hello web app that you wish toocreate.</span></span>

    "siteName":{
      "type":"string"
    }

### <a name="hostingplanname"></a><span data-ttu-id="ef72e-111">hostingPlanName</span><span class="sxs-lookup"><span data-stu-id="ef72e-111">hostingPlanName</span></span>
<span data-ttu-id="ef72e-112">Merhaba hello uygulama hizmeti adını hello web uygulamasını barındırmak için toouse planlayın.</span><span class="sxs-lookup"><span data-stu-id="ef72e-112">hello name of hello App Service plan toouse for hosting hello web app.</span></span>

    "hostingPlanName":{
      "type":"string"
    }

### <a name="sku"></a><span data-ttu-id="ef72e-113">SKU</span><span class="sxs-lookup"><span data-stu-id="ef72e-113">sku</span></span>
<span data-ttu-id="ef72e-114">Fiyatlandırma katmanı hello barındırma planı için hello.</span><span class="sxs-lookup"><span data-stu-id="ef72e-114">hello pricing tier for hello hosting plan.</span></span>

    "sku": {
      "type": "string",
      "allowedValues": [
        "F1",
        "D1",
        "B1",
        "B2",
        "B3",
        "S1",
        "S2",
        "S3",
        "P1",
        "P2",
        "P3",
        "P4"
      ],
      "defaultValue": "S1",
      "metadata": {
        "description": "hello pricing tier for hello hosting plan."
      }
    }

<span data-ttu-id="ef72e-115">Hello şablonu, bu parametre için izin verilen hello değerleri tanımlar ve herhangi bir değer belirtilmişse, varsayılan değer (S1) atar.</span><span class="sxs-lookup"><span data-stu-id="ef72e-115">hello template defines hello values that are permitted for this parameter, and assigns a default value (S1) if no value is specified.</span></span>

### <a name="workersize"></a><span data-ttu-id="ef72e-116">workerSize</span><span class="sxs-lookup"><span data-stu-id="ef72e-116">workerSize</span></span>
<span data-ttu-id="ef72e-117">barındırma planı (küçük, Orta veya büyük) hello Hello örnek boyutu.</span><span class="sxs-lookup"><span data-stu-id="ef72e-117">hello instance size of hello hosting plan (small, medium, or large).</span></span>

    "workerSize":{
      "type":"string",
      "allowedValues":[
        "0",
        "1",
        "2"
      ],
      "defaultValue":"0"
    }

<span data-ttu-id="ef72e-118">Merhaba şablonu (0, 1 veya 2) Bu parametre için izin verilen hello değerleri tanımlar ve herhangi bir değer belirtilmezse varsayılan değer (0) atar.</span><span class="sxs-lookup"><span data-stu-id="ef72e-118">hello template defines hello values that are permitted for this parameter (0, 1, or 2), and assigns a default value (0) if no value is specified.</span></span> <span data-ttu-id="ef72e-119">Merhaba değerler toosmall, Orta ve büyük karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="ef72e-119">hello values correspond toosmall, medium and large.</span></span>

