---
title: "U-SQL işleri hata ayıklama | Microsoft Docs"
description: "Visual Studio kullanarak bir U-SQL başarısız köşe hata ayıklama öğrenin."
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: jhubbard
editor: cgronlun
ms.assetid: bcd0b01e-1755-4112-8e8a-a5cabdca4df2
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 09/02/2016
ms.author: saveenr
ms.openlocfilehash: 2a77c72d3062272305208934d6406d040266c753
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="debug-user-defined-c-code-for-failed-u-sql-jobs"></a><span data-ttu-id="dec11-103">Hata ayıklama başarısız U-SQL işleri için kullanıcı tanımlı C# kodu</span><span class="sxs-lookup"><span data-stu-id="dec11-103">Debug user-defined C# code for failed U-SQL jobs</span></span>

<span data-ttu-id="dec11-104">U-SQL kullanarak bir özel ayıklayıcısı veya reducer gibi işlevsellikler eklemek için kodunuzu yazabilirsiniz şekilde C# ' ta, genişletilebilirlik modeli sağlar.</span><span class="sxs-lookup"><span data-stu-id="dec11-104">U-SQL provides an extensibility model using C#, so you can write your code to add functionality such as a custom extractor or reducer.</span></span> <span data-ttu-id="dec11-105">Daha fazla bilgi için bkz: [U-SQL Programlama Kılavuzu](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-u-sql-programmability-guide#use-user-defined-functions-udf).</span><span class="sxs-lookup"><span data-stu-id="dec11-105">To learn more, see [U-SQL programmability guide](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-u-sql-programmability-guide#use-user-defined-functions-udf).</span></span> <span data-ttu-id="dec11-106">Uygulamada hata ayıklama herhangi bir kod gerekebilir ve büyük veri sistemlerini yalnızca sınırlı çalışma zamanı hata ayıklama günlük dosyaları gibi bilgileri sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="dec11-106">In practice any code may need debugging, and big data systems may only provide limited runtime debugging information such as log files.</span></span>

<span data-ttu-id="dec11-107">Visual Studio için Azure Data Lake araçları adlı bir özelliği sağlar **köşe hata ayıklama başarısız**, olanak sağlayan, bulutta başarısız bir işi hata ayıklama için yerel makinenize klonlayın.</span><span class="sxs-lookup"><span data-stu-id="dec11-107">Azure Data Lake Tools for Visual Studio provides a feature called **Failed Vertex Debug**, which lets you clone a failed job from the cloud to your local machine for debugging.</span></span> <span data-ttu-id="dec11-108">Yerel kopya herhangi bir giriş veri ve kullanıcı kodu da dahil olmak üzere tüm bulut ortamı yakalar.</span><span class="sxs-lookup"><span data-stu-id="dec11-108">The local clone captures the entire cloud environment, including any input data and user code.</span></span>

<span data-ttu-id="dec11-109">Aşağıdaki videoda Visual Studio için Azure Data Lake araçları Debug başarısız köşe gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="dec11-109">The following video demonstrates Failed Vertex Debug in Azure Data Lake Tools for Visual Studio.</span></span>

