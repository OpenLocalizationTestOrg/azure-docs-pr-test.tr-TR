---
title: "aaaAdd Azure Otomasyonu runbook'ları toorecovery planları hello Klasik Portalı'nda | Microsoft Docs"
description: "Bu makalede, nasıl Azure Site Recovery şimdi kurtarma tooAzure sırasında Azure Otomasyon toocomplete karmaşık görevleri kullanarak tooextend kurtarma planlarını sağlar açıklanmaktadır"
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: f24eaa62-9dea-4fce-92e1-a72513ca0289
ms.service: site-recovery
ms.devlang: powershell
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 08/11/2017
ms.author: ruturajd
ms.openlocfilehash: 3bb7420911afbce289b656f28823b1923e8af0c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-azure-automation-runbooks-toorecovery-plans-in-hello-classic-portal"></a><span data-ttu-id="22dfe-103">Azure Otomasyonu runbook'ları toorecovery planları hello Klasik portalında ekleme</span><span class="sxs-lookup"><span data-stu-id="22dfe-103">Add Azure automation runbooks toorecovery plans in hello classic portal</span></span>
<span data-ttu-id="22dfe-104">Bu öğretici, Azure Site Recovery Azure Otomasyonu tooprovide genişletilebilirlik toorecovery planları ile nasıl tümleşik çalıştığını açıklar.</span><span class="sxs-lookup"><span data-stu-id="22dfe-104">This tutorial describes how Azure Site Recovery integrates with Azure Automation tooprovide extensibility toorecovery plans.</span></span> <span data-ttu-id="22dfe-105">Kurtarma planları kurtarma hem çoğaltma toosecondary bulut hem de çoğaltma tooAzure senaryoları için Azure Site Recovery tarafından korunan sanal makinelerinizin düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="22dfe-105">Recovery plans can orchestrate recovery of your virtual machines protected using Azure Site Recovery for both replication toosecondary cloud and replication tooAzure scenarios.</span></span> <span data-ttu-id="22dfe-106">Ayrıca hello kurtarma yaparken yardımcı **tutarlı bir şekilde doğru**, **yinelenebilir**, ve **otomatik**.</span><span class="sxs-lookup"><span data-stu-id="22dfe-106">They also help in making hello recovery **consistently accurate**, **repeatable**, and **automated**.</span></span> <span data-ttu-id="22dfe-107">Sanal makineleri tooAzure başarısız oluyorsa, Azure Automation tümleştirme kurtarma planları genişletir ve yetenek tooexecute runbook'lar, böylece güçlü bir otomatikleştirme görevleri sağlar verir.</span><span class="sxs-lookup"><span data-stu-id="22dfe-107">If you are failing over your virtual machines tooAzure, integration with Azure Automation extends the recovery plans and gives you capability tooexecute runbooks, thus allowing powerful automation tasks.</span></span>

