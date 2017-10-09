### <a name="open-tcp-ports-in-hello-windows-firewall-for-hello-default-instance-of-hello-database-engine"></a>Merhaba Windows Güvenlik Duvarı'nı hello varsayılan hello veritabanı altyapısı örneği için TCP bağlantı noktaları açma
1. Toohello sanal makine ile Uzak Masaüstü Bağlantısı. Toohello VM bağlanma hakkında ayrıntılı yönergeler için bkz: [bir SQL VM Uzak Masaüstü ile açma](../articles/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md#open-the-vm-with-remote-desktop).
2. ' De, hello başlangıç ekranında oturum sonra yazın **WF.msc**ve ardından ENTER tuşuna basın.
   
    ![Merhaba Güvenlik Duvarı programını Başlat](./media/virtual-machines-sql-server-connection-steps/12Open-WF.png)
3. Merhaba, **Gelişmiş Güvenlik Özellikli Windows Güvenlik Duvarı**, buna hello sol bölmesinde, sağ **gelen kuralları**ve ardından **yeni kural** hello eylem bölmesinde.
   
    ![Yeni Kural](./media/virtual-machines-sql-server-connection-steps/13New-FW-Rule.png)
4. Merhaba, **yeni gelen kuralı Sihirbazı** iletişim kutusunda **kural türü**seçin **bağlantı noktası**ve ardından **sonraki**.
5. Merhaba, **protokol ve bağlantı noktaları** iletişim, hello Varsayılanı kullan **TCP**. Merhaba, **belirli yerel bağlantı noktaları** kutusunda ardından türü hello bağlantı noktası numarasını hello hello veritabanı altyapısı örneği (**1433** hello varsayılan örneği veya hello hello uç nokta adımda özel bağlantı noktası için tercih ettiğiniz için).
   
    ![TCP Bağlantı Noktası 1433](./media/virtual-machines-sql-server-connection-steps/14Port-1433.png)
6. **İleri**’ye tıklayın.
7. Merhaba, **eylem** iletişim kutusunda **hello bağlantıya izin verme**ve ardından **sonraki**.
   
    **Güvenlik Notu:** seçme **güvenliyse hello bağlantıya izin verme** ek güvenlik sağlayabilir. Ortamınızda tooconfigure ek güvenlik seçenekleri istiyorsanız bu seçeneği belirleyin.
   
    ![Bağlantılara İzin Verme](./media/virtual-machines-sql-server-connection-steps/15Allow-Connection.png)
8. Merhaba, **profil** iletişim kutusunda **ortak**, **özel**, ve **etki alanı**. Ardından **İleri**'ye tıklayın.
   
    **Güvenlik Notu:** seçme **ortak** üzerinden erişime izin veren Internet hello. Mümkün olduğu durumlarda daha kısıtlayıcı bir profil seçin.
   
    ![Genel Profil](./media/virtual-machines-sql-server-connection-steps/16Public-Private-Domain-Profile.png)
9. Merhaba, **adı** iletişim kutusu, bir ad ve bu kural için bir açıklama yazın ve ardından **son**.
   
    ![Kural Adı](./media/virtual-machines-sql-server-connection-steps/17Rule-Name.png)

Gerekirse diğer bileşenler için ek bağlantı noktaları açın. Daha fazla bilgi için bkz: [hello Windows Güvenlik Duvarı tooAllow SQL Server erişimi yapılandırma](http://msdn.microsoft.com/library/cc646023.aspx).

### <a name="configure-sql-server-toolisten-on-hello-tcp-protocol"></a>SQL Server toolisten TCP protokolü hello üzerinde yapılandırma

[!INCLUDE [Enable TCP](virtual-machines-sql-server-connection-tcp-protocol.md)]

### <a name="configure-sql-server-for-mixed-mode-authentication"></a>SQL Server’ı karma mod kimlik doğrulaması için yapılandırma
Merhaba SQL Server veritabanı altyapısı etki alanı ortamında Windows kimlik doğrulamasını kullanamazsınız. başka bir bilgisayardan tooconnect toohello veritabanı altyapısının SQL Server karışık mod kimlik doğrulaması için yapılandırın. Karma mod kimlik doğrulaması hem SQL Server Kimlik Doğrulaması’na hem de Windows Kimlik Doğrulaması’na izin verir.

> [!NOTE]
> Yapılandırılmış bir etki alanı ortamıyla Azure Sanal Ağı’nı yapılandırdıysanız, karma mod kimlik doğrulamasını yapılandırmanız gerekmeyebilir.
> 
> 

1. Merhaba başlangıç sayfasında, bağlı toohello sanal makine çalışırken yazın **SQL Server Management Studio** ve hello seçili simgesine tıklayın.
   
    Merhaba ilk kez hello kullanıcılar Management Studio ortam oluşturmalısınız Management Studio'yu açın. Bu birkaç dakika sürebilir.
2. Management Studio'yu sunar hello **tooServer bağlanmak** iletişim kutusu. Merhaba, **sunucu adı** kutusu, tür hello hello Nesne Gezgini ile Merhaba sanal makine tooconnect toohello veritabanı altyapısı adını (de kullanabilir hello sanal makine adı yerine **(yerel)** veya hello olarak tek nokta **sunucu adı**). Seçin **Windows kimlik doğrulaması**, bırakıp  ***your_VM_name*\your_local_administrator** hello içinde **kullanıcı adı** kutusu. **Bağlan**'a tıklayın.
   
    ![TooServer Bağlan](./media/virtual-machines-sql-server-connection-steps/19Connect-to-Server.png)
3. SQL Server Management Studio Object Explorer, SQL Server (Merhaba sanal makine adı) hello örneği hello adına sağ tıklayın ve ardından **özellikleri**.
   
    ![Sunucu Özellikleri](./media/virtual-machines-sql-server-connection-steps/20Server-Properties.png)
4. Merhaba üzerinde **güvenlik** sayfasında **sunucu kimlik doğrulaması**seçin **SQL Server ve Windows kimlik doğrulaması modu**ve ardından **Tamam** .
   
    ![Kimlik Doğrulaması Modunu Seçme](./media/virtual-machines-sql-server-connection-steps/21Mixed-Mode.png)
5. Merhaba SQL Server Management Studio iletişim kutusunda tıklatın **Tamam** tooacknowledge hello gereksinim toorestart SQL Server.
6. Nesne Gezgini’nde, sunucunuza sağ tıklayın ve ardından **Yeniden Başlat**’a tıklayın. (SQL Server Agent çalışıyorsa, onun da yeniden başlatılması gerekir.)
   
    ![Yeniden Başlatma](./media/virtual-machines-sql-server-connection-steps/22Restart2.png)
7. Merhaba SQL Server Management Studio iletişim kutusunda tıklatın **Evet** tooagree toorestart SQL Server istiyor.

### <a name="create-sql-server-authentication-logins"></a>SQL Server kimlik doğrulaması için oturum açma kimliği oluşturma
başka bir bilgisayardan tooconnect toohello veritabanı altyapısı, en az bir SQL Server kimlik doğrulaması oturum açma oluşturmanız gerekir.

1. SQL Server Management Studio Object Explorer içinde toocreate hello yeni oturum açma istediğiniz hello sunucu örneğinin hello klasörünü genişletin.
2. Sağ hello **güvenlik** klasörü, çok noktası**yeni**seçip **oturum açma...** .
   
    ![Yeni Oturum Açma Kimliği](./media/virtual-machines-sql-server-connection-steps/23New-Login.png)
3. Merhaba, **yeni oturum açma -** iletişim kutusunda, hello **genel** sayfasında, hello hello hello yeni kullanıcı adını girin **oturum açma adı** kutusu.
4. **SQL Server kimlik doğrulaması**’nı seçin.
5. Merhaba, **parola** kutusunda, hello yeni kullanıcı için bir parola girin. Merhaba bu parolayı yeniden girin **parolayı onayla** kutusu.
6. Gerekli hello parola zorlama seçenekleri seçin (**Şifre politikasını**, **parola süre sonu zorunlu**, ve **kullanıcı bir sonraki oturum açışında parolasını değiştirmeniz**). Bu oturum açma kendiniz için kullanıyorsanız, parolayı değiştirmek hello bir sonraki oturum açışında toorequire gerekmez.
7. Merhaba gelen **varsayılan veritabanı** listesinde, hello oturum açma için varsayılan bir veritabanı seçin. **Ana** hello bu seçenek varsayılandır. Bir kullanıcı veritabanı henüz oluşturmadıysanız, bu çok ayarlamak bırakın**ana**.
   
    ![Oturum Açma Özellikleri](./media/virtual-machines-sql-server-connection-steps/24Test-Login.png)
8. Oluşturmakta olduğunuz hello ilk oturum açma varsa, bir SQL Server yöneticisi olarak bu oturum açma toodesignate isteyebilirsiniz. Öyleyse hello üzerinde **sunucu rolleri** sayfasında, onay **sysadmin**.
   
   > [!NOTE]
   > Merhaba sysadmin sabit sunucu rolünün üyeleri hello veritabanı altyapısı tam denetime sahiptir. Bu rolün üyeliğini dikkatle kısıtlamalısınız.
   > 
   > 
   
   ![sysadmin](./media/virtual-machines-sql-server-connection-steps/25sysadmin.png)
9. Tamam'a tıklayın.

SQL Server oturum açma kimlikleri hakkında daha fazla bilgi için bkz. [Oturum Açma Kimliği Oluşturma](http://msdn.microsoft.com/library/aa337562.aspx).

