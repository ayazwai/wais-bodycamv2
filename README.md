# WAIS-BODYCAM & DASHCAM V2
- #### Author: Ayazwai#3900 - Ayazwai
- #### Linkedin: [Ayaz Ekrem](https://www.linkedin.com/in/ayaz-ekrem-770305212/)
- #### Instagram: [Ayaz Ekrem](https://www.instagram.com/ayaz.ekremm/)
- ### Sold exclusively at [0resmon](0resmon.tebex.io) tebex.

# How to set it up

- Do not change the name of the script
- Put the script in the resources folder, do not use any folderisation.
- Prefer to start manually in server.cfg as follows.
- `wais-compatibility` script is required. Named `wais-compatibility-hudv5` in Keymaster

```
ensure wais-compatibility
#ensure other-wais-scripts
ensure wais-bodycamv2
```

- Read the `wais_records` table into SQL

- ### Framework Settings
- - You can change the framework variable to `esx` or `qbcore` depending on the type you use

- - In the ResourceName section, you should write the file name of the framework. Usually these are [es_extended, qb-core, nc-core blah blah blah]

- - If your infrastructure is new, the `NewCore` variable must be `@true`, if not, it must be `@false`. ESX Legacy and QBCore are newcore 

- - If you are using SharedEvent old core, you can find and paste the shared event from any script or from the infrastructure itself. This is important.

# How to add New Job

- Need the `name` of the job to be added
- The `vector3` axes of the coordinate where the menu will appear are required
- You have to adjust how far away the menu is visible. Example: `3.0` `@float`
- Text to be seen is required to access the menu

```
    ["police"] = {
        ["watch"] = vector3(0.0, 0.0, 0.0),
        ["distance"] = 0.0,
        ["text"] = "Menu Text",
        ["uiSettings"] = {
            ["color"] = "#", -- Color of the main color theme of the menu (base on a lighter or pastel shade of the selected color)
            ["title"] = "", -- Menu title above the categories in the right browser
            ["subtitle"] = "", -- Subtitle on the right side
            ["videoUrl"] = "", -- api or webhook to forward when recordings are stopped 
            ["backgroundColor"] = "#", -- Background color of the menu (based on a more muted shade of the selected color)
            ["badgeSettings"] = {
                ["image"] = "", -- the photo that will appear on the back when the camera is turned on
                ["darkerColor"] = "#",  --  the color of the badge that will appear on the back when the camera is turned on
                ["lighterColor"] = "#", --  the color of the badge that will appear on the back when the camera is turned on
                ["departmentName"] = "" -- the name of the department that will appear on the back when the camera is turned on
            }
        }
    },
```
# How do I change the size of the badge position

- Find the `Config.BadgeSettings` variable in Config
- Change the value of the variable `["scale"]` for size. Min: `0.1` Max: `1.0` `@float` 
- To relocate `["position"]`, just give it the value `"left"` or `"right"` as a string. @string

# How to activate screen recording

- Find the `Config.Records` variable in Config
- You can enable screen recording by setting `["enableRecord"]` to `true` in this variable.
- `["recordKey"]` This assigned key is pressed while Bodycam is active to start recording.

# How do I activate the Bodycam Prop system

- Find the variable `Config.Props` in Config
- `["attachBodycam"]` change this value to `true`. In this way, when the bodycam is used, the camera you set will appear on the person's body
- They have separate places in the clothing system for the Male character and the Female character.
- PV_COMP_HEAD = 0, "HEAD" PV_COMP_BERD = 1, "BEARD" PV_COMP_HAIR = 2, "HAIR" PV_COMP_UPPR = 3, "UPPER" PV_COMP_LOWR = 4, "LOWER" PV_COMP_HAND = 5, "HAND" PV_COMP_FEET = 6, "FEET" PV_COMP_TEEF = 7, "TEETH" PV_COMP_ACCS = 8, "ACCESSORIES" PV_COMP_TASK = 9, "TASK" PV_COMP_DECL = 10, "DECL" PV_COMP_JBIB = 11, "JBIB"
- 0: Face 1: Mask 2: Hair 3: Torso 4: Leg 5: Parachute / bag 6: Shoes 7: Accessory 8: Undershirt 9: Kevlar 10: Badge 11: Torso 2 List of Component IDs
- `["drawableId"]` is the id of the clothes.
- `["textureId"]` is the different type & texture id of the selected outfit

# How do I set up the items?

- Below you can find items and photos according to your framework or Ox inventory.
- FOR ESX:
```
INSERT INTO `items` (`name`, `label`, `weight`) VALUES
	('bodycam', 'Bodycam', 20),
	('dashcam', 'Dashcam', 20)
;
```
- FOR QB:
```
    bodycam = { name = 'bodycam', label = 'Body Cam', weight = 50, type = 'item', image = 'bodycam.png', unique = true, useable = true, shouldClose = true, combinable = nil, description = 'A bodycam for recording' },
    dashcam = { name = 'dashcam', label = 'Dash Cam', weight = 50, type = 'item', image = 'dashcam.png', unique = true, useable = true, shouldClose = true, combinable = nil, description = 'A dashcam for streaming' },
```
- FOR OX INVENTORY:
```
    ['bodycam'] = {
        label = 'Body Cam',
        weight = 20,
        stack = false,
        close = true,
        description = 'A bodycam for recording',
    },
    ['dashcam'] = {
        label = 'Dash Cam',
        weight = 20,
        stack = false,
        close = true,
        description = 'A dashcam for streaming',
    },
```
- You can find the item photos below
![bodycam](https://media.discordapp.net/attachments/1039535847361499177/1221848804291248138/bodycam.png?ex=6614125f&is=66019d5f&hm=b2f0e7694c0b401b7807345865ceaa51403ff401ce8b8d86eab3e6ea40177c6a&=&format=webp&quality=lossless&width=80&height=80)
![dashcam](https://media.discordapp.net/attachments/1039535847361499177/1221848804500836362/dashcam.png?ex=6614125f&is=66019d5f&hm=ab97ef83eb93200b904716dbab351b40398ce4584131bab375f496e37d68c5d5&=&format=webp&quality=lossless&width=80&height=80)

# Sometimes the character's head is visible in the bodycam

- Go to the `Config.CamSettings` variable in the config file
- Play with the `Y` value of the `["bodycamPositions"]` variable until it stops bothering you. For example, `-0.025` or `0.040` will do the way you want.

# How do I activate Notifications

- It will be enough to send the message and type by exporting or triggering the Framework or Notification script you are using
- Don't forget to install export according to the framework you are using

```
Config.SendNotifications = function(notif)
  local ESX = exports['es_extended']:getSharedObject()
  local QBCore = exports['qb-core']:GetCoreObject()

  --exports['okokNotify']:Alert('Title', Config.Notifications[notif].text, 2500, Config.Notifications[notif].type, false)
  --ESX.ShowNotification(Config.Notifications[notif].text)
  --QBCore.Functions.Notify(Config.Notifications[notif].text, Config.Notifications[notif].type)
```

# Are there UI's you want to disable when the Bodycam is turned on or off?

- It will be enough to put `export` or an Event Trigger inside the following functions
  
```
Config.OpenUIs = function()
    -- You can reopen closed UIs from here with export or trigger again
end

Config.CloseUIs = function()
    -- You can close UIs that you do not want to appear on the screen with export or trigger here
end
``` 
