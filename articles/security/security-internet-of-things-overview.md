---
title: "Nesnelerin interneti (IOT) Azure Internet bağlantınızın güvenli | Microsoft Docs"
description: " Azure Internet interneti (IOT) Hizmetleri çok çeşitli özellikler sunar. Bu makalede, Azure IOT çözümlerinizde güvenliğini sağlama anlamanıza yardımcı olur. "
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
ms.openlocfilehash: 3793f5453b74b6c06d9e58b426d89099298e1288
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="internet-of-things-security-overview"></a><span data-ttu-id="900a7-104">Nesnelerin interneti güvenliğine genel bakış</span><span class="sxs-lookup"><span data-stu-id="900a7-104">Internet of Things security overview</span></span>
<span data-ttu-id="900a7-105">Azure Internet interneti (IOT) Hizmetleri çok çeşitli özellikler sunar.</span><span class="sxs-lookup"><span data-stu-id="900a7-105">Azure internet of things (IoT) services offer a broad range of capabilities.</span></span> <span data-ttu-id="900a7-106">Bu kurumsal sınıf hizmetler şunları yapmanızı sağlar:</span><span class="sxs-lookup"><span data-stu-id="900a7-106">These enterprise grade services enable you to:</span></span>

* <span data-ttu-id="900a7-107">Cihazlardan veri toplama</span><span class="sxs-lookup"><span data-stu-id="900a7-107">Collect data from devices</span></span>
* <span data-ttu-id="900a7-108">Hareket halinde veri akışı çözümleme</span><span class="sxs-lookup"><span data-stu-id="900a7-108">Analyze data streams in-motion</span></span>
* <span data-ttu-id="900a7-109">Büyük veri gruplarını depolama ve sorgulama</span><span class="sxs-lookup"><span data-stu-id="900a7-109">Store and query large data sets</span></span>
* <span data-ttu-id="900a7-110">Gerçek zamanlı ve geçmiş verileri görselleştirme</span><span class="sxs-lookup"><span data-stu-id="900a7-110">Visualize both real-time and historical data</span></span>
* <span data-ttu-id="900a7-111">Arka ofis sistemleriyle tümleştirme</span><span class="sxs-lookup"><span data-stu-id="900a7-111">Integrate with back-office systems</span></span>

<span data-ttu-id="900a7-112">Bu özellikler, Azure IOT paketi paketleri önceden yapılandırılmış çözümler olarak birden çok Azure hizmetini özel uzantılarla birlikte sunmak için.</span><span class="sxs-lookup"><span data-stu-id="900a7-112">To deliver these capabilities, Azure IoT Suite packages together multiple Azure services with custom extensions as preconfigured solutions.</span></span> <span data-ttu-id="900a7-113">Bu önceden yapılandırılmış çözümler, IoT çözümlerinizi sunmak için geçirmeniz gereken süreyi azaltmak üzere genel IoT çözümü düzenlerinin temel uygulamalarıdır.</span><span class="sxs-lookup"><span data-stu-id="900a7-113">These preconfigured solutions are base implementations of common IoT solution patterns that help to reduce the time you take to deliver your IoT solutions.</span></span> <span data-ttu-id="900a7-114">IOT yazılım geliştirme setleri kullanarak, özelleştirme ve kendi gereksinimlerinizi karşılamak için bu çözümleri genişletir.</span><span class="sxs-lookup"><span data-stu-id="900a7-114">Using the IoT software development kits, you can customize and extend these solutions to meet your own requirements.</span></span> <span data-ttu-id="900a7-115">Ayrıca bu çözümleri, yeni IoT çözümleri geliştirirken örnekler ya da şablonlar olarak da kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="900a7-115">You can also use these solutions as examples or templates when you are developing new IoT solutions.</span></span>

<span data-ttu-id="900a7-116">Azure IOT paketi, IOT gereksinimleriniz için güçlü bir çözümdür.</span><span class="sxs-lookup"><span data-stu-id="900a7-116">The Azure IoT suite is a powerful solution for your IoT needs.</span></span> <span data-ttu-id="900a7-117">Ancak, IOT çözümlerinizi göz önünde bulundurularak başından tasarlanmıştır upmost önem derecesi vardır.</span><span class="sxs-lookup"><span data-stu-id="900a7-117">However, it’s of upmost importance that your IoT solutions are designed with security in mind from the start.</span></span> <span data-ttu-id="900a7-118">IOT cihazları çalıştırmaları sayısı nedeniyle, herhangi bir güvenlik olayı hızlı bir şekilde önemli sonuçları yaygın bir olayla haline gelebilir.</span><span class="sxs-lookup"><span data-stu-id="900a7-118">Because of the sheer number of IoT devices, any security incident can quickly become a widespread event with significant consequences.</span></span>

