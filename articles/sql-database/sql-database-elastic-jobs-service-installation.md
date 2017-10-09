---
title: "aaaInstalling esnek veritabanı işleri | Microsoft Docs"
description: "Merhaba esnek iş özellik yüklenmesinde size yol gösterir."
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: cbe0aa2b-17e3-4b6f-a16f-6ebc1f5a66af
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 0349f66a4428f81d00d43681d7f2177f273ec032
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="installing-elastic-database-jobs-overview"></a>Yükleme esnek veritabanı işleri genel bakış
[**Esnek veritabanı iş** ](sql-database-elastic-jobs-overview.md) PowerShell ile yüklenebilir veya toocreate Azure Klasik Portal.You elde hello erişmek ve işleri yalnızca hello PowerShell paketi yüklerseniz hello PowerShell API kullanarak yönetmek. Ayrıca, hello PowerShell API'lerinden sağlayın hello portal önemli ölçüde daha fazla işlevsellik bu anda.

Zaten yüklediyseniz, **esnek veritabanı işleri** mevcut bir kümeden hello Portal aracılığıyla **esnek havuz**, hello son Powershell Önizleme, mevcut yüklemenizi betikleri tooupgrade içerir. Yüksek oranda olduğu tooupgrade yükleme toohello en son önerilen **esnek veritabanı işleri** sipariş tootake aracılığıyla kullanıma sunulan yeni işlevsellikten avantajlarından bileşenlerinde hello PowerShell API'leri.

