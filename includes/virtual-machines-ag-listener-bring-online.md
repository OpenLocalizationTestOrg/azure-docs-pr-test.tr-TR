1. Yük Devretme Kümesi Yöneticisi'nde **rolleri**ve ardından, kullanılabilirlik grubunu vurgulayın.  

2. Merhaba üzerinde **kaynakları** sekmesinde hello dinleyici adına sağ tıklayın ve ardından **özellikleri**.

3. Merhaba tıklatın **bağımlılıkları** sekmesi. Birden fazla kaynak listelenmiyorsa, hello IP adreslerini veya değil olduğunu doğrulayın ve, bağımlılıkları.  

4. **Tamam** düğmesine tıklayın.

5. Merhaba dinleyici adına sağ tıklayın ve ardından **çevrimiçine**.

6. Merhaba sonra dinleyicisi hello üzerinde çevrimiçi **kaynakları** sekmesinde hello kullanılabilirlik grubuna sağ tıklayın ve ardından **özellikleri**.
   
    ![Merhaba kullanılabilirlik grubu kaynağını Yapılandır](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678772.gif)

7. Bir bağımlılık hello dinleyici adı kaynakta (Merhaba IP adresi kaynakları adı değil) oluşturun ve ardından **Tamam**.
   
    ![Merhaba dinleyici adına bağımlılık Ekle](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678773.gif)

8. SQL Server Management Studio'yu başlatın ve sonra toohello birincil çoğaltma bağlanın.

9. Çok Git**AlwaysOn yüksek kullanılabilirlik** > **kullanılabilirlik grupları** > **\<AvailabilityGroupName\>**   >  **Kullanılabilirlik grubu dinleyicileri**.  
    Yük Devretme Kümesi Yöneticisi'nde oluşturulan hello dinleyici adı görüntülenmesi gerekir.

10. Merhaba dinleyici adına sağ tıklayın ve ardından **özellikleri**.

11. Merhaba, **bağlantı noktası** kutusunda, daha önce kullanılan $EndpointPort hello kullanarak hello hello kullanılabilirlik grubu dinleyicisinin bağlantı noktası numarası belirtin (Bu öğreticide, hello varsayılan 1433 olduğu) ve ardından **Tamam**.

