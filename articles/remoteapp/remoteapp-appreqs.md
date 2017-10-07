---
title: "Azure RemoteApp için aaaApp gereksinimleri | Microsoft Docs"
description: "Azure remoteapp'te toouse istediğiniz uygulamalar için hello gereksinimleri hakkında bilgi edinin"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 4427eef6-288a-49e1-97eb-fee67d99f26a
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 3fa2bcdaab457a6fbee8ac52a81d1c4154bbdce1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="app-requirements"></a><span data-ttu-id="9ae45-103">Uygulama gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="9ae45-103">App requirements</span></span>
> [!IMPORTANT]
> <span data-ttu-id="9ae45-104">Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır.</span><span class="sxs-lookup"><span data-stu-id="9ae45-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="9ae45-105">Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="9ae45-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="9ae45-106">Azure RemoteApp akış 32 bit veya 64-bit Windows tabanlı uygulamalar bir Windows Server 2012 R2 görüntüsünden destekler.</span><span class="sxs-lookup"><span data-stu-id="9ae45-106">Azure RemoteApp supports streaming 32-bit or 64-bit Windows-based applications from a Windows Server 2012 R2 image.</span></span> <span data-ttu-id="9ae45-107">Varolan 32 bit veya 64-bit Windows tabanlı uygulamaların çoğu Azure Remoteapp'te "olduğu gibi" çalıştırın (Uzak Masaüstü Hizmetleri veya Terminal Hizmetleri önceden bilinen) ortamı.</span><span class="sxs-lookup"><span data-stu-id="9ae45-107">Most existing 32-bit or 64-bit Windows-based applications run "as is" in Azure RemoteApp (Remote Desktop Services or formerly known as Terminal Services) environment.</span></span> <span data-ttu-id="9ae45-108">Ancak, çalıştırma ve iyi çalışmasını arasında bir fark - bazı uygulamalar düzgün ve diğerlerinin desteklemediği olsa da gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="9ae45-108">However, there is a difference between running and running well - some applications function correctly and perform well, while others do not.</span></span> <span data-ttu-id="9ae45-109">Aşağıdaki bilgilerle hello bir Uzak Masaüstü Hizmetleri ortamında uygulamaları geliştirme ve test etme tooensure uyumluluk için yönergeler sağlanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="9ae45-109">hello following information provides guidance for developing applications in a Remote Desktop Services environment and testing tooensure compatibility.</span></span>

<span data-ttu-id="9ae45-110">İpucu: Bazı uygulamalar çalışma örnekleri için oluşturduğunuz üzerinde çalışıyoruz.</span><span class="sxs-lookup"><span data-stu-id="9ae45-110">Tip: We're working on creating some working examples of apps for you.</span></span> <span data-ttu-id="9ae45-111">Microsoft Access, QuickBooks ve App-V Remoteapp'te görüşmeniz yeni konular görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="9ae45-111">You'll see new topics that discuss using Microsoft Access, QuickBooks, and App-V in RemoteApp.</span></span>

## <a name="requirements"></a><span data-ttu-id="9ae45-112">Gereksinimler</span><span class="sxs-lookup"><span data-stu-id="9ae45-112">Requirements</span></span>
<span data-ttu-id="9ae45-113">Bu üç gereksinimleri izlediyseniz, iyi Remoteapp'te çalıştırmak, uygulamanızın yardımcı olur:</span><span class="sxs-lookup"><span data-stu-id="9ae45-113">These three requirements, if followed, help your application run well in RemoteApp:</span></span>

