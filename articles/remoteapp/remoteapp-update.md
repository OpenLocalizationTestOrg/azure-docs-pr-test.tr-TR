---
title: aaaUpdate Azure RemoteApp koleksiyonunuzun | Microsoft Docs
description: "Bilgi nasıl tooupdate Azure RemoteApp koleksiyonunuzun"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: e553d432-e581-48fe-b996-c432357eb64a
ms.service: remoteapp
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: compute
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 849d7abfdfad4dbe6a235d2a28c71f7943eb812c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="update-a-collection-in-azure-remoteapp"></a><span data-ttu-id="2cbeb-103">Azure RemoteApp koleksiyonunda güncelleştir</span><span class="sxs-lookup"><span data-stu-id="2cbeb-103">Update a collection in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="2cbeb-104">Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır.</span><span class="sxs-lookup"><span data-stu-id="2cbeb-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="2cbeb-105">Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="2cbeb-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="2cbeb-106">Tooupdate hello uygulamaları veya görüntü Azure RemoteApp koleksiyonunuzda gerektiğinde bir zaman kaçınılmaz olarak, gelen.</span><span class="sxs-lookup"><span data-stu-id="2cbeb-106">There will come a time, inevitably, when you need tooupdate hello apps or image in your Azure RemoteApp collection.</span></span> <span data-ttu-id="2cbeb-107">Bir bulut veya karma koleksiyonunda Azure RemoteApp aboneliğiniz ile birlikte gelen hello görüntülerden birini kullanıyorsanız, tüm güncelleştirmeleri kolay tuttuğunuzda şekilde Azure RemoteApp tarafından kendisine ele alınır.</span><span class="sxs-lookup"><span data-stu-id="2cbeb-107">If you are using one of hello images included with your Azure RemoteApp subscription, in either a cloud or hybrid collection, any and all updates are handled by Azure RemoteApp itself, so you can rest easy.</span></span>

<span data-ttu-id="2cbeb-108">Ancak, özel bir görüntü (sıfırdan yerleşik veya bizim görüntülerden birini değiştirerek oluşturulan) kullanıyorsanız, hello görüntü ve uygulamaların güncelliğini sorumlu değildir.</span><span class="sxs-lookup"><span data-stu-id="2cbeb-108">However, if you are using a custom image (either that you built from scratch or that you created by modifying one of our images), you are in charge of maintaining hello image and apps.</span></span> <span data-ttu-id="2cbeb-109">Görüntünüzü ya da herhangi bir hello uygulamalar içindeki tooupdate gerekiyorsa, bu yeni güncelleştirilmiş görüntüsü ile koleksiyonunuza ', hello görüntü ve Değiştir hello mevcut görüntü yeni ve güncelleştirilmiş sürümü toocreate ihtiyacı vardır.</span><span class="sxs-lookup"><span data-stu-id="2cbeb-109">If you need tooupdate your image or any of hello apps inside it, you need toocreate a new, updated version of hello image, and then replace hello existing image in your collection with this new updated image.</span></span>

<span data-ttu-id="2cbeb-110">Bu nedenle, nasıl gittiğiniz koleksiyonunuzu güncelleştirme hakkında?</span><span class="sxs-lookup"><span data-stu-id="2cbeb-110">So, how do you go about updating your collection?</span></span> <span data-ttu-id="2cbeb-111">Bu oldukça basittir:</span><span class="sxs-lookup"><span data-stu-id="2cbeb-111">It's fairly straightforward:</span></span>

