
1. <span data-ttu-id="115d7-101">Çözüm görünümünde (veya **Çözüm Gezgini** Visual Studio'da), sağ tıklatın **bileşenleri** klasörünü tıklatın **daha almak bileşenleri...** , arama **Google Cloud Messaging istemcisi** bileşeni ve bunu projeye ekleyin.</span><span class="sxs-lookup"><span data-stu-id="115d7-101">In the Solution view (or **Solution Explorer** in Visual Studio), right-click the **Components** folder, click  **Get More Components...**, search for the **Google Cloud Messaging Client** component and add it to the project.</span></span>
2. <span data-ttu-id="115d7-102">ToDoActivity.cs proje dosyasını açın ve aşağıdakileri ekleyin sınıfı deyimiyle:</span><span class="sxs-lookup"><span data-stu-id="115d7-102">Open the ToDoActivity.cs project file and add the following using statement to the class:</span></span>
   
        using Gcm.Client;
3. <span data-ttu-id="115d7-103">İçinde **ToDoActivity** sınıfında, aşağıdaki yeni kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="115d7-103">In the **ToDoActivity** class, add the following new code:</span></span> 
   
        // Create a new instance field for this activity.
        static ToDoActivity instance = new ToDoActivity();
   
        // Return the current activity instance.
        public static ToDoActivity CurrentActivity
        {
            get
            {
                return instance;
            }
        }
        // Return the Mobile Services client.
        public MobileServiceClient CurrentClient
        {
            get
            {
                return client;
            }
        }
   
    <span data-ttu-id="115d7-104">Bu, mobil istemci örneği itme işleyici hizmeti işleminin erişmenize olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="115d7-104">This enables you to access the mobile client instance from the push handler service process.</span></span>
4. <span data-ttu-id="115d7-105">Aşağıdaki kodu ekleyin **OnCreate** yöntemi, sonra **MobileServiceClient** oluşturulur:</span><span class="sxs-lookup"><span data-stu-id="115d7-105">Add the following code to the **OnCreate** method, after the **MobileServiceClient** is created:</span></span>
   
       // Set the current instance of TodoActivity.
       instance = this;
   
       // Make sure the GCM client is set up correctly.
       GcmClient.CheckDevice(this);
       GcmClient.CheckManifest(this);
   
       // Register the app for push notifications.
       GcmClient.Register(this, ToDoBroadcastReceiver.senderIDs);

<span data-ttu-id="115d7-106">**ToDoActivity** anında iletme bildirimleri eklemek için şimdi hazırlanır.</span><span class="sxs-lookup"><span data-stu-id="115d7-106">Your **ToDoActivity** is now prepared for adding push notifications.</span></span>

