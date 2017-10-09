---
<span data-ttu-id="087f4-101">Başlık: aaa "Azure Analysis Services öğretici Ders 11: roller oluşturma | Microsoft Docs"Açıklama: Azure Analysis Services öğretici proje toocreate rollerinde nasıl hello açıklar.</span><span class="sxs-lookup"><span data-stu-id="087f4-101">title: aaa"Azure Analysis Services tutorial lesson 11: Create roles | Microsoft Docs" description: Describes how toocreate roles in hello Azure Analysis Services tutorial project.</span></span> <span data-ttu-id="087f4-102">Hizmetleri: analysis services documentationcenter: '' Yazar: minewiskan Yöneticisi: erikre Düzenleyicisi: '' etiketler: ''</span><span class="sxs-lookup"><span data-stu-id="087f4-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="087f4-103">MS.assetid: ms.service: analysis services ms.devlang: NA ms.topic: get-makalesi ms.tgt_pltfrm: NA ms.workload: na ms.date: 26/05/2017 ms.author: owend</span><span class="sxs-lookup"><span data-stu-id="087f4-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span></span>
---
# <a name="lesson-11-create-roles"></a><span data-ttu-id="087f4-104">11. Ders: Rol oluşturma</span><span class="sxs-lookup"><span data-stu-id="087f4-104">Lesson 11: Create roles</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="087f4-105">Bu derste rol oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="087f4-105">In this lesson, you create roles.</span></span> <span data-ttu-id="087f4-106">Rolleri model veritabanı nesnesi ve veri güvenliği erişim tooonly sınırlayarak Rol üyeleri olan kullanıcılarla sağlar.</span><span class="sxs-lookup"><span data-stu-id="087f4-106">Roles provide model database object and data security by limiting access tooonly those users that are role members.</span></span> <span data-ttu-id="087f4-107">Her rol tek bir izinle tanımlanır: Hiçbiri, Okuma, Okuma ve İşlem, İşlem veya Yönetici.</span><span class="sxs-lookup"><span data-stu-id="087f4-107">Each role is defined with a single permission: None, Read, Read and Process, Process, or Administrator.</span></span> <span data-ttu-id="087f4-108">Roller, Rol Yöneticisi kullanılarak model yazma sırasında tanımlanabilir.</span><span class="sxs-lookup"><span data-stu-id="087f4-108">Roles can be defined during model authoring by using Role Manager.</span></span> <span data-ttu-id="087f4-109">Bir model dağıtıldıktan sonra SQL Server Management Studio’yu (SSMS) kullanarak rolleri yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="087f4-109">After a model has been deployed, you can manage roles by using SQL Server Management Studio (SSMS).</span></span> <span data-ttu-id="087f4-110">toolearn daha, fazla [rolleri](https://docs.microsoft.com/sql/analysis-services/tabular-models/roles-ssas-tabular).</span><span class="sxs-lookup"><span data-stu-id="087f4-110">toolearn more, see [Roles](https://docs.microsoft.com/sql/analysis-services/tabular-models/roles-ssas-tabular).</span></span>
  
> [!NOTE]  
> <span data-ttu-id="087f4-111">Roller oluşturma gerekli toocomplete bu öğreticidir.</span><span class="sxs-lookup"><span data-stu-id="087f4-111">Creating roles is not necessary toocomplete this tutorial.</span></span> <span data-ttu-id="087f4-112">Varsayılan olarak, hello hesabı ile oturum açmış olduğunuz hello model üzerinde yönetici ayrıcalıklarına sahip.</span><span class="sxs-lookup"><span data-stu-id="087f4-112">By default, hello account you are currently logged in with has Administrator privileges on hello model.</span></span> <span data-ttu-id="087f4-113">Ancak, raporlama istemcisi kullanarak, kuruluş toobrowse diğer kullanıcılar için en az bir rol ile Okuma izinleri oluşturun ve bu kullanıcıların üye olarak eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="087f4-113">However, for other users in your organization toobrowse by using a reporting client, you must create at least one role with Read permissions and add those users as members.</span></span>  
  
<span data-ttu-id="087f4-114">Üç rol oluşturursunuz:</span><span class="sxs-lookup"><span data-stu-id="087f4-114">You create three roles:</span></span>  
  
-   <span data-ttu-id="087f4-115">**Satış Yöneticisi** – bu rol, istediğiniz toohave okuma izni tooall model nesneleri ve veri, kuruluşunuzdaki kullanıcılar içerebilir.</span><span class="sxs-lookup"><span data-stu-id="087f4-115">**Sales Manager** – This role can include users in your organization for which you want toohave Read permission tooall model objects and data.</span></span>  
  
