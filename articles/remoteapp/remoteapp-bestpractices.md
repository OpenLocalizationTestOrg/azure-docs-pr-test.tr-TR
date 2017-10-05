---
title: Azure RemoteApp en iyi uygulamalar | Microsoft Docs
description: "Azure Remoteapp'in yapılandırılması ve kullanılması için en iyi uygulamalar."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: b851865b-bec4-4f29-82c0-7b9770c1a520
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: ab9c2dafc622e9b6f3bcd2767218cdc03e844847
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="best-practices-for-configuring-and-using-azure-remoteapp"></a><span data-ttu-id="318ef-103">Azure Remoteapp'in yapılandırılması ve kullanılması için en iyi uygulamalar</span><span class="sxs-lookup"><span data-stu-id="318ef-103">Best practices for configuring and using Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="318ef-104">Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır.</span><span class="sxs-lookup"><span data-stu-id="318ef-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="318ef-105">Ayrıntılı bilgi için [duyuruyu](https://blogs.technet.microsoft.com/enterprisemobility/2016/08/12/application-remoting-and-the-cloud/) okuyun.</span><span class="sxs-lookup"><span data-stu-id="318ef-105">Read the [announcement](https://blogs.technet.microsoft.com/enterprisemobility/2016/08/12/application-remoting-and-the-cloud/) for details.</span></span>
> 
> 

<span data-ttu-id="318ef-106">Aşağıdaki bilgiler yapılandırmanıza ve Azure RemoteApp üretken kullanmanıza yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="318ef-106">The following information can help you configure and use Azure RemoteApp productively.</span></span>

## <a name="connectivity"></a><span data-ttu-id="318ef-107">Bağlantı</span><span class="sxs-lookup"><span data-stu-id="318ef-107">Connectivity</span></span>
* <span data-ttu-id="318ef-108">Her zaman en son istemci sürümünü kullanın.</span><span class="sxs-lookup"><span data-stu-id="318ef-108">Always use the latest client version.</span></span> <span data-ttu-id="318ef-109">Eski istemciler kullanarak bağlantı sorunları ve diğer düşürülmüş deneyimleri neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="318ef-109">Using older clients might result in connectivity issues and other degraded experiences.</span></span> <span data-ttu-id="318ef-110">Cihazınız için otomatik uygulama güncelleştirmeleri etkinleştirme son istemci her zaman yüklü olduğunu güvence altına alır.</span><span class="sxs-lookup"><span data-stu-id="318ef-110">Enabling automatic application updates for your device will ensure that the latest client is always installed.</span></span>
* <span data-ttu-id="318ef-111">Her zaman kullanabileceğiniz en kararlı ve güvenilir Internet bağlantısı kullanır.</span><span class="sxs-lookup"><span data-stu-id="318ef-111">Always use the most stable and reliable internet connection available to you.</span></span>  
* <span data-ttu-id="318ef-112">En iyi bağlantı performans için yalnızca desteklenen proxy bağlantıları kullanın.</span><span class="sxs-lookup"><span data-stu-id="318ef-112">Use only supported proxy connections for optimal connectivity performance.</span></span>  <span data-ttu-id="318ef-113">SOCKS proxy desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="318ef-113">The SOCKS proxy is not supported.</span></span>

## <a name="applications"></a><span data-ttu-id="318ef-114">Uygulamalar</span><span class="sxs-lookup"><span data-stu-id="318ef-114">Applications</span></span>
* <span data-ttu-id="318ef-115">Kaydetme ve uygulama ile işiniz bittiğinde RemoteApp uygulamaları kapatın.</span><span class="sxs-lookup"><span data-stu-id="318ef-115">Save and close RemoteApp applications when you are done with the application.</span></span> <span data-ttu-id="318ef-116">Uygulama kapama değil veri kaybına neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="318ef-116">Not closing the application might result in data loss.</span></span>
* <span data-ttu-id="318ef-117">Özel uygulamalar Azure Remoteapp'te kullanmadan önce doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="318ef-117">Validate custom applications before using them in Azure RemoteApp.</span></span> <span data-ttu-id="318ef-118">Bu, çoklu oturum platformu üzerinde çalışır ve bellek ve aynı koleksiyondaki başka bir kullanıcı tamamen Kaynaksız bırakabilir CPU gibi gereksiz kaynaklarını tüketebilir yok emin olmayı içerir.</span><span class="sxs-lookup"><span data-stu-id="318ef-118">This includes ensuring they work on a multi-session platform and don’t consume unnecessary resources such as memory and CPU that might starve another user in the same collection.</span></span> <span data-ttu-id="318ef-119">Bilgi için indirebilir ve gözden [Uzak Masaüstü Hizmetleri için uygulama uyumluluk en iyi uygulamaları](http://www.dabcc.com/resources/Application%20Compatibility%20Best%20Practices%20for%20Remote%20Desktop%20Services.pdf).</span><span class="sxs-lookup"><span data-stu-id="318ef-119">For information, download and review the [Application Compatibility Best Practices for Remote Desktop Services](http://www.dabcc.com/resources/Application%20Compatibility%20Best%20Practices%20for%20Remote%20Desktop%20Services.pdf).</span></span>