<span data-ttu-id="900a7-119">IOT çözümlerinizi güvenliğini sağlama anlamanıza yardımcı olması için aşağıdaki bilgileri sahibiz.</span><span class="sxs-lookup"><span data-stu-id="900a7-119">To help you understand how to secure your IoT solutions, we have the following information.</span></span>

## <a name="security-architecture"></a><span data-ttu-id="900a7-120">Güvenlik mimarisi</span><span class="sxs-lookup"><span data-stu-id="900a7-120">Security architecture</span></span>
<span data-ttu-id="900a7-121">Sistem tasarlanırken, bu sistemde olası tehditler anlamak ve sistem tasarlanmış ve tasarlanmış gibi uygun savunma buna göre eklemek önemlidir.</span><span class="sxs-lookup"><span data-stu-id="900a7-121">When designing a system, it is important to understand the potential threats to that system, and add appropriate defenses accordingly, as the system is designed and architected.</span></span> <span data-ttu-id="900a7-122">Nasıl bir saldırganın bir sistemden olabilir emin uygun Azaltıcı Etkenler hale getirir anlama olduğundan başlangıçtan itibaren yerinde göz önünde bulundurularak ile başlangıç ürün tasarlamanız önemlidir.</span><span class="sxs-lookup"><span data-stu-id="900a7-122">It is important to design the product from the start with security in mind because understanding how an attacker might be able to compromise a system helps make sure appropriate mitigations are in place from the beginning.</span></span>

<span data-ttu-id="900a7-123">Okuyarak IOT güvenlik mimarisi hakkında bilgi edinebilirsiniz [şeyler güvenlik mimarisi Internet](../iot-suite/iot-security-architecture.md).</span><span class="sxs-lookup"><span data-stu-id="900a7-123">You can learn about IoT security architecture by reading [Internet of Things Security Architecture](../iot-suite/iot-security-architecture.md).</span></span>

<span data-ttu-id="900a7-124">Bu makalede aşağıdaki konular ele alınmıştır:</span><span class="sxs-lookup"><span data-stu-id="900a7-124">This article discusses the following topics:</span></span>

