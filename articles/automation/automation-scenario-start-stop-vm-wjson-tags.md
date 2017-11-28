---
title: "JSON biçimli etiketler tooschedule Azure VM durumunu aaaUse | Microsoft Docs"
description: "Bu makalede etiketler tooautomate hello VM başlatma ve kapatma zamanlama üzerinde nasıl toouse JSON dizeler gösterilmektedir."
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
ms.assetid: 6afed5d2-e939-4749-8b2c-9312b4c16fb2
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: magoedte;paulomarquesc
ms.openlocfilehash: f6bbf1dea1c193e5d1010f12f3b1ed63562f9daf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario-using-json-formatted-tags-toocreate-a-schedule-for-azure-vm-startup-and-shutdown"></a><span data-ttu-id="3aa9e-103">Azure otomasyonu senaryosu: kullanarak JSON biçimli etiketler toocreate Azure VM başlatma ve kapatma için bir zamanlama</span><span class="sxs-lookup"><span data-stu-id="3aa9e-103">Azure Automation scenario: Using JSON-formatted tags toocreate a schedule for Azure VM startup and shutdown</span></span>
<span data-ttu-id="3aa9e-104">Müşteriler genellikle tooschedule hello başlangıç istediğiniz ve sanal makineleri toohelp kapatma abonelik maliyetlerini azaltmak veya işletme ve teknik gereksinimleri destekler.</span><span class="sxs-lookup"><span data-stu-id="3aa9e-104">Customers often want tooschedule hello startup and shutdown of virtual machines toohelp reduce subscription costs or support business and technical requirements.</span></span>

<span data-ttu-id="3aa9e-105">Merhaba aşağıdaki senaryoyu tooset otomatik başlatma ve kapatma, VM'lerin bir kaynak grubu düzeyinde veya azure'da sanal makine düzeyinde Schedule adlı bir etiket kullanarak sağlar.</span><span class="sxs-lookup"><span data-stu-id="3aa9e-105">hello following scenario enables you tooset up automated startup and shutdown of your VMs by using a tag called Schedule at a resource group level or virtual machine level in Azure.</span></span> <span data-ttu-id="3aa9e-106">Bu zamanlamanın başlangıç zamanı ve kapatma süresi ile Pazar tooSaturday gelen yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="3aa9e-106">This schedule can be configured from Sunday tooSaturday with a startup time and shutdown time.</span></span>

<span data-ttu-id="3aa9e-107">Biz, bazı Giden kutusu seçeneğiniz vardır.</span><span class="sxs-lookup"><span data-stu-id="3aa9e-107">We do have some out-of-the-box options.</span></span> <span data-ttu-id="3aa9e-108">Bunlar:</span><span class="sxs-lookup"><span data-stu-id="3aa9e-108">These include:</span></span>

* <span data-ttu-id="3aa9e-109">[Sanal makine ölçek kümeleri](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) tooscale içeri veya dışarı etkinleştirmek otomatik ölçeklendirme ayarları.</span><span class="sxs-lookup"><span data-stu-id="3aa9e-109">[Virtual machine scale sets](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) with autoscale settings that enable you tooscale in or out.</span></span>
* <span data-ttu-id="3aa9e-110">[DevTest Labs](../devtest-lab/devtest-lab-overview.md) hizmetini başlatma ve kapatma işlemleri planlama hello yerleşik özelliğine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="3aa9e-110">[DevTest Labs](../devtest-lab/devtest-lab-overview.md) service, which has hello built-in capability of scheduling startup and shutdown operations.</span></span>

<span data-ttu-id="3aa9e-111">Ancak, bu yalnızca belirli senaryolar destek seçenekleri ve uygulanan tooinfrastructure olarak-hizmet (Iaas) VM'ler olamaz.</span><span class="sxs-lookup"><span data-stu-id="3aa9e-111">However, these options only support specific scenarios and cannot be applied tooinfrastructure-as-a-service (IaaS) VMs.</span></span>

<span data-ttu-id="3aa9e-112">Merhaba zamanlama etiketi uygulanan tooa kaynak grubu olduğunda, aynı zamanda uygulanan tooall sanal makineler bu kaynak grubu içinde olur.</span><span class="sxs-lookup"><span data-stu-id="3aa9e-112">When hello Schedule tag is applied tooa resource group, it's also applied tooall virtual machines inside that resource group.</span></span> <span data-ttu-id="3aa9e-113">Bir zamanlama da doğrudan uygulanan tooa VM ise, hello son zamanlama sırasının hello önceliklidir:</span><span class="sxs-lookup"><span data-stu-id="3aa9e-113">If a schedule is also directly applied tooa VM, hello last schedule takes precedence in hello following order:</span></span>

