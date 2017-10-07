---
title: "aaaAzure RemoteApp görüntü gereksinimleri | Microsoft Docs"
description: "Azure RemoteApp ile kullanılan görüntüleri toobe oluşturmak için hello gereksinimleri hakkında bilgi edinin"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 7cbb90f4-6dc9-462c-a429-088cdb57414e
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 4e35203eb93a866d4e0bd591d42b34746c7ffa4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="requirements-for-azure-remoteapp-images"></a><span data-ttu-id="0b70f-103">Azure RemoteApp görüntüleri için gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="0b70f-103">Requirements for Azure RemoteApp images</span></span>
> [!IMPORTANT]
> <span data-ttu-id="0b70f-104">Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır.</span><span class="sxs-lookup"><span data-stu-id="0b70f-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="0b70f-105">Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="0b70f-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="0b70f-106">Azure RemoteApp Kullanıcılarınızla tooshare istediğiniz tüm hello programlar Windows Server 2012 R2 görüntüsünü toohost kullanır.</span><span class="sxs-lookup"><span data-stu-id="0b70f-106">Azure RemoteApp uses a Windows Server 2012 R2 image toohost all hello programs that you want tooshare with your users.</span></span> <span data-ttu-id="0b70f-107">özel görüntü toocreate, varolan bir görüntüyle başlayabilir veya [yeni bir tane oluşturun](remoteapp-create-custom-image.md).</span><span class="sxs-lookup"><span data-stu-id="0b70f-107">toocreate a custom image, you can start with an existing image or [create a new one](remoteapp-create-custom-image.md).</span></span>

> [!TIP]
> <span data-ttu-id="0b70f-108">Tooa Windows Server 2012 R2 görüntüsünde, Azure RemoteApp abonelik erişmenizi kendi şablon görüntüsü toocreate kullanabileceğiniz Azure VM galeri hello biliyor muydunuz?</span><span class="sxs-lookup"><span data-stu-id="0b70f-108">Did you know that your Azure RemoteApp subscription gives you access tooa Windows Server 2012 R2 image in hello Azure VM gallery that you can use toocreate your own template image?</span></span> <span data-ttu-id="0b70f-109">[Kullanıma](remoteapp-image-on-azurevm.md).</span><span class="sxs-lookup"><span data-stu-id="0b70f-109">[Check it out](remoteapp-image-on-azurevm.md).</span></span>  
> 
> 

<span data-ttu-id="0b70f-110">Azure RemoteApp ile kullanılmak üzere karşıya hello görüntüsü için Hello gereksinimleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="0b70f-110">hello requirements for hello image that can be uploaded for use with Azure RemoteApp are:</span></span>

