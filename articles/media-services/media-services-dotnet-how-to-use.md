---
title: "aaaHow tooSet bilgisayarı .NET ile Media Services geliştirmeye yönelik kurma"
description: ".NET için hello Media Services SDK'sını kullanarak Media Services hello önkoşulları hakkında bilgi edinin. Da bilgi nasıl toocreate bir Visual Studio uygulaması."
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
ms.openlocfilehash: a5a2af3211d8156fd7dea99831fb769df4130d41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="media-services-development-with-net"></a>.NET ile Media Services Geliştirme
[!INCLUDE [media-services-selector-setup](../../includes/media-services-selector-setup.md)]

Bu konuda toostart geliştirme medya hizmetleri nasıl ele alınmıştır .NET kullanan uygulamalar.

Merhaba **Azure Media Services .NET SDK'sı** kitaplığı .NET kullanarak Media Services karşı tooprogram sağlar. Bu bile .NET ile daha kolay toodevelop hello toomake **Azure Media Services .NET SDK uzantıları** kitaplığı sağlanır. Bu kitaplığı bir dizi genişletme yöntemleri ve .NET kodunuzu basitleştirmeye yardımcı işlevlerini içerir. Her iki kitaplıkları aracılığıyla kullanılabilir **NuGet** ve **GitHub**.

## <a name="prerequisites"></a>Ön koşullar
* Yeni veya mevcut bir Azure aboneliğinde bir Media Services hesabı. Merhaba konusuna [nasıl tooCreate Media Services hesabı](media-services-portal-create-account.md).
* İşletim sistemleri: Windows 10, Windows 7, Windows 2008 R2 veya Windows 8.
* .NET framework 4.5.
* Visual Studio.

## <a name="create-and-configure-a-visual-studio-project"></a>Visual Studio projesi oluşturup yapılandırma
Bu bölümde, nasıl gösterilir toocreate Visual Studio Proje ve Media Services geliştirmeye kaydınızı ayarlayın.  Bu durumda, bir C# Windows konsol uygulaması hello projedir, ancak hello burada gösterilen aynı kurulum adımlarını geçerli tooother tür projeler için Media Services uygulamalar (örneğin, bir Windows Forms uygulaması veya bir ASP.NET Web uygulaması) oluşturabilirsiniz.

Bu bölümde gösterilmiştir nasıl toouse **NuGet** tooadd Media Services .NET SDK uzantıları ve diğer bağımlı kitaplıkları.

