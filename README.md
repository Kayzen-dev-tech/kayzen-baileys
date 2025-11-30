🚀 Kayzen Baileys - Advanced WhatsApp Bot Library

<div align="center">

https://img1.pixhost.to/images/10533/666042007_lyrra-md.jpg

https://img.shields.io/npm/v/kayzen-baileys.svg?style=for-the-badge&logo=npm
https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge
https://img.shields.io/badge/Node.js-16+-green.svg?style=for-the-badge&logo=node.js
https://img.shields.io/badge/WhatsApp-Multi--Device-brightgreen.svg?style=for-the-badge&logo=whatsapp
https://img.shields.io/badge/TypeScript-Ready-blue.svg?style=for-the-badge&logo=typescript

Advanced WhatsApp Bot Library dengan fitur pairing code kustom, pesan interaktif, dan manajemen sesi otomatis

Features • Installation • Quick Start • Examples • Documentation

</div>

✨ Features

<div align="center">

Feature Description Status
🔐 Custom Pairing Codes Kode pairing yang stabil dan aman untuk koneksi WhatsApp ✅ Implemented
💬 Interactive Messages Tombol aksi dan menu dinamis dengan mudah ✅ Implemented
🔄 Session Management Manajemen sesi otomatis dan efisien ✅ Implemented
📱 Multi-Device Support Kompatibel dengan fitur multi-perangkat terbaru ✅ Implemented
⚡ High Performance Optimized untuk penggunaan jangka panjang ✅ Implemented
🛡️ Security Proteksi dan manajemen kredensial yang aman ✅ Implemented

</div>

🚀 Installation

```bash
# Menggunakan npm
npm install kayzen-baileys

# Menggunakan yarn
yarn add kayzen-baileys

# Menggunakan pnpm
pnpm add kayzen-baileys
```

📖 Quick Start

Basic Bot Setup

```javascript
import KayzenClient from 'kayzen-baileys';

// Inisialisasi bot dengan konfigurasi
const bot = new KayzenClient({
  sessionId: 'my-awesome-bot',
  pairingCode: 'BOT123', // Opsional: kode pairing kustom
  logger: {
    info: (msg) => console.log(`🤖 ${msg}`),
    error: (msg) => console.error(`❌ ${msg}`)
  }
});

// Event handler untuk koneksi
bot.on('connected', () => {
  console.log('✅ Bot berhasil terhubung ke WhatsApp!');
});

// Handler untuk pesan masuk
bot.on('message', async ({ text, from, reply, react }) => {
  // React kepada pesan
  await react('👋');
  
  // Command handler sederhana
  if (text === '!ping') {
    await reply('🏓 Pong!');
  } else if (text === '!menu') {
    // Mengirim pesan interaktif dengan tombol
    const buttons = [
      { id: 'info', text: '📋 Info' },
      { id: 'help', text: '❓ Bantuan' },
      { id: 'about', text: '👨‍💻 Tentang' }
    ];
    
    await bot.sendInteractiveMessage(
      from,
      '🎯 **Menu Utama**\nPilih opsi di bawah:',
      buttons,
      { footer: 'Kayzen Baileys Bot' }
    );
  }
});

// Start bot
await bot.initialize();
```

🎯 Examples

1. Customer Service Bot

```javascript
import KayzenClient from 'kayzen-baileys';

const csBot = new KayzenClient({
  sessionId: 'customer-service',
  pairingCode: 'CS2024'
});

csBot.on('message', async ({ text, from, sender, reply }) => {
  const lowerText = text.toLowerCase();
  
  if (lowerText.includes('harga') || lowerText.includes('price')) {
    await reply(`Halo ${sender}! 🏷️\n\nBerikut daftar harga kami:
• Paket Basic: Rp 100.000/bulan
• Paket Pro: Rp 250.000/bulan
• Paket Enterprise: Rp 500.000/bulan
    
Silakan ketik "order" untuk memesan.`);
  }
  
  if (lowerText.includes('order') || lowerText.includes('pesan')) {
    const orderButtons = [
      { id: 'basic', text: '📦 Paket Basic' },
      { id: 'pro', text: '🚀 Paket Pro' },
      { id: 'enterprise', text: '🏢 Paket Enterprise' }
    ];
    
    await csBot.sendInteractiveMessage(
      from,
      `💼 **Form Pemesanan**\nPilih paket yang diinginkan:`,
      orderButtons,
      { footer: 'CS Team - Kayzen Baileys' }
    );
  }
});

await csBot.initialize();
```

2. Interactive Menu System

```javascript
// Contoh menu interaktif dengan list message
const menuSections = [
  {
    title: "🛍️ Produk & Layanan",
    rows: [
      {
        id: 'product_catalog',
        title: 'Katalog Produk',
        description: 'Lihat semua produk kami'
      },
      {
        id: 'service_info',
        title: 'Informasi Layanan',
        description: 'Detail layanan yang tersedia'
      }
    ]
  },
  {
    title: "ℹ️ Informasi",
    rows: [
      {
        id: 'company_profile',
        title: 'Profil Perusahaan',
        description: 'Tentang kami dan visi misi'
      },
      {
        id: 'contact_us',
        title: 'Hubungi Kami',
        description: 'Kontak customer service'
      }
    ]
  }
];

await bot.sendListMessage(
  from,
  '🏢 **Selamat datang di Company Name**\nPilih menu yang tersedia:',
  menuSections,
  {
    title: 'Menu Utama',
    footer: 'Terima kasih telah menghubungi kami',
    buttonText: 'Buka Menu'
  }
);
```

