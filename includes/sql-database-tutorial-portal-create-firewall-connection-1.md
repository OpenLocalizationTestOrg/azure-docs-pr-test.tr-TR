## <a name="log-in-toohello-azure-portal"></a>Toohello Azure portalında oturum açın

İçinde toohello oturum [Azure portal](https://portal.azure.com/).

## <a name="create-a-blank-sql-database-using-hello-azure-portal"></a>Hello Azure portalını kullanarak boş bir SQL veritabanı oluşturma

Azure SQL veritabanı bir dizi [işlem ve depolama kaynağı](../articles/sql-database/sql-database-service-tiers.md) ile oluşturulur. Merhaba veritabanı içinde oluşturulur bir [Azure kaynak grubu](../articles/azure-resource-manager/resource-group-overview.md) ve bir [Azure SQL Database mantıksal sunucusu](../articles/sql-database/sql-database-features.md). 

Bu adımları toocreate boş bir SQL veritabanı izleyin. 

1. Merhaba tıklatın **yeni** düğmesi hello sol üst köşesinin hello Azure portalı üzerinde bulunamadı.

2. Seçin **veritabanları** hello gelen **yeni** sayfasında ve seçin **SQL veritabanı** hello gelen **veritabanları** sayfası. 

   ![Boş veritabanı oluşturma](../articles/sql-database/media/sql-database-design-first-database/create-empty-database.png)

3. Hello SQL veritabanı formu görüntü önceki hello üzerinde gösterildiği gibi bilgileri, aşağıdaki hello ile doldurun:   

   | Ayar | Önerilen değer | Açıklama |
   | --------| --------------- | ----------- | 
   | **Veritabanı adı** | mySampleDatabase | Geçerli veritabanı adları için bkz. [Veritabanı Tanımlayıcıları](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers). | 
   | **Abonelik** | Aboneliğiniz  | Abonelikleriniz hakkında daha ayrıntılı bilgi için bkz. [Abonelikler](https://account.windowsazure.com/Subscriptions). |
   | **Kaynak grubu** | myResourceGroup | Geçerli kaynak grubu adları için bkz. [Adlandırma kuralları ve kısıtlamalar](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions). |
   | **Kaynak seçin** | Boş veritabanı | Boş bir veritabanı oluşturulması gerektiğini belirtir. |
   ||||

4. Tıklatın **Server** toocreate ve yeni veritabanı için yeni bir sunucu yapılandırabilirsiniz. Merhaba dolgu **yeni sunucu form** bilgisinden hello ile: 

   | Ayar | Önerilen değer | Açıklama |
   | --------| --------------- | ----------- | 
   | **Sunucu adı** | Herhangi bir genel benzersiz adı. | Geçerli sunucu adları için bkz. [Adlandırma kuralları ve kısıtlamalar](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions). | 
   | **Sunucu yöneticisi oturum açma bilgileri** | Herhangi bir geçerli adı. | Geçerli oturum açma adları için bkz. [Veritabanı Tanımlayıcıları](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers).|
   | **Parola** | Geçerli parola. | Parolanız en az sekiz karakter olmalıdır ve kategorileri aşağıdaki hello üçünden karakterler içermelidir: büyük harf karakterler, küçük harfler, sayılar ve alfasayısal olmayan karakter. |
   | **Konum** | Herhangi bir geçerli konumu. | Bölgeler hakkında bilgi için bkz. [Azure Bölgeleri](https://azure.microsoft.com/regions/). |
   ||||

   ![create database-server](../articles/sql-database/media/sql-database-design-first-database/create-database-server.png)

5. **Seç**'e tıklayın.

6. Tıklatın **fiyatlandırma katmanı** toospecify hello hizmeti katmanını ve performans düzeyini yeni veritabanı. Bu öğretici için seçin **20 Dtu'lar** ve **250** GB depolama alanı.

   ![create database-s1](../articles/sql-database/media/sql-database-design-first-database/create-empty-database-pricing-tier.png)

7. **Uygula**'ya tıklayın.  

8. Seçin bir **harmanlama** hello boş veritabanı (Bu öğretici için kullanım hello varsayılan değer). Harmanlamaları hakkında daha fazla bilgi için bkz: [harmanlamaları](https://docs.microsoft.com/sql/t-sql/statements/collations)

9. Tıklatın **oluşturma** tooprovision hello veritabanı. Bir dakika ve bir yarı toocomplete hakkında alır sağlama. 

10. Merhaba araç çubuğundan, **bildirimleri** toomonitor hello dağıtım işlemi.

   ![bildirim](../articles/sql-database/media/sql-database-get-started-portal/notification.png)

## <a name="create-a-server-level-firewall-rule-using-hello-azure-portal"></a>Hello Azure portal kullanarak bir sunucu düzeyinde güvenlik duvarı kuralı oluşturma

SQL veritabanı hizmetinin Hello hello sunucu düzeyinde güvenlik duvarı oluşturur. Başlangıçta hello güvenlik duvarı dış araçları ve uygulamaları toohello sunucu ya da hello sunucudaki tooany veritabanları bağlanmasını engeller. Bir güvenlik duvarı kuralı tooopen belirli IP adreslerini oluşturulduktan sonra bağlantılara izin verilir. Bu adımları toocreate izleyin bir [SQL veritabanı sunucu düzeyinde güvenlik duvarı kuralı](../articles/sql-database/sql-database-firewall-configure.md) , istemcinin IP adresi ve IP adresiniz yalnızca hello SQL veritabanı güvenlik duvarı üzerinden tooenable dış bağlantısı. 


> [!NOTE]
> Azure SQL veritabanı bağlantı noktası 1433 üzerinden iletişim kurar. Yalnızca hello güvenlik duvarı ağınızın 1433 bağlantı noktası üzerinden giden trafik verir sonra tooSQL veritabanı bağlanabilirsiniz.


1. Merhaba dağıtım tamamlandıktan sonra **SQL veritabanları** hello sol menüsünden ve ardından **mySampleDatabase** hello üzerinde **SQL veritabanları** sayfası. Merhaba hello tam olarak gösteren, veritabanı açılır genel bakış sayfasında tam sunucu adını (gibi **mynewserver20170313.database.windows.net**) ve diğer yapılandırmalar için seçenekler sağlar. Daha sonra kullanmak üzere bu tam sunucu adını kopyalayın.

   > [!IMPORTANT]
   > Sonraki hızlı başlatır, veritabanlarını ve bu tam sunucu adı tooconnect tooyour sunucu gerekir.
   > 

   ![sunucu adı](../articles/sql-database/media/sql-database-get-started-portal/server-name.png) 

2. Tıklatın **ayarlayın sunucu Güvenlik Duvarı** hello önceki görüntüde gösterildiği gibi hello araç. Merhaba **Güvenlik Duvarı ayarları** hello SQL veritabanı sunucusu sayfasını açar. 

   ![sunucu güvenlik duvarı kuralı](../articles/sql-database/media/sql-database-get-started-portal/server-firewall-rule.png) 


3. Tıklatın **istemci IP'si Ekle** hello araç tooadd üzerinde geçerli IP adresi tooa yeni güvenlik duvarı kuralı. Güvenlik duvarı kuralı, 1433 numaralı bağlantı noktasını tek bir IP adresi veya bir IP adresi aralığı için açabilir.

4. **Kaydet** düğmesine tıklayın. Geçerli IP adresiniz hello mantıksal sunucuda bağlantı noktası 1433'ü açmak için bir sunucu düzeyinde güvenlik duvarı kuralı oluşturulur.

   ![sunucu güvenlik duvarı kuralı ayarla](../articles/sql-database/media/sql-database-get-started-portal/server-firewall-rule-set.png) 

4. Tıklatın **Tamam** ve hello kapatın **Güvenlik Duvarı ayarları** sayfası.

Şimdi toohello Azure SQL veritabanı sunucusunu ve veritabanlarını SQL Server Management Studio (SSMS) gibi bir araç kullanarak bağlanabilir. Bu IP adresinden Hello bağlantıdır ve daha önce oluşturduğunuz hello server yönetici hesabı kullanır.


> [!IMPORTANT]
> Varsayılan olarak, tüm Azure hizmetlerini hello SQL veritabanı güvenlik duvarı üzerinden erişim etkin. Tıklatın **OFF** tüm Azure Hizmetleri için bu sayfayı toodisable üzerinde.


## <a name="get-connection-string-values-using-hello-azure-portal"></a>Hello Azure portal kullanarak bağlantı dizesi değerlerini alma

Azure SQL veritabanı sunucunuz için Hello tam sunucu adını hello Azure portal alın. SQL Server Management Studio'yu kullanarak hello tam adı tooconnect tooyour sunucusu kullanın.

1. İçinde toohello oturum [Azure portal](https://portal.azure.com/).

2. Seçin **SQL veritabanları** hello sol taraftaki menüden veritabanınızda hello tıklatıp **SQL veritabanları** sayfası. 

3. Merhaba, **Essentials** Merhaba, veritabanı için Azure portal sayfası bölmesinde bulun ve ardından hello kopyalayın **sunucu adı**.

   ![bağlantı bilgileri](../articles/sql-database/media/sql-database-get-started-portal/server-name.png) 
