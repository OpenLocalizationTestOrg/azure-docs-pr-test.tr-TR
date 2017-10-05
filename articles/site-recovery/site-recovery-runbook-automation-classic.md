---
title: "Kurtarma planları Klasik portalda Azure Otomasyonu runbook'ları ekleyin | Microsoft Docs"
description: "Bu makalede, nasıl Azure Site Recovery artık Azure Kurtarma sırasında karmaşık görevleri tamamlamak için Azure otomasyonu kullanarak kurtarma planlarını genişletmenizi sağlar açıklanmaktadır."
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
ms.openlocfilehash: 0a248e7c3f39a35ac10dc6ac64e5cef7d152e033
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="add-azure-automation-runbooks-to-recovery-plans-in-the-classic-portal"></a><span data-ttu-id="3fe13-103">Kurtarma planları Klasik portalda Azure Otomasyonu runbook'ları ekleyin</span><span class="sxs-lookup"><span data-stu-id="3fe13-103">Add Azure automation runbooks to recovery plans in the classic portal</span></span>
<span data-ttu-id="3fe13-104">Bu öğretici, Azure Site Recovery kurtarma planlarına genişletilebilirlik sağlamak için Azure Automation ile nasıl tümleşik çalıştığını açıklar.</span><span class="sxs-lookup"><span data-stu-id="3fe13-104">This tutorial describes how Azure Site Recovery integrates with Azure Automation to provide extensibility to recovery plans.</span></span> <span data-ttu-id="3fe13-105">Kurtarma planları ikincil bulut için çoğaltma ve Azure senaryoları için çoğaltma için Azure Site Recovery tarafından korunan sanal makinelerinizin kurtarma düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3fe13-105">Recovery plans can orchestrate recovery of your virtual machines protected using Azure Site Recovery for both replication to secondary cloud and replication to Azure scenarios.</span></span> <span data-ttu-id="3fe13-106">Ayrıca kurtarma yaparken yardımcı **tutarlı bir şekilde doğru**, **yinelenebilir**, ve **otomatik**.</span><span class="sxs-lookup"><span data-stu-id="3fe13-106">They also help in making the recovery **consistently accurate**, **repeatable**, and **automated**.</span></span> <span data-ttu-id="3fe13-107">Azure sanal makineleriniz başarısız oluyorsa, Azure Automation tümleştirme kurtarma planları genişletir ve runbook'ları, böylece güçlü bir otomatikleştirme görevleri sağlar yürütmek için yeteneği verir.</span><span class="sxs-lookup"><span data-stu-id="3fe13-107">If you are failing over your virtual machines to Azure, integration with Azure Automation extends the recovery plans and gives you capability to execute runbooks, thus allowing powerful automation tasks.</span></span>

