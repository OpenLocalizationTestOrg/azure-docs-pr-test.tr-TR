---
title: "Azure Otomasyonu ile Azure sanal makine dikey olarak ölçeklendirmek | Microsoft Docs"
description: "Azure Otomasyonu uyarılarla izleme yanıt dikey olarak Linux sanal makine ölçeklendirme"
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
ms.openlocfilehash: 1ffcecf1e61fc0cd9ee668514fbb913dafe39bd8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="vertically-scale-azure-linux-virtual-machine-with-azure-automation"></a><span data-ttu-id="21ab1-103">Dikey olarak Azure Automation ile Azure Linux sanal makine ölçekleme</span><span class="sxs-lookup"><span data-stu-id="21ab1-103">Vertically scale Azure Linux virtual machine with Azure Automation</span></span>
<span data-ttu-id="21ab1-104">Dikey ölçekleme artan veya azalan bir makine yanıt iş yükü olarak kaynakları işlemidir.</span><span class="sxs-lookup"><span data-stu-id="21ab1-104">Vertical scaling is the process of increasing or decreasing the resources of a machine in response to the workload.</span></span> <span data-ttu-id="21ab1-105">Azure'da bu sanal makine boyutunu değiştirerek gerçekleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="21ab1-105">In Azure this can be accomplished by changing the size of the Virtual Machine.</span></span> <span data-ttu-id="21ab1-106">Bu aşağıdaki senaryolarda yardımcı olabilir</span><span class="sxs-lookup"><span data-stu-id="21ab1-106">This can help in the following scenarios</span></span>

* <span data-ttu-id="21ab1-107">Sanal makine sık kullanılmayan, aylık, maliyetleri azaltmak için daha küçük bir boyuta aşağıya doğru boyutlandırabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="21ab1-107">If the Virtual Machine is not being used frequently, you can resize it down to a smaller size to reduce your monthly costs</span></span>
* <span data-ttu-id="21ab1-108">Sanal makine yoğun yük görmesini, onu kapasitesini artırmak için daha büyük bir boyuta yeniden boyutlandırılabilir</span><span class="sxs-lookup"><span data-stu-id="21ab1-108">If the Virtual Machine is seeing a peak load, it can be resized to a larger size to increase its capacity</span></span>

<span data-ttu-id="21ab1-109">Bunu gerçekleştirmek için gereken adımları anahat gibidir aşağıda</span><span class="sxs-lookup"><span data-stu-id="21ab1-109">The outline for the steps to accomplish this is as below</span></span>

1. <span data-ttu-id="21ab1-110">Sanal makinelerinize erişmek için Kurulum Azure Otomasyonu</span><span class="sxs-lookup"><span data-stu-id="21ab1-110">Setup Azure Automation to access your Virtual Machines</span></span>
2. <span data-ttu-id="21ab1-111">Aboneliğiniz Azure Otomasyon dikey ölçek runbook'ları içe</span><span class="sxs-lookup"><span data-stu-id="21ab1-111">Import the Azure Automation Vertical Scale runbooks into your subscription</span></span>
3. <span data-ttu-id="21ab1-112">Bir Web kancası runbook'a ekleyin</span><span class="sxs-lookup"><span data-stu-id="21ab1-112">Add a webhook to your runbook</span></span>
4. <span data-ttu-id="21ab1-113">Sanal makinenize bir uyarı Ekle</span><span class="sxs-lookup"><span data-stu-id="21ab1-113">Add an alert to your Virtual Machine</span></span>

