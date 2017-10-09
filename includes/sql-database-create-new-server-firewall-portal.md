
<!--
includes/sql-database-create-new-server-firewall-portal.md

Latest Freshness check:  2016-11-28 , rickbyh.

As of circa 2016-04-11, hello following topics might include this include:
articles/sql-database/sql-database-get-started.md
articles/sql-database/sql-database-configure-firewall-settings
articles/sql-data-warehouse-get-started-provision.md

-->
### <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a>Hello Azure portalında bir sunucu düzeyinde güvenlik duvarı kuralı oluşturma

1. Ayarlar altında hello SQL server dikey tıklayın **Güvenlik Duvarı** tooopen hello güvenlik duvarı dikey hello SQL server için.

    <!-- ![sql server firewall](../articles/sql-database/media/sql-database-get-started/sql-server-firewall.png) -->

2. Görüntülenen hello istemci IP adresi gözden geçirin ve bu IP adresinizin hello tercih ettiğiniz bir tarayıcı kullanarak Internet üzerinde olduğunu doğrulayın ("nedir IP adresimi isteyin). IP adresleri bazen çeşitli nedenlerle eşleşmez.

    <!-- ![your IP address](../articles/sql-database/media/sql-database-get-started/your-ip-address.png) -->

3. Merhaba IP adreslerinin eşleşmesi varsayılarak tıklatın **istemci IP'si Ekle** hello araç.

    ![istemci IP’si ekle](../articles/sql-data-warehouse/media/sql-data-warehouse-get-started-provision/add-client-ip.png)

    > [!NOTE]
    > Merhaba SQL veritabanı Güvenlik Duvarı'nı hello sunucu tooa tek IP adresi veya adresleri aralığının tamamını açabilirsiniz. Ve kullanıcıların toologin tooany veritabanında açılırken hello güvenlik duvarı sağlar SQL yöneticiler sunucu toowhich geçerli kimlik bilgilerine sahip oldukları hello.
    >

4. Tıklatın **kaydetmek** üzerinde bu sunucu düzeyinde güvenlik duvarı kuralı araç toosave hello ve ardından **Tamam**.

    ![istemci IP’si ekle](../articles/sql-database/media/sql-database-get-started-portal/server-firewall-rule.png)

> [!Tip]
> Öğretici için bkz. [SQL Veritabanı öğreticisi: Sunucu, sunucu düzeyinde güvenlik duvarı kuralı, örnek veritabanı, veritabanı düzeyinde güvenlik duvarı oluşturma ve SQL Server’a bağlanma](../articles/sql-database/sql-database-get-started.md).    
>
