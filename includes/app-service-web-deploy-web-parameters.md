<span data-ttu-id="34f44-101">Azure Resource Manager sayesinde, şablon dağıtıldığında belirtmek istediğiniz değerlerin parametrelerini siz tanımlarsınız.</span><span class="sxs-lookup"><span data-stu-id="34f44-101">With Azure Resource Manager, you define parameters for values you want to specify when the template is deployed.</span></span> <span data-ttu-id="34f44-102">Şablon tüm parametre değerleri içeren parametre adlı bir bölüm içerir.</span><span class="sxs-lookup"><span data-stu-id="34f44-102">The template includes a section called Parameters that contains all of the parameter values.</span></span>
<span data-ttu-id="34f44-103">Dağıttığınız projesini temel alan veya dağıttığınız ortamı dayanarak değişir bu değerleri için bir parametre tanımlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="34f44-103">You should define a parameter for those values that will vary based on the project you are deploying or based on the environment you are deploying to.</span></span> <span data-ttu-id="34f44-104">Her zaman aynı kalır değerleri parametrelerini tanımlamayın.</span><span class="sxs-lookup"><span data-stu-id="34f44-104">Do not define parameters for values that will always stay the same.</span></span> <span data-ttu-id="34f44-105">Her parametre değeri, dağıtılan kaynakları tanımlamak için şablonda kullanılır.</span><span class="sxs-lookup"><span data-stu-id="34f44-105">Each parameter value is used in the template to define the resources that are deployed.</span></span> 

<span data-ttu-id="34f44-106">Parametreleri tanımlarken kullanın **allowedValues** hangi kullanıcı değerleri belirtmek için alanını dağıtımı sırasında sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="34f44-106">When defining parameters, use the **allowedValues** field to specify which values a user can provide during deployment.</span></span> <span data-ttu-id="34f44-107">Kullanım **defaultValue** dağıtımı sırasında herhangi bir değer sağlanmazsa parametresi için bir değer atamaya alan.</span><span class="sxs-lookup"><span data-stu-id="34f44-107">Use the **defaultValue** field to assign a value to the parameter, if no value is provided during deployment.</span></span>

<span data-ttu-id="34f44-108">Biz şablondaki her bir parametreyi anlatmaktadır.</span><span class="sxs-lookup"><span data-stu-id="34f44-108">We will describe each parameter in the template.</span></span>

### <a name="sitename"></a><span data-ttu-id="34f44-109">SiteName</span><span class="sxs-lookup"><span data-stu-id="34f44-109">siteName</span></span>
<span data-ttu-id="34f44-110">Oluşturmak istediğiniz web uygulamasının adı.</span><span class="sxs-lookup"><span data-stu-id="34f44-110">The name of the web app that you wish to create.</span></span>

    "siteName":{
      "type":"string"
    }

### <a name="hostingplanname"></a><span data-ttu-id="34f44-111">hostingPlanName</span><span class="sxs-lookup"><span data-stu-id="34f44-111">hostingPlanName</span></span>
<span data-ttu-id="34f44-112">Web uygulamasını barındırmak için kullanılacak uygulama hizmeti planının adı.</span><span class="sxs-lookup"><span data-stu-id="34f44-112">The name of the App Service plan to use for hosting the web app.</span></span>

    "hostingPlanName":{
      "type":"string"
    }

### <a name="sku"></a><span data-ttu-id="34f44-113">SKU</span><span class="sxs-lookup"><span data-stu-id="34f44-113">sku</span></span>
<span data-ttu-id="34f44-114">Barındırma planı için fiyatlandırma katmanı.</span><span class="sxs-lookup"><span data-stu-id="34f44-114">The pricing tier for the hosting plan.</span></span>

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
        "description": "The pricing tier for the hosting plan."
      }
    }

<span data-ttu-id="34f44-115">Şablon bu parametre için izin verilen değerleri tanımlar ve herhangi bir değer belirtilmezse varsayılan değer (S1) atar.</span><span class="sxs-lookup"><span data-stu-id="34f44-115">The template defines the values that are permitted for this parameter, and assigns a default value (S1) if no value is specified.</span></span>

### <a name="workersize"></a><span data-ttu-id="34f44-116">workerSize</span><span class="sxs-lookup"><span data-stu-id="34f44-116">workerSize</span></span>
<span data-ttu-id="34f44-117">Barındırma planı (küçük, Orta veya büyük) örnek boyutunu.</span><span class="sxs-lookup"><span data-stu-id="34f44-117">The instance size of the hosting plan (small, medium, or large).</span></span>

    "workerSize":{
      "type":"string",
      "allowedValues":[
        "0",
        "1",
        "2"
      ],
      "defaultValue":"0"
    }

<span data-ttu-id="34f44-118">Şablon (0, 1 veya 2) Bu parametre için izin verilen değerleri tanımlar ve herhangi bir değer belirtilmezse varsayılan değer (0) atar.</span><span class="sxs-lookup"><span data-stu-id="34f44-118">The template defines the values that are permitted for this parameter (0, 1, or 2), and assigns a default value (0) if no value is specified.</span></span> <span data-ttu-id="34f44-119">Değerler için küçük, Orta ve büyük karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="34f44-119">The values correspond to small, medium and large.</span></span>

