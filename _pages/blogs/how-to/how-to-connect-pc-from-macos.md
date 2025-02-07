---
title: How to Connect PC from macOS
permalink: /blogs/how-to-connect-to-pc-from-macos
medium: blog
category: how-to
---

## **1. Find Your Windows PC’s IP Address**  

On the Windows PC, open **Command Prompt** and type:  

```sh
ipconfig
```  

Note the **IPv4 Address** (e.g., `192.168.1.100`).

## **2. Enable Remote Desktop on Windows**  

1. Go to **Settings > System > Remote Desktop**.  
2. Turn on **Remote Desktop** and note your **PC name**.  
3. Disable **Network Level Authentication (NLA)**:  
   - Open **Run (`Win + R`)**, type `sysdm.cpl`, and press **Enter**.  
   - Go to the **Remote** tab and **uncheck**:  
     ✅ "Require computers to use Network Level Authentication (NLA) to connect".  
   - Click **Apply** and **OK**.

## **3. Install & Set Up Microsoft Remote Desktop on macOS**  

1. Download **Microsoft Remote Desktop** from the **Mac App Store**.  
2. Open the app and click **"+" > Add PC**.  
3. Under **PC Name**, enter the **IP address** of your Windows PC.  
4. Under **User Account**, enter your **Azure AD credentials**:  

   ```text
   <AzureAD>\user.name
   ```

5. Click **Save**, then **double-click the PC** to connect.
