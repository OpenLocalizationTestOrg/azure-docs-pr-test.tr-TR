---
title: "Dosya tooAzure Azure CLI 1.0 kullanarak DNS aaaImport ve dışarı aktarma bir etki alanı bölgesi | Microsoft Docs"
description: "Nasıl tooimport ve dışarı aktarma DNS dosya tooAzure DNS Azure CLI 1.0 kullanarak bölge öğrenin"
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
ms.openlocfilehash: 4c3163395e151e9934c730349b828c612491016f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="import-and-export-a-dns-zone-file-using-hello-azure-cli-10"></a><span data-ttu-id="9b960-103">İçeri ve hello Azure CLI 1.0 kullanarak bir DNS bölge dosyasına dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="9b960-103">Import and export a DNS zone file using hello Azure CLI 1.0</span></span> 

<span data-ttu-id="9b960-104">Bu makalede Azure DNS kullanarak tooimport ve dışarı aktarma DNS bölge dosyaları için Azure CLI 1.0 nasıl hello aracılığıyla anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="9b960-104">This article walks you through how tooimport and export DNS zone files for Azure DNS using hello Azure CLI 1.0.</span></span>

## <a name="introduction-toodns-zone-migration"></a><span data-ttu-id="9b960-105">Giriş tooDNS bölge geçiş</span><span class="sxs-lookup"><span data-stu-id="9b960-105">Introduction tooDNS zone migration</span></span>

<span data-ttu-id="9b960-106">Bir DNS bölge dosyasına hello bölgedeki her etki alanı adı sistemi (DNS) kaydı ayrıntılarını içeren bir metin dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="9b960-106">A DNS zone file is a text file that contains details of every Domain Name System (DNS) record in hello zone.</span></span> <span data-ttu-id="9b960-107">DNS kayıtlarını DNS sistemler arasında aktarmak için uygun hale getirme standart bir biçimdedir.</span><span class="sxs-lookup"><span data-stu-id="9b960-107">It follows a standard format, making it suitable for transferring DNS records between DNS systems.</span></span> <span data-ttu-id="9b960-108">Bir bölge dosyası kullanarak bir hızlı, güvenilir ve uygun şekilde tootransfer içine veya dışına Azure DNS'ye bir DNS bölgesi değildir.</span><span class="sxs-lookup"><span data-stu-id="9b960-108">Using a zone file is a quick, reliable, and convenient way tootransfer a DNS zone into or out of Azure DNS.</span></span>

<span data-ttu-id="9b960-109">Azure DNS, içeri aktarma ve bölge dosyaları hello Azure komut satırı arabirimi (CLI) kullanarak dışa aktarma destekler.</span><span class="sxs-lookup"><span data-stu-id="9b960-109">Azure DNS supports importing and exporting zone files by using hello Azure command-line interface (CLI).</span></span> <span data-ttu-id="9b960-110">Bölge dosyası alma **değil** Azure PowerShell veya hello Azure portal aracılığıyla şu anda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="9b960-110">Zone file import is **not** currently supported via Azure PowerShell or hello Azure portal.</span></span>

