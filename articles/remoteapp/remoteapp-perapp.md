---
title: "aaaPublish uygulamaları tooindividual kullanıcıların bir Azure RemoteApp koleksiyonunda (Önizleme) | Microsoft Docs"
description: "Nasıl uygulamaları tooindividual kullanıcılar yerine gruplar, Azure RemoteApp bağlı olarak yayımlayabilirsiniz öğrenin."
services: remoteapp-preview
documentationcenter: 
author: piotrci
manager: mbaldwin
editor: 
ms.assetid: 1fd0539d-fa65-4ea5-a98e-0be0cf580690
ms.service: remoteapp
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 11/23/2016
ms.author: piotrci
ms.openlocfilehash: 87b435552ddbfc2c6d03aeb01d95a44985e71f9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-tooindividual-users-in-an-azure-remoteapp-collection-preview"></a><span data-ttu-id="7abd9-103">Bir Azure RemoteApp koleksiyonunda (Önizleme) uygulamaları tooindividual kullanıcılar yayımlama</span><span class="sxs-lookup"><span data-stu-id="7abd9-103">Publish applications tooindividual users in an Azure RemoteApp collection (Preview)</span></span>
> [!IMPORTANT]
> <span data-ttu-id="7abd9-104">Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır.</span><span class="sxs-lookup"><span data-stu-id="7abd9-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="7abd9-105">Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="7abd9-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="7abd9-106">Bu makalede açıklanır nasıl toopublish uygulamaları tooindividual kullanıcıların bir Azure RemoteApp koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="7abd9-106">This article explains how toopublish applications tooindividual users in an Azure RemoteApp collection.</span></span> <span data-ttu-id="7abd9-107">Azure RemoteApp, şu anda özel Önizleme ve kullanılabilir yalnızca tooselect erken Benimseyenler Değerlendirme amacıyla yeni işlevsellik budur.</span><span class="sxs-lookup"><span data-stu-id="7abd9-107">This is new functionality in Azure RemoteApp, currently in private preview and available only tooselect early adopters for evaluation purposes.</span></span>

<span data-ttu-id="7abd9-108">Başlangıçta Azure RemoteApp uygulama yayımlama için yalnızca tek yönlü etkin: Merhaba yönetici hello görüntüden uygulamaları yayımlamak ve hello koleksiyonunda görünür tooall kullanıcılar olacaktır.</span><span class="sxs-lookup"><span data-stu-id="7abd9-108">Originally Azure RemoteApp enabled only one way of publishing applications: hello administrator would publish apps from hello image and they would be visible tooall users in hello collection.</span></span>

<span data-ttu-id="7abd9-109">Birçok uygulama tek bir görüntü ve sipariş tooreduce yönetim maliyetlerini bir koleksiyona dağıtmak tooinclude buna ortak bir senaryodur.</span><span class="sxs-lookup"><span data-stu-id="7abd9-109">A common scenario is tooinclude many applications in a single image and deploy one collection in order tooreduce management costs.</span></span> <span data-ttu-id="7abd9-110">İlgili tooall kullanıcı görmemeleri tüm uygulamalardır – yöneticiler kendi uygulama Gereksiz uygulamaları görmek istemediğiniz toopublish uygulamaları tooindividual kullanıcılar tercih.</span><span class="sxs-lookup"><span data-stu-id="7abd9-110">Oftentimes not all applications are relevant tooall users – administrators would prefer toopublish apps tooindividual users so they don’t see unnecessary applications in their application feed.</span></span>

<span data-ttu-id="7abd9-111">Bu artık Azure RemoteApp’te şu anda sınırlı bir önizleme özelliği olarak mümkündür.</span><span class="sxs-lookup"><span data-stu-id="7abd9-111">This is now possible in Azure RemoteApp – currently as a limited preview feature.</span></span> <span data-ttu-id="7abd9-112">Merhaba yeni işlevsellik kısa bir özeti aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="7abd9-112">Here is a brief summary of hello new functionality:</span></span>

