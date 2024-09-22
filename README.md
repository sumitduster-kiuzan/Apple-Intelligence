apple intelligence

This actually downloads the models, and is NOT just new SiriUI. Hence, this process is complex and probably not worth it.

⚠️ Prepare to be disappointed and annoyed, and have your time wasted! ⚠️

What does not work: Writing Tools, Memories, Reduce Interruptions, Image Eraser and other tools that are within official Apple Intelligence on supported devices.
What does work: Slightly better Siri, New UI
(e.g) You can ask about the iPhone/iPad User Guide, or ask to play a specific song in Spotify, which Old Siri could not do.
⚠️ Small preface note

🧱 This will also temporarily brick your Face ID (fixable, see Fixing Face ID)
📺 This may also have some connection to breaking standby/AOD (not confirmed).
🚧 Always, only try this at your own risk 🚧

Modifying your device's MobileGestalt has a small risk of bricking your device, if done wrong.

Again, if you just want the new UI, this is NOT the tutorial you're looking for.

we (me, cowabunga) will NOT / are not obliged to provide support for this guide. You may ask for help in the Cowabunga server, but do not expect any help.

So, what does this do?

To get  Intelligence on older models:

Generative Model capability has to be added to MobileGestalt
Eligibility (regional ability, and also the "waitlist") for  Intelligence has to pass/be bypassed
Your iPhone model has to be temporarily spoofed to a newer model (e.g. 15 Pro) that is capable of  Intelligence, so that Apple servers let you download the model
Once the models are downloaded, undoing the spoofing keeps it working. It behaves as if the phone had always supported  Intelligence. But, to download these models, you first need to change your ProductType to 15 Pro or newer, wait for it to download, then revert the changes.

This is going to be a multi-stage process, with some trial and error. It doesn't always consistently initiate the download.

Part 0: Requirements

Your device must be an iPhone XS or newer, on iOS/iPadOS 18.1 Beta 4 / 18.1 Public Beta (or newer?)

Part 1: Gestalt modification

Grab a fresh .plist copy of your MobileGestalt file using the shortcut.
Make a backup copy somewhere! You will need this later, and if you want to revert this tweak.
Every time you apply any changes to your phone, such as updating it, run the shortcut again, and import/use the new MobileGestalt file instead.
Spoof your ProductType (Device Model)

Open the .plist file with ANY file editor, use CTRL + F to find h9jDsbgj7xIVeIQ8S3/X3Q. You should find the line with your iPhone/iPad model identifer under it. (Example: iPhone14,2).

Replace it with iPhone16,2 (OR iPad16,3 IF YOU ARE ON iPad) so the line should look something like this: <string>iPhone16,2</string>.

This will allow you to spoof Apple's servers into thinking you have an iPhone 15 Pro (or well iPad Pro M4), which enables you to download the models, but also is what will break Face ID temporarily (due to part seralisation.)

Add the Generative Model capability

Now, after this line in the file:

<key>CacheExtra</key>
  <dict>
add these 2 lines (the indentation does not matter)

<key>A62OafQ85EJAiiqKn4agtg</key>
<integer>1</integer>
Now, go to Nugget and apply the modified MobileGestalt .plist file to your device, then reboot.

MobileGestalt File path: /var/containers/Shared/SystemGroup/systemgroup.com.apple.mobilegestaltcache/Library/Caches/com.apple.MobileGestalt.plist
Part 2: Bypass the "Waitlist" / Eligibility

If you are in China, or don't see it after lots of trying, look at the Regional Requirements section You should now have the Apple Intelligence tab appear in Settings on your device.
If so, go to MisakaX then add the modified MobileGestalt .plist file then click on "Apple Intelligence (Extra)"

If it doesn't work, using the file attached to the end of this guide (scroll down eligibility.plist), go to Nugget, or Misaka and write the file to path /var/db/eligibilityd/eligibility.plist on your device.
You may have to repeat this step if you don't see the intelligence tab.

Part 3: Hope it works

Reboot your device, ensure you're connected to Wi-Fi and disable Low Battery Mode.
Then, wait upto 5 minutes to let the phone fully boot up, then close the Settings App then reopen it.
Ensure your device's region is set to the US, and the language is US English.
Ensure your Apple ID is NOT an EU account, if it is then just sign out of iCloud entirely. If still not working, redo step 2, and or make a non-EU apple ID.
Inside Apple Intelligence & Siri page:

Ensure your Apple Intelligence language is set to English: United States
If you do not have have the green/grey toggle next to "Apple Intelligence"
Wait for it to "download" for upto 15 minutes, if not then repeat step 2 and reboot.
Turn the Apple Intelligence toggle off, then back on again, then wait for it to download the models and install.
Indicators it's working:
If your phone gets very very hot
In settings > General > iPhone/iPad Storage > (scroll down) iOS, there should be "Apple Intelligence", growing from 44MB to until around 2.2GB-3GB (can vary).
If not working, you can try changing your Apple Intelligence language to something random, then wait a minute, then change it back to English: United States, then try again.
Part 4: Fixing Face ID?

You must wait for it Apple Intelligence (Siri) to be fully downloaded and working, before fixing Face ID/reverting your ProductType.
Get your modified MobileGestalt file from Part 1 (not the backup you made)
Change ProductType key (h9jDsbgj7xIVeIQ8S3/X3Q) back to the correct one for your device (e.g. iPhone14,2 or iPad12,1)
Find out at https://appledb.dev/device-selection/ if you've forgotten
By "back from part 1", you essentially need to keep the key DeviceSupportsGenerativeModelSystems
Now apply this new MobileGestalt file back to your device with Nugget.
Reboot your device, connect to Wi-Fi
Then, wait like 5 minutes again.
It should do some "downloading" for like upto 5 minutes, then the AI (Siri) should start working again!
Extra: Regional Requirements

If you get the AI option in Settings, but it disappears quickly, enable and apply the "Disable Regional Restrictions" option in Nugget.
If you are in China, first use the "Disable Shutter Sound" in MisakaX. This changes the device from Asia to Europe/USA, which should help with trying to get Apple Intelligence to work properly.
Extra: Other Information

I mean basically ensure your gestalt does not have internal storage thing...this might have broken it for me for a while (no evidence though)
You can also mess with feature flags, such as PrivateCloudCompute, TextComposer, Siri, SiriNL, etc

get  Intelligence on Intel Macs

/var/db/eligibilityd/eligibility.plist
you will find this file, make a copy of it, modify it identical to my screen (for greymatter basically: 1,4,3,3,3,3 as on the screen)
Save, do command+i on the file, click lock
Replace the old one with this one
That's it.. WITHOUT TOUCHING YOUR MAC SETTINGS, whether it's the region, the language and so on. You will be in the Apple Intelligence waiting list in Sequoia 15.1 beta 4
/System/Library/FeatureFlags/Domain
GenerativeModels.plist —> « true » to « GenerativeModelsAvailability
incomplete
Credits

@sneakyf1shy / @f1shy-dev - well, me! I figured lots of this out, and did this write-up, and other write-ups
@XeZrunner (twitter) - helping me figure all this out
@34306 - MisakaX
@lemin - Nugget
@legallywanted - Rewrote the guide a bit to make it easier to understand
@JJTech for Sparserestore/TrollRestore
pymobiledevice3
Apple (for making it so confusing)
