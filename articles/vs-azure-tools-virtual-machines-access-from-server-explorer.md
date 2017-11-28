---
title: Azure sanal makineleri Sunucu Gezgini'nden aaaAccessing | Microsoft Docs
description: "Tooview oluşturma ve Azure sanal makineleri (VM'ler) Visual Studio Sunucu Gezgininde yönetmek bir genel bakış alın."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: eb3afde6-ba90-4308-9ac1-3cc29da4ede0
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: f8326aed105a64ca558f766d712cc68701f82c15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-azure-virtual-machines-from-server-explorer"></a><span data-ttu-id="94cd1-103">Server Explorer'dan Azure sanal makineleri erişme</span><span class="sxs-lookup"><span data-stu-id="94cd1-103">Accessing Azure Virtual Machines from Server Explorer</span></span>
<span data-ttu-id="94cd1-104">Visual Studio'da Sunucu Gezgini kullanarak, Azure tarafından barındırılan sanal makinelerinizi hakkındaki bilgileri görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="94cd1-104">By using Server Explorer in Visual Studio, you can display information about your virtual machines hosted by Azure.</span></span>

## <a name="accessing-virtual-machines-in-server-explorer"></a><span data-ttu-id="94cd1-105">Sanal makineler Sunucu Gezgininde erişme</span><span class="sxs-lookup"><span data-stu-id="94cd1-105">Accessing virtual machines in Server Explorer</span></span>
<span data-ttu-id="94cd1-106">Azure tarafından barındırılan sanal makineler varsa, sunucu Gezgini'nde erişebilir.</span><span class="sxs-lookup"><span data-stu-id="94cd1-106">If you have virtual machines hosted by Azure, you can access them in Server Explorer.</span></span> <span data-ttu-id="94cd1-107">Mobil hizmetler tooyour Azure aboneliği tooview ilk kez oturum gerekir.</span><span class="sxs-lookup"><span data-stu-id="94cd1-107">You must first sign in tooyour Azure subscription tooview your mobile services.</span></span> <span data-ttu-id="94cd1-108">toosign, sunucu Gezgini'nde hello Azure düğümü için hello kısayol menüsünü açın ve seçin **tooMicrosoft Azure Connect**.</span><span class="sxs-lookup"><span data-stu-id="94cd1-108">toosign in, open hello shortcut menu for hello Azure node in Server Explorer, and choose **Connect tooMicrosoft Azure**.</span></span>

