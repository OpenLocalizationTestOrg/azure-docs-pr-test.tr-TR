---
title: "bir SharePoint grubu tooAzure yukarı aaaUse Azure yedekleme sunucusu tooback | Microsoft Docs"
description: "Azure yedekleme sunucusu tooback kullanır ve SharePoint verilerinizi geri yükleyin. Bu makalede, SharePoint grubu hello bilgi tooconfigure sunar, böylece istenen verileri Azure'da saklanabilir. Korumalı SharePoint verileri diskten veya Azure geri yükleyebilirsiniz."
services: backup
documentationcenter: 
author: pvrk
manager: shivamg
editor: 
ms.assetid: 34ba87a4-91f1-4054-a4a1-272af1e15496
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: pullabhk
ms.openlocfilehash: 350c1ac0f3518f400062f3b586bbe9710a79915a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-a-sharepoint-farm-tooazure"></a><span data-ttu-id="09a60-105">Bir SharePoint grubu tooAzure yedekleyin</span><span class="sxs-lookup"><span data-stu-id="09a60-105">Back up a SharePoint farm tooAzure</span></span>
<span data-ttu-id="09a60-106">Bir SharePoint yedekleme tooMicrosoft Azure kadar hello Microsoft Azure yedekleme sunucusu (MABS) kullanarak grubunuz diğer veri kaynaklarını geri aynı şekilde.</span><span class="sxs-lookup"><span data-stu-id="09a60-106">You back up a SharePoint farm tooMicrosoft Azure by using Microsoft Azure Backup Server (MABS) in much hello same way that you back up other data sources.</span></span> <span data-ttu-id="09a60-107">Azure yedekleme, günlük, haftalık, aylık veya yıllık yedekleme noktaları hello yedekleme zamanlaması toocreate esneklik sağlar ve çeşitli yedekleme noktaları için bekletme ilkesi seçenekler sunar.</span><span class="sxs-lookup"><span data-stu-id="09a60-107">Azure Backup provides flexibility in hello backup schedule toocreate daily, weekly, monthly, or yearly backup points and gives you retention policy options for various backup points.</span></span> <span data-ttu-id="09a60-108">Hızlı Kurtarma süresi hedefi (RTO) için de hello yetenek toostore yerel disk kopyaları sağlar ve toostore tooAzure ekonomik, uzun vadeli bekletme için kopyalar.</span><span class="sxs-lookup"><span data-stu-id="09a60-108">It also provides hello capability toostore local disk copies for quick recovery-time objectives (RTO) and toostore copies tooAzure for economical, long-term retention.</span></span>

## <a name="sharepoint-supported-versions-and-related-protection-scenarios"></a><span data-ttu-id="09a60-109">SharePoint desteklenen sürümleri ve ilgili koruma senaryoları</span><span class="sxs-lookup"><span data-stu-id="09a60-109">SharePoint supported versions and related protection scenarios</span></span>
<span data-ttu-id="09a60-110">Azure yedekleme DPM için hello aşağıdaki senaryoları destekler:</span><span class="sxs-lookup"><span data-stu-id="09a60-110">Azure Backup for DPM supports hello following scenarios:</span></span>

| <span data-ttu-id="09a60-111">İş yükü</span><span class="sxs-lookup"><span data-stu-id="09a60-111">Workload</span></span> | <span data-ttu-id="09a60-112">Sürüm</span><span class="sxs-lookup"><span data-stu-id="09a60-112">Version</span></span> | <span data-ttu-id="09a60-113">SharePoint dağıtımı</span><span class="sxs-lookup"><span data-stu-id="09a60-113">SharePoint deployment</span></span> | <span data-ttu-id="09a60-114">Koruma ve kurtarma</span><span class="sxs-lookup"><span data-stu-id="09a60-114">Protection and recovery</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="09a60-115">SharePoint</span><span class="sxs-lookup"><span data-stu-id="09a60-115">SharePoint</span></span> |<span data-ttu-id="09a60-116">SharePoint 2013, SharePoint 2010, SharePoint 2007'de, SharePoint 3.0</span><span class="sxs-lookup"><span data-stu-id="09a60-116">SharePoint 2013, SharePoint 2010, SharePoint 2007, SharePoint 3.0</span></span> |<span data-ttu-id="09a60-117">Bir fiziksel sunucu veya Hyper-V/VMware sanal makinesi dağıtılan SharePoint</span><span class="sxs-lookup"><span data-stu-id="09a60-117">SharePoint deployed as a physical server or Hyper-V/VMware virtual machine</span></span> <br> -------------- <br> <span data-ttu-id="09a60-118">SQL AlwaysOn</span><span class="sxs-lookup"><span data-stu-id="09a60-118">SQL AlwaysOn</span></span> | <span data-ttu-id="09a60-119">SharePoint grubu kurtarma seçeneklerini koruma: Kurtarma grubu, veritabanı ve disk kurtarma noktalarından dosya veya liste öğesi.</span><span class="sxs-lookup"><span data-stu-id="09a60-119">Protect SharePoint Farm recovery options: Recovery farm, database, and file or list item from disk recovery points.</span></span>  <span data-ttu-id="09a60-120">Azure kurtarma noktalarından grubu ve veritabanı kurtarma.</span><span class="sxs-lookup"><span data-stu-id="09a60-120">Farm and database recovery from Azure recovery points.</span></span> |

## <a name="before-you-start"></a><span data-ttu-id="09a60-121">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="09a60-121">Before you start</span></span>
<span data-ttu-id="09a60-122">Bir SharePoint grubu tooAzure yedeklenmeden önce tooconfirm gereken birkaç nokta vardır.</span><span class="sxs-lookup"><span data-stu-id="09a60-122">There are a few things you need tooconfirm before you back up a SharePoint farm tooAzure.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="09a60-123">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="09a60-123">Prerequisites</span></span>
<span data-ttu-id="09a60-124">Devam etmeden önce bilgisayarınızda yüklü olduğundan emin olun [yüklü ve hello Azure yedekleme sunucusu hazırlanan](backup-azure-microsoft-azure-backup.md) tooprotect iş yükleri.</span><span class="sxs-lookup"><span data-stu-id="09a60-124">Before you proceed, make sure that you have [installed and prepared hello Azure Backup Server](backup-azure-microsoft-azure-backup.md) tooprotect workloads.</span></span>

