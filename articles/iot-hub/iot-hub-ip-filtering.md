---
title: "aaaAzure IOT Hub IP bağlantı filtrelerini | Microsoft Docs"
description: "Nasıl tooyour Azure IOT hub için belirli IP tooblock bağlantılarından filtreleme toouse IP adresleri. Tek tek bağlantılarından veya IP adres aralıklarını engelleyebilirsiniz."
services: iot-hub
documentationcenter: 
author: BeatriceOltean
manager: timlt
editor: 
ms.assetid: f833eac3-5b5f-46a7-a47b-f4f6fc927f3f
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/23/2017
ms.author: boltean
ms.openlocfilehash: 45e5906a494561b6108895d86d6a04fc3b52b8fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-ip-filters"></a><span data-ttu-id="d41ef-104">IP filtreleri kullanın</span><span class="sxs-lookup"><span data-stu-id="d41ef-104">Use IP filters</span></span>

<span data-ttu-id="d41ef-105">Güvenlik Azure IOT hub'ına bağlı herhangi bir IOT çözümü önemli bir yönüdür.</span><span class="sxs-lookup"><span data-stu-id="d41ef-105">Security is an important aspect of any IoT solution based on Azure IoT Hub.</span></span> <span data-ttu-id="d41ef-106">Bazen tooexplicitly gereken güvenlik yapılandırmanızın bir parçası, cihazları bağlanabilir hello IP adreslerini belirtin.</span><span class="sxs-lookup"><span data-stu-id="d41ef-106">Sometimes you need tooexplicitly specify hello IP addresses from which devices can connect as part of your security configuration.</span></span> <span data-ttu-id="d41ef-107">Merhaba _IP Filtresi_ özelliği tooconfigure kurallarını reddetme veya belirli IPv4 adresleri gelen trafiği kabul etmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="d41ef-107">hello _IP filter_ feature enables you tooconfigure rules for rejecting or accepting traffic from specific IPv4 addresses.</span></span>

## <a name="when-toouse"></a><span data-ttu-id="d41ef-108">Zaman toouse</span><span class="sxs-lookup"><span data-stu-id="d41ef-108">When toouse</span></span>

<span data-ttu-id="d41ef-109">Belirli IP adresleri için yararlı tooblock hello IOT Hub uç noktaları olduğunda iki belirli kullanım örnekleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="d41ef-109">There are two specific use-cases when it is useful tooblock hello IoT Hub endpoints for certain IP addresses:</span></span>

- <span data-ttu-id="d41ef-110">IOT hub'ınızı trafiği yalnızca belirtilen IP adreslerinden almak ve şey Reddet gerekir.</span><span class="sxs-lookup"><span data-stu-id="d41ef-110">Your IoT hub should receive traffic only from a specified range of IP addresses and reject everything else.</span></span> <span data-ttu-id="d41ef-111">Örneğin, IOT hub'ınıza kullanarak [Azure Express rota] toocreate IOT hub'ı ve şirket içi altyapınızı arasında özel bağlantılar.</span><span class="sxs-lookup"><span data-stu-id="d41ef-111">For example, you are using your IoT hub with [Azure Express Route] toocreate private connections between an IoT hub and your on-premises infrastructure.</span></span>
- <span data-ttu-id="d41ef-112">Kuşkulu olarak hello IOT hub'ı yönetici tarafından belirlenen IP adreslerinden gelen tooreject trafiğine gerekir.</span><span class="sxs-lookup"><span data-stu-id="d41ef-112">You need tooreject traffic from IP addresses that have been identified as suspicious by hello IoT hub administrator.</span></span>

## <a name="how-filter-rules-are-applied"></a><span data-ttu-id="d41ef-113">Filtre kuralları nasıl uygulanır</span><span class="sxs-lookup"><span data-stu-id="d41ef-113">How filter rules are applied</span></span>

<span data-ttu-id="d41ef-114">Hello IP Filtresi kuralları IOT hub'ı hizmet düzeyi hello sırasında uygulanır.</span><span class="sxs-lookup"><span data-stu-id="d41ef-114">hello IP filter rules are applied at hello IoT Hub service level.</span></span> <span data-ttu-id="d41ef-115">Bu nedenle cihazları ve herhangi bir desteklenen protokolünü kullanarak arka uç uygulamaları tooall bağlantılarını hello IP filtresi kurallarını uygulayın.</span><span class="sxs-lookup"><span data-stu-id="d41ef-115">Therefore hello IP filter rules apply tooall connections from devices and back-end apps using any supported protocol.</span></span>

<span data-ttu-id="d41ef-116">IOT hub'ınızdaki rejecting IP kuralıyla eşleşen bir IP adresinden gelen bağlantı girişimleri yetkisiz 401 durum kodu ve açıklama alır.</span><span class="sxs-lookup"><span data-stu-id="d41ef-116">Any connection attempt from an IP address that matches a rejecting IP rule in your IoT hub receives an unauthorized 401 status code and description.</span></span> <span data-ttu-id="d41ef-117">Merhaba yanıt iletisi hello IP kural Bahsediyor değil.</span><span class="sxs-lookup"><span data-stu-id="d41ef-117">hello response message does not mention hello IP rule.</span></span>