> [!NOTE]
> <span data-ttu-id="21ab1-114">İlk sanal makine için Genişletilebilir boyutları boyutu nedeniyle geçerli sanal makine olarak dağıtılan kümedeki diğer boyutlara kullanılabilirliği nedeniyle sınırlanabilir.</span><span class="sxs-lookup"><span data-stu-id="21ab1-114">Because of the size of the first Virtual Machine, the sizes it can be scaled to, may be limited due to the availability of the other sizes in the cluster current Virtual Machine is deployed in.</span></span> <span data-ttu-id="21ab1-115">Bu makalede kullanılan yayımlanan Otomasyon runbook'ları Biz bu durumda dikkatli ve içinde yalnızca ölçeklendirme VM boyutu çiftleri aşağıda.</span><span class="sxs-lookup"><span data-stu-id="21ab1-115">In the published automation runbooks used in this article we take care of this case and only scale within the below VM size pairs.</span></span> <span data-ttu-id="21ab1-116">Bu bir Standard_D1v2 sanal makine değil aniden Standard_G5 için yukarı ölçeklendirilemez ya da Basic_A0 için genişletilmiş olduğunu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="21ab1-116">This means that a Standard_D1v2 Virtual Machine will not suddenly be scaled up to Standard_G5 or scaled down to Basic_A0.</span></span>
> 
> | <span data-ttu-id="21ab1-117">VM boyutları çifti ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="21ab1-117">VM sizes scaling pair</span></span> |  |
> | --- | --- |
> | <span data-ttu-id="21ab1-118">Basic_A0</span><span class="sxs-lookup"><span data-stu-id="21ab1-118">Basic_A0</span></span> |<span data-ttu-id="21ab1-119">Basic_A4</span><span class="sxs-lookup"><span data-stu-id="21ab1-119">Basic_A4</span></span> |
> | <span data-ttu-id="21ab1-120">Standard_A0</span><span class="sxs-lookup"><span data-stu-id="21ab1-120">Standard_A0</span></span> |<span data-ttu-id="21ab1-121">Standard_A4</span><span class="sxs-lookup"><span data-stu-id="21ab1-121">Standard_A4</span></span> |
> | <span data-ttu-id="21ab1-122">Standard_A5</span><span class="sxs-lookup"><span data-stu-id="21ab1-122">Standard_A5</span></span> |<span data-ttu-id="21ab1-123">Standard_A7</span><span class="sxs-lookup"><span data-stu-id="21ab1-123">Standard_A7</span></span> |
> | <span data-ttu-id="21ab1-124">Standard_A8</span><span class="sxs-lookup"><span data-stu-id="21ab1-124">Standard_A8</span></span> |<span data-ttu-id="21ab1-125">Standard_A9</span><span class="sxs-lookup"><span data-stu-id="21ab1-125">Standard_A9</span></span> |
> | <span data-ttu-id="21ab1-126">Standard_A10</span><span class="sxs-lookup"><span data-stu-id="21ab1-126">Standard_A10</span></span> |<span data-ttu-id="21ab1-127">Standard_A11</span><span class="sxs-lookup"><span data-stu-id="21ab1-127">Standard_A11</span></span> |
> | <span data-ttu-id="21ab1-128">Standard_D1</span><span class="sxs-lookup"><span data-stu-id="21ab1-128">Standard_D1</span></span> |<span data-ttu-id="21ab1-129">Standard_D4</span><span class="sxs-lookup"><span data-stu-id="21ab1-129">Standard_D4</span></span> |
> | <span data-ttu-id="21ab1-130">Standard_D11</span><span class="sxs-lookup"><span data-stu-id="21ab1-130">Standard_D11</span></span> |<span data-ttu-id="21ab1-131">Standard_D14</span><span class="sxs-lookup"><span data-stu-id="21ab1-131">Standard_D14</span></span> |
> | <span data-ttu-id="21ab1-132">Standard_DS1</span><span class="sxs-lookup"><span data-stu-id="21ab1-132">Standard_DS1</span></span> |<span data-ttu-id="21ab1-133">Standard_DS4</span><span class="sxs-lookup"><span data-stu-id="21ab1-133">Standard_DS4</span></span> |
> | <span data-ttu-id="21ab1-134">Standard_DS11</span><span class="sxs-lookup"><span data-stu-id="21ab1-134">Standard_DS11</span></span> |<span data-ttu-id="21ab1-135">Standard_DS14</span><span class="sxs-lookup"><span data-stu-id="21ab1-135">Standard_DS14</span></span> |
> | <span data-ttu-id="21ab1-136">Standard_D1v2</span><span class="sxs-lookup"><span data-stu-id="21ab1-136">Standard_D1v2</span></span> |<span data-ttu-id="21ab1-137">Standard_D5v2</span><span class="sxs-lookup"><span data-stu-id="21ab1-137">Standard_D5v2</span></span> |
> | <span data-ttu-id="21ab1-138">Standard_D11v2</span><span class="sxs-lookup"><span data-stu-id="21ab1-138">Standard_D11v2</span></span> |<span data-ttu-id="21ab1-139">Standard_D14v2</span><span class="sxs-lookup"><span data-stu-id="21ab1-139">Standard_D14v2</span></span> |
> | <span data-ttu-id="21ab1-140">Standard_G1</span><span class="sxs-lookup"><span data-stu-id="21ab1-140">Standard_G1</span></span> |<span data-ttu-id="21ab1-141">Standard_G5</span><span class="sxs-lookup"><span data-stu-id="21ab1-141">Standard_G5</span></span> |
> | <span data-ttu-id="21ab1-142">Standard_GS1</span><span class="sxs-lookup"><span data-stu-id="21ab1-142">Standard_GS1</span></span> |<span data-ttu-id="21ab1-143">Standard_GS5</span><span class="sxs-lookup"><span data-stu-id="21ab1-143">Standard_GS5</span></span> |
> 
> 

