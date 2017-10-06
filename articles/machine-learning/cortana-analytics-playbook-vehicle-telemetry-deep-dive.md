---
title: "aaaDeep dalın içine araç durumu tahmin etmek ve alışkanlık - Azure yürüten | Microsoft Docs"
description: "Yürüten alışkanlıklarınıza ve araç sistem durumunu Cortana Intelligence toogain gerçek zamanlı ve Tahmine dayalı Öngörüler Hello özelliklerini kullanın."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: d8866fa6-aba6-40e5-b3b3-33057393c1a8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: ba1448a5081762292561f904d9ec54617c9a5330
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="vehicle-telemetry-analytics-solution-playbook-deep-dive-into-hello-solution"></a><span data-ttu-id="e2337-103">Araç telemetri analizi çözüm playbook: hello çözüm derinlemesine bakış</span><span class="sxs-lookup"><span data-stu-id="e2337-103">Vehicle telemetry analytics solution playbook: deep dive into hello solution</span></span>
<span data-ttu-id="e2337-104">Bu **menü** bu playbook toohello bölümlerine bağlantılar:</span><span class="sxs-lookup"><span data-stu-id="e2337-104">This **menu** links toohello sections of this playbook:</span></span> 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

<span data-ttu-id="e2337-105">Bu bölümde kümede ayrıntısına gider her hello çözüm mimarisi yönergeleri ve özelleştirme işaretçileri gösterilen hello aşamaları.</span><span class="sxs-lookup"><span data-stu-id="e2337-105">This section drills down into each of hello stages depicted in hello Solution Architecture with instructions and pointers for customization.</span></span> 

## <a name="data-sources"></a><span data-ttu-id="e2337-106">Veri Kaynakları</span><span class="sxs-lookup"><span data-stu-id="e2337-106">Data Sources</span></span>
<span data-ttu-id="e2337-107">Merhaba çözüm iki farklı veri kaynakları kullanır:</span><span class="sxs-lookup"><span data-stu-id="e2337-107">hello solution uses two different data sources:</span></span>

* <span data-ttu-id="e2337-108">**Benzetimli araç sinyalleri ve tanılama veri kümesi** ve</span><span class="sxs-lookup"><span data-stu-id="e2337-108">**simulated vehicle signals and diagnostic dataset** and</span></span> 
* <span data-ttu-id="e2337-109">**araç Kataloğu**</span><span class="sxs-lookup"><span data-stu-id="e2337-109">**vehicle catalog**</span></span>