Alternatif olarak, Github'dan hello son Media Services .NET SDK'sı BITS alabilirsiniz ([github.com/Azure/azure-sdk-for-media-services](https://github.com/Azure/azure-sdk-for-media-services) veya [github.com/Azure/azure-sdk-for-media-services-extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions)) hello çözümü oluşturmak ve hello başvuruları toohello istemci projesi ekleyin. Tüm hello gerekli bağımlılıkları indirilir ve otomatik olarak ayıklanan.

1. Visual Studio’da yeni bir C# Konsol Uygulaması oluşturun. Merhaba girin **adı**, **konumu**, ve **çözüm adı**ve ardından Tamam'ı tıklatın.
2. Merhaba çözümü oluşturun.
3. Kullanım **NuGet** tooinstall ve ekleme **Azure Media Services .NET SDK uzantıları** (**windowsazure.mediaservices.extensions**). Bu paketin yüklenmesiyle **Media Services .NET SDK** da yüklenir ve diğer tüm gerekli bağımlılıklar eklenir.
   
    Hello en yeni sürümünü NuGet yüklü olduğundan emin olun. Daha fazla bilgi ve yükleme yönergeleri için bkz: [NuGet](http://nuget.codeplex.com/).
4. Çözüm Gezgini'nde, hello hello proje adına sağ tıklayın ve Manage NuGet paketleri seçin.
   
    Merhaba NuGet paketlerini Yönet iletişim kutusu görüntülenir.
5. Hello Çevrimiçi Galerisi, Azure MediaServices uzantıları için arama Azure Media Services .NET SDK uzantıları seçin ve ardından hello yükle düğmesine tıklayın.
   
    Merhaba proje değiştirilir ve toohello Media Services .NET SDK uzantıları, Media Services .NET SDK başvuruyor ve diğer bağımlı derlemelerden eklenir.
6. toopromote temizleyici bir geliştirme ortamı NuGet paketi geri yüklemeyi etkinleştirme göz önünde bulundurun. Daha fazla bilgi için bkz: [NuGet paket geri yükleme "](http://docs.nuget.org/consume/package-restore).
7. Bir başvuru çok ekleyin**System.Configuration** derleme. Bu derleme hello System.Configuration içerir. **ConfigurationManager** sınıf kullanılan tooaccess yapılandırma dosyaları (örneğin, App.config).
   
    Merhaba başvuruları Yönet iletişim kutusunu kullanarak tooadd başvuruları hello Çözüm Gezgini'nde hello proje adına sağ tıklayın. Ardından, Ekle ve başvurular seçin.
   
    Merhaba başvuruları Yönet iletişim kutusu görüntülenir.
8. .NET framework derlemeleri altındaki bulmak ve hello System.Configuration derleme seçin ve Tamam'ı tıklatın.
9. Merhaba App.config dosyasını açın ve eklemek bir *appSettings* bölüm toohello dosyası.     
   
    Gerekli tooconnect toohello Media Services API olan hello değerleri ayarlayın. Daha fazla bilgi için bkz: [Azure AD kimlik doğrulaması ile erişim hello Azure Media Services API](media-services-use-aad-auth-to-access-ams-api.md). 

    Kullanıyorsanız [kullanıcı kimlik doğrulaması](media-services-use-aad-auth-to-access-ams-api.md#types-of-authentication) yapılandırma dosyanızı büyük olasılıkla, Azure AD Kiracı etki alanı değerlere sahip ve AMS REST API uç noktası hello.
    
    >[!Important]
    >Hello Azure Media Services belgelerine çoğu kod örnekleri kümesi, kimlik doğrulama tooconnect toohello AMS API kullanıcı (etkileşimli) türünü kullanın. Bu kimlik doğrulama yöntemini de yönetim veya yerel uygulamalar izleme için çalışır: mobil uygulamaları, Windows uygulamaları ve konsol uygulamaları. Bu kimlik doğrulama yöntemi, sunucu, web Hizmetleri, uygulamaları API'leri türü için uygun değil.  Daha fazla bilgi için bkz: [Azure AD kimlik doğrulaması ile erişim hello AMS API](media-services-use-aad-auth-to-access-ams-api.md).

        <configuration>
        ...
            <appSettings>
              <add key="AADTenantDomain" value="YourAADTenantDomain" />
              <add key="MediaServiceRESTAPIEndpoint" value="YourRESTAPIEndpoint" />
            </appSettings>

        </configuration>

10. Merhaba var olanın üzerine yaz **kullanarak** koddan hello hello Program.cs dosyasının hello başında deyimleri.
           
        using System;
        using System.Configuration;
        using System.IO;
        using Microsoft.WindowsAzure.MediaServices.Client;
        using System.Threading;
        using System.Collections.Generic;
        using System.Linq;

Bu noktada, Media Services uygulama geliştirme hazır toostart var.    

## <a name="example"></a>Örnek

Burada, toohello AMS API bağlanır ve tüm kullanılabilir medya işlemcileri listeler küçük bir örnek verilmiştir.
    
    class Program
    {
        // Read values from hello App.config file.
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

Şimdi [toohello AMS API bağlanabilir](media-services-use-aad-auth-to-access-ams-api.md) ve başlangıç [geliştirme](media-services-dotnet-get-started.md).


## <a name="media-services-learning-paths"></a>Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

