---
title: "aaaView Azure etkinlik günlükleri toomonitor kaynakları | Microsoft Docs"
description: "Merhaba etkinlik günlükleri tooreview kullanıcı eylemleri ve hataları kullanın. Azure Portal PowerShell, Azure CLI ve REST gösterir."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: fcdb3125-13ce-4c3b-9087-f514c5e41e73
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: tomfitz
ms.openlocfilehash: 8430ed2a9c1dfe5f13423a55d358e590b0facb22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="view-activity-logs-tooaudit-actions-on-resources"></a><span data-ttu-id="31da5-104">Etkinliği Görüntüle kaynaklardaki tooaudit eylemlerini günlüğe kaydeder</span><span class="sxs-lookup"><span data-stu-id="31da5-104">View activity logs tooaudit actions on resources</span></span>
<span data-ttu-id="31da5-105">Etkinlik günlükleri, belirleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="31da5-105">Through activity logs, you can determine:</span></span>

* <span data-ttu-id="31da5-106">hangi işlemlerin aboneliğinizde hello kaynaklar üzerinde gerçekleştirilen</span><span class="sxs-lookup"><span data-stu-id="31da5-106">what operations were taken on hello resources in your subscription</span></span>
* <span data-ttu-id="31da5-107">(bir arka uç hizmeti tarafından başlatılan işlemleri bir kullanıcı olarak hello çağıran döndürmeyen rağmen) hello işlemi kimin başlattığını</span><span class="sxs-lookup"><span data-stu-id="31da5-107">who initiated hello operation (although operations initiated by a backend service do not return a user as hello caller)</span></span>
* <span data-ttu-id="31da5-108">Ne zaman hello işlemi oluştu</span><span class="sxs-lookup"><span data-stu-id="31da5-108">when hello operation occurred</span></span>
* <span data-ttu-id="31da5-109">Merhaba işlem Hello durumu</span><span class="sxs-lookup"><span data-stu-id="31da5-109">hello status of hello operation</span></span>
* <span data-ttu-id="31da5-110">Merhaba işlemi yardımcı olabilecek diğer özelliklerin değerlerine Hello araştırma</span><span class="sxs-lookup"><span data-stu-id="31da5-110">hello values of other properties that might help you research hello operation</span></span>

[!INCLUDE [resource-manager-audit-limitations](../../includes/resource-manager-audit-limitations.md)]

<span data-ttu-id="31da5-111">Merhaba portal, PowerShell, Azure CLI, Öngörüler REST API'si aracılığıyla hello etkinlik günlüklerindeki bilgi almak veya [Öngörüler .NET kitaplığı](https://www.nuget.org/packages/Microsoft.Azure.Insights/).</span><span class="sxs-lookup"><span data-stu-id="31da5-111">You can retrieve information from hello activity logs through hello portal, PowerShell, Azure CLI, Insights REST API, or [Insights .NET Library](https://www.nuget.org/packages/Microsoft.Azure.Insights/).</span></span>

## <a name="portal"></a><span data-ttu-id="31da5-112">Portal</span><span class="sxs-lookup"><span data-stu-id="31da5-112">Portal</span></span>
1. <span data-ttu-id="31da5-113">tooview hello etkinlik günlükleri hello portal üzerinden seçin **İzleyici**.</span><span class="sxs-lookup"><span data-stu-id="31da5-113">tooview hello activity logs through hello portal, select **Monitor**.</span></span>
   
    ![etkinlik günlükleri seçin](./media/resource-group-audit/select-monitor.png)

   <span data-ttu-id="31da5-115">Veya, tooautomatically filtre hello etkinlik günlüğü belirli kaynak veya kaynak grubu, select **etkinlik günlüğü** bu kaynak dikey penceresinden.</span><span class="sxs-lookup"><span data-stu-id="31da5-115">Or, tooautomatically filter hello activity log for a particular resource or resource group, select **Activity log** from that resource blade.</span></span> <span data-ttu-id="31da5-116">Bu hello etkinlik günlüğü seçili hello kaynak tarafından otomatik olarak filtrelenir dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="31da5-116">Notice that hello activity log is automatically filtered by hello selected resource.</span></span>
   
    ![Kaynağa göre filtrele](./media/resource-group-audit/filtered-by-resource.png)
