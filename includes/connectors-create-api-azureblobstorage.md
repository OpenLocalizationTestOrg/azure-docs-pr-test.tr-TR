### <a name="prerequisites"></a>Ön koşullar
* Bir Azure hesabı; oluşturabileceğiniz bir [ücretsiz bir hesap](https://azure.microsoft.com/free)
* Bir [Azure Blob Storage hesabı](../articles/storage/common/storage-create-storage-account.md) hello depolama hesabı adı ve erişim anahtarını dahil olmak üzere. Bu bilgileri hello Azure portal hello depolama hesabında hello özelliklerinde listelenir. Daha fazla bilgi edinin [Azure Storage](../articles/storage/common/storage-introduction.md).

Azure Blob Storage hesabınıza bir mantıksal uygulama kullanmadan önce tooyour Azure Blob Depolama hesabı bağlayın. Kolayca hello Azure portalı üzerinde mantıksal uygulama içinde bunu yapabilirsiniz.  

Merhaba aşağıdaki adımları kullanarak tooyour Azure Blob Storage hesabı Bağlan:  

1. Bir mantıksal uygulama oluşturun. Merhaba Logic Apps Tasarımcısı'nda bir tetikleyici ekleyin ve sonra bir eylem ekleyin. Seçin **Göster Microsoft yönetilen API'ler** hello açılan listeyi ve ardından "blob" Merhaba arama kutusuna girin. Merhaba eylemlerden birini seçin:  
   
    ![Azure Blob Depolama bağlantısı oluşturma adım](./media/connectors-create-api-azureblobstorage/azureblobstorage-1.png)  
2. TooAzure depolama daha önce herhangi bir bağlantısı oluşturmadıysanız, hello bağlantı ayrıntılarını istenir:   
   
    ![Azure Blob Depolama bağlantısı oluşturma adım](./media/connectors-create-api-azureblobstorage/connection-details.png)  
3. Merhaba depolama hesabı ayrıntılarını girin. Bir yıldız işareti özelliklerle gereklidir.
   
   | Özellik | Ayrıntılar |
   | --- | --- |
   | Bağlantı adı * |Bağlantınız için herhangi bir ad girin. |
   | Azure depolama hesabı adı * |Merhaba depolama hesabı adı girin. Merhaba depolama hesabı adı hello Azure Portalı'ndaki hello depolama özellikleri görüntülenir. |
   | Azure depolama hesabı erişim tuşu * |Merhaba depolama hesabı anahtarı girin. Merhaba erişim tuşları hello Azure Portalı'ndaki hello depolama özellikleri görüntülenir. |
   
    Bu kimlik bilgileri kullanılan tooauthorize mantığı uygulama tooconnect, verilerinizi erişim ve. 
4. **Oluştur**’u seçin.
5. Bildirim hello bağlantı oluşturuldu. Şimdi devam hello diğer mantıksal uygulamanızı adımlar: 
   
    ![Azure Blob Depolama bağlantısı oluşturma adım](./media/connectors-create-api-azureblobstorage/azureblobstorage-3.png)  

