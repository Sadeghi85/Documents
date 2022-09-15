

# Server 2019

1. Install the WSL optional feature using PowerShell
	* `Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux`
2. Enable the Virtual Machine Platform
	* `dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart`
3. Install VC Runtime 2019
	* `https://docs.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170`
4. Download a Linux distribution
	* `https://docs.microsoft.com/en-us/windows/wsl/install-manual#downloading-distributions`
5. Extract and install a Linux distribution
	* `Rename-Item .\Ubuntu2204-220620.AppxBundle .\Ubuntu2204-220620.zip`
	* `Expand-Archive .\Ubuntu2204-220620.zip .\Ubuntu2204-220620`
	* `Rename-Item .\Ubuntu2204-220620\Ubuntu_2204.0.10.0_x64.appx .\Ubuntu2204-220620\Ubuntu_2204.0.10.0_x64.zip`
	* `Expand-Archive .\Ubuntu2204-220620\Ubuntu_2204.0.10.0_x64.zip .\Ubuntu2204-220620\Ubuntu_2204.0.10.0_x64`
6. Run the exe file
	* `.\Ubuntu2204-220620\Ubuntu_2204.0.10.0_x64\ubuntu2204.exe`
7. Add your Linux distribution path to the Windows environment PATH (`C:\Ubuntu\Ubuntu2204-220620\Ubuntu_2204.0.10.0_x64` in this example), using PowerShell
	* `$userenv = [System.Environment]::GetEnvironmentVariable("Path", "User")`
	* `[System.Environment]::SetEnvironmentVariable("PATH", $userenv + ";C:\Ubuntu\Ubuntu2204-220620\Ubuntu_2204.0.10.0_x64", "User")`
	* `ubuntu2204.exe`