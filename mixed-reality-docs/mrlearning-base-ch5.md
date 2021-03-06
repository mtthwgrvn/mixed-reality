---
title: Getting started tutorials - 6. Exploring advanced input options
description: Complete this course to learn how to implement Azure Face Recognition within a mixed reality application.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: mixed reality, unity, tutorial, hololens
---

# 6. Exploring advanced input options

In this tutorial, several advanced input options for HoloLens 2 are explored, including the use of voice commands, panning gesture, and eye tracking. 

## Objectives

- Trigger events using voice commands and keywords
- Use tracked hands to pan textures and 3D objects with tracked hands
- Leverage HoloLens 2 eye tracking capabilities to select objects

## Enabling Voice Commands

In this section, two voice commands are implemented. First, the ability to toggle the frame rate diagnostics panel is introduced by saying "toggle diagnostics". Second, the ability to play a sound with a voice command is explored. The MRTK profiles and settings responsible for configuring voice commands is reviewed first.

1. In the BaseScene hierarchy, select MixedRealityToolkit. Then, in the Inspector panel, select Input and click the small Clone button to the left of the DefaultMixedRealityInputSystemProfile to open the Clone Profile popup. In the popup click Clone to create a new profile MixedRealityInputSystemProfile.

    ![mrlearning-base-ch5-1-step1a.png](images/mrlearning-base-ch5-1-step1a.png)

    This will also auto-populate the MixedRealityToolkitConfigurationProfile with the newly created MixedRealityInputSystemProfile.

    ![mrlearning-base-ch5-1-step1b.png](images/mrlearning-base-ch5-1-step1b.png)

2. In the input system profile, there are a variety of settings. For voice commands, expand the Speech section and follow the same process as in the previous step to clone the DefaultMixedRealitySpeechCommandsProfile and replace it with your own editable copy.

    ![mrlearning-base-ch5-1-step2.png](images/mrlearning-base-ch5-1-step2.png)

    In the speech command profile, you’ll notice a range of settings. For a full description of these settings, refer to the [MRTK speech documentation](<https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/Input/Speech.html>).

    By default, the general behavior is auto-start. This can be changed to manual-start, if desired. But for this example, keep it on auto-start. The MRTK comes with several default voice commands, such as menu, toggle diagnostics and toggle profiler. We will use the keyword “toggle diagnostics,” in order to turn on and off the diagnostics framerate counter. We will also add a new voice command in the steps below.

3. Add a new voice command. To do this, click the + Add a New Speech Command button. You'll see a new line that appears below the list of existing voice commands. Type the voice command you want to use. In this example, use the command “play music".

    ![mrlearning-base-ch5-1-step3.png](images/mrlearning-base-ch5-1-step3.png)

    >[!NOTE]
    >You can also set a keycode for speech commands. This allows for voice commands to trigger events upon the press of a keyboard key.

4. Add the ability to respond to voice commands. Select any object in the BaseScene hierarchy that does not have any other input scripts attached to it, for example, the MixedRealityPlayspace game object. In the Inspector panel, click Add Component, search for "speech", and select the Speech Input Handler script.

    ![mrlearning-base-ch5-1-step4.png](images/mrlearning-base-ch5-1-step4.png)

    By default, you will see two checkboxes. One is the Is Focus Required checkbox. So, as long as you are pointing at the object with a ray-eye-gaze, head-gaze, controller-gaze, or hand-gaze, the voice command will be triggered. Uncheck this checkbox so that the user does not have to look at the object to use the voice command.

5. Add the ability to respond to a voice command. To do this, click the + button that’s in the Speech Input Handler.

    ![mrlearning-base-ch5-1-step5.png](images/mrlearning-base-ch5-1-step5.png)

6. Next to Keyword, you'll see a dropdown menu. Select Toggle Diagnostics so that whenever the user says the phrase “toggle diagnostics”, it triggers an action. Note that you might need to expand Element 0 by pressing the arrow next to it.

    ![mrlearning-base-ch5-1-step6.png](images/mrlearning-base-ch5-1-step6.png)

    >[!NOTE]
    >These keywords are populated, based on the profile you edited in the step 3.

