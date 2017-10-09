
1. Hello çözüm görünümü içinde (veya **Çözüm Gezgini** Visual Studio'da), sağ hello **bileşenleri** klasörünü tıklatın **daha almak bileşenleri...** , hello Ara **Google Cloud Messaging istemcisi** bileşeni ve toohello proje ekleyin.
2. Merhaba ToDoActivity.cs proje dosyasını açın ve hello aşağıdakileri ekleyin deyimi toohello sınıfını kullanarak:
   
        using Gcm.Client;
3. Merhaba, **ToDoActivity** sınıfı, yeni kod aşağıdaki hello ekleyin: 
   
        // Create a new instance field for this activity.
        static ToDoActivity instance = new ToDoActivity();
   
        // Return hello current activity instance.
        public static ToDoActivity CurrentActivity
        {
            get
            {
                return instance;
            }
        }
        // Return hello Mobile Services client.
        public MobileServiceClient CurrentClient
        {
            get
            {
                return client;
            }
        }
   
    Bu, tooaccess hello mobil istemci hello itme işleyici hizmet işlemi örneğinden sağlar.
4. Aşağıdaki kodu toohello hello eklemek **OnCreate** hello sonra yöntemi **MobileServiceClient** oluşturulur:
   
       // Set hello current instance of TodoActivity.
       instance = this;
   
       // Make sure hello GCM client is set up correctly.
       GcmClient.CheckDevice(this);
       GcmClient.CheckManifest(this);
   
       // Register hello app for push notifications.
       GcmClient.Register(this, ToDoBroadcastReceiver.senderIDs);

**ToDoActivity** anında iletme bildirimleri eklemek için şimdi hazırlanır.