### <a name="protection-agent"></a><span data-ttu-id="09a60-125">Koruma Aracısı</span><span class="sxs-lookup"><span data-stu-id="09a60-125">Protection agent</span></span>
<span data-ttu-id="09a60-126">Merhaba koruma Aracısı, SharePoint, SQL Server çalıştıran hello sunucuları ve hello SharePoint grubunun parçası olan diğer tüm sunucuları çalıştıran hello sunucuda yüklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="09a60-126">hello Protection agent must be installed on hello server that's running SharePoint, hello servers that are running SQL Server, and all other servers that are part of hello SharePoint farm.</span></span> <span data-ttu-id="09a60-127">Hakkında daha fazla bilgi için tooset hello koruma aracısını kurma bkz [Kurulum koruma Aracısı](https://technet.microsoft.com/library/hh758034\(v=sc.12\).aspx).</span><span class="sxs-lookup"><span data-stu-id="09a60-127">For more information about how tooset up hello protection agent, see [Setup Protection Agent](https://technet.microsoft.com/library/hh758034\(v=sc.12\).aspx).</span></span>  <span data-ttu-id="09a60-128">Merhaba hello aracı yalnızca bir tek web front end (WFE) sunucusuna yükleyin işlemdir.</span><span class="sxs-lookup"><span data-stu-id="09a60-128">hello one exception is that you install hello agent only on a single web front end (WFE) server.</span></span> <span data-ttu-id="09a60-129">DPM, koruma için hello giriş noktası olarak bir WFE sunucusu yalnızca tooserve hello aracısında gerekir.</span><span class="sxs-lookup"><span data-stu-id="09a60-129">DPM needs hello agent on one WFE server only tooserve as hello entry point for protection.</span></span>

### <a name="sharepoint-farm"></a><span data-ttu-id="09a60-130">SharePoint grubu</span><span class="sxs-lookup"><span data-stu-id="09a60-130">SharePoint farm</span></span>
<span data-ttu-id="09a60-131">Merhaba gruptaki her 10 milyon öğe için en az 2 GB hello biriminde hello MABS klasörünün bulunduğu alan olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="09a60-131">For every 10 million items in hello farm, there must be at least 2 GB of space on hello volume where hello MABS folder is located.</span></span> <span data-ttu-id="09a60-132">Bu alanı katalog oluşturma için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="09a60-132">This space is required for catalog generation.</span></span> <span data-ttu-id="09a60-133">MABS toorecover belirli öğeleri (site koleksiyonları, siteler, listeler, belge kitaplıkları, klasörler, tek tek belgeler ve liste öğeleri), katalog oluşturma her içerik veritabanında bulunan hello URL'lerin bir listesini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="09a60-133">For MABS toorecover specific items (site collections, sites, lists, document libraries, folders, individual documents, and list items), catalog generation creates a list of hello URLs that are contained within each content database.</span></span> <span data-ttu-id="09a60-134">Merhaba hello kurtarılabilir öğe bölmesinde hello URL'lerin listesini görüntüleyebilirsiniz **kurtarma** MABS Yönetici Konsolu'nun alanı görev.</span><span class="sxs-lookup"><span data-stu-id="09a60-134">You can view hello list of URLs in hello recoverable item pane in hello **Recovery** task area of MABS Administrator Console.</span></span>

### <a name="sql-server"></a><span data-ttu-id="09a60-135">SQL Server</span><span class="sxs-lookup"><span data-stu-id="09a60-135">SQL Server</span></span>
<span data-ttu-id="09a60-136">MABS LocalSystem hesabı olarak çalışır.</span><span class="sxs-lookup"><span data-stu-id="09a60-136">MABS runs as a LocalSystem account.</span></span> <span data-ttu-id="09a60-137">tooback SQL Server veritabanlarını MABS SQL Server çalıştıran hello sunucu için bu hesabı üzerinde sysadmin ayrıcalıkları gerekir.</span><span class="sxs-lookup"><span data-stu-id="09a60-137">tooback up SQL Server databases, MABS needs sysadmin privileges on that account for hello server that's running SQL Server.</span></span> <span data-ttu-id="09a60-138">NT AUTHORITY\SYSTEM çok ayarlamak*sysadmin* önce SQL Server çalıştıran hello sunucuda yedekleyin.</span><span class="sxs-lookup"><span data-stu-id="09a60-138">Set NT AUTHORITY\SYSTEM too*sysadmin* on hello server that's running SQL Server before you back it up.</span></span>

<span data-ttu-id="09a60-139">Hello SharePoint grubu SQL Server diğer adlarıyla yapılandırılmış SQL Server veritabanları varsa, hello SQL Server istemci bileşenlerini MABS koruyacak hello ön uç Web sunucusuna yükleyin.</span><span class="sxs-lookup"><span data-stu-id="09a60-139">If hello SharePoint farm has SQL Server databases that are configured with SQL Server aliases, install hello SQL Server client components on hello front-end Web server that MABS will protect.</span></span>

### <a name="sharepoint-server"></a><span data-ttu-id="09a60-140">SharePoint Server</span><span class="sxs-lookup"><span data-stu-id="09a60-140">SharePoint Server</span></span>
<span data-ttu-id="09a60-141">Performans SharePoint grubu boyutu gibi birçok faktöre bağlıdır, ancak genel bir yönerge olarak 25 TB SharePoint grubunu bir MABS koruyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="09a60-141">While performance depends on many factors such as size of SharePoint farm, as general guidance one MABS can protect a 25 TB SharePoint farm.</span></span>

