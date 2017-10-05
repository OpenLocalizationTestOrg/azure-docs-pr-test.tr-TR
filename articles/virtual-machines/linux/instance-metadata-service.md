---
title: "Azure örneği meta veri hizmeti Linux VM'ler için | Microsoft Docs"
description: "Linux VM'ın işlem, ağ ve yaklaşan Bakımı olaylar hakkında bilgi almak için rESTful arabirimi."
services: virtual-machines-linux
documentationcenter: 
author: harijay
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 08/11/2017
ms.author: harijay
ms.openlocfilehash: a61acbe0532ece3a6a26ceb366c12c69db4c304c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-instance-metadata-service-for-linux-vms"></a><span data-ttu-id="79095-103">Linux VM'ler için Azure örneği meta veri hizmeti</span><span class="sxs-lookup"><span data-stu-id="79095-103">Azure Instance Metadata service for Linux VMs</span></span>


<span data-ttu-id="79095-104">Azure örneği meta veri hizmeti yönetmek ve sanal makinelerinizi yapılandırmak için kullanılan sanal makine örneği çalıştırma hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="79095-104">The Azure Instance Metadata Service provides information about running virtual machine instances that can be used to manage and configure your virtual machines.</span></span>
<span data-ttu-id="79095-105">Bu, SKU, ağ yapılandırması ve yaklaşan Bakımı olayları gibi bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="79095-105">This includes information such as SKU, network configuration, and upcoming maintenance events.</span></span> <span data-ttu-id="79095-106">Hangi tür bilgileri kullanılabilir daha fazla bilgi için bkz: [meta veri kategorileri](#instance-metadata-data-categories).</span><span class="sxs-lookup"><span data-stu-id="79095-106">For more information on what type of information is available, see [metadata categories](#instance-metadata-data-categories).</span></span>

<span data-ttu-id="79095-107">Azure'nın örnek meta veri hizmeti REST uç noktası aracılığıyla oluşturulan tüm Iaas VM'ler için erişilebilir olan [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span><span class="sxs-lookup"><span data-stu-id="79095-107">Azure's Instance Metadata Service is a REST Endpoint accessible to all IaaS VMs created via the [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span></span> <span data-ttu-id="79095-108">Uç nokta iyi bilinen yönlendirilemeyen IP adresinde mevcuttur (`169.254.169.254`), erişilebilir yalnızca VM dahilinde.</span><span class="sxs-lookup"><span data-stu-id="79095-108">The endpoint is available at a well-known non-routable IP address (`169.254.169.254`) that can be accessed only from within the VM.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="79095-109">Bu hizmet **genel olarak kullanılabilir** genel Azure bölgelerindeki.</span><span class="sxs-lookup"><span data-stu-id="79095-109">This service is  **generally available** in Global Azure Regions.</span></span> <span data-ttu-id="79095-110">Genel Önizleme kamu, Çin ve Almanca Azure bulutu için ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="79095-110">It is in Public preview for Government, China, and German Azure Cloud.</span></span> <span data-ttu-id="79095-111">Düzenli olarak, sanal makine örnekleri ilgili yeni bilgiler kullanıma sunmak için güncelleştirmeleri alır.</span><span class="sxs-lookup"><span data-stu-id="79095-111">It regularly receives updates to expose new information about virtual machine instances.</span></span> <span data-ttu-id="79095-112">Bu sayfayı güncel yansıtır [veri kategorilerini](#instance-metadata-data-categories) kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="79095-112">This page reflects the up-to-date [data categories](#instance-metadata-data-categories) available.</span></span>

## <a name="service-availability"></a><span data-ttu-id="79095-113">Hizmet kullanılabilirliği</span><span class="sxs-lookup"><span data-stu-id="79095-113">Service availability</span></span>
<span data-ttu-id="79095-114">Hizmeti genel olarak kullanılabilir tüm genel Azure bölgelerde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="79095-114">The service is available in all generally available Global Azure regions.</span></span> <span data-ttu-id="79095-115">Kamu, Çin veya Almanya bölgelerde genel önizlemede hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="79095-115">The service is in public preview  in the Government, China, or Germany regions.</span></span>

<span data-ttu-id="79095-116">Bölgeler</span><span class="sxs-lookup"><span data-stu-id="79095-116">Regions</span></span>                                        | <span data-ttu-id="79095-117">Kullanılabilirlik?</span><span class="sxs-lookup"><span data-stu-id="79095-117">Availability?</span></span>
-----------------------------------------------|-----------------------------------------------
[<span data-ttu-id="79095-118">Tüm genel olarak kullanılabilir genel Azure bölgeleri</span><span class="sxs-lookup"><span data-stu-id="79095-118">All Generally Available Global Azure Regions</span></span>](https://azure.microsoft.com/regions/)     | <span data-ttu-id="79095-119">Genel olarak kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="79095-119">Generally Available</span></span> 
[<span data-ttu-id="79095-120">Azure Devlet Kurumları</span><span class="sxs-lookup"><span data-stu-id="79095-120">Azure Government</span></span>](https://azure.microsoft.com/overview/clouds/government/)              | <span data-ttu-id="79095-121">Önizleme</span><span class="sxs-lookup"><span data-stu-id="79095-121">In Preview</span></span> 
[<span data-ttu-id="79095-122">Azure Çin</span><span class="sxs-lookup"><span data-stu-id="79095-122">Azure China</span></span>](https://www.azure.cn/)                                                           | <span data-ttu-id="79095-123">Önizleme</span><span class="sxs-lookup"><span data-stu-id="79095-123">In Preview</span></span>
[<span data-ttu-id="79095-124">Azure Almanya</span><span class="sxs-lookup"><span data-stu-id="79095-124">Azure Germany</span></span>](https://azure.microsoft.com/overview/clouds/germany/)                    | <span data-ttu-id="79095-125">Önizleme</span><span class="sxs-lookup"><span data-stu-id="79095-125">In Preview</span></span>

<span data-ttu-id="79095-126">Hizmet diğer Azure bulutta kullanılabilir olduğunda bu tabloya güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="79095-126">This table is updated when the service becomes available in other Azure clouds.</span></span>

<span data-ttu-id="79095-127">Örneği meta veri hizmeti denemek için bir VM'den oluşturmak [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/) veya [Azure portal](http://portal.azure.com) yukarıdaki bölgelerde ve aşağıdaki örnekleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="79095-127">To try out the Instance Metadata Service, create a VM from [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/) or the [Azure portal](http://portal.azure.com) in the above regions and follow the examples below.</span></span>

## <a name="usage"></a><span data-ttu-id="79095-128">Kullanım</span><span class="sxs-lookup"><span data-stu-id="79095-128">Usage</span></span>

### <a name="versioning"></a><span data-ttu-id="79095-129">Sürüm oluşturma</span><span class="sxs-lookup"><span data-stu-id="79095-129">Versioning</span></span>
<span data-ttu-id="79095-130">Örnek meta veri sürümü tutulan hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="79095-130">The Instance Metadata Service is versioned.</span></span> <span data-ttu-id="79095-131">Sürümleri zorunludur ve geçerli sürümü `2017-04-02`.</span><span class="sxs-lookup"><span data-stu-id="79095-131">Versions are mandatory and the current version is `2017-04-02`.</span></span>

> [!NOTE] 
> <span data-ttu-id="79095-132">Önceki Önizleme sürümleri {son} API sürümü desteklenen zamanlanmış olaylar.</span><span class="sxs-lookup"><span data-stu-id="79095-132">Previous preview releases of scheduled events supported {latest} as the api-version.</span></span> <span data-ttu-id="79095-133">Bu biçim artık desteklenmemektedir ve gelecekte kullanım dışı kalacaktır.</span><span class="sxs-lookup"><span data-stu-id="79095-133">This format is no longer supported and will be deprecated in the future.</span></span>

<span data-ttu-id="79095-134">Yeni sürümler eklediğimiz gibi komut dosyalarınızı belirli veri biçimleri üzerinde bağımlılıkları varsa, daha eski sürümlerini yine de uyumluluk için erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="79095-134">As we add newer versions, older versions can still be accessed for compatibility if your scripts have dependencies on specific data formats.</span></span> <span data-ttu-id="79095-135">Ancak, hizmetin genel olarak kullanılabilir olduğunda geçerli Önizleme version(2017-03-01) kullanılamayabilir olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="79095-135">However, note that the current preview version(2017-03-01) may not be available once the service is generally available.</span></span>

### <a name="using-headers"></a><span data-ttu-id="79095-136">Üst bilgileri kullanma</span><span class="sxs-lookup"><span data-stu-id="79095-136">Using headers</span></span>
<span data-ttu-id="79095-137">Örnek meta veri hizmeti sorguladığınızda başlık sağlamalısınız `Metadata: true` istek istemeden yönlendirilmeyen emin olmak için.</span><span class="sxs-lookup"><span data-stu-id="79095-137">When you query the Instance Metadata Service, you must provide the header `Metadata: true` to ensure the request was not unintentionally redirected.</span></span>

### <a name="retrieving-metadata"></a><span data-ttu-id="79095-138">Meta veri alma</span><span class="sxs-lookup"><span data-stu-id="79095-138">Retrieving metadata</span></span>

<span data-ttu-id="79095-139">Örnek meta verileri oluşturulan yönetilen/kullanarak sanal makineleri çalıştırmak için kullanılabilir [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span><span class="sxs-lookup"><span data-stu-id="79095-139">Instance metadata is available for running VMs created/managed using [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span></span> <span data-ttu-id="79095-140">Aşağıdaki isteği kullanarak bir sanal makine örneği için tüm veri kategorilerini erişebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="79095-140">Access all data categories for a virtual machine instance using the following request:</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

> [!NOTE] 
> <span data-ttu-id="79095-141">Tüm örnek meta veri sorguları büyük/küçük harfe duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="79095-141">All instance metadata queries are case-sensitive.</span></span>

### <a name="data-output"></a><span data-ttu-id="79095-142">Veri çıkışı</span><span class="sxs-lookup"><span data-stu-id="79095-142">Data output</span></span>
<span data-ttu-id="79095-143">Varsayılan olarak, örnek meta veri hizmeti verileri JSON biçiminde döndürür (`Content-Type: application/json`).</span><span class="sxs-lookup"><span data-stu-id="79095-143">By default, the Instance Metadata Service returns data in JSON format (`Content-Type: application/json`).</span></span> <span data-ttu-id="79095-144">Ancak, farklı API'leri verileri farklı biçimlerde istediyseniz döndürebilir.</span><span class="sxs-lookup"><span data-stu-id="79095-144">However, different APIs can return data in different formats if requested.</span></span>
<span data-ttu-id="79095-145">Aşağıdaki tabloda, API destekleyebilir diğer veri biçimlerini başvurudur.</span><span class="sxs-lookup"><span data-stu-id="79095-145">The following table is a reference of other data formats APIs may support.</span></span>

<span data-ttu-id="79095-146">API</span><span class="sxs-lookup"><span data-stu-id="79095-146">API</span></span> | <span data-ttu-id="79095-147">Varsayılan veri biçimi</span><span class="sxs-lookup"><span data-stu-id="79095-147">Default Data Format</span></span> | <span data-ttu-id="79095-148">Diğer biçimlere</span><span class="sxs-lookup"><span data-stu-id="79095-148">Other Formats</span></span>
--------|---------------------|--------------
<span data-ttu-id="79095-149">/instance</span><span class="sxs-lookup"><span data-stu-id="79095-149">/instance</span></span> | <span data-ttu-id="79095-150">JSON</span><span class="sxs-lookup"><span data-stu-id="79095-150">json</span></span> | <span data-ttu-id="79095-151">Metin</span><span class="sxs-lookup"><span data-stu-id="79095-151">text</span></span>
<span data-ttu-id="79095-152">/scheduledevents</span><span class="sxs-lookup"><span data-stu-id="79095-152">/scheduledevents</span></span> | <span data-ttu-id="79095-153">JSON</span><span class="sxs-lookup"><span data-stu-id="79095-153">json</span></span> | <span data-ttu-id="79095-154">Yok</span><span class="sxs-lookup"><span data-stu-id="79095-154">none</span></span>

<span data-ttu-id="79095-155">Varsayılan olmayan yanıt biçimi erişmek için bir istek sorgu dizesi parametresi olarak istenen biçim belirtin.</span><span class="sxs-lookup"><span data-stu-id="79095-155">To access a non-default response format, specify the requested format as a querystring parameter in the request.</span></span> <span data-ttu-id="79095-156">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="79095-156">For example:</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02&format=text"
```

### <a name="security"></a><span data-ttu-id="79095-157">Güvenlik</span><span class="sxs-lookup"><span data-stu-id="79095-157">Security</span></span>
<span data-ttu-id="79095-158">Örnek meta veri Hizmeti uç noktası yalnızca yönlendirilebilir olmayan bir IP adresi üzerinde çalışan sanal makine örneği içinde erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="79095-158">The Instance Metadata Service endpoint is accessible only from within the running virtual machine instance on a non-routable IP address.</span></span> <span data-ttu-id="79095-159">Ayrıca, herhangi bir ile istek bir `X-Forwarded-For` üstbilgi hizmeti tarafından reddedildi.</span><span class="sxs-lookup"><span data-stu-id="79095-159">In addition, any request with a `X-Forwarded-For` header is rejected by the service.</span></span>
<span data-ttu-id="79095-160">Biz de içerecek şekilde istekleri gerektiren bir `Metadata: true` üstbilgi gerçek isteği doğrudan istenen ve istenmeyen yeniden yönlendirme bir parçası olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="79095-160">We also require requests to contain a `Metadata: true` header to ensure that the actual request was directly intended and not a part of unintentional redirection.</span></span> 

### <a name="error"></a><span data-ttu-id="79095-161">Hata</span><span class="sxs-lookup"><span data-stu-id="79095-161">Error</span></span>
<span data-ttu-id="79095-162">Bir veri öğesi bulunamadı veya hatalı biçimlendirilmiş bir istek varsa örneği meta veri hizmeti standart HTTP hatalarını döndürür.</span><span class="sxs-lookup"><span data-stu-id="79095-162">If there is a data element not found or a malformed request, the Instance Metadata Service returns standard HTTP errors.</span></span> <span data-ttu-id="79095-163">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="79095-163">For example:</span></span>

<span data-ttu-id="79095-164">HTTP durum kodu</span><span class="sxs-lookup"><span data-stu-id="79095-164">HTTP Status Code</span></span> | <span data-ttu-id="79095-165">Neden</span><span class="sxs-lookup"><span data-stu-id="79095-165">Reason</span></span>
----------------|-------
<span data-ttu-id="79095-166">200 TAMAM</span><span class="sxs-lookup"><span data-stu-id="79095-166">200 OK</span></span> |
<span data-ttu-id="79095-167">400 Hatalı istek</span><span class="sxs-lookup"><span data-stu-id="79095-167">400 Bad Request</span></span> | <span data-ttu-id="79095-168">Eksik `Metadata: true` üstbilgisi</span><span class="sxs-lookup"><span data-stu-id="79095-168">Missing `Metadata: true` header</span></span>
<span data-ttu-id="79095-169">404 Bulunamadı</span><span class="sxs-lookup"><span data-stu-id="79095-169">404 Not Found</span></span> | <span data-ttu-id="79095-170">İstenen öğe does't var</span><span class="sxs-lookup"><span data-stu-id="79095-170">The requested element does't exist</span></span> 
<span data-ttu-id="79095-171">405 Yönteme izin verilmiyor</span><span class="sxs-lookup"><span data-stu-id="79095-171">405 Method Not Allowed</span></span> | <span data-ttu-id="79095-172">Yalnızca `GET` ve `POST` istekleri desteklenir</span><span class="sxs-lookup"><span data-stu-id="79095-172">Only `GET` and `POST` requests are supported</span></span>
<span data-ttu-id="79095-173">429 çok fazla istek</span><span class="sxs-lookup"><span data-stu-id="79095-173">429 Too Many Requests</span></span> | <span data-ttu-id="79095-174">API şu anda en fazla saniyede 5 sorgularını destekler</span><span class="sxs-lookup"><span data-stu-id="79095-174">The API currently supports a maximum of 5 queries per second</span></span>
<span data-ttu-id="79095-175">500 hizmet hatası</span><span class="sxs-lookup"><span data-stu-id="79095-175">500 Service Error</span></span>     | <span data-ttu-id="79095-176">Bir süre sonra yeniden deneyin</span><span class="sxs-lookup"><span data-stu-id="79095-176">Retry after some time</span></span>

### <a name="examples"></a><span data-ttu-id="79095-177">Örnekler</span><span class="sxs-lookup"><span data-stu-id="79095-177">Examples</span></span>

> [!NOTE] 
> <span data-ttu-id="79095-178">Tüm API yanıtları JSON dizelerdir.</span><span class="sxs-lookup"><span data-stu-id="79095-178">All API responses are JSON strings.</span></span> <span data-ttu-id="79095-179">Okunabilirlik için pretty yazdırılan tüm aşağıdaki örnek yanıtlar.</span><span class="sxs-lookup"><span data-stu-id="79095-179">All following example responses  are pretty-printed for readability.</span></span>

#### <a name="retrieving-network-information"></a><span data-ttu-id="79095-180">Ağ bilgileri alınıyor</span><span class="sxs-lookup"><span data-stu-id="79095-180">Retrieving network information</span></span>

<span data-ttu-id="79095-181">**İstek**</span><span class="sxs-lookup"><span data-stu-id="79095-181">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network?api-version=2017-04-02"
```

<span data-ttu-id="79095-182">**Yanıt**</span><span class="sxs-lookup"><span data-stu-id="79095-182">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="79095-183">Yanıtı bir JSON dizesidir.</span><span class="sxs-lookup"><span data-stu-id="79095-183">The response is a JSON string.</span></span> <span data-ttu-id="79095-184">Aşağıdaki örnek yanıt okunabilirlik için pretty yazdırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="79095-184">The following example response is pretty-printed for readability.</span></span>

```
{
  "interface": [
    {
      "ipv4": {
        "ipAddress": [
          {
            "privateIpAddress": "10.1.0.4",
            "publicIpAddress": "X.X.X.X"
          }
        ],
        "subnet": [
          {
            "address": "10.1.0.0",
            "prefix": "24"
          }
        ]
      },
      "ipv6": {
        "ipAddress": []
      },
      "macAddress": "000D3AF806EC"
    }
  ]
}

```

#### <a name="retrieving-public-ip-address"></a><span data-ttu-id="79095-185">Genel IP adresi alınıyor</span><span class="sxs-lookup"><span data-stu-id="79095-185">Retrieving public IP address</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network/interface/0/ipv4/ipAddress/0/publicIpAddress?api-version=2017-04-02&format=text"
```

#### <a name="retrieving-all-metadata-for-an-instance"></a><span data-ttu-id="79095-186">Bir örneği için tüm meta veri alma</span><span class="sxs-lookup"><span data-stu-id="79095-186">Retrieving all metadata for an instance</span></span>

<span data-ttu-id="79095-187">**İstek**</span><span class="sxs-lookup"><span data-stu-id="79095-187">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

<span data-ttu-id="79095-188">**Yanıt**</span><span class="sxs-lookup"><span data-stu-id="79095-188">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="79095-189">Yanıtı bir JSON dizesidir.</span><span class="sxs-lookup"><span data-stu-id="79095-189">The response is a JSON string.</span></span> <span data-ttu-id="79095-190">Aşağıdaki örnek yanıt okunabilirlik için pretty yazdırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="79095-190">The following example response is pretty-printed for readability.</span></span>

```
{
  "compute": {
    "location": "westcentralus",
    "name": "IMDSSample",
    "offer": "UbuntuServer",
    "osType": "Linux",
    "platformFaultDomain": "0",
    "platformUpdateDomain": "0",
    "publisher": "Canonical",
    "sku": "16.04.0-LTS",
    "version": "16.04.201610200",
    "vmId": "5d33a910-a7a0-4443-9f01-6a807801b29b",
    "vmSize": "Standard_A1"
  },
  "network": {
    "interface": [
      {
        "ipv4": {
          "ipAddress": [
            {
              "privateIpAddress": "10.1.0.4",
              "publicIpAddress": "X.X.X.X"
            }
          ],
          "subnet": [
            {
              "address": "10.1.0.0",
              "prefix": "24"
            }
          ]
        },
        "ipv6": {
          "ipAddress": []
        },
        "macAddress": "000D3AF806EC"
      }
    ]
  }
}
```

#### <a name="retrieving-metadata-in-windows-virtual-machine"></a><span data-ttu-id="79095-191">Meta veriler de Windows sanal makinesi alınıyor</span><span class="sxs-lookup"><span data-stu-id="79095-191">Retrieving metadata in Windows Virtual Machine</span></span>

<span data-ttu-id="79095-192">**İstek**</span><span class="sxs-lookup"><span data-stu-id="79095-192">**Request**</span></span>

<span data-ttu-id="79095-193">Örnek meta verileri alınabilir Windows PowerShell yardımcı programı `curl`:</span><span class="sxs-lookup"><span data-stu-id="79095-193">Instance metadata can be retrieved in Windows via the PowerShell utility `curl`:</span></span> 

```
curl -H @{'Metadata'='true'} http://169.254.169.254/metadata/instance?api-version=2017-04-02 | select -ExpandProperty Content
```

<span data-ttu-id="79095-194">Aracılığıyla veya `Invoke-RestMethod` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="79095-194">Or through the `Invoke-RestMethod` cmdlet:</span></span>
    
```
Invoke-RestMethod -Headers @{"Metadata"="true"} -URI http://169.254.169.254/metadata/instance?api-version=2017-04-02 -Method get 
```

<span data-ttu-id="79095-195">**Yanıt**</span><span class="sxs-lookup"><span data-stu-id="79095-195">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="79095-196">Yanıtı bir JSON dizesidir.</span><span class="sxs-lookup"><span data-stu-id="79095-196">The response is a JSON string.</span></span> <span data-ttu-id="79095-197">Aşağıdaki örnek yanıt okunabilirlik için pretty yazdırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="79095-197">The following example response  is pretty-printed for readability.</span></span>

```
{
  "compute": {
    "location": "westus",
    "name": "SQLTest",
    "offer": "SQL2016SP1-WS2016",
    "osType": "Windows",
    "platformFaultDomain": "0",
    "platformUpdateDomain": "0",
    "publisher": "MicrosoftSQLServer",
    "sku": "Enterprise",
    "version": "13.0.400110",
    "vmId": "453945c8-3923-4366-b2d3-ea4c80e9b70e",
    "vmSize": "Standard_DS2"
  },
  "network": {
    "interface": [
      {
        "ipv4": {
          "ipAddress": [
            {
              "privateIpAddress": "10.0.1.4",
              "publicIpAddress": "X.X.X.X"
            }
          ],
          "subnet": [
            {
              "address": "10.0.1.0",
              "prefix": "24"
            }
          ]
        },
        "ipv6": {
          "ipAddress": [
            
          ]
        },
        "macAddress": "002248020E1E"
      }
    ]
  }
}
```

## <a name="instance-metadata-data-categories"></a><span data-ttu-id="79095-198">Örnek meta veri kategorileri</span><span class="sxs-lookup"><span data-stu-id="79095-198">Instance metadata data categories</span></span>
<span data-ttu-id="79095-199">Aşağıdaki veri kategorilerini örneği meta veri hizmeti kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="79095-199">The following data categories are available through the Instance Metadata Service:</span></span>

<span data-ttu-id="79095-200">Veriler</span><span class="sxs-lookup"><span data-stu-id="79095-200">Data</span></span> | <span data-ttu-id="79095-201">Açıklama</span><span class="sxs-lookup"><span data-stu-id="79095-201">Description</span></span>
-----|------------
<span data-ttu-id="79095-202">location</span><span class="sxs-lookup"><span data-stu-id="79095-202">location</span></span> | <span data-ttu-id="79095-203">Azure bölgesi VM çalışır durumda</span><span class="sxs-lookup"><span data-stu-id="79095-203">Azure Region the VM is running in</span></span>
<span data-ttu-id="79095-204">ad</span><span class="sxs-lookup"><span data-stu-id="79095-204">name</span></span> | <span data-ttu-id="79095-205">VM adı</span><span class="sxs-lookup"><span data-stu-id="79095-205">Name of the VM</span></span> 
<span data-ttu-id="79095-206">Teklif</span><span class="sxs-lookup"><span data-stu-id="79095-206">offer</span></span> | <span data-ttu-id="79095-207">VM görüntüsü için bilgi sunar.</span><span class="sxs-lookup"><span data-stu-id="79095-207">Offer information for the VM image.</span></span> <span data-ttu-id="79095-208">Bu değer yalnızca Azure resmi Galerisi'nden dağıtılan görüntüleri için mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="79095-208">This value is only present for images deployed from Azure image gallery.</span></span>
<span data-ttu-id="79095-209">Yayımcı</span><span class="sxs-lookup"><span data-stu-id="79095-209">publisher</span></span> | <span data-ttu-id="79095-210">VM görüntüsü yayımcısı</span><span class="sxs-lookup"><span data-stu-id="79095-210">Publisher of the VM image</span></span>
<span data-ttu-id="79095-211">SKU</span><span class="sxs-lookup"><span data-stu-id="79095-211">sku</span></span> | <span data-ttu-id="79095-212">VM görüntüsü için belirli SKU</span><span class="sxs-lookup"><span data-stu-id="79095-212">Specific SKU for the VM image</span></span>  
<span data-ttu-id="79095-213">Sürüm</span><span class="sxs-lookup"><span data-stu-id="79095-213">version</span></span> | <span data-ttu-id="79095-214">VM görüntüsü</span><span class="sxs-lookup"><span data-stu-id="79095-214">Version of the VM image</span></span> 
<span data-ttu-id="79095-215">osType</span><span class="sxs-lookup"><span data-stu-id="79095-215">osType</span></span> | <span data-ttu-id="79095-216">Linux veya Windows</span><span class="sxs-lookup"><span data-stu-id="79095-216">Linux or Windows</span></span> 
<span data-ttu-id="79095-217">platformUpdateDomain</span><span class="sxs-lookup"><span data-stu-id="79095-217">platformUpdateDomain</span></span> |  <span data-ttu-id="79095-218">[Güncelleştirme etki alanı](manage-availability.md) VM'nin çalışır durumda</span><span class="sxs-lookup"><span data-stu-id="79095-218">[Update domain](manage-availability.md) the VM is running in</span></span>
<span data-ttu-id="79095-219">platformFaultDomain</span><span class="sxs-lookup"><span data-stu-id="79095-219">platformFaultDomain</span></span> | <span data-ttu-id="79095-220">[Hata etki alanı](manage-availability.md) VM'nin çalışır durumda</span><span class="sxs-lookup"><span data-stu-id="79095-220">[Fault domain](manage-availability.md) the VM is running in</span></span>
<span data-ttu-id="79095-221">Bunun nedeni</span><span class="sxs-lookup"><span data-stu-id="79095-221">vmId</span></span> | <span data-ttu-id="79095-222">[Benzersiz tanımlayıcı](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/) VM</span><span class="sxs-lookup"><span data-stu-id="79095-222">[Unique identifier](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/) for the VM</span></span>
<span data-ttu-id="79095-223">vmSize</span><span class="sxs-lookup"><span data-stu-id="79095-223">vmSize</span></span> | [<span data-ttu-id="79095-224">VM boyutu</span><span class="sxs-lookup"><span data-stu-id="79095-224">VM size</span></span>](sizes.md)
<span data-ttu-id="79095-225">IPv4/privateIpAddress</span><span class="sxs-lookup"><span data-stu-id="79095-225">ipv4/privateIpAddress</span></span> | <span data-ttu-id="79095-226">VM yerel IPv4 adresi</span><span class="sxs-lookup"><span data-stu-id="79095-226">Local IPv4 address of the VM</span></span> 
<span data-ttu-id="79095-227">IPv4/Publicıpaddress</span><span class="sxs-lookup"><span data-stu-id="79095-227">ipv4/publicIpAddress</span></span> | <span data-ttu-id="79095-228">VM genel IPv4 adresi</span><span class="sxs-lookup"><span data-stu-id="79095-228">Public IPv4 address of the VM</span></span>
<span data-ttu-id="79095-229">alt ağ/adresi</span><span class="sxs-lookup"><span data-stu-id="79095-229">subnet/address</span></span> | <span data-ttu-id="79095-230">VM alt ağ adresi</span><span class="sxs-lookup"><span data-stu-id="79095-230">Subnet address of the VM</span></span>
<span data-ttu-id="79095-231">alt ağ/öneki</span><span class="sxs-lookup"><span data-stu-id="79095-231">subnet/prefix</span></span> | <span data-ttu-id="79095-232">Alt ağ öneki, örnek 24</span><span class="sxs-lookup"><span data-stu-id="79095-232">Subnet prefix, example 24</span></span>
<span data-ttu-id="79095-233">IPv6/IPADDRESS</span><span class="sxs-lookup"><span data-stu-id="79095-233">ipv6/ipAddress</span></span> | <span data-ttu-id="79095-234">VM yerel IPv6 adresi</span><span class="sxs-lookup"><span data-stu-id="79095-234">Local IPv6 address of the VM</span></span>
<span data-ttu-id="79095-235">MacAddress</span><span class="sxs-lookup"><span data-stu-id="79095-235">macAddress</span></span> | <span data-ttu-id="79095-236">VM mac adresi</span><span class="sxs-lookup"><span data-stu-id="79095-236">VM mac address</span></span> 
<span data-ttu-id="79095-237">scheduledevents</span><span class="sxs-lookup"><span data-stu-id="79095-237">scheduledevents</span></span> | <span data-ttu-id="79095-238">Genel önizlemesini görmek, şu anda [scheduledevents](scheduled-events.md)</span><span class="sxs-lookup"><span data-stu-id="79095-238">Currently in Public Preview See [scheduledevents](scheduled-events.md)</span></span>

## <a name="example-scenarios-for-usage"></a><span data-ttu-id="79095-239">Kullanım için örnek senaryolar</span><span class="sxs-lookup"><span data-stu-id="79095-239">Example scenarios for usage</span></span>  

### <a name="tracking-vm-running-on-azure"></a><span data-ttu-id="79095-240">Azure üzerinde çalışan VM izleme</span><span class="sxs-lookup"><span data-stu-id="79095-240">Tracking VM running on Azure</span></span>

<span data-ttu-id="79095-241">Bir hizmet sağlayıcısı olarak yazılımınızı çalışan VM sayısı izlemek veya VM benzersizliğini izlemeniz gereken aracıların gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="79095-241">As a service provider, you may require to track the number of VMs running your software or have agents that need to track uniqueness of the VM.</span></span> <span data-ttu-id="79095-242">Bir VM için benzersiz bir kimliği elde edebilmek için kullanmak `vmId` örneği meta veri hizmetinden alan.</span><span class="sxs-lookup"><span data-stu-id="79095-242">To be able to get a unique ID for a VM, use the `vmId` field from Instance Metadata Service.</span></span>

<span data-ttu-id="79095-243">**İstek**</span><span class="sxs-lookup"><span data-stu-id="79095-243">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/vmId?api-version=2017-04-02&format=text"
```

<span data-ttu-id="79095-244">**Yanıt**</span><span class="sxs-lookup"><span data-stu-id="79095-244">**Response**</span></span>

```
5c08b38e-4d57-4c23-ac45-aca61037f084
```

### <a name="placement-of-containers-data-partitions-based-faultupdate-domain"></a><span data-ttu-id="79095-245">Yerleştirme kapsayıcıların veri bölümlerini arıza/güncelleştirme etki alanı tabanlı</span><span class="sxs-lookup"><span data-stu-id="79095-245">Placement of containers, data-partitions based fault/update domain</span></span> 

<span data-ttu-id="79095-246">Belirli senaryolar, farklı veri çoğaltmaları yerleşimini prime çok önemlidir.</span><span class="sxs-lookup"><span data-stu-id="79095-246">For certain scenarios, placement of different data replicas is of prime importance.</span></span> <span data-ttu-id="79095-247">Örneğin, [HDFS çoğaltma yerleştirme](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html#Replica_Placement:_The_First_Baby_Steps) veya kapsayıcı yerleştirme aracılığıyla bir [orchestrator](https://kubernetes.io/docs/user-guide/node-selection/) bilmek gerektirebilir `platformFaultDomain` ve `platformUpdateDomain` VM'nin çalışır.</span><span class="sxs-lookup"><span data-stu-id="79095-247">For example, [HDFS replica placement](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html#Replica_Placement:_The_First_Baby_Steps) or container placement via an [orchestrator](https://kubernetes.io/docs/user-guide/node-selection/) may you require to know the `platformFaultDomain` and `platformUpdateDomain` the VM is running on.</span></span>
<span data-ttu-id="79095-248">Bu veri örneği meta veri hizmeti üzerinden doğrudan sorgulayabilir.</span><span class="sxs-lookup"><span data-stu-id="79095-248">You can query this data directly via the Instance Metadata Service.</span></span>

<span data-ttu-id="79095-249">**İstek**</span><span class="sxs-lookup"><span data-stu-id="79095-249">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/platformFaultDomain?api-version=2017-04-02&format=text" 
```

<span data-ttu-id="79095-250">**Yanıt**</span><span class="sxs-lookup"><span data-stu-id="79095-250">**Response**</span></span>

```
0
```

### <a name="getting-more-information-about-the-vm-during-support-case"></a><span data-ttu-id="79095-251">Destek olayı sırasında VM hakkında daha fazla bilgi alma</span><span class="sxs-lookup"><span data-stu-id="79095-251">Getting more information about the VM during support case</span></span> 

<span data-ttu-id="79095-252">Bir hizmet sağlayıcısı olarak, burada VM hakkında daha fazla bilgiye istediğiniz bir destek çağrısı alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="79095-252">As a service provider, you may get a support call where you would like to know more information about the VM.</span></span> <span data-ttu-id="79095-253">İşlem meta verileri paylaşmak için müşteri isteyen Azure VM'de türü hakkında bilgi edinmek için profesyonel desteği için temel bilgiler sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="79095-253">Asking the customer to share the compute metadata can provide basic information for the support professional to know about the kind of VM on Azure.</span></span> 

<span data-ttu-id="79095-254">**İstek**</span><span class="sxs-lookup"><span data-stu-id="79095-254">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute?api-version=2017-04-02"
```

<span data-ttu-id="79095-255">**Yanıt**</span><span class="sxs-lookup"><span data-stu-id="79095-255">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="79095-256">Yanıtı bir JSON dizesidir.</span><span class="sxs-lookup"><span data-stu-id="79095-256">The response is a JSON string.</span></span> <span data-ttu-id="79095-257">Aşağıdaki örnek yanıt okunabilirlik için pretty yazdırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="79095-257">The following example response is pretty-printed for readability.</span></span>

```
{
  "compute": {
    "location": "CentralUS",
    "name": "IMDSCanary",
    "offer": "RHEL",
    "osType": "Linux",
    "platformFaultDomain": "0",
    "platformUpdateDomain": "0",
    "publisher": "RedHat",
    "sku": "7.2",
    "version": "7.2.20161026",
    "vmId": "5c08b38e-4d57-4c23-ac45-aca61037f084",
    "vmSize": "Standard_DS2"
  }
}
```

### <a name="examples-of-calling-metadata-service-using-different-languages-inside-the-vm"></a><span data-ttu-id="79095-258">VM içindeki farklı dillerde kullanarak meta veri hizmeti çağrılırken örnekleri</span><span class="sxs-lookup"><span data-stu-id="79095-258">Examples of calling metadata service using different languages inside the VM</span></span> 

<span data-ttu-id="79095-259">Dil</span><span class="sxs-lookup"><span data-stu-id="79095-259">Language</span></span> | <span data-ttu-id="79095-260">Örnek</span><span class="sxs-lookup"><span data-stu-id="79095-260">Example</span></span> 
---------|----------------
<span data-ttu-id="79095-261">Ruby</span><span class="sxs-lookup"><span data-stu-id="79095-261">Ruby</span></span>     | <span data-ttu-id="79095-262">https://github.com/Microsoft/azureimds/BLOB/master/IMDSSample.RB</span><span class="sxs-lookup"><span data-stu-id="79095-262">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.rb</span></span>
<span data-ttu-id="79095-263">LAN gidin</span><span class="sxs-lookup"><span data-stu-id="79095-263">Go Lan</span></span>   | <span data-ttu-id="79095-264">https://github.com/Microsoft/azureimds/BLOB/master/imdssample.go</span><span class="sxs-lookup"><span data-stu-id="79095-264">https://github.com/Microsoft/azureimds/blob/master/imdssample.go</span></span>            
<span data-ttu-id="79095-265">python</span><span class="sxs-lookup"><span data-stu-id="79095-265">python</span></span>   | <span data-ttu-id="79095-266">https://github.com/Microsoft/azureimds/BLOB/master/IMDSSample.PY</span><span class="sxs-lookup"><span data-stu-id="79095-266">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.py</span></span>
<span data-ttu-id="79095-267">C++</span><span class="sxs-lookup"><span data-stu-id="79095-267">C++</span></span>      | <span data-ttu-id="79095-268">https://github.com/Microsoft/azureimds/BLOB/master/IMDSSample-Windows.cpp</span><span class="sxs-lookup"><span data-stu-id="79095-268">https://github.com/Microsoft/azureimds/blob/master/IMDSSample-windows.cpp</span></span>
<span data-ttu-id="79095-269">C#</span><span class="sxs-lookup"><span data-stu-id="79095-269">C#</span></span>       | <span data-ttu-id="79095-270">https://github.com/Microsoft/azureimds/BLOB/master/IMDSSample.cs</span><span class="sxs-lookup"><span data-stu-id="79095-270">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.cs</span></span>
<span data-ttu-id="79095-271">Javascript</span><span class="sxs-lookup"><span data-stu-id="79095-271">Javascript</span></span> | <span data-ttu-id="79095-272">https://github.com/Microsoft/azureimds/BLOB/master/IMDSSample.js</span><span class="sxs-lookup"><span data-stu-id="79095-272">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.js</span></span>
<span data-ttu-id="79095-273">PowerShell</span><span class="sxs-lookup"><span data-stu-id="79095-273">Powershell</span></span> | <span data-ttu-id="79095-274">https://github.com/Microsoft/azureimds/BLOB/master/IMDSSample.ps1</span><span class="sxs-lookup"><span data-stu-id="79095-274">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.ps1</span></span>
<span data-ttu-id="79095-275">Bash</span><span class="sxs-lookup"><span data-stu-id="79095-275">Bash</span></span>       | <span data-ttu-id="79095-276">https://github.com/Microsoft/azureimds/BLOB/master/IMDSSample.sh</span><span class="sxs-lookup"><span data-stu-id="79095-276">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.sh</span></span>
    

## <a name="faq"></a><span data-ttu-id="79095-277">SSS</span><span class="sxs-lookup"><span data-stu-id="79095-277">FAQ</span></span>
1. <span data-ttu-id="79095-278">Hata alıyorum `400 Bad Request, Required metadata header not specified`.</span><span class="sxs-lookup"><span data-stu-id="79095-278">I am getting the error `400 Bad Request, Required metadata header not specified`.</span></span> <span data-ttu-id="79095-279">Bu ne anlama geliyor?</span><span class="sxs-lookup"><span data-stu-id="79095-279">What does this mean?</span></span>
   * <span data-ttu-id="79095-280">Üst bilgisi örneği meta veri hizmeti gerektiriyor `Metadata: true` istekte geçirilecek.</span><span class="sxs-lookup"><span data-stu-id="79095-280">The Instance Metadata Service requires the header `Metadata: true` to be passed in the request.</span></span> <span data-ttu-id="79095-281">Bu üst REST çağrısı geçirme örneği meta veri hizmeti erişmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="79095-281">Passing this header in the REST call allows access to the Instance Metadata Service.</span></span> 
2. <span data-ttu-id="79095-282">Neden VM'im için işlem bilgi alıyorum değil mi?</span><span class="sxs-lookup"><span data-stu-id="79095-282">Why am I not getting compute information for my VM?</span></span>
   * <span data-ttu-id="79095-283">Şu anda örneği meta veri hizmeti, yalnızca Azure Kaynak Yöneticisi ile oluşturulan örnekleri destekler.</span><span class="sxs-lookup"><span data-stu-id="79095-283">Currently the Instance Metadata Service only supports instances created with Azure Resource Manager.</span></span> <span data-ttu-id="79095-284">Gelecekte, biz bulut hizmeti VM'ler için destek ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="79095-284">In the future, we may add support for Cloud Service VMs.</span></span>
3. <span data-ttu-id="79095-285">Sanal Makinem Azure Resource Manager aracılığıyla geri bir süre oluşturdum.</span><span class="sxs-lookup"><span data-stu-id="79095-285">I created my Virtual Machine through Azure Resource Manager a while back.</span></span> <span data-ttu-id="79095-286">Bkz: değil neden ben meta veri bilgileri işlem?</span><span class="sxs-lookup"><span data-stu-id="79095-286">Why am I not see compute metadata information?</span></span>
   * <span data-ttu-id="79095-287">Eylül 2016 sonra oluşturulan tüm VM'ler için ekleme bir [etiketi](../../azure-resource-manager/resource-group-using-tags.md) görmeye başlayacaksınız için meta veri işlem.</span><span class="sxs-lookup"><span data-stu-id="79095-287">For any VMs created after Sep 2016, add a [Tag](../../azure-resource-manager/resource-group-using-tags.md) to start seeing compute metadata.</span></span> <span data-ttu-id="79095-288">(Eylül 2016 öncesinde oluşturulan) eski VM'ler için ekleme/meta verilerini yenilemek için VM uzantıları veya veri diski Kaldır.</span><span class="sxs-lookup"><span data-stu-id="79095-288">For older VMs (created before Sep 2016), add/remove extensions or data disks to the VM to refresh metadata.</span></span>
4. <span data-ttu-id="79095-289">Neden iletisi alıyorum hata `500 Internal Server Error`?</span><span class="sxs-lookup"><span data-stu-id="79095-289">Why am I getting the error `500 Internal Server Error`?</span></span>
   * <span data-ttu-id="79095-290">Lütfen üstel geri alma sistem göre isteğinizi yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="79095-290">Please retry your request based on exponential back off system.</span></span> <span data-ttu-id="79095-291">Sorun devam ederse Azure desteğine başvurun.</span><span class="sxs-lookup"><span data-stu-id="79095-291">If the issue persists contact  Azure support.</span></span>
5. <span data-ttu-id="79095-292">Burada ek soruları/açıklamalar paylaşmak?</span><span class="sxs-lookup"><span data-stu-id="79095-292">Where do I share additional questions/comments?</span></span>
   * <span data-ttu-id="79095-293">Yorumlarınızı üzerinde http://feedback.azure.com gönderin.</span><span class="sxs-lookup"><span data-stu-id="79095-293">Send your comments on http://feedback.azure.com.</span></span>
7. <span data-ttu-id="79095-294">Bu sanal makine ölçek kümesi örneği için çalışır?</span><span class="sxs-lookup"><span data-stu-id="79095-294">Would this work for Virtual Machine Scale Set Instance?</span></span>
   * <span data-ttu-id="79095-295">Evet meta veri hizmeti için ölçek kümesi örnek kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="79095-295">Yes Metadata service is available for Scale Set Instances.</span></span> 
6. <span data-ttu-id="79095-296">Hizmet için nasıl destek alma?</span><span class="sxs-lookup"><span data-stu-id="79095-296">How do I get support for the service?</span></span>
   * <span data-ttu-id="79095-297">Hizmeti için destek almak için uzun denemeden sonra meta veri yanıtı alabilir olduğunuz değil VM için Azure portalında bir destek sorununu oluşturma</span><span class="sxs-lookup"><span data-stu-id="79095-297">To get support for the service, create a support issue in Azure portal for the VM where you are not able to get metadata response after long retries</span></span> 

   ![Örnek meta verileri desteği](./media/instance-metadata-service/InstanceMetadata-support.png)
    
## <a name="next-steps"></a><span data-ttu-id="79095-299">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="79095-299">Next steps</span></span>

- <span data-ttu-id="79095-300">Daha fazla bilgi edinmek [zamanlanmış olayları](scheduled-events.md) API **genel önizlemede** örneği meta veri hizmeti tarafından sağlanan.</span><span class="sxs-lookup"><span data-stu-id="79095-300">Learn more about the [Scheduled Events](scheduled-events.md) API **in public preview** provided by the Instance Metadata service.</span></span>
