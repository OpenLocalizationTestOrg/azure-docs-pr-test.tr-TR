---
title: "Azure remoteapp'te QuickBooks dağıtma | Microsoft Docs"
description: "QuickBooks Azure RemoteApp ile paylaştığınız öğrenin."
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: c5d00753-77c0-4f0d-a5df-9451b46a31d3
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: bbfac45220f6ef36c9951daae0ced1974e8ddabb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-do-you-deploy-quickbooks-in-azure-remoteapp"></a><span data-ttu-id="da9a1-103">Azure remoteapp'te QuickBooks nasıl dağıttığınız?</span><span class="sxs-lookup"><span data-stu-id="da9a1-103">How do you deploy QuickBooks in Azure RemoteApp?</span></span>
> [!IMPORTANT]
> <span data-ttu-id="da9a1-104">Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır.</span><span class="sxs-lookup"><span data-stu-id="da9a1-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="da9a1-105">Ayrıntılı bilgi için [duyuruyu](https://go.microsoft.com/fwlink/?linkid=821148) okuyun.</span><span class="sxs-lookup"><span data-stu-id="da9a1-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="da9a1-106">Azure remoteapp'te bir uygulama olarak QuickBooks paylaşmak için aşağıdaki bilgileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="da9a1-106">Use the following information to share QuickBooks as an app in Azure RemoteApp.</span></span>

<span data-ttu-id="da9a1-107">QuickBooks 2015 kurumsal bir karma veya Bulut koleksiyonunda Azure RemoteApp ile paylaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="da9a1-107">You can share QuickBooks 2015 Enterprise with Azure RemoteApp in either a hybrid or cloud collection.</span></span> <span data-ttu-id="da9a1-108">Şirket dosyası Azure RemoteApp sunucularından ayrıdır QuickBooks veritabanı sunucusunu çalıştıran bir VM'de bulunmalıdır.</span><span class="sxs-lookup"><span data-stu-id="da9a1-108">The company file must reside on a VM that is running QuickBooks database server that is separate from the Azure RemoteApp servers.</span></span> <span data-ttu-id="da9a1-109">Hiçbir zaman şirket dosyası, Azure RemoteApp görüntüsüne depolamak - bunu yapmanız durumunda veri kaybını beklenir.</span><span class="sxs-lookup"><span data-stu-id="da9a1-109">Never store the company file on your Azure RemoteApp image - data loss is expected if you do this.</span></span> <span data-ttu-id="da9a1-110">Yalnızca QuickBooks kuruluş QuickBooks veritabanı sunucusuyla standart Windows ağ üzerinden erişilebilen bir harici paylaşımda QuickBooks dosyasını barındıran destekler.</span><span class="sxs-lookup"><span data-stu-id="da9a1-110">Only QuickBooks Enterprise supports hosting the QuickBooks file on an external share with QuickBooks database server accessible via standard Windows networking.</span></span>   

> [!IMPORTANT]
> <span data-ttu-id="da9a1-111">Şirket dosyası barındırma QuickBooks veritabanı sunucusu, Azure RemoteApp koleksiyonu olarak aynı sanal ağ içinde ayrı bir VM üzerinde bulunmalıdır.</span><span class="sxs-lookup"><span data-stu-id="da9a1-111">The QuickBooks database server that is hosting the company file must reside on a separate VM within the same VNET as the Azure RemoteApp collection.</span></span>  
> 
> 

## <a name="steps-to-deploy-quickbooks"></a><span data-ttu-id="da9a1-112">QuickBooks dağıtma adımları</span><span class="sxs-lookup"><span data-stu-id="da9a1-112">Steps to deploy QuickBooks</span></span>
1. <span data-ttu-id="da9a1-113">Bir Azure VM oluşturun ve QuickBooks, QuickBooks veritabanı sunucusu, yükleyin ve bir Azure VM şirket dosyayı yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="da9a1-113">Create an Azure VM and install QuickBooks, QuickBooks database server, and place the company file on a Azure VM.</span></span>  <span data-ttu-id="da9a1-114">Güvenlik duvarı kuralları doğru şekilde yapılandırdığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="da9a1-114">Make sure to properly configure firewall rules.</span></span>
2. <span data-ttu-id="da9a1-115">QuickBooks yüklemek bir [özel görüntü](remoteapp-imageoptions.md) ve oluşturma bir [Azure RemoteApp koleksiyonu](remoteapp-collections.md), Bulut veya karma burada QuickBooks barındırma VM veritabanı sunucusu şirket dosyaları ile tam aynı sanal ağ içinden yer alıyor.</span><span class="sxs-lookup"><span data-stu-id="da9a1-115">Install QuickBooks on a [custom image](remoteapp-imageoptions.md) and create an [Azure RemoteApp collection](remoteapp-collections.md), either cloud or hybrid, within the exact same VNET where the VM hosting the QuickBooks database server with company files resides.</span></span> 
3. <span data-ttu-id="da9a1-116">[Yayımlama](remoteapp-publish.md) kullanıcılara QuickBooks uygulama</span><span class="sxs-lookup"><span data-stu-id="da9a1-116">[Publish](remoteapp-publish.md) QuickBooks app to users</span></span>
4. <span data-ttu-id="da9a1-117">Azure RemoteApp barındırılan QuickBooks istemcisi başlatmak, standart Windows ağ QuickBooks veritabanı sunucusunu barındıran VM kullanarak gidin ve şirket dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="da9a1-117">Launch the Azure RemoteApp-hosted QuickBooks client, navigate using standard Windows networking to the VM hosting the QuickBooks database server and open the company file.</span></span> 

## <a name="documentation-references"></a><span data-ttu-id="da9a1-118">Belge başvuruları</span><span class="sxs-lookup"><span data-stu-id="da9a1-118">Documentation references</span></span>
* <span data-ttu-id="da9a1-119">QuickBooks [desteklenen yapılandırmalar](http://enterprisesuite.intuit.com/products/enterprise-solutions/technical/#top)</span><span class="sxs-lookup"><span data-stu-id="da9a1-119">QuickBooks [supported configurations](http://enterprisesuite.intuit.com/products/enterprise-solutions/technical/#top)</span></span>
* <span data-ttu-id="da9a1-120">QuickBooks [dağıtım seçenekleri](http://enterprisesuite.intuit.com/everythingenterprise/launchpad/new-user/)</span><span class="sxs-lookup"><span data-stu-id="da9a1-120">QuickBooks [deployment options](http://enterprisesuite.intuit.com/everythingenterprise/launchpad/new-user/)</span></span>

<span data-ttu-id="da9a1-121">Ignite sunumu kontrol edebilirsiniz [temelleri Microsoft Azure RemoteApp yönetimi ve Yönetim](https://channel9.msdn.com/Events/Ignite/2015/BRK3868) -ileri sarma QuickBooks bölümünü almak için 1:02:45.</span><span class="sxs-lookup"><span data-stu-id="da9a1-121">You can also check out my Ignite presentation, [Fundamentals of Microsoft Azure RemoteApp Management and Administration](https://channel9.msdn.com/Events/Ignite/2015/BRK3868) - fast-forward to 1:02:45 to get to the QuickBooks part.</span></span>

## <a name="deployment-architecture"></a><span data-ttu-id="da9a1-122">Dağıtım mimarisi</span><span class="sxs-lookup"><span data-stu-id="da9a1-122">Deployment architecture</span></span>
![QuickBooks + Azure RemoteApp dağıtım](./media/remoteapp-quickbooks/ra-quickbooks.png)

