
### <a name="cacheskuname"></a><span data-ttu-id="f9ed2-101">cacheSKUName</span><span class="sxs-lookup"><span data-stu-id="f9ed2-101">cacheSKUName</span></span>
<span data-ttu-id="f9ed2-102">Yeni Azure Redis önbelleği fiyatlandırma katmanı.</span><span class="sxs-lookup"><span data-stu-id="f9ed2-102">The pricing tier of the new Azure Redis Cache.</span></span>

    "cacheSKUName": {
      "type": "string",
      "allowedValues": [
        "Basic",
        "Standard"
      ],
      "defaultValue": "Basic",
      "metadata": {
        "description": "The pricing tier of the new Azure Redis Cache."
      }
    },

<span data-ttu-id="f9ed2-103">Şablon (temel veya standart) Bu parametre için izin verilen değerleri tanımlar ve herhangi bir değer belirtilmezse varsayılan değer (Temel) atar.</span><span class="sxs-lookup"><span data-stu-id="f9ed2-103">The template defines the values that are permitted for this parameter (Basic or Standard), and assigns a default value (Basic) if no value is specified.</span></span> <span data-ttu-id="f9ed2-104">Basic yukarı kullanılabilir birden çok boyutu ile tek bir düğüm 53 GB'a sağlar.</span><span class="sxs-lookup"><span data-stu-id="f9ed2-104">Basic provides a single node with multiple sizes available up to 53 GB.</span></span>
<span data-ttu-id="f9ed2-105">Standart iki düğümlü birincil/çoğaltma yukarı kullanılabilir birden çok boyutu, 53 GB'a ve % 99,9 SLA sağlar.</span><span class="sxs-lookup"><span data-stu-id="f9ed2-105">Standard provides two-node Primary/Replica with multiple sizes available up to 53 GB and 99.9% SLA.</span></span>

### <a name="cacheskufamily"></a><span data-ttu-id="f9ed2-106">cacheSKUFamily</span><span class="sxs-lookup"><span data-stu-id="f9ed2-106">cacheSKUFamily</span></span>
<span data-ttu-id="f9ed2-107">SKU ailesi.</span><span class="sxs-lookup"><span data-stu-id="f9ed2-107">The family for the sku.</span></span>

    "cacheSKUFamily": {
      "type": "string",
      "allowedValues": [
        "C"
      ],
      "defaultValue": "C",
      "metadata": {
        "description": "The family for the sku."
      }
    },


### <a name="cacheskucapacity"></a><span data-ttu-id="f9ed2-108">cacheSKUCapacity</span><span class="sxs-lookup"><span data-stu-id="f9ed2-108">cacheSKUCapacity</span></span>
<span data-ttu-id="f9ed2-109">Yeni Azure Redis önbelleği örneği boyutu.</span><span class="sxs-lookup"><span data-stu-id="f9ed2-109">The size of the new Azure Redis Cache instance.</span></span> 

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
        "description": "The size of the new Azure Redis Cache instance. "
      }
    }


<span data-ttu-id="f9ed2-110">Şablon bu parametre (0, 1, 2, 3, 4, 5 veya 6) için izin verilen değerleri tanımlar ve herhangi bir değer belirtilmezse varsayılan değer (1) atar.</span><span class="sxs-lookup"><span data-stu-id="f9ed2-110">The template defines the values that are permitted for this parameter (0, 1, 2, 3, 4, 5 or 6), and assigns a default value (1) if no value is specified.</span></span> <span data-ttu-id="f9ed2-111">Bu sayı aşağıdaki önbellek boyutlarına karşılık gelen: 0 = 250 MB, 1 = 1 GB, 2 = 2,5 GB, 3 = 6 GB, 4 = 13 GB, 5 = 26 GB, 6 = 53 GB'a</span><span class="sxs-lookup"><span data-stu-id="f9ed2-111">Those numbers correspond to following cache sizes: 0 = 250 MB, 1 = 1 GB, 2 = 2.5 GB, 3 = 6 GB, 4 = 13 GB, 5 = 26 GB, 6 = 53 GB</span></span>

