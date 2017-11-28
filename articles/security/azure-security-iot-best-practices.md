---
title: "en iyi güvenlik uygulamalarını, şeyler aaaInternet | Microsoft Docs"
description: "Merhaba makale seçkin Microsoft Internet şeyler en iyi güvenlik uygulamaları ve genel öneriler listesini sağlar."
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
ms.openlocfilehash: 7ee31c912e8ac230ffa5efcd5b4c2b0b0713584f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="internet-of-things-security-best-practices"></a><span data-ttu-id="4aea3-103">En iyi güvenlik uygulamalarını, noktalar, Internet</span><span class="sxs-lookup"><span data-stu-id="4aea3-103">Internet of Things Security Best Practices</span></span>
<span data-ttu-id="4aea3-104">Güvenliğini sağlama hello nesnelerin interneti (IOT) altyapısı çözümlere dahil herkes için kritik bir iş değil.</span><span class="sxs-lookup"><span data-stu-id="4aea3-104">Securing hello Internet of Things (IoT) infrastructure is a critical undertaking for anyone involved with IoT solutions.</span></span> <span data-ttu-id="4aea3-105">Merhaba ve cihazı dahil Hello sayısı nedeniyle, bu cihazların Merhaba etkisi bir güvenlik olayı dağıtılan yapı toocompromise milyonlarca IOT cihazları Önemsiz olmayan ve yaygın etkisi olabilir ilgili.</span><span class="sxs-lookup"><span data-stu-id="4aea3-105">Because of hello number of devices involved and hello distributed nature of these devices, hello impact a security event related toocompromise of millions of IoT devices is non-trivial and can have widespread impact.</span></span>

<span data-ttu-id="4aea3-106">Bu nedenle, bir güvenlik derinlemesine yaklaşım IOT güvenlik gerekir.</span><span class="sxs-lookup"><span data-stu-id="4aea3-106">For this reason, IoT security needs a security-in-depth approach.</span></span> <span data-ttu-id="4aea3-107">Veri gereksinimlerini toobe güvenli hello bulutta ve şekliyle özel ve genel ağları üzerinden taşır.</span><span class="sxs-lookup"><span data-stu-id="4aea3-107">Data needs toobe secure in hello cloud and as it moves over private and public networks.</span></span> <span data-ttu-id="4aea3-108">Yöntemleri yer toosecurely hello IOT cihazları sağlamak kendilerini toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="4aea3-108">Methods need toobe in place toosecurely provision hello IoT devices themselves.</span></span> <span data-ttu-id="4aea3-109">Aygıt, toonetwork, toocloud arka uç her katman güçlü güvenlik çıkışların gerekir.</span><span class="sxs-lookup"><span data-stu-id="4aea3-109">Each layer, from device, toonetwork, toocloud back-end needs strong security assurances.</span></span>

<span data-ttu-id="4aea3-110">IOT en iyi yöntemler hello yolu aşağıdaki kategorilere ayrılabilir:</span><span class="sxs-lookup"><span data-stu-id="4aea3-110">IoT best practices can be categorized in hello following way:</span></span>

* <span data-ttu-id="4aea3-111">IOT donanım üreticisi veya Tümleştirici</span><span class="sxs-lookup"><span data-stu-id="4aea3-111">IoT hardware manufacturer or integrator</span></span>
* <span data-ttu-id="4aea3-112">IOT Çözüm geliştiricisi</span><span class="sxs-lookup"><span data-stu-id="4aea3-112">IoT solution developer</span></span>
* <span data-ttu-id="4aea3-113">IOT çözüm dağıtıcı</span><span class="sxs-lookup"><span data-stu-id="4aea3-113">IoT solution deployer</span></span>
* <span data-ttu-id="4aea3-114">IOT çözüm işleci</span><span class="sxs-lookup"><span data-stu-id="4aea3-114">IoT solution operator</span></span>

