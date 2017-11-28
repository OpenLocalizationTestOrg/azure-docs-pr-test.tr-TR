---
title: "Azure Remoteapp'te uygulama yayımlama | Microsoft Docs"
description: "Uygulamaları ve kaynakları Azure Remoteapp'te yayımlama öğrenin."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: c7e1a2cd-8e1f-4a33-bd43-8032ec9ac952
ms.service: remoteapp
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 4565fa498dbadd0601004c73bfee5171efe1fad1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-publish-an-app-in-remoteapp"></a><span data-ttu-id="9ce63-103">Remoteapp'te uygulama yayımlama</span><span class="sxs-lookup"><span data-stu-id="9ce63-103">How to publish an app in RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="9ce63-104">Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır.</span><span class="sxs-lookup"><span data-stu-id="9ce63-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="9ce63-105">Ayrıntılı bilgi için [duyuruyu](https://go.microsoft.com/fwlink/?linkid=821148) okuyun.</span><span class="sxs-lookup"><span data-stu-id="9ce63-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="9ce63-106">RemoteApp koleksiyonunuzun oluşturduktan sonra uygulamaları veya kullanıcılarınız için kullanılabilir hale getirmek istediğiniz kaynakları yayımlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9ce63-106">After you create your RemoteApp collection, you need to publish the apps or resources that you want to make available for your users.</span></span> <span data-ttu-id="9ce63-107">Aboneliğinizle birlikte sağlanan şablon görüntüleri yalnızca birkaç uygulamaların diğer uygulamalar paylaşmak için varsayılan olarak - yayımlanan vardır, bunları yayımlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9ce63-107">The template images provided with your subscription only have a few apps published by default - to share the other apps, you need to publish them.</span></span>

> [!NOTE]
> <span data-ttu-id="9ce63-108">Bir uygulamayı güncelleştirmek gerekiyor mu?</span><span class="sxs-lookup"><span data-stu-id="9ce63-108">Do you need to update an app?</span></span> <span data-ttu-id="9ce63-109">Gerekir [görüntüden güncelleştirme](remoteapp-update.md) ilk.</span><span class="sxs-lookup"><span data-stu-id="9ce63-109">You'll need to [update the image](remoteapp-update.md) first.</span></span>
> 
> 

<span data-ttu-id="9ce63-110">Üzerinde **yayımlama** portalda sekmesini tıklatın, **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="9ce63-110">On the **Publishing** tab in the portal, click **Publish**.</span></span> <span data-ttu-id="9ce63-111">Bir uygulama şablonu görüntünüzün ekleyebilirsiniz **Başlat** menüsü veya uygulama şablonu görüntüde yüklendiği yolu sağlayın.</span><span class="sxs-lookup"><span data-stu-id="9ce63-111">You can either add an app from your template image's **Start** menu or provide the path to where the app is installed on the template image.</span></span> <span data-ttu-id="9ce63-112">Ekleme seçerseniz **Başlat** menüsünde listeden yayımlamak için uygulamayı seçin.</span><span class="sxs-lookup"><span data-stu-id="9ce63-112">If you choose to add from the **Start** menu, choose the app to publish from the list.</span></span> <span data-ttu-id="9ce63-113">Uygulama yolunu sağlamak seçerseniz, uygulama için uygulama ve yol için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="9ce63-113">If you choose to provide the path to the app, enter a name for the app and the path to the app.</span></span> <span data-ttu-id="9ce63-114">Değişkenleri yolun - Örneğin, "% systemdrive %" yerine kullanımı "c:\".</span><span class="sxs-lookup"><span data-stu-id="9ce63-114">Use variables in the path - for example, "%systemdrive%" instead of "c:\".</span></span>

> [!NOTE]
> <span data-ttu-id="9ce63-115">Uygulamanızdan eklemek istiyorsanız **Başlat** menüsünde olması gerekir *, uygulamanın eklendiğini **Başlat** şablon görüntünüze menüsü.*</span><span class="sxs-lookup"><span data-stu-id="9ce63-115">If you want to add your app from the **Start** menu, you need to have *added that app to the **Start** menu on your template image.*</span></span> <span data-ttu-id="9ce63-116">Aksi takdirde, RemoteApp yalnızca ne görürsünüz *olan* üzerinde **Başlat** menü ve kafası.</span><span class="sxs-lookup"><span data-stu-id="9ce63-116">Otherwise, RemoteApp will only see what *is* on the **Start** menu, and you will be confused.</span></span> 
> 
> <span data-ttu-id="9ce63-117">Emin olmak için uygulamanızın bulunduğu **Başlat** menüsünde bir kısayol dosya - yerleştirmeniz **.lnk** - %systemdrive%\ProgramData\Microsoft\Windows\Start Menu\Programs klasörünün içinde.</span><span class="sxs-lookup"><span data-stu-id="9ce63-117">To make sure your app is in the **Start** menu, place a shortcut file - **.lnk** - inside the %systemdrive%\ProgramData\Microsoft\Windows\Start Menu\Programs folder.</span></span>
> 
> <span data-ttu-id="9ce63-118">Uygulamaya eklemek unuttuysanız, **Başlat** şablonu oluşturduğunuzda menüsünü seçin yolu uygulamaya eklemek.</span><span class="sxs-lookup"><span data-stu-id="9ce63-118">If you forgot to add the app to the **Start** menu when you created the template, choose to add the path to the app.</span></span> <span data-ttu-id="9ce63-119">(Veya şablon görüntünüzü yeniden oluşturur ancak oldukça biraz daha fazla iş olmasıdır.)</span><span class="sxs-lookup"><span data-stu-id="9ce63-119">(Or recreate your template image, but that's quite a bit more work.)</span></span>
> 
> 