<span data-ttu-id="22dfe-108">Azure Automation hakkında henüz duymuş değil, kaydolma [burada](https://azure.microsoft.com/services/automation/) ve bunların örnek komut dosyası yükleme [burada](https://azure.microsoft.com/documentation/scripts/).</span><span class="sxs-lookup"><span data-stu-id="22dfe-108">If you have not heard about Azure Automation yet, sign up [here](https://azure.microsoft.com/services/automation/) and download their sample scripts [here](https://azure.microsoft.com/documentation/scripts/).</span></span> <span data-ttu-id="22dfe-109">Daha fazla bilgi edinin [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/) ve Kurtarma'yı kullanarak tooorchestrate kurtarma tooAzure nasıl planları [burada](https://azure.microsoft.com/blog/?p=166264).</span><span class="sxs-lookup"><span data-stu-id="22dfe-109">Read more about [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/) and how tooorchestrate recovery tooAzure using recovery plans [here](https://azure.microsoft.com/blog/?p=166264).</span></span>

<span data-ttu-id="22dfe-110">Kısa Bu öğreticide, nasıl Azure Otomasyon çalışma kitabı kurtarma planları tümleştirebilirsiniz arar.</span><span class="sxs-lookup"><span data-stu-id="22dfe-110">In this short tutorial, we will look at how you can integrate Azure Automation runbooks into recovery plans.</span></span> <span data-ttu-id="22dfe-111">Biz, daha önce el ile müdahale gerekli basit görevleri otomatik hale getirmek ve nasıl tooconvert bir çoklu adım kurtarma tek tıklamayla kurtarma eyleme bakın.</span><span class="sxs-lookup"><span data-stu-id="22dfe-111">We will automate simple tasks that earlier required manual intervention and see how tooconvert a multi step recovery into a single-click recovery action.</span></span> <span data-ttu-id="22dfe-112">Biz de sorun yaşanırsa nasıl basit bir komut dosyası giderebileceğinizi adresindeki arar.</span><span class="sxs-lookup"><span data-stu-id="22dfe-112">We will also look at how you can troubleshoot a simple script if it goes wrong.</span></span>

## <a name="protect-hello-application-tooazure"></a><span data-ttu-id="22dfe-113">Merhaba uygulama tooAzure koruma</span><span class="sxs-lookup"><span data-stu-id="22dfe-113">Protect hello application tooAzure</span></span>
<span data-ttu-id="22dfe-114">Bize iki sanal makine içeren basit bir uygulama ile başlar.</span><span class="sxs-lookup"><span data-stu-id="22dfe-114">Let us begin with a simple application consisting of two virtual machines.</span></span> <span data-ttu-id="22dfe-115">Burada, Fabrikam HRweb uygulamasının sahip.</span><span class="sxs-lookup"><span data-stu-id="22dfe-115">Here, we have a HRweb application of Fabrikam.</span></span> <span data-ttu-id="22dfe-116">Fabrikam HRweb frontend ve Fabrikam Hrweb arka Azure Site RECOVERY'yi kullanarak tooAzure korunan hello iki sanal makine var.</span><span class="sxs-lookup"><span data-stu-id="22dfe-116">Fabrikam-HRweb-frontend and Fabrikam-Hrweb-backend are hello two virtual machines protected tooAzure using Azure Site Recovery.</span></span> <span data-ttu-id="22dfe-117">Azure Site Recovery kullanarak tooprotect hello sanal makineleri hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="22dfe-117">tooprotect hello virtual machines using Azure Site Recovery, follow hello steps below.</span></span>

1. <span data-ttu-id="22dfe-118">Sanal makineler için korumayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="22dfe-118">Enable protection for your virtual machines.</span></span>
2. <span data-ttu-id="22dfe-119">Merhaba sanal makinelerin başlangıç çoğaltmasını tamamlamış olmanız ve çoğaltma yapıyorsanız emin olun.</span><span class="sxs-lookup"><span data-stu-id="22dfe-119">Ensure that hello virtual machines have completed initial replication and are replicating.</span></span>
3. <span data-ttu-id="22dfe-120">Merhaba ilk çoğaltma işlemi tamamlandıktan ve korumalı hello çoğaltma durumunu bildiren kadar bekleyin.</span><span class="sxs-lookup"><span data-stu-id="22dfe-120">Wait till hello initial replication completes and hello Replication status says Protected.</span></span>

## ![](media/site-recovery-runbook-automation/01.png)
<span data-ttu-id="22dfe-121">Bu öğreticide, bir kurtarma planı hello Fabrikam HRweb uygulama toofailover hello uygulama tooAzure için oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="22dfe-121">In this tutorial, we will create a recovery plan for hello Fabrikam HRweb application toofailover hello application tooAzure.</span></span> <span data-ttu-id="22dfe-122">Ardından biz bunu bir uç nokta Azure sanal makinesi tooserve web sayfalarını bağlantı noktası 80 üzerinden başarısız hello üzerinde oluşturacak bir runbook ile tümleştirir.</span><span class="sxs-lookup"><span data-stu-id="22dfe-122">Then we will integrate it with a runbook that will create an endpoint on hello failed over Azure virtual machine tooserve web pages at port 80.</span></span>

<span data-ttu-id="22dfe-123">Öncelikle, uygulamamız için bir kurtarma planı oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="22dfe-123">First, let's create a recovery plan for our application.</span></span>

## <a name="create-hello-recovery-plan"></a><span data-ttu-id="22dfe-124">Merhaba kurtarma planı oluşturun</span><span class="sxs-lookup"><span data-stu-id="22dfe-124">Create hello recovery plan</span></span>
<span data-ttu-id="22dfe-125">toorecover hello uygulama tooAzure toocreate bir kurtarma planı gerekir.</span><span class="sxs-lookup"><span data-stu-id="22dfe-125">toorecover hello application tooAzure, you need toocreate a recovery plan.</span></span>
<span data-ttu-id="22dfe-126">Kurtarma sanal makinelerin hello sırasını belirttiğiniz bir kurtarma planı kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="22dfe-126">Using a recovery plan you can specify hello order of recovery of the virtual machines.</span></span> <span data-ttu-id="22dfe-127">1 grupta Hello sanal makineyi kurtarmak ve ilk başlatın ve hello sanal makine 2 grubundaki izleyin.</span><span class="sxs-lookup"><span data-stu-id="22dfe-127">hello virtual machine placed in group 1 will recover and start first, and then hello virtual machine in group 2 will follow.</span></span>

<span data-ttu-id="22dfe-128">Aşağıdaki gibi görünen bir kurtarma planı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="22dfe-128">Create a Recovery Plan that looks like below.</span></span>

![](media/site-recovery-runbook-automation/12.png)

<span data-ttu-id="22dfe-129">belgeleri okuyun, Kurtarma planları hakkında daha fazla tooread [burada](https://msdn.microsoft.com/library/azure/dn788799.aspx "burada").</span><span class="sxs-lookup"><span data-stu-id="22dfe-129">tooread more about recovery plans, read documentation [here](https://msdn.microsoft.com/library/azure/dn788799.aspx "here").</span></span>

<span data-ttu-id="22dfe-130">Ardından, hello Azure Otomasyonu'nda gerekli yapıları oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="22dfe-130">Next, let's create hello necessary artifacts in Azure Automation.</span></span>

## <a name="create-hello-automation-account-and-its-assets"></a><span data-ttu-id="22dfe-131">Merhaba Otomasyon hesabı ve varlıklarını oluşturma</span><span class="sxs-lookup"><span data-stu-id="22dfe-131">Create hello automation account and its assets</span></span>
<span data-ttu-id="22dfe-132">Bir Azure Otomasyonu hesabı toocreate runbook'ları gerekir.</span><span class="sxs-lookup"><span data-stu-id="22dfe-132">You need an Azure Automation account toocreate runbooks.</span></span> <span data-ttu-id="22dfe-133">Bir hesap zaten yoksa tarafından gösterilen tooAzure Otomasyon sekmesine gidin ![](media/site-recovery-runbook-automation/02.png)ve yeni bir hesap oluşturun.</span><span class="sxs-lookup"><span data-stu-id="22dfe-133">If you do not already have an account, navigate tooAzure Automation tab denoted by ![](media/site-recovery-runbook-automation/02.png)and create a new account.</span></span>

1. <span data-ttu-id="22dfe-134">Merhaba hesabı adı tooidentify ile verin.</span><span class="sxs-lookup"><span data-stu-id="22dfe-134">Give hello account a name tooidentify with.</span></span>
2. <span data-ttu-id="22dfe-135">Coğrafi bölge tooplace hello hesap istediğiniz yeri belirtin.</span><span class="sxs-lookup"><span data-stu-id="22dfe-135">Specify a geographical region where you want tooplace hello account.</span></span>

<span data-ttu-id="22dfe-136">Merhaba tooplace hello hesabında önerilen hello ASR kasasıyla aynı bölgede.</span><span class="sxs-lookup"><span data-stu-id="22dfe-136">It is recommended tooplace hello account in hello same region as hello ASR vault.</span></span>

![](media/site-recovery-runbook-automation/03.png)

<span data-ttu-id="22dfe-137">Ardından, hello hesap varlıkları aşağıdaki hello oluşturun.</span><span class="sxs-lookup"><span data-stu-id="22dfe-137">Next, create hello following assets in hello Account.</span></span>

### <a name="add-a-subscription-name-as-asset"></a><span data-ttu-id="22dfe-138">Abonelik adı varlık ekleme</span><span class="sxs-lookup"><span data-stu-id="22dfe-138">Add a subscription name as asset</span></span>
1. <span data-ttu-id="22dfe-139">Yeni bir ayar Ekle ![](media/site-recovery-runbook-automation/04.png) içinde Azure Otomasyon varlıkları hello ve çok seçin![](media/site-recovery-runbook-automation/05.png)</span><span class="sxs-lookup"><span data-stu-id="22dfe-139">Add a new setting ![](media/site-recovery-runbook-automation/04.png) in hello Azure Automation Assets and select too![](media/site-recovery-runbook-automation/05.png)</span></span>
2. <span data-ttu-id="22dfe-140">Merhaba değişken türü olarak seçin **dize**</span><span class="sxs-lookup"><span data-stu-id="22dfe-140">Select hello variable type as **String**</span></span>
3. <span data-ttu-id="22dfe-141">Değişken adı olarak belirtmeniz **AzureSubscriptionName**</span><span class="sxs-lookup"><span data-stu-id="22dfe-141">Specify variable name as **AzureSubscriptionName**</span></span>

   ![](media/site-recovery-runbook-automation/06.png)
4. <span data-ttu-id="22dfe-142">Gerçek Azure aboneliği adınızı hello değişken değer olarak belirtin.</span><span class="sxs-lookup"><span data-stu-id="22dfe-142">Specify your actual Azure Subscription name as hello variable value.</span></span>

   ![](media/site-recovery-runbook-automation/07_1.png)

<span data-ttu-id="22dfe-143">Aboneliğinizi hello Ayarları sayfasından hello Azure portalı hesabınıza hello adını belirleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="22dfe-143">You can identify hello name of your subscription from hello settings page of your account on hello Azure portal.</span></span>

### <a name="add-an-azure-login-credential-as-asset"></a><span data-ttu-id="22dfe-144">Bir Azure oturum açma kimlik bilgileri varlık Ekle</span><span class="sxs-lookup"><span data-stu-id="22dfe-144">Add an Azure login credential as asset</span></span>
<span data-ttu-id="22dfe-145">Azure Otomasyonu, Azure PowerShell tooconnect toothe abonelik kullanır ve orada hello yapıları üzerine çalışır.</span><span class="sxs-lookup"><span data-stu-id="22dfe-145">Azure Automation uses Azure PowerShell tooconnect toothe subscription and operates on hello artifacts there.</span></span> <span data-ttu-id="22dfe-146">Bunun için Microsoft hesabınızla veya bir iş veya Okul hesabı kullanarak kimlik doğrulaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="22dfe-146">For this, you need to authenticate using your Microsoft account or a work or school account.</span></span>
<span data-ttu-id="22dfe-147">Merhaba hesap kimlik bilgilerini güvenli bir şekilde hello runbook tarafından kullanılan bir varlık toobe depolayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="22dfe-147">You can store hello account credentials in an asset toobe used securely by hello runbook.</span></span>

1. <span data-ttu-id="22dfe-148">Yeni bir ayar Ekle ![](media/site-recovery-runbook-automation/04.png) içinde Azure Otomasyon varlıkları hello ve seçin![](media/site-recovery-runbook-automation/09.png)</span><span class="sxs-lookup"><span data-stu-id="22dfe-148">Add a new setting ![](media/site-recovery-runbook-automation/04.png) in hello Azure Automation Assets and select ![](media/site-recovery-runbook-automation/09.png)</span></span>
2. <span data-ttu-id="22dfe-149">Merhaba kimlik bilgisi türü seçin **Windows PowerShell kimlik bilgisi**</span><span class="sxs-lookup"><span data-stu-id="22dfe-149">Select hello Credential type as **Windows PowerShell Credential**</span></span>
3. <span data-ttu-id="22dfe-150">Merhaba adı olarak belirtmeniz **AzureCredential**</span><span class="sxs-lookup"><span data-stu-id="22dfe-150">Specify hello name as **AzureCredential**</span></span>

   ![](media/site-recovery-runbook-automation/10.png)
4. <span data-ttu-id="22dfe-151">Merhaba kullanıcı adı ve parola toosign bileşeniyle birlikte belirtin.</span><span class="sxs-lookup"><span data-stu-id="22dfe-151">Specify hello username and password toosign-in with.</span></span>

<span data-ttu-id="22dfe-152">Şimdi iki bu ayarlar, varlıkları kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="22dfe-152">Now both these settings are available in your assets.</span></span>

![](media/site-recovery-runbook-automation/11.png)

<span data-ttu-id="22dfe-153">Tooconnect tooyour abonelik PowerShell aracılığıyla nasıl verilen hakkında daha fazla bilgi [burada](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="22dfe-153">More information about how tooconnect tooyour subscription via PowerShell is given [here](/powershell/azure/overview).</span></span>

<span data-ttu-id="22dfe-154">Ardından, Azure automation'da hello ön uç sanal makine için bir uç nokta yük devretme sonrasında ekleyebilirsiniz bir runbook oluşturun.</span><span class="sxs-lookup"><span data-stu-id="22dfe-154">Next, you will create a runbook in Azure Automation that can add an endpoint for hello front-end virtual machine after failover.</span></span>

## <a name="azure-automation-context"></a><span data-ttu-id="22dfe-155">Azure Otomasyonu bağlamı</span><span class="sxs-lookup"><span data-stu-id="22dfe-155">Azure automation context</span></span>
<span data-ttu-id="22dfe-156">ASR geçirir bağlam değişken toohello runbook toohelp belirleyici betikler oluşturma.</span><span class="sxs-lookup"><span data-stu-id="22dfe-156">ASR passes a context variable toohello runbook toohelp you write deterministic scripts.</span></span> <span data-ttu-id="22dfe-157">Bir hello bulut hizmeti ve sanal makine hello hello adları tahmin edilebilir, ancak, her zaman bir burada hello sanal makine adı hello adı nedeniyle değiştirilmiş olabilir hello gibi toocertain senaryoları owing hello durumda olmadığını olur karşıdır Azure toounsupported karakter.</span><span class="sxs-lookup"><span data-stu-id="22dfe-157">One could argue that hello names of hello Cloud Service and hello Virtual Machine are predictable, but happens that it is not always hello case owing toocertain scenarios such as hello one where hello name of hello virtual machine name might have changed due toounsupported characters in Azure.</span></span> <span data-ttu-id="22dfe-158">Bu nedenle bu bilgileri toohello ASR kurtarma planı hello bir parçası olarak geçirilen *bağlamı*.</span><span class="sxs-lookup"><span data-stu-id="22dfe-158">Hence this information is passed toohello ASR recovery plan as part of hello *context*.</span></span>

<span data-ttu-id="22dfe-159">Merhaba bağlamının nasıl göründüğünü örneği aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="22dfe-159">Below is an example of how hello context variable looks.</span></span>

        {"RecoveryPlanName":"hrweb-recovery",

        "FailoverType":"Test",

        "FailoverDirection":"PrimaryToSecondary",

        "GroupId":"1",

        "VmMap":{"7a1069c6-c1d6-49c5-8c5d-33bfce8dd183":

                {"CloudServiceName":"pod02hrweb-Chicago-test",

                "RoleName":"Fabrikam-Hrweb-frontend-test"}

                }

        }


<span data-ttu-id="22dfe-160">Merhaba tabloda hello bağlamda her bir değişken için ad ve açıklama içerir.</span><span class="sxs-lookup"><span data-stu-id="22dfe-160">hello table below contains name and description for each variable in hello context.</span></span>

| <span data-ttu-id="22dfe-161">**Değişken adı**</span><span class="sxs-lookup"><span data-stu-id="22dfe-161">**Variable name**</span></span> | <span data-ttu-id="22dfe-162">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="22dfe-162">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="22dfe-163">RecoveryPlanName</span><span class="sxs-lookup"><span data-stu-id="22dfe-163">RecoveryPlanName</span></span> |<span data-ttu-id="22dfe-164">Çalıştırılan planının adı.</span><span class="sxs-lookup"><span data-stu-id="22dfe-164">Name of plan being run.</span></span> <span data-ttu-id="22dfe-165">Eylem adını kullanarak temel aldığınız yardımcı hello aynı komut dosyası</span><span class="sxs-lookup"><span data-stu-id="22dfe-165">Helps you take action based on name using hello same script</span></span> |
| <span data-ttu-id="22dfe-166">FailoverType</span><span class="sxs-lookup"><span data-stu-id="22dfe-166">FailoverType</span></span> |<span data-ttu-id="22dfe-167">Merhaba yük devretme sınamasını olup olmadığını, planlı veya plansız belirtir.</span><span class="sxs-lookup"><span data-stu-id="22dfe-167">Specifies whether hello failover is test, planned, or unplanned.</span></span> |
| <span data-ttu-id="22dfe-168">FailoverDirection</span><span class="sxs-lookup"><span data-stu-id="22dfe-168">FailoverDirection</span></span> |<span data-ttu-id="22dfe-169">Kurtarma tooprimary veya ikincil olup olmadığını belirtin</span><span class="sxs-lookup"><span data-stu-id="22dfe-169">Specify whether recovery is tooprimary or secondary</span></span> |
| <span data-ttu-id="22dfe-170">GroupID</span><span class="sxs-lookup"><span data-stu-id="22dfe-170">GroupID</span></span> |<span data-ttu-id="22dfe-171">Merhaba planı çalıştırırken hello Grup numarası hello kurtarma planı içinde tanımlayın</span><span class="sxs-lookup"><span data-stu-id="22dfe-171">Identify hello group number within hello recovery plan when hello plan is running</span></span> |
| <span data-ttu-id="22dfe-172">VmMap</span><span class="sxs-lookup"><span data-stu-id="22dfe-172">VmMap</span></span> |<span data-ttu-id="22dfe-173">Dizi, hello grubundaki tüm hello sanal makineler</span><span class="sxs-lookup"><span data-stu-id="22dfe-173">Array of all hello virtual machines in hello group</span></span> |
| <span data-ttu-id="22dfe-174">VMMap anahtarı</span><span class="sxs-lookup"><span data-stu-id="22dfe-174">VMMap key</span></span> |<span data-ttu-id="22dfe-175">Her VM için benzersiz anahtar (GUID).</span><span class="sxs-lookup"><span data-stu-id="22dfe-175">Unique key (GUID) for each VM.</span></span> <span data-ttu-id="22dfe-176">Bunu sahip hello hello sanal makinenin VMM kimliği uygunsa hello gibi aynı.</span><span class="sxs-lookup"><span data-stu-id="22dfe-176">It's hello same as hello VMM ID of hello virtual machine where applicable.</span></span> |
| <span data-ttu-id="22dfe-177">Rol adı</span><span class="sxs-lookup"><span data-stu-id="22dfe-177">RoleName</span></span> |<span data-ttu-id="22dfe-178">Merhaba kurtarılmakta olan Azure VM adı</span><span class="sxs-lookup"><span data-stu-id="22dfe-178">Name of hello Azure VM that's being recovered</span></span> |
| <span data-ttu-id="22dfe-179">CloudServiceName</span><span class="sxs-lookup"><span data-stu-id="22dfe-179">CloudServiceName</span></span> |<span data-ttu-id="22dfe-180">Azure bulut hizmeti adı altında hangi hello sanal makine oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="22dfe-180">Azure Cloud Service name under which hello virtual machine is created.</span></span> |

<span data-ttu-id="22dfe-181">Ayrıca toohello VM özellikleri sayfasını ASR Git ve hello VM GUID özelliği Ara hello bağlamda tooidentify hello VmMap anahtarı.</span><span class="sxs-lookup"><span data-stu-id="22dfe-181">tooidentify hello VmMap Key in hello context you could also go toohello VM properties page in ASR and look at hello VM GUID property.</span></span>

![](media/site-recovery-runbook-automation/13.png)

## <a name="author-an-automation-runbook"></a><span data-ttu-id="22dfe-182">Bir Otomasyon runbook'u Yaz</span><span class="sxs-lookup"><span data-stu-id="22dfe-182">Author an Automation runbook</span></span>
<span data-ttu-id="22dfe-183">Şimdi hello runbook tooopen bağlantı noktası 80 üzerinde hello ön uç sanal makine oluşturun.</span><span class="sxs-lookup"><span data-stu-id="22dfe-183">Now create hello runbook tooopen port 80 on hello front-end virtual machine.</span></span>

1. <span data-ttu-id="22dfe-184">Hello Azure Automation hesabını hello ada sahip yeni bir runbook oluşturmak **OpenPort80**</span><span class="sxs-lookup"><span data-stu-id="22dfe-184">Create a new runbook in hello Azure Automation account with hello name **OpenPort80**</span></span>

   ![](media/site-recovery-runbook-automation/14.png)
2. <span data-ttu-id="22dfe-185">Toohello hello runbook Yazar görünümünü gidin ve hello taslak modunda girin.</span><span class="sxs-lookup"><span data-stu-id="22dfe-185">Navigate toohello Author view of hello runbook and enter hello draft mode.</span></span>
3. <span data-ttu-id="22dfe-186">İlk hello değişken toouse hello kurtarma planı bağlamı olarak belirtin</span><span class="sxs-lookup"><span data-stu-id="22dfe-186">First specify hello variable toouse as hello recovery plan context</span></span>

   ```
       param (
           [Object]$RecoveryPlanContext
       )

   ```
4. <span data-ttu-id="22dfe-187">Sonraki toohello abonelik hello kimlik bilgisi ve abonelik adını kullanarak bağlan</span><span class="sxs-lookup"><span data-stu-id="22dfe-187">Next connect toohello subscription using hello credential and subscription name</span></span>

   ```
       $Cred = Get-AutomationPSCredential -Name 'AzureCredential'

       # Connect tooAzure
       $AzureAccount = Add-AzureAccount -Credential $Cred
       $AzureSubscriptionName = Get-AutomationVariable –Name ‘AzureSubscriptionName’
       Select-AzureSubscription -SubscriptionName $AzureSubscriptionName
   ```

   <span data-ttu-id="22dfe-188">Hello Azure kullandığını unutmayın varlıklar – **AzureCredential** ve **AzureSubscriptionName** burada.</span><span class="sxs-lookup"><span data-stu-id="22dfe-188">Note that you use hello Azure assets – **AzureCredential** and **AzureSubscriptionName** here.</span></span>
5. <span data-ttu-id="22dfe-189">Şimdi hello uç nokta ayrıntılarını belirtin ve tooexpose hello endpoint istediğiniz hello sanal makine GUİD'si hello.</span><span class="sxs-lookup"><span data-stu-id="22dfe-189">Now specify hello endpoint details and hello GUID of hello virtual machine for which you want tooexpose hello endpoint.</span></span> <span data-ttu-id="22dfe-190">Bu örneği hello ön uç sanal makine.</span><span class="sxs-lookup"><span data-stu-id="22dfe-190">In this case hello front-end virtual machine.</span></span>

   ```
       # Specify hello parameters toobe used by hello script
       $AEProtocol = "TCP"
       $AELocalPort = 80
       $AEPublicPort = 80
       $AEName = "Port 80 for HTTP"
       $VMGUID = "7a1069c6-c1d6-49c5-8c5d-33bfce8dd183"
   ```

   <span data-ttu-id="22dfe-191">Bu, hello Azure uç noktası protokolü, yerel bağlantı noktası hello VM üzerinde ve eşlenen ortak bağlantı noktasını belirtir.</span><span class="sxs-lookup"><span data-stu-id="22dfe-191">This specifies hello Azure endpoint protocol, local port on hello VM and its mapped public port.</span></span> <span data-ttu-id="22dfe-192">Bu değişkenler parametreleri tarafından hello uç noktaları tooVMs eklemek Azure komutları gereklidir.</span><span class="sxs-lookup"><span data-stu-id="22dfe-192">These variables are parameters     required by hello Azure commands that add endpoints tooVMs.</span></span> <span data-ttu-id="22dfe-193">Merhaba VMGUID hello GUID hello sanal makinenin üzerinde toooperate gereken tutar.</span><span class="sxs-lookup"><span data-stu-id="22dfe-193">hello VMGUID holds hello GUID of hello virtual machine you need toooperate on.</span></span>
6. <span data-ttu-id="22dfe-194">Hello betik şimdi VM GUID verilen hello hello bağlamının ayıklamak ve bir uç nokta hello sanal makine tarafından başvurulan oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="22dfe-194">hello script will now extract hello context for hello given VM GUID and create an endpoint on hello virtual machine referenced by it.</span></span>

   ```
       #Read hello VM GUID from hello context
       $VM = $RecoveryPlanContext.VmMap.$VMGUID

       if ($VM -ne $null)
       {
           # Invoke pipeline commands within an InlineScript

           $EndpointStatus = InlineScript {
               # Invoke hello necessary pipeline commands tooadd a Azure Endpoint tooa specified Virtual Machine
               # Commands include: Get-AzureVM | Add-AzureEndpoint | Update-AzureVM (including parameters)

               $Status = Get-AzureVM -ServiceName $Using:VM.CloudServiceName -Name $Using:VM.RoleName | `
                   Add-AzureEndpoint -Name $Using:AEName -Protocol $Using:AEProtocol -PublicPort $Using:AEPublicPort -LocalPort $Using:AELocalPort | `
                   Update-AzureVM
               Write-Output $Status
           }
       }
   ```
7. <span data-ttu-id="22dfe-195">Tamamlandığında, Yayımla isabet ![](media/site-recovery-runbook-automation/20.png) tooallow, komut dosyası toobe yürütme için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="22dfe-195">Once this is complete, hit Publish ![](media/site-recovery-runbook-automation/20.png) tooallow your script toobe available for execution.</span></span>

<span data-ttu-id="22dfe-196">Merhaba tam komut dosyası başvuru için aşağıda verilmiştir</span><span class="sxs-lookup"><span data-stu-id="22dfe-196">hello complete script is given below for your reference</span></span>

```
  workflow OpenPort80
  {
    param (
        [Object]$RecoveryPlanContext
    )

    $Cred = Get-AutomationPSCredential -Name 'AzureCredential'

    # Connect tooAzure
    $AzureAccount = Add-AzureAccount -Credential $Cred
    $AzureSubscriptionName = Get-AutomationVariable –Name ‘AzureSubscriptionName’
    Select-AzureSubscription -SubscriptionName $AzureSubscriptionName

    # Specify hello parameters toobe used by hello script
    $AEProtocol = "TCP"
    $AELocalPort = 80
    $AEPublicPort = 80
    $AEName = "Port 80 for HTTP"
    $VMGUID = "7a1069c6-c1d6-49c5-8c5d-33bfce8dd183"

    #Read hello VM GUID from hello context
    $VM = $RecoveryPlanContext.VmMap.$VMGUID

    if ($VM -ne $null)
    {
        # Invoke pipeline commands within an InlineScript

        $EndpointStatus = InlineScript {
            # Invoke hello necessary pipeline commands tooadd an Azure Endpoint tooa specified Virtual Machine
            # This set of commands includes: Get-AzureVM | Add-AzureEndpoint | Update-AzureVM (including necessary parameters)

            $Status = Get-AzureVM -ServiceName $Using:VM.CloudServiceName -Name $Using:VM.RoleName | `
                Add-AzureEndpoint -Name $Using:AEName -Protocol $Using:AEProtocol -PublicPort $Using:AEPublicPort -LocalPort $Using:AELocalPort | `
                Update-AzureVM
            Write-Output $Status
        }
    }
  }
```

## <a name="add-hello-script-toohello-recovery-plan"></a><span data-ttu-id="22dfe-197">Merhaba betik toohello kurtarma planına ekleyin</span><span class="sxs-lookup"><span data-stu-id="22dfe-197">Add hello script toohello recovery plan</span></span>
<span data-ttu-id="22dfe-198">Merhaba betik hazır olduktan sonra daha önce oluşturduğunuz toohello kurtarma planı ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="22dfe-198">Once hello script is ready, you can add it toohello recovery plan that you created earlier.</span></span>

1. <span data-ttu-id="22dfe-199">Oluşturduğunuz hello kurtarma planında tooadd 2 gruptan sonra bir komut dosyası seçin.</span><span class="sxs-lookup"><span data-stu-id="22dfe-199">In hello recovery plan you created, choose tooadd a script after the group 2.</span></span> ![](media/site-recovery-runbook-automation/15.png)
2. <span data-ttu-id="22dfe-200">Bir komut dosyası adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="22dfe-200">Specify a script name.</span></span> <span data-ttu-id="22dfe-201">Yalnızca hello kurtarma planı içinde gösteren için bu komut için bir kolay ad budur.</span><span class="sxs-lookup"><span data-stu-id="22dfe-201">This is just a friendly name for this script for showing within hello Recovery plan.</span></span>
3. <span data-ttu-id="22dfe-202">Merhaba yük devretme tooAzure komut dosyasında – hello Azure Otomasyon hesabı adı seçin.</span><span class="sxs-lookup"><span data-stu-id="22dfe-202">In hello failover tooAzure script – Select hello Azure Automation Account name.</span></span>
4. <span data-ttu-id="22dfe-203">Hello Azure runbook'ları, yazdığınız hello runbook'u seçin.</span><span class="sxs-lookup"><span data-stu-id="22dfe-203">In hello Azure Runbooks, select hello runbook you authored.</span></span>

![](media/site-recovery-runbook-automation/16.png)

## <a name="primary-side-scripts"></a><span data-ttu-id="22dfe-204">Birincil tarafı betikler</span><span class="sxs-lookup"><span data-stu-id="22dfe-204">Primary side scripts</span></span>
<span data-ttu-id="22dfe-205">Bir yük devretme tooAzure yürütülürken birincil tarafı betikler tooexecute de seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="22dfe-205">When you are executing a failover tooAzure, you can also choose tooexecute primary side scripts.</span></span> <span data-ttu-id="22dfe-206">Bu komut dosyaları, yük devretme sırasında hello VMM sunucusunda çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="22dfe-206">These scripts will run on hello VMM server during failover.</span></span>
<span data-ttu-id="22dfe-207">Birincil tarafı komut dosyaları yalnızca yalnızca Kapatma öncesi için kullanılabilir ve kapatma aşamaları gönderin.</span><span class="sxs-lookup"><span data-stu-id="22dfe-207">Primary side scripts are only available only for pre-shutdown and post shutdown stages.</span></span> <span data-ttu-id="22dfe-208">Bir olağanüstü durum sağlar, hello birincil site toobe genellikle kullanılamaz bekliyoruz olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="22dfe-208">This is because we expect hello primary site toobe typically unavailable when a disaster strikes.</span></span>
<span data-ttu-id="22dfe-209">Planlanmamış bir yük devretme sırasında yalnızca birincil site işlemleri için kabul ederseniz toorun hello birincil tarafı betikler deneyecek.</span><span class="sxs-lookup"><span data-stu-id="22dfe-209">During an unplanned failover, only if you opt in for primary site operations, it will attempt toorun hello primary side scripts.</span></span> <span data-ttu-id="22dfe-210">Bunlar erişilebilir değil veya zaman aşımı, hello yük devretme devam edecek toorecover sanal makineleri hello.</span><span class="sxs-lookup"><span data-stu-id="22dfe-210">If they are not reachable or timeout, hello failover will continue toorecover hello virtual machines.</span></span>
<span data-ttu-id="22dfe-211">Birincil tarafı betikler beklemediğiniz -, yük devretme tooAzure sırasında korumalı VMM tooAzure olmadan VMware/fiziksel/Hyper-v siteler için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="22dfe-211">Primary side scripts are un-available for VMware/Physical/Hyper-v Sites without VMM protected tooAzure - while you failover tooAzure.</span></span>
<span data-ttu-id="22dfe-212">Ancak, ne zaman, yeniden çalışma Azure tooon içi, birincil tarafı komut dosyaları (Runbook'lar) VMware dışındaki tüm hedefler için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="22dfe-212">However, when you failback from Azure tooon-premises, primary side scripts (Runbooks) can be used for all targets except VMware.</span></span>

## <a name="test-hello-recovery-plan"></a><span data-ttu-id="22dfe-213">Test hello kurtarma planı</span><span class="sxs-lookup"><span data-stu-id="22dfe-213">Test hello recovery plan</span></span>
<span data-ttu-id="22dfe-214">Merhaba runbook toohello planı ekledikten sonra eylemde bakın ve yük devretme testi başlatın.</span><span class="sxs-lookup"><span data-stu-id="22dfe-214">Once you have added hello runbook toohello plan you can initiate a test failover and see it in action.</span></span> <span data-ttu-id="22dfe-215">Her zaman bir sınama yük devretme tootest toorun önerilen hatalar yoktur, uygulama ve hello kurtarma planı tooensure.</span><span class="sxs-lookup"><span data-stu-id="22dfe-215">It is always recommended toorun a test failover tootest your application and hello recovery plan tooensure that there are no errors.</span></span>

1. <span data-ttu-id="22dfe-216">Merhaba kurtarma planı seçin ve bir test yük devretme başlatın.</span><span class="sxs-lookup"><span data-stu-id="22dfe-216">Select hello recovery plan and initiate a test failover.</span></span>
2. <span data-ttu-id="22dfe-217">Merhaba planı yürütme sırasında hello runbook yürütüldü olup olmadığını veya durumunu aracılığıyla değil görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="22dfe-217">During hello plan execution, you can see whether hello runbook has executed or not via its status.</span></span>

   ![](media/site-recovery-runbook-automation/17.png)
3. <span data-ttu-id="22dfe-218">Ayrıca bkz hello ayrıntılı hello Azure Otomasyonu işleri sayfasında hello runbook için runbook yürütme durumu.</span><span class="sxs-lookup"><span data-stu-id="22dfe-218">You can also see hello detailed runbook execution status on hello Azure Automation jobs page for hello runbook.</span></span>

   ![](media/site-recovery-runbook-automation/18.png)
4. <span data-ttu-id="22dfe-219">Merhaba yük devretme tamamlandığında hello runbook yürütme sonucu dışında hello yürütme başarılı olup olmadığını veya hello Azure sanal makinesi sayfasını ziyaret ve hello Uç noktalara arayarak tarafından görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="22dfe-219">After hello failover completes, apart from hello runbook execution result, you can see whether hello execution is successful or not by visiting hello Azure virtual machine page and looking at hello endpoints.</span></span>

![](media/site-recovery-runbook-automation/19.png)

## <a name="sample-scripts"></a><span data-ttu-id="22dfe-220">Örnek komut dosyaları</span><span class="sxs-lookup"><span data-stu-id="22dfe-220">Sample scripts</span></span>
<span data-ttu-id="22dfe-221">Vazgeçtik sırada Bu öğreticide bir Azure sanal makine uç noktası tooan ekleme görev kullanılan bir genellikle otomatikleştirme, bir dizi Azure otomasyonu kullanarak diğer güçlü Otomasyon görevi yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="22dfe-221">While we walked through automating one commonly used task of adding an endpoint tooan Azure virtual machine in this tutorial, you could do a number of other powerful automation tasks using Azure automation.</span></span> <span data-ttu-id="22dfe-222">Microsoft ve hello Azure Automation topluluk yardımcı olabilecek örnek runbook'lar kendi çözümleri ve daha büyük bir otomatikleştirme görevleri için yapı taşı olarak kullanabileceğiniz yardımcı programı runbook'lar oluşturmaya başlamak sağlar.</span><span class="sxs-lookup"><span data-stu-id="22dfe-222">Microsoft and hello Azure Automation community provide sample runbooks which can help you get started creating your own solutions, and utility runbooks, which you can use as building blocks for larger automation tasks.</span></span> <span data-ttu-id="22dfe-223">Merhaba Galerisi'nden kullanmaya başlamak ve Azure Site Recovery kullanarak uygulamalarınızı için güçlü tek tıklatmayla kurtarma planları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="22dfe-223">Start using them from hello gallery and build  powerful one-click recovery plans for your applications using Azure Site Recovery.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="22dfe-224">Ek Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="22dfe-224">Additional Resources</span></span>
[<span data-ttu-id="22dfe-225">Azure Otomasyonu genel bakış</span><span class="sxs-lookup"><span data-stu-id="22dfe-225">Azure Automation Overview</span></span>](http://msdn.microsoft.com/library/azure/dn643629.aspx "Azure Otomasyonu genel bakış")

[<span data-ttu-id="22dfe-226">Örnek Azure Otomasyon betikleri</span><span class="sxs-lookup"><span data-stu-id="22dfe-226">Sample Azure Automation Scripts</span></span>](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=User&f\[0\].Value=SC%20Automation%20Product%20Team&f\[0\].Text=SC%20Automation%20Product%20Team "örnek Azure Otomasyonu komutlar")