> [!VIDEO https://e0d1.wpc.azureedge.net/80E0D1/OfficeMixProdMediaBlobStorage/asset-d3aeab42-6149-4ecc-b044-aa624901ab32/b0fc0373c8f94f1bb8cd39da1310adb8.mp4?sv=2012-02-12&sr=c&si=a91fad76-cfdd-4513-9668-483de39e739c&sig=K%2FR%2FdnIi9S6P%2FBlB3iLAEV5pYu6OJFBDlQy%2FQtZ7E7M%3D&se=2116-07-19T09:27:30Z&rscd=attachment%3B%20filename%3DDebugyourcustomcodeinUSQLADLA.mp4]
>

> [!NOTE]
> <span data-ttu-id="dec11-110">Visual Studio zaten yüklü değilse aşağıdaki iki güncelleştirmelerden gerektirir: [Microsoft Visual C++ 2015 Redistributable güncelleştirme 3](https://www.microsoft.com/en-us/download/details.aspx?id=53840) ve [Evrensel C çalışma zamanı için Windows](https://www.microsoft.com/download/details.aspx?id=50410).</span><span class="sxs-lookup"><span data-stu-id="dec11-110">Visual Studio requires the following two updates, if they are not already installed: [Microsoft Visual C++ 2015 Redistributable Update 3](https://www.microsoft.com/en-us/download/details.aspx?id=53840) and the [Universal C Runtime for Windows](https://www.microsoft.com/download/details.aspx?id=50410).</span></span>

## <a name="download-failed-vertex-to-local-machine"></a><span data-ttu-id="dec11-111">Yerel makineye yükleme başarısız köşe</span><span class="sxs-lookup"><span data-stu-id="dec11-111">Download failed vertex to local machine</span></span>

<span data-ttu-id="dec11-112">Visual Studio için Azure Data Lake araçları başarısız bir işi açtığınızda, sarı bir uyarı çubuğu için hata sekmesini ayrıntılı hata iletileri ile bakın.</span><span class="sxs-lookup"><span data-stu-id="dec11-112">When you open a failed job in Azure Data Lake Tools for Visual Studio, you see a yellow alert bar with detailed error messages in the error tab.</span></span>

1. <span data-ttu-id="dec11-113">Tıklatın **karşıdan** tüm gerekli kaynakları ve giriş akışları karşıdan yüklemek için.</span><span class="sxs-lookup"><span data-stu-id="dec11-113">Click **Download** to download all the required resources and input streams.</span></span> <span data-ttu-id="dec11-114">Karşıdan yükleme tamamlanmazsa, tıklatın **yeniden**.</span><span class="sxs-lookup"><span data-stu-id="dec11-114">If the download doesn't complete, click **Retry**.</span></span>

2. <span data-ttu-id="dec11-115">Tıklatın **açık** yerel hata ayıklama ortamı oluşturmak için indirme tamamlandıktan sonra.</span><span class="sxs-lookup"><span data-stu-id="dec11-115">Click **Open** after the download completes to generate a local debugging environment.</span></span> <span data-ttu-id="dec11-116">Hata ayıklama çözümü olan yeni bir Visual Studio örneği otomatik olarak oluşturulan ve açılır.</span><span class="sxs-lookup"><span data-stu-id="dec11-116">A new Visual Studio instance with a debugging solution is automatically created and opened.</span></span>

![Azure Data Lake Analytics U-SQL hata ayıklama visual studio indirme köşe](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-download-vertex.png)

<span data-ttu-id="dec11-118">İşlerini arka plan kodu kaynak dosyaları veya kayıtlı derlemeler içerebilir ve bu iki türlerinin farklı hata ayıklama senaryolar vardır.</span><span class="sxs-lookup"><span data-stu-id="dec11-118">Jobs may include code-behind source files or registered assemblies, and these two types have different debugging scenarios.</span></span>

- [<span data-ttu-id="dec11-119">Arka plan kodu ile başarısız bir işi hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="dec11-119">Debug a failed job with code-behind</span></span>](#debug-job-failed-with-code-behind)
- [<span data-ttu-id="dec11-120">Başarısız bir işi derlemeleri ile hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="dec11-120">Debug a failed job with assemblies</span></span>](#debug-job-failed-with-assemblies)


## <a name="debug-job-failed-with-code-behind"></a><span data-ttu-id="dec11-121">Hata ayıklama işi arka plan kodu ile başarısız oldu</span><span class="sxs-lookup"><span data-stu-id="dec11-121">Debug job failed with code-behind</span></span>

<span data-ttu-id="dec11-122">U-SQL işi başarısız oluyor ve iş kullanıcı kodu içeriyorsa (genellikle adlı `Script.usql.cs` U-SQL projesinde), kaynak kodu hata ayıklama çözüm içine alınır.</span><span class="sxs-lookup"><span data-stu-id="dec11-122">If a U-SQL job fails, and the job includes user code (typically named `Script.usql.cs` in a U-SQL project), that source code is imported into the debugging solution.</span></span>  <span data-ttu-id="dec11-123">Buradan, Visual Studio hata ayıklama araçları (izleme, değişkenleri, vb.) sorunu gidermek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dec11-123">From there you can use the Visual Studio debugging tools (watch, variables, etc.) to troubleshoot the problem.</span></span>

> [!NOTE]
> <span data-ttu-id="dec11-124">Hata ayıklama önce kontrol ettiğinizden emin olun **ortak dil çalışma zamanı özel durumları** özel ayarları penceresinde (**Ctrl + Alt + E**).</span><span class="sxs-lookup"><span data-stu-id="dec11-124">Before debugging, be sure to check **Common Language Runtime Exceptions** in the Exception Settings window (**Ctrl + Alt + E**).</span></span>

![Azure Data Lake Analytics U-SQL hata ayıklama visual studio ayarı](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-clr-exception-setting.png)

1. <span data-ttu-id="dec11-126">Tuşuna **F5** arka plan kodu kodu çalıştırmak için.</span><span class="sxs-lookup"><span data-stu-id="dec11-126">Press **F5** to run the code-behind code.</span></span> <span data-ttu-id="dec11-127">Bir özel durum tarafından durduruluncaya kadar çalışmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="dec11-127">It will run until it is stopped by an exception.</span></span>

2. <span data-ttu-id="dec11-128">Açık `ADLTool_Codebehind.usql.cs` dosya ve kesme, tuşuna basarak **F5** adım adım kodun hatalarını ayıklamak için.</span><span class="sxs-lookup"><span data-stu-id="dec11-128">Open the `ADLTool_Codebehind.usql.cs` file and set breakpoints, then press **F5** to debug the code step by step.</span></span>

    ![Azure Data Lake Analytics U-SQL hata ayıklama özel durumu](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-debug-exception.png)

## <a name="debug-job-failed-with-assemblies"></a><span data-ttu-id="dec11-130">Hata ayıklama işi derlemeleri ile başarısız oldu</span><span class="sxs-lookup"><span data-stu-id="dec11-130">Debug job failed with assemblies</span></span>

<span data-ttu-id="dec11-131">U-SQL komut dosyanıza kayıtlı derlemeleri kullanırsanız, sistem kaynak kodu otomatik olarak alınamıyor.</span><span class="sxs-lookup"><span data-stu-id="dec11-131">If you use registered assemblies in your U-SQL script, the system can't get the source code automatically.</span></span> <span data-ttu-id="dec11-132">Bu durumda, el ile derlemeleri kaynak kodu dosyaları çözüme ekleyin.</span><span class="sxs-lookup"><span data-stu-id="dec11-132">In this case, manually add the assemblies' source code files to the solution.</span></span>

### <a name="configure-the-solution"></a><span data-ttu-id="dec11-133">Çözümünüzü yapılandırma</span><span class="sxs-lookup"><span data-stu-id="dec11-133">Configure the solution</span></span>

1. <span data-ttu-id="dec11-134">Sağ **çözüm 'VertexDebug' > Ekle > mevcut proje...**  derlemeler kaynak kodu bulun ve hata ayıklama çözüme proje ekleyin.</span><span class="sxs-lookup"><span data-stu-id="dec11-134">Right-click **Solution 'VertexDebug' > Add > Existing Project...** to find the assemblies' source code and add the project to the debugging solution.</span></span>

    ![Azure Data Lake Analytics U-SQL hata ayıklama proje ekleyin](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-add-project-to-debug-solution.png)

2. <span data-ttu-id="dec11-136">Sağ **LocalVertexHost > Özellikler** çözüm kopyalayıp **çalışma dizini** yolu.</span><span class="sxs-lookup"><span data-stu-id="dec11-136">Right-click **LocalVertexHost > Properties** in the solution and copy the **Working Directory** path.</span></span>

3. <span data-ttu-id="dec11-137">Sağ **derleme kaynak kod projesi > Özellikleri**seçin **yapı** sekmesinde solda ve kopyalanan yolu olarak Yapıştır **çıkış > çıkış yolu**.</span><span class="sxs-lookup"><span data-stu-id="dec11-137">Right-Click **assembly source code project > Properties**, select the **Build** tab at left, and paste the copied path as **Output > Output path**.</span></span>

    ![Azure Data Lake Analytics U-SQL hata ayıklama pdb yolunu ayarlama](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-set-pdb-path.png)

4. <span data-ttu-id="dec11-139">Tuşuna **Ctrl + Alt + E**, denetleme **ortak dil çalışma zamanı özel durumları** özel ayarları penceresinde.</span><span class="sxs-lookup"><span data-stu-id="dec11-139">Press **Ctrl + Alt + E**, check **Common Language Runtime Exceptions** in Exception Settings window.</span></span>

### <a name="start-debug"></a><span data-ttu-id="dec11-140">Hata ayıklama Başlat</span><span class="sxs-lookup"><span data-stu-id="dec11-140">Start debug</span></span>

1. <span data-ttu-id="dec11-141">Sağ **derleme kaynak kod projesi > yeniden** çıkış .pdb dosyaları için `LocalVertexHost` çalışma dizini.</span><span class="sxs-lookup"><span data-stu-id="dec11-141">Right-click **assembly source code project > Rebuild** to output .pdb files to the `LocalVertexHost` working directory.</span></span>

2. <span data-ttu-id="dec11-142">Tuşuna **F5** ve bir özel durum tarafından durduruluncaya kadar proje çalışır.</span><span class="sxs-lookup"><span data-stu-id="dec11-142">Press **F5** and the project will run until it is stopped by an exception.</span></span> <span data-ttu-id="dec11-143">Güvenle yok sayabilirsiniz aşağıdaki uyarı iletisi görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dec11-143">You may see the following warning message, which you can safely ignore.</span></span> <span data-ttu-id="dec11-144">Bu işlem birkaç dakika hata ayıklama ekranı için kadar sürebilir.</span><span class="sxs-lookup"><span data-stu-id="dec11-144">It can take up to a minute to get to the debug screen.</span></span>

    ![Azure Data Lake Analytics U-SQL hata ayıklama visual studio uyarı](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-visual-studio-u-sql-debug-warning.png)

3. <span data-ttu-id="dec11-146">Kaynak kodunuz açın ve kesme, tuşuna basarak **F5** adım adım kodun hatalarını ayıklamak için.</span><span class="sxs-lookup"><span data-stu-id="dec11-146">Open your source code and set breakpoints, then press **F5** to debug the code step by step.</span></span>

<span data-ttu-id="dec11-147">Visual Studio hata ayıklama araçları (izleme, değişkenleri, vb.) sorunu gidermek için de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dec11-147">You can also use the Visual Studio debugging tools (watch, variables, etc.) to troubleshoot the problem.</span></span>

> [!NOTE]
> <span data-ttu-id="dec11-148">Derleme kaynak kodunu projeyi güncelleştirilmiş .pdb dosyaları oluşturmak için kodu değiştirdikten sonra her zaman yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="dec11-148">Rebuild the assembly source code project each time after you modify the code to generate updated .pdb files.</span></span>

<span data-ttu-id="dec11-149">Proje başarıyla tamamlarsa hata ayıklama sonra çıktı penceresinde aşağıdaki iletiyi gösterir:</span><span class="sxs-lookup"><span data-stu-id="dec11-149">After debugging, if the project completes successfully the output window shows the following message:</span></span>

```
The Program 'LocalVertexHost.exe' has exited with code 0 (0x0).
```

![Azure Data Lake Analytics U-SQL hata ayıklama başarılı](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-debug-succeed.png)

## <a name="resubmit-the-job"></a><span data-ttu-id="dec11-151">İş yeniden gönderin</span><span class="sxs-lookup"><span data-stu-id="dec11-151">Resubmit the job</span></span>

<span data-ttu-id="dec11-152">Hata ayıklama tamamladıktan sonra başarısız işi yeniden gönderin.</span><span class="sxs-lookup"><span data-stu-id="dec11-152">Once you have completed debugging, resubmit the failed job.</span></span>

1. <span data-ttu-id="dec11-153">Arka plan kodu çözümleriyle işleri için C# kodu arka plan kodu kaynak dosyaya kopyalayın (genellikle `Script.usql.cs`).</span><span class="sxs-lookup"><span data-stu-id="dec11-153">For jobs with code-behind solutions, copy your C# code into the code-behind source file (typically `Script.usql.cs`).</span></span>
2. <span data-ttu-id="dec11-154">Derlemeler ile işleri için güncelleştirilmiş .dll derlemelerine ADLA veritabanınızı kaydedin:</span><span class="sxs-lookup"><span data-stu-id="dec11-154">For jobs with assemblies, register the updated .dll assemblies into your ADLA database:</span></span>
    1. <span data-ttu-id="dec11-155">Sunucu Gezgini veya Bulut Gezgini'nden, genişletin **ADLA hesabı > veritabanları** düğümü.</span><span class="sxs-lookup"><span data-stu-id="dec11-155">From Server Explorer or Cloud Explorer, expand the **ADLA account > Databases** node.</span></span>
    2. <span data-ttu-id="dec11-156">Sağ **derlemeleri** ve yeni .dll derlemeleriniz ADLA veritabanı ile kaydetme: ![Azure Data Lake Analytics U-SQL hata ayıklama derlemesi kaydetme](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-register-assembly.png)</span><span class="sxs-lookup"><span data-stu-id="dec11-156">Right-click **Assemblies** and register your new .dll assemblies with the ADLA database: ![Azure Data Lake Analytics U-SQL debug register assembly](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-register-assembly.png)</span></span>
3. <span data-ttu-id="dec11-157">İşinizi yeniden gönderin.</span><span class="sxs-lookup"><span data-stu-id="dec11-157">Resubmit your job.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dec11-158">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="dec11-158">Next steps</span></span>

- [<span data-ttu-id="dec11-159">U-SQL Programlama Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="dec11-159">U-SQL programmability guide</span></span>](data-lake-analytics-u-sql-programmability-guide.md)
- [<span data-ttu-id="dec11-160">Azure Data Lake Analytics işleri için U-SQL kullanıcı tanımlı işleçleri geliştirme</span><span class="sxs-lookup"><span data-stu-id="dec11-160">Develop U-SQL User-defined operators for Azure Data Lake Analytics jobs</span></span>](data-lake-analytics-u-sql-develop-user-defined-operators.md)
- [<span data-ttu-id="dec11-161">Öğretici: Visual Studio için Data Lake Araçları'nı kullanarak U-SQL betikleri geliştirme</span><span class="sxs-lookup"><span data-stu-id="dec11-161">Tutorial: develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
