---
title: "Azure Site kurtarma aaaAdd Azure Otomasyonu runbook'ları toorecovery planları | Microsoft Docs"
description: "Azure Site Recovery kurtarma planları Azure otomasyonu kullanarak genişletme nasıl yardımcı olabileceğini öğrenin. Kurtarma tooAzure sırasında nasıl toocomplete karmaşık görevleri öğrenin."
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
ms.openlocfilehash: 90d517200cec5527e98a0d00da466bace587b70b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-azure-automation-runbooks-toorecovery-plans"></a><span data-ttu-id="a2a3a-104">Azure Otomasyonu runbook'ları toorecovery planları ekleme</span><span class="sxs-lookup"><span data-stu-id="a2a3a-104">Add Azure Automation runbooks toorecovery plans</span></span>
<span data-ttu-id="a2a3a-105">Bu makalede, sizi Azure Site Recovery Azure Otomasyonu toohelp ile nasıl tümleşik çalıştığını açıklamak kurtarma planlarınızı genişletir.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-105">In this article, we describe how Azure Site Recovery integrates with Azure Automation toohelp you extend your recovery plans.</span></span> <span data-ttu-id="a2a3a-106">Kurtarma planları korunan sanal makineleri kurtarma Site Recovery ile düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-106">Recovery plans can orchestrate recovery of VMs that are protected with Site Recovery.</span></span> <span data-ttu-id="a2a3a-107">Kurtarma planları çoğaltma tooa ikincil bulut hem çoğaltma tooAzure çalışır.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-107">Recovery plans work both for replication tooa secondary cloud, and for replication tooAzure.</span></span> <span data-ttu-id="a2a3a-108">Kurtarma planları de yardımcı hello kurtarma yapmak **tutarlı bir şekilde doğru**, **yinelenebilir**, ve **otomatik**.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-108">Recovery plans also help make hello recovery **consistently accurate**, **repeatable**, and **automated**.</span></span> <span data-ttu-id="a2a3a-109">Azure Otomasyonu ile tümleştirme, VM'ler tooAzure başarısız olursa kurtarma planlarınızı genişletir.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-109">If you fail over your VMs tooAzure, integration with Azure Automation extends your recovery plans.</span></span> <span data-ttu-id="a2a3a-110">Güçlü bir otomatikleştirme görevleri teklif tooexecute runbook'lar kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-110">You can use it tooexecute runbooks, which offer powerful automation tasks.</span></span>

