# ToolNetL

Stop downloading Keygens, prefer Open Source code!

Here is a recap of the long discussion process posted here, a Big thank you to those who explained the procedures, really thank you!

Remember that there have been changes over the versions, so if you want to understand the main points and anticipate future changes, reread the discussions, get your hands/fingers in!

Also remember to stop the updates.

And if the software is useful to you, consider purchasing it to support the developers behind it.

First Step:
Download DnSpy v6.1.8 win64bit (12.07.2020) (https://dnspy.org/) - A powerful open-source .NET debugging*

Close/Quit Netlimiter (NLClientApp.exe -> Task Manager - Details)
and
Stop the associated service NetLimiter Service (nlsvc.exe -> Task Manager - Services)

Open DnSpy.exe v6.1.8 win64bit (12.07.2020) as Administrator.
In DnSpy menu - Open the Netlimiter.dll file in its original installation/location (because the library is linked to other dlls) - Remember to make a copy/backup of this file, in case of mishandling.

First Change:
In Explore Assembly window:
plan summary: NetLimiter (version) => NetLimiter.dll => {} NetLimiter.Service => NLLicense -> NLLicense()
Expand Netlimiter (5.3.26), then Netlimiter.dll
Expand Netlimiter.Service
Expand NLLicense
Select NLLicense()

Right click on the code window -> "Edit this method C#"
(Or Left click on the code window -> Ctrl+Shift+E)

Replace:
this.IsRegistered = false; -> this.IsRegistered = true;

Click on Compile

Second Change:
In Explore Assembly window:
plan summary: NetLimiter (version) => NetLimiter.dll => {} NetLimiter.Service => NLServiceTemp -> InitLicense ()
Expand Netlimiter (5.3.26), then Netlimiter.dll
Expand Netlimiter.Service
Expand NLServiceTemp
Select InitLicense ()

Right click on the code window -> "Edit this method C#"
(Or Left click on the code window -> Ctrl+Shift+E)

Replace:
		DateTime expiration = installTime.AddDays(28.0);
->
		DateTime expiration = installTime.AddDays(99999.0);

Important - To avoid System.Exception error:
(In the same code window - Line 43)

Replace:
catch (Exception exception)
->
catch (System.Exception exception)

Replace here:

		catch (Exception exception)
		{
			regData = null;
			NLServiceTemp._logger.LogError(exception, "Failed to init existing license: {path}", new object[]
			{
				licensePath
			});
		}
->

		catch (System.Exception exception)
		{
			regData = null;
			NLServiceTemp._logger.LogError(exception, "Failed to init existing license: {path}", new object[]
			{
				licensePath
			});
		}
Click on Compile

If you want to do what is optional before finishing, do it!

In DnSpy, Menu - File -> Save All (or Ctrl+Shift+S) -> Click OK

Restart Netlimiter (NLClientApp.exe) and NetLimiter Service (nlsvc.exe)

Update ?
This works for version 5.3.25 and 5.3.26 (you can keep the same file for 5.3.26) but be aware that there may be future changes.

Most of the mistakes some people make are forgetting this -> Open the Netlimiter.dll file in its original installation/location (because the library is linked to other dlls)

Or sometimes this -> Stop the associated service NetLimiter Service (nlsvc.exe -> Task Manager - Services)

OPTIONAL: Change Registration Name
In Explore Assembly window:
plan summary: NetLimiter (version) => NetLimiter.dll => {} NetLimiter.Service => NLLicense => RegName ->get_RegName
Expand Netlimiter (5.3.26), then Netlimiter.dll
Expand Netlimiter.Service
Expand NLLicense
Expand RegName
Select get_RegName

Right click on the code window -> "Edit this method C#"
(Or Left click on the code window -> Ctrl+Shift+E)

Replace:
return this.<RegName>k__BackingField; -> return "YOURNAMEHERE";
(Example -> return "KupBE";)

Click on Compile
