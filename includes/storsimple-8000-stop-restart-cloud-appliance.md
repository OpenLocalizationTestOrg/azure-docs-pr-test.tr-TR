#### <a name="toostop-and-start-a-cloud-appliance"></a>toostop ve başlangıç bulut uygulaması

1. toostop bulut uygulaması toohello VM bulut uygulaması için gidin.
    ![StorSimple Cloud Appliance Sanal Makinesi](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart1.png)

2. Merhaba Komut çubuğundaki **durdurmak**.

    ![StorSimple Cloud Appliance Sanal Makinesi](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart2.png)

3. Onayınız istendiğinde **Evet**’e tıklayın.

    ![StorSimple Cloud Appliance Sanal Makinesi](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart3.png)

4. Bir VM durdurulduğunda serbest bırakılır. Merhaba bulut uygulaması durdurma olsa da, durumundadır **Deallocating**. Merhaba bulut uygulaması durdurulduktan sonra durumundadır **durduruldu (serbest bırakıldı)**.

    ![StorSimple Cloud Appliance Sanal Makinesi](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart4.png)

5. Bir VM durdurulduğunda tıklatın **Başlat** (düğmesi kullanılabilir olur) toostart hello VM. Merhaba bulut uygulaması başladıktan sonra durumundadır **başlatıldı**.

    ![StorSimple Cloud Appliance Sanal Makinesi](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart5.png)

Cmdlet'leri toostop aşağıdaki hello kullanın ve bulut uygulaması başlatın.

`Stop-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

`Start-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

#### <a name="toorestart-a-cloud-appliance"></a>toorestart bulut uygulaması

toorestart bulut uygulaması toohello VM bulut uygulaması için gidin. Merhaba Komut çubuğundaki **yeniden**. İstendiğinde, hello yeniden onaylayın. Merhaba bulut uygulaması, toouse hazır olduğunda, durumundadır **çalıştıran**.

![StorSimple Cloud Appliance Sanal Makinesi](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart6.png)

Cmdlet toorestart bulut uygulaması aşağıdaki hello kullanın.

`Restart-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

