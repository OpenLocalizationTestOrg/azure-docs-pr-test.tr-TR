---
title: "BT Hizmet Yönetimi Bağlayıcısı OMS | Microsoft Docs"
description: "Tüm sorunların hızla çözülmesine ve BT Hizmet Yönetimi Bağlayıcısı merkezi olarak izlemek ve OMS ITSM iş öğelerini yönetmek için kullanın."
services: log-analytics
documentationcenter: 
author: JYOTHIRMAISURI
manager: riyazp
editor: 
ms.assetid: 0b1414d9-b0a7-4e4e-a652-d3a6ff1118c4
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: v-jysur
ms.openlocfilehash: 54974ef06efdae69ddbfa12b1ba9278b48b113d3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="centrally-manage-itsm-work-items-using-it-service-management-connector-preview"></a><span data-ttu-id="ee005-103">ITSM iş öğelerini BT Hizmet Yönetimi Bağlayıcısı (Önizleme) kullanarak merkezi olarak yönetme</span><span class="sxs-lookup"><span data-stu-id="ee005-103">Centrally manage ITSM work items using IT Service Management Connector (Preview)</span></span>

![BT Hizmet Yönetimi Bağlayıcısı simgesi](./media/log-analytics-itsmc/itsmc-symbol.png)

<span data-ttu-id="ee005-105">Merkezi olarak izlemek ve ITSM ürünler/hizmetlerinizi arasında iş öğelerini yönetmek için OMS günlük analizi BT Hizmet Yönetimi Bağlayıcısı'nı (ITSMC) kullanın.</span><span class="sxs-lookup"><span data-stu-id="ee005-105">You can use the IT Service Management Connector (ITSMC) in OMS Log Analytics to centrally monitor and manage work items across your ITSM products/services.</span></span>

<span data-ttu-id="ee005-106">BT Hizmet Yönetimi Bağlayıcısı var olan BT Hizmet Yönetimi (ITSM) ürünleri ve Hizmetleri OMS günlük analizi ile tümleşir.</span><span class="sxs-lookup"><span data-stu-id="ee005-106">The IT Service Management Connector integrates your existing IT Service Management (ITSM) products and services with OMS Log Analytics.</span></span>  <span data-ttu-id="ee005-107">Çözümü OMS kullanıcılar ITSM çözümde olaylar, uyarılar ya da olaylar oluşturmak için bir seçenek sağladığı ITSM ürünler/hizmetler ile çift yönlü tümleştirme vardır.</span><span class="sxs-lookup"><span data-stu-id="ee005-107">The solution has bidirectional integration with ITSM products/services, where it provides the OMS users an option to create incidents, alerts, or events in ITSM solution.</span></span> <span data-ttu-id="ee005-108">Bağlayıcı da olaylar gibi verileri içe aktaran ve OMS günlük analizi ITSM çözümden değişiklik istekleri.</span><span class="sxs-lookup"><span data-stu-id="ee005-108">The connector also  imports data such as incidents, and change requests from ITSM solution into OMS Log Analytics.</span></span>

<span data-ttu-id="ee005-109">BT Hizmet Yönetimi Bağlayıcısı ile şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ee005-109">With IT Service Management Connector, you can:</span></span>

  - <span data-ttu-id="ee005-110">Merkezi olarak izlemek ve iş öğeleri için ITSM ürünler/hizmetler kuruluşunuz genelinde kullanılan yönetin.</span><span class="sxs-lookup"><span data-stu-id="ee005-110">Centrally monitor and manage work items for ITSM products/services used across your organization.</span></span>
  - <span data-ttu-id="ee005-111">ITSM iş öğeleri (örneğin, uyarı, olay, olay) içinde ITSM OMS uyarılardan ve günlük arama aracılığıyla oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ee005-111">Create ITSM work items (like alert, event, incident) in ITSM from OMS alerts and through log search.</span></span>
  - <span data-ttu-id="ee005-112">Olayları okuma ve ITSM çözümünüzden değişiklik istekleri ve ilgili günlük veri günlük analizi çalışma alanındaki ile ilişkilendirilmesi.</span><span class="sxs-lookup"><span data-stu-id="ee005-112">Read incidents and change requests from your ITSM solution and correlate with relevant log data in Log Analytics workspace.</span></span>
  - <span data-ttu-id="ee005-113">Beklenmeyen ve olağan dışı olayları bulmak ve son kullanıcılar çağırın ve Yardım için rapor bile önce bunları çözün.</span><span class="sxs-lookup"><span data-stu-id="ee005-113">Find any unexpected and unusual events and resolve them, even before the end users call and report them to the helpdesk.</span></span>
  - <span data-ttu-id="ee005-114">İş öğeleri veri günlük analizi alabilir ve ana performans göstergesi (KPI) raporları oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ee005-114">Import work items data into Log Analytics and create key performance indicator (KPI) reports.</span></span>  <span data-ttu-id="ee005-115">Bu raporları kullanarak, tanımlayabilir, değerlendirmek ve kötü amaçlı yazılım değerlendirmesi gibi birkaç önemli öğe hareket.</span><span class="sxs-lookup"><span data-stu-id="ee005-115">Using these reports, you can identify, assess and act on several important items such as malware assessment.</span></span>
  - <span data-ttu-id="ee005-116">Daha ayrıntılı Öngörüler için seçkin panolar üzerinde olayları görüntülemek için değişiklik istekleri ve etkilenen sistemler.</span><span class="sxs-lookup"><span data-stu-id="ee005-116">View curated dashboards for deeper insights on incidents, change requests and impacted systems.</span></span>
  - <span data-ttu-id="ee005-117">Daha hızlı günlük analizi çalışma alanındaki diğer yönetim çözümleri ile ilişkilendirilmesi yoluyla sorunlarını giderin.</span><span class="sxs-lookup"><span data-stu-id="ee005-117">Troubleshoot faster by correlating with other management solutions in the Log Analytics workspace.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="ee005-118">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="ee005-118">Prerequisites</span></span>

<span data-ttu-id="ee005-119">OMS günlük analizi ITSM iş öğelerini almak için çözüm OMS BT Hizmet Yönetimi bağlayıcıda ve iş öğeleri içeri aktarma BT SM Ürün/hizmet arasında bir bağlantı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="ee005-119">To import the ITSM work items into OMS Log Analytics, the solution requires a connection between the IT Service Management Connector in the OMS and the IT SM product/service from which you import the work items.</span></span>


## <a name="configuration"></a><span data-ttu-id="ee005-120">Yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ee005-120">Configuration</span></span>