<span data-ttu-id="4aea3-115">Bu makalede özetlenmektedir [Internet, şeyler en iyi güvenlik uygulamaları](../iot-suite/iot-security-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="4aea3-115">This article summarizes [Internet of Things Security Best Practices](../iot-suite/iot-security-best-practices.md).</span></span> <span data-ttu-id="4aea3-116">Daha ayrıntılı bilgi için lütfen toothat makalesine bakın.</span><span class="sxs-lookup"><span data-stu-id="4aea3-116">Please refer toothat article for more detailed information.</span></span>

## <a name="iot-hardware-manufacturer-or-integrator"></a><span data-ttu-id="4aea3-117">IOT donanım üreticisi veya Tümleştirici</span><span class="sxs-lookup"><span data-stu-id="4aea3-117">IoT hardware manufacturer or integrator</span></span>
<span data-ttu-id="4aea3-118">Bir IOT donanım üreticisine veya donanım Tümleştirici varsa hello aşağıdaki en iyi uygulamaları izleyin:</span><span class="sxs-lookup"><span data-stu-id="4aea3-118">Follow hello best practices below if you are an IoT hardware manufacture or a hardware integrator:</span></span>

* <span data-ttu-id="4aea3-119">**Kapsam donanım toominimum gereksinimleri**: hello donanım tasarımı hello donanım ve hiçbir şey daha fazla işlem için gereken en düşük özellikleri içermelidir.</span><span class="sxs-lookup"><span data-stu-id="4aea3-119">**Scope hardware toominimum requirements**: hello hardware design should include minimum features required for operation of hello hardware, and nothing more.</span></span> 
* <span data-ttu-id="4aea3-120">**Kanıt değiştirmesine donanım olun**: mekanizmaları toodetect fiziksel hello aygıt, vb. parçası kaldırma hello aygıt Kapak açma gibi donanım, izinsiz olarak oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4aea3-120">**Make hardware tamper proof**: build in mechanisms toodetect physical tampering of hardware, such as opening hello device cover, removing a part of hello device, etc.</span></span> 
* <span data-ttu-id="4aea3-121">**Güvenli donanım yapı**: varsa [SMM](https://en.wikipedia.org/wiki/Cost_of_goods_sold) izin, güvenli ve şifrelenmiş depolama ve Güvenilir Platform Modülü TPM tabanlı önyükleme işlevleri gibi güvenlik özellikleri yapı.</span><span class="sxs-lookup"><span data-stu-id="4aea3-121">**Build around secure hardware**: if [COGS](https://en.wikipedia.org/wiki/Cost_of_goods_sold) permit, build security features such as secure and encrypted storage and Trusted Platform Module (TPM)-based boot functionality.</span></span>
* <span data-ttu-id="4aea3-122">**Yükseltmeler güvenli hale**: hello aygıt ömrü boyunca bellenimi yükseltmek kaçınılmaz.</span><span class="sxs-lookup"><span data-stu-id="4aea3-122">**Make upgrades secure**: upgrading firmware during lifetime of hello device is inevitable.</span></span>

## <a name="iot-solution-developer"></a><span data-ttu-id="4aea3-123">IOT Çözüm geliştiricisi</span><span class="sxs-lookup"><span data-stu-id="4aea3-123">IoT solution developer</span></span>
<span data-ttu-id="4aea3-124">Bir IOT çözüm geliştirici iseniz hello aşağıdaki en iyi uygulamaları izleyin:</span><span class="sxs-lookup"><span data-stu-id="4aea3-124">Follow hello best practices below if you are an IoT solution developer:</span></span>

* <span data-ttu-id="4aea3-125">**Güvenli yazılım geliştirme metodolojisini izleyin**: Güvenli yazılım geliştirme başından başlayarak yukarı hello projesinin hello başlangıcından güvenliği hakkında tüm hello yolu tooits uygulaması, test ve dağıtım düşünüyorum gerektirir.</span><span class="sxs-lookup"><span data-stu-id="4aea3-125">**Follow secure software development methodology**: developing secure software requires ground-up thinking about security from hello inception of hello project all hello way tooits implementation, testing, and deployment.</span></span>
* <span data-ttu-id="4aea3-126">**Açık kaynak yazılımının dikkatle seçin**: açık kaynak yazılımının fırsatı sağlar tooquickly çözümleri geliştirin.</span><span class="sxs-lookup"><span data-stu-id="4aea3-126">**Choose open source software with care**: open source software provides an opportunity tooquickly develop solutions.</span></span>
* <span data-ttu-id="4aea3-127">**Dikkatli tümleştirmek**: hello yazılım güvenlik açıkları çoğunu kitaplıklarını ve API'lerini hello sınırında mevcut.</span><span class="sxs-lookup"><span data-stu-id="4aea3-127">**Integrate with care**: many of hello software security flaws exist at hello boundary of libraries and APIs.</span></span> 

## <a name="iot-solution-deployer"></a><span data-ttu-id="4aea3-128">IOT çözüm dağıtıcı</span><span class="sxs-lookup"><span data-stu-id="4aea3-128">IoT solution deployer</span></span>
<span data-ttu-id="4aea3-129">Bir IOT çözüm dağıtıcı varsa hello aşağıdaki en iyi uygulamaları izleyin:</span><span class="sxs-lookup"><span data-stu-id="4aea3-129">Follow hello best practices below if you are an IoT solution deployer:</span></span>

* <span data-ttu-id="4aea3-130">**Donanım güvenli bir şekilde dağıtmak**: IOT dağıtımları ortak alanları ya da Denetimsiz yerel ayarlara olduğu gibi güvenli olmayan konumlarda dağıtılan donanım toobe gerektirebilir.</span><span class="sxs-lookup"><span data-stu-id="4aea3-130">**Deploy hardware securely**: IoT deployments may require hardware toobe deployed in unsecure locations, such as in public spaces or unsupervised locales.</span></span>
* <span data-ttu-id="4aea3-131">**Kimlik doğrulama anahtarlarını güvenli kalmasına**: dağıtım sırasında her aygıt cihaz kimlikleri gerektirir ve hello bulut hizmeti tarafından oluşturulan kimlik doğrulaması anahtarlarla ilişkili.</span><span class="sxs-lookup"><span data-stu-id="4aea3-131">**Keep authentication keys safe**: during deployment, each device requires device IDs and associated authentication keys generated by hello cloud service.</span></span> <span data-ttu-id="4aea3-132">Bu anahtarları bile hello dağıtımdan sonra fiziksel olarak güvenli tutun.</span><span class="sxs-lookup"><span data-stu-id="4aea3-132">Keep these keys physically safe even after hello deployment.</span></span> <span data-ttu-id="4aea3-133">Güvenliği aşılmış bir tuşa mevcut bir cihazın kötü amaçlı aygıt toomasquerade tarafından kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="4aea3-133">Any compromised key can be used by a malicious device toomasquerade as an existing device.</span></span>

## <a name="iot-solution-operator"></a><span data-ttu-id="4aea3-134">IOT çözüm işleci</span><span class="sxs-lookup"><span data-stu-id="4aea3-134">IoT solution operator</span></span>
<span data-ttu-id="4aea3-135">Bir IOT çözüm işleç varsa hello aşağıdaki en iyi uygulamaları izleyin:</span><span class="sxs-lookup"><span data-stu-id="4aea3-135">Follow hello best practices below if you are an IoT solution operator:</span></span>

* <span data-ttu-id="4aea3-136">**Toodate sistemi tutmak**: cihaz işletim sistemleri ve tüm aygıt sürücülerini güncelleştirilmiş toohello en son sürümleri olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="4aea3-136">**Keep systems up toodate**: ensure device operating systems and all device drivers are updated toohello latest versions.</span></span> 
* <span data-ttu-id="4aea3-137">**Kötü amaçlı etkinliği karşı koruma**: hello işletim sistemi izin veriliyorsa, her cihaz işletim sisteminde hello son virüsten koruma ve kötü amaçlı yazılımdan özellikleri yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="4aea3-137">**Protect against malicious activity**: if hello operating system permits, place hello latest anti-virus and anti-malware capabilities on each device operating system.</span></span> 
* <span data-ttu-id="4aea3-138">**Sık denetim**: güvenlik sorunları olduğunda anahtar toosecurity olaylara yanıt ilgili IOT altyapı denetleme.</span><span class="sxs-lookup"><span data-stu-id="4aea3-138">**Audit frequently**: auditing IoT infrastructure for security related issues is key when responding toosecurity incidents.</span></span>
* <span data-ttu-id="4aea3-139">**Fiziksel olarak hello IOT altyapısını koruma**: hello güvenlik saldırılarına karşı IOT altyapı başlatılan fiziksel erişimi toodevices kullanarak en kötü.</span><span class="sxs-lookup"><span data-stu-id="4aea3-139">**Physically protect hello IoT infrastructure**: hello worst security attacks against IoT infrastructure are launched using physical access toodevices.</span></span>
* <span data-ttu-id="4aea3-140">**Bulut kimlik bilgileri korumaya**: Bulut kimlik doğrulaması kimlik bilgilerini yapılandırmak ve bir IOT dağıtım işletim için kullanılan büyük olasılıkla hello en kolay yolu toogain erişimi olan ve bir IOT sistemden.</span><span class="sxs-lookup"><span data-stu-id="4aea3-140">**Protect cloud credentials**: cloud authentication credentials used for configuring and operating an IoT deployment are possibly hello easiest way toogain access and compromise an IoT system.</span></span> 

