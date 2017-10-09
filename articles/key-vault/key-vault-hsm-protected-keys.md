---
title: "aaaHow toogenerate ve aktarım HSM korumalı anahtarları Azure anahtar kasası için | Microsoft Docs"
description: "Bu makale toohelp planlama, oluşturma ve ardından Azure anahtar kasası ile kendi HSM korumalı anahtarlar toouse aktarma kullanın. BYOK olarak da bilinen veya kendi anahtarını getir."
services: key-vault
documentationcenter: 
author: cabailey
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 51abafa1-812b-460f-a129-d714fdc391da
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: ambapat
ms.openlocfilehash: 3bb234bd1c4b81770542ccf7110e256385ca3309
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toogenerate-and-transfer-hsm-protected-keys-for-azure-key-vault"></a><span data-ttu-id="09e30-104">Nasıl toogenerate ve aktarım HSM korumalı anahtarları Azure anahtar kasası</span><span class="sxs-lookup"><span data-stu-id="09e30-104">How toogenerate and transfer HSM-protected keys for Azure Key Vault</span></span>
## <a name="introduction"></a><span data-ttu-id="09e30-105">Giriş</span><span class="sxs-lookup"><span data-stu-id="09e30-105">Introduction</span></span>
<span data-ttu-id="09e30-106">Ek güvence için Azure anahtar kasası kullandığınızda alabilir veya donanım güvenlik modülleri (HSM'ler)'hello HSM sınırını asla bırakın anahtarları oluştur.</span><span class="sxs-lookup"><span data-stu-id="09e30-106">For added assurance, when you use Azure Key Vault, you can import or generate keys in hardware security modules (HSMs) that never leave hello HSM boundary.</span></span> <span data-ttu-id="09e30-107">Bu senaryoda başvurulan tooas görülür *kendi anahtarını Getir*, veya BYOK.</span><span class="sxs-lookup"><span data-stu-id="09e30-107">This scenario is often referred tooas *bring your own key*, or BYOK.</span></span> <span data-ttu-id="09e30-108">Merhaba HSM'ler, FIPS 140-2 Düzey 2 doğrulanmasına şunlardır.</span><span class="sxs-lookup"><span data-stu-id="09e30-108">hello HSMs are FIPS 140-2 Level 2 validated.</span></span> <span data-ttu-id="09e30-109">Azure anahtar kasası HSM'ler tooprotect Thales nShield ailesi anahtarlarınızı kullanır.</span><span class="sxs-lookup"><span data-stu-id="09e30-109">Azure Key Vault uses Thales nShield family of HSMs tooprotect your keys.</span></span>

<span data-ttu-id="09e30-110">Bu konuda toohelp planlama, oluşturma ve ardından Azure anahtar kasası ile kendi HSM korumalı anahtarlar toouse aktarma Hello bilgileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="09e30-110">Use hello information in this topic toohelp you plan for, generate, and then transfer your own HSM-protected keys toouse with Azure Key Vault.</span></span>

<span data-ttu-id="09e30-111">Bu işlev Azure Çin için kullanılamıyor.</span><span class="sxs-lookup"><span data-stu-id="09e30-111">This functionality is not available for Azure China.</span></span>

> [!NOTE]
> <span data-ttu-id="09e30-112">Azure anahtar kasası hakkında daha fazla bilgi için bkz: [Azure anahtar kasası nedir?](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="09e30-112">For more information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>  
>
> <span data-ttu-id="09e30-113">Bir anahtar kasası için HSM korumalı anahtarlar oluşturma içeren bir başlangıç öğreticisinde için bkz: [Azure anahtar kasası ile çalışmaya başlama](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="09e30-113">For a getting started tutorial, which includes creating a key vault for HSM-protected keys, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span>
>
>

<span data-ttu-id="09e30-114">Oluşturma ve HSM korumalı anahtara hello Internet aktarma hakkında daha fazla bilgi için:</span><span class="sxs-lookup"><span data-stu-id="09e30-114">More information about generating and transferring an HSM-protected key over hello Internet:</span></span>

* <span data-ttu-id="09e30-115">Merhaba saldırı yüzeyini azaltan bir çevrimdışı iş istasyonundan hello anahtarı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="09e30-115">You generate hello key from an offline workstation, which reduces hello attack surface.</span></span>
* <span data-ttu-id="09e30-116">başlangıç anahtarı bir anahtar değişim anahtarı (aktarılan toohello Azure anahtar kasası HSM'ler olana kadar şifrelenmiş olarak kalan KEK ile), şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="09e30-116">hello key is encrypted with a Key Exchange Key (KEK), which stays encrypted until it is transferred toohello Azure Key Vault HSMs.</span></span> <span data-ttu-id="09e30-117">Yalnızca şifrelenmiş sürümü anahtarınızı hello hello özgün iş istasyonundan ayrılır.</span><span class="sxs-lookup"><span data-stu-id="09e30-117">Only hello encrypted version of your key leaves hello original workstation.</span></span>
* <span data-ttu-id="09e30-118">Merhaba araç takımı, anahtar toohello Azure anahtar kasası güvenlik dünyasına bağlar, Kiracı anahtarınızı özelliklerini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="09e30-118">hello toolset sets properties on your tenant key that binds your key toohello Azure Key Vault security world.</span></span> <span data-ttu-id="09e30-119">Bu nedenle Hello Azure anahtar kasası HSM'ler almak ve anahtarınızı şifresini sonra yalnızca bu HSM'ler bunu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="09e30-119">So after hello Azure Key Vault HSMs receive and decrypt your key, only these HSMs can use it.</span></span> <span data-ttu-id="09e30-120">Anahtarınız dışarı aktarılamaz.</span><span class="sxs-lookup"><span data-stu-id="09e30-120">Your key cannot be exported.</span></span> <span data-ttu-id="09e30-121">Bu bağlama hello Thales Hsm'leri tarafından zorlanır.</span><span class="sxs-lookup"><span data-stu-id="09e30-121">This binding is enforced by hello Thales HSMs.</span></span>
* <span data-ttu-id="09e30-122">Başlangıç anahtarınızı hello Azure anahtar kasası Hsm'lerinin içinde oluşturulur ve dışarı aktarılabilir olmadığı kullanılan tooencrypt olan anahtar değişim anahtarı (KEK).</span><span class="sxs-lookup"><span data-stu-id="09e30-122">hello Key Exchange Key (KEK) that is used tooencrypt your key is generated inside hello Azure Key Vault HSMs and is not exportable.</span></span> <span data-ttu-id="09e30-123">Merhaba HSM'ler hello KEK hello HSM'ler dışında NET bir sürümü olabilir uygulayın.</span><span class="sxs-lookup"><span data-stu-id="09e30-123">hello HSMs enforce that there can be no clear version of hello KEK outside hello HSMs.</span></span> <span data-ttu-id="09e30-124">Ayrıca, hello araç takımı KEK dışarı aktarılabilir olmadığı ve Thales tarafından üretilmiş orijinal bir HSM içinde oluşturulduğu bu hello Thales kanıtı içerir.</span><span class="sxs-lookup"><span data-stu-id="09e30-124">In addition, hello toolset includes attestation from Thales that hello KEK is not exportable and was generated inside a genuine HSM that was manufactured by Thales.</span></span>
* <span data-ttu-id="09e30-125">Merhaba araç takımı, hello Azure anahtar Kasası'nın güvenlik Dünyası da Thales tarafından üretilen orijinal bir HSM üzerinde oluşturulduğu Thales kanıtı içerir.</span><span class="sxs-lookup"><span data-stu-id="09e30-125">hello toolset includes attestation from Thales that hello Azure Key Vault security world was also generated on a genuine HSM manufactured by Thales.</span></span> <span data-ttu-id="09e30-126">Bu kanıtlama tooyou Microsoft orijinal donanım kullandığını kanıtlar.</span><span class="sxs-lookup"><span data-stu-id="09e30-126">This attestation proves tooyou that Microsoft is using genuine hardware.</span></span>
* <span data-ttu-id="09e30-127">Microsoft ve her bir coğrafi bölge güvenlik Dünyaları ayrı ayrı kullanır.</span><span class="sxs-lookup"><span data-stu-id="09e30-127">Microsoft uses separate KEKs and separate Security Worlds in each geographical region.</span></span> <span data-ttu-id="09e30-128">Bu ayrım anahtarınızı yalnızca veri merkezleri içinde şifrelediğiniz hello bölgede kullanılabilir olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="09e30-128">This separation ensures that your key can be used only in data centers in hello region in which you encrypted it.</span></span> <span data-ttu-id="09e30-129">Örneğin, Avrupalı bir müşterinin bir anahtarı Kuzey Amerika veya Asya'daki veri merkezlerinde kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="09e30-129">For example, a key from a European customer cannot be used in data centers in North American or Asia.</span></span>

## <a name="more-information-about-thales-hsms-and-microsoft-services"></a><span data-ttu-id="09e30-130">Thales Hsm'leri ve Microsoft Hizmetleri hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="09e30-130">More information about Thales HSMs and Microsoft services</span></span>
<span data-ttu-id="09e30-131">Thales e güvenlikle ilgili bir başında genel veri şifreleme ve siber güvenlik çözümleri toohello finansal hizmetler, yüksek teknoloji, üretim, kamu ve teknoloji sektörlerine sağlayıcısıdır.</span><span class="sxs-lookup"><span data-stu-id="09e30-131">Thales e-Security is a leading global provider of data encryption and cyber security solutions toohello financial services, high technology, manufacturing, government, and technology sectors.</span></span> <span data-ttu-id="09e30-132">40 yıllık korumadaki Kurumsal ve resmi bilgileri ile Thales çözümleri dört hello beş büyük enerji ve Havacılık şirketler tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="09e30-132">With a 40-year track record of protecting corporate and government information, Thales solutions are used by four of hello five largest energy and aerospace companies.</span></span> <span data-ttu-id="09e30-133">Çözümleri 22 NATO ülkesi tarafından da kullanılır ve birden fazla yüzde 80'tüm dünyadaki ödeme işlemlerinin güvenli.</span><span class="sxs-lookup"><span data-stu-id="09e30-133">Their solutions are also used by 22 NATO countries, and secure more than 80 per cent of worldwide payment transactions.</span></span>

<span data-ttu-id="09e30-134">Microsoft Thales tooenhance hello durumuyla resim HSM'ler için iş Birliği yapmaktadır.</span><span class="sxs-lookup"><span data-stu-id="09e30-134">Microsoft has collaborated with Thales tooenhance hello state of art for HSMs.</span></span> <span data-ttu-id="09e30-135">Bu geliştirmeler, tooget hello tipik yararları anahtarlarınızı üzerinde bırakmasını denetime sahip olmadan barındırılan hizmetler sağlar.</span><span class="sxs-lookup"><span data-stu-id="09e30-135">These enhancements enable you tooget hello typical benefits of hosted services without relinquishing control over your keys.</span></span> <span data-ttu-id="09e30-136">Özellikle, bu geliştirmeler, Microsoft'un gerek yoktur, böylece hello HSM'ler yönetmesine izin.</span><span class="sxs-lookup"><span data-stu-id="09e30-136">Specifically, these enhancements let Microsoft manage hello HSMs so that you do not have to.</span></span> <span data-ttu-id="09e30-137">Hizmet, Azure anahtar kasası kısa bildirimi toomeet ölçeklendirir bulut olarak kuruluşunuzun kullanım ani.</span><span class="sxs-lookup"><span data-stu-id="09e30-137">As a cloud service, Azure Key Vault scales up at short notice toomeet your organization’s usage spikes.</span></span> <span data-ttu-id="09e30-138">AT hello aynı zaman, anahtarınız, Microsoft'un Hsm'leri içerisinde korunur: hello anahtarı oluşturma ve tooMicrosoft'ın HSM'ler aktarma çünkü hello anahtar yaşam döngüsü üzerinde denetimi korumak.</span><span class="sxs-lookup"><span data-stu-id="09e30-138">At hello same time, your key is protected inside Microsoft’s HSMs: You retain control over hello key lifecycle because you generate hello key and transfer it tooMicrosoft’s HSMs.</span></span>

## <a name="implementing-bring-your-own-key-byok-for-azure-key-vault"></a><span data-ttu-id="09e30-139">Uygulama kendi anahtarını getir (BYOK) için Azure anahtar kasası</span><span class="sxs-lookup"><span data-stu-id="09e30-139">Implementing bring your own key (BYOK) for Azure Key Vault</span></span>
<span data-ttu-id="09e30-140">Kullanım Merhaba, kendi HSM korumalı anahtara oluşturmak ve tooAzure anahtar kasası aktarım bilgi ve yordamları izleyerek — hello kendi anahtarı (BYOK) senaryosu getirin.</span><span class="sxs-lookup"><span data-stu-id="09e30-140">Use hello following information and procedures if you will generate your own HSM-protected key and then transfer it tooAzure Key Vault—hello bring your own key (BYOK) scenario.</span></span>

## <a name="prerequisites-for-byok"></a><span data-ttu-id="09e30-141">BYOK için Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="09e30-141">Prerequisites for BYOK</span></span>
<span data-ttu-id="09e30-142">Tablo için bir önkoşul listesi için aşağıdaki hello kendi anahtarını getir (BYOK) Azure anahtar kasası için bkz.</span><span class="sxs-lookup"><span data-stu-id="09e30-142">See hello following table for a list of prerequisites for bring your own key (BYOK) for Azure Key Vault.</span></span>

| <span data-ttu-id="09e30-143">Gereksinim</span><span class="sxs-lookup"><span data-stu-id="09e30-143">Requirement</span></span> | <span data-ttu-id="09e30-144">Daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="09e30-144">More information</span></span> |
| --- | --- |
| <span data-ttu-id="09e30-145">Bir abonelik tooAzure</span><span class="sxs-lookup"><span data-stu-id="09e30-145">A subscription tooAzure</span></span> |<span data-ttu-id="09e30-146">Azure anahtar kasası toocreate, bir Azure aboneliği gerekir: [ücretsiz deneme için kaydolun](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="09e30-146">toocreate an Azure Key Vault, you need an Azure subscription: [Sign up for free trial](https://azure.microsoft.com/pricing/free-trial/)</span></span> |
| <span data-ttu-id="09e30-147">Azure anahtar kasası Premium Hizmet katmanını toosupport HSM korumalı anahtarlar hello</span><span class="sxs-lookup"><span data-stu-id="09e30-147">hello Azure Key Vault Premium service tier toosupport HSM-protected keys</span></span> |<span data-ttu-id="09e30-148">Azure anahtar kasası hello hizmet katmanları ve yetenekler hakkında daha fazla bilgi için bkz: Merhaba [Azure anahtar kasası fiyatlandırma](https://azure.microsoft.com/pricing/details/key-vault/) Web sitesi.</span><span class="sxs-lookup"><span data-stu-id="09e30-148">For more information about hello service tiers and capabilities for Azure Key Vault, see hello [Azure Key Vault Pricing](https://azure.microsoft.com/pricing/details/key-vault/) website.</span></span> |
| <span data-ttu-id="09e30-149">Thales HSM, akıllı kartlar ve destek yazılımı</span><span class="sxs-lookup"><span data-stu-id="09e30-149">Thales HSM, smartcards, and support software</span></span> |<span data-ttu-id="09e30-150">Bilmeniz gereken erişim tooa Thales donanım güvenlik modülü ve Thales HSM'ler hakkında temel operasyonel bilginiz.</span><span class="sxs-lookup"><span data-stu-id="09e30-150">You must have access tooa Thales Hardware Security Module and basic operational knowledge of Thales HSMs.</span></span> <span data-ttu-id="09e30-151">Bkz: [Thales donanım güvenlik modülü](https://www.thales-esecurity.com/msrms/buy) uyumlu modellerin veya toopurchase bir yoksa bir HSM hello listesi için.</span><span class="sxs-lookup"><span data-stu-id="09e30-151">See [Thales Hardware Security Module](https://www.thales-esecurity.com/msrms/buy) for hello list of compatible models, or toopurchase an HSM if you do not have one.</span></span> |
| <span data-ttu-id="09e30-152">Donanım ve yazılım hello:</span><span class="sxs-lookup"><span data-stu-id="09e30-152">hello following hardware and software:</span></span><ol><li><span data-ttu-id="09e30-153">Çevrimdışı bir x64 en az bir Windows işletim sistemi en az Windows 7 ve Thales nShield yazılımı sürümü ile iş istasyonu sürüm 11.50.</span><span class="sxs-lookup"><span data-stu-id="09e30-153">An offline x64 workstation with a minimum Windows operation system of Windows 7 and Thales nShield software that is at least version 11.50.</span></span><br/><br/><span data-ttu-id="09e30-154">Bu iş istasyonu Windows 7 çalıştırıyorsa, şunları yapmalısınız [Microsoft .NET Framework 4.5 sürümünü yüklemeniz](http://download.microsoft.com/download/b/a/4/ba4a7e71-2906-4b2d-a0e1-80cf16844f5f/dotnetfx45_full_x86_x64.exe).</span><span class="sxs-lookup"><span data-stu-id="09e30-154">If this workstation runs Windows 7, you must [install Microsoft .NET Framework 4.5](http://download.microsoft.com/download/b/a/4/ba4a7e71-2906-4b2d-a0e1-80cf16844f5f/dotnetfx45_full_x86_x64.exe).</span></span></li><li><span data-ttu-id="09e30-155">Bağlı toohello Internet ve Windows 7'in en az bir Windows işletim sistemi olan bir iş istasyonu ve [Azure PowerShell](/powershell/azure/overview) **en düşük sürüm 1.1.0** yüklü.</span><span class="sxs-lookup"><span data-stu-id="09e30-155">A workstation that is connected toohello Internet and has a minimum Windows operating system of Windows 7 and [Azure PowerShell](/powershell/azure/overview) **minimum version 1.1.0** installed.</span></span></li><li><span data-ttu-id="09e30-156">Bir USB sürücü veya en az 16 MB boş alana sahip başka bir taşınabilir depolama cihazı.</span><span class="sxs-lookup"><span data-stu-id="09e30-156">A USB drive or other portable storage device that has at least 16 MB free space.</span></span></li></ol> |<span data-ttu-id="09e30-157">Güvenlik nedenleriyle, o hello ilk iş istasyonunun bağlı tooa ağ değil öneririz.</span><span class="sxs-lookup"><span data-stu-id="09e30-157">For security reasons, we recommend that hello first workstation is not connected tooa network.</span></span> <span data-ttu-id="09e30-158">Ancak, bu öneri program aracılığıyla zorlanmaz.</span><span class="sxs-lookup"><span data-stu-id="09e30-158">However, this recommendation is not programmatically enforced.</span></span><br/><br/><span data-ttu-id="09e30-159">İzleyen hello yönergelerde başvurulan tooas hello bağlantısı kesilmiş iş istasyonu bu iş istasyonu olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="09e30-159">Note that in hello instructions that follow, this workstation is referred tooas hello disconnected workstation.</span></span></p></blockquote><br/><span data-ttu-id="09e30-160">Ayrıca, Kiracı anahtarınız bir üretim ağı için ise, ikinci ve ayrı iş istasyonu toodownload hello araç takımını ve karşıya yükleme hello Kiracı anahtarı kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="09e30-160">In addition, if your tenant key is for a production network, we recommend that you use a second, separate workstation toodownload hello toolset and upload hello tenant key.</span></span> <span data-ttu-id="09e30-161">Ancak test amacıyla kullanabilirsiniz birinci hello gibi aynı iş istasyonunu hello.</span><span class="sxs-lookup"><span data-stu-id="09e30-161">But for testing purposes, you can use hello same workstation as hello first one.</span></span><br/><br/><span data-ttu-id="09e30-162">İzleyen hello yönergelerde bu ikinci iş istasyonu başvurulan tooas hello Internet'e bağlı iş istasyonu olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="09e30-162">Note that in hello instructions that follow, this second workstation is referred tooas hello Internet-connected workstation.</span></span></p></blockquote><br/> |

## <a name="generate-and-transfer-your-key-tooazure-key-vault-hsm"></a><span data-ttu-id="09e30-163">Oluşturma ve anahtar kasası HSM anahtar, tooAzure aktarma</span><span class="sxs-lookup"><span data-stu-id="09e30-163">Generate and transfer your key tooAzure Key Vault HSM</span></span>
<span data-ttu-id="09e30-164">Aşağıdaki beş adımları toogenerate hello kullanabilir ve Azure anahtar kasası HSM anahtar, tooan aktarım:</span><span class="sxs-lookup"><span data-stu-id="09e30-164">You will use hello following five steps toogenerate and transfer your key tooan Azure Key Vault HSM:</span></span>

* [<span data-ttu-id="09e30-165">1. adım: Internet'e bağlı iş istasyonunuzu hazırlama</span><span class="sxs-lookup"><span data-stu-id="09e30-165">Step 1: Prepare your Internet-connected workstation</span></span>](#step-1-prepare-your-internet-connected-workstation)
* [<span data-ttu-id="09e30-166">2. adım: bağlantısı kesilmiş iş istasyonunuzu hazırlama</span><span class="sxs-lookup"><span data-stu-id="09e30-166">Step 2: Prepare your disconnected workstation</span></span>](#step-2-prepare-your-disconnected-workstation)
* [<span data-ttu-id="09e30-167">3. adım: anahtarınızı oluştur</span><span class="sxs-lookup"><span data-stu-id="09e30-167">Step 3: Generate your key</span></span>](#step-3-generate-your-key)
* [<span data-ttu-id="09e30-168">4. adım: anahtarınızı aktarım için hazırlama</span><span class="sxs-lookup"><span data-stu-id="09e30-168">Step 4: Prepare your key for transfer</span></span>](#step-4-prepare-your-key-for-transfer)
* [<span data-ttu-id="09e30-169">5. adım: Aktarım, anahtar tooAzure anahtar kasası</span><span class="sxs-lookup"><span data-stu-id="09e30-169">Step 5: Transfer your key tooAzure Key Vault</span></span>](#step-5-transfer-your-key-to-azure-key-vault)

## <a name="step-1-prepare-your-internet-connected-workstation"></a><span data-ttu-id="09e30-170">1. adım: Internet'e bağlı iş istasyonunuzu hazırlama</span><span class="sxs-lookup"><span data-stu-id="09e30-170">Step 1: Prepare your Internet-connected workstation</span></span>
<span data-ttu-id="09e30-171">Birinci adım için aşağıdaki bağlı toohello Internet olan iş istasyonunuza yordamlarını hello.</span><span class="sxs-lookup"><span data-stu-id="09e30-171">For this first step, do hello following procedures on your workstation that is connected toohello Internet.</span></span>

### <a name="step-11-install-azure-powershell"></a><span data-ttu-id="09e30-172">1.1. adım: Azure PowerShell'i yükleme</span><span class="sxs-lookup"><span data-stu-id="09e30-172">Step 1.1: Install Azure PowerShell</span></span>
<span data-ttu-id="09e30-173">Merhaba Internet'e bağlı iş istasyonundan, indirin ve hello cmdlet'leri toomanage Azure anahtar kasası içerir hello Azure PowerShell modülünü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="09e30-173">From hello Internet-connected workstation, download and install hello Azure PowerShell module that includes hello cmdlets toomanage Azure Key Vault.</span></span> <span data-ttu-id="09e30-174">Bu 0.8.13 en az bir sürümünü gerektirir.</span><span class="sxs-lookup"><span data-stu-id="09e30-174">This requires a minimum version of 0.8.13.</span></span>

<span data-ttu-id="09e30-175">Yükleme yönergeleri için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="09e30-175">For installation instructions, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

### <a name="step-12-get-your-azure-subscription-id"></a><span data-ttu-id="09e30-176">1.2. adım: Azure abonelik Kimliğinizi alma</span><span class="sxs-lookup"><span data-stu-id="09e30-176">Step 1.2: Get your Azure subscription ID</span></span>
<span data-ttu-id="09e30-177">Bir Azure PowerShell oturumu başlatın ve tooyour Azure hesabı komutu aşağıdaki hello kullanarak oturum açın:</span><span class="sxs-lookup"><span data-stu-id="09e30-177">Start an Azure PowerShell session and sign in tooyour Azure account by using hello following command:</span></span>

        Add-AzureAccount
<span data-ttu-id="09e30-178">Merhaba açılır tarayıcı penceresinde Azure hesabı kullanıcı adınızı ve parolanızı girin.</span><span class="sxs-lookup"><span data-stu-id="09e30-178">In hello pop-up browser window, enter your Azure account user name and password.</span></span> <span data-ttu-id="09e30-179">Ardından hello kullanın [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) komutu:</span><span class="sxs-lookup"><span data-stu-id="09e30-179">Then, use hello [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) command:</span></span>

        Get-AzureSubscription
<span data-ttu-id="09e30-180">Merhaba çıktısını Azure anahtar kasası için kullanacağınız hello abonelik için hello Kimliğini bulun.</span><span class="sxs-lookup"><span data-stu-id="09e30-180">From hello output, locate hello ID for hello subscription you will use for Azure Key Vault.</span></span> <span data-ttu-id="09e30-181">Bu abonelik kimliği daha sonra ihtiyacınız olacak.</span><span class="sxs-lookup"><span data-stu-id="09e30-181">You will need this subscription ID later.</span></span>

<span data-ttu-id="09e30-182">Hello Azure PowerShell penceresini kapatmayın.</span><span class="sxs-lookup"><span data-stu-id="09e30-182">Do not close hello Azure PowerShell window.</span></span>

### <a name="step-13-download-hello-byok-toolset-for-azure-key-vault"></a><span data-ttu-id="09e30-183">1.3. adım: Azure anahtar kasası için hello BYOK araç takımı indirme</span><span class="sxs-lookup"><span data-stu-id="09e30-183">Step 1.3: Download hello BYOK toolset for Azure Key Vault</span></span>
<span data-ttu-id="09e30-184">Toohello Microsoft Download Center gidin ve [hello Azure anahtar kasası BYOK araç takımı indirme](http://www.microsoft.com/download/details.aspx?id=45345) coğrafi bölge veya Azure örneği.</span><span class="sxs-lookup"><span data-stu-id="09e30-184">Go toohello Microsoft Download Center and [download hello Azure Key Vault BYOK toolset](http://www.microsoft.com/download/details.aspx?id=45345) for your geographic region or instance of Azure.</span></span> <span data-ttu-id="09e30-185">Merhaba aşağıdaki kullanın bilgi tooidentify hello paket adı toodownload ve karşılık gelen, SHA-256 karma paketi:</span><span class="sxs-lookup"><span data-stu-id="09e30-185">Use hello following information tooidentify hello package name toodownload and its corresponding SHA-256 package hash:</span></span>

- - -
<span data-ttu-id="09e30-186">**Amerika Birleşik Devletleri:**</span><span class="sxs-lookup"><span data-stu-id="09e30-186">**United States:**</span></span>

<span data-ttu-id="09e30-187">States.zip KeyVault-BYOK-araçları-birleşik</span><span class="sxs-lookup"><span data-stu-id="09e30-187">KeyVault-BYOK-Tools-UnitedStates.zip</span></span>

<span data-ttu-id="09e30-188">760EE9BD6445C87CFF0E8B032577118704B3BEAA045AA55977C10EF68BC67E2B</span><span class="sxs-lookup"><span data-stu-id="09e30-188">760EE9BD6445C87CFF0E8B032577118704B3BEAA045AA55977C10EF68BC67E2B</span></span>

- - -
<span data-ttu-id="09e30-189">**Avrupa:**</span><span class="sxs-lookup"><span data-stu-id="09e30-189">**Europe:**</span></span>

<span data-ttu-id="09e30-190">BYOK araçları Europe.zip KeyVault</span><span class="sxs-lookup"><span data-stu-id="09e30-190">KeyVault-BYOK-Tools-Europe.zip</span></span>

<span data-ttu-id="09e30-191">7A64B94225F59B847C5C27C2200BAD7D16C901E1687767EDBBB8B09BB285011D</span><span class="sxs-lookup"><span data-stu-id="09e30-191">7A64B94225F59B847C5C27C2200BAD7D16C901E1687767EDBBB8B09BB285011D</span></span>

- - -
<span data-ttu-id="09e30-192">**Asya:**</span><span class="sxs-lookup"><span data-stu-id="09e30-192">**Asia:**</span></span>

<span data-ttu-id="09e30-193">BYOK araçları AsiaPacific.zip KeyVault</span><span class="sxs-lookup"><span data-stu-id="09e30-193">KeyVault-BYOK-Tools-AsiaPacific.zip</span></span>

<span data-ttu-id="09e30-194">813DC94B23079CF7A5CEA71D5B444E86B292F463C53EE47AED25D4F7CD58E7D8</span><span class="sxs-lookup"><span data-stu-id="09e30-194">813DC94B23079CF7A5CEA71D5B444E86B292F463C53EE47AED25D4F7CD58E7D8</span></span>

- - -
<span data-ttu-id="09e30-195">**Latin Amerika:**</span><span class="sxs-lookup"><span data-stu-id="09e30-195">**Latin America:**</span></span>

<span data-ttu-id="09e30-196">BYOK araçları LatinAmerica.zip KeyVault</span><span class="sxs-lookup"><span data-stu-id="09e30-196">KeyVault-BYOK-Tools-LatinAmerica.zip</span></span>

<span data-ttu-id="09e30-197">3F29069E3500F95C0E156F4B8914E1DC60C20FB64B464306A299EA5145D755C0</span><span class="sxs-lookup"><span data-stu-id="09e30-197">3F29069E3500F95C0E156F4B8914E1DC60C20FB64B464306A299EA5145D755C0</span></span>

- - -
<span data-ttu-id="09e30-198">**Japonya:**</span><span class="sxs-lookup"><span data-stu-id="09e30-198">**Japan:**</span></span>

<span data-ttu-id="09e30-199">BYOK araçları Japan.zip KeyVault</span><span class="sxs-lookup"><span data-stu-id="09e30-199">KeyVault-BYOK-Tools-Japan.zip</span></span>

<span data-ttu-id="09e30-200">453FFEA2F8F410720B68B8BAC4CF79135A7F37F4E491FF840BE9E69E88A98C90</span><span class="sxs-lookup"><span data-stu-id="09e30-200">453FFEA2F8F410720B68B8BAC4CF79135A7F37F4E491FF840BE9E69E88A98C90</span></span>

- - -
<span data-ttu-id="09e30-201">**Kore:**</span><span class="sxs-lookup"><span data-stu-id="09e30-201">**Korea:**</span></span>

<span data-ttu-id="09e30-202">BYOK araçları Korea.zip KeyVault</span><span class="sxs-lookup"><span data-stu-id="09e30-202">KeyVault-BYOK-Tools-Korea.zip</span></span>

<span data-ttu-id="09e30-203">C17B7E93224DA80F5668E09CF7DAE2F92527E8226179995BBE2E43DA4323595A</span><span class="sxs-lookup"><span data-stu-id="09e30-203">C17B7E93224DA80F5668E09CF7DAE2F92527E8226179995BBE2E43DA4323595A</span></span>

- - -
<span data-ttu-id="09e30-204">**Avustralya:**</span><span class="sxs-lookup"><span data-stu-id="09e30-204">**Australia:**</span></span>

<span data-ttu-id="09e30-205">BYOK araçları Australia.zip KeyVault</span><span class="sxs-lookup"><span data-stu-id="09e30-205">KeyVault-BYOK-Tools-Australia.zip</span></span>

<span data-ttu-id="09e30-206">4AD893396E86F2D2A71682876A6A8EA59E3C7895BEAD2F7E7C8516682582C34B</span><span class="sxs-lookup"><span data-stu-id="09e30-206">4AD893396E86F2D2A71682876A6A8EA59E3C7895BEAD2F7E7C8516682582C34B</span></span>

- - -
[<span data-ttu-id="09e30-207">**Azure kamu:**</span><span class="sxs-lookup"><span data-stu-id="09e30-207">**Azure Government:**</span></span>](https://azure.microsoft.com/features/gov/)

<span data-ttu-id="09e30-208">BYOK araçları USGovCloud.zip KeyVault</span><span class="sxs-lookup"><span data-stu-id="09e30-208">KeyVault-BYOK-Tools-USGovCloud.zip</span></span>

<span data-ttu-id="09e30-209">3AAE1A96B9D15B899B8126CFC0380719EB54FDF2EA94489B43FAD21ECC745F64</span><span class="sxs-lookup"><span data-stu-id="09e30-209">3AAE1A96B9D15B899B8126CFC0380719EB54FDF2EA94489B43FAD21ECC745F64</span></span>

- - -
<span data-ttu-id="09e30-210">**ABD hükümeti savunma Bakanlığı:**</span><span class="sxs-lookup"><span data-stu-id="09e30-210">**US Government DOD:**</span></span>

<span data-ttu-id="09e30-211">BYOK araçları USGovernmentDoD.zip KeyVault</span><span class="sxs-lookup"><span data-stu-id="09e30-211">KeyVault-BYOK-Tools-USGovernmentDoD.zip</span></span>

<span data-ttu-id="09e30-212">A61E78297B0732DF2682FDE63D7B572CE4D23B0BC27CC48AFF620BD060BB9E9D</span><span class="sxs-lookup"><span data-stu-id="09e30-212">A61E78297B0732DF2682FDE63D7B572CE4D23B0BC27CC48AFF620BD060BB9E9D</span></span>

- - -
<span data-ttu-id="09e30-213">**Kanada:**</span><span class="sxs-lookup"><span data-stu-id="09e30-213">**Canada:**</span></span>

<span data-ttu-id="09e30-214">BYOK araçları Canada.zip KeyVault</span><span class="sxs-lookup"><span data-stu-id="09e30-214">KeyVault-BYOK-Tools-Canada.zip</span></span>

<span data-ttu-id="09e30-215">30B87A0BA8208F6B7241C30C794FED1C370D7445ACA179685816E4E156CD2AF7</span><span class="sxs-lookup"><span data-stu-id="09e30-215">30B87A0BA8208F6B7241C30C794FED1C370D7445ACA179685816E4E156CD2AF7</span></span>

- - -
<span data-ttu-id="09e30-216">**Almanya:**</span><span class="sxs-lookup"><span data-stu-id="09e30-216">**Germany:**</span></span>

<span data-ttu-id="09e30-217">BYOK araçları Germany.zip KeyVault</span><span class="sxs-lookup"><span data-stu-id="09e30-217">KeyVault-BYOK-Tools-Germany.zip</span></span>

<span data-ttu-id="09e30-218">5E3E4AA54715E4F93C3C145035B18275B7C6815A06D7ABB212E7FADBF2929261</span><span class="sxs-lookup"><span data-stu-id="09e30-218">5E3E4AA54715E4F93C3C145035B18275B7C6815A06D7ABB212E7FADBF2929261</span></span>

- - -
<span data-ttu-id="09e30-219">**Hindistan:**</span><span class="sxs-lookup"><span data-stu-id="09e30-219">**India:**</span></span>

<span data-ttu-id="09e30-220">BYOK araçları India.zip KeyVault</span><span class="sxs-lookup"><span data-stu-id="09e30-220">KeyVault-BYOK-Tools-India.zip</span></span>

<span data-ttu-id="09e30-221">136733A6C6A71D75571BB80819B3D55A9B83CCAD5C996C686BC5682A3F369BF7</span><span class="sxs-lookup"><span data-stu-id="09e30-221">136733A6C6A71D75571BB80819B3D55A9B83CCAD5C996C686BC5682A3F369BF7</span></span>

- - -
<span data-ttu-id="09e30-222">**Birleşik Krallık:**</span><span class="sxs-lookup"><span data-stu-id="09e30-222">**United Kingdom:**</span></span>

<span data-ttu-id="09e30-223">BYOK araçları UnitedKingdom.zip KeyVault</span><span class="sxs-lookup"><span data-stu-id="09e30-223">KeyVault-BYOK-Tools-UnitedKingdom.zip</span></span>

<span data-ttu-id="09e30-224">ED331A6F1D34A402317D3F27D5396046AF0E5C2D44B5D10CCCE293472942D268</span><span class="sxs-lookup"><span data-stu-id="09e30-224">ED331A6F1D34A402317D3F27D5396046AF0E5C2D44B5D10CCCE293472942D268</span></span>

- - -

<span data-ttu-id="09e30-225">toovalidate Merhaba, indirilen BYOK araç takımı, kullanım Merhaba, Azure PowerShell oturumundan bütünlüğünü [Get-FileHash](https://technet.microsoft.com/library/dn520872.aspx) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="09e30-225">toovalidate hello integrity of your downloaded BYOK toolset, from your Azure PowerShell session, use hello [Get-FileHash](https://technet.microsoft.com/library/dn520872.aspx) cmdlet.</span></span>

    Get-FileHash KeyVault-BYOK-Tools-*.zip

<span data-ttu-id="09e30-226">Merhaba araç takımı hello aşağıdakileri içerir:</span><span class="sxs-lookup"><span data-stu-id="09e30-226">hello toolset includes hello following:</span></span>

* <span data-ttu-id="09e30-227">İle başlayan bir ada sahip olan bir anahtar değişim anahtarı (KEK) paketi **BYOK-KEK - pkg-.**</span><span class="sxs-lookup"><span data-stu-id="09e30-227">A Key Exchange Key (KEK) package that has a name beginning with **BYOK-KEK-pkg-.**</span></span>
* <span data-ttu-id="09e30-228">İle başlayan bir ada sahip olan bir güvenlik Dünyası paketi **BYOK-SecurityWorld - pkg-.**</span><span class="sxs-lookup"><span data-stu-id="09e30-228">A Security World package that has a name beginning with **BYOK-SecurityWorld-pkg-.**</span></span>
* <span data-ttu-id="09e30-229">Adlı bir python komut **verifykeypackage.py.**</span><span class="sxs-lookup"><span data-stu-id="09e30-229">A python script named **verifykeypackage.py.**</span></span>
* <span data-ttu-id="09e30-230">Adlı bir komut satırı yürütülebilir dosyası **KeyTransferRemote.exe** ve ilişkili DLL'ler.</span><span class="sxs-lookup"><span data-stu-id="09e30-230">A command-line executable file named **KeyTransferRemote.exe** and associated DLLs.</span></span>
* <span data-ttu-id="09e30-231">Adlı bir Visual C++ yeniden dağıtılabilir paketi, **vcredist_x64.exe.**</span><span class="sxs-lookup"><span data-stu-id="09e30-231">A Visual C++ Redistributable Package, named **vcredist_x64.exe.**</span></span>

<span data-ttu-id="09e30-232">Merhaba paket tooa USB sürücü veya başka bir taşınabilir depolama kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="09e30-232">Copy hello package tooa USB drive or other portable storage.</span></span>

## <a name="step-2-prepare-your-disconnected-workstation"></a><span data-ttu-id="09e30-233">2. adım: bağlantısı kesilmiş iş istasyonunuzu hazırlama</span><span class="sxs-lookup"><span data-stu-id="09e30-233">Step 2: Prepare your disconnected workstation</span></span>
<span data-ttu-id="09e30-234">Bu ikinci adım için bağlı tooa ağ (Merhaba Internet veya iç ağınıza) olup olmadığını hello iş istasyonunda aşağıdaki yordamlarını hello.</span><span class="sxs-lookup"><span data-stu-id="09e30-234">For this second step, do hello following procedures on hello workstation that is not connected tooa network (either hello Internet or your internal network).</span></span>

### <a name="step-21-prepare-hello-disconnected-workstation-with-thales-hsm"></a><span data-ttu-id="09e30-235">2.1. adım: Thales HSM ile hello bağlantısı kesilmiş iş istasyonunuzu hazırlama</span><span class="sxs-lookup"><span data-stu-id="09e30-235">Step 2.1: Prepare hello disconnected workstation with Thales HSM</span></span>
<span data-ttu-id="09e30-236">Merhaba nCipher (Thales) destek yazılımını bir Windows bilgisayara yükleyin ve ardından bir Thales HSM toothat bilgisayar ekleyin.</span><span class="sxs-lookup"><span data-stu-id="09e30-236">Install hello nCipher (Thales) support software on a Windows computer, and then attach a Thales HSM toothat computer.</span></span>

<span data-ttu-id="09e30-237">Thales araçları bu hello yolunuzda olduğundan emin olun (**%nfast_home%\bin**).</span><span class="sxs-lookup"><span data-stu-id="09e30-237">Ensure that hello Thales tools are in your path (**%nfast_home%\bin**).</span></span> <span data-ttu-id="09e30-238">Örneğin, hello aşağıdakileri yazın:</span><span class="sxs-lookup"><span data-stu-id="09e30-238">For example, type hello following:</span></span>

        set PATH=%PATH%;"%nfast_home%\bin"

<span data-ttu-id="09e30-239">Daha fazla bilgi için Thales HSM hello ile Merhaba kullanıcı kılavuzuna bakın.</span><span class="sxs-lookup"><span data-stu-id="09e30-239">For more information, see hello user guide included with hello Thales HSM.</span></span>

### <a name="step-22-install-hello-byok-toolset-on-hello-disconnected-workstation"></a><span data-ttu-id="09e30-240">2.2. adım: Merhaba bağlantısı kesilmiş iş istasyonunda yükleme hello BYOK araç takımı</span><span class="sxs-lookup"><span data-stu-id="09e30-240">Step 2.2: Install hello BYOK toolset on hello disconnected workstation</span></span>
<span data-ttu-id="09e30-241">Merhaba USB sürücü veya başka bir taşınabilir depolama Hello BYOK araç takımı paketini kopyalayın ve ardından aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="09e30-241">Copy hello BYOK toolset package from hello USB drive or other portable storage, and then do hello following:</span></span>

1. <span data-ttu-id="09e30-242">Merhaba dosyaları karşıdan hello paketinden herhangi bir klasöre ayıklayın.</span><span class="sxs-lookup"><span data-stu-id="09e30-242">Extract hello files from hello downloaded package into any folder.</span></span>
2. <span data-ttu-id="09e30-243">Bu klasörden vcredist_x64.exe çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="09e30-243">From that folder, run vcredist_x64.exe.</span></span>
3. <span data-ttu-id="09e30-244">Toohello yükleme hello Visual C++ çalışma zamanı bileşenleri için Visual Studio 2013 hello yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="09e30-244">Follow hello instructions toohello install hello Visual C++ runtime components for Visual Studio 2013.</span></span>

## <a name="step-3-generate-your-key"></a><span data-ttu-id="09e30-245">3. adım: anahtarınızı oluştur</span><span class="sxs-lookup"><span data-stu-id="09e30-245">Step 3: Generate your key</span></span>
<span data-ttu-id="09e30-246">Bu üçüncü adımı için aşağıdaki hello bağlantısı kesilmiş iş istasyonunda yordamlarını hello.</span><span class="sxs-lookup"><span data-stu-id="09e30-246">For this third step, do hello following procedures on hello disconnected workstation.</span></span> <span data-ttu-id="09e30-247">toocomplete Bu adım, HSM başlatma modunda olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="09e30-247">toocomplete this step your HSM must be in initialization mode.</span></span> 


### <a name="step-31-change-hello-hsm-mode-tooi"></a><span data-ttu-id="09e30-248">3.1. adım: hello HSM modu too'I değiştirmek '</span><span class="sxs-lookup"><span data-stu-id="09e30-248">Step 3.1: Change hello HSM mode too'I'</span></span>
<span data-ttu-id="09e30-249">Thales nShield kenar, toochange hello modu kullanıyorsanız: 1.</span><span class="sxs-lookup"><span data-stu-id="09e30-249">If you are using Thales nShield Edge, toochange hello mode: 1.</span></span> <span data-ttu-id="09e30-250">Merhaba düğmesi toohighlight hello gerekli modu kullanın.</span><span class="sxs-lookup"><span data-stu-id="09e30-250">Use hello Mode button toohighlight hello required mode.</span></span> <span data-ttu-id="09e30-251">2.</span><span class="sxs-lookup"><span data-stu-id="09e30-251">2.</span></span> <span data-ttu-id="09e30-252">Birkaç saniye içinde hello Temizle düğmesini basılı birkaç saniye için.</span><span class="sxs-lookup"><span data-stu-id="09e30-252">Within a few seconds, press and hold hello Clear button for a couple of seconds.</span></span> <span data-ttu-id="09e30-253">Başlangıç modu değişirse, yeni modun yanıp LED durur ve Aydınlatma kalır hello.</span><span class="sxs-lookup"><span data-stu-id="09e30-253">If hello mode changes, hello new mode’s LED stops flashing and remains lit.</span></span> <span data-ttu-id="09e30-254">Merhaba durum LED birkaç saniye düzensiz flash ve düzenli olarak hello cihaz hazır olduğunda sonra yanıp sönen.</span><span class="sxs-lookup"><span data-stu-id="09e30-254">hello Status LED might flash irregularly for a few seconds and then flashes regularly when hello device is ready.</span></span> <span data-ttu-id="09e30-255">Aksi takdirde'hello geçerli modunda hello uygun modu ışığı hello aygıt kalır aydınlatma.</span><span class="sxs-lookup"><span data-stu-id="09e30-255">Otherwise, hello device remains in hello current mode, with hello appropriate mode LED lit.</span></span>

### <a name="step-32-create-a-security-world"></a><span data-ttu-id="09e30-256">3.2. adım: güvenlik Dünyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="09e30-256">Step 3.2: Create a security world</span></span>
<span data-ttu-id="09e30-257">Bir komut istemi başlatın ve hello Thales yeni dünya programını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="09e30-257">Start a command prompt and run hello Thales new-world program.</span></span>

    new-world.exe --initialize --cipher-suite=DLf1024s160mRijndael --module=1 --acs-quorum=2/3

<span data-ttu-id="09e30-258">Bu programın oluşturduğu bir **güvenlik Dünyası** % toohello C:\ProgramData\nCipher\Key Management Data\local klasörüne karşılık gelen NFAST_KMDATA%\local\world dosyası.</span><span class="sxs-lookup"><span data-stu-id="09e30-258">This program creates a **Security World** file at %NFAST_KMDATA%\local\world, which corresponds toohello C:\ProgramData\nCipher\Key Management Data\local folder.</span></span> <span data-ttu-id="09e30-259">Merhaba çekirdek için farklı değerler kullanabilirsiniz, ancak Bizim örneğimizde, istendiğinde tooenter üç adet boş kart ve her biri için PIN olduğunuz.</span><span class="sxs-lookup"><span data-stu-id="09e30-259">You can use different values for hello quorum but in our example, you’re prompted tooenter three blank cards and pins for each one.</span></span> <span data-ttu-id="09e30-260">Ardından, herhangi iki kart tam erişim toohello güvenlik Dünyası verin.</span><span class="sxs-lookup"><span data-stu-id="09e30-260">Then, any two cards give full access toohello security world.</span></span> <span data-ttu-id="09e30-261">Bu kartlar hello hale **yönetici kart Seti** hello yeni güvenlik Dünyası için.</span><span class="sxs-lookup"><span data-stu-id="09e30-261">These cards become hello **Administrator Card Set** for hello new security world.</span></span>

<span data-ttu-id="09e30-262">Ardından aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="09e30-262">Then do hello following:</span></span>

* <span data-ttu-id="09e30-263">Merhaba Dünya dosyasının yedeğini alın.</span><span class="sxs-lookup"><span data-stu-id="09e30-263">Back up hello world file.</span></span> <span data-ttu-id="09e30-264">Güvenli ve Merhaba Dünya dosyasını, hello yönetici kartlarını ve bunların PIN'lerini korumak ve tek bir kişinin erişim toomore bir kart daha olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="09e30-264">Secure and protect hello world file, hello Administrator Cards, and their pins, and make sure that no single person has access toomore than one card.</span></span>

### <a name="step-33-change-hello-hsm-mode-tooo"></a><span data-ttu-id="09e30-265">3.3. adım: hello HSM modu too'O değiştirmek '</span><span class="sxs-lookup"><span data-stu-id="09e30-265">Step 3.3: Change hello HSM mode too'O'</span></span>
<span data-ttu-id="09e30-266">Thales nShield kenar, toochange hello modu kullanıyorsanız: 1.</span><span class="sxs-lookup"><span data-stu-id="09e30-266">If you are using Thales nShield Edge, toochange hello mode: 1.</span></span> <span data-ttu-id="09e30-267">Merhaba düğmesi toohighlight hello gerekli modu kullanın.</span><span class="sxs-lookup"><span data-stu-id="09e30-267">Use hello Mode button toohighlight hello required mode.</span></span> <span data-ttu-id="09e30-268">2.</span><span class="sxs-lookup"><span data-stu-id="09e30-268">2.</span></span> <span data-ttu-id="09e30-269">Birkaç saniye içinde hello Temizle düğmesini basılı birkaç saniye için.</span><span class="sxs-lookup"><span data-stu-id="09e30-269">Within a few seconds, press and hold hello Clear button for a couple of seconds.</span></span> <span data-ttu-id="09e30-270">Başlangıç modu değişirse, yeni modun yanıp LED durur ve Aydınlatma kalır hello.</span><span class="sxs-lookup"><span data-stu-id="09e30-270">If hello mode changes, hello new mode’s LED stops flashing and remains lit.</span></span> <span data-ttu-id="09e30-271">Merhaba durum LED birkaç saniye düzensiz flash ve düzenli olarak hello cihaz hazır olduğunda sonra yanıp sönen.</span><span class="sxs-lookup"><span data-stu-id="09e30-271">hello Status LED might flash irregularly for a few seconds and then flashes regularly when hello device is ready.</span></span> <span data-ttu-id="09e30-272">Aksi takdirde'hello geçerli modunda hello uygun modu ışığı hello aygıt kalır aydınlatma.</span><span class="sxs-lookup"><span data-stu-id="09e30-272">Otherwise, hello device remains in hello current mode, with hello appropriate mode LED lit.</span></span>


### <a name="step-34-validate-hello-downloaded-package"></a><span data-ttu-id="09e30-273">3.4. adım: hello indirilen paketi doğrulama</span><span class="sxs-lookup"><span data-stu-id="09e30-273">Step 3.4: Validate hello downloaded package</span></span>
<span data-ttu-id="09e30-274">Bu adım isteğe bağlıdır hello aşağıdaki doğrulayabilmesi ancak önerilir:</span><span class="sxs-lookup"><span data-stu-id="09e30-274">This step is optional but recommended so that you can validate hello following:</span></span>

* <span data-ttu-id="09e30-275">Merhaba hello araç takımında yer alan anahtar değişim anahtarı, orijinal bir Thales HSM'den oluşturulmuştur.</span><span class="sxs-lookup"><span data-stu-id="09e30-275">hello Key Exchange Key that is included in hello toolset has been generated from a genuine Thales HSM.</span></span>
* <span data-ttu-id="09e30-276">hello hello araç takımında yer alan güvenlik World Hello karmasını orijinal bir Thales HSM'de oluşturulmuştur.</span><span class="sxs-lookup"><span data-stu-id="09e30-276">hello hash of hello Security World that is included in hello toolset has been generated in a genuine Thales HSM.</span></span>
* <span data-ttu-id="09e30-277">Merhaba anahtar değişim anahtarı aktarılamaz.</span><span class="sxs-lookup"><span data-stu-id="09e30-277">hello Key Exchange Key is non-exportable.</span></span>

> [!NOTE]
> <span data-ttu-id="09e30-278">Paket toovalidate hello indirilen, hello HSM bağlı olması gerekir, açık ve üzerindeki güvenlik Dünyası (örneğin, hello bir yeni oluşturduğunuz) olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="09e30-278">toovalidate hello downloaded package, hello HSM must be connected, powered on, and must have a security world on it (such as hello one you’ve just created).</span></span>
>
>

<span data-ttu-id="09e30-279">toovalidate hello indirilen paketi:</span><span class="sxs-lookup"><span data-stu-id="09e30-279">toovalidate hello downloaded package:</span></span>

1. <span data-ttu-id="09e30-280">Coğrafi bölge veya Azure örneği bağlı olarak hello aşağıdakilerden birini yazarak Hello verifykeypackage.py betiği çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="09e30-280">Run hello verifykeypackage.py script by typing one of hello following, depending on your geographic region or instance of Azure:</span></span>

   * <span data-ttu-id="09e30-281">Kuzey Amerika için:</span><span class="sxs-lookup"><span data-stu-id="09e30-281">For North America:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-NA-1 -w BYOK-SecurityWorld-pkg-NA-1
   * <span data-ttu-id="09e30-282">Avrupa için:</span><span class="sxs-lookup"><span data-stu-id="09e30-282">For Europe:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-EU-1 -w BYOK-SecurityWorld-pkg-EU-1
   * <span data-ttu-id="09e30-283">Asya için:</span><span class="sxs-lookup"><span data-stu-id="09e30-283">For Asia:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-AP-1 -w BYOK-SecurityWorld-pkg-AP-1
   * <span data-ttu-id="09e30-284">Latin Amerika için:</span><span class="sxs-lookup"><span data-stu-id="09e30-284">For Latin America:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-LATAM-1 -w BYOK-SecurityWorld-pkg-LATAM-1
   * <span data-ttu-id="09e30-285">Japonya için:</span><span class="sxs-lookup"><span data-stu-id="09e30-285">For Japan:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-JPN-1 -w BYOK-SecurityWorld-pkg-JPN-1
   * <span data-ttu-id="09e30-286">Kore için:</span><span class="sxs-lookup"><span data-stu-id="09e30-286">For Korea:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-KOREA-1 -w BYOK-SecurityWorld-pkg-KOREA-1
   * <span data-ttu-id="09e30-287">Avustralya için:</span><span class="sxs-lookup"><span data-stu-id="09e30-287">For Australia:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-AUS-1 -w BYOK-SecurityWorld-pkg-AUS-1
   * <span data-ttu-id="09e30-288">İçin [Azure kamu](https://azure.microsoft.com/features/gov/), Azure hello ABD hükümeti örneğini kullanır:</span><span class="sxs-lookup"><span data-stu-id="09e30-288">For [Azure Government](https://azure.microsoft.com/features/gov/), which uses hello US government instance of Azure:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-USGOV-1 -w BYOK-SecurityWorld-pkg-USGOV-1
   * <span data-ttu-id="09e30-289">ABD hükümeti savunma Bakanlığı için:</span><span class="sxs-lookup"><span data-stu-id="09e30-289">For US Government DOD:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-USDOD-1 -w BYOK-SecurityWorld-pkg-USDOD-1
   * <span data-ttu-id="09e30-290">Kanada için:</span><span class="sxs-lookup"><span data-stu-id="09e30-290">For Canada:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-CANADA-1 -w BYOK-SecurityWorld-pkg-CANADA-1
   * <span data-ttu-id="09e30-291">Almanya için:</span><span class="sxs-lookup"><span data-stu-id="09e30-291">For Germany:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-GERMANY-1 -w BYOK-SecurityWorld-pkg-GERMANY-1
   * <span data-ttu-id="09e30-292">Hindistan için:</span><span class="sxs-lookup"><span data-stu-id="09e30-292">For India:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-INDIA-1 -w BYOK-SecurityWorld-pkg-INDIA-1
     > [!TIP]
     > <span data-ttu-id="09e30-293">Hello Thales yazılımı, %NFAST_HOME%\python\bin python içerir</span><span class="sxs-lookup"><span data-stu-id="09e30-293">hello Thales software includes python at %NFAST_HOME%\python\bin</span></span>
     >
     >
2. <span data-ttu-id="09e30-294">Doğrulama başarılı gösterir hello aşağıdaki gördüğünüzü onaylayın: **Result: SUCCESS**</span><span class="sxs-lookup"><span data-stu-id="09e30-294">Confirm that you see hello following, which indicates successful validation: **Result: SUCCESS**</span></span>

<span data-ttu-id="09e30-295">Bu komut dosyası toohello Thales kök anahtarına yukarı hello imzalayan zincirini doğrular.</span><span class="sxs-lookup"><span data-stu-id="09e30-295">This script validates hello signer chain up toohello Thales root key.</span></span> <span data-ttu-id="09e30-296">Bu kök anahtarın Hello karma hello komut dosyasında katıştırılmış ve değeri **59178a47 de508c3f 291277ee 184f46c4 f1d9c639**.</span><span class="sxs-lookup"><span data-stu-id="09e30-296">hello hash of this root key is embedded in hello script and its value should be **59178a47 de508c3f 291277ee 184f46c4 f1d9c639**.</span></span> <span data-ttu-id="09e30-297">Ayrıca bu değeri ayrı ayrı hello ziyaret ederek doğrulayabilirsiniz [Thales Web sitesini](http://www.thalesesec.com/).</span><span class="sxs-lookup"><span data-stu-id="09e30-297">You can also confirm this value separately by visiting hello [Thales website](http://www.thalesesec.com/).</span></span>

<span data-ttu-id="09e30-298">Şimdi hazır toocreate yeni bir anahtar olduğunuz.</span><span class="sxs-lookup"><span data-stu-id="09e30-298">You’re now ready toocreate a new key.</span></span>

### <a name="step-35-create-a-new-key"></a><span data-ttu-id="09e30-299">3.5. adım: yeni bir anahtar oluşturun</span><span class="sxs-lookup"><span data-stu-id="09e30-299">Step 3.5: Create a new key</span></span>
<span data-ttu-id="09e30-300">Merhaba Thales kullanarak bir anahtar oluşturmak **generatekey** program.</span><span class="sxs-lookup"><span data-stu-id="09e30-300">Generate a key by using hello Thales **generatekey** program.</span></span>

<span data-ttu-id="09e30-301">Komut toogenerate hello anahtar aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="09e30-301">Run hello following command toogenerate hello key:</span></span>

    generatekey --generate simple type=RSA size=2048 protect=module ident=contosokey plainname=contosokey nvram=no pubexp=

<span data-ttu-id="09e30-302">Bu komutu çalıştırdığınızda, aşağıdaki yönergeleri kullanın:</span><span class="sxs-lookup"><span data-stu-id="09e30-302">When you run this command, use these instructions:</span></span>

* <span data-ttu-id="09e30-303">parametre hello *korumak* toohello değerinin ayarlanması gereken **Modülü**gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="09e30-303">hello parameter *protect* must be set toohello value **module**, as shown.</span></span> <span data-ttu-id="09e30-304">Bu, modül korumalı bir anahtar oluşturur.</span><span class="sxs-lookup"><span data-stu-id="09e30-304">This creates a module-protected key.</span></span> <span data-ttu-id="09e30-305">Merhaba BYOK araç takımı, OCS korumalı anahtarları desteklemez.</span><span class="sxs-lookup"><span data-stu-id="09e30-305">hello BYOK toolset does not support OCS-protected keys.</span></span>
* <span data-ttu-id="09e30-306">Merhaba değerini *contosokey* hello için **plainname** ve **contosokey** herhangi bir dize değeri ile.</span><span class="sxs-lookup"><span data-stu-id="09e30-306">Replace hello value of *contosokey* for hello **ident** and **plainname** with any string value.</span></span> <span data-ttu-id="09e30-307">toominimize yönetim ek yüklerini ve hello riskini azaltmak aynı değeri her ikisi için hello kullanmanızı tavsiye ederiz hatalarının,.</span><span class="sxs-lookup"><span data-stu-id="09e30-307">toominimize administrative overheads and reduce hello risk of errors, we recommend that you use hello same value for both.</span></span> <span data-ttu-id="09e30-308">Merhaba **plainname** değeri yalnızca sayı, tire ve küçük harf içermelidir.</span><span class="sxs-lookup"><span data-stu-id="09e30-308">hello **ident** value must contain only numbers, dashes, and lower case letters.</span></span>
* <span data-ttu-id="09e30-309">Bu örnekte Hello pubexp (varsayılan) boş bırakılır, ancak özel değerler belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="09e30-309">hello pubexp is left blank (default) in this example, but you can specify specific values.</span></span> <span data-ttu-id="09e30-310">Daha fazla bilgi için Thales belgelerine hello.</span><span class="sxs-lookup"><span data-stu-id="09e30-310">For more information, see hello Thales documentation.</span></span>

<span data-ttu-id="09e30-311">Bu komut, %NFAST_KMDATA%\local klasörünüzde adı ile bir simgeleştirilmiş anahtar dosyası oluşturur **key_simple_**hello ardından **plainname** hello komutta belirtildi.</span><span class="sxs-lookup"><span data-stu-id="09e30-311">This command creates a Tokenized Key file in your %NFAST_KMDATA%\local folder with a name starting with **key_simple_**, followed by hello **ident** that was specified in hello command.</span></span> <span data-ttu-id="09e30-312">Örneğin: **key_simple_contosokey**.</span><span class="sxs-lookup"><span data-stu-id="09e30-312">For example: **key_simple_contosokey**.</span></span> <span data-ttu-id="09e30-313">Bu dosya şifreli bir anahtar içerir.</span><span class="sxs-lookup"><span data-stu-id="09e30-313">This file contains an encrypted key.</span></span>

<span data-ttu-id="09e30-314">Bu simgeleştirilmiş anahtar dosyasını güvenli bir konuma yedekleyin.</span><span class="sxs-lookup"><span data-stu-id="09e30-314">Back up this Tokenized Key File in a safe location.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="09e30-315">Daha sonra anahtar tooAzure anahtar kasası aktardığınızda, Microsoft, anahtar ve güvenlik dünyanızı güvenli biçimde yedeklemeniz son derece önemli olacak şekilde bu anahtar geri tooyou dışarı aktaramazsınız.</span><span class="sxs-lookup"><span data-stu-id="09e30-315">When you later transfer your key tooAzure Key Vault, Microsoft cannot export this key back tooyou so it becomes extremely important that you back up your key and security world safely.</span></span> <span data-ttu-id="09e30-316">Kılavuzu ve anahtarınızı yedekleme için en iyi uygulamalar için Thales başvurun.</span><span class="sxs-lookup"><span data-stu-id="09e30-316">Contact Thales for guidance and best practices for backing up your key.</span></span>
>
>

<span data-ttu-id="09e30-317">Artık hazır tootransfer, anahtar tooAzure anahtar kasası şunlardır.</span><span class="sxs-lookup"><span data-stu-id="09e30-317">You are now ready tootransfer your key tooAzure Key Vault.</span></span>

## <a name="step-4-prepare-your-key-for-transfer"></a><span data-ttu-id="09e30-318">4. adım: anahtarınızı aktarım için hazırlama</span><span class="sxs-lookup"><span data-stu-id="09e30-318">Step 4: Prepare your key for transfer</span></span>
<span data-ttu-id="09e30-319">Dördüncü Bu adım için aşağıdaki hello bağlantısı kesilmiş iş istasyonunda yordamlarını hello.</span><span class="sxs-lookup"><span data-stu-id="09e30-319">For this fourth step, do hello following procedures on hello disconnected workstation.</span></span>

### <a name="step-41-create-a-copy-of-your-key-with-reduced-permissions"></a><span data-ttu-id="09e30-320">4.1. adım: sınırlı izinlerle anahtarınızın bir kopyasını oluşturma</span><span class="sxs-lookup"><span data-stu-id="09e30-320">Step 4.1: Create a copy of your key with reduced permissions</span></span>

<span data-ttu-id="09e30-321">Yeni bir komut istemi açın ve burada, hello BYOK ZIP dosyasının sıkıştırması açılmış hello geçerli dizin toohello konumunu değiştirin.</span><span class="sxs-lookup"><span data-stu-id="09e30-321">Open a new command prompt and change hello current directory toohello location where you unzipped hello BYOK zip file.</span></span> <span data-ttu-id="09e30-322">bir komut isteminden anahtarınızı tooreduce hello izinleri coğrafi bölge veya Azure örneği bağlı olarak hello aşağıdakilerden birini çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="09e30-322">tooreduce hello permissions on your key, from a command prompt, run one of hello following, depending on your geographic region or instance of Azure:</span></span>

* <span data-ttu-id="09e30-323">Kuzey Amerika için:</span><span class="sxs-lookup"><span data-stu-id="09e30-323">For North America:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1
* <span data-ttu-id="09e30-324">Avrupa için:</span><span class="sxs-lookup"><span data-stu-id="09e30-324">For Europe:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1
* <span data-ttu-id="09e30-325">Asya için:</span><span class="sxs-lookup"><span data-stu-id="09e30-325">For Asia:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1
* <span data-ttu-id="09e30-326">Latin Amerika için:</span><span class="sxs-lookup"><span data-stu-id="09e30-326">For Latin America:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-LATAM-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-LATAM-1
* <span data-ttu-id="09e30-327">Japonya için:</span><span class="sxs-lookup"><span data-stu-id="09e30-327">For Japan:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-JPN-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-JPN-1
* <span data-ttu-id="09e30-328">Kore için:</span><span class="sxs-lookup"><span data-stu-id="09e30-328">For Korea:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-KOREA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-KOREA-1
* <span data-ttu-id="09e30-329">Avustralya için:</span><span class="sxs-lookup"><span data-stu-id="09e30-329">For Australia:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AUS-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AUS-1
* <span data-ttu-id="09e30-330">İçin [Azure kamu](https://azure.microsoft.com/features/gov/), Azure hello ABD hükümeti örneğini kullanır:</span><span class="sxs-lookup"><span data-stu-id="09e30-330">For [Azure Government](https://azure.microsoft.com/features/gov/), which uses hello US government instance of Azure:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USGOV-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USGOV-1
* <span data-ttu-id="09e30-331">ABD hükümeti savunma Bakanlığı için:</span><span class="sxs-lookup"><span data-stu-id="09e30-331">For US Government DOD:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USDOD-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USDOD-1
* <span data-ttu-id="09e30-332">Kanada için:</span><span class="sxs-lookup"><span data-stu-id="09e30-332">For Canada:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-CANADA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-CANADA-1
* <span data-ttu-id="09e30-333">Almanya için:</span><span class="sxs-lookup"><span data-stu-id="09e30-333">For Germany:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-GERMANY-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-GERMANY-1
* <span data-ttu-id="09e30-334">Hindistan için:</span><span class="sxs-lookup"><span data-stu-id="09e30-334">For India:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-INDIA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-INDIA-1

<span data-ttu-id="09e30-335">Bu komutu çalıştırdığınızda, yerini *contosokey* hello ile aynı belirtilen değere **adım 3.5: yeni bir anahtar oluşturun** hello gelen [anahtarınızı](#step-3-generate-your-key) adım.</span><span class="sxs-lookup"><span data-stu-id="09e30-335">When you run this command, replace *contosokey* with hello same value you specified in **Step 3.5: Create a new key** from hello [Generate your key](#step-3-generate-your-key) step.</span></span>

<span data-ttu-id="09e30-336">Güvenlik Dünyası yönetim kartlarınızı tooplug istenir.</span><span class="sxs-lookup"><span data-stu-id="09e30-336">You are asked tooplug in your security world admin cards.</span></span>

<span data-ttu-id="09e30-337">Merhaba komutu tamamlandığında, gördüğünüz **sonucu: başarı** ve hello anahtarınızın sınırlı izinlere sahip kopyası, key_xferacıd_ adlı hello dosyasında olan<contosokey>.</span><span class="sxs-lookup"><span data-stu-id="09e30-337">When hello command completes, you see **Result: SUCCESS** and hello copy of your key with reduced permissions are in hello file named key_xferacId_<contosokey>.</span></span>

<span data-ttu-id="09e30-338">Merhaba ACL'ler inceler hello Thales yardımcı programlarını komutları kullanarak kullanarak:</span><span class="sxs-lookup"><span data-stu-id="09e30-338">You may inspects hello ACLS using following commands using hello Thales utilities:</span></span>

* <span data-ttu-id="09e30-339">aclprint.PY:</span><span class="sxs-lookup"><span data-stu-id="09e30-339">aclprint.py:</span></span>

        "%nfast_home%\bin\preload.exe" -m 1 -A xferacld -K contosokey "%nfast_home%\python\bin\python" "%nfast_home%\python\examples\aclprint.py"
* <span data-ttu-id="09e30-340">kmfile-dump.exe:</span><span class="sxs-lookup"><span data-stu-id="09e30-340">kmfile-dump.exe:</span></span>

        "%nfast_home%\bin\kmfile-dump.exe" "%NFAST_KMDATA%\local\key_xferacld_contosokey"
  <span data-ttu-id="09e30-341">Bu komutları çalıştırdığınızda, aynı değeri, belirtilen hello contosokey yerine **adım 3.5: yeni bir anahtar oluşturun** hello gelen [anahtarınızı](#step-3-generate-your-key) adım.</span><span class="sxs-lookup"><span data-stu-id="09e30-341">When you run these commands, replace contosokey with hello same value you specified in **Step 3.5: Create a new key** from hello [Generate your key](#step-3-generate-your-key) step.</span></span>

### <a name="step-42-encrypt-your-key-by-using-microsofts-key-exchange-key"></a><span data-ttu-id="09e30-342">4.2. adım: Microsoft'un anahtar değişim anahtarını kullanarak anahtarınızı şifreleme</span><span class="sxs-lookup"><span data-stu-id="09e30-342">Step 4.2: Encrypt your key by using Microsoft’s Key Exchange Key</span></span>
<span data-ttu-id="09e30-343">Komutları, coğrafi bölge veya Azure örneği bağlı olarak aşağıdaki hello birini çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="09e30-343">Run one of hello following commands, depending on your geographic region or instance of Azure:</span></span>

* <span data-ttu-id="09e30-344">Kuzey Amerika için:</span><span class="sxs-lookup"><span data-stu-id="09e30-344">For North America:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="09e30-345">Avrupa için:</span><span class="sxs-lookup"><span data-stu-id="09e30-345">For Europe:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="09e30-346">Asya için:</span><span class="sxs-lookup"><span data-stu-id="09e30-346">For Asia:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="09e30-347">Latin Amerika için:</span><span class="sxs-lookup"><span data-stu-id="09e30-347">For Latin America:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-LATAM-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-LATAM-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="09e30-348">Japonya için:</span><span class="sxs-lookup"><span data-stu-id="09e30-348">For Japan:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-JPN-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-JPN-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="09e30-349">Kore için:</span><span class="sxs-lookup"><span data-stu-id="09e30-349">For Korea:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-KOREA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-KOREA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="09e30-350">Avustralya için:</span><span class="sxs-lookup"><span data-stu-id="09e30-350">For Australia:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AUS-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AUS-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="09e30-351">İçin [Azure kamu](https://azure.microsoft.com/features/gov/), Azure hello ABD hükümeti örneğini kullanır:</span><span class="sxs-lookup"><span data-stu-id="09e30-351">For [Azure Government](https://azure.microsoft.com/features/gov/), which uses hello US government instance of Azure:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USGOV-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USGOV-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="09e30-352">ABD hükümeti savunma Bakanlığı için:</span><span class="sxs-lookup"><span data-stu-id="09e30-352">For US Government DOD:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USDOD-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USDOD-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="09e30-353">Kanada için:</span><span class="sxs-lookup"><span data-stu-id="09e30-353">For Canada:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-CANADA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-CANADA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="09e30-354">Almanya için:</span><span class="sxs-lookup"><span data-stu-id="09e30-354">For Germany:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-GERMANY-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-GERMANY-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="09e30-355">Hindistan için:</span><span class="sxs-lookup"><span data-stu-id="09e30-355">For India:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-INDIA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-INDIA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey

<span data-ttu-id="09e30-356">Bu komutu çalıştırdığınızda, aşağıdaki yönergeleri kullanın:</span><span class="sxs-lookup"><span data-stu-id="09e30-356">When you run this command, use these instructions:</span></span>

* <span data-ttu-id="09e30-357">Değiştir *contosokey* toogenerate hello anahtarında kullanılan hello tanımlayıcıyla **adım 3.5: yeni bir anahtar oluşturun** hello gelen [anahtarınızı](#step-3-generate-your-key) adım.</span><span class="sxs-lookup"><span data-stu-id="09e30-357">Replace *contosokey* with hello identifier that you used toogenerate hello key in **Step 3.5: Create a new key** from hello [Generate your key](#step-3-generate-your-key) step.</span></span>
* <span data-ttu-id="09e30-358">Değiştir *Subscriptionıd* hello anahtar kasanızı içeren Azure aboneliği hello kimliği.</span><span class="sxs-lookup"><span data-stu-id="09e30-358">Replace *SubscriptionID* with hello ID of hello Azure subscription that contains your key vault.</span></span> <span data-ttu-id="09e30-359">Bu değer alınan önceden, **adım 1.2: Azure abonelik Kimliğinizi alın** hello gelen [Internet'e bağlı iş istasyonunuzu hazırlama](#step-1-prepare-your-internet-connected-workstation) adım.</span><span class="sxs-lookup"><span data-stu-id="09e30-359">You retrieved this value previously, in **Step 1.2: Get your Azure subscription ID** from hello [Prepare your Internet-connected workstation](#step-1-prepare-your-internet-connected-workstation) step.</span></span>
* <span data-ttu-id="09e30-360">Değiştir *ContosoFirstHSMKey* , çıktı dosyanızın adı için kullanılan bir etikete sahip.</span><span class="sxs-lookup"><span data-stu-id="09e30-360">Replace *ContosoFirstHSMKey* with a label that is used for your output file name.</span></span>

<span data-ttu-id="09e30-361">Bu başarıyla tamamlandığında görüntüler **sonucu: başarı** ve yeni bir dosya adı aşağıdaki hello sahip hello geçerli klasörde: KeyTransferPackage -*ContosoFirstHSMkey*.byok</span><span class="sxs-lookup"><span data-stu-id="09e30-361">When this completes successfully, it displays **Result: SUCCESS** and there is a new file in hello current folder that has hello following name: KeyTransferPackage-*ContosoFirstHSMkey*.byok</span></span>

### <a name="step-43-copy-your-key-transfer-package-toohello-internet-connected-workstation"></a><span data-ttu-id="09e30-362">4.3. adım: anahtar aktarma paketini toohello Internet'e bağlı iş istasyonunuzu kopyalama</span><span class="sxs-lookup"><span data-stu-id="09e30-362">Step 4.3: Copy your key transfer package toohello Internet-connected workstation</span></span>
<span data-ttu-id="09e30-363">Bir USB sürücü veya diğer taşınabilir depolama toocopy hello çıktı dosyası hello önceki adım (KeyTransferPackage-ContosoFirstHSMkey.byok) tooyour Internet'e bağlı iş istasyonundan kullanın.</span><span class="sxs-lookup"><span data-stu-id="09e30-363">Use a USB drive or other portable storage toocopy hello output file from hello previous step (KeyTransferPackage-ContosoFirstHSMkey.byok) tooyour Internet-connected workstation.</span></span>

## <a name="step-5-transfer-your-key-tooazure-key-vault"></a><span data-ttu-id="09e30-364">5. adım: Aktarım, anahtar tooAzure anahtar kasası</span><span class="sxs-lookup"><span data-stu-id="09e30-364">Step 5: Transfer your key tooAzure Key Vault</span></span>
<span data-ttu-id="09e30-365">Bu son adım için hello Internet'e bağlı iş istasyonunda, hello kullan [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) hello kopyaladığınız cmdlet tooupload hello anahtar aktarma paketini bağlantısı kesilmiş iş istasyonu toohello Azure anahtar kasası HSM:</span><span class="sxs-lookup"><span data-stu-id="09e30-365">For this final step, on hello Internet-connected workstation, use hello [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) cmdlet tooupload hello key transfer package that you copied from hello disconnected workstation toohello Azure Key Vault HSM:</span></span>

    Add-AzureKeyVaultKey -VaultName 'ContosoKeyVaultHSM' -Name 'ContosoFirstHSMkey' -KeyFilePath 'c:\KeyTransferPackage-ContosoFirstHSMkey.byok' -Destination 'HSM'

<span data-ttu-id="09e30-366">Merhaba karşıya yükleme başarılı olursa, eklediğiniz hello anahtarının görüntülenen hello özelliklerine bakın.</span><span class="sxs-lookup"><span data-stu-id="09e30-366">If hello upload is successful, you see displayed hello properties of hello key that you just added.</span></span>

## <a name="next-steps"></a><span data-ttu-id="09e30-367">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="09e30-367">Next steps</span></span>
<span data-ttu-id="09e30-368">Bu gibi durumlarda, bu HSM korumalı anahtara artık anahtar kasanız kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="09e30-368">You can now use this HSM-protected key in your key vault.</span></span> <span data-ttu-id="09e30-369">Merhaba daha fazla bilgi için bkz: **toouse bir donanım güvenlik modülü (HSM) isteyip istemediğinizi** hello bölümünde [Azure anahtar kasası ile çalışmaya başlama](key-vault-get-started.md) Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="09e30-369">For more information, see hello **If you want toouse a hardware security module (HSM)** section in hello [Getting started with Azure Key Vault](key-vault-get-started.md) tutorial.</span></span>
