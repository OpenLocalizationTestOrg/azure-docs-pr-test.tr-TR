---
title: ".NET ile Media Services geliştirmeye yönelik bilgisayar kurma"
description: ".NET için Media Services SDK'sını kullanarak Media Services önkoşulları hakkında bilgi edinin. Ayrıca Visual Studio uygulamasının nasıl oluşturulacağını öğrenin."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: ec2804c7-c656-4fbf-b3e4-3f0f78599a7f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/23/2017
ms.author: juliako
ms.openlocfilehash: 15828bc74937a036871b26493498232ec7cf6f06
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="media-services-development-with-net"></a><span data-ttu-id="99ebc-104">.NET ile Media Services Geliştirme</span><span class="sxs-lookup"><span data-stu-id="99ebc-104">Media Services development with .NET</span></span>
[!INCLUDE [media-services-selector-setup](../../includes/media-services-selector-setup.md)]

<span data-ttu-id="99ebc-105">Bu konuda .NET kullanarak Media Services uygulamaları geliştirmeye başlamak nasıl ele alınmıştır.</span><span class="sxs-lookup"><span data-stu-id="99ebc-105">This topic discusses how to start developing Media Services applications using .NET.</span></span>

<span data-ttu-id="99ebc-106">**Azure Media Services .NET SDK'sı** kitaplığı .NET kullanarak Media Services karşı program olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="99ebc-106">The **Azure Media Services .NET SDK** library enables you to program against Media Services using .NET.</span></span> <span data-ttu-id="99ebc-107">.NET ile geliştirmek daha kolay hale getirmek için **Azure Media Services .NET SDK uzantıları** kitaplığı sağlanır.</span><span class="sxs-lookup"><span data-stu-id="99ebc-107">To make it even easier to develop with .NET, the **Azure Media Services .NET SDK Extensions** library is provided.</span></span> <span data-ttu-id="99ebc-108">Bu kitaplığı bir dizi genişletme yöntemleri ve .NET kodunuzu basitleştirmeye yardımcı işlevlerini içerir.</span><span class="sxs-lookup"><span data-stu-id="99ebc-108">This library contains a set of extension methods and helper functions that simplify your .NET code.</span></span> <span data-ttu-id="99ebc-109">Her iki kitaplıkları aracılığıyla kullanılabilir **NuGet** ve **GitHub**.</span><span class="sxs-lookup"><span data-stu-id="99ebc-109">Both libraries are available through **NuGet** and **GitHub**.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="99ebc-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="99ebc-110">Prerequisites</span></span>
* <span data-ttu-id="99ebc-111">Yeni veya mevcut bir Azure aboneliğinde bir Media Services hesabı.</span><span class="sxs-lookup"><span data-stu-id="99ebc-111">A Media Services account in a new or existing Azure subscription.</span></span> <span data-ttu-id="99ebc-112">[Media Services Hesabı Oluşturma](media-services-portal-create-account.md) konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="99ebc-112">See the topic [How to Create a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="99ebc-113">İşletim sistemleri: Windows 10, Windows 7, Windows 2008 R2 veya Windows 8.</span><span class="sxs-lookup"><span data-stu-id="99ebc-113">Operating Systems: Windows 10, Windows 7, Windows 2008 R2, or Windows 8.</span></span>
* <span data-ttu-id="99ebc-114">.NET framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="99ebc-114">.NET Framework 4.5.</span></span>
* <span data-ttu-id="99ebc-115">Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="99ebc-115">Visual Studio.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="99ebc-116">Visual Studio projesi oluşturup yapılandırma</span><span class="sxs-lookup"><span data-stu-id="99ebc-116">Create and configure a Visual Studio project</span></span>
<span data-ttu-id="99ebc-117">Bu bölümde Visual Studio'da bir proje oluşturun ve Media Services geliştirmeye kaydınızı ayarlayın gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="99ebc-117">This section shows you how to create a project in Visual Studio and set it up for Media Services development.</span></span>  <span data-ttu-id="99ebc-118">Bu durumda, bir C# Windows konsol uygulaması projedir, ancak diğer Media Services uygulamalar (örneğin, bir Windows Forms uygulaması veya bir ASP.NET Web uygulaması) için oluşturabileceğiniz proje türleri için burada gösterilen aynı kurulum adımlarını uygulayın.</span><span class="sxs-lookup"><span data-stu-id="99ebc-118">In this case, the project is a C# Windows console application, but the same setup steps shown here apply to other types of projects you can create for Media Services applications (for example, a Windows Forms application or an ASP.NET Web application).</span></span>

<span data-ttu-id="99ebc-119">Bu bölümde nasıl kullanılacağını gösterir **NuGet** Media Services .NET SDK uzantıları ve diğer bağımlı kitaplıkları eklemek için.</span><span class="sxs-lookup"><span data-stu-id="99ebc-119">This section shows how to use **NuGet** to add Media Services .NET SDK extensions and other dependent libraries.</span></span>

<span data-ttu-id="99ebc-120">Alternatif olarak, en son Media Services .NET SDK'sı BITS Github'dan alabilirsiniz ([github.com/Azure/azure-sdk-for-media-services](https://github.com/Azure/azure-sdk-for-media-services) veya [github.com/Azure/azure-sdk-for-media-services-extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions)) çözümü oluşturun ve istemci proje başvuruları ekleyin.</span><span class="sxs-lookup"><span data-stu-id="99ebc-120">Alternatively, you can get the latest Media Services .NET SDK bits from GitHub ([github.com/Azure/azure-sdk-for-media-services](https://github.com/Azure/azure-sdk-for-media-services) or [github.com/Azure/azure-sdk-for-media-services-extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions)), build the solution, and add the references to the client project.</span></span> <span data-ttu-id="99ebc-121">Gerekli tüm bağımlılıkları indirilir ve otomatik olarak ayıklanan.</span><span class="sxs-lookup"><span data-stu-id="99ebc-121">All the necessary dependencies get downloaded and extracted automatically.</span></span>

1. <span data-ttu-id="99ebc-122">Visual Studio’da yeni bir C# Konsol Uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="99ebc-122">Create a new C# Console Application in Visual Studio.</span></span> <span data-ttu-id="99ebc-123">Girin **adı**, **konumu**, ve **çözüm adı**ve ardından Tamam'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="99ebc-123">Enter the **Name**, **Location**, and **Solution name**, and then click OK.</span></span>
2. <span data-ttu-id="99ebc-124">Çözümü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="99ebc-124">Build the solution.</span></span>
3. <span data-ttu-id="99ebc-125">Kullanım **NuGet** yükleme ve ekleme **Azure Media Services .NET SDK uzantıları** (**windowsazure.mediaservices.extensions**).</span><span class="sxs-lookup"><span data-stu-id="99ebc-125">Use **NuGet** to install and add **Azure Media Services .NET SDK Extensions** (**windowsazure.mediaservices.extensions**).</span></span> <span data-ttu-id="99ebc-126">Bu paketin yüklenmesiyle **Media Services .NET SDK** da yüklenir ve diğer tüm gerekli bağımlılıklar eklenir.</span><span class="sxs-lookup"><span data-stu-id="99ebc-126">Installing this package, also installs **Media Services .NET SDK** and adds all other required dependencies.</span></span>
   
    <span data-ttu-id="99ebc-127">En yeni sürümünü NuGet yüklü olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="99ebc-127">Ensure that you have the newest version of NuGet installed.</span></span> <span data-ttu-id="99ebc-128">Daha fazla bilgi ve yükleme yönergeleri için bkz: [NuGet](http://nuget.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="99ebc-128">For more information and installation instructions, see [NuGet](http://nuget.codeplex.com/).</span></span>
4. <span data-ttu-id="99ebc-129">Çözüm Gezgini'nde proje adına sağ tıklayın ve Manage NuGet paketleri seçin.</span><span class="sxs-lookup"><span data-stu-id="99ebc-129">In Solution Explorer, right-click the name of the project and choose Manage NuGet packages.</span></span>
   
    <span data-ttu-id="99ebc-130">NuGet paketlerini Yönet iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="99ebc-130">The Manage NuGet Packages dialog box appears.</span></span>
5. <span data-ttu-id="99ebc-131">Çevrimiçi Galeri Azure MediaServices uzantıları için arama, Azure Media Services .NET SDK uzantıları seçin ve ardından yükle düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="99ebc-131">In the Online gallery, search for Azure MediaServices Extensions, choose Azure Media Services .NET SDK Extensions, and then click the Install button.</span></span>
   
    <span data-ttu-id="99ebc-132">Proje değiştirilebilir ve Media Services .NET SDK uzantıları, Media Services .NET SDK'sı ve diğer bağımlı derlemelerden başvuruları eklenir.</span><span class="sxs-lookup"><span data-stu-id="99ebc-132">The project is modified and references to the Media Services .NET SDK Extensions,  Media Services .NET SDK, and other dependent assemblies are added.</span></span>
6. <span data-ttu-id="99ebc-133">Temizleyici bir geliştirme ortamı yükseltmek için NuGet paketi geri yüklemeyi etkinleştirme göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="99ebc-133">To promote a cleaner development environment, consider enabling NuGet Package Restore.</span></span> <span data-ttu-id="99ebc-134">Daha fazla bilgi için bkz: [NuGet paket geri yükleme "](http://docs.nuget.org/consume/package-restore).</span><span class="sxs-lookup"><span data-stu-id="99ebc-134">For more information, see [NuGet Package Restore"](http://docs.nuget.org/consume/package-restore).</span></span>
7. <span data-ttu-id="99ebc-135">Bir başvuru ekleyin **System.Configuration** derleme.</span><span class="sxs-lookup"><span data-stu-id="99ebc-135">Add a reference to **System.Configuration** assembly.</span></span> <span data-ttu-id="99ebc-136">Bu derleme System.Configuration içerir. **ConfigurationManager** yapılandırma dosyaları (örneğin, App.config) erişmek için kullanılan sınıf.</span><span class="sxs-lookup"><span data-stu-id="99ebc-136">This assembly contains the System.Configuration.**ConfigurationManager** class that is used to access configuration files (for example, App.config).</span></span>
   
    <span data-ttu-id="99ebc-137">Başvuruları Yönet iletişim kutusunu kullanarak başvurular eklemek için Çözüm Gezgini'nde proje adına sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="99ebc-137">To add references using the Manage References dialog, right-click the project name in the Solution Explorer.</span></span> <span data-ttu-id="99ebc-138">Ardından, Ekle ve başvurular seçin.</span><span class="sxs-lookup"><span data-stu-id="99ebc-138">Then, select Add and References.</span></span>
   
    <span data-ttu-id="99ebc-139">Başvuruları Yönet iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="99ebc-139">The Manage References dialog appears.</span></span>
8. <span data-ttu-id="99ebc-140">.NET framework derlemeleri altındaki bulmak ve System.Configuration derleme seçin ve Tamam'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="99ebc-140">Under .NET framework assemblies, find and select the System.Configuration assembly and press OK.</span></span>
9. <span data-ttu-id="99ebc-141">App.config dosyasını açın ve eklemek bir *appSettings* dosyaya bölümü.</span><span class="sxs-lookup"><span data-stu-id="99ebc-141">Open the App.config file and add an *appSettings* section to the file.</span></span>     
   
    <span data-ttu-id="99ebc-142">Medya Hizmetleri API'sine bağlanmak için gereken değerleri ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="99ebc-142">Set the values that are needed to connect to the Media Services API.</span></span> <span data-ttu-id="99ebc-143">Daha fazla bilgi için bkz: [Azure AD kimlik doğrulaması ile Azure Media Services API erişim](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="99ebc-143">For more information, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

    <span data-ttu-id="99ebc-144">Kullanıyorsanız [kullanıcı kimlik doğrulaması](media-services-use-aad-auth-to-access-ams-api.md#types-of-authentication) yapılandırma dosyası büyük olasılıkla, Azure AD Kiracı etki alanı ve AMS REST API uç noktası için değerlere sahip olur.</span><span class="sxs-lookup"><span data-stu-id="99ebc-144">If you are using [user authentication](media-services-use-aad-auth-to-access-ams-api.md#types-of-authentication) your config file will probably have values for your Azure AD tenant domain and the AMS REST API endpoint.</span></span>
    
    >[!Important]
    ><span data-ttu-id="99ebc-145">Azure Media Services belgelerinde çoğu kod örnekleri kümesi, AMS API'sine bağlanmak için kimlik doğrulama kullanıcı (etkileşimli) türünü kullanın.</span><span class="sxs-lookup"><span data-stu-id="99ebc-145">Most code samples in the Azure Media Services documentation set, use a user (interactive) type of authentication to connect to the AMS API.</span></span> <span data-ttu-id="99ebc-146">Bu kimlik doğrulama yöntemini de yönetim veya yerel uygulamalar izleme için çalışır: mobil uygulamaları, Windows uygulamaları ve konsol uygulamaları.</span><span class="sxs-lookup"><span data-stu-id="99ebc-146">This authentication method will work well for management or monitoring native apps: mobile apps, Windows apps, and Console applications.</span></span> <span data-ttu-id="99ebc-147">Bu kimlik doğrulama yöntemi, sunucu, web Hizmetleri, uygulamaları API'leri türü için uygun değil.</span><span class="sxs-lookup"><span data-stu-id="99ebc-147">This authentication method is not suitable for server, web services, APIs type of applications.</span></span>  <span data-ttu-id="99ebc-148">Daha fazla bilgi için bkz: [Azure AD kimlik doğrulaması ile AMS API'sine erişim](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="99ebc-148">For more information, see [Access the AMS API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span>

        <configuration>
        ...
            <appSettings>
              <add key="AADTenantDomain" value="YourAADTenantDomain" />
              <add key="MediaServiceRESTAPIEndpoint" value="YourRESTAPIEndpoint" />
            </appSettings>

        </configuration>

10. <span data-ttu-id="99ebc-149">Aşağıdaki kodu, Program.cs dosyasının başındaki mevcut **using** deyimlerinin üzerine yazın.</span><span class="sxs-lookup"><span data-stu-id="99ebc-149">Overwrite the existing **using** statements at the beginning of the Program.cs file with the following code.</span></span>
           
        using System;
        using System.Configuration;
        using System.IO;
        using Microsoft.WindowsAzure.MediaServices.Client;
        using System.Threading;
        using System.Collections.Generic;
        using System.Linq;

<span data-ttu-id="99ebc-150">Bu noktada, Media Services uygulama geliştirmeye başlamak hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="99ebc-150">At this point, you are ready to start developing a Media Services application.</span></span>    

## <a name="example"></a><span data-ttu-id="99ebc-151">Örnek</span><span class="sxs-lookup"><span data-stu-id="99ebc-151">Example</span></span>

<span data-ttu-id="99ebc-152">Aşağıda AMS API'sine bağlanır ve tüm kullanılabilir medya işlemcileri listeler küçük bir örnek verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="99ebc-152">Here is a small example that connects to the AMS API and lists all available Media Processors.</span></span>
    
    class Program
    {
        // Read values from the App.config file.
        private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];
    
        private static CloudMediaContext _context = null;
        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
    
            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);
    
            // List all available Media Processors
            foreach (var mp in _context.MediaProcessors)
            {
                Console.WriteLine(mp.Name);
            }
    
        }

##<a name="next-steps"></a><span data-ttu-id="99ebc-153">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="99ebc-153">Next steps</span></span>

<span data-ttu-id="99ebc-154">Şimdi [AMS API'sine bağlanabilir](media-services-use-aad-auth-to-access-ams-api.md) ve başlangıç [geliştirme](media-services-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="99ebc-154">Now [you can connect to the AMS API](media-services-use-aad-auth-to-access-ams-api.md) and start [developing](media-services-dotnet-get-started.md).</span></span>


## <a name="media-services-learning-paths"></a><span data-ttu-id="99ebc-155">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="99ebc-155">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="99ebc-156">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="99ebc-156">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

