---
title: aaaSecure, nesnelerin interneti (IOT) azure'da | Microsoft Docs
description: " Azure Internet interneti (IOT) Hizmetleri çok çeşitli özellikler sunar. Bu makalede, anlamanıza yardımcı olur nasıl toosecure Azure IOT çözümlerinizde. "
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TomSh
ms.assetid: 1473c8dd-8669-48fb-86db-b3c50e2eaf59
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/23/2017
ms.author: terrylan
ms.openlocfilehash: b6cb2ea1c1facada854fb52c55066f34a8289e47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="internet-of-things-security-overview"></a><span data-ttu-id="483fe-104">Nesnelerin interneti güvenliğine genel bakış</span><span class="sxs-lookup"><span data-stu-id="483fe-104">Internet of Things security overview</span></span>
<span data-ttu-id="483fe-105">Azure Internet interneti (IOT) Hizmetleri çok çeşitli özellikler sunar.</span><span class="sxs-lookup"><span data-stu-id="483fe-105">Azure internet of things (IoT) services offer a broad range of capabilities.</span></span> <span data-ttu-id="483fe-106">Bu kurumsal sınıf hizmetler şunları yapmanızı sağlar:</span><span class="sxs-lookup"><span data-stu-id="483fe-106">These enterprise grade services enable you to:</span></span>

* <span data-ttu-id="483fe-107">Cihazlardan veri toplama</span><span class="sxs-lookup"><span data-stu-id="483fe-107">Collect data from devices</span></span>
* <span data-ttu-id="483fe-108">Hareket halinde veri akışı çözümleme</span><span class="sxs-lookup"><span data-stu-id="483fe-108">Analyze data streams in-motion</span></span>
* <span data-ttu-id="483fe-109">Büyük veri gruplarını depolama ve sorgulama</span><span class="sxs-lookup"><span data-stu-id="483fe-109">Store and query large data sets</span></span>
* <span data-ttu-id="483fe-110">Gerçek zamanlı ve geçmiş verileri görselleştirme</span><span class="sxs-lookup"><span data-stu-id="483fe-110">Visualize both real-time and historical data</span></span>
* <span data-ttu-id="483fe-111">Arka ofis sistemleriyle tümleştirme</span><span class="sxs-lookup"><span data-stu-id="483fe-111">Integrate with back-office systems</span></span>

<span data-ttu-id="483fe-112">Bu özellikler, Azure IOT paketi paketleri birlikte toodeliver önceden yapılandırılmış çözümler olarak özel uzantıları ile birden çok Azure Hizmetleri.</span><span class="sxs-lookup"><span data-stu-id="483fe-112">toodeliver these capabilities, Azure IoT Suite packages together multiple Azure services with custom extensions as preconfigured solutions.</span></span> <span data-ttu-id="483fe-113">Bu önceden yapılandırılmış çözümler, IOT çözümlerinizi toodeliver ele tooreduce hello zaman yardımcı genel IOT çözümü düzenlerinin temel uygulamalarıdır.</span><span class="sxs-lookup"><span data-stu-id="483fe-113">These preconfigured solutions are base implementations of common IoT solution patterns that help tooreduce hello time you take toodeliver your IoT solutions.</span></span> <span data-ttu-id="483fe-114">Merhaba IOT yazılım geliştirme setlerini kullanan, özelleştirebilir ve bu çözümleri toomeet kendi gereksinimlerinizi genişletir.</span><span class="sxs-lookup"><span data-stu-id="483fe-114">Using hello IoT software development kits, you can customize and extend these solutions toomeet your own requirements.</span></span> <span data-ttu-id="483fe-115">Ayrıca bu çözümleri, yeni IoT çözümleri geliştirirken örnekler ya da şablonlar olarak da kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="483fe-115">You can also use these solutions as examples or templates when you are developing new IoT solutions.</span></span>

<span data-ttu-id="483fe-116">Hello Azure IOT paketi, IOT gereksinimleriniz için güçlü bir çözümdür.</span><span class="sxs-lookup"><span data-stu-id="483fe-116">hello Azure IoT suite is a powerful solution for your IoT needs.</span></span> <span data-ttu-id="483fe-117">Ancak, IOT çözümlerinizi göz önünde bulundurularak hello başından tasarlanmıştır upmost önem derecesi vardır.</span><span class="sxs-lookup"><span data-stu-id="483fe-117">However, it’s of upmost importance that your IoT solutions are designed with security in mind from hello start.</span></span> <span data-ttu-id="483fe-118">Merhaba çalıştırmaları IOT cihaz sayısı nedeniyle, herhangi bir güvenlik olayı hızlı bir şekilde önemli sonuçları yaygın bir olayla haline gelebilir.</span><span class="sxs-lookup"><span data-stu-id="483fe-118">Because of hello sheer number of IoT devices, any security incident can quickly become a widespread event with significant consequences.</span></span>

