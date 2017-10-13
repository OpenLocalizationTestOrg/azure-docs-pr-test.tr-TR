1. Yük Devretme Kümesi Yöneticisi'nde **rolleri**ve ardından, kullanılabilirlik grubunu vurgulayın.  

2. Üzerinde **kaynakları** sekmesinde dinleyici adına sağ tıklayın ve ardından **özellikleri**.

3. Tıklatın **bağımlılıkları** sekmesi. Birden fazla kaynak listelenmiyorsa, IP adreslerini veya değil olduğunu doğrulayın ve, bağımlılıkları.  

4. **Tamam** düğmesine tıklayın.

5. Dinleyici adına sağ tıklayın ve ardından **çevrimiçine**.

6. Dinleyici üzerinde çevrimiçi olduktan sonra **kaynakları** sekmesinde, kullanılabilirlik grubunu sağ tıklatın ve ardından **özellikleri**.
   
    ![Kullanılabilirlik grubu kaynağını Yapılandır](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678772.gif)

7. (IP adresi kaynakları adı değil) dinleyici adı kaynağına bağlı bir bağımlılık oluşturun ve ardından **Tamam**.
   
    ![Dinleyici adına bağımlılık Ekle](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678773.gif)

8. SQL Server Management Studio'yu açın ve ardından birincil kopyaya bağlanın.

9. Git **AlwaysOn yüksek kullanılabilirlik** > **kullanılabilirlik grupları** > **\<AvailabilityGroupName\>**   >  **Kullanılabilirlik grubu dinleyicileri**.  
    Yük Devretme Kümesi Yöneticisi'nde oluşturulan dinleyici adı görüntülenmesi gerekir.

10. Dinleyici adına sağ tıklayın ve ardından **özellikleri**.

11. İçinde **bağlantı noktası** kutusunda, daha önce kullanılan $EndpointPort kullanarak için kullanılabilirlik grubu dinleyicisinin bağlantı noktası numarası belirtin (Bu öğreticide, varsayılan 1433 olduğu) ve ardından **Tamam**.

