---
title: "Uyarılar ve Azure işlevleri öngörülü ağ izleme yapmak için paket yakalama kullanın | Microsoft Docs"
description: "Bu makalede Azure Ağ İzleyicisi ile bir uyarı tetiklenen paket yakalama oluşturma"
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
ms.openlocfilehash: b813172fc1fc1cc683f463f05370c95bfec10f8d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="use-packet-capture-for-proactive-network-monitoring-with-alerts-and-azure-functions"></a><span data-ttu-id="d96ea-103">Paket yakalama öngörülü ağ izleme için uyarıları ve Azure işlevleri kullanın</span><span class="sxs-lookup"><span data-stu-id="d96ea-103">Use packet capture for proactive network monitoring with alerts and Azure Functions</span></span>

<span data-ttu-id="d96ea-104">Ağ İzleyicisi paket yakalama trafiği sanal makineler ve izlemek için yakalama oturumları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d96ea-104">Network Watcher packet capture creates capture sessions to track traffic in and out of virtual machines.</span></span> <span data-ttu-id="d96ea-105">Yakalama dosyası, izlemek istediğiniz trafiği izlemek için tanımlanmış bir filtre olabilir.</span><span class="sxs-lookup"><span data-stu-id="d96ea-105">The capture file can have a filter that is defined to track only the traffic that you want to monitor.</span></span> <span data-ttu-id="d96ea-106">Bu veriler, ardından bir depolama blob veya yerel olarak Konuk makinedeki depolanır.</span><span class="sxs-lookup"><span data-stu-id="d96ea-106">This data is then stored in a storage blob or locally on the guest machine.</span></span>

<span data-ttu-id="d96ea-107">Bu özellik, Azure işlevleri gibi diğer Otomasyon senaryolardan uzaktan başlatılabilir.</span><span class="sxs-lookup"><span data-stu-id="d96ea-107">This capability can be started remotely from other automation scenarios such as Azure Functions.</span></span> <span data-ttu-id="d96ea-108">Paket yakalama üzerinde tanımlı ağ anormallikleri dayalı öngörülü yakalamaları çalıştırmak için yeteneği verir.</span><span class="sxs-lookup"><span data-stu-id="d96ea-108">Packet capture gives you the capability to run proactive captures based on defined network anomalies.</span></span> <span data-ttu-id="d96ea-109">Diğer kullanımlar ağ yetkisiz erişim, hata ayıklama istemci-sunucu iletişimleri ve daha fazlasını hakkında bilgi alma ağ istatistikleri toplama içerir.</span><span class="sxs-lookup"><span data-stu-id="d96ea-109">Other uses include gathering network statistics, getting information about network intrusions, debugging client-server communications, and more.</span></span>

<span data-ttu-id="d96ea-110">Azure'da dağıtılan kaynakları 7/24 çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="d96ea-110">Resources that are deployed in Azure run 24/7.</span></span> <span data-ttu-id="d96ea-111">Sizin ve ekibinizin 7/24 tüm kaynakların durum etkin olarak izleyemez.</span><span class="sxs-lookup"><span data-stu-id="d96ea-111">You and your staff cannot actively monitor the status of all resources 24/7.</span></span> <span data-ttu-id="d96ea-112">Örneğin, 2'de bir sorun oluşursa ne olur?</span><span class="sxs-lookup"><span data-stu-id="d96ea-112">For example, what happens if an issue occurs at 2 AM?</span></span>

<span data-ttu-id="d96ea-113">Ağ İzleyicisi'ni kullanarak, uyarı ve işlevlerden Azure ekosistemi içinde veri ve ağınızdaki sorunları çözmek için araçları ile önceden yanıt verebilir.</span><span class="sxs-lookup"><span data-stu-id="d96ea-113">By using Network Watcher, alerting, and functions from within the Azure ecosystem, you can proactively respond with the data and tools to solve problems in your network.</span></span>

![Senaryo][scenario]

## <a name="prerequisites"></a><span data-ttu-id="d96ea-115">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="d96ea-115">Prerequisites</span></span>

