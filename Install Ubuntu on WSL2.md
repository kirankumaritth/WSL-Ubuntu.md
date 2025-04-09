# 🚀 **Install Ubuntu on WSL2**  
---

## 📌 **What You Will Learn**  
✅ How to enable and install **WSL** on **Windows 10** and **Windows 11**  
✅ How to install **Ubuntu 24.04 LTS** using the **Microsoft Store** or **WSL commands**  

---

## 🔧 **What You Will Need**  
✔️ **Windows 10 or 11** (physical device or virtual machine)  
✔️ **All the latest Windows updates installed**  

---

## 🛠 **Step 1: Install WSL**  
WSL can be installed from the **command line**.  

1️⃣ Open **PowerShell** as **Administrator** (Use **Windows Terminal** for the best experience).  
2️⃣ Run the following command:  

```powershell
wsl --install
```  

3️⃣ **Restart your computer** after the installation is complete.  

---

## 🏗 **Step 2: Install Ubuntu on WSL**  
There are **two methods** to install Ubuntu:  

### **📌 Method 1: Microsoft Store (GUI Installation)**  
1️⃣ Open the **Microsoft Store**.  
2️⃣ Search for your preferred Ubuntu version (**Ubuntu 24.04 LTS**).  
3️⃣ Click **"Get"** to install Ubuntu.  
4️⃣ Once installed, **launch Ubuntu** from the **Microsoft Store** or the **Windows search bar**.  

---

### **📌 Method 2: Install via WSL Commands**  
You can also install Ubuntu directly from the terminal:  

1️⃣ Open **PowerShell** as **Administrator**.  
2️⃣ Check available distributions:  

```powershell
wsl --list --online
```  

Example output:  
```
The following is a list of valid distributions that can be installed.
Install using 'wsl --install -d <Distro>'.

  NAME             FRIENDLY NAME
* Ubuntu          Ubuntu
  Debian          Debian GNU/Linux
  Ubuntu-22.04    Ubuntu 22.04 LTS
  Ubuntu-24.04    Ubuntu 24.04 LTS
```  

3️⃣ Install Ubuntu 24.04 LTS:  

```powershell
wsl --install -d Ubuntu-24.04
```  

4️⃣ Check installed distributions and WSL versions:  

```powershell
wsl -l -v
```  

Example output:  
```
  NAME            STATE           VERSION
  Ubuntu-20.04    Stopped         2
* Ubuntu-24.04    Stopped         2
```

---

## 📂 **Step 3: Install Ubuntu Without the Microsoft Store**  
If you **don't have access** to the Microsoft Store, you can install Ubuntu manually using an **imported tar file**:  

```powershell
wsl --import <DistroName> <InstallLocation> <InstallTarFile>
```
📌 **Note:** Microsoft also allows installing **Appx** and **MSIX packages** for Linux distributions. Check [Microsoft’s documentation](https://learn.microsoft.com/en-us/windows/wsl/install) for details.  

---

## 🚀 **Step 4: Run and Configure Ubuntu**  
To **launch Ubuntu 24.04**, run:  

```powershell
ubuntu2404.exe
```
🔹 The first time you open Ubuntu, you will be prompted to **create a username and password**.  
🔹 These **do not need to match** your Windows credentials.  

---

## 🔄 **Step 5: Update Ubuntu (Recommended)**  
Once Ubuntu is installed, update the system for security and stability:  

```bash
sudo apt update
sudo apt full-upgrade -y
```
🔹 Enter your **password** when prompted.  

---

## 🎉 **Enjoy Ubuntu on WSL!**  
Congratulations! 🎊 You’ve successfully installed **Ubuntu on WSL**.  

For more updates on **Ubuntu & WSL**, check out the **[Ubuntu Blog](https://ubuntu.com/blog)**. 🚀🔥 
