Getting Started
===============

Requirements
------------

Steam Audio requires **FMOD Studio 2.00** or later.

The Steam Audio FMOD Studio integration supports the following platforms:

-  Windows 7 or later (32-bit and 64-bit)
-  Linux (32-bit and 64-bit, tested with Ubuntu 16.04 LTS)
-  macOS 10.7 or later (64-bit Intel)
-  Android 5.0 or later (32-bit ARM, 64-bit ARM, 32-bit Intel)


Add Steam Audio to your FMOD Studio project
-------------------------------------------

To add Steam Audio to your FMOD Studio project:

1.  Download the latest version of the Steam Audio FMOD Studio integration: ``steamaudio_fmod.zip``. Extract the contents of this file to any directory of your choosing.
2.  In your project directory (this is the directory containing your project's ``.fspro`` file), create a subdirectory called ``Plugins``, if it doesn't already exist.
3.  Copy the following files from the directory you extracted ``steamaudio_fmod.zip`` into, to the ``Plugins`` directory of your FMOD Studio project.

    -   (Windows 32-bit editor only) ``lib/windows-x86/phonon.dll`` and ``lib/windows-x86/phonon_fmod.dll``
    -   (Windows 64-bit editor only) ``lib/windows-x64/phonon.dll`` and ``lib/windows-x64/phonon_fmod.dll``
    -   (macOS editor only) ``lib/osx/phonon.bundle`` and ``lib/osx/libphonon_fmod.dylib``
    -   (all platforms) ``src/phonon_fmod.plugin.js``


Spatialize an event
-------------------

Once Steam Audio is added to your project, you can spatialize any event:

1.  Select the event you want to spatialize.
2.  Click the **Master** track for the event.
3.  In the effects deck at the bottom of the window, right-click an empty spot, and choose **Add Effect** > **Plug-in Effects** > **Valve** > **Steam Audio Spatializer**.
4.  Drag the Steam Audio Spatializer to an appropriate position in the effect chain.

.. image:: media/spatializer_placement.png

If the event already contains FMOD's built-in spatializer effect, you can delete or bypass it.


Integrate Steam Audio with your game engine
-------------------------------------------

Before you can use the Steam Audio FMOD Studio integration in your game, you must configure your game engine to use Steam Audio and load the Steam Audio FMOD Studio integration.

If you are using Unity as your game engine, see the Unity tab below. Otherwise, see the C++ tab for instructions on how to configure your game engine to load the Steam Audio FMOD Studio integration via C++ code.

.. tabs::

    .. group-tab:: Unity

        These instructions assume that you have added the FMOD Studio Unity integration and the Steam Audio Unity integration to your Unity project.

        .. rubric:: Configure the FMOD Studio Unity integration to use Steam Audio

        1.  In Unity's main menu, click **FMOD** > **Edit Settings**.
        2.  Under **Dynamic Plugins**, click **Add Plugin**.
        3.  In the text box that appears, enter ``phonon_fmod``.

        .. image:: media/unity_fmodsettings.png

        .. rubric:: Configure the Steam Audio Unity integration to use FMOD Studio

        1.  In Unity's main menu, click **Steam Audio** > **Settings**.
        2.  Set **Audio Engine** to **FMOD Studio**.

        .. image:: media/unity_steamaudiosettings.png

    .. group-tab:: C++

        These instructions assume that you have integrated Steam Audio with your game engine via the Steam Audio SDK.

        .. rubric:: Load the Steam Audio FMOD Studio integration

        1.  When initializing FMOD Studio in your game engine, call ``FMOD::System::loadPlugin`` to load the Steam Audio FMOD Studio integration. The plugin files can be found in the ``steamaudio_fmod.zip`` file you downloaded earlier. The file name of the plugin depends on the platform:

            -   Windows 32-bit: ``lib/windows-x86/phonon_fmod.dll``
            -   Windows 64-bit: ``lib/windows-x64/phonon_fmod.dll``
            -   Linux 32-bit: ``lib/linux-x86/libphonon_fmod.so``
            -   Linux 64-bit: ``lib/linux-x64/libphonon_fmod.so``
            -   macOS: ``lib/osx/libphonon_fmod.dylib``
            -   Android ARMv7 (32-bit): ``lib/android-armv7/libphonon_fmod.so``
            -   Android ARMv8/AArch64 (64-bit): ``lib/android-armv8/libphonon_fmod.so``
            -   Android x86 (32-bit): ``lib/android-x86/libphonon_fmod.so``

        .. rubric:: Initialize the Steam Audio FMOD Studio integration

        2.  Call ``iplFMODInitialize`` after creating the Steam Audio context.
        3.  Create an HRTF (typically the default HRTF), and call ``iplFMODSetHRTF``.
        4.  Determine the simulation settings to use for subsequent simulations, and call ``iplFMODSetSimulationSettings``.
