---
title: "Hizmet Yönetimi Bağlayıcısı OMS içinde aaaIT | Microsoft Docs"
description: "Hello BT Hizmet Yönetimi Bağlayıcısı toocentrally İzleyicisi'ni kullanın ve OMS hello ITSM iş öğelerini yönetmek ve hızlı bir şekilde tüm sorunları giderin."
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
ms.openlocfilehash: 33ed5d432591b836eb41ba982c66c96f22879444
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="centrally-manage-itsm-work-items-using-it-service-management-connector-preview"></a><span data-ttu-id="15a99-103">ITSM iş öğelerini BT Hizmet Yönetimi Bağlayıcısı (Önizleme) kullanarak merkezi olarak yönetme</span><span class="sxs-lookup"><span data-stu-id="15a99-103">Centrally manage ITSM work items using IT Service Management Connector (Preview)</span></span>

![BT Hizmet Yönetimi Bağlayıcısı simgesi](./media/log-analytics-itsmc/itsmc-symbol.png)

<span data-ttu-id="15a99-105">OMS günlük analizi toocentrally İzleyicisi'nde hello BT Hizmet Yönetimi Bağlayıcısı (ITSMC) kullanın ve iş öğeleri ITSM ürünler/hizmetlerinizi yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="15a99-105">You can use hello IT Service Management Connector (ITSMC) in OMS Log Analytics toocentrally monitor and manage work items across your ITSM products/services.</span></span>

<span data-ttu-id="15a99-106">Merhaba BT Hizmet Yönetimi Bağlayıcısı var olan BT Hizmet Yönetimi (ITSM) ürünleri ve Hizmetleri OMS günlük analizi ile tümleşir.</span><span class="sxs-lookup"><span data-stu-id="15a99-106">hello IT Service Management Connector integrates your existing IT Service Management (ITSM) products and services with OMS Log Analytics.</span></span>  <span data-ttu-id="15a99-107">ITSM ürünler/hizmetler ile çift yönlü tümleştirme Hello çözümü vardır, OMS kullanıcılar bir seçenek toocreate olaylar, uyarılar veya ITSM çözüm olayların sağladığı burada hello.</span><span class="sxs-lookup"><span data-stu-id="15a99-107">hello solution has bidirectional integration with ITSM products/services, where it provides hello OMS users an option toocreate incidents, alerts, or events in ITSM solution.</span></span> <span data-ttu-id="15a99-108">Merhaba bağlayıcı da olaylar gibi verileri içe aktaran ve OMS günlük analizi ITSM çözümden değişiklik istekleri.</span><span class="sxs-lookup"><span data-stu-id="15a99-108">hello connector also  imports data such as incidents, and change requests from ITSM solution into OMS Log Analytics.</span></span>

<span data-ttu-id="15a99-109">BT Hizmet Yönetimi Bağlayıcısı ile şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="15a99-109">With IT Service Management Connector, you can:</span></span>

  - <span data-ttu-id="15a99-110">Merkezi olarak izlemek ve iş öğeleri için ITSM ürünler/hizmetler kuruluşunuz genelinde kullanılan yönetin.</span><span class="sxs-lookup"><span data-stu-id="15a99-110">Centrally monitor and manage work items for ITSM products/services used across your organization.</span></span>
  - <span data-ttu-id="15a99-111">ITSM iş öğeleri (örneğin, uyarı, olay, olay) içinde ITSM OMS uyarılardan ve günlük arama aracılığıyla oluşturun.</span><span class="sxs-lookup"><span data-stu-id="15a99-111">Create ITSM work items (like alert, event, incident) in ITSM from OMS alerts and through log search.</span></span>
  - <span data-ttu-id="15a99-112">Olayları okuma ve ITSM çözümünüzden değişiklik istekleri ve ilgili günlük veri günlük analizi çalışma alanındaki ile ilişkilendirilmesi.</span><span class="sxs-lookup"><span data-stu-id="15a99-112">Read incidents and change requests from your ITSM solution and correlate with relevant log data in Log Analytics workspace.</span></span>
  - <span data-ttu-id="15a99-113">Beklenmeyen ve olağan dışı olayları bulmak ve hatta hello son kullanıcıların çağırın ve toohello Yardım Masası rapor önce bunları çözün.</span><span class="sxs-lookup"><span data-stu-id="15a99-113">Find any unexpected and unusual events and resolve them, even before hello end users call and report them toohello helpdesk.</span></span>
  - <span data-ttu-id="15a99-114">İş öğeleri veri günlük analizi alabilir ve ana performans göstergesi (KPI) raporları oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="15a99-114">Import work items data into Log Analytics and create key performance indicator (KPI) reports.</span></span>  <span data-ttu-id="15a99-115">Bu raporları kullanarak, tanımlayabilir, değerlendirmek ve kötü amaçlı yazılım değerlendirmesi gibi birkaç önemli öğe hareket.</span><span class="sxs-lookup"><span data-stu-id="15a99-115">Using these reports, you can identify, assess and act on several important items such as malware assessment.</span></span>
  - <span data-ttu-id="15a99-116">Daha ayrıntılı Öngörüler için seçkin panolar üzerinde olayları görüntülemek için değişiklik istekleri ve etkilenen sistemler.</span><span class="sxs-lookup"><span data-stu-id="15a99-116">View curated dashboards for deeper insights on incidents, change requests and impacted systems.</span></span>
  - <span data-ttu-id="15a99-117">Daha hızlı hello günlük analizi çalışma alanındaki diğer yönetim çözümleri ile ilişkilendirilmesi yoluyla sorunlarını giderin.</span><span class="sxs-lookup"><span data-stu-id="15a99-117">Troubleshoot faster by correlating with other management solutions in hello Log Analytics workspace.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="15a99-118">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="15a99-118">Prerequisites</span></span>

<span data-ttu-id="15a99-119">tooimport hello ITSM iş öğeleri OMS günlük analizi içine hello çözüm hello OMS hello BT Hizmet Yönetimi Bağlayıcısı ile Merhaba BT SM Ürün/hizmet hello çalışma öğelerini içeri aktarma arasında bir bağlantı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="15a99-119">tooimport hello ITSM work items into OMS Log Analytics, hello solution requires a connection between hello IT Service Management Connector in hello OMS and hello IT SM product/service from which you import hello work items.</span></span>


## <a name="configuration"></a><span data-ttu-id="15a99-120">Yapılandırma</span><span class="sxs-lookup"><span data-stu-id="15a99-120">Configuration</span></span>

