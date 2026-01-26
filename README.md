# 🔐 Advanced File & Folder Encryptor

A powerful, client-side file and folder encryption tool with military-grade security. Built with vanilla JavaScript and the Web Crypto API, this tool runs entirely in your browser - no data ever leaves your device.

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Security: AES-256-GCM](https://img.shields.io/badge/Security-AES--256--GCM-green.svg)](https://en.wikipedia.org/wiki/Galois/Counter_Mode)
[![Client-Side: 100%](https://img.shields.io/badge/Client--Side-100%25-orange.svg)](https://github.com/BLK3L53Y/advanced-file-folder-encryptor)

## 🌟 Features

### Core Functionality
- **Single File Encryption** - Encrypt individual files of any type and size
- **Full Folder Encryption** - Encrypt entire folder structures while preserving directory hierarchy
- **Single-Layer Encryption** - Fast encryption with one password (`.enc` files)
- **Double-Layer Encryption** - Enhanced security with two passwords (`.enc2` files)
- **Two-Person Integrity (TPI) Mode** - Require two people to decrypt sensitive data

### Security Features
- **AES-256-GCM Encryption** - Military-grade symmetric encryption with authentication
- **PBKDF2 Key Derivation** - 600,000 iterations with SHA-256 hashing
- **Random Salt & Nonce** - 32-byte salt and 12-byte nonce per encryption layer
- **100% Client-Side** - All processing happens locally in your browser
- **No Data Transmission** - Files never leave your device
- **Zero Dependencies** - Pure vanilla JavaScript using native Web Crypto API

### User Experience
- **Dark Modern Interface** - Professional, easy-to-use design
- **Real-Time Progress Tracking** - Visual feedback for encryption/decryption operations
- **Batch File Download** - Select and download multiple files from decrypted folders
- **Password Validation** - Warnings for weak passwords
- **Security Reminders** - Prompts to delete original files after encryption
- **Responsive Design** - Works on desktop, tablet, and mobile devices

## 🚀 Quick Start

### Option 1: Direct Use
1. Download `Advanced_File___Folder_Encryptor.html`
2. Open it in any modern web browser
3. Start encrypting!

### Option 2: Host It Yourself
```bash
# Clone the repository
git clone https://github.com/BLK3L53Y/advanced-file-folder-encryptor.git

# Open the HTML file in your browser
cd advanced-file-folder-encryptor
open Advanced_File___Folder_Encryptor.html
```

### Option 3: GitHub Pages
Visit the live version at: `https://blk3l53y.github.io/advanced-file-folder-encryptor/`

## 📖 Usage Guide

### Encrypting a File

1. **Select Mode**: Choose "📄 Single File" or "📁 Folder"
2. **Choose File/Folder**: Click the input area and browse to your file or folder
3. **Select Encryption Strength**:
   - **Single Layer** - One password, fast encryption
   - **Double Layer** - Two passwords, maximum security (TPI mode)
4. **Enter Password(s)**: Minimum 8 characters (12+ recommended)
5. **Click Encrypt**: Your encrypted file downloads automatically
6. **Delete Original**: For maximum security, delete the unencrypted original

### Decrypting a File

1. **Select Encrypted File**: Click input area and choose your `.enc` or `.enc2` file
2. **Enter Password(s)**: Tool auto-detects encryption type
   - For `.enc2`: Enter Password 2 (outer layer) first, then Password 1 (inner layer)
3. **Click Decrypt**: File decrypts and downloads
4. **For Folders**: Browse and select files to download individually or in batch

## 🔒 Security Details

### Encryption Algorithm

```
Algorithm: AES-256-GCM (Galois/Counter Mode)
Key Size: 256 bits (32 bytes)
Key Derivation: PBKDF2-SHA-256
Iterations: 600,000
Salt Size: 32 bytes (256 bits) - Random per encryption
Nonce Size: 12 bytes (96 bits) - Random per encryption
```

### File Format

**Single Layer (.enc):**
```
[32-byte salt][12-byte nonce][encrypted data + auth tag]
```

**Double Layer (.enc2):**
```
[salt2][nonce2][encrypted([salt1][nonce1][encrypted(original data)])]
```

### Security Strength

With a strong password (20+ random characters):
- **Single Layer**: ~2^256 possible keys - computationally infeasible to break
- **Double Layer**: Exponentially harder (squared security)
- **PBKDF2 600K iterations**: Makes brute-force attacks ~600,000x slower

### Why 600,000 Iterations?

The PBKDF2 iteration count follows [OWASP recommendations](https://cheatsheetseries.owasp.org/cheatsheets/Password_Storage_Cheat_Sheet.html) for PBKDF2-SHA256, significantly slowing down any brute-force attempts while remaining fast enough for legitimate use.

## 🤝 Two-Person Integrity (TPI) Mode

### What is TPI?

Two-Person Integrity is a security principle where **two different people must cooperate** to access encrypted data. Neither person can decrypt the file alone - both passwords are required.

### Use Cases

- **Business**: CEO + CFO for sensitive financial records
- **Legal**: Two attorneys for confidential case files  
- **Cryptocurrency**: Split wallet key custody between partners
- **Family**: Two trustees for important documents
- **Research**: Two scientists for sensitive research data

### How to Use

1. Choose **Double Layer** encryption
2. **Person A** sets Password 1 (inner layer)
3. **Person B** sets Password 2 (outer layer)
4. Encrypt the file
5. To decrypt: Both Person A and Person B must provide their passwords

**Note**: You can also use TPI mode yourself with two different passwords for maximum security against various attack vectors.

## 🛡️ Best Practices

### Password Guidelines

✅ **Do:**
- Use at least 12 characters (longer is better)
- Mix uppercase, lowercase, numbers, and symbols
- Use unique passwords for different files
- Consider using a password manager
- Test decryption before deleting originals

❌ **Don't:**
- Use common words or personal information
- Reuse passwords from other services
- Store passwords with encrypted files
- Use the same password twice in double-layer mode
- Close browser during encryption/decryption

### File Management

- **Backup**: Keep multiple copies of encrypted files
- **Storage**: Store in backed-up locations (cloud, external drives)
- **Original Files**: Delete after confirming successful encryption
- **Testing**: Always test decryption before deleting originals

### When to Use Double Layer

- Extremely sensitive data requiring two-person access
- Legal or compliance requirements for dual custody
- Maximum security for long-term storage
- Protection against advanced attack scenarios

## 🔧 Technical Specifications

### Browser Compatibility

Requires a modern browser with Web Crypto API support:
- ✅ Chrome 60+
- ✅ Firefox 56+
- ✅ Safari 11+
- ✅ Edge 79+
- ✅ Opera 47+

### Folder Archive Format

The tool uses a custom binary archive format (not ZIP) that preserves complete folder structure:

```
[4-byte file count]
For each file:
  [4-byte path length]
  [path bytes (UTF-8)]
  [4-byte data length]
  [data bytes]
```

This format ensures:
- Preservation of full folder hierarchy
- Efficient binary packing
- No compression overhead before encryption
- Easy extraction with file browser modal

## 🐛 Troubleshooting

### Decryption Fails

**Problem**: "Decryption failed" error

**Solutions**:
- Verify password spelling and capitalization
- Check Caps Lock is off
- For `.enc2` files, ensure both passwords are correct
- Confirm password order (Password 2 first, then Password 1)

### Files Won't Download

**Problem**: Downloads don't start or are blocked

**Solutions**:
- Check browser's download settings
- Disable popup blockers for this page
- Ensure sufficient disk space
- Try a different browser

### Slow Performance

**Problem**: Encryption takes a long time

**Solutions**:
- This is normal for large files (encryption is computationally intensive)
- Watch the progress bar
- Don't close browser during operation
- For very large files (>1GB), consider breaking into smaller pieces

### File Browser Doesn't Appear

**Problem**: After folder decryption, no file browser shows

**Solutions**:
- Disable popup blockers
- Refresh page and try again
- Check browser console for errors

## 🤔 FAQ

**Q: Is my data really secure?**  
A: Yes! AES-256-GCM is the same encryption used by governments and militaries. With a strong password, your files are virtually unbreakable with current technology.

**Q: Can you decrypt my files if I forget my password?**  
A: No! Encryption happens entirely in your browser. There is no "back door" or recovery mechanism. If you lose your password, your data is unrecoverable.

**Q: Can I encrypt the same file multiple times?**  
A: Yes! You can encrypt already-encrypted files. Just remember to decrypt in reverse order.

**Q: Why use this instead of ZIP encryption?**  
A: ZIP encryption is weak and outdated. This tool uses modern, military-grade AES-256-GCM encryption with proper key derivation.

**Q: How do I encrypt really large files?**  
A: The tool can handle files of any size, but very large files (>2GB) may take several minutes. Watch the progress bar and keep your browser open.

**Q: Can I use this offline?**  
A: Yes! Download the HTML file and use it without an internet connection. All processing is local.

## 📜 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- Built with the [Web Crypto API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Crypto_API)
- Encryption standards from [NIST](https://www.nist.gov/)
- Security best practices from [OWASP](https://owasp.org/)

## ⚠️ Disclaimer

This software is provided "as is" without warranty of any kind. While it uses industry-standard encryption, no security system is 100% impenetrable. Use at your own risk. Always:
- Keep backups of important files
- Test decryption before deleting originals
- Use strong, unique passwords
- Don't share passwords over insecure channels

## 🔗 Links

- **GitHub**: [https://github.com/BLK3L53Y/advanced-file-folder-encryptor](https://github.com/BLK3L53Y/advanced-file-folder-encryptor)
- **Live Demo**: [https://blk3l53y.github.io/advanced-file-folder-encryptor/](https://blk3l53y.github.io/advanced-file-folder-encryptor/)
- **Issues**: [https://github.com/BLK3L53Y/advanced-file-folder-encryptor/issues](https://github.com/BLK3L53Y/advanced-file-folder-encryptor/issues)

## 💬 Support

If you find this tool useful, please consider:
- ⭐ Starring the repository
- 🐛 Reporting bugs
- 💡 Suggesting features
- 🔀 Contributing improvements

---

**Made with 🔐 by [BLK3L53Y](https://github.com/BLK3L53Y)**
