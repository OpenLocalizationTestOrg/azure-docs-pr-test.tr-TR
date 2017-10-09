1. Uzak Masaüstü ile bağlı toohello sanal makine arama **Configuration Manager**:

    ![SSCM’yi Açma](./media/virtual-machines-sql-server-connection-tcp-protocol/sql-server-configuration-manager.png)

1. SQL Server Yapılandırma Yöneticisi'nde hello Konsol bölmesinde **SQL Server Ağ Yapılandırması**.

1. Merhaba Konsol bölmesinde **MSSQLSERVER protokolleri** (Merhaba varsayılan örnek adı.) Merhaba Ayrıntılar bölmesinde, **TCP** tıklatıp **etkinleştirmek** zaten etkin değilse.

    ![TCP’yi Etkinleştirme](./media/virtual-machines-sql-server-connection-tcp-protocol/enable-tcp.png)

1. Merhaba Konsol bölmesinde **SQL Server Hizmetleri**. Merhaba Ayrıntılar bölmesinde,  **SQL Server (*örnek adı*) ** (Merhaba varsayılan örneği **SQL Server (MSSQLSERVER)**) ve ardından **yeniden başlatın** , SQL Server toostop ve yeniden başlatma hello örneği.

    ![Veritabanı Altyapısını Yeniden Başlatma](./media/virtual-machines-sql-server-connection-tcp-protocol/restart-sql-server.png)

1. SQL Server Yapılandırma Yöneticisi’ni kapatın.

Merhaba SQL Server veritabanı altyapısı protokolleri etkinleştirme hakkında daha fazla bilgi için bkz: [etkinleştirmek veya devre dışı bir sunucu ağ protokolü](http://msdn.microsoft.com/library/ms191294.aspx).
