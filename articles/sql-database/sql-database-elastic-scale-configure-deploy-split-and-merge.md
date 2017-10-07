---
title: "aaaDeploy bölünmüş birleştirme hizmetine | Microsoft Docs"
description: "Bölme ve esnek veritabanı araçları ile birleştirme"
services: sql-database
documentationcenter: 
author: ddove
manager: jhubbard
editor: 
ms.assetid: 9a993c0f-7052-46cd-aa59-073bea8d535a
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 6fef641cbc1e73ce34a851c53298a072dade8f9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-split-merge-service"></a>Ayırma-birleştirme hizmetini dağıtma
Merhaba bölünmüş Birleştirme aracı parçalı veritabanları arasında veri taşımanıza olanak tanır. Bkz: [ölçeklendirilmiş bulut veritabanları arasında veri taşıma](sql-database-elastic-scale-overview-split-and-merge.md)

## <a name="download-hello-split-merge-packages"></a>Merhaba bölünmüş birleştirme paketlerini yükleyin
1. Merhaba en son NuGet sürümü [NuGet](http://docs.nuget.org/docs/start-here/installing-nuget).
2. Bir komut istemi açın ve nuget.exe indirdiğiniz toohello dizinine gidin. Merhaba indirme PowerShell commmands içerir.
3. Merhaba komutu aşağıda ile Merhaba geçerli dizine Hello son bölünmüş birleştirme paketini indirin:
   ```
   nuget install Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge
   ```  

Merhaba dosyaları adlı bir dizinde yerleştirilir **Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge.x.x.xxx.x** nerede *x.x.xxx.x* hello sürüm numarası yansıtır. Merhaba hello bölünmüş birleştirme hizmet dosyalarını bulmak **content\splitmerge\service** alt dizini ve hello bölünmüş birleştirme PowerShell komut dosyaları (ve gerekli istemci .dll) hello **content\splitmerge\powershell** alt dizini.

## <a name="prerequisites"></a>Ön koşullar
1. Merhaba bölünmüş birleştirme durumu veritabanı olarak kullanılacak bir Azure SQL DB veritabanı oluşturun. Toohello Git [Azure portal](https://portal.azure.com). Yeni bir **SQL veritabanı**. Merhaba veritabanı bir ad verin ve yeni yönetici ve parola oluşturun. Daha sonra kullanmak için emin toorecord hello adı ve parola olabilir.
2. Azure SQL DB sunucunuz Azure Hizmetleri tooconnect tooit verdiğinden emin olun. Merhaba portalında, hello **güvenlik duvarı ayarlarını**, o hello olun **tooAzure Hizmetleri erişimine izin** ayar çok**üzerinde**. Merhaba "Kaydet" simgesine tıklayın.
   
   ![İzin verilen hizmetler][1]
3. Tanılama çıktı için kullanılacak bir Azure depolama hesabı oluşturun. Toohello Azure portalına gidin. Merhaba sol çubuğunda, **yeni**, tıklatın **veri + depolama**, ardından **depolama**.
4. Bölünmüş birleştirme hizmetinizi içerecek bir Azure bulut hizmeti oluşturun.  Toohello Azure portalına gidin. Merhaba sol çubuğunda, **yeni**, ardından **işlem**, **bulut hizmeti**, ve **oluşturma**. 

## <a name="configure-your-split-merge-service"></a>Bölünmüş birleştirme hizmetini yapılandırma
### <a name="split-merge-service-configuration"></a>Bölünmüş birleştirme hizmet yapılandırması
1. Merhaba bölünmüş birleştirme derlemeleri indirdiğiniz hello klasöründe hello bir kopyasını oluşturmak **ServiceConfiguration.Template.cscfg** yanında sevk dosya **SplitMergeService.cspkg** ve yeniden adlandırın **ServiceConfiguration.cscfg**.
2. Açık **ServiceConfiguration.cscfg** girişleri hello biçimi sertifika parmak izleri gibi doğrulama Visual Studio gibi bir metin düzenleyicisinde.
3. Yeni bir veritabanı oluşturmak veya hello durum veritabanı bölünmüş birleştirme işlemleri için varolan bir veritabanı tooserve seçin ve bu veritabanının hello bağlantı dizesini almak. 
   
   > [!IMPORTANT]
   > Şu anda hello durum veritabanı hello Latin harmanlamayı kullanması gerekir (SQL\_Latin1\_genel\_CP1\_CI\_AS). Daha fazla bilgi için bkz: [Windows harmanlama adı (Transact-SQL)](https://msdn.microsoft.com/library/ms188046.aspx).
   >

   Azure SQL DB ile Merhaba bağlantı dizesi genellikle hello şu şekildedir:
      ```
      Server=myservername.database.windows.net; Database=mydatabasename;User ID=myuserID; Password=mypassword; Encrypt=True; Connection Timeout=30
      ```

4. Her iki hello hello cscfg dosyasında bu bağlantı dizesi girin **SplitMergeWeb** ve **SplitMergeWorker** hello ElasticScaleMetadata ayarı rol bölümlerde.
5. Hello için **SplitMergeWorker** rol, geçerli bir bağlantı dizesi tooAzure depolama Merhaba girin **WorkerRoleSynchronizationStorageAccountConnectionString** ayarı.

### <a name="configure-security"></a>Güvenliği yapılandırma
Ayrıntılı yönergeler tooconfigure hello güvenlik hello hizmetinin için toohello başvuran [bölünmüş birleştirme Güvenlik Yapılandırması](sql-database-elastic-scale-split-merge-security-configuration.md).

Bu öğretici için basit bir sınama dağıtımı Hello amaçları doğrultusunda, yapılandırma adımları olacaktır en az sayıda tooget hello hizmeti çalışır gerçekleştirilir. Bu adımları yalnızca hello bir makine/toocommunicate hello hizmetiyle yürütme hesabını etkinleştirin.

### <a name="create-a-self-signed-certificate"></a>Otomatik olarak imzalanan sertifika oluşturma
Yeni bir dizin oluşturun ve aşağıdaki komutu kullanarak bu dizine yürütme hello bir [Visual Studio için geliştirici komut istemi](http://msdn.microsoft.com/library/ms229859.aspx) penceresi:

   ```
    makecert ^
    -n "CN=*.cloudapp.net" ^
    -r -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.1,1.3.6.1.5.5.7.3.2" ^
    -a sha1 -len 2048 ^
    -sr currentuser -ss root ^
    -sv MyCert.pvk MyCert.cer
   ```

Parola tooprotect hello için özel bir anahtar istenir. Güçlü bir parola girin ve onaylayın. Bir kez daha sonra kullanılan hello parola toobe için istenir. Tıklatın **Evet** hello son tooimport adresindeki onu toohello güvenilen sertifika yetkilileri kök deponuza.

### <a name="create-a-pfx-file"></a>Bir PFX dosyası oluşturma
Hello komutu aşağıdaki hello yürütme nerede makecert yürütüldü; aynı penceresi Kullanım, kullanılan toocreate hello sertifikanın aynı parolayı hello:

    pvk2pfx -pvk MyCert.pvk -spc MyCert.cer -pfx MyCert.pfx -pi <password>

### <a name="import-hello-client-certificate-into-hello-personal-store"></a>Merhaba kişisel deposuna Hello istemci sertifikasını içeri aktarın
1. Windows Gezgini'nde çift tıklayarak **mycert.pfx'i**.
2. Merhaba, **Sertifika Alma Sihirbazı'nı** seçin **geçerli kullanıcı** tıklatıp **sonraki**.
3. Merhaba dosya yolunu doğrulayın ve tıklatın **sonraki**.
4. Türü hello parola bırakın **dahil tüm genişletilmiş özellikleri** denetlenir ve tıklatın **sonraki**.
5. Bırakın **Otomatik Seç hello sertifika deposu [...]**  denetlenir ve tıklatın **sonraki**.
6. Tıklatın **son** ve **Tamam**.

### <a name="upload-hello-pfx-file-toohello-cloud-service"></a>Merhaba PFX dosyası toohello bulut hizmeti karşıya yükle
1. Toohello Git [Azure Portal](https://portal.azure.com).
2. Seçin **bulut hizmetlerini**.
3. Merhaba bölünmüş/Merge hizmeti için yukarıda oluşturduğunuz hello bulut hizmeti seçin.
4. Tıklatın **sertifikaları** hello üst menüsünde.
5. Tıklatın **karşıya** hello alt çubuğunda.
6. Merhaba PFX dosyasını seçin ve hello girin yukarıdaki aynı parola.
7. Tamamlandığında, hello sertifika parmak izi hello yeni giriş hello listesinde kopyalayın.

### <a name="update-hello-service-configuration-file"></a>Merhaba hizmeti yapılandırma dosyasını güncelleştir
Yukarıdaki hello parmak izi/value özniteliği bu ayarların kopyalanan hello sertifika parmak izi yapıştırın.
Merhaba çalışan rolü için:
   ```
    <Setting name="DataEncryptionPrimaryCertificateThumbprint" value="" />
    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />
   ```

Merhaba web rolü için:

   ```
    <Setting name="AdditionalTrustedRootCertificationAuthorities" value="" />
    <Setting name="AllowedClientCertificateThumbprints" value="" />
    <Setting name="DataEncryptionPrimaryCertificateThumbprint" value="" />
    <Certificate name="SSL" thumbprint="" thumbprintAlgorithm="sha1" />
    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />
    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />
   ```

Lütfen sunucu sertifikası ve istemci sertifikaları Merhaba, üretim dağıtımları ayrı sertifika şifreleme için CA ' nın hello için kullanılması gereken dikkat edin. Bu ayrıntılı yönergeler için bkz: [Güvenlik Yapılandırması](sql-database-elastic-scale-split-merge-security-configuration.md).

## <a name="deploy-your-service"></a>Hizmet dağıtma
1. Toohello Git [Azure portal](https://manage.windowsazure.com).
2. Merhaba tıklatın **bulut Hizmetleri** sekmesinde hello solda ve daha önce oluşturduğunuz hello bulut hizmeti seçin.
3. Tıklatın **Pano**.
4. Ortamı hazırlama hello seçin ve ardından **yeni bir hazırlama dağıtımı karşıya**.
   
   ![Hazırlama][3]
5. Merhaba iletişim kutusunda, bir dağıtım etiketini girin. 'Paketi' ve 'Configuration' için 'Den yerel' tıklatın ve hello seçin **SplitMergeService.cspkg** dosyası ve daha önce yapılandırılmış .cscfg dosyanız.
6. Etiketli o hello onay kutusunu olun **bir veya daha fazla rol tek bir örnek içeriyorsa bile Dağıt** denetlenir.
7. Merhaba alt sağ toobegin hello dağıtımda Hello onay düğmesine basın. Tootake beklediğiniz birkaç dakika toocomplete.

   ![Karşıya Yükle][4]

## <a name="troubleshoot-hello-deployment"></a>Merhaba dağıtım sorunlarını gider
Web rolünüz çevrimiçi toocome başarısız olursa, büyük olasılıkla hello güvenlik yapılandırması ile ilgili bir sorun olur. SSL yukarıda açıklandığı şekilde yapılandırıldığından bu hello denetleyin.

Çalışan rolü çevrimiçi toocome başarısız olur, ancak web rolünüz başarılı, büyük olasılıkla daha önce oluşturduğunuz toohello durum veritabanına bağlanırken bir sorun olur.

* Merhaba bağlantı dizesinde, .cscfg doğru olduğundan emin olun.
* Merhaba sunucu ve veritabanı var olduğundan ve hello kullanıcı kimliği ve parola doğru olduğunu denetleyin.
* Azure SQL DB için hello bağlantı dizesi hello biçiminde olmalıdır:

   ```  
   Server=myservername.database.windows.net; Database=mydatabasename;User ID=myuserID; Password=mypassword; Encrypt=True; Connection Timeout=30
   ```

* Bu hello sunucu adı ile başlayan değil olun **https://**.
* Azure SQL DB sunucunuz Azure Hizmetleri tooconnect tooit verdiğinden emin olun. toodo Bu, https://manage.windowsazure.com açın, "SQL veritabanlarını" Merhaba üzerinde sol tıklayın, "" Merhaba üstünde sunucular ve sunucunuzu seçin. Tıklatın **Yapılandır** hello en üst ve o hello olun **Azure Hizmetleri** ayar çok "Evet". (Merhaba önkoşullara bakın, bu makalenin hello üst kısmına).

## <a name="test-hello-service-deployment"></a>Merhaba hizmet dağıtımı test etme
### <a name="connect-with-a-web-browser"></a>Bir web tarayıcısı ile bağlanma
Bölünmüş birleştirme hizmetinizin Hello web uç noktası belirleyin. Bu hello Klasik Azure portalı giderek toohello tarafından bulabilirsiniz **Pano** , bulut hizmeti ve altında arayan **Site URL'si** hello sağ tarafında. Değiştir **http://** ile **https://** hello varsayılan güvenlik ayarlarını hello HTTP uç noktası devre dışı olduğundan. Başlangıç sayfası, bu URL için tarayıcınıza yükleyin.

### <a name="test-with-powershell-scripts"></a>PowerShell komut dosyalarıyla test
Merhaba dağıtım ve ortamınıza dahil hello örnek PowerShell komut dosyaları çalıştırarak test edilebilir.

Merhaba komut dosyaları dahil şunlardır:

1. **SetupSampleSplitMergeEnvironment.ps1** -bölünmüş/birleştirme için bir test veri katmanını ayarlar (ayrıntılı bir açıklaması için aşağıdaki tabloya bakın)
2. **ExecuteSampleSplitMerge.ps1** -hello testi test işlemlerini yürüten veri katmanı (ayrıntılı bir açıklaması için aşağıdaki tabloya bakın)
3. **GetMappings.ps1** - üst düzey örnek hello geçerli durumunu hello parça eşlemeleri yazdırır komut dosyası.
4. **ShardManagement.psm1** -sarmalar Yardımcısı betik hello ShardManagement API
5. **SqlDatabaseHelpers.psm1** -Yardımcısı betik oluşturma ve SQL veritabanlarını yönetme
   
   <table style="width:100%">
     <tr>
       <th>PowerShell dosyası</th>
       <th>Adımlar</th>
     </tr>
     <tr>
       <th rowspan="5">SetupSampleSplitMergeEnvironment.ps1</th>
       <td>1.    Bir parça eşleme Yöneticisi veritabanı oluşturur</td>
     </tr>
     <tr>
       <td>2.    2 parça veritabanları oluşturur.
     </tr>
     <tr>
       <td>3.    Bu veritabanı (varolan bir parça bu veritabanlarını eşlemeleri siler) için bir parça eşleme oluşturur. </td>
     </tr>
     <tr>
       <td>4.    Her iki hello parça küçük örnek bir tablo oluşturur ve hello parça hello tabloda doldurur.</td>
     </tr>
     <tr>
       <td>5.    Merhaba SchemaInfo hello parçalı tablo için bildirir.</td>
     </tr>
   </table>
   <table style="width:100%">
     <tr>
       <th>PowerShell dosyası</th>
       <th>Adımlar</th>
     </tr>
   <tr>
       <th rowspan="4">ExecuteSampleSplitMerge.ps1 </th>
       <td>1.    Hangi hello ilk parça toohello ikinci parça yarım hello verilerinden ayırır bir bölme isteği toohello bölünmüş birleştirme hizmetine web ön uç, gönderir.</td>
     </tr>
     <tr>
       <td>2.    Yoklamalar web ön uç hello istek tamamlanana kadar bölme istek durumunu ve bekler hello için hello.</td>
     </tr>
     <tr>
       <td>3.    Hangi hello ikinci parça geri toohello ilk parça hello verileri taşır bir birleştirme isteği toohello bölünmüş birleştirme hizmetine web ön uç, gönderir.</td>
     </tr>
     <tr>
       <td>4.    Anketler hello web ön hello birleştirme isteği durumu ve hello istek tamamlanana kadar bekler.</td>
     </tr>
   </table>
   
## <a name="use-powershell-tooverify-your-deployment"></a>Dağıtımınızı PowerShell tooverify kullanın
1. Yeni bir PowerShell penceresi açın ve hello bölünmüş birleştirme paketi indirdiğiniz toohello dizinine gidin ve ardından hello "powershell" dizinine gidin.
2. Bir Azure SQL database sunucusu oluşturun (veya var olan bir sunucu seçin) burada hello parça eşleme Yöneticisi ve parça oluşturulur.
   
   > [!NOTE]
   > Merhaba SetupSampleSplitMergeEnvironment.ps1 komut dosyası oluşturur bu veritabanları üzerinde hello aynı sunucu varsayılan tookeep hello betik basit tarafından. Bu bir kısıtlaması hello bölünmüş birleştirme hizmetine kendisini değil.
   >
   
   SQL kimlik doğrulaması oturum açma ile okuma/yazma erişimi toohello DBs hello bölünmüş birleştirme hizmet toomove verileri ve güncelleştirme hello parça eşleme için gerekli. Merhaba bölünmüş birleştirme hizmetine hello bulutta çalışan olduğundan, tümleşik kimlik doğrulaması şu anda desteklemiyor.
   
   Hello Azure SQL server yapılandırıldığından emin olun, bu komut dosyası çalıştırarak hello makinenin hello IP adresinden tooallow erişim. Bu ayar hello Azure SQL sunucusu altında bulabilirsiniz / configuration / izin verilen IP adreslerini.
3. Merhaba SetupSampleSplitMergeEnvironment.ps1 komut dosyası toocreate hello örnek ortamı yürütün.
   
   Bu komut dosyasını çalıştıran var olan tüm parça eşleme yönetim verilerini hello parça eşleme manager veritabanı ve hello parça yapıları temizleyin. Toore başlatma hello parça harita veya parça istiyorsanız yararlı toorerun hello komut dosyası olabilir.
   
   Örnek komut satırı:

   ```   
     .\SetupSampleSplitMergeEnvironment.ps1 
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net'
   ```      
4. Şu anda mevcut hello Getmappings.ps1 komut dosyası tooview hello eşlemelerini hello örnek ortamında yürütün.
   
   ```
     .\GetMappings.ps1 
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net'

   ```         
5. Merhaba ExecuteSampleSplitMerge.ps1 betik tooexecute (Merhaba ilk parça toohello ikinci parça üzerinde yarı hello veri taşıma) bir bölme işlemi'i ve ardından (Merhaba verileri hello ilk parça geri taşıma) bir birleştirme işlemi yürütün. SSL ve sol hello http uç noktası devre dışı yapılandırdıysanız, hello https:// uç noktası yerine kullandığınızdan emin olun.
   
   Örnek komut satırı:

   ```   
     .\ExecuteSampleSplitMerge.ps1
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net' 
         -SplitMergeServiceEndpoint 'https://mysplitmergeservice.cloudapp.net' 
         -CertificateThumbprint '0123456789abcdef0123456789abcdef01234567'
   ```      
   
   Hello aşağıda hata alırsanız, büyük olasılıkla Web uç noktanın sertifikayla ilgili bir sorun olduğunu. Sık kullanılan Web tarayıcınızda toohello Web uç noktası bağlanmayı deneyin ve bir sertifika hatası olup olmadığını denetleyin.
   
     ```
     Invoke-WebRequest : hello underlying connection was closed: Could not establish trust relationship for hello SSL/TLSsecure channel.
     ```
   
   Bu başarılı olursa hello çıktı hello aşağıdaki gibi görünmelidir:
   
   ```
   > .\ExecuteSampleSplitMerge.ps1 -UserName 'mysqluser' -Password 'MySqlPassw0rd' -ShardMapManagerServerName 'abcdefghij.database.windows.net' -SplitMergeServiceEndpoint 'http://mysplitmergeservice.cloudapp.net' -CertificateThumbprint 0123456789abcdef0123456789abcdef01234567
   > Sending split request
   > Began split operation with id dc68dfa0-e22b-4823-886a-9bdc903c80f3
   > Polling split-merge request status. Press Ctrl-C tooend
   > Progress: 0% | Status: Queued | Details: [Informational] Queued request
   > Progress: 5% | Status: Starting | Details: [Informational] Starting split-merge state machine for request.
   > Progress: 5% | Status: Starting | Details: [Informational] Performing data consistency checks on target     shards.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source tootarget shard.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Waiting for reference tables copy     completion.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source tootarget shard.
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Moving key range [100:110) of     Sharded tables
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Successfully copied key range     [100:110) for table [dbo].[MyShardedTable]
   > ...
   > ...
   > Progress: 90% | Status: Completing | Details: [Informational] Successfully deleted shardlets in table     [dbo].[MyShardedTable].
   > Progress: 90% | Status: Completing | Details: [Informational] Deleting any temp tables that were created     while processing hello request.
   > Progress: 100% | Status: Succeeded | Details: [Informational] Successfully processed request.
   > Sending merge request
   > Began merge operation with id 6ffc308f-d006-466b-b24e-857242ec5f66
   > Polling request status. Press Ctrl-C tooend
   > Progress: 0% | Status: Queued | Details: [Informational] Queued request
   > Progress: 5% | Status: Starting | Details: [Informational] Starting split-merge state machine for request.
   > Progress: 5% | Status: Starting | Details: [Informational] Performing data consistency checks on target     shards.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source tootarget shard.
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Moving key range [100:110) of     Sharded tables
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Successfully copied key range     [100:110) for table [dbo].[MyShardedTable]
   > ...
   > ...
   > Progress: 90% | Status: Completing | Details: [Informational] Successfully deleted shardlets in table     [dbo].[MyShardedTable].
   > Progress: 90% | Status: Completing | Details: [Informational] Deleting any temp tables that were created     while processing hello request.
   > Progress: 100% | Status: Succeeded | Details: [Informational] Successfully processed request.
   > 
   ```
6. Diğer veri türleri ile deneyin! Bu komut dosyalarının tümü toospecify hello anahtar türü sağlayan isteğe bağlı - ShardKeyType parametresi alın. Int32 Hello varsayılandır ancak Int64, GUID ya da ikili de belirtebilirsiniz.

## <a name="create-requests"></a>Oluşturma istekleri
Merhaba hizmet hello web kullanıcı arabirimini kullanarak veya içeri aktarma ve isteklerinizi hello web rolü aracılığıyla göndereceğini hello SplitMerge.psm1 PowerShell modülünü kullanarak kullanılabilir.

Merhaba hizmet parçalı tablolar ve başvuru tabloları veri taşıyabilirsiniz. Parçalı tablo parçalama anahtar sütunu ve her parça üzerinde farklı satır veri sahiptir. Bir başvuru tablosu parçalı değil hello içerecek şekilde aynı veri üzerinde her parça satır. Başvuru tabloları genellikle değiştirmez ve sorgularda parçalı tablolar ile kullanılan tooJOIN olan veriler için kullanışlıdır.

Sipariş tooperform bölünmüş birleştirme işlemi, hello parçalı tablolar ve taşınmış toohave istediğiniz başvuru tabloları bildirmeniz gerekir. Bu hello ile gerçekleştirilir **SchemaInfo** API. Bu API hello olan **Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.Schema** ad alanı.

1. Her parçalı tablo için oluşturun bir **ShardedTableInfo** Merhaba tablonun üst şema adını tanımlayan nesne (isteğe bağlı, çok varsayılan olarak "dbo"), hello tablo adı ve hello hello parçalama anahtarı içeren bu tablodaki sütun adı.
2. Her başvuru tablosu için bir **ReferenceTableInfo** Merhaba tablonun üst şema adını tanımlayan nesne (isteğe bağlı, çok varsayılan olarak "dbo") ve hello tablo adı.
3. Merhaba TableInfo nesneleri tooa yeni yukarıda eklemek **SchemaInfo** nesnesi.
4. Bir başvuru tooa almak **ShardMapManager** nesne ve çağrı **GetSchemaInfoCollection**.
5. Merhaba eklemek **SchemaInfo** toohello **SchemaInfoCollection**, hello parça eşleme adı sağlama.

Bunun bir örneğini hello SetupSampleSplitMergeEnvironment.ps1 betik görülebilir.

Merhaba bölünmüş birleştirme hizmetine hello hedef veritabanı (veya hello veritabanındaki herhangi bir tablo için şema), oluşturmaz. Bir istek toohello hizmet göndermeden önce önceden oluşturulmuş olmaları gerekir.

## <a name="troubleshooting"></a>Sorun giderme
Merhaba örnek powershell komut dosyaları çalıştırırken hello ileti aşağıda görebilirsiniz:

   ```
   Invoke-WebRequest : hello underlying connection was closed: Could not establish trust relationship for hello SSL/TLS secure channel.
   ```

Bu hata, SSL sertifikası doğru yapılandırılmamış anlamına gelir. Lütfen 'Bağlanıyor bir web tarayıcısı' bölümündeki hello yönergeleri izleyin.

İstek gönderemez varsa bu görebilirsiniz:

```
[Exception] System.Data.SqlClient.SqlException (0x80131904): Could not find stored procedure 'dbo.InsertRequest'. 
```

Bu durumda, belirli hello ayarı için yapılandırma dosyanızı denetleyin **WorkerRoleSynchronizationStorageAccountConnectionString**. Bu hata genellikle o hello çalışan rolü hello meta veri veritabanı ilk kullanımda başarıyla başlatılamadı gösterir. 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/allowed-services.png
[2]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/manage.png
[3]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/staging.png
[4]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/upload.png
[5]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/storage.png

