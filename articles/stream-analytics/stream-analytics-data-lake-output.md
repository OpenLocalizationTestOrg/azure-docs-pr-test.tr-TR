---
title: "aaaStream Analytics veri Gölü deposu çıkış | Microsoft Docs"
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
ms.openlocfilehash: 183cf51edb2e49ac3e42257e67a8077b95777258
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="stream-analytics-data-lake-store-output"></a><span data-ttu-id="935b0-103">Stream Analytics Data Lake Store çıktı</span><span class="sxs-lookup"><span data-stu-id="935b0-103">Stream Analytics Data Lake Store output</span></span>
<span data-ttu-id="935b0-104">Akış analizi işleri birkaç çıktı yöntemlerini destekleyen bir anda bir [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/).</span><span class="sxs-lookup"><span data-stu-id="935b0-104">Stream Analytics jobs support several output methods, one being an [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/).</span></span> <span data-ttu-id="935b0-105">Azure Data Lake Store, büyük veri analitik iş yükleri için kuruluş çapında hiper ölçekli bir depodur.</span><span class="sxs-lookup"><span data-stu-id="935b0-105">Azure Data Lake Store is an enterprise-wide hyper-scale repository for big data analytic workloads.</span></span> <span data-ttu-id="935b0-106">Data Lake Store işletimsel ve keşifsel analiz herhangi boyutu, türü ve alım hızına toostore veri sağlar.</span><span class="sxs-lookup"><span data-stu-id="935b0-106">Data Lake Store enables you toostore data of any size, type and ingestion speed for operational and exploratory analytics.</span></span>

## <a name="authorize-a-data-lake-store-account"></a><span data-ttu-id="935b0-107">Bir Data Lake Store hesabı yetki</span><span class="sxs-lookup"><span data-stu-id="935b0-107">Authorize a Data Lake Store account</span></span>
1. <span data-ttu-id="935b0-108">Data Lake Store'hello Azure portalında bir çıkış olarak seçildiğinde istenir varolan Data Lake Store veya toorequest tooauthorize kullanımı toohello Data Lake Store'a hello Klasik Portal üzerinden erişim.</span><span class="sxs-lookup"><span data-stu-id="935b0-108">When Data Lake Store is selected as an output in hello Azure portal, you will be prompted tooauthorize use of your existing Data Lake Store or toorequest access toohello Data Lake Store via hello Classic Portal.</span></span>
   
   ![](media/stream-analytics-data-lake-output/stream-analytics-data-lake-output-authorization.png)  
   
2. <span data-ttu-id="935b0-109">Zaten varsa tooData Lake Store'a erişmek, "Şimdi Yetkilendir"'i tıklatın ve bir sayfa kısa bir süre için pop "Yeniden yönlendirmek tooauthorization" belirten ayarlama.</span><span class="sxs-lookup"><span data-stu-id="935b0-109">If you already have access tooData Lake Store, click “Authorize Now” and for a brief time a page will pop up indicating “Redirecting tooauthorization”.</span></span> <span data-ttu-id="935b0-110">Başlangıç sayfası otomatik olarak kapanır ve tooconfigure hello Data Lake Store çıkış belirleyebilmesini hello sayfasıyla sunulur.</span><span class="sxs-lookup"><span data-stu-id="935b0-110">hello page will automatically close and you will be presented with hello page that would allow you tooconfigure hello Data Lake Store output.</span></span>