<span data-ttu-id="15a99-121">Açıklanan başlangıç işlemini kullanarak Ekle hello BT Hizmet Yönetimi Bağlayıcısı çözüm tooyour OMS çalışma alanı, [hello Çözümleri Galerisi eklemek günlük analizi çözümleri](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="15a99-121">Add hello IT Service Management Connector solution tooyour OMS work space, using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>

<span data-ttu-id="15a99-122">BT Hizmet Yönetimi Bağlayıcısı hello çözümleri Galerisi'nde gördüğünüz gibi döşeme:</span><span class="sxs-lookup"><span data-stu-id="15a99-122">IT Service Management Connector tile as you see in hello Solutions gallery:</span></span>

![Bağlayıcı döşeme](./media/log-analytics-itsmc/itsmc-solutions-tile.png)

<span data-ttu-id="15a99-124">Göreceğiniz başarılı ayrıca sonra BT Hizmet Yönetimi Bağlayıcısı altında hello **OMS** > **ayarları** > **bağlı kaynakları.**</span><span class="sxs-lookup"><span data-stu-id="15a99-124">After successful addition, you will see hello IT Service Management Connector under **OMS** > **Settings** > **Connected Sources.**</span></span>

![Bağlı ITSMC](./media/log-analytics-itsmc/itsmc-overview-solution-in-connected-sources.png)

> [!NOTE]

> <span data-ttu-id="15a99-126">Varsayılan olarak, BT Hizmet Yönetimi Bağlayıcısı hello 24 saatte bir kez hello bağlantının verileri yeniler.</span><span class="sxs-lookup"><span data-stu-id="15a99-126">By default, hello IT Service Management Connector refreshes hello connection's data once in every 24 hours.</span></span> <span data-ttu-id="15a99-127">toorefresh hello Yenile düğmesini görüntülenen sonraki tooyour Bağlantısı'nı tıklatın, yaptığınız herhangi bir düzenlemeler veya şablon için anında, bağlantının verileri güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="15a99-127">toorefresh your connection's data instantly for any edits or template updates that you make, click hello refresh button displayed next tooyour connection.</span></span>

 ![ITSMC Yenile](./media/log-analytics-itsmc/itsmc-connection-refresh.png)

## <a name="management-packs"></a><span data-ttu-id="15a99-129">Yönetim paketleri</span><span class="sxs-lookup"><span data-stu-id="15a99-129">Management packs</span></span>
<span data-ttu-id="15a99-130">Bu çözüm, herhangi bir Yönetim Paketi gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="15a99-130">This solution does not require any management packs.</span></span>

## <a name="connected-sources"></a><span data-ttu-id="15a99-131">Bağlı kaynaklar</span><span class="sxs-lookup"><span data-stu-id="15a99-131">Connected sources</span></span>

<span data-ttu-id="15a99-132">Merhaba aşağıdaki ITSM ürünler/hizmetler hello BT Hizmet Yönetimi Bağlayıcısı tarafından desteklenir:</span><span class="sxs-lookup"><span data-stu-id="15a99-132">hello following ITSM products/services are supported by hello IT Service Management Connector:</span></span>

- [<span data-ttu-id="15a99-133">System Center Service Manager (SCSM)</span><span class="sxs-lookup"><span data-stu-id="15a99-133">System Center Service Manager (SCSM)</span></span>](log-analytics-itsmc-connections.md#connect-system-center-service-manager-to-it-service-management-connector-in-oms)

- [<span data-ttu-id="15a99-134">ServiceNow</span><span class="sxs-lookup"><span data-stu-id="15a99-134">ServiceNow</span></span>](log-analytics-itsmc-connections.md#connect-servicenow-to-it-service-management-connector-in-oms)

- [<span data-ttu-id="15a99-135">Provance</span><span class="sxs-lookup"><span data-stu-id="15a99-135">Provance</span></span>](log-analytics-itsmc-connections.md#connect-provance-to-it-service-management-connector-in-oms)  

- [<span data-ttu-id="15a99-136">Cherwell</span><span class="sxs-lookup"><span data-stu-id="15a99-136">Cherwell</span></span>](log-analytics-itsmc-connections.md#connect-cherwell-to-it-service-management-connector-in-oms)

## <a name="using-hello-solution"></a><span data-ttu-id="15a99-137">Merhaba çözümünü kullanarak</span><span class="sxs-lookup"><span data-stu-id="15a99-137">Using hello solution</span></span>

<span data-ttu-id="15a99-138">ITSM hizmeti ile Merhaba OMS BT Hizmet Yönetimi Bağlayıcısı bağlandıktan sonra hello günlük analizi Hizmetleri başlatılır bağlı hello ITSM Ürün/hizmet hello veri toplama.</span><span class="sxs-lookup"><span data-stu-id="15a99-138">Once you connect hello OMS IT Service Management Connector with your ITSM service, hello Log Analytics services starts gathering hello data from hello connected ITSM products/service.</span></span>

> [!NOTE]
> - <span data-ttu-id="15a99-139">BT Hizmet Yönetimi Bağlayıcısı çözümü tarafından alınan veri olayların adlı günlük analizi görünür **ServiceDesk_CL**.</span><span class="sxs-lookup"><span data-stu-id="15a99-139">Data imported by IT Service Management Connector solution appears in Log Analytics as events named **ServiceDesk_CL**.</span></span>
- <span data-ttu-id="15a99-140">Olay adında bir alan içeriyor **ServiceDeskWorkItemType_s**.</span><span class="sxs-lookup"><span data-stu-id="15a99-140">Event contains a field named **ServiceDeskWorkItemType_s**.</span></span> <span data-ttu-id="15a99-141">hangi değer olay olarak ele veya değişiklik isteği, yapabilirsiniz hello bağlı olarak iş öğesi hello bulunan verileri **ServiceDesk_CL** olay.</span><span class="sxs-lookup"><span data-stu-id="15a99-141">which can take its value as incident, or change request, depending on hello work item data contained in hello **ServiceDesk_CL** event.</span></span>

## <a name="input-data"></a><span data-ttu-id="15a99-142">Giriş verisi</span><span class="sxs-lookup"><span data-stu-id="15a99-142">Input data</span></span>
<span data-ttu-id="15a99-143">İş öğeleri Hello ITSM ürünler/hizmetlerinden içeri aktarılan.</span><span class="sxs-lookup"><span data-stu-id="15a99-143">Work items imported from hello ITSM products/services.</span></span>

<span data-ttu-id="15a99-144">Merhaba aşağıdaki bilgileri hello BT Hizmet Yönetimi Bağlayıcısı tarafından toplanan veri örnekleri gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="15a99-144">hello following information shows examples of data gathered by hello IT Service Management connector:</span></span>

> [!NOTE]
> <span data-ttu-id="15a99-145">İş öğesi türü günlük analizi içeri Hello bağlı olarak **ServiceDesk_CL** alanları izleyen hello içerir:</span><span class="sxs-lookup"><span data-stu-id="15a99-145">Depending on hello work item type imported into Log Analytics, **ServiceDesk_CL** contains hello following fields:</span></span>

<span data-ttu-id="15a99-146">**İş öğesi:** **olaylar**</span><span class="sxs-lookup"><span data-stu-id="15a99-146">**Work item:** **Incidents**</span></span>  
<span data-ttu-id="15a99-147">ServiceDeskWorkItemType_s "Olay" =</span><span class="sxs-lookup"><span data-stu-id="15a99-147">ServiceDeskWorkItemType_s="Incident"</span></span>

<span data-ttu-id="15a99-148">**Alanları**</span><span class="sxs-lookup"><span data-stu-id="15a99-148">**Fields**</span></span>

- <span data-ttu-id="15a99-149">ServiceDeskConnectionName</span><span class="sxs-lookup"><span data-stu-id="15a99-149">ServiceDeskConnectionName</span></span>
- <span data-ttu-id="15a99-150">Hizmet Masası kimliği</span><span class="sxs-lookup"><span data-stu-id="15a99-150">Service Desk ID</span></span>
- <span data-ttu-id="15a99-151">Durum</span><span class="sxs-lookup"><span data-stu-id="15a99-151">State</span></span>
- <span data-ttu-id="15a99-152">Aciliyet</span><span class="sxs-lookup"><span data-stu-id="15a99-152">Urgency</span></span>
- <span data-ttu-id="15a99-153">Etkisi</span><span class="sxs-lookup"><span data-stu-id="15a99-153">Impact</span></span>
- <span data-ttu-id="15a99-154">Öncelik</span><span class="sxs-lookup"><span data-stu-id="15a99-154">Priority</span></span>
- <span data-ttu-id="15a99-155">Yükseltme</span><span class="sxs-lookup"><span data-stu-id="15a99-155">Escalation</span></span>
- <span data-ttu-id="15a99-156">Tarafından oluşturulan</span><span class="sxs-lookup"><span data-stu-id="15a99-156">Created By</span></span>
- <span data-ttu-id="15a99-157">Çözümleyen</span><span class="sxs-lookup"><span data-stu-id="15a99-157">Resolved By</span></span>
- <span data-ttu-id="15a99-158">Tarafından kapatıldı</span><span class="sxs-lookup"><span data-stu-id="15a99-158">Closed By</span></span>
- <span data-ttu-id="15a99-159">Kaynak</span><span class="sxs-lookup"><span data-stu-id="15a99-159">Source</span></span>
- <span data-ttu-id="15a99-160">Atanan</span><span class="sxs-lookup"><span data-stu-id="15a99-160">Assigned To</span></span>
- <span data-ttu-id="15a99-161">Kategori</span><span class="sxs-lookup"><span data-stu-id="15a99-161">Category</span></span>
- <span data-ttu-id="15a99-162">Başlık</span><span class="sxs-lookup"><span data-stu-id="15a99-162">Title</span></span>
- <span data-ttu-id="15a99-163">Açıklama</span><span class="sxs-lookup"><span data-stu-id="15a99-163">Description</span></span>
- <span data-ttu-id="15a99-164">Oluşturulma tarihi</span><span class="sxs-lookup"><span data-stu-id="15a99-164">Created Date</span></span>
- <span data-ttu-id="15a99-165">Kapatılma tarihi</span><span class="sxs-lookup"><span data-stu-id="15a99-165">Closed Date</span></span>
- <span data-ttu-id="15a99-166">Çözümlenme tarihi</span><span class="sxs-lookup"><span data-stu-id="15a99-166">Resolved Date</span></span>
- <span data-ttu-id="15a99-167">Son değiştirilme tarihi</span><span class="sxs-lookup"><span data-stu-id="15a99-167">Last Modified Date</span></span>
- <span data-ttu-id="15a99-168">Bilgisayar</span><span class="sxs-lookup"><span data-stu-id="15a99-168">Computer</span></span>


<span data-ttu-id="15a99-169">**İş öğesi:** **değişiklik istekleri**</span><span class="sxs-lookup"><span data-stu-id="15a99-169">**Work item:** **Change Requests**</span></span>

<span data-ttu-id="15a99-170">ServiceDeskWorkItemType_s "ChangeRequest" =</span><span class="sxs-lookup"><span data-stu-id="15a99-170">ServiceDeskWorkItemType_s="ChangeRequest"</span></span>

<span data-ttu-id="15a99-171">**Alanları**</span><span class="sxs-lookup"><span data-stu-id="15a99-171">**Fields**</span></span>
- <span data-ttu-id="15a99-172">ServiceDeskConnectionName</span><span class="sxs-lookup"><span data-stu-id="15a99-172">ServiceDeskConnectionName</span></span>
- <span data-ttu-id="15a99-173">Hizmet Masası kimliği</span><span class="sxs-lookup"><span data-stu-id="15a99-173">Service Desk ID</span></span>
- <span data-ttu-id="15a99-174">Tarafından oluşturulan</span><span class="sxs-lookup"><span data-stu-id="15a99-174">Created By</span></span>
- <span data-ttu-id="15a99-175">Tarafından kapatıldı</span><span class="sxs-lookup"><span data-stu-id="15a99-175">Closed By</span></span>
- <span data-ttu-id="15a99-176">Kaynak</span><span class="sxs-lookup"><span data-stu-id="15a99-176">Source</span></span>
- <span data-ttu-id="15a99-177">Atanan</span><span class="sxs-lookup"><span data-stu-id="15a99-177">Assigned To</span></span>
- <span data-ttu-id="15a99-178">Başlık</span><span class="sxs-lookup"><span data-stu-id="15a99-178">Title</span></span>
- <span data-ttu-id="15a99-179">Tür</span><span class="sxs-lookup"><span data-stu-id="15a99-179">Type</span></span>
- <span data-ttu-id="15a99-180">Kategori</span><span class="sxs-lookup"><span data-stu-id="15a99-180">Category</span></span>
- <span data-ttu-id="15a99-181">Durum</span><span class="sxs-lookup"><span data-stu-id="15a99-181">State</span></span>
- <span data-ttu-id="15a99-182">Yükseltme</span><span class="sxs-lookup"><span data-stu-id="15a99-182">Escalation</span></span>
- <span data-ttu-id="15a99-183">Çakışma durumu</span><span class="sxs-lookup"><span data-stu-id="15a99-183">Conflict Status</span></span>
- <span data-ttu-id="15a99-184">Aciliyet</span><span class="sxs-lookup"><span data-stu-id="15a99-184">Urgency</span></span>
- <span data-ttu-id="15a99-185">Öncelik</span><span class="sxs-lookup"><span data-stu-id="15a99-185">Priority</span></span>
- <span data-ttu-id="15a99-186">Riski</span><span class="sxs-lookup"><span data-stu-id="15a99-186">Risk</span></span>
- <span data-ttu-id="15a99-187">Etkisi</span><span class="sxs-lookup"><span data-stu-id="15a99-187">Impact</span></span>
- <span data-ttu-id="15a99-188">Atanan</span><span class="sxs-lookup"><span data-stu-id="15a99-188">Assigned To</span></span>
- <span data-ttu-id="15a99-189">Oluşturulma tarihi</span><span class="sxs-lookup"><span data-stu-id="15a99-189">Created Date</span></span>
- <span data-ttu-id="15a99-190">Kapatılma tarihi</span><span class="sxs-lookup"><span data-stu-id="15a99-190">Closed Date</span></span>
- <span data-ttu-id="15a99-191">Son değiştirilme tarihi</span><span class="sxs-lookup"><span data-stu-id="15a99-191">Last Modified Date</span></span>
- <span data-ttu-id="15a99-192">İstenen tarih</span><span class="sxs-lookup"><span data-stu-id="15a99-192">Requested Date</span></span>
- <span data-ttu-id="15a99-193">Planlanan başlangıç tarihi</span><span class="sxs-lookup"><span data-stu-id="15a99-193">Planned Start Date</span></span>
- <span data-ttu-id="15a99-194">Planlanan bitiş tarihi</span><span class="sxs-lookup"><span data-stu-id="15a99-194">Planned End Date</span></span>
- <span data-ttu-id="15a99-195">İş başlangıç tarihi</span><span class="sxs-lookup"><span data-stu-id="15a99-195">Work Start Date</span></span>
- <span data-ttu-id="15a99-196">İş bitiş tarihi</span><span class="sxs-lookup"><span data-stu-id="15a99-196">Work End Date</span></span>
- <span data-ttu-id="15a99-197">Açıklama</span><span class="sxs-lookup"><span data-stu-id="15a99-197">Description</span></span>
- <span data-ttu-id="15a99-198">Bilgisayar</span><span class="sxs-lookup"><span data-stu-id="15a99-198">Computer</span></span>

## <a name="output-data-for-a-servicenow-incident"></a><span data-ttu-id="15a99-199">ServiceNow olay için çıktı verileri</span><span class="sxs-lookup"><span data-stu-id="15a99-199">Output data for a ServiceNow incident</span></span>

| <span data-ttu-id="15a99-200">OMS alan</span><span class="sxs-lookup"><span data-stu-id="15a99-200">OMS field</span></span> | <span data-ttu-id="15a99-201">ITSM alan</span><span class="sxs-lookup"><span data-stu-id="15a99-201">ITSM field</span></span> |
|:--- |:--- |
| <span data-ttu-id="15a99-202">ServiceDeskId_s</span><span class="sxs-lookup"><span data-stu-id="15a99-202">ServiceDeskId_s</span></span>| <span data-ttu-id="15a99-203">Sayı</span><span class="sxs-lookup"><span data-stu-id="15a99-203">Number</span></span> |
| <span data-ttu-id="15a99-204">IncidentState_s</span><span class="sxs-lookup"><span data-stu-id="15a99-204">IncidentState_s</span></span> | <span data-ttu-id="15a99-205">Durum</span><span class="sxs-lookup"><span data-stu-id="15a99-205">State</span></span> |
| <span data-ttu-id="15a99-206">Urgency_s</span><span class="sxs-lookup"><span data-stu-id="15a99-206">Urgency_s</span></span> |<span data-ttu-id="15a99-207">Aciliyet</span><span class="sxs-lookup"><span data-stu-id="15a99-207">Urgency</span></span> |
| <span data-ttu-id="15a99-208">Impact_s</span><span class="sxs-lookup"><span data-stu-id="15a99-208">Impact_s</span></span> |<span data-ttu-id="15a99-209">Etkisi</span><span class="sxs-lookup"><span data-stu-id="15a99-209">Impact</span></span>|
| <span data-ttu-id="15a99-210">Priority_s</span><span class="sxs-lookup"><span data-stu-id="15a99-210">Priority_s</span></span> | <span data-ttu-id="15a99-211">Öncelik</span><span class="sxs-lookup"><span data-stu-id="15a99-211">Priority</span></span> |
| <span data-ttu-id="15a99-212">CreatedBy_s</span><span class="sxs-lookup"><span data-stu-id="15a99-212">CreatedBy_s</span></span> | <span data-ttu-id="15a99-213">Tarafından açılmış</span><span class="sxs-lookup"><span data-stu-id="15a99-213">Opened by</span></span> |
| <span data-ttu-id="15a99-214">ResolvedBy_s</span><span class="sxs-lookup"><span data-stu-id="15a99-214">ResolvedBy_s</span></span> | <span data-ttu-id="15a99-215">Çözümleyen</span><span class="sxs-lookup"><span data-stu-id="15a99-215">Resolved by</span></span>|
| <span data-ttu-id="15a99-216">ClosedBy_s</span><span class="sxs-lookup"><span data-stu-id="15a99-216">ClosedBy_s</span></span>  | <span data-ttu-id="15a99-217">Tarafından kapatıldı</span><span class="sxs-lookup"><span data-stu-id="15a99-217">Closed by</span></span> |
| <span data-ttu-id="15a99-218">Source_s</span><span class="sxs-lookup"><span data-stu-id="15a99-218">Source_s</span></span>| <span data-ttu-id="15a99-219">İlgili kişi türü</span><span class="sxs-lookup"><span data-stu-id="15a99-219">Contact type</span></span> |
| <span data-ttu-id="15a99-220">AssignedTo_s</span><span class="sxs-lookup"><span data-stu-id="15a99-220">AssignedTo_s</span></span> | <span data-ttu-id="15a99-221">Çok atanan</span><span class="sxs-lookup"><span data-stu-id="15a99-221">Assigned too</span></span> |
| <span data-ttu-id="15a99-222">Category_s</span><span class="sxs-lookup"><span data-stu-id="15a99-222">Category_s</span></span> | <span data-ttu-id="15a99-223">Kategori</span><span class="sxs-lookup"><span data-stu-id="15a99-223">Category</span></span> |
| <span data-ttu-id="15a99-224">Title_s</span><span class="sxs-lookup"><span data-stu-id="15a99-224">Title_s</span></span>|  <span data-ttu-id="15a99-225">Kısa açıklama</span><span class="sxs-lookup"><span data-stu-id="15a99-225">Short description</span></span> |
| <span data-ttu-id="15a99-226">Description_s</span><span class="sxs-lookup"><span data-stu-id="15a99-226">Description_s</span></span>|  <span data-ttu-id="15a99-227">Notlar</span><span class="sxs-lookup"><span data-stu-id="15a99-227">Notes</span></span> |
| <span data-ttu-id="15a99-228">CreatedDate_t</span><span class="sxs-lookup"><span data-stu-id="15a99-228">CreatedDate_t</span></span>|  <span data-ttu-id="15a99-229">Açılan</span><span class="sxs-lookup"><span data-stu-id="15a99-229">Opened</span></span> |
| <span data-ttu-id="15a99-230">ClosedDate_t</span><span class="sxs-lookup"><span data-stu-id="15a99-230">ClosedDate_t</span></span>| <span data-ttu-id="15a99-231">Kapalı</span><span class="sxs-lookup"><span data-stu-id="15a99-231">closed</span></span>|
| <span data-ttu-id="15a99-232">ResolvedDate_t</span><span class="sxs-lookup"><span data-stu-id="15a99-232">ResolvedDate_t</span></span>|<span data-ttu-id="15a99-233">Çözümlendi</span><span class="sxs-lookup"><span data-stu-id="15a99-233">Resolved</span></span>|
| <span data-ttu-id="15a99-234">Bilgisayar</span><span class="sxs-lookup"><span data-stu-id="15a99-234">Computer</span></span>  | <span data-ttu-id="15a99-235">Yapılandırma öğesi</span><span class="sxs-lookup"><span data-stu-id="15a99-235">Configuration item</span></span> |

## <a name="output-data-for-a-servicenow-change-request"></a><span data-ttu-id="15a99-236">Çıktı verileri bir ServiceNow için değişiklik isteği</span><span class="sxs-lookup"><span data-stu-id="15a99-236">Output data for a ServiceNow change request</span></span>

| <span data-ttu-id="15a99-237">OMS alan</span><span class="sxs-lookup"><span data-stu-id="15a99-237">OMS field</span></span> | <span data-ttu-id="15a99-238">ITSM alan</span><span class="sxs-lookup"><span data-stu-id="15a99-238">ITSM field</span></span> |
|:--- |:--- |
| <span data-ttu-id="15a99-239">ServiceDeskId_s</span><span class="sxs-lookup"><span data-stu-id="15a99-239">ServiceDeskId_s</span></span>| <span data-ttu-id="15a99-240">Sayı</span><span class="sxs-lookup"><span data-stu-id="15a99-240">Number</span></span> |
| <span data-ttu-id="15a99-241">CreatedBy_s</span><span class="sxs-lookup"><span data-stu-id="15a99-241">CreatedBy_s</span></span> | <span data-ttu-id="15a99-242">Tarafından istenen</span><span class="sxs-lookup"><span data-stu-id="15a99-242">Requested by</span></span> |
| <span data-ttu-id="15a99-243">ClosedBy_s</span><span class="sxs-lookup"><span data-stu-id="15a99-243">ClosedBy_s</span></span> | <span data-ttu-id="15a99-244">Tarafından kapatıldı</span><span class="sxs-lookup"><span data-stu-id="15a99-244">Closed by</span></span> |
| <span data-ttu-id="15a99-245">AssignedTo_s</span><span class="sxs-lookup"><span data-stu-id="15a99-245">AssignedTo_s</span></span> | <span data-ttu-id="15a99-246">Çok atanan</span><span class="sxs-lookup"><span data-stu-id="15a99-246">Assigned too</span></span> |
| <span data-ttu-id="15a99-247">Title_s</span><span class="sxs-lookup"><span data-stu-id="15a99-247">Title_s</span></span>|  <span data-ttu-id="15a99-248">Kısa açıklama</span><span class="sxs-lookup"><span data-stu-id="15a99-248">Short description</span></span> |
| <span data-ttu-id="15a99-249">Type_s</span><span class="sxs-lookup"><span data-stu-id="15a99-249">Type_s</span></span>|  <span data-ttu-id="15a99-250">Tür</span><span class="sxs-lookup"><span data-stu-id="15a99-250">Type</span></span> |
| <span data-ttu-id="15a99-251">Category_s</span><span class="sxs-lookup"><span data-stu-id="15a99-251">Category_s</span></span>|  <span data-ttu-id="15a99-252">Catgory</span><span class="sxs-lookup"><span data-stu-id="15a99-252">Catgory</span></span> |
| <span data-ttu-id="15a99-253">CRState_s</span><span class="sxs-lookup"><span data-stu-id="15a99-253">CRState_s</span></span>|  <span data-ttu-id="15a99-254">Durum</span><span class="sxs-lookup"><span data-stu-id="15a99-254">State</span></span>|
| <span data-ttu-id="15a99-255">Urgency_s</span><span class="sxs-lookup"><span data-stu-id="15a99-255">Urgency_s</span></span>|  <span data-ttu-id="15a99-256">Aciliyet</span><span class="sxs-lookup"><span data-stu-id="15a99-256">Urgency</span></span> |
| <span data-ttu-id="15a99-257">Priority_s</span><span class="sxs-lookup"><span data-stu-id="15a99-257">Priority_s</span></span>| <span data-ttu-id="15a99-258">Öncelik</span><span class="sxs-lookup"><span data-stu-id="15a99-258">Priority</span></span>|
| <span data-ttu-id="15a99-259">Risk_s</span><span class="sxs-lookup"><span data-stu-id="15a99-259">Risk_s</span></span>| <span data-ttu-id="15a99-260">Riski</span><span class="sxs-lookup"><span data-stu-id="15a99-260">Risk</span></span>|
| <span data-ttu-id="15a99-261">Impact_s</span><span class="sxs-lookup"><span data-stu-id="15a99-261">Impact_s</span></span>| <span data-ttu-id="15a99-262">Etkisi</span><span class="sxs-lookup"><span data-stu-id="15a99-262">Impact</span></span>|
| <span data-ttu-id="15a99-263">RequestedDate_t</span><span class="sxs-lookup"><span data-stu-id="15a99-263">RequestedDate_t</span></span>  | <span data-ttu-id="15a99-264">Tarihe göre istendi</span><span class="sxs-lookup"><span data-stu-id="15a99-264">Requested by date</span></span> |
| <span data-ttu-id="15a99-265">ClosedDate_t</span><span class="sxs-lookup"><span data-stu-id="15a99-265">ClosedDate_t</span></span> | <span data-ttu-id="15a99-266">Kapatılma tarihi</span><span class="sxs-lookup"><span data-stu-id="15a99-266">Closed date</span></span> |
| <span data-ttu-id="15a99-267">PlannedStartDate_t</span><span class="sxs-lookup"><span data-stu-id="15a99-267">PlannedStartDate_t</span></span>  |     <span data-ttu-id="15a99-268">Planlanan başlangıç tarihi</span><span class="sxs-lookup"><span data-stu-id="15a99-268">Planned start date</span></span> |
| <span data-ttu-id="15a99-269">PlannedEndDate_t</span><span class="sxs-lookup"><span data-stu-id="15a99-269">PlannedEndDate_t</span></span>  |   <span data-ttu-id="15a99-270">Planlanan bitiş tarihi</span><span class="sxs-lookup"><span data-stu-id="15a99-270">Planned end date</span></span> |
| <span data-ttu-id="15a99-271">WorkStartDate_t</span><span class="sxs-lookup"><span data-stu-id="15a99-271">WorkStartDate_t</span></span>  | <span data-ttu-id="15a99-272">Gerçek başlangıç tarihi</span><span class="sxs-lookup"><span data-stu-id="15a99-272">Actual start date</span></span> |
| <span data-ttu-id="15a99-273">WorkEndDate_t</span><span class="sxs-lookup"><span data-stu-id="15a99-273">WorkEndDate_t</span></span> | <span data-ttu-id="15a99-274">Gerçek bitiş tarihi</span><span class="sxs-lookup"><span data-stu-id="15a99-274">Actual end date</span></span>|
| <span data-ttu-id="15a99-275">Description_s</span><span class="sxs-lookup"><span data-stu-id="15a99-275">Description_s</span></span> | <span data-ttu-id="15a99-276">Açıklama</span><span class="sxs-lookup"><span data-stu-id="15a99-276">Description</span></span> |
| <span data-ttu-id="15a99-277">Bilgisayar</span><span class="sxs-lookup"><span data-stu-id="15a99-277">Computer</span></span>  | <span data-ttu-id="15a99-278">Yapılandırma öğesi</span><span class="sxs-lookup"><span data-stu-id="15a99-278">Configuration Item</span></span> |

<span data-ttu-id="15a99-279">**Örnek günlük analizi ekran ITSM verileri için:**</span><span class="sxs-lookup"><span data-stu-id="15a99-279">**Sample Log Analytics screen for ITSM data:**</span></span>

![Günlük analizi ekranı](./media/log-analytics-itsmc/itsmc-overview-sample-log-analytics.png)

## <a name="it-service-management-connector--integration-with-other-oms-solutions"></a><span data-ttu-id="15a99-281">BT Hizmet Yönetimi Bağlayıcısı – diğer OMS çözümleri ile tümleştirme</span><span class="sxs-lookup"><span data-stu-id="15a99-281">IT Service Management connector – integration with other OMS solutions</span></span>

<span data-ttu-id="15a99-282">BT Hizmet Yönetimi Bağlayıcısı, şu anda hello hizmet Haritası çözümü ile tümleştirmeyi destekler.</span><span class="sxs-lookup"><span data-stu-id="15a99-282">IT Service Management Connector, currently supports integration with hello Service Map solution.</span></span>

<span data-ttu-id="15a99-283">Hizmet eşlemesi uygulama bileşenleri Windows hello ve Linux sistemleri ve haritalar Hizmetleri arasındaki iletişimi hello otomatik olarak bulur.</span><span class="sxs-lookup"><span data-stu-id="15a99-283">Service Map automatically discovers hello application components on Windows and Linux systems and maps hello communication between services.</span></span> <span data-ttu-id="15a99-284">Sunucularınızın siz bunları – Kritik hizmetler sunan birbirine bağlı sistemler olarak düşündüğünüz tooview sağlar.</span><span class="sxs-lookup"><span data-stu-id="15a99-284">It allows you tooview your servers as you think of them – as interconnected systems that deliver critical services.</span></span> <span data-ttu-id="15a99-285">Bir aracı yüklemesini dışında hiçbir yapılandırma TCP bağlı mimarisiyle arasında bağlantı noktaları gerekli ve hizmet Haritası sunucuları, işlemleri arasındaki bağlantıları gösterir.</span><span class="sxs-lookup"><span data-stu-id="15a99-285">Service Map shows connections between servers, processes, and ports across any TCP-connected architecture with no configuration required other than installation of an agent.</span></span> <span data-ttu-id="15a99-286">Daha fazla bilgi: [hizmet Haritası](../operations-management-suite/operations-management-suite-service-map.md).</span><span class="sxs-lookup"><span data-stu-id="15a99-286">More information: [Service Map](../operations-management-suite/operations-management-suite-service-map.md).</span></span>

<span data-ttu-id="15a99-287">İle tümleştirme, hello aşağıdaki örnekte gösterildiği gibi hello ITSM çözümlerinde oluşturulan hello hizmet Masası öğeleri görüntüleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="15a99-287">With this integration, you can view hello service desk items created in hello ITSM solutions as shown in hello following example:</span></span>

![<span data-ttu-id="15a99-288">Tümleşik çözüm</span><span class="sxs-lookup"><span data-stu-id="15a99-288">Integrated solution</span></span> ](./media/log-analytics-itsmc/itsmc-overview-integrated-solutions.png)
## <a name="create-itsm-work-items-for-oms-alerts"></a><span data-ttu-id="15a99-289">OMS uyarılar için ITSM iş öğeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="15a99-289">Create ITSM work items for OMS alerts</span></span>

<span data-ttu-id="15a99-290">Merhaba OMS uyarılar için bağlı hello ITSM kaynaklarında ilişkili iş öğeleri oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="15a99-290">For hello OMS alerts, you can create associated work items in hello connected ITSM sources.</span></span>  <span data-ttu-id="15a99-291">toodo aşağıdaki yordamın bu, kullanım hello:</span><span class="sxs-lookup"><span data-stu-id="15a99-291">toodo this, use hello following procedure:</span></span>

1. <span data-ttu-id="15a99-292">Gelen **günlük arama** penceresinde bir günlük arama sorgusu tooview verilerini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="15a99-292">From **Log Search** window, run a log search query tooview data.</span></span> <span data-ttu-id="15a99-293">Sorgu sonuçları, iş öğeleri için hello kaynağıdır.</span><span class="sxs-lookup"><span data-stu-id="15a99-293">Query results are hello source for work items.</span></span>
2. <span data-ttu-id="15a99-294">İçinde **günlük arama**, tıklatın **uyarı** tooopen hello **uyarı kuralı Ekle** sayfası.</span><span class="sxs-lookup"><span data-stu-id="15a99-294">In **Log Search**, click **Alert** tooopen hello **Add Alert Rule** page.</span></span>

    ![Günlük analizi ekranı](./media/log-analytics-itsmc/itsmc-work-items-for-oms-alerts.png)

3. <span data-ttu-id="15a99-296">Hello üzerinde **uyarı kuralı Ekle** penceresinde hello gerekli ayrıntılarını sağlamak **adı**, **önem**, **arama sorgusu**, ve  **Uyarı ölçütleri** (zaman penceresi/ölçü ölçüm).</span><span class="sxs-lookup"><span data-stu-id="15a99-296">On hello **Add Alert Rule** window, provide hello required details for **Name**, **Severity**,  **Search query**, and **Alert criteria** (Time Window/Metric measurement).</span></span>
4. <span data-ttu-id="15a99-297">Seçin **Evet** için **ITSM Eylemler**.</span><span class="sxs-lookup"><span data-stu-id="15a99-297">Select **Yes** for **ITSM Actions**.</span></span>
5. <span data-ttu-id="15a99-298">Hello ITSM bağlantınızı seçin **seçin bağlantı** listesi.</span><span class="sxs-lookup"><span data-stu-id="15a99-298">Select your ITSM connection from hello **Select Connection** list.</span></span>
6. <span data-ttu-id="15a99-299">Gerekli Hello ayrıntıları belirtin.</span><span class="sxs-lookup"><span data-stu-id="15a99-299">Provide hello details as required.</span></span>
7. <span data-ttu-id="15a99-300">Bu uyarı, select hello her günlük girdisi için ayrı iş öğesi toocreate **her günlük girişinin için tek tek iş öğeleri oluşturma** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="15a99-300">toocreate a separate work item for each log entry of this alert, select hello **Create individual work items for each log entry** checkbox.</span></span>

    <span data-ttu-id="15a99-301">Veya</span><span class="sxs-lookup"><span data-stu-id="15a99-301">Or</span></span>

    <span data-ttu-id="15a99-302">Bu uyarı altında günlük girişlerini herhangi bir sayıda için bu onay kutusu seçili toocreate yalnızca bir iş öğesi bırakın.</span><span class="sxs-lookup"><span data-stu-id="15a99-302">leave this checkbox unselected toocreate only one work item for any number of log entries under this alert.</span></span>

7. <span data-ttu-id="15a99-303">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="15a99-303">Click **Save**.</span></span>

<span data-ttu-id="15a99-304">Merhaba OMS uyarı altında oluşturulacak **uyarıları**.</span><span class="sxs-lookup"><span data-stu-id="15a99-304">hello OMS alert will be created under **Alerts**.</span></span> <span data-ttu-id="15a99-305">Merhaba karşılık gelen ITSM bağlantının iş Hello belirtilen uyarının koşulu karşılandığında öğeleri oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="15a99-305">hello corresponding ITSM connection's work items are created when hello specified alert's condition is met.</span></span>

## <a name="create-itsm-work-items-from-oms-logs"></a><span data-ttu-id="15a99-306">OMS günlüklerinden ITSM iş öğeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="15a99-306">Create ITSM work items from OMS logs</span></span>

<span data-ttu-id="15a99-307">OMS günlük arama kullanarak bağlı hello ITSM kaynaklarında iş öğeleri oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="15a99-307">You can create work items in hello connected ITSM sources by using OMS Log Search.</span></span> <span data-ttu-id="15a99-308">toodo aşağıdaki yordamın bu, kullanım hello:</span><span class="sxs-lookup"><span data-stu-id="15a99-308">toodo this, use hello following procedure:</span></span>

1. <span data-ttu-id="15a99-309">Gelen **günlük arama**, gerekli hello veri arama, hello ayrıntı seçin ve'ı tıklatın **oluşturma çalışma öğesini**.</span><span class="sxs-lookup"><span data-stu-id="15a99-309">From **Log Search**,  search hello required data, select hello detail, and click **Create work item**.</span></span>

    <span data-ttu-id="15a99-310">Merhaba **oluşturma ITSM iş öğesi** penceresi görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="15a99-310">hello **Create ITSM Work item** window appears:</span></span>

    ![Günlük analizi ekranı](media/log-analytics-itsmc/itsmc-work-items-from-oms-logs.png)

2.   <span data-ttu-id="15a99-312">Aşağıdaki ayrıntılara hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="15a99-312">Add hello following details:</span></span>

  - <span data-ttu-id="15a99-313">**İş öğesi başlık**: hello iş öğesi için başlık.</span><span class="sxs-lookup"><span data-stu-id="15a99-313">**Work item Title**: Title for hello work item.</span></span>
  - <span data-ttu-id="15a99-314">**İş öğesi tanımı**: hello yeni iş öğesi için bir açıklama.</span><span class="sxs-lookup"><span data-stu-id="15a99-314">**Work item Description**: Description for hello new work item.</span></span>
  - <span data-ttu-id="15a99-315">**Bilgisayar etkilenen**: Bu günlük verileri nerede bulundu hello bilgisayarın adı.</span><span class="sxs-lookup"><span data-stu-id="15a99-315">**Affected Computer**: Name of hello computer where this log data was found.</span></span>
  - <span data-ttu-id="15a99-316">**Bağlantıyı seçin**: ITSM bağlantı istediğiniz toocreate bu iş öğesi.</span><span class="sxs-lookup"><span data-stu-id="15a99-316">**Select Connection**:  ITSM connection in which you want toocreate this work item.</span></span>
  - <span data-ttu-id="15a99-317">**İş öğesi**: iş öğesi türü.</span><span class="sxs-lookup"><span data-stu-id="15a99-317">**Work item**:  Type of work item.</span></span>

3. <span data-ttu-id="15a99-318">toouse var olan bir iş öğesi şablonunu bir olay için tıklatın **Evet** altında **Generate iş öğesi hello şablona dayalı** seçeneğini ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="15a99-318">toouse an existing work item template for an incident, click **Yes** under **Generate work item based on hello template** option and then click **Create**.</span></span>

    <span data-ttu-id="15a99-319">Veya</span><span class="sxs-lookup"><span data-stu-id="15a99-319">Or,</span></span>

    <span data-ttu-id="15a99-320">Tıklatın **Hayır** özelleştirilmiş değerlerinizi tooprovide istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="15a99-320">Click **No** if you want tooprovide your customized values.</span></span>

4. <span data-ttu-id="15a99-321">Merhaba Hello uygun değerleri sağlayın **kişi türündeki**, **etkisi**, **aciliyet**, **kategori**, ve **alt kategori**  metin kutuları ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="15a99-321">Provide hello appropriate values in hello **Contact Type**, **Impact**, **Urgency**, **Category**, and **Sub Category** text boxes, and then click **Create**.</span></span>

<span data-ttu-id="15a99-322">Merhaba iş öğesi hello OMS içinde de görüntüleyebilirsiniz ITSM içinde oluşturulacak.</span><span class="sxs-lookup"><span data-stu-id="15a99-322">hello work item will be created in hello ITSM, which you can also view in OMS.</span></span>

## <a name="troubleshoot-itsm-connections-in-oms"></a><span data-ttu-id="15a99-323">OMS ITSM bağlantı sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="15a99-323">Troubleshoot ITSM connections in OMS</span></span>
1.  <span data-ttu-id="15a99-324">Bağlantı başarısız bağlı kaynağın kullanıcı Arabiriminden ve hello alma **bağlantı kaydetmede hata** iletisi, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="15a99-324">If connection fails from connected source's UI and you get hello **Error in saving connection** message, do hello following:</span></span>
 - <span data-ttu-id="15a99-325">ServiceNow, Cherwell ve Provance bağlantıları durumunda doğru girilen hello kullanıcı adı/parola ve istemci kimliği/istemci parolası hello bağlantıların her biri için olun.</span><span class="sxs-lookup"><span data-stu-id="15a99-325">In case of ServiceNow, Cherwell and Provance connections, ensure you correctly entered  hello username/password and  client ID/client secret  for each of hello connections.</span></span> <span data-ttu-id="15a99-326">Merhaba hata devam ederse hello karşılık gelen ITSM ürün toomake hello bağlantısında yeterli ayrıcalıkları olup olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="15a99-326">If hello error persists, check if you have sufficient privileges  in hello corresponding ITSM product toomake hello connection.</span></span>
 - <span data-ttu-id="15a99-327">Service Manager durumunda hello Web uygulaması başarıyla dağıtılır ve karma bağlantı oluşturulan emin olun.</span><span class="sxs-lookup"><span data-stu-id="15a99-327">In case of Service Manager, ensure that hello Web app is successfully deployed and hybrid connection is created.</span></span> <span data-ttu-id="15a99-328">Merhaba Web uygulaması URL'si hello sağlama hello belgelerinde ayrıntılı olarak ziyaret edin hello şirket içi Service Manager makineyle tooverify hello bağlantı kuran başarıyla [karma bağlantı](log-analytics-itsmc-connections.md#configure-the-hybrid-connection).</span><span class="sxs-lookup"><span data-stu-id="15a99-328">tooverify hello connection is successfully established with hello on-prem Service Manager machine, visit hello  Web app URL as detailed in hello documentation for making hello [hybrid connection](log-analytics-itsmc-connections.md#configure-the-hybrid-connection).</span></span>

2.  <span data-ttu-id="15a99-329">ServiceNow verileri OMS eşitlenmedi, bu hello ServiceNow örneğinin değil uykuda emin olun.</span><span class="sxs-lookup"><span data-stu-id="15a99-329">If data from ServiceNow is not getting synced in OMS, ensure that hello ServiceNow instance is not sleeping.</span></span> <span data-ttu-id="15a99-330">Bu süre hello ServiceNow geliştirme örnekleri, boşta kalma zaman meydana gelir.</span><span class="sxs-lookup"><span data-stu-id="15a99-330">This might sometime happen in hello ServiceNow Dev instances, when idle.</span></span> <span data-ttu-id="15a99-331">Başka rapor hello sorun.</span><span class="sxs-lookup"><span data-stu-id="15a99-331">Else, report hello issue.</span></span>
3.  <span data-ttu-id="15a99-332">OMS uyarıları tetiklenir iş öğelerini ITSM üründe oluşturulmaz veya yapılandırma öğeleri toowork oluşturulan ve bağlantılı öğeler alamıyorsanız ancak veya herhangi bir genel bilgi için aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="15a99-332">If Alerts are getting fired from OMS but work items are not getting created in ITSM product or configuration items are not getting created/linked toowork items or for any generic information, do hello following:</span></span>
 -  <span data-ttu-id="15a99-333">OMS portalı BT Hizmet Yönetimi Bağlayıcısı çözümde kullanılan tooget bağlantıları/iş öğeleri/bilgisayarların vb. özetini olabilir. Merhaba durum dikey penceresinde Hello hata iletisi'ı tıklatın, çok gidin**günlük arama** ve hello hata iletisinde hello ayrıntıları kullanarak hello hatalı hello bağlantı görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="15a99-333">IT Service Management Connector solution in OMS portal could be used tooget a summary of connections/work items/computers etc. Click hello error message in hello status blade, navigate too**Log Search** and view hello connection that has hello error by using hello details in hello error message.</span></span>
 - <span data-ttu-id="15a99-334">hello doğrudan hello hataları ve ilgili bilgileri görüntüleyebilirsiniz **günlük arama** kullanarak sayfa *türü ServiceDeskLog_CL =*.</span><span class="sxs-lookup"><span data-stu-id="15a99-334">you can directly view hello errors/related information in hello **Log Search** page using *Type=ServiceDeskLog_CL*.</span></span>

## <a name="troubleshoot-service-manager-web-app-deployment"></a><span data-ttu-id="15a99-335">Service Manager Web uygulama dağıtım sorunlarını gider</span><span class="sxs-lookup"><span data-stu-id="15a99-335">Troubleshoot Service Manager Web App deployment</span></span>
1.  <span data-ttu-id="15a99-336">Web uygulama dağıtımına herhangi bir sorun olması durumunda hello abonelikte yeterli izinlere sahip olduğundan emin olun toocreate ve dağıtma kaynakları belirtiliyor.</span><span class="sxs-lookup"><span data-stu-id="15a99-336">In case of any trouble with web app deployment, ensure you have sufficient permissions in hello subscription mentioned toocreate/deploy resources.</span></span>
2.  <span data-ttu-id="15a99-337">Varsa **nesne başvurusu bir nesnenin tooinstance ayarlanmamış** hata iletisi görüntüleniyor hello çalıştırılırken [betik](log-analytics-itsmc-service-manager-script.md) altında geçerli değerler girdiğinizden emin olun **Kullanıcı Yapılandırması**bölümü.</span><span class="sxs-lookup"><span data-stu-id="15a99-337">If **Object reference not set tooinstance of an object** error message appears while running hello [script](log-analytics-itsmc-service-manager-script.md) ensure that you entered valid values  under **User Configuration** section.</span></span>
3.  <span data-ttu-id="15a99-338">Toocreate hizmet veri yolu geçişi ad başarısız olursa, o hello kaynak sağlayıcısı hello abonelikte kayıtlı gerekli emin olun.</span><span class="sxs-lookup"><span data-stu-id="15a99-338">If you fail toocreate service bus relay namespace, ensure that hello required resource provider is registered in hello subscription.</span></span> <span data-ttu-id="15a99-339">El ile kayıtlı değil, Azure portal hello oluşturun.</span><span class="sxs-lookup"><span data-stu-id="15a99-339">If not registered, manually create it from hello Azure portal.</span></span> <span data-ttu-id="15a99-340">Bunu sırasında da oluşturabilirsiniz [hello karma bağlantı oluşturma](log-analytics-itsmc-connections.md#configure-the-hybrid-connection) hello Azure Portalı'ndan.</span><span class="sxs-lookup"><span data-stu-id="15a99-340">You can also create it while [creating hello hybrid connection](log-analytics-itsmc-connections.md#configure-the-hybrid-connection) from hello Azure portal.</span></span>


## <a name="contact-us"></a><span data-ttu-id="15a99-341">Bizimle iletişim kurun</span><span class="sxs-lookup"><span data-stu-id="15a99-341">Contact us</span></span>

<span data-ttu-id="15a99-342">Tüm sorgular veya hello BT Hizmet Yönetimi Bağlayıcısı geribildirim için adresinden bize başvurun [ omsitsmfeedback@microsoft.com ](mailto:omsitsmfeedback@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="15a99-342">For any queries or feedback on hello IT Service Management Connector, contact us at [omsitsmfeedback@microsoft.com](mailto:omsitsmfeedback@microsoft.com).</span></span>

## <a name="next-steps"></a><span data-ttu-id="15a99-343">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="15a99-343">Next steps</span></span>
<span data-ttu-id="15a99-344">[ITSM ürünler/hizmetler tooIT Hizmet Yönetimi Bağlayıcısı eklemek](log-analytics-itsmc-connections.md).</span><span class="sxs-lookup"><span data-stu-id="15a99-344">[Add ITSM products/services tooIT Service Management Connector](log-analytics-itsmc-connections.md).</span></span>