7. Add the Diagnostics System Voice Controls script to toggle the framerate counter diagnostic on and off. To do this, press Add Component, search for Diagnostics System Voice Controls script and add it from the menu. This script can be added to any object, but for simplicity, we will add it to the same object as the speech input handler.

    ![mrlearning-base-ch5-1-step7.png](images/mrlearning-base-ch5-1-step7.png)

8. Add a new response in the speech input handler. To do this, click the "+" icon to add a new response to the response list.

    ![mrlearning-base-ch5-1-step8.png](images/mrlearning-base-ch5-1-step8.png)

9. Drag the object that has the Diagnostics System Voice Controls script to the new response you just created in the previous step.

    ![mrlearning-base-ch5-1-step9.png](images/mrlearning-base-ch5-1-step9.png)

10. Click the function dropdown (where it says No Function), then Diagnostics System Voice Controls, and select the ToggleDiagnostics () function which toggles your diagnostics on and off.

    ![mrlearning-base-ch5-1-step10.png](images/mrlearning-base-ch5-1-step10.png)

    >[!IMPORTANT]
    > Before building to your device, you need to enable mic settings. To do this, click File and go to Build Settings, Player Settings and ensure that the microphone capability is set.

    Next, add the ability to play an audio file from voice command using the Octa object. Recall from [lesson 4](mrlearning-base-ch4.md) that the ability to play an audio clip from touching the Octa object was added. We will leverage this same audio source for our music voice command.

11. Select the Octa object in the BaseScene hierarchy.

12. Add another speech input handler (repeat Steps 4 and 5), but with the octa object.

13. Instead of adding the Toggle Diagnostics voice command from step 6, add the Play Music voice command as shown in the image below.

    ![mrlearning-base-ch5-1-step13.png](images/mrlearning-base-ch5-1-step13.png)

14. As with Steps 8 and 9, add a new response and drag the Octa object, the object that has the Diagnostics System Voice Controls script on it, to the empty response slot.

15. Select the dropdown menu that says No Function. Then select Audio Source, followed by PlayOneShot (AudioClip).

    ![Lesson5 Chapter1 Step15im](images/Lesson5_chapter1_step15im.PNG)

16. For this example, we are going to use the same audio clip from [Lesson 4](mrlearning-base-ch4.md). Go into your Project panel, search for “MRTK_Gem” audio clip and drag it into the audio source slot as shown in the image below. Now your application will respond to the voice commands “toggle diagnostics” to toggle the Frame Rate Counter panel and Play Music to play the MRTK_Gem song.

    ![Lesson5 Chapter1 Step16im](images/Lesson5_chapter1_step16im.PNG)

## The Pan Gesture

In this section, you will learn how to use the pan gesture. This is useful for scrolling by using your finger or hand to scroll through content. You can also use the pan gesture to rotate objects, cycle through a collection of 3D objects, or even to scroll a 2D UI.

1. Create a quad. In your BaseScene hierarchy, right-click, select "3D Object" followed by Quad.

    ![Lesson5 Chapter2 Step2im](images/Lesson5_chapter2_step2im.PNG)

2. Reposition the quad, as appropriate. For our example, we set the x = 0, the y = 0 and the z = 1.5 away from the camera for a comfortable position from HoloLens 2.

    >[!NOTE]
    >If the quad blocks or is in front of any content from the previous lessons, be sure to move it so that it doesn’t block any of the other objects.

3. Apply a material to the quad. This material will be what we will be scrolling through with the pan gesture.

    ![Lesson5 Chapter2 Step3im](images/Lesson5_chapter2_step3im.PNG)

4. In your Projects panel, type “pan content” in the Search box. Drag that material onto the quad in your scene.

    >[!NOTE]
    >The PanContent material is not part of MRTK but included with the BaseModuleAssets asset imported in the previous lesson.

    To use the pan gesture, you will need a collider on your object. You may see the quad already has a mesh collider. However, the mesh collider is not ideal, because it is extremely thin and difficult to select. We suggest replacing the mesh collider with a box collider.

5. Right-click the mesh collider that’s on the quad from the Inspector panel. Then remove it by clicking Remove Component.

    ![Lesson5 Chapter2 Step5im](images/Lesson5_chapter2_step5im.PNG)

