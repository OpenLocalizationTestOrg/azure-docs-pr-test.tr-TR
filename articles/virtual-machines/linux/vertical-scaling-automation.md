---
title: "aaaVertically ölçek Azure Automation ile Azure sanal makine | Microsoft Docs"
description: "Nasıl toovertically ölçeklendirme Linux sanal makine yanıt toomonitoring uyarılar Azure Automation"
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: dcee199e-fa25-44d5-9b25-df564cee9b45
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/29/2016
ms.author: singhkay
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ee4c1c33a588bd907d107f1828380a8afdaa725e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="vertically-scale-azure-linux-virtual-machine-with-azure-automation"></a><span data-ttu-id="84b60-103">Dikey olarak Azure Automation ile Azure Linux sanal makine ölçekleme</span><span class="sxs-lookup"><span data-stu-id="84b60-103">Vertically scale Azure Linux virtual machine with Azure Automation</span></span>
<span data-ttu-id="84b60-104">Dikey ölçekleme artan veya azalan bir makine yanıt toohello iş yükü hello kaynakları hello işlemidir.</span><span class="sxs-lookup"><span data-stu-id="84b60-104">Vertical scaling is hello process of increasing or decreasing hello resources of a machine in response toohello workload.</span></span> <span data-ttu-id="84b60-105">Azure'da bu hello hello sanal makine boyutunu değiştirerek gerçekleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="84b60-105">In Azure this can be accomplished by changing hello size of hello Virtual Machine.</span></span> <span data-ttu-id="84b60-106">Bu senaryolar aşağıdaki hello yardımcı olabilir</span><span class="sxs-lookup"><span data-stu-id="84b60-106">This can help in hello following scenarios</span></span>

* <span data-ttu-id="84b60-107">Sanal makine Hello sık kullanılmayan, tooa daha küçük boyutu tooreduce aylık maliyetleriniz yeniden boyutlandırabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="84b60-107">If hello Virtual Machine is not being used frequently, you can resize it down tooa smaller size tooreduce your monthly costs</span></span>
* <span data-ttu-id="84b60-108">Sanal makine Hello yoğun yük görmesini yoksa, yapabilirsiniz yeniden boyutlandırılan tooa büyük boyutu tooincrease kapasitesi olabilir</span><span class="sxs-lookup"><span data-stu-id="84b60-108">If hello Virtual Machine is seeing a peak load, it can be resized tooa larger size tooincrease its capacity</span></span>

<span data-ttu-id="84b60-109">Merhaba anahat budur olarak hello adımları tooaccomplish için aşağıda</span><span class="sxs-lookup"><span data-stu-id="84b60-109">hello outline for hello steps tooaccomplish this is as below</span></span>

1. <span data-ttu-id="84b60-110">Azure Otomasyonu tooaccess sanal makinelerinizi Kurulumu</span><span class="sxs-lookup"><span data-stu-id="84b60-110">Setup Azure Automation tooaccess your Virtual Machines</span></span>
2. <span data-ttu-id="84b60-111">Aboneliğinizi Hello Azure Otomasyon dikey ölçek runbook'ları alma</span><span class="sxs-lookup"><span data-stu-id="84b60-111">Import hello Azure Automation Vertical Scale runbooks into your subscription</span></span>
3. <span data-ttu-id="84b60-112">Web kancası tooyour runbook Ekle</span><span class="sxs-lookup"><span data-stu-id="84b60-112">Add a webhook tooyour runbook</span></span>
4. <span data-ttu-id="84b60-113">Bir uyarı tooyour sanal makine ekleyin</span><span class="sxs-lookup"><span data-stu-id="84b60-113">Add an alert tooyour Virtual Machine</span></span>