## <a name="setup-azure-automation-to-access-your-virtual-machines"></a><span data-ttu-id="21ab1-144">Sanal makinelerinize erişmek için Kurulum Azure Otomasyonu</span><span class="sxs-lookup"><span data-stu-id="21ab1-144">Setup Azure Automation to access your Virtual Machines</span></span>
<span data-ttu-id="21ab1-145">Yapmanız gereken ilk şey VM ölçek kümesi örneklerinin ölçeklendirmek için kullanılan runbook'ları barındıracak bir Azure Otomasyonu hesabı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="21ab1-145">The first thing you need to do is create an Azure Automation account that will host the runbooks used to scale the VM Scale Set instances.</span></span> <span data-ttu-id="21ab1-146">Yakın zamanda Otomasyon hizmeti otomatik olarak çalışan runbook'ları kullanıcı adınıza çok kolay için ayar yukarı hizmet sorumlusu getirir "Farklı Çalıştır hesabı" özelliğini kullanıma sunmuştur.</span><span class="sxs-lookup"><span data-stu-id="21ab1-146">Recently the Automation service introduced the "Run As account" feature which makes setting up the Service Principal for automatically running the runbooks on the user's behalf very easy.</span></span> <span data-ttu-id="21ab1-147">Daha fazla bilgiyi bu konuda aşağıdaki makalede:</span><span class="sxs-lookup"><span data-stu-id="21ab1-147">You can read more about this in the article below:</span></span>

* [<span data-ttu-id="21ab1-148">Azure Farklı Çalıştır hesabıyla Runbook Kimlik Doğrulaması</span><span class="sxs-lookup"><span data-stu-id="21ab1-148">Authenticate Runbooks with Azure Run As account</span></span>](../../automation/automation-sec-configure-azure-runas-account.md)

## <a name="import-the-azure-automation-vertical-scale-runbooks-into-your-subscription"></a><span data-ttu-id="21ab1-149">Aboneliğiniz Azure Otomasyon dikey ölçek runbook'ları içe</span><span class="sxs-lookup"><span data-stu-id="21ab1-149">Import the Azure Automation Vertical Scale runbooks into your subscription</span></span>
<span data-ttu-id="21ab1-150">Sanal makineniz dikey ölçekleme için gerekli olan runbook'ları zaten Azure Otomasyonu Runbook Galerisi yayımlanır.</span><span class="sxs-lookup"><span data-stu-id="21ab1-150">The runbooks that are needed for Vertically Scaling your Virtual Machine are already published in the Azure Automation Runbook Gallery.</span></span> <span data-ttu-id="21ab1-151">Aboneliğinizi aktarmak gerekir.</span><span class="sxs-lookup"><span data-stu-id="21ab1-151">You will need to import them into your subscription.</span></span> <span data-ttu-id="21ab1-152">Runbook'ları makalesini okuyarak içeri öğrenebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21ab1-152">You can learn how to import runbooks by reading the following article.</span></span>

* [<span data-ttu-id="21ab1-153">Azure Otomasyonu Runbook ve modül galerileri</span><span class="sxs-lookup"><span data-stu-id="21ab1-153">Runbook and module galleries for Azure Automation</span></span>](../../automation/automation-runbook-gallery.md)

<span data-ttu-id="21ab1-154">Aşağıdaki resimde gösterilen içeri aktarılması gereken runbook'ları</span><span class="sxs-lookup"><span data-stu-id="21ab1-154">The runbooks that need to be imported are shown in the image below</span></span>