-   <span data-ttu-id="087f4-116">**Satış analist ABD** – bu rol yalnızca toobe mümkün toobrowse verileri istediğiniz, kuruluşunuzdaki kullanıcılar içerebilir ilgili hello Amerika Birleşik Devletleri toosales.</span><span class="sxs-lookup"><span data-stu-id="087f4-116">**Sales Analyst US** – This role can include users in your organization for which you want only toobe able toobrowse data related toosales in hello United States.</span></span> <span data-ttu-id="087f4-117">Bu rol için bir DAX formülü toodefine kullanmak bir *satır filtresi*, üyeleri yalnızca hello Amerika Birleşik Devletleri toobrowse verilerini kısıtlar.</span><span class="sxs-lookup"><span data-stu-id="087f4-117">For this role, you use a DAX formula toodefine a *Row Filter*, which restricts members toobrowse data only for hello United States.</span></span>  
  
-   <span data-ttu-id="087f4-118">**Yönetici** – bu rol, sınırsız erişim ve izinleri tooperform yönetim görevlerini hello model veritabanını verir toohave yönetici izni istediğiniz kullanıcıları içerebilir.</span><span class="sxs-lookup"><span data-stu-id="087f4-118">**Administrator** – This role can include users for which you want toohave Administrator permission, which allows unlimited access and permissions tooperform administrative tasks on hello model database.</span></span>  
  
<span data-ttu-id="087f4-119">Kuruluşunuzdaki Windows kullanıcı ve grup hesaplarını benzersiz olduğundan, belirli kuruluş toomembers hesapları ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="087f4-119">Because Windows user and group accounts in your organization are unique, you can add accounts from your particular organization toomembers.</span></span> <span data-ttu-id="087f4-120">Ancak, Bu öğretici için aynı zamanda hello üyeleri boş bırakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="087f4-120">However, for this tutorial, you can also leave hello members blank.</span></span> <span data-ttu-id="087f4-121">Daha sonra Ders 12'de her rol hello etkisini test edin: Excel'de Çözümle.</span><span class="sxs-lookup"><span data-stu-id="087f4-121">You test hello effect of each role later in Lesson 12: Analyze in Excel.</span></span>  
  
<span data-ttu-id="087f4-122">Bu ders zaman toocomplete tahmini: **15 dakika**</span><span class="sxs-lookup"><span data-stu-id="087f4-122">Estimated time toocomplete this lesson: **15 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="087f4-123">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="087f4-123">Prerequisites</span></span>  
<span data-ttu-id="087f4-124">Bu konu, sırayla tamamlanması gereken bir tablo modelleme öğreticisinin bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="087f4-124">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="087f4-125">Bu ders Hello görevleri gerçekleştirmeden önce hello önceki Ders tamamlandı: [Ders 10: bölümleri oluşturma](../tutorials/aas-lesson-10-create-partitions.md).</span><span class="sxs-lookup"><span data-stu-id="087f4-125">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 10: Create partitions](../tutorials/aas-lesson-10-create-partitions.md).</span></span>  
  
## <a name="create-roles"></a><span data-ttu-id="087f4-126">Rol oluşturma</span><span class="sxs-lookup"><span data-stu-id="087f4-126">Create roles</span></span>  
  
#### <a name="toocreate-a-sales-manager-user-role"></a><span data-ttu-id="087f4-127">toocreate satış yöneticisi kullanıcı rolü</span><span class="sxs-lookup"><span data-stu-id="087f4-127">toocreate a Sales Manager user role</span></span>  
  
1.  <span data-ttu-id="087f4-128">Tablo Model Gezgini'nde **Roller** > **Roller**’e sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="087f4-128">In Tabular Model Explorer, right-click **Roles** > **Roles**.</span></span>  
  
2.  <span data-ttu-id="087f4-129">Rol Yöneticisi'nde **Yeni**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="087f4-129">In Role Manager, click **New**.</span></span>  
  
3.  <span data-ttu-id="087f4-130">Merhaba yeni rolüne tıklayın ve ardından hello **adı** sütun hello rol çok yeniden adlandırma**Satış Yöneticisi**.</span><span class="sxs-lookup"><span data-stu-id="087f4-130">Click hello new role, and then in hello **Name** column, rename hello role too**Sales Manager**.</span></span>  
  
4.  <span data-ttu-id="087f4-131">Merhaba, **izinleri** sütunu hello açılır listeye tıklayın ve ardından hello seçin **okuma** izni.</span><span class="sxs-lookup"><span data-stu-id="087f4-131">In hello **Permissions** column, click hello dropdown list, and then select hello **Read** permission.</span></span> 

    ![aas-lesson11-new-role](../tutorials/media/aas-lesson11-new-role.png) 
  
5.  <span data-ttu-id="087f4-133">İsteğe bağlı: Tıklatın hello **üyeleri** sekmesini ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="087f4-133">Optional: Click hello **Members** tab, and then click **Add**.</span></span> <span data-ttu-id="087f4-134">Merhaba, **kullanıcıları veya Grupları Seç** iletişim kutusunda, hello Windows kullanıcıları veya grupları girin kuruluşunuzdan hello rolündeki tooinclude istiyor.</span><span class="sxs-lookup"><span data-stu-id="087f4-134">In hello **Select Users or Groups** dialog box, enter hello Windows users or groups from your organization you want tooinclude in hello role.</span></span>  
  
