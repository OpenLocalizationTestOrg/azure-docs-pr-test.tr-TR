---
title: "aaaAzure SDK .NET 3.0 sürüm notları | Microsoft Docs"
description: ".NET 3.0 için Azure SDK sürüm notları"
services: app-service\web
documentationcenter: .net
author: chrissfanos
editor: 
ms.assetid: c83d815b-fc19-4260-821e-7d2a7206dffc
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 03/07/2017
ms.author: juliako
ms.openlocfilehash: 8970b4c9b64de40dc29a33d69006a00ae5e38a50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-30-release-notes"></a><span data-ttu-id="a8809-103">.NET 3.0 için Azure SDK sürüm notları</span><span class="sxs-lookup"><span data-stu-id="a8809-103">Azure SDK for .NET 3.0 release notes</span></span>

<span data-ttu-id="a8809-104">Bu konu, .NET için Sürüm Notları'hello Azure SDK'ın 3.0 sürümü için içerir.</span><span class="sxs-lookup"><span data-stu-id="a8809-104">This topic includes release notes for version 3.0 of hello Azure SDK for .NET.</span></span>

##<a name="azure-sdk-for-net-30-release-summary"></a><span data-ttu-id="a8809-105">.NET 3.0 sürüm özeti için Azure SDK'sı</span><span class="sxs-lookup"><span data-stu-id="a8809-105">Azure SDK for .NET 3.0 release summary</span></span>

<span data-ttu-id="a8809-106">Yayın Tarihi: 07/03/2017</span><span class="sxs-lookup"><span data-stu-id="a8809-106">Release date: 03/07/2017</span></span>
 
<span data-ttu-id="a8809-107">Hiçbir en son değişiklikleri toohello Azure SDK 3.0 sunulan bu sürümde.</span><span class="sxs-lookup"><span data-stu-id="a8809-107">No breaking changes toohello Azure SDK 3.0 have been introduced in this release.</span></span> <span data-ttu-id="a8809-108">Bu SDK mevcut bulut hizmeti projeleri ile de hiçbir gereken yükseltme işlemi tooleverage yoktur.</span><span class="sxs-lookup"><span data-stu-id="a8809-108">There is also no upgrade process needed tooleverage this SDK with existing Cloud Service projects.</span></span> <span data-ttu-id="a8809-109">bir yükseltme işlemi, Azure SDK 3.0 gerektirmeden Azure SDK 3.0 hello tooallow kullanımını yükler toohello Azure SDK 2.9 aynı dizine.</span><span class="sxs-lookup"><span data-stu-id="a8809-109">tooallow use of hello Azure SDK 3.0 without requiring an upgrade process, Azure SDK 3.0 installs toohello same directories as Azure SDK 2.9.</span></span> <span data-ttu-id="a8809-110">Çoğu hello bileşenleri hello ana sürüm 2.9 değiştirilmemesi ancak bunun yerine yalnızca hello yapı numarası güncelleştirildi.</span><span class="sxs-lookup"><span data-stu-id="a8809-110">Most hello components did not change hello major version from 2.9 but instead just updated hello build number.</span></span>

## <a name="visual-studio-2017-rtw"></a><span data-ttu-id="a8809-111">Visual Studio 2017 RTW</span><span class="sxs-lookup"><span data-stu-id="a8809-111">Visual Studio 2017 RTW</span></span>

