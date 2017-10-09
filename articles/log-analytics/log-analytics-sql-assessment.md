---
title: "aaaOptimize Azure günlük analizi ile SQL Server ortamınızın | Microsoft Docs"
description: "Azure günlük analizi ile Merhaba SQL çözüm tooassess risk ve SQL server ortamlarınızın durumunu düzenli aralıklarla hello değerlendirme kullanabilirsiniz."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: e297eb57-1718-4cfe-a241-b9e84b2c42ac
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f31326d8cdad3ef5d5a190614d1a18c1dac826ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-your-sql-server-environment-with-hello-sql-assessment-solution-in-log-analytics"></a><span data-ttu-id="ea2d4-103">SQL Server ortamınızın hello SQL değerlendirmesi çözümde günlük analizi ile en iyi duruma getirme</span><span class="sxs-lookup"><span data-stu-id="ea2d4-103">Optimize your SQL Server environment with hello SQL Assessment solution in Log Analytics</span></span>

![SQL değerlendirmesi simgesi](./media/log-analytics-sql-assessment/sql-assessment-symbol.png)

<span data-ttu-id="ea2d4-105">Merhaba SQL çözüm tooassess risk ve sunucu ortamlarınızın durumunu düzenli aralıklarla hello değerlendirme kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-105">You can use hello SQL Assessment solution tooassess hello risk and health of your server environments on a regular interval.</span></span> <span data-ttu-id="ea2d4-106">Bu makalede, olası sorunlar için düzeltme eylemleri yararlanabilmeniz hello çözüm yüklemenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-106">This article will help you install hello solution so that you can take corrective actions for potential problems.</span></span>

<span data-ttu-id="ea2d4-107">Bu çözüm önerileri belirli tooyour dağıtılan sunucu altyapısı öncelikli listesi sağlar.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-107">This solution provides a prioritized list of recommendations specific tooyour deployed server infrastructure.</span></span> <span data-ttu-id="ea2d4-108">Merhaba önerileri hızla yardımcı alanları risk hello ve düzeltici işlemleri anlamak altı odak arasında ayrılır.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-108">hello recommendations are categorized across six focus areas which help you quickly understand hello risk and take corrective action.</span></span>

<span data-ttu-id="ea2d4-109">Merhaba önerilerin hello bilgi ve müşteri ziyaretleriniz binlerce Microsoft mühendisleri tarafından elde edilen deneyimlerden dayanır.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-109">hello recommendations made are based on hello knowledge and experience gained by Microsoft engineers from thousands of customer visits.</span></span> <span data-ttu-id="ea2d4-110">Her bir öneri, bir sorun tooyou neden önemli ve nasıl tooimplement hello değişiklikleri önerilen hakkında rehberlik sağlar.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-110">Each recommendation provides guidance about why an issue might matter tooyou and how tooimplement hello suggested changes.</span></span>

<span data-ttu-id="ea2d4-111">En önemli tooyour kuruluş ve ücretsiz ve sağlam bir risk ortam çalıştıran doğru ilerleme durumunuzu izlemenize odak alanlarına seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-111">You can choose focus areas that are most important tooyour organization and track your progress toward running a risk free and healthy environment.</span></span>

<span data-ttu-id="ea2d4-112">Merhaba çözüm ekledik ve bir değerlendirme tamamlanan, Özet sonra bilgi odak alanlarına odaklanmak için hello üzerinde gösterilen **SQL değerlendirmesi** Panosu ortamınızdaki hello altyapısını için.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-112">After you've added hello solution and an assessment is completed, summary information for focus areas is shown on hello **SQL Assessment** dashboard for hello infrastructure in your environment.</span></span> <span data-ttu-id="ea2d4-113">Merhaba aşağıdaki nasıl toouse hello hello hakkında bilgi bölümlerde **SQL değerlendirmesi** Pano, burada görüntüleyebilir ve ardından uygulayın Eylemler SQL server altyapınızı için önerilir.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-113">hello following sections describe how toouse hello information on hello **SQL Assessment** dashboard, where you can view and then take recommended actions for your SQL server infrastructure.</span></span>

![SQL değerlendirmesi döşeme görüntüsü](./media/log-analytics-sql-assessment/sql-assess-tile.png)

![SQL değerlendirmesi Pano görüntüsü](./media/log-analytics-sql-assessment/sql-assess-dash.png)

## <a name="installing-and-configuring-hello-solution"></a><span data-ttu-id="ea2d4-116">Yükleme ve yapılandırma hello çözümü</span><span class="sxs-lookup"><span data-stu-id="ea2d4-116">Installing and configuring hello solution</span></span>
<span data-ttu-id="ea2d4-117">SQL Server hello standart, Developer ve Enterprise sürümleri için şu anda desteklenen tüm sürümleri ile SQL değerlendirmesi çalışır.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-117">SQL Assessment works with all currently supported versions of SQL Server for hello Standard, Developer, and Enterprise editions.</span></span>

<span data-ttu-id="ea2d4-118">Bilgi tooinstall aşağıdaki hello kullanın ve hello çözüm yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-118">Use hello following information tooinstall and configure hello solution.</span></span>

