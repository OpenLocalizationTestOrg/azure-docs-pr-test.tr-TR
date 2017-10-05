---
title: "Azure RemoteApp görüntü gereksinimleri | Microsoft Docs"
description: "Azure RemoteApp ile kullanılacak görüntüleri oluşturmak için gereksinimleri hakkında bilgi edinin"
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
ms.openlocfilehash: 75b0f8d6b25a80f11002b683152cfb294cbb68bd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="requirements-for-azure-remoteapp-images"></a><span data-ttu-id="8013a-103">Azure RemoteApp görüntüleri için gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="8013a-103">Requirements for Azure RemoteApp images</span></span>
> [!IMPORTANT]
> <span data-ttu-id="8013a-104">Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır.</span><span class="sxs-lookup"><span data-stu-id="8013a-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="8013a-105">Ayrıntılı bilgi için [duyuruyu](https://go.microsoft.com/fwlink/?linkid=821148) okuyun.</span><span class="sxs-lookup"><span data-stu-id="8013a-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="8013a-106">Azure RemoteApp, kullanıcılarınız ile paylaşmak istediğiniz tüm programlar barındırmak için bir Windows Server 2012 R2 görüntüsünü kullanır.</span><span class="sxs-lookup"><span data-stu-id="8013a-106">Azure RemoteApp uses a Windows Server 2012 R2 image to host all the programs that you want to share with your users.</span></span> <span data-ttu-id="8013a-107">Özel bir görüntü oluşturmak için varolan bir görüntüyle başlatabilirsiniz veya [yeni bir tane oluşturun](remoteapp-create-custom-image.md).</span><span class="sxs-lookup"><span data-stu-id="8013a-107">To create a custom image, you can start with an existing image or [create a new one](remoteapp-create-custom-image.md).</span></span>

> [!TIP]
> <span data-ttu-id="8013a-108">Azure RemoteApp aboneliğiniz Windows Server 2012 R2 görüntüsünü kendi şablon görüntüsü oluşturmak için kullanabilirsiniz Azure VM galerisinde erişmenizi olduğunu biliyor muydunuz?</span><span class="sxs-lookup"><span data-stu-id="8013a-108">Did you know that your Azure RemoteApp subscription gives you access to a Windows Server 2012 R2 image in the Azure VM gallery that you can use to create your own template image?</span></span> <span data-ttu-id="8013a-109">[Kullanıma](remoteapp-image-on-azurevm.md).</span><span class="sxs-lookup"><span data-stu-id="8013a-109">[Check it out](remoteapp-image-on-azurevm.md).</span></span>  
> 
> 

<span data-ttu-id="8013a-110">Azure RemoteApp ile kullanılmak üzere yüklenen görüntü için gereksinimleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="8013a-110">The requirements for the image that can be uploaded for use with Azure RemoteApp are:</span></span>

