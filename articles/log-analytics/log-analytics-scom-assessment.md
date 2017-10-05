---
title: "System Center Operations Manager ortamınızı Azure günlük analizi ile en iyi duruma getirme | Microsoft Docs"
description: "System Center Operations Manager değerlendirme çözüm, risk ve sunucu ortamlarınızın durumunu düzenli aralıklarla değerlendirmek için kullanabilirsiniz."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: tysonn
ms.assetid: 49aad8b1-3e05-4588-956c-6fdd7715cda1
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/11/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4992d98397da409f7c1cfbdeb40fdb0cdd0d2f19
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="optimize-your-environment-with-the-system-center-operations-manager-assessment-preview-solution"></a><span data-ttu-id="fc469-103">Ortamınızı System Center Operations Manager değerlendirme (Önizleme) çözümü ile en iyi duruma getirme</span><span class="sxs-lookup"><span data-stu-id="fc469-103">Optimize your environment with the System Center Operations Manager Assessment (Preview) solution</span></span>

![System Center Operations Manager değerlendirme simgesi](./media/log-analytics-scom-assessment/scom-assessment-symbol.png)

<span data-ttu-id="fc469-105">System Center Operations Manager değerlendirme çözüm, risk ve System Center Operations Manager server ortamlarınızın durumunu düzenli aralıklarla değerlendirmek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fc469-105">You can use the System Center Operations Manager Assessment solution to assess the risk and health of your System Center Operations Manager server environments on a regular interval.</span></span> <span data-ttu-id="fc469-106">Bu makalede, yükleme, yapılandırma ve olası sorunlar için düzeltme eylemleri yararlanabilmeniz çözümü kullanan yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="fc469-106">This article helps you install, configure, and use the solution so that you can take corrective actions for potential problems.</span></span>

<span data-ttu-id="fc469-107">Bu çözüm önerileri dağıtılan sunucu altyapınızı belirli öncelikli listesi sağlar.</span><span class="sxs-lookup"><span data-stu-id="fc469-107">This solution provides a prioritized list of recommendations specific to your deployed server infrastructure.</span></span> <span data-ttu-id="fc469-108">Öneriler dört arasında ayrılır hızlı bir şekilde Yardım odak alanlarına riski anlamak ve düzeltme eylemlerini gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="fc469-108">The recommendations are categorized across four focus areas, which help you quickly understand the risk and take corrective action.</span></span>

<span data-ttu-id="fc469-109">Önerilerin bilgi ve müşteri ziyaretleriniz binlerce Microsoft mühendisleri tarafından elde edilen deneyimlerden dayanır.</span><span class="sxs-lookup"><span data-stu-id="fc469-109">The recommendations made are based on the knowledge and experience gained by Microsoft engineers from thousands of customer visits.</span></span> <span data-ttu-id="fc469-110">Her bir öneri, bir sorun için neden önemli ve önerilen değişiklikleri uygulamak nasıl hakkında rehberlik sağlar.</span><span class="sxs-lookup"><span data-stu-id="fc469-110">Each recommendation provides guidance about why an issue might matter to you and how to implement the suggested changes.</span></span>

<span data-ttu-id="fc469-111">Kuruluşunuz için en önemli ve ücretsiz ve sağlam bir risk ortam çalıştıran doğru ilerleme durumunuzu izlemenize odak alanlarına seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fc469-111">You can choose focus areas that are most important to your organization and track your progress toward running a risk free and healthy environment.</span></span>

<span data-ttu-id="fc469-112">Çözüm ekledik ve bir değerlendirme tamamlanan, Özet sonra odak alanlarına odaklanmak için bilgi gösterilir **System Center Operations Manager değerlendirme** altyapınız için Pano.</span><span class="sxs-lookup"><span data-stu-id="fc469-112">After you've added the solution and an assessment is completed, summary information for focus areas is shown on the **System Center Operations Manager Assessment** dashboard for your infrastructure.</span></span> <span data-ttu-id="fc469-113">Aşağıdaki bölümlerde bilgileri üzerinde nasıl kullanacağınızı **System Center Operations Manager değerlendirme** Pano, burada görüntüleyebilir ve ardından uygulayın Eylemler SCOM altyapınız için önerilen.</span><span class="sxs-lookup"><span data-stu-id="fc469-113">The following sections describe how to use the information on the **System Center Operations Manager Assessment** dashboard, where you can view and then take recommended actions for your SCOM infrastructure.</span></span>

![System Center Operations Manager çözüm döşeme](./media/log-analytics-scom-assessment/scom-tile.png)

![System Center Operations Manager değerlendirme Panosu](./media/log-analytics-scom-assessment/scom-dashboard01.png)

## <a name="installing-and-configuring-the-solution"></a><span data-ttu-id="fc469-116">Yükleme ve çözüm yapılandırılıyor</span><span class="sxs-lookup"><span data-stu-id="fc469-116">Installing and configuring the solution</span></span>

<span data-ttu-id="fc469-117">Çözüm, Microsoft System Operations Manager 2012 R2 ve 2012 SP1 ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="fc469-117">The solution works with Microsoft System Operations Manager 2012 R2 and 2012 SP1.</span></span>

<span data-ttu-id="fc469-118">Yüklemek ve çözüm yapılandırmak için aşağıdaki bilgileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="fc469-118">Use the following information to install and configure the solution.</span></span>

 - <span data-ttu-id="fc469-119">OMS içinde bir değerlendirme çözümü kullanmadan önce çözümü yüklenmiş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="fc469-119">Before you can use an assessment solution in OMS, you must have the solution installed.</span></span> <span data-ttu-id="fc469-120">Çözümden yüklemek [Azure Market](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.SCOMAssessmentOMS?tab=Overview) ya da'ndaki yönergeleri izleyerek [Çözümleri Galerisi eklemek günlük analizi çözümleri](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="fc469-120">Install the solution from [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.SCOMAssessmentOMS?tab=Overview) or by following the instructions in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>

 - <span data-ttu-id="fc469-121">Çözüm için çalışma alanına ekledikten sonra System Center Operations Manager değerlendirme döşemenin Panoda ek yapılandırma gerekli iletisi görüntüler.</span><span class="sxs-lookup"><span data-stu-id="fc469-121">After adding the solution to the workspace, the System Center Operations Manager Assessment tile on the dashboard displays the additional configuration required message.</span></span> <span data-ttu-id="fc469-122">Kutucuğuna tıklayın ve sayfasında belirtilen yapılandırma adımlarını izleyin</span><span class="sxs-lookup"><span data-stu-id="fc469-122">Click on the tile and follow the configuration steps mentioned in the page</span></span>

 ![System Center Operations Manager Pano kutucuğu](./media/log-analytics-scom-assessment/scom-configrequired-tile.png)

 <span data-ttu-id="fc469-124">System Center Operations Manager yapılandırmasını OMS çözümde yapılandırma sayfasında belirtilen adımları izleyerek komut dosyası aracılığıyla gerçekleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="fc469-124">Configuration of the System Center Operations Manager can be done through the script by following the steps mentioned in the configuration page of the solution in OMS.</span></span>

 <span data-ttu-id="fc469-125">Bunun yerine, değerlendirmesi SCOM konsolu üzerinden yapılandırmak için izleyin aşağıdaki adımları aynı sırada</span><span class="sxs-lookup"><span data-stu-id="fc469-125">Instead, to configure the assessment through SCOM Console, follow the below steps in the same order</span></span>