<span data-ttu-id="9b960-111">Hello Azure CLI 1.0 yönetme Azure Hizmetleri için kullanılan bir platformlar arası komut satırı aracıdır.</span><span class="sxs-lookup"><span data-stu-id="9b960-111">hello Azure CLI 1.0 is a cross-platform command-line tool used for managing Azure services.</span></span> <span data-ttu-id="9b960-112">Merhaba Windows, Mac ve Linux platformlarından hello kullanılabilir [Azure indirmeler sayfası](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="9b960-112">It is available for hello Windows, Mac, and Linux platforms from hello [Azure downloads page](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="9b960-113">Platformlar arası desteği, en yaygın ad sunucusu yazılımı, alma ve bölge dosyaları, çünkü verme hello için önemlidir [BAĞLAMAK](https://www.isc.org/downloads/bind/), genellikle Linux üzerinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="9b960-113">Cross-platform support is important for importing and exporting zone files, because hello most common name server software, [BIND](https://www.isc.org/downloads/bind/), typically runs on Linux.</span></span>

> [!NOTE]
> <span data-ttu-id="9b960-114">Şu anda hello Azure CLI iki sürümü de vardır.</span><span class="sxs-lookup"><span data-stu-id="9b960-114">There are currently two versions of hello Azure CLI.</span></span> <span data-ttu-id="9b960-115">CLI1.0 Node.js üzerinde temel alır ve "azure" ile başlayan komutlar vardır.</span><span class="sxs-lookup"><span data-stu-id="9b960-115">CLI1.0 is based on Node.js, and has commands beginning with "azure".</span></span>
> <span data-ttu-id="9b960-116">CLI2.0 Python üzerinde temel alır ve "az" ile başlayan komutlar vardır.</span><span class="sxs-lookup"><span data-stu-id="9b960-116">CLI2.0 is based on Python and has commands beginning with "az".</span></span> <span data-ttu-id="9b960-117">Bölge dosyası alma her iki sürümde de destekleniyorsa hello CLI1.0 komutlarını kullanarak bu sayfasında açıklandığı şekilde öneririz.</span><span class="sxs-lookup"><span data-stu-id="9b960-117">While zone file import is supported in both versions, we recommend using hello CLI1.0 commands, as described in this page.</span></span>

## <a name="obtain-your-existing-dns-zone-file"></a><span data-ttu-id="9b960-118">Var olan DNS bölge dosyanızı alın</span><span class="sxs-lookup"><span data-stu-id="9b960-118">Obtain your existing DNS zone file</span></span>

<span data-ttu-id="9b960-119">Azure DNS'yi bir DNS bölge dosyasına içeri aktarmadan önce tooobtain hello bölge dosyasının bir kopyasını gerekir.</span><span class="sxs-lookup"><span data-stu-id="9b960-119">Before you import a DNS zone file into Azure DNS, you need tooobtain a copy of hello zone file.</span></span> <span data-ttu-id="9b960-120">Bu dosyanın kaynağına Hello hello DNS bölgesi şu anda barındırıldığı üzerinde bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="9b960-120">hello source of this file depends on where hello DNS zone is currently hosted.</span></span>

* <span data-ttu-id="9b960-121">DNS bölgenizi (örneğin, etki alanı kayıt şirketi, ayrılmış DNS barındırma sağlayıcısı veya alternatif bulut sağlayıcısı) bir iş ortağı hizmeti tarafından barındırılıyorsa, bu hizmet hello özelliği toodownload hello DNS bölge dosyasına sağlamalıdır.</span><span class="sxs-lookup"><span data-stu-id="9b960-121">If your DNS zone is hosted by a partner service (such as a domain registrar, dedicated DNS hosting provider, or alternative cloud provider), that service should provide hello ability toodownload hello DNS zone file.</span></span>
* <span data-ttu-id="9b960-122">DNS bölgenizi Windows DNS üzerinde barındırılıyorsa hello hello bölge dosyaları için varsayılan klasör olan **%systemroot%\system32\dns**.</span><span class="sxs-lookup"><span data-stu-id="9b960-122">If your DNS zone is hosted on Windows DNS, hello default folder for hello zone files is **%systemroot%\system32\dns**.</span></span> <span data-ttu-id="9b960-123">Merhaba tam yolu tooeach bölge dosyası ayrıca üzerinde hello gösterir **genel** hello DNS konsolunun sekmesi.</span><span class="sxs-lookup"><span data-stu-id="9b960-123">hello full path tooeach zone file also shows on hello **General** tab of hello DNS console.</span></span>
* <span data-ttu-id="9b960-124">DNS bölgesi, BIND kullanarak barındırılıyorsa hello bölge dosyası her bölge için hello konumunu hello BIND yapılandırma dosyasında belirtilen **named.conf**.</span><span class="sxs-lookup"><span data-stu-id="9b960-124">If your DNS zone is hosted by using BIND, hello location of hello zone file for each zone is specified in hello BIND configuration file **named.conf**.</span></span>

> [!NOTE]
> <span data-ttu-id="9b960-125">GoDaddy indirilen bölge dosyaları biraz standart olmayan bir biçime sahip.</span><span class="sxs-lookup"><span data-stu-id="9b960-125">Zone files downloaded from GoDaddy have a slightly nonstandard format.</span></span> <span data-ttu-id="9b960-126">Azure DNS'yi bu bölge dosyalarını içeri aktarmadan önce toocorrect bu gerekir.</span><span class="sxs-lookup"><span data-stu-id="9b960-126">You need toocorrect this before you import these zone files into Azure DNS.</span></span>
>
> <span data-ttu-id="9b960-127">Merhaba RDATA her DNS kaydının DNS adlarını tam olarak nitelenmiş adlar belirtilmiş, ancak bir sonlandırma yok "." Bu, göreli adları olarak diğer DNS sistemler tarafından yorumlanan anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="9b960-127">DNS names in hello RDATA of each DNS record are specified as fully qualified names, but they don't have a terminating "." This means they are interpreted by other DNS systems as relative names.</span></span> <span data-ttu-id="9b960-128">Tooedit hello bölge dosyası tooappend hello sonlandırma gerekir "." Azure DNS'yi almadan önce tootheir adları.</span><span class="sxs-lookup"><span data-stu-id="9b960-128">You need tooedit hello zone file tooappend hello terminating "." tootheir names before you import them into Azure DNS.</span></span>
>
> <span data-ttu-id="9b960-129">Örneğin, CNAME kaydı "www 3600 CNAME contoso.com ORMANINDAKİ" Merhaba çok değiştirilmelidir "www 3600 ın CNAME contoso.com."</span><span class="sxs-lookup"><span data-stu-id="9b960-129">For example, hello CNAME record "www 3600 IN CNAME contoso.com" should be changed too"www 3600 IN CNAME contoso.com."</span></span>
> <span data-ttu-id="9b960-130">(bir sonlandırma ile ".").</span><span class="sxs-lookup"><span data-stu-id="9b960-130">(with a terminating ".").</span></span>

## <a name="import-a-dns-zone-file-into-azure-dns"></a><span data-ttu-id="9b960-131">Azure DNS'yi bir DNS bölge dosyasına alın</span><span class="sxs-lookup"><span data-stu-id="9b960-131">Import a DNS zone file into Azure DNS</span></span>

<span data-ttu-id="9b960-132">Bir bölge dosyasını içeri bir zaten mevcut değilse yeni bir bölge, Azure DNS'de oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9b960-132">Importing a zone file creates a new zone in Azure DNS if one does not already exist.</span></span> <span data-ttu-id="9b960-133">Merhaba bölgesi zaten varsa, hello hello bölge dosyası kayıt kümelerinde hello mevcut kayıt kümeleri birleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="9b960-133">If hello zone already exists, hello record sets in hello zone file must be merged with hello existing record sets.</span></span>

### <a name="merge-behavior"></a><span data-ttu-id="9b960-134">Davranış birleştirme</span><span class="sxs-lookup"><span data-stu-id="9b960-134">Merge behavior</span></span>

* <span data-ttu-id="9b960-135">Varsayılan olarak, var olan ve yeni kayıt kümelerini birleştirilir.</span><span class="sxs-lookup"><span data-stu-id="9b960-135">By default, existing and new record sets are merged.</span></span> <span data-ttu-id="9b960-136">Birleştirilmiş bir kayıt kümesi içinde aynı kayıtlar XML'deki yinelenen.</span><span class="sxs-lookup"><span data-stu-id="9b960-136">Identical records within a merged record set are de-duplicated.</span></span>
* <span data-ttu-id="9b960-137">Merhaba belirterek alternatif olarak, `--force` seçeneği, var olan kayıt kümeleri ile yeni kayıt kümeleri içeri aktarma işlemi değiştirir hello.</span><span class="sxs-lookup"><span data-stu-id="9b960-137">Alternatively, by specifying hello `--force` option, hello import process replaces existing record sets with new record sets.</span></span> <span data-ttu-id="9b960-138">Merhaba alınan bölge dosyasında ayarlanan karşılık gelen bir kayıt yok var olan kayıt kümeleri olması kaldırılmaz.</span><span class="sxs-lookup"><span data-stu-id="9b960-138">Existing record sets that do not have a corresponding record set in hello imported zone file are not be removed.</span></span>
* <span data-ttu-id="9b960-139">Kayıt kümeleri birleştirildiğinde hello süresi toolive (TTL) önceden var olan kayıt kümelerinin kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9b960-139">When record sets are merged, hello time toolive (TTL) of preexisting record sets is used.</span></span> <span data-ttu-id="9b960-140">Zaman `--force` olan kullanıldığında, hello hello yeni kayıt kümesi TTL kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9b960-140">When `--force` is used, hello TTL of hello new record set is used.</span></span>
* <span data-ttu-id="9b960-141">Yetki (SOA) parametreleri başlangıcı (dışında `host`) hello alınan bölge dosyasından mi bağımsız olarak her zaman gerçekleştirilecek `--force` kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9b960-141">Start of Authority (SOA) parameters (except `host`) are always taken from hello imported zone file, regardless of whether `--force` is used.</span></span> <span data-ttu-id="9b960-142">Benzer şekilde, ad sunucusu kaydı hello bölgenin tepesinde ayarlamak hello için hello TTL her zaman hello alınan bölge dosyasından alınır.</span><span class="sxs-lookup"><span data-stu-id="9b960-142">Similarly, for hello name server record set at hello zone apex, hello TTL is always taken from hello imported zone file.</span></span>
* <span data-ttu-id="9b960-143">İçeri aktarılan bir CNAME kaydı varolan bir CNAME değiştirmez kaydı ile aynı adı sürece hello hello `--force` parametresi.</span><span class="sxs-lookup"><span data-stu-id="9b960-143">An imported CNAME record does not replace an existing CNAME record with hello same name unless hello `--force` parameter is specified.</span></span>
* <span data-ttu-id="9b960-144">Bir çakışma bir CNAME kaydı ve başka bir kayıtla arasında duyduğunuzda (bakılmaksızın, varolan veya yeni) aynı ancak farklı ad hello türü, hello varolan kaydı korunur.</span><span class="sxs-lookup"><span data-stu-id="9b960-144">When a conflict arises between a CNAME record and another record of hello same name but different type (regardless of which is existing or new), hello existing record is retained.</span></span> <span data-ttu-id="9b960-145">Bu hello kullanımını bağımsızdır `--force`.</span><span class="sxs-lookup"><span data-stu-id="9b960-145">This is independent of hello use of `--force`.</span></span>

### <a name="additional-information-about-importing"></a><span data-ttu-id="9b960-146">İçeri aktarma hakkında ek bilgi</span><span class="sxs-lookup"><span data-stu-id="9b960-146">Additional information about importing</span></span>

<span data-ttu-id="9b960-147">Merhaba aşağıdaki notları hello bölge hakkında ek teknik ayrıntılar alma işlemi sağlar.</span><span class="sxs-lookup"><span data-stu-id="9b960-147">hello following notes provide additional technical details about hello zone import process.</span></span>

* <span data-ttu-id="9b960-148">Merhaba `$TTL` yönergesi isteğe bağlıdır ve desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="9b960-148">hello `$TTL` directive is optional, and it is supported.</span></span> <span data-ttu-id="9b960-149">Durumlarda `$TTL` yönergesi verilen, açık bir TTL olmadan kayıtları alınır tooa varsayılan TTL 3600 saniyelik ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9b960-149">When no `$TTL` directive is given, records without an explicit TTL are imported set tooa default TTL of 3600 seconds.</span></span> <span data-ttu-id="9b960-150">İki kaydeder hello aynı kayıt kümesi belirtin farklı TTLs, hello daha düşük değer kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9b960-150">When two records in hello same record set specify different TTLs, hello lower value is used.</span></span>
* <span data-ttu-id="9b960-151">Merhaba `$ORIGIN` yönergesi isteğe bağlıdır ve desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="9b960-151">hello `$ORIGIN` directive is optional, and it is supported.</span></span> <span data-ttu-id="9b960-152">Durumlarda `$ORIGIN` ayarlandığında, hello varsayılan kullanılan hello bölge adı hello komut satırında belirtilen değerdir (Merhaba sonlandırma artı ".").</span><span class="sxs-lookup"><span data-stu-id="9b960-152">When no `$ORIGIN` is set, hello default value used is hello zone name as specified on hello command line (plus hello terminating ".").</span></span>
* <span data-ttu-id="9b960-153">Merhaba `$INCLUDE` ve `$GENERATE` yönergeleri desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="9b960-153">hello `$INCLUDE` and `$GENERATE` directives are not supported.</span></span>
* <span data-ttu-id="9b960-154">Bu kayıt türleri desteklenir: A, AAAA, CNAME, MX, NS, SOA, SRV ve TXT.</span><span class="sxs-lookup"><span data-stu-id="9b960-154">These record types are supported: A, AAAA, CNAME, MX, NS, SOA, SRV, and TXT.</span></span>
* <span data-ttu-id="9b960-155">bir bölge oluşturulduğunda SOA kaydına hello Azure DNS tarafından otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="9b960-155">hello SOA record is created automatically by Azure DNS when a zone is created.</span></span> <span data-ttu-id="9b960-156">Bir bölge dosyasını içe aktardığınızda, tüm SOA parametreleri hello bölge dosyasından alınır *dışında* hello `host` parametresi.</span><span class="sxs-lookup"><span data-stu-id="9b960-156">When you import a zone file, all SOA parameters are taken from hello zone file *except* hello `host` parameter.</span></span> <span data-ttu-id="9b960-157">Bu parametre, Azure DNS tarafından sağlanan hello değeri kullanır.</span><span class="sxs-lookup"><span data-stu-id="9b960-157">This parameter uses hello value provided by Azure DNS.</span></span> <span data-ttu-id="9b960-158">Bu parametre Azure DNS tarafından sağlanan toohello birincil ad sunucusu başvurmalıdır olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="9b960-158">This is because this parameter must refer toohello primary name server provided by Azure DNS.</span></span>
* <span data-ttu-id="9b960-159">Merhaba bölge oluşturulduğunda hello ad sunucusu kaydı hello bölgenin tepesinde ayarlamak da Azure DNS tarafından otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="9b960-159">hello name server record set at hello zone apex is also created automatically by Azure DNS when hello zone is created.</span></span> <span data-ttu-id="9b960-160">Yalnızca hello bu kayıt kümesi TTL alınır.</span><span class="sxs-lookup"><span data-stu-id="9b960-160">Only hello TTL of this record set is imported.</span></span> <span data-ttu-id="9b960-161">Bu kayıtları Azure DNS tarafından sağlanan hello ad sunucusu adlarını içerir.</span><span class="sxs-lookup"><span data-stu-id="9b960-161">These records contain hello name server names provided by Azure DNS.</span></span> <span data-ttu-id="9b960-162">Merhaba kayıt verilerini hello alınan bölge dosyasında yer alan hello değerlere göre yazılmaz.</span><span class="sxs-lookup"><span data-stu-id="9b960-162">hello record data is not overwritten by hello values contained in hello imported zone file.</span></span>
* <span data-ttu-id="9b960-163">Genel Önizleme sırasında Azure DNS yalnızca tek dize TXT kaydı destekler.</span><span class="sxs-lookup"><span data-stu-id="9b960-163">During Public Preview, Azure DNS supports only single-string TXT records.</span></span> <span data-ttu-id="9b960-164">Çok dizeli TXT kayıtlarının birleştirilmiş ve kesilmiş too255 karakter olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="9b960-164">Multistring TXT records are be concatenated and truncated too255 characters.</span></span>

### <a name="cli-format-and-values"></a><span data-ttu-id="9b960-165">CLI biçim ve değerleri</span><span class="sxs-lookup"><span data-stu-id="9b960-165">CLI format and values</span></span>

<span data-ttu-id="9b960-166">hello Azure CLI komutu tooimport bir DNS bölgesi Hello biçimi şöyledir:</span><span class="sxs-lookup"><span data-stu-id="9b960-166">hello format of hello Azure CLI command tooimport a DNS zone is:</span></span>

```azurecli
azure network dns zone import [options] <resource group> <zone name> <zone file name>
```

<span data-ttu-id="9b960-167">Değerler:</span><span class="sxs-lookup"><span data-stu-id="9b960-167">Values:</span></span>

* <span data-ttu-id="9b960-168">`<resource group>`Merhaba hello kaynak grubunun Azure DNS bölgesinde hello adıdır.</span><span class="sxs-lookup"><span data-stu-id="9b960-168">`<resource group>` is hello name of hello resource group for hello zone in Azure DNS.</span></span>
* <span data-ttu-id="9b960-169">`<zone name>`Merhaba bölge Hello adıdır.</span><span class="sxs-lookup"><span data-stu-id="9b960-169">`<zone name>` is hello name of hello zone.</span></span>
* <span data-ttu-id="9b960-170">`<zone file name>`Merhaba yol/Merhaba bölge dosyası toobe içeri adıdır.</span><span class="sxs-lookup"><span data-stu-id="9b960-170">`<zone file name>` is hello path/name of hello zone file toobe imported.</span></span>

<span data-ttu-id="9b960-171">Bu ada sahip bir bölge hello kaynak grubunda mevcut değilse sizin için oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="9b960-171">If a zone with this name does not exist in hello resource group, it is created for you.</span></span> <span data-ttu-id="9b960-172">Hello bölgesi zaten varsa, hello alınan kayıt kümelerini var olan kayıt kümeleri ile birleştirilir.</span><span class="sxs-lookup"><span data-stu-id="9b960-172">If hello zone already exists, hello imported record sets are merged with existing record sets.</span></span> <span data-ttu-id="9b960-173">toooverwrite hello mevcut kayıt kümelerini kullanma hello `--force` seçeneği.</span><span class="sxs-lookup"><span data-stu-id="9b960-173">toooverwrite hello existing record sets, use hello `--force` option.</span></span>

<span data-ttu-id="9b960-174">Aslında, kullanım hello almadan olmadan bölge dosyasının tooverify hello biçimi `--parse-only` seçeneği.</span><span class="sxs-lookup"><span data-stu-id="9b960-174">tooverify hello format of a zone file without actually importing it, use hello `--parse-only` option.</span></span>

### <a name="step-1-import-a-zone-file"></a><span data-ttu-id="9b960-175">1. Adım</span><span class="sxs-lookup"><span data-stu-id="9b960-175">Step 1.</span></span> <span data-ttu-id="9b960-176">Bir bölge dosyasını içeri aktarma</span><span class="sxs-lookup"><span data-stu-id="9b960-176">Import a zone file</span></span>

<span data-ttu-id="9b960-177">tooimport hello bölgeye ilişkin bölge dosyası **contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="9b960-177">tooimport a zone file for hello zone **contoso.com**.</span></span>

1. <span data-ttu-id="9b960-178">İçinde tooyour Azure aboneliği hello Azure CLI 1.0 kullanarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="9b960-178">Sign in tooyour Azure subscription by using hello Azure CLI 1.0.</span></span>

    ```azurecli
    azure login
    ```

2. <span data-ttu-id="9b960-179">Merhaba aboneliği yeni DNS bölgenizi toocreate istediğiniz yeri seçin.</span><span class="sxs-lookup"><span data-stu-id="9b960-179">Select hello subscription where you want toocreate your new DNS zone.</span></span>

    ```azurecli
    azure account set <subscription name>
    ```

3. <span data-ttu-id="9b960-180">Hello Azure CLI anahtarlı tooResource Yöneticisi modunda olması gerekir böylece azure DNS bir Azure yalnızca Resource Manager, hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="9b960-180">Azure DNS is an Azure Resource Manager-only service, so hello Azure CLI must be switched tooResource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

4. <span data-ttu-id="9b960-181">Hello Azure DNS hizmeti kullanmadan önce abonelik toouse hello Microsoft.Network kaynak sağlayıcısı kaydetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9b960-181">Before you use hello Azure DNS service, you must register your subscription toouse hello Microsoft.Network resource provider.</span></span> <span data-ttu-id="9b960-182">(Her abonelik için tek seferlik bir işlem budur.)</span><span class="sxs-lookup"><span data-stu-id="9b960-182">(This is a one-time operation for each subscription.)</span></span>

    ```azurecli
    azure provider register Microsoft.Network
    ```

5. <span data-ttu-id="9b960-183">Zaten yoksa, ayrıca toocreate bir Resource Manager kaynak grubu gerekir.</span><span class="sxs-lookup"><span data-stu-id="9b960-183">If you don't have one already, you also need toocreate a Resource Manager resource group.</span></span>

    ```azurecli
    azure group create myresourcegroup westeurope
    ```

6. <span data-ttu-id="9b960-184">tooimport hello bölge **contoso.com** hello dosyasından **contoso.com.txt** hello kaynak grubunda yeni bir DNS bölgesi içinde **myresourcegroup**, hello komutu çalıştırın`azure network dns zone import`.</span><span class="sxs-lookup"><span data-stu-id="9b960-184">tooimport hello zone **contoso.com** from hello file **contoso.com.txt** into a new DNS zone in hello resource group **myresourcegroup**, run hello command `azure network dns zone import`.</span></span><BR><span data-ttu-id="9b960-185">Bu komut hello bölge dosyası yükler ve onu ayrıştırılamadı.</span><span class="sxs-lookup"><span data-stu-id="9b960-185">This command loads hello zone file and parse it.</span></span> <span data-ttu-id="9b960-186">Merhaba komutu hello Azure DNS hizmeti toocreate hello bölgesi üzerinde bir dizi komut yürütür ve tüm hello kayıt hello bölgesinde ayarlar.</span><span class="sxs-lookup"><span data-stu-id="9b960-186">hello command executes a series of commands on hello Azure DNS service toocreate hello zone and all hello record sets in hello zone.</span></span> <span data-ttu-id="9b960-187">Merhaba komut penceresinde hello konsol, herhangi bir hata veya uyarı birlikte ilerlemeyi raporlar.</span><span class="sxs-lookup"><span data-stu-id="9b960-187">hello command reports progress in hello console window, along with any errors or warnings.</span></span> <span data-ttu-id="9b960-188">Kayıt kümeleri serisinde oluşturulduğundan, birkaç dakika tooimport büyük bölge dosyası sürebilir.</span><span class="sxs-lookup"><span data-stu-id="9b960-188">Because record sets are created in series, it may take a few minutes tooimport a large zone file.</span></span>

    ```azurecli
    azure network dns zone import myresourcegroup contoso.com contoso.com.txt
    ```

### <a name="step-2-verify-hello-zone"></a><span data-ttu-id="9b960-189">2. Adım</span><span class="sxs-lookup"><span data-stu-id="9b960-189">Step 2.</span></span> <span data-ttu-id="9b960-190">Merhaba bölge doğrulayın</span><span class="sxs-lookup"><span data-stu-id="9b960-190">Verify hello zone</span></span>

<span data-ttu-id="9b960-191">tooverify hello DNS bölgesi hello dosyasını aldıktan sonra yöntemler aşağıdaki hello herhangi birini kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9b960-191">tooverify hello DNS zone after you import hello file, you can use any one of hello following methods:</span></span>

* <span data-ttu-id="9b960-192">Azure CLI komutu aşağıdaki hello kullanarak hello kayıtları listeleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9b960-192">You can list hello records by using hello following Azure CLI command:</span></span>

    ```azurecli
    azure network dns record-set list myresourcegroup contoso.com
    ```

* <span data-ttu-id="9b960-193">Merhaba PowerShell cmdlet'ini kullanarak hello kayıtları listeleyebilirsiniz `Get-AzureRmDnsRecordSet`.</span><span class="sxs-lookup"><span data-stu-id="9b960-193">You can list hello records by using hello PowerShell cmdlet `Get-AzureRmDnsRecordSet`.</span></span>
* <span data-ttu-id="9b960-194">Kullanabileceğiniz `nslookup` tooverify ad çözümlemesi için hello kaydeder.</span><span class="sxs-lookup"><span data-stu-id="9b960-194">You can use `nslookup` tooverify name resolution for hello records.</span></span> <span data-ttu-id="9b960-195">Merhaba Bölge henüz temsilci değil çünkü toospecify hello doğru Azure DNS ad sunucuları açıkça gerekir.</span><span class="sxs-lookup"><span data-stu-id="9b960-195">Because hello zone isn't delegated yet, you need toospecify hello correct Azure DNS name servers explicitly.</span></span> <span data-ttu-id="9b960-196">Merhaba aşağıdaki örnek tooretrieve hello ad sunucusu adlarını toohello bölge nasıl atanacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="9b960-196">hello following sample shows how tooretrieve hello name server names assigned toohello zone.</span></span> <span data-ttu-id="9b960-197">BT ayrıca nasıl kullanarak tooquery hello "www" kayıt gösterir `nslookup`.</span><span class="sxs-lookup"><span data-stu-id="9b960-197">IT also shows how tooquery hello "www" record by using `nslookup`.</span></span>

        C:\>azure network dns record-set show myresourcegroup contoso.com @ NS
        info:Executing command network dns record-set show
        + Looking up hello DNS Record Set "@" of type "NS"
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

### <a name="step-3-update-dns-delegation"></a><span data-ttu-id="9b960-198">3. Adım</span><span class="sxs-lookup"><span data-stu-id="9b960-198">Step 3.</span></span> <span data-ttu-id="9b960-199">DNS temsilcisini güncelleştir</span><span class="sxs-lookup"><span data-stu-id="9b960-199">Update DNS delegation</span></span>

<span data-ttu-id="9b960-200">Azure DNS ad sunucularının, doğruladıktan sonra hello bölge düzgün bir şekilde içeri tooupdate hello DNS temsilci toopoint toohello gerekir.</span><span class="sxs-lookup"><span data-stu-id="9b960-200">After you have verified that hello zone has been imported correctly, you need tooupdate hello DNS delegation toopoint toohello Azure DNS name servers.</span></span> <span data-ttu-id="9b960-201">Daha fazla bilgi için hello makalesine bakın [hello DNS temsilcisini Güncelleştir](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="9b960-201">For more information, see hello article [Update hello DNS delegation](dns-domain-delegation.md).</span></span>

## <a name="export-a-dns-zone-file-from-azure-dns"></a><span data-ttu-id="9b960-202">Azure DNS'yi bir DNS bölge dosyasına dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="9b960-202">Export a DNS zone file from Azure DNS</span></span>

<span data-ttu-id="9b960-203">hello Azure CLI komutu tooimport bir DNS bölgesi Hello biçimi şöyledir:</span><span class="sxs-lookup"><span data-stu-id="9b960-203">hello format of hello Azure CLI command tooimport a DNS zone is:</span></span>

```azurecli
azure network dns zone export [options] <resource group> <zone name> <zone file name>
```

<span data-ttu-id="9b960-204">Değerler:</span><span class="sxs-lookup"><span data-stu-id="9b960-204">Values:</span></span>

* <span data-ttu-id="9b960-205">`<resource group>`Merhaba hello kaynak grubunun Azure DNS bölgesinde hello adıdır.</span><span class="sxs-lookup"><span data-stu-id="9b960-205">`<resource group>` is hello name of hello resource group for hello zone in Azure DNS.</span></span>
* <span data-ttu-id="9b960-206">`<zone name>`Merhaba bölge Hello adıdır.</span><span class="sxs-lookup"><span data-stu-id="9b960-206">`<zone name>` is hello name of hello zone.</span></span>
* <span data-ttu-id="9b960-207">`<zone file name>`Merhaba yol/dışa aktarılan hello bölge dosyası toobe adıdır.</span><span class="sxs-lookup"><span data-stu-id="9b960-207">`<zone file name>` is hello path/name of hello zone file toobe exported.</span></span>

<span data-ttu-id="9b960-208">Merhaba bölge alma ile ilk olarak toosign gerektiği, aboneliğinizi seçin ve hello Azure CLI toouse Resource Manager modunu yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="9b960-208">As with hello zone import, you first need toosign in, choose your subscription, and configure hello Azure CLI toouse Resource Manager mode.</span></span>

### <a name="tooexport-a-zone-file"></a><span data-ttu-id="9b960-209">tooexport bölge dosyası</span><span class="sxs-lookup"><span data-stu-id="9b960-209">tooexport a zone file</span></span>

1. <span data-ttu-id="9b960-210">İçinde tooyour Azure aboneliği hello Azure CLI kullanarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="9b960-210">Sign in tooyour Azure subscription by using hello Azure CLI.</span></span>

    ```azurecli
    azure login
    ```

2. <span data-ttu-id="9b960-211">DNS bölgenizi toocreate istediğiniz yere hello aboneliği seçin.</span><span class="sxs-lookup"><span data-stu-id="9b960-211">Select hello subscription where you want toocreate your DNS zone.</span></span>

    ```azurecli
    azure account set <subscription name>
    ```

3. <span data-ttu-id="9b960-212">Azure DNS bir Azure yalnızca Resource Manager hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="9b960-212">Azure DNS is an Azure Resource Manager-only service.</span></span> <span data-ttu-id="9b960-213">Hello Azure CLI anahtarlı tooResource Yöneticisi modunda olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="9b960-213">hello Azure CLI must be switched tooResource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

4. <span data-ttu-id="9b960-214">tooexport hello mevcut Azure DNS bölgesi **contoso.com** kaynak grubunda **myresourcegroup** toohello dosya **contoso.com.txt** (Merhaba geçerli klasörde), çalıştırın`azure network dns zone export`.</span><span class="sxs-lookup"><span data-stu-id="9b960-214">tooexport hello existing Azure DNS zone **contoso.com** in resource group **myresourcegroup** toohello file **contoso.com.txt** (in hello current folder), run `azure network dns zone export`.</span></span> <span data-ttu-id="9b960-215">Azure DNS hizmeti tooenumerate çağrıları hello bu komut hello bölgesinde kayıt kümeleri ve hello sonuçları tooa bağlama uyumlu bölge dosyası dışarı aktarma.</span><span class="sxs-lookup"><span data-stu-id="9b960-215">This command  calls hello Azure DNS service tooenumerate record sets in hello zone and export hello results tooa BIND-compatible zone file.</span></span>

    ```azurecli
    azure network dns zone export myresourcegroup contoso.com contoso.com.txt
    ```