6. Now add the box collider by clicking Add Component and searching “box collider”. The default added box collider is still too thin, so click the Edit Collider button to edit. When it’s pressed in, you can adjust the size using the x, y and z values or the elements in the scene editor. For our example, we want to extend the box collider a little behind the quad. In the scene editor, drag the box collider from the back, outwards (see the image below). This lets the user not only use their finger, but their entire hand to scroll.

    ![Lesson5 Chapter2 Step6im](images/Lesson5_chapter2_step6im.PNG)

7. Make it interactive. Since we want to interact with the quad directly, we want to use the Near Interaction Touchable component that we used this in Lesson 4 for playing music from the Octa object. Click Add Component, search for “near interaction touchable” and select it as shown in the images below.

    ![mrlearning-base-ch5-2-step7a.png](images/mrlearning-base-ch5-2-step7a.png)

    If you see a yellow warning about bounds and/or center not matching the BoxCollider's size and/or center, click the Fix Bounds and/or Fix Center buttons to update the center and bounds values.

    ![mrlearning-base-ch5-2-step7b.png](images/mrlearning-base-ch5-2-step7b.png)

8. Add the ability to recognize the pan gesture. Click Add Component, type “hand interaction” in the search field and add the Hand Interaction Pan Zoom script component.

    ![mrlearning-base-ch5-2-step8a.png](images/mrlearning-base-ch5-2-step8a.png)

    And with that, you have a pan-enabled quad.

    As you can see, the Hand Interaction Pan Zoom script component has various settings, as an optional exercise, feel free to play around with them.

    ![mrlearning-base-ch5-2-step8b.png](images/mrlearning-base-ch5-2-step8b.png)

9. Next, we will learn how to pan 3D objects.

    In the Hierarchy, right-click the Quad object, to open the contextual popup menu, then select **3D Object** > **Cube** to add a cube to your scene.

    Ensure the Cube's **Position** is set to  _0, 0, 0_ so it's positioned neatly within the Quad. Scale the Cube down to a **Scale** of _0.1, 0.1, 0.1_.

    ![mrlearning-base-ch5-2-step9.png](images/mrlearning-base-ch5-2-step9.png)

    Duplicate the Cube three times by right-clicking the Cube, to open the contextual popup menu, and selecting **Duplicate**.

    Space the cubes out evenly. Your scene should look similar to the image below.

10. Add the MoveWithPan script to all the cubes by holding down the CTRL key while selecting each **Cube** object in the Hierarchy panel. In the Inspector panel, click Add Component, and search for and select the **Move With Pan** script to add it to all the cubes.

    ![mrlearning-base-ch5-2-step10a.png](images/mrlearning-base-ch5-2-step10a.png)

    >[!NOTE]
    >The MoveWithPan script is not part of MRTK but included with the BaseModuleAssets asset imported in the previous lesson.

    With the cubes still selected, drag the **Quad** object from the Hierarchy panel into the **Pan Input Source** field of the **Move With Pan** script component.

    ![mrlearning-base-ch5-2-step10b.png](images/mrlearning-base-ch5-2-step10b.png)

    Now, the cubes will move with your pan gesture.

    >[!TIP]
    >The MoveWithPan instance on each cube listens for the PanUpdated event sent from the HandInteractionPanZoom instance on the Quad object, that we added to the Pan Input Source field on each of the cubes, and updates the respective cube object's position accordingly.

    With the cubes still selected, move them forward along their Z axis so each cube's mesh is inside the **Quad**'s **Box Collider** by changing their **Position Z** values to _0.7_.

    ![mrlearning-base-ch5-2-step10c.png](images/mrlearning-base-ch5-2-step10c.png)

    Now, if you disable the **Quad**'s **Mesh Renderer** component by un-checking it in the Inspector panel, you will have an invisible quad where you can pan through a list of 3D objects.

    ![mrlearning-base-ch5-2-step10d.png](images/mrlearning-base-ch5-2-step10d.png)

## Eye Tracking