2. <span data-ttu-id="31da5-118">Merhaba, **etkinlik günlüğü** dikey penceresinde, son işlemleri özetini bakın.</span><span class="sxs-lookup"><span data-stu-id="31da5-118">In hello **Activity Log** blade, you see a summary of recent operations.</span></span>
   
    ![Eylemler Göster](./media/resource-group-audit/audit-summary.png)
3. <span data-ttu-id="31da5-120">toorestrict hello görüntülenen işlemlerinin sayısı farklı koşullar seçin.</span><span class="sxs-lookup"><span data-stu-id="31da5-120">toorestrict hello number of operations displayed, select different conditions.</span></span> <span data-ttu-id="31da5-121">Örneğin, hello aşağıdaki görüntüde hello gösterir **Timespan** ve **olayı başlatan tarafından** alanları belirli kullanıcı veya uygulamanın hello geçen ay tarafından yapılan tooview hello Eylemler değiştirildi.</span><span class="sxs-lookup"><span data-stu-id="31da5-121">For example, hello following image shows hello **Timespan** and **Event initiated by** fields changed tooview hello actions taken by a particular user or application for hello past month.</span></span> <span data-ttu-id="31da5-122">Seçin **Uygula** tooview hello Sorgunuzun sonuçlarını.</span><span class="sxs-lookup"><span data-stu-id="31da5-122">Select **Apply** tooview hello results of your query.</span></span>
   
    ![filtre seçeneklerini ayarlama](./media/resource-group-audit/set-filter.png)

4. <span data-ttu-id="31da5-124">Toorun hello sorgu daha sonra yeniden gereksinim duyarsanız, seçin **kaydetmek** ve hello sorgu bir ad verin.</span><span class="sxs-lookup"><span data-stu-id="31da5-124">If you need toorun hello query again later, select **Save** and give hello query a name.</span></span>
   
    ![Sorgu kaydetme](./media/resource-group-audit/save-query.png)
5. <span data-ttu-id="31da5-126">bir sorgu çalıştırın tooquickly dağıtımları başarısız gibi hello yerleşik sorguları birini seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="31da5-126">tooquickly run a query, you can select one of hello built-in queries, such as failed deployments.</span></span>

    ![seçme sorgusu](./media/resource-group-audit/select-quick-query.png)

   <span data-ttu-id="31da5-128">Merhaba seçili sorgu gerekli hello filtre değerleri otomatik olarak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="31da5-128">hello selected query automatically sets hello required filter values.</span></span>

    ![Dağıtım hataları görüntüleme](./media/resource-group-audit/view-failed-deployment.png)   

6. <span data-ttu-id="31da5-130">Merhaba işlemleri toosee hello olay özetini birini seçin.</span><span class="sxs-lookup"><span data-stu-id="31da5-130">Select one of hello operations toosee a summary of hello event.</span></span>

    ![Görünüm işlemi](./media/resource-group-audit/view-operation.png)  