* <span data-ttu-id="0b70f-111">Özel uygulamalar veri hello görüntüde yerel olarak depolamayın.</span><span class="sxs-lookup"><span data-stu-id="0b70f-111">Custom applications don’t store data locally on hello image.</span></span> <span data-ttu-id="0b70f-112">Bu görüntüler, durum bilgisiz ve uygulamalar yalnızca içermelidir.</span><span class="sxs-lookup"><span data-stu-id="0b70f-112">These images are stateless and should only contain applications.</span></span>
* <span data-ttu-id="0b70f-113">Merhaba görüntü kaybedilen veri içermiyor.</span><span class="sxs-lookup"><span data-stu-id="0b70f-113">hello image does not contain data that can be lost.</span></span>
* <span data-ttu-id="0b70f-114">Merhaba görüntü boyutu, MB katları olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="0b70f-114">hello image size should be a multiple of MBs.</span></span> <span data-ttu-id="0b70f-115">Tooupload tam katı değil bir görüntü deneyin hello karşıya yükleme başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="0b70f-115">If you try tooupload an image that is not an exact multiple, hello upload will fail.</span></span>
* <span data-ttu-id="0b70f-116">Merhaba görüntü boyutu 127 GB olmalıdır ya da daha küçük.</span><span class="sxs-lookup"><span data-stu-id="0b70f-116">hello image size must be 127 GB or smaller.</span></span>
* <span data-ttu-id="0b70f-117">Bir VHD dosyası üzerinde olmalıdır (VHDX dosyaları şu anda desteklenmiyor).</span><span class="sxs-lookup"><span data-stu-id="0b70f-117">It must be on a VHD file (VHDX files are not currently supported).</span></span>
* <span data-ttu-id="0b70f-118">Merhaba VHD 2. nesil sanal makine olmaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="0b70f-118">hello VHD must not be a generation 2 virtual machine.</span></span>
* <span data-ttu-id="0b70f-119">Merhaba VHD sabit boyutlu veya dinamik olarak genişletilen olabilir.</span><span class="sxs-lookup"><span data-stu-id="0b70f-119">hello VHD can be either fixed-size or dynamically expanding.</span></span> <span data-ttu-id="0b70f-120">Bir sabit boyutlu VHD dosyası'den daha az zaman tooupload tooAzure aldığından dinamik olarak genişleyen bir VHD önerilir.</span><span class="sxs-lookup"><span data-stu-id="0b70f-120">A dynamically expanding VHD is recommended because it takes less time tooupload tooAzure than a fixed-size VHD file.</span></span>
* <span data-ttu-id="0b70f-121">Merhaba ana önyükleme kaydı (MBR) bölümleme stilini kullanarak Hello disk başlatılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="0b70f-121">hello disk must be initialized using hello Master Boot Record (MBR) partitioning style.</span></span> <span data-ttu-id="0b70f-122">Merhaba GUID bölümleme tablosu (GPT) bölümleme stilini desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="0b70f-122">hello GUID partition table (GPT) partition style is not supported.</span></span>
* <span data-ttu-id="0b70f-123">Merhaba VHD tek bir Windows Server 2012 R2 yüklemesini içermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="0b70f-123">hello VHD must contain a single installation of Windows Server 2012 R2.</span></span> <span data-ttu-id="0b70f-124">Windows yüklemesini içeren birden çok birim, ancak yalnızca bir içerebilir.</span><span class="sxs-lookup"><span data-stu-id="0b70f-124">It can contain multiple volumes, but only one that contains an installation of Windows.</span></span>
* <span data-ttu-id="0b70f-125">Merhaba Uzak Masaüstü oturumu ana bilgisayarı (RDSH) rolü ve hello Masaüstü Deneyimi özelliği yüklü olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="0b70f-125">hello Remote Desktop Session Host (RDSH) role and hello Desktop Experience feature must be installed.</span></span>
* <span data-ttu-id="0b70f-126">Merhaba Uzak Masaüstü Bağlantı Aracısı rol gerekir *değil* yüklü olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="0b70f-126">hello Remote Desktop Connection Broker role must *not* be installed.</span></span>
* <span data-ttu-id="0b70f-127">Merhaba şifreleme dosya sistemi (EFS) devre dışı bırakılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="0b70f-127">hello Encrypting File System (EFS) must be disabled.</span></span>
* <span data-ttu-id="0b70f-128">Merhaba görüntüsü hello parametrelerini kullanarak bir Sysprep uygulanmış olması gerekir **/oobe / generalize/shutdown** (yapmak kullanmaz hello **/mode:vm** parametresi).</span><span class="sxs-lookup"><span data-stu-id="0b70f-128">hello image must be SYSPREPed using hello parameters **/oobe /generalize /shutdown** (DO NOT use hello **/mode:vm** parameter).</span></span>
* <span data-ttu-id="0b70f-129">Bir anlık görüntü zinciri, VHD'den karşıya yükleme desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="0b70f-129">Uploading your VHD from a snapshot chain is not supported.</span></span>

<span data-ttu-id="0b70f-130">Bkz: [Azure RemoteApp görüntüsü oluşturma](remoteapp-imageoptions.md) Azure RemoteApp için görüntüleri oluşturma hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="0b70f-130">See [Create an Azure RemoteApp image](remoteapp-imageoptions.md) for more information about creating images for Azure RemoteApp.</span></span>

