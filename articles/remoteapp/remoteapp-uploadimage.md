---
title: "Azure RemoteApp için özel bir görüntü aaaUpload | Microsoft Docs"
description: "Nasıl tooupload özel bir görüntü Azure RemoteApp için bilgi edinin"
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: 299e0510-1a6b-4fdf-914a-3631b061a360
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: ericor
ms.openlocfilehash: 6ad40fe58795ece37f4c7900be01bc713938da87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-custom-image-for-azure-remoteapp"></a><span data-ttu-id="61677-103">Özel görüntü Azure RemoteApp için karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="61677-103">Upload a custom image for Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="61677-104">Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır.</span><span class="sxs-lookup"><span data-stu-id="61677-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="61677-105">Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="61677-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="61677-106">Özel şablon görüntünüzü oluşturmuş veya değişikliklerle güncelleştirdiniz göre bu görüntü tooyour Azure RemoteApp görüntü kitaplığı tooupload gerekir.</span><span class="sxs-lookup"><span data-stu-id="61677-106">Now that you have created your custom template image or have updated it with changes, you need tooupload that image tooyour Azure RemoteApp image library.</span></span> <span data-ttu-id="61677-107">Bu adımları kullanın.</span><span class="sxs-lookup"><span data-stu-id="61677-107">Use these steps.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="61677-108">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="61677-108">Before you start</span></span>
1. <span data-ttu-id="61677-109">Özel görüntünüzü hello karşıladığını doğrulamak [görüntü gereksinimleri](remoteapp-imagereqs.md) ve [uygulama gereksinimleri](remoteapp-appreqs.md).</span><span class="sxs-lookup"><span data-stu-id="61677-109">Verify your custom image meets hello [image requirements](remoteapp-imagereqs.md) and [application requirements](remoteapp-appreqs.md).</span></span>
2. <span data-ttu-id="61677-110">Merhaba yüklemek [Azure PowerShell Modülü](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="61677-110">Install hello [Azure PowerShell module](/powershell/azure/overview).</span></span>

## <a name="step-by-step-on-how-tooupload-custom-image"></a><span data-ttu-id="61677-111">Adım adım izlenecek tooupload özel görüntü</span><span class="sxs-lookup"><span data-stu-id="61677-111">Step by step on how tooupload custom image</span></span>
1. <span data-ttu-id="61677-112">Azure Yönetim Portalı'nı açın ve toohello RemoteApp sayfasına gidin.</span><span class="sxs-lookup"><span data-stu-id="61677-112">Open Azure Management Portal and navigate toohello RemoteApp page.</span></span>
2. <span data-ttu-id="61677-113">Merhaba üzerinde **şablon görüntüleri** sekmesini tıklatın, **karşıya** hello sayfanın hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="61677-113">On hello **Template images** tab, click **Upload** at hello bottom of hello page.</span></span>
3. <span data-ttu-id="61677-114">Görüntü için kolay bir ad girin ve hello depolama hesap konumu belirtin.</span><span class="sxs-lookup"><span data-stu-id="61677-114">Enter a friendly name for your image and specify hello storage account location.</span></span> <span data-ttu-id="61677-115">Başlangıç konumu hello olduğundan emin olun, RemoteApp koleksiyonu veya toocreate bir istediğiniz bir konuma aynı konumda.</span><span class="sxs-lookup"><span data-stu-id="61677-115">Ensure hello location is hello same location as your RemoteApp collection or a location where you want toocreate one.</span></span>
4. <span data-ttu-id="61677-116">İstendiğinde, hello betik tooyour karşıdan yerel bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="61677-116">When prompted, download hello script tooyour local PC.</span></span>
5. <span data-ttu-id="61677-117">Merhaba komut parametreleri hello metin kutusu tooyour panoya kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="61677-117">Copy hello command parameters in hello text box tooyour clipboard.</span></span>
6. <span data-ttu-id="61677-118">Yükseltilmiş bir Windows PowerShell penceresi açın.</span><span class="sxs-lookup"><span data-stu-id="61677-118">Open an elevated Windows PowerShell window.</span></span>
7. <span data-ttu-id="61677-119">Windows PowerShell penceresinde Hello yükseltilmiş toohello gidin hello komut dosyasını indirdiğiniz aynı dizin.</span><span class="sxs-lookup"><span data-stu-id="61677-119">From hello elevated Windows PowerShell window, navigate toohello same directory where you downloaded hello script.</span></span>
8. <span data-ttu-id="61677-120">Yapıştır hello kopyalanan komutu ve tuşuna **Enter**.</span><span class="sxs-lookup"><span data-stu-id="61677-120">Paste hello copied command and press **Enter**.</span></span>
   
   <span data-ttu-id="61677-121">Merhaba karşıya yükleme işlemi başlar ve süre hello görüntünün boyutu ve ağ hızı dahil olmak üzere birçok faktöre bağlıdır</span><span class="sxs-lookup"><span data-stu-id="61677-121">hello upload process will begin and duration may depend on many factors including your network speed and size of hello image</span></span>
9. <span data-ttu-id="61677-122">Karşıya yüklemeyi ağ kesintisi veya şeyler nedeniyle gibi başarılı olmazsa, her zaman, başlangıcından hello karşıya yükleme işlemi devam edebilir.</span><span class="sxs-lookup"><span data-stu-id="61677-122">If your upload does not succeed because of network interruption or things like that, you can always resume hello upload process you began.</span></span> <span data-ttu-id="61677-123">Merhaba komut dosyasını kullanarak yeniden çalıştırmak tooresume bir karşıya yükleme hello aynı komut satırı.</span><span class="sxs-lookup"><span data-stu-id="61677-123">tooresume an upload, run hello script again using hello same command line.</span></span>

> [!WARNING]
> <span data-ttu-id="61677-124">Hiçbir zaman hello karşıya yükleme komut dosyasını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="61677-124">Never modify hello upload script.</span></span> <span data-ttu-id="61677-125">Özel denetimler görüntü hello görüntü gereksinimlerini karşıladığını ve uygulama gereksinimleri hello uygulanan tooensure olmuştur.</span><span class="sxs-lookup"><span data-stu-id="61677-125">Specific checks have been implemented tooensure that hello image meets hello image requirements and application requirements.</span></span>
> 
> 

## <a name="common-problems"></a><span data-ttu-id="61677-126">Sık karşılaşılan sorunları</span><span class="sxs-lookup"><span data-stu-id="61677-126">Common problems</span></span>
* <span data-ttu-id="61677-127">Windows PowerShell, Azure PowerShell kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="61677-127">Make sure you use Windows PowerShell, not Azure PowerShell.</span></span> <span data-ttu-id="61677-128">Belirli modüller hello karşıya yükleme işlemi sırasında gerekli olduğu için tooinstall hello Azure PowerShell modülü gerekir.</span><span class="sxs-lookup"><span data-stu-id="61677-128">You need tooinstall hello Azure PowerShell module because certain modules are needed during hello upload process.</span></span>
* <span data-ttu-id="61677-129">Hiçbir zaman hello betik alter, size kolaylık olması için doğrulamaları vardır.</span><span class="sxs-lookup"><span data-stu-id="61677-129">Never alter hello script, validations are there for your convenience.</span></span>
* <span data-ttu-id="61677-130">Hello vhd dosyasını karşıya yükleme sırasında kilitli, hello dosyasını kopyalayın veya bunu tooa yeni konum girişimi karşıya yükleyin ve yeniden taşıyın.</span><span class="sxs-lookup"><span data-stu-id="61677-130">If hello vhd file gets locked out during upload, copy hello file or move it tooa new location and attempt upload again.</span></span> <span data-ttu-id="61677-131">Karşıya yükleme engelliyor bazı Windows işlemi olabilir.</span><span class="sxs-lookup"><span data-stu-id="61677-131">There might be some Windows process that is preventing upload.</span></span>  