1. <span data-ttu-id="3aa9e-114">Zamanlama uygulanan tooa kaynak grubu</span><span class="sxs-lookup"><span data-stu-id="3aa9e-114">Schedule applied tooa resource group</span></span>
2. <span data-ttu-id="3aa9e-115">Uygulanan tooa kaynak grubu ve hello kaynak grubundaki sanal makine zamanlama</span><span class="sxs-lookup"><span data-stu-id="3aa9e-115">Schedule applied tooa resource group and virtual machine in hello resource group</span></span>
3. <span data-ttu-id="3aa9e-116">Uygulanan tooa sanal makine zamanlama</span><span class="sxs-lookup"><span data-stu-id="3aa9e-116">Schedule applied tooa virtual machine</span></span>

<span data-ttu-id="3aa9e-117">Bu senaryo, aslında bir JSON dizesinde belirtilen biçiminde alır ve hello değeri olarak ekler Schedule adlı bir etiket için.</span><span class="sxs-lookup"><span data-stu-id="3aa9e-117">This scenario essentially takes a JSON string with a specified format and adds it as hello value for a tag called Schedule.</span></span> <span data-ttu-id="3aa9e-118">Ardından bir runbook'un tüm kaynak grupları ve sanal makineleri listeler ve daha önce listelenen hello senaryolarını temel alarak her VM için hello zamanlamalar tanımlar.</span><span class="sxs-lookup"><span data-stu-id="3aa9e-118">Then a runbook lists all resource groups and virtual machines and identifies hello schedules for each VM based on hello scenarios listed earlier.</span></span> <span data-ttu-id="3aa9e-119">Sonraki bağlı zamanlamaları var. VM'ler hello döngüler ve ne yapılması değerlendirir.</span><span class="sxs-lookup"><span data-stu-id="3aa9e-119">Next it loops through hello VMs that have schedules attached and evaluates what action should be taken.</span></span> <span data-ttu-id="3aa9e-120">Örneğin, bunu VM'ler durduruldu, kapatmak veya göz ardı toobe gereken belirler.</span><span class="sxs-lookup"><span data-stu-id="3aa9e-120">For example, it determines which VMs need toobe stopped, shut down, or ignored.</span></span>

<span data-ttu-id="3aa9e-121">Bu runbook'lar hello kullanarak kimlik doğrulaması [Azure farklı çalıştır hesabı](automation-sec-configure-azure-runas-account.md).</span><span class="sxs-lookup"><span data-stu-id="3aa9e-121">These runbooks authenticate by using hello [Azure Run As account](automation-sec-configure-azure-runas-account.md).</span></span>

