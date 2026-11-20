# Kamu Portalı Botları ve İK Portalı

Türkiye'deki kamu portallarında elle tekrarlanan işleri otomatikleştiren tarayıcı botları ile bunlara bağlı bir İK portalı. Tüm botlar Telegram üzerinden yönetilir ve n8n ile zamanlanır.

> Bu depo bir proje vitrinidir. Kaynak kod paylaşılmamaktadır.

## Botlar

| Bot | Ne yapar |
|---|---|
| **e-Tebligat indirici** | Dijital Vergi Dairesi'ndeki tüm tebligatları ekleriyle indirir. Her tebligat bir kez iner, sonraki çalıştırmalarda yalnızca yeniler gelir. |
| **Borç durum yazısı** | Her sabah otomatik talep oluşturur, sonucu Telegram'a gönderir |
| **SGK işe giriş bildirgesi** | Telegram'a "işe giriş" yazılınca eksik alanları tek tek sorar ve formu doldurur. Onay sayfasının ekran görüntüsünü gönderir, "EVET" yanıtı gelince bildirgeyi verir ve PDF'i iletir. |
| **EKAP yardımcısı** | İhale dokümanlarını düzenleyen kullanıcı betiği (userscript) ve Python aracı |

## Ortak altyapı

- **Güvenli giriş:** Güvenlik kodu (captcha) Telegram'dan kullanıcıya sorulur. 10 dakika içinde cevap gelmezse çalışma iptal edilir ve bildirilir.
- **Oturum yeniden kullanımı:** Giriş sonrası sitenin kendi API'si çağrılır, gereksiz sayfa gezintisi yapılmaz.
- **Tetikleme servisi:** n8n'den gelen, token korumalı HTTP isteğiyle botlar başlatılır.
- Şifreler kod dışında, şifreli kurulum adımıyla saklanır.

## İK Portalı

- Personel kayıtları, kimlik ve sözleşme belgeleri, giriş-çıkış saatleri
- Belgeler web kökü dışında saklanır ve yalnızca oturum açmış kullanıcıya verilir
- İmzalı oturum çerezleri, botlar için API anahtarlı uçlar

## Teknolojiler

`Python` · `Playwright` · `FastAPI` · `Jinja2` · `SQLite` · `openpyxl` · `Telegram Bot API` · `n8n` · `Linux / cron`
