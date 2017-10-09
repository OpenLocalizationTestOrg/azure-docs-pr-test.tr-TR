### <a name="prerequisites"></a>Ön koşullar
* Twilio hesabı
* SMS alabileceği bir doğrulanmış Twilio telefon numarası
* SMS gönderebilen bir doğrulanmış Twilio telefon numarası

> [!NOTE]
> Twilio deneme hesabı kullanıyorsanız, yalnızca SMS çok gönderebilirsiniz**doğrulandı** telefon numaraları.  
> 
> 

Bir mantıksal uygulama Twilio hesabınızı kullanabilmeniz için önce hello mantığı uygulama tooconnect tooyour Twilio hesabını yetkilendirmeniz gerekir. Neyse ki, kolayca hello Azure portalı üzerinde mantıksal uygulama içinde bunu yapabilirsiniz. 

Mantıksal uygulama tooconnect tooyour Twilio hesabı hello adımları tooauthorize şunlardır:

1. Merhaba mantığı Uygulama Tasarımcısı'nda bir bağlantı tooTwilio toocreate seçin **Göster Microsoft yönetilen API'ler** Merhaba, açılan liste ardından girin *Twilio* hello arama kutusuna. Merhaba tetikleyici veya toouse beğendiğiniz eylem seçin:  
   ![](./media/connectors-create-api-twilio/twilio-0.png)
2. Tüm bağlantılar tooTwilio önce oluşturmadıysanız, istendiğinde tooprovide Twilio kimlik bilgilerinizi elde edersiniz. Bu kimlik bilgileri, Logic app tooconnect kullanılan tooauthorize olması ve Twilio hesabınızın veri erişim:  
   ![](./media/connectors-create-api-twilio/twilio-1.png)  
3. Merhaba gerekir **Twilio hesap kimliği** ve **Twilio erişim belirteci** Twilio içinde hello panodan şekilde bu iki parça bilgi tooyour Twilio hesabı şimdi toograb oturum:  
   ![](./media/connectors-create-api-twilio/twilio-2.png)  
4. Twilio ve Logic apps farklı adlar tooidentify bu iki parça bilgi kullanın. İşte nasıl bunları toohello Logic apps iletişim eşlemeniz gerekir:![](./media/connectors-create-api-twilio/twilio-3.png)  
5. Select hello **bağlantı oluşturmak** düğmesi:  
   ![](./media/connectors-create-api-twilio/twilio-4.png)
6. Merhaba bağlantı oluşturulur ve mantıksal uygulamanızı ücretsiz tooproceed hello diğer sahip adımlarını artık olduğunuz dikkat edin:  
   ![](./media/connectors-create-api-twilio/twilio-5.png)