![Runbook'ları alma](./media/vertical-scaling-automation/scale-runbooks.png)

## <a name="add-a-webhook-to-your-runbook"></a><span data-ttu-id="21ab1-156">Bir Web kancası runbook'a ekleyin</span><span class="sxs-lookup"><span data-stu-id="21ab1-156">Add a webhook to your runbook</span></span>
<span data-ttu-id="21ab1-157">Alınan sonra gerekir runbook'ları bir sanal makineden bir uyarı tarafından tetiklenebilir için bir Web kancası runbook'a ekleyin.</span><span class="sxs-lookup"><span data-stu-id="21ab1-157">Once you've imported the runbooks you'll need to add a webhook to the runbook so it can be triggered by an alert from a Virtual Machine.</span></span> <span data-ttu-id="21ab1-158">Runbook için bir Web kancası oluşturma ayrıntılarını burada okuyabilir</span><span class="sxs-lookup"><span data-stu-id="21ab1-158">The details of creating a webhook for your Runbook can be read here</span></span>

* [<span data-ttu-id="21ab1-159">Azure Otomasyonu Web kancası</span><span class="sxs-lookup"><span data-stu-id="21ab1-159">Azure Automation webhooks</span></span>](../../automation/automation-webhooks.md)

<span data-ttu-id="21ab1-160">Bu sonraki bölümde ihtiyaç duyacağınız Web kancası iletişim kutusunu kapatmadan önce Web kancası kopyaladığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="21ab1-160">Make sure you copy the webhook before closing the webhook dialog as you will need this in the next section.</span></span>

## <a name="add-an-alert-to-your-virtual-machine"></a><span data-ttu-id="21ab1-161">Sanal makinenize bir uyarı Ekle</span><span class="sxs-lookup"><span data-stu-id="21ab1-161">Add an alert to your Virtual Machine</span></span>
1. <span data-ttu-id="21ab1-162">Sanal makine ayarlarını seçin</span><span class="sxs-lookup"><span data-stu-id="21ab1-162">Select Virtual Machine settings</span></span>
2. <span data-ttu-id="21ab1-163">"Uyarı kuralları" seçeneğini belirleyin</span><span class="sxs-lookup"><span data-stu-id="21ab1-163">Select "Alert rules"</span></span>
3. <span data-ttu-id="21ab1-164">"Uyarı Ekle" seçin</span><span class="sxs-lookup"><span data-stu-id="21ab1-164">Select "Add alert"</span></span>
4. <span data-ttu-id="21ab1-165">Hakkında uyarı tetiklenecek bir ölçümü seçin</span><span class="sxs-lookup"><span data-stu-id="21ab1-165">Select a metric to fire the alert on</span></span>
5. <span data-ttu-id="21ab1-166">Bir koşul Seç hangi olduğunda yerine tetiklenecek uyarının nedeni</span><span class="sxs-lookup"><span data-stu-id="21ab1-166">Select a condition, which when fulfilled will cause the alert to fire</span></span>
6. <span data-ttu-id="21ab1-167">Koşul için bir eşik adım 5'te seçin.</span><span class="sxs-lookup"><span data-stu-id="21ab1-167">Select a threshold for the condition in Step 5.</span></span> <span data-ttu-id="21ab1-168">yerine getirilmesi için</span><span class="sxs-lookup"><span data-stu-id="21ab1-168">to be fulfilled</span></span>
7. <span data-ttu-id="21ab1-169">Üzerinde izleme hizmeti denetleyecek bir dönem için koşul ve eşik adımları 5 ve 6'seçin</span><span class="sxs-lookup"><span data-stu-id="21ab1-169">Select a period over which the monitoring service will check for the condition and threshold in Steps 5 & 6</span></span>
8. <span data-ttu-id="21ab1-170">Önceki bölümünde kopyaladığınız Web kancası yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="21ab1-170">Paste in the webhook you copied from the previous section.</span></span>

![Sanal makine 1 uyarısı ekleme](./media/vertical-scaling-automation/add-alert-webhook-1.png)

![Sanal makine 2 uyarısı ekleme](./media/vertical-scaling-automation/add-alert-webhook-2.png)

