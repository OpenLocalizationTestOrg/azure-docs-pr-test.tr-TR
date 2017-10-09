---
title: "aaaConfigure SSL boşaltma - Azure uygulama ağ geçidi - Azure portalı | Microsoft Docs"
description: "Bu sayfa bir uygulama ağ geçidi ile SSL boşaltma hello portalını kullanarak yönergeleri toocreate sağlar"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 8373379a-a26a-45d2-aa62-dd282298eff3
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: e87ac0bbe10ac45e307c18802741c7bc31764a20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-hello-portal"></a><span data-ttu-id="e46ae-103">Merhaba portalını kullanarak SSL yük boşaltımı için bir uygulama ağ geçidi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="e46ae-103">Configure an application gateway for SSL offload by using hello portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e46ae-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="e46ae-104">Azure portal</span></span>](application-gateway-ssl-portal.md)
> * [<span data-ttu-id="e46ae-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="e46ae-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ssl-arm.md)
> * [<span data-ttu-id="e46ae-106">Azure Klasik PowerShell</span><span class="sxs-lookup"><span data-stu-id="e46ae-106">Azure Classic PowerShell</span></span>](application-gateway-ssl.md)
> * [<span data-ttu-id="e46ae-107">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="e46ae-107">Azure CLI 2.0</span></span>](application-gateway-ssl-cli.md)

<span data-ttu-id="e46ae-108">Azure uygulama ağ geçidi yapılandırılmış tooterminate hello Güvenli Yuva Katmanı (SSL) hello ağ geçidi tooavoid maliyetli SSL şifre çözme görevleri toohappen hello web grubu adresindeki oturumunda olabilir.</span><span class="sxs-lookup"><span data-stu-id="e46ae-108">Azure Application Gateway can be configured tooterminate hello Secure Sockets Layer (SSL) session at hello gateway tooavoid costly SSL decryption tasks toohappen at hello web farm.</span></span> <span data-ttu-id="e46ae-109">SSL boşaltma ayrıca hello ön uç sunucusunun kurulumunu ve hello web uygulamasının yönetimini basitleştirir.</span><span class="sxs-lookup"><span data-stu-id="e46ae-109">SSL offload also simplifies hello front-end server setup and management of hello web application.</span></span>

## <a name="scenario"></a><span data-ttu-id="e46ae-110">Senaryo</span><span class="sxs-lookup"><span data-stu-id="e46ae-110">Scenario</span></span>

