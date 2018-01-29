1. [Azure portalında][Azure portal] oturum açın.
2. Soldaki menüden **+ Kaynak oluştur**'u seçin. Ardından **Kurumsal tümleştirme** > **Geçiş**'i seçin.
3. **Ad alanı oluştur** bölümüne bir ad alanı adı girin. Adın kullanılabilirliği sistem tarafından hemen denetlenir.
4. **Abonelik** kutusunda, ad alanı oluşturmak için kullanmak istediğiniz Azure aboneliğini seçin.
5. [Kaynak grubu](../articles/azure-resource-manager/resource-group-portal.md) kutusunda, ad alanını barındırmak üzere var olan bir kaynak grubunu seçin veya yeni bir kaynak grubu oluşturun.  
6. **Konum** alanında, ad alanınızın barındırılması gereken ülkeyi veya bölgeyi seçin.
   
    ![ad alanı oluşturma][create-namespace]
7. **Oluştur**’u seçin. Sistem ad alanınızı oluşturur ve kullanıma açar. Birkaç dakika sonra sistem, hesabınız için kaynakları sağlar.

### <a name="get-management-credentials"></a>Yönetim kimlik bilgilerini alma

1. **Tüm kaynaklar**'ı ve ardından yeni oluşturulan ad alanı adını seçin.
2. Geçiş ad alanı bölümünde, **Paylaşılan erişim ilkeleri**'ni seçin.  
3. **Paylaşılan erişim ilkeleri** bölümünde **RootManageSharedAccessKey** öğesini seçin.
   
    ![bağlantı bilgisi][connection-info]
4. **İlke: RootManageSharedAccessKey** bölümünde **Bağlantı dizesi–Birincil anahtar**'ın yanındaki **Kopyala** düğmesini seçin. Daha sonra kullanabilmeniz için bağlantı dizesi panonuza kopyalanır. Bu değeri Not Defteri veya başka bir geçici konuma yapıştırın.
   
    ![bağlantı dizesi][connection-string]

5. **Birincil anahtar** değerini daha sonra kullanmak üzere kopyalayıp geçici bir konuma yapıştırarak önceki adımı tekrarlayın.  

<!--Image references-->

[create-namespace]: ./media/relay-create-namespace-portal/create-namespace.png
[connection-info]: ./media/relay-create-namespace-portal/connection-info.png
[connection-string]: ./media/relay-create-namespace-portal/connection-string.png
[Azure portal]: https://portal.azure.com