<span data-ttu-id="ee005-121">BT Hizmet Yönetimi Bağlayıcısı çözüm açıklanan işlemi kullanarak OMS çalışma alanınıza ekleyin [Çözümleri Galerisi eklemek günlük analizi çözümleri](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="ee005-121">Add the IT Service Management Connector solution to your OMS work space, using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>

<span data-ttu-id="ee005-122">BT Hizmet Yönetimi Bağlayıcısı çözümleri Galerisi'nde gördüğünüz gibi döşeme:</span><span class="sxs-lookup"><span data-stu-id="ee005-122">IT Service Management Connector tile as you see in the Solutions gallery:</span></span>

![Bağlayıcı döşeme](./media/log-analytics-itsmc/itsmc-solutions-tile.png)

<span data-ttu-id="ee005-124">Başarılı ayrıca sonra BT Hizmet Yönetimi Bağlayıcısı altında görürsünüz **OMS** > **ayarları** > **bağlı kaynakları.**</span><span class="sxs-lookup"><span data-stu-id="ee005-124">After successful addition, you will see the IT Service Management Connector under **OMS** > **Settings** > **Connected Sources.**</span></span>

![Bağlı ITSMC](./media/log-analytics-itsmc/itsmc-overview-solution-in-connected-sources.png)

> [!NOTE]

> <span data-ttu-id="ee005-126">Varsayılan olarak, BT Hizmet Yönetimi Bağlayıcısı her 24 saatte bağlantının verileri yeniler.</span><span class="sxs-lookup"><span data-stu-id="ee005-126">By default, the IT Service Management Connector refreshes the connection's data once in every 24 hours.</span></span> <span data-ttu-id="ee005-127">Hemen tüm düzenlemeler veya şablon için bağlantının verileri yenilemek için bağlantınızı yanında görüntülenen Yenile düğmesini tıklatın yaptığınız güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="ee005-127">To refresh your connection's data instantly for any edits or template updates that you make, click the refresh button displayed next to your connection.</span></span>

 ![ITSMC Yenile](./media/log-analytics-itsmc/itsmc-connection-refresh.png)

## <a name="management-packs"></a><span data-ttu-id="ee005-129">Yönetim paketleri</span><span class="sxs-lookup"><span data-stu-id="ee005-129">Management packs</span></span>
<span data-ttu-id="ee005-130">Bu çözüm, herhangi bir Yönetim Paketi gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="ee005-130">This solution does not require any management packs.</span></span>

## <a name="connected-sources"></a><span data-ttu-id="ee005-131">Bağlı kaynaklar</span><span class="sxs-lookup"><span data-stu-id="ee005-131">Connected sources</span></span>

<span data-ttu-id="ee005-132">Aşağıdaki ITSM ürünler/hizmetler BT Hizmet Yönetimi Bağlayıcısı tarafından desteklenir:</span><span class="sxs-lookup"><span data-stu-id="ee005-132">The following ITSM products/services are supported by the IT Service Management Connector:</span></span>

- [<span data-ttu-id="ee005-133">System Center Service Manager (SCSM)</span><span class="sxs-lookup"><span data-stu-id="ee005-133">System Center Service Manager (SCSM)</span></span>](log-analytics-itsmc-connections.md#connect-system-center-service-manager-to-it-service-management-connector-in-oms)

- [<span data-ttu-id="ee005-134">ServiceNow</span><span class="sxs-lookup"><span data-stu-id="ee005-134">ServiceNow</span></span>](log-analytics-itsmc-connections.md#connect-servicenow-to-it-service-management-connector-in-oms)

- [<span data-ttu-id="ee005-135">Provance</span><span class="sxs-lookup"><span data-stu-id="ee005-135">Provance</span></span>](log-analytics-itsmc-connections.md#connect-provance-to-it-service-management-connector-in-oms)  

- [<span data-ttu-id="ee005-136">Cherwell</span><span class="sxs-lookup"><span data-stu-id="ee005-136">Cherwell</span></span>](log-analytics-itsmc-connections.md#connect-cherwell-to-it-service-management-connector-in-oms)

## <a name="using-the-solution"></a><span data-ttu-id="ee005-137">Çözümü kullanma</span><span class="sxs-lookup"><span data-stu-id="ee005-137">Using the solution</span></span>

<span data-ttu-id="ee005-138">OMS BT Hizmet Yönetimi Bağlayıcısı ITSM hizmetiniz ile bağladıktan sonra günlük analizi Hizmetleri başlatılır bağlı ITSM ürünler/hizmetinden veri toplama.</span><span class="sxs-lookup"><span data-stu-id="ee005-138">Once you connect the OMS IT Service Management Connector with your ITSM service, the Log Analytics services starts gathering the data from the connected ITSM products/service.</span></span>

> [!NOTE]
> - <span data-ttu-id="ee005-139">BT Hizmet Yönetimi Bağlayıcısı çözümü tarafından alınan veri olayların adlı günlük analizi görünür **ServiceDesk_CL**.</span><span class="sxs-lookup"><span data-stu-id="ee005-139">Data imported by IT Service Management Connector solution appears in Log Analytics as events named **ServiceDesk_CL**.</span></span>
- <span data-ttu-id="ee005-140">Olay adında bir alan içeriyor **ServiceDeskWorkItemType_s**.</span><span class="sxs-lookup"><span data-stu-id="ee005-140">Event contains a field named **ServiceDeskWorkItemType_s**.</span></span> <span data-ttu-id="ee005-141">hangi olay değeri alın veya değişiklik isteği içinde yer alan iş öğesi verilerine bağlı olarak **ServiceDesk_CL** olay.</span><span class="sxs-lookup"><span data-stu-id="ee005-141">which can take its value as incident, or change request, depending on the work item data contained in the **ServiceDesk_CL** event.</span></span>

## <a name="input-data"></a><span data-ttu-id="ee005-142">Giriş verisi</span><span class="sxs-lookup"><span data-stu-id="ee005-142">Input data</span></span>
<span data-ttu-id="ee005-143">İş öğeleri ITSM ürünler/hizmetlerinden içeri aktarılan.</span><span class="sxs-lookup"><span data-stu-id="ee005-143">Work items imported from the ITSM products/services.</span></span>

<span data-ttu-id="ee005-144">Aşağıdaki bilgiler BT Hizmet Yönetimi Bağlayıcısı tarafından toplanan veri örnekleri gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="ee005-144">The following information shows examples of data gathered by the IT Service Management connector:</span></span>

> [!NOTE]
> <span data-ttu-id="ee005-145">İş öğesi türüne bağlı olarak günlük analizi içeri **ServiceDesk_CL** aşağıdaki alanları içerir:</span><span class="sxs-lookup"><span data-stu-id="ee005-145">Depending on the work item type imported into Log Analytics, **ServiceDesk_CL** contains the following fields:</span></span>

<span data-ttu-id="ee005-146">**İş öğesi:** **olaylar**</span><span class="sxs-lookup"><span data-stu-id="ee005-146">**Work item:** **Incidents**</span></span>  
<span data-ttu-id="ee005-147">ServiceDeskWorkItemType_s "Olay" =</span><span class="sxs-lookup"><span data-stu-id="ee005-147">ServiceDeskWorkItemType_s="Incident"</span></span>

<span data-ttu-id="ee005-148">**Alanları**</span><span class="sxs-lookup"><span data-stu-id="ee005-148">**Fields**</span></span>

- <span data-ttu-id="ee005-149">ServiceDeskConnectionName</span><span class="sxs-lookup"><span data-stu-id="ee005-149">ServiceDeskConnectionName</span></span>
- <span data-ttu-id="ee005-150">Hizmet Masası kimliği</span><span class="sxs-lookup"><span data-stu-id="ee005-150">Service Desk ID</span></span>
- <span data-ttu-id="ee005-151">Durum</span><span class="sxs-lookup"><span data-stu-id="ee005-151">State</span></span>
- <span data-ttu-id="ee005-152">Aciliyet</span><span class="sxs-lookup"><span data-stu-id="ee005-152">Urgency</span></span>
- <span data-ttu-id="ee005-153">Etkisi</span><span class="sxs-lookup"><span data-stu-id="ee005-153">Impact</span></span>
- <span data-ttu-id="ee005-154">Öncelik</span><span class="sxs-lookup"><span data-stu-id="ee005-154">Priority</span></span>
- <span data-ttu-id="ee005-155">Yükseltme</span><span class="sxs-lookup"><span data-stu-id="ee005-155">Escalation</span></span>
- <span data-ttu-id="ee005-156">Tarafından oluşturulan</span><span class="sxs-lookup"><span data-stu-id="ee005-156">Created By</span></span>
- <span data-ttu-id="ee005-157">Çözümleyen</span><span class="sxs-lookup"><span data-stu-id="ee005-157">Resolved By</span></span>
- <span data-ttu-id="ee005-158">Tarafından kapatıldı</span><span class="sxs-lookup"><span data-stu-id="ee005-158">Closed By</span></span>
- <span data-ttu-id="ee005-159">Kaynak</span><span class="sxs-lookup"><span data-stu-id="ee005-159">Source</span></span>
- <span data-ttu-id="ee005-160">Atanan</span><span class="sxs-lookup"><span data-stu-id="ee005-160">Assigned To</span></span>
- <span data-ttu-id="ee005-161">Kategori</span><span class="sxs-lookup"><span data-stu-id="ee005-161">Category</span></span>
- <span data-ttu-id="ee005-162">Başlık</span><span class="sxs-lookup"><span data-stu-id="ee005-162">Title</span></span>
- <span data-ttu-id="ee005-163">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ee005-163">Description</span></span>
- <span data-ttu-id="ee005-164">Oluşturulma tarihi</span><span class="sxs-lookup"><span data-stu-id="ee005-164">Created Date</span></span>
- <span data-ttu-id="ee005-165">Kapatılma tarihi</span><span class="sxs-lookup"><span data-stu-id="ee005-165">Closed Date</span></span>
- <span data-ttu-id="ee005-166">Çözümlenme tarihi</span><span class="sxs-lookup"><span data-stu-id="ee005-166">Resolved Date</span></span>
- <span data-ttu-id="ee005-167">Son değiştirilme tarihi</span><span class="sxs-lookup"><span data-stu-id="ee005-167">Last Modified Date</span></span>
- <span data-ttu-id="ee005-168">Bilgisayar</span><span class="sxs-lookup"><span data-stu-id="ee005-168">Computer</span></span>


<span data-ttu-id="ee005-169">**İş öğesi:** **değişiklik istekleri**</span><span class="sxs-lookup"><span data-stu-id="ee005-169">**Work item:** **Change Requests**</span></span>

<span data-ttu-id="ee005-170">ServiceDeskWorkItemType_s "ChangeRequest" =</span><span class="sxs-lookup"><span data-stu-id="ee005-170">ServiceDeskWorkItemType_s="ChangeRequest"</span></span>

<span data-ttu-id="ee005-171">**Alanları**</span><span class="sxs-lookup"><span data-stu-id="ee005-171">**Fields**</span></span>
- <span data-ttu-id="ee005-172">ServiceDeskConnectionName</span><span class="sxs-lookup"><span data-stu-id="ee005-172">ServiceDeskConnectionName</span></span>
- <span data-ttu-id="ee005-173">Hizmet Masası kimliği</span><span class="sxs-lookup"><span data-stu-id="ee005-173">Service Desk ID</span></span>
- <span data-ttu-id="ee005-174">Tarafından oluşturulan</span><span class="sxs-lookup"><span data-stu-id="ee005-174">Created By</span></span>
- <span data-ttu-id="ee005-175">Tarafından kapatıldı</span><span class="sxs-lookup"><span data-stu-id="ee005-175">Closed By</span></span>
- <span data-ttu-id="ee005-176">Kaynak</span><span class="sxs-lookup"><span data-stu-id="ee005-176">Source</span></span>
- <span data-ttu-id="ee005-177">Atanan</span><span class="sxs-lookup"><span data-stu-id="ee005-177">Assigned To</span></span>
- <span data-ttu-id="ee005-178">Başlık</span><span class="sxs-lookup"><span data-stu-id="ee005-178">Title</span></span>
- <span data-ttu-id="ee005-179">Tür</span><span class="sxs-lookup"><span data-stu-id="ee005-179">Type</span></span>
- <span data-ttu-id="ee005-180">Kategori</span><span class="sxs-lookup"><span data-stu-id="ee005-180">Category</span></span>
- <span data-ttu-id="ee005-181">Durum</span><span class="sxs-lookup"><span data-stu-id="ee005-181">State</span></span>
- <span data-ttu-id="ee005-182">Yükseltme</span><span class="sxs-lookup"><span data-stu-id="ee005-182">Escalation</span></span>
- <span data-ttu-id="ee005-183">Çakışma durumu</span><span class="sxs-lookup"><span data-stu-id="ee005-183">Conflict Status</span></span>
- <span data-ttu-id="ee005-184">Aciliyet</span><span class="sxs-lookup"><span data-stu-id="ee005-184">Urgency</span></span>
- <span data-ttu-id="ee005-185">Öncelik</span><span class="sxs-lookup"><span data-stu-id="ee005-185">Priority</span></span>
- <span data-ttu-id="ee005-186">Riski</span><span class="sxs-lookup"><span data-stu-id="ee005-186">Risk</span></span>
- <span data-ttu-id="ee005-187">Etkisi</span><span class="sxs-lookup"><span data-stu-id="ee005-187">Impact</span></span>
- <span data-ttu-id="ee005-188">Atanan</span><span class="sxs-lookup"><span data-stu-id="ee005-188">Assigned To</span></span>
- <span data-ttu-id="ee005-189">Oluşturulma tarihi</span><span class="sxs-lookup"><span data-stu-id="ee005-189">Created Date</span></span>
- <span data-ttu-id="ee005-190">Kapatılma tarihi</span><span class="sxs-lookup"><span data-stu-id="ee005-190">Closed Date</span></span>
- <span data-ttu-id="ee005-191">Son değiştirilme tarihi</span><span class="sxs-lookup"><span data-stu-id="ee005-191">Last Modified Date</span></span>
- <span data-ttu-id="ee005-192">İstenen tarih</span><span class="sxs-lookup"><span data-stu-id="ee005-192">Requested Date</span></span>
- <span data-ttu-id="ee005-193">Planlanan başlangıç tarihi</span><span class="sxs-lookup"><span data-stu-id="ee005-193">Planned Start Date</span></span>
- <span data-ttu-id="ee005-194">Planlanan bitiş tarihi</span><span class="sxs-lookup"><span data-stu-id="ee005-194">Planned End Date</span></span>
- <span data-ttu-id="ee005-195">İş başlangıç tarihi</span><span class="sxs-lookup"><span data-stu-id="ee005-195">Work Start Date</span></span>
- <span data-ttu-id="ee005-196">İş bitiş tarihi</span><span class="sxs-lookup"><span data-stu-id="ee005-196">Work End Date</span></span>
- <span data-ttu-id="ee005-197">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ee005-197">Description</span></span>
- <span data-ttu-id="ee005-198">Bilgisayar</span><span class="sxs-lookup"><span data-stu-id="ee005-198">Computer</span></span>

## <a name="output-data-for-a-servicenow-incident"></a><span data-ttu-id="ee005-199">ServiceNow olay için çıktı verileri</span><span class="sxs-lookup"><span data-stu-id="ee005-199">Output data for a ServiceNow incident</span></span>

| <span data-ttu-id="ee005-200">OMS alan</span><span class="sxs-lookup"><span data-stu-id="ee005-200">OMS field</span></span> | <span data-ttu-id="ee005-201">ITSM alan</span><span class="sxs-lookup"><span data-stu-id="ee005-201">ITSM field</span></span> |
|:--- |:--- |
| <span data-ttu-id="ee005-202">ServiceDeskId_s</span><span class="sxs-lookup"><span data-stu-id="ee005-202">ServiceDeskId_s</span></span>| <span data-ttu-id="ee005-203">Sayı</span><span class="sxs-lookup"><span data-stu-id="ee005-203">Number</span></span> |
| <span data-ttu-id="ee005-204">IncidentState_s</span><span class="sxs-lookup"><span data-stu-id="ee005-204">IncidentState_s</span></span> | <span data-ttu-id="ee005-205">Durum</span><span class="sxs-lookup"><span data-stu-id="ee005-205">State</span></span> |
| <span data-ttu-id="ee005-206">Urgency_s</span><span class="sxs-lookup"><span data-stu-id="ee005-206">Urgency_s</span></span> |<span data-ttu-id="ee005-207">Aciliyet</span><span class="sxs-lookup"><span data-stu-id="ee005-207">Urgency</span></span> |
| <span data-ttu-id="ee005-208">Impact_s</span><span class="sxs-lookup"><span data-stu-id="ee005-208">Impact_s</span></span> |<span data-ttu-id="ee005-209">Etkisi</span><span class="sxs-lookup"><span data-stu-id="ee005-209">Impact</span></span>|
| <span data-ttu-id="ee005-210">Priority_s</span><span class="sxs-lookup"><span data-stu-id="ee005-210">Priority_s</span></span> | <span data-ttu-id="ee005-211">Öncelik</span><span class="sxs-lookup"><span data-stu-id="ee005-211">Priority</span></span> |
| <span data-ttu-id="ee005-212">CreatedBy_s</span><span class="sxs-lookup"><span data-stu-id="ee005-212">CreatedBy_s</span></span> | <span data-ttu-id="ee005-213">Tarafından açılmış</span><span class="sxs-lookup"><span data-stu-id="ee005-213">Opened by</span></span> |
| <span data-ttu-id="ee005-214">ResolvedBy_s</span><span class="sxs-lookup"><span data-stu-id="ee005-214">ResolvedBy_s</span></span> | <span data-ttu-id="ee005-215">Çözümleyen</span><span class="sxs-lookup"><span data-stu-id="ee005-215">Resolved by</span></span>|
| <span data-ttu-id="ee005-216">ClosedBy_s</span><span class="sxs-lookup"><span data-stu-id="ee005-216">ClosedBy_s</span></span>  | <span data-ttu-id="ee005-217">Tarafından kapatıldı</span><span class="sxs-lookup"><span data-stu-id="ee005-217">Closed by</span></span> |
| <span data-ttu-id="ee005-218">Source_s</span><span class="sxs-lookup"><span data-stu-id="ee005-218">Source_s</span></span>| <span data-ttu-id="ee005-219">İlgili kişi türü</span><span class="sxs-lookup"><span data-stu-id="ee005-219">Contact type</span></span> |
| <span data-ttu-id="ee005-220">AssignedTo_s</span><span class="sxs-lookup"><span data-stu-id="ee005-220">AssignedTo_s</span></span> | <span data-ttu-id="ee005-221">Atanan</span><span class="sxs-lookup"><span data-stu-id="ee005-221">Assigned to</span></span>  |
| <span data-ttu-id="ee005-222">Category_s</span><span class="sxs-lookup"><span data-stu-id="ee005-222">Category_s</span></span> | <span data-ttu-id="ee005-223">Kategori</span><span class="sxs-lookup"><span data-stu-id="ee005-223">Category</span></span> |
| <span data-ttu-id="ee005-224">Title_s</span><span class="sxs-lookup"><span data-stu-id="ee005-224">Title_s</span></span>|  <span data-ttu-id="ee005-225">Kısa açıklama</span><span class="sxs-lookup"><span data-stu-id="ee005-225">Short description</span></span> |
| <span data-ttu-id="ee005-226">Description_s</span><span class="sxs-lookup"><span data-stu-id="ee005-226">Description_s</span></span>|  <span data-ttu-id="ee005-227">Notlar</span><span class="sxs-lookup"><span data-stu-id="ee005-227">Notes</span></span> |
| <span data-ttu-id="ee005-228">CreatedDate_t</span><span class="sxs-lookup"><span data-stu-id="ee005-228">CreatedDate_t</span></span>|  <span data-ttu-id="ee005-229">Açılan</span><span class="sxs-lookup"><span data-stu-id="ee005-229">Opened</span></span> |
| <span data-ttu-id="ee005-230">ClosedDate_t</span><span class="sxs-lookup"><span data-stu-id="ee005-230">ClosedDate_t</span></span>| <span data-ttu-id="ee005-231">Kapalı</span><span class="sxs-lookup"><span data-stu-id="ee005-231">closed</span></span>|
| <span data-ttu-id="ee005-232">ResolvedDate_t</span><span class="sxs-lookup"><span data-stu-id="ee005-232">ResolvedDate_t</span></span>|<span data-ttu-id="ee005-233">Çözümlendi</span><span class="sxs-lookup"><span data-stu-id="ee005-233">Resolved</span></span>|
| <span data-ttu-id="ee005-234">Bilgisayar</span><span class="sxs-lookup"><span data-stu-id="ee005-234">Computer</span></span>  | <span data-ttu-id="ee005-235">Yapılandırma öğesi</span><span class="sxs-lookup"><span data-stu-id="ee005-235">Configuration item</span></span> |

## <a name="output-data-for-a-servicenow-change-request"></a><span data-ttu-id="ee005-236">Çıktı verileri bir ServiceNow için değişiklik isteği</span><span class="sxs-lookup"><span data-stu-id="ee005-236">Output data for a ServiceNow change request</span></span>

| <span data-ttu-id="ee005-237">OMS alan</span><span class="sxs-lookup"><span data-stu-id="ee005-237">OMS field</span></span> | <span data-ttu-id="ee005-238">ITSM alan</span><span class="sxs-lookup"><span data-stu-id="ee005-238">ITSM field</span></span> |
|:--- |:--- |
| <span data-ttu-id="ee005-239">ServiceDeskId_s</span><span class="sxs-lookup"><span data-stu-id="ee005-239">ServiceDeskId_s</span></span>| <span data-ttu-id="ee005-240">Sayı</span><span class="sxs-lookup"><span data-stu-id="ee005-240">Number</span></span> |
| <span data-ttu-id="ee005-241">CreatedBy_s</span><span class="sxs-lookup"><span data-stu-id="ee005-241">CreatedBy_s</span></span> | <span data-ttu-id="ee005-242">Tarafından istenen</span><span class="sxs-lookup"><span data-stu-id="ee005-242">Requested by</span></span> |
| <span data-ttu-id="ee005-243">ClosedBy_s</span><span class="sxs-lookup"><span data-stu-id="ee005-243">ClosedBy_s</span></span> | <span data-ttu-id="ee005-244">Tarafından kapatıldı</span><span class="sxs-lookup"><span data-stu-id="ee005-244">Closed by</span></span> |
| <span data-ttu-id="ee005-245">AssignedTo_s</span><span class="sxs-lookup"><span data-stu-id="ee005-245">AssignedTo_s</span></span> | <span data-ttu-id="ee005-246">Atanan</span><span class="sxs-lookup"><span data-stu-id="ee005-246">Assigned to</span></span>  |
| <span data-ttu-id="ee005-247">Title_s</span><span class="sxs-lookup"><span data-stu-id="ee005-247">Title_s</span></span>|  <span data-ttu-id="ee005-248">Kısa açıklama</span><span class="sxs-lookup"><span data-stu-id="ee005-248">Short description</span></span> |
| <span data-ttu-id="ee005-249">Type_s</span><span class="sxs-lookup"><span data-stu-id="ee005-249">Type_s</span></span>|  <span data-ttu-id="ee005-250">Tür</span><span class="sxs-lookup"><span data-stu-id="ee005-250">Type</span></span> |
| <span data-ttu-id="ee005-251">Category_s</span><span class="sxs-lookup"><span data-stu-id="ee005-251">Category_s</span></span>|  <span data-ttu-id="ee005-252">Catgory</span><span class="sxs-lookup"><span data-stu-id="ee005-252">Catgory</span></span> |
| <span data-ttu-id="ee005-253">CRState_s</span><span class="sxs-lookup"><span data-stu-id="ee005-253">CRState_s</span></span>|  <span data-ttu-id="ee005-254">Durum</span><span class="sxs-lookup"><span data-stu-id="ee005-254">State</span></span>|
| <span data-ttu-id="ee005-255">Urgency_s</span><span class="sxs-lookup"><span data-stu-id="ee005-255">Urgency_s</span></span>|  <span data-ttu-id="ee005-256">Aciliyet</span><span class="sxs-lookup"><span data-stu-id="ee005-256">Urgency</span></span> |
| <span data-ttu-id="ee005-257">Priority_s</span><span class="sxs-lookup"><span data-stu-id="ee005-257">Priority_s</span></span>| <span data-ttu-id="ee005-258">Öncelik</span><span class="sxs-lookup"><span data-stu-id="ee005-258">Priority</span></span>|
| <span data-ttu-id="ee005-259">Risk_s</span><span class="sxs-lookup"><span data-stu-id="ee005-259">Risk_s</span></span>| <span data-ttu-id="ee005-260">Riski</span><span class="sxs-lookup"><span data-stu-id="ee005-260">Risk</span></span>|
| <span data-ttu-id="ee005-261">Impact_s</span><span class="sxs-lookup"><span data-stu-id="ee005-261">Impact_s</span></span>| <span data-ttu-id="ee005-262">Etkisi</span><span class="sxs-lookup"><span data-stu-id="ee005-262">Impact</span></span>|
| <span data-ttu-id="ee005-263">RequestedDate_t</span><span class="sxs-lookup"><span data-stu-id="ee005-263">RequestedDate_t</span></span>  | <span data-ttu-id="ee005-264">Tarihe göre istendi</span><span class="sxs-lookup"><span data-stu-id="ee005-264">Requested by date</span></span> |
| <span data-ttu-id="ee005-265">ClosedDate_t</span><span class="sxs-lookup"><span data-stu-id="ee005-265">ClosedDate_t</span></span> | <span data-ttu-id="ee005-266">Kapatılma tarihi</span><span class="sxs-lookup"><span data-stu-id="ee005-266">Closed date</span></span> |
| <span data-ttu-id="ee005-267">PlannedStartDate_t</span><span class="sxs-lookup"><span data-stu-id="ee005-267">PlannedStartDate_t</span></span>  |     <span data-ttu-id="ee005-268">Planlanan başlangıç tarihi</span><span class="sxs-lookup"><span data-stu-id="ee005-268">Planned start date</span></span> |
| <span data-ttu-id="ee005-269">PlannedEndDate_t</span><span class="sxs-lookup"><span data-stu-id="ee005-269">PlannedEndDate_t</span></span>  |   <span data-ttu-id="ee005-270">Planlanan bitiş tarihi</span><span class="sxs-lookup"><span data-stu-id="ee005-270">Planned end date</span></span> |
| <span data-ttu-id="ee005-271">WorkStartDate_t</span><span class="sxs-lookup"><span data-stu-id="ee005-271">WorkStartDate_t</span></span>  | <span data-ttu-id="ee005-272">Gerçek başlangıç tarihi</span><span class="sxs-lookup"><span data-stu-id="ee005-272">Actual start date</span></span> |
| <span data-ttu-id="ee005-273">WorkEndDate_t</span><span class="sxs-lookup"><span data-stu-id="ee005-273">WorkEndDate_t</span></span> | <span data-ttu-id="ee005-274">Gerçek bitiş tarihi</span><span class="sxs-lookup"><span data-stu-id="ee005-274">Actual end date</span></span>|
| <span data-ttu-id="ee005-275">Description_s</span><span class="sxs-lookup"><span data-stu-id="ee005-275">Description_s</span></span> | <span data-ttu-id="ee005-276">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ee005-276">Description</span></span> |
| <span data-ttu-id="ee005-277">Bilgisayar</span><span class="sxs-lookup"><span data-stu-id="ee005-277">Computer</span></span>  | <span data-ttu-id="ee005-278">Yapılandırma öğesi</span><span class="sxs-lookup"><span data-stu-id="ee005-278">Configuration Item</span></span> |

<span data-ttu-id="ee005-279">**Örnek günlük analizi ekran ITSM verileri için:**</span><span class="sxs-lookup"><span data-stu-id="ee005-279">**Sample Log Analytics screen for ITSM data:**</span></span>

![Günlük analizi ekranı](./media/log-analytics-itsmc/itsmc-overview-sample-log-analytics.png)

## <a name="it-service-management-connector--integration-with-other-oms-solutions"></a><span data-ttu-id="ee005-281">BT Hizmet Yönetimi Bağlayıcısı – diğer OMS çözümleri ile tümleştirme</span><span class="sxs-lookup"><span data-stu-id="ee005-281">IT Service Management connector – integration with other OMS solutions</span></span>

<span data-ttu-id="ee005-282">BT Hizmet Yönetimi Bağlayıcısı, şu anda hizmet Haritası çözümüyle tümleştirmeyi destekler.</span><span class="sxs-lookup"><span data-stu-id="ee005-282">IT Service Management Connector, currently supports integration with the Service Map solution.</span></span>

<span data-ttu-id="ee005-283">Hizmet eşlemesi otomatik olarak sistemlerde, Windows ve Linux uygulama bileşenleri bulur ve Hizmetleri arasındaki iletişimi eşler.</span><span class="sxs-lookup"><span data-stu-id="ee005-283">Service Map automatically discovers the application components on Windows and Linux systems and maps the communication between services.</span></span> <span data-ttu-id="ee005-284">Bunları – Kritik hizmetler sunan birbirine bağlı sistemler olarak düşündüğünüz sunucularınızı görüntülemenize izin verir.</span><span class="sxs-lookup"><span data-stu-id="ee005-284">It allows you to view your servers as you think of them – as interconnected systems that deliver critical services.</span></span> <span data-ttu-id="ee005-285">Bir aracı yüklemesini dışında hiçbir yapılandırma TCP bağlı mimarisiyle arasında bağlantı noktaları gerekli ve hizmet Haritası sunucuları, işlemleri arasındaki bağlantıları gösterir.</span><span class="sxs-lookup"><span data-stu-id="ee005-285">Service Map shows connections between servers, processes, and ports across any TCP-connected architecture with no configuration required other than installation of an agent.</span></span> <span data-ttu-id="ee005-286">Daha fazla bilgi: [hizmet Haritası](../operations-management-suite/operations-management-suite-service-map.md).</span><span class="sxs-lookup"><span data-stu-id="ee005-286">More information: [Service Map](../operations-management-suite/operations-management-suite-service-map.md).</span></span>

<span data-ttu-id="ee005-287">İle tümleştirme, aşağıdaki örnekte gösterildiği gibi ITSM çözümlerinde oluşturulan hizmet Masası öğeleri görüntüleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ee005-287">With this integration, you can view the service desk items created in the ITSM solutions as shown in the following example:</span></span>

![<span data-ttu-id="ee005-288">Tümleşik çözüm</span><span class="sxs-lookup"><span data-stu-id="ee005-288">Integrated solution</span></span> ](./media/log-analytics-itsmc/itsmc-overview-integrated-solutions.png)
## <a name="create-itsm-work-items-for-oms-alerts"></a><span data-ttu-id="ee005-289">OMS uyarılar için ITSM iş öğeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="ee005-289">Create ITSM work items for OMS alerts</span></span>

<span data-ttu-id="ee005-290">OMS uyarılar için bağlı ITSM kaynaklarında ilişkili iş öğeleri oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ee005-290">For the OMS alerts, you can create associated work items in the connected ITSM sources.</span></span>  <span data-ttu-id="ee005-291">Bunu yapmak için aşağıdaki yordamı kullanın:</span><span class="sxs-lookup"><span data-stu-id="ee005-291">To do this, use the following procedure:</span></span>

1. <span data-ttu-id="ee005-292">Gelen **günlük arama** penceresinde verileri görüntülemek için bir günlük arama sorgusunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ee005-292">From **Log Search** window, run a log search query to view data.</span></span> <span data-ttu-id="ee005-293">Sorgu sonuçları, iş öğeleri için kaynaktır.</span><span class="sxs-lookup"><span data-stu-id="ee005-293">Query results are the source for work items.</span></span>
2. <span data-ttu-id="ee005-294">İçinde **günlük arama**, tıklatın **uyarı** açmak için **uyarı kuralı Ekle** sayfası.</span><span class="sxs-lookup"><span data-stu-id="ee005-294">In **Log Search**, click **Alert** to open the **Add Alert Rule** page.</span></span>

    ![Günlük analizi ekranı](./media/log-analytics-itsmc/itsmc-work-items-for-oms-alerts.png)

3. <span data-ttu-id="ee005-296">Üzerinde **uyarı kuralı Ekle** penceresinde sağlamak için gerekli ayrıntıları **adı**, **önem**, **arama sorgusu**, ve **uyarı Ölçüt** (zaman penceresi/ölçü ölçüm).</span><span class="sxs-lookup"><span data-stu-id="ee005-296">On the **Add Alert Rule** window, provide the required details for **Name**, **Severity**,  **Search query**, and **Alert criteria** (Time Window/Metric measurement).</span></span>
4. <span data-ttu-id="ee005-297">Seçin **Evet** için **ITSM Eylemler**.</span><span class="sxs-lookup"><span data-stu-id="ee005-297">Select **Yes** for **ITSM Actions**.</span></span>
5. <span data-ttu-id="ee005-298">ITSM bağlantınızı seçin **seçin bağlantı** listesi.</span><span class="sxs-lookup"><span data-stu-id="ee005-298">Select your ITSM connection from the **Select Connection** list.</span></span>
6. <span data-ttu-id="ee005-299">Gerekli ayrıntıları belirtin.</span><span class="sxs-lookup"><span data-stu-id="ee005-299">Provide the details as required.</span></span>
7. <span data-ttu-id="ee005-300">Bu uyarının her günlük girişinin için ayrı iş öğesi oluşturmak için seçin **her günlük girişinin için tek tek iş öğeleri oluşturma** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="ee005-300">To create a separate work item for each log entry of this alert, select the **Create individual work items for each log entry** checkbox.</span></span>

    <span data-ttu-id="ee005-301">Veya</span><span class="sxs-lookup"><span data-stu-id="ee005-301">Or</span></span>

    <span data-ttu-id="ee005-302">Bu onay kutusunu günlük girişlerini bu uyarı altında herhangi bir sayıda için yalnızca bir iş öğesi oluşturmak için seçili bırakın.</span><span class="sxs-lookup"><span data-stu-id="ee005-302">leave this checkbox unselected to create only one work item for any number of log entries under this alert.</span></span>

7. <span data-ttu-id="ee005-303">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ee005-303">Click **Save**.</span></span>

<span data-ttu-id="ee005-304">OMS uyarı altında oluşturulan **uyarıları**.</span><span class="sxs-lookup"><span data-stu-id="ee005-304">The OMS alert will be created under **Alerts**.</span></span> <span data-ttu-id="ee005-305">Belirtilen uyarının koşulu karşılandığında karşılık gelen ITSM bağlantı çalışma öğeleri oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="ee005-305">The corresponding ITSM connection's work items are created when the specified alert's condition is met.</span></span>

## <a name="create-itsm-work-items-from-oms-logs"></a><span data-ttu-id="ee005-306">OMS günlüklerinden ITSM iş öğeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="ee005-306">Create ITSM work items from OMS logs</span></span>

<span data-ttu-id="ee005-307">OMS günlük arama kullanarak bağlı ITSM kaynaklarında iş öğeleri oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ee005-307">You can create work items in the connected ITSM sources by using OMS Log Search.</span></span> <span data-ttu-id="ee005-308">Bunu yapmak için aşağıdaki yordamı kullanın:</span><span class="sxs-lookup"><span data-stu-id="ee005-308">To do this, use the following procedure:</span></span>

1. <span data-ttu-id="ee005-309">Gelen **günlük arama**, gerekli verileri arama, ayrıntı seçin ve tıklatın **oluşturma çalışma öğesini**.</span><span class="sxs-lookup"><span data-stu-id="ee005-309">From **Log Search**,  search the required data, select the detail, and click **Create work item**.</span></span>

    <span data-ttu-id="ee005-310">**Oluşturma ITSM iş öğesi** penceresi görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="ee005-310">The **Create ITSM Work item** window appears:</span></span>

    ![Günlük analizi ekranı](media/log-analytics-itsmc/itsmc-work-items-from-oms-logs.png)

2.   <span data-ttu-id="ee005-312">Aşağıdaki ayrıntıları ekleyin:</span><span class="sxs-lookup"><span data-stu-id="ee005-312">Add the following details:</span></span>

  - <span data-ttu-id="ee005-313">**İş öğesi başlık**: iş öğesi için başlık.</span><span class="sxs-lookup"><span data-stu-id="ee005-313">**Work item Title**: Title for the work item.</span></span>
  - <span data-ttu-id="ee005-314">**İş öğesi tanımı**: yeni çalışma öğesi için bir açıklama.</span><span class="sxs-lookup"><span data-stu-id="ee005-314">**Work item Description**: Description for the new work item.</span></span>
  - <span data-ttu-id="ee005-315">**Bilgisayar etkilenen**: Bu günlük verileri nerede bulundu bilgisayarın adı.</span><span class="sxs-lookup"><span data-stu-id="ee005-315">**Affected Computer**: Name of the computer where this log data was found.</span></span>
  - <span data-ttu-id="ee005-316">**Bağlantıyı seçin**: Bu iş öğesi oluşturmak istediğiniz ITSM bağlantı.</span><span class="sxs-lookup"><span data-stu-id="ee005-316">**Select Connection**:  ITSM connection in which you want to create this work item.</span></span>
  - <span data-ttu-id="ee005-317">**İş öğesi**: iş öğesi türü.</span><span class="sxs-lookup"><span data-stu-id="ee005-317">**Work item**:  Type of work item.</span></span>

3. <span data-ttu-id="ee005-318">Bir olay için var olan bir iş öğesi şablonunu kullanmak için tıklatın **Evet** altında **Generate iş öğesi şablona dayalı** seçeneğini ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="ee005-318">To use an existing work item template for an incident, click **Yes** under **Generate work item based on the template** option and then click **Create**.</span></span>

    <span data-ttu-id="ee005-319">Veya</span><span class="sxs-lookup"><span data-stu-id="ee005-319">Or,</span></span>

    <span data-ttu-id="ee005-320">Tıklatın **Hayır** özelleştirilmiş değerlerinizi sağlamak istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="ee005-320">Click **No** if you want to provide your customized values.</span></span>

4. <span data-ttu-id="ee005-321">Uygun değerleri sağlayın **kişi türündeki**, **etkisi**, **aciliyet**, **kategori**, ve **alt kategori** metin kutuları ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="ee005-321">Provide the appropriate values in the **Contact Type**, **Impact**, **Urgency**, **Category**, and **Sub Category** text boxes, and then click **Create**.</span></span>

<span data-ttu-id="ee005-322">İş öğesi içinde OMS de görüntüleyebilirsiniz ITSM içinde oluşturulacak.</span><span class="sxs-lookup"><span data-stu-id="ee005-322">The work item will be created in the ITSM, which you can also view in OMS.</span></span>

## <a name="troubleshoot-itsm-connections-in-oms"></a><span data-ttu-id="ee005-323">OMS ITSM bağlantı sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="ee005-323">Troubleshoot ITSM connections in OMS</span></span>
1.  <span data-ttu-id="ee005-324">Bağlantı başarısız bağlı kaynağın kullanıcı Arabiriminden ve elde **bağlantı kaydetmede hata** iletisi, aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="ee005-324">If connection fails from connected source's UI and you get the **Error in saving connection** message, do the following:</span></span>
 - <span data-ttu-id="ee005-325">ServiceNow, Cherwell ve Provance bağlantıları olması durumunda, doğru kullanıcı adı/parola ve istemci kimliği/istemci gizli anahtarı bağlantıların her biri için girdiğiniz emin olun.</span><span class="sxs-lookup"><span data-stu-id="ee005-325">In case of ServiceNow, Cherwell and Provance connections, ensure you correctly entered  the username/password and  client ID/client secret  for each of the connections.</span></span> <span data-ttu-id="ee005-326">Sorun devam ederse, bağlantıyı kurmak için karşılık gelen ITSM üründe yeterli ayrıcalıkları olup olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="ee005-326">If the error persists, check if you have sufficient privileges  in the corresponding ITSM product to make the connection.</span></span>
 - <span data-ttu-id="ee005-327">Service Manager durumunda, Web uygulaması başarıyla dağıtılır ve karma bağlantı oluşturulan emin olun.</span><span class="sxs-lookup"><span data-stu-id="ee005-327">In case of Service Manager, ensure that the Web app is successfully deployed and hybrid connection is created.</span></span> <span data-ttu-id="ee005-328">Şirket içi Service Manager makineyle bağlantı kuran başarıyla doğrulamak için Web uygulaması URL'si yapma belgelerindeki ayrıntılı olarak ziyaret [karma bağlantı](log-analytics-itsmc-connections.md#configure-the-hybrid-connection).</span><span class="sxs-lookup"><span data-stu-id="ee005-328">To verify the connection is successfully established with the on-prem Service Manager machine, visit the  Web app URL as detailed in the documentation for making the [hybrid connection](log-analytics-itsmc-connections.md#configure-the-hybrid-connection).</span></span>

2.  <span data-ttu-id="ee005-329">ServiceNow verileri OMS eşitlenmedi, örneği değil uykuda ServiceNow emin olun.</span><span class="sxs-lookup"><span data-stu-id="ee005-329">If data from ServiceNow is not getting synced in OMS, ensure that the ServiceNow instance is not sleeping.</span></span> <span data-ttu-id="ee005-330">Bu süre ServiceNow geliştirme durumlarda boşta olduğunda meydana gelir.</span><span class="sxs-lookup"><span data-stu-id="ee005-330">This might sometime happen in the ServiceNow Dev instances, when idle.</span></span> <span data-ttu-id="ee005-331">Aksi takdirde, sorunu bildirin.</span><span class="sxs-lookup"><span data-stu-id="ee005-331">Else, report the issue.</span></span>
3.  <span data-ttu-id="ee005-332">OMS uyarıları tetiklenir ancak iş öğelerini ITSM içinde oluşturulan ürün veya yapılandırma öğeleri oluşturulan/iş öğeleri ya da herhangi bir genel bilgi için aşağıdakileri yapın bağlantılı almıyorsa:</span><span class="sxs-lookup"><span data-stu-id="ee005-332">If Alerts are getting fired from OMS but work items are not getting created in ITSM product or configuration items are not getting created/linked to work items or for any generic information, do the following:</span></span>
 -  <span data-ttu-id="ee005-333">BT Hizmet Yönetimi Bağlayıcısı çözüm OMS portalında bağlantıları/iş öğeleri/bilgisayarların vb. özetini almak için kullanılabilir. Durum dikey penceresinde hata iletisi'ı tıklatın, gitmek **günlük arama** ve hata iletisinde ayrıntıları kullanarak hatalı bağlantı görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="ee005-333">IT Service Management Connector solution in OMS portal could be used to get a summary of connections/work items/computers etc. Click the error message in the status blade, navigate to **Log Search** and view the connection that has the error by using the details in the error message.</span></span>
 - <span data-ttu-id="ee005-334">doğrudan hataları ve ilgili bilgileri görüntüleyebileceğiniz **günlük arama** kullanarak sayfa *türü ServiceDeskLog_CL =*.</span><span class="sxs-lookup"><span data-stu-id="ee005-334">you can directly view the errors/related information in the **Log Search** page using *Type=ServiceDeskLog_CL*.</span></span>

## <a name="troubleshoot-service-manager-web-app-deployment"></a><span data-ttu-id="ee005-335">Service Manager Web uygulama dağıtım sorunlarını gider</span><span class="sxs-lookup"><span data-stu-id="ee005-335">Troubleshoot Service Manager Web App deployment</span></span>
1.  <span data-ttu-id="ee005-336">Web uygulama dağıtımına herhangi bir sorun olması durumunda, kaynakları oluşturun/dağıtmak için belirtilen abonelik yeterli izinlere sahip olun.</span><span class="sxs-lookup"><span data-stu-id="ee005-336">In case of any trouble with web app deployment, ensure you have sufficient permissions in the subscription mentioned to create/deploy resources.</span></span>
2.  <span data-ttu-id="ee005-337">Varsa **nesne bir nesnenin örneğine ayarlı değil referansı** hata iletisi görüntüleniyor çalıştırılırken [betik](log-analytics-itsmc-service-manager-script.md) altında geçerli değerler girdiğinizden emin olun **Kullanıcı Yapılandırması** bölüm.</span><span class="sxs-lookup"><span data-stu-id="ee005-337">If **Object reference not set to instance of an object** error message appears while running the [script](log-analytics-itsmc-service-manager-script.md) ensure that you entered valid values  under **User Configuration** section.</span></span>
3.  <span data-ttu-id="ee005-338">Service bus geçiş ad alanı oluşturma başarısız olursa, gereken kaynak sağlayıcısı abonelikte kayıtlı olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="ee005-338">If you fail to create service bus relay namespace, ensure that the required resource provider is registered in the subscription.</span></span> <span data-ttu-id="ee005-339">El ile kayıtlı değil, Azure portalından oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ee005-339">If not registered, manually create it from the Azure portal.</span></span> <span data-ttu-id="ee005-340">Bunu sırasında da oluşturabilirsiniz [karma bağlantı oluşturma](log-analytics-itsmc-connections.md#configure-the-hybrid-connection) Azure portalından.</span><span class="sxs-lookup"><span data-stu-id="ee005-340">You can also create it while [creating the hybrid connection](log-analytics-itsmc-connections.md#configure-the-hybrid-connection) from the Azure portal.</span></span>


## <a name="contact-us"></a><span data-ttu-id="ee005-341">Bizimle iletişim kurun</span><span class="sxs-lookup"><span data-stu-id="ee005-341">Contact us</span></span>

<span data-ttu-id="ee005-342">Tüm sorgular veya BT Hizmet Yönetimi Bağlayıcısı geribildirim için adresinden bize başvurun [ omsitsmfeedback@microsoft.com ](mailto:omsitsmfeedback@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="ee005-342">For any queries or feedback on the IT Service Management Connector, contact us at [omsitsmfeedback@microsoft.com](mailto:omsitsmfeedback@microsoft.com).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ee005-343">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ee005-343">Next steps</span></span>
<span data-ttu-id="ee005-344">[BT Hizmet Yönetimi Bağlayıcısı için ITSM ürünler/hizmetler eklemek](log-analytics-itsmc-connections.md).</span><span class="sxs-lookup"><span data-stu-id="ee005-344">[Add ITSM products/services to IT Service Management Connector](log-analytics-itsmc-connections.md).</span></span>
