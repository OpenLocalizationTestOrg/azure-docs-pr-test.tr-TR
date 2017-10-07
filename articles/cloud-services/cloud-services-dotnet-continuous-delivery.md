---
title: "Bulut için aaaContinuous teslim hizmetleri Azure içinde TFS ile | Microsoft Docs"
description: "Bilgi nasıl tooset Azure için sürekli teslimini bulut uygulamaları. MSBuild komut satırı deyimleri ve PowerShell komut dosyaları için kod örnekleri."
services: cloud-services
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 4f3c93c6-5c82-4779-9d19-7404a01e82ca
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/12/2017
ms.author: kraigb
ms.openlocfilehash: c0e5e72ffbd3c05b84ce1733068e92c528bcc4b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-delivery-for-cloud-services-in-azure"></a>Azure bulut Hizmetleri için devamlı teslim
Merhaba bu makalede açıklanan işlemi şunların nasıl yapıldığını gösterir Azure bulut uygulamaları için sürekli teslimini tooset. Bu işlem, paketleri otomatik olarak oluşturun ve kod her iade sonra hello paket tooAzure dağıtmanızı sağlar. Merhaba paket oluşturma işlemi bu makalede açıklanan olan eşdeğer toohello **paket** Visual Studio komut ve yayımlama adımlarını olan eşdeğer toohello **Yayımla** Visual Studio'da komutu.
Merhaba makale kapsar hello metodu toocreate yapı sunucusu MSBuild komut satırı deyimleri ve Windows PowerShell betikleri ve bu da kullanacağınız gösterir nasıl toooptionally yapılandırmak Visual Studio Team Foundation Server - ekip tanımları toouse hello MSBuild komutlar ve PowerShell komut dosyaları. Merhaba yapı ortamı ve Azure hedef ortamları için özelleştirilebilir bir işlemdir.

Visual Studio Team Services, olan TFS sürümü ayrıca kullanabileceğiniz daha kolay bu toodo Azure üzerinde barındırılan. 

Başlamadan önce uygulamanızı Visual Studio'dan yayımlamanız gerekir.
Bu tüm hello kaynakların kullanılabilir ve başlatılmış olduğundan emin olmak için tooautomate hello yayın işlem çalıştığınızda.

## <a name="1-configure-hello-build-server"></a>1: hello yapı sunucu yapılandırma
MSBuild kullanarak bir Azure paketi oluşturabilmeniz için önce hello yapı sunucuya hello gerekli yazılım ve araçları yüklemeniz gerekir.

Visual Studio gerekli toobe hello yapı sunucuda yüklü değil. Yapı sunucunuz toouse Team Foundation Yapı Hizmeti toomanage istiyorsanız hello hello yönergeleri izleyin [Team Foundation Yapı Hizmeti] [ Team Foundation Build Service] belgeleri.

