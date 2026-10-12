<div align="center">
  <img src="docs/images/logo.svg" alt="Kuantum Çift Yarık Logosu" width="112" height="112">
  <h1>Kuantum Çift Yarık · Quantum Double-Slit</h1>
  <p><strong>Gerçek Zamanlı WebGL 2 Kuantum Simülasyonu &amp; Schrödinger Dalga Mekaniği Laboratuvarı.</strong></p>

  <p>
    <strong>Dil:</strong> <a href="README.md"><strong>EN</strong></a> | <a href="README.tr.md"><strong>TR</strong></a>
    &nbsp;•&nbsp;
    <a href="#genel-bakış">Genel Bakış</a> ·
    <a href="#fizik-motoru">Fizik Motoru</a> ·
    <a href="#ölçüm-ve-dolanıklık">Ölçüm &amp; Dolanıklık</a> ·
    <a href="#kontroller">Kontroller</a> ·
    <a href="#destek">Destek</a>
  </p>

  <p>
    <img src="https://img.shields.io/badge/Dil-TR%20%7C%20EN-blue?style=flat-square" alt="TR | EN">
    <img src="https://img.shields.io/badge/Platform-Taray%C4%B1c%C4%B1%20%2F%20WebGL%202-0078D6?logo=webgl&style=flat-square" alt="WebGL 2">
    <img src="https://img.shields.io/badge/%C3%87ekirdek-Saf%20JavaScript-F7DF1E?logo=javascript&style=flat-square" alt="Vanilla JS">
    <img src="https://img.shields.io/badge/Tema-Starlit%20%E2%9C%A6-e7a0b9?style=flat-square" alt="Starlit Theme">
    <img src="https://img.shields.io/badge/Ba%C4%9F%C4%B1ml%C4%B1l%C4%B1k-S%C4%B1f%C4%B1r%20%2F%20Do%C4%9Fal-10B981?style=flat-square" alt="Sıfır Bağımlılık">
    <img src="https://img.shields.io/badge/Testler-Tamam%C4%B1%20Ge%C3%A7ti-success?style=flat-square" alt="Testler">
    <img src="https://img.shields.io/badge/Lisans-MIT-blue?style=flat-square" alt="MIT Lisansı">
  </p>

  <br>
  <img src="docs/images/preview.png" alt="Kuantum Çift Yarık Simülasyon Önizlemesi" width="940">
  <br>
</div>

---

## Destek

Eğer **Kuantum Çift Yarık** simülasyonunu fizik eğitiminizde, araştırmalarınızda veya kişisel merakınızda faydalı bulduysanız projeye destek olabilirsiniz:

<div align="center">
  <a href="https://buymeacoffee.com/hfatih" target="_blank">
    <img src="https://img.shields.io/badge/Buy_Me_A_Coffee-FFDD00?style=for-the-badge&logo=buy-me-a-coffee&logoColor=black" alt="Buy Me A Coffee">
  </a>
  &nbsp;&nbsp;
  <a href="https://github.com/sponsors/Hfatih" target="_blank">
    <img src="https://img.shields.io/badge/Sponsor_on_GitHub-EA4AAA?style=for-the-badge&logo=github-sponsors&logoColor=white" alt="GitHub Sponsor">
  </a>
  <p><sub><em>Desteğiniz projenin bağımsız, ücretsiz ve sürekli güncel kalmasını sağlar.</em></sub></p>
</div>

---

## Genel Bakış

**Kuantum Çift Yarık**, modern fiziğin temel deneyini doğrudan tarayıcı içinde gerçek zamanlı olarak simüle eden, **saf WebGL 2 gölgelendiricileriyle çalışan ve harici hiçbir kütüphaneye ihtiyaç duymayan** bir kuantum optik laboratuvarıdır.

Önceden çizilmiş veya yapay girişim dokuları kullanmak yerine, GPU üzerinde $1120 \times 608$ çözünürlüklü bir ızgarada **zamana bağlı iki boyutlu Schrödinger denklemini doğrudan çözer**:

$$i \frac{\partial \psi}{\partial t} = -\frac{1}{2} \nabla^2 \psi + V(\mathbf{r})\psi \quad (\hbar = m = 1)$$

### Öne Çıkan Özellikler

- **Gerçek Dalga Mekaniği:** Kenar yansımalarını yutan sünger katmanlara sahip, GPU sıçramalı (leapfrog FDTD) sayısal çözücü.
- **Born Kuralı & Parçacık Sayımı:** Ekrana ulaşan kuantum olasılık akısı $J_x = \int j_x \, dt$ anlık hesaplanır. Her bir parçacık ters-CDF Monte Carlo yöntemiyle dağılımdan tek tek çekilir. Tek tek rastgele, hepsi birlikte dalga deseni.
- **Yol Ölçümü & Kuantum Dolanıklığı:** Yarıklardaki dedektörü açarak kuantum dalga çöküşünü ve dekoheransı gözlemleyin. Hangi yoldan geçtiği bilinen dalgaların girişim terimi sıfırlanır ve saçaklar iki bağımsız yarığın klasik toplamına dönüşür ($V = 0.83 \to 0.00$).
- **Tek Parçacık Dalga Paketi Modu:** Kaynaktan çıkan tekil bir Gauss dalga paketinin iki yarıktan aynı anda süperpozisyon halinde geçişini ve ekranda tek bir noktaya çöküşünü adım adım izleyin.
- **Sürekli Demet Modu:** Kararlı ve yüksek akılı parçacık yağmuru; histogram ve kuramsal eğri ile anlık karşılaştırma.
- **Starlit / Cosmic Dark Tasarımı:** `#150a14` derin uzay mürdümü, `#f0abc5` göksel gül rengi, yarı saydam cam paneller ve 4 uçlu Starlit yıldızları (`✦`) ile özel tasarım.

