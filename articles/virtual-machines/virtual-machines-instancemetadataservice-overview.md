---
title: "Azure örneği meta veri hizmeti'ne genel bakış | Microsoft Docs"
description: "Sanal makinenin işlem, ağ ve yaklaşan Bakımı olaylar hakkında bilgi almak için rESTful arabirimi."
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
ms.openlocfilehash: d601d8fdb92bf2d3253ba99cdeee10e09591689c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-instance-metadata-service"></a><span data-ttu-id="a6f73-103">Azure örneği meta veri hizmeti</span><span class="sxs-lookup"><span data-stu-id="a6f73-103">Azure Instance Metadata Service</span></span> 


<span data-ttu-id="a6f73-104">Azure örneği meta veri hizmeti yönetmek ve sanal makinelerinizi yapılandırmak için kullanılan sanal makine örneği çalıştırma hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="a6f73-104">The Azure Instance Metadata Service provides information about running virtual machine instances that can be used to manage and configure your virtual machines.</span></span>
<span data-ttu-id="a6f73-105">Bu, SKU, ağ yapılandırması ve yaklaşan Bakımı olayları gibi bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="a6f73-105">This includes information such as SKU, network configuration, and upcoming maintenance events.</span></span> <span data-ttu-id="a6f73-106">Hangi tür bilgileri kullanılabilir daha fazla bilgi için bkz: [meta veri kategorileri](#instance-metadata-data-categories).</span><span class="sxs-lookup"><span data-stu-id="a6f73-106">For more information on what type of information is available, see [metadata categories](#instance-metadata-data-categories).</span></span>

<span data-ttu-id="a6f73-107">Azure'nın örnek meta veri hizmeti REST uç noktası aracılığıyla oluşturulan tüm Iaas VM'ler için erişilebilir olan [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span><span class="sxs-lookup"><span data-stu-id="a6f73-107">Azure's Instance Metadata Service is a REST Endpoint accessible to all IaaS VMs created via the [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span></span> <span data-ttu-id="a6f73-108">Uç nokta iyi bilinen yönlendirilemeyen IP adresinde mevcuttur (`169.254.169.254`), erişilebilir yalnızca VM dahilinde.</span><span class="sxs-lookup"><span data-stu-id="a6f73-108">The endpoint is available at a well-known non-routable IP address (`169.254.169.254`) that can be accessed only from within the VM.</span></span>

### <a name="important-information"></a><span data-ttu-id="a6f73-109">Önemli bilgiler</span><span class="sxs-lookup"><span data-stu-id="a6f73-109">Important information</span></span>

<span data-ttu-id="a6f73-110">Bu hizmet **genel olarak kullanılabilir** genel Azure bölgelerindeki.</span><span class="sxs-lookup"><span data-stu-id="a6f73-110">This service is  **generally available** in Global Azure Regions.</span></span> <span data-ttu-id="a6f73-111">Genel Önizleme kamu, Çin ve Almanca Azure bulutu için ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="a6f73-111">It is in Public preview for Government, China, and German Azure Cloud.</span></span> <span data-ttu-id="a6f73-112">Düzenli olarak, sanal makine örnekleri ilgili yeni bilgiler kullanıma sunmak için güncelleştirmeleri alır.</span><span class="sxs-lookup"><span data-stu-id="a6f73-112">It regularly receives updates to expose new information about virtual machine instances.</span></span> <span data-ttu-id="a6f73-113">Bu sayfayı güncel yansıtır [veri kategorilerini](#instance-metadata-data-categories) kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="a6f73-113">This page reflects the up-to-date [data categories](#instance-metadata-data-categories) available.</span></span>

## <a name="service-availability"></a><span data-ttu-id="a6f73-114">Hizmet kullanılabilirliği</span><span class="sxs-lookup"><span data-stu-id="a6f73-114">Service Availability</span></span>
<span data-ttu-id="a6f73-115">Hizmeti genel olarak kullanılabilir tüm genel Azure bölgelerde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="a6f73-115">The service is available in all generally available Global Azure regions.</span></span> <span data-ttu-id="a6f73-116">Kamu, Çin veya Almanya bölgelerde genel önizlemede hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="a6f73-116">The service is in public preview  in the Government, China, or Germany regions.</span></span>

<span data-ttu-id="a6f73-117">Bölgeler</span><span class="sxs-lookup"><span data-stu-id="a6f73-117">Regions</span></span>                                        | <span data-ttu-id="a6f73-118">Kullanılabilirlik?</span><span class="sxs-lookup"><span data-stu-id="a6f73-118">Availability?</span></span>
-----------------------------------------------|-----------------------------------------------
[<span data-ttu-id="a6f73-119">Tüm genel olarak kullanılabilir genel Azure bölgeleri</span><span class="sxs-lookup"><span data-stu-id="a6f73-119">All Generally Available Global Azure Regions</span></span>](https://azure.microsoft.com/en-us/regions/)     | <span data-ttu-id="a6f73-120">Genel olarak kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="a6f73-120">Generally Available</span></span> 
[<span data-ttu-id="a6f73-121">Azure Devlet Kurumları</span><span class="sxs-lookup"><span data-stu-id="a6f73-121">Azure Government</span></span>](https://azure.microsoft.com/en-us/overview/clouds/government/)              | <span data-ttu-id="a6f73-122">Önizleme</span><span class="sxs-lookup"><span data-stu-id="a6f73-122">In Preview</span></span> 
[<span data-ttu-id="a6f73-123">Azure Çin</span><span class="sxs-lookup"><span data-stu-id="a6f73-123">Azure China</span></span>](https://www.azure.cn/)                                                           | <span data-ttu-id="a6f73-124">Önizleme</span><span class="sxs-lookup"><span data-stu-id="a6f73-124">In Preview</span></span>
[<span data-ttu-id="a6f73-125">Azure Almanya</span><span class="sxs-lookup"><span data-stu-id="a6f73-125">Azure Germany</span></span>](https://azure.microsoft.com/en-us/overview/clouds/germany/)                    | <span data-ttu-id="a6f73-126">Önizleme</span><span class="sxs-lookup"><span data-stu-id="a6f73-126">In Preview</span></span>

<span data-ttu-id="a6f73-127">Hizmet diğer Azure bulutta kullanılabilir olduğunda bu tabloya güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="a6f73-127">This table is updated when the service becomes available in other Azure clouds.</span></span>

<span data-ttu-id="a6f73-128">Örneği meta veri hizmeti denemek için bir VM'den oluşturmak [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/) veya [Azure portal](http://portal.azure.com) yukarıdaki bölgelerde ve aşağıdaki örnekleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="a6f73-128">To try out the Instance Metadata Service, create a VM from [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/) or the [Azure portal](http://portal.azure.com) in the above regions and follow the examples below.</span></span>

## <a name="usage"></a><span data-ttu-id="a6f73-129">Kullanım</span><span class="sxs-lookup"><span data-stu-id="a6f73-129">Usage</span></span>

### <a name="versioning"></a><span data-ttu-id="a6f73-130">Sürüm oluşturma</span><span class="sxs-lookup"><span data-stu-id="a6f73-130">Versioning</span></span>
<span data-ttu-id="a6f73-131">Örnek meta veri sürümü tutulan hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="a6f73-131">The Instance Metadata Service is versioned.</span></span> <span data-ttu-id="a6f73-132">Sürümleri zorunludur ve geçerli sürümü `2017-04-02`.</span><span class="sxs-lookup"><span data-stu-id="a6f73-132">Versions are mandatory and the current version is `2017-04-02`.</span></span>

> [!NOTE] 
> <span data-ttu-id="a6f73-133">Önceki Önizleme sürümleri {son} API sürümü desteklenen zamanlanmış olaylar.</span><span class="sxs-lookup"><span data-stu-id="a6f73-133">Previous preview releases of scheduled events supported {latest} as the api-version.</span></span> <span data-ttu-id="a6f73-134">Bu biçim artık desteklenmemektedir ve gelecekte kullanım dışı kalacaktır.</span><span class="sxs-lookup"><span data-stu-id="a6f73-134">This format is no longer supported and will be deprecated in the future.</span></span>

<span data-ttu-id="a6f73-135">Yeni sürümler eklediğimiz gibi komut dosyalarınızı belirli veri biçimleri üzerinde bağımlılıkları varsa, daha eski sürümlerini yine de uyumluluk için erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="a6f73-135">As we add newer versions, older versions can still be accessed for compatibility if your scripts have dependencies on specific data formats.</span></span> <span data-ttu-id="a6f73-136">Ancak, hizmetin genel olarak kullanılabilir olduğunda geçerli Önizleme version(2017-03-01) kullanılamayabilir olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="a6f73-136">However, note that the current preview version(2017-03-01) may not be available once the service is generally available.</span></span>

### <a name="using-headers"></a><span data-ttu-id="a6f73-137">Üst bilgileri kullanma</span><span class="sxs-lookup"><span data-stu-id="a6f73-137">Using Headers</span></span>
<span data-ttu-id="a6f73-138">Örnek meta veri hizmeti sorguladığınızda başlık sağlamalısınız `Metadata: true` istek istemeden yönlendirilmeyen emin olmak için.</span><span class="sxs-lookup"><span data-stu-id="a6f73-138">When you query the Instance Metadata Service, you must provide the header `Metadata: true` to ensure the request was not unintentionally redirected.</span></span>

### <a name="retrieving-metadata"></a><span data-ttu-id="a6f73-139">Meta veri alma</span><span class="sxs-lookup"><span data-stu-id="a6f73-139">Retrieving metadata</span></span>

<span data-ttu-id="a6f73-140">Örnek meta verileri oluşturulan yönetilen/kullanarak sanal makineleri çalıştırmak için kullanılabilir [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span><span class="sxs-lookup"><span data-stu-id="a6f73-140">Instance metadata is available for running VMs created/managed using [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span></span> <span data-ttu-id="a6f73-141">Aşağıdaki isteği kullanarak bir sanal makine örneği için tüm veri kategorilerini erişebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a6f73-141">Access all data categories for a virtual machine instance using the following request:</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

> [!NOTE] 
> <span data-ttu-id="a6f73-142">Tüm örnek meta veri sorguları büyük/küçük harfe duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="a6f73-142">All instance metadata queries are case-sensitive.</span></span>

### <a name="data-output"></a><span data-ttu-id="a6f73-143">Veri çıkışı</span><span class="sxs-lookup"><span data-stu-id="a6f73-143">Data output</span></span>
<span data-ttu-id="a6f73-144">Varsayılan olarak, örnek meta veri hizmeti verileri JSON biçiminde döndürür (`Content-Type: application/json`).</span><span class="sxs-lookup"><span data-stu-id="a6f73-144">By default, the Instance Metadata Service returns data in JSON format (`Content-Type: application/json`).</span></span> <span data-ttu-id="a6f73-145">Ancak, farklı API'leri verileri farklı biçimlerde istediyseniz döndürebilir.</span><span class="sxs-lookup"><span data-stu-id="a6f73-145">However, different APIs can return data in different formats if requested.</span></span>
<span data-ttu-id="a6f73-146">Aşağıdaki tabloda, API destekleyebilir diğer veri biçimlerini başvurudur.</span><span class="sxs-lookup"><span data-stu-id="a6f73-146">The following table is a reference of other data formats APIs may support.</span></span>

<span data-ttu-id="a6f73-147">API</span><span class="sxs-lookup"><span data-stu-id="a6f73-147">API</span></span> | <span data-ttu-id="a6f73-148">Varsayılan veri biçimi</span><span class="sxs-lookup"><span data-stu-id="a6f73-148">Default Data Format</span></span> | <span data-ttu-id="a6f73-149">Diğer biçimlere</span><span class="sxs-lookup"><span data-stu-id="a6f73-149">Other Formats</span></span>
--------|---------------------|--------------
<span data-ttu-id="a6f73-150">/instance</span><span class="sxs-lookup"><span data-stu-id="a6f73-150">/instance</span></span> | <span data-ttu-id="a6f73-151">JSON</span><span class="sxs-lookup"><span data-stu-id="a6f73-151">json</span></span> | <span data-ttu-id="a6f73-152">Metin</span><span class="sxs-lookup"><span data-stu-id="a6f73-152">text</span></span>
<span data-ttu-id="a6f73-153">/scheduledevents</span><span class="sxs-lookup"><span data-stu-id="a6f73-153">/scheduledevents</span></span> | <span data-ttu-id="a6f73-154">JSON</span><span class="sxs-lookup"><span data-stu-id="a6f73-154">json</span></span> | <span data-ttu-id="a6f73-155">Yok</span><span class="sxs-lookup"><span data-stu-id="a6f73-155">none</span></span>

<span data-ttu-id="a6f73-156">Varsayılan olmayan yanıt biçimi erişmek için bir istek sorgu dizesi parametresi olarak istenen biçim belirtin.</span><span class="sxs-lookup"><span data-stu-id="a6f73-156">To access a non-default response format, specify the requested format as a querystring parameter in the request.</span></span> <span data-ttu-id="a6f73-157">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="a6f73-157">For example:</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02&format=text"
```

### <a name="security"></a><span data-ttu-id="a6f73-158">Güvenlik</span><span class="sxs-lookup"><span data-stu-id="a6f73-158">Security</span></span>
<span data-ttu-id="a6f73-159">Örnek meta veri Hizmeti uç noktası yalnızca yönlendirilebilir olmayan bir IP adresi üzerinde çalışan sanal makine örneği içinde erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="a6f73-159">The Instance Metadata Service endpoint is accessible only from within the running virtual machine instance on a non-routable IP address.</span></span> <span data-ttu-id="a6f73-160">Ayrıca, herhangi bir ile istek bir `X-Forwarded-For` üstbilgi hizmeti tarafından reddedildi.</span><span class="sxs-lookup"><span data-stu-id="a6f73-160">In addition, any request with a `X-Forwarded-For` header is rejected by the service.</span></span>
<span data-ttu-id="a6f73-161">Biz de içerecek şekilde istekleri gerektiren bir `Metadata: true` üstbilgi gerçek isteği doğrudan istenen ve istenmeyen yeniden yönlendirme bir parçası olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="a6f73-161">We also require requests to contain a `Metadata: true` header to ensure that the actual request was directly intended and not a part of unintentional redirection.</span></span> 

### <a name="error"></a><span data-ttu-id="a6f73-162">Hata</span><span class="sxs-lookup"><span data-stu-id="a6f73-162">Error</span></span>
<span data-ttu-id="a6f73-163">Bir veri öğesi bulunamadı veya hatalı biçimlendirilmiş bir istek varsa örneği meta veri hizmeti standart HTTP hatalarını döndürür.</span><span class="sxs-lookup"><span data-stu-id="a6f73-163">If there is a data element not found or a malformed request, the Instance Metadata Service returns standard HTTP errors.</span></span> <span data-ttu-id="a6f73-164">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="a6f73-164">For example:</span></span>

<span data-ttu-id="a6f73-165">HTTP durum kodu</span><span class="sxs-lookup"><span data-stu-id="a6f73-165">HTTP Status Code</span></span> | <span data-ttu-id="a6f73-166">Neden</span><span class="sxs-lookup"><span data-stu-id="a6f73-166">Reason</span></span>
----------------|-------
<span data-ttu-id="a6f73-167">200 TAMAM</span><span class="sxs-lookup"><span data-stu-id="a6f73-167">200 OK</span></span> |
<span data-ttu-id="a6f73-168">400 Hatalı istek</span><span class="sxs-lookup"><span data-stu-id="a6f73-168">400 Bad Request</span></span> | <span data-ttu-id="a6f73-169">Eksik `Metadata: true` üstbilgisi</span><span class="sxs-lookup"><span data-stu-id="a6f73-169">Missing `Metadata: true` header</span></span>
<span data-ttu-id="a6f73-170">404 Bulunamadı</span><span class="sxs-lookup"><span data-stu-id="a6f73-170">404 Not Found</span></span> | <span data-ttu-id="a6f73-171">İstenen öğe does't var</span><span class="sxs-lookup"><span data-stu-id="a6f73-171">The requested element does't exist</span></span> 
<span data-ttu-id="a6f73-172">405 Yönteme izin verilmiyor</span><span class="sxs-lookup"><span data-stu-id="a6f73-172">405 Method Not Allowed</span></span> | <span data-ttu-id="a6f73-173">Yalnızca `GET` ve `POST` istekleri desteklenir</span><span class="sxs-lookup"><span data-stu-id="a6f73-173">Only `GET` and `POST` requests are supported</span></span>
<span data-ttu-id="a6f73-174">429 çok fazla istek</span><span class="sxs-lookup"><span data-stu-id="a6f73-174">429 Too Many Requests</span></span> | <span data-ttu-id="a6f73-175">API şu anda en fazla saniyede 5 sorgularını destekler</span><span class="sxs-lookup"><span data-stu-id="a6f73-175">The API currently supports a maximum of 5 queries per second</span></span>
<span data-ttu-id="a6f73-176">500 hizmet hatası</span><span class="sxs-lookup"><span data-stu-id="a6f73-176">500 Service Error</span></span>     | <span data-ttu-id="a6f73-177">Bir süre sonra yeniden deneyin</span><span class="sxs-lookup"><span data-stu-id="a6f73-177">Retry after some time</span></span>

### <a name="examples"></a><span data-ttu-id="a6f73-178">Örnekler</span><span class="sxs-lookup"><span data-stu-id="a6f73-178">Examples</span></span>

> [!NOTE] 
> <span data-ttu-id="a6f73-179">Tüm API yanıtları JSON dizelerdir.</span><span class="sxs-lookup"><span data-stu-id="a6f73-179">All API responses are JSON strings.</span></span> <span data-ttu-id="a6f73-180">Okunabilirlik için pretty yazdırılan tüm aşağıdaki örnek yanıtlar.</span><span class="sxs-lookup"><span data-stu-id="a6f73-180">All following example responses  are pretty-printed for readability.</span></span>

#### <a name="retrieving-network-information"></a><span data-ttu-id="a6f73-181">Ağ bilgileri alınıyor</span><span class="sxs-lookup"><span data-stu-id="a6f73-181">Retrieving network information</span></span>

<span data-ttu-id="a6f73-182">**İstek**</span><span class="sxs-lookup"><span data-stu-id="a6f73-182">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network?api-version=2017-04-02"
```

<span data-ttu-id="a6f73-183">**Yanıt**</span><span class="sxs-lookup"><span data-stu-id="a6f73-183">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="a6f73-184">Yanıtı bir JSON dizesidir.</span><span class="sxs-lookup"><span data-stu-id="a6f73-184">The response is a JSON string.</span></span> <span data-ttu-id="a6f73-185">Aşağıdaki örnek yanıt okunabilirlik için pretty yazdırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="a6f73-185">The following example response is pretty-printed for readability.</span></span>

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

#### <a name="retrieving-public-ip-address"></a><span data-ttu-id="a6f73-186">Genel IP adresi alınıyor</span><span class="sxs-lookup"><span data-stu-id="a6f73-186">Retrieving public IP address</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network/interface/0/ipv4/ipAddress/0/publicIpAddress?api-version=2017-04-02&format=text"
```

#### <a name="retrieving-all-metadata-for-an-instance"></a><span data-ttu-id="a6f73-187">Bir örneği için tüm meta veri alma</span><span class="sxs-lookup"><span data-stu-id="a6f73-187">Retrieving all metadata for an instance</span></span>

<span data-ttu-id="a6f73-188">**İstek**</span><span class="sxs-lookup"><span data-stu-id="a6f73-188">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

<span data-ttu-id="a6f73-189">**Yanıt**</span><span class="sxs-lookup"><span data-stu-id="a6f73-189">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="a6f73-190">Yanıtı bir JSON dizesidir.</span><span class="sxs-lookup"><span data-stu-id="a6f73-190">The response is a JSON string.</span></span> <span data-ttu-id="a6f73-191">Aşağıdaki örnek yanıt okunabilirlik için pretty yazdırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="a6f73-191">The following example response is pretty-printed for readability.</span></span>

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

#### <a name="retrieving-metadata-in-windows-virtual-machine"></a><span data-ttu-id="a6f73-192">Meta veriler de Windows sanal makinesi alınıyor</span><span class="sxs-lookup"><span data-stu-id="a6f73-192">Retrieving metadata in Windows Virtual Machine</span></span>

<span data-ttu-id="a6f73-193">**İstek**</span><span class="sxs-lookup"><span data-stu-id="a6f73-193">**Request**</span></span>

<span data-ttu-id="a6f73-194">Örnek meta verileri alınabilir Windows PowerShell yardımcı programı `curl`:</span><span class="sxs-lookup"><span data-stu-id="a6f73-194">Instance metadata can be retrieved in Windows via the PowerShell utility `curl`:</span></span> 

```
curl -H @{'Metadata'='true'} http://169.254.169.254/metadata/instance?api-version=2017-04-02 | select -ExpandProperty Content
```

<span data-ttu-id="a6f73-195">Aracılığıyla veya `Invoke-RestMethod` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="a6f73-195">Or through the `Invoke-RestMethod` cmdlet:</span></span>
    
```
Invoke-RestMethod -Headers @{"Metadata"="true"} -URI http://169.254.169.254/metadata/instance?api-version=2017-04-02 -Method get 
```

<span data-ttu-id="a6f73-196">**Yanıt**</span><span class="sxs-lookup"><span data-stu-id="a6f73-196">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="a6f73-197">Yanıtı bir JSON dizesidir.</span><span class="sxs-lookup"><span data-stu-id="a6f73-197">The response is a JSON string.</span></span> <span data-ttu-id="a6f73-198">Aşağıdaki örnek yanıt okunabilirlik için pretty yazdırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="a6f73-198">The following example response  is pretty-printed for readability.</span></span>

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

## <a name="instance-metadata-data-categories"></a><span data-ttu-id="a6f73-199">Örnek meta veri kategorileri</span><span class="sxs-lookup"><span data-stu-id="a6f73-199">Instance metadata data categories</span></span>
<span data-ttu-id="a6f73-200">Aşağıdaki veri kategorilerini örneği meta veri hizmeti kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="a6f73-200">The following data categories are available through the Instance Metadata Service:</span></span>

<span data-ttu-id="a6f73-201">Veriler</span><span class="sxs-lookup"><span data-stu-id="a6f73-201">Data</span></span> | <span data-ttu-id="a6f73-202">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a6f73-202">Description</span></span>
-----|------------
<span data-ttu-id="a6f73-203">location</span><span class="sxs-lookup"><span data-stu-id="a6f73-203">location</span></span> | <span data-ttu-id="a6f73-204">Azure bölgesi VM çalışır durumda</span><span class="sxs-lookup"><span data-stu-id="a6f73-204">Azure Region the VM is running in</span></span>
<span data-ttu-id="a6f73-205">ad</span><span class="sxs-lookup"><span data-stu-id="a6f73-205">name</span></span> | <span data-ttu-id="a6f73-206">VM adı</span><span class="sxs-lookup"><span data-stu-id="a6f73-206">Name of the VM</span></span> 
<span data-ttu-id="a6f73-207">Teklif</span><span class="sxs-lookup"><span data-stu-id="a6f73-207">offer</span></span> | <span data-ttu-id="a6f73-208">VM görüntüsü için bilgi sunar.</span><span class="sxs-lookup"><span data-stu-id="a6f73-208">Offer information for the VM image.</span></span> <span data-ttu-id="a6f73-209">Bu değer yalnızca Azure resmi Galerisi'nden dağıtılan görüntüleri için mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="a6f73-209">This value is only present for images deployed from Azure image gallery.</span></span>
<span data-ttu-id="a6f73-210">Yayımcı</span><span class="sxs-lookup"><span data-stu-id="a6f73-210">publisher</span></span> | <span data-ttu-id="a6f73-211">VM görüntüsü yayımcısı</span><span class="sxs-lookup"><span data-stu-id="a6f73-211">Publisher of the VM image</span></span>
<span data-ttu-id="a6f73-212">SKU</span><span class="sxs-lookup"><span data-stu-id="a6f73-212">sku</span></span> | <span data-ttu-id="a6f73-213">VM görüntüsü için belirli SKU</span><span class="sxs-lookup"><span data-stu-id="a6f73-213">Specific SKU for the VM image</span></span>  
<span data-ttu-id="a6f73-214">Sürüm</span><span class="sxs-lookup"><span data-stu-id="a6f73-214">version</span></span> | <span data-ttu-id="a6f73-215">VM görüntüsü</span><span class="sxs-lookup"><span data-stu-id="a6f73-215">Version of the VM image</span></span> 
<span data-ttu-id="a6f73-216">osType</span><span class="sxs-lookup"><span data-stu-id="a6f73-216">osType</span></span> | <span data-ttu-id="a6f73-217">Linux veya Windows</span><span class="sxs-lookup"><span data-stu-id="a6f73-217">Linux or Windows</span></span> 
<span data-ttu-id="a6f73-218">platformUpdateDomain</span><span class="sxs-lookup"><span data-stu-id="a6f73-218">platformUpdateDomain</span></span> |  <span data-ttu-id="a6f73-219">[Güncelleştirme etki alanı](virtual-machines-windows-manage-availability.md) VM'nin çalışır durumda</span><span class="sxs-lookup"><span data-stu-id="a6f73-219">[Update domain](virtual-machines-windows-manage-availability.md) the VM is running in</span></span>
<span data-ttu-id="a6f73-220">platformFaultDomain</span><span class="sxs-lookup"><span data-stu-id="a6f73-220">platformFaultDomain</span></span> | <span data-ttu-id="a6f73-221">[Hata etki alanı](virtual-machines-windows-manage-availability.md) VM'nin çalışır durumda</span><span class="sxs-lookup"><span data-stu-id="a6f73-221">[Fault domain](virtual-machines-windows-manage-availability.md) the VM is running in</span></span>
<span data-ttu-id="a6f73-222">Bunun nedeni</span><span class="sxs-lookup"><span data-stu-id="a6f73-222">vmId</span></span> | <span data-ttu-id="a6f73-223">[Benzersiz tanımlayıcı](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/) VM</span><span class="sxs-lookup"><span data-stu-id="a6f73-223">[Unique identifier](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/) for the VM</span></span>
<span data-ttu-id="a6f73-224">vmSize</span><span class="sxs-lookup"><span data-stu-id="a6f73-224">vmSize</span></span> | [<span data-ttu-id="a6f73-225">VM boyutu</span><span class="sxs-lookup"><span data-stu-id="a6f73-225">VM size</span></span>](virtual-machines-windows-sizes.md)
<span data-ttu-id="a6f73-226">IPv4/privateIpAddress</span><span class="sxs-lookup"><span data-stu-id="a6f73-226">ipv4/privateIpAddress</span></span> | <span data-ttu-id="a6f73-227">VM yerel IPv4 adresi</span><span class="sxs-lookup"><span data-stu-id="a6f73-227">Local IPv4 address of the VM</span></span> 
<span data-ttu-id="a6f73-228">IPv4/Publicıpaddress</span><span class="sxs-lookup"><span data-stu-id="a6f73-228">ipv4/publicIpAddress</span></span> | <span data-ttu-id="a6f73-229">VM genel IPv4 adresi</span><span class="sxs-lookup"><span data-stu-id="a6f73-229">Public IPv4 address of the VM</span></span>
<span data-ttu-id="a6f73-230">alt ağ/adresi</span><span class="sxs-lookup"><span data-stu-id="a6f73-230">subnet/address</span></span> | <span data-ttu-id="a6f73-231">VM alt ağ adresi</span><span class="sxs-lookup"><span data-stu-id="a6f73-231">Subnet address of the VM</span></span>
<span data-ttu-id="a6f73-232">alt ağ/öneki</span><span class="sxs-lookup"><span data-stu-id="a6f73-232">subnet/prefix</span></span> | <span data-ttu-id="a6f73-233">Alt ağ öneki, örnek 24</span><span class="sxs-lookup"><span data-stu-id="a6f73-233">Subnet prefix, example 24</span></span>
<span data-ttu-id="a6f73-234">IPv6/IPADDRESS</span><span class="sxs-lookup"><span data-stu-id="a6f73-234">ipv6/ipAddress</span></span> | <span data-ttu-id="a6f73-235">VM yerel IPv6 adresi</span><span class="sxs-lookup"><span data-stu-id="a6f73-235">Local IPv6 address of the VM</span></span>
<span data-ttu-id="a6f73-236">MacAddress</span><span class="sxs-lookup"><span data-stu-id="a6f73-236">macAddress</span></span> | <span data-ttu-id="a6f73-237">VM mac adresi</span><span class="sxs-lookup"><span data-stu-id="a6f73-237">VM mac address</span></span> 
<span data-ttu-id="a6f73-238">scheduledevents</span><span class="sxs-lookup"><span data-stu-id="a6f73-238">scheduledevents</span></span> | <span data-ttu-id="a6f73-239">Genel önizlemesini görmek, şu anda [scheduledevents](virtual-machines-scheduled-events.md)</span><span class="sxs-lookup"><span data-stu-id="a6f73-239">Currently in Public Preview See [scheduledevents](virtual-machines-scheduled-events.md)</span></span>

## <a name="example-scenarios-for-usage"></a><span data-ttu-id="a6f73-240">Kullanım için örnek senaryolar</span><span class="sxs-lookup"><span data-stu-id="a6f73-240">Example Scenarios for usage</span></span>  

### <a name="tracking-vm-running-on-azure"></a><span data-ttu-id="a6f73-241">Azure üzerinde çalışan VM izleme</span><span class="sxs-lookup"><span data-stu-id="a6f73-241">Tracking VM running on Azure</span></span>

<span data-ttu-id="a6f73-242">Bir hizmet sağlayıcısı olarak yazılımınızı çalışan VM sayısı izlemek veya VM benzersizliğini izlemeniz gereken aracıların gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="a6f73-242">As a service provider, you may require to track the number of VMs running your software or have agents that need to track uniqueness of the VM.</span></span> <span data-ttu-id="a6f73-243">Bir VM için benzersiz bir kimliği elde edebilmek için kullanmak `vmId` örneği meta veri hizmetinden alan.</span><span class="sxs-lookup"><span data-stu-id="a6f73-243">To be able to get a unique ID for a VM, use the `vmId` field from Instance Metadata Service.</span></span>

<span data-ttu-id="a6f73-244">**İstek**</span><span class="sxs-lookup"><span data-stu-id="a6f73-244">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/vmId?api-version=2017-04-02&format=text"
```

<span data-ttu-id="a6f73-245">**Yanıt**</span><span class="sxs-lookup"><span data-stu-id="a6f73-245">**Response**</span></span>

```
5c08b38e-4d57-4c23-ac45-aca61037f084
```

### <a name="placement-of-containers-data-partitions-based-faultupdate-domain"></a><span data-ttu-id="a6f73-246">Yerleştirme kapsayıcıların veri bölümlerini arıza/güncelleştirme etki alanı tabanlı</span><span class="sxs-lookup"><span data-stu-id="a6f73-246">Placement of containers, data-partitions based Fault/Update domain</span></span> 

<span data-ttu-id="a6f73-247">Belirli senaryolar, farklı veri çoğaltmaları yerleşimini prime çok önemlidir.</span><span class="sxs-lookup"><span data-stu-id="a6f73-247">For certain scenarios, placement of different data replicas is of prime importance.</span></span> <span data-ttu-id="a6f73-248">Örneğin, [HDFS çoğaltma yerleştirme](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html#Replica_Placement:_The_First_Baby_Steps) veya kapsayıcı yerleştirme aracılığıyla bir [orchestrator](https://kubernetes.io/docs/user-guide/node-selection/) bilmek gerektirebilir `platformFaultDomain` ve `platformUpdateDomain` VM'nin çalışır.</span><span class="sxs-lookup"><span data-stu-id="a6f73-248">For example, [HDFS replica placement](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html#Replica_Placement:_The_First_Baby_Steps) or container placement via an [orchestrator](https://kubernetes.io/docs/user-guide/node-selection/) may you require to know the `platformFaultDomain` and `platformUpdateDomain` the VM is running on.</span></span>
<span data-ttu-id="a6f73-249">Bu veri örneği meta veri hizmeti üzerinden doğrudan sorgulayabilir.</span><span class="sxs-lookup"><span data-stu-id="a6f73-249">You can query this data directly via the Instance Metadata Service.</span></span>

<span data-ttu-id="a6f73-250">**İstek**</span><span class="sxs-lookup"><span data-stu-id="a6f73-250">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/platformFaultDomain?api-version=2017-04-02&format=text" 
```

<span data-ttu-id="a6f73-251">**Yanıt**</span><span class="sxs-lookup"><span data-stu-id="a6f73-251">**Response**</span></span>

```
0
```

### <a name="getting-more-information-about-the-vm-during-support-case"></a><span data-ttu-id="a6f73-252">Destek olayı sırasında VM hakkında daha fazla bilgi alma</span><span class="sxs-lookup"><span data-stu-id="a6f73-252">Getting more information about the VM during support case</span></span> 

<span data-ttu-id="a6f73-253">Bir hizmet sağlayıcısı olarak, burada VM hakkında daha fazla bilgiye istediğiniz bir destek çağrısı alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a6f73-253">As a service provider, you may get a support call where you would like to know more information about the VM.</span></span> <span data-ttu-id="a6f73-254">İşlem meta verileri paylaşmak için müşteri isteyen Azure VM'de türü hakkında bilgi edinmek için profesyonel desteği için temel bilgiler sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="a6f73-254">Asking the customer to share the compute metadata can provide basic information for the support professional to know about the kind of VM on Azure.</span></span> 

<span data-ttu-id="a6f73-255">**İstek**</span><span class="sxs-lookup"><span data-stu-id="a6f73-255">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute?api-version=2017-04-02"
```

<span data-ttu-id="a6f73-256">**Yanıt**</span><span class="sxs-lookup"><span data-stu-id="a6f73-256">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="a6f73-257">Yanıtı bir JSON dizesidir.</span><span class="sxs-lookup"><span data-stu-id="a6f73-257">The response is a JSON string.</span></span> <span data-ttu-id="a6f73-258">Aşağıdaki örnek yanıt okunabilirlik için pretty yazdırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="a6f73-258">The following example response is pretty-printed for readability.</span></span>

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

### <a name="examples-of-calling-metadata-service-using-different-languages-inside-the-vm"></a><span data-ttu-id="a6f73-259">VM içindeki farklı dillerde kullanarak meta veri hizmeti çağrılırken örnekleri</span><span class="sxs-lookup"><span data-stu-id="a6f73-259">Examples of calling metadata service using different languages inside the VM</span></span> 

<span data-ttu-id="a6f73-260">Dil</span><span class="sxs-lookup"><span data-stu-id="a6f73-260">Language</span></span> | <span data-ttu-id="a6f73-261">Örnek</span><span class="sxs-lookup"><span data-stu-id="a6f73-261">Example</span></span> 
---------|----------------
<span data-ttu-id="a6f73-262">Ruby</span><span class="sxs-lookup"><span data-stu-id="a6f73-262">Ruby</span></span>     | <span data-ttu-id="a6f73-263">https://github.com/Microsoft/azureimds/BLOB/master/IMDSSample.RB</span><span class="sxs-lookup"><span data-stu-id="a6f73-263">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.rb</span></span>
<span data-ttu-id="a6f73-264">LAN gidin</span><span class="sxs-lookup"><span data-stu-id="a6f73-264">Go Lan</span></span>   | <span data-ttu-id="a6f73-265">https://github.com/Microsoft/azureimds/BLOB/master/imdssample.go</span><span class="sxs-lookup"><span data-stu-id="a6f73-265">https://github.com/Microsoft/azureimds/blob/master/imdssample.go</span></span>            
<span data-ttu-id="a6f73-266">python</span><span class="sxs-lookup"><span data-stu-id="a6f73-266">python</span></span>   | <span data-ttu-id="a6f73-267">https://github.com/Microsoft/azureimds/BLOB/master/IMDSSample.PY</span><span class="sxs-lookup"><span data-stu-id="a6f73-267">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.py</span></span>
<span data-ttu-id="a6f73-268">C++</span><span class="sxs-lookup"><span data-stu-id="a6f73-268">C++</span></span>      | <span data-ttu-id="a6f73-269">https://github.com/Microsoft/azureimds/BLOB/master/IMDSSample-Windows.cpp</span><span class="sxs-lookup"><span data-stu-id="a6f73-269">https://github.com/Microsoft/azureimds/blob/master/IMDSSample-windows.cpp</span></span>
<span data-ttu-id="a6f73-270">C#</span><span class="sxs-lookup"><span data-stu-id="a6f73-270">C#</span></span>       | <span data-ttu-id="a6f73-271">https://github.com/Microsoft/azureimds/BLOB/master/IMDSSample.cs</span><span class="sxs-lookup"><span data-stu-id="a6f73-271">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.cs</span></span>
<span data-ttu-id="a6f73-272">Javascript</span><span class="sxs-lookup"><span data-stu-id="a6f73-272">Javascript</span></span> | <span data-ttu-id="a6f73-273">https://github.com/Microsoft/azureimds/BLOB/master/IMDSSample.js</span><span class="sxs-lookup"><span data-stu-id="a6f73-273">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.js</span></span>
<span data-ttu-id="a6f73-274">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a6f73-274">Powershell</span></span> | <span data-ttu-id="a6f73-275">https://github.com/Microsoft/azureimds/BLOB/master/IMDSSample.ps1</span><span class="sxs-lookup"><span data-stu-id="a6f73-275">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.ps1</span></span>
<span data-ttu-id="a6f73-276">Bash</span><span class="sxs-lookup"><span data-stu-id="a6f73-276">Bash</span></span>       | <span data-ttu-id="a6f73-277">https://github.com/Microsoft/azureimds/BLOB/master/IMDSSample.sh</span><span class="sxs-lookup"><span data-stu-id="a6f73-277">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.sh</span></span>
    

## <a name="faq"></a><span data-ttu-id="a6f73-278">SSS</span><span class="sxs-lookup"><span data-stu-id="a6f73-278">FAQ</span></span>
1. <span data-ttu-id="a6f73-279">Hata alıyorum `400 Bad Request, Required metadata header not specified`.</span><span class="sxs-lookup"><span data-stu-id="a6f73-279">I am getting the error `400 Bad Request, Required metadata header not specified`.</span></span> <span data-ttu-id="a6f73-280">Bu ne anlama geliyor?</span><span class="sxs-lookup"><span data-stu-id="a6f73-280">What does this mean?</span></span>
   * <span data-ttu-id="a6f73-281">Üst bilgisi örneği meta veri hizmeti gerektiriyor `Metadata: true` istekte geçirilecek.</span><span class="sxs-lookup"><span data-stu-id="a6f73-281">The Instance Metadata Service requires the header `Metadata: true` to be passed in the request.</span></span> <span data-ttu-id="a6f73-282">Bu üst REST çağrısı geçirme örneği meta veri hizmeti erişmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="a6f73-282">Passing this header in the REST call allows access to the Instance Metadata Service.</span></span> 
2. <span data-ttu-id="a6f73-283">Neden VM'im için işlem bilgi alıyorum değil mi?</span><span class="sxs-lookup"><span data-stu-id="a6f73-283">Why am I not getting compute information for my VM?</span></span>
   * <span data-ttu-id="a6f73-284">Şu anda örneği meta veri hizmeti, yalnızca Azure Kaynak Yöneticisi ile oluşturulan örnekleri destekler.</span><span class="sxs-lookup"><span data-stu-id="a6f73-284">Currently the Instance Metadata Service only supports instances created with Azure Resource Manager.</span></span> <span data-ttu-id="a6f73-285">Gelecekte, biz bulut hizmeti VM'ler için destek ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a6f73-285">In the future, we may add support for Cloud Service VMs.</span></span>
3. <span data-ttu-id="a6f73-286">Sanal Makinem Azure Resource Manager aracılığıyla geri bir süre oluşturdum.</span><span class="sxs-lookup"><span data-stu-id="a6f73-286">I created my Virtual Machine through Azure Resource Manager a while back.</span></span> <span data-ttu-id="a6f73-287">Bkz: değil neden ben meta veri bilgileri işlem?</span><span class="sxs-lookup"><span data-stu-id="a6f73-287">Why am I not see compute metadata information?</span></span>
   * <span data-ttu-id="a6f73-288">Eylül 2016 sonra oluşturulan tüm VM'ler için ekleme bir [etiketi](../azure-resource-manager/resource-group-using-tags.md) görmeye başlayacaksınız için meta veri işlem.</span><span class="sxs-lookup"><span data-stu-id="a6f73-288">For any VMs created after Sep 2016, add a [Tag](../azure-resource-manager/resource-group-using-tags.md) to start seeing compute metadata.</span></span> <span data-ttu-id="a6f73-289">(Eylül 2016 öncesinde oluşturulan) eski VM'ler için ekleme/meta verilerini yenilemek için VM uzantıları veya veri diski Kaldır.</span><span class="sxs-lookup"><span data-stu-id="a6f73-289">For older VMs (created before Sep 2016), add/remove extensions or data disks to the VM to refresh metadata.</span></span>
4. <span data-ttu-id="a6f73-290">Neden iletisi alıyorum hata `500 Internal Server Error`?</span><span class="sxs-lookup"><span data-stu-id="a6f73-290">Why am I getting the error `500 Internal Server Error`?</span></span>
   * <span data-ttu-id="a6f73-291">Lütfen üstel geri alma sistem göre isteğinizi yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="a6f73-291">Please retry your request based on exponential back off system.</span></span> <span data-ttu-id="a6f73-292">Sorun devam ederse Azure desteğine başvurun.</span><span class="sxs-lookup"><span data-stu-id="a6f73-292">If the issue persists contact  Azure support.</span></span>
5. <span data-ttu-id="a6f73-293">Burada ek soruları/açıklamalar paylaşmak?</span><span class="sxs-lookup"><span data-stu-id="a6f73-293">Where do I share additional questions/comments?</span></span>
   * <span data-ttu-id="a6f73-294">Yorumlarınızı üzerinde http://feedback.azure.com gönderin.</span><span class="sxs-lookup"><span data-stu-id="a6f73-294">Send your comments on http://feedback.azure.com.</span></span>
7. <span data-ttu-id="a6f73-295">Bu sanal makine ölçek kümesi örneği için çalışır?</span><span class="sxs-lookup"><span data-stu-id="a6f73-295">Would this work for Virtual Machine Scale Set Instance?</span></span>
   * <span data-ttu-id="a6f73-296">Evet meta veri hizmeti için ölçek kümesi örnek kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="a6f73-296">Yes Metadata service is available for Scale Set Instances.</span></span> 
6. <span data-ttu-id="a6f73-297">Hizmet için nasıl destek alma?</span><span class="sxs-lookup"><span data-stu-id="a6f73-297">How do I get support for the service?</span></span>
   * <span data-ttu-id="a6f73-298">Hizmeti için destek almak için uzun denemeden sonra meta veri yanıtı alabilir olduğunuz değil VM için Azure portalında bir destek sorununu oluşturma</span><span class="sxs-lookup"><span data-stu-id="a6f73-298">To get support for the service, create a support issue in Azure portal for the VM where you are not able to get metadata response after long retries</span></span> 

   ![Örnek meta verileri desteği](./media/virtual-machines-instancemetadataservice-overview/InstanceMetadata-support.png)
    
## <a name="next-steps"></a><span data-ttu-id="a6f73-300">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="a6f73-300">Next Steps</span></span>

- <span data-ttu-id="a6f73-301">Daha fazla bilgi edinmek [scheduledevents](virtual-machines-scheduled-events.md) API **içinde genel Önizleme** örneği meta veri hizmeti tarafından sağlanan.</span><span class="sxs-lookup"><span data-stu-id="a6f73-301">Learn more about the [scheduledevents](virtual-machines-scheduled-events.md) API **In Public Preview** provided by the Instance Metadata Service.</span></span>
