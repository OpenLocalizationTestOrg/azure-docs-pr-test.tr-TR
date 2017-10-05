---
title: "Azure Data Lake Analytics işleri için U-SQL derlemeleri geliştirme | Microsoft Docs"
description: "Kullanılan ve Data Lake Analytics işleri yeniden derlemeleri geliştirmeyi öğrenin. "
services: data-lake-analytics
documentationcenter: 
author: jejiang
manager: jhubbard
editor: cgronlun
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 11/30/2016
ms.author: jejiang
ms.openlocfilehash: c49f80f8dcd330d7f46726241e7178351b9cc28f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="develop-u-sql-assemblies-for-azure-data-lake-analytics-jobs"></a><span data-ttu-id="cffe6-103">Azure Data Lake Analytics işleri için U-SQL derlemeleri geliştirin</span><span class="sxs-lookup"><span data-stu-id="cffe6-103">Develop U-SQL assemblies for Azure Data Lake Analytics jobs</span></span>
<span data-ttu-id="cffe6-104">Arka plan kodu derlemeleri kullanılan ve Data Lake Analytics işleri yeniden dönüştürmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="cffe6-104">Learn how to turn code-behind into assemblies to be used and reused in Data Lake Analytics jobs.</span></span> 

<span data-ttu-id="cffe6-105">U-SQL C#, VB.Net veya F # gibi .net dillerinde kendi özel kod ekleme kolay hale getirir.</span><span class="sxs-lookup"><span data-stu-id="cffe6-105">U-SQL makes it easy to add your own custom code in .Net languages, such as C#, VB.Net or F#.</span></span> <span data-ttu-id="cffe6-106">Hatta diğer dilleri desteklemek için kendi çalışma zamanı dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cffe6-106">You can even deploy your own runtime to support other languages.</span></span>

