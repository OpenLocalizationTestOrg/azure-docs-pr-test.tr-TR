---
title: "B2B tümleştirme hesabı - Azure Logic Apps için aaaDisaster kurtarma | Microsoft Docs"
description: "Logic Apps B2B olağanüstü durum kurtarma"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: cf44af18-1fe5-41d5-9e06-cc57a968207c
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/10/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: e86564a3c5a2607d22514936c606e2843cba0416
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="logic-apps-b2b-cross-region-disaster-recovery"></a><span data-ttu-id="4ba8b-103">Logic Apps B2B çapraz bölge olağanüstü durum kurtarma</span><span class="sxs-lookup"><span data-stu-id="4ba8b-103">Logic Apps B2B cross-region disaster recovery</span></span>

<span data-ttu-id="4ba8b-104">B2B iş yükleri siparişler ve faturalar gibi para işlemleri içerir.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-104">B2B workloads involve money transactions like orders and invoices.</span></span> <span data-ttu-id="4ba8b-105">Bir olağanüstü sırasında iş düzeyi SLA kendi iş ortaklarıyla üzerinde anlaşmaya varılan bir iş tooquickly kurtarma toomeet hello önemlidir.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-105">During a disaster event, it's critical for a business tooquickly recover toomeet hello business-level SLAs agreed upon with their partners.</span></span> <span data-ttu-id="4ba8b-106">Bu makalede, toobuild iş sürekliliği planınızı B2B iş yükleri için nasıl gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-106">This article demonstrates how toobuild a business continuity plan for B2B workloads.</span></span> 

* <span data-ttu-id="4ba8b-107">Olağanüstü Durum Kurtarma Hazırlık</span><span class="sxs-lookup"><span data-stu-id="4ba8b-107">Disaster Recovery readiness</span></span> 
* <span data-ttu-id="4ba8b-108">Toosecondary bölge bir olağanüstü durum olay sırasında başarısız oluyor</span><span class="sxs-lookup"><span data-stu-id="4ba8b-108">Fail over toosecondary region during a disaster event</span></span> 
* <span data-ttu-id="4ba8b-109">Tooprimary bölge olağanüstü sonra geri dönüş</span><span class="sxs-lookup"><span data-stu-id="4ba8b-109">Fall back tooprimary region after a disaster event</span></span>

## <a name="disaster-recovery-readiness"></a><span data-ttu-id="4ba8b-110">Olağanüstü Durum Kurtarma Hazırlık</span><span class="sxs-lookup"><span data-stu-id="4ba8b-110">Disaster Recovery readiness</span></span>  

1. <span data-ttu-id="4ba8b-111">Bir ikincil bölge tanımlayabilir ve oluşturabilirsiniz bir [tümleştirme hesabını](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) hello ikincil bölge içinde.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-111">Identify a secondary region and create an [integration account](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) in hello secondary region.</span></span>

2. <span data-ttu-id="4ba8b-112">İş ortakları, şemalar ve burada çalışma durumu hello çoğaltılan toobe toosecondary bölge tümleştirme hesabının gerekir gerekli hello ileti akışları için anlaşmaları ekleyin.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-112">Add partners, schemas, and agreements for hello required message flows where hello run status needs toobe replicated toosecondary region integration account.</span></span>

   > [!TIP]
   > <span data-ttu-id="4ba8b-113">Tutarlılık hello tümleştirme hesap yapı'nın Adlandırma kuralında bölgeler arasında olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-113">Make sure there's consistency in hello integration account artifact's naming convention across regions.</span></span> 

3. <span data-ttu-id="4ba8b-114">Merhaba birincil bölgesinden çalışma durumu toopull hello hello ikincil bölge'de bir mantıksal uygulama oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-114">toopull hello run status from hello primary region, create a logic app in hello secondary region.</span></span> 

   <span data-ttu-id="4ba8b-115">Bu mantıksal uygulama olmalıdır bir *tetikleyici* ve bir *eylem*.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-115">This logic app should have a *trigger* and an *action*.</span></span> 
   <span data-ttu-id="4ba8b-116">Merhaba tetikleyici tooprimary bölge tümleştirme hesabını bağlaması ve hello eylem toosecondary bölge tümleştirme hesabını bağlaması.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-116">hello trigger should connect tooprimary region integration account, and hello action should connect toosecondary region integration account.</span></span> 
   <span data-ttu-id="4ba8b-117">Merhaba zaman aralığına dayalı, hello tetikleyici hello çalıştırmak birincil bölge durumu tablosu yoklar ve hello yeni kayıtlar varsa çeker.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-117">Based on hello time interval, hello trigger polls hello primary region run status table and pulls hello new records, if any.</span></span> <span data-ttu-id="4ba8b-118">Merhaba eylem bunları toosecondary bölge tümleştirme hesabını güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-118">hello action updates them toosecondary region integration account.</span></span> 
   <span data-ttu-id="4ba8b-119">Bu, birincil bölge toosecondary bölgesinden tooget artımlı çalışma zamanı durumu yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-119">This helps tooget incremental runtime status from primary region toosecondary region.</span></span>

