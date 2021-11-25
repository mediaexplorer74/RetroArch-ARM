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

- add <code>char* uwp_picker_recents[100];</code> under <code>win32_cpu_model_name</code>

- add <code>bool isAppReady = false;</code> after as well (will be used later)

<br/>

- Goto <b>libretro-common</b> -> <b>vfs</b>

- Replace <b>vfs_implementation_uwp.cpp</b> with the one we have

<br/>

- Goto <b>uwp</b> folder

- Check <b>uwp_func.h</b> and add what is missing from our file

<br/>

- Goto <b>frontend</b> -> <b>drivers</b>

- Open <b>platform_uwp.c</b> search for <code>frontend_uwp_parse_drive_list</code>

- Open our file and update the changes till the line with <b>menu_entries_append_enum</b>

- Be sure you disabled <code>DWORD drives = ...+all related code</code> it's not helpful in UWP

<br/>
	
- Goto <b>menu</b> -> <b>cbs</b>

- Open <b>menu_cbs_ok.c</b> search for <code>action_ok_open_picker</code>

- Update the function as to be like in the file we have

<br/>
After these changes you will be able to use <b>Load Content</b> correctly
 

# More

There is an issue will cause crash if you bring the app from background using it's launcher icon

- Goto <b>uwp</b> and open <b>uwp_main.cpp</b>

- Search for <code>App::Load(Platform::String^ entryPoint)</code>

- Add this at the first line: <code>if(isAppReady){return;}</code>

- Add this at the end of the function: <code>isAppReady = true;</code>

<br/>
Now the app no longer will crash if called again from it's launcher

<br/>
Hope these will help you

If you faced any issues contact me <a href="mailto:services@astifan.online">services@astifan.online</a>