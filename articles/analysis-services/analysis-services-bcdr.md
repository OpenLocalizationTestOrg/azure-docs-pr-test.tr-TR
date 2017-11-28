---
title: "Analysis Services yüksek kullanılabilirlik aaaAzure | Microsoft Docs"
description: "Azure Analysis Services yüksek kullanılabilirlik modemlerin."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
ms.assetid: 
ms.service: analysis-services
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 6e09536c5bd7dc7f88f9b662e1a9f42d2b8c969b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="analysis-services-high-availability"></a><span data-ttu-id="94e37-103">Analysis Services yüksek kullanılabilirlik</span><span class="sxs-lookup"><span data-stu-id="94e37-103">Analysis Services high availability</span></span>
<span data-ttu-id="94e37-104">Bu makalede, Azure Analysis Services sunucuları için yüksek kullanılabilirlik modemlerin açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="94e37-104">This article describes assuring high availability for Azure Analysis Services servers.</span></span> 


## <a name="assuring-high-availability-during-a-service-disruption"></a><span data-ttu-id="94e37-105">Yüksek oranda kullanılabilir bir hizmet kesintisi sırasında modemlerin</span><span class="sxs-lookup"><span data-stu-id="94e37-105">Assuring high availability during a service disruption</span></span>
<span data-ttu-id="94e37-106">Ender olsa da, bir Azure veri merkezinde bir kesinti olabilir.</span><span class="sxs-lookup"><span data-stu-id="94e37-106">While rare, an Azure data center can have an outage.</span></span> <span data-ttu-id="94e37-107">Kesinti oluştuğunda birkaç dakika son veya saat boyunca en son bir iş kesintiye neden olur.</span><span class="sxs-lookup"><span data-stu-id="94e37-107">When an outage occurs, it causes a business disruption that might last a few minutes or might last for hours.</span></span> <span data-ttu-id="94e37-108">Yüksek kullanılabilirlik, en sık sunucu artıklık ile elde edilir.</span><span class="sxs-lookup"><span data-stu-id="94e37-108">High availability is most often achieved with server redundancy.</span></span> <span data-ttu-id="94e37-109">Azure Analysis Services ile bir veya daha fazla bölgelerde ek, İkincil sunucuları oluşturarak artıklık elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="94e37-109">With Azure Analysis Services, you can achieve redundancy by creating additional, secondary servers in one or more regions.</span></span> <span data-ttu-id="94e37-110">Bu sunuculara yedek sunucuları, tooassure hello veri ve meta veri oluşturma-sync olduğunda bir bölgede hello sunucusuyla, çevrimdışı duruma geçti, şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="94e37-110">When creating redundant servers, tooassure hello data and metadata on those servers is in-sync with hello server in a region that has gone offline, you can:</span></span>

* <span data-ttu-id="94e37-111">Diğer bölgelerdeki modelleri tooredundant sunucular dağıtın.</span><span class="sxs-lookup"><span data-stu-id="94e37-111">Deploy models tooredundant servers in other regions.</span></span> <span data-ttu-id="94e37-112">Bu yöntem hem birincil sunucu hem de yedek sunucuları paralel veriler işlenirken gerektirir, tüm sunucuların modemlerin eşitleme.</span><span class="sxs-lookup"><span data-stu-id="94e37-112">This method requires processing data on both your primary server and redundant servers in-parallel, assuring all servers are in-sync.</span></span>

* <span data-ttu-id="94e37-113">Veritabanlarını, birincil sunucu ve geri yükleme yedekli sunucularda yedekleyin.</span><span class="sxs-lookup"><span data-stu-id="94e37-113">Back up databases from your primary server and restore on redundant servers.</span></span> <span data-ttu-id="94e37-114">Örneğin, gece yedekleme tooAzure depolama otomatikleştirmek ve diğer bölgelerdeki tooother yedek sunucular geri yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="94e37-114">For example, you can automate nightly backups tooAzure storage, and restore tooother redundant servers in other regions.</span></span> 

<span data-ttu-id="94e37-115">Her iki durumda da, birincil sunucunuz bir kesinti oluşursa istemcileri tooconnect toohello sunucu farklı bir bölgesel veri merkezinde raporlama hello bağlantı dizeleri değiştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="94e37-115">In either case, if your primary server experiences an outage, you must change hello connection strings in reporting clients tooconnect toohello server in a different regional datacenter.</span></span> <span data-ttu-id="94e37-116">Bu değişiklik son çare değerlendirilmesi ve yalnızca yıkıcı bölgesel veri merkezi kesintisinden oluşur.</span><span class="sxs-lookup"><span data-stu-id="94e37-116">This change should be considered a last resort and only if a catastrophic regional data center outage occurs.</span></span> <span data-ttu-id="94e37-117">Ağdaki tüm istemci bağlantıları güncelleştirebilir önce birincil sunucunuzu barındırma veri merkezi kesintisinden tekrar çevrimiçi duruma daha yüksektir.</span><span class="sxs-lookup"><span data-stu-id="94e37-117">It's more likely a data center outage hosting your primary server would come back online before you could update connections on all clients.</span></span> 



## <a name="related-information"></a><span data-ttu-id="94e37-118">İlgili bilgiler</span><span class="sxs-lookup"><span data-stu-id="94e37-118">Related information</span></span>
<span data-ttu-id="94e37-119">[Yedekleme ve geri yükleme](analysis-services-backup.md) </span><span class="sxs-lookup"><span data-stu-id="94e37-119">[Backup and restore](analysis-services-backup.md) </span></span>  
[<span data-ttu-id="94e37-120">Azure Analysis Services yönetme</span><span class="sxs-lookup"><span data-stu-id="94e37-120">Manage Azure Analysis Services</span></span>](analysis-services-manage.md) 