### <a name="whats-not-supported"></a><span data-ttu-id="09a60-142">Desteklenmeyen durumlar</span><span class="sxs-lookup"><span data-stu-id="09a60-142">What's not supported</span></span>
* <span data-ttu-id="09a60-143">Bir SharePoint grubu korur MABS, arama dizinlerini veya uygulama hizmeti veritabanlarını koruma sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="09a60-143">MABS that protects a SharePoint farm does not protect search indexes or application service databases.</span></span> <span data-ttu-id="09a60-144">Bu veritabanlarının tooconfigure hello koruma ayrı olarak gerekir.</span><span class="sxs-lookup"><span data-stu-id="09a60-144">You will need tooconfigure hello protection of these databases separately.</span></span>
* <span data-ttu-id="09a60-145">MABS, genişleme dosya sunucusu (SOFS) paylaşımları üzerinde barındırılan SharePoint SQL Server veritabanlarını yedekleme sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="09a60-145">MABS does not provide backup of SharePoint SQL Server databases that are hosted on scale-out file server (SOFS) shares.</span></span>

## <a name="configure-sharepoint-protection"></a><span data-ttu-id="09a60-146">SharePoint korumasını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="09a60-146">Configure SharePoint protection</span></span>
<span data-ttu-id="09a60-147">MABS tooprotect SharePoint kullanmadan önce kullanarak hello SharePoint VSS yazıcısı hizmetini (WSS yazıcısı hizmeti) yapılandırmanız gerekir **ConfigureSharePoint.exe**.</span><span class="sxs-lookup"><span data-stu-id="09a60-147">Before you can use MABS tooprotect SharePoint, you must configure hello SharePoint VSS Writer service (WSS Writer service) by using **ConfigureSharePoint.exe**.</span></span>

<span data-ttu-id="09a60-148">Bulabileceğiniz **ConfigureSharePoint.exe** hello [MABS yükleme yolu] \bin klasöründe hello ön uç web sunucusunda.</span><span class="sxs-lookup"><span data-stu-id="09a60-148">You can find **ConfigureSharePoint.exe** in hello [MABS Installation Path]\bin folder on hello front-end web server.</span></span> <span data-ttu-id="09a60-149">Bu araç hello koruma Aracısı hello kimlik bilgileriyle hello SharePoint grubu için sağlar.</span><span class="sxs-lookup"><span data-stu-id="09a60-149">This tool provides hello protection agent with hello credentials for hello SharePoint farm.</span></span> <span data-ttu-id="09a60-150">Bu tek bir WFE sunucusunda çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="09a60-150">You run it on a single WFE server.</span></span> <span data-ttu-id="09a60-151">Birden çok WFE sunucunuz varsa, bir koruma grubu yapılandırırken yalnızca bir tanesini seçin.</span><span class="sxs-lookup"><span data-stu-id="09a60-151">If you have multiple WFE servers, select just one when you configure a protection group.</span></span>

### <a name="tooconfigure-hello-sharepoint-vss-writer-service"></a><span data-ttu-id="09a60-152">tooconfigure hello SharePoint VSS Yazıcı hizmeti</span><span class="sxs-lookup"><span data-stu-id="09a60-152">tooconfigure hello SharePoint VSS Writer service</span></span>
1. <span data-ttu-id="09a60-153">Bir komut isteminde hello WFE sunucusunda çok Git [MABS yükleme konumu] \bin\\</span><span class="sxs-lookup"><span data-stu-id="09a60-153">On hello WFE server, at a command prompt, go too[MABS installation location]\bin\\</span></span>
2. <span data-ttu-id="09a60-154">ConfigureSharePoint - EnableSharePointProtection girin.</span><span class="sxs-lookup"><span data-stu-id="09a60-154">Enter ConfigureSharePoint -EnableSharePointProtection.</span></span>
3. <span data-ttu-id="09a60-155">Merhaba grubu yönetici kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="09a60-155">Enter hello farm administrator credentials.</span></span> <span data-ttu-id="09a60-156">Bu hesap hello WFE sunucusunda hello yerel yönetici grubunun bir üyesi olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="09a60-156">This account should be a member of hello local Administrator group on hello WFE server.</span></span> <span data-ttu-id="09a60-157">Merhaba Çiftlik Yöneticisi aşağıdaki izinleri hello WFE sunucusunda yerel yönetici grant hello değilse:</span><span class="sxs-lookup"><span data-stu-id="09a60-157">If hello farm administrator isn’t a local admin grant hello following permissions on hello WFE server:</span></span>
   * <span data-ttu-id="09a60-158">Merhaba WSS_Admin_WPG grubu tam denetim toohello DPM klasörünü (% Program Files%\Microsoft Azure Backup\DPM) verin.</span><span class="sxs-lookup"><span data-stu-id="09a60-158">Grant hello WSS_Admin_WPG group full control toohello DPM folder (%Program Files%\Microsoft Azure Backup\DPM).</span></span>
   * <span data-ttu-id="09a60-159">GRANT hello WSS_Admin_WPG grubu okuma erişimini toohello DPM kayıt defteri anahtarı (HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager).</span><span class="sxs-lookup"><span data-stu-id="09a60-159">Grant hello WSS_Admin_WPG group read access toohello DPM Registry key (HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager).</span></span>

> [!NOTE]
> <span data-ttu-id="09a60-160">Merhaba SharePoint grubu yönetici kimlik bilgilerinde bir değişiklik olduğunda toorerun ConfigureSharePoint.exe gerekir.</span><span class="sxs-lookup"><span data-stu-id="09a60-160">You’ll need toorerun ConfigureSharePoint.exe whenever there’s a change in hello SharePoint farm administrator credentials.</span></span>
>
>