1. Merhaba Hello yapı sunucuya yüklemek [.NET Framework 4.5.2][.NET Framework 4.5.2], MSBuild içerir.
2. Merhaba son yükleme [.NET için Azure yazma araçları](https://azure.microsoft.com/develop/net/).
3. Merhaba yüklemek [.NET için Azure kitaplıkları](http://go.microsoft.com/fwlink/?LinkId=623519).
4. Visual Studio yükleme toohello hello Microsoft.WebApplication.targets dosya Kopyala sunucusu oluşturun.

   Visual Studio'nun yüklü olan bir bilgisayarda bu dosyayı C: hello dizininde bulunan\\Program Files(x86)\\MSBuild\\Microsoft\\Visual Studio\\v14.0\\Web. Toohello kopyalamalısınız hello yapı sunucudaki aynı dizini.
5. Merhaba yüklemek [Visual Studio için Azure Araçları](https://www.visualstudio.com/features/azure-tools-vs.aspx).

## <a name="2-build-a-package-using-msbuild-commands"></a>2: MSBuild komutları kullanarak bir paket oluşturun
Bu bölümde nasıl tooconstruct bir MSBuild komut, açıklanmaktadır Azure bir paket oluşturur. Bu adım, her şeyin doğru şekilde yapılandırıldığını ve ne istediğiniz hello MSBuild komut yapan hello yapı sunucu tooverify üzerinde toodo çalıştırın. Hello sonraki bölümde açıklandığı gibi bu komut satırı tooexisting hello yapı sunucuda komut dosyaları derleme veya derleme bir TFS tanımında hello komut satırını kullanabilirsiniz ya da ekleyebilirsiniz. Komut satırı parametreleri ve MSBuild hakkında daha fazla bilgi için bkz: [MSBuild komut satırı başvurusu](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).

1. Visual Studio hello yapı sunucuda yüklüyse, bulun ve seçin **Visual Studio komut istemi** hello içinde **Visual Studio Araçları** Windows klasörü.

   Visual Studio hello yapı sunucuda yüklü değilse, bir komut istemi açın ve MSBuild.exe yola erişilebilir olduğundan emin olun. MSBuild hello yolu % WINDIR % hello .NET Framework yüklenmiş\\Microsoft.NET\\Framework\\*sürüm*. Örneğin, .NET Framework 4 yüklü olduğunda MSBuild.exe toohello PATH ortam değişkeni eklemek için komut hello komut isteminde aşağıdaki hello yazın:

       set PATH=%PATH%;"C:\Windows\Microsoft.NET\Framework\v4.0.30319"
2. Hello komut isteminde toobuild istediğiniz Azure projesi dosyasını içeren toohello klasörüne gidin.
3. MSBuild ile Merhaba/target çalıştırın: yayımlama hello aşağıdaki örneğine olduğu gibi seçeneği:

       MSBuild /target:Publish

   Bu seçenek /t kısaltılır: yayımlayın. hello Azure SDK'sı yüklü olduğunda hello /t:Publish MSBuild seçeneğinde Visual Studio'da kullanılabilir hello Yayımla komutları ile karıştırılmamalıdır. /t hello: derlemeleri Azure paketleri hello yalnızca Publish seçeneği. Visual Studio'da Hello Yayımla komutları gibi hello paketleri dağıtmaz.

   İsteğe bağlı olarak, bir MSBuild parametresi olarak hello proje adı belirtebilirsiniz. Belirtilmezse, geçerli dizin hello kullanılır. MSBuild komut satırı seçenekleri hakkında daha fazla bilgi için bkz: [MSBuild komut satırı başvurusu](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).
4. Merhaba çıkış bulun. Varsayılan olarak, bu komutu bir ilişkisi toohello kök klasöründe hello projesi için gibi dizini *ProjectDir*\\bin\\*yapılandırma* \\ app.Publish\\. Bir Azure projesi derlerken, iki dosya, hello paket dosyasının kendisini ve yapılandırma dosyası ile birlikte gelen hello oluştur:

   * Project.cspkg
   * ServiceConfiguration. *TargetProfile*.cscfg

   Varsayılan olarak, her Azure projesi yerel (hata ayıklama) yapılar ve bulut (hazırlık veya üretim) yapılar için başka bir hizmet yapılandırma dosyası (.cscfg dosyası) içerir, ancak ekleyip gerektiği gibi hizmet yapılandırma dosyalarını kaldırabilirsiniz. Visual Studio içinde bir paket oluşturduğunuzda, hangi hizmet yapılandırma dosyası tooinclude hello paket yanında istenir.
5. Merhaba hizmet yapılandırma dosyası belirtin. MSBuild kullanarak bir paket oluşturduğunuzda, hello yerel hizmet yapılandırma dosyası varsayılan olarak dahil edilir. tooinclude farklı hizmet yapılandırma dosyası aşağıdaki örneğine hello olduğu gibi hello MSBuild komut TargetProfile özelliğini ayarlayın:

       MSBuild /t:Publish /p:TargetProfile=Cloud
6. Merhaba Çıktı Hello konumunu belirtin. /P:PublishDir kullanarak hello yolu ayarla =*Directory* \\ aşağıdaki örneğine hello olduğu gibi ters eğik çizgi ayırıcı sondaki hello dahil olmak üzere seçeneği:

       MSBuild /target:Publish /p:PublishDir=\\myserver\drops\

   Oluşturulur ve test sonra uygun MSBuild satır toobuild projelerinizi komut ve bunları Azure bir pakete birleştirmek, bu komut satırı tooyour yapı komut dosyaları ekleyebilirsiniz. Yapı sunucunuz özel komut dosyaları kullanıyorsa, bu işlem, özel derleme işlem ayrıntılarını bağlıdır. Ardından bir yapı ortamı olarak TFS kullanıyorsanız, hello sonraki adım tooadd hello Azure paketi yapı tooyour derleme işlemindeki hello yönergeleri izleyebilir.

## <a name="3-build-a-package-using-tfs-team-build"></a>3: TFS ekip kullanarak bir paket oluşturun
Varsa Team Foundation Server (TFS) bir yapı denetleyicisi ve hello sunucu yapı olarak ayarlamak TFS yapı makinesi olarak ayarlamak, ardından Azure paketiniz için otomatikleştirilmiş bir yapıyı isteğe bağlı olarak ayarlayabilirsiniz. Yukarı tooset ve bir yapı sistemi olarak kullanılmasını Team Foundation server nasıl görürüm hakkında bilgi için [derleme sisteminiz genişletme][Scale out your build system]. Özellikle, aşağıdaki yordamda açıklandığı gibi yapı sunucunuz yapılandırdığınız varsayılmaktadır [dağıtma ve bir yapı sunucusunu yapılandırmak][Deploy and configure a build server], ve bir takım projesi oluşturduğunuz Bulutu oluşturulmuş Merhaba takım projesinde hizmet projesi.

tooconfigure TFS toobuild Azure paketler hello aşağıdaki adımları gerçekleştirin:

1. Visual Studio geliştirme bilgisayarınızda hello Görünüm menüsünde seçin **Takım Gezgini**, veya Ctrl + seçin\\, Ctrl + M. Takım Gezgini penceresinde hello genişletin **derlemeler** düğümü veya hello seçin **derlemeler** sayfasında ve seçin **yeni yapı tanımı**.

   ![Yeni bir yapı tanımı seçeneği][0]
2. Merhaba seçin **tetikleyici** sekmesini tıklatın ve hello istenen istediğinizde koşulları hello yerleşik paket toobe belirtin. Örneğin, **sürekli tümleştirme** bir kaynak denetim her iade toobuild hello paket oluşur.
3. Merhaba seçin **kaynak ayarları** sekmesinde ve proje klasörünüzdeki hello listelendiğinden emin olun **kaynak denetimi klasörü** sütun ve hello durumu **etkin**.
4. Merhaba seçin **Yapı Varsayılanları** sekmesini tıklatın ve yapı denetleyicisi altında hello hello yapı sunucu adını doğrulayın.  Ayrıca, hello seçeneği **Kopyala derleme çıktı toohello aşağıdaki bırakma klasörü** ve istenen hello bırakma konumu belirtin.
5. Merhaba seçin **işlem** sekmesi. Merhaba işlem sekmesinde altında hello varsayılan şablonu seçin **yapı**, zaten seçili değilse ve hello genişletin hello proje belirleyin **Gelişmiş** hello bölümünde **Yapı**hello kılavuz bölümü.
6. Seçin **MSBuild bağımsız değişkenleri**, yukarıda 2. adımda açıklandığı gibi hello uygun MSBuild komut satırı bağımsız değişkenleri ayarlayın. Örneğin **/t: /p:PublishDir yayımlama =\\\\myserver\\bırakır\\**  toobuild bir paket ve kopyalama hello paket dosyaları toohello konumunu \\ \\myserver\\bırakır\\:

   ![MSBuild bağımsız değişkenleri][2]

   > [!NOTE]
   > Merhaba dosyaları tooa kopyalama ortak paylaşıma kolaylaştırır daha kolay toomanually geliştirme bilgisayarınızda hello paketlerinden dağıtın.
7. Test, derleme adımının Hello başarılı bir değişiklik tooyour projesinde denetleyerek veya yeni bir yapıyı sıraya. Takım Gezgini'nde, yeni bir derleme yukarı tooqueue sağ **tüm yapı tanımlarını** ve ardından **yeni yapıyı sıraya al**.

## <a name="4-publish-a-package-using-a-powershell-script"></a>4: bir PowerShell komut dosyası kullanarak bir paket yayımlama
Bu bölümde, nasıl tooconstruct hello bulut uygulama paketi yayımlayacak bir Windows PowerShell Betiği isteğe bağlı parametreleri kullanarak tooAzure çıkış açıklanmaktadır. Bu komut dosyası Hello yapı adım sonra özel derleme otomasyonunuz çağrılabilir. Ayrıca, Visual Studio TFS takım yapısı içinde işlem şablonu iş akışı etkinliklerden de çağrılabilir.

1. Merhaba yüklemek [Azure PowerShell cmdlet'lerini] [ Azure PowerShell cmdlets] (v0.6.1 ya da daha yüksek).
   Merhaba cmdlet kurulumu aşamasında tooinstall bir ek bileşeni seçin. Hello önceki sürümler 2.x.x numaralı ancak bu resmi olarak desteklenen sürüm CodePlex sunulan hello eski sürümün yerine geçer unutmayın.
2. Azure PowerShell hello Başlat menüsünden veya başlangıç sayfasını kullanarak başlatın. Bu yolla başlatırsanız, hello Azure PowerShell cmdlet'leri yüklenir.
3. Merhaba PowerShell isteminde hello PowerShell cmdlet'leri hello kısmi komutunu girerek yüklendiğini doğrulamak `Get-Azure` ve tuşuna basarak hello deyim tamamlama için SEKME tuşunu.

   Art arda hello SEKME tuşuna basın, çeşitli Azure PowerShell komutlarını görmeniz gerekir.
4. Abonelik bilgilerinizi hello .publishsettings dosyasından içeri aktararak tooyour Azure aboneliği bağlanabildiğini doğrulayın.

   `Import-AzurePublishSettingsFile c:\scripts\WindowsAzure\default.publishsettings`

   Merhaba komutu girin

   `Get-AzureSubscription`

   Bu aboneliğiniz hakkında bilgi gösterir. Her şeyin doğru olduğundan emin olun.
5. Bu makalenin betikleri klasörünüze c: olarak hello sonunda sağlanan hello komut dosyası şablonu kaydetme\\betikleri\\WindowsAzure\\**PublishCloudService.ps1**.
6. Merhaba komut Hello parametreleri bölümü gözden geçirin. Ekleyin veya herhangi bir varsayılan değeri değiştirin. Bu değerler, her zaman açık parametreleri geçirerek kılınabilir.
7. Geçerli bir bulut hizmeti vardır ve komut dosyası hello tarafından hedeflenebilir aboneliğinizde oluşturulan depolama hesapları yayımlama emin olun. Depolama hesabı (blob depolama) kullanılan tooupload olmalı ve dağıtım oluşturulurken hello dağıtım paketini ve yapılandırma dosyası geçici olarak depolar.

   * toocreate yeni bir bulut hizmeti, bu komut dosyası veya kullanım hello çağırabilir [Azure portal](https://portal.azure.com). Merhaba bulut hizmeti adı tam etki alanı adının öneki olarak kullanılır ve bu nedenle benzersiz olmalıdır.

         New-AzureService -ServiceName "mytestcloudservice" -Location "North Central US" -Label "mytestcloudservice"
   * toocreate yeni bir depolama hesabı, bu komut dosyası veya kullanım hello çağırabilir [Azure portal](https://portal.azure.com). Merhaba depolama hesabı adı tam etki alanı adının öneki olarak kullanılır ve bu nedenle benzersiz olmalıdır. Bulut hizmeti olarak aynı ad hello kullanmayı deneyebilirsiniz.

         New-AzureStorageAccount -ServiceName "mytestcloudservice" -Location "North Central US" -Label "mytestcloudservice"
8. Bu komut dosyası tooyour konak yapı Otomasyon toooccur hello paket derleme sonrası wire veya doğrudan Azure Powershell'den Hello betik çağırın.

   > [!IMPORTANT]
   > Merhaba komut dosyası her zaman silin veya bunlar algılanırsa, var olan dağıtımlar varsayılan olarak değiştirin. Bu hiçbir kullanıcıdan mümkün olduğu Otomasyon sürekli teslimat etkinleştirmek gereklidir.
   >
   >

   **Örnek Senaryo 1:** sürekli dağıtım toohello bir hizmeti ortamını hazırlama:

       PowerShell c:\scripts\windowsazure\PublishCloudService.ps1 -environment Staging -serviceName mycloudservice -storageAccountName mystoragesaccount -packageLocation c:\drops\app.publish\ContactManager.Azure.cspkg -cloudConfigLocation c:\drops\app.publish\ServiceConfiguration.Cloud.cscfg -subscriptionDataFile c:\scripts\default.publishsettings

   Bu genellikle doğrulama ve bir VIP takası testi tarafından izlendiğinden. Merhaba VIP takas hello yapılabilir [Azure portal](https://portal.azure.com) veya hello taşıma dağıtım cmdlet'ini kullanarak.

   **Örnek Senaryo 2:** sürekli dağıtım toohello üretim ortamına ayrılmış sınama hizmeti

       PowerShell c:\scripts\windowsazure\PublishCloudService.ps1 -environment Production -enableDeploymentUpgrade 1 -serviceName mycloudservice -storageAccountName mystorageaccount -packageLocation c:\drops\app.publish\ContactManager.Azure.cspkg -cloudConfigLocation c:\drops\app.publish\ServiceConfiguration.Cloud.cscfg -subscriptionDataFile c:\scripts\default.publishsettings

   **Uzak Masaüstü:**

   Uzak Masaüstü Azure projenizde etkinse, bu komut dosyası tarafından hedeflenen tooall bulut Hizmetleri tooensure hello doğru bulut hizmet sertifikası karşıya tooperform ek tek seferlik adımlar gerekir.

   Rolleri tarafından beklenen hello sertifika parmak izi değerlerini bulun. Parmak izi değerleri bulut yapılandırma dosyasının (yani ServiceConfiguration.Cloud.cscfg) sertifikaları bölümünde hello görülebilir. Seçenekleri Göster ve görünüm hello sertifika seçtiğinizde de Visual Studio'da hello uzak masaüstü yapılandırması iletişim kutusu görünür.

       <Certificates>
             <Certificate name="Microsoft.WindowsAzure.Plugins.RemoteAccess.PasswordEncryption" thumbprint="C33B6C432C25581601B84C80F86EC2809DC224E8" thumbprintAlgorithm="sha1" />
       </Certificates>

   Uzak Masaüstü sertifikaları cmdlet komut dosyası izleyen hello kullanarak bir kerelik Kurulum adım olarak karşıya yükle:

       Add-AzureCertificate -serviceName <CLOUDSERVICENAME> -certToDeploy (get-item cert:\CurrentUser\MY\<THUMBPRINT>)

   Örneğin:

       Add-AzureCertificate -serviceName 'mytestcloudservice' -certToDeploy (get-item cert:\CurrentUser\MY\C33B6C432C25581601B84C80F86EC2809DC224E8

   Alternatif olarak özel anahtar ve karşıya yükleme sertifikaları tooeach hedef bulut hizmetini kullanarak hello sertifika dosyası PFX dışa aktarabilirsiniz [Azure portal](https://portal.azure.com).

   <!---
   Fixing broken links for Azure content migration from ACOM tooDOCS. I'm unable toofind a replacement links, so I'm commenting out this reference for now. hello author can investigate in hello future. "Read hello following article toolearn more: http://msdn.microsoft.com/library/windowsazure/gg443832.aspx.
   -->
   **Dağıtım vs yükseltin. Dağıtım - Sil\> yeni dağıtım**

   Merhaba betik varsayılan olarak gerçekleştirecek bir yükseltme dağıtımı ($enableDeploymentUpgrade = 1) ne zaman hiçbir parametre geçirilen veya 1 değerini açıkça geçirilir. Tek örnekleri için tam dağıtımını daha az zaman ayırdığınız avantajı vardır. Ayrıca bazı örnek diğerlerinde çalışıyor bırakarak hello avantajı vardır yüksek kullanılabilirliğin gerektiği örnekleri (, güncelleştirme etki alanının yürütülmesi) yükseltilir, artı, VIP silinmeyecek için.

   Yükseltme dağıtımı devre dışı bırakılabilir hello komut dosyasında ($enableDeploymentUpgrade = 0) veya geçirerek *- enableDeploymentUpgrade 0* bir parametre olarak varolan tüm dağıtım komut dosyası davranışı toofirst delete değiştirir ve ardından oluşturun bir yeni dağıtım.

   > [!IMPORTANT]
   > Merhaba komut dosyası her zaman silin veya bunlar algılanırsa, var olan dağıtımlar varsayılan olarak değiştirin. Hiçbir kullanıcı/işleci isteyen mümkün olduğu Otomasyon sürekli teslimat etkinleştirmek için gereken budur.
   >
   >

## <a name="5-publish-a-package-using-tfs-team-build"></a>5: TFS ekip kullanarak paket yayımlama
Bu isteğe bağlı adım yayımlama hello paketi yapı tooAzure, işleyen 4. adımda oluşturduğunuz TFS ekip toohello betik bağlanır. Bu, değiştirme hello işlem hello hello iş akışının sonunda bir yayımlama etkinliği çalışır, yapı tanımı tarafından kullanılan şablonu kapsar. Merhaba Yayımla etkinlik parametrelerinde hello yapıdan geçirme, PowerShell komutunu çalıştırır. MSBuild hedefler ve komut dosyası yayımlama hello çıktısını yöneltilen hello standart yapı çıkış.

1. Yapı tanımı sorumlu Hello Düzenle sürekli dağıtın.
2. Select hello **işlem** sekmesi.
3. İzleyin [bu yönergeleri](http://msdn.microsoft.com/library/dd647551.aspx) tooadd bir etkinlik projesi hello için yapı işlem şablonu, hello varsayılan şablonunu indirebilir, hello projeye ekleyin ve iade etme. Merhaba derleme işlem şablonu AzureBuildProcessTemplate gibi yeni bir ad verin.
4. Toohello iade **işlem** sekmesini tıklatın ve kullanmak **ayrıntıları göster** tooshow kullanılabilir yapı işlem şablonları listesi. Merhaba seçin **yeni...**  düğmesine tıklayın ve yalnızca eklenir ve iade toohello proje gidin. Yeni oluşturduğunuz hello şablonu bulun ve seçin **Tamam**.
5. Açık hello düzenleme için işlem şablonu seçili. Doğrudan hello iş akışı Tasarımcısı'nda veya hello XML Düzenleyicisi toowork hello XAML ile açabilirsiniz.
6. Ayrı satır öğeleri hello bağımsız değişkenleri sekmesi hello iş akışı Tasarımcısı'nın olarak yeni bağımsız değişkenlerinin listesi aşağıdaki hello ekleyin. Tüm bağımsız değişkenler yönü olması gerekir, = ve türü = String. Bunlar hangi sonra get kullanılan toocall hello betik yayımlama hello akışına hello yapı tanımından kullanılan tooflow parametreleri olacaktır.

       SubscriptionName
       StorageAccountName
       CloudConfigLocation
       PackageLocation
       Environment
       SubscriptionDataFileLocation
       PublishScriptLocation
       ServiceName

   ![Bağımsız değişkenler listesi][3]

   Merhaba karşılık gelen XAML şöyle görünür:

       <Activity  _ />
         <x:Members>
           <x:Property Name="BuildSettings" Type="InArgument(mtbwa:BuildSettings)" />
           <x:Property Name="TestSpecs" Type="InArgument(mtbwa:TestSpecList)" />
           <x:Property Name="BuildNumberFormat" Type="InArgument(x:String)" />
           <x:Property Name="CleanWorkspace" Type="InArgument(mtbwa:CleanWorkspaceOption)" />
           <x:Property Name="RunCodeAnalysis" Type="InArgument(mtbwa:CodeAnalysisOption)" />
           <x:Property Name="SourceAndSymbolServerSettings" Type="InArgument(mtbwa:SourceAndSymbolServerSettings)" />
           <x:Property Name="AgentSettings" Type="InArgument(mtbwa:AgentSettings)" />
           <x:Property Name="AssociateChangesetsAndWorkItems" Type="InArgument(x:Boolean)" />
           <x:Property Name="CreateWorkItem" Type="InArgument(x:Boolean)" />
           <x:Property Name="DropBuild" Type="InArgument(x:Boolean)" />
           <x:Property Name="MSBuildArguments" Type="InArgument(x:String)" />
           <x:Property Name="MSBuildPlatform" Type="InArgument(mtbwa:ToolPlatform)" />
           <x:Property Name="PerformTestImpactAnalysis" Type="InArgument(x:Boolean)" />
           <x:Property Name="CreateLabel" Type="InArgument(x:Boolean)" />
           <x:Property Name="DisableTests" Type="InArgument(x:Boolean)" />
           <x:Property Name="GetVersion" Type="InArgument(x:String)" />
           <x:Property Name="PrivateDropLocation" Type="InArgument(x:String)" />
           <x:Property Name="Verbosity" Type="InArgument(mtbw:BuildVerbosity)" />
           <x:Property Name="Metadata" Type="mtbw:ProcessParameterMetadataCollection" />
           <x:Property Name="SupportedReasons" Type="mtbc:BuildReason" />
           <x:Property Name="SubscriptionName" Type="InArgument(x:String)" />
           <x:Property Name="StorageAccountName" Type="InArgument(x:String)" />
           <x:Property Name="CloudConfigLocation" Type="InArgument(x:String)" />
           <x:Property Name="PackageLocation" Type="InArgument(x:String)" />
           <x:Property Name="Environment" Type="InArgument(x:String)" />
           <x:Property Name="SubscriptionDataFileLocation" Type="InArgument(x:String)" />
           <x:Property Name="PublishScriptLocation" Type="InArgument(x:String)" />
           <x:Property Name="ServiceName" Type="InArgument(x:String)" />
         </x:Members>

         <this:Process.MSBuildArguments>
7. Yeni bir sıra hello Aracısını Çalıştır sonuna ekleyin:

   1. Geçerli komut dosyası için bir If ifadesinden etkinlik toocheck ekleyerek başlayın. Merhaba koşul toothis değeri ayarlayın:

          Not String.IsNullOrEmpty(PublishScriptLocation)
   2. Hello hello If ifadesinden sonra bir durumunun, yeni bir dizi etkinlik ekleyin. Set hello görünen adı too'Start Yayımla '
   3. Başlangıç dizisi seçiliyken yayımlama hello ile yeni değişkenleri aşağıdaki listesini ayrı satırı öğeleri hello iş akışı Tasarımcısı'nın değişkenleri sekmesi olarak ekleyin. Tüm değişkenleri değişken türü olmalıdır = dize ve kapsam başlangıç = yayımlayın. Bu iş akışına hangi sonra get kullanılan toocall hello betik yayımlama hello yapı tanımından kullanılan tooflow parametreleri olacaktır.

      * Dize türünde SubscriptionDataFilePath
      * Dize türünde PublishScriptFilePath

        ![Yeni değişkenleri][4]
   4. Daha önce ConvertWorkspaceItem Etkinlik başına hello Ekle veya TFS 2012 kullanıyorsanız yeni sırası hello. TFS 2013 veya üzeri kullanıyorsanız, GetLocalPath etkinlik hello hello yeni sırası başında ekleyin. Bir ConvertWorkspaceItem için hello özellikleri aşağıdaki gibi ayarlayın: yönü ServerToLocal, DisplayName = 'Dönüştürme Yayımla betik filename' = giriş 'PublishScriptLocation', sonuç = 'PublishScriptFilePath', çalışma alanı = = 'Çalışma alanı'. Merhaba özelliği IncomingPath too'PublishScriptLocation bir GetLocalPath etkinliği için ayarlandı ', ve sonuç too'PublishScriptFilePath hello'. Bu etkinlik dönüştürür hello yolu toohello yayımlama TFS sunucusu konumlardan komut dosyası (eğer varsa) tooa standart yerel disk yolu.
   5. Daha önce başka bir ConvertWorkspaceItem etkinlik hello sonuna ekleyin veya TFS 2012 kullanıyorsanız yeni sırası hello. Yön ServerToLocal, DisplayName = 'abonelik filename Dönüştür' = giriş 'SubscriptionDataFileLocation', sonuç = 'SubscriptionDataFilePath', çalışma alanı = = 'Çalışma alanı'. TFS 2013 veya üzeri kullanıyorsanız, başka bir GetLocalPath ekleyin. IncomingPath 'SubscriptionDataFileLocation' = ve sonuç 'SubscriptionDataFilePath.' =
   6. InvokeProcess aktivite hello hello sonuna ekle yeni sırası.
      Bu etkinlik çağrıları PowerShell.exe hello bağımsız değişkenlerle hello yapı tanımı tarafından geçirildi.

      + Bağımsız değişkenler String.Format = ("-""{0}" "- serviceName {1} - storageAccountName {2} - packageLocation""{3}" "- cloudConfigLocation""{4}" "- subscriptionDataFile""{5}" "- selectedSubscription {6} dosya-ortam""{7}" "",  PublishScriptFilePath, ServiceName, StorageAccountName, PackageLocation, CloudConfigLocation, SubscriptionDataFilePath, varlığıyla SubscriptionName, ortamı)
      + DisplayName Execute = betik yayımlama
      + Dosya adı "PowerShell" = (Merhaba tırnak işaretleri dahil)
      + OutputEncoding System.Text.Encoding.GetEncoding(System.Globalization.CultureInfo.InstalledUICulture.TextInfo.OEMCodePage) =
   7. Merhaba, **işlemek standart çıktı** hello textbox değeri too'data bölümünde InvokeProcess textbox,'. Bir değişken toostore hello standart çıktı verileri budur.
   8. Merhaba hemen altındaki WriteBuildMessage etkinlik eklemek **işlemek standart çıktı** bölümü. Merhaba önem ayarlamak = 'Microsoft.TeamFoundation.Build.Client.BuildMessageImportance.High' ve hello Message = 'data'. Bu komut dosyasının hello standart çıktı toohello yapı çıktı yazılmış sağlar.
   9. Merhaba, **hata çıkış işleme** hello textbox değeri too'data bölümünde InvokeProcess textbox,'. Bu bir değişken toostore hello standart hata verilerdir.
   10. Merhaba hemen altındaki WriteBuildError etkinlik eklemek **hata çıkış işleme** bölümü. Merhaba ileti Ayarla = 'data'. Bu, hello standart hatalar hello komut toohello yapı hata çıktısı yazılan sağlar.
   11. Mavi ünlem işaretleri tarafından belirtilen tüm hataları düzeltin. Ünlem işaretleri tooget hello hata hakkında bir ipucu gelin. Hataları temizlemek için hello iş akışını kaydedin.

   Merhaba Hello sonucunu Yayımla iş akışı etkinlikleri hello Tasarımcısı'nda şöyle görünür:

   ![İş akışı etkinlikleri][5]

   İş akışı etkinlikleri XAML'de şuna benzeyecektir yayımlama hello Hello sonucunu:

       <If Condition="[Not String.IsNullOrEmpty(PublishScriptLocation)]" sap2010:WorkflowViewState.IdRef="If_1">
           <If.Then>
             <Sequence DisplayName="Start Publish" sap2010:WorkflowViewState.IdRef="Sequence_4">
               <Sequence.Variables>
                 <Variable x:TypeArguments="x:String" Name="SubscriptionDataFilePath" />
                 <Variable x:TypeArguments="x:String" Name="PublishScriptFilePath" />
               </Sequence.Variables>
               <mtbwa:ConvertWorkspaceItem DisplayName="Convert publish script filename" sap2010:WorkflowViewState.IdRef="ConvertWorkspaceItem_1" Input="[PublishScriptLocation]" Result="[PublishScriptFilePath]" Workspace="[Workspace]" />
               <mtbwa:ConvertWorkspaceItem DisplayName="Convert subscription filename" sap2010:WorkflowViewState.IdRef="ConvertWorkspaceItem_2" Input="[SubscriptionDataFileLocation]" Result="[SubscriptionDataFilePath]" Workspace="[Workspace]" />
               <mtbwa:InvokeProcess Arguments="[String.Format(&quot; -File &quot;&quot;{0}&quot;&quot; -serviceName {1}&#xD;&#xA;            -storageAccountName {2} -packageLocation &quot;&quot;{3}&quot;&quot;&#xD;&#xA;            -cloudConfigLocation &quot;&quot;{4}&quot;&quot; -subscriptionDataFile &quot;&quot;{5}&quot;&quot;&#xD;&#xA;            -selectedSubscription {6} -environment &quot;&quot;{7}&quot;&quot;&quot;,&#xD;&#xA;            PublishScriptFilePath, ServiceName, StorageAccountName,&#xD;&#xA;            PackageLocation, CloudConfigLocation,&#xD;&#xA;            SubscriptionDataFilePath, SubscriptionName, Environment)]" DisplayName="'Execute Publish Script'" FileName="[PowerShell]" sap2010:WorkflowViewState.IdRef="InvokeProcess_1">
                 <mtbwa:InvokeProcess.ErrorDataReceived>
                   <ActivityAction x:TypeArguments="x:String">
                     <ActivityAction.Argument>
                       <DelegateInArgument x:TypeArguments="x:String" Name="data" />
                     </ActivityAction.Argument>
                     <mtbwa:WriteBuildError Message="{x:Null}" sap2010:WorkflowViewState.IdRef="WriteBuildError_1" />
                   </ActivityAction>
                 </mtbwa:InvokeProcess.ErrorDataReceived>
                 <mtbwa:InvokeProcess.OutputDataReceived>
                   <ActivityAction x:TypeArguments="x:String">
                     <ActivityAction.Argument>
                       <DelegateInArgument x:TypeArguments="x:String" Name="data" />
                     </ActivityAction.Argument>
                     <mtbwa:WriteBuildMessage sap2010:WorkflowViewState.IdRef="WriteBuildMessage_2" Importance="[Microsoft.TeamFoundation.Build.Client.BuildMessageImportance.High]" Message="[data]" mva:VisualBasic.Settings="Assembly references and imported namespaces serialized as XML namespaces" />
                   </ActivityAction>
                 </mtbwa:InvokeProcess.OutputDataReceived>
               </mtbwa:InvokeProcess>
             </Sequence>
           </If.Then>
         </If>
       </Sequence>
8. Merhaba yapı işlem şablonu iş akışı ve iade bu dosyayı kaydedin.
9. Hello yapı tanımını Düzenle (kapatın, zaten açıksa) ve select hello **yeni** hello yeni şablon olarak işlem şablonlarını hello listesinde henüz görmüyorsanız düğmesine tıklayın.
10. Hello parametre özellik değerlerini hello çeşitli bölümü aşağıdaki gibi ayarlayın:

    1. CloudConfigLocation ='c:\\bırakır\\app.publish\\ServiceConfiguration.Cloud.cscfg' *bu değer türetilir: ($PublishDir)ServiceConfiguration.Cloud.cscfg*
    2. PackageLocation = ' c:\\bırakır\\app.publish\\ContactManager.Azure.cspkg' *bu değer türetilir: ($PublishDir)($ProjectName) .cspkg*
    3. PublishScriptLocation = ' c:\\betikleri\\WindowsAzure\\PublishCloudService.ps1'
    4. ServiceName = 'mycloudservicename' *hello uygun bulut hizmeti adını kullan burada*
    5. Ortam 'Hazırlama' =
    6. StorageAccountName 'mystorageaccountname' = *kullanım hello uygun depolama hesabı adı buraya*
    7. SubscriptionDataFileLocation = ' c:\\betikleri\\WindowsAzure\\Subscription.xml'
    8. Varlığıyla SubscriptionName = 'varsayılan'

    ![Parametre özellik değerleri][6]
11. Merhaba değişiklikleri toohello yapı tanımı kaydedin.
12. Her ikisi de paket yapı hello ve yayımlama yapı tooexecute sırası. TooContinuous tümleştirme ayarlamak tetikleyici varsa, her iade Bu davranış yürütülür.

### <a name="publishcloudserviceps1-script-template"></a>PublishCloudService.ps1 komut dosyası şablonu
```
Param(  $serviceName = "",
        $storageAccountName = "",
        $packageLocation = "",
        $cloudConfigLocation = "",
        $environment = "Staging",
        $deploymentLabel = "ContinuousDeploy too$servicename",
        $timeStampFormat = "g",
        $alwaysDeleteExistingDeployments = 1,
        $enableDeploymentUpgrade = 1,
        $selectedsubscription = "default",
        $subscriptionDataFile = ""
     )


function Publish()
{
    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot -ErrorVariable a -ErrorAction silentlycontinue
    if ($a[0] -ne $null)
    {
        Write-Output "$(Get-Date -f $timeStampFormat) - No deployment is detected. Creating a new deployment. "
    }
    #check for existing deployment and then either upgrade, delete + deploy, or cancel according too$alwaysDeleteExistingDeployments and $enableDeploymentUpgrade boolean variables
    if ($deployment.Name -ne $null)
    {
        switch ($alwaysDeleteExistingDeployments)
        {
            1
            {
                switch ($enableDeploymentUpgrade)
                {
                    1  #Update deployment inplace (usually faster, cheaper, won't destroy VIP)
                    {
                        Write-Output "$(Get-Date -f $timeStampFormat) - Deployment exists in $servicename.  Upgrading deployment."
                        UpgradeDeployment
                    }
                    0  #Delete then create new deployment
                    {
                        Write-Output "$(Get-Date -f $timeStampFormat) - Deployment exists in $servicename.  Deleting deployment."
                        DeleteDeployment
                        CreateNewDeployment

                    }
                } # switch ($enableDeploymentUpgrade)
            }
            0
            {
                Write-Output "$(Get-Date -f $timeStampFormat) - ERROR: Deployment exists in $servicename.  Script execution cancelled."
                exit
            }
        } #switch ($alwaysDeleteExistingDeployments)
    } else {
            CreateNewDeployment
    }
}

function CreateNewDeployment()
{
    write-progress -id 3 -activity "Creating New Deployment" -Status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Creating New Deployment: In progress"

    $opstat = New-AzureDeployment -Slot $slot -Package $packageLocation -Configuration $cloudConfigLocation -label $deploymentLabel -ServiceName $serviceName

    $completeDeployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $completeDeploymentID = $completeDeployment.deploymentid

    write-progress -id 3 -activity "Creating New Deployment" -completed -Status "Complete"
    Write-Output "$(Get-Date -f $timeStampFormat) - Creating New Deployment: Complete, Deployment ID: $completeDeploymentID"

    StartInstances
}

function UpgradeDeployment()
{
    write-progress -id 3 -activity "Upgrading Deployment" -Status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Upgrading Deployment: In progress"

    # perform Update-Deployment
    $setdeployment = Set-AzureDeployment -Upgrade -Slot $slot -Package $packageLocation -Configuration $cloudConfigLocation -label $deploymentLabel -ServiceName $serviceName -Force

    $completeDeployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $completeDeploymentID = $completeDeployment.deploymentid

    write-progress -id 3 -activity "Upgrading Deployment" -completed -Status "Complete"
    Write-Output "$(Get-Date -f $timeStampFormat) - Upgrading Deployment: Complete, Deployment ID: $completeDeploymentID"
}

function DeleteDeployment()
{

    write-progress -id 2 -activity "Deleting Deployment" -Status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Deleting Deployment: In progress"

    #WARNING - always deletes with force
    $removeDeployment = Remove-AzureDeployment -Slot $slot -ServiceName $serviceName -Force

    write-progress -id 2 -activity "Deleting Deployment: Complete" -completed -Status $removeDeployment
    Write-Output "$(Get-Date -f $timeStampFormat) - Deleting Deployment: Complete"

}

function StartInstances()
{
    write-progress -id 4 -activity "Starting Instances" -status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instances: In progress"

    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $runstatus = $deployment.Status

    if ($runstatus -ne 'Running')
    {
        $run = Set-AzureDeployment -Slot $slot -ServiceName $serviceName -Status Running
    }
    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $oldStatusStr = @("") * $deployment.RoleInstanceList.Count

    while (-not(AllInstancesRunning($deployment.RoleInstanceList)))
    {
        $i = 1
        foreach ($roleInstance in $deployment.RoleInstanceList)
        {
            $instanceName = $roleInstance.InstanceName
            $instanceStatus = $roleInstance.InstanceStatus

            if ($oldStatusStr[$i - 1] -ne $roleInstance.InstanceStatus)
            {
                $oldStatusStr[$i - 1] = $roleInstance.InstanceStatus
                Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instance '$instanceName': $instanceStatus"
            }

            write-progress -id (4 + $i) -activity "Starting Instance '$instanceName'" -status "$instanceStatus"
            $i = $i + 1
        }

        sleep -Seconds 1

        $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    }

    $i = 1
    foreach ($roleInstance in $deployment.RoleInstanceList)
    {
        $instanceName = $roleInstance.InstanceName
        $instanceStatus = $roleInstance.InstanceStatus

        if ($oldStatusStr[$i - 1] -ne $roleInstance.InstanceStatus)
        {
            $oldStatusStr[$i - 1] = $roleInstance.InstanceStatus
            Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instance '$instanceName': $instanceStatus"
        }

        $i = $i + 1
    }

    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $opstat = $deployment.Status

    write-progress -id 4 -activity "Starting Instances" -completed -status $opstat
    Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instances: $opstat"
}

function AllInstancesRunning($roleInstanceList)
{
    foreach ($roleInstance in $roleInstanceList)
    {
        if ($roleInstance.InstanceStatus -ne "ReadyRole")
        {
            return $false
        }
    }

    return $true
}

#configure powershell with Azure 1.7 modules
Import-Module Azure

#configure powershell with publishsettings for your subscription
$pubsettings = $subscriptionDataFile
Import-AzurePublishSettingsFile $pubsettings
Set-AzureSubscription -CurrentStorageAccountName $storageAccountName -SubscriptionName $selectedsubscription
Select-AzureSubscription $selectedsubscription

#set remaining environment variables for Azure cmdlets
$subscription = Get-AzureSubscription $selectedsubscription
$subscriptionname = $subscription.subscriptionname
$subscriptionid = $subscription.subscriptionid
$slot = $environment

#main driver - publish & write progress tooactivity log
Write-Output "$(Get-Date -f $timeStampFormat) - Azure Cloud Service deploy script started."
Write-Output "$(Get-Date -f $timeStampFormat) - Preparing deployment of $deploymentLabel for $subscriptionname with Subscription ID $subscriptionid."

Publish

$deployment = Get-AzureDeployment -slot $slot -serviceName $servicename
$deploymentUrl = $deployment.Url

Write-Output "$(Get-Date -f $timeStampFormat) - Created Cloud Service with URL $deploymentUrl."
Write-Output "$(Get-Date -f $timeStampFormat) - Azure Cloud Service deploy script finished."
```

## <a name="next-steps"></a>Sonraki adımlar
tooenable uzaktan kesintisiz teslim kullanılırken hata ayıklama bkz [kesintisiz teslim toopublish tooAzure kullanırken uzaktan hata ayıklamayı etkinleştirme](cloud-services-virtual-machines-dotnet-continuous-delivery-remote-debugging.md).

[Team Foundation Build Service]: https://msdn.microsoft.com/library/ee259687.aspx
[.NET Framework 4]: https://www.microsoft.com/download/details.aspx?id=17851
[.NET Framework 4.5]: https://www.microsoft.com/download/details.aspx?id=30653
[.NET Framework 4.5.2]: https://www.microsoft.com/download/details.aspx?id=42643
[Scale out your build system]: https://msdn.microsoft.com/library/dd793166.aspx
[Deploy and configure a build server]: https://msdn.microsoft.com/library/ms181712.aspx
[Azure PowerShell cmdlets]: /powershell/azureps-cmdlets-docs
[hello .publishsettings file]: https://manage.windowsazure.com/download/publishprofile.aspx?wa=wsignin1.0
[0]: ./media/cloud-services-dotnet-continuous-delivery/tfs-01bc.png
[2]: ./media/cloud-services-dotnet-continuous-delivery/tfs-02.png
[3]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-03.png
[4]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-04.png
[5]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-05.png
[6]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-06.png
