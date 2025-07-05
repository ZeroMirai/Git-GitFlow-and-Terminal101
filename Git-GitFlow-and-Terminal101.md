# 📘 Git, Git Flow & Terminal 101

## 🖥️ Command Line Interface (CLI) Structure
ส่วนใหญ่ Command Line Interface (CLI) มักมีโครงสร้างแบบนี้:

```bash
(program) (command) [arguments] [options]
````

แต่โครงสร้างก็แตกต่างกันไปตามคำสั่งได้ ตัวอย่างของ CLI:

|Full Command|Program|Command|Argument(s)|Option(s)|
|:-|:-:|:-:|:-:|:-:|
|`git push origin main --force`|`git`|`push`|`origin main`|`--force`|
|`git commit -m "Add login feature"`|`git`|`commit`| - |`-m "Add login feature"`|
|`git log --all --decorate --oneline --graph`|`git`|`log`|-|`--all --decorate --oneline --graph`|
|`ls ..`|-|`ls`|`..`|-|

สามารถหาข้อมูลเพิ่มเติมเกี่ยวกับคำสั่งต่างๆ ได้ที่
- [explainshell.com](https://explainshell.com/) – ช่วยแยกส่วนและอธิบายแต่ละพารามิเตอร์ของคำสั่ง CLI
- [tldr pages](https://tldr.sh/) – cheatsheet สรุปคำสั่งสั้น ๆ พร้อมตัวอย่าง

---

### ⚙️ Options & Flags

**Options** คือพารามิเตอร์ที่มักขึ้นต้นด้วย `-` หรือ `--` เช่น `-m`, `--force`
โดยส่วนใหญ่แล้วมักจะมาในรูปแบบ **key-value** เช่น:
```bash
git commit -m "Add login feature"
```

* `-m` คือ key
* `"Add login feature"` คือ value

**Flags** คือ options ที่ไม่มี value.
###### Flags simply toggle a feature on or off *(แต่บางโปรแกรมก็อนุญาติให้ flag รับค่าได้ `--color=auto`)*

```bash
git status            # No flag used – shows default output format
git status --short    # Flag is used – shows 'short' output format
ls -l -s -h           # Flag can be separate
ls -lsh               # Or can be combined (not all command can do this)
ls -hsl               # Or can be put in any order (not every tool does)
```

#### 🆘 Help Flags

ใช้ดูคำอธิบายการใช้งานคำสั่ง และบางคำสั่งก็แสดงผลต่างกันขึ้นอยู่กับ flag ที่ใช้ด้วย เช่น:

```bash
git push -h        # Short help
git push --help    # Full documentation
git help push      # Full documentation
```

---

### 📦 Arguments

คือ data or targets ที่ส่งให้ command เช่นชื่อไฟล์, ชื่อโฟลเดอร์ หรือชื่อ branch

```bash
git push origin main
```

* `origin`, `main` ทั้งคู่นี้คือ arguments

---

## 📁 Special Symbols in Terminal

|Symbol|ความหมาย|
|:-:|:-|
|`.`|โฟลเดอร์ปัจจุบัน|
|`..`|โฟลเดอร์ก่อนหน้า|
|`/`|Root directory|
|`~`|Home directory|

> [!NOTE]     
> *“Directory” = “Folder”*     

---

## 🧰 Git Basics

### 📦 Initialize Git

|Command|Description|
|:-|:-|
|`git init`|สร้าง local git repository|

### ⚙️ Git Configuration

|Command|Description|
|:-|:-|
|`git config`|ตั้งค่า git (คีย์ลัด, อีเมลล์, เชื่อมบัญชี, etc.)|

### 📄 Status & Staging

|Command|Description|
|:-|:-|
|`git status`|เช็คสถานะของไฟล์ใน repository (staged, modified, untracked)|
|`git add <file>`|เลือกไฟล์ที่ต้องการจะ save (add ไป staging area)|
|`git commit -m "massage"`|ยืนยันการ save พร้อมใส่คำอธิบาย (massage)|

### ☁️ GitHub / Remote

|Command|Description|
|:-|:-|
|`git remote add origin <URL>`|ผูก repo local กับ GitHub repo|
|`git push`|อัปโหลดงานขึ้น GitHub|
|`git pull`|ดึง (update) จาก GitHub|
|`git clone <URL>`|โหลด repo จาก GitHub ลงเครื่อง|

### 🌿 Branch

|Command|Description|
|:-|:-|
|`git branch`|ดู branch ทั้งหมด / สร้าง branch ใหม่|
|`git checkout <branch>`|สลับไป branch อื่น หรือ load checkpoint (commit)|
|`git checkout -b <branch>`|สร้าง branch ใหม่และสลับไปใช้|
|`git merge <branch>`|รวม branch เป้าหมายเข้ากับ branch ปัจจุบัน|

### 🚫 .gitignore

|File name|Description|
|:-|:-|
|`.gitignore`|กำหนดไฟล์ที่ไม่ให้ git track (เช่น key, ไฟล์ชั่วคราว) |

---

## 🔁 Git Flow

### 📘 Git Flow Command

|Command|Description|
|:-|:-|
|`git flow init`|ตั้งค่า Git Flow ครั้งแรก |
|`git flow <type> start <name>`|สร้าง branch และ checkout ไปยัง branch นั้นทันที               |
|`git flow <type> finish <name>`|merge กลับเข้า branch หลัก + ลบ branch (เฉพาะ feature/hotfix) -> พร้อมสร้าง tag เวอร์ชัน(เฉพาะ release/hotfix)|
|`git flow <type> publish <name>`|push branch ขึ้น remote|
|`git flow <type> pull <name>`|ดึง branch จาก remote มา local|

### 🌿 Git Flow Branch

|Branch|ใช้ทำอะไร|
|:-|:-|
|`main`|branch หลักสำหรับ production (โปรแกรมจริง)|
|`develop`|สำหรับพัฒนาและรวม feature ทั้งหมด|
|`feature/<name>`|ใช้พัฒนา feature ใหม่|
|`release/<version>`|เตรียม release, QA และ แก้บัคก่อน deploy|
|`hotfix/<version>`| แก้บัคด่วนที่เกิดขึ้นใน production (main)|

### ✅ ขั้นตอนการทำงาน Git Flow

1. เริ่มจาก `Branch main` ด้วยการสร้าง local Git repository

    ```bash
    git init
    ```

2. ตั้งค่า Git Flow แล้วสร้าง `Branch develop`

    ```bash
    git flow init
    ```

3. เริ่มพัฒนา feature
    ###### สร้าง `Branch feature` จาก `Branch develop` -> ย้าย(checkout)ไปยัง `Branch feature` 
    ```bash
    git flow feature start <name>
    ```

4. เมื่อพัฒนา feature เสร็จ
    ###### merge `Branch feature` เข้ากับ `Branch develop` -> ลบ `Branch feature` -> ย้าย(checkout)ไปยัง `Branch develop`
    ```bash
    git flow feature finish <name>
    ```

5. เมื่อโปรแกรมพร้อมจะปล่อยแล้ว:
    ###### สร้าง `Branch release` จาก `Branch develop` -> ย้าย(checkout)ไปยัง `Branch release` 
    ```bash
    git flow release start <version>
    ```

6. เมื่อ QA เสร็จและพร้อมปล่อยจริง:
    ###### merge `Branch release` เข้ากับ `Branch main` และ `Branch develop` -> พร้อมสร้าง tag เวอร์ชัน
    ```bash
    git flow release finish <version>
    ```

7. ถ้าเจอบัคที่ต้องได้รับการแก้ไขด่วนใน `Branch main`:
    ###### สร้าง `Branch hotfix` จาก `Branch main` -> ย้าย(checkout)ไปยัง `Branch hotfix` 
    ```bash
    git flow hotfix start <name>
    ```

8. แก้เสร็จให้ merge กลับเข้า main:
    ###### merge `Branch hotfix` เข้ากับ `Branch main` และ `Branch develop` -> ลบ `Branch hotfix` -> ย้าย(checkout)ไปยัง `Branch main` -> พร้อมสร้าง tag เวอร์ชัน
    ```bash
    git flow hotfix finish <name>
    ```

> [!NOTE]     
> หลังรัน `git flow release/hotfix finish <version>` Git-flow จะ **merge** โค้ดเข้าทั้ง `main` และ `develop` แล้วสร้าง **annotated tag**  (เช่น `v1.2.0`) ไว้ใน local เท่านั้น. เพื่อให้ทีมสามารถใช้งาน(checkout)เวอร์ชันนี้ได้ **อย่าลืม push tag ไปที่ remote** ด้วย `git push origin --tags`

---

## 💻 Terminal 101

### 📃 Basic Terminal Command

|Command|Description|
|:-|:-|
|`cls`|เคลียร์หน้าจอ Terminal|
|`dir`|แสดงรายการไฟล์/diretory|

### 📁 Directory Commands

|Command|Description|
|:-|:-|
|`cd <folder>`|เปิด/เปลี่ยน diretory|
|`mkdir <folder>`|สร้าง diretory|
|`rmdir <folder>`|ลบ diretory(ต้องเป็น diretory เปล่า)|

### 📄 File Commands

|Command|Description|
|:-|:-|
|`start <file>`|เปิดไฟล์|
|`echo > <file>`|สร้าง/เขียนทับไฟล์|
|`del <file>`|ลบไฟล์|

### 📦 Move & Rename Commands

|Command|Description|
|:-|:-|
|`move <file> <path>`|ย้ายไฟล์ไปยัง path ที่กำหนด|
|`move <oldname> <newname>`|เปลี่ยนชื่อไฟล์|

```bash
move file.txt ..        # ย้ายไป parent directory
move old.txt new.txt    # เปลี่ยนชื่อ
```

---

## Credits

- **Paula Santamaría** - For more information, visit [Command-Line Interfaces: Structure & Syntax](https://dev.to/paulasantamaria/command-line-interfaces-structure-syntax-2533)
- **Somkiat Puisungnoen** - For more information, visit [มาหาแนวทางการใช้ git ของคุณ และ ทีม กันดีกว่า](https://www.somkiat.cc/find-your-git-workflow/)
- **Tinnakorn Maneewong** - For more information, visit [Git flow คืออะไร มาลองใช้ Git flow กันเถอะ](https://dev.classmethod.jp/articles/introduce-git-flow-th/)
- **Daniel Kummer** - For more information, visit [git-flow cheatsheet](https://danielkummer.github.io/git-flow-cheatsheet/)
