---
title: "aaa\"Düzelt Otomasyon runbook'ları ile Azure VM uyarıları | Microsoft Docs\""
description: "Bu makalede Azure Otomasyon çalışma kitabı ile nasıl toointegrate Azure sanal makine uyarıları gösterir ve sorunları otomatik çözmek"
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 1f7baa7f-7283-4a4f-9385-3f5cd1062c7f
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/14/2016
ms.author: csand;magoedte
ms.openlocfilehash: c226368a5c4c51fbfb331f4b97f7f2f239e701c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---remediate-azure-vm-alerts"></a><span data-ttu-id="ab932-103">Azure otomasyonu senaryosu - Azure VM uyarıları Düzelt</span><span class="sxs-lookup"><span data-stu-id="ab932-103">Azure Automation scenario - remediate Azure VM alerts</span></span>
<span data-ttu-id="ab932-104">Azure Otomasyonu ve Azure sanal makineleri tooconfigure sanal makine (VM) uyarıları toorun Otomasyon runbook'ları sağlayan yeni bir özellik yayımlandı.</span><span class="sxs-lookup"><span data-stu-id="ab932-104">Azure Automation and Azure Virtual Machines have released a new feature allowing you tooconfigure Virtual Machine (VM) alerts toorun Automation runbooks.</span></span> <span data-ttu-id="ab932-105">Bu yeni özellik sağlar tooautomatically yanıt tooVM uyarıları, yeniden başlatma veya durdurma hello VM gibi standart düzeltme gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="ab932-105">This new capability allows you tooautomatically perform standard remediation in response tooVM alerts, like restarting or stopping hello VM.</span></span>

