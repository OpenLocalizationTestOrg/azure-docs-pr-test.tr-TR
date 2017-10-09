### <a name="prerequisites"></a>Ön koşullar
Bilmeniz gereken bir [Service Bus](https://azure.microsoft.com/services/service-bus/) hesabı.  

Bir mantıksal uygulama Azure Service Bus hesabınızı kullanabilmeniz için önce hello mantığı uygulama tooconnect tooyour hizmet veri yolu hesabı yetkilendirmeniz gerekir. Neyse ki, kolayca hello Azure portalı üzerinde mantıksal uygulama içinde bunu yapabilirsiniz.  

Mantıksal uygulama tooconnect tooyour Service Bus hesap hello adımları tooauthorize şunlardır:  

1. Merhaba mantığı Uygulama Tasarımcısı'nda bağlantı tooService veri yolu, toocreate seçin **Göster Microsoft yönetilen API'ler** hello aşağı açılan listesinde. Enter **hizmet veri yolu** hello arama kutusuna. Merhaba tetikleyici veya toouse istediğiniz eylemi seçin.  
    ![Hizmet veri yolu bağlantı görüntü 1](./media/connectors-create-api-servicebus/servicebus-1.png)  
2. Önce tüm bağlantılar tooService Bus oluşturmadıysanız, istendiğinde tooprovide Service Bus kimlik bilgileriniz olması. Bu kimlik bilgileri kullanılan tooauthorize olan mantığı uygulama tooconnect tooand Service Bus hesabınızın verilere erişebilir. Merhaba Service Bus Bağlayıcısı hello hizmet veri yolu ad alanı için hello bağlantı dizesi olması gerekir. Ayrıca gerektirir **Yönet** izinleri. Bağlantı dizenizi hello ad alanı için ya belirli bir varlık hello içerip içermediğini ise en iyi yolu tooknow `EntityPath` parametresi. Bulursa, bir mantıksal uygulama hello sağ bağlantı dizesi değil.  
    ![Hizmet veri yolu bağlantı dizesi](./media/connectors-create-api-servicebus/connectionstring.png)
3. Merhaba bağlantı dizesi hello ad alanı için alınan sonra hello Logic Apps, API bağlantısı için kullanabilirsiniz.  
    ![Hizmet veri yolu bağlantı görüntü 2](./media/connectors-create-api-servicebus/servicebus-2.png)  
4. Merhaba bağlantı oluşturulur ve mantıksal uygulamanızı ücretsiz tooproceed hello diğer sahip adımlarını artık olduğunuz dikkat edin.  
    ![Hizmet veri yolu bağlantı görüntü 3](./media/connectors-create-api-servicebus/servicebus-3.png)   

