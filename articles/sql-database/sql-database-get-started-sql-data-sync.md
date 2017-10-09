---
title: "aaaGetting başlatılan Azure SQL veri eşitleme (Önizleme) | Microsoft Docs"
description: "Bu öğreticide Azure SQL veri eşitleme (Önizleme) ile çalışmaya başlamanıza yardımcı olur."
services: sql-database
documentationcenter: 
author: douglaslms
manager: craigg
editor: 
ms.assetid: a295a768-7ff2-4a86-a253-0090281c8efa
ms.service: sql-database
ms.custom: load & move data
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: douglasl
ms.openlocfilehash: 666d09237e42acc23ae3c8c81e60734a413f5949
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-sql-data-sync-preview"></a>Azure SQL veri eşitleme (Önizleme) ile çalışmaya başlama
Bu öğreticide, bir karma eşitleme grubu oluşturarak Azure SQL veri eşitleme tooset Azure SQL Database ve SQL Server örneklerini içeren öğrenin. Merhaba yeni eşitleme grubu tam olarak yapılandırılmamış ve ayarladığınız hello zamanlamada eşitler.

Bu öğretici, SQL Database ve SQL Server ile en az bazı konusunda deneyim sahibi olduğunuzu varsayar. 

SQL veri eşitleme genel bakış için bkz: [verilerini](sql-database-sync-data.md).

Göster tam PowerShell örnekleri için nasıl tooconfigure SQL veri eşitleme makaleleri aşağıdaki hello bakın:
-   [Birden çok Azure SQL veritabanı arasında PowerShell toosync kullanın](scripts/sql-database-sync-data-between-sql-databases.md)
-   [Bir Azure SQL Database ve SQL Server içi veritabanı arasında PowerShell toosync kullanın](scripts/sql-database-sync-data-between-azure-onprem.md)

> [!NOTE]
> Merhaba tam teknik belgeler önceden, MSDN'de bulunan Azure SQL veri eşitleme için ayarlanmış olarak kullanılabilir bir. PDF belgesini. Karşıdan [burada](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true).

## <a name="step-1---create-sync-group"></a>1. adım - eşitleme grubu oluşturma

### <a name="locate-hello-data-sync-settings"></a>Merhaba veri eşitleme ayarlarını bulun

1.  Tarayıcınızda, toohello Azure portalına gidin.

2.  Merhaba Portalı'nda, SQL veritabanlarınızın panonuz veya hello SQL veritabanları simgesi hello araç çubuğunda bulun.

    ![Azure SQL veritabanı listesi](media/sql-database-get-started-sql-data-sync/datasync-preview-sqldbs.png)

3.  Merhaba üzerinde **SQL veritabanları** dikey penceresinde, select hello hello hub veritabanı için veri eşitleme hello SQL veritabanı dikey penceresini açar gibi toouse istediğiniz var olan SQL veritabanı.

4.  Merhaba SQL veritabanı dikey penceresinde hello seçili veritabanı, seçin **eşitleme tooother veritabanları**. Merhaba veri eşitleme dikey pencere açılır.

    ![Eşitleme tooother veritabanları seçeneği](media/sql-database-get-started-sql-data-sync/datasync-preview-newsyncgroup.png)

### <a name="create-a-new-sync-group"></a>Yeni bir eşitleme grubu oluşturun

1.  Merhaba veri eşitleme dikey penceresinde, seçin **yeni eşitleme grubu**. Merhaba **yeni eşitleme grubu** dikey pencere açılır adım 1 ile **eşitleme Grup Oluştur**, vurgulanan. Merhaba **veri eşitleme grubu oluşturma** dikey penceresi de açılır.

