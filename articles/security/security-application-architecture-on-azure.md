---
title: "Azure, mimari tasarımları içine aaaIntegrate güvenlik | Microsoft Docs"
description: " Bu makalede, Azure toomake hello uygulama ve Hizmetleri mimarisi anlamanıza yardımcı olur, tasarım ve uygulama halinde daha kolay toointegrate güvenlik. "
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TomSh
ms.assetid: 4f2d9386-bda3-4ec8-8b1a-cd0c11242ffc
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/23/2017
ms.author: terrylan
ms.openlocfilehash: cfca8a1a2766f72bc3340c4e3df0019eb8b5a1e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="application-architecture-on-azure"></a><span data-ttu-id="c380e-103">Azure’da uygulama mimarisi</span><span class="sxs-lookup"><span data-stu-id="c380e-103">Application architecture on Azure</span></span>
<span data-ttu-id="c380e-104">toohelp güvenli, bulut tabanlı çözümlerle Microsoft Azure üzerinde güçlü bir mimari temel önemlidir.</span><span class="sxs-lookup"><span data-stu-id="c380e-104">toohelp secure your cloud-based solutions on Microsoft Azure, a strong architectural foundation is critical.</span></span> <span data-ttu-id="c380e-105">Mimarlar tasarımcıları ve uygulayıcılar tüm uygulama ve Hizmetleri mimarisinin güçlü bir bilgilerini yararlanır.</span><span class="sxs-lookup"><span data-stu-id="c380e-105">Architects, designers, and implementers all benefit from a strong knowledge of application and services architecture.</span></span> <span data-ttu-id="c380e-106">Bu temel bilgi bulut tabanlı çözümler tüm hello bileşenlerini anlama ve daha kolay toointegrate güvenlik tasarımı ve uygulama tüm yönlerini olun yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="c380e-106">This foundational knowledge helps you understand all hello components of your cloud-based solutions and make it easier toointegrate security into all aspects of your design and implementation.</span></span>

<span data-ttu-id="c380e-107">Biz sahip hello toohelp, mimari araştırmalar ve tasarımlar ile:</span><span class="sxs-lookup"><span data-stu-id="c380e-107">We have hello following toohelp you with your architectural investigations and designs:</span></span>

* <span data-ttu-id="c380e-108">Mimari infographics</span><span class="sxs-lookup"><span data-stu-id="c380e-108">Architectural infographics</span></span>
* <span data-ttu-id="c380e-109">Mimari planlar</span><span class="sxs-lookup"><span data-stu-id="c380e-109">Architectural blueprints</span></span>
* <span data-ttu-id="c380e-110">Bulut ve kuruluş Sembol kümesi</span><span class="sxs-lookup"><span data-stu-id="c380e-110">Cloud and enterprise symbol set</span></span>
* <span data-ttu-id="c380e-111">3B şeması Visio şablonu</span><span class="sxs-lookup"><span data-stu-id="c380e-111">3D blueprint Visio template</span></span>

## <a name="architectural-infographics"></a><span data-ttu-id="c380e-112">Mimari infographics</span><span class="sxs-lookup"><span data-stu-id="c380e-112">Architectural infographics</span></span>
<span data-ttu-id="c380e-113">Microsoft çeşitli mimari ilgili posterler/infographics yayımlar.</span><span class="sxs-lookup"><span data-stu-id="c380e-113">Microsoft publishes several architectural related posters/infographics.</span></span> <span data-ttu-id="c380e-114">Bunlar:</span><span class="sxs-lookup"><span data-stu-id="c380e-114">They include:</span></span>

