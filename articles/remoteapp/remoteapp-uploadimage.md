---
title: "Özel görüntü Azure RemoteApp için karşıya yükleme | Microsoft Docs"
description: "Özel görüntü Azure RemoteApp için karşıya yükleme öğrenin"
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
ms.openlocfilehash: 5a235fac88d6e95ea294bda197641108acb4a09f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="upload-a-custom-image-for-azure-remoteapp"></a><span data-ttu-id="d4d0f-103">Özel görüntü Azure RemoteApp için karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="d4d0f-103">Upload a custom image for Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="d4d0f-104">Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır.</span><span class="sxs-lookup"><span data-stu-id="d4d0f-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="d4d0f-105">Ayrıntılı bilgi için [duyuruyu](https://go.microsoft.com/fwlink/?linkid=821148) okuyun.</span><span class="sxs-lookup"><span data-stu-id="d4d0f-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="d4d0f-106">Özel şablon görüntünüzü oluşturmuş veya değişikliklerle güncelleştirdiniz göre bu görüntüyü Azure RemoteApp görüntüsü kitaplığınıza karşıya gerekir.</span><span class="sxs-lookup"><span data-stu-id="d4d0f-106">Now that you have created your custom template image or have updated it with changes, you need to upload that image to your Azure RemoteApp image library.</span></span> <span data-ttu-id="d4d0f-107">Bu adımları kullanın.</span><span class="sxs-lookup"><span data-stu-id="d4d0f-107">Use these steps.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="d4d0f-108">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="d4d0f-108">Before you start</span></span>
1. <span data-ttu-id="d4d0f-109">Özel görüntünüzü karşıladığını doğrulamak [görüntü gereksinimleri](remoteapp-imagereqs.md) ve [uygulama gereksinimleri](remoteapp-appreqs.md).</span><span class="sxs-lookup"><span data-stu-id="d4d0f-109">Verify your custom image meets the [image requirements](remoteapp-imagereqs.md) and [application requirements](remoteapp-appreqs.md).</span></span>
2. <span data-ttu-id="d4d0f-110">Yükleme [Azure PowerShell Modülü](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d4d0f-110">Install the [Azure PowerShell module](/powershell/azure/overview).</span></span>

## <a name="step-by-step-on-how-to-upload-custom-image"></a><span data-ttu-id="d4d0f-111">Özel görüntü karşıya yüklemek adım adım hakkında</span><span class="sxs-lookup"><span data-stu-id="d4d0f-111">Step by step on how to upload custom image</span></span>
1. <span data-ttu-id="d4d0f-112">Azure Yönetim Portalı'nı açın ve RemoteApp sayfasına gidin.</span><span class="sxs-lookup"><span data-stu-id="d4d0f-112">Open Azure Management Portal and navigate to the RemoteApp page.</span></span>
2. <span data-ttu-id="d4d0f-113">Üzerinde **şablon görüntüleri** sekmesini tıklatın, **karşıya** sayfanın sonundaki.</span><span class="sxs-lookup"><span data-stu-id="d4d0f-113">On the **Template images** tab, click **Upload** at the bottom of the page.</span></span>
3. <span data-ttu-id="d4d0f-114">Görüntü için kolay bir ad girin ve depolama hesabı konumu belirtin.</span><span class="sxs-lookup"><span data-stu-id="d4d0f-114">Enter a friendly name for your image and specify the storage account location.</span></span> <span data-ttu-id="d4d0f-115">RemoteApp koleksiyonunuzun aynı konuma veya oluşturmak için istediğiniz bir konuma konumu olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="d4d0f-115">Ensure the location is the same location as your RemoteApp collection or a location where you want to create one.</span></span>
4. <span data-ttu-id="d4d0f-116">İstendiğinde, komut dosyasını yerel bilgisayarınıza indirin.</span><span class="sxs-lookup"><span data-stu-id="d4d0f-116">When prompted, download the script to your local PC.</span></span>
5. <span data-ttu-id="d4d0f-117">Komut parametreleri metin kutusuna panonuza kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="d4d0f-117">Copy the command parameters in the text box to your clipboard.</span></span>
6. <span data-ttu-id="d4d0f-118">Yükseltilmiş bir Windows PowerShell penceresi açın.</span><span class="sxs-lookup"><span data-stu-id="d4d0f-118">Open an elevated Windows PowerShell window.</span></span>
7. <span data-ttu-id="d4d0f-119">Yükseltilmiş Windows PowerShell penceresinden betik indirdiğiniz dizinine gidin.</span><span class="sxs-lookup"><span data-stu-id="d4d0f-119">From the elevated Windows PowerShell window, navigate to the same directory where you downloaded the script.</span></span>
8. <span data-ttu-id="d4d0f-120">Tuşuna basın ve kopyalanan komutu yapıştırın **Enter**.</span><span class="sxs-lookup"><span data-stu-id="d4d0f-120">Paste the copied command and press **Enter**.</span></span>
   
   <span data-ttu-id="d4d0f-121">Karşıya yükleme işlemi başlar ve süre ağ hızı ve görüntünün boyutuna dahil olmak üzere birçok faktöre bağlıdır</span><span class="sxs-lookup"><span data-stu-id="d4d0f-121">The upload process will begin and duration may depend on many factors including your network speed and size of the image</span></span>
9. <span data-ttu-id="d4d0f-122">Karşıya yüklemeyi ağ kesintisi veya şeyler nedeniyle gibi başarısız olursa, her zaman, başlangıcından karşıya yükleme işlemi devam edebilir.</span><span class="sxs-lookup"><span data-stu-id="d4d0f-122">If your upload does not succeed because of network interruption or things like that, you can always resume the upload process you began.</span></span> <span data-ttu-id="d4d0f-123">Karşıya yükleme sürdürmek için aynı komut satırını kullanarak yeniden komut dosyasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="d4d0f-123">To resume an upload, run the script again using the same command line.</span></span>

> [!WARNING]
> <span data-ttu-id="d4d0f-124">Hiçbir zaman karşıya yükleme komut dosyasını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="d4d0f-124">Never modify the upload script.</span></span> <span data-ttu-id="d4d0f-125">Görüntünün görüntü gereksinimleri ve uygulama gereksinimleri karşıladığından emin olmak için belirli denetimleri uygulanmamış olabilir.</span><span class="sxs-lookup"><span data-stu-id="d4d0f-125">Specific checks have been implemented to ensure that the image meets the image requirements and application requirements.</span></span>
> 
> 

## <a name="common-problems"></a><span data-ttu-id="d4d0f-126">Sık karşılaşılan sorunları</span><span class="sxs-lookup"><span data-stu-id="d4d0f-126">Common problems</span></span>
* <span data-ttu-id="d4d0f-127">Windows PowerShell, Azure PowerShell kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="d4d0f-127">Make sure you use Windows PowerShell, not Azure PowerShell.</span></span> <span data-ttu-id="d4d0f-128">Belirli modüller karşıya yükleme işlemi sırasında gerekli olduğu için Azure PowerShell modülünü yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="d4d0f-128">You need to install the Azure PowerShell module because certain modules are needed during the upload process.</span></span>
* <span data-ttu-id="d4d0f-129">Komut dosyası hiçbir zaman alter, size kolaylık olması için doğrulamaları vardır.</span><span class="sxs-lookup"><span data-stu-id="d4d0f-129">Never alter the script, validations are there for your convenience.</span></span>
* <span data-ttu-id="d4d0f-130">Vhd dosyasını karşıya yükleme sırasında kilitli, dosya kopyalama veya bunu yeni bir konum ve girişimi yüklemek üzere yeniden taşıyın.</span><span class="sxs-lookup"><span data-stu-id="d4d0f-130">If the vhd file gets locked out during upload, copy the file or move it to a new location and attempt upload again.</span></span> <span data-ttu-id="d4d0f-131">Karşıya yükleme engelliyor bazı Windows işlemi olabilir.</span><span class="sxs-lookup"><span data-stu-id="d4d0f-131">There might be some Windows process that is preventing upload.</span></span>  

