### navigate to download page to get fedora remix
https://github.com/WhitewaterFoundry/WSLFedoraRemix/releases
#### update filename from .appxbundle to .zip then extract
`rename-item Path-location Path Location`
#### do the same for the .appx to .zip then extract that
`rename-item Path-locatio Path Location`
`extract-archive Path-Location Path-Location`
#### run the .exe file
#### set the path as needed
`$userenv = [System.Environment]::GetEnvironmentVariable("Path", "User")
[System.Environment]::SetEnvironmentVariable("PATH", $userenv + "C:\Users\Administrator\Ubuntu", "User")`

#### Thats it
