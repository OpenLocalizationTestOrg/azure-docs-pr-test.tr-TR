### <a name="create-a-new-logical-sql-server-in-hello-azure-portal"></a>Hello Azure portalında yeni bir mantıksal SQL sunucusu oluşturma

1. **Yeni**'ye tıklayın, **mantıksal sunucu** terimini arayın ve **ENTER**'a basın.

    ![mantıksal sunucu arama](./media/sql-data-warehouse-create-logical-server/search-logical-server.png)
2. **SQL Server (mantıksal sunucu)** girişini seçin 

    ![mantıksal sunucu seçme](./media/sql-data-warehouse-create-logical-server/select-logical-server.png)
  
3. Tıklatın **oluşturma** tooopen hello yeni SQL Server (mantıksal sunucu) dikey.

   <kbd>![mantıksal sunucusu dikey penceresini açmak](./media/sql-data-warehouse-create-logical-server/open-logical-server-blade.png) </kbd> <kbd> ![mantıksal sunucusu dikey](./media/sql-data-warehouse-create-logical-server/logical-server-blade.png)</kbd>
  
3. Merhaba SQL Server (mantıksal sunucu) dikey'nın sunucu adı metin kutusuna, hello yeni mantıksal sunucu için geçerli bir ad sağlayın. Yeşil onay işareti, geçerli bir ad sağladığınızı gösterir.
    
    ![yeni sunucu adı](./media/sql-data-warehouse-create-logical-server/new-name-logical-server.png)

    > [!IMPORTANT]
    > Merhaba, yeni sunucu için tam ad < Sunucunuzun_Adı > olacaktır. database.windows.net.
    >
    
4. Merhaba Server yönetici oturum açma metin kutusuna, bu sunucu için hello SQL kimlik doğrulaması oturum açma için kullanıcı adı sağlayın. Bu oturum açma hello sunucu asıl oturum olarak bilinir. Yeşil onay işareti, geçerli bir ad sağladığınızı gösterir.
    
    ![SQL yöneticisi oturum açma adı](./media/sql-data-warehouse-create-logical-server/sql-admin-login.png)
5. Merhaba, **parola** ve **parolayı onayla** metin kutularında, hello sunucu asıl oturum açma hesabı için bir parola sağlayın. Yeşil onay işareti, geçerli bir parola sağladığınızı gösterir.
    
    ![SQL yönetici parolası](./media/sql-data-warehouse-create-logical-server/sql-admin-password.png)
6. İzin toocreate nesneleri sahip bir abonelik seçin.

    ![aboneliği](./media/sql-data-warehouse-create-logical-server/subscription.png)
7. Hello kaynak grubunun metin kutusunda **Yeni Oluştur** hello kaynak grubunun metin kutusunda, hello (da mevcut bir kaynak grubu için kendiniz bir tane önceden oluşturduğunuz halinde kullanabilirsiniz) yeni kaynak grubu için geçerli bir ad girin. Yeşil onay işareti, geçerli bir ad sağladığınızı gösterir.

    ![yeni kaynak grubu](./media/sql-data-warehouse-create-logical-server/new-resource-group.png)

8. Merhaba, **konumu** metin kutusunda bir veri merkezi - "Avustralya Doğu" gibi uygun tooyour konumu.
    
    ![sunucu konumu](./media/sql-data-warehouse-create-logical-server/server-location.png)
    
    > [!TIP]
    > onay kutusunu hello **izin azure Hizmetleri tooaccess sunucusu** bu dikey pencerede değiştirilemez. Merhaba sunucu güvenlik duvarı dikey penceresinde bu ayarı değiştirebilirsiniz. Daha fazla bilgi için bkz. [Güvenliğe giriş](../articles/sql-database/sql-database-manage-servers-portal.md).
    >
    
9. **Oluştur**’a tıklayın.

    ![oluştur düğmesi](./media/sql-data-warehouse-create-logical-server/create.png)

