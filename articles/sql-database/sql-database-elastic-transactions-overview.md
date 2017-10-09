---
title: "Bulut veritabanları arasında aaaDistributed işlemleri"
description: "Azure SQL Database esnek veritabanı işlemleri genel bakış"
services: sql-database
documentationcenter: 
author: torsteng
manager: jhubbard
editor: torsteng
ms.assetid: e14df7a3-7788-4cfb-bcd1-7ad6433ef1f9
ms.service: sql-database
ms.custom: scale out apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: sql-database
ms.date: 05/27/2016
ms.author: torsteng
ms.openlocfilehash: 9a18f2749108d337bf115b3dc21dd0c7828dd9c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="distributed-transactions-across-cloud-databases"></a>Bulut veritabanlarında dağıtılmış işlemler
Esnek veritabanı işlemleri için Azure SQL veritabanı (SQL DB) SQL DB birkaç veritabanlarında span toorun işlemleri izin verin. Esnek veritabanı işlemleri için SQL DB ADO .NET kullanarak .NET uygulamaları için kullanılabilir ve hello kullanarak hello tanıdık programlama deneyimiyle tümleştirmenize [System.Transaction](https://msdn.microsoft.com/library/system.transactions.aspx) sınıfları. tooget hello kitaplığı bkz [.NET Framework 4.6.1 (Web Yükleyicisi)](https://www.microsoft.com/download/details.aspx?id=49981).

Şirket içinde böyle bir senaryo, Microsoft Dağıtılmış İşlem Düzenleyicisi (MSDTC) çalıştıran genellikle gereklidir. MSDTC Azure hizmet olarak Platform uygulama için kullanılabilir olmadığından, hello özelliği toocoordinate dağıtılmış işlemler artık doğrudan bütünleştirilmiştir SQL Veritabanına. Uygulamaları tooany SQL veritabanı toolaunch dağıtılmış işlemleri bağlanabilir ve hello veritabanlarından birini saydam hello dağıtılmış işlem hello aşağıdaki şekilde gösterildiği gibi koordine. 

  ![Dağıtılmış işlemler Azure SQL Database esnek veritabanı işlemleri kullanma ][1]

## <a name="common-scenarios"></a>Genel senaryolar
Esnek veritabanı işlemleri için SQL DB birkaç farklı SQL veritabanlarında depolanan uygulamaları toomake atomik değişiklikleri toodata etkinleştirin. C# ve .NET istemci-tarafı geliştirme deneyimlerinde Hello Önizleme odaklanır. T-SQL kullanarak bir sunucu tarafı deneyimi daha sonraki bir zamana planlanmaktadır.  
Esnek veritabanı işlemleri hedefleri hello senaryolar:

* Azure çok veritabanı uygulamalarında: farklı veri türleri farklı veritabanlarında bulunan şekilde bu senaryoyla veri dikey SQL DB birkaç veritabanlarında genelinde bölümlenmiş. Bazı işlemler iki veya daha fazla veritabanlarında tutulur değişiklikleri toodata gerektirir. Merhaba uygulaması veritabanları arasında esnek veritabanı işlemleri toocoordinate hello değişiklikleri kullanır ve kararlılık emin olun.
* Azure parçalı veritabanı uygulamalarında: Bu senaryo ile Merhaba veri katmanı hello kullanan [esnek veritabanı istemci Kitaplığı](sql-database-elastic-database-client-library.md) ya da SQL DB içinde birçok veritabanı arasında self parçalama toohorizontally bölüm hello verileri. Bir belirgin kullanım durumu değişiklikleri kiracılar span hello gerek tooperform atomik değişiklikleri parçalı bir çok kiracılı uygulama için durumdur. Örneği için bir kiracı tooanother, her iki bulunan farklı veritabanlarında bir aktarımı düşünün. Hangi sırayla genellikle bazı atomik işlemleri gereksinimlerini toostretch hello için kullanılan birkaç veritabanları arasında aynı Kiracı gelir büyük bir kiracı için hassas parçalama tooaccommodate kapasite gereksinimlerini buna ikinci bir durumdur. Veritabanları arasında çoğaltılan atomik güncelleştirmeleri tooreference veri buna üçüncü bir durumdur. Bu satırlar boyunca atomik, hizmetteki, işlemleri şimdi hello Önizleme kullanarak birçok veritabanı arasında Eşgüdümlü.
  Esnek veritabanı işlemleri veritabanları arasında iki aşamalı yürütme tooensure işlem kararlılık kullanın. Tek bir işlem içinde her defasında 100'den az veritabanları gerektiren işlemler için iyi bir tercihtir olur. Bu sınırlamaları uygulanmaz ancak bir performans ve esnek veritabanı işlemleri toosuffer başarı oranları bu sınırları aşıldığında beklemelisiniz.

## <a name="installation-and-migration"></a>Yükleme ve yükseltme
SQL veritabanına esnek veritabanı işlemleri için Hello özellikleri güncelleştirmeleri toohello .NET kitaplıkları System.Data.dll ve System.Transactions.dll sağlanır. Merhaba DLL'leri bu iki aşamalı yürütme gerektiğinde kullanılır olun tooensure Atom oranı. Esnek veritabanı işlemleri kullanarak toostart geliştirme uygulamaları yükleme [.NET Framework 4.6.1](https://www.microsoft.com/download/details.aspx?id=49981) veya sonraki bir sürümü. Merhaba .NET framework'ün daha eski bir sürümünde çalışan, işlemleri toopromote tooa dağıtılmış işlem başarısız olur ve bir özel durum oluşturuldu.

Yükleme sonrasında, bağlantıları tooSQL DB içinde System.Transactions hello dağıtılmış işlem API'leri kullanabilirsiniz. Bu API'leri kullanarak mevcut MSDTC uygulamalarınız varsa, yalnızca .NET 4.6 için mevcut uygulamalarınızı hello 4.6.1 yükledikten sonra yeniden Framework. Projelerinizi .NET 4.6 hedefliyorsanız, bunlar güncelleştirilmiş hello DLL'lerden hello yeni Framework sürümünü ve dağıtılmış işlem API çağrıları DB şimdi başarılı olur bağlantıları tooSQL ile birlikte otomatik olarak kullanır.

Esnek veritabanı işlem MSDTC yüklemek gerekmez unutmayın. Bunun yerine, esnek veritabanı işlemleri doğrudan tarafından ve SQL DB içinde yönetilir. MSDTC dağıtımını değil SQL DB ile gerekli toouse dağıtılmış işlemler olduğundan bu bulut senaryolarında önemli ölçüde basitleştirir. 4. Bölüm nasıl toodeploy esnek veritabanı işlemleri hello bulut uygulamaları tooAzure birlikte .NET framework gerekli ve daha ayrıntılı olarak açıklanmaktadır.

## <a name="development-experience"></a>Geliştirme deneyimi
### <a name="multi-database-applications"></a>Birden çok veritabanı uygulamaları
Merhaba aşağıdaki örnek kod hello tanıdık programlama deneyimi ile .NET System.Transactions kullanır. Merhaba TransactionScope sınıfı .NET ortam bir işlemde oluşturur. ("Ortam işlem" bulunan hello geçerli iş parçacığı biridir.) Tüm bağlantılar TransactionScope Hello içinde açılmış hello işlemde katılın. Farklı veritabanlarına katılırsanız, hello işlem otomatik olarak yükseltilmiş tooa dağıtılmış bir işlemdir. Merhaba hello işlem sonucunu bir yürütme hello kapsam toocomplete tooindicate ayarlayarak denetlenir.

    using (var scope = new TransactionScope())
    {
        using (var conn1 = new SqlConnection(connStrDb1))
        {
            conn1.Open();
            SqlCommand cmd1 = conn1.CreateCommand();
            cmd1.CommandText = string.Format("insert into T1 values(1)");
            cmd1.ExecuteNonQuery();
        }

        using (var conn2 = new SqlConnection(connStrDb2))
        {
            conn2.Open();
            var cmd2 = conn2.CreateCommand();
            cmd2.CommandText = string.Format("insert into T2 values(2)");
            cmd2.ExecuteNonQuery();
        }

        scope.Complete();
    }

### <a name="sharded-database-applications"></a>Parçalı veritabanı uygulamaları
Esnek veritabanı işlemleri SQL DB için de destek kullandığınız hello esnek veritabanı istemci kitaplığı tooopen bağlantılarının hello OpenConnectionForKey yöntemi için genişletilmiş veri dağıtılmış işlemler Eşgüdümleme katmanı. Burada, tooguarantee işlemsel tutarlılık için değişiklikleri birkaç farklı parçalama anahtar değerleri arasında gerektirmelidir. Merhaba farklı parçalama anahtar değerleri barındırma bağlantıları toohello parça OpenConnectionForKey kullanarak aracılı. İşlem Güvenceleri sağlayarak bir dağıtılmış işlem gerektirir, hello genel durumda toodifferent parça hello bağlantıları olabilir. Aşağıdaki kod örneği hello bu yaklaşım gösterilmektedir. Bu, shardmap adlı bir değişken bir parça eşleme hello esnek veritabanı istemci Kitaplığı'ndan kullanılan toorepresent olduğunu varsayar:

    using (var scope = new TransactionScope())
    {
        using (var conn1 = shardmap.OpenConnectionForKey(tenantId1, credentialsStr))
        {
            conn1.Open();
            SqlCommand cmd1 = conn1.CreateCommand();
            cmd1.CommandText = string.Format("insert into T1 values(1)");
            cmd1.ExecuteNonQuery();
        }

        using (var conn2 = shardmap.OpenConnectionForKey(tenantId2, credentialsStr))
        {
            conn2.Open();
            var cmd2 = conn2.CreateCommand();
            cmd2.CommandText = string.Format("insert into T1 values(2)");
            cmd2.ExecuteNonQuery();
        }

        scope.Complete();
    }


## <a name="net-installation-for-azure-cloud-services"></a>.NET yüklemesi için Azure bulut Hizmetleri
Azure birkaç teklifleri toohost .NET uygulamalarını sağlar. Merhaba farklı teklifleri karşılaştırması kullanılabilir [Azure App Service, Cloud Services ve sanal makineler karşılaştırması](../app-service-web/choose-web-site-cloud-service-vm.md). Merhaba konuk işletim sistemi hello sunumun .NET 4.6.1 esnek işlemleri için gerekli küçükse, tooupgrade hello konuk işletim sistemi too4.6.1 gerekir. 

Azure uygulama hizmetleri için toohello konuk işletim sistemi tarafından şu anda desteklenmiyor yükseltir. Azure Virtual Machines için yalnızca VM hello oturum ve hello en son .NET framework için hello yükleyiciyi çalıştırın. Azure bulut Hizmetleri için hello başlangıç görevleri, dağıtımınızın içine yeni bir .NET sürümünü tooinclude hello yüklemesi gerekir. Merhaba kavramlar ve adımlar konusunda belgelenir [bir bulut hizmet rolü .NET yükleme](../cloud-services/cloud-services-dotnet-install-dotnet.md).  

.NET 4.6.1 hello Azure bulut Hizmetleri işlem .NET 4.6 yükleyici hello daha önyükleme sırasında daha fazla geçici depolama alanı gerektirebilir için yükleyici hello unutmayın. tooensure başarılı bir yükleme, tooincrease geçici depolama için Azure bulut hizmetinize ServiceDefinition.csdef dosyanızda hello LocalResources bölümü ve hello ortam ayarları, başlangıç görevinin hello aşağıda gösterildiği gibi gereksinim Örnek:

    <LocalResources>
    ...
        <LocalStorage name="TEMP" sizeInMB="5000" cleanOnRoleRecycle="false" />
        <LocalStorage name="TMP" sizeInMB="5000" cleanOnRoleRecycle="false" />
    </LocalResources>
    <Startup>
        <Task commandLine="install.cmd" executionContext="elevated" taskType="simple">
            <Environment>
        ...
                <Variable name="TEMP">
                    <RoleInstanceValue xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='TEMP']/@path" />
                </Variable>
                <Variable name="TMP">
                    <RoleInstanceValue xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='TMP']/@path" />
                </Variable>
            </Environment>
        </Task>
    </Startup>