<span data-ttu-id="ab932-106">Daha önce VM uyarı kuralı oluşturma sırasında çok girişiminizin[Otomasyonu Web kancası belirtin](https://azure.microsoft.com/blog/using-azure-automation-to-take-actions-on-azure-alerts/) hello uyarının her sipariş toorun hello runbook tooa runbook'ta.</span><span class="sxs-lookup"><span data-stu-id="ab932-106">Previously, during VM alert rule creation you were able too[specify an Automation webhook](https://azure.microsoft.com/blog/using-azure-automation-to-take-actions-on-azure-alerts/) tooa runbook in order toorun hello runbook whenever hello alert triggered.</span></span> <span data-ttu-id="ab932-107">Ancak, bu, toodo hello iş hello runbook oluşturma, hello runbook için hello Web kancası oluşturma ve ardından kopyalama ve uyarı kuralı oluşturma sırasında hello Web kancası yapıştırma gereklidir.</span><span class="sxs-lookup"><span data-stu-id="ab932-107">However, this required you toodo hello work of creating hello runbook, creating hello webhook for hello runbook, and then copying and pasting hello webhook during alert rule creation.</span></span> <span data-ttu-id="ab932-108">Bu yeni sürümle birlikte, çünkü, doğrudan bir runbook bir listeden uyarı kuralı oluşturma sırasında seçebilirsiniz ve hello runbook'u çalıştırmak veya kolayca bir hesap oluşturmasını bir Otomasyon hesabı seçebilir hello işlem daha kolay olur.</span><span class="sxs-lookup"><span data-stu-id="ab932-108">With this new release, hello process is much easier because you can directly choose a runbook from a list during alert rule creation, and you can choose an Automation account which will run hello runbook or easily create an account.</span></span>

<span data-ttu-id="ab932-109">Bu makalede, biz ne kadar kolay bir Azure VM uyarı oluşturan tooset olduğunu gösterir ve hello uyarıyı tetikleyen her bir Otomasyon runbook toorun yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="ab932-109">In this article, we will show you how easy it is tooset up an Azure VM alert and configure an Automation runbook toorun whenever hello alert triggers.</span></span> <span data-ttu-id="ab932-110">Örnek senaryolar hello bellek kullanımı hello VM bellek sızıntısı ile tooan uygulama nedeniyle bazı eşiğini aştığında bir VM'yi yeniden başlatırken veya hello CPU kullanıcı zamanı %1 son bir saat boyunca ve kullanımda olmadığında bir VM durdurma içerir.</span><span class="sxs-lookup"><span data-stu-id="ab932-110">Example scenarios include restarting a VM when hello memory usage exceeds some threshold due tooan application on hello VM with a memory leak, or stopping a VM when hello CPU user time has been below 1% for past hour and is not in use.</span></span> <span data-ttu-id="ab932-111">Ayrıca nasıl hello oluşturma otomatik açıklayacağız bir hizmet asıl, Automation hesabı Azure uyarı düzeltme runbook'larda hello kullanımını basitleştirir.</span><span class="sxs-lookup"><span data-stu-id="ab932-111">We’ll also explain how hello automated creation of a service principal in your Automation account simplifies hello use of runbooks in Azure alert remediation.</span></span>

## <a name="create-an-alert-on-a-vm"></a><span data-ttu-id="ab932-112">Bir VM üzerinde bir uyarı oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="ab932-112">Create an alert on a VM</span></span>
<span data-ttu-id="ab932-113">Eşiğini sağlandığında adımları tooconfigure bir runbook bir uyarı toolaunch aşağıdaki hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="ab932-113">Perform hello following steps tooconfigure an alert toolaunch a runbook when its threshold has been met.</span></span>

> [!NOTE]
> <span data-ttu-id="ab932-114">Bu sürümle birlikte, yalnızca V2 sanal makineler ve destek için Klasik VM'ler yakında eklenecek destekliyoruz.</span><span class="sxs-lookup"><span data-stu-id="ab932-114">With this release, we only support V2 virtual machines and support for classic VMs will be added soon.</span></span>  
> 
> 

1. <span data-ttu-id="ab932-115">Oturum toohello Azure portal ve tıklatın **sanal makineleri**.</span><span class="sxs-lookup"><span data-stu-id="ab932-115">Log in toohello Azure portal and click **Virtual Machines**.</span></span>  
2. <span data-ttu-id="ab932-116">Sanal makinelerinizi birini seçin.</span><span class="sxs-lookup"><span data-stu-id="ab932-116">Select one of your virtual machines.</span></span>  <span data-ttu-id="ab932-117">Merhaba sanal makine Pano dikey görünür hello ve **ayarları** dikey tooits sağ.</span><span class="sxs-lookup"><span data-stu-id="ab932-117">hello virtual machine dashboard blade will appear and hello **Settings** blade tooits right.</span></span>  
3. <span data-ttu-id="ab932-118">Merhaba gelen **ayarları** hello izleme bölümü seçin altında dikey **uyarı kuralları**.</span><span class="sxs-lookup"><span data-stu-id="ab932-118">From hello **Settings** blade, under hello Monitoring section select **Alert rules**.</span></span>
4. <span data-ttu-id="ab932-119">Merhaba üzerinde **uyarı kuralları** dikey penceresinde tıklatın **uyarı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="ab932-119">On hello **Alert rules** blade, click **Add alert**.</span></span>

<span data-ttu-id="ab932-120">Merhaba açılır **uyarı kuralı eklemek** burada hello uyarı hello koşulları yapılandırmak ve aşağıdakilerden birini veya bu seçeneklerin tümü arasında seçin dikey: e-posta toosomeone göndermek, bir Web kancası tooforward hello uyarı tooanother sistemi kullanmak ve/veya bir Otomasyon runbook'u yanıt girişimi tooremediate hello sorunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ab932-120">This opens up hello **Add an alert rule** blade, where you can configure hello conditions for hello alert and choose among one or all of these options: send email toosomeone, use a webhook tooforward hello alert tooanother system, and/or run an Automation runbook in response attempt tooremediate hello issue.</span></span>

## <a name="configure-a-runbook"></a><span data-ttu-id="ab932-121">Bir runbook yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ab932-121">Configure a runbook</span></span>
<span data-ttu-id="ab932-122">tooconfigure hello VM uyarı eşiği karşılandığında, bir runbook toorun seçin **Otomasyon Runbook'u**.</span><span class="sxs-lookup"><span data-stu-id="ab932-122">tooconfigure a runbook toorun when hello VM alert threshold is met, select **Automation Runbook**.</span></span> <span data-ttu-id="ab932-123">Merhaba, **runbook yapılandırma** dikey penceresinde hello runbook toorun ve hello Otomasyon hesabı toorun hello runbook'ta seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ab932-123">In hello **Configure runbook** blade, you can select hello runbook toorun and hello Automation account toorun hello runbook in.</span></span>

![Otomasyon runbook yapılandırma ve yeni bir Otomasyon hesabı oluşturma](media/automation-azure-vm-alert-integration/ConfigureRunbookNewAccount.png)

> [!NOTE]
> <span data-ttu-id="ab932-125">Bu sürüm için hello hizmet sağlayan – üç runbook'lardan VM yeniden başlatma, durdurma VM veya kaldırma VM seçebilirsiniz (silme).</span><span class="sxs-lookup"><span data-stu-id="ab932-125">For this release you can choose from three runbooks that hello service provides – Restart VM, Stop VM, or Remove VM (delete it).</span></span>  <span data-ttu-id="ab932-126">diğer runbook'lar özelliği tooselect hello veya kendi runbook'ları biri gelecekteki bir sürümde kullanılabilir olacaktır.</span><span class="sxs-lookup"><span data-stu-id="ab932-126">hello ability tooselect other runbooks or one of your own runbooks will be available in a future release.</span></span>
> 
> 

![Runbook'ları toochoose gelen](media/automation-azure-vm-alert-integration/RunbooksToChoose.png)

<span data-ttu-id="ab932-128">Merhaba üç kullanılabilir runbook'ları birini seçtikten sonra hello **Otomasyon hesabı** aşağı açılan listesi görüntülenir ve bir Otomasyon seçebilirsiniz hesap hello runbook olarak çalışır.</span><span class="sxs-lookup"><span data-stu-id="ab932-128">After you select one of hello three available runbooks, hello **Automation account** drop-down list appears and you can select an automation account hello runbook will run as.</span></span> <span data-ttu-id="ab932-129">Runbook'lar gerek toorun hello bağlamındaki bir [Otomasyon hesabı](automation-security-overview.md) Azure aboneliğinizde olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="ab932-129">Runbooks need toorun in hello context of an [Automation account](automation-security-overview.md) that is in your Azure subscription.</span></span> <span data-ttu-id="ab932-130">Önceden oluşturulmuş veya sizin için oluşturulan yeni bir Otomasyon hesabı olabilir bir Otomasyon hesabı seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ab932-130">You can select an Automation account that you already created, or you can have a new Automation account created for you.</span></span>

<span data-ttu-id="ab932-131">sağlanan hello runbook'ları tooAzure hizmet sorumlusunu kullanarak kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="ab932-131">hello runbooks that are provided authenticate tooAzure using a service principal.</span></span> <span data-ttu-id="ab932-132">Toorun hello runbook, var olan Otomasyon hesaplarından birini seçerseniz, otomatik olarak hello hizmet asıl sizin için oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="ab932-132">If you choose toorun hello runbook in one of your existing Automation accounts, we will automatically create hello service principal for you.</span></span> <span data-ttu-id="ab932-133">Yeni bir Otomasyon hesabı toocreate seçerseniz, ardından otomatik olarak hello hesabı ve hello hizmet sorumlusu oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="ab932-133">If you choose toocreate a new Automation account, then we will automatically create hello account and hello service principal.</span></span> <span data-ttu-id="ab932-134">Her iki durumda da, iki varlıklar da hello Otomasyon hesabı – adlı bir sertifika varlığı oluşturulacak **AzureRunAsCertificate** ve adlı bir bağlantı varlığı **AzureRunAsConnection**.</span><span class="sxs-lookup"><span data-stu-id="ab932-134">In both cases, two assets will also be created in hello Automation account – a certificate asset named **AzureRunAsCertificate** and a connection asset named **AzureRunAsConnection**.</span></span> <span data-ttu-id="ab932-135">Merhaba runbook'ları kullanacak **AzureRunAsConnection** sipariş tooperform hello Yönetimi eylem hello VM karşı Azure ile tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="ab932-135">hello runbooks will use **AzureRunAsConnection** tooauthenticate with Azure in order tooperform hello management action against hello VM.</span></span>

> [!NOTE]
> <span data-ttu-id="ab932-136">Merhaba hizmet sorumlusu hello abonelik kapsamında oluşturulan ve hello katkıda bulunan rolü atanır.</span><span class="sxs-lookup"><span data-stu-id="ab932-136">hello service principal is created in hello subscription scope and is assigned hello Contributor role.</span></span> <span data-ttu-id="ab932-137">Bu rol, sırayla hello hesap toohave izin toorun Otomasyon runbook'ları toomanage Azure VM'ler için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="ab932-137">This role is required in order for hello account toohave permission toorun Automation runbooks toomanage Azure VMs.</span></span>  <span data-ttu-id="ab932-138">Merhaba oluşturulmasını Automaton hesabı ve/veya hizmet sorumlusu tek seferlik bir olaydır.</span><span class="sxs-lookup"><span data-stu-id="ab932-138">hello creation of an Automaton account and/or service principal is a one-time event.</span></span> <span data-ttu-id="ab932-139">Oluşturulduktan sonra diğer Azure VM uyarılar için bu hesabı toorun runbook'ları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ab932-139">Once they are created, you can use that account toorun runbooks for other Azure VM alerts.</span></span>
> 
> 

<span data-ttu-id="ab932-140">Tıkladığınızda **Tamam** hello uyarı yapılandırılır ve hello seçeneği toocreate yeni bir Otomasyon hesabı seçtiyseniz, bu hello hizmet sorumlusu birlikte oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="ab932-140">When you click **OK** hello alert is configured and if you selected hello option toocreate a new Automation account, it is created along with hello service principal.</span></span>  <span data-ttu-id="ab932-141">Bu işlem birkaç saniye sürebilir toocomplete.</span><span class="sxs-lookup"><span data-stu-id="ab932-141">This can take a few seconds toocomplete.</span></span>  

![Yapılandırılmakta Runbook](media/automation-azure-vm-alert-integration/RunbookBeingConfigured.png)

<span data-ttu-id="ab932-143">Merhaba Yapılandırma tamamlandıktan sonra hello adını hello görünür hello runbook görürsünüz **uyarı kuralı eklemek** dikey.</span><span class="sxs-lookup"><span data-stu-id="ab932-143">After hello configuration is completed you will see hello name of hello runbook appear in hello **Add an alert rule** blade.</span></span>

![Yapılandırılmış Runbook](media/automation-azure-vm-alert-integration/RunbookConfigured.png)

<span data-ttu-id="ab932-145">Tıklatın **Tamam** hello içinde **uyarı kuralı eklemek** dikey penceresinde ve hello uyarı kuralı oluşturulur ve hello sanal makine çalışır durumda ise etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="ab932-145">Click **OK** in hello **Add an alert rule** blade and hello alert rule will be created and activate if hello virtual machine is in a running state.</span></span>

### <a name="enable-or-disable-a-runbook"></a><span data-ttu-id="ab932-146">Etkinleştirmek veya devre dışı bir runbook</span><span class="sxs-lookup"><span data-stu-id="ab932-146">Enable or disable a runbook</span></span>
<span data-ttu-id="ab932-147">Bir uyarı için yapılandırılmış bir runbook'unuz varsa, onu hello runbook yapılandırma kaldırmadan devre dışı bırakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ab932-147">If you have a runbook configured for an alert, you can disable it without removing hello runbook configuration.</span></span> <span data-ttu-id="ab932-148">Bu çalışan tookeep hello uyarı verir ve belki de hello uyarı kuralları bazılarını test ve daha sonra hello runbook yeniden etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="ab932-148">This allows you tookeep hello alert running and perhaps test some of hello alert rules and then later re-enable hello runbook.</span></span>

## <a name="create-a-runbook-that-works-with-an-azure-alert"></a><span data-ttu-id="ab932-149">Azure uyarı ile çalışan bir runbook'u oluşturma</span><span class="sxs-lookup"><span data-stu-id="ab932-149">Create a runbook that works with an Azure alert</span></span>
<span data-ttu-id="ab932-150">Bir Azure uyarı kuralının bir parçası bir runbook seçtiğinizde hello runbook toohave mantığında tooit geçirilen toomanage hello uyarı verileri gerekir.</span><span class="sxs-lookup"><span data-stu-id="ab932-150">When you choose a runbook as part of an Azure alert rule, hello runbook needs toohave logic in it toomanage hello alert data that is passed tooit.</span></span>  <span data-ttu-id="ab932-151">Bir runbook bir uyarı kuralı yapılandırıldığında, bir Web kancası hello runbook için oluşturulur; her zaman hello uyarı Tetikleyicileri runbook kullanılan toostart hello sonra o Web kancası olur.</span><span class="sxs-lookup"><span data-stu-id="ab932-151">When a runbook is configured in an alert rule, a webhook is created for hello runbook; that webhook is then used toostart hello runbook each time hello alert triggers.</span></span>  <span data-ttu-id="ab932-152">Merhaba gerçek çağrısını toostart hello runbook bir HTTP POST isteği toohello Web kancası URL'dir.</span><span class="sxs-lookup"><span data-stu-id="ab932-152">hello actual call toostart hello runbook is an HTTP POST request toohello webhook URL.</span></span> <span data-ttu-id="ab932-153">Merhaba POST isteği Hello gövdesini yararlı özellikleri ilgili toohello uyarı içeren bir JSON biçiminin nesnesi içerir.</span><span class="sxs-lookup"><span data-stu-id="ab932-153">hello body of hello POST request contains a JSON-formated object that contains useful properties related toohello alert.</span></span>  <span data-ttu-id="ab932-154">Aşağıda görüldüğü gibi hello uyarı verileri Subscriptionıd, resourceGroupName, resourceName ve resourceType gibi ayrıntıları içerir.</span><span class="sxs-lookup"><span data-stu-id="ab932-154">As you can see below, hello alert data contains details like subscriptionID, resourceGroupName, resourceName, and resourceType.</span></span>

### <a name="example-of-alert-data"></a><span data-ttu-id="ab932-155">Uyarı veri örneği</span><span class="sxs-lookup"><span data-stu-id="ab932-155">Example of Alert data</span></span>
```
{
    "WebhookName": "AzureAlertTest",
    "RequestBody": "{
    \"status\":\"Activated\",
    \"context\": {
        \"id\":\"/subscriptions/<subscriptionId>/resourceGroups/MyResourceGroup/providers/microsoft.insights/alertrules/AlertTest\",
        \"name\":\"AlertTest\",
        \"description\":\"\",
        \"condition\": {
            \"metricName\":\"CPU percentage guest OS\",
            \"metricUnit\":\"Percent\",
            \"metricValue\":\"4.26337916666667\",
            \"threshold\":\"1\",
            \"windowSize\":\"60\",
            \"timeAggregation\":\"Average\",
            \"operator\":\"GreaterThan\"},
        \"subscriptionId\":\<subscriptionID> \",
        \"resourceGroupName\":\"TestResourceGroup\",
        \"timestamp\":\"2016-04-24T23:19:50.1440170Z\",
        \"resourceName\":\"TestVM\",
        \"resourceType\":\"microsoft.compute/virtualmachines\",
        \"resourceRegion\":\"westus\",
        \"resourceId\":\"/subscriptions/<subscriptionId>/resourceGroups/TestResourceGroup/providers/Microsoft.Compute/virtualMachines/TestVM\",
        \"portalLink\":\"https://portal.azure.com/#resource/subscriptions/<subscriptionId>/resourceGroups/TestResourceGroup/providers/Microsoft.Compute/virtualMachines/TestVM\"
        },
    \"properties\":{}
    }",
    "RequestHeader": {
        "Connection": "Keep-Alive",
        "Host": "<webhookURL>"
    }
}
```

<span data-ttu-id="ab932-156">Merhaba Otomasyonu Web kancası hizmeti hello HTTP POST aldığında hello uyarı verileri ayıklar ve toohello runbook hello WebhookData runbook giriş parametresi geçirir.</span><span class="sxs-lookup"><span data-stu-id="ab932-156">When hello Automation webhook service receives hello HTTP POST it extracts hello alert data and passes it toohello runbook in hello WebhookData runbook input parameter.</span></span>  <span data-ttu-id="ab932-157">Nasıl toouse WebhookData parametresi hello hello uyarı verileri ayıklamak ve toomanage hello hello uyarıyı tetikleyen Azure kaynak kullanmak gösteren bir örnek runbook aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="ab932-157">Below is a sample runbook that shows how toouse hello WebhookData parameter and extract hello alert data and use it toomanage hello Azure resource that triggered hello alert.</span></span>

### <a name="example-runbook"></a><span data-ttu-id="ab932-158">Örnek runbook</span><span class="sxs-lookup"><span data-stu-id="ab932-158">Example runbook</span></span>
```
#  This runbook will restart an ARM (V2) VM in response tooan Azure VM alert.

[OutputType("PSAzureOperationResponse")]

param ( [object] $WebhookData )

if ($WebhookData)
{
    # Get hello data object from WebhookData
    $WebhookBody = (ConvertFrom-Json -InputObject $WebhookData.RequestBody)

    # Assure that hello alert status is 'Activated' (alert condition went from false tootrue)
    # and not 'Resolved' (alert condition went from true toofalse)
    if ($WebhookBody.status -eq "Activated")
    {
        # Get hello info needed tooidentify hello VM
        $AlertContext = [object] $WebhookBody.context
        $ResourceName = $AlertContext.resourceName
        $ResourceType = $AlertContext.resourceType
        $ResourceGroupName = $AlertContext.resourceGroupName
        $SubId = $AlertContext.subscriptionId

        # Assure that this is hello expected resource type
        Write-Verbose "ResourceType: $ResourceType"
        if ($ResourceType -eq "microsoft.compute/virtualmachines")
        {
            # This is an ARM (V2) VM

            # Authenticate tooAzure with service principal and certificate
            $ConnectionAssetName = "AzureRunAsConnection"
            $Conn = Get-AutomationConnection -Name $ConnectionAssetName
            if ($Conn -eq $null) {
                throw "Could not retrieve connection asset: $ConnectionAssetName. Check that this asset exists in hello Automation account."
            }
            Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint | Write-Verbose
            Set-AzureRmContext -SubscriptionId $SubId -ErrorAction Stop | Write-Verbose

            # Restart hello VM
            Restart-AzureRmVM -Name $ResourceName -ResourceGroupName $ResourceGroupName
        } else {
            Write-Error "$ResourceType is not a supported resource type for this runbook."
        }
    } else {
        # hello alert status was not 'Activated' so no action taken
        Write-Verbose ("No action taken. Alert status: " + $WebhookBody.status)
    }
} else {
    Write-Error "This runbook is meant toobe started from an Azure alert only."
}
```

## <a name="summary"></a><span data-ttu-id="ab932-159">Özet</span><span class="sxs-lookup"><span data-stu-id="ab932-159">Summary</span></span>
<span data-ttu-id="ab932-160">Azure VM temelinde bir uyarı yapılandırırken bir Otomasyon yapılandırma hello özelliği tooeasily şimdi sahip runbook tooautomatically hello uyarıyı tetikleyen zaman düzeltme eylemi gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="ab932-160">When you configure an alert on an Azure VM, you now have hello ability tooeasily configure an Automation runbook tooautomatically perform remediation action when hello alert triggers.</span></span> <span data-ttu-id="ab932-161">Bu sürüm için runbook'ları toorestart seçebilirsiniz, durdurmak veya uyarı senaryonuza bağlı olarak bir VM silme.</span><span class="sxs-lookup"><span data-stu-id="ab932-161">For this release, you can choose from runbooks toorestart, stop, or delete a VM depending on your alert scenario.</span></span> <span data-ttu-id="ab932-162">Bu uyarıyı tetikleyen olduğunda otomatik olarak gerçekleştirilecek hello eylemleri (bildirim, sorun giderme, düzeltme) kontrol burada senaryoları etkinleştirme yalnızca hello başlangıçtır.</span><span class="sxs-lookup"><span data-stu-id="ab932-162">This is just hello beginning of enabling scenarios where you control hello actions (notification, troubleshooting, remediation) that will be taken automatically when an alert triggers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ab932-163">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="ab932-163">Next Steps</span></span>
* <span data-ttu-id="ab932-164">Grafik runbook'ları ile çalışmaya tooget bakın [ilk grafik runbook Uygulamam](automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="ab932-164">tooget started with Graphical runbooks, see [My first graphical runbook](automation-first-runbook-graphical.md)</span></span>
* <span data-ttu-id="ab932-165">PowerShell iş akışı runbook'ları ile başlatılan tooget bakın [ilk PowerShell iş akışı runbook Uygulamam](automation-first-runbook-textual.md)</span><span class="sxs-lookup"><span data-stu-id="ab932-165">tooget started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span></span>
* <span data-ttu-id="ab932-166">runbook türleri, avantajları ve sınırlamaları, hakkında daha fazla toolearn bakın [Azure Automation runbook türleri](automation-runbook-types.md)</span><span class="sxs-lookup"><span data-stu-id="ab932-166">toolearn more about runbook types, their advantages and limitations, see [Azure Automation runbook types](automation-runbook-types.md)</span></span>

