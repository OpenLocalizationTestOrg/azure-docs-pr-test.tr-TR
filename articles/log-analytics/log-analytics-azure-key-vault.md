---
title: "Günlük analizi anahtar kasası çözümde aaaAzure | Microsoft Docs"
description: "Azure anahtar kasası günlükleri günlük analizi tooreview içinde hello Azure anahtar kasası çözüm kullanabilirsiniz."
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: jochan
editor: 
ms.assetid: 5e25e6d6-dd20-4528-9820-6e2958a40dae
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: richrund
ms.openlocfilehash: 1c6eae26ded7ad55b0159a3be09cdc9901596298
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-analytics-solution-in-log-analytics"></a><span data-ttu-id="c88cc-103">Günlük analizi Azure anahtar kasası Analytics çözümde</span><span class="sxs-lookup"><span data-stu-id="c88cc-103">Azure Key Vault Analytics solution in Log Analytics</span></span>

![Anahtar kasası simgesi](./media/log-analytics-azure-keyvault/key-vault-analytics-symbol.png)

<span data-ttu-id="c88cc-105">Azure anahtar kasası AuditEvent günlüklerini günlük analizi tooreview içinde hello Azure anahtar kasası çözüm kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c88cc-105">You can use hello Azure Key Vault solution in Log Analytics tooreview Azure Key Vault AuditEvent logs.</span></span>

<span data-ttu-id="c88cc-106">toouse hello çözüm tooenable günlüğü Azure anahtar kasası tanılama ve doğrudan hello tanılama tooa günlük analizi çalışma alanı gerekir.</span><span class="sxs-lookup"><span data-stu-id="c88cc-106">toouse hello solution, you need tooenable logging of Azure Key Vault diagnostics and direct hello diagnostics tooa Log Analytics workspace.</span></span> <span data-ttu-id="c88cc-107">Gerekli toowrite hello günlükleri tooAzure Blob Depolama olmadığı.</span><span class="sxs-lookup"><span data-stu-id="c88cc-107">It is not necessary toowrite hello logs tooAzure Blob storage.</span></span>

