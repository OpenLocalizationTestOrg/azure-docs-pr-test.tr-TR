---
title: "Azure RemoteApp için özel görüntülerinde aaaNever deposu hassas verileri | Microsoft Docs"
description: "Azure remoteapp'te özel görüntü verilerini depolamak için hello yönergeleri hakkında bilgi edinin"
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
ms.openlocfilehash: 86a0fea218f8826d6d25f50d3c4c36e368e26fb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="never-store-sensitive-data-on-custom-images"></a><span data-ttu-id="afbd3-103">Hiçbir zaman deposu hassas verileri özel görüntüleri</span><span class="sxs-lookup"><span data-stu-id="afbd3-103">Never store sensitive data on custom images</span></span>
> [!IMPORTANT]
> <span data-ttu-id="afbd3-104">Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır.</span><span class="sxs-lookup"><span data-stu-id="afbd3-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="afbd3-105">Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="afbd3-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="afbd3-106">Azure RemoteApp, kendi uygulamanızda barındırdığınızda hello ilk toocreate özel bir görüntü adımdır.</span><span class="sxs-lookup"><span data-stu-id="afbd3-106">When you host your own application in Azure RemoteApp, hello first step is toocreate a custom image.</span></span> <span data-ttu-id="afbd3-107">Uygulamalarınızı tooyour kullanıcılar hizmet bu özel görüntü toocreate VM örnekleri kullanırız.</span><span class="sxs-lookup"><span data-stu-id="afbd3-107">We use that custom image toocreate VM instances that serve your apps tooyour users.</span></span> <span data-ttu-id="afbd3-108">Merhaba özel görüntü yalnızca uygulamaları ve SQL veritabanları, personel dosyaları ya da QuickBooks şirket dosyaları gibi özel veri dosyaları gibi kayıp olabilecek hiçbir zaman hassas verileri içermelidir.</span><span class="sxs-lookup"><span data-stu-id="afbd3-108">hello custom image should contain ONLY applications and never sensitive data that can be lost, such as SQL databases, personnel files, or special data files like QuickBooks company files.</span></span> <span data-ttu-id="afbd3-109">Tüm gizli veriler dış tooAzure RemoteApp başka bir Azure VM, bir dosya sunucusunda veya SQL Azure bulunmalıdır.</span><span class="sxs-lookup"><span data-stu-id="afbd3-109">All sensitive data should reside external tooAzure RemoteApp on a file server, another Azure VM, or in SQL Azure.</span></span> <span data-ttu-id="afbd3-110">Merhaba görüntü toohello veri kaynağına bağlanan ve hello verileri sunan yalnızca konak Merhaba uygulaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="afbd3-110">hello image should just host hello application that connects toohello data source and presents hello data.</span></span> <span data-ttu-id="afbd3-111">Gözden geçirme [Azure RemoteApp görüntüleri için gereksinimleri](remoteapp-imagereqs.md) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="afbd3-111">Review [Requirements for Azure RemoteApp images](remoteapp-imagereqs.md) for more information.</span></span> 

<span data-ttu-id="afbd3-112">neden değil depoladığınız hassas verileri toounderstand Azure RemoteApp nasıl çalıştığını toounderstand gerekir.</span><span class="sxs-lookup"><span data-stu-id="afbd3-112">toounderstand why you should not store sensitive data, you need toounderstand how Azure RemoteApp works.</span></span> <span data-ttu-id="afbd3-113">Bir koleksiyonu oluşturulmuş veya güncelleştirilmiş hello arka planda birden çok klonlar veya hello görüntü kopyası oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="afbd3-113">When a collection is created or updated, behind hello scenes multiple clones or copies of hello image are created.</span></span> <span data-ttu-id="afbd3-114">Tüm VM örnekleri hello özel görüntü tam çoğaltmalarının; yine de uygun istiyor musunuz? Kullanıcıların uygulamaları başlattığınızda bu VM örnekleri bağlı tooone oldukları.</span><span class="sxs-lookup"><span data-stu-id="afbd3-114">All these VM instances are exact replicas of hello custom image; when users launch applications they are connected tooone of these VM instances.</span></span> <span data-ttu-id="afbd3-115">Ancak hello aynı örneği garanti edilmez ve kalıcı olmayan olduklarından önemli değil.</span><span class="sxs-lookup"><span data-stu-id="afbd3-115">But hello same instance is not guaranteed and should not matter because they are non-persistent.</span></span> <span data-ttu-id="afbd3-116">Örneğin, koleksiyon güncelleştirme sırasında temel yok veya silinmiş barındırma hello uygulamaları kalıcı olmayan ve olabilir VM örnekleri hello.</span><span class="sxs-lookup"><span data-stu-id="afbd3-116">hello VM instances hosting hello applications are non-persistent and can be destroyed or deleted based, for example, during collection update.</span></span> 