#### <a name="toocreate-a-sales-analyst-us-user-role"></a><span data-ttu-id="087f4-135">toocreate satış analisti ABD kullanıcı rolü</span><span class="sxs-lookup"><span data-stu-id="087f4-135">toocreate a Sales Analyst US user role</span></span>  
  
1.  <span data-ttu-id="087f4-136">Rol Yöneticisi'nde **Yeni**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="087f4-136">In Role Manager, click **New**.</span></span>    
  
2.  <span data-ttu-id="087f4-137">Merhaba rol çok yeniden adlandırma**satış analist ABD**.</span><span class="sxs-lookup"><span data-stu-id="087f4-137">Rename hello role too**Sales Analyst US**.</span></span>  
  
3.  <span data-ttu-id="087f4-138">Bu role **Okuma** izni verin.</span><span class="sxs-lookup"><span data-stu-id="087f4-138">Give this role **Read** permission.</span></span>  
  
4.  <span data-ttu-id="087f4-139">Merhaba satır filtreler sekmesine tıklayın ve ardından hello **DimGeography** hello DAX filtre sütununda formülü aşağıdaki türü hello yalnızca, tablo:</span><span class="sxs-lookup"><span data-stu-id="087f4-139">Click hello Row Filters tab, and then for hello **DimGeography** table only, in hello DAX Filter column, type hello following formula:</span></span>  
  
    ```Administrator
    =DimGeography[CountryRegionCode] = "US" 
    ```
    
    <span data-ttu-id="087f4-140">Bir satır Filtresi Formülü tooa Boole (TRUE/FALSE) değeri çözmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="087f4-140">A Row Filter formula must resolve tooa Boolean (TRUE/FALSE) value.</span></span> <span data-ttu-id="087f4-141">Bu formülü ile yalnızca "ABD" Merhaba ülke/bölge kodu değeri ile satırları görünür toohello kullanıcı olduğunu belirtiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="087f4-141">With this formula, you are specifying that only rows with hello Country Region Code value of “US” are visible toohello user.</span></span>  
    ![aas-lesson11-role-filter](../tutorials/media/aas-lesson11-role-filter.png) 
  
6.  <span data-ttu-id="087f4-143">İsteğe bağlı: Tıklatın hello **üyeleri** sekmesini ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="087f4-143">Optional: Click hello **Members** tab, and then click **Add**.</span></span> <span data-ttu-id="087f4-144">Merhaba, **kullanıcıları veya Grupları Seç** iletişim kutusunda, hello Windows kullanıcıları veya grupları girin kuruluşunuzdan hello rolündeki tooinclude istiyor.</span><span class="sxs-lookup"><span data-stu-id="087f4-144">In hello **Select Users or Groups** dialog box, enter hello Windows users or groups from your organization you want tooinclude in hello role.</span></span>  
  
#### <a name="toocreate-an-administrator-user-role"></a><span data-ttu-id="087f4-145">toocreate bir yönetici kullanıcı rolü</span><span class="sxs-lookup"><span data-stu-id="087f4-145">toocreate an Administrator user role</span></span>  
  
1.  <span data-ttu-id="087f4-146">**Yeni**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="087f4-146">Click **New**.</span></span>  
  
2.  <span data-ttu-id="087f4-147">Merhaba rol çok yeniden adlandırma**yönetici**.</span><span class="sxs-lookup"><span data-stu-id="087f4-147">Rename hello role too**Administrator**.</span></span>  
  
3.  <span data-ttu-id="087f4-148">Bu role **Yönetici** izni verin.</span><span class="sxs-lookup"><span data-stu-id="087f4-148">Give this role **Administrator** permission.</span></span>  
  
4.  <span data-ttu-id="087f4-149">İsteğe bağlı: Tıklatın hello **üyeleri** sekmesini ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="087f4-149">Optional: Click hello **Members** tab, and then click **Add**.</span></span> <span data-ttu-id="087f4-150">Merhaba, **kullanıcıları veya Grupları Seç** iletişim kutusunda, hello Windows kullanıcıları veya grupları girin kuruluşunuzdan hello rolündeki tooinclude istiyor.</span><span class="sxs-lookup"><span data-stu-id="087f4-150">In hello **Select Users or Groups** dialog box, enter hello Windows users or groups from your organization you want tooinclude in hello role.</span></span> 
  
  
## <a name="whats-next"></a><span data-ttu-id="087f4-151">Sırada ne var?</span><span class="sxs-lookup"><span data-stu-id="087f4-151">What's next?</span></span>
<span data-ttu-id="087f4-152">[12. Ders: Excel’de çözümleme](../tutorials/aas-lesson-12-analyze-in-excel.md).</span><span class="sxs-lookup"><span data-stu-id="087f4-152">[Lesson 12: Analyze in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md).</span></span>

  
  
