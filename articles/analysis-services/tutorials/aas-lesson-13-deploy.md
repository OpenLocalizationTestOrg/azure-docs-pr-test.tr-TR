---
<span data-ttu-id="bd714-101">Başlık: aaa "Azure Analysis Services öğretici Ders 13: dağıtma | Microsoft Docs"Açıklama: nasıl toodeploy hello öğretici proje tooAzure Analysis Services açıklar.</span><span class="sxs-lookup"><span data-stu-id="bd714-101">title: aaa"Azure Analysis Services tutorial lesson 13: Deploy | Microsoft Docs" description:  Describes how toodeploy hello tutorial project tooAzure Analysis Services.</span></span>
<span data-ttu-id="bd714-102">Hizmetleri: analysis services documentationcenter: '' Yazar: minewiskan Yöneticisi: erikre Düzenleyicisi: '' etiketler: ''</span><span class="sxs-lookup"><span data-stu-id="bd714-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="bd714-103">MS.assetid: ms.service: analysis services ms.devlang: NA ms.topic: get-makalesi ms.tgt_pltfrm: NA ms.workload: na ms.date: 07/17/2017 ms.author: owend</span><span class="sxs-lookup"><span data-stu-id="bd714-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 07/17/2017 ms.author: owend</span></span>
---
# <a name="lesson-13-deploy"></a><span data-ttu-id="bd714-104">13. Ders: Dağıtma</span><span class="sxs-lookup"><span data-stu-id="bd714-104">Lesson 13: Deploy</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="bd714-105">Bu alıştırmanın ilerisinde dağıtım özelliklerini yapılandırın; bir Azure Analysis Services sunucusu toodeploy tooand hello modeli için bir ad belirtme.</span><span class="sxs-lookup"><span data-stu-id="bd714-105">In this lesson, you configure deployment properties; specifying an Azure Analysis Services server toodeploy tooand a name for hello model.</span></span> <span data-ttu-id="bd714-106">Merhaba model toothat örneğini dağıtırsınız.</span><span class="sxs-lookup"><span data-stu-id="bd714-106">You then deploy hello model toothat instance.</span></span> <span data-ttu-id="bd714-107">Model dağıtıldıktan sonra kullanıcılar bir raporlama istemci uygulaması kullanarak tooit bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="bd714-107">After your model is deployed, users can connect tooit by using a reporting client application.</span></span> <span data-ttu-id="bd714-108">toolearn daha, fazla [tooAzure Analysis Services dağıtma](https://docs.microsoft.com/azure/analysis-services/analysis-services-deploy).</span><span class="sxs-lookup"><span data-stu-id="bd714-108">toolearn more, see [Deploy tooAzure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-deploy).</span></span>  
  