## <a name="prerequisites"></a>Ön koşullar
* Azure aboneliği. Ücretsiz deneme için bkz: [ücretsiz deneme sürümü](https://azure.microsoft.com/pricing/free-trial/).
* Azure PowerShell. Hello kullanarak hello en son sürümünü yüklemek [Web Platformu yükleyicisi](http://go.microsoft.com/fwlink/p/?linkid=320376). Ayrıntılı bilgi için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).
* [NuGet komut satırı yardımcı programı](https://nuget.org/nuget.exe) kullanılan tooinstall hello esnek veritabanı işleri paketidir. Daha fazla bilgi için http://docs.nuget.org/docs/start-here/installing-nuget bakın.

## <a name="download-and-import-hello-elastic-database-jobs-powershell-package"></a>Karşıdan yükle ve hello esnek veritabanı işleri PowerShell paketi Al
1. Microsoft Azure PowerShell komut penceresini başlatın ve NuGet komut satırı yardımcı programı (nuget.exe) indirdiğiniz toohello dizinine gidin.
2. İndirme ve içeri aktarma **esnek veritabanı işleri** komutu aşağıdaki hello ile Merhaba geçerli dizine paketi:
   
        PS C:\>.\nuget install Microsoft.Azure.SqlDatabase.Jobs -prerelease
   
    Merhaba **esnek veritabanı işleri** dosyaları hello yerel dizin adlı bir klasöre yerleştirilir **Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x** nerede *x.x.xxxx.x* Merhaba sürüm numarası yansıtır. (gerekli istemci .dll dahil) hello PowerShell cmdlet'leri hello bulunan **tools\ElasticDatabaseJobs** alt dizini hello PowerShell komut dosyaları tooinstall, yükseltme ve ayrıca kaldırma hello bulunan  **Araçlar** alt dizini.
3. Cd Araçlar, örneğin yazarak hello Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x klasörü altında toohello Araçlar alt dizinine gidin:
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools

4. Merhaba.\InstallElasticDatabaseJobsCmdlets.ps1 komut dosyası toocopy hello ElasticDatabaseJobs dizini $home\Documents\WindowsPowerShell\Modules yürütün. Bu da otomatik olarak hello modülü kullanmak, örneğin alınır:
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobsCmdlets.ps1
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\InstallElasticDatabaseJobsCmdlets.ps1

## <a name="install-hello-elastic-database-jobs-components-using-powershell"></a>PowerShell kullanarak hello esnek veritabanı işleri bileşenlerini yükle
1. Microsoft Azure PowerShell komut penceresini başlatın ve toohello \tools hello Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x klasörü altında alt dizinine gidin: cd \tools yazın
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools

2. Merhaba.\InstallElasticDatabaseJobs.ps1 PowerShell betiğini yürütün ve istenen değişkenleri için değerleri girin. Bu komut dosyası açıklanan hello bileşenleri oluşturacak [esnek veritabanı iş bileşenleri ve fiyatlandırma](sql-database-elastic-jobs-overview.md#components-and-pricing) hello Azure bulut hizmeti yapılandırma ile birlikte tooappropriately hello bağımlı bileşenlerini kullanır.

        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobs.ps1
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\InstallElasticDatabaseJobs.ps1

Bu komutu çalıştırdığınızda bir pencere açılır girmenizi isteyen bir **kullanıcı adı** ve **parola**. Bu Azure kimlik bilgilerinizi değil, hello kullanıcı adı ve hello yönetici kimlik bilgileri toocreate hello yeni sunucu için istediğiniz parola girin.

Bu örnek çağrısının sağlanan hello parametreleri için istenen ayarlarınız değiştirilebilir. Merhaba aşağıdaki her bir parametreyi hello davranışını daha fazla bilgi sağlar:

<table style="width:100%">
  <tr>
    <th>Parametre</th>
    <th>Açıklama</th>
  </tr>

<tr>
    <td>resourceGroupName</td>
    <td>Yeni Azure bileşenleri oluşturulan toocontain hello oluşturulan hello Azure kaynak grubu adı sağlar. Bu parametre çok varsayılan olarak "__ElasticDatabaseJob". Değil toochange önerilen bu değer.</td>
    </tr>

</tr>

    <tr>
    <td>ResourceGroupLocation</td>
    <td>Yeni Azure bileşenleri oluşturulan hello için kullanılan hello Azure konumu toobe sağlar. Bu parametre varsayılan olarak toohello Orta ABD konumu.</td>
</tr>

<tr>
    <td>ServiceWorkerCount</td>
    <td>Hizmet çalışanları tooinstall Hello sayısını sağlar. Bu parametre too1 varsayılan olarak ayarlanır. Daha yüksek bir sayı çalışanı hello hizmeti ve tooprovide yüksek kullanılabilirlik çıkışı kullanılan tooscale olabilir. Toouse "2" Merhaba hizmetinin yüksek kullanılabilirliğin gerektiği dağıtımlar için önerilir.</td>
    </tr>

</tr>
    <tr>
    <td>ServiceVmSize</td>
    <td>Merhaba VM boyutu hello bulut hizmeti içinde kullanımı sağlar. Bu parametre tooA0 varsayılan olarak ayarlanır. Parametre değerlerini A0/A1/A2/A3 hello çalışan rolü toouse çok küçük/küçük/Orta/büyük boyutu sırasıyla neden kabul edilir. FO çalışan rolü boyutları hakkında daha fazla bilgi görmek [esnek veritabanı iş bileşenleri ve fiyatlandırma](sql-database-elastic-jobs-overview.md#components-and-pricing).</td>
</tr>

</tr>
    <tr>
    <td>SqlServerDatabaseSlo</td>
    <td>Merhaba hizmet düzeyi hedefi Standard edition için sağlar. Bu parametre tooS0 varsayılan olarak ayarlanır. Parametre değerlerini S0/S1/S2/S3 hello Azure SQL veritabanı neden kabul edilir toouse hello ilgili SLO. SQL veritabanı Slo'lar hakkında daha fazla bilgi için bkz: [esnek veritabanı iş bileşenleri ve fiyatlandırma](sql-database-elastic-jobs-overview.md#components-and-pricing).</td>
</tr>

</tr>
    <tr>
    <td>SqlServerAdministratorUserName</td>
    <td>Hello Yöneticisi kullanıcı adı için yeni Azure SQL Database sunucusu oluşturulan hello sağlar. Belirtilmediğinde, bir PowerShell kimlik bilgileri penceresi hello kimlik bilgileri tooprompt açın.</td>
</tr>

</tr>
    <tr>
    <td>SqlServerAdministratorPassword</td>
    <td>Merhaba yönetici parolası yeni Azure SQL Database sunucusu oluşturulan Merhaba sağlar. Sağlanan değil, bir PowerShell kimlik bilgileri penceresi hello kimlik bilgileri tooprompt açın.</td>
</tr>
</table>

Çok sayıda paralel çok sayıda veritabanı karşı çalışan işleri sahip hedef sistemleri için toospecify parametreleri gibi önerilir: - ServiceWorkerCount 2 - ServiceVmSize A2 - SqlServerDatabaseSlo S2.

    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobs.ps1
    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>.\InstallElasticDatabaseJobs.ps1 -ServiceWorkerCount 2 -ServiceVmSize A2 -SqlServerDatabaseSlo S2

## <a name="update-an-existing-elastic-database-jobs-components-installation-using-powershell"></a>PowerShell kullanarak var olan esnek veritabanı işleri bileşenleri yüklemeyi güncelleştirme
**Esnek veritabanı iş** içinde var olan bir yüklemesini ölçek ve yüksek kullanılabilirlik için güncelleştirilmiştir. Bu işlem toodrop gerek kalmadan servis kodu gelecekteki yükseltmeler için sağlar ve hello denetim veritabanı oluşturun. Bu işlem ayrıca hello içinde kullanılabilir aynı sürüm toomodify hello hizmet VM boyutu veya hello server çalışan sayısı.

tooupdate hello VM boyutu yüklemesinin parametrelerle betik aşağıdaki çalışma hello tercih ettiğiniz toohello değerleri güncelleştirildi.

    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>Unblock-File .\UpdateElasticDatabaseJobs.ps1
    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>.\UpdateElasticDatabaseJobs.ps1 -ServiceVmSize A1 -ServiceWorkerCount 2

<table style="width:100%">
  <tr>
  <th>Parametre</th>
  <th>Açıklama</th>
</tr>

  <tr>
    <td>resourceGroupName</td>
    <td>Merhaba esnek veritabanı iş bileşenler ilk yüklendiğinde kullanılan hello Azure kaynak grubu adını tanımlar. Bu parametre çok varsayılan olarak "__ElasticDatabaseJob". Bunu olmadığından toochange önerilen bu değer bu parametre toospecify sahip olmamalıdır.</td>
    </tr>
</tr>

</tr>

  <tr>
    <td>ServiceWorkerCount</td>
    <td>Hizmet çalışanları tooinstall Hello sayısını sağlar.  Bu parametre too1 varsayılan olarak ayarlanır.  Daha yüksek bir sayı çalışanı hello hizmeti ve tooprovide yüksek kullanılabilirlik çıkışı kullanılan tooscale olabilir.  Toouse "2" Merhaba hizmetinin yüksek kullanılabilirliğin gerektiği dağıtımlar için önerilir.</td>
</tr>

</tr>

    <tr>
    <td>ServiceVmSize</td>
    <td>Merhaba VM boyutu hello bulut hizmeti içinde kullanımı sağlar. Bu parametre tooA0 varsayılan olarak ayarlanır. Parametre değerlerini A0/A1/A2/A3 hello çalışan rolü toouse çok küçük/küçük/Orta/büyük boyutu sırasıyla neden kabul edilir. FO çalışan rolü boyutları hakkında daha fazla bilgi görmek [esnek veritabanı iş bileşenleri ve fiyatlandırma](sql-database-elastic-jobs-overview.md#components-and-pricing).</td>
</tr>

</table>

## <a name="install-hello-elastic-database-jobs-components-using-hello-portal"></a>Merhaba Portal kullanarak hello esnek veritabanı işleri bileşenlerini yükle
Bulduktan sonra [bir esnek havuz oluşturulan](sql-database-elastic-pool-manage-portal.md), yükleyebileceğiniz **esnek veritabanı işleri** bileşenleri tooenable yürütme hello esnek havuzdaki her veritabanında yönetim görevleri. Ne zaman kullanarak hello aksine **esnek veritabanı işleri** PowerShell API'lerinden hello portal arabirimidir şu anda kısıtlı tooonly var olan bir havuzu karşı çalıştırma.

**Zaman toocomplete tahmini:** 10 dakika.

1. Merhaba aracılığıyla hello esnek havuzun hello Pano görünümden [Azure Portal](https://portal.azure.com/#) , tıklatın **oluşturma işi**.
2. Hello için bir işi ilk kez oluşturuyorsanız, yüklemelisiniz **esnek veritabanı işleri** tıklayarak **Önizleme koşulları**.
3. Onay kutusunu tıklatarak hello koşulları hello kabul edin.
4. Yükleme Hello "Hizmetler" Görüntüle'yi tıklatın **iş kimlik bilgilerini**.
   
    ![Merhaba Hizmetleri Yükleniyor][1]
5. Bir kullanıcı adı ve veritabanı yönetici parolasını yazın Merhaba yüklemesinin bir parçası olarak, yeni bir Azure SQL veritabanı sunucusu oluşturulur. Bu yeni sunucu içinde hello denetim veritabanı olarak bilinen yeni bir veritabanı oluşturulur ve esnek veritabanı işleri toocontain hello meta veriler kullanılır. Merhaba kullanıcı adı ve parola burada oluşturulan toohello denetim veritabanında günlük hello amacı için kullanılır. Ayrı bir kimlik bilgisi komut dosyası yürütme hello havuz içindeki hello veritabanlarında için kullanılır.
   
    ![Kullanıcı adı ve parola oluşturun.][2]
6. Merhaba Tamam düğmesine tıklayın. Merhaba bileşenleri oluşturulan sizin için birkaç dakika içinde yeni bir [kaynak grubu](../azure-resource-manager/resource-group-overview.md). Merhaba yeni kaynak grubu sabitlendiği toohello Panosu, aşağıda gösterildiği gibi başlatın. Oluşturduktan sonra esnek veritabanı işleri (bulut hizmeti, SQL veritabanı, hizmet veri yolu ve depolama) tüm hello grubunda oluşturulur.
   
    ![Başlangıç Panosu kaynak grubunda][3]
7. Toocreate deneyin veya esnek veritabanı işleri yüklüyor olsa da, sağlanırken bir işi yönetiyorsanız **kimlik bilgileri** iletiden hello görürsünüz.
   
    ![Dağıtımı hala devam ediyor][4]

Kaldırma işlemi gerekiyorsa, hello kaynak grubunu silin. Bkz: [nasıl toouninstall hello esnek veritabanı iş bileşenleri](sql-database-elastic-jobs-uninstall.md).

## <a name="next-steps"></a>Sonraki adımlar
Betik yürütme hello grubunda, daha fazla bilgi için her bir veritabanına oluşturulan için hello uygun haklara sahip bir kimlik bilgisi olun [SQL veritabanınızın güvenliğini sağlama](sql-database-manage-logins.md).
Bkz: [oluşturma ve bir esnek veritabanı işlerini yönetme](sql-database-elastic-jobs-create-and-manage.md) tooget başlatıldı.

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-service-installation/screen-1.png
[2]: ./media/sql-database-elastic-jobs-service-installation/credentials.png
[3]: ./media/sql-database-elastic-jobs-service-installation/start-board.png
[4]: ./media/sql-database-elastic-jobs-service-installation/not-done.png
