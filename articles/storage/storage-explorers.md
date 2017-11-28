---
title: "Azure Storage ile çalışmak için Araçlar | Microsoft Docs"
description: "Görünüm/Azure Storage verilerinizle etkileşim olanak sağlayan araçlar listesi."
services: storage
documentationcenter: 
author: dineshmurthy
manager: jahogg
editor: tysonn
ms.assetid: e4748642-98c4-437e-b0ed-4f9641c2e894
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: dineshmurthy
ms.openlocfilehash: 620efda06d8225b21b6bb9b104b79061ebb6515c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-storage-client-tools"></a><span data-ttu-id="e854f-103">Azure Storage İstemci Araçları</span><span class="sxs-lookup"><span data-stu-id="e854f-103">Azure Storage Client Tools</span></span>
<span data-ttu-id="e854f-104">Azure Storage kullanıcılarının sık bir Azure Storage istemci araç kullanarak kullanıcıların verileriyle görünüm/etkileşim kurmak kullanabilmek ister.</span><span class="sxs-lookup"><span data-stu-id="e854f-104">Users of Azure Storage frequently want to be able to view/interact with their data using an Azure Storage client tool.</span></span> <span data-ttu-id="e854f-105">Aşağıdaki tablolarda, bunu yapmak izin araçları sayısını listeler.</span><span class="sxs-lookup"><span data-stu-id="e854f-105">In the tables below, we list a number of tools that allow you to do this.</span></span> <span data-ttu-id="e854f-106">Ya da numaralandırır ve/veya veri soyutlama erişim olanağı sağlar, biz "X" her blok yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="e854f-106">We put an "X" in each block if it provides the ability to either enumerate and/or access the data abstraction.</span></span> <span data-ttu-id="e854f-107">Tablo ayrıca araçları olup olmadığını boş olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="e854f-107">The table also shows if the tools is free or not.</span></span> <span data-ttu-id="e854f-108">"Deneme" ücretsiz deneme yoktur, ancak tam ürün boş değil gösterir.</span><span class="sxs-lookup"><span data-stu-id="e854f-108">"Trial" indicates that there is a free trial, but the full product is not free.</span></span> <span data-ttu-id="e854f-109">"Y/N" farklı bir sürümünü satın almak için uygun olsa da bir sürümünün ücretsiz olarak kullanılabilir olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="e854f-109">"Y/N" indicates that a version is available for free, while a different version is available for purchase.</span></span>

<span data-ttu-id="e854f-110">Bir anlık görüntü kullanılabilir Azure Storage istemci Araçları'nın yalnızca sağladık.</span><span class="sxs-lookup"><span data-stu-id="e854f-110">We've only provided a snapshot of the available Azure Storage client tools.</span></span> <span data-ttu-id="e854f-111">Bu araçları gelişmesi ve işlevselliğinde büyümesine devam edebilir.</span><span class="sxs-lookup"><span data-stu-id="e854f-111">These tools may continue to evolve and grow in functionality.</span></span> <span data-ttu-id="e854f-112">Düzeltmeler veya güncelleştirmeler varsa, lütfen bize bildirin bir yorum bırakın.</span><span class="sxs-lookup"><span data-stu-id="e854f-112">If there are corrections or updates, please leave a comment to let us know.</span></span> <span data-ttu-id="e854f-113">Aynı burada - gelmelidir araçlarının biliyorsanız, biz eklemediğiniz mutluluk olacaktır geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="e854f-113">The same is true if you know of tools that ought to be here - we'd be happy to add them.</span></span>

<span data-ttu-id="e854f-114">**Microsoft Azure Storage istemci araçları**</span><span class="sxs-lookup"><span data-stu-id="e854f-114">**Microsoft Azure Storage Client Tools**</span></span>