1. <span data-ttu-id="7abd9-113">Bir koleksiyon iki moddan birini ayarlanabilir:</span><span class="sxs-lookup"><span data-stu-id="7abd9-113">A collection can be set into one of two modes:</span></span>
   
   * <span data-ttu-id="7abd9-114">bir koleksiyondaki tüm kullanıcıların görebileceğiniz hello özgün koleksiyon modu, yayımlanan tüm uygulamaları.</span><span class="sxs-lookup"><span data-stu-id="7abd9-114">hello original collection mode, where all users in a collection can see all published applications.</span></span> <span data-ttu-id="7abd9-115">Merhaba varsayılan mod budur.</span><span class="sxs-lookup"><span data-stu-id="7abd9-115">This is hello default mode.</span></span>
   * <span data-ttu-id="7abd9-116">Burada kullanıcılar açıkça toothem atanan uygulamalar yalnızca bkz hello yeni uygulama modu</span><span class="sxs-lookup"><span data-stu-id="7abd9-116">hello new application mode, where users only see applications that have been explicitly assigned toothem</span></span>
2. <span data-ttu-id="7abd9-117">Merhaba şu anda Azure RemoteApp PowerShell cmdlet'lerini kullanarak hello uygulama modu yalnızca etkinleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="7abd9-117">At hello moment hello application mode can only be enabled using Azure RemoteApp PowerShell cmdlets.</span></span>
   
   * <span data-ttu-id="7abd9-118">Ne zaman tooapplication modunu ayarlama, kullanıcı ataması hello koleksiyonundaki hello Azure portal yönetilemez.</span><span class="sxs-lookup"><span data-stu-id="7abd9-118">When set tooapplication mode, user assignment in hello collection cannot be managed through hello Azure portal.</span></span> <span data-ttu-id="7abd9-119">Kullanıcı Ataması PowerShell cmdlet'leri aracılığıyla yönetilen toobe sahiptir.</span><span class="sxs-lookup"><span data-stu-id="7abd9-119">User assignment has toobe managed through PowerShell cmdlets.</span></span>
3. <span data-ttu-id="7abd9-120">Kullanıcılar yalnızca görürsünüz hello yayımlanan uygulamaları doğrudan toothem.</span><span class="sxs-lookup"><span data-stu-id="7abd9-120">Users will only see hello applications published directly toothem.</span></span> <span data-ttu-id="7abd9-121">Kullanıcı toolaunch hello için hello görüntüde bulunan diğer uygulamaları doğrudan hello işletim sisteminde erişerek ancak bunu hala mümkün olabilir.</span><span class="sxs-lookup"><span data-stu-id="7abd9-121">However, it may still be possible for a user toolaunch hello other applications available on hello image by accessing them directly in hello operating system.</span></span>
   
   * <span data-ttu-id="7abd9-122">Bu özellik uygulamalara güvenli bir kilitleme sağlamaz; yalnızca, akış Merhaba uygulaması görünürlüğü sınırlar.</span><span class="sxs-lookup"><span data-stu-id="7abd9-122">This feature does not provide a secure lockdown of applications; it only limits visibility in hello application feed.</span></span>
   * <span data-ttu-id="7abd9-123">Uygulamaları kullanıcılardan tooisolate gerekiyorsa, toouse ayrı koleksiyonlar için gerekir.</span><span class="sxs-lookup"><span data-stu-id="7abd9-123">If you need tooisolate users from applications, you will need toouse separate collections for that.</span></span>

## <a name="how-tooget-azure-remoteapp-powershell-cmdlets"></a><span data-ttu-id="7abd9-124">Nasıl tooget Azure RemoteApp PowerShell cmdlet'leri</span><span class="sxs-lookup"><span data-stu-id="7abd9-124">How tooget Azure RemoteApp PowerShell cmdlets</span></span>
<span data-ttu-id="7abd9-125">tootry hello yeni önizleme işlevini, toouse Azure PowerShell cmdlet'lerini gerekir.</span><span class="sxs-lookup"><span data-stu-id="7abd9-125">tootry hello new preview functionality, you will need toouse Azure PowerShell cmdlets.</span></span> <span data-ttu-id="7abd9-126">Şu anda olası toouse hello Azure Management portal tooenable hello yeni uygulama yayımlama modunu olmadığı.</span><span class="sxs-lookup"><span data-stu-id="7abd9-126">It is currently not possible toouse hello Azure Management portal tooenable hello new application publishing mode.</span></span>

