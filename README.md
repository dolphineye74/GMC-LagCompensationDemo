# GMC Lag Compensation Demo

Lag compensation demo with a minimal "shooter" example using the General Movement Component (GMC) plugin for Unreal Engine 5.

# How does it work

The `Fire` input is detected in themovement component.
When that happens, the client start simulating the shoot, perform all the traces (pink color).

The fire event is attached to the move as the `WantsToFire` variable is bound via GMC.
When the server executes the move the player was executing when he fired, he can replay the shooting, and perform the appropriate traces too (green color).

Using this technique is efficient, as when the server is playing a move, the other players' position will be automatically rewinded at the move's timestamp.

However, when using the default settings of the GMC component, you might realize that past a certain distance between the player and target, the rewinding will no longer occur.
This happens due to the `Server Pawn Rollback Radius` property (in the Advanced settings of the GMC) being too small.
Hance, past the `Server Pawn Rollback Radius` value, the server won't rewind the potential targets.
In this demo, we set the value of `Server Pawn Rollback Radius` to the `Biped`'s `Net Cull Distance`.

# Side notes
Note that a character that does not move for 5 seconds will start to simulate movement.
This quick & dirty system was put in place to facilitate the debugging of the lag compensation when using two (or more) clients.

You may disable this feature in the `GMC` blueprint if needed.
