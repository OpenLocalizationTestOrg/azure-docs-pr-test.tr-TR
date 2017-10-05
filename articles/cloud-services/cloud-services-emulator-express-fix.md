---
title: "Visual Studio bulut Hizmetleri uygulamalarında hata ayıklama için öykünücüsü hızlı kurulumu | Microsoft Docs"
description: "Visual Studio öykünücüsü Express'te etkinleştirmek için C++ yeniden dağıtılabilir yükleme açıklanmaktadır"
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
ms.openlocfilehash: 05d672dcb1335c617bb8d8cae43947bcd5e9ab3d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-emulator-express-to-debug-cloud-services-application-in-vs-2017"></a><span data-ttu-id="7087c-103">Bulut Hizmetleri VS 2017 uygulamada hata ayıklamak için emulator Express kullanma</span><span class="sxs-lookup"><span data-stu-id="7087c-103">Use Emulator Express to debug Cloud Services application in VS 2017</span></span>
<span data-ttu-id="7087c-104">Bu makalede Emulator Express VS 2017 bulut Hizmetleri uygulamalarında hata ayıklama için nasıl kullanılacağı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="7087c-104">This article explains how to use Emulator Express to debug Cloud Services applications in VS 2017.</span></span>

## <a name="background-context"></a><span data-ttu-id="7087c-105">Arka plan bağlamı</span><span class="sxs-lookup"><span data-stu-id="7087c-105">Background context</span></span>
<span data-ttu-id="7087c-106">Öykünücü Express varsayılan olarak, bulut Hizmetleri Web ve çalışan rolleri Visual Studio'da hata ayıklama için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7087c-106">Emulator Express is used by default for debugging Cloud Services Web and Worker roles in Visual Studio.</span></span> <span data-ttu-id="7087c-107">Bu ayar, bulut Hizmetleri proje özellikleri sayfasında belirtilir.</span><span class="sxs-lookup"><span data-stu-id="7087c-107">This setting is specified in the Cloud Services project properties page.</span></span>

![Açık proje özellikleri][0]

![Öykünücü express varsayılan olarak seçilir][1]

<span data-ttu-id="7087c-110">[Visual C++ yeniden dağıtılabilir] [ Visual C++ Redistributable] express Visual Studio öykünücüsü tarafından gereklidir.</span><span class="sxs-lookup"><span data-stu-id="7087c-110">The [Visual C++ Redistributable][Visual C++ Redistributable] for Visual Studio is required by Emulator express.</span></span> <span data-ttu-id="7087c-111">Şu anda Azure yüküyle yüklenmedi.</span><span class="sxs-lookup"><span data-stu-id="7087c-111">Currently it is not installed with the Azure workload.</span></span> <span data-ttu-id="7087c-112">Bulut Hizmetleri uygulamalarında hata ayıklamak için F5 hareketi bu bileşeni yüklemek ve hata ayıklama ile devam etmek için Visual Studio sorar.</span><span class="sxs-lookup"><span data-stu-id="7087c-112">Upon F5 gesture to debug a Cloud Services applications, Visual Studio would prompt to install this component and proceed with debugging.</span></span>

![C++ yeniden dağıtılabilir yükleme sor][2]

<span data-ttu-id="7087c-114">C++ yeniden dağıtılabilir yüklemek için Evet'i tıklatın.</span><span class="sxs-lookup"><span data-stu-id="7087c-114">Click Yes to install C++ Redistributable.</span></span>

![C++ yeniden dağıtılabilir yükleme][3]

<span data-ttu-id="7087c-116">Hata ayıklama oturumları yeniden başlatmak için F5 tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="7087c-116">Press F5 again to launch debugging sessions.</span></span>

![Hata ayıklama başlatılamıyor][4]

![Başarılı hata ayıklama][5]

> <span data-ttu-id="7087c-119">Not: Visual C++ yeniden dağıtılabilir bir kez deneme yüklemektir.</span><span class="sxs-lookup"><span data-stu-id="7087c-119">Note: Installing Visual C++ Redistributable is a onetime effort.</span></span> <span data-ttu-id="7087c-120">Azure SDK'ın eski bir sürümden yükseltme olan ve Emulator Express yüklediyseniz, bu sorunla karşılaştığınızda olmaz.</span><span class="sxs-lookup"><span data-stu-id="7087c-120">If you were upgrading from an older version of Azure SDK and have installed Emulator Express, then you won’t encounter this problem.</span></span>
> 
> 

## <a name="manual-workaround"></a><span data-ttu-id="7087c-121">El ile geçici çözüm</span><span class="sxs-lookup"><span data-stu-id="7087c-121">Manual workaround</span></span>
<span data-ttu-id="7087c-122">Ayrıca yükleyebilirsiniz [Visual C++ yeniden dağıtılabilir] [ Visual C++ Redistributable] el ile ve aynı etkiye nasıl sisteminizde yüklü Visual Studio gibi uygulanır.</span><span class="sxs-lookup"><span data-stu-id="7087c-122">You can also install the [Visual C++ Redistributable][Visual C++ Redistributable] manually and same effect will be applied as how Visual Studio installed it on your system.</span></span>

<span data-ttu-id="7087c-123">[VCRedist_x86.exe][vcredist_x86.exe]</span><span class="sxs-lookup"><span data-stu-id="7087c-123">[vcredist_x86.exe][vcredist_x86.exe]</span></span>

<span data-ttu-id="7087c-124">[VCRedist_x64.exe][vcredist_x64.exe]</span><span class="sxs-lookup"><span data-stu-id="7087c-124">[vcredist_x64.exe][vcredist_x64.exe]</span></span>

## <a name="next-steps"></a><span data-ttu-id="7087c-125">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="7087c-125">Next Steps</span></span>
<span data-ttu-id="7087c-126">Visual Studio bulut Hizmetleri uygulamalarınızda hata ayıklamak için Azure bilgisayar öykünücüsü kullanma hakkında daha fazla bilgi edinin: [kullanarak çalıştırın ve bir bulut hizmeti yerel makinede hata ayıklamak için Emulator Express][Using Emulator Express to run and debug a cloud service on a local machine]</span><span class="sxs-lookup"><span data-stu-id="7087c-126">Learn more about using Azure Computer Emulator to debug your Cloud Services applications in Visual Studio: [Using Emulator Express to run and debug a cloud service on a local machine][Using Emulator Express to run and debug a cloud service on a local machine]</span></span>

[Visual C++ Redistributable]:https://www.microsoft.com/en-us/download/details.aspx?id=30679
[vcredist_x86.exe]:https://download.microsoft.com/download/1/6/B/16B06F60-3B20-4FF2-B699-5E9B7962F9AE/VSU_4/vcredist_x86.exe
[vcredist_x64.exe]:https://download.microsoft.com/download/1/6/B/16B06F60-3B20-4FF2-B699-5E9B7962F9AE/VSU_4/vcredist_x64.exe
[Using Emulator Express to run and debug a cloud service on a local machine]:https://azure.microsoft.com/en-us/documentation/articles/vs-azure-tools-emulator-express-debug-run/

[0]: ./media/cloud-services-emulator-express-fix/vs-05.png
[1]: ./media/cloud-services-emulator-express-fix/vs-06.png
[2]: ./media/cloud-services-emulator-express-fix/vs-01.png
[3]: ./media/cloud-services-emulator-express-fix/vs-02.png
[4]: ./media/cloud-services-emulator-express-fix/vs-03.png
[5]: ./media/cloud-services-emulator-express-fix/vs-04.png