* [<span data-ttu-id="900a7-125">Bir tehdit modeli ile güvenlik başlar</span><span class="sxs-lookup"><span data-stu-id="900a7-125">Security Starts with a Threat Model</span></span>](../iot-suite/iot-security-architecture.md#security-starts-with-a-threat-model)
* [<span data-ttu-id="900a7-126">IOT güvenlik</span><span class="sxs-lookup"><span data-stu-id="900a7-126">Security in IoT</span></span>](../iot-suite/iot-security-architecture.md#security-in-iot)
* [<span data-ttu-id="900a7-127">Tehdit modelleme Azure IOT başvuru mimarisi</span><span class="sxs-lookup"><span data-stu-id="900a7-127">Threat Modeling the Azure IoT Reference Architecture</span></span>](../iot-suite/iot-security-architecture.md#threat-modeling-the-azure-iot-reference-architecture)

## <a name="security-from-the-ground-up"></a><span data-ttu-id="900a7-128">Baştan sona güvenlik</span><span class="sxs-lookup"><span data-stu-id="900a7-128">Security from the ground up</span></span>
<span data-ttu-id="900a7-129">IOT işletmelere dünya çapındaki benzersiz güvenlik, gizlilik ve uyumluluk sorunları doğurur.</span><span class="sxs-lookup"><span data-stu-id="900a7-129">The IoT poses unique security, privacy, and compliance challenges to businesses worldwide.</span></span> <span data-ttu-id="900a7-130">Bu sorunları yazılım ve nasıl uygulandığı burada Uzayda Döndür geleneksel siber teknolojisi farklı olarak, sanal ve fiziksel dünyaları yakınsama ne olur IOT ilgilidir.</span><span class="sxs-lookup"><span data-stu-id="900a7-130">Unlike traditional cyber technology where these issues revolve around software and how it is implemented, IoT concerns what happens when the cyber and the physical worlds converge.</span></span> <span data-ttu-id="900a7-131">IOT çözümleri koruma cihazları, bu cihazlar ve Bulut ve işleme ve depolama sırasında bulutta güvenli veri koruması arasında güvenli bağlantı güvenli sağlanmasını sağlama gerektirir.</span><span class="sxs-lookup"><span data-stu-id="900a7-131">Protecting IoT solutions requires ensuring secure provisioning of devices, secure connectivity between these devices and the cloud, and secure data protection in the cloud during processing and storage.</span></span> <span data-ttu-id="900a7-132">Bu tür işlevselliği karşı çalışan, ancak, kaynak kısıtlı cihazları, dağıtımları coğrafi dağıtılması ve bir çözüm içinde çok sayıda aygıt değildir.</span><span class="sxs-lookup"><span data-stu-id="900a7-132">Working against such functionality, however, are resource-constrained devices, geographic distribution of deployments, and many devices within a solution.</span></span>

<span data-ttu-id="900a7-133">Bu alanlarda güvenlik okuyarak nasıl ele alınacağını öğrenin [nesnelerin interneti güvenlik sıfırdan](../iot-suite/securing-iot-ground-up.md).</span><span class="sxs-lookup"><span data-stu-id="900a7-133">You can learn how to handle security in these areas by reading [Internet of Things security from the ground up](../iot-suite/securing-iot-ground-up.md).</span></span>

<span data-ttu-id="900a7-134">Makaleyi aşağıdaki konular ele alınmıştır:</span><span class="sxs-lookup"><span data-stu-id="900a7-134">The article discusses the following topics:</span></span>

* [<span data-ttu-id="900a7-135">Sıfırdan güvenli altyapısı</span><span class="sxs-lookup"><span data-stu-id="900a7-135">Secure infrastructure from the ground up</span></span>](../iot-suite/securing-iot-ground-up.md#secure-infrastructure-from-the-ground-up)
* [<span data-ttu-id="900a7-136">Microsoft Azure – işletmeniz için güvenli IOT altyapısı</span><span class="sxs-lookup"><span data-stu-id="900a7-136">Microsoft Azure – secure IoT infrastructure for your business</span></span>](../iot-suite/securing-iot-ground-up.md#microsoft-azure---secure-iot-infrastructure-for-your-business)

## <a name="best-practices"></a><span data-ttu-id="900a7-137">En İyi Uygulamalar</span><span class="sxs-lookup"><span data-stu-id="900a7-137">Best Practices</span></span>
<span data-ttu-id="900a7-138">Bir IOT altyapısını koruma sıkı güvenlik derinlemesine stratejisi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="900a7-138">Securing an IoT infrastructure requires a rigorous security-in-depth strategy.</span></span> <span data-ttu-id="900a7-139">Cihazları, güvenli bir şekilde hazırlanması genel internet üzerinden aktarım sırasında veri bütünlüğü koruma verileri bulutta güvenli hale getirme her katman genel altyapısında daha yüksek güvenlik güvencesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="900a7-139">From securing data in the cloud, protecting data integrity while in transit over the public internet, to securely provisioning devices, each layer builds greater security assurance in the overall infrastructure.</span></span>

<span data-ttu-id="900a7-140">Okuyarak nesnelerin interneti güvenlikle ilgili en iyi yöntemler öğrenebilirsiniz [en iyi güvenlik uygulamalarını, nesnelerin interneti](../iot-suite/iot-security-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="900a7-140">You can learn about Internet of Things security best practices by reading [Internet of Things security best practices](../iot-suite/iot-security-best-practices.md).</span></span>

<span data-ttu-id="900a7-141">Makaleyi aşağıdaki konular ele alınmıştır:</span><span class="sxs-lookup"><span data-stu-id="900a7-141">The article discusses the following topics:</span></span>

* [<span data-ttu-id="900a7-142">IOT donanım üreticisinin/Tümleştirici</span><span class="sxs-lookup"><span data-stu-id="900a7-142">IoT hardware manufacturer/integrator</span></span>](../iot-suite/iot-security-best-practices.md#iot-hardware-manufacturerintegrator)
* [<span data-ttu-id="900a7-143">IOT Çözüm geliştiricisi</span><span class="sxs-lookup"><span data-stu-id="900a7-143">IoT solution developer</span></span>](../iot-suite/iot-security-best-practices.md#iot-solution-developer)
* [<span data-ttu-id="900a7-144">IOT çözüm dağıtıcı</span><span class="sxs-lookup"><span data-stu-id="900a7-144">IoT solution deployer</span></span>](../iot-suite/iot-security-best-practices.md#iot-solution-deployer)
* [<span data-ttu-id="900a7-145">IOT çözüm işleci</span><span class="sxs-lookup"><span data-stu-id="900a7-145">IoT solution operator</span></span>](../iot-suite/iot-security-best-practices.md#iot-solution-operator)