## <a name="default-setting"></a><span data-ttu-id="d41ef-118">Varsayılan ayar</span><span class="sxs-lookup"><span data-stu-id="d41ef-118">Default setting</span></span>

<span data-ttu-id="d41ef-119">Varsayılan olarak, hello **IP Filtresi** hello portalında bir IOT hub'ına yönelik kılavuz boştur.</span><span class="sxs-lookup"><span data-stu-id="d41ef-119">By default, hello **IP Filter** grid in hello portal for an IoT hub is empty.</span></span> <span data-ttu-id="d41ef-120">Bu varsayılan ayarı hub'ınızı herhangi bir IP adresi bağlantılarını kabul anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="d41ef-120">This default setting means that your hub accepts connections any IP address.</span></span> <span data-ttu-id="d41ef-121">Bu varsayılan ayarı hello 0.0.0.0/0 IP adresi aralığı kabul eşdeğer tooa kuralıdır.</span><span class="sxs-lookup"><span data-stu-id="d41ef-121">This default setting is equivalent tooa rule that accepts hello 0.0.0.0/0 IP address range.</span></span>

![IOT hub'ı varsayılan IP Filtresi Ayarları][img-ip-filter-default]

## <a name="add-or-edit-an-ip-filter-rule"></a><span data-ttu-id="d41ef-123">IP filtre kuralı Ekle veya Düzenle</span><span class="sxs-lookup"><span data-stu-id="d41ef-123">Add or edit an IP filter rule</span></span>

<span data-ttu-id="d41ef-124">IP filtre kuralı eklediğinizde, aşağıdaki değerleri Merhaba istenir:</span><span class="sxs-lookup"><span data-stu-id="d41ef-124">When you add an IP filter rule, you are prompted for hello following values:</span></span>

- <span data-ttu-id="d41ef-125">Bir **IP filtre kuralı adı** too128 karakter uzunluğunda yukarı benzersiz, büyük küçük harf duyarsız, alfasayısal bir dize olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d41ef-125">An **IP filter rule name** that must be a unique, case-insensitive, alphanumeric string up too128 characters long.</span></span> <span data-ttu-id="d41ef-126">Yalnızca ASCII 7 bit hello alfasayısal karakterler artı `{'-', ':', '/', '\', '.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '''}` kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="d41ef-126">Only hello ASCII 7-bit alphanumeric characters plus `{'-', ':', '/', '\', '.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '''}` are accepted.</span></span>
- <span data-ttu-id="d41ef-127">Seçin bir **Reddet** veya **kabul** hello olarak **eylem** hello IP filtre kuralı için.</span><span class="sxs-lookup"><span data-stu-id="d41ef-127">Select a **reject** or **accept** as hello **action** for hello IP filter rule.</span></span>
- <span data-ttu-id="d41ef-128">Tek bir IPv4 adresi veya IP adreslerinin CIDR gösteriminde sağlar.</span><span class="sxs-lookup"><span data-stu-id="d41ef-128">Provide a single IPv4 address or a block of IP addresses in CIDR notation.</span></span> <span data-ttu-id="d41ef-129">Örneğin, içinde CIDR gösterimi 192.168.100.0/22 hello 1024 IPv4 adresleri 192.168.100.0 temsil eden too192.168.103.255.</span><span class="sxs-lookup"><span data-stu-id="d41ef-129">For example, in CIDR notation 192.168.100.0/22 represents hello 1024 IPv4 addresses from 192.168.100.0 too192.168.103.255.</span></span>

![IP filtre kuralı tooan IOT hub'ı ekleme][img-ip-filter-add-rule]

<span data-ttu-id="d41ef-131">Hello kural kaydettikten sonra o hello güncelleştirme devam ediyor bildiren bir uyarı görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="d41ef-131">After you save hello rule, you see an alert notifying you that hello update is in progress.</span></span>

![IP filtre kuralı kaydetme hakkında bildirim][img-ip-filter-save-new-rule]

<span data-ttu-id="d41ef-133">Merhaba **Ekle** hello en fazla 10 IP filtresi kurallarını ulaştığında seçeneği devre dışıdır.</span><span class="sxs-lookup"><span data-stu-id="d41ef-133">hello **Add** option is disabled when you reach hello maximum of 10 IP filter rules.</span></span>

<span data-ttu-id="d41ef-134">Mevcut bir kuralı hello kuralı içeren hello satır çift tıklayarak düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d41ef-134">You can edit an existing rule by double-clicking hello row that contains hello rule.</span></span>

> [!NOTE]
> <span data-ttu-id="d41ef-135">Reddetme IP adresleri hello IOT hub ile etkileşim diğer Azure Hizmetleri (örneğin, Azure akış analizi, Azure sanal makineleri veya hello aygıt Explorer hello Portalı'nda) engelleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d41ef-135">Rejecting IP addresses can prevent other Azure Services (such as Azure Stream Analytics, Azure Virtual Machines, or hello Device Explorer in hello portal) from interacting with hello IoT hub.</span></span>

> [!WARNING]
> <span data-ttu-id="d41ef-136">IP Filtresi etkinleştirilmiş bir IOT hub'ı Azure akış analizi (ASA) tooread iletileri kullanıyorsanız hello Event Hub ile uyumlu ada ve IOT hub'ınızın uç hello ASA bağlantı dizesi kullanın.</span><span class="sxs-lookup"><span data-stu-id="d41ef-136">If you use Azure Stream Analytics (ASA) tooread messages from an IoT hub with IP filtering enabled, use hello Event Hub-compatible name and endpoint of your IoT Hub in hello ASA connection string.</span></span>

## <a name="delete-an-ip-filter-rule"></a><span data-ttu-id="d41ef-137">IP filtre kuralını Sil</span><span class="sxs-lookup"><span data-stu-id="d41ef-137">Delete an IP filter rule</span></span>

<span data-ttu-id="d41ef-138">toodelete bir IP filtre kuralı seçin bir veya daha fazla kural hello kılavuz ve tıklatın **silmek**.</span><span class="sxs-lookup"><span data-stu-id="d41ef-138">toodelete an IP filter rule, select one or more rules in hello grid and click **Delete**.</span></span>

![Bir IOT Hub IP Filtresi kuralını silmek][img-ip-filter-delete-rule]

## <a name="ip-filter-rule-evaluation"></a><span data-ttu-id="d41ef-140">IP filtre kural değerlendirmesi</span><span class="sxs-lookup"><span data-stu-id="d41ef-140">IP filter rule evaluation</span></span>

<span data-ttu-id="d41ef-141">IP filtresi kurallarını sırayla uygulanır ve hello ilk kural eşleşen hello IP adresi hello belirler veya eylem reddedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d41ef-141">IP filter rules are applied in order and hello first rule that matches hello IP address determines hello accept or reject action.</span></span>

<span data-ttu-id="d41ef-142">Örneğin, hello aralığı 192.168.100.0/22 tooaccept adresleri istiyorsanız ve şey Reddet hello ilk kural hello kılavuzunda hello adres aralığı 192.168.100.0/22 kabul etmelidir.</span><span class="sxs-lookup"><span data-stu-id="d41ef-142">For example, if you want tooaccept addresses in hello range 192.168.100.0/22 and reject everything else, hello first rule in hello grid should accept hello address range 192.168.100.0/22.</span></span> <span data-ttu-id="d41ef-143">Merhaba sonraki kural hello aralığı 0.0.0.0/0 kullanarak tüm adresleri reddedecek.</span><span class="sxs-lookup"><span data-stu-id="d41ef-143">hello next rule should reject all addresses by using hello range 0.0.0.0/0.</span></span>

<span data-ttu-id="d41ef-144">Merhaba üç dikey noktalar hello başlangıç satır tıklayarak ve sürükleme kullanarak IP Filtresi kurallarınızı hello kılavuzunda hello sırasını değiştirmek ve bırakın.</span><span class="sxs-lookup"><span data-stu-id="d41ef-144">You can change hello order of your IP filter rules in hello grid by clicking hello three vertical dots at hello start of a row and using drag and drop.</span></span>

<span data-ttu-id="d41ef-145">Yeni IP toosave filtre kuralı sipariş, tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="d41ef-145">toosave your new IP filter rule order, click **Save**.</span></span>

![IOT Hub IP Filtresi kurallarınızı Hello sırasını değiştirme][img-ip-filter-rule-order]

## <a name="next-steps"></a><span data-ttu-id="d41ef-147">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d41ef-147">Next steps</span></span>

<span data-ttu-id="d41ef-148">toofurther IOT hub'ı hello özelliklerini keşfedin, bakın:</span><span class="sxs-lookup"><span data-stu-id="d41ef-148">toofurther explore hello capabilities of IoT Hub, see:</span></span>

- <span data-ttu-id="d41ef-149">[İzleme işlemleri][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="d41ef-149">[Operations monitoring][lnk-monitor]</span></span>
- <span data-ttu-id="d41ef-150">[IOT hub'ı ölçümleri][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="d41ef-150">[IoT Hub metrics][lnk-metrics]</span></span>

<!-- Images -->
[img-ip-filter-default]: ./media/iot-hub-ip-filtering/ip-filter-default.png
[img-ip-filter-add-rule]: ./media/iot-hub-ip-filtering/ip-filter-add-rule.png
[img-ip-filter-save-new-rule]: ./media/iot-hub-ip-filtering/ip-filter-save-new-rule.png
[img-ip-filter-delete-rule]: ./media/iot-hub-ip-filtering/ip-filter-delete-rule.png
[img-ip-filter-rule-order]: ./media/iot-hub-ip-filtering/ip-filter-rule-order.png


<!-- Links -->

[IoT Hub developer guide]: iot-hub-devguide.md
[Azure Express rota]:  https://azure.microsoft.com/en-us/documentation/articles/expressroute-faqs/#supported-services

[lnk-monitor]: iot-hub-operations-monitoring.md
[lnk-metrics]: iot-hub-metrics.md