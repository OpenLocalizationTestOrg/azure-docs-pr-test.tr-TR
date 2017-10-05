---
title: "En iyi güvenlik uygulamalarını, noktalar, Internet | Microsoft Docs"
description: "Makaleyi seçkin Microsoft Internet şeyler en iyi güvenlik uygulamaları ve genel öneriler listesini sağlar."
services: security
documentationcenter: na
author: TomShinder
manager: StevenPo
editor: TomSh
ms.assetid: 2d5598c5-4c30-481d-b8f4-51ee024ea9a7
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/04/2017
ms.author: yurid
ms.openlocfilehash: 8efc0053458e338ac1afe98d9ce970c1d5cbfa81
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="internet-of-things-security-best-practices"></a><span data-ttu-id="7fc42-103">En iyi güvenlik uygulamalarını, noktalar, Internet</span><span class="sxs-lookup"><span data-stu-id="7fc42-103">Internet of Things Security Best Practices</span></span>
<span data-ttu-id="7fc42-104">Nesnelerin interneti (IOT) altyapısını koruma çözümlere dahil herkes için kritik bir iş değil.</span><span class="sxs-lookup"><span data-stu-id="7fc42-104">Securing the Internet of Things (IoT) infrastructure is a critical undertaking for anyone involved with IoT solutions.</span></span> <span data-ttu-id="7fc42-105">Cihazı dahil sayısı ve bu cihazların dağıtılan yapı, nedeniyle bir güvenlik olayı IOT cihazları milyonlarca tehlikeye ilgili etkisi Önemsiz olmayan ve yaygın etkisi olabilir.</span><span class="sxs-lookup"><span data-stu-id="7fc42-105">Because of the number of devices involved and the distributed nature of these devices, the impact a security event related to compromise of millions of IoT devices is non-trivial and can have widespread impact.</span></span>

<span data-ttu-id="7fc42-106">Bu nedenle, bir güvenlik derinlemesine yaklaşım IOT güvenlik gerekir.</span><span class="sxs-lookup"><span data-stu-id="7fc42-106">For this reason, IoT security needs a security-in-depth approach.</span></span> <span data-ttu-id="7fc42-107">Verileri bulutta güvenli olması gerekir ve özel ve genel ağları üzerinden hareket ederken.</span><span class="sxs-lookup"><span data-stu-id="7fc42-107">Data needs to be secure in the cloud and as it moves over private and public networks.</span></span> <span data-ttu-id="7fc42-108">Yöntemleri IOT cihazları güvenli bir şekilde sağlamak için karşılanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="7fc42-108">Methods need to be in place to securely provision the IoT devices themselves.</span></span> <span data-ttu-id="7fc42-109">Her katman, aygıttan ağına arka uç bulut güçlü güvenlik çıkışların gerekir.</span><span class="sxs-lookup"><span data-stu-id="7fc42-109">Each layer, from device, to network, to cloud back-end needs strong security assurances.</span></span>

<span data-ttu-id="7fc42-110">IOT en iyi yöntemler aşağıdaki gibi kategorilere ayrılabilir:</span><span class="sxs-lookup"><span data-stu-id="7fc42-110">IoT best practices can be categorized in the following way:</span></span>

* <span data-ttu-id="7fc42-111">IOT donanım üreticisi veya Tümleştirici</span><span class="sxs-lookup"><span data-stu-id="7fc42-111">IoT hardware manufacturer or integrator</span></span>
* <span data-ttu-id="7fc42-112">IOT Çözüm geliştiricisi</span><span class="sxs-lookup"><span data-stu-id="7fc42-112">IoT solution developer</span></span>
* <span data-ttu-id="7fc42-113">IOT çözüm dağıtıcı</span><span class="sxs-lookup"><span data-stu-id="7fc42-113">IoT solution deployer</span></span>
* <span data-ttu-id="7fc42-114">IOT çözüm işleci</span><span class="sxs-lookup"><span data-stu-id="7fc42-114">IoT solution operator</span></span>

