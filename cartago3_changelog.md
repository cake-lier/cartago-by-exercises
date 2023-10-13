# CArtAgO 3.0 changelog

Or, everything you would have liked to know but were too afraid to ask about CArtAgO 3.0.

## Workspaces, workspaces, workspaces

The main change between CArtAgO 2.0 and 3.O is about workspaces. There is no more the notion of a general, root environment in
which workspaces were located. Now, there exists a root workspace in which other workspaces can be created. Then, after entering
in a workspace other workspaces can be created, and so on, creating a hierarchical structure of workspaces.

This means that the use of the annotation "artifact_name" is not working as before. In the previous CArtAgO version, being that
workspaces followed a flat structure, there were always this notion of a "current workspace". This was the default workspace if
not specified otherwise, so the workspace called "main". After joining other workspaces, or after using the
"set_current_workspace" primitive, this could be changed. When using the "artifact_name" annotation alongside an operation
invocation or a percept perception, the workspace in which the artifact was searched for was implicitly the "current" one, but
another could be specified via the "wsp" annotation.

Now, you are obliged to specify the annotation "wsp" along with the "artifact_name" one when invoking an operation on an artifact
or perceiving a percept from one. The "non-annotated" versions still work fine.

⚠️ It is a known limitation that, in fact, using only the "artifact_name" when invoking an action gives you an error, but it
works anyway even if it shouldn't. On the other side, it's correctly not working for signals and observable property updates, but
no error is returned, which it should.

❓If "non annotated" versions of operation invoking and percept perception still work fine, aren't they routed to the current
workspace? So, does it exists a notion of "current workspace" or not? Shouldn't then artifacts searched by name between the ones
that an agent created, such as when the "artifact_id" annotation is used?

Before, a "current_wsp(WorkspaceId, WorkspaceName, NodeId)" was a belief that could be present into the belief base of an agent,
surely it was there containing the pieces of information about the default workspace. Being that the notion of current workspace
was abolished, this kind of belief can't exist no more. Only "joinedWsp(WorkspaceId, WorkspaceName, NodeId)" beliefs do exist,
informing an agent about all the workspaces that has currently joined. For the same reason, the "set_current_workspace" operation
was available to change the current workspace, which is now not available anymore.

The creation of a new workspace now follows the hierarchical nature of the workspace themselves. If a workspace is created while
inside another, it will became part of it.

⚠️ It is a known limitation that the "quitWorkspace" primitive does not seem to quit workspaces, because when a new one is
created, it is done inside the workspace just left and it is accessible only from there.

❓ It needs to be absolutely clear what the semantics of the "joinWorkspace" and "quitWorkspace" operation must be, even changing
their signature to allow a better control of where workspaces need to be inserted in the hierarchy.