* <span data-ttu-id="8013a-111">Özel uygulamalar veri görüntüde yerel olarak depolamayın.</span><span class="sxs-lookup"><span data-stu-id="8013a-111">Custom applications don’t store data locally on the image.</span></span> <span data-ttu-id="8013a-112">Bu görüntüler, durum bilgisiz ve uygulamalar yalnızca içermelidir.</span><span class="sxs-lookup"><span data-stu-id="8013a-112">These images are stateless and should only contain applications.</span></span>
* <span data-ttu-id="8013a-113">Görüntü kaybedilen veri içermiyor.</span><span class="sxs-lookup"><span data-stu-id="8013a-113">The image does not contain data that can be lost.</span></span>
* <span data-ttu-id="8013a-114">Görüntü boyutu, MB katları olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8013a-114">The image size should be a multiple of MBs.</span></span> <span data-ttu-id="8013a-115">Tam katı değil görüntüyü karşıya yüklemeye karşıya yükleme başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="8013a-115">If you try to upload an image that is not an exact multiple, the upload will fail.</span></span>
* <span data-ttu-id="8013a-116">Görüntü boyutu 127 GB olmalıdır ya da daha küçük.</span><span class="sxs-lookup"><span data-stu-id="8013a-116">The image size must be 127 GB or smaller.</span></span>
* <span data-ttu-id="8013a-117">Bir VHD dosyası üzerinde olmalıdır (VHDX dosyaları şu anda desteklenmiyor).</span><span class="sxs-lookup"><span data-stu-id="8013a-117">It must be on a VHD file (VHDX files are not currently supported).</span></span>
* <span data-ttu-id="8013a-118">2. nesil sanal makine VHD olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="8013a-118">The VHD must not be a generation 2 virtual machine.</span></span>
* <span data-ttu-id="8013a-119">VHD'yi sabit boyutlu veya dinamik olarak genişletilen olabilir.</span><span class="sxs-lookup"><span data-stu-id="8013a-119">The VHD can be either fixed-size or dynamically expanding.</span></span> <span data-ttu-id="8013a-120">Azure için bir sabit boyutlu VHD dosyasının karşıya yüklemek için daha az zaman alır çünkü dinamik olarak genişleyen bir VHD önerilir.</span><span class="sxs-lookup"><span data-stu-id="8013a-120">A dynamically expanding VHD is recommended because it takes less time to upload to Azure than a fixed-size VHD file.</span></span>
* <span data-ttu-id="8013a-121">Disk bölümleme stilini ana önyükleme kaydı (MBR) kullanarak başlatılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8013a-121">The disk must be initialized using the Master Boot Record (MBR) partitioning style.</span></span> <span data-ttu-id="8013a-122">GUID bölümleme tablosu (GPT) bölümleme stilini desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="8013a-122">The GUID partition table (GPT) partition style is not supported.</span></span>
* <span data-ttu-id="8013a-123">VHD'yi tek bir Windows Server 2012 R2 yüklemesini içermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="8013a-123">The VHD must contain a single installation of Windows Server 2012 R2.</span></span> <span data-ttu-id="8013a-124">Windows yüklemesini içeren birden çok birim, ancak yalnızca bir içerebilir.</span><span class="sxs-lookup"><span data-stu-id="8013a-124">It can contain multiple volumes, but only one that contains an installation of Windows.</span></span>
* <span data-ttu-id="8013a-125">Uzak Masaüstü oturumu ana bilgisayarı (RDSH) rolü ve Masaüstü Deneyimi özelliği yüklü olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8013a-125">The Remote Desktop Session Host (RDSH) role and the Desktop Experience feature must be installed.</span></span>
* <span data-ttu-id="8013a-126">Uzak Masaüstü Bağlantı Aracısı rol gerekir *değil* yüklü olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8013a-126">The Remote Desktop Connection Broker role must *not* be installed.</span></span>
* <span data-ttu-id="8013a-127">Şifreleme Dosya Sistemi (EFS) devre dışı bırakılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8013a-127">The Encrypting File System (EFS) must be disabled.</span></span>
* <span data-ttu-id="8013a-128">Resmin parametrelerini kullanarak bir Sysprep uygulanmış olması gerekir **/oobe / generalize/shutdown** (vermeyin kullanım **/mode:vm** parametresi).</span><span class="sxs-lookup"><span data-stu-id="8013a-128">The image must be SYSPREPed using the parameters **/oobe /generalize /shutdown** (DO NOT use the **/mode:vm** parameter).</span></span>
* <span data-ttu-id="8013a-129">Bir anlık görüntü zinciri, VHD'den karşıya yükleme desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="8013a-129">Uploading your VHD from a snapshot chain is not supported.</span></span>

<span data-ttu-id="8013a-130">Bkz: [Azure RemoteApp görüntüsü oluşturma](remoteapp-imageoptions.md) Azure RemoteApp için görüntüleri oluşturma hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="8013a-130">See [Create an Azure RemoteApp image](remoteapp-imageoptions.md) for more information about creating images for Azure RemoteApp.</span></span>

