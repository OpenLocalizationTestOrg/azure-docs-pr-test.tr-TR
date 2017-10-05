---
title: "Karma bağlantılar kullanarak Azure App Service web uygulamasından şirket içi SQL Server'a bağlanma"
description: "Microsoft Azure üzerinde bir web uygulaması oluşturma ve bir şirket içi SQL Server veritabanına bağlan"
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
ms.openlocfilehash: 12456ef3e2aecfa7a03cca97de2ff6ffd9602357
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-on-premises-sql-server-from-a-web-app-in-azure-app-service-using-hybrid-connections"></a><span data-ttu-id="772ab-103">Karma bağlantılar kullanarak Azure App Service web uygulamasından şirket içi SQL Server'a bağlanma</span><span class="sxs-lookup"><span data-stu-id="772ab-103">Connect to on-premises SQL Server from a web app in Azure App Service using Hybrid Connections</span></span>
<span data-ttu-id="772ab-104">Karma bağlantılar bağlanabilir [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web uygulamaları için statik bir TCP bağlantı noktası kullanan şirket içi kaynakları.</span><span class="sxs-lookup"><span data-stu-id="772ab-104">Hybrid Connections can connect [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps to on-premises resources that use a static TCP port.</span></span> <span data-ttu-id="772ab-105">Desteklenen kaynaklar Microsoft SQL Server, MySQL, HTTP Web API'leri, uygulama hizmeti ve birçok özel Web hizmeti içerir.</span><span class="sxs-lookup"><span data-stu-id="772ab-105">Supported resources include Microsoft SQL Server, MySQL, HTTP Web APIs, App Service, and most custom Web Services.</span></span>

<span data-ttu-id="772ab-106">Bu öğreticide, bir App Service web uygulamasının nasıl oluşturulacağını öğreneceksiniz [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715), web uygulamasının yeni karma bağlantı özelliğini kullanarak, yerel şirket içi SQL Server veritabanına bağlanmak, karma bağlantıyı kullan ve App Service web uygulaması uygulamayı dağıtmak basit bir ASP.NET uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="772ab-106">In this tutorial, you will learn how to create an App Service web app in the [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715), connect the web app to your local on-premises SQL Server database using the new Hybrid Connection feature, create a simple ASP.NET application that will use the hybrid connection, and deploy the application to the App Service web app.</span></span> <span data-ttu-id="772ab-107">Azure tamamlanan web uygulamasında kullanıcı kimlik bilgilerini şirket içi bir üyelik veritabanında depolar.</span><span class="sxs-lookup"><span data-stu-id="772ab-107">The completed web app on Azure stores user credentials in a membership database that is on-premises.</span></span> <span data-ttu-id="772ab-108">Öğretici, Azure veya ASP.NET kullanma konusunda deneyim varsayar.</span><span class="sxs-lookup"><span data-stu-id="772ab-108">The tutorial assumes no prior experience using Azure or ASP.NET.</span></span>

> [!NOTE]
> <span data-ttu-id="772ab-109">Azure hesabı için kaydolmadan önce Azure App Service’i kullanmaya başlamak isterseniz, App Service’te hemen kısa süreli bir başlangıç web uygulaması oluşturabileceğiniz [App Service’i Deneyin](https://azure.microsoft.com/try/app-service/) sayfasına gidin.</span><span class="sxs-lookup"><span data-stu-id="772ab-109">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="772ab-110">Kredi kartı ve taahhüt gerekmez.</span><span class="sxs-lookup"><span data-stu-id="772ab-110">No credit cards required; no commitments.</span></span>
> 
> <span data-ttu-id="772ab-111">Web uygulamalarının karma bağlantılar özelliği yalnızca bölümüdür [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="772ab-111">The Web Apps portion of the Hybrid Connections feature is available only in the [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="772ab-112">BizTalk Services'da bir bağlantı oluşturmak için bkz: [karma bağlantılar](http://go.microsoft.com/fwlink/p/?LinkID=397274).</span><span class="sxs-lookup"><span data-stu-id="772ab-112">To create a connection in BizTalk Services, see [Hybrid Connections](http://go.microsoft.com/fwlink/p/?LinkID=397274).</span></span>  
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="772ab-113">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="772ab-113">Prerequisites</span></span>
<span data-ttu-id="772ab-114">Bu öğreticiyi tamamlamak için aşağıdaki ürünler gerekir.</span><span class="sxs-lookup"><span data-stu-id="772ab-114">To complete this tutorial, you'll need the following products.</span></span> <span data-ttu-id="772ab-115">Azure için tamamen ücretsiz geliştirme başlatabilmeniz tüm boş sürümlerinde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="772ab-115">All are available in free versions, so you can start developing for Azure entirely for free.</span></span>

* <span data-ttu-id="772ab-116">**Azure aboneliği** - ücretsiz bir abonelik için bkz: [Azure ücretsiz deneme sürümü](/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="772ab-116">**Azure subscription** - For a free subscription, see [Azure Free Trial](/pricing/free-trial/).</span></span>
* <span data-ttu-id="772ab-117">**Visual Studio 2013** - Visual Studio 2013 ücretsiz bir deneme sürümünü karşıdan yüklemek için bkz: [Visual Studio indirmeleri](http://www.visualstudio.com/downloads/download-visual-studio-vs).</span><span class="sxs-lookup"><span data-stu-id="772ab-117">**Visual Studio 2013** - To download a free trial version of Visual Studio 2013, see [Visual Studio Downloads](http://www.visualstudio.com/downloads/download-visual-studio-vs).</span></span> <span data-ttu-id="772ab-118">Bu, devam etmeden önce yükleyin.</span><span class="sxs-lookup"><span data-stu-id="772ab-118">Install this before continuing.</span></span>
* <span data-ttu-id="772ab-119">**Microsoft .NET Framework 3.5 Service Pack 1** -işletim sisteminiz Windows 8.1, Windows Server 2012 R2, Windows 8, Windows Server 2012, Windows 7 veya Windows Server 2008 R2 ise, bu Denetim Masası'nda etkinleştirebilirsiniz > Programlar ve Özellikler > kapatma Windows özelliklerini aç veya kapat.</span><span class="sxs-lookup"><span data-stu-id="772ab-119">**Microsoft .NET Framework 3.5 Service Pack 1** - If your operating system is Windows 8.1, Windows Server 2012 R2, Windows 8, Windows Server 2012, Windows 7, or Windows Server 2008 R2, you can enable this in Control Panel > Programs and Features > Turn Windows features on or off.</span></span> <span data-ttu-id="772ab-120">Aksi takdirde, buradan indirebilirsiniz [Microsoft Download Center](http://www.microsoft.com/download/en/details.aspx?displaylang=en&id=22).</span><span class="sxs-lookup"><span data-stu-id="772ab-120">Otherwise, you can download it from the [Microsoft Download Center](http://www.microsoft.com/download/en/details.aspx?displaylang=en&id=22).</span></span>
* <span data-ttu-id="772ab-121">**SQL Server 2014 Express araçları ile** -Microsoft SQL Server Express, ücretsiz indirme [Microsoft Web Platformu veritabanı sayfası](http://www.microsoft.com/web/platform/database.aspx).</span><span class="sxs-lookup"><span data-stu-id="772ab-121">**SQL Server 2014 Express with Tools** - download Microsoft SQL Server Express for free at the [Microsoft Web Platform Database page](http://www.microsoft.com/web/platform/database.aspx).</span></span> <span data-ttu-id="772ab-122">Seçin **Express** (yerel veritabanı değil) sürümü.</span><span class="sxs-lookup"><span data-stu-id="772ab-122">Choose the **Express** (not LocalDB) version.</span></span> <span data-ttu-id="772ab-123">**Araçlarıyla Express** sürüm, bu öğreticide kullanacağı SQL Server Management Studio içerir.</span><span class="sxs-lookup"><span data-stu-id="772ab-123">The **Express with Tools** version includes SQL Server Management Studio, which you will use in this tutorial.</span></span>
* <span data-ttu-id="772ab-124">**SQL Server Management Studio Express** - yukarıda belirtilen araçları indirme ile SQL Server 2014 Express ile dahil, ancak ayrı olarak yüklemeniz gerekiyorsa, indirin ve şuradan yükleyin [SQL Server Express indirme sayfası](http://www.microsoft.com/web/platform/database.aspx).</span><span class="sxs-lookup"><span data-stu-id="772ab-124">**SQL Server Management Studio Express** - This is included with the SQL Server 2014 Express with Tools download mentioned above, but if you need to install it separately, you can download and install it from the [SQL Server Express download page](http://www.microsoft.com/web/platform/database.aspx).</span></span>

<span data-ttu-id="772ab-125">Öğretici, Visual Studio 2013 yüklediyseniz ve yüklenmemiş veya .NET Framework 3.5 etkin bir Azure aboneliğine sahip olduğunuzu varsayar.</span><span class="sxs-lookup"><span data-stu-id="772ab-125">The tutorial assumes that you have an Azure subscription, that you have installed Visual Studio 2013, and that you have installed or enabled .NET Framework 3.5.</span></span> <span data-ttu-id="772ab-126">Öğretici Azure karma bağlantılar özelliği (varsayılan bir örnek ile statik bir TCP bağlantı noktası) ile iyi çalışır bir yapılandırmasında SQL Server 2014 Express yükleme gösterir.</span><span class="sxs-lookup"><span data-stu-id="772ab-126">The tutorial shows you how to install SQL Server 2014 Express in a configuration that works well with the Azure Hybrid Connections feature (a default instance with a static TCP port).</span></span> <span data-ttu-id="772ab-127">Öğretici başlamadan önce SQL Server 2014 Express araçları ile SQL Server yüklü yoksa, yukarıda belirtilen konumdan indirin.</span><span class="sxs-lookup"><span data-stu-id="772ab-127">Before starting the tutorial, download SQL Server 2014 Express with Tools from the location mentioned above if you do not have SQL Server installed.</span></span>

### <a name="notes"></a><span data-ttu-id="772ab-128">Notlar</span><span class="sxs-lookup"><span data-stu-id="772ab-128">Notes</span></span>
<span data-ttu-id="772ab-129">Bir şirket içi SQL Server veya SQL Server Express veritabanı ile karma bağlantı kullanmak için TCP/IP'yi statik bağlantı noktasına etkinleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="772ab-129">To use an on-premises SQL Server or SQL Server Express database with a hybrid connection, TCP/IP needs to be enabled on a static port.</span></span> <span data-ttu-id="772ab-130">Adlandırılmış örneklerin yapılamaz SQL Server'da varsayılan örnekleri statik bağlantı noktası 1433 kullanın.</span><span class="sxs-lookup"><span data-stu-id="772ab-130">Default instances on SQL Server use static port 1433, whereas named instances do not.</span></span>

<span data-ttu-id="772ab-131">Şirket içi karma Bağlantı Yöneticisi Aracı yüklediğiniz bilgisayar:</span><span class="sxs-lookup"><span data-stu-id="772ab-131">The computer on which you install the on-premises Hybrid Connection Manager agent:</span></span>

* <span data-ttu-id="772ab-132">Azure giden bağlantısı üzerinden olması gerekir:</span><span class="sxs-lookup"><span data-stu-id="772ab-132">Must have outbound connectivity to Azure over:</span></span>

| <span data-ttu-id="772ab-133">Bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="772ab-133">Port</span></span> | <span data-ttu-id="772ab-134">Neden</span><span class="sxs-lookup"><span data-stu-id="772ab-134">Why</span></span> |
| --- | --- |
| <span data-ttu-id="772ab-135">80</span><span class="sxs-lookup"><span data-stu-id="772ab-135">80</span></span> |<span data-ttu-id="772ab-136">**Gerekli** sertifika doğrulama ve isteğe bağlı olarak veri bağlantısı için HTTP bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="772ab-136">**Required** for HTTP port for certificate validation and optionally for data connectivity.</span></span> |
| <span data-ttu-id="772ab-137">443</span><span class="sxs-lookup"><span data-stu-id="772ab-137">443</span></span> |<span data-ttu-id="772ab-138">**İsteğe bağlı** veri bağlantısı için.</span><span class="sxs-lookup"><span data-stu-id="772ab-138">**Optional** for data connectivity.</span></span> <span data-ttu-id="772ab-139">TCP bağlantı noktası 80, 443 giden bağlantı kullanılamıyorsa, kullanılır.</span><span class="sxs-lookup"><span data-stu-id="772ab-139">If outbound connectivity to 443 is unavailable, TCP port 80 is used.</span></span> |
| <span data-ttu-id="772ab-140">5671 ve 9352</span><span class="sxs-lookup"><span data-stu-id="772ab-140">5671 and 9352</span></span> |<span data-ttu-id="772ab-141">**Önerilen** ancak veri bağlantısı için isteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="772ab-141">**Recommended** but Optional for data connectivity.</span></span> <span data-ttu-id="772ab-142">Bu mod genellikle daha yüksek verimlilik verir unutmayın.</span><span class="sxs-lookup"><span data-stu-id="772ab-142">Note this mode usually yields higher throughput.</span></span> <span data-ttu-id="772ab-143">Bu bağlantı noktalarına giden bağlantı kullanılamıyorsa, TCP bağlantı noktası 443 kullanılır.</span><span class="sxs-lookup"><span data-stu-id="772ab-143">If outbound connectivity to these ports is unavailable, TCP port 443 is used.</span></span> |

* <span data-ttu-id="772ab-144">Ulaşabilmesi olmalıdır *ana bilgisayar adı*:*BağlantıNoktasıNumarası* , şirket içi kaynak.</span><span class="sxs-lookup"><span data-stu-id="772ab-144">Must be able to reach the *hostname*:*portnumber* of your on-premises resource.</span></span>

<span data-ttu-id="772ab-145">Bu makaledeki adımları, şirket içi karma Bağlantı Aracısı'nı barındıracak bilgisayarı tarayıcıdan kullandığınızı varsayar.</span><span class="sxs-lookup"><span data-stu-id="772ab-145">The steps in this article assume that you are using the browser from the computer that will host the on-premises hybrid connection agent.</span></span>

<span data-ttu-id="772ab-146">Bir yapılandırma ve yukarıda açıklanan koşullara uyan bir ortamda yüklü SQL Server zaten varsa, İleri atlayabilirsiniz ve başlayın [şirket içi SQL Server veritabanı oluşturma](#CreateSQLDB).</span><span class="sxs-lookup"><span data-stu-id="772ab-146">If you already have SQL Server installed in a configuration and in an environment that meets the conditions described above, you can skip ahead and start with [Create a SQL Server database on-premises](#CreateSQLDB).</span></span>

<a name="InstallSQL"></a>

## <a name="a-install-sql-server-express-enable-tcpip-and-create-a-sql-server-database-on-premises"></a><span data-ttu-id="772ab-147">A.</span><span class="sxs-lookup"><span data-stu-id="772ab-147">A.</span></span> <span data-ttu-id="772ab-148">SQL Server Express'i yüklemek, TCP/IP'yi etkinleştirin ve şirket içi SQL Server veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="772ab-148">Install SQL Server Express, enable TCP/IP, and create a SQL Server database on-premises</span></span>
<span data-ttu-id="772ab-149">Bu bölümde SQL Server Express'i yüklemek, TCP/IP'yi etkinleştirin ve böylece, web uygulamanızın Azure Portal ile çalışacak bir veritabanı oluşturmak nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="772ab-149">This section shows you how to install SQL Server Express, enable TCP/IP, and create a database so that your web application will work with the Azure Portal.</span></span>

### <a name="install-sql-server-express"></a><span data-ttu-id="772ab-150">SQL Server Express'i Yükleme</span><span class="sxs-lookup"><span data-stu-id="772ab-150">Install SQL Server Express</span></span>
1. <span data-ttu-id="772ab-151">SQL Server Express'i yüklemek için **SQLEXPRWT_x64_ENU.exe** veya **SQLEXPR_x86_ENU.exe** indirdiğiniz dosya.</span><span class="sxs-lookup"><span data-stu-id="772ab-151">To install SQL Server Express, run the **SQLEXPRWT_x64_ENU.exe** or **SQLEXPR_x86_ENU.exe** file that you downloaded.</span></span> <span data-ttu-id="772ab-152">SQL Server Yükleme Merkezi'ni Sihirbazı görünür.</span><span class="sxs-lookup"><span data-stu-id="772ab-152">The SQL Server Installation Center wizard appears.</span></span>
   
    ![SQL Server yükleme][SQLServerInstall]
2. <span data-ttu-id="772ab-154">Seçin **yeni SQL Server tek başına yükleme veya mevcut bir yüklemeye özellikler ekleme**.</span><span class="sxs-lookup"><span data-stu-id="772ab-154">Choose **New SQL Server stand-alone installation or add features to an existing installation**.</span></span> <span data-ttu-id="772ab-155">İçin elde edene kadar varsayılan seçenekleri ve ayarları, kabul etme yönergeleri izleyerek **örnek Yapılandırması** sayfası.</span><span class="sxs-lookup"><span data-stu-id="772ab-155">Follow the instructions, accepting the default choices and settings, until you get to the **Instance Configuration** page.</span></span>
3. <span data-ttu-id="772ab-156">Üzerinde **örnek Yapılandırması** sayfasında, **varsayılan örnek**.</span><span class="sxs-lookup"><span data-stu-id="772ab-156">On the **Instance Configuration** page, choose **Default instance**.</span></span>
   
    ![Varsayılan bir örnek seçin][ChooseDefaultInstance]
   
    <span data-ttu-id="772ab-158">Varsayılan olarak, SQL Server'ın varsayılan örneğinin statik bağlantı noktası 1433, SQL Server istemcilerinden gelen istekleri ne karma bağlantılar özellik gerektirir olduğu dinler.</span><span class="sxs-lookup"><span data-stu-id="772ab-158">By default, the default instance of SQL Server listens for requests from SQL Server clients on static port 1433, which is what the Hybrid Connections feature requires.</span></span> <span data-ttu-id="772ab-159">Karma bağlantılar tarafından desteklenmeyen dinamik bağlantı noktaları ve UDP, adlandırılmış örnekleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="772ab-159">Named instances use dynamic ports and UDP, which are not supported by Hybrid Connections.</span></span>
4. <span data-ttu-id="772ab-160">Varsayılanları kabul **sunucu yapılandırması** sayfası.</span><span class="sxs-lookup"><span data-stu-id="772ab-160">Accept the defaults on the **Server Configuration** page.</span></span>
5. <span data-ttu-id="772ab-161">Üzerinde **veritabanı altyapısı Yapılandırması** sayfasında **kimlik doğrulama modu**, seçin **karma mod (SQL Server kimlik doğrulaması ve Windows kimlik doğrulaması)**ve bir parola belirtin.</span><span class="sxs-lookup"><span data-stu-id="772ab-161">On the **Database Engine Configuration** page, under **Authentication Mode**, choose **Mixed Mode (SQL Server authentication and Windows authentication)**, and provide a password.</span></span>
   
    ![Karma mod seçin][ChooseMixedMode]
   
    <span data-ttu-id="772ab-163">Bu öğreticide, SQL Server kimlik doğrulamasını kullanır.</span><span class="sxs-lookup"><span data-stu-id="772ab-163">In this tutorial, you will be using SQL Server authentication.</span></span> <span data-ttu-id="772ab-164">Daha sonra ihtiyacınız olacak çünkü sağlarsanız, parolayı anımsa emin olun.</span><span class="sxs-lookup"><span data-stu-id="772ab-164">Be sure to remember the password that you provide, because you will need it later.</span></span>
6. <span data-ttu-id="772ab-165">Yüklemeyi tamamlamak için Sihirbazı'nı kullanılmadıkları adım.</span><span class="sxs-lookup"><span data-stu-id="772ab-165">Step through the rest of the wizard to complete the installation.</span></span>

### <a name="enable-tcpip"></a><span data-ttu-id="772ab-166">TCP/IP'yi etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="772ab-166">Enable TCP/IP</span></span>
<span data-ttu-id="772ab-167">TCP/IP'yi etkinleştirmek için SQL Server Express yüklendiğinde, yüklü olduğu SQL Server Configuration Manager kullanır.</span><span class="sxs-lookup"><span data-stu-id="772ab-167">To enable TCP/IP, you will use SQL Server Configuration Manager, which was installed when you installed SQL Server Express.</span></span> <span data-ttu-id="772ab-168">Adımları [SQL Server TCP/IP ağ protokolünü etkinleştirin](http://technet.microsoft.com/library/hh231672%28v=sql.110%29.aspx) devam etmeden önce.</span><span class="sxs-lookup"><span data-stu-id="772ab-168">Follow the steps in [Enable TCP/IP Network Protocol for SQL Server](http://technet.microsoft.com/library/hh231672%28v=sql.110%29.aspx) before continuing.</span></span>

<a name="CreateSQLDB"></a>

### <a name="create-a-sql-server-database-on-premises"></a><span data-ttu-id="772ab-169">Şirket içi SQL Server veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="772ab-169">Create a SQL Server database on-premises</span></span>
<span data-ttu-id="772ab-170">Visual Studio web uygulamanızı Azure tarafından erişilebilir bir üyelik veritabanı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="772ab-170">Your Visual Studio web application requires a membership database that can be accessed by Azure.</span></span> <span data-ttu-id="772ab-171">Bu bir SQL Server veya SQL Server Express veritabanı (varsayılan olarak MVC şablonu kullanan LocalDB veritabanı değil), gerektirir üyelik veritabanının sonraki oluşturmanız.</span><span class="sxs-lookup"><span data-stu-id="772ab-171">This requires a SQL Server or SQL Server Express database (not the LocalDB database that the MVC template uses by default), so you'll create the membership database next.</span></span>

1. <span data-ttu-id="772ab-172">SQL Server Management Studio'da yalnızca yüklü olan SQL Server bağlayın.</span><span class="sxs-lookup"><span data-stu-id="772ab-172">In SQL Server Management Studio, connect to the SQL Server you just installed.</span></span> <span data-ttu-id="772ab-173">(Varsa **sunucuya Bağlan** iletişim otomatik olarak görünmez, gitmek **Object Explorer** sol bölmede **Bağlan**ve ardından **veritabanı altyapısı**.) ![Sunucuya Bağlan][SSMSConnectToServer]</span><span class="sxs-lookup"><span data-stu-id="772ab-173">(If the **Connect to Server** dialog does not appear automatically, navigate to **Object Explorer** in the left pane, click **Connect**, and then click **Database Engine**.) ![Connect to Server][SSMSConnectToServer]</span></span>
   
    <span data-ttu-id="772ab-174">İçin **sunucu türü**, seçin **veritabanı altyapısı**.</span><span class="sxs-lookup"><span data-stu-id="772ab-174">For **Server type**, choose **Database Engine**.</span></span> <span data-ttu-id="772ab-175">İçin **sunucu adı**, kullanabileceğiniz **localhost** veya kullanmakta olduğunuz bilgisayarın adı.</span><span class="sxs-lookup"><span data-stu-id="772ab-175">For **Server name**, you can use **localhost** or the name of the computer that you are using.</span></span> <span data-ttu-id="772ab-176">Seçin **SQL Server kimlik doğrulaması**ve ardından sa kullanıcı adını ve daha önce oluşturduğunuz parola ile oturum açın.</span><span class="sxs-lookup"><span data-stu-id="772ab-176">Choose **SQL Server authentication**, and then log in with the sa user name and the password that you created earlier.</span></span>
2. <span data-ttu-id="772ab-177">SQL Server Management Studio'yu kullanarak yeni bir veritabanı oluşturmak için sağ **veritabanları** , Nesne Gezgini ve ardından **yeni veritabanı**.</span><span class="sxs-lookup"><span data-stu-id="772ab-177">To create a new database by using SQL Server Management Studio, right-click **Databases** in Object Explorer, and then click **New Database**.</span></span>
   
    ![Yeni veritabanı oluştur][SSMScreateNewDB]
3. <span data-ttu-id="772ab-179">İçinde **yeni veritabanı** iletişim kutusunda, MembershipDB veritabanı adını girin ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="772ab-179">In the **New Database** dialog, enter MembershipDB for the database name, and then click **OK**.</span></span>
   
    ![Veritabanı adı girin][SSMSprovideDBname]
   
    <span data-ttu-id="772ab-181">Veritabanına bu noktada değişiklik yok olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="772ab-181">Note that you do not make any changes to the database at this point.</span></span> <span data-ttu-id="772ab-182">Çalıştırdığınızda, web uygulamanız tarafından üyelik bilgilerini daha sonra otomatik olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="772ab-182">The membership information will be added automatically later by your web application when you run it.</span></span>
4. <span data-ttu-id="772ab-183">Nesne Gezgini'nde, genişletirseniz, **veritabanları**, üyelik veritabanının oluşturulduğunu görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="772ab-183">In Object Explorer, if you expand **Databases**, you will see that the membership database has been created.</span></span>
   
    ![Oluşturulan MembershipDB][SSMSMembershipDBCreated]

<a name="CreateSite"></a>

## <a name="b-create-a-web-app-in-the-azure-portal"></a><span data-ttu-id="772ab-185">B.</span><span class="sxs-lookup"><span data-stu-id="772ab-185">B.</span></span> <span data-ttu-id="772ab-186">Azure Portalı'nda bir web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="772ab-186">Create a web app in the Azure Portal</span></span>
> [!NOTE]
> <span data-ttu-id="772ab-187">Bu öğretici için kullanmak istediğiniz Azure Portalı'nda bir web uygulaması zaten oluşturduysanız, atlayabilirsiniz [karma bağlantı ve bir BizTalk hizmeti oluşturma](#CreateHC) ve buradan devam edin.</span><span class="sxs-lookup"><span data-stu-id="772ab-187">If you have already created a web app in the Azure Portal that you want to use for this tutorial, you can skip ahead to [Create a Hybrid Connection and a BizTalk Service](#CreateHC) and continue from there.</span></span>
> 
> 

1. <span data-ttu-id="772ab-188">İçinde [Azure Portal](https://portal.azure.com), tıklatın **yeni** > **Web + mobil** > **Web uygulaması**.</span><span class="sxs-lookup"><span data-stu-id="772ab-188">In the [Azure Portal](https://portal.azure.com), click **New** > **Web + Mobile** > **Web app**.</span></span>
   
    ![Yeni düğmesi][New]
2. <span data-ttu-id="772ab-190">Web Uygulamanızı yapılandırmak ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="772ab-190">Configure your web app, and then click **Create**.</span></span>
   
    ![Web sitesi adı][WebsiteCreationBlade]
3. <span data-ttu-id="772ab-192">Birkaç dakika sonra web uygulaması oluşturuldu ve kendi web uygulaması dikey penceresi görünür.</span><span class="sxs-lookup"><span data-stu-id="772ab-192">After a few moments, the web app is created and its web app blade appears.</span></span> <span data-ttu-id="772ab-193">Dikey web uygulamanızı yönetmenizi sağlayan bir dikey olarak kaydırılabilir Pano ' dir.</span><span class="sxs-lookup"><span data-stu-id="772ab-193">The blade is a vertically scrollable dashboard that lets you manage your web app.</span></span>
   
    ![Çalışan Web sitesi][WebSiteRunningBlade]
   
    <span data-ttu-id="772ab-195">Web uygulaması Canlı doğrulamak için tıklayabilirsiniz **Gözat** varsayılan sayfasını görüntülemek için simge.</span><span class="sxs-lookup"><span data-stu-id="772ab-195">To verify the web app is live, you can click the **Browse** icon to display the default page.</span></span>

<span data-ttu-id="772ab-196">Ardından, karma bir bağlantı ve web uygulaması BizTalk hizmeti oluşturur.</span><span class="sxs-lookup"><span data-stu-id="772ab-196">Next, you will create a hybrid connection and a BizTalk service for the web app.</span></span>

<a name="CreateHC"></a>

## <a name="c-create-a-hybrid-connection-and-a-biztalk-service"></a><span data-ttu-id="772ab-197">C.</span><span class="sxs-lookup"><span data-stu-id="772ab-197">C.</span></span> <span data-ttu-id="772ab-198">Karma bağlantı ve bir BizTalk hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="772ab-198">Create a Hybrid Connection and a BizTalk Service</span></span>
1. <span data-ttu-id="772ab-199">Geri Portalı'nda Ayarlar'a gidip tıklayın **ağ** > **karma bağlantı uç noktalarınızı yapılandırın**.</span><span class="sxs-lookup"><span data-stu-id="772ab-199">Back in the Portal, go to settings and click **Networking** > **Configure your hybrid connection endpoints**.</span></span>
   
    ![Karma bağlantılar][CreateHCHCIcon]
2. <span data-ttu-id="772ab-201">Karma bağlantılar dikey penceresinde **Ekle** > **yeni karma bağlantı**.</span><span class="sxs-lookup"><span data-stu-id="772ab-201">On the Hybrid connections blade, click **Add** > **New hybrid connection**.</span></span>
3. <span data-ttu-id="772ab-202">Üzerinde **karma bağlantı oluşturmak** dikey penceresinde:</span><span class="sxs-lookup"><span data-stu-id="772ab-202">On the **Create hybrid connection** blade:</span></span>
   
   * <span data-ttu-id="772ab-203">İçin **adı**, bağlantı için bir ad sağlayın.</span><span class="sxs-lookup"><span data-stu-id="772ab-203">For **Name**, provide a name for the connection.</span></span>
   * <span data-ttu-id="772ab-204">İçin **ana bilgisayar adı**, SQL Server ana bilgisayarınız bilgisayar adını girin.</span><span class="sxs-lookup"><span data-stu-id="772ab-204">For **Hostname**, enter the computer name of your SQL Server host computer.</span></span>
   * <span data-ttu-id="772ab-205">İçin **bağlantı noktası**, 1433 (varsayılan bağlantı noktası için SQL Server) girin.</span><span class="sxs-lookup"><span data-stu-id="772ab-205">For **Port**, enter 1433 (the default port for SQL Server).</span></span>
   * <span data-ttu-id="772ab-206">Tıklatın **BizTalk hizmeti** > **yeni BizTalk hizmeti** ve BizTalk hizmeti için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="772ab-206">Click **BizTalk Service** > **New BizTalk Service** and enter a name for the BizTalk service.</span></span>
     
     ![Karma bağlantı oluşturma][TwinCreateHCBlades]
4. <span data-ttu-id="772ab-208">Tıklatın **Tamam** iki kez.</span><span class="sxs-lookup"><span data-stu-id="772ab-208">Click **OK** twice.</span></span>
   
    <span data-ttu-id="772ab-209">İşlem tamamlandığında **bildirimleri** alanı yeşil flash **başarı** ve **karma bağlantı** dikey durumundaki yeni karma bağlantıyı gösterir **bağlı**.</span><span class="sxs-lookup"><span data-stu-id="772ab-209">When the process completes, the **Notifications** area will flash a green **SUCCESS** and the **Hybrid connection** blade will show the new hybrid connection with the status as **Not connected**.</span></span>
   
    ![Oluşturulan bir karma bağlantı][CreateHCOneConnectionCreated]

<span data-ttu-id="772ab-211">Bu noktada, bulut karma bağlantı altyapı önemli bir kısmını tamamladınız.</span><span class="sxs-lookup"><span data-stu-id="772ab-211">At this point, you have completed an important part of the cloud hybrid connection infrastructure.</span></span> <span data-ttu-id="772ab-212">Ardından, karşılık gelen bir şirket içi parça oluşturur.</span><span class="sxs-lookup"><span data-stu-id="772ab-212">Next, you will create a corresponding on-premises piece.</span></span>

<a name="InstallHCM"></a>

## <a name="d-install-the-on-premises-hybrid-connection-manager-to-complete-the-connection"></a><span data-ttu-id="772ab-213">D.</span><span class="sxs-lookup"><span data-stu-id="772ab-213">D.</span></span> <span data-ttu-id="772ab-214">Bağlantıyı tamamlamak için şirket içi karma Bağlantı Yöneticisi'ni yükleyin</span><span class="sxs-lookup"><span data-stu-id="772ab-214">Install the on-premises Hybrid Connection Manager to complete the connection</span></span>
[!INCLUDE [app-service-hybrid-connections-manager-install](../../includes/app-service-hybrid-connections-manager-install.md)]

<span data-ttu-id="772ab-215">Karma bağlantı altyapı tamamlandığına göre bunu kullanan bir web uygulaması oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="772ab-215">Now that the hybrid connection infrastructure is complete, you will create a web application that uses it.</span></span>

<a name="CreateASPNET"></a>

## <a name="e-create-a-basic-aspnet-web-project-edit-the-database-connection-string-and-run-the-project-locally"></a><span data-ttu-id="772ab-216">E.</span><span class="sxs-lookup"><span data-stu-id="772ab-216">E.</span></span> <span data-ttu-id="772ab-217">Temel bir ASP.NET web projesi oluşturun, veritabanı bağlantı dizesini düzenlemek ve projeyi yerel olarak çalıştırın</span><span class="sxs-lookup"><span data-stu-id="772ab-217">Create a basic ASP.NET web project, edit the database connection string, and run the project locally</span></span>
### <a name="create-a-basic-aspnet-project"></a><span data-ttu-id="772ab-218">Temel bir ASP.NET projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="772ab-218">Create a basic ASP.NET project</span></span>
1. <span data-ttu-id="772ab-219">Visual Studio'da üzerinde **dosya** menüsünde yeni bir proje oluşturun:</span><span class="sxs-lookup"><span data-stu-id="772ab-219">In Visual Studio, on the **File** menu, create a new Project:</span></span>
   
    ![Yeni Visual Studio projesi][HCVSNewProject]
2. <span data-ttu-id="772ab-221">İçinde **şablonları** bölümünü **yeni proje** iletişim kutusunda **Web** ve **ASP.NET Web uygulaması**ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="772ab-221">In the **Templates** section of the **New Project** dialog, select **Web** and choose **ASP.NET Web Application**, and then click **OK**.</span></span>
   
    ![ASP.NET Web uygulaması seçin][HCVSChooseASPNET]
3. <span data-ttu-id="772ab-223">İçinde **yeni ASP.NET projesi** iletişim kutusunda, seçin **MVC**ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="772ab-223">In the **New ASP.NET Project** dialog, choose **MVC**, and then click **OK**.</span></span>
   
    ![MVC seçin][HCVSChooseMVC]
4. <span data-ttu-id="772ab-225">Proje oluşturduğunuzda uygulama Benioku sayfası görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="772ab-225">When the project has been created, the application readme page appears.</span></span> <span data-ttu-id="772ab-226">Web projesinin henüz çalıştırmayın.</span><span class="sxs-lookup"><span data-stu-id="772ab-226">Do not run the web project yet.</span></span>
   
    ![Benioku sayfası][HCVSReadmePage]

### <a name="edit-the-database-connection-string-for-the-application"></a><span data-ttu-id="772ab-228">Uygulama için veritabanı bağlantı dizesini Düzenle</span><span class="sxs-lookup"><span data-stu-id="772ab-228">Edit the database connection string for the application</span></span>
<span data-ttu-id="772ab-229">Bu adımda, uygulamanızın yerel SQL Server Express veritabanınızın nerede bulacağını bildirir bağlantı dizesini düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="772ab-229">In this step, you edit the connection string that tells your application where to find your local SQL Server Express database.</span></span> <span data-ttu-id="772ab-230">Uygulama yapılandırma bilgilerini içeren uygulamanın Web.config dosyasında bağlantı dizesidir.</span><span class="sxs-lookup"><span data-stu-id="772ab-230">The connection string is in the application's Web.config file, which contains configuration information for the application.</span></span>

> [!NOTE]
> <span data-ttu-id="772ab-231">Uygulamanızı SQL Server Express ve olanı değil, Visual Studio'nun varsayılan yerel veritabanı oluşturulan veritabanı kullandığından emin olmak için projenizi çalıştırmadan önce bu adımı tamamlamak önemlidir.</span><span class="sxs-lookup"><span data-stu-id="772ab-231">To ensure that your application uses the database that you created in SQL Server Express, and not the one in Visual Studio's default LocalDB, it is important that you complete this step before running your project.</span></span>
> 
> 

1. <span data-ttu-id="772ab-232">Çözüm Gezgini'nde, Web.config dosyasını çift tıklatın.</span><span class="sxs-lookup"><span data-stu-id="772ab-232">In Solution Explorer, double-click the Web.config file.</span></span>
   
    ![Web.config][HCVSChooseWebConfig]
2. <span data-ttu-id="772ab-234">Düzen **connectionStrings** bölümü aşağıdaki söz dizimini aşağıdaki örnekte, yerel makinenizde SQL Server veritabanına işaret etmek için:</span><span class="sxs-lookup"><span data-stu-id="772ab-234">Edit the **connectionStrings** section to point to the SQL Server database on your local machine, following the syntax in the following example:</span></span>
   
    ![Bağlantı dizesi][HCVSConnectionString]
   
    <span data-ttu-id="772ab-236">Bağlantı dizesi oluştururken aşağıdakileri unutmayın:</span><span class="sxs-lookup"><span data-stu-id="772ab-236">When composing the connection string, keep in mind the following:</span></span>
   
   * <span data-ttu-id="772ab-237">Varsayılan örneği (örneğin, Sunucunuz\\sqlexpress) yerine adlandırılmış bir örneğine bağlanıyorsanız, SQL Server statik bağlantı noktalarını kullanacak şekilde yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="772ab-237">If you are connecting to a named instance instead of a default instance (for example, YourServer\SQLEXPRESS), you must configure your SQL Server to use static ports.</span></span> <span data-ttu-id="772ab-238">Statik bağlantı noktalarını yapılandırma hakkında daha fazla bilgi için bkz: [SQL Server'ın belirli bir bağlantı noktasında dinleyecek şekilde yapılandırma konusunda](http://support.microsoft.com/kb/823938).</span><span class="sxs-lookup"><span data-stu-id="772ab-238">For information on configuring static ports, see [How to configure SQL Server to listen on a specific port](http://support.microsoft.com/kb/823938).</span></span> <span data-ttu-id="772ab-239">Varsayılan olarak, adlandırılmış örnekleri UDP ve karma bağlantılar tarafından desteklenmeyen dinamik bağlantı noktaları kullanır.</span><span class="sxs-lookup"><span data-stu-id="772ab-239">By default, named instances use UDP and dynamic ports, which are not supported by Hybrid Connections.</span></span>
   * <span data-ttu-id="772ab-240">Önerilen bağlantı noktasını belirtin (varsayılan olarak örnekte gösterildiği gibi 1433) bağlantı dizesi, emin olabilir yerel SQL Server'ınızdaki sahip etkin TCP ve doğru bağlantı noktası kullanıyordur.</span><span class="sxs-lookup"><span data-stu-id="772ab-240">It is recommended that you specify the port (1433 by default, as shown in the example) on the connection string so that you can be sure that your local SQL Server has TCP enabled and is using the correct port.</span></span>
   * <span data-ttu-id="772ab-241">SQL Server kimlik doğrulaması bağlanmak için kullanılacak bağlantı dizenizi kullanıcı kimliği ve parola belirterek unutmayın.</span><span class="sxs-lookup"><span data-stu-id="772ab-241">Remember to use SQL Server Authentication to connect, specifying the user ID and password in your connection string.</span></span>
3. <span data-ttu-id="772ab-242">Tıklatın **kaydetmek** Web.config dosyasını kaydetmek için Visual Studio'da.</span><span class="sxs-lookup"><span data-stu-id="772ab-242">Click **Save** in Visual Studio to save the Web.config file.</span></span>

### <a name="run-the-project-locally-and-register-a-new-user"></a><span data-ttu-id="772ab-243">Projeyi yerel olarak çalıştırın ve yeni bir kullanıcı kaydı</span><span class="sxs-lookup"><span data-stu-id="772ab-243">Run the project locally and register a new user</span></span>
1. <span data-ttu-id="772ab-244">Artık, yeni web projeniz yerel olarak hata ayıklama altında Gözat düğmesine tıklayarak çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="772ab-244">Now, run your new web project locally by clicking the browse button under Debug.</span></span> <span data-ttu-id="772ab-245">Bu örnek, Internet Explorer kullanır.</span><span class="sxs-lookup"><span data-stu-id="772ab-245">This example uses Internet Explorer.</span></span>
   
    ![Projeyi çalıştırın][HCVSRunProject]
2. <span data-ttu-id="772ab-247">Sağ üst tarafındaki varsayılan web sayfası üzerinde seçin **kaydetmek** yeni bir hesap kaydetmek için:</span><span class="sxs-lookup"><span data-stu-id="772ab-247">On the upper right of the default web page, choose **Register** to register a new account:</span></span>
   
    ![Yeni bir hesap Kaydet][HCVSRegisterLocally]
3. <span data-ttu-id="772ab-249">Bir kullanıcı adı ve parola girin:</span><span class="sxs-lookup"><span data-stu-id="772ab-249">Enter a user name and password:</span></span>
   
    ![Kullanıcı adı ve parola girin][HCVSCreateNewAccount]
   
    <span data-ttu-id="772ab-251">Bu otomatik olarak bir veritabanı uygulamanız için üyelik bilgilerini tutan yerel SQL Server üzerinde oluşturur.</span><span class="sxs-lookup"><span data-stu-id="772ab-251">This automatically creates a database on your local SQL Server that holds the membership information for your application.</span></span> <span data-ttu-id="772ab-252">Tablolardan birini (**dbo. AspNetUsers**) ayrı tutma web uygulama kullanıcı kimlik bilgilerini girdiğiniz ayarlara benzer.</span><span class="sxs-lookup"><span data-stu-id="772ab-252">One of the tables (**dbo.AspNetUsers**) holds web app user credentials like the ones that you just entered.</span></span> <span data-ttu-id="772ab-253">Öğreticide daha sonra bu tabloyu görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="772ab-253">You will see this table later in the tutorial.</span></span>
4. <span data-ttu-id="772ab-254">Varsayılan web sayfasının tarayıcı penceresini kapatın.</span><span class="sxs-lookup"><span data-stu-id="772ab-254">Close the browser window of the default web page.</span></span> <span data-ttu-id="772ab-255">Bu, Visual Studio uygulamasında durdurur.</span><span class="sxs-lookup"><span data-stu-id="772ab-255">This stops the application in Visual Studio.</span></span>

<span data-ttu-id="772ab-256">Şimdi uygulamayı Azure'a yayımlama ve test için sonraki adıma hazır olursunuz.</span><span class="sxs-lookup"><span data-stu-id="772ab-256">You are now ready for the next step, which is to publish the application to Azure and test it.</span></span>

<a name="PubNTest"></a>

## <a name="f-publish-the-web-application-to-azure-and-test-it"></a><span data-ttu-id="772ab-257">F</span><span class="sxs-lookup"><span data-stu-id="772ab-257">F.</span></span> <span data-ttu-id="772ab-258">Azure web uygulamasına yayımlamak ve test</span><span class="sxs-lookup"><span data-stu-id="772ab-258">Publish the web application to Azure and test it</span></span>
<span data-ttu-id="772ab-259">Artık uygulamanızı App Service web uygulaması yayımlama ve web uygulamanızı yerel makinenizde veritabanına bağlanmak için daha önce yapılandırılmış karma bağlantı'nın nasıl kullanıldığını görmek için test.</span><span class="sxs-lookup"><span data-stu-id="772ab-259">Now, you'll publish your application to your App Service web app and then test it to see how the hybrid connection you configured earlier is being used to connect your web app to the database on your local machine.</span></span>

### <a name="publish-the-web-application"></a><span data-ttu-id="772ab-260">Web uygulaması yayımlama</span><span class="sxs-lookup"><span data-stu-id="772ab-260">Publish the web application</span></span>
1. <span data-ttu-id="772ab-261">Yayımlama profilinizi Azure Portalı'nda App Service web uygulaması için yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="772ab-261">You can download your publishing profile for the App Service web app in the Azure Portal.</span></span> <span data-ttu-id="772ab-262">Web uygulamanız için dikey penceresinde **Get yayımlama profili**ve ardından dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="772ab-262">On the blade for your web app, click **Get publish profile**, and then save the file to your computer.</span></span>
   
    ![Yayım profili indirin][PortalDownloadPublishProfile]
   
    <span data-ttu-id="772ab-264">Ardından, Visual Studio web uygulamanıza bu dosyayı içeri aktaracak.</span><span class="sxs-lookup"><span data-stu-id="772ab-264">Next, you will import this file into your Visual Studio web application.</span></span>
2. <span data-ttu-id="772ab-265">Visual Studio'daki Çözüm Gezgini'nde proje adına sağ tıklayın ve seçin **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="772ab-265">In Visual Studio, right-click the project name in Solution Explorer and select **Publish**.</span></span>
   
    ![Select yayımlama][HCVSRightClickProjectSelectPublish]
3. <span data-ttu-id="772ab-267">İçinde **Web'i Yayımla** iletişim, **profil** sekmesinde, seçin **alma**.</span><span class="sxs-lookup"><span data-stu-id="772ab-267">In the **Publish Web** dialog, on the **Profile** tab, choose **Import**.</span></span>
   
    ![İçeri Aktarma][HCVSPublishWebDialogImport]
4. <span data-ttu-id="772ab-269">İndirilen yayımlama profiline göz atın, onu seçin ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="772ab-269">Browse to your downloaded publishing profile, select it, and then click **OK**.</span></span>
   
    ![Profiline göz atın][HCVSBrowseToImportPubProfile]
5. <span data-ttu-id="772ab-271">Yayımlama bilgilerinizi içe aktarılır ve görüntüler **bağlantı** iletişim kutusunun sekmesi.</span><span class="sxs-lookup"><span data-stu-id="772ab-271">Your publishing information is imported and displays on the **Connection** tab of the dialog.</span></span>
   
    ![Yayınla'yı tıklatın][HCVSClickPublish]
   
    <span data-ttu-id="772ab-273">**Yayımla**’ta tıklayın.</span><span class="sxs-lookup"><span data-stu-id="772ab-273">Click **Publish**.</span></span>
   
    <span data-ttu-id="772ab-274">Yayımlama tamamlandığında tarayıcınızı başlatın ve şimdi bunu Azure bulutunda dinamik olması dışında şimdi bilinen ASP.NET uygulamanızın--Göster!</span><span class="sxs-lookup"><span data-stu-id="772ab-274">When publishing completes, your browser will launch and show your now familiar ASP.NET application -- except that now it is live in the Azure cloud!</span></span>

<span data-ttu-id="772ab-275">Ardından, uygulamada karma bağlantısını görmek için canlı web uygulamanızı kullanır.</span><span class="sxs-lookup"><span data-stu-id="772ab-275">Next, you will use your live web application to see its Hybrid Connection in action.</span></span>

### <a name="test-the-completed-web-application-on-azure"></a><span data-ttu-id="772ab-276">Azure üzerinde tamamlanan web uygulamasını test</span><span class="sxs-lookup"><span data-stu-id="772ab-276">Test the completed web application on Azure</span></span>
1. <span data-ttu-id="772ab-277">Üst kısmında, web sayfasının sağ Azure üzerinde seçin **oturum**.</span><span class="sxs-lookup"><span data-stu-id="772ab-277">On the top right of your web page on Azure, choose **Log in**.</span></span>
   
    ![Test oturum açma][HCTestLogIn]
2. <span data-ttu-id="772ab-279">App Service web uygulaması, web uygulamanızın üyelik veritabanının yerel makinenizde şimdi bağlı.</span><span class="sxs-lookup"><span data-stu-id="772ab-279">Your App Service web app is now connected to your web application's membership database on your local machine.</span></span> <span data-ttu-id="772ab-280">Bunu doğrulamak için daha önce girdiğiniz yerel veritabanında aynı kimlik bilgileriyle oturum açın.</span><span class="sxs-lookup"><span data-stu-id="772ab-280">To verify this, log in with the same credentials that you entered in the local database earlier.</span></span>
   
    ![Merhaba Karşılama][HCTestHelloContoso]
3. <span data-ttu-id="772ab-282">Daha fazla yeni karma bağlantınızı sınamak için Azure web uygulamanızın dışına oturum ve başka bir kullanıcı olarak kaydedin.</span><span class="sxs-lookup"><span data-stu-id="772ab-282">To further test your new hybrid connection, log off of your Azure web application and register as another user.</span></span> <span data-ttu-id="772ab-283">Yeni bir kullanıcı adı ve parolasını girin ve ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="772ab-283">Provide a new user name and password, and then click **Register**.</span></span>
   
    ![Test başka bir kullanıcı kaydetme][HCTestRegisterRelecloud]
4. <span data-ttu-id="772ab-285">Yeni kullanıcının kimlik bilgilerini yerel veritabanınızda karma bağlantınız üzerinden depolanmıştı doğrulamak için yerel bilgisayarınızda SQL Management Studio'yu açın.</span><span class="sxs-lookup"><span data-stu-id="772ab-285">To verify that the new user's credentials have been stored in your local database through your hybrid connection, open SQL Management Studio on your local computer.</span></span> <span data-ttu-id="772ab-286">Nesne Gezgini'nde genişletin **MembershipDB** veritabanı ve ardından **tabloları**.</span><span class="sxs-lookup"><span data-stu-id="772ab-286">In Object Explorer, expand the **MembershipDB** database, and then expand **Tables**.</span></span> <span data-ttu-id="772ab-287">Sağ **dbo. AspNetUsers** üyelik tablosunda ve seçin **ilk 1000 satırı Seç** sonuçları görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="772ab-287">Right-click the **dbo.AspNetUsers** membership table and choose **Select Top 1000 Rows** to view the results.</span></span>
   
    ![Sonuçları görüntüleme][HCTestSSMSTree]
5. <span data-ttu-id="772ab-289">Yerel üyelik tablonuz şimdi her iki hesap - yerel olarak oluşturulan ve Azure bulutta oluşturulan bir gösterir.</span><span class="sxs-lookup"><span data-stu-id="772ab-289">Your local membership table now shows both accounts - the one that you created locally, and the one that you created in the Azure cloud.</span></span> <span data-ttu-id="772ab-290">Bulutta oluşturulan bir Azure'nın karma bağlantı özelliği aracılığıyla şirket içi veritabanına kaydedildi.</span><span class="sxs-lookup"><span data-stu-id="772ab-290">The one that you created in the cloud has been saved to your on-premises database through Azure's Hybrid Connection feature.</span></span>
   
    ![Şirket içi veritabanında kayıtlı kullanıcılar][HCTestShowMemberDb]

<span data-ttu-id="772ab-292">Artık oluşturduğunuz ve bir web uygulaması Azure bulutta ve şirket içi SQL Server veritabanı arasında bir karma bağlantı kullanan bir ASP.NET web uygulaması dağıtılmış.</span><span class="sxs-lookup"><span data-stu-id="772ab-292">You have now created and deployed an ASP.NET web application that uses a hybrid connection between a web app in the Azure cloud and an on-premises SQL Server database.</span></span> <span data-ttu-id="772ab-293">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="772ab-293">Congratulations!</span></span>

## <a name="see-also"></a><span data-ttu-id="772ab-294">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="772ab-294">See Also</span></span>
[<span data-ttu-id="772ab-295">Karma Bağlantılara genel bakış</span><span class="sxs-lookup"><span data-stu-id="772ab-295">Hybrid Connections overview</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=397274)

[<span data-ttu-id="772ab-296">Karma bağlantılar (Channel 9 video) Josh geçiş sunar</span><span class="sxs-lookup"><span data-stu-id="772ab-296">Josh Twist introduces hybrid connections (Channel 9 video)</span></span>](http://channel9.msdn.com/Shows/Azure-Friday/Josh-Twist-introduces-hybrid-connections)

[<span data-ttu-id="772ab-297">Karma Bağlantılara genel bakış</span><span class="sxs-lookup"><span data-stu-id="772ab-297">Hybrid Connections overview</span></span>](/services/biztalk-services/)

[<span data-ttu-id="772ab-298">BizTalk Services: Pano, İzleyici, Ölçek, yapılandırma ve karma bağlantı sekmeleri</span><span class="sxs-lookup"><span data-stu-id="772ab-298">BizTalk Services: Dashboard, Monitor, Scale, Configure, and Hybrid Connection tabs</span></span>](../biztalk-services/biztalk-dashboard-monitor-scale-tabs.md)

[<span data-ttu-id="772ab-299">Gerçek dünya karma bir buluta sorunsuz uygulama taşıma (Channel 9 video) ile oluşturma</span><span class="sxs-lookup"><span data-stu-id="772ab-299">Building a Real-World Hybrid Cloud with Seamless Application Portability (Channel 9 video)</span></span>](http://channel9.msdn.com/events/TechEd/NorthAmerica/2014/DCIM-B323#fbid=)

[<span data-ttu-id="772ab-300">Azure App Service içinde karma bağlantılar kullanarak şirket kaynaklarına erişmek</span><span class="sxs-lookup"><span data-stu-id="772ab-300">Access on-premises resources using hybrid connections in Azure App Service</span></span>](web-sites-hybrid-connection-get-started.md)

[<span data-ttu-id="772ab-301">ASP.NET Kimliği'ne genel bakış</span><span class="sxs-lookup"><span data-stu-id="772ab-301">ASP.NET Identity Overview</span></span>](http://www.asp.net/identity)

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
