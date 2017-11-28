---
title: "Azure RemoteApp aaaMigrate kullanıcı verilerini | Microsoft Docs"
description: "Bilgi nasıl toomigrate kullanıcı verilerinizi Azure RemoteApp ve."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: d7e4fbf1-cb42-4430-94a0-ed6d4676fc86
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: aefc6ccc2c6173754acf6cad06102f27c8cb1d26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomigrate-data-into-and-out-of-azure-remoteapp"></a><span data-ttu-id="2095a-103">Nasıl toomigrate veri içine ve dışına Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="2095a-103">How toomigrate data into and out of Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="2095a-104">Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır.</span><span class="sxs-lookup"><span data-stu-id="2095a-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="2095a-105">Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="2095a-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="2095a-106">Birçok farklı araçlar ve yöntemleri tootransfer kullanabileceğiniz [kullanıcı verilerini](remoteapp-upd.md) içine ve dışına Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="2095a-106">You can use many different tools and methods tootransfer [user data](remoteapp-upd.md) into and out of Azure RemoteApp.</span></span> <span data-ttu-id="2095a-107">Bazı yöntemler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="2095a-107">Here are a few methods:</span></span>

* <span data-ttu-id="2095a-108">Kopyala ve Yapıştır Pano paylaşımını kullanma</span><span class="sxs-lookup"><span data-stu-id="2095a-108">Copy and paste using clipboard sharing</span></span>
* <span data-ttu-id="2095a-109">Dosyaları ve verileri tooa dosya sunucusuna kopyalayın</span><span class="sxs-lookup"><span data-stu-id="2095a-109">Copy files and data tooa file server</span></span>
* <span data-ttu-id="2095a-110">Dosyaları tooOneDrive iş için bir tarayıcı üzerinden kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="2095a-110">Copy files tooOneDrive for Business through a browser</span></span>
* <span data-ttu-id="2095a-111">Yeniden yönlendirme kullanarak dosyaları kopyalama</span><span class="sxs-lookup"><span data-stu-id="2095a-111">Copy files using redirection</span></span>

> [!NOTE]
> <span data-ttu-id="2095a-112">Merhaba OneDrive iş veya tüketici eşitleme aracılar için - etkinleştiremiyor bunlar [desteklenmez](remoteapp-onedrive.md) Azure remoteapp'te.</span><span class="sxs-lookup"><span data-stu-id="2095a-112">You cannot enable hello OneDrive for Business or Consumer sync agents - they [are not supported](remoteapp-onedrive.md) in Azure RemoteApp.</span></span>
> 
> 

## <a name="use-copy-and-paste-in-file-explorer"></a><span data-ttu-id="2095a-113">Kopyala ve Yapıştır dosya Gezgini'nde kullanın</span><span class="sxs-lookup"><span data-stu-id="2095a-113">Use copy and paste in File Explorer</span></span>
<span data-ttu-id="2095a-114">Kopyala ve Yapıştır hello Pano kullanarak RemoteApp dağıtımlarda etkin [varsayılan](remoteapp-redirection.md).</span><span class="sxs-lookup"><span data-stu-id="2095a-114">Copy and paste using hello clipboard is enabled in RemoteApp deployments [by default](remoteapp-redirection.md).</span></span> <span data-ttu-id="2095a-115">Bu, kullanıcıların kendi yerel bilgisayar ve RemoteApp uygulamalar arasında dosya kopyalama sağlar.</span><span class="sxs-lookup"><span data-stu-id="2095a-115">This lets users copy files between their local PC and RemoteApp apps.</span></span> <span data-ttu-id="2095a-116">Genellikle, RemoteApp uygulamaları kullanmanın hello normal seyrinde, kullanıcıların dosyalarını tootheir UPD - RemoteApp dışında veri kadar kolay olduğunu taşıma kaydetmiş:</span><span class="sxs-lookup"><span data-stu-id="2095a-116">Often, through hello normal course of using apps in RemoteApp, users have saved files tootheir UPDs - moving that data out of RemoteApp is easy:</span></span>

