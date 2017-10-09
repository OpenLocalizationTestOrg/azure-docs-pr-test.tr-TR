---
title: Azure RemoteApp PowerShell cmdlet'leriyle aaaUse | Microsoft Docs
description: "Bilgi nasıl toouse Azure RemoteApp Windows PowerShell cmdlet'leri."
services: remoteapp
documentationcenter: 
author: guscatalano
manager: mbaldwin
editor: 
ms.assetid: 7d3d5ded-6f73-4de6-a8ac-c1d622e842a2
ms.service: remoteapp
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: a09cae2093e2c3a4a2ed673b5d148a22ceb935f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-windows-powershell-cmdlets-with-azure-remoteapp"></a><span data-ttu-id="1cbc3-103">Azure RemoteApp ile Windows PowerShell cmdlet'lerini kullanma</span><span class="sxs-lookup"><span data-stu-id="1cbc3-103">Use Windows PowerShell cmdlets with Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="1cbc3-104">Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır.</span><span class="sxs-lookup"><span data-stu-id="1cbc3-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="1cbc3-105">Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="1cbc3-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

 <span data-ttu-id="1cbc3-106">Koleksiyonunuz korumak ve hello Azure RemoteApp PowerShell cmdlet'leri tooadminister kullanın.</span><span class="sxs-lookup"><span data-stu-id="1cbc3-106">You can use hello Azure RemoteApp PowerShell cmdlets tooadminister and maintain your collections.</span></span> <span data-ttu-id="1cbc3-107">Başlatılan bilgi tooget aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="1cbc3-107">Use hello following information tooget started.</span></span>

