### <a name="determine-hello-dns-name-of-hello-virtual-machine"></a>Merhaba DNS hello sanal makinenin adını belirleme
başka bir bilgisayardan tooconnect toohello SQL Server veritabanı altyapısı, hello etki alanı adı sistemi (DNS) bilmeniz gerekir hello sanal makine adı. (Merhaba adı hello Internet kullanır tooidentify hello sanal makine bulunuyor. Başlangıç IP adresi kullanabilirsiniz, ancak Azure artıklık veya bakım için kaynaklar taşındığında hello IP adresi değişebilir. Bu olabilir çünkü Hello DNS adı kararlı olacaktır tooa yeni IP adresini yeniden yönlendirildi.)  

1. Hello Azure Portal (veya hello önceki adımdaki), seçin **sanal makineleri (Klasik)**.
2. SQL VM’nizi seçin.
3. Merhaba üzerinde **sanal makine** dikey penceresinde, kopyalama hello **DNS adı** hello sanal makine için.
   
    ![DNS adı](./media/virtual-machines-sql-server-connection-steps/sql-vm-dns-name.png)

### <a name="connect-toohello-database-engine-from-another-computer"></a>Başka bir bilgisayardan toohello veritabanına bağlan
1. Bir bilgisayarda toohello bağlı Internet, SQL Server Management Studio'yu açın.
2. Merhaba, **tooServer bağlanmak** veya **tooDatabase altyapısı bağlanmak** iletişim kutusunda hello **sunucu adı** kutusuna, hello sanal makine (hello belirlenen hello DNS adını girin önceki görev) ve bir ortak uç nokta bağlantı noktası numarası hello biçiminde *DNSName, BağlantıNoktasıNumarası* gibi **mysqlvm.cloudapp.net,57500**.
   
    ![SSMS kullanarak bağlanma](./media/virtual-machines-sql-server-connection-steps/33Connect-SSMS.png)
   
    Merhaba ortak uç nokta bağlantı noktası numarasını hatırlamıyorsanız daha önce oluşturduğunuz, hello Bul **uç noktaları** hello alanı **sanal makine** dikey.
   
    ![Genel Bağlantı Noktası](./media/virtual-machines-sql-server-connection-steps/sql-vm-port-number.png)
3. Merhaba, **kimlik doğrulaması** kutusunda **SQL Server kimlik doğrulaması**.
4. Merhaba, **oturum açma** kutusu, bir önceki görevde oluşturduğunuz bir oturum açma türü hello adı.
5. Merhaba, **parola** kutusu, bir önceki görevde oluşturduğunuz hello oturum açma hello parolayı girin.
6. **Bağlan**'a tıklayın.

