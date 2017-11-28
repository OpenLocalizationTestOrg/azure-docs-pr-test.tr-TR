---
title: aaaTroubleshoot Azure RBAC | Microsoft Docs
description: "Sorunları veya soruları rol tabanlı erişim denetimi kaynaklar hakkında yardım alın."
services: azure-portal
documentationcenter: na
author: andredm7
manager: femila
ms.assetid: df42cca2-02d6-4f3c-9d56-260e1eb7dc44
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.openlocfilehash: 15feced32d8459d90c4c246d335932f90e1fc91f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="role-based-access-control-troubleshooting"></a><span data-ttu-id="ae606-103">Rol tabanlı erişim denetimi sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="ae606-103">Role-Based Access Control troubleshooting</span></span>

<span data-ttu-id="ae606-104">Hello Azure portal rollerinde hello ve erişim sorunlarını giderebilirsiniz kullanarak hangi tooexpect bilmesi belge makalede rolleri ile verilen hello özel erişim hakları hakkında sık sorulan soruları yanıtlar.</span><span class="sxs-lookup"><span data-stu-id="ae606-104">This document article answers common questions about hello specific access rights that are granted with roles, so that you know what tooexpect when using hello roles in hello Azure portal and can troubleshoot access problems.</span></span> <span data-ttu-id="ae606-105">Bu üç rol tüm kaynak türleri kapsar:</span><span class="sxs-lookup"><span data-stu-id="ae606-105">These three roles cover all resource types:</span></span>

* <span data-ttu-id="ae606-106">Sahip</span><span class="sxs-lookup"><span data-stu-id="ae606-106">Owner</span></span>  
* <span data-ttu-id="ae606-107">Katılımcı</span><span class="sxs-lookup"><span data-stu-id="ae606-107">Contributor</span></span>  
* <span data-ttu-id="ae606-108">Okuyucu</span><span class="sxs-lookup"><span data-stu-id="ae606-108">Reader</span></span>  

<span data-ttu-id="ae606-109">Tam erişim toohello yönetim deneyimi sahipleri ve katkıda bulunanları sahip ancak katılımcı erişim tooother kullanıcıları veya grupları veremez.</span><span class="sxs-lookup"><span data-stu-id="ae606-109">Owners and contributors both have full access toohello management experience, but a contributor can’t give access tooother users or groups.</span></span> <span data-ttu-id="ae606-110">Burada süre çok harcama yaptığımız böylece şeyler hello okuyucu rol ile biraz daha ilginç alın.</span><span class="sxs-lookup"><span data-stu-id="ae606-110">Things get a little more interesting with hello reader role, so that’s where we'll spend some time.</span></span> <span data-ttu-id="ae606-111">Merhaba bkz [rol tabanlı erişim denetimi get-started makale](role-based-access-control-configure.md) nasıl toogrant erişim ile ilgili ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="ae606-111">See hello [Role-Based Access Control get-started article](role-based-access-control-configure.md) for details on how toogrant access.</span></span>

## <a name="app-service-workloads"></a><span data-ttu-id="ae606-112">Uygulama hizmeti iş yükleri</span><span class="sxs-lookup"><span data-stu-id="ae606-112">App service workloads</span></span>
### <a name="write-access-capabilities"></a><span data-ttu-id="ae606-113">Yazma erişimi özellikleri</span><span class="sxs-lookup"><span data-stu-id="ae606-113">Write access capabilities</span></span>
<span data-ttu-id="ae606-114">Bir kullanıcı salt okunur erişim tooa tek bir web uygulaması vermek, beklediğiniz değil, bazı özellikler devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="ae606-114">If you grant a user read-only access tooa single web app, some features are disabled that you might not expect.</span></span> <span data-ttu-id="ae606-115">aşağıdaki yönetim özelliklerini hello gerektiren **yazma** erişim tooa web uygulaması (Katkıda bulunan veya sahibi) ve herhangi bir salt okunur senaryoda kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="ae606-115">hello following management capabilities require **write** access tooa web app (either Contributor or Owner), and aren’t available in any read-only scenario.</span></span>