In this section, we will explore how to enable eye tracking in our demo. We will slowly spin our 3D menu items when they are being gazed upon with your eye gaze. We will also trigger a fun effect when the gazed-upon item is selected.

1. Ensure the MRTK profiles are properly configured for eye tracking. To do this, go to the [Getting started with eye tracking in MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_BasicSetup.html) instructions and verify that eye tracking is properly configured by reviewing the steps in the [Setting up eye tracking step-by-step](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_BasicSetup.html#setting-up-eye-tracking-step-by-step) section. Complete any remaining steps in the documentation.

    >[!NOTE]
    >If you used the DefaultHoloLens2InputSystemProfile, as instructed in the [Configure the Mixed Reality Toolkit](https://docs.microsoft.com/windows/mixed-reality/mrlearning-base-ch1#configure-the-mixed-reality-toolkit) lesson, to clone your custom MRTK configuration profile, eye tracking is enabled by default in the Unity project but you will still have to set up eye tracking simulation for the Unity editor and configure Visual Studio to allow eye tracking for the build.

    The link above provides brief instructions for:

    - Creating the Windows Mixed Reality Eye Gaze Data Provider for use in the MRTK profile
    - Enabling eye tracking in the Gaze Provider attached to the camera
    - Setting up an eye tracking simulation in the Unity editor
    - Editing the Visual Studio solution's capabilities to allow eye tracking in the built application

2. Add the Eye Tracking Target component to target objects. To allow an object to respond to eye gaze events, we'll need to add the EyeTrackingTarget component on each object that we want to interact with by using eye gaze. Add this component to each of the nine 3D objects that are part of the grid collection.

    >[!TIP]
    >You can use the Shift and/or CRTL keys to select multiple items in the Hierarchy and then bulk-add the EyeTrackingTarget component.

    ![Lesson5 Chapter3 Step2](images/Lesson5Chapter3Step2.JPG)

3. Next, we will add the EyeTrackingTutorialDemo script for some exciting interactions. For each 3D object in the grid collection, add the EyeTrackingTutorialDemo script by searching for the component in the Add Component menu.

    ![Lesson5 Chapter3 Step3](images/Lesson5Chapter3Step3.JPG)

    >[!NOTE]
    >The EyeTrackingTutorialDemo script material is not part of MRTK but included with the BaseModuleAssets asset imported in the previous lesson.

4. Spin the object while looking at the target. We want to configure our 3D objects to spin while we are looking at them. To do this, insert a new field in the While Looking At Target() section of the EyeTrackingTarget component, as shown in the image below.

    ![Lesson5 Chapter3 Step4a](images/Lesson5Chapter3Step4a.JPG)

    In the newly-created field, add the current Game Object to the empty field, and select EyeTrackingTutorialDemo>RotateTarget(), as shown in the image below. Now the 3D object is configured to spin when it is being gazed upon with eye tracking.

    ![Lesson5 Chapter3 Step4b](images/Lesson5Chapter3Step4b.JPG)

5. Add in the ability to “blip target” that is being gazed at upon select by air-tap or saying “select”. Similar to Step 4, we want to trigger EyeTrackingTutorialDemo>BlipTarget() by assigning it to the game object’s Select() field of the EyeTrackingTarget component, as shown in the figure below. With this now configured, you will notice a slight blip in the game object whenever you trigger a select action, such as air-tap or the voice command “select”.

    ![Lesson5 Chapter3 Step5](images/Lesson5Chapter3Step5.JPG)

6. Ensure eye tracking capabilities are properly configured before building to HoloLens 2. As of this writing, Unity does not yet have the ability to set the gaze input for eye tracking capabilities. Setting this capability is required for eye tracking to work in HoloLens 2. Follow the [Testing your Unity app on a HoloLens 2](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_BasicSetup.html#testing-your-unity-app-on-a-hololens-2) instructions to enable the gaze input capability.

## Congratulations

You’ve successfully added basic eye tracking capabilities to your application. These actions are only the beginning of a world of possibilities with eye tracking. This chapter also concludes Lesson 5, where we learned about advanced input functionality, such as voice commands, panning gestures, and eye tracking.

[Next Lesson: 7. Creating a Lunar Module sample application](mrlearning-base-ch6.md)
