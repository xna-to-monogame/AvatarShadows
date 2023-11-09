> **⚠️ Note:**
> **This sample cannot be converted to MonoGame because it focuses specifically on the Xbox 360 avatar integration provided through `Microsoft.Framework.Xna.GameServices` which is not part of MonoGame.**
> If you have an idea for how to take this sample and make it relevant for something in MonoGame, please submit discussion on the [Port Issue](https://github.com/xna-to-monogame/AvatarShadows/issues/1)

 


# Avatar Shadows Sample

This sample demonstrates how to implement planar shadows for avatar characters to increase visual quality and richness of 3D scenes involving avatars.

## Sample Overview

The sample shows a collection of sixteen animated avatars that all cast planar shadows onto the ground. Each avatar has its own animation and rotation value to show how the technique scales. Additionally the camera and light direction can both be rotated to view the shadows from various angles.

## Sample Controls

This sample uses the following gamepad controls.

| Action                 | Gamepad control  |
| ---------------------- | ---------------- |
| Rotate Camera          | Left Thumbstick  |
| Rotate Light Direction | Right Thumbstick |
| Exit the sample        | **BACK**             |

## How the Sample Works

The sample combines a few different techniques to create shadows for avatars.

The first technique leveraged is planar shadows which are a method of creating a world matrix that will flatten an object onto a given plane. We use planar shadows because we cannot create a new effect for avatars nor do we have access to the underlying geometry of the avatar. We leverage the Matrix.CreateShadow method to create the matrix that will flatten an avatar onto the ground.

The second technique is a screen-space Alpha8 format render target. We draw our flattened avatars into this render target for a few reasons. One reason is that we don’t want to draw flat, colored avatars (that’d look really odd!) and the second reason is that we want to be able to control the alpha of our shadows which the avatar rendering doesn’t support.

Lastly we use a custom effect for the ground geometry that samples from the screen-space render target in order to find out whether a specific pixel lies underneath of a shadow or not. We then darken that pixel value by multiplying the RGB channels by .5 which simulates a 50% transparent shadow in that area.

## Extending the Sample

A great next step for this technique would be to implement soft shadows, either through applying a blur pass on top of the screen-space shadow texture or by performing multiple samples and filtering in the ground pixel shader.

© 2010 Microsoft Corporation. All rights reserved.