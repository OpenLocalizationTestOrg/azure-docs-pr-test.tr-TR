---
title: "Stream Analytics Data Lake Store çıkış | Microsoft Docs"
description: "Kimlik doğrulama ve yetkilendirme Stream Analytics işi bir Azure Data Lake Store'da ve yapılandırma"
keywords: 
services: stream-analytics
documentationcenter: 
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: ea5baafa-0054-4c70-973a-6a3a8c6eaffc
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: 3d867df3ef875d5cc41de418c3d1d269ff751fda
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="stream-analytics-data-lake-store-output"></a><span data-ttu-id="b7da1-103">Stream Analytics Data Lake Store çıktı</span><span class="sxs-lookup"><span data-stu-id="b7da1-103">Stream Analytics Data Lake Store output</span></span>
<span data-ttu-id="b7da1-104">Akış analizi işleri birkaç çıktı yöntemlerini destekleyen bir anda bir [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/).</span><span class="sxs-lookup"><span data-stu-id="b7da1-104">Stream Analytics jobs support several output methods, one being an [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/).</span></span> <span data-ttu-id="b7da1-105">Azure Data Lake Store, büyük veri analitik iş yükleri için kuruluş çapında hiper ölçekli bir depodur.</span><span class="sxs-lookup"><span data-stu-id="b7da1-105">Azure Data Lake Store is an enterprise-wide hyper-scale repository for big data analytic workloads.</span></span> <span data-ttu-id="b7da1-106">Data Lake Store herhangi boyutu, türü ve alım hızına işletimsel ve keşifsel analiz için verilerin depolamanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="b7da1-106">Data Lake Store enables you to store data of any size, type and ingestion speed for operational and exploratory analytics.</span></span>

## <a name="authorize-a-data-lake-store-account"></a><span data-ttu-id="b7da1-107">Bir Data Lake Store hesabı yetki</span><span class="sxs-lookup"><span data-stu-id="b7da1-107">Authorize a Data Lake Store account</span></span>
1. <span data-ttu-id="b7da1-108">Data Lake Store, Azure portalında bir çıkış olarak seçildiğinde, Data Lake Store'a Klasik Portal üzerinden erişim istemek için veya varolan Data Lake Store kullanımını yetkilendirmek için istenir.</span><span class="sxs-lookup"><span data-stu-id="b7da1-108">When Data Lake Store is selected as an output in the Azure portal, you will be prompted to authorize use of your existing Data Lake Store or to request access to the Data Lake Store via the Classic Portal.</span></span>
   
   ![](media/stream-analytics-data-lake-output/stream-analytics-data-lake-output-authorization.png)  
   
2. <span data-ttu-id="b7da1-109">Data Lake Store'a erişim zaten varsa, "Şimdi Yetkilendir"'i tıklatın ve bir sayfa kısa bir süre için "Yeniden yönlendirmek için yetkilendirme" belirten yukarı pop.</span><span class="sxs-lookup"><span data-stu-id="b7da1-109">If you already have access to Data Lake Store, click “Authorize Now” and for a brief time a page will pop up indicating “Redirecting to authorization”.</span></span> <span data-ttu-id="b7da1-110">Sayfa otomatik olarak kapanır ve Data Lake Store çıkış yapılandırmanıza olanak tanır sayfayla sunulur.</span><span class="sxs-lookup"><span data-stu-id="b7da1-110">The page will automatically close and you will be presented with the page that would allow you to configure the Data Lake Store output.</span></span>