* [<span data-ttu-id="c380e-115">Gerçek bulut uygulamaları oluşturma</span><span class="sxs-lookup"><span data-stu-id="c380e-115">Building Real-World Cloud Applications</span></span>](https://azure.microsoft.com/documentation/infographics/building-real-world-cloud-apps/)
* [<span data-ttu-id="c380e-116">Bulut Hizmetleri ile ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="c380e-116">Scaling with Cloud Services</span></span>](https://azure.microsoft.com/documentation/infographics/cloud-services/)

## <a name="architectural-blueprints"></a><span data-ttu-id="c380e-117">Mimari planlar</span><span class="sxs-lookup"><span data-stu-id="c380e-117">Architectural blueprints</span></span>
<span data-ttu-id="c380e-118">Microsoft yayımlar üst düzey bir dizi [mimari planlar](http://aka.ms/azblueprints) gösteren nasıl toobuild belirli türlerdeki Microsoft ürünlerini kullanan sistemleri.</span><span class="sxs-lookup"><span data-stu-id="c380e-118">Microsoft publishes a set of high-level [architectural blueprints](http://aka.ms/azblueprints) showing how toobuild specific types of systems using Microsoft products.</span></span>
<span data-ttu-id="c380e-119">Y: her şeması içerir</span><span class="sxs-lookup"><span data-stu-id="c380e-119">Each blueprint includes a:</span></span>

* <span data-ttu-id="c380e-120">İndirin ve değiştirebileceği düz 2B Visio 2003 tabanlı bir dosya</span><span class="sxs-lookup"><span data-stu-id="c380e-120">Flat 2D Visio 2003-based file that you can download and modify</span></span>
* <span data-ttu-id="c380e-121">Renkli 3B perspektifinin PDF dosyası toointroduce hello şeması tooless teknik izleyicileri</span><span class="sxs-lookup"><span data-stu-id="c380e-121">Colorful 3D perspective PDF file toointroduce hello blueprint tooless technical audiences</span></span>
* <span data-ttu-id="c380e-122">Merhaba 3B sürümü üzerinden anlatan video</span><span class="sxs-lookup"><span data-stu-id="c380e-122">Video that walks through hello 3D version</span></span>

## <a name="cloud-and-enterprise-symbol-set"></a><span data-ttu-id="c380e-123">Bulut ve kuruluş Sembol kümesi</span><span class="sxs-lookup"><span data-stu-id="c380e-123">Cloud and enterprise symbol set</span></span>
<span data-ttu-id="c380e-124">[Merhaba Visio ve video eğitim sembolleri görüntüleme](http://aka.ms/CnESymbolsVideo) ve ardından [hello Bulut ve kuruluş sembol kümesini indirmek](http://aka.ms/CnESymbols) toohelp Azure, Windows Server, SQL Server ve daha fazla açıklamak teknik malzemeleri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c380e-124">[View hello Visio and symbols training video](http://aka.ms/CnESymbolsVideo) and then [download hello Cloud and Enterprise Symbol set](http://aka.ms/CnESymbols) toohelp create technical materials that describe Azure, Windows Server, SQL Server and more.</span></span> <span data-ttu-id="c380e-125">Merhaba kitap trenler toouse Microsoft ürünleri kişiler, mimarisi diyagramları, eğitim malzemelerini, sunuları, veri sayfaları, infographics, teknik incelemeler ve hatta üçüncü taraf books hello simgeleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c380e-125">You can use hello symbols in architecture diagrams, training materials, presentations, datasheets, infographics, whitepapers, and even third party books if hello book trains people toouse Microsoft products.</span></span> <span data-ttu-id="c380e-126">Ancak, bunlar için kullanıcı arabirimleri kullanımda değildir.</span><span class="sxs-lookup"><span data-stu-id="c380e-126">However, they are not meant for use in user interfaces.</span></span>

## <a name="3d-blueprint-visio-template"></a><span data-ttu-id="c380e-127">3B şeması Visio şablonu</span><span class="sxs-lookup"><span data-stu-id="c380e-127">3D blueprint Visio template</span></span>
<span data-ttu-id="c380e-128">Merhaba 3B sürümleri hello [Microsoft mimarisi planlar](http://aka.ms/azblueprints) başlangıçta Microsoft dışı aracında oluşturulmuş.</span><span class="sxs-lookup"><span data-stu-id="c380e-128">hello 3D versions of hello [Microsoft Architecture Blueprints](http://aka.ms/azblueprints) were initially created in a non-Microsoft tool.</span></span> <span data-ttu-id="c380e-129">Yeni Visio 2013 (ve üstü) şablonu 5 Ağustos 2015 tarihinde parçası olarak gönderilen bir [EDX.ORG üzerinde dağıtılmış Microsoft Architecture sertifika indirmelere](https://docs.microsoft.com/azure/architecture/#microsoft-architecture-certification-course).</span><span class="sxs-lookup"><span data-stu-id="c380e-129">A new Visio 2013 (and later) template shipped on August 5, 2015 as part of a [Microsoft Architecture certification course distributed on EDX.ORG](https://docs.microsoft.com/azure/architecture/#microsoft-architecture-certification-course).</span></span>

<span data-ttu-id="c380e-130">Merhaba şablon hello indirmelere dışında da kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="c380e-130">hello template is also available outside hello course.</span></span>

* <span data-ttu-id="c380e-131">[Görüntüleme hello eğitim video](http://aka.ms/3dBlueprintTemplateVideo) yerine getirebileceği bilmesi ilk</span><span class="sxs-lookup"><span data-stu-id="c380e-131">[View hello training video](http://aka.ms/3dBlueprintTemplateVideo) first so you know what it can do</span></span>
* <span data-ttu-id="c380e-132">Merhaba karşıdan [Microsoft 3B şeması Visio şablonu](http://aka.ms/3DBlueprintTemplate)</span><span class="sxs-lookup"><span data-stu-id="c380e-132">Download hello [Microsoft 3d Blueprint Visio Template](http://aka.ms/3DBlueprintTemplate)</span></span>
* <span data-ttu-id="c380e-133">Merhaba karşıdan [Bulut ve kuruluş sembol](https://docs.microsoft.com/azure/architecture/#drawing-symbol-and-icon-sets) hello 3B şablonuyla toouse</span><span class="sxs-lookup"><span data-stu-id="c380e-133">Download hello [Cloud and Enterprise Symbols](https://docs.microsoft.com/azure/architecture/#drawing-symbol-and-icon-sets) toouse with hello 3D template</span></span>
