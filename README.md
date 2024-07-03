# Windows Firewall Configuration

This repository contains instructions for configuring firewall rules in Windows set to allow remote desktop connection and retrieving firewall profile configurations using PowerShell.

## Configure a Firewall Rule in Windows

### Steps to Enable Remote Desktop and Configure Firewall

1. **Attempt to Connect to DC1 from FS01**

   - **Log in to FS01:**
     Sign in as `Contoso\Administrator` using the password `*********!`.

   - **Open Remote Desktop Connection:**
     Navigate or search for Remote Connection on FS01
     Enter the IP address or hostname of DC1 and click "Connect".
     The connection will fail because the firewall on DC1 is not configured to allow Remote Desktop connections.

2. **Enable Remote Desktop on DC1 Using Server Manager**

   - **Log in to DC1:**
     Sign in as `Contoso\Administrator` using the password `*********!`.

   - **Open Server Manager:**
     Click on the "Server Manager" icon on the taskbar.

   - **Enable Remote Desktop:**
     In Server Manager, click on "Local Server".
     Find the "Remote Desktop" setting and click on "Disabled".
     In the "System Properties" window, under the "Remote" tab, select "Allow remote connections to this computer".
     Ensure "Allow connections only from computers running Remote Desktop with Network Level Authentication (recommended)" is checked.
     Click "Apply" and then "OK".

3. **Configure Windows Firewall to Allow Remote Desktop Access**

   - **Open Windows Firewall Settings:**
     Search for firewall and click to open windows firewall

   - **Allow Remote Desktop Through the Firewall:**
     In the left pane, click on "Inbound Rules".
     Scroll down and look for "Remote Desktop - User Mode (TCP-In)".
     Right-click and select "Enable Rule".
     Repeat for "Remote Desktop - User Mode (UDP-In)".

     Alternatively, create a new rule:
     ```powershell
     New-NetFirewallRule -DisplayName "Allow RDP" -Direction Inbound -LocalPort 3389 -Protocol TCP -Action Allow
     ```

4. **Reconnect from FS01**

   - **Open Remote Desktop Connection:**
     Enter the IP address or hostname of DC1 and click "Connect".
     Sign in as `Contoso\Administrator` using the password `*********!`.

## Retrieve Firewall Profile Configurations

### PowerShell Commands

1. **Retrieve Profile Configurations:**
   ```powershell
   Get-NetFirewallProfile

2. **Retrieve Current Remote Desktop Firewall Rules:**
   ```powershell
   Get-NetFirewallRule -DisplayName "Remote Desktop*"

3. **Retrieve Current Windows Firewall Rules:**
   ```powershell
   Get-NetFirewallRule

   
<img width="693" alt="Screenshot 2024-07-03 at 1 50 08 PM" src="https://github.com/ModeCyber/Windows-Firewall-Configuration/assets/173691504/a5af13b4-0c9d-400e-949d-cff9ad6744cd">
<img width="801" alt="Screenshot 2024-07-03 at 1 56 37 PM" src="https://github.com/ModeCyber/Windows-Firewall-Configuration/assets/173691504/8a6e6429-f728-4c5f-9cdd-948cc32f201e">
<img width="806" alt="Screenshot 2024-07-03 at 1 57 03 PM" src="https://github.com/ModeCyber/Windows-Firewall-Configuration/assets/173691504/5f62d7d0-1ef3-41af-bef5-775b127b92c3">
<img width="791" alt="Screenshot 2024-07-03 at 1 57 11 PM" src="https://github.com/ModeCyber/Windows-Firewall-Configuration/assets/173691504/b82fce8b-eca1-4837-a4f7-fdaa4e5caf6b">
<img width="789" alt="Screenshot 2024-07-03 at 1 57 29 PM" src="https://github.com/ModeCyber/Windows-Firewall-Configuration/assets/173691504/422af6b6-9245-4a02-a0d8-daaf8c161d85">
<img width="789" alt=<img width="766" alt="Screenshot 2024-07-03 at 2 03 12 PM" src="https://github.com/ModeCyber/Windows-Firewall-Configuration/assets/173691504/655c52f2-478f-47cc-aa68-e530c56bc426">
<img width="631" alt="Screenshot 20<img width="700" alt="Screenshot 2024-07-03 at 2 04 20 PM" src="https://github.com/ModeCyber/Windows-Firewall-Configuration/assets/173691504/08e54d0f-6aa8-42e1-b478-1cbd9773da26">
<img width="1019" alt="Scre<img width="851" alt="Screenshot 2024-07-03 at 2 08 43 PM" src="https://github.com/ModeCyber/Windows-Firewall-Configuration/assets/173691504/5ba199f3-bd03-4d9c-9b9f-4398e4f54496">
<img width="875" alt="Screenshot 2024-07-03 at 2 06 33 PM" src="https://github.com/ModeCyber/Windows-Firewall-Configuration/assets/173691504/cfc886d1-37b3-4c9c-900a-51eb4b10f7db">
<img width="1019" alt="Screenshot 2024-07-03 at 2 04 46 PM" src="https://github.com/ModeCyber/Windows-Firewall-Configuration/assets/173691504/ccca65e0-5265-4bfc-b3c0-a0724bf0ced5">
<img width="875" alt="Screenshot 2024-07-03 at 2 06 33 PM" src="https://github.com/ModeCyber/Windows-Firewall-Configuration/assets/173691504/b325d2a1-76bf-4060-9ed0-994da2aadbcc">
<img width="851" alt="Screenshot 2024-07-03 at 2 08 43 PM" src="https://github.com/ModeCyber/Windows-Firewall-Configuration/assets/173691504/040547b2-1c5e-4ebc-8b16-974ebbc6657e">