> [!NOTE]
> <span data-ttu-id="84b60-114">İlk sanal makine, bunu ölçeklendirilmiş için hello boyutları hello Hello boyutu nedeniyle sınırlanabilir hello toohello kullanılabilirliği, içinde geçerli sanal makine hello kümedeki diğer boyutlara dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="84b60-114">Because of hello size of hello first Virtual Machine, hello sizes it can be scaled to, may be limited due toohello availability of hello other sizes in hello cluster current Virtual Machine is deployed in.</span></span> <span data-ttu-id="84b60-115">Bu durumda ilgilenebilmek ve yalnızca VM boyutu çiftleri aşağıda hello içinde ölçeklendirmek bu makalede kullanılan Otomasyon runbook'ları Hello yayımladı.</span><span class="sxs-lookup"><span data-stu-id="84b60-115">In hello published automation runbooks used in this article we take care of this case and only scale within hello below VM size pairs.</span></span> <span data-ttu-id="84b60-116">Bu bir Standard_D1v2 sanal makine değil aniden tooStandard_G5 ölçeklendirilemez ya da tooBasic_A0 ölçeklendirilmiş olduğunu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="84b60-116">This means that a Standard_D1v2 Virtual Machine will not suddenly be scaled up tooStandard_G5 or scaled down tooBasic_A0.</span></span>
> 
> | <span data-ttu-id="84b60-117">VM boyutları çifti ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="84b60-117">VM sizes scaling pair</span></span> |  |
> | --- | --- |
> | <span data-ttu-id="84b60-118">Basic_A0</span><span class="sxs-lookup"><span data-stu-id="84b60-118">Basic_A0</span></span> |<span data-ttu-id="84b60-119">Basic_A4</span><span class="sxs-lookup"><span data-stu-id="84b60-119">Basic_A4</span></span> |
> | <span data-ttu-id="84b60-120">Standard_A0</span><span class="sxs-lookup"><span data-stu-id="84b60-120">Standard_A0</span></span> |<span data-ttu-id="84b60-121">Standard_A4</span><span class="sxs-lookup"><span data-stu-id="84b60-121">Standard_A4</span></span> |
> | <span data-ttu-id="84b60-122">Standard_A5</span><span class="sxs-lookup"><span data-stu-id="84b60-122">Standard_A5</span></span> |<span data-ttu-id="84b60-123">Standard_A7</span><span class="sxs-lookup"><span data-stu-id="84b60-123">Standard_A7</span></span> |
> | <span data-ttu-id="84b60-124">Standard_A8</span><span class="sxs-lookup"><span data-stu-id="84b60-124">Standard_A8</span></span> |<span data-ttu-id="84b60-125">Standard_A9</span><span class="sxs-lookup"><span data-stu-id="84b60-125">Standard_A9</span></span> |
> | <span data-ttu-id="84b60-126">Standard_A10</span><span class="sxs-lookup"><span data-stu-id="84b60-126">Standard_A10</span></span> |<span data-ttu-id="84b60-127">Standard_A11</span><span class="sxs-lookup"><span data-stu-id="84b60-127">Standard_A11</span></span> |
> | <span data-ttu-id="84b60-128">Standard_D1</span><span class="sxs-lookup"><span data-stu-id="84b60-128">Standard_D1</span></span> |<span data-ttu-id="84b60-129">Standard_D4</span><span class="sxs-lookup"><span data-stu-id="84b60-129">Standard_D4</span></span> |
> | <span data-ttu-id="84b60-130">Standard_D11</span><span class="sxs-lookup"><span data-stu-id="84b60-130">Standard_D11</span></span> |<span data-ttu-id="84b60-131">Standard_D14</span><span class="sxs-lookup"><span data-stu-id="84b60-131">Standard_D14</span></span> |
> | <span data-ttu-id="84b60-132">Standard_DS1</span><span class="sxs-lookup"><span data-stu-id="84b60-132">Standard_DS1</span></span> |<span data-ttu-id="84b60-133">Standard_DS4</span><span class="sxs-lookup"><span data-stu-id="84b60-133">Standard_DS4</span></span> |
> | <span data-ttu-id="84b60-134">Standard_DS11</span><span class="sxs-lookup"><span data-stu-id="84b60-134">Standard_DS11</span></span> |<span data-ttu-id="84b60-135">Standard_DS14</span><span class="sxs-lookup"><span data-stu-id="84b60-135">Standard_DS14</span></span> |
> | <span data-ttu-id="84b60-136">Standard_D1v2</span><span class="sxs-lookup"><span data-stu-id="84b60-136">Standard_D1v2</span></span> |<span data-ttu-id="84b60-137">Standard_D5v2</span><span class="sxs-lookup"><span data-stu-id="84b60-137">Standard_D5v2</span></span> |
> | <span data-ttu-id="84b60-138">Standard_D11v2</span><span class="sxs-lookup"><span data-stu-id="84b60-138">Standard_D11v2</span></span> |<span data-ttu-id="84b60-139">Standard_D14v2</span><span class="sxs-lookup"><span data-stu-id="84b60-139">Standard_D14v2</span></span> |
> | <span data-ttu-id="84b60-140">Standard_G1</span><span class="sxs-lookup"><span data-stu-id="84b60-140">Standard_G1</span></span> |<span data-ttu-id="84b60-141">Standard_G5</span><span class="sxs-lookup"><span data-stu-id="84b60-141">Standard_G5</span></span> |
> | <span data-ttu-id="84b60-142">Standard_GS1</span><span class="sxs-lookup"><span data-stu-id="84b60-142">Standard_GS1</span></span> |<span data-ttu-id="84b60-143">Standard_GS5</span><span class="sxs-lookup"><span data-stu-id="84b60-143">Standard_GS5</span></span> |
> 
> 

