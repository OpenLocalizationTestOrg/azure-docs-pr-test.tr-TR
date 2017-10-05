---
title: "Azure VM durumunu zamanlamak için JSON biçimli etiketler kullanın | Microsoft Docs"
description: "Bu makalede, JSON dizeler etiketlerini VM başlatma ve kapatma zamanlama otomatikleştirmek için nasıl kullanılacağı gösterilmektedir."
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
ms.openlocfilehash: f8d9563318c3afe299cebb7c889874392f114f84
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-automation-scenario-using-json-formatted-tags-to-create-a-schedule-for-azure-vm-startup-and-shutdown"></a><span data-ttu-id="046c3-103">Azure otomasyonu senaryosu: Azure VM başlatma ve kapatma için bir zamanlama oluşturmak için JSON biçimli etiketleri kullanma</span><span class="sxs-lookup"><span data-stu-id="046c3-103">Azure Automation scenario: Using JSON-formatted tags to create a schedule for Azure VM startup and shutdown</span></span>
<span data-ttu-id="046c3-104">Müşteriler genellikle başlatma ve kapatma abonelik maliyetlerini azaltmak veya işletme ve teknik gereksinimleri desteği yardımcı olmak için sanal makinelerin zamanlamak ister.</span><span class="sxs-lookup"><span data-stu-id="046c3-104">Customers often want to schedule the startup and shutdown of virtual machines to help reduce subscription costs or support business and technical requirements.</span></span>

<span data-ttu-id="046c3-105">Aşağıdaki senaryoda, bir kaynak grubu düzeyinde veya azure'da sanal makine düzeyinde Schedule adlı bir etiket kullanarak otomatik başlatma ve kapatma, VM'lerin ayarlamak sağlar.</span><span class="sxs-lookup"><span data-stu-id="046c3-105">The following scenario enables you to set up automated startup and shutdown of your VMs by using a tag called Schedule at a resource group level or virtual machine level in Azure.</span></span> <span data-ttu-id="046c3-106">Bu zamanlamayı Pazar Cumartesi için bir başlangıç saati ve kapatma saati ile yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="046c3-106">This schedule can be configured from Sunday to Saturday with a startup time and shutdown time.</span></span>

<span data-ttu-id="046c3-107">Biz, bazı Giden kutusu seçeneğiniz vardır.</span><span class="sxs-lookup"><span data-stu-id="046c3-107">We do have some out-of-the-box options.</span></span> <span data-ttu-id="046c3-108">Bunlar:</span><span class="sxs-lookup"><span data-stu-id="046c3-108">These include:</span></span>

* <span data-ttu-id="046c3-109">[Sanal makine ölçek kümeleri](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) etkinleştirmeniz veya ölçeklendirmek otomatik ölçeklendirme ayarları.</span><span class="sxs-lookup"><span data-stu-id="046c3-109">[Virtual machine scale sets](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) with autoscale settings that enable you to scale in or out.</span></span>
* <span data-ttu-id="046c3-110">[DevTest Labs](../devtest-lab/devtest-lab-overview.md) hizmetini başlatma ve kapatma işlemleri planlama yerleşik özelliğine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="046c3-110">[DevTest Labs](../devtest-lab/devtest-lab-overview.md) service, which has the built-in capability of scheduling startup and shutdown operations.</span></span>

<span data-ttu-id="046c3-111">Ancak, bu yalnızca belirli senaryolar destek seçenekleri ve altyapı olarak-hizmet (Iaas) VM'ler için uygulanamaz.</span><span class="sxs-lookup"><span data-stu-id="046c3-111">However, these options only support specific scenarios and cannot be applied to infrastructure-as-a-service (IaaS) VMs.</span></span>

<span data-ttu-id="046c3-112">Bir kaynak grubuna zamanlama etiket uygulandığında, bu kaynak grubu içindeki tüm sanal makinelere de uygulanır.</span><span class="sxs-lookup"><span data-stu-id="046c3-112">When the Schedule tag is applied to a resource group, it's also applied to all virtual machines inside that resource group.</span></span> <span data-ttu-id="046c3-113">Bir zamanlama da doğrudan bir VM'ye uyguladıysanız, son zamanlama önceliği aşağıdaki sırayla alır:</span><span class="sxs-lookup"><span data-stu-id="046c3-113">If a schedule is also directly applied to a VM, the last schedule takes precedence in the following order:</span></span>