## <a name="back-up-a-sharepoint-farm-by-using-mabs"></a><span data-ttu-id="09a60-161">SharePoint grubunun kurulumu MABS kullanarak yedekleyin</span><span class="sxs-lookup"><span data-stu-id="09a60-161">Back up a SharePoint farm by using MABS</span></span>
<span data-ttu-id="09a60-162">MABS ve hello daha önce açıklandığı gibi SharePoint grubu yapılandırdıktan sonra bu SharePoint MABS tarafından korunur.</span><span class="sxs-lookup"><span data-stu-id="09a60-162">After you have configured MABS and hello SharePoint farm as explained previously, SharePoint can be protected by MABS.</span></span>

### <a name="tooprotect-a-sharepoint-farm"></a><span data-ttu-id="09a60-163">tooprotect bir SharePoint grubu</span><span class="sxs-lookup"><span data-stu-id="09a60-163">tooprotect a SharePoint farm</span></span>
1. <span data-ttu-id="09a60-164">Merhaba gelen **koruma** hello MABS Yönetici Konsolu sekmesini **yeni**.</span><span class="sxs-lookup"><span data-stu-id="09a60-164">From hello **Protection** tab of hello MABS Administrator Console, click **New**.</span></span>
    <span data-ttu-id="09a60-165">![Yeni koruma sekmesi](./media/backup-azure-backup-sharepoint/dpm-new-protection-tab.png)</span><span class="sxs-lookup"><span data-stu-id="09a60-165">![New Protection Tab](./media/backup-azure-backup-sharepoint/dpm-new-protection-tab.png)</span></span>
2. <span data-ttu-id="09a60-166">Merhaba üzerinde **koruma grubu türünü seçin** hello sayfasının **yeni koruma grubu oluşturma** seçin **sunucuları**ve ardından **sonraki** .</span><span class="sxs-lookup"><span data-stu-id="09a60-166">On hello **Select Protection Group Type** page of hello **Create New Protection Group** wizard, select **Servers**, and then click **Next**.</span></span>

    ![Koruma grubu seç türü](./media/backup-azure-backup-sharepoint/select-protection-group-type.png)
3. <span data-ttu-id="09a60-168">Merhaba üzerinde **grup üyelerini seçin** ekran, select hello onay kutusunu tooprotect istediğiniz hello SharePoint Server **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="09a60-168">On hello **Select Group Members** screen, select hello check box for hello SharePoint server you want tooprotect and click **Next**.</span></span>

    ![Grup üyelerini seçin](./media/backup-azure-backup-sharepoint/select-group-members2.png)

   > [!NOTE]
   > <span data-ttu-id="09a60-170">Yüklü hello koruma Aracısı ile Merhaba sunucu hello Sihirbazı'nda görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="09a60-170">With hello protection agent installed, you can see hello server in hello wizard.</span></span> <span data-ttu-id="09a60-171">MABS da yapısını gösterir.</span><span class="sxs-lookup"><span data-stu-id="09a60-171">MABS also shows its structure.</span></span> <span data-ttu-id="09a60-172">ConfigureSharePoint.exe çalıştırdığınız için MABS hello SharePoint VSS yazıcısı hizmetini ve karşılık gelen SQL Server veritabanlarını ile iletişim kurar ve hello SharePoint grup yapısı tanır, içerik veritabanları ve karşılık gelen tüm öğeleri hello ilişkilendirilmiş.</span><span class="sxs-lookup"><span data-stu-id="09a60-172">Because you ran ConfigureSharePoint.exe, MABS communicates with hello SharePoint VSS Writer service and its corresponding SQL Server databases and recognizes hello SharePoint farm structure, hello associated content databases, and any corresponding items.</span></span>
   >
   >
4. <span data-ttu-id="09a60-173">Merhaba üzerinde **veri koruma yöntemini seçin** sayfasında, hello hello adını **koruma grubu**ve tercih ettiğiniz seçin *koruma yöntemleri*.</span><span class="sxs-lookup"><span data-stu-id="09a60-173">On hello **Select Data Protection Method** page, enter hello name of hello **Protection Group**, and select your preferred *protection methods*.</span></span> <span data-ttu-id="09a60-174">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="09a60-174">Click **Next**.</span></span>

    ![Veri koruma yöntemini seçin](./media/backup-azure-backup-sharepoint/select-data-protection-method1.png)

   > [!NOTE]
   > <span data-ttu-id="09a60-176">Merhaba disk koruma yöntemini toomeet kısa kurtarma zamanı hedeflerine yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="09a60-176">hello disk protection method helps toomeet short recovery-time objectives.</span></span>
   >
   >
5. <span data-ttu-id="09a60-177">Merhaba üzerinde **kısa vadeli hedefleri belirtin** sayfasında, tercih ettiğiniz **bekletme aralığı** ve yedeklemeleri toooccur istediğinizde belirleyin.</span><span class="sxs-lookup"><span data-stu-id="09a60-177">On hello **Specify Short-Term Goals** page, select your preferred **Retention range** and identify when you want backups toooccur.</span></span>

    ![Kısa vadeli hedefleri belirtin](./media/backup-azure-backup-sharepoint/specify-short-term-goals2.png)

   > [!NOTE]
   > <span data-ttu-id="09a60-179">Kurtarma genellikle beş günden eski olan verileri için gerekli olduğundan, biz diskteki beş günlük bir bekletme aralığı seçili ve bu örnek için üretim dışı saatlerde hello yedekleme olur güvence altına.</span><span class="sxs-lookup"><span data-stu-id="09a60-179">Because recovery is most often required for data that's less than five days old, we selected a retention range of five days on disk and ensured that hello backup happens during non-production hours, for this example.</span></span>
   >
   >