<span data-ttu-id="a2a3a-111">Yeni tooAzure Otomasyon varsa, şunları yapabilirsiniz [kaydolun](https://azure.microsoft.com/services/automation/) ve [örnek komut dosyası yükleme](https://azure.microsoft.com/documentation/scripts/).</span><span class="sxs-lookup"><span data-stu-id="a2a3a-111">If you are new tooAzure Automation, you can [sign up](https://azure.microsoft.com/services/automation/) and [download sample scripts](https://azure.microsoft.com/documentation/scripts/).</span></span> <span data-ttu-id="a2a3a-112">Daha fazla bilgi ve toolearn nasıl kullanarak tooorchestrate kurtarma tooAzure [kurtarma planlarına](https://azure.microsoft.com/blog/?p=166264), bkz: [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="a2a3a-112">For more information, and toolearn how tooorchestrate recovery tooAzure by using [recovery plans](https://azure.microsoft.com/blog/?p=166264), see [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/).</span></span>

<span data-ttu-id="a2a3a-113">Bu makalede, nasıl Azure Otomasyon çalışma kitabı kurtarma planlarınızı tümleştirebilir açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-113">In this article, we describe how you can integrate Azure Automation runbooks into your recovery plans.</span></span> <span data-ttu-id="a2a3a-114">Daha önce el ile müdahale gerekli örnekler tooautomate temel görevleri kullanırız.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-114">We use examples tooautomate basic tasks that previously required manual intervention.</span></span> <span data-ttu-id="a2a3a-115">Biz de nasıl tooconvert çok adımlı kurtarma tooa tek tıklamayla kurtarma eylemi açıklar.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-115">We also describe how tooconvert a multi-step recovery tooa single-click recovery action.</span></span>

## <a name="customize-hello-recovery-plan"></a><span data-ttu-id="a2a3a-116">Merhaba kurtarma planını özelleştirin</span><span class="sxs-lookup"><span data-stu-id="a2a3a-116">Customize hello recovery plan</span></span>
1. <span data-ttu-id="a2a3a-117">Toohello Git **Site Recovery** kurtarma planı kaynak dikey.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-117">Go toohello **Site Recovery** recovery plan resource blade.</span></span> <span data-ttu-id="a2a3a-118">Bu örnekte, kurtarma için iki VM'ler eklenen tooit hello kurtarma planına sahip.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-118">For this example, hello recovery plan has two VMs added tooit, for recovery.</span></span> <span data-ttu-id="a2a3a-119">bir runbook ekleme toobegin tıklatın hello **Özelleştir** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-119">toobegin adding a runbook, click hello **Customize** tab.</span></span>

    ![Merhaba Özelleştir düğmesini tıklatın](media/site-recovery-runbook-automation-new/essentials-rp.png)


2. <span data-ttu-id="a2a3a-121">Sağ **Grup 1: Başlangıç**ve ardından **post eylem eklemek**.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-121">Right-click **Group 1: Start**, and then select **Add post action**.</span></span>

    ![Sağ Grup 1: Başlatın ve sonrası eylemi ekleyin](media/site-recovery-runbook-automation-new/customize-rp.png)

3. <span data-ttu-id="a2a3a-123">Tıklatın **bir komut dosyası seçin**.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-123">Click **Choose a script**.</span></span>

4. <span data-ttu-id="a2a3a-124">Merhaba üzerinde **güncelleştirme eylem** dikey penceresinde, adı hello betik **Hello World**.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-124">On hello **Update action** blade, name hello script **Hello World**.</span></span>

    ![Merhaba güncelleştirme eylem dikey penceresi](media/site-recovery-runbook-automation-new/update-rp.png)

5. <span data-ttu-id="a2a3a-126">Bir Otomasyon hesabı adı girin.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-126">Enter an Automation account name.</span></span>
    >[!NOTE]
    > <span data-ttu-id="a2a3a-127">Merhaba Automation hesabı Azure herhangi bir bölgede olabilir.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-127">hello Automation account can be in any Azure region.</span></span> <span data-ttu-id="a2a3a-128">Merhaba Otomasyon hesabı hello olmalıdır hello Azure Site kurtarma kasasıyla aynı abonelik.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-128">hello Automation account must be in hello same subscription as hello Azure Site Recovery vault.</span></span>

6. <span data-ttu-id="a2a3a-129">Otomasyon hesabınızda bir runbook seçin.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-129">In your Automation account, select a runbook.</span></span> <span data-ttu-id="a2a3a-130">Bu runbook hello ilk grubunun hello kurtarma işleminden sonra hello kurtarma planının hello yürütme sırasında çalışır hello komut dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-130">This runbook is hello script that runs during hello execution of hello recovery plan, after hello recovery of hello first group.</span></span>

7. <span data-ttu-id="a2a3a-131">toosave hello betik tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-131">toosave hello script, click **OK**.</span></span> <span data-ttu-id="a2a3a-132">Merhaba betik çok eklenen**Grup 1: sonrası adımları**.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-132">hello script is added too**Group 1: Post-steps**.</span></span>

    ![Eylem sonrası Grup 1:Start](media/site-recovery-runbook-automation-new/addedscript-rp.PNG)


## <a name="considerations-for-adding-a-script"></a><span data-ttu-id="a2a3a-134">Bir komut dosyası eklemek için dikkat edilecek noktalar</span><span class="sxs-lookup"><span data-stu-id="a2a3a-134">Considerations for adding a script</span></span>

* <span data-ttu-id="a2a3a-135">Seçenekler için çok**bir adım silme** veya **güncelleştirme hello betik**, hello komut dosyasını sağ tıklatın.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-135">For options too**delete a step** or **update hello script**, right-click hello script.</span></span>
* <span data-ttu-id="a2a3a-136">Bir komut dosyası Azure üzerinde bir şirket içi makineyi tooAzure yük devretme sırasında çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-136">A script can run on Azure during failover from an on-premises machine tooAzure.</span></span> <span data-ttu-id="a2a3a-137">Ayrıca Azure üzerinde bir birincil site komut dosyası kapatma önce olarak Azure tooan şirket içi makineden yeniden çalışma sırasında çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-137">It also can run on Azure as a primary-site script before shutdown, during failback from Azure tooan on-premises machine.</span></span>
* <span data-ttu-id="a2a3a-138">Bir komut dosyası çalıştığında, bir kurtarma planı içeriği yerleştirir.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-138">When a script runs, it injects a recovery plan context.</span></span> <span data-ttu-id="a2a3a-139">Aşağıdaki örnek hello bir bağlam değişkeni gösterir:</span><span class="sxs-lookup"><span data-stu-id="a2a3a-139">hello following example shows a context variable:</span></span>

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

    <span data-ttu-id="a2a3a-140">Aşağıdaki tablonun hello hello adını ve her bir değişken hello bağlamda açıklamasını listeler.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-140">hello following table lists hello name and description of each variable in hello context.</span></span>

    | <span data-ttu-id="a2a3a-141">**Değişken adı**</span><span class="sxs-lookup"><span data-stu-id="a2a3a-141">**Variable name**</span></span> | <span data-ttu-id="a2a3a-142">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="a2a3a-142">**Description**</span></span> |
    | --- | --- |
    | <span data-ttu-id="a2a3a-143">RecoveryPlanName</span><span class="sxs-lookup"><span data-stu-id="a2a3a-143">RecoveryPlanName</span></span> |<span data-ttu-id="a2a3a-144">çalıştırılan hello planının Hello adı.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-144">hello name of hello plan being run.</span></span> <span data-ttu-id="a2a3a-145">Bu değişken, hello kurtarma planı adına göre farklı eylemleri yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-145">This variable helps you take different actions based on hello recovery plan name.</span></span> <span data-ttu-id="a2a3a-146">Ayrıca hello betiği yeniden kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-146">You also can reuse hello script.</span></span> |
    | <span data-ttu-id="a2a3a-147">FailoverType</span><span class="sxs-lookup"><span data-stu-id="a2a3a-147">FailoverType</span></span> |<span data-ttu-id="a2a3a-148">Merhaba yük devretme testi olup olmadığını belirtir, planlı veya plansız.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-148">Specifies whether hello failover is a test, planned, or unplanned.</span></span> |
    | <span data-ttu-id="a2a3a-149">FailoverDirection</span><span class="sxs-lookup"><span data-stu-id="a2a3a-149">FailoverDirection</span></span> |<span data-ttu-id="a2a3a-150">Kurtarma tooa birincil veya ikincil site olup olmadığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-150">Specifies whether recovery is tooa primary or secondary site.</span></span> |
    | <span data-ttu-id="a2a3a-151">GroupID</span><span class="sxs-lookup"><span data-stu-id="a2a3a-151">GroupID</span></span> |<span data-ttu-id="a2a3a-152">Merhaba planı çalıştırırken hello Grup numarası hello kurtarma planında tanımlar.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-152">Identifies hello group number in hello recovery plan when hello plan is running.</span></span> |
    | <span data-ttu-id="a2a3a-153">VmMap</span><span class="sxs-lookup"><span data-stu-id="a2a3a-153">VmMap</span></span> |<span data-ttu-id="a2a3a-154">Merhaba grubundaki tüm sanal makineleri bir dizi.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-154">An array of all VMs in hello group.</span></span> |
    | <span data-ttu-id="a2a3a-155">VMMap anahtarı</span><span class="sxs-lookup"><span data-stu-id="a2a3a-155">VMMap key</span></span> |<span data-ttu-id="a2a3a-156">Her VM için benzersiz anahtar (GUID).</span><span class="sxs-lookup"><span data-stu-id="a2a3a-156">A unique key (GUID) for each VM.</span></span> <span data-ttu-id="a2a3a-157">Aynı Azure Virtual Machine Manager (VMM) Kimliğini Merhaba, hello uygunsa VM hello.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-157">It's hello same as hello Azure Virtual Machine Manager (VMM) ID of hello VM, where applicable.</span></span> |
    | <span data-ttu-id="a2a3a-158">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="a2a3a-158">SubscriptionId</span></span> |<span data-ttu-id="a2a3a-159">hello Azure abonelik kimliği, VM hello oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-159">hello Azure subscription ID in which hello VM was created.</span></span> |
    | <span data-ttu-id="a2a3a-160">Rol adı</span><span class="sxs-lookup"><span data-stu-id="a2a3a-160">RoleName</span></span> |<span data-ttu-id="a2a3a-161">Merhaba kurtarılmakta olan Azure VM Hello adı.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-161">hello name of hello Azure VM that's being recovered.</span></span> |
    | <span data-ttu-id="a2a3a-162">CloudServiceName</span><span class="sxs-lookup"><span data-stu-id="a2a3a-162">CloudServiceName</span></span> |<span data-ttu-id="a2a3a-163">hello Azure bulut hizmeti adı altında VM hello oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-163">hello Azure cloud service name under which hello VM was created.</span></span> |
    | <span data-ttu-id="a2a3a-164">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="a2a3a-164">ResourceGroupName</span></span>|<span data-ttu-id="a2a3a-165">hello Azure kaynak grubu adı altında VM hello oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-165">hello Azure resource group name under which hello VM was created.</span></span> |
    | <span data-ttu-id="a2a3a-166">Recoverypointıd</span><span class="sxs-lookup"><span data-stu-id="a2a3a-166">RecoveryPointId</span></span>|<span data-ttu-id="a2a3a-167">Merhaba VM zaman kurtarılan için hello zaman damgası.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-167">hello timestamp for when hello VM is recovered.</span></span> |

* <span data-ttu-id="a2a3a-168">Bu Otomasyon hesabı hello modülleri aşağıdaki hello sahip emin olun:</span><span class="sxs-lookup"><span data-stu-id="a2a3a-168">Ensure that hello Automation account has hello following modules:</span></span>
    * <span data-ttu-id="a2a3a-169">AzureRM.profile</span><span class="sxs-lookup"><span data-stu-id="a2a3a-169">AzureRM.profile</span></span>
    * <span data-ttu-id="a2a3a-170">AzureRM.Resources</span><span class="sxs-lookup"><span data-stu-id="a2a3a-170">AzureRM.Resources</span></span>
    * <span data-ttu-id="a2a3a-171">AzureRM.Automation</span><span class="sxs-lookup"><span data-stu-id="a2a3a-171">AzureRM.Automation</span></span>
    * <span data-ttu-id="a2a3a-172">AzureRM.Network</span><span class="sxs-lookup"><span data-stu-id="a2a3a-172">AzureRM.Network</span></span>
    * <span data-ttu-id="a2a3a-173">AzureRM.Compute</span><span class="sxs-lookup"><span data-stu-id="a2a3a-173">AzureRM.Compute</span></span>

<span data-ttu-id="a2a3a-174">Tüm modüllerin uyumlu sürümlerini olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-174">All modules should be of compatible versions.</span></span> <span data-ttu-id="a2a3a-175">Tüm modüllerin uyumlu bir kolay bir yolu tooensure toouse hello en son sürümlerini hello olan tüm modülleri ' dir.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-175">An easy way tooensure that all modules are compatible is toouse hello latest versions of all hello modules.</span></span>

### <a name="access-all-vms-of-hello-vmmap-in-a-loop"></a><span data-ttu-id="a2a3a-176">Merhaba VMMap döngü tüm Vm'leri erişim</span><span class="sxs-lookup"><span data-stu-id="a2a3a-176">Access all VMs of hello VMMap in a loop</span></span>
<span data-ttu-id="a2a3a-177">Kod tooloop hello Microsoft VMMap tüm VM'ler üzerindeki aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="a2a3a-177">Use hello following code tooloop across all VMs of hello Microsoft VMMap:</span></span>

```
$VMinfo = $RecoveryPlanContext.VmMap | Get-Member | Where-Object MemberType -EQ NoteProperty | select -ExpandProperty Name
$vmMap = $RecoveryPlanContext.VmMap
 foreach($VMID in $VMinfo)
 {
     $VM = $vmMap.$VMID                
             if( !(($VM -eq $Null) -Or ($VM.ResourceGroupName -eq $Null) -Or ($VM.RoleName -eq $Null))) {
         #this check is tooensure that we skip when some data is not available else it will fail
 Write-output "Resource group name ", $VM.ResourceGroupName
 Write-output "Rolename " = $VM.RoleName
     }
 }

```

> [!NOTE]
> <span data-ttu-id="a2a3a-178">Merhaba betik bir ön eylem tooa önyükleme Grup olduğunda hello kaynak grubu adı ve rol adı değeri boş.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-178">hello resource group name and role name values are empty when hello script is a pre-action tooa boot group.</span></span> <span data-ttu-id="a2a3a-179">Merhaba, o grubun VM yük devretme kümesinde yalnızca başarılı olursa hello değerleri doldurulur.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-179">hello values are populated only if hello VM of that group succeeds in failover.</span></span> <span data-ttu-id="a2a3a-180">Merhaba betik hello önyükleme grubunun sonrası bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-180">hello script is a post-action of hello boot group.</span></span>

## <a name="use-hello-same-automation-runbook-in-multiple-recovery-plans"></a><span data-ttu-id="a2a3a-181">Kullanım hello aynı Otomasyon runbook'ta birden çok kurtarma planları</span><span class="sxs-lookup"><span data-stu-id="a2a3a-181">Use hello same Automation runbook in multiple recovery plans</span></span>

<span data-ttu-id="a2a3a-182">Dış değişkenler kullanarak birden çok kurtarma planları tek bir komut dosyası kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-182">You can use a single script in multiple recovery plans by using external variables.</span></span> <span data-ttu-id="a2a3a-183">Kullanabileceğiniz [Azure Otomasyon değişkenleri](../automation/automation-variables.md) için bir kurtarma geçirebilirsiniz toostore parametreleri yürütme planlayın.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-183">You can use [Azure Automation variables](../automation/automation-variables.md) toostore parameters that you can pass for a recovery plan execution.</span></span> <span data-ttu-id="a2a3a-184">Merhaba kurtarma planı adı öneki toohello değişken olarak ekleyerek, her kurtarma planı için bağımsız değişkenleri oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-184">By adding hello recovery plan name as a prefix toohello variable, you can create individual variables for each recovery plan.</span></span> <span data-ttu-id="a2a3a-185">Ardından, hello değişkenleri olarak parametreler kullanın.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-185">Then, use hello variables as parameters.</span></span> <span data-ttu-id="a2a3a-186">Merhaba betik değiştirmeden bir parametre değiştirebilirsiniz, ancak hala değişiklik hello şekilde hello betik çalışır.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-186">You can change a parameter without changing hello script, but still change hello way hello script works.</span></span>

### <a name="use-a-simple-string-variable-in-a-runbook-script"></a><span data-ttu-id="a2a3a-187">Basit bir dize değişkeni bir runbook komut dosyası kullanın</span><span class="sxs-lookup"><span data-stu-id="a2a3a-187">Use a simple string variable in a runbook script</span></span>

<span data-ttu-id="a2a3a-188">Bu örnekte, bir komut dosyası hello girdi bir ağ güvenlik grubu (NSG) alır ve bir kurtarma planı toohello Vm'leri uygular.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-188">In this example, a script takes hello input of a Network Security Group (NSG) and applies it toohello VMs of a recovery plan.</span></span>

<span data-ttu-id="a2a3a-189">Hangi kurtarma planı çalıştıran hello betik toodetect için hello kurtarma planı bağlam kullanın:</span><span class="sxs-lookup"><span data-stu-id="a2a3a-189">For hello script toodetect which recovery plan is running, use hello recovery plan context:</span></span>

```
workflow AddPublicIPAndNSG {
    param (
          [parameter(Mandatory=$false)]
          [Object]$RecoveryPlanContext
    )

    $RPName = $RecoveryPlanContext.RecoveryPlanName
```

<span data-ttu-id="a2a3a-190">Varolan bir NSG tooapply, hello NSG adını ve hello NSG kaynak grubu adını bilmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-190">tooapply an existing NSG, you must know hello NSG name and hello NSG resource group name.</span></span> <span data-ttu-id="a2a3a-191">Bu değişkenler kurtarma planı komut için giriş olarak kullanın.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-191">Use these variables as inputs for recovery plan scripts.</span></span> <span data-ttu-id="a2a3a-192">toodo Bu, iki değişken hello Otomasyon hesabı varlıklar oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-192">toodo this, create two variables in hello Automation account assets.</span></span> <span data-ttu-id="a2a3a-193">Bir önek toohello değişken adı olacak şekilde hello parametrelerini oluşturmakta olduğunuz hello kurtarma planı Hello adını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-193">Add hello name of hello recovery plan that you are creating hello parameters for as a prefix toohello variable name.</span></span>

1. <span data-ttu-id="a2a3a-194">Bir değişken toostore hello NSG adı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-194">Create a variable toostore hello NSG name.</span></span> <span data-ttu-id="a2a3a-195">Merhaba kurtarma planı hello adını kullanarak bir önek toohello değişken adı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-195">Add a prefix toohello variable name by using hello name of hello recovery plan.</span></span>

    ![Bir NSG adı değişkeni oluşturun](media/site-recovery-runbook-automation-new/var1.png)

2. <span data-ttu-id="a2a3a-197">Değişken toostore hello NSG'ın bir kaynak grubu adı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-197">Create a variable toostore hello NSG's resource group name.</span></span> <span data-ttu-id="a2a3a-198">Merhaba kurtarma planı hello adını kullanarak bir önek toohello değişken adı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-198">Add a prefix toohello variable name by using hello name of hello recovery plan.</span></span>

    ![Bir NSG kaynak grubu adı oluşturma](media/site-recovery-runbook-automation-new/var2.png)


3.  <span data-ttu-id="a2a3a-200">Merhaba komut dosyasında başvuru kodu tooget hello değişken değerleri aşağıdaki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="a2a3a-200">In hello script, use hello following reference code tooget hello variable values:</span></span>

    ```
    $NSGValue = $RecoveryPlanContext.RecoveryPlanName + "-NSG"
    $NSGRGValue = $RecoveryPlanContext.RecoveryPlanName + "-NSGRG"

    $NSGnameVar = Get-AutomationVariable -Name $NSGValue
    $RGnameVar = Get-AutomationVariable -Name $NSGRGValue
    ```

4.  <span data-ttu-id="a2a3a-201">Merhaba runbook tooapply hello NSG toohello ağ arabiriminin hello kullan hello değişkenleri başarısız oldu-VM üzerinde:</span><span class="sxs-lookup"><span data-stu-id="a2a3a-201">Use hello variables in hello runbook tooapply hello NSG toohello network interface of hello failed-over VM:</span></span>

    ```
    InlineScript {
    if (($Using:NSGname -ne $Null) -And ($Using:NSGRGname -ne $Null)) {
            $NSG = Get-AzureRmNetworkSecurityGroup -Name $Using:NSGname -ResourceGroupName $Using:NSGRGname
            Write-output $NSG.Id
            #Apply hello NSG tooa network interface
            #$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
            #Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd `
            #  -AddressPrefix 192.168.1.0/24 -NetworkSecurityGroup $NSG
        }
    }
    ```

<span data-ttu-id="a2a3a-202">Her kurtarma planı için bağımsız değişkenleri oluşturun, böylece hello betiği yeniden kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-202">For each recovery plan, create independent variables so that you can reuse hello script.</span></span> <span data-ttu-id="a2a3a-203">Merhaba kurtarma planı adı kullanarak bir önek ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-203">Add a prefix by using hello recovery plan name.</span></span> <span data-ttu-id="a2a3a-204">Bir tam, uçtan uca komut dosyası için bu senaryo için bkz: [bir Site Recovery kurtarma planı test yük devretmesi sırasında genel bir IP ve NSG tooVMs eklemek](https://gallery.technet.microsoft.com/Add-Public-IP-and-NSG-to-a6bb8fee).</span><span class="sxs-lookup"><span data-stu-id="a2a3a-204">For a complete, end-to-end script for this scenario, see [Add a public IP and NSG tooVMs during test failover of a Site Recovery recovery plan](https://gallery.technet.microsoft.com/Add-Public-IP-and-NSG-to-a6bb8fee).</span></span>


### <a name="use-a-complex-variable-toostore-more-information"></a><span data-ttu-id="a2a3a-205">Daha fazla bilgi karmaşık değişkeni toostore kullanın</span><span class="sxs-lookup"><span data-stu-id="a2a3a-205">Use a complex variable toostore more information</span></span>

<span data-ttu-id="a2a3a-206">Genel IP belirli vm'lerde üzerinde tek bir komut dosyası tooturn istediğiniz bir senaryo düşünün.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-206">Consider a scenario in which you want a single script tooturn on a public IP on specific VMs.</span></span> <span data-ttu-id="a2a3a-207">Başka bir senaryoda tooapply isteyebilirsiniz farklı Nsg'leri farklı vm'lerde (değil, tüm VM'ler).</span><span class="sxs-lookup"><span data-stu-id="a2a3a-207">In another scenario, you might want tooapply different NSGs on different VMs (not on all VMs).</span></span> <span data-ttu-id="a2a3a-208">Herhangi bir kurtarma planı için yeniden kullanılabilir bir komut dosyası yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-208">You can make a script that is reusable for any recovery plan.</span></span> <span data-ttu-id="a2a3a-209">Her kurtarma planı VM'ler değişken sayıda olabilir.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-209">Each recovery plan can have a variable number of VMs.</span></span> <span data-ttu-id="a2a3a-210">Örneğin, bir SharePoint kurtarma iki ön ucu vardır.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-210">For example, a SharePoint recovery has two front ends.</span></span> <span data-ttu-id="a2a3a-211">Bir temel çizgi iş kolu (LOB) uygulaması yalnızca bir ön uç vardır.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-211">A basic line-of-business (LOB) application has only one front end.</span></span> <span data-ttu-id="a2a3a-212">Her kurtarma planı için ayrı değişkenler oluşturamaz.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-212">You cannot create separate variables for each recovery plan.</span></span> 

<span data-ttu-id="a2a3a-213">Merhaba, aşağıdaki örnek, yeni bir teknik kullanır ve oluşturma bir [karmaşık değişkeni](https://msdn.microsoft.com/library/dn913767.aspx?f=255&MSPPError=-2147217396) hello Azure Otomasyon hesabı varlıkları içinde.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-213">In hello following example, we use a new technique and create a [complex variable](https://msdn.microsoft.com/library/dn913767.aspx?f=255&MSPPError=-2147217396) in hello Azure Automation account assets.</span></span> <span data-ttu-id="a2a3a-214">Bunun için birden çok değer belirterek.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-214">You do this by specifying multiple values.</span></span> <span data-ttu-id="a2a3a-215">Azure PowerShell toocomplete hello aşağıdaki adımları kullanmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="a2a3a-215">You must use Azure PowerShell toocomplete hello following steps:</span></span>

1. <span data-ttu-id="a2a3a-216">PowerShell'de tooyour Azure aboneliği imzalayın:</span><span class="sxs-lookup"><span data-stu-id="a2a3a-216">In PowerShell, sign in tooyour Azure subscription:</span></span>

    ```
    login-azurermaccount
    $sub = Get-AzureRmSubscription -Name <SubscriptionName>
    $sub | Select-AzureRmSubscription
    ```

2. <span data-ttu-id="a2a3a-217">toostore hello parametreleri hello kurtarma planı hello adını kullanarak hello karmaşık değişkeni oluşturun:</span><span class="sxs-lookup"><span data-stu-id="a2a3a-217">toostore hello parameters, create hello complex variable by using hello name of hello recovery plan:</span></span>

    ```
    $VMDetails = @{"VMGUID"=@{"ResourceGroupName"="RGNameOfNSG";"NSGName"="NameOfNSG"};"VMGUID2"=@{"ResourceGroupName"="RGNameOfNSG";"NSGName"="NameOfNSG"}}
        New-AzureRmAutomationVariable -ResourceGroupName <RG of Automation Account> -AutomationAccountName <AA Name> -Name <RecoveryPlanName> -Value $VMDetails -Encrypted $false
    ```

3. <span data-ttu-id="a2a3a-218">Bu karmaşık değişkeninde **VMDetails** VM hello korumalı hello VM kimliği aranır.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-218">In this complex variable, **VMDetails** is hello VM ID for hello protected VM.</span></span> <span data-ttu-id="a2a3a-219">hello Azure portal tooget hello VM kimliği hello VM özelliklerini görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-219">tooget hello VM ID, in hello Azure portal, view hello VM properties.</span></span> <span data-ttu-id="a2a3a-220">Merhaba aşağıdaki ekran görüntüsünde iki VM hello ayrıntılarını depolayan bir değişken gösterir:</span><span class="sxs-lookup"><span data-stu-id="a2a3a-220">hello following screenshot shows a variable that stores hello details of two VMs:</span></span>

    ![Merhaba VM kimliği GUID hello olarak kullanın](media/site-recovery-runbook-automation-new/vmguid.png)

4. <span data-ttu-id="a2a3a-222">Runbook'unuzda bu değişkeni kullanın.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-222">Use this variable in your runbook.</span></span> <span data-ttu-id="a2a3a-223">Merhaba VM GUID hello kurtarma planı bağlamda bulunan belirtilmişse hello NSG hello VM üzerinde geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="a2a3a-223">If hello indicated VM GUID is found in hello recovery plan context, apply hello NSG on hello VM:</span></span>

    ```
    $VMDetailsObj = Get-AutomationVariable -Name $RecoveryPlanContext.RecoveryPlanName
    ```

4. <span data-ttu-id="a2a3a-224">Runbook'unuzda, hello kurtarma planı bağlam hello VM'ler döngü.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-224">In your runbook, loop through hello VMs of hello recovery plan context.</span></span> <span data-ttu-id="a2a3a-225">Merhaba VM var olup olmadığını denetleyin **$VMDetailsObj**.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-225">Check whether hello VM exists in **$VMDetailsObj**.</span></span> <span data-ttu-id="a2a3a-226">Varsa, erişim hello değişken tooapply hello NSG hello özellikleri:</span><span class="sxs-lookup"><span data-stu-id="a2a3a-226">If it exists, access hello properties of hello variable tooapply hello NSG:</span></span>

    ```
        $VMinfo = $RecoveryPlanContext.VmMap | Get-Member | Where-Object MemberType -EQ NoteProperty | select -ExpandProperty Name
        $vmMap = $RecoveryPlanContext.VmMap

        foreach($VMID in $VMinfo) {
            Write-output $VMDetailsObj.value.$VMID

            if ($VMDetailsObj.value.$VMID -ne $Null) { #If hello VM exists in hello context, this will not b Null
                $VM = $vmMap.$VMID
                # Access hello properties of hello variable
                $NSGname = $VMDetailsObj.value.$VMID.'NSGName'
                $NSGRGname = $VMDetailsObj.value.$VMID.'NSGResourceGroupName'

                # Add code tooapply hello NSG properties toohello VM
            }
        }
    ```

<span data-ttu-id="a2a3a-227">Farklı bir kurtarma planları için aynı komut dosyası hello kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-227">You can use hello same script for different recovery plans.</span></span> <span data-ttu-id="a2a3a-228">Tooa kurtarma planı farklı değişkenlerine karşılık gelen hello değer depolayarak farklı parametreler girin.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-228">Enter different parameters by storing hello value that corresponds tooa recovery plan in different variables.</span></span>

## <a name="sample-scripts"></a><span data-ttu-id="a2a3a-229">Örnek komut dosyaları</span><span class="sxs-lookup"><span data-stu-id="a2a3a-229">Sample scripts</span></span>

<span data-ttu-id="a2a3a-230">toodeploy örnek komut dosyaları tooyour Automation hesabını tıklatın hello **tooAzure dağıtmak** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-230">toodeploy sample scripts tooyour Automation account, click hello **Deploy tooAzure** button.</span></span>

<span data-ttu-id="a2a3a-231">[![TooAzure dağıtma](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)</span><span class="sxs-lookup"><span data-stu-id="a2a3a-231">[![Deploy tooAzure](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)</span></span>

<span data-ttu-id="a2a3a-232">Video aşağıdaki hello başka bir örnek için bkz.</span><span class="sxs-lookup"><span data-stu-id="a2a3a-232">For another example, see hello following video.</span></span> <span data-ttu-id="a2a3a-233">Bunu gösteren nasıl toorecover iki katmanlı WordPress uygulama tooAzure:</span><span class="sxs-lookup"><span data-stu-id="a2a3a-233">It demonstrates how toorecover a two-tier WordPress application tooAzure:</span></span>


> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/One-click-failover-of-a-2-tier-WordPress-application-using-Azure-Site-Recovery/player]



## <a name="additional-resources"></a><span data-ttu-id="a2a3a-234">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="a2a3a-234">Additional resources</span></span>
* [<span data-ttu-id="a2a3a-235">Azure Otomasyon hizmeti farklı çalıştır hesabı</span><span class="sxs-lookup"><span data-stu-id="a2a3a-235">Azure Automation service Run As account</span></span>](../automation/automation-sec-configure-azure-runas-account.md)
* [<span data-ttu-id="a2a3a-236">Azure Otomasyonu genel bakış</span><span class="sxs-lookup"><span data-stu-id="a2a3a-236">Azure Automation overview</span></span>](http://msdn.microsoft.com/library/azure/dn643629.aspx "Azure Otomasyonu genel bakış")
* [<span data-ttu-id="a2a3a-237">Azure Automation örnek betikler</span><span class="sxs-lookup"><span data-stu-id="a2a3a-237">Azure Automation sample scripts</span></span>](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=User&f\[0\].Value=SC%20Automation%20Product%20Team&f\[0\].Text=SC%20Automation%20Product%20Team "Azure Automation örnek betikler")