1. <span data-ttu-id="046c3-114">Bir kaynak grubuna uygulanan zamanlama</span><span class="sxs-lookup"><span data-stu-id="046c3-114">Schedule applied to a resource group</span></span>
2. <span data-ttu-id="046c3-115">Bir kaynak grubu ve kaynak grubundaki sanal makine uygulanan zamanlama</span><span class="sxs-lookup"><span data-stu-id="046c3-115">Schedule applied to a resource group and virtual machine in the resource group</span></span>
3. <span data-ttu-id="046c3-116">Bir sanal makineye uygulanan zamanlama</span><span class="sxs-lookup"><span data-stu-id="046c3-116">Schedule applied to a virtual machine</span></span>

<span data-ttu-id="046c3-117">Bu senaryo, aslında bir JSON dizesinde belirtilen biçiminde alır ve değeri olarak ekler Schedule adlı bir etiket için.</span><span class="sxs-lookup"><span data-stu-id="046c3-117">This scenario essentially takes a JSON string with a specified format and adds it as the value for a tag called Schedule.</span></span> <span data-ttu-id="046c3-118">Ardından bir runbook'un tüm kaynak grupları ve sanal makineleri listeler ve daha önce listelenen senaryolarını temel alarak her VM için zamanlamaları tanımlar.</span><span class="sxs-lookup"><span data-stu-id="046c3-118">Then a runbook lists all resource groups and virtual machines and identifies the schedules for each VM based on the scenarios listed earlier.</span></span> <span data-ttu-id="046c3-119">Sonraki zamanlamaları bağlı olan sanal makineleri döngüler ve ne yapılması değerlendirir.</span><span class="sxs-lookup"><span data-stu-id="046c3-119">Next it loops through the VMs that have schedules attached and evaluates what action should be taken.</span></span> <span data-ttu-id="046c3-120">Örneğin, bu sanal makineleri durduruldu, kapatmak veya göz ardı gereken belirler.</span><span class="sxs-lookup"><span data-stu-id="046c3-120">For example, it determines which VMs need to be stopped, shut down, or ignored.</span></span>

<span data-ttu-id="046c3-121">Bu runbook'ları kullanarak kimlik doğrulaması [Azure farklı çalıştır hesabı](automation-sec-configure-azure-runas-account.md).</span><span class="sxs-lookup"><span data-stu-id="046c3-121">These runbooks authenticate by using the [Azure Run As account](automation-sec-configure-azure-runas-account.md).</span></span>

