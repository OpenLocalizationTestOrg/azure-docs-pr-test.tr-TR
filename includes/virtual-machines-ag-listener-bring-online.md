1. <span data-ttu-id="75892-101">Yük Devretme Kümesi Yöneticisi'nde **rolleri**ve ardından, kullanılabilirlik grubunu vurgulayın.</span><span class="sxs-lookup"><span data-stu-id="75892-101">In Failover Cluster Manager, expand **Roles**, and then highlight your availability group.</span></span>  

2. <span data-ttu-id="75892-102">Merhaba üzerinde **kaynakları** sekmesinde hello dinleyici adına sağ tıklayın ve ardından **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="75892-102">On hello **Resources** tab, right-click hello listener name, and then click **Properties**.</span></span>

3. <span data-ttu-id="75892-103">Merhaba tıklatın **bağımlılıkları** sekmesi. Birden fazla kaynak listelenmiyorsa, hello IP adreslerini veya değil olduğunu doğrulayın ve, bağımlılıkları.</span><span class="sxs-lookup"><span data-stu-id="75892-103">Click hello **Dependencies** tab. If multiple resources are listed, verify that hello IP addresses have OR, not AND, dependencies.</span></span>  

4. <span data-ttu-id="75892-104">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="75892-104">Click **OK**.</span></span>

5. <span data-ttu-id="75892-105">Merhaba dinleyici adına sağ tıklayın ve ardından **çevrimiçine**.</span><span class="sxs-lookup"><span data-stu-id="75892-105">Right-click hello listener name, and then click **Bring Online**.</span></span>

6. <span data-ttu-id="75892-106">Merhaba sonra dinleyicisi hello üzerinde çevrimiçi **kaynakları** sekmesinde hello kullanılabilirlik grubuna sağ tıklayın ve ardından **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="75892-106">After hello listener is online, on hello **Resources** tab, right-click hello availability group, and then click **Properties**.</span></span>
   
    ![Merhaba kullanılabilirlik grubu kaynağını Yapılandır](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678772.gif)

7. <span data-ttu-id="75892-108">Bir bağımlılık hello dinleyici adı kaynakta (Merhaba IP adresi kaynakları adı değil) oluşturun ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="75892-108">Create a dependency on hello listener name resource (not hello IP address resources name), and then click **OK**.</span></span>
   
    ![Merhaba dinleyici adına bağımlılık Ekle](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678773.gif)

8. <span data-ttu-id="75892-110">SQL Server Management Studio'yu başlatın ve sonra toohello birincil çoğaltma bağlanın.</span><span class="sxs-lookup"><span data-stu-id="75892-110">Start SQL Server Management Studio, and then connect toohello primary replica.</span></span>

9. <span data-ttu-id="75892-111">Çok Git**AlwaysOn yüksek kullanılabilirlik** > **kullanılabilirlik grupları** > **\<AvailabilityGroupName\>**   >  **Kullanılabilirlik grubu dinleyicileri**.</span><span class="sxs-lookup"><span data-stu-id="75892-111">Go too**AlwaysOn High Availability** > **Availability Groups** > **\<AvailabilityGroupName\>** > **Availability Group Listeners**.</span></span>  
    <span data-ttu-id="75892-112">Yük Devretme Kümesi Yöneticisi'nde oluşturulan hello dinleyici adı görüntülenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="75892-112">hello listener name that you created in Failover Cluster Manager should be displayed.</span></span>

10. <span data-ttu-id="75892-113">Merhaba dinleyici adına sağ tıklayın ve ardından **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="75892-113">Right-click hello listener name, and then click **Properties**.</span></span>

11. <span data-ttu-id="75892-114">Merhaba, **bağlantı noktası** kutusunda, daha önce kullanılan $EndpointPort hello kullanarak hello hello kullanılabilirlik grubu dinleyicisinin bağlantı noktası numarası belirtin (Bu öğreticide, hello varsayılan 1433 olduğu) ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="75892-114">In hello **Port** box, specify hello port number for hello availability group listener by using hello $EndpointPort that you used earlier (in this tutorial, 1433 was hello default), and then click **OK**.</span></span>