### <a name="tooget-information-about-your-virtual-machines"></a><span data-ttu-id="94cd1-109">sanal makinelerinizi hakkında tooget bilgi</span><span class="sxs-lookup"><span data-stu-id="94cd1-109">tooget information about your virtual machines</span></span>
1. <span data-ttu-id="94cd1-110">Sunucu Gezgini'nde, bir sanal makine seçin ve kendi özellikleri penceresinde hello F4 anahtar tooshow'i seçin.</span><span class="sxs-lookup"><span data-stu-id="94cd1-110">In Server Explorer, choose a virtual machine, and then choose hello F4 key tooshow its properties window.</span></span>
   
    <span data-ttu-id="94cd1-111">Aşağıdaki tablonun hello hangi özelliklerin kullanılabilir olduğunu gösterir, ancak tüm salt okunurdur.</span><span class="sxs-lookup"><span data-stu-id="94cd1-111">hello following table shows what properties are available, but they are all read-only.</span></span> <span data-ttu-id="94cd1-112">toochange bunları kullanan hello [Klasik Azure portalı](http://go.microsoft.com/fwlink/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="94cd1-112">toochange them, use hello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885).</span></span>
   
   | <span data-ttu-id="94cd1-113">Özellik</span><span class="sxs-lookup"><span data-stu-id="94cd1-113">Property</span></span> | <span data-ttu-id="94cd1-114">Açıklama</span><span class="sxs-lookup"><span data-stu-id="94cd1-114">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="94cd1-115">DNS Adı</span><span class="sxs-lookup"><span data-stu-id="94cd1-115">DNS Name</span></span> |<span data-ttu-id="94cd1-116">Merhaba hello sanal makinenin Internet adresi ile Merhaba URL'si.</span><span class="sxs-lookup"><span data-stu-id="94cd1-116">hello URL with hello Internet address of hello virtual machine.</span></span> |
   | <span data-ttu-id="94cd1-117">Ortam</span><span class="sxs-lookup"><span data-stu-id="94cd1-117">Environment</span></span> |<span data-ttu-id="94cd1-118">Bir sanal makine için hello bu özellik her zaman üretim değeridir.</span><span class="sxs-lookup"><span data-stu-id="94cd1-118">For a virtual machine, hello value of this property is always Production.</span></span> |
   | <span data-ttu-id="94cd1-119">Ad</span><span class="sxs-lookup"><span data-stu-id="94cd1-119">Name</span></span> |<span data-ttu-id="94cd1-120">Merhaba sanal makinenin adını Hello.</span><span class="sxs-lookup"><span data-stu-id="94cd1-120">hello name of hello virtual machine.</span></span> |
   | <span data-ttu-id="94cd1-121">Boyut</span><span class="sxs-lookup"><span data-stu-id="94cd1-121">Size</span></span> |<span data-ttu-id="94cd1-122">kullanılabilir bellek ve disk alanı miktarını hello yansıtır hello sanal makine Hello boyutu.</span><span class="sxs-lookup"><span data-stu-id="94cd1-122">hello size of hello virtual machine, which reflects hello amount of memory and disk space that’s available.</span></span> <span data-ttu-id="94cd1-123">Daha fazla bilgi için bkz: nasıl yapılır: sanal makine boyutlarını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="94cd1-123">For more information, see How To: Configure Virtual Machine Sizes.</span></span> |
   | <span data-ttu-id="94cd1-124">Durum</span><span class="sxs-lookup"><span data-stu-id="94cd1-124">Status</span></span> |<span data-ttu-id="94cd1-125">Değerleri başlatma, başlatıldı, durdurma, durduruldu ve alma durumunu içerir.</span><span class="sxs-lookup"><span data-stu-id="94cd1-125">Values include Starting, Started, Stopping, Stopped, and Retrieving Status.</span></span> <span data-ttu-id="94cd1-126">Durum alınıyor görünürse, hello geçerli durumu bilinmiyor.</span><span class="sxs-lookup"><span data-stu-id="94cd1-126">If Retrieving Status appears, hello current status is unknown.</span></span> <span data-ttu-id="94cd1-127">Bu özellik için Hello değerler farklı hello üzerinde kullanılan hello değerlerinden [Klasik Azure portalı](http://go.microsoft.com/fwlink/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="94cd1-127">hello values for this property differ from hello values that are used on hello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885).</span></span> |
   | <span data-ttu-id="94cd1-128">Subscriptionıd</span><span class="sxs-lookup"><span data-stu-id="94cd1-128">SubscriptionID</span></span> |<span data-ttu-id="94cd1-129">Azure hesabınız için Hello abonelik kimliği.</span><span class="sxs-lookup"><span data-stu-id="94cd1-129">hello subscription ID for your Azure account.</span></span> <span data-ttu-id="94cd1-130">Bu bilgileri üzerinde hello gösterebilir [Klasik Azure portalı](http://go.microsoft.com/fwlink/?LinkID=213885) bir abonelik hello özelliklerini görüntüleyerek.</span><span class="sxs-lookup"><span data-stu-id="94cd1-130">You can show this information on hello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885) by viewing hello properties for a subscription.</span></span> |
2. <span data-ttu-id="94cd1-131">Bir uç nokta düğümü seçin ve ardından hello görüntüleyin **özellikleri** penceresi.</span><span class="sxs-lookup"><span data-stu-id="94cd1-131">Choose an endpoint node, and then view hello **Properties** window.</span></span>
3. <span data-ttu-id="94cd1-132">Merhaba aşağıdaki tabloda açıklanmaktadır hello kullanılabilir özellikler uç noktaları, ancak salt okunurdur.</span><span class="sxs-lookup"><span data-stu-id="94cd1-132">hello following table describes hello available properties of endpoints, but they are read-only.</span></span> <span data-ttu-id="94cd1-133">tooadd veya düzenleme hello uç noktaları bir sanal makine için kullanmak hello [Klasik Azure portalı](http://go.microsoft.com/fwlink/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="94cd1-133">tooadd or edit hello endpoints for a virtual machine, use hello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885).</span></span> 
   
   | <span data-ttu-id="94cd1-134">Özellik</span><span class="sxs-lookup"><span data-stu-id="94cd1-134">Property</span></span> | <span data-ttu-id="94cd1-135">Açıklama</span><span class="sxs-lookup"><span data-stu-id="94cd1-135">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="94cd1-136">Ad</span><span class="sxs-lookup"><span data-stu-id="94cd1-136">Name</span></span> |<span data-ttu-id="94cd1-137">Merhaba uç noktası için bir tanımlayıcı.</span><span class="sxs-lookup"><span data-stu-id="94cd1-137">An identifier for hello endpoint.</span></span> |
   | <span data-ttu-id="94cd1-138">Özel bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="94cd1-138">Private Port</span></span> |<span data-ttu-id="94cd1-139">ağ erişim iç tooyour uygulaması için başlangıç bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="94cd1-139">hello port for network access internal tooyour application.</span></span> |
   | <span data-ttu-id="94cd1-140">Protokol</span><span class="sxs-lookup"><span data-stu-id="94cd1-140">Protocol</span></span> |<span data-ttu-id="94cd1-141">Bu uç noktası için Aktarım katmanı hello hello protokolü, TCP veya UDP'i kullanır.</span><span class="sxs-lookup"><span data-stu-id="94cd1-141">hello protocol that hello transport layer for this endpoint uses, either TCP or UDP.</span></span> |
   | <span data-ttu-id="94cd1-142">Genel Bağlantı Noktası</span><span class="sxs-lookup"><span data-stu-id="94cd1-142">Public Port</span></span> |<span data-ttu-id="94cd1-143">Genel erişim tooyour uygulama için kullanılacak başlangıç bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="94cd1-143">hello port that’s used for public access tooyour application.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="94cd1-144">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="94cd1-144">Next steps</span></span>
<span data-ttu-id="94cd1-145">Visual Studio'da Azure rolleri kullanma hakkında daha fazla toolearn bkz [Azure rolleri ile Uzak Masaüstü kullanarak](vs-azure-tools-remote-desktop-roles.md).</span><span class="sxs-lookup"><span data-stu-id="94cd1-145">toolearn more about using Azure roles in Visual Studio, see [Using Remote Desktop with Azure Roles](vs-azure-tools-remote-desktop-roles.md).</span></span>

