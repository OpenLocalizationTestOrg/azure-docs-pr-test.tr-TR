---
title: "Azure komut satırı derleme | Microsoft Docs"
description: "Azure komut satırı derleme"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 94b35d0d-0d35-48b6-b48b-3641377867fd
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/05/2017
ms.author: kraigb
ms.openlocfilehash: 5fe910e2757dd5ec783538e23e7f52e2f5725b39
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="building-azure-projects-from-the-command-line"></a><span data-ttu-id="a590f-103">Komut satırından Azure projeler derleme</span><span class="sxs-lookup"><span data-stu-id="a590f-103">Building Azure projects from the command line</span></span>
<span data-ttu-id="a590f-104">Microsoft Build Engine (MSBuild) kullanarak, Visual Studio değil yüklendiği yapı Laboratuvar ortamlarında ürünleri oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="a590f-104">Using the Microsoft Build Engine (MSBuild), you can build products in build-lab environments where Visual Studio is not installed.</span></span> <span data-ttu-id="a590f-105">MSBuild genişletilebilir ve Microsoft tarafından tam olarak desteklenen proje dosyaları için bir XML biçimi kullanır.</span><span class="sxs-lookup"><span data-stu-id="a590f-105">MSBuild uses an XML format for project files that's extensible and fully supported by Microsoft.</span></span> <span data-ttu-id="a590f-106">MSBuild dosya biçimini kullanarak, hangi öğeler olmalıdır açıklayabilirsiniz bir veya daha fazla platformlar ve yapılandırmaları için oluşturulmuştur.</span><span class="sxs-lookup"><span data-stu-id="a590f-106">Using the MSBuild file format, you can describe what items must be built for one or more platforms and configurations.</span></span>

<span data-ttu-id="a590f-107">MSBuild komut satırında çalıştırabilirsiniz ve bu konuda, bu yaklaşımı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="a590f-107">You can also run MSBuild at the command line, and this topic describes that approach.</span></span> <span data-ttu-id="a590f-108">Komut satırında özellikleri ayarlayarak, belirli yapılandırmaları bir proje oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a590f-108">By setting properties on the command line, you can build specific configurations of a project.</span></span> <span data-ttu-id="a590f-109">Benzer şekilde, MSBuild derlemeler hedefleri tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a590f-109">Similarly, you can also define the targets that MSBuild builds.</span></span> <span data-ttu-id="a590f-110">Komut satırı parametreleri ve MSBuild hakkında daha fazla bilgi için bkz: [MSBuild komut satırı başvurusu](https://msdn.microsoft.com/library/ms164311.aspx).</span><span class="sxs-lookup"><span data-stu-id="a590f-110">For more information about command-line parameters and MSBuild, see [MSBuild Command-Line Reference](https://msdn.microsoft.com/library/ms164311.aspx).</span></span>

## <a name="msbuild-parameters"></a><span data-ttu-id="a590f-111">MSBuild parametreleri</span><span class="sxs-lookup"><span data-stu-id="a590f-111">MSBuild parameters</span></span>
<span data-ttu-id="a590f-112">MSBuild ile çalıştırmak için bir paket oluşturmak için en basit yolu olan `/t:Publish` seçeneği.</span><span class="sxs-lookup"><span data-stu-id="a590f-112">The simplest way to create a package is to run MSBuild with the `/t:Publish` option.</span></span> <span data-ttu-id="a590f-113">Varsayılan olarak, bu komut bir dizin projenin kök klasörüne göre gibi oluşturur `<ProjectDirectory>\bin\Configuration\app.publish\`.</span><span class="sxs-lookup"><span data-stu-id="a590f-113">By default, this command creates a directory in relation to the root folder for the project, such as `<ProjectDirectory>\bin\Configuration\app.publish\`.</span></span> <span data-ttu-id="a590f-114">Bir Azure projesi derlerken, iki dosya oluşturulur: Paket dosyası kendisi ve eşlik eden yapılandırma dosyası:</span><span class="sxs-lookup"><span data-stu-id="a590f-114">When you build an Azure project, two files are generated: the package file itself and the accompanying configuration file:</span></span>

* <span data-ttu-id="a590f-115">Paket dosyası (`project.cspkg`)</span><span class="sxs-lookup"><span data-stu-id="a590f-115">Package File (`project.cspkg`)</span></span>
* <span data-ttu-id="a590f-116">Yapılandırma dosyası (`ServiceConfiguration.TargetProfile.cscfg`)</span><span class="sxs-lookup"><span data-stu-id="a590f-116">Configuration File (`ServiceConfiguration.TargetProfile.cscfg`)</span></span>

<span data-ttu-id="a590f-117">Varsayılan olarak, her Azure projesi yerel (hata ayıklama) yapılar için bir hizmet yapılandırma dosyası ve başka bir bulut (hazırlık veya üretim) derlemeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="a590f-117">By default, each Azure project includes one service-configuration file for local (debugging) builds and another for cloud (staging or production) builds.</span></span> <span data-ttu-id="a590f-118">Ancak, ekleyebilir veya gerektiği gibi hizmet yapılandırma dosyalarını kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a590f-118">However, you can add or remove service-configuration files as needed.</span></span> <span data-ttu-id="a590f-119">Visual Studio içinde bir paket oluşturduğunuzda, hangi hizmet yapılandırma dosyasında paketini içerecek şekilde istenir.</span><span class="sxs-lookup"><span data-stu-id="a590f-119">When you build a package within Visual Studio, you are asked which service-configuration file to include alongside the package.</span></span> <span data-ttu-id="a590f-120">MSBuild kullanarak bir paket oluşturduğunuzda, yerel hizmet yapılandırma dosyası varsayılan olarak dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="a590f-120">When you build a package by using MSBuild, the local service-configuration file is included by default.</span></span> <span data-ttu-id="a590f-121">Farklı bir hizmet yapılandırma dosyası içerecek şekilde `TargetProfile` MSBuild komut özelliği (`MSBuild /t:Publish /p:TargetProfile=ProfileName`).</span><span class="sxs-lookup"><span data-stu-id="a590f-121">To include a different service-configuration file, set the `TargetProfile` property of the MSBuild command (`MSBuild /t:Publish /p:TargetProfile=ProfileName`).</span></span>

<span data-ttu-id="a590f-122">Yapılandırma dosyalarını ve saklı paket için alternatif bir dizin kullanmak istiyorsanız, yolu kullanarak ayarlamak `/p:PublishDir=Directory\` sondaki eğik çizgi ayırıcı dahil olmak üzere seçeneği.</span><span class="sxs-lookup"><span data-stu-id="a590f-122">If you want to use an alternate directory for the stored package and configuration files, set the path by using the `/p:PublishDir=Directory\` option, including the trailing backslash separator.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a590f-123">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a590f-123">Next steps</span></span>
<span data-ttu-id="a590f-124">Paket oluşturulduktan sonra Azure'a dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a590f-124">After the package is built, you can deploy it to Azure.</span></span> <span data-ttu-id="a590f-125">Bu işlem otomatik hale getirmek nasıl oluşturulduğunu gösteren bir öğretici için bkz [Azure bulut Hizmetleri için devamlı teslim](./cloud-services/cloud-services-dotnet-continuous-delivery.md).</span><span class="sxs-lookup"><span data-stu-id="a590f-125">For a tutorial that demonstrates how to automate that process, see [Continuous Delivery for Cloud Services in Azure](./cloud-services/cloud-services-dotnet-continuous-delivery.md).</span></span>