4. <span data-ttu-id="4ba8b-120">İş sürekliliği tümleştirme hesabıdır Logic Apps içinde B2B protokolleri - X12, AS2 ve EDIFACT temel toosupport tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-120">Business continuity in Logic Apps integration account is designed toosupport based on B2B protocols - X12, AS2, and EDIFACT.</span></span> <span data-ttu-id="4ba8b-121">adımları toofind ayrıntılı, ilgili bağlantıları seçin hello.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-121">toofind detailed steps, select hello respective links.</span></span>

5. <span data-ttu-id="4ba8b-122">Merhaba öneri toodeploy ikincil bir bölgede tüm birincil bölge kaynakları çok uzun.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-122">hello recommendation is toodeploy all primary region resources in a secondary region too.</span></span> 

   <span data-ttu-id="4ba8b-123">Azure SQL Database veya Azure Cosmos DB, Azure Service Bus ve Azure olay hub'ın Mesajlaşma, Azure API Management ve Azure App Service hello Azure Logic Apps özelliği için kullanılan birincil bölge kaynaklar içerir.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-123">Primary region resources include Azure SQL Database or Azure Cosmos DB, Azure Service Bus and Azure Event Hubs used for messaging, Azure API Management, and hello Azure Logic Apps feature in Azure App Service.</span></span>   

6. <span data-ttu-id="4ba8b-124">Bir birincil bölge tooa ikincil bölge arasında bağlantı kurun.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-124">Establish a connection from a primary region tooa secondary region.</span></span> <span data-ttu-id="4ba8b-125">bir birincil bölge durumunu çalıştırmak toopull hello ikincil bir bölgede bir mantıksal uygulama oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-125">toopull hello run status from a primary region, create a logic app in a secondary region.</span></span> 

   <span data-ttu-id="4ba8b-126">Merhaba mantıksal uygulama tetikleyici ve eylem olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-126">hello logic app should have a trigger and an action.</span></span> 
   <span data-ttu-id="4ba8b-127">Merhaba tetikleyici tooa birincil bölge tümleştirme hesabını bağlanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-127">hello trigger should connect tooa primary region integration account.</span></span> 
   <span data-ttu-id="4ba8b-128">Merhaba eylem tooa ikincil bölge tümleştirme hesabını bağlanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-128">hello action should connect tooa secondary region integration account.</span></span> 
   <span data-ttu-id="4ba8b-129">Merhaba zaman aralığına dayalı, hello tetikleyici hello çalıştırmak birincil bölge durumu tablosu yoklar ve hello yeni kayıtlar varsa çeker.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-129">Based on hello time interval, hello trigger polls hello primary region run status table and pulls hello new records, if any.</span></span> 
   <span data-ttu-id="4ba8b-130">Merhaba eylem bunları tooa ikincil bölge tümleştirme hesabını güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-130">hello action updates them tooa secondary region integration account.</span></span> 
   <span data-ttu-id="4ba8b-131">Bu işlem tooget artımlı çalışma zamanı durumu hello birincil bölge toohello ikincil bölge ' yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-131">This process helps tooget incremental runtime status from hello primary region toohello secondary region.</span></span>

