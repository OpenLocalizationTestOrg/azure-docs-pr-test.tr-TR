
1. <span data-ttu-id="6bff8-101">Merhaba, **karma bağlantılar** dikey penceresinde hello karma bağlantı yeni oluşturulan tıklayın ve ardından **dinleyicisi Kur**.</span><span class="sxs-lookup"><span data-stu-id="6bff8-101">In hello **Hybrid connections** blade, click hello hybrid connection you just created, then click **Listener Setup**.</span></span>
   
    ![Dinleyici Kur'a tıklayın](./media/app-service-hybrid-connections-manager-install/D04ClickListenerSetup.png)
2. <span data-ttu-id="6bff8-103">Merhaba **karma bağlantı özelliklerini** dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="6bff8-103">hello **Hybrid connection properties** blade opens.</span></span> <span data-ttu-id="6bff8-104">Altında **şirket içi karma Bağlantı Yöneticisi**, seçin **indirme ve el ile yapılandırma**indirilen hello HybridConnectionManager.msi paketi kaydetmek ve kopyalama hello ağ geçidi bağlantı dizesi.</span><span class="sxs-lookup"><span data-stu-id="6bff8-104">Under **On-premises Hybrid Connection Manager**, choose **download and configure manually**, save hello downloaded HybridConnectionManager.msi package, and copy hello gateway connection string.</span></span>
   
    ![Tooinstall burayı tıklatın](./media/app-service-hybrid-connections-manager-install/D05ClickToInstallHCM.png)
3. <span data-ttu-id="6bff8-106">Bir yönetici komut isteminden komut toostart hello Yükleyici aşağıdaki hello yazın:</span><span class="sxs-lookup"><span data-stu-id="6bff8-106">From an administrator command prompt, type hello following command toostart hello installer:</span></span>
   
        start HybridConnectionManager.msi
4. <span data-ttu-id="6bff8-107">Merhaba sonra yükleyicisini çalıştırır, tıklatın **şimdi değil**, toohello %ProgramFiles%\Microsoft\HybridConnectionManager klasörüne göz atın, HCMConfigWizard.exe çalıştırın ve tıklatın **Evet** hello içinde **kullanıcı Hesap denetim** iletişim.</span><span class="sxs-lookup"><span data-stu-id="6bff8-107">After hello installer runs, click **Not now**, then browse toohello %ProgramFiles%\Microsoft\HybridConnectionManager folder, run HCMConfigWizard.exe and click **Yes** in hello **User Account Control** dialog.</span></span>
5. <span data-ttu-id="6bff8-108">Daha önce kopyaladığınız hello karma bağlantı dizesini yapıştırın ve tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="6bff8-108">Paste hello hybrid connection string that you copied earlier and click **OK**.</span></span> 
   
    ![Yükleme](./media/app-service-hybrid-connections-manager-install/D08aHCMInstallManual.png)
6. <span data-ttu-id="6bff8-110">Merhaba yükleme tamamlandığında tıklayın **Kapat**.</span><span class="sxs-lookup"><span data-stu-id="6bff8-110">When hello install completes, click **Close**.</span></span>
   
    ![Kapat'ı tıklatın](./media/app-service-hybrid-connections-manager-install/D09HCMInstallComplete.png)
   
    <span data-ttu-id="6bff8-112">Merhaba üzerinde **karma bağlantılar** dikey penceresinde, hello **durum** sütun şimdi gösterir **bağlı**.</span><span class="sxs-lookup"><span data-stu-id="6bff8-112">On hello **Hybrid connections** blade, hello **Status** column now shows **Connected**.</span></span> 
   
    ![Bağlı durumu](./media/app-service-hybrid-connections-manager-install/D10HCStatusConnected.png)

