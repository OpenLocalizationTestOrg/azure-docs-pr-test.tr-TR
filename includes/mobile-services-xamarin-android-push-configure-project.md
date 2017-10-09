
1. <span data-ttu-id="dc3ab-101">Hello çözüm görünümü içinde (veya **Çözüm Gezgini** Visual Studio'da), sağ hello **bileşenleri** klasörünü tıklatın **daha almak bileşenleri...** , hello Ara **Google Cloud Messaging istemcisi** bileşeni ve toohello proje ekleyin.</span><span class="sxs-lookup"><span data-stu-id="dc3ab-101">In hello Solution view (or **Solution Explorer** in Visual Studio), right-click hello **Components** folder, click  **Get More Components...**, search for hello **Google Cloud Messaging Client** component and add it toohello project.</span></span>
2. <span data-ttu-id="dc3ab-102">Merhaba ToDoActivity.cs proje dosyasını açın ve hello aşağıdakileri ekleyin deyimi toohello sınıfını kullanarak:</span><span class="sxs-lookup"><span data-stu-id="dc3ab-102">Open hello ToDoActivity.cs project file and add hello following using statement toohello class:</span></span>
   
        using Gcm.Client;
3. <span data-ttu-id="dc3ab-103">Merhaba, **ToDoActivity** sınıfı, yeni kod aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="dc3ab-103">In hello **ToDoActivity** class, add hello following new code:</span></span> 
   
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
   
    <span data-ttu-id="dc3ab-104">Bu, tooaccess hello mobil istemci hello itme işleyici hizmet işlemi örneğinden sağlar.</span><span class="sxs-lookup"><span data-stu-id="dc3ab-104">This enables you tooaccess hello mobile client instance from hello push handler service process.</span></span>
4. <span data-ttu-id="dc3ab-105">Aşağıdaki kodu toohello hello eklemek **OnCreate** hello sonra yöntemi **MobileServiceClient** oluşturulur:</span><span class="sxs-lookup"><span data-stu-id="dc3ab-105">Add hello following code toohello **OnCreate** method, after hello **MobileServiceClient** is created:</span></span>
   
       // Set hello current instance of TodoActivity.
       instance = this;
   
       // Make sure hello GCM client is set up correctly.
       GcmClient.CheckDevice(this);
       GcmClient.CheckManifest(this);
   
       // Register hello app for push notifications.
       GcmClient.Register(this, ToDoBroadcastReceiver.senderIDs);

<span data-ttu-id="dc3ab-106">**ToDoActivity** anında iletme bildirimleri eklemek için şimdi hazırlanır.</span><span class="sxs-lookup"><span data-stu-id="dc3ab-106">Your **ToDoActivity** is now prepared for adding push notifications.</span></span>