1. <span data-ttu-id="2095a-117">[Bir uygulama olarak dosya Gezgini yayımlama](remoteapp-publish.md) RemoteApp koleksiyonunda.</span><span class="sxs-lookup"><span data-stu-id="2095a-117">[Publish File Explorer as an app](remoteapp-publish.md) in a RemoteApp collection.</span></span> <span data-ttu-id="2095a-118">(Bu bir yönetim görevi olduğunu unutmayın.)</span><span class="sxs-lookup"><span data-stu-id="2095a-118">(Note that this is an administrative task.)</span></span>
2. <span data-ttu-id="2095a-119">Kullanıcıların toolaunch hello dosya Gezgini uygulamasını yayımladığınız ve toouse toocopy ve Yapıştır dosyaların hem kendi UPD içine ve onu dışına doğrudan.</span><span class="sxs-lookup"><span data-stu-id="2095a-119">Direct your users toolaunch hello File Explorer app you published and toouse that toocopy and paste files both into their UPD and out of it.</span></span>

## <a name="upload-files-and-data-tooa-file-server-by-using-standard-network-file-copy"></a><span data-ttu-id="2095a-120">Standart ağ dosya kopyalama kullanarak dosyaları ve verileri tooa dosya sunucusu yükleyin</span><span class="sxs-lookup"><span data-stu-id="2095a-120">Upload files and data tooa file server by using standard network file copy</span></span>
<span data-ttu-id="2095a-121">Genellikle kuruluş dosya sunucuları toostore genel verileri kullanır.</span><span class="sxs-lookup"><span data-stu-id="2095a-121">Often organizations use file servers toostore general data.</span></span> <span data-ttu-id="2095a-122">Hello sunucu adı veya konumu biliyorsanız, kullanıcılarınızın hello sunucusu yerel ağa hello göz atın ve çok yukarıda menülerin gibi kendi dosyalarını kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="2095a-122">If you know hello server name or location, your users can browse hello local network for hello server and then copy their files there, much like they did above.</span></span> <span data-ttu-id="2095a-123">Yeniden toopublish dosya Gezgini tooRemoteApp istediğiniz ve kullanıcılarınızla paylaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2095a-123">Again you'll want toopublish File Explorer tooRemoteApp and then share it with your users.</span></span>

> [!NOTE]
> <span data-ttu-id="2095a-124">Merhaba dosya sunucusu ağda RemoteApp içine dağıtılan hello yönlendirilebilir olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="2095a-124">hello file server must be on hello routable network that RemoteApp was deployed into.</span></span>
> 
> 

## <a name="copy-files-tooonedrive-for-business"></a><span data-ttu-id="2095a-125">İş için dosyaları tooOneDrive kopyalama</span><span class="sxs-lookup"><span data-stu-id="2095a-125">Copy files tooOneDrive for Business</span></span>
<span data-ttu-id="2095a-126">Merhaba OneDrive iş eşitleme Aracısı remoteapp'te etkinleştiremiyor rağmen hala dosyaları, UPD tooOneDrive iş için bir tarayıcı üzerinden kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2095a-126">Although you cannot enable hello OneDrive for Business sync agent in RemoteApp, you can still copy files from your UPD tooOneDrive for Business through a browser.</span></span> 

1. <span data-ttu-id="2095a-127">Dosya Gezgini tooRemoteApp yayımlayabilir ve kullanıcıların tooaccess dosyalar bu uygulama ile Merhaba söyleyin.</span><span class="sxs-lookup"><span data-stu-id="2095a-127">Publish File Explorer tooRemoteApp and then tell users tooaccess hello files through that app.</span></span> 
2. <span data-ttu-id="2095a-128">Sıkıştırılma biçimini, kullanıcıların tüm hello dosyaları toomove tooOneDrive iş için içeren bir .zip dosyası oluşturmanız gerekir böylece kolay tootransfer dosyaları olur.</span><span class="sxs-lookup"><span data-stu-id="2095a-128">It's easiest tootransfer files if they are compressed, so users should create a .zip file that contains all of hello files toomove tooOneDrive for Business.</span></span>
3. <span data-ttu-id="2095a-129">Kullanıcılar toogo toohello Office 365 portalı, isteyin ve sonra tooOneDrive gidin ve hello .zip dosyasını karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="2095a-129">Ask users toogo toohello Office 365 portal, and then go tooOneDrive and upload hello .zip file.</span></span>

