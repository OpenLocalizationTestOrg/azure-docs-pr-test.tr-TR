---
title: "Azure SQL veritabanlarının aaaManage grupları | Microsoft Docs"
description: "Oluşturulması ve esnek bir iş yönetimi yol."
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: f858344d-085b-4022-935e-1b5fa20adbac
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: a73c4fb24c332fae0e917c18272724cccd56f29a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-scaled-out-azure-sql-databases-using-elastic-jobs-preview"></a>Oluşturma ve esnek işleri (Önizleme) kullanarak Azure SQL veritabanlarını ölçeklendirilmiş yönetme


**Esnek veritabanı iş** şema değişiklikleri, kimlik bilgileri yönetimi, başvuru veri güncelleştirmeleri, performans verileri toplama veya Kiracı (müşteri) telemetri koleksiyonu gibi yönetim işlemlerini yürüterek veritabanlarının gruplarının yönetimi kolaylaştırabilir. Esnek veritabanı iş hello Azure portal ve PowerShell cmdlet'leri aracılığıyla şu anda mevcut değil. Ancak, tüm veritabanları arasında tooexecution hello Azure portal yüzeyleri işlevsellik sınırlı bir [esnek havuz (Önizleme)](sql-database-elastic-pool.md). tooaccess ek özellikleri ve bir grubu özel tanımlı bir koleksiyon veya bir parça dahil olmak üzere veritabanları arasında betiklerinin yürütülmesi ayarlayın (kullanılarak oluşturulan [esnek veritabanı istemci Kitaplığı](sql-database-elastic-scale-introduction.md)), bkz: [oluşturma ve yönetme PowerShell kullanarak işleri](sql-database-elastic-jobs-powershell.md). İşleri hakkında daha fazla bilgi için bkz: [esnek veritabanı işleri genel bakış](sql-database-elastic-jobs-overview.md). 

## <a name="prerequisites"></a>Ön koşullar
* Azure aboneliği. Ücretsiz deneme için bkz: [ücretsiz deneme sürümü](https://azure.microsoft.com/pricing/free-trial/).
* Bir esnek havuz. Bkz: [esnek havuzları hakkında](sql-database-elastic-pool.md).
* Esnek veritabanı iş hizmet bileşenlerini yükleme. Bkz: [hello esnek veritabanı iş hizmetini yükleme](sql-database-elastic-jobs-service-installation.md).

## <a name="creating-jobs"></a>İşleri oluşturuluyor
1. Hello kullanarak [Azure portal](https://portal.azure.com), var olan bir esnek veritabanı iş havuzundan tıklatın **oluşturma işi**.
2. Hello kullanıcı adı ve parolayı (işleri yükleme sırasında oluşturulan) hello veritabanı yöneticisinin hello işleri denetim veritabanı (meta veri depolama alanı işleri için) yazın.
   
    ![Merhaba iş adı yazın veya kodda yapıştırın ve Çalıştır'ı tıklatın][1]
3. Merhaba, **işi oluştur** dikey penceresinde hello işi için bir ad yazın.
4. Merhaba kullanıcı adı ve parola tooconnect toohello hedef veritabanları komut dosyası yürütme toosucceed için yeterli izinlere sahip yazın.
5. Merhaba T-SQL komut dosyası yazın veya yapıştırın.
6. Tıklatın **kaydetmek** ve ardından **çalıştırmak**.
   
    ![İşleri oluşturma ve çalıştırma][5]

## <a name="run-idempotent-jobs"></a>Idempotent işleri çalıştırma
Bir veritabanları kümesi karşı bir komut çalıştırdığınızda, hello betik ıdempotent olduğundan emin olmanız gerekir. Diğer bir deyişle, onu önce tamamlanmamış bir durumda başarısız olmuş olsa bile hello betik birden çok kez mümkün toorun olmalıdır. Bir komut dosyası başarısız olduğunda, başarılı olana dek gibi hello iş otomatik olarak yeniden denenecek (sınırlarda hello yeniden deneme mantığı sonunda hello yeniden deneniyor olmaz). Merhaba yolu toodo bu toouse hello bir "IF var" yan tümcesi ve yeni bir nesne oluşturmadan önce bulunan örnek silin. Örneği burada gösterilir:

    IF EXISTS (SELECT name FROM sys.indexes
            WHERE name = N'IX_ProductVendor_VendorID')
    DROP INDEX IX_ProductVendor_VendorID ON Purchasing.ProductVendor;
    GO
    CREATE INDEX IX_ProductVendor_VendorID
    ON Purchasing.ProductVendor (VendorID);

Alternatif olarak, yeni bir örneğini oluşturmadan önce bir "IF değil var" yan tümcesi kullanın:

    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'TestTable')
    BEGIN
     CREATE TABLE TestTable(
      TestTableId INT PRIMARY KEY IDENTITY,
      InsertionTime DATETIME2
     );
    END
    GO

    INSERT INTO TestTable(InsertionTime) VALUES (sysutcdatetime());
    GO

Bu komut dosyası ardından daha önce oluşturduğunuz hello tablosunu güncelleştirir.

    IF NOT EXISTS (SELECT columns.name FROM sys.columns INNER JOIN sys.tables on columns.object_id = tables.object_id WHERE tables.name = 'TestTable' AND columns.name = 'AdditionalInformation')
    BEGIN

    ALTER TABLE TestTable

    ADD AdditionalInformation NVARCHAR(400);
    END
    GO

    INSERT INTO TestTable(InsertionTime, AdditionalInformation) VALUES (sysutcdatetime(), 'test');
    GO


## <a name="checking-job-status"></a>İş durumunu denetleme
Bir işi başladıktan sonra üzerinde ilerleme durumunu denetleyebilirsiniz.

1. Merhaba esnek havuz sayfasından tıklatın **yönetmek işleri**.
   
    !["Yönet projeler"'i tıklatın][2]
2. Merhaba adına bir işin (a) tıklayın. Merhaba **durum** "Tamamlandı" veya "Başarısız" olabilir Merhaba işin ayrıntılarına (b), tarih ve saati oluşturma ve çalıştırma görünür. Tarih ve saat ayrıntılarını vermiş hello havuzundaki her veritabanında hello betik hello ilerlemesini gösterir hello aşağıda Hello listesi (c).
   
    ![Tamamlanmış iş denetleniyor][3]

## <a name="checking-failed-jobs"></a>İşlerini denetimi başarısız oldu
Bir işi başarısız olursa, yürütme günlüğü bulunabilir. Ayrıntılarını hello başarısız işi toosee Hello adına tıklayın.

![Başarısız işi denetleyin][4]

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-create-and-manage/screen-1.png
[2]: ./media/sql-database-elastic-jobs-create-and-manage/click-manage-jobs.png
[3]: ./media/sql-database-elastic-jobs-create-and-manage/running-jobs.png
[4]: ./media/sql-database-elastic-jobs-create-and-manage/failed.png
[5]: ./media/sql-database-elastic-jobs-create-and-manage/screen-2.png


