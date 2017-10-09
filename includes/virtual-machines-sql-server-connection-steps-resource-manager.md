### <a name="configure-a-dns-label-for-hello-public-ip-address"></a>Merhaba ortak IP adresi için bir DNS etiketi yapılandırın

Merhaba Internet'ten gelen tooconnect toohello SQL Server veritabanı altyapısı, ortak IP adresi için bir DNS etiketi oluşturmayı düşünün. IP adresine göre bağlanabilirsiniz ancak daha kolay tooidentify bir A kaydı hello DNS etiketi oluşturur ve temel alınan genel IP adresi özetleri hello.

> [!NOTE]
> DNS etiketleri gerekli değildir tooonly bağlanmak toohello SQL Server planı hello içinde aynı örneği, sanal ağ veya yalnızca yerel olarak.

bir DNS etiketi toocreate önce seçin **sanal makineleri** hello Portalı'nda. SQL Server VM toobring özelliklerini ayarlama seçin.

1. Merhaba sanal makineye genel bakış içinde seçin, **genel IP adresi**.

    ![genel ip adresi](./media/virtual-machines-sql-server-connection-steps/rm-public-ip-address.png)

1. Genel IP adresinizin Hello özelliklerinde genişletin **yapılandırma**.

1. DNS etiket adı girin. Itanium tabanlı sistemler için kullanılan tooconnect tooyour SQL Server VM adı yerine IP adresine göre tarafından doğrudan olabilir bir A kaydı adıdır.

1. Merhaba tıklatın **kaydetmek** düğmesi.

    ![dns etiketi](./media/virtual-machines-sql-server-connection-steps/rm-dns-label.png)

### <a name="connect-toohello-database-engine-from-another-computer"></a>Başka bir bilgisayardan toohello veritabanına bağlan

1. Bir bilgisayarda toohello bağlı Internet'e açık SQL Server Management Studio (SSMS). SQL Server Management Studio’nuz yoksa [buradan](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) indirebilirsiniz.

1. Merhaba, **tooServer bağlanmak** veya **tooDatabase altyapısı bağlanmak** iletişim kutusu, Düzen hello **sunucu adı** değeri. Başlangıç IP adresi veya (Merhaba önceki görevde saptanmıştır) hello sanal makinenin tam DNS adını girin. Ayrıca bir virgül ekleyebilir ya da SQL Server'ın TCP bağlantı noktasını sağlayabilirsiniz. Örneğin, `mysqlvmlabel.eastus.cloudapp.azure.com,1433`.

1. Merhaba, **kimlik doğrulaması** kutusunda **SQL Server kimlik doğrulaması**.

1. Merhaba, **oturum açma** kutusu, geçerli SQL oturum açma türü hello adı.

1. Merhaba, **parola** kutusu, hello oturum açma hello parolayı girin.

1. **Bağlan**'a tıklayın.

    ![ssms bağlanma](./media/virtual-machines-sql-server-connection-steps/rm-ssms-connect.png)