* <span data-ttu-id="ea2d4-119">Aracıları SQL Server'ın yüklü olması sunucularda yüklü olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-119">Agents must be installed on servers that have SQL Server installed.</span></span>
* <span data-ttu-id="ea2d4-120">Hello SQL değerlendirme çözümü bir OMS aracısı olan her bilgisayarda yüklü .NET Framework 4'ün desteklenen bir sürümünü gerektirir.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-120">hello SQL Assessment solution requires a supported version of .NET Framework 4 installed on each computer that has an OMS agent.</span></span>
* <span data-ttu-id="ea2d4-121">Kullanarak hello Azure portal sipariş tooinstall hello çözümde hello kullanıcı bir yönetici veya katkıda toohello Azure aboneliğiniz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-121">In order tooinstall hello solution, hello user must be an administrator or contributor toohello Azure subscription when using hello Azure portal.</span></span> <span data-ttu-id="ea2d4-122">Ayrıca, hello kullanıcı rolünün bir üyesi hello OMS çalışma katkıda bulunan veya yönetici hello OMS portalında olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-122">In addition, hello user must be a member of hello OMS workspace contributor or administrator role in hello OMS portal.</span></span>
* <span data-ttu-id="ea2d4-123">Merhaba Operations Manager aracısı SQL değerlendirmesi ile kullanırken, toouse bir Operations Manager Run-As hesabı gerekir.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-123">When using hello Operations Manager agent with SQL Assessment, you'll need toouse an Operations Manager Run-As account.</span></span> <span data-ttu-id="ea2d4-124">Bkz: [Operations Manager Çalıştır hesapları için OMS](#operations-manager-run-as-accounts-for-oms) altında daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-124">See [Operations Manager run-as accounts for OMS](#operations-manager-run-as-accounts-for-oms) below for more information.</span></span>

  > [!NOTE]
  > <span data-ttu-id="ea2d4-125">Merhaba MMA aracı Operations Manager Run-As hesaplarını desteklemez.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-125">hello MMA agent does not support Operations Manager Run-As accounts.</span></span>
  >
  >
* <span data-ttu-id="ea2d4-126">Merhaba işlemi kullanarak OMS çalışma açıklanan hello SQL değerlendirme çözümü tooyour eklemek [hello Çözümleri Galerisi eklemek günlük analizi çözümleri](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="ea2d4-126">Add hello SQL Assessment solution tooyour OMS workspace using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span> <span data-ttu-id="ea2d4-127">Başka bir yapılandırma işlemi gerekmez.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-127">There is no further configuration required.</span></span>

> [!NOTE]
> <span data-ttu-id="ea2d4-128">Merhaba çözüm ekledikten sonra hello AdvisorAssessment.exe dosyası tooservers aracılarıyla eklenir.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-128">After you've added hello solution, hello AdvisorAssessment.exe file is added tooservers with agents.</span></span> <span data-ttu-id="ea2d4-129">Yapılandırma verilerini okuma ve işleme hello bulutta toohello OMS hizmetine gönderilir.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-129">Configuration data is read and then sent toohello OMS service in hello cloud for processing.</span></span> <span data-ttu-id="ea2d4-130">Mantığı uygulanan toohello alınan veri ve hello bulut hizmeti hello verilerini kaydeder.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-130">Logic is applied toohello received data and hello cloud service records hello data.</span></span>

## <a name="sql-assessment-data-collection-details"></a><span data-ttu-id="ea2d4-131">SQL değerlendirmesi veri toplama ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="ea2d4-131">SQL Assessment data collection details</span></span>
<span data-ttu-id="ea2d4-132">SQL değerlendirmesi WMI verilerini, kayıt defteri verilerini, performans verilerini ve etkinleştirdiğiniz hello aracıları kullanarak SQL Server dinamik yönetim görünümünü sonuçları toplar.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-132">SQL Assessment collects WMI data, registry data, performance data, and SQL Server dynamic management view results using hello agents that you have enabled.</span></span>

<span data-ttu-id="ea2d4-133">Merhaba aşağıdaki tabloda veri toplama yöntemleri aracılar için Operations Manager (SCOM) gerekli olup olmadığını ve nasıl gösterilmektedir genellikle veri bir aracı tarafından toplanır.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-133">hello following table shows data collection methods for agents, whether Operations Manager (SCOM) is required, and how often data is collected by an agent.</span></span>

| <span data-ttu-id="ea2d4-134">Platform</span><span class="sxs-lookup"><span data-stu-id="ea2d4-134">platform</span></span> | <span data-ttu-id="ea2d4-135">Doğrudan Aracısı</span><span class="sxs-lookup"><span data-stu-id="ea2d4-135">Direct Agent</span></span> | <span data-ttu-id="ea2d4-136">SCOM Aracısı</span><span class="sxs-lookup"><span data-stu-id="ea2d4-136">SCOM agent</span></span> | <span data-ttu-id="ea2d4-137">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="ea2d4-137">Azure Storage</span></span> | <span data-ttu-id="ea2d4-138">SCOM gerekli?</span><span class="sxs-lookup"><span data-stu-id="ea2d4-138">SCOM required?</span></span> | <span data-ttu-id="ea2d4-139">Yönetim grubu gönderilen SCOM Aracısı verileri</span><span class="sxs-lookup"><span data-stu-id="ea2d4-139">SCOM agent data sent via management group</span></span> | <span data-ttu-id="ea2d4-140">Toplama sıklığı</span><span class="sxs-lookup"><span data-stu-id="ea2d4-140">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="ea2d4-141">Windows</span><span class="sxs-lookup"><span data-stu-id="ea2d4-141">Windows</span></span> | <span data-ttu-id="ea2d4-142">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ea2d4-142">&#8226;</span></span> | <span data-ttu-id="ea2d4-143">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ea2d4-143">&#8226;</span></span> |  |  | <span data-ttu-id="ea2d4-144">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ea2d4-144">&#8226;</span></span> |<span data-ttu-id="ea2d4-145">7 gün</span><span class="sxs-lookup"><span data-stu-id="ea2d4-145">7 days</span></span> |

## <a name="operations-manager-run-as-accounts-for-oms"></a><span data-ttu-id="ea2d4-146">Operations Manager hesapları OMS için Çalıştır</span><span class="sxs-lookup"><span data-stu-id="ea2d4-146">Operations Manager run-as accounts for OMS</span></span>
<span data-ttu-id="ea2d4-147">OMS günlük analizi hello Operations Manager aracısı ve yönetim grubu toocollect kullanır ve veri toohello OMS hizmetine gönderir.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-147">Log Analytics in OMS uses hello Operations Manager agent and management group toocollect and send data toohello OMS service.</span></span> <span data-ttu-id="ea2d4-148">Yönetim paketleri için iş yüklerini tooprovide bağlı OMS derlemeleri değeri-hizmetlerini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-148">OMS builds upon management packs for workloads tooprovide value-add services.</span></span> <span data-ttu-id="ea2d4-149">Her iş yükü, bir etki alanı hesabı gibi farklı güvenlik bağlamında iş yüküne özgü ayrıcalıkları toorun yönetim paketleri gerektirir.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-149">Each workload requires workload-specific privileges toorun management packs in a different security context, such as a domain account.</span></span> <span data-ttu-id="ea2d4-150">Bir Operations Manager farklı çalıştır hesabı yapılandırarak tooprovide kimlik bilgileri gerekir.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-150">You need tooprovide credential information by configuring an Operations Manager Run As account.</span></span>

<span data-ttu-id="ea2d4-151">SQL değerlendirmesi için Çalıştır bilgiler tooset hello Operations Manager hesabı aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-151">Use hello following information tooset hello Operations Manager run-as account for SQL Assessment.</span></span>

### <a name="set-hello-run-as-account-for-sql-assessment"></a><span data-ttu-id="ea2d4-152">SQL değerlendirmesi için Hello farklı çalıştır hesabı ayarlama</span><span class="sxs-lookup"><span data-stu-id="ea2d4-152">Set hello Run As account for SQL assessment</span></span>
 <span data-ttu-id="ea2d4-153">Merhaba SQL Server Yönetim Paketi zaten kullanıyorsanız, bu farklı çalıştır hesabı kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-153">If you are already using hello SQL Server management pack, you should use that Run As account.</span></span>

#### <a name="tooconfigure-hello-sql-run-as-account-in-hello-operations-console"></a><span data-ttu-id="ea2d4-154">tooconfigure hello hello işletim Konsolu SQL farklı çalıştır hesabı</span><span class="sxs-lookup"><span data-stu-id="ea2d4-154">tooconfigure hello SQL Run As account in hello Operations console</span></span>
> [!NOTE]
> <span data-ttu-id="ea2d4-155">Kullanıyorsanız hello OMS hello SCOM Aracısı yerine, aracı doğrudan, hello Yönetim Paketi hello güvenlik bağlamında hello yerel sistem hesabı her zaman çalışır.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-155">If you are using hello OMS direct agent, rather than hello SCOM agent, hello management pack always runs in hello security context of hello Local System account.</span></span> <span data-ttu-id="ea2d4-156">Atla adım 1-5 aşağıdaki ve çalıştırma ya da NT AUTHORITY\SYSTEM hello kullanıcı adı olarak belirterek, T-SQL veya Powershell örnek hello.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-156">Skip steps 1-5 below, and run either hello T-SQL or Powershell sample, specifying NT AUTHORITY\SYSTEM as hello user name.</span></span>
>
>

1. <span data-ttu-id="ea2d4-157">Operations Manager'da hello işletim konsolunu açın ve ardından **Yönetim**.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-157">In Operations Manager, open hello Operations console, and then click **Administration**.</span></span>
2. <span data-ttu-id="ea2d4-158">Altında **Çalıştır Yapılandırması**, tıklatın **profilleri**, açarak **OMS SQL değerlendirmesi farklı çalıştır profili**.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-158">Under **Run As Configuration**, click **Profiles**, and open **OMS SQL Assessment Run As Profile**.</span></span>
3. <span data-ttu-id="ea2d4-159">Merhaba üzerinde **farklı çalıştır hesapları** sayfasında, **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-159">On hello **Run As Accounts** page, click **Add**.</span></span>
4. <span data-ttu-id="ea2d4-160">SQL Server için gereken hello kimlik bilgilerini içeren bir Windows farklı çalıştır hesabı seçin veya tıklatın **yeni** toocreate biri.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-160">Select a Windows Run As account that contains hello credentials needed for SQL Server, or click **New** toocreate one.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ea2d4-161">Windows Hello farklı çalıştır hesap türü olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-161">hello Run As account type must be Windows.</span></span> <span data-ttu-id="ea2d4-162">Merhaba farklı çalıştır hesabı, aynı zamanda SQL Server örneklerini barındıran tüm Windows sunucularında yerel Administrators grubunun bir parçası olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-162">hello Run As account must also be part of Local Administrators group on all Windows Servers hosting SQL Server Instances.</span></span>
   >
   >
5. <span data-ttu-id="ea2d4-163">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-163">Click **Save**.</span></span>
6. <span data-ttu-id="ea2d4-164">Değiştirin ve sonra her SQL Server örneği toogrant minimum izinleri gerekli tooRun üzerinde hesabı tooperform SQL değerlendirmesi T-SQL örneği aşağıdaki hello yürütün.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-164">Modify and then execute hello following T-SQL sample on each SQL Server Instance toogrant minimum permissions required tooRun As Account tooperform SQL Assessment.</span></span> <span data-ttu-id="ea2d4-165">Ancak, bir farklı çalıştır hesabı SQL Server örnekleri üzerindeki hello sysadmin sunucu rolünün bir parçası ise bu toodo ihtiyacınız yoktur.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-165">However, you don’t need toodo this if a Run As Account is already part of hello sysadmin server role on SQL Server Instances.</span></span>

```
---
    -- Replace <UserName> with hello actual user name being used as Run As Account.
    USE master

    -- Create login for hello user, comment this line if login is already created.
    CREATE LOGIN [<UserName>] FROM WINDOWS

    -- Grant permissions toouser.
    GRANT VIEW SERVER STATE too[<UserName>]
    GRANT VIEW ANY DEFINITION too[<UserName>]
    GRANT VIEW ANY DATABASE too[<UserName>]

    -- Add database user for all hello databases on SQL Server Instance, this is required for connecting tooindividual databases.
    -- NOTE: This command must be run anytime new databases are added tooSQL Server instances.
    EXEC sp_msforeachdb N'USE [?]; CREATE USER [<UserName>] FOR LOGIN [<UserName>];'

```
#### <a name="tooconfigure-hello-sql-run-as-account-using-windows-powershell"></a><span data-ttu-id="ea2d4-166">tooconfigure hello Windows PowerShell kullanarak SQL farklı çalıştır hesabı</span><span class="sxs-lookup"><span data-stu-id="ea2d4-166">tooconfigure hello SQL Run As account using Windows PowerShell</span></span>
<span data-ttu-id="ea2d4-167">Bir PowerShell penceresi açın ve bilgilerinizle güncelleştirdikten sonra komut dosyası izleyen hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="ea2d4-167">Open a PowerShell window and run hello following script after you’ve updated it with your information:</span></span>

```

    import-module OperationsManager
    New-SCOMManagementGroupConnection "<your management group name>"

    $profile = Get-SCOMRunAsProfile -DisplayName "OMS SQL Assessment Run As Profile"
    $account = Get-SCOMrunAsAccount | Where-Object {$_.Name -eq "<your run as account name>"}
    Set-SCOMRunAsProfile -Action "Add" -Profile $Profile -Account $Account
```

## <a name="understanding-how-recommendations-are-prioritized"></a><span data-ttu-id="ea2d4-168">Önerilerin nasıl önceliklendirilir anlama</span><span class="sxs-lookup"><span data-stu-id="ea2d4-168">Understanding how recommendations are prioritized</span></span>
<span data-ttu-id="ea2d4-169">Yapılan her öneri hello öneri göreceli önemini hello tanımlayan bir ağırlıklı değer verilir.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-169">Every recommendation made is given a weighting value that identifies hello relative importance of hello recommendation.</span></span> <span data-ttu-id="ea2d4-170">Yalnızca hello on en önemli öneriler gösterilir.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-170">Only hello ten most important recommendations are shown.</span></span>

### <a name="how-weights-are-calculated"></a><span data-ttu-id="ea2d4-171">Ağırlıkları nasıl hesaplanır</span><span class="sxs-lookup"><span data-stu-id="ea2d4-171">How weights are calculated</span></span>
<span data-ttu-id="ea2d4-172">Ağırlık belirlemeyi üç anahtar faktörlerini temel alarak toplam değerler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="ea2d4-172">Weightings are aggregate values based on three key factors:</span></span>

* <span data-ttu-id="ea2d4-173">Merhaba *olasılık* tanımlanan bir sorunun sorunlara neden.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-173">hello *probability* that an issue identified will cause problems.</span></span> <span data-ttu-id="ea2d4-174">Daha yüksek olasılık büyük genel puan hello öneri tooa karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-174">A higher probability equates tooa larger overall score for hello recommendation.</span></span>
* <span data-ttu-id="ea2d4-175">Merhaba *etkisi* kuruluşunuzdaki bir soruna neden olursa hello sorun.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-175">hello *impact* of hello issue on your organization if it does cause a problem.</span></span> <span data-ttu-id="ea2d4-176">Daha yüksek bir etkisi, büyük genel puan hello öneri tooa karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-176">A higher impact equates tooa larger overall score for hello recommendation.</span></span>
* <span data-ttu-id="ea2d4-177">Merhaba *çaba* tooimplement hello öneri gerekli.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-177">hello *effort* required tooimplement hello recommendation.</span></span> <span data-ttu-id="ea2d4-178">Daha yüksek çaba küçük genel puan hello öneri tooa karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-178">A higher effort equates tooa smaller overall score for hello recommendation.</span></span>

<span data-ttu-id="ea2d4-179">Her bir öneri ağırlığı hello hello toplam puanı her odak alanı için kullanılabilir bir yüzdesi olarak ifade edilir.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-179">hello weighting for each recommendation is expressed as a percentage of hello total score available for each focus area.</span></span> <span data-ttu-id="ea2d4-180">Bir öneri hello güvenlik ve uyumluluk odaklanılan alan %5 puanı varsa, örneğin, bu öneri uygulama, genel güvenlik ve uyumluluk puan tarafından %5 artacaktır.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-180">For example, if a recommendation in hello Security and Compliance focus area has a score of 5%, implementing that recommendation will increase your overall Security and Compliance score by 5%.</span></span>

### <a name="focus-areas"></a><span data-ttu-id="ea2d4-181">Odak alanları</span><span class="sxs-lookup"><span data-stu-id="ea2d4-181">Focus areas</span></span>
<span data-ttu-id="ea2d4-182">**Güvenlik ve Uyumluluk** -bu odak alanı olası güvenlik tehditlerini ve ihlallerinden, şirket ilkelerini ve teknik ve yasal uyumluluk gereksinimleri için öneriler gösterir.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-182">**Security and Compliance** - This focus area shows recommendations for potential security threats and breaches, corporate policies, and technical, legal and regulatory compliance requirements.</span></span>

<span data-ttu-id="ea2d4-183">**Kullanılabilirlik ve iş sürekliliği** -bu odaklanılan alan hizmet kullanılabilirliği, altyapı ve iş koruması dayanıklılık için öneriler gösterir.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-183">**Availability and Business Continuity** - This focus area shows recommendations for service availability, resiliency of your infrastructure, and business protection.</span></span>

<span data-ttu-id="ea2d4-184">**Performans ve ölçeklenebilirlik** -bu odaklanılan alan önerileri toohelp kuruluşunuzun gösterir BT altyapısı arttıkça, BT ortamınız geçerli performans gereksinimlerini karşıladığından ve mümkün toorespond toochanging olduğundan emin olun Altyapı gerekir.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-184">**Performance and Scalability** - This focus area shows recommendations toohelp your organization's IT infrastructure grow, ensure that your IT environment meets current performance requirements, and is able toorespond toochanging infrastructure needs.</span></span>

<span data-ttu-id="ea2d4-185">**Yükseltme, geçiş ve dağıtım** - bu odak alanı yükseltme önerileri toohelp gösterir, geçirme ve SQL Server tooyour mevcut altyapıyı.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-185">**Upgrade, Migration and Deployment** - This focus area shows recommendations toohelp you upgrade, migrate, and deploy SQL Server tooyour existing infrastructure.</span></span>

<span data-ttu-id="ea2d4-186">**İşlemler ve izleme** - bu odaklanılan alan önerileri toohelp daha verimli hale BT işlemlerinizi gösterir önleyici bakım uygulamak ve performansı en üst düzeye çıkarın.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-186">**Operations and Monitoring** - This focus area shows recommendations toohelp streamline your IT operations, implement preventative maintenance, and maximize performance.</span></span>

<span data-ttu-id="ea2d4-187">**Değişiklik ve yapılandırma yönetimi** -bu odak alanı öneriler gösterir toohelp günlük işlemlerini korumak, değişiklikleri yok olumsuz altyapınızı etkiler, değişiklik denetim yordamları ve tootrack oluşturun ve denetim emin olun Sistem yapılandırması.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-187">**Change and Configuration Management** - This focus area shows recommendations toohelp protect day-to-day operations, ensure that changes don't negatively affect your infrastructure, establish change control procedures, and tootrack and audit system configurations.</span></span>

### <a name="should-you-aim-tooscore-100-in-every-focus-area"></a><span data-ttu-id="ea2d4-188">Her odak alanında % 100 tooscore hedeflemeniz gerektiğini?</span><span class="sxs-lookup"><span data-stu-id="ea2d4-188">Should you aim tooscore 100% in every focus area?</span></span>
<span data-ttu-id="ea2d4-189">Olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-189">Not necessarily.</span></span> <span data-ttu-id="ea2d4-190">Merhaba önerileri hello bilgi ve müşteri ziyaretleriniz binlerce arasında Microsoft mühendisleri tarafından elde edilen deneyimleri temel alır.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-190">hello recommendations are based on hello knowledge and experiences gained by Microsoft engineers across thousands of customer visits.</span></span> <span data-ttu-id="ea2d4-191">Ancak, iki sunucu altyapılar aynı hello ve belirli öneriler fazla veya az ilgili tooyou olabilir değildir.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-191">However, no two server infrastructures are hello same, and specific recommendations may be more or less relevant tooyou.</span></span> <span data-ttu-id="ea2d4-192">Örneğin, bazı güvenlik önerileri sanal makinelerinizi gösterilen toohello Internet değilseniz, daha az ilgili olabilir.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-192">For example, some security recommendations might be less relevant if your virtual machines are not exposed toohello Internet.</span></span> <span data-ttu-id="ea2d4-193">Bazı kullanılabilirlik öneriler düşük öncelik geçici veri toplama ve raporlama sağladığı hizmetler için daha az uygun olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-193">Some availability recommendations may be less relevant for services that provide low priority ad hoc data collection and reporting.</span></span> <span data-ttu-id="ea2d4-194">Önemli tooa olgun iş sorunlarını daha az önemli tooa başlatma olabilir.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-194">Issues that are important tooa mature business may be less important tooa start-up.</span></span> <span data-ttu-id="ea2d4-195">Önceliklerinizden hangi odak alanlarıdır tooidentify istediğiniz ve, puanları zamanla nasıl değiştiğini adresindeki bakın.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-195">You may want tooidentify which focus areas are your priorities and then look at how your scores change over time.</span></span>

<span data-ttu-id="ea2d4-196">Her öneri neden önemli olduğu hakkında yönergeler içerir.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-196">Every recommendation includes guidance about why it is important.</span></span> <span data-ttu-id="ea2d4-197">Merhaba öneri uygulama BT Hizmetleri ve hello iş gereksinimlerinizi kuruluşunuzun hello yapısını verilen sizin için uygun olup, bu kılavuzu tooevaluate kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-197">You should use this guidance tooevaluate whether implementing hello recommendation is appropriate for you, given hello nature of your IT services and hello business needs of your organization.</span></span>

## <a name="use-assessment-focus-area-recommendations"></a><span data-ttu-id="ea2d4-198">Değerlendirme odak alanı önerileri kullanın</span><span class="sxs-lookup"><span data-stu-id="ea2d4-198">Use assessment focus area recommendations</span></span>
<span data-ttu-id="ea2d4-199">OMS içinde bir değerlendirme çözümü kullanmadan önce hello çözümü yüklenmiş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-199">Before you can use an assessment solution in OMS, you must have hello solution installed.</span></span> <span data-ttu-id="ea2d4-200">çözümler, yükleme hakkında daha fazla tooread bkz [hello Çözümleri Galerisi eklemek günlük analizi çözümleri](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="ea2d4-200">tooread more about installing solutions, see [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span> <span data-ttu-id="ea2d4-201">Yüklendikten sonra hello genel bakış sayfasında OMS hello SQL değerlendirmesi kutucuğu kullanarak önerileri hello özetini görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-201">After it is installed, you can view hello summary of recommendations by using hello SQL Assessment tile on hello Overview page in OMS.</span></span>

<span data-ttu-id="ea2d4-202">Görünüm hello altyapınızı ve ardından-ayrıntıya önerileri için Uyumluluk değerlendirmesi özetlenir.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-202">View hello summarized compliance assessments for your infrastructure and then drill-into recommendations.</span></span>

### <a name="tooview-recommendations-for-a-focus-area-and-take-corrective-action"></a><span data-ttu-id="ea2d4-203">bir odak alanı ve Al düzeltme eylemi için tooview önerileri</span><span class="sxs-lookup"><span data-stu-id="ea2d4-203">tooview recommendations for a focus area and take corrective action</span></span>
1. <span data-ttu-id="ea2d4-204">Merhaba üzerinde **genel bakış** hello sayfasında, **SQL değerlendirmesi** döşeme.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-204">On hello **Overview** page, click hello **SQL Assessment** tile.</span></span>
2. <span data-ttu-id="ea2d4-205">Merhaba üzerinde **SQL değerlendirmesi** sayfasında hello odak alanı Kanatlar birinde hello özet bilgileri gözden geçirin ve aşağıdakilerden tooview önerileri bu odaklanılan alan için tıklatın.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-205">On hello **SQL Assessment** page, review hello summary information in one of hello focus area blades and then click one tooview recommendations for that focus area.</span></span>
3. <span data-ttu-id="ea2d4-206">Merhaba odak alanı sayfaları hiçbirinde ortamınız için öncelik hello önerilerin görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-206">On any of hello focus area pages, you can view hello prioritized recommendations made for your environment.</span></span> <span data-ttu-id="ea2d4-207">Önerinin altında tıklatın **etkilenen nesneler** tooview hakkında ayrıntılı hello öneri yapılan neden.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-207">Click a recommendation under **Affected Objects** tooview details about why hello recommendation is made.</span></span>  
    <span data-ttu-id="ea2d4-208">![SQL değerlendirmesi önerileri görüntüsü](./media/log-analytics-sql-assessment/sql-assess-focus.png)</span><span class="sxs-lookup"><span data-stu-id="ea2d4-208">![image of SQL Assessment recommendations](./media/log-analytics-sql-assessment/sql-assess-focus.png)</span></span>
4. <span data-ttu-id="ea2d4-209">Önerilen düzeltici eylemleri gerçekleştirebilirsiniz **önerilen eylemleri**.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-209">You can take corrective actions suggested in **Suggested Actions**.</span></span> <span data-ttu-id="ea2d4-210">Merhaba öğesi ele, önerilen eylemler gerçekleştirilen ve uyumluluk puan artıracaktır sonraki değerlendirmeleri kaydeder.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-210">When hello item has been addressed, later assessments will record that recommended actions were taken and your compliance score will increase.</span></span> <span data-ttu-id="ea2d4-211">Düzeltilmiş öğeler görünür olarak **geçirilen nesneleri**.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-211">Corrected items appear as **Passed Objects**.</span></span>

## <a name="ignore-recommendations"></a><span data-ttu-id="ea2d4-212">Öneriler yoksay</span><span class="sxs-lookup"><span data-stu-id="ea2d4-212">Ignore recommendations</span></span>
<span data-ttu-id="ea2d4-213">Tooignore istediğiniz önerileri varsa, OMS değerlendirme sonuçlarında görünmesini tooprevent önerileri kullanacağı bir metin dosyası oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-213">If you have recommendations that you want tooignore, you can create a text file that OMS will use tooprevent recommendations from appearing in your assessment results.</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

### <a name="tooidentify-recommendations-that-you-will-ignore"></a><span data-ttu-id="ea2d4-214">göz ardı eder tooidentify önerileri</span><span class="sxs-lookup"><span data-stu-id="ea2d4-214">tooidentify recommendations that you will ignore</span></span>
1. <span data-ttu-id="ea2d4-215">Tooyour çalışma alanında oturum ve günlük arama açın.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-215">Sign in tooyour workspace and open Log Search.</span></span> <span data-ttu-id="ea2d4-216">Aşağıdaki, ortamınızdaki bilgisayarları için başarısız olan sorgu toolist önerileri hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-216">Use hello following query toolist recommendations that have failed for computers in your environment.</span></span>

   ```
   Type=SQLAssessmentRecommendation RecommendationResult=Failed | select  Computer, RecommendationId, Recommendation | sort  Computer
   ```

   <span data-ttu-id="ea2d4-217">Bir ekran görüntüsü gösteren hello günlük arama sorgusu şöyledir: ![önerileri başarısız oldu](./media/log-analytics-sql-assessment/sql-assess-failed-recommendations.png)</span><span class="sxs-lookup"><span data-stu-id="ea2d4-217">Here's a screen shot showing hello Log Search query: ![failed recommendations](./media/log-analytics-sql-assessment/sql-assess-failed-recommendations.png)</span></span>
2. <span data-ttu-id="ea2d4-218">Öneriler tooignore istediğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-218">Choose recommendations that you want tooignore.</span></span> <span data-ttu-id="ea2d4-219">Merhaba sonraki yordamda Recommendationıd için hello değerleri kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-219">You’ll use hello values for RecommendationId in hello next procedure.</span></span>

### <a name="toocreate-and-use-an-ignorerecommendationstxt-text-file"></a><span data-ttu-id="ea2d4-220">toocreate ve IgnoreRecommendations.txt metin dosyayı kullan</span><span class="sxs-lookup"><span data-stu-id="ea2d4-220">toocreate and use an IgnoreRecommendations.txt text file</span></span>
1. <span data-ttu-id="ea2d4-221">IgnoreRecommendations.txt adlı bir dosya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-221">Create a file named IgnoreRecommendations.txt.</span></span>
2. <span data-ttu-id="ea2d4-222">Her Recommendationıd, OMS tooignore ayrı bir satırda istediğiniz ve ardından hello dosyasını kaydedip kapatın, her bir öneri için yazın veya yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-222">Paste or type each RecommendationId for each recommendation that you want OMS tooignore on a separate line and then save and close hello file.</span></span>
3. <span data-ttu-id="ea2d4-223">Merhaba dosya klasörü OMS tooignore önerileri istediğiniz her bilgisayarda aşağıdaki hello yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-223">Put hello file in hello following folder on each computer where you want OMS tooignore recommendations.</span></span>
   * <span data-ttu-id="ea2d4-224">Microsoft Monitoring Agent (doğrudan veya Operations Manager aracılığıyla bağlı) - hello olan bilgisayarlarda *SystemDrive*: \Program izleme Agent\Agent</span><span class="sxs-lookup"><span data-stu-id="ea2d4-224">On computers with hello Microsoft Monitoring Agent (connected directly or through Operations Manager) - *SystemDrive*:\Program Files\Microsoft Monitoring Agent\Agent</span></span>
   * <span data-ttu-id="ea2d4-225">Merhaba Operations Manager yönetim sunucusunda - *SystemDrive*: \Program System Center 2012 R2\Operations Manager\Server</span><span class="sxs-lookup"><span data-stu-id="ea2d4-225">On hello Operations Manager management server - *SystemDrive*:\Program Files\Microsoft System Center 2012 R2\Operations Manager\Server</span></span>

### <a name="tooverify-that-recommendations-are-ignored"></a><span data-ttu-id="ea2d4-226">tooverify önerileri göz ardı edilir</span><span class="sxs-lookup"><span data-stu-id="ea2d4-226">tooverify that recommendations are ignored</span></span>
1. <span data-ttu-id="ea2d4-227">Merhaba Hello sonraki zamanlanmış değerlendirme, varsayılan olarak 7 günde çalıştıktan sonra belirtilen önerileri yoksayıldı işaretlenir ve hello değerlendirme Panoda görünmez.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-227">After hello next scheduled assessment runs, by default every 7 days, hello specified recommendations are marked Ignored and will not appear on hello assessment dashboard.</span></span>
2. <span data-ttu-id="ea2d4-228">Tüm göz ardı hello önerileri günlük arama sorguları toolist aşağıdaki hello kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-228">You can use hello following Log Search queries toolist all hello ignored recommendations.</span></span>

   ```
   Type=SQLAssessmentRecommendation RecommendationResult=Ignored | select  Computer, RecommendationId, Recommendation | sort  Computer
   ```
3. <span data-ttu-id="ea2d4-229">Daha sonra göz ardı toosee önerileri istemediğinize karar verirseniz, tüm IgnoreRecommendations.txt dosyaları silin veya bunları RecommendationIDs kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-229">If you decide later that you want toosee ignored recommendations, remove any IgnoreRecommendations.txt files, or you can remove RecommendationIDs from them.</span></span>

## <a name="sql-assessment-solution-faq"></a><span data-ttu-id="ea2d4-230">SQL değerlendirme çözümü hakkında SSS</span><span class="sxs-lookup"><span data-stu-id="ea2d4-230">SQL Assessment solution FAQ</span></span>
<span data-ttu-id="ea2d4-231">*Sıklıkla bir değerlendirme çalışıyor mu?*</span><span class="sxs-lookup"><span data-stu-id="ea2d4-231">*How often does an assessment run?*</span></span>

* <span data-ttu-id="ea2d4-232">Merhaba değerlendirme 7 günde bir çalışır.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-232">hello assessment runs every 7 days.</span></span>

<span data-ttu-id="ea2d4-233">*Merhaba değerlendirme çalıştıran bir şekilde tooconfigure ne sıklıkta var mı?*</span><span class="sxs-lookup"><span data-stu-id="ea2d4-233">*Is there a way tooconfigure how often hello assessment runs?*</span></span>

* <span data-ttu-id="ea2d4-234">Şu anda değil.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-234">Not at this time.</span></span>

<span data-ttu-id="ea2d4-235">*I hello SQL değerlendirme çözümü ekledikten sonra başka bir sunucuya belirlediyseniz değerlendirileceğini?*</span><span class="sxs-lookup"><span data-stu-id="ea2d4-235">*If another server is discovered after I’ve added hello SQL assessment solution, will it be assessed?*</span></span>

* <span data-ttu-id="ea2d4-236">Evet, bunu daha sonra gelen her 7 günde değerlendirildiği bulunduktan sonra.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-236">Yes, once it is discovered it is assessed from then on, every 7 days.</span></span>

<span data-ttu-id="ea2d4-237">*Ne zaman bir sunucu kullanımdan alındığında hello değerlendirme kaldırılacak?*</span><span class="sxs-lookup"><span data-stu-id="ea2d4-237">*If a server is decommissioned, when will it be removed from hello assessment?*</span></span>

* <span data-ttu-id="ea2d4-238">Bir sunucu için 3 hafta veri göndermez, kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-238">If a server does not submit data for 3 weeks, it is removed.</span></span>

<span data-ttu-id="ea2d4-239">*Veri toplama hello hello işlemin hello adı nedir?*</span><span class="sxs-lookup"><span data-stu-id="ea2d4-239">*What is hello name of hello process that does hello data collection?*</span></span>

* <span data-ttu-id="ea2d4-240">AdvisorAssessment.exe</span><span class="sxs-lookup"><span data-stu-id="ea2d4-240">AdvisorAssessment.exe</span></span>

<span data-ttu-id="ea2d4-241">*Ne kadar süreyle için toplanan verileri toobe sürer?*</span><span class="sxs-lookup"><span data-stu-id="ea2d4-241">*How long does it take for data toobe collected?*</span></span>

* <span data-ttu-id="ea2d4-242">Merhaba gerçek veri toplama hello sunucuda yaklaşık 1 saat sürer.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-242">hello actual data collection on hello server takes about 1 hour.</span></span> <span data-ttu-id="ea2d4-243">Bu çok sayıda SQL örnekleri veya veritabanlarına sahip sunucularda uzun sürebilir.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-243">It may take longer on servers that have a large number of SQL instances or databases.</span></span>

<span data-ttu-id="ea2d4-244">*Hangi türde veri toplanır?*</span><span class="sxs-lookup"><span data-stu-id="ea2d4-244">*What type of data is collected?*</span></span>

* <span data-ttu-id="ea2d4-245">veri türleri aşağıdaki hello toplanır:</span><span class="sxs-lookup"><span data-stu-id="ea2d4-245">hello following types of data are collected:</span></span>
  * <span data-ttu-id="ea2d4-246">WMI</span><span class="sxs-lookup"><span data-stu-id="ea2d4-246">WMI</span></span>
  * <span data-ttu-id="ea2d4-247">Kayıt defteri</span><span class="sxs-lookup"><span data-stu-id="ea2d4-247">Registry</span></span>
  * <span data-ttu-id="ea2d4-248">Performans sayaçları</span><span class="sxs-lookup"><span data-stu-id="ea2d4-248">Performance counters</span></span>
  * <span data-ttu-id="ea2d4-249">SQL Dinamik Yönetim görünümlerini (DMV).</span><span class="sxs-lookup"><span data-stu-id="ea2d4-249">SQL dynamic management views (DMV).</span></span>

<span data-ttu-id="ea2d4-250">*Verileri toplandığında yolu tooconfigure var mı?*</span><span class="sxs-lookup"><span data-stu-id="ea2d4-250">*Is there a way tooconfigure when data is collected?*</span></span>

* <span data-ttu-id="ea2d4-251">Şu anda değil.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-251">Not at this time.</span></span>

<span data-ttu-id="ea2d4-252">*Bir farklı çalıştır hesabı neden tooconfigure var mı?*</span><span class="sxs-lookup"><span data-stu-id="ea2d4-252">*Why do I have tooconfigure a Run As Account?*</span></span>

* <span data-ttu-id="ea2d4-253">SQL Server için SQL sorguları az sayıda çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-253">For SQL Server, a small number of SQL queries are run.</span></span> <span data-ttu-id="ea2d4-254">Bunları sırayla toorun, bir farklı çalıştır hesabı VIEW SERVER STATE izinleri tooSQL birlikte kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-254">In order for them toorun, a Run As Account with VIEW SERVER STATE permissions tooSQL must be used.</span></span>  <span data-ttu-id="ea2d4-255">Ayrıca, sipariş tooquery WMI'da, yerel yönetici kimlik bilgileri gereklidir.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-255">In addition, in order tooquery WMI, local administrator credentials are required.</span></span>

<span data-ttu-id="ea2d4-256">*Neden yalnızca hello ilk 10 önerileri görüntülemek?*</span><span class="sxs-lookup"><span data-stu-id="ea2d4-256">*Why display only hello top 10 recommendations?*</span></span>

* <span data-ttu-id="ea2d4-257">Görevler kapsamlı bir zorlamayı listesi vermek yerine, öncelik hello önerileri adresleme odaklanmak öneririz.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-257">Instead of giving you an exhaustive overwhelming list of tasks, we recommend that you focus on addressing hello prioritized recommendations first.</span></span> <span data-ttu-id="ea2d4-258">Bunları çözün sonra ek öneriler kullanılabilir hale gelir.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-258">After you address them, additional recommendations will become available.</span></span> <span data-ttu-id="ea2d4-259">Toosee hello ayrıntılı liste tercih ederseniz, tüm öneriler hello OMS günlük arama özelliğini kullanarak görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-259">If you prefer toosee hello detailed list, you can view all recommendations using hello OMS log search.</span></span>

<span data-ttu-id="ea2d4-260">*Herhangi bir şekilde tooignore bir öneri var mı?*</span><span class="sxs-lookup"><span data-stu-id="ea2d4-260">*Is there a way tooignore a recommendation?*</span></span>

* <span data-ttu-id="ea2d4-261">Evet, bkz: [önerileri yoksay](#ignore-recommendations) yukarıdaki bölümde.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-261">Yes, see [Ignore recommendations](#ignore-recommendations) section above.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ea2d4-262">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ea2d4-262">Next steps</span></span>
* <span data-ttu-id="ea2d4-263">[Arama günlüklerini](log-analytics-log-searches.md) tooview ayrıntılı SQL Değerlendirme verileri ve öneriler.</span><span class="sxs-lookup"><span data-stu-id="ea2d4-263">[Search logs](log-analytics-log-searches.md) tooview detailed SQL Assessment data and recommendations.</span></span>