## <a name="transactions-across-multiple-servers"></a>Birden çok sunucudaki işlemleri
Esnek veritabanı işlemleri, Azure SQL veritabanında mantıksal farklı sunucular arasında desteklenir. Mantıksal sunucu sınırları işlemler arası olduğunda, hello Katılımcı sunucular önce karşılıklı iletişim ilişkisi girdiğiniz toobe gerekir. Merhaba iletişimi ilişki kurulduktan sonra iki sunucu veritabanlarından esnek hareketlerle katılabilir hello hiçbirinde herhangi bir veritabanı diğer sunucu hello. İkiden fazla mantıksal sunucularının genişleme işlemleri ile iletişim ilişkisi herhangi bir mantıksal sunucu çifti için yerinde toobe gerekir.

Esnek veritabanı işlemleri için PowerShell cmdlet'leri toomanage sunucular arası iletişim ilişki aşağıdaki hello kullan:

* **AzureRmSqlServerCommunicationLink yeni**: Bu cmdlet toocreate Azure SQL DB mantıksal iki sunucu arasında yeni bir iletişim ilişki kullanın. Merhaba her iki sunucuyu hello hareketlerle diğer sunucu başlatabilirsiniz yani simetrik ilişkidir.
* **Get-AzureRmSqlServerCommunicationLink**: Bu cmdlet tooretrieve mevcut iletişimi kullanan ilişkileri ve özellikleri.
* **Remove-AzureRmSqlServerCommunicationLink**: Bu cmdlet tooremove var olan bir iletişim ilişkisinin kullanın. 

