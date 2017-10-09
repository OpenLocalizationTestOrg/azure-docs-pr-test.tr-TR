---
title: Azure remoteapp'te QuickBooks aaaDeploy | Microsoft Docs
description: "Bilgi nasıl tooshare QuickBooks Azure RemoteApp ile."
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
ms.openlocfilehash: c21b1ac311449be2281f9ce157828260e856f55d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-do-you-deploy-quickbooks-in-azure-remoteapp"></a><span data-ttu-id="42288-103">Azure remoteapp'te QuickBooks nasıl dağıttığınız?</span><span class="sxs-lookup"><span data-stu-id="42288-103">How do you deploy QuickBooks in Azure RemoteApp?</span></span>
> [!IMPORTANT]
> <span data-ttu-id="42288-104">Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır.</span><span class="sxs-lookup"><span data-stu-id="42288-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="42288-105">Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="42288-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="42288-106">Azure remoteapp'te bir uygulama olarak bilgi tooshare QuickBooks aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="42288-106">Use hello following information tooshare QuickBooks as an app in Azure RemoteApp.</span></span>

<span data-ttu-id="42288-107">QuickBooks 2015 kurumsal bir karma veya Bulut koleksiyonunda Azure RemoteApp ile paylaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="42288-107">You can share QuickBooks 2015 Enterprise with Azure RemoteApp in either a hybrid or cloud collection.</span></span> <span data-ttu-id="42288-108">Merhaba şirket dosyası hello Azure RemoteApp sunucularından ayrıdır QuickBooks veritabanı sunucusunu çalıştıran bir VM'de bulunmalıdır.</span><span class="sxs-lookup"><span data-stu-id="42288-108">hello company file must reside on a VM that is running QuickBooks database server that is separate from hello Azure RemoteApp servers.</span></span> <span data-ttu-id="42288-109">Hiçbir zaman hello şirket dosyası, Azure RemoteApp görüntüsüne depolamak - bunu yapmanız durumunda veri kaybını beklenir.</span><span class="sxs-lookup"><span data-stu-id="42288-109">Never store hello company file on your Azure RemoteApp image - data loss is expected if you do this.</span></span> <span data-ttu-id="42288-110">Yalnızca QuickBooks kuruluş QuickBooks veritabanı sunucusuyla standart Windows ağ üzerinden erişilebilir bir dış paylaşımında barındırma hello QuickBooks dosya destekler.</span><span class="sxs-lookup"><span data-stu-id="42288-110">Only QuickBooks Enterprise supports hosting hello QuickBooks file on an external share with QuickBooks database server accessible via standard Windows networking.</span></span>   

> [!IMPORTANT]
> <span data-ttu-id="42288-111">Merhaba hello şirket dosyası barındırma QuickBooks veritabanı sunucusu hello içinde ayrı bir VM'de aynı bulunmalıdır hello Azure RemoteApp koleksiyonu olarak VNET.</span><span class="sxs-lookup"><span data-stu-id="42288-111">hello QuickBooks database server that is hosting hello company file must reside on a separate VM within hello same VNET as hello Azure RemoteApp collection.</span></span>  
> 
> 

## <a name="steps-toodeploy-quickbooks"></a><span data-ttu-id="42288-112">Adımları toodeploy QuickBooks</span><span class="sxs-lookup"><span data-stu-id="42288-112">Steps toodeploy QuickBooks</span></span>
1. <span data-ttu-id="42288-113">Bir Azure VM oluşturun ve QuickBooks, QuickBooks veritabanı sunucusu, yükleyin ve bir Azure VM hello şirket dosyayı yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="42288-113">Create an Azure VM and install QuickBooks, QuickBooks database server, and place hello company file on a Azure VM.</span></span>  <span data-ttu-id="42288-114">Güvenlik duvarı kurallarını yapılandırma emin tooproperly olun.</span><span class="sxs-lookup"><span data-stu-id="42288-114">Make sure tooproperly configure firewall rules.</span></span>
2. <span data-ttu-id="42288-115">QuickBooks yüklemek bir [özel görüntü](remoteapp-imageoptions.md) ve oluşturma bir [Azure RemoteApp koleksiyonu](remoteapp-collections.md), Bulut veya başlangıç içinde nerede hello VM barındırma izin ver hello QuickBooks veritabanı sunucusuyla aynı VNET'i tam karma Şirket dosyaları bulunur.</span><span class="sxs-lookup"><span data-stu-id="42288-115">Install QuickBooks on a [custom image](remoteapp-imageoptions.md) and create an [Azure RemoteApp collection](remoteapp-collections.md), either cloud or hybrid, within hello exact same VNET where hello VM hosting hello QuickBooks database server with company files resides.</span></span> 
3. <span data-ttu-id="42288-116">[Yayımlama](remoteapp-publish.md) QuickBooks uygulama toousers</span><span class="sxs-lookup"><span data-stu-id="42288-116">[Publish](remoteapp-publish.md) QuickBooks app toousers</span></span>
4. <span data-ttu-id="42288-117">Hello Azure RemoteApp barındırılan QuickBooks istemcisi başlatmak, standart Windows toohello VM barındırma hello QuickBooks veritabanı sunucusuna ağ kullanarak gidin ve hello şirket dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="42288-117">Launch hello Azure RemoteApp-hosted QuickBooks client, navigate using standard Windows networking toohello VM hosting hello QuickBooks database server and open hello company file.</span></span> 

## <a name="documentation-references"></a><span data-ttu-id="42288-118">Belge başvuruları</span><span class="sxs-lookup"><span data-stu-id="42288-118">Documentation references</span></span>
* <span data-ttu-id="42288-119">QuickBooks [desteklenen yapılandırmalar](http://enterprisesuite.intuit.com/products/enterprise-solutions/technical/#top)</span><span class="sxs-lookup"><span data-stu-id="42288-119">QuickBooks [supported configurations](http://enterprisesuite.intuit.com/products/enterprise-solutions/technical/#top)</span></span>
* <span data-ttu-id="42288-120">QuickBooks [dağıtım seçenekleri](http://enterprisesuite.intuit.com/everythingenterprise/launchpad/new-user/)</span><span class="sxs-lookup"><span data-stu-id="42288-120">QuickBooks [deployment options](http://enterprisesuite.intuit.com/everythingenterprise/launchpad/new-user/)</span></span>

<span data-ttu-id="42288-121">Ignite sunumu kontrol edebilirsiniz [temelleri Microsoft Azure RemoteApp yönetimi ve Yönetim](https://channel9.msdn.com/Events/Ignite/2015/BRK3868) -ileri sarma too1:02:45 tooget toohello QuickBooks bölümü.</span><span class="sxs-lookup"><span data-stu-id="42288-121">You can also check out my Ignite presentation, [Fundamentals of Microsoft Azure RemoteApp Management and Administration](https://channel9.msdn.com/Events/Ignite/2015/BRK3868) - fast-forward too1:02:45 tooget toohello QuickBooks part.</span></span>

## <a name="deployment-architecture"></a><span data-ttu-id="42288-122">Dağıtım mimarisi</span><span class="sxs-lookup"><span data-stu-id="42288-122">Deployment architecture</span></span>
![QuickBooks + Azure RemoteApp dağıtım](./media/remoteapp-quickbooks/ra-quickbooks.png)

