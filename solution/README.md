# About

Here you will find my solution for UWP version

this solution will help you to select the games folder only once

then you access to it directly from <b>Load Content</b>

multiple locations supported


# Why?

Libretro starts to use new Storage API Since 1.9.10 or below

it's only supported on build 17134+

and still you cannot access to the files directly from <b>Load Content</b>

but with this solution you will be able to access to the games from <b>Load Content</b>


# Note

- These changes applied on 1.9.13 and below, not tested on newer versions

- Don't copy and replace the files here directly, follow the steps below


# Steps

- Goto <b>uwp</b> and Open <b>uwp_main.cpp</b>

- add <b>char* uwp_picker_recents[100];</b> under <b>win32_cpu_model_name</b>

- add <b>bool isAppReady = false;</b> after as well (will be used later)

<br/>

- Goto <b>libretro-common</b> -> <b>vfs</b>

- Replace <b>vfs_implementation_uwp.cpp</b> with the one we have

<br/>

- Goto <b>uwp</b> folder

- Check <b>uwp_func.h</b> and add what is missing from our files

<br/>

- Goto <b>frontend</b> -> <b>drivers</b>

- Open <b>platform_uwp.c</b> search for <b>frontend_uwp_parse_drive_list</b>

- Open our file and update the changes till the line with <b>menu_entries_append_enum</b>

- Be sure you disabled <i>DWORD drives = ...+all related code</i> it's not helpful in UWP

<br/>
	
- Goto <b>menu</b> -> <b>cbs</b>

- Open <b>menu_cbs_ok.c</b> search for <b>action_ok_open_picker</b>

- Update the function as to be like in the file we have

<br/>
After these changes you will be able to use <b>Load Content</b> correctly
 

# More

There is an issue will cause crash if you bring the app from background using it's launcher icon

- Goto <b>uwp</b> and open <b>uwp_main.cpp</b>

- Search for <b>App::Load(Platform::String^ entryPoint)</b>

- Add this at the first line: <b>if(isAppReady){return;}</b>

- Add this at the end of the function: <b>isAppReady = true;</b>

<br/>
Now the app no longer will crash if called again from it's launcher


Hope these will help you

If you faced any issues contact me <a href="mailto:services@astifan.online">services@astifan.online</a>