## <a name="powershell"></a><span data-ttu-id="31da5-132">PowerShell</span><span class="sxs-lookup"><span data-stu-id="31da5-132">PowerShell</span></span>
1. <span data-ttu-id="31da5-133">Merhaba çalıştırmak tooretrieve günlük girişlerini **Get-AzureRmLog** komutu.</span><span class="sxs-lookup"><span data-stu-id="31da5-133">tooretrieve log entries, run hello **Get-AzureRmLog** command.</span></span> <span data-ttu-id="31da5-134">Ek parametreler toofilter hello girişlerinin listesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="31da5-134">You provide additional parameters toofilter hello list of entries.</span></span> <span data-ttu-id="31da5-135">Bir başlangıç ve bitiş zamanı belirtmezseniz hello son bir saat girişlerinde döndürülür.</span><span class="sxs-lookup"><span data-stu-id="31da5-135">If you do not specify a start and end time, entries for hello last hour are returned.</span></span> <span data-ttu-id="31da5-136">Örneğin, bir kaynak grubu için tooretrieve hello işlemleri sırasında hello son bir saat çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="31da5-136">For example, tooretrieve hello operations for a resource group during hello past hour run:</span></span>

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup
  ```
   
    <span data-ttu-id="31da5-137">Aşağıdaki örneğine hello nasıl toouse hello etkinlik oturum belirtilen süre boyunca gerçekleştirilecek tooresearch işlemleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="31da5-137">hello following example shows how toouse hello activity log tooresearch operations taken during a specified time.</span></span> <span data-ttu-id="31da5-138">Merhaba başlangıç ve bitiş tarihleri tarih biçiminde belirtilir.</span><span class="sxs-lookup"><span data-stu-id="31da5-138">hello start and end dates are specified in a date format.</span></span>

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime 2015-08-28T06:00 -EndTime 2015-09-10T06:00
  ```

    <span data-ttu-id="31da5-139">Ya da son 14 gün tarih işlevleri toospecify hello tarih aralığı, hello gibi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="31da5-139">Or, you can use date functions toospecify hello date range, such as hello last 14 days.</span></span>
   
  ```powershell 
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime (Get-Date).AddDays(-14)
  ```

2. <span data-ttu-id="31da5-140">Belirttiğiniz hello başlangıç saati bağlı olarak hello önceki komutları işlemleri hello kaynak grubu için uzun bir listesi döndürebilir.</span><span class="sxs-lookup"><span data-stu-id="31da5-140">Depending on hello start time you specify, hello previous commands can return a long list of operations for hello resource group.</span></span> <span data-ttu-id="31da5-141">Ne arama ölçütlerini sağlayarak aradığınız için hello sonuçları filtreleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="31da5-141">You can filter hello results for what you are looking for by providing search criteria.</span></span> <span data-ttu-id="31da5-142">Örneğin, bir web uygulaması nasıl durduruldu tooresearch çalışıyorsanız, komutu aşağıdaki hello çalıştırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="31da5-142">For example, if you are trying tooresearch how a web app was stopped, you could run hello following command:</span></span>

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime (Get-Date).AddDays(-14) | Where-Object OperationName -eq Microsoft.Web/sites/stop/action
  ```

    <span data-ttu-id="31da5-143">Bu örneğin gösterir durdurma eylemi tarafından gerçekleştirilen someone@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="31da5-143">Which for this example shows that a stop action was performed by someone@contoso.com.</span></span> 

  ```powershell 
  Authorization     :
  Scope     : /subscriptions/xxxxx/resourcegroups/ExampleGroup/providers/Microsoft.Web/sites/ExampleSite
  Action    : Microsoft.Web/sites/stop/action
  Role      : Subscription Admin
  Condition :
  Caller            : someone@contoso.com
  CorrelationId     : 84beae59-92aa-4662-a6fc-b6fecc0ff8da
  EventSource       : Administrative
  EventTimestamp    : 8/28/2015 4:08:18 PM
  OperationName     : Microsoft.Web/sites/stop/action
  ResourceGroupName : ExampleGroup
  ResourceId        : /subscriptions/xxxxx/resourcegroups/ExampleGroup/providers/Microsoft.Web/sites/ExampleSite
  Status            : Succeeded
  SubscriptionId    : xxxxx
  SubStatus         : OK
  ```

3. <span data-ttu-id="31da5-144">Hatta artık mevcut bir kaynak grubu için belirli bir kullanıcı tarafından yapılan hello Eylemler arayabilir.</span><span class="sxs-lookup"><span data-stu-id="31da5-144">You can look up hello actions taken by a particular user, even for a resource group that no longer exists.</span></span>

  ```powershell 
  Get-AzureRmLog -ResourceGroup deletedgroup -StartTime (Get-Date).AddDays(-14) -Caller someone@contoso.com
  ```

4. <span data-ttu-id="31da5-145">Başarısız işlemler için filtre uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="31da5-145">You can filter for failed operations.</span></span>

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -Status Failed
  ```

