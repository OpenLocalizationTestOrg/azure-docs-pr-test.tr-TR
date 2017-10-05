---
title: "Azure Uygulama Hizmeti’nde karma bağlantıları kullanarak şirket içi kaynaklara erişme"
description: "Azure App Service'in web uygulamasında ve statik bir TCP bağlantı noktası kullanan şirket içi kaynağı arasında bağlantı oluşturma"
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: mollybos
ms.assetid: a46ed26b-df8e-4fc3-8e05-2d002a6ee508
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2016
ms.author: cephalin
ms.openlocfilehash: fbd22e6e285c5ddaef2a473671d4a06a97384b4a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="access-on-premises-resources-using-hybrid-connections-in-azure-app-service"></a><span data-ttu-id="1f36d-103">Azure Uygulama Hizmeti’nde karma bağlantıları kullanarak şirket içi kaynaklara erişme</span><span class="sxs-lookup"><span data-stu-id="1f36d-103">Access on-premises resources using hybrid connections in Azure App Service</span></span>
<span data-ttu-id="1f36d-104">Azure App Service uygulama SQL Server, MySQL, HTTP Web API'leri ve birçok özel Web hizmeti gibi statik TCP bağlantı kullanan şirket içi kaynaklara bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="1f36d-104">You can connect an Azure App Service app to any on-premises resource that uses a static TCP port, such as SQL Server, MySQL, HTTP Web APIs, and most custom Web Services.</span></span> <span data-ttu-id="1f36d-105">Bu makale App Service ve bir şirket içi SQL Server veritabanı arasında bir karma bağlantı oluşturulacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="1f36d-105">This article shows you how to create a hybrid connection between App Service and an on-premises SQL Server database.</span></span>

