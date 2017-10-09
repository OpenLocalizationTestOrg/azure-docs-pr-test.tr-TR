> [!IMPORTANT]
> <span data-ttu-id="989fc-101">tooreceive Mobile Engagement anında iletme bildirimleri, gereksinim duyduğunuz tooenable `Silent Remote Notifications` uygulamanızda.</span><span class="sxs-lookup"><span data-stu-id="989fc-101">tooreceive Push Notifications from Mobile Engagement, you need tooenable `Silent Remote Notifications` in your application.</span></span> <span data-ttu-id="989fc-102">Info.plist dosyanızdaki tooadd hello uzaktan bildirim değeri toohello Uıbackgroundmodes dizisine gerekir.</span><span class="sxs-lookup"><span data-stu-id="989fc-102">You need tooadd hello remote-notification value toohello UIBackgroundModes array in your Info.plist file.</span></span>
> 
> 

1. <span data-ttu-id="989fc-103">Açık `info.plist` hello proje dosyasında</span><span class="sxs-lookup"><span data-stu-id="989fc-103">Open `info.plist` file in hello project</span></span>
2. <span data-ttu-id="989fc-104">Merhaba listesindeki hello üst öğeyi sağ tıklayın (`Information Property List`) ve yeni satır Ekle</span><span class="sxs-lookup"><span data-stu-id="989fc-104">Right click on hello top item in hello list (`Information Property List`) and add a new row</span></span>
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push1.png)
3. <span data-ttu-id="989fc-105">Yeni satır Hello girin`Required background modes`</span><span class="sxs-lookup"><span data-stu-id="989fc-105">In hello new row enter `Required background modes`</span></span>
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push2.png)
4. <span data-ttu-id="989fc-106">Merhaba sol ok tooexpand hello satırına tıklayın</span><span class="sxs-lookup"><span data-stu-id="989fc-106">Click on hello left arrow tooexpand hello row</span></span>
5. <span data-ttu-id="989fc-107">Değer toohello öğeyi 0 izleyen hello ekleme`App downloads content in response toopush notifications`</span><span class="sxs-lookup"><span data-stu-id="989fc-107">Add hello following value toohello item 0 `App downloads content in response toopush notifications`</span></span>
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push3.png)
6. <span data-ttu-id="989fc-108">Merhaba değişiklik yaptıktan sonra XML aşağıdaki hello içermelidir hello info.plist anahtar ve değer:</span><span class="sxs-lookup"><span data-stu-id="989fc-108">Once you make hello change, hello info.plist XML should contain hello following key and value:</span></span>
   
        <key>UIBackgroundModes</key>
        <array>
        <string>remote-notification</string>
        </array>
7. <span data-ttu-id="989fc-109">**Xcode 7 +** ve **iOS 9 +** kullanıyorsanız:</span><span class="sxs-lookup"><span data-stu-id="989fc-109">If you are using **Xcode 7+** and **iOS 9+**:</span></span>
   
   * <span data-ttu-id="989fc-110">**Anında İletme Bildirimleri**’ni Hedefler > Hedef Adınız > Özellikler’de etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="989fc-110">Enable **Push Notifications** in Targets > Your Target Name > Capabilities.</span></span>

