---
title: "aaaSetup öykünücüsü toodebug bulut Hizmetleri uygulamalarında Visual Studio express | Microsoft Docs"
description: "Nasıl tooinstall hello C++ yeniden dağıtılabilir tooenable Visual Studio öykünücüsü Express'te açıklar"
services: cloud-services
documentationcenter: 
author: cawa
manager: paulyuk
editor: 
ms.assetid: 22b20f7a-23f4-4f7f-b536-3bf1e01adcd1
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 11/02/2016
ms.author: cawa
ms.openlocfilehash: 6fb506f0b1384f2e52310799eb5ae2a102d777bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-emulator-express-toodebug-cloud-services-application-in-vs-2017"></a><span data-ttu-id="37ccd-103">VS 2017 toodebug bulut Hizmetleri uygulama emulator Express kullanın</span><span class="sxs-lookup"><span data-stu-id="37ccd-103">Use Emulator Express toodebug Cloud Services application in VS 2017</span></span>
<span data-ttu-id="37ccd-104">Bu makalede açıklanır nasıl toouse Emulator Express toodebug bulut Hizmetleri uygulamalarında VS 2017.</span><span class="sxs-lookup"><span data-stu-id="37ccd-104">This article explains how toouse Emulator Express toodebug Cloud Services applications in VS 2017.</span></span>

## <a name="background-context"></a><span data-ttu-id="37ccd-105">Arka plan bağlamı</span><span class="sxs-lookup"><span data-stu-id="37ccd-105">Background context</span></span>
<span data-ttu-id="37ccd-106">Öykünücü Express varsayılan olarak, bulut Hizmetleri Web ve çalışan rolleri Visual Studio'da hata ayıklama için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="37ccd-106">Emulator Express is used by default for debugging Cloud Services Web and Worker roles in Visual Studio.</span></span> <span data-ttu-id="37ccd-107">Bu ayar hello bulut Hizmetleri proje özellikleri sayfasında belirtilir.</span><span class="sxs-lookup"><span data-stu-id="37ccd-107">This setting is specified in hello Cloud Services project properties page.</span></span>

![Açık proje özellikleri][0]

![Öykünücü express varsayılan olarak seçilir][1]

<span data-ttu-id="37ccd-110">Merhaba [Visual C++ yeniden dağıtılabilir] [ Visual C++ Redistributable] express Visual Studio öykünücüsü tarafından gereklidir.</span><span class="sxs-lookup"><span data-stu-id="37ccd-110">hello [Visual C++ Redistributable][Visual C++ Redistributable] for Visual Studio is required by Emulator express.</span></span> <span data-ttu-id="37ccd-111">Şu anda Azure iş yükü hello ile yüklenmedi.</span><span class="sxs-lookup"><span data-stu-id="37ccd-111">Currently it is not installed with hello Azure workload.</span></span> <span data-ttu-id="37ccd-112">F5'e bir bulut Hizmetleri uygulamaları toodebug hareket, Visual Studio ve bu bileşen tooinstall sor hata ayıklamaya devam edin.</span><span class="sxs-lookup"><span data-stu-id="37ccd-112">Upon F5 gesture toodebug a Cloud Services applications, Visual Studio would prompt tooinstall this component and proceed with debugging.</span></span>

![C++ yeniden dağıtılabilir yükleme sor][2]

<span data-ttu-id="37ccd-114">Evet tooinstall C++ yeniden dağıtılabilir'i tıklatın.</span><span class="sxs-lookup"><span data-stu-id="37ccd-114">Click Yes tooinstall C++ Redistributable.</span></span>

![C++ yeniden dağıtılabilir yükleme][3]

<span data-ttu-id="37ccd-116">Yeniden toolaunch hata ayıklama oturumları F5'e basın.</span><span class="sxs-lookup"><span data-stu-id="37ccd-116">Press F5 again toolaunch debugging sessions.</span></span>

![Hata ayıklama başlatılamıyor][4]

