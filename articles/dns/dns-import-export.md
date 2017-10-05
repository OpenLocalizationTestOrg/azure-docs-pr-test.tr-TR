---
title: "Alma ve Azure CLI 1.0 kullanarak Azure DNS'ye bir etki alanı bölge dosyasına verme | Microsoft Docs"
description: "İçeri aktarma ve Azure CLI 1.0 kullanarak Azure DNS'ye bir DNS bölge dosyasına dışarı aktarma hakkında bilgi edinin"
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: f5797782-3005-4663-a488-ac0089809010
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2016
ms.author: gwallace
ms.openlocfilehash: d6d3fa7aa0e8b2462b3a6b4b66d3d87ab5535314
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="import-and-export-a-dns-zone-file-using-the-azure-cli-10"></a><span data-ttu-id="ea328-103">Alma ve Azure CLI 1.0 kullanarak bir DNS bölge dosyasına verme</span><span class="sxs-lookup"><span data-stu-id="ea328-103">Import and export a DNS zone file using the Azure CLI 1.0</span></span> 

<span data-ttu-id="ea328-104">Bu makalede, Azure CLI 1.0 kullanarak Azure DNS için DNS bölge dosyalarını vermek ve almak nasıl açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ea328-104">This article walks you through how to import and export DNS zone files for Azure DNS using the Azure CLI 1.0.</span></span>

## <a name="introduction-to-dns-zone-migration"></a><span data-ttu-id="ea328-105">DNS bölge geçişe giriş</span><span class="sxs-lookup"><span data-stu-id="ea328-105">Introduction to DNS zone migration</span></span>

<span data-ttu-id="ea328-106">Bir DNS bölge dosyasına bölgedeki her etki alanı adı sistemi (DNS) kaydı ayrıntılarını içeren bir metin dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="ea328-106">A DNS zone file is a text file that contains details of every Domain Name System (DNS) record in the zone.</span></span> <span data-ttu-id="ea328-107">DNS kayıtlarını DNS sistemler arasında aktarmak için uygun hale getirme standart bir biçimdedir.</span><span class="sxs-lookup"><span data-stu-id="ea328-107">It follows a standard format, making it suitable for transferring DNS records between DNS systems.</span></span> <span data-ttu-id="ea328-108">Bir bölge dosyası kullanarak içine veya dışına Azure DNS'ye bir DNS bölgesi aktarmak için bir hızlı, güvenilir ve kolay yoludur.</span><span class="sxs-lookup"><span data-stu-id="ea328-108">Using a zone file is a quick, reliable, and convenient way to transfer a DNS zone into or out of Azure DNS.</span></span>

<span data-ttu-id="ea328-109">Azure DNS, içeri aktarma ve Azure komut satırı arabirimi (CLI) kullanarak bölge dosyaları dışarı aktarma destekler.</span><span class="sxs-lookup"><span data-stu-id="ea328-109">Azure DNS supports importing and exporting zone files by using the Azure command-line interface (CLI).</span></span> <span data-ttu-id="ea328-110">Bölge dosyası alma **değil** Azure PowerShell veya Azure Portalı aracılığıyla şu anda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="ea328-110">Zone file import is **not** currently supported via Azure PowerShell or the Azure portal.</span></span>

