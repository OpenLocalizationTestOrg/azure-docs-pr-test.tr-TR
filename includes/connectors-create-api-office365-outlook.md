#### <a name="prerequisites"></a>Ön koşullar
* Bir Azure hesabı; oluşturabileceğiniz bir [ücretsiz bir hesap](https://azure.microsoft.com/free)
* Bir [Office 365](https://office365.com) hesabı  

Office 365 hesabınıza bir mantıksal uygulama kullanmadan önce hello mantığı uygulama tooconnect tooyour Office 365 hesabı yetkilendirin. Kolayca hello Azure portalı üzerinde mantıksal uygulama içinde bunu yapabilirsiniz.  

Merhaba aşağıdaki adımları kullanarak logic app tooconnect tooyour Office 365 hesabınıza yetkilendirin.

1. Bir mantıksal uygulama oluşturun. Merhaba Logic Apps Tasarımcısı'nda seçin **Göster Microsoft yönetilen API'ler** hello açılan listeyi ve ardından "office 365" Merhaba arama kutusuna girin. Merhaba Tetikleyicileri veya Eylemler birini seçin:  
    ![Office 365 bağlantı oluşturma adım](./media/connectors-create-api-office365-outlook/office365-sendemail.png)  
2. Daha önce tüm bağlantıları tooOffice 365 oluşturmadıysanız, Office 365 kimlik bilgilerinizi kullanarak istendiğinde toosign şunlardır:  
    ![Office 365 bağlantı oluşturma adım](./media/connectors-create-api-office365-outlook/office365-signin.png)  
3. Seçin **oturum**, kullanıcı adı ve parolayı girin. Seçin **oturum**:  
    ![Office 365 bağlantı oluşturma adım](./media/connectors-create-api-office365-outlook/office365-usernamepassword.png)
   
    Bu kimlik bilgileri, logic app tooconnect kullanılan tooauthorize olan ve Office 365 hesabınıza erişemiyor. 
4. Bildirim hello bağlantı oluşturuldu. Şimdi devam hello diğer mantıksal uygulamanızı adımlar:   
    ![Office 365 bağlantı oluşturma adım](./media/connectors-create-api-office365-outlook/office365-sendemailproperties.png)  

