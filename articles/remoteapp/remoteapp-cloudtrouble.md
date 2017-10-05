---
title: "RemoteApp bulut koleksiyonu - oluşturma sorunlarını giderme | Microsoft Docs"
description: "RemoteApp bulut koleksiyonu oluşturma hatalarını giderme öğrenin"
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
ms.openlocfilehash: 304ba7c5057b27c459bccbb75d3a711567757675
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-creating-remoteapp-cloud-collections"></a><span data-ttu-id="5d672-103">RemoteApp bulut koleksiyonu oluşturma sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="5d672-103">Troubleshoot creating RemoteApp cloud collections</span></span>
> [!IMPORTANT]
> <span data-ttu-id="5d672-104">Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır.</span><span class="sxs-lookup"><span data-stu-id="5d672-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="5d672-105">Ayrıntılı bilgi için [duyuruyu](https://go.microsoft.com/fwlink/?linkid=821148) okuyun.</span><span class="sxs-lookup"><span data-stu-id="5d672-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="5d672-106">Bulut koleksiyonu oluşturma sorun yaşıyorsanız, aşağıdaki bilgileri kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="5d672-106">If you are having problems creating a cloud collection, check out the following information.</span></span>

## <a name="your-image-is-invalid"></a><span data-ttu-id="5d672-107">Görüntünüzü geçersiz</span><span class="sxs-lookup"><span data-stu-id="5d672-107">Your image is invalid</span></span>
<span data-ttu-id="5d672-108">Koleksiyonunuz sağlamak Azure için beklenirken "GoldImageInvalid" gibi bir ileti görürseniz, şablon görüntünüzü karşılamıyor demektir [görüntü gereksinimleri tanımlanan](remoteapp-imagereqs.md).</span><span class="sxs-lookup"><span data-stu-id="5d672-108">If you see a message like, "GoldImageInvalid" when you are waiting for Azure to provision your collection, it means that your template image doesn't meet the [defined image requirements](remoteapp-imagereqs.md).</span></span> <span data-ttu-id="5d672-109">Bu nedenle, bu okuma Git [gereksinimleri](remoteapp-imagereqs.md)görüntünüzü düzeltin ve koleksiyonunuzu yeniden oluşturmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="5d672-109">So, go read those [requirements](remoteapp-imagereqs.md), fix your image, and try to create your collection again.</span></span>

## <a name="common-errors-seen-in-the-azure-management-portal"></a><span data-ttu-id="5d672-110">Azure Yönetim Portalı'nda görülen yaygın hatalar</span><span class="sxs-lookup"><span data-stu-id="5d672-110">Common errors seen in the Azure Management portal</span></span>
    DNS server could not be reached
    ProvisioningTimeout

<span data-ttu-id="5d672-111">Bulut koleksiyonları genellikle hata nedeniyle, oluşturma sırasında özel resimler kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="5d672-111">Cloud collections often fail during creation because of you are using custom images.</span></span>  <span data-ttu-id="5d672-112">Yukarıdaki hatalar birine bakın ve o koleksiyonu oluşturmak için özel bir görüntü kullanıyorsanız, lütfen şunları kontrol edin:</span><span class="sxs-lookup"><span data-stu-id="5d672-112">If you see one of the above errors and you are using a custom image to create the collection, please check the following things:</span></span>

* <span data-ttu-id="5d672-113">Karşıya yüklediğiniz özel görüntü görüntü gereksinimleri karşıladığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="5d672-113">Ensure that the custom image you uploaded meets image requirements.</span></span>
* <span data-ttu-id="5d672-114">En sık sık karşılaşılan görüntünün doğru Sysprep uygulanmış olmadığını sorundur.</span><span class="sxs-lookup"><span data-stu-id="5d672-114">Most often the common problem is that the image was not properly syspreped.</span></span>  
* <span data-ttu-id="5d672-115">Doğrulama görüntü önyükleme Hyper-V içinde veya bir IAAS VM görüntüsünü kullanarak doğrudan Azure aboneliğinizde oluşturmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="5d672-115">Verify the image can boot within Hyper-V or try creating an IAAS VM directly in your Azure subscription using the image.</span></span> <span data-ttu-id="5d672-116">Önyükleme ve değil başlatmak VM başarısız olursa, bu genellikle özel görüntü düzgün hazırlanmadı belirtir.</span><span class="sxs-lookup"><span data-stu-id="5d672-116">If the VM fails to boot and not start, then this usually indicates that the custom image was not prepared correctly.</span></span>  <span data-ttu-id="5d672-117">Özel görüntü nasıl aşağıdaki yapılmış doğrulayın RemoteApp için bir özel şablon görüntüsü oluşturmak için</span><span class="sxs-lookup"><span data-stu-id="5d672-117">Verify the custom image was built following the How to create a custom template image for RemoteApp</span></span>

<span data-ttu-id="5d672-118">Aboneliğinizde yer alan Microsoft görüntülerden birini kullanıyorsanız, koleksiyonu yeniden oluşturmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="5d672-118">If you are using one of the Microsoft images included with your subscription, try to create the collection again.</span></span> <span data-ttu-id="5d672-119">Sorun devam ederse lütfen Microsoft Destek'e başvurun.</span><span class="sxs-lookup"><span data-stu-id="5d672-119">If the issue persists then please contact Microsoft support.</span></span>

    PlatformImageTrialModeOnly

<span data-ttu-id="5d672-120">Bu hatayı görürseniz, bu genellikle anlamına gelir, ücretli bir hesabınız yükseltilmiş ancak yalnızca hizmetini deneme modunda geçerli bir Microsoft sağlanan görüntüsü kullanmaya çalışıyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="5d672-120">If you see this error this usually means that you been upgraded to a paid account but you are trying to use a Microsoft provided image that is valid only during the trial mode of the service.</span></span> <span data-ttu-id="5d672-121">Bu durumda, bulut koleksiyonu yeniden oluşturun, ancak doğru görüntüyü belirttiğinizden emin olun deneyin.</span><span class="sxs-lookup"><span data-stu-id="5d672-121">In this case, try to create your cloud collection again, but be sure to specify the correct image.</span></span>

