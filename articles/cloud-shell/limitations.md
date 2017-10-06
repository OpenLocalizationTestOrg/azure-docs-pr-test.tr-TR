---
title: "aaaAzure bulut Kabuğu (Önizleme) kısıtlamaları | Microsoft Docs"
description: "Azure bulut Kabuk sınırlamaları genel bakış"
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
ms.date: 08/21/2017
ms.author: juluk
ms.openlocfilehash: 8462b0b9850fcde790a386433009439bbab52c0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="limitations-of-azure-cloud-shell"></a><span data-ttu-id="0fcf2-103">Azure bulut Kabuk sınırlamaları</span><span class="sxs-lookup"><span data-stu-id="0fcf2-103">Limitations of Azure Cloud Shell</span></span>
<span data-ttu-id="0fcf2-104">Azure bulut Kabuk hello aşağıdaki bilinen sınırlamalara sahiptir:</span><span class="sxs-lookup"><span data-stu-id="0fcf2-104">Azure Cloud Shell has hello following known limitations:</span></span>

## <a name="system-state-and-persistence"></a><span data-ttu-id="0fcf2-105">Sistem durumu ve sürdürme</span><span class="sxs-lookup"><span data-stu-id="0fcf2-105">System state and persistence</span></span>
<span data-ttu-id="0fcf2-106">Bulut Kabuk oturumunuz sağlar hello makine geçicidir ve oturumunuz için 20 dakika etkin değil sonra geri dönüştürüldüğünde.</span><span class="sxs-lookup"><span data-stu-id="0fcf2-106">hello machine that provides your Cloud Shell session is temporary, and it is recycled after your session is inactive for 20 minutes.</span></span> <span data-ttu-id="0fcf2-107">Bulut Kabuk takılı bir dosya paylaşımı toobe gerektirir.</span><span class="sxs-lookup"><span data-stu-id="0fcf2-107">Cloud Shell requires a file share toobe mounted.</span></span> <span data-ttu-id="0fcf2-108">Sonuç olarak, aboneliğiniz depolama kaynakları tooaccess bulut Kabuk yukarı mümkün tooset olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="0fcf2-108">As a result, your subscription must be able tooset up storage resources tooaccess Cloud Shell.</span></span> <span data-ttu-id="0fcf2-109">Diğer konular şunlardır:</span><span class="sxs-lookup"><span data-stu-id="0fcf2-109">Other considerations include:</span></span>
* <span data-ttu-id="0fcf2-110">Takılı depolamayla yalnızca değişiklikleri içinde `$Home` dizin veya `clouddrive` dizin kaldı.</span><span class="sxs-lookup"><span data-stu-id="0fcf2-110">With mounted storage, only modifications within your `$Home` directory or `clouddrive` directory are persisted.</span></span>
* <span data-ttu-id="0fcf2-111">Dosya paylaşımları takılı yalnızca içinden, [bölgeye atanan](persisting-shell-storage.md#mount-a-new-clouddrive).</span><span class="sxs-lookup"><span data-stu-id="0fcf2-111">File shares can be mounted only from within your [assigned region](persisting-shell-storage.md#mount-a-new-clouddrive).</span></span>
* <span data-ttu-id="0fcf2-112">Azure dosyaları yalnızca yerel olarak yedekli depolama ve coğrafi olarak yedekli depolama hesaplarını destekler.</span><span class="sxs-lookup"><span data-stu-id="0fcf2-112">Azure Files supports only locally redundant storage and geo-redundant storage accounts.</span></span>

## <a name="user-permissions"></a><span data-ttu-id="0fcf2-113">Kullanıcı izinleri</span><span class="sxs-lookup"><span data-stu-id="0fcf2-113">User permissions</span></span>
<span data-ttu-id="0fcf2-114">İzinler, sudo erişimi olmadan normal kullanıcı olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="0fcf2-114">Permissions are set as regular users without sudo access.</span></span> <span data-ttu-id="0fcf2-115">Dışında herhangi bir yüklemesi, `$Home` dizin kalıcı olarak tutmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="0fcf2-115">Any installation outside your `$Home` directory will not persist.</span></span>
<span data-ttu-id="0fcf2-116">İçinde bazı komutlar hello rağmen `clouddrive` gibi dizin `git clone`, uygun izinlere sahip değilsiniz, `$Home` dizin izinlere sahiptir.</span><span class="sxs-lookup"><span data-stu-id="0fcf2-116">Although certain commands within hello `clouddrive` directory, such as `git clone`, do not have proper permissions, your `$Home` directory does have permissions.</span></span>

## <a name="browser-support"></a><span data-ttu-id="0fcf2-117">Tarayıcı desteği</span><span class="sxs-lookup"><span data-stu-id="0fcf2-117">Browser support</span></span>
<span data-ttu-id="0fcf2-118">Bulut Kabuğu'nu Microsoft Edge, Microsoft Internet Explorer, Google Chrome, Mozilla Firefox ve Apple Safari hello en son sürümlerini destekler.</span><span class="sxs-lookup"><span data-stu-id="0fcf2-118">Cloud Shell supports hello latest versions of Microsoft Edge, Microsoft Internet Explorer, Google Chrome, Mozilla Firefox, and Apple Safari.</span></span> <span data-ttu-id="0fcf2-119">Safari özel modunda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="0fcf2-119">Safari in private mode is not supported.</span></span>

## <a name="copy-and-paste"></a><span data-ttu-id="0fcf2-120">Kopyala ve Yapıştır</span><span class="sxs-lookup"><span data-stu-id="0fcf2-120">Copy and paste</span></span>
<span data-ttu-id="0fcf2-121">CTRL + C ve Ctrl + V kopyalayıp kısayolları bulut Kabuğu'nda Windows makinelerde yapıştırın, Ctrl + INSERT ve üst karakter + INSERT toocopy kullanın ve sırasıyla yapıştırmak gibi çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="0fcf2-121">Ctrl+C and Ctrl+V do not function as copy/paste shortcuts in Cloud Shell on Windows machines, use Ctrl+Insert and Shift+Insert toocopy and paste respectively.</span></span>

<span data-ttu-id="0fcf2-122">Sağ tıklama Kopyala ve Yapıştır seçeneklerini de kullanılabilir, ancak konu toobrowser özgü Pano erişim sağ işlevdir.</span><span class="sxs-lookup"><span data-stu-id="0fcf2-122">Right-click copy-and-paste options are also available, but right-click function is subject toobrowser-specific clipboard access.</span></span>

## <a name="editing-bashrc"></a><span data-ttu-id="0fcf2-123">.Bashrc düzenleme</span><span class="sxs-lookup"><span data-stu-id="0fcf2-123">Editing .bashrc</span></span>
<span data-ttu-id="0fcf2-124">Bunun yapılması .bashrc düzenleme beklenmeyen hatalara bulut Kabuğu'nda neden olabilir. uyarı alın.</span><span class="sxs-lookup"><span data-stu-id="0fcf2-124">Take caution when editing .bashrc, doing so can cause unexpected errors in Cloud Shell.</span></span>

## <a name="bashhistory"></a><span data-ttu-id="0fcf2-125">.bash_history</span><span class="sxs-lookup"><span data-stu-id="0fcf2-125">.bash_history</span></span>
<span data-ttu-id="0fcf2-126">Geçmişinizi bash komutların bulut Kabuk oturum kesintisi veya eşzamanlı oturum nedeniyle tutarsız olabilir.</span><span class="sxs-lookup"><span data-stu-id="0fcf2-126">Your history of bash commands may be inconsistent because of Cloud Shell session disruption or concurrent sessions.</span></span>

## <a name="usage-limits"></a><span data-ttu-id="0fcf2-127">Kullanım sınırları</span><span class="sxs-lookup"><span data-stu-id="0fcf2-127">Usage limits</span></span>
<span data-ttu-id="0fcf2-128">Bulut Kabuk etkileşimli kullanım durumları için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="0fcf2-128">Cloud Shell is intended for interactive use cases.</span></span> <span data-ttu-id="0fcf2-129">Sonuç olarak, tüm uzun süre çalışan etkileşimli olmayan oturumlar uyarmadan sonlandırılır.</span><span class="sxs-lookup"><span data-stu-id="0fcf2-129">As a result, any long-running non-interactive sessions are ended without warning.</span></span>

## <a name="network-connectivity"></a><span data-ttu-id="0fcf2-130">Ağ bağlantısı</span><span class="sxs-lookup"><span data-stu-id="0fcf2-130">Network connectivity</span></span>
<span data-ttu-id="0fcf2-131">Bulut Kabuğu'ndaki tüm gecikme konu toolocal internet bağlantısı, bulut Kabuk tooattempt toocarry gönderilen yönergeleri çıkışı devam eder.</span><span class="sxs-lookup"><span data-stu-id="0fcf2-131">Any latency in Cloud Shell is subject toolocal internet connectivity, Cloud Shell continues tooattempt toocarry out any instructions sent.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0fcf2-132">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0fcf2-132">Next steps</span></span>
[<span data-ttu-id="0fcf2-133">Bulut Kabuk hızlı başlangıç</span><span class="sxs-lookup"><span data-stu-id="0fcf2-133">Cloud Shell Quickstart</span></span>](quickstart.md)