> [!NOTE]
> <span data-ttu-id="c88cc-108">Ocak 2017 ' Analytics değiştirilen anahtar kasası tooLog günlükleri gönderme şekilde hello desteklenir.</span><span class="sxs-lookup"><span data-stu-id="c88cc-108">In January 2017, hello supported way of sending logs from Key Vault tooLog Analytics changed.</span></span> <span data-ttu-id="c88cc-109">Merhaba anahtar kasası çözümü kullanıyorsanız gösterir *(kullanım dışı)* hello başlığında çok başvurun[hello eski anahtar kasası çözüm'den geçiş](#migrating-from-the-old-key-vault-solution) adımları toofollow gerekir.</span><span class="sxs-lookup"><span data-stu-id="c88cc-109">If hello Key Vault solution you are using shows *(deprecated)* in hello title, refer too[migrating from hello old Key Vault solution](#migrating-from-the-old-key-vault-solution) for steps you need toofollow.</span></span>
>
>

## <a name="install-and-configure-hello-solution"></a><span data-ttu-id="c88cc-110">Yükleme ve yapılandırma hello çözümü</span><span class="sxs-lookup"><span data-stu-id="c88cc-110">Install and configure hello solution</span></span>
<span data-ttu-id="c88cc-111">Aşağıdaki yönergeler tooinstall hello kullanın ve hello Azure anahtar kasası çözüm yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="c88cc-111">Use hello following instructions tooinstall and configure hello Azure Key Vault solution:</span></span>

1. <span data-ttu-id="c88cc-112">Hello Azure anahtar kasası çözümden etkinleştirmek [Azure Market](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.KeyVaultAnalyticsOMS?tab=Overview) veya açıklanan hello işlemi kullanarak [hello Çözümleri Galerisi eklemek günlük analizi çözümleri](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="c88cc-112">Enable hello Azure Key Vault solution from [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.KeyVaultAnalyticsOMS?tab=Overview) or by using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="c88cc-113">Merhaba anahtar kasası kaynakları toomonitor için günlüğü, her iki hello kullanarak tanılamayı etkinleştirin [portal](#enable-key-vault-diagnostics-in-the-portal) veya [PowerShell](#enable-key-vault-diagnostics-using-powershell)</span><span class="sxs-lookup"><span data-stu-id="c88cc-113">Enable diagnostics logging for hello Key Vault resources toomonitor, using either hello [portal](#enable-key-vault-diagnostics-in-the-portal) or [PowerShell](#enable-key-vault-diagnostics-using-powershell)</span></span>

### <a name="enable-key-vault-diagnostics-in-hello-portal"></a><span data-ttu-id="c88cc-114">Anahtar kasası tanılama hello portalında etkinleştir</span><span class="sxs-lookup"><span data-stu-id="c88cc-114">Enable Key Vault diagnostics in hello portal</span></span>

1. <span data-ttu-id="c88cc-115">Toohello anahtar kasası kaynak toomonitor Hello Azure portalına gidin</span><span class="sxs-lookup"><span data-stu-id="c88cc-115">In hello Azure portal, navigate toohello Key Vault resource toomonitor</span></span>
2. <span data-ttu-id="c88cc-116">Seçin *tanılama günlükleri* sayfası aşağıdaki tooopen hello</span><span class="sxs-lookup"><span data-stu-id="c88cc-116">Select *Diagnostics logs* tooopen hello following page</span></span>

   ![Azure anahtar kasası döşeme görüntüsü](./media/log-analytics-azure-keyvault/log-analytics-keyvault-enable-diagnostics01.png)
3. <span data-ttu-id="c88cc-118">Tıklatın *tanılamayı açın* sayfası aşağıdaki tooopen hello</span><span class="sxs-lookup"><span data-stu-id="c88cc-118">Click *Turn on diagnostics* tooopen hello following page</span></span>

   ![Azure anahtar kasası döşeme görüntüsü](./media/log-analytics-azure-keyvault/log-analytics-keyvault-enable-diagnostics02.png)
4. <span data-ttu-id="c88cc-120">Tanılama üzerinde tooturn tıklatın *üzerinde* altında *durumu*</span><span class="sxs-lookup"><span data-stu-id="c88cc-120">tooturn on diagnostics, click *On* under *Status*</span></span>
5. <span data-ttu-id="c88cc-121">Merhaba onay kutusunu tıklatın *tooLog Analytics Gönder*</span><span class="sxs-lookup"><span data-stu-id="c88cc-121">Click hello checkbox for *Send tooLog Analytics*</span></span>
6. <span data-ttu-id="c88cc-122">Varolan bir günlük analizi çalışma alanını seçin veya bir çalışma alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="c88cc-122">Select an existing Log Analytics workspace, or create a workspace</span></span>
7. <span data-ttu-id="c88cc-123">tooenable *AuditEvent* günlükleri, günlük altında hello onay kutusunu tıklatın</span><span class="sxs-lookup"><span data-stu-id="c88cc-123">tooenable *AuditEvent* logs, click hello checkbox under Log</span></span>
8. <span data-ttu-id="c88cc-124">Tıklatın *kaydetmek* tooenable hello günlüğe tanılama tooLog analizi</span><span class="sxs-lookup"><span data-stu-id="c88cc-124">Click *Save* tooenable hello logging of diagnostics tooLog Analytics</span></span>

### <a name="enable-key-vault-diagnostics-using-powershell"></a><span data-ttu-id="c88cc-125">Anahtar kasası tanılamayı PowerShell kullanarak etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="c88cc-125">Enable Key Vault diagnostics using PowerShell</span></span>
<span data-ttu-id="c88cc-126">PowerShell Betiği aşağıdaki hello nasıl bir örnek sağlar toouse `Set-AzureRmDiagnosticSetting` tooenable anahtar kasası için günlüğü Tanılama:</span><span class="sxs-lookup"><span data-stu-id="c88cc-126">hello following PowerShell script provides an example of how toouse `Set-AzureRmDiagnosticSetting` tooenable diagnostic logging for Key Vault:</span></span>
```
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$kv = Get-AzureRmKeyVault -VaultName 'ContosoKeyVault'

Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```



## <a name="review-azure-key-vault-data-collection-details"></a><span data-ttu-id="c88cc-127">Azure anahtar kasası veri toplama ayrıntılarını gözden geçirin</span><span class="sxs-lookup"><span data-stu-id="c88cc-127">Review Azure Key Vault data collection details</span></span>
<span data-ttu-id="c88cc-128">Azure anahtar kasası çözüm tanılama günlükleri doğrudan hello anahtar Kasası ' toplar.</span><span class="sxs-lookup"><span data-stu-id="c88cc-128">Azure Key Vault solution collects diagnostics logs directly from hello Key Vault.</span></span>
<span data-ttu-id="c88cc-129">Gerekli toowrite hello günlükleri tooAzure Blob Depolama değil ve aracı için veri toplama gereklidir.</span><span class="sxs-lookup"><span data-stu-id="c88cc-129">It is not necessary toowrite hello logs tooAzure Blob storage and no agent is required for data collection.</span></span>

<span data-ttu-id="c88cc-130">Merhaba aşağıdaki tabloda veri toplama yöntemleri ve Azure anahtar kasası için verileri nasıl toplanır ilgili diğer ayrıntıları gösterir.</span><span class="sxs-lookup"><span data-stu-id="c88cc-130">hello following table shows data collection methods and other details about how data is collected for Azure Key Vault.</span></span>

| <span data-ttu-id="c88cc-131">Platform</span><span class="sxs-lookup"><span data-stu-id="c88cc-131">Platform</span></span> | <span data-ttu-id="c88cc-132">Doğrudan Aracısı</span><span class="sxs-lookup"><span data-stu-id="c88cc-132">Direct agent</span></span> | <span data-ttu-id="c88cc-133">Systems Center Operations Manager Aracısı</span><span class="sxs-lookup"><span data-stu-id="c88cc-133">Systems Center Operations Manager agent</span></span> | <span data-ttu-id="c88cc-134">Azure</span><span class="sxs-lookup"><span data-stu-id="c88cc-134">Azure</span></span> | <span data-ttu-id="c88cc-135">Operations Manager gerekli?</span><span class="sxs-lookup"><span data-stu-id="c88cc-135">Operations Manager required?</span></span> | <span data-ttu-id="c88cc-136">Operations Manager Aracısı verilerinin yönetim grubu gönderilen</span><span class="sxs-lookup"><span data-stu-id="c88cc-136">Operations Manager agent data sent via management group</span></span> | <span data-ttu-id="c88cc-137">Toplama sıklığı</span><span class="sxs-lookup"><span data-stu-id="c88cc-137">Collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="c88cc-138">Azure</span><span class="sxs-lookup"><span data-stu-id="c88cc-138">Azure</span></span> |  |  |<span data-ttu-id="c88cc-139">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c88cc-139">&#8226;</span></span> |  |  | <span data-ttu-id="c88cc-140">geldiğinde</span><span class="sxs-lookup"><span data-stu-id="c88cc-140">on arrival</span></span> |

## <a name="use-azure-key-vault"></a><span data-ttu-id="c88cc-141">Azure Key Vault kullanma</span><span class="sxs-lookup"><span data-stu-id="c88cc-141">Use Azure Key Vault</span></span>
<span data-ttu-id="c88cc-142">Çalıştırdıktan sonra [hello çözümü](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.KeyVaultAnalyticsOMS?tab=Overview), hello tıklayarak hello anahtar kasası verileri görüntüleme **Azure anahtar kasası** döşeme hello **genel bakış** günlük analizi sayfası.</span><span class="sxs-lookup"><span data-stu-id="c88cc-142">After you [install hello solution](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.KeyVaultAnalyticsOMS?tab=Overview), view hello Key Vault data by clicking hello **Azure Key Vault** tile from hello **Overview** page of Log Analytics.</span></span>

![Azure anahtar kasası döşeme görüntüsü](./media/log-analytics-azure-keyvault/log-analytics-keyvault-tile.png)

<span data-ttu-id="c88cc-144">Merhaba tıklattıktan sonra **genel bakış** kutucuğu toodetails kategorileri aşağıdaki hello için günlükleri ve ardından ayrıntıya özetlerini görüntüleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c88cc-144">After you click hello **Overview** tile, you can view summaries of your logs and then drill in toodetails for hello following categories:</span></span>

* <span data-ttu-id="c88cc-145">Tüm anahtar kasası işlemleri zaman içinde hacmi</span><span class="sxs-lookup"><span data-stu-id="c88cc-145">Volume of all key vault operations over time</span></span>
* <span data-ttu-id="c88cc-146">İşlem birimleri zaman içinde başarısız oldu</span><span class="sxs-lookup"><span data-stu-id="c88cc-146">Failed operation volumes over time</span></span>
* <span data-ttu-id="c88cc-147">İşlem tarafından işletimsel ortalama gecikme süresi</span><span class="sxs-lookup"><span data-stu-id="c88cc-147">Average operational latency by operation</span></span>
* <span data-ttu-id="c88cc-148">Birden fazla 1000 ms ele işlemlerinin hello sayısı ve birden fazla 1000 ms ele işlemleri listesini işlemleri için hizmet kalitesi</span><span class="sxs-lookup"><span data-stu-id="c88cc-148">Quality of service for operations with hello number of operations that take more than 1000 ms and a list of operations that take more than 1000 ms</span></span>

![Azure anahtar kasası Pano görüntüsü](./media/log-analytics-azure-keyvault/log-analytics-keyvault01.png)

![Azure anahtar kasası Pano görüntüsü](./media/log-analytics-azure-keyvault/log-analytics-keyvault02.png)

### <a name="tooview-details-for-any-operation"></a><span data-ttu-id="c88cc-151">herhangi bir işlem için tooview ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="c88cc-151">tooview details for any operation</span></span>
1. <span data-ttu-id="c88cc-152">Merhaba üzerinde **genel bakış** hello sayfasında, **Azure anahtar kasası** döşeme.</span><span class="sxs-lookup"><span data-stu-id="c88cc-152">On hello **Overview** page, click hello **Azure Key Vault** tile.</span></span>
2. <span data-ttu-id="c88cc-153">Merhaba üzerinde **Azure anahtar kasası** panoyu hello Kanatlar birinde hello özet bilgileri gözden geçirin ve ardından bir tooview hakkında ayrıntılı bilgi, hello günlük arama sayfasında.</span><span class="sxs-lookup"><span data-stu-id="c88cc-153">On hello **Azure Key Vault** dashboard, review hello summary information in one of hello blades, and then click one tooview detailed information about it in hello log search page.</span></span>

    <span data-ttu-id="c88cc-154">Merhaba günlük arama sayfaları hiçbirinde, sonuçları zaman, ayrıntılı sonuçları ve günlük arama geçmişi görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c88cc-154">On any of hello log search pages, you can view results by time, detailed results, and your log search history.</span></span> <span data-ttu-id="c88cc-155">Modelleri toonarrow hello sonuçlarına göre de filtre uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c88cc-155">You can also filter by facets toonarrow hello results.</span></span>

## <a name="log-analytics-records"></a><span data-ttu-id="c88cc-156">Log Analytics kayıtları</span><span class="sxs-lookup"><span data-stu-id="c88cc-156">Log Analytics records</span></span>
<span data-ttu-id="c88cc-157">Hello Azure anahtar kasası çözüm çözümler türünü içeren kayıtları **KeyVaults** gelen toplanan [AuditEvent günlükleri](../key-vault/key-vault-logging.md) Azure tanılama.</span><span class="sxs-lookup"><span data-stu-id="c88cc-157">hello Azure Key Vault solution analyzes records that have a type of **KeyVaults** that are collected from [AuditEvent logs](../key-vault/key-vault-logging.md) in Azure Diagnostics.</span></span>  <span data-ttu-id="c88cc-158">Bu kayıtlar için özellikleri aşağıdaki tablonun hello şunlardır:</span><span class="sxs-lookup"><span data-stu-id="c88cc-158">Properties for these records are in hello following table:</span></span>  

| <span data-ttu-id="c88cc-159">Özellik</span><span class="sxs-lookup"><span data-stu-id="c88cc-159">Property</span></span> | <span data-ttu-id="c88cc-160">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c88cc-160">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="c88cc-161">Tür</span><span class="sxs-lookup"><span data-stu-id="c88cc-161">Type</span></span> |<span data-ttu-id="c88cc-162">*AzureDiagnostics*</span><span class="sxs-lookup"><span data-stu-id="c88cc-162">*AzureDiagnostics*</span></span> |
| <span data-ttu-id="c88cc-163">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="c88cc-163">SourceSystem</span></span> |<span data-ttu-id="c88cc-164">*Azure*</span><span class="sxs-lookup"><span data-stu-id="c88cc-164">*Azure*</span></span> |
| <span data-ttu-id="c88cc-165">CallerIpAddress</span><span class="sxs-lookup"><span data-stu-id="c88cc-165">CallerIpAddress</span></span> |<span data-ttu-id="c88cc-166">Merhaba isteği yapan hello istemcinin IP adresi</span><span class="sxs-lookup"><span data-stu-id="c88cc-166">IP address of hello client who made hello request</span></span> |
| <span data-ttu-id="c88cc-167">Kategori</span><span class="sxs-lookup"><span data-stu-id="c88cc-167">Category</span></span> | <span data-ttu-id="c88cc-168">*AuditEvent*</span><span class="sxs-lookup"><span data-stu-id="c88cc-168">*AuditEvent*</span></span> |
| <span data-ttu-id="c88cc-169">CorrelationId</span><span class="sxs-lookup"><span data-stu-id="c88cc-169">CorrelationId</span></span> |<span data-ttu-id="c88cc-170">İstemci hello isteğe bağlı bir GUID toocorrelate istemci-tarafı günlüklerini Hizmet tarafı (anahtar kasası) günlükleriyle geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c88cc-170">An optional GUID that hello client can pass toocorrelate client-side logs with service-side (Key Vault) logs.</span></span> |
| <span data-ttu-id="c88cc-171">DurationMs</span><span class="sxs-lookup"><span data-stu-id="c88cc-171">DurationMs</span></span> |<span data-ttu-id="c88cc-172">Milisaniye cinsinden tooservice hello REST API isteği, geçen süre.</span><span class="sxs-lookup"><span data-stu-id="c88cc-172">Time it took tooservice hello REST API request, in milliseconds.</span></span> <span data-ttu-id="c88cc-173">Merhaba istemci tarafında ölçmek hello süre bu süreyle eşleşmeyebilir şekilde bu kez ağ gecikmesini içermez.</span><span class="sxs-lookup"><span data-stu-id="c88cc-173">This time does not include network latency, so hello time that you measure on hello client side might not match this time.</span></span> |
| <span data-ttu-id="c88cc-174">httpStatusCode_d</span><span class="sxs-lookup"><span data-stu-id="c88cc-174">httpStatusCode_d</span></span> |<span data-ttu-id="c88cc-175">HTTP durum kodu Hello istek tarafından döndürülen (örneğin, *200*)</span><span class="sxs-lookup"><span data-stu-id="c88cc-175">HTTP status code returned by hello request (for example, *200*)</span></span> |
| <span data-ttu-id="c88cc-176">id_s</span><span class="sxs-lookup"><span data-stu-id="c88cc-176">id_s</span></span> |<span data-ttu-id="c88cc-177">Merhaba isteğin benzersiz kimliği</span><span class="sxs-lookup"><span data-stu-id="c88cc-177">Unique ID of hello request</span></span> |
| <span data-ttu-id="c88cc-178">identity_claim_appid_g</span><span class="sxs-lookup"><span data-stu-id="c88cc-178">identity_claim_appid_g</span></span> | <span data-ttu-id="c88cc-179">Merhaba uygulama kimliği için GUID</span><span class="sxs-lookup"><span data-stu-id="c88cc-179">GUID for hello application id</span></span> |
| <span data-ttu-id="c88cc-180">OperationName</span><span class="sxs-lookup"><span data-stu-id="c88cc-180">OperationName</span></span> |<span data-ttu-id="c88cc-181">Açıklandığı gibi hello işlemi, adı [Azure anahtar kasası günlüğü](../key-vault/key-vault-logging.md)</span><span class="sxs-lookup"><span data-stu-id="c88cc-181">Name of hello operation, as documented in [Azure Key Vault Logging](../key-vault/key-vault-logging.md)</span></span> |
| <span data-ttu-id="c88cc-182">OperationVersion</span><span class="sxs-lookup"><span data-stu-id="c88cc-182">OperationVersion</span></span> |<span data-ttu-id="c88cc-183">Merhaba istemci tarafından istenen REST API sürümü (örneğin *2015-06-01*)</span><span class="sxs-lookup"><span data-stu-id="c88cc-183">REST API version requested by hello client (for example *2015-06-01*)</span></span> |
| <span data-ttu-id="c88cc-184">requestUri_s</span><span class="sxs-lookup"><span data-stu-id="c88cc-184">requestUri_s</span></span> |<span data-ttu-id="c88cc-185">Merhaba istek URI'sini</span><span class="sxs-lookup"><span data-stu-id="c88cc-185">Uri of hello request</span></span> |
| <span data-ttu-id="c88cc-186">Kaynak</span><span class="sxs-lookup"><span data-stu-id="c88cc-186">Resource</span></span> |<span data-ttu-id="c88cc-187">Merhaba anahtar kasasının adı</span><span class="sxs-lookup"><span data-stu-id="c88cc-187">Name of hello key vault</span></span> |
| <span data-ttu-id="c88cc-188">ResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c88cc-188">ResourceGroup</span></span> |<span data-ttu-id="c88cc-189">Merhaba anahtar kasasının kaynak grubu</span><span class="sxs-lookup"><span data-stu-id="c88cc-189">Resource group of hello key vault</span></span> |
| <span data-ttu-id="c88cc-190">ResourceId</span><span class="sxs-lookup"><span data-stu-id="c88cc-190">ResourceId</span></span> |<span data-ttu-id="c88cc-191">Azure Resource Manager Kaynak Kimliği.</span><span class="sxs-lookup"><span data-stu-id="c88cc-191">Azure Resource Manager Resource ID.</span></span> <span data-ttu-id="c88cc-192">Anahtar kasası günlükleri için bu hello anahtar kasası kaynak kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="c88cc-192">For Key Vault logs, this is hello Key Vault resource ID.</span></span> |
| <span data-ttu-id="c88cc-193">ResourceProvider</span><span class="sxs-lookup"><span data-stu-id="c88cc-193">ResourceProvider</span></span> |<span data-ttu-id="c88cc-194">*MICROSOFT. KEYVAULT*</span><span class="sxs-lookup"><span data-stu-id="c88cc-194">*MICROSOFT.KEYVAULT*</span></span> |
| <span data-ttu-id="c88cc-195">ResourceType</span><span class="sxs-lookup"><span data-stu-id="c88cc-195">ResourceType</span></span> | <span data-ttu-id="c88cc-196">*KASALARI*</span><span class="sxs-lookup"><span data-stu-id="c88cc-196">*VAULTS*</span></span> |
| <span data-ttu-id="c88cc-197">ResultSignature</span><span class="sxs-lookup"><span data-stu-id="c88cc-197">ResultSignature</span></span> |<span data-ttu-id="c88cc-198">HTTP durumu (örneğin, *Tamam*)</span><span class="sxs-lookup"><span data-stu-id="c88cc-198">HTTP status (for example, *OK*)</span></span> |
| <span data-ttu-id="c88cc-199">ResultType</span><span class="sxs-lookup"><span data-stu-id="c88cc-199">ResultType</span></span> |<span data-ttu-id="c88cc-200">REST API isteğinin sonucunu (örneğin, *başarı*)</span><span class="sxs-lookup"><span data-stu-id="c88cc-200">Result of REST API request (for example, *Success*)</span></span> |
| <span data-ttu-id="c88cc-201">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="c88cc-201">SubscriptionId</span></span> |<span data-ttu-id="c88cc-202">Merhaba anahtar kasası içeren hello aboneliğin Azure abonelik kimliği</span><span class="sxs-lookup"><span data-stu-id="c88cc-202">Azure subscription ID of hello subscription containing hello Key Vault</span></span> |

## <a name="migrating-from-hello-old-key-vault-solution"></a><span data-ttu-id="c88cc-203">Merhaba eski anahtar kasası çözüm'den geçiş</span><span class="sxs-lookup"><span data-stu-id="c88cc-203">Migrating from hello old Key Vault solution</span></span>
<span data-ttu-id="c88cc-204">Ocak 2017 ' Analytics değiştirilen anahtar kasası tooLog günlükleri gönderme şekilde hello desteklenir.</span><span class="sxs-lookup"><span data-stu-id="c88cc-204">In January 2017, hello supported way of sending logs from Key Vault tooLog Analytics changed.</span></span> <span data-ttu-id="c88cc-205">Bu değişiklikler hello aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="c88cc-205">These changes provide hello following advantages:</span></span>
+ <span data-ttu-id="c88cc-206">TooLog Analytics hello olmadan gereken doğrudan toouse bir depolama hesabı günlüklerine yazılır</span><span class="sxs-lookup"><span data-stu-id="c88cc-206">Logs are written directly tooLog Analytics without hello need toouse a storage account</span></span>
+ <span data-ttu-id="c88cc-207">Günlük analizi kullanılabilir olmasını durduracak toothem günlükleri olduğunda hello zamandan daha az gecikme oluşturulan</span><span class="sxs-lookup"><span data-stu-id="c88cc-207">Less latency from hello time when logs are generated toothem being available in Log Analytics</span></span>
+ <span data-ttu-id="c88cc-208">Daha az yapılandırma adımları</span><span class="sxs-lookup"><span data-stu-id="c88cc-208">Fewer configuration steps</span></span>
+ <span data-ttu-id="c88cc-209">Azure tanılama tüm türleri için ortak bir biçimi</span><span class="sxs-lookup"><span data-stu-id="c88cc-209">A common format for all types of Azure diagnostics</span></span>

<span data-ttu-id="c88cc-210">toouse hello çözüm güncelleştirildi:</span><span class="sxs-lookup"><span data-stu-id="c88cc-210">toouse hello updated solution:</span></span>

1. [<span data-ttu-id="c88cc-211">Anahtar Kasası'nı doğrudan tooLog Analytics gönderilen tanılama toobe yapılandırın</span><span class="sxs-lookup"><span data-stu-id="c88cc-211">Configure diagnostics toobe sent directly tooLog Analytics from Key Vault</span></span>](#enable-key-vault-diagnostics-in-the-portal)  
2. <span data-ttu-id="c88cc-212">Açıklanan hello işlemi kullanarak Hello Azure anahtar kasası çözümünü etkinleştirme [hello Çözümleri Galerisi çözümlerinden günlük analizi Ekle](log-analytics-add-solutions.md)</span><span class="sxs-lookup"><span data-stu-id="c88cc-212">Enable hello Azure Key Vault solution by using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md)</span></span>
3. <span data-ttu-id="c88cc-213">Tüm kayıtlı sorgu, panolar veya uyarıları toouse hello yeni veri türü güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="c88cc-213">Update any saved queries, dashboards, or alerts toouse hello new data type</span></span>
  + <span data-ttu-id="c88cc-214">Değişikliği türüdür: KeyVaults tooAzureDiagnostics.</span><span class="sxs-lookup"><span data-stu-id="c88cc-214">Type is change from: KeyVaults tooAzureDiagnostics.</span></span> <span data-ttu-id="c88cc-215">Merhaba ResourceType toofilter tooKey kasası günlükleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c88cc-215">You can use hello ResourceType toofilter tooKey Vault Logs.</span></span>
  - <span data-ttu-id="c88cc-216">Yerine: `Type=KeyVaults`, kullanın`Type=AzureDiagnostics ResourceType=VAULTS`</span><span class="sxs-lookup"><span data-stu-id="c88cc-216">Instead of: `Type=KeyVaults`, use `Type=AzureDiagnostics ResourceType=VAULTS`</span></span>
  + <span data-ttu-id="c88cc-217">Alanlar: (alan adları büyük küçük harfe duyarlı)</span><span class="sxs-lookup"><span data-stu-id="c88cc-217">Fields: (Field names are case-sensitive)</span></span>
  - <span data-ttu-id="c88cc-218">Sonekine sahip herhangi bir alan için \_s, \_d veya \_g hello adı hello ilk karakter toolower harf durumunu değiştir</span><span class="sxs-lookup"><span data-stu-id="c88cc-218">For any field that has a suffix of \_s, \_d, or \_g in hello name, change hello first character toolower case</span></span>
  - <span data-ttu-id="c88cc-219">Sonekine sahip herhangi bir alan için \_adında, hello veri o iç içe geçmiş hello alan adlarını temel alarak tek tek alanlara bölünür.</span><span class="sxs-lookup"><span data-stu-id="c88cc-219">For any field that has a suffix of \_o in name, hello data is split into individual fields based on hello nested field names.</span></span> <span data-ttu-id="c88cc-220">Örneğin, hello hello çağıran UPN bir alana depolanır`identity_claim_http_schemas_xmlsoap_org_ws_2005_05_identity_claims_upn_s`</span><span class="sxs-lookup"><span data-stu-id="c88cc-220">For example, hello UPN of hello caller is stored in a field `identity_claim_http_schemas_xmlsoap_org_ws_2005_05_identity_claims_upn_s`</span></span>
   - <span data-ttu-id="c88cc-221">Alan değiştirilen CallerIpAddress tooCallerIPAddress</span><span class="sxs-lookup"><span data-stu-id="c88cc-221">Field CallerIpAddress changed tooCallerIPAddress</span></span>
   - <span data-ttu-id="c88cc-222">Alan RemoteIPCountry artık mevcut değil</span><span class="sxs-lookup"><span data-stu-id="c88cc-222">Field RemoteIPCountry is no longer present</span></span>
4. <span data-ttu-id="c88cc-223">Merhaba kaldırmak *anahtar kasası Analytics (kullanım dışı)* çözümü.</span><span class="sxs-lookup"><span data-stu-id="c88cc-223">Remove hello *Key Vault Analytics (Deprecated)* solution.</span></span> <span data-ttu-id="c88cc-224">PowerShell kullanıyorsanız, kullanın`Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that hello workspace is in> -WorkspaceName <name of hello log analytics workspace> -IntelligencePackName "KeyVault" -Enabled $false`</span><span class="sxs-lookup"><span data-stu-id="c88cc-224">If you are using PowerShell, use `Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that hello workspace is in> -WorkspaceName <name of hello log analytics workspace> -IntelligencePackName "KeyVault" -Enabled $false`</span></span>

<span data-ttu-id="c88cc-225">Merhaba değişiklik hello yeni çözümde görünür değil önce veri toplanmadı.</span><span class="sxs-lookup"><span data-stu-id="c88cc-225">Data collected before hello change is not visible in hello new solution.</span></span> <span data-ttu-id="c88cc-226">Bu verileri kullanarak hello için eski türü ve alan adları tooquery devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c88cc-226">You can continue tooquery for this data using hello old Type and field names.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="c88cc-227">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="c88cc-227">Troubleshooting</span></span>
[!INCLUDE [log-analytics-troubleshoot-azure-diagnostics](../../includes/log-analytics-troubleshoot-azure-diagnostics.md)]

## <a name="next-steps"></a><span data-ttu-id="c88cc-228">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c88cc-228">Next steps</span></span>
* <span data-ttu-id="c88cc-229">Kullanım [günlük analizi aramaları oturum](log-analytics-log-searches.md) tooview ayrıntılı Azure anahtar kasası veri.</span><span class="sxs-lookup"><span data-stu-id="c88cc-229">Use [Log searches in Log Analytics](log-analytics-log-searches.md) tooview detailed Azure Key Vault data.</span></span>
