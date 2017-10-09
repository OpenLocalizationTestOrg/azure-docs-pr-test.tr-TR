---
title: "aaaInstalling esnek veritabanı işleri | Microsoft Docs"
description: "Merhaba esnek iş özellik yüklenmesinde size yol gösterir."
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: cbe0aa2b-17e3-4b6f-a16f-6ebc1f5a66af
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 0349f66a4428f81d00d43681d7f2177f273ec032
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="installing-elastic-database-jobs-overview"></a><span data-ttu-id="af379-103">Yükleme esnek veritabanı işleri genel bakış</span><span class="sxs-lookup"><span data-stu-id="af379-103">Installing Elastic Database jobs overview</span></span>
<span data-ttu-id="af379-104">[**Esnek veritabanı iş** ](sql-database-elastic-jobs-overview.md) PowerShell ile yüklenebilir veya toocreate Azure Klasik Portal.You elde hello erişmek ve işleri yalnızca hello PowerShell paketi yüklerseniz hello PowerShell API kullanarak yönetmek.</span><span class="sxs-lookup"><span data-stu-id="af379-104">[**Elastic Database jobs**](sql-database-elastic-jobs-overview.md) can be installed via PowerShell or through hello Azure Classic Portal.You can gain access toocreate and manage jobs using hello PowerShell API only if you install hello PowerShell package.</span></span> <span data-ttu-id="af379-105">Ayrıca, hello PowerShell API'lerinden sağlayın hello portal önemli ölçüde daha fazla işlevsellik bu anda.</span><span class="sxs-lookup"><span data-stu-id="af379-105">Additionally, hello PowerShell APIs provide significantly more functionality than hello portal at this point in time.</span></span>

