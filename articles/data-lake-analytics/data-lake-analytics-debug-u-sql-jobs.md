---
title: "aaaDebug U-SQL işleri | Microsoft Docs"
description: "Nasıl toodebug U-SQL Visual Studio kullanarak köşe başarısız öğrenin."
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
ms.openlocfilehash: 092bffa1a59ed91c5837402d0276447480b923fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-user-defined-c-code-for-failed-u-sql-jobs"></a><span data-ttu-id="b9702-103">Hata ayıklama başarısız U-SQL işleri için kullanıcı tanımlı C# kodu</span><span class="sxs-lookup"><span data-stu-id="b9702-103">Debug user-defined C# code for failed U-SQL jobs</span></span>

<span data-ttu-id="b9702-104">U-SQL, kod tooadd işlevselliği özel ayıklayıcısı veya reducer gibi yazma için C# kullanarak genişletilebilirlik modeli sağlar.</span><span class="sxs-lookup"><span data-stu-id="b9702-104">U-SQL provides an extensibility model using C#, so you can write your code tooadd functionality such as a custom extractor or reducer.</span></span> <span data-ttu-id="b9702-105">toolearn daha, fazla [U-SQL Programlama Kılavuzu](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-u-sql-programmability-guide#use-user-defined-functions-udf).</span><span class="sxs-lookup"><span data-stu-id="b9702-105">toolearn more, see [U-SQL programmability guide](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-u-sql-programmability-guide#use-user-defined-functions-udf).</span></span> <span data-ttu-id="b9702-106">Uygulamada hata ayıklama herhangi bir kod gerekebilir ve büyük veri sistemlerini yalnızca sınırlı çalışma zamanı hata ayıklama günlük dosyaları gibi bilgileri sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="b9702-106">In practice any code may need debugging, and big data systems may only provide limited runtime debugging information such as log files.</span></span>

<span data-ttu-id="b9702-107">Visual Studio için Azure Data Lake araçları adlı bir özelliği sağlar **köşe hata ayıklama başarısız**, olanak sağlayan, hata ayıklama için hello bulut tooyour yerel makinedeki başarısız bir işi klonlayın.</span><span class="sxs-lookup"><span data-stu-id="b9702-107">Azure Data Lake Tools for Visual Studio provides a feature called **Failed Vertex Debug**, which lets you clone a failed job from hello cloud tooyour local machine for debugging.</span></span> <span data-ttu-id="b9702-108">Merhaba yerel kopya hello tüm bulut ortamı, herhangi bir giriş veri ve kullanıcı kodu da dahil olmak üzere yakalar.</span><span class="sxs-lookup"><span data-stu-id="b9702-108">hello local clone captures hello entire cloud environment, including any input data and user code.</span></span>

<span data-ttu-id="b9702-109">Merhaba aşağıdaki videoda Azure Data Lake araçları Debug başarısız köşe için Visual Studio gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="b9702-109">hello following video demonstrates Failed Vertex Debug in Azure Data Lake Tools for Visual Studio.</span></span>

