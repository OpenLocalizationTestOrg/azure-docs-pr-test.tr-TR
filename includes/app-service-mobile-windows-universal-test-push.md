
1. <span data-ttu-id="f2118-101">Windows mağazası projesine sağ tıklayın, **başlangıç projesi olarak ayarla**, Windows mağazası uygulamasını çalıştırmak için F5 tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="f2118-101">Right-click the Windows Store project, click **Set as StartUp Project**, then press the F5 key to run the Windows Store app.</span></span>
   
    <span data-ttu-id="f2118-102">Uygulama başlatıldıktan sonra cihazın anında iletme bildirimleri için kayıtlı.</span><span class="sxs-lookup"><span data-stu-id="f2118-102">After the app starts, the device is registered for push notifications.</span></span>
2. <span data-ttu-id="f2118-103">Windows mağazası uygulaması durdurun ve Windows Phone mağazası uygulaması için önceki adımı yineleyin.</span><span class="sxs-lookup"><span data-stu-id="f2118-103">Stop the Windows Store app and repeat the previous step for the Windows Phone Store app.</span></span>
   
    <span data-ttu-id="f2118-104">Bu noktada, her iki anında iletme bildirimleri almak için kaydedilen aygıtlar.</span><span class="sxs-lookup"><span data-stu-id="f2118-104">At this point, both devices are registered to receive push notifications.</span></span>
3. <span data-ttu-id="f2118-105">Windows mağazası uygulamasını yeniden çalıştırın ve yazın metinde **Todoıtem Ekle**ve ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="f2118-105">Run the Windows Store app again, and type text in **Insert a TodoItem**, and then click **Save**.</span></span>
   
       Note that after the insert completes, both the Windows Store and the Windows Phone apps receive a push notification from WNS. The notification is displayed on Windows Phone even when the app isn't running.
   
       ![](./media/app-service-mobile-windows-universal-test-push/mobile-quickstart-push5-wp8.png)

