1. Uzak Masaüstü ile sanal makineye bağlıyken **Yapılandırma Yöneticisi**‘ni arayın:

    ![SSCM’yi Açma](./media/virtual-machines-sql-server-connection-tcp-protocol/sql-server-configuration-manager.png)

1. SQL Server Yapılandırma Yöneticisi’ndeki konsol bölmesinde **SQL Server Ağ Yapılandırması**’nı genişletin.

1. Konsol bölmesinde **MSSQLSERVER Protokolleri**’ne tıklayın (varsayılan örnek adı). Ayrıntılar bölmesinde **TCP**’ye sağ tıklayın ve henüz etkinleştirilmemişse **Etkinleştir**’e tıklayın.

    ![TCP’yi Etkinleştirme](./media/virtual-machines-sql-server-connection-tcp-protocol/enable-tcp.png)

1. Konsol bölmesinde **SQL Server Hizmetleri**’ne tıklayın. Ayrıntılar bölmesinde **SQL Server’a (*örnek adı*)** (varsayılan örnek adı: **SQL Server (MSSQLSERVER)**) sağ tıklayın ve sonra da SQL Server örneğini durdurmak ve yeniden başlatmak için **Yeniden Başlat**’a tıklayın.

    ![Veritabanı Altyapısını Yeniden Başlatma](./media/virtual-machines-sql-server-connection-tcp-protocol/restart-sql-server.png)

1. SQL Server Yapılandırma Yöneticisi’ni kapatın.

SQL Server Veritabanı Altyapısı’nda protokolleri etkinleştirme hakkında daha fazla bilgi için bkz. [Sunucu Ağ Protokolünü Etkinleştirme veya Devre Dışı Bırakma](http://msdn.microsoft.com/library/ms191294.aspx).