<span data-ttu-id="af379-106">Zaten yüklediyseniz, **esnek veritabanı işleri** mevcut bir kümeden hello Portal aracılığıyla **esnek havuz**, hello son Powershell Önizleme, mevcut yüklemenizi betikleri tooupgrade içerir.</span><span class="sxs-lookup"><span data-stu-id="af379-106">If you have already installed **Elastic Database jobs** through hello Portal from an existing **elastic pool**, hello latest Powershell preview includes scripts tooupgrade your existing installation.</span></span> <span data-ttu-id="af379-107">Yüksek oranda olduğu tooupgrade yükleme toohello en son önerilen **esnek veritabanı işleri** sipariş tootake aracılığıyla kullanıma sunulan yeni işlevsellikten avantajlarından bileşenlerinde hello PowerShell API'leri.</span><span class="sxs-lookup"><span data-stu-id="af379-107">It is highly recommended tooupgrade your installation toohello latest **Elastic Database jobs** components in order tootake advantage of new functionality exposed via hello PowerShell APIs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="af379-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="af379-108">Prerequisites</span></span>
* <span data-ttu-id="af379-109">Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="af379-109">An Azure subscription.</span></span> <span data-ttu-id="af379-110">Ücretsiz deneme için bkz: [ücretsiz deneme sürümü](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="af379-110">For a free trial, see [Free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="af379-111">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="af379-111">Azure PowerShell.</span></span> <span data-ttu-id="af379-112">Hello kullanarak hello en son sürümünü yüklemek [Web Platformu yükleyicisi](http://go.microsoft.com/fwlink/p/?linkid=320376).</span><span class="sxs-lookup"><span data-stu-id="af379-112">Install hello latest version using hello [Web Platform Installer](http://go.microsoft.com/fwlink/p/?linkid=320376).</span></span> <span data-ttu-id="af379-113">Ayrıntılı bilgi için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="af379-113">For detailed information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="af379-114">[NuGet komut satırı yardımcı programı](https://nuget.org/nuget.exe) kullanılan tooinstall hello esnek veritabanı işleri paketidir.</span><span class="sxs-lookup"><span data-stu-id="af379-114">[NuGet Command-line Utility](https://nuget.org/nuget.exe) is used tooinstall hello Elastic Database jobs package.</span></span> <span data-ttu-id="af379-115">Daha fazla bilgi için http://docs.nuget.org/docs/start-here/installing-nuget bakın.</span><span class="sxs-lookup"><span data-stu-id="af379-115">For more information, see http://docs.nuget.org/docs/start-here/installing-nuget.</span></span>

## <a name="download-and-import-hello-elastic-database-jobs-powershell-package"></a><span data-ttu-id="af379-116">Karşıdan yükle ve hello esnek veritabanı işleri PowerShell paketi Al</span><span class="sxs-lookup"><span data-stu-id="af379-116">Download and import hello Elastic Database jobs PowerShell package</span></span>
1. <span data-ttu-id="af379-117">Microsoft Azure PowerShell komut penceresini başlatın ve NuGet komut satırı yardımcı programı (nuget.exe) indirdiğiniz toohello dizinine gidin.</span><span class="sxs-lookup"><span data-stu-id="af379-117">Launch Microsoft Azure PowerShell command window and navigate toohello directory where you downloaded NuGet Command-line Utility (nuget.exe).</span></span>
2. <span data-ttu-id="af379-118">İndirme ve içeri aktarma **esnek veritabanı işleri** komutu aşağıdaki hello ile Merhaba geçerli dizine paketi:</span><span class="sxs-lookup"><span data-stu-id="af379-118">Download and import **Elastic Database jobs** package into hello current directory with hello following command:</span></span>
   
        PS C:\>.\nuget install Microsoft.Azure.SqlDatabase.Jobs -prerelease
   
    <span data-ttu-id="af379-119">Merhaba **esnek veritabanı işleri** dosyaları hello yerel dizin adlı bir klasöre yerleştirilir **Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x** nerede *x.x.xxxx.x* Merhaba sürüm numarası yansıtır.</span><span class="sxs-lookup"><span data-stu-id="af379-119">hello **Elastic Database jobs** files are placed in hello local directory in a folder named **Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x** where *x.x.xxxx.x* reflects hello version number.</span></span> <span data-ttu-id="af379-120">(gerekli istemci .dll dahil) hello PowerShell cmdlet'leri hello bulunan **tools\ElasticDatabaseJobs** alt dizini hello PowerShell komut dosyaları tooinstall, yükseltme ve ayrıca kaldırma hello bulunan  **Araçlar** alt dizini.</span><span class="sxs-lookup"><span data-stu-id="af379-120">hello PowerShell cmdlets (including required client .dlls) are located in hello **tools\ElasticDatabaseJobs** sub-directory and hello PowerShell scripts tooinstall, upgrade and uninstall also reside in hello **tools** sub-directory.</span></span>
3. <span data-ttu-id="af379-121">Cd Araçlar, örneğin yazarak hello Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x klasörü altında toohello Araçlar alt dizinine gidin:</span><span class="sxs-lookup"><span data-stu-id="af379-121">Navigate toohello tools sub-directory under hello Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x folder by typing cd tools, for example:</span></span>
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools

4. <span data-ttu-id="af379-122">Merhaba.\InstallElasticDatabaseJobsCmdlets.ps1 komut dosyası toocopy hello ElasticDatabaseJobs dizini $home\Documents\WindowsPowerShell\Modules yürütün.</span><span class="sxs-lookup"><span data-stu-id="af379-122">Execute hello .\InstallElasticDatabaseJobsCmdlets.ps1 script toocopy hello ElasticDatabaseJobs directory into $home\Documents\WindowsPowerShell\Modules.</span></span> <span data-ttu-id="af379-123">Bu da otomatik olarak hello modülü kullanmak, örneğin alınır:</span><span class="sxs-lookup"><span data-stu-id="af379-123">This will also automatically import hello module for use, for example:</span></span>
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobsCmdlets.ps1
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\InstallElasticDatabaseJobsCmdlets.ps1

## <a name="install-hello-elastic-database-jobs-components-using-powershell"></a><span data-ttu-id="af379-124">PowerShell kullanarak hello esnek veritabanı işleri bileşenlerini yükle</span><span class="sxs-lookup"><span data-stu-id="af379-124">Install hello Elastic Database jobs components using PowerShell</span></span>
1. <span data-ttu-id="af379-125">Microsoft Azure PowerShell komut penceresini başlatın ve toohello \tools hello Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x klasörü altında alt dizinine gidin: cd \tools yazın</span><span class="sxs-lookup"><span data-stu-id="af379-125">Launch a Microsoft Azure PowerShell command window and navigate toohello \tools sub-directory under hello Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x folder: Type cd \tools</span></span>
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools

2. <span data-ttu-id="af379-126">Merhaba.\InstallElasticDatabaseJobs.ps1 PowerShell betiğini yürütün ve istenen değişkenleri için değerleri girin.</span><span class="sxs-lookup"><span data-stu-id="af379-126">Execute hello .\InstallElasticDatabaseJobs.ps1 PowerShell script and supply values for its requested variables.</span></span> <span data-ttu-id="af379-127">Bu komut dosyası açıklanan hello bileşenleri oluşturacak [esnek veritabanı iş bileşenleri ve fiyatlandırma](sql-database-elastic-jobs-overview.md#components-and-pricing) hello Azure bulut hizmeti yapılandırma ile birlikte tooappropriately hello bağımlı bileşenlerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="af379-127">This script will create hello components described in [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing) along with configuring hello Azure Cloud Service tooappropriately use hello dependent components.</span></span>

        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobs.ps1
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\InstallElasticDatabaseJobs.ps1

<span data-ttu-id="af379-128">Bu komutu çalıştırdığınızda bir pencere açılır girmenizi isteyen bir **kullanıcı adı** ve **parola**.</span><span class="sxs-lookup"><span data-stu-id="af379-128">When you run this command a window opens asking for a **user name** and **password**.</span></span> <span data-ttu-id="af379-129">Bu Azure kimlik bilgilerinizi değil, hello kullanıcı adı ve hello yönetici kimlik bilgileri toocreate hello yeni sunucu için istediğiniz parola girin.</span><span class="sxs-lookup"><span data-stu-id="af379-129">This is not your Azure credentials, enter hello user name and password that will be hello administrator credentials you want toocreate for hello new server.</span></span>

<span data-ttu-id="af379-130">Bu örnek çağrısının sağlanan hello parametreleri için istenen ayarlarınız değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="af379-130">hello parameters provided on this sample invocation can be modified for your desired settings.</span></span> <span data-ttu-id="af379-131">Merhaba aşağıdaki her bir parametreyi hello davranışını daha fazla bilgi sağlar:</span><span class="sxs-lookup"><span data-stu-id="af379-131">hello following provides more information on hello behavior of each parameter:</span></span>

<table style="width:100%">
  <tr>
    <th><span data-ttu-id="af379-132">Parametre</span><span class="sxs-lookup"><span data-stu-id="af379-132">Parameter</span></span></th>
    <th><span data-ttu-id="af379-133">Açıklama</span><span class="sxs-lookup"><span data-stu-id="af379-133">Description</span></span></th>
  </tr>

<tr>
    <td><span data-ttu-id="af379-134">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="af379-134">ResourceGroupName</span></span></td>
    <td><span data-ttu-id="af379-135">Yeni Azure bileşenleri oluşturulan toocontain hello oluşturulan hello Azure kaynak grubu adı sağlar.</span><span class="sxs-lookup"><span data-stu-id="af379-135">Provides hello Azure resource group name created toocontain hello newly created Azure components.</span></span> <span data-ttu-id="af379-136">Bu parametre çok varsayılan olarak "__ElasticDatabaseJob".</span><span class="sxs-lookup"><span data-stu-id="af379-136">This parameter defaults too“__ElasticDatabaseJob”.</span></span> <span data-ttu-id="af379-137">Değil toochange önerilen bu değer.</span><span class="sxs-lookup"><span data-stu-id="af379-137">It is not recommended toochange this value.</span></span></td>
    </tr>

</tr>

    <tr>
    <td><span data-ttu-id="af379-138">ResourceGroupLocation</span><span class="sxs-lookup"><span data-stu-id="af379-138">ResourceGroupLocation</span></span></td>
    <td><span data-ttu-id="af379-139">Yeni Azure bileşenleri oluşturulan hello için kullanılan hello Azure konumu toobe sağlar.</span><span class="sxs-lookup"><span data-stu-id="af379-139">Provides hello Azure location toobe used for hello newly created Azure components.</span></span> <span data-ttu-id="af379-140">Bu parametre varsayılan olarak toohello Orta ABD konumu.</span><span class="sxs-lookup"><span data-stu-id="af379-140">This parameter defaults toohello Central US location.</span></span></td>
</tr>

<tr>
    <td><span data-ttu-id="af379-141">ServiceWorkerCount</span><span class="sxs-lookup"><span data-stu-id="af379-141">ServiceWorkerCount</span></span></td>
    <td><span data-ttu-id="af379-142">Hizmet çalışanları tooinstall Hello sayısını sağlar.</span><span class="sxs-lookup"><span data-stu-id="af379-142">Provides hello number of service workers tooinstall.</span></span> <span data-ttu-id="af379-143">Bu parametre too1 varsayılan olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="af379-143">This parameter defaults too1.</span></span> <span data-ttu-id="af379-144">Daha yüksek bir sayı çalışanı hello hizmeti ve tooprovide yüksek kullanılabilirlik çıkışı kullanılan tooscale olabilir.</span><span class="sxs-lookup"><span data-stu-id="af379-144">A higher number of workers can be used tooscale out hello service and tooprovide high availability.</span></span> <span data-ttu-id="af379-145">Toouse "2" Merhaba hizmetinin yüksek kullanılabilirliğin gerektiği dağıtımlar için önerilir.</span><span class="sxs-lookup"><span data-stu-id="af379-145">It is recommended toouse “2” for deployments that require high availability of hello service.</span></span></td>
    </tr>

</tr>
    <tr>
    <td><span data-ttu-id="af379-146">ServiceVmSize</span><span class="sxs-lookup"><span data-stu-id="af379-146">ServiceVmSize</span></span></td>
    <td><span data-ttu-id="af379-147">Merhaba VM boyutu hello bulut hizmeti içinde kullanımı sağlar.</span><span class="sxs-lookup"><span data-stu-id="af379-147">Provides hello VM size for usage within hello Cloud Service.</span></span> <span data-ttu-id="af379-148">Bu parametre tooA0 varsayılan olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="af379-148">This parameter defaults tooA0.</span></span> <span data-ttu-id="af379-149">Parametre değerlerini A0/A1/A2/A3 hello çalışan rolü toouse çok küçük/küçük/Orta/büyük boyutu sırasıyla neden kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="af379-149">Parameters values of A0/A1/A2/A3 are accepted which cause hello worker role toouse an ExtraSmall/Small/Medium/Large size, respectively.</span></span> <span data-ttu-id="af379-150">FO çalışan rolü boyutları hakkında daha fazla bilgi görmek [esnek veritabanı iş bileşenleri ve fiyatlandırma](sql-database-elastic-jobs-overview.md#components-and-pricing).</span><span class="sxs-lookup"><span data-stu-id="af379-150">Fo more information on worker role sizes, see [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing).</span></span></td>
</tr>

</tr>
    <tr>
    <td><span data-ttu-id="af379-151">SqlServerDatabaseSlo</span><span class="sxs-lookup"><span data-stu-id="af379-151">SqlServerDatabaseSlo</span></span></td>
    <td><span data-ttu-id="af379-152">Merhaba hizmet düzeyi hedefi Standard edition için sağlar.</span><span class="sxs-lookup"><span data-stu-id="af379-152">Provides hello service level objective for a Standard edition.</span></span> <span data-ttu-id="af379-153">Bu parametre tooS0 varsayılan olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="af379-153">This parameter defaults tooS0.</span></span> <span data-ttu-id="af379-154">Parametre değerlerini S0/S1/S2/S3 hello Azure SQL veritabanı neden kabul edilir toouse hello ilgili SLO.</span><span class="sxs-lookup"><span data-stu-id="af379-154">Parameter values of S0/S1/S2/S3 are accepted which cause hello Azure SQL Database toouse hello respective SLO.</span></span> <span data-ttu-id="af379-155">SQL veritabanı Slo'lar hakkında daha fazla bilgi için bkz: [esnek veritabanı iş bileşenleri ve fiyatlandırma](sql-database-elastic-jobs-overview.md#components-and-pricing).</span><span class="sxs-lookup"><span data-stu-id="af379-155">For more information on SQL Database SLOs, see [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing).</span></span></td>
</tr>

</tr>
    <tr>
    <td><span data-ttu-id="af379-156">SqlServerAdministratorUserName</span><span class="sxs-lookup"><span data-stu-id="af379-156">SqlServerAdministratorUserName</span></span></td>
    <td><span data-ttu-id="af379-157">Hello Yöneticisi kullanıcı adı için yeni Azure SQL Database sunucusu oluşturulan hello sağlar.</span><span class="sxs-lookup"><span data-stu-id="af379-157">Provides hello admin user name for hello newly created Azure SQL Database server.</span></span> <span data-ttu-id="af379-158">Belirtilmediğinde, bir PowerShell kimlik bilgileri penceresi hello kimlik bilgileri tooprompt açın.</span><span class="sxs-lookup"><span data-stu-id="af379-158">When not specified, a PowerShell credentials window will open tooprompt for hello credentials.</span></span></td>
</tr>

</tr>
    <tr>
    <td><span data-ttu-id="af379-159">SqlServerAdministratorPassword</span><span class="sxs-lookup"><span data-stu-id="af379-159">SqlServerAdministratorPassword</span></span></td>
    <td><span data-ttu-id="af379-160">Merhaba yönetici parolası yeni Azure SQL Database sunucusu oluşturulan Merhaba sağlar.</span><span class="sxs-lookup"><span data-stu-id="af379-160">Provides hello admin password for hello newly created Azure SQL Database server.</span></span> <span data-ttu-id="af379-161">Sağlanan değil, bir PowerShell kimlik bilgileri penceresi hello kimlik bilgileri tooprompt açın.</span><span class="sxs-lookup"><span data-stu-id="af379-161">When not provided, a PowerShell credentials window will open tooprompt for hello credentials.</span></span></td>
</tr>
</table>

<span data-ttu-id="af379-162">Çok sayıda paralel çok sayıda veritabanı karşı çalışan işleri sahip hedef sistemleri için toospecify parametreleri gibi önerilir: - ServiceWorkerCount 2 - ServiceVmSize A2 - SqlServerDatabaseSlo S2.</span><span class="sxs-lookup"><span data-stu-id="af379-162">For systems that target having large numbers of jobs running in parallel against a large number of databases, it is recommended toospecify parameters such as: -ServiceWorkerCount 2 -ServiceVmSize A2 -SqlServerDatabaseSlo S2.</span></span>

    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobs.ps1
    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>.\InstallElasticDatabaseJobs.ps1 -ServiceWorkerCount 2 -ServiceVmSize A2 -SqlServerDatabaseSlo S2

## <a name="update-an-existing-elastic-database-jobs-components-installation-using-powershell"></a><span data-ttu-id="af379-163">PowerShell kullanarak var olan esnek veritabanı işleri bileşenleri yüklemeyi güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="af379-163">Update an existing Elastic Database jobs components installation using PowerShell</span></span>
<span data-ttu-id="af379-164">**Esnek veritabanı iş** içinde var olan bir yüklemesini ölçek ve yüksek kullanılabilirlik için güncelleştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="af379-164">**Elastic Database jobs** can be updated within an existing installation for scale and high-availability.</span></span> <span data-ttu-id="af379-165">Bu işlem toodrop gerek kalmadan servis kodu gelecekteki yükseltmeler için sağlar ve hello denetim veritabanı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="af379-165">This process allows for future upgrades of service code without having toodrop and recreate hello control database.</span></span> <span data-ttu-id="af379-166">Bu işlem ayrıca hello içinde kullanılabilir aynı sürüm toomodify hello hizmet VM boyutu veya hello server çalışan sayısı.</span><span class="sxs-lookup"><span data-stu-id="af379-166">This process can also be used within hello same version toomodify hello service VM size or hello server worker count.</span></span>

<span data-ttu-id="af379-167">tooupdate hello VM boyutu yüklemesinin parametrelerle betik aşağıdaki çalışma hello tercih ettiğiniz toohello değerleri güncelleştirildi.</span><span class="sxs-lookup"><span data-stu-id="af379-167">tooupdate hello VM size of an installation, run hello following script with parameters updated toohello values of your choice.</span></span>

    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>Unblock-File .\UpdateElasticDatabaseJobs.ps1
    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>.\UpdateElasticDatabaseJobs.ps1 -ServiceVmSize A1 -ServiceWorkerCount 2

<table style="width:100%">
  <tr>
  <th><span data-ttu-id="af379-168">Parametre</span><span class="sxs-lookup"><span data-stu-id="af379-168">Parameter</span></span></th>
  <th><span data-ttu-id="af379-169">Açıklama</span><span class="sxs-lookup"><span data-stu-id="af379-169">Description</span></span></th>
</tr>

  <tr>
    <td><span data-ttu-id="af379-170">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="af379-170">ResourceGroupName</span></span></td>
    <td><span data-ttu-id="af379-171">Merhaba esnek veritabanı iş bileşenler ilk yüklendiğinde kullanılan hello Azure kaynak grubu adını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="af379-171">Identifies hello Azure resource group name used when hello Elastic Database job components were initially installed.</span></span> <span data-ttu-id="af379-172">Bu parametre çok varsayılan olarak "__ElasticDatabaseJob".</span><span class="sxs-lookup"><span data-stu-id="af379-172">This parameter defaults too“__ElasticDatabaseJob”.</span></span> <span data-ttu-id="af379-173">Bunu olmadığından toochange önerilen bu değer bu parametre toospecify sahip olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="af379-173">Since it is not recommended toochange this value, you shouldn't have toospecify this parameter.</span></span></td>
    </tr>
</tr>

</tr>

  <tr>
    <td><span data-ttu-id="af379-174">ServiceWorkerCount</span><span class="sxs-lookup"><span data-stu-id="af379-174">ServiceWorkerCount</span></span></td>
    <td><span data-ttu-id="af379-175">Hizmet çalışanları tooinstall Hello sayısını sağlar.</span><span class="sxs-lookup"><span data-stu-id="af379-175">Provides hello number of service workers tooinstall.</span></span>  <span data-ttu-id="af379-176">Bu parametre too1 varsayılan olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="af379-176">This parameter defaults too1.</span></span>  <span data-ttu-id="af379-177">Daha yüksek bir sayı çalışanı hello hizmeti ve tooprovide yüksek kullanılabilirlik çıkışı kullanılan tooscale olabilir.</span><span class="sxs-lookup"><span data-stu-id="af379-177">A higher number of workers can be used tooscale out hello service and tooprovide high availability.</span></span>  <span data-ttu-id="af379-178">Toouse "2" Merhaba hizmetinin yüksek kullanılabilirliğin gerektiği dağıtımlar için önerilir.</span><span class="sxs-lookup"><span data-stu-id="af379-178">It is recommended toouse “2” for deployments that require high availability of hello service.</span></span></td>
</tr>

</tr>

    <tr>
    <td><span data-ttu-id="af379-179">ServiceVmSize</span><span class="sxs-lookup"><span data-stu-id="af379-179">ServiceVmSize</span></span></td>
    <td><span data-ttu-id="af379-180">Merhaba VM boyutu hello bulut hizmeti içinde kullanımı sağlar.</span><span class="sxs-lookup"><span data-stu-id="af379-180">Provides hello VM size for usage within hello Cloud Service.</span></span> <span data-ttu-id="af379-181">Bu parametre tooA0 varsayılan olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="af379-181">This parameter defaults tooA0.</span></span> <span data-ttu-id="af379-182">Parametre değerlerini A0/A1/A2/A3 hello çalışan rolü toouse çok küçük/küçük/Orta/büyük boyutu sırasıyla neden kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="af379-182">Parameters values of A0/A1/A2/A3 are accepted which cause hello worker role toouse an ExtraSmall/Small/Medium/Large size, respectively.</span></span> <span data-ttu-id="af379-183">FO çalışan rolü boyutları hakkında daha fazla bilgi görmek [esnek veritabanı iş bileşenleri ve fiyatlandırma](sql-database-elastic-jobs-overview.md#components-and-pricing).</span><span class="sxs-lookup"><span data-stu-id="af379-183">Fo more information on worker role sizes, see [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing).</span></span></td>
</tr>

</table>

## <a name="install-hello-elastic-database-jobs-components-using-hello-portal"></a><span data-ttu-id="af379-184">Merhaba Portal kullanarak hello esnek veritabanı işleri bileşenlerini yükle</span><span class="sxs-lookup"><span data-stu-id="af379-184">Install hello Elastic Database jobs components using hello Portal</span></span>
<span data-ttu-id="af379-185">Bulduktan sonra [bir esnek havuz oluşturulan](sql-database-elastic-pool-manage-portal.md), yükleyebileceğiniz **esnek veritabanı işleri** bileşenleri tooenable yürütme hello esnek havuzdaki her veritabanında yönetim görevleri.</span><span class="sxs-lookup"><span data-stu-id="af379-185">Once you have [created an elastic pool](sql-database-elastic-pool-manage-portal.md), you can install **Elastic Database jobs** components tooenable execution of administrative tasks against each database in hello elastic pool.</span></span> <span data-ttu-id="af379-186">Ne zaman kullanarak hello aksine **esnek veritabanı işleri** PowerShell API'lerinden hello portal arabirimidir şu anda kısıtlı tooonly var olan bir havuzu karşı çalıştırma.</span><span class="sxs-lookup"><span data-stu-id="af379-186">Unlike when using hello **Elastic Database jobs** PowerShell APIs, hello portal interface is currently restricted tooonly executing against an existing pool.</span></span>

<span data-ttu-id="af379-187">**Zaman toocomplete tahmini:** 10 dakika.</span><span class="sxs-lookup"><span data-stu-id="af379-187">**Estimated time toocomplete:** 10 minutes.</span></span>

1. <span data-ttu-id="af379-188">Merhaba aracılığıyla hello esnek havuzun hello Pano görünümden [Azure Portal](https://portal.azure.com/#) , tıklatın **oluşturma işi**.</span><span class="sxs-lookup"><span data-stu-id="af379-188">From hello dashboard view of hello elastic pool via hello [Azure Portal](https://portal.azure.com/#) , click **Create job**.</span></span>
2. <span data-ttu-id="af379-189">Hello için bir işi ilk kez oluşturuyorsanız, yüklemelisiniz **esnek veritabanı işleri** tıklayarak **Önizleme koşulları**.</span><span class="sxs-lookup"><span data-stu-id="af379-189">If you are creating a job for hello first time, you must install **Elastic Database jobs** by clicking **PREVIEW TERMS**.</span></span>
3. <span data-ttu-id="af379-190">Onay kutusunu tıklatarak hello koşulları hello kabul edin.</span><span class="sxs-lookup"><span data-stu-id="af379-190">Accept hello terms by clicking hello checkbox.</span></span>
4. <span data-ttu-id="af379-191">Yükleme Hello "Hizmetler" Görüntüle'yi tıklatın **iş kimlik bilgilerini**.</span><span class="sxs-lookup"><span data-stu-id="af379-191">In hello "Install services" view, click **JOB CREDENTIALS**.</span></span>
   
    ![Merhaba Hizmetleri Yükleniyor][1]
5. <span data-ttu-id="af379-193">Bir kullanıcı adı ve veritabanı yönetici parolasını yazın Merhaba yüklemesinin bir parçası olarak, yeni bir Azure SQL veritabanı sunucusu oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="af379-193">Type a user name and password for a database admin. As part of hello installation, a new Azure SQL Database server is created.</span></span> <span data-ttu-id="af379-194">Bu yeni sunucu içinde hello denetim veritabanı olarak bilinen yeni bir veritabanı oluşturulur ve esnek veritabanı işleri toocontain hello meta veriler kullanılır.</span><span class="sxs-lookup"><span data-stu-id="af379-194">Within this new server, a new database, known as hello control database, is created and used toocontain hello meta data for Elastic Database jobs.</span></span> <span data-ttu-id="af379-195">Merhaba kullanıcı adı ve parola burada oluşturulan toohello denetim veritabanında günlük hello amacı için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="af379-195">hello user name and password created here are used for hello purpose of logging in toohello control database.</span></span> <span data-ttu-id="af379-196">Ayrı bir kimlik bilgisi komut dosyası yürütme hello havuz içindeki hello veritabanlarında için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="af379-196">A separate credential is used for script execution against hello databases within hello pool.</span></span>
   
    ![Kullanıcı adı ve parola oluşturun.][2]
6. <span data-ttu-id="af379-198">Merhaba Tamam düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="af379-198">Click hello OK button.</span></span> <span data-ttu-id="af379-199">Merhaba bileşenleri oluşturulan sizin için birkaç dakika içinde yeni bir [kaynak grubu](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="af379-199">hello components are created for you in a few minutes in a new [Resource group](../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="af379-200">Merhaba yeni kaynak grubu sabitlendiği toohello Panosu, aşağıda gösterildiği gibi başlatın.</span><span class="sxs-lookup"><span data-stu-id="af379-200">hello new resource group is pinned toohello start board, as shown below.</span></span> <span data-ttu-id="af379-201">Oluşturduktan sonra esnek veritabanı işleri (bulut hizmeti, SQL veritabanı, hizmet veri yolu ve depolama) tüm hello grubunda oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="af379-201">Once created, elastic database jobs (Cloud Service, SQL Database, Service Bus, and Storage) are all created in hello group.</span></span>
   
    ![Başlangıç Panosu kaynak grubunda][3]
7. <span data-ttu-id="af379-203">Toocreate deneyin veya esnek veritabanı işleri yüklüyor olsa da, sağlanırken bir işi yönetiyorsanız **kimlik bilgileri** iletiden hello görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="af379-203">If you attempt toocreate or manage a job while elastic database jobs is installing, when providing **Credentials** you will see hello following message.</span></span>
   
    ![Dağıtımı hala devam ediyor][4]

<span data-ttu-id="af379-205">Kaldırma işlemi gerekiyorsa, hello kaynak grubunu silin.</span><span class="sxs-lookup"><span data-stu-id="af379-205">If uninstallation is required, delete hello resource group.</span></span> <span data-ttu-id="af379-206">Bkz: [nasıl toouninstall hello esnek veritabanı iş bileşenleri](sql-database-elastic-jobs-uninstall.md).</span><span class="sxs-lookup"><span data-stu-id="af379-206">See [How toouninstall hello Elastic Database job components](sql-database-elastic-jobs-uninstall.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="af379-207">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="af379-207">Next steps</span></span>
<span data-ttu-id="af379-208">Betik yürütme hello grubunda, daha fazla bilgi için her bir veritabanına oluşturulan için hello uygun haklara sahip bir kimlik bilgisi olun [SQL veritabanınızın güvenliğini sağlama](sql-database-manage-logins.md).</span><span class="sxs-lookup"><span data-stu-id="af379-208">Ensure a credential with hello appropriate rights for script execution is created on each database in hello group, for more information see [Securing your SQL Database](sql-database-manage-logins.md).</span></span>
<span data-ttu-id="af379-209">Bkz: [oluşturma ve bir esnek veritabanı işlerini yönetme](sql-database-elastic-jobs-create-and-manage.md) tooget başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="af379-209">See [Creating and managing an Elastic Database jobs](sql-database-elastic-jobs-create-and-manage.md) tooget started.</span></span>

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-service-installation/screen-1.png
[2]: ./media/sql-database-elastic-jobs-service-installation/credentials.png
[3]: ./media/sql-database-elastic-jobs-service-installation/start-board.png
[4]: ./media/sql-database-elastic-jobs-service-installation/not-done.png
