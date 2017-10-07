---
title: "aaaSecure Azure SQL veritabanınızı | Microsoft Docs"
description: "Azure SQL veritabanınızı teknikler ve Özellikler toosecure hakkında bilgi edinin."
services: sql-database
documentationcenter: 
author: DRediske
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 06/28/2017
ms.author: daredis
ms.openlocfilehash: 1450d633d6f65faf1b8a2dc0dc7dfe996fb0719d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-your-azure-sql-database"></a>Azure SQL veritabanınızı güvenli

SQL veritabanı güvenlik duvarı kuralları, kullanıcıların tooprove kendi kimlik ve yetkilendirme toodata üyeliklerini rol tabanlı ve izinleri aracılığıyla yanı sıra aracılığıyla gerektiren kimlik doğrulama mekanizmaları kullanarak erişim tooyour veritabanı sınırlandırarak verilerinizi korur satır düzeyi güvenlik ve dinamik veri maskeleme.

Kötü amaçlı kullanıcılar ya da yalnızca birkaç basit adımla yetkisiz erişime karşı veritabanınızın hello koruma artırabilir. Bu öğreticide, öğrenin: 

> [!div class="checklist"]
> * Sunucunuzdaki hello Azure portal için sunucu düzeyinde güvenlik duvarı kuralları ayarlayın
> * SSMS kullanarak, veritabanı için veritabanı düzeyinde güvenlik duvarı kuralları ayarlayın
> * Güvenli bağlantı dizesi kullanarak tooyour veritabanına bağlanın
> * Kullanıcı erişimini yönetme
> * Şifreleme ile verilerinizi koruma
> * SQL veritabanı denetimi etkinleştir
> * SQL veritabanı tehdit algılama etkinleştir