---

## Fiziksel Formülasyon

```
 [ Koherent Kaynak ]            [ Engel ]                 [ Ölçüm Ekranı ]
       x = 140                    x = 360                       x = 1000
          │                          │                              │
  ════════╪══════════════════════════╡   Yarık 1                    │
          │                          │  (genişlik a)                │  Olasılık
    ψ(x, y, t) ────────────────────► ╞═══════════                  │  Akısı J(y)
          │                          │   Aralık d  ───────────────► │  ──────────────►
          │                          ╞═══════════                   │  Monte Carlo
  ════════╪══════════════════════════╡   Yarık 2                    │  Örnekleme N
          │                          │                              │
```

### 1. Sayısal Örgü Çözümü (Leapfrog Şeması)
Karmaşık dalga fonksiyonu $\psi = \psi_R + i\psi_I$ olarak ayrılarak zaman adımı $\Delta t = 0.4$ ile güncellenir:

$$\psi_R^{n+1/2} = \psi_R^{n-1/2} - \frac{\Delta t}{2} \nabla^2 \psi_I^n$$
$$\psi_I^{n+1} = \psi_I^n + \frac{\Delta t}{2} \nabla^2 \psi_R^{n+1/2}$$

### 2. Kuantum Olasılık Akı Yoğunluğu
Dedektör ekranından geçen akı:

$$j_x = \text{Im}\left(\psi^* \frac{\partial \psi}{\partial x}\right) = \psi_R \frac{\partial \psi_I}{\partial x} - \psi_I \frac{\partial \psi_R}{\partial x}$$

Kümülatif dağılım $P(y) \propto \int_0^t j_x(x_{\text{ekran}}, y, t')\, dt'$ Born kuralı uyarınca parçacık noktalarını belirler.

### 3. Kuramsal Saçak Aralığı
$L = 635\text{ birim}$ ekran mesafesi, $d$ yarık aralığı ve $\lambda$ de Broglie dalga boyu için:

$$\Delta y \approx \frac{\lambda L}{d}$$

Ölçülen simülasyon sonuçları analitik hiperbolik modelle **$<\%0.1$ hata** ile örtüşür.

### 4. Girişim Görünürlüğü (Michelson Kontrastı)
Girişim deseninin tepe ve çukur noktaları arasındaki kontrast:

$$V = \frac{I_{\max} - I_{\min}}{I_{\max} + I_{\min}}$$

- **Girişim Açıkken:** $V \approx 0.83$ (Belirgin koyu ve aydınlık saçaklar).
- **Dedektör Açıkken:** $V \approx 0.00$ (Yol bilgisi kaydedildiği için girişim tamamen kaybolur).

---

## Kontroller & Klavye Kısayolları

| Kısayol | İşlem | Açıklama |
| :--- | :--- | :--- |
| <kbd>Boşluk</kbd> | **Duraklat / Devam Et** | Zaman akışını dondurarak dalga fazını inceler |
| <kbd>C</kbd> | **Ekranı Temizle** | Dalga durumunu sıfırlamadan sadece parçacık noktalarını temizler |
| <kbd>R</kbd> | **Tümünü Sıfırla** | Simülasyonu ve dalga fonksiyonunu baştan başlatır |
| <kbd>D</kbd> | **Dedektörü Aç / Kapat** | Yarık gözlemcisini aktif veya pasif yapar |
| <kbd>M</kbd> | **Modu Değiştir** | Sürekli Demet ile Tek Parçacık modu arasında geçer |
| <kbd>1</kbd> | **\|ψ\|² Görünümü** | Olasılık yoğunluğunu göksel ışıma renginde gösterir |
| <kbd>2</kbd> | **Re ψ Görünümü** | Dalga tepelerini ve çukurlarını (gül pembesi / camgöbeği) gösterir |
| <kbd>3</kbd> | **Faz Görünümü** | Karmaşık açıyı $\arg(\psi) = \text{atan2}(\psi_I, \psi_R)$ renk çemberinde gösterir |

---

## Hızlı Başlangıç

Kurulum, paket yöneticisi veya sunucu gerekmez.

1. Depoyu klonlayın:
   ```bash
   git clone https://github.com/Hfatih/quantum-double-slit.git
   ```
2. `index.html` dosyasını WebGL 2 destekli herhangi bir modern tarayıcıda açın.

---

## Hazır Deneyler

- **✦ Girişim Deseni:** $\lambda = 12$, $d = 112$, $a = 30$, dedektör KAPALI.
- **✦ Dedektörü Aç:** Gözlemci devrede; dalga fonksiyonu dekoheransı ve saçak kaybı.
- **✦ Yarıklar Uzak:** $d = 180$; birbirine daha yakın ve sık saçaklar $\Delta y$.
- **✦ Dar Yarıklar:** $a = 14$; geniş tek-yarık kırınım zarfı.
- **✦ Uzun Dalga Boyu:** $\lambda = 18$; geniş aralıklı girişim saçakları.

---

## Lisans

Bu proje **[MIT Lisansı](LICENSE)** altında açık kaynaklıdır.

**[Fatih Han (Hfatih)](https://github.com/Hfatih)** tarafından ✦ ile geliştirilmiştir.
