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
# <a name="media-services-development-with-net"></a>.NET ile Media Services Geliştirme
[!INCLUDE [media-services-selector-setup](../../includes/media-services-selector-setup.md)]

Bu konuda .NET kullanarak Media Services uygulamaları geliştirmeye başlamak nasıl ele alınmıştır.

**Azure Media Services .NET SDK'sı** kitaplığı .NET kullanarak Media Services karşı program olanak sağlar. .NET ile geliştirmek daha kolay hale getirmek için **Azure Media Services .NET SDK uzantıları** kitaplığı sağlanır. Bu kitaplığı bir dizi genişletme yöntemleri ve .NET kodunuzu basitleştirmeye yardımcı işlevlerini içerir. Her iki kitaplıkları aracılığıyla kullanılabilir **NuGet** ve **GitHub**.

## <a name="prerequisites"></a>Ön koşullar
* Yeni veya mevcut bir Azure aboneliğinde bir Media Services hesabı. [Media Services Hesabı Oluşturma](media-services-portal-create-account.md) konusuna bakın.
* İşletim sistemleri: Windows 10, Windows 7, Windows 2008 R2 veya Windows 8.
* .NET framework 4.5.
* Visual Studio.

## <a name="create-and-configure-a-visual-studio-project"></a>Visual Studio projesi oluşturup yapılandırma
Bu bölümde Visual Studio'da bir proje oluşturun ve Media Services geliştirmeye kaydınızı ayarlayın gösterilmektedir.  Bu durumda, bir C# Windows konsol uygulaması projedir, ancak diğer Media Services uygulamalar (örneğin, bir Windows Forms uygulaması veya bir ASP.NET Web uygulaması) için oluşturabileceğiniz proje türleri için burada gösterilen aynı kurulum adımlarını uygulayın.

Bu bölümde nasıl kullanılacağını gösterir **NuGet** Media Services .NET SDK uzantıları ve diğer bağımlı kitaplıkları eklemek için.

Alternatif olarak, en son Media Services .NET SDK'sı BITS Github'dan alabilirsiniz ([github.com/Azure/azure-sdk-for-media-services](https://github.com/Azure/azure-sdk-for-media-services) veya [github.com/Azure/azure-sdk-for-media-services-extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions)) çözümü oluşturun ve istemci proje başvuruları ekleyin. Gerekli tüm bağımlılıkları indirilir ve otomatik olarak ayıklanan.

1. Visual Studio’da yeni bir C# Konsol Uygulaması oluşturun. Girin **adı**, **konumu**, ve **çözüm adı**ve ardından Tamam'ı tıklatın.
2. Çözümü oluşturun.
3. Kullanım **NuGet** yükleme ve ekleme **Azure Media Services .NET SDK uzantıları** (**windowsazure.mediaservices.extensions**). Bu paketin yüklenmesiyle **Media Services .NET SDK** da yüklenir ve diğer tüm gerekli bağımlılıklar eklenir.
   
    En yeni sürümünü NuGet yüklü olduğundan emin olun. Daha fazla bilgi ve yükleme yönergeleri için bkz: [NuGet](http://nuget.codeplex.com/).
4. Çözüm Gezgini'nde proje adına sağ tıklayın ve Manage NuGet paketleri seçin.
   
    NuGet paketlerini Yönet iletişim kutusu görüntülenir.
5. Çevrimiçi Galeri Azure MediaServices uzantıları için arama, Azure Media Services .NET SDK uzantıları seçin ve ardından yükle düğmesine tıklayın.
   
    Proje değiştirilebilir ve Media Services .NET SDK uzantıları, Media Services .NET SDK'sı ve diğer bağımlı derlemelerden başvuruları eklenir.
6. Temizleyici bir geliştirme ortamı yükseltmek için NuGet paketi geri yüklemeyi etkinleştirme göz önünde bulundurun. Daha fazla bilgi için bkz: [NuGet paket geri yükleme "](http://docs.nuget.org/consume/package-restore).
7. Bir başvuru ekleyin **System.Configuration** derleme. Bu derleme System.Configuration içerir. **ConfigurationManager** yapılandırma dosyaları (örneğin, App.config) erişmek için kullanılan sınıf.
   
    Başvuruları Yönet iletişim kutusunu kullanarak başvurular eklemek için Çözüm Gezgini'nde proje adına sağ tıklayın. Ardından, Ekle ve başvurular seçin.
   
    Başvuruları Yönet iletişim kutusu görüntülenir.
8. .NET framework derlemeleri altındaki bulmak ve System.Configuration derleme seçin ve Tamam'ı tıklatın.
9. App.config dosyasını açın ve eklemek bir *appSettings* dosyaya bölümü.     
   
    Medya Hizmetleri API'sine bağlanmak için gereken değerleri ayarlayın. Daha fazla bilgi için bkz: [Azure AD kimlik doğrulaması ile Azure Media Services API erişim](media-services-use-aad-auth-to-access-ams-api.md). 

    Kullanıyorsanız [kullanıcı kimlik doğrulaması](media-services-use-aad-auth-to-access-ams-api.md#types-of-authentication) yapılandırma dosyası büyük olasılıkla, Azure AD Kiracı etki alanı ve AMS REST API uç noktası için değerlere sahip olur.
    
    >[!Important]
    >Azure Media Services belgelerinde çoğu kod örnekleri kümesi, AMS API'sine bağlanmak için kimlik doğrulama kullanıcı (etkileşimli) türünü kullanın. Bu kimlik doğrulama yöntemini de yönetim veya yerel uygulamalar izleme için çalışır: mobil uygulamaları, Windows uygulamaları ve konsol uygulamaları. Bu kimlik doğrulama yöntemi, sunucu, web Hizmetleri, uygulamaları API'leri türü için uygun değil.  Daha fazla bilgi için bkz: [Azure AD kimlik doğrulaması ile AMS API'sine erişim](media-services-use-aad-auth-to-access-ams-api.md).

        <configuration>
        ...
            <appSettings>
              <add key="AADTenantDomain" value="YourAADTenantDomain" />
              <add key="MediaServiceRESTAPIEndpoint" value="YourRESTAPIEndpoint" />
            </appSettings>

        </configuration>

10. Aşağıdaki kodu, Program.cs dosyasının başındaki mevcut **using** deyimlerinin üzerine yazın.
           
        using System;
        using System.Configuration;
        using System.IO;
        using Microsoft.WindowsAzure.MediaServices.Client;
        using System.Threading;
        using System.Collections.Generic;
        using System.Linq;

Bu noktada, Media Services uygulama geliştirmeye başlamak hazırsınız.    

## <a name="example"></a>Örnek

Aşağıda AMS API'sine bağlanır ve tüm kullanılabilir medya işlemcileri listeler küçük bir örnek verilmiştir.
    
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

##<a name="next-steps"></a>Sonraki adımlar

Şimdi [AMS API'sine bağlanabilir](media-services-use-aad-auth-to-access-ams-api.md) ve başlangıç [geliştirme](media-services-dotnet-get-started.md).


## <a name="media-services-learning-paths"></a>Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

