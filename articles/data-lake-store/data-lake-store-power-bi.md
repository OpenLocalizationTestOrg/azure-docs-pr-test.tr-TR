---
title: "Power BI'ı kullanarak Data Lake Store'da verilerin çözümleme | Microsoft Docs"
description: "Azure Data Lake Store içinde depolanan verileri çözümlemek için Power BI'ı kullanın"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 57d19d27-e135-49d9-a7ea-46c48ef4e3bd
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 0cf7e385ef2edd650479e120f52469bc6632f2eb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="analyze-data-in-data-lake-store-by-using-power-bi"></a><span data-ttu-id="8ca64-103">Power BI'ı kullanarak Data Lake Store'da verilerin çözümleme</span><span class="sxs-lookup"><span data-stu-id="8ca64-103">Analyze data in Data Lake Store by using Power BI</span></span>
<span data-ttu-id="8ca64-104">Bu makalede, Power BI Desktop çözümlemek ve Azure Data Lake Store içinde depolanan verileri görselleştirmek için nasıl kullanılacağını öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="8ca64-104">In this article you will learn how to use Power BI Desktop to analyze and visualize data stored in Azure Data Lake Store.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8ca64-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="8ca64-105">Prerequisites</span></span>
<span data-ttu-id="8ca64-106">Bu öğreticiye başlamadan önce aşağıdakilere sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="8ca64-106">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="8ca64-107">**Azure aboneliği**.</span><span class="sxs-lookup"><span data-stu-id="8ca64-107">**An Azure subscription**.</span></span> <span data-ttu-id="8ca64-108">Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8ca64-108">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="8ca64-109">**Azure Data Lake Store hesabı**.</span><span class="sxs-lookup"><span data-stu-id="8ca64-109">**Azure Data Lake Store account**.</span></span> <span data-ttu-id="8ca64-110">[Azure Portal'ı kullanarak Azure Data Lake Store ile çalışmaya başlama](data-lake-store-get-started-portal.md) bölümündeki yönergeleri uygulayın.</span><span class="sxs-lookup"><span data-stu-id="8ca64-110">Follow the instructions at [Get started with Azure Data Lake Store using the Azure Portal](data-lake-store-get-started-portal.md).</span></span> <span data-ttu-id="8ca64-111">Bu makalede adlı bir Data Lake Store hesabı zaten oluşturduğunuzu varsayar **mybidatalakestore**ve bir örnek veri dosyasını karşıya (**Drivers.txt**) kendisine.</span><span class="sxs-lookup"><span data-stu-id="8ca64-111">This article assumes that you have already created a Data Lake Store account, called **mybidatalakestore**, and uploaded a sample data file (**Drivers.txt**) to it.</span></span> <span data-ttu-id="8ca64-112">Bu örnek dosya Merkezi'nden edinilebilir [Azure Data Lake Git deposu](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/Drivers.txt).</span><span class="sxs-lookup"><span data-stu-id="8ca64-112">This sample file is available for download from [Azure Data Lake Git Repository](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/Drivers.txt).</span></span>
* <span data-ttu-id="8ca64-113">**Power BI Desktop**.</span><span class="sxs-lookup"><span data-stu-id="8ca64-113">**Power BI Desktop**.</span></span> <span data-ttu-id="8ca64-114">Buradan indirebilirsiniz [Microsoft Download Center](https://www.microsoft.com/en-us/download/details.aspx?id=45331).</span><span class="sxs-lookup"><span data-stu-id="8ca64-114">You can download this from [Microsoft Download Center](https://www.microsoft.com/en-us/download/details.aspx?id=45331).</span></span> 

## <a name="create-a-report-in-power-bi-desktop"></a><span data-ttu-id="8ca64-115">Power BI Desktop'ta rapor oluşturma</span><span class="sxs-lookup"><span data-stu-id="8ca64-115">Create a report in Power BI Desktop</span></span>
1. <span data-ttu-id="8ca64-116">Power BI Desktop bilgisayarınızda başlatın.</span><span class="sxs-lookup"><span data-stu-id="8ca64-116">Launch Power BI Desktop on your computer.</span></span>
2. <span data-ttu-id="8ca64-117">Gelen **giriş** Şerit, tıklatın **Veri Al**ve daha fazlasını'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="8ca64-117">From the **Home** ribbon, click **Get Data**, and then click More.</span></span> <span data-ttu-id="8ca64-118">İçinde **Veri Al** iletişim kutusu, tıklatın **Azure**, tıklatın **Azure Data Lake Store**ve ardından **Bağlan**.</span><span class="sxs-lookup"><span data-stu-id="8ca64-118">In the **Get Data** dialog box, click **Azure**, click **Azure Data Lake Store**, and then click **Connect**.</span></span>
   
    <span data-ttu-id="8ca64-119">![Data Lake Store'a bağlama](./media/data-lake-store-power-bi/get-data-lake-store-account.png "Data Lake Store'a bağlama")</span><span class="sxs-lookup"><span data-stu-id="8ca64-119">![Connect to Data Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account.png "Connect to Data Lake Store")</span></span>
3. <span data-ttu-id="8ca64-120">Bir geliştirme aşamasında olan Bağlayıcısı hakkında bir iletişim kutusu görürseniz, devam etmek için kabul et.</span><span class="sxs-lookup"><span data-stu-id="8ca64-120">If you see a dialog box about the connector being in a development phase, opt to continue.</span></span>
4. <span data-ttu-id="8ca64-121">İçinde **Microsoft Azure Data Lake Store** iletişim kutusu, Data Lake Store hesabınızın URL'sini girin ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="8ca64-121">In the **Microsoft Azure Data Lake Store** dialog box, provide the URL to your Data Lake Store account, and then click **OK**.</span></span>
   
    <span data-ttu-id="8ca64-122">![Data Lake Store için URL](./media/data-lake-store-power-bi/get-data-lake-store-account-url.png "Data Lake Store için URL")</span><span class="sxs-lookup"><span data-stu-id="8ca64-122">![URL for Data Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account-url.png "URL for Data Lake Store")</span></span>
5. <span data-ttu-id="8ca64-123">Sonraki iletişim kutusunda tıklatın **oturum** Data Lake Store dikkate imzalamak için.</span><span class="sxs-lookup"><span data-stu-id="8ca64-123">In the next dialog box, click **Sign in** to sign into Data Lake Store account.</span></span> <span data-ttu-id="8ca64-124">Kuruluşunuzun oturum açma sayfasına yönlendirilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8ca64-124">You will be redirected to your organization's sign in page.</span></span> <span data-ttu-id="8ca64-125">Hesaba imzalamak için istemleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="8ca64-125">Follow the prompts to sign into the account.</span></span>
   
    <span data-ttu-id="8ca64-126">![Data Lake Store içine oturum](./media/data-lake-store-power-bi/get-data-lake-store-account-signin.png "oturum Data Lake Store açın")</span><span class="sxs-lookup"><span data-stu-id="8ca64-126">![Sign into Data Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account-signin.png "Sign into Data Lake Store")</span></span>
6. <span data-ttu-id="8ca64-127">Başarıyla oturum açtıktan sonra tıklayın **Bağlan**.</span><span class="sxs-lookup"><span data-stu-id="8ca64-127">After you have successfully signed in, click **Connect**.</span></span>
   
    <span data-ttu-id="8ca64-128">![Data Lake Store'a bağlama](./media/data-lake-store-power-bi/get-data-lake-store-account-connect.png "Data Lake Store'a bağlama")</span><span class="sxs-lookup"><span data-stu-id="8ca64-128">![Connect to Data Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account-connect.png "Connect to Data Lake Store")</span></span>
7. <span data-ttu-id="8ca64-129">Sonraki iletişim kutusunda, Data Lake Store hesabınıza karşıya dosya gösterir.</span><span class="sxs-lookup"><span data-stu-id="8ca64-129">The next dialog box shows the file that you uploaded to your Data Lake Store account.</span></span> <span data-ttu-id="8ca64-130">Bilgileri doğrulayın ve ardından **yük**.</span><span class="sxs-lookup"><span data-stu-id="8ca64-130">Verify the info and then click **Load**.</span></span>
   
    <span data-ttu-id="8ca64-131">![Data Lake Deposu'ndan veri veri yükleme](./media/data-lake-store-power-bi/get-data-lake-store-account-load.png "veri Data Lake Deposu'ndan veri yükleme")</span><span class="sxs-lookup"><span data-stu-id="8ca64-131">![Load data from Data Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account-load.png "Load data from Data Lake Store")</span></span>
8. <span data-ttu-id="8ca64-132">Verileri Power BI başarıyla yüklendikten sonra aşağıdaki alanlarda görürsünüz **alanları** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="8ca64-132">After the data has been successfully loaded into Power BI, you will see the following fields in the **Fields** tab.</span></span>
   
    <span data-ttu-id="8ca64-133">![Alınan alanları](./media/data-lake-store-power-bi/imported-fields.png "içe alanlar")</span><span class="sxs-lookup"><span data-stu-id="8ca64-133">![Imported fields](./media/data-lake-store-power-bi/imported-fields.png "Imported fields")</span></span>
   
    <span data-ttu-id="8ca64-134">Ancak, görselleştirin ve verileri çözümlemek için biz verilerin aşağıdaki alanlar kullanılabilir tercih</span><span class="sxs-lookup"><span data-stu-id="8ca64-134">However, to visualize and analyze the data, we prefer the data to be available per the following fields</span></span>
   
    <span data-ttu-id="8ca64-135">![Alanları istenen](./media/data-lake-store-power-bi/desired-fields.png "alanları istenen")</span><span class="sxs-lookup"><span data-stu-id="8ca64-135">![Desired fields](./media/data-lake-store-power-bi/desired-fields.png "Desired fields")</span></span>
   
    <span data-ttu-id="8ca64-136">İçeri aktarılan verileri istediğiniz biçimde dönüştürmek üzere sorgu sonraki adımlarda güncelleştireceğiz.</span><span class="sxs-lookup"><span data-stu-id="8ca64-136">In the next steps, we will update the query to convert the imported data in the desired format.</span></span>
9. <span data-ttu-id="8ca64-137">Gelen **giriş** Şerit, tıklatın **Düzenle sorguları**.</span><span class="sxs-lookup"><span data-stu-id="8ca64-137">From the **Home** ribbon, click **Edit Queries**.</span></span>
   
    <span data-ttu-id="8ca64-138">![Sorguları düzenleme](./media/data-lake-store-power-bi/edit-queries.png "sorgularını düzenleme")</span><span class="sxs-lookup"><span data-stu-id="8ca64-138">![Edit queries](./media/data-lake-store-power-bi/edit-queries.png "Edit queries")</span></span>
10. <span data-ttu-id="8ca64-139">Sorgu Düzenleyicisi'nde, altında **içerik** sütun tıklatın **ikili**.</span><span class="sxs-lookup"><span data-stu-id="8ca64-139">In the Query Editor, under the **Content** column, click **Binary**.</span></span>
    
    <span data-ttu-id="8ca64-140">![Sorguları düzenleme](./media/data-lake-store-power-bi/convert-query1.png "sorgularını düzenleme")</span><span class="sxs-lookup"><span data-stu-id="8ca64-140">![Edit queries](./media/data-lake-store-power-bi/convert-query1.png "Edit queries")</span></span>
11. <span data-ttu-id="8ca64-141">Temsil eden bir dosya simgesini görürsünüz **Drivers.txt** karşıya dosya.</span><span class="sxs-lookup"><span data-stu-id="8ca64-141">You will see a file icon, that represents the **Drivers.txt** file that you uploaded.</span></span> <span data-ttu-id="8ca64-142">Dosyayı sağ tıklayın ve **CSV**.</span><span class="sxs-lookup"><span data-stu-id="8ca64-142">Right-click the file, and click **CSV**.</span></span>    
    
    <span data-ttu-id="8ca64-143">![Sorguları düzenleme](./media/data-lake-store-power-bi/convert-query2.png "sorgularını düzenleme")</span><span class="sxs-lookup"><span data-stu-id="8ca64-143">![Edit queries](./media/data-lake-store-power-bi/convert-query2.png "Edit queries")</span></span>
12. <span data-ttu-id="8ca64-144">Aşağıda gösterildiği gibi bir çıktı görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8ca64-144">You should see an output as shown below.</span></span> <span data-ttu-id="8ca64-145">Verilerinizi görsel öğeleri oluşturmak için kullanabileceğiniz bir biçimde kullanıma sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="8ca64-145">Your data is now available in a format that you can use to create visualizations.</span></span>
    
    <span data-ttu-id="8ca64-146">![Sorguları düzenleme](./media/data-lake-store-power-bi/convert-query3.png "sorgularını düzenleme")</span><span class="sxs-lookup"><span data-stu-id="8ca64-146">![Edit queries](./media/data-lake-store-power-bi/convert-query3.png "Edit queries")</span></span>
13. <span data-ttu-id="8ca64-147">Gelen **giriş** Şerit, tıklatın **kapatın ve geçerli**ve ardından **kapatın ve geçerli**.</span><span class="sxs-lookup"><span data-stu-id="8ca64-147">From the **Home** ribbon, click **Close and Apply**, and then click **Close and Apply**.</span></span>
    
    <span data-ttu-id="8ca64-148">![Sorguları düzenleme](./media/data-lake-store-power-bi/load-edited-query.png "sorgularını düzenleme")</span><span class="sxs-lookup"><span data-stu-id="8ca64-148">![Edit queries](./media/data-lake-store-power-bi/load-edited-query.png "Edit queries")</span></span>
14. <span data-ttu-id="8ca64-149">Sorgu güncelleştirildikten sonra **alanları** sekmesini görselleştirme için kullanılabilir yeni alanları gösterir.</span><span class="sxs-lookup"><span data-stu-id="8ca64-149">Once the query is updated, the **Fields** tab will show the new fields available for visualization.</span></span>
    
    <span data-ttu-id="8ca64-150">![Alanları güncelleştirilmiş](./media/data-lake-store-power-bi/updated-query-fields.png "alanları güncelleştirildi")</span><span class="sxs-lookup"><span data-stu-id="8ca64-150">![Updated fields](./media/data-lake-store-power-bi/updated-query-fields.png "Updated fields")</span></span>
15. <span data-ttu-id="8ca64-151">Bize her şehir için belirli bir ülke sürücüleri temsil etmek için bir pasta grafik oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8ca64-151">Let us create a pie chart to represent the drivers in each city for a given country.</span></span> <span data-ttu-id="8ca64-152">Bunu yapmak için aşağıdaki seçimleri yapın.</span><span class="sxs-lookup"><span data-stu-id="8ca64-152">To do so, make the following selections.</span></span>
    
    1. <span data-ttu-id="8ca64-153">Görselleştirmeleri sekmesinden pasta grafiği için simgeyi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="8ca64-153">From the Visualizations tab, click the symbol for a pie chart.</span></span>
       
        <span data-ttu-id="8ca64-154">![Pasta grafiği oluşturmak](./media/data-lake-store-power-bi/create-pie-chart.png "pasta grafik oluşturma")</span><span class="sxs-lookup"><span data-stu-id="8ca64-154">![Create pie chart](./media/data-lake-store-power-bi/create-pie-chart.png "Create pie chart")</span></span>
    2. <span data-ttu-id="8ca64-155">Biz kullanacaksanız sütunlar **sütun 4** (şehrin adı) ve **sütun 7** (ülke adı).</span><span class="sxs-lookup"><span data-stu-id="8ca64-155">The columns that we are going to use are **Column 4** (name of the city) and **Column 7** (name of the country).</span></span> <span data-ttu-id="8ca64-156">Bu sütunlardan sürükleyin **alanları** için sekme **görselleştirmeleri** sekmesinde aşağıda gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="8ca64-156">Drag these columns from **Fields** tab to **Visualizations** tab as shown below.</span></span>
       
        <span data-ttu-id="8ca64-157">![Görselleştirmelerinin](./media/data-lake-store-power-bi/create-visualizations.png "görselleştirmeler oluşturun")</span><span class="sxs-lookup"><span data-stu-id="8ca64-157">![Create visualizations](./media/data-lake-store-power-bi/create-visualizations.png "Create visualizations")</span></span>
    3. <span data-ttu-id="8ca64-158">Pasta grafik şimdi aşağıda gösterilene benzer benzemelidir.</span><span class="sxs-lookup"><span data-stu-id="8ca64-158">The pie chart should now resemble like the one shown below.</span></span>
       
        <span data-ttu-id="8ca64-159">![Pasta grafik](./media/data-lake-store-power-bi/pie-chart.png "görselleştirmeler oluşturun")</span><span class="sxs-lookup"><span data-stu-id="8ca64-159">![Pie chart](./media/data-lake-store-power-bi/pie-chart.png "Create visualizations")</span></span>
16. <span data-ttu-id="8ca64-160">Belirli bir ülkeye sayfa düzeyi filtreleri seçerek, her şehir seçilen ülkenin sürücüleri sayısını şimdi görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8ca64-160">By selecting a specific country from the page level filters, you can now see the number of drivers in each city of the selected country.</span></span> <span data-ttu-id="8ca64-161">Örneğin, altında **görselleştirmeleri** sekmesinde, altında **sayfa düzeyi filtreleri**seçin **Brezilya**.</span><span class="sxs-lookup"><span data-stu-id="8ca64-161">For example, under the **Visualizations** tab, under **Page level filters**, select **Brazil**.</span></span>
    
    <span data-ttu-id="8ca64-162">![Bir ülke seçin](./media/data-lake-store-power-bi/select-country.png "bir ülke seçin")</span><span class="sxs-lookup"><span data-stu-id="8ca64-162">![Select a country](./media/data-lake-store-power-bi/select-country.png "Select a country")</span></span>
17. <span data-ttu-id="8ca64-163">Pasta grafik Brezilya şehirlerde sürücüleri görüntülemek için otomatik olarak güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="8ca64-163">The pie chart is automatically updated to display the drivers in the cities of Brazil.</span></span>
    
    <span data-ttu-id="8ca64-164">![Sürücüleri bir ülkede](./media/data-lake-store-power-bi/driver-per-country.png "ülke başına sürücüleri")</span><span class="sxs-lookup"><span data-stu-id="8ca64-164">![Drivers in a country](./media/data-lake-store-power-bi/driver-per-country.png "Drivers per country")</span></span>
18. <span data-ttu-id="8ca64-165">Gelen **dosya** menüsünde tıklatın **kaydetmek** görselleştirme Power BI Desktop dosyası olarak kaydetmek için.</span><span class="sxs-lookup"><span data-stu-id="8ca64-165">From the **File** menu, click **Save** to save the visualization as a Power BI Desktop file.</span></span>

## <a name="publish-report-to-power-bi-service"></a><span data-ttu-id="8ca64-166">Rapor Power BI hizmetinde yayımlama</span><span class="sxs-lookup"><span data-stu-id="8ca64-166">Publish report to Power BI service</span></span>
<span data-ttu-id="8ca64-167">Power BI Desktop'ta görselleştirmeleri oluşturduktan sonra bunu başkalarıyla Power BI hizmetinde yayımlayarak paylaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8ca64-167">Once you have created the visualizations in Power BI Desktop, you can share it with others by publishing it to the Power BI service.</span></span> <span data-ttu-id="8ca64-168">Bunun hakkında daha fazla yönerge için bkz: [Power BI masaüstünden Yayımla](https://powerbi.microsoft.com/documentation/powerbi-desktop-upload-desktop-files/).</span><span class="sxs-lookup"><span data-stu-id="8ca64-168">For instructions on how to do that, see [Publish from Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-upload-desktop-files/).</span></span>

## <a name="see-also"></a><span data-ttu-id="8ca64-169">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="8ca64-169">See also</span></span>
* [<span data-ttu-id="8ca64-170">Data Lake Analytics kullanarak Data Lake Store içinde verileri analiz etme</span><span class="sxs-lookup"><span data-stu-id="8ca64-170">Analyze data in Data Lake Store using Data Lake Analytics</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)

