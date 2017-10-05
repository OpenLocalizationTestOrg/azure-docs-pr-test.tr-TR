---
title: "Derin Dalış içine araç durumu tahmin etmek ve alışkanlık - Azure yürüten | Microsoft Docs"
description: "Araç sistem durumu ve yürüten gerçek zamanlı ve Tahmine dayalı Öngörüler elde etmek için Cortana Intelligence yeteneklerini kullanabilir alışkanlıklarınıza."
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
ms.openlocfilehash: 0a4dba58445cf0fd9fd8f51d443576bacd92251b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="vehicle-telemetry-analytics-solution-playbook-deep-dive-into-the-solution"></a><span data-ttu-id="940dc-103">Araç telemetri analizi çözüm kitabı: çözümün ayrıntılarına inme</span><span class="sxs-lookup"><span data-stu-id="940dc-103">Vehicle telemetry analytics solution playbook: deep dive into the solution</span></span>
<span data-ttu-id="940dc-104">Bu **menü** bu playbook bölümlerine bağlantılar:</span><span class="sxs-lookup"><span data-stu-id="940dc-104">This **menu** links to the sections of this playbook:</span></span> 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

<span data-ttu-id="940dc-105">Bu bölümde kümede ayrıntısına gider her yönergeleri ve özelleştirme işaretçileri ile çözüm mimarisinde gösterilen aşamaları.</span><span class="sxs-lookup"><span data-stu-id="940dc-105">This section drills down into each of the stages depicted in the Solution Architecture with instructions and pointers for customization.</span></span> 

## <a name="data-sources"></a><span data-ttu-id="940dc-106">Veri Kaynakları</span><span class="sxs-lookup"><span data-stu-id="940dc-106">Data Sources</span></span>
<span data-ttu-id="940dc-107">Çözüm iki farklı veri kaynakları kullanır:</span><span class="sxs-lookup"><span data-stu-id="940dc-107">The solution uses two different data sources:</span></span>

* <span data-ttu-id="940dc-108">**Benzetimli araç sinyalleri ve tanılama veri kümesi** ve</span><span class="sxs-lookup"><span data-stu-id="940dc-108">**simulated vehicle signals and diagnostic dataset** and</span></span> 
* <span data-ttu-id="940dc-109">**araç Kataloğu**</span><span class="sxs-lookup"><span data-stu-id="940dc-109">**vehicle catalog**</span></span>