6. <span data-ttu-id="09a60-180">Merhaba koruma grubu için ayrılmış hello depolama havuzu disk alanını gözden geçirin ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="09a60-180">Review hello storage pool disk space allocated for hello protection group, and click then **Next**.</span></span>
7. <span data-ttu-id="09a60-181">Her koruma grubu için MABS disk alanı toostore ayırır ve çoğaltmaları yönetin.</span><span class="sxs-lookup"><span data-stu-id="09a60-181">For every protection group, MABS allocates disk space toostore and manage replicas.</span></span> <span data-ttu-id="09a60-182">Bu noktada, MABS seçili hello verilerin bir kopyasını oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="09a60-182">At this point, MABS must create a copy of hello selected data.</span></span> <span data-ttu-id="09a60-183">Nasıl ve ne zaman, oluşturulan hello çoğaltma istediğiniz'ı seçin ve **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="09a60-183">Select how and when you want hello replica created, and then click **Next**.</span></span>

    ![Çoğaltma oluşturma yöntemini seçin](./media/backup-azure-backup-sharepoint/choose-replica-creation-method.png)

   > [!NOTE]
   > <span data-ttu-id="09a60-185">ağ trafiği parametreden etkilenir değil, emin toomake üretim saatleri dışında bir saat seçin.</span><span class="sxs-lookup"><span data-stu-id="09a60-185">toomake sure that network traffic is not effected, select a time outside production hours.</span></span>
   >
   >
8. <span data-ttu-id="09a60-186">MABS hello çoğaltma üzerinde tutarlılık denetimleri gerçekleştirerek veri bütünlüğü sağlar.</span><span class="sxs-lookup"><span data-stu-id="09a60-186">MABS ensures data integrity by performing consistency checks on hello replica.</span></span> <span data-ttu-id="09a60-187">Kullanılabilir iki seçenek vardır.</span><span class="sxs-lookup"><span data-stu-id="09a60-187">There are two available options.</span></span> <span data-ttu-id="09a60-188">Tanımlamak bir zamanlama toorun tutarlılık denetimlerinin veya tutarsız hale her DPM otomatik olarak hello çoğaltma üzerinde tutarlılık denetimleri çalışabilir.</span><span class="sxs-lookup"><span data-stu-id="09a60-188">You can define a schedule toorun consistency checks, or DPM can run consistency checks automatically on hello replica whenever it becomes inconsistent.</span></span> <span data-ttu-id="09a60-189">Tercih ettiğiniz seçeneği seçin ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="09a60-189">Select your preferred option, and then click **Next**.</span></span>

    ![Tutarlılık denetimi](./media/backup-azure-backup-sharepoint/consistency-check.png)
9. <span data-ttu-id="09a60-191">Merhaba üzerinde **çevrimiçi koruma verilerini belirtin** sayfasında, tooprotect istediğiniz ve ardından hello SharePoint grubu seçin **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="09a60-191">On hello **Specify Online Protection Data** page, select hello SharePoint farm that you want tooprotect, and then click **Next**.</span></span>

    ![DPM SharePoint Protection1](./media/backup-azure-backup-sharepoint/select-online-protection1.png)