<span data-ttu-id="483fe-119">anladığınızdan toohelp nasıl toosecure, IOT çözümlerinizi bilgisinden hello sahibiz.</span><span class="sxs-lookup"><span data-stu-id="483fe-119">toohelp you understand how toosecure your IoT solutions, we have hello following information.</span></span>

## <a name="security-architecture"></a><span data-ttu-id="483fe-120">Güvenlik mimarisi</span><span class="sxs-lookup"><span data-stu-id="483fe-120">Security architecture</span></span>
<span data-ttu-id="483fe-121">Sistem tasarlanırken önemli toounderstand hello olası tehditler toothat sistemidir ve hello sistem tasarlanmış ve tasarlanmış gibi uygun savunma buna göre ekleyin.</span><span class="sxs-lookup"><span data-stu-id="483fe-121">When designing a system, it is important toounderstand hello potential threats toothat system, and add appropriate defenses accordingly, as hello system is designed and architected.</span></span> <span data-ttu-id="483fe-122">Toodesign hello hello başlangıç üründen göz önünde bulundurularak ile nasıl bir saldırganın mümkün toocompromise bir sistem olabilir anlama uygun Azaltıcı Etkenler hello başından yerinde olduğundan emin olun yardımcı olması önemlidir.</span><span class="sxs-lookup"><span data-stu-id="483fe-122">It is important toodesign hello product from hello start with security in mind because understanding how an attacker might be able toocompromise a system helps make sure appropriate mitigations are in place from hello beginning.</span></span>

<span data-ttu-id="483fe-123">Okuyarak IOT güvenlik mimarisi hakkında bilgi edinebilirsiniz [şeyler güvenlik mimarisi Internet](../iot-suite/iot-security-architecture.md).</span><span class="sxs-lookup"><span data-stu-id="483fe-123">You can learn about IoT security architecture by reading [Internet of Things Security Architecture](../iot-suite/iot-security-architecture.md).</span></span>

<span data-ttu-id="483fe-124">Bu makalede aşağıdaki konularda hello ele alınmıştır:</span><span class="sxs-lookup"><span data-stu-id="483fe-124">This article discusses hello following topics:</span></span>

