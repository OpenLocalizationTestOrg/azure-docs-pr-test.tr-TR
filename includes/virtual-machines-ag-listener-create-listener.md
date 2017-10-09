Bu adımda, yük devretme kümesi Yöneticisi'ni ve SQL Server Management Studio hello kullanılabilirlik grubu dinleyicisi el ile oluşturun.

1. Hello birincil çoğaltmayı barındıran hello düğümden diğerine yük devretme kümesi Yöneticisi'ni açın.

2. Select hello **ağlar** düğümü ve Not hello küme ağ adı. Bu ad hello PowerShell Betiği hello $ClusterNetworkName değişkeni kullanılır.

3. Merhaba küme adını genişletin ve ardından **rolleri**.

4. Merhaba, **rolleri** bölmesi, sağ hello kullanılabilirlik grubu adını ve ardından **kaynak ekleme** > **istemci erişim noktası**.
   
    ![Kullanılabilirlik grubu için istemci erişim noktası Ekle](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678769.gif)

5. Merhaba, **adı** kutusunda, bu yeni dinleyici için bir ad oluşturun, **sonraki** iki kez tıkladıktan sonra **son**.  
    Merhaba dinleyicisi veya kaynağı çevrimiçi bu noktada Getir değil.

6. Merhaba tıklatın **kaynakları** sekmesini tıklatın ve ardından yeni oluşturduğunuz hello istemci erişim noktası genişletin. 
    Başlangıç IP adresi kaynağı, kümedeki her bir küme ağı için görüntülenir. Bu yalnızca Azure çözümünü ise, yalnızca bir IP adresi kaynak görüntülenir.

7. Merhaba aşağıdakilerden birini yapın:
   
   * karma bir çözüm tooconfigure:
     
        a. Tooyour şirket içi alt karşılık gelen başlangıç IP adresi kaynağı sağ tıklayın ve ardından **özellikleri**. Başlangıç IP adresi adı ve ağ adını not edin.
   
        b. Seçin **statik IP adresi**, kullanılmayan bir IP adresi atayın ve ardından **Tamam**.
 
   * yalnızca Azure çözümünü tooconfigure:

        a. Tooyour Azure alt ağa karşılık gelen başlangıç IP adresi kaynağı sağ tıklayın ve ardından **özellikleri**.
       
       > [!NOTE]
       > Merhaba dinleyicisi DHCP tarafından seçilen bir IP adresi nedeniyle çevrimiçi toocome daha sonra başarısız olursa, bu Özellikler penceresinde geçerli bir statik IP adresi yapılandırabilirsiniz.
       > 
       > 

       b. İçinde aynı hello **IP adresi** Özellikleri penceresinde, değişiklik hello **IP adresi adı**.  
        Bu ad hello PowerShell Betiği hello $IPResourceName değişkeninde kullanılır. Çözümünüzün birden fazla Azure sanal ağı yayılırsa, her IP kaynağı için bu adımı yineleyin.

