#### <a name="prerequisites"></a>Ön koşullar
* Bir Azure hesabı; oluşturabileceğiniz bir [ücretsiz bir hesap](https://azure.microsoft.com/free)
* A [OneDrive](https://www.microsoft.com/store/apps/onedrive/9wzdncrfj1p3) hesabı 

Bir mantıksal uygulama OneDrive hesabınıza kullanmadan önce hello mantığı uygulama tooconnect tooyour OneDrive hesabınıza yetkilendirin.  Kolayca hello Azure portalı üzerinde mantıksal uygulama içinde bunu yapabilirsiniz. 

Merhaba aşağıdaki adımları kullanarak logic app tooconnect tooyour OneDrive hesabınıza yetkilendirin.

1. Bir mantıksal uygulama oluşturun. Merhaba Logic Apps Tasarımcısı'nda seçin **Göster Microsoft yönetilen API'ler** hello açılan listeyi ve ardından "onedrive" Merhaba arama kutusuna girin. Merhaba Tetikleyicileri veya Eylemler birini seçin:  
   ![](./media/connectors-create-api-onedrive/onedrive-1.png)
2. Daha önce tüm bağlantıları tooOneDrive oluşturmadıysanız, OneDrive kimlik bilgilerinizi kullanarak istendiğinde toosign şunlardır:  
   ![](./media/connectors-create-api-onedrive/onedrive-2.png)
3. Seçin **oturum**, kullanıcı adı ve parolayı girin. Seçin **oturum**:  
   ![](./media/connectors-create-api-onedrive/onedrive-3.png)   
   
    Bu kimlik bilgileri kullanılan tooauthorize, logic app tooconnect, OneDrive hesabınızdaki hello verilere erişim ve. 
4. Seçin **Evet** tooauthorize OneDrive hesabınıza mantığı uygulama toouse hello:  
   ![](./media/connectors-create-api-onedrive/onedrive-4.png)   
5. Bildirim hello bağlantı oluşturuldu. Şimdi devam hello diğer mantıksal uygulamanızı adımlar:  
   ![](./media/connectors-create-api-onedrive/onedrive-5.png)

