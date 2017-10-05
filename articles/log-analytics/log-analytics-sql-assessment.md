---
title: "SQL Server ortamınızın Azure günlük analizi ile en iyi duruma getirme | Microsoft Docs"
description: "Azure günlük analizi ile risk ve SQL server ortamlarınızın durumunu düzenli aralıklarla değerlendirmek için SQL değerlendirme çözümü kullanabilirsiniz."
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
ms.openlocfilehash: d2aed3315fe60ace46dfb4176dc13aa417257b0c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="optimize-your-sql-server-environment-with-the-sql-assessment-solution-in-log-analytics"></a><span data-ttu-id="be4f3-103">SQL Server ortamınızın günlük analizi SQL değerlendirmesi çözümde ile en iyi duruma getirme</span><span class="sxs-lookup"><span data-stu-id="be4f3-103">Optimize your SQL Server environment with the SQL Assessment solution in Log Analytics</span></span>

![SQL değerlendirmesi simgesi](./media/log-analytics-sql-assessment/sql-assessment-symbol.png)

<span data-ttu-id="be4f3-105">SQL değerlendirme çözümü, risk ve sunucu ortamlarınızın durumunu düzenli aralıklarla değerlendirmek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="be4f3-105">You can use the SQL Assessment solution to assess the risk and health of your server environments on a regular interval.</span></span> <span data-ttu-id="be4f3-106">Bu makalede, olası sorunlar için düzeltme eylemleri yararlanabilmeniz çözümü yüklemenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="be4f3-106">This article will help you install the solution so that you can take corrective actions for potential problems.</span></span>

<span data-ttu-id="be4f3-107">Bu çözüm önerileri dağıtılan sunucu altyapınızı belirli öncelikli listesi sağlar.</span><span class="sxs-lookup"><span data-stu-id="be4f3-107">This solution provides a prioritized list of recommendations specific to your deployed server infrastructure.</span></span> <span data-ttu-id="be4f3-108">Öneriler altı arasında ayrılır hızla yardımcı odak alanlarına riski anlamak ve düzeltme eylemlerini gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="be4f3-108">The recommendations are categorized across six focus areas which help you quickly understand the risk and take corrective action.</span></span>

<span data-ttu-id="be4f3-109">Önerilerin bilgi ve müşteri ziyaretleriniz binlerce Microsoft mühendisleri tarafından elde edilen deneyimlerden dayanır.</span><span class="sxs-lookup"><span data-stu-id="be4f3-109">The recommendations made are based on the knowledge and experience gained by Microsoft engineers from thousands of customer visits.</span></span> <span data-ttu-id="be4f3-110">Her bir öneri, bir sorun için neden önemli ve önerilen değişiklikleri uygulamak nasıl hakkında rehberlik sağlar.</span><span class="sxs-lookup"><span data-stu-id="be4f3-110">Each recommendation provides guidance about why an issue might matter to you and how to implement the suggested changes.</span></span>

<span data-ttu-id="be4f3-111">Kuruluşunuz için en önemli ve ücretsiz ve sağlam bir risk ortam çalıştıran doğru ilerleme durumunuzu izlemenize odak alanlarına seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="be4f3-111">You can choose focus areas that are most important to your organization and track your progress toward running a risk free and healthy environment.</span></span>

<span data-ttu-id="be4f3-112">Çözüm ekledik ve bir değerlendirme tamamlanan, Özet sonra odak alanlarına odaklanmak için bilgi gösterilir **SQL değerlendirmesi** Panosu ortamınızdaki altyapısı için.</span><span class="sxs-lookup"><span data-stu-id="be4f3-112">After you've added the solution and an assessment is completed, summary information for focus areas is shown on the **SQL Assessment** dashboard for the infrastructure in your environment.</span></span> <span data-ttu-id="be4f3-113">Aşağıdaki bölümlerde bilgileri üzerinde nasıl kullanacağınızı **SQL değerlendirmesi** Pano, burada görüntüleyebilir ve ardından uygulayın önerilen eylemler için SQL server altyapınızı.</span><span class="sxs-lookup"><span data-stu-id="be4f3-113">The following sections describe how to use the information on the **SQL Assessment** dashboard, where you can view and then take recommended actions for your SQL server infrastructure.</span></span>

![SQL değerlendirmesi döşeme görüntüsü](./media/log-analytics-sql-assessment/sql-assess-tile.png)

![SQL değerlendirmesi Pano görüntüsü](./media/log-analytics-sql-assessment/sql-assess-dash.png)

## <a name="installing-and-configuring-the-solution"></a><span data-ttu-id="be4f3-116">Yükleme ve çözüm yapılandırılıyor</span><span class="sxs-lookup"><span data-stu-id="be4f3-116">Installing and configuring the solution</span></span>
<span data-ttu-id="be4f3-117">SQL Server Standard, Developer ve Enterprise sürümleri için şu anda desteklenen tüm sürümleri ile SQL değerlendirmesi çalışır.</span><span class="sxs-lookup"><span data-stu-id="be4f3-117">SQL Assessment works with all currently supported versions of SQL Server for the Standard, Developer, and Enterprise editions.</span></span>

<span data-ttu-id="be4f3-118">Yüklemek ve çözüm yapılandırmak için aşağıdaki bilgileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="be4f3-118">Use the following information to install and configure the solution.</span></span>