## <a name="copy-files-by-using-drive-redirection"></a><span data-ttu-id="2095a-130">Sürücü yeniden yönlendirme kullanarak dosyaları kopyalayın</span><span class="sxs-lookup"><span data-stu-id="2095a-130">Copy files by using drive redirection</span></span>
<span data-ttu-id="2095a-131">Etkinleştirdiyseniz [sürücüyü yeniden yönlendirme](remoteapp-redirection.md), kullanıcılarınız için eşlenmiş bir sürücüyü zaten oluşturulmuş.</span><span class="sxs-lookup"><span data-stu-id="2095a-131">If you have enabled [drive redirection](remoteapp-redirection.md), you have already created a mapped drive for your users.</span></span> <span data-ttu-id="2095a-132">Bu durumda, bunlar kendi dosyaları yeniden yönlendirilen hello sürücüde zip ve bunları tootheir kaydedin yerel bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="2095a-132">In this case, they can zip their files on hello redirected drive and then save them tootheir local PC.</span></span>

## <a name="how-administrators-can-export-data"></a><span data-ttu-id="2095a-133">Yöneticiler verileri nasıl verebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="2095a-133">How administrators can export data</span></span>

<span data-ttu-id="2095a-134">Abonelik tooAzure Azure PowerShell kullanarak depolama içinde tüm koleksiyonlar için tüm kullanıcı profili diskleri (UPD) Azure RemoteApp verebilirsiniz için yönetir cmdlet, dışa aktarma AzureRemoteAppUserDisk.</span><span class="sxs-lookup"><span data-stu-id="2095a-134">Administers for Azure RemoteApp can export all user profile disks (UPD) for all collections within a subscription tooAzure Storage using Azure PowerShell cmdlet, Export-AzureRemoteAppUserDisk.</span></span>  <span data-ttu-id="2095a-135">Hiçbir özelliği tooselect tek tek UPD's yoktur.</span><span class="sxs-lookup"><span data-stu-id="2095a-135">There is no ability tooselect individual UPD's.</span></span>  <span data-ttu-id="2095a-136">Merhaba PowerShell komut çalıştırıldığında, her kullanıcı disk sabit disk boyutu 50 gb olması ve dışarı aktarılan tooAzure depolama.</span><span class="sxs-lookup"><span data-stu-id="2095a-136">When hello PowerShell command is executed, each user disk will be a 50gb in fixed disk size and be exported tooAzure storage.</span></span>  <span data-ttu-id="2095a-137">Azure depolama maliyetinden hemen bu depolama için uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="2095a-137">Costs of Azure storage will incur immediately for this storage.</span></span>  <span data-ttu-id="2095a-138">Bu komutu çalıştırmak olun Aksi takdirde hello dışarı aktarma başarısız olur hiçbir oturum vardır.</span><span class="sxs-lookup"><span data-stu-id="2095a-138">When running this command ensure there are no sessions otherwise hello export will fail.</span></span>

<span data-ttu-id="2095a-139">UPD bilgisayarın etki alanına katılmış Azure RemoteApp dağıtımları için bir RDS dağıtımda yalnızca bir yeniden kullanılabilir, etki alanı olmayan birleştirilmiş dağıtımları kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="2095a-139">UPD's for domain joined Azure RemoteApp deployments can only be used again in an RDS deployment, non-domain joined deployments cannot be used.</span></span>  <span data-ttu-id="2095a-140">Bu diskleri bir RDS dağıtımında kullanılacaksa toouse öneririz bizim [betikleri otomatik](https://github.com/arcadiahlyy/aramigration) , aktarın, dönüştürme ve hello UPD'ın bir RDS dağıtımı ile aktarın.</span><span class="sxs-lookup"><span data-stu-id="2095a-140">If these disks will be used in an RDS deployment we recommend toouse our [automated scripts](https://github.com/arcadiahlyy/aramigration) that will export, convert, and import hello UPD's into an RDS deployment.</span></span>

