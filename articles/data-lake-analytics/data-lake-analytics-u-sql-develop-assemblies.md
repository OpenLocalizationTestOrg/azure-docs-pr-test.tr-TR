---
title: "Azure Data Lake Analytics işleri için U-SQL aaaDevelop derlemeleri | Microsoft Docs"
description: "Nasıl toodevelop derlemeleri toobe kullanılan ve Data Lake Analytics işleri yeniden öğrenin. "
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
ms.openlocfilehash: 86dd17b25e0967306ed36bb5b7f3178d9409d53d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-u-sql-assemblies-for-azure-data-lake-analytics-jobs"></a><span data-ttu-id="c2205-103">Azure Data Lake Analytics işleri için U-SQL derlemeleri geliştirin</span><span class="sxs-lookup"><span data-stu-id="c2205-103">Develop U-SQL assemblies for Azure Data Lake Analytics jobs</span></span>
<span data-ttu-id="c2205-104">Nasıl tooturn arka plan kod içinde kullanılan ve Data Lake Analytics işleri yeniden derlemeleri toobe öğrenin.</span><span class="sxs-lookup"><span data-stu-id="c2205-104">Learn how tooturn code-behind into assemblies toobe used and reused in Data Lake Analytics jobs.</span></span> 

<span data-ttu-id="c2205-105">U-SQL, kendi özel kod kolay tooadd C#, VB.Net veya F # gibi .net dillerinde kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="c2205-105">U-SQL makes it easy tooadd your own custom code in .Net languages, such as C#, VB.Net or F#.</span></span> <span data-ttu-id="c2205-106">Bu gibi durumlarda, kendi çalışma zamanı toosupport bile diğer dillerde dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c2205-106">You can even deploy your own runtime toosupport other languages.</span></span>

