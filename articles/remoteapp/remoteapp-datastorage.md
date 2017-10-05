---
title: "Hassas verileri özel görüntülerinde Azure RemoteApp için hiçbir zaman depolamak | Microsoft Docs"
description: "Azure remoteapp'te özel görüntü verilerini depolamak için yönergeleri hakkında bilgi edinin"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 5a19903b-15f9-49d9-9bc1-ae80f2671aa1
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 75d5415d33324d957617426e75909a6c6c58b1f9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="never-store-sensitive-data-on-custom-images"></a><span data-ttu-id="de6b7-103">Hiçbir zaman deposu hassas verileri özel görüntüleri</span><span class="sxs-lookup"><span data-stu-id="de6b7-103">Never store sensitive data on custom images</span></span>
> [!IMPORTANT]
> <span data-ttu-id="de6b7-104">Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır.</span><span class="sxs-lookup"><span data-stu-id="de6b7-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="de6b7-105">Ayrıntılı bilgi için [duyuruyu](https://go.microsoft.com/fwlink/?linkid=821148) okuyun.</span><span class="sxs-lookup"><span data-stu-id="de6b7-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="de6b7-106">Azure RemoteApp, kendi uygulamanızda barındırdığınızda, ilk adım özel bir görüntü oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="de6b7-106">When you host your own application in Azure RemoteApp, the first step is to create a custom image.</span></span> <span data-ttu-id="de6b7-107">Kullanıcılarınıza, uygulamalarınızı hizmet VM örnekleri oluşturmak için özel görüntü kullanırız.</span><span class="sxs-lookup"><span data-stu-id="de6b7-107">We use that custom image to create VM instances that serve your apps to your users.</span></span> <span data-ttu-id="de6b7-108">Özel görüntü yalnızca uygulamaları ve SQL veritabanları, personel dosyaları ya da QuickBooks şirket dosyaları gibi özel veri dosyaları gibi kayıp olabilecek hiçbir zaman hassas verileri içermelidir.</span><span class="sxs-lookup"><span data-stu-id="de6b7-108">The custom image should contain ONLY applications and never sensitive data that can be lost, such as SQL databases, personnel files, or special data files like QuickBooks company files.</span></span> <span data-ttu-id="de6b7-109">Tüm gizli verilerin başka bir Azure VM, bir dosya sunucusunda veya SQL Azure Azure RemoteApp harici bulunmalıdır.</span><span class="sxs-lookup"><span data-stu-id="de6b7-109">All sensitive data should reside external to Azure RemoteApp on a file server, another Azure VM, or in SQL Azure.</span></span> <span data-ttu-id="de6b7-110">Görüntü yalnızca veri kaynağına bağlanır ve verileri sunan uygulama ana bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="de6b7-110">The image should just host the application that connects to the data source and presents the data.</span></span> <span data-ttu-id="de6b7-111">Gözden geçirme [Azure RemoteApp görüntüleri için gereksinimleri](remoteapp-imagereqs.md) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="de6b7-111">Review [Requirements for Azure RemoteApp images](remoteapp-imagereqs.md) for more information.</span></span> 

<span data-ttu-id="de6b7-112">Neden, hassas verileri depolamamayı anlamak için Azure RemoteApp nasıl çalıştığını anlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="de6b7-112">To understand why you should not store sensitive data, you need to understand how Azure RemoteApp works.</span></span> <span data-ttu-id="de6b7-113">Ne zaman bir koleksiyon oluşturulur veya güncelleştirilir, arka planda birden çok klonlar veya görüntü kopyası oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="de6b7-113">When a collection is created or updated, behind the scenes multiple clones or copies of the image are created.</span></span> <span data-ttu-id="de6b7-114">Tüm VM örnekleri özel görüntü tam çoğaltmalarının; yine de uygun istiyor musunuz? Kullanıcıların uygulamaları başlattığında bunlar bu VM örnekleri birine bağlanır.</span><span class="sxs-lookup"><span data-stu-id="de6b7-114">All these VM instances are exact replicas of the custom image; when users launch applications they are connected to one of these VM instances.</span></span> <span data-ttu-id="de6b7-115">Ancak aynı örneğini garanti edilmez ve kalıcı olmayan olduklarından önemli değil.</span><span class="sxs-lookup"><span data-stu-id="de6b7-115">But the same instance is not guaranteed and should not matter because they are non-persistent.</span></span> <span data-ttu-id="de6b7-116">Uygulamaları barındıran VM örnekleri kalıcı değildir ve yok veya silinebilir tabanlı, örneğin, koleksiyon güncelleştirme sırasında.</span><span class="sxs-lookup"><span data-stu-id="de6b7-116">The VM instances hosting the applications are non-persistent and can be destroyed or deleted based, for example, during collection update.</span></span> 