<span data-ttu-id="4ba8b-132">Logic Apps tümleştirme hesabında iş sürekliliği hello B2B protokolleri X12, AS2 ve EDIFACT göre desteği sağlar.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-132">Business continuity in a Logic Apps integration account provides support based on hello B2B protocols X12, AS2, and EDIFACT.</span></span> <span data-ttu-id="4ba8b-133">X12 ve AS2 kullanma hakkında ayrıntılı adımlar için bkz: [X12](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#x12) ve [AS2](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#as2) bu makalede.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-133">For detailed steps on using X12 and AS2, see [X12](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#x12) and [AS2](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#as2) in this article.</span></span>

## <a name="fail-over-tooa-secondary-region-during-a-disaster-event"></a><span data-ttu-id="4ba8b-134">Tooa ikincil bölge bir olağanüstü durum olay sırasında başarısız oluyor</span><span class="sxs-lookup"><span data-stu-id="4ba8b-134">Fail over tooa secondary region during a disaster event</span></span>

<span data-ttu-id="4ba8b-135">Olağanüstü durum olay sırasında iş sürekliliği, doğrudan trafiği toohello ikincil bölge Hello birincil bölge bulunmaması durumunda.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-135">During a disaster event, when hello primary region is not available for business continuity, direct traffic toohello secondary region.</span></span> <span data-ttu-id="4ba8b-136">Bir iş toorecover hızla RPO'ya/RTO'ya anlaşmaya varılan toomeet hello ortakları tarafından işlevleri ikincil bölge yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-136">A secondary region helps a business toorecover functions quickly toomeet hello RPO/RTO agreed upon by their partners.</span></span> <span data-ttu-id="4ba8b-137">Bu ayrıca çaba toofail üzerinden bir bölge tooanother bölgesinden en aza indirir.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-137">It also minimizes efforts toofail over from one region tooanother region.</span></span> 

<span data-ttu-id="4ba8b-138">Bir birincil bölge tooa ikincil bölge ' denetim numaraları kopyalanırken beklenen bir gecikme süresi yok.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-138">There is an expected latency while copying control numbers from a primary region tooa secondary region.</span></span> <span data-ttu-id="4ba8b-139">Yinelenen oluşturulan denetim gönderme tooavoid sırasında bir olağanüstü toopartners sayılar, hello öneri tooincrement hello denetim numaraları hello ikincil bölge sözleşmelerde kullanarak [PowerShell cmdlet'leri](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).</span><span class="sxs-lookup"><span data-stu-id="4ba8b-139">tooavoid sending duplicate generated control numbers toopartners during a disaster event, hello recommendation is tooincrement hello control numbers in hello secondary region agreements by using [PowerShell cmdlets](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).</span></span>

## <a name="fall-back-tooa-primary-region-post-disaster-event"></a><span data-ttu-id="4ba8b-140">Geri dönüş tooa birincil bölge sonrası olağanüstü</span><span class="sxs-lookup"><span data-stu-id="4ba8b-140">Fall back tooa primary region post-disaster event</span></span>

<span data-ttu-id="4ba8b-141">mevcut olduğunda toofall geri tooa birincil bölge şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="4ba8b-141">toofall back tooa primary region when it is available, follow these steps:</span></span>

1. <span data-ttu-id="4ba8b-142">Merhaba ikincil bölge'de ortakları gelen iletileri kabul durdurun.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-142">Stop accepting messages from partners in hello secondary region.</span></span>  

