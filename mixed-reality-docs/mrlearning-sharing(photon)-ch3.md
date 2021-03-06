---
title: Multi-user capabilities tutorials - 3. Connecting multiple users
description: Complete this course to learn how to implement multi-user shared experiences within a HoloLens 2 application.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: mixed reality, unity, tutorial, hololens
---

# 3. Connecting multiple users

In this lesson, we learn how to connect multiple users as part of a live shared experience. By the end of this lesson, you'll be able to open the application on multiple devices and see the avatar, represented by a sphere for each person that joins.

## Objectives

* Configure PUN within your application
* Configure players
* Learn how to connect multiple users in a shared experience

## Instructions

1. In the Assets->Resources->Prefabs folder of the Project panel, drag and drop the NetworkLobby prefab into the hierarchy as shown in the image below.

    ![Module3Chapter3step1im](images/module3chapter3step1im.PNG)

2. When you expand NetworkLobby, you'll see a child object called NetworkRoom. With NetworkRoom selected, go into the Inspector panel and click Add Component. Search for PhotonView and add the component.

    ![Module3Chapter3tep2im](images/module3chapter3step2im.PNG)

3. Create a new empty game object in the hierarchy. Right-click in the hierarchy and select Empty from the Context menu. Ensure the positioning is set to x =0, y=0, z=0 and name the object, PhotonUser.

    ![Module3Chapter3step3im](images/module3chapter3step3im.PNG)

4. Click Add Component and type Generic Net Sync. Select the Generic Net Sync class. When the class appears, click the User check box to turn it on.

    ![module3chapter3updateStep4im](images/module3chapter3updateStep4im.png)

5. Click Add Component again, and type Photon View. Select the Photon View class that appears in the drop-down list.

    ![module3chapter3updateStep5im](images/module3chapter3updateStep5im.png)

6. Click the File icon for the Generic Net Sync class. Drag and drop it in the Photon View's Observed Components field.

    ![module3chapter3updateStep6im.png](images/module3chapter3updateStep6im.png)

7. Next, we create spheres to represent each person that joins a shared experience. Right-click the PhotonUser object you just created, scroll-down to "3D Object and click Sphere. This will create a sphere game object as a child of the PhotonUser object.

    ![Module3Chapter3step4im](images/module3chapter3step4im.PNG)

8. Scale the sphere down to x=0.06, y=0.06, ad z=0.06.

    ![Module3hapter3step5im](images/module3chapter3step5im.PNG)

9. Drag the PhotonUser game object into the Prefabs folder in the Project panel and then delete it from the scene. You have now created a prefab that can be used when spawning or instantiating new players in a shared experience.

    ![Module3Chapter3step6im](images/module3chapter3step6im.PNG)

    >[!NOTE]
    >Ensure that the game object has successfully copied into the Prefabs folder before deleting it from your hierarchy.

10. Create a new object in the hierarchy by following the instructions in Step 3 and name it SharedPlayground. Then, click Add Component and search for generic network manager.  Click it again to add the Generic Network Manager component. Change the position of the object to x=0, y=0, and z =0.

    ![Module3Chapter3step7im](images/module3chapter3step7im.PNG)

## Congratulations

Once all the steps above are complete and the build process is also complete, press the Play button and connect your HoloLens 2. You should see a sphere moving around as you move your head. This will be shown for any user that joins your Unity project!

[Next Lesson: 4. Sharing object movements with multiple users](mrlearning-sharing(photon)-ch4.md)