* <span data-ttu-id="ae606-116">Komutları (örneğin, Başlat, Durdur, vs.)</span><span class="sxs-lookup"><span data-stu-id="ae606-116">Commands (like start, stop, etc.)</span></span>
* <span data-ttu-id="ae606-117">Genel yapılandırma, Ölçek ayarları, Yedekleme ayarlarını ve izleme ayarları gibi ayarlarını değiştirme</span><span class="sxs-lookup"><span data-stu-id="ae606-117">Changing settings like general configuration, scale settings, backup settings, and monitoring settings</span></span>
* <span data-ttu-id="ae606-118">Yayımlama kimlik bilgileri ve uygulama ayarlarının ve bağlantı dizeleri gibi diğer parolaları erişme</span><span class="sxs-lookup"><span data-stu-id="ae606-118">Accessing publishing credentials and other secrets like app settings and connection strings</span></span>
* <span data-ttu-id="ae606-119">Akış günlükleri</span><span class="sxs-lookup"><span data-stu-id="ae606-119">Streaming logs</span></span>
* <span data-ttu-id="ae606-120">Tanılama günlüklerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ae606-120">Diagnostic logs configuration</span></span>
* <span data-ttu-id="ae606-121">Konsol (komut istemi)</span><span class="sxs-lookup"><span data-stu-id="ae606-121">Console (command prompt)</span></span>
* <span data-ttu-id="ae606-122">Etkin ve en son dağıtımları (için yerel git sürekli dağıtımı)</span><span class="sxs-lookup"><span data-stu-id="ae606-122">Active and recent deployments (for local git continuous deployment)</span></span>
* <span data-ttu-id="ae606-123">Tahmini harcamanız</span><span class="sxs-lookup"><span data-stu-id="ae606-123">Estimated spend</span></span>
* <span data-ttu-id="ae606-124">Web testleri</span><span class="sxs-lookup"><span data-stu-id="ae606-124">Web tests</span></span>
* <span data-ttu-id="ae606-125">Sanal ağ (sanal ağ yazma erişimine sahip bir kullanıcı tarafından önceden yapılandırılmışsa, yalnızca görünür tooa okuyucu).</span><span class="sxs-lookup"><span data-stu-id="ae606-125">Virtual network (only visible tooa reader if a virtual network has previously been configured by a user with write access).</span></span>

<span data-ttu-id="ae606-126">Bu kutucukların erişemiyorsanız tooask katkıda bulunan erişim toohello web uygulaması için yöneticinize gerekir.</span><span class="sxs-lookup"><span data-stu-id="ae606-126">If you can't access any of these tiles, you need tooask your administrator for Contributor access toohello web app.</span></span>

### <a name="dealing-with-related-resources"></a><span data-ttu-id="ae606-127">İlgili kaynaklar postalarla</span><span class="sxs-lookup"><span data-stu-id="ae606-127">Dealing with related resources</span></span>
<span data-ttu-id="ae606-128">Web uygulamaları tarafından Interplay birkaç farklı kaynakların hello varlığı karmaşık.</span><span class="sxs-lookup"><span data-stu-id="ae606-128">Web apps are complicated by hello presence of a few different resources that interplay.</span></span> <span data-ttu-id="ae606-129">Birkaç Web sitelerini tipik kaynak grubuyla şöyledir:</span><span class="sxs-lookup"><span data-stu-id="ae606-129">Here is a typical resource group with a couple websites:</span></span>

![Web uygulaması kaynak grubu](./media/role-based-access-control-troubleshooting/website-resource-model.png)

<span data-ttu-id="ae606-131">Erişim toojust hello web uygulaması vermeniz, sonuç olarak, hello Web sitesi dikey penceresinde hello Azure portalı üzerinde hello işlevlerinin çoğunu devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="ae606-131">As a result, if you grant someone access toojust hello web app, much of hello functionality on hello website blade in hello Azure portal is disabled.</span></span>

<span data-ttu-id="ae606-132">Bu öğeler gerektiren **yazma** toohello erişim **uygulama hizmeti planı** tooyour Web sitesi karşılık gelen:</span><span class="sxs-lookup"><span data-stu-id="ae606-132">These items require **write** access toohello **App Service plan** that corresponds tooyour website:</span></span>  

* <span data-ttu-id="ae606-133">Görüntüleme hello web uygulaması fiyatlandırma Katmanı (ücretsiz veya standart)</span><span class="sxs-lookup"><span data-stu-id="ae606-133">Viewing hello web app’s pricing tier (Free or Standard)</span></span>  
* <span data-ttu-id="ae606-134">Ölçek yapılandırma (örnekleri, sanal makine boyutu, otomatik ölçeklendirme ayarlarını sayısı)</span><span class="sxs-lookup"><span data-stu-id="ae606-134">Scale configuration (number of instances, virtual machine size, autoscale settings)</span></span>  
* <span data-ttu-id="ae606-135">Kotalar (depolama, bant genişliği, CPU)</span><span class="sxs-lookup"><span data-stu-id="ae606-135">Quotas (storage, bandwidth, CPU)</span></span>  

<span data-ttu-id="ae606-136">Bu öğeler gerektiren **yazma** erişim toohello tüm **kaynak grubu** Web sitenizi içerir:</span><span class="sxs-lookup"><span data-stu-id="ae606-136">These items require **write** access toohello whole **Resource group** that contains your website:</span></span>  

* <span data-ttu-id="ae606-137">SSL sertifikaları ve bağlamaları (SSL sertifikalarını hello siteler arasında paylaşılabilir aynı kaynak grubunu ve coğrafi konum)</span><span class="sxs-lookup"><span data-stu-id="ae606-137">SSL Certificates and bindings (SSL certificates can be shared between sites in hello same resource group and geo-location)</span></span>  
* <span data-ttu-id="ae606-138">Uyarı kuralları</span><span class="sxs-lookup"><span data-stu-id="ae606-138">Alert rules</span></span>  
* <span data-ttu-id="ae606-139">otomatik ölçeklendirme ayarları</span><span class="sxs-lookup"><span data-stu-id="ae606-139">Autoscale settings</span></span>  
* <span data-ttu-id="ae606-140">Uygulama Öngörüler bileşenleri</span><span class="sxs-lookup"><span data-stu-id="ae606-140">Application insights components</span></span>  
* <span data-ttu-id="ae606-141">Web testleri</span><span class="sxs-lookup"><span data-stu-id="ae606-141">Web tests</span></span>  