<span data-ttu-id="e2337-110">Bir araç telematik simulator bu çözümün bir parçası olarak dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="e2337-110">A vehicle telematics simulator is included as part of this solution.</span></span> <span data-ttu-id="e2337-111">Tanılama bilgisi yayar ve karşılık gelen toohello durumu hello araç ve düzeni, zaman içinde belirli bir anda yürüten toohello işaret eder.</span><span class="sxs-lookup"><span data-stu-id="e2337-111">It emits diagnostic information and signals corresponding toohello state of hello vehicle and toohello driving pattern at a given point in time.</span></span> <span data-ttu-id="e2337-112">Tıklatın [araç telematik Simulator](http://go.microsoft.com/fwlink/?LinkId=717075) toodownload hello **araç telematik Simulator Visual Studio çözümü** gereksinimlerinize göre özelleştirmeler.</span><span class="sxs-lookup"><span data-stu-id="e2337-112">Click [Vehicle Telematics Simulator](http://go.microsoft.com/fwlink/?LinkId=717075) toodownload hello **Vehicle Telematics Simulator Visual Studio Solution** for customizations based on your requirements.</span></span> <span data-ttu-id="e2337-113">Merhaba araç katalog Toplamıdır toomodel eşleme ile bir başvuru veri kümesi içerir.</span><span class="sxs-lookup"><span data-stu-id="e2337-113">hello vehicle catalog contains a reference dataset with a VIN toomodel mapping.</span></span>

![Araç telematik simulator](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig1-vehicle-telematics-simulator.png)

<span data-ttu-id="e2337-115">*Şekil 1 – araç telematik Simulator*</span><span class="sxs-lookup"><span data-stu-id="e2337-115">*Figure 1 – Vehicle Telematics Simulator*</span></span>

<span data-ttu-id="e2337-116">Bu şema aşağıdaki hello içeren bir JSON olarak biçimlendirilmiş bir veri kümesi olur.</span><span class="sxs-lookup"><span data-stu-id="e2337-116">This is a JSON-formatted dataset that contains hello following schema.</span></span>

| <span data-ttu-id="e2337-117">Sütun</span><span class="sxs-lookup"><span data-stu-id="e2337-117">Column</span></span> | <span data-ttu-id="e2337-118">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e2337-118">Description</span></span> | <span data-ttu-id="e2337-119">Değerler</span><span class="sxs-lookup"><span data-stu-id="e2337-119">Values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e2337-120">TOPLAMIDIR</span><span class="sxs-lookup"><span data-stu-id="e2337-120">VIN</span></span> |<span data-ttu-id="e2337-121">Rastgele oluşturulan araç kimlik numarası</span><span class="sxs-lookup"><span data-stu-id="e2337-121">Randomly generated Vehicle Identification Number</span></span> |<span data-ttu-id="e2337-122">Bu ana 10.000 rastgele oluşturulmuş araç kimlik numaraları listesinden elde edilir.</span><span class="sxs-lookup"><span data-stu-id="e2337-122">This is obtained from a master list of 10,000 randomly generated vehicle identification numbers.</span></span> |
| <span data-ttu-id="e2337-123">Dış sıcaklığı</span><span class="sxs-lookup"><span data-stu-id="e2337-123">Outside temperature</span></span> |<span data-ttu-id="e2337-124">Merhaba hello araç burada yürüten sıcaklık dışında</span><span class="sxs-lookup"><span data-stu-id="e2337-124">hello outside temperature where hello vehicle is driving</span></span> |<span data-ttu-id="e2337-125">0-100 arasında rastgele oluşturulmuş bir sayıya</span><span class="sxs-lookup"><span data-stu-id="e2337-125">Randomly generated number from 0-100</span></span> |
| <span data-ttu-id="e2337-126">Altyapısı sıcaklık</span><span class="sxs-lookup"><span data-stu-id="e2337-126">Engine temperature</span></span> |<span data-ttu-id="e2337-127">Merhaba altyapısı hello araç sıcaklığını</span><span class="sxs-lookup"><span data-stu-id="e2337-127">hello engine temperature of hello vehicle</span></span> |<span data-ttu-id="e2337-128">0-500 arasında rastgele oluşturulmuş sayı</span><span class="sxs-lookup"><span data-stu-id="e2337-128">Randomly generated number from 0-500</span></span> |
| <span data-ttu-id="e2337-129">Hız</span><span class="sxs-lookup"><span data-stu-id="e2337-129">Speed</span></span> |<span data-ttu-id="e2337-130">araç hangi hello yürüten hello altyapısı hızı</span><span class="sxs-lookup"><span data-stu-id="e2337-130">hello engine speed at which hello vehicle is driving</span></span> |<span data-ttu-id="e2337-131">0-100 arasında rastgele oluşturulmuş bir sayıya</span><span class="sxs-lookup"><span data-stu-id="e2337-131">Randomly generated number from 0-100</span></span> |
| <span data-ttu-id="e2337-132">Yakıt</span><span class="sxs-lookup"><span data-stu-id="e2337-132">Fuel</span></span> |<span data-ttu-id="e2337-133">Merhaba araç Hello yakıt düzeyi</span><span class="sxs-lookup"><span data-stu-id="e2337-133">hello fuel level of hello vehicle</span></span> |<span data-ttu-id="e2337-134">Rastgele oluşturulmuş bir sayıya 0-100 (yakıt düzeyi yüzdesi gösterir)</span><span class="sxs-lookup"><span data-stu-id="e2337-134">Randomly generated number from 0-100 (indicates fuel level percentage)</span></span> |
| <span data-ttu-id="e2337-135">EngineOil</span><span class="sxs-lookup"><span data-stu-id="e2337-135">EngineOil</span></span> |<span data-ttu-id="e2337-136">Merhaba araç Hello altyapısı Petrol düzeyi</span><span class="sxs-lookup"><span data-stu-id="e2337-136">hello engine oil level of hello vehicle</span></span> |<span data-ttu-id="e2337-137">Rastgele oluşturulmuş bir sayıya 0-100 (altyapısı Petrol düzeyi yüzdesi gösterir)</span><span class="sxs-lookup"><span data-stu-id="e2337-137">Randomly generated number from 0-100 (indicates engine oil level percentage)</span></span> |
| <span data-ttu-id="e2337-138">Lastiği baskısı</span><span class="sxs-lookup"><span data-stu-id="e2337-138">Tire pressure</span></span> |<span data-ttu-id="e2337-139">Merhaba lastiği baskısı hello araç</span><span class="sxs-lookup"><span data-stu-id="e2337-139">hello tire pressure of hello vehicle</span></span> |<span data-ttu-id="e2337-140">Rastgele oluşturulan numarası 0-50'den (lastiği baskısı düzeyi yüzdesi gösterir)</span><span class="sxs-lookup"><span data-stu-id="e2337-140">Randomly generated number from 0-50 (indicates tire pressure level percentage)</span></span> |
| <span data-ttu-id="e2337-141">Kilometre Sayacı</span><span class="sxs-lookup"><span data-stu-id="e2337-141">Odometer</span></span> |<span data-ttu-id="e2337-142">Merhaba araç Hello Kilometre Sayacı okunması</span><span class="sxs-lookup"><span data-stu-id="e2337-142">hello odometer reading of hello vehicle</span></span> |<span data-ttu-id="e2337-143">0-200000 arasında rastgele oluşturulmuş sayı</span><span class="sxs-lookup"><span data-stu-id="e2337-143">Randomly generated number from 0-200000</span></span> |
| <span data-ttu-id="e2337-144">Accelerator_pedal_position</span><span class="sxs-lookup"><span data-stu-id="e2337-144">Accelerator_pedal_position</span></span> |<span data-ttu-id="e2337-145">Merhaba Hızlandırıcı pedal konumunu hello araç</span><span class="sxs-lookup"><span data-stu-id="e2337-145">hello accelerator pedal position of hello vehicle</span></span> |<span data-ttu-id="e2337-146">Rastgele oluşturulmuş bir sayıya 0-100 (Hızlandırıcı düzeyi yüzdesi gösterir)</span><span class="sxs-lookup"><span data-stu-id="e2337-146">Randomly generated number from 0-100 (indicates accelerator level percentage)</span></span> |
| <span data-ttu-id="e2337-147">Parking_brake_status</span><span class="sxs-lookup"><span data-stu-id="e2337-147">Parking_brake_status</span></span> |<span data-ttu-id="e2337-148">Merhaba araç veya yerleşmiş durumdayken gösterir</span><span class="sxs-lookup"><span data-stu-id="e2337-148">Indicates whether hello vehicle is parked or not</span></span> |<span data-ttu-id="e2337-149">TRUE veya False</span><span class="sxs-lookup"><span data-stu-id="e2337-149">True or False</span></span> |
| <span data-ttu-id="e2337-150">Headlamp_status</span><span class="sxs-lookup"><span data-stu-id="e2337-150">Headlamp_status</span></span> |<span data-ttu-id="e2337-151">Burada hello ön ışık üzerinde olup olmadığını gösterir</span><span class="sxs-lookup"><span data-stu-id="e2337-151">Indicates where hello headlamp is on or not</span></span> |<span data-ttu-id="e2337-152">TRUE veya False</span><span class="sxs-lookup"><span data-stu-id="e2337-152">True or False</span></span> |
| <span data-ttu-id="e2337-153">Brake_pedal_status</span><span class="sxs-lookup"><span data-stu-id="e2337-153">Brake_pedal_status</span></span> |<span data-ttu-id="e2337-154">Merhaba Fren pedal veya basılı olup olmadığını gösterir</span><span class="sxs-lookup"><span data-stu-id="e2337-154">Indicates whether hello brake pedal is pressed or not</span></span> |<span data-ttu-id="e2337-155">TRUE veya False</span><span class="sxs-lookup"><span data-stu-id="e2337-155">True or False</span></span> |
| <span data-ttu-id="e2337-156">Transmission_gear_position</span><span class="sxs-lookup"><span data-stu-id="e2337-156">Transmission_gear_position</span></span> |<span data-ttu-id="e2337-157">Merhaba araç Hello iletim dişli konumu</span><span class="sxs-lookup"><span data-stu-id="e2337-157">hello transmission gear position of hello vehicle</span></span> |<span data-ttu-id="e2337-158">Durumları: ilk olarak, üçüncü, dördüncü beşinci, altıncı seventh, sekizinci ikinci</span><span class="sxs-lookup"><span data-stu-id="e2337-158">States: first, second, third, fourth, fifth, sixth, seventh, eighth</span></span> |
| <span data-ttu-id="e2337-159">Ignition_status</span><span class="sxs-lookup"><span data-stu-id="e2337-159">Ignition_status</span></span> |<span data-ttu-id="e2337-160">Merhaba araç çalışıyor veya durdurulmuştur olup olmadığını gösterir</span><span class="sxs-lookup"><span data-stu-id="e2337-160">Indicates whether hello vehicle is running or stopped</span></span> |<span data-ttu-id="e2337-161">TRUE veya False</span><span class="sxs-lookup"><span data-stu-id="e2337-161">True or False</span></span> |
| <span data-ttu-id="e2337-162">Windshield_wiper_status</span><span class="sxs-lookup"><span data-stu-id="e2337-162">Windshield_wiper_status</span></span> |<span data-ttu-id="e2337-163">Merhaba ön wiper veya açık olup olmadığını gösterir</span><span class="sxs-lookup"><span data-stu-id="e2337-163">Indicates whether hello windshield wiper is turned or not</span></span> |<span data-ttu-id="e2337-164">TRUE veya False</span><span class="sxs-lookup"><span data-stu-id="e2337-164">True or False</span></span> |
| <span data-ttu-id="e2337-165">ABS</span><span class="sxs-lookup"><span data-stu-id="e2337-165">ABS</span></span> |<span data-ttu-id="e2337-166">ABS veya bağlı olup olmadığını gösterir</span><span class="sxs-lookup"><span data-stu-id="e2337-166">Indicates whether ABS is engaged or not</span></span> |<span data-ttu-id="e2337-167">TRUE veya False</span><span class="sxs-lookup"><span data-stu-id="e2337-167">True or False</span></span> |
| <span data-ttu-id="e2337-168">zaman damgası</span><span class="sxs-lookup"><span data-stu-id="e2337-168">Timestamp</span></span> |<span data-ttu-id="e2337-169">Merhaba veri noktası oluşturulduğunda hello zaman damgası</span><span class="sxs-lookup"><span data-stu-id="e2337-169">hello timestamp when hello data point is created</span></span> |<span data-ttu-id="e2337-170">Tarih</span><span class="sxs-lookup"><span data-stu-id="e2337-170">Date</span></span> |
| <span data-ttu-id="e2337-171">Şehir</span><span class="sxs-lookup"><span data-stu-id="e2337-171">City</span></span> |<span data-ttu-id="e2337-172">Merhaba araç Hello konumu</span><span class="sxs-lookup"><span data-stu-id="e2337-172">hello location of hello vehicle</span></span> |<span data-ttu-id="e2337-173">Bu çözümdeki 4 Şehir: Bellevue, Redmond, Sammamish, Seattle</span><span class="sxs-lookup"><span data-stu-id="e2337-173">4 cities in this solution: Bellevue, Redmond, Sammamish, Seattle</span></span> |

<span data-ttu-id="e2337-174">Merhaba araç model başvuru dataset Toplamıdır toohello modeli eşleme içerir.</span><span class="sxs-lookup"><span data-stu-id="e2337-174">hello vehicle model reference dataset contains VIN toohello model mapping.</span></span> 

| <span data-ttu-id="e2337-175">TOPLAMIDIR</span><span class="sxs-lookup"><span data-stu-id="e2337-175">VIN</span></span> | <span data-ttu-id="e2337-176">modeli</span><span class="sxs-lookup"><span data-stu-id="e2337-176">Model</span></span> |
| --- | --- |
| <span data-ttu-id="e2337-177">FHL3O1SA4IEHB4WU1</span><span class="sxs-lookup"><span data-stu-id="e2337-177">FHL3O1SA4IEHB4WU1</span></span> |<span data-ttu-id="e2337-178">Sedan</span><span class="sxs-lookup"><span data-stu-id="e2337-178">Sedan</span></span> |
| <span data-ttu-id="e2337-179">8J0U8XCPRGW4Z3NQE</span><span class="sxs-lookup"><span data-stu-id="e2337-179">8J0U8XCPRGW4Z3NQE</span></span> |<span data-ttu-id="e2337-180">Karma</span><span class="sxs-lookup"><span data-stu-id="e2337-180">Hybrid</span></span> |
| <span data-ttu-id="e2337-181">WORG68Z2PLTNZDBI7</span><span class="sxs-lookup"><span data-stu-id="e2337-181">WORG68Z2PLTNZDBI7</span></span> |<span data-ttu-id="e2337-182">Aile Saloon</span><span class="sxs-lookup"><span data-stu-id="e2337-182">Family Saloon</span></span> |
| <span data-ttu-id="e2337-183">JTHMYHQTEPP4WBMRN</span><span class="sxs-lookup"><span data-stu-id="e2337-183">JTHMYHQTEPP4WBMRN</span></span> |<span data-ttu-id="e2337-184">Sedan</span><span class="sxs-lookup"><span data-stu-id="e2337-184">Sedan</span></span> |
| <span data-ttu-id="e2337-185">W9FTHG27LZN1YWO0Y</span><span class="sxs-lookup"><span data-stu-id="e2337-185">W9FTHG27LZN1YWO0Y</span></span> |<span data-ttu-id="e2337-186">Karma</span><span class="sxs-lookup"><span data-stu-id="e2337-186">Hybrid</span></span> |
| <span data-ttu-id="e2337-187">MHTP9N792PHK08WJM</span><span class="sxs-lookup"><span data-stu-id="e2337-187">MHTP9N792PHK08WJM</span></span> |<span data-ttu-id="e2337-188">Aile Saloon</span><span class="sxs-lookup"><span data-stu-id="e2337-188">Family Saloon</span></span> |
| <span data-ttu-id="e2337-189">EI4QXI2AXVQQING4I</span><span class="sxs-lookup"><span data-stu-id="e2337-189">EI4QXI2AXVQQING4I</span></span> |<span data-ttu-id="e2337-190">Sedan</span><span class="sxs-lookup"><span data-stu-id="e2337-190">Sedan</span></span> |
| <span data-ttu-id="e2337-191">5KKR2VB4WHQH97PF8</span><span class="sxs-lookup"><span data-stu-id="e2337-191">5KKR2VB4WHQH97PF8</span></span> |<span data-ttu-id="e2337-192">Karma</span><span class="sxs-lookup"><span data-stu-id="e2337-192">Hybrid</span></span> |
| <span data-ttu-id="e2337-193">W9NSZ423XZHAONYXB</span><span class="sxs-lookup"><span data-stu-id="e2337-193">W9NSZ423XZHAONYXB</span></span> |<span data-ttu-id="e2337-194">Aile Saloon</span><span class="sxs-lookup"><span data-stu-id="e2337-194">Family Saloon</span></span> |
| <span data-ttu-id="e2337-195">26WJSGHX4MA5ROHNL</span><span class="sxs-lookup"><span data-stu-id="e2337-195">26WJSGHX4MA5ROHNL</span></span> |<span data-ttu-id="e2337-196">Dönüştürülebilir</span><span class="sxs-lookup"><span data-stu-id="e2337-196">Convertible</span></span> |
| <span data-ttu-id="e2337-197">GHLUB6ONKMOSI7E77</span><span class="sxs-lookup"><span data-stu-id="e2337-197">GHLUB6ONKMOSI7E77</span></span> |<span data-ttu-id="e2337-198">İstasyon Wagon</span><span class="sxs-lookup"><span data-stu-id="e2337-198">Station Wagon</span></span> |
| <span data-ttu-id="e2337-199">9C2RHVRVLMEJDBXLP</span><span class="sxs-lookup"><span data-stu-id="e2337-199">9C2RHVRVLMEJDBXLP</span></span> |<span data-ttu-id="e2337-200">Küçük otomobil</span><span class="sxs-lookup"><span data-stu-id="e2337-200">Compact Car</span></span> |
| <span data-ttu-id="e2337-201">BRNHVMZOUJ6EOCP32</span><span class="sxs-lookup"><span data-stu-id="e2337-201">BRNHVMZOUJ6EOCP32</span></span> |<span data-ttu-id="e2337-202">Küçük SUV</span><span class="sxs-lookup"><span data-stu-id="e2337-202">Small SUV</span></span> |
| <span data-ttu-id="e2337-203">VCYVW0WUZNBTM594J</span><span class="sxs-lookup"><span data-stu-id="e2337-203">VCYVW0WUZNBTM594J</span></span> |<span data-ttu-id="e2337-204">Spor araba</span><span class="sxs-lookup"><span data-stu-id="e2337-204">Sports Car</span></span> |
| <span data-ttu-id="e2337-205">HNVCE6YFZSA5M82NY</span><span class="sxs-lookup"><span data-stu-id="e2337-205">HNVCE6YFZSA5M82NY</span></span> |<span data-ttu-id="e2337-206">Orta SUV</span><span class="sxs-lookup"><span data-stu-id="e2337-206">Medium SUV</span></span> |
| <span data-ttu-id="e2337-207">4R30FOR7NUOBL05GJ</span><span class="sxs-lookup"><span data-stu-id="e2337-207">4R30FOR7NUOBL05GJ</span></span> |<span data-ttu-id="e2337-208">İstasyon Wagon</span><span class="sxs-lookup"><span data-stu-id="e2337-208">Station Wagon</span></span> |
| <span data-ttu-id="e2337-209">WYNIIY42VKV6OQS1J</span><span class="sxs-lookup"><span data-stu-id="e2337-209">WYNIIY42VKV6OQS1J</span></span> |<span data-ttu-id="e2337-210">Büyük SUV</span><span class="sxs-lookup"><span data-stu-id="e2337-210">Large SUV</span></span> |
| <span data-ttu-id="e2337-211">8Y5QKG27QET1RBK7I</span><span class="sxs-lookup"><span data-stu-id="e2337-211">8Y5QKG27QET1RBK7I</span></span> |<span data-ttu-id="e2337-212">Büyük SUV</span><span class="sxs-lookup"><span data-stu-id="e2337-212">Large SUV</span></span> |
| <span data-ttu-id="e2337-213">DF6OX2WSRA6511BVG</span><span class="sxs-lookup"><span data-stu-id="e2337-213">DF6OX2WSRA6511BVG</span></span> |<span data-ttu-id="e2337-214">Coupe</span><span class="sxs-lookup"><span data-stu-id="e2337-214">Coupe</span></span> |
| <span data-ttu-id="e2337-215">Z2EOZWZBXAEW3E60T</span><span class="sxs-lookup"><span data-stu-id="e2337-215">Z2EOZWZBXAEW3E60T</span></span> |<span data-ttu-id="e2337-216">Sedan</span><span class="sxs-lookup"><span data-stu-id="e2337-216">Sedan</span></span> |
| <span data-ttu-id="e2337-217">M4TV6IEALD5QDS3IR</span><span class="sxs-lookup"><span data-stu-id="e2337-217">M4TV6IEALD5QDS3IR</span></span> |<span data-ttu-id="e2337-218">Karma</span><span class="sxs-lookup"><span data-stu-id="e2337-218">Hybrid</span></span> |
| <span data-ttu-id="e2337-219">VHRA1Y2TGTA84F00H</span><span class="sxs-lookup"><span data-stu-id="e2337-219">VHRA1Y2TGTA84F00H</span></span> |<span data-ttu-id="e2337-220">Aile Saloon</span><span class="sxs-lookup"><span data-stu-id="e2337-220">Family Saloon</span></span> |
| <span data-ttu-id="e2337-221">R0JAUHT1L1R3BIKI0</span><span class="sxs-lookup"><span data-stu-id="e2337-221">R0JAUHT1L1R3BIKI0</span></span> |<span data-ttu-id="e2337-222">Sedan</span><span class="sxs-lookup"><span data-stu-id="e2337-222">Sedan</span></span> |
| <span data-ttu-id="e2337-223">9230C202Z60XX84AU</span><span class="sxs-lookup"><span data-stu-id="e2337-223">9230C202Z60XX84AU</span></span> |<span data-ttu-id="e2337-224">Karma</span><span class="sxs-lookup"><span data-stu-id="e2337-224">Hybrid</span></span> |
| <span data-ttu-id="e2337-225">T8DNDN5UDCWL7M72H</span><span class="sxs-lookup"><span data-stu-id="e2337-225">T8DNDN5UDCWL7M72H</span></span> |<span data-ttu-id="e2337-226">Aile Saloon</span><span class="sxs-lookup"><span data-stu-id="e2337-226">Family Saloon</span></span> |
| <span data-ttu-id="e2337-227">4WPYRUZII5YV7YA42</span><span class="sxs-lookup"><span data-stu-id="e2337-227">4WPYRUZII5YV7YA42</span></span> |<span data-ttu-id="e2337-228">Sedan</span><span class="sxs-lookup"><span data-stu-id="e2337-228">Sedan</span></span> |
| <span data-ttu-id="e2337-229">D1ZVY26UV2BFGHZNO</span><span class="sxs-lookup"><span data-stu-id="e2337-229">D1ZVY26UV2BFGHZNO</span></span> |<span data-ttu-id="e2337-230">Karma</span><span class="sxs-lookup"><span data-stu-id="e2337-230">Hybrid</span></span> |
| <span data-ttu-id="e2337-231">XUF99EW9OIQOMV7Q7</span><span class="sxs-lookup"><span data-stu-id="e2337-231">XUF99EW9OIQOMV7Q7</span></span> |<span data-ttu-id="e2337-232">Aile Saloon</span><span class="sxs-lookup"><span data-stu-id="e2337-232">Family Saloon</span></span> |
| <span data-ttu-id="e2337-233">8OMCL3LGI7XNCC21U</span><span class="sxs-lookup"><span data-stu-id="e2337-233">8OMCL3LGI7XNCC21U</span></span> |<span data-ttu-id="e2337-234">Dönüştürülebilir</span><span class="sxs-lookup"><span data-stu-id="e2337-234">Convertible</span></span> |
| <span data-ttu-id="e2337-235">…….</span><span class="sxs-lookup"><span data-stu-id="e2337-235">…….</span></span> | |

### <a name="references"></a><span data-ttu-id="e2337-236">Başvurular</span><span class="sxs-lookup"><span data-stu-id="e2337-236">References</span></span>
[<span data-ttu-id="e2337-237">Araç telematik Simulator Visual Studio çözümü</span><span class="sxs-lookup"><span data-stu-id="e2337-237">Vehicle Telematics Simulator Visual Studio Solution</span></span>](http://go.microsoft.com/fwlink/?LinkId=717075) 

[<span data-ttu-id="e2337-238">Azure Event hub'ı</span><span class="sxs-lookup"><span data-stu-id="e2337-238">Azure Event Hub</span></span>](https://azure.microsoft.com/services/event-hubs/)

[<span data-ttu-id="e2337-239">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="e2337-239">Azure Data Factory</span></span>](https://azure.microsoft.com/documentation/learning-paths/data-factory/)

## <a name="ingestion"></a><span data-ttu-id="e2337-240">Alım</span><span class="sxs-lookup"><span data-stu-id="e2337-240">Ingestion</span></span>
<span data-ttu-id="e2337-241">Azure Event Hubs, Stream Analytics ve Data Factory birleşimleridir çevrelerini tooingest hello araç sinyalleri hello tanılama olayları ve gerçek zamanlı ve toplu analizi.</span><span class="sxs-lookup"><span data-stu-id="e2337-241">Combinations of Azure Event Hubs, Stream Analytics, and Data Factory are leveraged tooingest hello vehicle signals, hello diagnostic events, and real-time and batch analytics.</span></span> <span data-ttu-id="e2337-242">Tüm bu bileşenlerin oluşturulur ve hello çözüm dağıtımının bir parçası yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="e2337-242">All these components are created and configured as part of hello solution deployment.</span></span> 

### <a name="real-time-analysis"></a><span data-ttu-id="e2337-243">Gerçek zamanlı analiz</span><span class="sxs-lookup"><span data-stu-id="e2337-243">Real-time analysis</span></span>
<span data-ttu-id="e2337-244">Merhaba araç telematik Simulator hello tarafından oluşturulan olayları yayımlanan toohello olay hub'ı kullanarak hello olay hub'ı SDK.</span><span class="sxs-lookup"><span data-stu-id="e2337-244">hello events generated by hello Vehicle Telematics Simulator are published toohello Event Hub using hello Event Hub SDK.</span></span> <span data-ttu-id="e2337-245">Merhaba Stream Analytics işi hello olay hub'ı bu olayları alır ve işlemleri gerçek zamanlı tooanalyze hello araç sistem durumu verileri hello.</span><span class="sxs-lookup"><span data-stu-id="e2337-245">hello Stream Analytics job ingests these events from hello Event Hub and processes hello data in real time tooanalyze hello vehicle health.</span></span> 

![Olay hub'ı Panosu](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig4-vehicle-telematics-event-hub-dashboard.png) 

<span data-ttu-id="e2337-247">*Şekil 4 - Event Hub Panosu*</span><span class="sxs-lookup"><span data-stu-id="e2337-247">*Figure 4 - Event Hub dashboard*</span></span>

![Veriler işlenirken Analytics iş akışı](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig5-vehicle-telematics-stream-analytics-job-processing-data.png) 

<span data-ttu-id="e2337-249">*Şekil 5 - Stream Analytics işi veri işleme*</span><span class="sxs-lookup"><span data-stu-id="e2337-249">*Figure 5 - Stream Analytics job processing data*</span></span>

<span data-ttu-id="e2337-250">Merhaba Stream Analytics işi;</span><span class="sxs-lookup"><span data-stu-id="e2337-250">hello Stream Analytics job;</span></span>

* <span data-ttu-id="e2337-251">Merhaba Event Hub'ndan verileri alır</span><span class="sxs-lookup"><span data-stu-id="e2337-251">ingests data from hello Event Hub</span></span> 
* <span data-ttu-id="e2337-252">bir birleştirme hello başvuru veri toomap hello araç Toplamıdır toohello karşılık gelen modeli gerçekleştirir</span><span class="sxs-lookup"><span data-stu-id="e2337-252">performs a join with hello reference data toomap hello vehicle VIN toohello corresponding model</span></span> 
* <span data-ttu-id="e2337-253">bunları zengin toplu analiz için Azure blob depolama alanına devam ettirir.</span><span class="sxs-lookup"><span data-stu-id="e2337-253">persists them into Azure blob storage for rich batch analytics.</span></span> 

<span data-ttu-id="e2337-254">Stream Analytics sorgu aşağıdaki hello kullanılan toopersist hello veriler Azure blob depolama alanına bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="e2337-254">hello following Stream Analytics query is used toopersist hello data into Azure blob storage.</span></span> 

![Akış analizi işi sorgu veri alımı için](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig6-vehicle-telematics-stream-analytics-job-query-for-data-ingestion.png) 

<span data-ttu-id="e2337-256">*Şekil 6 - Stream Analytics işi veri alımı için sorgu*</span><span class="sxs-lookup"><span data-stu-id="e2337-256">*Figure 6 - Stream Analytics job query for data ingestion*</span></span>

### <a name="batch-analysis"></a><span data-ttu-id="e2337-257">Toplu iş analiz</span><span class="sxs-lookup"><span data-stu-id="e2337-257">Batch analysis</span></span>
<span data-ttu-id="e2337-258">Biz de benzetimli araç sinyalleri ve tanılama veri kümesi daha zengin toplu analizi için ek bir birim oluşturduğunu.</span><span class="sxs-lookup"><span data-stu-id="e2337-258">We are also generating an additional volume of simulated vehicle signals and diagnostic dataset for richer batch analytics.</span></span> <span data-ttu-id="e2337-259">Gerekli tooensure toplu işlem için iyi temsili veri birimi budur.</span><span class="sxs-lookup"><span data-stu-id="e2337-259">This is required tooensure a good representative data volume for batch processing.</span></span> <span data-ttu-id="e2337-260">Bu amaçla hello Azure Data Factory iş akışı toogenerate "PrepareSampleDataPipeline" adlı işlem hattını kullanıyoruz bir yılın tutarında benzetimli araç sinyalleri ve tanılama veri kümesi.</span><span class="sxs-lookup"><span data-stu-id="e2337-260">For this purpose, we are using a pipeline named "PrepareSampleDataPipeline" in hello Azure Data Factory workflow toogenerate one year's worth of simulated vehicle signals and diagnostic dataset.</span></span> <span data-ttu-id="e2337-261">Tıklatın [Data Factory özel etkinlik](http://go.microsoft.com/fwlink/?LinkId=717077) toodownload hello Data Factory özel DotNet etkinlik özelleştirmeleri için Visual Studio çözümü gereksinimlerinize göre tabanlı.</span><span class="sxs-lookup"><span data-stu-id="e2337-261">Click [Data Factory custom activity](http://go.microsoft.com/fwlink/?LinkId=717077) toodownload hello Data Factory custom DotNet activity Visual Studio solution for customizations based on your requirements.</span></span> 

![Toplu iş akışı işleme için örnek verileri hazırlama](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig7-vehicle-telematics-prepare-sample-data-for-batch-processing.png) 

<span data-ttu-id="e2337-263">*Şekil 7 - toplu işleme iş akışı için örnek verileri hazırlama*</span><span class="sxs-lookup"><span data-stu-id="e2337-263">*Figure 7 - Prepare Sample data for batch processing workflow*</span></span>

<span data-ttu-id="e2337-264">Merhaba ardışık düzen oluşur özel bir ADF .net etkinliği, burada göster:</span><span class="sxs-lookup"><span data-stu-id="e2337-264">hello pipeline consists of a custom ADF .Net Activity, show here:</span></span>

![PrepareSampleDataPipeline etkinliği](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig8-vehicle-telematics-prepare-sample-data-pipeline.png) 

<span data-ttu-id="e2337-266">*Şekil 8 - PrepareSampleDataPipeline*</span><span class="sxs-lookup"><span data-stu-id="e2337-266">*Figure 8 - PrepareSampleDataPipeline*</span></span>

<span data-ttu-id="e2337-267">Merhaba ardışık düzen başarıyla yürütür ve "RawCarEventsTable" veri kümesi "Hazır", yıllık değerinde benzetimli araç sinyaller ve tanılama işaretlenmiş sonra veri üretilir.</span><span class="sxs-lookup"><span data-stu-id="e2337-267">Once hello pipeline executes successfully and "RawCarEventsTable" dataset is marked "Ready", one-year worth of simulated vehicle signals and diagnostic data are produced.</span></span> <span data-ttu-id="e2337-268">Merhaba aşağıdakilere bakın klasör ve dosya depolama hesabınızda hello "connectedcar" kapsayıcısı altında oluşturulan:</span><span class="sxs-lookup"><span data-stu-id="e2337-268">You see hello following folder and file created in your storage account under hello "connectedcar" container:</span></span>

![PrepareSampleDataPipeline çıkış](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig9-vehicle-telematics-prepare-sample-data-pipeline-output.png) 

<span data-ttu-id="e2337-270">*Şekil 9 - PrepareSampleDataPipeline çıkış*</span><span class="sxs-lookup"><span data-stu-id="e2337-270">*Figure 9 - PrepareSampleDataPipeline Output*</span></span>

### <a name="references"></a><span data-ttu-id="e2337-271">Başvurular</span><span class="sxs-lookup"><span data-stu-id="e2337-271">References</span></span>
[<span data-ttu-id="e2337-272">Akış alımı için Azure olay hub'ı SDK</span><span class="sxs-lookup"><span data-stu-id="e2337-272">Azure Event Hub SDK for stream ingestion</span></span>](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)

<span data-ttu-id="e2337-273">[Azure Data Factory veri taşıma özellikleri](../data-factory/data-factory-data-movement-activities.md)
[Azure veri fabrikası DotNet etkinliği](../data-factory/data-factory-use-custom-activities.md)</span><span class="sxs-lookup"><span data-stu-id="e2337-273">[Azure Data Factory data movement capabilities](../data-factory/data-factory-data-movement-activities.md)
[Azure Data Factory DotNet Activity](../data-factory/data-factory-use-custom-activities.md)</span></span>

[<span data-ttu-id="e2337-274">Örnek verileri hazırlama için azure veri fabrikası DotNet etkinlik visual studio çözümü</span><span class="sxs-lookup"><span data-stu-id="e2337-274">Azure Data Factory DotNet activity visual studio solution for preparing sample data</span></span>](http://go.microsoft.com/fwlink/?LinkId=717077) 

## <a name="partition-hello-dataset"></a><span data-ttu-id="e2337-275">Bölüm hello veri kümesi</span><span class="sxs-lookup"><span data-stu-id="e2337-275">Partition hello dataset</span></span>
<span data-ttu-id="e2337-276">Merhaba ham yarı yapılandırılmış araç sinyalleri ve tanılama veri kümesi yıl/ay biçimine hello veri hazırlık adımı bölümlenir.</span><span class="sxs-lookup"><span data-stu-id="e2337-276">hello raw semi-structured vehicle signals and diagnostic dataset are partitioned in hello data preparation step into a YEAR/MONTH format.</span></span> <span data-ttu-id="e2337-277">Bu bölümleme daha verimli sorgulama yükseltir ve hataya üzerinden bir blob hesap toohello gelen hello ilk hesap olarak sonraki etkinleştirerek ölçeklenebilir uzun vadeli depolama dolar.</span><span class="sxs-lookup"><span data-stu-id="e2337-277">This partitioning promotes more efficient querying and scalable long-term storage by enabling fault-over from one blob account toohello next as hello first account fills up.</span></span> 

>[!NOTE] 
><span data-ttu-id="e2337-278">Bu adım hello çözümüne uygulanabilir yalnızca toobatch işleme bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="e2337-278">This step in hello solution is applicable only toobatch processing.</span></span>

<span data-ttu-id="e2337-279">Giriş ve çıkış veri veri yönetimi:</span><span class="sxs-lookup"><span data-stu-id="e2337-279">Input and output data data management:</span></span>

* <span data-ttu-id="e2337-280">Merhaba **çıktı verilerini** (etiketli *PartitionedCarEventsTable*) toobe uzun bir süre için veri hello Müşteri'nin "Data Lake" Merhaba temel / "rawest" form olarak tutulur.</span><span class="sxs-lookup"><span data-stu-id="e2337-280">hello **output data** (labeled *PartitionedCarEventsTable*) is toobe kept for a long period of time as hello foundational/"rawest" form of data in hello customer's "Data Lake".</span></span> 
* <span data-ttu-id="e2337-281">Merhaba **giriş verileri** toothis ardışık düzen genellikle atılmasını gerektirebilir gibi hello çıktı verileri içeren tam uygunluğunu toohello giriş - yalnızca (sonraki kullanım için daha iyi bölümlenmiş) depolanır.</span><span class="sxs-lookup"><span data-stu-id="e2337-281">hello **input data** toothis pipeline would typically be discarded as hello output data has full fidelity toohello input - it's just stored (partitioned) better for subsequent use.</span></span>

![Bölüm araba olayları iş akışı](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig10-vehicle-telematics-partition-car-events-workflow.png)

<span data-ttu-id="e2337-283">*Şekil 10 – bölüm araba olayları iş akışı*</span><span class="sxs-lookup"><span data-stu-id="e2337-283">*Figure 10 – Partition Car Events workflow*</span></span>

<span data-ttu-id="e2337-284">Hdınsight Hive etkinliği "PartitionCarEventsPipeline içinde" kullanarak Hello ham verileri bölümlenen.</span><span class="sxs-lookup"><span data-stu-id="e2337-284">hello raw data is partitioned using a Hive HDInsight activity in "PartitionCarEventsPipeline".</span></span> <span data-ttu-id="e2337-285">Merhaba örnek verileri bir yıl için 1. adımda oluşturulan yıl/AYA göre bölümlenmiş.</span><span class="sxs-lookup"><span data-stu-id="e2337-285">hello sample data generated in step 1 for a year is partitioned by YEAR/MONTH.</span></span> <span data-ttu-id="e2337-286">Merhaba kullanılan toogenerate araç sinyalleri ve tanılama verilerini her ay yılın (toplam 12 bölümler) bölümlerdir.</span><span class="sxs-lookup"><span data-stu-id="e2337-286">hello partitions are used toogenerate vehicle signals and diagnostic data for each month (total 12 partitions) of a year.</span></span> 

![PartitionCarEventsPipeline etkinliği](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig11-vehicle-telematics-partition-car-events-pipeline.png)

<span data-ttu-id="e2337-288">*Şekil 11 - PartitionCarEventsPipeline*</span><span class="sxs-lookup"><span data-stu-id="e2337-288">*Figure 11 - PartitionCarEventsPipeline*</span></span>

<span data-ttu-id="e2337-289">***PartitionConnectedCarEvents Hive betiği***</span><span class="sxs-lookup"><span data-stu-id="e2337-289">***PartitionConnectedCarEvents Hive Script***</span></span>

<span data-ttu-id="e2337-290">Merhaba "partitioncarevents.hql" adlı aşağıdaki Hive betiğini bölümleme için kullanılır ve hello "\demo\src\connectedcar\scripts" klasöründe hello indirilen ZIP bulunur.</span><span class="sxs-lookup"><span data-stu-id="e2337-290">hello following Hive script, named "partitioncarevents.hql", is used for partitioning and is located in hello "\demo\src\connectedcar\scripts" folder of hello downloaded zip.</span></span> 
    
    SET hive.exec.dynamic.partition=true;
    SET hive.exec.dynamic.partition.mode = nonstrict;
    set hive.cli.print.header=true;

    DROP TABLE IF EXISTS RawCarEvents; 
    CREATE EXTERNAL TABLE RawCarEvents 
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:RAWINPUT}'; 

    DROP TABLE IF EXISTS PartitionedCarEvents; 
    CREATE EXTERNAL TABLE PartitionedCarEvents 
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string
    ) partitioned by (YearNo int, MonthNo int) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:PARTITIONEDOUTPUT}';

    DROP TABLE IF EXISTS Stage_RawCarEvents; 
    CREATE TABLE IF NOT EXISTS Stage_RawCarEvents 
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string,
                YearNo                             int,
                MonthNo                         int) 
    ROW FORMAT delimited fields terminated by ',' LINES TERMINATED BY '10';

    INSERT OVERWRITE TABLE Stage_RawCarEvents
    SELECT
        vin,            
        model,
        timestamp,
        outsidetemperature,
        enginetemperature,
        speed,
        fuel,
        engineoil,
        tirepressure,
        odometer,
        city,
        accelerator_pedal_position,
        parking_brake_status,
        headlamp_status,
        brake_pedal_status,
        transmission_gear_position,
        ignition_status,
        windshield_wiper_status,
        abs,
        gendate,
        Year(gendate),
        Month(gendate)

    FROM RawCarEvents WHERE Year(gendate) = ${hiveconf:Year} AND Month(gendate) = ${hiveconf:Month}; 

    INSERT OVERWRITE TABLE PartitionedCarEvents PARTITION(YearNo, MonthNo) 
    SELECT
        vin,            
        model,
        timestamp,
        outsidetemperature,
        enginetemperature,
        speed,
        fuel,
        engineoil,
        tirepressure,
        odometer,
        city,
        accelerator_pedal_position,
        parking_brake_status,
        headlamp_status,
        brake_pedal_status,
        transmission_gear_position,
        ignition_status,
        windshield_wiper_status,
        abs,
        gendate,
        YearNo,
        MonthNo
    FROM Stage_RawCarEvents WHERE YearNo = ${hiveconf:Year} AND MonthNo = ${hiveconf:Month};

<span data-ttu-id="e2337-291">Merhaba ardışık düzen başarılı bir şekilde yürütüldükten sonra depolama hesabınızda hello "connectedcar" kapsayıcısı altında oluşturulan bölümler aşağıdaki hello bakın.</span><span class="sxs-lookup"><span data-stu-id="e2337-291">Once hello pipeline is executed successfully, you see hello following partitions generated in your storage account under hello "connectedcar" container.</span></span>

![Bölümlenmiş çıktı](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig12-vehicle-telematics-partitioned-output.png)

<span data-ttu-id="e2337-293">*Şekil 12 - bölümlenmiş çıktı*</span><span class="sxs-lookup"><span data-stu-id="e2337-293">*Figure 12 - Partitioned Output*</span></span>

<span data-ttu-id="e2337-294">Merhaba veri artık iyileştirilmiş, daha yönetilebilir ve toogain zengin toplu Öngörüler işlenmesi için hazırdır.</span><span class="sxs-lookup"><span data-stu-id="e2337-294">hello data is now optimized, is more manageable and ready for further processing toogain rich batch insights.</span></span> 

## <a name="data-analysis"></a><span data-ttu-id="e2337-295">Veri analizi</span><span class="sxs-lookup"><span data-stu-id="e2337-295">Data Analysis</span></span>
<span data-ttu-id="e2337-296">Bu bölümde, nasıl toocombine Azure akış analizi, Azure Machine Learning, Azure Data Factory ve Azure Hdınsight zengin için Gelişmiş bkz araç sistem durumu ve yürüten alışkanlıklarınıza.</span><span class="sxs-lookup"><span data-stu-id="e2337-296">In this section, you see how toocombine Azure Stream Analytics, Azure Machine Learning, Azure Data Factory, and Azure HDInsight for rich advanced analytics on vehicle health and driving habits.</span></span> <span data-ttu-id="e2337-297">Burada üç alt bölümleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="e2337-297">There are three subsections here:</span></span>

1. <span data-ttu-id="e2337-298">**Machine Learning**: Bu alt bölümde Bakım ve toosafety sorunları nedeniyle geri çekme gerektiren taşıtlardan bakım gerektiren bu çözüm toopredict taşıtlardan içinde kullanmış hello anomali algılama deneme ilgili bilgiler içerir.</span><span class="sxs-lookup"><span data-stu-id="e2337-298">**Machine Learning**: This subsection contains information on hello anomaly detection experiment that we have used in this solution toopredict vehicles requiring servicing maintenance and vehicles requiring recalls due toosafety issues.</span></span>
2. <span data-ttu-id="e2337-299">**Gerçek zamanlı analiz**: Bu alt bölümde hello Stream Analytics sorgu dili kullanarak ve hello machine learning faaliyete geçirmeye yönelik ilgili hello gerçek zamanlı analiz denemesini özel bir uygulama kullanarak gerçek zamanlı bilgiler içerir.</span><span class="sxs-lookup"><span data-stu-id="e2337-299">**Real-time analysis**: This subsection contains information regarding hello real-time analytics using hello Stream Analytics Query Language and operationalizing hello machine learning experiment in real time using a custom application.</span></span>
3. <span data-ttu-id="e2337-300">**Toplu analiz**: Bu alt bölümde dönüştürme ve Azure Hdınsight ve Azure Machine Learning Azure Data Factory tarafından kullanıma hazır hale getirilmiş kullanarak hello toplu veri işleme hello ilgili bilgiler içerir.</span><span class="sxs-lookup"><span data-stu-id="e2337-300">**Batch analysis**: This subsection contains information regarding hello transforming and processing of hello batch data using Azure HDInsight and Azure Machine Learning operationalized by Azure Data Factory.</span></span>

### <a name="machine-learning"></a><span data-ttu-id="e2337-301">Machine Learning</span><span class="sxs-lookup"><span data-stu-id="e2337-301">Machine Learning</span></span>
<span data-ttu-id="e2337-302">Amacımız burada Bakım veya belirli sistem durumu istatistiklerine bağlı geri çağırma gerektiren toopredict hello taşıtlardan ' dir.</span><span class="sxs-lookup"><span data-stu-id="e2337-302">Our goal here is toopredict hello vehicles that require maintenance or recall based on certain heath statistics.</span></span> <span data-ttu-id="e2337-303">Varsayımlar aşağıdaki hello vermiyoruz</span><span class="sxs-lookup"><span data-stu-id="e2337-303">We make hello following assumptions</span></span>

* <span data-ttu-id="e2337-304">Aşağıdaki üç koşul hello biri doğruysa hello taşıtlardan gerektiren **bakım Bakım**:</span><span class="sxs-lookup"><span data-stu-id="e2337-304">If one of hello following three conditions are true, hello vehicles require **servicing maintenance**:</span></span>
  
  * <span data-ttu-id="e2337-305">Lastiği baskısı düşük</span><span class="sxs-lookup"><span data-stu-id="e2337-305">Tire pressure is low</span></span>
  * <span data-ttu-id="e2337-306">Altyapısı Petrol düzeyinin düşük</span><span class="sxs-lookup"><span data-stu-id="e2337-306">Engine oil level is low</span></span>
  * <span data-ttu-id="e2337-307">Altyapısı sıcaklık yüksek</span><span class="sxs-lookup"><span data-stu-id="e2337-307">Engine temperature is high</span></span>
* <span data-ttu-id="e2337-308">Aşağıdaki koşullar hello biri doğruysa hello taşıtlardan olabilir bir **güvenlik sorunu** ve gerektiren **geri çağırma**:</span><span class="sxs-lookup"><span data-stu-id="e2337-308">If one of hello following conditions are true, hello vehicles may have a **safety issue** and require **recall**:</span></span>
  
  * <span data-ttu-id="e2337-309">Altyapısı sıcaklık yüksek olduğu, ancak dış sıcaklığı düşük</span><span class="sxs-lookup"><span data-stu-id="e2337-309">Engine temperature is high but outside temperature is low</span></span>
  * <span data-ttu-id="e2337-310">Altyapısı sıcaklık düşük olduğu, ancak dış sıcaklığı yüksek</span><span class="sxs-lookup"><span data-stu-id="e2337-310">Engine temperature is low but outside temperature is high</span></span>

<span data-ttu-id="e2337-311">Merhaba önceki gereksinimlerine bağlı olarak, iki ayrı modelleri toodetect anormallikleri, araç bakım algılaması için diğeri için araç geri çağırma algılama oluşturduk.</span><span class="sxs-lookup"><span data-stu-id="e2337-311">Based on hello previous requirements, we have created two separate models toodetect anomalies, one for vehicle maintenance detection, and one for vehicle recall detection.</span></span> <span data-ttu-id="e2337-312">Her iki bu modellerinde hello yerleşik asıl bileşen analiz (PCA) algoritması anomali algılama için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e2337-312">In both these models, hello built-in Principal Component Analysis (PCA) algorithm is used for anomaly detection.</span></span> 

<span data-ttu-id="e2337-313">**Bakım algılama modeli**</span><span class="sxs-lookup"><span data-stu-id="e2337-313">**Maintenance detection model**</span></span>

<span data-ttu-id="e2337-314">Üç göstergeleri - lastiği baskısı, altyapısı Petrol veya altyapısı sıcaklık - birini ilgili koşul uymazsa hello bakım algılama modelini bir anomali bildirir.</span><span class="sxs-lookup"><span data-stu-id="e2337-314">If one of three indicators - tire pressure, engine oil, or engine temperature - satisfies its respective condition, hello maintenance detection model reports an anomaly.</span></span> <span data-ttu-id="e2337-315">Sonuç olarak, yalnızca tooconsider hello model oluşturmanın bu üç değişkenleri ihtiyacımız var.</span><span class="sxs-lookup"><span data-stu-id="e2337-315">As a result, we only need tooconsider these three variables in building hello model.</span></span> <span data-ttu-id="e2337-316">Azure Machine learning'de bizim denemesinde önce kullandığımız bir **Select Columns in Dataset sütun** modülü tooextract bu üç değişkenleri.</span><span class="sxs-lookup"><span data-stu-id="e2337-316">In our experiment in Azure Machine Learning, we first use a **Select Columns in Dataset** module tooextract these three variables.</span></span> <span data-ttu-id="e2337-317">Sonraki hello PCA tabanlı anomali algılama modülü toobuild hello anomali algılama modelini kullanın.</span><span class="sxs-lookup"><span data-stu-id="e2337-317">Next we use hello PCA-based anomaly detection module toobuild hello anomaly detection model.</span></span> 

<span data-ttu-id="e2337-318">Asıl bileşen analiz (PCA) uygulanan toofeature seçim, Sınıflandırma ve anomali algılama olabilir machine learning'de kurulmuş bir tekniktir.</span><span class="sxs-lookup"><span data-stu-id="e2337-318">Principal Component Analysis (PCA) is an established technique in machine learning that can be applied toofeature selection, classification, and anomaly detection.</span></span> <span data-ttu-id="e2337-319">PCA durum büyük olasılıkla bağıntılı değişkenleri asıl bileşenleri adı verilen değerleri kümesine içeren bir dizi dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="e2337-319">PCA converts a set of case containing possibly correlated variables, into a set of values called principal components.</span></span> <span data-ttu-id="e2337-320">böylece daha kolay özellikleri ve anormallikleri tanımlanabilir hello anahtar PCA tabanlı model tooproject veri küçük boyutlu bir alanı üzerine olur.</span><span class="sxs-lookup"><span data-stu-id="e2337-320">hello key idea of PCA-based modeling is tooproject data onto a lower-dimensional space so that features and anomalies can be more easily identified.</span></span>

<span data-ttu-id="e2337-321">Her yeni giriş çok hello için algılama modelini hello anomali algılayıcısı ilk hello eigenvectors üzerinde kendi projeksiyon hesaplar ve sonra yeniden yapılandırma hata hesaplar hello normalleştirilmiş.</span><span class="sxs-lookup"><span data-stu-id="e2337-321">For each new input too hello detection model, hello anomaly detector first computes its projection on hello eigenvectors, and then computes hello normalized reconstruction error.</span></span> <span data-ttu-id="e2337-322">Merhaba anomali puanı bu normalleştirilmiş hatasıdır.</span><span class="sxs-lookup"><span data-stu-id="e2337-322">This normalized error is hello anomaly score.</span></span> <span data-ttu-id="e2337-323">Merhaba yüksek hello hata hello daha anormal hello örneğidir.</span><span class="sxs-lookup"><span data-stu-id="e2337-323">hello higher hello error, hello more anomalous hello instance is.</span></span> 

<span data-ttu-id="e2337-324">3 boyutlu boşluk nokta koordinatları lastiği baskısı, altyapısı Petrol ve altyapısı sıcaklık tarafından tanımlanan hello bakım algılama sorun her kayıt kabul edilebilir.</span><span class="sxs-lookup"><span data-stu-id="e2337-324">In hello maintenance detection problem, each record can be considered as a point in a 3-dimensional space defined by tire pressure, engine oil, and engine temperature coordinates.</span></span> <span data-ttu-id="e2337-325">toocapture bu anormallikleri biz hello özgün veriler hello 3 boyutlu alanda PCA kullanarak 2 boyutlu boşluk yansıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e2337-325">toocapture these anomalies, we can project hello original data in hello 3-dimensional space onto a 2-dimensional space using PCA.</span></span> <span data-ttu-id="e2337-326">Bu nedenle, PCA toobe 2 hello parametre bileşenleri toouse sayısını ayarlar.</span><span class="sxs-lookup"><span data-stu-id="e2337-326">Thus, we set hello parameter Number of components toouse in PCA toobe 2.</span></span> <span data-ttu-id="e2337-327">Bu parametre, PCA tabanlı anomali algılama uygulama önemli bir rol oynar.</span><span class="sxs-lookup"><span data-stu-id="e2337-327">This parameter plays an important role in applying PCA-based anomaly detection.</span></span> <span data-ttu-id="e2337-328">PCA kullanarak planlanması verileri sonra Biz bu anormallikleri daha kolay tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e2337-328">After projecting data using PCA, we can identify these anomalies more easily.</span></span>

<span data-ttu-id="e2337-329">**Geri çağırma anomali algılama modelini** hello Select Columns in Dataset ve PCA tabanlı anomali sütun kullanırız hello geri çağırma anomali algılama modelinde, benzer bir şekilde algılama modüller.</span><span class="sxs-lookup"><span data-stu-id="e2337-329">**Recall anomaly detection model** In hello recall anomaly detection model, we use hello Select Columns in Dataset and PCA-based anomaly detection modules in a similar way.</span></span> <span data-ttu-id="e2337-330">Özellikle de önce ayıklamanız biz üç değişkenleri - altyapısı sıcaklık, dış sıcaklık ve hızı - hello kullanarak **Select Columns in Dataset sütun** modülü.</span><span class="sxs-lookup"><span data-stu-id="e2337-330">Specifically, we first extract three variables - engine temperature, outside temperature, and speed - using hello **Select Columns in Dataset** module.</span></span> <span data-ttu-id="e2337-331">Ayrıca hello hızı eklediğimiz hello altyapısı sıcaklık genellikle olduğundan değişkeni bağıntılı toohello hızı.</span><span class="sxs-lookup"><span data-stu-id="e2337-331">We also include hello speed variable since hello engine temperature typically is correlated toohello speed.</span></span> <span data-ttu-id="e2337-332">Sonraki PCA tabanlı anomali algılama modülü tooproject hello veri 2 boyutlu boşluk üzerine hello 3 boyutlu alanından kullanırız.</span><span class="sxs-lookup"><span data-stu-id="e2337-332">Next we use PCA-based anomaly detection module tooproject hello data from hello 3-dimensional space onto a 2-dimensional space.</span></span> <span data-ttu-id="e2337-333">Hello geri çağırma ölçütlerini karşılamadı ve bu nedenle altyapısı sıcaklık ve dış sıcaklığı yüksek oranda olumsuz bağıntılı zaman hello araç geri çağırma gerektirir.</span><span class="sxs-lookup"><span data-stu-id="e2337-333">hello recall criteria are satisfied and so hello vehicle requires recall when engine temperature and outside temperature are highly negatively correlated.</span></span> <span data-ttu-id="e2337-334">PCA tabanlı anomali algılama algoritması kullanan, biz hello anormallikleri PCA gerçekleştirildikten sonra yakalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e2337-334">Using PCA-based anomaly detection algorithm, we can capture hello anomalies after performing PCA.</span></span> 

<span data-ttu-id="e2337-335">Her iki modeli eğitimindeki Bakım veya geri çağırma hello giriş verisi tootrain hello PCA tabanlı anomali algılama modeli olarak gerektirmez toouse normal veri ihtiyacımız var.</span><span class="sxs-lookup"><span data-stu-id="e2337-335">When training either model, we need toouse normal data, which does not require maintenance or recall as hello input data tootrain hello PCA-based anomaly detection model.</span></span> <span data-ttu-id="e2337-336">Deneme Puanlama hello Hello araç Bakım veya geri çağırma gerektirip gerektirmediğini eğitilmiş hello anomali algılama modelini toodetect kullanırız.</span><span class="sxs-lookup"><span data-stu-id="e2337-336">In hello scoring experiment, we use hello trained anomaly detection model toodetect whether or not hello vehicle requires maintenance or recall.</span></span> 

### <a name="real-time-analysis"></a><span data-ttu-id="e2337-337">Gerçek zamanlı analiz</span><span class="sxs-lookup"><span data-stu-id="e2337-337">Real-time analysis</span></span>
<span data-ttu-id="e2337-338">Stream Analytics SQL sorgusu aşağıdaki hello kullanılan tüm tooget hello ortalama hello araç hızı, yakıt düzeyi, altyapısı sıcaklık, Kilometre Sayacı okuma, lastiği baskısı, altyapısı Petrol düzeyinin ve diğerleri gibi önemli araç parametreleri.</span><span class="sxs-lookup"><span data-stu-id="e2337-338">hello following Stream Analytics SQL Query is used tooget hello average of all hello important vehicle parameters like vehicle speed, fuel level, engine temperature, odometer reading, tire pressure, engine oil level, and others.</span></span> <span data-ttu-id="e2337-339">Merhaba ortalamalar olan kullanılan toodetect anormallikleri vermek uyarıları ve belirlemek hello belirli bölgede işletilen taşıtlardan genel sistem durumu koşulları ve toodemographics ilişkilendirmek.</span><span class="sxs-lookup"><span data-stu-id="e2337-339">hello averages are used toodetect anomalies, issue alerts, and determine hello overall health conditions of vehicles operated in specific region and then correlate it toodemographics.</span></span> 

![Stream Analytics sorgu için gerçek zamanlı işleme](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig13-vehicle-telematics-stream-analytics-query-for-real-time-processing.png)

<span data-ttu-id="e2337-341">*Şekil 13 – Stream Analytics sorgu için gerçek zamanlı işleme*</span><span class="sxs-lookup"><span data-stu-id="e2337-341">*Figure 13 – Stream Analytics query for real-time processing*</span></span>

<span data-ttu-id="e2337-342">Tüm hello ortalamalar 3 saniyelik TumblingWindow hesaplanır.</span><span class="sxs-lookup"><span data-stu-id="e2337-342">All hello averages are calculated over a 3-second TumblingWindow.</span></span> <span data-ttu-id="e2337-343">Biz çakışmayan ve bitişik zaman aralıkları gerektiren bu yana TubmlingWindow bu durumda kullanıyoruz.</span><span class="sxs-lookup"><span data-stu-id="e2337-343">We are using TubmlingWindow in this case since we require non-overlapping and contiguous time intervals.</span></span> 

<span data-ttu-id="e2337-344">Azure Stream Analytics, tüm hello "Pencereleme" özellikleri hakkında daha fazla toolearn tıklatın [Pencereleme (Azure akış analizi)](https://msdn.microsoft.com/library/azure/dn835019.aspx).</span><span class="sxs-lookup"><span data-stu-id="e2337-344">toolearn more about all hello "Windowing" capabilities in Azure Stream Analytics, click [Windowing (Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835019.aspx).</span></span>

<span data-ttu-id="e2337-345">**Gerçek zamanlı tahmin**</span><span class="sxs-lookup"><span data-stu-id="e2337-345">**Real-time prediction**</span></span>

<span data-ttu-id="e2337-346">Bir uygulama gerçek zamanlı hello çözüm toooperationalize hello machine learning modelini bir parçası olarak dahil edilmiştir.</span><span class="sxs-lookup"><span data-stu-id="e2337-346">An application is included as part of hello solution toooperationalize hello machine learning model in real time.</span></span> <span data-ttu-id="e2337-347">"RealTimeDashboardApp" olarak adlandırılan bu uygulama oluşturulur ve hello çözüm dağıtımının bir parçası yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="e2337-347">This application called “RealTimeDashboardApp” is created and configured as part of hello solution deployment.</span></span> <span data-ttu-id="e2337-348">Merhaba uygulaması hello aşağıdakileri gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="e2337-348">hello application performs hello following:</span></span>

1. <span data-ttu-id="e2337-349">Burada Stream Analytics hello olayları bir modelinde sürekli yayımlama tooan olay hub'ı örneği dinler.</span><span class="sxs-lookup"><span data-stu-id="e2337-349">Listens tooan Event Hub instance where Stream Analytics is publishing hello events in a pattern continuously.</span></span> <span data-ttu-id="e2337-350">![Yayımlama hello veri akış analizi sorgu](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig14-vehicle-telematics-stream-analytics-query-for-publishing.png) *Şekil 14 – yayımlama hello veri tooan Stream Analytics sorgu çıktısını olay hub'ı örneği*</span><span class="sxs-lookup"><span data-stu-id="e2337-350">![Stream Analytics query for publishing hello data](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig14-vehicle-telematics-stream-analytics-query-for-publishing.png) *Figure 14 – Stream Analytics query for publishing hello data tooan output Event Hub instance*</span></span> 
2. <span data-ttu-id="e2337-351">Bu uygulamayı alır her olay için:</span><span class="sxs-lookup"><span data-stu-id="e2337-351">For every event that this application receives:</span></span> 
   
   * <span data-ttu-id="e2337-352">Machine Learning istek-yanıt Puanlama (RR) uç noktası kullanarak işlemleri hello verileri.</span><span class="sxs-lookup"><span data-stu-id="e2337-352">Processes hello data using Machine Learning Request-Response Scoring (RRS) endpoint.</span></span> <span data-ttu-id="e2337-353">Merhaba RRS endpoint hello dağıtımının bir parçası otomatik olarak yayımlanır.</span><span class="sxs-lookup"><span data-stu-id="e2337-353">hello RRS endpoint is automatically published as part of hello deployment.</span></span>
   * <span data-ttu-id="e2337-354">Merhaba RRS çıkışı hello itme API'lerini kullanarak yayımlanan tooa Power BI dataset yapılır.</span><span class="sxs-lookup"><span data-stu-id="e2337-354">hello RRS output is published tooa Power BI dataset using hello push APIs.</span></span>

<span data-ttu-id="e2337-355">Bu desen de toointegrate bir iş kolu (LoB) uygulaması ile Merhaba gerçek zamanlı analiz akış, uyarılar, bildirimler ve mesajlaşma gibi senaryolar için istediğiniz uygulanabilir tooscenarios olur.</span><span class="sxs-lookup"><span data-stu-id="e2337-355">This pattern is also applicable tooscenarios in which you want toointegrate a Line of Business (LoB) application with hello real-time analytics flow, for scenarios such as alerts, notifications, and messaging.</span></span>

<span data-ttu-id="e2337-356">Tıklatın [RealtimeDashboardApp indirme](http://go.microsoft.com/fwlink/?LinkId=717078) toodownload hello özelleştirmeler RealtimeDashboardApp Visual Studio çözümü.</span><span class="sxs-lookup"><span data-stu-id="e2337-356">Click [RealtimeDashboardApp download](http://go.microsoft.com/fwlink/?LinkId=717078) toodownload hello RealtimeDashboardApp Visual Studio solution for customizations.</span></span> 

<span data-ttu-id="e2337-357">**tooexecute hello gerçek zamanlı Pano uygulaması**</span><span class="sxs-lookup"><span data-stu-id="e2337-357">**tooexecute hello Real-time Dashboard Application**</span></span>
1. <span data-ttu-id="e2337-358">Ayıklayın ve yerel olarak Kaydet ![RealtimeDashboardApp klasörü](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig16-vehicle-telematics-realtimedashboardapp-folder.png) *Şekil 16 – RealtimeDashboardApp klasörü*</span><span class="sxs-lookup"><span data-stu-id="e2337-358">Extract and save locally ![RealtimeDashboardApp folder](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig16-vehicle-telematics-realtimedashboardapp-folder.png) *Figure 16 – RealtimeDashboardApp folder*</span></span>  
2. <span data-ttu-id="e2337-359">Merhaba uygulaması RealtimeDashboardApp.exe yürütme</span><span class="sxs-lookup"><span data-stu-id="e2337-359">Execute hello application RealtimeDashboardApp.exe</span></span>
3. <span data-ttu-id="e2337-360">Geçerli Power BI kimlik bilgilerini sağlayın, oturum açın ve Kabul Et'i tıklatın</span><span class="sxs-lookup"><span data-stu-id="e2337-360">Provide valid Power BI credentials, sign in and click Accept</span></span> ![Gerçek zamanlı Pano uygulama oturum açma tooPower BI](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig17a-vehicle-telematics-realtimedashboardapp-sign-in-to-powerbi.png) ![Gerçek zamanlı Pano uygulaması son oturum açma BI tooPower](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig17b-vehicle-telematics-realtimedashboardapp-sign-in-to-powerbi.png) 

<span data-ttu-id="e2337-363">*Şekil 17 – RealtimeDashboardApp: Oturum açma tooPower BI*</span><span class="sxs-lookup"><span data-stu-id="e2337-363">*Figure 17 – RealtimeDashboardApp: Sign-in tooPower BI*</span></span>

>[!NOTE] 
><span data-ttu-id="e2337-364">Tooflush hello Power BI dataset istiyorsanız hello RealtimeDashboardApp hello "flushdata" parametresiyle yürütün:</span><span class="sxs-lookup"><span data-stu-id="e2337-364">If you want tooflush hello Power BI dataset, execute hello RealtimeDashboardApp with hello "flushdata" parameter:</span></span> 

    RealtimeDashboardApp.exe -flushdata


### <a name="batch-analysis"></a><span data-ttu-id="e2337-365">Toplu iş analiz</span><span class="sxs-lookup"><span data-stu-id="e2337-365">Batch analysis</span></span>
<span data-ttu-id="e2337-366">Merhaba burada nasıl Contoso Motors tooshow düzeni, kullanım davranışı ve araç durumunu yürüten üzerinde hello Azure işlem özellikleri tooharness büyük veri toogain zengin Öngörüler yararlanan hedeftir.</span><span class="sxs-lookup"><span data-stu-id="e2337-366">hello goal here is tooshow how Contoso Motors utilizes hello Azure compute capabilities tooharness big data toogain rich insights on driving pattern, usage behavior, and vehicle health.</span></span> <span data-ttu-id="e2337-367">Bu, mümkün kılar:</span><span class="sxs-lookup"><span data-stu-id="e2337-367">This makes it possible to:</span></span>

* <span data-ttu-id="e2337-368">Merhaba müşteri deneyimini geliştirmek ve alışkanlık ve yakıt verimli yönlendirmeli davranışları yürüten üzerinde Öngörüler sağlayarak daha ucuzdur yapın</span><span class="sxs-lookup"><span data-stu-id="e2337-368">Improve hello customer experience and make it cheaper by providing insights on driving habits and fuel efficient driving behaviors</span></span>
* <span data-ttu-id="e2337-369">Proaktif olarak müşteriler ve bunların yönlendirmeli patters toogovern iş kararları hakkında bilgi edinin ve hello en iyi sınıf ürünler ve hizmetler sağlar</span><span class="sxs-lookup"><span data-stu-id="e2337-369">Learn proactively about customers and their driving patters toogovern business decisions and provide hello best in class products & services</span></span>

<span data-ttu-id="e2337-370">Bu çözümde, biz ölçümleri aşağıdaki hello hedeflediğiniz:</span><span class="sxs-lookup"><span data-stu-id="e2337-370">In this solution, we are targeting hello following metrics:</span></span>

1. <span data-ttu-id="e2337-371">**Davranış yürüten etkin**: hello eğilimini hello modelleri, konumları, yönlendirmeli koşullar ve agresif yönlendirmeli modeli hello yıl toogain ınsights süresini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="e2337-371">**Aggressive driving behavior**: Identifies hello trend of hello models, locations, driving conditions, and time of hello year toogain insights on aggressive driving patterns.</span></span> <span data-ttu-id="e2337-372">Contoso Motors bu Öngörüler kişiselleştirilmiş yeni özellikler ve kullanım tabanlı sigorta yürüten pazarlama kampanyaları için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e2337-372">Contoso Motors can use these insights for marketing campaigns, driving new personalized features and usage-based insurance.</span></span>
2. <span data-ttu-id="e2337-373">**Yakıt Al verimli yönlendirmeli davranışı**: hello eğilimini hello modelleri, konumları, yönlendirmeli koşullar ve yakıt verimli yönlendirmeli modeli hello yıl toogain ınsights süresini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="e2337-373">**Fuel efficient driving behavior**: Identifies hello trend of hello models, locations, driving conditions, and time of hello year toogain insights on fuel efficient driving patterns.</span></span> <span data-ttu-id="e2337-374">Contoso Motors bu Öngörüler, pazarlama kampanyalarının için yeni özellikler yürüten kullanabilirsiniz ve etkili ve ortam kolay yönlendirmeli alışkanlıklarınıza için öngörülü raporlama toohello sürücüleri maliyeti.</span><span class="sxs-lookup"><span data-stu-id="e2337-374">Contoso Motors can use these insights for marketing campaigns, driving new features and proactive reporting toohello drivers for cost effective and environment friendly driving habits.</span></span> 
3. <span data-ttu-id="e2337-375">**Modelleri geri çağırma**: Merhaba anomali algılama machine learning deneme faaliyete geçirmeye yönelik geri çekme gerektiren modelleri tanımlar</span><span class="sxs-lookup"><span data-stu-id="e2337-375">**Recall models**: Identifies models requiring recalls by operationalizing hello anomaly detection machine learning experiment</span></span>

<span data-ttu-id="e2337-376">Her bir bu ölçümleri hello ayrıntılara göz atalım,</span><span class="sxs-lookup"><span data-stu-id="e2337-376">Let's look into hello details of each of these metrics,</span></span>

<span data-ttu-id="e2337-377">**Agresif yönlendirmeli düzeni**</span><span class="sxs-lookup"><span data-stu-id="e2337-377">**Aggressive driving pattern**</span></span>

<span data-ttu-id="e2337-378">Merhaba bölümlenmiş araç sinyalleri ve tanılama veri işlenir koşullar ve sergiler diğer parametreleri "kullanarak Hive toodetermine hello modelleri, konum, araç AggresiveDrivingPatternPipeline" adlı hello ardışık düzeninde agresif yürüten Desen yürüten.</span><span class="sxs-lookup"><span data-stu-id="e2337-378">hello partitioned vehicle signals and diagnostic data are processed in hello pipeline named "AggresiveDrivingPatternPipeline" using Hive toodetermine hello models, location, vehicle, driving conditions, and other parameters that exhibits aggressive driving pattern.</span></span>

<span data-ttu-id="e2337-379">![Agresif yönlendirmeli düzeni iş akışı](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig18-vehicle-telematics-aggressive-driving-pattern.png) 
*Şekil 18 – agresif yönlendirmeli düzeni iş akışı*</span><span class="sxs-lookup"><span data-stu-id="e2337-379">![Aggressive driving pattern workflow](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig18-vehicle-telematics-aggressive-driving-pattern.png) 
*Figure 18 – Aggressive driving pattern workflow*</span></span>


<span data-ttu-id="e2337-380">***Agresif yönlendirmeli düzeni Hive sorgusu***</span><span class="sxs-lookup"><span data-stu-id="e2337-380">***Aggressive driving pattern Hive query***</span></span>

<span data-ttu-id="e2337-381">Merhaba "aggresivedriving.hql agresif yönlendirmeli koşul düzeni çözümlemek için kullanılan" adlandırılmış Hive betiğini hello indirilen ZIP "\demo\src\connectedcar\scripts" klasör bulunur.</span><span class="sxs-lookup"><span data-stu-id="e2337-381">hello Hive script named "aggresivedriving.hql" used for analyzing aggressive driving condition pattern is located at "\demo\src\connectedcar\scripts" folder of hello downloaded zip.</span></span> 

    DROP TABLE IF EXISTS PartitionedCarEvents; 
    CREATE EXTERNAL TABLE PartitionedCarEvents
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:PARTITIONEDINPUT}';

    DROP TABLE IF EXISTS CarEventsAggresive; 
    CREATE EXTERNAL TABLE CarEventsAggresive
    (
                   vin                         string, 
                model                        string,
                timestamp                    string,
                city                        string,
                speed                          string,
                transmission_gear_position    string,
                brake_pedal_status            string,
                Year                        string,
                Month                        string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:AGGRESIVEOUTPUT}';



    INSERT OVERWRITE TABLE CarEventsAggresive
    select
    vin,
    model,
    timestamp,
    city,
    speed,
    transmission_gear_position,
    brake_pedal_status,
    "${hiveconf:Year}" as Year,
    "${hiveconf:Month}" as Month
    from PartitionedCarEvents
    where transmission_gear_position IN ('fourth', 'fifth', 'sixth', 'seventh', 'eight') AND brake_pedal_status = '1' AND speed >= '50'


<span data-ttu-id="e2337-382">Bu araç'ın iletim dişli konum, Fren pedal durumu ve hız toodetect reckless/en yüksek hızda düzeni braking dayalı davranışı yürüten agresif hello bileşimini kullanır.</span><span class="sxs-lookup"><span data-stu-id="e2337-382">It uses hello combination of vehicle's transmission gear position, brake pedal status, and speed toodetect reckless/aggressive driving behavior based on braking pattern at high speed.</span></span> 

<span data-ttu-id="e2337-383">Merhaba ardışık düzen başarılı bir şekilde yürütüldükten sonra depolama hesabınızda hello "connectedcar" kapsayıcısı altında oluşturulan bölümler aşağıdaki hello bakın.</span><span class="sxs-lookup"><span data-stu-id="e2337-383">Once hello pipeline is executed successfully, you see hello following partitions generated in your storage account under hello "connectedcar" container.</span></span>

![AggressiveDrivingPatternPipeline çıkış](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig19-vehicle-telematics-aggressive-driving-pattern-output.png) 

<span data-ttu-id="e2337-385">*Şekil 19 – AggressiveDrivingPatternPipeline çıkış*</span><span class="sxs-lookup"><span data-stu-id="e2337-385">*Figure 19 – AggressiveDrivingPatternPipeline output*</span></span>

<span data-ttu-id="e2337-386">**Yakıt verimli yönlendirmeli düzeni**</span><span class="sxs-lookup"><span data-stu-id="e2337-386">**Fuel efficient driving pattern**</span></span>

<span data-ttu-id="e2337-387">araç sinyalleri Hello bölümlenmiş ve tanılama veri "FuelEfficientDrivingPatternPipeline" adlı hello ardışık düzeninde işlenir.</span><span class="sxs-lookup"><span data-stu-id="e2337-387">hello partitioned vehicle signals and diagnostic data are processed in hello pipeline named "FuelEfficientDrivingPatternPipeline".</span></span> <span data-ttu-id="e2337-388">Hive kullanılan toodetermine hello modelleri, konum, araç, yönlendirmeli koşullar ve yakıt verimli yönlendirmeli düzeni sergilemesine diğer özellikleri ' dir.</span><span class="sxs-lookup"><span data-stu-id="e2337-388">Hive is used toodetermine hello models, location, vehicle, driving conditions, and other properties that exhibit fuel efficient driving pattern.</span></span>

![Fuel-Efficient yönlendirmeli düzeni](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig19-vehicle-telematics-fuel-efficient-driving-pattern.png) 

<span data-ttu-id="e2337-390">*Şekil 20 – Fuel-efficient yönlendirmeli düzeni iş akışı*</span><span class="sxs-lookup"><span data-stu-id="e2337-390">*Figure 20 – Fuel-efficient driving pattern workflow*</span></span>

<span data-ttu-id="e2337-391">***Yakıt verimli yönlendirmeli düzeni Hive sorgusu***</span><span class="sxs-lookup"><span data-stu-id="e2337-391">***Fuel efficient driving pattern Hive query***</span></span>

<span data-ttu-id="e2337-392">Merhaba "fuelefficientdriving.hql agresif yönlendirmeli koşul düzeni çözümlemek için kullanılan" adlandırılmış Hive betiğini hello indirilen ZIP "\demo\src\connectedcar\scripts" klasör bulunur.</span><span class="sxs-lookup"><span data-stu-id="e2337-392">hello Hive script named "fuelefficientdriving.hql" used for analyzing aggressive driving condition pattern is located at "\demo\src\connectedcar\scripts" folder of hello downloaded zip.</span></span> 

    DROP TABLE IF EXISTS PartitionedCarEvents; 
    CREATE EXTERNAL TABLE PartitionedCarEvents
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:PARTITIONEDINPUT}';

    DROP TABLE IF EXISTS FuelEfficientDriving; 
    CREATE EXTERNAL TABLE FuelEfficientDriving
    (
                   vin                         string, 
                model                        string,
                   city                        string,
                speed                          string,
                transmission_gear_position    string,                
                brake_pedal_status            string,            
                accelerator_pedal_position    string,                             
                Year                        string,
                Month                        string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:FUELEFFICIENTOUTPUT}';



    INSERT OVERWRITE TABLE FuelEfficientDriving
    select
    vin,
    model,
    city,
    speed,
    transmission_gear_position,
    brake_pedal_status,
    accelerator_pedal_position,
    "${hiveconf:Year}" as Year,
    "${hiveconf:Month}" as Month
    from PartitionedCarEvents
    where transmission_gear_position IN ('fourth', 'fifth', 'sixth', 'seventh', 'eight') AND parking_brake_status = '0' AND brake_pedal_status = '0' AND speed <= '60' AND accelerator_pedal_position >= '50'


<span data-ttu-id="e2337-393">Araç'ın iletim dişli konumu, Fren pedal durumu, hız ve verimli yönlendirmeli davranışı braking, hızlandırmasını, temel Hızlandırıcı pedal konumu toodetect yakıt hello bileşimini kullanır ve desenler hızı.</span><span class="sxs-lookup"><span data-stu-id="e2337-393">It uses hello combination of vehicle's transmission gear position, brake pedal status, speed, and accelerator pedal position toodetect fuel efficient driving behavior based on acceleration, braking, and speed patterns.</span></span> 

<span data-ttu-id="e2337-394">Merhaba ardışık düzen başarılı bir şekilde yürütüldükten sonra depolama hesabınızda hello "connectedcar" kapsayıcısı altında oluşturulan bölümler aşağıdaki hello bakın.</span><span class="sxs-lookup"><span data-stu-id="e2337-394">Once hello pipeline is executed successfully, you see hello following partitions generated in your storage account under hello "connectedcar" container.</span></span>

![FuelEfficientDrivingPatternPipeline çıkış](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig20-vehicle-telematics-fuel-efficient-driving-pattern-output.png) 

<span data-ttu-id="e2337-396">*Şekil 21 – FuelEfficientDrivingPatternPipeline çıkış*</span><span class="sxs-lookup"><span data-stu-id="e2337-396">*Figure 21 – FuelEfficientDrivingPatternPipeline output*</span></span>

<span data-ttu-id="e2337-397">**Tahminleri geri çağırma**</span><span class="sxs-lookup"><span data-stu-id="e2337-397">**Recall Predictions**</span></span>

<span data-ttu-id="e2337-398">Merhaba makine öğrenimi denemesinin sağlandığında ve hello çözüm dağıtımının bir parçası olarak bir web hizmeti olarak yayımlanır.</span><span class="sxs-lookup"><span data-stu-id="e2337-398">hello machine learning experiment is provisioned and published as a web service as part of hello solution deployment.</span></span> <span data-ttu-id="e2337-399">Merhaba toplu Puanlama uç noktası data factory bağlantılı hizmet olarak kayıtlı ve veri fabrikası toplu iş Puanlama etkinliği kullanarak kullanıma hazır hale getirilmiş bu iş akışında yararlanır.</span><span class="sxs-lookup"><span data-stu-id="e2337-399">hello batch scoring end point is leveraged in this workflow, registered as a data factory linked service and operationalized using data factory batch scoring activity.</span></span>

![Machine Learning uç noktası](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig21-vehicle-telematics-machine-learning-endpoint.png) 

<span data-ttu-id="e2337-401">*Veri fabrikasında bağlı hizmet olarak Şekil 22 – Machine learning uç noktası kayıtlı*</span><span class="sxs-lookup"><span data-stu-id="e2337-401">*Figure 22 – Machine learning endpoint registered as a linked service in data factory*</span></span>

<span data-ttu-id="e2337-402">Merhaba kayıtlı bağlantılı hizmet hello anomali algılama modelini kullanarak hello DetectAnomalyPipeline tooscore hello verilerde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e2337-402">hello registered linked service is used in hello DetectAnomalyPipeline tooscore hello data using hello anomaly detection model.</span></span> 

![Machine Learning toplu veri fabrikasında Puanlama etkinliği](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig22-vehicle-telematics-aml-batch-scoring.png) 

<span data-ttu-id="e2337-404">*Şekil 23 – veri fabrikasında Azure Machine Learning toplu Puanlama etkinliği*</span><span class="sxs-lookup"><span data-stu-id="e2337-404">*Figure 23 – Azure Machine Learning Batch Scoring activity in data factory*</span></span> 

<span data-ttu-id="e2337-405">Web hizmeti Puanlama hello toplu işlemle operationalized böylece bu ardışık düzendeki veri hazırlığı için gerçekleştirilen birkaç adım vardır.</span><span class="sxs-lookup"><span data-stu-id="e2337-405">There are few steps performed in this pipeline for data preparation so that it can be operationalized with hello batch scoring web service.</span></span> 

![Geri çekme gerektiren taşıtlardan tahmin etmeye yönelik DetectAnomalyPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig23-vehicle-telematics-pipeline-predicting-recalls.png) 

<span data-ttu-id="e2337-407">*Şekil 24 – geri çekme gerektiren taşıtlardan tahmin etmeye yönelik DetectAnomalyPipeline*</span><span class="sxs-lookup"><span data-stu-id="e2337-407">*Figure 24 – DetectAnomalyPipeline for predicting vehicles requiring recalls*</span></span> 

<span data-ttu-id="e2337-408">***Anomali algılama Hive sorgusu***</span><span class="sxs-lookup"><span data-stu-id="e2337-408">***Anomaly detection Hive query***</span></span>

<span data-ttu-id="e2337-409">Merhaba Puanlama tamamlandığında, bir Hdınsight kullanılan tooprocess ve anormallikleri 0.60 veya daha yüksek olasılık puanı hello modeli tarafından ayrılır toplama hello veri etkinliktir.</span><span class="sxs-lookup"><span data-stu-id="e2337-409">Once hello scoring is completed, an HDInsight activity is used tooprocess and aggregate hello data that are categorized as anomalies by hello model with a probability score of 0.60 or higher.</span></span>

    DROP TABLE IF EXISTS CarEventsAnomaly; 
    CREATE EXTERNAL TABLE CarEventsAnomaly 
    (
                vin                            string,
                model                        string,
                gendate                        string,
                outsidetemperature            string,
                enginetemperature            string,
                speed                        string,
                fuel                        string,
                engineoil                    string,
                tirepressure                string,
                odometer                    string,
                city                        string,
                accelerator_pedal_position    string,
                parking_brake_status        string,
                headlamp_status                string,
                brake_pedal_status            string,
                transmission_gear_position    string,
                ignition_status                string,
                windshield_wiper_status        string,
                abs                          string,
                maintenanceLabel            string,
                maintenanceProbability        string,
                RecallLabel                    string,
                RecallProbability            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:ANOMALYOUTPUT}';

    DROP TABLE IF EXISTS RecallModel; 
    CREATE EXTERNAL TABLE RecallModel 
    (

                vin                            string,
                model                        string,
                city                        string,
                outsidetemperature            string,
                enginetemperature            string,
                speed                        string,
                Year                        string,
                Month                        string                

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:RECALLMODELOUTPUT}';

    INSERT OVERWRITE TABLE RecallModel
    select
    vin,
    model,
    city,
    outsidetemperature,
    enginetemperature,
    speed,
    "${hiveconf:Year}" as Year,
    "${hiveconf:Month}" as Month
    from CarEventsAnomaly
    where RecallLabel = '1' AND RecallProbability >= '0.60'


<span data-ttu-id="e2337-410">Merhaba ardışık düzen başarılı bir şekilde yürütüldükten sonra depolama hesabınızda hello "connectedcar" kapsayıcısı altında oluşturulan bölümler aşağıdaki hello bakın.</span><span class="sxs-lookup"><span data-stu-id="e2337-410">Once hello pipeline is executed successfully, you see hello following partitions generated in your storage account under hello "connectedcar" container.</span></span>

![DetectAnomalyPipeline çıkış](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig24-vehicle-telematics-detect-anamoly-pipeline-output.png) 

<span data-ttu-id="e2337-412">*Şekil 25 – DetectAnomalyPipeline çıkış*</span><span class="sxs-lookup"><span data-stu-id="e2337-412">*Figure 25 – DetectAnomalyPipeline output*</span></span>

## <a name="publish"></a><span data-ttu-id="e2337-413">Yayımlama</span><span class="sxs-lookup"><span data-stu-id="e2337-413">Publish</span></span>

### <a name="real-time-analysis"></a><span data-ttu-id="e2337-414">Gerçek zamanlı analiz</span><span class="sxs-lookup"><span data-stu-id="e2337-414">Real-time analysis</span></span>
<span data-ttu-id="e2337-415">Merhaba Stream Analytics işi hello sorgularda birini yayımlar hello olayları tooan çıkış Event Hub örneği.</span><span class="sxs-lookup"><span data-stu-id="e2337-415">One of hello queries in hello Stream Analytics job publishes hello events tooan output Event Hub instance.</span></span> 

![Akış analizi işi yayımlar tooan çıkış olay hub'ı örneği](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig25-vehicle-telematics-stream-analytics-job-publishes-output-event-hub.png)

<span data-ttu-id="e2337-417">*Şekil 26 – Stream Analytics işi yayımlar tooan çıkış olay hub'ı örneği*</span><span class="sxs-lookup"><span data-stu-id="e2337-417">*Figure 26 – Stream Analytics job publishes tooan output Event Hub instance*</span></span>

![Stream Analytics sorgu toopublish toohello olay hub'ı örnek çıkış](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig26-vehicle-telematics-stream-analytics-query-publish-output-event-hub.png)

<span data-ttu-id="e2337-419">*Şekil 27 – Stream Analytics sorgu toopublish toohello çıktısını olay hub'ı örneği*</span><span class="sxs-lookup"><span data-stu-id="e2337-419">*Figure 27 – Stream Analytics query toopublish toohello output Event Hub instance*</span></span>

<span data-ttu-id="e2337-420">Bu akış olayların RealTimeDashboardApp hello çözümdeki hello tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e2337-420">This stream of events is consumed by hello RealTimeDashboardApp included in hello solution.</span></span> <span data-ttu-id="e2337-421">Bu uygulamayı gerçek zamanlı Puanlama hello Machine Learning istek-yanıt web hizmetini yararlanır ve hello sonuç veri tooa Power BI dataset tüketimi için yayımlar.</span><span class="sxs-lookup"><span data-stu-id="e2337-421">This application leverages hello Machine Learning Request-Response web service for real-time scoring and publishes hello resultant data tooa Power BI dataset for consumption.</span></span> 

### <a name="batch-analysis"></a><span data-ttu-id="e2337-422">Toplu iş analiz</span><span class="sxs-lookup"><span data-stu-id="e2337-422">Batch analysis</span></span>
<span data-ttu-id="e2337-423">Merhaba toplu ve gerçek zamanlı işleme Hello sonuçları tüketimi için yayımlanan toohello Azure SQL veritabanı tabloları ' dir.</span><span class="sxs-lookup"><span data-stu-id="e2337-423">hello results of hello batch and real-time processing are published toohello Azure SQL Database tables for consumption.</span></span> <span data-ttu-id="e2337-424">Hello Azure SQL Server, veritabanı ve hello tablolar hello Kurulum komut dosyasının bir parçası otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="e2337-424">hello Azure SQL Server, Database, and hello tables are created automatically as part of hello setup script.</span></span> 

![Toplu işleme sonuçlarını toodata mart iş akışı kopyalama](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig27-vehicle-telematics-batch-processing-results-copy-to-data-mart.png)

<span data-ttu-id="e2337-426">*Şekil 28 – toplu sonuçları kopyalama toodata mart iş akışı işleme*</span><span class="sxs-lookup"><span data-stu-id="e2337-426">*Figure 28 – Batch processing results copy toodata mart workflow*</span></span>

![Akış analizi işi toodata mart yayımlar](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig28-vehicle-telematics-stream-analytics-job-publishes-to-data-mart.png)

<span data-ttu-id="e2337-428">*Şekil 29 – Stream Analytics işi toodata mart yayımlar*</span><span class="sxs-lookup"><span data-stu-id="e2337-428">*Figure 29 – Stream Analytics job publishes toodata mart*</span></span>

![Veri reyonu ayarında Stream Analytics işi](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig29-vehicle-telematics-data-mart-setting-in-stream-analytics-job.png)

<span data-ttu-id="e2337-430">*Şekil 30 – Data mart Stream Analytics işinde ayarlama*</span><span class="sxs-lookup"><span data-stu-id="e2337-430">*Figure 30 – Data mart setting in Stream Analytics job*</span></span>

## <a name="consume"></a><span data-ttu-id="e2337-431">Tüketme</span><span class="sxs-lookup"><span data-stu-id="e2337-431">Consume</span></span>
<span data-ttu-id="e2337-432">Power BI Bu çözüm gerçek zamanlı veri ve Tahmine dayalı analiz görselleştirmeleri için zengin bir Pano sağlar.</span><span class="sxs-lookup"><span data-stu-id="e2337-432">Power BI gives this solution a rich dashboard for real-time data and predictive analytics visualizations.</span></span> 

<span data-ttu-id="e2337-433">Merhaba Power BI raporları ve hello Pano ayarlama hakkında ayrıntılı yönergeler için buraya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e2337-433">Click here for detailed instructions on setting up hello Power BI reports and hello dashboard.</span></span> <span data-ttu-id="e2337-434">Merhaba son Pano şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="e2337-434">hello final dashboard looks like this:</span></span>

![Power BI Panosu](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig30-vehicle-telematics-powerbi-dashboard.png)

<span data-ttu-id="e2337-436">*Şekil 31 - Power BI Panosu*</span><span class="sxs-lookup"><span data-stu-id="e2337-436">*Figure 31 - Power BI Dashboard*</span></span>

## <a name="summary"></a><span data-ttu-id="e2337-437">Özet</span><span class="sxs-lookup"><span data-stu-id="e2337-437">Summary</span></span>
<span data-ttu-id="e2337-438">Bu belgede ayrıntılı ayrıntıya hello araç Telemetri analiz çözümü, içerir.</span><span class="sxs-lookup"><span data-stu-id="e2337-438">This document contains a detailed drill-down of hello Vehicle Telemetry Analytics Solution.</span></span> <span data-ttu-id="e2337-439">Bu bir lambda mimarisi desenini paylaşan gerçek zamanlı ve toplu analytics Öngörüler ve Eylemler ile.</span><span class="sxs-lookup"><span data-stu-id="e2337-439">This showcases a lambda architecture pattern for real-time and batch analytics with predictions and actions.</span></span> <span data-ttu-id="e2337-440">Bu desen (gerçek zamanlı) etkin yolunuzda gerektiren kullanım örnekleri tooa çeşitli uygular ve yolunuzda (toplu) analytics.</span><span class="sxs-lookup"><span data-stu-id="e2337-440">This pattern applies tooa wide range of use cases that require hot path (real-time) and cold path (batch) analytics.</span></span> 

