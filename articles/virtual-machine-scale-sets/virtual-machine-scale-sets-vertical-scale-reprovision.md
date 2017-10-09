---
title: "aaaVertically ölçek Azure sanal makine ölçek kümeleri | Microsoft Docs"
description: "Nasıl toovertically ölçeklendirme bir sanal makine yanıt toomonitoring uyarılar Azure Automation"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: madhana
editor: 
tags: azure-resource-manager
ms.assetid: 16b17421-6b8f-483e-8a84-26327c44e9d3
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 08/03/2016
ms.author: guybo
ms.openlocfilehash: 1cc35a805b6a5742252a89c21588ca451ff547a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="vertical-autoscale-with-virtual-machine-scale-sets"></a><span data-ttu-id="62e93-103">Sanal makine ölçek kümeleri ile dikey otomatik ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="62e93-103">Vertical autoscale with Virtual Machine Scale sets</span></span>
<span data-ttu-id="62e93-104">Nasıl toovertically ölçeklendirme Azure bu makalede [sanal makine ölçek kümeleri](https://azure.microsoft.com/services/virtual-machine-scale-sets/) ile veya sağlama işleminin olmadan.</span><span class="sxs-lookup"><span data-stu-id="62e93-104">This article describes how toovertically scale Azure [Virtual Machine Scale Sets](https://azure.microsoft.com/services/virtual-machine-scale-sets/) with or without reprovisioning.</span></span> <span data-ttu-id="62e93-105">Dikey Ölçek kümelerinde olmayan vm'lere ölçekleme için çok başvuran[Azure Automation ile Azure sanal makine dikey olarak ölçeklendirmek](../virtual-machines/windows/vertical-scaling-automation.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="62e93-105">For vertical scaling of VMs which are not in scale sets, refer too[Vertically scale Azure virtual machine with Azure Automation](../virtual-machines/windows/vertical-scaling-automation.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="62e93-106">Dikey olarak da bilinen ölçeklendirme, *ölçeği* ve *ölçeklendirmeyi azaltın*, artan veya azalan yanıt tooa iş yükü sanal makine (VM) boyutları anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="62e93-106">Vertical scaling, also known as *scale up* and *scale down*, means increasing or decreasing virtual machine (VM) sizes in response tooa workload.</span></span> <span data-ttu-id="62e93-107">Bu karşılaştırma [yatay ölçekleme](virtual-machine-scale-sets-autoscale-overview.md), tooas ya da *ölçeğini* ve *içinde ölçeklendirmek*, VM'lerin sayısını hello hello iş yüküne bağlı olarak burada değiştirilemez.</span><span class="sxs-lookup"><span data-stu-id="62e93-107">Compare this with [horizontal scaling](virtual-machine-scale-sets-autoscale-overview.md), also referred tooas *scale out* and *scale in*, where hello number of VMs is altered depending on hello workload.</span></span>

<span data-ttu-id="62e93-108">Sağlama işleminin, mevcut bir VM'yi kaldırarak ve yeni bir tane ile değiştirerek anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="62e93-108">Reprovisioning means removing an existing VM and replacing it with a new one.</span></span> <span data-ttu-id="62e93-109">Artırın veya VM ölçek kümesindeki sanal makineleri hello boyutunu azaltın, bazı durumlarda, VM'ler varolan tooresize istediğiniz ve diğer durumlarda toodeploy gerekirken, verilerinizi korumak hello yeni boyutunu yeni VM'ler.</span><span class="sxs-lookup"><span data-stu-id="62e93-109">When you increase or decrease hello size of VMs in a VM Scale Set, in some cases you want tooresize existing VMs and retain your data, while in other cases you need toodeploy new VMs of hello new size.</span></span> <span data-ttu-id="62e93-110">Bu belge her iki durumda da kapsar.</span><span class="sxs-lookup"><span data-stu-id="62e93-110">This document covers both cases.</span></span>

<span data-ttu-id="62e93-111">Dikey ölçekleme durumlarda yararlı olabilir:</span><span class="sxs-lookup"><span data-stu-id="62e93-111">Vertical scaling can be useful when:</span></span>

* <span data-ttu-id="62e93-112">Sanal makineler üzerinde oluşturulmuş bir (örneğin sonları) altında kullanılan hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="62e93-112">A service built on virtual machines is under-utilized (for example at weekends).</span></span> <span data-ttu-id="62e93-113">Merhaba VM boyutunun azaltılması aylık maliyetlerini azaltabilir.</span><span class="sxs-lookup"><span data-stu-id="62e93-113">Reducing hello VM size can reduce monthly costs.</span></span>
* <span data-ttu-id="62e93-114">VM boyutu toocope büyük talep ek sanal makineleri oluşturmadan artırma.</span><span class="sxs-lookup"><span data-stu-id="62e93-114">Increasing VM size toocope with larger demand without creating additional VMs.</span></span>

<span data-ttu-id="62e93-115">Dikey ayarlayabilirsiniz tetiklenen toobe ölçeklendirme temel ölçüm tabanlı uyarılardan VM ölçek kümesi.</span><span class="sxs-lookup"><span data-stu-id="62e93-115">You can set up vertical scaling toobe triggered based on metric based alerts from your VM Scale Set.</span></span> <span data-ttu-id="62e93-116">Merhaba uyarı etkinleştirildiğinde, bir Web Kancası Yukarı veya aşağı, Ölçek ölçeklenebilen bir runbook ayarlamak bu Tetikleyicileri tetikler.</span><span class="sxs-lookup"><span data-stu-id="62e93-116">When hello alert is activated it fires a webhook that triggers a runbook which can scale your scale set up or down.</span></span> <span data-ttu-id="62e93-117">Dikey ölçeklendirme, aşağıdaki adımları izleyerek yapılandırılabilir:</span><span class="sxs-lookup"><span data-stu-id="62e93-117">Vertical scaling can be configured by following these steps:</span></span>

1. <span data-ttu-id="62e93-118">Çalıştır özelliğine sahip bir Azure Otomasyonu hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="62e93-118">Create an Azure Automation account with run-as capability.</span></span>
2. <span data-ttu-id="62e93-119">Azure Otomasyonu dikey ölçek runbook'ları VM ölçek kümesi için aboneliğinizi alın.</span><span class="sxs-lookup"><span data-stu-id="62e93-119">Import Azure Automation Vertical Scale runbooks for VM Scale Sets into your subscription.</span></span>
3. <span data-ttu-id="62e93-120">Bir Web kancası tooyour runbook ekleyin.</span><span class="sxs-lookup"><span data-stu-id="62e93-120">Add a webhook tooyour runbook.</span></span>
4. <span data-ttu-id="62e93-121">Bir uyarı tooyour bir Web kancası bildirim kullanarak VM ölçek kümesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="62e93-121">Add an alert tooyour VM Scale Set using a webhook notification.</span></span>

> [!NOTE]
> <span data-ttu-id="62e93-122">Dikey otomatik ölçeklendirmeyi yalnızca belirli aralıklarında VM boyutları gerçekleşebilir.</span><span class="sxs-lookup"><span data-stu-id="62e93-122">Vertical autoscaling can only take place within certain ranges of VM sizes.</span></span> <span data-ttu-id="62e93-123">Bir tooanother gelen tooscale karar vermeden önce her boyutta Hello belirtimleri karşılaştırma (daha yüksek sayı her zaman belirtmez büyük VM boyutu).</span><span class="sxs-lookup"><span data-stu-id="62e93-123">Compare hello specifications of each size before deciding tooscale from one tooanother (higher number does not always indicate bigger VM size).</span></span> <span data-ttu-id="62e93-124">Tooscale boyutları çiftlerini aşağıdaki hello arasında seçim yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="62e93-124">You can choose tooscale between hello following pairs of sizes:</span></span>
> 
> | <span data-ttu-id="62e93-125">VM boyutları çifti ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="62e93-125">VM sizes scaling pair</span></span> |  |
> | --- | --- |
> | <span data-ttu-id="62e93-126">Standard_A0</span><span class="sxs-lookup"><span data-stu-id="62e93-126">Standard_A0</span></span> |<span data-ttu-id="62e93-127">Standard_A11</span><span class="sxs-lookup"><span data-stu-id="62e93-127">Standard_A11</span></span> |
> | <span data-ttu-id="62e93-128">Standard_D1</span><span class="sxs-lookup"><span data-stu-id="62e93-128">Standard_D1</span></span> |<span data-ttu-id="62e93-129">Standard_D14</span><span class="sxs-lookup"><span data-stu-id="62e93-129">Standard_D14</span></span> |
> | <span data-ttu-id="62e93-130">Standard_DS1</span><span class="sxs-lookup"><span data-stu-id="62e93-130">Standard_DS1</span></span> |<span data-ttu-id="62e93-131">Standard_DS14</span><span class="sxs-lookup"><span data-stu-id="62e93-131">Standard_DS14</span></span> |
> | <span data-ttu-id="62e93-132">Standard_D1v2</span><span class="sxs-lookup"><span data-stu-id="62e93-132">Standard_D1v2</span></span> |<span data-ttu-id="62e93-133">Standard_D15v2</span><span class="sxs-lookup"><span data-stu-id="62e93-133">Standard_D15v2</span></span> |
> | <span data-ttu-id="62e93-134">Standard_G1</span><span class="sxs-lookup"><span data-stu-id="62e93-134">Standard_G1</span></span> |<span data-ttu-id="62e93-135">Standard_G5</span><span class="sxs-lookup"><span data-stu-id="62e93-135">Standard_G5</span></span> |
> | <span data-ttu-id="62e93-136">Standard_GS1</span><span class="sxs-lookup"><span data-stu-id="62e93-136">Standard_GS1</span></span> |<span data-ttu-id="62e93-137">Standard_GS5</span><span class="sxs-lookup"><span data-stu-id="62e93-137">Standard_GS5</span></span> |
> 
> 

## <a name="create-an-azure-automation-account-with-run-as-capability"></a><span data-ttu-id="62e93-138">Çalıştır özelliğine sahip Azure Automation hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="62e93-138">Create an Azure Automation Account with run-as capability</span></span>
<span data-ttu-id="62e93-139">toodo ihtiyacınız hello ilk hello kullanılan runbook'ları tooscale hello VM ölçek kümesi örneklerinin barındıracak Azure Automation hesabı oluşturma şeydir.</span><span class="sxs-lookup"><span data-stu-id="62e93-139">hello first thing you need toodo is create an Azure Automation account that will host hello runbooks used tooscale hello VM Scale Set instances.</span></span> <span data-ttu-id="62e93-140">Yakın zamanda [Azure Otomasyonu](https://azure.microsoft.com/services/automation/) otomatik olarak hello çalışan runbook'ları bir kullanıcı adına çok kolay için hello hizmet sorumlusu ayarlama kılan hello "Farklı Çalıştır hesabı" özellik sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="62e93-140">Recently [Azure Automation](https://azure.microsoft.com/services/automation/) introduced hello "Run As account" feature which makes setting up hello Service Principal for automatically running hello runbooks on a user's behalf very easy.</span></span> <span data-ttu-id="62e93-141">Daha fazla bilgiyi bu konuda aşağıdaki hello makale:</span><span class="sxs-lookup"><span data-stu-id="62e93-141">You can read more about this in hello article below:</span></span>

* [<span data-ttu-id="62e93-142">Azure Farklı Çalıştır hesabıyla Runbook Kimlik Doğrulaması</span><span class="sxs-lookup"><span data-stu-id="62e93-142">Authenticate Runbooks with Azure Run As account</span></span>](../automation/automation-sec-configure-azure-runas-account.md)

## <a name="import-azure-automation-vertical-scale-runbooks-into-your-subscription"></a><span data-ttu-id="62e93-143">Aboneliğinizi Azure Otomasyon dikey ölçek runbook'ları alma</span><span class="sxs-lookup"><span data-stu-id="62e93-143">Import Azure Automation Vertical Scale runbooks into your subscription</span></span>
<span data-ttu-id="62e93-144">Merhaba runbook'ları VM ölçek kümesi zaten hello Azure Otomasyonu Runbook Galerisi yayımlanan toovertically ölçek gerekli.</span><span class="sxs-lookup"><span data-stu-id="62e93-144">hello runbooks needed toovertically scale your VM Scale Sets are already published in hello Azure Automation Runbook Gallery.</span></span> <span data-ttu-id="62e93-145">aboneliğinizi bunlara hello izleyin tooimport bu makaledeki adımları:</span><span class="sxs-lookup"><span data-stu-id="62e93-145">tooimport them into your subscription follow hello steps in this article:</span></span>

* [<span data-ttu-id="62e93-146">Azure Otomasyonu Runbook ve modül galerileri</span><span class="sxs-lookup"><span data-stu-id="62e93-146">Runbook and module galleries for Azure Automation</span></span>](../automation/automation-runbook-gallery.md)

<span data-ttu-id="62e93-147">Merhaba Runbook'lar menüsünden Hello Gözat galeri seçenek belirleyin:</span><span class="sxs-lookup"><span data-stu-id="62e93-147">Choose hello Browse Gallery option from hello Runbooks menu:</span></span>

![İçe aktarılan Runbook'lar toobe][runbooks]

<span data-ttu-id="62e93-149">toobe alınan ihtiyacınız hello runbook'lar gösterilir.</span><span class="sxs-lookup"><span data-stu-id="62e93-149">hello runbooks that need toobe imported are shown.</span></span> <span data-ttu-id="62e93-150">Merhaba runbook olup, Ölçek ile veya olmadan sağlama işleminin dikey istediğinize bağlı seçin:</span><span class="sxs-lookup"><span data-stu-id="62e93-150">Select hello runbook based on whether you want vertical scaling with or without reprovisioning:</span></span>

![Runbook Galerisi][gallery]

## <a name="add-a-webhook-tooyour-runbook"></a><span data-ttu-id="62e93-152">Web kancası tooyour runbook Ekle</span><span class="sxs-lookup"><span data-stu-id="62e93-152">Add a webhook tooyour runbook</span></span>
<span data-ttu-id="62e93-153">Merhaba runbook'ları içe sonra bir VM ölçek kümesi bir uyarıdan tarafından tetiklenebilir şekilde tooadd bir Web kancası toohello runbook gerekir.</span><span class="sxs-lookup"><span data-stu-id="62e93-153">Once you've imported hello runbooks you'll need tooadd a webhook toohello runbook so it can be triggered by an alert from a VM Scale Set.</span></span> <span data-ttu-id="62e93-154">Bu makalede, Runbook için bir Web kancası oluşturma hello ayrıntıları açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="62e93-154">hello details of creating a webhook for your Runbook are described in this article:</span></span>

* [<span data-ttu-id="62e93-155">Azure Otomasyonu Web kancası</span><span class="sxs-lookup"><span data-stu-id="62e93-155">Azure Automation webhooks</span></span>](../automation/automation-webhooks.md)

> [!NOTE]
> <span data-ttu-id="62e93-156">Bu hello sonraki bölümde ihtiyaç duyacağınız hello Web kancası iletişim kutusunu kapatmadan önce hello Web kancası URI kopyaladığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="62e93-156">Make sure you copy hello webhook URI before closing hello webhook dialog as you will need this in hello next section.</span></span>
> 
> 

## <a name="add-an-alert-tooyour-vm-scale-set"></a><span data-ttu-id="62e93-157">Bir uyarı tooyour VM ölçek kümesi Ekle</span><span class="sxs-lookup"><span data-stu-id="62e93-157">Add an alert tooyour VM Scale Set</span></span>
<span data-ttu-id="62e93-158">Bir PowerShell betiğini hangi gösterir nasıl aşağıdadır tooadd bir uyarı tooa VM ölçek kümesi.</span><span class="sxs-lookup"><span data-stu-id="62e93-158">Below is a PowerShell script which shows how tooadd an alert tooa VM Scale Set.</span></span> <span data-ttu-id="62e93-159">Makale tooget hello hello ölçüm toofire hello uyarı adını aşağıdaki toohello bakın: [Azure İzleyici otomatik ölçeklendirmeyi ortak ölçümleri](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="62e93-159">Refer toohello following article tooget hello name of hello metric toofire hello alert on: [Azure Monitor autoscaling common metrics](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md).</span></span>

```
$actionEmail = New-AzureRmAlertRuleEmail -CustomEmail user@contoso.com
$actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri <uri-of-the-webhook>
$threshold = <value-of-the-threshold>
$rg = <resource-group-name>
$id = <resource-id-to-add-the-alert-to>
$location = <location-of-the-resource>
$alertName = <name-of-the-resource>
$metricName = <metric-to-fire-the-alert-on>
$timeWindow = <time-window-in-hh:mm:ss-format>
$condition = <condition-for-the-threshold> # Other valid values are LessThanOrEqual, GreaterThan, GreaterThanOrEqual
$description = <description-for-the-alert>

Add-AzureRmMetricAlertRule  -Name  $alertName `
                            -Location  $location `
                            -ResourceGroup $rg `
                            -TargetResourceId $id `
                            -MetricName $metricName `
                            -Operator  $condition `
                            -Threshold $threshold `
                            -WindowSize  $timeWindow `
                            -TimeAggregationOperator Average `
                            -Actions $actionEmail, $actionWebhook `
                            -Description $description
```

> [!NOTE]
> <span data-ttu-id="62e93-160">Bu dikey ölçekleme tetikleme sırasını tooavoid hello uyarıda için makul zaman penceresi tooconfigure önerilen ve herhangi bir hizmet kesintisi, çok sık ilişkilendirilmiş.</span><span class="sxs-lookup"><span data-stu-id="62e93-160">It is recommended tooconfigure a reasonable time window for hello alert in order tooavoid triggering vertical scaling, and any associated service interruption, too often.</span></span> <span data-ttu-id="62e93-161">Pencerenin en az 20-30 dakika veya daha fazla göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="62e93-161">Consider a window of least 20-30 minutes or more.</span></span> <span data-ttu-id="62e93-162">Herhangi bir kesintiye tooavoid gerekiyorsa ölçeklendirme yatay göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="62e93-162">Consider horizontal scaling if you need tooavoid any interruption.</span></span>
> 
> 

<span data-ttu-id="62e93-163">Nasıl toocreate uyarıları makaleler toohello başvurmak hakkında daha fazla bilgi için:</span><span class="sxs-lookup"><span data-stu-id="62e93-163">For more information on how toocreate alerts refer toohello following articles:</span></span>

* [<span data-ttu-id="62e93-164">Azure İzleyici PowerShell hızlı başlangıç örnekleri</span><span class="sxs-lookup"><span data-stu-id="62e93-164">Azure Monitor PowerShell quick start samples</span></span>](../monitoring-and-diagnostics/insights-powershell-samples.md)
* [<span data-ttu-id="62e93-165">Azure İzleyici platformlar arası CLI hızlı başlangıç örnekleri</span><span class="sxs-lookup"><span data-stu-id="62e93-165">Azure Monitor Cross-platform CLI quick start samples</span></span>](../monitoring-and-diagnostics/insights-cli-samples.md)

## <a name="summary"></a><span data-ttu-id="62e93-166">Özet</span><span class="sxs-lookup"><span data-stu-id="62e93-166">Summary</span></span>
<span data-ttu-id="62e93-167">Bu makalede basit dikey ölçekleme örnekler gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="62e93-167">This article showed simple vertical scaling examples.</span></span> <span data-ttu-id="62e93-168">Bu yapı taşları ile - Automation hesabı, runbook'ları, Web kancalarını, uyarıları - zengin olayları çeşitli eylemler özelleştirilmiş bir dizi bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="62e93-168">With these building blocks - Automation account, runbooks, webhooks, alerts - you can connect a rich variety of events with a customized set of actions.</span></span>

[runbooks]: ./media/virtual-machine-scale-sets-vertical-scale-reprovision/runbooks.png
[gallery]: ./media/virtual-machine-scale-sets-vertical-scale-reprovision/runbooks-gallery.png
