1. <span data-ttu-id="bbff1-101">Yük Devretme Kümesi Yöneticisi'nde **rolleri**ve ardından, kullanılabilirlik grubunu vurgulayın.</span><span class="sxs-lookup"><span data-stu-id="bbff1-101">In Failover Cluster Manager, expand **Roles**, and then highlight your availability group.</span></span>  

2. <span data-ttu-id="bbff1-102">Üzerinde **kaynakları** sekmesinde dinleyici adına sağ tıklayın ve ardından **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="bbff1-102">On the **Resources** tab, right-click the listener name, and then click **Properties**.</span></span>

3. <span data-ttu-id="bbff1-103">Tıklatın **bağımlılıkları** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="bbff1-103">Click the **Dependencies** tab.</span></span> <span data-ttu-id="bbff1-104">Birden fazla kaynak listelenmiyorsa, IP adreslerini veya değil olduğunu doğrulayın ve, bağımlılıkları.</span><span class="sxs-lookup"><span data-stu-id="bbff1-104">If multiple resources are listed, verify that the IP addresses have OR, not AND, dependencies.</span></span>  

4. <span data-ttu-id="bbff1-105">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bbff1-105">Click **OK**.</span></span>

5. <span data-ttu-id="bbff1-106">Dinleyici adına sağ tıklayın ve ardından **çevrimiçine**.</span><span class="sxs-lookup"><span data-stu-id="bbff1-106">Right-click the listener name, and then click **Bring Online**.</span></span>

6. <span data-ttu-id="bbff1-107">Dinleyici üzerinde çevrimiçi olduktan sonra **kaynakları** sekmesinde, kullanılabilirlik grubunu sağ tıklatın ve ardından **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="bbff1-107">After the listener is online, on the **Resources** tab, right-click the availability group, and then click **Properties**.</span></span>
   
    ![Kullanılabilirlik grubu kaynağını Yapılandır](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678772.gif)

7. <span data-ttu-id="bbff1-109">(IP adresi kaynakları adı değil) dinleyici adı kaynağına bağlı bir bağımlılık oluşturun ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="bbff1-109">Create a dependency on the listener name resource (not the IP address resources name), and then click **OK**.</span></span>
   
    ![Dinleyici adına bağımlılık Ekle](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678773.gif)

8. <span data-ttu-id="bbff1-111">SQL Server Management Studio'yu açın ve ardından birincil kopyaya bağlanın.</span><span class="sxs-lookup"><span data-stu-id="bbff1-111">Start SQL Server Management Studio, and then connect to the primary replica.</span></span>

9. <span data-ttu-id="bbff1-112">Git **AlwaysOn yüksek kullanılabilirlik** > **kullanılabilirlik grupları** > **\<AvailabilityGroupName\>**   >  **Kullanılabilirlik grubu dinleyicileri**.</span><span class="sxs-lookup"><span data-stu-id="bbff1-112">Go to **AlwaysOn High Availability** > **Availability Groups** > **\<AvailabilityGroupName\>** > **Availability Group Listeners**.</span></span>  
    <span data-ttu-id="bbff1-113">Yük Devretme Kümesi Yöneticisi'nde oluşturulan dinleyici adı görüntülenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="bbff1-113">The listener name that you created in Failover Cluster Manager should be displayed.</span></span>

10. <span data-ttu-id="bbff1-114">Dinleyici adına sağ tıklayın ve ardından **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="bbff1-114">Right-click the listener name, and then click **Properties**.</span></span>

11. <span data-ttu-id="bbff1-115">İçinde **bağlantı noktası** kutusunda, daha önce kullanılan $EndpointPort kullanarak için kullanılabilirlik grubu dinleyicisinin bağlantı noktası numarası belirtin (Bu öğreticide, varsayılan 1433 olduğu) ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="bbff1-115">In the **Port** box, specify the port number for the availability group listener by using the $EndpointPort that you used earlier (in this tutorial, 1433 was the default), and then click **OK**.</span></span>

