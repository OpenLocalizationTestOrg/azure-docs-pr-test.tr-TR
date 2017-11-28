---
title: "aaaTroubleshoot RemoteApp bulut koleksiyonu - oluşturma | Microsoft Docs"
description: "Tootroubleshoot RemoteApp bulut koleksiyonu oluşturma hataları nasıl öğrenin"
services: remoteapp
documentationcenter: 
author: vkbucha
manager: mbaldwin
ms.assetid: 95eb7797-7b5e-4781-ad23-f15dd85b213d
ms.service: remoteapp
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 9484ecbdb048ede8df725215b313e049cc7648f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-creating-remoteapp-cloud-collections"></a><span data-ttu-id="6af88-103">RemoteApp bulut koleksiyonu oluşturma sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="6af88-103">Troubleshoot creating RemoteApp cloud collections</span></span>
> [!IMPORTANT]
> <span data-ttu-id="6af88-104">Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır.</span><span class="sxs-lookup"><span data-stu-id="6af88-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="6af88-105">Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="6af88-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="6af88-106">Bulut koleksiyonu oluşturma sorun yaşıyorsanız, aşağıdaki bilgilerle hello denetleyin.</span><span class="sxs-lookup"><span data-stu-id="6af88-106">If you are having problems creating a cloud collection, check out hello following information.</span></span>

## <a name="your-image-is-invalid"></a><span data-ttu-id="6af88-107">Görüntünüzü geçersiz</span><span class="sxs-lookup"><span data-stu-id="6af88-107">Your image is invalid</span></span>
<span data-ttu-id="6af88-108">Koleksiyonunuz için Azure tooprovision beklenirken "GoldImageInvalid" gibi bir ileti görürseniz, şablon görüntünüzü hello karşılamıyor demektir [görüntü gereksinimleri tanımlanan](remoteapp-imagereqs.md).</span><span class="sxs-lookup"><span data-stu-id="6af88-108">If you see a message like, "GoldImageInvalid" when you are waiting for Azure tooprovision your collection, it means that your template image doesn't meet hello [defined image requirements](remoteapp-imagereqs.md).</span></span> <span data-ttu-id="6af88-109">Bu nedenle, bu okuma Git [gereksinimleri](remoteapp-imagereqs.md)görüntünüzü düzeltin ve toocreate koleksiyonunuzu yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="6af88-109">So, go read those [requirements](remoteapp-imagereqs.md), fix your image, and try toocreate your collection again.</span></span>

## <a name="common-errors-seen-in-hello-azure-management-portal"></a><span data-ttu-id="6af88-110">Hello Azure Yönetim Portalı'nda görülen yaygın hatalar</span><span class="sxs-lookup"><span data-stu-id="6af88-110">Common errors seen in hello Azure Management portal</span></span>
    DNS server could not be reached
    ProvisioningTimeout

<span data-ttu-id="6af88-111">Bulut koleksiyonları genellikle hata nedeniyle, oluşturma sırasında özel resimler kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="6af88-111">Cloud collections often fail during creation because of you are using custom images.</span></span>  <span data-ttu-id="6af88-112">Hatalar yukarıda hello birine bakın ve bir özel görüntü toocreate hello koleksiyon kullanıyorsanız Lütfen şeyler aşağıdaki hello kontrol edin:</span><span class="sxs-lookup"><span data-stu-id="6af88-112">If you see one of hello above errors and you are using a custom image toocreate hello collection, please check hello following things:</span></span>

* <span data-ttu-id="6af88-113">Karşıya yüklediğiniz, hello özel görüntü görüntü gereksinimleri karşıladığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="6af88-113">Ensure that hello custom image you uploaded meets image requirements.</span></span>
* <span data-ttu-id="6af88-114">En sık hello ortak, hello görüntü düzgün Sysprep uygulanmış değildi sorunudur.</span><span class="sxs-lookup"><span data-stu-id="6af88-114">Most often hello common problem is that hello image was not properly syspreped.</span></span>  
* <span data-ttu-id="6af88-115">Doğrulama hello görüntü önyükleme Hyper-V içinde veya bir IAAS VM hello görüntüsünü kullanarak doğrudan Azure aboneliğinizde oluşturmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="6af88-115">Verify hello image can boot within Hyper-V or try creating an IAAS VM directly in your Azure subscription using hello image.</span></span> <span data-ttu-id="6af88-116">Merhaba VM tooboot ve başlatılmamasına başarısız olursa, bu genellikle, hello özel görüntü düzgün hazırlanmadı belirtir.</span><span class="sxs-lookup"><span data-stu-id="6af88-116">If hello VM fails tooboot and not start, then this usually indicates that hello custom image was not prepared correctly.</span></span>  <span data-ttu-id="6af88-117">Merhaba özel görüntü hello nasıl toocreate özel bir şablon görüntü RemoteApp için oluşturulmuş doğrulayın</span><span class="sxs-lookup"><span data-stu-id="6af88-117">Verify hello custom image was built following hello How toocreate a custom template image for RemoteApp</span></span>

<span data-ttu-id="6af88-118">Aboneliğinizde yer alan hello Microsoft görüntülerden birini kullanıyorsanız, toocreate hello koleksiyonu yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="6af88-118">If you are using one of hello Microsoft images included with your subscription, try toocreate hello collection again.</span></span> <span data-ttu-id="6af88-119">Merhaba sorun devam ederse lütfen Microsoft Destek'e başvurun.</span><span class="sxs-lookup"><span data-stu-id="6af88-119">If hello issue persists then please contact Microsoft support.</span></span>

    PlatformImageTrialModeOnly

<span data-ttu-id="6af88-120">Bu hatayı görürseniz, bu genellikle anlamına gelir, yükseltilmiş tooa Ücretli hesap ancak toouse yalnızca hello deneme modunda hello hizmetinin geçerli bir Microsoft sağlanan görüntüsü çalışıyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="6af88-120">If you see this error this usually means that you been upgraded tooa paid account but you are trying toouse a Microsoft provided image that is valid only during hello trial mode of hello service.</span></span> <span data-ttu-id="6af88-121">Bu durumda, toocreate bulut koleksiyonu yeniden deneyin, ancak emin toospecify hello doğru görüntüyü olabilir.</span><span class="sxs-lookup"><span data-stu-id="6af88-121">In this case, try toocreate your cloud collection again, but be sure toospecify hello correct image.</span></span>

