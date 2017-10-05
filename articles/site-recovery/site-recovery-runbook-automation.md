---
title: "Azure Site Recovery kurtarma planlarında Azure Otomasyon çalışma kitabı ekleme | Microsoft Docs"
description: "Azure Site Recovery kurtarma planları Azure otomasyonu kullanarak genişletme nasıl yardımcı olabileceğini öğrenin. Azure Kurtarma sırasında karmaşık görevleri tamamlamak öğrenin."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: ecece14d-5f92-4596-bbaf-5204addb95c2
ms.service: site-recovery
ms.devlang: powershell
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 06/23/2017
ms.author: ruturajd@microsoft.com
ms.openlocfilehash: 064a6782970b950543f93c24800998c1f104c8df
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="add-azure-automation-runbooks-to-recovery-plans"></a><span data-ttu-id="7e17f-104">Azure Otomasyon çalışma kitabı kurtarma planlara Ekle</span><span class="sxs-lookup"><span data-stu-id="7e17f-104">Add Azure Automation runbooks to recovery plans</span></span>
<span data-ttu-id="7e17f-105">Bu makalede, Azure Site Recovery kurtarma planlarınızı genişletmek amacıyla Azure Automation ile nasıl tümleşik çalıştığını açıklar.</span><span class="sxs-lookup"><span data-stu-id="7e17f-105">In this article, we describe how Azure Site Recovery integrates with Azure Automation to help you extend your recovery plans.</span></span> <span data-ttu-id="7e17f-106">Kurtarma planları korunan sanal makineleri kurtarma Site Recovery ile düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7e17f-106">Recovery plans can orchestrate recovery of VMs that are protected with Site Recovery.</span></span> <span data-ttu-id="7e17f-107">Kurtarma planları hem ikincil bulutu için çoğaltma ve çoğaltma Azure için çalışır.</span><span class="sxs-lookup"><span data-stu-id="7e17f-107">Recovery plans work both for replication to a secondary cloud, and for replication to Azure.</span></span> <span data-ttu-id="7e17f-108">Kurtarma planları de yardımcı kurtarma yapmak **tutarlı bir şekilde doğru**, **yinelenebilir**, ve **otomatik**.</span><span class="sxs-lookup"><span data-stu-id="7e17f-108">Recovery plans also help make the recovery **consistently accurate**, **repeatable**, and **automated**.</span></span> <span data-ttu-id="7e17f-109">Vm'lerinizi Azure üzerinden başarısız olursa, Azure Automation tümleştirme kurtarma planlarınızı genişletir.</span><span class="sxs-lookup"><span data-stu-id="7e17f-109">If you fail over your VMs to Azure, integration with Azure Automation extends your recovery plans.</span></span> <span data-ttu-id="7e17f-110">Runbook'ları, ama güçlü bir otomatikleştirme görevleri teklif çalıştırmak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7e17f-110">You can use it to execute runbooks, which offer powerful automation tasks.</span></span>