<span data-ttu-id="e46ae-111">Senaryo aşağıdaki hello nasıl yapılandıracağınız SSL boşaltma üzerinde var olan bir uygulama ağ geçidi gider.</span><span class="sxs-lookup"><span data-stu-id="e46ae-111">hello following scenario goes through configuring SSL offload on an existing application gateway.</span></span> <span data-ttu-id="e46ae-112">Merhaba senaryo, zaten hello adımları çok izlediğinizden varsayar[bir uygulama ağ geçidi oluşturma](application-gateway-create-gateway-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e46ae-112">hello scenario assumes that you have already followed hello steps too[Create an Application Gateway](application-gateway-create-gateway-portal.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="e46ae-113">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="e46ae-113">Before you begin</span></span>

<span data-ttu-id="e46ae-114">tooconfigure SSL yük boşaltımı bir uygulama ağ geçidi ile bir sertifika gereklidir.</span><span class="sxs-lookup"><span data-stu-id="e46ae-114">tooconfigure SSL offload with an application gateway, a certificate is required.</span></span> <span data-ttu-id="e46ae-115">Bu sertifika tooencrypt kullanılan hello uygulama ağ geçidinde yüklenir ve SSL gönderilen hello trafiğin şifresi.</span><span class="sxs-lookup"><span data-stu-id="e46ae-115">This certificate is loaded on hello application gateway and used tooencrypt and decrypt hello traffic sent via SSL.</span></span> <span data-ttu-id="e46ae-116">Merhaba sertifika toobe kişisel bilgi değişimi (pfx) biçiminde olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="e46ae-116">hello certificate needs toobe in Personal Information Exchange (pfx) format.</span></span> <span data-ttu-id="e46ae-117">Bu dosya biçimi, hangi hello uygulama ağ geçidi tooperform hello şifreleme ve şifre çözme trafik tarafından gerekli anahtar toobe dışarı Merhaba özel sağlar.</span><span class="sxs-lookup"><span data-stu-id="e46ae-117">This file format allows for hello private key toobe exported which is required by hello application gateway tooperform hello encryption and decryption of traffic.</span></span>

## <a name="add-an-https-listener"></a><span data-ttu-id="e46ae-118">Bir HTTPS dinleyicisi ekleme</span><span class="sxs-lookup"><span data-stu-id="e46ae-118">Add an HTTPS listener</span></span>

<span data-ttu-id="e46ae-119">Merhaba HTTPS dinleyicisi kendi yapılandırmasını temel alarak trafiği arar ve rota hello trafiği toohello arka uç havuzları yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="e46ae-119">hello HTTPS listener looks for traffic based on its configuration and helps route hello traffic toohello backend pools.</span></span>

### <a name="step-1"></a><span data-ttu-id="e46ae-120">1. Adım</span><span class="sxs-lookup"><span data-stu-id="e46ae-120">Step 1</span></span>

<span data-ttu-id="e46ae-121">Toohello Azure portalına gidin ve var olan bir uygulama ağ geçidi seçin</span><span class="sxs-lookup"><span data-stu-id="e46ae-121">Navigate toohello Azure portal and select an existing application gateway</span></span>

### <a name="step-2"></a><span data-ttu-id="e46ae-122">2. Adım</span><span class="sxs-lookup"><span data-stu-id="e46ae-122">Step 2</span></span>

<span data-ttu-id="e46ae-123">Dinleyicileri ve hello Ekle düğmesi tooadd dinleyici tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e46ae-123">Click Listeners and click hello Add button tooadd a listener.</span></span>

![Uygulama ağ geçidi'ne genel bakış dikey][1]

### <a name="step-3"></a><span data-ttu-id="e46ae-125">3. Adım</span><span class="sxs-lookup"><span data-stu-id="e46ae-125">Step 3</span></span>

<span data-ttu-id="e46ae-126">Merhaba dinleyici için gereken bilgileri hello ve karşıya yükleme hello .pfx sertifika, tamamlandığında, Tamam'ı tıklatın doldurun.</span><span class="sxs-lookup"><span data-stu-id="e46ae-126">Fill out hello required information for hello listener and upload hello .pfx certificate, when complete click OK.</span></span>

<span data-ttu-id="e46ae-127">**Ad** -bu değer hello dinleyicisi kolay adıdır.</span><span class="sxs-lookup"><span data-stu-id="e46ae-127">**Name** - This value is a friendly name of hello listener.</span></span>

<span data-ttu-id="e46ae-128">**Ön uç IP yapılandırmasını** -hello dinleyici için kullanılan hello ön uç IP yapılandırması bu değerdir.</span><span class="sxs-lookup"><span data-stu-id="e46ae-128">**Frontend IP configuration** - This value is hello frontend IP configuration that is used for hello listener.</span></span>

<span data-ttu-id="e46ae-129">**Ön uç bağlantı noktası (ad/bağlantı noktası)** -hello ön ucunda hello uygulama ağ geçidi ve kullanılan hello gerçek bağlantı noktası kullanılan başlangıç bağlantı noktası için bir kolay ad.</span><span class="sxs-lookup"><span data-stu-id="e46ae-129">**Frontend port (Name/Port)** - A friendly name for hello port used on hello front end of hello application gateway and hello actual port used.</span></span>

<span data-ttu-id="e46ae-130">**Protokol** -hello ön uç için https veya http kullanılıyorsa bir anahtar toodetermine.</span><span class="sxs-lookup"><span data-stu-id="e46ae-130">**Protocol** - A switch toodetermine if https or http is used for hello front end.</span></span>

<span data-ttu-id="e46ae-131">**Sertifika (ad/parola)** - varsa SSL boşaltma kullanılır, bu ayar için bir .pfx sertifika gereklidir ve bir kolay ad ve parola gereklidir.</span><span class="sxs-lookup"><span data-stu-id="e46ae-131">**Certificate (Name/Password)** - If SSL offload is used, a .pfx certificate is required for this setting and a friendly name and password are required.</span></span>

![Dinleyici dikey ekleme][2]

## <a name="create-a-rule-and-associate-it-toohello-listener"></a><span data-ttu-id="e46ae-133">Bir kural oluşturmak ve toohello dinleyicisi ilişkilendirme</span><span class="sxs-lookup"><span data-stu-id="e46ae-133">Create a rule and associate it toohello listener</span></span>

<span data-ttu-id="e46ae-134">Merhaba dinleyicisi şimdi oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="e46ae-134">hello listener has now been created.</span></span> <span data-ttu-id="e46ae-135">Zaman toocreate hello dinleyicisi kural toohandle hello trafiğinden olur.</span><span class="sxs-lookup"><span data-stu-id="e46ae-135">It is time toocreate a rule toohandle hello traffic from hello listener.</span></span> <span data-ttu-id="e46ae-136">Kuralları nasıl trafiği birden çok oturum tanımlama bilgisi temelli benzeşimi kullanılıp kullanılmadığını dahil olmak üzere, yapılandırma ayarlarını, protokol, bağlantı noktası ve sistem durumu araştırmalarının göre yönlendirilmiş toohello arka uç havuzları tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="e46ae-136">Rules define how traffic is routed toohello backend pools based on multiple configuration settings, including whether cookie-based session affinity is used, protocol, port, and health probes.</span></span>

### <a name="step-1"></a><span data-ttu-id="e46ae-137">1. Adım</span><span class="sxs-lookup"><span data-stu-id="e46ae-137">Step 1</span></span>

<span data-ttu-id="e46ae-138">Merhaba tıklatın **kuralları** hello uygulama ağ geçidi ve ardından Ekle'yi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="e46ae-138">Click hello **Rules** of hello application gateway, and then click Add.</span></span>

![Uygulama ağ geçidi kuralları dikey][3]

### <a name="step-2"></a><span data-ttu-id="e46ae-140">2. Adım</span><span class="sxs-lookup"><span data-stu-id="e46ae-140">Step 2</span></span>

<span data-ttu-id="e46ae-141">Merhaba üzerinde **Ekle temel kural** dikey penceresinde hello hello kuralı için kolay ad yazın ve hello önceki adımda oluşturduğunuz hello dinleyicisi seçin.</span><span class="sxs-lookup"><span data-stu-id="e46ae-141">On hello **Add basic rule** blade, type in hello friendly name for hello rule and choose hello listener created in hello previous step.</span></span> <span data-ttu-id="e46ae-142">Hello uygun arka uç havuzu ve http ayarını seçin ve tıklatın **Tamam**</span><span class="sxs-lookup"><span data-stu-id="e46ae-142">Choose hello appropriate backend pool and http setting and click **OK**</span></span>

![HTTPS Ayarları penceresi][4]

<span data-ttu-id="e46ae-144">Hello ayarları şimdi toohello uygulama ağ geçidi kaydedildi.</span><span class="sxs-lookup"><span data-stu-id="e46ae-144">hello settings are now saved toohello application gateway.</span></span> <span data-ttu-id="e46ae-145">Merhaba portal veya PowerShell aracılığıyla kullanılabilir tooview önce hello Kaydet işlemi bu ayarlar için biraz zaman alabilir.</span><span class="sxs-lookup"><span data-stu-id="e46ae-145">hello save process for these settings may take a while before they are available tooview through hello portal or through PowerShell.</span></span> <span data-ttu-id="e46ae-146">Bir kez kaydedilmiş hello uygulama ağ geçidi hello şifreleme ve şifre çözme trafiği işler.</span><span class="sxs-lookup"><span data-stu-id="e46ae-146">Once saved hello application gateway handles hello encryption and decryption of traffic.</span></span> <span data-ttu-id="e46ae-147">Merhaba uygulama ağ geçidi ile Merhaba arka uç web sunucuları arasındaki tüm trafik http üzerinden ele alınacaktır.</span><span class="sxs-lookup"><span data-stu-id="e46ae-147">All traffic between hello application gateway and hello backend web servers will be handled over http.</span></span> <span data-ttu-id="e46ae-148">HTTPS üzerinden başlattıysanız tüm iletişimi geri toohello istemci şifrelenmiş toohello istemci döndürülür.</span><span class="sxs-lookup"><span data-stu-id="e46ae-148">Any communication back toohello client if initiated over https will be returned toohello client encrypted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e46ae-149">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e46ae-149">Next steps</span></span>

<span data-ttu-id="e46ae-150">Azure uygulama ağ geçidi ile tooconfigure özel durumu araştırma nasıl toolearn bkz [bir özel durum araştırması oluşturmak](application-gateway-create-gateway-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e46ae-150">toolearn how tooconfigure a custom health probe with Azure Application Gateway, see [Create a custom health probe](application-gateway-create-gateway-portal.md).</span></span>

[1]: ./media/application-gateway-ssl-portal/figure1.png
[2]: ./media/application-gateway-ssl-portal/figure2.png
[3]: ./media/application-gateway-ssl-portal/figure3.png
[4]: ./media/application-gateway-ssl-portal/figure4.png
