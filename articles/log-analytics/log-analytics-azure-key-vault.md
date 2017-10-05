---
title: "Günlük analizi Azure anahtar kasası çözümde | Microsoft Docs"
description: "Azure anahtar kasası günlükleri gözden geçirmek için günlük analizi Azure anahtar kasası çözüm kullanabilirsiniz."
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
ms.openlocfilehash: 651586e0846ffb22a23e64b73c2cc614980d9b92
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-key-vault-analytics-solution-in-log-analytics"></a><span data-ttu-id="a0e86-103">Günlük analizi Azure anahtar kasası Analytics çözümde</span><span class="sxs-lookup"><span data-stu-id="a0e86-103">Azure Key Vault Analytics solution in Log Analytics</span></span>

![Anahtar kasası simgesi](./media/log-analytics-azure-keyvault/key-vault-analytics-symbol.png)

<span data-ttu-id="a0e86-105">Azure Key Vault AuditEvent günlüklerini incelemek için Log Analytics içindeki Azure Key Vault çözümünü kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a0e86-105">You can use the Azure Key Vault solution in Log Analytics to review Azure Key Vault AuditEvent logs.</span></span>

<span data-ttu-id="a0e86-106">Çözümü kullanmak için Azure anahtar kasası tanılama günlük kaydını etkinleştirmek ve tanılama günlük analizi çalışma alanı'na doğrudan gerekir.</span><span class="sxs-lookup"><span data-stu-id="a0e86-106">To use the solution, you need to enable logging of Azure Key Vault diagnostics and direct the diagnostics to a Log Analytics workspace.</span></span> <span data-ttu-id="a0e86-107">Günlükleri Azure Blob depolama alanına yazmak gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="a0e86-107">It is not necessary to write the logs to Azure Blob storage.</span></span>