- <span data-ttu-id="a8809-112">Visual Studio 2017 ' bu sürümü hello Azure SDK'sı, .NET için toohello Azure iş yükü yerleşik olarak bulunur.</span><span class="sxs-lookup"><span data-stu-id="a8809-112">In Visual Studio 2017, this release of hello Azure SDK for .NET is built in toohello Azure Workload.</span></span> <span data-ttu-id="a8809-113">Toodo Azure geliştirme gereken tüm hello araçları Visual Studio ileride 2017 bir parçası olur.</span><span class="sxs-lookup"><span data-stu-id="a8809-113">All hello tools you need toodo Azure development will be part of Visual Studio 2017 going forward.</span></span> <span data-ttu-id="a8809-114">Visual Studio 2015 için hello SDK Webpı kullanılabilir olmaya devam eder.</span><span class="sxs-lookup"><span data-stu-id="a8809-114">For Visual Studio 2015 hello SDK will still be available through WebPI.</span></span> <span data-ttu-id="a8809-115">Visual Studio 2017 yayımlanan göre Biz Visual Studio 2013 için .NET sürümleri için Azure SDK'sı sonlandırdıktan.</span><span class="sxs-lookup"><span data-stu-id="a8809-115">We have discontinued Azure SDK for .NET releases for Visual Studio 2013 now that Visual Studio 2017 has been released.</span></span>

### <a name="azure-diagnostics"></a><span data-ttu-id="a8809-116">Azure Tanılama</span><span class="sxs-lookup"><span data-stu-id="a8809-116">Azure Diagnostics</span></span>

- <span data-ttu-id="a8809-117">Değiştirilen hello davranışı tooonly bulut Hizmetleri tanılama depolama bağlantı dizesi için bir belirteç değiştirilmiştir hello anahtarla bir kısmi bağlantı dizesi depolar.</span><span class="sxs-lookup"><span data-stu-id="a8809-117">Changed hello behavior tooonly store a partial connection string with hello key replaced by a token for Cloud Services diagnostics storage connection string.</span></span> <span data-ttu-id="a8809-118">kendi erişim denetlenebilir şekilde hello gerçek depolama anahtarı artık hello kullanıcı profili klasöründe depolanır.</span><span class="sxs-lookup"><span data-stu-id="a8809-118">hello actual storage key is now stored in hello user profile folder so its access can be controlled.</span></span> <span data-ttu-id="a8809-119">Visual Studio yerel hata ayıklama ve yayımlama işlemi için kullanıcı profili klasöründen hello depolama anahtarı okur.</span><span class="sxs-lookup"><span data-stu-id="a8809-119">Visual Studio will read hello storage key from user profile folder for local debugging and publishing process.</span></span> 
- <span data-ttu-id="a8809-120">Yanıt toohello değişiklik yukarıda açıklanan Visual Studio Online ekip Gelişmiş hello Azure Cloud Services Dağıtımı görev şablonu kullanıcılar tooAzure içinde sürekli tümleştirme yayımlarken tanılama uzantısını ayarlamak için hello depolama anahtarı belirtebilirsiniz şekilde ve dağıtım.</span><span class="sxs-lookup"><span data-stu-id="a8809-120">In response toohello change described above, Visual Studio Online team enhanced hello Azure Cloud Services deployment task template so users could specify hello storage key for setting diagnostics extension when publishing tooAzure in Continuous Integration and Deployment.</span></span>
- <span data-ttu-id="a8809-121">Bu olası toostore güvenli bağlantı dizesi ve simgeleştirme için Azure tanılama (WAD), environements arasında yapılandırma sorunlarını çözmek toohelp yaptık.</span><span class="sxs-lookup"><span data-stu-id="a8809-121">We’ve made it possible toostore secure connection string and tokenization for Azure Diagnostics (WAD), toohelp you solve problems with configuration across environements.</span></span>
 
### <a name="windows-server-2016-virtual-machines"></a><span data-ttu-id="a8809-122">Windows Server 2016 sanal makineler</span><span class="sxs-lookup"><span data-stu-id="a8809-122">Windows Server 2016 virtual machines</span></span>

