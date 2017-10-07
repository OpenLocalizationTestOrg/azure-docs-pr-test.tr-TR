---
title: "aaaManage kişisel verileri Microsoft Azure | Microsoft Docs"
description: "yönergeler nasıl toocorrect, güncelleştirme, silme ve Azure Active Directory ve Azure SQL veritabanı kişisel verileri dışarı aktarma"
services: security
documentationcenter: na
author: barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: barclayn
ms.openlocfilehash: 032f70d32377cb9395cb2c35c27dad05001537c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-personal-data-in-microsoft-azure"></a>Microsoft Azure kişisel verileri yönetmek

Bu makalede nasıl toocorrect, güncelleştirme, silme ve Azure Active Directory ve Azure SQL veritabanı kişisel verileri dışarı aktarma yönergeleri sağlar.

## <a name="scenario"></a>Senaryo

Üst uç hedef Düğünler İrlanda ve hem de bir yerel ve uluslararası müşteri tabanı için Merhaba Dünya için tek adrestir alışveriş Dublin tabanlı şirket sağlar. Ofisleri, müşteriler, çalışanların ve satıcıların bunlar sunar hello world toofully hizmet hello görebildikleri bulunan sahiptirler.

Diğer birçok öğeler arasında hello şirket yemek Alerjiler ve dietary Tercihler dahil LCV'ler izler. Evlilik konuklar arabası, horseback gözatan, bot gibi üstündeçalýþan, vb. için çeşitli etkinlikleri kaydetmek ve hatta birbiriyle merkezi bir web sayfasında toohello olay baştaki hello ay sırasında etkileşim. Merhaba şirket, çalışanlar, satıcılar, müşteriler ve Evlilik konuklar kişisel bilgileri toplar. Hello nedeniyle hello iş hello şirket uluslararası yapısını düzenleme birden çok düzeyi ile uyumlu olmalıdır.

## <a name="problem-statement"></a>Sorun bildirimi

- Veri admins mümkün toocorrect yanlış kişisel bilgi ve güncelleştirme eksik ya da değişen kişisel bilgileri olması gerekir.

- Veri admins gerek mümkün toodelete bir veri konunun hello istek üzerine kişisel bilgileri olması gerekir.

- Veri admins tooexport verilere ihtiyaç ve tooa veri konu bilgilendirilmesine istek üzerine ortak, yapılandırılmış bir biçimde sağlayın.

## <a name="company-goals"></a>Şirketin hedeflerine

- Yanlış veya tamamlanmamış müşteri, Evlilik konuk, çalışan ve satıcı kişisel bilgileri düzeltildi veya gerekir Azure Active Directory ve Azure SQL veritabanı güncelleştirildi.

- Kişisel bilgiler Azure Active Directory ve Azure SQL veritabanı veri konu hello istek üzerine silinmesi gerekir.

- Kişisel veriler ortak, yapılandırılmış bir biçimde bir veri konunun hello istek üzerine aktarılması gerekir.

## <a name="solutions"></a>Çözümler

### <a name="azure-active-directory-rectifycorrect-inaccurate-or-incomplete-personal-data-and-erasedelete-personal-datauser-profiles"></a>Azure Active Directory: yanlış veya tamamlanmamış kişisel verileri düzeltmek/düzeltin ve silme/kişisel veri/kullanıcı profillerini Sil

