---
title: SharePoint grubunun Azure DPM/Azure yedekleme sunucusu koruma | Microsoft Docs
description: "Bu makale, Azure için SharePoint grubunun DPM/Azure yedekleme sunucusu koruma genel bir bakış sağlar"
services: backup
documentationcenter: 
author: adigan
manager: Nkolli1
editor: 
ms.assetid: e0c0c252-dc1d-4072-b777-7222c13950b0
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/29/2016
ms.author: adigan;giridham;jimpark;trinadhk;markgal
ms.openlocfilehash: 1bbf3233169fa9966e3dd0fac18ee448f26caa6b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="back-up-a-sharepoint-farm-to-azure"></a><span data-ttu-id="5475a-103">Bir SharePoint grubunu Azure’a yedekleme</span><span class="sxs-lookup"><span data-stu-id="5475a-103">Back up a SharePoint farm to Azure</span></span>
<span data-ttu-id="5475a-104">SharePoint grubunun kurulumu diğer veri kaynaklarını yedekleyen benzer şekilde, System Center Data Protection Manager (DPM) kullanarak Microsoft Azure'a yedekleyin.</span><span class="sxs-lookup"><span data-stu-id="5475a-104">You back up a SharePoint farm to Microsoft Azure by using System Center Data Protection Manager (DPM) in much the same way that you back up other data sources.</span></span> <span data-ttu-id="5475a-105">Azure yedekleme günlük oluşturmak için yedekleme zamanlamasını esneklik sağlar, haftalık, aylık veya yıllık yedekleme noktaları ve çeşitli yedekleme noktaları için bekletme ilkesi seçenekler sunar.</span><span class="sxs-lookup"><span data-stu-id="5475a-105">Azure Backup provides flexibility in the backup schedule to create daily, weekly, monthly, or yearly backup points and gives you retention policy options for various backup points.</span></span> <span data-ttu-id="5475a-106">DPM, Hızlı Kurtarma süresi hedefi (RTO) için yerel disk kopyaları depolamak ve ekonomik, uzun vadeli bekletme için Azure kopyaları depolamak için yeteneği sağlar.</span><span class="sxs-lookup"><span data-stu-id="5475a-106">DPM provides the capability to store local disk copies for quick recovery-time objectives (RTO) and to store copies to Azure for economical, long-term retention.</span></span>

## <a name="sharepoint-supported-versions-and-related-protection-scenarios"></a><span data-ttu-id="5475a-107">SharePoint desteklenen sürümleri ve ilgili koruma senaryoları</span><span class="sxs-lookup"><span data-stu-id="5475a-107">SharePoint supported versions and related protection scenarios</span></span>
<span data-ttu-id="5475a-108">Azure yedekleme DPM için aşağıdaki senaryoları destekler:</span><span class="sxs-lookup"><span data-stu-id="5475a-108">Azure Backup for DPM supports the following scenarios:</span></span>

| <span data-ttu-id="5475a-109">İş yükü</span><span class="sxs-lookup"><span data-stu-id="5475a-109">Workload</span></span> | <span data-ttu-id="5475a-110">Sürüm</span><span class="sxs-lookup"><span data-stu-id="5475a-110">Version</span></span> | <span data-ttu-id="5475a-111">SharePoint dağıtımı</span><span class="sxs-lookup"><span data-stu-id="5475a-111">SharePoint deployment</span></span> | <span data-ttu-id="5475a-112">DPM dağıtım türü</span><span class="sxs-lookup"><span data-stu-id="5475a-112">DPM deployment type</span></span> | <span data-ttu-id="5475a-113">DPM - System Center 2012 R2</span><span class="sxs-lookup"><span data-stu-id="5475a-113">DPM - System Center 2012 R2</span></span> | <span data-ttu-id="5475a-114">Koruma ve kurtarma</span><span class="sxs-lookup"><span data-stu-id="5475a-114">Protection and recovery</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="5475a-115">SharePoint</span><span class="sxs-lookup"><span data-stu-id="5475a-115">SharePoint</span></span> |<span data-ttu-id="5475a-116">SharePoint 2013, SharePoint 2010, SharePoint 2007'de, SharePoint 3.0</span><span class="sxs-lookup"><span data-stu-id="5475a-116">SharePoint 2013, SharePoint 2010, SharePoint 2007, SharePoint 3.0</span></span> |<span data-ttu-id="5475a-117">Bir fiziksel sunucu veya Hyper-V/VMware sanal makinesi dağıtılan SharePoint</span><span class="sxs-lookup"><span data-stu-id="5475a-117">SharePoint deployed as a physical server or Hyper-V/VMware virtual machine</span></span> <br> -------------- <br> <span data-ttu-id="5475a-118">SQL AlwaysOn</span><span class="sxs-lookup"><span data-stu-id="5475a-118">SQL AlwaysOn</span></span> |<span data-ttu-id="5475a-119">Fiziksel sunucu veya şirket içi Hyper-V sanal makine</span><span class="sxs-lookup"><span data-stu-id="5475a-119">Physical server or on-premises Hyper-V virtual machine</span></span> |<span data-ttu-id="5475a-120">Destekler yedekten Azure için Güncelleştirme Paketi 5</span><span class="sxs-lookup"><span data-stu-id="5475a-120">Supports backup to Azure from Update Rollup 5</span></span> |<span data-ttu-id="5475a-121">SharePoint grubu kurtarma seçeneklerini koruma: Kurtarma grubu, veritabanı ve disk kurtarma noktalarından dosya veya liste öğesi.</span><span class="sxs-lookup"><span data-stu-id="5475a-121">Protect SharePoint Farm recovery options: Recovery farm, database, and file or list item from disk recovery points.</span></span>  <span data-ttu-id="5475a-122">Azure kurtarma noktalarından grubu ve veritabanı kurtarma.</span><span class="sxs-lookup"><span data-stu-id="5475a-122">Farm and database recovery from Azure recovery points.</span></span> |

