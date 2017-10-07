---
title: "aaaUse paket yakalama toodo öngörülü ağ uyarılar ve Azure işlevleri izleme | Microsoft Docs"
description: "Paket yakalama Azure Ağ İzleyicisi ile nasıl toocreate bir uyarı tetikleyen bu makalede"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 75e6e7c4-b3ba-4173-8815-b00d7d824e11
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 4722a831f3a9d5537c0e6f53daba4dfc35d0cf24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-packet-capture-for-proactive-network-monitoring-with-alerts-and-azure-functions"></a><span data-ttu-id="8bece-103">Paket yakalama öngörülü ağ izleme için uyarıları ve Azure işlevleri kullanın</span><span class="sxs-lookup"><span data-stu-id="8bece-103">Use packet capture for proactive network monitoring with alerts and Azure Functions</span></span>

<span data-ttu-id="8bece-104">Ağ İzleyicisi paket yakalama yakalama oturumları tootrack trafiği sanal makineleri filtrelemek oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8bece-104">Network Watcher packet capture creates capture sessions tootrack traffic in and out of virtual machines.</span></span> <span data-ttu-id="8bece-105">Merhaba yakalama dosyası tanımlı bir filtre olabilir tootrack yalnızca hello trafiği toomonitor istiyor.</span><span class="sxs-lookup"><span data-stu-id="8bece-105">hello capture file can have a filter that is defined tootrack only hello traffic that you want toomonitor.</span></span> <span data-ttu-id="8bece-106">Bu veriler, ardından bir depolama blob veya yerel olarak hello Konuk makineye depolanır.</span><span class="sxs-lookup"><span data-stu-id="8bece-106">This data is then stored in a storage blob or locally on hello guest machine.</span></span>

<span data-ttu-id="8bece-107">Bu özellik, Azure işlevleri gibi diğer Otomasyon senaryolardan uzaktan başlatılabilir.</span><span class="sxs-lookup"><span data-stu-id="8bece-107">This capability can be started remotely from other automation scenarios such as Azure Functions.</span></span> <span data-ttu-id="8bece-108">Paket yakalama verir yetenek toorun öngörülü yakalamaları göre hello ağ anormallikleri tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="8bece-108">Packet capture gives you hello capability toorun proactive captures based on defined network anomalies.</span></span> <span data-ttu-id="8bece-109">Diğer kullanımlar ağ yetkisiz erişim, hata ayıklama istemci-sunucu iletişimleri ve daha fazlasını hakkında bilgi alma ağ istatistikleri toplama içerir.</span><span class="sxs-lookup"><span data-stu-id="8bece-109">Other uses include gathering network statistics, getting information about network intrusions, debugging client-server communications, and more.</span></span>

<span data-ttu-id="8bece-110">Azure'da dağıtılan kaynakları 7/24 çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="8bece-110">Resources that are deployed in Azure run 24/7.</span></span> <span data-ttu-id="8bece-111">Sizin ve ekibinizin tüm kaynakları 7/24 hello durumu etkin olarak izleyemez.</span><span class="sxs-lookup"><span data-stu-id="8bece-111">You and your staff cannot actively monitor hello status of all resources 24/7.</span></span> <span data-ttu-id="8bece-112">Örneğin, 2'de bir sorun oluşursa ne olur?</span><span class="sxs-lookup"><span data-stu-id="8bece-112">For example, what happens if an issue occurs at 2 AM?</span></span>

<span data-ttu-id="8bece-113">Ağ İzleyicisi'ni kullanarak, uyarı ve işlevlerden hello Azure ekosistemi içinde ağınızda önceden hello veri ve araçları toosolve sorunlara yanıt verebilir.</span><span class="sxs-lookup"><span data-stu-id="8bece-113">By using Network Watcher, alerting, and functions from within hello Azure ecosystem, you can proactively respond with hello data and tools toosolve problems in your network.</span></span>

![Senaryo][scenario]

## <a name="prerequisites"></a><span data-ttu-id="8bece-115">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="8bece-115">Prerequisites</span></span>