## <a name="setup-azure-automation-tooaccess-your-virtual-machines"></a><span data-ttu-id="84b60-144">Azure Otomasyonu tooaccess sanal makinelerinizi Kurulumu</span><span class="sxs-lookup"><span data-stu-id="84b60-144">Setup Azure Automation tooaccess your Virtual Machines</span></span>
<span data-ttu-id="84b60-145">toodo ihtiyacınız hello ilk hello kullanılan runbook'ları tooscale hello VM ölçek kümesi örneklerinin barındıracak Azure Automation hesabı oluşturma şeydir.</span><span class="sxs-lookup"><span data-stu-id="84b60-145">hello first thing you need toodo is create an Azure Automation account that will host hello runbooks used tooscale hello VM Scale Set instances.</span></span> <span data-ttu-id="84b60-146">Yakın zamanda hello Otomasyon hizmeti otomatik olarak hello çalışan runbook'ları hello kullanıcı adına çok kolay için hello hizmet sorumlusu ayarlama kılan hello "Farklı Çalıştır hesabı" özellik sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="84b60-146">Recently hello Automation service introduced hello "Run As account" feature which makes setting up hello Service Principal for automatically running hello runbooks on hello user's behalf very easy.</span></span> <span data-ttu-id="84b60-147">Daha fazla bilgiyi bu konuda aşağıdaki hello makale:</span><span class="sxs-lookup"><span data-stu-id="84b60-147">You can read more about this in hello article below:</span></span>

* [<span data-ttu-id="84b60-148">Azure Farklı Çalıştır hesabıyla Runbook Kimlik Doğrulaması</span><span class="sxs-lookup"><span data-stu-id="84b60-148">Authenticate Runbooks with Azure Run As account</span></span>](../../automation/automation-sec-configure-azure-runas-account.md)

## <a name="import-hello-azure-automation-vertical-scale-runbooks-into-your-subscription"></a><span data-ttu-id="84b60-149">Aboneliğinizi Hello Azure Otomasyon dikey ölçek runbook'ları alma</span><span class="sxs-lookup"><span data-stu-id="84b60-149">Import hello Azure Automation Vertical Scale runbooks into your subscription</span></span>
<span data-ttu-id="84b60-150">Sanal makineniz zaten hello Azure Otomasyonu Runbook Galerisi yayımlanan dikey ölçekleme için gerekli olan hello runbook'ları.</span><span class="sxs-lookup"><span data-stu-id="84b60-150">hello runbooks that are needed for Vertically Scaling your Virtual Machine are already published in hello Azure Automation Runbook Gallery.</span></span> <span data-ttu-id="84b60-151">Tooimport gerekir, aboneliğe bunları.</span><span class="sxs-lookup"><span data-stu-id="84b60-151">You will need tooimport them into your subscription.</span></span> <span data-ttu-id="84b60-152">Makalede okuyarak tooimport runbook'ları nasıl hello öğrenebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="84b60-152">You can learn how tooimport runbooks by reading hello following article.</span></span>

* [<span data-ttu-id="84b60-153">Azure Otomasyonu Runbook ve modül galerileri</span><span class="sxs-lookup"><span data-stu-id="84b60-153">Runbook and module galleries for Azure Automation</span></span>](../../automation/automation-runbook-gallery.md)

<span data-ttu-id="84b60-154">Aşağıdaki hello görüntü toobe alınan ihtiyacınız hello runbook'lar gösterilir</span><span class="sxs-lookup"><span data-stu-id="84b60-154">hello runbooks that need toobe imported are shown in hello image below</span></span>