<span data-ttu-id="7fc42-115">Bu makalede özetlenmektedir [Internet, şeyler en iyi güvenlik uygulamaları](../iot-suite/iot-security-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="7fc42-115">This article summarizes [Internet of Things Security Best Practices](../iot-suite/iot-security-best-practices.md).</span></span> <span data-ttu-id="7fc42-116">Lütfen daha ayrıntılı bilgi için bu makalesine bakın.</span><span class="sxs-lookup"><span data-stu-id="7fc42-116">Please refer to that article for more detailed information.</span></span>

## <a name="iot-hardware-manufacturer-or-integrator"></a><span data-ttu-id="7fc42-117">IOT donanım üreticisi veya Tümleştirici</span><span class="sxs-lookup"><span data-stu-id="7fc42-117">IoT hardware manufacturer or integrator</span></span>
<span data-ttu-id="7fc42-118">Bir IOT donanım üreticisine veya donanım Tümleştirici ise en iyi uygulamaları izleyin:</span><span class="sxs-lookup"><span data-stu-id="7fc42-118">Follow the best practices below if you are an IoT hardware manufacture or a hardware integrator:</span></span>

* <span data-ttu-id="7fc42-119">**Kapsam en düşük gereksinimler için donanım**: donanım tasarımı donanım ve hiçbir şey daha fazla işlem için gereken en düşük özellikleri içermelidir.</span><span class="sxs-lookup"><span data-stu-id="7fc42-119">**Scope hardware to minimum requirements**: the hardware design should include minimum features required for operation of the hardware, and nothing more.</span></span> 
* <span data-ttu-id="7fc42-120">**Kanıt değiştirmesine donanım olun**: fiziksel aygıt, vb. parçası kaldırarak cihaz Kapak açma gibi donanım, izinsiz algılamak için mekanizmaları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7fc42-120">**Make hardware tamper proof**: build in mechanisms to detect physical tampering of hardware, such as opening the device cover, removing a part of the device, etc.</span></span> 
* <span data-ttu-id="7fc42-121">**Güvenli donanım yapı**: varsa [SMM](https://en.wikipedia.org/wiki/Cost_of_goods_sold) izin, güvenli ve şifrelenmiş depolama ve Güvenilir Platform Modülü TPM tabanlı önyükleme işlevleri gibi güvenlik özellikleri yapı.</span><span class="sxs-lookup"><span data-stu-id="7fc42-121">**Build around secure hardware**: if [COGS](https://en.wikipedia.org/wiki/Cost_of_goods_sold) permit, build security features such as secure and encrypted storage and Trusted Platform Module (TPM)-based boot functionality.</span></span>
* <span data-ttu-id="7fc42-122">**Yükseltmeler güvenli hale**: cihaz ömrü boyunca bellenimi yükseltmek kaçınılmaz.</span><span class="sxs-lookup"><span data-stu-id="7fc42-122">**Make upgrades secure**: upgrading firmware during lifetime of the device is inevitable.</span></span>

## <a name="iot-solution-developer"></a><span data-ttu-id="7fc42-123">IOT Çözüm geliştiricisi</span><span class="sxs-lookup"><span data-stu-id="7fc42-123">IoT solution developer</span></span>
<span data-ttu-id="7fc42-124">Bir IOT çözüm geliştirici varsa en iyi uygulamaları izleyin:</span><span class="sxs-lookup"><span data-stu-id="7fc42-124">Follow the best practices below if you are an IoT solution developer:</span></span>

* <span data-ttu-id="7fc42-125">**Güvenli yazılım geliştirme metodolojisini izleyin**: Güvenli yazılım geliştirme, kendi uygulama, test ve dağıtım için tüm proje başlangıcından güvenlik başından başlayarak yukarı düşünmek gerektirir.</span><span class="sxs-lookup"><span data-stu-id="7fc42-125">**Follow secure software development methodology**: developing secure software requires ground-up thinking about security from the inception of the project all the way to its implementation, testing, and deployment.</span></span>
* <span data-ttu-id="7fc42-126">**Açık kaynak yazılımının dikkatle seçin**: açık kaynak yazılımının hızla çözümleri geliştirmek için bir fırsat sağlar.</span><span class="sxs-lookup"><span data-stu-id="7fc42-126">**Choose open source software with care**: open source software provides an opportunity to quickly develop solutions.</span></span>
* <span data-ttu-id="7fc42-127">**Dikkatli tümleştirmek**: çoğu yazılım güvenlik açıkları kitaplıklarını ve API'lerini sınırında mevcut.</span><span class="sxs-lookup"><span data-stu-id="7fc42-127">**Integrate with care**: many of the software security flaws exist at the boundary of libraries and APIs.</span></span> 

## <a name="iot-solution-deployer"></a><span data-ttu-id="7fc42-128">IOT çözüm dağıtıcı</span><span class="sxs-lookup"><span data-stu-id="7fc42-128">IoT solution deployer</span></span>
<span data-ttu-id="7fc42-129">Bir IOT çözüm dağıtıcı varsa en iyi uygulamaları izleyin:</span><span class="sxs-lookup"><span data-stu-id="7fc42-129">Follow the best practices below if you are an IoT solution deployer:</span></span>

* <span data-ttu-id="7fc42-130">**Donanım güvenli bir şekilde dağıtmak**: IOT dağıtımları ortak alanları ya da Denetimsiz yerel ayarlara olduğu gibi güvenli olmayan konumlarda dağıtılacak donanım gerektirebilir.</span><span class="sxs-lookup"><span data-stu-id="7fc42-130">**Deploy hardware securely**: IoT deployments may require hardware to be deployed in unsecure locations, such as in public spaces or unsupervised locales.</span></span>
* <span data-ttu-id="7fc42-131">**Kimlik doğrulama anahtarlarını güvenli kalmasına**: dağıtım sırasında her cihaz cihaz kimlikleri gerektirir ve kimlik doğrulaması anahtarları bulut hizmeti tarafından oluşturulan ilişkili.</span><span class="sxs-lookup"><span data-stu-id="7fc42-131">**Keep authentication keys safe**: during deployment, each device requires device IDs and associated authentication keys generated by the cloud service.</span></span> <span data-ttu-id="7fc42-132">Bu anahtarları daha sonra dağıtım fiziksel olarak güvenli tutun.</span><span class="sxs-lookup"><span data-stu-id="7fc42-132">Keep these keys physically safe even after the deployment.</span></span> <span data-ttu-id="7fc42-133">Güvenliği aşılmış bir tuşa kötü amaçlı bir aygıt tarafından geçici var olan bir cihaz için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="7fc42-133">Any compromised key can be used by a malicious device to masquerade as an existing device.</span></span>

## <a name="iot-solution-operator"></a><span data-ttu-id="7fc42-134">IOT çözüm işleci</span><span class="sxs-lookup"><span data-stu-id="7fc42-134">IoT solution operator</span></span>
<span data-ttu-id="7fc42-135">Bir IOT çözüm işleç varsa en iyi uygulamaları izleyin:</span><span class="sxs-lookup"><span data-stu-id="7fc42-135">Follow the best practices below if you are an IoT solution operator:</span></span>

* <span data-ttu-id="7fc42-136">**Sistemleri güncel tutmak**: cihaz işletim sistemleri ve tüm aygıt sürücülerini en son sürümüne güncelleştirilir emin olun.</span><span class="sxs-lookup"><span data-stu-id="7fc42-136">**Keep systems up to date**: ensure device operating systems and all device drivers are updated to the latest versions.</span></span> 
* <span data-ttu-id="7fc42-137">**Kötü amaçlı etkinliği karşı koruma**: işletim sistemi izin veriliyorsa, her cihaz işletim sisteminde en son virüsten koruma ve kötü amaçlı yazılımdan özellikleri yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="7fc42-137">**Protect against malicious activity**: if the operating system permits, place the latest anti-virus and anti-malware capabilities on each device operating system.</span></span> 
* <span data-ttu-id="7fc42-138">**Sık denetim**: güvenlik sorunları olduğunda anahtar güvenlik olaylarını yanıtlama ilgili IOT altyapı denetleme.</span><span class="sxs-lookup"><span data-stu-id="7fc42-138">**Audit frequently**: auditing IoT infrastructure for security related issues is key when responding to security incidents.</span></span>
* <span data-ttu-id="7fc42-139">**Fiziksel olarak IOT altyapısını koruma**: cihazlara fiziksel erişim kullanarak IOT altyapı kötü güvenlik saldırıları başlatılabilir.</span><span class="sxs-lookup"><span data-stu-id="7fc42-139">**Physically protect the IoT infrastructure**: the worst security attacks against IoT infrastructure are launched using physical access to devices.</span></span>
* <span data-ttu-id="7fc42-140">**Bulut kimlik bilgileri korumaya**: Bulut kimlik doğrulaması kimlik bilgilerini yapılandırmak ve bir IOT dağıtım işletim için kullanılan olan büyük olasılıkla erişebilir ve bir IOT sistemden yapmanın en kolay yolu.</span><span class="sxs-lookup"><span data-stu-id="7fc42-140">**Protect cloud credentials**: cloud authentication credentials used for configuring and operating an IoT deployment are possibly the easiest way to gain access and compromise an IoT system.</span></span> 