1. [<span data-ttu-id="fc469-126">System Center Operations Manager değerlendirmesi için farklı çalıştır hesabı ayarlama</span><span class="sxs-lookup"><span data-stu-id="fc469-126">Set the Run As account for System Center Operations Manager Assessment</span></span>](#operations-manager-run-as-accounts-for-oms)  
2. [<span data-ttu-id="fc469-127">System Center Operations Manager değerlendirme kuralı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="fc469-127">Configure the System Center Operations Manager Assessment rule</span></span>](#configure-the-assessment-rule)

## <a name="system-center-operations-manager-assessment-data-collection-details"></a><span data-ttu-id="fc469-128">System Center Operations Manager değerlendirme veri toplama ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="fc469-128">System Center Operations Manager assessment data collection details</span></span>

<span data-ttu-id="fc469-129">System Center Operations Manager değerlendirme WMI verilerini, kayıt defteri verilerini, olay günlüğü verilerini, Windows PowerShell, SQL sorguları, dosya bilgileri Toplayıcı etkinleştirdiğiniz kullanarak sunucu üzerinden Operations Manager veri toplar.</span><span class="sxs-lookup"><span data-stu-id="fc469-129">The System Center Operations Manager assessment collects WMI data, Registry data, EventLog data, Operations Manager data through Windows PowerShell, SQL Queries, File information collector using the server that you have enabled.</span></span>

<span data-ttu-id="fc469-130">Aşağıdaki tabloda System Center Operations Manager değerlendirmesi için veri toplama yöntemi gösterir ve ne sıklıkta bir aracı tarafından toplanan veriler.</span><span class="sxs-lookup"><span data-stu-id="fc469-130">The following table shows data collection methods for System Center Operations Manager Assessment, and how often data is collected by an agent.</span></span>

| <span data-ttu-id="fc469-131">Platform</span><span class="sxs-lookup"><span data-stu-id="fc469-131">platform</span></span> | <span data-ttu-id="fc469-132">Doğrudan Aracısı</span><span class="sxs-lookup"><span data-stu-id="fc469-132">Direct Agent</span></span> | <span data-ttu-id="fc469-133">SCOM Aracısı</span><span class="sxs-lookup"><span data-stu-id="fc469-133">SCOM agent</span></span> | <span data-ttu-id="fc469-134">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="fc469-134">Azure Storage</span></span> | <span data-ttu-id="fc469-135">SCOM gerekli?</span><span class="sxs-lookup"><span data-stu-id="fc469-135">SCOM required?</span></span> | <span data-ttu-id="fc469-136">Yönetim grubu gönderilen SCOM Aracısı verileri</span><span class="sxs-lookup"><span data-stu-id="fc469-136">SCOM agent data sent via management group</span></span> | <span data-ttu-id="fc469-137">Toplama sıklığı</span><span class="sxs-lookup"><span data-stu-id="fc469-137">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="fc469-138">Windows</span><span class="sxs-lookup"><span data-stu-id="fc469-138">Windows</span></span> | | | | <span data-ttu-id="fc469-139">&#8226;</span><span class="sxs-lookup"><span data-stu-id="fc469-139">&#8226;</span></span> | | <span data-ttu-id="fc469-140">yedi gün</span><span class="sxs-lookup"><span data-stu-id="fc469-140">seven days</span></span> |

## <a name="operations-manager-run-as-accounts-for-oms"></a><span data-ttu-id="fc469-141">Operations Manager hesapları OMS için Çalıştır</span><span class="sxs-lookup"><span data-stu-id="fc469-141">Operations Manager run-as accounts for OMS</span></span>

<span data-ttu-id="fc469-142">Yönetim paketlerine sağlamak iş yükleri için OMS derlemeleri değeri-hizmetlerini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="fc469-142">OMS builds on management packs for workloads to provide value-add services.</span></span> <span data-ttu-id="fc469-143">Her iş yükü, bir etki alanı hesabı gibi farklı güvenlik bağlamında yönetim paketlerini çalıştırmak için iş yüküne özgü ayrıcalıkları gerektirir.</span><span class="sxs-lookup"><span data-stu-id="fc469-143">Each workload requires workload-specific privileges to run management packs in a different security context, such as a domain account.</span></span> <span data-ttu-id="fc469-144">Kimlik bilgileri sağlamak için bir Operations Manager farklı çalıştır hesabı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="fc469-144">Configure an Operations Manager Run As account to provide credential information.</span></span>

<span data-ttu-id="fc469-145">System Center Operations Manager değerlendirmesi için Operations Manager farklı çalıştırma hesabını ayarlamak için aşağıdaki bilgileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="fc469-145">Use the following information to set the Operations Manager run-as account for System Center Operations Manager Assessment.</span></span>

### <a name="set-the-run-as-account"></a><span data-ttu-id="fc469-146">Farklı Çalıştır hesabı ayarlama</span><span class="sxs-lookup"><span data-stu-id="fc469-146">Set the Run As account</span></span>

1. <span data-ttu-id="fc469-147">Operations Manager konsolunda, Git **Yönetim** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="fc469-147">In the Operations Manager Console, go to the **Administration** tab.</span></span>
2. <span data-ttu-id="fc469-148">Altında **Çalıştır Yapılandırması**, tıklatın **hesapları**.</span><span class="sxs-lookup"><span data-stu-id="fc469-148">Under the **Run As Configuration**, click **Accounts**.</span></span>
3. <span data-ttu-id="fc469-149">Farklı Çalıştır bir Windows hesabı oluşturma sihirbazı kullanarak, aşağıdaki hesabı, oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fc469-149">Create the Run As Account, following through the Wizard, creating a Windows account.</span></span> <span data-ttu-id="fc469-150">Hesabını kullanacak şekilde tanımlanır ve aşağıdaki önkoşullar sahip olur:</span><span class="sxs-lookup"><span data-stu-id="fc469-150">The account to use is the one identified and having all the prerequisites below:</span></span>

    >[!NOTE]
    <span data-ttu-id="fc469-151">Farklı Çalıştır hesabı gereksinimleri karşılaması gerekir:</span><span class="sxs-lookup"><span data-stu-id="fc469-151">The Run As account must meet following requirements:</span></span>
    - <span data-ttu-id="fc469-152">(Tüm işlem yöneticisi rolleri - yönetim sunucusu, OpsMgr veritabanı, veri ambarı, raporlama, Web konsolu, ağ geçidi) ortamında tüm sunucularda yerel Administrators grubunun bir etki alanı hesabı üyesi</span><span class="sxs-lookup"><span data-stu-id="fc469-152">A domain account member of the local Administrators group on all servers in the environment (All Operations Manager Roles - Management Server, OpsMgr Database, Data Warehouse, Reporting, Web Console, Gateway)</span></span>
    - <span data-ttu-id="fc469-153">İşlem yöneticisi rolü incelenen yönetim grubu için</span><span class="sxs-lookup"><span data-stu-id="fc469-153">Operation Manager Administrator Role for the management group being assessed</span></span>
    - <span data-ttu-id="fc469-154">Yürütme [betik](#sql-script-to-grant-granular-permissions-to-the-run-as-account) hesabı Operations Manager tarafından kullanılan SQL örneğinde ayrıntılı izinleri vermek için.</span><span class="sxs-lookup"><span data-stu-id="fc469-154">Execute the [script](#sql-script-to-grant-granular-permissions-to-the-run-as-account) to grant granular permissions to the account on SQL instance used by Operations Manager.</span></span>
      <span data-ttu-id="fc469-155">Not: Bu hesap sysadmin hakları zaten varsa, sonra komut dosyası yürütme atlayın.</span><span class="sxs-lookup"><span data-stu-id="fc469-155">Note: If this account has sysadmin rights already, then skip the script execution.</span></span>

4. <span data-ttu-id="fc469-156">Altında **dağıtım güvenliği**seçin **daha güvenli**.</span><span class="sxs-lookup"><span data-stu-id="fc469-156">Under **Distribution Security**, select **More secure**.</span></span>
5. <span data-ttu-id="fc469-157">Hesap dağıtılacağı yeri yönetim sunucusu belirtin.</span><span class="sxs-lookup"><span data-stu-id="fc469-157">Specify the management server where the account is distributed.</span></span>
3. <span data-ttu-id="fc469-158">Çalıştır yapılandırması için geri dönün ve tıklatın **profilleri**.</span><span class="sxs-lookup"><span data-stu-id="fc469-158">Go back to the Run As Configuration and click **Profiles**.</span></span>
4. <span data-ttu-id="fc469-159">Arama *SCOM değerlendirme profili*.</span><span class="sxs-lookup"><span data-stu-id="fc469-159">Search for the *SCOM Assessment Profile*.</span></span>
5. <span data-ttu-id="fc469-160">Profil adı olmalıdır: *Microsoft System Center Advisor SCOM değerlendirme farklı çalıştır profili*.</span><span class="sxs-lookup"><span data-stu-id="fc469-160">The profile name should be: *Microsoft System Center Advisor SCOM Assessment Run As Profile*.</span></span>
6. <span data-ttu-id="fc469-161">Sağ tıklayın ve özelliklerini güncelleştirmek ve son oluşturduğunuz farklı çalıştır 3. adımda oluşturduğunuz hesabı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="fc469-161">Right-click and update its properties and add the recently created Run As Account you created in step 3.</span></span>

### <a name="sql-script-to-grant-granular-permissions-to-the-run-as-account"></a><span data-ttu-id="fc469-162">Farklı Çalıştır hesabı ayrıntılı izinleri vermek için SQL komut dosyası</span><span class="sxs-lookup"><span data-stu-id="fc469-162">SQL script to grant granular permissions to the Run As account</span></span>

<span data-ttu-id="fc469-163">Farklı Çalıştır hesabının Operations Manager tarafından kullanılan SQL örneğinde gerekli izinleri vermek için aşağıdaki SQL betiğini yürütün.</span><span class="sxs-lookup"><span data-stu-id="fc469-163">Execute the following SQL script to grant required permissions to the Run As account on the SQL instance used by Operations Manager.</span></span>

```
-- Replace <UserName> with the actual user name being used as Run As Account.
USE master

-- Create login for the user, comment this line if login is already created.
CREATE LOGIN [UserName] FROM WINDOWS


--GRANT permissions to user.
GRANT VIEW SERVER STATE TO [UserName]
GRANT VIEW ANY DEFINITION TO [UserName]
GRANT VIEW ANY DATABASE TO [UserName]

-- Add database user for all the databases on SQL Server Instance, this is required for connecting to individual databases.
-- NOTE: This command must be run anytime new databases are added to SQL Server instances.
EXEC sp_msforeachdb N'USE [?]; CREATE USER [UserName] FOR LOGIN [UserName];'

Use msdb
GRANT SELECT To [UserName]
Go

--Give SELECT permission on all Operations Manager related Databases

--Replace the Operations Manager database name with the one in your environment
Use [OperationsManager];
GRANT SELECT To [UserName]
GO

--Replace the Operations Manager DatawareHouse database name with the one in your environment
Use [OperationsManagerDW];
GRANT SELECT To [UserName]
GO

--Replace the Operations Manager Audit Collection database name with the one in your environment
Use [OperationsManagerAC];
GRANT SELECT To [UserName]
GO

--Give db_owner on [OperationsManager] DB
--Replace the Operations Manager database name with the one in your environment
USE [OperationsManager]
GO
ALTER ROLE [db_owner] ADD MEMBER [UserName]

```


### <a name="configure-the-assessment-rule"></a><span data-ttu-id="fc469-164">Değerlendirme kuralı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="fc469-164">Configure the assessment rule</span></span>

<span data-ttu-id="fc469-165">System Center Operations Manager değerlendirme çözümün Yönetim Paketi, adında bir kural içerir *Microsoft System Center Advisor SCOM değerlendirme değerlendirme kural çalıştırma*.</span><span class="sxs-lookup"><span data-stu-id="fc469-165">The System Center Operations Manager Assessment solution’s management pack includes a rule named *Microsoft System Center Advisor SCOM Assessment Run Assessment Rule*.</span></span> <span data-ttu-id="fc469-166">Bu kural, değerlendirme çalıştırmaktan sorumludur.</span><span class="sxs-lookup"><span data-stu-id="fc469-166">This rule is responsible for running the assessment.</span></span> <span data-ttu-id="fc469-167">Kuralı etkinleştirmek ve sıklığı yapılandırmak için aşağıdaki yordamları kullanın.</span><span class="sxs-lookup"><span data-stu-id="fc469-167">To enable the rule and configure the frequency, use the procedures below.</span></span>

<span data-ttu-id="fc469-168">Varsayılan olarak, Microsoft System Center Advisor SCOM değerlendirme çalıştırmak değerlendirme kural devre dışıdır.</span><span class="sxs-lookup"><span data-stu-id="fc469-168">By default, the Microsoft System Center Advisor SCOM Assessment Run Assessment Rule is disabled.</span></span> <span data-ttu-id="fc469-169">Değerlendirme çalıştırmak için bir yönetim sunucusunda kural etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="fc469-169">To run the assessment, you must enable the rule on a management server.</span></span> <span data-ttu-id="fc469-170">Aşağıdaki adımları kullanın.</span><span class="sxs-lookup"><span data-stu-id="fc469-170">Use the following steps.</span></span>

#### <a name="enable-the-rule-for-a-specific-management-server"></a><span data-ttu-id="fc469-171">Belirli yönetim sunucusuna ilişkin kuralını etkinleştir</span><span class="sxs-lookup"><span data-stu-id="fc469-171">Enable the rule for a specific management server</span></span>

1. <span data-ttu-id="fc469-172">İçinde **yazma** arama kuralı için Operations Manager konsolunun çalışma *Microsoft System Center Advisor SCOM değerlendirme değerlendirme kural çalıştırma* içinde **kuralları** bölmesi.</span><span class="sxs-lookup"><span data-stu-id="fc469-172">In the **Authoring** workspace of the Operations Manager console, search for the rule *Microsoft System Center Advisor SCOM Assessment Run Assessment Rule* in the **Rules** pane.</span></span>
2. <span data-ttu-id="fc469-173">Arama sonuçlarında metin içeren bir tanesini seçin *türü: Yönetim sunucusu*.</span><span class="sxs-lookup"><span data-stu-id="fc469-173">In the search results, select the one that includes the text *Type: Management Server*.</span></span>
3. <span data-ttu-id="fc469-174">Kuralı sağ tıklatın ve ardından **geçersiz kılmaları** > **sınıfın belirli bir nesnesi için: Yönetim sunucusu**.</span><span class="sxs-lookup"><span data-stu-id="fc469-174">Right-click the rule and then click **Overrides** > **For a specific object of class: Management Server**.</span></span>
4.  <span data-ttu-id="fc469-175">Kullanılabilir yönetim sunucuları listesini kural çalıştırdığı yönetim sunucusu seçin.</span><span class="sxs-lookup"><span data-stu-id="fc469-175">In the available management servers list, select the management server where the rule should run.</span></span>
5.  <span data-ttu-id="fc469-176">Geçersiz kılma değerine değiştirdiğinizden emin olun **True** için **etkin** parametre değeri.</span><span class="sxs-lookup"><span data-stu-id="fc469-176">Ensure that you change override value to **True** for the **Enabled** parameter value.</span></span>  
    <span data-ttu-id="fc469-177">![parametresi geçersiz kıl](./media/log-analytics-scom-assessment/rule.png)</span><span class="sxs-lookup"><span data-stu-id="fc469-177">![override parameter](./media/log-analytics-scom-assessment/rule.png)</span></span>

<span data-ttu-id="fc469-178">Bu pencerede hala, bir sonraki yordamı kullanarak çalışma sıklığını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="fc469-178">While still in this window, configure the frequency of the run using the next procedure.</span></span>

#### <a name="configure-the-run-frequency"></a><span data-ttu-id="fc469-179">Çalışma sıklığını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="fc469-179">Configure the run frequency</span></span>

<span data-ttu-id="fc469-180">Değerlendirme her 10.080 dakikadır (veya yedi gün) çalışmak üzere yapılandırılan varsayılan zaman aralığı.</span><span class="sxs-lookup"><span data-stu-id="fc469-180">The assessment is configured to run every 10,080 minutes (or seven days), the default interval.</span></span> <span data-ttu-id="fc469-181">En küçük değerini 1440 dakika (veya bir gün) değerine geçersiz kılabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fc469-181">You can override the value to a minimum value of 1440 minutes (or one day).</span></span> <span data-ttu-id="fc469-182">Değerin ardışık değerlendirme çalışmaları arasında gerekli en düşük zaman aralığı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="fc469-182">The value represents the minimum time gap required between successive assessment runs.</span></span> <span data-ttu-id="fc469-183">Aralık geçersiz kılmak için aşağıdaki adımları kullanın.</span><span class="sxs-lookup"><span data-stu-id="fc469-183">To override the interval, use the steps below.</span></span>

1. <span data-ttu-id="fc469-184">İçinde **yazma** arama kuralı için Operations Manager konsolunun çalışma *Microsoft System Center Advisor SCOM değerlendirme değerlendirme kural çalıştırma* içinde **kuralları** bölmesi.</span><span class="sxs-lookup"><span data-stu-id="fc469-184">In the **Authoring** workspace of the Operations Manager console, search for the rule *Microsoft System Center Advisor SCOM Assessment Run Assessment Rule* in the **Rules** pane.</span></span>
2. <span data-ttu-id="fc469-185">Arama sonuçlarında metin içeren bir tanesini seçin *türü: Yönetim sunucusu*.</span><span class="sxs-lookup"><span data-stu-id="fc469-185">In the search results, select the one that includes the text *Type: Management Server*.</span></span>
3. <span data-ttu-id="fc469-186">Kuralı sağ tıklatın ve ardından **kuralı geçersiz kıl** > **sınıfın tüm nesneleri için: Yönetim sunucusu**.</span><span class="sxs-lookup"><span data-stu-id="fc469-186">Right-click the rule and then click **Override the Rule** > **For all objects of class: Management Server**.</span></span>
4. <span data-ttu-id="fc469-187">Değişiklik **aralığı** , istenen aralık değeri için parametre değeri.</span><span class="sxs-lookup"><span data-stu-id="fc469-187">Change the **Interval** parameter value to your desired interval value.</span></span> <span data-ttu-id="fc469-188">Aşağıdaki örnekte, değer 1440 dakika (bir gün) olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="fc469-188">In the example below, the value is set to 1440 minutes (one day).</span></span>  
    <span data-ttu-id="fc469-189">![aralığı parametresi](./media/log-analytics-scom-assessment/interval.png)</span><span class="sxs-lookup"><span data-stu-id="fc469-189">![interval parameter](./media/log-analytics-scom-assessment/interval.png)</span></span>  
    <span data-ttu-id="fc469-190">Değer 1440 dakikadan daha kısa bir süre için ayarlarsanız, kuralın bir gün aralığında çalışır.</span><span class="sxs-lookup"><span data-stu-id="fc469-190">If the value is set to less than 1440 minutes, then the rule runs at a one day interval.</span></span> <span data-ttu-id="fc469-191">Bu örnekte, kural aralık değeri göz ardı eder ve bir gün sıklığında çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="fc469-191">In this example, the rule ignores the interval value and runs at a frequency of one day.</span></span>


## <a name="understanding-how-recommendations-are-prioritized"></a><span data-ttu-id="fc469-192">Önerilerin nasıl önceliklendirilir anlama</span><span class="sxs-lookup"><span data-stu-id="fc469-192">Understanding how recommendations are prioritized</span></span>

<span data-ttu-id="fc469-193">Yapılan her öneri öneri göreceli önemini tanımlayan bir ağırlıklı değer verilir.</span><span class="sxs-lookup"><span data-stu-id="fc469-193">Every recommendation made is given a weighting value that identifies the relative importance of the recommendation.</span></span> <span data-ttu-id="fc469-194">Yalnızca 10 en önemli öneriler gösterilir.</span><span class="sxs-lookup"><span data-stu-id="fc469-194">Only the 10 most important recommendations are shown.</span></span>

### <a name="how-weights-are-calculated"></a><span data-ttu-id="fc469-195">Ağırlıkları nasıl hesaplanır</span><span class="sxs-lookup"><span data-stu-id="fc469-195">How weights are calculated</span></span>

<span data-ttu-id="fc469-196">Ağırlık belirlemeyi üç anahtar faktörlerini temel alarak toplam değerler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="fc469-196">Weightings are aggregate values based on three key factors:</span></span>

- <span data-ttu-id="fc469-197">*Olasılık* tanımlanan bir sorunun sorunlara neden.</span><span class="sxs-lookup"><span data-stu-id="fc469-197">The *probability* that an issue identified will cause problems.</span></span> <span data-ttu-id="fc469-198">Daha yüksek olasılık öneri için daha büyük bir genel puan karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="fc469-198">A higher probability equates to a larger overall score for the recommendation.</span></span>
- <span data-ttu-id="fc469-199">*Etkisi* kuruluşunuzdaki bir soruna neden olursa sorun.</span><span class="sxs-lookup"><span data-stu-id="fc469-199">The *impact* of the issue on your organization if it does cause a problem.</span></span> <span data-ttu-id="fc469-200">Daha yüksek bir etkisi öneri için daha büyük bir genel puan karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="fc469-200">A higher impact equates to a larger overall score for the recommendation.</span></span>
- <span data-ttu-id="fc469-201">*Çaba* öneriyi uygulamak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="fc469-201">The *effort* required to implement the recommendation.</span></span> <span data-ttu-id="fc469-202">Daha yüksek çaba öneri için daha küçük bir genel puan karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="fc469-202">A higher effort equates to a smaller overall score for the recommendation.</span></span>

<span data-ttu-id="fc469-203">Her öneri ağırlıklı her odak alanı için kullanılabilir toplam puanı yüzdesi olarak ifade edilir.</span><span class="sxs-lookup"><span data-stu-id="fc469-203">The weighting for each recommendation is expressed as a percentage of the total score available for each focus area.</span></span> <span data-ttu-id="fc469-204">Örneğin, bu öneri uygulama kullanılabilirlik ve iş sürekliliği odak alanında bir öneri %5 puanı varsa, genel kullanılabilirlik ve iş sürekliliği puan tarafından %5 artırır.</span><span class="sxs-lookup"><span data-stu-id="fc469-204">For example, if a recommendation in the Availability and Business Continuity focus area has a score of 5%, implementing that recommendation increases your overall Availability and Business Continuity score by 5%.</span></span>

### <a name="focus-areas"></a><span data-ttu-id="fc469-205">Odak alanları</span><span class="sxs-lookup"><span data-stu-id="fc469-205">Focus areas</span></span>

<span data-ttu-id="fc469-206">**Kullanılabilirlik ve iş sürekliliği** -bu odaklanılan alan hizmet kullanılabilirliği, altyapı ve iş koruması dayanıklılık için öneriler gösterir.</span><span class="sxs-lookup"><span data-stu-id="fc469-206">**Availability and Business Continuity** - This focus area shows recommendations for service availability, resiliency of your infrastructure, and business protection.</span></span>

<span data-ttu-id="fc469-207">**Performans ve ölçeklenebilirlik** -bu odak alanı kuruluşunuzun yardımcı olacak öneriler gösterir BT altyapısı arttıkça, BT ortamınız geçerli performans gereksinimlerini karşıladığından ve altyapı değiştirmeye yanıt verebilmesini olduğundan emin olun gerekir.</span><span class="sxs-lookup"><span data-stu-id="fc469-207">**Performance and Scalability** - This focus area shows recommendations to help your organization's IT infrastructure grow, ensure that your IT environment meets current performance requirements, and is able to respond to changing infrastructure needs.</span></span>

<span data-ttu-id="fc469-208">**Yükseltme, geçiş ve dağıtım** -bu odak alanı, yükseltme, geçirme ve SQL Server mevcut altyapınızda dağıtmanıza yardımcı olacak öneriler gösterir.</span><span class="sxs-lookup"><span data-stu-id="fc469-208">**Upgrade, Migration, and Deployment** - This focus area shows recommendations to help you upgrade, migrate, and deploy SQL Server to your existing infrastructure.</span></span>

<span data-ttu-id="fc469-209">**İşlemler ve izleme** -bu odak alanı BT işlemlerinizi kolaylaştırır, önleyici bakım uygulamak ve performansı en üst düzeye çıkarmanıza yardımcı olacak öneriler gösterir.</span><span class="sxs-lookup"><span data-stu-id="fc469-209">**Operations and Monitoring** - This focus area shows recommendations to help streamline your IT operations, implement preventative maintenance, and maximize performance.</span></span>

### <a name="should-you-aim-to-score-100-in-every-focus-area"></a><span data-ttu-id="fc469-210">Her odaklanılan alan % 100 puanlı hedefleyin?</span><span class="sxs-lookup"><span data-stu-id="fc469-210">Should you aim to score 100% in every focus area?</span></span>

<span data-ttu-id="fc469-211">Olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="fc469-211">Not necessarily.</span></span> <span data-ttu-id="fc469-212">Öneriler bilgi ve müşteri ziyaretleriniz binlerce arasında Microsoft mühendisleri tarafından elde edilen deneyimleri temel alır.</span><span class="sxs-lookup"><span data-stu-id="fc469-212">The recommendations are based on the knowledge and experiences gained by Microsoft engineers across thousands of customer visits.</span></span> <span data-ttu-id="fc469-213">Ancak, iki sunucu altyapılar aynıdır ve özel öneriler için daha az veya uygun olabilir.</span><span class="sxs-lookup"><span data-stu-id="fc469-213">However, no two server infrastructures are the same, and specific recommendations may be more or less relevant to you.</span></span> <span data-ttu-id="fc469-214">Örneğin, bazı güvenlik önerileri sanal makinelerinizi Internet'e açık değildir, daha az ilgili olabilir.</span><span class="sxs-lookup"><span data-stu-id="fc469-214">For example, some security recommendations might be less relevant if your virtual machines are not exposed to the Internet.</span></span> <span data-ttu-id="fc469-215">Bazı kullanılabilirlik öneriler düşük öncelik geçici veri toplama ve raporlama sağladığı hizmetler için daha az uygun olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="fc469-215">Some availability recommendations may be less relevant for services that provide low priority ad hoc data collection and reporting.</span></span> <span data-ttu-id="fc469-216">Olgun bir iş için önemli olan sorunları bir başlangıcından daha az önemli olabilir.</span><span class="sxs-lookup"><span data-stu-id="fc469-216">Issues that are important to a mature business may be less important to a start-up.</span></span> <span data-ttu-id="fc469-217">Hangi odak alanların önceliklerinizden olduğunu belirlemek ve, puanları zamanla nasıl değiştiğini adresindeki Ara isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fc469-217">You may want to identify which focus areas are your priorities and then look at how your scores change over time.</span></span>

<span data-ttu-id="fc469-218">Her öneri neden önemli olduğu hakkında yönergeler içerir.</span><span class="sxs-lookup"><span data-stu-id="fc469-218">Every recommendation includes guidance about why it is important.</span></span> <span data-ttu-id="fc469-219">Öneri uygulama verilen BT hizmetlerinizi yapısını ve kuruluşunuzun iş gereksinimlerini sizin için uygun olup olmadığını değerlendirmek için bu kılavuzu kullanın.</span><span class="sxs-lookup"><span data-stu-id="fc469-219">Use this guidance to evaluate whether implementing the recommendation is appropriate for you, given the nature of your IT services and the business needs of your organization.</span></span>

## <a name="use-assessment-focus-area-recommendations"></a><span data-ttu-id="fc469-220">Değerlendirme odak alanı önerileri kullanın</span><span class="sxs-lookup"><span data-stu-id="fc469-220">Use assessment focus area recommendations</span></span>

<span data-ttu-id="fc469-221">OMS içinde bir değerlendirme çözümü kullanmadan önce çözümü yüklenmiş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="fc469-221">Before you can use an assessment solution in OMS, you must have the solution installed.</span></span> <span data-ttu-id="fc469-222">Daha fazla bilgi için çözümleri yükleme hakkında bkz [Çözümleri Galerisi eklemek günlük analizi çözümleri](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="fc469-222">To read more about installing solutions, see [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span> <span data-ttu-id="fc469-223">Yüklendikten sonra OMS genel bakış sayfasında System Center Operations Manager değerlendirme döşeme kullanarak önerileri özetini görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fc469-223">After it is installed, you can view the summary of recommendations by using the System Center Operations Manager Assessment tile on the Overview page in OMS.</span></span>

<span data-ttu-id="fc469-224">Altyapınız ve ardından-ayrıntıya önerileri için özetlenmiş uyumluluk değerlendirmesi görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="fc469-224">View the summarized compliance assessments for your infrastructure and then drill-into recommendations.</span></span>

### <a name="to-view-recommendations-for-a-focus-area-and-take-corrective-action"></a><span data-ttu-id="fc469-225">Odak alanı için öneriler görüntülemek ve düzeltici işlemleri için</span><span class="sxs-lookup"><span data-stu-id="fc469-225">To view recommendations for a focus area and take corrective action</span></span>

1. <span data-ttu-id="fc469-226">Üzerinde **genel bakış** sayfasında, **System Center Operations Manager değerlendirme** döşeme.</span><span class="sxs-lookup"><span data-stu-id="fc469-226">On the **Overview** page, click the **System Center Operations Manager Assessment** tile.</span></span>
2. <span data-ttu-id="fc469-227">Üzerinde **System Center Operations Manager değerlendirme** sayfasında odak alanı Kanatlar birinde özet bilgilerini inceleyin ve sonra bu odak alanı için öneriler görüntülemek için tıklatın.</span><span class="sxs-lookup"><span data-stu-id="fc469-227">On the **System Center Operations Manager Assessment** page, review the summary information in one of the focus area blades and then click one to view recommendations for that focus area.</span></span>
3. <span data-ttu-id="fc469-228">Odak alanı sayfaları hiçbirinde ortamınız için öncelikli önerilerin görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fc469-228">On any of the focus area pages, you can view the prioritized recommendations made for your environment.</span></span> <span data-ttu-id="fc469-229">Önerinin altında tıklatın **etkilenen nesneleri** öneri neden yapılan hakkında ayrıntıları görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="fc469-229">Click a recommendation under **Affected Objects** to view details about why the recommendation is made.</span></span>  
    <span data-ttu-id="fc469-230">![Odaklanılan alan](./media/log-analytics-scom-assessment/focus-area.png)</span><span class="sxs-lookup"><span data-stu-id="fc469-230">![focus area](./media/log-analytics-scom-assessment/focus-area.png)</span></span>
4. <span data-ttu-id="fc469-231">Önerilen düzeltici eylemleri gerçekleştirebilirsiniz **önerilen eylemleri**.</span><span class="sxs-lookup"><span data-stu-id="fc469-231">You can take corrective actions suggested in **Suggested Actions**.</span></span> <span data-ttu-id="fc469-232">Öğe ele, önerilen eylemler gerçekleştirilen ve uyumluluk puan artıracaktır sonraki değerlendirmeleri kaydeder.</span><span class="sxs-lookup"><span data-stu-id="fc469-232">When the item has been addressed, later assessments will record that recommended actions were taken and your compliance score will increase.</span></span> <span data-ttu-id="fc469-233">Düzeltilmiş öğeler görünür olarak **geçirilen nesneleri**.</span><span class="sxs-lookup"><span data-stu-id="fc469-233">Corrected items appear as **Passed Objects**.</span></span>

## <a name="ignore-recommendations"></a><span data-ttu-id="fc469-234">Öneriler yoksay</span><span class="sxs-lookup"><span data-stu-id="fc469-234">Ignore recommendations</span></span>

<span data-ttu-id="fc469-235">Yoksay istediğiniz önerileri varsa, öneriler değerlendirme sonuçlarında görünmesini engellemek için OMS kullanan bir metin dosyası oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fc469-235">If you have recommendations that you want to ignore, you can create a text file that OMS uses to prevent recommendations from appearing in your assessment results.</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

### <a name="to-identify-recommendations-that-you-want-to-ignore"></a><span data-ttu-id="fc469-236">Yoksay istediğiniz önerileri tanımlamak için</span><span class="sxs-lookup"><span data-stu-id="fc469-236">To identify recommendations that you want to ignore</span></span>

1. <span data-ttu-id="fc469-237">Sunucunuzdan çalışma alanınıza oturum açın ve günlük arama açın.</span><span class="sxs-lookup"><span data-stu-id="fc469-237">Sign in to your workspace and open Log Search.</span></span> <span data-ttu-id="fc469-238">Ortamınızdaki bilgisayarları için başarısız olan liste önerileri için aşağıdaki sorguyu kullanın.</span><span class="sxs-lookup"><span data-stu-id="fc469-238">Use the following query to list recommendations that have failed for computers in your environment.</span></span>

    ```
    Type=SCOMAssessmentRecommendationRecommendationResult=Failed | select  Computer, RecommendationId, Recommendation | sort  Computer
    ```

    <span data-ttu-id="fc469-239">Günlük arama sorgusu gösteren ekran görüntüsü aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="fc469-239">Here's a screen shot showing the Log Search query:</span></span>  
    ![günlük araması](./media/log-analytics-scom-assessment/scom-log-search.png)

2. <span data-ttu-id="fc469-241">Yoksay istediğiniz önerileri seçin.</span><span class="sxs-lookup"><span data-stu-id="fc469-241">Choose recommendations that you want to ignore.</span></span> <span data-ttu-id="fc469-242">Sonraki yordamda Recommendationıd için değerleri kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="fc469-242">You'll use the values for RecommendationId in the next procedure.</span></span>

### <a name="to-create-and-use-an-ignorerecommendationstxt-text-file"></a><span data-ttu-id="fc469-243">Oluşturma ve bir IgnoreRecommendations.txt metin dosyası kullanma</span><span class="sxs-lookup"><span data-stu-id="fc469-243">To create and use an IgnoreRecommendations.txt text file</span></span>

1. <span data-ttu-id="fc469-244">IgnoreRecommendations.txt adlı bir dosya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fc469-244">Create a file named IgnoreRecommendations.txt.</span></span>
2. <span data-ttu-id="fc469-245">Her Recommendationıd ayrı bir satırda yoksay ve sonra dosyayı kaydedip kapatın için OMS istediğiniz her bir öneri için yazın veya yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="fc469-245">Paste or type each RecommendationId for each recommendation that you want OMS to ignore on a separate line and then save and close the file.</span></span>
3. <span data-ttu-id="fc469-246">Dosya aşağıdaki klasörde önerileri yoksaymak için OMS istediğiniz her bilgisayara yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="fc469-246">Put the file in the following folder on each computer where you want OMS to ignore recommendations.</span></span>
4. <span data-ttu-id="fc469-247">Operations Manager yönetim sunucusunda - *SystemDrive*: \Program System Center 2012 R2\Operations Manager\Server.</span><span class="sxs-lookup"><span data-stu-id="fc469-247">On the Operations Manager management server - *SystemDrive*:\Program Files\Microsoft System Center 2012 R2\Operations Manager\Server.</span></span>

### <a name="to-verify-that-recommendations-are-ignored"></a><span data-ttu-id="fc469-248">Öneriler göz ardı edilir doğrulamak için</span><span class="sxs-lookup"><span data-stu-id="fc469-248">To verify that recommendations are ignored</span></span>

1. <span data-ttu-id="fc469-249">Sonraki değerlendirme çalıştığında, varsayılan olarak yedi günde zamanlanmış sonra belirtilen önerileri yoksayıldı işaretlenir ve değerlendirme Panoda görünmez.</span><span class="sxs-lookup"><span data-stu-id="fc469-249">After the next scheduled assessment runs, by default every seven days, the specified recommendations are marked Ignored and will not appear on the assessment dashboard.</span></span>
2. <span data-ttu-id="fc469-250">Tüm yoksayılan öneriler listelemek için aşağıdaki günlük arama sorgularını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fc469-250">You can use the following Log Search queries to list all the ignored recommendations.</span></span>

    ```
    Type=SCOMAssessmentRecommendationRecommendationResult=Ignored | select  Computer, RecommendationId, Recommendation | sort  Computer
    ```

3. <span data-ttu-id="fc469-251">Daha sonra yoksayılan önerileri görmek istediğiniz karar verirseniz, tüm IgnoreRecommendations.txt dosyaları silin veya bunları RecommendationIDs kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fc469-251">If you decide later that you want to see ignored recommendations, remove any IgnoreRecommendations.txt files, or you can remove RecommendationIDs from them.</span></span>

## <a name="system-center-operations-manager-assessment-solution-faq"></a><span data-ttu-id="fc469-252">System Center Operations Manager değerlendirme çözümü hakkında SSS</span><span class="sxs-lookup"><span data-stu-id="fc469-252">System Center Operations Manager Assessment solution FAQ</span></span>

<span data-ttu-id="fc469-253">*OMS çalışma alanıma değerlendirme çözümü ekledim. Ancak önerilerini görmek yok. Neden olmasın?*</span><span class="sxs-lookup"><span data-stu-id="fc469-253">*I added the assessment solution to my OMS workspace. But I don’t see the recommendations. Why not?*</span></span> <span data-ttu-id="fc469-254">Çözüm eklendikten sonra aşağıdaki adımları görünümü OMS Panoda önerileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="fc469-254">After adding the solution, use the following steps view the recommendations on the OMS dashboard.</span></span>  

- [<span data-ttu-id="fc469-255">System Center Operations Manager değerlendirmesi için farklı çalıştır hesabı ayarlama</span><span class="sxs-lookup"><span data-stu-id="fc469-255">Set the Run As account for System Center Operations Manager Assessment</span></span>](#operations-manager-run-as-accounts-for-oms)  
- [<span data-ttu-id="fc469-256">System Center Operations Manager değerlendirme kuralı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="fc469-256">Configure the System Center Operations Manager Assessment rule</span></span>](#configure-the-assessment-rule)


<span data-ttu-id="fc469-257">*Ne sıklıkta değerlendirme çalıştıran yapılandırmak için yolu var mı?*</span><span class="sxs-lookup"><span data-stu-id="fc469-257">*Is there a way to configure how often the assessment runs?*</span></span> <span data-ttu-id="fc469-258">Evet.</span><span class="sxs-lookup"><span data-stu-id="fc469-258">Yes.</span></span> <span data-ttu-id="fc469-259">Bkz: [çalışma sıklığını yapılandırma](#configure-the-run-frequency).</span><span class="sxs-lookup"><span data-stu-id="fc469-259">See [Configure the run frequency](#configure-the-run-frequency).</span></span>

<span data-ttu-id="fc469-260">*System Center Operations Manager değerlendirme çözümü ekledim sonra başka bir sunucuya bulunmuşsa, değerlendirileceğini?*</span><span class="sxs-lookup"><span data-stu-id="fc469-260">*If another server is discovered after I’ve added the System Center Operations Manager Assessment solution, will it be assessed?*</span></span> <span data-ttu-id="fc469-261">Evet, bulma sonra onu sonra itibaren--varsayılan olarak, her yedi günde değerlendirildiği.</span><span class="sxs-lookup"><span data-stu-id="fc469-261">Yes, after discovery, it is assessed from then on--by default, every seven days.</span></span>

<span data-ttu-id="fc469-262">*Veri toplama mu işlemin adı nedir?*</span><span class="sxs-lookup"><span data-stu-id="fc469-262">*What is the name of the process that does the data collection?*</span></span> <span data-ttu-id="fc469-263">AdvisorAssessment.exe</span><span class="sxs-lookup"><span data-stu-id="fc469-263">AdvisorAssessment.exe</span></span>

<span data-ttu-id="fc469-264">*Burada AdvisorAssessment.exe işlemi çalışıyor mu?*</span><span class="sxs-lookup"><span data-stu-id="fc469-264">*Where does the AdvisorAssessment.exe process run?*</span></span> <span data-ttu-id="fc469-265">AdvisorAssessment.exe değerlendirme kural etkinleştirdiğiniz sistem sağlığı hizmeti yönetim sunucusunun altında çalışır.</span><span class="sxs-lookup"><span data-stu-id="fc469-265">AdvisorAssessment.exe runs under the HealthService of the management server where the assessment rule is enabled.</span></span> <span data-ttu-id="fc469-266">Bu işlemi kullanarak, tüm ortamınız keşfinin uzak veri toplulukta elde edilir.</span><span class="sxs-lookup"><span data-stu-id="fc469-266">Using that process, discovery of your entire environment is achieved through remote data collection.</span></span>

<span data-ttu-id="fc469-267">*Ne kadar veri toplamaya yönelik sürer?*</span><span class="sxs-lookup"><span data-stu-id="fc469-267">*How long does it take for data collection?*</span></span> <span data-ttu-id="fc469-268">Veri toplama sunucusundaki yaklaşık bir saat sürer.</span><span class="sxs-lookup"><span data-stu-id="fc469-268">Data collection on the server takes about one hour.</span></span> <span data-ttu-id="fc469-269">Bu, pek çok Operations Manager örnekleri veya veritabanlarına sahip ortamlarda daha uzun sürebilir.</span><span class="sxs-lookup"><span data-stu-id="fc469-269">It may take longer in environments that have many Operations Manager instances or databases.</span></span>

<span data-ttu-id="fc469-270">*Ne değerlendirme aralığını 1440 dakikadan daha kısa bir süre için ayarlarım?*</span><span class="sxs-lookup"><span data-stu-id="fc469-270">*What if I set the interval of the assessment to less than 1440 minutes?*</span></span> <span data-ttu-id="fc469-271">Değerlendirme en fazla günde bir kez çalıştırmak üzere önceden yapılandırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="fc469-271">The assessment is pre-configured to run at a maximum of once per day.</span></span> <span data-ttu-id="fc469-272">1440 dakikadan daha kısa bir değer aralığı değeri geçersiz kılarsanız değerlendirme 1440 dakika aralık değeri kullanır.</span><span class="sxs-lookup"><span data-stu-id="fc469-272">If you override the interval value to a value less than 1440 minutes, then the assessment uses 1440 minutes as the interval value.</span></span>

<span data-ttu-id="fc469-273">*Önkoşul hataları olup olmadığını bilmek nasıl?*</span><span class="sxs-lookup"><span data-stu-id="fc469-273">*How to know if there are pre-requisite failures?*</span></span> <span data-ttu-id="fc469-274">Ardından değerlendirme çalıştırdı ve sonuçları görmüyorsanız, değerlendirme için önkoşulların bazıları başarısız olabilir.</span><span class="sxs-lookup"><span data-stu-id="fc469-274">If the assessment ran and you don't see results, then it is likely that some of the pre-requisites for the assessment failed.</span></span> <span data-ttu-id="fc469-275">Sorguları çalıştırabilirsiniz: `Type=Operation Solution=SCOMAssessment` ve `Type=SCOMAssessmentRecommendation FocusArea=Prerequisites` günlük başarısız ön koşullar görmek için Ara.</span><span class="sxs-lookup"><span data-stu-id="fc469-275">You can execute queries: `Type=Operation Solution=SCOMAssessment` and `Type=SCOMAssessmentRecommendation FocusArea=Prerequisites` in Log Search to see the failed pre-requisites.</span></span>

<span data-ttu-id="fc469-276">*Var olan bir `Failed to connect to the SQL Instance (….).` önkoşul hatası iletisi. Sorun nedir?*</span><span class="sxs-lookup"><span data-stu-id="fc469-276">*There is a `Failed to connect to the SQL Instance (….).` message in pre-requisite failures. What is the issue?*</span></span> <span data-ttu-id="fc469-277">AdvisorAssessment.exe, toplar, işlem sistem sağlığı hizmeti yönetim sunucusunun altında çalışır.</span><span class="sxs-lookup"><span data-stu-id="fc469-277">AdvisorAssessment.exe, the process that collects data, runs under the HealthService of the management server.</span></span> <span data-ttu-id="fc469-278">Değerlendirme bir parçası olarak, işlem Operations Manager veritabanı mevcut olduğu SQL Server'a bağlanmak çalışır.</span><span class="sxs-lookup"><span data-stu-id="fc469-278">As part of the assessment, the process attempts to connect to the SQL Server where the Operations Manager database is present.</span></span> <span data-ttu-id="fc469-279">Güvenlik duvarı kuralları SQL Server örneği bağlantısı engellediğinizde bu hata oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="fc469-279">This error can occur when firewall rules block the connection to the SQL Server instance.</span></span>

<span data-ttu-id="fc469-280">*Hangi türde veri toplanır?*</span><span class="sxs-lookup"><span data-stu-id="fc469-280">*What type of data is collected?*</span></span> <span data-ttu-id="fc469-281">Aşağıdaki veri türlerini toplanır: - WMI verilerini - kayıt defteri - olay günlüğü verilerini - Operations Manager verilerini Windows PowerShell, SQL sorguları ve dosya bilgileri Toplayıcı aracılığıyla.</span><span class="sxs-lookup"><span data-stu-id="fc469-281">The following types of data are collected: - WMI data - Registry data - EventLog data - Operations Manager data through Windows PowerShell, SQL Queries and File information collector.</span></span>

<span data-ttu-id="fc469-282">*Bir farklı çalıştır hesabı yapılandırmak neden var mı?*</span><span class="sxs-lookup"><span data-stu-id="fc469-282">*Why do I have to configure a Run As Account?*</span></span> <span data-ttu-id="fc469-283">Bir Operations Manager sunucusu için çeşitli SQL sorguları çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="fc469-283">For an Operations Manager server, various SQL queries are run.</span></span> <span data-ttu-id="fc469-284">Sırayla bunları çalıştırmak gerekli izinlere sahip bir farklı çalıştır hesabı kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="fc469-284">In order for them to run, you must use a Run As Account with necessary permissions.</span></span> <span data-ttu-id="fc469-285">Ayrıca, yerel yönetici kimlik bilgileri WMI sorgusu için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="fc469-285">In addition, local administrator credentials are required to query WMI.</span></span>

<span data-ttu-id="fc469-286">*Neden yalnızca ilk 10 önerileri görüntülemek?*</span><span class="sxs-lookup"><span data-stu-id="fc469-286">*Why display only the top 10 recommendations?*</span></span> <span data-ttu-id="fc469-287">Görevlerin kapsamlı, zorlamayı listesi vermek yerine, Önceliklendirilmiş önerileri adresleme odaklanmak öneririz.</span><span class="sxs-lookup"><span data-stu-id="fc469-287">Instead of giving you an exhaustive, overwhelming list of tasks, we recommend that you focus on addressing the prioritized recommendations first.</span></span> <span data-ttu-id="fc469-288">Bunları çözün sonra ek öneriler kullanılabilir hale gelir.</span><span class="sxs-lookup"><span data-stu-id="fc469-288">After you address them, additional recommendations will become available.</span></span> <span data-ttu-id="fc469-289">Ayrıntılı listesini görmek isterseniz, tüm önerileri günlük arama özelliğini kullanarak görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fc469-289">If you prefer to see the detailed list, you can view all recommendations using Log Search.</span></span>

<span data-ttu-id="fc469-290">*Bir öneri yoksaymak için yolu var mı?*</span><span class="sxs-lookup"><span data-stu-id="fc469-290">*Is there a way to ignore a recommendation?*</span></span> <span data-ttu-id="fc469-291">Evet, bkz: [önerileri yoksay](#Ignore-recommendations).</span><span class="sxs-lookup"><span data-stu-id="fc469-291">Yes, see the [Ignore recommendations](#Ignore-recommendations).</span></span>


## <a name="next-steps"></a><span data-ttu-id="fc469-292">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fc469-292">Next steps</span></span>

- <span data-ttu-id="fc469-293">[Arama günlüklerini](log-analytics-log-searches.md) ayrıntılı System Center Operations Manager Değerlendirme verileri ve öneriler görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="fc469-293">[Search logs](log-analytics-log-searches.md) to view detailed System Center Operations Manager Assessment data and recommendations.</span></span>
