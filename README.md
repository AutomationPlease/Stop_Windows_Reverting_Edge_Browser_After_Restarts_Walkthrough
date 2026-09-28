## Stop_Windows_Reverting_Edge_Browser_After_Restarts_Walkthrough

*This walkthrough was made out of annoyance of dealing with the default browser reverting issue.*</br>

Use any browser of your choosing. This walkthrough will be using Chrome.


## Steps
1. Set defaults for Chrome for everything in Settings, Default Apps. Make sure there are no Edge instances still being used.
2. Disable Edge background processes
   - Open Microsoft Edge, go to Settings, then System and Performance.
   - Turn off the following:
     - Startup boost
     - Continue running background apps when Microsoft Edge is closed
3. Press `Win + r`, type `regegit`, hit enter.
4. Go to this Key: `HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\Explorer`
   - Create the `Explorer` key if it does not already exist.
5. Create a new `DWORD (32-bit) Value` named `NoOpenWith` and set it to `1`
    - In the right pane of the explorer key, right click an empty space
    - Choose New, DWORD 32bit Value
    - You should see a near value appear named New Value #1
    - Right click this new value and choose Rename.
    - Call it `NoOpenWith`.
    - Press enter.
    - Double click the `NoOpenWith` value.
    - In the edit window:
      - Value data: 1
      - Make sure Base is set to Hexadecimal
      - Click ok.
    - It should now look like this in the right pane:
      - Name: `NoOpenWith`
      - Type: `REG_DWORD`
      - Data: `0x00000001 (1)`
    - Important notes:
      - The exact path should be: `HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\Explorer`
      - If you already have a value called `NoOpenWith`, just edit its data to `1`.
6. Restart PC, upon reboot, go to default apps in settings and check to see if your browser choice stuck.

This prevents Windows from automatically resetting file associations after updates/reboots (major updates might change this)

## Final Notes
- Even with disabling all of the Edge background processes there are still going to be instances running on Windows 10/11 machines. They will be called something like `msedgewebview2.exe`.
  - `msedgewebview2.exe` is not a full Edge browser.
  - It's an annoying lightweight web rendering engine (I think based on Chromium) that alot of Windows apps and programs use in the background (they steal yo data between each other).
    - File explorer, Settings app, Microsoft store, Office apps, etc.. All use this Edge background process.
    - Most if not all will be at 0% CPU usage.
  - You can attempt to mitigate these in task manager but you'll find yourself back there repeating it all over and over again.
  - I just ignore them and move on.
