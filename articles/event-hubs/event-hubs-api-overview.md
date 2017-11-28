---
title: "aaaAzure olay Hubs API'sine genel bakış | Microsoft Docs"
description: "Kullanılabilir Azure olay hub'ları API'larının genel bakış"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 3f221a0c-182d-4e39-9f3d-3a3c16c5c6ed
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: 46dfcc544ff92642cfd7a967f9ec38a0d8e2bd5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="available-event-hubs-apis"></a><span data-ttu-id="4b405-103">Kullanılabilir olay hub'ları API'leri</span><span class="sxs-lookup"><span data-stu-id="4b405-103">Available Event Hubs APIs</span></span>

## <a name="runtime-apis"></a><span data-ttu-id="4b405-104">Çalışma zamanı API'leri</span><span class="sxs-lookup"><span data-stu-id="4b405-104">Runtime APIs</span></span>

<span data-ttu-id="4b405-105">Merhaba, şu anda kullanılabilir tüm Azure Event Hubs çalışma zamanı istemcileri açıklaması verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="4b405-105">hello following is a description of all currently available Azure Event Hubs runtime clients.</span></span> <span data-ttu-id="4b405-106">Bu kitaplıklar de sınırlı yönetim işlevselliğine bazıları olsa da vardır [belirli kitaplıkları](#management-apis) ayrılmış toomanagement işlemleri.</span><span class="sxs-lookup"><span data-stu-id="4b405-106">While some of these libraries also include limited management functionality, there are also [specific libraries](#management-apis) dedicated toomanagement operations.</span></span> <span data-ttu-id="4b405-107">Bu kitaplıklar Hello çekirdek odağını toosend olan iletiler ve bir event hub'ından alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4b405-107">hello core focus of these libraries is toosend and receive messages from an event hub.</span></span>

<span data-ttu-id="4b405-108">Bkz: [ek bilgi](#additional-information) her çalışma zamanı kitaplığı hello geçerli durumu ile ilgili daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="4b405-108">See [additional information](#additional-information) for more details on hello current status of each runtime library.</span></span>

| <span data-ttu-id="4b405-109">Dil/Platform</span><span class="sxs-lookup"><span data-stu-id="4b405-109">Language/Platform</span></span> | <span data-ttu-id="4b405-110">İstemci paketi</span><span class="sxs-lookup"><span data-stu-id="4b405-110">Client package</span></span> | <span data-ttu-id="4b405-111">EventProcessorHost paketi</span><span class="sxs-lookup"><span data-stu-id="4b405-111">EventProcessorHost package</span></span> | <span data-ttu-id="4b405-112">Depo</span><span class="sxs-lookup"><span data-stu-id="4b405-112">Repository</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="4b405-113">.NET standart</span><span class="sxs-lookup"><span data-stu-id="4b405-113">.NET Standard</span></span> | [<span data-ttu-id="4b405-114">NuGet</span><span class="sxs-lookup"><span data-stu-id="4b405-114">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) | [<span data-ttu-id="4b405-115">NuGet</span><span class="sxs-lookup"><span data-stu-id="4b405-115">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) | [<span data-ttu-id="4b405-116">GitHub</span><span class="sxs-lookup"><span data-stu-id="4b405-116">GitHub</span></span>](https://github.com/azure/azure-event-hubs-dotnet) |
| <span data-ttu-id="4b405-117">.NET framework</span><span class="sxs-lookup"><span data-stu-id="4b405-117">.NET Framework</span></span> | [<span data-ttu-id="4b405-118">NuGet</span><span class="sxs-lookup"><span data-stu-id="4b405-118">NuGet</span></span>](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) | [<span data-ttu-id="4b405-119">NuGet</span><span class="sxs-lookup"><span data-stu-id="4b405-119">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) | <span data-ttu-id="4b405-120">Yok</span><span class="sxs-lookup"><span data-stu-id="4b405-120">N/A</span></span> |
| <span data-ttu-id="4b405-121">Java</span><span class="sxs-lookup"><span data-stu-id="4b405-121">Java</span></span> | [<span data-ttu-id="4b405-122">Maven</span><span class="sxs-lookup"><span data-stu-id="4b405-122">Maven</span></span>](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22) | [<span data-ttu-id="4b405-123">Maven</span><span class="sxs-lookup"><span data-stu-id="4b405-123">Maven</span></span>](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs-eph%22) | [<span data-ttu-id="4b405-124">GitHub</span><span class="sxs-lookup"><span data-stu-id="4b405-124">GitHub</span></span>](https://github.com/Azure/azure-event-hubs-java) |
| <span data-ttu-id="4b405-125">Node</span><span class="sxs-lookup"><span data-stu-id="4b405-125">Node</span></span> | [<span data-ttu-id="4b405-126">NPM</span><span class="sxs-lookup"><span data-stu-id="4b405-126">NPM</span></span>](https://www.npmjs.com/package/azure-event-hubs) | <span data-ttu-id="4b405-127">Yok</span><span class="sxs-lookup"><span data-stu-id="4b405-127">N/A</span></span> | [<span data-ttu-id="4b405-128">GitHub</span><span class="sxs-lookup"><span data-stu-id="4b405-128">GitHub</span></span>](https://github.com/Azure/azure-event-hubs-node) |
| <span data-ttu-id="4b405-129">C</span><span class="sxs-lookup"><span data-stu-id="4b405-129">C</span></span> | <span data-ttu-id="4b405-130">Yok</span><span class="sxs-lookup"><span data-stu-id="4b405-130">N/A</span></span> | <span data-ttu-id="4b405-131">Yok</span><span class="sxs-lookup"><span data-stu-id="4b405-131">N/A</span></span> | [<span data-ttu-id="4b405-132">GitHub</span><span class="sxs-lookup"><span data-stu-id="4b405-132">GitHub</span></span>](https://github.com/Azure/azure-event-hubs-c) |

### <a name="additional-information"></a><span data-ttu-id="4b405-133">Ek bilgiler</span><span class="sxs-lookup"><span data-stu-id="4b405-133">Additional information</span></span>

#### <a name="net"></a><span data-ttu-id="4b405-134">.NET</span><span class="sxs-lookup"><span data-stu-id="4b405-134">.NET</span></span>
<span data-ttu-id="4b405-135">birden çok çalışma zamanları Hello .NET ekosistemi vardır, bu nedenle olay hub'ları için birden çok .NET kitaplıklarına vardır.</span><span class="sxs-lookup"><span data-stu-id="4b405-135">hello .NET ecosystem has multiple runtimes, hence there are multiple .NET libraries for Event Hubs.</span></span> <span data-ttu-id="4b405-136">Merhaba .NET standart kitaplığı hello .NET Framework kitaplığı yalnızca bir .NET Framework ortamında çalıştırılabilir .NET Core veya Merhaba, .NET Framework kullanarak çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4b405-136">hello .NET Standard library can be run using either .NET Core or hello .NET Framework, while hello .NET Framework library can only be run in a .NET Framework environment.</span></span> <span data-ttu-id="4b405-137">.NET Framework ile ilgili daha fazla bilgi için bkz: [framework sürümlerini](https://docs.microsoft.com/dotnet/articles/standard/frameworks#framework-versions).</span><span class="sxs-lookup"><span data-stu-id="4b405-137">For more information on .NET Frameworks, see [framework versions](https://docs.microsoft.com/dotnet/articles/standard/frameworks#framework-versions).</span></span>

#### <a name="node"></a><span data-ttu-id="4b405-138">Node</span><span class="sxs-lookup"><span data-stu-id="4b405-138">Node</span></span>

<span data-ttu-id="4b405-139">Merhaba Node.js kitaplığı şu anda önizlemede ve yan projesi olarak Microsoft çalışanlarına ve dış katkıda bulunanlar tarafından korunur.</span><span class="sxs-lookup"><span data-stu-id="4b405-139">hello Node.js library is currently in preview and is maintained as a side project by Microsoft employees and external contributors.</span></span> <span data-ttu-id="4b405-140">Kaynak kodu da dahil olmak üzere tüm katılımlar Hoş Geldiniz ve incelenecektir.</span><span class="sxs-lookup"><span data-stu-id="4b405-140">All contributions including source code are welcome and will be reviewed.</span></span>

## <a name="management-apis"></a><span data-ttu-id="4b405-141">Yönetim API'leri</span><span class="sxs-lookup"><span data-stu-id="4b405-141">Management APIs</span></span>

<span data-ttu-id="4b405-142">Merhaba, tüm şu anda kullanılabilir yönetim belirli kitaplıkları bir listesi verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="4b405-142">hello following is a listing of all currently available management specific libraries.</span></span> <span data-ttu-id="4b405-143">Bu kitaplıklar hiçbiri çalışma zamanı işlemleri içerir ve Event Hubs varlıkları yönetme hello tek amacı olan.</span><span class="sxs-lookup"><span data-stu-id="4b405-143">None of these libraries contain runtime operations, and are for hello sole purpose of managing Event Hubs entities.</span></span>

| <span data-ttu-id="4b405-144">Dil/Platform</span><span class="sxs-lookup"><span data-stu-id="4b405-144">Language/Platform</span></span> | <span data-ttu-id="4b405-145">Yönetim Paketi</span><span class="sxs-lookup"><span data-stu-id="4b405-145">Management package</span></span> | <span data-ttu-id="4b405-146">Depo</span><span class="sxs-lookup"><span data-stu-id="4b405-146">Repository</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="4b405-147">.NET standart</span><span class="sxs-lookup"><span data-stu-id="4b405-147">.NET Standard</span></span> | [<span data-ttu-id="4b405-148">NuGet</span><span class="sxs-lookup"><span data-stu-id="4b405-148">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Management.EventHub) | [<span data-ttu-id="4b405-149">GitHub</span><span class="sxs-lookup"><span data-stu-id="4b405-149">GitHub</span></span>](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/ResourceManagement/EventHub) |

## <a name="next-steps"></a><span data-ttu-id="4b405-150">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4b405-150">Next steps</span></span>
<span data-ttu-id="4b405-151">Bağlantılar aşağıdaki hello ziyaret ederek Event Hubs hakkında daha fazla bilgi edinebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="4b405-151">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="4b405-152">Event Hubs’a genel bakış</span><span class="sxs-lookup"><span data-stu-id="4b405-152">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="4b405-153">Olay Hub’ı oluşturma</span><span class="sxs-lookup"><span data-stu-id="4b405-153">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="4b405-154">Event Hubs ile ilgili SSS</span><span class="sxs-lookup"><span data-stu-id="4b405-154">Event Hubs FAQ</span></span>](event-hubs-faq.md)