* <span data-ttu-id="d96ea-116">En son sürümünü [Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="d96ea-116">The latest version of [Azure PowerShell](/powershell/azure/install-azurerm-ps).</span></span>
* <span data-ttu-id="d96ea-117">Ağ İzleyicisi var olan bir örneği.</span><span class="sxs-lookup"><span data-stu-id="d96ea-117">An existing instance of Network Watcher.</span></span> <span data-ttu-id="d96ea-118">Zaten yoksa, [Ağ İzleyicisi örneği oluşturun](network-watcher-create.md).</span><span class="sxs-lookup"><span data-stu-id="d96ea-118">If you don't already have one, [create an instance of Network Watcher](network-watcher-create.md).</span></span>
* <span data-ttu-id="d96ea-119">Ağ İzleyicisi ile aynı bölgede var olan bir sanal makine [Windows uzantısı](../virtual-machines/windows/extensions-nwa.md) veya [Linux sanal makine uzantısı](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="d96ea-119">An existing virtual machine in the same region as Network Watcher with the [Windows extension](../virtual-machines/windows/extensions-nwa.md) or [Linux virtual machine extension](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="scenario"></a><span data-ttu-id="d96ea-120">Senaryo</span><span class="sxs-lookup"><span data-stu-id="d96ea-120">Scenario</span></span>

<span data-ttu-id="d96ea-121">Bu örnekte, VM normalden daha çok TCP kesimini gönderme ve uyarı almak istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="d96ea-121">In this example, your VM is sending more TCP segments than usual, and you want to be alerted.</span></span> <span data-ttu-id="d96ea-122">TCP kesimini burada bir örnek olarak kullanılır, ancak hiçbir uyarı koşulu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d96ea-122">TCP segments are used as an example here, but you can use any alert condition.</span></span>

<span data-ttu-id="d96ea-123">Uyarı aldığınızda iletişimi neden artırmıştır anlamak için paket düzeyinde verileri almak istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="d96ea-123">When you are alerted, you want to receive packet-level data to understand why communication has increased.</span></span> <span data-ttu-id="d96ea-124">Daha sonra sanal makineyi normal iletişimi döndürmek için adımları alabilir.</span><span class="sxs-lookup"><span data-stu-id="d96ea-124">Then you can take steps to return the virtual machine to regular communication.</span></span>

<span data-ttu-id="d96ea-125">Bu senaryo, Ağ İzleyicisi'ni ve geçerli bir sanal makine ile bir kaynak grubu mevcut bir örneği olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="d96ea-125">This scenario assumes that you have an existing instance of Network Watcher and a resource group with a valid virtual machine.</span></span>

<span data-ttu-id="d96ea-126">Liste aşağıda gerçekleşir iş akışına genel bir bakış verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="d96ea-126">The following list is an overview of the workflow that takes place:</span></span>

1. <span data-ttu-id="d96ea-127">Bir uyarı, VM tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="d96ea-127">An alert is triggered on your VM.</span></span>
1. <span data-ttu-id="d96ea-128">Uyarı Azure işlevinizi aracılığıyla bir Web kancası çağırır.</span><span class="sxs-lookup"><span data-stu-id="d96ea-128">The alert calls your Azure function via a webhook.</span></span>
1. <span data-ttu-id="d96ea-129">Azure işlevinizi uyarı işler ve bir Ağ İzleyicisi paket yakalama oturumu başlatır.</span><span class="sxs-lookup"><span data-stu-id="d96ea-129">Your Azure function processes the alert and starts a Network Watcher packet capture session.</span></span>
1. <span data-ttu-id="d96ea-130">Paket yakalama VM üzerinde çalışır ve trafik toplar.</span><span class="sxs-lookup"><span data-stu-id="d96ea-130">The packet capture runs on the VM and collects traffic.</span></span>
1. <span data-ttu-id="d96ea-131">Paket yakalama dosyasını gözden geçirin ve tanılama için bir depolama hesabı için yüklenir.</span><span class="sxs-lookup"><span data-stu-id="d96ea-131">The packet capture file is uploaded to a storage account for review and diagnosis.</span></span>

<span data-ttu-id="d96ea-132">Bu işlemi otomatikleştirmek için oluşturun ve bir uyarı olayı meydana geldiğinde tetiklemek için bizim VM bağlanın.</span><span class="sxs-lookup"><span data-stu-id="d96ea-132">To automate this process, we create and connect an alert on our VM to trigger when the incident occurs.</span></span> <span data-ttu-id="d96ea-133">Biz de Ağ İzleyicisi çağırmak için bir işlev oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d96ea-133">We also create a function to call into Network Watcher.</span></span>

<span data-ttu-id="d96ea-134">Bu senaryo şunları yapar:</span><span class="sxs-lookup"><span data-stu-id="d96ea-134">This scenario does the following:</span></span>

* <span data-ttu-id="d96ea-135">Paket yakalama başlatır Azure bir işlev oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d96ea-135">Creates an Azure function that starts a packet capture.</span></span>
* <span data-ttu-id="d96ea-136">Bir sanal makinede bir uyarı kuralı oluşturur ve Azure işlevi çağırmak için uyarı kuralı yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="d96ea-136">Creates an alert rule on a virtual machine and configures the alert rule to call the Azure function.</span></span>

## <a name="create-an-azure-function"></a><span data-ttu-id="d96ea-137">Bir Azure işlevi oluşturma</span><span class="sxs-lookup"><span data-stu-id="d96ea-137">Create an Azure function</span></span>

<span data-ttu-id="d96ea-138">İlk adımı, uyarıyı işlemek ve paket yakalama oluşturmak için bir Azure işlevi oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="d96ea-138">The first step is to create an Azure function to process the alert and create a packet capture.</span></span>

1. <span data-ttu-id="d96ea-139">İçinde [Azure portal](https://portal.azure.com)seçin **yeni** > **işlem** > **işlev uygulaması**.</span><span class="sxs-lookup"><span data-stu-id="d96ea-139">In the [Azure portal](https://portal.azure.com), select **New** > **Compute** > **Function App**.</span></span>

    ![Bir işlev uygulaması oluşturma][1-1]

2. <span data-ttu-id="d96ea-141">Üzerinde **işlev uygulaması** dikey penceresinde, aşağıdaki değerleri girin ve ardından **Tamam** uygulama oluşturmak için:</span><span class="sxs-lookup"><span data-stu-id="d96ea-141">On the **Function App** blade, enter the following values, and then select **OK** to create the app:</span></span>

    |<span data-ttu-id="d96ea-142">**Ayar**</span><span class="sxs-lookup"><span data-stu-id="d96ea-142">**Setting**</span></span> | <span data-ttu-id="d96ea-143">**Değer**</span><span class="sxs-lookup"><span data-stu-id="d96ea-143">**Value**</span></span> | <span data-ttu-id="d96ea-144">**Ayrıntılar**</span><span class="sxs-lookup"><span data-stu-id="d96ea-144">**Details**</span></span> |
    |---|---|---|
    |<span data-ttu-id="d96ea-145">**Uygulama adı**</span><span class="sxs-lookup"><span data-stu-id="d96ea-145">**App name**</span></span>|<span data-ttu-id="d96ea-146">PacketCaptureExample</span><span class="sxs-lookup"><span data-stu-id="d96ea-146">PacketCaptureExample</span></span>|<span data-ttu-id="d96ea-147">İşlev uygulaması adı.</span><span class="sxs-lookup"><span data-stu-id="d96ea-147">The name of the function app.</span></span>|
    |<span data-ttu-id="d96ea-148">**Abonelik**</span><span class="sxs-lookup"><span data-stu-id="d96ea-148">**Subscription**</span></span>|<span data-ttu-id="d96ea-149">[Aboneliğinizi] Abonelik için işlev uygulaması oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="d96ea-149">[Your subscription]The subscription for which to create the function app.</span></span>||
    |<span data-ttu-id="d96ea-150">**Kaynak Grubu**</span><span class="sxs-lookup"><span data-stu-id="d96ea-150">**Resource Group**</span></span>|<span data-ttu-id="d96ea-151">PacketCaptureRG</span><span class="sxs-lookup"><span data-stu-id="d96ea-151">PacketCaptureRG</span></span>|<span data-ttu-id="d96ea-152">İşlev uygulaması içeren kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="d96ea-152">The resource group to contain the function app.</span></span>|
    |<span data-ttu-id="d96ea-153">**Barındırma planı**</span><span class="sxs-lookup"><span data-stu-id="d96ea-153">**Hosting Plan**</span></span>|<span data-ttu-id="d96ea-154">Tüketim planı</span><span class="sxs-lookup"><span data-stu-id="d96ea-154">Consumption Plan</span></span>| <span data-ttu-id="d96ea-155">Türü, işlev uygulaması kullanır planlayın.</span><span class="sxs-lookup"><span data-stu-id="d96ea-155">The type of plan your function app uses.</span></span> <span data-ttu-id="d96ea-156">Seçenekler şunlardır tüketimi veya Azure uygulama hizmeti planı.</span><span class="sxs-lookup"><span data-stu-id="d96ea-156">Options are Consumption or Azure App Service plan.</span></span> |
    |<span data-ttu-id="d96ea-157">**Konum**</span><span class="sxs-lookup"><span data-stu-id="d96ea-157">**Location**</span></span>|<span data-ttu-id="d96ea-158">Orta ABD</span><span class="sxs-lookup"><span data-stu-id="d96ea-158">Central US</span></span>| <span data-ttu-id="d96ea-159">Bölge, işlev uygulaması oluşturmak kullanın.</span><span class="sxs-lookup"><span data-stu-id="d96ea-159">The region in which to create the function app.</span></span>|
    |<span data-ttu-id="d96ea-160">**Depolama hesabı**</span><span class="sxs-lookup"><span data-stu-id="d96ea-160">**Storage Account**</span></span>|<span data-ttu-id="d96ea-161">{otomatik olarak oluşturulur}</span><span class="sxs-lookup"><span data-stu-id="d96ea-161">{autogenerated}</span></span>| <span data-ttu-id="d96ea-162">Azure işlevleri için genel amaçlı depolama alanı ihtiyaçlarınızı depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="d96ea-162">The storage account that Azure Functions needs for general-purpose storage.</span></span>|

3. <span data-ttu-id="d96ea-163">Üzerinde **PacketCaptureExample işlev uygulamalarının** dikey penceresinde, select **işlevleri** > **özel işlevi**  >  **+**.</span><span class="sxs-lookup"><span data-stu-id="d96ea-163">On the **PacketCaptureExample Function Apps** blade, select **Functions** > **Custom function** >**+**.</span></span>

4. <span data-ttu-id="d96ea-164">Seçin **HttpTrigger Powershell**ve ardından kalan bilgileri girin.</span><span class="sxs-lookup"><span data-stu-id="d96ea-164">Select **HttpTrigger-Powershell**, and then enter the remaining information.</span></span> <span data-ttu-id="d96ea-165">Son olarak, işlev oluşturmak için seçin **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="d96ea-165">Finally, to create the function, select **Create**.</span></span>

    |<span data-ttu-id="d96ea-166">**Ayar**</span><span class="sxs-lookup"><span data-stu-id="d96ea-166">**Setting**</span></span> | <span data-ttu-id="d96ea-167">**Değer**</span><span class="sxs-lookup"><span data-stu-id="d96ea-167">**Value**</span></span> | <span data-ttu-id="d96ea-168">**Ayrıntılar**</span><span class="sxs-lookup"><span data-stu-id="d96ea-168">**Details**</span></span> |
    |---|---|---|
    |<span data-ttu-id="d96ea-169">**Senaryo**</span><span class="sxs-lookup"><span data-stu-id="d96ea-169">**Scenario**</span></span>|<span data-ttu-id="d96ea-170">Deneysel</span><span class="sxs-lookup"><span data-stu-id="d96ea-170">Experimental</span></span>|<span data-ttu-id="d96ea-171">Tür senaryosu</span><span class="sxs-lookup"><span data-stu-id="d96ea-171">Type of scenario</span></span>|
    |<span data-ttu-id="d96ea-172">**İşlevinizi adlandırın**</span><span class="sxs-lookup"><span data-stu-id="d96ea-172">**Name your function**</span></span>|<span data-ttu-id="d96ea-173">AlertPacketCapturePowerShell</span><span class="sxs-lookup"><span data-stu-id="d96ea-173">AlertPacketCapturePowerShell</span></span>|<span data-ttu-id="d96ea-174">İşlevin adı</span><span class="sxs-lookup"><span data-stu-id="d96ea-174">Name of the function</span></span>|
    |<span data-ttu-id="d96ea-175">**Yetkilendirme düzeyi**</span><span class="sxs-lookup"><span data-stu-id="d96ea-175">**Authorization level**</span></span>|<span data-ttu-id="d96ea-176">İşlevi</span><span class="sxs-lookup"><span data-stu-id="d96ea-176">Function</span></span>|<span data-ttu-id="d96ea-177">Yetki düzeyini işlevi</span><span class="sxs-lookup"><span data-stu-id="d96ea-177">Authorization level for the function</span></span>|

![İşlevleri örneği][functions1]

> [!NOTE]
> <span data-ttu-id="d96ea-179">PowerShell şablon Deneysel ve tam desteğine sahip değil.</span><span class="sxs-lookup"><span data-stu-id="d96ea-179">The PowerShell template is experimental and does not have full support.</span></span>

<span data-ttu-id="d96ea-180">Özelleştirmeleri bu örnek için gereklidir ve aşağıdaki adımlarda açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="d96ea-180">Customizations are required for this example and are explained in the following steps.</span></span>

### <a name="add-modules"></a><span data-ttu-id="d96ea-181">Modüller ekleme</span><span class="sxs-lookup"><span data-stu-id="d96ea-181">Add modules</span></span>

<span data-ttu-id="d96ea-182">Ağ İzleyicisi PowerShell cmdlet'lerini kullanmak için işlev uygulaması son PowerShell modülünü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="d96ea-182">To use Network Watcher PowerShell cmdlets, upload the latest PowerShell module to the function app.</span></span>

1. <span data-ttu-id="d96ea-183">Yerel makinenizde yüklü en son Azure PowerShell modülleri ile aşağıdaki PowerShell komutunu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="d96ea-183">On your local machine with the latest Azure PowerShell modules installed, run the following PowerShell command:</span></span>

    ```powershell
    (Get-Module AzureRM.Network).Path
    ```

    <span data-ttu-id="d96ea-184">Bu örnek, Azure PowerShell modüllerinizi yerel yolunu sağlar.</span><span class="sxs-lookup"><span data-stu-id="d96ea-184">This example gives you the local path of your Azure PowerShell modules.</span></span> <span data-ttu-id="d96ea-185">Bu klasörler, bir sonraki adımda kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d96ea-185">These folders are used in a later step.</span></span> <span data-ttu-id="d96ea-186">Bu senaryoda kullanılan modülleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="d96ea-186">The modules that are used in this scenario are:</span></span>

    * <span data-ttu-id="d96ea-187">AzureRM.Network</span><span class="sxs-lookup"><span data-stu-id="d96ea-187">AzureRM.Network</span></span>

    * <span data-ttu-id="d96ea-188">AzureRM.Profile</span><span class="sxs-lookup"><span data-stu-id="d96ea-188">AzureRM.Profile</span></span>

    * <span data-ttu-id="d96ea-189">AzureRM.Resources</span><span class="sxs-lookup"><span data-stu-id="d96ea-189">AzureRM.Resources</span></span>

    ![PowerShell klasörleri][functions5]

1. <span data-ttu-id="d96ea-191">Seçin **işlev uygulaması ayarları** > **App Service Düzenleyici'ye gidin**.</span><span class="sxs-lookup"><span data-stu-id="d96ea-191">Select **Function app settings** > **Go to App Service Editor**.</span></span>

    ![İşlev uygulama ayarları][functions2]

1. <span data-ttu-id="d96ea-193">Sağ **AlertPacketCapturePowershell** klasörünü ve ardından adlı bir klasör oluşturun **azuremodules**.</span><span class="sxs-lookup"><span data-stu-id="d96ea-193">Right-click the **AlertPacketCapturePowershell** folder, and then create a folder called **azuremodules**.</span></span> 

4. <span data-ttu-id="d96ea-194">Gereksinim duyduğunuz her modül için bir alt klasör oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d96ea-194">Create a subfolder for each module that you need.</span></span>

    ![Klasör ve alt klasörleri][functions3]

    * <span data-ttu-id="d96ea-196">AzureRM.Network</span><span class="sxs-lookup"><span data-stu-id="d96ea-196">AzureRM.Network</span></span>

    * <span data-ttu-id="d96ea-197">AzureRM.Profile</span><span class="sxs-lookup"><span data-stu-id="d96ea-197">AzureRM.Profile</span></span>

    * <span data-ttu-id="d96ea-198">AzureRM.Resources</span><span class="sxs-lookup"><span data-stu-id="d96ea-198">AzureRM.Resources</span></span>

1. <span data-ttu-id="d96ea-199">Sağ **AzureRM.Network** alt ve ardından **dosya yükleme**.</span><span class="sxs-lookup"><span data-stu-id="d96ea-199">Right-click the **AzureRM.Network** subfolder, and then select **Upload Files**.</span></span> 

6. <span data-ttu-id="d96ea-200">Azure modüllerinizi gidin.</span><span class="sxs-lookup"><span data-stu-id="d96ea-200">Go to your Azure modules.</span></span> <span data-ttu-id="d96ea-201">Yerel **AzureRM.Network** klasörü, klasördeki tüm dosyaları seçin.</span><span class="sxs-lookup"><span data-stu-id="d96ea-201">In the local **AzureRM.Network** folder, select all the files in the folder.</span></span> <span data-ttu-id="d96ea-202">Ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="d96ea-202">Then select **OK**.</span></span> 

7. <span data-ttu-id="d96ea-203">İçin bu adımları yineleyin **AzureRM.Profile** ve **AzureRM.Resources**.</span><span class="sxs-lookup"><span data-stu-id="d96ea-203">Repeat these steps for **AzureRM.Profile** and **AzureRM.Resources**.</span></span>

    ![Dosyaları karşıya yükleme][functions6]

1. <span data-ttu-id="d96ea-205">Tamamlandı sonra her klasör, yerel makinenize PowerShell modülü dosyalarından olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d96ea-205">After you've finished, each folder should have the PowerShell module files from your local machine.</span></span>

    ![PowerShell dosyaları][functions7]

### <a name="authentication"></a><span data-ttu-id="d96ea-207">Kimlik Doğrulaması</span><span class="sxs-lookup"><span data-stu-id="d96ea-207">Authentication</span></span>

<span data-ttu-id="d96ea-208">PowerShell cmdlet'lerini kullanmak için kimlik doğrulaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d96ea-208">To use the PowerShell cmdlets, you must authenticate.</span></span> <span data-ttu-id="d96ea-209">İşlev uygulamasında kimlik doğrulamasını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="d96ea-209">You configure authentication in the function app.</span></span> <span data-ttu-id="d96ea-210">Kimlik doğrulamasını yapılandırmak için ortam değişkenleri yapılandırmanız ve şifreli bir anahtar dosyası işlevi uygulamaya karşıya gerekir.</span><span class="sxs-lookup"><span data-stu-id="d96ea-210">To configure authentication, you must configure environment variables and upload an encrypted key file to the function app.</span></span>

> [!NOTE]
> <span data-ttu-id="d96ea-211">Bu senaryo, nasıl Azure işlevleri ile kimlik doğrulaması uygulamak yalnızca bir örnek sağlar.</span><span class="sxs-lookup"><span data-stu-id="d96ea-211">This scenario provides just one example of how to implement authentication with Azure Functions.</span></span> <span data-ttu-id="d96ea-212">Bunu yapmak için başka yolları vardır.</span><span class="sxs-lookup"><span data-stu-id="d96ea-212">There are other ways to do this.</span></span>

#### <a name="encrypted-credentials"></a><span data-ttu-id="d96ea-213">Şifrelenmiş kimlik bilgileri</span><span class="sxs-lookup"><span data-stu-id="d96ea-213">Encrypted credentials</span></span>

<span data-ttu-id="d96ea-214">Aşağıdaki PowerShell betiğini adlı bir anahtar dosyası oluşturur **PassEncryptKey.key**.</span><span class="sxs-lookup"><span data-stu-id="d96ea-214">The following PowerShell script creates a key file called **PassEncryptKey.key**.</span></span> <span data-ttu-id="d96ea-215">Sağlanan parola şifreli sürümünü de sağlar.</span><span class="sxs-lookup"><span data-stu-id="d96ea-215">It also provides an encrypted version of the password that's supplied.</span></span> <span data-ttu-id="d96ea-216">Bu parola kimlik doğrulaması için kullanılan Azure Active Directory uygulaması için tanımlanan aynı paroladır.</span><span class="sxs-lookup"><span data-stu-id="d96ea-216">This password is the same password that is defined for the Azure Active Directory application that's used for authentication.</span></span>

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

<span data-ttu-id="d96ea-217">Uygulama hizmeti Düzenleyicisi'nde işlevi uygulamanın adlı bir klasör oluşturun **anahtarları** altında **AlertPacketCapturePowerShell**.</span><span class="sxs-lookup"><span data-stu-id="d96ea-217">In the App Service Editor of the function app, create a folder called **keys** under **AlertPacketCapturePowerShell**.</span></span> <span data-ttu-id="d96ea-218">Ardından karşıya **PassEncryptKey.key** önceki PowerShell örneğinde oluşturulan dosyası.</span><span class="sxs-lookup"><span data-stu-id="d96ea-218">Then upload the **PassEncryptKey.key** file that you created in the previous PowerShell sample.</span></span>

![İşlevler anahtarı][functions8]

### <a name="retrieve-values-for-environment-variables"></a><span data-ttu-id="d96ea-220">Ortam değişkenleri için değerleri alma</span><span class="sxs-lookup"><span data-stu-id="d96ea-220">Retrieve values for environment variables</span></span>

<span data-ttu-id="d96ea-221">Son kimlik doğrulaması için değerlerine erişmek için gerekli olan ortam değişkenleri ayarlamak için gereksinimdir.</span><span class="sxs-lookup"><span data-stu-id="d96ea-221">The final requirement is to set up the environment variables that are necessary to access the values for authentication.</span></span> <span data-ttu-id="d96ea-222">Aşağıdaki liste, oluşturulan ortam değişkenleri gösterir:</span><span class="sxs-lookup"><span data-stu-id="d96ea-222">The following list shows the environment variables that are created:</span></span>

* <span data-ttu-id="d96ea-223">AzureClientID</span><span class="sxs-lookup"><span data-stu-id="d96ea-223">AzureClientID</span></span>

* <span data-ttu-id="d96ea-224">AzureTenant</span><span class="sxs-lookup"><span data-stu-id="d96ea-224">AzureTenant</span></span>

* <span data-ttu-id="d96ea-225">AzureCredPassword</span><span class="sxs-lookup"><span data-stu-id="d96ea-225">AzureCredPassword</span></span>


#### <a name="azureclientid"></a><span data-ttu-id="d96ea-226">AzureClientID</span><span class="sxs-lookup"><span data-stu-id="d96ea-226">AzureClientID</span></span>

<span data-ttu-id="d96ea-227">İstemci kimliği Azure Active Directory'de bir uygulamanın uygulama Kimliğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="d96ea-227">The client ID is the Application ID of an application in Azure Active Directory.</span></span>

1. <span data-ttu-id="d96ea-228">Kullanmak için bir uygulama zaten yoksa, bir uygulama oluşturmak için aşağıdaki örneği çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="d96ea-228">If you don't already have an application to use, run the following example to create an application.</span></span>

    ```powershell
    $app = New-AzureRmADApplication -DisplayName "ExampleAutomationAccount_MF" -HomePage "https://exampleapp.com" -IdentifierUris "https://exampleapp1.com/ExampleFunctionsAccount" -Password "<same password as defined earlier>"
    New-AzureRmADServicePrincipal -ApplicationId $app.ApplicationId
    Start-Sleep 15
    New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $app.ApplicationId
    ```

   > [!NOTE]
   > <span data-ttu-id="d96ea-229">Uygulama oluştururken kullandığınız parolayı anahtar dosyası kaydedilirken daha önce oluşturduğunuz aynı parola olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d96ea-229">The password that you use when creating the application should be the same password that you created earlier when saving the key file.</span></span>

1. <span data-ttu-id="d96ea-230">Azure portalında seçin **abonelikleri**.</span><span class="sxs-lookup"><span data-stu-id="d96ea-230">In the Azure portal, select **Subscriptions**.</span></span> <span data-ttu-id="d96ea-231">Abonelik kullanın ve ardından seçmek için Seç **erişim denetimi (IAM)**.</span><span class="sxs-lookup"><span data-stu-id="d96ea-231">Select the subscription to use, and then select **Access control (IAM)**.</span></span>

    ![İşlevler IAM][functions9]

1. <span data-ttu-id="d96ea-233">Kullanın ve ardından için hesabı seçin **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="d96ea-233">Choose the account to use, and then select **Properties**.</span></span> <span data-ttu-id="d96ea-234">Uygulama Kimliği kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="d96ea-234">Copy the Application ID.</span></span>

    ![İşlevleri uygulama kimliği][functions10]

#### <a name="azuretenant"></a><span data-ttu-id="d96ea-236">AzureTenant</span><span class="sxs-lookup"><span data-stu-id="d96ea-236">AzureTenant</span></span>

<span data-ttu-id="d96ea-237">Aşağıdaki PowerShell örnek çalıştırarak Kiracı kimliği alın:</span><span class="sxs-lookup"><span data-stu-id="d96ea-237">Obtain the tenant ID  by running the following PowerShell sample:</span></span>

```powershell
(Get-AzureRmSubscription -SubscriptionName "<subscriptionName>").TenantId
```

#### <a name="azurecredpassword"></a><span data-ttu-id="d96ea-238">AzureCredPassword</span><span class="sxs-lookup"><span data-stu-id="d96ea-238">AzureCredPassword</span></span>

<span data-ttu-id="d96ea-239">AzureCredPassword ortam değişkeni aşağıdaki PowerShell örneğini çalıştıran alma değer değeridir.</span><span class="sxs-lookup"><span data-stu-id="d96ea-239">The value of the AzureCredPassword environment variable is the value that you get from running the following PowerShell sample.</span></span> <span data-ttu-id="d96ea-240">Bu örnek bir önceki gösterilen aynıdır **şifrelenmiş kimlik bilgileri** bölümü.</span><span class="sxs-lookup"><span data-stu-id="d96ea-240">This example is the same one that's shown in the preceding **Encrypted credentials** section.</span></span> <span data-ttu-id="d96ea-241">Gerekli olan çıktısını değerdir `$Encryptedpassword` değişkeni.</span><span class="sxs-lookup"><span data-stu-id="d96ea-241">The value that's needed is the output of the `$Encryptedpassword` variable.</span></span>  <span data-ttu-id="d96ea-242">PowerShell Betiği kullanılarak şifrelenmiş hizmet asıl parolası budur.</span><span class="sxs-lookup"><span data-stu-id="d96ea-242">This is the service principal password that you encrypted by using the PowerShell script.</span></span>

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

### <a name="store-the-environment-variables"></a><span data-ttu-id="d96ea-243">Ortam değişkenleri depolama</span><span class="sxs-lookup"><span data-stu-id="d96ea-243">Store the environment variables</span></span>

1. <span data-ttu-id="d96ea-244">İşlev uygulamasına gidin.</span><span class="sxs-lookup"><span data-stu-id="d96ea-244">Go to the function app.</span></span> <span data-ttu-id="d96ea-245">Ardından **işlev uygulaması ayarları** > **uygulaması ayarlarını yapılandır**.</span><span class="sxs-lookup"><span data-stu-id="d96ea-245">Then select **Function app settings** > **Configure app settings**.</span></span>

    ![Uygulama ayarlarını yapılandırma][functions11]

1. <span data-ttu-id="d96ea-247">Ortam değişkenlerini ve değerleri için uygulama ayarları ekleyin ve ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="d96ea-247">Add the environment variables and their values to the app settings, and then select **Save**.</span></span>

    ![Uygulama ayarları][functions12]

### <a name="add-powershell-to-the-function"></a><span data-ttu-id="d96ea-249">PowerShell işlevine ekleyin</span><span class="sxs-lookup"><span data-stu-id="d96ea-249">Add PowerShell to the function</span></span>

<span data-ttu-id="d96ea-250">Bu Ağ İzleyicisi ' çağrılarını Azure işlevi içinde olmak üzere sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="d96ea-250">It's now time to make calls into Network Watcher from within the Azure function.</span></span> <span data-ttu-id="d96ea-251">Bu işlev uygulaması gereksinimlerine bağlı olarak değişebilir.</span><span class="sxs-lookup"><span data-stu-id="d96ea-251">Depending on the requirements, the implementation of this function can vary.</span></span> <span data-ttu-id="d96ea-252">Ancak, genel akış kod aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="d96ea-252">However, the general flow of the code is as follows:</span></span>

1. <span data-ttu-id="d96ea-253">İşlem giriş parametreleri.</span><span class="sxs-lookup"><span data-stu-id="d96ea-253">Process input parameters.</span></span>
2. <span data-ttu-id="d96ea-254">Sınırlarını doğrulayın ve ad çakışmalarını çözmek için sorgu varolan paket yakalar.</span><span class="sxs-lookup"><span data-stu-id="d96ea-254">Query existing packet captures to verify limits and resolve name conflicts.</span></span>
3. <span data-ttu-id="d96ea-255">Paket yakalama uygun parametrelerle oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d96ea-255">Create a packet capture with appropriate parameters.</span></span>
4. <span data-ttu-id="d96ea-256">Yoklama paket düzenli aralıklarla tamamlanana kadar yakalayın.</span><span class="sxs-lookup"><span data-stu-id="d96ea-256">Poll packet capture periodically until it's complete.</span></span>
5. <span data-ttu-id="d96ea-257">Paket yakalama oturumu tamamlandıktan kullanıcıya bildir.</span><span class="sxs-lookup"><span data-stu-id="d96ea-257">Notify the user that the packet capture session is complete.</span></span>

<span data-ttu-id="d96ea-258">Aşağıdaki örnek, işlevde kullanılabilmesi için PowerShell koddur.</span><span class="sxs-lookup"><span data-stu-id="d96ea-258">The following example is PowerShell code that can be used in the function.</span></span> <span data-ttu-id="d96ea-259">İçin değiştirilmesi gereken değerler **Subscriptionıd**, **resourceGroupName**, ve **storageAccountName**.</span><span class="sxs-lookup"><span data-stu-id="d96ea-259">There are values that need to be replaced for **subscriptionId**, **resourceGroupName**, and **storageAccountName**.</span></span>

```powershell
            #Import Azure PowerShell modules required to make calls to Network Watcher
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Profile\AzureRM.Profile.psd1" -Global
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Network\AzureRM.Network.psd1" -Global
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Resources\AzureRM.Resources.psd1" -Global

            #Process alert request body
            $requestBody = Get-Content $req -Raw | ConvertFrom-Json

            #Storage account ID to save captures in
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


            #Get the VM that fired the alert
            if($requestBody.context.resourceType -eq "Microsoft.Compute/virtualMachines")
            {
                Write-Output ("Subscription ID: {0}" -f $requestBody.context.subscriptionId)
                Write-Output ("Resource Group:  {0}" -f $requestBody.context.resourceGroupName)
                Write-Output ("Resource Name:  {0}" -f $requestBody.context.resourceName)
                Write-Output ("Resource Type:  {0}" -f $requestBody.context.resourceType)

                #Get the Network Watcher in the VM's region
                $nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $requestBody.context.resourceRegion}
                $networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

                #Get existing packetCaptures
                $packetCaptures = Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher

                #Remove existing packet capture created by the function (if it exists)
                $packetCaptures | %{if($_.Name -eq $packetCaptureName)
                { 
                    Remove-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName $packetCaptureName
                }}

                #Initiate packet capture on the VM that fired the alert
                if ((Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher).Count -lt $packetCaptureLimit){
                    echo "Initiating Packet Capture"
                    New-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -TargetVirtualMachineId $requestBody.context.resourceId -PacketCaptureName $packetCaptureName -StorageAccountId $storageaccountid -TimeLimitInSeconds $packetCaptureDuration
                    Out-File -Encoding Ascii -FilePath $res -inputObject "Packet Capture created on ${requestBody.context.resourceID}"
                }
            } 
 ``` 
#### <a name="retrieve-the-function-url"></a><span data-ttu-id="d96ea-260">İşlev URL'sini alın</span><span class="sxs-lookup"><span data-stu-id="d96ea-260">Retrieve the function URL</span></span> 
1. <span data-ttu-id="d96ea-261">İşlevinizi oluşturduktan sonra işlev ile ilişkili URL çağırmak için uyarıyı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="d96ea-261">After you've created your function, configure your alert to call the URL that's associated with the function.</span></span> <span data-ttu-id="d96ea-262">Bu değer almak için işlevi uygulamanızdan işlevi URL'sini kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="d96ea-262">To get this value, copy the function URL from your function app.</span></span>

    ![İşlev URL bulma][functions13]

2. <span data-ttu-id="d96ea-264">İşlev uygulamanız için işlevi URL'sini kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="d96ea-264">Copy the function URL for your function app.</span></span>

    ![İşlev URL kopyalanması][2]

<span data-ttu-id="d96ea-266">Web kancası POST isteği yükte özel özellikler gerektiriyorsa, başvurmak [bir Web kancası Azure ölçüm uyarıyı yapılandırmak](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="d96ea-266">If you require custom properties in the payload of the webhook POST request, refer to [Configure a webhook on an Azure metric alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span>

## <a name="configure-an-alert-on-a-vm"></a><span data-ttu-id="d96ea-267">Bir VM üzerinde bir uyarı yapılandırmak</span><span class="sxs-lookup"><span data-stu-id="d96ea-267">Configure an alert on a VM</span></span>

<span data-ttu-id="d96ea-268">Uyarıları, belirli bir ölçüyü kendisine atanmış bir eşik kestiği kişilere bildirmek için yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="d96ea-268">Alerts can be configured to notify individuals when a specific metric crosses a threshold that's assigned to it.</span></span> <span data-ttu-id="d96ea-269">Bu örnekte, gönderilen TCP kesimlerinde uyarısıdır, ancak uyarı için birçok diğer ölçümleri tetiklenebilir.</span><span class="sxs-lookup"><span data-stu-id="d96ea-269">In this example, the alert is on the TCP segments that are sent, but the alert can be triggered for many other metrics.</span></span> <span data-ttu-id="d96ea-270">Bu örnekte, bir uyarı işlevi çağırmak için bir Web kancası çağırmak için yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="d96ea-270">In this example, an alert is configured to call a webhook to call the function.</span></span>

### <a name="create-the-alert-rule"></a><span data-ttu-id="d96ea-271">Uyarı kuralı oluştur</span><span class="sxs-lookup"><span data-stu-id="d96ea-271">Create the alert rule</span></span>

<span data-ttu-id="d96ea-272">Varolan bir sanal makineye gidin ve ardından bir uyarı kuralı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d96ea-272">Go to an existing virtual machine, and then add an alert rule.</span></span> <span data-ttu-id="d96ea-273">Uyarıları yapılandırma hakkında daha ayrıntılı belgeler bulunabilir [oluşturma uyarıları Azure İzleyicisi'nde için Azure services - Azure portalında](../monitoring-and-diagnostics/insights-alerts-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d96ea-273">More detailed documentation about configuring alerts can be found at [Create alerts in Azure Monitor for Azure services - Azure portal](../monitoring-and-diagnostics/insights-alerts-portal.md).</span></span> <span data-ttu-id="d96ea-274">Aşağıdaki değerleri girin **uyarı kuralı** dikey ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="d96ea-274">Enter the following values in the **Alert rule** blade, and then select **OK**.</span></span>

  |<span data-ttu-id="d96ea-275">**Ayar**</span><span class="sxs-lookup"><span data-stu-id="d96ea-275">**Setting**</span></span> | <span data-ttu-id="d96ea-276">**Değer**</span><span class="sxs-lookup"><span data-stu-id="d96ea-276">**Value**</span></span> | <span data-ttu-id="d96ea-277">**Ayrıntılar**</span><span class="sxs-lookup"><span data-stu-id="d96ea-277">**Details**</span></span> |
  |---|---|---|
  |<span data-ttu-id="d96ea-278">**Ad**</span><span class="sxs-lookup"><span data-stu-id="d96ea-278">**Name**</span></span>|<span data-ttu-id="d96ea-279">TCP_Segments_Sent_Exceeded</span><span class="sxs-lookup"><span data-stu-id="d96ea-279">TCP_Segments_Sent_Exceeded</span></span>|<span data-ttu-id="d96ea-280">Uyarı kuralı adı.</span><span class="sxs-lookup"><span data-stu-id="d96ea-280">Name of the alert rule.</span></span>|
  |<span data-ttu-id="d96ea-281">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="d96ea-281">**Description**</span></span>|<span data-ttu-id="d96ea-282">TCP kesimini aşıldı eşik gönderilen</span><span class="sxs-lookup"><span data-stu-id="d96ea-282">TCP segments sent exceeded threshold</span></span>|<span data-ttu-id="d96ea-283">Uyarı kuralı açıklaması.</span><span class="sxs-lookup"><span data-stu-id="d96ea-283">The description for the alert rule.</span></span>||
  |<span data-ttu-id="d96ea-284">**Ölçüm**</span><span class="sxs-lookup"><span data-stu-id="d96ea-284">**Metric**</span></span>|<span data-ttu-id="d96ea-285">Gönderilen TCP kesimleri</span><span class="sxs-lookup"><span data-stu-id="d96ea-285">TCP segments sent</span></span>| <span data-ttu-id="d96ea-286">Uyarı tetiklemek için kullanılacak ölçüm.</span><span class="sxs-lookup"><span data-stu-id="d96ea-286">The metric to use to trigger the alert.</span></span> |
  |<span data-ttu-id="d96ea-287">**Koşul**</span><span class="sxs-lookup"><span data-stu-id="d96ea-287">**Condition**</span></span>|<span data-ttu-id="d96ea-288">Şu değerden fazla:</span><span class="sxs-lookup"><span data-stu-id="d96ea-288">Greater than</span></span>| <span data-ttu-id="d96ea-289">Ölçüm hesaplanırken kullanılacak koşulu.</span><span class="sxs-lookup"><span data-stu-id="d96ea-289">The condition to use when evaluating the metric.</span></span>|
  |<span data-ttu-id="d96ea-290">**Eşik**</span><span class="sxs-lookup"><span data-stu-id="d96ea-290">**Threshold**</span></span>|<span data-ttu-id="d96ea-291">100</span><span class="sxs-lookup"><span data-stu-id="d96ea-291">100</span></span>| <span data-ttu-id="d96ea-292">Uyarıyı tetikleyen ölçüm değeri.</span><span class="sxs-lookup"><span data-stu-id="d96ea-292">The  value of the metric that triggers the alert.</span></span> <span data-ttu-id="d96ea-293">Bu değer, ortamınız için geçerli bir değere ayarlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d96ea-293">This value should be set to a valid value for your environment.</span></span>|
  |<span data-ttu-id="d96ea-294">**Süresi**</span><span class="sxs-lookup"><span data-stu-id="d96ea-294">**Period**</span></span>|<span data-ttu-id="d96ea-295">Son beş dakika boyunca</span><span class="sxs-lookup"><span data-stu-id="d96ea-295">Over the last five minutes</span></span>| <span data-ttu-id="d96ea-296">Ölçüm eşiğine arayın olduğu süreyi belirler.</span><span class="sxs-lookup"><span data-stu-id="d96ea-296">Determines the period in which to look for the threshold on the metric.</span></span>|
  |<span data-ttu-id="d96ea-297">**Web kancası**</span><span class="sxs-lookup"><span data-stu-id="d96ea-297">**Webhook**</span></span>|<span data-ttu-id="d96ea-298">[işlev uygulaması URL'SİNDEN Web kancası]</span><span class="sxs-lookup"><span data-stu-id="d96ea-298">[webhook URL from function app]</span></span>| <span data-ttu-id="d96ea-299">Önceki adımlarda oluşturulan işlevi uygulamasından Web kancası URL'si.</span><span class="sxs-lookup"><span data-stu-id="d96ea-299">The webhook URL from the function app that was created in the previous steps.</span></span>|

> [!NOTE]
> <span data-ttu-id="d96ea-300">TCP kesimleri ölçümü varsayılan olarak etkin değildir.</span><span class="sxs-lookup"><span data-stu-id="d96ea-300">The TCP segments metric is not enabled by default.</span></span> <span data-ttu-id="d96ea-301">Ek ölçümler ziyaret ederek etkinleştirme hakkında daha fazla bilgi edinin [izleme ve tanılama](../monitoring-and-diagnostics/insights-how-to-use-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="d96ea-301">Learn more about how to enable additional metrics by visiting [Enable monitoring and diagnostics](../monitoring-and-diagnostics/insights-how-to-use-diagnostics.md).</span></span>

## <a name="review-the-results"></a><span data-ttu-id="d96ea-302">Sonuçları gözden geçirin</span><span class="sxs-lookup"><span data-stu-id="d96ea-302">Review the results</span></span>

<span data-ttu-id="d96ea-303">Uyarı Tetikleyicileri ölçütlerine sonra bir paket yakalama oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="d96ea-303">After the criteria for the alert triggers, a packet capture is created.</span></span> <span data-ttu-id="d96ea-304">Ağ İzleyicisi gidin ve ardından **paket yakalama**.</span><span class="sxs-lookup"><span data-stu-id="d96ea-304">Go to Network Watcher, and then select **Packet capture**.</span></span> <span data-ttu-id="d96ea-305">Bu sayfada, paket yakalama indirmek için paket yakalama dosyası bağlantısı seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d96ea-305">On this page, you can select the packet capture file link to download the packet capture.</span></span>

![Görünüm paket yakalama][functions14]

<span data-ttu-id="d96ea-307">Yakalama dosyası yerel olarak depolanıyorsa, sanal makineye oturum açarak alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d96ea-307">If the capture file is stored locally, you can retrieve it by signing in to the virtual machine.</span></span>

<span data-ttu-id="d96ea-308">Azure depolama hesaplarından dosyalarını yükleme hakkında yönergeler için bkz: [.NET kullanarak Azure Blob storage'ı kullanmaya başlama](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="d96ea-308">For instructions about downloading files from Azure storage accounts, see [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="d96ea-309">Kullanabileceğiniz başka bir araçtır [Depolama Gezgini](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="d96ea-309">Another tool you can use is [Storage Explorer](http://storageexplorer.com/).</span></span>

<span data-ttu-id="d96ea-310">Yakalama yüklendikten sonra okuyabilir herhangi bir aracı kullanarak görüntüleyebilirsiniz bir **.cap** dosya.</span><span class="sxs-lookup"><span data-stu-id="d96ea-310">After your capture has been downloaded, you can view it by using any tool that can read a **.cap** file.</span></span> <span data-ttu-id="d96ea-311">Aşağıdaki iki bu araçların bağlantıları verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="d96ea-311">Following are links to two of these tools:</span></span>

- [<span data-ttu-id="d96ea-312">Microsoft Message Analyzer</span><span class="sxs-lookup"><span data-stu-id="d96ea-312">Microsoft Message Analyzer</span></span>](https://technet.microsoft.com/library/jj649776.aspx)
- [<span data-ttu-id="d96ea-313">WireShark</span><span class="sxs-lookup"><span data-stu-id="d96ea-313">WireShark</span></span>](https://www.wireshark.org/)

## <a name="next-steps"></a><span data-ttu-id="d96ea-314">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d96ea-314">Next steps</span></span>

<span data-ttu-id="d96ea-315">Paket yakalama ziyaret ederek görüntülemeyi öğrenin [paket yakalama çözümlemesini Wireshark ile](network-watcher-deep-packet-inspection.md).</span><span class="sxs-lookup"><span data-stu-id="d96ea-315">Learn how to view your packet captures by visiting [Packet capture analysis with Wireshark](network-watcher-deep-packet-inspection.md).</span></span>


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
