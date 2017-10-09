
### <a name="cacheskuname"></a><span data-ttu-id="182a5-101">cacheSKUName</span><span class="sxs-lookup"><span data-stu-id="182a5-101">cacheSKUName</span></span>
<span data-ttu-id="182a5-102">Fiyatlandırma katmanı hello Hello yeni Azure Redis önbelleği.</span><span class="sxs-lookup"><span data-stu-id="182a5-102">hello pricing tier of hello new Azure Redis Cache.</span></span>

    "cacheSKUName": {
      "type": "string",
      "allowedValues": [
        "Basic",
        "Standard"
      ],
      "defaultValue": "Basic",
      "metadata": {
        "description": "hello pricing tier of hello new Azure Redis Cache."
      }
    },

<span data-ttu-id="182a5-103">Merhaba şablonu (temel veya standart) Bu parametre için izin verilen ve herhangi bir değer belirtilmezse varsayılan değer (Temel) atayan hello değerleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="182a5-103">hello template defines hello values that are permitted for this parameter (Basic or Standard), and assigns a default value (Basic) if no value is specified.</span></span> <span data-ttu-id="182a5-104">Basic too53 GB kullanılabilir birden çok boyutu ile tek bir düğüm sağlar.</span><span class="sxs-lookup"><span data-stu-id="182a5-104">Basic provides a single node with multiple sizes available up too53 GB.</span></span>
<span data-ttu-id="182a5-105">Standart, iki düğümlü birincil/çoğaltma too53 GB ve % 99,9 SLA kullanılabilir birden çok boyutu, sağlar.</span><span class="sxs-lookup"><span data-stu-id="182a5-105">Standard provides two-node Primary/Replica with multiple sizes available up too53 GB and 99.9% SLA.</span></span>

### <a name="cacheskufamily"></a><span data-ttu-id="182a5-106">cacheSKUFamily</span><span class="sxs-lookup"><span data-stu-id="182a5-106">cacheSKUFamily</span></span>
<span data-ttu-id="182a5-107">Merhaba sku ailesi Hello.</span><span class="sxs-lookup"><span data-stu-id="182a5-107">hello family for hello sku.</span></span>

    "cacheSKUFamily": {
      "type": "string",
      "allowedValues": [
        "C"
      ],
      "defaultValue": "C",
      "metadata": {
        "description": "hello family for hello sku."
      }
    },


### <a name="cacheskucapacity"></a><span data-ttu-id="182a5-108">cacheSKUCapacity</span><span class="sxs-lookup"><span data-stu-id="182a5-108">cacheSKUCapacity</span></span>
<span data-ttu-id="182a5-109">Merhaba yeni Azure Redis önbelleği örneği Hello boyutu.</span><span class="sxs-lookup"><span data-stu-id="182a5-109">hello size of hello new Azure Redis Cache instance.</span></span> 

    "cacheSKUCapacity": {
      "type": "int",
      "allowedValues": [
        0,
        1,
        2,
        3,
        4,
        5,
        6
      ],
      "defaultValue": 0,
      "metadata": {
        "description": "hello size of hello new Azure Redis Cache instance. "
      }
    }


<span data-ttu-id="182a5-110">Merhaba şablonu (0, 1, 2, 3, 4, 5 veya 6) Bu parametre için izin verilen hello değerleri tanımlar ve herhangi bir değer belirtilmişse, varsayılan değer (1) atar.</span><span class="sxs-lookup"><span data-stu-id="182a5-110">hello template defines hello values that are permitted for this parameter (0, 1, 2, 3, 4, 5 or 6), and assigns a default value (1) if no value is specified.</span></span> <span data-ttu-id="182a5-111">Bu sayılar toofollowing önbellek boyutlarını karşılık gelir: 0 = 250 MB, 1 = 1 GB, 2 = 2,5 GB, 3 = 6 GB, 4 = 13 GB, 5 = 26 GB, 6 = 53 GB'a</span><span class="sxs-lookup"><span data-stu-id="182a5-111">Those numbers correspond toofollowing cache sizes: 0 = 250 MB, 1 = 1 GB, 2 = 2.5 GB, 3 = 6 GB, 4 = 13 GB, 5 = 26 GB, 6 = 53 GB</span></span>

