# Unity-Scene-Notation

In Unity, scene construction can be deeply confusing. Even developers
with years of experience can become overwhelmed by the abstract complexity 
of scenes, the sheer number of moving parts, and the lack of a definitive, 
human-readable way to describe what is actually contained in a scene.
There is no standard method for clearly communicating which objects exist, 
how they are related, what was intentionally added, what was dragged in, 
and what a human must interact with in order to finish a project.
Editors obscure intent, implicit behavior hides structure, and screenshots 
fail to scale. This gap makes scenes harder to reason about, harder to lock, 
harder to document, harder to teach, and harder to rebuild after failure.
This notation exists to bridge that gap—not as shorthand, not as code, 
and not as an engine-accurate representation—but as a visual scaffolding 
and debugging tool for humans. It is designed to make scene structure legible at a 
glance, to preserve intent outside the editor, and to provide a calm, 
consistent way to think about and communicate scene composition without 
relying on screenshots, memory, or fragile tooling.

Key Visual Rules (as demonstrated)
	•	Columns matter — alignment conveys meaning.
	•	{{ }} = parent / structural GameObject
	•	[[ ]] = child GameObject
	•	:: = containment / attachment
	•	^||_____ = dragged item
	•	^:: = subordinate reference (script or asset)
	•	+ ((Component)) = multiple components on the same target
	•	Vertical position + column alignment = ownership


EXAMPLE 1 (SIMPLE)
>~ {{ROOT}}
    :: [[MANAGER]]
        :: ((Baseline))
        ^||_____((*DragInit*))
        :: ((AfterInit))

    :: [[UI]]
        :: ((UIBase))


EXAMPLE 2 (MODERATE)
>~ {{ROOT}}
    :: [[SYSTEMS]]
        :: ((Clock))
        ^||_____((*DragHotkeys*))
        :: ((Input))
            :: <<Keymap.asset>>
                ^^

    :: [[UI]]
        :: ((UIDocument))
            :: <<MainUI.uxml>>
                ^^
        ^||_____((*DragUIBinder*))
        :: ((UIController))
            :: <<MainUI.uxml>>
                ^^

    :: [[WORLD]]
        :: ((CameraLogic))

EXAMPLE 3 (COMPLEX)
>~ {{ROOT}}
    :: [[SYSTEMS]]
        :: ((State))
        :: ((Events))
            :: <<EventTable.asset>>
                ^^
        ^||_____((*DragDebugger*))
        :: ((Telemetry))
            :: <<EventTable.asset>>
                ^^

    :: [[UI]]
        :: ((UIDocument))
            :: <<Shell.uxml>>
                ^^
        :: ((ShellController))
            :: <<Shell.uxml>>
                ^^
        ^||_____((*DragOverlayTools*))

        :: [[OVERLAY]]
            :: ((OverlayLogic))
                :: <<Theme.uss>>
                    ^^

    :: [[ACTOR]]
        :: ((Movement))
        ^||_____((*DragAbilities*))
        :: ((Health))
            :: <<SharedStats.asset>>
                ^^

        :: [[MESH]]
            :: ((Renderer))
                :: <<Actor.mat>>
                    ^^

    :: [[SPAWNER]]
        :: ((SpawnLogic))
            :: <<SpawnTable.asset>>
                ^^
        ^||_____((*DragSpawnRules*))
        :: ((SpawnRules))
            :: <<SpawnTable.asset>>
                ^^


* if this notatation does not help you, dont use it!
if it does, it did its job!
:)