* <span data-ttu-id="be4f3-119">Aracıları SQL Server'ın yüklü olması sunucularda yüklü olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="be4f3-119">Agents must be installed on servers that have SQL Server installed.</span></span>
* <span data-ttu-id="be4f3-120">SQL değerlendirme çözümü bir OMS aracısı olan her bilgisayarda yüklü .NET Framework 4'ün desteklenen bir sürümünü gerektirir.</span><span class="sxs-lookup"><span data-stu-id="be4f3-120">The SQL Assessment solution requires a supported version of .NET Framework 4 installed on each computer that has an OMS agent.</span></span>
* <span data-ttu-id="be4f3-121">Çözümü yüklemek için kullanıcı bir yönetici ya da Azure aboneliğini katkıda bulunan Azure portal kullanırken olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="be4f3-121">In order to install the solution, the user must be an administrator or contributor to the Azure subscription when using the Azure portal.</span></span> <span data-ttu-id="be4f3-122">Buna ek olarak, kullanıcının OMS portalındaki OMS çalışma alanı katılımcısı veya yöneticisi rolünün üyesi olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="be4f3-122">In addition, the user must be a member of the OMS workspace contributor or administrator role in the OMS portal.</span></span>
* <span data-ttu-id="be4f3-123">Operations Manager aracısı SQL değerlendirmesi ile kullanırken, bir Operations Manager Run-As hesabı kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="be4f3-123">When using the Operations Manager agent with SQL Assessment, you'll need to use an Operations Manager Run-As account.</span></span> <span data-ttu-id="be4f3-124">Bkz: [Operations Manager Çalıştır hesapları için OMS](#operations-manager-run-as-accounts-for-oms) altında daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="be4f3-124">See [Operations Manager run-as accounts for OMS](#operations-manager-run-as-accounts-for-oms) below for more information.</span></span>

  > [!NOTE]
  > <span data-ttu-id="be4f3-125">MMA aracı Operations Manager Run-As hesaplarını desteklemez.</span><span class="sxs-lookup"><span data-stu-id="be4f3-125">The MMA agent does not support Operations Manager Run-As accounts.</span></span>
  >
  >