<span data-ttu-id="c2205-107">Merhaba en kolay yolu toouse özel toouse hello Data Lake araçları, Visual Studio'nun arka plan kodu özellikleri kodudur.</span><span class="sxs-lookup"><span data-stu-id="c2205-107">hello easiest way toouse custom code is toouse hello Data Lake Tools for Visual Studio’s code-behind capabilities.</span></span> <span data-ttu-id="c2205-108">Daha fazla bilgi için bkz: [öğretici: Visual Studio için Data Lake Araçları'nı kullanarak U-SQL betikleri geliştirme](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c2205-108">For more information, see [Tutorial: develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span> <span data-ttu-id="c2205-109">Arka plan kodu kullanmanın birkaç dezavantajları vardır:</span><span class="sxs-lookup"><span data-stu-id="c2205-109">There are a few drawbacks of using code-behind:</span></span>

- <span data-ttu-id="c2205-110">Merhaba kaynak kodu her komut dosyası gönderi için karşıya.</span><span class="sxs-lookup"><span data-stu-id="c2205-110">hello source code gets uploaded for every script submission.</span></span>
- <span data-ttu-id="c2205-111">arka plan kodu diğer işlemlerle paylaşılamaz.</span><span class="sxs-lookup"><span data-stu-id="c2205-111">code-behind cannot be shared with other jobs.</span></span>

<span data-ttu-id="c2205-112">tooaddress bu dezavantajları arka plan kodu derlemelerine açmak ve hello derlemeleri toohello Data Lake Analytics Kataloğu kaydedin.</span><span class="sxs-lookup"><span data-stu-id="c2205-112">tooaddress these drawbacks, you can turn code-behind into assemblies, and register hello assemblies toohello Data Lake Analytics catalog.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c2205-113">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="c2205-113">Prerequisites</span></span>
* <span data-ttu-id="c2205-114">Visual Studio 2017, Visual Studio 2015, Visual Studio 2013 4 veya Visual Studio 2012 Visual C++ yüklü güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="c2205-114">Visual Studio 2017, Visual Studio 2015, Visual Studio 2013 update 4, or Visual Studio 2012 with Visual C++ Installed</span></span>
* <span data-ttu-id="c2205-115">.NET sürüm 2.5 veya üzeri için Microsoft Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="c2205-115">Microsoft Azure SDK for .NET version 2.5 or above.</span></span>  <span data-ttu-id="c2205-116">Merhaba Web Platformu yükleyicisi veya Visual Studio Yükleyicisi'ni kullanarak yükleme</span><span class="sxs-lookup"><span data-stu-id="c2205-116">Install it using hello Web platform installer or Visual Studio Installer</span></span>
* <span data-ttu-id="c2205-117">Bir Data Lake Analytics hesabı.</span><span class="sxs-lookup"><span data-stu-id="c2205-117">A Data Lake Analytics account.</span></span>  <span data-ttu-id="c2205-118">Bkz. [Azure portalını kullanarak Azure Data Lake Analytics ile çalışmaya başlama](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c2205-118">See [Get Started with Azure Data Lake Analytics using Azure portal](data-lake-analytics-get-started-portal.md).</span></span>
* <span data-ttu-id="c2205-119">Merhaba aracılığıyla gidin [Azure Data Lake Analytics U-SQL Studio ile çalışmaya başlama](data-lake-analytics-u-sql-get-started.md) Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="c2205-119">Go through hello [Get started with Azure Data Lake Analytics U-SQL Studio](data-lake-analytics-u-sql-get-started.md) tutorial.</span></span>
* <span data-ttu-id="c2205-120">TooAzure bağlanın.</span><span class="sxs-lookup"><span data-stu-id="c2205-120">Connect tooAzure.</span></span>
* <span data-ttu-id="c2205-121">Merhaba kaynak verileri yüklemek için bkz: [Azure Data Lake Analytics U-SQL Studio ile çalışmaya başlama](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c2205-121">Upload hello source data, see [Get started with Azure Data Lake Analytics U-SQL Studio](data-lake-analytics-u-sql-get-started.md).</span></span> 

## <a name="develop-assemblies-for-u-sql"></a><span data-ttu-id="c2205-122">U-SQL derlemelerde geliştirin</span><span class="sxs-lookup"><span data-stu-id="c2205-122">Develop assemblies for U-SQL</span></span>

<span data-ttu-id="c2205-123">**toocreate ve U-SQL işi gönderin**</span><span class="sxs-lookup"><span data-stu-id="c2205-123">**toocreate and submit a U-SQL job**</span></span>

1. <span data-ttu-id="c2205-124">Merhaba gelen **dosya** menüsünde tıklatın **yeni**ve ardından **proje**.</span><span class="sxs-lookup"><span data-stu-id="c2205-124">From hello **File** menu, click **New**, and then click **Project**.</span></span>
2. <span data-ttu-id="c2205-125">Genişletme **yüklü**, **şablonları**, **Azure Data Lake**, **U-SQL(ADLA)**seçin hello **sınıf kitaplığı (için U-SQL Uygulama)** şablonu ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="c2205-125">Expand **Installed**, **Templates**, **Azure Data Lake**, **U-SQL(ADLA)**, select hello **Class Library (For U-SQL Application)** template, and then click **OK**.</span></span>
3. <span data-ttu-id="c2205-126">Kodunuzu Class1.cs içinde yazın.</span><span class="sxs-lookup"><span data-stu-id="c2205-126">Write your code in Class1.cs.</span></span>  <span data-ttu-id="c2205-127">Merhaba, bir kod örneği verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="c2205-127">hello following is a code sample.</span></span>

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
4. <span data-ttu-id="c2205-128">Merhaba tıklatın **yapı** menüsüne ve ardından **yapı çözümü** toocreate hello dll.</span><span class="sxs-lookup"><span data-stu-id="c2205-128">Click hello **Build** menu, and then click **Build Solution** toocreate hello dll.</span></span>

## <a name="register-assemblies"></a><span data-ttu-id="c2205-129">Derlemeleri kaydetme</span><span class="sxs-lookup"><span data-stu-id="c2205-129">Register assemblies</span></span>

<span data-ttu-id="c2205-130">Bkz: [kullanım Data Lake Analytics(U-SQL) katalog](data-lake-analytics-use-u-sql-catalog.md).</span><span class="sxs-lookup"><span data-stu-id="c2205-130">See [Use Data Lake Analytics(U-SQL) catalog](data-lake-analytics-use-u-sql-catalog.md).</span></span>


## <a name="use-hello-assemblies"></a><span data-ttu-id="c2205-131">Merhaba derlemeleri kullanma</span><span class="sxs-lookup"><span data-stu-id="c2205-131">Use hello assemblies</span></span>

<span data-ttu-id="c2205-132">Bkz: [hello Azure Data Lake araçları kullanmak için Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="c2205-132">See [Use hello Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="c2205-133">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="c2205-133">See also</span></span>
* [<span data-ttu-id="c2205-134">PowerShell kullanarak Data Lake Analytics ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="c2205-134">Get started with Data Lake Analytics using PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="c2205-135">Hello Azure portal kullanarak Data Lake Analytics ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="c2205-135">Get started with Data Lake Analytics using hello Azure portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="c2205-136">U-SQL uygulamalarını geliştirmek için Visual Studio için Data Lake araçları kullanın</span><span class="sxs-lookup"><span data-stu-id="c2205-136">Use Data Lake Tools for Visual Studio for developing U-SQL applications</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="c2205-137">Kullanım Data Lake Analytics(U-SQL) Kataloğu</span><span class="sxs-lookup"><span data-stu-id="c2205-137">Use Data Lake Analytics(U-SQL) catalog</span></span>](data-lake-analytics-use-u-sql-catalog.md)
* [<span data-ttu-id="c2205-138">Hello Azure Data Lake araçları Visual Studio kodunu kullanın</span><span class="sxs-lookup"><span data-stu-id="c2205-138">Use hello Azure Data Lake Tools for Visual Studio Code</span></span>](data-lake-analytics-data-lake-tools-for-vscode.md)
