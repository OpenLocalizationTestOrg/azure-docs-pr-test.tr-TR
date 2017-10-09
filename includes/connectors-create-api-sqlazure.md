### <a name="prerequisites"></a>Ön koşullar
* Bir Azure hesabı; oluşturabileceğiniz bir [ücretsiz bir hesap](https://azure.microsoft.com/free)
* Bir [Azure SQL veritabanı](../articles/sql-database/sql-database-get-started.md) hello sunucu adı, veritabanı adı ve kullanıcı adı/parola, bağlantı bilgileriyle birlikte de dahil olmak üzere. Bu bilgiler hello SQL veritabanı bağlantı dizesi dahil edilir:
  
    Sunucu = tcp:*yoursqlservername*. database.windows.net,1433;Initial katalog =*yourqldbname*; Kalıcı güvenlik bilgisi = False; Kullanıcı Kimliği {your_username} =; Parola {your_password} =; MultipleActiveResultSets = False; Şifreleme = True; TrustServerCertificate = False; Bağlantı zaman aşımı = 30;
  
    Daha fazla bilgi edinin [Azure SQL veritabanlarını](https://azure.microsoft.com/services/sql-database).

> [!NOTE]
> Bir Azure SQL veritabanı oluşturduğunuzda, aynı zamanda SQL ile dahil hello örnek veritabanları oluşturabilirsiniz. 
> 
> 

Azure SQL veritabanınıza bir mantıksal uygulama kullanmadan önce tooyour SQL veritabanına bağlayın. Kolayca hello Azure portalı üzerinde mantıksal uygulama içinde bunu yapabilirsiniz.  

Aşağıdaki hello kullanarak Azure SQL veritabanı adımları tooyour Bağlan:  

1. Bir mantıksal uygulama oluşturun. Merhaba Logic Apps Tasarımcısı'nda bir tetikleyici ekleyin ve sonra bir eylem ekleyin. Seçin **Göster Microsoft yönetilen API'ler** hello açılan listeyi ve ardından "sql" Merhaba arama kutusuna girin. Merhaba eylemlerden birini seçin:  
   
    ![SQL Azure bağlantısı oluşturma adım](./media/connectors-create-api-sqlazure/sql-actions.png)
2. Tüm bağlantılar tooSQL veritabanını daha önce oluşturmadıysanız, hello bağlantı ayrıntılarını istenir:  
   
    ![SQL Azure bağlantısı oluşturma adım](./media/connectors-create-api-sqlazure/connection-details.png) 
3. Merhaba SQL veritabanının ayrıntılarını girin. Bir yıldız işareti özelliklerle gereklidir.
   
   | Özellik | Ayrıntılar |
   | --- | --- |
   | Ağ geçidi bağlanma |İşaretlemeden bırakın. Tooan bağlanma SQL Server içi olduğunda kullanılır. |
   | Bağlantı adı * |Bağlantınız için herhangi bir ad girin. |
   | SQL Server adı * |Merhaba sunucu adı girin; aşağıdakine benzer olduğu *servername.database.windows.net*. Merhaba sunucu ad hello Azure Portalı'ndaki hello SQL veritabanı özellikleri görüntülenir ve hello bağlantı dizesini de görüntülenir. |
   | SQL veritabanı adı * |SQL veritabanınız verdiğiniz hello adı girin. Bu hello bağlantı dizesinde hello SQL veritabanı özelliklerinde listelenir: Initial Catalog =*yoursqldbname*. |
   | Kullanıcı adı * |Merhaba SQL Database oluşturduğunuzda oluşturulan hello kullanıcı adı girin. Bu, hello Azure Portalı'ndaki hello SQL veritabanı özellikleri listelenir. |
   | Parola * |Merhaba SQL Database oluşturduğunuzda oluşturulan hello parolayı girin. |
   
    Bu kimlik bilgileri kullanılan tooauthorize mantığı uygulama tooconnect, SQL veri erişim ve. Tamamlandıktan sonra bağlantı ayrıntılarınızı benzer toohello aşağıdaki bakın:  
   
    ![SQL Azure bağlantısı oluşturma adım](./media/connectors-create-api-sqlazure/sample-connection.png) 
4. **Oluştur**’u seçin. 
5. Bildirim hello bağlantı oluşturuldu. Şimdi devam hello diğer mantıksal uygulamanızı adımlar: 
   
    ![SQL Azure bağlantısı oluşturma adım](./media/connectors-create-api-sqlazure/table.png)

