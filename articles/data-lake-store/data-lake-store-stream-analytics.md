---
title: "Stream Analytics Data Lake Store içine aaaStream verilerden | Microsoft Docs"
description: "Azure Stream Analytics toostream verileri Azure Data Lake Store içinde kullanma"
services: data-lake-store,stream-analytics
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: edb58e0b-311f-44b0-a499-04d7e6c07a90
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 68c727d4807db0abe6efa90145d68c78902eb789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="stream-data-from-azure-storage-blob-into-data-lake-store-using-azure-stream-analytics"></a><span data-ttu-id="165d9-103">Azure Akış Analizi’ni kullanarak Azure Depolama Blobundan Data Lake Store’a veri akışı gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="165d9-103">Stream data from Azure Storage Blob into Data Lake Store using Azure Stream Analytics</span></span>
<span data-ttu-id="165d9-104">Bu makalede Azure Data Lake nasıl toouse depolamak için bir Azure akış analizi işi bir çıktı olarak öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="165d9-104">In this article you will learn how toouse Azure Data Lake Store as an output for an Azure Stream Analytics job.</span></span> <span data-ttu-id="165d9-105">Bu makale bir Azure Storage blobundan (giriş) verilerini okuyan basit bir senaryo gösterir ve veri tooData Lake deposu (çıktı) yazma hello.</span><span class="sxs-lookup"><span data-stu-id="165d9-105">This article demonstrates a simple scenario that reads data from an Azure Storage blob (input) and writes hello data tooData Lake Store (output).</span></span>