<span data-ttu-id="940dc-110">Bir araç telematik simulator bu çözümün bir parçası olarak dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="940dc-110">A vehicle telematics simulator is included as part of this solution.</span></span> <span data-ttu-id="940dc-111">Tanılama bilgisi yayar ve araç durumunu ve belirli bir noktada yönlendirmeli düzeni zamanında karşılık gelen işaret eder.</span><span class="sxs-lookup"><span data-stu-id="940dc-111">It emits diagnostic information and signals corresponding to the state of the vehicle and to the driving pattern at a given point in time.</span></span> <span data-ttu-id="940dc-112">Tıklatın [araç telematik Simulator](http://go.microsoft.com/fwlink/?LinkId=717075) indirmek için **araç telematik Simulator Visual Studio çözümü** gereksinimlerinize göre özelleştirmeler.</span><span class="sxs-lookup"><span data-stu-id="940dc-112">Click [Vehicle Telematics Simulator](http://go.microsoft.com/fwlink/?LinkId=717075) to download the **Vehicle Telematics Simulator Visual Studio Solution** for customizations based on your requirements.</span></span> <span data-ttu-id="940dc-113">Araç katalog Toplamıdır modeli eşlemesi ile başvuru dataset içerir.</span><span class="sxs-lookup"><span data-stu-id="940dc-113">The vehicle catalog contains a reference dataset with a VIN to model mapping.</span></span>

![Araç telematik simulator](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig1-vehicle-telematics-simulator.png)

<span data-ttu-id="940dc-115">*Şekil 1 – araç telematik Simulator*</span><span class="sxs-lookup"><span data-stu-id="940dc-115">*Figure 1 – Vehicle Telematics Simulator*</span></span>

<span data-ttu-id="940dc-116">Aşağıdaki şema içeren bir JSON olarak biçimlendirilmiş bir veri kümesi budur.</span><span class="sxs-lookup"><span data-stu-id="940dc-116">This is a JSON-formatted dataset that contains the following schema.</span></span>

| <span data-ttu-id="940dc-117">Sütun</span><span class="sxs-lookup"><span data-stu-id="940dc-117">Column</span></span> | <span data-ttu-id="940dc-118">Açıklama</span><span class="sxs-lookup"><span data-stu-id="940dc-118">Description</span></span> | <span data-ttu-id="940dc-119">Değerler</span><span class="sxs-lookup"><span data-stu-id="940dc-119">Values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="940dc-120">TOPLAMIDIR</span><span class="sxs-lookup"><span data-stu-id="940dc-120">VIN</span></span> |<span data-ttu-id="940dc-121">Rastgele oluşturulan araç kimlik numarası</span><span class="sxs-lookup"><span data-stu-id="940dc-121">Randomly generated Vehicle Identification Number</span></span> |<span data-ttu-id="940dc-122">Bu ana 10.000 rastgele oluşturulmuş araç kimlik numaraları listesinden elde edilir.</span><span class="sxs-lookup"><span data-stu-id="940dc-122">This is obtained from a master list of 10,000 randomly generated vehicle identification numbers.</span></span> |
| <span data-ttu-id="940dc-123">Dış sıcaklığı</span><span class="sxs-lookup"><span data-stu-id="940dc-123">Outside temperature</span></span> |<span data-ttu-id="940dc-124">Aracın burada yürüten dış sıcaklığı</span><span class="sxs-lookup"><span data-stu-id="940dc-124">The outside temperature where the vehicle is driving</span></span> |<span data-ttu-id="940dc-125">0-100 arasında rastgele oluşturulmuş bir sayıya</span><span class="sxs-lookup"><span data-stu-id="940dc-125">Randomly generated number from 0-100</span></span> |
| <span data-ttu-id="940dc-126">Altyapısı sıcaklık</span><span class="sxs-lookup"><span data-stu-id="940dc-126">Engine temperature</span></span> |<span data-ttu-id="940dc-127">Aracın altyapısı sıcaklığını</span><span class="sxs-lookup"><span data-stu-id="940dc-127">The engine temperature of the vehicle</span></span> |<span data-ttu-id="940dc-128">0-500 arasında rastgele oluşturulmuş sayı</span><span class="sxs-lookup"><span data-stu-id="940dc-128">Randomly generated number from 0-500</span></span> |
| <span data-ttu-id="940dc-129">Hız</span><span class="sxs-lookup"><span data-stu-id="940dc-129">Speed</span></span> |<span data-ttu-id="940dc-130">Aracın yönlendiren altyapısı hızı</span><span class="sxs-lookup"><span data-stu-id="940dc-130">The engine speed at which the vehicle is driving</span></span> |<span data-ttu-id="940dc-131">0-100 arasında rastgele oluşturulmuş bir sayıya</span><span class="sxs-lookup"><span data-stu-id="940dc-131">Randomly generated number from 0-100</span></span> |
| <span data-ttu-id="940dc-132">Yakıt</span><span class="sxs-lookup"><span data-stu-id="940dc-132">Fuel</span></span> |<span data-ttu-id="940dc-133">Aracın yakıt düzeyi</span><span class="sxs-lookup"><span data-stu-id="940dc-133">The fuel level of the vehicle</span></span> |<span data-ttu-id="940dc-134">Rastgele oluşturulmuş bir sayıya 0-100 (yakıt düzeyi yüzdesi gösterir)</span><span class="sxs-lookup"><span data-stu-id="940dc-134">Randomly generated number from 0-100 (indicates fuel level percentage)</span></span> |
| <span data-ttu-id="940dc-135">EngineOil</span><span class="sxs-lookup"><span data-stu-id="940dc-135">EngineOil</span></span> |<span data-ttu-id="940dc-136">Aracın altyapısı Petrol düzeyi</span><span class="sxs-lookup"><span data-stu-id="940dc-136">The engine oil level of the vehicle</span></span> |<span data-ttu-id="940dc-137">Rastgele oluşturulmuş bir sayıya 0-100 (altyapısı Petrol düzeyi yüzdesi gösterir)</span><span class="sxs-lookup"><span data-stu-id="940dc-137">Randomly generated number from 0-100 (indicates engine oil level percentage)</span></span> |
| <span data-ttu-id="940dc-138">Lastiği baskısı</span><span class="sxs-lookup"><span data-stu-id="940dc-138">Tire pressure</span></span> |<span data-ttu-id="940dc-139">Aracın lastiği Basıncı</span><span class="sxs-lookup"><span data-stu-id="940dc-139">The tire pressure of the vehicle</span></span> |<span data-ttu-id="940dc-140">Rastgele oluşturulan numarası 0-50'den (lastiği baskısı düzeyi yüzdesi gösterir)</span><span class="sxs-lookup"><span data-stu-id="940dc-140">Randomly generated number from 0-50 (indicates tire pressure level percentage)</span></span> |
| <span data-ttu-id="940dc-141">Kilometre Sayacı</span><span class="sxs-lookup"><span data-stu-id="940dc-141">Odometer</span></span> |<span data-ttu-id="940dc-142">Aracın Kilometre Sayacı okuma</span><span class="sxs-lookup"><span data-stu-id="940dc-142">The odometer reading of the vehicle</span></span> |<span data-ttu-id="940dc-143">0-200000 arasında rastgele oluşturulmuş sayı</span><span class="sxs-lookup"><span data-stu-id="940dc-143">Randomly generated number from 0-200000</span></span> |
| <span data-ttu-id="940dc-144">Accelerator_pedal_position</span><span class="sxs-lookup"><span data-stu-id="940dc-144">Accelerator_pedal_position</span></span> |<span data-ttu-id="940dc-145">Aracın Hızlandırıcı pedal konumu</span><span class="sxs-lookup"><span data-stu-id="940dc-145">The accelerator pedal position of the vehicle</span></span> |<span data-ttu-id="940dc-146">Rastgele oluşturulmuş bir sayıya 0-100 (Hızlandırıcı düzeyi yüzdesi gösterir)</span><span class="sxs-lookup"><span data-stu-id="940dc-146">Randomly generated number from 0-100 (indicates accelerator level percentage)</span></span> |
| <span data-ttu-id="940dc-147">Parking_brake_status</span><span class="sxs-lookup"><span data-stu-id="940dc-147">Parking_brake_status</span></span> |<span data-ttu-id="940dc-148">Aracın veya yerleşmiş durumdayken gösterir</span><span class="sxs-lookup"><span data-stu-id="940dc-148">Indicates whether the vehicle is parked or not</span></span> |<span data-ttu-id="940dc-149">TRUE veya False</span><span class="sxs-lookup"><span data-stu-id="940dc-149">True or False</span></span> |
| <span data-ttu-id="940dc-150">Headlamp_status</span><span class="sxs-lookup"><span data-stu-id="940dc-150">Headlamp_status</span></span> |<span data-ttu-id="940dc-151">Burada ön ışık üzerinde olup olmadığını gösterir</span><span class="sxs-lookup"><span data-stu-id="940dc-151">Indicates where the headlamp is on or not</span></span> |<span data-ttu-id="940dc-152">TRUE veya False</span><span class="sxs-lookup"><span data-stu-id="940dc-152">True or False</span></span> |
| <span data-ttu-id="940dc-153">Brake_pedal_status</span><span class="sxs-lookup"><span data-stu-id="940dc-153">Brake_pedal_status</span></span> |<span data-ttu-id="940dc-154">Fren pedal veya basılı olup olmadığını gösterir</span><span class="sxs-lookup"><span data-stu-id="940dc-154">Indicates whether the brake pedal is pressed or not</span></span> |<span data-ttu-id="940dc-155">TRUE veya False</span><span class="sxs-lookup"><span data-stu-id="940dc-155">True or False</span></span> |
| <span data-ttu-id="940dc-156">Transmission_gear_position</span><span class="sxs-lookup"><span data-stu-id="940dc-156">Transmission_gear_position</span></span> |<span data-ttu-id="940dc-157">Aracın iletim dişli konumu</span><span class="sxs-lookup"><span data-stu-id="940dc-157">The transmission gear position of the vehicle</span></span> |<span data-ttu-id="940dc-158">Durumları: ilk olarak, üçüncü, dördüncü beşinci, altıncı seventh, sekizinci ikinci</span><span class="sxs-lookup"><span data-stu-id="940dc-158">States: first, second, third, fourth, fifth, sixth, seventh, eighth</span></span> |
| <span data-ttu-id="940dc-159">Ignition_status</span><span class="sxs-lookup"><span data-stu-id="940dc-159">Ignition_status</span></span> |<span data-ttu-id="940dc-160">Aracın çalışıyor veya durdurulmuştur olup olmadığını gösterir</span><span class="sxs-lookup"><span data-stu-id="940dc-160">Indicates whether the vehicle is running or stopped</span></span> |<span data-ttu-id="940dc-161">TRUE veya False</span><span class="sxs-lookup"><span data-stu-id="940dc-161">True or False</span></span> |
| <span data-ttu-id="940dc-162">Windshield_wiper_status</span><span class="sxs-lookup"><span data-stu-id="940dc-162">Windshield_wiper_status</span></span> |<span data-ttu-id="940dc-163">Ön wiper veya açık olup olmadığını gösterir</span><span class="sxs-lookup"><span data-stu-id="940dc-163">Indicates whether the windshield wiper is turned or not</span></span> |<span data-ttu-id="940dc-164">TRUE veya False</span><span class="sxs-lookup"><span data-stu-id="940dc-164">True or False</span></span> |
| <span data-ttu-id="940dc-165">ABS</span><span class="sxs-lookup"><span data-stu-id="940dc-165">ABS</span></span> |<span data-ttu-id="940dc-166">ABS veya bağlı olup olmadığını gösterir</span><span class="sxs-lookup"><span data-stu-id="940dc-166">Indicates whether ABS is engaged or not</span></span> |<span data-ttu-id="940dc-167">TRUE veya False</span><span class="sxs-lookup"><span data-stu-id="940dc-167">True or False</span></span> |
| <span data-ttu-id="940dc-168">zaman damgası</span><span class="sxs-lookup"><span data-stu-id="940dc-168">Timestamp</span></span> |<span data-ttu-id="940dc-169">Veri noktası oluşturulduğunda, zaman damgası</span><span class="sxs-lookup"><span data-stu-id="940dc-169">The timestamp when the data point is created</span></span> |<span data-ttu-id="940dc-170">Tarih</span><span class="sxs-lookup"><span data-stu-id="940dc-170">Date</span></span> |
| <span data-ttu-id="940dc-171">Şehir</span><span class="sxs-lookup"><span data-stu-id="940dc-171">City</span></span> |<span data-ttu-id="940dc-172">Aracın konumu</span><span class="sxs-lookup"><span data-stu-id="940dc-172">The location of the vehicle</span></span> |<span data-ttu-id="940dc-173">Bu çözümdeki 4 Şehir: Bellevue, Redmond, Sammamish, Seattle</span><span class="sxs-lookup"><span data-stu-id="940dc-173">4 cities in this solution: Bellevue, Redmond, Sammamish, Seattle</span></span> |

<span data-ttu-id="940dc-174">Araç model başvuru dataset Toplamıdır modeli eşleme içerir.</span><span class="sxs-lookup"><span data-stu-id="940dc-174">The vehicle model reference dataset contains VIN to the model mapping.</span></span> 

| <span data-ttu-id="940dc-175">TOPLAMIDIR</span><span class="sxs-lookup"><span data-stu-id="940dc-175">VIN</span></span> | <span data-ttu-id="940dc-176">modeli</span><span class="sxs-lookup"><span data-stu-id="940dc-176">Model</span></span> |
| --- | --- |
| <span data-ttu-id="940dc-177">FHL3O1SA4IEHB4WU1</span><span class="sxs-lookup"><span data-stu-id="940dc-177">FHL3O1SA4IEHB4WU1</span></span> |<span data-ttu-id="940dc-178">Sedan</span><span class="sxs-lookup"><span data-stu-id="940dc-178">Sedan</span></span> |
| <span data-ttu-id="940dc-179">8J0U8XCPRGW4Z3NQE</span><span class="sxs-lookup"><span data-stu-id="940dc-179">8J0U8XCPRGW4Z3NQE</span></span> |<span data-ttu-id="940dc-180">Karma</span><span class="sxs-lookup"><span data-stu-id="940dc-180">Hybrid</span></span> |
| <span data-ttu-id="940dc-181">WORG68Z2PLTNZDBI7</span><span class="sxs-lookup"><span data-stu-id="940dc-181">WORG68Z2PLTNZDBI7</span></span> |<span data-ttu-id="940dc-182">Aile Saloon</span><span class="sxs-lookup"><span data-stu-id="940dc-182">Family Saloon</span></span> |
| <span data-ttu-id="940dc-183">JTHMYHQTEPP4WBMRN</span><span class="sxs-lookup"><span data-stu-id="940dc-183">JTHMYHQTEPP4WBMRN</span></span> |<span data-ttu-id="940dc-184">Sedan</span><span class="sxs-lookup"><span data-stu-id="940dc-184">Sedan</span></span> |
| <span data-ttu-id="940dc-185">W9FTHG27LZN1YWO0Y</span><span class="sxs-lookup"><span data-stu-id="940dc-185">W9FTHG27LZN1YWO0Y</span></span> |<span data-ttu-id="940dc-186">Karma</span><span class="sxs-lookup"><span data-stu-id="940dc-186">Hybrid</span></span> |
| <span data-ttu-id="940dc-187">MHTP9N792PHK08WJM</span><span class="sxs-lookup"><span data-stu-id="940dc-187">MHTP9N792PHK08WJM</span></span> |<span data-ttu-id="940dc-188">Aile Saloon</span><span class="sxs-lookup"><span data-stu-id="940dc-188">Family Saloon</span></span> |
| <span data-ttu-id="940dc-189">EI4QXI2AXVQQING4I</span><span class="sxs-lookup"><span data-stu-id="940dc-189">EI4QXI2AXVQQING4I</span></span> |<span data-ttu-id="940dc-190">Sedan</span><span class="sxs-lookup"><span data-stu-id="940dc-190">Sedan</span></span> |
| <span data-ttu-id="940dc-191">5KKR2VB4WHQH97PF8</span><span class="sxs-lookup"><span data-stu-id="940dc-191">5KKR2VB4WHQH97PF8</span></span> |<span data-ttu-id="940dc-192">Karma</span><span class="sxs-lookup"><span data-stu-id="940dc-192">Hybrid</span></span> |
| <span data-ttu-id="940dc-193">W9NSZ423XZHAONYXB</span><span class="sxs-lookup"><span data-stu-id="940dc-193">W9NSZ423XZHAONYXB</span></span> |<span data-ttu-id="940dc-194">Aile Saloon</span><span class="sxs-lookup"><span data-stu-id="940dc-194">Family Saloon</span></span> |
| <span data-ttu-id="940dc-195">26WJSGHX4MA5ROHNL</span><span class="sxs-lookup"><span data-stu-id="940dc-195">26WJSGHX4MA5ROHNL</span></span> |<span data-ttu-id="940dc-196">Dönüştürülebilir</span><span class="sxs-lookup"><span data-stu-id="940dc-196">Convertible</span></span> |
| <span data-ttu-id="940dc-197">GHLUB6ONKMOSI7E77</span><span class="sxs-lookup"><span data-stu-id="940dc-197">GHLUB6ONKMOSI7E77</span></span> |<span data-ttu-id="940dc-198">İstasyon Wagon</span><span class="sxs-lookup"><span data-stu-id="940dc-198">Station Wagon</span></span> |
| <span data-ttu-id="940dc-199">9C2RHVRVLMEJDBXLP</span><span class="sxs-lookup"><span data-stu-id="940dc-199">9C2RHVRVLMEJDBXLP</span></span> |<span data-ttu-id="940dc-200">Küçük otomobil</span><span class="sxs-lookup"><span data-stu-id="940dc-200">Compact Car</span></span> |
| <span data-ttu-id="940dc-201">BRNHVMZOUJ6EOCP32</span><span class="sxs-lookup"><span data-stu-id="940dc-201">BRNHVMZOUJ6EOCP32</span></span> |<span data-ttu-id="940dc-202">Küçük SUV</span><span class="sxs-lookup"><span data-stu-id="940dc-202">Small SUV</span></span> |
| <span data-ttu-id="940dc-203">VCYVW0WUZNBTM594J</span><span class="sxs-lookup"><span data-stu-id="940dc-203">VCYVW0WUZNBTM594J</span></span> |<span data-ttu-id="940dc-204">Spor araba</span><span class="sxs-lookup"><span data-stu-id="940dc-204">Sports Car</span></span> |
| <span data-ttu-id="940dc-205">HNVCE6YFZSA5M82NY</span><span class="sxs-lookup"><span data-stu-id="940dc-205">HNVCE6YFZSA5M82NY</span></span> |<span data-ttu-id="940dc-206">Orta SUV</span><span class="sxs-lookup"><span data-stu-id="940dc-206">Medium SUV</span></span> |
| <span data-ttu-id="940dc-207">4R30FOR7NUOBL05GJ</span><span class="sxs-lookup"><span data-stu-id="940dc-207">4R30FOR7NUOBL05GJ</span></span> |<span data-ttu-id="940dc-208">İstasyon Wagon</span><span class="sxs-lookup"><span data-stu-id="940dc-208">Station Wagon</span></span> |
| <span data-ttu-id="940dc-209">WYNIIY42VKV6OQS1J</span><span class="sxs-lookup"><span data-stu-id="940dc-209">WYNIIY42VKV6OQS1J</span></span> |<span data-ttu-id="940dc-210">Büyük SUV</span><span class="sxs-lookup"><span data-stu-id="940dc-210">Large SUV</span></span> |
| <span data-ttu-id="940dc-211">8Y5QKG27QET1RBK7I</span><span class="sxs-lookup"><span data-stu-id="940dc-211">8Y5QKG27QET1RBK7I</span></span> |<span data-ttu-id="940dc-212">Büyük SUV</span><span class="sxs-lookup"><span data-stu-id="940dc-212">Large SUV</span></span> |
| <span data-ttu-id="940dc-213">DF6OX2WSRA6511BVG</span><span class="sxs-lookup"><span data-stu-id="940dc-213">DF6OX2WSRA6511BVG</span></span> |<span data-ttu-id="940dc-214">Coupe</span><span class="sxs-lookup"><span data-stu-id="940dc-214">Coupe</span></span> |
| <span data-ttu-id="940dc-215">Z2EOZWZBXAEW3E60T</span><span class="sxs-lookup"><span data-stu-id="940dc-215">Z2EOZWZBXAEW3E60T</span></span> |<span data-ttu-id="940dc-216">Sedan</span><span class="sxs-lookup"><span data-stu-id="940dc-216">Sedan</span></span> |
| <span data-ttu-id="940dc-217">M4TV6IEALD5QDS3IR</span><span class="sxs-lookup"><span data-stu-id="940dc-217">M4TV6IEALD5QDS3IR</span></span> |<span data-ttu-id="940dc-218">Karma</span><span class="sxs-lookup"><span data-stu-id="940dc-218">Hybrid</span></span> |
| <span data-ttu-id="940dc-219">VHRA1Y2TGTA84F00H</span><span class="sxs-lookup"><span data-stu-id="940dc-219">VHRA1Y2TGTA84F00H</span></span> |<span data-ttu-id="940dc-220">Aile Saloon</span><span class="sxs-lookup"><span data-stu-id="940dc-220">Family Saloon</span></span> |
| <span data-ttu-id="940dc-221">R0JAUHT1L1R3BIKI0</span><span class="sxs-lookup"><span data-stu-id="940dc-221">R0JAUHT1L1R3BIKI0</span></span> |<span data-ttu-id="940dc-222">Sedan</span><span class="sxs-lookup"><span data-stu-id="940dc-222">Sedan</span></span> |
| <span data-ttu-id="940dc-223">9230C202Z60XX84AU</span><span class="sxs-lookup"><span data-stu-id="940dc-223">9230C202Z60XX84AU</span></span> |<span data-ttu-id="940dc-224">Karma</span><span class="sxs-lookup"><span data-stu-id="940dc-224">Hybrid</span></span> |
| <span data-ttu-id="940dc-225">T8DNDN5UDCWL7M72H</span><span class="sxs-lookup"><span data-stu-id="940dc-225">T8DNDN5UDCWL7M72H</span></span> |<span data-ttu-id="940dc-226">Aile Saloon</span><span class="sxs-lookup"><span data-stu-id="940dc-226">Family Saloon</span></span> |
| <span data-ttu-id="940dc-227">4WPYRUZII5YV7YA42</span><span class="sxs-lookup"><span data-stu-id="940dc-227">4WPYRUZII5YV7YA42</span></span> |<span data-ttu-id="940dc-228">Sedan</span><span class="sxs-lookup"><span data-stu-id="940dc-228">Sedan</span></span> |
| <span data-ttu-id="940dc-229">D1ZVY26UV2BFGHZNO</span><span class="sxs-lookup"><span data-stu-id="940dc-229">D1ZVY26UV2BFGHZNO</span></span> |<span data-ttu-id="940dc-230">Karma</span><span class="sxs-lookup"><span data-stu-id="940dc-230">Hybrid</span></span> |
| <span data-ttu-id="940dc-231">XUF99EW9OIQOMV7Q7</span><span class="sxs-lookup"><span data-stu-id="940dc-231">XUF99EW9OIQOMV7Q7</span></span> |<span data-ttu-id="940dc-232">Aile Saloon</span><span class="sxs-lookup"><span data-stu-id="940dc-232">Family Saloon</span></span> |
| <span data-ttu-id="940dc-233">8OMCL3LGI7XNCC21U</span><span class="sxs-lookup"><span data-stu-id="940dc-233">8OMCL3LGI7XNCC21U</span></span> |<span data-ttu-id="940dc-234">Dönüştürülebilir</span><span class="sxs-lookup"><span data-stu-id="940dc-234">Convertible</span></span> |
| <span data-ttu-id="940dc-235">…….</span><span class="sxs-lookup"><span data-stu-id="940dc-235">…….</span></span> | |

### <a name="references"></a><span data-ttu-id="940dc-236">Başvurular</span><span class="sxs-lookup"><span data-stu-id="940dc-236">References</span></span>
[<span data-ttu-id="940dc-237">Araç telematik Simulator Visual Studio çözümü</span><span class="sxs-lookup"><span data-stu-id="940dc-237">Vehicle Telematics Simulator Visual Studio Solution</span></span>](http://go.microsoft.com/fwlink/?LinkId=717075) 

[<span data-ttu-id="940dc-238">Azure Event hub'ı</span><span class="sxs-lookup"><span data-stu-id="940dc-238">Azure Event Hub</span></span>](https://azure.microsoft.com/services/event-hubs/)

[<span data-ttu-id="940dc-239">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="940dc-239">Azure Data Factory</span></span>](https://azure.microsoft.com/documentation/learning-paths/data-factory/)

## <a name="ingestion"></a><span data-ttu-id="940dc-240">Alım</span><span class="sxs-lookup"><span data-stu-id="940dc-240">Ingestion</span></span>
<span data-ttu-id="940dc-241">Azure Event Hubs, Stream Analytics ve Data Factory birleşimleri araç sinyalleri, tanılama olayları alma için kullanılabilir ve gerçek zamanlı ve toplu analizi.</span><span class="sxs-lookup"><span data-stu-id="940dc-241">Combinations of Azure Event Hubs, Stream Analytics, and Data Factory are leveraged to ingest the vehicle signals, the diagnostic events, and real-time and batch analytics.</span></span> <span data-ttu-id="940dc-242">Tüm bu bileşenlerin oluşturulur ve çözüm dağıtımının bir parçası yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="940dc-242">All these components are created and configured as part of the solution deployment.</span></span> 

### <a name="real-time-analysis"></a><span data-ttu-id="940dc-243">Gerçek zamanlı analiz</span><span class="sxs-lookup"><span data-stu-id="940dc-243">Real-time analysis</span></span>
<span data-ttu-id="940dc-244">Araç telematik Simulator tarafından oluşturulan olayları olay Olay Hub SDK'sını kullanarak Hub'ına yayımlanır.</span><span class="sxs-lookup"><span data-stu-id="940dc-244">The events generated by the Vehicle Telematics Simulator are published to the Event Hub using the Event Hub SDK.</span></span> <span data-ttu-id="940dc-245">Stream Analytics işi, bu olayları olay hub'ı alır ve araç durumu çözümlemek için gerçek zamanlı verileri işler.</span><span class="sxs-lookup"><span data-stu-id="940dc-245">The Stream Analytics job ingests these events from the Event Hub and processes the data in real time to analyze the vehicle health.</span></span> 

![Olay hub'ı Panosu](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig4-vehicle-telematics-event-hub-dashboard.png) 

<span data-ttu-id="940dc-247">*Şekil 4 - Event Hub Panosu*</span><span class="sxs-lookup"><span data-stu-id="940dc-247">*Figure 4 - Event Hub dashboard*</span></span>

![Veriler işlenirken Analytics iş akışı](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig5-vehicle-telematics-stream-analytics-job-processing-data.png) 

<span data-ttu-id="940dc-249">*Şekil 5 - Stream Analytics işi veri işleme*</span><span class="sxs-lookup"><span data-stu-id="940dc-249">*Figure 5 - Stream Analytics job processing data*</span></span>

<span data-ttu-id="940dc-250">Stream Analytics işi;</span><span class="sxs-lookup"><span data-stu-id="940dc-250">The Stream Analytics job;</span></span>

* <span data-ttu-id="940dc-251">Olay hub'ı verileri alır</span><span class="sxs-lookup"><span data-stu-id="940dc-251">ingests data from the Event Hub</span></span> 
* <span data-ttu-id="940dc-252">araç Toplamıdır karşılık gelen modeline eşlemek için başvuru verileri ile bir birleştirme gerçekleştirir</span><span class="sxs-lookup"><span data-stu-id="940dc-252">performs a join with the reference data to map the vehicle VIN to the corresponding model</span></span> 
* <span data-ttu-id="940dc-253">bunları zengin toplu analiz için Azure blob depolama alanına devam ettirir.</span><span class="sxs-lookup"><span data-stu-id="940dc-253">persists them into Azure blob storage for rich batch analytics.</span></span> 

<span data-ttu-id="940dc-254">Aşağıdaki akış analizi sorgu verileri Azure blob depolama alanına kalıcı hale getirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="940dc-254">The following Stream Analytics query is used to persist the data into Azure blob storage.</span></span> 

![Akış analizi işi sorgu veri alımı için](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig6-vehicle-telematics-stream-analytics-job-query-for-data-ingestion.png) 

<span data-ttu-id="940dc-256">*Şekil 6 - Stream Analytics işi veri alımı için sorgu*</span><span class="sxs-lookup"><span data-stu-id="940dc-256">*Figure 6 - Stream Analytics job query for data ingestion*</span></span>

### <a name="batch-analysis"></a><span data-ttu-id="940dc-257">Toplu iş analiz</span><span class="sxs-lookup"><span data-stu-id="940dc-257">Batch analysis</span></span>
<span data-ttu-id="940dc-258">Biz de benzetimli araç sinyalleri ve tanılama veri kümesi daha zengin toplu analizi için ek bir birim oluşturduğunu.</span><span class="sxs-lookup"><span data-stu-id="940dc-258">We are also generating an additional volume of simulated vehicle signals and diagnostic dataset for richer batch analytics.</span></span> <span data-ttu-id="940dc-259">Bu toplu işlem için iyi temsili veri birimi emin olmak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="940dc-259">This is required to ensure a good representative data volume for batch processing.</span></span> <span data-ttu-id="940dc-260">Bu amaç için "PrepareSampleDataPipeline" adlı işlem hattını Azure Data Factory iş akışında bir yılın tutarında benzetimli araç sinyalleri ve tanılama veri kümesi oluşturmak için kullanıyoruz.</span><span class="sxs-lookup"><span data-stu-id="940dc-260">For this purpose, we are using a pipeline named "PrepareSampleDataPipeline" in the Azure Data Factory workflow to generate one year's worth of simulated vehicle signals and diagnostic dataset.</span></span> <span data-ttu-id="940dc-261">Tıklatın [Data Factory özel etkinlik](http://go.microsoft.com/fwlink/?LinkId=717077) Data Factory özel DotNet etkinlik gereksinimlerinize göre özelleştirmeleri için Visual Studio çözümü karşıdan yüklemek için.</span><span class="sxs-lookup"><span data-stu-id="940dc-261">Click [Data Factory custom activity](http://go.microsoft.com/fwlink/?LinkId=717077) to download the Data Factory custom DotNet activity Visual Studio solution for customizations based on your requirements.</span></span> 

![Toplu iş akışı işleme için örnek verileri hazırlama](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig7-vehicle-telematics-prepare-sample-data-for-batch-processing.png) 

<span data-ttu-id="940dc-263">*Şekil 7 - toplu işleme iş akışı için örnek verileri hazırlama*</span><span class="sxs-lookup"><span data-stu-id="940dc-263">*Figure 7 - Prepare Sample data for batch processing workflow*</span></span>

<span data-ttu-id="940dc-264">Ardışık Düzen özel bir ADF .net oluşan etkinlik, burada göster:</span><span class="sxs-lookup"><span data-stu-id="940dc-264">The pipeline consists of a custom ADF .Net Activity, show here:</span></span>

![PrepareSampleDataPipeline etkinliği](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig8-vehicle-telematics-prepare-sample-data-pipeline.png) 

<span data-ttu-id="940dc-266">*Şekil 8 - PrepareSampleDataPipeline*</span><span class="sxs-lookup"><span data-stu-id="940dc-266">*Figure 8 - PrepareSampleDataPipeline*</span></span>

<span data-ttu-id="940dc-267">Ardışık Düzen başarıyla yürütür ve "RawCarEventsTable" veri kümesi "Hazır", yıllık değerinde benzetimli araç sinyaller ve tanılama işaretlenmiş sonra veri üretilir.</span><span class="sxs-lookup"><span data-stu-id="940dc-267">Once the pipeline executes successfully and "RawCarEventsTable" dataset is marked "Ready", one-year worth of simulated vehicle signals and diagnostic data are produced.</span></span> <span data-ttu-id="940dc-268">Aşağıdaki klasör ve dosya depolama hesabınızda "connectedcar" kapsayıcısı altında oluşturulan bakın:</span><span class="sxs-lookup"><span data-stu-id="940dc-268">You see the following folder and file created in your storage account under the "connectedcar" container:</span></span>

![PrepareSampleDataPipeline çıkış](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig9-vehicle-telematics-prepare-sample-data-pipeline-output.png) 

<span data-ttu-id="940dc-270">*Şekil 9 - PrepareSampleDataPipeline çıkış*</span><span class="sxs-lookup"><span data-stu-id="940dc-270">*Figure 9 - PrepareSampleDataPipeline Output*</span></span>

### <a name="references"></a><span data-ttu-id="940dc-271">Başvurular</span><span class="sxs-lookup"><span data-stu-id="940dc-271">References</span></span>
[<span data-ttu-id="940dc-272">Akış alımı için Azure olay hub'ı SDK</span><span class="sxs-lookup"><span data-stu-id="940dc-272">Azure Event Hub SDK for stream ingestion</span></span>](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)

<span data-ttu-id="940dc-273">[Azure Data Factory veri taşıma özellikleri](../data-factory/data-factory-data-movement-activities.md)
[Azure veri fabrikası DotNet etkinliği](../data-factory/data-factory-use-custom-activities.md)</span><span class="sxs-lookup"><span data-stu-id="940dc-273">[Azure Data Factory data movement capabilities](../data-factory/data-factory-data-movement-activities.md)
[Azure Data Factory DotNet Activity](../data-factory/data-factory-use-custom-activities.md)</span></span>

[<span data-ttu-id="940dc-274">Örnek verileri hazırlama için azure veri fabrikası DotNet etkinlik visual studio çözümü</span><span class="sxs-lookup"><span data-stu-id="940dc-274">Azure Data Factory DotNet activity visual studio solution for preparing sample data</span></span>](http://go.microsoft.com/fwlink/?LinkId=717077) 

## <a name="partition-the-dataset"></a><span data-ttu-id="940dc-275">Bölüm veri kümesi</span><span class="sxs-lookup"><span data-stu-id="940dc-275">Partition the dataset</span></span>
<span data-ttu-id="940dc-276">Ham yarı yapılandırılmış araç sinyalleri ve tanılama veri kümesi yıl/ay biçimine veri hazırlık adımı bölümlenir.</span><span class="sxs-lookup"><span data-stu-id="940dc-276">The raw semi-structured vehicle signals and diagnostic dataset are partitioned in the data preparation step into a YEAR/MONTH format.</span></span> <span data-ttu-id="940dc-277">Bu bölümleme daha verimli şekilde sorgulamak ve ölçeklenebilir uzun vadeli depolama ilk hesap dolduğunda diğerine hatası-üzerinden bir blob hesabından etkinleştirerek yükseltir.</span><span class="sxs-lookup"><span data-stu-id="940dc-277">This partitioning promotes more efficient querying and scalable long-term storage by enabling fault-over from one blob account to the next as the first account fills up.</span></span> 

>[!NOTE] 
><span data-ttu-id="940dc-278">Bu adımda çözümü, yalnızca toplu işleme için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="940dc-278">This step in the solution is applicable only to batch processing.</span></span>

<span data-ttu-id="940dc-279">Giriş ve çıkış veri veri yönetimi:</span><span class="sxs-lookup"><span data-stu-id="940dc-279">Input and output data data management:</span></span>

* <span data-ttu-id="940dc-280">**Çıktı verilerini** (etiketli *PartitionedCarEventsTable*) "Data Lake" Müşteri'nin veri temel / "rawest" form olarak uzun bir süre için tutulması sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="940dc-280">The **output data** (labeled *PartitionedCarEventsTable*) is to be kept for a long period of time as the foundational/"rawest" form of data in the customer's "Data Lake".</span></span> 
* <span data-ttu-id="940dc-281">**Giriş verileri** bu ardışık düzen genellikle atılan gibi çıktı veri girişi için tam uygunluğa sahiptir - yalnızca (sonraki kullanım için daha iyi bölümlenmiş) depolanır.</span><span class="sxs-lookup"><span data-stu-id="940dc-281">The **input data** to this pipeline would typically be discarded as the output data has full fidelity to the input - it's just stored (partitioned) better for subsequent use.</span></span>

![Bölüm araba olayları iş akışı](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig10-vehicle-telematics-partition-car-events-workflow.png)

<span data-ttu-id="940dc-283">*Şekil 10 – bölüm araba olayları iş akışı*</span><span class="sxs-lookup"><span data-stu-id="940dc-283">*Figure 10 – Partition Car Events workflow*</span></span>

<span data-ttu-id="940dc-284">Hdınsight Hive etkinliği "PartitionCarEventsPipeline içinde" kullanarak ham verileri bölümlenen.</span><span class="sxs-lookup"><span data-stu-id="940dc-284">The raw data is partitioned using a Hive HDInsight activity in "PartitionCarEventsPipeline".</span></span> <span data-ttu-id="940dc-285">1. adımda bir yıl için oluşturulan örnek verileri yıl/AYA göre bölümlenmiş.</span><span class="sxs-lookup"><span data-stu-id="940dc-285">The sample data generated in step 1 for a year is partitioned by YEAR/MONTH.</span></span> <span data-ttu-id="940dc-286">Bölümler araç sinyalleri ve tanılama verilerini her ay yılın (toplam 12 bölümler) oluşturmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="940dc-286">The partitions are used to generate vehicle signals and diagnostic data for each month (total 12 partitions) of a year.</span></span> 

![PartitionCarEventsPipeline etkinliği](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig11-vehicle-telematics-partition-car-events-pipeline.png)

<span data-ttu-id="940dc-288">*Şekil 11 - PartitionCarEventsPipeline*</span><span class="sxs-lookup"><span data-stu-id="940dc-288">*Figure 11 - PartitionCarEventsPipeline*</span></span>

<span data-ttu-id="940dc-289">***PartitionConnectedCarEvents Hive betiği***</span><span class="sxs-lookup"><span data-stu-id="940dc-289">***PartitionConnectedCarEvents Hive Script***</span></span>

<span data-ttu-id="940dc-290">"Partitioncarevents.hql" adlı aşağıdaki Hive betiğini bölümleme için kullanılır ve indirilen ZIP "\demo\src\connectedcar\scripts" klasöründe bulunur.</span><span class="sxs-lookup"><span data-stu-id="940dc-290">The following Hive script, named "partitioncarevents.hql", is used for partitioning and is located in the "\demo\src\connectedcar\scripts" folder of the downloaded zip.</span></span> 
    
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

<span data-ttu-id="940dc-291">Ardışık Düzen başarılı bir şekilde yürütüldükten sonra depolama hesabınızda "connectedcar" kapsayıcısı altında oluşturulur şu bölümlerde bakın.</span><span class="sxs-lookup"><span data-stu-id="940dc-291">Once the pipeline is executed successfully, you see the following partitions generated in your storage account under the "connectedcar" container.</span></span>

![Bölümlenmiş çıktı](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig12-vehicle-telematics-partitioned-output.png)

<span data-ttu-id="940dc-293">*Şekil 12 - bölümlenmiş çıktı*</span><span class="sxs-lookup"><span data-stu-id="940dc-293">*Figure 12 - Partitioned Output*</span></span>

<span data-ttu-id="940dc-294">Veriler artık iyileştirilmiş, daha yönetilebilir ve zengin toplu Öngörüler kazanmak için daha fazla işleme için hazırdır.</span><span class="sxs-lookup"><span data-stu-id="940dc-294">The data is now optimized, is more manageable and ready for further processing to gain rich batch insights.</span></span> 

## <a name="data-analysis"></a><span data-ttu-id="940dc-295">Veri analizi</span><span class="sxs-lookup"><span data-stu-id="940dc-295">Data Analysis</span></span>
<span data-ttu-id="940dc-296">Bu bölümde, Azure akış analizi, Azure Machine Learning, Azure Data Factory ve Azure Hdınsight araç sistem durumunu gelişmiş analizler ve alışkanlık yürüten zengin için birleştirme bakın.</span><span class="sxs-lookup"><span data-stu-id="940dc-296">In this section, you see how to combine Azure Stream Analytics, Azure Machine Learning, Azure Data Factory, and Azure HDInsight for rich advanced analytics on vehicle health and driving habits.</span></span> <span data-ttu-id="940dc-297">Burada üç alt bölümleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="940dc-297">There are three subsections here:</span></span>

1. <span data-ttu-id="940dc-298">**Machine Learning**: Bu alt bölümde bakım bakım gerektiren Araçlar ve güvenlik sorunları nedeniyle geri çekme gerektiren taşıtlardan tahmin etmek için bu çözümde kullanılan anomali algılama denemeler hakkında bilgi içerir.</span><span class="sxs-lookup"><span data-stu-id="940dc-298">**Machine Learning**: This subsection contains information on the anomaly detection experiment that we have used in this solution to predict vehicles requiring servicing maintenance and vehicles requiring recalls due to safety issues.</span></span>
2. <span data-ttu-id="940dc-299">**Gerçek zamanlı analiz**: Bu alt bölümde Stream Analytics sorgu dili kullanarak ve özel bir uygulama kullanarak gerçek zamanlı machine learning deneme faaliyete geçirmeye yönelik gerçek zamanlı analiz ilgili bilgiler içerir.</span><span class="sxs-lookup"><span data-stu-id="940dc-299">**Real-time analysis**: This subsection contains information regarding the real-time analytics using the Stream Analytics Query Language and operationalizing the machine learning experiment in real time using a custom application.</span></span>
3. <span data-ttu-id="940dc-300">**Toplu analiz**: Bu alt bölümde Azure Hdınsight ve Azure Machine Learning Azure Data Factory tarafından kullanıma hazır hale getirilmiş kullanarak toplu veri işleme ve dönüştürme ile ilgili bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="940dc-300">**Batch analysis**: This subsection contains information regarding the transforming and processing of the batch data using Azure HDInsight and Azure Machine Learning operationalized by Azure Data Factory.</span></span>

### <a name="machine-learning"></a><span data-ttu-id="940dc-301">Machine Learning</span><span class="sxs-lookup"><span data-stu-id="940dc-301">Machine Learning</span></span>
<span data-ttu-id="940dc-302">Amacımız burada Bakım veya belirli sistem durumu istatistiklerine bağlı geri çağırma gerektiren taşıtlardan tahmin etmektir.</span><span class="sxs-lookup"><span data-stu-id="940dc-302">Our goal here is to predict the vehicles that require maintenance or recall based on certain heath statistics.</span></span> <span data-ttu-id="940dc-303">Aşağıdaki varsayımlar vermiyoruz</span><span class="sxs-lookup"><span data-stu-id="940dc-303">We make the following assumptions</span></span>

* <span data-ttu-id="940dc-304">Aşağıdaki üç koşullardan biri geçerliyse taşıtlardan gerektiren **bakım Bakım**:</span><span class="sxs-lookup"><span data-stu-id="940dc-304">If one of the following three conditions are true, the vehicles require **servicing maintenance**:</span></span>
  
  * <span data-ttu-id="940dc-305">Lastiği baskısı düşük</span><span class="sxs-lookup"><span data-stu-id="940dc-305">Tire pressure is low</span></span>
  * <span data-ttu-id="940dc-306">Altyapısı Petrol düzeyinin düşük</span><span class="sxs-lookup"><span data-stu-id="940dc-306">Engine oil level is low</span></span>
  * <span data-ttu-id="940dc-307">Altyapısı sıcaklık yüksek</span><span class="sxs-lookup"><span data-stu-id="940dc-307">Engine temperature is high</span></span>
* <span data-ttu-id="940dc-308">Aşağıdaki koşullardan biri geçerliyse taşıtlardan olabilir bir **güvenlik sorunu** ve gerektiren **geri çağırma**:</span><span class="sxs-lookup"><span data-stu-id="940dc-308">If one of the following conditions are true, the vehicles may have a **safety issue** and require **recall**:</span></span>
  
  * <span data-ttu-id="940dc-309">Altyapısı sıcaklık yüksek olduğu, ancak dış sıcaklığı düşük</span><span class="sxs-lookup"><span data-stu-id="940dc-309">Engine temperature is high but outside temperature is low</span></span>
  * <span data-ttu-id="940dc-310">Altyapısı sıcaklık düşük olduğu, ancak dış sıcaklığı yüksek</span><span class="sxs-lookup"><span data-stu-id="940dc-310">Engine temperature is low but outside temperature is high</span></span>

<span data-ttu-id="940dc-311">Önceki gereksinimlerine bağlı olarak, daha fazla bilgi, araç bakım algılaması için diğeri için araç geri çağırma algılama algılamak için iki ayrı modelleri oluşturduk.</span><span class="sxs-lookup"><span data-stu-id="940dc-311">Based on the previous requirements, we have created two separate models to detect anomalies, one for vehicle maintenance detection, and one for vehicle recall detection.</span></span> <span data-ttu-id="940dc-312">Her iki bu modellerinde yerleşik asıl bileşen analiz (PCA) algoritması anomali algılama için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="940dc-312">In both these models, the built-in Principal Component Analysis (PCA) algorithm is used for anomaly detection.</span></span> 

<span data-ttu-id="940dc-313">**Bakım algılama modeli**</span><span class="sxs-lookup"><span data-stu-id="940dc-313">**Maintenance detection model**</span></span>

<span data-ttu-id="940dc-314">Üç göstergeleri - lastiği baskısı, altyapısı Petrol veya altyapısı sıcaklık - birini ilgili koşul uymazsa, bakım algılama modelini bir anomali bildirir.</span><span class="sxs-lookup"><span data-stu-id="940dc-314">If one of three indicators - tire pressure, engine oil, or engine temperature - satisfies its respective condition, the maintenance detection model reports an anomaly.</span></span> <span data-ttu-id="940dc-315">Sonuç olarak, biz yalnızca model oluşturmanın bu üç değişkenleri dikkate almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="940dc-315">As a result, we only need to consider these three variables in building the model.</span></span> <span data-ttu-id="940dc-316">Azure Machine learning'de bizim denemesinde önce kullandığımız bir **Select Columns in Dataset sütun** bu üç değişkenleri ayıklamak için modülü.</span><span class="sxs-lookup"><span data-stu-id="940dc-316">In our experiment in Azure Machine Learning, we first use a **Select Columns in Dataset** module to extract these three variables.</span></span> <span data-ttu-id="940dc-317">Sonraki PCA tabanlı anomali algılama modülü anomali algılama modelini oluşturmak için kullanırız.</span><span class="sxs-lookup"><span data-stu-id="940dc-317">Next we use the PCA-based anomaly detection module to build the anomaly detection model.</span></span> 

<span data-ttu-id="940dc-318">Asıl bileşen analiz (PCA), özellik seçimi, Sınıflandırma ve anomali algılama uygulanan machine learning'de kurulmuş bir tekniktir.</span><span class="sxs-lookup"><span data-stu-id="940dc-318">Principal Component Analysis (PCA) is an established technique in machine learning that can be applied to feature selection, classification, and anomaly detection.</span></span> <span data-ttu-id="940dc-319">PCA durum büyük olasılıkla bağıntılı değişkenleri asıl bileşenleri adı verilen değerleri kümesine içeren bir dizi dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="940dc-319">PCA converts a set of case containing possibly correlated variables, into a set of values called principal components.</span></span> <span data-ttu-id="940dc-320">PCA tabanlı modelleme anahtar fikrini küçük boyutlu bir alanı üzerine proje verileri, böylelikle daha kolay özellikleri ve anormallikleri tanımlanabilir.</span><span class="sxs-lookup"><span data-stu-id="940dc-320">The key idea of PCA-based modeling is to project data onto a lower-dimensional space so that features and anomalies can be more easily identified.</span></span>

<span data-ttu-id="940dc-321">Her yeni giriş algılama modeline anomali algılayıcısı ilk eigenvectors üzerinde kendi projeksiyon hesaplar ve normalleştirilmiş yeniden yapılandırma hata hesaplar.</span><span class="sxs-lookup"><span data-stu-id="940dc-321">For each new input to  the detection model, the anomaly detector first computes its projection on the eigenvectors, and then computes the normalized reconstruction error.</span></span> <span data-ttu-id="940dc-322">Anomali puanı bu normalleştirilmiş hatasıdır.</span><span class="sxs-lookup"><span data-stu-id="940dc-322">This normalized error is the anomaly score.</span></span> <span data-ttu-id="940dc-323">Yüksek hata, daha anormal örneğidir.</span><span class="sxs-lookup"><span data-stu-id="940dc-323">The higher the error, the more anomalous the instance is.</span></span> 

<span data-ttu-id="940dc-324">3 boyutlu boşluk nokta koordinatları lastiği baskısı, altyapısı Petrol ve altyapısı sıcaklık tarafından tanımlanan bakım algılama sorunu her kayıt kabul edilebilir.</span><span class="sxs-lookup"><span data-stu-id="940dc-324">In the maintenance detection problem, each record can be considered as a point in a 3-dimensional space defined by tire pressure, engine oil, and engine temperature coordinates.</span></span> <span data-ttu-id="940dc-325">Bu anormallikleri yakalamak için biz 3 boyutlu alanı özgün verileri PCA kullanarak 2 boyutlu boşluk yansıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="940dc-325">To capture these anomalies, we can project the original data in the 3-dimensional space onto a 2-dimensional space using PCA.</span></span> <span data-ttu-id="940dc-326">Bu nedenle, parametresi 2 PCA içinde kullanmak için bileşenlerin sayısını ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="940dc-326">Thus, we set the parameter Number of components to use in PCA to be 2.</span></span> <span data-ttu-id="940dc-327">Bu parametre, PCA tabanlı anomali algılama uygulama önemli bir rol oynar.</span><span class="sxs-lookup"><span data-stu-id="940dc-327">This parameter plays an important role in applying PCA-based anomaly detection.</span></span> <span data-ttu-id="940dc-328">PCA kullanarak planlanması verileri sonra Biz bu anormallikleri daha kolay tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="940dc-328">After projecting data using PCA, we can identify these anomalies more easily.</span></span>

<span data-ttu-id="940dc-329">**Geri çağırma anomali algılama modelini** Select Columns in Dataset ve PCA tabanlı anomali sütun kullanırız geri çağırma anomali algılama modelinde algılama modüllerini benzer şekilde.</span><span class="sxs-lookup"><span data-stu-id="940dc-329">**Recall anomaly detection model** In the recall anomaly detection model, we use the Select Columns in Dataset and PCA-based anomaly detection modules in a similar way.</span></span> <span data-ttu-id="940dc-330">Özellikle, biz ilk üç değişkenleri - sıcaklık ve hız dışında altyapısı sıcaklık - kullanarak ayıklamak **Select Columns in Dataset sütun** modülü.</span><span class="sxs-lookup"><span data-stu-id="940dc-330">Specifically, we first extract three variables - engine temperature, outside temperature, and speed - using the **Select Columns in Dataset** module.</span></span> <span data-ttu-id="940dc-331">Altyapısı sıcaklık hızı için genellikle bağıntılı bu yana biz de hızı değişken içerir.</span><span class="sxs-lookup"><span data-stu-id="940dc-331">We also include the speed variable since the engine temperature typically is correlated to the speed.</span></span> <span data-ttu-id="940dc-332">Sonraki PCA tabanlı anomali algılama modülü 2 boyutlu boşluk 3 boyutlu alanı verilerden proje için kullanırız.</span><span class="sxs-lookup"><span data-stu-id="940dc-332">Next we use PCA-based anomaly detection module to project the data from the 3-dimensional space onto a 2-dimensional space.</span></span> <span data-ttu-id="940dc-333">Geri çağırma ölçütlerini karşılamadı ve bu nedenle altyapısı sıcaklık ve dış sıcaklığı yüksek oranda olumsuz bağıntılı olduğunda araç geri çağırma gerektirir.</span><span class="sxs-lookup"><span data-stu-id="940dc-333">The recall criteria are satisfied and so the vehicle requires recall when engine temperature and outside temperature are highly negatively correlated.</span></span> <span data-ttu-id="940dc-334">PCA tabanlı anomali algılama algoritması kullanan, biz anormallikleri PCA gerçekleştirildikten sonra yakalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="940dc-334">Using PCA-based anomaly detection algorithm, we can capture the anomalies after performing PCA.</span></span> 

<span data-ttu-id="940dc-335">Her iki modeli eğitimindeki biz Bakım veya geri çağırma PCA tabanlı anomali algılama modelini eğitmek için girdi verisi olarak gerektirmez normal veri kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="940dc-335">When training either model, we need to use normal data, which does not require maintenance or recall as the input data to train the PCA-based anomaly detection model.</span></span> <span data-ttu-id="940dc-336">Puanlama denemesinde eğitilen anomali algılama modelini araç Bakım veya geri çağırma gerektirip gerektirmediğini algılamak için kullanırız.</span><span class="sxs-lookup"><span data-stu-id="940dc-336">In the scoring experiment, we use the trained anomaly detection model to detect whether or not the vehicle requires maintenance or recall.</span></span> 

### <a name="real-time-analysis"></a><span data-ttu-id="940dc-337">Gerçek zamanlı analiz</span><span class="sxs-lookup"><span data-stu-id="940dc-337">Real-time analysis</span></span>
<span data-ttu-id="940dc-338">Aşağıdaki akış analizi SQL sorgusunu araç hızı, yakıt düzeyi, altyapısı sıcaklık, Kilometre Sayacı okuma, lastiği baskısı, altyapısı Petrol düzeyinin ve diğerleri gibi tüm önemli araç parametreleri ortalamasını almak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="940dc-338">The following Stream Analytics SQL Query is used to get the average of all the important vehicle parameters like vehicle speed, fuel level, engine temperature, odometer reading, tire pressure, engine oil level, and others.</span></span> <span data-ttu-id="940dc-339">Ortalamalar anormallikleri algılayıp, uyarılar, sorun belirli bölgede işletilen taşıtlardan genel sistem durumu koşulları belirlemek ve demografisine için ilişkilendirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="940dc-339">The averages are used to detect anomalies, issue alerts, and determine the overall health conditions of vehicles operated in specific region and then correlate it to demographics.</span></span> 

![Stream Analytics sorgu için gerçek zamanlı işleme](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig13-vehicle-telematics-stream-analytics-query-for-real-time-processing.png)

<span data-ttu-id="940dc-341">*Şekil 13 – Stream Analytics sorgu için gerçek zamanlı işleme*</span><span class="sxs-lookup"><span data-stu-id="940dc-341">*Figure 13 – Stream Analytics query for real-time processing*</span></span>

<span data-ttu-id="940dc-342">Tüm ortalamalar 3 saniyelik TumblingWindow hesaplanır.</span><span class="sxs-lookup"><span data-stu-id="940dc-342">All the averages are calculated over a 3-second TumblingWindow.</span></span> <span data-ttu-id="940dc-343">Biz çakışmayan ve bitişik zaman aralıkları gerektiren bu yana TubmlingWindow bu durumda kullanıyoruz.</span><span class="sxs-lookup"><span data-stu-id="940dc-343">We are using TubmlingWindow in this case since we require non-overlapping and contiguous time intervals.</span></span> 

<span data-ttu-id="940dc-344">Azure Stream Analytics tüm "Pencereleme" özellikleri hakkında daha fazla bilgi edinmek için tıklayın [Pencereleme (Azure akış analizi)](https://msdn.microsoft.com/library/azure/dn835019.aspx).</span><span class="sxs-lookup"><span data-stu-id="940dc-344">To learn more about all the "Windowing" capabilities in Azure Stream Analytics, click [Windowing (Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835019.aspx).</span></span>

<span data-ttu-id="940dc-345">**Gerçek zamanlı tahmin**</span><span class="sxs-lookup"><span data-stu-id="940dc-345">**Real-time prediction**</span></span>

<span data-ttu-id="940dc-346">Bir uygulamayı gerçek zamanlı machine learning modelini faaliyete çözümün parçası olarak dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="940dc-346">An application is included as part of the solution to operationalize the machine learning model in real time.</span></span> <span data-ttu-id="940dc-347">"RealTimeDashboardApp" olarak adlandırılan bu uygulama oluşturulur ve çözüm dağıtımının bir parçası yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="940dc-347">This application called “RealTimeDashboardApp” is created and configured as part of the solution deployment.</span></span> <span data-ttu-id="940dc-348">Uygulama aşağıdakileri gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="940dc-348">The application performs the following:</span></span>

1. <span data-ttu-id="940dc-349">Olay hub'ı örneği burada Stream Analytics olayları bir modelinde sürekli yayımlama dinler.</span><span class="sxs-lookup"><span data-stu-id="940dc-349">Listens to an Event Hub instance where Stream Analytics is publishing the events in a pattern continuously.</span></span> <span data-ttu-id="940dc-350">![Verileri yayımlamak için stream Analytics sorgu](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig14-vehicle-telematics-stream-analytics-query-for-publishing.png) *Şekil 14 – bir çıkış veri yayımlamak için Stream Analytics sorgu olay hub'ı örneği*</span><span class="sxs-lookup"><span data-stu-id="940dc-350">![Stream Analytics query for publishing the data](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig14-vehicle-telematics-stream-analytics-query-for-publishing.png) *Figure 14 – Stream Analytics query for publishing the data to an output Event Hub instance*</span></span> 
2. <span data-ttu-id="940dc-351">Bu uygulamayı alır her olay için:</span><span class="sxs-lookup"><span data-stu-id="940dc-351">For every event that this application receives:</span></span> 
   
   * <span data-ttu-id="940dc-352">Machine Learning istek-yanıt Puanlama (RR) uç noktası kullanarak verileri işler.</span><span class="sxs-lookup"><span data-stu-id="940dc-352">Processes the data using Machine Learning Request-Response Scoring (RRS) endpoint.</span></span> <span data-ttu-id="940dc-353">RRS endpoint dağıtımının bir parçası otomatik olarak yayımlanır.</span><span class="sxs-lookup"><span data-stu-id="940dc-353">The RRS endpoint is automatically published as part of the deployment.</span></span>
   * <span data-ttu-id="940dc-354">RRS çıkış push API'lerini kullanarak bir Power BI veri kümesine yayımlanır.</span><span class="sxs-lookup"><span data-stu-id="940dc-354">The RRS output is published to a Power BI dataset using the push APIs.</span></span>

<span data-ttu-id="940dc-355">Bu deseni, bir iş kolu (LoB) uygulaması uyarılar, bildirimler ve mesajlaşma gibi senaryolar için gerçek zamanlı analiz akış ile tümleştirmek istediğiniz senaryoları için de geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="940dc-355">This pattern is also applicable to scenarios in which you want to integrate a Line of Business (LoB) application with the real-time analytics flow, for scenarios such as alerts, notifications, and messaging.</span></span>

<span data-ttu-id="940dc-356">Tıklatın [RealtimeDashboardApp indirme](http://go.microsoft.com/fwlink/?LinkId=717078) özelleştirmeler RealtimeDashboardApp Visual Studio çözümü karşıdan yüklemek için.</span><span class="sxs-lookup"><span data-stu-id="940dc-356">Click [RealtimeDashboardApp download](http://go.microsoft.com/fwlink/?LinkId=717078) to download the RealtimeDashboardApp Visual Studio solution for customizations.</span></span> 

<span data-ttu-id="940dc-357">**Gerçek zamanlı Pano uygulamasını çalıştırmak için**</span><span class="sxs-lookup"><span data-stu-id="940dc-357">**To execute the Real-time Dashboard Application**</span></span>
1. <span data-ttu-id="940dc-358">Ayıklayın ve yerel olarak Kaydet ![RealtimeDashboardApp klasörü](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig16-vehicle-telematics-realtimedashboardapp-folder.png) *Şekil 16 – RealtimeDashboardApp klasörü*</span><span class="sxs-lookup"><span data-stu-id="940dc-358">Extract and save locally ![RealtimeDashboardApp folder](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig16-vehicle-telematics-realtimedashboardapp-folder.png) *Figure 16 – RealtimeDashboardApp folder*</span></span>  
2. <span data-ttu-id="940dc-359">Uygulamanın RealtimeDashboardApp.exe yürütme</span><span class="sxs-lookup"><span data-stu-id="940dc-359">Execute the application RealtimeDashboardApp.exe</span></span>
3. <span data-ttu-id="940dc-360">Geçerli Power BI kimlik bilgilerini sağlayın, oturum açın ve Kabul Et'i tıklatın</span><span class="sxs-lookup"><span data-stu-id="940dc-360">Provide valid Power BI credentials, sign in and click Accept</span></span> ![Gerçek zamanlı Pano uygulama oturum açma Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig17a-vehicle-telematics-realtimedashboardapp-sign-in-to-powerbi.png) ![Gerçek zamanlı Pano uygulaması son oturum açma Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig17b-vehicle-telematics-realtimedashboardapp-sign-in-to-powerbi.png) 

<span data-ttu-id="940dc-363">*Şekil 17 – RealtimeDashboardApp: Oturum açma Power BI*</span><span class="sxs-lookup"><span data-stu-id="940dc-363">*Figure 17 – RealtimeDashboardApp: Sign-in to Power BI*</span></span>

>[!NOTE] 
><span data-ttu-id="940dc-364">Power BI veri kümesi temizlemek isterseniz, "flushdata" parametresiyle RealtimeDashboardApp yürütün:</span><span class="sxs-lookup"><span data-stu-id="940dc-364">If you want to flush the Power BI dataset, execute the RealtimeDashboardApp with the "flushdata" parameter:</span></span> 

    RealtimeDashboardApp.exe -flushdata


### <a name="batch-analysis"></a><span data-ttu-id="940dc-365">Toplu iş analiz</span><span class="sxs-lookup"><span data-stu-id="940dc-365">Batch analysis</span></span>
<span data-ttu-id="940dc-366">Burada amaç, Contoso Motors düzeni, kullanım davranışı ve araç durumunu yürüten üzerinde zengin serisidir büyük veri harekete geçirmek Azure işlem özellikleri nasıl kullanacağını göstermektir.</span><span class="sxs-lookup"><span data-stu-id="940dc-366">The goal here is to show how Contoso Motors utilizes the Azure compute capabilities to harness big data to gain rich insights on driving pattern, usage behavior, and vehicle health.</span></span> <span data-ttu-id="940dc-367">Bu, mümkün kılar:</span><span class="sxs-lookup"><span data-stu-id="940dc-367">This makes it possible to:</span></span>

* <span data-ttu-id="940dc-368">Müşteri deneyimini geliştirmek ve alışkanlık ve yakıt verimli yönlendirmeli davranışları yürüten üzerinde Öngörüler sağlayarak daha ucuzdur yapın</span><span class="sxs-lookup"><span data-stu-id="940dc-368">Improve the customer experience and make it cheaper by providing insights on driving habits and fuel efficient driving behaviors</span></span>
* <span data-ttu-id="940dc-369">Müşteriler ve bunların yönlendirmeli patters iş kararları yönetir ve en iyi sınıf ürünler ve hizmetler sağlamak için proaktif olarak öğrenin</span><span class="sxs-lookup"><span data-stu-id="940dc-369">Learn proactively about customers and their driving patters to govern business decisions and provide the best in class products & services</span></span>

<span data-ttu-id="940dc-370">Bu çözümde, biz aşağıdaki ölçümleri hedeflediğiniz:</span><span class="sxs-lookup"><span data-stu-id="940dc-370">In this solution, we are targeting the following metrics:</span></span>

1. <span data-ttu-id="940dc-371">**Davranış yürüten etkin**: modelleri, konumları, yönlendirmeli koşullar, saat ve agresif yönlendirmeli modeli Öngörüler elde etmek için yılın eğilimi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="940dc-371">**Aggressive driving behavior**: Identifies the trend of the models, locations, driving conditions, and time of the year to gain insights on aggressive driving patterns.</span></span> <span data-ttu-id="940dc-372">Contoso Motors bu Öngörüler kişiselleştirilmiş yeni özellikler ve kullanım tabanlı sigorta yürüten pazarlama kampanyaları için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="940dc-372">Contoso Motors can use these insights for marketing campaigns, driving new personalized features and usage-based insurance.</span></span>
2. <span data-ttu-id="940dc-373">**Yakıt Al verimli yönlendirmeli davranışı**: modelleri, konumları, yönlendirmeli koşullar, saat ve yakıt verimli yönlendirmeli modeli Öngörüler elde etmek için yılın eğilimi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="940dc-373">**Fuel efficient driving behavior**: Identifies the trend of the models, locations, driving conditions, and time of the year to gain insights on fuel efficient driving patterns.</span></span> <span data-ttu-id="940dc-374">Contoso Motors bu Öngörüler, pazarlama kampanyalarının için yeni özellikler yürüten kullanabilirsiniz ve sürücülerini öngörülü raporlama etkili ve ortam kolay yönlendirmeli alışkanlıklarınıza maliyeti.</span><span class="sxs-lookup"><span data-stu-id="940dc-374">Contoso Motors can use these insights for marketing campaigns, driving new features and proactive reporting to the drivers for cost effective and environment friendly driving habits.</span></span> 
3. <span data-ttu-id="940dc-375">**Modelleri geri çağırma**: anomali algılama makine öğrenimi denemesinin faaliyete geçirmeye yönelik geri çekme gerektiren modelleri tanımlar</span><span class="sxs-lookup"><span data-stu-id="940dc-375">**Recall models**: Identifies models requiring recalls by operationalizing the anomaly detection machine learning experiment</span></span>

<span data-ttu-id="940dc-376">Her bir bu ölçümleri ayrıntılara göz atalım,</span><span class="sxs-lookup"><span data-stu-id="940dc-376">Let's look into the details of each of these metrics,</span></span>

<span data-ttu-id="940dc-377">**Agresif yönlendirmeli düzeni**</span><span class="sxs-lookup"><span data-stu-id="940dc-377">**Aggressive driving pattern**</span></span>

<span data-ttu-id="940dc-378">Bölümlenmiş araç sinyalleri ve Tanılama verileri ", agresif yürüten sergiler, modelleri, konum, araç, yönlendirmeli koşullar ve diğer parametreleri belirlemek için Hive kullanarak AggresiveDrivingPatternPipeline" adlı ardışık düzeninde işlenir Desen.</span><span class="sxs-lookup"><span data-stu-id="940dc-378">The partitioned vehicle signals and diagnostic data are processed in the pipeline named "AggresiveDrivingPatternPipeline" using Hive to determine the models, location, vehicle, driving conditions, and other parameters that exhibits aggressive driving pattern.</span></span>

<span data-ttu-id="940dc-379">![Agresif yönlendirmeli düzeni iş akışı](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig18-vehicle-telematics-aggressive-driving-pattern.png) 
*Şekil 18 – agresif yönlendirmeli düzeni iş akışı*</span><span class="sxs-lookup"><span data-stu-id="940dc-379">![Aggressive driving pattern workflow](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig18-vehicle-telematics-aggressive-driving-pattern.png) 
*Figure 18 – Aggressive driving pattern workflow*</span></span>


<span data-ttu-id="940dc-380">***Agresif yönlendirmeli düzeni Hive sorgusu***</span><span class="sxs-lookup"><span data-stu-id="940dc-380">***Aggressive driving pattern Hive query***</span></span>

<span data-ttu-id="940dc-381">"Aggresivedriving.hql agresif yönlendirmeli koşul düzeni çözümlemek için kullanılan" adlandırılmış Hive betiğini indirilen ZIP "\demo\src\connectedcar\scripts" klasör bulunur.</span><span class="sxs-lookup"><span data-stu-id="940dc-381">The Hive script named "aggresivedriving.hql" used for analyzing aggressive driving condition pattern is located at "\demo\src\connectedcar\scripts" folder of the downloaded zip.</span></span> 

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


<span data-ttu-id="940dc-382">En yüksek hızda düzeni braking göre reckless/agresif yönlendirmeli davranışlarını algılamak için araç'ın iletim dişli konumu, Fren pedal durumu ve hız birleşimini kullanır.</span><span class="sxs-lookup"><span data-stu-id="940dc-382">It uses the combination of vehicle's transmission gear position, brake pedal status, and speed to detect reckless/aggressive driving behavior based on braking pattern at high speed.</span></span> 

<span data-ttu-id="940dc-383">Ardışık Düzen başarılı bir şekilde yürütüldükten sonra depolama hesabınızda "connectedcar" kapsayıcısı altında oluşturulur şu bölümlerde bakın.</span><span class="sxs-lookup"><span data-stu-id="940dc-383">Once the pipeline is executed successfully, you see the following partitions generated in your storage account under the "connectedcar" container.</span></span>

![AggressiveDrivingPatternPipeline çıkış](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig19-vehicle-telematics-aggressive-driving-pattern-output.png) 

<span data-ttu-id="940dc-385">*Şekil 19 – AggressiveDrivingPatternPipeline çıkış*</span><span class="sxs-lookup"><span data-stu-id="940dc-385">*Figure 19 – AggressiveDrivingPatternPipeline output*</span></span>

<span data-ttu-id="940dc-386">**Yakıt verimli yönlendirmeli düzeni**</span><span class="sxs-lookup"><span data-stu-id="940dc-386">**Fuel efficient driving pattern**</span></span>

<span data-ttu-id="940dc-387">Bölümlenmiş araç sinyalleri ve tanılama veri "FuelEfficientDrivingPatternPipeline" adlı ardışık düzeninde işlenir.</span><span class="sxs-lookup"><span data-stu-id="940dc-387">The partitioned vehicle signals and diagnostic data are processed in the pipeline named "FuelEfficientDrivingPatternPipeline".</span></span> <span data-ttu-id="940dc-388">Hive modelleri, konum, araç, yönlendirmeli koşullar ve yakıt verimli yönlendirmeli düzeni sergilemesine diğer özelliklerini belirlemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="940dc-388">Hive is used to determine the models, location, vehicle, driving conditions, and other properties that exhibit fuel efficient driving pattern.</span></span>

![Fuel-Efficient yönlendirmeli düzeni](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig19-vehicle-telematics-fuel-efficient-driving-pattern.png) 

<span data-ttu-id="940dc-390">*Şekil 20 – Fuel-efficient yönlendirmeli düzeni iş akışı*</span><span class="sxs-lookup"><span data-stu-id="940dc-390">*Figure 20 – Fuel-efficient driving pattern workflow*</span></span>

<span data-ttu-id="940dc-391">***Yakıt verimli yönlendirmeli düzeni Hive sorgusu***</span><span class="sxs-lookup"><span data-stu-id="940dc-391">***Fuel efficient driving pattern Hive query***</span></span>

<span data-ttu-id="940dc-392">"Fuelefficientdriving.hql agresif yönlendirmeli koşul düzeni çözümlemek için kullanılan" adlandırılmış Hive betiğini indirilen ZIP "\demo\src\connectedcar\scripts" klasör bulunur.</span><span class="sxs-lookup"><span data-stu-id="940dc-392">The Hive script named "fuelefficientdriving.hql" used for analyzing aggressive driving condition pattern is located at "\demo\src\connectedcar\scripts" folder of the downloaded zip.</span></span> 

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


<span data-ttu-id="940dc-393">Araç'ın iletim dişli konumu bileşimini kullanır, Fren pedal durumu, hızlı ve Hızlandırıcı braking, hızlandırmasını, temel yakıt verimli yönlendirmeli davranışlarını algılamak için konumunu pedal ve desenler hızı.</span><span class="sxs-lookup"><span data-stu-id="940dc-393">It uses the combination of vehicle's transmission gear position, brake pedal status, speed, and accelerator pedal position to detect fuel efficient driving behavior based on acceleration, braking, and speed patterns.</span></span> 

<span data-ttu-id="940dc-394">Ardışık Düzen başarılı bir şekilde yürütüldükten sonra depolama hesabınızda "connectedcar" kapsayıcısı altında oluşturulur şu bölümlerde bakın.</span><span class="sxs-lookup"><span data-stu-id="940dc-394">Once the pipeline is executed successfully, you see the following partitions generated in your storage account under the "connectedcar" container.</span></span>

![FuelEfficientDrivingPatternPipeline çıkış](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig20-vehicle-telematics-fuel-efficient-driving-pattern-output.png) 

<span data-ttu-id="940dc-396">*Şekil 21 – FuelEfficientDrivingPatternPipeline çıkış*</span><span class="sxs-lookup"><span data-stu-id="940dc-396">*Figure 21 – FuelEfficientDrivingPatternPipeline output*</span></span>

<span data-ttu-id="940dc-397">**Tahminleri geri çağırma**</span><span class="sxs-lookup"><span data-stu-id="940dc-397">**Recall Predictions**</span></span>

<span data-ttu-id="940dc-398">Deneme öğrenme makine sağlandığında ve çözüm dağıtımının bir parçası olarak bir web hizmeti olarak yayımlanır.</span><span class="sxs-lookup"><span data-stu-id="940dc-398">The machine learning experiment is provisioned and published as a web service as part of the solution deployment.</span></span> <span data-ttu-id="940dc-399">Data factory bağlantılı hizmet olarak kayıtlı ve veri fabrikası toplu iş Puanlama etkinliği kullanarak kullanıma hazır hale getirilmiş bu iş akışında, toplu Puanlama uç noktası yararlanır.</span><span class="sxs-lookup"><span data-stu-id="940dc-399">The batch scoring end point is leveraged in this workflow, registered as a data factory linked service and operationalized using data factory batch scoring activity.</span></span>

![Machine Learning uç noktası](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig21-vehicle-telematics-machine-learning-endpoint.png) 

<span data-ttu-id="940dc-401">*Veri fabrikasında bağlı hizmet olarak Şekil 22 – Machine learning uç noktası kayıtlı*</span><span class="sxs-lookup"><span data-stu-id="940dc-401">*Figure 22 – Machine learning endpoint registered as a linked service in data factory*</span></span>

<span data-ttu-id="940dc-402">Kayıtlı bağlantılı hizmet DetectAnomalyPipeline anomali algılama modelini kullanarak veri Puanlama amacıyla kullanılır.</span><span class="sxs-lookup"><span data-stu-id="940dc-402">The registered linked service is used in the DetectAnomalyPipeline to score the data using the anomaly detection model.</span></span> 

![Machine Learning toplu veri fabrikasında Puanlama etkinliği](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig22-vehicle-telematics-aml-batch-scoring.png) 

<span data-ttu-id="940dc-404">*Şekil 23 – veri fabrikasında Azure Machine Learning toplu Puanlama etkinliği*</span><span class="sxs-lookup"><span data-stu-id="940dc-404">*Figure 23 – Azure Machine Learning Batch Scoring activity in data factory*</span></span> 

<span data-ttu-id="940dc-405">Web hizmeti Puanlama toplu işlemle operationalized böylece bu ardışık düzendeki veri hazırlığı için gerçekleştirilen birkaç adım vardır.</span><span class="sxs-lookup"><span data-stu-id="940dc-405">There are few steps performed in this pipeline for data preparation so that it can be operationalized with the batch scoring web service.</span></span> 

![Geri çekme gerektiren taşıtlardan tahmin etmeye yönelik DetectAnomalyPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig23-vehicle-telematics-pipeline-predicting-recalls.png) 

<span data-ttu-id="940dc-407">*Şekil 24 – geri çekme gerektiren taşıtlardan tahmin etmeye yönelik DetectAnomalyPipeline*</span><span class="sxs-lookup"><span data-stu-id="940dc-407">*Figure 24 – DetectAnomalyPipeline for predicting vehicles requiring recalls*</span></span> 

<span data-ttu-id="940dc-408">***Anomali algılama Hive sorgusu***</span><span class="sxs-lookup"><span data-stu-id="940dc-408">***Anomaly detection Hive query***</span></span>

<span data-ttu-id="940dc-409">Puanlama tamamlandığında, bir Hdınsight etkinliği işlemek ve anormallikleri 0.60 olasılık puanı modeli tarafından olarak kategorilere ayrılmış veya daha yüksek veri toplamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="940dc-409">Once the scoring is completed, an HDInsight activity is used to process and aggregate the data that are categorized as anomalies by the model with a probability score of 0.60 or higher.</span></span>

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


<span data-ttu-id="940dc-410">Ardışık Düzen başarılı bir şekilde yürütüldükten sonra depolama hesabınızda "connectedcar" kapsayıcısı altında oluşturulur şu bölümlerde bakın.</span><span class="sxs-lookup"><span data-stu-id="940dc-410">Once the pipeline is executed successfully, you see the following partitions generated in your storage account under the "connectedcar" container.</span></span>

![DetectAnomalyPipeline çıkış](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig24-vehicle-telematics-detect-anamoly-pipeline-output.png) 

<span data-ttu-id="940dc-412">*Şekil 25 – DetectAnomalyPipeline çıkış*</span><span class="sxs-lookup"><span data-stu-id="940dc-412">*Figure 25 – DetectAnomalyPipeline output*</span></span>

## <a name="publish"></a><span data-ttu-id="940dc-413">Yayımlama</span><span class="sxs-lookup"><span data-stu-id="940dc-413">Publish</span></span>

### <a name="real-time-analysis"></a><span data-ttu-id="940dc-414">Gerçek zamanlı analiz</span><span class="sxs-lookup"><span data-stu-id="940dc-414">Real-time analysis</span></span>
<span data-ttu-id="940dc-415">Bir çıkış akış analizi işi sorgularda birini yayımlar olayların Event Hub örneği.</span><span class="sxs-lookup"><span data-stu-id="940dc-415">One of the queries in the Stream Analytics job publishes the events to an output Event Hub instance.</span></span> 

![Akış analizi işi yayımlar için çıktı olay hub'ı örneği](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig25-vehicle-telematics-stream-analytics-job-publishes-output-event-hub.png)

<span data-ttu-id="940dc-417">*Şekil 26 – Stream Analytics işi yayımlar için çıktı olay hub'ı örneği*</span><span class="sxs-lookup"><span data-stu-id="940dc-417">*Figure 26 – Stream Analytics job publishes to an output Event Hub instance*</span></span>

![Stream Analytics sorgu çıkışı yayımlamak için olay hub'ı örneği](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig26-vehicle-telematics-stream-analytics-query-publish-output-event-hub.png)

<span data-ttu-id="940dc-419">*Şekil 27 – çıkışı yayımlamak için Stream Analytics sorgu olay hub'ı örneği*</span><span class="sxs-lookup"><span data-stu-id="940dc-419">*Figure 27 – Stream Analytics query to publish to the output Event Hub instance*</span></span>

<span data-ttu-id="940dc-420">Bu akış olayların çözümdeki RealTimeDashboardApp tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="940dc-420">This stream of events is consumed by the RealTimeDashboardApp included in the solution.</span></span> <span data-ttu-id="940dc-421">Bu uygulamayı gerçek zamanlı Puanlama için makine öğrenme istek-yanıt web hizmetini kullanır ve Power BI veri kümesi tüketimi için sonuç verileri yayımlar.</span><span class="sxs-lookup"><span data-stu-id="940dc-421">This application leverages the Machine Learning Request-Response web service for real-time scoring and publishes the resultant data to a Power BI dataset for consumption.</span></span> 

### <a name="batch-analysis"></a><span data-ttu-id="940dc-422">Toplu iş analiz</span><span class="sxs-lookup"><span data-stu-id="940dc-422">Batch analysis</span></span>
<span data-ttu-id="940dc-423">Toplu işlem ve gerçek zamanlı işleme sonuçlarını tüketimi için Azure SQL veritabanı tabloları yayımlanır.</span><span class="sxs-lookup"><span data-stu-id="940dc-423">The results of the batch and real-time processing are published to the Azure SQL Database tables for consumption.</span></span> <span data-ttu-id="940dc-424">Azure SQL Server, veritabanı ve tablo Kurulum komut dosyasının bir parçası otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="940dc-424">The Azure SQL Server, Database, and the tables are created automatically as part of the setup script.</span></span> 

![Veri reyonu akışına toplu işleme sonuçlarını kopyalayın](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig27-vehicle-telematics-batch-processing-results-copy-to-data-mart.png)

<span data-ttu-id="940dc-426">*Şekil 28 – toplu veri reyonu akışına sonuçları kopyalama işleme*</span><span class="sxs-lookup"><span data-stu-id="940dc-426">*Figure 28 – Batch processing results copy to data mart workflow*</span></span>

![Akış analizi işi veri reyonuna yayımlar](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig28-vehicle-telematics-stream-analytics-job-publishes-to-data-mart.png)

<span data-ttu-id="940dc-428">*Şekil 29 – Stream Analytics işi veri reyonuna yayımlar*</span><span class="sxs-lookup"><span data-stu-id="940dc-428">*Figure 29 – Stream Analytics job publishes to data mart*</span></span>

![Veri reyonu ayarında Stream Analytics işi](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig29-vehicle-telematics-data-mart-setting-in-stream-analytics-job.png)

<span data-ttu-id="940dc-430">*Şekil 30 – Data mart Stream Analytics işinde ayarlama*</span><span class="sxs-lookup"><span data-stu-id="940dc-430">*Figure 30 – Data mart setting in Stream Analytics job*</span></span>

## <a name="consume"></a><span data-ttu-id="940dc-431">Tüketme</span><span class="sxs-lookup"><span data-stu-id="940dc-431">Consume</span></span>
<span data-ttu-id="940dc-432">Power BI Bu çözüm gerçek zamanlı veri ve Tahmine dayalı analiz görselleştirmeleri için zengin bir Pano sağlar.</span><span class="sxs-lookup"><span data-stu-id="940dc-432">Power BI gives this solution a rich dashboard for real-time data and predictive analytics visualizations.</span></span> 

<span data-ttu-id="940dc-433">Power BI raporları ve panoyu ayarlama hakkında ayrıntılı yönergeler için buraya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="940dc-433">Click here for detailed instructions on setting up the Power BI reports and the dashboard.</span></span> <span data-ttu-id="940dc-434">Son Pano şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="940dc-434">The final dashboard looks like this:</span></span>

![Power BI Panosu](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig30-vehicle-telematics-powerbi-dashboard.png)

<span data-ttu-id="940dc-436">*Şekil 31 - Power BI Panosu*</span><span class="sxs-lookup"><span data-stu-id="940dc-436">*Figure 31 - Power BI Dashboard*</span></span>

## <a name="summary"></a><span data-ttu-id="940dc-437">Özet</span><span class="sxs-lookup"><span data-stu-id="940dc-437">Summary</span></span>
<span data-ttu-id="940dc-438">Bu belgede ayrıntılı ayrıntıya araç Telemetri analizi çözümün içerir.</span><span class="sxs-lookup"><span data-stu-id="940dc-438">This document contains a detailed drill-down of the Vehicle Telemetry Analytics Solution.</span></span> <span data-ttu-id="940dc-439">Bu bir lambda mimarisi desenini paylaşan gerçek zamanlı ve toplu analytics Öngörüler ve Eylemler ile.</span><span class="sxs-lookup"><span data-stu-id="940dc-439">This showcases a lambda architecture pattern for real-time and batch analytics with predictions and actions.</span></span> <span data-ttu-id="940dc-440">Çeşitli etkin yolunuzda (gerçek zamanlı) gerektiren kullanım durumları için bu deseni uygular ve yolunuzda (toplu) analytics.</span><span class="sxs-lookup"><span data-stu-id="940dc-440">This pattern applies to a wide range of use cases that require hot path (real-time) and cold path (batch) analytics.</span></span> 