> [!VIDEO https://e0d1.wpc.azureedge.net/80E0D1/OfficeMixProdMediaBlobStorage/asset-d3aeab42-6149-4ecc-b044-aa624901ab32/b0fc0373c8f94f1bb8cd39da1310adb8.mp4?sv=2012-02-12&sr=c&si=a91fad76-cfdd-4513-9668-483de39e739c&sig=K%2FR%2FdnIi9S6P%2FBlB3iLAEV5pYu6OJFBDlQy%2FQtZ7E7M%3D&se=2116-07-19T09:27:30Z&rscd=attachment%3B%20filename%3DDebugyourcustomcodeinUSQLADLA.mp4]
>

> [!NOTE]
> <span data-ttu-id="b9702-110">Visual Studio zaten yüklü değilse şu iki güncelleştirmeleri hello gerektirir: [Microsoft Visual C++ 2015 Redistributable güncelleştirme 3](https://www.microsoft.com/en-us/download/details.aspx?id=53840) ve [Evrensel C çalışma zamanı için Windows](https://www.microsoft.com/download/details.aspx?id=50410).</span><span class="sxs-lookup"><span data-stu-id="b9702-110">Visual Studio requires hello following two updates, if they are not already installed: [Microsoft Visual C++ 2015 Redistributable Update 3](https://www.microsoft.com/en-us/download/details.aspx?id=53840) and the [Universal C Runtime for Windows](https://www.microsoft.com/download/details.aspx?id=50410).</span></span>

## <a name="download-failed-vertex-toolocal-machine"></a><span data-ttu-id="b9702-111">Yükleme başarısız köşe toolocal makine</span><span class="sxs-lookup"><span data-stu-id="b9702-111">Download failed vertex toolocal machine</span></span>

<span data-ttu-id="b9702-112">Visual Studio için Azure Data Lake araçları başarısız bir işi açtığınızda, sarı bir uyarı çubuğu hello hata sekmesinde ayrıntılı hata iletileri ile bakın.</span><span class="sxs-lookup"><span data-stu-id="b9702-112">When you open a failed job in Azure Data Lake Tools for Visual Studio, you see a yellow alert bar with detailed error messages in hello error tab.</span></span>

1. <span data-ttu-id="b9702-113">Tıklatın **karşıdan** tüm hello toodownload gerekli kaynakları ve giriş akışları.</span><span class="sxs-lookup"><span data-stu-id="b9702-113">Click **Download** toodownload all hello required resources and input streams.</span></span> <span data-ttu-id="b9702-114">Merhaba indirme tamamlanmazsa, tıklatın **yeniden**.</span><span class="sxs-lookup"><span data-stu-id="b9702-114">If hello download doesn't complete, click **Retry**.</span></span>

2. <span data-ttu-id="b9702-115">Tıklatın **açık** toogenerate yerel hata ayıklama ortamı hello yükleme tamamlandıktan sonra.</span><span class="sxs-lookup"><span data-stu-id="b9702-115">Click **Open** after hello download completes toogenerate a local debugging environment.</span></span> <span data-ttu-id="b9702-116">Hata ayıklama çözümü olan yeni bir Visual Studio örneği otomatik olarak oluşturulan ve açılır.</span><span class="sxs-lookup"><span data-stu-id="b9702-116">A new Visual Studio instance with a debugging solution is automatically created and opened.</span></span>

![Azure Data Lake Analytics U-SQL hata ayıklama visual studio indirme köşe](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-download-vertex.png)

<span data-ttu-id="b9702-118">İşlerini arka plan kodu kaynak dosyaları veya kayıtlı derlemeler içerebilir ve bu iki türlerinin farklı hata ayıklama senaryolar vardır.</span><span class="sxs-lookup"><span data-stu-id="b9702-118">Jobs may include code-behind source files or registered assemblies, and these two types have different debugging scenarios.</span></span>

- [<span data-ttu-id="b9702-119">Arka plan kodu ile başarısız bir işi hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="b9702-119">Debug a failed job with code-behind</span></span>](#debug-job-failed-with-code-behind)
- [<span data-ttu-id="b9702-120">Başarısız bir işi derlemeleri ile hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="b9702-120">Debug a failed job with assemblies</span></span>](#debug-job-failed-with-assemblies)


## <a name="debug-job-failed-with-code-behind"></a><span data-ttu-id="b9702-121">Hata ayıklama işi arka plan kodu ile başarısız oldu</span><span class="sxs-lookup"><span data-stu-id="b9702-121">Debug job failed with code-behind</span></span>

<span data-ttu-id="b9702-122">U-SQL işi başarısız olursa ve hello işi kullanıcı kodu içerir (genellikle adlı `Script.usql.cs` U-SQL projesinde), kaynak kodu çözüm hata ayıklama hello alınır.</span><span class="sxs-lookup"><span data-stu-id="b9702-122">If a U-SQL job fails, and hello job includes user code (typically named `Script.usql.cs` in a U-SQL project), that source code is imported into hello debugging solution.</span></span>  <span data-ttu-id="b9702-123">Buradan hello Visual Studio hata ayıklama araçları (izleme, değişkenleri, vb.) tootroubleshoot hello sorun kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b9702-123">From there you can use hello Visual Studio debugging tools (watch, variables, etc.) tootroubleshoot hello problem.</span></span>

> [!NOTE]
> <span data-ttu-id="b9702-124">Hata ayıklama önce emin toocheck olması **ortak dil çalışma zamanı özel durumları** hello özel ayarları penceresinde (**Ctrl + Alt + E**).</span><span class="sxs-lookup"><span data-stu-id="b9702-124">Before debugging, be sure toocheck **Common Language Runtime Exceptions** in hello Exception Settings window (**Ctrl + Alt + E**).</span></span>

![Azure Data Lake Analytics U-SQL hata ayıklama visual studio ayarı](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-clr-exception-setting.png)

1. <span data-ttu-id="b9702-126">Tuşuna **F5** toorun hello arka plan kodu kodu.</span><span class="sxs-lookup"><span data-stu-id="b9702-126">Press **F5** toorun hello code-behind code.</span></span> <span data-ttu-id="b9702-127">Bir özel durum tarafından durduruluncaya kadar çalışmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="b9702-127">It will run until it is stopped by an exception.</span></span>

2. <span data-ttu-id="b9702-128">Açık hello `ADLTool_Codebehind.usql.cs` dosya ve kesme, tuşuna basarak **F5** toodebug hello kod adım adım.</span><span class="sxs-lookup"><span data-stu-id="b9702-128">Open hello `ADLTool_Codebehind.usql.cs` file and set breakpoints, then press **F5** toodebug hello code step by step.</span></span>

    ![Azure Data Lake Analytics U-SQL hata ayıklama özel durumu](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-debug-exception.png)

## <a name="debug-job-failed-with-assemblies"></a><span data-ttu-id="b9702-130">Hata ayıklama işi derlemeleri ile başarısız oldu</span><span class="sxs-lookup"><span data-stu-id="b9702-130">Debug job failed with assemblies</span></span>

<span data-ttu-id="b9702-131">U-SQL komut dosyanıza kayıtlı derlemeleri kullanırsanız, hello sistem hello kaynak kodu otomatik olarak alınamıyor.</span><span class="sxs-lookup"><span data-stu-id="b9702-131">If you use registered assemblies in your U-SQL script, hello system can't get hello source code automatically.</span></span> <span data-ttu-id="b9702-132">Bu durumda, hello derlemeleri kaynak kodu dosyaları toohello çözümü el ile ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b9702-132">In this case, manually add hello assemblies' source code files toohello solution.</span></span>

### <a name="configure-hello-solution"></a><span data-ttu-id="b9702-133">Merhaba çözümünüzü yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b9702-133">Configure hello solution</span></span>

1. <span data-ttu-id="b9702-134">Sağ **çözüm 'VertexDebug' > Ekle > mevcut proje...**  toofind derlemelerin kaynak kodu hello ve çözüm hata ayıklama hello proje toohello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b9702-134">Right-click **Solution 'VertexDebug' > Add > Existing Project...** toofind hello assemblies' source code and add hello project toohello debugging solution.</span></span>

    ![Azure Data Lake Analytics U-SQL hata ayıklama proje ekleyin](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-add-project-to-debug-solution.png)

2. <span data-ttu-id="b9702-136">Sağ **LocalVertexHost > Özellikler** hello çözüm ve kopyalama hello içinde **çalışma dizini** yolu.</span><span class="sxs-lookup"><span data-stu-id="b9702-136">Right-click **LocalVertexHost > Properties** in hello solution and copy hello **Working Directory** path.</span></span>

3. <span data-ttu-id="b9702-137">Sağ **derleme kaynak kod projesi > Özellikleri**seçin hello **yapı** sekmesinde solda ve kopyalanan hello yolu olarak Yapıştır **çıkış > çıkış yolu**.</span><span class="sxs-lookup"><span data-stu-id="b9702-137">Right-Click **assembly source code project > Properties**, select hello **Build** tab at left, and paste hello copied path as **Output > Output path**.</span></span>

    ![Azure Data Lake Analytics U-SQL hata ayıklama pdb yolunu ayarlama](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-set-pdb-path.png)

4. <span data-ttu-id="b9702-139">Tuşuna **Ctrl + Alt + E**, denetleme **ortak dil çalışma zamanı özel durumları** özel ayarları penceresinde.</span><span class="sxs-lookup"><span data-stu-id="b9702-139">Press **Ctrl + Alt + E**, check **Common Language Runtime Exceptions** in Exception Settings window.</span></span>

### <a name="start-debug"></a><span data-ttu-id="b9702-140">Hata ayıklama Başlat</span><span class="sxs-lookup"><span data-stu-id="b9702-140">Start debug</span></span>

1. <span data-ttu-id="b9702-141">Sağ **derleme kaynak kod projesi > yeniden** toooutput .pdb dosyaları toohello `LocalVertexHost` çalışma dizini.</span><span class="sxs-lookup"><span data-stu-id="b9702-141">Right-click **assembly source code project > Rebuild** toooutput .pdb files toohello `LocalVertexHost` working directory.</span></span>

2. <span data-ttu-id="b9702-142">Tuşuna **F5** ve başlangıç projesi bir özel durum tarafından durduruluncaya kadar çalışır.</span><span class="sxs-lookup"><span data-stu-id="b9702-142">Press **F5** and hello project will run until it is stopped by an exception.</span></span> <span data-ttu-id="b9702-143">Güvenle yok sayabilirsiniz uyarı iletisi aşağıdaki hello görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b9702-143">You may see hello following warning message, which you can safely ignore.</span></span> <span data-ttu-id="b9702-144">Tooa minute tooget toohello hata ayıklama ekranı alabilir.</span><span class="sxs-lookup"><span data-stu-id="b9702-144">It can take up tooa minute tooget toohello debug screen.</span></span>

    ![Azure Data Lake Analytics U-SQL hata ayıklama visual studio uyarı](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-visual-studio-u-sql-debug-warning.png)

3. <span data-ttu-id="b9702-146">Kaynak kodunuz açın ve kesme, tuşuna basarak **F5** toodebug hello kod adım adım.</span><span class="sxs-lookup"><span data-stu-id="b9702-146">Open your source code and set breakpoints, then press **F5** toodebug hello code step by step.</span></span>

<span data-ttu-id="b9702-147">Merhaba Visual Studio hata ayıklama araçları (izleme, değişkenleri, vb.) tootroubleshoot hello sorun de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b9702-147">You can also use hello Visual Studio debugging tools (watch, variables, etc.) tootroubleshoot hello problem.</span></span>

> [!NOTE]
> <span data-ttu-id="b9702-148">Merhaba derleme kaynak kod projesi hello kod güncelleştirilmiş toogenerate .pdb dosyaları değiştirdikten sonra her zaman yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b9702-148">Rebuild hello assembly source code project each time after you modify hello code toogenerate updated .pdb files.</span></span>

<span data-ttu-id="b9702-149">Hello Proje başarıyla tamamlarsa hata ayıklama sonra hello çıktı penceresinde hello iletiden gösterir:</span><span class="sxs-lookup"><span data-stu-id="b9702-149">After debugging, if hello project completes successfully hello output window shows hello following message:</span></span>

```
hello Program 'LocalVertexHost.exe' has exited with code 0 (0x0).
```

![Azure Data Lake Analytics U-SQL hata ayıklama başarılı](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-debug-succeed.png)

## <a name="resubmit-hello-job"></a><span data-ttu-id="b9702-151">Merhaba işi yeniden gönderin</span><span class="sxs-lookup"><span data-stu-id="b9702-151">Resubmit hello job</span></span>

<span data-ttu-id="b9702-152">Hata ayıklama tamamladıktan sonra hello başarısız işi yeniden gönderin.</span><span class="sxs-lookup"><span data-stu-id="b9702-152">Once you have completed debugging, resubmit hello failed job.</span></span>

1. <span data-ttu-id="b9702-153">Arka plan kodu çözümleriyle işleri için C# kodu hello arka plan kodu kaynak dosyaya kopyalayın (genellikle `Script.usql.cs`).</span><span class="sxs-lookup"><span data-stu-id="b9702-153">For jobs with code-behind solutions, copy your C# code into hello code-behind source file (typically `Script.usql.cs`).</span></span>
2. <span data-ttu-id="b9702-154">Derlemeler ile işleri için güncelleştirilmiş hello .dll derlemelerine ADLA veritabanınızı kaydedin:</span><span class="sxs-lookup"><span data-stu-id="b9702-154">For jobs with assemblies, register hello updated .dll assemblies into your ADLA database:</span></span>
    1. <span data-ttu-id="b9702-155">Sunucu Gezgini veya Bulut Gezgini'nden, hello genişletin **ADLA hesabı > veritabanları** düğümü.</span><span class="sxs-lookup"><span data-stu-id="b9702-155">From Server Explorer or Cloud Explorer, expand hello **ADLA account > Databases** node.</span></span>
    2. <span data-ttu-id="b9702-156">Sağ **derlemeleri** ve yeni .dll derlemeleriniz hello ADLA veritabanı ile kaydetme: ![Azure Data Lake Analytics U-SQL hata ayıklama derlemesi kaydetme](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-register-assembly.png)</span><span class="sxs-lookup"><span data-stu-id="b9702-156">Right-click **Assemblies** and register your new .dll assemblies with hello ADLA database: ![Azure Data Lake Analytics U-SQL debug register assembly](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-register-assembly.png)</span></span>
3. <span data-ttu-id="b9702-157">İşinizi yeniden gönderin.</span><span class="sxs-lookup"><span data-stu-id="b9702-157">Resubmit your job.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b9702-158">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b9702-158">Next steps</span></span>

- [<span data-ttu-id="b9702-159">U-SQL Programlama Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="b9702-159">U-SQL programmability guide</span></span>](data-lake-analytics-u-sql-programmability-guide.md)
- [<span data-ttu-id="b9702-160">Azure Data Lake Analytics işleri için U-SQL kullanıcı tanımlı işleçleri geliştirme</span><span class="sxs-lookup"><span data-stu-id="b9702-160">Develop U-SQL User-defined operators for Azure Data Lake Analytics jobs</span></span>](data-lake-analytics-u-sql-develop-user-defined-operators.md)
- [<span data-ttu-id="b9702-161">Öğretici: Visual Studio için Data Lake Araçları'nı kullanarak U-SQL betikleri geliştirme</span><span class="sxs-lookup"><span data-stu-id="b9702-161">Tutorial: develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