![Runbook'ları alma](./media/vertical-scaling-automation/scale-runbooks.png)

## <a name="add-a-webhook-tooyour-runbook"></a><span data-ttu-id="84b60-156">Web kancası tooyour runbook Ekle</span><span class="sxs-lookup"><span data-stu-id="84b60-156">Add a webhook tooyour runbook</span></span>
<span data-ttu-id="84b60-157">Merhaba runbook'ları içe sonra bir sanal makineden bir uyarı tarafından tetiklenebilir şekilde tooadd bir Web kancası toohello runbook gerekir.</span><span class="sxs-lookup"><span data-stu-id="84b60-157">Once you've imported hello runbooks you'll need tooadd a webhook toohello runbook so it can be triggered by an alert from a Virtual Machine.</span></span> <span data-ttu-id="84b60-158">Runbook için bir Web kancası oluşturma hello ayrıntıları buraya okuyabilir</span><span class="sxs-lookup"><span data-stu-id="84b60-158">hello details of creating a webhook for your Runbook can be read here</span></span>

* [<span data-ttu-id="84b60-159">Azure Otomasyonu Web kancası</span><span class="sxs-lookup"><span data-stu-id="84b60-159">Azure Automation webhooks</span></span>](../../automation/automation-webhooks.md)

<span data-ttu-id="84b60-160">Bu hello sonraki bölümde ihtiyaç duyacağınız hello Web kancası iletişim kutusunu kapatmadan önce hello Web kancası kopyaladığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="84b60-160">Make sure you copy hello webhook before closing hello webhook dialog as you will need this in hello next section.</span></span>

## <a name="add-an-alert-tooyour-virtual-machine"></a><span data-ttu-id="84b60-161">Bir uyarı tooyour sanal makine ekleyin</span><span class="sxs-lookup"><span data-stu-id="84b60-161">Add an alert tooyour Virtual Machine</span></span>
1. <span data-ttu-id="84b60-162">Sanal makine ayarlarını seçin</span><span class="sxs-lookup"><span data-stu-id="84b60-162">Select Virtual Machine settings</span></span>
2. <span data-ttu-id="84b60-163">"Uyarı kuralları" seçeneğini belirleyin</span><span class="sxs-lookup"><span data-stu-id="84b60-163">Select "Alert rules"</span></span>
3. <span data-ttu-id="84b60-164">"Uyarı Ekle" seçin</span><span class="sxs-lookup"><span data-stu-id="84b60-164">Select "Add alert"</span></span>
4. <span data-ttu-id="84b60-165">Ölçüm toofire hello uyarıyı seçin</span><span class="sxs-lookup"><span data-stu-id="84b60-165">Select a metric toofire hello alert on</span></span>
5. <span data-ttu-id="84b60-166">Bir koşul Seç hangi olduğunda yerine hello uyarı toofire neden</span><span class="sxs-lookup"><span data-stu-id="84b60-166">Select a condition, which when fulfilled will cause hello alert toofire</span></span>
6. <span data-ttu-id="84b60-167">Adım 5'te hello koşul için bir eşik seçin.</span><span class="sxs-lookup"><span data-stu-id="84b60-167">Select a threshold for hello condition in Step 5.</span></span> <span data-ttu-id="84b60-168">yerine toobe</span><span class="sxs-lookup"><span data-stu-id="84b60-168">toobe fulfilled</span></span>
7. <span data-ttu-id="84b60-169">İzleme hizmeti hangi hello denetleyecek bir dönem için hello koşul ve eşik adımları 5 ve 6'seçin</span><span class="sxs-lookup"><span data-stu-id="84b60-169">Select a period over which hello monitoring service will check for hello condition and threshold in Steps 5 & 6</span></span>
8. <span data-ttu-id="84b60-170">Merhaba önceki bölümünde kopyaladığınız hello Web kancası yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="84b60-170">Paste in hello webhook you copied from hello previous section.</span></span>

![Uyarı tooVirtual makine 1 ekleme](./media/vertical-scaling-automation/add-alert-webhook-1.png)

![Uyarı tooVirtual makine 2 ekleme](./media/vertical-scaling-automation/add-alert-webhook-2.png)