> [!NOTE]
> <span data-ttu-id="a0e86-108">Ocak 2017 ' günlükleri için günlük analizi anahtar Kasası'nı gönderme desteklenen şekilde değiştirildi.</span><span class="sxs-lookup"><span data-stu-id="a0e86-108">In January 2017, the supported way of sending logs from Key Vault to Log Analytics changed.</span></span> <span data-ttu-id="a0e86-109">Anahtar kasası çözümü kullanıyorsanız gösterir *(kullanım dışı)* başlığında başvurmak [eski anahtar kasası çözüm'den geçiş](#migrating-from-the-old-key-vault-solution) adımları izlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="a0e86-109">If the Key Vault solution you are using shows *(deprecated)* in the title, refer to [migrating from the old Key Vault solution](#migrating-from-the-old-key-vault-solution) for steps you need to follow.</span></span>
>
>

## <a name="install-and-configure-the-solution"></a><span data-ttu-id="a0e86-110">Yükleyin ve yapılandırın</span><span class="sxs-lookup"><span data-stu-id="a0e86-110">Install and configure the solution</span></span>
<span data-ttu-id="a0e86-111">Yükleme ve Azure anahtar kasası çözümü yapılandırmak için aşağıdaki yönergeleri kullanın:</span><span class="sxs-lookup"><span data-stu-id="a0e86-111">Use the following instructions to install and configure the Azure Key Vault solution:</span></span>

1. <span data-ttu-id="a0e86-112">Azure anahtar kasası çözümden etkinleştirmek [Azure Market](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.KeyVaultAnalyticsOMS?tab=Overview) veya açıklanan işlemi kullanarak [Çözümleri Galerisi eklemek günlük analizi çözümleri](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="a0e86-112">Enable the Azure Key Vault solution from [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.KeyVaultAnalyticsOMS?tab=Overview) or by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="a0e86-113">Kullanarak izlemek, anahtar kasası kaynaklar için tanılama günlüğünü etkinleştirme [portal](#enable-key-vault-diagnostics-in-the-portal) veya [PowerShell](#enable-key-vault-diagnostics-using-powershell)</span><span class="sxs-lookup"><span data-stu-id="a0e86-113">Enable diagnostics logging for the Key Vault resources to monitor, using either the [portal](#enable-key-vault-diagnostics-in-the-portal) or [PowerShell](#enable-key-vault-diagnostics-using-powershell)</span></span>

### <a name="enable-key-vault-diagnostics-in-the-portal"></a><span data-ttu-id="a0e86-114">Anahtar kasası tanılama portalda etkinleştir</span><span class="sxs-lookup"><span data-stu-id="a0e86-114">Enable Key Vault diagnostics in the portal</span></span>

1. <span data-ttu-id="a0e86-115">Azure portalında izlemek için anahtar kasası kaynak gidin</span><span class="sxs-lookup"><span data-stu-id="a0e86-115">In the Azure portal, navigate to the Key Vault resource to monitor</span></span>
2. <span data-ttu-id="a0e86-116">Seçin *tanılama günlükleri* aşağıdaki sayfasını açmak için</span><span class="sxs-lookup"><span data-stu-id="a0e86-116">Select *Diagnostics logs* to open the following page</span></span>

   ![Azure anahtar kasası döşeme görüntüsü](./media/log-analytics-azure-keyvault/log-analytics-keyvault-enable-diagnostics01.png)
3. <span data-ttu-id="a0e86-118">Tıklatın *tanılamayı açın* aşağıdaki sayfasını açmak için</span><span class="sxs-lookup"><span data-stu-id="a0e86-118">Click *Turn on diagnostics* to open the following page</span></span>

   ![Azure anahtar kasası döşeme görüntüsü](./media/log-analytics-azure-keyvault/log-analytics-keyvault-enable-diagnostics02.png)
4. <span data-ttu-id="a0e86-120">Tanılama'yı açmak için tıklatın *üzerinde* altında *durumu*</span><span class="sxs-lookup"><span data-stu-id="a0e86-120">To turn on diagnostics, click *On* under *Status*</span></span>
5. <span data-ttu-id="a0e86-121">Onay kutusunu tıklatın *için günlük analizi Gönder*</span><span class="sxs-lookup"><span data-stu-id="a0e86-121">Click the checkbox for *Send to Log Analytics*</span></span>
6. <span data-ttu-id="a0e86-122">Varolan bir günlük analizi çalışma alanını seçin veya bir çalışma alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a0e86-122">Select an existing Log Analytics workspace, or create a workspace</span></span>
7. <span data-ttu-id="a0e86-123">Etkinleştirmek için *AuditEvent* günlükleri, günlük altında onay kutusunu tıklatın</span><span class="sxs-lookup"><span data-stu-id="a0e86-123">To enable *AuditEvent* logs, click the checkbox under Log</span></span>
8. <span data-ttu-id="a0e86-124">Tıklatın *kaydetmek* günlük analizi için tanılama günlük kaydını etkinleştirmek için</span><span class="sxs-lookup"><span data-stu-id="a0e86-124">Click *Save* to enable the logging of diagnostics to Log Analytics</span></span>

### <a name="enable-key-vault-diagnostics-using-powershell"></a><span data-ttu-id="a0e86-125">Anahtar kasası tanılamayı PowerShell kullanarak etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="a0e86-125">Enable Key Vault diagnostics using PowerShell</span></span>
<span data-ttu-id="a0e86-126">Aşağıdaki PowerShell betiğini nasıl kullanılacağını gösteren bir örnek sağlar `Set-AzureRmDiagnosticSetting` anahtar kasası için tanılama günlük kaydını etkinleştirmek için:</span><span class="sxs-lookup"><span data-stu-id="a0e86-126">The following PowerShell script provides an example of how to use `Set-AzureRmDiagnosticSetting` to enable diagnostic logging for Key Vault:</span></span>
```
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$kv = Get-AzureRmKeyVault -VaultName 'ContosoKeyVault'

Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```



## <a name="review-azure-key-vault-data-collection-details"></a><span data-ttu-id="a0e86-127">Azure anahtar kasası veri toplama ayrıntılarını gözden geçirin</span><span class="sxs-lookup"><span data-stu-id="a0e86-127">Review Azure Key Vault data collection details</span></span>
<span data-ttu-id="a0e86-128">Azure anahtar kasası çözüm tanılama günlükleri doğrudan anahtar Kasası'nı toplar.</span><span class="sxs-lookup"><span data-stu-id="a0e86-128">Azure Key Vault solution collects diagnostics logs directly from the Key Vault.</span></span>
<span data-ttu-id="a0e86-129">Günlükleri Azure Blob depolama alanına yazmak gerekli değildir ve aracı için veri toplama gereklidir.</span><span class="sxs-lookup"><span data-stu-id="a0e86-129">It is not necessary to write the logs to Azure Blob storage and no agent is required for data collection.</span></span>

<span data-ttu-id="a0e86-130">Aşağıdaki tabloda, veri toplama yöntemleri ve Azure anahtar kasası için verileri nasıl toplanır ilgili diğer ayrıntıları gösterir.</span><span class="sxs-lookup"><span data-stu-id="a0e86-130">The following table shows data collection methods and other details about how data is collected for Azure Key Vault.</span></span>

| <span data-ttu-id="a0e86-131">Platform</span><span class="sxs-lookup"><span data-stu-id="a0e86-131">Platform</span></span> | <span data-ttu-id="a0e86-132">Doğrudan Aracısı</span><span class="sxs-lookup"><span data-stu-id="a0e86-132">Direct agent</span></span> | <span data-ttu-id="a0e86-133">Systems Center Operations Manager Aracısı</span><span class="sxs-lookup"><span data-stu-id="a0e86-133">Systems Center Operations Manager agent</span></span> | <span data-ttu-id="a0e86-134">Azure</span><span class="sxs-lookup"><span data-stu-id="a0e86-134">Azure</span></span> | <span data-ttu-id="a0e86-135">Operations Manager gerekli?</span><span class="sxs-lookup"><span data-stu-id="a0e86-135">Operations Manager required?</span></span> | <span data-ttu-id="a0e86-136">Operations Manager Aracısı verilerinin yönetim grubu gönderilen</span><span class="sxs-lookup"><span data-stu-id="a0e86-136">Operations Manager agent data sent via management group</span></span> | <span data-ttu-id="a0e86-137">Toplama sıklığı</span><span class="sxs-lookup"><span data-stu-id="a0e86-137">Collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="a0e86-138">Azure</span><span class="sxs-lookup"><span data-stu-id="a0e86-138">Azure</span></span> |  |  |<span data-ttu-id="a0e86-139">&#8226;</span><span class="sxs-lookup"><span data-stu-id="a0e86-139">&#8226;</span></span> |  |  | <span data-ttu-id="a0e86-140">geldiğinde</span><span class="sxs-lookup"><span data-stu-id="a0e86-140">on arrival</span></span> |

## <a name="use-azure-key-vault"></a><span data-ttu-id="a0e86-141">Azure Key Vault kullanma</span><span class="sxs-lookup"><span data-stu-id="a0e86-141">Use Azure Key Vault</span></span>
<span data-ttu-id="a0e86-142">Çalıştırdıktan sonra [çözümü yüklemek](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.KeyVaultAnalyticsOMS?tab=Overview), tıklayarak anahtar kasası verisinin **Azure anahtar kasası** gelen döşeme **genel bakış** günlük analizi sayfası.</span><span class="sxs-lookup"><span data-stu-id="a0e86-142">After you [install the solution](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.KeyVaultAnalyticsOMS?tab=Overview), view the Key Vault data by clicking the **Azure Key Vault** tile from the **Overview** page of Log Analytics.</span></span>

![Azure anahtar kasası döşeme görüntüsü](./media/log-analytics-azure-keyvault/log-analytics-keyvault-tile.png)

<span data-ttu-id="a0e86-144">Tıklattıktan sonra **genel bakış** döşeme, günlüklerinizi özetlerini görüntüleyin ve aşağıdaki kategorilerde ayrıntıları için detaya:</span><span class="sxs-lookup"><span data-stu-id="a0e86-144">After you click the **Overview** tile, you can view summaries of your logs and then drill in to details for the following categories:</span></span>

* <span data-ttu-id="a0e86-145">Tüm anahtar kasası işlemleri zaman içinde hacmi</span><span class="sxs-lookup"><span data-stu-id="a0e86-145">Volume of all key vault operations over time</span></span>
* <span data-ttu-id="a0e86-146">İşlem birimleri zaman içinde başarısız oldu</span><span class="sxs-lookup"><span data-stu-id="a0e86-146">Failed operation volumes over time</span></span>
* <span data-ttu-id="a0e86-147">İşlem tarafından işletimsel ortalama gecikme süresi</span><span class="sxs-lookup"><span data-stu-id="a0e86-147">Average operational latency by operation</span></span>
* <span data-ttu-id="a0e86-148">Birden fazla 1000 ms ele işlemlerinin sayısı ve birden fazla 1000 ms ele işlemleri listesini işlemleri için hizmet kalitesi</span><span class="sxs-lookup"><span data-stu-id="a0e86-148">Quality of service for operations with the number of operations that take more than 1000 ms and a list of operations that take more than 1000 ms</span></span>

![Azure anahtar kasası Pano görüntüsü](./media/log-analytics-azure-keyvault/log-analytics-keyvault01.png)

![Azure anahtar kasası Pano görüntüsü](./media/log-analytics-azure-keyvault/log-analytics-keyvault02.png)

### <a name="to-view-details-for-any-operation"></a><span data-ttu-id="a0e86-151">Herhangi bir işlem ayrıntılarını görüntülemek için</span><span class="sxs-lookup"><span data-stu-id="a0e86-151">To view details for any operation</span></span>
1. <span data-ttu-id="a0e86-152">Üzerinde **genel bakış** sayfasında, **Azure anahtar kasası** döşeme.</span><span class="sxs-lookup"><span data-stu-id="a0e86-152">On the **Overview** page, click the **Azure Key Vault** tile.</span></span>
2. <span data-ttu-id="a0e86-153">Üzerinde **Azure anahtar kasası** Pano, dikey pencereleri birinde özet bilgilerini inceleyin ve bir günlük arama sayfasında ilgili ayrıntılı bilgileri görüntülemek için tıklatın.</span><span class="sxs-lookup"><span data-stu-id="a0e86-153">On the **Azure Key Vault** dashboard, review the summary information in one of the blades, and then click one to view detailed information about it in the log search page.</span></span>

    <span data-ttu-id="a0e86-154">Herhangi bir günlük arama sayfası üzerinde sonuçları zaman, ayrıntılı sonuçları ve günlük arama geçmişi görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a0e86-154">On any of the log search pages, you can view results by time, detailed results, and your log search history.</span></span> <span data-ttu-id="a0e86-155">Sonuçları daraltmak için modelleri göre de filtre uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a0e86-155">You can also filter by facets to narrow the results.</span></span>

## <a name="log-analytics-records"></a><span data-ttu-id="a0e86-156">Log Analytics kayıtları</span><span class="sxs-lookup"><span data-stu-id="a0e86-156">Log Analytics records</span></span>
<span data-ttu-id="a0e86-157">Azure anahtar kasası çözüm türünü içeren kayıtları çözümler **KeyVaults** gelen toplanan [AuditEvent günlükleri](../key-vault/key-vault-logging.md) Azure tanılama.</span><span class="sxs-lookup"><span data-stu-id="a0e86-157">The Azure Key Vault solution analyzes records that have a type of **KeyVaults** that are collected from [AuditEvent logs](../key-vault/key-vault-logging.md) in Azure Diagnostics.</span></span>  <span data-ttu-id="a0e86-158">Aşağıdaki tabloda bu kayıtları için özellikleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="a0e86-158">Properties for these records are in the following table:</span></span>  

| <span data-ttu-id="a0e86-159">Özellik</span><span class="sxs-lookup"><span data-stu-id="a0e86-159">Property</span></span> | <span data-ttu-id="a0e86-160">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a0e86-160">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="a0e86-161">Tür</span><span class="sxs-lookup"><span data-stu-id="a0e86-161">Type</span></span> |<span data-ttu-id="a0e86-162">*AzureDiagnostics*</span><span class="sxs-lookup"><span data-stu-id="a0e86-162">*AzureDiagnostics*</span></span> |
| <span data-ttu-id="a0e86-163">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="a0e86-163">SourceSystem</span></span> |<span data-ttu-id="a0e86-164">*Azure*</span><span class="sxs-lookup"><span data-stu-id="a0e86-164">*Azure*</span></span> |
| <span data-ttu-id="a0e86-165">CallerIpAddress</span><span class="sxs-lookup"><span data-stu-id="a0e86-165">CallerIpAddress</span></span> |<span data-ttu-id="a0e86-166">İsteği yapan istemcinin IP adresi</span><span class="sxs-lookup"><span data-stu-id="a0e86-166">IP address of the client who made the request</span></span> |
| <span data-ttu-id="a0e86-167">Kategori</span><span class="sxs-lookup"><span data-stu-id="a0e86-167">Category</span></span> | <span data-ttu-id="a0e86-168">*AuditEvent*</span><span class="sxs-lookup"><span data-stu-id="a0e86-168">*AuditEvent*</span></span> |
| <span data-ttu-id="a0e86-169">CorrelationId</span><span class="sxs-lookup"><span data-stu-id="a0e86-169">CorrelationId</span></span> |<span data-ttu-id="a0e86-170">İstemci tarafı günlüklerini hizmet tarafı (Anahtar Kasası) günlükleriyle ilişkilendirmek için istemcinin geçirebileceği isteğe bağlı bir GUID.</span><span class="sxs-lookup"><span data-stu-id="a0e86-170">An optional GUID that the client can pass to correlate client-side logs with service-side (Key Vault) logs.</span></span> |
| <span data-ttu-id="a0e86-171">DurationMs</span><span class="sxs-lookup"><span data-stu-id="a0e86-171">DurationMs</span></span> |<span data-ttu-id="a0e86-172">Milisaniye cinsinden REST API'si isteğini sunmak için geçen süre.</span><span class="sxs-lookup"><span data-stu-id="a0e86-172">Time it took to service the REST API request, in milliseconds.</span></span> <span data-ttu-id="a0e86-173">İstemci tarafında ölçmek süre bu süreyle eşleşmeyebilir şekilde bu kez ağ gecikmesini içermez.</span><span class="sxs-lookup"><span data-stu-id="a0e86-173">This time does not include network latency, so the time that you measure on the client side might not match this time.</span></span> |
| <span data-ttu-id="a0e86-174">httpStatusCode_d</span><span class="sxs-lookup"><span data-stu-id="a0e86-174">httpStatusCode_d</span></span> |<span data-ttu-id="a0e86-175">İstek tarafından döndürülen HTTP durum kodu (örneğin, *200*)</span><span class="sxs-lookup"><span data-stu-id="a0e86-175">HTTP status code returned by the request (for example, *200*)</span></span> |
| <span data-ttu-id="a0e86-176">id_s</span><span class="sxs-lookup"><span data-stu-id="a0e86-176">id_s</span></span> |<span data-ttu-id="a0e86-177">İsteğin benzersiz kimliği</span><span class="sxs-lookup"><span data-stu-id="a0e86-177">Unique ID of the request</span></span> |
| <span data-ttu-id="a0e86-178">identity_claim_appid_g</span><span class="sxs-lookup"><span data-stu-id="a0e86-178">identity_claim_appid_g</span></span> | <span data-ttu-id="a0e86-179">Uygulama kimliği için GUID</span><span class="sxs-lookup"><span data-stu-id="a0e86-179">GUID for the application id</span></span> |
| <span data-ttu-id="a0e86-180">OperationName</span><span class="sxs-lookup"><span data-stu-id="a0e86-180">OperationName</span></span> |<span data-ttu-id="a0e86-181">Açıklandığı gibi işlemin adı [Azure anahtar kasası günlüğü](../key-vault/key-vault-logging.md)</span><span class="sxs-lookup"><span data-stu-id="a0e86-181">Name of the operation, as documented in [Azure Key Vault Logging](../key-vault/key-vault-logging.md)</span></span> |
| <span data-ttu-id="a0e86-182">OperationVersion</span><span class="sxs-lookup"><span data-stu-id="a0e86-182">OperationVersion</span></span> |<span data-ttu-id="a0e86-183">İstemci tarafından istenen REST API sürümü (örneğin *2015-06-01*)</span><span class="sxs-lookup"><span data-stu-id="a0e86-183">REST API version requested by the client (for example *2015-06-01*)</span></span> |
| <span data-ttu-id="a0e86-184">requestUri_s</span><span class="sxs-lookup"><span data-stu-id="a0e86-184">requestUri_s</span></span> |<span data-ttu-id="a0e86-185">İsteğin URI'si</span><span class="sxs-lookup"><span data-stu-id="a0e86-185">Uri of the request</span></span> |
| <span data-ttu-id="a0e86-186">Kaynak</span><span class="sxs-lookup"><span data-stu-id="a0e86-186">Resource</span></span> |<span data-ttu-id="a0e86-187">Anahtar kasasının adı</span><span class="sxs-lookup"><span data-stu-id="a0e86-187">Name of the key vault</span></span> |
| <span data-ttu-id="a0e86-188">ResourceGroup</span><span class="sxs-lookup"><span data-stu-id="a0e86-188">ResourceGroup</span></span> |<span data-ttu-id="a0e86-189">Anahtar kasasının kaynak grubu</span><span class="sxs-lookup"><span data-stu-id="a0e86-189">Resource group of the key vault</span></span> |
| <span data-ttu-id="a0e86-190">ResourceId</span><span class="sxs-lookup"><span data-stu-id="a0e86-190">ResourceId</span></span> |<span data-ttu-id="a0e86-191">Azure Resource Manager Kaynak Kimliği.</span><span class="sxs-lookup"><span data-stu-id="a0e86-191">Azure Resource Manager Resource ID.</span></span> <span data-ttu-id="a0e86-192">Anahtar kasası günlükleri için bu anahtar kasası kaynak kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="a0e86-192">For Key Vault logs, this is the Key Vault resource ID.</span></span> |
| <span data-ttu-id="a0e86-193">ResourceProvider</span><span class="sxs-lookup"><span data-stu-id="a0e86-193">ResourceProvider</span></span> |<span data-ttu-id="a0e86-194">*MICROSOFT. KEYVAULT*</span><span class="sxs-lookup"><span data-stu-id="a0e86-194">*MICROSOFT.KEYVAULT*</span></span> |
| <span data-ttu-id="a0e86-195">ResourceType</span><span class="sxs-lookup"><span data-stu-id="a0e86-195">ResourceType</span></span> | <span data-ttu-id="a0e86-196">*KASALARI*</span><span class="sxs-lookup"><span data-stu-id="a0e86-196">*VAULTS*</span></span> |
| <span data-ttu-id="a0e86-197">ResultSignature</span><span class="sxs-lookup"><span data-stu-id="a0e86-197">ResultSignature</span></span> |<span data-ttu-id="a0e86-198">HTTP durumu (örneğin, *Tamam*)</span><span class="sxs-lookup"><span data-stu-id="a0e86-198">HTTP status (for example, *OK*)</span></span> |
| <span data-ttu-id="a0e86-199">ResultType</span><span class="sxs-lookup"><span data-stu-id="a0e86-199">ResultType</span></span> |<span data-ttu-id="a0e86-200">REST API isteğinin sonucunu (örneğin, *başarı*)</span><span class="sxs-lookup"><span data-stu-id="a0e86-200">Result of REST API request (for example, *Success*)</span></span> |
| <span data-ttu-id="a0e86-201">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="a0e86-201">SubscriptionId</span></span> |<span data-ttu-id="a0e86-202">Anahtar kasası içeren abonelik Azure abonelik kimliği</span><span class="sxs-lookup"><span data-stu-id="a0e86-202">Azure subscription ID of the subscription containing the Key Vault</span></span> |

## <a name="migrating-from-the-old-key-vault-solution"></a><span data-ttu-id="a0e86-203">Eski anahtar kasası çözüm'den geçiş</span><span class="sxs-lookup"><span data-stu-id="a0e86-203">Migrating from the old Key Vault solution</span></span>
<span data-ttu-id="a0e86-204">Ocak 2017 ' günlükleri için günlük analizi anahtar Kasası'nı gönderme desteklenen şekilde değiştirildi.</span><span class="sxs-lookup"><span data-stu-id="a0e86-204">In January 2017, the supported way of sending logs from Key Vault to Log Analytics changed.</span></span> <span data-ttu-id="a0e86-205">Bu değişiklikler, aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="a0e86-205">These changes provide the following advantages:</span></span>
+ <span data-ttu-id="a0e86-206">Günlükleri doğrudan günlük analizi depolama hesabı kullanmak zorunda kalmadan yazılır</span><span class="sxs-lookup"><span data-stu-id="a0e86-206">Logs are written directly to Log Analytics without the need to use a storage account</span></span>
+ <span data-ttu-id="a0e86-207">Günlükleri bunları günlük analizi kullanılabilir olması için ne zaman oluşturulur zamandan daha az gecikme süresi</span><span class="sxs-lookup"><span data-stu-id="a0e86-207">Less latency from the time when logs are generated to them being available in Log Analytics</span></span>
+ <span data-ttu-id="a0e86-208">Daha az yapılandırma adımları</span><span class="sxs-lookup"><span data-stu-id="a0e86-208">Fewer configuration steps</span></span>
+ <span data-ttu-id="a0e86-209">Azure tanılama tüm türleri için ortak bir biçimi</span><span class="sxs-lookup"><span data-stu-id="a0e86-209">A common format for all types of Azure diagnostics</span></span>

<span data-ttu-id="a0e86-210">Güncellenen çözümü kullanmak için:</span><span class="sxs-lookup"><span data-stu-id="a0e86-210">To use the updated solution:</span></span>

1. [<span data-ttu-id="a0e86-211">Anahtar Kasası'nı doğrudan günlük analizi için gönderilecek tanılama Yapılandır</span><span class="sxs-lookup"><span data-stu-id="a0e86-211">Configure diagnostics to be sent directly to Log Analytics from Key Vault</span></span>](#enable-key-vault-diagnostics-in-the-portal)  
2. <span data-ttu-id="a0e86-212">Azure anahtar kasası çözüm açıklanan işlemi kullanarak etkinleştirin [Çözümleri Galerisi çözümlerinden günlük analizi Ekle](log-analytics-add-solutions.md)</span><span class="sxs-lookup"><span data-stu-id="a0e86-212">Enable the Azure Key Vault solution by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md)</span></span>
3. <span data-ttu-id="a0e86-213">Tüm kayıtlı sorgu, panolar veya yeni veri türünü kullanmak için uyarıları güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="a0e86-213">Update any saved queries, dashboards, or alerts to use the new data type</span></span>
  + <span data-ttu-id="a0e86-214">Değişikliği türüdür: AzureDiagnostics KeyVaults.</span><span class="sxs-lookup"><span data-stu-id="a0e86-214">Type is change from: KeyVaults to AzureDiagnostics.</span></span> <span data-ttu-id="a0e86-215">Kaynak türü, anahtar kasası günlükleri için filtre uygulamak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a0e86-215">You can use the ResourceType to filter to Key Vault Logs.</span></span>
  - <span data-ttu-id="a0e86-216">Yerine: `Type=KeyVaults`, kullanın`Type=AzureDiagnostics ResourceType=VAULTS`</span><span class="sxs-lookup"><span data-stu-id="a0e86-216">Instead of: `Type=KeyVaults`, use `Type=AzureDiagnostics ResourceType=VAULTS`</span></span>
  + <span data-ttu-id="a0e86-217">Alanlar: (alan adları büyük küçük harfe duyarlı)</span><span class="sxs-lookup"><span data-stu-id="a0e86-217">Fields: (Field names are case-sensitive)</span></span>
  - <span data-ttu-id="a0e86-218">Sonekine sahip herhangi bir alan için \_s, \_d veya \_g adı küçük harflere ilk karakter değiştirme</span><span class="sxs-lookup"><span data-stu-id="a0e86-218">For any field that has a suffix of \_s, \_d, or \_g in the name, change the first character to lower case</span></span>
  - <span data-ttu-id="a0e86-219">Sonekine sahip herhangi bir alan için \_adında, verileri o iç içe geçmiş alan adlarını temel alarak tek tek alanlara bölünür.</span><span class="sxs-lookup"><span data-stu-id="a0e86-219">For any field that has a suffix of \_o in name, the data is split into individual fields based on the nested field names.</span></span> <span data-ttu-id="a0e86-220">Örneğin, çağıran UPN bir alanda depolanır`identity_claim_http_schemas_xmlsoap_org_ws_2005_05_identity_claims_upn_s`</span><span class="sxs-lookup"><span data-stu-id="a0e86-220">For example, the UPN of the caller is stored in a field `identity_claim_http_schemas_xmlsoap_org_ws_2005_05_identity_claims_upn_s`</span></span>
   - <span data-ttu-id="a0e86-221">Alan CallerIpAddress CallerIPAddress için değiştirildi</span><span class="sxs-lookup"><span data-stu-id="a0e86-221">Field CallerIpAddress changed to CallerIPAddress</span></span>
   - <span data-ttu-id="a0e86-222">Alan RemoteIPCountry artık mevcut değil</span><span class="sxs-lookup"><span data-stu-id="a0e86-222">Field RemoteIPCountry is no longer present</span></span>
4. <span data-ttu-id="a0e86-223">Kaldırma *anahtar kasası Analytics (kullanım dışı)* çözümü.</span><span class="sxs-lookup"><span data-stu-id="a0e86-223">Remove the *Key Vault Analytics (Deprecated)* solution.</span></span> <span data-ttu-id="a0e86-224">PowerShell kullanıyorsanız, kullanın`Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that the workspace is in> -WorkspaceName <name of the log analytics workspace> -IntelligencePackName "KeyVault" -Enabled $false`</span><span class="sxs-lookup"><span data-stu-id="a0e86-224">If you are using PowerShell, use `Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that the workspace is in> -WorkspaceName <name of the log analytics workspace> -IntelligencePackName "KeyVault" -Enabled $false`</span></span>

<span data-ttu-id="a0e86-225">Değişiklik yeni çözümde görünür değil önce veri toplanmadı.</span><span class="sxs-lookup"><span data-stu-id="a0e86-225">Data collected before the change is not visible in the new solution.</span></span> <span data-ttu-id="a0e86-226">Eski türü ve alan adları kullanarak bu verileri sorgulamak devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a0e86-226">You can continue to query for this data using the old Type and field names.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="a0e86-227">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="a0e86-227">Troubleshooting</span></span>
[!INCLUDE [log-analytics-troubleshoot-azure-diagnostics](../../includes/log-analytics-troubleshoot-azure-diagnostics.md)]

## <a name="next-steps"></a><span data-ttu-id="a0e86-228">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a0e86-228">Next steps</span></span>
* <span data-ttu-id="a0e86-229">Kullanım [günlük analizi aramaları oturum](log-analytics-log-searches.md) ayrıntılı Azure anahtar kasası verileri görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="a0e86-229">Use [Log searches in Log Analytics](log-analytics-log-searches.md) to view detailed Azure Key Vault data.</span></span>