<span data-ttu-id="cffe6-107">Özel kod kullanmak için en kolay yolu, Visual Studio'nun arka plan kodu özellikleri için Data Lake araçları kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="cffe6-107">The easiest way to use custom code is to use the Data Lake Tools for Visual Studio’s code-behind capabilities.</span></span> <span data-ttu-id="cffe6-108">Daha fazla bilgi için bkz: [öğretici: Visual Studio için Data Lake Araçları'nı kullanarak U-SQL betikleri geliştirme](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="cffe6-108">For more information, see [Tutorial: develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span> <span data-ttu-id="cffe6-109">Arka plan kodu kullanmanın birkaç dezavantajları vardır:</span><span class="sxs-lookup"><span data-stu-id="cffe6-109">There are a few drawbacks of using code-behind:</span></span>

- <span data-ttu-id="cffe6-110">Kaynak kodu her komut dosyası gönderi için karşıya.</span><span class="sxs-lookup"><span data-stu-id="cffe6-110">The source code gets uploaded for every script submission.</span></span>
- <span data-ttu-id="cffe6-111">arka plan kodu diğer işlemlerle paylaşılamaz.</span><span class="sxs-lookup"><span data-stu-id="cffe6-111">code-behind cannot be shared with other jobs.</span></span>

<span data-ttu-id="cffe6-112">Bu dezavantajları çözmek için arka plan kodu derlemelerine kapatma ve Data Lake Analytics Kataloğu'na derlemelerini kaydedin.</span><span class="sxs-lookup"><span data-stu-id="cffe6-112">To address these drawbacks, you can turn code-behind into assemblies, and register the assemblies to the Data Lake Analytics catalog.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cffe6-113">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="cffe6-113">Prerequisites</span></span>
* <span data-ttu-id="cffe6-114">Visual Studio 2017, Visual Studio 2015, Visual Studio 2013 4 veya Visual Studio 2012 Visual C++ yüklü güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="cffe6-114">Visual Studio 2017, Visual Studio 2015, Visual Studio 2013 update 4, or Visual Studio 2012 with Visual C++ Installed</span></span>
* <span data-ttu-id="cffe6-115">.NET sürüm 2.5 veya üzeri için Microsoft Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="cffe6-115">Microsoft Azure SDK for .NET version 2.5 or above.</span></span>  <span data-ttu-id="cffe6-116">Web Platformu yükleyicisi ya da Visual Studio Yükleyicisi'ni kullanarak yükleme</span><span class="sxs-lookup"><span data-stu-id="cffe6-116">Install it using the Web platform installer or Visual Studio Installer</span></span>
* <span data-ttu-id="cffe6-117">Bir Data Lake Analytics hesabı.</span><span class="sxs-lookup"><span data-stu-id="cffe6-117">A Data Lake Analytics account.</span></span>  <span data-ttu-id="cffe6-118">Bkz. [Azure portalını kullanarak Azure Data Lake Analytics ile çalışmaya başlama](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="cffe6-118">See [Get Started with Azure Data Lake Analytics using Azure portal](data-lake-analytics-get-started-portal.md).</span></span>
* <span data-ttu-id="cffe6-119">Git üzerinden [Azure Data Lake Analytics U-SQL Studio ile çalışmaya başlama](data-lake-analytics-u-sql-get-started.md) Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="cffe6-119">Go through the [Get started with Azure Data Lake Analytics U-SQL Studio](data-lake-analytics-u-sql-get-started.md) tutorial.</span></span>
* <span data-ttu-id="cffe6-120">Azure'a bağlayın.</span><span class="sxs-lookup"><span data-stu-id="cffe6-120">Connect to Azure.</span></span>
* <span data-ttu-id="cffe6-121">Veri kaynağını karşıya yüklemek için bkz: [Azure Data Lake Analytics U-SQL Studio ile çalışmaya başlama](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="cffe6-121">Upload the source data, see [Get started with Azure Data Lake Analytics U-SQL Studio](data-lake-analytics-u-sql-get-started.md).</span></span> 

## <a name="develop-assemblies-for-u-sql"></a><span data-ttu-id="cffe6-122">U-SQL derlemelerde geliştirin</span><span class="sxs-lookup"><span data-stu-id="cffe6-122">Develop assemblies for U-SQL</span></span>

<span data-ttu-id="cffe6-123">**Oluşturmak ve U-SQL işi göndermek için**</span><span class="sxs-lookup"><span data-stu-id="cffe6-123">**To create and submit a U-SQL job**</span></span>

1. <span data-ttu-id="cffe6-124">**Dosya** menüsünde **Yeni**'ye ve ardından **Proje**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="cffe6-124">From the **File** menu, click **New**, and then click **Project**.</span></span>
2. <span data-ttu-id="cffe6-125">Genişletme **yüklü**, **şablonları**, **Azure Data Lake**, **U-SQL(ADLA)**seçin **sınıf kitaplığı (için U-SQL Uygulama)** şablonu ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="cffe6-125">Expand **Installed**, **Templates**, **Azure Data Lake**, **U-SQL(ADLA)**, select the **Class Library (For U-SQL Application)** template, and then click **OK**.</span></span>
3. <span data-ttu-id="cffe6-126">Kodunuzu Class1.cs içinde yazın.</span><span class="sxs-lookup"><span data-stu-id="cffe6-126">Write your code in Class1.cs.</span></span>  <span data-ttu-id="cffe6-127">Kod örneği verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="cffe6-127">The following is a code sample.</span></span>

        using Microsoft.Analytics.Interfaces;

        namespace USQLApplication_codebehind
        {
            [SqlUserDefinedProcessor]
            public class MyProcessor : IProcessor
            {
                public override IRow Process(IRow input, IUpdatableRow output)
                {
                    output.Set(0, input.Get<string>(0));
                    output.Set(0, input.Get<string>(0));
                    return output.AsReadOnly();
                }
            }
        }
4. <span data-ttu-id="cffe6-128">Tıklatın **yapı** menüsüne ve ardından **yapı çözümü** dll oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="cffe6-128">Click the **Build** menu, and then click **Build Solution** to create the dll.</span></span>

## <a name="register-assemblies"></a><span data-ttu-id="cffe6-129">Derlemeleri kaydetme</span><span class="sxs-lookup"><span data-stu-id="cffe6-129">Register assemblies</span></span>

<span data-ttu-id="cffe6-130">Bkz: [kullanım Data Lake Analytics(U-SQL) katalog](data-lake-analytics-use-u-sql-catalog.md).</span><span class="sxs-lookup"><span data-stu-id="cffe6-130">See [Use Data Lake Analytics(U-SQL) catalog](data-lake-analytics-use-u-sql-catalog.md).</span></span>


## <a name="use-the-assemblies"></a><span data-ttu-id="cffe6-131">Derlemeleri kullanma</span><span class="sxs-lookup"><span data-stu-id="cffe6-131">Use the assemblies</span></span>

<span data-ttu-id="cffe6-132">Bkz: [Azure Data Lake araçları Visual Studio kodunu kullanın](data-lake-analytics-data-lake-tools-for-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="cffe6-132">See [Use the Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="cffe6-133">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="cffe6-133">See also</span></span>
* [<span data-ttu-id="cffe6-134">PowerShell kullanarak Data Lake Analytics ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="cffe6-134">Get started with Data Lake Analytics using PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="cffe6-135">Azure Portalı'nı kullanarak Data Lake Analytics ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="cffe6-135">Get started with Data Lake Analytics using the Azure portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="cffe6-136">U-SQL uygulamalarını geliştirmek için Visual Studio için Data Lake araçları kullanın</span><span class="sxs-lookup"><span data-stu-id="cffe6-136">Use Data Lake Tools for Visual Studio for developing U-SQL applications</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="cffe6-137">Kullanım Data Lake Analytics(U-SQL) Kataloğu</span><span class="sxs-lookup"><span data-stu-id="cffe6-137">Use Data Lake Analytics(U-SQL) catalog</span></span>](data-lake-analytics-use-u-sql-catalog.md)
* [<span data-ttu-id="cffe6-138">Visual Studio Code için Azure Data Lake Araçları’nı kullanma</span><span class="sxs-lookup"><span data-stu-id="cffe6-138">Use the Azure Data Lake Tools for Visual Studio Code</span></span>](data-lake-analytics-data-lake-tools-for-vscode.md)