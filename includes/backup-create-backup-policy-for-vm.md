## <a name="defining-a-backup-policy"></a>Yedekleme ilkesi tanımlama
Bir yedekleme İlkesi zaman hello veri anlık görüntülerinin alınma ve bu anlık görüntülerin ne kadar süreyle saklanacağını bir matrisini tanımlar. VM yedeklemesi için bir ilke tanımlandığında, yedekleme işini *günde bir kez* tetikleyebilirsiniz. Yeni bir ilke oluşturduğunuzda, uygulanan toohello kasası olur. Merhaba yedekleme İlkesi arabirimi şöyle görünür:

![Yedekleme ilkesi](./media/backup-create-policy-for-vms/backup-policy.png)

bir ilke toocreate:

1. Hello için bir ad girin **ilke adı**.
2. Verilerinizin anlık görüntüleri Günlük veya Haftalık aralıklarla alınabilir. Kullanım hello **yedekleme sıklığı** açılır menü toochoose olup veri anlık görüntülerinin günlük mü, yoksa haftalık.
   
   * Günlük bir aralık seçin, vurgulanmış hello denetim tooselect hello hello günün saatini hello anlık görüntü için kullanın. toochange hello saat hello saat seçimini kaldırıp hello yeni saati seçin.
     
     ![Günlük yedekleme ilkesi](./media/backup-create-policy-for-vms/backup-policy-daily.png) <br/>
   * Haftalık aralığını seçerseniz, hello vurgulanan denetimleri tooselect hello gün hello haftanın ve hello saat gün tootake hello anlık görüntüsünün kullanın. Merhaba gün menüsünde, bir veya birden çok gün seçin. Merhaba saat menüsünde bir saat seçin. toochange hello saat hello seçili saatin seçimini ve hello yeni saati seçin.
     
     ![Haftalık yedekleme ilkesi](./media/backup-create-policy-for-vms/backup-policy-weekly.png)
3. Varsayılan olarak, tüm **Elde Tutma Aralığı** seçenekleri seçilidir. Toouse istemediğiniz tüm bekletme aralığı sınırının seçimini kaldırın. Ardından, hello aralıkları toouse belirtin.
   
    Aylık ve yıllık elde tutma aralıkları günlük veya haftalık artışı temel toospecify hello anlık görüntüleri izin verin.
   
   > [!NOTE]
   > VM korurken yedekleme işi günde bir kez çalıştırılır. Merhaba zaman zaman hello yedekleme çalıştırılana olduğu hello aynı her elde tutma aralığı için.
   > 
   > 
4. Hello ilkesi için tüm seçenekleri ayarladıktan sonra hello dikey penceresinde hello üstünde tıklatın **kaydetmek**.
   
    Merhaba yeni ilke hemen uygulanan toohello kasası olur.