## <a name="download-the-runbooks-for-the-scenario"></a><span data-ttu-id="046c3-122">Senaryo için runbook'ları indirme</span><span class="sxs-lookup"><span data-stu-id="046c3-122">Download the runbooks for the scenario</span></span>
<span data-ttu-id="046c3-123">Bu senaryo indirebileceğiniz dört PowerShell iş akışı runbook oluşur [TechNet Galerisi](https://gallery.technet.microsoft.com/Azure-Automation-Runbooks-84f0efc7) veya [GitHub](https://github.com/paulomarquesdacosta/azure-automation-scheduled-shutdown-and-startup) bu proje için depo.</span><span class="sxs-lookup"><span data-stu-id="046c3-123">This scenario consists of four PowerShell Workflow runbooks that you can download from the [TechNet Gallery](https://gallery.technet.microsoft.com/Azure-Automation-Runbooks-84f0efc7) or the [GitHub](https://github.com/paulomarquesdacosta/azure-automation-scheduled-shutdown-and-startup) repository for this project.</span></span>

| <span data-ttu-id="046c3-124">Runbook</span><span class="sxs-lookup"><span data-stu-id="046c3-124">Runbook</span></span> | <span data-ttu-id="046c3-125">Açıklama</span><span class="sxs-lookup"><span data-stu-id="046c3-125">Description</span></span> |
| --- | --- |
| <span data-ttu-id="046c3-126">Test-ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="046c3-126">Test-ResourceSchedule</span></span> |<span data-ttu-id="046c3-127">Her sanal makine zamanlamayı denetler ve kapanması veya başlatılması zamanlamaya bağlı olarak gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="046c3-127">Checks each virtual machine schedule and performs shutdown or startup depending on the schedule.</span></span> |
| <span data-ttu-id="046c3-128">Ekleme ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="046c3-128">Add-ResourceSchedule</span></span> |<span data-ttu-id="046c3-129">Zamanlama etiketi bir VM veya kaynak grubuna ekler.</span><span class="sxs-lookup"><span data-stu-id="046c3-129">Adds the Schedule tag to a VM or resource group.</span></span> |
| <span data-ttu-id="046c3-130">Güncelleştirme ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="046c3-130">Update-ResourceSchedule</span></span> |<span data-ttu-id="046c3-131">Varolan bir zamanlamayı etiketi, yeni bir tane ile değiştirerek değiştirir.</span><span class="sxs-lookup"><span data-stu-id="046c3-131">Modifies the existing Schedule tag by replacing it with a new one.</span></span> |
| <span data-ttu-id="046c3-132">Remove-ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="046c3-132">Remove-ResourceSchedule</span></span> |<span data-ttu-id="046c3-133">Zamanlama etiketi bir VM veya kaynak grubundan kaldırır.</span><span class="sxs-lookup"><span data-stu-id="046c3-133">Removes the Schedule tag from a VM or resource group.</span></span> |

## <a name="install-and-configure-this-scenario"></a><span data-ttu-id="046c3-134">Bu senaryoyu yükleme ve yapılandırma</span><span class="sxs-lookup"><span data-stu-id="046c3-134">Install and configure this scenario</span></span>
### <a name="install-and-publish-the-runbooks"></a><span data-ttu-id="046c3-135">Runbook yükleme ve yayımlama</span><span class="sxs-lookup"><span data-stu-id="046c3-135">Install and publish the runbooks</span></span>
<span data-ttu-id="046c3-136">Runbook'ları indirdikten sonra bunları yordamı kullanarak içeri aktarabilirsiniz [oluşturma veya bir Azure Otomasyonu runbook'u içeri aktarma](automation-creating-importing-runbook.md#importing-a-runbook-from-a-file-into-azure-automation).</span><span class="sxs-lookup"><span data-stu-id="046c3-136">After downloading the runbooks, you can import them by using the procedure in [Creating or importing a runbook in Azure Automation](automation-creating-importing-runbook.md#importing-a-runbook-from-a-file-into-azure-automation).</span></span>  <span data-ttu-id="046c3-137">Otomasyon hesabınızda başarıyla alındıktan sonra her runbook yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="046c3-137">Publish each runbook after it has been successfully imported into your Automation account.</span></span>

### <a name="add-a-schedule-to-the-test-resourceschedule-runbook"></a><span data-ttu-id="046c3-138">Test-ResourceSchedule runbook'a bir zamanlama Ekle</span><span class="sxs-lookup"><span data-stu-id="046c3-138">Add a schedule to the Test-ResourceSchedule runbook</span></span>
<span data-ttu-id="046c3-139">Test-ResourceSchedule runbook zamanlamasını etkinleştirmek için aşağıdaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="046c3-139">Follow these steps to enable the schedule for the Test-ResourceSchedule runbook.</span></span> <span data-ttu-id="046c3-140">Hangi sanal makinelerin başlatıldı, kapatmak veya olarak sol doğrular runbook budur.</span><span class="sxs-lookup"><span data-stu-id="046c3-140">This is the runbook that verifies which virtual machines should be started, shut down, or left as is.</span></span>

1. <span data-ttu-id="046c3-141">Azure portalından Automation hesabınızı açın ve ardından **Runbook'lar** döşeme.</span><span class="sxs-lookup"><span data-stu-id="046c3-141">From the Azure portal, open your Automation account, and then click the **Runbooks** tile.</span></span>
2. <span data-ttu-id="046c3-142">Üzerinde **Test ResourceSchedule** dikey penceresinde tıklatın **zamanlamaları** döşeme.</span><span class="sxs-lookup"><span data-stu-id="046c3-142">On the **Test-ResourceSchedule** blade, click the **Schedules** tile.</span></span>
3. <span data-ttu-id="046c3-143">Üzerinde **zamanlamaları** dikey penceresinde tıklatın **bir zamanlama Ekle**.</span><span class="sxs-lookup"><span data-stu-id="046c3-143">On the **Schedules** blade, click **Add a schedule**.</span></span>
4. <span data-ttu-id="046c3-144">Üzerinde **zamanlamaları** dikey penceresinde, select **runbook'a bir zamanlama Bağla**.</span><span class="sxs-lookup"><span data-stu-id="046c3-144">On the **Schedules** blade, select **Link a schedule to your runbook**.</span></span> <span data-ttu-id="046c3-145">Ardından **yeni bir zamanlama oluşturmak**.</span><span class="sxs-lookup"><span data-stu-id="046c3-145">Then select **Create a new schedule**.</span></span>
5. <span data-ttu-id="046c3-146">Üzerinde **yeni zamanlama** dikey penceresinde, bu zamanlamayı adını yazın örneğin: *HourlyExecution*.</span><span class="sxs-lookup"><span data-stu-id="046c3-146">On the **New schedule** blade, type in the name of this schedule, for example: *HourlyExecution*.</span></span>
6. <span data-ttu-id="046c3-147">Zamanlama için **Başlat**, başlangıç saati bir saat artışı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="046c3-147">For the schedule **Start**, set the start time to an hour increment.</span></span>
7. <span data-ttu-id="046c3-148">Seçin **yineleme**ve ardından **her aralığı yinelenmesini**seçin **1 saat**.</span><span class="sxs-lookup"><span data-stu-id="046c3-148">Select **Recurrence**, and then for **Recur every interval**, select **1 hour**.</span></span>
8. <span data-ttu-id="046c3-149">Doğrulayın **sona erme süresini ayarlamanıza** ayarlanır **Hayır**ve ardından **oluşturma** yeni zamanlamanızı kaydetmek için.</span><span class="sxs-lookup"><span data-stu-id="046c3-149">Verify that **Set expiration** is set to **No**, and then click **Create** to save your new schedule.</span></span>
9. <span data-ttu-id="046c3-150">Üzerinde **zamanlama Runbook** seçenekleri dikey penceresinde, select **parametreler ve çalıştırma ayarları**.</span><span class="sxs-lookup"><span data-stu-id="046c3-150">On the **Schedule Runbook** options blade, select **Parameters and run settings**.</span></span> <span data-ttu-id="046c3-151">Test ResourceSchedule içinde **parametreleri** dikey penceresinde, aboneliğinizde adını girin **varlığıyla SubscriptionName** alan.</span><span class="sxs-lookup"><span data-stu-id="046c3-151">In the Test-ResourceSchedule **Parameters** blade, enter the name of your subscription in the **SubscriptionName** field.</span></span>  <span data-ttu-id="046c3-152">Bu runbook için gerekli olan tek bir parametredir.</span><span class="sxs-lookup"><span data-stu-id="046c3-152">This is the only parameter that's required for the runbook.</span></span>  <span data-ttu-id="046c3-153">İşiniz bittiğinde tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="046c3-153">When you're finished, click **OK**.</span></span>

<span data-ttu-id="046c3-154">Tamamlandığında runbook zamanlaması aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="046c3-154">The runbook schedule should look like the following when it's completed:</span></span>

![Yapılandırılmış Test ResourceSchedule runbook](./media/automation-scenario-start-stop-vm-wjson-tags/automation-schedule-config.png)<br>

## <a name="format-the-json-string"></a><span data-ttu-id="046c3-156">Biçim JSON dizesi</span><span class="sxs-lookup"><span data-stu-id="046c3-156">Format the JSON string</span></span>
<span data-ttu-id="046c3-157">Bu çözüm, JSON ile belirtilen bir biçim dizesi ve bir etiket için değer olarak ekler alır zamanlama temel olarak çağrılır.</span><span class="sxs-lookup"><span data-stu-id="046c3-157">This solution basically takes a JSON string with a specified format and adds it as the value for a tag called Schedule.</span></span> <span data-ttu-id="046c3-158">Ardından bir runbook'un tüm kaynak grupları ve sanal makineleri listeler ve her bir sanal makine için zamanlamalar tanımlar.</span><span class="sxs-lookup"><span data-stu-id="046c3-158">Then a runbook lists all resource groups and virtual machines and identifies the schedules for each virtual machine.</span></span>

<span data-ttu-id="046c3-159">Runbook bağlı zamanlamaları sahip sanal makineler üzerinde döngüler ve hangi eylemleri alınıp alınmayacağını denetler.</span><span class="sxs-lookup"><span data-stu-id="046c3-159">The runbook loops over the virtual machines that have schedules attached and checks what actions should be taken.</span></span> <span data-ttu-id="046c3-160">Çözümler nasıl biçimlendirilmiş bir örnek verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="046c3-160">The following is an example of how the solutions should be formatted:</span></span>

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

<span data-ttu-id="046c3-161">Bu yapı hakkında ayrıntılı bazı bilgiler aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="046c3-161">Here is some detailed information about this structure:</span></span>

1. <span data-ttu-id="046c3-162">Bu JSON yapısındaki biçimi Azure içindeki bir tek etiket değeri 256 karakterlik sınırlamaya geçici olarak çözmek için optimize edilmiştir.</span><span class="sxs-lookup"><span data-stu-id="046c3-162">The format of this JSON structure is optimized to work around the 256-character limitation of a single tag value in Azure.</span></span>
2. <span data-ttu-id="046c3-163">*TZID* sanal makinenin saat dilimini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="046c3-163">*TzId* represents the time zone of the virtual machine.</span></span> <span data-ttu-id="046c3-164">Bu kodu bir PowerShell oturumu--içinde Timezoneınfo .NET sınıfını kullanarak elde edilebilir**[System.TimeZoneInfo]:: GetSystemTimeZones()**.</span><span class="sxs-lookup"><span data-stu-id="046c3-164">This ID can be obtained by using the TimeZoneInfo .NET class in a PowerShell session--**[System.TimeZoneInfo]::GetSystemTimeZones()**.</span></span>

   ![PowerShell'de GetSystemTimeZones](./media/automation-scenario-start-stop-vm-wjson-tags/automation-get-timzone-powershell.png)

   * <span data-ttu-id="046c3-166">Haftanın günü altı sıfır sayısal değeri ile temsil edilir.</span><span class="sxs-lookup"><span data-stu-id="046c3-166">Weekdays are represented with a numeric value of zero to six.</span></span> <span data-ttu-id="046c3-167">Sıfır değeri Pazar eşittir.</span><span class="sxs-lookup"><span data-stu-id="046c3-167">The value zero equals Sunday.</span></span>
   * <span data-ttu-id="046c3-168">Başlangıç saati ile temsil edilen **S** özniteliği ve değerini 24 saat biçiminde değil.</span><span class="sxs-lookup"><span data-stu-id="046c3-168">The start time is represented with the **S** attribute, and its value is in a 24-hour format.</span></span>
   * <span data-ttu-id="046c3-169">Son veya kapatma süresi ile temsil edilen **E** özniteliği ve değerini 24 saat biçiminde değil.</span><span class="sxs-lookup"><span data-stu-id="046c3-169">The end or shutdown time is represented with the **E** attribute, and its value is in a 24-hour format.</span></span>

     <span data-ttu-id="046c3-170">Varsa **S** ve **E** her özniteliklere sahip bir değeri sıfır (0), sanal makine değerlendirme aynı anda mevcut durumda kalır.</span><span class="sxs-lookup"><span data-stu-id="046c3-170">If the **S** and **E** attributes each have a value of zero (0), the virtual machine will be left in its present state at the time of evaluation.</span></span>
3. <span data-ttu-id="046c3-171">Haftanın belirli bir gün için değerlendirme atlamak istiyorsanız, bir bölümü, haftanın günü için eklemeyin.</span><span class="sxs-lookup"><span data-stu-id="046c3-171">If you want to skip evaluation for a specific day of the week, don’t add a section for that day of the week.</span></span> <span data-ttu-id="046c3-172">Aşağıdaki örnekte, yalnızca Pazartesi değerlendirilir ve haftanın günlerini göz ardı edilir:</span><span class="sxs-lookup"><span data-stu-id="046c3-172">In the following example, only Monday is evaluated, and the other days of the week are ignored:</span></span>

    ```json
    {
        "TzId": "Eastern Standard Time",
        "1": {
            "S": "11",
            "E": "17"
        }
    }
    ```

## <a name="tag-resource-groups-or-vms"></a><span data-ttu-id="046c3-173">Etiket kaynak grupları veya VM'ler</span><span class="sxs-lookup"><span data-stu-id="046c3-173">Tag resource groups or VMs</span></span>
<span data-ttu-id="046c3-174">Sanal makineleri kapatmaya VM'ler veya içinde bulunduğu oldukları kaynak grupları etiket gerekir.</span><span class="sxs-lookup"><span data-stu-id="046c3-174">To shut down VMs, you need to tag either the VMs or the resource groups in which they're located.</span></span> <span data-ttu-id="046c3-175">Bir zamanlama etiketi sahip olmayan sanal makineleri değerlendirilmez.</span><span class="sxs-lookup"><span data-stu-id="046c3-175">Virtual machines that don't have a Schedule tag are not evaluated.</span></span> <span data-ttu-id="046c3-176">Bu nedenle, bunlar çalışmaya veya kapat.</span><span class="sxs-lookup"><span data-stu-id="046c3-176">Therefore, they aren't started or shut down.</span></span>

<span data-ttu-id="046c3-177">Bu çözümle etiketi kaynak grupları ya da sanal makineleri iki yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="046c3-177">There are two ways to tag resource groups or VMs with this solution.</span></span> <span data-ttu-id="046c3-178">Bu doğrudan portalından yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="046c3-178">You can do it directly from the portal.</span></span> <span data-ttu-id="046c3-179">Veya Ekle ResourceSchedule, güncelleştirme ResourceSchedule ve Kaldır-ResourceSchedule runbook'ları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="046c3-179">Or you can use the Add-ResourceSchedule, Update-ResourceSchedule, and Remove-ResourceSchedule runbooks.</span></span>

### <a name="tag-through-the-portal"></a><span data-ttu-id="046c3-180">Portalı aracılığıyla etiketi</span><span class="sxs-lookup"><span data-stu-id="046c3-180">Tag through the portal</span></span>
<span data-ttu-id="046c3-181">Bir sanal makine ya da kaynak grubu portalda etiketlemek için şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="046c3-181">Follow these steps to tag a virtual machine or resource group in the portal:</span></span>

1. <span data-ttu-id="046c3-182">JSON dizesindeki düzleştirmek ve boşluk olmayan doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="046c3-182">Flatten the JSON string and verify that there aren't any spaces.</span></span>  <span data-ttu-id="046c3-183">JSON dizenizi aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="046c3-183">Your JSON string should look like this:</span></span>

    ```json
    {"TzId":"Eastern Standard Time","0":{"S":"11","E":"17"},"1":{"S":"9","E":"19"},"2": {"S":"9","E":"19"},"3":{"S":"9","E":"19"},"4":{"S":"9","E":"19"},"5":{"S":"9","E":"19"},"6":{"S":"11","E":"17"}}
    ```

2. <span data-ttu-id="046c3-184">Seçin **etiketi** Bu zamanlamanın uygulamak bir VM veya kaynak grubu simgesi.</span><span class="sxs-lookup"><span data-stu-id="046c3-184">Select the **Tag** icon for a VM or resource group to apply this schedule.</span></span>

   ![VM etiketi seçeneği](./media/automation-scenario-start-stop-vm-wjson-tags/automation-vm-tag-option.png)

3. <span data-ttu-id="046c3-186">Etiketler, bir anahtar/değer çifti aşağıdaki tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="046c3-186">Tags are defined following a key/value pair.</span></span> <span data-ttu-id="046c3-187">Tür **zamanlama** içinde **anahtar** alan ve JSON dizeye yapıştırın **değeri** alan.</span><span class="sxs-lookup"><span data-stu-id="046c3-187">Type **Schedule** in the **Key** field, and then paste the JSON string into the **Value** field.</span></span> <span data-ttu-id="046c3-188">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="046c3-188">Click **Save**.</span></span> <span data-ttu-id="046c3-189">Yeni etiket şimdi kaynağınız için etiketler listesinde gösterilmelidir.</span><span class="sxs-lookup"><span data-stu-id="046c3-189">Your new tag should now appear in the list of tags for your resource.</span></span>

   ![VM zamanlama etiketi](./media/automation-scenario-start-stop-vm-wjson-tags/automation-vm-schedule-tag.png)

### <a name="tag-from-powershell"></a><span data-ttu-id="046c3-191">PowerShell etiketinden</span><span class="sxs-lookup"><span data-stu-id="046c3-191">Tag from PowerShell</span></span>
<span data-ttu-id="046c3-192">Tüm içeri aktarılan runbook'lar runbook'ları doğrudan Powershell'den yürütmek açıklar komut dosyasının başında Yardım bilgilerini içerir.</span><span class="sxs-lookup"><span data-stu-id="046c3-192">All imported runbooks contain help information at the beginning of the script that describes how to execute the runbooks directly from PowerShell.</span></span> <span data-ttu-id="046c3-193">Add-ScheduleResource ve güncelleştirme ScheduleResource runbook'lar Powershell'den çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="046c3-193">You can call the Add-ScheduleResource and Update-ScheduleResource runbooks from PowerShell.</span></span> <span data-ttu-id="046c3-194">Bunun için bir VM veya kaynak grubunu portal dışında zamanlama etiketinde güncelle sağlayan gerekli parametreleri geçirerek.</span><span class="sxs-lookup"><span data-stu-id="046c3-194">You do this by passing required parameters that enable you to create or update the Schedule tag on a VM or resource group outside of the portal.</span></span>

<span data-ttu-id="046c3-195">Oluşturmak için Ekle ve PowerShell, ilk gerek aracılığıyla etiketleri silmek [için Azure PowerShell ortamınızı ayarlayın](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="046c3-195">To create, add, and delete tags through PowerShell, you first need to [set up your PowerShell environment for Azure](/powershell/azure/overview).</span></span> <span data-ttu-id="046c3-196">Kurulum tamamlandıktan sonra aşağıdaki adımlarla devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="046c3-196">After you complete the setup, you can proceed with the following steps.</span></span>

### <a name="create-a-schedule-tag-with-powershell"></a><span data-ttu-id="046c3-197">PowerShell ile bir zamanlama etiket oluşturma</span><span class="sxs-lookup"><span data-stu-id="046c3-197">Create a schedule tag with PowerShell</span></span>
1. <span data-ttu-id="046c3-198">Bir PowerShell oturumu açın.</span><span class="sxs-lookup"><span data-stu-id="046c3-198">Open a PowerShell session.</span></span> <span data-ttu-id="046c3-199">Ardından, farklı çalıştır hesabıyla kimlik doğrulaması ve abonelik belirtmek için aşağıdaki örneği kullanın:</span><span class="sxs-lookup"><span data-stu-id="046c3-199">Then use the following example to authenticate with your Run As account and to specify a subscription:</span></span>

    ```powershell
    $Conn = Get-AutomationConnection -Name AzureRunAsConnection
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

2. <span data-ttu-id="046c3-200">Bir zamanlama karma tablo tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="046c3-200">Define a schedule hash table.</span></span> <span data-ttu-id="046c3-201">Nasıl oluşturulmalıdır örneği şöyledir:</span><span class="sxs-lookup"><span data-stu-id="046c3-201">Here is an example of how it should be constructed:</span></span>

    ```powershell
    $schedule= @{ "TzId"="Eastern Standard Time"; "0"= @{"S"="11";"E"="17"};"1"= @{"S"="9";"E"="19"};"2"= @{"S"="9";"E"="19"};"3"= @{"S"="9";"E"="19"};"4"= @{"S"="9";"E"="19"};"5"= @{"S"="9";"E"="19"};"6"= @{"S"="11";"E"="17"}}
    ```

3. <span data-ttu-id="046c3-202">Runbook tarafından gerekli parametrelerini tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="046c3-202">Define the parameters that are required by the runbook.</span></span> <span data-ttu-id="046c3-203">Aşağıdaki örnekte, biz VM hedeflediğiniz:</span><span class="sxs-lookup"><span data-stu-id="046c3-203">In the following example, we are targeting a VM:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"; "VmName"="VM01";"Schedule"=$schedule}
    ```

    <span data-ttu-id="046c3-204">Bir kaynak grubu etiketleme kaldırmanız *VMName* $params karma parametresinden tablo şu şekilde:</span><span class="sxs-lookup"><span data-stu-id="046c3-204">If you’re tagging a resource group, remove the *VMName* parameter from the $params hash table as follows:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"; "Schedule"=$schedule}
    ```

4. <span data-ttu-id="046c3-205">Add-ResourceSchedule runbook zamanlama etiket oluşturmak için aşağıdaki parametrelerle çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="046c3-205">Run the Add-ResourceSchedule runbook with the following parameters to create the Schedule tag:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Add-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

5. <span data-ttu-id="046c3-206">Bir kaynak grubunu veya sanal makine etiketi güncelleştirmek için yürütme **güncelleştirme ResourceSchedule** runbook aşağıdaki parametrelerle:</span><span class="sxs-lookup"><span data-stu-id="046c3-206">To update a resource group or virtual machine tag, execute the **Update-ResourceSchedule** runbook with the following parameters:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Update-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

### <a name="remove-a-schedule-tag-with-powershell"></a><span data-ttu-id="046c3-207">PowerShell ile bir zamanlama Etiketi Kaldır</span><span class="sxs-lookup"><span data-stu-id="046c3-207">Remove a schedule tag with PowerShell</span></span>
1. <span data-ttu-id="046c3-208">Bir PowerShell oturumu açın ve, farklı çalıştır hesabıyla kimlik doğrulaması seçin ve bir aboneliği belirtmek için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="046c3-208">Open a PowerShell session and run the following to authenticate with your Run As account and to select and specify a subscription:</span></span>

    ```powershell
    Conn = Get-AutomationConnection -Name AzureRunAsConnection
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

2. <span data-ttu-id="046c3-209">Runbook tarafından gerekli parametrelerini tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="046c3-209">Define the parameters that are required by the runbook.</span></span> <span data-ttu-id="046c3-210">Aşağıdaki örnekte, biz VM hedeflediğiniz:</span><span class="sxs-lookup"><span data-stu-id="046c3-210">In the following example, we are targeting a VM:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01";"VmName"="VM01"}
    ```

    <span data-ttu-id="046c3-211">Bir kaynak grubundan bir etiket kaldırıyorsanız kaldırmak *VMName* $params karma parametresinden tablo şu şekilde:</span><span class="sxs-lookup"><span data-stu-id="046c3-211">If you’re removing a tag from a resource group, remove the *VMName* parameter from the $params hash table as follows:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"}
    ```

3. <span data-ttu-id="046c3-212">Zamanlama etiketi kaldırmak için Remove-ResourceSchedule runbook yürütün:</span><span class="sxs-lookup"><span data-stu-id="046c3-212">Execute the Remove-ResourceSchedule runbook to remove the Schedule tag:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Remove-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

4. <span data-ttu-id="046c3-213">Bir kaynak grubunu veya sanal makine etiketi güncelleştirmek için aşağıdaki parametreleri Kaldır ResourceSchedule runbook'la yürütün:</span><span class="sxs-lookup"><span data-stu-id="046c3-213">To update a resource group or virtual machine tag, execute the Remove-ResourceSchedule runbook with the following parameters:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Remove-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

> [!NOTE]
> <span data-ttu-id="046c3-214">Biz, önceden sanal makinelerinizi kapatıldığını doğrulamak için bu runbook'lar (ve sanal makine durumları) aşağı izlemeniz önerilir ve buna uygun olarak başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="046c3-214">We recommend that you proactively monitor these runbooks (and the virtual machine states) to verify that your virtual machines are being shut down and started accordingly.</span></span>
>

<span data-ttu-id="046c3-215">Azure Portalı'nda Test ResourceSchedule runbook işi ayrıntılarını görüntülemek için seçin **işleri** döşeme runbook'un.</span><span class="sxs-lookup"><span data-stu-id="046c3-215">To view the details of the Test-ResourceSchedule runbook job in the Azure portal, select the **Jobs** tile of the runbook.</span></span> <span data-ttu-id="046c3-216">İş özetinde giriş parametreleri ve çıkış akışına ek olarak işe ilişkin genel bilgiler ve gerçekleşmişse özel durumlar gösterilir.</span><span class="sxs-lookup"><span data-stu-id="046c3-216">The job summary displays the input parameters and the output stream, in addition to general information about the job and any exceptions if they occurred.</span></span>

<span data-ttu-id="046c3-217">**İş Özeti** bölümünde çıkış, uyarı ve hata akışlarından iletiler bulunur.</span><span class="sxs-lookup"><span data-stu-id="046c3-217">The **Job Summary** includes messages from the output, warning, and error streams.</span></span> <span data-ttu-id="046c3-218">Runbook yürütmeyle ilgili ayrıntılı sonuçları görüntülemek için **Çıkış** kutucuğunu seçin.</span><span class="sxs-lookup"><span data-stu-id="046c3-218">Select the **Output** tile to view detailed results from the runbook execution.</span></span>

![Test ResourceSchedule çıkış](./media/automation-scenario-start-stop-vm-wjson-tags/automation-job-output.png)

## <a name="next-steps"></a><span data-ttu-id="046c3-220">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="046c3-220">Next steps</span></span>
* <span data-ttu-id="046c3-221">PowerShell iş akışı runbook'larını kullanmaya başlamak için bkz. [İlk PowerShell iş akışı runbook uygulamam](automation-first-runbook-textual.md).</span><span class="sxs-lookup"><span data-stu-id="046c3-221">To get started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md).</span></span>
* <span data-ttu-id="046c3-222">Runbook türleri ve avantajları ve sınırlamaları hakkında daha fazla bilgi için bkz: [Azure Automation runbook türleri](automation-runbook-types.md).</span><span class="sxs-lookup"><span data-stu-id="046c3-222">To learn more about runbook types, and their advantages and limitations, see [Azure Automation runbook types](automation-runbook-types.md).</span></span>
* <span data-ttu-id="046c3-223">PowerShell betik desteği özellikleri hakkında daha fazla bilgi için bkz: [Azure automation'da yerel PowerShell betik desteği](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/).</span><span class="sxs-lookup"><span data-stu-id="046c3-223">For more information about PowerShell script support features, see [Native PowerShell script support in Azure Automation](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/).</span></span>
* <span data-ttu-id="046c3-224">Runbook günlüğü ve çıktı hakkında daha fazla bilgi için bkz: [Runbook çıkışı ve iletileri Azure Automation](automation-runbook-output-and-messages.md).</span><span class="sxs-lookup"><span data-stu-id="046c3-224">To learn more about runbook logging and output, see [Runbook output and messages in Azure Automation](automation-runbook-output-and-messages.md).</span></span>
* <span data-ttu-id="046c3-225">Bir Azure farklı çalıştır hesabı ve bunu kullanarak runbook'larınızın kimliklerini nasıl hakkında daha fazla bilgi için bkz: [runbook'ları Azure farklı çalıştır hesabıyla kimlik doğrulaması](automation-sec-configure-azure-runas-account.md).</span><span class="sxs-lookup"><span data-stu-id="046c3-225">To learn more about an Azure Run As account and how to authenticate your runbooks by using it, see [Authenticate runbooks with Azure Run As account](automation-sec-configure-azure-runas-account.md).</span></span>