* <span data-ttu-id="8bece-116">Merhaba en son sürümünü [Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="8bece-116">hello latest version of [Azure PowerShell](/powershell/azure/install-azurerm-ps).</span></span>
* <span data-ttu-id="8bece-117">Ağ İzleyicisi var olan bir örneği.</span><span class="sxs-lookup"><span data-stu-id="8bece-117">An existing instance of Network Watcher.</span></span> <span data-ttu-id="8bece-118">Zaten yoksa, [Ağ İzleyicisi örneği oluşturun](network-watcher-create.md).</span><span class="sxs-lookup"><span data-stu-id="8bece-118">If you don't already have one, [create an instance of Network Watcher](network-watcher-create.md).</span></span>
* <span data-ttu-id="8bece-119">Merhaba, mevcut bir sanal makine Ağ İzleyicisi Merhaba ile aynı bölgede [Windows uzantısı](../virtual-machines/windows/extensions-nwa.md) veya [Linux sanal makine uzantısı](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="8bece-119">An existing virtual machine in hello same region as Network Watcher with hello [Windows extension](../virtual-machines/windows/extensions-nwa.md) or [Linux virtual machine extension](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="scenario"></a><span data-ttu-id="8bece-120">Senaryo</span><span class="sxs-lookup"><span data-stu-id="8bece-120">Scenario</span></span>

<span data-ttu-id="8bece-121">Bu örnekte, VM normalden daha çok TCP kesimini gönderme ve uyarı toobe istiyor.</span><span class="sxs-lookup"><span data-stu-id="8bece-121">In this example, your VM is sending more TCP segments than usual, and you want toobe alerted.</span></span> <span data-ttu-id="8bece-122">TCP kesimini burada bir örnek olarak kullanılır, ancak hiçbir uyarı koşulu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8bece-122">TCP segments are used as an example here, but you can use any alert condition.</span></span>

<span data-ttu-id="8bece-123">Uyarı aldığınızda iletişimi neden artırmıştır tooreceive paket düzeyinde veri toounderstand istiyor.</span><span class="sxs-lookup"><span data-stu-id="8bece-123">When you are alerted, you want tooreceive packet-level data toounderstand why communication has increased.</span></span> <span data-ttu-id="8bece-124">Ardından tooreturn hello sanal makine tooregular iletişimi adımları uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8bece-124">Then you can take steps tooreturn hello virtual machine tooregular communication.</span></span>

<span data-ttu-id="8bece-125">Bu senaryo, Ağ İzleyicisi'ni ve geçerli bir sanal makine ile bir kaynak grubu mevcut bir örneği olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="8bece-125">This scenario assumes that you have an existing instance of Network Watcher and a resource group with a valid virtual machine.</span></span>

<span data-ttu-id="8bece-126">liste aşağıdaki hello gerçekleşir hello iş akışına genel bir bakış verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="8bece-126">hello following list is an overview of hello workflow that takes place:</span></span>

1. <span data-ttu-id="8bece-127">Bir uyarı, VM tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="8bece-127">An alert is triggered on your VM.</span></span>
1. <span data-ttu-id="8bece-128">Merhaba uyarı Azure işlevinizi aracılığıyla bir Web kancası çağırır.</span><span class="sxs-lookup"><span data-stu-id="8bece-128">hello alert calls your Azure function via a webhook.</span></span>
1. <span data-ttu-id="8bece-129">Azure işlevinizi hello uyarı işler ve bir Ağ İzleyicisi paket yakalama oturumu başlatır.</span><span class="sxs-lookup"><span data-stu-id="8bece-129">Your Azure function processes hello alert and starts a Network Watcher packet capture session.</span></span>
1. <span data-ttu-id="8bece-130">Merhaba paket yakalama hello VM üzerinde çalışır ve trafik toplar.</span><span class="sxs-lookup"><span data-stu-id="8bece-130">hello packet capture runs on hello VM and collects traffic.</span></span>
1. <span data-ttu-id="8bece-131">Merhaba paket yakalama dosyasını karşıya tooa inceleme ve tanılama depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="8bece-131">hello packet capture file is uploaded tooa storage account for review and diagnosis.</span></span>

<span data-ttu-id="8bece-132">tooautomate bu işlem, biz oluşturabilir ve hello olay gerçekleştiğinde bir uyarı bizim VM tootrigger bağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8bece-132">tooautomate this process, we create and connect an alert on our VM tootrigger when hello incident occurs.</span></span> <span data-ttu-id="8bece-133">Ayrıca bir işlev toocall Ağ İzleyicisi oluşturuyoruz.</span><span class="sxs-lookup"><span data-stu-id="8bece-133">We also create a function toocall into Network Watcher.</span></span>

<span data-ttu-id="8bece-134">Bu senaryo aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="8bece-134">This scenario does hello following:</span></span>

* <span data-ttu-id="8bece-135">Paket yakalama başlatır Azure bir işlev oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8bece-135">Creates an Azure function that starts a packet capture.</span></span>
* <span data-ttu-id="8bece-136">Bir sanal makinede bir uyarı kuralı oluşturur ve hello uyarı kuralı toocall hello Azure işlevi yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="8bece-136">Creates an alert rule on a virtual machine and configures hello alert rule toocall hello Azure function.</span></span>

## <a name="create-an-azure-function"></a><span data-ttu-id="8bece-137">Bir Azure işlevi oluşturma</span><span class="sxs-lookup"><span data-stu-id="8bece-137">Create an Azure function</span></span>

<span data-ttu-id="8bece-138">Merhaba ilk adımı toocreate bir Azure işlevi tooprocess hello uyarı ve paket yakalama oluşturma.</span><span class="sxs-lookup"><span data-stu-id="8bece-138">hello first step is toocreate an Azure function tooprocess hello alert and create a packet capture.</span></span>

1. <span data-ttu-id="8bece-139">Merhaba, [Azure portal](https://portal.azure.com)seçin **yeni** > **işlem** > **işlev uygulaması**.</span><span class="sxs-lookup"><span data-stu-id="8bece-139">In hello [Azure portal](https://portal.azure.com), select **New** > **Compute** > **Function App**.</span></span>

    ![Bir işlev uygulaması oluşturma][1-1]

2. <span data-ttu-id="8bece-141">Merhaba üzerinde **işlev uygulaması** dikey penceresinde hello aşağıdaki değerleri girin ve ardından **Tamam** toocreate hello uygulama:</span><span class="sxs-lookup"><span data-stu-id="8bece-141">On hello **Function App** blade, enter hello following values, and then select **OK** toocreate hello app:</span></span>

    |<span data-ttu-id="8bece-142">**Ayar**</span><span class="sxs-lookup"><span data-stu-id="8bece-142">**Setting**</span></span> | <span data-ttu-id="8bece-143">**Değer**</span><span class="sxs-lookup"><span data-stu-id="8bece-143">**Value**</span></span> | <span data-ttu-id="8bece-144">**Ayrıntılar**</span><span class="sxs-lookup"><span data-stu-id="8bece-144">**Details**</span></span> |
    |---|---|---|
    |<span data-ttu-id="8bece-145">**Uygulama adı**</span><span class="sxs-lookup"><span data-stu-id="8bece-145">**App name**</span></span>|<span data-ttu-id="8bece-146">PacketCaptureExample</span><span class="sxs-lookup"><span data-stu-id="8bece-146">PacketCaptureExample</span></span>|<span data-ttu-id="8bece-147">Merhaba işlev uygulaması Hello adı.</span><span class="sxs-lookup"><span data-stu-id="8bece-147">hello name of hello function app.</span></span>|
    |<span data-ttu-id="8bece-148">**Abonelik**</span><span class="sxs-lookup"><span data-stu-id="8bece-148">**Subscription**</span></span>|<span data-ttu-id="8bece-149">[Aboneliğinizi] hello hangi toocreate hello işlev uygulaması için aboneliği.</span><span class="sxs-lookup"><span data-stu-id="8bece-149">[Your subscription]hello subscription for which toocreate hello function app.</span></span>||
    |<span data-ttu-id="8bece-150">**Kaynak Grubu**</span><span class="sxs-lookup"><span data-stu-id="8bece-150">**Resource Group**</span></span>|<span data-ttu-id="8bece-151">PacketCaptureRG</span><span class="sxs-lookup"><span data-stu-id="8bece-151">PacketCaptureRG</span></span>|<span data-ttu-id="8bece-152">Merhaba kaynak grubu toocontain hello işlev uygulaması.</span><span class="sxs-lookup"><span data-stu-id="8bece-152">hello resource group toocontain hello function app.</span></span>|
    |<span data-ttu-id="8bece-153">**Barındırma planı**</span><span class="sxs-lookup"><span data-stu-id="8bece-153">**Hosting Plan**</span></span>|<span data-ttu-id="8bece-154">Tüketim planı</span><span class="sxs-lookup"><span data-stu-id="8bece-154">Consumption Plan</span></span>| <span data-ttu-id="8bece-155">Merhaba türü, işlev uygulaması kullanır planlayın.</span><span class="sxs-lookup"><span data-stu-id="8bece-155">hello type of plan your function app uses.</span></span> <span data-ttu-id="8bece-156">Seçenekler şunlardır tüketimi veya Azure uygulama hizmeti planı.</span><span class="sxs-lookup"><span data-stu-id="8bece-156">Options are Consumption or Azure App Service plan.</span></span> |
    |<span data-ttu-id="8bece-157">**Konum**</span><span class="sxs-lookup"><span data-stu-id="8bece-157">**Location**</span></span>|<span data-ttu-id="8bece-158">Orta ABD</span><span class="sxs-lookup"><span data-stu-id="8bece-158">Central US</span></span>| <span data-ttu-id="8bece-159">hangi toocreate hello işlev uygulaması bölgede Hello.</span><span class="sxs-lookup"><span data-stu-id="8bece-159">hello region in which toocreate hello function app.</span></span>|
    |<span data-ttu-id="8bece-160">**Depolama hesabı**</span><span class="sxs-lookup"><span data-stu-id="8bece-160">**Storage Account**</span></span>|<span data-ttu-id="8bece-161">{otomatik olarak oluşturulur}</span><span class="sxs-lookup"><span data-stu-id="8bece-161">{autogenerated}</span></span>| <span data-ttu-id="8bece-162">Azure işlevleri için genel amaçlı depolama alanı ihtiyaçlarınızı hello depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="8bece-162">hello storage account that Azure Functions needs for general-purpose storage.</span></span>|

3. <span data-ttu-id="8bece-163">Merhaba üzerinde **PacketCaptureExample işlev uygulamalarının** dikey penceresinde, select **işlevleri** > **özel işlevi**  >  **+**.</span><span class="sxs-lookup"><span data-stu-id="8bece-163">On hello **PacketCaptureExample Function Apps** blade, select **Functions** > **Custom function** >**+**.</span></span>

4. <span data-ttu-id="8bece-164">Seçin **HttpTrigger Powershell**ve ardından bilgi kalan hello girin.</span><span class="sxs-lookup"><span data-stu-id="8bece-164">Select **HttpTrigger-Powershell**, and then enter hello remaining information.</span></span> <span data-ttu-id="8bece-165">Son olarak, toocreate hello işlevi, select **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="8bece-165">Finally, toocreate hello function, select **Create**.</span></span>

    |<span data-ttu-id="8bece-166">**Ayar**</span><span class="sxs-lookup"><span data-stu-id="8bece-166">**Setting**</span></span> | <span data-ttu-id="8bece-167">**Değer**</span><span class="sxs-lookup"><span data-stu-id="8bece-167">**Value**</span></span> | <span data-ttu-id="8bece-168">**Ayrıntılar**</span><span class="sxs-lookup"><span data-stu-id="8bece-168">**Details**</span></span> |
    |---|---|---|
    |<span data-ttu-id="8bece-169">**Senaryo**</span><span class="sxs-lookup"><span data-stu-id="8bece-169">**Scenario**</span></span>|<span data-ttu-id="8bece-170">Deneysel</span><span class="sxs-lookup"><span data-stu-id="8bece-170">Experimental</span></span>|<span data-ttu-id="8bece-171">Tür senaryosu</span><span class="sxs-lookup"><span data-stu-id="8bece-171">Type of scenario</span></span>|
    |<span data-ttu-id="8bece-172">**İşlevinizi adlandırın**</span><span class="sxs-lookup"><span data-stu-id="8bece-172">**Name your function**</span></span>|<span data-ttu-id="8bece-173">AlertPacketCapturePowerShell</span><span class="sxs-lookup"><span data-stu-id="8bece-173">AlertPacketCapturePowerShell</span></span>|<span data-ttu-id="8bece-174">Merhaba işlevin adı</span><span class="sxs-lookup"><span data-stu-id="8bece-174">Name of hello function</span></span>|
    |<span data-ttu-id="8bece-175">**Yetkilendirme düzeyi**</span><span class="sxs-lookup"><span data-stu-id="8bece-175">**Authorization level**</span></span>|<span data-ttu-id="8bece-176">İşlevi</span><span class="sxs-lookup"><span data-stu-id="8bece-176">Function</span></span>|<span data-ttu-id="8bece-177">Merhaba işlevi için yetkilendirme düzeyi</span><span class="sxs-lookup"><span data-stu-id="8bece-177">Authorization level for hello function</span></span>|

![İşlevleri örneği][functions1]

> [!NOTE]
> <span data-ttu-id="8bece-179">Merhaba PowerShell şablon Deneysel ve tam desteğine sahip değil.</span><span class="sxs-lookup"><span data-stu-id="8bece-179">hello PowerShell template is experimental and does not have full support.</span></span>

<span data-ttu-id="8bece-180">Özelleştirmeleri bu örnek için gereklidir ve aşağıdaki adımları hello açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="8bece-180">Customizations are required for this example and are explained in hello following steps.</span></span>

### <a name="add-modules"></a><span data-ttu-id="8bece-181">Modüller ekleme</span><span class="sxs-lookup"><span data-stu-id="8bece-181">Add modules</span></span>

<span data-ttu-id="8bece-182">toouse Ağ İzleyicisi PowerShell cmdlet'leri hello en yeni PowerShell modülü toohello işlevi uygulamasını karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="8bece-182">toouse Network Watcher PowerShell cmdlets, upload hello latest PowerShell module toohello function app.</span></span>

1. <span data-ttu-id="8bece-183">Yerel makinenizde hello yüklü en son Azure PowerShell modülleri, hello aşağıdaki PowerShell komutunu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="8bece-183">On your local machine with hello latest Azure PowerShell modules installed, run hello following PowerShell command:</span></span>

    ```powershell
    (Get-Module AzureRM.Network).Path
    ```

    <span data-ttu-id="8bece-184">Bu örnek, Azure PowerShell modülü yerel yol hello olanağı sağlar.</span><span class="sxs-lookup"><span data-stu-id="8bece-184">This example gives you hello local path of your Azure PowerShell modules.</span></span> <span data-ttu-id="8bece-185">Bu klasörler, bir sonraki adımda kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8bece-185">These folders are used in a later step.</span></span> <span data-ttu-id="8bece-186">Bu senaryoda kullanılan hello modülleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="8bece-186">hello modules that are used in this scenario are:</span></span>

    * <span data-ttu-id="8bece-187">AzureRM.Network</span><span class="sxs-lookup"><span data-stu-id="8bece-187">AzureRM.Network</span></span>

    * <span data-ttu-id="8bece-188">AzureRM.Profile</span><span class="sxs-lookup"><span data-stu-id="8bece-188">AzureRM.Profile</span></span>

    * <span data-ttu-id="8bece-189">AzureRM.Resources</span><span class="sxs-lookup"><span data-stu-id="8bece-189">AzureRM.Resources</span></span>

    ![PowerShell klasörleri][functions5]

1. <span data-ttu-id="8bece-191">Seçin **işlev uygulaması ayarları** > **tooApp Hizmet Düzenleyicisi Git**.</span><span class="sxs-lookup"><span data-stu-id="8bece-191">Select **Function app settings** > **Go tooApp Service Editor**.</span></span>

    ![İşlev uygulama ayarları][functions2]

1. <span data-ttu-id="8bece-193">Sağ hello **AlertPacketCapturePowershell** klasörünü ve ardından adlı bir klasör oluşturun **azuremodules**.</span><span class="sxs-lookup"><span data-stu-id="8bece-193">Right-click hello **AlertPacketCapturePowershell** folder, and then create a folder called **azuremodules**.</span></span> 

4. <span data-ttu-id="8bece-194">Gereksinim duyduğunuz her modül için bir alt klasör oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8bece-194">Create a subfolder for each module that you need.</span></span>

    ![Klasör ve alt klasörleri][functions3]

    * <span data-ttu-id="8bece-196">AzureRM.Network</span><span class="sxs-lookup"><span data-stu-id="8bece-196">AzureRM.Network</span></span>

    * <span data-ttu-id="8bece-197">AzureRM.Profile</span><span class="sxs-lookup"><span data-stu-id="8bece-197">AzureRM.Profile</span></span>

    * <span data-ttu-id="8bece-198">AzureRM.Resources</span><span class="sxs-lookup"><span data-stu-id="8bece-198">AzureRM.Resources</span></span>

1. <span data-ttu-id="8bece-199">Sağ hello **AzureRM.Network** alt ve ardından **dosya yükleme**.</span><span class="sxs-lookup"><span data-stu-id="8bece-199">Right-click hello **AzureRM.Network** subfolder, and then select **Upload Files**.</span></span> 

6. <span data-ttu-id="8bece-200">Tooyour Azure Git modüller.</span><span class="sxs-lookup"><span data-stu-id="8bece-200">Go tooyour Azure modules.</span></span> <span data-ttu-id="8bece-201">Merhaba yerel **AzureRM.Network** klasörü, tüm hello dosyaları hello klasörü seçin.</span><span class="sxs-lookup"><span data-stu-id="8bece-201">In hello local **AzureRM.Network** folder, select all hello files in hello folder.</span></span> <span data-ttu-id="8bece-202">Ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="8bece-202">Then select **OK**.</span></span> 

7. <span data-ttu-id="8bece-203">İçin bu adımları yineleyin **AzureRM.Profile** ve **AzureRM.Resources**.</span><span class="sxs-lookup"><span data-stu-id="8bece-203">Repeat these steps for **AzureRM.Profile** and **AzureRM.Resources**.</span></span>

    ![Dosyaları karşıya yükleme][functions6]

1. <span data-ttu-id="8bece-205">Tamamlandı sonra her klasör hello PowerShell modülü yerel makinenize dosyalarından sahip olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8bece-205">After you've finished, each folder should have hello PowerShell module files from your local machine.</span></span>

    ![PowerShell dosyaları][functions7]

### <a name="authentication"></a><span data-ttu-id="8bece-207">Kimlik Doğrulaması</span><span class="sxs-lookup"><span data-stu-id="8bece-207">Authentication</span></span>

<span data-ttu-id="8bece-208">toouse hello PowerShell cmdlet'leri, kimlik doğrulaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8bece-208">toouse hello PowerShell cmdlets, you must authenticate.</span></span> <span data-ttu-id="8bece-209">Merhaba işlevi uygulamasında kimlik doğrulamasını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="8bece-209">You configure authentication in hello function app.</span></span> <span data-ttu-id="8bece-210">tooconfigure kimlik doğrulaması, ortam değişkenleri yapılandırmanız ve şifrelenmiş anahtar dosyası toohello işlevi uygulama yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8bece-210">tooconfigure authentication, you must configure environment variables and upload an encrypted key file toohello function app.</span></span>

> [!NOTE]
> <span data-ttu-id="8bece-211">Bu senaryoyu nasıl sadece bir örnek sağlar Azure işlevleri ile tooimplement kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="8bece-211">This scenario provides just one example of how tooimplement authentication with Azure Functions.</span></span> <span data-ttu-id="8bece-212">Vardır diğer yolları toodo bu.</span><span class="sxs-lookup"><span data-stu-id="8bece-212">There are other ways toodo this.</span></span>

#### <a name="encrypted-credentials"></a><span data-ttu-id="8bece-213">Şifrelenmiş kimlik bilgileri</span><span class="sxs-lookup"><span data-stu-id="8bece-213">Encrypted credentials</span></span>

<span data-ttu-id="8bece-214">PowerShell Betiği aşağıdaki hello adlı bir anahtar dosyası oluşturur **PassEncryptKey.key**.</span><span class="sxs-lookup"><span data-stu-id="8bece-214">hello following PowerShell script creates a key file called **PassEncryptKey.key**.</span></span> <span data-ttu-id="8bece-215">Ayrıca, sağlanan hello parola şifreli sürümünü sağlar.</span><span class="sxs-lookup"><span data-stu-id="8bece-215">It also provides an encrypted version of hello password that's supplied.</span></span> <span data-ttu-id="8bece-216">Merhaba bu paroladır hello Azure Active Directory kimlik doğrulaması için kullanılan bir uygulama için tanımlanmış aynı parola.</span><span class="sxs-lookup"><span data-stu-id="8bece-216">This password is hello same password that is defined for hello Azure Active Directory application that's used for authentication.</span></span>

```powershell
#Variables
$keypath = "C:\temp\PassEncryptKey.key"
$AESKey = New-Object Byte[] 32
$Password = "<insert a password here>"

#Keys
[Security.Cryptography.RNGCryptoServiceProvider]::Create().GetBytes($AESKey) 
Set-Content $keypath $AESKey

#Get encrypted password
$secPw = ConvertTo-SecureString -AsPlainText $Password -Force
$AESKey = Get-content $KeyPath
$Encryptedpassword = $secPw | ConvertFrom-SecureString -Key $AESKey
$Encryptedpassword
```

<span data-ttu-id="8bece-217">Hello hello işlev uygulaması App Service Düzenleyicisi, adlı bir klasör oluşturun **anahtarları** altında **AlertPacketCapturePowerShell**.</span><span class="sxs-lookup"><span data-stu-id="8bece-217">In hello App Service Editor of hello function app, create a folder called **keys** under **AlertPacketCapturePowerShell**.</span></span> <span data-ttu-id="8bece-218">Merhaba karşıya yükleme **PassEncryptKey.key** hello önceki PowerShell örneğinde oluşturulan dosyası.</span><span class="sxs-lookup"><span data-stu-id="8bece-218">Then upload hello **PassEncryptKey.key** file that you created in hello previous PowerShell sample.</span></span>

![İşlevler anahtarı][functions8]

### <a name="retrieve-values-for-environment-variables"></a><span data-ttu-id="8bece-220">Ortam değişkenleri için değerleri alma</span><span class="sxs-lookup"><span data-stu-id="8bece-220">Retrieve values for environment variables</span></span>

<span data-ttu-id="8bece-221">Merhaba son tooset kimlik doğrulaması için gerekli tooaccess hello değerler hello ortam değişkenlerini ayarlama gereksinimdir.</span><span class="sxs-lookup"><span data-stu-id="8bece-221">hello final requirement is tooset up hello environment variables that are necessary tooaccess hello values for authentication.</span></span> <span data-ttu-id="8bece-222">Merhaba aşağıdaki listede oluşturulan hello ortam değişkenleri gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="8bece-222">hello following list shows hello environment variables that are created:</span></span>

* <span data-ttu-id="8bece-223">AzureClientID</span><span class="sxs-lookup"><span data-stu-id="8bece-223">AzureClientID</span></span>

* <span data-ttu-id="8bece-224">AzureTenant</span><span class="sxs-lookup"><span data-stu-id="8bece-224">AzureTenant</span></span>

* <span data-ttu-id="8bece-225">AzureCredPassword</span><span class="sxs-lookup"><span data-stu-id="8bece-225">AzureCredPassword</span></span>


#### <a name="azureclientid"></a><span data-ttu-id="8bece-226">AzureClientID</span><span class="sxs-lookup"><span data-stu-id="8bece-226">AzureClientID</span></span>

<span data-ttu-id="8bece-227">Merhaba istemci hello Azure Active Directory'de bir uygulamanın uygulama Kimliğini kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="8bece-227">hello client ID is hello Application ID of an application in Azure Active Directory.</span></span>

1. <span data-ttu-id="8bece-228">Bir uygulama toouse zaten sahip değilseniz, örnek toocreate aşağıdaki hello bir uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="8bece-228">If you don't already have an application toouse, run hello following example toocreate an application.</span></span>

    ```powershell
    $app = New-AzureRmADApplication -DisplayName "ExampleAutomationAccount_MF" -HomePage "https://exampleapp.com" -IdentifierUris "https://exampleapp1.com/ExampleFunctionsAccount" -Password "<same password as defined earlier>"
    New-AzureRmADServicePrincipal -ApplicationId $app.ApplicationId
    Start-Sleep 15
    New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $app.ApplicationId
    ```

   > [!NOTE]
   > <span data-ttu-id="8bece-229">Merhaba uygulaması oluşturma hello olmalıdır kullandığınız hello parola hello anahtar dosyası kaydedilirken daha önce oluşturduğunuz aynı parola.</span><span class="sxs-lookup"><span data-stu-id="8bece-229">hello password that you use when creating hello application should be hello same password that you created earlier when saving hello key file.</span></span>

1. <span data-ttu-id="8bece-230">Hello Azure portal, seçin **abonelikleri**.</span><span class="sxs-lookup"><span data-stu-id="8bece-230">In hello Azure portal, select **Subscriptions**.</span></span> <span data-ttu-id="8bece-231">Merhaba abonelik toouse seçin ve ardından **erişim denetimi (IAM)**.</span><span class="sxs-lookup"><span data-stu-id="8bece-231">Select hello subscription toouse, and then select **Access control (IAM)**.</span></span>

    ![İşlevler IAM][functions9]

1. <span data-ttu-id="8bece-233">Merhaba hesap toouse seçin ve ardından **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="8bece-233">Choose hello account toouse, and then select **Properties**.</span></span> <span data-ttu-id="8bece-234">Kopya hello uygulama kimliği</span><span class="sxs-lookup"><span data-stu-id="8bece-234">Copy hello Application ID.</span></span>

    ![İşlevleri uygulama kimliği][functions10]

#### <a name="azuretenant"></a><span data-ttu-id="8bece-236">AzureTenant</span><span class="sxs-lookup"><span data-stu-id="8bece-236">AzureTenant</span></span>

<span data-ttu-id="8bece-237">PowerShell örnek aşağıdaki hello çalıştırarak Hello Kiracı kimliği alın:</span><span class="sxs-lookup"><span data-stu-id="8bece-237">Obtain hello tenant ID  by running hello following PowerShell sample:</span></span>

```powershell
(Get-AzureRmSubscription -SubscriptionName "<subscriptionName>").TenantId
```

#### <a name="azurecredpassword"></a><span data-ttu-id="8bece-238">AzureCredPassword</span><span class="sxs-lookup"><span data-stu-id="8bece-238">AzureCredPassword</span></span>

<span data-ttu-id="8bece-239">Merhaba hello AzureCredPassword ortam değişkeninin değerini PowerShell örnek aşağıdaki hello çalışmasını alma hello değerdir.</span><span class="sxs-lookup"><span data-stu-id="8bece-239">hello value of hello AzureCredPassword environment variable is hello value that you get from running hello following PowerShell sample.</span></span> <span data-ttu-id="8bece-240">Bu örnek aynı hello önceki gösterilen hello olan **şifrelenmiş kimlik bilgileri** bölümü.</span><span class="sxs-lookup"><span data-stu-id="8bece-240">This example is hello same one that's shown in hello preceding **Encrypted credentials** section.</span></span> <span data-ttu-id="8bece-241">Merhaba gerekli olan değer hello hello çıkışıdır `$Encryptedpassword` değişkeni.</span><span class="sxs-lookup"><span data-stu-id="8bece-241">hello value that's needed is hello output of hello `$Encryptedpassword` variable.</span></span>  <span data-ttu-id="8bece-242">Bu hello PowerShell Betiği kullanılarak şifrelenmiş hello hizmet asıl paroladır.</span><span class="sxs-lookup"><span data-stu-id="8bece-242">This is hello service principal password that you encrypted by using hello PowerShell script.</span></span>

```powershell
#Variables
$keypath = "C:\temp\PassEncryptKey.key"
$AESKey = New-Object Byte[] 32
$Password = "<insert a password here>"

#Keys
[Security.Cryptography.RNGCryptoServiceProvider]::Create().GetBytes($AESKey) 
Set-Content $keypath $AESKey

#Get encrypted password
$secPw = ConvertTo-SecureString -AsPlainText $Password -Force
$AESKey = Get-content $KeyPath
$Encryptedpassword = $secPw | ConvertFrom-SecureString -Key $AESKey
$Encryptedpassword
```

### <a name="store-hello-environment-variables"></a><span data-ttu-id="8bece-243">Depolama hello ortam değişkenleri</span><span class="sxs-lookup"><span data-stu-id="8bece-243">Store hello environment variables</span></span>

1. <span data-ttu-id="8bece-244">Toohello işlev uygulaması gidin.</span><span class="sxs-lookup"><span data-stu-id="8bece-244">Go toohello function app.</span></span> <span data-ttu-id="8bece-245">Ardından **işlev uygulaması ayarları** > **uygulaması ayarlarını yapılandır**.</span><span class="sxs-lookup"><span data-stu-id="8bece-245">Then select **Function app settings** > **Configure app settings**.</span></span>

    ![Uygulama ayarlarını yapılandırma][functions11]

1. <span data-ttu-id="8bece-247">Merhaba ortam değişkenlerini ve değerleri toohello uygulama ayarlarına ekleyin ve ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="8bece-247">Add hello environment variables and their values toohello app settings, and then select **Save**.</span></span>

    ![Uygulama ayarları][functions12]

### <a name="add-powershell-toohello-function"></a><span data-ttu-id="8bece-249">Add PowerShell toohello işlevi</span><span class="sxs-lookup"><span data-stu-id="8bece-249">Add PowerShell toohello function</span></span>

<span data-ttu-id="8bece-250">Ağ İzleyicisi ' içine hello Azure işlevi içinde zaman toomake çağırır artık olur.</span><span class="sxs-lookup"><span data-stu-id="8bece-250">It's now time toomake calls into Network Watcher from within hello Azure function.</span></span> <span data-ttu-id="8bece-251">Merhaba gereksinimlerine bağlı olarak, bu işlevin hello uygulama farklılık gösterebilir.</span><span class="sxs-lookup"><span data-stu-id="8bece-251">Depending on hello requirements, hello implementation of this function can vary.</span></span> <span data-ttu-id="8bece-252">Ancak, hello genel akış hello kod aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="8bece-252">However, hello general flow of hello code is as follows:</span></span>

1. <span data-ttu-id="8bece-253">İşlem giriş parametreleri.</span><span class="sxs-lookup"><span data-stu-id="8bece-253">Process input parameters.</span></span>
2. <span data-ttu-id="8bece-254">Sorgu varolan paket tooverify sınırları yakalar ve adı çakışmalarını.</span><span class="sxs-lookup"><span data-stu-id="8bece-254">Query existing packet captures tooverify limits and resolve name conflicts.</span></span>
3. <span data-ttu-id="8bece-255">Paket yakalama uygun parametrelerle oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8bece-255">Create a packet capture with appropriate parameters.</span></span>
4. <span data-ttu-id="8bece-256">Yoklama paket düzenli aralıklarla tamamlanana kadar yakalayın.</span><span class="sxs-lookup"><span data-stu-id="8bece-256">Poll packet capture periodically until it's complete.</span></span>
5. <span data-ttu-id="8bece-257">Merhaba paket yakalama oturumu tamamlandıktan Hello kullanıcıyı bilgilendirir.</span><span class="sxs-lookup"><span data-stu-id="8bece-257">Notify hello user that hello packet capture session is complete.</span></span>

<span data-ttu-id="8bece-258">Merhaba aşağıdaki örnek, hello işlevinde kullanılabilir PowerShell kodu bulunur.</span><span class="sxs-lookup"><span data-stu-id="8bece-258">hello following example is PowerShell code that can be used in hello function.</span></span> <span data-ttu-id="8bece-259">İçin yerini toobe gereken değerler **Subscriptionıd**, **resourceGroupName**, ve **storageAccountName**.</span><span class="sxs-lookup"><span data-stu-id="8bece-259">There are values that need toobe replaced for **subscriptionId**, **resourceGroupName**, and **storageAccountName**.</span></span>

```powershell
            #Import Azure PowerShell modules required toomake calls tooNetwork Watcher
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Profile\AzureRM.Profile.psd1" -Global
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Network\AzureRM.Network.psd1" -Global
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Resources\AzureRM.Resources.psd1" -Global

            #Process alert request body
            $requestBody = Get-Content $req -Raw | ConvertFrom-Json

            #Storage account ID toosave captures in
            $storageaccountid = "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{storageAccountName}"

            #Packet capture vars
            $packetcapturename = "PSAzureFunction"
            $packetCaptureLimit = 10
            $packetCaptureDuration = 10

            #Credentials
            $tenant = $env:AzureTenant
            $pw = $env:AzureCredPassword
            $clientid = $env:AzureClientId
            $keypath = "D:\home\site\wwwroot\AlertPacketCapturePowerShell\keys\PassEncryptKey.key"

            #Authentication
            $secpassword = $pw | ConvertTo-SecureString -Key (Get-Content $keypath)
            $credential = New-Object System.Management.Automation.PSCredential ($clientid, $secpassword)
            Add-AzureRMAccount -ServicePrincipal -Tenant $tenant -Credential $credential #-WarningAction SilentlyContinue | out-null


            #Get hello VM that fired hello alert
            if($requestBody.context.resourceType -eq "Microsoft.Compute/virtualMachines")
            {
                Write-Output ("Subscription ID: {0}" -f $requestBody.context.subscriptionId)
                Write-Output ("Resource Group:  {0}" -f $requestBody.context.resourceGroupName)
                Write-Output ("Resource Name:  {0}" -f $requestBody.context.resourceName)
                Write-Output ("Resource Type:  {0}" -f $requestBody.context.resourceType)

                #Get hello Network Watcher in hello VM's region
                $nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $requestBody.context.resourceRegion}
                $networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

                #Get existing packetCaptures
                $packetCaptures = Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher

                #Remove existing packet capture created by hello function (if it exists)
                $packetCaptures | %{if($_.Name -eq $packetCaptureName)
                { 
                    Remove-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName $packetCaptureName
                }}

                #Initiate packet capture on hello VM that fired hello alert
                if ((Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher).Count -lt $packetCaptureLimit){
                    echo "Initiating Packet Capture"
                    New-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -TargetVirtualMachineId $requestBody.context.resourceId -PacketCaptureName $packetCaptureName -StorageAccountId $storageaccountid -TimeLimitInSeconds $packetCaptureDuration
                    Out-File -Encoding Ascii -FilePath $res -inputObject "Packet Capture created on ${requestBody.context.resourceID}"
                }
            } 
 ``` 
#### <a name="retrieve-hello-function-url"></a><span data-ttu-id="8bece-260">Merhaba işlevi URL'sini alın</span><span class="sxs-lookup"><span data-stu-id="8bece-260">Retrieve hello function URL</span></span> 
1. <span data-ttu-id="8bece-261">İşlevinizi oluşturduktan sonra hello işlev ile ilişkili uyarı toocall hello URL'nizi yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="8bece-261">After you've created your function, configure your alert toocall hello URL that's associated with hello function.</span></span> <span data-ttu-id="8bece-262">tooget bu değer, kopyalama hello işlevi işlevi uygulamanızı URL'den.</span><span class="sxs-lookup"><span data-stu-id="8bece-262">tooget this value, copy hello function URL from your function app.</span></span>

    ![Merhaba işlevi URL bulma][functions13]

2. <span data-ttu-id="8bece-264">İşlev uygulamanız için Hello işlevi URL'sini kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="8bece-264">Copy hello function URL for your function app.</span></span>

    ![Merhaba işlevi URL kopyalanması][2]

<span data-ttu-id="8bece-266">Özel özellikler hello Web kancası POST isteğinin hello yükte gerektiriyorsa, çok başvurmak[bir Web kancası Azure ölçüm uyarıyı yapılandırmak](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="8bece-266">If you require custom properties in hello payload of hello webhook POST request, refer too[Configure a webhook on an Azure metric alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span>

## <a name="configure-an-alert-on-a-vm"></a><span data-ttu-id="8bece-267">Bir VM üzerinde bir uyarı yapılandırmak</span><span class="sxs-lookup"><span data-stu-id="8bece-267">Configure an alert on a VM</span></span>

<span data-ttu-id="8bece-268">Uyarılar, yapılandırılmış toonotify kişiler olabilir, belirli bir ölçüyü atanmış bir eşik kestiği zaman tooit.</span><span class="sxs-lookup"><span data-stu-id="8bece-268">Alerts can be configured toonotify individuals when a specific metric crosses a threshold that's assigned tooit.</span></span> <span data-ttu-id="8bece-269">Bu örnekte, hello üzerinde hello gönderilen TCP kesimini uyarısıdır, ancak diğer birçok ölçümlerini hello uyarı tetiklenebilir.</span><span class="sxs-lookup"><span data-stu-id="8bece-269">In this example, hello alert is on hello TCP segments that are sent, but hello alert can be triggered for many other metrics.</span></span> <span data-ttu-id="8bece-270">Bu örnekte, bir uyarı yapılandırılmış toocall bir Web kancası toocall hello işlevi ' dir.</span><span class="sxs-lookup"><span data-stu-id="8bece-270">In this example, an alert is configured toocall a webhook toocall hello function.</span></span>

### <a name="create-hello-alert-rule"></a><span data-ttu-id="8bece-271">Merhaba uyarı kuralı oluştur</span><span class="sxs-lookup"><span data-stu-id="8bece-271">Create hello alert rule</span></span>

<span data-ttu-id="8bece-272">Tooan varolan sanal makine gidin ve ardından bir uyarı kuralı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="8bece-272">Go tooan existing virtual machine, and then add an alert rule.</span></span> <span data-ttu-id="8bece-273">Uyarıları yapılandırma hakkında daha ayrıntılı belgeler bulunabilir [oluşturma uyarıları Azure İzleyicisi'nde için Azure services - Azure portalında](../monitoring-and-diagnostics/insights-alerts-portal.md).</span><span class="sxs-lookup"><span data-stu-id="8bece-273">More detailed documentation about configuring alerts can be found at [Create alerts in Azure Monitor for Azure services - Azure portal](../monitoring-and-diagnostics/insights-alerts-portal.md).</span></span> <span data-ttu-id="8bece-274">Merhaba değerleri aşağıdaki hello girin **uyarı kuralı** dikey ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="8bece-274">Enter hello following values in hello **Alert rule** blade, and then select **OK**.</span></span>

  |<span data-ttu-id="8bece-275">**Ayar**</span><span class="sxs-lookup"><span data-stu-id="8bece-275">**Setting**</span></span> | <span data-ttu-id="8bece-276">**Değer**</span><span class="sxs-lookup"><span data-stu-id="8bece-276">**Value**</span></span> | <span data-ttu-id="8bece-277">**Ayrıntılar**</span><span class="sxs-lookup"><span data-stu-id="8bece-277">**Details**</span></span> |
  |---|---|---|
  |<span data-ttu-id="8bece-278">**Ad**</span><span class="sxs-lookup"><span data-stu-id="8bece-278">**Name**</span></span>|<span data-ttu-id="8bece-279">TCP_Segments_Sent_Exceeded</span><span class="sxs-lookup"><span data-stu-id="8bece-279">TCP_Segments_Sent_Exceeded</span></span>|<span data-ttu-id="8bece-280">Merhaba uyarı kuralının adı.</span><span class="sxs-lookup"><span data-stu-id="8bece-280">Name of hello alert rule.</span></span>|
  |<span data-ttu-id="8bece-281">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="8bece-281">**Description**</span></span>|<span data-ttu-id="8bece-282">TCP kesimini aşıldı eşik gönderilen</span><span class="sxs-lookup"><span data-stu-id="8bece-282">TCP segments sent exceeded threshold</span></span>|<span data-ttu-id="8bece-283">Merhaba uyarı kuralı Hello açıklaması.</span><span class="sxs-lookup"><span data-stu-id="8bece-283">hello description for hello alert rule.</span></span>||
  |<span data-ttu-id="8bece-284">**Ölçüm**</span><span class="sxs-lookup"><span data-stu-id="8bece-284">**Metric**</span></span>|<span data-ttu-id="8bece-285">Gönderilen TCP kesimleri</span><span class="sxs-lookup"><span data-stu-id="8bece-285">TCP segments sent</span></span>| <span data-ttu-id="8bece-286">Merhaba ölçüm toouse tootrigger hello uyarı.</span><span class="sxs-lookup"><span data-stu-id="8bece-286">hello metric toouse tootrigger hello alert.</span></span> |
  |<span data-ttu-id="8bece-287">**Koşul**</span><span class="sxs-lookup"><span data-stu-id="8bece-287">**Condition**</span></span>|<span data-ttu-id="8bece-288">Şu değerden fazla:</span><span class="sxs-lookup"><span data-stu-id="8bece-288">Greater than</span></span>| <span data-ttu-id="8bece-289">Koşul toouse hello ölçüm değerlendirirken hello.</span><span class="sxs-lookup"><span data-stu-id="8bece-289">hello condition toouse when evaluating hello metric.</span></span>|
  |<span data-ttu-id="8bece-290">**Eşik**</span><span class="sxs-lookup"><span data-stu-id="8bece-290">**Threshold**</span></span>|<span data-ttu-id="8bece-291">100</span><span class="sxs-lookup"><span data-stu-id="8bece-291">100</span></span>| <span data-ttu-id="8bece-292">Merhaba uyarıyı tetikleyen hello ölçüm Hello değeri.</span><span class="sxs-lookup"><span data-stu-id="8bece-292">hello  value of hello metric that triggers hello alert.</span></span> <span data-ttu-id="8bece-293">Bu değer, ortamınız için geçerli değer tooa ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8bece-293">This value should be set tooa valid value for your environment.</span></span>|
  |<span data-ttu-id="8bece-294">**Süresi**</span><span class="sxs-lookup"><span data-stu-id="8bece-294">**Period**</span></span>|<span data-ttu-id="8bece-295">Merhaba son beş dakika içinde</span><span class="sxs-lookup"><span data-stu-id="8bece-295">Over hello last five minutes</span></span>| <span data-ttu-id="8bece-296">Hangi toolook Hello dönemde hello ölçüm hello eşiğine için belirler.</span><span class="sxs-lookup"><span data-stu-id="8bece-296">Determines hello period in which toolook for hello threshold on hello metric.</span></span>|
  |<span data-ttu-id="8bece-297">**Web kancası**</span><span class="sxs-lookup"><span data-stu-id="8bece-297">**Webhook**</span></span>|<span data-ttu-id="8bece-298">[işlev uygulaması URL'SİNDEN Web kancası]</span><span class="sxs-lookup"><span data-stu-id="8bece-298">[webhook URL from function app]</span></span>| <span data-ttu-id="8bece-299">Merhaba önceki adımlarda oluşturduğunuz hello işlevi uygulamadan Hello Web kancası URL'si.</span><span class="sxs-lookup"><span data-stu-id="8bece-299">hello webhook URL from hello function app that was created in hello previous steps.</span></span>|

> [!NOTE]
> <span data-ttu-id="8bece-300">Merhaba TCP kesimleri ölçümü varsayılan olarak etkin değildir.</span><span class="sxs-lookup"><span data-stu-id="8bece-300">hello TCP segments metric is not enabled by default.</span></span> <span data-ttu-id="8bece-301">Hakkında daha fazla bilgi şu adresi ziyaret ederek tooenable ek ölçümler [izleme ve tanılama](../monitoring-and-diagnostics/insights-how-to-use-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="8bece-301">Learn more about how tooenable additional metrics by visiting [Enable monitoring and diagnostics](../monitoring-and-diagnostics/insights-how-to-use-diagnostics.md).</span></span>

## <a name="review-hello-results"></a><span data-ttu-id="8bece-302">Merhaba sonuçlarını gözden geçirin</span><span class="sxs-lookup"><span data-stu-id="8bece-302">Review hello results</span></span>

<span data-ttu-id="8bece-303">Merhaba ölçütlerine sonra hello uyarı tetikleyiciler, bir paket yakalama oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="8bece-303">After hello criteria for hello alert triggers, a packet capture is created.</span></span> <span data-ttu-id="8bece-304">TooNetwork İzleyici gidin ve ardından **paket yakalama**.</span><span class="sxs-lookup"><span data-stu-id="8bece-304">Go tooNetwork Watcher, and then select **Packet capture**.</span></span> <span data-ttu-id="8bece-305">Bu sayfada hello paket yakalama dosyası bağlantı toodownload hello paket yakalama seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8bece-305">On this page, you can select hello packet capture file link toodownload hello packet capture.</span></span>

![Görünüm paket yakalama][functions14]

<span data-ttu-id="8bece-307">Merhaba yakalama dosyasını yerel olarak depolanıyorsa, toohello sanal makinede oturum açarak alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8bece-307">If hello capture file is stored locally, you can retrieve it by signing in toohello virtual machine.</span></span>

<span data-ttu-id="8bece-308">Azure depolama hesaplarından dosyalarını yükleme hakkında yönergeler için bkz: [.NET kullanarak Azure Blob storage'ı kullanmaya başlama](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="8bece-308">For instructions about downloading files from Azure storage accounts, see [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="8bece-309">Kullanabileceğiniz başka bir araçtır [Depolama Gezgini](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="8bece-309">Another tool you can use is [Storage Explorer](http://storageexplorer.com/).</span></span>

<span data-ttu-id="8bece-310">Yakalama yüklendikten sonra okuyabilir herhangi bir aracı kullanarak görüntüleyebilirsiniz bir **.cap** dosya.</span><span class="sxs-lookup"><span data-stu-id="8bece-310">After your capture has been downloaded, you can view it by using any tool that can read a **.cap** file.</span></span> <span data-ttu-id="8bece-311">Bu araçların bağlantılar tootwo şunlardır:</span><span class="sxs-lookup"><span data-stu-id="8bece-311">Following are links tootwo of these tools:</span></span>

- [<span data-ttu-id="8bece-312">Microsoft Message Analyzer</span><span class="sxs-lookup"><span data-stu-id="8bece-312">Microsoft Message Analyzer</span></span>](https://technet.microsoft.com/library/jj649776.aspx)
- [<span data-ttu-id="8bece-313">WireShark</span><span class="sxs-lookup"><span data-stu-id="8bece-313">WireShark</span></span>](https://www.wireshark.org/)

## <a name="next-steps"></a><span data-ttu-id="8bece-314">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8bece-314">Next steps</span></span>

<span data-ttu-id="8bece-315">Nasıl tooview ziyaret ederek, paket yakalar öğrenin [paket yakalama çözümlemesini Wireshark ile](network-watcher-deep-packet-inspection.md).</span><span class="sxs-lookup"><span data-stu-id="8bece-315">Learn how tooview your packet captures by visiting [Packet capture analysis with Wireshark](network-watcher-deep-packet-inspection.md).</span></span>


[1]: ./media/network-watcher-alert-triggered-packet-capture/figure1.png
[1-1]: ./media/network-watcher-alert-triggered-packet-capture/figure1-1.png
[2]: ./media/network-watcher-alert-triggered-packet-capture/figure2.png
[3]: ./media/network-watcher-alert-triggered-packet-capture/figure3.png
[functions1]:./media/network-watcher-alert-triggered-packet-capture/functions1.png
[functions2]:./media/network-watcher-alert-triggered-packet-capture/functions2.png
[functions3]:./media/network-watcher-alert-triggered-packet-capture/functions3.png
[functions4]:./media/network-watcher-alert-triggered-packet-capture/functions4.png
[functions5]:./media/network-watcher-alert-triggered-packet-capture/functions5.png
[functions6]:./media/network-watcher-alert-triggered-packet-capture/functions6.png
[functions7]:./media/network-watcher-alert-triggered-packet-capture/functions7.png
[functions8]:./media/network-watcher-alert-triggered-packet-capture/functions8.png
[functions9]:./media/network-watcher-alert-triggered-packet-capture/functions9.png
[functions10]:./media/network-watcher-alert-triggered-packet-capture/functions10.png
[functions11]:./media/network-watcher-alert-triggered-packet-capture/functions11.png
[functions12]:./media/network-watcher-alert-triggered-packet-capture/functions12.png
[functions13]:./media/network-watcher-alert-triggered-packet-capture/functions13.png
[functions14]:./media/network-watcher-alert-triggered-packet-capture/functions14.png
[scenario]:./media/network-watcher-alert-triggered-packet-capture/scenario.png
