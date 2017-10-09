## <a name="what-are-service-bus-topics-and-subscriptions"></a>Service Bus konuları ve abonelikleri nelerdir?
Service Bus konuları ve abonelikleri *publish/subscribe* mesajlaşma iletişim modelini destekler. Konular ve abonelikler kullanıldığında, dağıtılmış uygulamanın bileşenleri birbirleriyle doğrudan iletişim kurmazlar; bunun yerine bir aracı gibi davranan bir konu aracılığıyla iletileri değiş tokuş eder.

![TopicConcepts](./media/howto-service-bus-topics/sb-topics-01.png)

Service Bus kuyruklarının tersine, burada her ileti bir tüketici tarafından işlenir; konular ve abonelikler, publish/subscribe modelini kullanarak iletişimin "bir-çok" biçimini sağlar. Birden çok abonelik tooa konu kaydetmek mümkündür. Tooa konu bir ileti gönderildiğinde, ardından kullanılabilir tooeach abonelik toohandle/işlem bağımsız olarak yapılır.

Bir abonelik tooa konu toohello konu gönderilen Merhaba iletileri kopyalarını alan sanal kuyruğa benzer. İsteğe bağlı olarak toofilter sağlayan bir abonelik başına temelinde bir konu için filtre kuralları kaydedilemedi veya hangi iletileri tooa konu hangi konu abonelikleriyle alınan kısıtlayın.

Service Bus konuları ve abonelikleri tooscale etkinleştirmek ve çok sayıda kullanıcıdan ve uygulamadan gelen iletileri çok sayıda işlem.

## <a name="create-a-namespace"></a>Ad alanı oluşturma
Azure'da Service Bus konuları ve abonelikleri kullanarak toobegin önce oluşturmanız gerekir bir *hizmet ad alanı*. Ad alanı, uygulamanızda bulunan Service Bus kaynaklarını adreslemek için içeriğin kapsamını belirleyen bir kapsayıcı sunar.

toocreate bir ad alanı:

1. Toohello üzerinde oturum [Azure portal][Azure portal].
2. Hello sol gezinti bölmesinde hello portalı tıklatın **yeni**, ardından **Kurumsal tümleştirme**ve ardından **Service Bus**.
3. Merhaba, **ad alanı oluşturma** iletişim kutusunda, bir ad alanı adı girin. Merhaba adı olup olmadığını hello sistem hemen toosee denetler.
4. Emin hello ad alanı adı yapmadan kullanılabilir olduktan sonra fiyatlandırma Katmanı (temel, standart veya Premium) hello seçin.
5. Merhaba, **abonelik** alanında, hangi toocreate hello ad alanında bir Azure aboneliği seçin.
6. Merhaba, **kaynak grubu** alanında, hangi hello ad alanı Canlı veya yeni bir tane oluşturmak varolan bir kaynak grubu seçin.      
7. İçinde **konumu**, hello ülke veya bölge içinde ad alanınızın barındırılması seçin.
   
    ![ad alanı oluşturma][create-namespace]
8. Merhaba tıklatın **oluşturma** düğmesi. Şimdi Hello sistem ad alanınızı oluşturur ve kullanıma açar. Hesabınız için hello sistem kaynakları sağlarken birkaç dakika toowait olabilir.

### <a name="obtain-hello-credentials"></a>Merhaba kimlik bilgilerini alma
1. Ad alanları Hello listesinde yeni oluşturulan ad alanı adı hello tıklayın.
2. Merhaba, **Service Bus ad alanı** dikey penceresinde tıklatın **paylaşılan erişim ilkeleri**.
3. Merhaba, **paylaşılan erişim ilkeleri** dikey penceresinde tıklatın **RootManageSharedAccessKey**.
   
    ![bağlantı bilgisi][connection-info]
4. Merhaba, **İlkesi: RootManageSharedAccessKey** dikey penceresinde hello Kopyala düğmesini tıklatın ardından çok**bağlantı dizesi – birincil anahtarı**, daha sonra kullanmak için toocopy hello bağlantı dizesi tooyour Pano.
   
    ![bağlantı dizesi][connection-string]

[Azure portal]: https://portal.azure.com
[create-namespace]: ./media/howto-service-bus-topics/create-namespace.png
[connection-info]: ./media/howto-service-bus-topics/connection-info.png
[connection-string]: ./media/howto-service-bus-topics/connection-string.png


