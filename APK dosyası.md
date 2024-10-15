import tkinter as tk
from tkinter import simpledialog, messagebox, ttk
import webbrowser
import random
import datetime
import time

class Saat():
    def __init__(self, master):
        self.label = tk.Label(master, font=('calibri', 6, 'bold'), bg='yellow')
        self.label.pack(anchor='nw')
        self.zaman_guncelle()

    def zaman_guncelle(self):
        self.zaman = time.strftime('%H:%M:%S')
        self.label.config(text="canlı saat ; " + self.zaman)
        self.label.after(1000, self.zaman_guncelle)

class Oyuncu:
    def __init__(self):
        self.puan = 30
        self.kalan_hak = 6
        self.tahmin_edilen_harfler = []
        self.oyun_surumu = "1.01.1"  # Sürümü güncelledik
        self.gece_modu = False
        self.toplam_oynama_sayisi = 0
        self.toplam_kazanma_sayisi = 0
        self.toplam_kaybetme_sayisi = 0

    def kelime_sec(self):
        kelimeler = {
            "isimler":[
                ("ronaldo", ["G.O.A.T kim'dir"]),
                ("messi", ["10 numara forma giyen yer cucesi kimdir ayrıca goat diyiyorlar ama aslında goat değildir"]),
                ("Ronaldinho", ["2024 yılında Survivor'a gelen ünlü futbol'cu kim'dir"]),
                ("dario moreno", ["her akşam votka rakı ve şarap şarkısını söyleyen şarkıcı kim'dir"]),
                ("kaká", ["yakışıklı bir futbolcu "]),
                ("turabi", ["survivor'da en sevilen oyun'cu kimdir"]),
             ("ronaldo", ["yakışıklı bir futbolcu"]),
                ("gökkuşağı", ["yağmur ve güneş varsa ortaya ne çıkar"]),
                ("vikings", ["RAGNER LOTHBROK oynadıgı dizi hangisi'dir"]),
                ("futbol", ["popüler bir spor dalı"]),
                ("üç", ["pele'nin kaç tane dünya kupası var'dır"]),
              
                ("hard shelby", ["oyunu tasarlayan kişi kim'dir"]),
                
                ("gri", ["siyah ve beyaz'ın karışı nedir"] ),
                
                ("kivi" , ["bir meyve türü yazınız"]),
                ("Figüran", ["film'lerde yardımcı oyuncu adı nedir"]),
                ("kırmızı lark", ["yasak'lanan bir sigara markası"]),
                ("tablo", ["duvara asılan bir şey yazınız."]),  
                ("doritos", ["bir cips marka'sı giriniz."]),
             ("maserati", ["bir araba marka'sı giriniz."]),
             ("python", ["bu oyun hangi program dilin'de yazılmış'tır."]),
             
             ("fabri", ["beşiktaş'ın en iyi kaleci'si kim'dir"]),
             
             ("mavi", ["sevilen bir renk yazınız"]),
             ("çene", ["insan vücudu'nun en güçlü yeri neresi'dir"]),
             
             ("sema", ["2024 yılın'da diskalifiye edilen kadın yarışmacı"]),
             
             ("maradona", ["sol ayak kullanan bir futbol'cu"]),
               
            ],
            "iletişim":[
            ("araştırma", ["internet denilince insanların aklına ilk ne gelir?."]),
            ("oyunlar", ["telefon'da en sevilen uygulamalar hangisi'dir"]),
            ("whatsapp", ["hangi uygulama'da görüntülü shopet edilir."]), 
            ("capcut", ["video düzenleyici bir uygulama"]),
            ("chatgbt", ["popüler bir yapay zeka modeli'dir"]),
            
            ("parol", ["baş ağrı'sına iyi gelen bir ilaç'tır"]),
            
            ("beş", ["ronaldo'nun kaç tane ballandor'u vardır"]),
            
            ("marsupilami", ["yumurcak tv'de sevilen bir çizgi film'dir "]),
            
            
            ],
            
            "araçlar":[
            
            ("toog", ["italyan mal'ı ama türkiyede üretilen araç"]),
            ("gtr", ["paul walker'in hızlı ve öfke filmin'de hangi aracı kullanmıştır"]),
            
            ],
           
            "programlama": [
                ("python", ["Yüksek seviyeli bir programlama dilidir."]),
                ("java", ["Nesne yönelimli bir programlama dilidir."]),
                ("javascript", ["Web sayfalarını etkileşimli hale getirmek için kullanılır"]),
                ("algoritma", ["Bir problemi çözmek için belirlenen yol veya adım."]),
                ("değişken", ["Bir değeri saklamak veya temsil etmek için kullanılan isim."])
            ],
            "hayvanlar": [
                ("kartal", ["Büyük bir yırtıcı kuş."]),
                ("şahin", ["Hızlı ve keskin bakışlı bir yırtıcı kuş."]),
                ("aslan", ["doğanın kral'ı olarak bilinen hayvan'dır"]),
                ("timsah", ["hem su'da hem'de karada yaşayan bir hayvan türü'dür"]),
                ("doğan", ["Ormanlık alanlarda yaşayan bir yırtıcı kuş."]),
                ("yılan", ["insanların korktuğu sürüngen hayvan hangisi'dir"]),
                ("atmaca", ["Genellikle dağlık bölgelerde bulunan bir yırtıcı kuş."]),
                ("fil", ["uzun kulaklı olan hayvan'dır"]),
                ("kaplan", ["kedi türün'den en güçlü hayvandır."]),
                ("sinek", ["uçan bir hayvan yazınız"]),
                ("geyik", ["otçul bir hayvan'dır"]),
                
                ("kaplumbağa", ["sırtın'da  kabuğu olan hayvan hangisi'dir"]), 
                ("baykuş", ["gece'leyin en iyi gören kuş türü'dür"]),
                ("papağan", ["hangi kuş türü konuşur"]),
                ("sırtlan", ["sürüyle gezen hayvan hangisi'dir"]),
                ("panda", ["çin'e özgü siyah beyaz hayvan"]),
                ("yedi", ["bir rakam yazınız"]),
            ],
            "ülkeler": [
                ("almanya", ["Orta Avrupa'da bir ülkedir."]),
                ("fransa", ["Batı Avrupa'da bir ülkedir."]),
                ("japonya", ["Doğu Asya'da bir ada ülkesidir."]),
                ("portekiz", ["cristiano ronaldo nereli"]),
                ("brezilya", ["Güney Amerika'nın en büyük ülkelerinden biridir."]),
                ("almanya", ["o.khan nereli'dir"]),
                ("avustralya", ["Okyanusya kıtasında bir ülkedir."]),
                ("amerika", ["en güzel ülke hangisi'dir"]),
              ("şanlıurfa", ["göbekli tepe nerede'dir"]),
                ("brezilya", ["rio karnavalı nerede yapılır"]),
                ("mısır", ["piramitler hangi ülke'de bulunur"]),
                
    ("konya", ["etli ekmek hangi şehirimize   ait'dir"]),
    
    ("malatya", ["en çok kayısı nerde yetişir"]),
    
    
    
          ("kanada", ["en güzel ülke hangisi'dir"]),
          ("norveç", ["en güzel ülke hangisi'dir"]),
          ("fransa", ["en güzel ülke hangisi'dir"]),
          ("ingiltere", ["en güzel ülke hangisi'dir"]),
          ("almanya", ["en güzel ülke hangisi'dir"]),
            ("ingiltere", ["peaky blenders film'i nerede çekilmiştir"]),
            ]
        }
        kategori = random.choice(list(kelimeler.keys()))
        kelime, aciklama = random.choice(kelimeler[kategori])
        return kategori, kelime, aciklama

    def kategori_aciklama(self, kategori, aciklama):
        return f"{kategori.capitalize()} ile ilgili bir açıklama: {aciklama}"

    def kelime_goster(self, kelime):
        return " ".join([harf if harf.lower() in self.tahmin_edilen_harfler or not harf.isalpha() else "_" for harf in kelime])

    def tebrik_mesaji(self, oyuncu_isim):
        messagebox.showinfo("Tebrikler", f"{oyuncu_isim}, KAZANDINIZ! (hadi birdaha kazanalım)")

    def kaybettiniz_mesaji(self, kelime, oyuncu_isim):
        messagebox.showinfo("Üzgünüm", f"{oyuncu_isim}, KAYBETTİNİZ! (bu sefer olcak))\nDoğru kelime: {kelime}")

    def animate_hangman(self, karakter_durumu):
        hangman_graphics = [
            """
        +-----+

       |        |

                |

                |

    _____  |

     |     |     |

    =========""", """

       +-----+

       |        |

      O       |

                |

    _____  |

     |     |     |

    =========""", """

       +-----+

       |        |

      O       |

       |        |

    _____  |

     |     |     |

    =========""", """

       +-----+

       |        |

      O       |

      /|        |

    _____  |

     |     |     |

    =========""", """

       +-----+

       |        |

      O       |

      /|\       |

    _____  |

     |     |     |

    =========""", """

       +-----+

       |        |

      O       |

      /|\       |

    _/___   |

     |     |     |

    =========""", """

       +-----+

       |        |

      O       |

      /|\       |

   _/_\_     |

     |     |     |

    =========""", """

       +-----+

       |        |

      O       |

      /|\       |

   _/_\_     |

     |     \     |

    =========""", """

       +-----+

       |        |

      O       |

      /|\       |

   _/_\_     |

     /     \     |

    =========""", """

       +-----+

       |        |

      O       |

      /|\       |

   _/_\      |

     /     _  |

    =========""", """

       +-----+

       |        |

      O       |

      /|\       |

    _/ \       |

     /   _ _  |

    =========""", """

       +-----+

       |        |

      O       |

      /|\       |

      / \       |

     ___     |

    =========""",]

        messagebox.showinfo("Karakter Durumu", hangman_graphics[karakter_durumu])

    def insan_dogrulama(self):
        num1 = random.randint(1, 10)
        num2 = random.randint(1, 20)
        dogru_cevap = num1 + num2

        while True:
            cevap = simpledialog.askinteger("İnsan Doğrulaması", f"{num1} + {num2} = ?")
            if cevap == dogru_cevap:
                return True
            else:
                messagebox.showinfo("Hatalı Doğrulama", "Yanlış cevap. Lütfen doğru cevabı girin.")

    def adam_asmaca(self):
        # İnsan doğrulaması
        if not self.insan_dogrulama():
            messagebox.showinfo("İnsan Doğrulaması Başarısız", "Üzgünüz, insan doğrulamasını geçemediniz. Oyunu başlatmak için tekrar deneyin.")
            return

        # Yaş sınırı doğrulaması
        while True:
            yas = simpledialog.askinteger("Yaş Doğrulaması", "Lütfen yaşınızı girin:")
            if yas is None:
                messagebox.showinfo("Oyun İptal Edildi", "Oyun iptal edildi. Yeni bir oyun başlatmak için tekrar deneyin.")
                return
            elif yas < 8:
                messagebox.showinfo("Yaş Sınırı", "Üzgünüz, bu oyunu oynamak için yaşınız uygun değil.")
            else:
                break

        # İsim girişi
        oyuncu_isim = simpledialog.askstring("Oyuna Başla", "Lütfen isminizi girin:")
        if oyuncu_isim is None:
            messagebox.showinfo("Oyun İptal Edildi", "Oyun iptal edildi. Yeni bir oyun başlatmak için tekrar deneyin.")
            return

        while True:
            kategori, kelime, aciklama = self.kelime_sec()
            karakter_durumu = 0
            self.kalan_hak = 6
            self.tahmin_edilen_harfler = []

            messagebox.showinfo("Adam Asmaca Oyununa Hoş Geldiniz! (hard shelby)", f"Açıklama: {aciklama}\nPuanınız: {self.puan}\nOyuncu İsmi: {oyuncu_isim}")

            aciklama_metin.delete('1.0', tk.END)
            kelime_metin.delete('1.0', tk.END)

            aciklama_metin.insert(tk.END, aciklama)
            kelime_metin.insert(tk.END, self.kelime_goster(kelime))

            while self.kalan_hak > 0 and "_" in self.kelime_goster(kelime):
                tahmin = simpledialog.askstring("Adam Asmaca", f"Tahmin edilen kelime: {self.kelime_goster(kelime)}\nHarf almak için 'hardshelby' yazınız")
                if tahmin is not None:
                    tahmin = tahmin.lower()
                    if not tahmin and self.puan >= 20:
                        self.puan -= 20
                        messagebox.showinfo("Geçersiz Giriş", f"Geçersiz giriş! 20 puan kesildi. Güncel puanınız: {self.puan}")
                    elif tahmin == 'hardshelby':
                        if self.puan >= 10:
                            self.puan -= 10
                            rastgele_harf = random.choice([harf for harf in kelime if harf.isalpha() and harf.lower() not in self.tahmin_edilen_harfler])
                            self.tahmin_edilen_harfler.append(rastgele_harf)
                            messagebox.showinfo("Harf Satın Aldınız", f"Bir harf satın aldınız: {rastgele_harf}. Güncel puanınız: {self.puan}")
                            kelime_metin.delete('1.0', tk.END)
                            kelime_metin.insert(tk.END, self.kelime_goster(kelime))
                        else:
                            messagebox.showinfo("Yetersiz Puan", "Yeterli puanınız yok. Daha fazla harf almak için puan kazanın.")
                    elif tahmin.isalpha() and len(tahmin) == 1:
                        if tahmin in self.tahmin_edilen_harfler:
                            messagebox.showinfo("Tekrarlanan Harf", f"Bu harfi zaten tahmin ettiniz. 10 puan kesildi. Güncel puanınız: {self.puan - 10}")
                            self.puan -= 10
                        else:
                            self.tahmin_edilen_harfler.append(tahmin)
                            if tahmin not in kelime:
                                self.kalan_hak -= 1
                                karakter_durumu += 1
                                messagebox.showinfo("Yanlış Tahmin", f"Yanlış tahmin! Kalan hakkınız: {self.kalan_hak}")
                            else:
                                messagebox.showinfo("Doğru Tahmin", "Doğru tahmin!")
                                kelime_metin.delete('1.0', tk.END)
                                kelime_metin.insert(tk.END, self.kelime_goster(kelime))
                    elif tahmin.isalpha() and len(tahmin) > 1:
                        if tahmin == kelime.lower():
                            self.tebrik_mesaji(oyuncu_isim)
                            messagebox.showinfo("Tebrikler", f"Tebrikler, kazandınız!\nPuanınız: {self.puan}")
                            self.toplam_kazanma_sayisi += 1
                            break
                        else:
                            self.kalan_hak -= 3
                            karakter_durumu += 2
                            messagebox.showinfo("Yanlış Kelime Tahmini", f"Yanlış kelime tahmini! Kalan hakkınız: {self.kalan_hak}")
                    else:
                        messagebox.showinfo("Geçersiz Giriş", "Geçersiz giriş. Lütfen harf veya kelime girin veya 'marka.editss.' yazarak harf alın.")
                else:
                    messagebox.showinfo("Oyun İptal Edildi", "Oyun iptal edildi. Yeni bir oyun başlatmak için tekrar deneyin.")
                    break

                self.animate_hangman(karakter_durumu)

            if self.kalan_hak == 0:
                self.kaybettiniz_mesaji(kelime, oyuncu_isim)
                self.toplam_kaybetme_sayisi += 1

            self.toplam_oynama_sayisi += 1

            # Burada oyun tekrar başladığında soru sorabilirsiniz.
            soru = messagebox.askyesno("Oyun Bitti", "Yeni bir oyun başlatmak ister misiniz?")
            if not soru:
                break

    def istatistikleri_goster(self):
        istatistikler = f"Toplam Oynama Sayısı: {self.toplam_oynama_sayisi}\n"
        istatistikler += f"Toplam Kazanma Sayısı: {self.toplam_kazanma_sayisi}\n"
        istatistikler += f"Toplam Kaybetme Sayısı: {self.toplam_kaybetme_sayisi}"
        messagebox.showinfo("İstatistikler (hard shelby)", istatistikler)

    def instagrama_git(self):
        webbrowser.open_new("https://www.instagram.com/wmre_aydin/")

    def tiktoka_git(self):
        webbrowser.open_new("https://www.tiktok.com/@marka.editsss?_t=8qYydQvHg3U&_r=1")

    def iletisim_kur(self):
        messagebox.showinfo("(İletişim Kur) (oyunla ile ilgili bilgiler) (hard shelby)", "Müşteri temsilcisi'ne ulaşmak için \n1. instegram butonuna basınız\n2. tiktok butonuna basınız  \n3. pabgy ID; 51390998845 \n4. hard shelby oyunu tasarlamıştır. \n \n 'oyunla ile ilgili bilgiler;' \n \n1-) bütün harfler küçük yazılır. \n2-) rakam yerine harf belirtilir mesela \n örnk; '5 yerine beş' '653 yerine \n altıyüzeliüç' '4531 yerine \n dörtbinbeşyüzotuzbir şeklinde ' yazılır \n3-) oyun güncelenmesi için belirli \n bir gün yoktur. \n4-) sade bir oyun deneyimi'dir \n5-) önemli uyarı ®= _____  ______ şu \n şekil'de görürseniz bir kereden \n tahmin edemez'siniz tek tek harf \n vermeniz gerekir. \n6-) bazen aynı sorular gözüküyor \n bu sorun çözülecek'tir \n7-) oyunu oynadığınız için teşekkür \n ederiz. (^_^)  \n8-) oyun yapılış tarih'i  ©•01/05/2024•")

    def gece_modunu_degistir(self):
        self.gece_modu = not self.gece_modu
        if self.gece_modu:
            # Gece modu için arka plan rengini ve yazı renklerini değiştirme
            pencere.configure(bg="black")
        else:
            # Gündüz moduna geri dönüş için arka plan rengini ve yazı renklerini eski haline getirme
            pencere.configure(bg="white")

    def diger_sayfaya_git(self):
        yeni_pencere = tk.Toplevel()
        yeni_pencere.title("Diğer Sayfa")

        instagram_buton = tk.Button(yeni_pencere, text="Instagram", command=self.instagrama_git)
        instagram_buton.pack(pady=20)

        tiktok_buton = tk.Button(yeni_pencere, text="TikTok", command=self.tiktoka_git)
        tiktok_buton.pack(pady=20)

        iletisim_buton = tk.Button(yeni_pencere, text="İletişim Kur", command=self.iletisim_kur)
        iletisim_buton.pack(pady=20)

        yeni_pencere.mainloop()

    def main(self):
        global pencere, aciklama_metin, kelime_metin
        pencere = tk.Tk()
        pencere.title("Adam Asmaca Oyunu")  # Başlığı sadece oyun adı olarak bıraktık
        pencere.geometry("600x400+0+0")
        pencere.configure(bg="white")  # Başlangıçta arka plan rengini beyaz olarak ayarladık

        saat = Saat(pencere)  # Saat nesnesini oluşturduk ve pencereye ekledik

        ayarlar_buton = tk.Button(pencere, text="\u2699️", font=("Segoe UI Symbol", 12), command=self.gece_modunu_degistir, bg="white", bd=0, activebackground="white", highlightthickness=0)
        ayarlar_buton.pack(anchor="ne", padx=10, pady=10)

        oyuna_basla_buton = tk.Button(pencere, text="Oyuna Başla", command=self.adam_asmaca, fg="red")
        oyuna_basla_buton.pack(side="top", pady=20)

        istatistikler_buton = tk.Button(pencere, text="İstatistikler ", command=self.istatistikleri_goster)
        istatistikler_buton.pack(side="top", pady=20)

        diger_sayfa_buton = tk.Button(pencere, text="Diğer Sayfa ", command=self.diger_sayfaya_git)
        diger_sayfa_buton.pack(side="top", pady=20)

        aciklama_metin = tk.Text(pencere, height=4, width=50)
        aciklama_metin.pack(pady=10)

        kelime_metin = tk.Text(pencere, height=2, width=50)
        kelime_metin.pack(pady=10)
        
            # Sürüm bilgisini gösterme
        surum_label = tk.Label(pencere, text=f" hard shelby \n Oyun Sürümü : {self.oyun_surumu}", bg="white")
        surum_label.pack(side="bottom", pady=10)

        pencere.mainloop()

oyuncu = Oyuncu()
oyuncu.main()
