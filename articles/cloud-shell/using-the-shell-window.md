---
title: "aaaUsing hello Azure bulut Kabuğu (Önizleme) penceresi | Microsoft Docs"
description: "İzlenecek yol hello Azure bulut Kabuğu penceresini açın."
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: juluk
ms.openlocfilehash: 571db3c8e177799a9e05f38a7cf8d2a4d5f8c8de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cloud-shell-window"></a><span data-ttu-id="8ec7d-103">Hello Azure bulut Kabuğu penceresini kullanma</span><span class="sxs-lookup"><span data-stu-id="8ec7d-103">Using hello Azure Cloud Shell window</span></span>

<span data-ttu-id="8ec7d-104">Bu belgede nasıl toouse hello bulut Kabuğu penceresini açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="8ec7d-104">This document explains how toouse hello Cloud Shell window.</span></span>

## <a name="concurrent-sessions"></a><span data-ttu-id="8ec7d-105">Eşzamanlı oturum</span><span class="sxs-lookup"><span data-stu-id="8ec7d-105">Concurrent sessions</span></span>
<span data-ttu-id="8ec7d-106">Bulut Kabuk her oturum tooexist ayrı bir Bash işlem olarak vererek tarayıcı sekmelerde birden fazla eşzamanlı oturum sağlar.</span><span class="sxs-lookup"><span data-stu-id="8ec7d-106">Cloud Shell enables multiple concurrent sessions across browser tabs by allowing each session tooexist as a separate Bash process.</span></span>
<span data-ttu-id="8ec7d-107">Bir oturum çıkma varsa her oturum penceresinden tooexit çalıştıkları olsa da her işlem bağımsız olarak çalışan hello aynı emin makine.</span><span class="sxs-lookup"><span data-stu-id="8ec7d-107">If exiting a session, be sure tooexit from each session window as each process runs independently although they run on hello same machine.</span></span>

## <a name="restart-cloud-shell"></a><span data-ttu-id="8ec7d-108">Bulut Kabuk yeniden başlatın</span><span class="sxs-lookup"><span data-stu-id="8ec7d-108">Restart Cloud Shell</span></span>
![](media/recycle.png)
> [!WARNING]
> <span data-ttu-id="8ec7d-109">Bulut Kabuğu'nu yeniden makine durumunu sıfırlamak ve tüm dosyaları dosyanız tarafından kalıcı olmayan paylaşımı kaybolacak.</span><span class="sxs-lookup"><span data-stu-id="8ec7d-109">Restarting Cloud Shell will reset machine state and any files not persisted by your file share will be lost.</span></span>

* <span data-ttu-id="8ec7d-110">Merhaba araç tooreceive yeni bir bulut Kabuk ortamı Hello yeniden simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8ec7d-110">Click hello restart icon on hello toolbar tooreceive a new Cloud Shell environment.</span></span>

## <a name="minimize--maximize-cloud-shell-window"></a><span data-ttu-id="8ec7d-111">Simge Durumuna Küçült & Bulut Kabuk penceresinin ekranı kaplamasını sağlayın</span><span class="sxs-lookup"><span data-stu-id="8ec7d-111">Minimize & maximize Cloud Shell window</span></span>
![](media/minmax.png)
* <span data-ttu-id="8ec7d-112">Hello tıklatın hello simgesine en aza indirmek top hello penceresi toohide sağındaki onu.</span><span class="sxs-lookup"><span data-stu-id="8ec7d-112">Click hello minimize icon on hello top right of hello window toohide it.</span></span> <span data-ttu-id="8ec7d-113">Merhaba bulut Kabuk simgesi toounhide yeniden tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8ec7d-113">Click hello Cloud Shell icon again toounhide.</span></span>
* <span data-ttu-id="8ec7d-114">Merhaba tıklatın simgesi tooset pencere toomax yüksekliği en üst düzeye çıkarın.</span><span class="sxs-lookup"><span data-stu-id="8ec7d-114">Click hello maximize icon tooset window toomax height.</span></span> <span data-ttu-id="8ec7d-115">toorestore penceresi tooprevious boyutu, geri yükleme'yi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="8ec7d-115">toorestore window tooprevious size, click restore.</span></span>

## <a name="copy-and-paste"></a><span data-ttu-id="8ec7d-116">Kopyala ve Yapıştır</span><span class="sxs-lookup"><span data-stu-id="8ec7d-116">Copy and paste</span></span>
* <span data-ttu-id="8ec7d-117">Windows: `Ctrl-insert` toocopy ve `Shift-insert` toopaste.</span><span class="sxs-lookup"><span data-stu-id="8ec7d-117">Windows: `Ctrl-insert` toocopy and `Shift-insert` toopaste.</span></span> <span data-ttu-id="8ec7d-118">Sağ açılır, kopyala/yapıştır etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8ec7d-118">Right-click dropdown can also enable copy/paste.</span></span>
  * <span data-ttu-id="8ec7d-119">FireFox/IE Pano izinleri düzgün desteklemiyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="8ec7d-119">FireFox/IE may not support clipboard permissions properly.</span></span>
* <span data-ttu-id="8ec7d-120">Mac OS: `Cmd-c` toocopy ve `Cmd-v` toopaste.</span><span class="sxs-lookup"><span data-stu-id="8ec7d-120">Mac OS: `Cmd-c` toocopy and `Cmd-v` toopaste.</span></span> <span data-ttu-id="8ec7d-121">Sağ açılır, kopyala/yapıştır etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8ec7d-121">Right-click dropdown can also enable copy/paste.</span></span>

## <a name="resize-cloud-shell-window"></a><span data-ttu-id="8ec7d-122">Bulut Kabuğu penceresini yeniden boyutlandırın</span><span class="sxs-lookup"><span data-stu-id="8ec7d-122">Resize Cloud Shell window</span></span>
* <span data-ttu-id="8ec7d-123">' I tıklatın ve yukarı veya aşağı tooresize hello bulut Kabuğu penceresini hello üst hello araç kenarını sürükleyin.</span><span class="sxs-lookup"><span data-stu-id="8ec7d-123">Click and drag hello top edge of hello toolbar up or down tooresize hello Cloud Shell window.</span></span>

## <a name="scrolling-text-display"></a><span data-ttu-id="8ec7d-124">Kayan metin görüntüleme</span><span class="sxs-lookup"><span data-stu-id="8ec7d-124">Scrolling text display</span></span>
* <span data-ttu-id="8ec7d-125">Fare veya dokunmatik toomove terminal metninizi kaydırın.</span><span class="sxs-lookup"><span data-stu-id="8ec7d-125">Scroll with your mouse or touchpad toomove terminal text.</span></span>

## <a name="exit-command"></a><span data-ttu-id="8ec7d-126">Çıkış komutu</span><span class="sxs-lookup"><span data-stu-id="8ec7d-126">Exit command</span></span>
<span data-ttu-id="8ec7d-127">Çalışan `exit` hello etkin oturum sona erer.</span><span class="sxs-lookup"><span data-stu-id="8ec7d-127">Running `exit` terminates hello active session.</span></span> <span data-ttu-id="8ec7d-128">Bu davranışı varsayılan olarak etkileşimi olmadan 20 dakika sonra gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="8ec7d-128">This behavior occurs by default after 20 minutes without interaction.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8ec7d-129">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8ec7d-129">Next steps</span></span>
[<span data-ttu-id="8ec7d-130">Bulut Kabuk hızlı başlangıç</span><span class="sxs-lookup"><span data-stu-id="8ec7d-130">Cloud Shell Quickstart</span></span>](quickstart.md)
