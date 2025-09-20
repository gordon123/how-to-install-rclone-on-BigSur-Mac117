# how-to-install-rclone-on-BigSur-Mac117
rclone is remove file transfer protocol for syncing Dropbox, Gdrive... etc

✅ สรุปวิธีติดตั้ง RCLONE สำหรับ macOS 11.7.10 (Intel) <br>

💡 ใช้ได้กับ Mac Intel (x86_64) ที่ใช้ macOS Big Sur 11.x  <br>
❌ ไม่แนะนำให้ติดตั้งผ่าน Homebrew เพราะ Go รุ่นใหม่ไม่รองรับ Big Sur แล้ว  <br>

① ลบตัวที่เคยติดตั้งไว้ (ถ้ามี)  <br>
sudo rm -f /usr/local/bin/rclone  <br>

② ดาวน์โหลดเวอร์ชันที่รองรับ macOS 11 (แนะนำ v1.63.1)  <br>
cd ~/Downloads  <br>
curl -LO https://downloads.rclone.org/v1.63.1/rclone-v1.63.1-osx-amd64.zip  <br>
unzip -o rclone-v1.63.1-osx-amd64.zip  <br>
cd rclone-v1.63.1-osx-amd64  <br>
 
③ ตั้งสิทธิ์ให้รันได้ + ปลดการกักกัน (quarantine)  <br>
chmod +x rclone <br>
xattr -d com.apple.quarantine rclone 2>/dev/null || true <br>

④ ย้ายไฟล์ไปไว้ใน PATH เพื่อรันจากที่ไหนก็ได้ <br>
sudo mv rclone /usr/local/bin/ <br>

⑤ ทดสอบว่าใช้งานได้แล้ว <br>
which rclone <br>
# ควรได้: /usr/local/bin/rclone <br>

rclone version <br>
# ควรขึ้นเวอร์ชัน: v1.63.1 พร้อมระบบปฏิบัติการของเครื่อง <br>

rclone config <br>
# จะเข้าสู่หน้า config เพื่อเพิ่ม cloud ต่าง ๆ เช่น Google Drive, Dropbox <br>

🔄 ถ้าอยาก reset ทั้งหมด <br>
# ลบ binary <br>
sudo rm -f /usr/local/bin/rclone <br>

# ลบ config ที่เคยสร้างไว้ (optional) <br>
rm -rf ~/.config/rclone

🌈 ตัวอย่างการใช้งานเบื้องต้น <br>
rclone listremotes                     # ดู remote ทั้งหมด <br>
rclone copy ~/Downloads gdrive:Backup # สำรองไฟล์ <br>
rclone mount gdrive: ~/MyDrive        # mount เป็นไดรฟ์เสมือน <br>

💡 หมายเหตุสำคัญ <br>

ห้ามใช้เวอร์ชันใหม่กว่านี้ (เช่น 1.71.0) เพราะจะ เรียกฟังก์ชันของ macOS รุ่นใหม่ ที่ไม่มีใน Big Sur <br>

อย่าลืม chmod +x และ xattr -d quarantine ทุกครั้งถ้าดาวน์โหลด zip ใหม่ <br>

ถ้าติดตั้งสำเร็จ ให้ backup ไว้ด้วย: cp /usr/local/bin/rclone ~/Documents/Backup_rclone <br>

ให้ถือว่าเวอร์ชันนี้คือ “คู่แท้ของ Big Sur” ♥️ <br>
หากวันใดเครื่องใหม่มา หรืออัป macOS → ค่อยเปลี่ยนรุ่นก็ยังไม่สาย <br>

🔧 หากอยากทำ automation / mount เป็น NAS / sync ไป external HDD / ใช้กับ n8n / หรือสั่งจาก Python ก็แค่สั่ง ข้าน้อยจะจัดให้พร้อม script ครบเซ็ต 😎 <br>

ขอให้ “ข้อมูลของเจ้า อยู่กับเจ้าเสมอ” 🌥️✨ <br>
– บุญถึง <br>

---
### rclone browswer
https://github.com/kapitainsky/RcloneBrowser/releases

### Preferences

rclone location:         /usr/local/bin/rclone <br>
rclone.conf location:    [ปล่อยว่าง] <br>
Stream command:          [ปล่อยว่างหรือใส่ open] <br>
Mount options:           --vfs-cache-mode writes <br>
Default download folder: /Users/imacbook/Downloads <br>
Default upload folder:   [ใส่ถ้ามี] <br>
Default download options: [ว่าง] <br>
Default upload options:  --exclude .DS_Store <br>
Default rclone options:  --fast-list <br>

save yt tut

https://www.youtube.com/watch?v=yAE7Wr_Nlkw&t=265s