## <a name="get-hello-cmdlets"></a><span data-ttu-id="1cbc3-108">Merhaba cmdlet'lerini alma</span><span class="sxs-lookup"><span data-stu-id="1cbc3-108">Get hello cmdlets</span></span>
- - -
<span data-ttu-id="1cbc3-109">İlk hello Azure Powershell cmdlet'lerini indirin [burada](http://go.microsoft.com/?linkid=9811175), hello RemoteApp cmdlet'lerini içine dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="1cbc3-109">First download hello Azure Powershell cmdlets [here](http://go.microsoft.com/?linkid=9811175), hello RemoteApp cmdlets are included in it.</span></span> 

<span data-ttu-id="1cbc3-110">Merhaba denetleyin [Azure RemoteApp cmdlet Yardım](/powershell/module/azure?view=azuresmps-3.7.0).</span><span class="sxs-lookup"><span data-stu-id="1cbc3-110">Check out hello [Azure RemoteApp cmdlet help](/powershell/module/azure?view=azuresmps-3.7.0).</span></span>

## <a name="configure-azure-cmdlets-toouse-your-subscription"></a><span data-ttu-id="1cbc3-111">Aboneliğiniz Azure cmdlet'lerini toouse yapılandırın</span><span class="sxs-lookup"><span data-stu-id="1cbc3-111">Configure Azure cmdlets toouse your subscription</span></span>
- - -
<span data-ttu-id="1cbc3-112">İzleyin [bu kılavuzda](/powershell/azure/overview) hello cmdlet'leri, Azure aboneliğinizin karşı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1cbc3-112">Follow [this guide](/powershell/azure/overview) so you can use hello cmdlets against your Azure subscription.</span></span>

<span data-ttu-id="1cbc3-113">Bu adımları tooget hızlı şekilde kullanmaya kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="1cbc3-113">You can use these steps tooget started quickly:</span></span>

1. <span data-ttu-id="1cbc3-114">Merhaba yükleyip [Azure PowerShell cmdlet'lerini](http://go.microsoft.com/?linkid=9811175).</span><span class="sxs-lookup"><span data-stu-id="1cbc3-114">Download and install hello [Azure PowerShell cmdlets](http://go.microsoft.com/?linkid=9811175).</span></span>
2. <span data-ttu-id="1cbc3-115">Microsoft Azure PowerShell'i başlatın.</span><span class="sxs-lookup"><span data-stu-id="1cbc3-115">Launch Microsoft Azure PowerShell.</span></span>
3. <span data-ttu-id="1cbc3-116">Çalıştırma **Add-AzureAccount** tooauthenticate tooyour Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="1cbc3-116">Run **Add-AzureAccount** tooauthenticate tooyour Azure subscription.</span></span> <span data-ttu-id="1cbc3-117">İstendiğinde, girin hello aynı kullanıcı adı ve parola tooAzure Portalı'nda toosign kullanın.</span><span class="sxs-lookup"><span data-stu-id="1cbc3-117">When prompted, enter hello same user name and password that you use toosign in tooAzure portal.</span></span>  
4. <span data-ttu-id="1cbc3-118">Çalıştırma **Get-AzureSubscription** kullanıcı hesabınızla ilişkili toolist hello abonelik.</span><span class="sxs-lookup"><span data-stu-id="1cbc3-118">Run **Get-AzureSubscription** toolist hello subscriptions associated with your user account.</span></span> 
5. <span data-ttu-id="1cbc3-119">Çalıştırma **Select-AzureSubscription - varlığıyla SubscriptionName &lt;abonelik adı&gt;**  veya **Select-AzureSubscription - Subscriptionıd &lt;abonelik kimliği&gt;**  toospecify hello abonelik toouse.</span><span class="sxs-lookup"><span data-stu-id="1cbc3-119">Run **Select-AzureSubscription -SubscriptionName &lt;subscription name&gt;** or **Select-AzureSubscription -SubscriptionId &lt;subscription ID&gt;** toospecify hello subscription toouse.</span></span>

<span data-ttu-id="1cbc3-120">Tebrikler, Azure PowerShell konsolunuza yapılandırılmış ve hazır toouse.</span><span class="sxs-lookup"><span data-stu-id="1cbc3-120">Congratulations, your Azure PowerShell console is configured and ready toouse.</span></span> <span data-ttu-id="1cbc3-121">Merhaba hello Azure PowerShell konsolunda her başlattığınızda toorepeate adımları 2'den 5 gerekir unutmayın.</span><span class="sxs-lookup"><span data-stu-id="1cbc3-121">Be aware that you'll need toorepeate steps 2 through 5 each time you start hello hello Azure PowerShell console.</span></span>  


## <a name="list-all-collections"></a><span data-ttu-id="1cbc3-122">Tüm koleksiyonları listesi</span><span class="sxs-lookup"><span data-stu-id="1cbc3-122">List all collections</span></span>
- - -
     <span data-ttu-id="1cbc3-123">Get-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="1cbc3-123">Get-AzureRemoteAppCollection</span></span>

## <a name="delete-a-collection"></a><span data-ttu-id="1cbc3-124">Bir koleksiyonu silin</span><span class="sxs-lookup"><span data-stu-id="1cbc3-124">Delete a collection</span></span>
- - -
    <span data-ttu-id="1cbc3-125">Remove-AzureRemoteAppCollection<enter collection name></span><span class="sxs-lookup"><span data-stu-id="1cbc3-125">Remove-AzureRemoteAppCollection <enter collection name></span></span>

<span data-ttu-id="1cbc3-126">Örnek: `Remove-AzureRemoteAppCollection ContosoProduction`.</span><span class="sxs-lookup"><span data-stu-id="1cbc3-126">Example:  `Remove-AzureRemoteAppCollection ContosoProduction`.</span></span>

## <a name="create-a-cloud-collection"></a><span data-ttu-id="1cbc3-127">Bulut koleksiyonu oluşturma</span><span class="sxs-lookup"><span data-stu-id="1cbc3-127">Create a cloud collection</span></span>
- - -
<span data-ttu-id="1cbc3-128">Merhaba aşağıdaki komutu çalıştırın, basittir:</span><span class="sxs-lookup"><span data-stu-id="1cbc3-128">It's simple, run hello following command:</span></span>

    New-AzureRemoteAppCollection -Collectionname RAppO365Col1 -ImageName "Office 365 ProPlus (Subscription required)" -Plan Basic -Location "West US" - Description "Office 365 Collection."

<span data-ttu-id="1cbc3-129">Yukarıdaki komut Hello Microsoft Office 365 uygulamaları (Excel, OneNote, Outlook, PowerPoint, Visio ve Word) otomatik olarak yayımlar.</span><span class="sxs-lookup"><span data-stu-id="1cbc3-129">hello above command automatically publishes Microsoft Office 365 applications (Excel, OneNote, Outlook, PowerPoint, Visio and Word).</span></span>

<span data-ttu-id="1cbc3-130">Koleksiyon oluşturma 30 dakika veya daha uzun toocomplete alabilir.</span><span class="sxs-lookup"><span data-stu-id="1cbc3-130">Collection creation can take 30 minutes or longer toocomplete.</span></span> <span data-ttu-id="1cbc3-131">Bu nedenle, bu komut aşağıdaki gibi kullanabilirsiniz izleme kimliği döndürür:</span><span class="sxs-lookup"><span data-stu-id="1cbc3-131">Therefore, this command returns a tracking ID that you can use as follows:</span></span>

    Get-AzureRemoteAppOperationResult -TrackingId xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

<span data-ttu-id="1cbc3-132">Merhaba koleksiyonu yapıldıktan sonra komutu aşağıdaki hello ile kullanıcı toohello toplama ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="1cbc3-132">After hello collection is done, you can add users toohello collection with hello following command:</span></span>

    Add-AzureRemoteAppUser -CollectionName RAppO365Col1 -Type microsoftAccount -UserUpn someone@domain.com

<span data-ttu-id="1cbc3-133">Ve bitirdiniz!</span><span class="sxs-lookup"><span data-stu-id="1cbc3-133">And you're done!</span></span> <span data-ttu-id="1cbc3-134">Bu kullanıcının bulunan hello Azure RemoteApp istemcisini kullanarak mümkün tooconnect toohello application olmalıdır. [burada](https://www.remoteapp.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="1cbc3-134">That user should be able tooconnect toohello application using hello Azure RemoteApp client found [here](https://www.remoteapp.windowsazure.com/).</span></span>

## <a name="available-cmdlets"></a><span data-ttu-id="1cbc3-135">Kullanılabilen cmdlet'ler</span><span class="sxs-lookup"><span data-stu-id="1cbc3-135">Available cmdlets</span></span>
<span data-ttu-id="1cbc3-136">Çok sayıda sahibiz diğer komutlar vardır, bunları hello belgelerine kısa bir süre sonra gelen:</span><span class="sxs-lookup"><span data-stu-id="1cbc3-136">There are lots of other commands that we have, hello documentation for them will be coming shortly:</span></span>

<span data-ttu-id="1cbc3-137">Temel RemoteApp koleksiyonu cmdlet:</span><span class="sxs-lookup"><span data-stu-id="1cbc3-137">Basic RemoteApp Collection cmdlets:</span></span> 

* <span data-ttu-id="1cbc3-138">New-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="1cbc3-138">New-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="1cbc3-139">Get-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="1cbc3-139">Get-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="1cbc3-140">Set-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="1cbc3-140">Set-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="1cbc3-141">Update-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="1cbc3-141">Update-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="1cbc3-142">Remove-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="1cbc3-142">Remove-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="1cbc3-143">Add-AzureRemoteAppUser</span><span class="sxs-lookup"><span data-stu-id="1cbc3-143">Add-AzureRemoteAppUser</span></span>
* <span data-ttu-id="1cbc3-144">Get-AzureRemoteAppUser</span><span class="sxs-lookup"><span data-stu-id="1cbc3-144">Get-AzureRemoteAppUser</span></span>
* <span data-ttu-id="1cbc3-145">Remove-AzureRemoteAppUser</span><span class="sxs-lookup"><span data-stu-id="1cbc3-145">Remove-AzureRemoteAppUser</span></span>
* <span data-ttu-id="1cbc3-146">Get-AzureRemoteAppSession</span><span class="sxs-lookup"><span data-stu-id="1cbc3-146">Get-AzureRemoteAppSession</span></span>
* <span data-ttu-id="1cbc3-147">Disconnect-AzureRemoteAppSession</span><span class="sxs-lookup"><span data-stu-id="1cbc3-147">Disconnect-AzureRemoteAppSession</span></span>
* <span data-ttu-id="1cbc3-148">Invoke-AzureRemoteAppSessionLogoff</span><span class="sxs-lookup"><span data-stu-id="1cbc3-148">Invoke-AzureRemoteAppSessionLogoff</span></span>
* <span data-ttu-id="1cbc3-149">Send-AzureRemoteAppSessionMessage</span><span class="sxs-lookup"><span data-stu-id="1cbc3-149">Send-AzureRemoteAppSessionMessage</span></span>
* <span data-ttu-id="1cbc3-150">Get-AzureRemoteAppProgram</span><span class="sxs-lookup"><span data-stu-id="1cbc3-150">Get-AzureRemoteAppProgram</span></span>
* <span data-ttu-id="1cbc3-151">Get-AzureRemoteAppStartMenuProgram</span><span class="sxs-lookup"><span data-stu-id="1cbc3-151">Get-AzureRemoteAppStartMenuProgram</span></span>
* <span data-ttu-id="1cbc3-152">Publish-AzureRemoteAppProgram</span><span class="sxs-lookup"><span data-stu-id="1cbc3-152">Publish-AzureRemoteAppProgram</span></span>
* <span data-ttu-id="1cbc3-153">Unpublish-AzureRemoteAppProgram</span><span class="sxs-lookup"><span data-stu-id="1cbc3-153">Unpublish-AzureRemoteAppProgram</span></span>
* <span data-ttu-id="1cbc3-154">Get-AzureRemoteAppCollectionUsageDetails</span><span class="sxs-lookup"><span data-stu-id="1cbc3-154">Get-AzureRemoteAppCollectionUsageDetails</span></span>
* <span data-ttu-id="1cbc3-155">Get-AzureRemoteAppCollectionUsageSummary</span><span class="sxs-lookup"><span data-stu-id="1cbc3-155">Get-AzureRemoteAppCollectionUsageSummary</span></span>
* <span data-ttu-id="1cbc3-156">Get-AzureRemoteAppPlan</span><span class="sxs-lookup"><span data-stu-id="1cbc3-156">Get-AzureRemoteAppPlan</span></span>

<span data-ttu-id="1cbc3-157">RemoteApp sanal ağı cmdlet:</span><span class="sxs-lookup"><span data-stu-id="1cbc3-157">RemoteApp virtual network cmdlets:</span></span>

* <span data-ttu-id="1cbc3-158">New-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="1cbc3-158">New-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="1cbc3-159">Get-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="1cbc3-159">Get-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="1cbc3-160">Set-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="1cbc3-160">Set-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="1cbc3-161">Remove-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="1cbc3-161">Remove-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="1cbc3-162">Get-AzureRemoteAppVpnDevice</span><span class="sxs-lookup"><span data-stu-id="1cbc3-162">Get-AzureRemoteAppVpnDevice</span></span>
* <span data-ttu-id="1cbc3-163">Get--AzureRemoteAppVpnDeviceConfigScript</span><span class="sxs-lookup"><span data-stu-id="1cbc3-163">Get-- AzureRemoteAppVpnDeviceConfigScript</span></span>
* <span data-ttu-id="1cbc3-164">Reset-AzureRemoteAppVpnSharedKey</span><span class="sxs-lookup"><span data-stu-id="1cbc3-164">Reset-AzureRemoteAppVpnSharedKey</span></span>

<span data-ttu-id="1cbc3-165">RemoteApp şablon görüntüsü cmdlet:</span><span class="sxs-lookup"><span data-stu-id="1cbc3-165">RemoteApp template image cmdlets:</span></span>

* <span data-ttu-id="1cbc3-166">New-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="1cbc3-166">New-AzureRemoteAppTemplateImage</span></span>
* <span data-ttu-id="1cbc3-167">Get-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="1cbc3-167">Get-AzureRemoteAppTemplateImage</span></span>
* <span data-ttu-id="1cbc3-168">Rename-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="1cbc3-168">Rename-AzureRemoteAppTemplateImage</span></span>
* <span data-ttu-id="1cbc3-169">Remove-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="1cbc3-169">Remove-AzureRemoteAppTemplateImage</span></span>

<span data-ttu-id="1cbc3-170">Diğer RemoteApp cmdlet'lerini:</span><span class="sxs-lookup"><span data-stu-id="1cbc3-170">Other RemoteApp cmdlets:</span></span>

* <span data-ttu-id="1cbc3-171">Get-AzureRemoteAppLocation</span><span class="sxs-lookup"><span data-stu-id="1cbc3-171">Get-AzureRemoteAppLocation</span></span>
* <span data-ttu-id="1cbc3-172">Get-AzureRemoteAppWorkspace</span><span class="sxs-lookup"><span data-stu-id="1cbc3-172">Get-AzureRemoteAppWorkspace</span></span>
* <span data-ttu-id="1cbc3-173">Set-AzureRemoteAppWorkspace</span><span class="sxs-lookup"><span data-stu-id="1cbc3-173">Set-AzureRemoteAppWorkspace</span></span>
* <span data-ttu-id="1cbc3-174">Get-AzureRemoteAppOperationResult</span><span class="sxs-lookup"><span data-stu-id="1cbc3-174">Get-AzureRemoteAppOperationResult</span></span>

