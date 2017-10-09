---
title: aaaAzure RemoteApp en iyi uygulamalar | Microsoft Docs
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
ms.openlocfilehash: f4d09ef30816eaebb74b69f26f3242c69ea27591
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-configuring-and-using-azure-remoteapp"></a><span data-ttu-id="bad31-103">Azure Remoteapp'in yapılandırılması ve kullanılması için en iyi uygulamalar</span><span class="sxs-lookup"><span data-stu-id="bad31-103">Best practices for configuring and using Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="bad31-104">Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır.</span><span class="sxs-lookup"><span data-stu-id="bad31-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="bad31-105">Okuma hello [duyuru](https://blogs.technet.microsoft.com/enterprisemobility/2016/08/12/application-remoting-and-the-cloud/) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="bad31-105">Read hello [announcement](https://blogs.technet.microsoft.com/enterprisemobility/2016/08/12/application-remoting-and-the-cloud/) for details.</span></span>
> 
> 

<span data-ttu-id="bad31-106">Aşağıdaki bilgilerle hello yapılandırmanıza ve Azure RemoteApp üretken kullanmanıza yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="bad31-106">hello following information can help you configure and use Azure RemoteApp productively.</span></span>

## <a name="connectivity"></a><span data-ttu-id="bad31-107">Bağlantı</span><span class="sxs-lookup"><span data-stu-id="bad31-107">Connectivity</span></span>
* <span data-ttu-id="bad31-108">Her zaman hello son istemci sürümünü kullanın.</span><span class="sxs-lookup"><span data-stu-id="bad31-108">Always use hello latest client version.</span></span> <span data-ttu-id="bad31-109">Eski istemciler kullanarak bağlantı sorunları ve diğer düşürülmüş deneyimleri neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="bad31-109">Using older clients might result in connectivity issues and other degraded experiences.</span></span> <span data-ttu-id="bad31-110">Cihazınız için otomatik uygulama güncelleştirmeleri etkinleştirme hello son istemci her zaman yüklü güvence altına alır.</span><span class="sxs-lookup"><span data-stu-id="bad31-110">Enabling automatic application updates for your device will ensure that hello latest client is always installed.</span></span>
* <span data-ttu-id="bad31-111">Her zaman hello en kararlı ve güvenilir Internet bağlantısı kullanılabilir tooyou kullanın.</span><span class="sxs-lookup"><span data-stu-id="bad31-111">Always use hello most stable and reliable internet connection available tooyou.</span></span>  
* <span data-ttu-id="bad31-112">En iyi bağlantı performans için yalnızca desteklenen proxy bağlantıları kullanın.</span><span class="sxs-lookup"><span data-stu-id="bad31-112">Use only supported proxy connections for optimal connectivity performance.</span></span>  <span data-ttu-id="bad31-113">Merhaba SOCKS proxy desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="bad31-113">hello SOCKS proxy is not supported.</span></span>

## <a name="applications"></a><span data-ttu-id="bad31-114">Uygulamalar</span><span class="sxs-lookup"><span data-stu-id="bad31-114">Applications</span></span>
* <span data-ttu-id="bad31-115">Kaydedin ve hello uygulamayla bittiğinde RemoteApp uygulamaları kapatın.</span><span class="sxs-lookup"><span data-stu-id="bad31-115">Save and close RemoteApp applications when you are done with hello application.</span></span> <span data-ttu-id="bad31-116">Merhaba uygulaması kapama değil veri kaybına neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="bad31-116">Not closing hello application might result in data loss.</span></span>
* <span data-ttu-id="bad31-117">Özel uygulamalar Azure Remoteapp'te kullanmadan önce doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="bad31-117">Validate custom applications before using them in Azure RemoteApp.</span></span> <span data-ttu-id="bad31-118">Bu bir çoklu oturum platformda çalışmak ve bellek ve başka bir kullanıcı hello tamamen Kaynaksız bırakabilir CPU gibi gereksiz kaynaklarını tüketebilir yok emin olmayı içerir aynı koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="bad31-118">This includes ensuring they work on a multi-session platform and don’t consume unnecessary resources such as memory and CPU that might starve another user in hello same collection.</span></span> <span data-ttu-id="bad31-119">Bilgi için indirme ve hello gözden [Uzak Masaüstü Hizmetleri için uygulama uyumluluk en iyi uygulamaları](http://www.dabcc.com/resources/Application%20Compatibility%20Best%20Practices%20for%20Remote%20Desktop%20Services.pdf).</span><span class="sxs-lookup"><span data-stu-id="bad31-119">For information, download and review hello [Application Compatibility Best Practices for Remote Desktop Services](http://www.dabcc.com/resources/Application%20Compatibility%20Best%20Practices%20for%20Remote%20Desktop%20Services.pdf).</span></span>

## <a name="configuration-and-management"></a><span data-ttu-id="bad31-120">Yapılandırması ve Yönetimi</span><span class="sxs-lookup"><span data-stu-id="bad31-120">Configuration and management</span></span>
* <span data-ttu-id="bad31-121">Şablon görüntülerinizi gerektiği gibi yazılım güncelleştirmeleri ve diğer önemli düzeltmelerin yüklenmesi toodate yukarı tutun.</span><span class="sxs-lookup"><span data-stu-id="bad31-121">Keep your template images up toodate, installing software updates and other critical fixes as needed.</span></span> <span data-ttu-id="bad31-122">Bu, Azure RemoteApp otomatik-toomeet ölçekler gibi her bir örnek kapasitenizi düzeltme sağlar.</span><span class="sxs-lookup"><span data-stu-id="bad31-122">This ensures that as Azure RemoteApp auto-scales toomeet your capacity, each instance is patched.</span></span>  
* <span data-ttu-id="bad31-123">Active Directory Federasyon Hizmetleri (AD FS) dağıtımınızı güvenli ve güvenilir olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="bad31-123">Make sure your Active Directory Federation Services (AD FS) deployment is secure and reliable.</span></span> <span data-ttu-id="bad31-124">Aksi takdirde istemci kimlik doğrulama, kullanıcıların Azure RemoteApp erişmesini önleme başarısız olabilir.</span><span class="sxs-lookup"><span data-stu-id="bad31-124">Otherwise client authentications might fail, preventing users from accessing Azure RemoteApp.</span></span>
* <span data-ttu-id="bad31-125">Şablon görüntüleri yüklü uygulamalar, roller veya özellikler durum bilgisiz gibi yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="bad31-125">Configure template images with installed applications, roles, or features such that they are stateless.</span></span> <span data-ttu-id="bad31-126">Merhaba sanal makinelerin durumunu sürekli bir RemoteApp Hizmeti'nin'ın tüm örneklerini dayanarak doğrulamamalısınız.</span><span class="sxs-lookup"><span data-stu-id="bad31-126">They should not rely on any instances of hello virtual machines in a RemoteApp service being in a persistent state.</span></span>
  * <span data-ttu-id="bad31-127">Şirket içi dosya paylaşımları veya OneDrive gibi kullanıcı profilleri veya diğer depolama konumları dış toohello hizmeti tüm kullanıcı verileri depolar.</span><span class="sxs-lookup"><span data-stu-id="bad31-127">Store all user data in user profiles or other storage locations external toohello service, such as on-premises file shares or OneDrive.</span></span>
  * <span data-ttu-id="bad31-128">Şirket içi dosya paylaşımları veya OneDrive gibi paylaşılan veri depolama konumları dış toohello Hizmeti'nde depolayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bad31-128">Store shared data in storage locations external toohello service, such as on-premises file shares or OneDrive.</span></span>
  * <span data-ttu-id="bad31-129">Merhaba şablon görüntüsü yerine bir hizmette tek tek sanal makinelerde hiçbir sistem genelindeki ayarları yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="bad31-129">Configure any system-wide settings in hello template image rather than on individual virtual machines in a service.</span></span>
  * <span data-ttu-id="bad31-130">Otomatik yazılım güncelleştirmeleri yayımlanan uygulamalar için devre dışı bırak - bunun yerine toohello şablon görüntüsü'bunları el ile geçerli ve hello şablondan dağıtmadan önce bunları test.</span><span class="sxs-lookup"><span data-stu-id="bad31-130">Disable automatic software updates for published applications - instead apply them manually toohello template image and test them before you deploy  from hello template.</span></span>