2.  Merhaba üzerinde **veri eşitleme grubu oluşturma** dikey penceresinde, öğeleri hello:

    1.  Merhaba, **eşitleme grubu adı** alanında, hello yeni eşitleme grubu için bir ad girin.

    2.  Merhaba, **eşitleme meta veri veritabanı** bölümünde, toocreate (önerilen) yeni bir veritabanı veya toouse var olan veritabanı olup olmadığını seçin.

        > [!NOTE]
        > Microsoft, eşitleme meta veri veritabanı hello gibi bir yeni, boş bir veritabanı toouse oluşturduğunuz önerir. Veri Eşitleme bu veritabanında tablolar oluşturur ve sık kullanılan bir iş yükü çalıştırır. Bu veritabanı, otomatik olarak hello tüm eşitleme gruplarınızı hello seçili bölgede için eşitleme meta veri veritabanı olarak paylaşılır. Bırakma olmadan hello eşitleme meta veri veritabanı, adını ya da kendi hizmet düzeyi değiştiremezsiniz.

        Seçerseniz **yeni veritabanı**seçin **yeni veritabanı oluştur.** Merhaba **SQL veritabanı** dikey pencere açılır. Merhaba üzerinde **SQL veritabanı** dikey penceresinde, adı ve hello yeni veritabanını yapılandırın. Ardından **Tamam**.

        Seçerseniz **varolan veritabanını kullan**seçin hello veritabanından hello listesi.

    3.  Merhaba, **otomatik eşitleme** bölümünde, ilk seçin **üzerinde** veya **devre dışı**.

        Seçerseniz **üzerinde**, hello içinde **eşitleme sıklığı** bölümünde, bir sayı girin ve saniye, dakika, saat veya gün seçin.

        ![Eşitleme sıklığı belirtin](media/sql-database-get-started-sql-data-sync/datasync-preview-syncfreq.png)

    4.  Merhaba, **çakışma çözümü** bölümünde, "Hub wins" veya "Üye WINS." seçin

        ![Çakışmalar nasıl çözümlenir belirtin](media/sql-database-get-started-sql-data-sync/datasync-preview-conflictres.png)

    5.  Seçin **Tamam** ve oluşturulan ve dağıtılan hello yeni eşitleme grubu toobe için bekleyin.

## <a name="step-2---add-sync-members"></a>2. adım - eşitleme üyeleri Ekle

Hello yeni eşitleme grubu oluşturup, adım 2 ' yi dağıttıktan sonra **eşitleme üye eklemek**, hello vurgulanmış **yeni eşitleme grubu** dikey.

Merhaba, **Hub veritabanı** bölümünde, için hello SQL veritabanı sunucusu hangi hello hub veritabanı bulunduğu hello varolan kimlik bilgilerini girin. Girmeyin *yeni* Bu bölümde kimlik bilgileri.

![Hub veritabanı toosync Grup eklendi](media/sql-database-get-started-sql-data-sync/datasync-preview-hubadded.png)

## <a name="add-an-azure-sql-database"></a>Bir Azure SQL veritabanı Ekle

Merhaba, **üye veritabanı** bölümünde, isteğe bağlı olarak bir Azure SQL veritabanı toohello eşitleme grubu seçerek eklemek **Azure veritabanı Ekle**. Merhaba **Azure veritabanını yapılandırma** dikey pencere açılır.

Merhaba üzerinde **Azure veritabanını yapılandırma** dikey penceresinde, öğeleri hello:

1.  Merhaba, **eşitleme üye adı** alanında, hello yeni eşitleme üyesi için bir ad sağlayın. Bu ad hello veritabanının kendisi hello adından farklıdır.

2.  Merhaba, **abonelik** alanında, select hello ilişkili faturalandırma için Azure aboneliği.

3.  Merhaba, **Azure SQL Server** alanında, select hello varolan SQL veritabanı sunucusu.

4.  Merhaba, **Azure SQL veritabanı** alanında, select hello varolan bir SQL veritabanının.

5.  Merhaba, **eşitleme yönergeleri** alanında, çift yönlü eşitleme, toohello Hub'ı seçin veya hello Hub.

    ![Yeni bir SQL veritabanı eşitleme üye ekleme](media/sql-database-get-started-sql-data-sync/datasync-preview-memberadding.png)

6.  Merhaba, **kullanıcıadı** ve **parola** alanlar için hello SQL veritabanı sunucusu hangi hello üye veritabanı bulunduğu hello varolan kimlik bilgilerini girin. Girmeyin *yeni* Bu bölümde kimlik bilgileri.

7.  Seçin **Tamam** ve oluşturulan ve dağıtılan hello yeni eşitleme üye toobe için bekleyin.

    ![Yeni SQL veritabanı eşitleme üye eklendi](media/sql-database-get-started-sql-data-sync/datasync-preview-memberadded.png)