<span data-ttu-id="3fe13-108">Azure Automation hakkında henüz duymuş değil, kaydolma [burada](https://azure.microsoft.com/services/automation/) ve bunların örnek komut dosyası yükleme [burada](https://azure.microsoft.com/documentation/scripts/).</span><span class="sxs-lookup"><span data-stu-id="3fe13-108">If you have not heard about Azure Automation yet, sign up [here](https://azure.microsoft.com/services/automation/) and download their sample scripts [here](https://azure.microsoft.com/documentation/scripts/).</span></span> <span data-ttu-id="3fe13-109">Daha fazla bilgi edinin [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/) ve kurtarma planlarınızı kullanarak Azure kurtarma düzenlemek nasıl [burada](https://azure.microsoft.com/blog/?p=166264).</span><span class="sxs-lookup"><span data-stu-id="3fe13-109">Read more about [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/) and how to orchestrate recovery to Azure using recovery plans [here](https://azure.microsoft.com/blog/?p=166264).</span></span>

<span data-ttu-id="3fe13-110">Kısa Bu öğreticide, nasıl Azure Otomasyon çalışma kitabı kurtarma planları tümleştirebilirsiniz arar.</span><span class="sxs-lookup"><span data-stu-id="3fe13-110">In this short tutorial, we will look at how you can integrate Azure Automation runbooks into recovery plans.</span></span> <span data-ttu-id="3fe13-111">Biz, daha önce el ile müdahale gerekli basit görevleri otomatik hale getirmek ve birden çok adım kurtarma tek tıklamayla kurtarma eyleme dönüştürmek bkz.</span><span class="sxs-lookup"><span data-stu-id="3fe13-111">We will automate simple tasks that earlier required manual intervention and see how to convert a multi step recovery into a single-click recovery action.</span></span> <span data-ttu-id="3fe13-112">Biz de sorun yaşanırsa nasıl basit bir komut dosyası giderebileceğinizi adresindeki arar.</span><span class="sxs-lookup"><span data-stu-id="3fe13-112">We will also look at how you can troubleshoot a simple script if it goes wrong.</span></span>

## <a name="protect-the-application-to-azure"></a><span data-ttu-id="3fe13-113">Uygulamayı Azure'a koruma</span><span class="sxs-lookup"><span data-stu-id="3fe13-113">Protect the application to Azure</span></span>
<span data-ttu-id="3fe13-114">Bize iki sanal makine içeren basit bir uygulama ile başlar.</span><span class="sxs-lookup"><span data-stu-id="3fe13-114">Let us begin with a simple application consisting of two virtual machines.</span></span> <span data-ttu-id="3fe13-115">Burada, Fabrikam HRweb uygulamasının sahip.</span><span class="sxs-lookup"><span data-stu-id="3fe13-115">Here, we have a HRweb application of Fabrikam.</span></span> <span data-ttu-id="3fe13-116">Fabrikam HRweb frontend ve Fabrikam Hrweb arka Azure için korunan iki sanal makine Azure Site Recovery kullanıldığında'dır.</span><span class="sxs-lookup"><span data-stu-id="3fe13-116">Fabrikam-HRweb-frontend and Fabrikam-Hrweb-backend are the two virtual machines protected to Azure using Azure Site Recovery.</span></span> <span data-ttu-id="3fe13-117">Azure Site Recovery kullanarak sanal makineleri korumak için aşağıdaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="3fe13-117">To protect the virtual machines using Azure Site Recovery, follow the steps below.</span></span>

1. <span data-ttu-id="3fe13-118">Sanal makineler için korumayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="3fe13-118">Enable protection for your virtual machines.</span></span>
2. <span data-ttu-id="3fe13-119">Sanal makinelerin başlangıç çoğaltmasını tamamlamış olmanız ve çoğaltma olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="3fe13-119">Ensure that the virtual machines have completed initial replication and are replicating.</span></span>
3. <span data-ttu-id="3fe13-120">İlk çoğaltma işlemi tamamlandıktan ve korumalı çoğaltma durumunu bildiren kadar bekleyin.</span><span class="sxs-lookup"><span data-stu-id="3fe13-120">Wait till the initial replication completes and the Replication status says Protected.</span></span>

## ![](media/site-recovery-runbook-automation/01.png)
<span data-ttu-id="3fe13-121">Bu öğreticide, bir kurtarma planı yük devretme uygulamayı Azure'a Fabrikam HRweb uygulamasının oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="3fe13-121">In this tutorial, we will create a recovery plan for the Fabrikam HRweb application to failover the application to Azure.</span></span> <span data-ttu-id="3fe13-122">Biz bir uç nokta başarısız üzerinde oluşturacak bir runbook ile tümleştirecek sonra bağlantı noktası 80 web sayfaları için Azure sanal makinesi üzerinde.</span><span class="sxs-lookup"><span data-stu-id="3fe13-122">Then we will integrate it with a runbook that will create an endpoint on the failed over Azure virtual machine to serve web pages at port 80.</span></span>

<span data-ttu-id="3fe13-123">Öncelikle, uygulamamız için bir kurtarma planı oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="3fe13-123">First, let's create a recovery plan for our application.</span></span>

## <a name="create-the-recovery-plan"></a><span data-ttu-id="3fe13-124">Kurtarma planı oluşturun</span><span class="sxs-lookup"><span data-stu-id="3fe13-124">Create the recovery plan</span></span>
<span data-ttu-id="3fe13-125">Uygulamayı Azure'a kurtarmak için bir kurtarma planı oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="3fe13-125">To recover the application to Azure, you need to create a recovery plan.</span></span>
<span data-ttu-id="3fe13-126">Kurtarma sanal makinelerin sırasını belirttiğiniz bir kurtarma planı kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="3fe13-126">Using a recovery plan you can specify the order of recovery of the virtual machines.</span></span> <span data-ttu-id="3fe13-127">1 grupta sanal makineyi kurtarmak ve ilk başlatın ve sonra 2 grubundaki sanal makine izleyin.</span><span class="sxs-lookup"><span data-stu-id="3fe13-127">The virtual machine placed in group 1 will recover and start first, and then the virtual machine in group 2 will follow.</span></span>

<span data-ttu-id="3fe13-128">Aşağıdaki gibi görünen bir kurtarma planı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3fe13-128">Create a Recovery Plan that looks like below.</span></span>

![](media/site-recovery-runbook-automation/12.png)

<span data-ttu-id="3fe13-129">Daha fazla bilgi için kurtarma planları hakkında belgelerini okuyun [burada](https://msdn.microsoft.com/library/azure/dn788799.aspx "burada").</span><span class="sxs-lookup"><span data-stu-id="3fe13-129">To read more about recovery plans, read documentation [here](https://msdn.microsoft.com/library/azure/dn788799.aspx "here").</span></span>

<span data-ttu-id="3fe13-130">Ardından, gerekli yapıları Azure Otomasyonu'nda oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="3fe13-130">Next, let's create the necessary artifacts in Azure Automation.</span></span>

## <a name="create-the-automation-account-and-its-assets"></a><span data-ttu-id="3fe13-131">Otomasyon hesabı ve varlıklarını oluşturma</span><span class="sxs-lookup"><span data-stu-id="3fe13-131">Create the automation account and its assets</span></span>
<span data-ttu-id="3fe13-132">Runbook'ları oluşturmak için bir Azure Otomasyonu hesabı gerekir.</span><span class="sxs-lookup"><span data-stu-id="3fe13-132">You need an Azure Automation account to create runbooks.</span></span> <span data-ttu-id="3fe13-133">Bir hesap zaten yoksa tarafından belirtilen Azure Otomasyonu sekmesine gidin ![](media/site-recovery-runbook-automation/02.png)ve yeni bir hesap oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3fe13-133">If you do not already have an account, navigate to Azure Automation tab denoted by ![](media/site-recovery-runbook-automation/02.png)and create a new account.</span></span>

1. <span data-ttu-id="3fe13-134">Hesabı ile tanımlamak için bir ad verin.</span><span class="sxs-lookup"><span data-stu-id="3fe13-134">Give the account a name to identify with.</span></span>
2. <span data-ttu-id="3fe13-135">Coğrafi bölge hesap eklemek istediğiniz yeri belirtin.</span><span class="sxs-lookup"><span data-stu-id="3fe13-135">Specify a geographical region where you want to place the account.</span></span>

<span data-ttu-id="3fe13-136">ASR kasasıyla aynı bölgede hesap yerleştirmek için önerilir.</span><span class="sxs-lookup"><span data-stu-id="3fe13-136">It is recommended to place the account in the same region as the ASR vault.</span></span>

![](media/site-recovery-runbook-automation/03.png)

<span data-ttu-id="3fe13-137">Ardından, aşağıdaki varlıklar hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3fe13-137">Next, create the following assets in the Account.</span></span>

### <a name="add-a-subscription-name-as-asset"></a><span data-ttu-id="3fe13-138">Abonelik adı varlık ekleme</span><span class="sxs-lookup"><span data-stu-id="3fe13-138">Add a subscription name as asset</span></span>
1. <span data-ttu-id="3fe13-139">Yeni bir ayar Ekle ![](media/site-recovery-runbook-automation/04.png) Azure Otomasyon varlıkları ve seçmek için![](media/site-recovery-runbook-automation/05.png)</span><span class="sxs-lookup"><span data-stu-id="3fe13-139">Add a new setting ![](media/site-recovery-runbook-automation/04.png) in the Azure Automation Assets and select to ![](media/site-recovery-runbook-automation/05.png)</span></span>
2. <span data-ttu-id="3fe13-140">Değişken türü olarak seçin **dize**</span><span class="sxs-lookup"><span data-stu-id="3fe13-140">Select the variable type as **String**</span></span>
3. <span data-ttu-id="3fe13-141">Değişken adı olarak belirtmeniz **AzureSubscriptionName**</span><span class="sxs-lookup"><span data-stu-id="3fe13-141">Specify variable name as **AzureSubscriptionName**</span></span>

   ![](media/site-recovery-runbook-automation/06.png)
4. <span data-ttu-id="3fe13-142">Değişken değeri olarak, gerçek Azure abonelik adını belirtin.</span><span class="sxs-lookup"><span data-stu-id="3fe13-142">Specify your actual Azure Subscription name as the variable value.</span></span>

   ![](media/site-recovery-runbook-automation/07_1.png)

<span data-ttu-id="3fe13-143">Aboneliğiniz Azure portalındaki hesabınızın Ayarları sayfasından adını belirleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3fe13-143">You can identify the name of your subscription from the settings page of your account on the Azure portal.</span></span>

### <a name="add-an-azure-login-credential-as-asset"></a><span data-ttu-id="3fe13-144">Bir Azure oturum açma kimlik bilgileri varlık Ekle</span><span class="sxs-lookup"><span data-stu-id="3fe13-144">Add an Azure login credential as asset</span></span>
<span data-ttu-id="3fe13-145">Azure Otomasyonu aboneliğine bağlanmak için Azure PowerShell kullanır ve var. yapıları üzerinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="3fe13-145">Azure Automation uses Azure PowerShell to connect to the subscription and operates on the artifacts there.</span></span> <span data-ttu-id="3fe13-146">Bunun için Microsoft hesabınızla veya bir iş veya Okul hesabı kullanarak kimlik doğrulaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="3fe13-146">For this, you need to authenticate using your Microsoft account or a work or school account.</span></span>
<span data-ttu-id="3fe13-147">Hesap kimlik bilgilerini güvenli bir şekilde runbook tarafından kullanılacak bir varlık depolayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3fe13-147">You can store the account credentials in an asset to be used securely by the runbook.</span></span>

1. <span data-ttu-id="3fe13-148">Yeni bir ayar Ekle ![](media/site-recovery-runbook-automation/04.png) Azure Otomasyon varlıkları ve seçin![](media/site-recovery-runbook-automation/09.png)</span><span class="sxs-lookup"><span data-stu-id="3fe13-148">Add a new setting ![](media/site-recovery-runbook-automation/04.png) in the Azure Automation Assets and select ![](media/site-recovery-runbook-automation/09.png)</span></span>
2. <span data-ttu-id="3fe13-149">Kimlik bilgisi türü seçin **Windows PowerShell kimlik bilgisi**</span><span class="sxs-lookup"><span data-stu-id="3fe13-149">Select the Credential type as **Windows PowerShell Credential**</span></span>
3. <span data-ttu-id="3fe13-150">Adı olarak belirtmeniz **AzureCredential**</span><span class="sxs-lookup"><span data-stu-id="3fe13-150">Specify the name as **AzureCredential**</span></span>

   ![](media/site-recovery-runbook-automation/10.png)
4. <span data-ttu-id="3fe13-151">Kullanıcı adı ve oturum ile açmak için parola belirtin.</span><span class="sxs-lookup"><span data-stu-id="3fe13-151">Specify the username and password to sign-in with.</span></span>

<span data-ttu-id="3fe13-152">Şimdi iki bu ayarlar, varlıkları kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="3fe13-152">Now both these settings are available in your assets.</span></span>

![](media/site-recovery-runbook-automation/11.png)

<span data-ttu-id="3fe13-153">Aboneliğinizi PowerShell aracılığıyla bağlanma hakkında daha fazla bilgi verilen [burada](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3fe13-153">More information about how to connect to your subscription via PowerShell is given [here](/powershell/azure/overview).</span></span>

<span data-ttu-id="3fe13-154">Ardından, ön uç sanal makine için bir uç nokta yük devretme sonrasında ekleyebilirsiniz Azure Automation runbook oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3fe13-154">Next, you will create a runbook in Azure Automation that can add an endpoint for the front-end virtual machine after failover.</span></span>

## <a name="azure-automation-context"></a><span data-ttu-id="3fe13-155">Azure Otomasyonu bağlamı</span><span class="sxs-lookup"><span data-stu-id="3fe13-155">Azure automation context</span></span>
<span data-ttu-id="3fe13-156">ASR runbook'a belirleyici komut dosyaları yazmanıza yardımcı olacak bir bağlamının geçirir.</span><span class="sxs-lookup"><span data-stu-id="3fe13-156">ASR passes a context variable to the runbook to help you write deterministic scripts.</span></span> <span data-ttu-id="3fe13-157">Bir bulut hizmeti ve sanal makine adları tahmin edilebilir, ancak, her zaman bir gibi belirli senaryolar owing to durumda olduğu sanal makinenin adı desteklenmeyen karakterler nedeniyle değiştirilmiş olabilir olmadığını olur karşıdır Azure.</span><span class="sxs-lookup"><span data-stu-id="3fe13-157">One could argue that the names of the Cloud Service and the Virtual Machine are predictable, but happens that it is not always the case owing to certain scenarios such as the one where the name of the virtual machine name might have changed due to unsupported characters in Azure.</span></span> <span data-ttu-id="3fe13-158">Bu nedenle bu bilgileri ASR kurtarma planına parçası olarak geçirilen *bağlamı*.</span><span class="sxs-lookup"><span data-stu-id="3fe13-158">Hence this information is passed to the ASR recovery plan as part of the *context*.</span></span>

<span data-ttu-id="3fe13-159">Aşağıda bağlamının nasıl göründüğünü bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="3fe13-159">Below is an example of how the context variable looks.</span></span>

        {"RecoveryPlanName":"hrweb-recovery",

        "FailoverType":"Test",

        "FailoverDirection":"PrimaryToSecondary",

        "GroupId":"1",

        "VmMap":{"7a1069c6-c1d6-49c5-8c5d-33bfce8dd183":

                {"CloudServiceName":"pod02hrweb-Chicago-test",

                "RoleName":"Fabrikam-Hrweb-frontend-test"}

                }

        }


<span data-ttu-id="3fe13-160">Aşağıdaki tabloda, her bir değişken bağlamında için ad ve açıklama içerir.</span><span class="sxs-lookup"><span data-stu-id="3fe13-160">The table below contains name and description for each variable in the context.</span></span>

| <span data-ttu-id="3fe13-161">**Değişken adı**</span><span class="sxs-lookup"><span data-stu-id="3fe13-161">**Variable name**</span></span> | <span data-ttu-id="3fe13-162">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="3fe13-162">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="3fe13-163">RecoveryPlanName</span><span class="sxs-lookup"><span data-stu-id="3fe13-163">RecoveryPlanName</span></span> |<span data-ttu-id="3fe13-164">Çalıştırılan planının adı.</span><span class="sxs-lookup"><span data-stu-id="3fe13-164">Name of plan being run.</span></span> <span data-ttu-id="3fe13-165">Aynı komut dosyasını kullanarak adına göre eyleme yardımcı olur</span><span class="sxs-lookup"><span data-stu-id="3fe13-165">Helps you take action based on name using the same script</span></span> |
| <span data-ttu-id="3fe13-166">FailoverType</span><span class="sxs-lookup"><span data-stu-id="3fe13-166">FailoverType</span></span> |<span data-ttu-id="3fe13-167">Yük devretme sınamasını olup olmadığını, planlı veya plansız belirtir.</span><span class="sxs-lookup"><span data-stu-id="3fe13-167">Specifies whether the failover is test, planned, or unplanned.</span></span> |
| <span data-ttu-id="3fe13-168">FailoverDirection</span><span class="sxs-lookup"><span data-stu-id="3fe13-168">FailoverDirection</span></span> |<span data-ttu-id="3fe13-169">Kurtarma birincil veya ikincil olup olmadığını belirtin</span><span class="sxs-lookup"><span data-stu-id="3fe13-169">Specify whether recovery is to primary or secondary</span></span> |
| <span data-ttu-id="3fe13-170">GroupID</span><span class="sxs-lookup"><span data-stu-id="3fe13-170">GroupID</span></span> |<span data-ttu-id="3fe13-171">Kurtarma planı içinde Grup numarası plan çalıştırırken tanımlayın</span><span class="sxs-lookup"><span data-stu-id="3fe13-171">Identify the group number within the recovery plan when the plan is running</span></span> |
| <span data-ttu-id="3fe13-172">VmMap</span><span class="sxs-lookup"><span data-stu-id="3fe13-172">VmMap</span></span> |<span data-ttu-id="3fe13-173">Dizi, gruptaki tüm sanal makineler</span><span class="sxs-lookup"><span data-stu-id="3fe13-173">Array of all the virtual machines in the group</span></span> |
| <span data-ttu-id="3fe13-174">VMMap anahtarı</span><span class="sxs-lookup"><span data-stu-id="3fe13-174">VMMap key</span></span> |<span data-ttu-id="3fe13-175">Her VM için benzersiz anahtar (GUID).</span><span class="sxs-lookup"><span data-stu-id="3fe13-175">Unique key (GUID) for each VM.</span></span> <span data-ttu-id="3fe13-176">Bu sanal makinenin VMM kimliği uygunsa aynıdır.</span><span class="sxs-lookup"><span data-stu-id="3fe13-176">It's the same as the VMM ID of the virtual machine where applicable.</span></span> |
| <span data-ttu-id="3fe13-177">Rol adı</span><span class="sxs-lookup"><span data-stu-id="3fe13-177">RoleName</span></span> |<span data-ttu-id="3fe13-178">Kurtarılacak Azure VM adı</span><span class="sxs-lookup"><span data-stu-id="3fe13-178">Name of the Azure VM that's being recovered</span></span> |
| <span data-ttu-id="3fe13-179">CloudServiceName</span><span class="sxs-lookup"><span data-stu-id="3fe13-179">CloudServiceName</span></span> |<span data-ttu-id="3fe13-180">Azure bulut hizmeti adı altında sanal makine oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="3fe13-180">Azure Cloud Service name under which the virtual machine is created.</span></span> |

<span data-ttu-id="3fe13-181">Bağlam VmMap anahtarında tanımlamak için ayrıca ASR VM özellikler sayfasına gidin ve VM GUID özelliğine bakın.</span><span class="sxs-lookup"><span data-stu-id="3fe13-181">To identify the VmMap Key in the context you could also go to the VM properties page in ASR and look at the VM GUID property.</span></span>

![](media/site-recovery-runbook-automation/13.png)

## <a name="author-an-automation-runbook"></a><span data-ttu-id="3fe13-182">Bir Otomasyon runbook'u Yaz</span><span class="sxs-lookup"><span data-stu-id="3fe13-182">Author an Automation runbook</span></span>
<span data-ttu-id="3fe13-183">Ön uç sanal makine üzerinde bağlantı noktası 80 açmak için runbook'u şimdi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3fe13-183">Now create the runbook to open port 80 on the front-end virtual machine.</span></span>

1. <span data-ttu-id="3fe13-184">Azure Otomasyonu hesabı adıyla yeni bir runbook oluşturmak **OpenPort80**</span><span class="sxs-lookup"><span data-stu-id="3fe13-184">Create a new runbook in the Azure Automation account with the name **OpenPort80**</span></span>

   ![](media/site-recovery-runbook-automation/14.png)
2. <span data-ttu-id="3fe13-185">Runbook yazarı görünümüne gidin ve taslak modunda girin.</span><span class="sxs-lookup"><span data-stu-id="3fe13-185">Navigate to the Author view of the runbook and enter the draft mode.</span></span>
3. <span data-ttu-id="3fe13-186">Kurtarma planı bağlamı olarak kullanmak için değişken ilk belirtin</span><span class="sxs-lookup"><span data-stu-id="3fe13-186">First specify the variable to use as the recovery plan context</span></span>

   ```
       param (
           [Object]$RecoveryPlanContext
       )

   ```
4. <span data-ttu-id="3fe13-187">Sonraki kimlik bilgisi ve abonelik adını kullanarak aboneliğine bağlanma</span><span class="sxs-lookup"><span data-stu-id="3fe13-187">Next connect to the subscription using the credential and subscription name</span></span>

   ```
       $Cred = Get-AutomationPSCredential -Name 'AzureCredential'

       # Connect to Azure
       $AzureAccount = Add-AzureAccount -Credential $Cred
       $AzureSubscriptionName = Get-AutomationVariable –Name ‘AzureSubscriptionName’
       Select-AzureSubscription -SubscriptionName $AzureSubscriptionName
   ```

   <span data-ttu-id="3fe13-188">Azure varlıklar – kullandığını unutmayın **AzureCredential** ve **AzureSubscriptionName** burada.</span><span class="sxs-lookup"><span data-stu-id="3fe13-188">Note that you use the Azure assets – **AzureCredential** and **AzureSubscriptionName** here.</span></span>
5. <span data-ttu-id="3fe13-189">Artık uç nokta ayrıntılarını ve uç noktayı kullanıma sunmak istediğiniz sanal makine GUID belirtin.</span><span class="sxs-lookup"><span data-stu-id="3fe13-189">Now specify the endpoint details and the GUID of the virtual machine for which you want to expose the endpoint.</span></span> <span data-ttu-id="3fe13-190">Bu, ön uç sanal makine durumda.</span><span class="sxs-lookup"><span data-stu-id="3fe13-190">In this case the front-end virtual machine.</span></span>

   ```
       # Specify the parameters to be used by the script
       $AEProtocol = "TCP"
       $AELocalPort = 80
       $AEPublicPort = 80
       $AEName = "Port 80 for HTTP"
       $VMGUID = "7a1069c6-c1d6-49c5-8c5d-33bfce8dd183"
   ```

   <span data-ttu-id="3fe13-191">Bu, Azure uç noktası protokolü, VM'de yerel bağlantı noktası ve eşlenen ortak bağlantı noktasını belirtir.</span><span class="sxs-lookup"><span data-stu-id="3fe13-191">This specifies the Azure endpoint protocol, local port on the VM and its mapped public port.</span></span> <span data-ttu-id="3fe13-192">Bu değişkenler VM'ler için uç noktaları ekleme Azure komutları gerekli parametrelerdir.</span><span class="sxs-lookup"><span data-stu-id="3fe13-192">These variables are parameters     required by the Azure commands that add endpoints to VMs.</span></span> <span data-ttu-id="3fe13-193">VMGUID üzerinde çalışması için gereken sanal makine GUID tutar.</span><span class="sxs-lookup"><span data-stu-id="3fe13-193">The VMGUID holds the GUID of the virtual machine you need to operate on.</span></span>
6. <span data-ttu-id="3fe13-194">Komut dosyası şimdi bağlam için belirtilen VM GUID ayıklayın ve tarafından başvurulan sanal makineye bir uç nokta oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3fe13-194">The script will now extract the context for the given VM GUID and create an endpoint on the virtual machine referenced by it.</span></span>

   ```
       #Read the VM GUID from the context
       $VM = $RecoveryPlanContext.VmMap.$VMGUID

       if ($VM -ne $null)
       {
           # Invoke pipeline commands within an InlineScript

           $EndpointStatus = InlineScript {
               # Invoke the necessary pipeline commands to add a Azure Endpoint to a specified Virtual Machine
               # Commands include: Get-AzureVM | Add-AzureEndpoint | Update-AzureVM (including parameters)

               $Status = Get-AzureVM -ServiceName $Using:VM.CloudServiceName -Name $Using:VM.RoleName | `
                   Add-AzureEndpoint -Name $Using:AEName -Protocol $Using:AEProtocol -PublicPort $Using:AEPublicPort -LocalPort $Using:AELocalPort | `
                   Update-AzureVM
               Write-Output $Status
           }
       }
   ```
7. <span data-ttu-id="3fe13-195">Tamamlandığında, Yayımla isabet ![](media/site-recovery-runbook-automation/20.png) , komut yürütme için kullanılabilir olmasını sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="3fe13-195">Once this is complete, hit Publish ![](media/site-recovery-runbook-automation/20.png) to allow your script to be available for execution.</span></span>

<span data-ttu-id="3fe13-196">Tam komut dosyası başvuru için aşağıda verilmiştir</span><span class="sxs-lookup"><span data-stu-id="3fe13-196">The complete script is given below for your reference</span></span>

```
  workflow OpenPort80
  {
    param (
        [Object]$RecoveryPlanContext
    )

    $Cred = Get-AutomationPSCredential -Name 'AzureCredential'

    # Connect to Azure
    $AzureAccount = Add-AzureAccount -Credential $Cred
    $AzureSubscriptionName = Get-AutomationVariable –Name ‘AzureSubscriptionName’
    Select-AzureSubscription -SubscriptionName $AzureSubscriptionName

    # Specify the parameters to be used by the script
    $AEProtocol = "TCP"
    $AELocalPort = 80
    $AEPublicPort = 80
    $AEName = "Port 80 for HTTP"
    $VMGUID = "7a1069c6-c1d6-49c5-8c5d-33bfce8dd183"

    #Read the VM GUID from the context
    $VM = $RecoveryPlanContext.VmMap.$VMGUID

    if ($VM -ne $null)
    {
        # Invoke pipeline commands within an InlineScript

        $EndpointStatus = InlineScript {
            # Invoke the necessary pipeline commands to add an Azure Endpoint to a specified Virtual Machine
            # This set of commands includes: Get-AzureVM | Add-AzureEndpoint | Update-AzureVM (including necessary parameters)

            $Status = Get-AzureVM -ServiceName $Using:VM.CloudServiceName -Name $Using:VM.RoleName | `
                Add-AzureEndpoint -Name $Using:AEName -Protocol $Using:AEProtocol -PublicPort $Using:AEPublicPort -LocalPort $Using:AELocalPort | `
                Update-AzureVM
            Write-Output $Status
        }
    }
  }
```

## <a name="add-the-script-to-the-recovery-plan"></a><span data-ttu-id="3fe13-197">Komut dosyası kurtarma planına ekleyin</span><span class="sxs-lookup"><span data-stu-id="3fe13-197">Add the script to the recovery plan</span></span>
<span data-ttu-id="3fe13-198">Komut dosyası hazır olduktan sonra daha önce oluşturduğunuz kurtarma planına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3fe13-198">Once the script is ready, you can add it to the recovery plan that you created earlier.</span></span>

1. <span data-ttu-id="3fe13-199">Oluşturduğunuz kurtarma planında, Grup 2 sonra bir komut dosyası eklemek seçin.</span><span class="sxs-lookup"><span data-stu-id="3fe13-199">In the recovery plan you created, choose to add a script after the group 2.</span></span> ![](media/site-recovery-runbook-automation/15.png)
2. <span data-ttu-id="3fe13-200">Bir komut dosyası adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="3fe13-200">Specify a script name.</span></span> <span data-ttu-id="3fe13-201">Yalnızca kurtarma planı içinde gösteren için bu komut için bir kolay ad budur.</span><span class="sxs-lookup"><span data-stu-id="3fe13-201">This is just a friendly name for this script for showing within the Recovery plan.</span></span>
3. <span data-ttu-id="3fe13-202">Azure'a yük devretme betiği – Azure Automation hesabı adını seçin.</span><span class="sxs-lookup"><span data-stu-id="3fe13-202">In the failover to Azure script – Select the Azure Automation Account name.</span></span>
4. <span data-ttu-id="3fe13-203">Azure Runbook'larda yazdığınız runbook'u seçin.</span><span class="sxs-lookup"><span data-stu-id="3fe13-203">In the Azure Runbooks, select the runbook you authored.</span></span>

![](media/site-recovery-runbook-automation/16.png)

## <a name="primary-side-scripts"></a><span data-ttu-id="3fe13-204">Birincil tarafı betikler</span><span class="sxs-lookup"><span data-stu-id="3fe13-204">Primary side scripts</span></span>
<span data-ttu-id="3fe13-205">Bir yük devretme Azure yürütülürken birincil tarafı komut yürütmek seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3fe13-205">When you are executing a failover to Azure, you can also choose to execute primary side scripts.</span></span> <span data-ttu-id="3fe13-206">Bu komut dosyaları, yük devretme sırasında VMM sunucusunda çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="3fe13-206">These scripts will run on the VMM server during failover.</span></span>
<span data-ttu-id="3fe13-207">Birincil tarafı komut dosyaları yalnızca yalnızca Kapatma öncesi için kullanılabilir ve kapatma aşamaları gönderin.</span><span class="sxs-lookup"><span data-stu-id="3fe13-207">Primary side scripts are only available only for pre-shutdown and post shutdown stages.</span></span> <span data-ttu-id="3fe13-208">Birincil sitenin bir olağanüstü durum sağlar, normal olarak kullanılamaz hale gelmesine bekliyoruz olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="3fe13-208">This is because we expect the primary site to be typically unavailable when a disaster strikes.</span></span>
<span data-ttu-id="3fe13-209">Yalnızca birincil site işlemleri için kabul ederseniz planlanmamış bir yük devretme sırasında birincil tarafı komut dosyalarını çalıştırmak deneyecek.</span><span class="sxs-lookup"><span data-stu-id="3fe13-209">During an unplanned failover, only if you opt in for primary site operations, it will attempt to run the primary side scripts.</span></span> <span data-ttu-id="3fe13-210">Bunlar erişilebilir değil veya zaman aşımı, sanal makineler kurtarmak yük devretme devam edecek varsa.</span><span class="sxs-lookup"><span data-stu-id="3fe13-210">If they are not reachable or timeout, the failover will continue to recover the virtual machines.</span></span>
<span data-ttu-id="3fe13-211">Birincil tarafı komut dosyaları, yük devretme Azure sırasında Azure için - korumalı VMM olmadan VMware/fiziksel/Hyper-v siteleri için beklemediğiniz kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="3fe13-211">Primary side scripts are un-available for VMware/Physical/Hyper-v Sites without VMM protected to Azure - while you failover to Azure.</span></span>
<span data-ttu-id="3fe13-212">Ancak, ne zaman, azure'dan şirket içi, birincil tarafı komut dosyaları (Runbook'lar) VMware dışındaki tüm hedefler için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="3fe13-212">However, when you failback from Azure to on-premises, primary side scripts (Runbooks) can be used for all targets except VMware.</span></span>

## <a name="test-the-recovery-plan"></a><span data-ttu-id="3fe13-213">Kurtarma planı test</span><span class="sxs-lookup"><span data-stu-id="3fe13-213">Test the recovery plan</span></span>
<span data-ttu-id="3fe13-214">Runbook bir test yük devretme başlatın ve istemciyi kullanımda görme plana ekledikten sonra.</span><span class="sxs-lookup"><span data-stu-id="3fe13-214">Once you have added the runbook to the plan you can initiate a test failover and see it in action.</span></span> <span data-ttu-id="3fe13-215">Ayrıca, uygulamanızı ve herhangi bir hata olduğundan emin olmak için kurtarma planını test etmek için bir yük devretme testi çalıştırmak için her zaman önerilir.</span><span class="sxs-lookup"><span data-stu-id="3fe13-215">It is always recommended to run a test failover to test your application and the recovery plan to ensure that there are no errors.</span></span>

1. <span data-ttu-id="3fe13-216">Kurtarma planı seçin ve bir test yük devretme başlatın.</span><span class="sxs-lookup"><span data-stu-id="3fe13-216">Select the recovery plan and initiate a test failover.</span></span>
2. <span data-ttu-id="3fe13-217">Plan yürütme sırasında runbook yürütüldü olup olmadığını veya durumunu aracılığıyla değil görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3fe13-217">During the plan execution, you can see whether the runbook has executed or not via its status.</span></span>

   ![](media/site-recovery-runbook-automation/17.png)
3. <span data-ttu-id="3fe13-218">Azure Otomasyonu işleri sayfasında runbook için ayrıntılı runbook yürütme durumu de görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3fe13-218">You can also see the detailed runbook execution status on the Azure Automation jobs page for the runbook.</span></span>

   ![](media/site-recovery-runbook-automation/18.png)
4. <span data-ttu-id="3fe13-219">Yük devretme tamamlandığında runbook yürütme sonucu dışında yürütme başarılı olup olmadığını veya Azure sanal makinesi sayfasını ziyaret ve uç noktada arayarak tarafından görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3fe13-219">After the failover completes, apart from the runbook execution result, you can see whether the execution is successful or not by visiting the Azure virtual machine page and looking at the endpoints.</span></span>

![](media/site-recovery-runbook-automation/19.png)

## <a name="sample-scripts"></a><span data-ttu-id="3fe13-220">Örnek komut dosyaları</span><span class="sxs-lookup"><span data-stu-id="3fe13-220">Sample scripts</span></span>
<span data-ttu-id="3fe13-221">Vazgeçtik sırada Bu öğreticide bir Azure sanal makineye bir uç nokta ekleme görev kullanılan bir genellikle otomatikleştirme, bir dizi Azure otomasyonu kullanarak diğer güçlü Otomasyon görevi yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3fe13-221">While we walked through automating one commonly used task of adding an endpoint to an Azure virtual machine in this tutorial, you could do a number of other powerful automation tasks using Azure automation.</span></span> <span data-ttu-id="3fe13-222">Microsoft ve Azure Automation topluluk yardımcı olabilecek örnek runbook'lar kendi çözümleri ve daha büyük bir otomatikleştirme görevleri için yapı taşı olarak kullanabileceğiniz yardımcı programı runbook'lar oluşturmaya başlamak sağlar.</span><span class="sxs-lookup"><span data-stu-id="3fe13-222">Microsoft and the Azure Automation community provide sample runbooks which can help you get started creating your own solutions, and utility runbooks, which you can use as building blocks for larger automation tasks.</span></span> <span data-ttu-id="3fe13-223">Galeriden kullanmaya başlamak ve Azure Site Recovery kullanarak uygulamalarınızı için güçlü tek tıklatmayla kurtarma planları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3fe13-223">Start using them from the gallery and build  powerful one-click recovery plans for your applications using Azure Site Recovery.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3fe13-224">Ek Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="3fe13-224">Additional Resources</span></span>
[<span data-ttu-id="3fe13-225">Azure Otomasyonu genel bakış</span><span class="sxs-lookup"><span data-stu-id="3fe13-225">Azure Automation Overview</span></span>](http://msdn.microsoft.com/library/azure/dn643629.aspx "Azure Otomasyonu genel bakış")

[<span data-ttu-id="3fe13-226">Örnek Azure Otomasyon betikleri</span><span class="sxs-lookup"><span data-stu-id="3fe13-226">Sample Azure Automation Scripts</span></span>](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=User&f\[0\].Value=SC%20Automation%20Product%20Team&f\[0\].Text=SC%20Automation%20Product%20Team "örnek Azure Otomasyonu komutlar")