<span data-ttu-id="b7da1-111">Data Lake Store için kaydolmadıysanız, isteği başlatmak veya izleyin için "şimdi kaydolun" bağlantı izleyebilirsiniz [başlatılan yönergeleri almak](../data-lake-store/data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b7da1-111">If you have not signed up for Data Lake Store, you can follow the “Sign up now” link to initiate the request, or follow the [get started instructions](../data-lake-store/data-lake-store-get-started-portal.md).</span></span>

## <a name="configure-the-data-lake-store-output-properties"></a><span data-ttu-id="b7da1-112">Data Lake Store çıktı özelliklerini yapılandırın</span><span class="sxs-lookup"><span data-stu-id="b7da1-112">Configure the Data Lake Store output properties</span></span>
<span data-ttu-id="b7da1-113">Kimliği doğrulanmış Data Lake Store hesabına sahip olduğunda, Data Lake Store çıktı için özelliklerini yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b7da1-113">Once you have the Data Lake Store account authenticated, you can configure the properties for your Data Lake Store output.</span></span> <span data-ttu-id="b7da1-114">Aşağıdaki tablo özellik adları ve Data Lake Store çıkış yapılandırmak için açıklamalarına listesidir.</span><span class="sxs-lookup"><span data-stu-id="b7da1-114">The table below is the list of property names and their description to configure your Data Lake Store output.</span></span>

<table>
<tbody>
<tr>
<td><span data-ttu-id="b7da1-115"><B>ÖZELLİK ADI</B></span><span class="sxs-lookup"><span data-stu-id="b7da1-115"><B>PROPERTY NAME</B></span></span></td>
<td><span data-ttu-id="b7da1-116"><B>AÇIKLAMA</B></span><span class="sxs-lookup"><span data-stu-id="b7da1-116"><B>DESCRIPTION</B></span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b7da1-117">Çıkış diğer adları</span><span class="sxs-lookup"><span data-stu-id="b7da1-117">Output Alias</span></span></td>
<td><span data-ttu-id="b7da1-118">Bu, sorgu çıktısı bu Data Lake Store'a doğrudan sorgularda kullanılan kolay bir addır.</span><span class="sxs-lookup"><span data-stu-id="b7da1-118">This is a friendly name used in queries to direct the query output to this Data Lake Store.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b7da1-119">Data Lake Store hesabı</span><span class="sxs-lookup"><span data-stu-id="b7da1-119">Data Lake Store Account</span></span></td>
<td><span data-ttu-id="b7da1-120">Burada, Çıkış göndermeyi depolama hesabı adı.</span><span class="sxs-lookup"><span data-stu-id="b7da1-120">The name of the storage account where you are sending your output.</span></span> <span data-ttu-id="b7da1-121">Oturum açan kullanıcının erişimi Data Lake Store hesaplarının bir listesiyle birlikte sunulur.</span><span class="sxs-lookup"><span data-stu-id="b7da1-121">You will be presented with a list of Data Lake Store accounts  the logged in user has access to.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b7da1-122">Yol önek deseni [<I>isteğe bağlı</I>]</span><span class="sxs-lookup"><span data-stu-id="b7da1-122">Path Prefix Pattern [<I>optional</I>]</span></span></td>
<td><span data-ttu-id="b7da1-123">Belirtilen veri Gölü deposu hesabı içinde dosyalarınızı yazmak için kullanılan dosya yolu.</span><span class="sxs-lookup"><span data-stu-id="b7da1-123">The file path used to write your files within the specified Data Lake Store Account.</span></span> <BR><span data-ttu-id="b7da1-124">{date} {time}</span><span class="sxs-lookup"><span data-stu-id="b7da1-124">{date}, {time}</span></span><BR><span data-ttu-id="b7da1-125">Örnek 1: klasör1/logs / {date} / {time}</span><span class="sxs-lookup"><span data-stu-id="b7da1-125">Example 1: folder1/logs/{date}/{time}</span></span><BR><span data-ttu-id="b7da1-126">Örnek 2: klasör1/logs / {date}</span><span class="sxs-lookup"><span data-stu-id="b7da1-126">Example 2: folder1/logs/{date}</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b7da1-127">Tarih biçimi [<I>isteğe bağlı</I>]</span><span class="sxs-lookup"><span data-stu-id="b7da1-127">Date Format [<I>optional</I>]</span></span></td>
<td><span data-ttu-id="b7da1-128">Bir tarih belirteci önek yolunda kullanılırsa, dosyalarınızı organize edilmiştir tarih biçimi seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b7da1-128">If the date token is used in the prefix path, you can select the date format in which your files are organized.</span></span> <span data-ttu-id="b7da1-129">Örnek: YYYY/AA/GG</span><span class="sxs-lookup"><span data-stu-id="b7da1-129">Example: YYYY/MM/DD</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b7da1-130">Saat biçimi [<I>isteğe bağlı</I>]</span><span class="sxs-lookup"><span data-stu-id="b7da1-130">Time Format [<I>optional</I>]</span></span></td>
<td><span data-ttu-id="b7da1-131">Zaman belirteci önek yolunda kullanılırsa, dosyalarınızı düzenlenmiş zaman biçimini belirtin.</span><span class="sxs-lookup"><span data-stu-id="b7da1-131">If the time token is used in the prefix path, specify the time format in which your files are organized.</span></span> <span data-ttu-id="b7da1-132">Şu anda desteklenen tek değer HH ' dir.</span><span class="sxs-lookup"><span data-stu-id="b7da1-132">Currently the only supported value is HH.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b7da1-133">Olayı seri hale getirme biçimi</span><span class="sxs-lookup"><span data-stu-id="b7da1-133">Event Serialization Format</span></span></td>
<td><span data-ttu-id="b7da1-134">Çıkış verileri seri hale getirme biçimi.</span><span class="sxs-lookup"><span data-stu-id="b7da1-134">Serialization format for output data.</span></span> <span data-ttu-id="b7da1-135">JSON, CSV ve Avro desteklenir.</span><span class="sxs-lookup"><span data-stu-id="b7da1-135">JSON, CSV, and Avro are supported.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b7da1-136">Encoding</span><span class="sxs-lookup"><span data-stu-id="b7da1-136">Encoding</span></span></td>
<td><span data-ttu-id="b7da1-137">Bir kodlama, CSV veya JSON biçiminde, belirtilmiş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b7da1-137">If CSV or JSON format, an encoding must be specified.</span></span> <span data-ttu-id="b7da1-138">Şu anda desteklenen tek kodlama biçimi UTF-8'dir.</span><span class="sxs-lookup"><span data-stu-id="b7da1-138">UTF-8 is the only supported encoding format at this time.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b7da1-139">sınırlayıcı</span><span class="sxs-lookup"><span data-stu-id="b7da1-139">Delimiter</span></span></td>
<td><span data-ttu-id="b7da1-140">Yalnızca, CSV serileştirme için de geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="b7da1-140">Only applicable for CSV serialization.</span></span> <span data-ttu-id="b7da1-141">Akış analizi, CSV verileri seri hale getirme için bir dizi ortak sınırlayıcıları destekler.</span><span class="sxs-lookup"><span data-stu-id="b7da1-141">Stream Analytics supports a number of common delimiters for serializing CSV data.</span></span> <span data-ttu-id="b7da1-142">Virgül, noktalı virgül, boşluk, sekme ve dikey çubuk bunun desteklenen değerlerdir.</span><span class="sxs-lookup"><span data-stu-id="b7da1-142">Supported values are comma, semicolon, space, tab and vertical bar.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b7da1-143">Biçimi</span><span class="sxs-lookup"><span data-stu-id="b7da1-143">Format</span></span></td>
<td><span data-ttu-id="b7da1-144">Yalnızca JSON serileştirmesi için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="b7da1-144">Only applicable for JSON serialization.</span></span> <span data-ttu-id="b7da1-145">Ayrılmış çizgi çıkış sahip yeni bir çizgiyle ayrılmış her bir JSON nesnesi olarak biçimlendirileceğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="b7da1-145">Line separated specifies that the output will be formatted by having each JSON object separated by a new line.</span></span> <span data-ttu-id="b7da1-146">Dizi çıkışı bir dizi JSON nesnesi biçimlendirileceğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="b7da1-146">Array specifies that the output will be formatted as an array of JSON objects.</span></span></td>
</tr>
</tbody>
</table>

## <a name="renew-data-lake-store-authorization"></a><span data-ttu-id="b7da1-147">Data Lake Store yetkilendirmeyi yenileyin</span><span class="sxs-lookup"><span data-stu-id="b7da1-147">Renew Data Lake Store Authorization</span></span>
<span data-ttu-id="b7da1-148">Şu anda, burada kimlik doğrulama belirteci 90 günde Data Lake Store çıktıyla tüm işleri el ile yenilenmesi gerekiyor bir sınırlama yoktur.</span><span class="sxs-lookup"><span data-stu-id="b7da1-148">Currently, there is a limitation where the authentication token needs to be manually refreshed every 90 days for all jobs with Data Lake Store output.</span></span> <span data-ttu-id="b7da1-149">İşinizi oluşturulmuş veya son kimliği doğrulanmış yana parolanızı değiştirdiyseniz Data Lake Store hesabınızı yeniden kimlik doğrulaması gerekecektir.</span><span class="sxs-lookup"><span data-stu-id="b7da1-149">You will also need to re-authenticate your Data Lake Store account if you have changed your password since your job was created or last authenticated.</span></span> <span data-ttu-id="b7da1-150">Bu sorun belirtisi hiçbir iş çıktısı ve işlem günlükleri'ni yeniden yetkilendirme gereksinimini belirten bir hata var.</span><span class="sxs-lookup"><span data-stu-id="b7da1-150">A symptom of this issue is no job output and an error in the Operation Logs indicating need for re-authorization.</span></span>

<span data-ttu-id="b7da1-151">Bu sorunu çözmek için çalışan bir işi durdurmak ve Data Lake Store çıktısına gidin.</span><span class="sxs-lookup"><span data-stu-id="b7da1-151">To resolve this issue, stop your running job and go to your Data Lake Store output.</span></span> <span data-ttu-id="b7da1-152">"Yetkilendirmeyi yenileyin" bağlantısına tıklayın ve bir sayfa kısa bir süre için "Yeniden yönlendirmek için yetkilendirme.." belirten yukarı pop.</span><span class="sxs-lookup"><span data-stu-id="b7da1-152">Click the “Renew authorization” link, and for a brief time a page will pop up indicating “Redirecting to authorization..”.</span></span> <span data-ttu-id="b7da1-153">Sayfa otomatik olarak kapatılacak ve başarılı olursa, "Yetkilendirme başarıyla yenilendi" gösterir.</span><span class="sxs-lookup"><span data-stu-id="b7da1-153">The page will automatically close and if successful, will indicate “Authorization has been successfully renewed”.</span></span> <span data-ttu-id="b7da1-154">Sonra gerek sayfasının en altında "Kaydet"'i tıklatın ve işinizi zamandan son durduruldu veri kaybını önlemek için yeniden başlatarak devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b7da1-154">You then need to click “Save” at the bottom of the page, and can proceed by restarting your job from the Last Stopped Time to avoid data loss.</span></span>

![](media/stream-analytics-data-lake-output/stream-analytics-data-lake-output-renew-authorization.png)