## <a name="download-hello-runbooks-for-hello-scenario"></a><span data-ttu-id="3aa9e-122">Merhaba runbook'lar hello senaryo için karşıdan yükle</span><span class="sxs-lookup"><span data-stu-id="3aa9e-122">Download hello runbooks for hello scenario</span></span>
<span data-ttu-id="3aa9e-123">Bu senaryo hello indirebilirsiniz dört PowerShell iş akışı runbook oluşur [TechNet Galerisi](https://gallery.technet.microsoft.com/Azure-Automation-Runbooks-84f0efc7) veya hello [GitHub](https://github.com/paulomarquesdacosta/azure-automation-scheduled-shutdown-and-startup) bu proje için depo.</span><span class="sxs-lookup"><span data-stu-id="3aa9e-123">This scenario consists of four PowerShell Workflow runbooks that you can download from hello [TechNet Gallery](https://gallery.technet.microsoft.com/Azure-Automation-Runbooks-84f0efc7) or hello [GitHub](https://github.com/paulomarquesdacosta/azure-automation-scheduled-shutdown-and-startup) repository for this project.</span></span>

| <span data-ttu-id="3aa9e-124">Runbook</span><span class="sxs-lookup"><span data-stu-id="3aa9e-124">Runbook</span></span> | <span data-ttu-id="3aa9e-125">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3aa9e-125">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3aa9e-126">Test-ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="3aa9e-126">Test-ResourceSchedule</span></span> |<span data-ttu-id="3aa9e-127">Her sanal makine zamanlamayı denetler ve kapanması veya başlatılması hello zamanlamaya bağlı olarak gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="3aa9e-127">Checks each virtual machine schedule and performs shutdown or startup depending on hello schedule.</span></span> |
| <span data-ttu-id="3aa9e-128">Ekleme ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="3aa9e-128">Add-ResourceSchedule</span></span> |<span data-ttu-id="3aa9e-129">VM veya kaynak Hello zamanlama etiketi tooa grubu ekler.</span><span class="sxs-lookup"><span data-stu-id="3aa9e-129">Adds hello Schedule tag tooa VM or resource group.</span></span> |
| <span data-ttu-id="3aa9e-130">Güncelleştirme ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="3aa9e-130">Update-ResourceSchedule</span></span> |<span data-ttu-id="3aa9e-131">Yeni bir tane ile değiştirerek Hello varolan bir zamanlamayı etiketi değiştirir.</span><span class="sxs-lookup"><span data-stu-id="3aa9e-131">Modifies hello existing Schedule tag by replacing it with a new one.</span></span> |
| <span data-ttu-id="3aa9e-132">Remove-ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="3aa9e-132">Remove-ResourceSchedule</span></span> |<span data-ttu-id="3aa9e-133">Merhaba zamanlama etiketi bir VM veya kaynak grubundan kaldırır.</span><span class="sxs-lookup"><span data-stu-id="3aa9e-133">Removes hello Schedule tag from a VM or resource group.</span></span> |

## <a name="install-and-configure-this-scenario"></a><span data-ttu-id="3aa9e-134">Bu senaryoyu yükleme ve yapılandırma</span><span class="sxs-lookup"><span data-stu-id="3aa9e-134">Install and configure this scenario</span></span>
### <a name="install-and-publish-hello-runbooks"></a><span data-ttu-id="3aa9e-135">Yükleme ve yayımlama hello runbook'ları</span><span class="sxs-lookup"><span data-stu-id="3aa9e-135">Install and publish hello runbooks</span></span>
<span data-ttu-id="3aa9e-136">Merhaba runbook'ları indirdikten sonra bunları hello yordamı kullanarak içeri aktarabilirsiniz [oluşturma veya bir Azure Otomasyonu runbook'u içeri aktarma](automation-creating-importing-runbook.md#importing-a-runbook-from-a-file-into-azure-automation).</span><span class="sxs-lookup"><span data-stu-id="3aa9e-136">After downloading hello runbooks, you can import them by using hello procedure in [Creating or importing a runbook in Azure Automation](automation-creating-importing-runbook.md#importing-a-runbook-from-a-file-into-azure-automation).</span></span>  <span data-ttu-id="3aa9e-137">Otomasyon hesabınızda başarıyla alındıktan sonra her runbook yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="3aa9e-137">Publish each runbook after it has been successfully imported into your Automation account.</span></span>

### <a name="add-a-schedule-toohello-test-resourceschedule-runbook"></a><span data-ttu-id="3aa9e-138">Zamanlama toohello Test ResourceSchedule runbook Ekle</span><span class="sxs-lookup"><span data-stu-id="3aa9e-138">Add a schedule toohello Test-ResourceSchedule runbook</span></span>
<span data-ttu-id="3aa9e-139">Merhaba Test ResourceSchedule runbook için bu adımları tooenable hello zamanlama izleyin.</span><span class="sxs-lookup"><span data-stu-id="3aa9e-139">Follow these steps tooenable hello schedule for hello Test-ResourceSchedule runbook.</span></span> <span data-ttu-id="3aa9e-140">Kapalı hangi sanal makinelerin başlatılmalıdır doğrular hello runbook veya olarak sol budur.</span><span class="sxs-lookup"><span data-stu-id="3aa9e-140">This is hello runbook that verifies which virtual machines should be started, shut down, or left as is.</span></span>

1. <span data-ttu-id="3aa9e-141">Hello Azure portal, Automation hesabınızı açın ve hello ardından **Runbook'lar** döşeme.</span><span class="sxs-lookup"><span data-stu-id="3aa9e-141">From hello Azure portal, open your Automation account, and then click hello **Runbooks** tile.</span></span>
2. <span data-ttu-id="3aa9e-142">Merhaba üzerinde **Test ResourceSchedule** dikey penceresinde hello tıklatın **zamanlamaları** döşeme.</span><span class="sxs-lookup"><span data-stu-id="3aa9e-142">On hello **Test-ResourceSchedule** blade, click hello **Schedules** tile.</span></span>
3. <span data-ttu-id="3aa9e-143">Merhaba üzerinde **zamanlamaları** dikey penceresinde tıklatın **bir zamanlama Ekle**.</span><span class="sxs-lookup"><span data-stu-id="3aa9e-143">On hello **Schedules** blade, click **Add a schedule**.</span></span>
4. <span data-ttu-id="3aa9e-144">Merhaba üzerinde **zamanlamaları** dikey penceresinde, select **bir zamanlama tooyour runbook bağlantı**.</span><span class="sxs-lookup"><span data-stu-id="3aa9e-144">On hello **Schedules** blade, select **Link a schedule tooyour runbook**.</span></span> <span data-ttu-id="3aa9e-145">Ardından **yeni bir zamanlama oluşturmak**.</span><span class="sxs-lookup"><span data-stu-id="3aa9e-145">Then select **Create a new schedule**.</span></span>
5. <span data-ttu-id="3aa9e-146">Merhaba üzerinde **yeni zamanlama** dikey penceresinde hello ad yazın, bu zamanlamanın örneğin: *HourlyExecution*.</span><span class="sxs-lookup"><span data-stu-id="3aa9e-146">On hello **New schedule** blade, type in hello name of this schedule, for example: *HourlyExecution*.</span></span>
6. <span data-ttu-id="3aa9e-147">Merhaba zamanlama için **Başlat**, hello başlangıç zaman tooan saat artışı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="3aa9e-147">For hello schedule **Start**, set hello start time tooan hour increment.</span></span>
7. <span data-ttu-id="3aa9e-148">Seçin **yineleme**ve ardından **her aralığı yinelenmesini**seçin **1 saat**.</span><span class="sxs-lookup"><span data-stu-id="3aa9e-148">Select **Recurrence**, and then for **Recur every interval**, select **1 hour**.</span></span>
8. <span data-ttu-id="3aa9e-149">Doğrulayın **sona erme süresini ayarlamanıza** çok ayarlanır**Hayır**ve ardından **oluşturma** toosave yeni zamanlamanızı.</span><span class="sxs-lookup"><span data-stu-id="3aa9e-149">Verify that **Set expiration** is set too**No**, and then click **Create** toosave your new schedule.</span></span>
9. <span data-ttu-id="3aa9e-150">Merhaba üzerinde **zamanlama Runbook** seçenekleri dikey penceresinde, select **parametreler ve çalıştırma ayarları**.</span><span class="sxs-lookup"><span data-stu-id="3aa9e-150">On hello **Schedule Runbook** options blade, select **Parameters and run settings**.</span></span> <span data-ttu-id="3aa9e-151">Merhaba Test ResourceSchedule içinde **parametreleri** dikey penceresinde hello aboneliğinizi hello adını girin **varlığıyla SubscriptionName** alan.</span><span class="sxs-lookup"><span data-stu-id="3aa9e-151">In hello Test-ResourceSchedule **Parameters** blade, enter hello name of your subscription in hello **SubscriptionName** field.</span></span>  <span data-ttu-id="3aa9e-152">Merhaba runbook için gerekli olan tek bir parametre hello budur.</span><span class="sxs-lookup"><span data-stu-id="3aa9e-152">This is hello only parameter that's required for hello runbook.</span></span>  <span data-ttu-id="3aa9e-153">İşiniz bittiğinde tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="3aa9e-153">When you're finished, click **OK**.</span></span>

<span data-ttu-id="3aa9e-154">tamamlandığında hello runbook zamanlaması hello aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="3aa9e-154">hello runbook schedule should look like hello following when it's completed:</span></span>

![Yapılandırılmış Test ResourceSchedule runbook](./media/automation-scenario-start-stop-vm-wjson-tags/automation-schedule-config.png)<br>

## <a name="format-hello-json-string"></a><span data-ttu-id="3aa9e-156">Biçim hello JSON dizesi</span><span class="sxs-lookup"><span data-stu-id="3aa9e-156">Format hello JSON string</span></span>
<span data-ttu-id="3aa9e-157">Bu çözüm, JSON ile belirtilen bir biçim dizesi ve bir etiket için başlangıç değeri olarak ekler alır zamanlama temel olarak çağrılır.</span><span class="sxs-lookup"><span data-stu-id="3aa9e-157">This solution basically takes a JSON string with a specified format and adds it as hello value for a tag called Schedule.</span></span> <span data-ttu-id="3aa9e-158">Ardından bir runbook'un tüm kaynak grupları ve sanal makineleri listeler ve her bir sanal makine için hello zamanlamaları tanımlar.</span><span class="sxs-lookup"><span data-stu-id="3aa9e-158">Then a runbook lists all resource groups and virtual machines and identifies hello schedules for each virtual machine.</span></span>

<span data-ttu-id="3aa9e-159">Merhaba runbook hello sanal makineleri bağlı zamanlamaları var. döngüler ve hangi eylemleri alınıp alınmayacağını denetler.</span><span class="sxs-lookup"><span data-stu-id="3aa9e-159">hello runbook loops over hello virtual machines that have schedules attached and checks what actions should be taken.</span></span> <span data-ttu-id="3aa9e-160">Merhaba, hello çözümleri nasıl biçimlendirilmiş bir örnek verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="3aa9e-160">hello following is an example of how hello solutions should be formatted:</span></span>

```json
{
    "TzId": "Eastern Standard Time",
    "0": {
        "S": "11",
        "E": "17"
    },
    "1": {
        "S": "9",
        "E": "19"
    },
    "2": {
        "S": "9",
        "E": "19"
    },
}
```

<span data-ttu-id="3aa9e-161">Bu yapı hakkında ayrıntılı bazı bilgiler aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="3aa9e-161">Here is some detailed information about this structure:</span></span>

1. <span data-ttu-id="3aa9e-162">Merhaba bu JSON yapısındaki en iyi duruma getirilmiş toowork Azure içindeki bir tek etiket değeri hello 256 karakterlik yazıtiplerinden biçimidir.</span><span class="sxs-lookup"><span data-stu-id="3aa9e-162">hello format of this JSON structure is optimized toowork around hello 256-character limitation of a single tag value in Azure.</span></span>
2. <span data-ttu-id="3aa9e-163">*TZID* hello hello sanal makinenin saat dilimini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="3aa9e-163">*TzId* represents hello time zone of hello virtual machine.</span></span> <span data-ttu-id="3aa9e-164">Bu kodu bir PowerShell oturumu--içinde hello Timezoneınfo .NET sınıfını kullanarak elde edilebilir**[System.TimeZoneInfo]:: GetSystemTimeZones()**.</span><span class="sxs-lookup"><span data-stu-id="3aa9e-164">This ID can be obtained by using hello TimeZoneInfo .NET class in a PowerShell session--**[System.TimeZoneInfo]::GetSystemTimeZones()**.</span></span>

   ![PowerShell'de GetSystemTimeZones](./media/automation-scenario-start-stop-vm-wjson-tags/automation-get-timzone-powershell.png)

   * <span data-ttu-id="3aa9e-166">Haftanın günü sıfır toosix sayısal bir değeri ile temsil edilir.</span><span class="sxs-lookup"><span data-stu-id="3aa9e-166">Weekdays are represented with a numeric value of zero toosix.</span></span> <span data-ttu-id="3aa9e-167">Merhaba değeri sıfır Pazar eşittir.</span><span class="sxs-lookup"><span data-stu-id="3aa9e-167">hello value zero equals Sunday.</span></span>
   * <span data-ttu-id="3aa9e-168">Merhaba başlangıç saati hello ile temsil edilen **S** özniteliği ve değerini 24 saat biçiminde değil.</span><span class="sxs-lookup"><span data-stu-id="3aa9e-168">hello start time is represented with hello **S** attribute, and its value is in a 24-hour format.</span></span>
   * <span data-ttu-id="3aa9e-169">Merhaba son veya kapatma süresi hello ile temsil edilen **E** özniteliği ve değerini 24 saat biçiminde değil.</span><span class="sxs-lookup"><span data-stu-id="3aa9e-169">hello end or shutdown time is represented with hello **E** attribute, and its value is in a 24-hour format.</span></span>

     <span data-ttu-id="3aa9e-170">Merhaba, **S** ve **E** her özniteliklere sahip bir değeri sıfır (0), hello sanal makine sol değerlendirme hello aynı anda mevcut durumda.</span><span class="sxs-lookup"><span data-stu-id="3aa9e-170">If hello **S** and **E** attributes each have a value of zero (0), hello virtual machine will be left in its present state at hello time of evaluation.</span></span>
3. <span data-ttu-id="3aa9e-171">Merhaba haftanın belirli bir gün için tooskip değerlendirme istiyorsanız, o hello haftanın günü için bir bölüm eklemeyin.</span><span class="sxs-lookup"><span data-stu-id="3aa9e-171">If you want tooskip evaluation for a specific day of hello week, don’t add a section for that day of hello week.</span></span> <span data-ttu-id="3aa9e-172">Merhaba örneği, yalnızca Pazartesi aşağıdaki değerlendirilir ve hello hello haftanın diğer günleri göz ardı edilir:</span><span class="sxs-lookup"><span data-stu-id="3aa9e-172">In hello following example, only Monday is evaluated, and hello other days of hello week are ignored:</span></span>

    ```json
    {
        "TzId": "Eastern Standard Time",
        "1": {
            "S": "11",
            "E": "17"
        }
    }
    ```

## <a name="tag-resource-groups-or-vms"></a><span data-ttu-id="3aa9e-173">Etiket kaynak grupları veya VM'ler</span><span class="sxs-lookup"><span data-stu-id="3aa9e-173">Tag resource groups or VMs</span></span>
<span data-ttu-id="3aa9e-174">tooshut VM'ler aşağı tootag ihtiyacınız hello VM'ler veya hello kaynak grupları, bunlar bulunduğu.</span><span class="sxs-lookup"><span data-stu-id="3aa9e-174">tooshut down VMs, you need tootag either hello VMs or hello resource groups in which they're located.</span></span> <span data-ttu-id="3aa9e-175">Bir zamanlama etiketi sahip olmayan sanal makineleri değerlendirilmez.</span><span class="sxs-lookup"><span data-stu-id="3aa9e-175">Virtual machines that don't have a Schedule tag are not evaluated.</span></span> <span data-ttu-id="3aa9e-176">Bu nedenle, bunlar çalışmaya veya kapat.</span><span class="sxs-lookup"><span data-stu-id="3aa9e-176">Therefore, they aren't started or shut down.</span></span>

<span data-ttu-id="3aa9e-177">Bu çözüm ile iki şekilde tootag kaynak grupları veya VM'ler vardır.</span><span class="sxs-lookup"><span data-stu-id="3aa9e-177">There are two ways tootag resource groups or VMs with this solution.</span></span> <span data-ttu-id="3aa9e-178">Bu doğrudan hello portalından yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3aa9e-178">You can do it directly from hello portal.</span></span> <span data-ttu-id="3aa9e-179">Veya hello Ekle ResourceSchedule, güncelleştirme ResourceSchedule ve Kaldır-ResourceSchedule runbook'ları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3aa9e-179">Or you can use hello Add-ResourceSchedule, Update-ResourceSchedule, and Remove-ResourceSchedule runbooks.</span></span>

### <a name="tag-through-hello-portal"></a><span data-ttu-id="3aa9e-180">Merhaba Portalı aracılığıyla etiketi</span><span class="sxs-lookup"><span data-stu-id="3aa9e-180">Tag through hello portal</span></span>
<span data-ttu-id="3aa9e-181">Bu adımları tootag bir sanal makine veya kaynak grubu hello portalında izleyin:</span><span class="sxs-lookup"><span data-stu-id="3aa9e-181">Follow these steps tootag a virtual machine or resource group in hello portal:</span></span>

1. <span data-ttu-id="3aa9e-182">Merhaba JSON dizesi düzleştirmek ve boşluk olmayan doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="3aa9e-182">Flatten hello JSON string and verify that there aren't any spaces.</span></span>  <span data-ttu-id="3aa9e-183">JSON dizenizi aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="3aa9e-183">Your JSON string should look like this:</span></span>

    ```json
    {"TzId":"Eastern Standard Time","0":{"S":"11","E":"17"},"1":{"S":"9","E":"19"},"2": {"S":"9","E":"19"},"3":{"S":"9","E":"19"},"4":{"S":"9","E":"19"},"5":{"S":"9","E":"19"},"6":{"S":"11","E":"17"}}
    ```

2. <span data-ttu-id="3aa9e-184">Select hello **etiketi** simgesi VM veya kaynak grubu tooapply Bu zamanlama.</span><span class="sxs-lookup"><span data-stu-id="3aa9e-184">Select hello **Tag** icon for a VM or resource group tooapply this schedule.</span></span>

   ![VM etiketi seçeneği](./media/automation-scenario-start-stop-vm-wjson-tags/automation-vm-tag-option.png)

3. <span data-ttu-id="3aa9e-186">Etiketler, bir anahtar/değer çifti aşağıdaki tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="3aa9e-186">Tags are defined following a key/value pair.</span></span> <span data-ttu-id="3aa9e-187">Tür **zamanlama** hello içinde **anahtar** alan ve hello JSON dizesi hello yapıştırın **değeri** alan.</span><span class="sxs-lookup"><span data-stu-id="3aa9e-187">Type **Schedule** in hello **Key** field, and then paste hello JSON string into hello **Value** field.</span></span> <span data-ttu-id="3aa9e-188">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3aa9e-188">Click **Save**.</span></span> <span data-ttu-id="3aa9e-189">Yeni etiket şimdi kaynağınız için etiketler hello listesinde gösterilmelidir.</span><span class="sxs-lookup"><span data-stu-id="3aa9e-189">Your new tag should now appear in hello list of tags for your resource.</span></span>

   ![VM zamanlama etiketi](./media/automation-scenario-start-stop-vm-wjson-tags/automation-vm-schedule-tag.png)

### <a name="tag-from-powershell"></a><span data-ttu-id="3aa9e-191">PowerShell etiketinden</span><span class="sxs-lookup"><span data-stu-id="3aa9e-191">Tag from PowerShell</span></span>
<span data-ttu-id="3aa9e-192">Tüm içeri aktarılan runbook'ları nasıl tooexecute hello PowerShell doğrudan runbook'lardan açıklar hello betik hello başında Yardım bilgilerini içerir.</span><span class="sxs-lookup"><span data-stu-id="3aa9e-192">All imported runbooks contain help information at hello beginning of hello script that describes how tooexecute hello runbooks directly from PowerShell.</span></span> <span data-ttu-id="3aa9e-193">Merhaba Ekle ScheduleResource ve güncelleştirme ScheduleResource runbook'lar Powershell'den çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3aa9e-193">You can call hello Add-ScheduleResource and Update-ScheduleResource runbooks from PowerShell.</span></span> <span data-ttu-id="3aa9e-194">Bunun için bir VM veya kaynak grubundaki hello portal dışında toocreate veya güncelleştirme hello zamanlama etiketi etkinleştirmeniz gerekli parametreleri geçirerek.</span><span class="sxs-lookup"><span data-stu-id="3aa9e-194">You do this by passing required parameters that enable you toocreate or update hello Schedule tag on a VM or resource group outside of hello portal.</span></span>

<span data-ttu-id="3aa9e-195">toocreate, ekleme ve PowerShell aracılığıyla etiketleri silme, ilk çok gerek[için Azure PowerShell ortamınızı ayarlayın](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3aa9e-195">toocreate, add, and delete tags through PowerShell, you first need too[set up your PowerShell environment for Azure](/powershell/azure/overview).</span></span> <span data-ttu-id="3aa9e-196">Merhaba kurulumu tamamladıktan sonra aşağıdaki adımları hello ile devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3aa9e-196">After you complete hello setup, you can proceed with hello following steps.</span></span>

### <a name="create-a-schedule-tag-with-powershell"></a><span data-ttu-id="3aa9e-197">PowerShell ile bir zamanlama etiket oluşturma</span><span class="sxs-lookup"><span data-stu-id="3aa9e-197">Create a schedule tag with PowerShell</span></span>
1. <span data-ttu-id="3aa9e-198">Bir PowerShell oturumu açın.</span><span class="sxs-lookup"><span data-stu-id="3aa9e-198">Open a PowerShell session.</span></span> <span data-ttu-id="3aa9e-199">Ardından örnek tooauthenticate farklı çalıştır hesabı ve toospecify bir abonelik aşağıdaki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="3aa9e-199">Then use hello following example tooauthenticate with your Run As account and toospecify a subscription:</span></span>

    ```powershell
    $Conn = Get-AutomationConnection -Name AzureRunAsConnection
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

2. <span data-ttu-id="3aa9e-200">Bir zamanlama karma tablo tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="3aa9e-200">Define a schedule hash table.</span></span> <span data-ttu-id="3aa9e-201">Nasıl oluşturulmalıdır örneği şöyledir:</span><span class="sxs-lookup"><span data-stu-id="3aa9e-201">Here is an example of how it should be constructed:</span></span>

    ```powershell
    $schedule= @{ "TzId"="Eastern Standard Time"; "0"= @{"S"="11";"E"="17"};"1"= @{"S"="9";"E"="19"};"2"= @{"S"="9";"E"="19"};"3"= @{"S"="9";"E"="19"};"4"= @{"S"="9";"E"="19"};"5"= @{"S"="9";"E"="19"};"6"= @{"S"="11";"E"="17"}}
    ```

3. <span data-ttu-id="3aa9e-202">Merhaba runbook tarafından gerekli hello parametrelerini tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="3aa9e-202">Define hello parameters that are required by hello runbook.</span></span> <span data-ttu-id="3aa9e-203">Aşağıdaki örneğine hello biz VM hedeflediğiniz:</span><span class="sxs-lookup"><span data-stu-id="3aa9e-203">In hello following example, we are targeting a VM:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"; "VmName"="VM01";"Schedule"=$schedule}
    ```

    <span data-ttu-id="3aa9e-204">Bir kaynak grubu etiketleme hello kaldırmanız *VMName* hello $params karma parametresinden tablo şu şekilde:</span><span class="sxs-lookup"><span data-stu-id="3aa9e-204">If you’re tagging a resource group, remove hello *VMName* parameter from hello $params hash table as follows:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"; "Schedule"=$schedule}
    ```

4. <span data-ttu-id="3aa9e-205">Merhaba Ekle ResourceSchedule runbook parametreleri toocreate hello zamanlama etiketi aşağıdaki hello ile çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="3aa9e-205">Run hello Add-ResourceSchedule runbook with hello following parameters toocreate hello Schedule tag:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Add-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

5. <span data-ttu-id="3aa9e-206">bir kaynak grubu ya da sanal makineyi etiketi tooupdate yürütme hello **güncelleştirme ResourceSchedule** şu parametreler hello runbook'la:</span><span class="sxs-lookup"><span data-stu-id="3aa9e-206">tooupdate a resource group or virtual machine tag, execute hello **Update-ResourceSchedule** runbook with hello following parameters:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Update-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

### <a name="remove-a-schedule-tag-with-powershell"></a><span data-ttu-id="3aa9e-207">PowerShell ile bir zamanlama Etiketi Kaldır</span><span class="sxs-lookup"><span data-stu-id="3aa9e-207">Remove a schedule tag with PowerShell</span></span>
1. <span data-ttu-id="3aa9e-208">Bir PowerShell oturumu açın ve aşağıdaki farklı çalıştır hesabı ve tooselect tooauthenticate hello çalıştırın ve bir abonelik belirtin:</span><span class="sxs-lookup"><span data-stu-id="3aa9e-208">Open a PowerShell session and run hello following tooauthenticate with your Run As account and tooselect and specify a subscription:</span></span>

    ```powershell
    Conn = Get-AutomationConnection -Name AzureRunAsConnection
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

2. <span data-ttu-id="3aa9e-209">Merhaba runbook tarafından gerekli hello parametrelerini tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="3aa9e-209">Define hello parameters that are required by hello runbook.</span></span> <span data-ttu-id="3aa9e-210">Aşağıdaki örneğine hello biz VM hedeflediğiniz:</span><span class="sxs-lookup"><span data-stu-id="3aa9e-210">In hello following example, we are targeting a VM:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01";"VmName"="VM01"}
    ```

    <span data-ttu-id="3aa9e-211">Bir kaynak grubundan bir etiket kaldırıyorsanız hello kaldırmak *VMName* hello $params karma parametresinden tablo şu şekilde:</span><span class="sxs-lookup"><span data-stu-id="3aa9e-211">If you’re removing a tag from a resource group, remove hello *VMName* parameter from hello $params hash table as follows:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"}
    ```

3. <span data-ttu-id="3aa9e-212">Merhaba Kaldır ResourceSchedule runbook tooremove hello zamanlama etiketi yürütün:</span><span class="sxs-lookup"><span data-stu-id="3aa9e-212">Execute hello Remove-ResourceSchedule runbook tooremove hello Schedule tag:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Remove-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

4. <span data-ttu-id="3aa9e-213">tooupdate bir kaynak grubu ya da sanal makineyi etiketi ile şu parametreler hello hello Kaldır ResourceSchedule runbook yürütün:</span><span class="sxs-lookup"><span data-stu-id="3aa9e-213">tooupdate a resource group or virtual machine tag, execute hello Remove-ResourceSchedule runbook with hello following parameters:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Remove-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

> [!NOTE]
> <span data-ttu-id="3aa9e-214">Biz proaktif olarak bu runbook'ları (ve hello sanal makine durumları), sanal makineleriniz yükleniyor tooverify kapatma izlemeniz önerilir ve buna uygun olarak başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="3aa9e-214">We recommend that you proactively monitor these runbooks (and hello virtual machine states) tooverify that your virtual machines are being shut down and started accordingly.</span></span>
>

<span data-ttu-id="3aa9e-215">Azure portal, select hello proje hello tooview hello ayrıntıları hello Test ResourceSchedule runbook'un **işleri** hello runbook parçasına.</span><span class="sxs-lookup"><span data-stu-id="3aa9e-215">tooview hello details of hello Test-ResourceSchedule runbook job in hello Azure portal, select hello **Jobs** tile of hello runbook.</span></span> <span data-ttu-id="3aa9e-216">Hello hello giriş parametreleri iş özeti görüntüler ve hello çıkış akışı, ayrıca hello işle ilgili toogeneral bilgileri ve özel durumlar bunlar ortaya çıktıysa.</span><span class="sxs-lookup"><span data-stu-id="3aa9e-216">hello job summary displays hello input parameters and hello output stream, in addition toogeneral information about hello job and any exceptions if they occurred.</span></span>

<span data-ttu-id="3aa9e-217">Merhaba **iş özeti** hello çıktı, uyarı ve hata akışları gelen iletileri içerir.</span><span class="sxs-lookup"><span data-stu-id="3aa9e-217">hello **Job Summary** includes messages from hello output, warning, and error streams.</span></span> <span data-ttu-id="3aa9e-218">Select hello **çıkış** tooview döşeme ayrıntılı hello runbook yürütme sonuçları.</span><span class="sxs-lookup"><span data-stu-id="3aa9e-218">Select hello **Output** tile tooview detailed results from hello runbook execution.</span></span>

![Test ResourceSchedule çıkış](./media/automation-scenario-start-stop-vm-wjson-tags/automation-job-output.png)

## <a name="next-steps"></a><span data-ttu-id="3aa9e-220">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3aa9e-220">Next steps</span></span>
* <span data-ttu-id="3aa9e-221">PowerShell iş akışı runbook'ları ile başlatılan tooget bkz [ilk PowerShell iş akışı runbook Uygulamam](automation-first-runbook-textual.md).</span><span class="sxs-lookup"><span data-stu-id="3aa9e-221">tooget started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md).</span></span>
* <span data-ttu-id="3aa9e-222">runbook türleri ve avantajları ve sınırlamaları, hakkında daha fazla toolearn bkz [Azure Automation runbook türleri](automation-runbook-types.md).</span><span class="sxs-lookup"><span data-stu-id="3aa9e-222">toolearn more about runbook types, and their advantages and limitations, see [Azure Automation runbook types](automation-runbook-types.md).</span></span>
* <span data-ttu-id="3aa9e-223">PowerShell betik desteği özellikleri hakkında daha fazla bilgi için bkz: [Azure automation'da yerel PowerShell betik desteği](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/).</span><span class="sxs-lookup"><span data-stu-id="3aa9e-223">For more information about PowerShell script support features, see [Native PowerShell script support in Azure Automation](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/).</span></span>
* <span data-ttu-id="3aa9e-224">runbook günlüğü ve çıktı hakkında daha fazla toolearn bkz [Runbook çıkışı ve iletileri Azure Automation](automation-runbook-output-and-messages.md).</span><span class="sxs-lookup"><span data-stu-id="3aa9e-224">toolearn more about runbook logging and output, see [Runbook output and messages in Azure Automation](automation-runbook-output-and-messages.md).</span></span>
* <span data-ttu-id="3aa9e-225">bir Azure farklı çalıştır hesabı ve tooauthenticate runbook'larınızın, kullanarak nasıl görürüm hakkında daha fazla toolearn [runbook'ları Azure farklı çalıştır hesabıyla kimlik doğrulaması](automation-sec-configure-azure-runas-account.md).</span><span class="sxs-lookup"><span data-stu-id="3aa9e-225">toolearn more about an Azure Run As account and how tooauthenticate your runbooks by using it, see [Authenticate runbooks with Azure Run As account](automation-sec-configure-azure-runas-account.md).</span></span>
