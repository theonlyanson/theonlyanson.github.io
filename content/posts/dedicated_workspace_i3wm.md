+++
title = 'Assigning a Dedicated Workspace for Specific Applications in i3wm'
date = 2025-03-24T15:51:49+05:30
draft = false
tags = ["i3wm","Linux","window manager","tiling","workspace management"]
+++

![i3wm](/img/i3wm.jpg)
# Assigning a Dedicated Workspace for Specific Applications in i3wm

In this guide, I’ll show you how to assign specific applications to dedicated workspaces in `i3wm`, a tiling window manager for Linux. By doing this, you can streamline your workflow by ensuring that certain applications always open in their designated workspace, making your setup more organized and efficient.

---

## ✅ **Step 1: Identify the Application Class Name**

To assign an application to a specific workspace, you need to first identify its **class name**. This is essential because `i3wm` uses the window class name to match the application.

### **1.1. Launch the Application**
Open the application you want to assign to a dedicated workspace. For example, if you want to assign Firefox, launch it by running:

```bash
firefox &
```

### **1.2. Use `xprop` to Find the Class Name**
`xprop` is a tool used to retrieve window properties. Run the following command and then click on the window of the application you want to assign:

```bash
xprop | grep WM_CLASS
```

- **Explanation:**  
    - `xprop`: Launches the window property inspector.  
    - `| grep WM_CLASS`: Filters the output to show only the class information.

### **1.3. Interpret the Output**
You will see an output similar to this:

```
WM_CLASS(STRING) = "Navigator", "firefox"
```

- The output consists of two parts:  
    - The **first value** (`Navigator`) is the instance name.  
    - The **second value** (`firefox`) is the class name.  
- For workspace assignment, you’ll need the **second value** (`firefox` in this case).

---

## 🔧 **Step 2: Modify the i3wm Configuration File**

Once you have the class name, you can assign it to a specific workspace by editing your i3wm configuration file.

### **2.1. Open the Configuration File**
Use a text editor to open the i3 configuration file:

```bash
nano ~/.config/i3/config
```

### **2.2. Add the Workspace Assignment**
Add the following line at the end of the configuration file:

```bash
assign [class="<application_class>"] <workspace_number>
```

- Replace `<application_class>` with the class name you got from `xprop`.  
- Replace `<workspace_number>` with the workspace number where you want the application to open.

### **Example**
If you want Firefox to always open in workspace `2` and Terminal (Alacritty) in workspace `1`, add:

```bash
assign [class="firefox"] 2
assign [class="Alacritty"] 1
```

- This ensures Firefox always opens on workspace `2`, and Alacritty on workspace `1`.

---

## 🔄 **Step 3: Reload i3wm Configuration**

After making the changes, reload the i3wm configuration to apply the new workspace rules:

```bash
i3-msg reload
```
or
```bash
Mod+Shift+R
```
- `Mod` is usually mapped to the `Super` (Windows) key.

---

## 🚀 **Step 4: Verify the Workspace Assignment**

To verify, close the applications and reopen them. They should automatically launch in their assigned workspaces.

---

## 🛠️ **Tips and Tricks**

1. **Assign Multiple Applications to the Same Workspace:**  
    You can assign multiple applications to the same workspace by separating them with a comma:

    ```bash
    assign [class="firefox"], [class="Chromium"] 2
    ```

2. **Use Floating Windows:**  
    If you want specific applications to open in floating mode, you can add:

    ```bash
    for_window [class="pavucontrol"] floating enable
    ```

3. **Check Config Syntax:**  
    After editing, ensure there are no syntax errors by running:

    ```bash
    i3-msg reload
    ```

---

## 🎯 **Conclusion**

By assigning dedicated workspaces for specific applications in `i3wm`, you can enhance your productivity and keep your desktop environment organized. This setup ensures that your frequently used applications always open where you expect them, streamlining your workflow.

---

✅ **Tip:** If you want to explore more i3wm customization options, check out the [official i3wm documentation](https://i3wm.org/docs/userguide.html).

---

📌 *Tags: i3wm, Linux, window manager, tiling, workspace management*