2. <span data-ttu-id="4ba8b-143">Artır tüm hello birincil bölge anlaşmalar için oluşturulan hello denetim numaraları kullanarak [PowerShell cmdlet'leri](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).</span><span class="sxs-lookup"><span data-stu-id="4ba8b-143">Increment hello generated control numbers for all hello primary region agreements by using [PowerShell cmdlets](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).</span></span>  

3. <span data-ttu-id="4ba8b-144">Merhaba ikincil bölge toohello birincil bölge doğrudan trafiğinden.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-144">Direct traffic from hello secondary region toohello primary region.</span></span>

4. <span data-ttu-id="4ba8b-145">Çalışma durumu hello birincil bölgesinden çekmek için hello ikincil bölgede oluşturulan bu hello mantıksal uygulama etkinleştirildiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-145">Check that hello logic app created in hello secondary region for pulling run status from hello primary region is enabled.</span></span>

## <a name="x12"></a><span data-ttu-id="4ba8b-146">X12</span><span class="sxs-lookup"><span data-stu-id="4ba8b-146">X12</span></span> 

<span data-ttu-id="4ba8b-147">EDI iş sürekliliği X 12 belgeler üzerinde denetim numaraları dayanır:</span><span class="sxs-lookup"><span data-stu-id="4ba8b-147">Business continuity for EDI X12 documents is based on control numbers:</span></span>

> [!TIP]
> <span data-ttu-id="4ba8b-148">Merhaba de kullanabilirsiniz [X12 hızlı başlatma şablonunu](https://azure.microsoft.com/documentation/templates/201-logic-app-x12-disaster-recovery-replication/) toocreate mantıksal uygulamalar.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-148">You can also use hello [X12 quick start template](https://azure.microsoft.com/documentation/templates/201-logic-app-x12-disaster-recovery-replication/) toocreate logic apps.</span></span> <span data-ttu-id="4ba8b-149">Oluşturma birincil ve ikincil tümleştirme Önkoşullar toouse hello şablon hesaplarıdır.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-149">Creating primary and secondary integration accounts are prerequisites toouse hello template.</span></span> <span data-ttu-id="4ba8b-150">Merhaba şablonu toocreate iki logic apps, alınan denetim numaraları için bir ve oluşturulan denetim numaraları için başka bir yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-150">hello template helps toocreate two logic apps, one for received control numbers and another for generated control numbers.</span></span> <span data-ttu-id="4ba8b-151">İlgili tetikleyiciler ve Eylemler hello tetikleyici toohello birincil tümleştirme hesabı ve hello eylem toohello ikincil tümleştirme hesabı bağlanma hello logic apps içinde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-151">Respective triggers and actions are created in hello logic apps, connecting hello trigger toohello primary integration account and hello action toohello secondary integration account.</span></span>

<span data-ttu-id="4ba8b-152">**Önkoşullar**</span><span class="sxs-lookup"><span data-stu-id="4ba8b-152">**Prerequisites**</span></span>

<span data-ttu-id="4ba8b-153">gelen iletiler için tooenable olağanüstü durum kurtarma hello X12 anlaşmanın alma ayarlarında hello yinelenen onay ayarlarını seçin.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-153">tooenable disaster recovery for inbound messages, select hello duplicate check settings in hello X12 agreement's Receive Settings.</span></span>

![Yinelenen onay ayarlarını Seç](./media/logic-apps-enterprise-integration-b2b-business-continuity/dupcheck.png)  

1. <span data-ttu-id="4ba8b-155">Oluşturma bir [mantıksal uygulama](../logic-apps/logic-apps-create-a-logic-app.md) ikincil bir bölgede.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-155">Create a [logic app](../logic-apps/logic-apps-create-a-logic-app.md) in a secondary region.</span></span>    

2. <span data-ttu-id="4ba8b-156">Arama **X12**seçip **bir denetim numarasını değiştirildiğinde X12-**.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-156">Search on **X12**, and select **X12 - When a control number is modified**.</span></span>   

   ![X12 arayın](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn1.png)

   <span data-ttu-id="4ba8b-158">Merhaba tetikleyici bağlantı tooan tümleştirme hesabı tooestablish ister.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-158">hello trigger prompts you tooestablish a connection tooan integration account.</span></span> 
   <span data-ttu-id="4ba8b-159">Merhaba tetikleyici olmalıdır bağlı tooa birincil bölge tümleştirme hesabı.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-159">hello trigger should be connected tooa primary region integration account.</span></span>

3. <span data-ttu-id="4ba8b-160">Bir bağlantı adı girin, seçin, *birincil bölge tümleştirme hesabını* hello gelen listelemek ve seçin **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-160">Enter a connection name, select your *primary region integration account* from hello list, and choose **Create**.</span></span>   

   ![Birincil bölge tümleştirme hesap adı](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn2.png)

4. <span data-ttu-id="4ba8b-162">Merhaba **DateTime toostart denetim sayı eşitleme** ayardır isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-162">hello **DateTime toostart control number sync** setting is optional.</span></span> <span data-ttu-id="4ba8b-163">Merhaba **sıklığı** çok ayarlanabilir**gün**, **saat**, **Minute**, veya **ikinci** bir aralık ile.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-163">hello **Frequency** can be set too**Day**, **Hour**, **Minute**, or **Second** with an interval.</span></span>   

   ![DateTime ve sıklığı](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn3.png)

5. <span data-ttu-id="4ba8b-165">Seçin **yeni adım** > **Eylem Ekle**.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-165">Select **New step** > **Add an action**.</span></span>

   ![Yeni adım, bir eylem Ekle](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn4.png)

6. <span data-ttu-id="4ba8b-167">Arama **X12**seçip **X12-ekleme veya güncelleştirme denetim numaraları**.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-167">Search on **X12**, and select **X12 - Add or update control numbers**.</span></span>   

   ![Ekleyin veya denetim numaraları güncelleştirin](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn5.png)

7. <span data-ttu-id="4ba8b-169">tooconnect bir eylem tooa ikincil bölge tümleştirme hesabı seçin **değiştirmek bağlantı** > **yeni bağlantı ekleme** hello kullanılabilir tümleştirme hesapları listesi.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-169">tooconnect an action tooa secondary region integration account, select **Change connection** > **Add new connection** for a list of hello available integration accounts.</span></span> <span data-ttu-id="4ba8b-170">Bir bağlantı adı girin, seçin, *ikincil bölge tümleştirme hesabını* hello gelen listelemek ve seçin **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-170">Enter a connection name, select your *secondary region integration account* from hello list, and choose **Create**.</span></span> 

   ![İkincil bölge tümleştirme hesap adı](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn6.png)

8. <span data-ttu-id="4ba8b-172">Tooraw girişleri sağ üst köşesinde hello simgesine tıklayarak geçin.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-172">Switch tooraw inputs by clicking on hello icon in upper right corner.</span></span>

   ![Anahtar tooraw girişleri](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12rawinputs.png)

9. <span data-ttu-id="4ba8b-174">Gövde hello dinamik içerik seçiciden seçin ve hello mantıksal uygulama kaydedin.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-174">Select Body from hello dynamic content picker, and save hello logic app.</span></span>

   ![Dinamik içerik alanları](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn7.png)

   <span data-ttu-id="4ba8b-176">Merhaba zaman aralığına dayalı, hello tetikleyici hello alınan birincil bölge denetim sayı tablosunu yoklar ve hello yeni kayıtlar çeker.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-176">Based on hello time interval, hello trigger polls hello primary region received control number table and pulls hello new records.</span></span> 
   <span data-ttu-id="4ba8b-177">Hello eylemin hello ikincil bölge tümleştirme hesabındaki hello kayıtlarını güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-177">hello action updates hello records in hello secondary region integration account.</span></span> 
   <span data-ttu-id="4ba8b-178">Herhangi bir güncelleştirme varsa, hello tetikleyici durum olarak görünür **Atlanan**.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-178">If there are no updates, hello trigger status appears as **Skipped**.</span></span>   

   ![Denetim sayı tablosu](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12recevicedcn8.png)

<span data-ttu-id="4ba8b-180">Merhaba zaman aralığında, bir birincil bölge tooa ikincil bölge ' hello artımlı çalışma zamanı durumu çoğaltır.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-180">Based on hello time interval, hello incremental runtime status replicates from a primary region tooa secondary region.</span></span> <span data-ttu-id="4ba8b-181">Olağanüstü durum olay sırasında iş sürekliliği için kullanılabilir, doğrudan trafiğini toohello ikincil bölge Hello birincil bölge değilse.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-181">During a disaster event, when hello primary region is not available, direct traffic toohello secondary region for business continuity.</span></span> 

## <a name="edifact"></a><span data-ttu-id="4ba8b-182">EDIFACT</span><span class="sxs-lookup"><span data-stu-id="4ba8b-182">EDIFACT</span></span> 

<span data-ttu-id="4ba8b-183">İş sürekliliği EDI EDIFACT belgeler için Denetim numaralarında temel alır.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-183">Business continuity for EDI EDIFACT documents is based on control numbers.</span></span>

<span data-ttu-id="4ba8b-184">**Önkoşullar**</span><span class="sxs-lookup"><span data-stu-id="4ba8b-184">**Prerequisites**</span></span>

<span data-ttu-id="4ba8b-185">tooenable olağanüstü durum kurtarma gelen iletiler için EDIFACT anlaşmanızın alma ayarlarında hello yinelenen onay ayarlarını seçin.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-185">tooenable disaster recovery for inbound messages, select hello duplicate check settings in your EDIFACT agreement's Receive Settings.</span></span>

![Yinelenen onay ayarlarını Seç](./media/logic-apps-enterprise-integration-b2b-business-continuity/edifactdupcheck.png)  

1. <span data-ttu-id="4ba8b-187">Oluşturma bir [mantıksal uygulama](../logic-apps/logic-apps-create-a-logic-app.md) ikincil bir bölgede.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-187">Create a [logic app](../logic-apps/logic-apps-create-a-logic-app.md) in a secondary region.</span></span>    

2. <span data-ttu-id="4ba8b-188">Arama **EDIFACT**seçip **bir denetim numarasını değiştirildiğinde EDIFACT -**.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-188">Search on **EDIFACT**, and select **EDIFACT - When a control number is modified**.</span></span>

   ![EDIFACT arayın](./media/logic-apps-enterprise-integration-b2b-business-continuity/edifactcn1.png)

   <span data-ttu-id="4ba8b-190">Merhaba tetikleyici bağlantı tooan tümleştirme hesabı tooestablish ister.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-190">hello trigger prompts you tooestablish a connection tooan integration account.</span></span> 
   <span data-ttu-id="4ba8b-191">Merhaba tetikleyici olmalıdır bağlı tooa birincil bölge tümleştirme hesabı.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-191">hello trigger should be connected tooa primary region integration account.</span></span> 

3. <span data-ttu-id="4ba8b-192">Bir bağlantı adı girin, seçin, *birincil bölge tümleştirme hesabını* hello gelen listelemek ve seçin **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-192">Enter a connection name, select your *primary region integration account* from hello list, and choose **Create**.</span></span>    

   ![Birincil bölge tümleştirme hesap adı](./media/logic-apps-enterprise-integration-b2b-business-continuity/X12CN2.png)

4. <span data-ttu-id="4ba8b-194">Merhaba **DateTime toostart denetim sayı eşitleme** ayardır isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-194">hello **DateTime toostart control number sync** setting is optional.</span></span> <span data-ttu-id="4ba8b-195">Merhaba **sıklığı** çok ayarlanabilir**gün**, **saat**, **Minute**, veya **ikinci** bir aralık ile.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-195">hello **Frequency** can be set too**Day**, **Hour**, **Minute**, or **Second** with an interval.</span></span>    

   ![DateTime ve sıklığı](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn3.png)

6. <span data-ttu-id="4ba8b-197">Seçin **yeni adım** > **Eylem Ekle**.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-197">Select **New step** > **Add an action**.</span></span>    

   ![Yeni adım, bir eylem Ekle](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn4.png)

7. <span data-ttu-id="4ba8b-199">Arama **EDIFACT**seçip **EDIFACT - ekleme veya güncelleştirme denetim numaraları**.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-199">Search on **EDIFACT**, and select **EDIFACT - Add or update control numbers**.</span></span>   

   ![Ekleyin veya denetim numaraları güncelleştirin](./media/logic-apps-enterprise-integration-b2b-business-continuity/EdifactChooseAction.png)

8. <span data-ttu-id="4ba8b-201">tooconnect bir eylem tooa ikincil bölge tümleştirme hesabı seçin **değiştirmek bağlantı** > **yeni bağlantı ekleme** hello kullanılabilir tümleştirme hesapları listesi.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-201">tooconnect an action tooa secondary region integration account, select **Change connection** > **Add new connection** for a list of hello available integration accounts.</span></span> <span data-ttu-id="4ba8b-202">Bir bağlantı adı girin, seçin, *ikincil bölge tümleştirme hesabını* hello gelen listelemek ve seçin **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-202">Enter a connection name, select your *secondary region integration account* from hello list, and choose **Create**.</span></span>

   ![İkincil bölge tümleştirme hesap adı](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn6.png)

9. <span data-ttu-id="4ba8b-204">Tooraw girişleri sağ üst köşesinde hello simgesine tıklayarak geçin.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-204">Switch tooraw inputs by clicking on hello icon in upper right corner.</span></span>

   ![Anahtar tooraw girişleri](./media/logic-apps-enterprise-integration-b2b-business-continuity/Edifactrawinputs.png)

10. <span data-ttu-id="4ba8b-206">Gövde hello dinamik içerik seçiciden seçin ve hello mantıksal uygulama kaydedin.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-206">Select Body from hello dynamic content picker, and save hello logic app.</span></span>   

   ![Dinamik içerik alanları](./media/logic-apps-enterprise-integration-b2b-business-continuity/X12CN7.png)

   <span data-ttu-id="4ba8b-208">Merhaba zaman aralığına dayalı, hello tetikleyici hello alınan birincil bölge denetim sayı tablosunu yoklar ve hello yeni kayıtlar çeker.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-208">Based on hello time interval, hello trigger polls hello primary region received control number table and pulls hello new records.</span></span>
   <span data-ttu-id="4ba8b-209">Merhaba eylemin hello kayıtları toohello ikincil bölge tümleştirme hesabını güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-209">hello action updates hello records toohello secondary region integration account.</span></span> 
   <span data-ttu-id="4ba8b-210">Herhangi bir güncelleştirme varsa, hello tetikleyici durum olarak görünür **Atlanan**.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-210">If there are no updates, hello trigger status appears as **Skipped**.</span></span>

   ![Denetim sayı tablosu](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12recevicedcn8.png)

<span data-ttu-id="4ba8b-212">Merhaba zaman aralığında, bir birincil bölge tooa ikincil bölge ' hello artımlı çalışma zamanı durumu çoğaltır.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-212">Based on hello time interval, hello incremental runtime status replicates from a primary region tooa secondary region.</span></span> <span data-ttu-id="4ba8b-213">Olağanüstü durum olay sırasında iş sürekliliği için kullanılabilir, doğrudan trafiğini toohello ikincil bölge Hello birincil bölge değilse.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-213">During a disaster event, when hello primary region is not available, direct traffic toohello secondary region for business continuity.</span></span> 

## <a name="as2"></a><span data-ttu-id="4ba8b-214">AS2</span><span class="sxs-lookup"><span data-stu-id="4ba8b-214">AS2</span></span> 

<span data-ttu-id="4ba8b-215">İş sürekliliği hello AS2 protokolünü kullanan belgeler için hello ileti kimliği ve hello MIC değeri temel alır.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-215">Business continuity for documents that use hello AS2 protocol is based on hello message ID and hello MIC value.</span></span>

> [!TIP]
> <span data-ttu-id="4ba8b-216">Merhaba de kullanabilirsiniz [AS2 Hızlı Başlangıç şablonu](https://github.com/Azure/azure-quickstart-templates/pull/3302) toocreate mantıksal uygulamalar.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-216">You can also use hello [AS2 quick start template](https://github.com/Azure/azure-quickstart-templates/pull/3302) toocreate logic apps.</span></span> <span data-ttu-id="4ba8b-217">Oluşturma birincil ve ikincil tümleştirme Önkoşullar toouse hello şablon hesaplarıdır.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-217">Creating primary and secondary integration accounts are prerequisites toouse hello template.</span></span> <span data-ttu-id="4ba8b-218">Merhaba şablonu bir tetikleyici ve eylem sahip bir mantıksal uygulama oluşturma yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-218">hello template helps create a logic app that has a trigger and an action.</span></span> <span data-ttu-id="4ba8b-219">Merhaba mantıksal uygulama, bir tetikleyici tooa birincil tümleştirme hesabı ve eylem tooa ikincil tümleştirme hesabı bir bağlantı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-219">hello logic app creates a connection from a trigger tooa primary integration account and an action tooa secondary integration account.</span></span>

1. <span data-ttu-id="4ba8b-220">Oluşturma bir [mantıksal uygulama](../logic-apps/logic-apps-create-a-logic-app.md) hello ikincil bölge içinde.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-220">Create a [logic app](../logic-apps/logic-apps-create-a-logic-app.md) in hello secondary region.</span></span>  

2. <span data-ttu-id="4ba8b-221">Arama **AS2**seçip **AS2 - olduğunda bir MIC değer oluşturulur**.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-221">Search on **AS2**, and select **AS2 - When a MIC value is created**.</span></span>   

   ![AS2 arayın](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid1.png)

   <span data-ttu-id="4ba8b-223">Bir tetikleyici tooestablish bağlantı tooan tümleştirme hesabı ister.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-223">A trigger prompts you tooestablish a connection tooan integration account.</span></span> 
   <span data-ttu-id="4ba8b-224">Merhaba tetikleyici olmalıdır bağlı tooa birincil bölge tümleştirme hesabı.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-224">hello trigger should be connected tooa primary region integration account.</span></span> 
   
3. <span data-ttu-id="4ba8b-225">Bir bağlantı adı girin, seçin, *birincil bölge tümleştirme hesabını* hello gelen listelemek ve seçin **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-225">Enter a connection name, select your *primary region integration account* from hello list, and choose **Create**.</span></span>

   ![Birincil bölge tümleştirme hesap adı](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid2.png)

4. <span data-ttu-id="4ba8b-227">Merhaba **DateTime toostart MIC değer eşitleme** ayardır isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-227">hello **DateTime toostart MIC value sync** setting is optional.</span></span> <span data-ttu-id="4ba8b-228">Merhaba **sıklığı** çok ayarlanabilir**gün**, **saat**, **Minute**, veya **ikinci** bir aralık ile.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-228">hello **Frequency** can be set too**Day**, **Hour**, **Minute**, or **Second** with an interval.</span></span>   

   ![DateTime ve sıklığı](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid3.png)

5. <span data-ttu-id="4ba8b-230">Seçin **yeni adım** > **Eylem Ekle**.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-230">Select **New step** > **Add an action**.</span></span>  

   ![Yeni adım, bir eylem Ekle](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid4.png)

6. <span data-ttu-id="4ba8b-232">Arama **AS2**seçip **AS2 - MIC içeriği güncelleştirmek ya da eklemek**.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-232">Search on **AS2**, and select **AS2 - Add or update MIC contents**.</span></span>  

   ![MIC ekleme veya güncelleştirme](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid5.png)

7. <span data-ttu-id="4ba8b-234">tooconnect bir eylem tooa ikincil tümleştirme hesabı seçin **değiştirmek bağlantı** > **yeni bağlantı ekleme** hello kullanılabilir tümleştirme hesapları listesi.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-234">tooconnect an action tooa secondary integration account, select **Change connection** > **Add new connection** for a list of hello available integration accounts.</span></span> <span data-ttu-id="4ba8b-235">Bir bağlantı adı girin, seçin, *ikincil bölge tümleştirme hesabını* hello gelen listelemek ve seçin **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-235">Enter a connection name, select your *secondary region integration account* from hello list, and choose **Create**.</span></span>

   ![İkincil bölge tümleştirme hesap adı](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid6.png)

8. <span data-ttu-id="4ba8b-237">Tooraw girişleri sağ üst köşesinde hello simgesine tıklayarak geçin.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-237">Switch tooraw inputs by clicking on hello icon in upper right corner.</span></span>

   ![Anahtar tooraw girişleri](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2rawinputs.png)

9. <span data-ttu-id="4ba8b-239">Gövde hello dinamik içerik seçiciden seçin ve hello mantıksal uygulama kaydedin.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-239">Select Body from hello dynamic content picker, and save hello logic app.</span></span>   

   ![Dinamik içerik](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid7.png)

   <span data-ttu-id="4ba8b-241">Merhaba zaman aralığına dayalı, hello tetikleyici hello birincil bölge tablo yoklar ve hello yeni kayıtlar çeker.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-241">Based on hello time interval, hello trigger polls hello primary region table and pulls hello new records.</span></span> <span data-ttu-id="4ba8b-242">Merhaba eylem bunları toohello ikincil bölge tümleştirme hesabını güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-242">hello action updates them toohello secondary region integration account.</span></span> 
   <span data-ttu-id="4ba8b-243">Herhangi bir güncelleştirme varsa, hello tetikleyici durum olarak görünür **Atlanan**.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-243">If there are no updates, hello trigger status appears as **Skipped**.</span></span>  

   ![Birincil bölge tablosu](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid8.png)

<span data-ttu-id="4ba8b-245">Merhaba zaman aralığına dayalı, hello artımlı çalışma zamanı durumu hello birincil bölge toohello ikincil bölge ' çoğaltır.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-245">Based on hello time interval, hello incremental runtime status replicates from hello primary region toohello secondary region.</span></span> <span data-ttu-id="4ba8b-246">Olağanüstü durum olay sırasında iş sürekliliği için kullanılabilir, doğrudan trafiğini toohello ikincil bölge Hello birincil bölge değilse.</span><span class="sxs-lookup"><span data-stu-id="4ba8b-246">During a disaster event, when hello primary region is not available, direct traffic toohello secondary region for business continuity.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="4ba8b-247">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4ba8b-247">Next steps</span></span>

[<span data-ttu-id="4ba8b-248">B2B iletilerini izleme</span><span class="sxs-lookup"><span data-stu-id="4ba8b-248">Monitor B2B messages</span></span>](logic-apps-monitor-b2b-message.md)

