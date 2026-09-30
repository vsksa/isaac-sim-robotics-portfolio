

## Isaac Sim 6.1 Installation on Windows


### System Configuration

| Component | Specification |
|---|---|
| Laptop | Lenovo Legion Pro 5i |
| CPU | Intel Core Ultra 9 275HX |
| GPU | NVIDIA GeForce RTX 5070 Ti Laptop GPU |
| Dedicated VRAM | 12 GB |
| RAM | 32 GB |
| Storage | 1 TB SSD |
| Operating System | Windows 11 Home |
| NVIDIA Driver | 592.01 |
| Isaac Sim Version | 6.1.0 |

> Isaac Sim 6.1 officially specifies 16 GB of VRAM as its minimum. My
> system has 12 GB, so I plan to begin with tutorials and small-to-medium
> simulation environments.

### 1. Verify the NVIDIA GPU

I opened Command Prompt and ran: nvidia-smi
This gave me the following output.
Wed Sep 30 12:38:51 2026
+-----------------------------------------------------------------------------------------+
| NVIDIA-SMI 592.01                 Driver Version: 592.01         CUDA Version: 13.1     |
+-----------------------------------------+------------------------+----------------------+
| GPU  Name                  Driver-Model | Bus-Id          Disp.A | Volatile Uncorr. ECC |
| Fan  Temp   Perf          Pwr:Usage/Cap |           Memory-Usage | GPU-Util  Compute M. |
|                                         |                        |               MIG M. |
|=========================================+========================+======================|
|   0  NVIDIA GeForce RTX 5070 ...  WDDM  |   00000000:02:00.0 Off |                  N/A |
| N/A   49C    P0             15W /   95W |       0MiB /  12227MiB |      0%      Default |
|                                         |                        |                  N/A |
+-----------------------------------------+------------------------+----------------------+

+-----------------------------------------------------------------------------------------+
| Processes:                                                                              |
|  GPU   GI   CI              PID   Type   Process name                        GPU Memory |
|        ID   ID                                                               Usage      |
|=========================================================================================|
|  No running processes found                                                             |
+-----------------------------------------------------------------------------------------+

2. Download Isaac Sim
I installed the standalone Windows version of NVIDIA Isaac Sim 6.1.0 on
my Lenovo Legion Pro 5i by downloading it from the following link.
Here is the link https://docs.isaacsim.omniverse.nvidia.com/latest/installation/download.html
The downloaded ZIP file was initially saved in the Windows Downloads
folder.

3. Extract Isaac Sim
I extracted the package into a short directory on the local C: drive:
C:\isaacsim
Using a short installation path helps avoid Windows path-length problems.
After extraction, I confirmed that the following required file existed:

4. Run the Installation Scripts
I opened Command Prompt in admin  mode, changed to the Isaac Sim installation directory,
and ran three batch files in sequence:
cd /d C:\isaacsim
post_install.bat
isaac-sim.compatibility_check.bat
isaac-sim.bat

The scripts perform the following operations:
1. post_install.bat
   - Completes the post-installation configuration.
   - Creates a symbolic link for the extension examples.
2. isaac-sim.compatibility_check.bat
   - Checks the operating system, CPU, RAM, NVIDIA GPU, VRAM, and driver.
3. isaac-sim.bat
   - Starts the main NVIDIA Isaac Sim application.
  
Installation Issues and Solutions
Batch window opened and closed immediately
When I initially double-clicked post_install.bat, a Command Prompt window
opened and closed immediately.
I resolved this by opening Command Prompt first and running the script from
the Isaac Sim installation directory. This allowed me to read its output
and identify errors.

Insufficient symbolic-link privileges
The first post-installation attempt displayed:
You do not have sufficient privilege to perform this operation.
Symlink extension_examples not created.

This occurred because Windows did not allow the script to create a symbolic
link.
The solution was to run Command Prompt as Administrator. Windows Developer
Mode can also allow symbolic-link creation without an elevated terminal.
Compatibility checker could not find the specified path
The compatibility checker initially displayed:

The system cannot find the path specified.
Investigation showed that the required file below was missing:
C:\isaacsim\kit\kit.exe
The file was present inside the downloaded ZIP, which indicated that the
first extraction was incomplete.
I extracted the package again with 7-Zip into the short C:\isaacsim
directory and verified that kit\kit.exe was present before rerunning the
batch files.
