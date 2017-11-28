> [!IMPORTANT]
> <span data-ttu-id="7b228-101">Mobile Engagement’tan Anında İletme Bildirimi almak için uygulamanızda `Silent Remote Notifications` etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="7b228-101">To receive Push Notifications from Mobile Engagement, you need to enable `Silent Remote Notifications` in your application.</span></span> <span data-ttu-id="7b228-102">Info.plist dosyanızdaki UIBackgroundModes dizisine uzaktan bildirim değeri eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="7b228-102">You need to add the remote-notification value to the UIBackgroundModes array in your Info.plist file.</span></span>
> 
> 

1. <span data-ttu-id="7b228-103">Projede `info.plist` dosyasını açın</span><span class="sxs-lookup"><span data-stu-id="7b228-103">Open `info.plist` file in the project</span></span>
2. <span data-ttu-id="7b228-104">Listedeki ilk öğeye (`Information Property List`) sağ tıklayın ve yeni bir satır ekleyin</span><span class="sxs-lookup"><span data-stu-id="7b228-104">Right click on the top item in the list (`Information Property List`) and add a new row</span></span>
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push1.png)
3. <span data-ttu-id="7b228-105">Yeni satıra `Required background modes` girin</span><span class="sxs-lookup"><span data-stu-id="7b228-105">In the new row enter `Required background modes`</span></span>
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push2.png)
4. <span data-ttu-id="7b228-106">Satırı genişletmek için sol oka tıklayın</span><span class="sxs-lookup"><span data-stu-id="7b228-106">Click on the left arrow to expand the row</span></span>
5. <span data-ttu-id="7b228-107">0 öğesine şu değeri ekleyin: `App downloads content in response to push notifications`</span><span class="sxs-lookup"><span data-stu-id="7b228-107">Add the following value to the item 0 `App downloads content in response to push notifications`</span></span>
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push3.png)
6. <span data-ttu-id="7b228-108">Değişikliği yaptıktan sonra XML info.plist dosyasında şu anahtar ve değer olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="7b228-108">Once you make the change, the info.plist XML should contain the following key and value:</span></span>
   
        <key>UIBackgroundModes</key>
        <array>
        <string>remote-notification</string>
        </array>
7. <span data-ttu-id="7b228-109">**Xcode 7 +** ve **iOS 9 +** kullanıyorsanız:</span><span class="sxs-lookup"><span data-stu-id="7b228-109">If you are using **Xcode 7+** and **iOS 9+**:</span></span>
   
   * <span data-ttu-id="7b228-110">**Anında İletme Bildirimleri**’ni Hedefler > Hedef Adınız > Özellikler’de etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="7b228-110">Enable **Push Notifications** in Targets > Your Target Name > Capabilities.</span></span>