<span data-ttu-id="935b0-111">Data Lake Store için kaydolmadıysanız, hello "şimdi kaydolun" bağlantı tooinitiate hello isteği izleyin, veya hello izleyin [başlatılan yönergeleri almak](../data-lake-store/data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="935b0-111">If you have not signed up for Data Lake Store, you can follow hello “Sign up now” link tooinitiate hello request, or follow hello [get started instructions](../data-lake-store/data-lake-store-get-started-portal.md).</span></span>

## <a name="configure-hello-data-lake-store-output-properties"></a><span data-ttu-id="935b0-112">Merhaba Data Lake Store çıktı özelliklerini yapılandırın</span><span class="sxs-lookup"><span data-stu-id="935b0-112">Configure hello Data Lake Store output properties</span></span>
<span data-ttu-id="935b0-113">Kimliği doğrulanmış hello Data Lake Store hesabına sahip olduğunda, Data Lake Store çıktı için hello özelliklerini yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="935b0-113">Once you have hello Data Lake Store account authenticated, you can configure hello properties for your Data Lake Store output.</span></span> <span data-ttu-id="935b0-114">Merhaba tabloda hello özellik adları ve Data Lake Store çıktı kendi açıklama tooconfigure listesidir.</span><span class="sxs-lookup"><span data-stu-id="935b0-114">hello table below is hello list of property names and their description tooconfigure your Data Lake Store output.</span></span>

<table>
<tbody>
<tr>
<td><span data-ttu-id="935b0-115"><B>ÖZELLİK ADI</B></span><span class="sxs-lookup"><span data-stu-id="935b0-115"><B>PROPERTY NAME</B></span></span></td>
<td><span data-ttu-id="935b0-116"><B>AÇIKLAMA</B></span><span class="sxs-lookup"><span data-stu-id="935b0-116"><B>DESCRIPTION</B></span></span></td>
</tr>
<tr>
<td><span data-ttu-id="935b0-117">Çıkış diğer adları</span><span class="sxs-lookup"><span data-stu-id="935b0-117">Output Alias</span></span></td>
<td><span data-ttu-id="935b0-118">Bu sorguları toodirect hello sorgu çıktı toothis Data Lake Store kullanılan kolay bir addır.</span><span class="sxs-lookup"><span data-stu-id="935b0-118">This is a friendly name used in queries toodirect hello query output toothis Data Lake Store.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="935b0-119">Data Lake Store hesabı</span><span class="sxs-lookup"><span data-stu-id="935b0-119">Data Lake Store Account</span></span></td>
<td><span data-ttu-id="935b0-120">Burada, Çıkış göndermeyi hello depolama hesabı Hello adı.</span><span class="sxs-lookup"><span data-stu-id="935b0-120">hello name of hello storage account where you are sending your output.</span></span> <span data-ttu-id="935b0-121">Kullanıcı oturum hello erişimi Data Lake Store hesapları listesiyle birlikte sunulur.</span><span class="sxs-lookup"><span data-stu-id="935b0-121">You will be presented with a list of Data Lake Store accounts  hello logged in user has access to.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="935b0-122">Yol önek deseni [<I>isteğe bağlı</I>]</span><span class="sxs-lookup"><span data-stu-id="935b0-122">Path Prefix Pattern [<I>optional</I>]</span></span></td>
<td><span data-ttu-id="935b0-123">dosya yolu kullanılan toowrite hello dosyalarınızı hello içinde belirtilen Data Lake Store hesabı.</span><span class="sxs-lookup"><span data-stu-id="935b0-123">hello file path used toowrite your files within hello specified Data Lake Store Account.</span></span> <BR><span data-ttu-id="935b0-124">{date} {time}</span><span class="sxs-lookup"><span data-stu-id="935b0-124">{date}, {time}</span></span><BR><span data-ttu-id="935b0-125">Örnek 1: klasör1/logs / {date} / {time}</span><span class="sxs-lookup"><span data-stu-id="935b0-125">Example 1: folder1/logs/{date}/{time}</span></span><BR><span data-ttu-id="935b0-126">Örnek 2: klasör1/logs / {date}</span><span class="sxs-lookup"><span data-stu-id="935b0-126">Example 2: folder1/logs/{date}</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="935b0-127">Tarih biçimi [<I>isteğe bağlı</I>]</span><span class="sxs-lookup"><span data-stu-id="935b0-127">Date Format [<I>optional</I>]</span></span></td>
<td><span data-ttu-id="935b0-128">Merhaba bir tarih belirteci hello önek yolunda kullanılırsa, dosyalarınızı organize edilmiştir hello tarih biçimi seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="935b0-128">If hello date token is used in hello prefix path, you can select hello date format in which your files are organized.</span></span> <span data-ttu-id="935b0-129">Örnek: YYYY/AA/GG</span><span class="sxs-lookup"><span data-stu-id="935b0-129">Example: YYYY/MM/DD</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="935b0-130">Saat biçimi [<I>isteğe bağlı</I>]</span><span class="sxs-lookup"><span data-stu-id="935b0-130">Time Format [<I>optional</I>]</span></span></td>
<td><span data-ttu-id="935b0-131">Merhaba zaman belirteci hello önek yolunda kullanılırsa, dosyalarınızı organize edilmiştir hello saat biçimini belirtin.</span><span class="sxs-lookup"><span data-stu-id="935b0-131">If hello time token is used in hello prefix path, specify hello time format in which your files are organized.</span></span> <span data-ttu-id="935b0-132">Şu anda HH yalnızca desteklenen hello değerdir.</span><span class="sxs-lookup"><span data-stu-id="935b0-132">Currently hello only supported value is HH.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="935b0-133">Olayı seri hale getirme biçimi</span><span class="sxs-lookup"><span data-stu-id="935b0-133">Event Serialization Format</span></span></td>
<td><span data-ttu-id="935b0-134">Çıkış verileri seri hale getirme biçimi.</span><span class="sxs-lookup"><span data-stu-id="935b0-134">Serialization format for output data.</span></span> <span data-ttu-id="935b0-135">JSON, CSV ve Avro desteklenir.</span><span class="sxs-lookup"><span data-stu-id="935b0-135">JSON, CSV, and Avro are supported.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="935b0-136">Encoding</span><span class="sxs-lookup"><span data-stu-id="935b0-136">Encoding</span></span></td>
<td><span data-ttu-id="935b0-137">Bir kodlama, CSV veya JSON biçiminde, belirtilmiş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="935b0-137">If CSV or JSON format, an encoding must be specified.</span></span> <span data-ttu-id="935b0-138">UTF-8 hello kodlama biçimi şu anda yalnızca desteklenir. ' dir.</span><span class="sxs-lookup"><span data-stu-id="935b0-138">UTF-8 is hello only supported encoding format at this time.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="935b0-139">sınırlayıcı</span><span class="sxs-lookup"><span data-stu-id="935b0-139">Delimiter</span></span></td>
<td><span data-ttu-id="935b0-140">Yalnızca, CSV serileştirme için de geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="935b0-140">Only applicable for CSV serialization.</span></span> <span data-ttu-id="935b0-141">Akış analizi, CSV verileri seri hale getirme için bir dizi ortak sınırlayıcıları destekler.</span><span class="sxs-lookup"><span data-stu-id="935b0-141">Stream Analytics supports a number of common delimiters for serializing CSV data.</span></span> <span data-ttu-id="935b0-142">Virgül, noktalı virgül, boşluk, sekme ve dikey çubuk bunun desteklenen değerlerdir.</span><span class="sxs-lookup"><span data-stu-id="935b0-142">Supported values are comma, semicolon, space, tab and vertical bar.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="935b0-143">Biçimi</span><span class="sxs-lookup"><span data-stu-id="935b0-143">Format</span></span></td>
<td><span data-ttu-id="935b0-144">Yalnızca JSON serileştirmesi için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="935b0-144">Only applicable for JSON serialization.</span></span> <span data-ttu-id="935b0-145">Ayrılmış çizgi hello çıkış sahip yeni bir çizgiyle ayrılmış her bir JSON nesnesi olarak biçimlendirileceğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="935b0-145">Line separated specifies that hello output will be formatted by having each JSON object separated by a new line.</span></span> <span data-ttu-id="935b0-146">Dizi hello çıktı bir dizi JSON nesnesi biçimlendirileceğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="935b0-146">Array specifies that hello output will be formatted as an array of JSON objects.</span></span></td>
</tr>
</tbody>
</table>

## <a name="renew-data-lake-store-authorization"></a><span data-ttu-id="935b0-147">Data Lake Store yetkilendirmeyi yenileyin</span><span class="sxs-lookup"><span data-stu-id="935b0-147">Renew Data Lake Store Authorization</span></span>
<span data-ttu-id="935b0-148">Şu anda, burada hello kimlik doğrulama belirteci el ile 90 günde Data Lake Store çıktıyla tüm işleri yenilenir toobe gereken bir sınırlama yoktur.</span><span class="sxs-lookup"><span data-stu-id="935b0-148">Currently, there is a limitation where hello authentication token needs toobe manually refreshed every 90 days for all jobs with Data Lake Store output.</span></span> <span data-ttu-id="935b0-149">Toore de gerekir-işinizi oluşturulmuş veya son kimliği doğrulanmış yana parolanızı değiştirdiyseniz Data Lake Store hesabınızın kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="935b0-149">You will also need toore-authenticate your Data Lake Store account if you have changed your password since your job was created or last authenticated.</span></span> <span data-ttu-id="935b0-150">Bu sorun belirtisi hiçbir iş çıktısı ve hello işlem günlükleri'ni yeniden yetkilendirme gereksinimini belirten bir hata var.</span><span class="sxs-lookup"><span data-stu-id="935b0-150">A symptom of this issue is no job output and an error in hello Operation Logs indicating need for re-authorization.</span></span>

<span data-ttu-id="935b0-151">tooresolve Bu sorun, çalışan bir işi durdurmak ve tooyour Data Lake Store çıktı gidin.</span><span class="sxs-lookup"><span data-stu-id="935b0-151">tooresolve this issue, stop your running job and go tooyour Data Lake Store output.</span></span> <span data-ttu-id="935b0-152">Merhaba "Yenileme yetkilendirme" bağlantısına tıklayın ve bir sayfa kısa bir süre için "Yeniden yönlendirmek tooauthorization.." belirten yukarı pop.</span><span class="sxs-lookup"><span data-stu-id="935b0-152">Click hello “Renew authorization” link, and for a brief time a page will pop up indicating “Redirecting tooauthorization..”.</span></span> <span data-ttu-id="935b0-153">Başlangıç sayfası otomatik olarak kapatılacak ve başarılı olursa, "Yetkilendirme başarıyla yenilendi" gösterir.</span><span class="sxs-lookup"><span data-stu-id="935b0-153">hello page will automatically close and if successful, will indicate “Authorization has been successfully renewed”.</span></span> <span data-ttu-id="935b0-154">Ardından tooclick "Kaydet" Merhaba hello sayfa sonunda ve gerekir, hello son durdurulma zamanı tooavoid veri kaybı işten başlatarak devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="935b0-154">You then need tooclick “Save” at hello bottom of hello page, and can proceed by restarting your job from hello Last Stopped Time tooavoid data loss.</span></span>

![](media/stream-analytics-data-lake-output/stream-analytics-data-lake-output-renew-authorization.png)