## <a name="add-an-on-premises-sql-server-database"></a>Bir şirket içi SQL Server veritabanı ekleyin

Merhaba, **üye veritabanı** bölümünde, isteğe bağlı olarak bir şirket içi SQL Server toohello eşitleme grubu seçerek eklemek **bir şirket içi veritabanı Ekle**. Merhaba **yapılandırma şirket içi** dikey pencere açılır.

Merhaba üzerinde **yapılandırma şirket içi** dikey penceresinde, öğeleri hello:

1.  Seçin **Seç hello eşitleme Aracısı ağ geçidi**. Merhaba **seçin eşitleme Aracısı** dikey pencere açılır.

    ![Merhaba eşitleme Aracısı ağ geçidi seçin](media/sql-database-get-started-sql-data-sync/datasync-preview-choosegateway.png)

2.  Merhaba üzerinde **Seç hello eşitleme Aracısı ağ geçidi** dikey penceresinde, seçin olup olmadığını toouse var olan bir aracıyı veya yeni bir aracı oluşturun.

    Seçerseniz **varolan aracıları**, hello hello listeden var olan aracıyı seçin.

    Seçerseniz **yeni bir aracı oluşturma**, öğeleri hello:

    1.  Sağlanan hello bağlantısından Hello istemci eşitleme Aracısı yazılımını indirin ve hello SQL Server bulunduğu hello bilgisayara yükleyin.
 
        > [!IMPORTANT]
        > Merhaba sunucusuyla iletişim tooopen giden TCP bağlantı noktası 1433 hello güvenlik duvarı toolet hello istemci aracısında var.


    2.  Merhaba aracısı için bir ad girin.

    3.  Seçin **oluşturun ve anahtarı oluşturmak**.

    4.  Merhaba Aracısı anahtar toohello panoya kopyalayın.
        
        ![Yeni bir eşitleme aracı oluşturma](media/sql-database-get-started-sql-data-sync/datasync-preview-selectsyncagent.png)

    5.  Seçin **Tamam** tooclose hello **seçin eşitleme Aracısı** dikey.

    6.  Merhaba SQL Server bilgisayarında, bulun ve hello istemci eşitleme Aracısı uygulamayı çalıştırın.

        ![İstemci Aracısı uygulama Hello veri eşitleme](media/sql-database-get-started-sql-data-sync/datasync-preview-clientagent.png)

    7.  Merhaba eşitleme Aracısı uygulamada seçin **aracı anahtarını Gönder**. Merhaba **eşitleme meta veri veritabanı yapılandırması** iletişim kutusu açılır.

    8.  Merhaba, **eşitleme meta veri veritabanı yapılandırması** iletişim kutusu, Azure portal hello kopyalanan hello aracı anahtarını yapıştırın. Ayrıca hello hello Azure SQL veritabanı sunucusu hangi hello meta veri veritabanının bulunduğu için var olan kimlik bilgilerini sağlayın. (Yeni bir meta veri veritabanı oluşturduysanız, bu üzerinde hello veritabanıdır hello hub veritabanı aynı sunucuya.) Seçin **Tamam** ve hello yapılandırma toofinish için bekleyin.

        ![Merhaba aracı anahtarını ve sunucu kimlik bilgilerini girin](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-enterkey.png)

        >   [!NOTE] 
        >   Bu noktada bir güvenlik duvarı hatası alırsanız, toocreate bir güvenlik duvarı kuralı hello SQL Server bilgisayardan gelen trafiği Azure tooallow sahip. Merhaba kural hello Portalı'nda el ile oluşturabilirsiniz, ancak daha kolay toocreate bulabilirsiniz, SQL Server Management Studio (SSMS). SSMS, Azure üzerinde tooconnect toohello hub veritabanı deneyin. Adı olarak girin \<hub_database_name\>. database.windows.net. Merhaba iletişim kutusu tooconfigure hello Azure güvenlik duvarı kuralı Hello adımları izleyin. Ardından toohello istemci eşitleme Aracısı uygulamaya dönün.

    9.  Merhaba istemci eşitleme Aracısı uygulamanın tıklayın **kaydetmek** tooregister hello Aracısı ile bir SQL Server veritabanı. Merhaba **SQL Server yapılandırma** iletişim kutusu açılır.

        ![Ekleme ve bir SQL Server veritabanı yapılandırma](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-adddb.png)

    10. Merhaba, **SQL Server yapılandırma** iletişim kutusunda, seçin olup olmadığını tooconnect SQL Server kimlik doğrulaması veya Windows kimlik doğrulaması kullanarak. SQL Server kimlik doğrulamasını seçerseniz, hello varolan kimlik bilgilerini girin. Merhaba SQL Server adı ve hello hello veritabanının adını toosync istediğinizi belirtin. Seçin **Bağlantıyı Sına** tootest ayarlarınızı. Ardından **kaydetmek**. Merhaba kayıtlı veritabanı hello listesinde görüntülenir.

        ![SQL Server veritabanı artık kayıtlı](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-dbadded.png)

    11. Merhaba istemci eşitleme Aracısı uygulama artık kapatabilirsiniz.

    12. Hello portalında, hello **yapılandırma şirket içi** dikey penceresinde, select **hello veritabanı seçin.** Merhaba **Veritabanı Seç** dikey pencere açılır.

    13. Merhaba üzerinde **Veritabanı Seç** dikey penceresinde hello **eşitleme üye adı** alanında, hello yeni eşitleme üyesi için bir ad sağlayın. Bu ad hello veritabanının kendisi hello adından farklıdır. Merhaba veritabanı hello listeden seçin. Merhaba, **eşitleme yönergeleri** alanında, çift yönlü eşitleme, toohello Hub'ı seçin veya hello Hub.

        ![Şirket içi veritabanında Hello seçin](media/sql-database-get-started-sql-data-sync/datasync-preview-selectdb.png)

    14. Seçin **Tamam** tooclose hello **Veritabanı Seç** dikey. Ardından **Tamam** tooclose hello **yapılandırma şirket içi** dikey ve hello bekle yeni oluşturulan ve dağıtılan üye toobe eşitleme. Son olarak, tıklatın **Tamam** tooclose hello **eşitleme üyeleri seçin** dikey.

        ![Şirket içi veritabanında toosync Grup eklendi](media/sql-database-get-started-sql-data-sync/datasync-preview-onpremadded.png)