![Başarılı hata ayıklama][5]

> <span data-ttu-id="37ccd-119">Not: Visual C++ yeniden dağıtılabilir bir kez deneme yüklemektir.</span><span class="sxs-lookup"><span data-stu-id="37ccd-119">Note: Installing Visual C++ Redistributable is a onetime effort.</span></span> <span data-ttu-id="37ccd-120">Azure SDK'ın eski bir sürümden yükseltme olan ve Emulator Express yüklediyseniz, bu sorunla karşılaştığınızda olmaz.</span><span class="sxs-lookup"><span data-stu-id="37ccd-120">If you were upgrading from an older version of Azure SDK and have installed Emulator Express, then you won’t encounter this problem.</span></span>
> 
> 

## <a name="manual-workaround"></a><span data-ttu-id="37ccd-121">El ile geçici çözüm</span><span class="sxs-lookup"><span data-stu-id="37ccd-121">Manual workaround</span></span>
<span data-ttu-id="37ccd-122">Merhaba de yükleyebilirsiniz [Visual C++ yeniden dağıtılabilir] [ Visual C++ Redistributable] el ile ve aynı etkiye nasıl sisteminizde yüklü Visual Studio gibi uygulanır.</span><span class="sxs-lookup"><span data-stu-id="37ccd-122">You can also install hello [Visual C++ Redistributable][Visual C++ Redistributable] manually and same effect will be applied as how Visual Studio installed it on your system.</span></span>

<span data-ttu-id="37ccd-123">[VCRedist_x86.exe][vcredist_x86.exe]</span><span class="sxs-lookup"><span data-stu-id="37ccd-123">[vcredist_x86.exe][vcredist_x86.exe]</span></span>

<span data-ttu-id="37ccd-124">[VCRedist_x64.exe][vcredist_x64.exe]</span><span class="sxs-lookup"><span data-stu-id="37ccd-124">[vcredist_x64.exe][vcredist_x64.exe]</span></span>

## <a name="next-steps"></a><span data-ttu-id="37ccd-125">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="37ccd-125">Next Steps</span></span>
<span data-ttu-id="37ccd-126">Visual Studio bulut Hizmetleri uygulamalarınızda Azure bilgisayar öykünücüsü toodebug kullanma hakkında daha fazla bilgi edinin: [Emulator Express kullanarak toorun ve bir bulut hizmeti yerel makinede hata ayıklama][Using Emulator Express toorun and debug a cloud service on a local machine]</span><span class="sxs-lookup"><span data-stu-id="37ccd-126">Learn more about using Azure Computer Emulator toodebug your Cloud Services applications in Visual Studio: [Using Emulator Express toorun and debug a cloud service on a local machine][Using Emulator Express toorun and debug a cloud service on a local machine]</span></span>

[Visual C++ Redistributable]:https://www.microsoft.com/en-us/download/details.aspx?id=30679
[vcredist_x86.exe]:https://download.microsoft.com/download/1/6/B/16B06F60-3B20-4FF2-B699-5E9B7962F9AE/VSU_4/vcredist_x86.exe
[vcredist_x64.exe]:https://download.microsoft.com/download/1/6/B/16B06F60-3B20-4FF2-B699-5E9B7962F9AE/VSU_4/vcredist_x64.exe
[Using Emulator Express toorun and debug a cloud service on a local machine]:https://azure.microsoft.com/en-us/documentation/articles/vs-azure-tools-emulator-express-debug-run/

[0]: ./media/cloud-services-emulator-express-fix/vs-05.png
[1]: ./media/cloud-services-emulator-express-fix/vs-06.png
[2]: ./media/cloud-services-emulator-express-fix/vs-01.png
[3]: ./media/cloud-services-emulator-express-fix/vs-02.png
[4]: ./media/cloud-services-emulator-express-fix/vs-03.png
[5]: ./media/cloud-services-emulator-express-fix/vs-04.png
