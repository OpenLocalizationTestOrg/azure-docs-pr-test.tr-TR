---
title: "aaaConnect karma bağlantılar kullanarak Azure App Service web uygulamasından tooon içi SQL Server"
description: "Microsoft Azure üzerinde bir web uygulaması oluşturma ve tooan şirket içi SQL Server veritabanına bağlan"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: mollybos
ms.assetid: 2b4e0539-1a0b-4aa1-8a69-b4b053c3b2e5
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2016
ms.author: cephalin
ms.openlocfilehash: 2e8f8f7e0b9733cfb0433697615faba4358c6023
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooon-premises-sql-server-from-a-web-app-in-azure-app-service-using-hybrid-connections"></a><span data-ttu-id="d20cc-103">Karma bağlantılar kullanarak Azure App Service web uygulamasından tooon içi SQL Server'a bağlanma</span><span class="sxs-lookup"><span data-stu-id="d20cc-103">Connect tooon-premises SQL Server from a web app in Azure App Service using Hybrid Connections</span></span>
<span data-ttu-id="d20cc-104">Karma bağlantılar bağlanabilir [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) statik bir TCP bağlantı noktası kullanan Web uygulamaları tooon içi kaynakları.</span><span class="sxs-lookup"><span data-stu-id="d20cc-104">Hybrid Connections can connect [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps tooon-premises resources that use a static TCP port.</span></span> <span data-ttu-id="d20cc-105">Desteklenen kaynaklar Microsoft SQL Server, MySQL, HTTP Web API'leri, uygulama hizmeti ve birçok özel Web hizmeti içerir.</span><span class="sxs-lookup"><span data-stu-id="d20cc-105">Supported resources include Microsoft SQL Server, MySQL, HTTP Web APIs, App Service, and most custom Web Services.</span></span>

<span data-ttu-id="d20cc-106">Bu öğreticide, nasıl toocreate bir App Service web hello uygulamada öğreneceksiniz [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715), hello yeni karma bağlantı özelliğini kullanarak hello web uygulama tooyour yerel şirket içi SQL Server veritabanına bağlanmak, basit bir ASP.NET oluşturma Merhaba karma bağlantıyı kullan ve hello uygulama toohello App Service web uygulaması dağıtma uygulama.</span><span class="sxs-lookup"><span data-stu-id="d20cc-106">In this tutorial, you will learn how toocreate an App Service web app in hello [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715), connect hello web app tooyour local on-premises SQL Server database using hello new Hybrid Connection feature, create a simple ASP.NET application that will use hello hybrid connection, and deploy hello application toohello App Service web app.</span></span> <span data-ttu-id="d20cc-107">Azure web uygulamasında tamamlandı hello kullanıcı kimlik bilgilerini şirket içi bir üyelik veritabanında depolar.</span><span class="sxs-lookup"><span data-stu-id="d20cc-107">hello completed web app on Azure stores user credentials in a membership database that is on-premises.</span></span> <span data-ttu-id="d20cc-108">Merhaba öğretici Azure veya ASP.NET kullanma konusunda deneyim varsayar.</span><span class="sxs-lookup"><span data-stu-id="d20cc-108">hello tutorial assumes no prior experience using Azure or ASP.NET.</span></span>

> [!NOTE]
> <span data-ttu-id="d20cc-109">Azure hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git[App Service'i deneyin](https://azure.microsoft.com/try/app-service/), burada hemen bir kısa süreli başlangıç web uygulaması App Service'te oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d20cc-109">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="d20cc-110">Kredi kartı ve taahhüt gerekmez.</span><span class="sxs-lookup"><span data-stu-id="d20cc-110">No credit cards required; no commitments.</span></span>
> 
> <span data-ttu-id="d20cc-111">Hello Web Apps bölümü hello karma bağlantılar özelliği yalnızca hello kullanılabilir [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d20cc-111">hello Web Apps portion of hello Hybrid Connections feature is available only in hello [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="d20cc-112">toocreate BizTalk Services bağlantısında bkz [karma bağlantılar](http://go.microsoft.com/fwlink/p/?LinkID=397274).</span><span class="sxs-lookup"><span data-stu-id="d20cc-112">toocreate a connection in BizTalk Services, see [Hybrid Connections](http://go.microsoft.com/fwlink/p/?LinkID=397274).</span></span>  
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="d20cc-113">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="d20cc-113">Prerequisites</span></span>
<span data-ttu-id="d20cc-114">toocomplete Bu öğretici, ürünleri aşağıdaki hello gerekir.</span><span class="sxs-lookup"><span data-stu-id="d20cc-114">toocomplete this tutorial, you'll need hello following products.</span></span> <span data-ttu-id="d20cc-115">Azure için tamamen ücretsiz geliştirme başlatabilmeniz tüm boş sürümlerinde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="d20cc-115">All are available in free versions, so you can start developing for Azure entirely for free.</span></span>

* <span data-ttu-id="d20cc-116">**Azure aboneliği** - ücretsiz bir abonelik için bkz: [Azure ücretsiz deneme sürümü](/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d20cc-116">**Azure subscription** - For a free subscription, see [Azure Free Trial](/pricing/free-trial/).</span></span>
* <span data-ttu-id="d20cc-117">**Visual Studio 2013** -Visual Studio 2013, ücretsiz bir deneme sürümünü toodownload bkz [Visual Studio indirmeleri](http://www.visualstudio.com/downloads/download-visual-studio-vs).</span><span class="sxs-lookup"><span data-stu-id="d20cc-117">**Visual Studio 2013** - toodownload a free trial version of Visual Studio 2013, see [Visual Studio Downloads](http://www.visualstudio.com/downloads/download-visual-studio-vs).</span></span> <span data-ttu-id="d20cc-118">Bu, devam etmeden önce yükleyin.</span><span class="sxs-lookup"><span data-stu-id="d20cc-118">Install this before continuing.</span></span>
* <span data-ttu-id="d20cc-119">**Microsoft .NET Framework 3.5 Service Pack 1** -işletim sisteminiz Windows 8.1, Windows Server 2012 R2, Windows 8, Windows Server 2012, Windows 7 veya Windows Server 2008 R2 ise, bu Denetim Masası'nda etkinleştirebilirsiniz > Programlar ve Özellikler > kapatma Windows özelliklerini aç veya kapat.</span><span class="sxs-lookup"><span data-stu-id="d20cc-119">**Microsoft .NET Framework 3.5 Service Pack 1** - If your operating system is Windows 8.1, Windows Server 2012 R2, Windows 8, Windows Server 2012, Windows 7, or Windows Server 2008 R2, you can enable this in Control Panel > Programs and Features > Turn Windows features on or off.</span></span> <span data-ttu-id="d20cc-120">Aksi durumda, hello indirebilirsiniz [Microsoft Download Center](http://www.microsoft.com/download/en/details.aspx?displaylang=en&id=22).</span><span class="sxs-lookup"><span data-stu-id="d20cc-120">Otherwise, you can download it from hello [Microsoft Download Center](http://www.microsoft.com/download/en/details.aspx?displaylang=en&id=22).</span></span>
* <span data-ttu-id="d20cc-121">**SQL Server 2014 Express araçları ile** -Microsoft SQL Server Express ücretsiz hello karşıdan [Microsoft Web Platformu veritabanı sayfası](http://www.microsoft.com/web/platform/database.aspx).</span><span class="sxs-lookup"><span data-stu-id="d20cc-121">**SQL Server 2014 Express with Tools** - download Microsoft SQL Server Express for free at hello [Microsoft Web Platform Database page](http://www.microsoft.com/web/platform/database.aspx).</span></span> <span data-ttu-id="d20cc-122">Merhaba seçin **Express** (yerel veritabanı değil) sürümü.</span><span class="sxs-lookup"><span data-stu-id="d20cc-122">Choose hello **Express** (not LocalDB) version.</span></span> <span data-ttu-id="d20cc-123">Merhaba **araçlarıyla Express** sürüm, bu öğreticide kullanacağı SQL Server Management Studio içerir.</span><span class="sxs-lookup"><span data-stu-id="d20cc-123">hello **Express with Tools** version includes SQL Server Management Studio, which you will use in this tutorial.</span></span>
* <span data-ttu-id="d20cc-124">**SQL Server Management Studio Express** - yukarıda belirtilen araçları indirme ile Merhaba ile SQL Server 2014 Express dahil, ancak tooinstall gerekiyorsa, ayrı ayrı indirebilir ve hello yüklemek [SQL Server Express indirme sayfasının](http://www.microsoft.com/web/platform/database.aspx).</span><span class="sxs-lookup"><span data-stu-id="d20cc-124">**SQL Server Management Studio Express** - This is included with hello SQL Server 2014 Express with Tools download mentioned above, but if you need tooinstall it separately, you can download and install it from hello [SQL Server Express download page](http://www.microsoft.com/web/platform/database.aspx).</span></span>

<span data-ttu-id="d20cc-125">Başlangıç Öğreticisi, Visual Studio 2013 yüklediyseniz ve yüklenmemiş veya .NET Framework 3.5 etkin bir Azure aboneliğine sahip olduğunuzu varsayar.</span><span class="sxs-lookup"><span data-stu-id="d20cc-125">hello tutorial assumes that you have an Azure subscription, that you have installed Visual Studio 2013, and that you have installed or enabled .NET Framework 3.5.</span></span> <span data-ttu-id="d20cc-126">Merhaba öğretici nasıl tooinstall SQL Server 2014 Express iyi hello Azure karma bağlantılar ile çalışan bir yapılandırma özellik (varsayılan bir örnek statik bir TCP bağlantı noktası ile) gösterir.</span><span class="sxs-lookup"><span data-stu-id="d20cc-126">hello tutorial shows you how tooinstall SQL Server 2014 Express in a configuration that works well with hello Azure Hybrid Connections feature (a default instance with a static TCP port).</span></span> <span data-ttu-id="d20cc-127">Merhaba öğreticiye başlamadan önce SQL Server 2014 Express araçları ile SQL Server yüklü yoksa, yukarıda belirtilen hello konumdan yükleyin.</span><span class="sxs-lookup"><span data-stu-id="d20cc-127">Before starting hello tutorial, download SQL Server 2014 Express with Tools from hello location mentioned above if you do not have SQL Server installed.</span></span>

### <a name="notes"></a><span data-ttu-id="d20cc-128">Notlar</span><span class="sxs-lookup"><span data-stu-id="d20cc-128">Notes</span></span>
<span data-ttu-id="d20cc-129">toouse bir şirket içi SQL Server veya SQL Server Express veritabanı ile karma bağlantı, TCP/IP'yi statik bağlantı noktası üzerinde etkin toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="d20cc-129">toouse an on-premises SQL Server or SQL Server Express database with a hybrid connection, TCP/IP needs toobe enabled on a static port.</span></span> <span data-ttu-id="d20cc-130">Adlandırılmış örneklerin yapılamaz SQL Server'da varsayılan örnekleri statik bağlantı noktası 1433 kullanın.</span><span class="sxs-lookup"><span data-stu-id="d20cc-130">Default instances on SQL Server use static port 1433, whereas named instances do not.</span></span>

<span data-ttu-id="d20cc-131">Merhaba bilgisayar hello şirket içi karma Bağlantı Yöneticisi aracısı yükleyin:</span><span class="sxs-lookup"><span data-stu-id="d20cc-131">hello computer on which you install hello on-premises Hybrid Connection Manager agent:</span></span>

* <span data-ttu-id="d20cc-132">Giden bağlantı tooAzure üzerinden olması gerekir:</span><span class="sxs-lookup"><span data-stu-id="d20cc-132">Must have outbound connectivity tooAzure over:</span></span>

| <span data-ttu-id="d20cc-133">Bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="d20cc-133">Port</span></span> | <span data-ttu-id="d20cc-134">Neden</span><span class="sxs-lookup"><span data-stu-id="d20cc-134">Why</span></span> |
| --- | --- |
| <span data-ttu-id="d20cc-135">80</span><span class="sxs-lookup"><span data-stu-id="d20cc-135">80</span></span> |<span data-ttu-id="d20cc-136">**Gerekli** sertifika doğrulama ve isteğe bağlı olarak veri bağlantısı için HTTP bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="d20cc-136">**Required** for HTTP port for certificate validation and optionally for data connectivity.</span></span> |
| <span data-ttu-id="d20cc-137">443</span><span class="sxs-lookup"><span data-stu-id="d20cc-137">443</span></span> |<span data-ttu-id="d20cc-138">**İsteğe bağlı** veri bağlantısı için.</span><span class="sxs-lookup"><span data-stu-id="d20cc-138">**Optional** for data connectivity.</span></span> <span data-ttu-id="d20cc-139">Giden bağlantı too443 kullanılamıyorsa, TCP bağlantı noktası 80 kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d20cc-139">If outbound connectivity too443 is unavailable, TCP port 80 is used.</span></span> |
| <span data-ttu-id="d20cc-140">5671 ve 9352</span><span class="sxs-lookup"><span data-stu-id="d20cc-140">5671 and 9352</span></span> |<span data-ttu-id="d20cc-141">**Önerilen** ancak veri bağlantısı için isteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="d20cc-141">**Recommended** but Optional for data connectivity.</span></span> <span data-ttu-id="d20cc-142">Bu mod genellikle daha yüksek verimlilik verir unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d20cc-142">Note this mode usually yields higher throughput.</span></span> <span data-ttu-id="d20cc-143">TCP bağlantı noktası 443 giden bağlantı toothese bağlantı noktalarını kullanılamıyorsa, kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d20cc-143">If outbound connectivity toothese ports is unavailable, TCP port 443 is used.</span></span> |

* <span data-ttu-id="d20cc-144">Mümkün tooreach hello olmalıdır *ana bilgisayar adı*:*BağlantıNoktasıNumarası* , şirket içi kaynak.</span><span class="sxs-lookup"><span data-stu-id="d20cc-144">Must be able tooreach hello *hostname*:*portnumber* of your on-premises resource.</span></span>

<span data-ttu-id="d20cc-145">Bu makaledeki adımları Hello hello tarayıcı hello şirket içi karma bağlantı aracısını barındıracak bir hello bilgisayardan kullandığınızı varsayar.</span><span class="sxs-lookup"><span data-stu-id="d20cc-145">hello steps in this article assume that you are using hello browser from hello computer that will host hello on-premises hybrid connection agent.</span></span>

<span data-ttu-id="d20cc-146">Bir yapılandırma ve yukarıda açıklanan hello koşullara uyan bir ortamda yüklü SQL Server zaten varsa, İleri atlayabilirsiniz ve başlayın [şirket içi SQL Server veritabanı oluşturma](#CreateSQLDB).</span><span class="sxs-lookup"><span data-stu-id="d20cc-146">If you already have SQL Server installed in a configuration and in an environment that meets hello conditions described above, you can skip ahead and start with [Create a SQL Server database on-premises](#CreateSQLDB).</span></span>

<a name="InstallSQL"></a>

## <a name="a-install-sql-server-express-enable-tcpip-and-create-a-sql-server-database-on-premises"></a><span data-ttu-id="d20cc-147">A.</span><span class="sxs-lookup"><span data-stu-id="d20cc-147">A.</span></span> <span data-ttu-id="d20cc-148">SQL Server Express'i yüklemek, TCP/IP'yi etkinleştirin ve şirket içi SQL Server veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="d20cc-148">Install SQL Server Express, enable TCP/IP, and create a SQL Server database on-premises</span></span>
<span data-ttu-id="d20cc-149">Bu bölümde, nasıl tooinstall SQL Server Express, TCP/IP'yi etkinleştirin ve bir veritabanı oluşturun, böylece web uygulamanızı hello Azure Portal ile çalışıp çalışmayacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="d20cc-149">This section shows you how tooinstall SQL Server Express, enable TCP/IP, and create a database so that your web application will work with hello Azure Portal.</span></span>

### <a name="install-sql-server-express"></a><span data-ttu-id="d20cc-150">SQL Server Express'i Yükleme</span><span class="sxs-lookup"><span data-stu-id="d20cc-150">Install SQL Server Express</span></span>
1. <span data-ttu-id="d20cc-151">Merhaba çalıştırmak bir tooinstall SQL Server Express, **SQLEXPRWT_x64_ENU.exe** veya **SQLEXPR_x86_ENU.exe** indirdiğiniz dosya.</span><span class="sxs-lookup"><span data-stu-id="d20cc-151">tooinstall SQL Server Express, run hello **SQLEXPRWT_x64_ENU.exe** or **SQLEXPR_x86_ENU.exe** file that you downloaded.</span></span> <span data-ttu-id="d20cc-152">Merhaba SQL Server Yükleme Merkezi'ni Sihirbazı görünür.</span><span class="sxs-lookup"><span data-stu-id="d20cc-152">hello SQL Server Installation Center wizard appears.</span></span>
   
    ![SQL Server yükleme][SQLServerInstall]
2. <span data-ttu-id="d20cc-154">Seçin **yeni SQL Server tek başına yükleme veya özellikler tooan mevcut yükleme eklemek**.</span><span class="sxs-lookup"><span data-stu-id="d20cc-154">Choose **New SQL Server stand-alone installation or add features tooan existing installation**.</span></span> <span data-ttu-id="d20cc-155">Toohello elde edene kadar hello varsayılan seçenekleri ve ayarları, kabul etme hello yönergeleri **örnek Yapılandırması** sayfası.</span><span class="sxs-lookup"><span data-stu-id="d20cc-155">Follow hello instructions, accepting hello default choices and settings, until you get toohello **Instance Configuration** page.</span></span>
3. <span data-ttu-id="d20cc-156">Merhaba üzerinde **örnek Yapılandırması** sayfasında, **varsayılan örnek**.</span><span class="sxs-lookup"><span data-stu-id="d20cc-156">On hello **Instance Configuration** page, choose **Default instance**.</span></span>
   
    ![Varsayılan bir örnek seçin][ChooseDefaultInstance]
   
    <span data-ttu-id="d20cc-158">Varsayılan olarak, hangi hello karma bağlantılar özellik gerektirir olduğu SQL Server statik bağlantı noktası 1433, istemcilerde gelen istekleri için hello varsayılan SQL Server örneğini dinler.</span><span class="sxs-lookup"><span data-stu-id="d20cc-158">By default, hello default instance of SQL Server listens for requests from SQL Server clients on static port 1433, which is what hello Hybrid Connections feature requires.</span></span> <span data-ttu-id="d20cc-159">Karma bağlantılar tarafından desteklenmeyen dinamik bağlantı noktaları ve UDP, adlandırılmış örnekleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="d20cc-159">Named instances use dynamic ports and UDP, which are not supported by Hybrid Connections.</span></span>
4. <span data-ttu-id="d20cc-160">Merhaba Hello varsayılanlarına kabul **sunucu yapılandırması** sayfası.</span><span class="sxs-lookup"><span data-stu-id="d20cc-160">Accept hello defaults on hello **Server Configuration** page.</span></span>
5. <span data-ttu-id="d20cc-161">Merhaba üzerinde **veritabanı altyapısı Yapılandırması** sayfasında **kimlik doğrulama modu**, seçin **karma mod (SQL Server kimlik doğrulaması ve Windows kimlik doğrulaması)**ve sağlayın bir parola.</span><span class="sxs-lookup"><span data-stu-id="d20cc-161">On hello **Database Engine Configuration** page, under **Authentication Mode**, choose **Mixed Mode (SQL Server authentication and Windows authentication)**, and provide a password.</span></span>
   
    ![Karma mod seçin][ChooseMixedMode]
   
    <span data-ttu-id="d20cc-163">Bu öğreticide, SQL Server kimlik doğrulamasını kullanır.</span><span class="sxs-lookup"><span data-stu-id="d20cc-163">In this tutorial, you will be using SQL Server authentication.</span></span> <span data-ttu-id="d20cc-164">Sağlarsanız, emin tooremember hello parola olabilir, çünkü daha sonra ihtiyacınız olacak.</span><span class="sxs-lookup"><span data-stu-id="d20cc-164">Be sure tooremember hello password that you provide, because you will need it later.</span></span>
6. <span data-ttu-id="d20cc-165">Merhaba Sihirbazı toocomplete hello yükleme Hello kullanılmadıkları adım.</span><span class="sxs-lookup"><span data-stu-id="d20cc-165">Step through hello rest of hello wizard toocomplete hello installation.</span></span>

### <a name="enable-tcpip"></a><span data-ttu-id="d20cc-166">TCP/IP'yi etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="d20cc-166">Enable TCP/IP</span></span>
<span data-ttu-id="d20cc-167">TCP/IP'yi tooenable, SQL Server Express yüklendiğinde, yüklü olduğu SQL Server Configuration Manager kullanır.</span><span class="sxs-lookup"><span data-stu-id="d20cc-167">tooenable TCP/IP, you will use SQL Server Configuration Manager, which was installed when you installed SQL Server Express.</span></span> <span data-ttu-id="d20cc-168">Merhaba adımları [SQL Server TCP/IP ağ protokolünü etkinleştirin](http://technet.microsoft.com/library/hh231672%28v=sql.110%29.aspx) devam etmeden önce.</span><span class="sxs-lookup"><span data-stu-id="d20cc-168">Follow hello steps in [Enable TCP/IP Network Protocol for SQL Server](http://technet.microsoft.com/library/hh231672%28v=sql.110%29.aspx) before continuing.</span></span>

<a name="CreateSQLDB"></a>

### <a name="create-a-sql-server-database-on-premises"></a><span data-ttu-id="d20cc-169">Şirket içi SQL Server veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="d20cc-169">Create a SQL Server database on-premises</span></span>
<span data-ttu-id="d20cc-170">Visual Studio web uygulamanızı Azure tarafından erişilebilir bir üyelik veritabanı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="d20cc-170">Your Visual Studio web application requires a membership database that can be accessed by Azure.</span></span> <span data-ttu-id="d20cc-171">Bu bir SQL Server veya SQL Server Express veritabanı (, varsayılan MVC şablonu kullanan hello hello LocalDB veritabanını değil), gerektirir hello üyelik veritabanının sonraki oluşturmanız.</span><span class="sxs-lookup"><span data-stu-id="d20cc-171">This requires a SQL Server or SQL Server Express database (not hello LocalDB database that hello MVC template uses by default), so you'll create hello membership database next.</span></span>

1. <span data-ttu-id="d20cc-172">SQL Server Management Studio'da toohello yalnızca yüklü SQL Server bağlayın.</span><span class="sxs-lookup"><span data-stu-id="d20cc-172">In SQL Server Management Studio, connect toohello SQL Server you just installed.</span></span> <span data-ttu-id="d20cc-173">(Merhaba, **tooServer bağlanmak** iletişim görünmez otomatik olarak gidin çok**Nesne Gezgini** hello sol bölmede **Bağlan**ve ardından **Veritabanı altyapısı**.) ![TooServer Bağlan][SSMSConnectToServer]</span><span class="sxs-lookup"><span data-stu-id="d20cc-173">(If hello **Connect tooServer** dialog does not appear automatically, navigate too**Object Explorer** in hello left pane, click **Connect**, and then click **Database Engine**.) ![Connect tooServer][SSMSConnectToServer]</span></span>
   
    <span data-ttu-id="d20cc-174">İçin **sunucu türü**, seçin **veritabanı altyapısı**.</span><span class="sxs-lookup"><span data-stu-id="d20cc-174">For **Server type**, choose **Database Engine**.</span></span> <span data-ttu-id="d20cc-175">İçin **sunucu adı**, kullanabileceğiniz **localhost** veya kullanmakta olduğunuz hello bilgisayarın hello adı.</span><span class="sxs-lookup"><span data-stu-id="d20cc-175">For **Server name**, you can use **localhost** or hello name of hello computer that you are using.</span></span> <span data-ttu-id="d20cc-176">Seçin **SQL Server kimlik doğrulaması**ve ardından hello sa kullanıcı adı ve daha önce oluşturduğunuz hello parolayla oturum açın.</span><span class="sxs-lookup"><span data-stu-id="d20cc-176">Choose **SQL Server authentication**, and then log in with hello sa user name and hello password that you created earlier.</span></span>
2. <span data-ttu-id="d20cc-177">SQL Server Management Studio'yu kullanarak yeni bir veritabanı toocreate sağ **veritabanları** , Nesne Gezgini ve ardından **yeni veritabanı**.</span><span class="sxs-lookup"><span data-stu-id="d20cc-177">toocreate a new database by using SQL Server Management Studio, right-click **Databases** in Object Explorer, and then click **New Database**.</span></span>
   
    ![Yeni veritabanı oluştur][SSMScreateNewDB]
3. <span data-ttu-id="d20cc-179">Merhaba, **yeni veritabanı** iletişim kutusunda, MembershipDB için hello veritabanı adı girin ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="d20cc-179">In hello **New Database** dialog, enter MembershipDB for hello database name, and then click **OK**.</span></span>
   
    ![Veritabanı adı girin][SSMSprovideDBname]
   
    <span data-ttu-id="d20cc-181">Herhangi bir değişiklik toohello veritabanı bu noktada yapmayın unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d20cc-181">Note that you do not make any changes toohello database at this point.</span></span> <span data-ttu-id="d20cc-182">çalıştırdığınızda, web uygulamanız tarafından hello üyelik bilgilerini daha sonra otomatik olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="d20cc-182">hello membership information will be added automatically later by your web application when you run it.</span></span>
4. <span data-ttu-id="d20cc-183">Nesne Gezgini'nde, genişletirseniz, **veritabanları**, hello üyelik veritabanının oluşturulan görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="d20cc-183">In Object Explorer, if you expand **Databases**, you will see that hello membership database has been created.</span></span>
   
    ![Oluşturulan MembershipDB][SSMSMembershipDBCreated]

<a name="CreateSite"></a>

## <a name="b-create-a-web-app-in-hello-azure-portal"></a><span data-ttu-id="d20cc-185">B.</span><span class="sxs-lookup"><span data-stu-id="d20cc-185">B.</span></span> <span data-ttu-id="d20cc-186">Hello Azure portalı bir web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="d20cc-186">Create a web app in hello Azure Portal</span></span>
> [!NOTE]
> <span data-ttu-id="d20cc-187">Merhaba toouse Bu öğretici için istediğiniz Azure Portal'ın bir web uygulaması zaten oluşturduysanız, şimdi çok atlayabilirsiniz[karma bağlantı ve bir BizTalk hizmeti oluşturma](#CreateHC) ve buradan devam edin.</span><span class="sxs-lookup"><span data-stu-id="d20cc-187">If you have already created a web app in hello Azure Portal that you want toouse for this tutorial, you can skip ahead too[Create a Hybrid Connection and a BizTalk Service](#CreateHC) and continue from there.</span></span>
> 
> 

1. <span data-ttu-id="d20cc-188">Merhaba, [Azure Portal](https://portal.azure.com), tıklatın **yeni** > **Web + mobil** > **Web uygulaması**.</span><span class="sxs-lookup"><span data-stu-id="d20cc-188">In hello [Azure Portal](https://portal.azure.com), click **New** > **Web + Mobile** > **Web app**.</span></span>
   
    ![Yeni düğmesi][New]
2. <span data-ttu-id="d20cc-190">Web Uygulamanızı yapılandırmak ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="d20cc-190">Configure your web app, and then click **Create**.</span></span>
   
    ![Web sitesi adı][WebsiteCreationBlade]
3. <span data-ttu-id="d20cc-192">Birkaç dakika sonra hello web uygulaması oluşturuldu ve kendi web uygulaması dikey penceresi görünür.</span><span class="sxs-lookup"><span data-stu-id="d20cc-192">After a few moments, hello web app is created and its web app blade appears.</span></span> <span data-ttu-id="d20cc-193">Merhaba dikey web uygulamanızı yönetmenizi sağlayan bir dikey olarak kaydırılabilir Pano ' dir.</span><span class="sxs-lookup"><span data-stu-id="d20cc-193">hello blade is a vertically scrollable dashboard that lets you manage your web app.</span></span>
   
    ![Çalışan Web sitesi][WebSiteRunningBlade]
   
    <span data-ttu-id="d20cc-195">tooverify hello web uygulaması canlı, hello tıklayabilirsiniz **Gözat** simgesi toodisplay hello varsayılan sayfası.</span><span class="sxs-lookup"><span data-stu-id="d20cc-195">tooverify hello web app is live, you can click hello **Browse** icon toodisplay hello default page.</span></span>

<span data-ttu-id="d20cc-196">Ardından, karma bir bağlantı ve BizTalk hizmeti hello web uygulaması için oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d20cc-196">Next, you will create a hybrid connection and a BizTalk service for hello web app.</span></span>

<a name="CreateHC"></a>

## <a name="c-create-a-hybrid-connection-and-a-biztalk-service"></a><span data-ttu-id="d20cc-197">C.</span><span class="sxs-lookup"><span data-stu-id="d20cc-197">C.</span></span> <span data-ttu-id="d20cc-198">Karma bağlantı ve bir BizTalk hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="d20cc-198">Create a Hybrid Connection and a BizTalk Service</span></span>
1. <span data-ttu-id="d20cc-199">Geri toosettings hello Portal, Git ve tıklatın **ağ** > **karma bağlantı uç noktalarınızı yapılandırın**.</span><span class="sxs-lookup"><span data-stu-id="d20cc-199">Back in hello Portal, go toosettings and click **Networking** > **Configure your hybrid connection endpoints**.</span></span>
   
    ![Karma bağlantılar][CreateHCHCIcon]
2. <span data-ttu-id="d20cc-201">Merhaba karma bağlantıları dikey penceresinde **Ekle** > **yeni karma bağlantı**.</span><span class="sxs-lookup"><span data-stu-id="d20cc-201">On hello Hybrid connections blade, click **Add** > **New hybrid connection**.</span></span>
3. <span data-ttu-id="d20cc-202">Merhaba üzerinde **karma bağlantı oluşturmak** dikey penceresinde:</span><span class="sxs-lookup"><span data-stu-id="d20cc-202">On hello **Create hybrid connection** blade:</span></span>
   
   * <span data-ttu-id="d20cc-203">İçin **adı**, hello bağlantı için bir ad sağlayın.</span><span class="sxs-lookup"><span data-stu-id="d20cc-203">For **Name**, provide a name for hello connection.</span></span>
   * <span data-ttu-id="d20cc-204">İçin **ana bilgisayar adı**, SQL Server ana bilgisayarınız hello bilgisayar adını girin.</span><span class="sxs-lookup"><span data-stu-id="d20cc-204">For **Hostname**, enter hello computer name of your SQL Server host computer.</span></span>
   * <span data-ttu-id="d20cc-205">İçin **bağlantı noktası**, 1433 (hello için varsayılan bağlantı noktası SQL Server) girin.</span><span class="sxs-lookup"><span data-stu-id="d20cc-205">For **Port**, enter 1433 (hello default port for SQL Server).</span></span>
   * <span data-ttu-id="d20cc-206">Tıklatın **BizTalk hizmeti** > **yeni BizTalk hizmeti** ve hello BizTalk hizmeti için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="d20cc-206">Click **BizTalk Service** > **New BizTalk Service** and enter a name for hello BizTalk service.</span></span>
     
     ![Karma bağlantı oluşturma][TwinCreateHCBlades]
4. <span data-ttu-id="d20cc-208">Tıklatın **Tamam** iki kez.</span><span class="sxs-lookup"><span data-stu-id="d20cc-208">Click **OK** twice.</span></span>
   
    <span data-ttu-id="d20cc-209">Merhaba işlemi tamamlandığında, hello **bildirimleri** alanı yeşil flash **başarı** ve hello **karma bağlantı** dikey penceresinde hello yeni karma bağlantıyla gösterir Merhaba durumu olarak **bağlı**.</span><span class="sxs-lookup"><span data-stu-id="d20cc-209">When hello process completes, hello **Notifications** area will flash a green **SUCCESS** and hello **Hybrid connection** blade will show hello new hybrid connection with hello status as **Not connected**.</span></span>
   
    ![Oluşturulan bir karma bağlantı][CreateHCOneConnectionCreated]

<span data-ttu-id="d20cc-211">Bu noktada, hello bulut karma bağlantı altyapı önemli bir kısmını tamamladınız.</span><span class="sxs-lookup"><span data-stu-id="d20cc-211">At this point, you have completed an important part of hello cloud hybrid connection infrastructure.</span></span> <span data-ttu-id="d20cc-212">Ardından, karşılık gelen bir şirket içi parça oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d20cc-212">Next, you will create a corresponding on-premises piece.</span></span>

<a name="InstallHCM"></a>

## <a name="d-install-hello-on-premises-hybrid-connection-manager-toocomplete-hello-connection"></a><span data-ttu-id="d20cc-213">D.</span><span class="sxs-lookup"><span data-stu-id="d20cc-213">D.</span></span> <span data-ttu-id="d20cc-214">Merhaba şirket içi karma Bağlantı Yöneticisi toocomplete hello Bağlantısı'nı yükleme</span><span class="sxs-lookup"><span data-stu-id="d20cc-214">Install hello on-premises Hybrid Connection Manager toocomplete hello connection</span></span>
[!INCLUDE [app-service-hybrid-connections-manager-install](../../includes/app-service-hybrid-connections-manager-install.md)]

<span data-ttu-id="d20cc-215">Bu hello karma bağlantı altyapı tamamlandı şimdi kullanan bir web uygulaması oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="d20cc-215">Now that hello hybrid connection infrastructure is complete, you will create a web application that uses it.</span></span>

<a name="CreateASPNET"></a>

## <a name="e-create-a-basic-aspnet-web-project-edit-hello-database-connection-string-and-run-hello-project-locally"></a><span data-ttu-id="d20cc-216">E.</span><span class="sxs-lookup"><span data-stu-id="d20cc-216">E.</span></span> <span data-ttu-id="d20cc-217">Temel bir ASP.NET web projesi oluşturma hello veritabanı bağlantı dizesi düzenleme ve Merhaba projeyi yerel olarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="d20cc-217">Create a basic ASP.NET web project, edit hello database connection string, and run hello project locally</span></span>
### <a name="create-a-basic-aspnet-project"></a><span data-ttu-id="d20cc-218">Temel bir ASP.NET projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="d20cc-218">Create a basic ASP.NET project</span></span>
1. <span data-ttu-id="d20cc-219">Visual Studio'da, hello **dosya** menüsünde yeni bir proje oluşturun:</span><span class="sxs-lookup"><span data-stu-id="d20cc-219">In Visual Studio, on hello **File** menu, create a new Project:</span></span>
   
    ![Yeni Visual Studio projesi][HCVSNewProject]
2. <span data-ttu-id="d20cc-221">Merhaba, **şablonları** hello bölümünü **yeni proje** iletişim kutusunda **Web** ve **ASP.NET Web uygulaması**ve 'ıtıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="d20cc-221">In hello **Templates** section of hello **New Project** dialog, select **Web** and choose **ASP.NET Web Application**, and then click **OK**.</span></span>
   
    ![ASP.NET Web uygulaması seçin][HCVSChooseASPNET]
3. <span data-ttu-id="d20cc-223">Merhaba, **yeni ASP.NET projesi** iletişim kutusunda, seçin **MVC**ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="d20cc-223">In hello **New ASP.NET Project** dialog, choose **MVC**, and then click **OK**.</span></span>
   
    ![MVC seçin][HCVSChooseMVC]
4. <span data-ttu-id="d20cc-225">Başlangıç projesi oluşturduğunuzda hello uygulama Benioku sayfası görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="d20cc-225">When hello project has been created, hello application readme page appears.</span></span> <span data-ttu-id="d20cc-226">Merhaba web projesi henüz çalıştırmayın.</span><span class="sxs-lookup"><span data-stu-id="d20cc-226">Do not run hello web project yet.</span></span>
   
    ![Benioku sayfası][HCVSReadmePage]

### <a name="edit-hello-database-connection-string-for-hello-application"></a><span data-ttu-id="d20cc-228">Merhaba uygulaması için Hello veritabanı bağlantı dizesini Düzenle</span><span class="sxs-lookup"><span data-stu-id="d20cc-228">Edit hello database connection string for hello application</span></span>
<span data-ttu-id="d20cc-229">Bu adımda, uygulamanızın söyler hello bağlantı dizesini Düzenle nerede toofind yerel SQL Server Express veritabanı.</span><span class="sxs-lookup"><span data-stu-id="d20cc-229">In this step, you edit hello connection string that tells your application where toofind your local SQL Server Express database.</span></span> <span data-ttu-id="d20cc-230">Merhaba uygulaması için yapılandırma bilgilerini içeren hello uygulamanın Web.config dosyasında Hello bağlantı dizesi değil.</span><span class="sxs-lookup"><span data-stu-id="d20cc-230">hello connection string is in hello application's Web.config file, which contains configuration information for hello application.</span></span>

> [!NOTE]
> <span data-ttu-id="d20cc-231">SQL Server Express ve değil hello bir LocalDB Visual Studio'nun varsayılan oluşturduğunuz hello veritabanı uygulamanızın kullandığı tooensure, projenizin çalıştırmadan önce bu adımı tamamlamak önemlidir.</span><span class="sxs-lookup"><span data-stu-id="d20cc-231">tooensure that your application uses hello database that you created in SQL Server Express, and not hello one in Visual Studio's default LocalDB, it is important that you complete this step before running your project.</span></span>
> 
> 

1. <span data-ttu-id="d20cc-232">Çözüm Gezgini'nde hello Web.config dosyasına çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d20cc-232">In Solution Explorer, double-click hello Web.config file.</span></span>
   
    ![Web.config][HCVSChooseWebConfig]
2. <span data-ttu-id="d20cc-234">Merhaba Düzenle **connectionStrings** bölüm toopoint toohello SQL Server veritabanı örneği aşağıdaki hello hello dizimini izleyerek, yerel makinenizde:</span><span class="sxs-lookup"><span data-stu-id="d20cc-234">Edit hello **connectionStrings** section toopoint toohello SQL Server database on your local machine, following hello syntax in hello following example:</span></span>
   
    ![Bağlantı dizesi][HCVSConnectionString]
   
    <span data-ttu-id="d20cc-236">Merhaba bağlantı dizesi oluştururken hello aşağıdakileri göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="d20cc-236">When composing hello connection string, keep in mind hello following:</span></span>
   
   * <span data-ttu-id="d20cc-237">Adlandırılmış örneği varsayılan örnek (örneğin, Sunucunuz\\sqlexpress) yerine tooa bağlanıyorsanız, SQL Server toouse statik bağlantı noktalarını yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d20cc-237">If you are connecting tooa named instance instead of a default instance (for example, YourServer\SQLEXPRESS), you must configure your SQL Server toouse static ports.</span></span> <span data-ttu-id="d20cc-238">Statik bağlantı noktalarını yapılandırma hakkında daha fazla bilgi için bkz: [nasıl tooconfigure SQL Server toolisten belirli bir bağlantı noktası](http://support.microsoft.com/kb/823938).</span><span class="sxs-lookup"><span data-stu-id="d20cc-238">For information on configuring static ports, see [How tooconfigure SQL Server toolisten on a specific port](http://support.microsoft.com/kb/823938).</span></span> <span data-ttu-id="d20cc-239">Varsayılan olarak, adlandırılmış örnekleri UDP ve karma bağlantılar tarafından desteklenmeyen dinamik bağlantı noktaları kullanır.</span><span class="sxs-lookup"><span data-stu-id="d20cc-239">By default, named instances use UDP and dynamic ports, which are not supported by Hybrid Connections.</span></span>
   * <span data-ttu-id="d20cc-240">Merhaba belirtmeniz önerilir (Merhaba örnekte gösterildiği gibi varsayılan 1433) hello bağlantı dizesine bağlantı noktası, bu yerel SQL Server'ınızdaki sahip etkin TCP ve hello doğru bağlantı noktasını kullanarak emin olabilir.</span><span class="sxs-lookup"><span data-stu-id="d20cc-240">It is recommended that you specify hello port (1433 by default, as shown in hello example) on hello connection string so that you can be sure that your local SQL Server has TCP enabled and is using hello correct port.</span></span>
   * <span data-ttu-id="d20cc-241">Bağlantı dizenizi Hello kullanıcı kimliği ve parola belirterek toouse SQL Server kimlik doğrulaması tooconnect unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d20cc-241">Remember toouse SQL Server Authentication tooconnect, specifying hello user ID and password in your connection string.</span></span>
3. <span data-ttu-id="d20cc-242">Tıklatın **kaydetmek** Visual Studio toosave hello Web.config dosyasında.</span><span class="sxs-lookup"><span data-stu-id="d20cc-242">Click **Save** in Visual Studio toosave hello Web.config file.</span></span>

### <a name="run-hello-project-locally-and-register-a-new-user"></a><span data-ttu-id="d20cc-243">Merhaba projeyi yerel olarak çalıştırın ve yeni bir kullanıcı kaydı</span><span class="sxs-lookup"><span data-stu-id="d20cc-243">Run hello project locally and register a new user</span></span>
1. <span data-ttu-id="d20cc-244">Şimdi, yeni web projeniz yerel olarak hata ayıklama altında hello Gözat düğmesine tıklayarak çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="d20cc-244">Now, run your new web project locally by clicking hello browse button under Debug.</span></span> <span data-ttu-id="d20cc-245">Bu örnek, Internet Explorer kullanır.</span><span class="sxs-lookup"><span data-stu-id="d20cc-245">This example uses Internet Explorer.</span></span>
   
    ![Projeyi çalıştırın][HCVSRunProject]
2. <span data-ttu-id="d20cc-247">Merhaba sağ üst köşesinde hello varsayılan web sayfası üzerinde seçin **kaydetmek** tooregister yeni bir hesap:</span><span class="sxs-lookup"><span data-stu-id="d20cc-247">On hello upper right of hello default web page, choose **Register** tooregister a new account:</span></span>
   
    ![Yeni bir hesap Kaydet][HCVSRegisterLocally]
3. <span data-ttu-id="d20cc-249">Bir kullanıcı adı ve parola girin:</span><span class="sxs-lookup"><span data-stu-id="d20cc-249">Enter a user name and password:</span></span>
   
    ![Kullanıcı adı ve parola girin][HCVSCreateNewAccount]
   
    <span data-ttu-id="d20cc-251">Bu otomatik olarak bir veritabanı uygulamanız için hello üyelik bilgilerini tutan yerel SQL Server üzerinde oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d20cc-251">This automatically creates a database on your local SQL Server that holds hello membership information for your application.</span></span> <span data-ttu-id="d20cc-252">Merhaba tablolardan biri (**dbo. AspNetUsers**) ayrı tutma web girdiğiniz olanları hello gibi uygulama kullanıcı kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="d20cc-252">One of hello tables (**dbo.AspNetUsers**) holds web app user credentials like hello ones that you just entered.</span></span> <span data-ttu-id="d20cc-253">Bu tablo daha sonra hello öğreticide görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="d20cc-253">You will see this table later in hello tutorial.</span></span>
4. <span data-ttu-id="d20cc-254">Merhaba varsayılan web sayfasının Hello tarayıcı penceresini kapatın.</span><span class="sxs-lookup"><span data-stu-id="d20cc-254">Close hello browser window of hello default web page.</span></span> <span data-ttu-id="d20cc-255">Visual Studio'da hello durdurur.</span><span class="sxs-lookup"><span data-stu-id="d20cc-255">This stops hello application in Visual Studio.</span></span>

<span data-ttu-id="d20cc-256">Şimdi toopublish hello uygulama tooAzure olan hello sonraki adım için hazır ve test.</span><span class="sxs-lookup"><span data-stu-id="d20cc-256">You are now ready for hello next step, which is toopublish hello application tooAzure and test it.</span></span>

<a name="PubNTest"></a>

## <a name="f-publish-hello-web-application-tooazure-and-test-it"></a><span data-ttu-id="d20cc-257">F</span><span class="sxs-lookup"><span data-stu-id="d20cc-257">F.</span></span> <span data-ttu-id="d20cc-258">Yayımlama Hello web uygulama tooAzure ve test</span><span class="sxs-lookup"><span data-stu-id="d20cc-258">Publish hello web application tooAzure and test it</span></span>
<span data-ttu-id="d20cc-259">Şimdi,, uygulama tooyour App Service web uygulaması yayımlama ve nasıl daha önce yapılandırdığınız hello karma bağlantıdır toosee test web uygulama toohello veritabanınızı yerel makinenizde kullanılan tooconnect bırakılıyor.</span><span class="sxs-lookup"><span data-stu-id="d20cc-259">Now, you'll publish your application tooyour App Service web app and then test it toosee how hello hybrid connection you configured earlier is being used tooconnect your web app toohello database on your local machine.</span></span>

### <a name="publish-hello-web-application"></a><span data-ttu-id="d20cc-260">Merhaba web uygulaması yayımlama</span><span class="sxs-lookup"><span data-stu-id="d20cc-260">Publish hello web application</span></span>
1. <span data-ttu-id="d20cc-261">Yayımlama profilinizi hello hello Azure Portal, App Service web uygulaması için yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d20cc-261">You can download your publishing profile for hello App Service web app in hello Azure Portal.</span></span> <span data-ttu-id="d20cc-262">Web uygulamanız için Hello dikey penceresinde **Get yayımlama profili**ve ardından hello dosya tooyour bilgisayara kaydedin.</span><span class="sxs-lookup"><span data-stu-id="d20cc-262">On hello blade for your web app, click **Get publish profile**, and then save hello file tooyour computer.</span></span>
   
    ![Yayım profili indirin][PortalDownloadPublishProfile]
   
    <span data-ttu-id="d20cc-264">Ardından, Visual Studio web uygulamanıza bu dosyayı içeri aktaracak.</span><span class="sxs-lookup"><span data-stu-id="d20cc-264">Next, you will import this file into your Visual Studio web application.</span></span>
2. <span data-ttu-id="d20cc-265">Visual Studio'da hello Çözüm Gezgini'nde proje adına sağ tıklayın ve seçin **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="d20cc-265">In Visual Studio, right-click hello project name in Solution Explorer and select **Publish**.</span></span>
   
    ![Select yayımlama][HCVSRightClickProjectSelectPublish]
3. <span data-ttu-id="d20cc-267">Merhaba, **Web'i Yayımla** iletişim kutusunda, hello **profil** sekmesinde, seçin **alma**.</span><span class="sxs-lookup"><span data-stu-id="d20cc-267">In hello **Publish Web** dialog, on hello **Profile** tab, choose **Import**.</span></span>
   
    ![İçeri Aktarma][HCVSPublishWebDialogImport]
4. <span data-ttu-id="d20cc-269">Gözat tooyour indirdiğiniz yayımlama profili, onu seçin ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="d20cc-269">Browse tooyour downloaded publishing profile, select it, and then click **OK**.</span></span>
   
    ![Tooprofile Gözat][HCVSBrowseToImportPubProfile]
5. <span data-ttu-id="d20cc-271">Yayımlama bilgilerinizi içe aktarılır ve üzerinde hello görüntüler **bağlantı** hello iletişim sekmesinde.</span><span class="sxs-lookup"><span data-stu-id="d20cc-271">Your publishing information is imported and displays on hello **Connection** tab of hello dialog.</span></span>
   
    ![Yayınla'yı tıklatın][HCVSClickPublish]
   
    <span data-ttu-id="d20cc-273">**Yayımla**’ta tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d20cc-273">Click **Publish**.</span></span>
   
    <span data-ttu-id="d20cc-274">Yayımlama tamamlandıktan sonra tarayıcınızı başlatın ve şimdi hello Azure bulut dinamik olması dışında şimdi bilinen ASP.NET uygulamanızın--Göster!</span><span class="sxs-lookup"><span data-stu-id="d20cc-274">When publishing completes, your browser will launch and show your now familiar ASP.NET application -- except that now it is live in hello Azure cloud!</span></span>

<span data-ttu-id="d20cc-275">Ardından, canlı web uygulama toosee eylemde karma bağlantısını kullanır.</span><span class="sxs-lookup"><span data-stu-id="d20cc-275">Next, you will use your live web application toosee its Hybrid Connection in action.</span></span>

### <a name="test-hello-completed-web-application-on-azure"></a><span data-ttu-id="d20cc-276">Azure web uygulamasına test hello tamamlandı</span><span class="sxs-lookup"><span data-stu-id="d20cc-276">Test hello completed web application on Azure</span></span>
1. <span data-ttu-id="d20cc-277">Merhaba üstte, web sayfasının sağ Azure üzerinde seçin **oturum**.</span><span class="sxs-lookup"><span data-stu-id="d20cc-277">On hello top right of your web page on Azure, choose **Log in**.</span></span>
   
    ![Test oturum açma][HCTestLogIn]
2. <span data-ttu-id="d20cc-279">Web uygulaması sunulmuştur uygulama hizmetiniz tooyour web uygulamasının üyelik veritabanının yerel makinenizde bağlı.</span><span class="sxs-lookup"><span data-stu-id="d20cc-279">Your App Service web app is now connected tooyour web application's membership database on your local machine.</span></span> <span data-ttu-id="d20cc-280">tooverify hello hello yerel girdiğiniz aynı kimlik bilgileri veritabanına daha önce bu, oturum.</span><span class="sxs-lookup"><span data-stu-id="d20cc-280">tooverify this, log in with hello same credentials that you entered in hello local database earlier.</span></span>
   
    ![Merhaba Karşılama][HCTestHelloContoso]
3. <span data-ttu-id="d20cc-282">toofurther yeni karma bağlantınız sınamak için Azure web uygulamanızın dışına oturum ve başka bir kullanıcı olarak kaydedin.</span><span class="sxs-lookup"><span data-stu-id="d20cc-282">toofurther test your new hybrid connection, log off of your Azure web application and register as another user.</span></span> <span data-ttu-id="d20cc-283">Yeni bir kullanıcı adı ve parolasını girin ve ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="d20cc-283">Provide a new user name and password, and then click **Register**.</span></span>
   
    ![Test başka bir kullanıcı kaydetme][HCTestRegisterRelecloud]
4. <span data-ttu-id="d20cc-285">Merhaba yeni kullanıcının kimlik bilgilerini yerel veritabanınızda karma bağlantınız üzerinden depolanmıştı tooverify, yerel bilgisayarınızda SQL Management Studio'yu açın.</span><span class="sxs-lookup"><span data-stu-id="d20cc-285">tooverify that hello new user's credentials have been stored in your local database through your hybrid connection, open SQL Management Studio on your local computer.</span></span> <span data-ttu-id="d20cc-286">Merhaba, nesne Gezgini'nde genişletin **MembershipDB** veritabanı ve ardından **tabloları**.</span><span class="sxs-lookup"><span data-stu-id="d20cc-286">In Object Explorer, expand hello **MembershipDB** database, and then expand **Tables**.</span></span> <span data-ttu-id="d20cc-287">Sağ hello **dbo. AspNetUsers** üyelik tablosunda ve seçin **ilk 1000 satırı Seç** tooview hello sonuçları.</span><span class="sxs-lookup"><span data-stu-id="d20cc-287">Right-click hello **dbo.AspNetUsers** membership table and choose **Select Top 1000 Rows** tooview hello results.</span></span>
   
    ![Merhaba sonuçları görüntüleme][HCTestSSMSTree]
5. <span data-ttu-id="d20cc-289">Yerel üyelik tablonuz şimdi her iki hesap - yerel olarak oluşturulmuş bir hello ve hello hello Azure bulut oluşturulmuş bir gösterir.</span><span class="sxs-lookup"><span data-stu-id="d20cc-289">Your local membership table now shows both accounts - hello one that you created locally, and hello one that you created in hello Azure cloud.</span></span> <span data-ttu-id="d20cc-290">Merhaba bulutta oluşturulmuş bir Hello Azure'nın karma bağlantı özelliği aracılığıyla tooyour şirket içi veritabanına kaydedildi.</span><span class="sxs-lookup"><span data-stu-id="d20cc-290">hello one that you created in hello cloud has been saved tooyour on-premises database through Azure's Hybrid Connection feature.</span></span>
   
    ![Şirket içi veritabanında kayıtlı kullanıcılar][HCTestShowMemberDb]

<span data-ttu-id="d20cc-292">Artık oluşturduğunuz ve bir web uygulamasını hello Azure Bulut ve şirket içi SQL Server veritabanı arasında bir karma bağlantı kullanan bir ASP.NET web uygulaması dağıtılmış.</span><span class="sxs-lookup"><span data-stu-id="d20cc-292">You have now created and deployed an ASP.NET web application that uses a hybrid connection between a web app in hello Azure cloud and an on-premises SQL Server database.</span></span> <span data-ttu-id="d20cc-293">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="d20cc-293">Congratulations!</span></span>

## <a name="see-also"></a><span data-ttu-id="d20cc-294">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="d20cc-294">See Also</span></span>
[<span data-ttu-id="d20cc-295">Karma Bağlantılara genel bakış</span><span class="sxs-lookup"><span data-stu-id="d20cc-295">Hybrid Connections overview</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=397274)

[<span data-ttu-id="d20cc-296">Karma bağlantılar (Channel 9 video) Josh geçiş sunar</span><span class="sxs-lookup"><span data-stu-id="d20cc-296">Josh Twist introduces hybrid connections (Channel 9 video)</span></span>](http://channel9.msdn.com/Shows/Azure-Friday/Josh-Twist-introduces-hybrid-connections)

[<span data-ttu-id="d20cc-297">Karma Bağlantılara genel bakış</span><span class="sxs-lookup"><span data-stu-id="d20cc-297">Hybrid Connections overview</span></span>](/services/biztalk-services/)

[<span data-ttu-id="d20cc-298">BizTalk Services: Pano, İzleyici, Ölçek, yapılandırma ve karma bağlantı sekmeleri</span><span class="sxs-lookup"><span data-stu-id="d20cc-298">BizTalk Services: Dashboard, Monitor, Scale, Configure, and Hybrid Connection tabs</span></span>](../biztalk-services/biztalk-dashboard-monitor-scale-tabs.md)

[<span data-ttu-id="d20cc-299">Gerçek dünya karma bir buluta sorunsuz uygulama taşıma (Channel 9 video) ile oluşturma</span><span class="sxs-lookup"><span data-stu-id="d20cc-299">Building a Real-World Hybrid Cloud with Seamless Application Portability (Channel 9 video)</span></span>](http://channel9.msdn.com/events/TechEd/NorthAmerica/2014/DCIM-B323#fbid=)

[<span data-ttu-id="d20cc-300">Azure App Service içinde karma bağlantılar kullanarak şirket kaynaklarına erişmek</span><span class="sxs-lookup"><span data-stu-id="d20cc-300">Access on-premises resources using hybrid connections in Azure App Service</span></span>](web-sites-hybrid-connection-get-started.md)

[<span data-ttu-id="d20cc-301">ASP.NET Kimliği'ne genel bakış</span><span class="sxs-lookup"><span data-stu-id="d20cc-301">ASP.NET Identity Overview</span></span>](http://www.asp.net/identity)

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

<!-- IMAGES -->
[SQLServerInstall]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A01SQLServerInstall.png
[ChooseDefaultInstance]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A02ChooseDefaultInstance.png
[ChooseMixedMode]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A03ChooseMixedMode.png
[SSMSConnectToServer]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A04SSMSConnectToServer.png
[SSMScreateNewDB]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A05SSMScreateNewDBlh.png
[SSMSprovideDBname]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A06SSMSprovideDBname.png
[SSMSMembershipDBCreated]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A07SSMSMembershipDBCreated.png
[New]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B01New.png
[NewWebsite]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B02NewWebsite.png
[WebsiteCreationBlade]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B03WebsiteCreationBlade.png
[WebSiteRunningBlade]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B04WebSiteRunningBlade.png
[Browse]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B05Browse.png
[DefaultWebSitePage]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B06DefaultWebSitePage.png
[CreateHCHCIcon]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C01CreateHCHCIcon.png
[CreateHCAddHC]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C02CreateHCAddHC.png
[TwinCreateHCBlades]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C03TwinCreateHCBlades.png
[CreateHCCreateBTS]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C04CreateHCCreateBTS.png
[CreateBTScomplete]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C05CreateBTScomplete.png
[CreateHCSuccessNotification]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C06CreateHCSuccessNotification.png
[CreateHCOneConnectionCreated]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C07CreateHCOneConnectionCreated.png
[HCIcon]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D01HCIcon.png
[NotConnected]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D02NotConnected.png
[NotConnectedBlade]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D03NotConnectedBlade.png
[ClickListenerSetup]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D04ClickListenerSetup.png
[ClickToInstallHCM]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D05ClickToInstallHCM.png
[ApplicationRunWarning]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D06ApplicationRunWarning.png
[UAC]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D07UAC.png
[HCMInstalling]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D08HCMInstalling.png
[HCMInstallComplete]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D09HCMInstallComplete.png
[HCStatusConnected]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D10HCStatusConnected.png
[HCVSNewProject]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E01HCVSNewProject.png
[HCVSChooseASPNET]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E02HCVSChooseASPNET.png
[HCVSChooseMVC]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E03HCVSChooseMVC.png
[HCVSReadmePage]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E04HCVSReadmePage.png
[HCVSChooseWebConfig]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E05HCVSChooseWebConfig.png
[HCVSConnectionString]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E06HCVSConnectionString.png
[HCVSRunProject]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E06HCVSRunProject.png
[HCVSRegisterLocally]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E07HCVSRegisterLocally.png
[HCVSCreateNewAccount]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E08HCVSCreateNewAccount.png
[PortalDownloadPublishProfile]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F01PortalDownloadPublishProfile.png
[HCVSPublishProfileInDownloadsFolder]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F02HCVSPublishProfileInDownloadsFolder.png
[HCVSRightClickProjectSelectPublish]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F03HCVSRightClickProjectSelectPublish.png
[HCVSPublishWebDialogImport]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F04HCVSPublishWebDialogImport.png
[HCVSBrowseToImportPubProfile]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F05HCVSBrowseToImportPubProfile.png
[HCVSClickPublish]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F06HCVSClickPublish.png
[HCTestLogIn]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F07HCTestLogIn.png
[HCTestHelloContoso]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F08HCTestHelloContoso.png
[HCTestRegisterRelecloud]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F09HCTestRegisterRelecloud.png
[HCTestSSMSTree]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F10HCTestSSMSTree.png
[HCTestShowMemberDb]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F11HCTestShowMemberDb.png
