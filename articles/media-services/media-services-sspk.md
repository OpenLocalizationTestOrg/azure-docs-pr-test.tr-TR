---
title: "aaaLicensing Microsoft® kesintisiz akış istemci bağlantı noktası oluşturma Seti"
description: "Nasıl toolicensing hello hakkında Microsoft® kesintisiz akış istemci bağlantı noktası oluşturma Seti öğrenin."
services: media-services
documentationcenter: 
author: xpouyat
manager: cfowler
editor: 
ms.assetid: e3b488e7-8428-4c10-a072-eb3af46c82ad
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: xpouyat
ms.openlocfilehash: 56c3dccda73dd02207bb4dbe8109ba6fda917a6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="licensing-microsoft-smooth-streaming-client-porting-kit"></a><span data-ttu-id="08200-103">Kit taşıma lisanslama Microsoft® kesintisiz akış istemcisi</span><span class="sxs-lookup"><span data-stu-id="08200-103">Licensing Microsoft® Smooth Streaming Client Porting Kit</span></span>
## <a name="overview"></a><span data-ttu-id="08200-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="08200-104">Overview</span></span>
<span data-ttu-id="08200-105">Microsoft kesintisiz akış istemci bağlantı noktası oluşturma Seti (**SSPK** kısaca) en iyi duruma getirilmiş toohelp katıştırılmış cihaz üreticisinin, kablo ve mobil işleçleri, içerik hizmet sağlayıcıları, ahize kesintisiz akış bir istemci uygulaması Üreticiler, bağımsız yazılım satıcılarının (ISV'ler) ve çözüm sağlayıcıları toocreate ürünleri ve kesintisiz akış biçiminde Uyarlamalı akış içeriği akışla Hizmetleri.</span><span class="sxs-lookup"><span data-stu-id="08200-105">Microsoft Smooth Streaming Client Porting Kit (**SSPK** for short) is a Smooth Streaming client implementation that is optimized toohelp embedded device manufacturers, cable and mobile operators, content service providers, handset manufacturers, independent software vendors (ISVs), and solution providers toocreate products and services for streaming adaptive streaming content in Smooth Streaming format.</span></span> <span data-ttu-id="08200-106">SSPK bir cihaz ve platform bağımsız hello edinmediyseniz tooany cihaz ve platform tarafından bağlantı noktalı kesintisiz akış istemci uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="08200-106">SSPK is a device and platform independent implementation of Smooth Streaming client that can be ported by hello licensee tooany device and platform.</span></span> 

<span data-ttu-id="08200-107">Aşağıda yüksek düzey bir mimari ve IIS kesintisiz akış bağlantı noktası oluşturma Seti kutusunu Microsoft tarafından sağlanan hello Smooth Streaming Client uygulamasıdır ve kesintisiz akış içeriği kayıttan yürütmeyi için tüm hello çekirdek mantığını içerir.</span><span class="sxs-lookup"><span data-stu-id="08200-107">Included below is a high level architecture and IIS Smooth Streaming Porting Kit box is hello Smooth Streaming Client implementation provided by Microsoft and includes all hello core logic for playback of Smooth Streaming content.</span></span> <span data-ttu-id="08200-108">Bundan sonra belirli bir aygıt veya platformu için iş ortakları tarafından uygun arabirimleri uygulayarak verilen.</span><span class="sxs-lookup"><span data-stu-id="08200-108">This is then ported by partners for a specific device or platform by implementing appropriate interfaces.</span></span> 

![SSPK](./media/media-services-sspk/sspk-arch.png)

## <a name="description"></a><span data-ttu-id="08200-110">Açıklama</span><span class="sxs-lookup"><span data-stu-id="08200-110">Description</span></span>
<span data-ttu-id="08200-111">SSPK mükemmel iş değerini sunan koşullarınızda lisanslıdır.</span><span class="sxs-lookup"><span data-stu-id="08200-111">SSPK is licensed on terms that offer excellent business value.</span></span> <span data-ttu-id="08200-112">SSPK lisans ile Merhaba endüstri sağlar:</span><span class="sxs-lookup"><span data-stu-id="08200-112">SSPK license provides hello industry with:</span></span>

* <span data-ttu-id="08200-113">C++'ta kesintisiz akış bağlantı noktası oluşturma Seti kaynak</span><span class="sxs-lookup"><span data-stu-id="08200-113">Smooth Streaming Porting Kit source in C++</span></span> 
  * <span data-ttu-id="08200-114">Smooth Streaming Client işlevselliğini hayata Geçiren</span><span class="sxs-lookup"><span data-stu-id="08200-114">implements Smooth Streaming Client functionality</span></span>
  * <span data-ttu-id="08200-115">ayrıştırma, arabelleğe alma mantığı, vb. buluşsal yöntemler, biçimi ekler.</span><span class="sxs-lookup"><span data-stu-id="08200-115">adds format parsing, heuristics, buffering logic, etc.</span></span>
* <span data-ttu-id="08200-116">Oynatıcı uygulaması API'leri</span><span class="sxs-lookup"><span data-stu-id="08200-116">Player application APIs</span></span> 
  * <span data-ttu-id="08200-117">medya oynatıcı uygulaması ile etkileşim için programlama arabirimleri</span><span class="sxs-lookup"><span data-stu-id="08200-117">programming interfaces for interaction with a media player application</span></span>
* <span data-ttu-id="08200-118">Platform Soyutlama Katmanı (PAL) arabirimi</span><span class="sxs-lookup"><span data-stu-id="08200-118">Platform Abstraction Layer (PAL) Interface</span></span> 
  * <span data-ttu-id="08200-119">Merhaba işletim sistemi (iş parçacıkları, yuva) ile etkileşim için programlama arabirimleri</span><span class="sxs-lookup"><span data-stu-id="08200-119">programming interfaces for interaction with hello operating system (threads, sockets)</span></span>
* <span data-ttu-id="08200-120">Donanım özet düzeyi (HAL) arabirimi</span><span class="sxs-lookup"><span data-stu-id="08200-120">Hardware Abstraction Layer (HAL) Interface</span></span> 
  * <span data-ttu-id="08200-121">programlama arabirimleri donanım A ile etkileşim için / (kod çözme, işleme) V kod çözücüleri</span><span class="sxs-lookup"><span data-stu-id="08200-121">programming interfaces for interaction with hardware A/V decoders (decoding, rendering)</span></span>
* <span data-ttu-id="08200-122">Dijital Hak Yönetimi (DRM) arabirimi</span><span class="sxs-lookup"><span data-stu-id="08200-122">Digital Rights Management (DRM) Interface</span></span> 
  * <span data-ttu-id="08200-123">DRM hello DRM özet düzeyi (DAL) işlemek için programlama arabirimleri</span><span class="sxs-lookup"><span data-stu-id="08200-123">programming interfaces for handling DRM through hello DRM Abstraction Layer (DAL)</span></span>
  * <span data-ttu-id="08200-124">Microsoft PlayReady bağlantı noktası oluşturma Seti ayrı olarak gelir ancak bu arabirimi aracılığıyla tümleştirir.</span><span class="sxs-lookup"><span data-stu-id="08200-124">Microsoft PlayReady Porting Kit ships separately but integrates through this interface.</span></span> <span data-ttu-id="08200-125">Microsoft PlayReady Device lisanslama hakkında daha fazla ayrıntı için tıklatın [burada](http://www.microsoft.com/playready/licensing/device_technology.mspx#pddipdl).</span><span class="sxs-lookup"><span data-stu-id="08200-125">For more details on Microsoft PlayReady Device licensing, click [here](http://www.microsoft.com/playready/licensing/device_technology.mspx#pddipdl).</span></span>
* <span data-ttu-id="08200-126">Uygulama örnekleri</span><span class="sxs-lookup"><span data-stu-id="08200-126">Implementation samples</span></span> 
  * <span data-ttu-id="08200-127">Linux için örnek PAL uygulama</span><span class="sxs-lookup"><span data-stu-id="08200-127">sample PAL implementation for Linux</span></span>
  * <span data-ttu-id="08200-128">Örnek HAL uygulama GStreamer için</span><span class="sxs-lookup"><span data-stu-id="08200-128">sample HAL implementation for GStreamer</span></span>

## <a name="licensing-options"></a><span data-ttu-id="08200-129">Lisanslama Seçenekleri</span><span class="sxs-lookup"><span data-stu-id="08200-129">Licensing Options</span></span>
<span data-ttu-id="08200-130">Microsoft kesintisiz akış istemci bağlantı noktası oluşturma Seti altında iki ayrı lisans sözleşmelerini kullanılabilir toolicensees yapılır: bir kesintisiz akış istemci geçici ürünleri ve kesintisiz akış istemci son ürünler tooend kullanıcılara dağıtmak için başka bir geliştirmek için.</span><span class="sxs-lookup"><span data-stu-id="08200-130">Microsoft Smooth Streaming Client Porting Kit is made available toolicensees under two distinct license agreements: one for developing Smooth Streaming Client Interim Products and another for distributing Smooth Streaming Client Final Products tooend users.</span></span>

* <span data-ttu-id="08200-131">Yonga kümesi üreticileri, sistem tümleştiricileri veya bağımsız yazılım satıcıları (ISV) bir kaynak kod bağlantı noktası oluşturma gereksinim duyan toodevelop geçici ürünler, bir Microsoft kesintisiz akış istemci bağlantı noktası oluşturma Seti Seti **geçici Ürün lisans** yürütülmelidir.</span><span class="sxs-lookup"><span data-stu-id="08200-131">For chipset manufacturers, system integrators, or independent software vendors (ISVs) who require a source code porting kit toodevelop Interim Products, a Microsoft Smooth Streaming Client Porting Kit **Interim Product License** should be executed.</span></span>
* <span data-ttu-id="08200-132">Cihaz üreticileri veya kesintisiz akış istemci son ürünler tooend kullanıcılar için dağıtım hakları gerektiren ISV'ler hello için Microsoft kesintisiz akış istemci bağlantı noktası oluşturma Seti **son ürün lisans** yürütülmelidir.</span><span class="sxs-lookup"><span data-stu-id="08200-132">For device manufacturers or ISVs who require distribution rights for Smooth Streaming Client Final Products tooend users, hello Microsoft Smooth Streaming Client Porting Kit **Final Product License** should be executed.</span></span>

### <a name="microsoft-smooth-streaming-client-porting-kit-interim-product-license"></a><span data-ttu-id="08200-133">Microsoft Smooth Streaming Client Seti geçici Ürün lisans bağlantı noktası oluşturma</span><span class="sxs-lookup"><span data-stu-id="08200-133">Microsoft Smooth Streaming Client Porting Kit Interim Product License</span></span>
<span data-ttu-id="08200-134">Bu lisansı altında Microsoft bir kesintisiz akış istemci bağlantı noktası oluşturma Seti sunar ve gerekli fikri mülkiyet hakları toodevelop hello ve kesintisiz akış istemci geçici ürünleri tooother kesintisiz akış istemci bağlantı noktası oluşturma Seti aygıt lisans sahipleri dağıtmak, Kesintisiz akış istemci son ürünler dağıtın.</span><span class="sxs-lookup"><span data-stu-id="08200-134">Under this license, Microsoft offers a Smooth Streaming Client Porting Kit and hello necessary intellectual property rights toodevelop and distribute Smooth Streaming Client Interim Products tooother Smooth Streaming Client Porting Kit device licensees that distribute Smooth Streaming Client Final Products.</span></span>

#### <a name="fee-structure"></a><span data-ttu-id="08200-135">Ücret yapısı</span><span class="sxs-lookup"><span data-stu-id="08200-135">Fee structure</span></span>
<span data-ttu-id="08200-136">ABD 50.000 tek seferlik lisans ücret erişim toohello kesintisiz akış istemci bağlantı noktası oluşturma Seti sağlar.</span><span class="sxs-lookup"><span data-stu-id="08200-136">A U.S. $50,000 one-time license fee provides access toohello Smooth Streaming Client Porting Kit.</span></span> 

### <a name="microsoft-smooth-streaming-client-porting-kit-final-product-license"></a><span data-ttu-id="08200-137">Microsoft Smooth Streaming Client Seti son ürün lisans bağlantı noktası oluşturma</span><span class="sxs-lookup"><span data-stu-id="08200-137">Microsoft Smooth Streaming Client Porting Kit Final Product License</span></span>
<span data-ttu-id="08200-138">Bu lisansı altında diğer kesintisiz akış istemci bağlantı noktası oluşturma Seti lisans sahipleri ve şirket markalı-kesintisiz akış istemci son toodistribute tüm gerekli fikri mülkiyet hakları tooreceive kesintisiz akış istemci geçici ürünleri Microsoft yapılandırmayı sunar. Ürünleri tooend kullanıcılar.</span><span class="sxs-lookup"><span data-stu-id="08200-138">Under this license, Microsoft offers all necessary intellectual property rights tooreceive Smooth Streaming Client Interim Products from other Smooth Streaming Client Porting Kit licensees and toodistribute company-branded Smooth Streaming Client Final Products tooend users.</span></span>

#### <a name="fee-structure"></a><span data-ttu-id="08200-139">Ücret yapısı</span><span class="sxs-lookup"><span data-stu-id="08200-139">Fee structure</span></span>
<span data-ttu-id="08200-140">Merhaba kesintisiz akış istemci son ürün altında lisanslı model olarak altında sunulur:</span><span class="sxs-lookup"><span data-stu-id="08200-140">hello Smooth Streaming Client Final Product is offered under a royalty model as under:</span></span>

* <span data-ttu-id="08200-141">cihaz uygulaması başına 0,10 sevk</span><span class="sxs-lookup"><span data-stu-id="08200-141">$0.10 per device implementation shipped</span></span>
* <span data-ttu-id="08200-142">Merhaba lisanslı 50.000 her yıl tutulabilir</span><span class="sxs-lookup"><span data-stu-id="08200-142">hello royalty is capped at $50,000 each year</span></span>
* <span data-ttu-id="08200-143">İlk 10.000 cihaz uygulamaları her yıl için hiçbir lisanslı</span><span class="sxs-lookup"><span data-stu-id="08200-143">No royalty for first 10,000 device implementations each year</span></span> 

## <a name="licensing-procedure-and-sspk-access"></a><span data-ttu-id="08200-144">Lisans yordamı ve SSPK erişim</span><span class="sxs-lookup"><span data-stu-id="08200-144">Licensing Procedure and SSPK access</span></span>
<span data-ttu-id="08200-145">Lütfen e-posta [ sspkinfo@microsoft.com ](mailto:sspkinfo@microsoft.com) tüm lisans sorgular.</span><span class="sxs-lookup"><span data-stu-id="08200-145">Please email [sspkinfo@microsoft.com](mailto:sspkinfo@microsoft.com) for all licensing queries.</span></span>

<span data-ttu-id="08200-146">Merhaba [SSPK dağıtım portal](https://microsoft.sharepoint.com/teams/SSPKDOWNLOAD/) geçici lisans sahipleri için erişilebilir tooregistered değil.</span><span class="sxs-lookup"><span data-stu-id="08200-146">hello [SSPK Distribution portal](https://microsoft.sharepoint.com/teams/SSPKDOWNLOAD/) is accessible tooregistered Interim licensees.</span></span>

<span data-ttu-id="08200-147">Lisans sahipleri için geçici ve son SSPK gönderebilir teknik sorular çok[smoothpk@microsoft.com](mailto:smoothpk@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="08200-147">Interim and Final SSPK licensees can submit technical questions too[smoothpk@microsoft.com](mailto:smoothpk@microsoft.com).</span></span>

## <a name="microsoft-smooth-streaming-client-interim-product-agreement-licensees"></a><span data-ttu-id="08200-148">Microsoft istemci geçici ürün sözleşmesi lisans sahipleri akış kesintisiz</span><span class="sxs-lookup"><span data-stu-id="08200-148">Microsoft Smooth Streaming Client Interim Product Agreement Licensees</span></span>
* <span data-ttu-id="08200-149">Adroit işletme çözümleri, Inc</span><span class="sxs-lookup"><span data-stu-id="08200-149">Adroit Business Solutions, Inc</span></span>
* <span data-ttu-id="08200-150">Gelişmiş dijital yayın SA'sı</span><span class="sxs-lookup"><span data-stu-id="08200-150">Advanced Digital Broadcast SA</span></span>
* <span data-ttu-id="08200-151">AirTies Kablosuz Iletism Sanayive Dış Ticaret A.S.</span><span class="sxs-lookup"><span data-stu-id="08200-151">AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.</span></span>
* <span data-ttu-id="08200-152">Albis teknolojileri Ltd.</span><span class="sxs-lookup"><span data-stu-id="08200-152">Albis Technologies Ltd.</span></span>
* <span data-ttu-id="08200-153">Alticast Corporation</span><span class="sxs-lookup"><span data-stu-id="08200-153">Alticast Corporation</span></span>
* <span data-ttu-id="08200-154">Amazon dijital Hizmetleri, Inc.</span><span class="sxs-lookup"><span data-stu-id="08200-154">Amazon Digital Services, Inc.</span></span>
* <span data-ttu-id="08200-155">Arion Technology, Inc.</span><span class="sxs-lookup"><span data-stu-id="08200-155">Arion Technology, Inc.</span></span>
* <span data-ttu-id="08200-156">AVC multimedya yazılım Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="08200-156">AVC Multimedia Software Co., Ltd.</span></span>
* <span data-ttu-id="08200-157">Cavium, Inc.</span><span class="sxs-lookup"><span data-stu-id="08200-157">Cavium, Inc.</span></span>
* <span data-ttu-id="08200-158">EchoStar Corporation'ın satın alma</span><span class="sxs-lookup"><span data-stu-id="08200-158">EchoStar Purchasing Corporation</span></span>
* <span data-ttu-id="08200-159">Enseo, Inc.</span><span class="sxs-lookup"><span data-stu-id="08200-159">Enseo, Inc.</span></span>
* <span data-ttu-id="08200-160">Fluendo Güney Amerika</span><span class="sxs-lookup"><span data-stu-id="08200-160">Fluendo S.A.</span></span>
* <span data-ttu-id="08200-161">HANDAN BroadInfoCom Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="08200-161">HANDAN BroadInfoCom Co., Ltd.</span></span>
* <span data-ttu-id="08200-162">Infomir GMBH</span><span class="sxs-lookup"><span data-stu-id="08200-162">Infomir GMBH</span></span>
* <span data-ttu-id="08200-163">Irdeto ABD Inc.</span><span class="sxs-lookup"><span data-stu-id="08200-163">Irdeto USA Inc.</span></span>
* <span data-ttu-id="08200-164">iWEDIA Güney Amerika</span><span class="sxs-lookup"><span data-stu-id="08200-164">iWEDIA S.A.</span></span> 
* <span data-ttu-id="08200-165">Serbest genel Hizmetleri BV</span><span class="sxs-lookup"><span data-stu-id="08200-165">Liberty Global Services BV</span></span>
* <span data-ttu-id="08200-166">MediaTek Inc.</span><span class="sxs-lookup"><span data-stu-id="08200-166">MediaTek Inc.</span></span>
* <span data-ttu-id="08200-167">MStar Co, Ltd</span><span class="sxs-lookup"><span data-stu-id="08200-167">MStar Co, Ltd</span></span>
* <span data-ttu-id="08200-168">Nintendo Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="08200-168">Nintendo Co., Ltd.</span></span>
* <span data-ttu-id="08200-169">OpenTV, Inc.</span><span class="sxs-lookup"><span data-stu-id="08200-169">OpenTV, Inc.</span></span>
* <span data-ttu-id="08200-170">Saffron dijital sınırlı</span><span class="sxs-lookup"><span data-stu-id="08200-170">Saffron Digital Limited</span></span>
* <span data-ttu-id="08200-171">Sichuan Changhong elektrik Co., Ltd</span><span class="sxs-lookup"><span data-stu-id="08200-171">Sichuan Changhong Electric Co., Ltd</span></span>
* <span data-ttu-id="08200-172">SoftAtHome</span><span class="sxs-lookup"><span data-stu-id="08200-172">SoftAtHome</span></span>
* <span data-ttu-id="08200-173">Sony Corporation</span><span class="sxs-lookup"><span data-stu-id="08200-173">Sony Corporation</span></span>
* <span data-ttu-id="08200-174">Tatung Technology Inc.</span><span class="sxs-lookup"><span data-stu-id="08200-174">Tatung Technology Inc.</span></span>
* <span data-ttu-id="08200-175">TCL Technoly elektronik bileşenleri (Huizhou) Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="08200-175">TCL Technoly Electronics (Huizhou) Co., Ltd.</span></span>
* <span data-ttu-id="08200-176">Üst sırrı Yatırımlar, Ltd</span><span class="sxs-lookup"><span data-stu-id="08200-176">Top Victory Investments, Ltd.</span></span>
* <span data-ttu-id="08200-177">Vestel Elektronik Sanayi ullanıcı Ticaret A.S.</span><span class="sxs-lookup"><span data-stu-id="08200-177">Vestel Elektronik Sanayi ve Ticaret A.S.</span></span>
* <span data-ttu-id="08200-178">VisualOn, Inc.</span><span class="sxs-lookup"><span data-stu-id="08200-178">VisualOn, Inc.</span></span>
* <span data-ttu-id="08200-179">ZTE Corporation</span><span class="sxs-lookup"><span data-stu-id="08200-179">ZTE Corporation</span></span>

## <a name="microsoft-smooth-streaming-client-final-product-agreement-licensees"></a><span data-ttu-id="08200-180">Microsoft istemci son ürün sözleşmesi lisans sahipleri akış kesintisiz</span><span class="sxs-lookup"><span data-stu-id="08200-180">Microsoft Smooth Streaming Client Final Product Agreement Licensees</span></span>
* <span data-ttu-id="08200-181">Gelişmiş dijital yayın SA'sı</span><span class="sxs-lookup"><span data-stu-id="08200-181">Advanced Digital Broadcast SA</span></span>
* <span data-ttu-id="08200-182">AirTies Kablosuz Iletism Sanayive Dış Ticaret A.S.</span><span class="sxs-lookup"><span data-stu-id="08200-182">AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.</span></span>
* <span data-ttu-id="08200-183">Albis teknolojileri Ltd.</span><span class="sxs-lookup"><span data-stu-id="08200-183">Albis Technologies Ltd.</span></span>
* <span data-ttu-id="08200-184">Amazon dijital Hizmetleri, Inc.</span><span class="sxs-lookup"><span data-stu-id="08200-184">Amazon Digital Services, Inc.</span></span>
* <span data-ttu-id="08200-185">AmTRAN teknoloji Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="08200-185">AmTRAN Technology Co., Ltd.</span></span>
* <span data-ttu-id="08200-186">Arcadyan teknoloji Corporation</span><span class="sxs-lookup"><span data-stu-id="08200-186">Arcadyan Technology Corporation</span></span>
* <span data-ttu-id="08200-187">Arion Technology, Inc.</span><span class="sxs-lookup"><span data-stu-id="08200-187">Arion Technology, Inc.</span></span>
* <span data-ttu-id="08200-188">ATMACA ELEKTRONİK SAN.</span><span class="sxs-lookup"><span data-stu-id="08200-188">ATMACA ELEKTRONİK SAN.</span></span> <span data-ttu-id="08200-189">HEDEFTEKİ TİC.</span><span class="sxs-lookup"><span data-stu-id="08200-189">VE TİC.</span></span> <span data-ttu-id="08200-190">A.Ş</span><span class="sxs-lookup"><span data-stu-id="08200-190">A.Ş</span></span>
* <span data-ttu-id="08200-191">İngiliz Sky yayın sınırlı</span><span class="sxs-lookup"><span data-stu-id="08200-191">British Sky Broadcasting Limited</span></span>
* <span data-ttu-id="08200-192">CastPal Technology Inc. Shenzhen</span><span class="sxs-lookup"><span data-stu-id="08200-192">CastPal Technology Inc., Shenzhen</span></span>
* <span data-ttu-id="08200-193">Compal Electronics, Inc.</span><span class="sxs-lookup"><span data-stu-id="08200-193">Compal Electronics, Inc.</span></span>
* <span data-ttu-id="08200-194">Dongguan dijital AV teknolojisi Corp., Ltd</span><span class="sxs-lookup"><span data-stu-id="08200-194">Dongguan Digital AV Technology Corp., Ltd.</span></span>
* <span data-ttu-id="08200-195">EchoStar Corporation'ın satın alma</span><span class="sxs-lookup"><span data-stu-id="08200-195">EchoStar Purchasing Corporation</span></span>
* <span data-ttu-id="08200-196">Enseo, Inc.</span><span class="sxs-lookup"><span data-stu-id="08200-196">Enseo, Inc.</span></span>
* <span data-ttu-id="08200-197">Filmflex filmler sınırlı</span><span class="sxs-lookup"><span data-stu-id="08200-197">Filmflex Movies Limited</span></span>
* <span data-ttu-id="08200-198">Fluendo Güney Amerika</span><span class="sxs-lookup"><span data-stu-id="08200-198">Fluendo S.A.</span></span>
* <span data-ttu-id="08200-199">Gibson yenilikleri sınırlı</span><span class="sxs-lookup"><span data-stu-id="08200-199">Gibson Innovations Limited</span></span>
* <span data-ttu-id="08200-200">Haier bilgi Applicantion S.R.L</span><span class="sxs-lookup"><span data-stu-id="08200-200">Haier Information Applicantion S.R.L</span></span>
* <span data-ttu-id="08200-201">HANDAN BroadInfoCom Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="08200-201">HANDAN BroadInfoCom Co., Ltd.</span></span>
* <span data-ttu-id="08200-202">Hisense uluslararası Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="08200-202">Hisense International Co., Ltd.</span></span> 
* <span data-ttu-id="08200-203">Homecast Co., Ltd</span><span class="sxs-lookup"><span data-stu-id="08200-203">Homecast Co.,Ltd</span></span>
* <span data-ttu-id="08200-204">Hon Hai duyarlık endüstri Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="08200-204">Hon Hai Precision Industry Co., Ltd.</span></span>
* <span data-ttu-id="08200-205">Infomir GMBH</span><span class="sxs-lookup"><span data-stu-id="08200-205">Infomir GMBH</span></span>
* <span data-ttu-id="08200-206">Kaonmedia Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="08200-206">Kaonmedia Co., Ltd.</span></span>
* <span data-ttu-id="08200-207">KDDI Corporation</span><span class="sxs-lookup"><span data-stu-id="08200-207">KDDI Corporation</span></span>
* <span data-ttu-id="08200-208">Nintendo Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="08200-208">Nintendo Co., Ltd.</span></span>
* <span data-ttu-id="08200-209">Turuncu SA'sı</span><span class="sxs-lookup"><span data-stu-id="08200-209">Orange SA</span></span>
* <span data-ttu-id="08200-210">Saffron dijital sınırlı</span><span class="sxs-lookup"><span data-stu-id="08200-210">Saffron Digital Limited</span></span>
* <span data-ttu-id="08200-211">Sagemcom geniş bant SAS</span><span class="sxs-lookup"><span data-stu-id="08200-211">Sagemcom Broadband SAS</span></span>
* <span data-ttu-id="08200-212">Shenzhen Coship Electronics CO., LTD</span><span class="sxs-lookup"><span data-stu-id="08200-212">Shenzhen Coship Electronics CO., LTD</span></span>
* <span data-ttu-id="08200-213">Shenzhen Jiuzhou elektrik Co., Ltd</span><span class="sxs-lookup"><span data-stu-id="08200-213">Shenzhen Jiuzhou Electric Co.,Ltd</span></span>
* <span data-ttu-id="08200-214">Shenzhen Skyworth dijital teknoloji Co., Ltd</span><span class="sxs-lookup"><span data-stu-id="08200-214">Shenzhen Skyworth Digital Technology Co., Ltd</span></span>
* <span data-ttu-id="08200-215">Sichuan Changhong elektrik Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="08200-215">Sichuan Changhong Electric Co., Ltd.</span></span>
* <span data-ttu-id="08200-216">Skardin endüstriyel Corp.</span><span class="sxs-lookup"><span data-stu-id="08200-216">Skardin Industrial Corp.</span></span>
* <span data-ttu-id="08200-217">Deutschland Fernsehen GmbH & Co. KG sky</span><span class="sxs-lookup"><span data-stu-id="08200-217">Sky Deutschland Fernsehen GmbH & Co. KG</span></span>
* <span data-ttu-id="08200-218">SmarDTV Güney Amerika</span><span class="sxs-lookup"><span data-stu-id="08200-218">SmarDTV S.A.</span></span>
* <span data-ttu-id="08200-219">SoftAtHome</span><span class="sxs-lookup"><span data-stu-id="08200-219">SoftAtHome</span></span>
* <span data-ttu-id="08200-220">Sony Corporation</span><span class="sxs-lookup"><span data-stu-id="08200-220">Sony Corporation</span></span>
* <span data-ttu-id="08200-221">TCL deniz aşırı pazarlama (Offshore Makao ticari) sınırlı</span><span class="sxs-lookup"><span data-stu-id="08200-221">TCL Overseas Marketing (Macao Commercial Offshore) Limited</span></span>
* <span data-ttu-id="08200-222">Technicolor teslim teknolojileri, SAS</span><span class="sxs-lookup"><span data-stu-id="08200-222">Technicolor Delivery Technologies, SAS</span></span>
* <span data-ttu-id="08200-223">Tongfang genel Ltd.</span><span class="sxs-lookup"><span data-stu-id="08200-223">Tongfang Global Ltd.</span></span>
* <span data-ttu-id="08200-224">Üst sırrı Yatırımlar, Ltd</span><span class="sxs-lookup"><span data-stu-id="08200-224">Top Victory Investments, Ltd.</span></span>
* <span data-ttu-id="08200-225">Toshiba Lifestyle ürünler ve hizmetler Corporation</span><span class="sxs-lookup"><span data-stu-id="08200-225">Toshiba Lifestyle Products & Services Corporation</span></span>
* <span data-ttu-id="08200-226">Evrensel medya Corporation /Slovakia/ s.r.o.</span><span class="sxs-lookup"><span data-stu-id="08200-226">Universal Media Corporation /Slovakia/ s.r.o.</span></span>
* <span data-ttu-id="08200-227">VIZIO, Inc.</span><span class="sxs-lookup"><span data-stu-id="08200-227">VIZIO, Inc.</span></span>
* <span data-ttu-id="08200-228">Wistron Corporation</span><span class="sxs-lookup"><span data-stu-id="08200-228">Wistron Corporation</span></span>
* <span data-ttu-id="08200-229">ZTE Corporation</span><span class="sxs-lookup"><span data-stu-id="08200-229">ZTE Corporation</span></span>


## <a name="media-services-learning-paths"></a><span data-ttu-id="08200-230">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="08200-230">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="08200-231">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="08200-231">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

