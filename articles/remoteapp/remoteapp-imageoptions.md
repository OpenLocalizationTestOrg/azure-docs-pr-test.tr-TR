---
title: "Azure RemoteApp görüntüsü aaaCreate | Microsoft Docs"
description: "Azure RemoteApp için görüntüleri oluşturmak için kullanılabilen hello seçenekleri hakkında bilgi edinin"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: cb0f9424-6185-45a1-abe9-c23f1edf34f2
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 54e63b6fa13addfcda96ce581910e1ac48d91e70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-remoteapp-image"></a><span data-ttu-id="fa02f-103">Azure RemoteApp görüntüsü oluşturma</span><span class="sxs-lookup"><span data-stu-id="fa02f-103">Create an Azure RemoteApp image</span></span>
> [!IMPORTANT]
> <span data-ttu-id="fa02f-104">Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır.</span><span class="sxs-lookup"><span data-stu-id="fa02f-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="fa02f-105">Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="fa02f-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="fa02f-106">Azure RemoteApp Kullanıcılarınızla paylaşabilirsiniz görüntüleri toohold hello uygulamaları kullanır.</span><span class="sxs-lookup"><span data-stu-id="fa02f-106">Azure RemoteApp uses images toohold hello apps that you share with your users.</span></span> <span data-ttu-id="fa02f-107">(Biz görüntünüzü alın ve bunu Azure RemoteApp oturum açtığınızda ne hello kullanıcıların erişimi kullanıcının toocreate VM'ler - kullanın.) Bulut veya karma, olup toocreate uygulamaların tercih ettiğiniz ile bir Azure RemoteApp koleksiyonu, yüklü Bu uygulamalarla görüntü oluşturmaya başlayın.</span><span class="sxs-lookup"><span data-stu-id="fa02f-107">(We take your image and use it toocreate VMs - that's what hello users access when they sign into Azure RemoteApp.) toocreate an Azure RemoteApp collection with your choice of applications, whether it is cloud or hybrid, you  start by creating an image with those applications installed.</span></span> <span data-ttu-id="fa02f-108">Ardından, bu görüntüyü kullanan bir koleksiyon oluşturun, toohello koleksiyonu kullanıcılar atayın ve uygulamaları toothose kullanıcılar yayımlama.</span><span class="sxs-lookup"><span data-stu-id="fa02f-108">Then, create a collection that uses that image, assign users toohello collection, and publish apps toothose users.</span></span>

<span data-ttu-id="fa02f-109">Oluşturma veya görüntüleri kullanmak için birkaç seçeneğiniz vardır.</span><span class="sxs-lookup"><span data-stu-id="fa02f-109">You have several options for creating or using images.</span></span> <span data-ttu-id="fa02f-110">Merhaba temel [gereksinim](remoteapp-imagereqs.md) için görüntüyü Windows Server 2012 R2 çalıştıran ve hello Uzak Masaüstü oturumu ana bilgisayarı (RDSH) rolü yüklü olması.</span><span class="sxs-lookup"><span data-stu-id="fa02f-110">hello basic [requirement](remoteapp-imagereqs.md) for an image is that it run Windows Server 2012 R2 and have hello Remote Desktop Session Host (RDSH) role installed.</span></span> <span data-ttu-id="fa02f-111">Size nasıl şeyler ilginç nereden olur.</span><span class="sxs-lookup"><span data-stu-id="fa02f-111">How you get that is where things get interesting.</span></span>

<span data-ttu-id="fa02f-112">Tooimages geldiğinde seçenekleri aşağıdaki hello vardır:</span><span class="sxs-lookup"><span data-stu-id="fa02f-112">You have hello following options when it comes tooimages:</span></span>

* <span data-ttu-id="fa02f-113">İçeri aktarma ve kullanabileceğiniz bir [görüntünün temel bir Azure sanal makinede](remoteapp-image-on-azurevm.md).</span><span class="sxs-lookup"><span data-stu-id="fa02f-113">You can import and use an [image based on an Azure virtual machine](remoteapp-image-on-azurevm.md).</span></span> <span data-ttu-id="fa02f-114">Bu, özel ayarlar gerektiren satır iş kolu uygulamaları için uygundur.</span><span class="sxs-lookup"><span data-stu-id="fa02f-114">This is good for line-of-business apps that require custom settings.</span></span> <span data-ttu-id="fa02f-115">Merhaba görüntü toowork hello uygulama için özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fa02f-115">You can customize hello image toowork for hello app.</span></span>
* <span data-ttu-id="fa02f-116">Yapabilecekleriniz [özel bir görüntü oluşturup](remoteapp-create-custom-image.md).</span><span class="sxs-lookup"><span data-stu-id="fa02f-116">You can [create and upload a custom image](remoteapp-create-custom-image.md).</span></span> <span data-ttu-id="fa02f-117">Şirket içi Uzak Masaüstü Hizmetleri dağıtımınız için kullandığınız bir görüntü zaten varsa bu kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="fa02f-117">This is good if you already have an image that you use for your on-premises Remote Desktop Services deployment.</span></span>
* <span data-ttu-id="fa02f-118">Merhaba birini kullanabilirsiniz [şablon görüntüleri](remoteapp-images.md) RemoteApp aboneliğinize dahil.</span><span class="sxs-lookup"><span data-stu-id="fa02f-118">You can use one of hello [template images](remoteapp-images.md) included in your RemoteApp subscription.</span></span> <span data-ttu-id="fa02f-119">Bu görüntüleri oluşturulur ve hello RemoteApp ekibi tarafından korunan ve bazı standart uygulama kullanılabilir tooyour kullanıcılar yapabilir (gibi hello Office suite) içerir.</span><span class="sxs-lookup"><span data-stu-id="fa02f-119">These images are created and maintained by hello RemoteApp team and contain some standard applications (like hello Office suite) that you can make available tooyour users.</span></span> <span data-ttu-id="fa02f-120">Yalnızca bu hello Office 365 Pro Plus görüntüyü bir üretim ortamında kullanılabileceğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="fa02f-120">Note that only hello Office 365 Pro Plus image can be used in a production setting.</span></span>

<span data-ttu-id="fa02f-121">Görüntünüzü nereden veya oluşturduğunuz nasıl bağımsız olarak toomake hello anladığınızdan emin isteyeceksiniz [uygulama gereksinimleri](remoteapp-appreqs.md) iyi Remoteapp'te uygulamanızı çalışır tooensure.</span><span class="sxs-lookup"><span data-stu-id="fa02f-121">Regardless of where you get your image or how you create it, you'll want toomake sure you understand hello [app requirements](remoteapp-appreqs.md) tooensure that your app works well in RemoteApp.</span></span> <span data-ttu-id="fa02f-122">Ardından, hello sonraki toocreate adımdır bir [bulut](remoteapp-create-cloud-deployment.md) veya [karma](remoteapp-create-hybrid-deployment.md) koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="fa02f-122">Then, hello next step is toocreate a [cloud](remoteapp-create-cloud-deployment.md) or [hybrid](remoteapp-create-hybrid-deployment.md) collection.</span></span>

