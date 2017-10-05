---
title: "Azure uygulama ağ geçidi - Azure portalı SSL boşaltma - yapılandırma | Microsoft Docs"
description: "Bu sayfa, portal kullanarak SSL ile bir uygulama ağ geçidi oluşturma yönergelerini boşaltma sağlar."
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
ms.openlocfilehash: f61be0cc4c9274c9914f7c468ce48a2a3d0a4f4a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-the-portal"></a><span data-ttu-id="417a3-103">Portalı kullanarak SSL yük boşaltımı için bir uygulama ağ geçidi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="417a3-103">Configure an application gateway for SSL offload by using the portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="417a3-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="417a3-104">Azure portal</span></span>](application-gateway-ssl-portal.md)
> * [<span data-ttu-id="417a3-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="417a3-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ssl-arm.md)
> * [<span data-ttu-id="417a3-106">Azure Klasik PowerShell</span><span class="sxs-lookup"><span data-stu-id="417a3-106">Azure Classic PowerShell</span></span>](application-gateway-ssl.md)
> * [<span data-ttu-id="417a3-107">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="417a3-107">Azure CLI 2.0</span></span>](application-gateway-ssl-cli.md)

<span data-ttu-id="417a3-108">Azure Application Gateway, web grubunda maliyetli SSL şifre çözme görevlerinin oluşmasından kaçınmak için Güvenli Yuva Katmanı (SSL) oturumunu sonlandırmak amacıyla yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="417a3-108">Azure Application Gateway can be configured to terminate the Secure Sockets Layer (SSL) session at the gateway to avoid costly SSL decryption tasks to happen at the web farm.</span></span> <span data-ttu-id="417a3-109">SSL yük boşaltımı ön uç sunucusunun kurulumunu ve web uygulamasının yönetimini de basitleştirir.</span><span class="sxs-lookup"><span data-stu-id="417a3-109">SSL offload also simplifies the front-end server setup and management of the web application.</span></span>

## <a name="scenario"></a><span data-ttu-id="417a3-110">Senaryo</span><span class="sxs-lookup"><span data-stu-id="417a3-110">Scenario</span></span>