## <a name="before-you-start"></a><span data-ttu-id="5475a-123">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="5475a-123">Before you start</span></span>
<span data-ttu-id="5475a-124">Bir SharePoint grubuna Azure yedekleme önce onaylamak için gereken birkaç nokta vardır.</span><span class="sxs-lookup"><span data-stu-id="5475a-124">There are a few things you need to confirm before you back up a SharePoint farm to Azure.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="5475a-125">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="5475a-125">Prerequisites</span></span>
<span data-ttu-id="5475a-126">Devam etmeden önce tüm karşıladığınızdan emin olun [Microsoft Azure Yedekleme kullanılarak önkoşulları](backup-azure-dpm-introduction.md#prerequisites) iş yüklerini korumak için.</span><span class="sxs-lookup"><span data-stu-id="5475a-126">Before you proceed, make sure that you have met all the [prerequisites for using Microsoft Azure Backup](backup-azure-dpm-introduction.md#prerequisites) to protect workloads.</span></span> <span data-ttu-id="5475a-127">Önkoşullar için bazı görevler aşağıdakileri içerir: bir yedekleme kasası oluşturun, kasa kimlik bilgilerini indirme, Azure Yedekleme aracısı yükleyin ve DPM/Azure yedekleme sunucusu kasayla kaydedin.</span><span class="sxs-lookup"><span data-stu-id="5475a-127">Some tasks for prerequisites include: create a backup vault, download vault credentials, install Azure Backup Agent, and register DPM/Azure Backup Server with the vault.</span></span>

### <a name="dpm-agent"></a><span data-ttu-id="5475a-128">DPM Aracısı</span><span class="sxs-lookup"><span data-stu-id="5475a-128">DPM agent</span></span>
<span data-ttu-id="5475a-129">DPM Aracısı, SharePoint, SQL Server çalıştıran sunucular ve SharePoint grubunun parçası olan diğer tüm sunucuları çalıştıran sunucuda yüklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="5475a-129">The DPM agent must be installed on the server that's running SharePoint, the servers that are running SQL Server, and all other servers that are part of the SharePoint farm.</span></span> <span data-ttu-id="5475a-130">Koruma aracısını ayarlama hakkında daha fazla bilgi için bkz: [Kurulum koruma Aracısı](https://technet.microsoft.com/library/hh758034\(v=sc.12\).aspx).</span><span class="sxs-lookup"><span data-stu-id="5475a-130">For more information about how to set up the protection agent, see [Setup Protection Agent](https://technet.microsoft.com/library/hh758034\(v=sc.12\).aspx).</span></span>  <span data-ttu-id="5475a-131">Aracı yalnızca bir tek web front end (WFE) sunucusuna yükleyin istisnadır.</span><span class="sxs-lookup"><span data-stu-id="5475a-131">The one exception is that you install the agent only on a single web front end (WFE) server.</span></span> <span data-ttu-id="5475a-132">DPM yalnızca koruma için giriş noktası olarak hizmet verecek bir WFE sunucusunda aracının gerekir.</span><span class="sxs-lookup"><span data-stu-id="5475a-132">DPM needs the agent on one WFE server only to serve as the entry point for protection.</span></span>

### <a name="sharepoint-farm"></a><span data-ttu-id="5475a-133">SharePoint grubu</span><span class="sxs-lookup"><span data-stu-id="5475a-133">SharePoint farm</span></span>
<span data-ttu-id="5475a-134">Gruptaki her 10 milyon öğe için en az 2 GB alan DPM klasörünün bulunduğu birimde olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5475a-134">For every 10 million items in the farm, there must be at least 2 GB of space on the volume where the DPM folder is located.</span></span> <span data-ttu-id="5475a-135">Bu alanı katalog oluşturma için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="5475a-135">This space is required for catalog generation.</span></span> <span data-ttu-id="5475a-136">Belirli öğeleri (site koleksiyonları, siteler, listeler, belge kitaplıkları, klasörler, tek tek belgeler ve liste öğeleri) kurtarmak DPM için katalog oluşturma her içerik veritabanında bulunan URL'lerin bir listesini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5475a-136">For DPM to recover specific items (site collections, sites, lists, document libraries, folders, individual documents, and list items), catalog generation creates a list of the URLs that are contained within each content database.</span></span> <span data-ttu-id="5475a-137">Kurtarılabilir öğe bölmesinde URL'lerin listesini görüntüleyebilirsiniz **kurtarma** görev alanındaki DPM Yönetici Konsolu'nun.</span><span class="sxs-lookup"><span data-stu-id="5475a-137">You can view the list of URLs in the recoverable item pane in the **Recovery** task area of DPM Administrator Console.</span></span>

### <a name="sql-server"></a><span data-ttu-id="5475a-138">SQL Server</span><span class="sxs-lookup"><span data-stu-id="5475a-138">SQL Server</span></span>
<span data-ttu-id="5475a-139">DPM LocalSystem hesabı olarak çalışır.</span><span class="sxs-lookup"><span data-stu-id="5475a-139">DPM runs as a LocalSystem account.</span></span> <span data-ttu-id="5475a-140">SQL Server veritabanlarını yedeklemek için DPM SQL Server çalıştıran sunucu için bu hesabı üzerinde sysadmin ayrıcalıkları gerekir.</span><span class="sxs-lookup"><span data-stu-id="5475a-140">To back up SQL Server databases, DPM needs sysadmin privileges on that account for the server that's running SQL Server.</span></span> <span data-ttu-id="5475a-141">Kümesine NT AUTHORITY\SYSTEM *sysadmin* önce SQL Server çalıştıran sunucuda yedekleyin.</span><span class="sxs-lookup"><span data-stu-id="5475a-141">Set NT AUTHORITY\SYSTEM to *sysadmin* on the server that's running SQL Server before you back it up.</span></span>

<span data-ttu-id="5475a-142">SharePoint grubu SQL Server diğer adlarıyla yapılandırılmış SQL Server veritabanlarını ise, DPM korunacak ön uç Web sunucusunda SQL Server istemci bileşenlerini yükleyin.</span><span class="sxs-lookup"><span data-stu-id="5475a-142">If the SharePoint farm has SQL Server databases that are configured with SQL Server aliases, install the SQL Server client components on the front-end Web server that DPM will protect.</span></span>

### <a name="sharepoint-server"></a><span data-ttu-id="5475a-143">SharePoint Server</span><span class="sxs-lookup"><span data-stu-id="5475a-143">SharePoint Server</span></span>
<span data-ttu-id="5475a-144">Performans SharePoint grubu boyutu gibi birçok faktöre bağlıdır, ancak genel bir yönerge olarak 25 TB SharePoint grubunu bir DPM sunucusu koruyabilir.</span><span class="sxs-lookup"><span data-stu-id="5475a-144">While performance depends on many factors such as size of SharePoint farm, as general guidance one DPM server can protect a 25 TB SharePoint farm.</span></span>

### <a name="dpm-update-rollup-5"></a><span data-ttu-id="5475a-145">DPM Güncelleştirme Paketi 5</span><span class="sxs-lookup"><span data-stu-id="5475a-145">DPM Update Rollup 5</span></span>
<span data-ttu-id="5475a-146">SharePoint grubunun azure'a korumayı başlatmak için DPM Güncelleştirme Paketi 5 veya sonraki sürümünü yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="5475a-146">To begin protection of a SharePoint farm to Azure, you need to install DPM Update Rollup 5 or later.</span></span> <span data-ttu-id="5475a-147">Güncelleştirme Paketi 5 grubu SQL AlwaysOn kullanarak yapılandırılmışsa Azure bir SharePoint grubuna koruma olanağı sağlar.</span><span class="sxs-lookup"><span data-stu-id="5475a-147">Update Rollup 5 provides the ability to protect a SharePoint farm to Azure if the farm is configured by using SQL AlwaysOn.</span></span>
<span data-ttu-id="5475a-148">Daha fazla bilgi için bkz: blog tanıtır post [DPM Güncelleştirme Paketi 5](http://blogs.technet.com/b/dpm/archive/2015/02/11/update-rollup-5-for-system-center-2012-r2-data-protection-manager-is-now-available.aspx)</span><span class="sxs-lookup"><span data-stu-id="5475a-148">For more information, see the blog post that introduces [DPM Update Rollup 5](http://blogs.technet.com/b/dpm/archive/2015/02/11/update-rollup-5-for-system-center-2012-r2-data-protection-manager-is-now-available.aspx)</span></span>

### <a name="whats-not-supported"></a><span data-ttu-id="5475a-149">Desteklenmeyen durumlar</span><span class="sxs-lookup"><span data-stu-id="5475a-149">What's not supported</span></span>
* <span data-ttu-id="5475a-150">Bir SharePoint grubu koruyan DPM arama dizinlerini veya uygulama hizmeti veritabanlarını koruma sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="5475a-150">DPM that protects a SharePoint farm does not protect search indexes or application service databases.</span></span> <span data-ttu-id="5475a-151">Bu veritabanlarını koruma ayrı olarak yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5475a-151">You will need to configure the protection of these databases separately.</span></span>
* <span data-ttu-id="5475a-152">DPM, genişleme dosya sunucusu (SOFS) paylaşımları üzerinde barındırılan SharePoint SQL Server veritabanlarını yedekleme sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="5475a-152">DPM does not provide backup of SharePoint SQL Server databases that are hosted on scale-out file server (SOFS) shares.</span></span>

## <a name="configure-sharepoint-protection"></a><span data-ttu-id="5475a-153">SharePoint korumasını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="5475a-153">Configure SharePoint protection</span></span>
<span data-ttu-id="5475a-154">SharePoint'i koruma için DPM kullanmadan önce kullanarak SharePoint VSS yazıcısı hizmetini (WSS yazıcısı hizmeti) yapılandırmanız gerekir **ConfigureSharePoint.exe**.</span><span class="sxs-lookup"><span data-stu-id="5475a-154">Before you can use DPM to protect SharePoint, you must configure the SharePoint VSS Writer service (WSS Writer service) by using **ConfigureSharePoint.exe**.</span></span>

<span data-ttu-id="5475a-155">Bulabileceğiniz **ConfigureSharePoint.exe** [DPM yükleme yolu] \bin klasöründe ön uç web sunucusunda.</span><span class="sxs-lookup"><span data-stu-id="5475a-155">You can find **ConfigureSharePoint.exe** in the [DPM Installation Path]\bin folder on the front-end web server.</span></span> <span data-ttu-id="5475a-156">Bu araç SharePoint grubu için kimlik bilgileriyle koruma aracısını sağlar.</span><span class="sxs-lookup"><span data-stu-id="5475a-156">This tool provides the protection agent with the credentials for the SharePoint farm.</span></span> <span data-ttu-id="5475a-157">Bu tek bir WFE sunucusunda çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="5475a-157">You run it on a single WFE server.</span></span> <span data-ttu-id="5475a-158">Birden çok WFE sunucunuz varsa, bir koruma grubu yapılandırırken yalnızca bir tanesini seçin.</span><span class="sxs-lookup"><span data-stu-id="5475a-158">If you have multiple WFE servers, select just one when you configure a protection group.</span></span>

### <a name="to-configure-the-sharepoint-vss-writer-service"></a><span data-ttu-id="5475a-159">SharePoint VSS yazıcısı hizmetini yapılandırmak için</span><span class="sxs-lookup"><span data-stu-id="5475a-159">To configure the SharePoint VSS Writer service</span></span>
1. <span data-ttu-id="5475a-160">WFE sunucusundaki bir komut isteminde [DPM yükleme konumuna] \bin\ konumuna gidin.</span><span class="sxs-lookup"><span data-stu-id="5475a-160">On the WFE server, at a command prompt, go to [DPM installation location]\bin\\</span></span>
2. <span data-ttu-id="5475a-161">ConfigureSharePoint - EnableSharePointProtection girin.</span><span class="sxs-lookup"><span data-stu-id="5475a-161">Enter ConfigureSharePoint -EnableSharePointProtection.</span></span>
3. <span data-ttu-id="5475a-162">Grup Yöneticisi kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="5475a-162">Enter the farm administrator credentials.</span></span> <span data-ttu-id="5475a-163">Bu hesap, WFE sunucusunda yerel yönetici grubunun bir üyesi olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5475a-163">This account should be a member of the local Administrator group on the WFE server.</span></span> <span data-ttu-id="5475a-164">Grup Yöneticisi yerel değilse yönetici WFE sunucusunda aşağıdaki izinleri verin:</span><span class="sxs-lookup"><span data-stu-id="5475a-164">If the farm administrator isn’t a local admin grant the following permissions on the WFE server:</span></span>
   * <span data-ttu-id="5475a-165">WSS_Admin_WPG grubu tam denetimini DPM klasörünü (% Program Files%\Microsoft Data Protection Manager\DPM) verin.</span><span class="sxs-lookup"><span data-stu-id="5475a-165">Grant the WSS_Admin_WPG group full control to the DPM folder (%Program Files%\Microsoft Data Protection Manager\DPM).</span></span>
   * <span data-ttu-id="5475a-166">WSS_Admin_WPG grubu okuma erişimini (HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager) DPM kayıt defteri anahtarına verin.</span><span class="sxs-lookup"><span data-stu-id="5475a-166">Grant the WSS_Admin_WPG group read access to the DPM Registry key (HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager).</span></span>

> [!NOTE]
> <span data-ttu-id="5475a-167">SharePoint grubu yönetici kimlik bilgilerinde bir değişiklik olduğunda ConfigureSharePoint.exe yeniden çalıştırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5475a-167">You’ll need to rerun ConfigureSharePoint.exe whenever there’s a change in the SharePoint farm administrator credentials.</span></span>
> 
> 

## <a name="back-up-a-sharepoint-farm-by-using-dpm"></a><span data-ttu-id="5475a-168">DPM kullanarak bir SharePoint grubunun kurulumu yedekleyin</span><span class="sxs-lookup"><span data-stu-id="5475a-168">Back up a SharePoint farm by using DPM</span></span>
<span data-ttu-id="5475a-169">DPM ve daha önce açıklandığı gibi SharePoint grubu yapılandırdıktan sonra bu SharePoint DPM tarafından korunur.</span><span class="sxs-lookup"><span data-stu-id="5475a-169">After you have configured DPM and the SharePoint farm as explained previously, SharePoint can be protected by DPM.</span></span>

### <a name="to-protect-a-sharepoint-farm"></a><span data-ttu-id="5475a-170">Bir SharePoint grubunu korumak için</span><span class="sxs-lookup"><span data-stu-id="5475a-170">To protect a SharePoint farm</span></span>
1. <span data-ttu-id="5475a-171">Gelen **koruma** sekmesini tıklatın, DPM Yönetici Konsolu'nda **yeni**.</span><span class="sxs-lookup"><span data-stu-id="5475a-171">From the **Protection** tab of the DPM Administrator Console, click **New**.</span></span>
    <span data-ttu-id="5475a-172">![Yeni koruma sekmesi](./media/backup-azure-backup-sharepoint/dpm-new-protection-tab.png)</span><span class="sxs-lookup"><span data-stu-id="5475a-172">![New Protection Tab](./media/backup-azure-backup-sharepoint/dpm-new-protection-tab.png)</span></span>
2. <span data-ttu-id="5475a-173">Üzerinde **koruma grubu türünü seçin** sayfasında **yeni koruma grubu oluşturma** seçin **sunucuları**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="5475a-173">On the **Select Protection Group Type** page of the **Create New Protection Group** wizard, select **Servers**, and then click **Next**.</span></span>
   
    ![Koruma grubu seç türü](./media/backup-azure-backup-sharepoint/select-protection-group-type.png)
3. <span data-ttu-id="5475a-175">Üzerinde **grup üyelerini seçin** ekranında, önce korumak istediğiniz SharePoint server için onay kutusunu işaretleyin **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="5475a-175">On the **Select Group Members** screen, select the check box for the SharePoint server you want to protect and click **Next**.</span></span>
   
    ![Grup üyelerini seçin](./media/backup-azure-backup-sharepoint/select-group-members2.png)
   
   > [!NOTE]
   > <span data-ttu-id="5475a-177">DPM aracı yüklü olan sunucunun Sihirbazı'nda görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5475a-177">With the DPM agent installed, you can see the server in the wizard.</span></span> <span data-ttu-id="5475a-178">DPM, aynı zamanda yapısını gösterir.</span><span class="sxs-lookup"><span data-stu-id="5475a-178">DPM also shows its structure.</span></span> <span data-ttu-id="5475a-179">ConfigureSharePoint.exe çalıştırdığınız için DPM SharePoint VSS Yazıcı hizmeti ve karşılık gelen SQL Server veritabanlarını ile iletişim kurar ve SharePoint grup yapısı, ilişkili içerik veritabanları ve karşılık gelen tüm öğeleri tanır.</span><span class="sxs-lookup"><span data-stu-id="5475a-179">Because you ran ConfigureSharePoint.exe, DPM communicates with the SharePoint VSS Writer service and its corresponding SQL Server databases and recognizes the SharePoint farm structure, the associated content databases, and any corresponding items.</span></span>
   > 
   > 
4. <span data-ttu-id="5475a-180">Üzerinde **veri koruma yöntemini seçin** sayfasında, adını girin **koruma grubu**ve tercih ettiğiniz seçin *koruma yöntemleri*.</span><span class="sxs-lookup"><span data-stu-id="5475a-180">On the **Select Data Protection Method** page, enter the name of the **Protection Group**, and select your preferred *protection methods*.</span></span> <span data-ttu-id="5475a-181">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5475a-181">Click **Next**.</span></span>
   
    ![Veri koruma yöntemini seçin](./media/backup-azure-backup-sharepoint/select-data-protection-method1.png)
   
   > [!NOTE]
   > <span data-ttu-id="5475a-183">Disk koruması yöntemi kısa kurtarma zamanı hedeflerine yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="5475a-183">The disk protection method helps to meet short recovery-time objectives.</span></span> <span data-ttu-id="5475a-184">Azure için bantları karşılaştırıldığında ekonomik, uzun vadeli koruma hedefidir.</span><span class="sxs-lookup"><span data-stu-id="5475a-184">Azure is an economical, long-term protection target compared to tapes.</span></span> <span data-ttu-id="5475a-185">Daha fazla bilgi için bkz: [bant altyapınızın yerini alması için Azure Yedekleme'yi](https://azure.microsoft.com/documentation/articles/backup-azure-backup-cloud-as-tape/)</span><span class="sxs-lookup"><span data-stu-id="5475a-185">For more information, see [Use Azure Backup to replace your tape infrastructure](https://azure.microsoft.com/documentation/articles/backup-azure-backup-cloud-as-tape/)</span></span>
   > 
   > 
5. <span data-ttu-id="5475a-186">Üzerinde **kısa vadeli hedefleri belirtin** sayfasında, tercih ettiğiniz **bekletme aralığı** ve gerçekleşmesini istediğinizde belirleyin.</span><span class="sxs-lookup"><span data-stu-id="5475a-186">On the **Specify Short-Term Goals** page, select your preferred **Retention range** and identify when you want backups to occur.</span></span>
   
    ![Kısa vadeli hedefleri belirtin](./media/backup-azure-backup-sharepoint/specify-short-term-goals2.png)
   
   > [!NOTE]
   > <span data-ttu-id="5475a-188">Kurtarma genellikle beş günden eski olan verileri için gerekli olduğundan, biz diskteki beş günlük bir bekletme aralığı seçili ve yedekleme Bu örnek için üretim dışı saatlerde olur güvence altına.</span><span class="sxs-lookup"><span data-stu-id="5475a-188">Because recovery is most often required for data that's less than five days old, we selected a retention range of five days on disk and ensured that the backup happens during non-production hours, for this example.</span></span>
   > 
   > 
6. <span data-ttu-id="5475a-189">Depolama havuzuna disk alanı koruma grubu için ayrılmış ve ardından gözden geçirme **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="5475a-189">Review the storage pool disk space allocated for the protection group, and click then **Next**.</span></span>
7. <span data-ttu-id="5475a-190">Her koruma grubu için DPM depolamak ve çoğaltmaları yönetmek için disk alanı ayırır.</span><span class="sxs-lookup"><span data-stu-id="5475a-190">For every protection group, DPM allocates disk space to store and manage replicas.</span></span> <span data-ttu-id="5475a-191">Bu noktada, DPM seçili verilerin bir kopyasını oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5475a-191">At this point, DPM must create a copy of the selected data.</span></span> <span data-ttu-id="5475a-192">Nasıl ve ne zaman, oluşturulan çoğaltma istediğiniz'ı seçin ve **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="5475a-192">Select how and when you want the replica created, and then click **Next**.</span></span>
   
    ![Çoğaltma oluşturma yöntemini seçin](./media/backup-azure-backup-sharepoint/choose-replica-creation-method.png)
   
   > [!NOTE]
   > <span data-ttu-id="5475a-194">Ağ trafiği değil parametreden emin olmak için üretim saatleri dışında bir saat seçin.</span><span class="sxs-lookup"><span data-stu-id="5475a-194">To make sure that network traffic is not effected, select a time outside production hours.</span></span>
   > 
   > 
8. <span data-ttu-id="5475a-195">DPM, çoğaltma üzerinde tutarlılık denetimleri gerçekleştirerek veri bütünlüğü sağlar.</span><span class="sxs-lookup"><span data-stu-id="5475a-195">DPM ensures data integrity by performing consistency checks on the replica.</span></span> <span data-ttu-id="5475a-196">Kullanılabilir iki seçenek vardır.</span><span class="sxs-lookup"><span data-stu-id="5475a-196">There are two available options.</span></span> <span data-ttu-id="5475a-197">Tutarlılık denetimleri çalıştırmak için bir zamanlama tanımlayın veya tutarsız hale her DPM otomatik olarak çoğaltma üzerinde tutarlılık denetimleri çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5475a-197">You can define a schedule to run consistency checks, or DPM can run consistency checks automatically on the replica whenever it becomes inconsistent.</span></span> <span data-ttu-id="5475a-198">Tercih ettiğiniz seçeneği seçin ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="5475a-198">Select your preferred option, and then click **Next**.</span></span>
   
    ![Tutarlılık denetimi](./media/backup-azure-backup-sharepoint/consistency-check.png)
9. <span data-ttu-id="5475a-200">Üzerinde **çevrimiçi koruma verilerini belirtin** sayfasında, koruma ve ardından istediğiniz SharePoint grubu seçin **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="5475a-200">On the **Specify Online Protection Data** page, select the SharePoint farm that you want to protect, and then click **Next**.</span></span>
   
    ![DPM SharePoint Protection1](./media/backup-azure-backup-sharepoint/select-online-protection1.png)
10. <span data-ttu-id="5475a-202">Üzerinde **çevrimiçi yedekleme zamanlamasını belirtin** sayfasında, tercih ettiğiniz zamanlamayı seçin ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="5475a-202">On the **Specify Online Backup Schedule** page, select your preferred schedule, and then click **Next**.</span></span>
    
    ![Online_backup_schedule](./media/backup-azure-backup-sharepoint/specify-online-backup-schedule.png)
    
    > [!NOTE]
    > <span data-ttu-id="5475a-204">DPM en fazla iki günlük yedeklemeler için Azure farklı zamanlarda sağlar.</span><span class="sxs-lookup"><span data-stu-id="5475a-204">DPM provides a maximum of two daily backups to Azure at different times.</span></span> <span data-ttu-id="5475a-205">Azure yedekleme de en yüksek ve saatlere yedeklemelerin kullanarak kullanılabilir WAN bant genişliği miktarını kontrol [Azure yedekleme ağ azaltma](https://azure.microsoft.com/en-in/documentation/articles/backup-configure-vault/#enable-network-throttling).</span><span class="sxs-lookup"><span data-stu-id="5475a-205">Azure Backup can also control the amount of WAN bandwidth that can be used for backups in peak and off-peak hours by using [Azure Backup Network Throttling](https://azure.microsoft.com/en-in/documentation/articles/backup-configure-vault/#enable-network-throttling).</span></span>
    > 
    > 
11. <span data-ttu-id="5475a-206">Üzerinde seçili yedekleme zamanlaması bağlı olarak **çevrimiçi bekletme ilkesini belirtin** sayfasında, günlük, haftalık, aylık ve yıllık yedekleme noktası bekletme ilkesi seçin.</span><span class="sxs-lookup"><span data-stu-id="5475a-206">Depending on the backup schedule that you selected, on the **Specify Online Retention Policy** page, select the retention policy for daily, weekly, monthly, and yearly backup points.</span></span>
    
    ![Online_retention_policy](./media/backup-azure-backup-sharepoint/specify-online-retention.png)
    
    > [!NOTE]
    > <span data-ttu-id="5475a-208">DPM, farklı yedekleme noktaları için farklı bir bekletme ilkesi seçilebilir bir üst öğe son bekletme düzeni kullanır.</span><span class="sxs-lookup"><span data-stu-id="5475a-208">DPM uses a grandfather-father-son retention scheme in which a different retention policy can be chosen for different backup points.</span></span>
    > 
    > 
12. <span data-ttu-id="5475a-209">Disk benzeyen, bir ilk başvuru noktası çoğaltmasını Azure içinde oluşturulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="5475a-209">Similar to disk, an initial reference point replica needs to be created in Azure.</span></span> <span data-ttu-id="5475a-210">Azure bir ilk yedek kopyasını oluşturun ve ardından tercih ettiğiniz seçeneği seçin **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="5475a-210">Select your preferred option to create an initial backup copy to Azure, and then click **Next**.</span></span>
    
    ![Online_replica](./media/backup-azure-backup-sharepoint/online-replication.png)
13. <span data-ttu-id="5475a-212">Seçtiğiniz ayarları gözden **Özet** sayfasında ve ardından **Grup Oluştur**.</span><span class="sxs-lookup"><span data-stu-id="5475a-212">Review your selected settings on the **Summary** page, and then click **Create Group**.</span></span> <span data-ttu-id="5475a-213">Koruma grubu oluşturulduktan sonra bir başarı iletisi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="5475a-213">You will see a success message after the protection group has been created.</span></span>
    
    ![Özet](./media/backup-azure-backup-sharepoint/summary.png)

## <a name="restore-a-sharepoint-item-from-disk-by-using-dpm"></a><span data-ttu-id="5475a-215">DPM kullanarak bir SharePoint öğesi diskten geri yükleme</span><span class="sxs-lookup"><span data-stu-id="5475a-215">Restore a SharePoint item from disk by using DPM</span></span>
<span data-ttu-id="5475a-216">Aşağıdaki örnekte, *SharePoint kurtarma öğesi* yanlışlıkla silinmişse ve geri yüklenmesi gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="5475a-216">In the following example, the *Recovering SharePoint item* has been accidentally deleted and needs to be recovered.</span></span>
<span data-ttu-id="5475a-217">![DPM SharePoint Protection4](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection5.png)</span><span class="sxs-lookup"><span data-stu-id="5475a-217">![DPM SharePoint Protection4](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection5.png)</span></span>

1. <span data-ttu-id="5475a-218">Açık **DPM Yönetici Konsolu**.</span><span class="sxs-lookup"><span data-stu-id="5475a-218">Open the **DPM Administrator Console**.</span></span> <span data-ttu-id="5475a-219">DPM tarafından korunan tüm SharePoint grupları gösterilen **koruma** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="5475a-219">All SharePoint farms that are protected by DPM are shown in the **Protection** tab.</span></span>
   
    ![DPM SharePoint Protection3](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection4.png)
2. <span data-ttu-id="5475a-221">Öğeyi kurtarmak başlamak için seçin **kurtarma** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="5475a-221">To begin to recover the item, select the **Recovery** tab.</span></span>
   
    ![DPM SharePoint Protection5](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection6.png)
3. <span data-ttu-id="5475a-223">SharePoint için arama yapabilirsiniz *SharePoint kurtarma öğesi* kurtarma içinde bir joker karakter tabanlı arama kullanarak aralığı gösterin.</span><span class="sxs-lookup"><span data-stu-id="5475a-223">You can search SharePoint for *Recovering SharePoint item* by using a wildcard-based search within a recovery point range.</span></span>
   
    ![DPM SharePoint Protection6](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection7.png)
4. <span data-ttu-id="5475a-225">Arama sonuçlarından uygun Kurtarma noktasını seçin, öğeyi sağ tıklatın ve ardından **kurtarmak**.</span><span class="sxs-lookup"><span data-stu-id="5475a-225">Select the appropriate recovery point from the search results, right-click the item, and then select **Recover**.</span></span>
5. <span data-ttu-id="5475a-226">Ayrıca, çeşitli kurtarma noktalarına göz ve bir veritabanı veya kurtarmak için öğeyi seçin.</span><span class="sxs-lookup"><span data-stu-id="5475a-226">You can also browse through various recovery points and select a database or item to recover.</span></span> <span data-ttu-id="5475a-227">Seçin **tarihi > kurtarma süresini**ve ardından doğru seçin **veritabanı > SharePoint grubu > kurtarma noktası > öğesi**.</span><span class="sxs-lookup"><span data-stu-id="5475a-227">Select **Date > Recovery time**, and then select the correct **Database > SharePoint farm > Recovery point > Item**.</span></span>
   
    ![DPM SharePoint Protection7](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection8.png)
6. <span data-ttu-id="5475a-229">Öğeyi sağ tıklatın ve ardından **kurtarmak** açmak için **Kurtarma Sihirbazı'nı**.</span><span class="sxs-lookup"><span data-stu-id="5475a-229">Right-click the item, and then select **Recover** to open the **Recovery Wizard**.</span></span> <span data-ttu-id="5475a-230">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5475a-230">Click **Next**.</span></span>
   
    ![Kurtarma seçimini inceleyin](./media/backup-azure-backup-sharepoint/review-recovery-selection.png)
7. <span data-ttu-id="5475a-232">Gerçekleştirin ve ardından istediğiniz kurtarma türünü seçin **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="5475a-232">Select the type of recovery that you want to perform, and then click **Next**.</span></span>
   
    ![Kurtarma türü](./media/backup-azure-backup-sharepoint/select-recovery-type.png)
   
   > [!NOTE]
   > <span data-ttu-id="5475a-234">Seçimi **özgün kurtarmak** örnekte özgün SharePoint sitesi öğesine kurtarır.</span><span class="sxs-lookup"><span data-stu-id="5475a-234">The selection of **Recover to original** in the example recovers the item to the original SharePoint site.</span></span>
   > 
   > 
8. <span data-ttu-id="5475a-235">Seçin **kurtarma işlemi** kullanmak istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="5475a-235">Select the **Recovery Process** that you want to use.</span></span>
   
   * <span data-ttu-id="5475a-236">Seçin **kurtarma grubu kullanmadan kurtarmak** SharePoint grubu değişmedi ve geri yükleniyor kurtarma noktası ile aynıdır.</span><span class="sxs-lookup"><span data-stu-id="5475a-236">Select **Recover without using a recovery farm** if the SharePoint farm has not changed and is the same as the recovery point that is being restored.</span></span>
   * <span data-ttu-id="5475a-237">Seçin **kurtarma grubu kullanarak kurtarma** kurtarma noktası oluşturulduktan sonra SharePoint grubu değiştirilmesi durumunda.</span><span class="sxs-lookup"><span data-stu-id="5475a-237">Select **Recover using a recovery farm** if the SharePoint farm has changed since the recovery point was created.</span></span>
     
     ![Kurtarma işlemi](./media/backup-azure-backup-sharepoint/recovery-process.png)
9. <span data-ttu-id="5475a-239">Veritabanı geçici olarak kurtarmak için hazırlama bir SQL Server örneğinin konumu sağlayın ve DPM sunucusu ve öğeyi kurtarmak için SharePoint çalıştıran sunucu hazırlama bir dosya paylaşımı sağlayın.</span><span class="sxs-lookup"><span data-stu-id="5475a-239">Provide a staging SQL Server instance location to recover the database temporarily, and provide a staging file share on the DPM server and the server that's running SharePoint to recover the item.</span></span>
   
    ![Hazırlama Location1](./media/backup-azure-backup-sharepoint/staging-location1.png)
   
    <span data-ttu-id="5475a-241">DPM geçici SQL Server örneği için SharePoint öğe barındırma içerik veritabanını ekler.</span><span class="sxs-lookup"><span data-stu-id="5475a-241">DPM attaches the content database that is hosting the SharePoint item to the temporary SQL Server instance.</span></span> <span data-ttu-id="5475a-242">İçerik veritabanından DPM sunucusu öğesi kurtarır ve DPM sunucusundaki hazırlama dosya konumuna yerleştirir.</span><span class="sxs-lookup"><span data-stu-id="5475a-242">From the content database, the DPM server recovers the item and puts it on the staging file location on the DPM server.</span></span> <span data-ttu-id="5475a-243">DPM sunucusunun hazırlama konumuna sunulmuştur Kurtarılan bir öğeye SharePoint grubu üzerinde hazırlama konumu için aktarılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="5475a-243">The recovered item that's on the staging location of the DPM server now needs to be exported to the staging location on the SharePoint farm.</span></span>
   
    ![Hazırlama Location2](./media/backup-azure-backup-sharepoint/staging-location2.png)
10. <span data-ttu-id="5475a-245">Seçin **kurtarma seçeneklerini belirtin**, SharePoint grubu için güvenlik ayarlarını Uygula ve kurtarma noktası güvenlik ayarlarını uygula.</span><span class="sxs-lookup"><span data-stu-id="5475a-245">Select **Specify recovery options**, and apply security settings to the SharePoint farm or apply the security settings of the recovery point.</span></span> <span data-ttu-id="5475a-246">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5475a-246">Click **Next**.</span></span>
    
    ![Kurtarma Seçenekleri](./media/backup-azure-backup-sharepoint/recovery-options.png)
    
    > [!NOTE]
    > <span data-ttu-id="5475a-248">Ağ bant genişliği kullanımını azaltma seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5475a-248">You can choose to throttle the network bandwidth usage.</span></span> <span data-ttu-id="5475a-249">Bu, üretim saatleri içinde üretim sunucusu üzerinde etkisi azaltır.</span><span class="sxs-lookup"><span data-stu-id="5475a-249">This minimizes impact to the production server during production hours.</span></span>
    > 
    > 
11. <span data-ttu-id="5475a-250">Özet bilgilerini inceleyin ve ardından **kurtarmak** dosyasının kurtarmayı başlatmak için.</span><span class="sxs-lookup"><span data-stu-id="5475a-250">Review the summary information, and then click **Recover** to begin recovery of the file.</span></span>
    
    ![Kurtarma özeti](./media/backup-azure-backup-sharepoint/recovery-summary.png)
12. <span data-ttu-id="5475a-252">Şimdi seçin **izleme** sekmesinde **DPM Yönetici Konsolu'nu** görüntülemek için **durum** kurtarma.</span><span class="sxs-lookup"><span data-stu-id="5475a-252">Now select the **Monitoring** tab in the **DPM Administrator Console** to view the **Status** of the recovery.</span></span>
    
    ![Kurtarma durumu](./media/backup-azure-backup-sharepoint/recovery-monitoring.png)
    
    > [!NOTE]
    > <span data-ttu-id="5475a-254">Dosya artık geri yüklenir.</span><span class="sxs-lookup"><span data-stu-id="5475a-254">The file is now restored.</span></span> <span data-ttu-id="5475a-255">Geri yüklenen dosya denetlemek için SharePoint sitesi yenileyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5475a-255">You can refresh the SharePoint site to check the restored file.</span></span>
    > 
    > 

## <a name="restore-a-sharepoint-database-from-azure-by-using-dpm"></a><span data-ttu-id="5475a-256">DPM kullanarak bir SharePoint veritabanı Azure'dan geri yükleme</span><span class="sxs-lookup"><span data-stu-id="5475a-256">Restore a SharePoint database from Azure by using DPM</span></span>
1. <span data-ttu-id="5475a-257">Bir SharePoint içerik veritabanını kurtarmak için (daha önce gösterildiği gibi) çeşitli kurtarma noktalarına göz ve geri yüklemek istediğiniz kurtarma noktasını seçin.</span><span class="sxs-lookup"><span data-stu-id="5475a-257">To recover a SharePoint content database, browse through various recovery points (as shown previously), and select the recovery point that you want to restore.</span></span>
   
    ![DPM SharePoint Protection8](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection9.png)
2. <span data-ttu-id="5475a-259">SharePoint kurtarma noktası kullanılabilir SharePoint katalog bilgileri görüntülemek için çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5475a-259">Double-click the SharePoint recovery point to show the available SharePoint catalog information.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="5475a-260">SharePoint grubu Azure uzun vadeli bekletme için korumalı olduğundan, hiçbir Kataloğu bilgi (meta veriler) DPM sunucusunda kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="5475a-260">Because the SharePoint farm is protected for long-term retention in Azure, no catalog information (metadata) is available on the DPM server.</span></span> <span data-ttu-id="5475a-261">Sonuç olarak, bir zaman içinde nokta SharePoint içerik veritabanı kurtarılması gereken her SharePoint grubu yeniden katalog gerekir.</span><span class="sxs-lookup"><span data-stu-id="5475a-261">As a result, whenever a point-in-time SharePoint content database needs to be recovered, you need to catalog the SharePoint farm again.</span></span>
   > 
   > 
3. <span data-ttu-id="5475a-262">Tıklatın **yeniden kataloglama**.</span><span class="sxs-lookup"><span data-stu-id="5475a-262">Click **Re-catalog**.</span></span>
   
    ![DPM SharePoint Protection10](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection12.png)
   
    <span data-ttu-id="5475a-264">**Bulut yeniden katalogla** durum penceresi açar.</span><span class="sxs-lookup"><span data-stu-id="5475a-264">The **Cloud Recatalog** status window opens.</span></span>
   
    ![DPM SharePoint Protection11](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection13.png)
   
    <span data-ttu-id="5475a-266">Katalog tamamlandıktan sonra durum değişikliklerini *başarı*.</span><span class="sxs-lookup"><span data-stu-id="5475a-266">After cataloging is finished, the status changes to *Success*.</span></span> <span data-ttu-id="5475a-267">**Kapat**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5475a-267">Click **Close**.</span></span>
   
    ![DPM SharePoint Protection12](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection14.png)
4. <span data-ttu-id="5475a-269">DPM gösterilen SharePoint nesnesine tıklayın **kurtarma** içerik veritabanı yapısı almak için sekmesini.</span><span class="sxs-lookup"><span data-stu-id="5475a-269">Click the SharePoint object shown in the DPM **Recovery** tab to get the content database structure.</span></span> <span data-ttu-id="5475a-270">Öğeyi sağ tıklatın ve ardından **kurtarmak**.</span><span class="sxs-lookup"><span data-stu-id="5475a-270">Right-click the item, and then click **Recover**.</span></span>
   
    ![DPM SharePoint Protection13](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection15.png)
5. <span data-ttu-id="5475a-272">Bu noktada, izleyin [kurtarma adımları bu makalenin önceki bölümlerinde](#restore-a-sharepoint-item-from-disk-using-dpm) diskten bir SharePoint içerik veritabanını kurtarmak için.</span><span class="sxs-lookup"><span data-stu-id="5475a-272">At this point, follow the [recovery steps earlier in this article](#restore-a-sharepoint-item-from-disk-using-dpm) to recover a SharePoint content database from disk.</span></span>

## <a name="faqs"></a><span data-ttu-id="5475a-273">SSS</span><span class="sxs-lookup"><span data-stu-id="5475a-273">FAQs</span></span>
<span data-ttu-id="5475a-274">S: hangi sürümlerinin DPM, SQL Server 2014 ve SQL 2012 (SP2) destekliyor?</span><span class="sxs-lookup"><span data-stu-id="5475a-274">Q: Which versions of DPM support SQL Server 2014 and SQL 2012 (SP2)?</span></span><br>
<span data-ttu-id="5475a-275">Y: DPM 2012 R2 güncelleştirme paketi 4 ile hem de destekler.</span><span class="sxs-lookup"><span data-stu-id="5475a-275">A: DPM 2012 R2 with Update Rollup 4 supports both.</span></span>

<span data-ttu-id="5475a-276">S: özgün konuma SharePoint öğesi, SharePoint SQL AlwaysOn (disk koruması) kullanılarak yapılandırılmışsa kurtarma?</span><span class="sxs-lookup"><span data-stu-id="5475a-276">Q: Can I recover a SharePoint item to the original location if SharePoint is configured by using SQL AlwaysOn (with protection on disk)?</span></span><br>
<span data-ttu-id="5475a-277">A: Evet öğenin özgün SharePoint sitesine kurtarılabilir.</span><span class="sxs-lookup"><span data-stu-id="5475a-277">A: Yes, the item can be recovered to the original SharePoint site.</span></span>

<span data-ttu-id="5475a-278">S: bir SharePoint veritabanını özgün konumuna, SharePoint SQL AlwaysOn kullanarak yapılandırılmışsa kurtarma?</span><span class="sxs-lookup"><span data-stu-id="5475a-278">Q: Can I recover a SharePoint database to the original location if SharePoint is configured by using SQL AlwaysOn?</span></span><br>
<span data-ttu-id="5475a-279">A: SharePoint veritabanlarını SQL AlwaysOn yapılandırıldığından, kullanılabilirlik grubu kaldırılmadığı sürece bunlar değiştirilemez.</span><span class="sxs-lookup"><span data-stu-id="5475a-279">A: Because SharePoint databases are configured in SQL AlwaysOn, they cannot be modified unless the availability group is removed.</span></span> <span data-ttu-id="5475a-280">Sonuç olarak, DPM bir veritabanını özgün konumuna geri yükleyemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="5475a-280">As a result, DPM cannot restore a database to the original location.</span></span> <span data-ttu-id="5475a-281">SQL Server veritabanını başka bir SQL Server örneğine kurtarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5475a-281">You can recover a SQL Server database to another SQL Server instance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5475a-282">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5475a-282">Next steps</span></span>
* <span data-ttu-id="5475a-283">DPM SharePoint koruması hakkında daha fazla bilgi - bkz [Video serisi - SharePoint DPM koruma](http://channel9.msdn.com/Series/Azure-Backup/Microsoft-SCDPM-Protection-of-SharePoint-1-of-2-How-to-create-a-SharePoint-Protection-Group)</span><span class="sxs-lookup"><span data-stu-id="5475a-283">Learn more about DPM Protection of SharePoint - see [Video Series - DPM Protection of SharePoint](http://channel9.msdn.com/Series/Azure-Backup/Microsoft-SCDPM-Protection-of-SharePoint-1-of-2-How-to-create-a-SharePoint-Protection-Group)</span></span>
* <span data-ttu-id="5475a-284">Gözden geçirme [System Center 2012 - Data Protection Manager için sürüm notları](https://technet.microsoft.com/library/jj860415.aspx)</span><span class="sxs-lookup"><span data-stu-id="5475a-284">Review [Release Notes for System Center 2012 - Data Protection Manager](https://technet.microsoft.com/library/jj860415.aspx)</span></span>
* <span data-ttu-id="5475a-285">Gözden geçirme [System Center 2012 SP1 Data Protection Manager için sürüm notları](https://technet.microsoft.com/library/jj860394.aspx)</span><span class="sxs-lookup"><span data-stu-id="5475a-285">Review [Release Notes for Data Protection Manager in System Center 2012 SP1](https://technet.microsoft.com/library/jj860394.aspx)</span></span>