<span data-ttu-id="de6b7-117">Koleksiyon sağlanan ve kullanıcıların Başlat Vm'lere bağlanması sonra kullanıcı verilerini kalıcı olan ve sizi arayarak bir VHD içinde ayrı bir depolama üzerinde kaydedildiğinden korumalı bir [kullanıcı profili diski (UPD)](remoteapp-upd.md), c:\users kullanıcı profilinde olduğu\<USERPROFILE >.</span><span class="sxs-lookup"><span data-stu-id="de6b7-117">Once the collection is provisioned and users start connecting to the VMs, user data is persistent and protected because it is saved on separate storage within a VHD that we call a [user profile disk (UPD)](remoteapp-upd.md), which is the user profile in c:\users\<userprofile>.</span></span> <span data-ttu-id="de6b7-118">Bir uygulama başlatıldığında UPD bağlanır ve yalnızca yerel kullanıcı profili gibi işletim sistemi tarafından kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="de6b7-118">When an application starts, the UPD is mounted and treated just like a local user profile by the operating system.</span></span> <span data-ttu-id="de6b7-119">Nasıl hakkında daha fazla bilgiyi [Azure RemoteApp kullanıcı verilerini ve ayarlarını kaydeder](remoteapp-upd.md).</span><span class="sxs-lookup"><span data-stu-id="de6b7-119">Read more about how [Azure RemoteApp saves user data and settings](remoteapp-upd.md).</span></span>

<span data-ttu-id="de6b7-120">Görüntüde yer almalıdır. değil örnek verileri:</span><span class="sxs-lookup"><span data-stu-id="de6b7-120">Example data that should not reside in the image:</span></span>

* <span data-ttu-id="de6b7-121">Paylaşılan veri erişmeleri kullanıcılara</span><span class="sxs-lookup"><span data-stu-id="de6b7-121">Shared data for users to access</span></span>
* <span data-ttu-id="de6b7-122">SQL DB ya da QuickBooks DB</span><span class="sxs-lookup"><span data-stu-id="de6b7-122">SQL DB or QuickBooks DB</span></span>
* <span data-ttu-id="de6b7-123">D:\ içinde herhangi bir veri</span><span class="sxs-lookup"><span data-stu-id="de6b7-123">Any data in D:\\</span></span>

<span data-ttu-id="de6b7-124">Tüm kullanıcıların UPD kopyalanacak varsayılan profili bulunabilir örnek verileri:</span><span class="sxs-lookup"><span data-stu-id="de6b7-124">Example data that can reside in the default profile to be copied into every users’ UPD:</span></span>

* <span data-ttu-id="de6b7-125">Kullanıcı başına yapılandırma dosyaları</span><span class="sxs-lookup"><span data-stu-id="de6b7-125">Configuration files per user</span></span>
* <span data-ttu-id="de6b7-126">Kendi UPD korunur kullanıcılar gerekir komut dosyaları</span><span class="sxs-lookup"><span data-stu-id="de6b7-126">Scripts that users would need preserved in their UPD</span></span>

<span data-ttu-id="de6b7-127">Önemli noktaları:</span><span class="sxs-lookup"><span data-stu-id="de6b7-127">Key points:</span></span>

* <span data-ttu-id="de6b7-128">Görüntüde oluşturulurken özel bir görüntü kaybedilen hiçbir zaman deposu hassas veriler.</span><span class="sxs-lookup"><span data-stu-id="de6b7-128">Never store sensitive data that can be lost on the image when creating a custom image.</span></span>
* <span data-ttu-id="de6b7-129">Hassas verileri her zaman ayrı bir dosya sunucusunda, ayrı Azure VM, Bulut ve her zaman dış uygulamalarınızı Azure RemoteApp içinde barındırma VM örnekleri yer almalıdır.</span><span class="sxs-lookup"><span data-stu-id="de6b7-129">Sensitive data should always reside on a separate file server, separate Azure VM, on the cloud, and always external to the VM instances hosting your applications within Azure RemoteApp.</span></span> 
* <span data-ttu-id="de6b7-130">Kullanıcı verileri kaydedilir ve kullanıcı profili diski (UPD) devam ettirir</span><span class="sxs-lookup"><span data-stu-id="de6b7-130">User data is saved and persists in the user profile disk (UPD)</span></span>