<span data-ttu-id="bd714-109">Bu ders zaman toocomplete tahmini: **5 dakika**</span><span class="sxs-lookup"><span data-stu-id="bd714-109">Estimated time toocomplete this lesson: **5 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="bd714-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="bd714-110">Prerequisites</span></span>  
<span data-ttu-id="bd714-111">Bu konu, sırayla tamamlanması gereken bir tablo modelleme öğreticisinin bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="bd714-111">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="bd714-112">Bu ders Hello görevleri gerçekleştirmeden önce hello önceki Ders tamamlandı: [Ders 12: Excel'de Çözümle özelliğini](../tutorials/aas-lesson-12-analyze-in-excel.md).</span><span class="sxs-lookup"><span data-stu-id="bd714-112">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 12: Analyze in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md).</span></span>  

> [!IMPORTANT]  
> <span data-ttu-id="bd714-113">Bilmeniz gereken [yönetici izinleri](../analysis-services-server-admins.md) üzerinde hello uzak Analysis Services sunucusu sıralı toodeploy tooit.</span><span class="sxs-lookup"><span data-stu-id="bd714-113">You must have [Administrator permissions](../analysis-services-server-admins.md) on hello remote Analysis Services server in-order toodeploy tooit.</span></span>  

> [!IMPORTANT]  
> <span data-ttu-id="bd714-114">Bir şirket içi SQL sunucusunda hello AdventureWorksDW2014 örnek veritabanı yüklediyseniz ve model tooan Azure Analysis Services sunucusuna dağıtıyorsunuz bir [şirket içi veri ağ geçidi](../analysis-services-gateway.md) gereklidir.</span><span class="sxs-lookup"><span data-stu-id="bd714-114">If you installed hello AdventureWorksDW2014 sample database on an on-premises SQL Server, and you're deploying your model tooan Azure Analysis Services server, an [On-premises data gateway](../analysis-services-gateway.md) is required.</span></span>
  
## <a name="deploy-hello-model"></a><span data-ttu-id="bd714-115">Merhaba model dağıtma</span><span class="sxs-lookup"><span data-stu-id="bd714-115">Deploy hello model</span></span>  
  
#### <a name="tooconfigure-deployment-properties"></a><span data-ttu-id="bd714-116">tooconfigure dağıtım özellikleri</span><span class="sxs-lookup"><span data-stu-id="bd714-116">tooconfigure deployment properties</span></span>  

  
1.  <span data-ttu-id="bd714-117">İçinde **Çözüm Gezgini**, sağ hello **AW Internet satış** proje ve ardından **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="bd714-117">In **Solution Explorer**, right-click hello **AW Internet Sales** project, and then click **Properties**.</span></span>  
  
2.  <span data-ttu-id="bd714-118">Merhaba, **AW Internet satış özellik sayfaları** iletişim kutusunda **dağıtım sunucusu**, hello içinde **Server** özelliği, hello tam sunucu girin.</span><span class="sxs-lookup"><span data-stu-id="bd714-118">In hello **AW Internet Sales Property Pages** dialog box, under **Deployment Server**, in hello **Server** property, enter hello full server.</span></span>  

    ![aas-lesson13-deploy-property](../tutorials/media/aas-lesson13-deploy-property.png)
  
3.  <span data-ttu-id="bd714-120">Merhaba, **veritabanı** özelliği, türü **Adventure Works Internet satış**.</span><span class="sxs-lookup"><span data-stu-id="bd714-120">In hello **Database** property, type **Adventure Works Internet Sales**.</span></span>  
  
4.  <span data-ttu-id="bd714-121">Merhaba, **Model adı** özelliği, türü **Adventure Works Internet satış modeli**.</span><span class="sxs-lookup"><span data-stu-id="bd714-121">In hello **Model Name** property, type **Adventure Works Internet Sales Model**.</span></span>  
  
5.  <span data-ttu-id="bd714-122">Seçimlerinizi doğrulayıp **Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bd714-122">Verify your selections and then click **OK**.</span></span>  
  
#### <a name="toodeploy-hello-adventure-works-internet-sales"></a><span data-ttu-id="bd714-123">toodeploy hello Adventure Works Internet satış</span><span class="sxs-lookup"><span data-stu-id="bd714-123">toodeploy hello Adventure Works Internet Sales</span></span>
  
1.  <span data-ttu-id="bd714-124">İçinde **Çözüm Gezgini**, sağ hello **AW Internet satış** Proje > **yapı**.</span><span class="sxs-lookup"><span data-stu-id="bd714-124">In **Solution Explorer**, right-click hello **AW Internet Sales** project > **Build**.</span></span>  

2.  <span data-ttu-id="bd714-125">Sağ hello **AW Internet satış** Proje > **dağıtma**.</span><span class="sxs-lookup"><span data-stu-id="bd714-125">Right-click hello **AW Internet Sales** project > **Deploy**.</span></span>

    <span data-ttu-id="bd714-126">TooAzure Analysis Services dağıtırken, olabilir istendiğinde tooenter hesabınızın olması.</span><span class="sxs-lookup"><span data-stu-id="bd714-126">When deploying tooAzure Analysis Services, you may be prompted tooenter your account.</span></span> <span data-ttu-id="bd714-127">Kuruluş hesabınızı ve parolanızı girin, örneğin nancy@adventureworks.com. Bu hesap Admins hello sunucuda olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="bd714-127">Enter your organizational account and password, for example nancy@adventureworks.com. This account must be in Admins on hello server.</span></span>
  
    <span data-ttu-id="bd714-128">Merhaba Dağıt iletişim kutusu görünür ve başlangıç dağıtım durumu hello meta verilerin ve hello modele dahil her bir tablo görüntüler.</span><span class="sxs-lookup"><span data-stu-id="bd714-128">hello Deploy dialog box appears and displays hello deployment status of hello metadata and each table included in hello model.</span></span>  
    
    ![aas-lesson13-deploy-status](../tutorials/media/aas-lesson13-deploy-status.png)
  
3. <span data-ttu-id="bd714-130">Dağıtım başarıyla tamamlandığında devam edin ve **Kapat**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bd714-130">When deployment successfully completes, go ahead and click **Close**.</span></span>  
  
## <a name="conclusion"></a><span data-ttu-id="bd714-131">Sonuç</span><span class="sxs-lookup"><span data-stu-id="bd714-131">Conclusion</span></span>  
<span data-ttu-id="bd714-132">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="bd714-132">Congratulations!</span></span> <span data-ttu-id="bd714-133">İlk Analysis Services Tablo modelinizi yazma ve dağıtma işlemini tamamladınız.</span><span class="sxs-lookup"><span data-stu-id="bd714-133">You're finished authoring and deploying your first Analysis Services Tabular model.</span></span> <span data-ttu-id="bd714-134">Bu öğretici, tablolu model oluşturma hello en yaygın görevleri tamamlama aracılığıyla Kılavuzu Yardım.</span><span class="sxs-lookup"><span data-stu-id="bd714-134">This tutorial has helped guide you through completing hello most common tasks in creating a tabular model.</span></span> <span data-ttu-id="bd714-135">Adventure Works Internet satış modelinizi dağıtılır, SQL Server Management Studio toomanage hello modelini kullanabilirsiniz; işlem komut dosyaları ve bir yedekleme planı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="bd714-135">Now that your Adventure Works Internet Sales model is deployed, you can use SQL Server Management Studio toomanage hello model; create process scripts and a backup plan.</span></span> <span data-ttu-id="bd714-136">Kullanıcılar artık Microsoft Excel veya Power BI gibi bir raporlama istemci uygulaması kullanarak toohello modeli bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="bd714-136">Users can also now connect toohello model using a reporting client application such as Microsoft Excel or Power BI.</span></span>  

![aas-lesson13-ssms](../tutorials/media/aas-lesson13-ssms.png)
  
  
  
## <a name="whats-next"></a><span data-ttu-id="bd714-138">Sırada ne var?</span><span class="sxs-lookup"><span data-stu-id="bd714-138">What's next?</span></span>
<span data-ttu-id="bd714-139">[Power BI Desktop ile bağlanma](../analysis-services-connect-pbi.md) </span><span class="sxs-lookup"><span data-stu-id="bd714-139">[Connect with Power BI Desktop](../analysis-services-connect-pbi.md) </span></span>  
<span data-ttu-id="bd714-140">[Ek Ders - Dinamik güvenlik](../tutorials/aas-supplemental-lesson-dynamic-security.md) </span><span class="sxs-lookup"><span data-stu-id="bd714-140">[Supplemental Lesson - Dynamic security](../tutorials/aas-supplemental-lesson-dynamic-security.md) </span></span>  
<span data-ttu-id="bd714-141">[Ek Ders - Ayrıntı satırları](../tutorials/aas-supplemental-lesson-detail-rows.md) </span><span class="sxs-lookup"><span data-stu-id="bd714-141">[Supplemental Lesson - Detail rows](../tutorials/aas-supplemental-lesson-detail-rows.md) </span></span>  
[<span data-ttu-id="bd714-142">Ek Ders - Düzensiz hiyerarşiler</span><span class="sxs-lookup"><span data-stu-id="bd714-142">Supplemental Lesson - Ragged hierarchies</span></span>](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)   
