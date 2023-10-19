# CArtAgO 3.0 changelog

Or, everything you would have liked to know but were too afraid to ask about CArtAgO 3.0.

## Workspaces, workspaces, workspaces

The main change between CArtAgO 2.0 and 3.0 is about workspaces. There is no more the notion of a general, root environment in
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
no error is returned, which it should. Moreover, using both the "artifact_name" and "wsp" annotations doesn't do anything, even
if it should.

❓If "non annotated" versions of operation invoking and percept perception still work fine, aren't they routed to the current
workspace? So, does it exists a notion of "current workspace" or not? Shouldn't then artifacts searched by name between the ones
in the current workspace, as the "non annotated" versions do? This can be seen in the [tests for the new workspace model](https://github.com/CArtAgO-lang/cartago/blob/440cd41c1810ceef6a627477c461776b3200236b/src/test/jaca/test/tester_agent_new_wsp_model.asl#L44).

## Keeping the current workspace in the flow

Before, there was at least one "current_wsp(WorkspaceId, WorkspaceName, NodeId)" belief into the belief base of an agent,
containing the pieces of information about the default workspace. Being that the notion of current workspace was abolished, this
kind of belief can't exist no more. Only "joinedWsp(WorkspaceId, WorkspaceName, NodeId)" beliefs do exist, informing an agent
about all the workspaces that has currently joined. It exists a new internal operation, called "current_wsps", that returns a list
with all the ids of the workspaces that an agent has currently joined.

For the same reason, the "set_current_workspace" operation was available to change the current workspace, which is now not
available anymore. The "joinWorkspace" took its place, allowing to reset the current workspace without throwing any error if the
workspace was already joined.

The creation of a new workspace now follows the hierarchical nature of the workspace themselves. If a workspace is created by name
or, in other words, relatively to the current workspace, it will became part of it. The workspaces can now be referenced by path,
either relative to the current one or absolute from the root one, while creating and joining them.

⚠️ It is a known limitation that the "quitWorkspace" primitive does not seem to do anything besides removing the corresponding
"joinedWsp" belief in the agent that called it and maybe from some internal data structure. With a "joinWorkspace", the agents can
still set the quit workspace as the current one, use the artifacts in it and not being notified about their joining, as they never
left that workspace at all.

❓ It needs to be absolutely clear what the semantics of the "joinWorkspace" and "quitWorkspace" operations must be. Is it right
that we can join a workspace multiple times, even just for resetting the "current workspace"? What should the "quitWorkspace" do:
going back to the parent workspace, quit the workspace but not resetting the current one, limiting to block the percepts to be
perceived and the actions to be performed, going back to the root one...? These primitives can also be removed altogether or their
signature changed to be more apt to the new workspace structure.

## Linking workspaces

The new workspace structure allows also to link workspaces. In a filesystem a "link" is just a reference to a file reachable from
another path inside said filesystem. An alternative path to the file, if you will. In CArtAgO 3.0, the concept is the same. A new
"linkWorkspace" primitive has been introduced which takes two or three parameters. The first one is the "linking" workspace, the
one from which the link starts to reach the one used as a second parameter, the "linked" workspace. After the operation, the
linked workspace will appear as a child of the linking workspace, even if this is not the case. The third, additional parameter,
is to be used for renaming the linked workspace when accessed from the linking one, to change its name just for the linking one.
The workspace to be linked needs to be specified with an absolute path if it is a local one, with a URL if it is a remote one.
An alternative to the "linkWorkspace" primitive is the "mountWorkspace" one, which links a remote workspace as a local workspace
while specifying the absolute path of where to mount, or link, the remote one. In a single parameter is then specified the linking
workspace and the name of the remote one for the linked workspace.

## The remote side of the workspaces

Both the "joinWorkspace" and the "linkWorkspace" have a remote counterpart, respectively called "joinRemoteWorkspace" and
"linkRemoteWorkspace". In CArtAgO 3.0 they are not more powerful than the first ones, they just limit themselves to work with
remote workspaces, a thing that their "non-remote" counterparts can do all the same.

⚠️ It is a known limitation that the "joinRemoteWorkspace" is not working as in CArtAgO 2.0: specifying the name of the workspace
to join and the address of the node on which that workspace is located, made by a host and a port, is not enough anymore.
Specifying a URL after the path argument, either absolute or relative, of the workspace to join doesn't work either.

❓ The existence of these "remote" primitives is up to debate: do we want to be transparent to distribution or not? Is joining a
remote workspace just a matter of specifying a URI? And if so, what URIs can be supported? Can joining a local workspace using its
path be assimilated to specifying only a part of a URI, where the rest of it is left implicit? Do workspaces have multiple URIs
then?

⚠️ It is a known limitation that the "default" protocol for connection, "Java RMI", appears not to be working because superseded
by a new, "web" one based on the "HTTP" protocol.

❓ This is very apt with the idea of assigning URIs to workspaces to identify and join them. But should we support other
web-standardized protocols, such as MQTT, CoAP, Websocket, WebSub, et cetera? Shouldn't be URIs independent from the connection
protocol we want to use, or can they serve a double purpose as in Yggdrasil?

⚠️ It is a known limitation The "joinWorkspace" primitive works if used for joining a remote workspaces but suspends indefinitely
the agent's plan. The remote node shows no problem whatsoever, while the local one waits for something to happen that never
comes.
