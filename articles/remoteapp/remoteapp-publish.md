---
title: "bir uygulamayı Azure RemoteApp aaaPublish | Microsoft Docs"
description: "Bilgi nasıl toopublish uygulamaları ve kaynakları Azure remoteapp'te."
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
ms.openlocfilehash: d7d92187e9ed999ac79554c9bb61f56a8eceeb31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toopublish-an-app-in-remoteapp"></a><span data-ttu-id="c505f-103">Nasıl toopublish remoteapp'te uygulama</span><span class="sxs-lookup"><span data-stu-id="c505f-103">How toopublish an app in RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="c505f-104">Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır.</span><span class="sxs-lookup"><span data-stu-id="c505f-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="c505f-105">Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="c505f-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="c505f-106">RemoteApp koleksiyonunuzun oluşturduktan sonra toopublish hello uygulamaları veya kullanıcılarınız için kullanılabilir toomake istediğiniz kaynakları gerekir.</span><span class="sxs-lookup"><span data-stu-id="c505f-106">After you create your RemoteApp collection, you need toopublish hello apps or resources that you want toomake available for your users.</span></span> <span data-ttu-id="c505f-107">Merhaba, aboneliğiniz ile sağlanan şablon görüntüleri yalnızca birkaç uygulamalara sahip varsayılan olarak - yayımlanan tooshare Merhaba diğer uygulamalar, toopublish ihtiyacınız bunları.</span><span class="sxs-lookup"><span data-stu-id="c505f-107">hello template images provided with your subscription only have a few apps published by default - tooshare hello other apps, you need toopublish them.</span></span>

> [!NOTE]
> <span data-ttu-id="c505f-108">Tooupdate bir uygulama gerekiyor mu?</span><span class="sxs-lookup"><span data-stu-id="c505f-108">Do you need tooupdate an app?</span></span> <span data-ttu-id="c505f-109">Çok gerekir[güncelleştirme hello resmi](remoteapp-update.md) ilk.</span><span class="sxs-lookup"><span data-stu-id="c505f-109">You'll need too[update hello image](remoteapp-update.md) first.</span></span>
> 
> 

<span data-ttu-id="c505f-110">Merhaba üzerinde **yayımlama** hello Portalı'nda sekmesini tıklatın, **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="c505f-110">On hello **Publishing** tab in hello portal, click **Publish**.</span></span> <span data-ttu-id="c505f-111">Bir uygulama şablonu görüntünüzün ekleyebilirsiniz **Başlat** menüsü veya hello yolu toowhere hello uygulama hello şablon görüntüsü üzerinde yüklü sağlayın.</span><span class="sxs-lookup"><span data-stu-id="c505f-111">You can either add an app from your template image's **Start** menu or provide hello path toowhere hello app is installed on hello template image.</span></span> <span data-ttu-id="c505f-112">Hello tooadd seçerseniz **Başlat** menüsünde hello uygulama toopublish hello listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="c505f-112">If you choose tooadd from hello **Start** menu, choose hello app toopublish from hello list.</span></span> <span data-ttu-id="c505f-113">Tooprovide hello yolu toohello uygulama seçerseniz, hello uygulaması ve hello yolu toohello uygulaması için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="c505f-113">If you choose tooprovide hello path toohello app, enter a name for hello app and hello path toohello app.</span></span> <span data-ttu-id="c505f-114">Değişkenleri hello yolun - Örneğin, "% systemdrive %" yerine kullanımı "c:\".</span><span class="sxs-lookup"><span data-stu-id="c505f-114">Use variables in hello path - for example, "%systemdrive%" instead of "c:\".</span></span>

> [!NOTE]
> <span data-ttu-id="c505f-115">Hello uygulamanızdan tooadd istiyorsanız **Başlat** menüsünde toohave ihtiyacınız *o uygulama toohello eklenen **Başlat** şablon görüntünüze menüsü.*</span><span class="sxs-lookup"><span data-stu-id="c505f-115">If you want tooadd your app from hello **Start** menu, you need toohave *added that app toohello **Start** menu on your template image.*</span></span> <span data-ttu-id="c505f-116">Aksi takdirde, RemoteApp yalnızca ne görürsünüz *olan* hello üzerinde **Başlat** menü ve kafası.</span><span class="sxs-lookup"><span data-stu-id="c505f-116">Otherwise, RemoteApp will only see what *is* on hello **Start** menu, and you will be confused.</span></span> 
> 
> <span data-ttu-id="c505f-117">toomake emin uygulamanızı olduğu hello **Başlat** menüsünde bir kısayol dosya - yerleştirmeniz **.lnk** - hello %systemdrive%\ProgramData\Microsoft\Windows\Start Menu\Programs klasörünün içinde.</span><span class="sxs-lookup"><span data-stu-id="c505f-117">toomake sure your app is in hello **Start** menu, place a shortcut file - **.lnk** - inside hello %systemdrive%\ProgramData\Microsoft\Windows\Start Menu\Programs folder.</span></span>
> 
> <span data-ttu-id="c505f-118">Tooadd hello uygulama toohello unuttuysanız, **Başlat** hello şablonu oluşturduğunuzda menü tooadd hello yolu toohello uygulama seçin.</span><span class="sxs-lookup"><span data-stu-id="c505f-118">If you forgot tooadd hello app toohello **Start** menu when you created hello template, choose tooadd hello path toohello app.</span></span> <span data-ttu-id="c505f-119">(Veya şablon görüntünüzü yeniden oluşturur ancak oldukça biraz daha fazla iş olmasıdır.)</span><span class="sxs-lookup"><span data-stu-id="c505f-119">(Or recreate your template image, but that's quite a bit more work.)</span></span>
> 
> 