<span data-ttu-id="7abd9-127">Öncelikle, hello sahip olduğunuzdan emin olun [Azure PowerShell Modülü](/powershell/azure/overview) yüklü.</span><span class="sxs-lookup"><span data-stu-id="7abd9-127">First, make sure you have hello [Azure PowerShell module](/powershell/azure/overview) installed.</span></span>

<span data-ttu-id="7abd9-128">Ardından Yönetici modunda ve aşağıdaki cmdlet'i çalıştırın hello hello PowerShell konsolunu başlatın:</span><span class="sxs-lookup"><span data-stu-id="7abd9-128">Then launch hello PowerShell console in administrator mode and run hello following cmdlet:</span></span>

        Add-AzureAccount

<span data-ttu-id="7abd9-129">Sizden Azure kullanıcı adı ve parola bilgilerini ister.</span><span class="sxs-lookup"><span data-stu-id="7abd9-129">It will prompt you for your Azure user name and password.</span></span> <span data-ttu-id="7abd9-130">Oturum açtıktan sonra Azure aboneliklerinize karşı mümkün toorun Azure RemoteApp cmdlet'lerini olacaktır.</span><span class="sxs-lookup"><span data-stu-id="7abd9-130">Once signed in, you will be able toorun Azure RemoteApp cmdlets against your Azure subscriptions.</span></span>

## <a name="how-toocheck-which-mode-a-collection-is-in"></a><span data-ttu-id="7abd9-131">Nasıl bir koleksiyon hangi modun konusu toocheck</span><span class="sxs-lookup"><span data-stu-id="7abd9-131">How toocheck which mode a collection is in</span></span>
<span data-ttu-id="7abd9-132">Hello aşağıdaki cmdlet'i çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="7abd9-132">Run hello following cmdlet:</span></span>

        Get-AzureRemoteAppCollection <collectionName>

![Merhaba koleksiyonu modunu kontrol etme](./media/remoteapp-perapp/araacllelvel.png)

<span data-ttu-id="7abd9-134">Merhaba AclLevel özelliği aşağıdaki değerleri hello sahip olabilir:</span><span class="sxs-lookup"><span data-stu-id="7abd9-134">hello AclLevel property can have hello following values:</span></span>

* <span data-ttu-id="7abd9-135">Koleksiyonu: hello özgün yayımlama modu.</span><span class="sxs-lookup"><span data-stu-id="7abd9-135">Collection: hello original publishing mode.</span></span> <span data-ttu-id="7abd9-136">Tüm kullanıcılar yayımlanan bütün uygulamaları görür.</span><span class="sxs-lookup"><span data-stu-id="7abd9-136">All users see all published apps.</span></span>
* <span data-ttu-id="7abd9-137">Uygulama: hello yeni yayımlama modu.</span><span class="sxs-lookup"><span data-stu-id="7abd9-137">Application: hello new publishing mode.</span></span> <span data-ttu-id="7abd9-138">Kullanıcılar yalnızca hello uygulamaları doğrudan toothem yayımlanan bakın.</span><span class="sxs-lookup"><span data-stu-id="7abd9-138">Users see only hello apps published directly toothem.</span></span>

## <a name="how-tooswitch-tooapplication-publishing-mode"></a><span data-ttu-id="7abd9-139">Nasıl tooswitch tooapplication yayımlama modu</span><span class="sxs-lookup"><span data-stu-id="7abd9-139">How tooswitch tooapplication publishing mode</span></span>
<span data-ttu-id="7abd9-140">Hello aşağıdaki cmdlet'i çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="7abd9-140">Run hello following cmdlet:</span></span>

        Set-AzureRemoteAppCollection -CollectionName -AclLevel Application

<span data-ttu-id="7abd9-141">Uygulama yayımlama durumu muhafaza edilir: Başlangıçta tüm kullanıcılar tüm hello özgün yayımlanan bütün uygulamaları görür.</span><span class="sxs-lookup"><span data-stu-id="7abd9-141">Application publishing state will be preserved: initially all users will see all of hello original published apps.</span></span>