<table>
  <tr>
    <th rowspan="2"><span data-ttu-id="e854f-115">Azure Storage istemci aracı</span><span class="sxs-lookup"><span data-stu-id="e854f-115">Azure Storage Client Tool</span></span></th>
    <th rowspan="2"><span data-ttu-id="e854f-116">Blok blobu</span><span class="sxs-lookup"><span data-stu-id="e854f-116">Block Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="e854f-117">Sayfa blobu</span><span class="sxs-lookup"><span data-stu-id="e854f-117">Page Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="e854f-118">BLOB ekleme</span><span class="sxs-lookup"><span data-stu-id="e854f-118">Append Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="e854f-119">Tablolar</span><span class="sxs-lookup"><span data-stu-id="e854f-119">Tables</span></span></th>
    <th rowspan="2"><span data-ttu-id="e854f-120">Kuyruklar</span><span class="sxs-lookup"><span data-stu-id="e854f-120">Queues</span></span></th>
    <th rowspan="2"><span data-ttu-id="e854f-121">Dosyalar</span><span class="sxs-lookup"><span data-stu-id="e854f-121">Files</span></span></th>
    <th rowspan="2"><span data-ttu-id="e854f-122">Ücretsiz</span><span class="sxs-lookup"><span data-stu-id="e854f-122">Free</span></span></th>
    <th colspan="4"><span data-ttu-id="e854f-123">Platform</span><span class="sxs-lookup"><span data-stu-id="e854f-123">Platform</span></span></th>
  </tr>
  <tr>
    <td><span data-ttu-id="e854f-124">Web</span><span class="sxs-lookup"><span data-stu-id="e854f-124">Web</span></span></td>
    <td><span data-ttu-id="e854f-125">Windows</span><span class="sxs-lookup"><span data-stu-id="e854f-125">Windows</span></span></td>
    <td><span data-ttu-id="e854f-126">OSX</span><span class="sxs-lookup"><span data-stu-id="e854f-126">OSX</span></span></td>
    <td><span data-ttu-id="e854f-127">Linux</span><span class="sxs-lookup"><span data-stu-id="e854f-127">Linux</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="e854f-128"><a href="https://azure.microsoft.com/features/azure-portal/">Microsoft Azure portalı</a></span><span class="sxs-lookup"><span data-stu-id="e854f-128"><a href="https://azure.microsoft.com/features/azure-portal/">Microsoft Azure Portal</a></span></span></td>
    <td><span data-ttu-id="e854f-129">X</span><span class="sxs-lookup"><span data-stu-id="e854f-129">X</span></span></td>
    <td><span data-ttu-id="e854f-130">X</span><span class="sxs-lookup"><span data-stu-id="e854f-130">X</span></span></td>
    <td><span data-ttu-id="e854f-131">X</span><span class="sxs-lookup"><span data-stu-id="e854f-131">X</span></span></td>
    <td><span data-ttu-id="e854f-132">X</span><span class="sxs-lookup"><span data-stu-id="e854f-132">X</span></span></td>
    <td><span data-ttu-id="e854f-133">X</span><span class="sxs-lookup"><span data-stu-id="e854f-133">X</span></span></td>
    <td><span data-ttu-id="e854f-134">X</span><span class="sxs-lookup"><span data-stu-id="e854f-134">X</span></span></td>
    <td><span data-ttu-id="e854f-135">E</span><span class="sxs-lookup"><span data-stu-id="e854f-135">Y</span></span></td>
    <td><span data-ttu-id="e854f-136">X</span><span class="sxs-lookup"><span data-stu-id="e854f-136">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="e854f-137"><a href="http://storageexplorer.com/">Microsoft Azure Depolama Gezgini</a></span><span class="sxs-lookup"><span data-stu-id="e854f-137"><a href="http://storageexplorer.com/">Microsoft Azure Storage Explorer</a></span></span></td>
    <td><span data-ttu-id="e854f-138">X</span><span class="sxs-lookup"><span data-stu-id="e854f-138">X</span></span></td>
    <td><span data-ttu-id="e854f-139">X</span><span class="sxs-lookup"><span data-stu-id="e854f-139">X</span></span></td>
    <td><span data-ttu-id="e854f-140">X</span><span class="sxs-lookup"><span data-stu-id="e854f-140">X</span></span></td>
    <td><span data-ttu-id="e854f-141">X</span><span class="sxs-lookup"><span data-stu-id="e854f-141">X</span></span></td>
    <td><span data-ttu-id="e854f-142">X</span><span class="sxs-lookup"><span data-stu-id="e854f-142">X</span></span></td>
    <td><span data-ttu-id="e854f-143">X</span><span class="sxs-lookup"><span data-stu-id="e854f-143">X</span></span></td>
    <td><span data-ttu-id="e854f-144">E</span><span class="sxs-lookup"><span data-stu-id="e854f-144">Y</span></span></td>
    <td></td>
    <td><span data-ttu-id="e854f-145">X</span><span class="sxs-lookup"><span data-stu-id="e854f-145">X</span></span></td>
    <td><span data-ttu-id="e854f-146">X</span><span class="sxs-lookup"><span data-stu-id="e854f-146">X</span></span></td>
    <td><span data-ttu-id="e854f-147">X</span><span class="sxs-lookup"><span data-stu-id="e854f-147">X</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="e854f-148"><a href="https://www.visualstudio.com/features/azure-tools-vs.aspx">Microsoft Visual Studio Sunucu Gezgini</a></span><span class="sxs-lookup"><span data-stu-id="e854f-148"><a href="https://www.visualstudio.com/features/azure-tools-vs.aspx">Microsoft Visual Studio Server Explorer</a></span></span></td>
    <td><span data-ttu-id="e854f-149">X</span><span class="sxs-lookup"><span data-stu-id="e854f-149">X</span></span></td>
    <td><span data-ttu-id="e854f-150">X</span><span class="sxs-lookup"><span data-stu-id="e854f-150">X</span></span></td>
    <td><span data-ttu-id="e854f-151">X</span><span class="sxs-lookup"><span data-stu-id="e854f-151">X</span></span></td>
    <td><span data-ttu-id="e854f-152">X</span><span class="sxs-lookup"><span data-stu-id="e854f-152">X</span></span></td>
    <td><span data-ttu-id="e854f-153">X</span><span class="sxs-lookup"><span data-stu-id="e854f-153">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="e854f-154">E</span><span class="sxs-lookup"><span data-stu-id="e854f-154">Y</span></span></td>
    <td></td>
    <td><span data-ttu-id="e854f-155">X</span><span class="sxs-lookup"><span data-stu-id="e854f-155">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