## <a name="configuration-and-management"></a><span data-ttu-id="318ef-120">Yapılandırması ve Yönetimi</span><span class="sxs-lookup"><span data-stu-id="318ef-120">Configuration and management</span></span>
* <span data-ttu-id="318ef-121">Şablon görüntüleri gerektiği gibi yazılım güncelleştirmeleri ve diğer önemli düzeltmelerin yüklenmesi güncel tutun.</span><span class="sxs-lookup"><span data-stu-id="318ef-121">Keep your template images up to date, installing software updates and other critical fixes as needed.</span></span> <span data-ttu-id="318ef-122">Bu, Azure RemoteApp otomatik-kapasitenizi karşılayacak şekilde ölçekler gibi her bir örnek düzeltme sağlar.</span><span class="sxs-lookup"><span data-stu-id="318ef-122">This ensures that as Azure RemoteApp auto-scales to meet your capacity, each instance is patched.</span></span>  
* <span data-ttu-id="318ef-123">Active Directory Federasyon Hizmetleri (AD FS) dağıtımınızı güvenli ve güvenilir olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="318ef-123">Make sure your Active Directory Federation Services (AD FS) deployment is secure and reliable.</span></span> <span data-ttu-id="318ef-124">Aksi takdirde istemci kimlik doğrulama, kullanıcıların Azure RemoteApp erişmesini önleme başarısız olabilir.</span><span class="sxs-lookup"><span data-stu-id="318ef-124">Otherwise client authentications might fail, preventing users from accessing Azure RemoteApp.</span></span>
* <span data-ttu-id="318ef-125">Şablon görüntüleri yüklü uygulamalar, roller veya özellikler durum bilgisiz gibi yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="318ef-125">Configure template images with installed applications, roles, or features such that they are stateless.</span></span> <span data-ttu-id="318ef-126">Bir RemoteApp hizmetinde kalıcı bir durumda olan sanal makinelerin tüm örneklerinde güvenmemelisiniz.</span><span class="sxs-lookup"><span data-stu-id="318ef-126">They should not rely on any instances of the virtual machines in a RemoteApp service being in a persistent state.</span></span>
  * <span data-ttu-id="318ef-127">Şirket içi dosya paylaşımları veya OneDrive gibi kullanıcı profilleri veya hizmet için dış diğer depolama konumları tüm kullanıcı verileri depolar.</span><span class="sxs-lookup"><span data-stu-id="318ef-127">Store all user data in user profiles or other storage locations external to the service, such as on-premises file shares or OneDrive.</span></span>
  * <span data-ttu-id="318ef-128">Şirket içi dosya paylaşımları veya OneDrive gibi paylaşılan veri depolama konumları hizmetine dış depolayın.</span><span class="sxs-lookup"><span data-stu-id="318ef-128">Store shared data in storage locations external to the service, such as on-premises file shares or OneDrive.</span></span>
  * <span data-ttu-id="318ef-129">Şablon görüntüsü yerine bir hizmette tek tek sanal makinelerde hiçbir sistem genelindeki ayarları yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="318ef-129">Configure any system-wide settings in the template image rather than on individual virtual machines in a service.</span></span>
  * <span data-ttu-id="318ef-130">Otomatik yazılım güncelleştirmeleri yayımlanan uygulamalar için devre dışı bırak - bunun yerine bunları el ile şablon görüntüye ve şablonu dağıtmadan önce bunları test.</span><span class="sxs-lookup"><span data-stu-id="318ef-130">Disable automatic software updates for published applications - instead apply them manually to the template image and test them before you deploy  from the template.</span></span>

