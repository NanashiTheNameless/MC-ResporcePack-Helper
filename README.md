# MC-ResporcePack-Helper
helper for minecraft resource packs.
This Program ONLY Suppords Windows 7, 8 and Windows 10.

code is as follows:
`<# : chooser.bat
  @echo off
  :begenning
  setlocal
  set pwshcmd=powershell -noprofile -command "&{[System.Reflection.Assembly]::LoadWithPartialName('System.windows.forms') | Out-Null;$OpenFileDialog = New-Object System.Windows.Forms.OpenFileDialog; $OpenFileDialog.ShowDialog()|out-null; $OpenFileDialog.FileName}"
  for /f "delims=" %%I in ('%pwshcmd%') do set "selectedFile=%%I" (
  set /P c=You Selected %selectedFile% Is This Correct? [y/n] *must be lowercase*
  if /I "%c%" EQU "y" goto :copy 
  if /I "%c%" EQU "n" goto :begenning 
  )
  :copy
  echo copying %selectedFile% to minecraft resourcepacks folder!
  xcopy "%selectedFile%" "%appdata%/.minecraft/resourcepacks"
  pause
  exit
  goto :EOF
  : end Batch portion / begin PowerShell hybrid chimera #>
  Add-Type -AssemblyName System.Windows.Forms
  $f = new-object Windows.Forms.OpenFileDialog
  $f.InitialDirectory = pwd
  $f.Filter = "Zipped Files (*.zip)|*.zip|All Files (*.*)|*.*"
  $f.Multiselect = $false
  [void]$f.ShowDialog()
  if ($f.Multiselect) { $f.FileNames } else { $f.FileName }`