## <a name="monitoring-transaction-status"></a>İşlem durumunu izleme
SQL DB toomonitor durumunu ve ilerlemesini, devam eden esnek veritabanı işlem içinde dinamik yönetim görünümlerini (Dmv'leri) kullanın. Tüm Dmv'leri ilgili tootransactions SQL DB dağıtılmış işlemlere ilgilidir. Merhaba karşılık gelen listesi Dmv'leri burada bulabilirsiniz: [işlem ilgili dinamik yönetim görünümlerini ve işlevleri (Transact-SQL)](https://msdn.microsoft.com/library/ms178621.aspx).

Bu Dmv'leri özellikle yararlı olur:

* **sys.DM\_tran\_etkin\_işlemleri**: geçerli durumda etkin işlemlerin ve durumlarını listeler. Merhaba UOW (iş birimi) sütun toohello ait hello farklı alt işlemleri belirlemek aynı dağıtılmış işlem. Tüm işlemler aynı dağıtılmış işlem taşımak hello dahilinde hello aynı UOW değeri. Merhaba bkz [DMV belgelerine](https://msdn.microsoft.com/library/ms174302.aspx) daha fazla ayrıntı için.
* **sys.DM\_tran\_veritabanı\_işlemleri**: hello günlüğünde hello hareketinin yerleştirme gibi işlemleri hakkında ek bilgi sağlar. Merhaba bkz [DMV belgelerine](https://msdn.microsoft.com/library/ms186957.aspx) daha fazla ayrıntı için.
* **sys.DM\_tran\_kilitleri**: şu anda devam eden işlemler tarafından tutulan hello kilitleri hakkında bilgi sağlar. Merhaba bkz [DMV belgelerine](https://msdn.microsoft.com/library/ms190345.aspx) daha fazla ayrıntı için.

## <a name="limitations"></a>Sınırlamalar
sınırlamalar şu anda aşağıdaki hello tooelastic veritabanı işlemleri SQL veritabanına uygulayın:

* Yalnızca işlemleri SQL DB veritabanları arasında desteklenir. Diğer [X / açmak XA](https://en.wikipedia.org/wiki/X/Open_XA) kaynak sağlayıcıları ve veritabanları SQL DB dışına esnek veritabanı işlemleri katılmak olamaz. Esnek veritabanı işlemleri arasında şirket içinde SQL Server ve Azure SQL veritabanları uzatma edilemez olduğunu anlamına gelir. Şirket içi dağıtılmış işlemler için toouse MSDTC devam edin. 
* Yalnızca istemci Eşgüdümlü işlemleri bir .NET uygulamasında desteklenir. T-SQL BEGIN TRANSACTION dağıtılmış gibi sunucu tarafı desteği, planlanmış, ancak henüz kullanılamıyor. 
* WCF hizmetleri üzerinden işlemleri desteklenmez. Örneğin, bir işlem yürüten bir WCF Hizmeti yöntemine sahip. Merhaba çağrısı bir işlem kapsamı içinde kapsayan başarısız olur olarak bir [System.ServiceModel.ProtocolException](https://msdn.microsoft.com/library/system.servicemodel.protocolexception).

## <a name="next-steps"></a>Sonraki adımlar
Sorular için lütfen hello üzerinde toous ulaşmak [SQL veritabanı Forumu](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) ve özellik istekleri için lütfen toohello eklemesini [SQL veritabanı geri bildirim Forumunda](https://feedback.azure.com/forums/217321-sql-database/).

<!--Image references-->
[1]: ./media/sql-database-elastic-transactions-overview/distributed-transactions.png



