# Box Sync 4 Installer

## What were we trying to solve?

Some of the apps used at JAMF Software are updated frequently enough that they are tedious to maintain packages for, but there are not enough of them to warrant the use of a setup like AutoPkg. A few of these are small enough that they could be downloaded on-demand without impacting our network or causing a significant delay in install time to the user. Box Sync was the first app to be a scripted install from Self Service.

## What does it do?

The script downloads the Box Sync DMG from the static download URL at https://app.box.com/sync4mac, mounts the DMG, copies the app to the Applications directory, copies the com.box.sync.bootstrapper file into /Library/PrivilegedHelperTools (see Box's deployment article here for more details), executes the same file from within the app bundle (allowing Box Sync to be opened without a prompt for admin credentials), and the app is automatically opened for the user to log into.

Because the latest version of Box Sync is always available from the above URL, the installer policy never needs to be updated (unless, of course, the download URL were to change).

## How to deploy this script in a policy

Upload the script to your JSS and create a policy. As this script will kill running Box Sync processes and delete pre-existing copies of apps from the Applications directory, we have our policy set to be available "Ongoing" to "All Computers" so users can reinstall over the existing copy. This script has been tested against 10.8, 10.9 and 10.10 clients.

## License

```
Copyright (c) 2015, JAMF Software, LLC. All rights reserved.

Redistribution and use in source and binary forms, with or without modification, are
permitted provided that the following conditions are met:

    * Redistributions of source code must retain the above copyright notice, this
      list of conditions and the following disclaimer.
    * Redistributions in binary form must reproduce the above copyright notice, this
      list of conditions and the following disclaimer in the documentation and/or
      other materials provided with the distribution.
    * Neither the name of the JAMF Software, LLC nor the names of its contributors
      may be used to endorse or promote products derived from this software without
      specific prior written permission.
      
THIS SOFTWARE IS PROVIDED BY JAMF SOFTWARE, LLC "AS IS" AND ANY EXPRESS OR IMPLIED
WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY
AND FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL JAMF SOFTWARE,
LLC BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR
CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS
OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED
AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT
(INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE,
EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
```