<span data-ttu-id="afbd3-117">Merhaba koleksiyonu hazırlanır ve kullanıcıların başlangıç bağlantı toohello VM'ler sonra kullanıcı verilerini kalıcı olan ve sizi arayarak bir VHD içinde ayrı bir depolama üzerinde kaydedildiğinden korumalı bir [kullanıcı profili diski (UPD)](remoteapp-upd.md), hello kullanıcı profili olduğu c:\users içinde\<USERPROFILE >.</span><span class="sxs-lookup"><span data-stu-id="afbd3-117">Once hello collection is provisioned and users start connecting toohello VMs, user data is persistent and protected because it is saved on separate storage within a VHD that we call a [user profile disk (UPD)](remoteapp-upd.md), which is hello user profile in c:\users\<userprofile>.</span></span> <span data-ttu-id="afbd3-118">Bir uygulama başlatıldığında hello UPD bağlanır ve yalnızca yerel kullanıcı profili gibi hello işletim sistemi tarafından kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="afbd3-118">When an application starts, hello UPD is mounted and treated just like a local user profile by hello operating system.</span></span> <span data-ttu-id="afbd3-119">Nasıl hakkında daha fazla bilgiyi [Azure RemoteApp kullanıcı verilerini ve ayarlarını kaydeder](remoteapp-upd.md).</span><span class="sxs-lookup"><span data-stu-id="afbd3-119">Read more about how [Azure RemoteApp saves user data and settings](remoteapp-upd.md).</span></span>

<span data-ttu-id="afbd3-120">Merhaba görüntüde bulunmalıdır değil örnek verileri:</span><span class="sxs-lookup"><span data-stu-id="afbd3-120">Example data that should not reside in hello image:</span></span>

* <span data-ttu-id="afbd3-121">Kullanıcıların tooaccess için paylaşılan veri</span><span class="sxs-lookup"><span data-stu-id="afbd3-121">Shared data for users tooaccess</span></span>
* <span data-ttu-id="afbd3-122">SQL DB ya da QuickBooks DB</span><span class="sxs-lookup"><span data-stu-id="afbd3-122">SQL DB or QuickBooks DB</span></span>
* <span data-ttu-id="afbd3-123">D:\ içinde herhangi bir veri</span><span class="sxs-lookup"><span data-stu-id="afbd3-123">Any data in D:\\</span></span>

<span data-ttu-id="afbd3-124">Tüm kullanıcıların UPD kopyalanan hello varsayılan profili toobe bulunabilir örnek verileri:</span><span class="sxs-lookup"><span data-stu-id="afbd3-124">Example data that can reside in hello default profile toobe copied into every users’ UPD:</span></span>

* <span data-ttu-id="afbd3-125">Kullanıcı başına yapılandırma dosyaları</span><span class="sxs-lookup"><span data-stu-id="afbd3-125">Configuration files per user</span></span>
* <span data-ttu-id="afbd3-126">Kendi UPD korunur kullanıcılar gerekir komut dosyaları</span><span class="sxs-lookup"><span data-stu-id="afbd3-126">Scripts that users would need preserved in their UPD</span></span>

<span data-ttu-id="afbd3-127">Önemli noktaları:</span><span class="sxs-lookup"><span data-stu-id="afbd3-127">Key points:</span></span>

* <span data-ttu-id="afbd3-128">Hiçbir zaman hello görüntüyü özel görüntü oluşturulurken kayıp hassas verileri depolar.</span><span class="sxs-lookup"><span data-stu-id="afbd3-128">Never store sensitive data that can be lost on hello image when creating a custom image.</span></span>
* <span data-ttu-id="afbd3-129">Hassas verileri her zaman ayrı bir dosya sunucusunda bulunan, hello Bulut ve uygulamalarınızı Azure RemoteApp içinde barındıran her zaman dış toohello VM örneklerinin Azure VM ayırın.</span><span class="sxs-lookup"><span data-stu-id="afbd3-129">Sensitive data should always reside on a separate file server, separate Azure VM, on hello cloud, and always external toohello VM instances hosting your applications within Azure RemoteApp.</span></span> 
* <span data-ttu-id="afbd3-130">Kullanıcı verileri kaydedilir ve hello kullanıcı profili diski (UPD) devam ettirir</span><span class="sxs-lookup"><span data-stu-id="afbd3-130">User data is saved and persists in hello user profile disk (UPD)</span></span>