<span data-ttu-id="417a3-111">Aşağıdaki senaryoda nasıl yapılandıracağınız SSL boşaltma üzerinde var olan bir uygulama ağ geçidi gider.</span><span class="sxs-lookup"><span data-stu-id="417a3-111">The following scenario goes through configuring SSL offload on an existing application gateway.</span></span> <span data-ttu-id="417a3-112">Senaryo adımları zaten izlediğinizden varsayar [bir uygulama ağ geçidi oluşturma](application-gateway-create-gateway-portal.md).</span><span class="sxs-lookup"><span data-stu-id="417a3-112">The scenario assumes that you have already followed the steps to [Create an Application Gateway](application-gateway-create-gateway-portal.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="417a3-113">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="417a3-113">Before you begin</span></span>

<span data-ttu-id="417a3-114">Bir uygulama ağ geçidi ile SSL yük boşaltmayı yapılandırmak için bir sertifika gereklidir.</span><span class="sxs-lookup"><span data-stu-id="417a3-114">To configure SSL offload with an application gateway, a certificate is required.</span></span> <span data-ttu-id="417a3-115">Bu sertifika uygulama ağ geçidinde yüklü ve SSL gönderilen trafiğin şifresi ve şifrelemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="417a3-115">This certificate is loaded on the application gateway and used to encrypt and decrypt the traffic sent via SSL.</span></span> <span data-ttu-id="417a3-116">Sertifika kişisel bilgi değişimi (pfx) biçiminde olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="417a3-116">The certificate needs to be in Personal Information Exchange (pfx) format.</span></span> <span data-ttu-id="417a3-117">Bu dosya biçimi, uygulama ağ geçidi tarafından şifreleme ve şifre çözme trafik gerçekleştirmek için gereken özel anahtar verilebilsin sağlar.</span><span class="sxs-lookup"><span data-stu-id="417a3-117">This file format allows for the private key to be exported which is required by the application gateway to perform the encryption and decryption of traffic.</span></span>

## <a name="add-an-https-listener"></a><span data-ttu-id="417a3-118">Bir HTTPS dinleyicisi ekleme</span><span class="sxs-lookup"><span data-stu-id="417a3-118">Add an HTTPS listener</span></span>

<span data-ttu-id="417a3-119">Kendi yapılandırmasına bağlı olarak trafik HTTPS dinleyicisi arar ve yardımcı olur, arka uç havuzları trafiği yönlendirmek.</span><span class="sxs-lookup"><span data-stu-id="417a3-119">The HTTPS listener looks for traffic based on its configuration and helps route the traffic to the backend pools.</span></span>

### <a name="step-1"></a><span data-ttu-id="417a3-120">1. Adım</span><span class="sxs-lookup"><span data-stu-id="417a3-120">Step 1</span></span>

<span data-ttu-id="417a3-121">Azure Portalı'na gidin ve var olan bir uygulama ağ geçidi seçin</span><span class="sxs-lookup"><span data-stu-id="417a3-121">Navigate to the Azure portal and select an existing application gateway</span></span>

### <a name="step-2"></a><span data-ttu-id="417a3-122">2. Adım</span><span class="sxs-lookup"><span data-stu-id="417a3-122">Step 2</span></span>

<span data-ttu-id="417a3-123">Dinleyicileri tıklayın ve bir dinleyici eklemek için Ekle düğmesini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="417a3-123">Click Listeners and click the Add button to add a listener.</span></span>

![Uygulama ağ geçidi'ne genel bakış dikey][1]

### <a name="step-3"></a><span data-ttu-id="417a3-125">3. Adım</span><span class="sxs-lookup"><span data-stu-id="417a3-125">Step 3</span></span>

<span data-ttu-id="417a3-126">.Pfx sertifika tamamlandıktan sonra Tamam'ı tıklatın gerekli bilgileri karşıya yükleme ve dinleyici için doldurun.</span><span class="sxs-lookup"><span data-stu-id="417a3-126">Fill out the required information for the listener and upload the .pfx certificate, when complete click OK.</span></span>

<span data-ttu-id="417a3-127">**Ad** -bu değer dinleyicisi kolay adıdır.</span><span class="sxs-lookup"><span data-stu-id="417a3-127">**Name** - This value is a friendly name of the listener.</span></span>

<span data-ttu-id="417a3-128">**Ön uç IP yapılandırmasını** -dinleyici için kullanılan ön uç IP yapılandırması bu değerdir.</span><span class="sxs-lookup"><span data-stu-id="417a3-128">**Frontend IP configuration** - This value is the frontend IP configuration that is used for the listener.</span></span>

<span data-ttu-id="417a3-129">**Ön uç bağlantı noktası (ad/bağlantı noktası)** - bağlantı noktası için bir kolay ad uygulama ağ geçidi ön ucunda gerçek bağlantı noktası kullanılır ve.</span><span class="sxs-lookup"><span data-stu-id="417a3-129">**Frontend port (Name/Port)** - A friendly name for the port used on the front end of the application gateway and the actual port used.</span></span>

<span data-ttu-id="417a3-130">**Protokol** -https veya http ön uç için kullanılıp kullanılmadığını belirlemek için bir anahtar.</span><span class="sxs-lookup"><span data-stu-id="417a3-130">**Protocol** - A switch to determine if https or http is used for the front end.</span></span>

<span data-ttu-id="417a3-131">**Sertifika (ad/parola)** - varsa SSL boşaltma kullanılır, bu ayar için bir .pfx sertifika gereklidir ve bir kolay ad ve parola gereklidir.</span><span class="sxs-lookup"><span data-stu-id="417a3-131">**Certificate (Name/Password)** - If SSL offload is used, a .pfx certificate is required for this setting and a friendly name and password are required.</span></span>

![Dinleyici dikey ekleme][2]

## <a name="create-a-rule-and-associate-it-to-the-listener"></a><span data-ttu-id="417a3-133">Bir kural oluşturmak ve dinleyiciye ilişkilendirme</span><span class="sxs-lookup"><span data-stu-id="417a3-133">Create a rule and associate it to the listener</span></span>

<span data-ttu-id="417a3-134">Dinleyici şimdi oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="417a3-134">The listener has now been created.</span></span> <span data-ttu-id="417a3-135">Dinleyici trafiği işlemek için bir kural oluşturmak için zaman yapılır.</span><span class="sxs-lookup"><span data-stu-id="417a3-135">It is time to create a rule to handle the traffic from the listener.</span></span> <span data-ttu-id="417a3-136">Kuralları trafiği birden çok oturum tanımlama bilgisi temelli benzeşimi kullanılıp kullanılmadığını dahil olmak üzere, yapılandırma ayarlarını, protokol, bağlantı noktası ve sistem durumu araştırmalarının göre arka uç havuzları nasıl yönlendirildiğini tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="417a3-136">Rules define how traffic is routed to the backend pools based on multiple configuration settings, including whether cookie-based session affinity is used, protocol, port, and health probes.</span></span>

### <a name="step-1"></a><span data-ttu-id="417a3-137">1. Adım</span><span class="sxs-lookup"><span data-stu-id="417a3-137">Step 1</span></span>

<span data-ttu-id="417a3-138">Tıklatın **kuralları** uygulama ağ geçidi ve ardından Ekle'yi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="417a3-138">Click the **Rules** of the application gateway, and then click Add.</span></span>

![Uygulama ağ geçidi kuralları dikey][3]

### <a name="step-2"></a><span data-ttu-id="417a3-140">2. Adım</span><span class="sxs-lookup"><span data-stu-id="417a3-140">Step 2</span></span>

<span data-ttu-id="417a3-141">Üzerinde **Ekle temel kural** dikey penceresinde, kural için bir kolay ad yazın ve önceki adımda oluşturduğunuz dinleyicisi seçin.</span><span class="sxs-lookup"><span data-stu-id="417a3-141">On the **Add basic rule** blade, type in the friendly name for the rule and choose the listener created in the previous step.</span></span> <span data-ttu-id="417a3-142">Http ayarlama ve uygun arka uç havuzu seçin ve tıklatın **Tamam**</span><span class="sxs-lookup"><span data-stu-id="417a3-142">Choose the appropriate backend pool and http setting and click **OK**</span></span>

![HTTPS Ayarları penceresi][4]

<span data-ttu-id="417a3-144">Ayarları artık uygulama ağ geçidi için kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="417a3-144">The settings are now saved to the application gateway.</span></span> <span data-ttu-id="417a3-145">Kaydetme işlemi portal veya PowerShell aracılığıyla görüntülemek kullanılabilir önce bu ayarları biraz zaman alabilir.</span><span class="sxs-lookup"><span data-stu-id="417a3-145">The save process for these settings may take a while before they are available to view through the portal or through PowerShell.</span></span> <span data-ttu-id="417a3-146">Uygulama ağ geçidi kaydedildikten sonra şifreleme ve şifre çözme trafiği işler.</span><span class="sxs-lookup"><span data-stu-id="417a3-146">Once saved the application gateway handles the encryption and decryption of traffic.</span></span> <span data-ttu-id="417a3-147">Uygulama ağ geçidi ve arka uç web sunucuları arasındaki tüm trafik http üzerinden ele alınacaktır.</span><span class="sxs-lookup"><span data-stu-id="417a3-147">All traffic between the application gateway and the backend web servers will be handled over http.</span></span> <span data-ttu-id="417a3-148">Tüm iletişim https üzerinden başlattıysanız istemciye şifrelenmiş istemciye döndürülür.</span><span class="sxs-lookup"><span data-stu-id="417a3-148">Any communication back to the client if initiated over https will be returned to the client encrypted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="417a3-149">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="417a3-149">Next steps</span></span>

<span data-ttu-id="417a3-150">Azure uygulama ağ geçidi ile bir özel durum araştırması yapılandırma konusunda bilgi edinmek için [bir özel durum araştırması oluşturmak](application-gateway-create-gateway-portal.md).</span><span class="sxs-lookup"><span data-stu-id="417a3-150">To learn how to configure a custom health probe with Azure Application Gateway, see [Create a custom health probe](application-gateway-create-gateway-portal.md).</span></span>

[1]: ./media/application-gateway-ssl-portal/figure1.png
[2]: ./media/application-gateway-ssl-portal/figure2.png
[3]: ./media/application-gateway-ssl-portal/figure3.png
[4]: ./media/application-gateway-ssl-portal/figure4.png