[Azure Active Directory](https://azure.microsoft.com/services/active-directory/) Microsoft'un bulut tabanlı, çok kiracılı dizin ve kimlik yönetimi hizmetidir.
Düzeltin, güncelleştirmek veya müşteri ve çalışan kullanıcı profilleri ve bir kullanıcının adını, iş başlığı, adresi veya telefon numarası gibi kişisel verileri içerdiğini kullanıcı iş bilgilerini silmek, [Azure Active Directory](https://azure.microsoft.com/services/active-directory/) (AAD) hello kullanarak ortam [Azure portal](https://portal.azure.com/).

Merhaba dizin için genel yönetici olan bir hesapla oturum gerekir.

#### <a name="how-do-i-correct-or-update-user-profile-and-work-information-in-azure-active-directory"></a>Nasıl düzeltin veya kullanıcı profili ve iş güncelleştirme bilgileri Azure Active Directory'de?

1. İçinde toohello oturum [Azure portal](https://portal.azure.com) hello dizin için genel yönetici olan bir hesapla.

2. Seçin **daha fazla hizmet**, girin **kullanıcılar ve gruplar** hello metin kutusuna ve ardından **Enter**.

    ![Medya/image1.png](media/manage-personal-data-azure/image001.png)

3. Merhaba üzerinde **kullanıcılar ve gruplar** dikey penceresinde, select **kullanıcılar**.

    ![Medya/image2.png](media/manage-personal-data-azure/image003.png)

4. Merhaba üzerinde **kullanıcılar ve gruplar - kullanıcıların** dikey penceresinde hello listeden bir kullanıcı seçin ve sonra hello dikey penceresinde hello seçilen kullanıcı,'i seçin **profil** düzeltildi toobe gereken tooview hello kullanıcı profili bilgileri veya güncelleştirilmiş.

    ![Medya/image3.png](media/manage-personal-data-azure/image005.png)

5. Düzeltin veya güncelleştirme hello bilgileri ve hello komut çubuğunda, ardından **kaydedin.**

6.  Merhaba dikey penceresinde hello seçilen kullanıcı, seçin **iş bilgisi** toobe gereken tooview kullanıcı iş bilgilerini düzeltildi veya güncelleştirilir.

    ![Medya/image4.png](media/manage-personal-data-azure/image007.png)

7. Düzeltin veya hello kullanıcı iş bilgilerini güncelleştirmek ve hello komut çubuğunda, ardından **kaydedin.**

#### <a name="how-do-i-delete-a-user-profile-in-azure-active-directory"></a>Azure Active Directory'de bir kullanıcı profili nasıl silebilirim?

1. İçinde toohello oturum [Azure portal](https://portal.azure.com) hello dizin için genel yönetici olan bir hesapla.

2. Seçin **daha fazla hizmet**, girin **kullanıcılar ve gruplar** hello metin kutusuna ve ardından **Enter**.

    ![](media/manage-personal-data-azure/image001.png)

3. Merhaba üzerinde **kullanıcılar ve gruplar** dikey penceresinde, select **kullanıcılar**.

    ![Medya/image2.png](media/manage-personal-data-azure/image003.png)

4. Merhaba üzerinde **kullanıcılar ve gruplar - kullanıcıların** dikey penceresinde, kullanıcı hello listeden seçin.

    ![Medya/image3.png](media/manage-personal-data-azure/image007.png)

5. Merhaba dikey penceresinde hello seçilen kullanıcı, seçin **genel bakış**ve hello komut çubuğunda, ardından **silmek**.

    ![](media/manage-personal-data-azure/image013.png)

### <a name="sql-database-rectifycorrect-inaccurate-or-incomplete-personal-data-erasedelete-personal-data-export-personal-data"></a>SQL veritabanı: düzeltin ve düzeltmek yanlış veya tamamlanmamış kişisel veri; Kişisel verileri silme veya silme; Kişisel verileri dışarı aktarma 

[Azure SQL veritabanı](https://azure.microsoft.com/services/sql-database/?v=16.50) yapı ve uygulamalarını geliştiriciler yardımcı olan bir bulut veritabanıdır.

Kişisel veriler güncelleştirilebilir [Azure SQL veritabanı](https://azure.microsoft.com/services/sql-database/?v=16.50) standart SQL sorguları kullanılarak da silinebilir. Ayrıca, kişisel verileri çeşitli hello Azure SQL Server içeri ve Dışarı Aktarma Sihirbazı'nı dahil olmak üzere yöntemleri ve biçimleri, bir BACPAC dosyası dahil olmak üzere çeşitli kullanarak SQL veritabanından dışa aktarılabilir.

#### <a name="how-do-i-correct-update-or-erase-personal-data-in-sql-database"></a>Nasıl düzeltin, güncelleştirme veya SQL veritabanında kişisel verileri silme?

toolearn nasıl toocorrect veya güncelleştirme kişisel verileri SQL veritabanında ziyaret hello [güncelleştirme (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/queries/update-transact-sql), [güncelleştirme metin](https://docs.microsoft.com/sql/t-sql/queries/updatetext-transact-sql), [güncelleştirme ile ortak tablo ifadesinin](https://docs.microsoft.com/sql/t-sql/queries/with-common-table-expression-transact-sql), veya [ Metni Yaz güncelleştirme](https://docs.microsoft.com/sql/t-sql/queries/writetext-transact-sql) belgeleri.

toolearn nasıl toodelete kişisel veriler SQL veritabanında ziyaret hello [(Transact-SQL) Delete](https://docs.microsoft.com/sql/t-sql/statements/delete-transact-sql) belgeleri.

#### <a name="how-do-i-export-personal-data-tooa-bacpac-file-in-sql-database"></a>Kişisel veri tooa BACPAC SQL veritabanı dosyasında nasıl dışarı?

Bir BACPAC dosya hello SQL veritabanı veri ve meta verileri içerir ve bir BACPAC uzantılı bir zip dosyası. Bu yapılabilir hello kullanarak [Azure portal](https://portal.azure.com/), SQLPackage komut satırı yardımcı programı, SQL Server Management Studio (SSMS) veya PowerShell hello.

toolearn nasıl tooexport veri tooa BACPAC dosyası, ziyaret hello [bir Azure SQL veritabanı tooa BACPAC dosyasını dışarı](https://docs.microsoft.com/azure/sql-database/sql-database-export) sayfasında, yukarıda listelenen her bir yöntemin ayrıntılı yönergeler içerir.

Kişisel veriler nasıl SQL veritabanıyla hello SQL Server içeri ve Dışarı Aktarma Sihirbazı verme?

Bu sihirbaz bir kaynak tooa hedef veri kopyalamanıza yardımcı olur. Bir giriş toohello Sihirbazı için nasıl tooget, izinleri bilgiler ve nasıl tooget yardımcı hello aracıyla ziyaret dahil olmak üzere hello [içeri aktarma ve dışarı aktarma veri ile Merhaba SQL Server içeri ve Dışarı Aktarma Sihirbazı](https://docs.microsoft.com/sql/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard) web sayfası.

Merhaba hello Sihirbazı için adımlara genel bakış için ziyaret [hello SQL Server içeri ve Dışarı Aktarma Sihirbazı'ndaki adımları](https://docs.microsoft.com/sql/integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard) web sayfası.

## <a name="next-steps"></a>Sonraki Adımlar:

[Azure SQL Veritabanı](https://azure.microsoft.com/services/sql-database/?v=16.50) 

[Azure Active Directory](https://azure.microsoft.com/services/active-directory/)

