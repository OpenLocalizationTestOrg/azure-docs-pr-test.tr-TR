---
title: "Azure Analysis Services yüksek kullanılabilirlik | Microsoft Docs"
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
ms.openlocfilehash: 84b4c59bac1feeb8611b3a8d783d093ba073e532
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="analysis-services-high-availability"></a><span data-ttu-id="4ff3e-103">Analysis Services yüksek kullanılabilirlik</span><span class="sxs-lookup"><span data-stu-id="4ff3e-103">Analysis Services high availability</span></span>
<span data-ttu-id="4ff3e-104">Bu makalede, Azure Analysis Services sunucuları için yüksek kullanılabilirlik modemlerin açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="4ff3e-104">This article describes assuring high availability for Azure Analysis Services servers.</span></span> 


## <a name="assuring-high-availability-during-a-service-disruption"></a><span data-ttu-id="4ff3e-105">Yüksek oranda kullanılabilir bir hizmet kesintisi sırasında modemlerin</span><span class="sxs-lookup"><span data-stu-id="4ff3e-105">Assuring high availability during a service disruption</span></span>
<span data-ttu-id="4ff3e-106">Ender olsa da, bir Azure veri merkezinde bir kesinti olabilir.</span><span class="sxs-lookup"><span data-stu-id="4ff3e-106">While rare, an Azure data center can have an outage.</span></span> <span data-ttu-id="4ff3e-107">Kesinti oluştuğunda birkaç dakika son veya saat boyunca en son bir iş kesintiye neden olur.</span><span class="sxs-lookup"><span data-stu-id="4ff3e-107">When an outage occurs, it causes a business disruption that might last a few minutes or might last for hours.</span></span> <span data-ttu-id="4ff3e-108">Yüksek kullanılabilirlik, en sık sunucu artıklık ile elde edilir.</span><span class="sxs-lookup"><span data-stu-id="4ff3e-108">High availability is most often achieved with server redundancy.</span></span> <span data-ttu-id="4ff3e-109">Azure Analysis Services ile bir veya daha fazla bölgelerde ek, İkincil sunucuları oluşturarak artıklık elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4ff3e-109">With Azure Analysis Services, you can achieve redundancy by creating additional, secondary servers in one or more regions.</span></span> <span data-ttu-id="4ff3e-110">Veri ve meta verileri bu sunucular üzerinde güvence altına almak için yedek sunucuları oluşturma-sync olduğunda bir bölgede sunucusuyla, çevrimdışı duruma geçti, şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="4ff3e-110">When creating redundant servers, to assure the data and metadata on those servers is in-sync with the server in a region that has gone offline, you can:</span></span>

* <span data-ttu-id="4ff3e-111">Modelleri diğer bölgelerdeki yedek sunucular dağıtın.</span><span class="sxs-lookup"><span data-stu-id="4ff3e-111">Deploy models to redundant servers in other regions.</span></span> <span data-ttu-id="4ff3e-112">Bu yöntem hem birincil sunucu hem de yedek sunucuları paralel veriler işlenirken gerektirir, tüm sunucuların modemlerin eşitleme.</span><span class="sxs-lookup"><span data-stu-id="4ff3e-112">This method requires processing data on both your primary server and redundant servers in-parallel, assuring all servers are in-sync.</span></span>

* <span data-ttu-id="4ff3e-113">Veritabanlarını, birincil sunucu ve geri yükleme yedekli sunucularda yedekleyin.</span><span class="sxs-lookup"><span data-stu-id="4ff3e-113">Back up databases from your primary server and restore on redundant servers.</span></span> <span data-ttu-id="4ff3e-114">Örneğin, Azure depolama gecelik yedekleme otomatikleştirmek ve diğer bölgelerdeki yedekli diğer sunuculara geri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="4ff3e-114">For example, you can automate nightly backups to Azure storage, and restore to other redundant servers in other regions.</span></span> 

<span data-ttu-id="4ff3e-115">Her iki durumda da, birincil sunucunuz bir kesinti oluşursa farklı bir bölgesel veri merkezinde sunucusuna bağlanmak için raporlama istemcileri bağlantı dizelerinde değiştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="4ff3e-115">In either case, if your primary server experiences an outage, you must change the connection strings in reporting clients to connect to the server in a different regional datacenter.</span></span> <span data-ttu-id="4ff3e-116">Bu değişiklik son çare değerlendirilmesi ve yalnızca yıkıcı bölgesel veri merkezi kesintisinden oluşur.</span><span class="sxs-lookup"><span data-stu-id="4ff3e-116">This change should be considered a last resort and only if a catastrophic regional data center outage occurs.</span></span> <span data-ttu-id="4ff3e-117">Ağdaki tüm istemci bağlantıları güncelleştirebilir önce birincil sunucunuzu barındırma veri merkezi kesintisinden tekrar çevrimiçi duruma daha yüksektir.</span><span class="sxs-lookup"><span data-stu-id="4ff3e-117">It's more likely a data center outage hosting your primary server would come back online before you could update connections on all clients.</span></span> 



## <a name="related-information"></a><span data-ttu-id="4ff3e-118">İlgili bilgiler</span><span class="sxs-lookup"><span data-stu-id="4ff3e-118">Related information</span></span>
<span data-ttu-id="4ff3e-119">[Yedekleme ve geri yükleme](analysis-services-backup.md) </span><span class="sxs-lookup"><span data-stu-id="4ff3e-119">[Backup and restore](analysis-services-backup.md) </span></span>  
[<span data-ttu-id="4ff3e-120">Azure Analysis Services yönetme</span><span class="sxs-lookup"><span data-stu-id="4ff3e-120">Manage Azure Analysis Services</span></span>](analysis-services-manage.md) 