<span data-ttu-id="ea328-111">Azure CLI 1.0 Azure hizmetleri yönetmek için kullanılan bir platformlar arası komut satırı aracıdır.</span><span class="sxs-lookup"><span data-stu-id="ea328-111">The Azure CLI 1.0 is a cross-platform command-line tool used for managing Azure services.</span></span> <span data-ttu-id="ea328-112">Windows, Mac ve Linux platformlarından için kullanılabilir [Azure indirmeler sayfası](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="ea328-112">It is available for the Windows, Mac, and Linux platforms from the [Azure downloads page](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="ea328-113">Platformlar arası desteği önemlidir içeri ve dışarı aktarma bölge dosyaları için çünkü en yaygın adı sunucu yazılımı [BAĞLAMAK](https://www.isc.org/downloads/bind/), genellikle Linux üzerinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="ea328-113">Cross-platform support is important for importing and exporting zone files, because the most common name server software, [BIND](https://www.isc.org/downloads/bind/), typically runs on Linux.</span></span>

> [!NOTE]
> <span data-ttu-id="ea328-114">Şu anda Azure CLI iki sürümü de vardır.</span><span class="sxs-lookup"><span data-stu-id="ea328-114">There are currently two versions of the Azure CLI.</span></span> <span data-ttu-id="ea328-115">CLI1.0 Node.js üzerinde temel alır ve "azure" ile başlayan komutlar vardır.</span><span class="sxs-lookup"><span data-stu-id="ea328-115">CLI1.0 is based on Node.js, and has commands beginning with "azure".</span></span>
> <span data-ttu-id="ea328-116">CLI2.0 Python üzerinde temel alır ve "az" ile başlayan komutlar vardır.</span><span class="sxs-lookup"><span data-stu-id="ea328-116">CLI2.0 is based on Python and has commands beginning with "az".</span></span> <span data-ttu-id="ea328-117">Bölge dosyası alma her iki sürümde de destekleniyorsa CLI1.0 komutlarını kullanarak bu sayfasında açıklandığı şekilde öneririz.</span><span class="sxs-lookup"><span data-stu-id="ea328-117">While zone file import is supported in both versions, we recommend using the CLI1.0 commands, as described in this page.</span></span>

## <a name="obtain-your-existing-dns-zone-file"></a><span data-ttu-id="ea328-118">Var olan DNS bölge dosyanızı alın</span><span class="sxs-lookup"><span data-stu-id="ea328-118">Obtain your existing DNS zone file</span></span>

<span data-ttu-id="ea328-119">Azure DNS'yi bir DNS bölge dosyasına içeri aktarmadan önce bölge dosyasının bir kopyasını edinmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ea328-119">Before you import a DNS zone file into Azure DNS, you need to obtain a copy of the zone file.</span></span> <span data-ttu-id="ea328-120">DNS bölgesi şu anda barındırıldığı üzerinde bu dosyanın kaynağına bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="ea328-120">The source of this file depends on where the DNS zone is currently hosted.</span></span>

* <span data-ttu-id="ea328-121">DNS bölgenizi (örneğin, etki alanı kayıt şirketi, ayrılmış DNS barındırma sağlayıcısı veya alternatif bulut sağlayıcısı) bir iş ortağı hizmeti tarafından barındırılıyorsa, bu hizmetin DNS bölge dosya yükleme olanağı sağlamalıdır.</span><span class="sxs-lookup"><span data-stu-id="ea328-121">If your DNS zone is hosted by a partner service (such as a domain registrar, dedicated DNS hosting provider, or alternative cloud provider), that service should provide the ability to download the DNS zone file.</span></span>
* <span data-ttu-id="ea328-122">DNS bölgenizi Windows DNS üzerinde barındırılıyorsa, bölge dosyaları için varsayılan klasördür **%systemroot%\system32\dns**.</span><span class="sxs-lookup"><span data-stu-id="ea328-122">If your DNS zone is hosted on Windows DNS, the default folder for the zone files is **%systemroot%\system32\dns**.</span></span> <span data-ttu-id="ea328-123">Her bölge dosyasının tam yolunu da gösterir **genel** DNS konsolunun sekmesi.</span><span class="sxs-lookup"><span data-stu-id="ea328-123">The full path to each zone file also shows on the **General** tab of the DNS console.</span></span>
* <span data-ttu-id="ea328-124">DNS bölgenizi BIND kullanarak barındırılıyorsa, her bölge için bölge dosyasının konumu BIND yapılandırma dosyasında belirtilen **named.conf**.</span><span class="sxs-lookup"><span data-stu-id="ea328-124">If your DNS zone is hosted by using BIND, the location of the zone file for each zone is specified in the BIND configuration file **named.conf**.</span></span>

> [!NOTE]
> <span data-ttu-id="ea328-125">GoDaddy indirilen bölge dosyaları biraz standart olmayan bir biçime sahip.</span><span class="sxs-lookup"><span data-stu-id="ea328-125">Zone files downloaded from GoDaddy have a slightly nonstandard format.</span></span> <span data-ttu-id="ea328-126">Azure DNS'yi bu bölge dosyalarını içeri aktarmadan önce bunu düzeltmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ea328-126">You need to correct this before you import these zone files into Azure DNS.</span></span>
>
> <span data-ttu-id="ea328-127">RDATA her DNS kaydının DNS adlarını tam olarak nitelenmiş adlar belirtilmiş, ancak bir sonlandırma yok "." Bu, göreli adları olarak diğer DNS sistemler tarafından yorumlanan anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="ea328-127">DNS names in the RDATA of each DNS record are specified as fully qualified names, but they don't have a terminating "." This means they are interpreted by other DNS systems as relative names.</span></span> <span data-ttu-id="ea328-128">Sonlandırma eklenecek bölge dosyasını düzenlemeniz gerekir "." Azure DNS'yi almadan önce adlarıyla.</span><span class="sxs-lookup"><span data-stu-id="ea328-128">You need to edit the zone file to append the terminating "." to their names before you import them into Azure DNS.</span></span>
>
> <span data-ttu-id="ea328-129">Örneğin, "www 3600 CNAME contoso.com ORMANINDAKİ" CNAME kaydı "CNAME contoso.com 3600 www." değiştirilmesi gerekir</span><span class="sxs-lookup"><span data-stu-id="ea328-129">For example, the CNAME record "www 3600 IN CNAME contoso.com" should be changed to "www 3600 IN CNAME contoso.com."</span></span>
> <span data-ttu-id="ea328-130">(bir sonlandırma ile ".").</span><span class="sxs-lookup"><span data-stu-id="ea328-130">(with a terminating ".").</span></span>

## <a name="import-a-dns-zone-file-into-azure-dns"></a><span data-ttu-id="ea328-131">Azure DNS'yi bir DNS bölge dosyasına alın</span><span class="sxs-lookup"><span data-stu-id="ea328-131">Import a DNS zone file into Azure DNS</span></span>

<span data-ttu-id="ea328-132">Bir bölge dosyasını içeri bir zaten mevcut değilse yeni bir bölge, Azure DNS'de oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ea328-132">Importing a zone file creates a new zone in Azure DNS if one does not already exist.</span></span> <span data-ttu-id="ea328-133">Bölgesi zaten varsa, bölge dosyası kayıt kümelerinde mevcut kayıt kümeleriyle birleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="ea328-133">If the zone already exists, the record sets in the zone file must be merged with the existing record sets.</span></span>

### <a name="merge-behavior"></a><span data-ttu-id="ea328-134">Davranış birleştirme</span><span class="sxs-lookup"><span data-stu-id="ea328-134">Merge behavior</span></span>

* <span data-ttu-id="ea328-135">Varsayılan olarak, var olan ve yeni kayıt kümelerini birleştirilir.</span><span class="sxs-lookup"><span data-stu-id="ea328-135">By default, existing and new record sets are merged.</span></span> <span data-ttu-id="ea328-136">Birleştirilmiş bir kayıt kümesi içinde aynı kayıtlar XML'deki yinelenen.</span><span class="sxs-lookup"><span data-stu-id="ea328-136">Identical records within a merged record set are de-duplicated.</span></span>
* <span data-ttu-id="ea328-137">Belirterek alternatif olarak, `--force` seçeneği, var olan kayıt kümeleri yeni kayıt kümeleri ile içeri aktarma işlemi değiştirir.</span><span class="sxs-lookup"><span data-stu-id="ea328-137">Alternatively, by specifying the `--force` option, the import process replaces existing record sets with new record sets.</span></span> <span data-ttu-id="ea328-138">Alınan bölge dosyasında ayarlanan karşılık gelen bir kayıt yok var olan kayıt kümeleri olması kaldırılmaz.</span><span class="sxs-lookup"><span data-stu-id="ea328-138">Existing record sets that do not have a corresponding record set in the imported zone file are not be removed.</span></span>
* <span data-ttu-id="ea328-139">Kayıt kümeleri birleştirildiğinde, yaşam süresi (TTL) önceden var olan kayıt kümelerinin kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ea328-139">When record sets are merged, the time to live (TTL) of preexisting record sets is used.</span></span> <span data-ttu-id="ea328-140">Zaman `--force` olan kullanıldığında, yeni kayıt kümesi TTL kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ea328-140">When `--force` is used, the TTL of the new record set is used.</span></span>
* <span data-ttu-id="ea328-141">Yetki (SOA) parametreleri başlangıcı (dışında `host`) içeri aktarılan bölge dosyasından mi bağımsız olarak her zaman gerçekleştirilecek `--force` kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ea328-141">Start of Authority (SOA) parameters (except `host`) are always taken from the imported zone file, regardless of whether `--force` is used.</span></span> <span data-ttu-id="ea328-142">Benzer şekilde, bölgenin tepesinde ayarlamak ad sunucusu kaydı için TTL her zaman alınan bölge dosyasından alınır.</span><span class="sxs-lookup"><span data-stu-id="ea328-142">Similarly, for the name server record set at the zone apex, the TTL is always taken from the imported zone file.</span></span>
* <span data-ttu-id="ea328-143">İçeri aktarılan bir CNAME kaydı aynı ada sahip varolan bir CNAME kaydı sürece değiştirmez `--force` parametresi belirtilir.</span><span class="sxs-lookup"><span data-stu-id="ea328-143">An imported CNAME record does not replace an existing CNAME record with the same name unless the `--force` parameter is specified.</span></span>
* <span data-ttu-id="ea328-144">Bir CNAME kaydı ve başka bir kayıtla aynı adlı ancak farklı türü (bakılmaksızın, varolan veya yeni) arasında bir çakışma ortaya etkinleştirildiğinde, varolan bir kaydı korunur.</span><span class="sxs-lookup"><span data-stu-id="ea328-144">When a conflict arises between a CNAME record and another record of the same name but different type (regardless of which is existing or new), the existing record is retained.</span></span> <span data-ttu-id="ea328-145">Bu kullanımını bağımsızdır `--force`.</span><span class="sxs-lookup"><span data-stu-id="ea328-145">This is independent of the use of `--force`.</span></span>

### <a name="additional-information-about-importing"></a><span data-ttu-id="ea328-146">İçeri aktarma hakkında ek bilgi</span><span class="sxs-lookup"><span data-stu-id="ea328-146">Additional information about importing</span></span>

<span data-ttu-id="ea328-147">Aşağıdaki notlar, bölge hakkında ek teknik ayrıntılar alma işlemi sunar.</span><span class="sxs-lookup"><span data-stu-id="ea328-147">The following notes provide additional technical details about the zone import process.</span></span>

* <span data-ttu-id="ea328-148">`$TTL` Yönergesi isteğe bağlıdır ve desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="ea328-148">The `$TTL` directive is optional, and it is supported.</span></span> <span data-ttu-id="ea328-149">Durumlarda `$TTL` yönergesi verilen, açık bir TTL olmadan kayıtları varsayılan TTL 3600 saniyelik alınan kümesi.</span><span class="sxs-lookup"><span data-stu-id="ea328-149">When no `$TTL` directive is given, records without an explicit TTL are imported set to a default TTL of 3600 seconds.</span></span> <span data-ttu-id="ea328-150">Aynı kayıt kümesindeki iki kayıt farklı TTLs belirttiğinizde, daha düşük değer kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ea328-150">When two records in the same record set specify different TTLs, the lower value is used.</span></span>
* <span data-ttu-id="ea328-151">`$ORIGIN` Yönergesi isteğe bağlıdır ve desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="ea328-151">The `$ORIGIN` directive is optional, and it is supported.</span></span> <span data-ttu-id="ea328-152">Durumlarda `$ORIGIN` , kullanılan varsayılan değer: komut satırında belirtilen bölge adı ayarlanmadı (sonlandırma artı ".").</span><span class="sxs-lookup"><span data-stu-id="ea328-152">When no `$ORIGIN` is set, the default value used is the zone name as specified on the command line (plus the terminating ".").</span></span>
* <span data-ttu-id="ea328-153">`$INCLUDE` Ve `$GENERATE` yönergeleri desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="ea328-153">The `$INCLUDE` and `$GENERATE` directives are not supported.</span></span>
* <span data-ttu-id="ea328-154">Bu kayıt türleri desteklenir: A, AAAA, CNAME, MX, NS, SOA, SRV ve TXT.</span><span class="sxs-lookup"><span data-stu-id="ea328-154">These record types are supported: A, AAAA, CNAME, MX, NS, SOA, SRV, and TXT.</span></span>
* <span data-ttu-id="ea328-155">Bir bölge oluşturulduğunda SOA kaydı Azure DNS tarafından otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="ea328-155">The SOA record is created automatically by Azure DNS when a zone is created.</span></span> <span data-ttu-id="ea328-156">Bir bölge dosyasını içe aktardığınızda, tüm SOA parametreleri bölge dosyasından alınır *dışında* `host` parametresi.</span><span class="sxs-lookup"><span data-stu-id="ea328-156">When you import a zone file, all SOA parameters are taken from the zone file *except* the `host` parameter.</span></span> <span data-ttu-id="ea328-157">Bu parametre, Azure DNS tarafından sağlanan değeri kullanır.</span><span class="sxs-lookup"><span data-stu-id="ea328-157">This parameter uses the value provided by Azure DNS.</span></span> <span data-ttu-id="ea328-158">Bu durum, bu parametre Azure DNS tarafından sağlanan birincil ad sunucusu başvurması gerekir çünkü.</span><span class="sxs-lookup"><span data-stu-id="ea328-158">This is because this parameter must refer to the primary name server provided by Azure DNS.</span></span>
* <span data-ttu-id="ea328-159">Bölge oluşturulduğunda bölgenin tepesinde ayarlamak ad sunucusu kaydı da Azure DNS tarafından otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="ea328-159">The name server record set at the zone apex is also created automatically by Azure DNS when the zone is created.</span></span> <span data-ttu-id="ea328-160">Yalnızca bu kayıt kümesi TTL alınır.</span><span class="sxs-lookup"><span data-stu-id="ea328-160">Only the TTL of this record set is imported.</span></span> <span data-ttu-id="ea328-161">Bu kayıtları Azure DNS tarafından sağlanan ad sunucusu adlarını içerir.</span><span class="sxs-lookup"><span data-stu-id="ea328-161">These records contain the name server names provided by Azure DNS.</span></span> <span data-ttu-id="ea328-162">Kayıt verileri tarafından alınan bölge dosyasında yer alan değerler yazılmaz.</span><span class="sxs-lookup"><span data-stu-id="ea328-162">The record data is not overwritten by the values contained in the imported zone file.</span></span>
* <span data-ttu-id="ea328-163">Genel Önizleme sırasında Azure DNS yalnızca tek dize TXT kaydı destekler.</span><span class="sxs-lookup"><span data-stu-id="ea328-163">During Public Preview, Azure DNS supports only single-string TXT records.</span></span> <span data-ttu-id="ea328-164">Çok dizeli TXT kayıtlarının birleştirilmiş ve 255 karakter olarak kesildi.</span><span class="sxs-lookup"><span data-stu-id="ea328-164">Multistring TXT records are be concatenated and truncated to 255 characters.</span></span>

### <a name="cli-format-and-values"></a><span data-ttu-id="ea328-165">CLI biçim ve değerleri</span><span class="sxs-lookup"><span data-stu-id="ea328-165">CLI format and values</span></span>

<span data-ttu-id="ea328-166">Bir DNS bölgesi almak için Azure CLI komut biçimi şöyledir:</span><span class="sxs-lookup"><span data-stu-id="ea328-166">The format of the Azure CLI command to import a DNS zone is:</span></span>

```azurecli
azure network dns zone import [options] <resource group> <zone name> <zone file name>
```

<span data-ttu-id="ea328-167">Değerler:</span><span class="sxs-lookup"><span data-stu-id="ea328-167">Values:</span></span>

* <span data-ttu-id="ea328-168">`<resource group>`kaynak grubunun Azure DNS bölgesinde adıdır.</span><span class="sxs-lookup"><span data-stu-id="ea328-168">`<resource group>` is the name of the resource group for the zone in Azure DNS.</span></span>
* <span data-ttu-id="ea328-169">`<zone name>`Bölge adıdır.</span><span class="sxs-lookup"><span data-stu-id="ea328-169">`<zone name>` is the name of the zone.</span></span>
* <span data-ttu-id="ea328-170">`<zone file name>`İçeri aktarılacak bölge dosyası yolu/adıdır.</span><span class="sxs-lookup"><span data-stu-id="ea328-170">`<zone file name>` is the path/name of the zone file to be imported.</span></span>

<span data-ttu-id="ea328-171">Bu ada sahip bir bölge kaynak grubunda mevcut değilse sizin için oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="ea328-171">If a zone with this name does not exist in the resource group, it is created for you.</span></span> <span data-ttu-id="ea328-172">Bölgesi zaten varsa, içeri aktarılan kayıt kümelerini var olan kayıt kümeleri ile birleştirilir.</span><span class="sxs-lookup"><span data-stu-id="ea328-172">If the zone already exists, the imported record sets are merged with existing record sets.</span></span> <span data-ttu-id="ea328-173">Var olan kayıt kümeleri üzerine yazmak için kullanın `--force` seçeneği.</span><span class="sxs-lookup"><span data-stu-id="ea328-173">To overwrite the existing record sets, use the `--force` option.</span></span>

<span data-ttu-id="ea328-174">Bir bölge dosyası biçimi gerçekten almadan doğrulamak için kullanın `--parse-only` seçeneği.</span><span class="sxs-lookup"><span data-stu-id="ea328-174">To verify the format of a zone file without actually importing it, use the `--parse-only` option.</span></span>

### <a name="step-1-import-a-zone-file"></a><span data-ttu-id="ea328-175">1. Adım</span><span class="sxs-lookup"><span data-stu-id="ea328-175">Step 1.</span></span> <span data-ttu-id="ea328-176">Bir bölge dosyasını içeri aktarma</span><span class="sxs-lookup"><span data-stu-id="ea328-176">Import a zone file</span></span>

<span data-ttu-id="ea328-177">Bölge için bir bölge dosyasına aktarmak için **contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="ea328-177">To import a zone file for the zone **contoso.com**.</span></span>

1. <span data-ttu-id="ea328-178">Azure CLI 1.0 kullanarak Azure aboneliğinizde oturum açın.</span><span class="sxs-lookup"><span data-stu-id="ea328-178">Sign in to your Azure subscription by using the Azure CLI 1.0.</span></span>

    ```azurecli
    azure login
    ```

2. <span data-ttu-id="ea328-179">Yeni DNS bölgenizi oluşturmak istediğiniz aboneliği seçin.</span><span class="sxs-lookup"><span data-stu-id="ea328-179">Select the subscription where you want to create your new DNS zone.</span></span>

    ```azurecli
    azure account set <subscription name>
    ```

3. <span data-ttu-id="ea328-180">Azure DNS bir Azure yalnızca Resource Manager hizmeti kitabıdır Azure CLI Resource Manager moduna geçirilmesi gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="ea328-180">Azure DNS is an Azure Resource Manager-only service, so the Azure CLI must be switched to Resource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

4. <span data-ttu-id="ea328-181">Azure DNS hizmeti kullanmadan önce Microsoft.Network kaynak sağlayıcısını kullanmak için aboneliğinizi kaydetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ea328-181">Before you use the Azure DNS service, you must register your subscription to use the Microsoft.Network resource provider.</span></span> <span data-ttu-id="ea328-182">(Her abonelik için tek seferlik bir işlem budur.)</span><span class="sxs-lookup"><span data-stu-id="ea328-182">(This is a one-time operation for each subscription.)</span></span>

    ```azurecli
    azure provider register Microsoft.Network
    ```

5. <span data-ttu-id="ea328-183">Zaten yoksa, ayrıca bir Resource Manager kaynak grubu oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ea328-183">If you don't have one already, you also need to create a Resource Manager resource group.</span></span>

    ```azurecli
    azure group create myresourcegroup westeurope
    ```

6. <span data-ttu-id="ea328-184">Bölge almak için **contoso.com** dosyasından **contoso.com.txt** kaynak grubunda yeni bir DNS bölgesi içinde **myresourcegroup**, komutu çalıştırmak `azure network dns zone import`.</span><span class="sxs-lookup"><span data-stu-id="ea328-184">To import the zone **contoso.com** from the file **contoso.com.txt** into a new DNS zone in the resource group **myresourcegroup**, run the command `azure network dns zone import`.</span></span><BR><span data-ttu-id="ea328-185">Bu komut bölge dosyasını yükler ve bu ayrıştırılamadı.</span><span class="sxs-lookup"><span data-stu-id="ea328-185">This command loads the zone file and parse it.</span></span> <span data-ttu-id="ea328-186">Komutu bir dizi komut bölgesi oluşturmak için Azure DNS hizmeti yürütür ve tüm kayıt bölgeyi ayarlar.</span><span class="sxs-lookup"><span data-stu-id="ea328-186">The command executes a series of commands on the Azure DNS service to create the zone and all the record sets in the zone.</span></span> <span data-ttu-id="ea328-187">Komut konsol penceresinde herhangi bir hata veya uyarı birlikte ilerlemeyi raporlar.</span><span class="sxs-lookup"><span data-stu-id="ea328-187">The command reports progress in the console window, along with any errors or warnings.</span></span> <span data-ttu-id="ea328-188">Kayıt kümeleri serisinde oluşturulduğundan, büyük bölge dosyasını içeri aktarmak için birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="ea328-188">Because record sets are created in series, it may take a few minutes to import a large zone file.</span></span>

    ```azurecli
    azure network dns zone import myresourcegroup contoso.com contoso.com.txt
    ```

### <a name="step-2-verify-the-zone"></a><span data-ttu-id="ea328-189">2. Adım</span><span class="sxs-lookup"><span data-stu-id="ea328-189">Step 2.</span></span> <span data-ttu-id="ea328-190">Bölge doğrulayın</span><span class="sxs-lookup"><span data-stu-id="ea328-190">Verify the zone</span></span>

<span data-ttu-id="ea328-191">Dosyayı içeri aktardıktan sonra DNS bölgesi doğrulamak için aşağıdaki yöntemlerden birini kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ea328-191">To verify the DNS zone after you import the file, you can use any one of the following methods:</span></span>

* <span data-ttu-id="ea328-192">Aşağıdaki Azure CLI komutunu kullanarak kayıtları listeleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ea328-192">You can list the records by using the following Azure CLI command:</span></span>

    ```azurecli
    azure network dns record-set list myresourcegroup contoso.com
    ```

* <span data-ttu-id="ea328-193">PowerShell cmdlet'ini kullanarak kayıtları listeleyebilirsiniz `Get-AzureRmDnsRecordSet`.</span><span class="sxs-lookup"><span data-stu-id="ea328-193">You can list the records by using the PowerShell cmdlet `Get-AzureRmDnsRecordSet`.</span></span>
* <span data-ttu-id="ea328-194">Kullanabileceğiniz `nslookup` kayıtlar için ad çözümlemesini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="ea328-194">You can use `nslookup` to verify name resolution for the records.</span></span> <span data-ttu-id="ea328-195">Bölge henüz temsilci değil çünkü doğru Azure DNS ad sunucuları açıkça belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ea328-195">Because the zone isn't delegated yet, you need to specify the correct Azure DNS name servers explicitly.</span></span> <span data-ttu-id="ea328-196">Aşağıdaki örnek, bölgenize atanan ad sunucusu adlarını almak gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ea328-196">The following sample shows how to retrieve the name server names assigned to the zone.</span></span> <span data-ttu-id="ea328-197">BT ayrıca kullanarak "www" kayıt sorgulama gösterir `nslookup`.</span><span class="sxs-lookup"><span data-stu-id="ea328-197">IT also shows how to query the "www" record by using `nslookup`.</span></span>

        C:\>azure network dns record-set show myresourcegroup contoso.com @ NS
        info:Executing command network dns record-set show
        + Looking up the DNS Record Set "@" of type "NS"
        data:Id: /subscriptions/.../resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com/NS/@
        data:Name: @
        data:Type: Microsoft.Network/dnszones/NS
        data:Location: global
        data:TTL : 3600
        data:NS records
        data:Name server domain name : ns1-01.azure-dns.com
        data:Name server domain name : ns2-01.azure-dns.net
        data:Name server domain name : ns3-01.azure-dns.org
        data:Name server domain name : ns4-01.azure-dns.info
        data:
        info:network dns record-set show command OK

        C:\> nslookup www.contoso.com ns1-01.azure-dns.com

        Server: ns1-01.azure-dns.com
        Address:  40.90.4.1

        Name:www.contoso.com
        Addresses:  134.170.185.46
        134.170.188.221

### <a name="step-3-update-dns-delegation"></a><span data-ttu-id="ea328-198">3. Adım</span><span class="sxs-lookup"><span data-stu-id="ea328-198">Step 3.</span></span> <span data-ttu-id="ea328-199">DNS temsilcisini güncelleştir</span><span class="sxs-lookup"><span data-stu-id="ea328-199">Update DNS delegation</span></span>

<span data-ttu-id="ea328-200">Bölge düzgün bir şekilde içeri olduğunu doğruladıktan sonra Azure DNS ad sunucularını işaret edecek şekilde DNS temsilcisini güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ea328-200">After you have verified that the zone has been imported correctly, you need to update the DNS delegation to point to the Azure DNS name servers.</span></span> <span data-ttu-id="ea328-201">Daha fazla bilgi için bkz: [DNS temsilcisini güncelleştirmesi](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="ea328-201">For more information, see the article [Update the DNS delegation](dns-domain-delegation.md).</span></span>

## <a name="export-a-dns-zone-file-from-azure-dns"></a><span data-ttu-id="ea328-202">Azure DNS'yi bir DNS bölge dosyasına dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="ea328-202">Export a DNS zone file from Azure DNS</span></span>

<span data-ttu-id="ea328-203">Bir DNS bölgesi almak için Azure CLI komut biçimi şöyledir:</span><span class="sxs-lookup"><span data-stu-id="ea328-203">The format of the Azure CLI command to import a DNS zone is:</span></span>

```azurecli
azure network dns zone export [options] <resource group> <zone name> <zone file name>
```

<span data-ttu-id="ea328-204">Değerler:</span><span class="sxs-lookup"><span data-stu-id="ea328-204">Values:</span></span>

* <span data-ttu-id="ea328-205">`<resource group>`kaynak grubunun Azure DNS bölgesinde adıdır.</span><span class="sxs-lookup"><span data-stu-id="ea328-205">`<resource group>` is the name of the resource group for the zone in Azure DNS.</span></span>
* <span data-ttu-id="ea328-206">`<zone name>`Bölge adıdır.</span><span class="sxs-lookup"><span data-stu-id="ea328-206">`<zone name>` is the name of the zone.</span></span>
* <span data-ttu-id="ea328-207">`<zone file name>`dışa aktarılacak bölge dosyası yolu/adıdır.</span><span class="sxs-lookup"><span data-stu-id="ea328-207">`<zone file name>` is the path/name of the zone file to be exported.</span></span>

<span data-ttu-id="ea328-208">Olarak bölge alma işleminde, ilk oturum için aboneliğinizi seçin ve Resource Manager modunu kullanmak için Azure CLI yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="ea328-208">As with the zone import, you first need to sign in, choose your subscription, and configure the Azure CLI to use Resource Manager mode.</span></span>

### <a name="to-export-a-zone-file"></a><span data-ttu-id="ea328-209">Bir bölge dosyasına dışarı aktarmak için</span><span class="sxs-lookup"><span data-stu-id="ea328-209">To export a zone file</span></span>

1. <span data-ttu-id="ea328-210">Azure CLI kullanarak Azure aboneliğinizde oturum açın.</span><span class="sxs-lookup"><span data-stu-id="ea328-210">Sign in to your Azure subscription by using the Azure CLI.</span></span>

    ```azurecli
    azure login
    ```

2. <span data-ttu-id="ea328-211">DNS bölgenizi oluşturmak istediğiniz aboneliği seçin.</span><span class="sxs-lookup"><span data-stu-id="ea328-211">Select the subscription where you want to create your DNS zone.</span></span>

    ```azurecli
    azure account set <subscription name>
    ```

3. <span data-ttu-id="ea328-212">Azure DNS bir Azure yalnızca Resource Manager hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="ea328-212">Azure DNS is an Azure Resource Manager-only service.</span></span> <span data-ttu-id="ea328-213">Azure CLI Resource Manager moduna geçirilmesi gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="ea328-213">The Azure CLI must be switched to Resource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

4. <span data-ttu-id="ea328-214">Varolan bir Azure DNS bölgesi dışarı aktarmak için **contoso.com** kaynak grubunda **myresourcegroup** dosyaya **contoso.com.txt** (geçerli), çalışma klasörü `azure network dns zone export`.</span><span class="sxs-lookup"><span data-stu-id="ea328-214">To export the existing Azure DNS zone **contoso.com** in resource group **myresourcegroup** to the file **contoso.com.txt** (in the current folder), run `azure network dns zone export`.</span></span> <span data-ttu-id="ea328-215">Bu komutun bölge içindeki kayıt kümelerini numaralandırır ve sonuçları bir BIND uyumlu bölge dosyasına dışarı aktarmak için Azure DNS hizmeti çağırır.</span><span class="sxs-lookup"><span data-stu-id="ea328-215">This command  calls the Azure DNS service to enumerate record sets in the zone and export the results to a BIND-compatible zone file.</span></span>

    ```azurecli
    azure network dns zone export myresourcegroup contoso.com contoso.com.txt
    ```