## <a name="virtual-machine-workloads"></a><span data-ttu-id="ae606-142">Sanal makine iş yükleri</span><span class="sxs-lookup"><span data-stu-id="ae606-142">Virtual machine workloads</span></span>
<span data-ttu-id="ae606-143">Çok gibi web apps ile bazı özellikler hello sanal makine dikey yazma erişimi toohello sanal makine ya da tooother kaynakları hello kaynak grubunda gerektirir.</span><span class="sxs-lookup"><span data-stu-id="ae606-143">Much like with web apps, some features on hello virtual machine blade require write access toohello virtual machine, or tooother resources in hello resource group.</span></span>

<span data-ttu-id="ae606-144">Sanal makine ilgili tooDomain adları, sanal ağlar, depolama hesapları ve uyarı kuralları yok.</span><span class="sxs-lookup"><span data-stu-id="ae606-144">Virtual machines are related tooDomain names, virtual networks, storage accounts, and alert rules.</span></span>

<span data-ttu-id="ae606-145">Bu öğeler gerektiren **yazma** toohello erişim **sanal makine**:</span><span class="sxs-lookup"><span data-stu-id="ae606-145">These items require **write** access toohello **Virtual machine**:</span></span>

* <span data-ttu-id="ae606-146">Uç Noktalar</span><span class="sxs-lookup"><span data-stu-id="ae606-146">Endpoints</span></span>  
* <span data-ttu-id="ae606-147">IP adresleri</span><span class="sxs-lookup"><span data-stu-id="ae606-147">IP addresses</span></span>  
* <span data-ttu-id="ae606-148">Diskler</span><span class="sxs-lookup"><span data-stu-id="ae606-148">Disks</span></span>  
* <span data-ttu-id="ae606-149">Uzantılar</span><span class="sxs-lookup"><span data-stu-id="ae606-149">Extensions</span></span>  

<span data-ttu-id="ae606-150">Bunlar **yazma** erişim tooboth hello **sanal makine**ve hello **kaynak grubu** (Merhaba etki alanı adı ile birlikte), BT zamanı:</span><span class="sxs-lookup"><span data-stu-id="ae606-150">These require **write** access tooboth hello **Virtual machine**, and hello **Resource group** (along with hello Domain name) that it is in:</span></span>  

* <span data-ttu-id="ae606-151">Kullanılabilirlik kümesi</span><span class="sxs-lookup"><span data-stu-id="ae606-151">Availability set</span></span>  
* <span data-ttu-id="ae606-152">Yük dengeli kümesi</span><span class="sxs-lookup"><span data-stu-id="ae606-152">Load balanced set</span></span>  
* <span data-ttu-id="ae606-153">Uyarı kuralları</span><span class="sxs-lookup"><span data-stu-id="ae606-153">Alert rules</span></span>  

<span data-ttu-id="ae606-154">Bu kutucukların erişemiyorsanız yöneticinize katkıda bulunan erişim toohello kaynak grubu için isteyin.</span><span class="sxs-lookup"><span data-stu-id="ae606-154">If you can't access any of these tiles, ask your administrator for Contributor access toohello Resource group.</span></span>

## <a name="see-more"></a><span data-ttu-id="ae606-155">Diğerlerini görüntüle</span><span class="sxs-lookup"><span data-stu-id="ae606-155">See more</span></span>
* <span data-ttu-id="ae606-156">[Rol tabanlı erişim denetimi](role-based-access-control-configure.md): hello Azure portalında RBAC ile çalışmaya başlama.</span><span class="sxs-lookup"><span data-stu-id="ae606-156">[Role Based Access Control](role-based-access-control-configure.md): Get started with RBAC in hello Azure portal.</span></span>
* <span data-ttu-id="ae606-157">[Yerleşik roller](role-based-access-built-in-roles.md): Get RBAC standart gelen hello rolleri hakkında ayrıntılar.</span><span class="sxs-lookup"><span data-stu-id="ae606-157">[Built-in roles](role-based-access-built-in-roles.md): Get details about hello roles that come standard in RBAC.</span></span>
* <span data-ttu-id="ae606-158">[Azure rbac'de özel roller](role-based-access-control-custom-roles.md): toocreate özel roller toofit erişiminizi nasıl gerektiğini öğrenin.</span><span class="sxs-lookup"><span data-stu-id="ae606-158">[Custom roles in Azure RBAC](role-based-access-control-custom-roles.md): Learn how toocreate custom roles toofit your access needs.</span></span>
* <span data-ttu-id="ae606-159">[Erişim değişiklik geçmişi raporu oluşturma](role-based-access-control-access-change-history-report.md): RBAC içinde rol atamalarını değiştirme izler.</span><span class="sxs-lookup"><span data-stu-id="ae606-159">[Create an access change history report](role-based-access-control-access-change-history-report.md): Keep track of changing role assignments in RBAC.</span></span>