* <span data-ttu-id="be4f3-126">Açıklanan işlemi kullanarak, OMS çalışma SQL değerlendirme çözümü eklemek [Çözümleri Galerisi eklemek günlük analizi çözümleri](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="be4f3-126">Add the SQL Assessment solution to your OMS workspace using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span> <span data-ttu-id="be4f3-127">Başka bir yapılandırma işlemi gerekmez.</span><span class="sxs-lookup"><span data-stu-id="be4f3-127">There is no further configuration required.</span></span>

> [!NOTE]
> <span data-ttu-id="be4f3-128">Çözüm ekledikten sonra aracıları sunucularıyla AdvisorAssessment.exe dosyası eklenir.</span><span class="sxs-lookup"><span data-stu-id="be4f3-128">After you've added the solution, the AdvisorAssessment.exe file is added to servers with agents.</span></span> <span data-ttu-id="be4f3-129">Yapılandırma verilerini okuma ve işleme için bulutta OMS hizmetine gönderilir.</span><span class="sxs-lookup"><span data-stu-id="be4f3-129">Configuration data is read and then sent to the OMS service in the cloud for processing.</span></span> <span data-ttu-id="be4f3-130">Mantığı alınan verilere uygulanır ve bulut hizmeti verilerini kaydeder.</span><span class="sxs-lookup"><span data-stu-id="be4f3-130">Logic is applied to the received data and the cloud service records the data.</span></span>

## <a name="sql-assessment-data-collection-details"></a><span data-ttu-id="be4f3-131">SQL değerlendirmesi veri toplama ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="be4f3-131">SQL Assessment data collection details</span></span>
<span data-ttu-id="be4f3-132">SQL değerlendirmesi WMI verilerini, kayıt defteri verilerini, performans verilerini ve etkinleştirdiğiniz aracıları kullanarak SQL Server dinamik yönetim görünümünü sonuçları toplar.</span><span class="sxs-lookup"><span data-stu-id="be4f3-132">SQL Assessment collects WMI data, registry data, performance data, and SQL Server dynamic management view results using the agents that you have enabled.</span></span>

<span data-ttu-id="be4f3-133">Aşağıdaki tablo, Operations Manager (SCOM) gerekli olup olmadığını ve nasıl aracılar için veri toplama yöntemleri yapılandırmayı gösterir. genellikle veri bir aracı tarafından toplanır.</span><span class="sxs-lookup"><span data-stu-id="be4f3-133">The following table shows data collection methods for agents, whether Operations Manager (SCOM) is required, and how often data is collected by an agent.</span></span>

| <span data-ttu-id="be4f3-134">Platform</span><span class="sxs-lookup"><span data-stu-id="be4f3-134">platform</span></span> | <span data-ttu-id="be4f3-135">Doğrudan Aracısı</span><span class="sxs-lookup"><span data-stu-id="be4f3-135">Direct Agent</span></span> | <span data-ttu-id="be4f3-136">SCOM Aracısı</span><span class="sxs-lookup"><span data-stu-id="be4f3-136">SCOM agent</span></span> | <span data-ttu-id="be4f3-137">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="be4f3-137">Azure Storage</span></span> | <span data-ttu-id="be4f3-138">SCOM gerekli?</span><span class="sxs-lookup"><span data-stu-id="be4f3-138">SCOM required?</span></span> | <span data-ttu-id="be4f3-139">Yönetim grubu gönderilen SCOM Aracısı verileri</span><span class="sxs-lookup"><span data-stu-id="be4f3-139">SCOM agent data sent via management group</span></span> | <span data-ttu-id="be4f3-140">Toplama sıklığı</span><span class="sxs-lookup"><span data-stu-id="be4f3-140">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="be4f3-141">Windows</span><span class="sxs-lookup"><span data-stu-id="be4f3-141">Windows</span></span> | <span data-ttu-id="be4f3-142">&#8226;</span><span class="sxs-lookup"><span data-stu-id="be4f3-142">&#8226;</span></span> | <span data-ttu-id="be4f3-143">&#8226;</span><span class="sxs-lookup"><span data-stu-id="be4f3-143">&#8226;</span></span> |  |  | <span data-ttu-id="be4f3-144">&#8226;</span><span class="sxs-lookup"><span data-stu-id="be4f3-144">&#8226;</span></span> |<span data-ttu-id="be4f3-145">7 gün</span><span class="sxs-lookup"><span data-stu-id="be4f3-145">7 days</span></span> |

## <a name="operations-manager-run-as-accounts-for-oms"></a><span data-ttu-id="be4f3-146">Operations Manager hesapları OMS için Çalıştır</span><span class="sxs-lookup"><span data-stu-id="be4f3-146">Operations Manager run-as accounts for OMS</span></span>
<span data-ttu-id="be4f3-147">OMS günlük analizi toplamak ve OMS hizmetine veri göndermek için Operations Manager aracısı ve yönetim grubu kullanır.</span><span class="sxs-lookup"><span data-stu-id="be4f3-147">Log Analytics in OMS uses the Operations Manager agent and management group to collect and send data to the OMS service.</span></span> <span data-ttu-id="be4f3-148">Bağlı Yönetim paketleri sağlamak iş yükleri için OMS derlemeleri değeri-hizmetlerini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="be4f3-148">OMS builds upon management packs for workloads to provide value-add services.</span></span> <span data-ttu-id="be4f3-149">Her iş yükü, bir etki alanı hesabı gibi farklı güvenlik bağlamında yönetim paketlerini çalıştırmak için iş yüküne özgü ayrıcalıkları gerektirir.</span><span class="sxs-lookup"><span data-stu-id="be4f3-149">Each workload requires workload-specific privileges to run management packs in a different security context, such as a domain account.</span></span> <span data-ttu-id="be4f3-150">Bir Operations Manager farklı çalıştır hesabı yapılandırarak kimlik bilgilerini sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="be4f3-150">You need to provide credential information by configuring an Operations Manager Run As account.</span></span>

<span data-ttu-id="be4f3-151">SQL değerlendirmesi için Operations Manager farklı çalıştırma hesabını ayarlamak için aşağıdaki bilgileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="be4f3-151">Use the following information to set the Operations Manager run-as account for SQL Assessment.</span></span>

### <a name="set-the-run-as-account-for-sql-assessment"></a><span data-ttu-id="be4f3-152">SQL değerlendirmesi için farklı çalıştır hesabı ayarlama</span><span class="sxs-lookup"><span data-stu-id="be4f3-152">Set the Run As account for SQL assessment</span></span>
 <span data-ttu-id="be4f3-153">SQL Server Yönetim Paketi zaten kullanıyorsanız, bu farklı çalıştır hesabı kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="be4f3-153">If you are already using the SQL Server management pack, you should use that Run As account.</span></span>

#### <a name="to-configure-the-sql-run-as-account-in-the-operations-console"></a><span data-ttu-id="be4f3-154">İşlemler konsolunda SQL farklı çalıştır hesabı yapılandırmak için</span><span class="sxs-lookup"><span data-stu-id="be4f3-154">To configure the SQL Run As account in the Operations console</span></span>
> [!NOTE]
> <span data-ttu-id="be4f3-155">SCOM Aracısı'nı yerine OMS doğrudan Aracısı'nı kullanıyorsanız, Yönetim Paketi her zaman yerel sistem hesabı bağlamında çalışır.</span><span class="sxs-lookup"><span data-stu-id="be4f3-155">If you are using the OMS direct agent, rather than the SCOM agent, the management pack always runs in the security context of the Local System account.</span></span> <span data-ttu-id="be4f3-156">Adım 1-aşağıdaki 5 atlayın ve T-SQL veya Powershell örnek, NT AUTHORITY\SYSTEM kullanıcı adı olarak belirterek çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="be4f3-156">Skip steps 1-5 below, and run either the T-SQL or Powershell sample, specifying NT AUTHORITY\SYSTEM as the user name.</span></span>
>
>

1. <span data-ttu-id="be4f3-157">Operations Manager işletim konsolunu açın ve ardından **Yönetim**.</span><span class="sxs-lookup"><span data-stu-id="be4f3-157">In Operations Manager, open the Operations console, and then click **Administration**.</span></span>
2. <span data-ttu-id="be4f3-158">Altında **Çalıştır Yapılandırması**, tıklatın **profilleri**, açarak **OMS SQL değerlendirmesi farklı çalıştır profili**.</span><span class="sxs-lookup"><span data-stu-id="be4f3-158">Under **Run As Configuration**, click **Profiles**, and open **OMS SQL Assessment Run As Profile**.</span></span>
3. <span data-ttu-id="be4f3-159">Üzerinde **farklı çalıştır hesapları** sayfasında, **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="be4f3-159">On the **Run As Accounts** page, click **Add**.</span></span>
4. <span data-ttu-id="be4f3-160">SQL Server için gereken kimlik bilgilerini içeren bir Windows farklı çalıştır hesabı seçin veya tıklatın **yeni** oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="be4f3-160">Select a Windows Run As account that contains the credentials needed for SQL Server, or click **New** to create one.</span></span>

   > [!NOTE]
   > <span data-ttu-id="be4f3-161">Farklı Çalıştır hesap türü Windows olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="be4f3-161">The Run As account type must be Windows.</span></span> <span data-ttu-id="be4f3-162">Farklı Çalıştır hesabı, aynı zamanda SQL Server örneklerini barındıran tüm Windows sunucularında yerel Administrators grubunun bir parçası olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="be4f3-162">The Run As account must also be part of Local Administrators group on all Windows Servers hosting SQL Server Instances.</span></span>
   >
   >
5. <span data-ttu-id="be4f3-163">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="be4f3-163">Click **Save**.</span></span>
6. <span data-ttu-id="be4f3-164">Değiştirin ve sonra aşağıdaki T-SQL örneği her SQL Server SQL değerlendirmesi gerçekleştirmek için farklı çalıştır hesabı için gerekli minimum izinleri vermek için örneğinde yürütün.</span><span class="sxs-lookup"><span data-stu-id="be4f3-164">Modify and then execute the following T-SQL sample on each SQL Server Instance to grant minimum permissions required to Run As Account to perform SQL Assessment.</span></span> <span data-ttu-id="be4f3-165">Ancak, bir farklı çalıştır hesabı SQL Server örnekleri üzerindeki sysadmin sunucu rolünün bir parçası ise bu yapmanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="be4f3-165">However, you don’t need to do this if a Run As Account is already part of the sysadmin server role on SQL Server Instances.</span></span>

```
---
    -- Replace <UserName> with the actual user name being used as Run As Account.
    USE master

    -- Create login for the user, comment this line if login is already created.
    CREATE LOGIN [<UserName>] FROM WINDOWS

    -- Grant permissions to user.
    GRANT VIEW SERVER STATE TO [<UserName>]
    GRANT VIEW ANY DEFINITION TO [<UserName>]
    GRANT VIEW ANY DATABASE TO [<UserName>]

    -- Add database user for all the databases on SQL Server Instance, this is required for connecting to individual databases.
    -- NOTE: This command must be run anytime new databases are added to SQL Server instances.
    EXEC sp_msforeachdb N'USE [?]; CREATE USER [<UserName>] FOR LOGIN [<UserName>];'

```
#### <a name="to-configure-the-sql-run-as-account-using-windows-powershell"></a><span data-ttu-id="be4f3-166">Windows PowerShell kullanarak SQL farklı çalıştır hesabını yapılandırmak için</span><span class="sxs-lookup"><span data-stu-id="be4f3-166">To configure the SQL Run As account using Windows PowerShell</span></span>
<span data-ttu-id="be4f3-167">Bir PowerShell penceresi açın ve bilgilerinizle güncelleştirdikten sonra aşağıdaki betiği çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="be4f3-167">Open a PowerShell window and run the following script after you’ve updated it with your information:</span></span>

```

    import-module OperationsManager
    New-SCOMManagementGroupConnection "<your management group name>"

    $profile = Get-SCOMRunAsProfile -DisplayName "OMS SQL Assessment Run As Profile"
    $account = Get-SCOMrunAsAccount | Where-Object {$_.Name -eq "<your run as account name>"}
    Set-SCOMRunAsProfile -Action "Add" -Profile $Profile -Account $Account
```

## <a name="understanding-how-recommendations-are-prioritized"></a><span data-ttu-id="be4f3-168">Önerilerin nasıl önceliklendirilir anlama</span><span class="sxs-lookup"><span data-stu-id="be4f3-168">Understanding how recommendations are prioritized</span></span>
<span data-ttu-id="be4f3-169">Yapılan her öneri öneri göreceli önemini tanımlayan bir ağırlıklı değer verilir.</span><span class="sxs-lookup"><span data-stu-id="be4f3-169">Every recommendation made is given a weighting value that identifies the relative importance of the recommendation.</span></span> <span data-ttu-id="be4f3-170">Yalnızca on en önemli öneriler gösterilir.</span><span class="sxs-lookup"><span data-stu-id="be4f3-170">Only the ten most important recommendations are shown.</span></span>

### <a name="how-weights-are-calculated"></a><span data-ttu-id="be4f3-171">Ağırlıkları nasıl hesaplanır</span><span class="sxs-lookup"><span data-stu-id="be4f3-171">How weights are calculated</span></span>
<span data-ttu-id="be4f3-172">Ağırlık belirlemeyi üç anahtar faktörlerini temel alarak toplam değerler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="be4f3-172">Weightings are aggregate values based on three key factors:</span></span>

* <span data-ttu-id="be4f3-173">*Olasılık* tanımlanan bir sorunun sorunlara neden.</span><span class="sxs-lookup"><span data-stu-id="be4f3-173">The *probability* that an issue identified will cause problems.</span></span> <span data-ttu-id="be4f3-174">Daha yüksek olasılık öneri için daha büyük bir genel puan karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="be4f3-174">A higher probability equates to a larger overall score for the recommendation.</span></span>
* <span data-ttu-id="be4f3-175">*Etkisi* kuruluşunuzdaki bir soruna neden olursa sorun.</span><span class="sxs-lookup"><span data-stu-id="be4f3-175">The *impact* of the issue on your organization if it does cause a problem.</span></span> <span data-ttu-id="be4f3-176">Daha yüksek bir etkisi öneri için daha büyük bir genel puan karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="be4f3-176">A higher impact equates to a larger overall score for the recommendation.</span></span>
* <span data-ttu-id="be4f3-177">*Çaba* öneriyi uygulamak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="be4f3-177">The *effort* required to implement the recommendation.</span></span> <span data-ttu-id="be4f3-178">Daha yüksek çaba öneri için daha küçük bir genel puan karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="be4f3-178">A higher effort equates to a smaller overall score for the recommendation.</span></span>

<span data-ttu-id="be4f3-179">Her öneri ağırlıklı her odak alanı için kullanılabilir toplam puanı yüzdesi olarak ifade edilir.</span><span class="sxs-lookup"><span data-stu-id="be4f3-179">The weighting for each recommendation is expressed as a percentage of the total score available for each focus area.</span></span> <span data-ttu-id="be4f3-180">Güvenlik ve uyumluluk odak alanında bir öneri %5 puanı varsa, örneğin, bu öneri uygulama, genel güvenlik ve uyumluluk puan tarafından %5 artacaktır.</span><span class="sxs-lookup"><span data-stu-id="be4f3-180">For example, if a recommendation in the Security and Compliance focus area has a score of 5%, implementing that recommendation will increase your overall Security and Compliance score by 5%.</span></span>

### <a name="focus-areas"></a><span data-ttu-id="be4f3-181">Odak alanları</span><span class="sxs-lookup"><span data-stu-id="be4f3-181">Focus areas</span></span>
<span data-ttu-id="be4f3-182">**Güvenlik ve Uyumluluk** -bu odak alanı olası güvenlik tehditlerini ve ihlallerinden, şirket ilkelerini ve teknik ve yasal uyumluluk gereksinimleri için öneriler gösterir.</span><span class="sxs-lookup"><span data-stu-id="be4f3-182">**Security and Compliance** - This focus area shows recommendations for potential security threats and breaches, corporate policies, and technical, legal and regulatory compliance requirements.</span></span>

<span data-ttu-id="be4f3-183">**Kullanılabilirlik ve iş sürekliliği** -bu odaklanılan alan hizmet kullanılabilirliği, altyapı ve iş koruması dayanıklılık için öneriler gösterir.</span><span class="sxs-lookup"><span data-stu-id="be4f3-183">**Availability and Business Continuity** - This focus area shows recommendations for service availability, resiliency of your infrastructure, and business protection.</span></span>

<span data-ttu-id="be4f3-184">**Performans ve ölçeklenebilirlik** -bu odak alanı kuruluşunuzun yardımcı olacak öneriler gösterir BT altyapısı arttıkça, BT ortamınız geçerli performans gereksinimlerini karşıladığından ve altyapı değiştirmeye yanıt verebilmesini olduğundan emin olun gerekir.</span><span class="sxs-lookup"><span data-stu-id="be4f3-184">**Performance and Scalability** - This focus area shows recommendations to help your organization's IT infrastructure grow, ensure that your IT environment meets current performance requirements, and is able to respond to changing infrastructure needs.</span></span>

<span data-ttu-id="be4f3-185">**Yükseltme, geçiş ve dağıtım** -bu odak alanı, yükseltme, geçirme ve SQL Server mevcut altyapınızda dağıtmanıza yardımcı olacak öneriler gösterir.</span><span class="sxs-lookup"><span data-stu-id="be4f3-185">**Upgrade, Migration and Deployment** - This focus area shows recommendations to help you upgrade, migrate, and deploy SQL Server to your existing infrastructure.</span></span>

<span data-ttu-id="be4f3-186">**İşlemler ve izleme** -bu odak alanı BT işlemlerinizi kolaylaştırır, önleyici bakım uygulamak ve performansı en üst düzeye çıkarmanıza yardımcı olacak öneriler gösterir.</span><span class="sxs-lookup"><span data-stu-id="be4f3-186">**Operations and Monitoring** - This focus area shows recommendations to help streamline your IT operations, implement preventative maintenance, and maximize performance.</span></span>

<span data-ttu-id="be4f3-187">**Değişiklik ve yapılandırma yönetimi** -bu odak alanı günlük işlemlerini korumak, değişiklikleri yok olumsuz altyapınızı etkiler, değişiklik denetim yordamları kurmak emin olun yardımcı olmak için izleme ve denetim için öneriler gösterir Sistem yapılandırması.</span><span class="sxs-lookup"><span data-stu-id="be4f3-187">**Change and Configuration Management** - This focus area shows recommendations to help protect day-to-day operations, ensure that changes don't negatively affect your infrastructure, establish change control procedures, and to track and audit system configurations.</span></span>

### <a name="should-you-aim-to-score-100-in-every-focus-area"></a><span data-ttu-id="be4f3-188">Her odaklanılan alan % 100 puanlı hedefleyin?</span><span class="sxs-lookup"><span data-stu-id="be4f3-188">Should you aim to score 100% in every focus area?</span></span>
<span data-ttu-id="be4f3-189">Olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="be4f3-189">Not necessarily.</span></span> <span data-ttu-id="be4f3-190">Öneriler bilgi ve müşteri ziyaretleriniz binlerce arasında Microsoft mühendisleri tarafından elde edilen deneyimleri temel alır.</span><span class="sxs-lookup"><span data-stu-id="be4f3-190">The recommendations are based on the knowledge and experiences gained by Microsoft engineers across thousands of customer visits.</span></span> <span data-ttu-id="be4f3-191">Ancak, iki sunucu altyapılar aynıdır ve özel öneriler için daha az veya uygun olabilir.</span><span class="sxs-lookup"><span data-stu-id="be4f3-191">However, no two server infrastructures are the same, and specific recommendations may be more or less relevant to you.</span></span> <span data-ttu-id="be4f3-192">Örneğin, bazı güvenlik önerileri sanal makinelerinizi Internet'e açık değildir, daha az ilgili olabilir.</span><span class="sxs-lookup"><span data-stu-id="be4f3-192">For example, some security recommendations might be less relevant if your virtual machines are not exposed to the Internet.</span></span> <span data-ttu-id="be4f3-193">Bazı kullanılabilirlik öneriler düşük öncelik geçici veri toplama ve raporlama sağladığı hizmetler için daha az uygun olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="be4f3-193">Some availability recommendations may be less relevant for services that provide low priority ad hoc data collection and reporting.</span></span> <span data-ttu-id="be4f3-194">Olgun bir iş için önemli olan sorunları bir başlangıcından daha az önemli olabilir.</span><span class="sxs-lookup"><span data-stu-id="be4f3-194">Issues that are important to a mature business may be less important to a start-up.</span></span> <span data-ttu-id="be4f3-195">Hangi odak alanların önceliklerinizden olduğunu belirlemek ve, puanları zamanla nasıl değiştiğini adresindeki Ara isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="be4f3-195">You may want to identify which focus areas are your priorities and then look at how your scores change over time.</span></span>

<span data-ttu-id="be4f3-196">Her öneri neden önemli olduğu hakkında yönergeler içerir.</span><span class="sxs-lookup"><span data-stu-id="be4f3-196">Every recommendation includes guidance about why it is important.</span></span> <span data-ttu-id="be4f3-197">Öneri uygulama verilen BT hizmetlerinizi yapısını ve kuruluşunuzun iş gereksinimlerini sizin için uygun olup olmadığını değerlendirmek için bu yönergeleri kullanmanız.</span><span class="sxs-lookup"><span data-stu-id="be4f3-197">You should use this guidance to evaluate whether implementing the recommendation is appropriate for you, given the nature of your IT services and the business needs of your organization.</span></span>

## <a name="use-assessment-focus-area-recommendations"></a><span data-ttu-id="be4f3-198">Değerlendirme odak alanı önerileri kullanın</span><span class="sxs-lookup"><span data-stu-id="be4f3-198">Use assessment focus area recommendations</span></span>
<span data-ttu-id="be4f3-199">OMS içinde bir değerlendirme çözümü kullanmadan önce çözümü yüklenmiş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="be4f3-199">Before you can use an assessment solution in OMS, you must have the solution installed.</span></span> <span data-ttu-id="be4f3-200">Daha fazla bilgi için çözümleri yükleme hakkında bkz [Çözümleri Galerisi eklemek günlük analizi çözümleri](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="be4f3-200">To read more about installing solutions, see [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span> <span data-ttu-id="be4f3-201">Yüklendikten sonra OMS genel bakış sayfasında SQL değerlendirmesi döşeme kullanarak önerileri özetini görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="be4f3-201">After it is installed, you can view the summary of recommendations by using the SQL Assessment tile on the Overview page in OMS.</span></span>

<span data-ttu-id="be4f3-202">Altyapınız ve ardından-ayrıntıya önerileri için özetlenmiş uyumluluk değerlendirmesi görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="be4f3-202">View the summarized compliance assessments for your infrastructure and then drill-into recommendations.</span></span>

### <a name="to-view-recommendations-for-a-focus-area-and-take-corrective-action"></a><span data-ttu-id="be4f3-203">Odak alanı için öneriler görüntülemek ve düzeltici işlemleri için</span><span class="sxs-lookup"><span data-stu-id="be4f3-203">To view recommendations for a focus area and take corrective action</span></span>
1. <span data-ttu-id="be4f3-204">Üzerinde **genel bakış** sayfasında, **SQL değerlendirmesi** döşeme.</span><span class="sxs-lookup"><span data-stu-id="be4f3-204">On the **Overview** page, click the **SQL Assessment** tile.</span></span>
2. <span data-ttu-id="be4f3-205">Üzerinde **SQL değerlendirmesi** sayfasında odak alanı Kanatlar birinde özet bilgilerini inceleyin ve sonra bu odak alanı için öneriler görüntülemek için tıklatın.</span><span class="sxs-lookup"><span data-stu-id="be4f3-205">On the **SQL Assessment** page, review the summary information in one of the focus area blades and then click one to view recommendations for that focus area.</span></span>
3. <span data-ttu-id="be4f3-206">Odak alanı sayfaları hiçbirinde ortamınız için öncelikli önerilerin görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="be4f3-206">On any of the focus area pages, you can view the prioritized recommendations made for your environment.</span></span> <span data-ttu-id="be4f3-207">Önerinin altında tıklatın **etkilenen nesneleri** öneri neden yapılan hakkında ayrıntıları görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="be4f3-207">Click a recommendation under **Affected Objects** to view details about why the recommendation is made.</span></span>  
    <span data-ttu-id="be4f3-208">![SQL değerlendirmesi önerileri görüntüsü](./media/log-analytics-sql-assessment/sql-assess-focus.png)</span><span class="sxs-lookup"><span data-stu-id="be4f3-208">![image of SQL Assessment recommendations](./media/log-analytics-sql-assessment/sql-assess-focus.png)</span></span>
4. <span data-ttu-id="be4f3-209">Önerilen düzeltici eylemleri gerçekleştirebilirsiniz **önerilen eylemleri**.</span><span class="sxs-lookup"><span data-stu-id="be4f3-209">You can take corrective actions suggested in **Suggested Actions**.</span></span> <span data-ttu-id="be4f3-210">Öğe ele, önerilen eylemler gerçekleştirilen ve uyumluluk puan artıracaktır sonraki değerlendirmeleri kaydeder.</span><span class="sxs-lookup"><span data-stu-id="be4f3-210">When the item has been addressed, later assessments will record that recommended actions were taken and your compliance score will increase.</span></span> <span data-ttu-id="be4f3-211">Düzeltilmiş öğeler görünür olarak **geçirilen nesneleri**.</span><span class="sxs-lookup"><span data-stu-id="be4f3-211">Corrected items appear as **Passed Objects**.</span></span>

## <a name="ignore-recommendations"></a><span data-ttu-id="be4f3-212">Öneriler yoksay</span><span class="sxs-lookup"><span data-stu-id="be4f3-212">Ignore recommendations</span></span>
<span data-ttu-id="be4f3-213">Yoksay istediğiniz önerileri varsa, OMS önerileri değerlendirme sonuçlarında görünmesini engellemek için kullanacağı bir metin dosyası oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="be4f3-213">If you have recommendations that you want to ignore, you can create a text file that OMS will use to prevent recommendations from appearing in your assessment results.</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

### <a name="to-identify-recommendations-that-you-will-ignore"></a><span data-ttu-id="be4f3-214">Göz ardı eder önerileri tanımlamak için</span><span class="sxs-lookup"><span data-stu-id="be4f3-214">To identify recommendations that you will ignore</span></span>
1. <span data-ttu-id="be4f3-215">Sunucunuzdan çalışma alanınıza oturum açın ve günlük arama açın.</span><span class="sxs-lookup"><span data-stu-id="be4f3-215">Sign in to your workspace and open Log Search.</span></span> <span data-ttu-id="be4f3-216">Ortamınızdaki bilgisayarları için başarısız olan liste önerileri için aşağıdaki sorguyu kullanın.</span><span class="sxs-lookup"><span data-stu-id="be4f3-216">Use the following query to list recommendations that have failed for computers in your environment.</span></span>

   ```
   Type=SQLAssessmentRecommendation RecommendationResult=Failed | select  Computer, RecommendationId, Recommendation | sort  Computer
   ```

   <span data-ttu-id="be4f3-217">Günlük arama sorgusu gösteren ekran görüntüsü şöyledir: ![önerileri başarısız oldu](./media/log-analytics-sql-assessment/sql-assess-failed-recommendations.png)</span><span class="sxs-lookup"><span data-stu-id="be4f3-217">Here's a screen shot showing the Log Search query: ![failed recommendations](./media/log-analytics-sql-assessment/sql-assess-failed-recommendations.png)</span></span>
2. <span data-ttu-id="be4f3-218">Yoksay istediğiniz önerileri seçin.</span><span class="sxs-lookup"><span data-stu-id="be4f3-218">Choose recommendations that you want to ignore.</span></span> <span data-ttu-id="be4f3-219">Sonraki yordamda Recommendationıd için değerleri kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="be4f3-219">You’ll use the values for RecommendationId in the next procedure.</span></span>

### <a name="to-create-and-use-an-ignorerecommendationstxt-text-file"></a><span data-ttu-id="be4f3-220">Oluşturma ve bir IgnoreRecommendations.txt metin dosyası kullanma</span><span class="sxs-lookup"><span data-stu-id="be4f3-220">To create and use an IgnoreRecommendations.txt text file</span></span>
1. <span data-ttu-id="be4f3-221">IgnoreRecommendations.txt adlı bir dosya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="be4f3-221">Create a file named IgnoreRecommendations.txt.</span></span>
2. <span data-ttu-id="be4f3-222">Her Recommendationıd ayrı bir satırda yoksay ve sonra dosyayı kaydedip kapatın için OMS istediğiniz her bir öneri için yazın veya yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="be4f3-222">Paste or type each RecommendationId for each recommendation that you want OMS to ignore on a separate line and then save and close the file.</span></span>
3. <span data-ttu-id="be4f3-223">Dosya aşağıdaki klasörde önerileri yoksaymak için OMS istediğiniz her bilgisayara yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="be4f3-223">Put the file in the following folder on each computer where you want OMS to ignore recommendations.</span></span>
   * <span data-ttu-id="be4f3-224">Microsoft Monitoring (doğrudan veya Operations Manager aracılığıyla bağlı) Agent - olan bilgisayarlarda *SystemDrive*: \Program izleme Agent\Agent</span><span class="sxs-lookup"><span data-stu-id="be4f3-224">On computers with the Microsoft Monitoring Agent (connected directly or through Operations Manager) - *SystemDrive*:\Program Files\Microsoft Monitoring Agent\Agent</span></span>
   * <span data-ttu-id="be4f3-225">Operations Manager yönetim sunucusunda - *SystemDrive*: \Program System Center 2012 R2\Operations Manager\Server</span><span class="sxs-lookup"><span data-stu-id="be4f3-225">On the Operations Manager management server - *SystemDrive*:\Program Files\Microsoft System Center 2012 R2\Operations Manager\Server</span></span>

### <a name="to-verify-that-recommendations-are-ignored"></a><span data-ttu-id="be4f3-226">Öneriler göz ardı edilir doğrulamak için</span><span class="sxs-lookup"><span data-stu-id="be4f3-226">To verify that recommendations are ignored</span></span>
1. <span data-ttu-id="be4f3-227">Sonraki değerlendirme çalıştığında, varsayılan olarak 7 günde zamanlanmış sonra belirtilen önerileri yoksayıldı işaretlenir ve değerlendirme Panoda görünmez.</span><span class="sxs-lookup"><span data-stu-id="be4f3-227">After the next scheduled assessment runs, by default every 7 days, the specified recommendations are marked Ignored and will not appear on the assessment dashboard.</span></span>
2. <span data-ttu-id="be4f3-228">Tüm yoksayılan öneriler listelemek için aşağıdaki günlük arama sorgularını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="be4f3-228">You can use the following Log Search queries to list all the ignored recommendations.</span></span>

   ```
   Type=SQLAssessmentRecommendation RecommendationResult=Ignored | select  Computer, RecommendationId, Recommendation | sort  Computer
   ```
3. <span data-ttu-id="be4f3-229">Daha sonra yoksayılan önerileri görmek istediğiniz karar verirseniz, tüm IgnoreRecommendations.txt dosyaları silin veya bunları RecommendationIDs kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="be4f3-229">If you decide later that you want to see ignored recommendations, remove any IgnoreRecommendations.txt files, or you can remove RecommendationIDs from them.</span></span>

## <a name="sql-assessment-solution-faq"></a><span data-ttu-id="be4f3-230">SQL değerlendirme çözümü hakkında SSS</span><span class="sxs-lookup"><span data-stu-id="be4f3-230">SQL Assessment solution FAQ</span></span>
<span data-ttu-id="be4f3-231">*Sıklıkla bir değerlendirme çalışıyor mu?*</span><span class="sxs-lookup"><span data-stu-id="be4f3-231">*How often does an assessment run?*</span></span>

* <span data-ttu-id="be4f3-232">Değerlendirme 7 günde bir çalışır.</span><span class="sxs-lookup"><span data-stu-id="be4f3-232">The assessment runs every 7 days.</span></span>

<span data-ttu-id="be4f3-233">*Ne sıklıkta değerlendirme çalıştıran yapılandırmak için yolu var mı?*</span><span class="sxs-lookup"><span data-stu-id="be4f3-233">*Is there a way to configure how often the assessment runs?*</span></span>

* <span data-ttu-id="be4f3-234">Şu anda değil.</span><span class="sxs-lookup"><span data-stu-id="be4f3-234">Not at this time.</span></span>

<span data-ttu-id="be4f3-235">*T SQL değerlendirme çözümü ekledikten sonra başka bir sunucuya belirlediyseniz değerlendirileceğini?*</span><span class="sxs-lookup"><span data-stu-id="be4f3-235">*If another server is discovered after I’ve added the SQL assessment solution, will it be assessed?*</span></span>

* <span data-ttu-id="be4f3-236">Evet, bunu daha sonra gelen her 7 günde değerlendirildiği bulunduktan sonra.</span><span class="sxs-lookup"><span data-stu-id="be4f3-236">Yes, once it is discovered it is assessed from then on, every 7 days.</span></span>

<span data-ttu-id="be4f3-237">*Ne zaman bir sunucu kullanımdan alındığında değerlendirme kaldırılacak?*</span><span class="sxs-lookup"><span data-stu-id="be4f3-237">*If a server is decommissioned, when will it be removed from the assessment?*</span></span>

* <span data-ttu-id="be4f3-238">Bir sunucu için 3 hafta veri göndermez, kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="be4f3-238">If a server does not submit data for 3 weeks, it is removed.</span></span>

<span data-ttu-id="be4f3-239">*Veri toplama mu işlemin adı nedir?*</span><span class="sxs-lookup"><span data-stu-id="be4f3-239">*What is the name of the process that does the data collection?*</span></span>

* <span data-ttu-id="be4f3-240">AdvisorAssessment.exe</span><span class="sxs-lookup"><span data-stu-id="be4f3-240">AdvisorAssessment.exe</span></span>

<span data-ttu-id="be4f3-241">*Ne kadar süreyle verilerinin toplanmasını sürer?*</span><span class="sxs-lookup"><span data-stu-id="be4f3-241">*How long does it take for data to be collected?*</span></span>

* <span data-ttu-id="be4f3-242">Gerçek veri toplama sunucusundaki yaklaşık 1 saat sürer.</span><span class="sxs-lookup"><span data-stu-id="be4f3-242">The actual data collection on the server takes about 1 hour.</span></span> <span data-ttu-id="be4f3-243">Bu çok sayıda SQL örnekleri veya veritabanlarına sahip sunucularda uzun sürebilir.</span><span class="sxs-lookup"><span data-stu-id="be4f3-243">It may take longer on servers that have a large number of SQL instances or databases.</span></span>

<span data-ttu-id="be4f3-244">*Hangi türde veri toplanır?*</span><span class="sxs-lookup"><span data-stu-id="be4f3-244">*What type of data is collected?*</span></span>

* <span data-ttu-id="be4f3-245">Aşağıdaki veri türlerini toplanır:</span><span class="sxs-lookup"><span data-stu-id="be4f3-245">The following types of data are collected:</span></span>
  * <span data-ttu-id="be4f3-246">WMI</span><span class="sxs-lookup"><span data-stu-id="be4f3-246">WMI</span></span>
  * <span data-ttu-id="be4f3-247">Kayıt defteri</span><span class="sxs-lookup"><span data-stu-id="be4f3-247">Registry</span></span>
  * <span data-ttu-id="be4f3-248">Performans sayaçları</span><span class="sxs-lookup"><span data-stu-id="be4f3-248">Performance counters</span></span>
  * <span data-ttu-id="be4f3-249">SQL Dinamik Yönetim görünümlerini (DMV).</span><span class="sxs-lookup"><span data-stu-id="be4f3-249">SQL dynamic management views (DMV).</span></span>

<span data-ttu-id="be4f3-250">*Verileri toplandığında yapılandırmak için yolu var mı?*</span><span class="sxs-lookup"><span data-stu-id="be4f3-250">*Is there a way to configure when data is collected?*</span></span>

* <span data-ttu-id="be4f3-251">Şu anda değil.</span><span class="sxs-lookup"><span data-stu-id="be4f3-251">Not at this time.</span></span>

<span data-ttu-id="be4f3-252">*Bir farklı çalıştır hesabı yapılandırmak neden var mı?*</span><span class="sxs-lookup"><span data-stu-id="be4f3-252">*Why do I have to configure a Run As Account?*</span></span>

* <span data-ttu-id="be4f3-253">SQL Server için SQL sorguları az sayıda çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="be4f3-253">For SQL Server, a small number of SQL queries are run.</span></span> <span data-ttu-id="be4f3-254">Bir farklı çalıştır hesabı SQL VIEW SERVER STATE izni olan çalışmasını sırayla kullanılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="be4f3-254">In order for them to run, a Run As Account with VIEW SERVER STATE permissions to SQL must be used.</span></span>  <span data-ttu-id="be4f3-255">Ayrıca, WMI sorgusu için yerel yönetici kimlik bilgileri gereklidir.</span><span class="sxs-lookup"><span data-stu-id="be4f3-255">In addition, in order to query WMI, local administrator credentials are required.</span></span>

<span data-ttu-id="be4f3-256">*Neden yalnızca ilk 10 önerileri görüntülemek?*</span><span class="sxs-lookup"><span data-stu-id="be4f3-256">*Why display only the top 10 recommendations?*</span></span>

* <span data-ttu-id="be4f3-257">Görevler kapsamlı bir zorlamayı listesi vermek yerine, Önceliklendirilmiş önerileri adresleme odaklanmak öneririz.</span><span class="sxs-lookup"><span data-stu-id="be4f3-257">Instead of giving you an exhaustive overwhelming list of tasks, we recommend that you focus on addressing the prioritized recommendations first.</span></span> <span data-ttu-id="be4f3-258">Bunları çözün sonra ek öneriler kullanılabilir hale gelir.</span><span class="sxs-lookup"><span data-stu-id="be4f3-258">After you address them, additional recommendations will become available.</span></span> <span data-ttu-id="be4f3-259">Ayrıntılı listesini görmek isterseniz, OMS günlük arama özelliğini kullanarak tüm önerileri görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="be4f3-259">If you prefer to see the detailed list, you can view all recommendations using the OMS log search.</span></span>

<span data-ttu-id="be4f3-260">*Bir öneri yoksaymak için yolu var mı?*</span><span class="sxs-lookup"><span data-stu-id="be4f3-260">*Is there a way to ignore a recommendation?*</span></span>

* <span data-ttu-id="be4f3-261">Evet, bkz: [önerileri yoksay](#ignore-recommendations) yukarıdaki bölümde.</span><span class="sxs-lookup"><span data-stu-id="be4f3-261">Yes, see [Ignore recommendations](#ignore-recommendations) section above.</span></span>

## <a name="next-steps"></a><span data-ttu-id="be4f3-262">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="be4f3-262">Next steps</span></span>
* <span data-ttu-id="be4f3-263">[Arama günlüklerini](log-analytics-log-searches.md) ayrıntılı SQL Değerlendirme verileri ve öneriler görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="be4f3-263">[Search logs](log-analytics-log-searches.md) to view detailed SQL Assessment data and recommendations.</span></span>
