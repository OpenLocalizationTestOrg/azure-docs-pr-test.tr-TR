
1. <span data-ttu-id="be349-101">İçinde **karma bağlantılar** dikey penceresinde, oluşturulan, ardından yeni karma bağlantıyı tıklatarak **dinleyicisi Kur**.</span><span class="sxs-lookup"><span data-stu-id="be349-101">In the **Hybrid connections** blade, click the hybrid connection you just created, then click **Listener Setup**.</span></span>
   
    ![Dinleyici Kur'a tıklayın](./media/app-service-hybrid-connections-manager-install/D04ClickListenerSetup.png)
2. <span data-ttu-id="be349-103">**Karma bağlantı özelliklerini** dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="be349-103">The **Hybrid connection properties** blade opens.</span></span> <span data-ttu-id="be349-104">Altında **şirket içi karma Bağlantı Yöneticisi**, seçin **indirme ve el ile yapılandırma**indirilen HybridConnectionManager.msi paketi kaydedin ve ağ geçidi bağlantı dizesini kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="be349-104">Under **On-premises Hybrid Connection Manager**, choose **download and configure manually**, save the downloaded HybridConnectionManager.msi package, and copy the gateway connection string.</span></span>
   
    ![Yüklemek için burayı tıklatın](./media/app-service-hybrid-connections-manager-install/D05ClickToInstallHCM.png)
3. <span data-ttu-id="be349-106">Bir yönetici komut isteminden yükleyiciyi başlatmak için aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="be349-106">From an administrator command prompt, type the following command to start the installer:</span></span>
   
        start HybridConnectionManager.msi
4. <span data-ttu-id="be349-107">Yükleyici çalıştıktan sonra tıklatın **şimdi değil**, %ProgramFiles%\Microsoft\HybridConnectionManager klasöre göz atın, HCMConfigWizard.exe çalıştırın ve tıklatın **Evet** içinde **kullanıcı hesabı Denetim** iletişim.</span><span class="sxs-lookup"><span data-stu-id="be349-107">After the installer runs, click **Not now**, then browse to the %ProgramFiles%\Microsoft\HybridConnectionManager folder, run HCMConfigWizard.exe and click **Yes** in the **User Account Control** dialog.</span></span>
5. <span data-ttu-id="be349-108">Daha önce kopyaladığınız karma bağlantı dizesini yapıştırın ve tıklayın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="be349-108">Paste the hybrid connection string that you copied earlier and click **OK**.</span></span> 
   
    ![Yükleme](./media/app-service-hybrid-connections-manager-install/D08aHCMInstallManual.png)
6. <span data-ttu-id="be349-110">Yükleme tamamlandığında tıklayın **Kapat**.</span><span class="sxs-lookup"><span data-stu-id="be349-110">When the install completes, click **Close**.</span></span>
   
    ![Kapat'ı tıklatın](./media/app-service-hybrid-connections-manager-install/D09HCMInstallComplete.png)
   
    <span data-ttu-id="be349-112">Üzerinde **karma bağlantılar** dikey penceresinde **durum** sütun şimdi gösterir **bağlı**.</span><span class="sxs-lookup"><span data-stu-id="be349-112">On the **Hybrid connections** blade, the **Status** column now shows **Connected**.</span></span> 
   
    ![Bağlı durumu](./media/app-service-hybrid-connections-manager-install/D10HCStatusConnected.png)