- <span data-ttu-id="a8809-123">Visual Studio şimdi dağıtma bulut Hizmetleri tooOS ailesi 5 (Windows Server 2016) sanal makineleri destekler.</span><span class="sxs-lookup"><span data-stu-id="a8809-123">Visual Studio now supports deploying Cloud Services tooOS Family 5 (Windows Server 2016) virtual machines.</span></span> <span data-ttu-id="a8809-124">Mevcut bulut hizmetlerini ayarları tootarget değiştirebilirsiniz yeni işletim sistemi ailesi hello.</span><span class="sxs-lookup"><span data-stu-id="a8809-124">For existing cloud services, you can change your settings tootarget hello new OS Family.</span></span> <span data-ttu-id="a8809-125">.Net 4.6 ya da daha yüksek kullanarak toocreate hello hizmet seçerseniz yeni bulut Hizmetleri, oluştururken, varsayılan olarak hello hizmet toouse işletim sistemi ailesi 5 alır.</span><span class="sxs-lookup"><span data-stu-id="a8809-125">When creating new cloud services, if you choose toocreate hello service using .net 4.6 or higher, it will default hello service toouse OS Family 5.</span></span>  <span data-ttu-id="a8809-126">Daha fazla bilgi için hello gözden geçirebilirsiniz [konuk işletim sistemi ailesi destek tablo](../cloud-services/cloud-services-guestos-update-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="a8809-126">For more information, you can review hello [Guest OS Family support table](../cloud-services/cloud-services-guestos-update-matrix.md).</span></span>

### <a name="known-issues"></a><span data-ttu-id="a8809-127">Bilinen sorunlar</span><span class="sxs-lookup"><span data-stu-id="a8809-127">Known issues</span></span>

- <span data-ttu-id="a8809-128">Azure .NET SDK 3.0 bir sorun, Visual Studio 2017 Visual Studio 2015 ile yan yana yapılandırmasında kaldırırken kullanıma sunuldu.</span><span class="sxs-lookup"><span data-stu-id="a8809-128">Azure .NET SDK 3.0 introduced an issue when removing Visual Studio 2017 in a side by side configuration with Visual Studio 2015.</span></span>  <span data-ttu-id="a8809-129">Hello Azure SDK'sı için Visual Studio 2015 yüklü varsa, Microsoft Azure Storage öykünücüsü hello ve Microsoft Azure işlem öykünücüsü, Visual Studio 2017'i kaldırırsanız kaldırılacak.</span><span class="sxs-lookup"><span data-stu-id="a8809-129">If you have hello Azure SDK installed for Visual Studio 2015, hello Microsoft Azure Storage Emulator and Microsoft Azure Compute Emulator will be removed if you uninstall Visual Studio 2017.</span></span>  <span data-ttu-id="a8809-130">Bu oluşturma ve Visual Studio 2015 yeni bulut Hizmetleri projelerinde hata ayıklama sırasında bir hata oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a8809-130">This will produce an error when creating and debugging new Cloud services projects in Visual Studio 2015.</span></span> <span data-ttu-id="a8809-131">İçinde bu sorunu toofix sipariş, hello Web Platformu Yükleyicisi'nden hello Azure SDK'sını yeniden yükleyin.</span><span class="sxs-lookup"><span data-stu-id="a8809-131">In order toofix this issue,  reinstall hello Azure SDK from hello Web Platform Installer.</span></span>  <span data-ttu-id="a8809-132">Merhaba sorun çözümlenir gelecekteki bir Visual Studio 2017 güncelleştirme.</span><span class="sxs-lookup"><span data-stu-id="a8809-132">hello issue will be resolved in a future Visual Studio 2017 update.</span></span>  <span data-ttu-id="a8809-133">.</span><span class="sxs-lookup"><span data-stu-id="a8809-133">.</span></span>

 
### <a name="azure-in-role-cache"></a><span data-ttu-id="a8809-134">Azure rol içi önbellek</span><span class="sxs-lookup"><span data-stu-id="a8809-134">Azure In-Role Cache</span></span> 

- <span data-ttu-id="a8809-135">Azure rol içi önbelleği için destek, 30 Kasım 2016 tarihinde sona erdi.</span><span class="sxs-lookup"><span data-stu-id="a8809-135">Support for Azure In-Role Cache ended on November 30, 2016.</span></span> <span data-ttu-id="a8809-136">Daha fazla ayrıntı için tıklatın [burada](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/).</span><span class="sxs-lookup"><span data-stu-id="a8809-136">For more details, click [here](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/).</span></span>




