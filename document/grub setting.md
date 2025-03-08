# grub time change

## 1 **. Open the GRUB configuration file:**

You need to edit the `/etc/default/grub` file with root privileges. You can use a text editor like `nano`, `vim`, or `gedit`. Here's how to open it with `nano`:

```bash
sudo nano /etc/default/grub
```
## **2. Find the `GRUB_TIMEOUT` line:**

In the file, look for the line that starts with `GRUB_TIMEOUT`. It might be set to a different value (like `5` or `0`) or it might be commented out with a `#` at the beginning.

```
GRUB_TIMEOUT=5
```

## **3. Change the `GRUB_TIMEOUT` value to `10`:**

Modify the line to set the timeout to 10 seconds:

```
GRUB_TIMEOUT=10
```

_If the line is commented out (starts with `#`), remove the `#` and then set the value to `10`._

## **4. (Optional) Ensure the GRUB menu is displayed:**

If you want to make sure the GRUB menu is always displayed, even if you only have one operating system, you can check the `GRUB_TIMEOUT_STYLE` line. Ensure it is set to `menu` or `show`:

```
GRUB_TIMEOUT_STYLE=menu
```

or

```
GRUB_TIMEOUT_STYLE=show
```

If you want a hidden menu that only appears if you press a key, you can use `GRUB_TIMEOUT_STYLE=hidden`, but make sure `GRUB_TIMEOUT` is set to a value greater than 0 for it to work.

## **5. Save the file:**

- **If you are using `nano`:** Press `Ctrl + O` to write out (save) the file, then press `Enter` to confirm the filename, and then `Ctrl + X` to exit `nano`.
- **If you are using `vim`:** Press `Esc` to enter command mode, then type `:wq` and press `Enter` to write and quit.
- **If you are using `gedit` (or another graphical editor):** Click the "Save" button and then close the editor.


## 6. **Update GRUB**:

This is the crucial step to apply the changes you made to the grub file. Run the following command in the terminal:
Bash

```
sudo update-grub
```

This command will regenerate the GRUB configuration file (/boot/grub/grub.cfg) based on the settings in /etc/default/grub and other configuration files.
### 1. Reboot your system:

Restart your computer to see the changes in the GRUB menu:
Bash

```
sudo reboot
```

Now, when your system starts, you should see the GRUB menu for 10 seconds before it automatically boots into the default operating system.

> [!note]
>    update-grub is essential: Simply editing /etc/default/grub will not change the GRUB timeout. You must run sudo update-grub for the changes to be applied.

> [!note]
Manjaro GRUB: Manjaro uses a customized GRUB. Make sure you are modifying the correct /etc/default/grub file for your Manjaro installation, especially if you have a dual-boot setup. Usually, running sudo update-grub from within Manjaro will update the correct GRUB configuration.

> [!note] 
No Errors: If you encounter errors when running sudo update-grub, carefully check the changes you made to /etc/default/grub for typos or incorrect syntax.