5. <span data-ttu-id="31da5-146">Bu girişi için hello durum iletisini bakarak bir hatada odaklanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="31da5-146">You can focus on one error by looking at hello status message for that entry.</span></span>
   
        ((Get-AzureRmLog -Status Failed -ResourceGroup ExampleGroup -DetailedOutput).Properties[1].Content["statusMessage"] | ConvertFrom-Json).error
   
    <span data-ttu-id="31da5-147">Hangi döndürür:</span><span class="sxs-lookup"><span data-stu-id="31da5-147">Which returns:</span></span>
   
        code           message                                                                        
        ----           -------                                                                        
        DnsRecordInUse DNS record dns.westus.cloudapp.azure.com is already used by another public IP. 


## <a name="azure-cli"></a><span data-ttu-id="31da5-148">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="31da5-148">Azure CLI</span></span>
* <span data-ttu-id="31da5-149">tooretrieve günlük girişlerini, çalıştırdığınız hello **azure Grup günlük Göster** komutu.</span><span class="sxs-lookup"><span data-stu-id="31da5-149">tooretrieve log entries, you run hello **azure group log show** command.</span></span>

  ```azurecli
  azure group log show ExampleGroup --json
  ```


## <a name="rest-api"></a><span data-ttu-id="31da5-150">REST API</span><span class="sxs-lookup"><span data-stu-id="31da5-150">REST API</span></span>
<span data-ttu-id="31da5-151">Merhaba etkinlik günlüğü ile çalışmaya yönelik hello REST işlemlerini hello parçası olan [Insights REST API](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span><span class="sxs-lookup"><span data-stu-id="31da5-151">hello REST operations for working with hello activity log are part of hello [Insights REST API](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span> <span data-ttu-id="31da5-152">tooretrieve etkinlik günlüğü olaylarını görme [listesinde bir abonelikte hello Yönetimi olayları](https://msdn.microsoft.com/library/azure/dn931934.aspx).</span><span class="sxs-lookup"><span data-stu-id="31da5-152">tooretrieve activity log events, see [List hello management events in a subscription](https://msdn.microsoft.com/library/azure/dn931934.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="31da5-153">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="31da5-153">Next steps</span></span>
* <span data-ttu-id="31da5-154">Azure etkinlik günlükleri, Power BI toogain fazla öngörü aboneliğinizde hello eylemler hakkında ile kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="31da5-154">Azure Activity logs can be used with Power BI toogain greater insights about hello actions in your subscription.</span></span> <span data-ttu-id="31da5-155">Bkz: [Görünüm ve Power BI ve daha fazla Azure etkinlik günlüklerini analiz edin](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/).</span><span class="sxs-lookup"><span data-stu-id="31da5-155">See [View and analyze Azure Activity Logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/).</span></span>
* <span data-ttu-id="31da5-156">güvenlik ilkelerini ayarlama hakkında toolearn bkz [Azure rol tabanlı erişim denetimi](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="31da5-156">toolearn about setting security policies, see [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>
* <span data-ttu-id="31da5-157">toolearn dağıtım işlemlerini görüntülemek için hello komutlar hakkında bkz [görüntülemek dağıtım işlemlerini](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="31da5-157">toolearn about hello commands for viewing deployment operations, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="31da5-158">tooprevent silme tüm kullanıcılar için bir kaynakta nasıl görürüm toolearn [Azure Resource Manager ile kaynakları kilitleme](resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="31da5-158">toolearn how tooprevent deletions on a resource for all users, see [Lock resources with Azure Resource Manager](resource-group-lock-resources.md).</span></span>