</table>

<span data-ttu-id="e854f-156">**Üçüncü taraf Azure Storage istemci araçları**</span><span class="sxs-lookup"><span data-stu-id="e854f-156">**Third-Party Azure Storage Client Tools**</span></span>

<span data-ttu-id="e854f-157">Biz işlev veya aşağıdaki üçüncü taraf araçları tarafından talep kalite doğrulamadınız demektir ve bunların listeleme Microsoft tarafından bir onay anlamına gelmez.</span><span class="sxs-lookup"><span data-stu-id="e854f-157">We have not verified the functionality or quality claimed by the following third-party tools and their listing does not imply an endorsement by Microsoft.</span></span>

<table>
  <tr>
    <th rowspan="2"><span data-ttu-id="e854f-158">Azure Storage istemci aracı</span><span class="sxs-lookup"><span data-stu-id="e854f-158">Azure Storage Client Tool</span></span></th>
    <th rowspan="2"><span data-ttu-id="e854f-159">Blok blobu</span><span class="sxs-lookup"><span data-stu-id="e854f-159">Block Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="e854f-160">Sayfa blobu</span><span class="sxs-lookup"><span data-stu-id="e854f-160">Page Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="e854f-161">BLOB ekleme</span><span class="sxs-lookup"><span data-stu-id="e854f-161">Append Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="e854f-162">Tablolar</span><span class="sxs-lookup"><span data-stu-id="e854f-162">Tables</span></span></th>
    <th rowspan="2"><span data-ttu-id="e854f-163">Kuyruklar</span><span class="sxs-lookup"><span data-stu-id="e854f-163">Queues</span></span></th>
    <th rowspan="2"><span data-ttu-id="e854f-164">Dosyalar</span><span class="sxs-lookup"><span data-stu-id="e854f-164">Files</span></span></th>
    <th rowspan="2"><span data-ttu-id="e854f-165">Ücretsiz</span><span class="sxs-lookup"><span data-stu-id="e854f-165">Free</span></span></th>
    <th colspan="4"><span data-ttu-id="e854f-166">Platform</span><span class="sxs-lookup"><span data-stu-id="e854f-166">Platform</span></span></th>
  </tr>
  <tr>
    <td><span data-ttu-id="e854f-167">Web</span><span class="sxs-lookup"><span data-stu-id="e854f-167">Web</span></span></td>
    <td><span data-ttu-id="e854f-168">Windows</span><span class="sxs-lookup"><span data-stu-id="e854f-168">Windows</span></span></td>
    <td><span data-ttu-id="e854f-169">OSX</span><span class="sxs-lookup"><span data-stu-id="e854f-169">OSX</span></span></td>
    <td><span data-ttu-id="e854f-170">Linux</span><span class="sxs-lookup"><span data-stu-id="e854f-170">Linux</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="e854f-171"><a href="http://www.cloudportam.com/">Bulut Portam</a></span><span class="sxs-lookup"><span data-stu-id="e854f-171"><a href="http://www.cloudportam.com/">Cloud Portam</a></span></span></td>
    <td><span data-ttu-id="e854f-172">X</span><span class="sxs-lookup"><span data-stu-id="e854f-172">X</span></span></td>
    <td><span data-ttu-id="e854f-173">X</span><span class="sxs-lookup"><span data-stu-id="e854f-173">X</span></span></td>
    <td><span data-ttu-id="e854f-174">X</span><span class="sxs-lookup"><span data-stu-id="e854f-174">X</span></span></td>
    <td><span data-ttu-id="e854f-175">X</span><span class="sxs-lookup"><span data-stu-id="e854f-175">X</span></span></td>
    <td><span data-ttu-id="e854f-176">X</span><span class="sxs-lookup"><span data-stu-id="e854f-176">X</span></span></td>
    <td><span data-ttu-id="e854f-177">X</span><span class="sxs-lookup"><span data-stu-id="e854f-177">X</span></span></td>
    <td><span data-ttu-id="e854f-178">Deneme</span><span class="sxs-lookup"><span data-stu-id="e854f-178">Trial</span></span></td>
    <td><span data-ttu-id="e854f-179">X</span><span class="sxs-lookup"><span data-stu-id="e854f-179">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="e854f-180"><a href="http://www.cerebrata.com/products/azure-management-studio/introduction">Cerabrata: Azure Management Studio</a></span><span class="sxs-lookup"><span data-stu-id="e854f-180"><a href="http://www.cerebrata.com/products/azure-management-studio/introduction">Cerabrata: Azure Management Studio</a></span></span></td>
    <td><span data-ttu-id="e854f-181">X</span><span class="sxs-lookup"><span data-stu-id="e854f-181">X</span></span></td>
    <td><span data-ttu-id="e854f-182">X</span><span class="sxs-lookup"><span data-stu-id="e854f-182">X</span></span></td>
    <td><span data-ttu-id="e854f-183">X</span><span class="sxs-lookup"><span data-stu-id="e854f-183">X</span></span></td>
    <td><span data-ttu-id="e854f-184">X</span><span class="sxs-lookup"><span data-stu-id="e854f-184">X</span></span></td>
    <td><span data-ttu-id="e854f-185">X</span><span class="sxs-lookup"><span data-stu-id="e854f-185">X</span></span></td>
    <td><span data-ttu-id="e854f-186">X</span><span class="sxs-lookup"><span data-stu-id="e854f-186">X</span></span></td>
    <td><span data-ttu-id="e854f-187">Deneme</span><span class="sxs-lookup"><span data-stu-id="e854f-187">Trial</span></span></td>
    <td></td>
    <td><span data-ttu-id="e854f-188">X</span><span class="sxs-lookup"><span data-stu-id="e854f-188">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="e854f-189"><a href="http://www.cerebrata.com/products/azure-explorer/introduction">Cerabrata: Azure Gezgini</a></span><span class="sxs-lookup"><span data-stu-id="e854f-189"><a href="http://www.cerebrata.com/products/azure-explorer/introduction">Cerabrata: Azure Explorer</a></span></span></td>
    <td><span data-ttu-id="e854f-190">X</span><span class="sxs-lookup"><span data-stu-id="e854f-190">X</span></span></td>
    <td><span data-ttu-id="e854f-191">X</span><span class="sxs-lookup"><span data-stu-id="e854f-191">X</span></span></td>
    <td><span data-ttu-id="e854f-192">X</span><span class="sxs-lookup"><span data-stu-id="e854f-192">X</span></span></td>
    <td></td>
    <td></td>
    <td><span data-ttu-id="e854f-193">X</span><span class="sxs-lookup"><span data-stu-id="e854f-193">X</span></span></td>
    <td><span data-ttu-id="e854f-194">E</span><span class="sxs-lookup"><span data-stu-id="e854f-194">Y</span></span></td>
    <td></td>
    <td><span data-ttu-id="e854f-195">X</span><span class="sxs-lookup"><span data-stu-id="e854f-195">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="e854f-196"><a href="https://github.com/sebagomez/azurestorageexplorer">Azure Depolama Gezgini</a></span><span class="sxs-lookup"><span data-stu-id="e854f-196"><a href="https://github.com/sebagomez/azurestorageexplorer">Azure Storage Explorer</a></span></span></td>
    <td><span data-ttu-id="e854f-197">X</span><span class="sxs-lookup"><span data-stu-id="e854f-197">X</span></span></td>
    <td><span data-ttu-id="e854f-198">X</span><span class="sxs-lookup"><span data-stu-id="e854f-198">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="e854f-199">X</span><span class="sxs-lookup"><span data-stu-id="e854f-199">X</span></span></td>
    <td><span data-ttu-id="e854f-200">X</span><span class="sxs-lookup"><span data-stu-id="e854f-200">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="e854f-201">E</span><span class="sxs-lookup"><span data-stu-id="e854f-201">Y</span></span></td>
    <td></td>
    <td><span data-ttu-id="e854f-202">X</span><span class="sxs-lookup"><span data-stu-id="e854f-202">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="e854f-203"><a href="http://www.cloudberrylab.com/free-microsoft-azure-explorer.aspx">CloudBerry Gezgini</a></span><span class="sxs-lookup"><span data-stu-id="e854f-203"><a href="http://www.cloudberrylab.com/free-microsoft-azure-explorer.aspx">CloudBerry Explorer</a></span></span></td>
    <td><span data-ttu-id="e854f-204">X</span><span class="sxs-lookup"><span data-stu-id="e854f-204">X</span></span></td>
    <td><span data-ttu-id="e854f-205">X</span><span class="sxs-lookup"><span data-stu-id="e854f-205">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
    <td><span data-ttu-id="e854f-206">X</span><span class="sxs-lookup"><span data-stu-id="e854f-206">X</span></span></td>
    <td><span data-ttu-id="e854f-207">Y/N</span><span class="sxs-lookup"><span data-stu-id="e854f-207">Y/N</span></span></td>
    <td></td>
    <td><span data-ttu-id="e854f-208">X</span><span class="sxs-lookup"><span data-stu-id="e854f-208">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="e854f-209"><a href="http://www.gapotchenko.com/cloudcombine">Bulut birleştirin</a></span><span class="sxs-lookup"><span data-stu-id="e854f-209"><a href="http://www.gapotchenko.com/cloudcombine">Cloud Combine</a></span></span></td>
    <td><span data-ttu-id="e854f-210">X</span><span class="sxs-lookup"><span data-stu-id="e854f-210">X</span></span></td>
    <td><span data-ttu-id="e854f-211">X</span><span class="sxs-lookup"><span data-stu-id="e854f-211">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="e854f-212">X</span><span class="sxs-lookup"><span data-stu-id="e854f-212">X</span></span></td>
    <td><span data-ttu-id="e854f-213">X</span><span class="sxs-lookup"><span data-stu-id="e854f-213">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="e854f-214">Deneme</span><span class="sxs-lookup"><span data-stu-id="e854f-214">Trial</span></span></td>
    <td></td>
    <td><span data-ttu-id="e854f-215">X</span><span class="sxs-lookup"><span data-stu-id="e854f-215">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="e854f-216"><a href="http://clumsyleaf.com">ClumsyLeaf: AzureXplorer, CloudXplorer, TableXplorer</a></span><span class="sxs-lookup"><span data-stu-id="e854f-216"><a href="http://clumsyleaf.com">ClumsyLeaf: AzureXplorer, CloudXplorer, TableXplorer</a></span></span></td>
    <td><span data-ttu-id="e854f-217">X</span><span class="sxs-lookup"><span data-stu-id="e854f-217">X</span></span></td>
    <td><span data-ttu-id="e854f-218">X</span><span class="sxs-lookup"><span data-stu-id="e854f-218">X</span></span></td>
    <td><span data-ttu-id="e854f-219">X</span><span class="sxs-lookup"><span data-stu-id="e854f-219">X</span></span></td>
    <td><span data-ttu-id="e854f-220">X</span><span class="sxs-lookup"><span data-stu-id="e854f-220">X</span></span></td>
    <td><span data-ttu-id="e854f-221">X</span><span class="sxs-lookup"><span data-stu-id="e854f-221">X</span></span></td>
    <td><span data-ttu-id="e854f-222">X</span><span class="sxs-lookup"><span data-stu-id="e854f-222">X</span></span></td>
    <td><span data-ttu-id="e854f-223">E</span><span class="sxs-lookup"><span data-stu-id="e854f-223">Y</span></span></td>
    <td></td>
    <td><span data-ttu-id="e854f-224">X</span><span class="sxs-lookup"><span data-stu-id="e854f-224">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="e854f-225"><a href="http://www.gladinet.com/Azure-Storage/index.htm">Gladinet bulut</a></span><span class="sxs-lookup"><span data-stu-id="e854f-225"><a href="http://www.gladinet.com/Azure-Storage/index.htm">Gladinet Cloud</a></span></span></td>
    <td><span data-ttu-id="e854f-226">X</span><span class="sxs-lookup"><span data-stu-id="e854f-226">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td><span data-ttu-id="e854f-227">Deneme</span><span class="sxs-lookup"><span data-stu-id="e854f-227">Trial</span></span></td>
    <td></td>
    <td><span data-ttu-id="e854f-228">X</span><span class="sxs-lookup"><span data-stu-id="e854f-228">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="e854f-229"><a href="http://storageexplorer.codeplex.com/">Azure Web Depolama Gezgini</a></span><span class="sxs-lookup"><span data-stu-id="e854f-229"><a href="http://storageexplorer.codeplex.com/">Azure Web Storage Explorer</a></span></span></td>
    <td><span data-ttu-id="e854f-230">X</span><span class="sxs-lookup"><span data-stu-id="e854f-230">X</span></span></td>
    <td><span data-ttu-id="e854f-231">X</span><span class="sxs-lookup"><span data-stu-id="e854f-231">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="e854f-232">X</span><span class="sxs-lookup"><span data-stu-id="e854f-232">X</span></span></td>
    <td><span data-ttu-id="e854f-233">X</span><span class="sxs-lookup"><span data-stu-id="e854f-233">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="e854f-234">E</span><span class="sxs-lookup"><span data-stu-id="e854f-234">Y</span></span></td>
    <td><span data-ttu-id="e854f-235">X</span><span class="sxs-lookup"><span data-stu-id="e854f-235">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="e854f-236"><a href="https://zudio.co/">Zudio</a></span><span class="sxs-lookup"><span data-stu-id="e854f-236"><a href="https://zudio.co/">Zudio</a></span></span></td>
    <td><span data-ttu-id="e854f-237">X</span><span class="sxs-lookup"><span data-stu-id="e854f-237">X</span></span></td>
    <td><span data-ttu-id="e854f-238">X</span><span class="sxs-lookup"><span data-stu-id="e854f-238">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="e854f-239">X</span><span class="sxs-lookup"><span data-stu-id="e854f-239">X</span></span></td>
    <td><span data-ttu-id="e854f-240">X</span><span class="sxs-lookup"><span data-stu-id="e854f-240">X</span></span></td>
    <td><span data-ttu-id="e854f-241">X</span><span class="sxs-lookup"><span data-stu-id="e854f-241">X</span></span></td>
    <td><span data-ttu-id="e854f-242">Deneme</span><span class="sxs-lookup"><span data-stu-id="e854f-242">Trial</span></span></td>
    <td><span data-ttu-id="e854f-243">X</span><span class="sxs-lookup"><span data-stu-id="e854f-243">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
</table>