* [<span data-ttu-id="483fe-125">Bir tehdit modeli ile güvenlik başlar</span><span class="sxs-lookup"><span data-stu-id="483fe-125">Security Starts with a Threat Model</span></span>](../iot-suite/iot-security-architecture.md#security-starts-with-a-threat-model)
* [<span data-ttu-id="483fe-126">IOT güvenlik</span><span class="sxs-lookup"><span data-stu-id="483fe-126">Security in IoT</span></span>](../iot-suite/iot-security-architecture.md#security-in-iot)
* [<span data-ttu-id="483fe-127">Tehdit modelleme hello Azure IOT başvuru mimarisi</span><span class="sxs-lookup"><span data-stu-id="483fe-127">Threat Modeling hello Azure IoT Reference Architecture</span></span>](../iot-suite/iot-security-architecture.md#threat-modeling-the-azure-iot-reference-architecture)

## <a name="security-from-hello-ground-up"></a><span data-ttu-id="483fe-128">Plan hello güvenlikten</span><span class="sxs-lookup"><span data-stu-id="483fe-128">Security from hello ground up</span></span>
<span data-ttu-id="483fe-129">Merhaba IOT benzersiz güvenlik, gizlilik ve uyumluluk sorunları toobusinesses dünya çapında doğurur.</span><span class="sxs-lookup"><span data-stu-id="483fe-129">hello IoT poses unique security, privacy, and compliance challenges toobusinesses worldwide.</span></span> <span data-ttu-id="483fe-130">Bu sorunları yazılım ve nasıl uygulandığı burada Uzayda Döndür geleneksel siber teknolojisi hello siber ve hello fiziksel dünyaları yakınsama ne olur IOT ilgilidir.</span><span class="sxs-lookup"><span data-stu-id="483fe-130">Unlike traditional cyber technology where these issues revolve around software and how it is implemented, IoT concerns what happens when hello cyber and hello physical worlds converge.</span></span> <span data-ttu-id="483fe-131">IOT çözümleri koruma cihazları, bu cihazlar ve hello Bulut ve işleme ve depolama sırasında hello bulutta güvenli veri koruması arasında güvenli bağlantı güvenli sağlanmasını sağlama gerektirir.</span><span class="sxs-lookup"><span data-stu-id="483fe-131">Protecting IoT solutions requires ensuring secure provisioning of devices, secure connectivity between these devices and hello cloud, and secure data protection in hello cloud during processing and storage.</span></span> <span data-ttu-id="483fe-132">Bu tür işlevselliği karşı çalışan, ancak, kaynak kısıtlı cihazları, dağıtımları coğrafi dağıtılması ve bir çözüm içinde çok sayıda aygıt değildir.</span><span class="sxs-lookup"><span data-stu-id="483fe-132">Working against such functionality, however, are resource-constrained devices, geographic distribution of deployments, and many devices within a solution.</span></span>

<span data-ttu-id="483fe-133">Bilgi edinebilirsiniz nasıl toohandle güvenlik okuyarak bu alanlarda [plan hello nesnelerin interneti güvenlikten](../iot-suite/securing-iot-ground-up.md).</span><span class="sxs-lookup"><span data-stu-id="483fe-133">You can learn how toohandle security in these areas by reading [Internet of Things security from hello ground up](../iot-suite/securing-iot-ground-up.md).</span></span>

<span data-ttu-id="483fe-134">Merhaba, aşağıdaki konularda hello anlatılmaktadır:</span><span class="sxs-lookup"><span data-stu-id="483fe-134">hello article discusses hello following topics:</span></span>

* [<span data-ttu-id="483fe-135">Plan hello altyapısından güvenli</span><span class="sxs-lookup"><span data-stu-id="483fe-135">Secure infrastructure from hello ground up</span></span>](../iot-suite/securing-iot-ground-up.md#secure-infrastructure-from-the-ground-up)
* [<span data-ttu-id="483fe-136">Microsoft Azure – işletmeniz için güvenli IOT altyapısı</span><span class="sxs-lookup"><span data-stu-id="483fe-136">Microsoft Azure – secure IoT infrastructure for your business</span></span>](../iot-suite/securing-iot-ground-up.md#microsoft-azure---secure-iot-infrastructure-for-your-business)

## <a name="best-practices"></a><span data-ttu-id="483fe-137">En İyi Uygulamalar</span><span class="sxs-lookup"><span data-stu-id="483fe-137">Best Practices</span></span>
<span data-ttu-id="483fe-138">Bir IOT altyapısını koruma sıkı güvenlik derinlemesine stratejisi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="483fe-138">Securing an IoT infrastructure requires a rigorous security-in-depth strategy.</span></span> <span data-ttu-id="483fe-139">Güvenli hale getirme gelen hello üzerinden aktarımda toosecurely sağlama aygıtlar, her katman genel internet daha yüksek güvenlik güvencesi oluşturuncaya kadar veri bütünlüğü koruma verileri hello bulutta hello genel altyapı.</span><span class="sxs-lookup"><span data-stu-id="483fe-139">From securing data in hello cloud, protecting data integrity while in transit over hello public internet, toosecurely provisioning devices, each layer builds greater security assurance in hello overall infrastructure.</span></span>

<span data-ttu-id="483fe-140">Okuyarak nesnelerin interneti güvenlikle ilgili en iyi yöntemler öğrenebilirsiniz [en iyi güvenlik uygulamalarını, nesnelerin interneti](../iot-suite/iot-security-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="483fe-140">You can learn about Internet of Things security best practices by reading [Internet of Things security best practices](../iot-suite/iot-security-best-practices.md).</span></span>

<span data-ttu-id="483fe-141">Merhaba, aşağıdaki konularda hello anlatılmaktadır:</span><span class="sxs-lookup"><span data-stu-id="483fe-141">hello article discusses hello following topics:</span></span>

* [<span data-ttu-id="483fe-142">IOT donanım üreticisinin/Tümleştirici</span><span class="sxs-lookup"><span data-stu-id="483fe-142">IoT hardware manufacturer/integrator</span></span>](../iot-suite/iot-security-best-practices.md#iot-hardware-manufacturerintegrator)
* [<span data-ttu-id="483fe-143">IOT Çözüm geliştiricisi</span><span class="sxs-lookup"><span data-stu-id="483fe-143">IoT solution developer</span></span>](../iot-suite/iot-security-best-practices.md#iot-solution-developer)
* [<span data-ttu-id="483fe-144">IOT çözüm dağıtıcı</span><span class="sxs-lookup"><span data-stu-id="483fe-144">IoT solution deployer</span></span>](../iot-suite/iot-security-best-practices.md#iot-solution-deployer)
* [<span data-ttu-id="483fe-145">IOT çözüm işleci</span><span class="sxs-lookup"><span data-stu-id="483fe-145">IoT solution operator</span></span>](../iot-suite/iot-security-best-practices.md#iot-solution-operator)