Bir Azure aboneliğiniz yoksa [ücretsiz bir hesap oluşturma](https://azure.microsoft.com/free/) başlamadan önce.

## <a name="prerequisites"></a>Ön koşullar

toocomplete Bu öğretici, yapma emin aşağıdaki hello sahip:

- Yüklü hello en yeni sürümünü [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS). 
- Yüklü Microsoft Excel
- Bir Azure SQL server ve veritabanı - oluşturulan bkz [hello Azure portalında bir Azure SQL veritabanı oluşturma](sql-database-get-started-portal.md), [hello Azure CLI kullanarak tek bir Azure SQL veritabanı oluşturma](sql-database-get-started-cli.md), ve [tek bir Azure SQL oluşturma PowerShell kullanarak veritabanı](sql-database-get-started-powershell.md). 

## <a name="log-in-toohello-azure-portal"></a>Toohello Azure portalında oturum açın

İçinde toohello oturum [Azure portal](https://portal.azure.com/).

## <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a>Hello Azure portalında bir sunucu düzeyinde güvenlik duvarı kuralı oluşturma

SQL veritabanları Azure güvenlik duvarı tarafından korunur. Varsayılan olarak, diğer Azure hizmetleriyle bağlantılarından hariç tüm bağlantıları toohello sunucusu ve hello veritabanları hello Sunucusu'ndaki reddedilir. Daha fazla bilgi için bkz: [Azure SQL veritabanı sunucusu ve veritabanı düzeyi güvenlik duvarı kuralları](sql-database-firewall-configure.md).

Merhaba en güvenli tooset 'tooAzure Hizmetleri erişime izin ver' tooOFF yapılandırmadır. Bir Azure VM veya Bulut hizmeti tooconnect toohello veritabanından gerekiyorsa, oluşturmalısınız bir [ayrılmış IP](../virtual-network/virtual-networks-reserved-public-ip.md) ve yalnızca hello ayrılmış IP adresi erişim hello güvenlik duvarı aracılığıyla izin verin. 

Bu adımları toocreate izleyin bir [SQL veritabanı sunucu düzeyinde güvenlik duvarı kuralı](sql-database-firewall-configure.md) belirli bir IP adresi, sunucu tooallow bağlantıları için. 

> [!NOTE]
> Azure'da hello önceki öğreticiler veya quickstarts ve misiniz birini kullanarak bir örnek veritabanı oluşturduysanız hello olan bir bilgisayarda bu öğreticiyi gerçekleştirmeden aynı IP adresi, BT'nin sahip şekilde bu öğreticileri gitti aldığında sahip, bu adımı atlayabilirsiniz zaten bir sunucu düzeyinde güvenlik duvarı kuralı oluşturdu.
>

1. Tıklatın **SQL veritabanları** hello sol menüsüne ve ardından hello veritabanından tooconfigure hello güvenlik duvarı kuralı için başlangıç istediğiniz **SQL veritabanları** sayfa. Merhaba hello tam olarak gösteren, veritabanı açılır genel bakış sayfasında tam sunucu adını (gibi **mynewserver 20170313.database.windows.net**) ve diğer yapılandırmalar için seçenekler sağlar.

      ![sunucu güvenlik duvarı kuralı](./media/sql-database-security-tutorial/server-firewall-rule.png) 

2. Tıklatın **ayarlayın sunucu Güvenlik Duvarı** hello önceki görüntüde gösterildiği gibi hello araç. Merhaba **Güvenlik Duvarı ayarları** hello SQL veritabanı sunucusu sayfasını açar. 

3. Tıklatın **istemci IP'si Ekle** üzerinde hello araç tooadd hello genel IP adresi hello bilgisayar bağlı toohello portalıyla veya hello güvenlik duvarı kuralı el ile girin ve ardından **kaydetmek**.

      ![sunucu güvenlik duvarı kuralı ayarla](./media/sql-database-security-tutorial/server-firewall-rule-set.png) 

4. Tıklatın **Tamam** ve hello ardından **X** tooclose hello **Güvenlik Duvarı ayarları** sayfası.

Belirtilen hello ile Merhaba Server'daki tooany veritabanı artık bağlanabilir IP adresi veya IP adresi aralığı.

> [!NOTE]
> SQL Veritabanı 1433 numaralı bağlantı noktası üzerinden iletişim kurar. Bir şirket ağından gelen tooconnect çalışıyorsanız, bağlantı noktası 1433 üzerinden giden trafik, ağınızın güvenlik duvarı tarafından izin verilmiyor. Öyleyse, BT departmanınızın 1433 numaralı bağlantı noktasını açar sürece mümkün tooconnect tooyour Azure SQL veritabanı sunucusu olmaz.
>

## <a name="create-a-database-level-firewall-rule-using-ssms"></a>SSMS kullanarak bir veritabanı düzeyinde güvenlik duvarı kuralı oluşturma

Veritabanı düzeyinde güvenlik duvarı kuralları aynı mantıksal sunucu ve toocreate güvenlik duvarı kuralları, taşınabilir - takip etmeleri sırasında hello veritabanı anlamı hello içinde farklı veritabanları için toocreate farklı bir güvenlik duvarı ayarlarını etkinleştir bir [yük devretme ](sql-database-geo-replication-overview.md) hello SQL sunucusunda depolanıp depolanmadığı yerine. Merhaba ilk sunucu düzeyinde güvenlik duvarı kuralını yapılandırdıktan sonra veritabanı düzeyinde güvenlik duvarı kuralları yalnızca Transact-SQL deyimi kullanarak yapılandırılmış ve yalnızca olabilir. Daha fazla bilgi için bkz: [Azure SQL veritabanı sunucusu ve veritabanı düzeyi güvenlik duvarı kuralları](sql-database-firewall-configure.md).

Bu adımları toocreate bir veritabanı özel güvenlik duvarı kuralı izler.

1. Örneğin kullanarak tooyour veritabanı bağlantı [SQL Server Management Studio](./sql-database-connect-query-ssms.md).

2. Bir güvenlik duvarı için kural ve tıklatın tooadd istediğiniz hello veritabanında nesne Gezgini'nde sağ **yeni sorgu**. Boş sorgu penceresi bağlı tooyour veritabanını başka bir deyişle açar.

3. Merhaba sorgu penceresinde hello IP adresi tooyour ortak IP adresini değiştirmek ve sorgu aşağıdaki hello yürütün:

    ```sql
    EXECUTE sp_set_database_firewall_rule N'Example DB Rule','0.0.0.4','0.0.0.4';
    ```

4. Merhaba araç çubuğundan, **yürütme** toocreate hello güvenlik duvarı kuralı.

## <a name="view-how-tooconnect-an-application-tooyour-database-using-a-secure-connection-string"></a>Bir uygulama tooyour tooconnect nasıl veritabanı güvenli bağlantı dizesi kullanarak görüntüleme

tooensure bir istemci uygulaması ve SQL veritabanı arasında güvenli, şifreli bir bağlantı, hello bağlantı dizesi için yapılandırılmış toobe sahiptir:

- Şifreli bir bağlantı isteği ve
- toonot güven hello sunucu sertifikası. 

Bu Aktarım Katmanı Güvenliği (TLS) kullanarak bağlantı kurar ve man-in--middle saldırıları hello riskini azaltır. Doğru yapılandırılmış bağlantı dizeleri desteklenen istemci için SQL veritabanınızın sürücüleri hello Azure portal ' ADO.net için bu ekran görüntüsünde gösterildiği gibi alabilirsiniz.

1. Seçin **SQL veritabanları** hello sol taraftaki menüden veritabanınızda hello tıklatıp **SQL veritabanları** sayfası.

2. Merhaba üzerinde **genel bakış** sayfasında veritabanınız için **veritabanı bağlantı dizelerini Göster**.

3. Gözden geçirme hello tam **ADO.NET** bağlantı dizesi.

    ![ADO.NET bağlantı dizesi](./media/sql-database-security-tutorial/adonet-connection-string.png)

## <a name="creating-database-users"></a>Veritabanı kullanıcısı oluşturma

Herhangi bir kullanıcı oluşturmadan önce ilk Azure SQL veritabanı tarafından desteklenen iki kimlik doğrulama türleri birini seçmeniz gerekir: 

**SQL kimlik doğrulaması**kullanan kullanıcı adı ve parola oturumları için ve yalnızca, geçerli olan kullanıcılar bir mantıksal sunucu içinde belirli bir veritabanı bağlamında hello. 

**Azure Active Directory kimlik doğrulaması**, Azure Active Directory tarafından yönetilen kimlikleri kullanır. 

Toouse istiyorsanız [Azure Active Directory](./sql-database-aad-authentication.md) tooauthenticate SQL veritabanında doldurulan bir Azure Active Directory devam etmeden önce bulunmalıdır.

Bu adımları toocreate SQL kimlik doğrulaması kullanan bir kullanıcının izleyin:

1. Örneğin kullanarak tooyour veritabanı bağlantı [SQL Server Management Studio](./sql-database-connect-query-ssms.md) server yönetici kimlik bilgilerinizi kullanarak.

2. Nesne Gezgini'nde üzerinde üzerinde yeni bir kullanıcı tooadd istediğiniz hello veritabanını sağ tıklatın **yeni sorgu**. Boş sorgu penceresi, diğer bir deyişle bağlı toohello seçili veritabanı açılır.

3. Merhaba sorgu penceresinde, sorgu aşağıdaki hello girin:

    ```sql
    CREATE USER ApplicationUser WITH PASSWORD = 'YourStrongPassword1';
    ```

4. Merhaba araç çubuğundan, **yürütme** toocreate hello kullanıcı.

5. Varsayılan olarak, hello kullanıcı toohello veritabanı bağlanabilirsiniz, ancak izinleri tooread veya yazma veri yok. toogrant bu izinleri toohello yeni oluşturulan kullanıcı, aşağıdaki iki komutu yeni bir sorgu penceresinde hello yürütme

    ```sql
    ALTER ROLE db_datareader ADD MEMBER ApplicationUser;
    ALTER ROLE db_datawriter ADD MEMBER ApplicationUser;
    ```

Bu yönetici olmayan hesaplar hello veritabanı düzeyi tooconnect tooyour en yeni kullanıcılar oluşturma gibi tooexecute yönetici görevleri gerekmedikçe veritabanı en iyi yöntem toocreate olur. Lütfen hello gözden [Azure Active Directory öğretici](./sql-database-aad-authentication-configure.md) nasıl Azure Active Directory'yi kullanarak tooauthenticate.


## <a name="protect-your-data-with-encryption"></a>Şifreleme ile verilerinizi koruma

Azure SQL veritabanında saydam veri şifreleme (TDE) tüm değişiklikleri toohello uygulama hello şifrelenmiş veritabanı erişimi gerek kalmadan, rest, verileri otomatik olarak şifreler. Yeni oluşturulan veritabanları için TDE varsayılan olarak açıktır. tooenable TDE veritabanı veya TDE açıktır tooverify için şu adımları izleyin:

1. Seçin **SQL veritabanları** hello sol taraftaki menüden veritabanınızda hello tıklatıp **SQL veritabanları** sayfası. 

2. Tıklayın **saydam veri şifreleme** TDE için tooopen hello yapılandırma sayfası.

    ![Saydam Veri Şifrelemesi](./media/sql-database-security-tutorial/transparent-data-encryption-enabled.png)

3. Gerekirse, ayarlamak **veri şifreleme** tooON tıklatıp **kaydetmek**.

Merhaba arka planda Hello şifreleme işlemi başlatır. Bağlantı tooSQL veritabanını kullanarak hello ilerlemesini izleyebilirsiniz [SQL Server Management Studio](./sql-database-connect-query-ssms.md) hello hello encryption_state sütunu sorgulamak `sys.dm_database_encryption_keys` görünümü.

## <a name="enable-sql-database-auditing-if-necessary"></a>SQL veritabanı denetimi, gerekirse etkinleştirme

Azure SQL veritabanı denetimi veritabanı olaylarını izler ve bunları Azure depolama hesabınızdaki tooan denetim günlüğünü yazar. Denetim, yönetmeliklere uygunluğu korumanıza, veritabanı etkinliklerini anlamanıza ve ifade eden tutarsızlıklar ve olası güvenlik ihlallerini gösterebilir anormallikleri kavramanıza yardımcı olabilir. Bu adımları toocreate SQL veritabanınız için varsayılan bir denetim ilkesini izleyin:

1. Seçin **SQL veritabanları** hello sol taraftaki menüden veritabanınızda hello tıklatıp **SQL veritabanları** sayfası. 

2. Hello ayarları dikey penceresinde, seçin **denetim ve tehdit algılama**. Bildirim olduğunu ve sunucu düzeyi denetimi devre: bir **sunucu ayarlarını görüntüleyin** bağlantıyı tooview sağlar veya bu bağlamından hello sunucu denetim ayarlarını değiştirin.

    ![Denetim dikey penceresi](./media/sql-database-security-tutorial/auditing-get-started-settings.png)

3. Tooenable bir denetim türü (veya konum?) tercih ederseniz hello bir hello sunucu düzeyinde belirtilen farklı Aç **ON** denetleme ve hello seçin **Blob** denetim türü. Sunucu Blob denetimi etkinse hello yapılandırılmış veritabanı denetimi hello sunucu Blob denetim yan yana yer alır.

    ![Denetim Aç](./media/sql-database-security-tutorial/auditing-get-started-turn-on.png)

4. Seçin **depolama ayrıntıları** tooopen hello denetim günlüklerini depolama dikey. Burada günlükleri kaydedilecek select hello Azure depolama hesabı ve hello saklama dönemi, hangi hello sonra eski günlükleri silinecek, ardından **Tamam** hello altındaki. 

   > [!TIP]
   > Kullanım hello aynı depolama hesabı en hello denetimi dışında tüm denetlenen veritabanları tooget hello için raporları şablonları.
   > 

5. **Kaydet** düğmesine tıklayın.

> [!IMPORTANT]
> Toocustomize denetlenen hello olayları istiyorsanız, PowerShell veya REST API - bunu yapabilirsiniz hello bkz [Otomasyon (PowerShell / REST API)](sql-database-auditing.md#subheading-7) daha fazla ayrıntı için bölüm.
>

## <a name="enable-sql-database-threat-detection"></a>SQL veritabanı tehdit algılama etkinleştir

Tehdit algılama müşteriler toodetect sağlar ve güvenlik uyarıları anormal etkinlikler sağlayarak göründüklerinde toopotential tehditlerine yanıt güvenliği, yeni bir katman sağlar. Kullanıcılar bir girişim tooaccess, ihlali neden veya hello veritabanındaki verileri yararlanma SQL veritabanı denetimi toodetermine kullanarak hello şüpheli olayları gözden geçirebilirsiniz. Tehdit algılama basit tooaddress olası tehditler toohello veritabanı hello gerek toobe güvenlik Uzman olmadan kolaylaştırır veya sistemleri izleme Gelişmiş Güvenlik yönetin.
Örneğin, tehdit algılama olası SQL ekleme girişimlerini gösteren belirli anormal veritabanı etkinliklerini algılar. SQL ekleme hello ortak Web uygulaması güvenlik sorunlarını hello Internet, veri güdümlü kullanılan tooattack uygulamalar üzerinde biridir. Saldırganlar uygulama güvenlik açıkları tooinject kötü amaçlı SQL deyimlerini ihlal veya hello veritabanındaki verileri değiştirmek için uygulama giriş alanları içine yararlanın.

1. Merhaba toomonitor istediğiniz SQL veritabanını toohello yapılandırma dikey gidin. Hello ayarları dikey penceresinde, seçin **denetim ve tehdit algılama**.

    ![Gezinti Bölmesi](./media/sql-database-security-tutorial/auditing-get-started-settings.png)
2. Merhaba, **denetim ve tehdit algılama** yapılandırma dikey Aç **ON** denetleme, hangi görüntüler hello tehdit algılama ayarları.

3. Kapatma **ON** tehdit algılama.

4. Güvenlik Uyarıları anormal veritabanı etkinliklerini algılandığında alacak e-postaları Hello listesini yapılandırın.

5. Tıklatın **kaydetmek** hello içinde **denetim ve tehdit algılama** dikey toosave hello yeni veya güncelleştirilmiş denetim ve tehdit algılama ilkesi.

    ![Gezinti Bölmesi](./media/sql-database-security-tutorial/td-turn-on-threat-detection.png)

    Anormal veritabanı etkinliklerini algılanmazsa, anormal veritabanı etkinliklerini algılandığında bir e-posta bildirimi alırsınız. Merhaba e-posta hello şüpheli güvenlik olayı hello yapısını hello anormal etkinlikler, veritabanı adı, sunucu adını ve hello olay zaman dahil olmak üzere bilgileri sağlarız. Ayrıca, olası nedenler bilgileri sağlarız Eylemler tooinvestigate önerilen ve hello olası tehdit toohello veritabanı etkisini azaltır. Merhaba hangi toodo size gereken sonraki adımları ilerlemesi gibi e-posta alırsınız:

    ![Tehdit algılama e-posta](./media/sql-database-threat-detection-get-started/4_td_email.png)

6. Hello postada hello üzerinde tıklatın **Azure SQL denetim günlüğü** hello Azure portal'ı başlatın ve hello ilgili denetim kayıtları hello şüpheli olay hello sırada geçici Göster bağlantı.

    ![Denetim kaydı](./media/sql-database-threat-detection-get-started/5_td_audit_records.png)

7. SQL deyimi gibi hello veritabanı kuşkulu etkinlikleri hakkında daha fazla ayrıntı Hello denetim kayıtları tooview üzerinde tıklatın başarısızlık nedeni ve istemci IP.

    ![Kayıt ayrıntıları](./media/sql-database-security-tutorial/6_td_audit_record_details.png)

8. Merhaba denetimi kayıtları dikey penceresinde tıklayın **Excel'de Aç** tooopen önceden yapılandırılmış excel şablonu tooimport ve hello denetim günlüğü hello şüpheli olay hello sırada geçici çalışma daha derin çözümlenmesi.

    > [!NOTE]
    > Excel 2010 veya üzeri, Power Query ve hello **hızlı Birleştir** ayarı gereklidir.

    ![Kayıtları Excel'de Aç](./media/sql-database-threat-detection-get-started/7_td_audit_records_open_excel.png)

9. tooconfigure hello **hızlı Birleştir** ayarında - hello **POWER QUERY** Şerit sekmesi, select **seçenekleri** toodisplay hello Seçenekleri iletişim kutusu. Merhaba gizlilik bölümünü seçin ve 'Hello gizlilik düzeylerini yoksayın ve potansiyel performansı geliştirin' hello ikinci seçeneği - belirtin:

    ![Excel hızlı Birleştir](./media/sql-database-threat-detection-get-started/8_td_excel_fast_combine.png)

10. tooload SQL denetim günlüklerini hello parametreleri hello Ayarlar sekmesinde doğru ayarlandığından ve ardından hello 'Verileri' Şerit'i seçin ve hello 'Tümünü Yenile' düğmesini tıklatın emin olun.

    ![Excel parametreleri](./media/sql-database-threat-detection-get-started/9_td_excel_parameters.png)

11. Merhaba sonuçları görünen hello **SQL denetim günlüklerini** toorun daha derin algılanan ve uygulamanızda hello güvenlik olayı hello etkisini hello anormal etkinlikler analizini sağlayan sayfası.


## <a name="next-steps"></a>Sonraki adımlar
Kötü amaçlı kullanıcılar ya da yalnızca birkaç basit adımla yetkisiz erişime karşı veritabanınızın hello koruma artırabilir. Bu öğreticide, öğrenin: 

> [!div class="checklist"]
> * Sunucu ve veya veritabanı için güvenlik duvarı kuralları ayarlayın
> * Güvenli bağlantı dizesi kullanarak tooyour veritabanına bağlanın
> * Kullanıcı erişimini yönetme
> * Şifreleme ile verilerinizi koruma
> * SQL veritabanı denetimi etkinleştir
> * SQL veritabanı tehdit algılama etkinleştir

> [!div class="nextstepaction"]
>[SQL Veritabanı performansını iyileştirme](sql-database-performance-tutorial.md)