## <a name="how-toolist-users-who-can-see-a-specific-application"></a><span data-ttu-id="7abd9-142">Nasıl belirli bir uygulamayı görebilen toolist kullanıcıları</span><span class="sxs-lookup"><span data-stu-id="7abd9-142">How toolist users who can see a specific application</span></span>
<span data-ttu-id="7abd9-143">Hello aşağıdaki cmdlet'i çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="7abd9-143">Run hello following cmdlet:</span></span>

        Get-AzureRemoteAppUser -CollectionName <collectionName> -Alias <appAlias>

<span data-ttu-id="7abd9-144">Bu hello uygulamayı görebilen tüm kullanıcıları listeler.</span><span class="sxs-lookup"><span data-stu-id="7abd9-144">This lists all users who can see hello application.</span></span>

<span data-ttu-id="7abd9-145">Not: Get-AzureRemoteAppProgram - CollectionName çalıştırarak hello uygulama diğer adlarını (yukarıdaki hello söz diziminde "app alias" olarak adlandırılır) görebilirsiniz <collectionName>.</span><span class="sxs-lookup"><span data-stu-id="7abd9-145">Note: You can see hello application aliases (called "app alias" in hello syntax above) by running Get-AzureRemoteAppProgram -CollectionName <collectionName>.</span></span>

## <a name="how-tooassign-an-application-tooa-user"></a><span data-ttu-id="7abd9-146">Nasıl tooassign uygulama tooa kullanıcısı</span><span class="sxs-lookup"><span data-stu-id="7abd9-146">How tooassign an application tooa user</span></span>
<span data-ttu-id="7abd9-147">Hello aşağıdaki cmdlet'i çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="7abd9-147">Run hello following cmdlet:</span></span>

        Add-AzureRemoteAppUser -CollectionName <collectionName> -UserUpn <user@domain.com> -Type <OrgId|MicrosoftAccount> -Alias <appAlias>

<span data-ttu-id="7abd9-148">Merhaba kullanıcı artık Merhaba uygulaması hello Azure RemoteApp istemcisinde görür ve mümkün tooconnect tooit olacaktır.</span><span class="sxs-lookup"><span data-stu-id="7abd9-148">hello user will now see hello application in hello Azure RemoteApp client and will be able tooconnect tooit.</span></span>

## <a name="how-tooremove-an-application-from-a-user"></a><span data-ttu-id="7abd9-149">Nasıl tooremove bir kullanıcı bir uygulamadan</span><span class="sxs-lookup"><span data-stu-id="7abd9-149">How tooremove an application from a user</span></span>
<span data-ttu-id="7abd9-150">Hello aşağıdaki cmdlet'i çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="7abd9-150">Run hello following cmdlet:</span></span>

        Remove-AzureRemoteAppUser -CollectionName <collectionName> -UserUpn <user@domain.com> -Type <OrgId|MicrosoftAccount> -Alias <appAlias>

## <a name="providing-feedback"></a><span data-ttu-id="7abd9-151">Geribildirim sağlama</span><span class="sxs-lookup"><span data-stu-id="7abd9-151">Providing feedback</span></span>
<span data-ttu-id="7abd9-152">Bu önizleme özelliğiyle ilgili teşekkür ver önerileriniz için teşekkür ederiz.</span><span class="sxs-lookup"><span data-stu-id="7abd9-152">We appreciate your feedback and suggestions regarding this preview feature.</span></span> <span data-ttu-id="7abd9-153">Lütfen hello doldurun [anket](http://www.instant.ly/s/FDdrb) Bize düşüncelerinizi toolet.</span><span class="sxs-lookup"><span data-stu-id="7abd9-153">Please fill out hello [survey](http://www.instant.ly/s/FDdrb) toolet us know what you think.</span></span>

## <a name="havent-had-a-chance-tootry-hello-preview-feature"></a><span data-ttu-id="7abd9-154">Bir fırsat tootry hello önizleme özelliği henüz oldu?</span><span class="sxs-lookup"><span data-stu-id="7abd9-154">Haven't had a chance tootry hello preview feature?</span></span>
<span data-ttu-id="7abd9-155">Hello henüz önizlemeye değil, lütfen bu kullanırsanız [anket](http://www.instant.ly/s/AY83p) toorequest erişim.</span><span class="sxs-lookup"><span data-stu-id="7abd9-155">If you have not participated in hello preview yet, please use this [survey](http://www.instant.ly/s/AY83p) toorequest access.</span></span>

