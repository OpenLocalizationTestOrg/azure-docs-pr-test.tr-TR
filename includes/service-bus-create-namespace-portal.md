Azure'da Service Bus kullanarak toobegin kuyruklar, öncelikle bir ad alanı Azure arasında benzersiz bir ad ile oluşturmanız gerekir. Ad alanı, uygulamanızda bulunan Service Bus kaynaklarını adreslemek için içeriğin kapsamını belirleyen bir kapsayıcı sunar.

toocreate bir ad alanı:

1. Toohello üzerinde oturum [Azure portal][Azure portal].
2. Hello sol gezinti bölmesinde hello portalı tıklatın **yeni**, ardından **Kurumsal tümleştirme**ve ardından **Service Bus**.
3. Merhaba, **ad alanı oluşturma** iletişim kutusunda, bir ad alanı adı girin. Merhaba adı olup olmadığını hello sistem hemen toosee denetler.
4. Emin hello ad alanı adı yapmadan kullanılabilir olduktan sonra fiyatlandırma Katmanı (temel, standart veya Premium) hello seçin.
5. Merhaba, **abonelik** alanında, hangi toocreate hello ad alanında bir Azure aboneliği seçin.
6. Merhaba, **kaynak grubu** alanında, hangi hello ad alanı Canlı veya yeni bir tane oluşturmak varolan bir kaynak grubu seçin.      
7. İçinde **konumu**, hello ülke veya bölge içinde ad alanınızın barındırılması seçin.
   
    ![ad alanı oluşturma][create-namespace]
8. **Oluştur**'a tıklayın. Şimdi Hello sistem ad alanınızı oluşturur ve kullanıma açar. Hesabınız için hello sistem kaynakları sağlarken birkaç dakika toowait olabilir.

### <a name="obtain-hello-management-credentials"></a>Merhaba yönetim kimlik bilgilerini alma

1. Ad alanları Hello listesinde yeni oluşturulan ad alanı adı hello tıklayın.
2. Merhaba ad alanı dikey penceresinde tıklayın **paylaşılan erişim ilkeleri**.
3. Merhaba, **paylaşılan erişim ilkeleri** dikey penceresinde tıklatın **RootManageSharedAccessKey**.
   
    ![bağlantı bilgisi][connection-info]
4. Merhaba, **İlkesi: RootManageSharedAccessKey** dikey penceresinde hello Kopyala düğmesini tıklatın ardından çok**bağlantı dizesi – birincil anahtarı**, daha sonra kullanmak için toocopy hello bağlantı dizesi tooyour Pano. Bu değeri Not Defteri veya başka bir geçici konuma yapıştırın.
   
    ![bağlantı dizesi][connection-string]

5. Kopyalama ve yapıştırma hello değerini yineleme hello önceki adımda **birincil anahtar** tooa daha sonra kullanmak için geçici konum.

<!--Image references-->

[create-namespace]: ./media/service-bus-create-namespace-portal/create-namespace.png
[connection-info]: ./media/service-bus-create-namespace-portal/connection-info.png
[connection-string]: ./media/service-bus-create-namespace-portal/connection-string.png
[Azure portal]: https://portal.azure.com
