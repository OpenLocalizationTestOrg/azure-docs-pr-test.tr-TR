---
title: "aaaAzure örneği meta veri hizmetine genel bakış | Microsoft Docs"
description: "Sanal makinenin işlem, ağ ve yaklaşan Bakımı olayları hakkında rESTful arabirimi tooget bilgi."
services: virtual-machines-windows, virtual-machines-linux,virtual-machines-scale-sets, cloud-services
documentationcenter: virtual-machines
author: harijay
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure
ms.date: 03/27/2017
ms.author: harijay
ms.openlocfilehash: e87cdf28f80b9ef8cc566b637549c48846862f0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-instance-metadata-service"></a><span data-ttu-id="0c332-103">Azure örneği meta veri hizmeti</span><span class="sxs-lookup"><span data-stu-id="0c332-103">Azure Instance Metadata Service</span></span> 


<span data-ttu-id="0c332-104">Hello Azure örneği meta veri hizmeti kullanılan toomanage ve sanal makineleri yapılandırma sanal makine örneği çalıştırma hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="0c332-104">hello Azure Instance Metadata Service provides information about running virtual machine instances that can be used toomanage and configure your virtual machines.</span></span>
<span data-ttu-id="0c332-105">Bu, SKU, ağ yapılandırması ve yaklaşan Bakımı olayları gibi bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="0c332-105">This includes information such as SKU, network configuration, and upcoming maintenance events.</span></span> <span data-ttu-id="0c332-106">Hangi tür bilgileri kullanılabilir daha fazla bilgi için bkz: [meta veri kategorileri](#instance-metadata-data-categories).</span><span class="sxs-lookup"><span data-stu-id="0c332-106">For more information on what type of information is available, see [metadata categories](#instance-metadata-data-categories).</span></span>

<span data-ttu-id="0c332-107">Azure'nın örnek meta verileri hizmetidir, erişilebilir tooall Iaas Vm'leri hello oluşturulan bir REST uç [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span><span class="sxs-lookup"><span data-stu-id="0c332-107">Azure's Instance Metadata Service is a REST Endpoint accessible tooall IaaS VMs created via hello [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span></span> <span data-ttu-id="0c332-108">Merhaba uç nokta iyi bilinen yönlendirilemeyen IP adresinde mevcuttur (`169.254.169.254`), erişilebilir yalnızca VM hello içinde.</span><span class="sxs-lookup"><span data-stu-id="0c332-108">hello endpoint is available at a well-known non-routable IP address (`169.254.169.254`) that can be accessed only from within hello VM.</span></span>

### <a name="important-information"></a><span data-ttu-id="0c332-109">Önemli bilgiler</span><span class="sxs-lookup"><span data-stu-id="0c332-109">Important information</span></span>

<span data-ttu-id="0c332-110">Bu hizmet **genel olarak kullanılabilir** genel Azure bölgelerindeki.</span><span class="sxs-lookup"><span data-stu-id="0c332-110">This service is  **generally available** in Global Azure Regions.</span></span> <span data-ttu-id="0c332-111">Genel Önizleme kamu, Çin ve Almanca Azure bulutu için ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="0c332-111">It is in Public preview for Government, China, and German Azure Cloud.</span></span> <span data-ttu-id="0c332-112">Düzenli olarak, sanal makine örnekleri hakkında güncelleştirmeleri tooexpose yeni bilgi alır.</span><span class="sxs-lookup"><span data-stu-id="0c332-112">It regularly receives updates tooexpose new information about virtual machine instances.</span></span> <span data-ttu-id="0c332-113">Bu sayfayı hello güncel yansıtır [veri kategorilerini](#instance-metadata-data-categories) kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="0c332-113">This page reflects hello up-to-date [data categories](#instance-metadata-data-categories) available.</span></span>

## <a name="service-availability"></a><span data-ttu-id="0c332-114">Hizmet kullanılabilirliği</span><span class="sxs-lookup"><span data-stu-id="0c332-114">Service Availability</span></span>
<span data-ttu-id="0c332-115">Merhaba hizmeti tüm genel olarak kullanılabilir genel Azure bölgelerde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="0c332-115">hello service is available in all generally available Global Azure regions.</span></span> <span data-ttu-id="0c332-116">Merhaba hello kamu, Çin veya Almanya bölgelerde genel önizlemede hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="0c332-116">hello service is in public preview  in hello Government, China, or Germany regions.</span></span>

<span data-ttu-id="0c332-117">Bölgeler</span><span class="sxs-lookup"><span data-stu-id="0c332-117">Regions</span></span>                                        | <span data-ttu-id="0c332-118">Kullanılabilirlik?</span><span class="sxs-lookup"><span data-stu-id="0c332-118">Availability?</span></span>
-----------------------------------------------|-----------------------------------------------
[<span data-ttu-id="0c332-119">Tüm genel olarak kullanılabilir genel Azure bölgeleri</span><span class="sxs-lookup"><span data-stu-id="0c332-119">All Generally Available Global Azure Regions</span></span>](https://azure.microsoft.com/en-us/regions/)     | <span data-ttu-id="0c332-120">Genel olarak kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="0c332-120">Generally Available</span></span> 
[<span data-ttu-id="0c332-121">Azure Devlet Kurumları</span><span class="sxs-lookup"><span data-stu-id="0c332-121">Azure Government</span></span>](https://azure.microsoft.com/en-us/overview/clouds/government/)              | <span data-ttu-id="0c332-122">Önizleme</span><span class="sxs-lookup"><span data-stu-id="0c332-122">In Preview</span></span> 
[<span data-ttu-id="0c332-123">Azure Çin</span><span class="sxs-lookup"><span data-stu-id="0c332-123">Azure China</span></span>](https://www.azure.cn/)                                                           | <span data-ttu-id="0c332-124">Önizleme</span><span class="sxs-lookup"><span data-stu-id="0c332-124">In Preview</span></span>
[<span data-ttu-id="0c332-125">Azure Almanya</span><span class="sxs-lookup"><span data-stu-id="0c332-125">Azure Germany</span></span>](https://azure.microsoft.com/en-us/overview/clouds/germany/)                    | <span data-ttu-id="0c332-126">Önizleme</span><span class="sxs-lookup"><span data-stu-id="0c332-126">In Preview</span></span>

<span data-ttu-id="0c332-127">Merhaba hizmet diğer Azure bulutta kullanılabilir olduğunda bu tabloya güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="0c332-127">This table is updated when hello service becomes available in other Azure clouds.</span></span>

<span data-ttu-id="0c332-128">hello örneği meta veri hizmeti, çıkışı tootry oluşturma bir sanal makineden [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/) veya hello [Azure portal](http://portal.azure.com) bölgeler ve izleme hello örneklere yukarıda hello içinde.</span><span class="sxs-lookup"><span data-stu-id="0c332-128">tootry out hello Instance Metadata Service, create a VM from [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/) or hello [Azure portal](http://portal.azure.com) in hello above regions and follow hello examples below.</span></span>

## <a name="usage"></a><span data-ttu-id="0c332-129">Kullanım</span><span class="sxs-lookup"><span data-stu-id="0c332-129">Usage</span></span>

### <a name="versioning"></a><span data-ttu-id="0c332-130">Sürüm oluşturma</span><span class="sxs-lookup"><span data-stu-id="0c332-130">Versioning</span></span>
<span data-ttu-id="0c332-131">Merhaba örneği meta veri hizmeti sürümü tutulan ' dir.</span><span class="sxs-lookup"><span data-stu-id="0c332-131">hello Instance Metadata Service is versioned.</span></span> <span data-ttu-id="0c332-132">Sürümleri zorunludur ve hello geçerli sürümü `2017-04-02`.</span><span class="sxs-lookup"><span data-stu-id="0c332-132">Versions are mandatory and hello current version is `2017-04-02`.</span></span>

> [!NOTE] 
> <span data-ttu-id="0c332-133">Önceki Önizleme sürümleri {son} hello api sürümü desteklenen zamanlanmış olaylar.</span><span class="sxs-lookup"><span data-stu-id="0c332-133">Previous preview releases of scheduled events supported {latest} as hello api-version.</span></span> <span data-ttu-id="0c332-134">Bu biçim artık desteklenmemektedir ve hello gelecekteki kullanım dışı kalacaktır.</span><span class="sxs-lookup"><span data-stu-id="0c332-134">This format is no longer supported and will be deprecated in hello future.</span></span>

<span data-ttu-id="0c332-135">Yeni sürümler eklediğimiz gibi komut dosyalarınızı belirli veri biçimleri üzerinde bağımlılıkları varsa, daha eski sürümlerini yine de uyumluluk için erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="0c332-135">As we add newer versions, older versions can still be accessed for compatibility if your scripts have dependencies on specific data formats.</span></span> <span data-ttu-id="0c332-136">Ancak, hello hizmeti genel olarak kullanılabilir olduğunda bu hello geçerli Önizleme version(2017-03-01) kullanılamayabilir unutmayın.</span><span class="sxs-lookup"><span data-stu-id="0c332-136">However, note that hello current preview version(2017-03-01) may not be available once hello service is generally available.</span></span>

### <a name="using-headers"></a><span data-ttu-id="0c332-137">Üst bilgileri kullanma</span><span class="sxs-lookup"><span data-stu-id="0c332-137">Using Headers</span></span>
<span data-ttu-id="0c332-138">Merhaba örneği meta veri hizmeti sorguladığınızda hello üstbilgi sağlamalısınız `Metadata: true` tooensure hello talep istemeden yönlendirilmeyen.</span><span class="sxs-lookup"><span data-stu-id="0c332-138">When you query hello Instance Metadata Service, you must provide hello header `Metadata: true` tooensure hello request was not unintentionally redirected.</span></span>

### <a name="retrieving-metadata"></a><span data-ttu-id="0c332-139">Meta veri alma</span><span class="sxs-lookup"><span data-stu-id="0c332-139">Retrieving metadata</span></span>

<span data-ttu-id="0c332-140">Örnek meta verileri oluşturulan yönetilen/kullanarak sanal makineleri çalıştırmak için kullanılabilir [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span><span class="sxs-lookup"><span data-stu-id="0c332-140">Instance metadata is available for running VMs created/managed using [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span></span> <span data-ttu-id="0c332-141">İstek aşağıdaki hello kullanarak bir sanal makine örneği için tüm veri kategorilerini erişebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="0c332-141">Access all data categories for a virtual machine instance using hello following request:</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

> [!NOTE] 
> <span data-ttu-id="0c332-142">Tüm örnek meta veri sorguları büyük/küçük harfe duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="0c332-142">All instance metadata queries are case-sensitive.</span></span>

### <a name="data-output"></a><span data-ttu-id="0c332-143">Veri çıkışı</span><span class="sxs-lookup"><span data-stu-id="0c332-143">Data output</span></span>
<span data-ttu-id="0c332-144">Varsayılan olarak, JSON biçiminde hello örneği meta veri hizmeti verileri döndürür (`Content-Type: application/json`).</span><span class="sxs-lookup"><span data-stu-id="0c332-144">By default, hello Instance Metadata Service returns data in JSON format (`Content-Type: application/json`).</span></span> <span data-ttu-id="0c332-145">Ancak, farklı API'leri verileri farklı biçimlerde istediyseniz döndürebilir.</span><span class="sxs-lookup"><span data-stu-id="0c332-145">However, different APIs can return data in different formats if requested.</span></span>
<span data-ttu-id="0c332-146">Merhaba aşağıdaki tabloda bir API destekleyebilir diğer veri biçimlerinin başvurudur.</span><span class="sxs-lookup"><span data-stu-id="0c332-146">hello following table is a reference of other data formats APIs may support.</span></span>

<span data-ttu-id="0c332-147">API</span><span class="sxs-lookup"><span data-stu-id="0c332-147">API</span></span> | <span data-ttu-id="0c332-148">Varsayılan veri biçimi</span><span class="sxs-lookup"><span data-stu-id="0c332-148">Default Data Format</span></span> | <span data-ttu-id="0c332-149">Diğer biçimlere</span><span class="sxs-lookup"><span data-stu-id="0c332-149">Other Formats</span></span>
--------|---------------------|--------------
<span data-ttu-id="0c332-150">/instance</span><span class="sxs-lookup"><span data-stu-id="0c332-150">/instance</span></span> | <span data-ttu-id="0c332-151">JSON</span><span class="sxs-lookup"><span data-stu-id="0c332-151">json</span></span> | <span data-ttu-id="0c332-152">Metin</span><span class="sxs-lookup"><span data-stu-id="0c332-152">text</span></span>
<span data-ttu-id="0c332-153">/scheduledevents</span><span class="sxs-lookup"><span data-stu-id="0c332-153">/scheduledevents</span></span> | <span data-ttu-id="0c332-154">JSON</span><span class="sxs-lookup"><span data-stu-id="0c332-154">json</span></span> | <span data-ttu-id="0c332-155">Yok</span><span class="sxs-lookup"><span data-stu-id="0c332-155">none</span></span>

<span data-ttu-id="0c332-156">Varsayılan olmayan yanıt biçimi tooaccess hello isteği bir sorgu dizesi parametresi olarak hello istenen biçim belirtin.</span><span class="sxs-lookup"><span data-stu-id="0c332-156">tooaccess a non-default response format, specify hello requested format as a querystring parameter in hello request.</span></span> <span data-ttu-id="0c332-157">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="0c332-157">For example:</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02&format=text"
```

### <a name="security"></a><span data-ttu-id="0c332-158">Güvenlik</span><span class="sxs-lookup"><span data-stu-id="0c332-158">Security</span></span>
<span data-ttu-id="0c332-159">Merhaba örneği meta veri Hizmeti uç noktası yalnızca yönlendirilebilir olmayan bir IP adresi üzerinde sanal makine örneğini çalıştıran hello içinde erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="0c332-159">hello Instance Metadata Service endpoint is accessible only from within hello running virtual machine instance on a non-routable IP address.</span></span> <span data-ttu-id="0c332-160">Ayrıca, herhangi bir ile istek bir `X-Forwarded-For` üstbilgi hello hizmeti tarafından reddedildi.</span><span class="sxs-lookup"><span data-stu-id="0c332-160">In addition, any request with a `X-Forwarded-For` header is rejected by hello service.</span></span>
<span data-ttu-id="0c332-161">Biz de istekleri toocontain gerektiren bir `Metadata: true` gerçek isteği hello üstbilgi tooensure olan doğrudan istenen ve istenmeyen yeniden yönlendirme parçası değil.</span><span class="sxs-lookup"><span data-stu-id="0c332-161">We also require requests toocontain a `Metadata: true` header tooensure that hello actual request was directly intended and not a part of unintentional redirection.</span></span> 

### <a name="error"></a><span data-ttu-id="0c332-162">Hata</span><span class="sxs-lookup"><span data-stu-id="0c332-162">Error</span></span>
<span data-ttu-id="0c332-163">Bir veri öğesi bulunamadı veya hatalı biçimlendirilmiş bir istek varsa hello örneği meta veri hizmeti standart HTTP hatalarını döndürür.</span><span class="sxs-lookup"><span data-stu-id="0c332-163">If there is a data element not found or a malformed request, hello Instance Metadata Service returns standard HTTP errors.</span></span> <span data-ttu-id="0c332-164">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="0c332-164">For example:</span></span>

<span data-ttu-id="0c332-165">HTTP durum kodu</span><span class="sxs-lookup"><span data-stu-id="0c332-165">HTTP Status Code</span></span> | <span data-ttu-id="0c332-166">Neden</span><span class="sxs-lookup"><span data-stu-id="0c332-166">Reason</span></span>
----------------|-------
<span data-ttu-id="0c332-167">200 TAMAM</span><span class="sxs-lookup"><span data-stu-id="0c332-167">200 OK</span></span> |
<span data-ttu-id="0c332-168">400 Hatalı istek</span><span class="sxs-lookup"><span data-stu-id="0c332-168">400 Bad Request</span></span> | <span data-ttu-id="0c332-169">Eksik `Metadata: true` üstbilgisi</span><span class="sxs-lookup"><span data-stu-id="0c332-169">Missing `Metadata: true` header</span></span>
<span data-ttu-id="0c332-170">404 Bulunamadı</span><span class="sxs-lookup"><span data-stu-id="0c332-170">404 Not Found</span></span> | <span data-ttu-id="0c332-171">Merhaba İstenen öğe does't var</span><span class="sxs-lookup"><span data-stu-id="0c332-171">hello requested element does't exist</span></span> 
<span data-ttu-id="0c332-172">405 Yönteme izin verilmiyor</span><span class="sxs-lookup"><span data-stu-id="0c332-172">405 Method Not Allowed</span></span> | <span data-ttu-id="0c332-173">Yalnızca `GET` ve `POST` istekleri desteklenir</span><span class="sxs-lookup"><span data-stu-id="0c332-173">Only `GET` and `POST` requests are supported</span></span>
<span data-ttu-id="0c332-174">429 çok fazla istek</span><span class="sxs-lookup"><span data-stu-id="0c332-174">429 Too Many Requests</span></span> | <span data-ttu-id="0c332-175">Merhaba API şu anda en fazla saniye başına 5 sorguları destekler</span><span class="sxs-lookup"><span data-stu-id="0c332-175">hello API currently supports a maximum of 5 queries per second</span></span>
<span data-ttu-id="0c332-176">500 hizmet hatası</span><span class="sxs-lookup"><span data-stu-id="0c332-176">500 Service Error</span></span>     | <span data-ttu-id="0c332-177">Bir süre sonra yeniden deneyin</span><span class="sxs-lookup"><span data-stu-id="0c332-177">Retry after some time</span></span>

### <a name="examples"></a><span data-ttu-id="0c332-178">Örnekler</span><span class="sxs-lookup"><span data-stu-id="0c332-178">Examples</span></span>

> [!NOTE] 
> <span data-ttu-id="0c332-179">Tüm API yanıtları JSON dizelerdir.</span><span class="sxs-lookup"><span data-stu-id="0c332-179">All API responses are JSON strings.</span></span> <span data-ttu-id="0c332-180">Okunabilirlik için pretty yazdırılan tüm aşağıdaki örnek yanıtlar.</span><span class="sxs-lookup"><span data-stu-id="0c332-180">All following example responses  are pretty-printed for readability.</span></span>

#### <a name="retrieving-network-information"></a><span data-ttu-id="0c332-181">Ağ bilgileri alınıyor</span><span class="sxs-lookup"><span data-stu-id="0c332-181">Retrieving network information</span></span>

<span data-ttu-id="0c332-182">**İstek**</span><span class="sxs-lookup"><span data-stu-id="0c332-182">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network?api-version=2017-04-02"
```

<span data-ttu-id="0c332-183">**Yanıt**</span><span class="sxs-lookup"><span data-stu-id="0c332-183">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="0c332-184">Merhaba yanıt bir JSON dizesidir.</span><span class="sxs-lookup"><span data-stu-id="0c332-184">hello response is a JSON string.</span></span> <span data-ttu-id="0c332-185">Aşağıdaki örnek yanıt hello okunabilirlik için pretty yazdırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="0c332-185">hello following example response is pretty-printed for readability.</span></span>

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

#### <a name="retrieving-public-ip-address"></a><span data-ttu-id="0c332-186">Genel IP adresi alınıyor</span><span class="sxs-lookup"><span data-stu-id="0c332-186">Retrieving public IP address</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network/interface/0/ipv4/ipAddress/0/publicIpAddress?api-version=2017-04-02&format=text"
```

#### <a name="retrieving-all-metadata-for-an-instance"></a><span data-ttu-id="0c332-187">Bir örneği için tüm meta veri alma</span><span class="sxs-lookup"><span data-stu-id="0c332-187">Retrieving all metadata for an instance</span></span>

<span data-ttu-id="0c332-188">**İstek**</span><span class="sxs-lookup"><span data-stu-id="0c332-188">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

<span data-ttu-id="0c332-189">**Yanıt**</span><span class="sxs-lookup"><span data-stu-id="0c332-189">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="0c332-190">Merhaba yanıt bir JSON dizesidir.</span><span class="sxs-lookup"><span data-stu-id="0c332-190">hello response is a JSON string.</span></span> <span data-ttu-id="0c332-191">Aşağıdaki örnek yanıt hello okunabilirlik için pretty yazdırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="0c332-191">hello following example response is pretty-printed for readability.</span></span>

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

#### <a name="retrieving-metadata-in-windows-virtual-machine"></a><span data-ttu-id="0c332-192">Meta veriler de Windows sanal makinesi alınıyor</span><span class="sxs-lookup"><span data-stu-id="0c332-192">Retrieving metadata in Windows Virtual Machine</span></span>

<span data-ttu-id="0c332-193">**İstek**</span><span class="sxs-lookup"><span data-stu-id="0c332-193">**Request**</span></span>

<span data-ttu-id="0c332-194">Örnek meta verileri alınabilir Windows hello PowerShell yardımcı programı `curl`:</span><span class="sxs-lookup"><span data-stu-id="0c332-194">Instance metadata can be retrieved in Windows via hello PowerShell utility `curl`:</span></span> 

```
curl -H @{'Metadata'='true'} http://169.254.169.254/metadata/instance?api-version=2017-04-02 | select -ExpandProperty Content
```

<span data-ttu-id="0c332-195">Merhaba aracılığıyla veya `Invoke-RestMethod` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="0c332-195">Or through hello `Invoke-RestMethod` cmdlet:</span></span>
    
```
Invoke-RestMethod -Headers @{"Metadata"="true"} -URI http://169.254.169.254/metadata/instance?api-version=2017-04-02 -Method get 
```

<span data-ttu-id="0c332-196">**Yanıt**</span><span class="sxs-lookup"><span data-stu-id="0c332-196">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="0c332-197">Merhaba yanıt bir JSON dizesidir.</span><span class="sxs-lookup"><span data-stu-id="0c332-197">hello response is a JSON string.</span></span> <span data-ttu-id="0c332-198">Aşağıdaki örnek yanıt hello okunabilirlik için pretty yazdırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="0c332-198">hello following example response  is pretty-printed for readability.</span></span>

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

## <a name="instance-metadata-data-categories"></a><span data-ttu-id="0c332-199">Örnek meta veri kategorileri</span><span class="sxs-lookup"><span data-stu-id="0c332-199">Instance metadata data categories</span></span>
<span data-ttu-id="0c332-200">Veri kategorilerini aşağıdaki hello hello örneği meta veri hizmeti kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="0c332-200">hello following data categories are available through hello Instance Metadata Service:</span></span>

<span data-ttu-id="0c332-201">Veriler</span><span class="sxs-lookup"><span data-stu-id="0c332-201">Data</span></span> | <span data-ttu-id="0c332-202">Açıklama</span><span class="sxs-lookup"><span data-stu-id="0c332-202">Description</span></span>
-----|------------
<span data-ttu-id="0c332-203">location</span><span class="sxs-lookup"><span data-stu-id="0c332-203">location</span></span> | <span data-ttu-id="0c332-204">Azure bölgesi hello VM çalışıyor</span><span class="sxs-lookup"><span data-stu-id="0c332-204">Azure Region hello VM is running in</span></span>
<span data-ttu-id="0c332-205">ad</span><span class="sxs-lookup"><span data-stu-id="0c332-205">name</span></span> | <span data-ttu-id="0c332-206">Merhaba VM adı</span><span class="sxs-lookup"><span data-stu-id="0c332-206">Name of hello VM</span></span> 
<span data-ttu-id="0c332-207">Teklif</span><span class="sxs-lookup"><span data-stu-id="0c332-207">offer</span></span> | <span data-ttu-id="0c332-208">Merhaba VM görüntüsü için bilgi sunar.</span><span class="sxs-lookup"><span data-stu-id="0c332-208">Offer information for hello VM image.</span></span> <span data-ttu-id="0c332-209">Bu değer yalnızca Azure resmi Galerisi'nden dağıtılan görüntüleri için mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="0c332-209">This value is only present for images deployed from Azure image gallery.</span></span>
<span data-ttu-id="0c332-210">Yayımcı</span><span class="sxs-lookup"><span data-stu-id="0c332-210">publisher</span></span> | <span data-ttu-id="0c332-211">Merhaba VM görüntüsü yayımcısı</span><span class="sxs-lookup"><span data-stu-id="0c332-211">Publisher of hello VM image</span></span>
<span data-ttu-id="0c332-212">SKU</span><span class="sxs-lookup"><span data-stu-id="0c332-212">sku</span></span> | <span data-ttu-id="0c332-213">Belirli SKU hello VM görüntüsü için</span><span class="sxs-lookup"><span data-stu-id="0c332-213">Specific SKU for hello VM image</span></span>  
<span data-ttu-id="0c332-214">Sürüm</span><span class="sxs-lookup"><span data-stu-id="0c332-214">version</span></span> | <span data-ttu-id="0c332-215">Merhaba VM görüntüsü</span><span class="sxs-lookup"><span data-stu-id="0c332-215">Version of hello VM image</span></span> 
<span data-ttu-id="0c332-216">osType</span><span class="sxs-lookup"><span data-stu-id="0c332-216">osType</span></span> | <span data-ttu-id="0c332-217">Linux veya Windows</span><span class="sxs-lookup"><span data-stu-id="0c332-217">Linux or Windows</span></span> 
<span data-ttu-id="0c332-218">platformUpdateDomain</span><span class="sxs-lookup"><span data-stu-id="0c332-218">platformUpdateDomain</span></span> |  <span data-ttu-id="0c332-219">[Güncelleştirme etki alanı](virtual-machines-windows-manage-availability.md) hello VM çalışır</span><span class="sxs-lookup"><span data-stu-id="0c332-219">[Update domain](virtual-machines-windows-manage-availability.md) hello VM is running in</span></span>
<span data-ttu-id="0c332-220">platformFaultDomain</span><span class="sxs-lookup"><span data-stu-id="0c332-220">platformFaultDomain</span></span> | <span data-ttu-id="0c332-221">[Hata etki alanı](virtual-machines-windows-manage-availability.md) hello VM çalışır</span><span class="sxs-lookup"><span data-stu-id="0c332-221">[Fault domain](virtual-machines-windows-manage-availability.md) hello VM is running in</span></span>
<span data-ttu-id="0c332-222">Bunun nedeni</span><span class="sxs-lookup"><span data-stu-id="0c332-222">vmId</span></span> | <span data-ttu-id="0c332-223">[Benzersiz tanımlayıcı](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/) hello VM için</span><span class="sxs-lookup"><span data-stu-id="0c332-223">[Unique identifier](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/) for hello VM</span></span>
<span data-ttu-id="0c332-224">vmSize</span><span class="sxs-lookup"><span data-stu-id="0c332-224">vmSize</span></span> | [<span data-ttu-id="0c332-225">VM boyutu</span><span class="sxs-lookup"><span data-stu-id="0c332-225">VM size</span></span>](virtual-machines-windows-sizes.md)
<span data-ttu-id="0c332-226">IPv4/privateIpAddress</span><span class="sxs-lookup"><span data-stu-id="0c332-226">ipv4/privateIpAddress</span></span> | <span data-ttu-id="0c332-227">Merhaba VM yerel IPv4 adresi</span><span class="sxs-lookup"><span data-stu-id="0c332-227">Local IPv4 address of hello VM</span></span> 
<span data-ttu-id="0c332-228">IPv4/Publicıpaddress</span><span class="sxs-lookup"><span data-stu-id="0c332-228">ipv4/publicIpAddress</span></span> | <span data-ttu-id="0c332-229">Merhaba VM genel IPv4 adresi</span><span class="sxs-lookup"><span data-stu-id="0c332-229">Public IPv4 address of hello VM</span></span>
<span data-ttu-id="0c332-230">alt ağ/adresi</span><span class="sxs-lookup"><span data-stu-id="0c332-230">subnet/address</span></span> | <span data-ttu-id="0c332-231">Merhaba VM alt ağ adresi</span><span class="sxs-lookup"><span data-stu-id="0c332-231">Subnet address of hello VM</span></span>
<span data-ttu-id="0c332-232">alt ağ/öneki</span><span class="sxs-lookup"><span data-stu-id="0c332-232">subnet/prefix</span></span> | <span data-ttu-id="0c332-233">Alt ağ öneki, örnek 24</span><span class="sxs-lookup"><span data-stu-id="0c332-233">Subnet prefix, example 24</span></span>
<span data-ttu-id="0c332-234">IPv6/IPADDRESS</span><span class="sxs-lookup"><span data-stu-id="0c332-234">ipv6/ipAddress</span></span> | <span data-ttu-id="0c332-235">Merhaba VM yerel IPv6 adresi</span><span class="sxs-lookup"><span data-stu-id="0c332-235">Local IPv6 address of hello VM</span></span>
<span data-ttu-id="0c332-236">MacAddress</span><span class="sxs-lookup"><span data-stu-id="0c332-236">macAddress</span></span> | <span data-ttu-id="0c332-237">VM mac adresi</span><span class="sxs-lookup"><span data-stu-id="0c332-237">VM mac address</span></span> 
<span data-ttu-id="0c332-238">scheduledevents</span><span class="sxs-lookup"><span data-stu-id="0c332-238">scheduledevents</span></span> | <span data-ttu-id="0c332-239">Genel önizlemesini görmek, şu anda [scheduledevents](virtual-machines-scheduled-events.md)</span><span class="sxs-lookup"><span data-stu-id="0c332-239">Currently in Public Preview See [scheduledevents](virtual-machines-scheduled-events.md)</span></span>

## <a name="example-scenarios-for-usage"></a><span data-ttu-id="0c332-240">Kullanım için örnek senaryolar</span><span class="sxs-lookup"><span data-stu-id="0c332-240">Example Scenarios for usage</span></span>  

### <a name="tracking-vm-running-on-azure"></a><span data-ttu-id="0c332-241">Azure üzerinde çalışan VM izleme</span><span class="sxs-lookup"><span data-stu-id="0c332-241">Tracking VM running on Azure</span></span>

<span data-ttu-id="0c332-242">Bir hizmet sağlayıcısı olarak tootrack hello yazılımınızı çalışan VM sayısı gerektirebilir veya hello VM tootrack benzersizliğini gereksinim aracılara sahip.</span><span class="sxs-lookup"><span data-stu-id="0c332-242">As a service provider, you may require tootrack hello number of VMs running your software or have agents that need tootrack uniqueness of hello VM.</span></span> <span data-ttu-id="0c332-243">toobe mümkün tooget benzersiz bir kimlik kullanmak hello bir VM için `vmId` örneği meta veri hizmetinden alan.</span><span class="sxs-lookup"><span data-stu-id="0c332-243">toobe able tooget a unique ID for a VM, use hello `vmId` field from Instance Metadata Service.</span></span>

<span data-ttu-id="0c332-244">**İstek**</span><span class="sxs-lookup"><span data-stu-id="0c332-244">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/vmId?api-version=2017-04-02&format=text"
```

<span data-ttu-id="0c332-245">**Yanıt**</span><span class="sxs-lookup"><span data-stu-id="0c332-245">**Response**</span></span>

```
5c08b38e-4d57-4c23-ac45-aca61037f084
```

### <a name="placement-of-containers-data-partitions-based-faultupdate-domain"></a><span data-ttu-id="0c332-246">Yerleştirme kapsayıcıların veri bölümlerini arıza/güncelleştirme etki alanı tabanlı</span><span class="sxs-lookup"><span data-stu-id="0c332-246">Placement of containers, data-partitions based Fault/Update domain</span></span> 

<span data-ttu-id="0c332-247">Belirli senaryolar, farklı veri çoğaltmaları yerleşimini prime çok önemlidir.</span><span class="sxs-lookup"><span data-stu-id="0c332-247">For certain scenarios, placement of different data replicas is of prime importance.</span></span> <span data-ttu-id="0c332-248">Örneğin, [HDFS çoğaltma yerleştirme](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html#Replica_Placement:_The_First_Baby_Steps) veya kapsayıcı yerleştirme aracılığıyla bir [orchestrator](https://kubernetes.io/docs/user-guide/node-selection/) tooknow hello gerektirebilir `platformFaultDomain` ve `platformUpdateDomain` VM üzerinde çalışan hello.</span><span class="sxs-lookup"><span data-stu-id="0c332-248">For example, [HDFS replica placement](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html#Replica_Placement:_The_First_Baby_Steps) or container placement via an [orchestrator](https://kubernetes.io/docs/user-guide/node-selection/) may you require tooknow hello `platformFaultDomain` and `platformUpdateDomain` hello VM is running on.</span></span>
<span data-ttu-id="0c332-249">Bu verileri hello örneği meta veri hizmeti aracılığıyla doğrudan sorgulayabilir.</span><span class="sxs-lookup"><span data-stu-id="0c332-249">You can query this data directly via hello Instance Metadata Service.</span></span>

<span data-ttu-id="0c332-250">**İstek**</span><span class="sxs-lookup"><span data-stu-id="0c332-250">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/platformFaultDomain?api-version=2017-04-02&format=text" 
```

<span data-ttu-id="0c332-251">**Yanıt**</span><span class="sxs-lookup"><span data-stu-id="0c332-251">**Response**</span></span>

```
0
```

### <a name="getting-more-information-about-hello-vm-during-support-case"></a><span data-ttu-id="0c332-252">Destek olayı sırasında hello VM hakkında daha fazla bilgi alma</span><span class="sxs-lookup"><span data-stu-id="0c332-252">Getting more information about hello VM during support case</span></span> 

<span data-ttu-id="0c332-253">Bir hizmet sağlayıcısı olarak hello VM hakkında daha fazla bilgi bir destek çağrısı tooknow oluşturulacağı yeri alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0c332-253">As a service provider, you may get a support call where you would like tooknow more information about hello VM.</span></span> <span data-ttu-id="0c332-254">Merhaba müşteri tooshare soran hello işlem meta verileri VM hello tür hakkında temel bilgiler hello destek profesyonel tooknow için Azure üzerinde sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="0c332-254">Asking hello customer tooshare hello compute metadata can provide basic information for hello support professional tooknow about hello kind of VM on Azure.</span></span> 

<span data-ttu-id="0c332-255">**İstek**</span><span class="sxs-lookup"><span data-stu-id="0c332-255">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute?api-version=2017-04-02"
```

<span data-ttu-id="0c332-256">**Yanıt**</span><span class="sxs-lookup"><span data-stu-id="0c332-256">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="0c332-257">Merhaba yanıt bir JSON dizesidir.</span><span class="sxs-lookup"><span data-stu-id="0c332-257">hello response is a JSON string.</span></span> <span data-ttu-id="0c332-258">Aşağıdaki örnek yanıt hello okunabilirlik için pretty yazdırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="0c332-258">hello following example response is pretty-printed for readability.</span></span>

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

### <a name="examples-of-calling-metadata-service-using-different-languages-inside-hello-vm"></a><span data-ttu-id="0c332-259">Farklı diller hello VM içinde kullanarak meta veri hizmeti çağrılırken örnekleri</span><span class="sxs-lookup"><span data-stu-id="0c332-259">Examples of calling metadata service using different languages inside hello VM</span></span> 

<span data-ttu-id="0c332-260">Dil</span><span class="sxs-lookup"><span data-stu-id="0c332-260">Language</span></span> | <span data-ttu-id="0c332-261">Örnek</span><span class="sxs-lookup"><span data-stu-id="0c332-261">Example</span></span> 
---------|----------------
<span data-ttu-id="0c332-262">Ruby</span><span class="sxs-lookup"><span data-stu-id="0c332-262">Ruby</span></span>     | <span data-ttu-id="0c332-263">https://github.com/Microsoft/azureimds/BLOB/master/IMDSSample.RB</span><span class="sxs-lookup"><span data-stu-id="0c332-263">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.rb</span></span>
<span data-ttu-id="0c332-264">LAN gidin</span><span class="sxs-lookup"><span data-stu-id="0c332-264">Go Lan</span></span>   | <span data-ttu-id="0c332-265">https://github.com/Microsoft/azureimds/BLOB/master/imdssample.go</span><span class="sxs-lookup"><span data-stu-id="0c332-265">https://github.com/Microsoft/azureimds/blob/master/imdssample.go</span></span>            
<span data-ttu-id="0c332-266">python</span><span class="sxs-lookup"><span data-stu-id="0c332-266">python</span></span>   | <span data-ttu-id="0c332-267">https://github.com/Microsoft/azureimds/BLOB/master/IMDSSample.PY</span><span class="sxs-lookup"><span data-stu-id="0c332-267">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.py</span></span>
<span data-ttu-id="0c332-268">C++</span><span class="sxs-lookup"><span data-stu-id="0c332-268">C++</span></span>      | <span data-ttu-id="0c332-269">https://github.com/Microsoft/azureimds/BLOB/master/IMDSSample-Windows.cpp</span><span class="sxs-lookup"><span data-stu-id="0c332-269">https://github.com/Microsoft/azureimds/blob/master/IMDSSample-windows.cpp</span></span>
<span data-ttu-id="0c332-270">C#</span><span class="sxs-lookup"><span data-stu-id="0c332-270">C#</span></span>       | <span data-ttu-id="0c332-271">https://github.com/Microsoft/azureimds/BLOB/master/IMDSSample.cs</span><span class="sxs-lookup"><span data-stu-id="0c332-271">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.cs</span></span>
<span data-ttu-id="0c332-272">Javascript</span><span class="sxs-lookup"><span data-stu-id="0c332-272">Javascript</span></span> | <span data-ttu-id="0c332-273">https://github.com/Microsoft/azureimds/BLOB/master/IMDSSample.js</span><span class="sxs-lookup"><span data-stu-id="0c332-273">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.js</span></span>
<span data-ttu-id="0c332-274">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0c332-274">Powershell</span></span> | <span data-ttu-id="0c332-275">https://github.com/Microsoft/azureimds/BLOB/master/IMDSSample.ps1</span><span class="sxs-lookup"><span data-stu-id="0c332-275">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.ps1</span></span>
<span data-ttu-id="0c332-276">Bash</span><span class="sxs-lookup"><span data-stu-id="0c332-276">Bash</span></span>       | <span data-ttu-id="0c332-277">https://github.com/Microsoft/azureimds/BLOB/master/IMDSSample.sh</span><span class="sxs-lookup"><span data-stu-id="0c332-277">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.sh</span></span>
    

## <a name="faq"></a><span data-ttu-id="0c332-278">SSS</span><span class="sxs-lookup"><span data-stu-id="0c332-278">FAQ</span></span>
1. <span data-ttu-id="0c332-279">Merhaba hata alıyorum `400 Bad Request, Required metadata header not specified`.</span><span class="sxs-lookup"><span data-stu-id="0c332-279">I am getting hello error `400 Bad Request, Required metadata header not specified`.</span></span> <span data-ttu-id="0c332-280">Bu ne anlama geliyor?</span><span class="sxs-lookup"><span data-stu-id="0c332-280">What does this mean?</span></span>
   * <span data-ttu-id="0c332-281">Hello örneği meta veri hizmeti gerektirir hello üstbilgi `Metadata: true` toobe hello istekte geçirildi.</span><span class="sxs-lookup"><span data-stu-id="0c332-281">hello Instance Metadata Service requires hello header `Metadata: true` toobe passed in hello request.</span></span> <span data-ttu-id="0c332-282">Bu üst hello REST çağrısı erişim toohello örneği meta veri hizmeti sağlar.</span><span class="sxs-lookup"><span data-stu-id="0c332-282">Passing this header in hello REST call allows access toohello Instance Metadata Service.</span></span> 
2. <span data-ttu-id="0c332-283">Neden VM'im için işlem bilgi alıyorum değil mi?</span><span class="sxs-lookup"><span data-stu-id="0c332-283">Why am I not getting compute information for my VM?</span></span>
   * <span data-ttu-id="0c332-284">Şu anda hello örneği meta veri hizmeti, yalnızca Azure Kaynak Yöneticisi ile oluşturulan örnekleri destekler.</span><span class="sxs-lookup"><span data-stu-id="0c332-284">Currently hello Instance Metadata Service only supports instances created with Azure Resource Manager.</span></span> <span data-ttu-id="0c332-285">Hello gelecekteki, biz bulut hizmeti VM'ler için destek ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0c332-285">In hello future, we may add support for Cloud Service VMs.</span></span>
3. <span data-ttu-id="0c332-286">Sanal Makinem Azure Resource Manager aracılığıyla geri bir süre oluşturdum.</span><span class="sxs-lookup"><span data-stu-id="0c332-286">I created my Virtual Machine through Azure Resource Manager a while back.</span></span> <span data-ttu-id="0c332-287">Bkz: değil neden ben meta veri bilgileri işlem?</span><span class="sxs-lookup"><span data-stu-id="0c332-287">Why am I not see compute metadata information?</span></span>
   * <span data-ttu-id="0c332-288">Eylül 2016 sonra oluşturulan tüm VM'ler için ekleme bir [etiketi](../azure-resource-manager/resource-group-using-tags.md) toostart görme işlem meta verileri.</span><span class="sxs-lookup"><span data-stu-id="0c332-288">For any VMs created after Sep 2016, add a [Tag](../azure-resource-manager/resource-group-using-tags.md) toostart seeing compute metadata.</span></span> <span data-ttu-id="0c332-289">(Eylül 2016 öncesinde oluşturulan) eski VM'ler için ekleme/uzantıları veya veri diskleri toohello VM toorefresh meta verileri kaldır.</span><span class="sxs-lookup"><span data-stu-id="0c332-289">For older VMs (created before Sep 2016), add/remove extensions or data disks toohello VM toorefresh metadata.</span></span>
4. <span data-ttu-id="0c332-290">Neden iletisi alıyorum hello hata `500 Internal Server Error`?</span><span class="sxs-lookup"><span data-stu-id="0c332-290">Why am I getting hello error `500 Internal Server Error`?</span></span>
   * <span data-ttu-id="0c332-291">Lütfen üstel geri alma sistem göre isteğinizi yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="0c332-291">Please retry your request based on exponential back off system.</span></span> <span data-ttu-id="0c332-292">Merhaba sorun devam ederse Azure desteğine başvurun.</span><span class="sxs-lookup"><span data-stu-id="0c332-292">If hello issue persists contact  Azure support.</span></span>
5. <span data-ttu-id="0c332-293">Burada ek soruları/açıklamalar paylaşmak?</span><span class="sxs-lookup"><span data-stu-id="0c332-293">Where do I share additional questions/comments?</span></span>
   * <span data-ttu-id="0c332-294">Yorumlarınızı üzerinde http://feedback.azure.com gönderin.</span><span class="sxs-lookup"><span data-stu-id="0c332-294">Send your comments on http://feedback.azure.com.</span></span>
7. <span data-ttu-id="0c332-295">Bu sanal makine ölçek kümesi örneği için çalışır?</span><span class="sxs-lookup"><span data-stu-id="0c332-295">Would this work for Virtual Machine Scale Set Instance?</span></span>
   * <span data-ttu-id="0c332-296">Evet meta veri hizmeti için ölçek kümesi örnek kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="0c332-296">Yes Metadata service is available for Scale Set Instances.</span></span> 
6. <span data-ttu-id="0c332-297">Merhaba hizmeti için destek nasıl sağlarım?</span><span class="sxs-lookup"><span data-stu-id="0c332-297">How do I get support for hello service?</span></span>
   * <span data-ttu-id="0c332-298">hello hizmet tooget desteği hello değil mümkün tooget meta veri yanıtı uzun denemeden sonra olduğunuz VM için Azure portalında bir destek sorununu oluşturma</span><span class="sxs-lookup"><span data-stu-id="0c332-298">tooget support for hello service, create a support issue in Azure portal for hello VM where you are not able tooget metadata response after long retries</span></span> 

   ![Örnek meta verileri desteği](./media/virtual-machines-instancemetadataservice-overview/InstanceMetadata-support.png)
    
## <a name="next-steps"></a><span data-ttu-id="0c332-300">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="0c332-300">Next Steps</span></span>

- <span data-ttu-id="0c332-301">Merhaba hakkında daha fazla bilgi [scheduledevents](virtual-machines-scheduled-events.md) API **içinde genel Önizleme** hello örneği meta veri hizmeti tarafından sağlanan.</span><span class="sxs-lookup"><span data-stu-id="0c332-301">Learn more about hello [scheduledevents](virtual-machines-scheduled-events.md) API **In Public Preview** provided by hello Instance Metadata Service.</span></span>