1. <span data-ttu-id="9ae45-114">Tümüne uyan uygulamalar [Windows Masaüstü uygulamaları için sertifika gereksinimleri](https://msdn.microsoft.com/library/windows/desktop/hh749939.aspx) ve çok uyması[yönergeleri programlama Uzak Masaüstü Hizmetleri](https://msdn.microsoft.com/library/aa383490.aspx) RemoteApp ile tam uyumluluk sahip olur.</span><span class="sxs-lookup"><span data-stu-id="9ae45-114">Applications that meet all [Certification requirements for Windows desktop apps](https://msdn.microsoft.com/library/windows/desktop/hh749939.aspx) and adhere too[Remote Desktop Services programming guidelines](https://msdn.microsoft.com/library/aa383490.aspx) will have complete compatibility with RemoteApp.</span></span>
2. <span data-ttu-id="9ae45-115">Uygulamaları hiç veri yerel olarak hello görüntü veya kaybolabilir RemoteApp örnekleri depolamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9ae45-115">Applications should never store data locally on hello image or RemoteApp instances that can be lost.</span></span>  <span data-ttu-id="9ae45-116">RemoteApp koleksiyonu oluşturduktan sonra hello örnekleri kopyalandığı ve durum bilgisiz ve uygulamalar yalnızca içermelidir.</span><span class="sxs-lookup"><span data-stu-id="9ae45-116">After you create a RemoteApp collection, hello instances are cloned and are stateless and should only contain applications.</span></span> <span data-ttu-id="9ae45-117">Bir dış kaynağa veya hello kullanıcının profilindeki verileri depolar.</span><span class="sxs-lookup"><span data-stu-id="9ae45-117">Store data in an external source or within hello user's profile.</span></span>
3. <span data-ttu-id="9ae45-118">Özel resimler hiçbir zaman kaybolabilir veri içermelidir.</span><span class="sxs-lookup"><span data-stu-id="9ae45-118">Custom images should never contain data that can be lost.</span></span>  

## <a name="testing-your-apps"></a><span data-ttu-id="9ae45-119">Uygulamalarınızı test etme</span><span class="sxs-lookup"><span data-stu-id="9ae45-119">Testing your apps</span></span>
<span data-ttu-id="9ae45-120">Bu adımları tootesting uygulamaları kullanın:</span><span class="sxs-lookup"><span data-stu-id="9ae45-120">Use these steps tootesting applications:</span></span>

1. <span data-ttu-id="9ae45-121">Windows Server 2012 R2 ve uygulamanızı yükleyin</span><span class="sxs-lookup"><span data-stu-id="9ae45-121">Install Windows Server 2012 R2 and your application</span></span>
2. <span data-ttu-id="9ae45-122">Uzak Masaüstü'nü etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="9ae45-122">Enable Remote Desktop</span></span>
3. <span data-ttu-id="9ae45-123">UserA ve userb adlı iki kullanıcı hesapları toohello Uzak Masaüstü güvenlik grubuna ekleme, iki kullanıcı hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9ae45-123">Create two user accounts, UserA and UserB, adding both user accounts toohello Remote Desktop security group.</span></span>
4. <span data-ttu-id="9ae45-124">İki eşzamanlı RDS oturumları toohello PC hello uygulama başlatılırken oluşturarak çoklu oturum uyumluluğunu denetleyin.</span><span class="sxs-lookup"><span data-stu-id="9ae45-124">Check multi-session compatibility by establishing two simultaneous RDS sessions toohello PC while launching hello application.</span></span>
5. <span data-ttu-id="9ae45-125">Uygulamanızın davranışını doğrula</span><span class="sxs-lookup"><span data-stu-id="9ae45-125">Validate app behavior</span></span>

## <a name="application-development-guidelines"></a><span data-ttu-id="9ae45-126">Uygulama geliştirme yönergeleri</span><span class="sxs-lookup"><span data-stu-id="9ae45-126">Application development guidelines</span></span>
<span data-ttu-id="9ae45-127">RemoteApp uygulamaları geliştirmek için yönergeleri izleyerek hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="9ae45-127">Use hello following guidelines for developing applications for RemoteApp.</span></span>

### <a name="multiple-users"></a><span data-ttu-id="9ae45-128">Birden çok kullanıcı</span><span class="sxs-lookup"><span data-stu-id="9ae45-128">Multiple users</span></span>
* <span data-ttu-id="9ae45-129">Yükleme bir [tek bir kullanıcı için uygulama ](https://msdn.microsoft.com/library/aa380661.aspx)çok kullanıcılı bir ortamda sorunlara neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="9ae45-129">Installing an [application for a single user ](https://msdn.microsoft.com/library/aa380661.aspx)can create problems in a multiuser environment.</span></span>
* <span data-ttu-id="9ae45-130">Uygulamaları gereken [kullanıcıya özgü bilgileri depolamak](https://msdn.microsoft.com/library/aa383452.aspx) kullanıcıya özgü konumlarda ayrı olarak genel bilgileri, tooall kullanıcılar geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="9ae45-130">Applications should [store user-specific information](https://msdn.microsoft.com/library/aa383452.aspx) in user-specific locations, separately from global information that applies tooall users.</span></span>
* <span data-ttu-id="9ae45-131">RemoteApp kullanan birden çok [çekirdek nesneler için ad alanları](https://msdn.microsoft.com/library/aa382954.aspx); genel ad alanı öncelikle istemci/sunucu uygulamaları hizmetleri tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9ae45-131">RemoteApp uses multiple [namespaces for kernel objects](https://msdn.microsoft.com/library/aa382954.aspx); a global namespace is used primarily by services in client/server applications.</span></span>
* <span data-ttu-id="9ae45-132">Bilgisayar adı veya hello hello güvenli tooassume değil [IP adresi](https://msdn.microsoft.com/library/aa382942.aspx) birden çok kullanıcı aynı anda tooa üzerinde Uzak Masaüstü oturumu ana bilgisayarı (RD Oturumu kaydedilebilir çünkü atanan toohello bilgisayarı tek bir kullanıcıyla ilişkili Ana bilgisayarı) sunucusu.</span><span class="sxs-lookup"><span data-stu-id="9ae45-132">It is not safe tooassume that hello computer name or hello [IP address](https://msdn.microsoft.com/library/aa382942.aspx) assigned toohello computer are associated with a single user because multiple users can be logged on simultaneously tooa Remote Desktop Session Host (RD Session Host) server.</span></span>

### <a name="performance"></a><span data-ttu-id="9ae45-133">Performans</span><span class="sxs-lookup"><span data-stu-id="9ae45-133">Performance</span></span>
* <span data-ttu-id="9ae45-134">Devre dışı [grafik efektleri](https://msdn.microsoft.com/library/aa380822.aspx) uygulama tooRemoteApp eklemeden önce.</span><span class="sxs-lookup"><span data-stu-id="9ae45-134">Disable [graphic effects](https://msdn.microsoft.com/library/aa380822.aspx) before you add your app tooRemoteApp.</span></span>
* <span data-ttu-id="9ae45-135">tüm kullanıcılar için toomaximize CPU kullanılabilirlik ya da devre dışı [arka plan görevleri ](https://msdn.microsoft.com/library/aa380665.aspx) veya kaynak kullanımı yoğun olmayan verimli arka plan görevleri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9ae45-135">toomaximize CPU availability for all users, either disable [background tasks ](https://msdn.microsoft.com/library/aa380665.aspx) or create efficient background tasks that are not resource-intensive.</span></span>
* <span data-ttu-id="9ae45-136">Ayarlama ve uygulama Bakiye [iş parçacığı kullanımı](https://msdn.microsoft.com/library/aa383520.aspx) çok kullanıcılı, çok işlemcili bir ortam için.</span><span class="sxs-lookup"><span data-stu-id="9ae45-136">You should tune and balance application [thread usage](https://msdn.microsoft.com/library/aa383520.aspx) for a multiuser, multiprocessor environment.</span></span>
* <span data-ttu-id="9ae45-137">toooptimize performans, çok uygulamalar için iyi bir uygulama olan[algılamak](https://msdn.microsoft.com/library/aa380798.aspx) çalıştırdıkları bir istemci oturumunda.</span><span class="sxs-lookup"><span data-stu-id="9ae45-137">toooptimize performance, it is good practice for applications too[detect](https://msdn.microsoft.com/library/aa380798.aspx) whether they are running in a client session.</span></span>

