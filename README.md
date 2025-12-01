# Vizy Path Mapper

**Version:** 1.0.0  
**Author:** Onur Unlu (Vizy3D)  
**Compatibility:** Blender 4.0+ (Windows & Linux)  
**Category:** Pipeline / System

## 🚀 Overview

**Vizy Path Mapper** is a professional pipeline tool designed to handle broken file paths in Blender. It automatically remaps absolute paths based on user-defined rules, making it essential for:

1.  **Cross-Platform Workflows:** Moving projects between Windows (Drive Letters) and Linux (Mount Points).
2.  **Client Handovers:** Opening external projects where the file structure differs from your local storage (e.g., Client used `Y:\Project`, you stored it in `D:\Clients\ClientName\Project`).

It runs globally and automatically, ensuring that assets load correctly without modifying the original `.blend` file structure destructively.

---

## 🎯 Common Use Cases

### Scenario A: The "Client Handover" (Deep Path Remapping)
A client sends a project linked to their internal server structure. You save it to your local customer archive.
* **Incoming Path (Client):** `Y:\Avatar_Project\Shots\cg_015\textures\wood.jpg`
* **Your Local Path:** `D:\Customers\WarnerBros\Avatar_Project\Shots\cg_015\textures\wood.jpg`
* **The Fix:** You simply create a rule mapping `Y:` to `D:\Customers\WarnerBros\`. The add-on handles the rest automatically.

### Scenario B: Mixed OS Pipeline (Windows <-> Linux)
You work on Linux, but receive files from a Windows freelancer.
* **Incoming Path (Windows):** `M:\Assets\Characters\Hero.blend`
* **Your Local Path (Linux):** `/mnt/M/Assets/Characters/Hero.blend`
* **The Fix:** Map `M:` to `/mnt/M`.

*Note: This works both ways. If you create a file on Linux (`/mnt/Projects`), a Windows user can map `/mnt/Projects` to `Z:\Projects` to open your file seamlessly.*

---

## ✨ Key Features

* **Prefix Swapping:** Replaces any starting directory path, not just drive letters. Works for complex folder structures.
* **Global Rules:** Set your mappings once in the Add-on Preferences; they apply to every file you open.
* **Auto-Run Handler:** Hooks into Blender’s `load_post` routine to fix paths instantly upon opening a file.
* **Absolute Path Enforcer:** Automatically forces target paths to be **Absolute**, preventing broken relative links when switching between different project directories.
* **Smart UI:**
    * **Source Input:** Manual entry for missing/foreign drive letters.
    * **Target Input:** Native folder selector to ensure the local path exists.

---

## 📦 Installation

1.  Download **`vizy_path_mapper.zip`**.
2.  In Blender, go to **Edit > Preferences > Add-ons**.
3.  Click **Install...** and select the zip file.
4.  Enable **Pipeline: Vizy Path Mapper**.

---

## ⚙️ How to Configure

Go to **Edit > Preferences > Add-ons > Vizy Path Mapper**.

### 1. Mapping a Client Project
If the client worked on `Y:\Film\Shot_01`, but you have the files at `D:\Work\Film\Shot_01`:

* **Add Rule**
* **Source (Windows/Incoming):** `Y:\`
* **Target (Local):** Select your local folder: `D:\Work\`
* *Result:* Blender will look for `D:\Work\Film\Shot_01...` instead of `Y:\Film\Shot_01...`

### 2. Mapping for Linux (Standard Pipeline)
* **Add Rule**
* **Source:** `M:`
* **Target:** `/mnt/M`

### 3. Automation
Ensure **"Auto-Run on File Load"** is checked. The remapping happens silently in the background every time you open a file.

---

## 🔧 Technical Notes

* **Non-Destructive:** The tool updates the file paths in memory when loaded. If you save the file, the new paths are saved.
* **String Matching:** It uses a "Starts With" logic. It finds the matching prefix in the file path and swaps it with your local target string.
* **Supported Data:** Images, Libraries (Linked Files), Volumes (VDB), and Cache files.

---

## 📝 License

Developed for internal VFX pipeline efficiency.