<span data-ttu-id="7e17f-111">Azure Otomasyonu yeniyseniz, yapabilecekleriniz [kaydolun](https://azure.microsoft.com/services/automation/) ve [örnek komut dosyası yükleme](https://azure.microsoft.com/documentation/scripts/).</span><span class="sxs-lookup"><span data-stu-id="7e17f-111">If you are new to Azure Automation, you can [sign up](https://azure.microsoft.com/services/automation/) and [download sample scripts](https://azure.microsoft.com/documentation/scripts/).</span></span> <span data-ttu-id="7e17f-112">Daha fazla bilgi için ve Azure Kurtarma kullanarak düzenlemek öğrenmek için [kurtarma planlarına](https://azure.microsoft.com/blog/?p=166264), bkz: [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="7e17f-112">For more information, and to learn how to orchestrate recovery to Azure by using [recovery plans](https://azure.microsoft.com/blog/?p=166264), see [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/).</span></span>

<span data-ttu-id="7e17f-113">Bu makalede, nasıl Azure Otomasyon çalışma kitabı kurtarma planlarınızı tümleştirebilir açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="7e17f-113">In this article, we describe how you can integrate Azure Automation runbooks into your recovery plans.</span></span> <span data-ttu-id="7e17f-114">Daha önce el ile müdahale gerekli temel görevleri otomatikleştirmek için örnekler kullanırız.</span><span class="sxs-lookup"><span data-stu-id="7e17f-114">We use examples to automate basic tasks that previously required manual intervention.</span></span> <span data-ttu-id="7e17f-115">Biz de çok adımlı kurtarma için bir tek tıklamalı kurtarma eylemi dönüştürmek açıklar.</span><span class="sxs-lookup"><span data-stu-id="7e17f-115">We also describe how to convert a multi-step recovery to a single-click recovery action.</span></span>

## <a name="customize-the-recovery-plan"></a><span data-ttu-id="7e17f-116">Kurtarma planı özelleştirme</span><span class="sxs-lookup"><span data-stu-id="7e17f-116">Customize the recovery plan</span></span>
1. <span data-ttu-id="7e17f-117">Git **Site Recovery** kurtarma planı kaynak dikey.</span><span class="sxs-lookup"><span data-stu-id="7e17f-117">Go to the **Site Recovery** recovery plan resource blade.</span></span> <span data-ttu-id="7e17f-118">Bu örnekte, iki VM, kurtarma için eklenene kurtarma planına sahip.</span><span class="sxs-lookup"><span data-stu-id="7e17f-118">For this example, the recovery plan has two VMs added to it, for recovery.</span></span> <span data-ttu-id="7e17f-119">Bir runbook eklemeye başlamak için tıklatın **Özelleştir** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="7e17f-119">To begin adding a runbook, click the **Customize** tab.</span></span>

    ![Özelleştirme düğmesini tıklatın](media/site-recovery-runbook-automation-new/essentials-rp.png)


2. <span data-ttu-id="7e17f-121">Sağ **Grup 1: Başlangıç**ve ardından **post eylem eklemek**.</span><span class="sxs-lookup"><span data-stu-id="7e17f-121">Right-click **Group 1: Start**, and then select **Add post action**.</span></span>

    ![Sağ Grup 1: Başlatın ve sonrası eylemi ekleyin](media/site-recovery-runbook-automation-new/customize-rp.png)

3. <span data-ttu-id="7e17f-123">Tıklatın **bir komut dosyası seçin**.</span><span class="sxs-lookup"><span data-stu-id="7e17f-123">Click **Choose a script**.</span></span>

4. <span data-ttu-id="7e17f-124">Üzerinde **güncelleştirme eylem** dikey penceresinde, adı betik **Hello World**.</span><span class="sxs-lookup"><span data-stu-id="7e17f-124">On the **Update action** blade, name the script **Hello World**.</span></span>

    ![Güncelleştirme eylem dikey penceresi](media/site-recovery-runbook-automation-new/update-rp.png)

5. <span data-ttu-id="7e17f-126">Bir Otomasyon hesabı adı girin.</span><span class="sxs-lookup"><span data-stu-id="7e17f-126">Enter an Automation account name.</span></span>
    >[!NOTE]
    > <span data-ttu-id="7e17f-127">Otomasyon hesabının Azure herhangi bir bölgede olabilir.</span><span class="sxs-lookup"><span data-stu-id="7e17f-127">The Automation account can be in any Azure region.</span></span> <span data-ttu-id="7e17f-128">Otomasyon hesabının Azure Site kurtarma kasası ile aynı abonelikte olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="7e17f-128">The Automation account must be in the same subscription as the Azure Site Recovery vault.</span></span>

6. <span data-ttu-id="7e17f-129">Otomasyon hesabınızda bir runbook seçin.</span><span class="sxs-lookup"><span data-stu-id="7e17f-129">In your Automation account, select a runbook.</span></span> <span data-ttu-id="7e17f-130">Bu runbook ilk grup kurtarma işleminden sonra kurtarma planı yürütülmesi sırasında çalışan komut dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="7e17f-130">This runbook is the script that runs during the execution of the recovery plan, after the recovery of the first group.</span></span>

7. <span data-ttu-id="7e17f-131">Komut dosyasını kaydetmek için tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="7e17f-131">To save the script, click **OK**.</span></span> <span data-ttu-id="7e17f-132">Komut dosyası eklenen **Grup 1: sonrası adımları**.</span><span class="sxs-lookup"><span data-stu-id="7e17f-132">The script is added to **Group 1: Post-steps**.</span></span>

    ![Eylem sonrası Grup 1:Start](media/site-recovery-runbook-automation-new/addedscript-rp.PNG)


## <a name="considerations-for-adding-a-script"></a><span data-ttu-id="7e17f-134">Bir komut dosyası eklemek için dikkat edilecek noktalar</span><span class="sxs-lookup"><span data-stu-id="7e17f-134">Considerations for adding a script</span></span>

* <span data-ttu-id="7e17f-135">Seçenekler için **bir adım silme** veya **betik güncelleştirme**, komut dosyasını sağ tıklatın.</span><span class="sxs-lookup"><span data-stu-id="7e17f-135">For options to **delete a step** or **update the script**, right-click the script.</span></span>
* <span data-ttu-id="7e17f-136">Bir komut dosyası Azure üzerinde yük devretme sırasında bir şirket içi makineden Azure'a çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7e17f-136">A script can run on Azure during failover from an on-premises machine to Azure.</span></span> <span data-ttu-id="7e17f-137">Ayrıca Azure üzerinde bir birincil site komut dosyası kapatma önce olarak azure'dan şirket içi makineye sırasında çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7e17f-137">It also can run on Azure as a primary-site script before shutdown, during failback from Azure to an on-premises machine.</span></span>
* <span data-ttu-id="7e17f-138">Bir komut dosyası çalıştığında, bir kurtarma planı içeriği yerleştirir.</span><span class="sxs-lookup"><span data-stu-id="7e17f-138">When a script runs, it injects a recovery plan context.</span></span> <span data-ttu-id="7e17f-139">Aşağıdaki örnek, bir bağlam değişkeni gösterir:</span><span class="sxs-lookup"><span data-stu-id="7e17f-139">The following example shows a context variable:</span></span>

    ```
            {"RecoveryPlanName":"hrweb-recovery",

            "FailoverType":"Test",

            "FailoverDirection":"PrimaryToSecondary",

            "GroupId":"1",

            "VmMap":{"7a1069c6-c1d6-49c5-8c5d-33bfce8dd183":

                    { "SubscriptionId":"7a1111111-c1d6-49c5-8c5d-111ce8dd183",

                    "ResourceGroupName":"ContosoRG",

                    "CloudServiceName":"pod02hrweb-Chicago-test",

                    "RoleName":"Fabrikam-Hrweb-frontend-test",

                    "RecoveryPointId":"TimeStamp"}

                    }

            }
    ```

    <span data-ttu-id="7e17f-140">Aşağıdaki tabloda, ad ve açıklama bağlamında her değişkenin listeler.</span><span class="sxs-lookup"><span data-stu-id="7e17f-140">The following table lists the name and description of each variable in the context.</span></span>

    | <span data-ttu-id="7e17f-141">**Değişken adı**</span><span class="sxs-lookup"><span data-stu-id="7e17f-141">**Variable name**</span></span> | <span data-ttu-id="7e17f-142">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="7e17f-142">**Description**</span></span> |
    | --- | --- |
    | <span data-ttu-id="7e17f-143">RecoveryPlanName</span><span class="sxs-lookup"><span data-stu-id="7e17f-143">RecoveryPlanName</span></span> |<span data-ttu-id="7e17f-144">Çalıştırılan planın adı.</span><span class="sxs-lookup"><span data-stu-id="7e17f-144">The name of the plan being run.</span></span> <span data-ttu-id="7e17f-145">Bu değişken, kurtarma planı adına göre farklı eylemleri yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="7e17f-145">This variable helps you take different actions based on the recovery plan name.</span></span> <span data-ttu-id="7e17f-146">Ayrıca komut dosyasını yeniden kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7e17f-146">You also can reuse the script.</span></span> |
    | <span data-ttu-id="7e17f-147">FailoverType</span><span class="sxs-lookup"><span data-stu-id="7e17f-147">FailoverType</span></span> |<span data-ttu-id="7e17f-148">Yük devretme testi olup olmadığını belirtir, planlı veya plansız.</span><span class="sxs-lookup"><span data-stu-id="7e17f-148">Specifies whether the failover is a test, planned, or unplanned.</span></span> |
    | <span data-ttu-id="7e17f-149">FailoverDirection</span><span class="sxs-lookup"><span data-stu-id="7e17f-149">FailoverDirection</span></span> |<span data-ttu-id="7e17f-150">Kurtarma için birincil veya ikincil bir siteye olup olmadığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="7e17f-150">Specifies whether recovery is to a primary or secondary site.</span></span> |
    | <span data-ttu-id="7e17f-151">GroupID</span><span class="sxs-lookup"><span data-stu-id="7e17f-151">GroupID</span></span> |<span data-ttu-id="7e17f-152">Plan çalıştırırken Grup numarası kurtarma planında tanımlar.</span><span class="sxs-lookup"><span data-stu-id="7e17f-152">Identifies the group number in the recovery plan when the plan is running.</span></span> |
    | <span data-ttu-id="7e17f-153">VmMap</span><span class="sxs-lookup"><span data-stu-id="7e17f-153">VmMap</span></span> |<span data-ttu-id="7e17f-154">Gruptaki tüm sanal makineleri bir dizi.</span><span class="sxs-lookup"><span data-stu-id="7e17f-154">An array of all VMs in the group.</span></span> |
    | <span data-ttu-id="7e17f-155">VMMap anahtarı</span><span class="sxs-lookup"><span data-stu-id="7e17f-155">VMMap key</span></span> |<span data-ttu-id="7e17f-156">Her VM için benzersiz anahtar (GUID).</span><span class="sxs-lookup"><span data-stu-id="7e17f-156">A unique key (GUID) for each VM.</span></span> <span data-ttu-id="7e17f-157">Bu VM, Azure Virtual Machine Manager (VMM) Kimliğini uygunsa aynıdır.</span><span class="sxs-lookup"><span data-stu-id="7e17f-157">It's the same as the Azure Virtual Machine Manager (VMM) ID of the VM, where applicable.</span></span> |
    | <span data-ttu-id="7e17f-158">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="7e17f-158">SubscriptionId</span></span> |<span data-ttu-id="7e17f-159">VM oluşturulduğu Azure abonelik kimliği.</span><span class="sxs-lookup"><span data-stu-id="7e17f-159">The Azure subscription ID in which the VM was created.</span></span> |
    | <span data-ttu-id="7e17f-160">Rol adı</span><span class="sxs-lookup"><span data-stu-id="7e17f-160">RoleName</span></span> |<span data-ttu-id="7e17f-161">Kurtarılacak Azure VM adı.</span><span class="sxs-lookup"><span data-stu-id="7e17f-161">The name of the Azure VM that's being recovered.</span></span> |
    | <span data-ttu-id="7e17f-162">CloudServiceName</span><span class="sxs-lookup"><span data-stu-id="7e17f-162">CloudServiceName</span></span> |<span data-ttu-id="7e17f-163">VM oluşturulduğu Azure bulut hizmeti adı.</span><span class="sxs-lookup"><span data-stu-id="7e17f-163">The Azure cloud service name under which the VM was created.</span></span> |
    | <span data-ttu-id="7e17f-164">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="7e17f-164">ResourceGroupName</span></span>|<span data-ttu-id="7e17f-165">VM oluşturulduğu Azure kaynak grubu adı.</span><span class="sxs-lookup"><span data-stu-id="7e17f-165">The Azure resource group name under which the VM was created.</span></span> |
    | <span data-ttu-id="7e17f-166">Recoverypointıd</span><span class="sxs-lookup"><span data-stu-id="7e17f-166">RecoveryPointId</span></span>|<span data-ttu-id="7e17f-167">VM zaman kurtarılan için zaman damgası.</span><span class="sxs-lookup"><span data-stu-id="7e17f-167">The timestamp for when the VM is recovered.</span></span> |

* <span data-ttu-id="7e17f-168">Otomasyon hesabı aşağıdaki modüller sahip olduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="7e17f-168">Ensure that the Automation account has the following modules:</span></span>
    * <span data-ttu-id="7e17f-169">AzureRM.profile</span><span class="sxs-lookup"><span data-stu-id="7e17f-169">AzureRM.profile</span></span>
    * <span data-ttu-id="7e17f-170">AzureRM.Resources</span><span class="sxs-lookup"><span data-stu-id="7e17f-170">AzureRM.Resources</span></span>
    * <span data-ttu-id="7e17f-171">AzureRM.Automation</span><span class="sxs-lookup"><span data-stu-id="7e17f-171">AzureRM.Automation</span></span>
    * <span data-ttu-id="7e17f-172">AzureRM.Network</span><span class="sxs-lookup"><span data-stu-id="7e17f-172">AzureRM.Network</span></span>
    * <span data-ttu-id="7e17f-173">AzureRM.Compute</span><span class="sxs-lookup"><span data-stu-id="7e17f-173">AzureRM.Compute</span></span>

<span data-ttu-id="7e17f-174">Tüm modüllerin uyumlu sürümlerini olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7e17f-174">All modules should be of compatible versions.</span></span> <span data-ttu-id="7e17f-175">Tüm modüllerin uyumlu olduğundan emin olmak için kolay bir yol tüm modülleri en son sürümlerini kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="7e17f-175">An easy way to ensure that all modules are compatible is to use the latest versions of all the modules.</span></span>

### <a name="access-all-vms-of-the-vmmap-in-a-loop"></a><span data-ttu-id="7e17f-176">Döngü VMMap tüm Vm'leri erişim</span><span class="sxs-lookup"><span data-stu-id="7e17f-176">Access all VMs of the VMMap in a loop</span></span>
<span data-ttu-id="7e17f-177">Microsoft VMMap tüm VM'ler arasında döngü için aşağıdaki kodu kullanın:</span><span class="sxs-lookup"><span data-stu-id="7e17f-177">Use the following code to loop across all VMs of the Microsoft VMMap:</span></span>

```
$VMinfo = $RecoveryPlanContext.VmMap | Get-Member | Where-Object MemberType -EQ NoteProperty | select -ExpandProperty Name
$vmMap = $RecoveryPlanContext.VmMap
 foreach($VMID in $VMinfo)
 {
     $VM = $vmMap.$VMID                
             if( !(($VM -eq $Null) -Or ($VM.ResourceGroupName -eq $Null) -Or ($VM.RoleName -eq $Null))) {
         #this check is to ensure that we skip when some data is not available else it will fail
 Write-output "Resource group name ", $VM.ResourceGroupName
 Write-output "Rolename " = $VM.RoleName
     }
 }

```

> [!NOTE]
> <span data-ttu-id="7e17f-178">Komut dosyasını bir ön eylem önyükleme grubuna olduğunda kaynak grubu adı ve rol adı değeri boş.</span><span class="sxs-lookup"><span data-stu-id="7e17f-178">The resource group name and role name values are empty when the script is a pre-action to a boot group.</span></span> <span data-ttu-id="7e17f-179">Yalnızca bu grubun VM yük devretme kümesinde başarılı olursa değerleri doldurulur.</span><span class="sxs-lookup"><span data-stu-id="7e17f-179">The values are populated only if the VM of that group succeeds in failover.</span></span> <span data-ttu-id="7e17f-180">Komut dosyası, önyükleme grubunun sonrası bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="7e17f-180">The script is a post-action of the boot group.</span></span>

## <a name="use-the-same-automation-runbook-in-multiple-recovery-plans"></a><span data-ttu-id="7e17f-181">Birden çok kurtarma planları aynı Otomasyon runbook'u kullanın</span><span class="sxs-lookup"><span data-stu-id="7e17f-181">Use the same Automation runbook in multiple recovery plans</span></span>

<span data-ttu-id="7e17f-182">Dış değişkenler kullanarak birden çok kurtarma planları tek bir komut dosyası kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7e17f-182">You can use a single script in multiple recovery plans by using external variables.</span></span> <span data-ttu-id="7e17f-183">Kullanabileceğiniz [Azure Otomasyon değişkenleri](../automation/automation-variables.md) depolamak için bir kurtarma planı yürütme geçirdiğiniz parametreler için.</span><span class="sxs-lookup"><span data-stu-id="7e17f-183">You can use [Azure Automation variables](../automation/automation-variables.md) to store parameters that you can pass for a recovery plan execution.</span></span> <span data-ttu-id="7e17f-184">Kurtarma planı adı önek olarak değişkenine için ekleyerek, her kurtarma planı için bağımsız değişkenleri oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7e17f-184">By adding the recovery plan name as a prefix to the variable, you can create individual variables for each recovery plan.</span></span> <span data-ttu-id="7e17f-185">Ardından, değişkenleri olarak parametreler kullanın.</span><span class="sxs-lookup"><span data-stu-id="7e17f-185">Then, use the variables as parameters.</span></span> <span data-ttu-id="7e17f-186">Komut dosyası olmadan bir parametre değiştirmek, ancak hala komut dosyası çalışma biçimini değiştirme.</span><span class="sxs-lookup"><span data-stu-id="7e17f-186">You can change a parameter without changing the script, but still change the way the script works.</span></span>

### <a name="use-a-simple-string-variable-in-a-runbook-script"></a><span data-ttu-id="7e17f-187">Basit bir dize değişkeni bir runbook komut dosyası kullanın</span><span class="sxs-lookup"><span data-stu-id="7e17f-187">Use a simple string variable in a runbook script</span></span>

<span data-ttu-id="7e17f-188">Bu örnekte, bir komut dosyası bir ağ güvenlik grubu (NSG) girdi alır ve bir kurtarma planı VM'ler için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="7e17f-188">In this example, a script takes the input of a Network Security Group (NSG) and applies it to the VMs of a recovery plan.</span></span>

<span data-ttu-id="7e17f-189">Hangi kurtarma algılamak için komut dosyası için plan çalıştığından, kurtarma planı bağlam kullanın:</span><span class="sxs-lookup"><span data-stu-id="7e17f-189">For the script to detect which recovery plan is running, use the recovery plan context:</span></span>

```
workflow AddPublicIPAndNSG {
    param (
          [parameter(Mandatory=$false)]
          [Object]$RecoveryPlanContext
    )

    $RPName = $RecoveryPlanContext.RecoveryPlanName
```

<span data-ttu-id="7e17f-190">Varolan bir NSG'yi uygulamak için NSG adını ve NSG kaynak grubu adını bilmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="7e17f-190">To apply an existing NSG, you must know the NSG name and the NSG resource group name.</span></span> <span data-ttu-id="7e17f-191">Bu değişkenler kurtarma planı komut için giriş olarak kullanın.</span><span class="sxs-lookup"><span data-stu-id="7e17f-191">Use these variables as inputs for recovery plan scripts.</span></span> <span data-ttu-id="7e17f-192">Bunu yapmak için Otomasyon hesabı varlıkları iki değişken oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7e17f-192">To do this, create two variables in the Automation account assets.</span></span> <span data-ttu-id="7e17f-193">Değişken adı öneki olarak parametrelerini oluşturmakta olduğunuz kurtarma planının adı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="7e17f-193">Add the name of the recovery plan that you are creating the parameters for as a prefix to the variable name.</span></span>

1. <span data-ttu-id="7e17f-194">NSG adı depolamak için bir değişken oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7e17f-194">Create a variable to store the NSG name.</span></span> <span data-ttu-id="7e17f-195">Bir önek kurtarma planının adı kullanarak değişken adına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="7e17f-195">Add a prefix to the variable name by using the name of the recovery plan.</span></span>

    ![Bir NSG adı değişkeni oluşturun](media/site-recovery-runbook-automation-new/var1.png)

2. <span data-ttu-id="7e17f-197">NSG'ın kaynak grubu adı depolamak için bir değişken oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7e17f-197">Create a variable to store the NSG's resource group name.</span></span> <span data-ttu-id="7e17f-198">Bir önek kurtarma planının adı kullanarak değişken adına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="7e17f-198">Add a prefix to the variable name by using the name of the recovery plan.</span></span>

    ![Bir NSG kaynak grubu adı oluşturma](media/site-recovery-runbook-automation-new/var2.png)


3.  <span data-ttu-id="7e17f-200">Komut dosyasında aşağıdaki başvuru kodu değişken değerleri almak için kullanın:</span><span class="sxs-lookup"><span data-stu-id="7e17f-200">In the script, use the following reference code to get the variable values:</span></span>

    ```
    $NSGValue = $RecoveryPlanContext.RecoveryPlanName + "-NSG"
    $NSGRGValue = $RecoveryPlanContext.RecoveryPlanName + "-NSGRG"

    $NSGnameVar = Get-AutomationVariable -Name $NSGValue
    $RGnameVar = Get-AutomationVariable -Name $NSGRGValue
    ```

4.  <span data-ttu-id="7e17f-201">NSG başarısız üzerinden VM ağ arabirimine uygulamak için runbook değişkenlerde kullanın:</span><span class="sxs-lookup"><span data-stu-id="7e17f-201">Use the variables in the runbook to apply the NSG to the network interface of the failed-over VM:</span></span>

    ```
    InlineScript {
    if (($Using:NSGname -ne $Null) -And ($Using:NSGRGname -ne $Null)) {
            $NSG = Get-AzureRmNetworkSecurityGroup -Name $Using:NSGname -ResourceGroupName $Using:NSGRGname
            Write-output $NSG.Id
            #Apply the NSG to a network interface
            #$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
            #Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd `
            #  -AddressPrefix 192.168.1.0/24 -NetworkSecurityGroup $NSG
        }
    }
    ```

<span data-ttu-id="7e17f-202">Her kurtarma planı için bağımsız değişkenleri oluşturun, böylece komut dosyasını yeniden kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7e17f-202">For each recovery plan, create independent variables so that you can reuse the script.</span></span> <span data-ttu-id="7e17f-203">Kurtarma planı adı kullanarak bir önek ekleyin.</span><span class="sxs-lookup"><span data-stu-id="7e17f-203">Add a prefix by using the recovery plan name.</span></span> <span data-ttu-id="7e17f-204">Bir tam, uçtan uca komut dosyası için bu senaryo için bkz: [bir ortak IP NSG VM'ler için bir Site Recovery kurtarma planı test yük devretmesi sırasında ekleyip](https://gallery.technet.microsoft.com/Add-Public-IP-and-NSG-to-a6bb8fee).</span><span class="sxs-lookup"><span data-stu-id="7e17f-204">For a complete, end-to-end script for this scenario, see [Add a public IP and NSG to VMs during test failover of a Site Recovery recovery plan](https://gallery.technet.microsoft.com/Add-Public-IP-and-NSG-to-a6bb8fee).</span></span>


### <a name="use-a-complex-variable-to-store-more-information"></a><span data-ttu-id="7e17f-205">Daha fazla bilgi depolamak için bir karmaşık değişkenini kullanın</span><span class="sxs-lookup"><span data-stu-id="7e17f-205">Use a complex variable to store more information</span></span>

<span data-ttu-id="7e17f-206">Genel IP belirli vm'lerde etkinleştirmek için tek bir komut dosyası istediğiniz bir senaryo düşünün.</span><span class="sxs-lookup"><span data-stu-id="7e17f-206">Consider a scenario in which you want a single script to turn on a public IP on specific VMs.</span></span> <span data-ttu-id="7e17f-207">Başka bir senaryoda, farklı sanal makineleri (değil, tüm VM'ler) üzerinde farklı Nsg'leri uygulamak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7e17f-207">In another scenario, you might want to apply different NSGs on different VMs (not on all VMs).</span></span> <span data-ttu-id="7e17f-208">Herhangi bir kurtarma planı için yeniden kullanılabilir bir komut dosyası yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7e17f-208">You can make a script that is reusable for any recovery plan.</span></span> <span data-ttu-id="7e17f-209">Her kurtarma planı VM'ler değişken sayıda olabilir.</span><span class="sxs-lookup"><span data-stu-id="7e17f-209">Each recovery plan can have a variable number of VMs.</span></span> <span data-ttu-id="7e17f-210">Örneğin, bir SharePoint kurtarma iki ön ucu vardır.</span><span class="sxs-lookup"><span data-stu-id="7e17f-210">For example, a SharePoint recovery has two front ends.</span></span> <span data-ttu-id="7e17f-211">Bir temel çizgi iş kolu (LOB) uygulaması yalnızca bir ön uç vardır.</span><span class="sxs-lookup"><span data-stu-id="7e17f-211">A basic line-of-business (LOB) application has only one front end.</span></span> <span data-ttu-id="7e17f-212">Her kurtarma planı için ayrı değişkenler oluşturamaz.</span><span class="sxs-lookup"><span data-stu-id="7e17f-212">You cannot create separate variables for each recovery plan.</span></span> 

<span data-ttu-id="7e17f-213">Aşağıdaki örnekte, yeni bir teknik kullanır ve oluşturma bir [karmaşık değişkeni](https://msdn.microsoft.com/library/dn913767.aspx?f=255&MSPPError=-2147217396) Azure Otomasyon hesabı varlıkları içinde.</span><span class="sxs-lookup"><span data-stu-id="7e17f-213">In the following example, we use a new technique and create a [complex variable](https://msdn.microsoft.com/library/dn913767.aspx?f=255&MSPPError=-2147217396) in the Azure Automation account assets.</span></span> <span data-ttu-id="7e17f-214">Bunun için birden çok değer belirterek.</span><span class="sxs-lookup"><span data-stu-id="7e17f-214">You do this by specifying multiple values.</span></span> <span data-ttu-id="7e17f-215">Aşağıdaki adımları tamamlamak için Azure PowerShell kullanmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="7e17f-215">You must use Azure PowerShell to complete the following steps:</span></span>

1. <span data-ttu-id="7e17f-216">PowerShell'de, Azure aboneliğinizde oturum açın:</span><span class="sxs-lookup"><span data-stu-id="7e17f-216">In PowerShell, sign in to your Azure subscription:</span></span>

    ```
    login-azurermaccount
    $sub = Get-AzureRmSubscription -Name <SubscriptionName>
    $sub | Select-AzureRmSubscription
    ```

2. <span data-ttu-id="7e17f-217">Parametreleri depolamak için kurtarma planının adı kullanarak karmaşık değişkeni oluşturun:</span><span class="sxs-lookup"><span data-stu-id="7e17f-217">To store the parameters, create the complex variable by using the name of the recovery plan:</span></span>

    ```
    $VMDetails = @{"VMGUID"=@{"ResourceGroupName"="RGNameOfNSG";"NSGName"="NameOfNSG"};"VMGUID2"=@{"ResourceGroupName"="RGNameOfNSG";"NSGName"="NameOfNSG"}}
        New-AzureRmAutomationVariable -ResourceGroupName <RG of Automation Account> -AutomationAccountName <AA Name> -Name <RecoveryPlanName> -Value $VMDetails -Encrypted $false
    ```

3. <span data-ttu-id="7e17f-218">Bu karmaşık değişkeninde **VMDetails** korumalı VM için VM kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="7e17f-218">In this complex variable, **VMDetails** is the VM ID for the protected VM.</span></span> <span data-ttu-id="7e17f-219">Azure portalında VM Kimliği almak için VM özelliklerini görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="7e17f-219">To get the VM ID, in the Azure portal, view the VM properties.</span></span> <span data-ttu-id="7e17f-220">Aşağıdaki ekran görüntüsünde, iki VM ayrıntılarını depolayan bir değişken gösterir:</span><span class="sxs-lookup"><span data-stu-id="7e17f-220">The following screenshot shows a variable that stores the details of two VMs:</span></span>

    ![VM kimliği GUID olarak kullanın](media/site-recovery-runbook-automation-new/vmguid.png)

4. <span data-ttu-id="7e17f-222">Runbook'unuzda bu değişkeni kullanın.</span><span class="sxs-lookup"><span data-stu-id="7e17f-222">Use this variable in your runbook.</span></span> <span data-ttu-id="7e17f-223">Belirtilen VM GUID kurtarma planı bağlamda bulunursa, NSG VM Uygula:</span><span class="sxs-lookup"><span data-stu-id="7e17f-223">If the indicated VM GUID is found in the recovery plan context, apply the NSG on the VM:</span></span>

    ```
    $VMDetailsObj = Get-AutomationVariable -Name $RecoveryPlanContext.RecoveryPlanName
    ```

4. <span data-ttu-id="7e17f-224">Runbook'unuzda, kurtarma planı bağlam VM'ler döngü.</span><span class="sxs-lookup"><span data-stu-id="7e17f-224">In your runbook, loop through the VMs of the recovery plan context.</span></span> <span data-ttu-id="7e17f-225">VM var olup olmadığını denetleyin **$VMDetailsObj**.</span><span class="sxs-lookup"><span data-stu-id="7e17f-225">Check whether the VM exists in **$VMDetailsObj**.</span></span> <span data-ttu-id="7e17f-226">Varsa, erişim NSG'yi uygulamak için değişken özellikleri:</span><span class="sxs-lookup"><span data-stu-id="7e17f-226">If it exists, access the properties of the variable to apply the NSG:</span></span>

    ```
        $VMinfo = $RecoveryPlanContext.VmMap | Get-Member | Where-Object MemberType -EQ NoteProperty | select -ExpandProperty Name
        $vmMap = $RecoveryPlanContext.VmMap

        foreach($VMID in $VMinfo) {
            Write-output $VMDetailsObj.value.$VMID

            if ($VMDetailsObj.value.$VMID -ne $Null) { #If the VM exists in the context, this will not b Null
                $VM = $vmMap.$VMID
                # Access the properties of the variable
                $NSGname = $VMDetailsObj.value.$VMID.'NSGName'
                $NSGRGname = $VMDetailsObj.value.$VMID.'NSGResourceGroupName'

                # Add code to apply the NSG properties to the VM
            }
        }
    ```

<span data-ttu-id="7e17f-227">Farklı bir kurtarma planları için aynı komut dosyasını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7e17f-227">You can use the same script for different recovery plans.</span></span> <span data-ttu-id="7e17f-228">Bir kurtarma planı farklı değişkenlerine karşılık gelen değer depolayarak farklı parametreler girin.</span><span class="sxs-lookup"><span data-stu-id="7e17f-228">Enter different parameters by storing the value that corresponds to a recovery plan in different variables.</span></span>

## <a name="sample-scripts"></a><span data-ttu-id="7e17f-229">Örnek komut dosyaları</span><span class="sxs-lookup"><span data-stu-id="7e17f-229">Sample scripts</span></span>

<span data-ttu-id="7e17f-230">Automation hesabınız için örnek komut dosyaları dağıtmak için **Azure'a Dağıt** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="7e17f-230">To deploy sample scripts to your Automation account, click the **Deploy to Azure** button.</span></span>

<span data-ttu-id="7e17f-231">[![Azure’a dağıtma](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)</span><span class="sxs-lookup"><span data-stu-id="7e17f-231">[![Deploy to Azure](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)</span></span>

<span data-ttu-id="7e17f-232">Başka bir örnek için aşağıdaki videoya bakın.</span><span class="sxs-lookup"><span data-stu-id="7e17f-232">For another example, see the following video.</span></span> <span data-ttu-id="7e17f-233">İki katmanlı WordPress uygulamayı azure'a kurtarmak nasıl gösterir:</span><span class="sxs-lookup"><span data-stu-id="7e17f-233">It demonstrates how to recover a two-tier WordPress application to Azure:</span></span>


> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/One-click-failover-of-a-2-tier-WordPress-application-using-Azure-Site-Recovery/player]



## <a name="additional-resources"></a><span data-ttu-id="7e17f-234">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="7e17f-234">Additional resources</span></span>
* [<span data-ttu-id="7e17f-235">Azure Otomasyon hizmeti farklı çalıştır hesabı</span><span class="sxs-lookup"><span data-stu-id="7e17f-235">Azure Automation service Run As account</span></span>](../automation/automation-sec-configure-azure-runas-account.md)
* [<span data-ttu-id="7e17f-236">Azure Otomasyonu genel bakış</span><span class="sxs-lookup"><span data-stu-id="7e17f-236">Azure Automation overview</span></span>](http://msdn.microsoft.com/library/azure/dn643629.aspx "Azure Otomasyonu genel bakış")
* [<span data-ttu-id="7e17f-237">Azure Automation örnek betikler</span><span class="sxs-lookup"><span data-stu-id="7e17f-237">Azure Automation sample scripts</span></span>](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=User&f\[0\].Value=SC%20Automation%20Product%20Team&f\[0\].Text=SC%20Automation%20Product%20Team "Azure Automation örnek betikler")