3.  tooconnect tooSQL veri eşitleme ve hello yerel aracı, ekleme, kullanıcı adı toohello rolünüz `DataSync_Executor`. Veri Eşitleme hello SQL Server örneğinde bu rol oluşturur.

## <a name="step-3---configure-sync-group"></a>3. adım - eşitleme grubunu yapılandırma

Merhaba yeni eşitleme grubu üyeleri oluşturulan ve dağıtılan, adım 3, sonra **yapılandırma eşitleme grubu**, hello vurgulanmış **yeni eşitleme grubu** dikey.

1.  Merhaba üzerinde **tabloları** eşitleme hello listesinden bir veritabanı grubu üyeleri ve ardından dikey penceresinde, select **yenileme şema**.

2.  Kullanılabilir tabloların Hello listeden toosync istediğiniz hello tabloları seçin.

    ![Tablolar toosync seçin](media/sql-database-get-started-sql-data-sync/datasync-preview-tables.png)

3.  Varsayılan olarak, hello tablodaki tüm sütunları seçilir. Tüm hello sütunları toosync istemiyorsanız, toosync istemediğiniz hello sütunları hello onay kutusunu devre dışı bırakın. Tooleave hello birincil anahtar sütunu seçili olduğundan emin olun.

    ![Alanları toosync seçin](media/sql-database-get-started-sql-data-sync/datasync-preview-tables2.png)

4.  Son olarak, seçin **kaydetmek**.

## <a name="next-steps"></a>Sonraki adımlar
Tebrikler. Bir SQL veritabanı örneğini ve SQL Server veritabanı içeren bir eşitleme grubu oluşturdunuz.

SQL Database ve SQL veri eşitleme hakkında daha fazla bilgi için bkz:

-   [Merhaba tam SQL veri eşitleme teknik belgeler indirin](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true)
-   [Merhaba SQL veri eşitleme REST API belgelerini indirebilirsiniz](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_REST_API.pdf?raw=true)
-   [SQL veritabanı genel bakış](sql-database-technical-overview.md)
-   [Veritabanı yaşam döngüsü yönetimi](https://msdn.microsoft.com/library/jj907294.aspx)