⚙️ Configuration

Client Options

```javascript
const options = {
  // Required
  sessionId: 'unique-bot-id',
  
  // Optional
  pairingCode: 'CUSTOM123',      // Kode pairing kustom
  sessionSaveMode: 'AUTO',       // AUTO, MANUAL, FILE
  logger: console,               // Custom logger
  
  // Advanced
  authPath: './sessions',        // Custom auth path
  retryCount: 3,                 // Retry attempts
  connectTimeout: 30000          // Connection timeout
};

const bot = new KayzenClient(options);
```

Event Handlers

```javascript
// Koneksi events
bot.on('connected', () => {
  console.log('✅ Bot connected successfully');
});

bot.on('disconnected', (reason) => {
  console.log('🔌 Bot disconnected:', reason);
});

// Message events
bot.on('message', async ({ message, text, from, reply }) => {
  // Handle semua pesan masuk
});

bot.on('message.button', async ({ buttonId, from, reply }) => {
  // Handle tombol yang diklik
  switch(buttonId) {
    case 'info':
      await reply('Ini adalah informasi...');
      break;
    case 'help':
      await reply('Bantuan tersedia...');
      break;
  }
});
```

📚 API Reference

Core Methods

Method Parameters Description
sendMessage jid, content, options Mengirim pesan biasa
sendInteractiveMessage jid, text, buttons, options Mengirim pesan dengan tombol
sendListMessage jid, text, sections, options Mengirim list message
sendReaction jid, key, emoji Mengirim reaction ke pesan
initialize - Memulai koneksi WhatsApp
destroy - Mematikan koneksi dengan aman

Message Types

```javascript
// Text message
await bot.sendMessage(jid, { text: 'Hello World!' });

// Image message
await bot.sendMessage(jid, {
  image: { url: 'https://example.com/image.jpg' },
  caption: 'Ini adalah gambar'
});

// Button message
await bot.sendInteractiveMessage(jid, 'Pilih opsi:', [
  { id: 'btn1', text: 'Button 1' },
  { id: 'btn2', text: 'Button 2' }
]);

// List message
await bot.sendListMessage(jid, 'Pilih menu:', sections);
```

🏗️ Architecture

```
Kayzen Baileys Structure
├── 📱 Core Layer
│   ├── KayzenClient (Main Class)
│   ├── SessionManager (Session Handling)
│   └── PairingManager (Custom Pairing Codes)
├── 💬 Features Layer
│   ├── InteractiveMessages (Buttons & Lists)
│   ├── ButtonManager (Button Interactions)
│   └── MenuManager (Dynamic Menus)
├── 🔧 Utils Layer
│   ├── Helpers (Utility Functions)
│   └── Constants (Enums & Configs)
└── 🎯 Examples
    ├── Basic Bot
    ├── Customer Service
    └── Interactive Menu
```

🤝 Contributing

Kami menyambut kontribusi dari komunitas! Berikut cara berkontribusi:

1. Fork repository ini
2. Buat branch untuk fitur baru (git checkout -b feature/AmazingFeature)
3. Commit perubahan (git commit -m 'Add some AmazingFeature')
4. Push ke branch (git push origin feature/AmazingFeature)
5. Buat Pull Request

Development Setup

```bash
# Clone repository
git clone https://github.com/yourusername/kayzen-baileys.git
cd kayzen-baileys

# Install dependencies
npm install

# Run examples
npm run example:basic
npm run example:service
npm run example:menu
```

📊 Performance

Metric Value Description
Connection Time < 5s Waktu koneksi ke WhatsApp
Message Delivery < 2s Rata-rata pengiriman pesan
Session Recovery < 3s Pemulihan sesi otomatis
Memory Usage < 100MB Penggunaan memory optimal

🐛 Troubleshooting

Common Issues

1. Connection Failed
   ```bash
   # Pastikan internet stabil
   # Cek firewall/port
   # Gunakan pairing code kustom
   ```
2. Session Expired
   ```bash
   # Hapus folder sessions
   rm -rf sessions/
   # Inisialisasi ulang bot
   ```
3. Message Not Sent
   ```javascript
   // Gunakan error handling
   try {
     await bot.sendMessage(jid, content);
   } catch (error) {
     console.error('Send failed:', error);
   }
   ```

📄 License

Distributed under the MIT License. See LICENSE file for more information.

🙏 Acknowledgments

· Baileys - WhatsApp Web API
· WhatsApp - Platform
· Contributors - Semua kontributor yang membantu pengembangan

---

<div align="center">

Kayzen Baileys - 🤖 Advanced WhatsApp Bot Library

[📚 Documentation](https://github.com/Kayzen-dev-tech/kayzen-baileys/wiki)

⭐ Jangan lupa beri bintang di repository ini jika kamu menyukainya!

</div>