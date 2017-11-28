<!--author=alkohli last changed: 01/13/17-->

<span data-ttu-id="4bea0-101">Birim kapsayıcısı birimleri ilişkili varsa bu birimlerin çevrimdışı ilk alın.</span><span class="sxs-lookup"><span data-stu-id="4bea0-101">If the volume container has associated volumes, take those volumes offline first.</span></span> <span data-ttu-id="4bea0-102">Adımları [bir birim çevrimdışına](../articles/storsimple/storsimple-manage-volumes.md#take-a-volume-offline).</span><span class="sxs-lookup"><span data-stu-id="4bea0-102">Follow the steps in [Take a volume offline](../articles/storsimple/storsimple-manage-volumes.md#take-a-volume-offline).</span></span> <span data-ttu-id="4bea0-103">Birimleri çevrimdışı olduktan sonra bunları silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4bea0-103">After the volumes are offline, you can delete them.</span></span> <span data-ttu-id="4bea0-104">Birim kapsayıcısı ilişkili birim olduğunda, birim kapsayıcısı silin.</span><span class="sxs-lookup"><span data-stu-id="4bea0-104">When the volume container has no associated volumes, delete the volume container.</span></span> <span data-ttu-id="4bea0-105">Birim kapsayıcısı silmek için aşağıdaki yordamı gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="4bea0-105">Perform the following procedure to delete a volume container.</span></span>

#### <a name="to-delete-a-volume-container"></a><span data-ttu-id="4bea0-106">Birim kapsayıcısı silmek için</span><span class="sxs-lookup"><span data-stu-id="4bea0-106">To delete a volume container</span></span>
1. <span data-ttu-id="4bea0-107">StorSimple Cihaz Yöneticisi hizmetinize gidin ve **Cihazlar**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4bea0-107">Go to your StorSimple Device Manager service and click **Devices**.</span></span> <span data-ttu-id="4bea0-108">Seçin ve aygıtı tıklatın ve ardından gidin **ayarlar > Yönet > birim kapsayıcıları**.</span><span class="sxs-lookup"><span data-stu-id="4bea0-108">Select and click the device and then go to **Settings > Manage > Volume containers**.</span></span>

    ![Birim kapsayıcıları dikey penceresi](./media/storsimple-8000-create-volume-container/createvolumecontainer2.png)

2. <span data-ttu-id="4bea0-110">Birim kapsayıcıları Tablo listesinden silmek için sağ tıklayın, istediğiniz birim kapsayıcısı seçin **...**  ve ardından **silmek**.</span><span class="sxs-lookup"><span data-stu-id="4bea0-110">From the tabular list of volume containers, select the volume container you want to delete, right click **...** and then select **Delete**.</span></span>

    ![Birim kapsayıcısı Sil](./media/storsimple-8000-delete-volume-container/deletevolumecontainer1.png)

3. <span data-ttu-id="4bea0-112">Birim kapsayıcısı ilişkili birim varsa, silinebilir.</span><span class="sxs-lookup"><span data-stu-id="4bea0-112">If a volume container has no associated volumes, then it can be deleted.</span></span> <span data-ttu-id="4bea0-113">Onayınız istendiğinde gözden geçirin ve birim kapsayıcısı silme etkisini belirten onay kutusunu seçin.</span><span class="sxs-lookup"><span data-stu-id="4bea0-113">When prompted for confirmation, review and select the checkbox stating the impact of deleting the volume container.</span></span> <span data-ttu-id="4bea0-114">Tıklatın **silmek** birim kapsayıcısı silmek için.</span><span class="sxs-lookup"><span data-stu-id="4bea0-114">Click **Delete** to then delete the volume container.</span></span>

    ![Silme işlemini onaylama](./media/storsimple-8000-delete-volume-container/deletevolumecontainer2.png)

<span data-ttu-id="4bea0-116">Birim kapsayıcıları listesi silinen birim kapsayıcısı yansıtacak şekilde güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="4bea0-116">The list of volume containers is updated to reflect the deleted volume container.</span></span>

![](./media/storsimple-8000-delete-volume-container/deletevolumecontainer5.png)


