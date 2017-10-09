### <a name="prepare-for-a-push-installation-on-a-windows-computer"></a>Bir Windows bilgisayarda göndermeli yüklemesi için hazırlama

1. Merhaba Windows bilgisayar ve hello işlem sunucusu arasında ağ bağlantısı olduğundan emin olun.
2. Bu hello işlem sunucusu tooaccess hello bilgisayar kullanabilir bir hesap oluşturun. Merhaba hesabı yönetici hakları (yerel veya etki alanı) olması gerekir. (Yalnızca hello göndermeli yüklemesi için ve aracı güncelleştirmeleri için bu hesabı kullanın.)

   > [!NOTE]
   > Bir etki alanı hesabı kullanmıyorsanız hello yerel bilgisayarda Uzak kullanıcı erişim denetimi devre dışı bırakın. toodisable uzak kullanıcı erişim denetimi, hello HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System kayıt defteri anahtarı altında yeni bir DWORD değeri ekleyin: **LocalAccountTokenFilterPolicy**. Merhaba değeri çok ayarlayın**1**. toodo şu anda bir komut isteminde, hello aşağıdaki komutu çalıştırın:  
   `REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1`
   >
   >
2. Tooprotect, select istediğiniz hello bilgisayardaki Windows Güvenlik Duvarı'nda **bir uygulama veya özelliğin güvenlik duvarı aracılığıyla izin**. Etkinleştirme **dosya ve Yazıcı Paylaşımı** ve **Windows Yönetim Araçları (WMI)**. Tooa etki alanına ait bilgisayarlar için Grup İlkesi nesnesi (GPO) kullanarak hello güvenlik duvarı ayarlarını yapılandırabilirsiniz.

   ![Güvenlik duvarı ayarları](./media/site-recovery-prepare-push-install-mob-svc-win/mobility1.png)

3. CSPSConfigtool içinde oluşturulan hello hesabını ekleyin.
    1.  Tooyour yapılandırma sunucusunda oturum açın.
    2.  **cspsconfigtool.exe** dosyasını açın. (Merhaba masaüstünde ve hello %ProgramData%\home\svsystems\bin klasöründeki bir kısayol olarak bulunur.)
    3.  Merhaba üzerinde **hesaplarını yönetme** sekmesine **hesabı Ekle**.
    4.  Oluşturduğunuz hello hesabı ekleyin.
    5.  Bir bilgisayar için çoğaltma etkinleştirdiğinizde, kullandığınız hello kimlik bilgilerini girin.