10. <span data-ttu-id="09a60-193">Merhaba üzerinde **çevrimiçi yedekleme zamanlamasını belirtin** sayfasında, tercih ettiğiniz zamanlamayı seçin ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="09a60-193">On hello **Specify Online Backup Schedule** page, select your preferred schedule, and then click **Next**.</span></span>

    ![Online_backup_schedule](./media/backup-azure-backup-sharepoint/specify-online-backup-schedule.png)

    > [!NOTE]
    > <span data-ttu-id="09a60-195">MABS en fazla iki günlük yedekleri tooAzure hello silip kullanılabilir en son disk yedekleme noktası sağlar.</span><span class="sxs-lookup"><span data-stu-id="09a60-195">MABS provides a maximum of two daily backups tooAzure from hello then available latest disk backup point.</span></span> <span data-ttu-id="09a60-196">Azure yedekleme de hello yedeklemeler yoğun ve yoğun olmayan saatler için kullanarak kullanılabilir WAN bant genişliği miktarını kontrol [Azure yedekleme ağ azaltma](https://azure.microsoft.com/documentation/articles/backup-configure-vault/#enable-network-throttling).</span><span class="sxs-lookup"><span data-stu-id="09a60-196">Azure Backup can also control hello amount of WAN bandwidth that can be used for backups in peak and off-peak hours by using [Azure Backup Network Throttling](https://azure.microsoft.com/documentation/articles/backup-configure-vault/#enable-network-throttling).</span></span>
    >
    >
11. <span data-ttu-id="09a60-197">Merhaba üzerinde seçili hello yedekleme zamanlaması bağlı olarak **çevrimiçi bekletme ilkesini belirtin** sayfası, günlük, haftalık, aylık ve yıllık yedekleme noktaları için select hello bekletme ilkesi.</span><span class="sxs-lookup"><span data-stu-id="09a60-197">Depending on hello backup schedule that you selected, on hello **Specify Online Retention Policy** page, select hello retention policy for daily, weekly, monthly, and yearly backup points.</span></span>

    ![Online_retention_policy](./media/backup-azure-backup-sharepoint/specify-online-retention.png)

    > [!NOTE]
    > <span data-ttu-id="09a60-199">MABS farklı yedekleme noktaları için farklı bir bekletme ilkesi seçilebilir bir üst öğe son bekletme düzeni kullanır.</span><span class="sxs-lookup"><span data-stu-id="09a60-199">MABS uses a grandfather-father-son retention scheme in which a different retention policy can be chosen for different backup points.</span></span>
    >
    >
12. <span data-ttu-id="09a60-200">Benzer toodisk bir ilk başvuru noktası çoğaltmasını Azure içinde oluşturulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="09a60-200">Similar toodisk, an initial reference point replica needs toobe created in Azure.</span></span> <span data-ttu-id="09a60-201">Tercih edilen seçenek toocreate ilk yedek kopyayı tooAzure seçin ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="09a60-201">Select your preferred option toocreate an initial backup copy tooAzure, and then click **Next**.</span></span>

    ![Online_replica](./media/backup-azure-backup-sharepoint/online-replication.png)
13. <span data-ttu-id="09a60-203">Merhaba üzerinde seçtiğiniz ayarları gözden **Özet** sayfasında ve ardından **Grup Oluştur**.</span><span class="sxs-lookup"><span data-stu-id="09a60-203">Review your selected settings on hello **Summary** page, and then click **Create Group**.</span></span> <span data-ttu-id="09a60-204">Merhaba koruma grubu oluşturulduktan sonra bir başarı iletisi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="09a60-204">You will see a success message after hello protection group has been created.</span></span>

    ![Özet](./media/backup-azure-backup-sharepoint/summary.png)

## <a name="restore-a-sharepoint-item-from-disk-by-using-mabs"></a><span data-ttu-id="09a60-206">Bir SharePoint öğesi MABS kullanarak diskten geri yükleme</span><span class="sxs-lookup"><span data-stu-id="09a60-206">Restore a SharePoint item from disk by using MABS</span></span>
<span data-ttu-id="09a60-207">Aşağıdaki örneğine hello hello *SharePoint kurtarma öğesi* yanlışlıkla silinmişse ve kurtarılan toobe gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="09a60-207">In hello following example, hello *Recovering SharePoint item* has been accidentally deleted and needs toobe recovered.</span></span>
<span data-ttu-id="09a60-208">![MABS SharePoint Protection4](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection5.png)</span><span class="sxs-lookup"><span data-stu-id="09a60-208">![MABS SharePoint Protection4](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection5.png)</span></span>

1. <span data-ttu-id="09a60-209">Açık hello **DPM Yönetici Konsolu'nu**.</span><span class="sxs-lookup"><span data-stu-id="09a60-209">Open hello **DPM Administrator Console**.</span></span> <span data-ttu-id="09a60-210">DPM tarafından korunan tüm SharePoint grupları hello gösterilen **koruma** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="09a60-210">All SharePoint farms that are protected by DPM are shown in hello **Protection** tab.</span></span>

    ![MABS SharePoint Protection3](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection4.png)
2. <span data-ttu-id="09a60-212">toobegin toorecover hello öğesi, select hello **kurtarma** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="09a60-212">toobegin toorecover hello item, select hello **Recovery** tab.</span></span>

    ![MABS SharePoint Protection5](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection6.png)
3. <span data-ttu-id="09a60-214">SharePoint için arama yapabilirsiniz *SharePoint kurtarma öğesi* kurtarma içinde bir joker karakter tabanlı arama kullanarak aralığı gösterin.</span><span class="sxs-lookup"><span data-stu-id="09a60-214">You can search SharePoint for *Recovering SharePoint item* by using a wildcard-based search within a recovery point range.</span></span>

    ![MABS SharePoint Protection6](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection7.png)
4. <span data-ttu-id="09a60-216">Merhaba Arama sonuçlarından Hello uygun kurtarma noktası seçin, hello öğeyi sağ tıklatın ve ardından **kurtarmak**.</span><span class="sxs-lookup"><span data-stu-id="09a60-216">Select hello appropriate recovery point from hello search results, right-click hello item, and then select **Recover**.</span></span>
5. <span data-ttu-id="09a60-217">Ayrıca, çeşitli kurtarma noktalarına göz ve bir veritabanı veya öğeyi toorecover seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="09a60-217">You can also browse through various recovery points and select a database or item toorecover.</span></span> <span data-ttu-id="09a60-218">Seçin **tarihi > kurtarma süresini**ve ardından hello doğru **veritabanı > SharePoint grubu > kurtarma noktası > öğesi**.</span><span class="sxs-lookup"><span data-stu-id="09a60-218">Select **Date > Recovery time**, and then select hello correct **Database > SharePoint farm > Recovery point > Item**.</span></span>

    ![MABS SharePoint Protection7](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection8.png)
6. <span data-ttu-id="09a60-220">Merhaba öğeyi sağ tıklatın ve ardından **kurtarmak** tooopen hello **Kurtarma Sihirbazı'nı**.</span><span class="sxs-lookup"><span data-stu-id="09a60-220">Right-click hello item, and then select **Recover** tooopen hello **Recovery Wizard**.</span></span> <span data-ttu-id="09a60-221">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="09a60-221">Click **Next**.</span></span>

    ![Kurtarma seçimini inceleyin](./media/backup-azure-backup-sharepoint/review-recovery-selection.png)
7. <span data-ttu-id="09a60-223">Merhaba tooperform istediğiniz ve ardından Kurtarma türünü seçin **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="09a60-223">Select hello type of recovery that you want tooperform, and then click **Next**.</span></span>

    ![Kurtarma türü](./media/backup-azure-backup-sharepoint/select-recovery-type.png)

   > [!NOTE]
   > <span data-ttu-id="09a60-225">Merhaba seçimi **kurtarmak toooriginal** hello örnek hello öğesi toohello özgün SharePoint sitesini kurtarır.</span><span class="sxs-lookup"><span data-stu-id="09a60-225">hello selection of **Recover toooriginal** in hello example recovers hello item toohello original SharePoint site.</span></span>
   >
   >
8. <span data-ttu-id="09a60-226">Select hello **kurtarma işlemi** toouse istiyor.</span><span class="sxs-lookup"><span data-stu-id="09a60-226">Select hello **Recovery Process** that you want toouse.</span></span>

   * <span data-ttu-id="09a60-227">Seçin **kurtarma grubu kullanmadan kurtarmak** hello SharePoint grubu değişmemiştir ve aynı hello kurtarma noktası hello geri yükleniyor.</span><span class="sxs-lookup"><span data-stu-id="09a60-227">Select **Recover without using a recovery farm** if hello SharePoint farm has not changed and is hello same as hello recovery point that is being restored.</span></span>
   * <span data-ttu-id="09a60-228">Seçin **kurtarma grubu kullanarak kurtarma** hello SharePoint grubu hello kurtarma noktası oluşturulduğundan beri değişmişse.</span><span class="sxs-lookup"><span data-stu-id="09a60-228">Select **Recover using a recovery farm** if hello SharePoint farm has changed since hello recovery point was created.</span></span>

     ![Kurtarma işlemi](./media/backup-azure-backup-sharepoint/recovery-process.png)
9. <span data-ttu-id="09a60-230">Hazırlama bir SQL Server örneğinin konumu toorecover hello veritabanı geçici olarak sağlayın ve SharePoint toorecover hello öğesi çalışan MABS ve hello sunucuya hazırlama bir dosya paylaşımı sağlayın.</span><span class="sxs-lookup"><span data-stu-id="09a60-230">Provide a staging SQL Server instance location toorecover hello database temporarily, and provide a staging file share on MABS and hello server that's running SharePoint toorecover hello item.</span></span>

    ![Hazırlama Location1](./media/backup-azure-backup-sharepoint/staging-location1.png)

    <span data-ttu-id="09a60-232">MABS hello SharePoint öğesi toohello geçici SQL Server örneği barındırma hello içerik veritabanını ekler.</span><span class="sxs-lookup"><span data-stu-id="09a60-232">MABS attaches hello content database that is hosting hello SharePoint item toohello temporary SQL Server instance.</span></span> <span data-ttu-id="09a60-233">Merhaba içerik veritabanından onu hello öğesi kurtarır ve dosya konumuna MABS hazırlama hello üzerinde koyar.</span><span class="sxs-lookup"><span data-stu-id="09a60-233">From hello content database, it recovers hello item and puts it on hello staging file location on MABS.</span></span> <span data-ttu-id="09a60-234">Merhaba hazırlama konumuna şimdi hello üzerinde hello SharePoint grubu üzerinde hazırlama gereksinimlerini dışarı toobe toohello öğeyi kurtarıldı.</span><span class="sxs-lookup"><span data-stu-id="09a60-234">hello recovered item that's on hello staging location now needs toobe exported toohello staging location on hello SharePoint farm.</span></span>

    ![Hazırlama Location2](./media/backup-azure-backup-sharepoint/staging-location2.png)
10. <span data-ttu-id="09a60-236">Seçin **kurtarma seçeneklerini belirtin**, güvenlik ayarları toohello SharePoint grubu uygulamak ve hello kurtarma noktası hello güvenlik ayarlarını uygula.</span><span class="sxs-lookup"><span data-stu-id="09a60-236">Select **Specify recovery options**, and apply security settings toohello SharePoint farm or apply hello security settings of hello recovery point.</span></span> <span data-ttu-id="09a60-237">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="09a60-237">Click **Next**.</span></span>

    ![Kurtarma Seçenekleri](./media/backup-azure-backup-sharepoint/recovery-options.png)

    > [!NOTE]
    > <span data-ttu-id="09a60-239">Toothrottle hello ağ bant genişliği kullanımını seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="09a60-239">You can choose toothrottle hello network bandwidth usage.</span></span> <span data-ttu-id="09a60-240">Bu etki toohello üretim sunucusu üretim saatleri dışında en aza indirir.</span><span class="sxs-lookup"><span data-stu-id="09a60-240">This minimizes impact toohello production server during production hours.</span></span>
    >
    >
11. <span data-ttu-id="09a60-241">Merhaba özet bilgileri gözden geçirin ve ardından **kurtarmak** hello dosyasının toobegin kurtarma.</span><span class="sxs-lookup"><span data-stu-id="09a60-241">Review hello summary information, and then click **Recover** toobegin recovery of hello file.</span></span>

    ![Kurtarma özeti](./media/backup-azure-backup-sharepoint/recovery-summary.png)
12. <span data-ttu-id="09a60-243">Şimdi hello seçin **izleme** hello sekmesinde **MABS Yönetici Konsolu** tooview hello **durum** hello kurtarma.</span><span class="sxs-lookup"><span data-stu-id="09a60-243">Now select hello **Monitoring** tab in hello **MABS Administrator Console** tooview hello **Status** of hello recovery.</span></span>

    ![Kurtarma durumu](./media/backup-azure-backup-sharepoint/recovery-monitoring.png)

    > [!NOTE]
    > <span data-ttu-id="09a60-245">Merhaba dosya şimdi geri yüklenir.</span><span class="sxs-lookup"><span data-stu-id="09a60-245">hello file is now restored.</span></span> <span data-ttu-id="09a60-246">Merhaba SharePoint site toocheck geri hello dosyası yenileyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="09a60-246">You can refresh hello SharePoint site toocheck hello restored file.</span></span>
    >
    >

## <a name="restore-a-sharepoint-database-from-azure-by-using-dpm"></a><span data-ttu-id="09a60-247">DPM kullanarak bir SharePoint veritabanı Azure'dan geri yükleme</span><span class="sxs-lookup"><span data-stu-id="09a60-247">Restore a SharePoint database from Azure by using DPM</span></span>
1. <span data-ttu-id="09a60-248">bir SharePoint içerik veritabanı toorecover (daha önce gösterildiği gibi) çeşitli kurtarma noktalarına göz ve toorestore istediğiniz hello kurtarma noktası seçin.</span><span class="sxs-lookup"><span data-stu-id="09a60-248">toorecover a SharePoint content database, browse through various recovery points (as shown previously), and select hello recovery point that you want toorestore.</span></span>

    ![MABS SharePoint Protection8](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection9.png)
2. <span data-ttu-id="09a60-250">Merhaba SharePoint kurtarma noktası tooshow hello kullanılabilir SharePoint katalog bilgileri çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="09a60-250">Double-click hello SharePoint recovery point tooshow hello available SharePoint catalog information.</span></span>

   > [!NOTE]
   > <span data-ttu-id="09a60-251">Merhaba SharePoint grubu Azure uzun vadeli bekletme için korumalı olduğundan, hiçbir Kataloğu bilgi (meta veriler) MABS üzerinde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="09a60-251">Because hello SharePoint farm is protected for long-term retention in Azure, no catalog information (metadata) is available on MABS.</span></span> <span data-ttu-id="09a60-252">Zaman içinde nokta SharePoint içerik veritabanını kurtarılan toobe her gerektiğinde, sonuç olarak, toocatalog hello SharePoint grubu yeniden gerekir.</span><span class="sxs-lookup"><span data-stu-id="09a60-252">As a result, whenever a point-in-time SharePoint content database needs toobe recovered, you need toocatalog hello SharePoint farm again.</span></span>
   >
   >
3. <span data-ttu-id="09a60-253">Tıklatın **yeniden kataloglama**.</span><span class="sxs-lookup"><span data-stu-id="09a60-253">Click **Re-catalog**.</span></span>

    ![MABS SharePoint Protection10](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection12.png)

    <span data-ttu-id="09a60-255">Merhaba **bulut yeniden katalogla** durum penceresi açar.</span><span class="sxs-lookup"><span data-stu-id="09a60-255">hello **Cloud Recatalog** status window opens.</span></span>

    ![MABS SharePoint Protection11](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection13.png)

    <span data-ttu-id="09a60-257">Katalog tamamlandıktan sonra hello çok durumuna*başarı*.</span><span class="sxs-lookup"><span data-stu-id="09a60-257">After cataloging is finished, hello status changes too*Success*.</span></span> <span data-ttu-id="09a60-258">**Kapat**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="09a60-258">Click **Close**.</span></span>

    ![MABS SharePoint Protection12](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection14.png)
4. <span data-ttu-id="09a60-260">Merhaba MABS gösterilen hello SharePoint nesnesine tıklayın **kurtarma** sekmesinde tooget hello içerik veritabanı yapısı.</span><span class="sxs-lookup"><span data-stu-id="09a60-260">Click hello SharePoint object shown in hello MABS **Recovery** tab tooget hello content database structure.</span></span> <span data-ttu-id="09a60-261">Merhaba öğeyi sağ tıklatın ve ardından **kurtarmak**.</span><span class="sxs-lookup"><span data-stu-id="09a60-261">Right-click hello item, and then click **Recover**.</span></span>

    ![MABS SharePoint Protection13](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection15.png)
5. <span data-ttu-id="09a60-263">Bu noktada, hello izleyin [kurtarma adımları bu makalenin önceki bölümlerinde](#restore-a-sharepoint-item-from-disk-using-dpm) toorecover diskten bir SharePoint içerik veritabanı.</span><span class="sxs-lookup"><span data-stu-id="09a60-263">At this point, follow hello [recovery steps earlier in this article](#restore-a-sharepoint-item-from-disk-using-dpm) toorecover a SharePoint content database from disk.</span></span>

## <a name="faqs"></a><span data-ttu-id="09a60-264">SSS</span><span class="sxs-lookup"><span data-stu-id="09a60-264">FAQs</span></span>
<span data-ttu-id="09a60-265">S: bir SharePoint öğesi toohello özgün konumuna, SharePoint SQL AlwaysOn (disk koruması) kullanılarak yapılandırılmışsa kurtarma?</span><span class="sxs-lookup"><span data-stu-id="09a60-265">Q: Can I recover a SharePoint item toohello original location if SharePoint is configured by using SQL AlwaysOn (with protection on disk)?</span></span><br>
<span data-ttu-id="09a60-266">A: Evet hello öğesi kurtarılan toohello özgün SharePoint sitesi olabilir.</span><span class="sxs-lookup"><span data-stu-id="09a60-266">A: Yes, hello item can be recovered toohello original SharePoint site.</span></span>

<span data-ttu-id="09a60-267">S: bir SharePoint veritabanı toohello özgün konumu, SQL AlwaysOn kullanarak SharePoint yapılandırdıysanız kurtarmak?</span><span class="sxs-lookup"><span data-stu-id="09a60-267">Q: Can I recover a SharePoint database toohello original location if SharePoint is configured by using SQL AlwaysOn?</span></span><br>
<span data-ttu-id="09a60-268">A: SharePoint veritabanlarını SQL AlwaysOn yapılandırıldığından, bunlar hello kullanılabilirlik grubu kaldırılmadığı sürece değiştirilemez.</span><span class="sxs-lookup"><span data-stu-id="09a60-268">A: Because SharePoint databases are configured in SQL AlwaysOn, they cannot be modified unless hello availability group is removed.</span></span> <span data-ttu-id="09a60-269">Sonuç olarak, MABS veritabanı toohello özgün konumuna geri yükleyemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="09a60-269">As a result, MABS cannot restore a database toohello original location.</span></span> <span data-ttu-id="09a60-270">Bir SQL Server veritabanı tooanother SQL Sunucusu örneğine kurtarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="09a60-270">You can recover a SQL Server database tooanother SQL Server instance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="09a60-271">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="09a60-271">Next steps</span></span>
* <span data-ttu-id="09a60-272">SharePoint MABS koruma hakkında daha fazla bilgi - bkz [Video serisi - SharePoint DPM koruma](http://channel9.msdn.com/Series/Azure-Backup/Microsoft-SCDPM-Protection-of-SharePoint-1-of-2-How-to-create-a-SharePoint-Protection-Group)</span><span class="sxs-lookup"><span data-stu-id="09a60-272">Learn more about MABS Protection of SharePoint - see [Video Series - DPM Protection of SharePoint](http://channel9.msdn.com/Series/Azure-Backup/Microsoft-SCDPM-Protection-of-SharePoint-1-of-2-How-to-create-a-SharePoint-Protection-Group)</span></span>