> [!NOTE]
> <span data-ttu-id="1f36d-106">Web uygulamalarının karma bağlantılar özelliği yalnızca bölümüdür [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1f36d-106">The Web Apps portion of the Hybrid Connections feature is available only in the [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="1f36d-107">BizTalk Services'da bir bağlantı oluşturmak için bkz: [karma bağlantılar](http://go.microsoft.com/fwlink/p/?LinkID=397274).</span><span class="sxs-lookup"><span data-stu-id="1f36d-107">To create a connection in BizTalk Services, see [Hybrid Connections](http://go.microsoft.com/fwlink/p/?LinkID=397274).</span></span> 
> 
> <span data-ttu-id="1f36d-108">Bu içerik, Azure App Service'de Mobile Apps için de geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="1f36d-108">This content also applies to Mobile Apps in Azure App Service.</span></span> 
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="1f36d-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="1f36d-109">Prerequisites</span></span>
* <span data-ttu-id="1f36d-110">Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="1f36d-110">An Azure subscription.</span></span> <span data-ttu-id="1f36d-111">Ücretsiz bir abonelik için bkz: [Azure ücretsiz deneme sürümü](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1f36d-111">For a free subscription, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
  
    <span data-ttu-id="1f36d-112">Azure hesabı için kaydolmadan önce Azure App Service’i kullanmaya başlamak isterseniz, App Service’te hemen kısa süreli bir başlangıç web uygulaması oluşturabileceğiniz [App Service’i Deneyin](https://azure.microsoft.com/try/app-service/) sayfasına gidin.</span><span class="sxs-lookup"><span data-stu-id="1f36d-112">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="1f36d-113">Kredi kartı ve taahhüt gerekmez.</span><span class="sxs-lookup"><span data-stu-id="1f36d-113">No credit cards required; no commitments.</span></span>
* <span data-ttu-id="1f36d-114">Bir şirket içi SQL Server veya SQL Server Express veritabanı ile karma bağlantı kullanmak için TCP/IP'yi statik bağlantı noktasına etkinleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="1f36d-114">To use an on-premises SQL Server or SQL Server Express database with a hybrid connection, TCP/IP needs to be enabled on a static port.</span></span> <span data-ttu-id="1f36d-115">Statik bağlantı noktası 1433 kullandığından, varsayılan bir örnek SQL Server üzerinde kullanılması önerilir.</span><span class="sxs-lookup"><span data-stu-id="1f36d-115">Using a default instance on SQL Server is recommended because it uses static port 1433.</span></span> <span data-ttu-id="1f36d-116">Yükleme ve karma bağlantılar ile kullanmak için SQL Server Express yapılandırma hakkında daha fazla bilgi için bkz: [karma bağlantılar kullanarak bir Azure web sitesinden bir şirket içi SQL Server'a Bağlan](http://go.microsoft.com/fwlink/?LinkID=397979).</span><span class="sxs-lookup"><span data-stu-id="1f36d-116">For information on installing and configuring SQL Server Express for use with hybrid connections, see [Connect to an on-premises SQL Server from an Azure web site using Hybrid Connections](http://go.microsoft.com/fwlink/?LinkID=397979).</span></span>
* <span data-ttu-id="1f36d-117">Bilgisayar üzerinde bu makalenin sonraki bölümlerinde açıklanan şirket içi karma Bağlantı Yöneticisi aracısı yükleyin:</span><span class="sxs-lookup"><span data-stu-id="1f36d-117">The computer on which you install the on-premises Hybrid Connection Manager agent described later in this article:</span></span>
  
  * <span data-ttu-id="1f36d-118">Azure için bağlantı noktası 5671 üzerinden bağlanabilmesi gerekir</span><span class="sxs-lookup"><span data-stu-id="1f36d-118">Must be able to connect to Azure over port 5671</span></span>
  * <span data-ttu-id="1f36d-119">Ulaşabilmesi olmalıdır *ana bilgisayar adı*:*BağlantıNoktasıNumarası* , şirket içi kaynak.</span><span class="sxs-lookup"><span data-stu-id="1f36d-119">Must be able to reach the *hostname*:*portnumber* of your on-premises resource.</span></span> 

> [!NOTE]
> <span data-ttu-id="1f36d-120">Bu makaledeki adımları, şirket içi karma Bağlantı Aracısı'nı barındıracak bilgisayarı tarayıcıdan kullandığınızı varsayar.</span><span class="sxs-lookup"><span data-stu-id="1f36d-120">The steps in this article assume that you are using the browser from the computer that will host the on-premises hybrid connection agent.</span></span>
> 
> 

## <a name="create-a-web-app-in-the-azure-portal"></a><span data-ttu-id="1f36d-121">Azure Portalı'nda bir web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="1f36d-121">Create a web app in the Azure Portal</span></span>
> [!NOTE]
> <span data-ttu-id="1f36d-122">Bu öğretici için kullanmak istediğiniz Azure Portalı'nda bir web uygulaması veya mobil uygulama arka ucu zaten oluşturmuş durumdaysanız, atlayabilirsiniz [karma bağlantı ve bir BizTalk hizmeti oluşturma](#CreateHC) ve buradan başlayın.</span><span class="sxs-lookup"><span data-stu-id="1f36d-122">If you have already created a web app or Mobile App backend in the Azure Portal that you want to use for this tutorial, you can skip ahead to [Create a Hybrid Connection and a BizTalk Service](#CreateHC) and start from there.</span></span>
> 
> 

1. <span data-ttu-id="1f36d-123">Sol üst köşesindeki [Azure Portal](https://portal.azure.com), tıklatın **yeni** > **Web + mobil** > **Web uygulaması**.</span><span class="sxs-lookup"><span data-stu-id="1f36d-123">In the upper left corner of the [Azure Portal](https://portal.azure.com), click **New** > **Web + Mobile** > **Web App**.</span></span>
   
    ![Yeni web uygulaması][NewWebsite]
2. <span data-ttu-id="1f36d-125">Üzerinde **Web uygulaması** dikey penceresinde, bir URL sağlayın ve tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="1f36d-125">On the **Web app** blade, provide a URL and click **Create**.</span></span> 
   
    ![Web sitesi adı][WebsiteCreationBlade]
3. <span data-ttu-id="1f36d-127">Birkaç dakika sonra web uygulaması oluşturuldu ve kendi web uygulaması dikey penceresi görünür.</span><span class="sxs-lookup"><span data-stu-id="1f36d-127">After a few moments, the web app is created and its web app blade appears.</span></span> <span data-ttu-id="1f36d-128">Dikey sitenizi yönetmenize olanak sağlayan bir dikey olarak kaydırılabilir Pano ' dir.</span><span class="sxs-lookup"><span data-stu-id="1f36d-128">The blade is a vertically scrollable dashboard that lets you manage your site.</span></span>
   
    ![Çalışan Web sitesi][WebSiteRunningBlade]
4. <span data-ttu-id="1f36d-130">Site Canlı doğrulamak için tıklayabilirsiniz **Gözat** varsayılan sayfasını görüntülemek için simge.</span><span class="sxs-lookup"><span data-stu-id="1f36d-130">To verify the site is live, you can click the **Browse** icon to display the default page.</span></span>
   
    ![Web uygulamanızı görmek için Gözat'ı tıklatın][Browse]
   
    ![Varsayılan web uygulama sayfası][DefaultWebSitePage]

<span data-ttu-id="1f36d-133">Ardından, karma bir bağlantı ve web uygulaması BizTalk hizmeti oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1f36d-133">Next, you will create a hybrid connection and a BizTalk service for the web app.</span></span>

<a name="CreateHC"></a>

## <a name="create-a-hybrid-connection-and-a-biztalk-service"></a><span data-ttu-id="1f36d-134">Karma bağlantı ve bir BizTalk hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="1f36d-134">Create a Hybrid Connection and a BizTalk Service</span></span>
1. <span data-ttu-id="1f36d-135">Web uygulaması dikey penceresinde tıklayın **tüm ayarları** > **ağ** > **karma bağlantı uç noktalarınızı yapılandırın**.</span><span class="sxs-lookup"><span data-stu-id="1f36d-135">In your web app blade click on **All settings** > **Networking** > **Configure your hybrid connection endpoints**.</span></span>
   
    ![Karma bağlantılar][CreateHCHCIcon]
2. <span data-ttu-id="1f36d-137">Karma bağlantılar dikey penceresinde **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="1f36d-137">On the Hybrid connections blade, click **Add**.</span></span>
   
    <!-- ![Add a hybrid connnection][CreateHCAddHC]
   -->
3. <span data-ttu-id="1f36d-138">**Karma bağlantı ekleyin** dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="1f36d-138">The **Add a hybrid connection** blade opens.</span></span>  <span data-ttu-id="1f36d-139">Bu ilk karma bağlantınız olduğundan **yeni karma bağlantı** seçeneği seçilmiş ve **karma bağlantı oluşturmak** sizin için dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="1f36d-139">Since this is your first hybrid connection, the **New hybrid connection** option is preselected, and the **Create hybrid connection** blade opens for you.</span></span>
   
    ![Karma bağlantı oluşturma][TwinCreateHCBlades]
   
    <span data-ttu-id="1f36d-141">Üzerinde **oluşturma karma bağlantı dikey**:</span><span class="sxs-lookup"><span data-stu-id="1f36d-141">On the **Create hybrid connection blade**:</span></span>
   
   * <span data-ttu-id="1f36d-142">İçin **adı**, bağlantı için bir ad sağlayın.</span><span class="sxs-lookup"><span data-stu-id="1f36d-142">For **Name**, provide a name for the connection.</span></span>
   * <span data-ttu-id="1f36d-143">İçin **ana bilgisayar adı**, kaynağınızın barındıran şirket içi bilgisayarın adını girin.</span><span class="sxs-lookup"><span data-stu-id="1f36d-143">For **Hostname**, enter the name of the on-premises computer that hosts your resource.</span></span>
   * <span data-ttu-id="1f36d-144">İçin **bağlantı noktası**, şirket içi kaynağa (1433 SQL Server varsayılan bir örnek için) kullandığı bağlantı noktası numarası girin.</span><span class="sxs-lookup"><span data-stu-id="1f36d-144">For **Port**, enter the port number that your on-premises resource uses (1433 for a SQL Server default instance).</span></span>
   * <span data-ttu-id="1f36d-145">Tıklatın **Biz konuşması hizmeti**</span><span class="sxs-lookup"><span data-stu-id="1f36d-145">Click **Biz Talk Service**</span></span>
4. <span data-ttu-id="1f36d-146">**BizTalk hizmeti oluşturma** dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="1f36d-146">The **Create BizTalk Service** blade opens.</span></span> <span data-ttu-id="1f36d-147">BizTalk hizmeti için bir ad girin ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="1f36d-147">Enter a name for the BizTalk service, and then click **OK**.</span></span>
   
    ![BizTalk hizmeti oluşturma][CreateHCCreateBTS]
   
    <span data-ttu-id="1f36d-149">**BizTalk hizmeti oluşturma** dikey penceresi kapanır ve döndürülürsünüz **karma bağlantı oluşturmak** dikey.</span><span class="sxs-lookup"><span data-stu-id="1f36d-149">The **Create BizTalk Service** blade closes and you are returned to the **Create hybrid connection** blade.</span></span>
5. <span data-ttu-id="1f36d-150">Create karma bağlantı dikey penceresinde **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="1f36d-150">On the Create hybrid connection blade, click **OK**.</span></span> 
   
    ![Tamam'ı tıklatın][CreateBTScomplete]
6. <span data-ttu-id="1f36d-152">İşlem tamamlandığında, Portal bildirimleri alanında bağlantı başarıyla oluşturuldu bildirir.</span><span class="sxs-lookup"><span data-stu-id="1f36d-152">When the process completes, the notifications area in the Portal informs you that the connection has been successfully created.</span></span>
   
    <!--- TODO
   
    Everything fails at this step. I can't create a BizTalk service in the dogfood portal. I switch to the classic portal
    (full portal) and created the BizTalk service but it doesn't seem to let you connnect them - When you finish the
    Create hybrid conn step, you get the following error
    Failed to create hybrid connection RelecIoudHC. The 
    resource type could not be found in the namespace 
    'Microsoft.BizTaIkServices for api version 2014-06-01'.
   
    The error indicates it couldn't find the type, not the instance.
    ![Success notification][CreateHCSuccessNotification]
    -->
7. <span data-ttu-id="1f36d-153">Web uygulamanızın dikey penceresinde, **karma bağlantılar** simgesi artık gösterir 1 karma bağlantı oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="1f36d-153">On the web app's blade, the **Hybrid connections** icon now shows that 1 hybrid connection has been created.</span></span>
   
    ![Oluşturulan bir karma bağlantı][CreateHCOneConnectionCreated]

<span data-ttu-id="1f36d-155">Bu noktada, bulut karma bağlantı altyapı önemli bir kısmını tamamladınız.</span><span class="sxs-lookup"><span data-stu-id="1f36d-155">At this point, you have completed an important part of the cloud hybrid connection infrastructure.</span></span> <span data-ttu-id="1f36d-156">Ardından, karşılık gelen bir şirket içi parça oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1f36d-156">Next, you will create a corresponding on-premises piece.</span></span>

<a name="InstallHCM"></a>

## <a name="install-the-on-premises-hybrid-connection-manager-to-complete-the-connection"></a><span data-ttu-id="1f36d-157">Bağlantıyı tamamlamak için şirket içi karma Bağlantı Yöneticisi'ni yükleyin</span><span class="sxs-lookup"><span data-stu-id="1f36d-157">Install the on-premises Hybrid Connection Manager to complete the connection</span></span>
1. <span data-ttu-id="1f36d-158">Web uygulamanızın dikey penceresinde **tüm ayarları** > **ağ** > **karma bağlantı uç noktalarınızı yapılandırın**.</span><span class="sxs-lookup"><span data-stu-id="1f36d-158">On the web app's blade, click **All settings** > **Networking** > **Configure your hybrid connection endpoints**.</span></span> 
   
    ![Karma bağlantıları simgesi][HCIcon]
2. <span data-ttu-id="1f36d-160">Üzerinde **karma bağlantılar** dikey penceresinde **durum** sütun için en son eklenen uç nokta gösterir **bağlı**.</span><span class="sxs-lookup"><span data-stu-id="1f36d-160">On the **Hybrid connections** blade, the **Status** column for the recently added endpoint shows **Not connected**.</span></span> <span data-ttu-id="1f36d-161">Yapılandırmak için bağlantıyı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="1f36d-161">Click the connection to configure it.</span></span>
   
    ![Bağlı değil][NotConnected]
   
    <span data-ttu-id="1f36d-163">Karma bağlantı dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="1f36d-163">The Hybrid connection blade opens.</span></span>
   
    ![NotConnectedBlade][NotConnectedBlade]
3. <span data-ttu-id="1f36d-165">Dikey penceresinde **dinleyicisi Kur**.</span><span class="sxs-lookup"><span data-stu-id="1f36d-165">On the blade, click **Listener Setup**.</span></span>
   
    ![Dinleyici Kur'a tıklayın][ClickListenerSetup]
4. <span data-ttu-id="1f36d-167">**Karma bağlantı özelliklerini** dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="1f36d-167">The **Hybrid connection properties** blade opens.</span></span> <span data-ttu-id="1f36d-168">Altında **şirket içi karma Bağlantı Yöneticisi**, seçin **yüklemek için burayı tıklatın**.</span><span class="sxs-lookup"><span data-stu-id="1f36d-168">Under **On-premises Hybrid Connection Manager**, choose **Click here to install**.</span></span>
   
    ![Yüklemek için burayı tıklatın][ClickToInstallHCM]
5. <span data-ttu-id="1f36d-170">Uygulamayı çalıştırmak Güvenlik Uyarısı iletişim kutusunda seçin **çalıştırmak** devam etmek için.</span><span class="sxs-lookup"><span data-stu-id="1f36d-170">In the Application Run security warning dialog, choose **Run** to continue.</span></span>
   
    ![Devam etmek için Çalıştır'ı seçin][ApplicationRunWarning]
6. <span data-ttu-id="1f36d-172">İçinde **kullanıcı hesabı denetimi** iletişim kutusunda, seçin **Evet**.</span><span class="sxs-lookup"><span data-stu-id="1f36d-172">In the **User Account Control** dialog, choose **Yes**.</span></span>
   
   ![Evet'i seçin][UAC]
7. <span data-ttu-id="1f36d-174">Karma Bağlantı Yöneticisi'ni indirilen ve yüklenmiş.</span><span class="sxs-lookup"><span data-stu-id="1f36d-174">The Hybrid Connection Manager is downloaded and installed for you.</span></span> 
   
    ![Yükleme][HCMInstalling]
8. <span data-ttu-id="1f36d-176">Yükleme tamamlandığında tıklayın **Kapat**.</span><span class="sxs-lookup"><span data-stu-id="1f36d-176">When the install completes, click **Close**.</span></span>
   
    ![Kapat'ı tıklatın][HCMInstallComplete]
   
    <span data-ttu-id="1f36d-178">Üzerinde **karma bağlantılar** dikey penceresinde **durum** sütun şimdi gösterir **bağlı**.</span><span class="sxs-lookup"><span data-stu-id="1f36d-178">On the **Hybrid connections** blade, the **Status** column now shows **Connected**.</span></span> 
   
    ![Bağlı durumu][HCStatusConnected]

<span data-ttu-id="1f36d-180">Karma bağlantı altyapı tamamlandığına göre bunu kullanan bir karma uygulama oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1f36d-180">Now that the hybrid connection infrastructure is complete, you can create a hybrid application that uses it.</span></span> 

> [!NOTE]
> <span data-ttu-id="1f36d-181">Aşağıdaki bölümlerde, Mobile Apps .NET arka uç projesi ile karma bağlantı kullanmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="1f36d-181">The following sections show you how to use a hybrid connection with a Mobile Apps .NET backend project.</span></span>
> 
> 

## <a name="configure-the-mobile-app-net-backend-project-to-connect-to-the-sql-server-database"></a><span data-ttu-id="1f36d-182">SQL Server veritabanına bağlanmak için mobil uygulama .NET arka uç projesini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="1f36d-182">Configure the Mobile App .NET backend project to connect to the SQL Server database</span></span>
<span data-ttu-id="1f36d-183">App Service'de Mobile Apps .NET arka uç projesi yalnızca ASP.NET web uygulamasını bir ek Mobile Apps yüklenmiş ve başlatılmış SDK'sı ' dir.</span><span class="sxs-lookup"><span data-stu-id="1f36d-183">In App Service, a Mobile Apps .NET backend project is just an ASP.NET web app with an additional Mobile Apps SDK installed and initialized.</span></span> <span data-ttu-id="1f36d-184">Web uygulamanızı Mobile Apps arka ucu olarak kullanmak için şunları yapmalısınız [karşıdan yüklemek ve mobil uygulamaları .NET arka ucu SDK başlatma](../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#install-sdk).</span><span class="sxs-lookup"><span data-stu-id="1f36d-184">To use your web app as a Mobile Apps backend, you must [download and initialize the Mobile Apps .NET backend SDK](../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#install-sdk).</span></span>  

<span data-ttu-id="1f36d-185">Mobil uygulamalar için ayrıca şirket içi veritabanına bir bağlantı dizesi tanımlayın ve bu bağlantıyı kullanmak için arka uç değiştirmek gerekir.</span><span class="sxs-lookup"><span data-stu-id="1f36d-185">For Mobile Apps, you also need to define a connection string for the on-premises database and modify the backend to use this connection.</span></span> 

1. <span data-ttu-id="1f36d-186">Visual Studio'da Çözüm Gezgini'nde, mobil uygulama .NET arka ucu için Web.config dosyasını açın, bulun **connectionStrings** bölümünde, yeni bir SqlClient giriş şirket içi SQL Server veritabanına işaret eden aşağıdaki gibi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="1f36d-186">In Solution Explorer in Visual Studio, open the Web.config file for your Mobile App .NET backend, locate the **connectionStrings** section, add a new SqlClient entry like the following, which points to the on-premises SQL Server database:</span></span>
   
        <add name="OnPremisesDBConnection"
         connectionString="Data Source=OnPremisesServer,1433;
         Initial Catalog=OnPremisesDB;
         User ID=HybridConnectionLogin;
         Password=<**secure_password**>;
         MultipleActiveResultSets=True"
         providerName="System.Data.SqlClient" />
   
    <span data-ttu-id="1f36d-187">Değiştirilecek unutmayın `<**secure_password**>` için oluşturduğunuz parola ile bu dizesinde *HybridConnectionLogin*.</span><span class="sxs-lookup"><span data-stu-id="1f36d-187">Remember to replace `<**secure_password**>` in this string with the password you created for  *HybridConnectionLogin*.</span></span>
2. <span data-ttu-id="1f36d-188">Tıklatın **kaydetmek** Web.config dosyasını kaydetmek için Visual Studio'da.</span><span class="sxs-lookup"><span data-stu-id="1f36d-188">Click **Save** in Visual Studio to save the Web.config file.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="1f36d-189">Bu bağlantı ayarı, yerel bilgisayarda çalışırken kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1f36d-189">This connection setting is used when running on the local computer.</span></span> <span data-ttu-id="1f36d-190">Azure üzerinde çalışırken, bu ayarı geçersiz kılınmadı Portalı'nda tanımlanan bağlantı ayarlayarak.</span><span class="sxs-lookup"><span data-stu-id="1f36d-190">When running in Azure, this setting is overriden by the connection setting defined in the portal.</span></span>
   > 
   > 
3. <span data-ttu-id="1f36d-191">Genişletme **modelleri** klasörü ve açık ile biten veri modeli dosyası *Context.cs*.</span><span class="sxs-lookup"><span data-stu-id="1f36d-191">Expand the **Models** folder and open the data model file, which ends in *Context.cs*.</span></span>
4. <span data-ttu-id="1f36d-192">Değiştirme **DbContext** değeri geçirmek için örnek oluşturucusu `OnPremisesDBConnection` bankasına **DbContext** oluşturucusu, aşağıdaki kod parçacığını benzer:</span><span class="sxs-lookup"><span data-stu-id="1f36d-192">Modify the **DbContext** instance constructor to pass the value `OnPremisesDBConnection` to the base **DbContext** constructor, similar to the following snippet:</span></span>
   
        public class hybridService1Context : DbContext
        {
            public hybridService1Context()
                : base("OnPremisesDBConnection")
            {
            }
        }
   
    <span data-ttu-id="1f36d-193">Hizmeti artık yeni SQL Server veritabanına bağlantı kullanır.</span><span class="sxs-lookup"><span data-stu-id="1f36d-193">The service will now use the new connection to the SQL Server database.</span></span>

## <a name="update-the-mobile-app-backend-to-use-the-on-premises-connection-string"></a><span data-ttu-id="1f36d-194">Şirket içi bağlantı dizesi kullanmak için mobil uygulama arka ucu güncelleştir</span><span class="sxs-lookup"><span data-stu-id="1f36d-194">Update the Mobile App backend to use the on-premises connection string</span></span>
<span data-ttu-id="1f36d-195">Ardından, böylece Azure'dan kullanılabilmesi için bu yeni bağlantı dizesi için bir uygulama ayarı eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1f36d-195">Next, you need to add an app setting for this new connection string so that it can be used from Azure.</span></span>  

1. <span data-ttu-id="1f36d-196">Geri [Azure portal](https://portal.azure.com) mobil uygulamanızın web app arka uç kodu içini tıklatın **tüm ayarları**, ardından **uygulama ayarları**.</span><span class="sxs-lookup"><span data-stu-id="1f36d-196">Back in the [Azure portal](https://portal.azure.com) in the web app backend code for your Mobile App, click **All settings**, then **Application settings**.</span></span>
2. <span data-ttu-id="1f36d-197">İçinde **Web uygulaması ayarları** dikey penceresinde, aşağı kaydırın **bağlantı dizeleri** ve yeni bir ekleme **SQL Server** adlı bağlantı dizesi `OnPremisesDBConnection` gibi bir değerle `Server=OnPremisesServer,1433;Database=OnPremisesDB;User ID=HybridConnectionsLogin;Password=<**secure_password**>`.</span><span class="sxs-lookup"><span data-stu-id="1f36d-197">In the **Web app settings** blade, scroll down to **Connection strings** and add an new **SQL Server** connection string named `OnPremisesDBConnection` with a value like `Server=OnPremisesServer,1433;Database=OnPremisesDB;User ID=HybridConnectionsLogin;Password=<**secure_password**>`.</span></span>
   
    <span data-ttu-id="1f36d-198">Değiştir `<**secure_password**>` şirket içi veritabanınız için güvenli parola ile.</span><span class="sxs-lookup"><span data-stu-id="1f36d-198">Replace `<**secure_password**>` with the secure password for your on-premises database.</span></span>
   
    ![Şirket içi veritabanı için bağlantı dizesi](./media/web-sites-hybrid-connection-get-started/set-sql-server-database-connection.png)
3. <span data-ttu-id="1f36d-200">Tuşuna **kaydetmek** karma kaydetmek için bağlantı ve bağlantı, yeni oluşturduğunuz dize.</span><span class="sxs-lookup"><span data-stu-id="1f36d-200">Press **Save** to save the hybrid connection and connection string you just created.</span></span>

<span data-ttu-id="1f36d-201">Bu noktada sunucu projesi yeniden yayımlamanız ve mevcut Mobile Apps istemcileriniz ile yeni bağlantıyı sınayın.</span><span class="sxs-lookup"><span data-stu-id="1f36d-201">At this point you can republish the server project and test the new connection with your existing Mobile Apps clients.</span></span> <span data-ttu-id="1f36d-202">Veri okuma ve karma bağlantıyı kullanarak şirket içi veritabanına yazılır.</span><span class="sxs-lookup"><span data-stu-id="1f36d-202">Data will be read from and written to the on-premises database using the hybrid connection.</span></span>

<a name="NextSteps"></a>

## <a name="next-steps"></a><span data-ttu-id="1f36d-203">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="1f36d-203">Next Steps</span></span>
* <span data-ttu-id="1f36d-204">Karma bağlantı kullanan bir ASP.NET web uygulaması oluşturma hakkında daha fazla bilgi için bkz: [karma bağlantılar kullanarak bir Azure web sitesinden bir şirket içi SQL Server'a Bağlan](http://go.microsoft.com/fwlink/?LinkID=397979).</span><span class="sxs-lookup"><span data-stu-id="1f36d-204">For information on creating an ASP.NET web application that uses a hybrid connection, see [Connect to an on-premises SQL Server from an Azure web site using Hybrid Connections](http://go.microsoft.com/fwlink/?LinkID=397979).</span></span> 

### <a name="additional-resources"></a><span data-ttu-id="1f36d-205">Ek Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="1f36d-205">Additional Resources</span></span>
[<span data-ttu-id="1f36d-206">Karma Bağlantılara genel bakış</span><span class="sxs-lookup"><span data-stu-id="1f36d-206">Hybrid Connections overview</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=397274)

[<span data-ttu-id="1f36d-207">Karma bağlantılar (Channel 9 video) Josh geçiş sunar</span><span class="sxs-lookup"><span data-stu-id="1f36d-207">Josh Twist introduces hybrid connections (Channel 9 video)</span></span>](http://channel9.msdn.com/Shows/Azure-Friday/Josh-Twist-introduces-hybrid-connections)

[<span data-ttu-id="1f36d-208">Karma bağlantılar web sitesi</span><span class="sxs-lookup"><span data-stu-id="1f36d-208">Hybrid Connections web site</span></span>](https://azure.microsoft.com/services/biztalk-services/)

[<span data-ttu-id="1f36d-209">BizTalk Services: Pano, İzleyici, Ölçek, yapılandırma ve karma bağlantı sekmeleri</span><span class="sxs-lookup"><span data-stu-id="1f36d-209">BizTalk Services: Dashboard, Monitor, Scale, Configure, and Hybrid Connection tabs</span></span>](../biztalk-services/biztalk-dashboard-monitor-scale-tabs.md)

[<span data-ttu-id="1f36d-210">Gerçek dünya karma bir buluta sorunsuz uygulama taşıma (Channel 9 video) ile oluşturma</span><span class="sxs-lookup"><span data-stu-id="1f36d-210">Building a Real-World Hybrid Cloud with Seamless Application Portability (Channel 9 video)</span></span>](http://channel9.msdn.com/events/TechEd/NorthAmerica/2014/DCIM-B323#fbid=)

[<span data-ttu-id="1f36d-211">Azure Mobile Services karma bağlantılar (Channel 9 video) kullanarak bir şirket içi SQL Server'a bağlanma</span><span class="sxs-lookup"><span data-stu-id="1f36d-211">Connect to an on-premises SQL Server from Azure Mobile Services using Hybrid Connections (Channel 9 video)</span></span>](http://channel9.msdn.com/Series/Windows-Azure-Mobile-Services/Connect-to-an-on-premises-SQL-Server-from-Azure-Mobile-Services-using-Hybrid-Connections)

## <a name="whats-changed"></a><span data-ttu-id="1f36d-212">Yapılan değişiklikler</span><span class="sxs-lookup"><span data-stu-id="1f36d-212">What's changed</span></span>
* <span data-ttu-id="1f36d-213">Web Sitelerinden App Service’e kadar değiştirme kılavuzu için bkz. [Azure App Service ve Mevcut Azure Hizmetlerine Etkileri](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="1f36d-213">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- IMAGES -->
[New]:./media/web-sites-hybrid-connection-get-started/B01New.png
[NewWebsite]:./media/web-sites-hybrid-connection-get-started/B02NewWebsite.png
[WebsiteCreationBlade]:./media/web-sites-hybrid-connection-get-started/B03WebsiteCreationBlade.png
[WebSiteRunningBlade]:./media/web-sites-hybrid-connection-get-started/B04WebSiteRunningBlade.png
[Browse]:./media/web-sites-hybrid-connection-get-started/B05Browse.png
[DefaultWebSitePage]:./media/web-sites-hybrid-connection-get-started/B06DefaultWebSitePage.png
[CreateHCHCIcon]:./media/web-sites-hybrid-connection-get-started/C01CreateHCHCIcon.png
[CreateHCAddHC]:./media/web-sites-hybrid-connection-get-started/C02CreateHCAddHC.png
[TwinCreateHCBlades]:./media/web-sites-hybrid-connection-get-started/C03TwinCreateHCBlades.png
[CreateHCCreateBTS]:./media/web-sites-hybrid-connection-get-started/C04CreateHCCreateBTS.png
[CreateBTScomplete]:./media/web-sites-hybrid-connection-get-started/C05CreateBTScomplete.png
[CreateHCSuccessNotification]:./media/web-sites-hybrid-connection-get-started/C06CreateHCSuccessNotification.png
[CreateHCOneConnectionCreated]:./media/web-sites-hybrid-connection-get-started/C07CreateHCOneConnectionCreated.png
[HCIcon]:./media/web-sites-hybrid-connection-get-started/D01HCIcon.png
[NotConnected]:./media/web-sites-hybrid-connection-get-started/D02NotConnected.png
[NotConnectedBlade]:./media/web-sites-hybrid-connection-get-started/D03NotConnectedBlade.png
[ClickListenerSetup]:./media/web-sites-hybrid-connection-get-started/D04ClickListenerSetup.png
[ClickToInstallHCM]:./media/web-sites-hybrid-connection-get-started/D05ClickToInstallHCM.png
[ApplicationRunWarning]:./media/web-sites-hybrid-connection-get-started/D06ApplicationRunWarning.png
[UAC]:./media/web-sites-hybrid-connection-get-started/D07UAC.png
[HCMInstalling]:./media/web-sites-hybrid-connection-get-started/D08HCMInstalling.png
[HCMInstallComplete]:./media/web-sites-hybrid-connection-get-started/D09HCMInstallComplete.png
[HCStatusConnected]:./media/web-sites-hybrid-connection-get-started/D10HCStatusConnected.png