1. <span data-ttu-id="2cbeb-112">Koleksiyonunuzda kullanılan hello görüntü güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="2cbeb-112">Update hello image that you used in your collection.</span></span> <span data-ttu-id="2cbeb-113">Herhangi bir düzeltme ekleri veya gerekli güncelleştirmeleri uygulamak ve yeni bir adla kaydedin.</span><span class="sxs-lookup"><span data-stu-id="2cbeb-113">Apply any patches or updates needed, and then save it with a new name.</span></span>
2. <span data-ttu-id="2cbeb-114">[Karşıya yükleme](remoteapp-uploadimage.md) veya [alma](remoteapp-image-on-azurevm.md) bu görüntü tooRemoteApp.</span><span class="sxs-lookup"><span data-stu-id="2cbeb-114">[Upload](remoteapp-uploadimage.md) or [import](remoteapp-image-on-azurevm.md) that image tooRemoteApp.</span></span>
3. <span data-ttu-id="2cbeb-115">Şimdi, hello koleksiyonu sayfasında, tıklatın **güncelleştirme**.</span><span class="sxs-lookup"><span data-stu-id="2cbeb-115">Now, on hello collection page, click **Update**.</span></span>
4. <span data-ttu-id="2cbeb-116">Hello Hello yeni görüntü Seç **şablon görüntüsü** listesi.</span><span class="sxs-lookup"><span data-stu-id="2cbeb-116">Choose hello new image from hello **Template Image** list.</span></span>
5. <span data-ttu-id="2cbeb-117">Hello hassas bölümü İşte - toodecide nasıl gereken bir uygulamayı hello koleksiyonunda kullanmakta olduğunuz tüm kullanıcılarla toodeal.</span><span class="sxs-lookup"><span data-stu-id="2cbeb-117">Here's hello tricky part - you need toodecide how toodeal with any users that are currently using an app in hello collection.</span></span> <span data-ttu-id="2cbeb-118">Seçenekler aşağıdaki hello vardır:</span><span class="sxs-lookup"><span data-stu-id="2cbeb-118">You have hello following choices:</span></span>
   
   * <span data-ttu-id="2cbeb-119">**Kullanıcılara hello güncelleştirmeden sonra 60 dakika ver**.</span><span class="sxs-lookup"><span data-stu-id="2cbeb-119">**Give users 60 minutes after hello update**.</span></span> <span data-ttu-id="2cbeb-120">Merhaba Güncelleştirme tamamlandıktan hemen sonra Azure RemoteApp iş ve oturum kapatma ve tekrar oturum toosave söyleyen bir ileti tooany active bir kullanıcıları görüntüler.</span><span class="sxs-lookup"><span data-stu-id="2cbeb-120">As soon as hello update is finished, Azure RemoteApp will display a message tooany active users telling them toosave their work and log off and log back in.</span></span> <span data-ttu-id="2cbeb-121">60 dakika sonra kapattınız olmayan herhangi bir etkin kullanıcılar otomatik olarak oturumunuz kapatılacak.</span><span class="sxs-lookup"><span data-stu-id="2cbeb-121">After 60 minutes, any active users who have not logged off will be automatically logged off.</span></span> <span data-ttu-id="2cbeb-122">Kullanıcılar hemen oturum açın.</span><span class="sxs-lookup"><span data-stu-id="2cbeb-122">Users can immediately log back on.</span></span>
   * <span data-ttu-id="2cbeb-123">**Kullanıcıların oturumunu hemen kapat**.</span><span class="sxs-lookup"><span data-stu-id="2cbeb-123">**Sign users out immediately**.</span></span> <span data-ttu-id="2cbeb-124">Merhaba Güncelleştirme tamamlandıktan hemen sonra herhangi bir uyarı olmadan otomatik olarak tüm kullanıcıların oturumunu.</span><span class="sxs-lookup"><span data-stu-id="2cbeb-124">As soon as hello update is finished, log off all users automatically without any warning.</span></span> <span data-ttu-id="2cbeb-125">Bu seçeneği seçerseniz, kullanıcılar veri kaybedebilir.</span><span class="sxs-lookup"><span data-stu-id="2cbeb-125">If you choose this option, users might lose data.</span></span> <span data-ttu-id="2cbeb-126">Ancak, bunlar toohello uygulama hemen bağlanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2cbeb-126">However, they can reconnect toohello app immediately.</span></span>
6. <span data-ttu-id="2cbeb-127">Merhaba onay işareti toostart hello Güncelleştir'i tıklatın.</span><span class="sxs-lookup"><span data-stu-id="2cbeb-127">Click hello check mark toostart hello update.</span></span>

