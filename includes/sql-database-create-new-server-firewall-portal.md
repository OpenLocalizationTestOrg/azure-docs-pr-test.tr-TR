
<!--
includes/sql-database-create-new-server-firewall-portal.md

Latest Freshness check:  2016-11-28 , rickbyh.

As of circa 2016-04-11, hello following topics might include this include:
articles/sql-database/sql-database-get-started.md
articles/sql-database/sql-database-configure-firewall-settings
articles/sql-data-warehouse-get-started-provision.md

-->
### <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a><span data-ttu-id="f47ef-101">Hello Azure portalında bir sunucu düzeyinde güvenlik duvarı kuralı oluşturma</span><span class="sxs-lookup"><span data-stu-id="f47ef-101">Create a server-level firewall rule in hello Azure portal</span></span>

1. <span data-ttu-id="f47ef-102">Ayarlar altında hello SQL server dikey tıklayın **Güvenlik Duvarı** tooopen hello güvenlik duvarı dikey hello SQL server için.</span><span class="sxs-lookup"><span data-stu-id="f47ef-102">On hello SQL server blade, under Settings, click **Firewall** tooopen hello Firewall blade for hello SQL server.</span></span>

    <!-- ![sql server firewall](../articles/sql-database/media/sql-database-get-started/sql-server-firewall.png) -->

2. <span data-ttu-id="f47ef-103">Görüntülenen hello istemci IP adresi gözden geçirin ve bu IP adresinizin hello tercih ettiğiniz bir tarayıcı kullanarak Internet üzerinde olduğunu doğrulayın ("nedir IP adresimi isteyin).</span><span class="sxs-lookup"><span data-stu-id="f47ef-103">Review hello client IP address displayed and validate that this is your IP address on hello Internet using a browser of your choice (ask "what is my IP address).</span></span> <span data-ttu-id="f47ef-104">IP adresleri bazen çeşitli nedenlerle eşleşmez.</span><span class="sxs-lookup"><span data-stu-id="f47ef-104">Occasionally they do not match for a various reasons.</span></span>

    <!-- ![your IP address](../articles/sql-database/media/sql-database-get-started/your-ip-address.png) -->

3. <span data-ttu-id="f47ef-105">Merhaba IP adreslerinin eşleşmesi varsayılarak tıklatın **istemci IP'si Ekle** hello araç.</span><span class="sxs-lookup"><span data-stu-id="f47ef-105">Assuming that hello IP addresses match, click **Add client IP** on hello toolbar.</span></span>

    ![istemci IP’si ekle](../articles/sql-data-warehouse/media/sql-data-warehouse-get-started-provision/add-client-ip.png)

    > [!NOTE]
    > <span data-ttu-id="f47ef-107">Merhaba SQL veritabanı Güvenlik Duvarı'nı hello sunucu tooa tek IP adresi veya adresleri aralığının tamamını açabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f47ef-107">You can open hello SQL Database firewall on hello server tooa single IP address or an entire range of addresses.</span></span> <span data-ttu-id="f47ef-108">Ve kullanıcıların toologin tooany veritabanında açılırken hello güvenlik duvarı sağlar SQL yöneticiler sunucu toowhich geçerli kimlik bilgilerine sahip oldukları hello.</span><span class="sxs-lookup"><span data-stu-id="f47ef-108">Opening hello firewall enables SQL administrators and users toologin tooany database on hello server toowhich they have valid credentials.</span></span>
    >

4. <span data-ttu-id="f47ef-109">Tıklatın **kaydetmek** üzerinde bu sunucu düzeyinde güvenlik duvarı kuralı araç toosave hello ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="f47ef-109">Click **Save** on hello toolbar toosave this server-level firewall rule and then click **OK**.</span></span>

    ![istemci IP’si ekle](../articles/sql-database/media/sql-database-get-started-portal/server-firewall-rule.png)

> [!Tip]
> <span data-ttu-id="f47ef-111">Öğretici için bkz. [SQL Veritabanı öğreticisi: Sunucu, sunucu düzeyinde güvenlik duvarı kuralı, örnek veritabanı, veritabanı düzeyinde güvenlik duvarı oluşturma ve SQL Server’a bağlanma](../articles/sql-database/sql-database-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f47ef-111">For a tutorial, see [SQL Database tutorial: Create a server, a server-level firewall rule, a sample database, a database-level firewall rule and connect with SQL Server](../articles/sql-database/sql-database-get-started.md).</span></span>    
>
