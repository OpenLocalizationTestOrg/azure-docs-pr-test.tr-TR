---
title: "Azure RemoteApp şablon görüntülerinde neler var? | Microsoft Belgeleri"
description: "Azure RemoteApp ile birlikte gelen şablon görüntüleri hakkında bilgi edinin."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 7f8442b2-81da-421e-a453-aa53ba2066b7
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 9cd4e1a16a7c42bd00d9e543d7b62b72e9de3fc8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="what-is-in-the-azure-remoteapp-template-images"></a><span data-ttu-id="f80ba-104">Azure RemoteApp şablon görüntülerinde neler var?</span><span class="sxs-lookup"><span data-stu-id="f80ba-104">What is in the Azure RemoteApp template images?</span></span>
> [!IMPORTANT]
> <span data-ttu-id="f80ba-105">Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır.</span><span class="sxs-lookup"><span data-stu-id="f80ba-105">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="f80ba-106">Ayrıntılı bilgi için [duyuruyu](https://go.microsoft.com/fwlink/?linkid=821148) okuyun.</span><span class="sxs-lookup"><span data-stu-id="f80ba-106">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="f80ba-107">Azure RemoteApp aboneliğiniz üç şablon görüntüsü içerir:</span><span class="sxs-lookup"><span data-stu-id="f80ba-107">Your Azure RemoteApp subscription includes three template images:</span></span>

* <span data-ttu-id="f80ba-108">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="f80ba-108">Windows Server 2012</span></span>
* <span data-ttu-id="f80ba-109">Microsoft Office 365 ProPlus (Office 365 aboneliği gereklidir)</span><span class="sxs-lookup"><span data-stu-id="f80ba-109">Microsoft Office 365 ProPlus (Office 365 subscription required)</span></span>
* <span data-ttu-id="f80ba-110">Microsoft Office 2013 Professional Plus (yalnızca deneme)</span><span class="sxs-lookup"><span data-stu-id="f80ba-110">Microsoft Office 2013 Professional Plus (trial only)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f80ba-111">Azure RemoteApp aboneliğiniz, ayrı bir abonelik gerektiren Office 365 ProPlus ve üretimde kullanılamayan Office 2013 dışında görüntülerdeki yazılımlara erişim sağlar.</span><span class="sxs-lookup"><span data-stu-id="f80ba-111">Your Azure RemoteApp subscription grants you access to the software in the images, with the exception of Office 365 ProPlus, which requires a separate subscription, and Office 2013, which cannot be used in production.</span></span> <span data-ttu-id="f80ba-112">Bu, şablon görüntülerindeki program veya uygulamaları kullanıcılarınızla paylaşabileceğiniz anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="f80ba-112">This means that you can share the programs or apps on the template images with your users.</span></span> <span data-ttu-id="f80ba-113">Örneğin, Windows Server 2012 R2 görüntüsünü kullanan bir koleksiyon oluşturursanız, kullanıcıların RemoteApp üzerinden erişmesi için System Center Endpoint Protection’ı yayımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f80ba-113">For example, if you create a collection that uses the Windows Server 2012 R2 image, you can publish System Center Endpoint Protection for users to access through RemoteApp.</span></span>
> 
> <span data-ttu-id="f80ba-114">Daha fazla bilgi için [RemoteApp lisanslama ayrıntılarına](remoteapp-licensing.md) bakın.</span><span class="sxs-lookup"><span data-stu-id="f80ba-114">Check out the [RemoteApp licensing details](remoteapp-licensing.md) for more information.</span></span> <span data-ttu-id="f80ba-115">Ayrıca Office lisanslama bilgileri için [Azure RemoteApp ile Office’i kullanma](remoteapp-o365.md) bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="f80ba-115">And [Using Office with Azure RemoteApp](remoteapp-o365.md) for the Office licensing info.</span></span>
> 
> 

<span data-ttu-id="f80ba-116">Her görüntünün içerdikleri ile ilgili ayrıntılar için okumaya devam edin.</span><span class="sxs-lookup"><span data-stu-id="f80ba-116">Read on for details on what each image contains.</span></span>

## <a name="windows-server-2012-r2--the-vanilla-image"></a><span data-ttu-id="f80ba-117">Windows Server 2012 R2 ("temel alınan görüntü")</span><span class="sxs-lookup"><span data-stu-id="f80ba-117">Windows Server 2012 R2  ("the vanilla image")</span></span>
<span data-ttu-id="f80ba-118">Bu görüntü Microsoft Windows Server 2012 R2 Datacenter işletim sistemini temel alır ve Azure RemoteApp şablon görüntüleri için gereksinimleri karşılamak üzere aşağıdaki roller ve özellikleri içerir:</span><span class="sxs-lookup"><span data-stu-id="f80ba-118">This image is based on Microsoft Windows Server 2012 R2 Datacenter operating system and has the following roles and features installed to meet the requirements for Azure RemoteApp template images:</span></span>

* <span data-ttu-id="f80ba-119">.NET Framework 4.5, 3.5.1, 3.5</span><span class="sxs-lookup"><span data-stu-id="f80ba-119">.NET Framework 4.5, 3.5.1, 3.5</span></span>
* <span data-ttu-id="f80ba-120">Masaüstü Deneyimi</span><span class="sxs-lookup"><span data-stu-id="f80ba-120">Desktop Experience</span></span>
* <span data-ttu-id="f80ba-121">Mürekkep ve El Yazısı Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="f80ba-121">Ink and Handwriting Services</span></span>
* <span data-ttu-id="f80ba-122">Medya Altyapısı</span><span class="sxs-lookup"><span data-stu-id="f80ba-122">Media Foundation</span></span>
* <span data-ttu-id="f80ba-123">Uzak Masaüstü Oturumu Konağı</span><span class="sxs-lookup"><span data-stu-id="f80ba-123">Remote Desktop Session Host</span></span>
* <span data-ttu-id="f80ba-124">Windows PowerShell 4.0</span><span class="sxs-lookup"><span data-stu-id="f80ba-124">Windows PowerShell 4.0</span></span>
* <span data-ttu-id="f80ba-125">Windows PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="f80ba-125">Windows PowerShell ISE</span></span>
* <span data-ttu-id="f80ba-126">WoW64 Desteği</span><span class="sxs-lookup"><span data-stu-id="f80ba-126">WoW64 Support</span></span>

<span data-ttu-id="f80ba-127">Bu görüntüde ayrıca şu uygulamalar yüklüdür:</span><span class="sxs-lookup"><span data-stu-id="f80ba-127">This image also has the following applications installed:</span></span>

* <span data-ttu-id="f80ba-128">Adobe Flash Player</span><span class="sxs-lookup"><span data-stu-id="f80ba-128">Adobe Flash Player</span></span>
* <span data-ttu-id="f80ba-129">Microsoft Silverlight</span><span class="sxs-lookup"><span data-stu-id="f80ba-129">Microsoft Silverlight</span></span>
* <span data-ttu-id="f80ba-130">Microsoft System Center 2012 Endpoint Protection</span><span class="sxs-lookup"><span data-stu-id="f80ba-130">Microsoft System Center 2012 Endpoint Protection</span></span>
* <span data-ttu-id="f80ba-131">Microsoft Windows Media Player</span><span class="sxs-lookup"><span data-stu-id="f80ba-131">Microsoft Windows Media Player</span></span>

## <a name="microsoft-office-365-proplus-subscription-required"></a><span data-ttu-id="f80ba-132">Microsoft Office 365 ProPlus (abonelik gereklidir)</span><span class="sxs-lookup"><span data-stu-id="f80ba-132">Microsoft Office 365 ProPlus (subscription required)</span></span>
<span data-ttu-id="f80ba-133">Office 365 en çok istenen uygulama olduğundan, çalışmanız için "özel" bir görüntü oluşturduk.</span><span class="sxs-lookup"><span data-stu-id="f80ba-133">Office 365 is the most requested application, so we created a "custom" image for you to work with.</span></span>

<span data-ttu-id="f80ba-134">Bu görüntü, temel alınan görüntünün bir uzantısıdır ve Windows Server 2012 R2 görüntüsünde açıklanan bileşenlere ek olarak aşağıdaki Microsoft Office 365 ProPlus bileşenlerini içerir:</span><span class="sxs-lookup"><span data-stu-id="f80ba-134">This image is an extension of the vanilla image and has the following components of Microsoft Office 365 ProPlus installed in addition to the components described in the Windows Server 2012 R2 image:</span></span>

* <span data-ttu-id="f80ba-135">Access</span><span class="sxs-lookup"><span data-stu-id="f80ba-135">Access</span></span>
* <span data-ttu-id="f80ba-136">Excel</span><span class="sxs-lookup"><span data-stu-id="f80ba-136">Excel</span></span>
* <span data-ttu-id="f80ba-137">Lync</span><span class="sxs-lookup"><span data-stu-id="f80ba-137">Lync</span></span>
* <span data-ttu-id="f80ba-138">OneNote</span><span class="sxs-lookup"><span data-stu-id="f80ba-138">OneNote</span></span>
* <span data-ttu-id="f80ba-139">OneDrive İş (eşitleme aracısının Azure RemoteApp ile kullanılması desteklenmez)</span><span class="sxs-lookup"><span data-stu-id="f80ba-139">OneDrive for Business (note that the sync agent is not supported for use with Azure RemoteApp)</span></span>
* <span data-ttu-id="f80ba-140">Outlook</span><span class="sxs-lookup"><span data-stu-id="f80ba-140">Outlook</span></span>
* <span data-ttu-id="f80ba-141">PowerPoint</span><span class="sxs-lookup"><span data-stu-id="f80ba-141">PowerPoint</span></span>
* <span data-ttu-id="f80ba-142">Word</span><span class="sxs-lookup"><span data-stu-id="f80ba-142">Word</span></span>
* <span data-ttu-id="f80ba-143">Microsoft Office Yazım Denetleme Araçları</span><span class="sxs-lookup"><span data-stu-id="f80ba-143">Microsoft Office Proofing Tools</span></span>

<span data-ttu-id="f80ba-144">Görüntü ayrıca Visio Pro ve Project Pro’yu da içerir.</span><span class="sxs-lookup"><span data-stu-id="f80ba-144">The image also includes Visio Pro and Project Pro.</span></span>

<span data-ttu-id="f80ba-145">Aşağıdaki uygulamalar da dahildir:</span><span class="sxs-lookup"><span data-stu-id="f80ba-145">And the following applications, as well:</span></span>

* <span data-ttu-id="f80ba-146">SQL Native istemcisi</span><span class="sxs-lookup"><span data-stu-id="f80ba-146">SQL Native client</span></span>
* <span data-ttu-id="f80ba-147">ODBC Sürücüsü</span><span class="sxs-lookup"><span data-stu-id="f80ba-147">ODBC Driver</span></span>
* <span data-ttu-id="f80ba-148">SQL Server Data Mining istemcisi</span><span class="sxs-lookup"><span data-stu-id="f80ba-148">SQL Server Data Mining client</span></span>
* <span data-ttu-id="f80ba-149">MasterDataServices istemcisi</span><span class="sxs-lookup"><span data-stu-id="f80ba-149">MasterDataServices client</span></span>
* <span data-ttu-id="f80ba-150">Microsoft Publisher</span><span class="sxs-lookup"><span data-stu-id="f80ba-150">Microsoft Publisher</span></span>
* <span data-ttu-id="f80ba-151">PowerQuery</span><span class="sxs-lookup"><span data-stu-id="f80ba-151">PowerQuery</span></span>
* <span data-ttu-id="f80ba-152">PowerMap</span><span class="sxs-lookup"><span data-stu-id="f80ba-152">PowerMap</span></span>

<span data-ttu-id="f80ba-153">Office 365 ProPlus uygulamalarının tüm işlevleri yalnızca bir Office 365 ProPlus planı olan kullanıcılar tarafından kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="f80ba-153">Full functionality of Office 365 ProPlus apps is available only for users who have an Office 365 ProPlus plan.</span></span> <span data-ttu-id="f80ba-154">Office 365 abonelik planları hakkında daha fazla bilgi için bkz. [Office 365 hizmet planları](http://technet.microsoft.com/library/office-365-plan-options.aspx).</span><span class="sxs-lookup"><span data-stu-id="f80ba-154">For more details on the Office 365 subscription plans see [Office 365 service plans](http://technet.microsoft.com/library/office-365-plan-options.aspx).</span></span> <span data-ttu-id="f80ba-155">Hala sorularınız mı var?</span><span class="sxs-lookup"><span data-stu-id="f80ba-155">Still have questions?</span></span> <span data-ttu-id="f80ba-156">[Office 365 + RemoteApp](remoteapp-o365.md) hakkındaki bilgilere göz atın.</span><span class="sxs-lookup"><span data-stu-id="f80ba-156">Check out the [Office 365 + RemoteApp](remoteapp-o365.md) information.</span></span> <span data-ttu-id="f80ba-157">Ayrıca [Azure RemoteApp ile Office 365 aboneliğinizi kullanma](remoteapp-officesubscription.md) başlıklı yeni makaleye de göz atın.</span><span class="sxs-lookup"><span data-stu-id="f80ba-157">Also check out the new article, [How to use your Office 365 subscription with Azure RemoteApp](remoteapp-officesubscription.md).</span></span>

<span data-ttu-id="f80ba-158">Office 365 ProPlus, Visio Pro ve Project Pro’nun kendi lisanslarına sahip olduğuna ve ayrı ayrı lisanslanmaları gerektiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="f80ba-158">Note that you need to license Office 365 ProPlus, Visio Pro, and Project Pro separately - they each have their own license.</span></span>

## <a name="microsoft-office-2013-professional-plus-trial-only"></a><span data-ttu-id="f80ba-159">Microsoft Office 2013 Professional Plus (yalnızca deneme)</span><span class="sxs-lookup"><span data-stu-id="f80ba-159">Microsoft Office 2013 Professional Plus (trial only)</span></span>
<span data-ttu-id="f80ba-160">Ücretsiz deneme süresi boyunca, hizmeti Office 2013 görüntüsüyle test edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f80ba-160">During the free trial period, you can test the service with the Office 2013 image.</span></span>

<span data-ttu-id="f80ba-161">Bu görüntü, temel alınan görüntünün bir uzantısıdır ve Windows Server 2012 R2 görüntüsünde açıklanan bileşenlere ek olarak aşağıdaki Microsoft Office 2013 Professional Plus bileşenlerini içerir:</span><span class="sxs-lookup"><span data-stu-id="f80ba-161">This image is an extension of the vanilla image and has the following components of Microsoft Office 2013 Professional Plus installed in addition to the components described in the Windows Server 2012 R2 image:</span></span>

* <span data-ttu-id="f80ba-162">Access</span><span class="sxs-lookup"><span data-stu-id="f80ba-162">Access</span></span>
* <span data-ttu-id="f80ba-163">Excel</span><span class="sxs-lookup"><span data-stu-id="f80ba-163">Excel</span></span>
* <span data-ttu-id="f80ba-164">Lync</span><span class="sxs-lookup"><span data-stu-id="f80ba-164">Lync</span></span>
* <span data-ttu-id="f80ba-165">OneNote</span><span class="sxs-lookup"><span data-stu-id="f80ba-165">OneNote</span></span>
* <span data-ttu-id="f80ba-166">OneDrive İş (eşitleme aracısının Azure RemoteApp ile kullanılması desteklenmez)</span><span class="sxs-lookup"><span data-stu-id="f80ba-166">OneDrive for Business (note that the sync agent is not supported for use with Azure RemoteApp)</span></span>
* <span data-ttu-id="f80ba-167">Outlook</span><span class="sxs-lookup"><span data-stu-id="f80ba-167">Outlook</span></span>
* <span data-ttu-id="f80ba-168">PowerPoint</span><span class="sxs-lookup"><span data-stu-id="f80ba-168">PowerPoint</span></span>
* <span data-ttu-id="f80ba-169">Project</span><span class="sxs-lookup"><span data-stu-id="f80ba-169">Project</span></span>
* <span data-ttu-id="f80ba-170">Visio</span><span class="sxs-lookup"><span data-stu-id="f80ba-170">Visio</span></span>
* <span data-ttu-id="f80ba-171">Word</span><span class="sxs-lookup"><span data-stu-id="f80ba-171">Word</span></span>
* <span data-ttu-id="f80ba-172">Microsoft Office Yazım Denetleme Araçları</span><span class="sxs-lookup"><span data-stu-id="f80ba-172">Microsoft Office Proofing Tools</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f80ba-173">**Yasal bilgiler:** Bu görüntü bir Microsoft Office lisansı içermez ve *üretim için kullanılamaz*.</span><span class="sxs-lookup"><span data-stu-id="f80ba-173">**Legal information:** This image does not include a Microsoft Office license and *cannot be used for production*.</span></span> <span data-ttu-id="f80ba-174">Office 2013 Professional Plus görüntüsü yalnızca deneme kullanımı için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="f80ba-174">The Office 2013 Professional Plus image is intended for trial use only.</span></span> <span data-ttu-id="f80ba-175">Office uygulamalarını Azure RemoteApp içinde üretim için kullanmak istiyorsanız, Office 365 ProPlus görüntüsünü kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f80ba-175">If you want to use Office apps in Azure RemoteApp for production, you need to use the Office 365 ProPlus image.</span></span> <span data-ttu-id="f80ba-176">Office’i lisanslama hakkında daha fazla bilgi için bkz. [Azure RemoteApp ile Office 365’i kullanma](remoteapp-o365.md)</span><span class="sxs-lookup"><span data-stu-id="f80ba-176">For more details on licensing Office, see [Using Office 365 with Azure RemoteApp](remoteapp-o365.md)</span></span>
> 
> 