> [!NOTE]
> <span data-ttu-id="165d9-106">Şu anda oluşturma ve Data Lake Store yapılandırmasını çıkaran Stream Analytics yalnızca hello desteklenen [Klasik Azure portalı](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="165d9-106">At this time, creation and configuration of Data Lake Store outputs for Stream Analytics is supported only in hello [Azure Classic Portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="165d9-107">Bu nedenle, bu öğreticinin bazı bölümleri hello Klasik Azure portalı kullanır.</span><span class="sxs-lookup"><span data-stu-id="165d9-107">Hence, some parts of this tutorial will use hello Azure Classic Portal.</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="165d9-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="165d9-108">Prerequisites</span></span>
<span data-ttu-id="165d9-109">Bu öğreticiye başlamadan önce hello şunlara sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="165d9-109">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="165d9-110">**Bir Azure aboneliği**.</span><span class="sxs-lookup"><span data-stu-id="165d9-110">**An Azure subscription**.</span></span> <span data-ttu-id="165d9-111">Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="165d9-111">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="165d9-112">**Azure Depolama hesabı**.</span><span class="sxs-lookup"><span data-stu-id="165d9-112">**Azure Storage account**.</span></span> <span data-ttu-id="165d9-113">Bu hesap tooinput verilerden bir blob kapsayıcı için bir akış analizi işi kullanır.</span><span class="sxs-lookup"><span data-stu-id="165d9-113">You will use a blob container from this account tooinput data for a Stream Analytics job.</span></span> <span data-ttu-id="165d9-114">Bu öğretici için adlı bir depolama hesabı olduğunu varsayın **storageforasa** hello hesabı içindeki bir kapsayıcı adı verilen ve **storageforasacontainer**.</span><span class="sxs-lookup"><span data-stu-id="165d9-114">For this tutorial, assume you have a storage account called **storageforasa** and a container within hello account called **storageforasacontainer**.</span></span> <span data-ttu-id="165d9-115">Merhaba kapsayıcısı oluşturduktan sonra bir örnek veri dosyası tooit karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="165d9-115">Once you have created hello container, upload a sample data file tooit.</span></span> 
  
* <span data-ttu-id="165d9-116">**Azure Data Lake Store hesabı**.</span><span class="sxs-lookup"><span data-stu-id="165d9-116">**Azure Data Lake Store account**.</span></span> <span data-ttu-id="165d9-117">Merhaba yönergeleri izleyin [Azure Data Lake hello Azure Portal kullanarak Store ile çalışmaya başlama](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="165d9-117">Follow hello instructions at [Get started with Azure Data Lake Store using hello Azure Portal](data-lake-store-get-started-portal.md).</span></span> <span data-ttu-id="165d9-118">Adlı bir Data Lake Store hesabı sahip varsayalım **asadatalakestore**.</span><span class="sxs-lookup"><span data-stu-id="165d9-118">Let's assume you have a Data Lake Store account called **asadatalakestore**.</span></span> 

## <a name="create-a-stream-analytics-job"></a><span data-ttu-id="165d9-119">Akış analizi işi oluşturma</span><span class="sxs-lookup"><span data-stu-id="165d9-119">Create a Stream Analytics Job</span></span>
<span data-ttu-id="165d9-120">Bir giriş kaynağı ve bir çıkış hedefini içeren bir akış analizi işi oluşturarak başlayın.</span><span class="sxs-lookup"><span data-stu-id="165d9-120">You start by creating a Stream Analytics job that includes an input source and an output destination.</span></span> <span data-ttu-id="165d9-121">Bu öğretici için hello kaynak bir Azure blob kapsayıcısı ve hello hedef Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="165d9-121">For this tutorial, hello source is an Azure blob container and hello destination is Data Lake Store.</span></span>

1. <span data-ttu-id="165d9-122">Toohello üzerinde oturum [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="165d9-122">Sign on toohello [Azure Portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="165d9-123">Merhaba sol bölmeden tıklatın **akış analizi işleri**ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="165d9-123">From hello left pane, click **Stream Analytics jobs**, and then click **Add**.</span></span>

    <span data-ttu-id="165d9-124">![Stream Analytics işi oluşturmak](./media/data-lake-store-stream-analytics/create.job.png "Stream Analytics işi oluşturma")</span><span class="sxs-lookup"><span data-stu-id="165d9-124">![Create a Stream Analytics Job](./media/data-lake-store-stream-analytics/create.job.png "Create a Stream Analytics job")</span></span>

    > [!NOTE]
    > <span data-ttu-id="165d9-125">Hello iş oluşturduğunuzdan emin olun veya hello depolama hesabı ile aynı bölgeye bölgeler arasında veri taşıma ek maliyet erişimliye.</span><span class="sxs-lookup"><span data-stu-id="165d9-125">Make sure you create job in hello same region as hello storage account or you will incur additional cost of moving data between regions.</span></span>
    >

## <a name="create-a-blob-input-for-hello-job"></a><span data-ttu-id="165d9-126">Bir Blob giriş hello işi için oluşturma</span><span class="sxs-lookup"><span data-stu-id="165d9-126">Create a Blob input for hello job</span></span>

1. <span data-ttu-id="165d9-127">Merhaba sol bölmesinden hello Stream Analytics işi için açık hello sayfasını tıklatın hello **girişleri** sekmesini ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="165d9-127">Open hello page for hello Stream Analytics job, from hello left pane click hello **Inputs** tab, and then click **Add**.</span></span>

    <span data-ttu-id="165d9-128">![Bir giriş tooyour işi eklemek](./media/data-lake-store-stream-analytics/create.input.1.png "bir giriş tooyour işi ekleme")</span><span class="sxs-lookup"><span data-stu-id="165d9-128">![Add an input tooyour job](./media/data-lake-store-stream-analytics/create.input.1.png "Add an input tooyour job")</span></span>

2. <span data-ttu-id="165d9-129">Merhaba üzerinde **yeni giriş** dikey penceresinde hello aşağıdaki değerleri sağlayın.</span><span class="sxs-lookup"><span data-stu-id="165d9-129">On hello **New input** blade, provide hello following values.</span></span>

    <span data-ttu-id="165d9-130">![Bir giriş tooyour işi eklemek](./media/data-lake-store-stream-analytics/create.input.2.png "bir giriş tooyour işi ekleme")</span><span class="sxs-lookup"><span data-stu-id="165d9-130">![Add an input tooyour job](./media/data-lake-store-stream-analytics/create.input.2.png "Add an input tooyour job")</span></span>

    * <span data-ttu-id="165d9-131">İçin **giriş diğer adı**, hello iş giriş için benzersiz bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="165d9-131">For **Input alias**, enter a unique name for hello job input.</span></span>
    * <span data-ttu-id="165d9-132">İçin **kaynak türünü**seçin **veri akışı**.</span><span class="sxs-lookup"><span data-stu-id="165d9-132">For **Source type**, select **Data stream**.</span></span>
    * <span data-ttu-id="165d9-133">İçin **kaynak**seçin **Blob storage**.</span><span class="sxs-lookup"><span data-stu-id="165d9-133">For **Source**, select **Blob storage**.</span></span>
    * <span data-ttu-id="165d9-134">İçin **abonelik**seçin **blob storage'ı geçerli aboneliğe ilişkin kullanma**.</span><span class="sxs-lookup"><span data-stu-id="165d9-134">For **Subscription**, select **Use blob storage from current subscription**.</span></span>
    * <span data-ttu-id="165d9-135">İçin **depolama hesabı**, hello Önkoşullar bir parçası olarak, oluşturduğunuz hello depolama hesabını seçin.</span><span class="sxs-lookup"><span data-stu-id="165d9-135">For **Storage account**, select hello storage account that you created as part of hello prerequisites.</span></span> 
    * <span data-ttu-id="165d9-136">İçin **kapsayıcı**seçin hello oluşturulan hello kapsayıcı seçilen depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="165d9-136">For **Container**, select hello container that you created in hello selected storage account.</span></span>
    * <span data-ttu-id="165d9-137">İçin **olayı seri hale getirme biçimi**seçin **CSV**.</span><span class="sxs-lookup"><span data-stu-id="165d9-137">For **Event serialization format**, select **CSV**.</span></span>
    * <span data-ttu-id="165d9-138">İçin **sınırlayıcı**seçin **sekmesini**.</span><span class="sxs-lookup"><span data-stu-id="165d9-138">For **Delimiter**, select **tab**.</span></span>
    * <span data-ttu-id="165d9-139">İçin **kodlama**seçin **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="165d9-139">For **Encoding**, select **UTF-8**.</span></span>

    <span data-ttu-id="165d9-140">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="165d9-140">Click **Create**.</span></span> <span data-ttu-id="165d9-141">Merhaba portal şimdi hello giriş ekler ve hello bağlantı tooit sınar.</span><span class="sxs-lookup"><span data-stu-id="165d9-141">hello portal now adds hello input and tests hello connection tooit.</span></span>


## <a name="create-a-data-lake-store-output-for-hello-job"></a><span data-ttu-id="165d9-142">Bir Data Lake Store çıktı hello işi için oluşturma</span><span class="sxs-lookup"><span data-stu-id="165d9-142">Create a Data Lake Store output for hello job</span></span>

1. <span data-ttu-id="165d9-143">Merhaba hello Stream Analytics işi hello sayfasını açın, **çıkışları** sekmesini ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="165d9-143">Open hello page for hello Stream Analytics job, click hello **Outputs** tab, and then click **Add**.</span></span>

    <span data-ttu-id="165d9-144">![Bir çıkış tooyour işi eklemek](./media/data-lake-store-stream-analytics/create.output.1.png "bir çıktı tooyour işi ekleme")</span><span class="sxs-lookup"><span data-stu-id="165d9-144">![Add an output tooyour job](./media/data-lake-store-stream-analytics/create.output.1.png "Add an output tooyour job")</span></span>

2. <span data-ttu-id="165d9-145">Merhaba üzerinde **yeni çıktı** dikey penceresinde hello aşağıdaki değerleri sağlayın.</span><span class="sxs-lookup"><span data-stu-id="165d9-145">On hello **New output** blade, provide hello following values.</span></span>

    <span data-ttu-id="165d9-146">![Bir çıkış tooyour işi eklemek](./media/data-lake-store-stream-analytics/create.output.2.png "bir çıktı tooyour işi ekleme")</span><span class="sxs-lookup"><span data-stu-id="165d9-146">![Add an output tooyour job](./media/data-lake-store-stream-analytics/create.output.2.png "Add an output tooyour job")</span></span>

    * <span data-ttu-id="165d9-147">İçin **çıkış diğer adları**, girin bir hello iş çıktısı için benzersiz bir ad.</span><span class="sxs-lookup"><span data-stu-id="165d9-147">For **Output alias**, enter a a unique name for hello job output.</span></span> <span data-ttu-id="165d9-148">Bu sorguları toodirect hello sorgu çıktı toothis Data Lake Store kullanılan kolay bir addır.</span><span class="sxs-lookup"><span data-stu-id="165d9-148">This is a friendly name used in queries toodirect hello query output toothis Data Lake Store.</span></span>
    * <span data-ttu-id="165d9-149">İçin **havuzu**seçin **Data Lake Store**.</span><span class="sxs-lookup"><span data-stu-id="165d9-149">For **Sink**, select **Data Lake Store**.</span></span>
    * <span data-ttu-id="165d9-150">İstendiğinde tooauthorize olacaktır erişim tooData Lake Store hesabı.</span><span class="sxs-lookup"><span data-stu-id="165d9-150">You will be prompted tooauthorize access tooData Lake Store account.</span></span> <span data-ttu-id="165d9-151">Tıklatın **yetkilendirmek**.</span><span class="sxs-lookup"><span data-stu-id="165d9-151">Click **Authorize**.</span></span>

3. <span data-ttu-id="165d9-152">Hello üzerinde **yeni çıktı** dikey penceresinde değerleri aşağıdaki tooprovide hello devam edin.</span><span class="sxs-lookup"><span data-stu-id="165d9-152">On hello **New output** blade, continue tooprovide hello following values.</span></span>

    <span data-ttu-id="165d9-153">![Bir çıkış tooyour işi eklemek](./media/data-lake-store-stream-analytics/create.output.3.png "bir çıktı tooyour işi ekleme")</span><span class="sxs-lookup"><span data-stu-id="165d9-153">![Add an output tooyour job](./media/data-lake-store-stream-analytics/create.output.3.png "Add an output tooyour job")</span></span>

    * <span data-ttu-id="165d9-154">İçin **hesap adı**, hello Data Lake Store hesabını önceden oluşturulmuş hello proje çıktı toobe gönderilmesini istediğiniz yeri seçin.</span><span class="sxs-lookup"><span data-stu-id="165d9-154">For **Account name**, select hello Data Lake Store account you already created where you want hello job output toobe sent to.</span></span>
    * <span data-ttu-id="165d9-155">İçin **yol önek deseni**, bir dosya yolu kullanılan toowrite girin dosyalarınızı hello içinde belirtilen Data Lake Store hesabı.</span><span class="sxs-lookup"><span data-stu-id="165d9-155">For **Path prefix pattern**, enter a file path used toowrite your files within hello specified Data Lake Store account.</span></span>
    * <span data-ttu-id="165d9-156">İçin **tarih biçimi**, hello önek yolunda bir tarih belirteci kullandıysanız, dosyalarınızı düzenlenir hello tarih biçimi seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="165d9-156">For **Date format**, if you used a date token in hello prefix path, you can select hello date format in which your files are organized.</span></span>
    * <span data-ttu-id="165d9-157">İçin **saat biçimi**, bir zaman belirteci hello önek yolunda kullandıysanız, dosyalarınızı düzenlenir hello saat biçimini belirtin.</span><span class="sxs-lookup"><span data-stu-id="165d9-157">For **Time format**, if you used a time token in hello prefix path, specify hello time format in which your files are organized.</span></span>
    * <span data-ttu-id="165d9-158">İçin **olayı seri hale getirme biçimi**seçin **CSV**.</span><span class="sxs-lookup"><span data-stu-id="165d9-158">For **Event serialization format**, select **CSV**.</span></span>
    * <span data-ttu-id="165d9-159">İçin **sınırlayıcı**seçin **sekmesini**.</span><span class="sxs-lookup"><span data-stu-id="165d9-159">For **Delimiter**, select **tab**.</span></span>
    * <span data-ttu-id="165d9-160">İçin **kodlama**seçin **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="165d9-160">For **Encoding**, select **UTF-8**.</span></span>
    
    <span data-ttu-id="165d9-161">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="165d9-161">Click **Create**.</span></span> <span data-ttu-id="165d9-162">Merhaba portal şimdi hello çıktı ekler ve hello bağlantı tooit sınar.</span><span class="sxs-lookup"><span data-stu-id="165d9-162">hello portal now adds hello output and tests hello connection tooit.</span></span>
    
## <a name="run-hello-stream-analytics-job"></a><span data-ttu-id="165d9-163">Merhaba Stream Analytics işini çalıştır</span><span class="sxs-lookup"><span data-stu-id="165d9-163">Run hello Stream Analytics job</span></span>

1. <span data-ttu-id="165d9-164">toorun Stream Analytics işi, bir sorgu hello çalıştırmalısınız **sorgu** sekmesi. Bu öğretici için değiştirerek hello örnek sorgu çalıştırabilirsiniz hello hello yer tutucularını iş giriş ve çıkış diğer adları, aşağıdaki hello ekran görüntüsünde gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="165d9-164">toorun a Stream Analytics job, you must run a query from hello **Query** tab. For this tutorial, you can run hello sample query by replacing hello placeholders with hello job input and output aliases, as shown in hello screen capture below.</span></span>

    <span data-ttu-id="165d9-165">![Sorguyu çalıştırmak](./media/data-lake-store-stream-analytics/run.query.png "sorgusu çalıştırma")</span><span class="sxs-lookup"><span data-stu-id="165d9-165">![Run query](./media/data-lake-store-stream-analytics/run.query.png "Run query")</span></span>

2. <span data-ttu-id="165d9-166">Tıklatın **kaydetmek** hello ekranın hello ve ardından hello **genel bakış** sekmesini tıklatın, **Başlat**.</span><span class="sxs-lookup"><span data-stu-id="165d9-166">Click **Save** from hello top of hello screen, and then from hello **Overview** tab, click **Start**.</span></span> <span data-ttu-id="165d9-167">Merhaba iletişim kutusundan **özel zaman**ve geçerli tarih ve saat hello ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="165d9-167">From hello dialog box, select **Custom Time**, and then set hello current date and time.</span></span>

    <span data-ttu-id="165d9-168">![İş saati ayarlayın](./media/data-lake-store-stream-analytics/run.query.2.png "iş saati ayarlayın")</span><span class="sxs-lookup"><span data-stu-id="165d9-168">![Set job time](./media/data-lake-store-stream-analytics/run.query.2.png "Set job time")</span></span>

    <span data-ttu-id="165d9-169">Tıklatın **Başlat** toostart hello işi.</span><span class="sxs-lookup"><span data-stu-id="165d9-169">Click **Start** toostart hello job.</span></span> <span data-ttu-id="165d9-170">Tooa birkaç dakika toostart hello işi alabilir.</span><span class="sxs-lookup"><span data-stu-id="165d9-170">It can take up tooa couple minutes toostart hello job.</span></span>

3. <span data-ttu-id="165d9-171">tootrigger hello iş toopick hello verilerden hello blob kopyalama bir örnek veri dosyası toohello blob kapsayıcısı.</span><span class="sxs-lookup"><span data-stu-id="165d9-171">tootrigger hello job toopick hello data from hello blob, copy a sample data file toohello blob container.</span></span> <span data-ttu-id="165d9-172">Örnek veri dosyası hello alabilirsiniz [Azure Data Lake Git deposu](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/Drivers.txt).</span><span class="sxs-lookup"><span data-stu-id="165d9-172">You can get a sample data file from hello [Azure Data Lake Git Repository](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/Drivers.txt).</span></span> <span data-ttu-id="165d9-173">Bu öğretici için şimdi hello dosya kopyalama **vehicle1_09142014.csv**.</span><span class="sxs-lookup"><span data-stu-id="165d9-173">For this tutorial, let's copy hello file **vehicle1_09142014.csv**.</span></span> <span data-ttu-id="165d9-174">Çeşitli istemciler gibi kullanabilir [Azure Storage Gezgini](http://storageexplorer.com/), tooupload veri tooa blob kapsayıcısı.</span><span class="sxs-lookup"><span data-stu-id="165d9-174">You can use various clients, such as [Azure Storage Explorer](http://storageexplorer.com/), tooupload data tooa blob container.</span></span>

4. <span data-ttu-id="165d9-175">Merhaba gelen **genel bakış** sekmesinde, altında **izleme**, hello verileri nasıl işlendiği bakın.</span><span class="sxs-lookup"><span data-stu-id="165d9-175">From hello **Overview** tab, under **Monitoring**, see how hello data was processed.</span></span>

    <span data-ttu-id="165d9-176">![İzleyici işi](./media/data-lake-store-stream-analytics/run.query.3.png "İzleyici işi")</span><span class="sxs-lookup"><span data-stu-id="165d9-176">![Monitor job](./media/data-lake-store-stream-analytics/run.query.3.png "Monitor job")</span></span>

5. <span data-ttu-id="165d9-177">Son olarak, hello proje çıktı verilerini hello Data Lake Store hesabında kullanılabilir olup olmadığını doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="165d9-177">Finally, you can verify that hello job output data is available in hello Data Lake Store account.</span></span> 

    <span data-ttu-id="165d9-178">![Doğrulama çıktı](./media/data-lake-store-stream-analytics/run.query.4.png "çıkış doğrulayın")</span><span class="sxs-lookup"><span data-stu-id="165d9-178">![Verify output](./media/data-lake-store-stream-analytics/run.query.4.png "Verify output")</span></span>

    <span data-ttu-id="165d9-179">Merhaba Veri Gezgini bölmesinde, o hello çıktı yazılı tooa klasör yolu olarak belirtilen hello Data Lake Store çıktı ayarları dikkat edin (`streamanalytics/job/output/{date}/{time}`).</span><span class="sxs-lookup"><span data-stu-id="165d9-179">In hello Data Explorer pane, notice that hello output is written tooa folder path as specified in hello Data Lake Store output settings (`streamanalytics/job/output/{date}/{time}`).</span></span>  

## <a name="see-also"></a><span data-ttu-id="165d9-180">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="165d9-180">See also</span></span>
* [<span data-ttu-id="165d9-181">Hdınsight küme toouse Data Lake Store oluşturma</span><span class="sxs-lookup"><span data-stu-id="165d9-181">Create an HDInsight cluster toouse Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
